---
title: Geçişi izle
titleSuffix: Configuration Manager
description: Geçiş işlerinin ilerlemesini ve başarısını izlemek için Configuration Manager konsolunu nasıl kullanacağınızı öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713005"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>Configuration Manager geçiş etkinliğini izlemeyi planlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ile, hedef hiyerarşiye bağlanan Configuration Manager konsolundaki geçişi izleyebilirsiniz. **Yönetim** çalışma alanındaki Configuration Manager konsolunda, geçiş işlerinin ilerlemesini ve başarısını Izlemek için **geçiş** düğümünü kullanabilirsiniz. Geçirilen nesneleri, henüz geçirilmeyen nesneleri ve bir geçiş işinden dışlanan nesne sayısını tanımlayan her bir geçiş işi için Özet bilgileri görüntüleyebilirsiniz. Ayrıca, herhangi bir geçiş sorunu hakkındaki ayrıntıları görürsünüz.  

## <a name="view-migration-progress"></a>Geçiş Ilerlemesini görüntüleme  
 Bir geçiş işinin ilerlemesini görüntülemek için aşağıdaki eylemlerden herhangi birini kullanın:  

-   Configuration Manager konsolunun **Yönetim** çalışma alanında **geçiş işleri** düğümünü genişletin, bir geçiş Işi seçin ve sonra **iş sekmesinde nesneler** ' i seçin.  

-   Geçiş ilerlemesini gözden geçirmek veya sorunları belirlemek için Configuration Manager günlük dosyalarını kullanın. Geçiş Yöneticisi, geçiş eylemlerini izleyen Configuration Manager işlemidir ve bunları site sunucusundaki ** \&lt;\>\\InstallationPath logs** klasöründeki migmctrl. log dosyasına kaydeder.  

    > [!NOTE]  
    >  Bir geçiş işi başarısız olursa, migmctrl. log dosyasındaki ayrıntıları mümkün olan en kısa sürede gözden geçirin. Geçiş günlüğü girdileri, dosyaya sürekli olarak eklenir ve eski ayrıntıların üzerine yazılır. Girişlerin üzerine yazılırsa, geçirilen nesnelerle karşılaşabileceğiniz herhangi bir sorunun geçiş sorunlarıyla ilgili olup olmadığını belirleyemeyebilirsiniz. Geçiş etkinliği, geçişi yapılandırırken Configuration Manager konsolunuzun bağlandığı siteden bağımsız olarak hiyerarşinin en üst\-düzey sitesinde günlüğe kaydedilir.  

-   Configuration Manager raporlama kullanın. Configuration Manager, geçiş için\-birkaç yerleşik rapor sağlar veya bu raporları gereksinimlerinize uyacak şekilde düzenleyebilirsiniz. Configuration Manager raporları hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../servers/manage/introduction-to-reporting.md).  
