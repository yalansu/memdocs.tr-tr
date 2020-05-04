---
title: Görev dizisi medyası oluşturma
titleSuffix: Configuration Manager
description: Configuration Manager ortamınızdaki bir hedef bilgisayara bir işletim sistemi dağıtmak için görev dizisi medyası oluşturun.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711031"
---
# <a name="create-task-sequence-media"></a>Görev dizisi medyası oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir başvuru bilgisayarından işletim sistemi görüntüsü yakalamak veya Configuration Manager ortamınızdaki bir hedef bilgisayara bir işletim sistemi dağıtmak için medyayı kullanabilirsiniz. Oluşturduğunuz medya bir CD, DVD seti veya bir USB flash sürücü olabilir.  

Medya, genellikle bir ağ bağlantısı bulunmayan veya Configuration Manager sitenize düşük bant genişliğine sahip bir bağlantısı olan hedef bilgisayarlarda işletim sistemi dağıtmak için kullanılır. Bununla birlikte, mevcut bir Windows işletim sisteminin dışında bir işletim sistemi dağıtımını başlatmak için medyayı de kullanabilirsiniz. Bu yöntem, mevcut bir işletim sistemi olmadığında, işletim sistemi çalışmadığı veya sabit diski yeniden bölümlemek istediğinizde yararlıdır.  

Dağıtım medyası, önyüklenebilir medyayı, tek başına medyayı ve önceden hazırlanan medyayı içerir. Medya içeriği, kullandığınız medya türüne bağlı olarak farklılık gösterir. Örneğin, tek başına medya, işletim sistemini dağıtan görev dizisini içerir. Diğer medya türleri, görev dizilerini yönetim noktasından alır.  

> [!IMPORTANT]  
> Görev sırası medyası oluşturmak için, Configuration Manager konsolunu çalıştırdığınız bilgisayarda bir yönetici olmanız gerekir. Yönetici değilseniz, görev sırası medyası oluşturma Sihirbazı 'nı başlattığınızda yönetici kimlik bilgileri istenir.  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a>Medyayı yakala

Yakalama medyası, başvuru bilgisayarından bir işletim sistemi görüntüsü yakalamanızı sağlar. Yakalama medyası, başvuru bilgisayarını Başlatan önyükleme görüntüsünü ve işletim sistemi görüntüsünü yakalayan görev dizisini içerir.

Yakalama medyası oluşturma hakkında daha fazla bilgi için bkz. [yakalama medyası oluşturma](create-capture-media.md).  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a>Önyüklenebilir medya

Önyüklenebilir medya aşağıdaki bileşenleri içerir:

- Önyükleme görüntüsü
- İsteğe bağlı [başlatma öncesi komutları](../understand/prestart-commands-for-task-sequence-media.md) ve gerekli dosyaları
- Configuration Manager ikililer

Hedef bilgisayar başladığında, ağa bağlanır ve görev dizisini, işletim sistemi görüntüsünü ve diğer tüm gerekli içeriği ağdan alır. Görev sırası medyada olmadığından, medyayı yeniden oluşturmak zorunda kalmadan görev dizisini veya içeriği değiştirebilirsiniz.  

> [!IMPORTANT]  
> Önyüklenebilir medyadaki paketler şifrelenmez. Paket içeriklerinin yetkisiz kullanıcılardan güvenli olduğundan emin olmak için medyaya parola ekleme gibi uygun güvenlik önlemlerini alın.  

Önyüklenebilir medya oluşturma hakkında daha fazla bilgi için [önyüklenebilir medya oluşturun](create-bootable-media.md).  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a>Önceden hazırlanan medya

Önceden hazırlanan medya, sağlama işleminden önce bir sabit diske önyüklenebilir medya ve bir işletim sistemi görüntüsü uygulamanıza olanak tanır. Önceden hazırlanan medya bir Windows Image (WıM) dosyasıdır. Üretici tarafından veya hazırlama merkezinizde üretim Configuration Manager ortamına bağlı olmayan çıplak bir bilgisayara yüklenebilir.  

Önceden hazırlanan medya, hedef bilgisayarı başlatmak için kullanılan önyükleme görüntüsünü ve hedef bilgisayara uygulanan işletim sistemi görüntüsünü içerir. Önceden hazırlanan medyaya dahil edilecek uygulamaları, paketleri ve sürücü paketlerini de belirtebilirsiniz. İşletim sistemini dağıtan görev dizisi medyaya dahil değildir. Önceden hazırlanan medya kullanan bir görev dizisini dağıttığınızda istemci, ilk olarak geçerli içerik için yerel görev sırası önbelleğini denetler. İçerik bulunamazsa veya yeniden değiştirilmişse, istemci içeriği bir dağıtım noktasından veya eşinden indirir.  

Önceden hazırlanmış medya, yeni bir bilgisayar son kullanıcıya gönderilmeden önce o bilgisayarın sabit sürücüsüne uygulanır. Önceden hazırlanan medyayı uyguladıktan sonra bilgisayar ilk kez başlatıldığında, bilgisayar Windows PE 'de başlatılır. İşletim sistemi dağıtım işlemini tamamlayan görev dizisini bulmak için bir yönetim noktasına bağlanır.  

> [!IMPORTANT]  
> Önceden hazırlanan medyadaki paketler şifrelenmez. Paket içeriklerinin yetkisiz kullanıcılardan güvenli olduğundan emin olmak için medyaya parola ekleme gibi uygun güvenlik önlemlerini alın.  

Önceden hazırlanmış medya oluşturma hakkında daha fazla bilgi için bkz. [önceden hazırlanmış medya oluşturma](create-prestaged-media.md).  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a>Tek başına medya

Tek başına medya, işletim sistemini dağıtmak için gereken her şeyi içerir. Bu içerik, görev dizisini ve diğer tüm gerekli içeriği içerir. İşletim sistemini dağıtmak için gerekli olan her şey tek başına medyada depolandığından, tek başına medya için gereken disk alanı diğer medya türlerine göre daha büyük olur.  

Tek başına medyanın nasıl oluşturulacağı hakkında daha fazla bilgi için bkz. [tek başına medya oluşturma](create-stand-alone-media.md).  


## <a name="considerations-when-using-https"></a>HTTPS kullanırken dikkat edilecek noktalar

Yönetim noktalarınızı ve dağıtım noktalarınızı HTTPS kullanmak üzere yapılandırdığınızda, merkezi yönetim sitesinde değil, birincil sitede Önyükleme medyası ve önceden hazırlanmış medya oluşturun. Ayrıca, medyanın dinamik veya site tabanlı olarak mı yapılandırılacağını belirlemenize yardımcı olması için aşağıdaki noktayı göz önünde bulundurun:  

- Medyayı dinamik medya olarak yapılandırmak için tüm birincil sitelerin, medyayı oluşturduğunuz sitenin kök sertifika yetkilisine (CA) sahip olması gerekir. Hiyerarşinizdeki tüm birincil sitelerde kök CA'yı içe aktarabilirsiniz.  

- Configuration Manager hiyerarşinizdeki birincil siteler farklı kök CA 'Lar kullandığında, her sitede site tabanlı medya kullanmanız gerekir.  
