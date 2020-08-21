---
title: SMS Sağlayıcı planı
titleSuffix: Configuration Manager
description: Configuration Manager 'da SMS Sağlayıcısı site sistemi rolü hakkında bilgi edinin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c83d0da07474c8b078ee226d249b73f00562e0f5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700172"
---
# <a name="plan-for-the-sms-provider"></a>SMS Sağlayıcı planı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager yönetmek için, **SMS sağlayıcısı**örneğine bağlanan bir Configuration Manager konsolunu kullanırsınız. Varsayılan olarak, bir merkezi yönetim sitesi veya birincil site yüklediğinizde bir SMS Sağlayıcısı site sunucusuna yüklenir.

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> SMS sağlayıcı hakkında  

SMS sağlayıcı, bir sitedeki Configuration Manager veritabanına **okuma** ve **yazma** erişimi atayan bir Windows Yönetim Araçları (WMI) sağlayıcıdır.  

- Her merkezi yönetim sitesi ve birincil site en az bir SMS Sağlayıcısı gerektirir. Gerektiğinde ek sağlayıcılar yükleyebilirsiniz.  

- **SMS yöneticileri** GÜVENLIK grubu SMS Sağlayıcısına erişim sağlar. Configuration Manager, bu grubu site sunucusunda ve SMS sağlayıcısı 'nın bir örneğini yüklediğiniz her bilgisayarda otomatik olarak oluşturur. Daha fazla bilgi için bkz. [SMS yöneticileri](accounts.md#sms-admins).  

- İkincil siteler SMS sağlayıcı rolünü desteklemez.  

Configuration Manager yönetici kullanıcılar, veritabanında depolanan bilgilere erişmek için bir SMS sağlayıcısı kullanır. Bunu yapmak için, Yöneticiler Configuration Manager konsolunu, Kaynak Gezgini, araçları ve özel betikleri kullanabilir. SMS sağlayıcısı Configuration Manager istemcilerle etkileşime girmez. Bir Configuration Manager konsolu bir siteye bağlandığında, kullanılacak SMS sağlayıcısının bir örneğini bulmak için site sunucusundaki WMI 'yı sorgular.  

SMS sağlayıcısı Configuration Manager güvenliği zorlamaya yardımcı olur. Yalnızca konsol kullanıcısının görüntüleme yetkisine sahip olduğu bilgileri döndürür.  

SMS sağlayıcısı, **Yönetim hizmeti**olarak adlandırılan https üzerinden API birlikte çalışabilirlik erişimi de sağlar. Bu REST API, siteden bilgilere erişmek için özel bir Web hizmetinin yerine kullanılabilir. Daha fazla bilgi için bkz. [Yönetim hizmeti nedir?](../../../develop/adminservice/overview.md).

> [!IMPORTANT]  
> Bir site için SMS sağlayıcısı 'nın her örneği çevrimdışıyken Configuration Manager konsolları siteye bağlanamaz.  

SMS sağlayıcısının nasıl yönetileceği hakkında daha fazla bilgi için bkz. [SMS sağlayıcısını yönetme](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).  

## <a name="installation-prerequisites"></a>Yükleme önkoşulları  

SMS Sağlayıcıyı desteklemek için hedef sunucunun aşağıdaki önkoşulları karşılaması gerekir:  

- Site sunucusu ve site veritabanı site sistemleriyle aynı etki alanında  

- Farklı bir siteden site sistem rolü olamaz  

- Herhangi bir siteden SMS sağlayıcısı zaten bulunamaz  

- Desteklenen bir işletim sistemi sürümünü çalıştırma  

