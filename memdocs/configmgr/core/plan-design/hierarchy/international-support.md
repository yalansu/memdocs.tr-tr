---
title: Uluslararası destek
titleSuffix: Configuration Manager
description: Configuration Manager, belirli Uluslararası gereksinimlerle uyumlu olacak şekilde yapılandırın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720943"
---
# <a name="international-support-in-configuration-manager"></a>Configuration Manager 'da uluslararası destek

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşağıdaki bölümlerde, Configuration Manager belirli Uluslararası gereksinimlerle uyumlu hale getirmenize yardımcı olacak teknik ayrıntılar sağlanmaktadır.  

## <a name="gb18030-requirements"></a>GB18030 Gereksinimleri  
 Configuration Manager, Çin 'de Configuration Manager kullanabilmeniz için GB18030 'da tanımlanan standartları karşılar. Configuration Manager dağıtımının, GB18030 gereksinimlerini karşılamak için aşağıdaki yapılandırmalara sahip olması gerekir:  

-   Configuration Manager ile kullandığınız her bir site sunucusu bilgisayarı ve SQL Server bilgisayarın bir Çince işletim sistemi kullanması gerekir.  

-   Hiyerarşideki her bir site veritabanının ve her bir SQL Server örneğinin aynı harmanlamayı kullanması ve aşağıdakilerden biri olması gerekir:  

    -   Çince_Basitleştirilmiş_Pinyin_100_CI_AI  

    -   Çince_Basitleştirilmiş_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Bu veritabanı harmanlamaları, [Configuration Manager için SQL Server sürümleri Için destek](../../../core/plan-design/configs/support-for-sql-server-versions.md)bölümünde belirtilen gereksinimler için bir özel durumdur.  

-   Hiyerarşideki her bir site sunucusu bilgisayarının kök klasörüne **GB18030.SMS** adıyla bir dosya yerleştirmeniz gerekir. Bu dosya hiçbir veri içermez ve bu gereksinimi karşılamak için adlandırılmış boş bir metin dosyası olabilir.  
