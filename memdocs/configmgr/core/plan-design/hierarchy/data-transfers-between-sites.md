---
title: Siteler arasında veri aktarımı
titleSuffix: Configuration Manager
description: Configuration Manager, siteler arasında verileri nasıl taşıcağınızı ve verilerin ağınızda aktarımını nasıl yönetebileceğinizi öğrenin.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720215"
---
# <a name="data-transfers-between-sites"></a>Siteler arasında veri aktarımı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, siteler arasında farklı bilgi türlerini aktarmak için *dosya tabanlı çoğaltmayı* ve *veritabanı çoğaltmasını* kullanır. Configuration Manager verileri siteler arasında taşıma ve ağınız arasında veri aktarımını yönetme hakkında bilgi edinin.  

## <a name="types-of-replication"></a>Çoğaltma türleri

### <a name="file-based-replication"></a><a name="bkmk_fileroute" />Dosya tabanlı çoğaltma

Configuration Manager hiyerarşinizdeki siteler arasında dosya tabanlı verileri aktarmak için dosya tabanlı çoğaltmayı kullanır. Bu veriler, alt sitelerdeki dağıtım noktalarına dağıtmak istediğiniz uygulamaları ve paketleri içerir. Ayrıca, sitenin üst sitesine aktardığı işlenmemiş bulma verisi kayıtlarını işler ve sonra işler.  

Daha fazla bilgi için bkz. [dosya tabanlı çoğaltma](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" />Veritabanı çoğaltması

Configuration Manager veritabanı çoğaltması, verileri aktarmak için SQL Server kullanır. Site veritabanındaki değişiklikleri hiyerarşideki diğer sitelerdeki bilgilerle birleştirmek için bu yöntemi kullanır.

Daha fazla bilgi için bkz. [veritabanı çoğaltma](database-replication.md).

SQL çoğaltma sorunlarını gidermeye yönelik yardım için bkz. [SQL çoğaltma sorunlarını giderme](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Ayrıca bkz.

[Çoğaltmayı izleme](../../servers/manage/monitor-replication.md)
