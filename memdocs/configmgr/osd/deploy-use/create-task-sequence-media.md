---
title: Görev dizisi medyası oluşturma
titleSuffix: Configuration Manager
description: Configuration Manager ortamınızdaki bir hedef bilgisayara bir işletim sistemi dağıtmak için görev dizisi medyası oluşturun.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf7ce32ed9e126b5526c68b7da03cf44d9b5062d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125177"
---
# <a name="create-task-sequence-media"></a>Görev dizisi medyası oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir başvuru bilgisayarından işletim sistemi görüntüsü yakalamak veya Configuration Manager ortamınızdaki bir hedef bilgisayara bir işletim sistemi dağıtmak için medyayı kullanabilirsiniz. Oluşturduğunuz medya bir CD, DVD seti veya bir USB flash sürücü olabilir.

Medya, genellikle bir ağ bağlantısı olmayan veya siteye düşük bant genişliğine sahip bir bağlantısı olan bilgisayarlara bir işletim sistemi dağıtmak için kullanılır. Bununla birlikte, mevcut bir Windows işletim sisteminin dışında bir işletim sistemi dağıtımını başlatmak için medyayı de kullanabilirsiniz. Bu yöntem, işletim sistemi olmadığında, işletim sistemi çalışmadığı veya diski yeniden bölümlemek istediğinizde yararlıdır.

Dağıtım medyası önyüklenebilir medyayı, tek başına medyayı ve önceden hazırlanan medyayı içerir. Medya içeriği, kullandığınız medya türüne bağlı olarak farklılık gösterir. Örneğin, tek başına medya, işletim sistemini dağıtan görev dizisini içerir. Diğer medya türleri, görev dizilerini yönetim noktasından alır.

> [!IMPORTANT]
> Görev sırası medyası oluşturmak için, Configuration Manager konsolunu çalıştırdığınız bilgisayarda bir yönetici olmanız gerekir. Yönetici değilseniz, görev sırası medyası oluşturma Sihirbazı 'nı başlattığınızda yönetici kimlik bilgileri istenir.

## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a>Medyayı yakala

Yakalama medyası, başvuru bilgisayarından bir işletim sistemi görüntüsü yakalamanızı sağlar. Yakalama medyası, başvuru bilgisayarını Başlatan önyükleme görüntüsünü ve işletim sistemi görüntüsünü yakalayan görev dizisini içerir.

## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a>Önyüklenebilir medya

Önyüklenebilir medya aşağıdaki bileşenleri içerir:

- Önyükleme görüntüsü
- İsteğe bağlı [başlatma öncesi komutları](../understand/prestart-commands-for-task-sequence-media.md) ve gerekli dosyaları
- Configuration Manager ikililer

Hedef bilgisayar başladığında, ağa bağlanır ve görev dizisini, işletim sistemi görüntüsünü ve diğer tüm gerekli içeriği ağdan alır. Görev sırası medyada olmadığından, medyayı yeniden oluşturmak zorunda kalmadan görev dizisini veya içeriği değiştirebilirsiniz.  

> [!IMPORTANT]  
> Önyüklenebilir medyadaki paketler şifrelenmez. Paket içeriklerinin yetkisiz kullanıcılardan güvenli olduğundan emin olmak için medyaya parola ekleme gibi uygun güvenlik önlemlerini alın.  

Sürüm 2006 ' den başlayarak önyüklenebilir medya, bulut tabanlı içeriği indirebilir. Cihazın hala yönetim noktasına bir intranet bağlantısı olması gerekir. İçerik özellikli bir bulut yönetimi ağ geçidi (CMG) veya bulut dağıtım noktasından içerik alabilir.<!--6209223--> Daha fazla bilgi için bkz. [bulut tabanlı Içerik desteği](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a>Önceden hazırlanan medya

Önceden hazırlanan medya, sağlama işleminden önce bir sabit diske önyüklenebilir medya ve bir işletim sistemi görüntüsü uygulamanıza olanak tanır. Önceden hazırlanan medya bir Windows Image (WıM) dosyasıdır. Üretici, yapı sürecinde bunu çıplak bilgisayara yükleyebilir. Ya da bunu, üretim Configuration Manager ortamına bağlı olmayan bir hazırlama merkezinde kullanabilirsiniz.

Önceden hazırlanan medya, hedef bilgisayarı başlatmak için kullanılan önyükleme görüntüsünü ve hedef bilgisayara uygulanan işletim sistemi görüntüsünü içerir. Önceden hazırlanan medyaya dahil edilecek uygulamaları, paketleri ve sürücü paketlerini de belirtebilirsiniz. İşletim sistemini dağıtan görev dizisi medyaya dahil değildir. Önceden hazırlanan medya kullanan bir görev dizisini dağıttığınızda istemci, ilk olarak geçerli içerik için yerel görev sırası önbelleğini denetler. İçerik bulunamazsa veya yeniden değiştirilmişse, istemci içeriği bir dağıtım noktasından veya eşinden indirir.  

Bilgisayarı kullanıcıya göndermeden önce yeni bir bilgisayarın sabit sürücüsüne önceden hazırlanan medya uygularsınız. Önceden hazırlanan medyayı uyguladıktan sonra bilgisayar ilk kez başlatıldığında, bilgisayar Windows PE 'de başlatılır. İşletim sistemi dağıtım işlemini tamamlayan görev dizisini bulmak için bir yönetim noktasına bağlanır.  

> [!IMPORTANT]
> Önceden hazırlanan medyadaki paketler şifrelenmez. Paket içeriklerinin yetkisiz kullanıcılardan güvenli olduğundan emin olmak için medyaya parola ekleme gibi uygun güvenlik önlemlerini alın.

## <a name="standalone-media"></a><a name="BKMK_PlanStandaloneMedia"></a>Tek başına medya

Tek başına medya, işletim sistemini dağıtmak için gereken her şeyi içerir. Bu içerik, görev dizisini ve diğer tüm gerekli içeriği içerir. Medyada her şey olduğundan, gerekli disk alanı diğer medya türlerine göre daha büyük.

## <a name="considerations-when-using-https"></a>HTTPS kullanırken dikkat edilecek noktalar

Yönetim noktalarınızı ve dağıtım noktalarınızı HTTPS kullanmak üzere yapılandırdığınızda, merkezi yönetim sitesinde değil, birincil sitede Önyükleme medyası ve önceden hazırlanmış medya oluşturun. Ayrıca, medyanın dinamik veya site tabanlı olarak mı yapılandırılacağını belirlemenize yardımcı olması için aşağıdaki noktayı göz önünde bulundurun:  

- Medyayı dinamik medya olarak yapılandırmak için tüm birincil sitelerin, medyayı oluşturduğunuz sitenin kök sertifika yetkilisine (CA) sahip olması gerekir. Hiyerarşinizdeki tüm birincil sitelerde kök CA'yı içe aktarabilirsiniz.  

- Configuration Manager hiyerarşinizdeki birincil siteler farklı kök CA 'Lar kullandığında, her sitede site tabanlı medya kullanmanız gerekir.  

## <a name="next-steps"></a>Sonraki adımlar

- [Yakalama ortamı oluşturma](create-capture-media.md)

- [Önyüklenebilir ortam oluşturma](create-bootable-media.md)

- [Önceden hazırlanan ortam oluşturma](create-prestaged-media.md)

- [Tek başına medya oluşturma](create-stand-alone-media.md)
