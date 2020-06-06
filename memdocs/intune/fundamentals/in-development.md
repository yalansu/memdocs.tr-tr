---
title: Geliştirme-Microsoft Intune
titleSuffix: ''
description: Geliştirmede Microsoft Intune Özellikler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5fb4bfba0dbcdfe28b2fbce8123b0e2e919fd308
ms.sourcegitcommit: e618ea7cb864635c838b672bc71a1e926bf7c047
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84458109"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>İOS/ıpados ve macOS şirket portallarının cihazlar sayfasında geliştirmeler<!-- 6055001  -->
İOS/ıpados ve Mac için Şirket Portalı uygulamasının **cihazlar** sayfasının kullanıcı deneyiminde çeşitli geliştirmeler yaptık. **Cihazlar** sayfasını daha modern bir cihaz ve daha iyi bir cihaz bilgileri organizasyonu olacak şekilde yeniden yaptık. Tanımlı bölüm üstbilgileri olan tek bir sütun kullanarak, kuruluşunuzun iOS/ıpados ve macOS kullanıcıları, güvenli kalmasını sağlamak ve kuruluşunuzun kaynaklarına erişimi sürdürmek için cihazlarının durumunu kolayca denetleyebilir. Ayrıca, cihazları uyumsuz olan kullanıcılar için daha net mesajlaşma ve ek sorun giderme adımları ekledik. Şirket Portalı hakkında daha fazla bilgi için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>MacOS kayıt deneyimi için Şirket Portalı geliştirmeleri<!-- 6444452  -->
MacOS kayıt deneyimi için Şirket Portalı, iOS kayıt deneyimi için Şirket Portalı daha yakından hizalanan daha basit bir kayıt işlemine sahip olacaktır. Cihaz kullanıcıları şunları görür:  
- Bir uyleyici Kullanıcı arabirimi.  
- İyileştirilmiş bir kayıt denetim listesi.  
- Cihazlarını nasıl kaydedebileceğinize ilişkin daha net yönergeler.  
- Gelişmiş sorun giderme seçenekleri.  

Şirket Portalı hakkında daha fazla bilgi için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>İOS Şirket Portalı oturum açma/kapatma uygulaması olacak şekilde yapılandırmak için otonom tek uygulama modu ayarlarını kullanın<!-- 7055619  -->
İOS Şirket Portalı, otonom tek uygulama modu (ASAM) kullanacak şekilde yapılandırabileceksiniz. İOS Şirket Portalı, oturum kapatma ve oturum açma sırasında tek uygulama moduna geçmek üzere yapılandırmak için Microsoft Uç Nokta Yöneticisi konsolundaki ASAM ayarlarını kullanabilirsiniz. Şirket Portalı ASAM 'da olduğunda, kullanıcılar, Şirket Portalı oturum açana kadar cihazdaki herhangi bir uygulamayı veya giriş düğmesini kullanamaz. Oturumu kapatma sırasında Şirket Portalı, tek uygulama moduna geri döner. 

