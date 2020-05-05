---
title: Fabrikada veya yerel depoda OEM için görüntü oluşturma
titleSuffix: Configuration Manager
description: Bir işletim sistemini tam olarak sağlanmamış bir bilgisayara dağıtırken ağ trafiğini azaltmak için önceden hazırlanan medya dağıtımlarını kullanın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c4d445d18b9e239ace673199f6a7d0f26d10a42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723001"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Configuration Manager ile bir OEM veya yerel deposu için bir görüntü oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager önceden hazırlanan medya dağıtımları, bir işletim sistemini tam olarak sağlanmamış bir bilgisayara dağıtmanızı sağlar. Önceden hazırlanan medya, üretici (OEM) tarafından veya Configuration Manager ortamına bağlı olmayan bir kuruluş hazırlama merkezinde çıplak bir bilgisayara yüklenebilen bir Windows Imaging Format (WıM) dosyasıdır. Configuration Manager ortamında, bilgisayar, medya tarafından sağlanan önyükleme görüntüsünü kullanarak başlar, önceden hazırlanmış medya üzerinde geçerli olduğundan emin olmak için bir karma denetimi çalıştırılır ve ardından bilgisayar, indirme işlemini tamamlayan kullanılabilir görev dizileri için site yönetim noktasına bağlanır.


Önyükleme görüntüsü ve işletim sistemi görüntüsü zaten hedef bilgisayarda olduğundan, bu dağıtım yöntemi ağ trafiğini azaltabilir. Önceden hazırlanmış medyanın dahil edileceği uygulamaları, paketleri ve sürücü paketlerini belirtebilirsiniz. Bilgisayara işletim sistemi yüklendikten sonra, yerel görev dizisi önbelleğinde ilk önce uygulamalar, paketler veya sürücü paketleri denetlenir; içerik bulunamazsa veya değiştirilmişse, içerik önceden hazırlanmış medyada yapılandırılan dağıtım noktasından indirilir ve sonra yüklenir.  

 Önceden hazırlanmış medyayı aşağıdaki işletim sistemi dağıtım senaryolarında kullanabilirsiniz:  

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)  

- [Mevcut bir bilgisayarı değiştirme ve ayarları aktarma](replace-an-existing-computer-and-transfer-settings.md)  

  İşletim sistemi dağıtım senaryolarından birindeki adımları tamamlayın ve ardından aşağıdaki bölümleri kullanarak önceden hazırlanmış medyayı hazırlayın ve oluşturun.  

## <a name="configure-deployment-settings"></a>Dağıtım ayarlarını yapılandırma  
 İşletim sistemi dağıtım işlemini başlatmak üzere önceden hazırlanmış medya kullandığınızda, işletim sistemini medya tarafından kullanılabilir hale getirmek için dağıtımı yapılandırmanız gerekir. Bu yapılandırmayı Yazılım Dağıtma Sihirbazı’nın **Dağıtım Ayarları** sayfasında veya dağıtımın özelliklerindeki **Dağıtım Ayarları** sekmesinde yapabilirsiniz.  **Aşağıdakiler için kullanılabilir yap** ayarı için aşağıdakilerden birini yapılandırın:  

-   **Configuration Manager istemcileri, medya ve PXE**  

-   **Yalnızca medya ve PXE**  

-   **Yalnızca medya ve PXE (gizli)**  

## <a name="create-the-prestaged-media"></a>Önceden hazırlanmış medya oluşturma  
 OEM veya yerel deponuza göndermek üzere önceden hazırlanmış medya dosyasını oluşturun. Daha fazla bilgi için bkz. [Configuration Manager ile önceden hazırlanmış medya oluşturma](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Önceden hazırlanmış medya dosyasını OEM veya yerel dosya gönderme  
 Medyayı OEM veya yerel deponuza göndererek bilgisayarları önceden hazırlayın. Önceden hazırlanmış medya dosyası, bilgisayarda biçimlendirilmiş bir sabit diske uygulanır.  

## <a name="start-the-computer-to-install-the-operating-system"></a>İşletim sistemini yüklemek için bilgisayarı başlatma  
 Önceden hazırlanmış medya dosyası bilgisayarlara uygulanır. Bilgisayar ilk kez başlatıldığında, işletim sistemi yükleme işlemi başlatılır.  
