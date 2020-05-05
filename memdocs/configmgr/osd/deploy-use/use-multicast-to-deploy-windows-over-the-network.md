---
title: Windows’u ağ üzerinden dağıtmak için çok noktaya yayın kullanma
titleSuffix: Configuration Manager
description: Birden çok bilgisayarın işletim sistemi görüntüsünü eşzamanlı olarak indirebilmesi için Configuration Manager ortamınızda çok noktaya yayın kullanın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f81b23d3783d397d83a3925b98c0c8f601fa4012
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720124"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager ile ağ üzerinden Windows dağıtmak için çok noktaya yayın kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Çok noktaya yayın, birden çok istemcinin aynı işletim sistemi görüntüsünü aynı anda indirebileceği Configuration Manager ortamınızda kullanabileceğiniz bir ağ iyileştirme yöntemidir. Çok noktaya yayın kullanıldığında, aynı anda birden fazla bilgisayar aynı işletim sistemi yansımasını, verinin bir kopyasını ayrı bir bağlantı üzerindeki her bir istemciye göndermesi için dağıtım noktasına talimat vermek yerine, dağıtım noktası tarafından gönderildiği şekilde indirir.  

 Aşağıdaki işletim sistemi dağıtım senaryolarında çok noktaya yayın kullanarak ağ üzerinden işletim sistemlerini dağıtabilirsiniz:  

- [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)  

  İşletim sistemi dağıtım senaryolarından birindeki adımları tamamlayın ve ardından çok noktaya yayını desteklemek için aşağıdaki bölümleri kullanın.  

##  <a name="configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> Dağıtım noktasını çok noktaya yayını destekleyecek şekilde yapılandırma  
 İşletim sistemlerini dağıtırken çok noktaya yayın kullanmak için, çok noktaya yayını destekleyecek şekilde bir dağıtım noktası yapılandırmanız gerekir. Daha fazla bilgi için bkz. [dağıtım noktalarını yükleyip yapılandırma](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast). Çok noktaya yayını desteklemek için gereken bağlantı noktalarının listesi için bkz. [bağlantı noktaları](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>İşletim sistemi görüntüsünü çok noktaya yayın dağıtımları için hazırlama  
 İşletim sistemi görüntü paketini çok noktaya yayını destekleyecek şekilde yapılandırmak için bkz. [Prepare the operating system image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Görev dizisini dağıtma  
 İşletim sistemini bir hedef koleksiyona dağıtın. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).  
