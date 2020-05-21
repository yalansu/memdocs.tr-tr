---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle virüsten koruma ayarlarını yönetme | Microsoft Docs
description: Microsoft Endpoint Manager 'daki Endpoint Security Antivirus ilkesiyle yönettiğiniz cihazlar için ilkeleri yapılandırma ve dağıtma ve raporları kullanma.
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
ms.openlocfilehash: 2f3a378cdb3b5e24371edb2fd6dc240962f80342
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431384"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için virüsten koruma ilkesi

Intune Endpoint Security virüsten koruma ilkeleri, güvenlik yöneticilerinin yönetilen cihazlar için ayrı virüsten koruma ayarları grubunu yönetmeye odaklanmasına yardımcı olabilir. Virüsten koruma ilkesini kullanmak için, Intune 'U Microsoft Defender Gelişmiş tehdit koruması (Defender ATP) ile bir mobil tehdit savunma çözümü olarak tümleştirin.

Virüsten koruma ilkesi çeşitli profiller içerir. Her profil, yalnızca macOS, Windows 10 veya Windows 10 cihazlarında Windows Güvenlik uygulamasındaki kullanıcı deneyimi için Defender ATP virüsten koruma için uygun olan ayarları içerir.

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin uç nokta güvenlik düğümünde, **Yönetim** altındaki virüsten koruma ilkelerini bulacaksınız.

Virüsten koruma ilkeleri, *uç nokta koruma* veya cihaz [yapılandırma](../configuration/device-profile-create.md) ilkesi için *cihaz kısıtlama* profillerinde bulunan ayarların aynısını içerir ve [cihaz uyumluluk](../protect/device-compliance-get-started.md) ilkesindeki ayarlara benzer. Ancak, bu ilke türleri, virüsten koruma ile ilgili olmayan ek ayar kategorilerini içerir. Ek ayarlar, virüsten koruma yapılandırma görevini karmaşıklaştırabilir. Ayrıca, macOS için virüsten koruma ilkesinde bulunan ayarlar diğer ilke türleri aracılığıyla kullanılamaz. MacOS virüsten koruma profili, dosyaları kullanarak ayarları yapılandırma ihtiyacını değiştirir `.plist` .

## <a name="prerequisites-for-antivirus-policy"></a>Virüsten koruma ilkesi önkoşulları

