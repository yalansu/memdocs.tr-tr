---
title: Power Viewer Aracı
titleSuffix: Configuration Manager
description: Configuration Manager istemcisinde güç yönetimi özelliğinin durumunu görüntülemek için Power Viewer aracını kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723197"
---
# <a name="power-viewer-tool"></a>Power Viewer Aracı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Power Viewer aracı [Configuration Manager araçlarından](tools.md)biridir. Configuration Manager istemcisinde güç yönetimi özelliğinin durumunu görüntülemek için kullanın.

**PowerVwr. exe** ' yi yönetici olarak çalıştırın. Araç başlatıldığında, güç **yapılandırma** sekmesinde Yerel bilgisayarın güç özelliklerini ve güç ayarlarını görüntüler. 

Uzak bir bilgisayarın güç yönetimi verilerini görüntülemek için:  

1. **Dosya** menüsüne gidin ve **Bağlan**' a tıklayın. 

2. **Bilgisayar** adını, gerekirse bir **Kullanıcı** adı ve **parolayı**girin. 

Power Viewer 'da üç sekme bulunur:  

- **Power config**: hedeflenen bilgisayarın güç özelliklerini ve güç ayarlarını görüntüleyin.  

- **Günlük etkinlik**: istemcinin günlük etkinlik grafiklerini görüntüleyerek aşağıdaki bilgileri de içerir:  

    - **Bilgisayar açık**: bir günde bilgisayarın güç durumu. Uyku modu kapalı olarak değerlendirilir.  

    - **İzleme açık**: bir günde izleyici durumunda açık veya kapalı durumu.  

    - **Kullanıcı etkin**: bir günde Kullanıcı etkinliği bilgileri.  

- **Güç olayları**: tüm günlük güç olaylarını görüntüleyin. İstemci bu olayları 12:00 olarak özetler. Bu özetleme, günlük etkinlik grafiğine yönelik verileri oluşturur.  
