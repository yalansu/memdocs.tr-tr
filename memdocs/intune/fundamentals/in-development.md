---
title: Geliştirme-Microsoft Intune
titleSuffix: ''
description: Geliştirmede Microsoft Intune Özellikler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f910320e59c12f34570ff6d354bfb8f6934a9e66
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406388"
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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Mac için Şirket Portalı 'de birden çok hesap desteği<!-- 5779449  -->
MacOS cihazlarındaki Şirket Portalı artık Kullanıcı hesaplarını önbelleğe alır, oturum açma daha kolay hale getirir. Kullanıcıların, uygulamayı her başlattığında artık Şirket Portalı oturum açması gerekmez. Ayrıca, birden çok kullanıcı hesabı önbelleğe alınmışsa, kullanıcıların kullanıcı adını girmesi gerekmiyorsa Şirket Portalı bir hesap seçici görüntülenir. 

### <a name="auto-update-vpp-available-apps---3640511----"></a>VPP ile kullanılabilen uygulamaları otomatik güncelleştirme<!-- 3640511  -->
Toplu satın alma programı (VPP) kullanılabilir uygulamalar olarak yayımlanan uygulamalar, **otomatik uygulama GÜNCELLEŞTIRMELERI** VPP belirteci için etkinleştirildiğinde otomatik olarak güncelleştirilir. Şu anda VPP ile kullanılabilir uygulamalar otomatik olarak güncelleştirmez. Bunun yerine, son kullanıcılar Şirket Portalı gitmeli ve daha yeni bir sürüm varsa uygulamayı yeniden yüklemektir. Ancak gerekli uygulamalar şu anda otomatik güncelleştirmeleri destekler.

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>Şirket Portalı self servis cihaz eylemlerini özelleştirme<!--4393379  -->
Şirket Portalı uygulamasında ve Web sitesinde son kullanıcılara gösterilen kullanılabilir self servis cihaz eylemlerini özelleştirebilirsiniz. İstenmeyen cihaz eylemlerini önlemeye yardımcı olmak için, **Kiracı Yönetimi**  >  **özelleştirmesi**  >  **Oluştur**  >  **Gizle özellikleri**' ni seçerek Şirket portalı uygulaması için bu ayarları yapılandırabileceksiniz. Aşağıdaki eylemler kullanılabilir:
- Kurumsal Windows cihazında **Kaldır** düğmesini gizleyin.
- Kurumsal Windows cihazlarında **sıfırlama** düğmesini gizleyin.
- Kurumsal iOS cihazlarında **sıfırlama** düğmesini gizleyin.
- Kurumsal iOS cihazlarda **Kaldır** düğmesini gizleyin.

Daha fazla bilgi için, [Şirket portalı Kullanıcı self servis cihaz eylemleri](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal)bölümüne bakın.

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Şirket Portalı Azure AD kurumsal veya Office Online uygulamalarının birleştirilmiş teslimi<!--4404429 -->
Şirket Portalı Azure AD kurumsal veya Office Online uygulamalarının görüntülenmesini (**gizleyebilir** veya **gösterebilirsiniz**) mümkün olacaktır. Her Kullanıcı, seçilen Microsoft hizmetinden Uygulama Kataloğu 'nun tamamını görür. Varsayılan olarak, her bir ek uygulama kaynağı **gizleyecek**şekilde ayarlanır. Bu özellik ilk olarak 2005 sürümündeki Şirket Portalı Web sitesinde, Windows, iOS/ıpados ve daha sonra izlenmesi beklenen macOS şirket portallarındaki destek ile etkili olacaktır. Bu gelecekteki ayarı bulmak için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde **Kiracı Yönetimi**  >  **özelleştirmesi** ' nı seçin. İlgili bilgiler için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>Şirket Portalı Intune belgelerini arama<!-- 1736480 -->
Artık doğrudan macOS uygulamasındaki Şirket Portalı Intune belgelerini arayabilirsiniz. Menü çubuğunda **Yardım**  >  **Ara** ' yı seçin ve sorularınızın yanıtlarını hızlı bir şekilde bulmak için aramanızın anahtar sözcüklerini girin.

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Android için Şirket Portalı, kullanıcıların iş profili kaydından sonra uygulama almasını yönlendirecektir <!-- 6103999  -->
Kullanıcıların uygulamaları bulmasını ve yüklemesini kolaylaştırmak için Şirket Portalı 'teki uygulama içi Kılavuzu geliştiriyoruz.  İş profili yönetimine kaydolduktan sonra, kullanıcılar, Google Play 'in hatalı sürümünde önerilen uygulamaları bulabilecekleri bir ileti görür. Kullanıcılar ayrıca soldaki Şirket Portalı çekmecede yeni bir **uygulamalar al** bağlantısı görür. Bu yeni ve geliştirilmiş deneyimlere yönelik bir yöntem oluşturmak için, **uygulamalar** sekmesi kaldırılır. 

