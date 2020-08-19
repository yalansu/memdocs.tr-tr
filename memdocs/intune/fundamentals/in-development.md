---
title: Geliştirme-Microsoft Intune
titleSuffix: ''
description: Geliştirmede Microsoft Intune Özellikler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c1a51f327f87e26a07cc7c344d0a0afc0bfde9b
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614792"
---
# <a name="in-development-for-microsoft-intune"></a>Microsoft Intune için geliştirme aşamasında

Hazırlık ve planlamada yardımcı olması için bu sayfada Intune Kullanıcı Arabirimi güncelleştirmeleri ve geliştirme aşamasında olan ancak henüz yayınlanmayan özellikler listelenir. Bu sayfadaki bilgilere ek olarak: 

- Bir değişiklikten önce işlem yapmanız gerektiğini düşünüyorsanız, Office ileti merkezi 'nde tamamlayıcı bir gönderi yayımlayacağız.
- Bir özellik üretim girdiğinde, bir önizleme veya genel kullanıma sunulduktan sonra özellik açıklaması bu [sayfadan yenilikler 'e taşınır.](whats-new.md)
- Bu [sayfa ve yenilikler sayfası düzenli](whats-new.md) aralıklarla güncelleştirilir. Ek güncelleştirmeleri daha sonra denetleyin.
- Stratejik teslim edilebilirler ve zaman çizelgeleri için [Microsoft 365 yol haritasını](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) inceleyin.

> [!NOTE]
> Bu sayfa, yaklaşan bir sürümdeki Intune özellikleri hakkındaki geçerli beklentilerimizi yansıtır. Tarihler ve bireysel Özellikler değişebilir. Bu sayfa, geliştirmede tüm özellikleri tanımlamaz.

**RSS akışı**: aşağıdaki URL 'yi kopyalayıp akış okuyucunuzun içine yapıştırarak bu sayfanın ne zaman güncelleştirileceğini öğrenin: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

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

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS Şirket Portalı, Apple 'ın Kullanıcı benzeşimi olmadan otomatik cihaz kaydını destekleyecektir<!-- 7282707  --> 
iOS Şirket Portalı, Apple 'ın otomatik cihaz kaydı kullanılarak kaydedilen cihazlarda atanmış bir Kullanıcı gerekmeden desteklenecektir. Son Kullanıcı iOS Şirket Portalı, cihaz benzeşimi olmadan kaydedilen bir iOS/ıpados cihazında birincil kullanıcı olarak kurmak için oturum açabilir. Otomatik cihaz kaydı hakkında daha fazla bilgi için bkz. [Apple 'ın otomatik cihaz kaydı Ile iOS/ıpados cihazlarını otomatik olarak kaydetme](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>Windows Şirket Portalı Configuration Manager uygulama desteği ekliyor<!-- 4297660 -->
Windows Şirket Portalı artık Configuration Manager uygulamalarını desteklemektedir. Bu özellik, son kullanıcıların birlikte yönetilen müşteriler için Windows Şirket Portalı içinde hem Configuration Manager hem de Intune tarafından dağıtılan uygulamaları görmesini sağlar. Bu destek, yöneticilerin farklı Son Kullanıcı Portalı deneyimlerini birleştirmesine yardımcı olur. Daha fazla bilgi için bkz. [ortak yönetilen cihazlarda şirket portalı uygulamasını kullanma](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Cihaz yapılandırması

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Android kurumsal tam olarak yönetilen cihazlar (COBO) için PKCS sertifika profilleri oluşturma<!-- 4839686 -->
Android kurumsal cihaz sahibine ve iş profili cihazlarına sertifika dağıtmak için PKCS sertifika profilleri oluşturabilirsiniz (**cihaz**  >  **yapılandırma profilleri**  >  **Create profile**  >  yalnızca profil için **PKCS** > için SDK kurumsal **> cihaz sahibini**veya **Android kurumsal > iş profilini** oluşturur).

Yakında, Android kurumsal tam olarak yönetilen cihazlar için PKCS sertifika profilleri oluşturabileceksiniz. Intune PFX Sertifika bağlayıcısı gereklidir. SCEP kullanmıyorsanız ve yalnızca PKCS kullanıyorsanız, yeni PFX bağlayıcısını yükledikten sonra NDES bağlayıcısını kaldırabilirsiniz. Yeni PFX Bağlayıcısı PFX dosyalarını içeri aktarır ve PKCS sertifikalarını tüm platformlara dağıtır.

PKCS sertifikaları hakkında daha fazla bilgi için bkz. [Intune Ile PKCS sertifikalarını yapılandırma ve kullanma](../protect/certficates-pfx-configure.md).

Aşağıdakiler cihazlar için geçerlidir:
- Android kurumsal tam yönetilen (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631---"></a>İOS/ıpados ve macOS cihazları için VPN bağlantı türü olarak NetMotion kullanma<!-- 1333631 -->
Bir VPN profili oluşturduğunuzda netmotion, bir VPN bağlantı türü olarak kullanılabilir (**cihazlar**  >  **cihaz yapılandırması**  >  **Create profile**  >  **iOS/ıpados** veya **MacOS** for platform > **VPN** for platform > bağlantı türü için **netmotion** ).

Intune 'da VPN profilleri hakkında daha fazla bilgi için bkz. VPN [sunucularına bağlanmak IÇIN VPN profilleri oluşturma](../configuration/vpn-settings-configure.md).

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS
- macOS

### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024---"></a>Windows 10 Wi-Fi profilleri için daha fazla korunan Genişletilebilir Kimlik Doğrulama Protokolü (PEAP) seçenekleri<!-- 3805024 -->
Windows 10 cihazlarında, Wi-Fi bağlantılarının kimliğini doğrulamak için Genişletilebilir Kimlik Doğrulama Protokolü (EAP) kullanarak Wi-Fi profilleri oluşturabilirsiniz (**cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  **Windows 10 and later** profil > **Enterprise**için **Wi-Fi** >. Korumalı EAP (PEAP) seçeneğini belirlediğinizde kullanılabilir yeni ayarlar vardır:

- **PEAP aşamasında sunucu doğrulaması gerçekleştirme 1**: PEAP anlaşma aşaması 1 ' de, cihazlar sertifikayı doğrular ve sunucuyu doğrular.
  - **PEAP aşaması 1 ' de sunucu doğrulaması için Kullanıcı Istemlerini devre dışı bırak**: PEAP anlaşma aşaması 1 ' de, Kullanıcı tarafından güvenilen sertifika yetkilileri IÇIN yeni PEAP sunucularının yetkilendirilmesini isteyen istemler gösterilmez.
- **Şifreleme bağlaması gerektir**: PEAP anlaşması sırasında şifre BAĞLAMAYı kullanmayan PEAP sunucularıyla bağlantıları engeller.

Şu anda yapılandırabileceğiniz ayarları görmek için [Windows 10 ve üzeri cihazlar Için Wi-Fi ayarları ekle](../configuration/wi-fi-settings-windows.md)' ye gidin.

Aşağıdakiler cihazlar için geçerlidir: 
- Windows 10 ve üzeri

### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576---"></a>MacOS Microsoft Enterprise SSO eklentisini yapılandırma<!-- 5627576 -->
Microsoft Azure AD ekibi, macOS 10.15 + kullanıcılarına Microsoft uygulamalarına, kuruluş uygulamalarına ve Apple 'ın SSO özelliğini destekleyen ve Azure AD 'yi kullanarak kimlik doğrulaması yapan, tek bir oturum açma işlemiyle erişim elde etmesine izin vermek için bir yeniden yönlendirme çoklu oturum açma (SSO) uygulama uzantısı oluşturdu. Microsoft Enterprise SSO eklentisi sürümü sayesinde, SSO uzantısını yeni Microsoft Azure AD uygulama uzantısı türüyle**yapılandırabilirsiniz (cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  profil için**MacOS** for platform > **cihaz özellikleri** > **Çoklu oturum açma uygulama** uzantısı > SSO uygulama uzantısı türü > **Microsoft Azure AD**).

Microsoft Azure AD SSO uygulama uzantısı türüyle SSO sağlamak için, kullanıcıların macOS cihazlarındaki Şirket Portalı uygulamasını yüklemesi ve üzerinde oturum açması gerekir. 

MacOS SSO uygulama uzantıları hakkında daha fazla bilgi için bkz. [Çoklu oturum açma uygulama uzantısı](../configuration/device-features-configure.md#single-sign-on-app-extension).

Aşağıdakiler cihazlar için geçerlidir:
- macOS 10,15 ve üzeri

### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991---"></a>Microsoft Enterprise SSO eklentisiyle diğer iOS/ıpados uygulamalarında SSO uygulama uzantılarını kullanın<!-- 7369991 -->
[Apple cihazları Için Microsoft ENTERPRISE SSO eklentisi](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) , SSO uygulama uzantılarını destekleyen tüm uygulamalarla birlikte kullanılabilir. Intune 'da bu özellik, eklentinin Apple cihazları için Microsoft kimlik doğrulama kitaplığı 'nı (MSAL) kullanmayan Mobile iOS/ıpados uygulamalarıyla birlikte çalışacağı anlamına gelir. Uygulamaların MSAL kullanması gerekmez, ancak Azure AD uç noktalarında kimlik doğrulaması yapması gerekir.

İOS/ıpados uygulamalarınızı eklentiyle birlikte SSO 'yu kullanacak şekilde yapılandırmak için bir iOS/ıpados yapılandırma profiline uygulama paketi tanımlayıcıları**ekleyin (cihaz**  >  **yapılandırma**  >  **Create profile**  >  **iOS/iPadOS** > > profilleri, **Device features** SSO uygulama uzantısı türü > uygulama paketi kimlikleri) için **Çoklu oturum açma uygulama uzantısı**  >  **Microsoft Azure AD** **App bundle IDs**

Yapılandırabileceğiniz geçerli SSO uygulama uzantısı ayarlarını görmek için [Çoklu oturum açma uygulaması uzantısına](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)gidin.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## <a name="device-management"></a>Cihaz yönetimi

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

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>MacOS cihazlarına yazılım güncelleştirmeleri dağıtma <!-- 3194876 -->
MacOS cihazları gruplarına yazılım güncelleştirmeleri dağıtabileceksiniz. Bu özellik kritik, bellenim, yapılandırma dosyası ve diğer güncelleştirmeleri içerir. Güncelleştirmeleri bir sonraki cihaz iadede gönderebilecek veya zaman içinde güncelleştirmeleri dağıtmak için haftalık bir zamanlama seçebileceğiniz şekilde ayarlayabilirsiniz. Bu, standart çalışma saatleri dışında veya yardım masanıza tam olarak çalıştırıldığında cihazları güncelleştirmek istediğinizde yardımcı olur. Ayrıca güncelleştirmelerin dağıtıldığı tüm macOS cihazlarının ayrıntılı bir raporunu alırsınız. Belirli güncelleştirmelerin durumlarını görmek için, raporu cihaz başına temelinde inceleyebilirsiniz.

### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322---"></a>Apple VPP belirtecinin silinmesinden önce ilişkili lisanslar iptal edildi<!--6195322 -->
Gelecekteki bir güncelleştirmede, Microsoft Endpoint Manager 'da bir Apple VPP belirtecini sildiğinizde, bu belirteçle ilişkilendirilen tüm Intune tarafından atanan lisanslar silinmeden önce otomatik olarak iptal edilir.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI uyumluluk raporu şablonu V 2.0<!-- 636958  -->
Yöneticiler, Power BI uyumluluk raporu şablonu sürümünü V 1.0 'dan V 2.0 'a güncelleştirebilir. V 2.0, gelişmiş bir tasarım, Ayrıca, şablonun bir parçası olarak ortaya çıkacak hesaplamalarda ve verilerde yapılan değişiklikleri içerir. İlgili bilgiler için bkz. [Power BI veri ambarına bağlanma](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Güvenlik

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Symantec Endpoint Security ve Check Point sandblast için uygulama koruma ilkesi desteği<!--  4452423, 4731168 -->

Ekim 2019 ' de Intune uygulama koruma ilkesi, Microsoft Threat Defense iş ortaklarından (MTD iş ortakları) bazılarının verilerini kullanma özelliğini ekledi. Bir cihazın sistem durumuna bağlı olarak kullanıcının şirket verilerini engellemek veya seçmeli olarak silmek üzere bir uygulama koruma İlkesi kullanmak için aşağıdaki iş ortakları için destek ekliyoruz:

- **Check Point sandblast** for Android, IOS ve ıpados
- Android, iOS ve ıpados üzerinde **Symantec uç nokta güvenliği**

MTD iş ortaklarıyla uygulama koruma ilkesi kullanma hakkında daha fazla bilgi için bkz. [Intune Ile mobil tehdit savunması uygulama koruma Ilkesi oluşturma](../protect/mtd-app-protection-policy.md).

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP, güvenlik açığı ayrıntılarıyla Endpoint Manager güvenlik görevi oluşturuyor<!-- 5568193  -->
Microsoft Defender ATP 'de tehdit ve güvenlik açığı yönetimi (TVM) cihazlarda yanlış yapılandırılmış güvenlik ayarlarını bulur. Yöneticiler bu bilgileri güvenlik açığı olan cihazları güncelleştirmek için kullanır.

Yakında, Microsoft Defender ATP, güvenlik açığı ayrıntıları ile bir Endpoint Manager güvenlik görevi (**Endpoint Manager**  >  **uç nokta güvenlik**  >  **Güvenlik görevleri**) oluşturabilir ve etkilenen cihazları gösterebilir. BT yöneticileri güvenlik görevini kabul edebilir ve gerekli yapılandırmayı dağıtabilir. 

Güvenlik görevleri hakkında daha fazla bilgi için bkz. [Microsoft Defender ATP tarafından tanımlanan güvenlik açıklarını düzeltmek Için Intune kullanma](../protect/atp-manage-vulnerabilities.md).

### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119----"></a>Endpoint Security virüsten koruma ilkesi dışlamaları için değişiklikler<!--5583940, 6018119  -->
Endpoint Security virüsten koruma ilkesinin bir parçası olarak yapılandırdığınız Microsoft Defender virüsten koruma dışlama listelerini yönetmek için iki değişiklik sunuyoruz. (**Uç nokta güvenliği**  >  **Virüsten koruma**  >  **Ilke oluştur**  >  Platform için **Windows 10 ve üzeri** ). Bu iki değişiklik, ilkeler arasındaki çakışmaların önlenmesine yardımcı olur ve çakışma durumunda olan mevcut ilkeler artık dışlamaları listesi için çakışmaya neden olmaz:

- İlk olarak, Windows 10 ve üzeri için yeni bir profil türü ekliyoruz; **Microsoft Defender virüsten koruma dışlamaları**.  Bu yeni profil türü yalnızca, Microsoft Defender 'ın taramasını istemediğiniz bir Defender *işlem*, *Dosya Uzantısı*ve *Dosya* ve *klasör* listesini belirtmek için ayarları içerir. Bu, dışlama listelerinizi, diğer ilke yapılandırmalarından ayırarak yönetimini basitleştirmenize yardımcı olabilir.
- İkinci değişiklik, farklı profillerde tanımladığınız dışlamaları listesinin, belirli bir kullanıcı veya cihaza uygulanan bireysel ilkelere bağlı olarak, her bir cihaz veya Kullanıcı için tek bir Dışlamadır listesine birleştirilecektir. Örneğin, üç ayrı ilke ile bir kullanıcıyı hedeflediğinizde, bu üç ilkenin dışlama listeleri, daha sonra kullanıcıya uygulanan Microsoft Defender virüsten koruma dışlamaları 'nın tek bir üst kümesi ile birleştirilir. Bu birleştirme, yeni profil türünden, *Microsoft Defender virüsten koruma* profilinde yapılandırılmış olan tüm mevcut ilkelerden ve ekleme dışlamaları listesini içerir.



<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.
