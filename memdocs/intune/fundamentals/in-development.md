---
title: Geliştirme-Microsoft Intune
titleSuffix: ''
description: Geliştirmede Microsoft Intune Özellikler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1f261d8d61fc2c4273ae8f137a43bb6c607430d
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002707"
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


<!-- ***********************************************-->
## <a name="device-configuration"></a>Cihaz yapılandırması

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Android kurumsal tam olarak yönetilen cihazlar (COBO) için PKCS sertifika profilleri oluşturma<!-- 4839686 -->
Android kurumsal cihaz sahibine ve iş profili cihazlarına sertifika dağıtmak için PKCS sertifika profilleri oluşturabilirsiniz (**cihaz**  >  **yapılandırma profilleri**  >  **Create profile**  >  yalnızca profil için **PKCS** > için SDK kurumsal **> cihaz sahibini**veya **Android kurumsal > iş profilini** oluşturur).

Yakında, Android kurumsal tam olarak yönetilen cihazlar için PKCS sertifika profilleri oluşturabileceksiniz. Intune PFX Sertifika bağlayıcısı gereklidir. SCEP kullanmıyorsanız ve yalnızca PKCS kullanıyorsanız, yeni PFX bağlayıcısını yükledikten sonra NDES bağlayıcısını kaldırabilirsiniz. Yeni PFX Bağlayıcısı PFX dosyalarını içeri aktarır ve PKCS sertifikalarını tüm platformlara dağıtır.

PKCS sertifikaları hakkında daha fazla bilgi için bkz. [Intune Ile PKCS sertifikalarını yapılandırma ve kullanma](../protect/certficates-pfx-configure.md).

