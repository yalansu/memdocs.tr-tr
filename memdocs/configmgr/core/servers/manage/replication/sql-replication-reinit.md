---
title: SQL çoğaltma yeniden başlatma
titleSuffix: Configuration Manager
description: Configuration Manager siteleri arasında SQL çoğaltma yeniden başlatma sorunlarını gidermeye başlamak için bu diyagramı kullanın
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6207ed4eeeef892de38c85096d2cc80189214d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078574"
---
# <a name="sql-replication-reinit"></a>SQL çoğaltma yeniden başlatma

Çok siteli bir hiyerarşide, siteler arasında veri aktarmak için SQL çoğaltmasını kullanır Configuration Manager. Daha fazla bilgi için bkz. [veritabanı çoğaltma](../../../plan-design/hierarchy/database-replication.md).

SQL çoğaltma yeniden başlatma sorunlarını gidermeye başlamak için aşağıdaki diyagramı kullanın (reınit):

![SQL çoğaltma yeniden başlatma sorunlarını gidermek için diyagram](media/sql-replication-reinit.svg)

## <a name="queries"></a>Sorgular

Bu diyagram aşağıdaki sorguları kullanır:

### <a name="check-if-site-is-in-maintenance-mode"></a>Sitenin bakım modunda olup olmadığını denetle

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>Hangi çoğaltma grubunun yeniden init tamamlanmadığını denetleyin

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>Genel verileri denetle

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>Site verilerini denetle

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Sonraki adımlar

- [Genel verileri yeniden başlatma](global-data-reinit.md)
- [Site verilerini yeniden başlatma](site-data-reinit.md)
- [SQL yapılandırması](sql-configuration.md)
