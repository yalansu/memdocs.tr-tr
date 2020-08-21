---
title: Technical Preview 1605 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1605 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 1836a4c7d08547405dad08d7e60eb108d0dfd00f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695724"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Configuration Manager için Technical Preview 1605 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1605 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz.      Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).  

 **Bu teknik önizlemede bilinen sorunlar:**  

- Technical Preview 1605 ile, bir yönetim noktasının yüklendikten sonra özelliklerini güncelleştirirseniz, konsolu kapatmaya zorlayan bir konsol hatası görebilirsiniz.  Bu durumda, yönetim noktasını kaldırabilir ve ardından istenen ayarları kullanarak yönetim noktasını yeniden yükleyebilirsiniz. Alternatif olarak, Technical Preview 1605 ' i yüklemeden önce yönetim noktasını değiştirebilirsiniz.  

- Technical Preview 1604 ile Iş için Windows Mağazası özelliğini kullandığınızda ve ardından Technical Preview 1605 ' ye yükseltirseniz, artık ekleme verilerini görüntüleyemezsiniz. Diğer tüm işlevsellik çalışmaya devam eder. Technical Preview 1604 ile eklendi, Technical Preview 1605 ' i yükledikten sonra eklendi olarak kalır ve başka bir eylem gerçekleştirmeniz gerekir.  

  **Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a> Windows 10 cihazları için uygulama başına VPN  
 Intune ile Configuration Manager kullanılarak yönetilen Windows 10 cihazlarında, Configuration Manager Yönetici Konsolu aracılığıyla yapılandırdığınız bir VPN bağlantısını otomatik olarak açan uygulamaların bir listesini ekleyebilirsiniz. VPN trafiğini bu uygulamalarla kısıtlama seçeneğiniz vardır veya VPN bağlantısı üzerinden tüm trafiğe izin vermeyi sürdürebilirsiniz.  

 **Gereksinimler**:  

-   Intune ile Configuration Manager  

-   En az bir cihaza dağıtılan bir Windows 10 VPN profili  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a> Yazılım güncelleştirmelerini yüklemek görev sırası geliştirmeleri  
 Yazılım güncelleştirmelerini yüklemek görev sırasında aşağıdaki geliştirmeler yapılmıştır:  

-   Yazılım güncelleştirmelerini yükler görev dizisi adımı sırasında yazılım güncelleştirmeleri taramasıyla ilgili zaman aşımını denetlemenize olanak tanımak için, SMSTSSoftwareUpdateScanTimeout yeni bir görev dizisi değişkeni vardır. Varsayılan değer 30 dakikadır.  

-   Günlüğe kaydetme geliştirmeleri vardı. Smsts. log günlük dosyası, yazılım güncelleştirmeleri yükleme işlemi sırasında sorunları gidermenize yardımcı olacak diğer günlük dosyalarına başvuran yeni günlük girişleri içerir.  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a> Yakalama için ConfigMgr Istemcisini hazırla görev dizisi adımındaki geliştirmeler  
 ConfigMgr Istemcisini hazırla adımı yalnızca anahtar bilgilerini kaldırmak yerine Configuration Manager istemcisini tamamen kaldırır. Görev dizisi yakalanan işletim sistemi görüntüsünü dağıttığında, her seferinde yeni bir Configuration Manager istemci yükler.  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a> Gerekli uygulama dağıtımları için yetkisiz kullanım süresi  
 Bazı durumlarda, kullanıcıların gerekli uygulama dağıtımlarını yapılandırdığınız son tarihlerden daha fazla zaman yüklemesine izin vermek isteyebilirsiniz. Örneğin, bir son kullanıcı tatilden yeni döndürülürse, süresi geçmiş uygulama dağıtımları yüklenirken uzun süredir beklemek zorunda kalabilir. Ancak, uygulamayı istedikleri zaman hemen yükleyebilir.  

 Bu sorunu çözmeye yardımcı olmak için artık Configuration Manager istemci ayarlarını bir koleksiyona dağıtarak bir **yetkisiz kullanım süresi** tanımlayabilirsiniz.  

 Yetkisiz kullanım süresini yapılandırmak için aşağıdaki işlemleri gerçekleştirin:  

1. İstemci ayarları ' nın **Bilgisayar Aracısı** sayfasında, **dağıtım son tarihi (saat) sonra** , **1** ila **120** saat arasında bir değere sahip zorlama için yeni özellik yetkisiz kullanım süresini yapılandırın.  

