---
title: Microsoft Intune - Azure’da cihaz profilleri oluşturma | Microsoft Docs
description: Microsoft Intune’da cihaz yapılandırma profili ekleyin veya yapılandırın. Platform türünü seçin, ayarları yapılandırın, bir kapsam etiketi ekleyin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c2031ba23b49bda4890d2638272e3b808b4bf5a9
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327445"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>Microsoft Intune’da cihaz profili oluşturma

Cihaz profillerini kullanarak ayar ekleyip yapılandırabilir ve daha sonra bu ayarları kuruluşunuzdaki cihazlara gönderebilirsiniz. [Cihaz profillerini kullanarak cihazlarınıza özellik ve ayar uygulama](device-profiles.md) sayfasında yapabileceğiniz işlemlerle ilgili ayrıntılı bilgilere yer verilmiştir.

Bu makalede:

- Profil oluşturma adımları listelenmiştir.
- Profili "filtrelemek" için kapsam etiketi ekleme adımları gösterilmektedir.
- Windows 10 cihazlarında uygulanabilirlik kurallarını açıklar ve bir kuralın nasıl oluşturulacağını gösterir.
- Cihazların profilleri ve profil güncelleştirmelerini aldığı iade yenileme döngüsü süreleri listelenmiştir.

## <a name="create-the-profile"></a>Profili oluşturma

