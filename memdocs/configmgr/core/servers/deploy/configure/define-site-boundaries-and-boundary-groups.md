---
title: Sınırları ve sınır gruplarını kullanma
titleSuffix: Configuration Manager
description: Yönettiğiniz cihazlar için ağ konumlarını ve erişilebilir site sistemlerini tanımlamak üzere sınırları ve sınır gruplarını kullanın.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0b1a6bb6ff9fdffad65db884fe8c3b68d3fc3263
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711248"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Site sınırlarını ve sınır gruplarını tanımlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager *sınırları* , intranetinizdeki ağ konumlarını tanımlar. Bu konumlar yönetmek istediğiniz cihazları içerir. *Sınır grupları* , yapılandırdığınız sınırların mantıksal gruplarıdır.

Bir hiyerarşi herhangi bir sayıda sınır grubu içerebilir. Her sınır grubu aşağıdaki sınır türlerinin herhangi bir birleşimini içerebilir:  

- IP alt ağı  
- Active Directory site adı  
- IPv6 öneki  
- IP adresi aralığı  

İntranet üzerindeki istemciler, geçerli ağ konumunu değerlendirir ve bu bilgileri ait oldukları sınır gruplarını tanımlamak için kullanır.  

İstemciler, sınır gruplarını şu amaçlarla kullanır:  

- **Atanmış bir site bulun:** Sınır grupları, istemcilerin istemci ataması için bir birincil site bulmasını sağlar. Bu davranış, *otomatik site ataması*olarak da bilinir.  

- Kullanabilecekleri **belirli site sistem rollerini bulun:** Bir sınır grubunu belirli site sistemi rolleriyle ilişkilendirin. Daha sonra site, istemcilere sınır grubundaki site sistemleri listesini sağlar. İstemciler, içerik bulma veya yakın yönetim noktası gibi eylemler için bu site sistemlerini kullanır.  

İnternet üzerindeki veya yalnızca Internet istemcileri olarak yapılandırılan istemciler sınır bilgilerini kullanmaz. Bu istemciler otomatik site atamasını kullanamaz. Kendilerine atanan sitesinden veya bulut tabanlı dağıtım noktasından Internet tabanlı bir dağıtım noktasından içerik indirebilir.  

Sürüm 1902 ' den başlayarak bir bulut yönetimi ağ geçidini (CMG) bir sınır grubuyla ilişkilendirebilirsiniz. Daha fazla bilgi için bkz. [CMG hiyerarşi tasarımı](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design).<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a>Öneri

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Gereksinimlerinizi karşılayan en az sınırların karışımını kullanın

Ortamınız için çalışmayı seçtiğiniz sınır türü veya türleri kullanın. Yönetim görevlerinizi basitleştirmek için, en az sayıda sınırı kullanmanıza izin veren sınır türlerini kullanın.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Otomatik site ataması için çakışan sınırları önleyin

Her sınır grubu hem site atamasını hem de site sistem başvurusunu desteklese de, yalnızca site ataması için kullanılacak ayrı bir sınır grupları kümesi oluşturun. Bir sınır grubundaki her sınırın, farklı bir site atamasına sahip başka bir sınır grubunun üyesi olmadığından emin olun.

- Tek bir sınır birden fazla sınır grubuna dahil edilebilir  

- Her sınır grubu, site ataması için farklı bir birincil site ile ilişkilendirilebilir.  

- Farklı site atamalarına sahip iki farklı sınır grubunun üyesi olan bir sınır için istemciler, katılacak bir siteyi rastgele seçer. Bu davranış, istemcinin katılması istediğiniz site için olmayabilir. Bu yapılandırmaya *çakışan sınırlar*adı verilir.  

    Çakışan sınırlar, içerik konumu için bir sorun değildir. İstemcilere kullanabilecekleri ek kaynaklar veya içerik konumları sağlayan yararlı bir yapılandırma olabilir.  


## <a name="next-steps"></a>Sonraki adımlar

- [Ağ konumlarını sınırlar olarak tanımlama](boundaries.md)

- [Sınır gruplarını yapılandırma](boundary-groups.md)
