---
title: Mevcut bir bilgisayarı değiştirme ve ayarları aktarma
titleSuffix: Configuration Manager
description: Configuration Manager, var olan bir bilgisayarı yeni bir bilgisayar ile değiştirmek için önyüklenebilir medya, çok noktaya yayın veya yazılım merkezi gibi dağıtım yöntemlerinden birini seçin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 860ee3aeb255921ccd8bf3b1695a9647b514752f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124877"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Var olan bir bilgisayarı değiştirme ve ayarları Configuration Manager ile aktarma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konuda, var olan bir bilgisayarı yeni bir bilgisayar ile değiştirmek için Configuration Manager genel adımlar sağlanmaktadır. Bu senaryo için önyüklenebilir medya, çok noktaya yayın veya Yazılım Merkezi gibi birçok farklı dağıtım yöntemi arasından seçim yapabilirsiniz. Ayrıca, ayarların depolanacağı bir durum geçiş noktası yüklemeyi ve ardından bunları yüklendikten sonra yeni işletim sistemine geri yüklemeyi seçebilirsiniz. Sizin için doğru işletim sistemi dağıtım senaryosunun bu olduğundan emin değilseniz, bkz. [Kurumsal işletim sistemlerini dağıtma senaryoları](scenarios-to-deploy-enterprise-operating-systems.md).  

 Var olan bir bilgisayarı yeni bir Windows sürümü ile yenilemek için aşağıdaki bölümleri kullanın.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Planınızın  

-   **Altyapı gereksinimlerini planlama ve uygulama**  

     Windows ADK, Kullanıcı Durumu Taşıma Aracı (USMT), Windows Dağıtım Hizmetleri (WDS), desteklenen sabit disk yapılandırması vb. gibi işletim sistemlerini dağıtabilmeniz için önce yerinde olması gereken birkaç altyapı gereksinimi vardır. Daha fazla bilgi için bkz. [işletim sistemi dağıtımı Için altyapı gereksinimleri](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)  

-   **Bir durum geçiş noktası yükleme (yalnızca ayarları aktarırsanız gereklidir)**  

     Ayarları var olan bilgisayardan yakaladıktan sonra yeni işletim sistemine geri yükleyecekseniz bir durum geçiş noktası yüklemeniz gerekir. Daha fazla bilgi için, bkz. [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="configure"></a><a name="BKMK_Configure"></a>Yapılandırma  

1.  **Önyükleme görüntüsü hazırlama**  

     Önyükleme görüntüleri bir bilgisayarı Windows PE ortamında (sınırlı bileşen ve hizmetlere sahip en düşük işletim sistemi) başlatır ve ardından bilgisayara tam bir Windows işletim sistemi yükleyebilir. İşletim sistemlerini dağıtırken görüntüyü kullanmak ve dağıtım noktasına dağıtmak için bir önyükleme görüntüsü seçmeniz gerekir. Önyükleme görüntüsünü hazırlamak için aşağıdakileri kullanın:  

    -   Önyükleme görüntüleri hakkında daha fazla bilgi edinmek için bkz. [önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md).  

    -   Önyükleme görüntüsünü özelleştirme hakkında daha fazla bilgi için bkz. [önyükleme görüntülerini özelleştirme](../get-started/customize-boot-images.md).  

    -   Önyükleme görüntüsünü dağıtım noktalarına dağıtın. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **İşletim sistemi görüntüsü hazırlama**  

     İşletim sistemi görüntüsü, işletim sistemini hedef bilgisayara yüklemek için gerekli dosyaları içerir. İşletim sistemi görüntüsünü hazırlamak için aşağıdakileri kullanın:  

    -   Bir işletim sistemi görüntüsü oluşturma hakkında daha fazla bilgi edinmek için bkz. [işletim sistemi görüntülerini yönetme](../get-started/manage-operating-system-images.md).  

    -   İşletim sistemi görüntüsünü dağıtım noktalarına dağıtın. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Ağ üzerinden işletim sistemlerini dağıtmak için görev dizisi oluşturma**  

     Ağ üzerinden işletim sisteminin yüklenmesini otomatik hale getirmek için bir görev dizisi kullanın. İşletim sistemini dağıtmak üzere görev dizisi oluşturmak üzere [bir işletim sistemi yüklemek için görev dizisi oluşturma](create-a-task-sequence-to-install-an-operating-system.md) bölümündeki adımları kullanın. Seçtiğiniz dağıtım yöntemine bağlı olarak, görev dizisi için ek hususlar olabilir.  

    > [!NOTE]  
    >  Bu senaryoda kullanıcı ayarlarını ve dosyalarını yakalayıp geri yüklerseniz, bir durum geçiş noktası kullanmayı veya dosyaları yerel olarak kaydetmeyi seçebilirsiniz. Daha fazla bilgi için bkz. [Kullanıcı durumunu yönetme](../get-started/manage-user-state.md).  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Dağıtımı  

-   İşletim sistemini dağıtmak için aşağıdaki dağıtım yöntemlerinden birini kullanın:  

    -   [Windows’u ağ üzerinden dağıtmak için Yazılım Merkezi’ni kullanma](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Windows’u ağ üzerinden dağıtmak için önyüklenebilir ortam kullanma](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Windows’u ağ üzerinden dağıtmak için çok noktaya yayın kullanma](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Fabrikada veya yerel depoda OEM için görüntü oluşturma](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>İzleme  

-   **Görev dizisi dağıtımını izleme**  

     İşletim sistemini yüklemek üzere görev dizisi dağıtımını izlemek için bkz. [işletim sistemi dağıtımlarını izleme](monitor-operating-system-deployments.md).  
