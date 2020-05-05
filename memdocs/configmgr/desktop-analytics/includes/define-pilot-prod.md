---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723652"
---
Pilot ve üretim arasında ayrım yapmak için aşağıdaki tanımları kullanın:  

- **Pilot**: daha büyük bir kümeye dağıtmadan önce doğrulamak istediğiniz cihazlarınızın bir alt kümesi. Cihazları pilot kümesine benzersiz olarak işaretlemek için masaüstü Analizi 'ni kullanın. Pilot sürümündeki cihazlar hiçbir varlık engellenmeden yükseltmeye hazırlardır. Engelleyici bir varlık *kritik* olarak *işaretlenir ve yükseltilemiyor* .  

- **Üretim**: pilot ortamında olmayan masaüstü analizine kaydolan diğer tüm cihazlar. Üretim cihazları, tüm varlıklar oturum kapattığında yükseltmeye hazırız. Masaüstü analizi, kritik olmayan varlıkların otomatik olarak oturumunu kapatır.  