- **macOS**
  - Tüm desteklenen macOS sürümleri
  - Intune 'un bir cihazdaki virüsten koruma ayarlarını yönetmesi için, Defender ATP 'nin bu cihaza yüklenmesi gerekir. Bakýn. [MacOS Için Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (Defender ATP belgelerinde)

- **Windows 10 ve üzeri**
  - Intune 'un bir cihazdaki virüsten koruma ayarlarını yönetmesi için, Defender ATP 'nin bu cihaza yüklenmesi gerekir. Intune belgelerinde, [Windows Için Microsoft Defender ATP](../protect/advanced-threat-protection.md)bölümüne bakın.
  - Windows güvenlik uygulaması, Windows 10 çalıştıran tüm cihazlara yüklenir ve ek önkoşul gerekmez.

## <a name="antivirus-profiles"></a>Virüsten koruma profilleri

**MacOS profilleri**:

- **Virüsten koruma** -MacOS Için [Virüsten koruma ilkesi ayarlarını](../protect/antivirus-microsoft-defender-settings-macos.md) yönetin.

  [Mac Için Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)'yi kullandığınızda, dosyaları kullanarak bu ayarları yapılandırmak yerine, yönetilen MacOS cihazlarınıza Intune aracılığıyla bir virüsten koruma ayarları yapılandırabilir ve dağıtabilirsiniz `.plist` .

**Windows 10 profilleri**:

- **Microsoft Defender virüsten koruma** -Windows 10 Için [Virüsten koruma ilkesi ayarlarını](../protect/antivirus-microsoft-defender-settings-windows.md) yönetin.

  Defender virüsten koruma, Microsoft Defender Gelişmiş tehdit koruması 'nın (Microsoft Defender ATP) yeni nesil koruma bileşenidir. Yeni nesil koruma, kurumsal kuruluşunuzdaki cihazları korumak için makine öğrenimi, büyük veri analizi, derinlemesine tehdit dirençlerini ve bulut altyapısını birlikte getirir.

  *Microsoft Defender virüsten koruma* profili, cihaz yapılandırma Ilkesinin *cihaz kısıtlama profilinde* bulunan virüsten koruma ayarlarının ayrı bir örneğidir.
  
  Bir *cihaz kısıtlama profilindeki*virüsten koruma ayarlarından farklı olarak, bu ayarları ortak yönetilen cihazlarla kullanabilirsiniz. Bu ayarları kullanmak için, Endpoint Protection için [ortak yönetim iş yükü kaydırıcısının](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) Intune olarak ayarlanması gerekir.

- **Windows Güvenlik deneyimi** – son kullanıcıların Microsoft Defender Güvenlik Merkezi 'nde görüntüleyebilecekleri [Windows güvenlik uygulaması ayarlarını](../protect/antivirus-security-experience-windows-settings.md) ve aldıkları bildirimleri yönetin. Windows güvenlik uygulaması, makinenin sistem durumu ve güvenliği hakkında bildirimler sağlamak için bir dizi Windows güvenlik özelliği tarafından kullanılır. Güvenlik uygulamaları bildirimleri arasında güvenlik duvarları, virüsten koruma ürünleri, Windows Defender SmartScreen ve diğerleri bulunur.

## <a name="antivirus-policy-reports"></a>Virüsten koruma ilkesi raporları

Virüsten koruma ilkesi raporları, uç nokta güvenliği virüsten koruma ilkeleriniz ve cihaz durumunuz hakkındaki durum ayrıntılarını görüntüler. Bu raporlar, Microsoft Endpoint Manager Yönetim Merkezi 'nin uç nokta güvenlik düğümünde bulunabilir.

Raporları görüntülemek için, [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde uç nokta güvenliği ' ne gidin ve **Virüsten koruma**' yı seçin. Virüsten koruma seçildiğinde Özet sayfası açılır. Ek sayfalar olarak ek rapor ve durum görünümleri mevcuttur.

### <a name="summary"></a>Özet

**Özet** sayfasında, [yeni ilkeler oluşturabilir](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) ve daha önce oluşturulmuş ilkelerin bir listesini görüntüleyebilirsiniz. Liste, ilkenin içerdiği profille ilgili üst düzey ayrıntıları (Ilke türü) ve ilke atanmışsa içerir.

![Virüsten koruma ilkesinin genel bakış sayfası](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Listeden bir ilke seçtiğinizde, bu ilke örneğinin *genel bakış* sayfası açılır ve daha fazla bilgi görüntülenir. Bu görünümden bir kutucuk seçtiğinizde, Intune varsa, bu profilin ek ayrıntılarını görüntüler.

![Virüsten koruma ilkesinin genel bakış sayfası](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Windows 10 sağlıksız uç noktalar

**Windows 10 sağlıksız uç noktalar** SAYFASıNDA, MDM Ile yönetilen Windows 10 cihazlarınızın virüsten koruma durumu hakkında bilgi görüntüleyebilirsiniz. Bu bilgiler, *tehdit Aracısı durumu*olarak cihazda çalışan Windows Defender virüsten koruma 'dan döndürülür.

Bu görünümde yalnızca algılanan sorunları olan cihazlar görüntülenir. Bu görünüm, temiz olarak tanımlanan cihazların ayrıntılarını görüntülemez.

![Virüsten koruma ilkesinin genel bakış sayfası](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Sonraki adımlar

[Uç nokta güvenlik ilkelerini yapılandırma](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