- Windows ADK bileşenlerini desteklemek için en az 650 MB boş disk alanı. Windows ADK ve SMS sağlayıcısı hakkında daha fazla bilgi için bkz. [OS dağıtım gereksinimleri](#BKMK_WAIKforSMSProv).  

- [Yönetim hizmeti](../../../develop/adminservice/overview.md) REST API için:

  - .NET 4,5 veya üzeri

  - Windows Server rolünü etkinleştirme **Web sunucusu (IIS)**

    > [!Note]  
    > Her SMS sağlayıcısı, bir sertifika gerektiren Yönetim hizmetini yüklemeye çalışır. Bu hizmetin, bu sertifikayı HTTPS bağlantı noktası 443 ' e bağlamak için IIS 'e bağımlılığı vardır. [GELIŞMIŞ http](enhanced-http.md)'yi etkinleştirirseniz site, bu sertifikayı IIS API 'leri kullanarak bağlar. Siteniz PKI kullanıyorsa, SMS sağlayıcısı üzerinde IIS 'de bir PKI sertifikasını el ile bağlamanız gerekir. Sürüm 2002 ' den başlayarak, site otomatik olarak otomatik olarak imzalanan sertifikayı kullanır.

## <a name="locations"></a><a name="bkmk_location"></a> Yerlerini  

Bir sitesi yüklediğinizde, site için ilk SMS Sağlayıcıyı otomatik olarak yüklersiniz. SMS Sağlayıcısı için aşağıdaki desteklenen konumlardan birini belirtebilirsiniz:  

- Site sunucusu  

- Site veritabanı sunucusu  

- [Yükleme önkoşullarını](#installation-prerequisites) karşılayan başka bir sunucu  

Bir site için her SMS sağlayıcısının konumlarını görüntülemek için:

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Listeden istediğiniz siteyi seçin ve ardından şeritte **Özellikler** ' i seçin.  

3. Site **özelliklerinin** **genel** sekmesinde, **SMS sağlayıcısı konum** alanını görüntüleyin.  

Her bir SMS Sağlayıcısı, birden çok istekten eş zamanlı bağlantıyı destekler. Bu bağlantılardaki tek sınırlamalar, Windows için kullanılabilen sunucu bağlantısı sayısı ve bağlantı isteklerine hizmet vermek için sunucudaki kullanılabilir kaynaklardır.  

Bir siteyi yükledikten sonra site sunucusunda Configuration Manager kurulumunu yeniden çalıştırabilirsiniz. Mevcut bir SMS sağlayıcısının yerini değiştirmek veya o sitede ek SMS Sağlayıcılarını yüklemek için kurulum 'u kullanın. Bir bilgisayara yalnızca bir SMS sağlayıcısı yükler. Bir bilgisayar, birden fazla siteden SMS sağlayıcısı barındırmıyor.  

### <a name="choosing-a-location"></a>Konum seçme

Aşağıdaki bölümlerde, her desteklenen konuma bir SMS sağlayıcısı yüklemenin avantajları ve dezavantajları açıklanır:  

#### <a name="configuration-manager-site-server"></a>Configuration Manager site sunucusu

- **Üstünlü**  

  - SMS sağlayıcısı, site veritabanı bilgisayarının sistem kaynaklarını kullanmaz.  

  - Bu konum, site sunucusu veya site veritabanı bilgisayarından başka bir bilgisayarda bulunan SMS Sağlayıcısından daha iyi performans sağlar.  

- **Olumsuz**  

  - SMS Sağlayıcısı, site sunucu işlemlerine ayrılabilecek sistem ve ağ kaynaklarını kullanır.  

#### <a name="sql-server-that-hosts-the-site-database"></a>Site veritabanını barındıran SQL Server

- **Üstünlü**  

  - SMS sağlayıcısı, site sunucusunda sistem kaynaklarını kullanmaz.  

  - Yeterli sunucu kaynakları mevcutsa bu konum üç konumdan en iyi performansı verir.  

- **Olumsuz**  

  - SMS Sağlayıcısı, site veritabanı işlemlerine ayrılabilecek sistem ve ağ kaynaklarını kullanır.  

  - Site veritabanı bir SQL Server kümelenmiş örneğinde barındırılıyorsa, bu konumu kullanamazsınız.  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Site sunucusu veya site veritabanı sunucusu dışında bir bilgisayar

- **Üstünlü**  

  - SMS sağlayıcısı, site sunucusu veya site veritabanı sistem kaynaklarını kullanmaz.  

  - Bu tür konum, bağlantılar için yüksek kullanılabilirlik sağlamak üzere ek SMS Sağlayıcıları dağıtmanızı sağlar.  

- **Olumsuz**  

  - SMS sağlayıcısı performansı azalabilir. Bu davranışın nedeni, site sunucusu ve site veritabanı bilgisayarıyla koordine etmek için gereken ek ağ etkinliğidir.  

  - Bu sunucu her zaman site veritabanı sunucusu ve Configuration Manager konsolunun yüklü olduğu tüm bilgisayarlar için erişilebilir olmalıdır.  

  - Bu konum, aksi takdirde diğer hizmetlere ayrılan sistem kaynaklarını kullanabilir.  

## <a name="authentication"></a><a name="bkmk_auth"></a> Yetkilendirmesi

<!--1357013-->
Sürüm 1810 ' den başlayarak, yöneticilerin Configuration Manager sitelere erişmesi için en düşük kimlik doğrulama düzeyini belirtebilirsiniz. Bu özellik, yöneticilerin Windows 'da gerekli düzeyiyle oturum açmasını zorlar. SMS sağlayıcısına erişen tüm bileşenler için geçerlidir. Örneğin, Configuration Manager konsolu, SDK yöntemleri ve Windows PowerShell cmdlet 'leri.

### <a name="configure-authentication"></a>Kimlik doğrulamasını yapılandırma

Bu ayarı yapılandırmak için ilk olarak Windows 'da amaçlanan kimlik doğrulama düzeyiyle oturum açın.

> [!Important]  
> Bu yapılandırma, hiyerarşi genelinde bir ayardır. Bu ayarı değiştirmeden önce, tüm Configuration Manager yöneticilerinin Windows 'da gerekli kimlik doğrulama düzeyiyle oturum açmasını sağlayın.

Bu ayarı yapılandırmak için aşağıdaki adımları kullanın:

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Şeritte **Hiyerarşi ayarları** ' nı seçin.  

3. **Kimlik doğrulama** sekmesine geçin. istenen [kimlik doğrulama düzeyini](#authentication-levels)seçin ve **Tamam**' ı seçin.  

    - Yalnızca gerekli olduğunda, belirli kullanıcıları veya grupları dışlamak için **Ekle** ' yi seçin. Daha fazla bilgi için bkz. [Dışlamalar](#exclusions).  

### <a name="authentication-levels"></a>Kimlik doğrulama düzeyleri

Aşağıdaki düzeyler mevcuttur:

- **Windows kimlik doğrulaması**: Active Directory etki alanı kimlik bilgileriyle kimlik doğrulaması gerektir. Bu ayar önceki davranış ve geçerli varsayılan ayardır. Siteyi güncelleştirdiğinizde kimlik doğrulama düzeyinde hiçbir değişiklik yapılmaz.  

- **Sertifika kimlik doğrulaması**: GÜVENILEN bir PKI sertifika yetkilisi tarafından verilen geçerli bir sertifika ile kimlik doğrulaması gerektir. Bu sertifikayı Configuration Manager ' de yapılandırmayın. Configuration Manager, yöneticinin PKI kullanarak Windows 'da oturum açmanızı gerektirir.  

- **İş Için Windows Hello kimlik doğrulaması**: bir cihaza bağlı olan ve Biyometri veya PIN kullanan güçlü iki öğeli kimlik doğrulama ile kimlik doğrulaması gerektir. Daha fazla bilgi için bkz. [iş Için Windows Hello](/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="exclusions"></a>Dışlamalar

Hiyerarşi ayarlarının **kimlik doğrulama** sekmesinden, bazı kullanıcıları veya grupları da hariç tutabilir. Bu seçeneği gelişigüzel bir şekilde kullanın. Örneğin, belirli kullanıcılar Configuration Manager konsoluna erişim gerektirdiğinde, ancak gerekli düzeyde Windows 'da kimlik doğrulayamıyorum. Ayrıca, bir sistem hesabı bağlamında çalışan Otomasyon veya hizmetler için de gerekli olabilir.

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> SMS sağlayıcı dilleri hakkında  

SMS sağlayıcısı, yüklediğiniz sunucunun görüntüleme dilinden bağımsız olarak çalışır.  

Bir yönetici kullanıcı veya Configuration Manager işlemi, SMS sağlayıcısını kullanarak veri istediğinde, bu verileri istek yapan bilgisayarın işletim sistemi diliyle eşleşen bir biçimde döndürmeye çalışır.

Dili eşleştirme girişimi, dolaylı bir şekilde yapılır. SMS sağlayıcısı bilgileri bir dilden diğerine çevirmez. Configuration Manager konsolunda görüntülenmek üzere veri döndürdüğünde, verilerin görüntüleme dili nesne ve depolama alanının kaynağına bağlıdır.  

Configuration Manager veritabanındaki bir nesne için veri depoladığında, kullanılabilir diller aşağıdaki etkenlere bağlıdır:  

- Configuration Manager birden çok dil için destek kullanarak oluşturduğu nesneleri depolar. Kurulumu çalıştırdığınızda site için yapılandırdığınız dilleri kullanarak nesneyi site veritabanında depolar. Configuration Manager konsolu bu nesneleri, istenen bilgisayarın görüntüleme dilinde, bu dil nesne için kullanılabilir olduğunda görüntüler. Konsol, nesneyi istenen bilgisayarın görüntüleme dilinde görüntüleyemiyorum, nesneyi varsayılan dilde (Ingilizce) görüntüler.  

- Configuration Manager, bir yönetici kullanıcının, nesneyi oluşturmak için kullanılan dili kullanarak oluşturduğu nesneleri depolar. Bu nesneler Configuration Manager konsolunda aynı dilde görüntülenir. SMS sağlayıcısı bu dosyaları çeviremez ve birden çok dil seçeneklerine sahip değildir.  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> Birden çok SMS sağlayıcısı kullanma  

Site yüklemeyi tamamladıktan sonra, site için ek SMS Sağlayıcıları yükleyebilirsiniz. Ek SMS Sağlayıcılarını yüklemek için site sunucusunda Configuration Manager kurulumunu çalıştırın.

Aşağıdakilerden biri doğruysa ek SMS sağlayıcıları yüklemeyi göz önünde bulundurun:  

- Birçok yönetici kullanıcının Configuration Manager konsolunu kullanması ve bir siteye aynı anda bağlanması gerekir.  

- Configuration Manager SDK veya diğer ürünleri kullanarak SMS sağlayıcısına sık yapılan çağrılar ortaya çıkabilir.  

- SMS sağlayıcısının yüksek kullanılabilirliği için bir iş gereksinimidir.  

Bir sitede birden çok SMS sağlayıcısı yüklediğinizde ve bir bağlantı isteği yapıldığında, site her yeni bağlantı isteğini yüklü bir SMS sağlayıcısını kullanacak şekilde rastgele atar. Belirli bir bağlantı oturumuyla kullanılacak SMS sağlayıcısını belirtemezsiniz.  

> [!NOTE]  
> Her SMS sağlayıcısı konumunun avantajlarını ve dezavantajlarını göz önünde bulundurun. Daha fazla bilgi için bkz. [konumlar](#bkmk_location). Her yeni bağlantı için hangi SMS sağlayıcısının kullanıldığını denetleyemiyorum bilgilerle bu hususları dengeleyin.  

Bir Configuration Manager konsolunu bir siteye ilk kez bağladığınızda, bağlantı site sunucusundaki WMI 'yı sorgular. Bu sorgu, konsolunun kullandığı SMS sağlayıcısının bir örneğini tanımlar. SMS sağlayıcısının bu belirli örneği, oturum sona erene kadar Konsolu tarafından kullanımda kalır. Oturum sona erdiğinde, SMS sağlayıcı sunucusu ağda kullanılamadığından, Konsolu siteye yeniden bağladığınızda, ilk sorgu yinelenir. Site, kullanılamayan aynı SMS sağlayıcısı örneğini atar. Bu davranış gerçekleşirse, site kullanılabilir bir SMS sağlayıcısı döndürdüğünden konsolu yeniden bağlamayı deneyin.  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> SMS sağlayıcı ad alanı hakkında  

Configuration Manager WMI şeması, SMS sağlayıcısı 'nın yapısını tanımlar. Şema ad alanları, SMS sağlayıcı şeması içindeki Configuration Manager verilerinin konumunu anlatır. Aşağıdaki tabloda SMS sağlayıcısı tarafından kullanılan bazı yaygın ad alanları yer almaktadır:  

|Ad Alanı|Açıklama|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|Configuration Manager konsolu, Kaynak Gezgini, Configuration Manager araçları ve betikler tarafından yaygın olarak kullanılan SMS sağlayıcısı.|  
|`Root\SMS\SMS_ProviderLocation`|Bir site için SMS sağlayıcısı bilgisayarlarının konumu.|  
|`Root\CIMv2`|Donanım ve yazılım envanteri sırasında WMI ad alanı bilgileri için Envantere kaydedilen konum.|  
|`Root\CCM`|İstemci yapılandırma ilkeleri ve istemci verileri Configuration Manager.|  
|`Root\CIMv2\SMS`|Envanter istemci aracısının topladığı Envanter raporlama sınıflarının konumu. İstemciler, bilgisayar ilkesi değerlendirmesi sırasında bu ayarları derler. Bu ayarlar, bilgisayarın istemci ayarları yapılandırmasını temel alır.|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a> İşletim sistemi dağıtım gereksinimleri

SMS sağlayıcısı 'nın bir örneğini yüklediğiniz bilgisayar desteklenen bir Windows ADK sürümü gerektirir.  

Bu gereksinim hakkında daha fazla bilgi için bkz. [işletim sistemi dağıtımı Için altyapı gereksinimleri](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10) ve [Windows 10 desteği](../configs/support-for-windows-10.md).  

İşletim sistemi dağıtımlarını yönetirken, Windows ADK, SMS sağlayıcısı 'nın çeşitli görevleri tamamlamasını sağlar, örneğin:  

- WIM dosyası ayrıntılarını görüntüle  

- Var olan önyükleme yansımalarına sürücü dosyaları ekle  

- Önyükleme ISO dosyaları oluştur  

Windows ADK yüklemesi, SMS Sağlayıcısı’nı yükleyen her bilgisayarda 650 MB’ye kadar boş disk alanı gerektirebilir. Bu yüksek disk alanı gereksinimi, Configuration Manager Windows PE önyükleme görüntülerini yüklemesi için gereklidir.  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a> Yönetim hizmeti

<!--3607711, fka 1321523-->

SMS sağlayıcısı, **Yönetim hizmeti**olarak ADLANDıRıLAN bir https OData BAĞLANTıSı üzerinden API birlikte çalışabilirlik erişimi sağlar. Bu REST API, siteden bilgilere erişmek için özel bir Web hizmetinin yerine kullanılabilir.

Daha fazla bilgi için bkz. [Yönetim hizmeti nedir?](../../../develop/adminservice/overview.md)