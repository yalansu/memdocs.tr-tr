---
title: Cihaz ve kullanıcı kaynaklarını bulma
titleSuffix: Configuration Manager
description: Bulma işlemi ve bulma verileri kayıtlarına genel bir bakış edinin.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718374"
---
# <a name="run-discovery-for-configuration-manager"></a>Configuration Manager için bulmayı Çalıştır

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yönetebileceğiniz cihaz ve kullanıcı kaynaklarını bulmak için Configuration Manager ' de bir veya daha fazla bulma yöntemi kullanırsınız. Ayrıca, bulma işlemini ortamınızdaki ağ altyapısını tanımlamak için de kullanabilirsiniz. Farklı şeyleri keşfedebilmeniz için kullanabileceğiniz çeşitli farklı yöntemler vardır ve her yöntemin kendi yapılandırmalarına ve kısıtlamalarına sahip olması gerekir.  

## <a name="overview-of-discovery"></a>Bulma işlemine genel bakış  
 Bulma işlemi, Configuration Manager yönetebileceğiniz şeyleri öğreniyor. Kullanılabilecek bulma yöntemleri şunlardır:  

-   Active Directory Orman Saptama  

-   Active Directory Grup Saptama  

-   Active Directory Sistem Saptama  

-   Active Directory Kullanıcı Saptama  

-   Sistem Durumu Bulma  

-   Ağ Bulma  

-   Sunucu Bulma  

> [!TIP]  
>  [Configuration Manager bulma yöntemleri hakkında](../../../../core/servers/deploy/configure/about-discovery-methods.md)' de bireysel bulma yöntemleri hakkında bilgi edinebilirsiniz.  
>   
>  Hangi yöntemlerin kullanılacağını seçerken yardım almak için ve hiyerarşinizdeki sitelerde, bkz. [Configuration Manager için kullanılacak bulma yöntemlerini seçme](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Çoğu bulma yöntemini kullanmak için, yöntemi bir sitede etkinleştirmeniz ve belirli ağ veya Active Directory konumları arayacak şekilde ayarlamanız gerekir. Çalıştığında, Configuration Manager yönetebileceği cihazlar veya kullanıcılar hakkında bilgi için belirtilen konumu sorgular. Bir bulma yöntemi bir kaynak hakkında başarıyla bilgi bulduğunda, bu bilgileri bulgu verileri kaydı (DDR) adlı bir dosyaya koyar. Bu dosya daha sonra birincil veya merkezi yönetim sitesi tarafından işlenir. Bir DDR dosyasının işlenmesi, site veritabanında yeni bulunan kaynaklar için yeni bir kayıt oluşturur veya mevcut kayıtları yeni bilgilerle güncelleştirir.  

 Bazı bulma yöntemleri büyük miktarda ağ trafiği oluşturabilir ve bunların ürettiği DDR 'ler, işleme sırasında CPU kaynaklarının önemli bir kullanımına neden olabilir. Bu nedenle, yalnızca hedeflerinizi karşılamak için gerekli olan bulma yöntemlerini kullanmayı planlayın. Yalnızca bir veya iki bulma yöntemini kullanarak başlayabilir, sonra ortamınızdaki bulma düzeyini genişletmek için denetimli bir şekilde ek yöntemler etkinleştirebilirsiniz.  

 Bulma bilgileri site veritabanına eklendikten sonra, bu bilgiler, keşfedildiği veya işlendiği durumlar ne olursa olsun, hiyerarşideki her bir siteye çoğaltılır. Bu nedenle, farklı sitelerde bulma yöntemleri için farklı zamanlamalar ve ayarlar ayarlayabilmeniz sırasında, yalnızca tek bir sitede belirli bir bulma yöntemi çalıştırabilirsiniz. Bu, yinelenen bulma eylemleri aracılığıyla ağ bant genişliğinin kullanımını azaltır ve çok sayıda sitede gereksiz keşif verilerinin işlenmesini azaltır.  

 Yönetim görevleri için kaynakları mantıksal olarak gruplandıran özel koleksiyonlar ve sorgular oluşturmak için bulma verilerini kullanabilirsiniz. Örneğin:  

-   İstemci yüklemelerini iletme veya yükseltme.  

-   Kullanıcılara veya cihazlara içerik dağıtma.  

-   İstemci ayarları ve ilgili yapılandırmaların dağıtımı.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a>Bulma verileri kayıtları hakkında  
 DDR 'ler bir bulma yöntemi tarafından oluşturulan dosyalardır. Bilgisayarlar, kullanıcılar ve bazı durumlarda ağ altyapısı gibi Configuration Manager yönetebileceğiniz bir kaynakla ilgili bilgiler içerirler. Bunlar birincil sitelerde veya merkezi yönetim sitelerinde işlenir. DDR 'deki kaynak bilgileri veritabanına girildikten sonra, DDR silinir ve bilgiler hiyerarşideki tüm sitelere genel veriler olarak çoğaltılır.  

 DDR'nin işlendiği site, içerdiği bilgilere bağlıdır:  

-   Veritabanında olmayan yeni bulunan kaynakların DDR 'leri hiyerarşinin üst düzey sitesinde işlenir. Üst düzey site veritabanında yeni bir kaynak kaydı oluşturur ve benzersiz bir tanımlayıcı atar. DDR 'ler üst düzey siteye ulaşana kadar dosya tabanlı çoğaltma ile aktarılır.  

-   Daha önce bulunmuş nesnelerin DDR'leri birincil sitelerde işlenir. DDR zaten veritabanında olan bir kaynakla ilgili bilgiler içerdiğinde alt birincil siteler DDR'leri merkezi yönetim sitesine aktarmaz.  

-   İkincil siteler DDR 'leri işlemez ve bunları her zaman dosya tabanlı çoğaltma yoluyla üst birincil sitelerine aktarır.  

DDR dosyaları .ddr uzantısı ile tanımlanır ve yaklaşık boyutları 1 KB'tır.  

## <a name="get-started-with-discovery"></a>Bulma kullanmaya başlama:  
 Bulmayı ayarlamak için Configuration Manager konsolunu kullanmadan önce Yöntemler, neler yapabilecekleri ve bazı sınırlamalar için aralarındaki farkları anlamanız gerekir.  

Aşağıdaki konular bulma yöntemlerini başarıyla kullanmanıza yardımcı olacak bir temel oluşturabilir:  

-   [Configuration Manager için bulma yöntemleri hakkında](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Configuration Manager için kullanılacak bulma yöntemlerini seçin](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Ardından, kullanmak istediğiniz yöntemleri anladığınızda, [Configuration Manager için bulma yöntemlerini yapılandırma](../../../../core/servers/deploy/configure/configure-discovery-methods.md)bölümünde her bir yöntemi ayarlama kılavuzunu bulun.  
