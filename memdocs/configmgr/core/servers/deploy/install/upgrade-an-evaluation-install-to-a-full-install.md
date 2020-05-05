---
title: Yükseltme değerlendirme yüklemeleri
titleSuffix: Configuration Manager
description: Bir değerlendirme yüklemesini Configuration Manager tam yüklemesine yükseltmeyi öğrenin.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8a42b2538ff1baaceb6895d371081ac2a444c5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718003"
---
# <a name="upgrade-an-evaluation-installation-of-configuration-manager-to-a-full-installation"></a>Configuration Manager değerlendirme yüklemesini tam yüklemeye yükseltme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Değerlendirme sürümü olarak Configuration Manager yüklediyseniz, 180 gün sonra Configuration Manager konsolu, ürünü kurulum 'daki **Site Bakımı** sayfasından etkinleştirene kadar salt okunurdur. 180 günlük dönemden önce veya sonra herhangi bir zamanda, bir değerlendirme yüklemesini tam yüklemeye yükseltme seçeneğiniz vardır.  

> [!NOTE]  
>  Bir Configuration Manager konsolunu Configuration Manager değerlendirme yüklemesine bağladığınızda, konsol başlık çubuğu, değerlendirme yüklemesi sona erene kadar kalan gün sayısını görüntüler. Gün sayısı otomatik olarak yenilenmez ve yalnızca bir siteye yeni bir bağlantı yaptığınızda güncelleştirilir.  

 Değerlendirme yüklemesi çalıştıran aşağıdaki siteleri yükseltebilirsiniz:  

-   Merkezi yönetim sitesi  
-   Birincil site  

İkincil siteler değerlendirme yüklemeleri olarak değerlendirilmediğinden, birincil üst sitesi tam yüklemeye yükseltildikten sonra ikincil bir siteyi değiştirmeniz gerekmez.  

Bir değerlendirme sürümünü lisanslı bir sürüme yükseltmek için Önkoşullar:  

-   Yükseltme sırasında kullanmak için geçerli bir ürün olmalıdır.  
-   Hesabınızın, sitenin yüklendiği bilgisayarda **yönetici** haklarına sahip olması gerekir.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Configuration Manager bir değerlendirme sürümünü lisanslı bir sürüme yükseltmek için  

1.  Site sunucusunda, Configuration Manager yükleme klasöründen (**%Path%\Bin\X64**) **Setup. exe** ' yi (Configuration Manager Setup) çalıştırın. Kurulum 'U yükleme medyasından çalıştırdığınızda site bakım seçenekleri kullanılamadığından, Configuration Manager klasöründeki site sunucusunda bulunan kurulum kopyasını çalıştırmanız gerekir.  
2.  **Başlamadan önce** sayfasında, **İleri**' yi seçin.  
3.  **Başlarken** sayfasında, **Site bakımı yap veya siteyi sıfırla**' yı seçin ve ardından **İleri**' yi seçin.  
4.  **Site Bakımı** sayfasında, **değerlendirme sürümünü lisanslı bir sürüme yükselt**' i seçin, geçerli bir ürün anahtarı girin ve ardından **İleri**' yi seçin.  
5.  **Microsoft yazılımı lisans koşulları** sayfasında, lisans koşullarını okuyup kabul edin ve ardından **İleri**' yi seçin.  
6.  Sihirbazı tamamladıktan sonra **yapılandırma** sayfasında **Kapat** ' ı seçin.  

    > [!NOTE]  
    >  Yükseltmeniz gereken siteye bağlı kalan bir Configuration Manager konsolunun başlık çubuğu, Konsolu siteye yeniden bağlanana kadar sitenin hala bir değerlendirme sürümü olduğunu gösteriyor olabilir.  
