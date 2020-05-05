---
title: '1606 temel medyasını kullanarak bir site yükler '
titleSuffix: Configuration Manager
description: System Center Configuration Manager için LTSB 'yi yükler veya yükseltin.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722805"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Sürüm 1606 temel medyasını yükleyip yükseltme

*Uygulama hedefi: System Center Configuration Manager (uzun süreli bakım dalı)*

Configuration Manager için sürüm 1606 temel medyasından kurulum 'u çalıştırdığınızda, System Center Configuration Manager uzun süreli bakım dalı sitesini yükleyebilirsiniz.

Temel medya, Microsoft System Center 2016 'nin bir parçası olarak veya uzun süreli bakım dalı sürüm 1606 ' den System Center Configuration Manager itibaren DVD 'de kullanılabilir. Temel medya hakkında bilgi edinmek için bkz. [temel ve güncelleştirme sürümleri](../servers/manage/updates.md#bkmk_Baselines).


Sürüm 1606 temel medyasını kullandığınızda yüklediğiniz veya yükselttiğiniz site şu şekilde olur:
- İlk olarak 1511 temel medyası kullanılarak yüklenen bir siteyle eşdeğer bir *güncel dalı sitesi* ve ardından 1606 sürümüne ve 1606 düzeltme TOPLAMASı-KB3186654 ' e güncelleştirildi.
- Sürüm 1606 ' i ve 1606 düzeltme toplaması-KB3186654 ' ni çalıştıran Güncel Dalı sitesiyle eşdeğer bir *LTSB sitesi* . Temel medya, düzeltme toplamasını zaten içeriyor.  Ancak, LTSB, [System Center Configuration Manager uzun süreli bakım dalına giriş](introduction-to-the-ltsb.md)bölümünde açıklandığı gibi, güncel dalı ile kullanılabilen tüm özellikleri veya yetenekleri desteklemez.

Configuration Manager farklı dallarına alışkın değilseniz, [hangi Configuration Manager dalını kullanmalıyım?](which-branch-should-i-use.md)bölümüne bakın.




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Kurulum 'da 1606 temel medyayla yapılan değişiklikler
1606 temel medyası Configuration Manager Kurulum için aşağıdaki değişiklikleri tanıtır.

### <a name="branch-and-edition"></a>Dal ve sürüm
Kurulumu çalıştırdığınızda, şimdi yüklemek istediğiniz Configuration Manager dalını seçebileceğiniz bir lisanslama sayfası sunulur. Lisanslı bir yükleme olarak Güncel Dalı veya LTSB ' yi seçebilir veya Güncel Dalı bir değerlendirme sürümünü lisanslı olmayan bir yükleme olarak seçebilirsiniz.

