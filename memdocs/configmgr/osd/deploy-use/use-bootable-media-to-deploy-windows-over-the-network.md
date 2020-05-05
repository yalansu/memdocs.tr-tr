---
title: Windows’u ağ üzerinden dağıtmak için önyüklenebilir ortam kullanma
titleSuffix: Configuration Manager
description: Hedef bilgisayar başladığında işletim sistemini dağıtmak için Configuration Manager 'da önyüklenebilir medya dağıtımlarını kullanın.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724366"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager ile ağ üzerinden Windows dağıtmak için önyüklenebilir medya kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hedef bilgisayar önyüklenebilir medya dağıtımı kullanmaya başladığında işletim sistemini dağıtabilirsiniz. Medya, görev sırası, işletim sistemi görüntüsü ve ağdan diğer gerekli içeriğe yönelik bir işaretçi içerir. Hedef bilgisayar başladığında, bilgisayar İşaretçisinde başvurulan öğeleri alır. Önyüklenebilir medya içerik boş olduğunda, medyayı medyada değiştirmek zorunda kalmadan güncelleştirebilirsiniz.

Aşağıdaki işletim sistemi dağıtım senaryolarında çok noktaya yayın kullanarak işletim sistemlerini ağ üzerinden dağıtabilirsiniz:

-   [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Mevcut bir bilgisayarı değiştirme ve ayarları aktarma](replace-an-existing-computer-and-transfer-settings.md)  

İşletim sistemi dağıtımı senaryolarından birindeki adımları tamamlayın ve ardından işletim sistemini dağıtmak için önyüklenebilir medyayı kullanmak üzere aşağıdaki bölümlerden yararlanın.  

## <a name="configure-deployment-settings"></a>Dağıtım ayarlarını yapılandırma  
İşletim sistemi dağıtım işlemini başlatmak üzere önyüklenebilir medya kullandığınızda, işletim sistemini medya tarafından kullanılabilir hale getirmek için dağıtımı yapılandırın. Bu seçeneği, Yazılım Dağıtma Sihirbazı 'nın **dağıtım ayarları** sayfasında veya dağıtımın özelliklerindeki **dağıtım ayarları** sekmesinde ayarlayabilirsiniz. **Aşağıdakiler için kullanılabilir yap** ayarı için aşağıdakilerden birini yapılandırın:

-   İstemcileri, medyayı ve PXE 'yi Configuration Manager

-   Yalnızca medya ve PXE

-   Yalnızca medya ve PXE (gizli)

## <a name="create-the-bootable-media"></a>Önyüklenebilir medya oluşturma
Önyüklenebilir medyanın bir USB flash sürücü veya CD/DVD seti olup olmadığını belirtebilirsiniz. Medyayı başlatan bilgisayar önyüklenebilir sürücü olarak belirlediğiniz seçeneği desteklemelidir. Daha fazla bilgi için bkz. [önyüklenebilir medya oluşturma](create-bootable-media.md).  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Önyüklenebilir medyadan işletim sistemini yükleme  
Önyüklenebilir medyayı bilgisayarda önyüklenebilir bir sürücüye yerleştirin ve ardından çalıştırarak işletim sistemini yükleyin.
