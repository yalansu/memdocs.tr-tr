---
title: Site verilerini yeniden başlatma
titleSuffix: Configuration Manager
description: Configuration Manager hiyerarşisindeki site verileri için SQL çoğaltma yeniden başlatma sorunlarını gidermeye başlamak için bu diyagramı kullanın
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078608"
---
# <a name="troubleshoot-site-data-reinit"></a>Site veri reinit sorunlarını giderme

Çok siteli bir hiyerarşide, siteler arasında veri aktarmak için SQL çoğaltmasını kullanır Configuration Manager. Daha fazla bilgi için bkz. [veritabanı çoğaltma](../../../plan-design/hierarchy/database-replication.md).

Configuration Manager hiyerarşisindeki site verileri için SQL çoğaltma yeniden başlatma (reınit) sorunlarını gidermeye başlamak üzere aşağıdaki diyagramı kullanın:

![Site verileri yeniden başlatma sorunlarını gidermek için diyagram](media/site-data-reinit.svg)

## <a name="queries"></a>Sorgular

Bu diyagram aşağıdaki sorguları kullanır:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Site çoğaltmasının yeniden başlatma işlemi bitmediğini denetle

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>CA 'lardan Trackingguıd & durumunu al

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Birincil siteden TrackingGuid & durumunu al

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Birincil sitenin bakım modunda olmadığından emin olun

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>İzleme KIMLIĞI için istek durumunu denetle

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Sonraki adımlar

- [Eksik iletiyi yeniden başlatma](reinit-missing-message.md)
- [Genel verileri yeniden başlatma](global-data-reinit.md)
