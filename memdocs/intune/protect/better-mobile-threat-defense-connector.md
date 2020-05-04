---
title: Intune ile Better Mobile Threat Defense bağlayıcısı
titleSuffix: Intune on Azure
description: Intune ile Better Mobile Threat Defense bağlayıcısını ayarlayın.
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
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329910"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Intune ile Better Mobile Threat Defense bağlayıcısı

Microsoft Intune ile tümleştirilen Mobile Threat Defense (MTD) çözümü daha Iyi mobil tarafından gerçekleştirilen risk değerlendirmesine dayalı koşullu erişimi kullanarak mobil cihaz erişimini kontrol edebilirsiniz. Risk, Better Mobile uygulamasını çalıştıran cihazlardan toplanan telemetriye göre değerlendirilir.

Kayıtlı cihazlar için Intune cihaz uyumluluk ilkeleri aracılığıyla etkinleştirilen ve uyumlu olmayan cihazların, algılanan tehditlere dayalı olarak şirket kaynaklarına erişmesine izin vermek veya erişimi engellemek için kullanabileceğiniz daha Iyi mobil risk değerlendirmesi temelinde koşullu erişim ilkelerini yapılandırabilirsiniz. Kayıtlı olmayan cihazlar için, algılanan tehditlere dayalı olarak bir blok veya seçmeli Temizleme zorlamak için uygulama koruma ilkelerini kullanabilirsiniz.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Intune ve Better Mobile şirket kaynaklarınızın korunmasına nasıl yardımcı olur?

Better Mobile uygulaması mobil cihazlara yüklenir ve mobil cihazlarda çalışır. Bu uygulama varsa dosya sistemi, ağ yığını, cihaz ve uygulama telemetrisini yakalar ve mobil tehditlere karşı cihazın riskini değerlendirmek için verileri Better Mobile bulut hizmetine gönderir.

- **Kayıtlı cihazlar Için destek** -Intune cihaz uyumluluk Ilkesi, Mobile Threat Defense (MTD) Için daha iyi mobil 'ten risk değerlendirmesi bilgilerini kullanabileceğiniz bir kural içerir. MTD kuralı etkinleştirildiğinde, Intune, etkin olan ilkeyle cihaz uyumluluğunu değerlendirir. Cihaz uyumsuz bulunursa kullanıcıların Exchange Online ve SharePoint Online gibi kurumsal kaynaklara erişimi engellenir. Kullanıcılar ayrıca, sorunu çözmek ve kurumsal kaynaklara yeniden erişim kazanmak için cihazlarında yüklü olan Better Mobile uygulamasından yönergeler alır. Kayıtlı cihazlarla daha Iyi mobil kullanımı desteklemek için:
  - [Cihazlara MTD uygulamaları ekleme](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [MTD 'yi destekleyen bir cihaz uyumluluk ilkesi oluşturma](../protect/mtd-device-compliance-policy-create.md)
  - [Intune'da MTD bağlayıcısını etkinleştirme](../protect/mtd-connector-enable.md)

- **Kayıtlı olmayan cihazlar Için destek** -Intune, Intune uygulama koruma ilkeleri kullandığınızda kayıtlı olmayan cihazlarda daha iyi mobil uygulamadaki risk değerlendirmesi verilerini kullanabilir. Yöneticiler bu bileşimi, [Microsoft Intune korunan bir uygulamadaki](../apps/apps-supported-intune-apps.md)kurumsal verilerin korunmasına yardımcı olmak için kullanabilir. Yöneticiler, kayıtlı olmayan cihazlarda Kurumsal veriler için bir blok veya seçmeli silme de verebilir. Kayıtlı olmayan cihazlarla daha Iyi mobil kullanımı desteklemek için:
  - [MTD uygulamasını kayıtlı olmayan cihazlara ekleme](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Mobile Threat Defense uygulama koruma ilkesi oluşturma](../protect/mtd-app-protection-policy.md)
  - [Kayıtlı olmayan cihazlar için Intune 'da MTD bağlayıcısını etkinleştirme](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Desteklenen platformlar

- **Android 4.1 ve üzeri**

- **iOS 8,0 ve üzeri**

## <a name="prerequisites"></a>Önkoşullar

- Azure Active Directory Premium

- Microsoft Intune aboneliği

- Better Mobile Threat Defense aboneliği

  - Daha fazla bilgi için [Better Mobile web sitesine](https://www.better.mobi/) bakın.

## <a name="sample-scenarios"></a>Örnek senaryolar

Burada sık karşılaşılan bazı senaryolar verilmiştir.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kötü amaçlı uygulamalardan kaynaklanan tehditlere dayalı olarak erişimi denetleme

Cihazlarda kötü amaçlı yazılım gibi kötü amaçlı uygulamalar algılandığında, tehdit çözülene kadar cihazların aşağıdaki eylemleri gerçekleştirmesini engelleyebilirsiniz:

- Şirket e-postasına bağlanma

- OneDrive İş uygulaması ile şirket dosyalarını eşitleme

- Şirket uygulamalarına erişme

Kötü amaçlı yazılımlar algılandığında engelleme:

![Algılanan kötü amaçlı uygulamaları gösteren resim](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

Düzeltmeye erişim verildi:

![Kötü amaçlı uygulamalar algılandı erişim izni verildi](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak erişimi denetleme

**Bağlantıyı izinsiz izleme** saldırıları gibi ağınıza yönelik tehditleri algılayın ve cihaz riskine dayalı olarak Wi-Fi ağlarına erişimi koruyun.

Wi-Fi üzerinden ağ erişimini engelleme:

![Wi-Fi üzerinden ağ erişimini engelleme](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

Düzeltmeye erişim verildi:

![Düzeltilmekte olan erişimi gösteren resim](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak SharePoint Online’a erişimi denetleme

**Bağlantıyı izinsiz izleme** saldırıları gibi ağınıza yönelik tehditleri algılayın ve cihaz riskine dayalı olarak kurumsal dosyaların eşitlenmesini engelleyin.

Ağ tehditleri algılandığında SharePoint Online 'ı engelleyin:

![Ağ tehditleri algılandığında SharePoint Online’ı engelleme](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Düzeltme ile erişim izni verildi:

![Sharepoint için düzeltme ile erişim izni verme örneği](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Kötü amaçlı uygulamalardaki tehditleri temel alan kayıtlı olmayan cihazlarda erişimi denetleme

DAHA ıyı bir mobil tehdit savunması çözümü, bir cihazı bulaşma olarak düşünür: ![algılanan kötü amaçlı yazılım nedeniyle uygulama koruma ilkesi blokları](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

Düzeltmeye erişim verildi:

![Uygulama koruma ilkesi düzeltilmek için erişim izni verildi](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Sonraki adımlar

- [Better Mobile'ı Intune ile tümleştirme](better-mobile-mtd-connector-integration.md)

- [Better Mobile uygulamalarını ayarlama](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Better Mobile cihaz uyumluluk ilkesi oluşturma](mtd-device-compliance-policy-create.md)

- [Better Mobile MTD bağlayıcısını etkinleştirme](mtd-connector-enable.md)

- [MTD uygulaması koruma ilkesi oluşturma](mtd-app-protection-policy.md) 
