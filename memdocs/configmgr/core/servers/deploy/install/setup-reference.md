---
title: Kurulum başvurusu
titleSuffix: Configuration Manager
description: Bir Configuration Manager sitesini veya hiyerarşisini yüklemeye hazırlanmanıza yardımcı olması için bu başvuruyu gözden geçirin.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff2d5c6df0da6b25395858a55ef1ee8a3c0da00b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906533"
---
# <a name="reference-for-configuration-manager-setup"></a>Configuration Manager Kurulum başvurusu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Kurulum aşağıdaki bölümlerde ayrıntılı olarak açıklanan birkaç konuya bağlantı sağlar. Burada sunulan bilgiler, bir Configuration Manager sitesini veya hiyerarşisini yüklemeye hazırlamanıza ve yükleme sırasında yapmanız gereken bazı kararlara hazırlanmanıza yardımcı olabilir.  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a>Başlamadan önce  
Yeni Configuration Manager sitelerini yüklemeden önce, başarılı bir dağıtım tasarımının aşamasını ayarlamanıza yardımcı olabilecek aşağıdaki bilgileri gözden geçirdiğinizden emin olun:  

-   [Configuration Manager'ın temelleri](../../../../core/understand/fundamentals.md)  
-   [Configuration Manager altyapısını planlayın](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Configuration Manager siteleri yüklemeye hazırlanma](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a>Sunucu hazırlığını değerlendirme  
Yeni bir site yüklemesine başlamadan önce, site için kullanmayı planladığınız site sunucusunun ve uzak site sistemi sunucularının (örneğin, site veritabanını barındıran sunucu) tüm önkoşul yapılandırmalarına uygun olduğundan emin olun. Belge kitaplığındaki bu konular şu konularda yardımcı olabilir:  

-   [Configuration Manager için desteklenen yapılandırmalar](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Önkoşul denetleyicisi](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Diğer işletim sistemlerinin istemcileri  
Configuration Manager için istemci yazılımını, aşağıdaki işletim sistemleri için Microsoft Indirme Merkezi ' nden indirebilirsiniz:  

- macOS (Apple)
- UNIX
- Linux

Kullandığınız Configuration Manager sürümü için istemcileri indirmek üzere aşağıdaki bağlantıları kullanın:  

- [Microsoft uç nokta Configuration Manager-macOS Istemcisi (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Ek işletim sistemleri için Microsoft Configuration Manager istemcileri](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Kullanım verileri düzeyleri ve ayarları  
İlk Configuration Manager sitenizi yüklediğinizde, Configuration Manager site sunucusundaki **hizmet bağlantı noktası**olan yeni bir site sistem rolünü otomatik olarak yükler ve yapılandırır. Hizmet bağlantı noktası şu varsayılan ayarlara sahiptir:  

-   **Çevrimiçi** mod (çevrimdışı mod da kullanılabilir)  
-   **Geliştirilmiş** veri toplama düzeyi (diğer iki veri toplama düzeyi (temel ve tam) de mevcuttur)  

Hizmet bağlantı noktası site sistemi rolü çevrimiçi olduğunda, Microsoft otomatik olarak tanılama ve kullanım bilgilerini Internet üzerinden toplayabilir. Toplanan bilgiler aşağıdaki konularda yardımcı olur:  

-   Sorunları tanımlama ve giderme  
-   Ürünlerimizi ve hizmeti geliştirme  
-   Kullandığınız Configuration Manager sürümü için geçerli olan Configuration Manager güncelleştirmelerini tanımlama  

### <a name="levels-of-data-collection"></a>Veri toplama düzeyleri  
Veri toplama şu üç düzeyi içerir:

-   **Temel** , site sayısı ve hangi Configuration Manager özelliklerinin etkinleştirildiği gibi kurulum ve yükseltme ile ilgili veriler içerir. Kişisel olarak tanımlanabilir bilgiler aktarılmaz.  

-   **Gelişmiş** , temel düzey ayarda verileri içerir ve ayrıca, bir sistem veya uygulama kilitlenmesi gerçekleştiğinde, her bir özelliğin nasıl kullanıldığı (sıklık ve süre) ve sunucunuzun bellek durumu gibi gelişmiş tanı bilgilerini iletir. Hiçbir kişisel olarak tanımlanabilir veri aktarılmaz.  

-   **Tam** , temel ve Gelişmiş düzey ayarlarındaki verileri içerir ve ayrıca sistem dosyaları ve bellek anlık görüntüleri gibi gelişmiş tanılama bilgileri de gönderir. Bu seçenek, kişisel olarak tanımlanabilir bilgiler içerebilir, ancak bu bilgileri sizi tanımlamak veya sizinle iletişim kurmak ya da size reklam sağlamak için kullanmayacağız.  

Her düzey tarafından toplanan ayrıntıların açıklanması dahil olmak üzere daha fazla bilgi için bkz. [Configuration Manager Için tanılama ve kullanım verileri](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Daha fazla bilgi için bkz. [Microsoft gizlilik bildirimi](https://privacy.microsoft.com/privacystatement).
