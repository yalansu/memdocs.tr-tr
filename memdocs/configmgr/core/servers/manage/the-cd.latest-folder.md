---
title: CD.Latest klasörü
titleSuffix: Configuration Manager
description: Configuration Manager konsolundan ürüne güncelleştirmeleri teslim eden işlem hakkında bilgi edinin.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720516"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>CD. Configuration Manager için en son klasör

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Configuration Manager konsolundan ürüne güncelleştirmeleri teslim etmeye yönelik bir işlemdir. Bu yeni Configuration Manager güncelleştirme yöntemini desteklemek için CD adlı yeni bir klasör oluşturulur **. En son**. Bu klasör, sitenizin güncelleştirilmiş sürümü için Configuration Manager yükleme dosyalarının bir kopyasını içerir.  

CD. En son klasör, kurulum 'un indirdiği ve kullandığı yeniden dağıtılabilir dosyaları içeren **Redist**adlı bir klasör içerir. Bu dosyalar, CD.Latest klasöründe bulunan Configuration Manager dosyalarının sürümüyle eşleştirilir. Kurulum’u bir CD.Latest klasöründen çalıştırdığınızda, bu Kurulum sürümüyle eşleştirilmiş dosyaları kullanmanız gerekir. Microsoft 'tan yeni ve güncel dosyaları indirmek için kurulum 'U yönlendirebilir ya da doğrudan kurulum 'U CD 'ye dahil edilen Redist klasöründeki dosyaları kullanacak şekilde yönlendirebilirsiniz. En son klasör.

Temel medya bir **Redist** klasörü içermez. Site, konsol içi bir güncelleştirme yükleyene kadar bir yeniden dağıtım klasörü oluşturmaz. Bu sırada, temel ortamdan siteler yüklerken kullandığınız Redist klasörünü kullanın.  

> [!TIP]  
> Kullandığınız yeniden dağıtılabilir dosyaların güncel olduğundan emin olun. Yeniden dağıtılabilir dosyaları yakın zamanda indirmediyseniz, kurulum 'un Microsoft 'tan bunu yapmasına izin vermeyi planlayın.   

Aşağıdaki senaryolar CD 'yi oluşturur veya güncelleştirir. Bir merkezi yönetim sitesi veya birincil site sunucusundaki en son klasör:  

- Configuration Manager konsolundan bir güncelleştirme veya düzeltme yüklediğinizde, site Configuration Manager yükleme klasöründeki klasörü oluşturur veya güncelleştirir.  

- Yerleşik Configuration Manager yedekleme görevini çalıştırdığınızda site, belirlenen yedekleme klasörü konumu altında klasörü oluşturur veya güncelleştirir.  

- Temel medyayı kullanarak yeni bir site yüklediğinizde, site CD 'yi oluşturur. En son klasör.


## <a name="supported-scenarios"></a>Desteklenen senaryolar

CD 'deki kaynak dosyalar. En son klasör aşağıdaki senaryolar için desteklenir:  

### <a name="backup-and-recovery"></a>Yedekleme ve kurtarma
Bir siteyi kurtarmak için CD 'deki kaynak dosyalarını kullanın. Siteniz ile eşleşen en son klasör. Yerleşik site yedekleme görevini kullanarak bir site yedeklemesi çalıştırdığınızda CD. En son klasör yedeklemenin bir parçası olarak dahil edilmiştir.

- Bir siteyi bir site kurtarmasının parçası olarak yeniden yüklerken siteyi yedeğinize dahil edilen CD.Latest klasöründen yüklersiniz. Bu eylem, siteyi, site yedeğiniz ve site veritabanınız ile eşleşen dosya sürümlerini kullanarak kurar.  

    - Doğru CD 'ye erişiminiz yoksa. En son klasör sürümü, CD 'yi alın. Laboratuvar ortamında bir site yükleyerek doğru dosya sürümleriyle en son klasör. Ardından, bu siteyi kurtarmak istediğiniz sürümle eşleşecek şekilde güncelleştirin.  

    - Doğru CD 'niz yoksa. En son klasör ve içeriği kullanılabilir, bir siteyi kurtaramazsınız. Bu durumda, siteyi yeniden yüklemeniz gerekir.  

- Bir CD 'niz yoksa. En son klasör, ancak çalışan bir alt birincil siteniz veya merkezi yönetim sitesi varsa, bu siteyi bir site kurtarması için başvuru sitesi olarak kullanabilirsiniz.  

### <a name="install-a-child-primary-site"></a>Alt birincil site yükler
Konsol içi bir veya daha fazla güncelleştirme yüklemiş bir merkezi yönetim sitesinin altına yeni bir alt birincil site yüklemek istediğinizde, CD 'den kurulum 'U ve kaynak dosyalarını kullanın. Merkezi yönetim sitesinden en son klasör. Bu işlem, merkezi yönetim sitesinin sürümüyle eşleşen yükleme kaynak dosyalarını kullanır. Daha fazla bilgi için bkz. [siteleri yüklemek Için Kurulum Sihirbazı 'Nı kullanma](../deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="expand-a-stand-alone-primary-site"></a>Tek başına birincil siteyi genişletme
Tek başına bir birincil siteyi yeni bir merkezi yönetim sitesi yükleyerek genişlettiğinizde, kurulum 'U ve kaynak dosyaları CD 'den kullanın. Birincil sitedeki en son klasör. Bu işlem, birincil sitenin sürümüyle eşleşen yükleme kaynak dosyalarını kullanır. Daha fazla bilgi için bkz. [tek başına birincil siteyi genişletme](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).

### <a name="install-a-secondary-site"></a>İkincil site yükler
<!-- SCCMDocs-pr issue #3164 -->
Konsol içi güncelleştirmeleri bir veya daha fazla yükleyen birincil sitenin altına yeni bir ikincil site yüklemek istediğinizde CD 'deki kaynak dosyalarını kullanın. Birincil sitedeki en son klasör. 

Daha fazla bilgi için bkz. [ikincil site yüklemesi](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Desteklenmeyen senaryolar

Güncelleştirilmiş CD. İçin en son kaynak dosyaları desteklenmez:  

- Yeni bir hiyerarşi için yeni bir site yükleme  
- Güncel dala Configuration Manager bir Microsoft System Center 2012 Configuration Manager sitesini yükseltme
- Configuration Manager istemcilerini yükleme
- Configuration Manager konsolları yükleniyor