2. Yeni bir uygulama dağıtımında veya var olan bir dağıtımın özelliklerinde, **zamanlama** sayfasında, istemci ayarlarında tanımlanan yetkisiz kullanım süresine kadar, **kullanıcı tercihlerine göre bu dağıtımın uygulanmasını geciktir**onay kutusunu seçin.  

    Bu onay kutusunun seçili olduğu ve istemci ayarını dağıttığınız cihazlara hedeflenen tüm dağıtımlar yetkisiz kullanım süresini kullanır.  

   Bu sürümde, yapılandırdığınız yetkisiz kullanım süresi istemci cihazlar tarafından kullanılmaz. Bir yetkisiz kullanım süresi yapılandırır ve onay kutusunu seçerseniz, uygulama, kullanıcının son tarihten sonra yapılandırdığı ilk iş dışı penceresine yüklenir.  

   Yazılım güncelleştirmeleri dağıtım sihirbazına, otomatik dağıtım kuralları sihirbazına ve özellikler sayfalarına benzer seçenekler eklenmiştir. Ancak bunlar şu anda bu teknik önizlemede uygulanmıyor.  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a> Uzak cihaz eylemleri için yeni deneyim  
 Configuration Manager konsolundan uzak cihaz eylemlerini gerçekleştirmeye yönelik deneyim geliştirilmiştir.  
Artık **varlıklar ve uyum** çalışma alanından erişilen **uzak cihaz eylemleri** menüsünde **devre dışı bırakma/Temizleme**, **sıfırlama geçiş kodu**, **Uzaktan kilitleme**ve **atlama Etkinleştirme Kilidi** gibi genel eylemler bulunabilir.  

 ![Yeni uzak cihaz eylemleri ekran görüntüsü](media/New-Remote-Device-Actions.png)  

 Bu işlemlerin her biri için durumu aşağıdaki yerlerde bulabilirsiniz:  

- Ayrıntılar bölmesinde, **cihazlar** düğümünden bir cihaz seçtiğinizde.  

- Bir cihazın **Özellikler** sayfasında.  

