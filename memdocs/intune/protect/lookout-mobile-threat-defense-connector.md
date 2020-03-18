---
title: Microsoft Intune ile Lookout MTD bağlayıcısı
titleSuffix: Microsoft Intune
description: Şirket kaynaklarınıza mobil cihaz erişimini kontrol etmek için Lookout Mobile Threat Defense’i (MTD) Intune ile tümleştirme hakkında bilgi edinin.
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
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1b3927f09bb74f9058b19dad7f2f3b72f21a0d43
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329278"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Intune ile mobil uç nokta güvenlik bağlayıcısını gevle

Microsoft Intune ile tümleşik bir Mobile Threat Defense çözümü olan Lookout tarafından gerçekleştirilen risk değerlendirmesine dayalı olarak mobil cihazlardan şirket kaynaklarına erişimi denetleyebilirsiniz. Risk, Lookout hizmeti tarafından cihazlardan toplanan ve aşağıdakileri içeren telemetriye göre değerlendirilir:

- İşletim sistemi güvenlik açıkları
- Yüklenen kötü amaçlı uygulamalar
- Kötü amaçlı ağ profilleri

Kayıtlı cihazlar için Intune uyumluluk ilkeleri aracılığıyla etkinleştirilen koşullu erişim ilkelerini, algılanan tehditlere dayalı olarak uyumlu olmayan cihazların şirket kaynaklarına erişmesine izin vermek veya erişimi engellemek için kullanabileceğiniz bir şekilde yapılandırabilirsiniz. Kayıtlı olmayan cihazlar için, algılanan tehditlere dayalı olarak bir blok veya seçmeli Temizleme zorlamak için uygulama koruma ilkelerini kullanabilirsiniz.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Mobil uç nokta güvenliğini Intune ve Gevþme etme şirket kaynaklarını korumaya nasıl yardımcı olur?

BT 'nin mobil uygulaması, **iş Için GEVME**ve mobil cihazlarda yüklü ve çalışır. Bu uygulama varsa dosya sistemi, ağ yığını, cihaz ve uygulama telemetrisini yakalar ve mobil tehditlere karşı cihazın riskini değerlendirmek için bunları Lookout bulut hizmetine gönderir. Lookout konsolundaki tehditlere yönelik risk düzeyi sınıflandırmalarını gereksinimlerinize uyacak şekilde değiştirebilirsiniz.

