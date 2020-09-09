---
title: Surface cihaz panosu
titleSuffix: Configuration Manager
description: Panoyu kullanarak yüzey cihazları hakkındaki bilgileri gözden geçirin.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: cbea7d7e126b120145533b7cf19822b54b3cb701
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607973"
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
     ![Surface bellenim araç ipucu](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Daha fazla bilgi

Surface cihazları hakkında daha fazla bilgi için [Surface](https://www.microsoft.com/surface) Web sitesine bakın.

Surface bellenim güncelleştirmelerini Configuration Manager dağıtma hakkında daha fazla bilgi için bkz. [Surface sürücü güncelleştirmelerini yönetme](../../../sum/deploy-use/surface-drivers.md).




