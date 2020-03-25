---
title: Geliştirme-Microsoft Intune
titleSuffix: ''
description: Geliştirmede Microsoft Intune Özellikler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220141"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>Microsoft Intune için geliştirme sırasında-Mart 2020

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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>İOS için Şirket Portalı yatay modunu destekleyecek şekilde<!--6048329  -->
Kullanıcılar cihazlarını kaydedebilir, uygulama bulabilir ve tercih ettikleri ekran yönünü kullanarak BT desteği alabilir. Kullanıcılar ekranı dikey modda kilitlemedikleri takdirde uygulama ekranları dikey veya yatay moda uyacak şekilde otomatik olarak algılar ve ayarlar.

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Android için Şirket Portalı 'de geliştirilmiş oturum açma deneyimi<!-- 6103997  -->
Daha modern, basit ve kullanıcılar için temiz bir deneyim sunmak amacıyla Android için Şirket Portalı uygulamasındaki çeşitli oturum açma ekranlarının yerleşimini güncelleştiriyoruz.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Cihaz yapılandırması

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>MacOS cihazları için kablolu ağ cihaz yapılandırma profilleri<!-- 3508686  -->
Kablolu ağları yapılandıran yeni bir macOS cihaz yapılandırma profili kullanılabilir (**cihaz yapılandırma** > **profilleri** ** > ,** > Platform için **MacOS** > profil türü için **kablolu ağ** ). Kablolu ağları yönetmek için 802.1 x profilleri oluşturmak ve bu kablolu ağları macOS cihazlarınıza dağıtmak için bu özelliği kullanın.

Uygulama alanı:
- Mac OS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>İOS/ıpados ve macOS cihazlarında yapılandırma profilleri oluştururken Geliştirilmiş kullanıcı arabirimi deneyimi<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
İOS/ıpados veya macOS cihazları için bir profil oluşturduğunuzda, uç nokta yönetimi Yönetim Merkezi 'ndeki deneyim güncelleştirilir. Bu değişiklik, aşağıdaki cihaz yapılandırma profillerini**etkiler (cihaz** > **yapılandırma profilleri** > platform Için **iOS** veya **MacOS** > **profili oluşturma** ):

- Özel: iOS/ıpados, macOS
- Cihaz özellikleri: iOS/ıpados, macOS
- Cihaz kısıtlamaları: iOS/ıpados, macOS
- Endpoint Protection: macOS
- Uzantılar: macOS
- Tercih dosyası: macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Android kurumsal cihazlarda OEMConfig yapılandırma profilleri oluştururken Geliştirilmiş kullanıcı arabirimi deneyimi<!-- 5568645   -->
Android Kurumsal cihazları için bir OEMConfig profili oluştururken veya düzenlerken, Endpoint Management Yönetim Merkezi 'ndeki deneyim güncellenir. Güncelleştirilmiş deneyim, bir bakışta yapılandırdığınız ayarların özetini sağlayacaktır. Bu değişiklik, OEMConfig cihaz yapılandırma profilini (**cihazlar** > **yapılandırma profillerini** etkiler > platform için **Android Enterprise** >, profil türü için **oemconfig** ) > **oluşturur** .

Bu özellik şu platformlarda geçerlidir:
- Android Kurumsal 

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Cihaz yapılandırma profili ayarları ve değerleri Windows platformları için güncelleştirilecektir<!-- 4091122 -->
Windows platformları için cihaz yapılandırma profilleri oluşturduğunuzda (**cihaz** > **yapılandırma profilleri** > platform için herhangi bir **Windows** seçeneği > **profil oluşturma** ), bazı ayarlar ve bunların değerleri CSP 'den farklıdır ve kafa karıştırıcı olabilir. Ayar adları ve değerleri daha açık olacak şekilde güncelleştirilecektir.

Uygulama alanı:

- Windows 10 ve üzeri cihaz yapılandırma profilleri
- Windows holographic for Business cihaz yapılandırma profilleri
- Windows 8.1 cihaz yapılandırma profilleri
- Windows Phone 8,1 cihaz yapılandırma profilleri

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Android ve Android kurumsal cihazlarda cihaz kısıtlama profilleri oluştururken Geliştirilmiş kullanıcı arabirimi deneyimi<!-- 5841361 -->
Android veya Android Kurumsal cihazları için bir profil oluşturduğunuzda, uç nokta yönetimi Yönetim Merkezi 'ndeki deneyim güncelleştirilir. Bu değişiklik aşağıdaki cihaz yapılandırma profillerini etkiler (**cihazlar** > **yapılandırma profilleri** > **profil oluşturma** > **Android Cihaz Yöneticisi** veya platform için **Android Enterprise** ):

- Cihaz kısıtlamaları: Android Cihaz Yöneticisi
- Cihaz kısıtlamaları: Android kurumsal cihaz sahibi
- Cihaz kısıtlamaları: Android kurumsal iş profili