- **Kayıtlı cihazlar Için destek** -Intune cihaz uyumluluk Ilkesi, Mobile Threat Defense (MTD) için bir kural içerir ve bu, risk değerlendirmesi bilgilerini Iş açısından gevşekilde kullanabilir. MTD kuralı etkinleştirildiğinde, Intune, etkin olan ilkeyle cihaz uyumluluğunu değerlendirir. Cihaz uyumsuz bulunursa kullanıcıların Exchange Online ve SharePoint Online gibi kurumsal kaynaklara erişimi engellenir. Kullanıcılar ayrıca, sorunu çözmek ve kurumsal kaynaklara yeniden erişim kazanmak için cihazlarında yüklü olan çalışma uygulaması uygulamasının bir kılavuzunu alırlar. Kayıtlı cihazlarla çalışma için Gevbir sorun kullanmayı desteklemek için:
  - [Cihazlara MTD uygulamaları ekleme](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [MTD 'yi destekleyen bir cihaz uyumluluk ilkesi oluşturma](../protect/mtd-device-compliance-policy-create.md)
  - [Intune 'da MTD bağlayıcısını etkinleştirme](../protect/mtd-connector-enable.md)

- **Kayıtlı olmayan cihazlar Için destek** -Intune, Intune uygulama koruma ilkeleri kullandığınızda, kayıtlı olmayan cihazlarda Iş için gevyana uygulama uygulamasının risk değerlendirmesi verilerini kullanabilir. Yöneticiler bu bileşimi, [Microsoft Intune korunan bir uygulamadaki](../apps/apps-supported-intune-apps.md)kurumsal verilerin korunmasına yardımcı olmak için kullanabilir. Yöneticiler, kayıtlı olmayan cihazlarda Kurumsal veriler için bir blok veya seçmeli silme de verebilir. Kayıtlı olmayan cihazlarla iş için Gevyetkinlikleri kullanmayı desteklemek için:
  - [MTD uygulamasını kayıtlı olmayan cihazlara ekleme](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Mobile Threat Defense uygulama koruma ilkesi oluşturma](../protect/mtd-app-protection-policy.md)
  - [Kayıtlı olmayan cihazlar için Intune 'da MTD bağlayıcısını etkinleştirme](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Desteklenen platformlar

Aşağıdaki platformlar Intune'da kayıtlıysa Lookout için desteklenir:

- **Android 4.1 ve üzeri**  
- **iOS 8 ve üzeri**  

Platform ve dil desteği hakkında daha fazla bilgi için, [GEVME Web sitesini](https://personal.support.lookout.com/hc/articles/114094140253)ziyaret edin.  

## <a name="prerequisites"></a>Önkoşullar

- Lookout Mobil Uç Nokta Güvenliği kurumsal aboneliği  
- Microsoft Intune aboneliği
- Azure Active Directory Premium
- Kullanıcılara atanmış lisanslarla kurumsal taşınabilirlik ve güvenlik (EMS) E3 veya E5.  

Daha fazla bilgi için bkz: [Lookout Mobil Uç Nokta Güvenliği](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="sample-scenarios"></a>Örnek senaryolar

Intune ile mobil uç nokta güvenliği kullanılırken yaygın senaryolar aşağıda verilmiştir.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kötü amaçlı uygulamalardan kaynaklanan tehditlere dayalı olarak erişimi denetleme

Cihazlarda kötü amaçlı yazılım gibi kötü amaçlı uygulamalar algılandığında, tehdit çözülene kadar cihazların aşağıdaki işlemleri gerçekleştirmesini engelleyebilirsiniz:

- Şirket e-postasına bağlanma
- OneDrive İş uygulaması ile şirket dosyalarını eşitleme
- Şirket uygulamalarına erişme

*Kötü amaçlı yazılımlar algılandığında engelleme:*

> [!div class="mx-imgBorder"]
> kötü amaçlı uygulamalar nedeniyle, ilkenin erişimini engelleyen kavramsal bir resim ![](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> Düzeltme sonrasında cihazlara erişim izni gösteren kavramsal resim ![](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak erişimi denetleme

Bağlantıyı izinsiz izleme saldırıları gibi ağınıza yönelik tehditleri algılayın ve cihaz riskine dayalı olarak WiFi ağlarına erişimi koruyun.

*WiFi üzerinden ağ erişimini engelleme:*

> [!div class="mx-imgBorder"]
> ağ tehditlerine dayalı olarak WiFi erişiminin engellenmesini gösteren ![resim](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> düzeltmeden sonra erişime izin veren Koşullu erişimin kavramsal görüntüsünü ![](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak SharePoint Online’a erişimi denetleme

Bağlantıyı izinsiz izleme saldırıları gibi ağınıza yönelik tehditleri algılar ve cihaz riskine dayalı olarak kurumsal dosyaların eşitlenmesini engeller.

*Ağ tehditleri algılandığında SharePoint Online’ı engelle:*

> [!div class="mx-imgBorder"]
> SharePoint Online 'a erişimi engellemeye yönelik kavramsal resim ![](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> Ağ tehdidi düzeltildikten sonra erişime izin vermenin kavramsal görüntüsünü ![](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Kötü amaçlı uygulamalardaki tehditleri temel alan kayıtlı olmayan cihazlarda erişimi denetleme

Mobil tehdit savunma çözümünü Gevlüme, bir cihazı bulaşma olarak kabul eder:
> [!div class="mx-imgBorder"]
> algılanan kötü amaçlı yazılım nedeniyle uygulama koruma ilkesi blokları ![](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

Düzeltmeye erişim verildi:

> [!div class="mx-imgBorder"]
> ![erişim, uygulama koruma ilkesi için düzeltilmek üzere verilir](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu çözümü uygulamak için yapılması gereken ana adımlar şunlardır:

- [Lookout tümleştirmenizi ayarlama](lookout-mtd-connector-integration.md)
- [Intune 'da mobil uç nokta güvenliğini etkinleştirme](mtd-connector-enable.md)
- [Lookout for Work uygulamasını ekleme ve atama](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Lookout cihaz uyumluluğu ilkesini yapılandırma](mtd-device-compliance-policy-create.md)
- [MTD uygulama koruma ilkesi oluşturma](mtd-app-protection-policy.md)