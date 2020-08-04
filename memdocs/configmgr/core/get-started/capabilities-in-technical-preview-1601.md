---
title: Technical Preview 1601 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1601 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: be1401f28ccbd15de2561a19169ed67a81a91550
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526041"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Configuration Manager için Technical Preview 1601 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1601 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz.      Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).  

 **Bu Technical Preview için bilinen sorunlar:**  

-   Bir ön üretim istemcisini üretime yükseltmek için **Istemci güncelleştirme seçeneklerini** yönetirken, onay kutusunun metni gerçek istemci derleme numarası yerine sıfır (0) istemci sürümünü görüntüler. Doğru üretim öncesi istemci sürümü, bu seçeneğin üzerindeki yüzeyde gösterilir ve bu seçeneği belirlediğinizde üretime yükseltilen istemci sürümdür.  

-   Technical Preview 1601 ' e güncelleştirirken ve Configuration Manager istemcisini bir ön üretim koleksiyonunda sınamayı seçtiğinizde, koleksiyonun istemci paketi yükseltilmeyecektir. Bu sorun yalnızca Technical Preview 1601 içindir.  

     Bu sorunları geçici olarak çözmek için, aşağıdakilerden birini yapın:  

    -   Birincil sitenin veritabanında aşağıdaki SQL betiğini çalıştırın:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Laboratuvar sitenize yeni bir dağıtım noktası site sistem rolü ekleyin. Yeni dağıtım noktası, ön üretim koleksiyonunu yeni istemci paketiyle yükseltecektir.  

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a>Microsoft Intune tümleştirme geliştirmeleri  
1601 Technical Preview sürümünde aşağıdaki özellikler için destek ekledik:  

### <a name="improvements-to-conditional-access"></a>Koşullu erişim geliştirmeleri  

