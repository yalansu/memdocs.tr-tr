---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle saldırı yüzeyi azaltma ayarlarını yönetme | Microsoft Docs
description: Microsoft Intune uç nokta güvenliği saldırı yüzeyi Azaltma ilkesi ayarlarıyla yönettiğiniz cihazlar için ilkeleri yapılandırma ve dağıtma
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 6d94748356b342fe6dc9498d815edbdb92038af3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913503"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Intune 'da Endpoint Security için saldırı yüzeyi Azaltma ilkesi

Defender virüsten koruma Windows 10 cihazlarınızda kullanımda olduğunda, cihazlarınız için bu ayarları yönetmek üzere saldırı yüzeyi azaltma için Intune uç nokta güvenlik ilkelerini kullanabilirsiniz.

Saldırı yüzeyi azaltma ilkeleri, kuruluşunuzun siber tehditlere ve saldırılara açık olduğu yerleri en aza indirerek saldırı yüzeylerinizi azaltmaya yardımcı olur. Daha fazla bilgi için bkz. Windows tehdit koruması belgelerindeki [saldırı yüzeyi azaltmaya genel bakış]( /windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) .

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin **uç nokta güvenlik** düğümünde *Yönet* bölümünde saldırı yüzeyi azaltma için uç nokta güvenlik ilkelerini bulun. Her saldırı yüzeyi azaltma *profili* , bir Windows 10 cihazının belirli bir alanının ayarlarını yönetir.

[Saldırı yüzeyi azaltma profillerinin ayarlarını](../protect/endpoint-security-asr-profile-settings.md)görüntüleyin.

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>Saldırı yüzeyi azaltma profillerinin önkoşulları

- Windows 10 veya üzeri
- Defender virüsten koruma, cihazda birincil virüsten koruma olmalıdır

## <a name="attack-surface-reduction-profiles"></a>Saldırı yüzeyi azaltma profilleri

**Windows 10 profilleri**:

- **Uygulama ve tarayıcı yalıtımı** – Defender ATP 'nin bir parçası olarak Windows Defender Application Guard (Application Guard) ayarlarını yönetin. Application Guard, eski ve yeni gelişmekte olan saldırıları önlemeye yardımcı olur ve kurumsal tanımlı siteleri, hangi sitelerin, bulut kaynaklarının ve iç ağların güvenilir olduğunu tanımlarken güvenilmeyen olarak yalıtabilir.

  Daha fazla bilgi için bkz. Microsoft Defender ATP belgelerindeki [Application Guard](/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) .

- **Web koruması** – MICROSOFT Defender ATP 'de Web koruması için yönetebileceğiniz ayarlar, makinelerinizin Web tehditlerine karşı güvenliğini sağlamak için ağ korumasını yapılandırın. Web koruması, Microsoft Edge ve Chrome ve Firefox gibi popüler üçüncü taraf tarayıcılarla tümleştirerek Web proxy 'si olmayan Web tehditleri durduruyor ve uzakta veya şirket içi olduklarında makineleri koruyabilirler. Web koruması şu erişimi durduruyor:
  - Sızdırma siteleri
  - Kötü amaçlı yazılım vektörleri
  - Yararlanma siteleri
  - Güvenilmeyen veya düşük saygınlı siteler
  - Özel gösterge listenizde engellediğiniz siteler.

  Daha fazla bilgi için bkz. Microsoft Defender ATP belgelerindeki [Web koruması](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) .

- **Uygulama denetimi** -uygulama denetimi ayarları, kullanıcıların çalıştıracağı uygulamaları ve sistem çekirdeğinde (çekirdek) çalışan kodu kısıtlayarak güvenlik tehditlerini azaltmaya yardımcı olabilir. İmzasız betikleri ve Mssıs 'yi engelleyebilen ayarları yönetin ve Windows PowerShell 'i kısıtlanmış dil modunda çalışacak şekilde kısıtlayın.

  Daha fazla bilgi için bkz. Microsoft Defender ATP belgelerindeki [uygulama denetimi](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) .

- **Saldırı yüzeyi azaltma kuralları** – kötü amaçlı yazılımların ve kötü amaçlı uygulamaların tipik olarak bilgisayarlara bulaşma için kullandığı davranışları hedefleyen saldırı yüzeyi azaltma kuralları ayarlarını yapılandırın; örneğin:
  - Dosya indirmeyi veya çalıştırmayı deneyen Office uygulamalarında veya Web postada kullanılan yürütülebilir dosyalar ve betikler
  - Karıştırılmış veya diğer şüpheli betikler
  - Uygulamalar genellikle, saldırı yüzeyinizi azaltmak, saldırı yüzeyini düşürmek için daha az yol sunmak anlamına gelir.

  Daha fazla bilgi için bkz. Microsoft Defender ATP belgelerindeki [saldırı yüzeyi azaltma kuralları](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) .

- **Cihaz denetimi** – cihaz denetimi ayarları ile, çıkarılabilir medyayı güvenli hale getirmek için cihazları katmanlı bir yaklaşım için yapılandırabilirsiniz. Microsoft Defender ATP, yetkisiz çevre birimlerinin cihazlarınızdan ödün vermeden tehditleri önlemeye yardımcı olmak için birden çok izleme ve denetim özelliği sağlar.

  Daha fazla bilgi edinmek için bkz. Microsoft Defender ATP belgelerindeki [Microsoft Defender ATP kullanarak USB cihazlarını ve diğer çıkarılabilir medyayı denetleme](/windows/security/threat-protection/device-control/control-usb-devices-using-intune) .

- **Yararlanma koruması** -Exploit Protection ayarları, cihazları ve yayılmak için kötüye kullanımları kullanan kötü amaçlı yazılımlara karşı korumaya yardımcı olabilir. Yararlanma koruması, işletim sistemine veya bağımsız uygulamalara uygulanabilecek bir dizi azaltmasından oluşur.

  Daha fazla bilgi için bkz. Microsoft Defender ATP belgelerinde [açıktan yararlanma korumasını etkinleştirme](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) .

## <a name="next-steps"></a>Sonraki adımlar

[Uç nokta güvenlik ilkelerini yapılandırma](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)