---
title: Genel verileri yeniden başlatma
titleSuffix: Configuration Manager
description: Configuration Manager hiyerarşisindeki genel veriler için SQL çoğaltma yeniden başlatma sorunlarını gidermeye başlamak için bu diyagramı kullanın
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713635"
---
# <a name="troubleshoot-global-data-reinit"></a>Genel veri reinit sorunlarını giderme

Çok siteli bir hiyerarşide, siteler arasında veri aktarmak için SQL çoğaltmasını kullanır Configuration Manager. Daha fazla bilgi için bkz. [veritabanı çoğaltma](../../../plan-design/hierarchy/database-replication.md).

Configuration Manager hiyerarşisindeki genel veriler için SQL çoğaltma yeniden başlatma (reinit) sorunlarını gidermeye başlamak üzere aşağıdaki diyagramı kullanın:

![Genel veri yeniden başlatma sorunlarını gidermek için diyagram](media/global-data-reinit.svg)

## <a name="queries"></a>Sorgular

Bu diyagram aşağıdaki sorguları kullanır:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Site çoğaltmasının yeniden başlatma işlemi bitmediğini denetle

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Birincil siteden TrackingGuid & durumunu al

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>CA 'lardan Trackingguıd & durumunu al

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>İzleme KIMLIĞI için istek durumunu denetle

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Sonraki adımlar

- [Eksik iletiyi yeniden başlatma](reinit-missing-message.md)
