---
title: Technical Preview 1604 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1604 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1785880af8c7d0d106abfe3eea8ecd390f6ce6b1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074461"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Configuration Manager için Technical Preview 1604 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1604 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz.      Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).  

 Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a>Iş için Windows Mağazası 'ndan toplu satın alınan uygulamaları yönetme  
 [İş Için Windows Mağazası](https://www.microsoft.com/business-store) , kuruluşunuz için tek tek veya toplu olarak uygulamaları bulabileceğiniz ve satın alabileceğiniz yerdir. Mağazayı Configuration Manager bağlayarak, toplu satın alınan uygulamaları Configuration Manager konsolundan yönetebilirsiniz, örneğin:  

-   Satın alınan uygulama listesini Configuration Manager ile eşitlenebilir  

-   Eşitlenen uygulamalar Configuration Manager konsolunda görünür ve bunları diğer uygulamalar gibi dağıtabilirsiniz  

-   Kaç tane lisansın kullanılabilir olduğunu ve Configuration Manager konsolunda kaç tane kullanıldığını izleyebilirsiniz  

### <a name="try-it-out"></a>Deneyin!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Senaryo 1: Iş için Windows Mağazası eşitlemesini ayarlama  

1.  Azure Active Directory, Configuration Manager bir "Web uygulaması ve/veya Web API" yönetim aracı olarak kaydettirin. Bu, daha sonra ihtiyacınız olacak bir istemci KIMLIĞI sağlar.  

    1.  **Active Directory** düğümünde [https://manage.windowsazure.com](https://manage.windowsazure.com), Azure Active Directory seçin ve ardından **uygulamalar** > **Ekle**' ye tıklayın.  

    2.  **Kuruluşumun geliştirmekte olduğu bir uygulama ekle**' ye tıklayın.  

    3.  Uygulama için bir ad girin, **Web uygulaması** ve/veya **Web API 'si**seçin ve ardından ileri okuna tıklayın.  

    4.  **Oturum açma URL** 'Si ve **uygulama kimliği URI**'si için aynı URL 'yi girin.  URL herhangi bir şey olabilir ve gerçek bir adrese çözülmesi gerekmez. Örneğin, **https://&lt;\>EtkiAlanınız/SCCM**adlı bir giriş yapabilirsiniz.  

    5.  Sihirbazı tamamlayın.  

2.  Azure Active Directory, kayıtlı yönetim aracı için bir istemci anahtarı oluşturun.  

    1.  Yeni oluşturduğunuz uygulamayı vurgulayın ve **Yapılandır**' a tıklayın.  

    2.  **Anahtarlar**' ın altında, listeden bir süre seçin ve **Kaydet**' e tıklayın.  Bu, yeni bir istemci anahtarı oluşturur.  Iş için Windows Mağazası Configuration Manager için başarıyla eklendi, bu sayfadan uzaklaşmayın.  

3.  Iş için Windows Mağazası 'nda, Configuration Manager depolama yönetimi aracı olarak yapılandırın.  

    1.  İstenirse [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) açın ve oturum açın.  

    2.  Gerekirse kullanım koşullarını kabul edin.  

    3.  **Yönetim Araçları**' nın altında, **Yönetim Aracı Ekle**' ye tıklayın.  

    4.  **Aracı ada göre ara** alanına daha önce AAD'de oluşturduğunuz uygulamanın adını yazın ve **Ekle**’ye tıklayın.  

    5.  Yeni içeri aktardığınız uygulamanın yanındaki **Etkinleştir** ' e tıklayın.  

    6.  Çevrimdışı lisanslı uygulamaların satın alınacaksa izin vermek istiyorsanız **çevrimdışı lisanslı uygulamaları göster** sihirbazında **Evet** ' e tıklayın.  

4.  Iş için Windows Mağazası 'ndan en az bir uygulama satın alın.  

5.  Configuration Manager konsolunun **Yönetim** çalışma alanında, **Cloud Services**' i genişletin ve **iş için Windows Mağazası**' na tıklayın.  

6.  **Giriş** sekmesinde, **Oluştur** grubunda, **Iş için Windows Mağazası hesabı ekle**' ye tıklayın.  

7.  Kiracı KIMLIĞINIZ, istemci kimliğiniz ve istemci anahtarınızı Azure Active Directory ' den ekleyip Sihirbazı doldurun.  

8.  İşiniz bittiğinde, Configuration Manager konsolundaki **iş Için Windows Mağazası hesapları** listesinde yapılandırdığınız hesabı görürsünüz.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Senaryo 2: Iş için Windows Mağazası 'nda çevrimdışı lisanslı bir uygulama Configuration Manager uygulama oluşturma ve dağıtma  

1.  Configuration Manager konsolunun **yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **Mağaza uygulamaları için lisans bilgileri**' ne tıklayın.  

2.  **Satın alınan iş Için Windows Mağazası uygulamaları** listesi, mağazadan eşitlenen uygulamaların listesini gösterir. Dağıtmak istediğiniz uygulamayı seçin, sonra **giriş** sekmesinde, **Oluştur** grubunda, **uygulama oluştur**' a tıklayın.  

3.  Iş için Windows Mağazası uygulamasını içeren bir Configuration Manager uygulaması oluşturulur. Daha sonra bu uygulamayı diğer Configuration Manager uygulamaları gibi dağıtabilir ve izleyebilirsiniz.  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a>İş için Microsoft Passport yönetimi geliştirmeleri  
 Artık Configuration Manager istemcisi tarafından yönetilen etki alanına katılmış Windows 10 cihazlarına Passport for Work ilkeleri dağıtabilirsiniz.  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a>İstemcilerin yeni bir yazılım güncelleştirme noktasına geçiş yapma seçeneği  
 1604 Technical Preview sürümünde, etkin yazılım güncelleştirme noktasıyla ilgili sorunlar olduğunda Configuration Manager istemcilerinin yeni bir yazılım güncelleştirme noktasına geçiş yapma seçeneğini etkinleştirebilirsiniz. Bu seçenek için, birincil sitede birden çok yazılım güncelleştirme noktanız olması gerekir. Bu seçeneği bir cihaz koleksiyonunda etkinleştirir ve etkinleştirildikten sonra, istemci etkin yazılım güncelleştirme noktasına başarıyla bağlanamazsa, koleksiyondaki istemciler bir sonraki taramada başka bir yazılım güncelleştirme noktası arar. WSUS Yapılandırma ayarlarınıza (güncelleştirme sınıflandırmaları, ürünler vb.) bağlı olarak, yeni bir yazılım güncelleştirme noktasına geçiş, ek ağ trafiği oluşturacaktır. Bu nedenle, bu seçeneği yalnızca gerekli olduğunda kullanmalısınız.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Yazılım güncelleştirme noktası değiştirme seçeneğini etkinleştirmek için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyumluluk> Genel Bakış > Cihaz Koleksiyonları**’na gidin.  

2.  **Giriş** sekmesindeki **Koleksiyon** grubunda **İstemci Bildirimi**’ne ve ardından **Sonraki Yazılım Güncelleştirme Noktasına Geç**’e tıklayın.  

> [!NOTE]  
>  Bu seçenek yalnızca birden çok yazılım güncelleştirme noktası bulunan sitelerde kullanılabilir.  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a>İstemci önbellek ayarlarını ve istemci eş önbelleğini yönetmek için istemci ayarları  
 Technical Preview sürüm 1604, bir istemcinin önbelleğinin kullanımını etkileyen iki yeni cihaz istemci ayarı sunar. Her ikisi de tek başına kullanılabilir, ancak istemci ayarları için aynı özellik sayfasında yapılandırılır ve uzak konumlardaki istemcileriniz için içerik dağıtımını yönetmenize yardımcı olmak için birleştirilir.  

-   İlk olarak **Istemci eş önbelleği**, istemcilerin diğer istemcilerle doğrudan yerel önbelleğiyle içerik paylaşmasını sağlamak için yerleşik bir Configuration Manager çözümüdür. Eş önbellek istemcilerinin içerik paylaşması için, aynı sınır grubunun üyesi olmaları gerekir. Eş önbellek, köşeli ayraç Nchcache gibi diğer çözümlerin kullanımını değiştirmez, bunun yerine dağıtım noktaları gibi geleneksel içerik dağıtım çözümlerini uzatmak için daha fazla seçenek sunmak üzere yan yana çalışmaktadır.  

     Bir koleksiyona eş önbelleği etkinleştiren istemci ayarlarını dağıttıktan sonra, bu koleksiyonun üyeleri, kendi sınır grubundaki diğer istemciler için bir eş içerik kaynağı olarak hareket edebilir.  Eş içerik kaynağı olarak çalışan istemci, yönetim noktasına önbelleğe aldığı kullanılabilir içeriğin bir listesini gönderir. Daha sonra, bu sınır grubundaki bir sonraki istemci bu içeriği istediğinde, eş önbellek kaynağı, hızlı olacak şekilde yapılandırılmış tüm dağıtım noktalarıyla birlikte olası bir içerik kaynağı olarak sunulur. İstemci bu Birleşik içerik kaynağı havuzundan rastgele bir içerik kaynağı seçer. İstemciler yalnızca sınır grubunda hızlı dağıtım noktaları veya eş önbellek kaynağı bulunmadığı zaman yavaş olacak şekilde yapılandırılmış bir dağıtım noktasından içerik arar.  

-   İkinci yeni ayar, istemcilerde **önbelleğin boyutunu yönetmenizi** sağlar. Önbelleği, en büyük boyutu megabayt cinsinden, istemciler sürücü alanının yüzdesi cinsinden en büyük boyuta sahip olacak şekilde ayarlayabilirsiniz.  İstemci, ilk olarak ulaşılan ayarı zorlar.  

İstemci eş önbelleğinin kullanımını anlamanıza yardımcı olması için **Istemci veri kaynakları** panosunu görüntüleyebilirsiniz. Konsolunda, **Istemci veri kaynakları > > Istemci durumunu izleme**bölümüne gidin. Buraya, panoya uygulanacak bir zaman aralığı seçebilirsiniz. Ardından, ekranda, bilgilerini görüntülemek istediğiniz sınır grubunu veya paketini seçebilirsiniz. Bilgileri görüntülerken, farklı içerik veya ilke kaynakları hakkında daha fazla ayrıntı görmek için farenizi yüzey üzerine getirin.  

 Her bir sınır grubu için istemci veri kaynaklarının özetlemesini görüntülemek için yeni bir rapor, **Istemci veri kaynakları-özetleme**' yi de kullanabilirsiniz.   
**Eş önbellek kullanma gereksinimleri:**  

-   Sitenizi her istemcideki önbellek klasörüne **tam denetime** sahip bir **ağ erişim hesabı** ile yapılandırmanız gerekir. Bu, varsayılan olarak **%windir%\ccmcache** 'dir  

-   İstemciler yalnızca aynı sınır grubuna üye olduklarında eş önbellek kullanarak içerik aktarabilir.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Istemci eş önbelleği istemci ayarlarını yapılandırmak için  

1.  Her iki ayar de istemci ayarlarının aynı sayfasında yapılandırılır. Configuration Manager konsolunda **yönetim > Istemci ayarları**' na gidin ve ardından kullanmak istediğiniz cihaz istemci ayarları nesnesini açın. Varsayılan Istemci ayarları nesnesini de değiştirebilirsiniz.  

2.  Kullanılabilir ayarlar listesinden **Istemci önbellek ayarları**' nı seçin.  

3.  Önbelleğin boyutunu yönetmek için, **istemci önbellek boyutunu Yapılandır** ' ı **Evet**olarak ayarlayın. Daha sonra, maksimum önbellek boyutunu hem megabayt hem de istemciler sürücü alanının yüzdesi olarak yapılandırabilirsiniz.  

4.  İstemcilerin istemci eş önbelleğine katılmasını sağlamak için **tam işletim sisteminde Configuration Manager Istemcisinin** **Evet**' e eşit içerik paylaşmasını etkinleştir ayarını yapın. Daha sonra, HTTP veya HTTPS gibi istemciler tarafından kullanılan bağlantı noktalarını yapılandırabilirsiniz.  

### <a name="try-it-out"></a>Deneyin!  
 Aşağıdaki görevleri tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için bu konunun en üstündeki geri bildirim bilgilerini kullanın:  

1.  İstemci ayarlarını değiştirerek istemci önbelleği için yeni bir boyut belirtin ve sonra bu ayarı bir istemcide onaylayın.  

2.  Eş Önbelleği kullanmak üzere birden fazla istemciyi yapılandırmak için istemci ayarlarını kullanın  

3.  Bir veya daha fazla istemcinin bu içeriği eş önbellek kullanarak başka bir istemciden alması için istemcilere içerik dağıtın.  Yeni panoyu görüntüleyerek kullanılan içerik kaynağını doğrulayabilirsiniz.  

    > [!NOTE]  
    >  Bu görevi Teknik Önizleme ve tek bir dağıtım noktasıyla gerçekleştirmek için, dağıtım noktasını tüm istemcilerinizin ağ konumu için yavaş olacak şekilde yapılandırın. Ardından, içeriği tek bir istemciye dağıtın.  İstemci, içeriği aldıktan sonra, istemcinin konumundan yavaş olduğu kabul edilen dağıtım noktasını kullanmadan önce içerik kaynağı olarak kullanmak üzere yerel eşleri bulması gereken ek istemcilere içeriği dağıtabilirsiniz.  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a>Bir KSP olarak Iş için Passport desteği  
 Configuration Manager, bir parolayı, akıllı kartı ya da sanal akıllı kartı değiştirmek için Active Directory veya Azure Active Directory hesabı kullanan alternatif bir oturum açma yöntemi olan İş için Microsoft Passport tümleştirmenize olanak tanır.  
Passport oturum açmak için parola yerine bir kullanıcı hareketi kullanmanıza imkan tanır. Kullanıcı hareketi basit bir PIN, Windows Hello gibi bir biyometrik kimlik doğrulaması ya da parmak izi okuyucu gibi harici bir cihaz olabilir.  

-   Kullanıcıların oturum açmak için hangi hareketleri kullanabileceğini ve kullanabileceğini denetlemek ve PIN karmaşıklığı gereksinimlerini yapılandırmak için Configuration Manager kullanabilirsiniz.  

-   Kimlik doğrulama sertifikalarını İş için Passport anahtar depolama sağlayıcısına (KSP) depolayabilirsiniz.  

Bir Kullanıcı bir Passport PIN 'ı oluşturduğunda, Windows Configuration Manager dinlediği bir bildirim gönderir.  Bu, Configuration Manager kullanıcıların bir Passport PIN 'ı oluşturduğunu hızlı bir şekilde haberdar etmesine olanak tanır. Configuration Manager, Passport bir sertifika profilinde anahtar depolama sağlayıcısı olarak kullanılıyorsa, bu kullanıcılara yeni sertifikalar de verebilir.  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a>Şirket içi Cihaz Sistem Durumu Kanıtlama  
 Windows 10 cihazları için sistem durumu kanıtlama artık şirket içi altyapıyı kullanarak iletişim kuracak şekilde yapılandırılabilir.  Yöneticiler, raporlamanın bulut veya şirket içi kaynaklar aracılığıyla yapılıp yapılmadığını belirtebilir.  Sistem durumu kanıtlama raporlaması için **Şirket içi** seçilirse, hizmet IÇIN bir URI belirtilebilir. Bu, internet erişimi olmayan istemci bilgisayarların sistem durumu kanıtlama kullanarak cihazları etkinleştirme ve yönetme özelliğini kullanmasını sağlar.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Şirket içi cihazlarda sistem durumu kanıtlamasını etkinleştirme  

1.  Configuration Manager konsolunda, **Yönetim** > **genel bakış** > **istemci ayarları**' na gidin ve şirket **içi sistem durumu kanıtlama hizmetini kullan** ' ı **Evet**olarak ayarlayın.  

2.  **Şirket içi Sistem Durumu Kanıtlama Hizmeti URL'si**belirtin ve **Tamam**’a tıklayın.  

Denemek için, istemci Aracısı ayarlarını kullanarak şirket içi sistem durumu kanıtlama hizmetini yapılandırın.  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a>Android cihazlar için SmartLock ayarı  
 **Android ve Samsung KNOX** yapılandırma öğesine, **akıllı kilit ve diğer güven aracılarına izin veren** yeni bir ayar, uyumlu Android cihazlarda Smartlock özelliğini denetlemenize olanak tanır. Güven aracıları olarak da bilinen bu telefon özelliği, cihaz belirli bir Bluetooth cihazına bağlı olmak ya da bir NFC etiketinin yakınında olmak gibi güvenilir bir konumda bulunduğunda, cihaz kilit ekranı parolasının devre dışı bırakılmasına veya atlanmasına olanak sağlar. Son kullanıcıların SmartLock yapılandırmasını engellemek için bu ayarı kullanabilirsiniz.  
