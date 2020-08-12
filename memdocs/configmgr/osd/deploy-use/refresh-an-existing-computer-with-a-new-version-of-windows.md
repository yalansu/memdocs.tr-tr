---
title: Mevcut bir bilgisayarın işletim sistemini Yenile
titleSuffix: Configuration Manager
description: Var olan bir bilgisayarı bölümlemek ve biçimlendirmek ve bilgisayara yeni bir işletim sistemi yüklemek için Configuration Manager çeşitli yöntemler kullanabilirsiniz.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b635301d9d5bd8a0fb81771255acddb21097f23b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124911"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Mevcut bir bilgisayarı bölümlemek ve biçimlendirmek ve sonra yeni bir işletim sistemi yüklemek için Configuration Manager kullanın. Bu işleme bazen *yeniden görüntüleme* veya *silme ve yükleme*denir. Bu senaryo için PXE, önyüklenebilir medya veya yazılım merkezi gibi birçok farklı dağıtım yöntemi arasından seçim yapın. Ayrıca, ayarları depolamak için bir durum geçiş noktası kullanabilir ve sonra bunları yeni işletim sistemine geri yükleyebilirsiniz.

Doğru işletim sistemi dağıtım senaryosunu seçmek için bkz. [Kurumsal işletim sistemlerini dağıtma senaryoları](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="plan"></a><a name="BKMK_Plan"></a>Planınızın  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Altyapı gereksinimlerini planlayın ve uygulayın

Bir işletim sistemini dağıtmadan önce yerinde olması gereken birkaç altyapı gereksinimi vardır. Bu gereksinimlerin bazıları Windows ADK, Kullanıcı Durumu Taşıma Aracı (USMT) ve Windows Dağıtım Hizmetleri 'ni (WDS) içerir. Daha fazla bilgi için bkz. [işletim sistemi dağıtımı Için altyapı gereksinimleri](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="install-a-state-migration-point"></a>Bir durum geçiş noktası yükler

Mevcut bir bilgisayardan ayarları yakalamak ve sonra ayarları yeni işletim sistemine geri yüklemek istiyorsanız, bir durum geçiş noktası kullanmayı düşünün. Daha fazla bilgi için, bkz. [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="configure"></a><a name="BKMK_Configure"></a>Yapılandırma  

### <a name="prepare-a-boot-image"></a>Önyükleme görüntüsü hazırlama

Önyükleme yansımaları bir Windows PE ortamında bir bilgisayar başlatır. Windows PE, sınırlı bileşen ve hizmetlere sahip en düşük bir işletim sistemi. Windows PE 'den Configuration Manager, ardından bilgisayara tam bir Windows işletim sistemi yükleyebilir.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md)

- [Önyükleme görüntülerini özelleştirme](../get-started/customize-boot-images.md)

- [İçeriği dağıt](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Bir işletim sistemi görüntüsü hazırlama

İşletim sistemi görüntüsü, işletim sistemini hedef bilgisayara yüklemek için gerekli dosyaları içerir.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [İşletim sistemi görüntülerini yönetme](../get-started/manage-operating-system-images.md)

- [İçeriği dağıt](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>İşletim sistemini dağıtmak için görev dizisi oluşturma

İşletim sistemini yüklemeyi otomatikleştirmek için bir görev dizisi kullanın. Seçtiğiniz dağıtım yöntemine bağlı olarak, görev dizisi için ek hususlar olabilir.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [İşletim sistemi yüklemek için görev dizisi oluşturma](create-a-task-sequence-to-install-an-operating-system.md)

- [Kullanıcı durumunu yönetme](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a>Dağıtımı

- İşletim sistemini dağıtmak için aşağıdaki dağıtım yöntemlerinden birini kullanın:  

  - [Windows’u ağ üzerinden dağıtmak için PXE kullanma](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Windows’u ağ üzerinden dağıtmak için çok noktaya yayın kullanma](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Fabrikada veya yerel depoda OEM için görüntü oluşturma](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Windows’u ağ kullanmadan dağıtmak için tek başına ortam kullanma](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [Windows’u ağ üzerinden dağıtmak için önyüklenebilir ortam kullanma](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Windows’u ağ üzerinden dağıtmak için Yazılım Merkezi’ni kullanma](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>İzleme  

Daha fazla bilgi için bkz. [işletim sistemi dağıtımlarını izleme](monitor-operating-system-deployments.md).  

> [!Note]
> Bir UEFı cihazını yeniden görüntüdığınızda, Windows Önyükleme Yöneticisi önyükleme yükleyicisinde yeni bir giriş oluşturur. Bu davranış, bir test ortamında veya bir öğrenci laboratuvarında olduğu gibi bir cihazı tekrar tekrar yeniden görüntüyorsanız en belirgin bir davranıştır. Genellikle cihazın performansını veya kullanımını etkilemez. Liste çok büyük alırsa, bazı belirli donanım cihazları işlevsel sorunlarla karşılaşabilir. Örneğin, bir dış USB sürücüsüne önyükleme değil veya listeden geçerli önyükleme girdisini seçemeyebilirsiniz. Kullanılmayan önyükleme girdilerini temizlemek için Windows **bcdedit** komutunu kullanın. Daha fazla bilgi için bkz. [bcdedit/deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
