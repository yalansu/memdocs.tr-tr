---
title: SQL yapılandırması
titleSuffix: Configuration Manager
description: Configuration Manager için SQL yapılandırması sorunlarını gidermeye başlamak için bu diyagramı kullanın
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723232"
---
# <a name="sql-configuration"></a>SQL yapılandırması

Çok siteli bir hiyerarşide, siteler arasında veri aktarmak için SQL çoğaltmasını kullanır Configuration Manager. Daha fazla bilgi için bkz. [veritabanı çoğaltma](../../../plan-design/hierarchy/database-replication.md).

SQL Hizmet Aracısı ile ilişkili SQL yapılandırması sorunlarını gidermeye başlamak için aşağıdaki diyagramı kullanın:

![SQL yapılandırması sorunlarını gidermek için diyagram](media/sql-configuration.svg)

## <a name="queries"></a>Sorgular

Bu diyagramda aşağıdaki sorgular ve eylemler bulunur:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>SQL 'in SSB iletileri sunabilme olup olmadığını denetle

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Düzeltme eylemleri

### <a name="remediate-the-issues-reported-from-transmission_status"></a>Transmission_status bildirilen sorunları düzeltin

Yaygın sorunlar:

- Güvenlik duvarı yapılandırması
- Ağ yapılandırması
- SSB sertifikası yanlış yapılandırılmış

### <a name="run-sql-profiler-to-trace-ssb-events"></a>SSB olaylarını izlemek için SQL Profiler 'ı çalıştırma

SQL Hizmet Aracısı ilgili olayları izlemek için CAS ve birincil site veritabanında SQL Profiler 'ı çalıştırın:

- **Denetim Aracısı oturum açma**
- **Denetim Aracısı konuşması**
- **Aracı** kategorisindeki olaylar
