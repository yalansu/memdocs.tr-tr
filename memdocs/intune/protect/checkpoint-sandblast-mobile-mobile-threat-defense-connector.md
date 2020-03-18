---
title: Check Point SandBlast MTD ayarlayın
titleSuffix: Microsoft Intune
description: Şirket kaynaklarınıza mobil cihaz erişimini kontrol etmek için Check Point SandBlast Mobile Threat Defense’i Intune ile tümleştirme hakkında bilgi edinin.
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
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: afd3f7a7c92fba23fc28903b328bc95f8555ba3d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329758"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Check Point SandBlast Mobile Threat Defense bağlayıcısı ile Intune

Microsoft Intune ile tümleşen bir mobil tehdit savunma çözümü olan Check Point SandBlast Mobile tarafından gerçekleştirilen risk değerlendirmesine dayalı koşullu erişimi kullanarak mobil cihaz erişimini denetleyebilirsiniz. Risk, Check Point SandBlast Mobile uygulamasını çalıştıran cihazlardan toplanan telemetriye göre değerlendirilir.

Intune cihaz uyumluluk ilkeleri aracılığıyla etkinleştirilen Check Point SandBlast Mobile risk değerlendirmesini temel alan koşullu erişim ilkelerini yapılandırabilirsiniz ve bu sayede uyumsuz cihazların algılanan şirket kaynaklarına erişmesine izin vermek veya erişimi engellemek için kullanabilirsiniz tehditleri.

> [!NOTE]
> Bu mobil tehdit savunma satıcısı, kayıtlı olmayan cihazlar için desteklenmez.

## <a name="supported-platforms"></a>Desteklenen platformlar

- **Android 4.1 ve üzeri**

- **iOS 8 ve üzeri**

## <a name="pre-requisites"></a>Ön koşullar

- Azure Active Directory Premium

- Microsoft Intune aboneliği

- Check Point SandBlast Mobile Threat Defense aboneliği
  - Daha fazla bilgi için bkz. [CheckPoint SandBlast web sitesi](https://www.checkpoint.com/).

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>Intune ve Check Point SandBlast Mobile, şirket kaynaklarınızın korunmasına nasıl yardımcı olur?

Check Point sandblast Mobile App for Android ve iOS/ıpados, kullanılabilir olduğunda dosya sistemi, ağ yığını, cihaz ve uygulama telemetrisini yakalar ve mobil tehditlere karşı cihazın riskini değerlendirmek için telemetri verilerini Check Point SandBlast bulut hizmetine gönderir.

Intune cihaz uyumluluğu ilkesi, Check Point SandBlast risk değerlendirmesini temel alan bir Check Point SandBlast Mobile Tehdit Savunmasına yönelik bir kural içerir. Bu kural etkinleştirildiğinde Intune, cihazın etkinleştirdiğiniz ilke ile uyumluluğunu değerlendirir. Cihaz uyumsuz bulunursa kullanıcıların Exchange Online ve SharePoint Online gibi kurumsal kaynaklara erişimi engellenir. Kullanıcılar ayrıca, sorunu çözmek ve kurumsal kaynaklara yeniden erişim kazanmak için cihazlarında yüklü olan Check Point SandBlast mobil uygulamasından yol gösteren yönergeler alır.

Burada sık karşılaşılan bazı senaryolar verilmiştir:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kötü amaçlı uygulamalardan kaynaklanan tehditlere dayalı olarak erişimi denetleme

Cihazlarda kötü amaçlı yazılım gibi kötü amaçlı uygulamalar algılandığında, tehdit çözülene kadar cihazları engelleyebilirsiniz:

- Şirket e-postasına bağlanma

- OneDrive İş uygulaması ile şirket dosyalarını eşitleme

- Şirket uygulamalarına erişme

*Kötü amaçlı yazılımlar algılandığında engelleme:*

> [!div class="mx-imgBorder"]
> kötü amaçlı uygulamalar algılandığında Check Point MTD bloğunu ![](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD erişimi verildi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak erişimi denetleme

Ağda **bağlantıyı izinsiz izleme** gibi tehditleri algılayın ve cihaz riskine dayalı olarak Wi-Fi ağlarına erişimi koruyun.

*Wi-Fi üzerinden ağ erişimini engelleme:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD, Wi-Fi ile ağ erişimini engelleyin](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD Wi-Fi erişimi verildi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak SharePoint Online’a erişimi denetleme

Ağda **Bağlantıyı izinsiz izleme** gibi tehditleri algılar ve cihaz riskine dayalı olarak kurumsal dosyaların eşitlenmesini engeller.

*Ağ tehditleri algılandığında SharePoint Online’ı engelle:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD SharePoint Online erişimini engelle](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*Düzeltme ile erişim izni verildi:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD SharePoint Online erişimi verildi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Sonraki adımlar

- [Check Point SandBlast ile Intune tümleştirmesi](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [CheckPoint SandBlast Mobile uygulama kurulumu](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [CheckPoint SandBlast Mobile cihaz uyumluluk ilkesi oluşturma](mtd-device-compliance-policy-create.md)

- [CheckPoint SandBlast Mobile MTD bağlayıcısı](mtd-connector-enable.md)
