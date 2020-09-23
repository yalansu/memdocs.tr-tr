---
title: Microsoft Intune - Azure’daki yenilikler | Microsoft Docs
titleSuffix: ''
description: Intune Azure portalındaki yenilikleri keşfedin
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/22/2020
ms.topic: reference
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
ms.openlocfilehash: 0f169da16cec126dd160a32543a835fbb99db546
ms.sourcegitcommit: b70cfbccd5ce6947fd7ce9235da2be84ab00666e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91107551"
---
# <a name="whats-new-in-microsoft-intune"></a>Microsoft Intune'daki yenilikler

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
### Scripts

<!-- ########################## -->
## <a name="week-of-september-21-2020"></a>21 Eylül 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### <a name="device-management"></a>Cihaz yönetimi

### <a name="tenant-attach-run-scripts-from-the-admin-center"></a>Kiracı iliştirme: yönetim merkezinden betikleri çalıştırma
<!--7220536, CM6234688-->
Şirket içi Configuration Manager [Çalıştır](../../configmgr/apps/deploy-use/create-deploy-scripts.md) özelliğinin gücünü Microsoft Endpoint Manager yönetim merkezine taşıyın. Yardım masası gibi ek personbuna, tek başına Configuration Manager yönetilen bir cihaza gerçek zamanlı olarak, PowerShell betikleri çalıştırmanızı sağlar. Bu, bu yeni ortama Configuration Manager yöneticisi tarafından önceden tanımlanmış ve onaylanmış olan PowerShell betiklerinin tüm geleneksel avantajlarını sağlar. Daha fazla bilgi için bkz. [kiracı iliştirme: yönetim merkezinden betikleri çalıştırma](../../configmgr/tenant-attach/scripts.md).

### <a name="app-management"></a>Uygulama yönetimi

#### <a name="app-protection-policies-allow-administrators-to-configure-incoming-org-data-locations---4176693---"></a>Uygulama koruma ilkeleri, yöneticilerin gelen kuruluş veri konumlarını yapılandırmasına izin verir<!-- 4176693 -->
Artık, kuruluş belgelerinde hangi güvenilen veri kaynaklarının açmasına izin verileceğini denetleyebilirsiniz. **Kuruluş verilerini** uygulama koruma ilkesi 'nin var olan kopyalarına benzer şekilde, hangi gelen veri konumlarına güvenildiğini tanımlayabilirsiniz. Bu işlevsellik, aşağıdaki uygulama koruma ilkesi ayarlarıyla ilgilidir:
- **Kuruluş verilerinin kopyalarını Kaydet**
- **Verileri kuruluş belgelerine açın**
- **Kullanıcıların seçili hizmetlerden veri açmasına izin ver**

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **uygulamalar**  >  **Uygulama koruma ilkeleri**  >  **ilke oluştur**' u seçin. Bu işlevselliği kullanmak için, Intune ilkesi tarafından yönetilen uygulamaların bu denetim için destek uygulaması gerekir. Daha fazla bilgi için bkz. [iOS uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-ios.md) ve [Android uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-android.md).

