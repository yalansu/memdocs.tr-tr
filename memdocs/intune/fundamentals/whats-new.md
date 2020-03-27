---
title: Microsoft Intune - Azure’daki yenilikler | Microsoft Docs
titleSuffix: ''
description: Intune Azure portalındaki yenilikleri keşfedin
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: b33b33415628dab471d1d4951e141c2ce718eaa0
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326657"
---
# <a name="whats-new-in-microsoft-intune"></a>Microsoft Intune yenilikler nelerdir?

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde Microsoft Intune her hafta yenilikleri öğrenin. Ayrıca, [önemli bildirimler](#notices), [Geçmiş yayınlar](whats-new-archive.md)ve [Intune hizmet güncelleştirmelerinin nasıl yayımlandığına](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)ilişkin bilgileri de bulabilirsiniz. 

> [!Note]
> Her [aylık güncelleştirmenin](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) piyasaya çıkma üç güne kadar sürebilir ve şu sırada olacaktır:
>
> - Gün 1: Asya Pasifik (APAC)
> - Gün 2: Avrupa, Orta Doğu, Afrika (EMEA)
> - Gün 3: Kuzey Amerika
> - Gün 4 +: kamu için Intune
>
> Bazı özelliklerin piyasaya çıkması birkaç haftayı bulabilir ve tüm özellikler ilk hafta bütün müşterilerimize sunulmamış olabilir.
>
> Bir sürümdeki yaklaşan özelliklerin bir listesi için [geliştirme sayfasını](in-development.md) inceleyin.

**RSS akışı**: aşağıdaki URL 'yi kopyalayıp akış okuyucunuzun içine yapıştırarak Bu sayfa güncelleştirildikten sonra bildirim alın: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
-->  

<!-- ########################## -->
## <a name="week-of-march-16-2020-2003-service-release"></a>16 Mart 2020 haftası (2003 hizmet sürümü)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>macOS ve iOS Şirket Portalı güncelleştirmeleri<!-- 5779439, 5780234  -->
MacOS ve iOS Şirket Portalı profil bölmesi, oturum kapatma düğmesini içerecek şekilde güncelleştirilmiştir. Ayrıca, macOS Şirket Portalı profil bölmesinde UI geliştirmeleri yapılmıştır. Şirket Portalı hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Web kliplerini iOS cihazlarında Microsoft Edge 'e yeniden hedefle<!-- 5455276   -->
Korunan bir tarayıcıda açılması gereken iOS cihazlarında yeni dağıtılan web klipleri (sabitlenmiş Web uygulamaları) Intune Managed Browser yerine Microsoft Edge 'de açılır. Managed Browser yerine Microsoft Edge 'de açıldıklarından emin olmak için önceden mevcut web kliplerini yeniden hedeflemeniz gerekir. Daha fazla bilgi için bkz. [Microsoft Edge kullanarak Web erişimini yönetme Microsoft Intune](../apps/manage-microsoft-edge.md) ve [Microsoft Intune Web uygulamaları ekleme](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Android için Microsoft Edge ile Intune Tanılama aracını kullanma<!-- 4735244  -->
Android için Microsoft Edge artık Intune Tanılama aracı ile tümleşiktir. İOS için Microsoft Edge deneyiminden benzer şekilde, cihazdaki Microsoft Edge 'in URL çubuğuna "about: ıntunehelp" girilmesi, Intune Tanılama aracını başlatacak. Bu araç ayrıntılı Günlükler sağlar. Kullanıcılar bu günlükleri kendi BT departmanlarına toplayıp göndermek veya belirli uygulamalar için MAM günlüklerini görüntülemek için Kılavuzlu olabilir.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Intune marka ve özelleştirme güncelleştirmeleri<!-- 5236032  -->
"Marka ve özelleştirme" adlı Intune bölmesini, geliştirmeler de dahil olmak üzere güncelleştirdik:

- Bölmeyi **özelleştirmek**için yeniden adlandırma.
- Kuruluş ve ayarların tasarımını geliştirme.
- Ayarlar metin ve araç ipuçlarını geliştirme.

Bu ayarları Intune 'da bulmak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' ne gidin, **Kiracı Yönetimi** > **Özelleştirme**' yi seçin. Varolan özelleştirme hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Kullanıcının kişisel şifreli kurtarma anahtarı<!-- 6273943  -->
Kullanıcıların, Android Şirket Portalı uygulaması veya Android Intune uygulaması aracılığıyla Mac cihazları için kişisel şifreli **Filekasasını** kurtarma anahtarını almasına olanak sağlayan yeni bir Intune özelliği vardır. Hem Şirket Portalı uygulaması hem de Intune uygulamasında, kullanıcının Mac cihazlarına erişmek için gereken **Filekasasını** kurtarma anahtarını görebildiği Web şirket portalı bir Chrome tarayıcısı açacak bir bağlantı vardır. Şifreleme hakkında daha fazla bilgi için bkz. [Intune ile cihaz şifrelemesini kullanma](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580-wnready---"></a>İyileştirilmiş ayrılmış cihaz kaydı <!-- 6114580 wnready -->
Android kurumsal adanmış cihazları için kaydı iyileştirmekte ve Wi-Fi ile ilişkili SCEP sertifikalarının, 22 Kasım 2019 ' den önce kaydedilen adanmış cihazlara uygulanması daha kolay hale getiriyoruz. Yeni kayıtlar söz konusu olduğunda, Intune uygulaması yüklenmeye devam eder, ancak son kullanıcıların kayıt sırasında **Intune Aracısını Etkinleştir** adımını gerçekleştirmesi artık gerekmez. Taksit arka planda otomatik olarak gerçekleşir ve Wi-Fi ile ilişkili SCEP sertifikaları, son kullanıcı etkileşimi olmadan dağıtılabilir ve ayarlanabilir.  

Bu değişiklikler, Intune hizmet arka ucu dağıttığı için Mart ayının her gününde aşamalı olarak kullanıma sunulacaktır. Tüm kiracıların bu yeni davranışı Mart sonuna kadar olacak. İlgili bilgiler için bkz. [Android kurumsal adanmış CIHAZLARDA SCEP sertifikaları Için destek](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Windows cihazlarında Yönetim Şablonları oluştururken yeni kullanıcı deneyimi<!--5096036 -->
Müşteri geri bildirimlerine göre ve yeni Azure tam ekran deneyimine geçtiğimiz için, Yönetim Şablonları profili deneyimini bir klasör görünümüyle yeniden oluşturduk. Herhangi bir ayarlarda veya mevcut profillerde değişiklik yapmadık. Bu nedenle, mevcut profilleriniz aynı kalır ve yeni görünümde kullanılabilir. **Tüm ayarlar ' ı**seçip ara ' yı kullanarak tüm ayarlar seçeneklerinde gezinmeye devam edebilirsiniz. Ağaç görünümü bilgisayar ve Kullanıcı yapılandırmalarına göre bölünür. Windows, Office ve Edge ayarlarını ilişkili klasörlerinde bulacaksınız.  

Uygulama alanı:
- Windows 10 ve üzeri

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>IKEv2 VPN bağlantılarına sahip VPN profilleri, her zaman iOS/ıpados cihazlarıyla birlikte kullanılabilir<!-- 1947932   -->
İOS/ıpados cihazlarında, Ikev2 bağlantısı kullanan bir VPN profili oluşturabilirsiniz (**cihaz** > **yapılandırma profilleri** > profil **oluşturma** > **iOS/ıpados** , profil türü için > **VPN** ). Şimdi, Ikev2 ile her zaman açık yapılandırma yapabilirsiniz. Yapılandırıldığında, IKEv2 VPN profilleri otomatik olarak bağlanır ve VPN 'ye bağlı (veya hızlı bir şekilde yeniden bağlantı) kalır. Ağlar arasında hareket etmekle veya cihazları yeniden başlatırken bile bağlı kalır.

İOS/ıpados 'da, her zaman VPN Ikev2 profilleriyle sınırlıdır.

Yapılandırabileceğiniz Ikev2 ayarlarını görmek için [Microsoft Intune iOS CIHAZLARıNDA VPN ayarları ekle](../configuration/vpn-settings-ios.md#ikev2-settings)' ye gidin.

Uygulama alanı:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Android kurumsal cihazlarda OEMConfig cihaz yapılandırma profillerindeki paketleri ve paket dizilerini silme<!-- 5550355   -->
Android kurumsal cihazlarda, OEMConfig **profilleri oluşturun ve** güncelleştirin (**cihaz** > **yapılandırma profilleri** >  > SDK için **Android Enterprise** > profil türü için **oemconfig** ). Kullanıcılar artık Intune 'daki **yapılandırma tasarımcısını** kullanarak demeti ve paket dizilerini silebilir.

OEMConfig profilleri hakkında daha fazla bilgi için bkz. [Microsoft Intune 'de oemconfig Ile Android Kurumsal cihazları kullanma ve yönetme](../configuration/android-oem-configuration-overview.md).

Uygulama alanı:
- Android Kurumsal

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>İOS/ıpados Microsoft Azure AD SSO uygulama uzantısını yapılandırma<!-- 5672534   -->
Microsoft Azure AD ekibi, iOS/ıpados 13.0 + kullanıcılarına tek bir oturum açma ile Microsoft uygulamalarına ve Web sitelerine erişim elde etmesine izin vermek için bir yeniden yönlendirme çoklu oturum açma (SSO) uygulama uzantısı oluşturdu. Daha önce Microsoft Authenticator uygulama ile aracılı kimlik doğrulaması yapmış olan tüm uygulamalar, yeni SSO uzantısıyla SSO almaya devam edecektir. Azure AD SSO uygulama uzantısı sürümü sayesinde, SSO uzantısını yeniden yönlendirme **SSO uygulama uzantısı**türü (**cihazlar** > **yapılandırma profilleri** > profil **oluşturma** > **iOS/IPA> > DOS** ) ile yapılandırabilirsiniz. **Device features**

Uygulama alanı:
- iOS 13,0 ve üzeri
- ıpados 13,0 ve üzeri

İOS SSO uygulama uzantıları hakkında daha fazla bilgi için bkz. [Çoklu oturum açma uygulama uzantısı](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>Kurumsal uygulama güven ayarları değiştirme ayarı iOS/ıpados cihaz kısıtlama profillerden kaldırılır<!-- 6225131   -->
İOS/ıpados cihazlarında, bir cihaz kısıtlama profili (**cihazlar** > **yapılandırma profilleri** oluşturma > profil **oluşturma** için **iOS/IPA> DOS** > profil türü için **cihaz kısıtlamaları** ) oluşturun. **Kurumsal uygulama güven ayarları değiştirme** ayarı Apple tarafından kaldırılır ve Intune 'dan kaldırılır. Şu anda bu ayarı bir profilde kullanıyorsanız, hiçbir etkisi yoktur ve mevcut profillerden kaldırılır. Bu ayar ayrıca Intune 'daki herhangi bir raporlamadan kaldırılır.

Uygulama alanı:
- iOS/iPadOS

Kısıtlayacakları ayarları görmek için [iOS ve ıpados cihaz ayarları ' na giderek özelliklere izin verin veya kısıtlayın](../configuration/device-restrictions-ios.md).

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Sorun giderme: bekleyen MAM ilkesi bildirimi bilgilendirici simgesine değiştirildi<!--6348954 -->
Sorun giderme dikey penceresinde bekleyen bir MAM ilkesi için bildirim simgesi bir bilgilendirme simgesine değiştirilmiştir.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Uyumluluk ilkesini yapılandırırken kullanıcı arabirimi güncelleştirmesi<!-- 3961639    -->
Microsoft Endpoint Manager 'da [uyumluluk ilkeleri oluşturmak](../protect/create-compliance-policy.md#create-the-policy) için Kullanıcı arabirimini güncelleştirdik (**cihaz** > **uyumluluk ilkeleri** > **ilkeleri** **ilke oluştur** > ). Daha önce kullandığınız ayarların ve ayrıntıların aynısını içeren yeni bir kullanıcı deneyimi sunuyoruz. Yeni deneyim, Uyumluluk ilkesini oluşturmak için sihirbaza benzer bir süreç izler ve ilke için *atamalar* ekleyebileceğiniz bir sayfa ve ilkeyi oluşturmadan önce yapılandırmanızı gözden geçirebileceğiniz bir *İnceleme + oluştur* sayfası içerir.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Uyumsuz cihazları devre dışı bırak<!-- 1827291       -->
Uyumsuz cihazlara ekleyebileceğiniz uyumlu olmayan cihazlar için, [uyumsuz cihazı devre dışı](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance)bırakmak üzere yeni bir eylem ekledik.  Yeni eylem, **uyumsuz cihazı devre dışı bırakma**, cihazdaki tüm şirket verilerinin kaldırılmasına neden olur ve ayrıca cihazın Intune tarafından yönetilmesini kaldırır.  Bu eylem, gün cinsinden yapılandırılan değere ulaşıldığında ve bu noktada cihaz kullanımdan kalkmaya uygun hale geldiğinde çalışır. Minimum değer 30 gündür.  Yöneticilerin uygun olan tüm cihazları devre dışı bırakabileceği *uyumlu olmayan cihazları devre* dışı bırak bölümü kullanılarak cihazları devre dışı bırakmak IÇIN açık BT yöneticisi onayı gerekecektir.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>İOS Enterprise Wi-Fi profillerinde WPA ve WPA2 desteği<!--6215273   -->
[İOS Için Enterprise Wi-Fi profilleri](../configuration/wi-fi-settings-ios.md#enterprise-profiles) artık *güvenlik türü* alanını destekliyor. *Güvenlik türü*Için, **WPA Enterprise** veya **WPA/WPA2 kurumsal**seçeneklerinden birini seçebilir ve ardından *EAP türü*için bir seçim belirtebilirsiniz.  (**Cihazlar** > **yapılandırma profilleri** > **Profil oluştur** ve *Platform* için **iOS/ıpados** ve ardından *profil*için **Wi-Fi** seçin). 

Yeni kurumsal seçenekler, iOS için temel bir Wi-Fi profili için kullanılabilir olanlar gibidir.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Sertifika, e-posta, VPN ve Wi-Fi, VPN profilleri için yeni kullanıcı deneyimi<!-- 5615208   -->
Aşağıdaki profil türlerini oluşturmak ve değiştirmek için uç nokta yönetimi Yönetim Merkezi 'ndeki (**cihazlar** > **yapılandırma profilleri** > **profil oluşturma**) [Kullanıcı deneyimini](../configuration/device-profile-create.md) güncelleştirdik. Yeni deneyim, daha önce olduğu gibi aynı ayarları sunar, ancak çok yatay kaydırma gerektirmeyen sihirbaza benzer bir deneyim kullanır. Mevcut konfigürasyonları yeni deneyimle değiştirmeniz gerekmez.

- Türetilmiş kimlik bilgileri
- E-posta
- PKCS sertifikası
- PKCS içeri aktarılmış sertifikası
- SCEP sertifikası
- Güvenilir sertifika
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Şirket Portalı, Android ve iOS için kayıt için kullanılabilir olup olmadığını yapılandırın<!-- 4260128  -->
Android ve iOS cihazlarındaki Şirket Portalı cihaz kaydının, istemler olmadan veya kullanıcılar tarafından kullanılamayan istemlerle kullanılabilir olup olmadığını yapılandırabilirsiniz. Bu ayarı Intune 'da bulmak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' ne gidin ve > **cihaz kaydını** **düzenlemek** > **Kiracı Yönetimi** > **Özelleştirme** ' yi seçin.  

Cihaz kayıt ayarı için destek, son kullanıcıların bu Şirket Portalı sürümlerine sahip olmasını gerektirir:
-    İOS üzerinde Şirket Portalı: sürüm 4,4 veya üzeri
-    Android üzerinde Şirket Portalı: sürüm 5.0.4715.0 veya üzeri

Varolan Şirket Portalı özelleştirmesi hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Android cihazlarına yeni Android raporuna genel bakış sayfası<!-- 5435435   -->
Her bir cihaz yönetimi çözümüne kaç tane Android cihaz kaydedildiğini gösteren Android cihazlara Genel Bakış sayfasında Microsoft Endpoint Manager yönetim konsoluna bir rapor ekledik. Bu grafik (Azure konsolunda aynı grafik gibi), iş profilini, tam olarak yönetilen, adanmış ve Cihaz Yöneticisi kayıtlı cihaz sayısını gösterir. Raporu görmek için **cihazlar** > **Android** > **genel bakış**' ı seçin.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-idready-wnready-wnstaged--"></a>Android Cihaz Yöneticisi yönetiminden iş profili yönetimine kadar Kullanıcı Kılavuzu<!--5857738 idready wnready wnstaged-->
Android Cihaz Yöneticisi platformu için yeni bir uyumluluk ayarı yayınlıyoruz. Bu ayar cihaz yöneticisiyle yönetiliyorsa bir cihazı uyumsuz hale getirme olanağı sağlar.

Uyumlu olmayan bu cihazlarda, **cihaz ayarlarını Güncelleştir** sayfasında kullanıcılar **yeni cihaz yönetimi kurulum** iletisi ' ne git ' i görür. **Çözümle** düğmesine dokunduklarında, bunlara göre kılavuzluk edilecek:

1. Cihaz Yöneticisi yönetiminden kaydı geri al
2. İş profili yönetimine kaydolma
3. Uyumluluk sorunlarını çözme 
 
Google, Android Enterprise ile modern, daha zengin ve daha güvenli cihaz yönetimine geçme çabasında yeni Android sürümlerindeki Cihaz Yöneticisi desteğini düşürdüğünde.  Intune, yalnızca S2 CY2020 aracılığıyla Android 10 ve üzeri çalıştıran cihaz yönetici tarafından yönetilen Android cihazları için tam destek sağlayabilir. Android 10 veya sonraki sürümleri çalıştıran Cihaz Yöneticisi tarafından yönetilen cihazlar (Samsung hariç), tamamen yönetilemez. Özellikle, etkilenen cihazlar yeni parola gereksinimleri almaz. Daha fazla bilgi için bu [bildirimin](#decreasing-support-for-android-device-administrator)bölümüne bakın.

Bu ayar hakkında daha fazla bilgi için bkz. [Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşıma](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Veri ambarı artık MAC adresini sağlıyor<!-- 6123680  -->
Intune veri ambarı, yöneticilerin Kullanıcı ve ana bilgisayar MAC adresi arasında ilişki yapmasına izin vermek için `device` varlığındaki yeni bir Özellik (`EthernetMacAddress`) olarak sunulur. Bu özellik belirli kullanıcılara ulaşmaya ve ağda gerçekleşen olay sorunlarını gidermenize yardımcı olur. Yöneticiler daha zengin raporlar oluşturmak için bu özelliği [Power BI raporlarında](../developer/reports-proc-get-a-link-powerbi.md) da kullanabilir. Daha fazla bilgi için bkz. Intune veri ambarı [cihaz](../developer/intune-data-warehouse-collections.md#devices) varlığı.

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Ek veri ambarı cihaz envanteri özellikleri<!-- 6125732  -->
Intune veri ambarı kullanılarak ek cihaz envanteri özellikleri kullanılabilir. Aşağıdaki özellikler artık [cihazlar](../developer/intune-data-warehouse-collections.md#devices) koleksiyonu aracılığıyla kullanıma sunulmuştur:
- ' Model '-cihaz modeli.
- ' Office365Version '-cihaza yüklü Office 365 sürümü.
- ' Physicalmemorınbytes '-bayt cinsinden fiziksel bellek.
- `TotalStorageSpaceInBytes`-toplam depolama kapasitesi (bayt cinsinden).

Daha fazla bilgi için bkz. [Microsoft Intune veri ambarı API 'si](../developer/reports-nav-intune-data-warehouse.md) ve Intune veri ambarı [cihaz](../developer/intune-data-warehouse-collections.md#devices) varlığı.

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Ek hizmetleri desteklemek için yardım ve destek iş akışı güncelleştirmesi<!-- 5654170   -->
Microsoft Endpoint Manager Yönetim Merkezi 'ndeki yardım ve destek sayfasını, artık [kullandığınız yönetim türünü seçtiğiniz](../fundamentals/get-support.md#options-to-access-help-and-support)şekilde güncelleştirdik. Bu değişiklik ile aşağıdaki yönetim türlerinden seçim yapabilirsiniz:

- Configuration Manager (Masaüstü analizlerini içerir)
- Intune
- Ortak yönetim

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Güvenlik

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Endpoint Security 'nin bir parçası olarak güvenlik yöneticisi odaklı ilkelerinin önizlemesini kullanın<!--6131401  -->
Genel önizleme olarak, Microsoft uç nokta yönetimi Yönetim Merkezi 'nde uç nokta güvenlik düğümü altına birçok yeni ilke grubu ekledik. Güvenlik Yöneticisi olarak, bu yeni ilkeleri cihaz güvenliğinin belirli yönlerine odaklanmak için, daha büyük cihaz yapılandırma ilkesi gövdesinin ek yükü olmadan farklı ilgili ayarları yönetmek üzere kullanabilirsiniz.

*Microsoft Defender virüsten koruma için yeni virüsten koruma ilkesi* dışında (aşağıda bkz.), bu yeni önizleme ilkelerinin ve profillerinin her bir sürümündeki ayarlar şu anda [cihaz yapılandırma profilleri](../configuration/device-profile-create.md) aracılığıyla yapılandırdığınız ayarların aynısıdır.

Aşağıda, önizleme aşamasında olan yeni ilke türleri ve bunların kullanılabilir profil türleri verilmiştir:

- **Virüsten koruma (Önizleme)** :
  - MacOS
    - **Virüsten koruma** - [Mac IÇIN Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)'Yi yönetmek üzere MacOS için [Virüsten koruma ilkesi ayarlarını](../protect/antivirus-microsoft-defender-settings-macos.md) yönetin.

  - Windows 10 ve üzeri:
    - **Microsoft Defender virüsten koruma** -bulut koruması, virüsten koruma dışlamaları, düzeltme, tarama seçenekleri ve daha fazlası Için [Virüsten koruma ilkesi ayarlarını](../protect/antivirus-microsoft-defender-settings-windows.md) yönetin.

      *Microsoft Defender virüsten koruma* Için virüsten koruma profili, cihaz kısıtlama profilinin bir parçası olarak bulunan ayarların yeni bir örneğini tanıtan bir özel durumdur. Bu yeni virüsten koruma ayarları:

        - , Cihaz kısıtlamalarında bulunan ayarlardır, ancak cihaz kısıtlaması olarak yapılandırıldığında kullanılamayan yapılandırma için üçüncü bir seçeneği destekler.
        - Endpoint Protection için [ortak yönetim iş yükü kaydırıcısının](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) Intune olarak ayarlandığı durumlarda Configuration Manager ile birlikte yönetilen cihazlara uygulanır.

     Bir cihaz kısıtlama profili aracılığıyla yapılandırma yerine yeni *Virüsten koruma* > *Microsoft Defender virüsten koruma* profilini kullanmayı planlayın.

  - **Windows Güvenlik deneyimi** -son kullanıcıların Microsoft Defender Güvenlik Merkezi 'nde görüntüleyebilecekleri Windows güvenlik ayarlarını ve aldıkları bildirimleri yönetin. Bu ayarlar, cihaz yapılandırma Endpoint Protection profili olarak kullanılabilenlerden değiştirilmez.

- **Disk şifrelemesi (Önizleme)** :
  - MacOS
    - **FileVault**
  - Windows 10 ve üzeri:
    - **Kurulumu**
- **Güvenlik Duvarı (Önizleme)** :
  - MacOS
    - **macOS güvenlik duvarı**
  - Windows 10 ve üzeri:
    - **Microsoft Defender güvenlik duvarı**
- **Uç nokta algılama ve yanıt (Önizleme)** :
  - Windows 10 ve üzeri: -**Windows 10 Intune**
- **Saldırı yüzeyi azaltma (Önizleme)** :
  - Windows 10 ve üzeri:
    - **Uygulama ve tarayıcı yalıtımı**
    - **Web koruması**
    - **Uygulama denetimi**
    - **Saldırı yüzeyi azaltma kuralları**
    - **Cihaz denetimi**
    - **Exploit koruması**
- **Hesap koruması (Önizleme)** :
  - Windows 10 ve üzeri:
    - **Hesap koruması**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>9 Mart 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Win32 uygulama içeriğini indirirken teslim Iyileştirme aracısını yapılandırma<!-- 5410945 -->

Teslim Iyileştirme aracısını, atamaya göre arka planda veya ön plan modunda Win32 uygulama içeriğini indirmek için yapılandırabilirsiniz. Mevcut Win32 uygulamaları için içerik arka plan modunda indirilmeye devam edecektir. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **uygulamalar** > **tüm uygulamalar** ' ı seçin > *Win32 uygulama* > **özelliklerini**seçin. **Atamalar**' ın yanındaki **Düzenle** ' yi seçin.  **Gerekli** bölümde **mod** altında **Ekle** seçeneğini belirleyerek atamayı düzenleyin.  Yeni ayarı, **uygulama ayarları** bölümünde bulabilirsiniz. Teslim Iyileştirme hakkında daha fazla bilgi için bkz. [Win32 uygulama yönetimi-teslim iyileştirmesi](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Windows cihazları için birincil kullanıcıyı değiştirme<!-- 3794742   -->
Birincil kullanıcıyı Windows hibrit ve Azure AD 'ye katılmış cihazlar için değiştirebilirsiniz. Bunu yapmak için **ıntune** > **cihazlar** > **tüm cihazlar** ' a gidin > bir cihaz > **özellikleri** > **birincil Kullanıcı**seçin. Daha fazla bilgi için bkz. [bir cihazın birincil kullanıcısını değiştirme](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

Bu görev için yeni bir RBAC izni (yönetilen cihazlar/set birincil kullanıcı) de oluşturuldu. Bu izin, yardım masası operatörü, Okul Yöneticisi ve uç nokta güvenlik Yöneticisi dahil yerleşik rollere eklenmiştir.

Bu özellik, genel olarak önizleme aşamasında müşterilere gönderilir. Sonraki birkaç hafta içinde özelliği görmeniz gerekir.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>2 Mart 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Microsoft Uç Nokta Yöneticisi kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri<!-- 6317104, CM3555758-->
Microsoft Uç Nokta Yöneticisi tek bir konsolda Configuration Manager ve Intune 'U bir araya getiriyor. Configuration Manager Technical Preview sürüm 2002,2 ' den başlayarak, Configuration Manager cihazlarınızı bulut hizmetine yükleyebilir ve yönetici merkezinde bu işlemler üzerinde işlem yapabilirsiniz. Daha fazla bilgi için [Configuration Manager Technical Preview sürüm 2002,2 ' deki Özellikler](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach)bölümüne bakın.

Bu güncelleştirmeyi yüklemeden önce [Configuration Manager Technical Preview makalesini](https://docs.microsoft.com/configmgr/core/get-started/technical-preview) gözden geçirin. Bu makale, Technical Preview kullanma, sürümler arasında güncelleştirme ve geri bildirim sağlama ile ilgili genel gereksinimleri ve sınırlamaları tamamladığınızda tercihinize.

#### <a name="bulk-remote-actions--4576882--"></a>Toplu uzak eylemler<!--4576882-->
Artık şu uzak eylemler için toplu komutlar verebilirsiniz: yeniden başlatma, yeniden adlandırma, Autopilot sıfırlama, silme ve silme. Yeni toplu eylemleri görmek için [Microsoft Endpoint Manager yönetim merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) > **cihazlar** > **tüm cihazlar** **toplu işlemler** > ' ne gidin.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Tüm cihazlar için geliştirilmiş arama, sıralama ve filtreleme listeleri<!--6179023-->
Tüm cihazlar listesi, daha iyi performans, arama, sıralama ve filtreleme için geliştirilmiştir. Daha fazla bilgi için [Bu destek ipucunu](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946)inceleyin.

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>24 Şubat 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>macOS Şirket Portalı Kullanıcı deneyimi geliştirmeleri<!-- 5568987 -->
MacOS cihaz kayıt deneyimlerine ve Mac için Şirket Portalı uygulamasına yönelik iyileştirmeler yaptık. Aşağıdaki geliştirmeleri görürsünüz:
- Kayıt sırasında, kullanıcılarınızın Şirket Portalı en son sürümüne sahip olmasını sağlayacak daha iyi bir Microsoft **Otomatik güncelleştirme** deneyimi.
- Kayıt sırasında gelişmiş bir uyumluluk denetimi adımı.
- Kopyalanmış olay kimlikleri için destek, kullanıcılarınız cihazlarından Şirket destek ekibine daha hızlı bir şekilde hata gönderebilir.

Mac için kayıt ve Şirket Portalı uygulaması hakkında daha fazla bilgi için bkz. [Şirket Portalı uygulamasını kullanarak macOS cihazınızı kaydetme](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Daha Iyi mobil için uygulama koruma ilkeleri artık iOS ve ıpados 'yi destekliyor<!-- 6224512  -->

Ekim 2019 ' de Intune uygulama koruma ilkesi, Microsoft tehdit savunma iş ortaklarımızın verilerini kullanma özelliğini ekledi. Bu güncelleştirmeyle, artık iOS ve ıpados üzerinde daha Iyi bir mobil uygulama kullanarak kullanıcıların şirket verilerini engellemek veya seçmeli olarak silmek için bir uygulama koruma İlkesi kullanabilirsiniz.  Daha fazla bilgi için bkz. [Intune Ile mobil tehdit savunma uygulama koruma Ilkesi oluşturma](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Tüm cihazlar listesinden Şimdi daraltılmış CSV biçiminde dışarı aktarır<!--6343117-->
**Cihazların** > **tüm cihazlar** sayfası artık daraltılmış CSV biçiminde dışarı aktarır.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>17 Şubat 2020 (2002 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>MacOS için Microsoft Defender Gelişmiş tehdit koruması (ATP) uygulaması<!-- 5424618 -->
Intune, macOS için Microsoft Defender Gelişmiş tehdit koruması (ATP) uygulamasını yönetilen Mac cihazlarına dağıtmanın kolay bir yolunu sunar. Daha fazla bilgi için bkz. [Mac için Microsoft Intune ve Microsoft Defender Gelişmiş tehdit koruması](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) [kullanarak MacOS CIHAZLARıNA Microsoft Defender ATP ekleme](../apps/apps-advanced-threat-protection-macos.md) .  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>İOS cihazlarında Cisco AnyConnect VPN ile ağ erişim denetimi 'ni (NAC) etkinleştirme<!-- 4860111  -->
İOS cihazlarında, bir VPN profili oluşturabilir ve Cisco AnyConnect (**cihaz yapılandırma** > **profilleri** >  > farklı bağlantı türleri kullanabilirsiniz. Örneğin, bağlantı türü için **Cisco AnyConnect** **> profil** türü için **iOS** > **VPN** platformu.

Cisco AnyConnect ile ağ erişim denetimi 'ni (NAC) etkinleştirebilirsiniz. Bu özelliği kullanmak için:

1. [Cisco kimlik hizmetleri altyapısı yönetici kılavuzunda](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html), Azure 'Da Cisco Identity Services altyapısını (ISE) YAPıLANDıRMAK Için **MDM sunucusu olarak Microsoft Intune yapılandırma** bölümündeki adımları kullanın.
2. Intune cihaz yapılandırma profilinde **ağ Access Control etkinleştir (NAC)** ayarını seçin.

Tüm kullanılabilir VPN ayarlarını görmek için [iOS CIHAZLARıNDA VPN ayarlarını yapılandırma](../configuration/vpn-settings-ios.md)bölümüne gidin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Apple MDM anında Iletme sertifikası sayfasındaki seri numarası<!--5947765  -->
Apple MDM anında Iletme sertifikası sayfasında artık seri numarası görüntülenir. Sertifikayı oluşturan Apple KIMLIĞINE erişim kaybolursa, Apple MDM anında Iletme sertifikasına erişimi yeniden kazanmak için seri numarası gereklidir. Seri numarasını görmek için **cihazlar** > **iOS** > **IOS kaydı** > **Apple MDM anında iletme sertifikası**' na gidin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Kayıtlı iOS/ıpados cihazlarına işletim sistemi güncelleştirmelerini göndermek için yeni güncelleştirme zamanlaması seçenekleri<!--5879689  -->
İOS/ıpados cihazları için işletim sistemi güncelleştirmelerini zamanlarken aşağıdaki seçenekler arasından seçim yapabilirsiniz. Bu seçenekler, Apple Business Manager veya Apple Okul Yöneticisi kayıt türlerini kullanan cihazlar için geçerlidir.
- Sonraki iadede Güncelleştir
- Zamanlanan süre içinde güncelleştirme
- Zamanlanan sürenin dışında güncelleştirme

İkinci iki seçenek için birden çok zaman penceresi oluşturabilirsiniz.

Yeni seçenekleri görmek **için > iOS** **/ıpados** > **Profil oluştur** > **iOS** > güncelleştirme ilkeleri ' ne gidin.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Kayıtlı cihazlara hangi iOS/ıpados güncelleştirmelerinin göndermek istediğinizi seçin<!--5879689  -->
Apple Business Manager veya Apple Okul Yöneticisi kullanılarak kaydedilmiş cihazlara gönderim yapmak için belirli bir iOS/ıpados Güncelleştirmesi (en son güncelleştirme dışında) seçebilirsiniz. Bu tür cihazlarda, yazılım güncelleştirme görünürlüğünü birkaç gün boyunca geciktirmek için bir cihaz yapılandırma ilkesi ayarlanmış olmalıdır. Bu özelliği görmek **için > iOS** **/ıpados** > **Profil oluştur** > **iOS** > güncelleştirme ilkeleri ' ne gidin.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="improved-intune-reporting-experience---3791418-----"></a>İyileştirilmiş Intune raporlama deneyimi<!-- 3791418   -->
Intune artık yeni rapor türleri, daha iyi rapor organizasyonu, daha odaklanmış görünümler, geliştirilmiş rapor işlevselliği ve daha tutarlı ve zamanında veriler de dahil olmak üzere gelişmiş bir raporlama deneyimi sunmaktadır. Raporlama deneyimi, genel önizlemeden GA 'ye (genel kullanılabilirlik) geçmeyecektir. Ayrıca, GA sürümü, [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'ndeki kutucuklar üzerinde yerelleştirme desteği, hata düzeltmeleri, tasarım iyileştirmeleri ve cihaz uyumluluk verileri toplama sağlar.

Yeni rapor türleri aşağıdaki bilgilere odaklanmaktadır:

- **İşletimsel** -negatif bir sistem durumu odaklı yeni kayıtlar sağlar. 
- **Kuruluş** -genel durumun daha geniş bir özetini sağlar.
- **Geçmiş** -bir süre boyunca desenler ve eğilimler sağlar.
- **Uzman** -kendi özel raporlarınızı oluşturmak için ham verileri kullanmanıza olanak sağlar.

Yeni raporların ilk kümesi cihaz uyumluluğuna odaklanır. Daha fazla bilgi için bkz. [blog-Microsoft Intune raporlama çerçevesi](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) ve [Intune raporları](reports.md).

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Kullanıcı arabirimindeki güvenlik temellerinin konumu birleştirildi<!-- 6177074   -->
Çeşitli kullanıcı arabirimi konumlarından *güvenlik temellerini* kaldırarak Microsoft Endpoint Manager Yönetim merkezinde [güvenlik temellerini](../protect/security-baselines.md) bulmak için yolları birleştiriyoruz. Güvenlik temellerini bulmak için artık şu yolu kullanacaksınız: **Endpoint security** > **Security temelleri**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>İçeri aktarılan PKCS sertifikaları için genişletilmiş destek<!-- 6044197  -->
*Android kurumsal tam olarak yönetilen cihazları*desteklemek için [içeri aktarılan PKCS sertifikalarını](../protect/certificates-imported-pfx-configure.md#supported-platforms) kullanma desteğini genişlettik. Genellikle, PFX sertifikalarını içeri aktarma işlemi, e-posta şifrenin gerçekleşebilmesi için bir kullanıcının tüm cihazlarında gerekli olduğu S/MIME şifreleme senaryolarında kullanılır.

Aşağıdaki platformlar PFX sertifikalarının içeri aktarımını destekler:

- Android-Cihaz Yöneticisi
- Android kurumsal-tam yönetilen
- Android kurumsal Iş profili
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Cihazlar için uç nokta güvenlik yapılandırmasını görüntüleme<!-- 6206460  -->
[Belirli bir cihaza uygulanan Endpoint Security yapılandırmalarının](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)görüntülenmesi Için Microsoft Endpoint Manager Yönetim Merkezi ' nde seçeneğin adını güncelleştirdik. Bu seçenek, uygun güvenlik temellerini ve güvenlik temelleri dışında oluşturulan ek ilkeleri gösterdiği için **uç nokta güvenlik yapılandırması** olarak yeniden adlandırılır. Daha önce Bu seçenek *güvenlik temelleri*olarak adlandırılmıştı.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Intune rolleri Kullanıcı arabirimi değişiklikleri geliyor<!--5801612   -->
[Microsoft Endpoint Manager yönetim merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) > **Kiracı Yönetimi** > **rolleri** için Kullanıcı arabirimi, daha kolay ve sezgisel bir tasarıma geliştirilmiştir. Bu deneyim, şimdi kullandığınız ayarların ve ayrıntıların aynısını sağlar, ancak yeni deneyim sihirbaz benzeri bir işlem kullanır.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>17 Şubat 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="microsofts-new-office-app---5859926---"></a>Microsoft 'un yeni Office uygulaması<!-- 5859926 -->
Microsoft 'un yeni Office uygulaması artık indirme ve kullanım için genel kullanıma sunulmuştur. Office uygulaması, kullanıcılarınızın tek bir uygulama içinde Word, Excel ve PowerPoint 'te çalışabilecekleri birleştirilmiş bir deneyimdir. Erişilmekte olan verilerin korunduğundan emin olmak için uygulamayı bir uygulama koruma ilkesiyle hedefleyebilirsiniz.

Daha fazla bilgi için bkz. [Office mobil önizleme uygulamasıyla Intune uygulama koruma ilkelerini etkinleştirme](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>10 Şubat 2020 haftası

### <a name="windows-7-ends-extended-support--3042987---"></a>Windows 7 genişletilmiş desteği sonlandırır<!--3042987 -->
Windows 7, 14 Ocak 2020 ' de Genişletilmiş desteğin sonuna ulaştı. Intune, Windows 7 çalıştıran cihazlar için aynı anda kullanım dışı desteği. BILGISAYARıNıZı korumaya yardımcı olan teknik yardım ve otomatik güncelleştirmeler artık kullanılamaz. Windows 10 ' a yükseltmeniz gerekir. Daha fazla bilgi için bkz. [değişiklik için blog gönderisi planı](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Windows 10 cihazlarda Microsoft Edge sürüm 77 ve üzeri<!-- 5843584 -->
Intune artık Windows 10 cihazlarda Microsoft Edge sürüm 77 ve üstünü kaldırmayı desteklemektedir. Daha fazla bilgi için bkz. [Windows 10 Için Microsoft Edge 'i Microsoft Intune 'e ekleme](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>Şirket Portalı, Android iş profili kaydından kaldırılan ekran<!--6103987 -->
**Sonraki nedir?** ekranı, Kullanıcı deneyimini kolaylaştırmak Için Şirket portalı Android iş profili kayıt akışından kaldırılmıştır. Güncelleştirilmiş Android iş profili kayıt akışını görmek için [Android iş profiline kaydol](../user-help/enroll-device-android-work-profile.md) ' a gidin.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Şirket Portalı Uygulama performansı geliştirildi<!-- 6178652 -->
Şirket Portalı uygulaması, Surface Pro X gibi ARM64 işlemciler kullanan cihazlar için iyileştirilmiş performansı destekleyecek şekilde güncelleştirilmiştir. daha önce, öykünülmüş bir ARM32 modunda çalıştırılan Şirket Portalı. Artık sürüm 10.4.7080.0 ve üzeri sürümlerde Şirket Portalı uygulaması, ARM64 için yerel olarak derlenir. Şirket Portalı uygulaması hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>27 Ocak 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>MacOS için ek Microsoft Edge sürüm 77 dağıtım kanalı için Intune desteği<!-- 5983950  -->
Microsoft Intune artık macOS için Microsoft Edge uygulaması için ek **kararlı** dağıtım kanalını desteklemektedir. **Kararlı** kanal, kurumsal ortamlarda Microsoft Edge 'i büyük ölçüde dağıtmak için önerilen kanaldır. Her altı haftada bir güncelleştirilir, her sürüm **Beta** kanalından geliştirmeler içerir. Intune, **kararlı** ve **Beta** kanallara ek olarak bir **geliştirme** kanalını da destekler. Genel Önizleme, macOS için Microsoft Edge sürüm 77 ve üzeri için kararlı ve geliştirme kanalları sunar. Tarayıcının otomatik güncelleştirmeleri varsayılan olarak açık. Daha fazla bilgi için bkz. [Microsoft Intune kullanarak macOS cihazları Için Microsoft Edge ekleme](../apps/apps-edge-macos.md).

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>Intune Managed Browser emekli<!--5728447 -->
Intune Managed Browser kullanımdan kaldırılacak. Korumalı Intune tarayıcı deneyiminiz için Microsoft Edge kullanın. Daha fazla bilgi için aşağıdaki [Bildirimler](whats-new.md#notices) bölümünde bulunan '[Işlem yap: korumalı Intune tarayıcı deneyiminiz için Microsoft Edge 'i kullanma](whats-new.md#take-action-use-microsoft-edge-for-your-protected-intune-browser-experience)"girdisine bakın.

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>20 Ocak 2020 (2001 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>Intune 'a uygulama eklenirken Kullanıcı deneyimi değişikliği<!-- 4705829   -->
Intune aracılığıyla uygulamasına uygulama eklerken yeni bir kullanıcı deneyimi görürsünüz. Bu deneyim, daha önce kullandığınız ayarların ve ayrıntıların aynısını sağlar ancak yeni deneyim, bir uygulamayı Intune 'a eklemeden önce sihirbaza benzer bir işlem izler. Bu yeni deneyim, uygulamayı eklemeden önce bir gözden geçirme sayfası da sağlar. [Microsoft Uç Nokta Yöneticisi Yönetim merkezinden](https://go.microsoft.com/fwlink/?linkid=2109431), **uygulamalar** > **tüm uygulamalar** > **Ekle**' yi seçin. Daha fazla bilgi için bkz. [Microsoft Intune’a uygulama ekleme](../apps/apps-add.md).

#### <a name="require-win32-apps-to-restart----5622282-----"></a>Win32 uygulamalarının yeniden başlatılmasını gerektir <!-- 5622282   -->
Başarılı bir yüklemeden sonra bir Win32 uygulamasının yeniden başlatılmasını zorunlu kılabilirsiniz. Ayrıca, yeniden başlatmanın gerçekleşmesi için gereken süreyi (yetkisiz kullanım süresi) seçebilirsiniz.

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>Intune 'da uygulama yapılandırılırken Kullanıcı deneyimi değişikliği<!-- 4207990   -->
Intune 'da uygulama yapılandırma ilkeleri oluştururken yeni bir kullanıcı deneyimi görürsünüz. Bu deneyim, daha önce kullandığınız ayarların ve ayrıntıların aynısını sağlar ancak yeni deneyim, Intune 'a ilke eklemeden önce sihirbaza benzer bir işlem izler. [Microsoft Uç Nokta Yöneticisi Yönetim merkezinden](https://go.microsoft.com/fwlink/?linkid=2109431), **uygulama yapılandırma Ilkeleri** ** >  > ** **Ekle**' yi seçin. Daha fazla bilgi için bkz. [Microsoft Intune Için uygulama yapılandırma ilkeleri](../apps/app-configuration-policies-overview.md). 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>Windows 10 için ek Microsoft Edge dağıtım kanalı için Intune desteği<!-- 5861774 -->
Microsoft Intune artık Windows 10 uygulaması için Microsoft Edge (sürüm 77 ve üzeri) için ek **kararlı** dağıtım kanalını desteklemektedir. **Kararlı** kanal, kurumsal ortamlarda Windows 10 Için Microsoft Edge 'i dağıtmak için önerilen kanaldır. Bu kanal her altı haftada bir güncelleştirilir, her sürüm **Beta** kanalından geliştirmeler içerir. Intune, **kararlı** ve **Beta** kanallara ek olarak bir **geliştirme** kanalını da destekler. Daha fazla bilgi için bkz. [Windows 10 Için Microsoft Edge-uygulama ayarlarını yapılandırma](../apps/apps-windows-edge.md#configure-app-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>Exchange ActiveSync şirket içi bağlayıcı kullanıcı arabirimini yapılandırırken geliştirilmiş Kullanıcı arabirimi deneyimi<!-- 5695492   -->
[Exchange ActiveSync şirket içi bağlayıcısını yapılandırma](../protect/exchange-connector-install.md)deneyimini güncelleştirdik. Güncelleştirilmiş deneyim, şirket içi bağlayıcılarınızın ayrıntılarını yapılandırmak, düzenlemek ve özetlemek için tek bir bölme kullanır.

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>Android kurumsal iş profillerine yönelik Wi-Fi profillerine otomatik ara sunucu ayarları ekleme<!-- 4490822   -->
Android kurumsal Iş profili cihazlarında Wi-Fi profilleri oluşturabilirsiniz. Wi-Fi kurumsal türünü seçtiğinizde, Wi-Fi ağınızda kullanılan Genişletilebilir Kimlik Doğrulama Protokolü (EAP) türünü de girebilirsiniz.

Artık kuruluş türünü seçtiğinizde, `proxy.contoso.com`gibi bir proxy sunucu URL 'SI de dahil olmak üzere otomatik proxy ayarlarını da girebilirsiniz.

Yapılandırabileceğiniz geçerli Wi-Fi ayarlarını görmek için [Microsoft Intune ' de Android Enterprise ve Android bilgi noktası çalıştıran cihazlar Için Wi-Fi ayarları ekle](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only)' ye gidin.

Uygulama alanı:
- Android kurumsal iş profili

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>Android kayıtlarını cihaz üreticisine göre engelle<!--5197392  -->
Cihazın üreticisine bağlı olarak cihazların kaydedilmesini engelleyebilirsiniz. Bu özellik Android Cihaz Yöneticisi ve Android kurumsal iş profili cihazları için geçerlidir. Kayıt kısıtlamalarını görmek için [Microsoft Endpoint Manager yönetim merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) > **cihazlar** > **Kayıt kısıtlamaları**' na gidin.

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>İOS/ıpados oluşturma kayıt türü profili kullanıcı arabirimi geliştirmeleri<!-- 6055005 -->
İOS/ıpados Kullanıcı kaydı için, aynı işlevselliği **korurken kayıt türü seçim işlemini** geliştirmek üzere **kayıt türü profil** **ayarları** Oluştur sayfası kolaylaştırılmıştır. Yeni Kullanıcı arabirimini görmek için [Microsoft Endpoint Manager yönetim merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) > **cihazları** > **IOS** > **ios kaydı** > **kayıt türleri** > profil > ayarları **Oluştur** sayfasına gidin **Settings** . Daha fazla bilgi için bkz. [Intune 'Da Kullanıcı kayıt profili oluşturma](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="new-information-in-device-details---4471759-5604099----"></a>Cihaz ayrıntılarında yeni bilgiler<!-- 4471759 5604099  -->
Aşağıdaki bilgiler artık cihazlar için **genel bakış** sayfasıdır:
- Bellek kapasitesi (cihazdaki fiziksel bellek miktarı)
- Depolama kapasitesi (cihazdaki fiziksel depolama miktarı) 
- CPU mimarisi

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>iOS bypass Etkinleştirme Kilidi uzak eylem devre dışı olarak yeniden adlandırıldı Etkinleştirme Kilidi <!--5904591  -->
Uzak eylem **atlama Etkinleştirme Kilidi** , **Etkinleştirme Kilidi devre dışı bırakılacak**şekilde yeniden adlandırıldı. Daha fazla bilgi için bkz. [Intune Ile iOS etkinleştirme kilidi devre dışı bırakma](../remote-actions/device-activation-lock-disable.md).

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>Autopilot cihazlar için Windows 10 özellik güncelleştirme dağıtım desteği<!-- 5948137   -->
Intune artık [Windows 10 özellik güncelleştirme dağıtımlarını](../protect/windows-update-for-business-configure.md#windows-10-feature-updates)kullanarak Autopilot kayıtlı cihazların hedeflenmesini desteklemektedir.

Windows 10 özellik güncelleştirme ilkeleri, Autopilot Out deneyimi (OOBE) sırasında uygulanamıyor ve yalnızca bir cihazın sağlama işlemini tamamladıktan (genellikle bir gün) sonra ilk Windows Update taramaya uygulanır.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Windows Autopilot dağıtım raporları (Önizleme) <!-- 3856172   -->
Yeni bir rapor, Windows Autopilot aracılığıyla dağıtılan her bir cihazın ayrıntılarına sahiptir. Daha fazla bilgi için bkz. [Autopilot Deployment Report](../enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>Yeni Intune yerleşik rol uç noktası Güvenlik Yöneticisi<!--4253397   -->
Yeni bir Intune yerleşik rolü kullanılabilir: Endpoint Security Manager. Bu yeni rol, yöneticilere Intune 'daki Endpoint Manager düğümüne tam erişim ve diğer alanlara yalnızca erişim izni verir. Rol, Azure AD 'den "Güvenlik Yöneticisi" rolünün bir genişletmesinden oluşur. Şu anda yalnızca rol olarak genel yöneticileriniz varsa, hiçbir değişiklik yapmanız gerekmez. Rolleri kullanıyorsanız ve Endpoint Security Manager 'ın sağladığı ayrıntı düzeyini beğenmezseniz, bu rolü kullanılabilir olduğunda atayın. Yerleşik roller hakkında daha fazla bilgi için bkz. [rol tabanlı erişim denetimi](role-based-access-control.md).

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>6 Ocak 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>İOS için Microsoft Outlook için S/MIME desteği<!-- 2669398 -->
Intune, iOS cihazlarda iOS için Outlook ile kullanılabilen S/MIME imzalama ve şifreleme sertifikalarının teslim edilmesini destekler. Daha fazla bilgi için bkz. [iOS ve Android Için Outlook 'Ta duyarlılık etiketleme ve koruma](https://aka.ms/omsmime).

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>Microsoft bağlı önbellek sunucusunu kullanarak Win32 uygulama içeriğini önbelleğe alma<!-- 6030314 -->
Intune Win32 uygulama içeriğini önbelleğe almak için, Configuration Manager dağıtım noktalarınıza Microsoft bağlı önbellek sunucusu yükleyebilirsiniz. Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği Configuration Manager-Intune Win32 uygulamaları Için destek](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Windows 10 Yönetim Şablonları (ADMX) profilleri artık kapsam etiketlerini destekliyor <!--5137390 -->
Artık, yönetim şablonu profillerine (ADMX) kapsam etiketleri atayabilirsiniz. Bunu yapmak için **ıntune** > **cihazlar** > **yapılandırma profilleri** ' ne gidin > Liste > **Özellikler** > **kapsam etiketleri**' nde bir Yönetim Şablonları profili seçin. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [diğer nesnelere kapsam etiketleri atama](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>30 Aralık 2019 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>MEM şifreli macOS cihazlarından kişisel kurtarma anahtarını alma<!-- 4851745 -->
Son kullanıcılar, iOS Şirket Portalı uygulamasını kullanarak kişisel kurtarma anahtarını (Filekasası anahtarı) alabilir. Kişisel kurtarma anahtarına sahip olan cihaz Intune 'a kaydolmalıdır ve Intune aracılığıyla Filekasasıyla şifrelenir. İOS Şirket Portalı uygulamasını kullanarak, bir son kullanıcı, **Kurtarma anahtarını al**' a tıklayarak kişisel kurtarma anahtarını şifreli MacOS cihazında alabilir. Kurtarma anahtarını, *şifreli ve kayıtlı macOS cihazı* ** >  > ** **Kurtarma anahtarı al**' a seçerek de Intune 'dan alabilirsiniz. Filekasası hakkında daha fazla bilgi için bkz. [macOS Için dosya Kasası şifrelemesi](../protect/encrypt-devices.md#filevault-encryption-for-macos).

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>iOS ve ıpados Kullanıcı lisanslı VPP uygulamaları<!-- 5619268 -->
Kullanıcı tarafından kaydedilen iOS ve ıpados cihazlarında, son kullanıcılar artık kullanılabilir olarak dağıtılan yeni oluşturulan cihaz lisanslı VPP uygulamalarıyla birlikte sunulmayacaktır. Ancak, son kullanıcılar Şirket Portalı içinde Kullanıcı lisanslı tüm VPP uygulamalarını görmeye devam eder. VPP uygulamaları hakkında daha fazla bilgi için bkz. [Microsoft Intune ile Apple Volume Purchase program aracılığıyla satın alınan iOS ve macOS uygulamalarını yönetme](../apps/vpp-apps-ios.md).

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>23 Aralık 2019 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>Uyarı-Windows 10 1703 (RS2) destek dışında hareket edecek <!-- 5026679 -->
9 Ekim 2018 ' den itibaren, Windows 10 1703 (RS2), Iş Istasyonları için Home, Pro ve Pro sürümleri için Microsoft platformu desteği dışına taşındı. Windows 10 Enterprise ve eğitim sürümlerinde, Windows 10 1703 (RS2) 8 Ekim 2019 ' de platform desteği dışına taşındı. 26 Aralık 2019 ' den itibaren, Windows Şirket Portalı uygulamasının en düşük sürümünü Windows 10 1709 (RS3) olarak güncelleştiriyoruz. 1709 ' den önceki sürümleri çalıştıran bilgisayarlar artık Microsoft Store uygulama için güncelleştirilmiş sürümleri almamayacaktır. Daha önce bu değişikliği ileti merkezi aracılığıyla Windows 10 ' un eski sürümlerini yöneten müşterilere ilettik. Daha fazla bilgi için bkz. [Windows yaşam döngüsü olgu sayfası](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>16 Aralık 2019 haftası

### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Windows 10 cihazları için Yönetim Şablonları güncelleştirmeleri <!-- 5941568 -->

Microsoft Edge, Office ve Windows ayarlarını denetlemek ve yönetmek için Microsoft Intune 'de ADMX şablonlarını kullanabilirsiniz. Intune 'da Yönetim Şablonları aşağıdaki ilke ayarı güncelleştirmelerini yaptı:

- Microsoft Edge sürümleri 78 ve 79 için destek eklendi.
- [Yönetim şablonu dosyalarında (ADMX/ADML) 11 kasım 2019 ADMX dosyalarını ve office 365 ProPlus, office 2019 ve office 2016 Için Office Özelleştirme Aracı](https://www.microsoft.com/download/details.aspx?id=49030)'nı içerir.

Intune 'da ADMX şablonları hakkında daha fazla bilgi için, bkz. [Microsoft Intune Grup İlkesi ayarlarını yapılandırmak Için Windows 10 şablonlarını kullanma](../configuration/administrative-templates-windows.md).

Uygulama alanı:

- Windows 10 ve üzeri

## <a name="week-of-december-9-2019-1912-service-release"></a>9 Aralık 2019 (1912 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>Yönetilen gözatma senaryolarında Microsoft Edge 'e geçiş<!-- 5173762 -->
Intune Managed Browser emekliliğe yaklaşarak, kullanıcılarınızı uçtan uca taşımak için gereken adımları basitleştirmek amacıyla uygulama koruma ilkelerinde değişiklikler yaptık. Uygulama koruma ilkesi ayarı, **diğer uygulamalarla Web içeriği aktarımını kısıtla** seçeneklerini, aşağıdakilerden biri olacak şekilde güncelleştirdik:

- Herhangi bir uygulama
- Intune Yönetilen Tarayıcı
- Microsoft Edge
- Yönetilmeyen tarayıcı 

**Microsoft Edge**' i seçtiğinizde, son kullanıcılarınız Microsoft Edge 'in yönetilen gözatma senaryolarında gerekli olduğunu bildiren koşullu erişim mesajlaşmasını görür. Henüz yapmadıysanız, bu kullanıcıların AAD hesaplarıyla Microsoft Edge 'i indirip oturum açması istenir.  Bu, MAM özellikli uygulamalarınızı, uygulama yapılandırma ayarıyla `com.microsoft.intune.useEdge` **true**olarak ayarlanmış şekilde hedefleyen bir değer olacaktır. **İlke ile yönetilen tarayıcılar** ayarının kullanıldığı mevcut uygulama koruma ilkeleri artık **Intune Managed Browser** seçili olacak ve davranışta hiçbir değişiklik görmez. Bu, **useedge** uygulama yapılandırma ayarını **doğru**olarak ayarladıysanız kullanıcılarınızın Microsoft Edge 'i kullanmak için mesajlaşma göreceği anlamına gelir. Yönetilen gözatma senaryolarından yararlanan tüm müşterilerin, Microsoft Edge 'e geçiş yapmak için uygun Kılavuzu görmesini sağlamak üzere, kullanıcıların bağlantıları hangi uygulamadan başlatdıklarından emin olmak için, uygulama koruma ilkelerini **diğer uygulamalarla kısıtla** . 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>Kuruluş hesapları için uygulama bildirim içeriğini yapılandırma<!-- 2576686  -->
Android ve iOS cihazlarında Intune uygulama koruma ilkeleri (uygulama), kuruluş hesapları için uygulama bildirim içeriğini denetlemenize olanak tanır. Seçili uygulama için kuruluş hesaplarına yönelik bildirimlerin nasıl gösterileceğini belirtmek için bir seçenek (Izin ver, kuruluş verilerini engelle veya engellendi) seçeneğini belirleyebilirsiniz. Bu özellik, uygulamalardan destek gerektirir ve UYGULAMANıN etkinleştirildiği tüm uygulamalar için kullanılamayabilir. İOS için Outlook sürüm 4.15.0 (veya üzeri) ve Outlook for Android 4.83.0 (veya üzeri), bu ayarı destekler. Ayar konsolunda mevcuttur, ancak işlevsellik 16 Aralık 2019 ' den sonra devreye girer. UYGULAMA hakkında daha fazla bilgi için bkz. [Uygulama koruma ilkeleri nelerdir?](../apps/app-protection-policy.md).

#### <a name="microsoft-app-icons-update--4677605----"></a>Microsoft uygulama simgeleri güncelleştirmesi<!--4677605  -->
Uygulama koruma ilkeleri ve uygulama yapılandırma ilkeleri için uygulama hedefleme bölmesinde Microsoft uygulamaları için kullanılan simgeler güncelleştirilmiştir.

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>Android üzerinde onaylanan Klavye kullanımını gerektir<!--4761794  -->
Uygulama koruma ilkesinin bir parçası olarak, yönetilen Android uygulamalarıyla hangi Android klavyeleri kullanılabileceğini yönetmek için [**onaylanan klavyeler**](../apps/app-protection-policy-settings-android.md#data-protection) ayarını belirtebilirsiniz. Bir Kullanıcı yönetilen uygulamayı açtığında ve bu uygulama için henüz onaylanmış bir klavye kullanmıyorsa, bu kullanıcılara cihazlarında zaten yüklü olan onaylanmış klavyelerin birine geçiş yapması istenir. Gerekirse, bunlar tarafından yüklenip ayarlanabilecek Google Play Store onaylanan bir klavyeyi indirmek için bir bağlantı sunulur. Kullanıcı, yönetilen bir uygulamadaki metin alanlarını, etkin klavyesi onaylanan klavyelerin biri olmadığında düzenleyebilir.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>İOS, ıpados ve macOS cihazlarınızdaki uygulamalar ve Web siteleri için çoklu oturum açma deneyimi güncelleştirildi<!-- 4999578  -->
Intune, iOS, ıpados ve macOS cihazları için daha fazla çoklu oturum açma (SSO) ayarı ekledi. Artık kuruluşunuz tarafından veya kimlik sağlayıcınız tarafından yazılmış yeniden yönlendirme SSO uygulaması uzantılarını yapılandırabilirsiniz. OAuth ve SAML2 gibi modern kimlik doğrulama yöntemlerini kullanan uygulamalar ve Web siteleri için sorunsuz bir çoklu oturum açma deneyimi yapılandırmak üzere bu ayarları kullanın. 

Bu yeni ayarlar, SSO uygulama uzantıları ve Apple 'ın yerleşik Kerberos uzantısı için önceki ayarlarda (**cihazlar** > **cihaz yapılandırma** > **profillerinin** > profil **oluşturma** > **iOS/ıpados** veya **MacOS** ' u, profil türü için > **cihaz özellikleri** ) genişletir. 

Yapılandırabileceğiniz SSO uygulama uzantısı ayarlarının tam aralığını görmek için, [macOS 'Ta](../configuration/macos-device-features-settings.md#single-sign-on-app-extension)IOS ve SSO ['daki SSO](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) ' ya gidin.

Uygulama alanı:

- iOS/iPadOS
- Mac OS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>İOS ve ıpados cihazları için davranışlarını düzeltmek üzere iki cihaz kısıtlama ayarını güncelleştirdik<!-- 5701352    -->
İOS cihazlarında, **Kablosuz PKI güncelleştirmelerine izin** veren cihaz kısıtlama profilleri OLUŞTURABILIR ve **USB kısıtlı modunu** (**cihazlar** > **cihaz yapılandırma** > **profilleri** için > **profil oluşturma** > **iOS/ıpados** ' ı profil türü için iOS > **cihaz kısıtlamalarına** göre engeller). Bu sürümden önce, aşağıdaki ayarlar için Kullanıcı arabirimi ayarları ve açıklamaları hatalıydı ve artık düzeltildi. Bu sürümden itibaren, ayarlar davranışı aşağıdaki gibidir:

**Kablosuz PKI güncelleştirmelerini engelle**: **blok** , cihazın bir bilgisayara bağlı olmadığı durumlar dışında yazılım güncelleştirmelerini almasını engeller. **Yapılandırılmadı** (varsayılan): bir cihazın bir bilgisayara bağlı olmadan yazılım güncelleştirmelerini almasına izin verir.
- Daha önce, bu ayar, kullanıcılarınızın cihazlarını bir bilgisayara bağlamadan yazılım güncelleştirmeleri almasına Izin veren: **Izin ver**olarak yapılandırmanızı sağlar.
**Cihaz KILITLIYKEN USB donatılara Izin ver**: **ızın ver** , USB aksesuarları 'nin bir saatten daha fazla kilitlenmiş bir cihazla veri alışverişi yapmasına olanak sağlar. **Yapılandırılmamış** (varsayılan), USB kısıtlı modunu cihazda güncelleştirmez ve USB aksesuarları bir saatten daha fazla kilitleniyorsa cihazdan veri aktarımını engellenecektir.
- Bu ayar daha önce bu ayarı olarak yapılandırmanızı sağlar: denetimli cihazlarda USB kısıtlı modunu devre dışı bırakmayı **engeller** .

Yapılandırabileceğiniz ayar hakkında daha fazla bilgi için bkz. [iOS ve ıpados cihaz ayarları Intune kullanarak özellikleri izin vermek veya kısıtlamak için](../configuration/device-restrictions-ios.md).

Bu özellik şu platformlarda geçerlidir:

- OS/ıpados

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>MacOS cihazları için kablolu ağ cihaz yapılandırma profilleri<!-- 3508686  -->
   > [!NOTE]
   > Bu özellik gecikti, ancak yakında yayımlanacak.

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>Kullanıcıların, Android kurumsal cihaz sahibi cihazlarda yönetilen anahtar deposunda sertifika kimlik bilgilerini yapılandırmalarını engelleyin<!-- 3311998 -->
Android kurumsal cihaz sahibi cihazlarda, kullanıcıların yönetilen anahtar deposunda (**cihaz yapılandırma** > **profiller** ** > sertifika** kimlik bilgilerini yapılandırmalarını engelleyen yeni bir ayar yapılandırabilirsiniz. > **Android Enterprise** for platform > cihaz sahibi yalnızca profil türü > **Kullanıcılar + hesaplar**) için **cihaz kısıtlamalarını >** .

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="protected-wipe-action-now-available--51150000---"></a>Korumalı silme eylemi şimdi kullanılabilir<!--51150000 -->
Artık bir cihazın korumalı silme işlemini gerçekleştirmek için cihazı silme eylemini kullanma seçeneğiniz vardır. Korumalı wpes 'ler, standart wpes ile aynıdır, ancak cihaz kapatılanarak bu dosyalar atlatılabilir. Korumalı silme işlemi başarılı olana kadar cihazı sıfırlamaya çalışmaya devam edecektir. Bazı yapılandırmalarda, bu eylem cihazın yeniden başlatılamamasından kalabilir. Daha fazla bilgi için bkz. [cihazları devre dışı bırakma veya silme](../remote-actions/devices-wipe.md).

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>Cihazın genel bakış sayfasına eklenen cihaz Ethernet MAC adresi<!--5562275 -->
Artık cihaz ayrıntıları sayfasında bir cihazın Ethernet MAC adresini görebilirsiniz (**cihazlar > aygıtlar** > bir cihaz seçin **All devices** > **genel bakış**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>Cihaz tabanlı koşullu erişim ilkeleri etkinleştirildiğinde paylaşılan bir cihazda geliştirilmiş deneyim<!-- 1734096  -->
İlke zorlarken Kullanıcı için en son uyumluluk değerlendirmesini denetleyerek, cihaz tabanlı koşullu erişim ilkesiyle hedeflenen birden fazla kullanıcıyla paylaşılan bir cihazda deneyim geliştirdik. Daha fazla bilgi için aşağıdaki genel bakış makalelerine bakın:
- [Koşullu erişim için Azure genel bakış](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Intune cihaz uyumluluğuna genel bakış](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>Sertifikalar ile cihaz sağlamak için PKCS sertifika profillerini kullanma<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
Artık, Wi-Fi ve VPN için olanlar gibi profillerle ilişkilendirildiğinde Android for Work, iOS/ıpados ve Windows çalıştıran *cihazlara* sertifika vermek için PKCS sertifika profillerini kullanabilirsiniz. Daha önce bu üç platform yalnızca Kullanıcı tabanlı sertifikaları desteklemekte ve cihaz tabanlı destek, macOS ile sınırlandırılmıştır.

> [!NOTE]
> PKCS sertifika profilleri, Wi-Fi profilleriyle desteklenmez. Bunun yerine, bir [EAP türü](../configuration/wi-fi-settings-windows.md#enterprise-profile)kullandığınızda SCEP sertifika profillerini kullanın.

Cihaz tabanlı bir sertifika kullanmak için, desteklenen platformlar için [PKCS sertifika profili oluştururken](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) **Ayarlar**' ı seçin. Artık, cihaz veya Kullanıcı seçeneklerini destekleyen **sertifika türü**ayarını görürsünüz.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="centralized-audit-logs--5603185-5697164---"></a>Merkezi denetim günlükleri<!--5603185, 5697164 -->
Yeni bir merkezi denetim günlüğü deneyimi artık tüm kategoriler için Denetim günlüklerini tek bir sayfada toplar. Aradığınız verileri almak için günlüklere filtre uygulayabilirsiniz. Denetim günlüklerini görmek için, **kiracı yönetimi** > **Denetim günlükleri**' ne gidin. 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>Denetim günlüğü etkinlik ayrıntılarına dahil edilen kapsam etiketi bilgileri<!--5763534 -->
Denetim günlüğü etkinlik ayrıntıları artık kapsam etiketi bilgilerini içerir (kapsam etiketlerini destekleyen Intune nesneleri için). Denetim günlükleri hakkında daha fazla bilgi için bkz. [olayları izlemek ve izlemek için Denetim günlüklerini kullanma](monitor-audit-logs.md).

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>2 Aralık 2019 haftası

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>Yeni Microsoft uç noktası Configuration Manager ortak yönetim lisansı<!--5027281-->
Yazılım Güvencesi kapsamındaki Configuration Manager müşteriler, ortak yönetim için ek bir Intune lisansı satın almak zorunda kalmadan Windows 10 bilgisayarları için Intune ortak yönetimini alabilir. Müşteriler, Windows 10 ' un ortak yönetimi için son kullanıcılarına ayrı Intune/EMS lisansları atamaya gerek kalmaz.
- Configuration Manager tarafından yönetilen ve ortak yönetime kaydedilen cihazlar, Intune tek başına MDM ile yönetilen bilgisayarlar ile neredeyse aynı haklara sahiptir. Ancak, sıfırlandıktan sonra Autopilot kullanılarak yeniden sağlanamazlar.
- Diğer yollarla Intune 'a kayıtlı Windows 10 cihazları tam Intune lisansları gerektirir.
- Diğer platformlardaki cihazlarda hala tam Intune lisansları gerekir.

Daha fazla bilgi için bkz. [Lisans koşulları](https://www.microsoft.com/en-us/Licensing/product-licensing/products).

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>18 Kasım 2019 (1911 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>Uygulama verilerini seçmeli olarak silme sırasında kullanıcı arabirimi güncelleştirmesi<!-- 4102028 -->
Intune 'da uygulama verilerini seçmeli olarak silme Kullanıcı arabirimi güncelleştirilmiştir. UI değişiklikleri şunları içerir:
- Bir bölme içinde bir sihirbaz stili biçim kullanarak basitleştirilmiş bir deneyim.
- Atamaları eklemek için akış oluşturma için bir güncelleştirme.
- Yeni bir ilke oluşturmadan veya bir özellik düzenlenirken önce özellikleri görüntülerken ayarlanan tüm öğelerin özetlenen sayfası. Ayrıca, Özellikler düzenlenirken, Özet yalnızca düzenlenmekte olan özellikler kategorisinden öğe listesini gösterir.

Daha fazla bilgi için bkz. [Intune tarafından yönetilen uygulamalardan kurumsal verileri temizleme](../apps/apps-selective-wipe.md).

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>iOS ve ıpados üçüncü taraf klavye desteği<!-- 4922950 -->
Mart 2019 ' de, "üçüncü taraf klavyeleri" iOS uygulama koruma ilkesi ayarı için desteğin kaldırılmasını duyurduk. Bu özellik hem iOS hem de ıpados desteğiyle Intune 'a döndürülüyor. Bu ayarı etkinleştirmek için, yeni veya mevcut bir iOS/ıpados uygulama koruma ilkesinin **veri koruma** sekmesini ziyaret edin ve **veri aktarımı**altında **üçüncü taraf klavyeler** ayarını bulun.

Bu ilke ayarının davranışı, önceki uygulamadan biraz farklılık gösterir. SDK sürüm 12.0.16 ve üstünü kullanan çoklu kimlik uygulamalarında, bu ayar **engellenecek**şekilde yapılandırılmış olan uygulama koruma ilkeleri tarafından hedeflenirse son kullanıcılar hem kuruluşlarındaki hem de kişisel hesaplarında üçüncü taraf klavyeleri kabul etmeyecektir. SDK 12.0.12 ve önceki sürümlerini kullanan uygulamalar, blog gönderdiğimiz başlığında belgelenen davranışı göstermeye devam edecektir, [bilinen sorun: üçüncü taraf klavyeleri, kişisel hesaplar Için iOS 'ta engellenmiyor](https://aka.ms/3rdparty_iOS_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>JAMF yönetimini gerektirecek macOS Kullanıcı gruplarını hedefleme<!-- 4061739  --> 
[JAMF tarafından yönetilen MacOS cihazlarını](../protect/conditional-access-integrate-jamf.md)alacak belirli kullanıcı gruplarını hedefleyebilirsiniz. Bu hedefleme, diğer cihazlar Intune tarafından yönetilirken, bir macOS cihazları alt kümesine JAMF uyumluluk tümleştirmesini uygulamanıza olanak sağlar. JAMF tümleştirmesini zaten kullanıyorsanız, tüm kullanıcılar tümleştirme için varsayılan olarak hedeflenmeyecektir.

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>İOS cihazlarında e-posta cihaz yapılandırma profili oluştururken yeni Exchange ActiveSync ayarları<!-- 4892824   --> 
İOS/ıpados cihazlarında, bir cihaz yapılandırma profilinde e-posta bağlantısını yapılandırabilirsiniz (**cihaz yapılandırma** > **profilleri** > profil **oluşturmak** > için **IOS/ıpados** > profil türü **e-postası** ). 

Aşağıdakiler dahil olmak üzere kullanılabilir yeni Exchange ActiveSync ayarları vardır:
- **Eşitlenecek Exchange verileri**: Takvim, kişiler, anımsatıcılar, notlar ve e-posta Için eşitlenecek Exchange hizmetlerini seçin (veya eşitlemeyi engelleyin).
- **Kullanıcıların eşitleme ayarlarını değiştirmesine Izin ver**: kullanıcıların cihazlarında bu hizmetler için eşitleme ayarlarını değiştirmesine izin ver (veya engelle).  

Bu ayarlar hakkında daha fazla bilgi için, [Intune 'Da iOS cihazları Için e-posta profili ayarları](../configuration/email-settings-ios.md)' na gidin. 

Uygulama alanı:

- iOS 13,0 ve üzeri
- ıpados 13,0 ve üzeri

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>Kullanıcıların Android kurumsal tam olarak yönetilen ve adanmış cihazlara kişisel Google hesapları eklemesini engelleyin<!-- 5353228   -->
Android kurumsal tam olarak yönetilen ve ayrılmış cihazlarda, kullanıcıların kişisel Google **hesapları > ** **oluşturmalarına** engel olan yeni bir ayar vardır (**cihaz yapılandırma** > **profilleri** > bir cihaz sahibi > yalnızca **Kullanıcı ve hesap ayarları** > **kişisel Google hesapları**) için **cihaz kısıtlamaları** >. > 

Yapılandırabileceğiniz ayarları görmek için [Android kurumsal cihaz ayarları ' na giderek Intune kullanarak özelliklere izin verin veya kısıtlayın](../configuration/device-restrictions-android-for-work.md).

Uygulama alanı:

- Android kurumsal tam yönetilen cihazlar
- Android kurumsal adanmış cihazlar

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>Siri komutları ayarı için sunucu tarafı günlüğü, iOS/ıpados cihaz kısıtlamaları profilinde kaldırılır <!-- 5468501   -->
İOS ve ıpados cihazlarında, **Siri Için sunucu tarafı günlük kaydı** , Microsoft Endpoint Manager Yönetici konsolundan (**cihaz yapılandırma** > **profilleri** > profil **oluşturma** > **iOS/ıpados** > **cihaz kısıtlamaları** > **yerleşik uygulamalar**) kaldırılır. 

Bu ayarın cihazlar üzerinde hiçbir etkisi yoktur. Bu ayarı mevcut profillerden kaldırmak için, profili açın, tüm değişiklikleri yapın ve ardından profili kaydedin. Profil güncelleştirilir ve ayar cihazlardan silinir.

Yapılandırabileceğiniz tüm ayarları görmek için [iOS ve ıpados cihaz ayarları ' na bakın ve Intune kullanarak özelliklere izin verin veya kısıtlayın](../configuration/device-restrictions-ios.md).

Uygulama alanı:

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Windows 10 özellik güncelleştirmeleri (Genel Önizleme)<!-- 2384877 -->
Windows 10 [özellik güncelleştirmelerini](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) artık Windows 10 cihazlara dağıtabilirsiniz. Windows 10 özellik güncelleştirmeleri, cihazların yüklenmesini ve devam etmek istediğiniz Windows 10 sürümünü ayarlayan yeni bir yazılım güncelleştirme ilkesidir. Bu yeni ilke türünü, mevcut Windows 10 güncelleştirme halkalarınızla birlikte kullanabilirsiniz.

Windows 10 özellik güncelleştirmeleri ilkesini alan cihazlar Windows 'un belirtilen sürümünü yükler ve ardından ilke düzenlenene veya kaldırılana kadar o sürümde kalır. Windows 'un daha sonraki bir sürümünü çalıştıran cihazlar güncel sürümlerinde kalır. Windows 'un belirli bir sürümünde tutulan cihazlar, Windows 10 güncelleştirme halkalarından bu sürüm için kalite ve güvenlik güncelleştirmeleri yüklemeye devam edebilir.

Bu yeni ilke türü bu hafta kiracılar için kullanıma sunulmaya başlar. Bu ilke henüz kiracınızda yoksa, yakında olacaktır.

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>MacOS uygulamaları için plist dosyalarında anahtar bilgilerini ekleme ve değiştirme<!-- 4736278 -->
MacOS cihazlarında artık, bir uygulamayla veya cihazla ilişkili bir özellik listesi**dosyasını (.** plist) karşıya yükleyen bir cihaz yapılandırma profili oluşturabilirsiniz (Platform > için SDK > **yapılandırma profilleri** > profil **oluşturma** > **MacOS** profil türü için bir **tercih dosyası** ).

Yalnızca bazı uygulamalar yönetilen tercihleri destekler ve bu uygulamalar tüm ayarları yönetmenize izin vermiyor. Kullanıcı kanalı ayarlarını değil cihaz kanalı ayarlarını yapılandıran bir özellik listesi dosyasını karşıya yüklediğinizden emin olun.

Bu özellik hakkında daha fazla bilgi için, bkz. [Microsoft Intune kullanarak macOS cihazlarına özellik listesi dosyası ekleme](../configuration/preference-file-settings-macos.md).

Uygulama alanı:

- 10,7 ve daha yeni çalıştıran macOS cihazları

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>Autopilot cihazlar için cihaz adı değerini Düzenle<!-- 2640074 -->
Azure AD 'ye katılmış Autopilot cihazları için cihaz adı değerini düzenleyebilirsiniz.  Daha fazla bilgi için bkz. [Autopilot cihaz özniteliklerini düzenleme](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>Autopilot cihazlar için Grup etiketi değerini Düzenle<!-- 4816775   -->
Autopilot cihazlar için Grup etiketi değerini düzenleyebilirsiniz. Daha fazla bilgi için bkz. [Autopilot cihaz özniteliklerini düzenleme](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="updated-support-experience---5012398---"></a>Güncelleştirilmiş destek deneyimi<!-- 5012398 -->

Bugünden itibaren, [Intune 'a yönelik yardım ve destek almak](get-support.md) için güncelleştirilmiş ve kolaylaştırılmış bir konsol deneyimi kiracılara gönderilir. Henüz bu yeni deneyim yoksa, yakında sunulacaktır.

Genel sorunlar ve destek ile iletişim kurmak için kullandığınız iş akışı için konsol içi arama ve geri bildirim geliştirdik. Bir destek sorunu açarken, bir geri çağırma veya e-posta yanıtı beklendiğinde gerçek zamanlı tahminleri görürsünüz ve Premier ve Birleşik destek müşterileri, daha hızlı destek almaya yardımcı olmak için kendi sorunları için kolayca önem derecesi belirtebilir.

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>İyileştirilmiş Intune raporlama deneyimi (Genel Önizleme) <!-- 3791418 -->
Intune artık yeni rapor türleri, daha iyi rapor organizasyonu, daha odaklanmış görünümler, geliştirilmiş rapor işlevselliği ve daha tutarlı ve zamanında veriler de dahil olmak üzere gelişmiş bir raporlama deneyimi sunmaktadır. Yeni rapor türleri aşağıdakilere odaklanılmıştır:

- **İşletimsel** -negatif bir sistem durumu odaklı yeni kayıtlar sağlar. 
- **Kuruluş** -genel durumun daha geniş bir özetini sağlar.
- **Geçmiş** -bir süre boyunca desenler ve eğilimler sağlar.
- **Uzman** -kendi özel raporlarınızı oluşturmak için ham verileri kullanmanıza olanak sağlar.

Yeni raporların ilk kümesi cihaz uyumluluğuna odaklanır. Daha fazla bilgi için bkz. [blog-Microsoft Intune raporlama çerçevesi](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) ve [Intune raporları](reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>Yinelenen özel veya yerleşik roller <!-- 1081938   -->
Artık yerleşik ve özel rolleri kopyalayabilirsiniz. Daha fazla bilgi için bkz. [rolü kopyalama](../fundamentals/create-custom-role.md#copy-a-role).

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>Okul Yöneticisi rolü için yeni izinler <!-- 5621805  -->  
İki yeni izin, **profil** ve **eşitleme cihazı**ata, **kayıt programları** ** > >** , okul yöneticisi rolüne eklenmiştir. Eşitleme profili izni, grup yöneticilerinin Windows Autopilot cihazlarını eşitlemesini sağlar. Profil atama izni, kullanıcıların başlattığı Apple kayıt profillerini silmesine izin verir. Ayrıca, Autopilot cihaz atamalarını ve Autopilot dağıtım profili atamalarını yönetme izni verir. Tüm okul yöneticisi/Grup Yöneticisi izinlerinin listesi için bkz. [Grup yöneticileri atama](https://docs.microsoft.com/intune-education/group-admin-delegate).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Güvenlik

#### <a name="bitlocker-key-rotation---2564951----"></a>BitLocker anahtar döndürme<!-- 2564951  -->
Windows sürüm 1909 veya üstünü çalıştıran yönetilen cihazlar için [BitLocker kurtarma anahtarlarını uzaktan döndürmek](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) üzere bir Intune cihaz eylemi kullanabilirsiniz. Kurtarma anahtarlarının döndürülmeyeceğini nitelemek için cihazların kurtarma anahtarı döndürmesini destekleyecek şekilde yapılandırılması gerekir.  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>SCEP cihaz sertifikası dağıtımını desteklemek için adanmış cihaz kaydına yönelik güncelleştirmeler <!-- 5198878  -->
Intune artık, Wi-Fi profillerine sertifika tabanlı erişim için Android kurumsal adanmış cihazlara SCEP cihaz sertifikası dağıtımını desteklemektedir. Dağıtımın çalışması için cihazda Microsoft Intune uygulamanın mevcut olması gerekir. Sonuç olarak, Android kurumsal adanmış cihazlara yönelik kayıt deneyimini güncelleştirdik. Yeni kayıtlar yine de aynı (QR, NFC, sıfır-Touch veya cihaz tanımlayıcısı ile) hala başlatılır, ancak artık kullanıcıların Intune uygulamasını yüklemesini gerektiren bir adım vardır. Mevcut cihazlar, uygulamayı düzenli olarak otomatik olarak yüklenecek şekilde başlatacak.

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>İşletmeden işletmeye işbirliği için Intune denetim günlükleri<!--5670211 -->
İşletmeden işletmeye (B2B) işbirliği, şirketinizin uygulamalarını ve hizmetlerini başka bir kuruluştan Konuk kullanıcılarla güvenli bir şekilde paylaşmanızı sağlarken kendi şirket verileriniz üzerinde denetim sağlar. Intune artık B2B Konuk kullanıcıları için Denetim günlüklerini desteklemektedir. Örneğin, Konuk kullanıcılar değişiklik yaparken, Intune bu verileri denetim günlükleri aracılığıyla yakalayabilir. Daha fazla bilgi için bkz. [Azure ACTIVE DIRECTORY B2B 'de Konuk Kullanıcı erişimi nedir?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>11 Kasım 2019 haftası  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>Şirket Portalı 'de geliştirilmiş macOS kayıt deneyimi <!-- 5074349  -->  
MacOS kayıt deneyiminin Şirket Portalı, iOS kayıt deneyimi için Şirket Portalı daha yakından hizalanan daha basit bir kayıt işlemine sahiptir. Cihaz kullanıcıları şimdi şunları görür:  

- Bir uyleyici Kullanıcı arabirimi.  
- İyileştirilmiş bir kayıt denetim listesi.  
- Cihazlarını nasıl kaydedebileceğinize ilişkin daha net yönergeler.  
- Gelişmiş sorun giderme seçenekleri.  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>Windows Şirket Portalı uygulamasından başlatılan web uygulamaları<!-- 5030972 -->
Son kullanıcılar artık doğrudan Windows Şirket Portalı uygulamasından Web uygulamaları başlatabilir. Son kullanıcılar Web uygulamasını seçip **tarayıcıda aç**seçeneğini belirleyebilir. Yayınlanan Web URL 'SI doğrudan bir Web tarayıcısında açılır. Bu işlevsellik bir sonraki hafta boyunca alınacaktır. Web Apps hakkında daha fazla bilgi için bkz. [Microsoft Intune Web Apps ekleme](../apps/web-app.md).  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Windows 10 için Şirket Portalı yeni atama türü sütunu <!-- 5459950  -->
Şirket Portalı > **yüklü uygulamalar** > **atama türü** sütunu, **kuruluşunuzun gerektirdiği**şekilde yeniden adlandırıldı.  Bu sütunda, kullanıcılar bir uygulamanın gerekli olduğunu ya da kuruluşlarına göre isteğe bağlı olduğunu göstermek için **Evet** veya **Hayır** değeri görür. Cihaz kullanıcıları kullanılabilir uygulamalar kavramı hakkında karışdığı için bu değişiklikler yapılmıştır. Kullanıcılarınız, [cihazınızdaki uygulamaları yükleme ve paylaşma](../user-help/install-apps-cpapp-windows.md)konusundaki Şirket portalı uygulamaları yükleme hakkında daha fazla bilgi bulabilir. Kullanıcılarınız için Şirket Portalı uygulamasını yapılandırma hakkında daha fazla bilgi için bkz. [Microsoft Intune şirket portalı uygulamasını yapılandırma](../apps/company-portal-app.md).  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>4 Kasım 2019 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Güvenlik temelleri Microsoft Azure Kamu destekleniyor<!-- 4062552 -->

*Microsoft Azure Kamu* barındırılan Intune örnekleri artık kullanıcılarınızın ve cihazlarınızın güvenliğini sağlamanıza ve korumanıza yardımcı olan [güvenlik temellerini](../protect/security-baselines.md) kullanabilir.

## <a name="whats-new-archive"></a>Yenilikler arşivi
Önceki aylar için bkz. yenilikler [Arşivi](whats-new-archive.md).

## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


