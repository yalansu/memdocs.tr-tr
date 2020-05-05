---
title: Genişletilmiş birlikte çalışabilirlik istemcisi
titleSuffix: Configuration Manager
description: Geçerli bir dal sitesi olan statik bir Configuration Manager istemcisinin uzun süreli desteği için genişletilmiş birlikte çalışabilirlik istemcisini kullanma hakkında bilgi edinin.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61296321251be45cfa0449a3e4f21ba79a024753
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722784"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Güncel Dalı sitesinin gelecek sürümleriyle genişletilmiş birlikte çalışabilirlik için Configuration Manager istemci yazılımını kullanın

*Uygulama hedefi: Configuration Manager (geçerli dal)*  

İş gereksinimleri, bazı cihazlarda Configuration Manager istemcisini düzenli olarak güncelleştirmenize izin vermiyor. Örneğin, değişiklik yönetimi ilkelerini izlemeniz veya cihazın görev açısından kritik olması gerekir. Uzun süreli kullanım için yeni bir istemci yükleyerek, genişletilmiş birlikte çalışabilirlik istemcisi (EIC) olarak adlandırılan bu gereksinimlere uyum sağlamak. Yalnızca bilgi noktası veya satış noktası cihazları gibi sık güncelleştirilemeyebilir belirli cihazlar için EIC 'yi kullanın. İstemcilerinizin çoğu için [otomatik istemci yükseltmesini](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) kullanmaya devam edin.

## <a name="how-it-works"></a>Nasıl çalışır?

Genellikle, Configuration Manager için yeni bir [konsol içi güncelleştirme](../servers/manage/install-in-console-updates.md) yüklediğinizde istemciler, bu yeni özellikleri kullanabilmesi için istemci yazılımını otomatik olarak güncelleştirir. Bu senaryoyla, yeni özellikleri ve güncelleştirmeleri alan geçerli dala hala güncelleştireceğinizi görürsünüz. Çoğu cihaz, yüklediğiniz her sürüm güncelleştirmesiyle Configuration Manager istemci yazılımını güncelleştirir. Ancak, istemci yazılım güncelleştirmelerini almak istemediğiniz kritik sistemler alt kümesinde, genişletilmiş birlikte çalışabilirlik istemcisini yüklersiniz. Bu istemciler, istemci yazılımının yeni bir sürümünü açıkça dağıtana kadar yeni istemci yazılımı yüklemez.

## <a name="supported-versions"></a>Desteklenen sürümler

Aşağıdaki tabloda, bu senaryo için desteklenen Configuration Manager istemcisinin sürümleri listelenmektedir:

| Sürüm | Kullanılabilirlik tarihi | Destek bitiş tarihi |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 27 Mart 2019 | 27 Mart 2021 ' den önce değil |
| 1802<br/>5.00.8634 | 1 Mayıs 2018 | 1 Mayıs 2020 ' den önce değil |
| 1606<br/>5.00.8412 | 18 Kasım 2016 | 1 Mayıs 2019 |

> [!TIP]  
> EIC, yayın tarihinden en az iki yıl boyunca desteklenir. Sürüm tarihleri hakkında daha fazla bilgi için bkz. [Configuration Manager geçerli dal sürümleri Için destek](../servers/manage/current-branch-versions-supported.md).  

İstemci süresi dolmadan önce geçerli Dalla yönettiğiniz cihazlarda genişletilmiş birlikte çalışabilirlik istemcisini güncelleştirmeyi planlayın. Bunu yapmak için Microsoft 'tan istemcisinin yeni bir sürümünü indirin ve ardından bu güncelleştirilmiş istemci yazılımını, geçerli genişletilmiş birlikte çalışabilirlik istemcisini kullanan cihazlarınıza dağıtın.

## <a name="how-to-use-the-eic"></a>EIC 'yi kullanma

1. Bu cihazları bir koleksiyona ekleyin ve bu koleksiyonu otomatik istemci yükseltmelerinden hariç tutun. Daha fazla bilgi için bkz. [istemcileri yükseltmeden dışlama](../clients/manage/upgrade/exclude-clients-windows.md).  

1. Configuration Manager güncelleştirme yükleme ortamının `\SMSSETUP\Client` klasöründen EIC 'nin desteklenen bir sürümünü edinin. Klasörün tüm içeriğini kopyalamadığınızdan emin olun.  

    > [!TIP]  
    > [Toplu Lisanslama hizmeti Merkezi](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) 'nde (vlsc) Configuration Manager medya bulmak için **indirmeler ve anahtarlar** sekmesine gidin, arama `System Center Config`yapın ve ardından **System Center config MGR (geçerli dal)** öğesini seçin.

1. EIC 'yi bu cihazlara el ile yükleyebilirsiniz. Daha fazla bilgi için bkz. [Istemciyi el ile yükleyebilirsiniz](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).  

    > [!Important]  
    > Sürüm 1606 istemcilerini 1802 sürümüne yükseltirken, CCMSETUP seçeneğini kullanın **/Alwaysexcludeupgrade: true**. Aksi halde, istemci, dışlama ilkesi öncesinde otomatik olarak yükseltmek için yönetim noktasından ilke alabilir.  

## <a name="limitations"></a>Sınırlamalar

- Genişletilmiş birlikte çalışabilirlik istemci yazılımı güncelleştirmeleri konsol içi güncelleştirmeler kullanılarak kullanılamaz. EIC 'yi güncelleştirme hakkında daha fazla bilgi için bkz. [Dışlanan istemciyi yükseltme](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override).  

- EIC yalnızca aşağıdaki özellikleri destekler:  

  - Yazılım güncelleştirmeleri  
  - Donanım ve yazılım envanteri
  - Paketler ve programlar

## <a name="next-steps"></a>Sonraki adımlar

[İstemcileri yükseltmeden dışlama](../clients/manage/upgrade/exclude-clients-windows.md)

İstemcilerin istediğiniz cihazlara doğru yüklendiğinden emin olmak için bkz. [istemcileri izleme](../clients/manage/monitor-clients.md).