#### <a name="new-app-categories-to-target-app-protection-policies-more-easily---4802581----"></a>Uygulama koruma ilkelerini daha kolay hedefleyecek yeni uygulama kategorileri<!-- 4802581  -->
Intune 'un 2009 sürümü sayesinde, uygulama koruma ilkelerini daha kolay ve hızlı bir şekilde hedeflemek için kullanabileceğiniz uygulama kategorileri oluşturarak Microsoft Endpoint Manager 'ın UX ' i geliştirdik. Bu kategoriler **tüm ortak uygulamalar**, **Microsoft uygulamaları**ve **temel Microsoft uygulamalardır**. Hedeflenen uygulama koruma ilkesini oluşturduktan sonra, bu ilkeden etkilenecek uygulamaların listesini görüntülemek için **hedeflenecek uygulamaların listesini görüntüle** ' yi seçebilirsiniz. Yeni uygulamalar desteklenene kadar bu kategorileri bu uygulamaları uygun şekilde içerecek şekilde dinamik olarak güncelleştiririz ve ilkeleriniz seçtiğiniz Kategorideki tüm uygulamalara otomatik olarak uygulanacaktır. Gerekirse, tek tek uygulamalar için ilkeleri hedeflemek için de devam edebilirsiniz. Daha fazla bilgi için bkz. [Uygulama koruma ilkeleri oluşturma ve atama](../apps/app-protection-policies.md) ve [ıntune ile WINDOWS Information Protection (WIP) ilkesi oluşturma ve dağıtma](../apps/windows-information-protection-policy-create.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355----"></a>COPE Preview güncelleştirmesi: iş profili içeren Android kurumsal şirkete ait cihazlar için iş profili parolası gereksinimleri oluşturmaya yönelik yeni ayarlar<!--7088355  -->
Yeni ayarlar artık yöneticilere iş profili içeren Android kurumsal şirkete ait cihazlar için iş profili parolasını ayarlama olanağı sunar:

- Gerekli parola türü
- Minimum parola uzunluğu
- Parolanın süresi dolana kadar geçen gün sayısı
- Kullanıcının bir parolayı yeniden kullanabilmesi için gereken parola sayısı
- Cihaz silinmeden önceki oturum açma hatası sayısı

Daha fazla bilgi için bkz. [Intune kullanarak özelliklere izin vermek veya bunları kısıtlamak için Android Kurumsal cihaz ayarları](../configuration/device-restrictions-android-for-work.md).

#### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356-----"></a>COPE önizleme güncelleştirmesi: Android kurumsal şirkete ait cihazlar için kişisel profili bir iş profiliyle yapılandırmaya yönelik yeni ayarlar<!-- 7086356   -->
İş profili olan Android kurumsal şirkete ait cihazlar için, yalnızca kişisel profile uygulanan yeni ayarlar vardır (**cihaz**  >  **yapılandırma profilleri**  >  platform için bir**profil**  >  **Android Enterprise** >, **tam olarak yönetilen, adanmış ve şirkete ait iş profili**  >  **cihaz kısıtlamalarını** , profil > **kişisel profil**):

- **Kamera**: kişisel kullanım sırasında kameraya erişimi engellemek için bu ayarı kullanın.
- **Ekran yakalama**: kişisel kullanım sırasında ekran yakalamalarını engellemek için bu ayarı kullanın.
- **Kullanıcıların kişisel profilde bilinmeyen kaynaklardan uygulama yüklemesini etkinleştirmesine Izin ver**: Bu ayarı, kullanıcıların kişisel profilde bilinmeyen kaynaklardan uygulama yüklemelerine izin vermek için kullanın. 

Aşağıdakiler cihazlar için geçerlidir:
- İş profili, kişisel olarak etkinleştirilen Android kurumsal şirkete ait cihazlar.

Yapılandırabileceğiniz tüm ayarları görmek için [Android kurumsal cihaz ayarları ' na giderek özelliklere izin verin veya kısıtlayın](../configuration/device-restrictions-android-for-work.md).

#### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics--7200950-----"></a>Grup ilkesi Analytics kullanarak şirket içi GPO 'larınızı çözümleyin<!--7200950   -->
**Cihazlar**  >  **Grup İlkesi Analytics (Önizleme)** bölümünde, Grup İlkesi nesnelerinizi (GPO) Endpoint Manager Yönetim merkezinde içeri aktarabilirsiniz. İçeri aktardığınızda Intune, GPO 'YU otomatik olarak analiz eder ve Intune 'da eşdeğer ayarlara sahip olan ilkeleri gösterir. Ayrıca kullanım dışı olan veya artık desteklenmeyen GPO 'Ları gösterir. Daha ayrıntılı bir ayrıntıya gitme için, **Reports**  >   geçiş hazırlığı raporuna > raporlar**Grup İlkesi Analizi (Önizleme)** bölümüne gidin.

Bu özellik hakkında daha fazla bilgi için bkz. [Grup İlkesi Analytics](../configuration/group-policy-analytics.md).

Aşağıdakiler cihazlar için geçerlidir:
- Windows 10 ve üzeri

#### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422-----"></a>İOS/ıpados üzerinde uygulama kliplerini engelleyin ve macOS cihazlarındaki işletim sistemi olmayan yazılım güncelleştirmelerini erteleyin<!-- 7518422   -->
İOS/ıpados ve macOS cihazlarında bir cihaz kısıtlamaları profili oluşturduğunuzda, bazı yeni ayarlar vardır:

**iOS/ıpados 14.0 + uygulama kliplerini engelle**

- İOS/ıpados 14,0 ve üzeri için geçerlidir.
- Cihazların cihaz kaydı veya otomatik cihaz kaydı (denetimli cihazlar) ile kaydedilmiş olması gerekir.
- **Uygulama kliplerini engelle** ayarı, yönetilen cihazlarda uygulama kliplerini**engeller (cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **iOS/ıpados** for platform > **cihaz kısıtlamaları** > **genel**). Bloke edildiğinde, kullanıcılar uygulama klipleri ekleyemez ve mevcut uygulama klipleri kaldırılır.

**macOS 11 + yazılım güncelleştirmelerini ertele**

- MacOS 11 ve üzeri için geçerlidir. Denetimli macOS cihazlarında, cihazda Kullanıcı tarafından onaylanan cihaz kaydı veya otomatik cihaz kaydı üzerinden kaydedilmiş olması gerekir.
- Var olan **yazılım güncelleştirmelerini ertele** ayarı artık işletim sistemi ve işletim sistemi olmayan güncelleştirmeleri**geciktirebilir (cihaz**  >  **yapılandırma profilleri**, profil için  >  **Create profile**  >  **ma> cos** profilini **Device restrictions** oluşturur > **genel**). **Yazılım güncelleştirmeleri ayarının mevcut gecikme görünürlüğü** , işletim sistemi ve işletim sistemi olmayan güncelleştirmeler için geçerlidir. İşletim sistemi olmayan yazılım güncelleştirmelerinin erteleniyor, zamanlanmış güncelleştirmeleri etkilemez.
- Mevcut ilkelerin davranışı değiştirilmez, etkilenmez veya silinmez. Mevcut ilkeler, otomatik olarak aynı yapılandırmanızla yeni ayara geçirilir.

Yapılandırabileceğiniz cihaz kısıtlama ayarlarını görmek için bkz. [iOS/ıpados](../configuration/device-restrictions-ios.md) ve [MacOS](../configuration/device-restrictions-macos.md).

#### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886-----"></a>İOS/ıpados ve macOS cihazlarında uygulama başına VPN veya isteğe bağlı VPN kullanan yeni ayarlar<!-- 7758772 7758837 7758886   -->
**Cihazların**otomatik VPN  >  **Configuration profiles**  >  **Create profile**  >  > profili için iOS > **VPN** için**iOS** veya **MacOS** **Automatic VPN**profili oluşturma, cihazlar yapılandırma profillerinde otomatik VPN profilleri yapılandırabilirsiniz. Yapılandırabileceğiniz yeni uygulama başına VPN ayarları vardır:

- **Kullanıcıların OTOMATIK VPN 'yi devre dışı bırakmasını engelle**: otomatik olarak **uygulama başına VPN** veya **isteğe bağlı VPN** bağlantısı oluştururken, kullanıcıları otomatik VPN 'yi etkin ve çalışır durumda tutmaya zorlayabilirsiniz.
- **İlişkili etki alanları**: otomatik olarak **uygulama başına VPN** bağlantısı oluştururken, VPN profilinde VPN bağlantısını otomatik olarak başlatan ilişkili etki alanlarını ekleyebilirsiniz. İlişkili etki alanları hakkında daha fazla bilgi için bkz. [ilişkili etki alanları](../configuration/device-features-configure.md#associated-domains).
- **Dışlanan etki alanları**: otomatik **uygulama başına VPN** bağlantısı oluştururken, uygulama başına VPN bağlıyken VPN bağlantısını atlayabileceğiniz etki alanları ekleyebilirsiniz.

Bu ayarları ve yapılandırabileceğiniz diğer ayarları görmek için [iOS/ıpados VPN ayarları](../configuration/vpn-settings-ios.md) ve [MacOS VPN ayarları](../configuration/vpn-settings-macos.md)' na gidin.

[İOS/ıpados cihazları için uygulama başına sanal özel ağ (VPN)](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile)ayarlayın.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 14 ve üzeri
- macOS Big Sur (macOS 11)

#### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>İOS/ıpados cihazlarında IKEv2 VPN bağlantıları için en yüksek iletim birimini ayarlayın<!-- 7758937  -->
İOS/ıpados 14 ve daha yeni cihazlardan başlayarak, IKEv2 VPN bağlantıları kullanırken özel bir en yüksek iletim birimi (MTU) yapılandırabilirsiniz (**cihaz**  >  **yapılandırma profilleri**  >  **Create profile**  >  > profil oluşturma >**iOS** **VPN** **IKEv2**

Bu ayar ve yapılandırabileceğiniz diğerleri hakkında daha fazla bilgi için bkz. [Ikev2 ayarları](../configuration/vpn-settings-ios.md#ikev2-settings).

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 14 ve üzeri

#### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116-----"></a>İOS/ıpados cihazlarındaki e-posta profilleri için hesap başına VPN bağlantısı<!-- 7759116   -->
İOS/ıpados 14 ' ten başlayarak, yerel posta uygulaması için e-posta trafiği, kullanıcının kullandığı hesaba göre bir VPN aracılığıyla yönlendirilebilir. Intune 'da, **Hesap başına VPN profili için VPN profilini** yapılandırabilirsiniz (**cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**  >  **iOS/ıpados** for platform > **e-posta** > **Exchange ActiveSync e-posta ayarları**). 

Bu özellik, hesap tabanlı bir VPN bağlantısı için kullanmak üzere uygulama başına VPN profili seçmenizi sağlar. Kullanıcılar, e-posta uygulamasında Kuruluş hesabını kullandıklarında, uygulama başına VPN bağlantısı otomatik olarak açılır.

Bu ayarı ve yapılandırabileceğiniz diğerlerini görmek için [iOS ve ıpados cihazları için e-posta ayarları ekle](../configuration/email-settings-ios.md)' ye gidin.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 14 ve üzeri

#### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689-----"></a>İOS/ıpados cihazlarında Wi-Fi ağlarında MAC adresi rastgele seçimini devre dışı bırakma<!-- 7758689   -->
İOS/ıpados 14 ' den başlayarak, varsayılan olarak cihazlar bir ağa bağlanırken fiziksel MAC adresi yerine rastgele bir MAC adresi sunar. Bu davranış, bir cihazı MAC adresine göre izlemek daha zor olduğundan gizlilik için önerilir. Bu özellik ayrıca ağ erişim denetimi (NAC) dahil olmak üzere statik bir MAC adresine dayanan işlevselliği de keser.

Wi-Fi profillerinde ağ başına rastgele olarak MAC adresi rastgele seçimini devre dışı bırakabilirsiniz (**cihaz**yapılandırma profilleri, for the The The  >  **Configuration profiles**  >  **Create profile**  >  **iOS/iPadOS** **Basic** veya **Enterprise** for Wi-Fi Type for the Configuration for platform > **Wi-> Fi** ).

Bu ayarı ve yapılandırabileceğiniz diğerlerini görmek için [iOS ve ıpados cihazları Için Wi-Fi ayarları ekleme](../configuration/wi-fi-settings-ios.md)bölümüne gidin.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/ıpados 14 ve üzeri

#### <a name="new-settings-for-device-control-profiles----8368028---"></a>Cihaz denetim profillerine yönelik yeni ayarlar <!-- 8368028 -->
Windows 10 veya üzerini çalıştıran cihazlara yönelik *saldırı yüzeyi azaltma* Ilkesi için [ *cihaz denetim* profiline](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) bir çift ayar ekledik:

- **Çıkarılabilir depolama birimi**
- **USB bağlantıları (yalnızca HoloLens)**
 
*Saldırı yüzeyi azaltma* Ilkesi, Intune 'daki [Endpoint Security](../protect/endpoint-security-policy.md) 'nin bir parçasıdır.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="enrollment-status-page-shows-critical-kiosk-policies--7021540---"></a>Kayıt durumu sayfası kritik bilgi noktası ilkelerini gösterir<!--7021540 -->
Artık kayıt durumu sayfasında izlenen aşağıdaki ilkeleri görebileceksiniz
- Atanan erişim
- Bilgi noktası tarayıcı ayarları
- Edge tarayıcı ayarları

Diğer tüm bilgi noktası ilkeleri Şu anda izlenemez.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987----"></a>Zeköşeli cihazlar için PowerPrecision ve PowerPrecision + pille destek<!--3724987  -->
Bir cihazın Donanım Ayrıntıları sayfasında, şimdi PowerPrecision ve PowerPrecision ve pil kullanarak Zeköşeli cihazlarla ilgili aşağıdaki bilgileri görebilirsiniz:
- Zepoya tarafından belirlendiği şekilde sistem durumu derecelendirmesi (yalnızca PowerPrecision + piller)
- Tüketilen tam ücret döngüsü sayısı
- Cihazda son bulunan pil için son iade tarihi
- Cihazda en son bulunan pil paketinin seri numarası

#### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228----"></a>COPE önizleme güncelleştirmesi: iş profiliyle şirkete ait Android Kurumsal cihazları için iş profili parolasını sıfırlama <!--7217228  -->
Artık, Android kurumsal şirkete ait cihazlarda iş profili parolasını bir iş profiliyle sıfırlayabilirsiniz. Daha fazla bilgi için bkz. [geçiş kodunu sıfırlama](../remote-actions/device-passcode-reset.md#reset-a-passcode).

#### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043----"></a>Azure Active Directory birleştirilmiş bir ortak yönetilen cihazı yeniden adlandırma<!--7728043  -->
Artık Azure AD 'ye katılmış bir ortak yönetilen cihazı yeniden adlandırabilirsiniz. Daha fazla bilgi için bkz. [Intune 'da cihazı yeniden adlandırma](../remote-actions/device-rename.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="microsoft-tunnel-gateway-vpn-solution-in-preview---7843124----"></a>Önizleme aşamasında Microsoft Tunnel Gateway VPN çözümü<!-- 7843124  -->
Artık iOS ve Android Enterprise (tam olarak yönetilen, şirkete ait Iş profili, Iş profili) cihazlarındaki şirket içi kaynaklara uzaktan erişim sağlamak için [Microsoft tünel ağ geçidini](../protect/microsoft-tunnel-overview.md) dağıtabilirsiniz.

Microsoft tüneli, modern kimlik doğrulaması kullanarak uygulama başına ve tam cihaz VPN, bölünmüş tünel oluşturma ve koşullu erişim özelliklerini destekler.  Tünel, üretim hazırlığı için yüksek kullanılabilirlik için birden çok ağ geçidi sunucusunu destekleyebilir.

#### <a name="additional-biometric-authentication-support-for-android-devices---5706213----"></a>Android cihazlar için ek biyometrik kimlik doğrulama desteği<!-- 5706213  -->
Yeni Android cihazları, parmak izlerinin ötesinde daha farklı bir biyometri kümesi kullanmaktır. OEM 'Ler, parmak izi olmayan Biyometri için destek uygularken, son kullanıcıların güvenli erişim ve daha iyi bir deneyim için bu özelliği kullanma olasılığı vardır. Intune 'un 2009 sürümü ile son kullanıcılarınızın Android cihazının desteklediği seçeneğe bağlı olarak parmak izini veya yüzü açma kilidini kullanmasına izin verebilirsiniz. Parmak izinin ötesinde tüm biyometrik türlerin kimlik doğrulaması için kullanılıp kullanılamayacağını yapılandırabilirsiniz. Daha fazla bilgi için bkz. [Android cihazları Için uygulama koruma deneyimi](../apps/app-protection-policy.md#app-protection-experience-for-android-devices).

#### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-------"></a>Bir cihaz için uç nokta güvenlik yapılandırmasındaki yeni ayrıntılar<!-- 7745029     -->
Artık cihazlar için bir cihaz *uç noktası güvenlik yapılandırmasının*parçası olarak ek ayrıntılar görüntüleyebilirsiniz. Cihazlara dağıttığınız ilkelerle ilgili durum ayrıntılarını görüntülemek için ayrıntıya gidin, şimdi şunları bulabilirsiniz:
 
- **UPN** (Kullanıcı asıl adı): UPN, cihazdaki belirli bir kullanıcıya hangi uç nokta Güvenlik profilinin atandığını tanımlar. Bu, bir cihazdaki birden çok kullanıcının ve cihaza atanan bir profilin veya taban çizgisinin birden çok girişinin ayırt edilmesine yardımcı olmak için yararlıdır. 

Daha fazla bilgi için bkz. [güvenlik temelleri için çakışmaları çözme](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines).

#### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374------"></a>Uç nokta güvenlik rolü için genişletilmiş RBAC izinleri<!--7312374    -->
Intune için **Endpoint Security Manager** rolünde, [ **uzak görevler**için ek rol tabanlı erişim denetimi (RBAC) izinleri](../protect/endpoint-security.md#permissions-granted-by-the-endpoint-security-manager-role)vardır.
 
Bu rol, Microsoft Endpoint Manager yönetim merkezine erişim verir ve güvenlik temelleri, cihaz uyumluluğu, koşullu erişim ve Microsoft Defender Gelişmiş tehdit koruması dahil olmak üzere güvenlik ve uyumluluk özelliklerini yöneten kişiler tarafından kullanılabilir.
 
*Uzak görevlere* yönelik yeni izinler şunlardır:
 
- Şimdi yeniden Başlat
- Uzaktan kilitleme
- BitLockerKeys 'i döndürme (Önizleme)
- Filekasa anahtarını döndür
- Cihazları eşitleme
- Microsoft Defender
- Yapılandırma Yöneticisi eylemini Başlat
 
Herhangi bir Intune RBAC rolü için tüm izin kümesini görüntülemek için (**Kiracı Yöneticisi**  >  **Intune rolleri**  >  *bir rol*  >  **izinleri**seçin) bölümüne gidin.

#### <a name="updates-for-security-baselines---7102146-7103916-------"></a>Güvenlik temelleri için güncelleştirmeler<!-- 7102146, 7103916     -->
Aşağıdaki [güvenlik temelleri](../protect/security-baselines.md)için yeni sürümlere sahipsiniz:  
 
- **[MDM güvenlik temeli (Windows 10 güvenliği)](../protect/security-baseline-settings-mdm-all.md?pivots-mdm-sept-2020)**
- **[Microsoft Defender ATP temeli](../protect/security-baseline-settings-defender-atp.md?pivots=atp-sept-2020)**
 
Güncelleştirilmiş temel sürümler, ilgili ürün ekipleri tarafından önerilen en iyi yöntem yapılandırmalarının bakımını yapmanıza yardımcı olmak için son ayarlar için destek getirir.

Sürümler arasında nelerin değiştirildiğini anlamak için, bkz. nasıl dışarı aktarılacağını öğrenmek için [temel sürümleri karşılaştırın](../protect/security-baselines.md#compare-baseline-versions) . Değişiklikleri gösteren CSV dosyası.  

#### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503------"></a>Cihazların ilke çakışmalarının kaynağını belirlemek için uç nokta güvenlik yapılandırması ayrıntılarını kullanın<!-- 7567503    -->
Çakışma çözümüne yardımcı olmak için, artık seçili bir cihazın *uç nokta güvenlik yapılandırmasını* görüntülemek için güvenlik temeli profilinde detaya gidebilirsiniz. Buradan, bir *Çakışma* veya *hata* gösteren ayarları seçebilir ve çakışmanın bir parçası olan profilleri ve ilkeleri içeren ayrıntıların bir listesini görüntülemek için ayrıntıya devam edebilirsiniz.
 
Daha sonra bir çakışmanın kaynağı olan bir ilke seçerseniz, Intune, ilke yapılandırmasını gözden geçirebileceğiniz veya değiştirebileceğiniz ilkelere genel bakış bölmesini açar.
 
Aşağıdaki ilke türleri bir güvenlik temeliyle detaydan bir çakışma kaynağı olarak tanımlanabilir:

- Cihaz yapılandırma ilkesi
- Uç nokta güvenlik ilkeleri
 
Daha fazla bilgi için bkz. [güvenlik temelleri için çakışmaları çözme](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines).

#### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>İOS ve macOS cihazlarında 4096 anahtar boyutuna sahip sertifikalar için destek<!-- 7659175   -->
İOS/ıpados veya macOS cihazları için bir *SCEP sertifika* profili yapılandırdığınızda artık **4096** bitlik bir **anahtar boyutu (bit)** belirtebilirsiniz. 
 
Intune, aşağıdaki platformlar için 4096 bitlik anahtarları destekler: 
- iOS 14 ve üzeri
- macOS 11 ve üzeri  
 
SCEP sertifika profillerini yapılandırmak için bkz. [SCEP sertifika profili oluşturma](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile).

#### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Android 11 güvenilen kök sertifikaların Cihaz Yöneticisi kayıtlı cihazlara dağıtımını kullanımdan kaldırma<!--7662775  -->
Android 11 ' den başlayarak, güvenilen kök sertifikalar artık *Android Cihaz Yöneticisi*olarak kaydeden cihazlara güvenilen kök sertifikayı yükleyemez. Bu sınırlama, Samsung KNOX cihazlarını etkilemez. Samsung olmayan cihazlarda, kullanıcıların güvenilen kök sertifikayı cihaza el ile yüklemesi gerekir. 
 
Güvenilen kök sertifika bir cihaza el ile yüklendikten sonra, cihaza sertifika sağlamak için SCEP kullanabilirsiniz. Hala cihaza *güvenilir bir sertifika* İlkesi oluşturup dağıtmanız ve bu ilkeyi *SCEP sertifika* profiline bağlamanız gerekir.

- Güvenilen kök sertifika cihazdayken, SCEP sertifika profili başarıyla yüklenebilir. 
- Güvenilen sertifika cihazda bulunamıyorsa, SCEP sertifika profili başarısız olur.

Daha fazla bilgi için bkz. [Android Cihaz Yöneticisi Için güvenilen sertifika profilleri](../protect/certificates-configure.md#trusted-certificate-profiles-for-android-device-administrator).


#### <a name="tri-state-options-for-more-settings-in-endpoint-security-firewall-policy---6586159----"></a>Uç nokta güvenlik duvarı ilkesinde daha fazla ayar için üçlü durum seçenekleri<!-- 6586159  -->
[Windows 10 Için uç nokta güvenlik güvenlik duvarı ilkelerindeki](../protect/endpoint-security-firewall-profile-settings.md)birkaç farklı ayar durumuna bir yapılandırma ekledik.

Aşağıdaki ayarlar güncelleştirilir:
- **Durum bilgisi olan Dosya Aktarım Protokolü (FTP)** artık *Yapılandırılmadı*, *izin ver*ve *devre dışı*.
- **Anahtar modüllerinin yalnızca desteklemediği kimlik doğrulama paketlerini yok saymasını gerektir** , artık *Yapılandırılmadı*, *etkin*ve *devre dışı*.

#### <a name="improved-certificate-deployment-for-android-enterprise----6296499-------"></a>Android Enterprise için geliştirilmiş sertifika dağıtımı <!-- 6296499     -->
Tam olarak yönetilen, adanmış ve şirkete ait Iş profilleri olarak kaydeden Android kurumsal cihazlarda şifreleme ve imzalama için [Outlook Için S/MIME sertifikaları](../protect/certificates-s-mime-encryption-sign.md) kullanma desteğimizi geliştirdik. Daha önce, S/MIME kullanımı cihaz kullanıcısına erişime izin vermek için gereklidir. Artık, S/MIME sertifikaları kullanıcı etkileşimi olmadan kullanılabilir.   

Desteklenen Android cihazlara S/MIME sertifikaları dağıtmak için, cihaz yapılandırması için [PKCS içeri aktarılan sertifika profili](../protect/certificates-imported-pfx-configure.md) veya [SCEP sertifika profili](../protect/certificates-profile-scep.md) kullanın. **Android Enterprise** için bir profil oluşturun ve ardından *tam olarak yönetilen, adanmış ve şirkete ait iş profili*için kategoriden **PKCS içeri aktarılan sertifikası** ' nı seçin.

#### <a name="improved-status-details-in-security-baseline-reports---7221051---"></a>Güvenlik temeli raporlarında geliştirilmiş durum ayrıntıları<!-- 7221051 -->
[Güvenlik temeli için durum ayrıntılarının](../protect/security-baselines-monitor.md)çoğunu geliştirmeye başladık. Dağıttığınız taban çizgisi sürümleri hakkında bilgi görüntülerken artık daha anlamlı ve ayrıntılı durum görürsünüz.
 
Özellikle, bir taban çizgisi seçtiğinizde, *Sürüm*' ü seçtiğinizde ve bu taban çizgisinin bir örneğini seçtiğinizde, Ilk genel bakış aşağıdakileri görüntüler:
 
- **Güvenlik temeli duruşunu** grafiği-bu grafik artık aşağıdaki durum ayrıntılarını gösterir:
  - **Varsayılan taban çizgisiyle eşleşir** – bu durum, *eşleşen taban çizgisini* değiştirir ve bir cihaz yapılandırmasının varsayılan (değiştirilmemiş) taban çizgisi yapılandırmasıyla ne zaman eşleştiğini tanımlar.
  - **Özel ayarlarla eşleşir** – bu, bir cihaz yapılandırmasının yapılandırdığınız (özelleştirilmiş) ve dağıtılan taban çizgisiyle ne zaman eşleştiğini tanımlar.
  - **Yanlış yapılandırılmış** – bu bir cihazdan üç durum koşulu temsil eden bir toplu hatadır: *hata*, *bekleyen*veya *Çakışma*. Bu ayrı durumlar, aşağıda açıklandığı gibi diğer görünümlerde kullanılabilir.
  - **Uygulanamaz** -bu, ilkeyi alamayacak bir cihazı temsil eder. Örneğin, ilke Windows 'un en son sürümüne özgü bir ayarı güncelleştirir, ancak cihaz bu ayarı desteklemeyen daha eski (eski) bir sürümünü çalıştırır. 
- **Kategoriye göre güvenlik temeli** geri yükleme-Bu, cihaz durumunu kategoriye göre görüntüleyen bir liste görünümüdür. Kullanılabilir sütunlar *güvenlik temeli duruşunu* grafiğinin çoğunu yansıtır, ancak *yanlış yapılandırılmış* durum yerine, yanlış yapılandırılmış durum için üç sütun görürsünüz:
  - **Hata**: ilke uygulanamadı. Bu ileti, genellikle bir açıklamaya bağlantı veren bir hata kodu görüntüler.
  - **Çakışma**: aynı cihaza iki ayar uygulanır ve Intune çakışmayı sıralayamazsınız. Yöneticinin gözden geçirmesi gerekir.
  - **Bekliyor**: cihaz, ilkeyi henüz alacak şekilde Intune ile iade edilmedi.

#### <a name="new-setting-for-password-complexity-for-android-10-and-later-for-device-administrator-enrolled-devices---7992114---"></a>Cihaz Yöneticisi kayıtlı cihazlar için Android 10 ve üzeri için parola karmaşıklığı için yeni ayar<!-- 7992114 -->

Android 10 ve üzeri Android Cihaz Yöneticisi olarak kaydedilen cihazlarda yeni seçenekleri desteklemek için, hem [*cihaz uyumluluk*](../protect/compliance-policy-create-android.md#password) ilkesi hem de [*cihaz kısıtlama*](../configuration/device-restrictions-android.md#password) ilkesi için **parola karmaşıklığı** adlı yeni bir ayar ekledik.  Bu yeni ayarı, parola türü, uzunluğu ve kalitesindeki bir parola kuvvetinin bir *ölçüsünü* yönetmek için kullanırsınız. 
 
Samsung KNOX cihazları için parola karmaşıklığı uygulanmaz. Bu cihazlarda parola uzunluğu ve tür ayarları, parola karmaşıklığını geçersiz kılar.

Parola karmaşıklığı aşağıdaki seçenekleri destekler:

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
 
<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="bulk-actions-for-devices-listed-in-operational-report---8218481----"></a>İşletimsel raporda listelenen cihazlara yönelik toplu eylemler<!-- 8218481  -->
Microsoft Endpoint Manager güvenliği altında kullanıma sunulacak olan yeni virüsten koruma raporlarının bir parçası olarak, **Windows 10 algılanan kötü amaçlı yazılım** kullanım raporu, rapor içinde seçilen cihazlar için geçerli olan toplu eylemler sağlar. Eylemler **yeniden başlatma**, **hızlı tarama**ve **tam tarama**içerir. Daha fazla bilgi için bkz. [Windows 10 algılanan kötü amaçlı yazılım raporu](../fundamentals/reports.md#windows-10-detected-malware-report-operational).

#### <a name="export-intune-reports-using-graph-apis---8270831----"></a>Grafik API 'Lerini kullanarak Intune raporlarını dışarı aktarma<!-- 8270831  -->
Intune raporlama altyapısına geçirilmiş tüm raporlar, tek bir üst düzey dışarı aktarma API 'sinden dışarı aktarmak için kullanılabilir. Daha fazla bilgi için bkz. [Graph API 'lerini kullanarak Intune raporlarını dışa aktarma](../fundamentals/reports-export-graph-apis.md).

#### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Windows 10 ve üzeri için yeni ve geliştirilmiş Microsoft Defender virüsten koruma raporlaması<!-- 6018169  -->
Microsoft Endpoint Manager 'da Windows 10 ' da Microsoft Defender virüsten koruma için dört yeni rapor ekliyoruz. Bu raporlar şunları içerir:
- İki işlemsel rapor, *Windows 10 sağlıksız uç noktaları* ve *Windows 10 kötü amaçlı yazılım algıladı*. Microsoft Endpoint Manager 'da **Endpoint Security**  >  **Antivirus**' ü seçin.
- İki kuruluş raporu, *Virüsten koruma Aracısı durumu* ve *algılanan kötü amaçlı yazılım*. Microsoft Endpoint Manager 'da **raporlar**  >  **Microsoft Defender virüsten koruma**' yı seçin.

Daha fazla bilgi için bkz. [Intune raporları](../fundamentals/reports.md) ve [Microsoft Intune uç nokta güvenliği yönetimi](../protect/endpoint-security.md).

#### <a name="new-windows-10-feature-update-failures-report---6473121-----"></a>Yeni Windows 10 özellik güncelleştirme hatalarının raporu<!-- 6473121   -->
**Özellik güncelleştirme hataları** işlem raporu, bir **Windows 10 özellik güncelleştirmeleri** ilkesiyle hedeflenen ve bir güncelleştirmeyi denemeyen cihazlara yönelik hata ayrıntıları sağlar. Bu raporu görüntülemek için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde, **cihazlar**  >  **Monitor**  >  **özellik güncelleştirme hatalarının sayısı** ' nı seçin. Daha fazla bilgi için bkz. [Windows 10 güncelleştirmeleri Için](../protect/windows-update-for-business-configure.md#validation-and-reporting-for-windows-10-updates) [özellik güncelleştirme hatalarıyla Ilgili rapor](../fundamentals/reports.md#feature-update-failures-report-operational) ve doğrulama ve raporlama.

#### <a name="new-windows-10-feature-update-report---6473128----"></a>Yeni Windows 10 Özellik Güncelleştirme raporu<!-- 6473128  -->
**Windows 10 özellik güncelleştirme** raporu, bir **Windows 10 özellik güncelleştirmeleri** ilkesiyle hedeflenen cihazların Uyumluluk görünümünü sağlar. Bu raporun özetini görüntülemek için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde **raporlar**  >  **Windows güncelleştirmeleri** ' ni seçin. Belirli ilkelerin raporlarını görmek için **Windows güncelleştirmeleri** iş yükünde, **raporlar** sekmesini seçin ve **Windows özellik güncelleştirme raporunu**açın. Daha fazla bilgi için bkz. [Windows 10 özellik güncelleştirmeleri](../fundamentals/reports.md#windows-10-feature-updates-organizational).


<!-- ########################## -->
## <a name="week-of-september-7-2020"></a>7 Eylül 2020 haftası
<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381--"></a>Kiracı iliştirme: Yönetim merkezinde cihaz zaman çizelgesi<!--7220536, CM7141381-->
Configuration Manager, kiracı iliştirme aracılığıyla bir cihazı Microsoft Uç Nokta Yöneticisi ile eşitlediğinde, olayların bir zaman çizelgesini görebileceksiniz. Bu zaman çizelgesi, cihazdaki sorunları gidermenize yardımcı olabilecek geçmiş etkinlikleri gösterir. Daha fazla bilgi için bkz. [kiracı iliştirme: yönetim merkezindeki cihaz zaman çizelgesi](../../configmgr/tenant-attach/timeline.md).

#### <a name="tenant-attach-resource-explorer-in-the-admin-center--in7220536-cm6479284---"></a><a name="bkmk_hinv"></a> Kiracı iliştirme: Yönetim merkezinde kaynak Gezgini<!--IN7220536, CM6479284 -->
Microsoft uç nokta Yönetimi yönetim merkezinden, kaynak Gezgini 'ni kullanarak karşıya yüklenen Configuration Manager cihazları için donanım envanterini görüntüleyebilirsiniz. Daha fazla bilgi için bkz. [Yönetim merkezinde kiracı iliştirme: kaynak Gezgini](../../configmgr/tenant-attach/resource-explorer.md).

#### <a name="tenant-attach-cmpivot-from-the-admin-center--in7220536-cm6024392--"></a>Kiracı iliştirme: yönetim merkezinden CMPivot<!--IN7220536, CM6024392-->
CMPivot 'in gücünü Microsoft Endpoint Manager yönetim merkezine taşıyın. Yardım masası gibi ek kişilerin buluttan, tek bir ConfigMgr tarafından yönetilen cihaza karşı gerçek zamanlı sorgular başlatabilmesini ve sonuçları yönetim merkezine geri döndürmesini sağlar. Bu, CMPivot 'in tüm geleneksel avantajlarından yararlanmanızı sağlar. Bu, BT yöneticilerinin ve diğer belirlenen kişilerin, ortamlarında cihazların durumunu hızlıca değerlendirebilme ve işlem yapması için sahip olduğu bir işlemdir.

Yönetim merkezinden CMPivot hakkında daha fazla bilgi için bkz. [CMPivot önkoşulları](../../configmgr/tenant-attach/cmpivot-start.md), [CMPivot genel bakış](../../configmgr/tenant-attach/cmpivot-overview-attached.md)ve [CMPivot örnek komut dosyaları](../../configmgr/tenant-attach/cmpivot-samples-attached.md).

## <a name="week-of-august-31-2020"></a>31 Ağustos 2020 haftası

### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="new-version-of-the-pfx-certificate-connector-and-changes-for-pkcs-certificate-profile-support----4839686----"></a>PFX Sertifika bağlayıcısının yeni sürümü ve PKCS sertifika profili desteği değişiklikleri<!--  4839686  -->

PFX Sertifika Bağlayıcısı 'nın sürüm **6.2008.60.607**yeni bir sürümünü yayımladık. Bu yeni bağlayıcı sürümü:

- Windows 8.1 dışındaki tüm desteklenen platformlarda PKCS sertifika profillerini destekler
 
  PFX Sertifika Bağlayıcısı 'ndaki tüm PCKS desteğini birleştiriyoruz.  Bu, ortamınızda SCEP kullanmıyorsanız ve diğer amaçlar için NDES kullanmıyorsanız, Microsoft sertifika bağlayıcısını kaldırabilir ve NDES 'yi ortamınızdan kaldırabilirsiniz. 
 
- Microsoft sertifika Bağlayıcısı işlevselliği kaldırmadığı için, onları PKCS sertifika profillerini desteklemek üzere kullanmaya devam edebilirsiniz.
- Outlook S/MIME için sertifika iptalini destekler
- .NET Framework 4.7.2 gerektirir

Sertifika bağlayıcıları hakkında daha fazla bilgi için, her iki sertifika Bağlayıcısı için bağlayıcı sürümü listesi de dahil olmak üzere, bkz. [sertifika bağlayıcıları](../protect/certificate-connectors.md)


<!-- ########################## -->
## <a name="week-of-august-24-2020-2008-service-release"></a>24 Ağustos 2020 (2008 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322----"></a>Apple VPP belirtecinin silinmesinden önce ilişkili lisanslar iptal edildi<!--6195322  -->
Microsoft Endpoint Manager 'da bir Apple VPP belirtecini sildiğinizde, bu belirteçle ilişkilendirilen tüm Intune tarafından atanan lisanslar silinmeden önce otomatik olarak iptal edilir.

#### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-shows-descriptions----7414768-wnstaged---"></a>Android için Şirket Portalı App 'teki cihaz ayarlarını güncelleştirme iyileştirmesi açıklamaları gösterir <!-- 7414768 wnstaged -->
Android cihazlarda Şirket Portalı uygulamasında, **cihaz ayarlarını Güncelleştir** sayfası, güncelleştirilmesi gereken ayarları listeler. Kullanıcılar daha fazla bilgi görmek için sorunu genişletir ve **Çözümle** düğmesine bakın.

Bu Kullanıcı deneyimi geliştirilmiştir. Listelenen ayarlar, açıklamayı göstermek için varsayılan olarak genişletilir ve uygunsa **Çözümle** düğmesini gösterir. Daha önce, sorunlar varsayılan olarak daraltılıydı. Bu varsayılan davranış, kullanıcıların sorunları daha hızlı çözümleyebilmeleri için tıklama sayısını azaltır.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631-----"></a>İOS/ıpados ve macOS cihazları için VPN bağlantı türü olarak NetMotion kullanma<!-- 1333631   -->
Bir VPN profili oluşturduğunuzda netmotion, bir VPN bağlantı türü olarak kullanılabilir (**cihazlar**  >  **cihaz yapılandırması**  >  **Create profile**  >  **iOS/ıpados** veya **MacOS** for platform > **VPN** for platform > bağlantı türü için **netmotion** ).

Intune 'da VPN profilleri hakkında daha fazla bilgi için bkz. VPN [sunucularına bağlanmak IÇIN VPN profilleri oluşturma](../configuration/vpn-settings-configure.md).

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS
- macOS

#### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024----"></a>Windows 10 Wi-Fi profilleri için daha fazla korunan Genişletilebilir Kimlik Doğrulama Protokolü (PEAP) seçenekleri<!-- 3805024  -->
Windows 10 cihazlarında, Wi-Fi bağlantılarının kimliğini doğrulamak için Genişletilebilir Kimlik Doğrulama Protokolü (EAP) kullanarak Wi-Fi profilleri oluşturabilirsiniz (**cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  **Windows 10 and later** profil > **Enterprise**için **Wi-Fi** >.

Korumalı EAP (PEAP) seçeneğini belirlediğinizde kullanılabilir yeni ayarlar vardır:
- **PEAP aşamasında sunucu doğrulaması gerçekleştirme 1**: PEAP anlaşma aşaması 1 ' de, sunucu sertifika doğrulaması tarafından doğrulanır.
  - **PEAP aşaması 1 ' de sunucu doğrulaması için Kullanıcı Istemlerini devre dışı bırak**: PEAP anlaşma aşaması 1 ' de, Kullanıcı tarafından güvenilen sertifika yetkilileri IÇIN yeni PEAP sunucularının yetkilendirilmesini isteyen istemler gösterilmez.
- **Şifreleme bağlaması gerektir**: PEAP anlaşması sırasında şifre tabanlı bağlama kullanmayan PEAP sunucularıyla bağlantıları engeller.

Yapılandırabileceğiniz ayarları görmek için [Windows 10 ve üzeri cihazlar Için Wi-Fi ayarları ekle](../configuration/wi-fi-settings-windows.md)' ye gidin.

Aşağıdakiler cihazlar için geçerlidir: 
- Windows 10 ve üzeri

#### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576--idstaged---"></a>MacOS Microsoft Enterprise SSO eklentisini yapılandırma<!-- 5627576  idstaged -->

> [!IMPORTANT]
> MacOS 'ta Microsoft Azure AD SSO uzantısı hala geliştirilmektedir. Intune kullanıcı arabiriminde listelenir, ancak beklendiği gibi çalışmaz. MacOS 'ta SSO uygulama uzantısı türü için **Microsoft Azure AD** kullanmayın.

Microsoft Azure AD ekibi, macOS 10.15 + kullanıcılarına Microsoft uygulamalarına, kuruluş uygulamalarına ve Apple 'ın SSO özelliğini destekleyen ve Azure AD 'yi kullanarak kimlik doğrulaması yapan, tek bir oturum açma işlemiyle erişim elde etmesine izin vermek için bir yeniden yönlendirme çoklu oturum açma (SSO) uygulama uzantısı oluşturdu. Microsoft Enterprise SSO eklentisi sürümü sayesinde, SSO uzantısını yeni Microsoft Azure AD uygulama uzantısı türüyle**yapılandırabilirsiniz (cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  profil için**MacOS** for platform > **cihaz özellikleri** > **Çoklu oturum açma uygulama** uzantısı > SSO uygulama uzantısı türü > **Microsoft Azure AD**).

Microsoft Azure AD SSO uygulama uzantısı türüyle SSO sağlamak için, kullanıcıların macOS cihazlarındaki Şirket Portalı uygulamasını yüklemesi ve üzerinde oturum açması gerekir. 

MacOS SSO uygulama uzantıları hakkında daha fazla bilgi için bkz. [Çoklu oturum açma uygulama uzantısı](../configuration/device-features-configure.md#single-sign-on-app-extension).

Aşağıdakiler cihazlar için geçerlidir:
- macOS 10,15 ve üzeri

#### <a name="prevent-users-from-unlocking-android-enterprise-work-profile-devices-using-face-and-iris-scanning--6069759-idmiss---"></a>Kullanıcıların yüz ve Iris taramasını kullanarak Android kurumsal iş profili cihazlarını kilidini kullanmalarını engelleyin<!--6069759 idmiss -->
Artık kullanıcıların yüz veya Iris taramasını kullanmasını engelleyebilirsiniz. Bu, cihaz düzeyinde veya iş profili düzeyinde iş profili Yönetilen cihazlarının kilidini açabilir. Bu **, cihaz**  >  **yapılandırma profilleri**  >  için**profil oluşturma**  >  **Android Enterprise** for platform > **iş > profili** , profil > **iş profili ayarları** ve **parola** bölümleri için cihaz kısıtlamaları oluşturabilir ' de ayarlanabilir.

Daha fazla bilgi için bkz. [Intune kullanarak özelliklere izin vermek veya bunları kısıtlamak için Android Kurumsal cihaz ayarları](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Aşağıdakiler cihazlar için geçerlidir: 
- Android kurumsal iş profili

#### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991----"></a>Microsoft Enterprise SSO eklentisiyle diğer iOS/ıpados uygulamalarında SSO uygulama uzantılarını kullanın<!-- 7369991  -->
[Apple cihazları Için Microsoft ENTERPRISE SSO eklentisi](/azure/active-directory/develop/apple-sso-plugin) , SSO uygulama uzantılarını destekleyen tüm uygulamalarla birlikte kullanılabilir. Intune 'da bu özellik, eklentinin Apple cihazları için Microsoft kimlik doğrulama kitaplığı 'nı (MSAL) kullanmayan Mobile iOS/ıpados uygulamalarıyla birlikte çalışacağı anlamına gelir. Uygulamaların MSAL kullanması gerekmez, ancak Azure AD uç noktalarında kimlik doğrulaması yapması gerekir.

İOS/ıpados uygulamalarınızı eklentiyle birlikte SSO 'yu kullanacak şekilde yapılandırmak için bir iOS/ıpados yapılandırma profiline uygulama paketi tanımlayıcıları**ekleyin (cihaz**  >  **yapılandırma**  >  **Create profile**  >  **iOS/iPadOS** > > profilleri, **Device features** SSO uygulama uzantısı türü > uygulama paketi kimlikleri) için **Çoklu oturum açma uygulama uzantısı**  >  **Microsoft Azure AD** **App bundle IDs**

Yapılandırabileceğiniz geçerli SSO uygulama uzantısı ayarlarını görmek için [Çoklu oturum açma uygulaması uzantısına](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)gidin.

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="deploy-endpoint-security-antivirus-policy-to-tenant-attached-devices-preview---5475441----"></a>Kiracı ekli cihazlarına Endpoint Security virüsten koruma ilkesini dağıtma (Önizleme)<!-- 5475441  -->
Önizleme olarak, Configuration Manager ile yönettiğiniz cihazlara [Virüsten koruma için](../protect/endpoint-security-antivirus-policy.md) uç nokta güvenlik ilkesi dağıtabilirsiniz. Bu senaryo, desteklenen bir Configuration Manager sürümü ve Intune aboneliğiniz arasında bir kiracı iliştirme yapılandırması yapılandırmanızı gerektirir. Aşağıdaki Configuration Manager sürümleri desteklenir:

- Geçerli dalı Configuration Manager 2006

Daha fazla bilgi için, kiracı eklemeyi desteklemek üzere [Intune uç nokta güvenlik ilkelerine yönelik gereksinimlere](../protect/tenant-attach-intune.md#specific-requirements-for-intune-endpoint-security-policies) bakın.

#### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119------"></a>Endpoint Security virüsten koruma ilkesi dışlamaları için değişiklikler<!--5583940, 6018119    -->
[Endpoint Security virüsten koruma ilkesinin](../protect/endpoint-security-antivirus-policy.md)bir parçası olarak yapılandırdığınız Microsoft Defender virüsten koruma dışlama listelerini yönetmek için iki değişiklik yaptık. Değişiklikler, farklı ilkeler arasındaki çakışmaları önlemenize ve önceden dağıtılan ilkeleriniz üzerinde mevcut olabilecek dışlama listesi çakışmalarını çözmenize yardımcı olur.

Her iki değişiklik de aşağıdaki [Microsoft Defender virüsten koruma yapılandırma hizmeti sağlayıcılarının](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions) (CSP 'ler) ilke ayarları için geçerlidir:

- Defender/ExcludedPaths
- Defender/ExcludedExtensions
- Defender/ExcludedProcesses

Değişiklikler şunlardır:

- Yeni profil türü: **Microsoft Defender virüsten koruma dışlamaları** -yalnızca virüsten koruma dışlamalarıyla odaklanan bir ilke tanımlamak için Windows 10 ve üzeri için bu yeni profil türünü kullanın. Bu profil, diğer ilke yapılandırmalarından ayırarak dışlama listelerinizin yönetimini basitleştirmeye yardımcı olur.

  Yapılandırabileceğiniz Dışlamalar, Defender *süreçlerini*, *dosya uzantılarını*ve Microsoft Defender 'ın tarayabilmesi istemediğiniz *Dosya* ve *klasörleri* içerir.

- **İlke birleştirme** – Intune artık ayrı profillerde tanımladığınız dışlamaları listesini her bir cihaza veya kullanıcıya uygulanacak tek bir dışlamaları listesine birleştirir. Örneğin, üç ayrı ilke ile bir kullanıcıyı hedefliyorsanız, bu üç ilkenin dışlama listeleri *Microsoft Defender virüsten koruma dışlamalarının*tek bir üst kümesi ile birleştirilir ve bu da bu kullanıcı için geçerlidir.

#### <a name="import-and-export-lists-of-address-ranges-for-windows-firewall-rules---8125400----"></a>Windows güvenlik duvarı kuralları için adres aralıklarının listesini içeri ve dışarı aktarma<!-- 8125400  -->

. Csv dosyalarını kullanarak bir adres aralıkları listesini, uç nokta güvenliği için güvenlik duvarı ilkesinde Microsoft Defender güvenlik duvarı kuralları profiline **içeri** veya **dışarı aktarma** desteği ekledik. Aşağıdaki Windows güvenlik duvarı kuralı ayarları artık içeri ve dışarı aktarmayı destekliyor:

- **Yerel adres aralıkları**
- **Uzak adres aralıkları**

Ayrıca, yinelenen veya geçersiz girişlerin engellenmesine yardımcı olmak için hem yerel hem de uzak adres aralığı girişinin doğrulanmasını geliştirdik.

Bu ayarlar hakkında daha fazla bilgi için bkz. [Microsoft Defender güvenlik duvarı kuralları](../protect/endpoint-security-firewall-profile-settings.md#microsoft-defender-firewall-rules)ayarları.





<!-- ########################## -->
## <a name="week-of-august-17-2020"></a>17 Ağustos 2020 haftası

### <a name="intune-apps"></a>Intune uygulamaları

#### <a name="custom-brand-image-now-displayed-in-the-windows-company-portal-profile-page---4280187---"></a>Özel marka resmi artık Windows Şirket Portalı profili sayfasında görüntüleniyor<!-- 4280187 -->
Microsoft Intune Yöneticisi olarak, Intune 'a, Windows Şirket Portalı uygulamasındaki kullanıcının profil sayfasında bir arka plan görüntüsü olarak görüntülenecek özel bir marka resmi yükleyebilirsiniz. Daha fazla bilgi için bkz. [uygulamaları, Şirket portalı Web sitesini ve Intune uygulamasını özelleştirme Intune şirket portalı](../apps/company-portal-app.md#branding).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Şirket Portalı Configuration Manager uygulama desteği ekler<!-- 4297660 -->
Şirket Portalı artık Configuration Manager uygulamalarını desteklemektedir. Bu özellik, son kullanıcıların ortak yönetilen müşteriler için Şirket Portalı hem Configuration Manager hem de Intune tarafından dağıtılan uygulamaları görmesini sağlar. Şirket Portalı bu yeni sürümü, tüm ortak yönetilen müşteriler için Configuration Manager dağıtılan uygulamaları görüntüler. Bu destek, yöneticilerin farklı Son Kullanıcı Portalı deneyimlerini birleştirmesine yardımcı olur. Daha fazla bilgi için bkz. [ortak yönetilen cihazlarda şirket portalı uygulamasını kullanma](../../configmgr/comanage/company-portal.md). 

### <a name="device-security"></a>Cihaz güvenliği

#### <a name="set-device-compliance-state-from-third-party-mdm-providers---6361689---"></a>Üçüncü taraf MDM sağlayıcılarından cihaz uyumluluk durumunu ayarla<!-- 6361689 -->

Intune artık [cihaz uyumluluk ayrıntıları kaynağı olarak üçüncü taraf MDM çözümlerini](../protect/device-compliance-partners.md)desteklemektedir. Bu üçüncü taraf uyumluluk verileri, Microsoft Intune tümleştirmesi aracılığıyla iOS ve Android üzerinde Microsoft 365 uygulamalar için koşullu erişim ilkelerini zorlamak üzere kullanılabilir.  Intune, bir cihazın güvenilir olup olmadığını anlamak için üçüncü taraf sağlayıcıdan uyumluluk ayrıntılarını değerlendirir ve ardından Azure AD 'de koşullu erişim özniteliklerini ayarlar.  Azure AD koşullu erişim ilkelerinizi Microsoft Endpoint Manager yönetim merkezi veya Azure AD portalı içinden oluşturmaya devam edersiniz.

Aşağıdaki üçüncü taraf MDM sağlayıcıları, genel önizleme olarak bu yayında desteklenir:

- VMware çalışma alanı BIR UEM (daha önce AirWatch olarak biliniyordu)

*Bu güncelleştirme, müşterilere küresel olarak gönderilir. Bu özelliği bir sonraki hafta içinde görmeniz gerekir.*

<!-- ########################## -->
## <a name="week-of-august-10-2020"></a>10 Ağustos 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="tenant-attach-install-an-application-from-the-admin-center----in7220536-cm6024389--"></a>Kiracı iliştirme: yönetim merkezinden bir uygulama yükler <!-- IN7220536 CM6024389-->
Artık Microsoft Endpoint Manager yönetim merkezinden bir kiracıya bağlı cihaz için bir uygulamayı gerçek zamanlı olarak yüklemeyi başlatabilirsiniz. Daha fazla bilgi için bkz. [kiracı iliştirme: yönetim merkezinden uygulama yüklemesi](../../configmgr/tenant-attach/applications.md).

<!-- ########################## -->
## <a name="week-of-july-27-2020"></a>27 Temmuz 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="power-bi-compliance-report-template-v20---636958---"></a>Power BI uyumluluk raporu şablonu V 2.0<!-- 636958 -->
Power BI şablon uygulamaları, Power BI iş ortaklarının çok az kodlamayla veya hiç kodlama kullanmadan Power BI uygulamaları oluşturmasını ve bunları Power BI müşterilerine dağıtmasını sağlar. Yöneticiler, Power BI uyumluluk raporu şablonunun sürümünü V 1.0 'dan V 2.0 'a güncelleştirebilir. V 2.0, gelişmiş bir tasarım, Ayrıca, şablonun bir parçası olarak ortaya çıkacak hesaplamalarda ve verilerde yapılan değişiklikleri içerir. Daha fazla bilgi için bkz. [Power BI Ile veri ambarına bağlanma](../developer/reports-proc-get-a-link-powerbi.md) ve [bir şablon uygulamasını güncelleştirme](/power-bi/service-template-apps-install-distribute#update-a-template-app). Ayrıca, [Intune veri ambarı ile Power BI uyumluluk raporunun yeni bir sürümünü duyuran](https://aka.ms/new_compliance_report)blog gönderisine bakın.

<!-- ########################## -->
## <a name="week-of-july-13-2020--2007-service-release"></a>13 Temmuz 2020 (2007 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="exchange-on-premises-connector-support---7138486----"></a>Exchange şirket Içi bağlayıcı desteği<!-- 7138486  -->
Intune, 2007 (Temmuz) sürümünden itibaren Intune hizmetinden şirket Içi Exchange Bağlayıcı özelliği desteğini kaldırıyor. Etkin bağlayıcı içeren mevcut müşteriler şu anda geçerli işlevselliğe devam edebilir. Etkin Bağlayıcısı olmayan yeni müşteriler ve mevcut müşteriler, artık yeni bağlayıcılar oluşturamaz veya Intune 'dan Exchange ActiveSync (EAS) cihazlarını yönetemez. Bu müşteriler için, Microsoft şirket içi Exchange 'e erişimi korumak için Exchange [karma modern kimlik doğrulamasının (HMA)](/office365/enterprise/hybrid-modern-auth-overview) kullanılmasını önerir. HMA hem Intune Uygulama Koruması Ilkelerini (MAM olarak da bilinir) hem de şirket içi Exchange için Outlook Mobile aracılığıyla koşullu erişim imkanı sunar.

#### <a name="smime-for-outlook-on-ios-and-android-devices-without-enrollment---6517155---"></a>Kayıt olmadan iOS ve Android cihazlarda Outlook için S/MIME<!-- 6517155 -->
Artık, yönetilen uygulamalar için bir uygulama yapılandırma ilkesi kullanarak iOS ve Android cihazlarda Outlook için S/MIME 'yi etkinleştirebilirsiniz. Bu, cihaz kayıt durumundan bağımsız olarak ilke teslimine izin verir. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **uygulamalar**  >  **uygulama yapılandırma ilkeleri**  >  **Add**  >  **yönetilen uygulamalar**Ekle ' yi seçin. Ayrıca, kullanıcıların Outlook 'ta bu ayarı değiştirmesine izin verip vermeyeceğinizi de seçebilirsiniz. Ancak, S/MIME sertifikalarını iOS ve Android için Outlook 'a otomatik olarak dağıtmak için cihazın kayıtlı olması gerekir. S/MIME hakkında genel bilgi için bkz. [Intune 'da e-postayı imzalamak ve şifrelemek Için s/MIME 'ye genel bakış](../protect/certificates-s-mime-encryption-sign.md). Outlook yapılandırma ayarları hakkında daha fazla bilgi için bkz. [Microsoft Outlook yapılandırma ayarları](../apps/app-configuration-policies-outlook.md) ve [cihaz kaydı olmadan yönetilen uygulamalar için uygulama yapılandırma ilkeleri ekleme](../apps/app-configuration-policies-managed-app.md). İOS ve Android S/MIME bilgileri için Outlook için bkz. [s/MIME senaryoları](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios) ve [yapılandırma anahtarları-S/MIME ayarları](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122-----"></a>Windows 10 ve daha yeni cihazlar için yeni VPN ayarları<!-- 6602122   -->

Ikev2 bağlantı türünü kullanarak bir VPN profili oluşturduğunuzda yapılandırabileceğiniz yeni ayarlar vardır (**cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **Windows 10 ve sonrası** için platform > **VPN** > **temel VPN**):

- **Cihaz tüneli**: cihazların Kullanıcı oturumu açma da dahil olmak üzere herhangi bir Kullanıcı ETKILEŞIMI gerekmeden VPN 'ye otomatik olarak bağlanmasına izin verir. Bu özellik **her zaman açık**' i etkinleştirmenizi ve **makine sertifikalarını** kimlik doğrulama yöntemi olarak kullanmanızı gerektirir.
- Şifreleme paketi ayarları: istemci ve sunucu ayarlarını eşleştirmeye izin veren ıKE ve alt güvenlik ilişkilerinin güvenliğini sağlamak için kullanılan algoritmaları yapılandırın.

Yapılandırabileceğiniz ayarları görmek için, [Intune kullanarak VPN bağlantıları eklemek üzere Windows cihaz ayarları](../configuration/vpn-settings-windows-10.md)' na gidin.

Aşağıdakiler cihazlar için geçerlidir:

- Windows 10 ve üzeri

#### <a name="configure-more-microsoft-launcher-settings-in-a-device-restrictions-profile-on-android-enterprise-devices-cobo---6285001----"></a>Android kurumsal cihazlarda (COBO) cihaz kısıtlamaları profilinde daha fazla Microsoft Başlatıcı ayarı yapılandırma<!-- 6285001  -->

Android kurumsal tam olarak yönetilen cihazlarda, bir cihaz kısıtlamaları profili kullanarak daha fazla Microsoft başlatıcısı ayarı**yapılandırabilirsiniz (cihaz**  >  **yapılandırma profilleri**,  >  platform için bir**profil**  >  **Android Enterprise** > **cihaz sahibi yalnızca**  >  **cihaz kısıtlamaları**cihaz  >  **deneyimi**  >  **tam olarak yönetilir**). 

Bu ayarları görmek için [Android kurumsal cihaz ayarları ' na giderek özelliklere izin verin veya kısıtlayın](../configuration/device-restrictions-android-for-work.md#device-experience).

Ayrıca, Microsoft Başlatıcı ayarlarını bir [uygulama yapılandırma profili](../apps/configure-microsoft-launcher.md)kullanarak da yapılandırabilirsiniz.

Aşağıdakiler cihazlar için geçerlidir:

- Android kurumsal cihaz sahibi tam olarak yönetilen cihazlar (COBO)

#### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184---idstaged---"></a>Android kurumsal cihaz sahibi adanmış cihazlarda (COSU) yönetilen giriş ekranı için yeni özellikler<!-- 7414175 7133328 7133720 7134873 7135184   idstaged -->

Android kurumsal cihazlarda Yöneticiler, birden çok uygulama bilgi noktası modunu kullanarak adanmış cihazlarda yönetilen giriş ekranını özelleştirmek için cihaz yapılandırma profillerini kullanabilir (**cihazlar**  >  **yapılandırma profilleri**, cihaz  >  **Create profile**  >  **Android Enterprise** sahibi > cihaz **sahibine yalnızca**  >  **Device Restrictions** profil > cihaz için **Device experience**  >  **ayrılmış**cihaz  >  **Çoklu uygulaması**) cihaz kısıtlamalarına sahip olabilir.

Özellikle şunları yapabilirsiniz:

- Simgeleri özelleştirme, ekran yönünü değiştirme ve rozet simgelerinde uygulama bildirimlerini gösterme <!--7414175-->
- Yönetilen ayarlar kısayolunu gizle <!--7133328-->
- Hata ayıklama menüsüne daha kolay erişim <!--7133720-->
- Wi-Fi ağlarının izin verilen bir listesini oluşturma <!-- 7134873-->
- Cihaz bilgilerine daha kolay erişin <!-- 7135184-->

Daha fazla bilgi için bkz. [Android kurumsal cihaz ayarları, özelliklere izin vermek veya](../configuration/device-restrictions-android-for-work.md) [Bu blogu](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060)kısıtlamak için.

Aşağıdakiler cihazlar için geçerlidir:

- Android kurumsal cihaz sahibi, adanmış cihazlar (COSU)

#### <a name="administrative-templates-updated-for-microsoft-edge-84--7722068--"></a>Microsoft Edge 84 için güncelleştirilmiş Yönetim Şablonları<!--7722068-->
Microsoft Edge için kullanılabilen ADMX ayarları güncelleştirildi. Son kullanıcılar artık Edge 84 ' de eklenen yeni ADMX ayarlarını yapılandırabilir ve dağıtabilir. Daha fazla bilgi için bkz. [Edge 84 sürüm notları](/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="corporate-owned-personally-enabled-devices-preview--4442275----"></a>Şirkete ait, kişisel olarak etkinleştirilen cihazlar (Önizleme)<!--4442275  -->
Intune artık Android 8 ve üzeri işletim sistemi sürümleri için iş profiliyle iOS kurumsal şirkete ait cihazları desteklemektedir. İş profiline sahip şirkete ait cihazlar, Android kurumsal çözüm kümesindeki kurumsal yönetim senaryolarından biridir. Bu senaryo, kurumsal ve kişisel kullanım için tasarlanan tek Kullanıcı cihazlarına yöneliktir. Şirkete ait, kişisel olarak etkinleştirilen bu (COPE) senaryo şunları sunar:

- çalışma ve kişisel profil kapsayıcılama
- Yöneticiler için cihaz düzeyi denetimi
- Son kullanıcılara kişisel verilerinin ve uygulamalarının özel olarak kalacağı garantisi

İlk genel önizleme sürümü, genel olarak kullanılabilir sürüme dahil edilecek özelliklerin bir alt kümesini içerir. Ek özellikler, toplama temelinde eklenecektir. İlk önizlemede kullanılabilir olacak özellikler şunlardır:

- Kayıt: Yöneticiler, son tarihi olmayan benzersiz belirteçlerle birden çok kayıt profili oluşturabilir. Cihaz kaydı NFC, Token entry, QR Code, Zero Touch veya Knox Mobile kaydı aracılığıyla yapılabilir.
- Cihaz yapılandırması: mevcut, tam olarak yönetilen ve ayrılmış cihaz ayarlarının bir alt kümesi.
- Cihaz Uyumluluğu: Şu anda tam olarak yönetilen cihazlar için kullanılabilen uyumluluk ilkeleri.
- Cihaz eylemleri: cihazı silme (fabrika sıfırlaması), cihazı yeniden başlatma ve cihazı kilitleme.  
- Uygulama Yönetimi: uygulama atamaları, uygulama yapılandırması ve ilişkili raporlama özellikleri 
- Koşullu Erişim

Şirkete ait iş profili önizlemesi hakkında daha fazla bilgi için bkz. [destek blogu](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805-----"></a>MacOS cihazları için uzaktan kilitleme eylemine yönelik güncelleştirmeler<!--7032805   -->
MacOS cihazları için uzaktan kilitleme eyleminde yapılan değişiklikler şunları içerir:
- Kurtarma PIN 'i silinmeden önce 30 gün boyunca görüntülenir (7 gün yerine).
- Bir yöneticinin açık ikinci bir tarayıcısı varsa ve komutu farklı bir sekmeden ya da tarayıcıdan yeniden tetiklemeyi denediğinde, Intune komutun geçmesine izin verir. Ancak raporlama durumu, yeni bir PIN oluşturmak yerine başarısız olarak ayarlanır.
- Önceki komut hala beklenirse veya cihaz geri ayarlanmamışsa, yöneticinin başka bir uzaktan kilitleme komutu vermesine izin verilmez.
Bu değişiklikler, birden çok uzaktan kilitleme komutlarından sonra doğru PIN 'in üzerine yazılmasını engellemek için tasarlanmıştır.

#### <a name="device-actions-report-differentiates-between-wipe-and-protected-wipe--7118901---"></a>Cihaz eylemleri silme ve korumalı silme arasındaki farklılıklar<!--7118901 -->
**Cihaz eylemleri** raporu artık silme ve korumalı silme eylemleri arasında farklılaştırır. Raporu görmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **Monitor**  >  **cihaz eylemlerini** izleme ( **diğer**altında) bölümüne gidin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="microsoft-defender-firewall-rule-migration-tool-preview---6423187-----"></a>Microsoft Defender güvenlik duvarı kuralı geçiş aracı önizlemesi<!-- 6423187   -->
Genel önizleme olarak, Microsoft Defender güvenlik duvarı kurallarını geçiren bir PowerShell tabanlı araç üzerinde çalışıyoruz. Aracı yükleyip çalıştırdığınızda, Windows 10 istemcisinin geçerli yapılandırmasına dayalı olarak Intune için uç nokta güvenliği Güvenlik Duvarı kural ilkelerini otomatik olarak oluşturur. Daha fazla bilgi için bkz. [Endpoint Security güvenlik duvarı kuralı geçiş aracına genel bakış](../protect/endpoint-security-firewall-rule-tool.md).

#### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-generally-available---7303816-----"></a>Kiracı ekli cihazlarını MDADTP 'ye ekleme için uç nokta algılama ve yanıt ilkesi genel kullanıma sunuldu<!-- 7303816   -->
Intune 'daki Endpoint Security 'nin bir parçası olarak, [Configuration Manager tarafından yönetilen cihazlarla kullanılmak üzere uç nokta algılama ve yanıt (EDR) ilkeleri](../protect/endpoint-security-edr-policy.md) artık *Önizleme* aşamasındadır ve *genel kullanıma sunulmuştur*.

EDR ilkesini Configuration Manager desteklenen bir sürümünden cihazlarla kullanmak için, [Configuration Manager Için kiracı eklemeyi](../../configmgr/tenant-attach/device-sync-actions.md)yapılandırın. Kiracı ekleme yapılandırmasını tamamladıktan sonra, Microsoft Defender Gelişmiş tehdit koruması 'na (Microsoft Defender ATP) Configuration Manager tarafından yönetilen cihazları eklemek için EDR ilkeleri dağıtabilirsiniz.

#### <a name="bluetooth-settings-are-available-in-device-control-profiles-for-endpoint-security-attack-surface-reduction-policy---7032084-----"></a>Endpoint Security saldırı yüzeyi Azaltma ilkesi için cihaz denetim profillerinde Bluetooth ayarları bulunur <!--7032084   -->
Windows 10 cihazlarında Bluetooth 'u, *uç nokta güvenliği saldırı yüzeyi Azaltma ilkesi*için [cihaz denetim profiline](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) ekledik.  Bunlar, cihaz *yapılandırması*için cihaz kısıtlama profillerinde kullanılabilir olanlarla aynı ayarlardır.

#### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801-----"></a>Windows 10 cihazları için Endpoint Security virüsten koruma ilkesiyle birlikte tanım güncelleştirmelerinin kaynak konumlarını yönetme<!-- 6347801   -->  
[Windows 10 cihazları için Endpoint Security virüsten koruma Ilkesinin](../protect/antivirus-microsoft-defender-settings-windows.md#updates) *güncelleştirmeler* kategorisine, cihazların güncelleştirme tanımlarını alma biçimini yönetmenize yardımcı olabilecek iki yeni ayar ekledik:

- *Tanım güncelleştirmelerini indirmek için dosya paylaşımlarını tanımlayın*
- *Tanım güncelleştirmelerini indirmek için kaynak sırasını tanımlayın*

Yeni ayarlarla, tanım güncelleştirmeleri için kaynak konumları indirme olarak UNC dosya paylaşımları ekleyebilir ve farklı kaynak konumlarına hangi sırada bağlantı kurulacağınızı tanımlayabilirsiniz.

#### <a name="improved-security-baselines-node---7433136------"></a>Geliştirilmiş güvenlik temelleri düğümü<!-- 7433136    -->
Microsoft Endpoint Manager Yönetim merkezinde [güvenlik temeli düğümünün](../protect/security-baselines.md) kullanılabilirliğini geliştirmek için bazı değişiklikler yaptık. Artık **uç nokta güvenlik**  >  **güvenliği temelleri** detayına gidin ve ardından, **profiller** bölmesi ile sunulan MDM güvenlik temeli gibi bir güvenlik taban çizgisi türü seçin. Profiller bölmesinde, bu taban çizgisi türü için oluşturduğunuz profilleri görüntüleyin.  Daha önce konsol, her zaman ayrı profiller için raporlarda bulunan ayrıntılarla eşleşen bir toplam veri toplamasını içeren bir genel bakış bölmesi sundu.

Değiştirilmeden, profiller bölmesinden, bu profil özelliklerinin yanı sıra *izleyici*altında bulunan çeşitli raporları görüntülemek için detaya gitme için bir profil seçebilirsiniz.  Benzer şekilde, profillerle aynı düzeyde, dağıttığınız bu profil türünün çeşitli sürümlerini görüntülemek için hala **sürümler** ' i seçebilirsiniz. Bir sürümde detaya gitme yaptığınızda, profil raporlarına benzer şekilde raporlara de erişebilirsiniz. 

#### <a name="derived-credentials-support-for-windows---4886090-----"></a>Windows için türetilmiş kimlik bilgileri desteği<!-- 4886090   -->
Artık Windows cihazlarınızla türetilmiş kimlik bilgilerini kullanabilirsiniz. Bu, iOS/ıpados ve Android için mevcut desteğe genişletilir ve aynı türetilmiş kimlik bilgileri sağlayıcıları için kullanılabilir olacaktır:
- Entrust Datacard
- Intercede
- DıŞA purebred

Tek başına desteği, Wi-Fi veya VPN profillerinin kimliğini doğrulamak için türetilmiş bir kimlik bilgisinin kullanımını içerir. Windows cihazlarında, türetilmiş kimlik bilgileri, kullandığınız türetilmiş kimlik bilgisi sağlayıcısı tarafından verilen istemci uygulamasından verilir.

#### <a name="manage-filevault-encryption-for-devices-that-were-encrypted-by-the-device-user-and-not-by-intune--5239424----"></a>Intune tarafından değil, cihaz kullanıcısı tarafından şifrelenen cihazlar için dosya Kasası şifrelemesini yönetme<!--5239424  -->
Intune artık, Intune ilkesi tarafından değil [cihaz kullanıcısı tarafından şifrelenen bir macOS cihazında dosya Kasası disk şifrelemesi yönetimini varsayabilir](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices).  Bu senaryo şunları gerektirir:
- Intune 'dan, dosya kasasını sağlayan disk şifreleme ilkesini alacak olan cihaz.
- Cihaz kullanıcısı, şifreli cihaz için kişisel kurtarma anahtarını Intune 'a yüklemek üzere Şirket Portalı Web sitesini kullanır. Anahtarı karşıya yüklemek için şifrelenmiş macOS cihazı için *Mağaza kurtarma anahtarı* seçeneğini seçeceğiz.

Kullanıcı kurtarma anahtarını karşıya yükledikten sonra, Intune geçerli olduğunu doğrulamak için anahtarı döndürür. Intune artık, cihazı doğrudan şifrelemek için ilkeyi kullandığımıza göre anahtarı ve şifrelemeyi yönetebilir. Bir kullanıcının cihazını kurtarmaları gerekir, bu, aşağıdaki konumlardan herhangi bir cihaz kullanarak kurtarma anahtarına erişebilirler:   
- Şirket Portalı web sitesi
- İOS için Şirket Portalı App/ıpados 
- Android için Şirket Portalı uygulaması
- Intune uygulaması

#### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632--"></a>MacOS Filekasası disk şifrelemesi sırasında bir cihaz kullanıcısının kişisel kurtarma anahtarını gizle<!--  5475632-->
MacOS Filekasası disk şifrelemesini yapılandırmak için uç nokta güvenlik ilkesi kullandığınızda, cihaz şifrelenirken *kişisel kurtarma anahtarının* görüntülenmesini engellemek için [**Kurtarma anahtarını Gizle**](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) ayarını kullanın. Şifreleme sırasında anahtarı gizleyerek, kullanıcıların cihaz şifrelemesini beklerken daha sonra yazamayacak kadar güvenli kalmasına yardımcı olabilirsiniz. 

Daha sonra, kurtarma gerekliyse, Kullanıcı Intune Şirket Portalı Web sitesi, iOS/ıpados Şirket Portalı, Android Şirket Portalı veya Intune uygulaması aracılığıyla kişisel kurtarma anahtarını görüntülemek için her zaman herhangi bir cihazı kullanabilir.

#### <a name="improved-view-of-security-baseline-details-for-devices---5536846----"></a>Cihazlar için güvenlik temeli ayrıntılarının geliştirilmiş görünümü<!-- 5536846  -->
Artık, cihaza uygulanan güvenlik temellerine yönelik ayar ayrıntılarını görüntülemek için bir cihazın ayrıntılarında ayrıntıya gidebilirsiniz. Ayarlar, ayarı kategorisi, ayar adı ve durumu içeren basit, düz bir liste içinde görüntülenir. Daha fazla bilgi için bkz. [cihaz başına Endpoint Security yapılandırmasını görüntüleme](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="device-compliance-logs-now-in-english--6014904----"></a>Cihaz uyumluluk günlükleri artık Ingilizce olarak<!--6014904  -->
Intune Devicekarmaşık kuruluş günlükleri daha önce yalnızca Karmaşıkstate, OwnerType ve DeviceHealthThreatLevel için numaralandırmalar içeriyordu. Artık bu günlüklerde sütunlarda Ingilizce bilgiler vardır.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

#### <a name="assign-profile-and-update-profile-permission-changes--7177586-----"></a>Profil ata ve profili Güncelleştir izin değişiklikleri<!--7177586   -->
Otomatik cihaz kayıt akışı için profil atama ve güncelleştirme profili için rol tabanlı erişim denetimi izinleri değişti:

Profil ata: Yöneticiler bu izinle profiller ve otomatik cihaz kaydı için bir belirtece varsayılan bir profil atar.

Güncelleştirme profili: Bu izne sahip yöneticiler, yalnızca otomatik cihaz kaydı için mevcut profilleri güncelleştirebilir.

Bu rolleri görmek için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **kiracı yönetim**  >  **rolleri**  >  **tüm roller**  >  **Create**  >  **izin**  >  **rolleri**oluşturma ' ya gidin.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Betik Oluşturma

#### <a name="additional-data-warehouse-v10-properties---6125732----"></a>Ek veri ambarı v 1.0 özellikleri<!-- 6125732  -->
Intune veri ambarı v 1.0 kullanılarak ek özellikler mevcuttur. Aşağıdaki özellikler artık [cihazlar](../developer/reports-ref-devices.md#devices) varlığı aracılığıyla kullanıma sunulmuştur:
- `ethernetMacAddress` -Bu cihazın benzersiz ağ tanımlayıcısı.
- `office365Version` -Cihaza yüklü Microsoft 365 sürümü.

Aşağıdaki özellikler artık [Devicepropertygeçmişin](../developer/reports-ref-devices.md#devicepropertyhistories) varlığı aracılığıyla kullanıma sunulmuştur:
- `physicalMemoryInBytes` -Bayt cinsinden fiziksel bellek.
- `totalStorageSpaceInBytes` -Bayt cinsinden toplam depolama kapasitesi.

Daha fazla bilgi için bkz. [Microsoft Intune veri ambarı API 'si](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## <a name="week-of-july-06-2020"></a>06 Temmuz 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023---"></a>Android 'de Şirket Portalı ve Intune uygulamalarında cihaz simgelerine güncelleştirme<!-- 6057023 -->
Android cihazlarda Şirket Portalı ve Intune uygulamalarındaki cihaz simgelerini, daha modern bir görünüm oluşturmak ve Microsoft 'un akıcı tasarım sistemiyle uyum sağlamak için güncelleştirdik. İlgili bilgiler için bkz. [iOS/ıpados ve macOS için şirket portalı App 'teki simgelere güncelleştirme](whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707---"></a>iOS Şirket Portalı, Apple 'ın Kullanıcı benzeşimi olmadan otomatik cihaz kaydını destekleyecektir<!-- 7282707 --> 
İOS Şirket Portalı, artık Apple 'ın otomatik cihaz kaydı kullanılarak kaydedilmiş cihazlarda atanmış bir Kullanıcı gerekmeden desteklenmektedir. Son Kullanıcı iOS Şirket Portalı, cihaz benzeşimi olmadan kaydedilen bir iOS/ıpados cihazında birincil kullanıcı olarak kurmak için oturum açabilir. Otomatik cihaz kaydı hakkında daha fazla bilgi için bkz. [Apple 'ın otomatik cihaz kaydı Ile iOS/ıpados cihazlarını otomatik olarak kaydetme](../enrollment/device-enrollment-program-enroll-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview---7552762---"></a>Kiracı iliştirme: Yönetim merkezinde ConfigMgr istemci ayrıntıları (Önizleme)<!-- 7552762 -->

Artık Microsoft Endpoint Manager Yönetim Merkezi 'nde belirli bir cihaz için Koleksiyonlar, sınır grubu üyeliği ve gerçek zamanlı istemci bilgilerini içeren ConfigMgr istemci ayrıntılarını görebilirsiniz. Daha fazla bilgi için bkz. [kiracı iliştirme: ConfigMgr istemci ayrıntıları Yönetim Merkezi (Önizleme)](../../configmgr/tenant-attach/client-details.md).

## <a name="week-of-june-22-2020"></a>22 Haziran 2020 haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Intune için yeni kullanılabilir korumalı uygulamalar<!-- 7248952 -->
Aşağıdaki korumalı uygulamalar artık kullanılabilir:
- BlueJeans görüntülü konferans
- Intune için Cisco Jabber
- Intune için Tableau Mobile
- Intune için sıfır

Korumalı uygulamalar hakkında daha fazla bilgi için bkz. [Microsoft Intune korumalı uygulamalar](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>İzleme ve sorun giderme

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>Kullanıcı üretkenliğini artırmak ve BT destek maliyetlerini azaltmak için Endpoint Analytics 'i kullanın<!-- 5653063 --> 
Sonraki hafta boyunca bu özellik kullanıma sunulacaktır. Kullanıcı üretkenliğini geliştirmek ve Kullanıcı deneyimine yönelik Öngörüler sunarak BT destek maliyetlerini azaltmak için Endpoint Analytics amaçlar. İçgörüler, BT 'nin son kullanıcı deneyimini öngörülü destekle en uygun hale getirmesine ve yapılandırma değişikliklerinin Kullanıcı etkisini değerlendirerek Kullanıcı deneyimine yönelik gerilemeleri algılamasına olanak tanır. Daha fazla bilgi için bkz. [Endpoint Analytics önizlemesi](https://aka.ms/uea).

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>Komut dosyası paketlerini kullanarak Son Kullanıcı cihaz sorunlarını önceden düzelt<!-- 5933328 -->
Kuruluşunuzdaki en önemli destek sorunlarını önceden bulmak ve gidermek için, Son Kullanıcı cihazlarında betik paketleri oluşturup çalıştırabilirsiniz. Betik paketlerinin dağıtımı, destek çağrılarını azaltmanıza yardımcı olur. Kendi betik paketlerinizi oluşturmayı seçin veya yazdığımız ve destek biletlerini azaltmak için ortamımızda kullandığımız komut dosyası paketlerinden birini dağıtın. Intune, dağıtılan betik paketlerinizin durumunu görmenizi ve algılama ve düzeltme sonuçlarını izlemenizi sağlar. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **raporlar**  >  **Endpoint Analytics**  >  **proaktif**düzeltmeler ' i seçin. Daha fazla bilgi için bkz. [proaktif](https://aka.ms/uea_prs)düzeltmeler.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Android için uyumluluk ilkelerinde Microsoft Defender ATP kullanma<!-- 4425686  -->

Artık Intune 'U [Android cihazları Microsoft Defender Gelişmiş tehdit koruması](../protect/advanced-threat-protection-configure.md#onboard-devices) (MICROSOFTDEFENDER ATP) uygulamasına eklemek için kullanabilirsiniz. Kayıtlı cihazlarınız eklendi olduktan sonra, Android için uyumluluk ilklarınız Microsoft Defender ATP 'den *tehdit düzeyi* sinyallerini kullanabilir. Bunlar, daha önce Windows 10 cihazlarında kullanabileceğiniz sinyallerdir.

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563----"></a>Android cihazlar için Defender ATP Web korumasını yapılandırma<!-- 6185563  -->

Android cihazlar için Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP) kullandığınızda, [Microsoft Defender ATP Web koruması](../protect/advanced-threat-protection-manage-android.md) 'nı, kimlik avı taraması özelliğini devre dışı bırakmak için yapılandırabilir veya taramanın VPN kullanmasını engelleyebilirsiniz.

Android cihazınızın Intune 'a nasıl oluşturulduğuna bağlı olarak, aşağıdaki seçenekler kullanılabilir:

- Android Cihaz Yöneticisi-Web Koruması özelliğini devre dışı bırakmak veya taramalar sırasında yalnızca VPN 'lerin kullanımını devre dışı bırakmak için özel OMA-URI ayarlarını kullanın.
- Android kurumsal iş profili-tüm Web koruması yeteneklerini devre dışı bırakmak için bir uygulama yapılandırma profili ve yapılandırma Tasarımcısı kullanın.

<!-- ########################## -->
## <a name="week-of-june-15-2020--2006-service-release"></a>15 Haziran 2020 (2006 hizmet sürümü) haftası

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Uygulama yönetimi  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>Yönetilen uygulamalar için telekomünikasyon veri aktarımı koruması<!-- 6884491  -->
Korumalı bir uygulamada köprülü telefon numarası algılandığında, Intune, sayının bir çevirici uygulamasına aktarılmasını sağlayan bir koruma ilkesinin uygulanıp uygulanmadığı kontrol eder. İlke ile yönetilen bir uygulamadan başlatıldığında bu tür bir içerik aktarımını nasıl işleyebileceğini seçebilirsiniz. Microsoft Endpoint Manager 'da bir uygulama koruma ilkesi oluştururken, **Kuruluş verilerini diğer uygulamalara gönder**' den yönetilen bir uygulama seçeneği belirleyin ve ardından Iletişim **verilerini aktarma**seçeneğini belirleyin. Bu veri koruma ayarı hakkında daha fazla bilgi için, Microsoft Intune ve [iOS uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-ios.md) ['nda Android uygulama koruma ilkesi ayarları](../apps/app-protection-policy-settings-android.md) bölümüne bakın. 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---7414033----"></a>Windows Şirket Portalı Azure AD kurumsal ve Office Online uygulamalarının birleştirilmiş teslimi<!-- 7414033  -->
Intune 'un **Özelleştirme** bölmesinde Şirket portalı hem **Azure AD kurumsal uygulamalarını** hem de **Office Online uygulamalarını** **gizleme** veya **gösterme** seçeneğini belirleyebilirsiniz. Her Son Kullanıcı tüm uygulama kataloglarını seçilen Microsoft hizmetinden görürler. Varsayılan olarak, her bir ek uygulama kaynağı **gizleyecek**şekilde ayarlanır. Bu özellik ilk olarak Şirket Portalı Web sitesinde, izlenmesi beklenen Windows Şirket Portalı desteğiyle etkili olacaktır. Bu yapılandırma ayarını bulmak için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde **Kiracı Yönetimi**  >  **özelleştirmesi** ' nı seçin. İlgili bilgiler için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>MacOS kayıt deneyimi için Şirket Portalı geliştirmeleri<!-- 6444452  -->
MacOS kayıt deneyiminin Şirket Portalı, iOS kayıt deneyimi için Şirket Portalı daha yakından hizalanan daha basit bir kayıt işlemine sahiptir. Cihaz kullanıcıları şunları görür:  
- Bir uyleyici Kullanıcı arabirimi.  
- İyileştirilmiş bir kayıt denetim listesi.  
- Cihazlarını nasıl kaydedebileceğinize ilişkin daha net yönergeler.  
- Gelişmiş sorun giderme seçenekleri.  

Şirket Portalı hakkında daha fazla bilgi için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md).

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>İOS/ıpados ve macOS şirket portallarının cihazlar sayfasında geliştirmeler<!-- 6055001 -->
İOS/ıpados ve Mac kullanıcıları için uygulama deneyimini geliştirmek üzere Şirket Portalı **cihazları** sayfasında değişiklikler yaptık. Daha modern bir görünüm oluşturmaya ek olarak, kullanıcıların cihaz durumunu görebilmesi daha kolay olması için, tanımlı bölüm üst bilgilerine sahip tek bir sütun altındaki cihaz ayrıntılarını yeniden güncelleştirdik. Ayrıca, cihazları uyumsuz olan kullanıcılar için daha net mesajlaşma ve sorun giderme adımları ekledik. Şirket Portalı hakkında daha fazla bilgi için bkz. [Intune şirket portalı uygulamalar, Şirket portalı Web sitesi ve Intune uygulaması nasıl özelleştirilir](../apps/company-portal-app.md). Bir cihazı el ile eşitlemek için bkz. [iOS cihazınızı El Ile eşitleme](../user-help/sync-your-device-manually-ios.md).  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>İOS/ıpados Şirket Portalı uygulaması için bulut ayarı<!-- 7071303  -->
İOS/ıpados Şirket Portalı için yeni bir **bulut** ayarı, kullanıcıların kimlik doğrulamasını kuruluşunuz için uygun buluta yönlendirmelerini sağlar. Varsayılan olarak, ayar **Otomatik**olarak yapılandırılır, bu da kimlik doğrulaması otomatik olarak kullanıcının cihazı tarafından algılanır. Kuruluşunuzun kimlik doğrulaması otomatik olarak algılanan buluttan başka bir buluta yönlendirilmelidir (örneğin, kamu veya kamu), kullanıcılarınız > **Şirket portalı**Cloud **Settings** uygulamasını seçerek uygun bulutu el ile seçebilir  >  **Cloud**. Kullanıcılarınız yalnızca başka bir cihazdan oturum açtıklarında **bulut** ayarını **Otomatik** olarak değiştirmeli ve uygun bulut cihaz tarafından otomatik olarak algılanmaz. 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>Yinelenen Apple VPP belirteçleri<!-- 7101606  -->
Aynı **belirteç konumuna** sahıp Apple VPP belirteçleri artık **yinelenen** olarak işaretlenir ve yinelenen belirteç kaldırıldığında yeniden eşitlenebilir. Hala yinelenen olarak işaretlenmiş belirteçler için lisans atayabilir ve iptal edebilirsiniz. Ancak, bir belirteç yinelenen olarak işaretlendikten sonra satın alınan yeni uygulamalar ve Kitaplar için lisanslar yansıtılmayabilir. Kiracınız için Apple VPP belirteçlerini bulmak için, [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nden **kiracı yönetim**bağlayıcıları ' nı seçin  >  **ve**  >  **Apple VPP belirteçlerini**belirteçler yapın. VPP belirteçleri hakkında daha fazla bilgi için bkz. [Microsoft Intune ile Apple Volume Purchase program aracılığıyla satın alınan iOS ve macOS uygulamalarını yönetme](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Cihaz yapılandırması

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>MacOS cihazlarında Wi-Fi profillerindeki EAP-TLS kimlik doğrulaması için birden çok kök sertifika ekleme<!-- 2077871  -->

MacOS cihazlarında, bir Wi-Fi profili oluşturabilir ve Genişletilebilir Kimlik Doğrulama Protokolü (EAP) kimlik doğrulama türünü seçebilirsiniz (**cihaz**  >  **yapılandırma profilleri**for  >  **Create profile**  >  **macOS** platform > **Wi-> Fi** **Wi-Fi type** ' y i seçin.

EAP **türünü** **EAP-TLS**, **EAP-TTLS**veya **PEAP** kimlik doğrulaması olarak ayarladığınızda, birden çok kök sertifika ekleyebilirsiniz. Daha önce yalnızca bir kök sertifika ekleyebilirsiniz.

Yapılandırabileceğiniz ayarlar hakkında daha fazla bilgi için, bkz. [Microsoft Intune macOS cihazları Için Wi-Fi ayarları ekleme](../configuration/wi-fi-settings-macos.md).

Aşağıdakiler cihazlar için geçerlidir:
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>Windows 10 ve daha yeni cihazlarda Wi-Fi profilleriyle PKCS sertifikaları kullanma<!-- 3246388   -->
Windows Wi-Fi profillerinin kimlik doğrulaması için SCEP sertifikaları (**cihaz yapılandırma**  >  **profilleri**  >  **Create profile**  >  **Windows 10 ve üzeri** için profil oluşturma > **Wi-Fi** for platform > **Enterprise**  >  **EAP Type**). Şimdi, Windows Wi-Fi profilleriniz ile PKCS sertifikaları kullanabilirsiniz. Bu özellik, kiracınızdaki yeni veya mevcut PKCS sertifika profillerini kullanarak Wi-Fi profillerinin kimlik doğrulamasından geçmesini sağlar. 

Yapılandırabileceğiniz Wi-Fi ayarları hakkında daha fazla bilgi için, bkz. [Intune 'Da Windows 10 ve üzeri cihazlar Için Wi-Fi ayarları ekleme](../configuration/wi-fi-settings-windows.md).

Aşağıdakiler cihazlar için geçerlidir:
- Windows 10 ve üzeri

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>MacOS cihazları için kablolu ağ cihaz yapılandırma profilleri<!-- 3508686  -->
Kablolu ağları yapılandıran yeni bir MacOS cihaz yapılandırma profili vardır (**cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  platform için**MacOS profil oluşturma MacOS** for profile için **kablolu ağ** >). Kablolu ağları yönetmek için 802.1 x profilleri oluşturmak ve bu kablolu ağları macOS cihazlarınıza dağıtmak için bu özelliği kullanın.

Bu özellik hakkında daha fazla bilgi için bkz. [macOS cihazlarda kablolu ağlar](../configuration/wired-networks-configure.md).

Aşağıdakiler cihazlar için geçerlidir:
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>Tam olarak yönetilen Android Kurumsal cihazları için varsayılan başlatıcı olarak Microsoft başlatıcısı 'nı kullanın<!-- 4927976   -->
Android kurumsal cihaz sahibi cihazlarda, Microsoft başlatıcısı 'nı tam olarak yönetilen cihazlar için varsayılan başlatıcı olarak**ayarlayabilirsiniz (cihaz**  >  **yapılandırma profilleri**,  >  **Create profile**  >  **Android Enterprise** profil > **Device owner**  >  **cihaz deneyimi**için cihaz sahibi**cihaz kısıtlamalarına** >). Diğer tüm Microsoft Başlatıcı ayarlarını yapılandırmak için [uygulama yapılandırma ilkelerini](../apps/configure-microsoft-launcher.md)kullanın. 

Ayrıca, **cihaz deneyimine**yeniden adlandırılmakta olan **adanmış cihazlar** dahil bazı farklı Kullanıcı Arabirimi güncelleştirmeleri de vardır.

Kısıtlayabilecek tüm ayarları görmek için bkz. [Intune kullanarak özelliklere izin vermek veya erişimi kısıtlamak Için Android kurumsal cihaz ayarları](../configuration/device-restrictions-android-for-work.md). 

Aşağıdakiler cihazlar için geçerlidir:
- Android kurumsal cihaz sahibi tam olarak yönetilen cihazlar (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>İOS Şirket Portalı uygulamasını bir oturum açma/kapatma uygulaması olacak şekilde yapılandırmak için otonom tek uygulama modu ayarlarını kullanın<!-- 7055619   -->
İOS/ıpados cihazlarında, uygulamaları otonom tek uygulama modunda (ASAM) çalışacak şekilde yapılandırabilirsiniz. Artık Şirket Portalı uygulama ASAM 'yi destekliyor ve "oturum aç/oturumu Kapat" uygulaması olacak şekilde yapılandırılabilir. Bu modda, kullanıcıların cihazdaki diğer uygulamaları ve ana ekran düğmesini kullanabilmesi için Şirket Portalı uygulamada oturum açması gerekir. Şirket Portalı uygulamasında oturum açtıklarında, cihaz tek uygulama moduna geri döner ve Şirket Portalı uygulamasındaki kilitler.

Şirket portalı, Asam içinde olacak şekilde yapılandırmak için, bkz. **cihaz**  >  **yapılandırma profilleri**  >  **profil oluşturma**  >  **iOS/ıpados** , **tek uygulama modu**> profil için **cihaz kısıtlamaları > cihaz kısıtlamaları** .

Daha fazla bilgi için bkz. [otonom tek uygulama modu (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) ve [tek uygulama modu](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (Apple 'ın Web sitesini açar).

Aşağıdakiler cihazlar için geçerlidir:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>MacOS cihazlarında içerik önbelleğe almayı yapılandırma<!-- 7106872   -->
MacOS cihazlarında, içerik önbelleğe almayı yapılandıran bir yapılandırma profili**oluşturabilirsiniz (cihaz**  >  **yapılandırma profilleri**profil  >  için MacOS**profili oluşturma**  >  **MacOS** > for profile için **cihaz özellikleri** ). Önbelleği silmek, paylaşılan önbelleğe izin vermek, diskte önbellek sınırı ayarlamak ve daha fazlasını yapmak için bu ayarları kullanın.

İçerik önbelleğe alma hakkında daha fazla bilgi için bkz. [contentcaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (Apple 'ın Web sitesini açar).

Yapılandırabileceğiniz ayarları görmek için [Intune 'Da MacOS cihaz özelliği ayarları](../configuration/macos-device-features-settings.md)' na gidin.

Aşağıdakiler cihazlar için geçerlidir:
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Android Enterprise üzerinde OEMConfig kullanarak yeni şema ayarları ekleme ve mevcut şema ayarlarını arama<!-- 6394386   -->
Intune 'da, Android kurumsal cihazlarındaki ayarları yönetmek için oemconfig kullanabilirsiniz (**cihaz**  >  **yapılandırma profilleri**Intune için bir  >  **profil**  >  **Android Enterprise** for platform > **için bkz** .). **Yapılandırma tasarımcısını**kullandığınızda, uygulama şemasındaki özellikler gösterilir. Şimdi, **yapılandırma tasarımcısında**şunları yapabilirsiniz:

- Uygulama şemasına yeni ayarlar ekleyin.
- Uygulama şemasında yeni ve var olan ayarları arayın.

Intune 'daki OEMConfig profilleri hakkında daha fazla bilgi için, bkz. [Microsoft Intune 'de oemconfig Ile Android Kurumsal cihazları kullanma ve yönetme](../configuration/android-oem-configuration-overview.md).

Aşağıdakiler cihazlar için geçerlidir:
- Android Kurumsal

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>Paylaşılan iPad cihazlarda paylaşılan iPad geçici oturumlarını engelle<!-- 6613794  -->
Intune 'da, paylaşılan iPad cihazlarında geçici oturumları engelleyen, paylaşılan yeni bir **iPad geçici oturumları** ayarı**vardır (cihaz**  >  **yapılandırma profilleri**profil  >  **oluşturma**  >  **iOS/ıpados** > profil türü > **paylaşılan iPad**için **cihaz kısıtlamaları** ). Etkinleştirildiğinde, son kullanıcılar Konuk hesabını kullanamaz. Yönetilen Apple KIMLIĞI ve parolasıyla cihazda oturum açması gerekir. 

Daha fazla bilgi için bkz. [iOS ve ıpados cihaz ayarları, özelliklere izin vermek veya erişimi kısıtlamak](../configuration/device-restrictions-ios.md).

Aşağıdakiler cihazlar için geçerlidir:
- İOS/ıpados 13,4 ve daha yeni çalıştıran paylaşılan iPad cihazları

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Cihaz kaydı

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>Kendi cihazlarını getir, dağıtmak için VPN kullanabilir<!--5015344  -->
Yeni Autopilot profili **etki alanı bağlantısını atla onay** geçişi, üçüncü taraf Win32 VPN istemcinizi kullanarak kurumsal ağınıza erişim olmadan karma Azure AD JOIN cihazlarını dağıtmanıza olanak tanır. Yeni geçişi görmek için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**   >  **Windows**  >  **Windows kayıt**  >  **dağıtım profilleri**  >  **profil oluşturma**öncesi  >  **deneyim (OOBE)** bölümüne gidin.

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>Kayıt durumu sayfası profilleri, cihaz gruplarına ayarlanabilir<!--3952138 -->
Daha önce, kayıt durumu sayfası (ESP) profilleri yalnızca Kullanıcı gruplarını hedefleyebilir. Artık, bunları hedef cihaz gruplarına da ayarlayabilirsiniz. Daha fazla bilgi için bkz. [kayıt durumu sayfası ayarlama](../enrollment/windows-enrollment-status.md).

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Otomatik cihaz kaydı Eşitleme hataları<!-- 6988214 -->
İOS/ıpados ve macOS cihazları dahil olmak üzere yeni hatalar raporlanır
- Telefon numarasında geçersiz karakterler veya bu alan boş. 
- Profil için geçersiz veya boş yapılandırma adı. 
- Geçersiz/zaman aşımına uğradı imleç değeri veya imleç bulunamadı.
- Reddedilen veya süre dolma belirteci. 
- Departman alanı boş veya uzunluk çok uzun. 
- Profil Apple tarafından bulunmadı ve yeni bir tane oluşturulması gerekiyor. 
- Cihazların durumunu gördüğünüz genel bakış sayfasına, kaldırılan bir Apple Business Manager cihazı sayısı eklenecektir.

#### <a name="shared-ipads-for-business--6367326-----"></a>Iş için paylaşılan IPad 'ler<!--6367326   -->
Birden çok çalışanın cihaz paylaşabilmesi için, Intune ve Apple Business Manager 'ı kullanarak paylaşılan iPad 'i kolayca ve güvenli bir şekilde ayarlayabilirsiniz. Apple 'ın [paylaşılan iPad](https://developer.apple.com/education/shared-ipad/) 'i, Kullanıcı verilerini korurken birden çok kullanıcı için kişiselleştirilmiş bir deneyim sağlar. Yönetilen bir Apple KIMLIĞI kullanarak, kullanıcılar kuruluşlarındaki paylaşılan iPad 'de oturum açtıktan sonra uygulamalarına, verilerine ve ayarlarına erişebilirler. Paylaşılan iPad, Federasyon kimlikleriyle birlikte çalışmaktadır.

Bu özelliği görmek için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **iOS**  >  **iOS kaydı**  >  **kayıt programı belirteçleri**' ne gidin  >  **bir belirteç**  >  **profilleri**seçin  >  **iOS profili oluştur**  >  **iOS**. **Yönetim ayarları** sayfasında, **Kullanıcı benzeşimi olmadan kaydet** ' i seçin ve **paylaşılan iPad** seçeneğini görürsünüz.

Şunları gerektirir: ıpados 13,4 ve üzeri. Bu sürüm, kullanıcıların yönetilen bir Apple KIMLIĞI olmadan bir cihaza erişebilmeleri için paylaşılan iPad ile geçici oturumlar için destek ekledi. Oturum kapatma sonrasında cihaz tüm Kullanıcı verilerini siler, böylece cihaz kullanıma hemen kullanılabilir hale gelir ve cihaz temizleme gereksinimini ortadan kaldırır. 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Apple 'ın otomatik cihaz kaydı için güncelleştirilmiş Kullanıcı arabirimi<!--7430322 -->
Kullanıcı arabirimi Apple 'ın Aygıt Kayıt Programı Apple terminolojisini yansıtacak şekilde otomatik cihaz kaydına değiştirecek şekilde güncelleştirilmiştir.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Cihaz yönetimi

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>MacOS için cihaz uzaktan kilitleme PIN 'i kullanılabilir<!--7281557   -->
MacOS cihaz uzaktan kilitleme PIN 'lerinin kullanılabilirliği 7 günden 30 güne yükselmiştir.

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>Ortak yönetilen cihazlarda birincil kullanıcıyı değiştirme<!--7319183  -->
Bir cihazın birincil kullanıcısını, ortak yönetilen Windows cihazları için değiştirebilirsiniz. Bunu bulma ve değiştirme hakkında daha fazla bilgi için bkz. [Intune cihazının birincil kullanıcısını bulma](../remote-actions/find-primary-user.md). Bu özellik önümüzdeki birkaç hafta içinde kademeli olarak kullanıma sunulacaktır.

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Intune birincil kullanıcı ayarı da Azure AD Owner özelliğini ayarlar<!--7319227 -->
Bu yeni özellik, yeni kaydedilen karma Azure AD 'ye katılmış cihazlarda sahip özelliğini Intune birincil kullanıcısının ayarlandığı anda otomatik olarak ayarlar. Birincil Kullanıcı hakkında daha fazla bilgi için bkz. [Intune cihazının birincil kullanıcısını bulma](../remote-actions/find-primary-user.md).

Bu, kayıt işlemine yapılan bir değişiklik ve yalnızca yeni kaydedilen cihazlar için geçerlidir. Mevcut karma Azure AD 'ye katılmış cihazlar için Azure AD Owner özelliğini el ile güncelleştirmeniz gerekir. Bunu yapmak için [birincil Kullanıcı Değiştir özelliğini](../remote-actions/find-primary-user.md#change-a-devices-primary-user) veya [bir komut dosyasını](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)kullanabilirsiniz.

Windows 10 cihazları karma Azure Azure dizini 'ne katıldığında, cihazın ilk kullanıcısı Endpoint Manager 'da birincil Kullanıcı olur.  Şu anda Kullanıcı ilgili Azure AD cihaz nesnesinde ayarlanmadı. Bu, *sahip* özelliğini Microsoft Endpoint Manager Yönetim Merkezi 'ndeki *birincil Kullanıcı* ÖZELLIĞI ile bir Azure AD portalından karşılaştırırken tutarsızlığa neden olur. Azure AD Owner özelliği, BitLocker Kurtarma anahtarlarına erişimin güvenliğini sağlamak için kullanılır. Özelliği, karma Azure AD 'ye katılmış cihazlarda doldurulmamış. Bu sınırlama, Azure AD 'den BitLocker kurtarma 'nın self servis kurulumunu engeller. Yakında sunulacak olan bu özellik bu kısıtlamayı çözer.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Cihaz güvenliği

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>MacOS cihazları için dosya Kasası 2 şifrelemesi sırasında, kurtarma anahtarını kullanıcılardan gizle<!-- 5459801  -->
[MacOS Endpoint Protection](../protect/endpoint-protection-macos.md#filevault) şablonu Içindeki *filekasası* kategorisine yeni bir ayar ekledik: **Kurtarma anahtarını gizleyin**. Bu ayar, Filekasa2 şifrelemesi sırasında son kullanıcıdan kişisel anahtarı gizler. 

Şifrelenmiş bir macOS cihazının kişisel kurtarma anahtarını görüntülemek için, cihaz kullanıcısı aşağıdaki konumlardan birine gidebilir ve macOS cihazı için *Kurtarma anahtarını al* ' a tıklayabilirsiniz: 

- İOS/ıpados Şirket portalı uygulaması
- Intune uygulaması
- Şirket portalı web sitesi
- Android şirket portalı uygulaması

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Android 'de tam olarak yönetilen ve Outlook ile S/MIME imzalama ve şifreleme sertifikaları desteği<!--5896415   -->
Artık Android kurumsal tam olarak yönetilen cihazlarda Outlook ile S/MIME imzalama ve şifreleme için sertifikaları kullanabilirsiniz.

Bu, diğer Android sürümleri (Android 'de Outlook ile S/MIME imzalama ve şifreleme sertifikaları desteği) için geçen aya eklenen desteğe genişletilir. Bu sertifikaları SCEP ve PKCS içeri aktarılan sertifika profillerini kullanarak sağlayabilirsiniz.

Bu destek hakkında daha fazla bilgi için Exchange belgelerindeki [iOS ve Android Için Outlook 'Ta duyarlılık etiketleme ve koruma](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) bölümüne bakın.

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Uyumsuzluk için e-postalara Şirket Portalı Destek Web sitenizin bağlantısını ekleyin<!-- 7225498    -->
Uyumsuzluk için e-posta bildirimleri göndermek üzere [bir bildirim iletisi şablonu yapılandırdığınızda](../protect/actions-for-noncompliance.md#create-a-notification-message-template) , Şirket portalı Web sitenizin bağlantısını otomatik olarak eklemek için yeni ayar **Şirket portalı Web sitesi bağlantısını** kullanın. Bu seçenek *etkin*olarak ayarlandığında, bu şablona dayalı e-posta alan uyumlu olmayan cihazlara sahip kullanıcılar, cihazlarının neden uyumlu olmadığı hakkında daha fazla bilgi edinmek için bir Web sitesi açmak üzere bağlantıyı kullanabilir. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>Lisanslama

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>Yöneticiler artık Microsoft Endpoint Manager Yönetici konsoluna erişmek için bir Intune lisansı gerektirmez<!--1335430 -->
Artık, yöneticilerin MEM Yönetici Konsolu ve sorgu grafiği API 'Lerine erişmesi için Intune lisans gereksinimini kaldıran kiracı genelinde bir geçiş ayarlayabilirsiniz. Lisans gereksinimini kaldırdıktan sonra, bunu hiçbir şekilde yeniden devreye sokmanız gerekir. 


> [!Note]
> TeamViewer Bağlayıcısı akışı dahil bazı eylemler, yine de bir Intune lisansının tamamlanmasını gerektirir.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>Betikler 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>MacOS cihazlarında kabuk betiklerinin kullanılabilirliği<!-- 7134839  -->
MacOS cihazları için kabuk betikleri artık kamu bulutu ve Çin müşterileri tarafından kullanılabilir. Kabuk betikleri hakkında daha fazla bilgi için bkz. [Intune 'Da macOS cihazlarında Shell betikleri kullanma](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>8 Haziran 2020 haftası   

### <a name="app-management"></a>Uygulama yönetimi  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>İOS/ıpados için Şirket Portalı bilgi ekranı güncelleştirmeleri <!--7032452 -->
İOS/ıpados için Şirket Portalı bir bilgilendirici ekran, yöneticinin cihazları neleri görebileceğini ve ne yapabileceğini daha iyi açıklamak için güncelleştirilmiştir. Bu açıklamalar yalnızca şirkete ait cihazlar içindir. Yalnızca metin güncelleştirildi, yöneticinin Kullanıcı cihazlarını neleri görebileceklerini veya yapabileceğini hiçbir gerçek değişiklik yapılmadı. Güncelleştirilmiş ekranları görmek için [Intune son kullanıcı uygulamaları Için Kullanıcı Arabirimi güncelleştirmeleri](./whats-new-app-ui.md)' ne gidin.

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Güncelleştirilmiş Android UYGULAMASı koşullu başlatma Son Kullanıcı deneyimi<!-- 5736084 -->
Android Şirket Portalı 2006 sürümünde, 2005 sürümündeki güncelleştirmelerde derleme yapan değişiklikler vardır. 2005 ' de, bir uygulama koruma ilkesi tarafından uyarı veren, blok veya temizleme yapan son Android cihaz kullanıcılarının, uyarı, blok veya silme nedeninizi ve sorunları düzeltmek için gereken adımları açıklayan bir tam sayfa mesajı görürsünüz. 2006 ' de, uygulama erişiminin engellenmesine neden olan sorunları düzeltmek için bir uygulama koruma ilkesi atanan Android uygulamalarının ilk kullanıcıları, kılavuzlu bir akış aracılığıyla alınacaktır. 



## <a name="whats-new-archive"></a>Yenilikler arşivi
Önceki aylar için bkz. yenilikler [Arşivi](whats-new-archive.md).

## <a name="notices"></a>Bildirimler

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
