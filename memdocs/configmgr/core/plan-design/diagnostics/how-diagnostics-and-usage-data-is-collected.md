---
title: Tanılama verileri toplama
titleSuffix: Configuration Manager
description: Configuration Manager kendisiyle ilgili tanılama ve kullanım verilerini nasıl topladığı hakkında bilgi edinin.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709540"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Configuration Manager tanılama ve kullanım verilerini toplar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için tanılama ve kullanım verilerini toplamak için, her birincil site haftalık olarak SQL Server sorguları çalıştırır. Çok siteli bir hiyerarşide, veriler merkezi yönetim sitesine çoğaltılır.  

Bir hiyerarşinin en üst düzey sitesinde hizmet bağlantı noktası, Güncelleştirmeleri denetlerken bu bilgileri gönderir. Hizmet bağlantı noktasının modu, verilerin nasıl aktarılacağını belirler:

- **Çevrimiçi**: haftada bir kez, hizmet bağlantı noktası otomatik olarak bulut hizmetine tanılama ve kullanım verileri gönderir.

- **Çevrimdışı**: tanılama ve kullanım verilerini [hizmet bağlantı aracı](../../servers/manage/use-the-service-connection-tool.md)ile el ile aktarırsınız.

Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../../servers/deploy/configure/about-the-service-connection-point.md).

> [!div class="nextstepaction"]
> [Tanılama ve kullanım verilerini görüntüleme](view-diagnostics-and-usage-data.md)
