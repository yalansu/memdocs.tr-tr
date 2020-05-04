---
title: Uzaktan denetim önkoşulları
titleSuffix: Configuration Manager
description: Configuration Manager içindeki uzaktan denetim için önkoşulları alın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715119"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Configuration Manager 'de uzaktan denetim önkoşulları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager uzaktan denetimin dış bağımlılıkları ve ürün içinde bağımlılıkları vardır.  

## <a name="dependencies-external-to-configuration-manager"></a>Bağımlılıklar dış Configuration Manager  

|Bağımlılık|Daha fazla bilgi|  
|----------------|----------------------|  
|Bilgisayar ekran kartı sürücüsü|En iyi uzaktan denetim performansını elde etmek için istemci bilgisayarlarda en güncel video sürücüsünün yüklü olduğundan emin olun.|  

 Windows Embedded, Hizmet Noktası için Windows Embedded (POS) ve Windows Fundamentals for Legacy PCs çalıştıran cihazlar uzaktan denetim görüntüleyicisini desteklemez, ancak uzaktan denetim istemcisini destekler.  

 Configuration Manager uzaktan denetim, Systems Management Server 2003 veya 2007 Configuration Manager çalıştıran istemci bilgisayarları uzaktan yönetmek için kullanılamaz.  

> [!NOTE]  
>  Uzaktan denetim için dış bağımlılık olarak bir Windows hizmeti gerekli değildir.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Uzaktan denetim görüntüleyicisi için desteklenen işletim sistemleri  
Uzaktan Denetim Görüntüleyicisi, Configuration Manager konsolu için desteklenen tüm işletim sistemlerinde desteklenir. Bilgi için bkz. [Configuration Manager konsolları Için desteklenen konfigürasyonlar](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Configuration Manager bağımlılıkları  

|Bağımlılık|Daha fazla bilgi|  
|----------------|----------------------|  
|Uzaktan denetimin istemciler için etkin olması gerekir|Configuration Manager yüklediğinizde, uzaktan denetim varsayılan olarak etkin değildir. Uzaktan denetimi etkinleştirme ve yapılandırma hakkında daha fazla bilgi için bkz. [Uzaktan denetimi yapılandırma](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Raporlama hizmetleri noktası|Uzaktan denetim için raporları çalıştırmadan önce raporlama hizmetleri noktası site sistemi rolünün yüklenmesi gerekir. Daha fazla bilgi için bkz. [raporlamaya giriş](../../../servers/manage/introduction-to-reporting.md).|  
|Uzaktan denetimi yönetmek için güvenlik izinleri|Koleksiyon kaynaklarına erişmek ve Configuration Manager konsolundan bir uzaktan denetim oturumu başlatmak için: **koleksiyon** nesnesi için **Oku**, **kaynağı oku**ve **Uzaktan denetim** izni.<br /><br /> **Uzak Araçlar işleci** güvenlik rolü, Configuration Manager içinde uzaktan denetimi yönetmek için gerekli olan bu izinleri içerir.<br /><br /> Daha fazla bilgi için bkz. [Configuration Manager için rol tabanlı yönetimi yapılandırma](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Ayrıca, izin verilen görüntüleyicilerin, uzak **Araçlar** istemci ayarlarındaki uzaktan **Denetim ve uzaktan yardım listesi görüntüleyicilerine** bu kullanıcıları ekleyerek uzaktan denetimi kullanma izni verilmesi gerekir.
