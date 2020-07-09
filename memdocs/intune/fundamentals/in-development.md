---
title: Geliştirme-Microsoft Intune
titleSuffix: ''
description: Geliştirmede Microsoft Intune Özellikler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5afca831e2f3cbcda69150adcbbcff996bf99554
ms.sourcegitcommit: 01c1ca337e82c5e8e92153079ed89f79e20bde9e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86157816"
---
# <a name="in-development-for-microsoft-intune"></a>Microsoft Intune için geliştirme aşamasında

Hazırlık ve planlamada yardımcı olması için bu sayfada Intune Kullanıcı Arabirimi güncelleştirmeleri ve geliştirme aşamasında olan ancak henüz yayınlanmayan özellikler listelenir. Bu sayfadaki bilgilere ek olarak: 

- Bir değişiklikten önce işlem yapmanız gerektiğini düşünüyorsanız, Office ileti merkezi 'nde tamamlayıcı bir gönderi yayımlayacağız.
- Bir özellik üretim girdiğinde, bir önizleme veya genel kullanıma sunulduktan sonra özellik açıklaması bu [sayfadan yenilikler 'e taşınır.](whats-new.md)
- Bu [sayfa ve yenilikler sayfası düzenli](whats-new.md) aralıklarla güncelleştirilir. Ek güncelleştirmeleri daha sonra denetleyin.
- Stratejik teslim edilebilirler ve zaman çizelgeleri için [Microsoft 365 yol haritasını](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) inceleyin.

> [!NOTE]
> Bu sayfa, yaklaşan bir sürümdeki Intune özellikleri hakkındaki geçerli beklentilerimizi yansıtır. Tarihler ve bireysel Özellikler değişebilir. Bu sayfa, geliştirmede tüm özellikleri tanımlamaz.

**RSS akışı**: aşağıdaki URL 'yi kopyalayıp akış okuyucunuzun içine yapıştırarak bu sayfanın ne zaman güncelleştirileceğini öğrenin:`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Bu makale, yukarıdaki başlık altında listelenen tarihte son güncelleştirilme aşamasındadır.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Uygulama yönetimi

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Android 'de Şirket Portalı ve Intune uygulamalarında cihaz simgelerine güncelleştirme<!-- 6057023  -->
Android cihazlarda Şirket Portalı ve Intune uygulamalarındaki cihaz simgelerini güncelleştiriyoruz ve Microsoft 'un akıcı tasarım sistemiyle uyum sağlar. İlgili bilgiler için bkz. [iOS/ıpados ve macOS için şirket portalı App 'teki simgelere güncelleştirme](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>İOS ve Android kurumsal cihazlarda kayıt olmadan yönetilen Outlook için S/MIME<!-- 6517155  -->
Kayıt olmadan yönetilen cihazlar için uygulama yapılandırma ilkelerini kullanarak iOS ve Android kurumsal cihazlarda Outlook için S/MIME 'yi etkinleştirebileceksiniz. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen uygulamalar**Ekle ' yi seçin. Ayrıca, kullanıcıların Outlook 'ta bu ayarı değiştirmesine izin verip vermeyeceğinizi de seçebilirsiniz. Outlook yapılandırma ayarları hakkında daha fazla bilgi için bkz. [Microsoft Outlook yapılandırma ayarları](../apps/app-configuration-policies-outlook.md).

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS Şirket Portalı, Apple 'ın Kullanıcı benzeşimi olmadan otomatik cihaz kaydını destekleyecektir<!-- 7282707  --> 
iOS Şirket Portalı, Apple 'ın otomatik cihaz kaydı kullanılarak kaydedilen cihazlarda atanmış bir Kullanıcı gerekmeden desteklenecektir. Son Kullanıcı iOS Şirket Portalı, cihaz benzeşimi olmadan kaydedilen bir iOS/ıpados cihazında birincil kullanıcı olarak kurmak için oturum açabilir. Otomatik cihaz kaydı hakkında daha fazla bilgi için bkz. [Apple 'ın otomatik cihaz kaydı Ile iOS/ıpados cihazlarını otomatik olarak kaydetme](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Win32 uygulaması Yükleme bildirimleri ve Şirket Portalı<!-- 7485945  -->
Son kullanıcılar, [Microsoft Intune web Şirket portalı](https://portal.manage.microsoft.com/) gösterilen uygulamaların şirket portalı uygulama veya Web şirket portalı tarafından açılıp açılmayacağı konusunda karar verebilir. Bu seçenek yalnızca son kullanıcının yüklü Şirket Portalı uygulaması varsa ve bir Web Şirket Portalı uygulamasını tarayıcı dışında başlattığında kullanılabilir.

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Şirket Portalı Configuration Manager uygulama desteği ekler<!-- 4297660 -->
Şirket Portalı artık Configuration Manager uygulamalarını desteklemektedir. Bu özellik, son kullanıcıların ortak yönetilen müşteriler için Şirket Portalı hem Configuration Manager hem de Intune tarafından dağıtılan uygulamaları görmesini sağlar. Bu destek, yöneticilerin farklı Son Kullanıcı Portalı deneyimlerini birleştirmesine yardımcı olur. Daha fazla bilgi için bkz. [ortak yönetilen cihazlarda şirket portalı uygulamasını kullanma](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Cihaz yapılandırması

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Üçüncü taraf MDM iş ortaklarından cihaz uyumluluk durumunu ayarlama<!-- 6361689   -->
Üçüncü taraf MDM çözümlerine sahip olan Microsoft 365 müşteriler, Microsoft Intune cihaz uyumluluk hizmeti ile tümleştirme yoluyla iOS ve Android üzerinde Microsoft 365 uygulamalar için koşullu erişim ilkelerini zorlayabilir. Üçüncü taraf MDM satıcısı, Intune cihaz uyumluluk hizmetinden yararlanarak cihaz uyumluluk verilerini Intune 'a gönderir. Daha sonra Intune, cihazın güvenilir olup olmadığını ve Azure AD 'de koşullu erişim özniteliklerini ayarlamanızı sağlayacak şekilde değerlendirilir.  Müşterilerin, Microsoft Endpoint Manager yönetim merkezi veya Azure AD portalı içinden Azure AD koşullu erişim ilkeleri ayarlaması gerekecektir.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Windows 10 ve daha yeni cihazlar için yeni VPN ayarları<!-- 6602122  -->
Ikev2 bağlantı türünü kullanarak bir VPN profili oluşturduğunuzda yapılandırabileceğiniz yeni ayarlar vardır (**cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **Windows 10 ve sonrası** için platform > **VPN** > **temel VPN**):

- **Cihaz tüneli**: cihazların Kullanıcı oturumu açma da dahil olmak üzere herhangi bir Kullanıcı ETKILEŞIMI gerekmeden VPN 'ye otomatik olarak bağlanmasına izin verir. Bu özellik **her zaman açık**' i etkinleştirmenizi ve **makine sertifikalarını** kimlik doğrulama yöntemi olarak kullanmanızı gerektirir.
- Şifreleme paketi ayarları: istemci ve sunucu ayarlarını eşleştirmeye izin veren ıKE ve alt güvenlik ilişkilerinin güvenliğini sağlamak için kullanılan algoritmaları yapılandırın.

Yapılandırabileceğiniz ayarları görmek için, [Intune kullanarak VPN bağlantıları eklemek üzere Windows cihaz ayarları](../configuration/vpn-settings-windows-10.md)' na gidin.

Aşağıdakiler cihazlar için geçerlidir:
- Windows 10 ve üzeri

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Android kurumsal cihaz sahibi adanmış cihazlarda (COSU) yönetilen giriş ekranı için yeni özellikler<!-- 7414175 7133328 7133720 7134873 7135184  -->
Android kurumsal cihazlarda Yöneticiler, çok uygulama bilgi noktası modunu kullanarak adanmış cihazlarda yönetilen giriş ekranını özelleştirmek için cihaz yapılandırma profillerini kullanabilir (**cihazlar**  >  **yapılandırma profilleri**,  >  **Create profile**  >  **Android Enterprise** **cihaz sahibi > yalnızca**  >  profil > **cihaz deneyimi**için cihaz**kısıtlamalarına** sahiptir).

Özellikle şunları yapabilirsiniz:

- Simgeleri özelleştirme, ekran yönünü değiştirme ve rozet simgelerinde uygulama bildirimlerini gösterme <!--7414175-->
- Yönetilen ayarlar giriş noktasını gizle <!--7133328-->
- Hata ayıklama menüsüne daha kolay erişin <!--7133720-->
- Wi-Fi ağlarının izin verilen bir listesini oluşturma <!-- 7134873-->
- Cihaz bilgilerine daha kolay erişin <!-- 7135184-->

Daha fazla bilgi için bkz. [özelliklere izin vermek veya erişimi kısıtlamak Için Android kurumsal cihaz ayarları](../configuration/device-restrictions-android-for-work.md).

Aşağıdakiler cihazlar için geçerlidir:

- Android kurumsal cihaz sahibi, adanmış cihazlar (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Cihaz kaydı

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>Şirkete ait, kişisel olarak etkinleştirilen cihazlar (Önizleme)<!--4442275 -->
Intune, Android 8 ve üzeri işletim sistemi sürümleri için iş profiliyle iOS kurumsal şirkete ait cihazları destekleyecektir. İş profiline sahip şirkete ait cihazlar, Android kurumsal çözüm kümesindeki kurumsal yönetim senaryolarından biridir. Bu senaryo, kurumsal ve kişisel kullanım için tasarlanan tek Kullanıcı cihazlarına yöneliktir. Şirkete ait, kişisel olarak etkinleştirilen bu (COPE) senaryo şunları sunar:

- çalışma ve kişisel profil kapsayıcılama
- Yöneticiler için cihaz düzeyi denetimi
- Son kullanıcılara kişisel verilerinin ve uygulamalarının özel olarak kalacağı garantisi

İlk genel önizleme sürümü, genel olarak kullanılabilir sürüme dahil edilecek özelliklerin bir alt kümesini içerir. Ek özellikler, toplama temelinde eklenecektir. İlk önizlemede kullanılabilir olacak özellikler şunlardır:

- Kayıt: Yöneticiler, son tarihi olmayan benzersiz belirteçlerle birden çok kayıt profili oluşturabilir. Cihaz kaydı NFC, Token entry, QR Code, Zero Touch veya Knox Mobile kaydı aracılığıyla yapılabilir.
- Cihaz yapılandırması: mevcut, tam olarak yönetilen ve ayrılmış cihaz ayarlarının bir alt kümesi.
- Cihaz Uyumluluğu: Şu anda tam olarak yönetilen cihazlar için kullanılabilen uyumluluk ilkeleri.
- Cihaz eylemleri: cihazı silme (fabrika sıfırlaması), cihazı yeniden başlatma ve cihazı kilitleme.  
- Uygulama Yönetimi: uygulama atamaları, uygulama yapılandırması ve ilişkili raporlama özellikleri 
- Koşullu Erişim



<!-- ***********************************************-->
## <a name="device-management"></a>Cihaz yönetimi

### <a name="device-compliance-logs-now-in-english--6014904---"></a>Cihaz uyumluluk günlükleri artık Ingilizce olarak<!--6014904 -->
Intunedevicekarmaşıkanceorg yalnızca Karmaşıkstate, OwnerType ve DeviceHealthThreatLevel için numaralandırmalar vardır. Gelecekteki bir güncelleştirmede, bu günlüklerde sütunlarda Ingilizce bilgiler olacaktır.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>KCG cihazları için PowerShell betikleri desteği<!-- 1862833  -->
PowerShell betikleri, Intune 'da Azure AD kayıtlı cihazlarını destekleyecektir. PowerShell hakkında daha fazla bilgi için bkz. [Intune 'Da Windows 10 cihazlarda PowerShell betiklerini kullanma](../apps/intune-management-extension.md). Bu işlevsellik, Windows 10 Home Edition çalıştıran cihazları desteklemez.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics, cihaz ayrıntıları günlüğünü içerecektir<!--6014987  -->
Intune cihaz ayrıntı günlükleri, **raporlar**  >  **Log Analytics**' te kullanılabilir. Özel sorgular ve Azure çalışma kitapları oluşturmak için cihaz ayrıntılarını ilişkilendirebilirler.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Kiracı iliştirme: Yönetim merkezinde cihaz zaman çizelgesi<!--7220536, CM7141381 -->
Configuration Manager, kiracı iliştirme aracılığıyla bir cihazı Microsoft Uç Nokta Yöneticisi ile eşitlediğinde, olayların bir zaman çizelgesini görebileceksiniz. Bu zaman çizelgesi, cihazdaki sorunları gidermenize yardımcı olabilecek geçmiş etkinlikleri gösterir. Daha fazla bilgi için bkz. [Teknik önizleme 2005 Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Kiracı iliştirme: yönetim merkezinden bir uygulama yükler<!-- 7220536, CM6024389 -->
Microsoft uç nokta Yönetimi yönetim merkezinden bir kiracıya bağlı cihaz için bir uygulama yüklemesini gerçek zamanlı olarak başlatabileceksiniz. Daha fazla bilgi için bkz. [Teknik önizleme 2005 Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Kiracı iliştirme: yönetim merkezinden CMPivot<!--7220536, CM6024392 -->
[CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) 'In gücünü Microsoft Endpoint Manager yönetim merkezine getirebileceksiniz. Yardım masası gibi ek kişilerin buluttan, tek bir ConfigMgr tarafından yönetilen cihaza karşı gerçek zamanlı sorgular başlatabilmesini ve sonuçları yönetim merkezine geri döndürmesini sağlar. Bu, CMPivot 'in tüm geleneksel avantajlarından yararlanmanızı sağlar. Bu, BT yöneticilerinin ve diğer belirlenen kişilerin, ortamlarında cihazların durumunu hızlıca değerlendirebilme ve işlem yapması için sahip olduğu bir işlemdir. Daha fazla bilgi için bkz. [Teknik önizleme 2005 Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Kiracı iliştirme: yönetim merkezinden betikleri çalıştırma<!--7220536, CM6234688 -->
Şirket içi Configuration Manager [Çalıştır](../../configmgr/apps/deploy-use/create-deploy-scripts.md) özelliğinin gücünü Microsoft Endpoint Manager yönetim merkezine getirebileceksiniz. Yardım masası gibi ek personbuna, tek Configuration Manager yönetilen bir cihaza karşı, buluttan PowerShell betikleri çalıştırmasına izin verin. Bu, bu yeni ortama Configuration Manager yöneticisi tarafından önceden tanımlanmış ve onaylanmış olan PowerShell betiklerinin tüm geleneksel avantajlarını sağlar. Daha fazla bilgi için bkz. [Teknik önizleme 2005 Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Windows 10 cihazları için yeni birleştirme mantığı<!--179048-->
Günümüzde, bir müşteri bir cihazı yeniden görüntüler ve sonra yeniden kaydederse, Microsoft Endpoint Manager Yönetici konsolunda cihaz için birden çok kayıt görünür. Yeni birleştirme mantığı, Windows 10 cihazlarında bu tür yinelenen kayıtları birleştirmek için geliştirme aşamasındadır.

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>MacOS cihazları için uzaktan kilitleme eylemine yönelik güncelleştirmeler<!--7032805 -->
MacOS cihazları için uzaktan kilitleme eyleminin güncelleştirmeleri şunları içerir:
- Kurtarma PIN 'i silinmeden önce 30 gün boyunca görüntülenecektir (yedi gün yerine).
- Bir yöneticinin açık ikinci bir tarayıcısı varsa ve komutu farklı bir sekmeden ya da tarayıcıdan yeniden tetiklemeyi denediğinde, Intune komutun geçmesine izin verir. Ancak raporlama durumu, yeni bir PIN oluşturmak yerine başarısız olarak ayarlanır.
- Önceki komut hala beklenirse veya cihaz geri iade edilmemişse, yönetici başka bir uzaktan kilitleme komutu veremez.
Bu değişiklikler, birden çok uzaktan kilitleme komutlarından sonra doğru PIN 'in üzerine yazılmasını engellemek için tasarlanmıştır.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>MacOS cihazlarına yazılım güncelleştirmeleri dağıtma <!-- 3194876 -->
MacOS cihazları gruplarına yazılım güncelleştirmeleri dağıtabileceksiniz. Bu özellik kritik, bellenim, yapılandırma dosyası ve diğer güncelleştirmeleri içerir. Güncelleştirmeleri bir sonraki cihaz iadede gönderebilecek veya zaman içinde güncelleştirmeleri dağıtmak için haftalık bir zamanlama seçebileceğiniz şekilde ayarlayabilirsiniz. Bu, standart çalışma saatleri dışında veya yardım masanıza tam olarak çalıştırıldığında cihazları güncelleştirmek istediğinizde yardımcı olur. Ayrıca güncelleştirmelerin dağıtıldığı tüm macOS cihazlarının ayrıntılı bir raporunu alırsınız. Belirli güncelleştirmelerin durumlarını görmek için, raporu cihaz başına temelinde inceleyebilirsiniz.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>Ek veri ambarı v 1.0 özellikleri<!-- 6125732   -->
Intune veri ambarı v 1.0 kullanılarak ek özellikler mevcuttur. Aşağıdaki özellikler artık [cihazlar](../developer/reports-ref-devices.md#devices) varlığı aracılığıyla kullanıma sunulmuştur:
- `ethernetMacAddress`-Bu cihazın benzersiz ağ tanımlayıcısı.
- `office365Version`-Cihaza yüklü Office 365 sürümü.

Aşağıdaki özellikler artık [Devicepropertygeçmişin](../developer/reports-ref-devices.md#devicepropertyhistories) varlığı aracılığıyla kullanıma sunulmuştur:
- `physicalMemoryInBytes`-Bayt cinsinden fiziksel bellek.
- `totalStorageSpaceInBytes`-Bayt cinsinden toplam depolama kapasitesi.

Daha fazla bilgi için bkz. [Microsoft Intune veri ambarı API 'si](../developer/reports-nav-intune-data-warehouse.md).

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI uyumluluk raporu şablonu V 2.0<!-- 636958  -->
Yöneticiler, Power BI uyumluluk raporu şablonu sürümünü V 1.0 'dan V 2.0 'a güncelleştirebilir. V 2.0, gelişmiş bir tasarım, Ayrıca, şablonun bir parçası olarak ortaya çıkacak hesaplamalarda ve verilerde yapılan değişiklikleri içerir. İlgili bilgiler için bkz. [Power BI veri ambarına bağlanma](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Özelleştirme İlkeleri için kapsam etiketi desteği<!--6182440 -->
Özelleştirme ilkelerine kapsam etiketleri atayabileceksiniz. Bunu yapmak için, kapsam etiketleri yapılandırma seçeneklerini göreceğiniz [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **kiracı yönetim** >  **özelleştirmesi** ' **Scope tags** na gidin.

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>Profil ata ve profili Güncelleştir izin değişiklikleri<!--7177586 -->
Rol tabanlı erişim denetimi izinleri, atama profili ve güncelleştirme profili için değişecek:
- Profil ata: Yöneticiler bu izne sahip profiller için de profiller atayabilir ve bir belirtece varsayılan bir profil atayabilir.
- Güncelleştirme profili: Bu izne sahip Yöneticiler yalnızca var olan profilleri güncelleştirebilecektir.

<!-- ***********************************************-->
## <a name="security"></a>Güvenlik

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Symantec Endpoint Security ve Check Point sandblast için uygulama koruma ilkesi desteği<!--  4452423, 4731168 -->

Ekim 2019 ' de Intune uygulama koruma ilkesi, Microsoft Threat Defense iş ortaklarından (MTD iş ortakları) bazılarının verilerini kullanma özelliğini ekledi. Bir cihazın sistem durumuna bağlı olarak kullanıcının şirket verilerini engellemek veya seçmeli olarak silmek üzere bir uygulama koruma İlkesi kullanmak için aşağıdaki iş ortakları için destek ekliyoruz:

- **Check Point sandblast** for Android, IOS ve ıpados
- Android, iOS ve ıpados üzerinde **Symantec uç nokta güvenliği**

MTD iş ortaklarıyla uygulama koruma ilkesi kullanma hakkında daha fazla bilgi için bkz. [Intune Ile mobil tehdit savunması uygulama koruma Ilkesi oluşturma](../protect/mtd-app-protection-policy.md).

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>Intune 'a kaydolmadan önce Filekasasıyla şifrelenen bir macOS cihazının kurtarma anahtarını depolayın<!--5239424   -->
Yakında, bir macOS cihazının Intune 'dan dosya Kasası ilkesi tarafından şifrelenmeyen veya Intune 'a kaydolmadan önce şifrelendiğinden, Intune tarafından yeniden şifrelenecek şekilde cihaz şifresinin çözülmesi gerekmez. Bunun yerine, geçerli şifreleme yerinde kalabilir ve Kullanıcı şifrelenmiş macOS cihazı için kişisel kurtarma anahtarını göndermek üzere *Mağaza kurtarma anahtarını* seçebilecekleri Şirket portalı Web sitesine gidebilir. Intune, geçerli bir anahtarın gönderilmesinden sonra, Şirket Portalı Web sitesi, iOS/Şirket Portalı, Android Şirket Portalı veya Intune uygulaması aracılığıyla kullanıcının kullanımına açık olan yeni bir anahtar oluşturmak için kişisel anahtarı döndürür. Kullanıcılar daha sonra bu konumlara herhangi bir cihazdan erişebilir ve bu da anahtarı, macOS cihazlarından kilitlenmeleri gerekir.

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>MacOS Filekasası disk şifrelemesi sırasında bir cihaz kullanıcısının kişisel kurtarma anahtarını gizle<!--  5475632  -->
Dosya Kasası için uç nokta güvenlik diski şifreleme ilkesine *Kurtarma anahtarını Gizle* adlı yeni bir ayar ekledik (**uç nokta güvenlik**  >  **diski şifrelemesi**  >  **Create PROFILE**  >  **MacOS**  >  **filekasası**). Yeni ayarı etkinleştirdiğinizde, Intune şifreleme sırasında macOS cihazının kullanıcısının kişisel kurtarma anahtarını gizler. Şu anda anahtarı gizleyerek, kullanıcıların cihazın şifrelenmesini beklerken daha sonra yazamayacak kadar güvenli kalmasına yardımcı olabilirsiniz. Bunun yerine, kurtarma gerekliyse, Kullanıcı Intune Şirket Portalı Web sitesi aracılığıyla kişisel kurtarma anahtarını görüntülemek için her zaman herhangi bir cihazı kullanabilir.

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>Cihazlar için güvenlik temeli ayrıntılarının geliştirilmiş görünümü<!-- 5536846   -->
Bir cihazın ayrıntılarına (**uç nokta güvenlik**  >  **cihazları**) göz katdığınızda güvenlik temeli ayarlarına yönelik ayrıntıların görüntülenmesini geliştirmek için çalışıyoruz.  Atanan her güvenlik temeli için, her bir ayarın kategori, ayar adı ve bu cihazdaki her ayarın durumunu içeren bir ayrıntı listesini görüntüleyebileceksiniz.

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>Windows 10 cihazları için Endpoint Security virüsten koruma ilkesiyle birlikte tanım güncelleştirmelerinin kaynak konumlarını yönetme<!-- 6347801  -->  
Windows 10 cihazları için Endpoint Security Antivirus ilkesinin *Updates* kategorisine iki yeni ayar ekliyoruz. cihazları güncelleştirme tanımlarını alma (**uç nokta güvenliği** > * * virüsten koruma * * > **ilke**  >  **Windows 10 ve üzeri**  >  **Microsoft Defender virüsten koruma**) yönetme konusunda size yardımcı olabilir.

Yeni ayarlar sayesinde, UNC dosya paylaşımlarını tanım güncelleştirmeleri için indirme kaynak konumları olarak ekleyebilir ve farklı kaynak konumlarına hangi sıra ile iletişim kurulabildiğini tanımlayabilirsiniz. Yeni ayarlar aşağıdaki Defender CSP 'Leri yönetir:

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallkarşılanamayan](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>Kiracı ekli cihazlarını MDADTP 'ye ekleme için uç nokta algılama ve yanıt ilkesi önizleme dışına taşınıyor<!-- 7303816   -->
Intune 'daki Endpoint Security 'nin bir parçası olarak, Configuration Manager tarafından yönetilen cihazlar ile kullanım için uç nokta algılama ve yanıt (EDR) ilkeleri yakında ön izleme dışında hareket eder ve genel kullanıma sunulacaktır (**uç nokta güvenlik**  >  **uç noktası algılama ve yanıt**  >  **oluşturma ilkesi**  >  **Windows 10 ve Windows Server**). [Configuration Manager Için kiracı ekleme](../../configmgr/tenant-attach/device-sync-actions.md)yapılandırdığınızda, EDR ilkelerini kullanarak Configuration Manager tarafından yönetilen cihazları Microsoft Defender Gelişmiş tehdit koruması 'Na (MICROSOFT Defender ATP) ekleyebilirsiniz. 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>Güvenlik temelleri düğümü geliştirmeleri<!-- 7433136   -->
Microsoft Endpoint Manager Yönetim Merkezi 'nde güvenlik temeli düğümünün kullanılabilirliğini artırmak için, her bir taban çizgisinin *genel bakış* sekmesini kaldırdık ve bunun yerine taban çizgileri **profil** sekmesini (**uç nokta güvenlik**  >  **güvenliği temelleri**  >  *taban çizgisi*) açmanız gerekir.

Her bir taban çizgisinin *genel bakış* sayfası, dağıttığınız son temel sürümden sonuçları toplayan grafikleri ve kutucukları görüntüler. Bu bilgiler, daha fazla ayrıntı için bir sürüme göz atın, gördüğünüz bilgilerden yinelenir. *Genel bakış* sayfası kaldırıldıktan sonra, sürüme doğrudan göz katdığınızda Bu grafikler ve toplu ayrıntılar kullanılabilir olmaya devam edecektir.  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>Güvenlik duvarı kuralı geçiş aracı önizlemesi<!-- 6423187  -->
Genel önizleme olarak, Windows Defender güvenlik duvarı kurallarını geçiren bir PowerShell tabanlı araç üzerinde çalışıyoruz. Aracı yükleyip çalıştırdığınızda, Windows 10 istemcisinin geçerli yapılandırmasına dayalı olarak Intune için uç nokta güvenliği Güvenlik Duvarı kural ilkelerini otomatik olarak oluşturur.

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>Uç nokta güvenlik saldırısı yüzeyi azaltma ilkesinde cihaz denetim profili için yeni ayarlar<!--7032084 -->
Endpoint Security saldırı yüzeyi Azaltma ilkesi için cihaz denetim profiline Windows 10 cihazları için çeşitli ayarlar ekliyoruz (**uç nokta güvenlik**  >  **saldırısı yüzeyi azaltma**  >  **ilke**  >  **Windows 10 ve daha yeni**  >  **cihaz denetimi**oluştur). 

Yeni ayarlar, *cihaz yapılandırması*için [cihaz kısıtlama profillerinde](../configuration/device-restrictions-windows-10.md) bugün kullanılabilen ayarlarla aynı olacaktır. *Cihaz denetim* profiline eklenmekte olan ayarlar çeşitli Bluetooth ayarlarını içermelidir.  


<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.
