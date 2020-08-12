---
title: Windows’u ağ üzerinden dağıtmak için çok noktaya yayın kullanma
titleSuffix: Configuration Manager
description: Birden çok bilgisayarın işletim sistemi görüntüsünü eşzamanlı olarak indirebilmesi için Configuration Manager ortamınızda çok noktaya yayın kullanın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124714"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager ile ağ üzerinden Windows dağıtmak için çok noktaya yayın kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Çok noktaya yayın, birden çok istemci aynı anda aynı işletim sistemi görüntüsünü indirebileceğiniz durumlarda kullanabileceğiniz bir ağ iyileştirme yöntemidir. Çok noktaya yayın kullandığınızda, birden çok bilgisayar aynı anda işletim sistemi görüntüsünü dağıtım noktası tarafından çok noktaya yayın olarak indirir. Bu davranış, her istemci yerine dağıtım noktasından ayrı bir bağlantı üzerinden görüntünün bir kopyasını indirmede yapılır.

Aşağıdaki işletim SISTEMI dağıtım senaryolarında çok noktaya yayın kullanarak işletim sistemlerini ağ üzerinden dağıtın:

- [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)

Bu işletim sistemi dağıtım senaryolarından birindeki adımları doldurun. Daha sonra, çok noktaya yayını desteklemek için aşağıdaki bölümleri kullanın.

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a>Çok noktaya yayın için dağıtım noktalarını yapılandırma

Çok noktaya yayın kullanmak için en az bir dağıtım noktasını çok noktaya yayını destekleyecek şekilde yapılandırın. Daha fazla bilgi için bkz. [dağıtım noktalarını yükleyip yapılandırma](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

Çok noktaya yayını desteklemek için gereken bağlantı noktalarının listesi için bkz. [bağlantı noktaları](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).

## <a name="prepare-an-os-image-for-multicast"></a>Çok noktaya yayın için bir işletim sistemi görüntüsü hazırlama

İşletim sistemi görüntüsünü çok noktaya yayını destekleyecek şekilde yapılandırmanız gerekir. Daha fazla bilgi için bkz. [işletim sistemi görüntüsünü çok noktaya yayın dağıtımları Için hazırlama](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Görev dizisini dağıtma

İşletim sistemini bir hedef koleksiyona dağıtın. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="next-steps"></a>Sonraki adımlar

[İşletim sistemi dağıtımı için kullanıcı deneyimleri](../understand/user-experience.md)
