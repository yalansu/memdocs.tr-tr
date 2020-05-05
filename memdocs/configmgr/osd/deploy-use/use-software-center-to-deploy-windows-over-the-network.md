---
title: Windows’u ağ üzerinden dağıtmak için Yazılım Merkezi’ni kullanma
titleSuffix: Configuration Manager
description: Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenilemek veya Windows 'un en son sürümüne yükseltmek için, bir işletim sistemini yazılım merkezi 'ne dağıtabilirsiniz.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724219"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager ile Windows 'u ağ üzerinden dağıtmak için yazılım merkezi 'ni kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yazılım Merkezi 'nde kullanılabilir Configuration Manager bir işletim sistemi yükleyen görev sırasını yapabilirsiniz. Aşağıdaki işletim sistemi dağıtım senaryolarıyla bir işletim sistemini yazılım merkezi 'ne dağıtabilirsiniz:

-   [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Windows’u en yeni sürüme yükseltme](upgrade-windows-to-the-latest-version.md)

İşletim sistemi dağıtım senaryolarından birindeki adımları doldurun. Ardından, yazılım merkezi 'nde mevcut olan dağıtımlar için hazırlanmak üzere aşağıdaki bölümleri kullanın.

## <a name="configure-deployment-settings"></a>Dağıtım ayarlarını yapılandırma  
İşletim sistemi dağıtımını yazılım merkezi 'nde kullanılabilir hale getirmek için dağıtımı yapılandırın. Dağıtımı, Yazılım Dağıtma Sihirbazı 'nın **dağıtım ayarları** sayfasında veya dağıtımın özelliklerindeki **dağıtım ayarları** sekmesinde yapılandırabilirsiniz. **Aşağıdakiler için kullanılabilir yap** ayarı için **Yalnızca Configuration Manager İstemcileri** veya **Configuration Manager istemcileri, medya ve PXE**ayarını yapılandırın. Sistem işletim sistemini dağıttığında, işletim sistemi, hedef koleksiyonun üyeleri için yazılım merkezi 'nde görüntülenir.

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> Görev dizisini bilgisayarlara dağıtma  
İşletim sistemini bir hedef koleksiyona dağıtın. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md). Yazılım Merkezi için işletim sistemlerini dağıttığınızda, dağıtımın gerekli veya kullanılabilir olup olmadığını yapılandırabilirsiniz.

-   **Gerekli dağıtım**: Gerekli dağıtımlar işletim sistemini Yazılım Merkezi’nde kullanılabilir hale getirir, ancak yapılandırılmış atama zamanlamasında otomatik olarak başlatılır.

-   **Kullanılabilir dağıtım**: İşletim sistemi Yazılım Merkezi'nde kullanılabilir hale gelir ve kullanıcı bunu isteğe bağlı olarak yükleyebilir.