Profiller, [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oluşturulur. Bu yönetim merkezinde **cihazlar**' ı seçin. Şu seçenekleriniz vardır:

- **Genel bakış**: profillerinizin durumunu listeler ve kullanıcılara ve cihazlara atadığınız profiller hakkında ek ayrıntılar sağlar.
- **İzleyici**: başarılı veya başarısız için profillerinizin durumunu denetleyin ve ayrıca profilinizde günlükleri görüntüleyin.
- **Platforma göre**: platformunuz için ilkeler ve Profiller oluşturun ve görüntüleyin. Bu görünüm, platforma özgü özellikleri de gösterebilir. Örneğin, **Windows**' u seçin. **Windows 10 güncelleştirme halkaları** ve **PowerShell betikleri**gibi Windows 'a özgü özellikler görürsünüz.
- **İlke**: cihaz profilleri oluşturun, cihazlarda çalıştırmak Için özel [PowerShell betikleri](../apps/intune-management-extension.md) yükleyin ve [esım](esim-device-configuration.md)kullanarak cihazlara veri planları ekleyin.

Bir profil oluşturduğunuzda ( **profil oluşturma** > **yapılandırma profilleri** ), platformunuzu seçin:

- **Android Cihaz Yöneticisi**
- **Android Kurumsal**
- **iOS/ıpados**
- **macOS**
- **Windows 10 ve üzeri**
- **Windows 8.1 ve üzeri**
- **Windows Phone 8.1**

Ardından profil türünü seçin. Seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklılık gösterir. Aşağıdaki makaleler farklı profil türleri için ayarları anlatmaktadır:

- [Yönetim Şablonları (Windows)](administrative-templates-windows.md)
- [Özel](custom-settings-configure.md)
- [Teslim iyileştirme (Windows)](delivery-optimization-windows.md)
- [Türetilmiş kimlik bilgileri (Android Enterprise, iOS, ıpados)](../protect/derived-credentials.md)
- [Cihaz özellikleri (macOS, iOS, ıpados)](device-features-configure.md)
- [Cihaz üretici yazılımı (Windows)](device-firmware-configuration-interface-windows.md)
- [Cihaz kısıtlamaları](device-restrictions-configure.md)
- [Etki alanına ekleme (Windows)](domain-join-configure.md)
- [Sürüm yükseltme ve mod anahtarı (Windows)](edition-upgrade-configure-windows-10.md)
- [Eğitim (iOS, ıpados)](../fundamentals/education-settings-configure-ios.md)
- [E-posta](email-settings-configure.md)
- [Endpoint Protection (macOS, Windows)](../protect/endpoint-protection-configure.md)
- [Uzantılar (macOS)](kernel-extensions-overview-macos.md)
- [Kimlik koruması (Windows)](../protect/identity-protection-configure.md)
- [Bilgi noktası](kiosk-settings.md)
- [Microsoft Defender ATP (Windows)](../protect/advanced-threat-protection.md)
- [Mobility uzantıları (MX) profili (Android Cihaz Yöneticisi)](android-zebra-mx-overview.md)
- [OEMConfig (Android kurumsal)](android-oem-configuration-overview.md)
- [PKCS sertifikası](../protect/certficates-pfx-configure.md)
- [PKCS içeri aktarılan sertifika](../protect/certificates-imported-pfx-configure.md)
- [Tercih dosyası (macOS)](preference-file-settings-macos.md)
- [SCEP sertifikası](../protect/certificates-scep-configure.md)
- [Güvenli değerlendirme (eğitim) (Windows)](education-settings-configure.md)
- [Paylaşılan çok kullanıcılı cihaz (Windows)](shared-user-device-settings.md)
- [Telekom giderleri (Android Cihaz Yöneticisi, iOS, ıpados)](telecom-expenses-monitor.md)
- [Güvenilir sertifika](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)

Örneğin, platform için **iOS/ıpados** ' ı seçerseniz, profil türü seçenekleriniz aşağıdaki profile benzer şekilde görünür:

> [!div class="mx-imgBorder"]
> Intune 'da iOS/ıpados profili oluşturma ![](./media/device-profile-create/create-device-profile.png)

## <a name="scope-tags"></a>Kapsam etiketleri

Profilinize ayar ekledikten sonra bir kapsam etiketi de ekleyebilirsiniz. Kapsam etiketleri, `US-NC IT Team` veya `JohnGlenn_ITDepartment`gibi belirli BT gruplarına filtre sağlar. Ve, dağıtıldığı için kullanılır.

Kapsam etiketleri ve yapabilecekleriniz hakkında daha fazla bilgi için bkz. [Dağıtılmış BT için RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

## <a name="applicability-rules"></a>Uygulanabilirlik kuralları

Uygulama alanı:

- Windows 10 ve üzeri

Uygulanabilirlik kuralları, yöneticilerin belirli ölçütlere uyan bir gruptaki cihazları hedeflemesini sağlar. Örneğin, **tüm Windows 10 cihazları** grubuna uygulanan bir cihaz kısıtlama profili oluşturursunuz. Ancak, profili yalnızca Windows 10 Enterprise çalıştıran cihazlara atanmasını istersiniz.

Bu görevi yapmak için bir **uygulanabilirlik kuralı**oluşturun. Bu kurallar aşağıdaki senaryolar için uygundur:

- Windows 10 eğitim (EDU) kullanıyorsunuz. Bellows üniversite 'de, tüm Windows 10 EDU cihazlarını RS3 ve RS4 arasında hedeflemek istiyorsunuz.
- Contoso 'daki Insan kaynakları ' nda tüm kullanıcıları hedeflemek istiyorsunuz, ancak yalnızca Windows 10 Professional veya Kurumsal cihazları istiyorum.

Bu senaryolara yaklaşımak için şunları yapın:

- Bellows üniversite 'deki tüm cihazları içeren bir cihaz grubu oluşturun. Profilde, işletim sistemi en düşük sürümü `16299` ve en yüksek sürüm `17134`, bu nedenle uygulanacak bir uygulanabilirlik kuralı ekleyin. Bu profili Bellows okul cihazları grubuna atayın.

  Atandığında profil, girdiğiniz en düşük ve en yüksek sürüm arasındaki cihazlara uygulanır. Girdiğiniz en düşük ve en yüksek sürümler arasında olmayan cihazlarda, durumları **geçerli değil**olarak gösterilir.

- Contoso 'da Insan kaynakları (HR) içindeki tüm kullanıcıları içeren bir Kullanıcı grubu oluşturun. Profilde, Windows 10 Professional veya Enterprise çalıştıran cihazlara uygulanacak bir uygulanabilirlik kuralı ekleyin. Bu profili HR kullanıcıları grubuna atayın.

  Atandığında, profil Windows 10 Professional veya Enterprise çalıştıran cihazlara uygulanır. Bu sürümleri çalıştırmayan cihazlarda, durumları **geçerli değil**olarak gösterilir.

- Tam olarak aynı ayarlara sahip iki profil varsa, bir uygulanabilirlik kuralı olmayan profil uygulanır. 

  Örneğin, ProfileA, Windows 10 cihazlar grubunu hedefler, BitLocker 'ı etkinleştirmez ve bir uygulanabilirlik kuralına sahip değildir. ProfileB aynı Windows 10 cihazları grubunu hedefler, BitLocker 'ı sağlar ve profili yalnızca Windows 10 Enterprise 'a uygulamak için bir uygulanabilirlik kuralına sahiptir.

  Her iki profil atandığında, bir uygulanabilirlik kuralına sahip olmadığından ProfileA uygulanır. 

Profili gruplara atadığınızda, uygulanabilirlik kuralları bir filtre işlevi görür ve yalnızca ölçütlerinizi karşılayan cihazları hedefleyin.

### <a name="add-a-rule"></a>Kural ekleme

1. **Uygulanabilirlik kuralları**' nı seçin. **Kural**, **özellik**ve **işletim sistemi sürümünü**seçebilirsiniz:

    > [!div class="mx-imgBorder"]
    > Microsoft Intune](./media/device-profile-create/applicability-rules.png) cihaz yapılandırma profiline uygulanabilirlik kuralı ekleme ![

2. **Kuralda**, kullanıcıları veya grupları dahil etmek veya dışlamak istediğinizi seçin. Seçenekleriniz şunlardır:

    - **Profil ata**: girdiğiniz ölçütlere uyan kullanıcıları veya grupları içerir.
    - Şu **durumlarda profil atamayın**: girdiğiniz ölçütlere uyan kullanıcıları veya grupları dışlar.

3. **Özellik**' de filtrenizi seçin. Seçenekleriniz şunlardır: 

    - **Işletim sistemi sürümü**: listede, kuralınıza dahil etmek istediğiniz Windows 10 sürümlerini (veya hariç tutmak) denetleyin.
    - **Işletim sistemi sürümü**: kuralınıza dahil etmek (veya dışlamak) istediğiniz **En düşük** ve **en yüksek** Windows 10 sürüm numaralarını girin. Her iki değer de gereklidir.

      Örneğin, en yüksek sürüm için en düşük sürüm ve `10.0.17134.0` (RS4 veya 1803) için `10.0.16299.0` (RS3 veya 1709) girebilirsiniz. Ya da daha ayrıntılı olabilir ve en yüksek sürüm için en düşük sürüm ve `10.0.17134.319` `10.0.16299.001` girebilirsiniz.

4. Değişikliklerinizi kaydetmek için **Ekle** ' yi seçin.

## <a name="refresh-cycle-times"></a>Yenileme döngü süreleri

Intune, yapılandırma profillerinin güncelleştirmelerini denetlemek için farklı yenileme döngüleri kullanır. Cihaz yakın zamanda kaydedildiyse, iade etme daha sık çalışır. [İlke ve profil yenileme döngüleri](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) tahmini yenileme zamanlarını listeler.

Kullanıcılar profil güncelleştirmelerini istedikleri zaman denetlemek için Şirket Portalı uygulamasını açıp cihazı eşitleyebilir.

## <a name="recommendations"></a>Öneriler

Profiller oluştururken aşağıdaki önerileri göz önünde bulundurun:

- İlkelerine ne olduğunu ve ne yaptığını bilmek için ilkelerinizi adlandırın. Tüm [uyumluluk ilkeleri](../protect/create-compliance-policy.md) ve [yapılandırma profillerinin](../configuration/device-profile-create.md) isteğe bağlı bir **Açıklama** özelliği vardır. **Açıklama**' da, özel olarak, diğerlerinin ilkenin ne yaptığını bilmesi için bilgi ekleyin.

  Bazı yapılandırma profili örnekleri şunları içerir:

  **Profil adı**: yönetici şablonu-tüm Windows 10 kullanıcıları için OneDrive yapılandırma profili  
  **Profil açıklaması**: tüm Windows 10 kullanıcıları için en düşük ve temel ayarları içeren OneDrive yönetici şablonu profili. Kullanıcıların kurumsal verileri kişisel OneDrive hesaplarına paylaşmasını engellemek için user@contoso.com tarafından oluşturulur.

  **Profil adı**: Tüm IOS/ıpados kullanıcıları için VPN profili  
  **Profil açıklaması**: contoso VPN 'ye bağlanacak tüm IOS/ıpados kullanıcıları için en düşük ve temel ayarları içeren VPN profili. Kullanıcıların Kullanıcı adı ve parola istemek yerine VPN 'de otomatik olarak kimlik doğrulaması yaptığı için user@contoso.com tarafından oluşturulur.

- Microsoft Edge ayarlarını yapılandırma, Microsoft Defender Anti-Virus ayarlarını etkinleştirme, iOS/ıpados jailbreak uygulanmış cihazlarını engelleme vb. gibi görevine göre profilinizi oluşturun.

- Pazarlama, satış, BT yöneticileri veya konuma veya okul sistemine göre belirli gruplar için uygulanan Profiller oluşturun.

- Kullanıcı ilkelerini cihaz ilkelerinden ayırın.

  Örneğin, [Intune 'da Yönetim Şablonları](administrative-templates-windows.md) yüzlerce ADMX ayarı vardır. Bu şablonlar, bir ayarın kullanıcılara veya cihazlara uygulanacağını gösterir. Yönetici şablonları oluştururken, kullanıcı ayarlarınızı bir kullanıcılar grubuna atayın ve cihaz ayarlarınızı bir cihaz grubuna atayın.

  Aşağıdaki görüntüde kullanıcılara uygulanabilecek ve/veya cihazlara uygulanabilecek bir ayarın örneği gösterilmektedir:

  > [!div class="mx-imgBorder"]
  > Kullanıcı ve cihazlara uygulanan ![Intune yönetici şablonu](./media/device-profile-create/setting-applies-to-user-and-device.png)

- Her kısıtlayıcı ilke oluşturduğunuzda, bu değişikliği kullanıcılarınıza iletişim kurun. Örneğin, geçiş kodu gereksinimini 4 karakterden 6 karaktere değiştiriyorsanız, ilke atamadan önce kullanıcılarınızın bunu bilmesini sağlayın.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).
