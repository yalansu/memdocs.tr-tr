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
ms.openlocfilehash: caec61f93b3b651c18d2c4fd81467d462de75fc1
ms.sourcegitcommit: cb9b452f8e566fe026717b59c142b65f426e5033
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86491244"
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

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS Şirket Portalı, Apple 'ın Kullanıcı benzeşimi olmadan otomatik cihaz kaydını destekleyecektir<!-- 7282707  --> 
iOS Şirket Portalı, Apple 'ın otomatik cihaz kaydı kullanılarak kaydedilen cihazlarda atanmış bir Kullanıcı gerekmeden desteklenecektir. Son Kullanıcı iOS Şirket Portalı, cihaz benzeşimi olmadan kaydedilen bir iOS/ıpados cihazında birincil kullanıcı olarak kurmak için oturum açabilir. Otomatik cihaz kaydı hakkında daha fazla bilgi için bkz. [Apple 'ın otomatik cihaz kaydı Ile iOS/ıpados cihazlarını otomatik olarak kaydetme](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Şirket Portalı Configuration Manager uygulama desteği ekler<!-- 4297660 -->
Şirket Portalı artık Configuration Manager uygulamalarını desteklemektedir. Bu özellik, son kullanıcıların ortak yönetilen müşteriler için Şirket Portalı hem Configuration Manager hem de Intune tarafından dağıtılan uygulamaları görmesini sağlar. Bu destek, yöneticilerin farklı Son Kullanıcı Portalı deneyimlerini birleştirmesine yardımcı olur. Daha fazla bilgi için bkz. [ortak yönetilen cihazlarda şirket portalı uygulamasını kullanma](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Cihaz yapılandırması

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Üçüncü taraf MDM iş ortaklarından cihaz uyumluluk durumunu ayarlama<!-- 6361689   -->
Üçüncü taraf MDM çözümlerine sahip olan Microsoft 365 müşteriler, Microsoft Intune cihaz uyumluluk hizmeti ile tümleştirme yoluyla iOS ve Android üzerinde Microsoft 365 uygulamalar için koşullu erişim ilkelerini zorlayabilir. Üçüncü taraf MDM satıcısı, Intune cihaz uyumluluk hizmetinden yararlanarak cihaz uyumluluk verilerini Intune 'a gönderir. Daha sonra Intune, cihazın güvenilir olup olmadığını ve Azure AD 'de koşullu erişim özniteliklerini ayarlamanızı sağlayacak şekilde değerlendirilir.  Müşterilerin, Microsoft Endpoint Manager yönetim merkezi veya Azure AD portalı içinden Azure AD koşullu erişim ilkeleri ayarlaması gerekecektir.  

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

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Windows 10 cihazları için yeni birleştirme mantığı<!--179048-->
Günümüzde, bir müşteri bir cihazı yeniden görüntüler ve sonra yeniden kaydederse, Microsoft Endpoint Manager Yönetici konsolunda cihaz için birden çok kayıt görünür. Yeni birleştirme mantığı, Windows 10 cihazlarında bu tür yinelenen kayıtları birleştirmek için geliştirme aşamasındadır.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>MacOS cihazlarına yazılım güncelleştirmeleri dağıtma <!-- 3194876 -->
MacOS cihazları gruplarına yazılım güncelleştirmeleri dağıtabileceksiniz. Bu özellik kritik, bellenim, yapılandırma dosyası ve diğer güncelleştirmeleri içerir. Güncelleştirmeleri bir sonraki cihaz iadede gönderebilecek veya zaman içinde güncelleştirmeleri dağıtmak için haftalık bir zamanlama seçebileceğiniz şekilde ayarlayabilirsiniz. Bu, standart çalışma saatleri dışında veya yardım masanıza tam olarak çalıştırıldığında cihazları güncelleştirmek istediğinizde yardımcı olur. Ayrıca güncelleştirmelerin dağıtıldığı tüm macOS cihazlarının ayrıntılı bir raporunu alırsınız. Belirli güncelleştirmelerin durumlarını görmek için, raporu cihaz başına temelinde inceleyebilirsiniz.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI uyumluluk raporu şablonu V 2.0<!-- 636958  -->
Yöneticiler, Power BI uyumluluk raporu şablonu sürümünü V 1.0 'dan V 2.0 'a güncelleştirebilir. V 2.0, gelişmiş bir tasarım, Ayrıca, şablonun bir parçası olarak ortaya çıkacak hesaplamalarda ve verilerde yapılan değişiklikleri içerir. İlgili bilgiler için bkz. [Power BI veri ambarına bağlanma](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Özelleştirme İlkeleri için kapsam etiketi desteği<!--6182440 -->
Özelleştirme ilkelerine kapsam etiketleri atayabileceksiniz. Bunu yapmak için, kapsam etiketleri yapılandırma seçeneklerini göreceğiniz [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **kiracı yönetim** >  **özelleştirmesi** ' **Scope tags** na gidin.

<!-- ***********************************************-->
## <a name="security"></a>Güvenlik

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Symantec Endpoint Security ve Check Point sandblast için uygulama koruma ilkesi desteği<!--  4452423, 4731168 -->

Ekim 2019 ' de Intune uygulama koruma ilkesi, Microsoft Threat Defense iş ortaklarından (MTD iş ortakları) bazılarının verilerini kullanma özelliğini ekledi. Bir cihazın sistem durumuna bağlı olarak kullanıcının şirket verilerini engellemek veya seçmeli olarak silmek üzere bir uygulama koruma İlkesi kullanmak için aşağıdaki iş ortakları için destek ekliyoruz:

- **Check Point sandblast** for Android, IOS ve ıpados
- Android, iOS ve ıpados üzerinde **Symantec uç nokta güvenliği**

MTD iş ortaklarıyla uygulama koruma ilkesi kullanma hakkında daha fazla bilgi için bkz. [Intune Ile mobil tehdit savunması uygulama koruma Ilkesi oluşturma](../protect/mtd-app-protection-policy.md).


<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.
