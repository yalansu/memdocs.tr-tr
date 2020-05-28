---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268801"
---
Pilot ve üretim arasında ayrım yapmak için aşağıdaki tanımları kullanın:  

- **Pilot**: daha büyük bir kümeye dağıtmadan önce doğrulamak istediğiniz cihazlarınızın bir alt kümesi. Cihazları pilot kümesine benzersiz olarak işaretlemek için masaüstü Analizi 'ni kullanın. Pilot sürümündeki cihazlar hiçbir varlık engellenmeden yükseltmeye hazırlardır. Engelleyici bir varlık *kritik* olarak *işaretlenir ve yükseltilemiyor* .  

- **Üretim**: pilot ortamında olmayan masaüstü analizine kaydolan diğer tüm cihazlar. Üretim cihazları, tüm varlıklar oturum kapattığında yükseltmeye hazırız. Masaüstü analizi, kritik olmayan varlıkların otomatik olarak oturumunu kapatır.  
