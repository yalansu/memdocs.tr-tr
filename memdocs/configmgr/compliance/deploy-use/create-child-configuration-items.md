---
title: Alt yapılandırma öğeleri oluşturma
titleSuffix: Configuration Manager
description: Configuration Manager alt yapılandırma öğeleri oluşturun.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d194d9e80c037a13dde3d694793b695dfa5902e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712872"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Configuration Manager alt yapılandırma öğeleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager alt yapılandırma öğeleri, özgün yapılandırma öğesiyle bir ilişkiyi koruyan yapılandırma öğelerinin kopyalardır ve bu, ilk yapılandırmayı üst yapılandırma öğesinden alırlar.  

Configuration Manager konsolundaki bir alt yapılandırma öğesinin özelliklerini görüntülerken, devralınan nesneleri ve ayarları doğrulama ölçütlerine göre düzenleyemezsiniz. Ancak, alt yapılandırma öğesine ek doğrulama ölçütlerini ekledikten sonra düzenleyebilir ve aynı zamanda alt yapılandırma öğesine yeni nesneler ve ayarlar ekleyebilirsiniz.
Alt yapılandırma öğesi oluşturma ve düzenlemeyle ilgili bir örnek, iş gereksinimlerinizi karşılamak için özgün yapılandırma öğesini iyileştirmeniz.  

> [!NOTE]  
>  Alt yapılandırma öğelerini yalnızca **Windows Masaüstleri ve Sunucuları (özel)** türündeki yapılandırma öğelerinden oluşturabilirsiniz.  

## <a name="to-create-a-child-configuration-item"></a>Alt yapılandırma öğesi oluşturmak için  

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **Uyumluluk ayarları** > **yapılandırma öğeleri**' ne tıklayın.  

3.  **Yapılandırma Öğeleri** listesinde, alt yapılandırma öğesi oluşturmak istediğiniz yapılandırma öğesini seçin ve ardından **Giriş** sekmesinde, **Yapılandırma Öğesi** grubundaki **Alt Yapılandırma Öğesi Oluştur**’a tıklayın.  

4.  **Alt Yapılandırma Öğesi Oluştur Sihirbazı** ’nın **Genel**sayfasında, alt yapılandırma öğesini oluşturmak için kullanılacak üst yapılandırma öğesinin belirli bir düzeltmesini seçebilirsiniz. Bu sihirbazdaki diğer adımlar, standart bir yapılandırma öğesi oluştururken kullanacağınız adımlarla aynıdır. Daha fazla bilgi için bkz. [Windows Masaüstü ve sunucu bilgisayarları için özel yapılandırma öğeleri oluşturma](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Sihirbazı tamamlayın. Yeni alt yapılandırma öğesi **Yapılandırma Öğeleri** listesinde görüntülenir.  
