---
title: Geçiş planlaması
titleSuffix: Configuration Manager
description: Configuration Manager geçerli dal hedef hiyerarşisine veri geçirmeden önce siteler ve Hiyerarşiler hakkında bilgi edinin.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719662"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Geçerli dala Configuration Manager geçiş planlaması

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli bir dal hedef hiyerarşisine veri geçirmeden önce, Configuration Manager siteleri ve hiyerarşileri hakkında bilgi sahibi olduğunuzdan emin olun. Siteler ve Hiyerarşiler hakkında daha fazla bilgi için bkz. [Configuration Manager Temelleri](../../core/understand/fundamentals.md).  

Desteklenen bir kaynak hiyerarşisinden verileri geçirmeden önce hedef hiyerarşisi olarak Configuration Manager geçerli bir dal hiyerarşisi yükleyebilirsiniz.  

Hedef hiyerarşiyi yükledikten sonra, verileri geçirmeye başlamadan önce hedef hiyerarşinizde kullanmak istediğiniz yönetim özelliklerini ve işlevlerini ayarlayın.  

Ayrıca, kaynak hiyerarşisi ve hedef hiyerarşiniz arasında örtüşme planlaması yapmanız gerekebilir. Örneğin, kaynak hiyerarşisini hedef hiyerarşiniz ile aynı ağ konumlarını veya sınırları kullanacak şekilde ayarlayabilir ve ardından yeni istemcileri hedef hiyerarşinize yükleyip otomatik site atamasını kullanabilirsiniz. Bu senaryoda, yeni yüklenen bir Configuration Manager istemcisi iki hiyerarşiden da bir site seçip, istemci kaynak hiyerarşinize yanlış atayabilir. Bu nedenle, otomatik site ataması kullanmak yerine hedef hiyerarşideki her yeni istemciyi bu hiyerarşideki belirli bir siteye atamayı planlayın.  

Site atamaları hakkında daha fazla bilgi için bkz. [Configuration Manager farklı sürümleri arasında birlikte çalışabilirlik](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)için [istemci site ataması konuları](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) .  

Desteklenen bir kaynak hiyerarşisini Configuration Manager hedef hiyerarşisine geçirmeyi planlamaya yardımcı olması için aşağıdaki makaleleri kullanın:

-   [Geçiş için önkoşullar](../../core/migration/prerequisites-for-migration.md)  

-   [Geçiş planlaması için yönetici denetim listeleri](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Geçerli dala Configuration Manager veri geçirilip geçirmeyeceğinizi belirleme](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Kaynak hiyerarşisi stratejisi planlayın](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Geçiş planlaması için yönetici denetim listeleri](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [İstemci geçiş stratejisi planlayın](../../core/migration/planning-a-client-migration-strategy.md)  

-   [İçerik dağıtımı geçiş stratejisi planlayın](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Configuration Manager nesnelerinin geçerli dala Configuration Manager geçişini planlayın](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Geçiş etkinliğini izlemeyi planlayın](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Geçişi tamamlamayı planlayın](../../core/migration/planning-to-complete-migration.md)  
