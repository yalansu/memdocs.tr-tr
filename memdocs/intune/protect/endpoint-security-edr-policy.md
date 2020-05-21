---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle Endpoint Detection ve yanıt ayarlarını yönetme | Microsoft Docs
description: Microsoft Uç Nokta Yöneticisi 'nde uç nokta güvenlik uç noktası algılama ve yanıt ilkesiyle yönettiğiniz cihazlar için ilkeleri yapılandırın ve dağıtın.
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
ms.openlocfilehash: 3ca9d8f1db36856d9d696a2a1c3933ff4a54b7c3
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431308"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için uç nokta algılama ve yanıt ilkesi

Defender ATP 'yi Intune ile tümleştirdiğinizde, EDR ayarlarını yönetmek ve cihazları Defender ATP 'ye eklemek için uç nokta algılama ve yanıt (EDR) için uç nokta güvenlik ilkelerini kullanabilirsiniz.

Microsoft Defender ATP uç noktası algılama ve yanıtının özellikleri, gerçek zamanlı ve eyleme dönüştürülebilir gelişmiş saldırı algılamalarını sağlar. Güvenlik analistleri uyarıları etkin bir şekilde önceliklendirebilir, ihlalin tam kapsamına yönelik görünürlük elde edebilir ve tehditleri düzeltmek için yanıt işlemleri gerçekleştirebilir.

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin **uç nokta güvenlik** düğümünde, EDR için uç nokta güvenlik ilkelerini bulun. *Manage*

[Uç nokta algılama ve yanıt profillerinin ayarlarını](../protect/endpoint-security-edr-profile-settings.md)görüntüleyin.

## <a name="prerequisites-for-edr-profiles"></a>EDR profilleri için Önkoşullar

- Windows 10 veya üzeri
- Intune 'un bir cihazda uç nokta algılamayı ve yanıt ayarlarını yönetmesi için, cihazı Defender ATP ile birlikte yüklemelisiniz.

## <a name="edr-profiles"></a>EDR profilleri

**Windows 10 profilleri**:

- **Endpoint Detection ve yanıt** – [Microsoft Defender ATP uç noktası algılama ve yanıt ayarlarını](endpoint-security-edr-profile-settings.md)yönetin.

  Microsoft Defender ATP uç noktası algılama ve yanıtının özellikleri, gerçek zamanlı ve eyleme dönüştürülebilir gelişmiş saldırı algılamalarını sağlar.

  Daha fazla bilgi için bkz. Microsoft Defender ATP belgelerindeki [Endpoint Detection ve yanıt](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) .

## <a name="next-steps"></a>Sonraki adımlar

[Uç nokta güvenlik ilkelerini yapılandırma](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
