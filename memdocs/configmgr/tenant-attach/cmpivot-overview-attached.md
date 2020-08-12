---
title: Kiracı ekli CMPivot genel bakış
titleSuffix: Configuration Manager
description: Microsoft Endpoint Manager kiracıya bağlı cihazlar için CMPivot genel bakış.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 048309c40718f091d2d232d90bf8d77a0d56c7b7
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127629"
---
# <a name="tenant-attach-cmpivot-overview"></a>Kiracı iliştirme: CMPivot genel bakış

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

> [!Important]
> Bu makale, Configuration Manager yönelik Technical Preview dalı için geçerlidir. Daha fazla bilgi için bkz. [Technical Preview sürüm 2005 Configuration Manager](../core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot).

CMPivot, ortamınızdaki bir cihazın durumunu hızlı bir şekilde değerlendirmenize ve işlem yapmanıza olanak sağlar. Bir sorgu girdiğinizde, CMPivot Şu anda bağlı olan cihazda gerçek zamanlı olarak bir sorgu çalıştırır. Döndürülen veriler, iş sorularını yanıtlamak, ortamınızdaki sorunları gidermek veya güvenlik tehditlerine yanıt vermek için filtrelenebilir, gruplandırılabilir ve iyileştirilmelidir. CMPivot kullanma hakkında daha fazla bilgi için bkz. [Use CMPivot](../core/servers/manage/cmpivot.md).

## <a name="refine-cmpivot-queries"></a><a name="bkmk_refine"></a>CMPivot sorgularını iyileştir

Microsoft Endpoint Manager Yönetici konsolundan CMPivot kullanırken, sorgularınızın performans için ayarlanmış olduğundan emin olun. Çok büyük bir veri kümesine sahip bir sorgu istemeniz durumunda alabilirsiniz `Error: The query result is too large, retry with additional filters` . Bu hatayı görürseniz sorgunuzu daha belirgin olacak şekilde daraltın. Aşağıdaki işleçler genellikle sorguları iyileştirmek için kullanılır:

- `count`Yalnızca döndürülen öğe sayısına ihtiyaç duyuyorsanız kullanın.
- `project`Yalnızca belirli sütunlara ihtiyacınız varsa kullanın.
- `take`Belirtilen sayıda satıra geri dönmek için kullanın.
- `top`Belirtilen sütunlara göre sıralanan Ilk N kaydı döndürmek için kullanın.

> [!Important]
> Bir cihazı sorgulamak için CMPivot kullanıldığında, 10 dakika içinde bir yanıt yoksa sorgu zaman aşımına uğrayacaktır. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Endpoint Manager and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla örnek komut dosyası için bkz. [Microsoft Endpoint Manager kiracı iliştirme: CMPivot betik örnekleri](cmpivot-samples-attached.md).
