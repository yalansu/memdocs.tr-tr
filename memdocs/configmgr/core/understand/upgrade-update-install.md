---
title: Yükseltme, güncelleştirme ve yükleme hakkında
titleSuffix: Configuration Manager
description: Configuration Manager altyapısını yönetirken, Install, Update ve Upgrade terimleri arasındaki farkı öğrenin.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722602"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Site ve hiyerarşi altyapısı için yükseltme, güncelleştirme ve yükleme hakkında

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager siteleri ve hiyerarşi altyapısını yönetirken, *yükseltme*, *güncelleştirme ve güncelleştirme*terimleri üç ayrı kavramı *tanımlamakta kullanılır.*

## <a name="upgrade"></a>Yükseltme

*Yükseltme* veya *yerinde yükseltme*, Configuration Manager 2012 sitenizin veya hiyerarşisinin geçerli dalı Configuration Manager çalışan bir sürümüne dönüştürülürken kullanılır.

System Center 2012 Configuration Manager Configuration Manager güncel dala yükselttiğinizde, sitelerinizi ve site sunucularınızı barındırmak için aynı sunucuları kullanmaya devam edersiniz ve mevcut veri ve yapılandırmalardan Configuration Manager koruyabilirsiniz.  Bu, yeni donanıma yüklenmiş yeni Configuration Manager dal siteleri kullanırken, yönetilen cihazlarla ilgili yapılandırma ve verilerinizi saklamanın bir yolu olan [geçişten](../migration/migrate-data-between-hierarchies.md) farklıdır.

Daha ayrıntılı bilgi için bkz. [Configuration Manager yükseltme](../servers/deploy/install/upgrade-to-configuration-manager.md).



## <a name="update"></a>Güncelleştirme
*Güncelleştirme* , Configuration Manager için konsol içi güncelleştirmeleri yüklemek ve Configuration Manager konsolundan teslim edilemez güncelleştirmeler olan bant dışı güncelleştirmeler için kullanılır. Konsol içi güncelleştirmeler, Güncel Dalı sitenizin (veya Technical Preview sitesinin) sürümünü daha yüksek bir sürüm çalışacak şekilde değiştirebilir. Örneğin, siteniz sürüm 1806 çalıştırıyorsa, sürüm 1810 için bir güncelleştirme yükleyebilirsiniz. Güncelleştirmeler, site sürümünü değiştirmeden bilinen bir sorun için düzeltmeler de yükleyebilir.      

Güncelleştirmeler genellikle, mevcut dağıtımınıza güvenlik düzeltmeleri, kalite iyileştirmeleri ve yeni özellikler ekler. Technical Preview dalını kullanıyorsanız, bir güncelleştirme daha yeni bir Technical Preview sürümü yükleyebilir.
- Hiyerarşinizin en üst katmanında başlayarak konsol içi güncelleştirmenin ne zaman yükleneceğini seçersiniz.
- Konsolunun içinden kullanılabilir olan herhangi bir güncelleştirmeyi yükleyebilirsiniz. Örneğin, siteniz 1802 sürümünü çalıştırıyorsa ve her iki 1806 ve 1810 de sunulursa, her sürüm daha önce yayımlanmış sürümlerde kullanılabilir olan özellikleri içerdiğinden, sürüm 1810 ' i yüklemeniz önerilir.
- Yeni bir güncelleştirme, üst katman sitenizde yüklemeyi tamamladıktan sonra, alt birincil siteler güncelleştirme işlemini otomatik olarak başlatır. Ancak, [hizmet pencerelerini](../servers/manage/service-windows.md) güncelleştirmelerin zamanlamasını denetlemek için ayarlayabilirsiniz.
- İkincil siteler güncelleştirmeleri otomatik olarak yüklemez. Bunun yerine, Configuration Manager konsolunun içinden güncelleştirmeyi el ile başlatabilirsiniz.

Daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](../servers/manage/updates.md)ve [Configuration Manager için teknik önizleme](../get-started/technical-preview.md).



## <a name="install"></a>Yükleme
*Install* , sıfırdan yeni bir Configuration Manager hiyerarşisi oluştururken veya var olan bir hiyerarşiye ek siteler eklerken kullanılır.  

Yeni bir birincil site veya merkezi yönetim sitesi yüklediğinizde, Setup. exe ' nin ve kullandığınız ilgili kaynak dosyalarının konumu yükleme senaryonuza bağlıdır.

Daha fazla bilgi için bkz. [siteleri yüklemeye hazırlanma](../servers/deploy/install/prepare-to-install-sites.md).