Aşağıdakiler cihazlar için geçerlidir:
- Android kurumsal tam yönetilen (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>Android kurumsal iş profili cihazları için NetMotion 'ı VPN bağlantı türü olarak kullanma<!-- 7764263 -->
Bir VPN profili oluşturduğunuzda netmotion bir VPN bağlantı türü olarak kullanılabilir (**cihazlar**  >  **cihaz yapılandırması**  >  **profil oluşturma**  >  **Android kurumsal iş profili** için platform > bağlantı için **netmotion** > **VPN** ).

Intune 'da VPN profilleri hakkında daha fazla bilgi için bkz. VPN [sunucularına bağlanmak IÇIN VPN profilleri oluşturma](../configuration/vpn-settings-configure.md).

Aşağıdakiler cihazlar için geçerlidir:
- Android kurumsal iş profili

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>Android Cihaz Yöneticisi için cihaz kısıtlama profillerindeki parola ayarlarına yönelik değişiklikler<!-- 7662279  --> 
*Android Cihaz Yöneticisi*için *cihaz kısıtlama* ve *Uyumluluk* ilkeleri için parola ayarlarına yönelik birkaç değişiklik sunuyoruz. (**Cihazlar**  >  **Yapılandırma profilleri**  >  **Profil oluştur**  >  **Cihaz kısıtlamaları** ve **cihazların**  >  **uyumluluk ilkeleri**  >  **ilke oluştur**) Bu değişiklikler, Intune 'un Android sürüm 10 ve üzerinde değişikliklere uyum sağlaması için, parolaların ayarlarının beklendiği gibi cihazlara uygulanmaya devam etmesine yardımcı olur.
 
Değişiklikler şunları içerir:
- **Parola**için üst düzey seçeneğinin kaldırılması.  
- Ayarlar, hangi cihazlara uygulanacağını temel alan bölümlerle yeniden düzenlenecektir.
- Parola **türü** , parola uzunluğunun geçerli olduğu bir değere yapılandırılmadığı takdirde, **En düşük parola uzunluğu** kullanım için devre dışı bırakılır.
- Etiketlere ve örnek metne yönelik ek güncelleştirmeler.

Bu değişiklikler, ayarlar için Kullanıcı arabirimine uygulanır ve mevcut profilleri etkilemez. 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Cihaz kaydı

### <a name="ending-support-for-ios-11--7327321---"></a>İOS 11 için destek bitiriliyor<!--7327321 -->
İOS 14 yayımlandıktan sonra, Intune kaydı ve Şirket Portalı uygulaması iOS sürümlerini 12 ve üstünü destekleyecektir. Eski sürümler desteklenmez, ancak ilkeleri almaya devam edecektir.

### <a name="ending-support-for-macos-1012--7327326---"></a>MacOS 10,12 için destek bitiriliyor<!--7327326 -->
MacOS 11 yayımlandıktan sonra, Intune kaydı ve Şirket Portalı macOS 10,13 ve sonraki sürümlerini destekler. Eski sürümler desteklenmez.


<!-- ***********************************************-->
## <a name="device-management"></a>Cihaz yönetimi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>KCG cihazları için PowerShell betikleri desteği<!-- 1862833  -->
PowerShell betikleri, Intune 'da Azure AD kayıtlı cihazlarını destekleyecektir. PowerShell hakkında daha fazla bilgi için bkz. [Intune 'Da Windows 10 cihazlarda PowerShell betiklerini kullanma](../apps/intune-management-extension.md). Bu işlevsellik, Windows 10 Home Edition çalıştıran cihazları desteklemez.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics, cihaz ayrıntıları günlüğünü içerecektir<!--6014987  -->
Intune cihaz ayrıntı günlükleri, **raporlar**  >  **Log Analytics**' te kullanılabilir. Özel sorgular ve Azure çalışma kitapları oluşturmak için cihaz ayrıntılarını ilişkilendirebilirler.

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Kiracı iliştirme: yönetim merkezinden betikleri çalıştırma<!--7220536, CM6234688 -->
Şirket içi Configuration Manager [Çalıştır](../../configmgr/apps/deploy-use/create-deploy-scripts.md) özelliğinin gücünü Microsoft Endpoint Manager yönetim merkezine getirebileceksiniz. Yardım masası gibi ek personbuna, tek Configuration Manager yönetilen bir cihaza karşı, buluttan PowerShell betikleri çalıştırmasına izin verin. Bu, bu yeni ortama Configuration Manager yöneticisi tarafından önceden tanımlanmış ve onaylanmış olan PowerShell betiklerinin tüm geleneksel avantajlarını sağlar. Daha fazla bilgi için bkz. [Teknik önizleme 2005 Configuration Manager](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>MacOS cihazlarına yazılım güncelleştirmeleri dağıtma <!-- 3194876 -->
MacOS cihazları gruplarına yazılım güncelleştirmeleri dağıtabileceksiniz. Bu özellik kritik, bellenim, yapılandırma dosyası ve diğer güncelleştirmeleri içerir. Güncelleştirmeleri bir sonraki cihaz iadede gönderebilecek veya zaman içinde güncelleştirmeleri dağıtmak için haftalık bir zamanlama seçebileceğiniz şekilde ayarlayabilirsiniz. Bu, standart çalışma saatleri dışında veya yardım masanıza tam olarak çalıştırıldığında cihazları güncelleştirmek istediğinizde yardımcı olur. Ayrıca güncelleştirmelerin dağıtıldığı tüm macOS cihazlarının ayrıntılı bir raporunu alırsınız. Belirli güncelleştirmelerin durumlarını görmek için, raporu cihaz başına temelinde inceleyebilirsiniz.

<!-- ***********************************************-->
## <a name="intune-apps"></a>Intune uygulamaları

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Windows Şirket Portalı Azure AD kurumsal ve Office Online uygulamalarının birleştirilmiş teslimi<!-- 1817861  -->
2006 sürümünde, [Şirket portalı Azure AD kurumsal ve Office Online uygulamalarının birleştirilmiş teslimini](../fundamentals/whats-new.md)duyurduk. Bu özellik Windows Şirket Portalı desteklenecektir. Intune 'un **Özelleştirme** bölmesinde, Windows Şirket portalı hem **Azure AD kurumsal uygulamalarını** hem de **Office Online uygulamalarını** **gizleme** veya **gösterme** seçeneğini belirleyebileceksiniz. Her Son Kullanıcı tüm uygulama kataloglarını seçilen Microsoft hizmetinden görürler. Varsayılan olarak, her bir ek uygulama kaynağı **gizleyecek**şekilde ayarlanır. Bu yapılandırma ayarını bulmak için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde **Kiracı Yönetimi**  >  **özelleştirmesi** ' nı seçersiniz. İlgili bilgiler için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).
 

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



<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.
