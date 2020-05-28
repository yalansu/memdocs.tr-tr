---
title: Surface cihaz panosu
titleSuffix: Configuration Manager
description: Panoyu kullanarak yüzey cihazları hakkındaki bilgileri gözden geçirin.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: f9b9c49bde16754b7a60112905f14da2cd5e48eb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906285"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Configuration Manager Surface cihaz panosu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sürüm 1802 ' den başlayarak Surface cihaz panosu, ortamınızda bulunan yüzey cihazları hakkında tek bir bakışta bilgi verir. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Surface cihaz panosunu açma

Surface cihaz panosunu açmak için aşağıdaki adımları kullanın: 

1. Configuration Manager konsolunu açın. 
2. **İzleme** düğümüne tıklayın. 
3. Panoyu yüklemek için **yüzey cihazları**' na tıklayın.

**Surface cihaz panosu** 
 ![ Surface cihaz panosu](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Surface cihaz panosundaki bilgileri gözden geçirme

Surface cihaz panosu, ortamınız için üç grafik gösterir. 

- **Surface cihazlarının yüzdesi** -size, ortamınız genelinde Surface cihazlarının yüzdesini verir.

    ![Surface cihazlarının yüzdesi grafiği](media/Percent-Surface-Devices.PNG)
- **Yüzey modelleri** -yüzey modeli başına cihaz sayısını gösterir. 
  - Bir grafik bölümünün üzerine gelindiğinde, modelin seçildiği yüzey cihazlarının yüzdesi size verilir. 

       ![Surface modeller grafiği](media/Surface-Models-Hover.PNG)
  - Bir Graph bölümüne tıkladığınızda model için bir cihaz listesi gönderilir. 
      ![Surface model cihaz listesi](media/Surface-Model-Device-List.PNG)

- **En çok beş bellenim sürümü**-ortamınızda en çok beş bellenim modeli içeren bir grafik görüntüler. 
  - Bir grafik bölümünün üzerine gelindiğinde, size üretici yazılımı sürümünün seçildiği yüzey cihazlarının sayısını verir. Configuration Manager sürüm 1806 ' den başlayarak bir Graph bölümüne tıkladığınızda ilgili cihazların bir listesi görüntülenir. <!--1358654-->
     ![Surface model cihaz listesi](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Daha fazla bilgi

Surface cihazları hakkında daha fazla bilgi için [Surface](https://www.microsoft.com/surface) Web sitesine bakın.

Surface bellenim güncelleştirmelerini Configuration Manager dağıtma hakkında daha fazla bilgi için bkz. [Surface sürücü güncelleştirmelerini yönetme](https://support.microsoft.com/help/4098906).




