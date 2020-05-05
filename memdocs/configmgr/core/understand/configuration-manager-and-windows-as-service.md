---
title: Configuration Manager ve Hizmet olarak Windows
titleSuffix: Configuration Manager
description: Hizmet olarak Windows 'u desteklemek için geçerli dalı Configuration Manager benimseme hakkındaki temel bilgileri alın.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718556"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager ve Hizmet olarak Windows

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Windows 10 için özellik güncelleştirmeleri üzerinde kapsamlı denetim sağlar. Windows 'u bir hizmet modeli olarak tamamen benimsemek için, geçerli dal modelini Configuration Manager benimsemeniz gerekir. Windows 10 ile güncel kalmak için en iyi deneyim için Configuration Manager güncel kalabilmeniz gerekir. Yeni Configuration Manager sürümleri, Windows 10 için heyecan verici yeni kurumsal özelliklerden tam olarak yararlanabilmek için gereklidir. Bu makalede, geçerli dalı Configuration Manager benimsemek için gereken temel makalelerin bir giriş sayfası olması amaçlanmıştır. Güncel dalı Configuration Manager, size hizmet olarak Windows 'un yolunu getirir.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Geçerli dalı Configuration Manager benimseyen önemli makaleler

| Makale        | Açıklama          | 
| ------------- |-------------|
|[Geçerli dala Configuration Manager genel bakış](../plan-design/changes/whats-new-incremental-versions.md)|Configuration Manager için yeni bakım modelinin önemli noktalarının kısa bir özetini sağlar (Güncel Dalı)|
|[Destek yaşam döngüsü](../servers/manage/current-branch-versions-supported.md)|Yeni destek ve bakım modelini açıklar.|
|[Kaldırılan ve kullanımdan kaldırılan öğeler](../plan-design/changes/deprecated/removed-and-deprecated.md)|Configuration Manager kullanımını etkileyebilecek gelecekteki değişiklikler hakkında erken bildirim sağlar.|
|[Güncel dala Configuration Manager güncelleştirmeler](../servers/manage/updates.md)|Configuration Manager için özellik güncelleştirmelerini uygulayan kolay konsol içi yöntemi açıklar.|
|[Kullanılabilir güncelleştirmeleri alma](../servers/manage/install-in-console-updates.md#get-available-updates)|Yeni Configuration Manager Özellik güncelleştirmelerini almak için kullanılabilen iki modu açıklar.|
|[Güncelleştirme denetim listesi](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Varsa sürüme özgü güncelleştirme denetim listelerini sağlar.| 
|[Yeni Configuration Manager Özellik güncelleştirmelerini yükler](../servers/manage/install-in-console-updates.md#bkmk_install)|Özellik güncelleştirmelerine yönelik basit yükleme adımlarını açıklar.|
|[Windows 10 için destek](../plan-design/configs/support-for-windows-10.md)|Windows 10 (ve ADK) sürümleri için destek matrisi sağlar.|
|[Configuration Manager için teknik önizlemeler](../get-started/technical-preview.md)|ConfigMgr Technical Preview programı hakkında bilgi sağlar.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Hizmet olarak Windows 'un benimseme hakkındaki önemli makaleler

| Makale        | Açıklama          |
| ------------- |-------------|
|[Hizmet olarak Windows yönetme](../../osd/deploy-use/manage-windows-as-a-service.md)|Windows 10 özellik güncelleştirmelerini dağıtmak için bakım planlarının nasıl kullanılacağını açıklar.|
|[Görev dizisi aracılığıyla Windows 10 ' un yükseltme](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|Windows 10 ' un ek önerilerle yükseltilmesi için bir görev dizisi oluşturma ayrıntıları.|
|[Aşamalı dağıtımlar](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|Aşamalı dağıtımlar, birden çok koleksiyonda bir görev dizisinin Eşgüdümlü, sıralı bir şekilde dağıtımını otomatik hale getirir.|  
|[Windows 10 güncelleştirme teslimini en iyi duruma getirme](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Windows 10 ' da güncel kalmasını sağlamak üzere güncelleştirme içeriğini yönetmek için Configuration Manager kullanın.|
|[Masaüstü analizlerini kullanma](../../desktop-analytics/overview.md)|Masaüstü analizi, Windows 10 ' a yükseltme için ortamınızdaki cihazların hazır olduğunu değerlendirmenize ve analiz etmenize olanak tanır.|
|[Iş tümleştirmesi için Windows Update (isteğe bağlı)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Configuration Manager kullanılarak Windows Update for Business (WUfB) ilkelerinin nasıl tanımlanacağını ve dağıtılacağını açıklar.|
|[Iş için Microsoft Intune ve Windows Update birlikte ortak yönetimi kullanma (isteğe bağlı)](../../comanage/overview.md)|Ortak yönetime genel bakış sağlar|


## <a name="related-articles"></a>İlgili makaleler:

- [System Center 2012 Configuration Manager güncel dalına yerinde yükseltme Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Geçerli dala Configuration Manager geçiş planlaması](../migration/planning-for-migration.md)
