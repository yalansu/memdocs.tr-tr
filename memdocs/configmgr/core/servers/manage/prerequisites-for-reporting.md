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
ms.openlocfilehash: e08833a5ef560a0f958fe68b4ade0d4717dffc73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720145"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Configuration Manager raporlama önkoşulları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager raporlama Aşağıdaki bağımlılıklara sahiptir:

- SQL Server Reporting Services
- Raporlama hizmetleri noktası
- Power BI Rapor Sunucusu (isteğe bağlı, sürüm 2002 ' den başlayarak)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Configuration Manager ' de raporlamayı kullanabilmeniz için, SQL Server Reporting Services yükleyip yapılandırın.

Raporlama Hizmetleri planlama ve dağıtma hakkında daha fazla bilgi için bkz. [ınstall SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).

Reporting Services veritabanını varsayılan örneğe veya 64 bit SQL Server yüklemesinin adlandırılmış bir örneğine yükleme. SQL Server örneğini site sistem sunucusuyla birlikte bulundurma veya uzak bir bilgisayarda yapılandırma.

Configuration Manager, site veritabanı için yaptığı gibi raporlama için SQL Server aynı sürümlerini destekler. Daha fazla bilgi için bkz. [desteklenen SQL Server sürümleri](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Raporlama hizmetleri noktası

Configuration Manager ' de raporlamayı kullanabilmeniz için, Raporlama Hizmetleri noktası site sistemi rolünü yapılandırın.

Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint).

## <a name="power-bi-report-server"></a>Power BI Rapor Sunucusu

Sürüm 2002 ' den başlayarak raporlamayı Power BI Rapor Sunucusu ile tümleştirebilirsiniz. Önkoşullar dahil daha fazla bilgi için bkz. [Power BI rapor sunucusu tümleştirme](powerbi-report-server.md).

## <a name="next-steps"></a>Sonraki adımlar

[Raporlamayı yapılandırma](configuring-reporting.md)
