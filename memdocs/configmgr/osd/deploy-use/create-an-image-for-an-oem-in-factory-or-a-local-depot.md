---
title: Fabrikada veya yerel depoda OEM için görüntü oluşturma
titleSuffix: Configuration Manager
description: Bir işletim sistemini tam olarak sağlanmamış bir bilgisayara dağıtırken ağ trafiğini azaltmak için önceden hazırlanan medya dağıtımlarını kullanın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125449"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Configuration Manager ile bir OEM veya yerel deposu için bir görüntü oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager önceden hazırlanan medya dağıtımları, bir işletim sistemini tam olarak sağlanmamış bir bilgisayara dağıtmanızı sağlar. Önceden hazırlanan medya bir Windows Image (WıM) dosyasıdır. Üretici (OEM) bunu çıplak bir bilgisayara yükleyebilir veya üretim ortamınızdan ayrı bir hazırlama merkezinde kullanabilirsiniz.

Önyükleme görüntüsü ve işletim sistemi görüntüsü zaten hedef bilgisayarda olduğundan, bu dağıtım yöntemi ağ trafiğini azaltabilir. Önceden hazırlanan medyaya dahil edilecek uygulamaları, paketleri ve sürücü paketlerini de belirtebilirsiniz. İşletim sistemini bilgisayara yükledikten sonra, görev sırası öncelikle uygulamalar, paketler veya sürücü paketleri için önceden hazırlanan önbelleği denetler. Gerekli içeriği bulamazsa veya çevrimiçi olarak yeni bir düzeltme varsa, görev sırası içeriği bir dağıtım noktasından indirir.

Önceden hazırlanmış medyayı aşağıdaki işletim sistemi dağıtım senaryolarında kullanın:

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)

- [Mevcut bir bilgisayarı değiştirme ve ayarları aktarma](replace-an-existing-computer-and-transfer-settings.md)

Bu işletim sistemi dağıtım senaryolarından birindeki adımları doldurun. Ardından aşağıdaki bölümleri kullanarak önceden hazırlanmış medyayı hazırlayın ve oluşturun.

## <a name="configure-deployment-settings"></a>Dağıtım ayarlarını yapılandırma

Dağıtımın **dağıtım ayarları** sayfasında, **aşağıdaki için kullanılabilir yap** ayarı için aşağıdaki seçeneklerden birini belirleyin:

- İstemcileri, medyayı ve PXE 'yi Configuration Manager

- Yalnızca medya ve PXE

- Yalnızca medya ve PXE (gizli)

## <a name="create-the-prestaged-media"></a>Önceden hazırlanmış medya oluşturma

OEM veya yerel deponuza göndermek üzere önceden hazırlanmış medya dosyasını oluşturun. Daha fazla bilgi için bkz. [Configuration Manager ile önceden hazırlanmış medya oluşturma](create-prestaged-media.md).

## <a name="send-the-prestaged-media-file"></a>Önceden hazırlanan medya dosyasını gönder

Medyayı bilgisayarlara önceden hazırlamak için OEM 'ye veya yerel deposu gönderin. Görüntü dosyası, bilgisayardaki biçimlendirilen bir sabit diske uygulanır.

## <a name="deliver-the-computer"></a>Bilgisayarı teslim et

Bilgisayarı bir kullanıcıya teslim ettiğinizde ve ilk kez açmak için:

1. Bilgisayar önceden hazırlanan Önyükleme görüntüsüyle başlar.

1. Geçerli olduğundan emin olmak için önceden hazırlanmış medyada bir karmayı denetler.

1. Bilgisayar, işlemi gerçekleştirmek için kullanılabilir görev dizileri için yönetim noktasına bağlanır.

## <a name="next-steps"></a>Sonraki adımlar

[İşletim sistemi dağıtımı için kullanıcı deneyimleri](../understand/user-experience.md)
