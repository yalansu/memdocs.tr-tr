---
title: Sanallaştırma desteği
titleSuffix: Configuration Manager
description: Sanallaştırma ortamında Configuration Manager istemci ve site sistemi rollerini yükleme gereksinimleri.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709596"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Configuration Manager ile sanallaştırma ortamları için destek

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, bu makaledeki sanallaştırma ortamlarında sanal makine olarak çalışan desteklenen işletim sistemlerine istemci ve site sistem rollerinin yüklenmesini destekler. Bu destek, sanal makine Konağı (sanallaştırma ortamı) istemci veya site sunucusu olarak desteklenmediğinde bile vardır.  

Örneğin, Windows Server 2012 çalıştıran bir sanal makineyi barındırmak için Microsoft Hyper-V Server 2012 ' i kullanırsınız. İstemci veya site sistem rollerini Windows Server 2012 çalıştıran sanal makineye yükleyebilirsiniz. İstemciyi Microsoft Hyper-V Server 2012 çalıştıran konağa yükleyemezsiniz.  

## <a name="virtualization-environments"></a>Sanallaştırma ortamları

- Windows Server 2019  
- Windows Server 2016 <sup> [Note 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Note 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a>Note 1: Iç Içe sanallaştırma

Configuration Manager, Windows Server 2016 ile yeni olan [iç içe sanallaştırmayı](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new)desteklemez.

### <a name="virtualization-environment-support"></a>Sanallaştırma ortamı desteği

Her bir sanal bilgisayar, fiziksel Configuration Manager bilgisayar için kullanacağınız donanım ve yazılım gereksinimlerine aynı veya daha fazla gereksinim duyuyor.  

Sanallaştırma ortamınızın Configuration Manager için desteklendiğini doğrulamak için sunucu sanallaştırma doğrulama programını kullanın. Bir çevrimiçi sanallaştırma programı destek Ilkesi Sihirbazı 'Nı içerir. Daha fazla bilgi için bkz. [Windows Server sanallaştırma doğrulama programı](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
> Configuration Manager, Mac bilgisayarlarda çalışan sanal bılgısayar veya sanal sunucu konuk işletim sistemlerini desteklemez.  

Configuration Manager, çevrimdışı olmaları durumunda sanal makineleri yönetemez. Ana bilgisayardaki Configuration Manager istemcisi kullanılarak çevrimdışı bir sanal makine görüntüsü güncelleştirilemez ve envanter tahsil edilebilir.  

Sanal makineler için herhangi bir ayrıcalık yoktur. Örneğin Configuration Manager, sanal makine durdurulduysa ve güncelleştirmenin uygulandığı sanal makinenin durumu kaydedilmeden yeniden başlatılırsa, bir güncelleştirmenin bir sanal makine görüntüsüne yeniden uygulanması gerekip gerekmediğini belirleyemeyebilir.  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Microsoft Azure sanal makineleri  

Configuration Manager, veri merkezinizdeki şirket içinde çalıştığı gibi Azure 'daki sanal makinelerde çalıştırılabilir. Aşağıdaki senaryolarda Azure sanal makinelerle Configuration Manager kullanın:  

- **Senaryo 1**: Azure sanal makinesinde Configuration Manager çalıştırın. Diğer Azure sanal makinelerinde istemcileri yönetmek için bunu kullanın.  

- **Senaryo 2**: Azure sanal makinesinde Configuration Manager çalıştırın. Azure 'da çalıştırmayan istemcileri yönetmek için bunu kullanın.  

- **Senaryo 3**: Azure sanal makinelerinde farklı Configuration Manager site sistem rolleri çalıştırın. Azure 'a doğru şekilde bağlı olan şirket içi veri merkezinizde diğer rolleri çalıştırın.  

Ağlar, desteklenen konfigürasyonlar ve şirket içi yüklemek için uygulanan donanım gereksinimleri için aynı Configuration Manager gereksinimleri, Azure sanal makinelerinde yükleme için de geçerlidir.  

Daha fazla bilgi için bkz. [Azure 'da Configuration Manager](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]  
> Azure sanal makinelerinde çalışan Configuration Manager siteleri ve istemcileri, şirket içi yüklemelerle aynı lisans gereksinimlerine tabidir.  

## <a name="windows-virtual-desktop"></a>Windows Sanal Masaüstü

[Windows sanal masaüstü](https://docs.microsoft.com/azure/virtual-desktop/) Microsoft Azure ve Microsoft 365 bir önizleme özelliğidir. Sürüm 1906 ' den başlayarak, Azure 'da Windows çalıştıran bu sanal cihazları yönetmek için Configuration Manager kullanın. Daha fazla bilgi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemleri](supported-operating-systems-for-clients-and-devices.md).
