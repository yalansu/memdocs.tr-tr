---
title: SQL çoğaltması
titleSuffix: Configuration Manager
description: Configuration Manager siteleri arasında SQL çoğaltma sorunlarını gidermeye başlamak için bu diyagramı kullanın
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717527"
---
# <a name="sql-replication"></a>SQL çoğaltması

Çok siteli bir hiyerarşide, siteler arasında veri aktarmak için SQL çoğaltmasını kullanır Configuration Manager. Daha fazla bilgi için bkz. [veritabanı çoğaltma](../../../plan-design/hierarchy/database-replication.md).

Bir bağlantı başarısız olduğunda SQL çoğaltma sorunlarını gidermeye başlamak için aşağıdaki diyagramı kullanın:

![SQL çoğaltma sorunlarını gidermek için diyagram](media/sql-replication.svg)

## <a name="queries"></a>Sorgular

Bu diyagram aşağıdaki sorguları kullanır:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>Çoğaltma grubu bağlantısının düşürülmüş veya başarısız durumunda olup olmadığını denetleyin

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>Çoğaltma grubu bağlantısının yakın zamanda hesaplanıp hesaplanmayacağını denetle

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>SQL bakım modunu denetle

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Sonraki adımlar

- [SQL çoğaltmayı yeniden başlatma (yeniden başlatma)](sql-replication-reinit.md)
- [SQL performansı](sql-performance.md)
- [SQL yapılandırması](sql-configuration.md)
