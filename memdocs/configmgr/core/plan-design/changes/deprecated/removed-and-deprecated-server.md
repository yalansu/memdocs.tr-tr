---
title: Site sunucuları için kullanım dışı
titleSuffix: Configuration Manager
description: Configuration Manager artık site sunucuları için desteklemediği ürünler ve işletim sistemleri hakkında bilgi edinin.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719480"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Configuration Manager site sunucuları için kaldırıldı ve kullanım dışı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager site sunucuları için destekten kaldırılmış olan veya gelecekteki bir güncelleştirmede kaldırılacak olan ürünler ve işletim sistemleri açıklanmaktadır (kullanım dışı). Configuration Manager kullanımını etkileyebilecek gelecekteki değişiklikler hakkında erken bildirim sağlar.  

Bu bilgiler gelecekte değişebilir. Kullanım dışı bırakılan her özelliği, ürünü veya işletim sistemini dahil edebilir.  

## <a name="server-os"></a>Sunucu işletim sistemi  

|İşletim sistemleri|İlk duyurulan kullanımdan kaldırma|Kaldırılan destek|
|-|-|-|
|SP1 ile Windows Server 2008 R2|10 Temmuz 2015| Sürüm 1702|
|Windows Server 2008 SP2|10 Temmuz 2015|Sürüm 1511|

## <a name="sql-server"></a>SQL Server

|SQL Server sürümleri|İlk duyurulan kullanımdan kaldırma|Kaldırılan destek|
|-|-|-|
|SQL Server 2008 R2|10 Temmuz 2015|Sürüm 1702|
|SQL Server 2008|10 Temmuz 2015|Sürüm 1511|

SQL Server sürümünüzü yükseltmeniz gerekiyorsa, kolayca daha karmaşık olan aşağıdaki yöntemleri öneririz:

1. [SQL Server yerinde yükseltin](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (önerilir).  

2. Yeni bir bilgisayara SQL Server yeni bir sürümünü yükler. Ardından, site sunucunuzu yeni SQL Server olarak göstermek için Configuration Manager Kurulum 'un [veritabanı taşıma seçeneğini kullanın](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) .  

3. [Yedekleme ve kurtarma](../../../servers/manage/backup-and-recovery.md)kullanın.  

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Kaldırılan ve kullanım dışı bırakılan](removed-and-deprecated.md)  

- [Microsoft Desteği yaşam döngüsü](https://support.microsoft.com/lifecycle)  

- [Configuration Manager güncel dal sürümleri için destek](../../../servers/manage/current-branch-versions-supported.md)  
