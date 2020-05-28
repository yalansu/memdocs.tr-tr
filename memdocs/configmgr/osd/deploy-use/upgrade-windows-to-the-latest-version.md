---
title: Windows 10’a yükseltme
titleSuffix: Configuration Manager
description: Windows 7 veya üzeri bir işletim sistemini Windows 10 ' a yükseltmek için Configuration Manager nasıl kullanacağınızı öğrenin.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8bfb45ba835851c33d6017f7f0a884bd2c1e9421
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429334"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Windows Configuration Manager ile en son sürüme yükseltme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, bir bilgisayardaki işletim sistemini yükseltmek için Configuration Manager adımları sağlanmaktadır. Tek başına medya veya Yazılım Merkezi gibi birçok farklı dağıtım yöntemi arasından seçim yapabilirsiniz. Yerinde yükseltme senaryosunda aşağıdaki özellikler bulunur:  

- İşletim sistemini Windows 10 veya Windows Server 2016 ve üzeri sürümüne yükseltir

- Bilgisayardaki uygulamaları, ayarları ve Kullanıcı verilerini tutar

- Windows ADK gibi dış bağımlılıkları yoktur

- Geleneksel işletim sistemi dağıtımlarından daha hızlı ve daha esnektir

> [!Note]  
> Windows 10 yerinde yükseltme görev sırası, [bulut yönetimi ağ geçidi](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)aracılığıyla yönetilen internet tabanlı istemcilere dağıtımı destekler. Bu özellik, uzak kullanıcıların intranete bağlanmasına gerek kalmadan Windows 10 ' a daha kolay yükseltmesine olanak sağlar. Daha fazla bilgi için bkz. [CMG aracılığıyla Windows 10 yerinde yükseltme dağıtımı](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->


## <a name="supported-versions"></a>Desteklenen sürümler

### <a name="upgrade-version"></a>Yükseltme sürümü

Yalnızca aşağıdaki işletim sistemi sürümlerine yükseltmek için işletim sistemi yükseltme paketleri oluşturun:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>Özgün sürüm

Cihazların bir işletim sistemi yükseltme görev sırasını hedeflemek için aşağıdaki işletim sistemi sürümlerinden birini çalıştırması gerekir:

#### <a name="windows-client"></a>Windows istemcisi

- Windows 7
- Windows 8.1
- Windows 10 ' un önceki bir sürümü. Örneğin, Windows 10, sürüm 1809 sürümünü Windows 10, sürüm 1903 ' ye yükseltebilirsiniz.  

Daha fazla bilgi için bkz. [Windows 10 yükseltme yolları](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths).

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016 ' in önceki bir sürümü
- Windows Server 2019 ' in önceki bir sürümü

