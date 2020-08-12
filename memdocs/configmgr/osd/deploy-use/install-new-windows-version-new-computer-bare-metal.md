---
title: Windows 'u yeni bir bilgisayara yükler
titleSuffix: Configuration Manager
description: PXE, OEM veya tek başına medyayı kullanarak yeni bir bilgisayara (çıplak) bir işletim sistemi yüklemek için Configuration Manager kullanın.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eb880b6cb6f45de06b602bc9caa8ca7b98022d5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125091"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Yeni bir bilgisayara yeni bir Windows sürümü (çıplak) Configuration Manager ile yükler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konuda, yeni bir bilgisayara bir işletim sistemi yüklemek için Configuration Manager içindeki genel adımlar sağlanmaktadır. Bu senaryo için PXE, OEM veya tek başına medya gibi birçok farklı dağıtım yöntemi arasından seçim yapabilirsiniz. Sizin için doğru işletim sistemi dağıtım senaryosunun bu olduğundan emin değilseniz, bkz. [Kurumsal işletim sistemlerini dağıtma senaryoları](scenarios-to-deploy-enterprise-operating-systems.md).  

Var olan bir bilgisayarı yeni bir Windows sürümü ile yenilemek için aşağıdaki bölümleri kullanın.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Planınızın  

-   **Altyapı gereksinimlerini planlama ve uygulama**  

     Windows ADK, Windows Dağıtım Hizmetleri (WDS), desteklenen sabit disk yapılandırması vb. gibi işletim sistemlerini dağıtabilmeniz için önce yerinde olması gereken birkaç altyapı gereksinimi vardır. Daha fazla bilgi için bkz. [işletim sistemi dağıtımı Için altyapı gereksinimleri](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

##  <a name="configure"></a><a name="BKMK_Configure"></a>Yapılandırma  

1.  **Önyükleme görüntüsü hazırlama**  

     Önyükleme görüntüleri bir bilgisayarı Windows PE ortamında (sınırlı bileşen ve hizmetlere sahip en düşük işletim sistemi) başlatır ve ardından bilgisayara tam bir Windows işletim sistemi yükleyebilir.   İşletim sistemlerini dağıtırken görüntüyü kullanmak ve dağıtım noktasına dağıtmak için bir önyükleme görüntüsü seçmeniz gerekir. Önyükleme görüntüsünü hazırlamak için aşağıdakileri kullanın:  

    -   Önyükleme görüntüleri hakkında daha fazla bilgi edinmek için bkz. [önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md).  

    -   Önyükleme görüntüsünü özelleştirme hakkında daha fazla bilgi için bkz. [önyükleme görüntülerini özelleştirme](../get-started/customize-boot-images.md).  

    -   Önyükleme görüntüsünü dağıtım noktalarına dağıtın. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **İşletim sistemi görüntüsü hazırlama**  

     İşletim sistemi görüntüsü, işletim sistemini hedef bilgisayara yüklemek için gerekli dosyaları içerir. İşletim sistemi görüntüsünü hazırlamak için aşağıdakileri kullanın:  

    -   Bir işletim sistemi görüntüsü oluşturma hakkında daha fazla bilgi edinmek için bkz. [işletim sistemi görüntülerini yönetme](../get-started/manage-operating-system-images.md).

    -   İşletim sistemi görüntüsünü dağıtım noktalarına dağıtın. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > Windows 'un yeni yüklemeleri, işletim sistemi yükseltme paketleri aracılığıyla yükleme kaynak dosyalarından da gerçekleştirilebilir, ancak bunun yerine **Install. wim** gibi işletim sistemi görüntülerini kullanabilirsiniz.
    >
    > İşletim sistemi yükseltme paketleri aracılığıyla yeni Windows yüklemelerini dağıtmak hala desteklenmektedir, ancak bu yöntemle uyumlu olan sürücülere bağımlıdır. Windows 'u bir işletim sistemi yükseltme paketinden yüklerken, Windows PE 'de hala Windows PE sırasında eklenen sürücüler yüklenir. Bazı sürücüler, Windows PE 'de çalışırken yüklenmekte olan ile uyumlu değildir. Sürücüler Windows PE 'de yükleme ile uyumlu değilse, bunun yerine bir işletim sistemi görüntüsü kullanın.  

3.  **Ağ üzerinden işletim sistemlerini dağıtmak için görev dizisi oluşturma**  

     Ağ üzerinden işletim sisteminin yüklenmesini otomatik hale getirmek için bir görev dizisi kullanın. İşletim sistemini dağıtmak üzere görev dizisi oluşturmak üzere [bir işletim sistemi yüklemek için görev dizisi oluşturma](create-a-task-sequence-to-install-an-operating-system.md) bölümündeki adımları kullanın. Seçtiğiniz dağıtım yöntemine bağlı olarak, görev dizisi için ek hususlar olabilir.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Dağıtımı  

-   İşletim sistemini dağıtmak için aşağıdaki dağıtım yöntemlerinden birini kullanın:  

    -   [Windows’u ağ üzerinden dağıtmak için PXE kullanma](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Windows’u ağ üzerinden dağıtmak için çok noktaya yayın kullanma](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Fabrikada veya yerel depoda OEM için görüntü oluşturma](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Windows’u ağ kullanmadan dağıtmak için tek başına ortam kullanma](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Windows’u ağ üzerinden dağıtmak için önyüklenebilir ortam kullanma](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>İzleme  

-   **Görev dizisi dağıtımını izleme**  

     İşletim sistemini yüklemek üzere görev dizisi dağıtımını izlemek için bkz. [işletim sistemi dağıtımlarını izleme](monitor-operating-system-deployments.md).  
