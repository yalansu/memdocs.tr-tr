---
title: IntuneManagementExtension Varlığı
titleSuffix: Microsoft Intune
description: Intune Veri Ambarı API’sindeki varlık koleksiyonlarının IntuneManagementExtension Varlığı kategorisi için başvuru konusu.
keywords: Intune Veri Ambarı
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 73DF3B90-6D52-4EF6-AFFD-1873A18C7421
ms.reviewer: dariusz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f8152eb12779376e1885d0a2b2898cd602aa825d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331690"
---
# <a name="reference-for-intune-management-extensions"></a>Intune yönetim uzantılarına yönelik başvuru

**Intunemanagemenlersions** kategorisi, mobil cihazlar için şu gibi bilgileri izleyen varlıklar içerir:

- IntuneManagementExtension sürümleri
- IntuneManagementExtension yükleme durumu

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions

**Intunemanagemenısionversion** varlığı, ıntunemanagemenlersions tarafından kullanılan tüm sürümleri listeler.

| Özellik  | Açıklama | Örnek |
|---------|------------|--------|
| extensionVersionKey |Intunemanagemenmalesions sürümünün benzersiz tanıtıcısı. | 1 |
| extensionVersion |4 basamaklı sürüm numarası. |1.0.2.0 |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates

**Intunemanagemenısionhealthstate** , ıntunemanagemensions 'in tüm olası sistem durumlarını listeler.

| Özellik  | Açıklama | Örnek |
|---------|------------|--------|
| extensionStateKey |Sistem durumunun benzersiz tanımlayıcısı. | 2 |
| extensionState |IntuneManagementExtension sistem durumu. | Sağlam |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions

**Intunemanagementextension** , günlük her Windows 10 cihazında ıntunemanagemenlersions sistem durumunu listeler.
Son 60 günün verileri alınır. 


|      Özellik       |                         Açıklama                         | Örnek |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               Tarihin benzersiz tanımlayıcısı.                |   123   |
|      tenantKey      |              Kiracının benzersiz tanımlayıcısı.               |   456   |
|      deviceKey      |              Cihazın benzersiz tanımlayıcısı.               |   789   |
| extensionVersionKey | Intunemanagementextension sürümünün benzersiz tanıtıcısı. |    1    |
|  extensionStateKey  |             Sistem durumunun benzersiz tanımlayıcısı.              |    2    |

