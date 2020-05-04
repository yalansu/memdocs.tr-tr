---
title: Intune ile Zimperium MTD bağlayıcısı
titleSuffix: Intune on Azure
description: Şirket kaynaklarınıza mobil cihaz erişimini kontrol etmek için Zimperium Mobile Threat Defense’i Intune ile tümleştirme hakkında bilgi edinin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed623abeb602e599866af7b7249756edd87d5a29
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79328438"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Intune ile Zimperium Mobile Threat Defense bağlayıcısı

Microsoft Intune ile tümleştirilen bir Mobile Threat Defense (MTD) çözümü olan Zemium tarafından gerçekleştirilen risk değerlendirmesine dayalı koşullu erişimi kullanarak mobil cihaz erişimini kontrol edebilirsiniz. Risk, Zimperium uygulamasını çalıştıran cihazlardan toplanan telemetriye göre değerlendirilir.

Kayıtlı cihazlar için Intune cihaz uyumluluk ilkeleri aracılığıyla etkinleştirilen, uyumsuz cihazların, algılanan tehditlere dayalı olarak şirket kaynaklarına erişmesine izin vermek veya erişimi engellemek için kullanabileceğiniz, bulunan Zzium risk değerlendirmesi temelinde koşullu erişim ilkelerini yapılandırabilirsiniz. Kayıtlı olmayan cihazlar için, algılanan tehditlere dayalı olarak bir blok veya seçmeli Temizleme zorlamak için uygulama koruma ilkelerini kullanabilirsiniz.

## <a name="supported-platforms"></a>Desteklenen platformlar

- **Android 4.1 ve üzeri**

- **iOS 8 ve üzeri**

## <a name="prerequisites"></a>Önkoşullar

- Azure Active Directory Premium

- Microsoft Intune aboneliği

- Zimperium Mobile Threat Defense aboneliği

  - Daha fazla bilgi için bkz. [Zkusurium Web sitesi](https://www.zimperium.com/zips-mobile-ips).

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Intune ve Zimperium şirket kaynaklarınızın korunmasına nasıl yardımcı olur?

Android ve iOS/ıpados için Zanium uygulaması dosya sistemi, ağ yığını, cihaz ve kullanılabilir olduğunda uygulama telemetrisini yakalar ve mobil tehditlere karşı cihazın riskini değerlendirmek için telemetri verilerini Zıium bulut hizmetine gönderir.

- **Kayıtlı cihazlar Için destek** -Intune cihaz uyumluluk Ilkesi, Zmıium 'ten risk değerlendirmesi bilgilerini kullanabileceğiniz bir mobil tehdit savunması (MTD) için bir kural içerir. MTD kuralı etkinleştirildiğinde, Intune, etkin olan ilkeyle cihaz uyumluluğunu değerlendirir. Cihaz uyumsuz bulunursa kullanıcıların Exchange Online ve SharePoint Online gibi kurumsal kaynaklara erişimi engellenir. Kullanıcılar ayrıca, sorunu çözmek ve kurumsal kaynaklara yeniden erişim kazanmak için cihazlarında yüklü olan Zimperium uygulamasından yönergeler alır. Kayıtlı cihazlarla Zkusurium kullanımını desteklemek için:
  - [Cihazlara MTD uygulamaları ekleme](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [MTD 'yi destekleyen bir cihaz uyumluluk ilkesi oluşturma](../protect/mtd-device-compliance-policy-create.md)
  - [Intune'da MTD bağlayıcısını etkinleştirme](../protect/mtd-connector-enable.md)

- **Kayıtlı olmayan cihazlar Için destek** -Intune, Intune uygulama koruma ilkelerini kullandığınızda, kayıtlı olmayan cihazlarda zboyutlu en yüksek uygulamadaki risk değerlendirmesi verilerini kullanabilir. Yöneticiler bu bileşimi, [Microsoft Intune korunan bir uygulamadaki](../apps/apps-supported-intune-apps.md)kurumsal verilerin korunmasına yardımcı olmak için kullanabilir. Yöneticiler, kayıtlı olmayan cihazlarda Kurumsal veriler için bir blok veya seçmeli silme de verebilir. Kayıtlı olmayan cihazlarla Zkusurium kullanımını desteklemek için:
  - [MTD uygulamasını kayıtlı olmayan cihazlara ekleme](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Mobile Threat Defense uygulama koruma ilkesi oluşturma](../protect/mtd-app-protection-policy.md)
  - [Kayıtlı olmayan cihazlar için Intune 'da MTD bağlayıcısını etkinleştirme](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>Örnek senaryolar

Aşağıda Zimperium ile Intune tümleştirmesi için birkaç senaryo bulabilirsiniz:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kötü amaçlı uygulamalardan kaynaklanan tehditlere dayalı olarak erişimi denetleme

Cihazlarda kötü amaçlı yazılım gibi kötü amaçlı uygulamalar algılandığında, tehdit çözülene kadar cihazları engelleyebilirsiniz:

- Şirket e-postasına bağlanma

- OneDrive İş uygulaması ile şirket dosyalarını eşitleme

- Şirket uygulamalarına erişme

*Kötü amaçlı yazılımlar algılandığında engelleme:*

> [!div class="mx-imgBorder"]
> ![Algılanan kötü amaçlı uygulamaların kavramsal görüntüsü](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> ![Düzeltmeden sonra erişim izni verilen kavramsal resim](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak erişimi denetleme

Ağda **bağlantıyı izinsiz izleme** gibi tehditleri algılayın ve cihaz riskine dayalı olarak Wi-Fi ağlarına erişimi koruyun.

*Wi-Fi üzerinden ağ erişimini engelleme:*

> [!div class="mx-imgBorder"]
> ![Wi-Fi üzerinden ağ erişimini engelleyin](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> ![Düzeltmeye erişim verildi](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak SharePoint Online’a erişimi denetleme

Ağda **Bağlantıyı izinsiz izleme** gibi tehditleri algılar ve cihaz riskine dayalı olarak kurumsal dosyaların eşitlenmesini engeller.

*Ağ tehditleri algılandığında SharePoint Online 'ı engelleyin:*

> [!div class="mx-imgBorder"]
> ![Ağ tehditleri algılandığında SharePoint Online’ı engelleme](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> ![Sharepoint için düzeltme ile erişim izni verme örneği](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Kötü amaçlı uygulamalardaki tehditleri temel alan kayıtlı olmayan cihazlarda erişimi denetleme

Zyium Mobile Threat Defense çözümü, bir cihazı bulaşma için kabul eder:

> [!div class="mx-imgBorder"]
> ![Algılanan kötü amaçlı yazılım nedeniyle uygulama koruma ilkesi blokları](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

Düzeltmeye erişim verildi:

> [!div class="mx-imgBorder"]
> ![Uygulama koruma ilkesi düzeltilmek için erişim izni verildi](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Sonraki adımlar

- [Zimperium'u Intune ile tümleştirme](zimperium-mtd-connector-integration.md)

- [Zimperium uygulamalarını ayarlama](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Zimperium cihaz uyumluluk ilkesi oluşturma](mtd-device-compliance-policy-create.md)

- [Zimperium MTD bağlayıcısını etkinleştirme](mtd-connector-enable.md)

- [MTD uygulaması koruma ilkesi oluşturma](../protect/mtd-app-protection-policy.md)
