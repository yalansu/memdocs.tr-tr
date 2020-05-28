---
title: Önerilen donanım
titleSuffix: Configuration Manager
description: Configuration Manager ortamınızı temel bir dağıtımın ötesinde ölçeklendirmenize yardımcı olacak donanım önerileri alın.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428793"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Configuration Manager için önerilen donanım

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşağıdaki öneriler, sitelerin, site sistemlerinin ve istemcilerin çok basit dağıtımından daha fazlasını desteklemek için Configuration Manager ortamınızı ölçeklendirmenize yardımcı olan kılavuzlardır. Olası tüm site ve hiyerarşi yapılandırmalarının kapsamaları amaçlanmamıştır.  

Donanım planlaması yapmanıza yardımcı olması için aşağıdaki bölümlerdeki bilgileri bir kılavuz olarak kullanın. Donanımınızın, kullanılabilir Configuration Manager özelliklerini kullanan istemciler ve siteler için işleme yüklerini karşılayabilmesini sağlayın.

Daha fazla bilgi için bkz. [performans ve ölçek kılavuzu teknik incelemesi Configuration Manager](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Site sistemleri

Bu bölümde Configuration Manager site sistemleri için önerilen donanım konfigürasyonları sunulmaktadır. En fazla istemci sayısını desteklemek ve Configuration Manager özelliklerinin çoğunu veya tümünü kullanmak için bu önerileri kullanın. Ortamınız en yüksek sayıda istemciden daha azını destekliyorsa ve kullanılabilir tüm özellikleri kullanmıyorsa, daha az kaynak gerekebilir. Genel olarak, aşağıdaki anahtar faktörleri genel sistemin performansını sınırlar:

1. Disk G/Ç performansı

2. Kullanılabilir bellek

3. CPU

En iyi performans için, tüm veri sürücüleri ve 1 GB/sn 'lik bir Ethernet ağı için RAID 10 yapılandırması kullanın.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Site sunucuları

|Site yapılandırması|CPU (çekirdek)|Bellek (GB)|SQL Server için bellek ayırma (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Aynı sunucu notunda bir veritabanı site rolü olan tek başına birincil site sunucusu <sup> [1](#bkmk_note1)</sup>|16|96|80|  
|Uzak site veritabanına sahip tek başına birincil site sunucusu|8|16|-|  
|Tek başına birincil siteye ait uzak veritabanı sunucusu|16|72|90|  
|Aynı sunucu notunda bir veritabanı site rolü olan merkezi yönetim sitesi sunucusu <sup> [1](#bkmk_note1)</sup>|20|128|80|  
|Uzak site veritabanına sahip merkezi yönetim sitesi sunucusu|8|16|-|  
|Merkezi yönetim sitesine ait uzak veritabanı sunucusu|16|96|90|  
|Aynı sunucuda veritabanı site rolüne sahip alt birincil site|16|96|80|  
|Uzak site veritabanına sahip alt birincil site sunucusu|8|16|-|  
|Alt birincil siteye ait uzak veritabanı sunucusu|16|72|90|  
|İkincil site sunucusu|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a>Note 1: birlikte bulunan SQL

Site sunucusunu ve SQL Server aynı bilgisayara yüklediğinizde dağıtım, siteler ve istemciler için en büyük [boyut ve ölçek numaralarını](size-and-scale-numbers.md) destekler. Bu yapılandırma SQL Server kümesi kullanma gibi [yüksek kullanılabilirlik seçeneklerini](../../servers/deploy/configure/high-availability-options.md)sınırlayabilir. Aynı bilgisayardaki her iki rolü de desteklemeye yönelik daha yüksek g/ç gereksinimleri nedeniyle daha büyük bir ortamınız varsa, uzak bir SQL Server kullanmayı göz önünde bulundurun.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Uzak site sistemi sunucuları

Aşağıdaki kılavuz, tek bir site sistem rolü tutan bilgisayarlar içindir. Aynı bilgisayara birden fazla site sistem rolü yüklediğinizde ayarlamayı planlayın.

|Site sistemi rolü|CPU (çekirdek)|Bellek (GB)|Disk alanı (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Yönetim noktası|4|8|50|  
|Dağıtım noktası|2|8|İşletim sisteminin gerektirdiği gibi, dağıttığınız içeriği depolamak için|  
|Yazılım güncelleştirme noktası <sup> [2](#bkmk_note2) .</sup>|8|16|İşletim sisteminin gerektirdiği gibi, dağıttığınız güncelleştirmeleri depolamak için|  
|Diğer tüm site sistem rolleri|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a>2. Note: WSUS yapılandırması

Yazılım güncelleştirme noktası barındıran bilgisayar, IIS uygulama havuzları için aşağıdaki yapılandırmalara sahip olması gerekir:  

- **WsusPool kuyruğu uzunluğunu** **2000**olarak arttırın.  

- **WsusPool özel bellek sınırını** dört kez artırın veya **0** (sınırsız) olarak ayarlayın.  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Site sistemleri için disk alanı

Disk ayırma ve yapılandırma Configuration Manager performansına katkıda bulunur. Her Configuration Manager ortamı farklı olduğundan, uyguladığınız değerler aşağıdaki kılavuzdan farklı olabilir.

En iyi performans için, her bir nesneyi ayrılmış farklı bir RAID birimine yerleştirin. Configuration Manager ve veritabanı dosyaları için tüm veri birimlerinde, en iyi performans için RAID 10 kullanın.

|Veri kullanımı|En az disk alanı|25.000 istemci|50.000 istemci|100.000 istemci|150.000 istemci|700.000 istemci (merkezi yönetim sitesi)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Uygulama ve günlük dosyaları Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Site veritabanı .mdf dosyası|Her 25.000 istemci için 75 GB|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Site veritabanı .ldf dosyası|Her 25.000 istemci için 25 GB|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Geçici veritabanı dosyaları (.mdf ve .ldf)|Gereken şekilde|Gereken şekilde|Gereken şekilde|Gereken şekilde|Gereken şekilde|Gereken şekilde|  

Windows sistem diski için bkz. yüklü işletim sistemi sürümü için boyutlandırma Kılavuzu.

Dağıtım noktaları üzerindeki içerik için dağıtımlarınıza bağlıdır. Bu kılavuz, site sunucusundaki veya dağıtım noktalarında içerik kitaplığı için gereken disk alanını içermez. Daha fazla bilgi için bkz. [içerik kitaplığı](../../../core/plan-design/hierarchy/the-content-library.md).

Disk alanı gereksinimlerini planlarken, aşağıdaki ek yönergeleri göz önünde bulundurun:

- Her istemcinin veritabanında yaklaşık 5-10 MB alan olması gerekir. Bu sayı, hiyerarşi türüne, yapılandırmaya ve istemci sayısına bağlıdır. Boyut genellikle daha büyük ortamlarda daha küçüktür. Daha küçük sitelerde, istemci başına daha fazla veritabanı kullanımı vardır.<!-- SCCMDocs#1048 -->

- Birincil sitenin geçici veritabanı için, site veritabanı. mdf dosyasının %25 ' i ile %30 ' a kadar Birleşik bir boyut planlayın. Gerçek boyut daha küçük veya daha büyük olabilir. Bu, site sunucusunun performansına ve hem kısa hem de uzun süreler boyunca gelen verilerin hacmine bağlıdır.

  > [!NOTE]
  > Bir sitede 50.000 veya daha fazla istemciniz olduğunda, dört veya daha fazla geçici veritabanı. mdf dosyası kullanmayı planlayın.

- Bir merkezi yönetim sitesi için geçici veritabanı boyutu genellikle birincil bir siteden çok daha küçüktür.

- İkincil site veritabanı için SQL Server Express kullanıyorsanız, veritabanı boyutunu 10 GB ile sınırlandırır.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a>İstemcinin

Bu bölümde, Configuration Manager istemci yazılımını kullanarak yönettiğiniz bilgisayarlar için önerilen donanım konfigürasyonları sağlanmaktadır.

### <a name="client-for-windows-computers"></a>Windows bilgisayarları için istemciler

Aşağıdaki en düşük gereksinimler, Configuration Manager kullanarak yönettiğiniz Windows tabanlı bilgisayarlar için, katıştırılmış sürümler dahil olmak üzere:

- **İşlemci ve bellek:** İşletim sistemi için işlemci ve RAM gereksinimlerine bakın.

- **Disk alanı:** 500 MB kullanılabilir disk alanı, Configuration Manager istemci önbelleği IÇIN 5 GB önerilir. Configuration Manager istemcisini yüklemek için özelleştirilmiş ayarları kullanırsanız daha az disk alanı gerekir.

  - Varsayılan 5120 MB değerinden daha küçük bir önbellek boyutu ayarlamak için **SMSCachesize** Client. msi özelliğini kullanın. En düşük boyut 1 MB’tır. Aşağıdaki örnek, 2 MB 'lik bir önbellek oluşturur:`CCMSetup.exe SMSCACHESIZE=2`

    Daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../../core/clients/deploy/about-client-installation-properties.md).

    > [!TIP]
    > İstemciyi en az disk alanıyla yüklemeniz, genellikle standart Windows bilgisayarlarından daha küçük disk boyutlarına sahip Windows Embedded cihazları için faydalıdır.

Aşağıdaki ek en düşük donanım gereksinimleri Configuration Manager isteğe bağlı işlevlere yöneliktir:

- **Işletim sistemi dağıtımı:** En az 384 MB RAM

- **Yazılım Merkezi:** En az bir 500 MHz işlemci

- **Uzaktan denetim:** En iyi deneyim için en az 1 GB RAM 'e sahip bir Pentium 4 hiper Iş parçacıklı 3 GHz (tek çekirdek) veya karşılaştırılabilir CPU.

### <a name="client-for-linux-and-unix"></a>Linux ve UNIX İstemcisi

Aşağıdaki minimum gereksinimler Configuration Manager ile yönettiğiniz Linux ve UNIX sunucuları içindir.

|Gereksinim|Ayrıntılar|  
|-----------------|-------------|  
|İşlemci ve bellek|Bilgisayarın işletim sistemi için işlemci ve RAM gereksinimlerine bakın.|  
|Disk alanı|500 MB kullanılabilir disk alanı, Configuration Manager istemci önbelleği için 5 GB önerilir.|  
|Ağ bağlantısı|Configuration Manager istemci bilgisayarlarının yönetimi etkinleştirmek için site sistemlerine Configuration Manager ağ bağlantısı olması gerekir.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Configuration Manager konsolu

Configuration Manager konsolunu çalıştıran her bilgisayar için aşağıdaki en düşük donanım gereksinimleri geçerlidir:

- Intel i3 veya karşılaştırılabilir CPU  

- 2 GB RAM  

- 2 GB disk alanı  

|DPI ayarı|En düşük çözünürlük|  
|-----------------|------------------------|  
|%96/100|1024 x 768|  
|%120/125|1280 x 960|  
|%144/150|1600 x 1200|  
|%196/200|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Laboratuvar dağıtımları

Configuration Manager laboratuvar ve test dağıtımları için aşağıdaki en düşük donanım önerilerini kullanın. Bu öneriler, 100 istemciye kadar tüm site türleri için geçerlidir:  

|Rol|CPU (çekirdek)|Bellek (GB)|Disk alanı (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Site ve veritabanı sunucusu|2 - 4|8 - 12|100|  
|Site sistemi sunucusu|1 - 4|2 - 4|50|  
|İstemci|1 - 2|1 - 3|30|  