- **Cihazlar** düğümünün ana sayfasında (tüm sütunlar varsayılan olarak görünür olmayabilir).  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a> Iş için Windows Mağazası uygulamaları  
 [İş Için Windows Mağazası](https://www.microsoft.com/business-store) , kuruluşunuz için tek tek veya toplu olarak uygulamaları bulabileceğiniz ve satın alabileceğiniz yerdir. Mağazayı Configuration Manager bağlayarak, toplu satın alınan uygulamaları Configuration Manager konsolundan yönetebilirsiniz, örneğin:  

- Satın alınan uygulama listesini Configuration Manager ile eşitlenebilir  

- Eşitlenen uygulamalar Configuration Manager konsolunda görünür ve bunları diğer uygulamalar gibi dağıtabilirsiniz  

- Configuration Manager, her 24 saatte bir uygulama lisanslama bilgilerini mağazadan indirir ve bunu Configuration Manager konsolunda inceleyebilirsiniz  

  1604 Technical Preview sürümünde, uygulamaları Configuration Manager konsolundaki Iş için Windows Mağazası 'ndan eşitleyebilir ve görüntüleyebilirsiniz. Bu sürümde, eşitlenmiş mağaza uygulamalarından Configuration Manager uygulamalar oluşturma ve dağıtma özelliği ekledik.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Iş için Windows Mağazası eşitlemesini ayarlama  

1.  Azure Active Directory, Configuration Manager bir "Web uygulaması ve/veya Web API" yönetim aracı olarak kaydettirin. Bu, daha sonra ihtiyacınız olacak bir istemci KIMLIĞI sağlar.  

    1.  Active Directory düğümünde [https://manage.windowsazure.com](https://manage.windowsazure.com) , Azure Active Directory seçin ve ardından **uygulamalar**  >  **Ekle**' ye tıklayın.  

    2.  **Kuruluşumun geliştirmekte olduğu bir uygulama ekle**' ye tıklayın.  

    3.  Uygulama için bir ad girin, **Web uygulaması** ve/veya **Web API 'si**seçin ve ardından **İleri** okuna tıklayın.  

    4.  **Oturum açma URL** 'Si ve **uygulama kimliği URI**'si için aynı URL 'yi girin. URL herhangi bir şey olabilir ve gerçek bir adrese çözülmesi gerekmez. Örneğin, **https:// &lt; EtkiAlanınız>/SCCM**girebilirsiniz.  

    5.  Sihirbazı tamamlayın.  

2.  Azure Active Directory, kayıtlı yönetim aracı için bir istemci anahtarı oluşturun.  

    1.  Yeni oluşturduğunuz uygulamayı vurgulayın ve **Yapılandır**' a tıklayın.  

    2.  **Anahtarlar**' ın altında, listeden bir süre seçin ve **Kaydet**' e tıklayın. Bu, yeni bir istemci anahtarı oluşturur. Iş için Windows Mağazası Configuration Manager için başarıyla eklendi, bu sayfadan uzaklaşmayın.  

3.  Iş için Windows Mağazası 'nda, Configuration Manager depolama yönetimi aracı olarak yapılandırın.  

    1.  [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools)İstenirse açın ve oturum açın.  

    2.  Gerekirse kullanım koşullarını kabul edin.  

    3.  **Yönetim Araçları**' nın altında, **Yönetim Aracı Ekle**' ye tıklayın.  

    4.  **Aracı ada göre ara** alanına daha önce AAD'de oluşturduğunuz uygulamanın adını yazın ve **Ekle**’ye tıklayın.  

    5.  Yeni içeri aktardığınız uygulamanın yanındaki **Etkinleştir** ' e tıklayın.  

    6.  Çevrimdışı lisanslı uygulamaların satın alınacaksa izin vermek istiyorsanız **çevrimdışı lisanslı uygulamaları göster** sihirbazında **Evet** ' e tıklayın.  

4.  Iş için Windows Mağazası 'ndan en az bir uygulama satın alın.  

5.  Configuration Manager konsolunun **Yönetim** çalışma alanında, **Cloud Services**' i genişletin ve **iş için Windows Mağazası** ' na tıklayın.  

6.  **Giriş** sekmesinde, **Oluştur** grubunda, **Iş için Windows Mağazası hesabı ekle**' ye tıklayın.  

7.  Kiracı KIMLIĞINIZ, istemci kimliğiniz ve istemci anahtarınızı Azure Active Directory ' den ekleyip Sihirbazı doldurun.  

8.  İşiniz bittiğinde, Configuration Manager konsolundaki **iş Için Windows Mağazası hesapları** listesinde yapılandırdığınız hesabı görürsünüz.  

### <a name="try-it-out"></a>Deneyin!  
 Aşağıdaki görevi tamamlamayı deneyin ve Microsoft Connect sitesinin [Configuration Manager geri bildirim programı](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sayfasındaki geri bildirim formumuzu kullanarak nasıl çalıştığını bize bilgilendirin:  

 Iş için çevrimdışı lisanslı bir uygulama için Windows Mağazası 'ndan bir Configuration Manager uygulaması oluşturun ve dağıtın.  

1. Configuration Manager konsolunun **yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **Mağaza uygulamaları için lisans bilgileri**' ne tıklayın.  

2. Dağıtmak istediğiniz uygulamayı seçin, sonra **giriş** sekmesinde, **Oluştur** grubunda, **uygulama oluştur**' a tıklayın.  

   Iş için Windows Mağazası uygulamasını içeren bir Configuration Manager uygulaması oluşturulur. Daha sonra bu uygulamayı diğer Configuration Manager uygulamaları gibi dağıtabilir ve izleyebilirsiniz.  

> [!IMPORTANT]  
>  Çevrimdışı lisanslı bir uygulamadan tek bir dağıtım türüyle Configuration Manager bir uygulama oluşturduğunuzda, bu, MDM tarafından yönetilen ve ayrıca Configuration Manager istemcisiyle yönetilen cihazlara dağıtılabilir. Bir uygulamayı birden çok dağıtım türüyle dağıtmaya çalışırsanız, yükleme başarısız olur.  
>   
>  Şu anda Configuration Manager ile çevrimiçi lisanslanmış uygulamalar dağıtamazsınız.  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a> Toplu satın alınan uygulamalar için genel geliştirmeler  

-   Bu sürümde, Iş için Windows Mağazası 'ndan toplu satın alınan uygulamalar ve iOS Uygulama Mağazası, **Mağaza uygulamaları Için lisans bilgileri**olan aynı görünüme birleştirildi.  

-   İOS toplu satın alınan uygulamalar için Apple Volume Purchase Program sekmesi, uygulama oluşturma Sihirbazı 'ndaki **IOS tarayıcısı Için uygulama paketi** iletişim kutusundan kaldırılmıştır. İOS için toplu satın alınan bir uygulama oluşturmak üzere şu adımları kullanın:  

    1.  1.  Configuration Manager konsolunun **yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **Mağaza uygulamaları için lisans bilgileri**' ne tıklayın.  

    2.  2.  Dağıtmak istediğiniz uygulamayı seçin, sonra **giriş** sekmesinde, **Oluştur** grubunda, **uygulama oluştur**' a tıklayın.  

-   Configuration Manager konsolundaki toplu satın alınan uygulamalara yönelik bir Apple VPP belirtecini almak ve yüklemek için kullandığınız konum değişmiştir. Bunu artık **Admin** **Cloud Services**  >  **Apple Volume Purchase program belirteçleri** düğümü altındaki yönetici çalışma alanında yapabilirsiniz.  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a> Kurumsal veri koruma (EDP)  
 Kurumsal veri koruma (EDP) ilkelerinizi dağıtmanıza olanak sağlayan yapılandırma öğeleri oluşturabilirsiniz, bu da korumalı uygulamalarınızı, EDP koruma düzeyinizi ve ağ üzerinde kurumsal verilerin nasıl bulunacağını seçmenizi sağlar. EDP hakkında daha fazla bilgi için aşağıdaki konulara bakın:  

- [Windows Information Protection (WıP) kullanarak kurumsal verilerinizi koruma](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Configuration Manager kullanarak bir Windows Information Protection (WıP) ilkesi oluşturma ve dağıtma](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a> Son kullanıcılar Şirket Portalı uygulama yükleyebilir  
 Şirket içi MDM, Configuration Manager sürüm 1511 ' de tanıtılmıştır. Önceki sürümlerde, uygulamaları MDM ile yönetilen Windows 10 cihazlarına, şirket içi MDM tarafından yönetilen cihazlar için **gereken** yüklemede dağıtım amacını dağıtabilirsiniz.  

 Bu sürümde, artık şirket içi MDM ile yönetilen Windows 10 bilgisayarlarının kullanıcıları için **kullanılabilir** dağıtım amacına sahip uygulamaları dağıtabilirsiniz ve kullanıcılar artık bu uygulamaları şirket portalı yükleyebilir.
Bu teknik önizlemede, Şirket Portalı 15 dakikadan uzun bir süre açık ise, Son Kullanıcı bir hata mesajı görür. Sorunu geçici olarak çözmek için Şirket Portalı yeniden başlatın.  

### <a name="before-you-start"></a>Başlamadan önce  

#### <a name="server-prerequisites"></a>Sunucu önkoşulları  

-   .NET 4,5 veya üzeri (yeniden başlatma gerektirir)  

-   Yapılandırma betiği için PowerShell 3,0 (yeniden başlatma gerektirir)  

#### <a name="client-prerequisites"></a>İstemci önkoşulları  

-   Windows 10 Masaüstü 1511 (OS derleme 10586,218) veya üzeri  

#### <a name="general-prerequisites"></a>Genel önkoşullar  

-   [Şirket ıçı MDM Için hazırlık adımlarını](../../mdm/plan-design/plan-on-premises-mdm.md) tamamladığınızdan ve [cihazlarınızı](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)kaydettiniz.  

-   Şirket Portalı kullanırken en iyi uygulama yüklemesi deneyimi için Configuration Manager Microsoft Intune etkin bir bağlantısına sahip olduğundan emin olun.  

-   Toplu kayıt seçeneğini belirlerseniz, bu senaryoyu denemeden önce kayıtlı cihaz için Kullanıcı cihaz benzeşimini yapılandırın.  

### <a name="configuration-steps"></a>Yapılandırma adımları  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Uygulama Kataloğu rollerini yükleyip mobil cihaz yönetimi desteğini etkinleştir  

1.  Uygulama Kataloğu Web hizmeti ve Web sitesi rolleri ekleme  

    1.  **Https modunu** ve **mobil cihazların bu uygulama Kataloğu Web hizmeti noktasını kullanmasına izin ver** seçeneğini belirleyin.  

    2.  Bu teknik önizlemede sınırlamalar:  

        -   Mobil cihazların bağlanmasına izin ver seçeneğini seçmeden önce mevcut Uygulama Kataloğu rollerini kaldırmanız gerekir.  

        -   Uygulama Kataloğu rollerinin yalnızca bir kümesi olduğundan ve rollerin, kayıt noktası ve kayıt proxy noktası rolleriyle aynı site sisteminde birlikte bulunduğundan emin olun.  

2.  Aşağıdaki bileşenlerin Configuration Manager konsolundaki bileşen durumu düğümünden çalıştığını doğrulayın:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Sınırları Yapılandır  
 Yalnızca intranet dağıtım noktaları için gerekli sınırları yapılandırın.  

> [!NOTE]  
>  Mobil cihaz yönetimi için şu anda yalnızca IPv4 aralığı sınırları destekleniyor.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Şirket Portalı uygulamayı ve yapılandırmayı dağıtma  

1. Şirket Portalı dağıtımı ve yapılandırmayı hazırlamak için Technical Preview ile birlikte gelen yapılandırma betiğini kullanın:  

   1. Yükseltilmiş bir PowerShell komut penceresi açın.  

   2. **Set-executionPolicy RemoteSigned** Çalıştır  

   3. ** &lt; SCCM yükleme dizini \> \CD.exe \ Test\smssetup\tools\mdm** Run klasöründen **.\ConfigurationScript.ps1**  

      Yapılandırma betiği şunları yapar:  

   4. Aynı klasörde **CompanyPortalOnPremisesMDM. appx** kullanarak Windows uygulama paketi dağıtım türü ile bir Configuration Manager uygulaması oluşturur.  

   5. Şirket Portalı yapılandıran bir yapılandırma öğesi ve yapılandırma temeli oluşturur.  

   6. Yapılandırma temelini ve uygulamayı dağıtır ve uygulamayı tüm dağıtım noktalarına ekler.  

   > [!NOTE]
   >  Uygulama Kataloğu rolleri birincil siteyle birlikte konumlandırmadıysanız, aşağıdaki işlemleri gerçekleştirin:  
   > 
   > - **Varlıklar ve uyum** çalışma alanında **Onpremmdm Portal Configuration CI-Server URL 'leri** yapılandırma öğesini bulun  
   >   -   **Uyumluluk kuralları** değerini, uygulama kataloğu rollerinin bulunduğu site sisteminin tam etki alanı adıyla değiştirin.  

2. Şirket Portalı uygulaması ve yapılandırması her ikisi de dağıtıldıktan sonra, Configuration Manager konsolunun **dağıtımlar** 'ı kullanarak belirtilen cihaz için uygulama ve yapılandırma temelinin uyumlu olduğunu doğrulayın. Şirket Portalı, cihazdaki Başlat menüsünde **Şirket portalı (Technical Preview)** olarak gösterilir.  

### <a name="try-it-out"></a>Deneyin!  
 Aşağıdaki görevleri tamamlamayı deneyin ve Microsoft Connect sitesinin [Configuration Manager geri bildirim programı](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sayfasındaki geri bildirim formumuzu kullanarak nasıl çalıştığını bize bilgilendirin:  

1.  Desteklenen Dağıtım türlerine sahip birkaç uygulamayı **kullanılabilir**dağıtım amacına sahip bir kullanıcı koleksiyonuna dağıtın. Bu teknik önizleme için yönetici onayı gerektiren uygulamalar desteklenmez ve Şirket Portalı gösterilmez.  

2.  Kullanıcılar daha sonra Şirket Portalı uygulamalara gözatabilir ve yükleyebilir.  

     Şirket Portalı açtıktan sonra, oturum açmak için kullanıcının Active Directory kimlik bilgilerini ( **Configuration Manager** user@domain veya etki alanı \ Kullanıcı biçiminde) belirten Configuration Manager adlı bir kimlik doğrulama iletişim kutusu görüntülenir.  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a> Yazılım Merkezi 'nde güncelleştirmeler ve Işletim sistemleri için yeni sekmeler  
 Bu sürümde, Yazılım Merkezi uygulamasının yerleşimini geliştirmek için aşağıdaki değişiklikler yapılmıştır:  

-   **Uygulamalar** sekmesi, **güncelleştirmeler**, **Işletim sistemleri** (daha önce **Filtreler** listesinde bulunan) ve **uygulamalar**için üç ayrı sekmeye bölünür.  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a> Sunucu grubu hizmeti  
 Configuration Manager sürüm 1511 ' de Technical Preview, koleksiyondaki tüm cihazların bir sunucu grubu üzerinde oluşturulduğu bir koleksiyon oluşturma özelliğini içeriyordu. Ardından, sunucu grubuna yazılım güncelleştirmelerini dağıtırken kullanılacak sunucu grubu ayarlarını yapılandırabilir, belirli bir zamanda güncellenen bilgisayarların yüzdesini denetleyebilir ve dağıtım öncesi ve dağıtım sonrası PowerShell betiklerini özel eylemleri çalıştıracak şekilde yapılandırabilirsiniz.  

 Configuration Manager, sürüm 1605 için teknik önizleme, sunucu grubundaki bilgisayarları tanımladığınız belirli bir sırada güncelleştirme özelliği ekler, sunucu grubundaki bilgisayarların durumunu görüntülemek için Gelişmiş izleme ekler ve istemciler yazılım güncelleştirmelerini yükleyemazken ve diğer istemcilerin yazılım güncelleştirmelerini yüklemesini engelliyorsa faydalı olan dağıtım kilitlerini temizleyebilme olanağı sağlar.  

### <a name="try-it-out"></a>Deneyin!  
 Aşağıdaki görevleri tamamlamayı deneyin ve Microsoft Connect sitesinin [Configuration Manager geri bildirim programı](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sayfasındaki geri bildirim formumuzu kullanarak nasıl çalıştığını bize bilgilendirin:  

-   Sunucu grubunu temsil eden bir koleksiyon oluşturbiliyorum. Bu test için, toplama üyelik kurallarınızı bu koleksiyonda 2 makineye sahip olacak şekilde yapılandırabilirsiniz.   

-   Sunucu grubundaki bilgisayarların, yazılım güncelleştirmelerini koleksiyonun sunucu grubu ayarlarına göre belirli bir sırada yüklemesini belirtebilirsiniz. Dağıtım öncesi ve dağıtım sonrası betikleri belirtmek için yordamdaki örnek betikleri kullanın.  

-   Bu koleksiyona bir yazılım güncelleştirmesi dağıtabiliyorum. C:\Temp ' teki start.txt ve end.txt dosyalarını (örnek betiklerden oluşturulan) gözden geçirin ve sunucu grubundaki bilgisayarlarda dağıtımın başlangıç ve bitiş zamanlarını doğrulayın. Daha fazla bilgi için UpdatesDeployment. log dosyasını gözden geçirin.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Bir sunucu grubu için koleksiyon oluşturmak için  

1.  Sunucu grubundaki bilgisayarları içeren [bir cihaz koleksiyonu oluşturun](../clients/manage/collections/create-collections.md) .  

2.  **Varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları**' na tıklayın, sunucu grubundaki bilgisayarları içeren koleksiyona sağ tıklayın ve ardından **Özellikler**' e tıklayın.  

3.  **Genel** sekmesinde, **tüm cihazlar aynı sunucu grubunun bir parçası olan**' ı seçin ve ardından **Ayarlar**' a tıklayın.  

4.  **Sunucu grubu ayarları** sayfasında, aşağıdaki ayarlardan birini belirtin:  

    -   **Makinelerin bir yüzdesinin aynı anda güncelleştirilmesine Izin ver**: herhangi bir anda yalnızca belirli bir istemci yüzdesinin güncelleştirileceğini belirtir. Örneğin, koleksiyonda 10 istemci varsa ve koleksiyon aynı anda istemcilerin %30 ' u güncelleştirmek üzere yapılandırılmışsa, belirli bir zamanda yalnızca 3 istemci yazılım güncelleştirmelerini yükler.  

    -   **Aynı anda bir dizi makinenin güncelleştirilmesine Izin ver**: herhangi bir anda yalnızca belirli sayıda istemcinin güncelleştirileceğini belirtir.  

    -   **Bakım sırasını belirtin**: koleksiyondaki istemcilerin yapılandırdığınız sırada bir seferde güncelleştirileceğini belirtir. İstemci, yazılım güncelleştirmelerini yalnızca listede bundan sonraki istemci, yazılım güncelleştirmelerini yüklemeyi tamamladığında yükler.  

5.  Dağıtım öncesi (düğüm boşaltma) betiği mi yoksa dağıtım sonrası (düğüm özgeçmişi) betiği mi kullanacağınızı belirtin.  

    > [!TIP]  
    >  Aşağıda, geçerli saati bir metin dosyasına yazan dağıtım öncesi ve dağıtım sonrası betikleri için test etmek üzere kullanabileceğiniz örnekler verilmiştir:  
    >   
    >  **Dağıtım öncesi**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Dağıtım sonrası**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Yazılım güncelleştirmelerini sunucu grubuna dağıtmak ve durumu izlemek için  

1.  [Yazılım güncelleştirmelerini](../../sum/deploy-use/deploy-software-updates.md) sunucu grubu koleksiyonuna dağıtın.  

2.  [Yazılım güncelleştirme dağıtımını izleyin](../../sum/deploy-use/monitor-software-updates.md). Yazılım güncelleştirmeleri dağıtımı için standart izleme görünümlerine ek olarak, istemci yazılım güncelleştirmelerini yüklemeyi beklerken yeni bir durum açıklaması görüntülenir. Bu yeni durum için **Kilit bekleniyor** görüntülenir.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Bir sunucu grubundaki bilgisayarlar için dağıtım kilitlerini temizlemek için  

1.  **Varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları**' na tıklayın ve dağıtım kilitlerini temizlemek için koleksiyona tıklayın.  

2.  **Giriş** sekmesinde, **dağıtım** grubunda, **sunucu grubu dağıtım kilitlerini temizle**' ye tıklayın. İstemciler yazılım güncelleştirmelerini yükleyemediyse ve diğer istemcilerin yazılım güncelleştirmelerini yüklemesini engelliyorsa, dağıtım kilitleri el ile temizlenebilir.  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a> Microsoft Defender Gelişmiş tehdit koruması hizmeti desteği  
 Microsoft Defender Gelişmiş tehdit koruması (ATP), kuruluşların ağlarında gelişmiş saldırıları algılamasına, araştırmasına ve yanıt vermesine yardımcı olacak bir hizmettir. Microsoft Defender ATP daha önce Windows Defender ATP olarak bilinirdi. [Microsoft Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection)hakkında daha fazla bilgi edinin. Configuration Manager, yönetilen Windows 10 yıldönümü Edition istemci cihazlarını eklemenize ve izlemenize yardımcı olabilir.  

### <a name="try-it-now"></a>Hemen deneyin!  
 Aşağıdaki görevleri tamamlamayı deneyin ve Microsoft Connect sitesinin [Configuration Manager geri bildirim programı](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sayfasındaki geri bildirim formumuzu kullanarak nasıl çalıştığını bize bilgilendirin:  

- Cihazları Microsoft Defender Gelişmiş tehdit koruması (ATP) çevrimiçi hizmetine ekleme  

- Yönetilen cihazlara Microsoft Defender ATP dağıtımını izleme  

  **Önkoşullar**  

- Microsoft Defender Gelişmiş tehdit koruması çevrimiçi hizmetine abonelik  

- Windows 10, yıldönümü sürümü (derleme 14328 ve üzeri) çalıştıran istemciler  

- İstemci ekleme yapılandırma dosyası oluşturma  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Ekleme yapılandırma dosyası oluşturma  

  1.  Microsoft Defender ATP çevrimiçi hizmetinde oturum açma  

  2.  **İstemci görsel taslak** menü öğesine tıklayın  

  3.  **Configuration Manager** öğesini seçin ve **paketi indir**' e tıklayın.  

  4.  Sıkıştırılmış arşiv (. zip) dosyasını indirin ve içerikleri ayıklayın.  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Microsoft Defender ATP için cihazları ekleme  

1. Configuration Manager konsolunda, **varlıklar ve uyum**  >  **genel bakış**  >  **Endpoint Protection**  >  **Windows Defender ATP ilkeleri** ' ne gidin ve **Windows Defender ATP İlkesi Oluştur**' a tıklayın. Microsoft Defender ATP Ilkesi Sihirbazı açılır.  

2. Microsoft Defender ATP ilkesi için **ad** ve **Açıklama** yazın ve **ekleme**' yi seçin. İleri'ye tıklayın.  

3. Kuruluşunuzun Microsoft Defender ATP bulut hizmeti kiracısı tarafından sunulan yapılandırma dosyasına **gidin** . **İleri**’ye tıklayın.  

4. Analiz edilmek üzere yönetilen cihazlardan toplanan ve paylaşılan dosya örneklerini belirtin.  

   - **Hiçbiri** – analiz için örnek dosya toplanmadı  

   - **Taşınabilir yürütülebilir dosyalar** – program dosyaları (. exe), dinamik kitaplık bağlantısı (. dll) dosyaları, yazı tipi dosyaları ve Side yararlanılabilen benzer dosyalar gibi dosyalar, analiz için toplanır ve paylaştırılır  

     **İleri**’ye tıklayın.  

5. Özeti gözden geçirin ve Sihirbazı doldurun.  

6. Şimdi **Dağıt**' a tıklayarak MICROSOFT Defender ATP ilkesini yönetilen istemci bilgisayarlara dağıtabilirsiniz.  

##### <a name="monitor-microsoft-defender-atp"></a>Microsoft Defender ATP 'yi izleme  

1.  Configuration Manager konsolunda, **izleme**  >  **genel bakış**  >  **güvenlik** ' e gidin ve ardından **Windows Defender ATP**' ye tıklayın.  

2.  Microsoft Defender Gelişmiş tehdit koruması panosunu gözden geçirin.  

    -   **Windows Defender Aracısı dağıtım durumu** : etkin MICROSOFT Defender ATP ilkesi eklendi uygun yönetilen istemci bilgisayarlarının sayısı ve yüzdesi  

    -   **Windows Defender atp Aracı durumu** – MICROSOFT Defender ATP Aracısı için durum bildiren bilgisayar istemcilerinin yüzdesi  

        -   **Sağlıklı** -düzgün çalışıyor  

        -   **Etkin** olmayan-zaman aralığı boyunca hizmete veri gönderilmez  

        -   **Aracı durumu** -Windows 'ta aracının sistem hizmeti çalışmıyor  

        -   **Eklendi** -Policy uygulanmadı, ancak aracı ilke üzerinde yer bildirmedi  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a> Şirket içi Cihaz Sistem Durumu Kanıtlama  
 Windows 10 cihazları için sistem durumu kanıtlama artık şirket içi altyapıyı kullanarak iletişim kuracak şekilde yapılandırılabilir. Yöneticiler, raporlamanın bulut veya şirket içi kaynaklar aracılığıyla yapılıp yapılmadığını belirtebilir. Sistem durumu kanıtlama raporlaması için şirket içi seçilirse, hizmet için bir URL belirtilebilir. Bu, internet erişimi olmayan istemci bilgisayarların sistem durumu kanıtlama kullanarak cihazları etkinleştirmesine ve yönetmesine olanak tanır.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Şirket içi cihazlarda sistem durumu kanıtlamasını etkinleştirme  
 1605 ' de, 1604 Technical Preview 'da bulunan birkaç hata düzeltildi.  Denemek için, istemci Aracısı ayarlarını kullanarak şirket içi sistem durumu kanıtlama hizmetini yapılandırın.  

1.  Configuration Manager konsolunda, **Yönetim**  >  **genel bakış**  >  **istemci ayarları**' na gidin ve şirket **içi sistem durumu kanıtlama hizmetini kullan** ' ı **Evet**olarak ayarlayın.  

2.  **Şirket içi Sistem Durumu Kanıtlama Hizmeti URL'si**belirtin ve **Tamam**’a tıklayın.  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Windows 10 istemcileri için yazılım güncelleştirme yüklemesinden sonra yeni yeniden başlatma seçenekleri  
 Yeniden başlatma gerektiren bir yazılım güncelleştirmesi Configuration Manager kullanılarak dağıtıldığında ve bir bilgisayara yüklendiğinde, bekleyen bir yeniden başlatma zamanlanır ve bir yeniden başlatma iletişim kutusu görüntülenir. Şu anda Windows 8 ve üzeri için, Windows güç seçeneklerini kullanarak bilgisayarı kapatır veya yeniden başlatırsanız (yeniden başlatma iletişim kutusu yerine), bilgisayar yeniden başlatıldıktan sonra yeniden başlatma iletişim kutusu kalır ve bilgisayarın yapılandırılan son tarihte yeniden başlatılması gerekir. Bu Technical Preview sürümünde, Configuration Manager yazılım güncelleştirmesi için bekleyen bir yeniden başlatma olduğunda, **güncelleştirme ve yeniden başlatma** ve **güncelleştirme ve kapatma** seçeneği Windows 10 bilgisayarlarda Windows güç seçeneklerinde kullanılabilir olacaktır. Bu seçeneklerden biri kullanıldığında, bilgisayar yeniden başlatıldıktan sonra yeniden başlatma iletişim kutusu görüntülenmez.  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a> Şirkete ait cihazları ıMEı veya iOS seri numarası ile önceden bildirme  
 Artık, şirketin sahip olduğu cihazları Uluslararası istasyon mobil ekipman kimliği (ıMEı) numaralarını içeri aktararak tanımlayabilirsiniz. Cihaz ıMEı numaralarını içeren bir virgülle ayrılmış değerler (. csv) dosyasını karşıya yükleyebilir veya cihaz bilgilerini el ile girebilirsiniz.  İOS cihazlarının seri numaralarını da içeri aktarabilirsiniz.  İçeri aktarılan bilgiler, "Kurumsal" olarak kaydeden cihazların sahipliğini ayarlar.  Hizmete erişen her kullanıcı için bir Intune lisansı hala gereklidir.  

### <a name="try-it-out"></a>Deneyin!  
 Aşağıdaki görevleri tamamlamayı deneyin ve Microsoft Connect sitesinin [Configuration Manager geri bildirim programı](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) sayfasındaki geri bildirim formumuzu kullanarak nasıl çalıştığını bize bilgilendirin:  

-   Bir. csv dosyasında ıMEı numaraları kümesini içeri aktarın. Her satırda ıMEı numarası ve ardından bir ayrıntılar alanı bulunabilir.  

-   Configuration Manager konsolundan ıMEı numaralarını el ile içeri aktarın.  

-   Bir. csv dosyasında bir iOS seri numarası kümesini içeri aktarın. Yine, her satır bir sayı ve ardından cihaz ayrıntılarını içerir.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Şirkete ait cihazları IMEI veya iOS seri numarası ile önceden bildirme  

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**'  >  **e genel bakış**  >  **şirkete ait tüm cihazlar**  >  **önceden tanımlanmış cihazlar**' a gidin ve ardından **önceden tanımlanmış cihazlar oluştur**' a tıklayın. Önceden tanımlanmış cihazlar Sihirbazı açılır.  

2. Cihaz bilgilerini nasıl eklemek istediğinizi belirtin:  

   -   **IMEı numaralarını ve ayrıntılarını içeren bir. csv dosyasını karşıya yükle** -sayı listesini karşıya yüklemek için, bkz. Adım #3.  

   -   **IMEI numaralarını ve ayrıntılarını el ile ekleme** -bilgileri el ile girmek için, cihazların IMEI numarasını veya iOS seri numarasını ve ayrıntılarını yazın ve ardından #4 adımına geçin.  

3. Karşıya yüklenen dosyalar için şirkete ait cihazları önceden bildirmek üzere bilgileri içeren. csv dosyasına gidin. Dosya, üst satırı dışlayarak aşağıdaki biçimde olmalıdır (yalnızca rehberlik için verilmiştir):  

   |**IMEı #**|**iOS seri**|**İşletim sistemi**|**Ayrıntılar**|
   |---|---|---|---|
   |123456789012345||PENCERELERIN|Şirkete ait Windows cihazı|
   |123456789012|A0BCD0EFGH0J|IOS|Şirkete ait iOS cihazlar|
   |123456789012346||ANDROID|Şirkete ait Android cihazı|

    **Sütunlardan**  

   - Sütun 1: ıMEı numarası – her satır için ıMEı numarası veya iOS seri numarası gereklidir  

   - Sütun 2: iOS seri numarası – yalnızca iOS seri numaraları önceden tanımlanmış olabilir. Diğer cihaz platformları için ıMEı numarası kullan  

   - Sütun 3: cihazın Işletim sistemi (büyük/küçük harf gereklidir):  

     -   IOS – tüm iOS cihazları  

     -   WINDOWS – Windows Phone, Windows 10 Mobile ve Windows bilgisayarları Içerir  

     -   ANDROID – tüm Android cihazlar  

   - Sütun 4: Ayrıntılar – Configuration Manager konsolunda görünen ek cihaz bilgileri  

     **İleri**’ye tıklayın.  

4. Dosya içeri aktarma işleminin sonuçlarını gözden geçirin. Daha önce içeri aktarılan ıMEı veya seri numaralarının ayrıntıları, yeni ayrıntılarla güncelleştirilir.  Devam etmek için **İleri** ' ye, güncelleştirilmiş ayrıntıları korumak için **geri** ' ye veya sonra Sihirbazı doldurun.