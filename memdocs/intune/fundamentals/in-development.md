---
title: Geliştirme-Microsoft Intune
titleSuffix: ''
description: Geliştirmede Microsoft Intune Özellikler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764212"
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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Android için Şirket Portalı, kullanıcıların iş profili kaydından sonra uygulama almasını yönlendirecektir <!-- 6103999  -->
Kullanıcıların uygulamaları bulmasını ve yüklemesini kolaylaştırmak için Şirket Portalı 'teki uygulama içi Kılavuzu geliştiriyoruz.  İş profili yönetimine kaydolduktan sonra, kullanıcılar, Google Play 'in hatalı sürümünde önerilen uygulamaları bulabilecekleri bir ileti görür. Kullanıcılar ayrıca soldaki Şirket Portalı çekmecede yeni bir **uygulamalar al** bağlantısı görür. Bu yeni ve geliştirilmiş deneyimlere yönelik bir yöntem oluşturmak için, **uygulamalar** sekmesi kaldırılır. 

<!-- ***********************************************-->
## <a name="device-configuration"></a>Cihaz yapılandırması

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Cihaz yapılandırma profili ayarları ve değerleri Windows platformları için güncelleştirilecektir<!-- 4091122 -->
Windows platformları için cihaz yapılandırma profilleri oluştururken (**cihaz**  >  **yapılandırma profilleri**  >  **Create profile** platform için herhangi bir **Windows** seçeneği >), bazı ayarlar ve bunların değerleri CSP 'den farklıdır ve kafa karıştırıcı olabilir. Ayar adları ve değerleri daha net olacak şekilde güncelleştirilecektir.

Şunlara uygulanır:

- Windows 10 ve üzeri cihaz yapılandırma profilleri
- Windows holographic for Business cihaz yapılandırma profilleri
- Windows 8.1 cihaz yapılandırma profilleri
- Windows Phone 8,1 cihaz yapılandırma profilleri

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>MacOS Endpoint Protection cihaz yapılandırma ilkesi için yeni Filekasası ayarı<!-- 5459801   -->
[MacOS Endpoint Protection](../protect/endpoint-protection-macos.md) şablonu Içindeki filekasası kategorisine yeni bir ayar ekliyoruz: kurtarma anahtarını gizleyin. (**Cihazlar**  >  **Yapılandırma profilleri**  >  **Profil oluştur**, *Platform* için **MacOS** ' u ve ardından *profil türü*için **uç nokta koruması** ' nı seçin. Bu ayar, Filekasa2 şifrelemesi sırasında son kullanıcıdan kişisel anahtarı gizler. Bir cihaz kullanıcısı, kişisel kurtarma anahtarını iOS şirket portalı uygulamasından veya şifrelenmiş macOS cihazının Şirket portalı Web sitesinden dilediğiniz zaman görüntüleyebilir. Kişisel kurtarma anahtarını görüntülemek için cihaz ayrıntılarına gidebilir ve *Kurtarma anahtarı al*' a tıklayabilirsiniz.

Bu ayar, önceden oluşturulan ilkede kullanılamaz. Bu ayarı kullanmak üzere yapılandırmak için dosya Kasası ilkelerini yeniden oluşturmanız gerekir. 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>Cihaz kaydı

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Kendi cihazlarını getir, dağıtmak için VPN kullanabilir<!--5015344 -->
Bu özellik gecikebilir.

### <a name="shared-ipads-for-business--6367326---"></a>Iş için paylaşılan IPad 'ler<!--6367326 -->
Birden çok çalışanın cihazları paylaşabilmesi için Intune ve Apple Business Manager 'ı kullanarak paylaşılan iPad 'i kolayca ve güvenli bir şekilde ayarlayabilirsiniz. Apple 'ın [paylaşılan iPad](https://developer.apple.com/education/shared-ipad/) 'i, Kullanıcı verilerini korurken birden çok kullanıcı için kişiselleştirilmiş bir deneyim sağlar. Yönetilen bir Apple KIMLIĞI kullanarak, kullanıcılar kuruluşlarındaki paylaşılan iPad 'de oturum açtıktan sonra uygulamalarına, verilerine ve ayarlarına erişebilirler. Paylaşılan iPad, Federasyon kimlikleriyle birlikte çalışmaktadır.

Bu özelliği görmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **iOS**  >  **iOS kayıt**  >  **kayıt programı belirteçleri** ' ne gidin > belirteç seçin * * > **profiller**  >  **Profil oluştur**  >  **iOS**. **Yönetim ayarları** sayfasında, **Kullanıcı benzeşimi olmadan kaydet** ' i seçin ve **paylaşılan iPad** seçeneğini görürsünüz.

**Uygulama hedefi:** ıpados 13,4 ve üzeri. Bu sürüm, kullanıcıların yönetilen bir Apple KIMLIĞI olmadan bir cihaza erişebilmeleri için paylaşılan iPad ile geçici oturumlar için destek ekledi. Oturum kapatma sonrasında cihaz tüm Kullanıcı verilerini siler, böylece cihaz kullanıma hemen kullanılabilir hale gelir ve cihaz temizleme gereksinimini ortadan kaldırır. 

<!-- ***********************************************-->
## <a name="device-management"></a>Cihaz yönetimi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>KCG cihazları için PowerShell betikleri desteği<!-- 1862833  -->
PowerShell betikleri, Intune 'da Azure AD kayıtlı cihazlarını destekleyecektir. PowerShell hakkında daha fazla bilgi için bkz. [Intune 'Da Windows 10 cihazlarda PowerShell betiklerini kullanma](../apps/intune-management-extension.md). Bu işlevsellik, Windows 10 Home Edition çalıştıran cihazları desteklemez.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics, cihaz ayrıntıları günlüğünü içerecektir<!--6014987  -->
Intune cihaz ayrıntı günlükleri, **raporlar**  >  **Log Analytics**' te kullanılabilir. Özel sorgular ve Azure çalışma kitapları oluşturmak için cihaz ayrıntılarını ilişkilendirebilirler.


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


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Uç nokta güvenliğine ait ilkelerinizi çoğaltın<!-- 5892558   -->
Microsoft Endpoint Manager Yönetim Merkezi 'nin uç nokta güvenlik düğümünde oluşturduğunuz bir ilkeyi seçebileceksiniz ve sonra bir kopya oluşturmak için onu çoğaltabilirsiniz.  Bu ilkeler, sizin için oluşturduğunuz ilkeleri içerir: 

- Virüsten Koruma
- Disk şifrelemesi
- Güvenlik duvarı
- Uç nokta algılama ve yanıt
- Saldırı yüzeyini azaltma
- Hesap koruması

Çoğaltma, özgün ilkenin bir kopyasını oluşturacak ve daha sonra yeniden adlandırabilir ve düzenleyebilirim. Kopya, orijinalden atamalar içermez.

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Uç nokta güvenlik duvarı ilkesi için yeni profil<!-- 5653324   -->
Önizleme olarak, Intune 'un uç nokta güvenliğine yönelik güvenlik duvarı ilkesine Windows 10 ve üzeri için ek bir profil ekliyoruz (**uç nokta güvenlik**  >  **güvenlik duvarı**  >  **ilke oluştur** > **Windows 10 ve üstünü**seçin). 

Bu yeni profilin her örneği en fazla 150 özel *Microsoft Defender güvenlik duvarı kuralını*destekler. Microsoft Defender güvenlik duvarı kuralları profili, Windows 10 ' da bağlantı noktalarına ve uygulamalara izin vermek veya bunları engellemek için ayrıntılı Windows güvenlik duvarı kuralları tanımlamanızı sağlar.

<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.