Yapılandırabileceğiniz cihaz kısıtlamaları hakkında daha fazla bilgi için bkz. [Android Cihaz Yöneticisi](../configuration/device-restrictions-android.md) ve [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>MacOS için Microsoft Defender ATP uygulamasını yapılandırma  <!-- 5520115  -->
Yakında bir Endpoint Protection cihaz yapılandırma profilinin parçası olarak macOS çalıştıran cihazlar için Microsoft Defender ATP uygulamasının [ayarlarını](../protect/endpoint-protection-macos.md) yapılandırabilirsiniz (**cihaz** > **yapılandırma profillerinin** > **profil oluşturma**, *Platform*için **MacOS** ve ardından *profil türü*için **Endpoint Protection** ). MacOS cihaz yapılandırması için sekiz ayar olacaktır. 

Defender ATP, macOS 10,13 (High Sierra) ve üzeri sürümlerde desteklenir ve bu ayarlar uygulandıktan *sonra* [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) uygulamasının cihaza dağıtılması gerekir. Uygulama dağıtılmadan önce ayarların cihaza gönderilmesi gerekir. MacOS 'un beta sürümleri desteklenmez.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>MacOS Endpoint Protection cihaz yapılandırma ilkesi için yeni Filekasası ayarı<!-- 5459801   -->
[MacOS Endpoint Protection](../protect/endpoint-protection-macos.md) şablonu Içindeki filekasası kategorisine yeni bir ayar ekliyoruz: kurtarma anahtarını gizleyin. (**Cihazlar** > **yapılandırma profillerini** **Profil oluştur** > , *Platform* için **MacOS** ' u ve ardından *profil türü*için **Endpoint Protection** ' ı seçin. Bu ayar, Filekasa2 şifrelemesi sırasında son kullanıcıdan kişisel anahtarı gizler. Bir cihaz kullanıcısı, kişisel kurtarma anahtarını iOS şirket portalı uygulamasından veya şifrelenmiş macOS cihazının Şirket portalı Web sitesinden dilediğiniz zaman görüntüleyebilir. Kişisel kurtarma anahtarını görüntülemek için cihaz ayrıntılarına gidebilir ve *Kurtarma anahtarı al*' a tıklayabilirsiniz.

Bu ayar, önceden oluşturulan ilkede kullanılamaz. Bu ayarı kullanmak üzere yapılandırmak için dosya Kasası ilkelerini yeniden oluşturmanız gerekir. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Win32 uygulama içeriğini indirirken teslim Iyileştirme aracısını yapılandırma<!-- 5410945  -->
Teslim Iyileştirme aracısını, atamaya göre arka planda veya ön plan modunda Win32 uygulama içeriğini indirmek için yapılandırabileceksiniz. Mevcut Win32 uygulamaları için içerik arka plan modunda indirilmeye devam edecektir. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **uygulamalar** > **tüm uygulamalar** ' ı seçin > *Win32 uygulama* > **özelliklerini**seçin. **Atamalar**' ın yanındaki **Düzenle** ' yi seçin.  **Gerekli** bölümde **mod** altında **Ekle** seçeneğini belirleyerek atamayı düzenleyin.  Yeni ayarı, kullanılabilir hale geldiğinde **uygulama ayarları** bölümünde bulacaksınız. Teslim Iyileştirme hakkında daha fazla bilgi için bkz. [Win32 uygulama yönetimi-teslim iyileştirmesi](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Cihaz yönetimi

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Windows cihazları için birincil kullanıcıyı değiştirme <!-- 3794742 -->
Windows karma ve Azure AD 'ye katılmış cihazlar için birincil kullanıcıyı değiştirebileceksiniz. Bunu yapmak için **ıntune** > **cihazlar** > **tüm cihazlar** ' a gidin > bir cihaz > **özellikleri** > **birincil Kullanıcı**seçin.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>KCG cihazları için PowerShell betikleri desteği<!-- 1862833  -->
PowerShell betikleri, Intune 'da Azure AD kayıtlı cihazlarını destekleyecektir. PowerShell hakkında daha fazla bilgi için bkz. [Intune 'Da Windows 10 cihazlarda PowerShell betiklerini kullanma](../apps/intune-management-extension.md). Bu işlevsellik, Windows 10 Home Edition çalıştıran cihazları desteklemez.

### <a name="new-information-in-device-details---5604099---"></a>Cihaz ayrıntılarında yeni bilgiler<!-- 5604099 -->
Aşağıdaki bilgiler cihazların **genel bakış** sayfasında olacaktır:

- Depolama kapasitesi (cihazdaki fiziksel depolama miktarı)
- Bellek kapasitesi (cihazdaki fiziksel bellek miktarı)

### <a name="script-support-for-macos-devices---4280361----"></a>MacOS cihazları için betik desteği<!-- 4280361  -->
MacOS cihazlarına komut dosyaları ekleyebilir ve bunları dağıtabileceksiniz. Bu destek, MacOS cihazlarındaki yerel MDM yeteneklerini kullanarak, macOS cihazlarını mümkün olduğunca fazla yapılandırma yeteneğinizi genişletmektedir.

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
