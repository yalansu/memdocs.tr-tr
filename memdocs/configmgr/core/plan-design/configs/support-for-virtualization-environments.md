---
title: Sanallaştırma desteği
titleSuffix: Configuration Manager
description: Sanallaştırma ortamında Configuration Manager istemci ve site sistemi rollerini yükleme gereksinimleri.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d2977fc34e9c398e9e266cbc9b223ea74a1dd18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700240"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Configuration Manager ile sanallaştırma ortamları için destek

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, belirli sanallaştırma ortamlarında sanal makine (VM) olarak çalışan desteklenen işletim sistemlerine istemci ve site sistem rollerinin yüklenmesini destekler. Bu destek, sanal konak (sanallaştırma ortamı) istemci veya site sunucusu olarak desteklenmediğinde bile vardır.

Örneğin, Windows Server 2019 çalıştıran bir sanal makineyi barındırmak için Microsoft Hyper-V Server 2016 ' i kullanırsınız. İstemci veya site sistem rollerini Windows Server 2019 çalıştıran VM 'ye yükleyebilirsiniz. İstemciyi Microsoft Hyper-V Server 2016 çalıştıran konağa yükleyemezsiniz.

## <a name="virtualization-environments"></a>Sanallaştırma ortamları

- Windows Server 2019  
- Windows Server 2016 <sup> [Note 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Note 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager, Windows Server 2016 ile yeni olan [iç içe sanallaştırmayı](/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new)desteklemez.

### <a name="virtualization-environment-support"></a>Sanallaştırma ortamı desteği

Her bir sanal bilgisayar, fiziksel Configuration Manager bilgisayar için kullanacağınız donanım ve yazılım gereksinimlerine aynı veya daha fazla gereksinim duyuyor.

Configuration Manager sanallaştırma ortamınızı desteklediğini doğrulamak için, sunucu sanallaştırma doğrulama programını kullanın. Bir çevrimiçi sanallaştırma programı destek Ilkesi Sihirbazı 'Nı içerir. Daha fazla bilgi için bkz. [Windows Server sanallaştırma doğrulama programı](https://www.windowsservercatalog.com/svvp.aspx).

Configuration Manager, çevrimdışıyken VM 'Leri yönetemez. Ana bilgisayardaki Configuration Manager istemcisi çevrimdışı bir VM görüntüsünü yönetemez. Örneğin, yazılım güncelleştirmelerini yükleyemez veya donanım envanterini toplayamazlar.

Genel olarak, Configuration Manager VM 'lere özel bir göz önüne alınmaz. Örneğin, bir VM 'yi durdurur ve durumunu kaydetmezseniz Configuration Manager, bir yazılım güncelleştirmesini yeniden yüklemem gerekip gerekmediğini belirleyemeyebilir.

Birden çok kullanıcı oturumunu destekleyen sanal ortamlarda istemci performansına Configuration Manager yardımcı olması için, varsayılan olarak kullanıcı ilkesini devre dışı bırakır. Sürüm 1910 ' den başlayarak, bu senaryoda kullanıcı ilkesini etkinleştirebilirsiniz. Daha fazla bilgi için bkz. [istemci ayarları hakkında-birden çok Kullanıcı oturumu için Kullanıcı Ilkesini etkinleştirme](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions).

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a> Microsoft Azure VM 'Ler

Configuration Manager, veri merkezinizdeki şirket içinde çalıştığı gibi Azure 'daki sanal makinelerde çalıştırılabilir. Aşağıdaki senaryolarda Azure sanal makinelerinden Configuration Manager kullanın:

- **Senaryo 1**: Azure VM üzerinde Configuration Manager çalıştırın. Diğer Azure VM 'lerinde istemcileri yönetmek için kullanın.

- **Senaryo 2**: Azure VM üzerinde Configuration Manager çalıştırın. Azure 'da çalıştırmayan istemcileri yönetmek için bunu kullanın.

- **Senaryo 3**: Azure VM 'lerinde farklı Configuration Manager site sistem rolleri çalıştırın. Azure 'a doğru şekilde bağlı olan şirket içi veri merkezinizde diğer rolleri çalıştırın.

Ağlar, desteklenen konfigürasyonlar ve donanım gereksinimleri için aynı Configuration Manager gereksinimleri, Azure VM 'Leri için de geçerlidir.

Daha fazla bilgi için bkz. [Azure 'da Configuration Manager](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]
> Azure VM 'lerinde çalışan Configuration Manager siteleri ve istemcileri, şirket içi yüklemelerle aynı lisans gereksinimlerine tabidir.

## <a name="windows-virtual-desktop"></a>Windows Sanal Masaüstü

[Windows sanal masaüstü](/azure/virtual-desktop/) , Microsoft Azure üzerinde çalışan bir masaüstü ve uygulama sanallaştırma hizmetidir. Sürüm 1906 ' den başlayarak, Azure 'da Windows çalıştıran bu sanal cihazları yönetmek için Configuration Manager kullanın. Daha fazla bilgi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemleri](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="next-steps"></a>Sonraki adımlar

[Bir sanal masaüstü altyapısında (VDı) Configuration Manager istemcilerini yönetme](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)