Windows Server tarafından desteklenen yükseltme yolları hakkında daha fazla bilgi için bkz. [Windows server 2016 desteklenen yükseltme yolları](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) ve [Windows Server yükseltme merkezi](https://aka.ms/upgradecenter).


## <a name="plan"></a><a name="BKMK_Plan"></a>Planınızın  

### <a name="task-sequence-requirements-and-limitations"></a>Görev sırası gereksinimleri ve sınırlamaları

Bir işletim sistemini yükseltmek için görev dizisinin aşağıdaki gereksinimlerini ve sınırlamalarını gözden geçirerek gereksinimlerinizi karşıladığından emin olun:  

- Yalnızca işletim sistemini yükseltmenin temel göreviyle ilgili görev sırası adımlarını ekleyin. Bu adımlar öncelikle paket, uygulama veya güncelleştirme yüklemeyi içerir. Ayrıca komut satırları, PowerShell veya dinamik değişkenleri ayarla ' yı çalıştıran adımları kullanın.  

- Bilgisayarlarda yüklü olan sürücüleri ve uygulamaları gözden geçirin. Yükseltme görev sırasını dağıtmadan önce, sürücülerin Windows 10 ile uyumlu olduğundan emin olun.  

Aşağıdaki görevler yerinde yükseltme ile uyumlu değildir. Geleneksel işletim sistemi dağıtımlarını kullanmanızı gerektirir:  

- Bilgisayarın etki alanı üyeliğini değiştirme veya yerel Yöneticiler grubunu güncelleştirme.  

- Bilgisayarda temel bir değişiklik uygulama, örneğin:

  - Disk bölümlerini değiştirme
  - Sistem mimarisini x86 'dan x64 'e değiştirme
  - UEFı uygulama. (Olası bir seçenek hakkında daha fazla bilgi için bkz. [yerinde yükseltme SıRASıNDA BIOS 'TAN UEFI 'ye dönüştürme](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).)
  - Temel işletim sistemi dilini değiştirme  

- Özel bir temel görüntü kullanma, üçüncü taraf disk şifrelemeyi kullanma veya WinPE çevrimdışı işlemleri gerektirme dahil olmak üzere özel gereksinimleriniz vardır.  

### <a name="infrastructure-requirements"></a>Altyapı gereksinimleri  

Yükseltme senaryosu için tek önkoşul, kullanılabilir bir dağıtım noktasıdır. İşletim sistemi yükseltme paketini ve görev dizisine dahil ettiğiniz diğer paketleri dağıtın. Daha fazla bilgi için, bkz. [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).


## <a name="configure"></a><a name="BKMK_Configure"></a>Yapılandırma  

### <a name="prepare-the-os-upgrade-package"></a>İşletim sistemi yükseltme paketini hazırlama  

Windows 10 yükseltme paketi, hedef bilgisayardaki işletim sistemini yükseltmek için gerekli kaynak dosyaları içerir. Yükseltme paketi, yükselttiğiniz istemcilerle aynı sürüm, mimari ve dilde olmalıdır. Daha fazla bilgi için bkz. [işletim sistemi yükseltme paketlerini yönetme](../get-started/manage-operating-system-upgrade-packages.md).  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>İşletim sistemini yükseltmek için görev dizisi oluşturma  

İşletim sistemini yükseltme işlemini otomatik hale getirmek üzere bir [işletim sistemini yükseltmek için görev dizisi oluşturma](create-a-task-sequence-to-upgrade-an-operating-system.md) bölümündeki adımları kullanın.  

> [!NOTE]  
> Bir işletim sistemini Windows 10 ' a yükseltmek üzere bir görev dizisi oluşturmak için, genellikle bir [işletim sistemini yükseltmek için görev dizisi oluşturma](create-a-task-sequence-to-upgrade-an-operating-system.md)bölümündeki adımları kullanın. Görev sırası, **işletim sistemini yükseltme** adımını ve ayrıca uçtan uca yükseltme işlemini işleyecek önerilen adımları ve grupları içerir.
>
> Özel bir görev dizisi oluşturabilir ve [işletim sistemi yükseltme](../understand/task-sequence-steps.md#BKMK_UpgradeOS) adımını ekleyebilirsiniz. Bu adım, işletim sistemini Windows 10 ' a yükseltmek için gereken tek bir adımdır. Bu yöntemi seçerseniz, yükseltmeyi gerçekleştirmek için **işletim sistemini yükseltme** adımından sonra [Bilgisayarı yeniden Başlat](../understand/task-sequence-steps.md#BKMK_RestartComputer) adımını da ekleyin. Bilgisayarı Windows PE 'ye değil yüklü IŞLETIM sisteminde yeniden başlatmak için **Şu anda yüklü varsayılan işletim sistemi** ayarını kullandığınızdan emin olun.  


## <a name="deploy"></a><a name="BKMK_Deploy"></a>Dağıtımı  

İşletim sistemini dağıtmak için aşağıdaki dağıtım yöntemlerinden birini kullanın:  

- [Windows’u ağ üzerinden dağıtmak için Yazılım Merkezi’ni kullanma](use-software-center-to-deploy-windows-over-the-network.md)  

- [Windows’u ağ kullanmadan dağıtmak için tek başına ortam kullanma](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > Tek başına medya kullandığınızda, görev dizisine bir önyükleme görüntüsü dahil etmeniz gerekir. Bu yapılandırma görev sırasını görev sırası Medyası Sihirbazı 'nda kullanılabilir hale getirir.


## <a name="monitor"></a>İzleme  

İşletim sistemini yükseltmek üzere görev dizisi dağıtımını izlemek için bkz. [işletim sistemi dağıtımlarını izleme](monitor-operating-system-deployments.md).  
