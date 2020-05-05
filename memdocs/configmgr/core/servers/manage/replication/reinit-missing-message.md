---
title: Eksik iletiyi yeniden başlatma
titleSuffix: Configuration Manager
description: Configuration Manager SQL çoğaltma yeniden başlatma ile eksik bir ileti sorunlarını gidermeye başlamak için bu diyagramı kullanın
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720467"
---
# <a name="reinit-missing-message"></a>Eksik iletiyi yeniden başlatma

Çok siteli bir hiyerarşide, siteler arasında veri aktarmak için SQL çoğaltmasını kullanır Configuration Manager. Daha fazla bilgi için bkz. [veritabanı çoğaltma](../../../plan-design/hierarchy/database-replication.md).

SQL çoğaltma yeniden başlatma (reinit) ile eksik bir ileti sorunlarını gidermeye başlamak için aşağıdaki diyagramı kullanın:

![Eksik iletiyi yeniden başlatma sorunlarını gidermek için diyagram](media/reinit-missing-message.svg)

## <a name="queries"></a>Sorgular

Bu diyagram aşağıdaki sorguları kullanır:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Site çoğaltmasının yeniden başlatma işlemi bitmediğini denetle

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>Abone sitesinden Trackingguıd & durumunu al

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>Yayımlama sitesinden Trackingguıd & durumunu al

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Düzeltme eylemleri

### <a name="version-1902-and-later"></a>Sürüm 1902 ve üzeri

Sorunu ve yeniden init saptamak için [Çoğaltma Bağlantısı Çözümleyicisi](../monitor-replication.md#BKMK_RLA)çalıştırın.

### <a name="version-1810-and-earlier"></a>Sürüm 1810 ve öncesi

Aşağıdakileri almak için aşağıdaki SQL sorgusunu çalıştırın `ReplicationGroupID`:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Ardından, `InitializeData` `SMS_ReplicationGroup` WMI sınıfındaki yöntemini aşağıdaki değerlerle kullanın:

- Replicationgroupıd: Yukarıdaki SQL sorgusundan
- SiteCode1: üst site
- SiteCode2: alt site

Daha fazla bilgi için [SMS_ReplicationGroup sınıfında ınitializedata yöntemi](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md)bölümüne bakın.

#### <a name="example"></a>Örnek

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Sonraki adımlar

- [SQL çoğaltmayı yeniden başlatma (yeniden başlatma)](sql-replication-reinit.md)
