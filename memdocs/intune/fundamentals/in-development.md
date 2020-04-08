---
title: Geliştirme-Microsoft Intune
titleSuffix: ''
description: Geliştirmede Microsoft Intune Özellikler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f53096f25b4bb05b80d11246ac2fa01486f6e42
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808169"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>Microsoft Intune için geliştirme sırasında-Nisan 2020

Hazırlık ve planlamada yardımcı olması için bu sayfada Intune Kullanıcı Arabirimi güncelleştirmeleri ve geliştirme aşamasında olan ancak henüz yayınlanmayan özellikler listelenir. Bu sayfadaki bilgilere ek olarak: 

- Bir değişiklikten önce işlem yapmanız gerektiğini düşünüyorsanız, Office ileti merkezi 'nde tamamlayıcı bir gönderi yayımlayacağız.
- Bir özellik üretim girdiğinde, bir önizleme veya genel kullanıma sunulduktan sonra özellik açıklaması bu [sayfadan yenilikler 'e taşınır.](whats-new.md)
- Bu [sayfa ve yenilikler sayfası düzenli](whats-new.md) aralıklarla güncelleştirilir. Ek güncelleştirmeleri daha sonra denetleyin.
- Stratejik teslim edilebilirler ve zaman çizelgeleri için [Microsoft 365 yol haritasını](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) inceleyin.

> [!NOTE]
> Bu sayfa, gelecekteki bir sürümde Intune özelliklerine ilişkin geçerli beklentilerimizi yansıtır. Tarihler ve bireysel Özellikler değişebilir. Bu sayfa, geliştirmede tüm özellikleri tanımlamaz.

**RSS akışı**: Şu URL 'yi kopyalayıp akış okuyucunuzun içine yapıştırarak bu sayfanın ne zaman güncelleştirileceğini öğrenin: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

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

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Android uygulama yapılandırma ilkelerine güncelleştirme<!-- 6113334  -->
Android uygulama yapılandırma ilkeleri, yöneticilerin bir uygulama yapılandırma profili oluşturmadan önce cihaz kayıt türünü seçmesine olanak tanımak üzere güncelleştirilir. İşlev, kayıt türü (Iş profili veya cihaz sahibi) tabanlı sertifika profillerinin hesabına ekleniyor.  Yayın sonrasında aşağıdakiler gerçekleşir:

- Bu özelliğin, ilkeyle ilişkili herhangi bir sertifika profili olmayan, varsayılan olarak, cihaz kayıt türü için Iş profili ve cihaz sahibi profili olmak üzere oluşturulan mevcut ilkeler.
- Bu özelliğin ilişkili olduğu Sertifika profillerinin bulunduğu sürümden önce oluşturulan mevcut ilkeler, varsayılan olarak yalnızca Iş profili ' dir.
- Yeni bir profil oluşturulduysa ve cihaz kayıt türü için Iş profili ve cihaz sahibi profili seçilirse, bir sertifika profilini uygulama yapılandırma ilkesiyle ilişkilendiremeyeceksiniz.
- Yeni bir profil oluşturulup Iş profili yalnızca seçili ise, cihaz yapılandırması altında oluşturulan Iş profili sertifika ilkeleri kullanılabilir.
- Yeni bir profil oluşturulduysa ve yalnızca cihaz sahibi seçilirse, cihaz yapılandırması altında oluşturulan cihaz sahibi sertifika ilkeleri kullanılabilir.

Mevcut ilkeler yeni sertifikaları düzeltmez veya vermez.

Ayrıca, her iki e-posta yapılandırma türünde Sertifika profillerinin kullanılması da dahil olmak üzere hem Iş profili hem de cihaz sahibi kayıt türleri için çalışacak Gmail ve dokuz e-posta yapılandırma profilleri ekliyoruz.  Iş profillerinin cihaz yapılandırması altında oluşturduğunuz Gmail veya dokuz ilke cihaza uygulanmaya devam eder ve bunları uygulama yapılandırma ilkelerine taşımak gerekli değildir.

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **uygulamalar** > **uygulama yapılandırma**ilkeleri ' ni seçerek uygulama yapılandırma ilkelerini bulabilirsiniz. Uygulama yapılandırma ilkeleri hakkında daha fazla bilgi için bkz. [Microsoft Intune Için uygulama yapılandırma ilkeleri](../apps/app-configuration-policies-overview.md).

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft ekipleri artık macOS için Office 365 Suite 'e eklenmiştir<!-- 5903936  -->
Microsoft Endpoint Manager 'da macOS için Microsoft Office atanan kullanıcılar artık mevcut Microsoft Office uygulamalarına (Word, Excel, PowerPoint, Outlook ve OneNote) ek olarak Microsoft ekipleri alacak. Intune, diğer Office macOS uygulamaları yüklü olan mevcut Mac cihazlarını algılar ve cihaz Intune ile bir dahaki sefer iade ettiğinde Microsoft ekipleri yüklemeye çalışır. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, MacOS için **Office 365 Suite** 'i, **MacOS** > **Add** > **uygulamalar** ' ı seçerek bulabilirsiniz. Daha fazla bilgi için bkz. [Microsoft Intune Ile macOS cihazlarına Office 365 atama](../apps/apps-add-office365-macos.md).

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>Özelleştirme bölmesi için Grup hedefleme desteği <!-- 4722837  -->
Özelleştirme bölmesindeki ayarları Kullanıcı gruplarına hedefleyebilirsiniz. Intune portalından, **istemci uygulamaları** > **Özelleştirme**' yi seçin. Daha fazla bilgi için bkz. [Intune Şirket Portalı uygulamalar, Şirket Portalı Web sitesi ve Intune uygulaması özelleştirme] (şirket-Portal-app.md].

<!-- ***********************************************-->
## <a name="device-configuration"></a>Cihaz yapılandırması

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>MacOS cihazları için kablolu ağ cihaz yapılandırma profilleri<!-- 3508686  -->
Kablolu ağları yapılandıran yeni bir macOS cihaz yapılandırma profili kullanılabilir (**cihaz yapılandırma** > **profilleri** ** > ,** > Platform için **MacOS** > profil türü için **kablolu ağ** ). Kablolu ağları yönetmek için 802.1 x profilleri oluşturmak ve bu kablolu ağları macOS cihazlarınıza dağıtmak için bu özelliği kullanın.

Uygulama alanı:
- Mac OS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Cihaz yapılandırma profili ayarları ve değerleri Windows platformları için güncelleştirilecektir<!-- 4091122 -->
Windows platformları için cihaz yapılandırma profilleri oluşturduğunuzda (**cihaz** > **yapılandırma profilleri** > platform için herhangi bir **Windows** seçeneği > **profil oluşturma** ), bazı ayarlar ve bunların değerleri CSP 'den farklıdır ve kafa karıştırıcı olabilir. Ayar adları ve değerleri daha net olacak şekilde güncelleştirilecektir.

Uygulama alanı:

- Windows 10 ve üzeri cihaz yapılandırma profilleri
- Windows holographic for Business cihaz yapılandırma profilleri
- Windows 8.1 cihaz yapılandırma profilleri
- Windows Phone 8,1 cihaz yapılandırma profilleri

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>MacOS için Microsoft Defender ATP uygulamasını yapılandırma  <!-- 5520115  -->
Yakında bir Endpoint Protection cihaz yapılandırma profilinin parçası olarak macOS çalıştıran cihazlar için Microsoft Defender ATP uygulamasının [ayarlarını](../protect/endpoint-protection-macos.md) yapılandırabilirsiniz (**cihaz** > **yapılandırma profillerinin** > **profil oluşturma**, *Platform*için **MacOS** ve ardından *profil türü*için **Endpoint Protection** ). MacOS cihaz yapılandırması için sekiz ayar olacaktır. 

Defender ATP, macOS 10,13 (High Sierra) ve üzeri sürümlerde desteklenir ve bu ayarlar uygulandıktan *sonra* [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) uygulamasının cihaza dağıtılması gerekir. Uygulama dağıtılmadan önce ayarların cihaza gönderilmesi gerekir. MacOS 'un beta sürümleri desteklenmez.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>MacOS Endpoint Protection cihaz yapılandırma ilkesi için yeni Filekasası ayarı<!-- 5459801   -->
[MacOS Endpoint Protection](../protect/endpoint-protection-macos.md) şablonu Içindeki filekasası kategorisine yeni bir ayar ekliyoruz: kurtarma anahtarını gizleyin. (**Cihazlar** > **yapılandırma profillerini** **Profil oluştur** > , *Platform* için **MacOS** ' u ve ardından *profil türü*için **Endpoint Protection** ' ı seçin. Bu ayar, Filekasa2 şifrelemesi sırasında son kullanıcıdan kişisel anahtarı gizler. Bir cihaz kullanıcısı, kişisel kurtarma anahtarını iOS şirket portalı uygulamasından veya şifrelenmiş macOS cihazının Şirket portalı Web sitesinden dilediğiniz zaman görüntüleyebilir. Kişisel kurtarma anahtarını görüntülemek için cihaz ayrıntılarına gidebilir ve *Kurtarma anahtarı al*' a tıklayabilirsiniz.

Bu ayar, önceden oluşturulan ilkede kullanılamaz. Bu ayarı kullanmak üzere yapılandırmak için dosya Kasası ilkelerini yeniden oluşturmanız gerekir. 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Uyumsuzluk için eylem olarak anında iletme bildirimleri gönder <!-- 1733150   -->
İOS ve Android platformları için Şirket Portalı uygulaması aracılığıyla uygulama anında iletme bildirimi gönderecek uyumsuzluk için yeni bir eylem ekliyoruz. Kullanıcılar, Şirket Portalı uygulamasını başlatarak, uyumsuz oldukları nedeni görüntüleyen bildirimlere tıklayabilir. Yöneticiler bu yeni eylemi, Microsoft Endpoint Manager Yönetim Merkezi 'nde **cihazlara** giderek **uyumluluk ilkelerine** > , **ilke oluştur** > ve ardından uygulama anında iletme bildirimi göndermek için *eylemi* seçerek yapılandırabilecektir.

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Yönetilen Google Play uygulamaları için yayın öncesi test<!-- 2681933  -->
[Uygulama ön sürümü testi için Google Play 'ın kapalı test izlerini](https://support.google.com/googleplay/android-developer/answer/3131213) kullanan kuruluşlar, bu parçaları Intune ile yönetebilecektir. Test yapmak için Google Play 'in ön üretim izlerini, pilot gruplarına yayımlayan Iş kolu uygulamalarını seçmeli olarak atayabileceksiniz. Intune 'da, bir uygulamanın kendisine yayımlanmış bir üretim öncesi derleme testi izlemesine sahip olup olmadığını ve bu izlemeyi AAD Kullanıcı veya cihaz gruplarına atayabilmesini de görebileceksiniz. Bu özellik, şu anda desteklenen Android kurumsal senaryolarımız (iş profili, tam olarak yönetilen ve adanmış) için kullanılabilir. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **uygulamalar** > **Android** > **Ekle**' yi seçerek yönetilen bir Google Play uygulaması ekleyebilirsiniz. Daha fazla bilgi için bkz. [Intune Ile Android Enterprise cihazlarına yönetilen Google Play uygulamaları ekleme](../apps/apps-add-android-for-work.md).

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>Android 'de Outlook için S/MIME ayarlarını yönetme<!-- 6517085   -->
Android Enterprise çalıştıran cihazlarda Outlook için S/MIME ayarını yönetmek üzere uygulama yapılandırma ilkelerini kullanabilirsiniz. Ayrıca, cihaz kullanıcılarının Outlook ayarları ' nda S/MIME 'yi etkinleştirmesine veya devre dışı bırakmasına izin verip vermeyeceğinizi seçebileceksiniz. Android için uygulama yapılandırma ilkesi 'ni kullanmak için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) 'nde **uygulamalar** > **uygulama yapılandırma Ilkeleri** ' ne gidin > **yönetilen cihaz** **ekleyin** > .

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>İOS/ıpados cihazlarında SSO ve SSO uygulama uzantısı profillerindeki ek seçenekler<!-- 6504155  -->
İOS/ıpados cihazlarında şunları yapabilirsiniz:

- SSO profillerdeki (**cihazlar** > **yapılandırma profilleri** > profil **oluşturma** > **IOS/ıpados** için Platform > **cihaz özellikleri** > **Çoklu oturum açma**) için, Kerberos asıl adını SSO profillerindeki güvenlik hesabı Yöneticisi (Sam) hesap adı olarak ayarlayın. 
- SSO uygulama uzantısı profillerinde (**cihazlar** > **yapılandırma profilleri** > profil **oluşturma** > **IOS/ıpados** , profil > **Çoklu oturum açma uygulama uzantısı**için Platform > **cihaz özellikleri** ), yeni bir SSO uygulama uzantısı türü kullanarak iOS/ıpados Microsoft Azure ad uzantısını daha az tıklamayla yapılandırın. Paylaşılan cihazlar için Azure AD uzantısını etkinleştirebilir ve uzantıya özgü verileri uzantıya gönderebilirsiniz.

Uygulama alanı:
- iOS/ıpados 13.0 +

İOS/ıpados cihazlarında çoklu oturum açma kullanma hakkında daha fazla bilgi için bkz. [Çoklu oturum açma uygulama uzantısına genel bakış](../configuration/device-features-configure.md#single-sign-on-app-extension) ve [Çoklu oturum açma ayarları listesi](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Cihaz kaydı

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Kendi cihazlarını getir, dağıtmak için VPN kullanabilir<!--5015344 -->
Yeni Autopilot profili **etki alanı bağlantısını atla onay** geçişi, kendi üçüncü taraf Win32 VPN istemcinizi kullanarak kurumsal ağınıza erişim olmadan karma Azure AD JOIN cihazlarını dağıtmanıza olanak tanır. Yeni geçişi görmek için [Microsoft Endpoint Manager yönetim merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) > **cihazlar**  > **Windows** > **Windows kayıt** > **dağıtım PROFILLERI** ' ne gidin > **kullanıma hazır deneyim (OOBE)** **oluşturun** . > 

<!-- ***********************************************-->
## <a name="device-management"></a>Cihaz yönetimi

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>KCG cihazları için PowerShell betikleri desteği<!-- 1862833  -->
PowerShell betikleri, Intune 'da Azure AD kayıtlı cihazlarını destekleyecektir. PowerShell hakkında daha fazla bilgi için bkz. [Intune 'Da Windows 10 cihazlarda PowerShell betiklerini kullanma](../apps/intune-management-extension.md). Bu işlevsellik, Windows 10 Home Edition çalıştıran cihazları desteklemez.

### <a name="script-support-for-macos-devices---4280361----"></a>MacOS cihazları için betik desteği<!-- 4280361  -->
MacOS cihazlarına komut dosyaları ekleyebilir ve bunları dağıtabileceksiniz. Bu destek, MacOS cihazlarındaki yerel MDM yeteneklerini kullanarak, macOS cihazlarını mümkün olduğunca fazla yapılandırma yeteneğinizi genişletmektedir.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics, cihaz ayrıntıları günlüğünü içerecektir<!--6014987  -->
Intune cihaz ayrıntı günlükleri, **raporlar** > **Log Analytics**'te kullanılabilir. Özel sorgular ve Azure çalışma kitapları oluşturmak için cihaz ayrıntılarını ilişkilendirebilirler.

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>Cihaz sahiplik türü değiştirildiğinde anında iletme bildirimi<!-- 5575875  -->
Hem Android hem de iOS Şirket Portalı kullanıcılarınıza, cihaz sahiplik türü kişisel olarak bir gizlilik özelliği olarak değiştirildiğinde, bu kullanıcılara göndermek üzere bir anında iletme bildirimi yapılandırabileceksiniz. Bu ayar, Microsoft uç nokta yöneticisinde **kiracı yönetimi** > **özelleştirmesi**seçilerek bulunabilir. Cihaz sahipliğinin son kullanıcılarınızı nasıl etkilediği hakkında daha fazla bilgi edinmek için bkz. [cihaz sahipliğini değiştirme](../enrollment/corporate-identifiers-add.md#change-device-ownership).

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Güvenlik

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Android tam olarak yönetilen cihazlarda türetilmiş kimlik bilgileri desteği<!--4839592-->
Android kurumsal tam olarak yönetilen cihazlarda türetilmiş kimlik bilgilerini kullanabilirsiniz. Entrust Datacard, ıntercede ve DıŞA purebred için türetilmiş bir kimlik bilgisi almak üzere destek eklenecektir. Uygulama kimlik doğrulaması, Wi-Fi, VPN veya S/MIME imzalama ve/veya şifrelemeyi destekleyen uygulamalarla şifreleme için türetilmiş bir kimlik bilgisi kullanabileceksiniz.

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>MacOS cihazları için Gizlilik Tercihleri ayarları<!-- 2934232 --> 
MacOS Catalina 10,15 sürümü sayesinde, Apple yeni güvenlik ve gizlilik iyileştirmeleri ekledi. Varsayılan olarak, uygulamalar ve süreçler Kullanıcı izni olmadan belirli verilere erişemez. Kullanıcılar onay sağlamıyorsa, uygulamalar ve süreçler çalışmayabilir. Intune, macOS 10,14 ve üstünü çalıştıran cihazlarda son kullanıcılar adına, BT yöneticilerinin veri erişimine izin vermesini veya bu izni vermemeyi sağlayan ayarlar için destek ekliyor. Bu ayarlar, uygulamaların ve işlemlerin düzgün şekilde çalışmaya devam etmesini ve son kullanıcıların deneyimlerine yönelik istem sayısını azaltmasını sağlar.

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Windows 10 Endpoint Protection profili ayarları için Kullanıcı arabirimi metni ve Etiketler güncelleştirildi<!-- 5983747 -->
Kullanım ve sonuç olarak tasarlanan ayarları daha kolay anlamak için Windows 10 cihaz yapılandırma profilleri olarak yapılandırdığınız çeşitli ayarların metnini güncelleştiriyoruz.

Güncelleştiriyoruz ayarlar şunlar için Windows 10 cihaz yapılandırma profillerini içerir:

- Microsoft Defender virüsten koruma > [cihaz kısıtlamaları](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender virüsten koruma

Intune ile desteklenen ayarlar değişmemektedir. Bu yalnızca Microsoft uç nokta yönetimi Yönetim Merkezi 'ndeki Kullanıcı arabirimi metnine yönelik bir güncelleştirmedir.

<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.



