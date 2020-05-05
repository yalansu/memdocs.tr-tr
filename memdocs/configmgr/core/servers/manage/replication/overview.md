---
title: SQL çoğaltma sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager siteleri arasında SQL çoğaltmasını anlamanıza ve sorunlarını gidermenize yardımcı olması için bu diyagramları kullanın
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720474"
---
# <a name="troubleshoot-sql-replication"></a>SQL çoğaltma sorunlarını giderme

Çok siteli bir hiyerarşide, siteler arasında veri aktarmak için SQL çoğaltmasını kullanır Configuration Manager. Daha fazla bilgi için bkz. [veritabanı çoğaltma](../../../plan-design/hierarchy/database-replication.md).

SQL çoğaltmasıyla ilgili sorunları daha iyi anlamak ve sorun gidermek için bu diyagramları kullanın.

- [SQL çoğaltması](sql-replication.md)
- [SQL yapılandırması](sql-configuration.md)
- [SQL performansı](sql-performance.md)
- [SQL çoğaltmayı yeniden başlatma (yeniden başlatma)](sql-replication-reinit.md)
- [Genel verileri yeniden başlatma](global-data-reinit.md)
- [Site verilerini yeniden başlatma](site-data-reinit.md)
- [Eksik iletiyi yeniden başlatma](reinit-missing-message.md)

Bu sorun giderme diyagramları birbirine bağlı. İlişkilerini anlamak için aşağıdaki diyagramı kullanın:

![SQL çoğaltma sorunlarını giderme işleminin genel bakış Diyagramı](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Daha fazla bilgi için Microsoft Desteği aşağıdaki blog dizisine bakın:

- [ConfigMgr DRS eşitleme Iç Işlevleri](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [ConfigMgr 2012 Veri Çoğaltma Hizmeti (DRS) sızıntısı](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS – SSS sorunlarını giderme](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [ConfigMgr 2012 DRS başlatma Iç Işlevleri](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012: DRS ve SQL Hizmet Aracısı sertifika sorunları](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
