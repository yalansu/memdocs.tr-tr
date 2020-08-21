---
title: Yazılım güncelleştirmeleri için en iyi uygulamalar
titleSuffix: Configuration Manager
description: Configuration Manager yazılım güncelleştirmeleri için bu en iyi yöntemleri kullanın.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 3a48ce044f3d1aecbebf2ba93e936dd34b904140
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696647"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Configuration Manager 'de yazılım güncelleştirmeleri için en iyi uygulamalar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, Configuration Manager yazılım güncelleştirmeleri için en iyi yöntemleri içerir. Bilgiler ilk yüklemeye yönelik en iyi yöntemlere ve devam eden işlemlere göre sıralanır.  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a> En iyi yükleme uygulamaları  

Configuration Manager ' de yazılım güncelleştirmelerini yüklerken aşağıdaki en iyi yöntemleri kullanın.  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a> Yazılım güncelleştirme noktaları için paylaşılan WSUS veritabanı kullanma  

Bir birincil siteye birden çok yazılım güncelleştirme noktası yüklediğinizde aynı Active Directory ormanındaki her yazılım güncelleştirme noktası için aynı WSUS veritabanını kullanın. Aynı veritabanını paylaşıyorsanız, istemciler yeni bir yazılım güncelleştirme noktasına geçiş yaparken karşılaşabileceğiniz istemci ve ağ performansı etkilerini önemli ölçüde azaltır, ancak tamamen ortadan kaldırmaz. Bir istemci eski yazılım güncelleştirme noktasıyla bir veritabanını paylaşan yeni bir yazılım güncelleştirme noktasına geçtiğinde bir Delta taraması devam ediyor, ancak tarama WSUS sunucusunun kendi veritabanına sahip olması durumunda olacak kadar küçüktür. Yazılım güncelleştirme noktası değiştirme hakkında daha fazla bilgi için bkz. [yazılım güncelleştirme noktası geçişi](plan-for-software-updates.md#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Ayrıca, yazılım güncelleştirme noktaları için paylaşılan bir WSUS veritabanı kullandığınızda yerel WSUS içerik klasörlerini de paylaşabilirsiniz.  

WSUS veritabanını paylaşma hakkında daha fazla bilgi için aşağıdaki blog gönderilerine bakın:  

- [Configuration Manager yazılım güncelleştirme noktaları için paylaşılan bir SUSDB uygulama](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Configuration Manager kullanırken bir içerik veritabanını paylaşan birden çok WSUS örneği Için dikkat edilmesi gerekenler](/archive/blogs/wsus/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb).


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a> Configuration Manager ve WSUS aynı SQL Server kullanırken varsayılan örneği kullanmak için bir adlandırılmış örnek ve diğerini kullanacak şekilde yapılandırın  

Configuration Manager ve WSUS veritabanları aynı SQL Server örneğini paylaşıyorsa, iki uygulama arasındaki kaynak kullanımını kolayca belirleyemiyoruz. Configuration Manager ve WSUS için farklı SQL Server örnekleri kullanın. Bu yapılandırma, her bir uygulama için oluşabilecek kaynak kullanımı sorunlarını gidermeyi ve tanılamayı kolaylaştırır.  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a> "Güncelleştirmeleri yerel olarak depola" ayarını belirtin  

WSUS 'u yüklerken, **güncelleştirmeleri yerel olarak depolamak**için ayarı seçin. Bu ayar, WSUS 'nin yazılım güncelleştirmeleriyle ilişkili lisans koşullarını indirmesine neden olur. Eşitleme işlemi sırasında koşulları indirir ve WSUS sunucusunun yerel sabit sürücüsünde depolar. Bu ayarı seçmezseniz, istemci bilgisayarlar lisans koşulları olan yazılım güncelleştirmeleri için uyumluluk taramalarının başarısız olmasına neden olabilir. Yazılım güncelleştirme noktasının **WSUS Eşitleme Yöneticisi** bileşeni, bu ayarın her 60 dakikada bir varsayılan olarak etkinleştirildiğini doğrular.  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a> İşletimsel En Iyi uygulamalar  

Yazılım güncelleştirmelerini kullanırken aşağıdaki en iyi yöntemleri kullanın:  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a> Yazılım güncelleştirmelerini tek bir yazılım güncelleştirme dağıtımında 1000 ile sınırlayın  

Yazılım güncelleştirme sayısını her yazılım güncelleştirmesi dağıtımında 1000 ile sınırlayın. Bir otomatik dağıtım kuralı oluşturduğunuzda, belirtilen ölçütün 1000 ' den fazla yazılım güncelleştirmesi sonucu içermediğinden emin olun. Yazılım güncelleştirmelerini el ile dağıtıyorsanız 1000 'den fazla güncelleştirme seçmeyin.  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a> "Salı Düzeltme Eki" ve genel dağıtımlar için her ADR çalıştırıldığında yeni bir yazılım güncelleştirme grubu oluşturun  

Bir dağıtımda 1000 yazılım güncelleştirmesi sınırlaması vardır. Bir otomatik dağıtım kuralı (ADR) oluşturduğunuzda, kural her çalıştığında varolan bir güncelleştirme grubunun mi kullanılacağını, yoksa yeni bir güncelleştirme grubu mu oluşturulacağını belirtirsiniz. Birden çok yazılım güncelleştirmesi ile sonuçlanan bir ADR 'de ölçüt belirtirseniz ve kural yinelenen bir zamanlamaya göre çalışıyorsa, kural her çalıştığında yeni bir yazılım güncelleştirme grubu oluşturun. Bu davranış, dağıtımın dağıtım başına 1000 yazılım güncelleştirmesi sınırını geçmesini önler.  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a> Endpoint Protection tanım güncelleştirmeleri için ADRs için mevcut bir yazılım güncelleştirme grubu kullanın  

Endpoint Protection tanım güncelleştirmelerini sık aralıklarla dağıtmak için ADR kullandığınızda, her zaman mevcut bir yazılım güncelleştirme grubunu kullanın. Aksi halde ADR, zaman içinde yüzlerce yazılım güncelleştirme grubu oluşturuyor olabilir. Tanım güncelleştirme yayımcıları genellikle tanım güncelleştirmelerini, yenisiyle değiştirildikten sonra dört daha yeni güncelleştirme ile sona ermek üzere ayarlar. Bu nedenle, ADR tarafından oluşturulan yazılım güncelleştirme grubu hiçbir şekilde yayımcı için dörtten fazla tanım güncelleştirmesi içermez: bir etkin ve üç yenisiyle değiştirilmiştir.  



## <a name="see-also"></a>Ayrıca Bkz.  
 [Yazılım güncelleştirmelerini planlama](plan-for-software-updates.md)