Daha fazla bilgi için bkz. [Configuration Manager Için lisanslama ve dallar](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Yazılım Güvencesi süre sonu
Kurulum sırasında, **yazılım güvencesi sona erme tarihi** değerini girme seçeneğiniz vardır. Bu, uygun bir anımsatıcı olarak belirtebileceğiniz isteğe bağlı bir değerdir.

> [!NOTE]
> Microsoft, girdiğiniz sona erme tarihini doğrulamaz ve bu tarihi lisans doğrulaması için kullanmaz.  Bunun yerine, bunu sona erme tarihinin bir anımsatıcısı olarak kullanabilirsiniz. Configuration Manager, çevrimiçi olarak sunulan yeni yazılım güncelleştirmelerini düzenli olarak denetlediği ve yazılım güvencesi lisans durumunuz bu ek güncelleştirmeleri kullanmaya uygun olması için geçerli olmalıdır.    

- Kurulumu, Configuration Manager sürüm 1606 temel medyasından çalıştırdığınızda, Kurulum sihirbazının **ürün anahtarı** sayfasında tarih değerini belirtebilirsiniz.
- Bu tarihi Ayrıca, Configuration Manager konsolundaki **Hiyerarşi ayarları özellikleri** > **lisansı** ' nı seçerek de belirtebilirsiniz.

Daha fazla bilgi için [lisanslama ve Configuration Manager için dallardaki](learn-more-editions.md)"yazılım güvencesi sözleşmeleri" bölümüne bakın.


### <a name="additional-pre-upgrade-configurations"></a>Diğer yükseltme öncesi yapılandırma
System Center 2012 Configuration Manager 'nin LTSB 'ye yükseltmesini başlatmadan önce, yükseltme öncesi denetim listesinin bir parçası olarak aşağıdaki ek adımları uygulamanız gerekir.  
LTSB 'nin desteklemediği site sistem rollerini kaldırın:
- Varlık Yönetim Bilgileri eşitleme noktası
- Microsoft Intune bağlayıcısı
- Bulut tabanlı dağıtım noktaları

Daha fazla bilgi için bkz. [Configuration Manager yükseltme](../servers/deploy/install/upgrade-to-configuration-manager.md).


### <a name="new-scripted-installation-options"></a>Yeni komut dosyalı yükleme seçenekleri
Sürüm 1606 temel medyası, yeni bir üst düzey sitenin betikleştirilmiş yüklemeleri için yeni bir katılımsız betik dosyası anahtarı destekler. Bu, yeni bir tek başına birincil site yüklemek veya bir site genişletme senaryosunun parçası olarak bir merkezi yönetim sitesi eklemek için geçerlidir.

Lisanslı bir dalı yüklemek için katılımsız bir betik kullanırken, betiğinizin Seçenekler bölümüne aşağıdaki bölümü, anahtar adlarını ve değerleri eklemeniz gerekir. Güncel Dalı bir değerlendirme sürümünün yüklenmesini komut dosyasına almak için bu değerleri kullanmanız gerekmez:  

 **SABranchOptions**
- **Anahtar adı: SAActive**
  - Değerler: 0 veya 1.  
  - Ayrıntılar: 0, Güncel Dalı lisanslı olmayan bir değerlendirme sürümü yüklüyor ve 1 lisanslı bir sürüm yüklüyor.   

- **CurrentBranch**
  - Değerler: 0 veya 1.  
  - Ayrıntılar: 0 uzun süreli bakım dalını yükleme ve 1 Güncel Dalı yükleme.  

Örneğin, kullanabileceğiniz lisanslı bir Güncel Dalı sürümünü yüklemek için:

**Anahtar adı: SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> **Sabranchoptions** yalnızca temel ortamdan kurulum ile birlikte kullanılabilir. Kurulum 'U CD 'den çalıştırdığınızda uygulanmaz. Sürüm 1606 temel medyasını kullanarak daha önce yüklediğiniz sitenin en son klasörü.
>
> **Sabranchoptions** , System Center 2012 Configuration Manager ile betikleştirilmiş yükseltmelere uygulanmaz ve güncel dalı her zaman sonuçlanır.

Daha fazla bilgi için bkz. [Configuration Manager siteleri yüklemek için komut satırı kullanma](../servers/deploy/install/use-a-command-line-to-install-sites.md).


## <a name="install-a-new-site"></a>Yeni bir site yükler
Her iki dalın de yeni bir sitesini yüklemek için 1606 temel medyasını kullandığınızda, kurulum için aşağıdaki noktalara dikkat edin [Configuration Manager siteleri yükleme](../servers/deploy/install/installing-sites.md) konusunda belgelenen site planlama, hazırlık ve yükleme yordamlarını kullanın:

- Kurulum sırasında, yüklemek istediğiniz Configuration Manager dalını seçmeniz ve yazılım güvencesi anlaşmanızın ayrıntılarını belirtebilirsiniz.
- Aynı hiyerarşideki tüm sitelerin aynı dalı çalıştırması gerekir. LTSB karışımı ve farklı sitelerde Güncel Dalı olan bir hiyerarşiye sahip olmak desteklenmez.
- Yeni komut dosyalı yükleme. Daha fazla bilgi için, bu makalenin önceki kısımlarında yer olarak "yeni betikle yükleme seçenekleri" bölümüne bakın.

## <a name="expand-a-stand-alone-primary-site"></a>Tek başına birincil siteyi genişletme
LTSB 'yi çalıştıran tek başına bir birincil siteyi genişletebilirsiniz.  İşlem, tek bir desteklenmediği uyarısıyla Güncel Dalı site için kullanılandan farklı değildir:

- Yeni Merkezi yönetim sitesini yüklerken, LTSB sitesini yüklemek için kullandığınız orijinal kaynak medyasından kurulum 'U kullanmanız gerekir. Kurulum 'U CD 'den çalıştırma. Bu senaryo için en son klasör desteklenmiyor.

Bir siteyi genişletme hakkında daha fazla bilgi için, [Kurulum Sihirbazı 'nı kullanarak site yükleme](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md)konusundaki "tek başına birincil siteyi genişletme" bölümüne bakın.

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>System Center 2012 Configuration Manager yükseltme
System Center 2012 Configuration Manager yükselttiğinizde, site planlama, hazırlık ve yordamları, [Configuration Manager yükseltme](../servers/deploy/install/upgrade-to-configuration-manager.md) konusunda belgelendiği gibi, ancak aşağıdaki değişikliklerle birlikte kullanın:

**Güncel Dalı yükseltin:**
- Kurulum sırasında Güncel Dalı seçmeniz gerekir ve yazılım güvencesi anlaşmanızın ayrıntılarını belirtebilirsiniz.
- Yeni komut dosyalı yükleme. Daha fazla bilgi için, bu makalenin önceki kısımlarında yer olarak "yeni betikle yükleme seçenekleri" bölümüne bakın.

**LTSB 'ye yükseltin:**  
- Yükseltme öncesi denetim listesinde takip edilecek ek adımlar.
- Kurulum sırasında LTSB 'yi seçmeniz gerekir ve yazılım güvencesi anlaşmanızın ayrıntılarını belirtebilirsiniz.
- System Center 2012 Configuration Manager çalıştıran bir siteyi yalnızca hizmet paketi 1, Service Pack 2 ile System Center 2012 Configuration Manager, Service Pack 2 ile System Center 2012 R2 Configuration Manager veya Service Pack 1 ile System Center 2012 R2 Configuration Manager çalıştıran bir siteyi yükseltebilmeniz gerekir.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>1606 temel medyası için yerinde yükseltme yolları
Aşağıdakileri Configuration Manager lisanslı bir sürümüne yükseltmek için 1606 temel medyasını kullanabilirsiniz:
- System Center 2012 R2 Configuration Manager Service Pack 1
- System Center 2012 R2 Configuration Manager hizmet paketi yok (Bu 2016, 15 Aralık 'ta yeniden yayımlanan sürüm 1606 için temel medyanın kullanılmasını gerektirir.)
- System Center 2012 Configuration Manager Service Pack 2
- System Center 2012, Service Pack 1 ile Configuration Manager (Bu 2016, 15 Aralık 'ta yeniden yayımlanan sürüm 1606 için temel medyanın kullanılmasını gerektirir.)


Bu medyayı Ayrıca, Güncel Dalı lisanslı olmayan bir değerlendirme sürümünü Güncel Dalı tam lisanslı bir sürümüne yükseltmek için de kullanabilirsiniz.

Bu medya, ' nin yükseltmesini desteklemez:
- System Center 2012 ' nin diğer sürümleri Configuration Manager.
- Configuration Manager 2007 veya daha önceki bir sürüm.
- Configuration Manager Release Candidate yüklemesi.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>CD hakkında. En son klasör ve LTSB
Aşağıda, Configuration Manager CD 'de oluşturduğu medyayı kullanma sınırlamaları verilmiştir. Site sunucusundaki en son klasör. Bu sınırlar, LTSB 'yi çalıştıran siteler için geçerlidir:

CD 'deki medya. İçin en son klasör desteklenir:
- Site Recovery.
- Site Bakımı.
- Ek alt birincil siteler yükleniyor.

CD 'deki medya. İçin en son klasör desteklenmez:  
- Bir merkezi yönetim sitesini bir site genişletme senaryosunun parçası olarak yükleme.

Daha fazla bilgi için [CD 'ye bakın. En son klasör](../servers/manage/the-cd.latest-folder.md).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>LTSB için yedekleme, kurtarma ve Site Bakımı
LTSB çalıştıran bir sitede site bakımını yedeklemek, kurtarmak veya çalıştırmak için [yedekleme ve kurtarma Configuration Manager yönelik](../servers/manage/backup-and-recovery.md)kılavuz ve yordamları kullanın.  

CD 'den Configuration Manager Kurulum 'U kullanın. LTSB sitenizin yedeğinin en son klasörü.