### <a name="android-company-portal-user-experience---5736084---"></a>Android Şirket Portalı Kullanıcı deneyimi<!-- 5736084 -->
Android Şirket Portalı 2005 sürümünde, bir uygulama koruma ilkesi tarafından uyarı veren, blok veya temizleme yapan Android cihazların son kullanıcıları yeni bir kullanıcı deneyimi görür. Son kullanıcılar, geçerli iletişim kutusu deneyimi yerine, uyarı, blok veya silme nedeninizi ve sorunu düzeltmek için gereken adımları açıklayan bir tam sayfa mesajı görür. Daha fazla bilgi için, bkz. Microsoft Intune [Android cihazları Için uygulama koruma deneyimi](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) ve [Android uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-android.md).


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

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>MacOS cihazlarında sistem uzantılarını yapılandırma<!-- 6255624  -->
MacOS cihazlarında, çekirdek düzeyinde ayarları yapılandırmak için bir çekirdek uzantıları profili oluşturabilirsiniz (**cihaz**  >  **yapılandırma profilleri**  >  **macOS** for platform > Platform **uzantıları** for profile). Apple, daha sonra çekirdek uzantılarını kullanımdan kaldırır ve sonraki sürümlerde sistem uzantıları ile değiştirmektir. Sistem uzantıları Kullanıcı alanında çalışır ve çekirdeğe erişim vermez. Amaç, güvenliği artırmak ve daha fazla Son Kullanıcı denetimi sağlamak, ancak saldırıları çekirdek düzeyinde sınırlandırmaktır. Her iki çekirdek uzantısı ve sistem uzantısı, kullanıcıların işletim sisteminin yerel yeteneklerini genişleten uygulama uzantılarını yüklemelerine izin verir.

Intune 'da, hem çekirdek uzantılarını hem de sistem uzantılarını yapılandırabilirsiniz (**cihaz**  >  **yapılandırma profilleri**  >  **MacOS** for platform >, profil için **sistem uzantıları** ). Çekirdek uzantıları, 10.13.2 ve üzeri için geçerlidir. Sistem uzantıları 10,15 ve üzeri sürümler için geçerlidir. MacOS 10,15 ' den macOS 10.15.4, çekirdek uzantıları ve sistem uzantıları yan yana çalışabilir. 

MacOS cihazlarındaki çekirdek uzantıları hakkında bilgi edinmek için bkz. [MacOS çekirdek uzantıları ekleme](../configuration/kernel-extensions-overview-macos.md).

Şunlara uygulanır:
- macOS 10,15 ve üzeri

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Cihaz kaydı

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Kendi cihazlarını getir, dağıtmak için VPN kullanabilir<!--5015344 -->
Bu özellik gecikebilir.

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>Otomatik cihaz eşitleme aralığı, 12 saate kadar<!--3077535 -->
Apple 'ın otomatik cihaz kaydı için, Intune ile Apple Business Manager arasındaki otomatik cihaz eşitleme aralığı, 24 saatten 12 saate kadar azaltılır. Eşitleme hakkında daha fazla bilgi için bkz. [yönetilen cihazları eşitleme](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>HoloLens 2 cihazları için Autopilot desteği<!--6305220-->
Windows Autopilot, Hololens 2 cihazlarını destekleyecektir. Intune 'da Autopilot kullanma hakkında daha fazla bilgi için bkz. [Windows Autopilot kullanarak Intune 'Da Windows cihazlarını kaydetme](../enrollment/enrollment-autopilot.md).

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>Kayıt kısıtlamaları kapsam etiketlerini destekleyecektir<!--4209550 -->
Kayıt kısıtlamalarına kapsam etiketleri atayabileceksiniz. Bunu yapmak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **Kayıt kısıtlamaları**  >  **oluşturma kısıtlaması**' na gidin. Her iki kısıtlama türünü de oluşturun ve **kapsam etiketleri** sayfasını görürsünüz.

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


