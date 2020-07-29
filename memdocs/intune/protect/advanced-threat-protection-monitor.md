---
title: Microsoft Intune-Azure 'da Microsoft Defender Gelişmiş tehdit koruması (ATP) tümleştirmesini izleme | Microsoft Docs
description: Cihaz uyumluluğu ve ekleme durumu dahil olmak üzere Intune ile Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP) izleyin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264486"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>Microsoft Defender ATP 'yi Intune ile tümleştirdiğinizde cihaz durumunu izleme

Microsoft Intune ve Microsoft Defender Gelişmiş tehdit koruması 'nı (ATP) tümleştirdiğinizde, Microsoft Endpoint Manager Yönetim Merkezi ' nde cihaz uyumluluğu ve ekleme hakkında bilgi görüntüleyebilirsiniz.

## <a name="monitor-device-compliance"></a>Cihaz uyumluluğunu izleme

Microsoft Defender ATP Uyumluluk ilkesine sahip cihazların durumunu izleyin.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Cihazları**seçin  >  **Monitor**  >  **ilke uyumluluğunu**izleyin.

3. Listede Microsoft Defender ATP ilkenizi bulun ve hangi cihazların uyumlu veya uyumsuz olduğunu görün.

Aynı konumdaki uyumsuz cihazlar için *işletimsel* raporu da kullanabilirsiniz:

- **Devices**  >  **Monitor**  >  **Uyumsuz cihazları**izlemek için cihazlar ' ı seçin.

Raporlar hakkında daha fazla bilgi için bkz. [Intune raporları](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Ekleme durumunu görüntüle

Intune tarafından yönetilen cihazların ekleme durumunu görüntülemek için **Endpoint Security**  >  **Microsoft Defender ATP**sayfasına gidin. Bu sayfadan, Microsoft Defender ATP 'ye daha fazla cihaz eklemek için bir cihaz yapılandırma profili de oluşturabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

[Intune 'da koşullu erişimle Microsoft Defender ATP için uyumluluğu zorlama](../protect/advanced-threat-protection.md)
