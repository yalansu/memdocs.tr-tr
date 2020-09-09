---
title: Kiracı ekli CMPivot kullanımına genel bakış
titleSuffix: Configuration Manager
description: CMPivot kullanım genel bakış Microsoft Endpoint Manager kiracı ekli cihazlar için.
ms.date: 09/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8967957883a1c8d397377c30409cb94139014214
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564076"
---
# <a name="tenant-attach-cmpivot-preview-usage-overview"></a>Kiracı iliştirme: CMPivot (Önizleme) kullanımına genel bakış

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]
> - Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.

CMPivot, ortamınızdaki bir cihazın durumunu hızlı bir şekilde değerlendirmenize ve işlem yapmanıza olanak sağlar. Bir sorgu girdiğinizde, CMPivot Şu anda bağlı olan cihazda gerçek zamanlı olarak bir sorgu çalıştırır. Döndürülen veriler, iş sorularını yanıtlamak, ortamınızdaki sorunları gidermek veya güvenlik tehditlerine yanıt vermek için filtrelenebilir, gruplandırılabilir ve iyileştirilmelidir. CMPivot kullanma hakkında daha fazla bilgi için bkz. [Use CMPivot](../core/servers/manage/cmpivot.md).

## <a name="refine-cmpivot-queries"></a><a name="bkmk_refine"></a> CMPivot sorgularını iyileştir

Microsoft Endpoint Manager Yönetici konsolundan CMPivot kullanırken, sorgularınızın performans için ayarlanmış olduğundan emin olun. Çok büyük bir veri kümesine sahip bir sorgu istemeniz durumunda alabilirsiniz `Error: The query result is too large, retry with additional filters` . Bu hatayı görürseniz sorgunuzu daha belirgin olacak şekilde daraltın. Aşağıdaki işleçler genellikle sorguları iyileştirmek için kullanılır:

- `count`Yalnızca döndürülen öğe sayısına ihtiyaç duyuyorsanız kullanın.
- `project`Yalnızca belirli sütunlara ihtiyacınız varsa kullanın.
- `take`Belirtilen sayıda satıra geri dönmek için kullanın.
- `top`Belirtilen sütunlara göre sıralanan Ilk N kaydı döndürmek için kullanın.

> [!Important]
> Bir cihazı sorgulamak için CMPivot kullanıldığında, 10 dakika içinde bir yanıt yoksa sorgu zaman aşımına uğrayacaktır. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Endpoint Manager and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]


## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz. [Launch CMPivot (Önizleme) for the Admin Center 'dan](cmpivot-start.md) daha fazla örnek betik için bkz. [Microsoft Endpoint Manager kiracı iliştirme: CMPivot betik örnekleri](cmpivot-samples-attached.md).
