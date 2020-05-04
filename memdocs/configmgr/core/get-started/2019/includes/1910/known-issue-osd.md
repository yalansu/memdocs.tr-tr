---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716120"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a>Görev dizileri PXE veya medya için kullanılamaz

<!--5578298-->
PXE veya medya (USB veya DVD) için bir görev sırası dağıtırsanız, istemci ilkeyi almaz. **Smsts. log**dosyasında şu ileti bulunur:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Geçici çözüm

Görev dizisini yazılım merkezinden başlatın.
