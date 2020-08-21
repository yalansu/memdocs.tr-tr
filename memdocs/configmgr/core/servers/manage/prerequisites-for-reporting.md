---
title: Raporlama için önkoşullar
titleSuffix: Configuration Manager
description: Configuration Manager rapor kullanımını etkileyen çeşitli bağımlılıkları anlayın.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b082ae578052a92c0afacd3d1f62fdb2e21bd6d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699543"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Configuration Manager raporlama önkoşulları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager raporlama Aşağıdaki bağımlılıklara sahiptir:

- SQL Server Reporting Services
- Raporlama hizmetleri noktası
- Power BI Rapor Sunucusu (isteğe bağlı, sürüm 2002 ' den başlayarak)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Configuration Manager ' de raporlamayı kullanabilmeniz için, SQL Server Reporting Services yükleyip yapılandırın.

Raporlama Hizmetleri planlama ve dağıtma hakkında daha fazla bilgi için bkz. [ınstall SQL Server Reporting Services](/sql/reporting-services/install-windows/install-reporting-services).

Reporting Services veritabanını varsayılan örneğe veya 64 bit SQL Server yüklemesinin adlandırılmış bir örneğine yükleme. SQL Server örneğini site sistem sunucusuyla birlikte bulundurma veya uzak bir bilgisayarda yapılandırma.

Configuration Manager, site veritabanı için yaptığı gibi raporlama için SQL Server aynı sürümlerini destekler. Daha fazla bilgi için bkz. [desteklenen SQL Server sürümleri](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Raporlama hizmetleri noktası

Configuration Manager ' de raporlamayı kullanabilmeniz için, Raporlama Hizmetleri noktası site sistemi rolünü yapılandırın.

Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint).

## <a name="power-bi-report-server"></a>Power BI Rapor Sunucusu

Sürüm 2002 ' den başlayarak raporlamayı Power BI Rapor Sunucusu ile tümleştirebilirsiniz. Önkoşullar dahil daha fazla bilgi için bkz. [Power BI rapor sunucusu tümleştirme](powerbi-report-server.md).

## <a name="next-steps"></a>Sonraki adımlar

[Raporlamayı yapılandırma](configuring-reporting.md)