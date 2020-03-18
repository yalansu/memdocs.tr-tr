---
title: Geçiş konusunda dikkat edilmesi gereken önemli noktalar
titleSuffix: Microsoft Intune
description: Bu makalede, Microsoft Intune’a geçiş sürecini başlatmadan önce geçiş konusunda dikkat edilmesi gereken önemli noktalar sağlanmaktadır.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f29d2894-e98b-4f2c-b444-a8ccc1b7efdd
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a954732b2df5824d7116dc10e035b10290c0290
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331246"
---
# <a name="special-migration-considerations"></a>Geçiş konusunda dikkat edilmesi gereken önemli noktalar

Geçiş konusunda, mevcut MDM sağlayıcısı ortamınıza bağlı olarak geçerli olabilecek bazı önemli noktalar vardır.

## <a name="wipe-for-apples-device-enrollment-program-dep"></a>Apple 'ın Aygıt Kayıt Programı (DEP) için Temizleme

Apple Aygıt Kayıt Programı (DEP), son kullanıcı tarafından kaldırılamayan cihaz yapılandırmaları uygular. DEP’in gelişmiş yönetim özelliklerini korumak üzere cihazın Intune’a kaydedilebilmesi için silinerek kullanıma hazır (yeni) duruma getirilmesi gerekir.

Intune 'da cihazları yönetmek için DEP kullanmaya devam etmek için [aygıt kayıt programı Ile iOS/ıpados cihaz kaydını ayarlayın](../enrollment/device-enrollment-program-enroll-ios.md).

## <a name="next-steps"></a>Sonraki adımlar

[2. Aşama: Geçiş kampanyası](migration-guide-campaign.md)
