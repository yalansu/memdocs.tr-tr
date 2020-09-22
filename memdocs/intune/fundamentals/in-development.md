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
ms.openlocfilehash: cb9c5c43e3e5c1f9542e06ab1fa4b3b1868924e8
ms.sourcegitcommit: 37dc6b78de8bb904b83a9d571f3c9f414b54f321
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90848394"
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

### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>İOS ve macOS cihazlarında 4096 anahtar boyutuna sahip sertifikalar için destek<!-- 7659175   -->
Intune, SCEP sertifika profilleri için 4096 bitlik bir anahtar boyutu kullanımını yakında desteklemektedir. (**Cihazlar**  >  **Yapılandırma profilleri**  >  **Profil oluştur**  >  *platform seçin*  >  *Profil*  =  **SCEP sertifikası**)

4096 bitlik anahtarlar için destek aşağıdaki platformlar için olacaktır: 
- iOS 14 ve üzeri
- macOS 11 ve üzeri    

### <a name="new-setting-for-password-complexity-for-android-10-and-later---7992114----"></a>Android 10 ve üzeri için parola karmaşıklığı için yeni ayar<!-- 7992114  -->
Android 10 ve üzeri için yeni seçenekleri desteklemek üzere hem *cihaz uyumluluk* ilkesi hem de *cihaz kısıtlama* ilkesi için **parola karmaşıklığı** adlı yeni bir ayar ekledik. (**Cihazlar**  >  **Yapılandırma profilleri**  >  **Profil oluştur**  >  **Cihaz kısıtlamaları** ve **cihaz**  >  **uyumluluk ilkeleri**  >  **ilke oluştur**) Bu ayarla, parola türü, uzunluğu ve kalitesi gibi bir parola gücü ölçüsünü yönetebileceksiniz. 

Aşağıdaki karmaşıklık düzeyleri desteklenecektir:
- **Hiçbiri** -parola yok
- **Düşük** -parola aşağıdakilerden birini karşılar:
  - Desen
  - Yinelenen (4444) veya sıralı (1234, 4321, 2468) dizileriyle SABITLE
- **Orta** -parola aşağıdakilerden birini karşılar:
  - Yinelenen (4444) veya sıralı (1234, 4321, 2468) dizileri olmadan SABITLE, en az 4 uzunluğunda
  - Alfabetik, uzunluk en az 4
  - Alfasayısal, uzunluk en az 4
- **Yüksek** -parola aşağıdakilerden birini karşılar:
  - Yinelenen (4444) veya sıralı (1234, 4321, 2468) diziler olmadan PIN, en az 8 Uzunluk
  - Alfabetik, uzunluk en az 6
  - Alfasayısal, uzunluk en az 6

Parola karmaşıklığı, Android 10 ve üzeri çalıştıran Samsung KNOX cihazları için geçerlidir. Bu cihazlarda parola uzunluğu ve/veya parola türü ayarları, parola karmaşıklığını geçersiz kılar.

### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355---"></a>COPE Preview güncelleştirmesi: iş profili içeren Android kurumsal şirkete ait cihazlar için iş profili parolası gereksinimleri oluşturmaya yönelik yeni ayarlar<!--7088355 -->
Gelecekteki ayarlar yöneticilere iş profili olan Android kurumsal şirkete ait cihazlar için iş profili parolası ayarlama olanağı sağlar.  (**Cihazlar**  >  **Yapılandırma profilleri**  >  **Profil oluştur**  >  Platform için **Android Enterprise** > profil > iş profili parolası için **tam olarak yönetilen, adanmış ve şirkete ait iş profili**  >  **cihaz kısıtlamaları** : **Work profile password**

- Gerekli parola türü
- Minimum parola uzunluğu
- Parolanın süresi dolana kadar geçen gün sayısı
- Kullanıcının bir parolayı yeniden kullanabilmesi için gereken parola sayısı
- Cihaz silinmeden önceki oturum açma hatası sayısı


### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886----"></a>İOS/ıpados ve macOS cihazlarında uygulama başına VPN veya isteğe bağlı VPN kullanan yeni ayarlar<!-- 7758772 7758837 7758886  -->
- **Kullanıcıların OTOMATIK VPN 'yi devre dışı bırakmasını engelle**: otomatik olarak **uygulama başına VPN** veya **isteğe bağlı VPN** bağlantısı oluştururken, kullanıcıları otomatik VPN 'yi etkin ve çalışır durumda tutmaya zorlayabilirsiniz.
- **İlişkili etki alanları**: otomatik olarak **uygulama başına VPN** bağlantısı oluştururken, VPN PROFILINDEKI ilişkili etki alanlarını VPN bağlantısını otomatik olarak başlatacak şekilde belirtebilirsiniz. 
- **Dışlanan etki alanları**: otomatik **uygulama başına VPN** bağlantısı oluştururken, uygulama başına VPN bağlıyken VPN bağlantısını atlayabileceğiniz etki alanlarının bir listesini oluşturabilirsiniz.

**Cihazların**otomatik VPN  >  **Configuration profiles**  >  **Create profile**  >  > profili için iOS > **VPN** için**iOS** veya **MacOS** **Automatic VPN**profili oluşturma, cihazlar yapılandırma profillerinde otomatik VPN profilleri yapılandırabilirsiniz.

İlişkili etki alanları hakkında daha fazla bilgi için bkz. [ilişkili etki alanları](../configuration/device-features-configure.md#associated-domains).

Yapılandırabileceğiniz ayarları görmek için bkz. [iOS/ıpados cihazları için uygulama başına sanal özel ağ (VPN) ayarlama](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile).

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 14 ve üzeri
- macOS Big Sur (macOS 11)

### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356----"></a>COPE önizleme güncelleştirmesi: Android kurumsal şirkete ait cihazlar için kişisel profili bir iş profiliyle yapılandırmaya yönelik yeni ayarlar<!-- 7086356  -->
İş profili olan Android kurumsal şirkete ait cihazlar için, yalnızca kişisel profile uygulanan yeni ayarlar vardır (**cihaz**  >  **yapılandırma profilleri**  >  platform için bir**profil**  >  **Android Enterprise** >, **tam olarak yönetilen, adanmış ve şirkete ait iş profili**  >  **cihaz kısıtlamalarını** , profil > **kişisel profil**):

- **Kamera**: kişisel kullanım sırasında kameraya erişimi engellemek için bu ayarı kullanın.
- **Ekran yakalama**: kişisel kullanım sırasında ekran yakalamalarını engellemek için bu ayarı kullanın.
- **Kullanıcıların kişisel profilde bilinmeyen kaynaklardan uygulama yüklemesini etkinleştirmesine Izin ver**: Bu ayarı, kullanıcıların kişisel profilde bilinmeyen kaynaklardan uygulama yüklemelerine izin vermek için kullanın. 

Yapılandırabileceğiniz geçerli ayarları görmek için [Android kurumsal cihaz ayarları ' na giderek özelliklere izin verin veya kısıtlayın](../configuration/device-restrictions-android-for-work.md).

### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422----"></a>İOS/ıpados üzerinde uygulama kliplerini engelleyin ve macOS cihazlarındaki işletim sistemi olmayan yazılım güncelleştirmelerini erteleyin<!-- 7518422  -->
İOS/ıpados ve macOS cihazlarında bir cihaz kısıtlamaları profili oluşturduğunuzda, bazı yeni ayarlar vardır:

**iOS/ıpados 14.0 + uygulama kliplerini engelle**
- İOS/ıpados 14,0 ve üzeri için geçerlidir.
- Cihazların cihaz kaydı veya otomatik cihaz kaydı (denetimli cihazlar) ile kaydedilmiş olması gerekir.
- **Uygulama kliplerini engelle** ayarı, yönetilen cihazlarda uygulama kliplerini**engeller (cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **iOS/ıpados** for platform > **cihaz kısıtlamaları** > **genel**). Engellendiğinde, kullanıcılar herhangi bir uygulama klibi ekleyemez ve var olan tüm uygulama klipleri cihazdan kaldırılır.  

**macOS 11 + yazılım güncelleştirmelerini ertele**
- MacOS 11 ve üzeri için geçerlidir. Denetimli macOS cihazlarında, cihazda Kullanıcı tarafından onaylanan cihaz kaydı veya otomatik cihaz kaydı üzerinden kaydedilmiş olması gerekir.
- **Yazılım güncelleştirmelerini ertele** ayarı, işletim sistemi olmayan yazılım güncelleştirmelerinin Kullanıcı görünürlüğünü geciktirir (**cihaz**  >  **yapılandırma profilleri**, profil için  >  **Create profile**  >  **MacOS** >, **genel**> profili için **cihaz kısıtlamaları** oluşturur). Bu güncelleştirmeleri ertelerseniz, yeni yayınlanan güncelleştirmeler, **yazılım güncelleştirmeleri ayarlarının gecikme görünürlüğü** kullanılarak yapılandırılan erteleme süresinden sonra kullanıcılara görünmez. İşletim sistemi olmayan yazılım güncelleştirmelerinin erteleniyor, zamanlanmış güncelleştirmeleri etkilemez.
- Var olan **yazılım güncelleştirmelerini ertele** ayarı bu yeni ayarla birleştirilir. Yeni ayarı kullanarak, işletim sistemi yazılım güncelleştirmelerini ve işletim sistemi olmayan yazılım güncelleştirmelerini erteleyebilirsiniz. Yazılım güncelleştirmelerini erteleme her iki ayar için de uygulanacak gün sayısını ayarlamak için **yazılım güncelleştirmeleri gecikme süresi** ayarını kullanmaya devam edersiniz.
- Mevcut ilkelerin davranışı değiştirilmez, etkilenmez veya silinmez. Mevcut ilkeler, otomatik olarak aynı yapılandırmanızla yeni ayara geçirilir.

### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689----"></a>İOS/ıpados cihazlarında Wi-Fi ağlarında MAC adresi rastgele seçimini devre dışı bırakma<!-- 7758689  -->
İOS/ıpados 14 ' den başlayarak, varsayılan olarak, cihazlar fiziksel MAC adresi yerine bir ağa bağlanırken rastgele bir MAC adresi sunar. Bu davranış, bir cihazı MAC adresine göre izlemek daha zor olduğundan gizlilik için önerilir. Bu özellik ayrıca ağ erişim denetimi (NAC) dahil olmak üzere statik bir MAC adresine dayanan işlevselliği de keser. 

Wi-Fi profillerinde ağ başına rastgele olarak MAC adresi rastgele seçimini devre dışı bırakabilirsiniz (**cihaz**yapılandırma profilleri, for the The The  >  **Configuration profiles**  >  **Create profile**  >  **iOS/iPadOS** **Basic** veya **Enterprise** for Wi-Fi Type for the Configuration for platform > **Wi-> Fi** ).

Şu anda yapılandırabileceğiniz ayarları görmek için [iOS ve ıpados cihazları Için Wi-Fi ayarları ekle](../configuration/wi-fi-settings-ios.md)' ye gidin.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 14 ve üzeri

### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>İOS/ıpados cihazlarında IKEv2 VPN bağlantıları için en yüksek iletim birimini ayarlayın<!-- 7758937  -->
İOS/ıpados 14 ve daha yeni cihazlardan başlayarak, IKEv2 VPN bağlantıları kullanırken özel bir en yüksek iletim birimi (MTU) yapılandırabilirsiniz (**cihaz**  >  **yapılandırma profilleri**profil  >  **Oluştur**  >  **iOS/ıpados** for platform > bağlantı türü **VPN** için > Ikev2).

Yapılandırabileceğiniz ayarlar hakkında daha fazla bilgi için bkz. [Ikev2 ayarları](../configuration/vpn-settings-ios.md#ikev2-settings).

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 14 ve üzeri

### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116----"></a>İOS/ıpados cihazlarındaki e-posta profilleri için hesap başına VPN bağlantısı<!-- 7759116  -->
İOS/ıpados 14 ' ten başlayarak, yerel posta uygulaması için e-posta trafiği, kullanıcının kullandığı hesaba göre bir VPN aracılığıyla yönlendirilebilir. Şimdi, bu hesap tabanlı VPN bağlantısı için kullanılacak bir uygulama başına VPN profili belirtebilirsiniz.  Kullanıcılar, e-posta uygulamasında Kuruluş hesabını kullandıklarında, uygulama başına VPN bağlantısı otomatik olarak açılır.

Şu anda yapılandırabileceğiniz ayarları görmek için [iOS ve ıpados cihazları için e-posta ayarları ekle](../configuration/email-settings-ios.md)' ye gidin.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 14 ve üzeri

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

### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228---"></a>COPE önizleme güncelleştirmesi: iş profiliyle şirkete ait Android Kurumsal cihazları için iş profili parolasını sıfırlama <!--7217228 -->
Gelecekteki bir yönetici eylemi, yöneticilerin Android kurumsal şirkete ait cihazlarda iş profili parolasını bir iş profiliyle sıfırlamasına izin verir.

### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043---"></a>Azure Active Directory birleştirilmiş bir ortak yönetilen cihazı yeniden adlandırma<!--7728043 -->
Azure AD 'ye katılmış bir ortak yönetilen cihazı yeniden adlandırabileceksiniz. Bunu yapmak için, bellek > **cihazlar**  >  **tüm cihazlar** ' a gidin > bir cihaz seçin > **..**  >  . **Cihazı yeniden adlandır**.

### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987---"></a>Zeköşeli cihazlar için PowerPrecision ve PowerPrecision + pille destek<!--3724987 -->
Bir cihazın Donanım Ayrıntıları sayfasında, PowerPrecision ve PowerPrecision ve pil kullanarak Zeköşeli cihazlarla ilgili aşağıdaki bilgileri görebilirsiniz:
- Zepoya tarafından belirlendiği şekilde sistem durumu derecelendirmesi (yalnızca PowerPrecision + piller)
- Tüketilen tam ücret döngüsü sayısı
- Cihazda son bulunan pil için son iade tarihi
- Cihazda en son bulunan pil paketinin seri numarası

<!-- ***********************************************-->
## <a name="intune-apps"></a>Intune uygulamaları

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Windows Şirket Portalı Azure AD kurumsal ve Office Online uygulamalarının birleştirilmiş teslimi<!-- 1817861  -->
2006 sürümünde, [Şirket portalı Azure AD kurumsal ve Office Online uygulamalarının birleştirilmiş teslimini](../fundamentals/whats-new.md)duyurduk. Bu özellik Windows Şirket Portalı desteklenecektir. Intune 'un **Özelleştirme** bölmesinde, Windows Şirket portalı hem **Azure AD kurumsal uygulamalarını** hem de **Office Online uygulamalarını** **gizleme** veya **gösterme** seçeneğini belirleyebileceksiniz. Her Son Kullanıcı tüm uygulama kataloglarını seçilen Microsoft hizmetinden görürler. Varsayılan olarak, her bir ek uygulama kaynağı **gizleyecek**şekilde ayarlanır. Bu yapılandırma ayarını bulmak için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde **Kiracı Yönetimi**  >  **özelleştirmesi** ' nı seçersiniz. İlgili bilgiler için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI uyumluluk raporu şablonu V 2.0<!-- 636958  -->
Yöneticiler, Power BI uyumluluk raporu şablonu sürümünü V 1.0 'dan V 2.0 'a güncelleştirebilir. V 2.0, gelişmiş bir tasarım, Ayrıca, şablonun bir parçası olarak ortaya çıkacak hesaplamalarda ve verilerde yapılan değişiklikleri içerir. İlgili bilgiler için bkz. [Power BI veri ambarına bağlanma](../developer/reports-proc-get-a-link-powerbi.md).


### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Windows 10 ve üzeri için yeni ve geliştirilmiş Microsoft Defender virüsten koruma raporlaması<!-- 6018169  -->
**Endpoint Security**Antivirus altında, Windows 10 ' a Microsoft Defender virüsten koruma dört yeni rapor ekliyoruz  >  **Antivirus**.
- İki işlemsel rapor, *kötü amaçlı yazılım* ve *Aracı durumu*algılanan cihazlar.
- İki kuruluş raporu, *algılanan kötü amaçlı yazılım* ve *Aracı durumu*.

Örnek olarak, işletimsel rapor *Aracısı durumu* cihaz adı, Kullanıcı adı, kullanıcı e-POSTASı ve UPN 'ye bir bakışta ve gerçek zamanlı koruma ile ağ koruması etkinleştirilmişse görüntülenir. Bu raporlar kullanıma hazır olduğunda daha fazla ayrıntı paylaşacağız.

Intune 'da Endpoint Security hakkında daha fazla bilgi için bkz. [Microsoft Intune Endpoint Security 'Yi yönetme](../protect/endpoint-security.md).

### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics-preview--7200950---"></a>Grup ilkesi Analytics kullanarak şirket içi GPO 'larınızı çözümleyin (Önizleme)<!--7200950 -->
**Cihazlar**  >  **Grup İlkesi Analytics (Önizleme)** bölümünde, Grup İlkesi nesnelerinizi (GPO) Endpoint Manager Yönetim merkezinde içeri aktarabilirsiniz. İçeri aktardığınızda Intune, GPO 'YU otomatik olarak analiz eder ve Intune 'da eşdeğer ayarlara sahip olan ilkeleri gösterir. Ayrıca kullanım dışı olan veya artık desteklenmeyen GPO 'Ları gösterir.

Aşağıdakiler cihazlar için geçerlidir:
- Windows 10 ve üzeri

#### <a name="new-windows-10-feature-update-report---6473128----"></a>Yeni Windows 10 Özellik Güncelleştirme raporu<!-- 6473128  -->
**Windows özellik güncelleştirmeleri** raporu, bir **Windows 10 özellik güncelleştirmeleri** ilkesiyle hedeflenen cihazların Uyumluluk görünümünü sağlar. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde, **Reports**  >  Bu raporun özetini görüntülemek için**Windows güncelleştirmeleri (Önizleme)**  >  **özellik güncelleştirme hatalarıyla** ilgili raporlar ' ı seçersiniz. Belirli ilkelerin raporlarını görmek için **raporlar** sekmesini seçin ve **Windows özellik güncelleştirme raporunu**açın. 

#### <a name="new-windows-10-feature-failures-update-report---6473121-----"></a>Yeni Windows 10 özellik arızaları güncelleştirme raporu<!-- 6473121   -->
**Özellik güncelleştirme hataları** raporu, bir **Windows 10 özellik güncelleştirmeleri** ilkesiyle hedeflenen ve güncelleştirme girişiminde bulunan cihazların hata ayrıntılarını sağlar. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **Devices**  >  **Monitor**  >  Bu raporu görüntülemek için cihazlar**özellik güncelleştirme başarısızlıklarını** İzle ' yi seçersiniz. "

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

### <a name="improved-certificate-deployment-for-android-enterprise----6296499----"></a>Android Enterprise için geliştirilmiş sertifika dağıtımı <!-- 6296499  -->
Android kurumsal tam olarak yönetilen, adanmış ve şirkete ait Iş profilleri çalıştıran cihazlar yakında bir cihaz kullanıcısının erişime izin vermek zorunda kalmadan Outlook için S/MIME sertifikaları kullanabilir. S/MIME sertifikaları, cihaz yapılandırması için PKCS içeri aktarılan sertifika profili kullanılarak dağıtılır. (**Cihazlar**  >  **Yapılandırma profilleri**  >  **Profil oluştur**  >  **Android kurumsal**  >  *Tam olarak yönetilen, adanmış ve şirkete ait Iş profili*Için kategoriden **PKCS içeri aktarılan sertifika** .

### <a name="tri-state-options-for-settings-are-coming-to-endpoint-security-firewall-policy---6586159-----"></a>Ayarlar için üçlü durum seçenekleri Endpoint Security Güvenlik Duvarı ilkesine geliyor<!-- 6586159   -->
Endpoint Security Güvenlik Duvarı ilkelerinde, platformun (Windows veya MacOS) ek seçeneği (**uç nokta güvenlik**  >  **güvenlik duvarı**) destekleyebildiği ayarlar için üçüncü bir yapılandırma durumu ekliyoruz.

Örneğin, şu anda bir ayar **yapılandırılmadığı** ve **Evet**, platform tarafından destekleniyorsa, **Hayır**seçeneğini ekleyeceğiz.

### <a name="new-security-baseline-for-office---3150261----"></a>Office için yeni güvenlik temeli<!-- 3150261  -->
Microsoft Office O365 ayarlarını yönetmek için yeni bir güvenlik temeli (**uç nokta güvenlik**  >  **güvenliği temelleri**) ekliyoruz. *Microsoft Office O365* Taban çizgisi ayarları, *eklenti yönetimi*,  *MIME işleme*ve daha fazlası gibi Office uygulamalarına yönelik yapılandırmaların dahil edilir.

### <a name="improved-status-details-in-security-baseline-reports---7221051------"></a>Güvenlik temeli raporlarında geliştirilmiş durum ayrıntıları<!-- 7221051    -->
Dağıtılan güvenlik temellerinizin sonuçlarını görüntülerken göreceğiniz durum ayrıntılarını geliştiriyoruz. (**Uç nokta güvenliği**  >  **Güvenlik temelleri**  >   **Windows 10 güvenlik temelleri**profilleri *gibi bir güvenlik temeli türü seçin*  >  **Profiles**  >  *durumu görüntülemek için bu profilin bir örneğini seçin*  >  **cihaz durumu***gibi bir profil raporu seçin*

Geliştirmeler, durum için kullandığımız ortak Etiketler ve tanımları, durumun amacına daha iyi uyacak şekilde düzeltecektir. Örnek:
- **Eşleşen taban çizgisi**  , **varsayılan ayarlarla eşleşecek**şekilde güncelleştirilecek ve bu, bir cihaz yapılandırmasının varsayılan (değiştirilmemiş) temel yapılandırmasıyla ne zaman eşleştiğini daha iyi açıklar.
- **Yanlış yapılandırılmış** ayrıntılar, **hata**, **Çakışma**ve **bekleyen**gibi daha ayrıntılı bilgiler oluşturacak. Yeni durumlar konsolunun diğer bölümlerine tutarlılığı sağlar.

### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374--idstaged---"></a>Uç nokta güvenlik rolü için genişletilmiş RBAC izinleri<!--7312374  idstaged -->
Intune için **uç nokta güvenlik yöneticisi** rolü, uzak görevler için ek rol tabanlı erişim denetımı (RBAC) izinleri alıyor. Bu rol, Microsoft Endpoint Manager yönetim merkezine erişim verir ve güvenlik temelleri, cihaz uyumluluğu, koşullu erişim ve Microsoft Defender Gelişmiş tehdit koruması dahil olmak üzere güvenlik ve uyumluluk özelliklerini yöneten kişiler tarafından kullanılabilir.

Bir Intune RBAC rolünün iznini görüntülemek için (**Kiracı Yöneticisi**  >  **Intune rolleri**  >  *bir rol*  >  **izinleri**seçin) bölümüne gidin.

Uzak görevler için genişletilmiş izinler şunları içerir:

- Şimdi yeniden Başlat
- Uzaktan kilitleme
- BitLockerKeys 'i döndürme (Önizleme)
- Filekasa anahtarını döndür
- Cihazları eşitleme
- Microsoft Defender
- Yapılandırma Yöneticisi eylemini Başlat

### <a name="updates-for-security-baselines---7102146-7103916----"></a>Güvenlik temelleri için güncelleştirmeler<!-- 7102146, 7103916  -->
Güncelleştirmeleri yakında aşağıdaki güvenlik temellerine yayınlarız (**uç nokta güvenlik**  >  **güvenliği temelleri**):
- **MDM güvenlik temeli** (Windows 10 güvenliği)
- **Microsoft Defender ATP temeli**

Güncelleştirilmiş temel sürümler, ilgili ürün ekipleri tarafından önerilen en iyi yöntem yapılandırmalarının bakımını yapmanıza yardımcı olmak için son ayarlar için destek getirir.

### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503--idstaged----"></a>Cihazların ilke çakışmalarının kaynağını belirlemek için uç nokta güvenlik yapılandırması ayrıntılarını kullanın<!-- 7567503  idstaged  -->
Çakışma çözümüne yardımcı olmak için, bir güvenlik temeli profili aracılığıyla, seçilen bir cihaz için *uç nokta güvenlik yapılandırmasını* görüntülemek üzere detaya gidebilirsiniz. Buradan, bir *Çakışma* veya *hata* gösteren ayarları seçebilir ve çakışmanın bir parçası olan profilleri ve ilkeleri içeren ayrıntıların bir listesini görüntülemek için ayrıntıya devam edebilirsiniz. Daha sonra bir çakışmanın kaynağı olan bir ilke seçerseniz, Intune ilke yapılandırmasını gözden geçirebileceğiniz veya değiştirebileceğiniz ilkelere genel bakış bölmesini açar. (**Cihazlar**  >  *bir cihaz seçin*  >  **Uç nokta güvenlik yapılandırması**  >  *bir profil veya taban çizgisi seçin*  >  *Cihaza uygulanan ayarlar listesinden bir ayar seçin*.

Aşağıdaki ilke türleri bir güvenlik temeliyle detaydan bir çakışma kaynağı olarak tanımlanabilir:
- Cihaz yapılandırma ilkesi
- Uç nokta güvenlik ilkeleri

### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-----"></a>Bir cihaz için uç nokta güvenlik yapılandırmasındaki yeni ayrıntılar<!-- 7745029   -->
Cihazların bir uç nokta güvenlik yapılandırması kapsamında görüntülenecek olan cihazlar için yeni ayrıntılar ekliyoruz. (**Uç nokta güvenliği**  >  **Güvenlik temelleri**  >  *Seçili taban çizgisi*  >  **Profiller**  >  *Seçili profil*  >  **Cihaz durumu**  >  **Uç nokta güvenlik yapılandırması**). Yeni Ayrıntılar:

- **UPN** (Kullanıcı asıl adı): UPN, cihazdaki belirli bir kullanıcıya hangi uç nokta Güvenlik profilinin atandığını tanımlar. Bu, bir cihazdaki birden çok kullanıcının ve cihaza atanan bir profilin veya taban çizgisinin birden çok girişinin ayırt edilmesine yardımcı olmak için yararlıdır. 
- En **kötü durum**: Bu ayrıntı, cihaz için en düşük iyi durum koşulunu tanımlar. Bu durum **başarılı**olduğunda, cihazda ilke çakışması veya hatası yok demektir.

### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Android 11 güvenilen kök sertifikaların Cihaz Yöneticisi kayıtlı cihazlara dağıtımını kullanımdan kaldırma<!--7662775  -->
Android 11 ile, güvenilen kök sertifikalar artık *Android Cihaz Yöneticisi*olarak kaydedilmiş cihazlara dağıtılamaz. Bu değişiklik, Intune 'un Knox platformuyla tümleştirilmesi nedeniyle Samsung KNOX cihazlarını etkilemez. Samsung olmayan cihazlarda, kullanıcıların güvenilen kök sertifikayı cihaza el ile yüklemesi gerekir. 

Güvenilir kök sertifika bir cihaza el ile yüklendiğinde, cihaza sertifika sağlamak için SCEP kullanabilirsiniz. Bu senaryoda, hala cihaza *güvenilir bir sertifika* İlkesi oluşturup dağıtmanız ve bu ilkeyi *SCEP sertifika* profiline bağlamanız gerekir.

- Güvenilir kök sertifika cihazdayken, SCEP sertifika profili başarıyla yüklenir. 
- Güvenilen sertifika bulunamazsa, SCEP sertifika profili başarısız olur.

<!-- ***********************************************-->
## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Ayrıca bkz.

Son gelişmeler hakkında daha fazla bilgi için bkz. [Microsoft Intune](whats-new.md)yenilikleri.
