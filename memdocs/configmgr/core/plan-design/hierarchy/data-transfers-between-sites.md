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
ms.openlocfilehash: c3b74ceab892c67abbd56e8cb2a5c123374a92be
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663320"
---
# <a name="data-transfers-between-sites"></a>Siteler arasında veri aktarımı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, siteler arasında farklı bilgi türlerini aktarmak için *dosya tabanlı çoğaltmayı* ve *veritabanı çoğaltmasını* kullanır. Configuration Manager verileri siteler arasında taşıma ve ağınız arasında veri aktarımını yönetme hakkında bilgi edinin.  

## <a name="types-of-replication"></a>Çoğaltma türleri

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /></a> File-based replication

Configuration Manager hiyerarşinizdeki siteler arasında dosya tabanlı verileri aktarmak için dosya tabanlı çoğaltmayı kullanır. Bu veriler, alt sitelerdeki dağıtım noktalarına dağıtmak istediğiniz uygulamaları ve paketleri içerir. Ayrıca, sitenin üst sitesine aktardığı işlenmemiş bulma verisi kayıtlarını işler ve sonra işler.  

Daha fazla bilgi için bkz. [dosya tabanlı çoğaltma](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /></a> Database replication

Configuration Manager veritabanı çoğaltması, verileri aktarmak için SQL Server kullanır. Site veritabanındaki değişiklikleri hiyerarşideki diğer sitelerdeki bilgilerle birleştirmek için bu yöntemi kullanır.

Daha fazla bilgi için bkz. [veritabanı çoğaltma](database-replication.md).

SQL çoğaltma sorunlarını gidermeye yönelik yardım için bkz. [SQL çoğaltma sorunlarını giderme](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Ayrıca bkz.

[Çoğaltmayı izleme](../../servers/manage/monitor-replication.md)
