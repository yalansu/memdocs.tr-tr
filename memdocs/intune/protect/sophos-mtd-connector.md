---
title: Intune ile Sophos Mobile kullanma
titleSuffix: Intune on Azure
description: Şirket kaynaklarınıza mobil cihaz erişimini denetlemek için Microsoft Intune ile Sophos Mobile çözümünü kullanma.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: be5cf3d0ba83fe1027dcec9dcde50257e30b7c47
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988200"
---
# <a name="sophos-mobile-threat-defense-connector-with-intune"></a>Intune ile Sophos Mobile Threat Defense Bağlayıcısı
Microsoft Intune ile tümleştirilen bir Mobile Threat Defense (MTD) çözümü olan Sophos Mobile tarafından gerçekleştirilen risk değerlendirmesine dayalı koşullu erişimi kullanarak mobil cihaz erişimini kontrol edebilirsiniz. Risk, Sophos mobil uygulamasını çalıştıran cihazlardan toplanan telemetriye göre değerlendirilir.
Intune cihaz uyumluluk ilkeleri aracılığıyla etkinleştirilen Sophos Mobile risk değerlendirmesini temel alan koşullu erişim ilkelerini, algılanan tehditlere dayalı olarak uyumlu olmayan cihazların şirket kaynaklarına erişmesine izin vermek veya erişimi engellemek için kullanabileceğiniz şekilde yapılandırabilirsiniz.

> [!NOTE]
> Bu mobil tehdit savunma satıcısı, kayıtlı olmayan cihazlar için desteklenmez.

## <a name="supported-platforms"></a>Desteklenen platformlar

- Android 5,0 ve üzeri
- iOS 11.0 ve üzeri

## <a name="prerequisites"></a>Ön koşullar

- Azure Active Directory Premium
- Microsoft Intune aboneliği
- Sophos Mobile Threat Defense aboneliği

Daha fazla bilgi için bkz. [Sophos Web sitesi](https://www.sophos.com/products/mobile-control.aspx).

## <a name="how-do-intune-and-sophos-mobile-help-protect-your-company-resources"></a>Intune ve Sophos Mobile, şirket kaynaklarınızın korunmasına nasıl yardımcı olur?

Android ve iOS/ıpados için Sophos Mobile uygulaması dosya sistemi, ağ yığını, cihaz ve kullanılabilir olduğunda uygulama telemetrisini yakalar ve ardından telemetri verilerini, cihazın mobil tehditlere karşı riskini değerlendirmek için Sophos mobil bulut hizmetine gönderir.

Intune cihaz uyumluluk ilkesi, Sophos Mobile risk değerlendirmesini temel alan bir Sophos Mobile Threat Defense kuralı içerir. Bu kural etkinleştirildiğinde Intune, cihazın etkinleştirdiğiniz ilke ile uyumluluğunu değerlendirir. Cihaz uyumsuz bulunursa kullanıcıların Exchange Online ve SharePoint Online gibi kurumsal kaynaklara erişimi engellenir. Kullanıcılar ayrıca, sorunu çözmek ve kurumsal kaynaklara yeniden erişim kazanmak için cihazlarında yüklü olan Sophos mobil uygulamasından kılavuz alır.  

## <a name="sample-scenarios"></a>Örnek senaryolar

Burada sık karşılaşılan bazı senaryolar verilmiştir.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kötü amaçlı uygulamalardan kaynaklanan tehditlere dayalı olarak erişimi denetleme

Cihazlarda kötü amaçlı yazılım gibi kötü amaçlı uygulamalar algılandığında, tehdit çözülene kadar cihazların aşağıdaki eylemleri gerçekleştirmesini engelleyebilirsiniz:

- Şirket e-postasına bağlanma
- OneDrive İş uygulaması ile şirket dosyalarını eşitleme
- Şirket uygulamalarına erişme

*Kötü amaçlı uygulamalar algılandığında engelle*:

![Algılanan kötü amaçlı uygulamaların kavramsal görüntüsü](./media/sophos-mtd-connector/sophos-malicious-apps-blocked.png)  

*Düzeltmeye erişim izni verildi*:  
![Düzeltmeden sonra erişim izni verilen kavramsal resim](./media/sophos-mtd-connector/sophos-malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak erişimi denetleme

Bağlantıyı izinsiz izleme saldırıları gibi ağınıza yönelik tehditleri algılayın ve cihaz riskine dayalı olarak Wi-Fi ağlarına erişimi koruyun.  

*Wi-Fi üzerinden ağ erişimini engelleyin*:  
![Wi-Fi üzerinden ağ erişimini engelleyin](./media/sophos-mtd-connector/sophos-network-wifi-blocked.png)

*Düzeltmeye erişim izni verildi*:   
![Düzeltmeye erişim verildi](./media/sophos-mtd-connector/sophos-network-wifi-unblocked.png)  

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Ağa yönelik tehdide dayalı olarak SharePoint Online’a erişimi denetleme

Bağlantıyı izinsiz izleme saldırıları gibi ağınıza yönelik tehditleri algılayın ve cihaz riskine dayalı olarak kurumsal dosyaların eşitlenmesini engelleyin.  

*Ağ tehditleri algılandığında SharePoint Online 'ı engelleyin*:

![Ağ tehditleri algılandığında SharePoint Online’ı engelleme](./media/sophos-mtd-connector/sophos-network-spo-blocked.png)  

*Düzeltmeye erişim izni verildi*:

![Sharepoint için düzeltme ile erişim izni verme örneği](./media/sophos-mtd-connector/sophos-network-spo-unblocked.png)  

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Sophos Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/sophos-mtd-connector/sophos-mobile-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/sophos-mtd-connector/sophos-mobile-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Sonraki adımlar

- [Sophos ile Intune 'U tümleştirme](sophos-mtd-connector-integration.md)
- [Sophos uygulamalarını ayarlama](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Sophos cihaz uyumluluk ilkesi oluştur](mtd-device-compliance-policy-create.md)
- [Sophos MTD bağlayıcısını etkinleştir](mtd-connector-enable.md)