-   **Configuration Manager tarafından yönetilen bilgisayarlar için koşullu erişim desteği**  

     Artık, Exchange Online ve SharePoint Online hizmetlerine erişmek için bilgisayarların uyumluluk ilkesiyle uyumlu olmasını gerektiren Configuration Manager tarafından yönetilen bilgisayarlar için koşullu erişim ilkeleri ayarlayabilirsiniz.  Bu yeni işlevle Ayrıca, uyumluluk ilkesi aracılığıyla bilgisayarları Azure AD 'ye kaydedebilir ve Azure AD kaydını izleyip rapor edebilirsiniz.  

    > [!NOTE]  
    >  Koşullu erişim henüz Windows 10 ' da desteklenmiyor.  

    Bu özelliği kullanmak için Önkoşullar aşağıda verilmiştir:  

    -   Abonelik ve ADFS eşitlemesini Azure Active Directory Premium.  

    -   Microsoft Intune Aboneliği. Microsoft Intune aboneliğin Configuration Manager konsolunda yapılandırılması gerekir.  

    -   [Azure AD otomatik kaydı Için Önkoşullar](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Seçeneğini kullanmak için, aşağıda açıklanan belirli kurallara sahip Configuration Manager bir uyumluluk ilkesi oluşturmanız ve Intune konsolunda bir koşullu erişim ilkesi ayarlamanız gerekir.  Ayrıca, yalnızca uyumlu bilgisayarların erişimine izin verildiğinden emin olmak için Windows BILGISAYARı gereksinimini **cihazlar uyumlu** olmalıdır seçeneğine ayarlamanız gerekir. Configuration Manager tarafından yönetilen bilgisayarlar için geçerli olan uyumlu ilke kuralları aşağıda verilmiştir.  

    -   **Azure ActiveDirectory 'de kayıt gerektir:** Bu kural, kullanıcının cihazının Azure AD 'ye katılıp katılmadığını denetler ve yoksa cihaz otomatik olarak Azure AD 'ye kaydedilir. Otomatik kayıt yalnızca Windows 8.1’de desteklenir. Windows 7 bilgisayarlar için otomatik kayıt gerçekleştirmek üzere bir MSI dağıtın. Daha fazla bilgi için [buraya](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)bakın.  

    -   **Belirli bir gün sayısından daha eski bir son tarihe sahip tüm gerekli güncelleştirmeler:** Bu kural, kullanıcının cihazında, sizin belirttiğiniz son tarih ve yetkisiz kullanım süresi içinde gerekli tüm güncelleştirmelerin ( **gerekli otomatik güncelleştirmeler** kuralında belirtilir) olup olmadığını denetler ve bekleyen gerekli güncelleştirmeleri otomatik olarak yükler.  

    -   **BitLocker Sürücü Şifrelemesi gerektir:** Bu, cihazdaki birincil sürücünün (ör. C:) BitLocker şifreli olup olmadığını görmek için bir denetledir \\ . Birincil cihazda BitLocker şifresi etkin değilse, e-posta ve SharePoint Online hizmetlerine erişim engellenir.  

    -   **Kötü amaçlı yazılımdan koruma gerektir:** Bu, kötü amaçlı yazılımdan koruma yazılımının (yalnızca System Center Endpoint Protection veya Windows Defender) etkinleştirilip etkinleştirilmediğini ve çalıştığını görmek için bir denetdir.  
         Etkin değilse, e-posta ve SharePoint hizmetlerine erişim engellenir.  

    Uyumsuzluk nedeniyle engellenen son kullanıcılar yazılım merkezindeki uyumluluk bilgilerini görüntüler ve uyumluluk sorunları düzeltildiğinde yeni bir ilke değerlendirmesi başlatır.  

-   **Durum kanıtlama hizmeti Ile koşullu erişim** Artık, cihaz sistem durumu kanıtlama hizmeti tarafından raporlanan cihazların sistem durumuna bağlı olarak e-posta ve 0365 hizmetlerine erişimi kısıtlayabilirsiniz.  Ayrıca, Intune tarafından yönetilen cihazlar cihaz sistem durumu raporlarına dahil edilir.  

    Configuration Manager konsoluna, cihazların sistem durumlarına göre erişim izni verilip verilmeyeceğini belirtmenize izin veren yeni bir uyumluluk kuralı eklenmiştir.  Bu kuralı oluşturmak için **Uyumluluk Ilkesi oluşturma Sihirbazı**' nı açın ve yeni bir kural ekleyin.  Koşul için **sistem durumu kanıtlama hizmeti tarafından bildirilen sistem durumu olarak bildirildi** ' i seçin ve değeri **true**olarak ayarlayın.  Bu, yalnızca sağlıklı olarak bildirilen cihazların şirket kaynaklarınıza erişime sahip olduğundan emin olur. Sistem durumu kanıtlama hizmeti ve Intune 'da cihazların sistem durumunun nasıl bildirildiği hakkında ayrıntılar için, bkz. [cihaz sistem durumu kanıtlama](capabilities-in-technical-preview-1512.md#bkmk_devicehealth).  

-   **Yeni uyumluluk ilkesi ayarları:** Yeni uyumluluk ilkesi ayarları, şirket e-postasına ve SharePoint hizmetlerine erişmek için kullanılan cihazlarda güvenlik ve korumanın artırılmasına yardımcı olur:  

    -   **Otomatik güncelleştirmeleri gerektir:** Güncelleştirmelerin otomatik olarak yüklenmesine izin vermek için Windows 8.1 veya üzeri cihazları zorunlu kılabilir ve ayrıca yüklü olan güncelleştirmelerin sınıfını belirtebilirsiniz.  Aşağıdakilerden birini seçebilirsiniz: yalnızca önemli olarak işaretlenmiş güncelleştirmeleri yükleyebilir veya tüm önerilen güncelleştirmeleri yükleyebilirsiniz.  

         Otomatik Güncelleştirmeler için bir kural oluşturmak üzere **Uyumluluk Ilkesi oluşturma Sihirbazı**' nı açın ve yeni bir kural ekleyin.  Koşul olarak **gereken güncelleştirmelerin minimum sınıflandırmasını** seçin ve değeri kullanılabilir değerlerden birine ayarlayın: **hiçbiri**, **Önerilen**ve **önemli**.  

        -   **Hiçbiri:** Güncelleştirmeler otomatik olarak yüklenmez.  

        -   **Önerilen:** Önerilen tüm güncelleştirmeler yüklendi  

        -   **Önemli:** Yalnızca önemli olarak sınıflandırılan güncelleştirmeler yüklenir.  

    -   **Mobil cihazların kilidini açmak için parola gerektir:** Bu ayar **Evet**olarak ayarlandığında, son kullanıcıların cihazlarına erişebilmeleri için önce bir parola girmesi gerekir.  

         Mobil cihazların kilidini açmak için parola kuralı oluşturmak üzere **Uyumluluk Ilkesi oluşturma Sihirbazı**' nı açın ve yeni bir kural ekleyin. Koşul olarak **boş bir cihazın kilidini açmak için parola gerektir** ' i seçin ve değeri **true**olarak ayarlayın.  

    -   **Parola istenmeden önce geçen işlem yapılmayan dakika sayısı:**  Kullanıcı parolasını yeniden girmeden önce boşta geçen süreyi belirtir.  

         Bu kuralı oluşturmak için **Uyumluluk Ilkesi oluşturma Sihirbazı**' nı açın ve yeni bir kural ekleyin. Koşul için **parola istenmeden önce geçen işlem yapılmayan dakika sayısını seçin** ve değeri kullanılabilir seçeneklerden birine ayarlayın: 1 dakika, 5 dakika, 15 dakika, 30 dakika, ı saat.  

-   **Varsayılan kuralı geçersiz kılma-Intune 'a kayıtlı ve uyumlu cihazların şirket içi Exchange 'e erişmesine her zaman izin ver:**  

     Bu seçeneği belirlediğinizde, Intune 'a kayıtlı ve uyumluluk ilkeleriyle uyumlu cihazların şirket içi Exchange 'e erişmesine izin verilir. Bu kural varsayılan kuralı geçersiz kılar. Bu, varsayılan kuralı karantina veya engelleme erişimi olarak ayarlamış olsanız bile kayıtlı ve uyumlu cihazların şirket içi Exchange 'e erişebileceği anlamına gelir.  
     Kayıtlı ve uyumlu cihazların her zaman şirket içi Exchange aracılığıyla e-posta erişimine sahip olmasını istiyorsanız bu ayarı kullanın.  

     Bu, aşağıdaki platformlarda desteklenir: Windows Phone 8 ve üzeri, iOS 6 ve üzeri. Android 4,0 ve üzeri, Samsung KNOX Standard 4,0 ve üzeri.  

     Bu seçeneği kullanmak için şirket içi Exchange için **koşullu erişim Ilkesini Yapılandırma Sihirbazı** ' nın **genel** sayfasına gidin.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a>İstemci çevrimiçi durumu  
Technical Preview 1601 ' den başlayarak, bir istemcinin Configuration Manager konsolunda çevrimiçi veya çevrimdışı olduğunu bir bakışta belirleyebilirsiniz. Konsol cihaz dökümlerinin güncelleştirilmiş simgeleri ve sütunları ile, sorun alanını ve ilgilenmeniz gerekebilecek diğer sorunları belirlemek için ortamınızdaki istemcilerin durumunu değerlendirebilirsiniz.  

İstemci şu anda Configuration Manager bir yönetim noktası site sistemi rolüne bağlıysa çevrimiçi hale gelir. Yönetim noktası istemciden ping benzeri iletiler aldığı sürece, durumu çevrimiçi olur. Yönetim, 5 dakika boyunca bir ileti almazsa, istemcinin durumu çevrimdışı olarak değişir.  

### <a name="icons-for-client-status"></a>İstemci durumu simgeleri  

| Simge | Açıklama |
| ---- | ----------- |
|![istemciler için çevrimiçi durum simgesi](media/online-status-icon.png)|İstemci çevrimiçi.|  
|![istemciler için çevrimdışı durum simgesi](media/offline-status-icon.png)|İstemci çevrimdışı.|  
|![istemciler için bilinmeyen durum simgesi](media/unknown-status-icon.png)|İstemci durumu bilinmiyor.|  

### <a name="prerequisites"></a>Önkoşullar  
 İstemci çevrimiçi durumunun önkoşulları yok. Teknik Önizleme 1601 Configuration Manager yüklendiği anda kullanmaya başlayabilirsiniz.  

### <a name="limitations"></a>Sınırlamalar  
 İstemci çevrimiçi durumu yalnızca Configuration Manager istemcisinin yüklendiği Windows bilgisayarlarda kullanılabilir. İstemci çevrimiçi durumu, Mac bilgisayarlar, Linux veya UNIX bilgisayar ya da \- Şirket Içi mobil cihaz yönetimi ile yönetilen cihazlar için desteklenmez.  

### <a name="to-view-client-online-status"></a>İstemci çevrimiçi durumunu görüntülemek için  

1. Configuration Manager konsolunda, **varlıklar ve uyumluluk > genel bakış > cihazlara**gidin.  

2. Sütun başlığına sağ tıklayın ve ardından istemci çevrimiçi durumu alanlarından birine tıklayarak cihaz görünümüne ekleyin. Alanlar  

   -   **Cihaz Çevrimiçi Durumu** istemcinin o anda çevrimiçi veya çevrimdışı olduğunu gösterir.  

   -   **Son çevrimiçi zamanı** , istemci çevrimiçi durumunun çevrimdışı iken çevrimiçi durumuna değiştiğini gösterir.  

   -   **Son çevrimdışı süre** , durumun çevrimiçi iken çevrimdışına ne zaman değiştiğini gösterir.  

   İstemci durumundaki son değişiklikleri göstermek için konsolu yenileyin.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a>Uygulama yönetimi geliştirmeleri  
 1601 Technical Preview sürümünde aşağıdaki özellikler için destek ekledik:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>iOS cihazları için toplu satın alınan uygulamaları yönetme  
 Bazı uygulama depoları, kuruluşunuzda çalıştırmak istediğiniz bir uygulama için birden fazla lisans satın almanıza olanak sağlayabilir. Bu durum, satın alınan uygulamaların birden fazla kopyasın izlemeye yönelik yönetim yükünü azaltmanıza yardımcı olabilir.  

 Configuration Manager, lisans bilgilerini uygulama mağazasından içeri aktararak ve kaç lisansın kullanıldığını izleyerek böyle bir program aracılığıyla satın aldığınız uygulamaları yönetmenize yardımcı olur.  


### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS-Uygulamalar için uygulama yapılandırması<br />Hibrit  
 Bazı iOS uygulamaları, uygulamanın bağlanması gereken sunucu veya veritabanı gibi ayarları önceden yapılandırmayı destekler. Configuration Manager artık, uygulamanın bu bilgileri bilmeleri gerekmeden uygulamayı hemen kullanmasını sağlayan cihaza uygulama yapılandırma ilkelerinin dağıtılmasını desteklemektedir. Geliştiricilerin uygulamalarında bu işlevselliği etkinleştirmesi gerekir.  

 Genel olarak yayınlanan sınırlı sayıda uygulama, şu anda ayarları önceden yapılandırmayı destekliyor. Ayrıca, bunları destekleyen, şirket içi geliştirilmiş iş kolu uygulamalarına da sahip olabilirsiniz.  

#### <a name="prerequisites-for-this-scenario"></a>Bu senaryonun önkoşulları  

-   Configuration Manager için bir Microsoft Intune aboneliği eklemiş olmanız gerekir.  

-   Intune aboneliğine geçerli bir Apple APNs sertifikası eklemiş olmanız gerekir.  

-   Uygulama yapılandırmasını destekleyen bir iOS uygulaması dağıtmış olmanız gerekir.  

#### <a name="try-it-out"></a>Deneyin!  
 Yukarıdaki önkoşullar karşılandıktan sonra, iOS dağıtım türü kullanan bir Configuration Manager uygulaması oluşturmanız gerekir. Kullandığınız uygulamanın uygulama yapılandırmasını desteklemesi gerekir. Belirli öğelerin (ad/değer çiftleri) ne şekilde yapılandırılacağını öğrenmek için uygulamanın satıcı belgelerine bakın.  

 Ardından, uygulama dağıtımı sırasında uygulama yapılandırma ilkesini iOS dağıtım türü ile ilişkilendirirsiniz. İlkeyi, mevcut bir uygulama ve koleksiyona hedeflenmiş **uygulama yapılandırma ilkeleri** düğümünden da dağıtabilirsiniz.  

 Aşağıdaki görevleri tamamlamayı deneyin ve daha sonra bu konunun en üstündeki geri bildirim bilgilerini kullanarak nasıl çalıştıhaberdar etmemizi sağlayın:  

-   Uygulama yapılandırmasını destekleyen bir iOS uygulamanız varsa, uygulamayı yapılandırmak için belirtmeniz gereken ad ve değer çiftlerini öğrenmek için uygulama satıcısının belgelerine başvurun.  

-   **Uygulama yapılandırma Ilkesi oluşturma** Sihirbazı 'nı başlatın. Sihirbazın **IOS ilkesi** sayfasında, uygulama satıcısı belgelerinden bulduğunuz ad ve değer çiftlerini eklemeyi deneyin veya gerekli değerleri IÇEREN bir XML dosyasını içeri aktarabilirsiniz.  

-   **Yazılım dağıtma** Sihirbazı ' nda, **uygulama yapılandırma ilkesi** sayfasında, oluşturduğunuz uygulama yapılandırma ilkesini uygulamadan uyumlu bir dağıtım türüyle ilişkilendirin.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a>Uyumluluk ayarları geliştirmeleri  
 1601 Technical Preview sürümünde aşağıdaki özellikler için destek ekledik:  

### <a name="microsoft-edge-browser-settings"></a>Microsoft Edge tarayıcı ayarları  
 Microsoft Edge tarayıcısının yeni ayarları **Windows 8.1 ve Windows 10** yapılandırma öğesine eklenmiştir (ayarlar yalnızca Windows 10 cihazları için geçerlidir).  

 Yeni ayarları görmek için, **yapılandırma öğesi oluştur** sihirbazının yapılandırma öğesi **cihaz ayarları** sayfasında **Microsoft Edge** ' i seçin.  

 Daha fazla bilgi için bkz. [Configuration Manager istemcisi olmadan yönetilen Windows 8.1 ve Windows 10 cihazları için yapılandırma öğeleri oluşturma](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Windows 10 Team cihazları için uyumluluk ayarları  
 Surface Hub cihazları gibi Windows 10 ekibini çalıştıran cihazları yapılandırmak için bu yeni uyumluluk ayarlarını kullanın.  

 Yeni ayarları görmek için, **yapılandırma öğesi oluştur** sihirbazının yapılandırma öğesi **cihaz ayarları** sayfasında **Windows 10 Team** ' i seçin.  

 Daha fazla bilgi için bkz. [Configuration Manager istemcisi olmadan yönetilen Windows 8.1 ve Windows 10 cihazları için yapılandırma öğeleri oluşturma](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Samsung KNOX Standard için Android bilgi noktası modu<br />Hibrit  
 Bilgi noktası modu bir cihazı yalnızca belirli özelliklerin çalışmasına izin verecek şekilde kilitlemenize imkan tanır. Örneğin, bir cihazın yalnızca belirttiğiniz bir yönetilen uygulamayı çalıştırmasına izin verebilir veya bir cihazdaki ses düğmelerini devre dışı bırakabilirsiniz. Bu ayarlar, bir cihazın tanıtım modeli için veya satış noktası cihazı gibi yalnızca bir işlevi gerçekleştirmeye ayrılan bir cihaz için kullanılabilir. Bu ayarlar **Windows 8.1 ve Windows 10** yapılandırma ÖĞESINDE Samsung KNOX Standard cihazlarında kullanılamaz (ayarlar yalnızca Windows 10 cihazlarına uygulanır).  

 Yeni ayarları görmek için, **yapılandırma öğesi oluştur** sihirbazının yapılandırma öğesi **cihaz ayarları** sayfasında **BILGI noktası modu-Samsung KNOX** ' u seçin.  

 Daha fazla bilgi için bkz. [Configuration Manager istemcisi olmadan yönetilen Windows 8.1 ve Windows 10 cihazları için yapılandırma öğeleri oluşturma](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