Microsoft Endpoint Manager 'da Şirket portalı Asam içinde olacak şekilde yapılandırmak için, **cihazlar**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin. Platform olarak **iOS/ıpados** ' ı seçin ve profil olarak **cihaz kısıtlamalarını** seçin. **Yapılandırma ayarları** sekmesinde, **otonom tek uygulama modu**' nu seçin. **Uygulama adını** olarak ayarlayın `Company Portal` ve **uygulama paketi kimliğini** olarak ayarlayın `com.app.CompanyPortal` . Daha fazla bilgi için bkz. [otonom tek uygulama modu (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) ve [tek uygulama modu](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Cihaz yapılandırması

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Üçüncü taraf MDM iş ortaklarından cihaz uyumluluk durumunu ayarlama<!-- 6361689   -->
Üçüncü taraf MDM çözümlerine sahip olan Microsoft 365 müşteriler, Microsoft Intune cihaz uyumluluk hizmeti ile tümleştirme yoluyla iOS ve Android üzerinde Microsoft 365 uygulamalar için koşullu erişim ilkelerini zorlayabilir. Üçüncü taraf MDM satıcısı, Intune cihaz uyumluluk hizmetinden yararlanarak cihaz uyumluluk verilerini Intune 'a gönderir. Daha sonra Intune, cihazın güvenilir olup olmadığını ve Azure AD 'de koşullu erişim özniteliklerini ayarlamanızı sağlayacak şekilde değerlendirilir.  Müşterilerin, Microsoft Endpoint Manager yönetim merkezi veya Azure AD portalı içinden Azure AD koşullu erişim ilkeleri ayarlaması gerekecektir.  

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Uyumsuzluk için e-postalara Şirket Portalı Destek Web sitenizin bağlantısını ekleyin<!-- 7225498    -->
E-posta bildirim şablonuna, uyumlu olmayan cihazların kullanıcılarına gönderilen e-posta bildirimlerine Şirket portalı Web sitenizin bağlantısını ekleyecek yeni bir ayar ekliyoruz. (**Uç nokta güvenliği**  >  **Cihaz uyumluluğu**  >  **Bildirimler**  >  **Bildirim oluştur**).  Uyumsuz bir cihaza sahip olması nedeniyle bir e-posta alan kullanıcılar, cihazlarının neden uyumlu olmadığı hakkında daha fazla bilgi edinmek için bir Web sitesi açmak üzere bağlantıyı kullanabilir.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>MacOS Endpoint Protection cihaz yapılandırma ilkesi için yeni Filekasası ayarı<!-- 5459801   -->
[MacOS Endpoint Protection](../protect/endpoint-protection-macos.md) şablonu Içindeki filekasası kategorisine yeni bir ayar ekliyoruz: kurtarma anahtarını gizleyin. (**Cihazlar**  >  **Yapılandırma profilleri**  >  **Profil oluştur**, *Platform* için **MacOS** ' u ve ardından *profil türü*için **uç nokta koruması** ' nı seçin. Bu ayar, Filekasa2 şifrelemesi sırasında son kullanıcıdan kişisel anahtarı gizler. Bir cihaz kullanıcısı, kişisel kurtarma anahtarını iOS şirket portalı uygulamasından veya şifrelenmiş macOS cihazının Şirket portalı Web sitesinden dilediğiniz zaman görüntüleyebilir. Kişisel kurtarma anahtarını görüntülemek için cihaz ayrıntılarına gidebilir ve *Kurtarma anahtarı al*' a tıklayabilirsiniz.

Bu ayar, önceden oluşturulan ilkede kullanılamaz. Bu ayarı kullanmak üzere yapılandırmak için dosya Kasası ilkelerini yeniden oluşturmanız gerekir. 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>MacOS cihazlarında içerik önbelleğe almayı yapılandırma<!-- 7106872 -->
MacOS cihazlarında, içerik önbelleğe almayı yapılandıran bir yapılandırma profili**oluşturabilirsiniz (cihaz**  >  **yapılandırma profilleri**profil  >  için MacOS**profili oluşturma**  >  **MacOS** > for profile için **cihaz özellikleri** ). Önbelleği silmek, paylaşılan önbelleğe izin vermek, diskte önbellek sınırı ayarlamak ve daha fazlasını yapmak için bu ayarları kullanın.

İçerik önbelleğe alma hakkında daha fazla bilgi için bkz. [contentcaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (Apple 'ın Web sitesini açar).

Şu anda yapılandırabileceğiniz ayarları görmek için [Intune 'Da MacOS cihaz özelliği ayarları](../configuration/macos-device-features-settings.md)' na gidin.

Aşağıdakiler cihazlar için geçerlidir:
- Mac OS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Windows 10 ve daha yeni cihazlar için yeni VPN ayarları<!-- 6602122  -->
Ikev2 bağlantı türünü kullanarak bir VPN profili oluşturduğunuzda yapılandırabileceğiniz yeni ayarlar vardır (**cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **Windows 10 ve sonrası** için platform > **VPN** > **temel VPN**):

- **Cihaz tüneli**: cihazların Kullanıcı oturumu açma da dahil olmak üzere herhangi bir Kullanıcı ETKILEŞIMI gerekmeden VPN 'ye otomatik olarak bağlanmasına izin verir. Bu özellik **her zaman açık**' i etkinleştirmenizi ve **makine sertifikalarını** kimlik doğrulama yöntemi olarak kullanmanızı gerektirir.
- Şifreleme paketi ayarları: istemci ve sunucu ayarlarını eşleştirmeye izin veren ıKE ve alt güvenlik ilişkilerinin güvenliğini sağlamak için kullanılan algoritmaları yapılandırın.

Yapılandırabileceğiniz ayarları görmek için, [Intune kullanarak VPN bağlantıları eklemek üzere Windows cihaz ayarları](../configuration/vpn-settings-windows-10.md)' na gidin.

Aşağıdakiler cihazlar için geçerlidir:
- Windows 10 ve üzeri

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>Paylaşılan iPad cihazlarda paylaşılan iPad geçici oturumlarını engelle<!-- 6613794 -->
Intune 'da, paylaşılan iPad cihazlarında geçici oturumları engelleyen, paylaşılan yeni bir **iPad geçici oturumları** ayarı**vardır (cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **iOS/ıpados** > profil türü > **paylaşılan iPad**için **cihaz kısıtlamaları** ). Etkinleştirildiğinde, son kullanıcılar Konuk hesabını kullanamaz. Yönetilen Apple KIMLIĞI ve parolasıyla cihazda oturum açması gerekir. 

Yapılandırabileceğiniz ayarlar hakkında daha fazla bilgi için bkz. [iOS ve ıpados cihaz ayarları, özelliklere izin vermek veya kısıtlamak için](../configuration/device-restrictions-ios.md).

Aşağıdakiler cihazlar için geçerlidir:
- İOS/ıpados 13,4 ve daha yeni çalıştıran paylaşılan iPad cihazları

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>Tam olarak yönetilen Android Kurumsal cihazları için varsayılan başlatıcı olarak Microsoft başlatıcısı 'nı kullanın<!-- 4927976  -->
Android kurumsal cihaz sahibi cihazlarda, Microsoft başlatıcısı 'nı tam olarak yönetilen cihazlar için varsayılan başlatıcı olarak**ayarlayabilirsiniz (cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  **Android Enterprise** profil > **Device owner**  >  **cihaz deneyimi**için cihaz sahibi**cihaz kısıtlamalarına** >). Diğer tüm Microsoft Başlatıcı ayarlarını yapılandırmak için uygulama yapılandırma ilkelerini kullanın. 

Ayrıca, **cihaz deneyimine**yeniden adlandırılmakta olan **adanmış cihazlar** dahil bazı farklı Kullanıcı Arabirimi güncelleştirmeleri de vardır.

Kısıtlayabilecek tüm ayarları görmek için bkz. [Intune kullanarak özelliklere izin vermek veya erişimi kısıtlamak Için Android kurumsal cihaz ayarları](../configuration/device-restrictions-android-for-work.md). 

Aşağıdakiler cihazlar için geçerlidir:
- Android kurumsal cihaz sahibi tam olarak yönetilen cihazlar (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>Android Enterprise üzerinde OEMConfig kullanarak yeni şema ayarları ekleme ve mevcut şema ayarlarını arama<!-- 6394386  -->
Intune 'da, Android kurumsal cihazlarındaki ayarları yönetmek için oemconfig kullanabilirsiniz (**cihaz**  >  **yapılandırma profilleri**Intune için bir  >  **profil**  >  **Android Enterprise** for platform > **için bkz** .). **Yapılandırma tasarımcısını**kullandığınızda, uygulama şemasındaki özellikler gösterilir. Şimdi, **yapılandırma tasarımcısında**şunları yapabilirsiniz:
- Uygulama şemasına yeni ayarlar ekleyin.
- Uygulama şemasında yeni ve var olan ayarları arayın.

Intune 'daki OEMConfig profilleri hakkında daha fazla bilgi için, bkz. [Microsoft Intune 'de oemconfig Ile Android Kurumsal cihazları kullanma ve yönetme](../configuration/android-oem-configuration-overview.md).

Aşağıdakiler cihazlar için geçerlidir:
- Android Kurumsal

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Cihaz kaydı

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Otomatik cihaz kaydı Eşitleme hataları<!-- 6988214 -->
İOS/ıpados ve macOS cihazları dahil olmak üzere yeni hatalar raporlanır
- Telefon numarasında geçersiz karakterler veya bu alan boş. 
- Profil için geçersiz veya boş yapılandırma adı. 
- Geçersiz/zaman aşımına uğradı imleç değeri veya imleç bulunamadı.
- Reddedilen veya süre dolma belirteci. 
- Departman alanı boş veya uzunluk çok uzun. 
- Profil Apple tarafından bulunmadı ve yeni bir tane oluşturulması gerekiyor. 
- Cihazların durumunu gördüğünüz genel bakış sayfasına, kaldırılan bir Apple Business Manager cihazı sayısı eklenecektir.

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Kendi cihazlarını getir, dağıtmak için VPN kullanabilir<!--5015344 -->
Yeni Autopilot profili **etki alanı bağlantısını atla onay** geçişi, üçüncü taraf Win32 VPN istemcinizi kullanarak kurumsal ağınıza erişim olmadan karma Azure AD JOIN cihazlarını dağıtmanıza olanak tanır. Yeni geçişi görmek için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**   >  **Windows**  >  **Windows kayıt**  >  **dağıtım profilleri**  >  **profil oluşturma**öncesi  >  **deneyim (OOBE)** bölümüne gidin.

### <a name="shared-ipads-for-business--6367326---"></a>Iş için paylaşılan IPad 'ler<!--6367326 -->
Birden çok çalışanın cihazları paylaşabilmesi için Intune ve Apple Business Manager 'ı kullanarak paylaşılan iPad 'i kolayca ve güvenli bir şekilde ayarlayabilirsiniz. Apple 'ın [paylaşılan iPad](https://developer.apple.com/education/shared-ipad/) 'i, Kullanıcı verilerini korurken birden çok kullanıcı için kişiselleştirilmiş bir deneyim sağlar. Yönetilen bir Apple KIMLIĞI kullanarak, kullanıcılar kuruluşlarındaki paylaşılan iPad 'de oturum açtıktan sonra uygulamalarına, verilerine ve ayarlarına erişebilirler. Paylaşılan iPad, Federasyon kimlikleriyle birlikte çalışmaktadır.

Bu özelliği görmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **iOS**  >  **iOS kayıt**  >  **kayıt programı belirteçleri** ' ne gidin > belirteç seçin > **profiller**  >  **Profil oluştur**  >  **iOS**. **Yönetim ayarları** sayfasında, **Kullanıcı benzeşimi olmadan kaydet** ' i seçin ve **paylaşılan iPad** seçeneğini görürsünüz.

**Uygulama hedefi:** ıpados 13,4 ve üzeri. Bu sürüm, kullanıcıların yönetilen bir Apple KIMLIĞI olmadan bir cihaza erişebilmeleri için paylaşılan iPad ile geçici oturumlar için destek ekledi. Oturum kapatma sonrasında cihaz tüm Kullanıcı verilerini siler, böylece cihaz kullanıma hemen kullanılabilir hale gelir ve cihaz temizleme gereksinimini ortadan kaldırır. 

<!-- ***********************************************-->
## <a name="device-management"></a>Cihaz yönetimi

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>Ortak yönetilen cihazlarda birincil kullanıcıyı değiştirme<!--7319183 -->
Ortak yönetilen Windows cihazları için bir cihazın birincil kullanıcısını değiştirebileceksiniz. Bunu bulma ve değiştirme hakkında daha fazla bilgi için bkz. [Intune cihazının birincil kullanıcısını bulma](../remote-actions/find-primary-user.md).

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>KCG cihazları için PowerShell betikleri desteği<!-- 1862833  -->
PowerShell betikleri, Intune 'da Azure AD kayıtlı cihazlarını destekleyecektir. PowerShell hakkında daha fazla bilgi için bkz. [Intune 'Da Windows 10 cihazlarda PowerShell betiklerini kullanma](../apps/intune-management-extension.md). Bu işlevsellik, Windows 10 Home Edition çalıştıran cihazları desteklemez.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics, cihaz ayrıntıları günlüğünü içerecektir<!--6014987  -->
Intune cihaz ayrıntı günlükleri, **raporlar**  >  **Log Analytics**' te kullanılabilir. Özel sorgular ve Azure çalışma kitapları oluşturmak için cihaz ayrıntılarını ilişkilendirebilirler.

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Intune birincil kullanıcı ayarı da Azure AD Owner özelliğini ayarlar<!--7319227 -->
Bu gelecek özellik, Intune birincil kullanıcısının ayarlandığı anda, yeni kayıtlı karma Azure AD 'ye katılmış cihazlarda Owner özelliğini otomatik olarak ayarlar. Birincil Kullanıcı hakkında daha fazla bilgi için bkz. [Intune cihazının birincil kullanıcısını bulma](../remote-actions/find-primary-user.md).

Bu, kayıt işlemine yapılan bir değişiklik ve yalnızca yeni kaydedilen cihazlar için geçerlidir. Mevcut karma Azure AD 'ye katılmış cihazlar için Azure AD Owner özelliğini el ile güncelleştirmeniz gerekir. Bunu yapmak için [birincil Kullanıcı Değiştir özelliğini](../remote-actions/find-primary-user.md#change-a-devices-primary-user) veya [bir komut dosyasını](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)kullanabilirsiniz.

Windows 10 cihazları karma Azure Azure dizini 'ne katıldığında, cihazın ilk kullanıcısı Endpoint Manager 'da birincil Kullanıcı olur.  Şu anda Kullanıcı ilgili Azure AD cihaz nesnesinde ayarlanmadı. Bu, *sahip* özelliğini Microsoft Endpoint Manager Yönetim Merkezi 'ndeki *birincil Kullanıcı* ÖZELLIĞI ile bir Azure AD portalından karşılaştırırken tutarsızlığa neden olur. Azure AD Owner özelliği, BitLocker Kurtarma anahtarlarına erişimin güvenliğini sağlamak için kullanılır. Özelliği, karma Azure AD 'ye katılmış cihazlarda doldurulmamış. Bu sınırlama, Azure AD 'den BitLocker kurtarma 'nın self servis kurulumunu engeller. Yakında sunulacak olan bu özellik bu kısıtlamayı çözer.

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

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>MacOS cihazları için uzaktan kilitleme PIN kullanılabilirliği<!--7281557-->
MacOS cihaz uzaktan kilitleme PIN 'lerinin kullanılabilirliği 7 günden 30 güne yükseltilir.

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
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.
