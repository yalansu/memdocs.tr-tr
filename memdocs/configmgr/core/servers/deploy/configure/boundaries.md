---
title: Sınırları tanımla
titleSuffix: Configuration Manager
description: İntranetinizde, yönetmek istediğiniz cihazları içerebilen ağ konumlarını nasıl tanımlayacağınızı anlayın.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f53088843e0bf42a93c1d959255c7885b07dfe35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721118"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Ağ konumlarını Configuration Manager için sınır olarak tanımlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager sınırları, ağınızda yönetmek istediğiniz cihazları içeren konumlardır. Bir cihazın açık olduğu sınır Active Directory sitesine veya cihaza yüklü Configuration Manager istemcisiyle tanımlanan ağ IP adresine eşdeğerdir.
- Tekil sınırları el ile oluşturabilirsiniz. Ancak Configuration Manager, sınır olarak doğrudan bir üst ağ girişini desteklemez. Bunun yerine, IP adres aralığı sınır türünü kullanın.
- [Active Directory orman bulma](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) YÖNTEMINI her IP alt ağının ve bulduğu Active Directory sitenin sınırlarını otomatik olarak bulmak ve oluşturmak üzere yapılandırabilirsiniz. Active Directory orman keşfi bir Active Directory sitesine atanmış bir üst ağ belirlediğinde Configuration Manager, üst ağı bir IP adresi aralığı sınırına dönüştürür.  

Bir cihazın Configuration Manager yöneticisinin farkında olmadığı bir IP adresi kullanması yaygın olmayan bir durumdur. Bir cihazın ağ konumu şüpheli olduğunda, cihazdaki **IPCONFIG** komutunu kullanarak cihazın konum olarak ne rapor yaptığını doğrulayın.  

Bir sınır oluşturduğunuzda bu sınır, türüne ve kapsamına göre otomatik olarak adlandırılır. Bu adı değiştiremezsiniz. Bunun yerine, Configuration Manager konsolundaki sınırı tanımlamanızı sağlayacak bir açıklama belirtebilirsiniz.  

Her sınır hiyerarşinizdeki her site tarafından kullanılabilir. Sınır oluşturulduktan sonra, özelliklerini aşağıdaki şekilde değiştirebilirsiniz:  
- Sınırı bir veya daha fazla sınır grubuna ekleyin.  
- Sınırın türünü veya kapsamını değiştirin.  
- Sınır grubu ile hangi site sistem sunucularının (dağıtım noktaları, durum geçiş noktaları ve yönetim noktaları) ilişkili olduğunu görmek için sınır grubunun **Site Sistemleri** sekmesini görüntüleyin.  

## <a name="to-create-a-boundary"></a>Sınır oluşturmak için  

1.  Configuration Manager konsolunda, **Yönetim** > **hiyerarşisi yapılandırma** > **sınırları** ' na tıklayın.  

2.  **Giriş** sekmesinde, **Oluştur** grubunda, **Oluştur Boundary.**'u tıklatın.  

3.  Sınır Oluştur iletişim kutusunun **Genel** sekmesinde, sınırı bir kolay adla ve referansla tanımlamak üzere bir **Açıklama** belirtebilirsiniz.  

4.  Bu sınır için bir **Tür** seçin:  

    - **IP Alt Ağı**'nı seçerseniz, bu sınır için bir **Alt Ağ Kimliği** belirtmeniz gerekir.  
      > [!TIP]  
      > **Alt Ağ Kimliği** 'nin otomatik olarak belirtilmesi için **Ağ** ve **Alt ağ maskesi** 'ni belirtebilirsiniz. Sınırı kaydettiğinizde yalnızca Alt Ağ Kimliği değeri kaydedilir.  

    - **Active Directory sitesi**öğesini seçerseniz, site sunucusunun yerel ormanında bir Active Directory sitesi belirtmeniz veya **Gözat** ile konumunu göstermeniz gerekir.  
        
      - Sınır için bir Active Directory sitesi belirttiğinizde, sınır bu Active Directory sitesinin üyesi olan her IP Alt Ağı'nı içerir. Active Directory sitesinin yapılandırması Active Directory'de değişirse, bu sınırda yer alan ağ konumları da değişir.  

      - Active Directory site sınırları, saf AzureAD istemcileri için çalışmaz. Şirket içinde dolaşırsa, yalnızca AD siteleri kullanılarak tanımlanmışsa herhangi bir sınıra düşmez.

    - **IPv6 öneki**'ni seçerseniz, IPv6 öneki biçiminde bir **Önek** belirtmeniz gerekir.  

    - **IP Adresi Aralığı**'n seçerseniz, bir IP Alt Ağının veya birçok IP Alt Ağının parçasını içeren bir **Başlangıç IP adresi** ve **Bitiş IP adresi** belirtmeniz gerekir.    

5.  Yeni sınırı kaydetmek için **Tamam** 'ı tıklatın.  

## <a name="to-configure-a-boundary"></a>Sınırı yapılandırmak için  

1.  Configuration Manager konsolunda, **Yönetim** > **hiyerarşisi yapılandırma** > **sınırları** ' na tıklayın.  

2.  Değiştirmek istediğiniz sınırı seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

4.  Sınırın **Özellikler** iletişim kutusunda, sınırın **Açıklama** veya **Tür** değerini düzenlemek için **Genel** sekmesini seçin. Bir sınırın kapsamını, sınırın ağ konumlarını düzenleyerek de değiştirebilirsiniz. Örneğin, bir Active Directory sitesi sınırı için yeni bir Active Directory sitesi adı belirtebilirsiniz.  

5.  Bu sınırla ilişkilendirilmiş site sistemlerini görüntülemek için **Site Sistemleri** sekmesini seçin. Bu yapılandırmayı sınırın özelliklerinden değiştiremezsiniz.  

    > [!TIP]  
    > Bir site sistemi sunucusunun bir sınırda site sistemi olarak listelenmesi için, site sistemi sunucusunun bu sınırı içeren en az bir sınır grubu için site sistem sunucusu olarak ilişkilendirilmesi gerekir. Bu ayar bir sınır grubunun **Başvurular** sekmesinde yapılandırılır.  

6.  Bu sınır için sınır grubu üyeliğini değiştirmek için **Sınır Grupları** sekmesini seçin:  

    - Bu sınırı bir veya daha fazla sınır grubuna eklemek için, **Ekle**'yi tıklatın, bir veya daha fazla sınır grubunun onay kutusunu seçip **Tamam**'ı tıklatın.  

    - Bu sınırı bir sınır grubundan kaldırmak için, sınır grubunu seçip **Kaldır**'ı tıklatın.  

7.  Sınır özelliklerini kapatmak ve yapılandırmayı kaydetmek için **Tamam** 'ı tıklatın.  
