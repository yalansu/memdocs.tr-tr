---
title: Tanılama ve kullanım verileri
titleSuffix: Configuration Manager
description: Configuration Manager kendisi hakkında toplanan tanılama ve kullanım verileri hakkında bilgi edinin.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6fff68eaad52f753d27971562a4bbfaa47a6cf6e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711570"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Configuration Manager için tanılama ve kullanım verileri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Microsoft tarafından gelecek sürümlerin yükleme deneyimini, kalitesini ve güvenliğini geliştirmek için kullanılan tanılama ve kullanım verilerini toplar.  

Her Configuration Manager hiyerarşisi tanılama ve kullanım verilerini sunar. Her birincil sitede ve merkezi yönetim sitesinde (CAS) haftalık olarak çalışan SQL Server sorgulardan oluşur. Hiyerarşi bir CA kullandığında, alt birincil siteler verilerini bu CA 'lara çoğaltır. Hiyerarşinizin en üst düzey sitesinde [hizmet bağlantı noktası](../../servers/deploy/configure/about-the-service-connection-point.md) , Güncelleştirmeleri denetlerken bu bilgileri gönderir. Hizmet bağlantı noktası çevrimdışı modda ise, [hizmet bağlantı aracını](../../servers/manage/use-the-service-connection-tool.md)kullanarak bilgileri aktarırsınız.

> [!NOTE]  
> Configuration Manager yalnızca sitenin SQL Server veritabanından veri toplar ve doğrudan istemcilerden veya site sunucularından veri toplamaz.  

Daha fazla bilgi için bkz. [Microsoft gizlilik bildirimi](https://go.microsoft.com/fwlink/?LinkID=626527).  

> [!div class="nextstepaction"]
> [Microsoft’un tanılama ve kullanım bilgilerini kullanma şekli](how-diagnostics-and-usage-data-is-used.md)