### <a name="macos-script-support---6376978----"></a>macOS betik desteği<!-- 6376978  -->
MacOS için betik desteği genel kullanıma sunuldu. Ayrıca, Apple 'ın otomatik cihaz kaydına (eski adıyla Aygıt Kayıt Programı) kaydedilmiş Kullanıcı tarafından atanan betikler ve macOS cihazları için de destek ekleyeceğiz. Daha fazla bilgi için bkz. [Intune 'Da macOS cihazlarında Shell betikleri kullanma](../apps/macos-shell-scripts.md).

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

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Android cihazlarda DıŞA ınpurebred için türetilmiş kimlik bilgileri desteği<!--4839592 -->
Android kurumsal tam olarak yönetilen cihazlarda (**kiracı yönetim**bağlayıcıları ve belirteçleri türetilmiş kimlik bilgileri), bir [türetilmiş kimlik bilgileri](../protect/derived-credentials.md) sağlayıcısı olarak, *reberkred* 'yi kullanabileceksiniz  >  **Connectors and tokens**  >  **Derived Credentials**. DıPUREBRED için türetilmiş bir kimlik bilgisi alma desteği dahil edilir. Uygulama kimlik doğrulaması, Wi-Fi, VPN veya S/MIME imzalama ve/veya şifrelemeyi destekleyen uygulamalarla şifreleme için türetilmiş bir kimlik bilgisi kullanabileceksiniz. 

Nisan 'da Intune, türetilmiş kimlik bilgileri için *Entrust Datacard* ve *ıntercede* sağlayıcıları için destek ekledi. 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>MacOS cihazları için Gizlilik Tercihleri ayarları<!-- 2934232 --> 
MacOS Catalina 10,15 sürümü sayesinde, Apple yeni güvenlik ve gizlilik iyileştirmeleri ekledi. Varsayılan olarak, uygulamalar ve süreçler Kullanıcı izni olmadan belirli verilere erişemez. Kullanıcılar onay sağlamıyorsa, uygulamalar ve süreçler çalışmayabilir. Intune, macOS 10,14 ve üstünü çalıştıran cihazlarda son kullanıcılar adına, BT yöneticilerinin veri erişimine izin vermesini veya bu izni vermemeyi sağlayan ayarlar için destek ekliyor. Bu ayarlar, uygulamaların ve işlemlerin düzgün şekilde çalışmaya devam etmesini ve son kullanıcıların deneyimlerine yönelik istem sayısını azaltmasını sağlar.


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Uç nokta güvenliğine ait ilkelerinizi çoğaltın<!-- 5892558   -->
Microsoft Endpoint Manager Yönetim Merkezi 'nin uç nokta güvenlik düğümünde oluşturduğunuz bir ilkeyi seçebileceksiniz ve sonra bir kopya oluşturmak için onu çoğaltabilirsiniz.  Bu ilkeler, sizin için oluşturduğunuz ilkeleri içerir: 

- Virüsten Koruma
- Disk şifrelemesi
- Güvenlik duvarı
- Uç nokta algılama ve yanıt
- Saldırı yüzeyi azaltma
- Hesap koruması

Çoğaltma, özgün ilkenin bir kopyasını oluşturacak ve daha sonra yeniden adlandırabilir ve düzenleyebilirim. Kopya, orijinalden atamalar içermez.

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Uyumsuzluk için eylem olarak anında iletme bildirimleri gönder <!-- 1733150   -->
İOS ve Android platformları için Şirket Portalı uygulaması aracılığıyla uygulama anında iletme bildirimi gönderecek uyumsuzluk için yeni bir eylem ekliyoruz. Kullanıcılar Şirket Portalı uygulamasını Başlatan bildirimlere tıklayabilir ve bu nedenle uyumsuz oldukları nedeni görüntüler. Yöneticiler, **cihaz**  >  **uyumluluk ilkeleri**  >  **ilke oluştur**' a giderek ve ardından uygulama anında iletme bildirimi gönderecek *eylemi* seçerek Microsoft Endpoint Manager Yönetim merkezinde uyumsuzluk için bu yeni eylemi yapılandırabilecektir. 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Uç nokta güvenlik duvarı ilkesi için yeni profil<!-- 5653324   -->
Önizleme olarak, Intune 'un uç nokta güvenliğine yönelik güvenlik duvarı ilkesine Windows 10 ve üzeri için ek bir profil ekliyoruz (**uç nokta güvenlik**  >  **güvenlik duvarı**  >  **ilke oluştur** > **Windows 10 ve üstünü**seçin). 

Bu yeni profilin her örneği en fazla 150 özel *Microsoft Defender güvenlik duvarı kuralını*destekler. Microsoft Defender güvenlik duvarı kuralları profili, Windows 10 ' da bağlantı noktalarına ve uygulamalara izin vermek veya bunları engellemek için ayrıntılı Windows güvenlik duvarı kuralları tanımlamanızı sağlar.

<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.



