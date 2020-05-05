---
title: Önerilen donanım
titleSuffix: Configuration Manager
description: Configuration Manager ortamınızı temel bir dağıtımın ötesinde ölçeklendirmenize yardımcı olacak donanım önerileri alın.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d741e34325da859d4fe1f0af554544ce146a42f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719165"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Configuration Manager için önerilen donanım

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşağıdaki öneriler, sitelerin, site sistemlerinin ve istemcilerin çok basit dağıtımından daha fazlasını desteklemek için Configuration Manager ortamınızı ölçeklendirmenize yardımcı olan kılavuzlardır. Bunlar, mümkün olan tüm site ve hiyerarşi yapılandırmalarını kapsamaz.  

Varsayılan yapılandırmalara sahip kullanılabilir Configuration Manager özelliklerini kullanan istemciler ve sitelerin işlem yüklerini karşılayabilmeniz için aşağıdaki bölümlerde yer alan bilgileri kullanın.  



##  <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Site sistemleri  
Bu bölümde, en fazla istemci sayısını destekleyen ve Configuration Manager özelliklerinin çoğunu veya tümünü kullanan dağıtımlar için Configuration Manager site sistemleri için önerilen donanım yapılandırması sağlanmaktadır. En fazla istemci sayısını destekleyen ve kullanılabilir tüm özellikleri kullanmayan dağıtımlar, daha az bilgisayar kaynağı gerektirebilir. Genel sistem performansını sınırlandıran anahtar etkenler sırasıyla şunlardır:  

1.  Disk G/Ç performansı  

2.  Kullanılabilir bellek  

3.  CPU  

En iyi performans için, tüm veri sürücüleri ve 1 GB/sn 'lik bir Ethernet ağı için RAID 10 yapılandırması kullanın.  

###  <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Site sunucuları  

|Site yapılandırması|CPU (çekirdek)|Bellek (GB)|SQL Server için bellek ayırma (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Aynı sunucuda veritabanı site rolü olan tek başına birincil site sunucusu<sup>1</sup>|16|96|80|  
|Uzak site veritabanına sahip tek başına birincil site sunucusu|8|16|-|  
|Tek başına birincil siteye ait uzak veritabanı sunucusu|16|72|90|  
|Aynı sunucuda veritabanı site rolü olan merkezi yönetim sitesi sunucusu<sup>1</sup>|20|128|80|  
|Uzak site veritabanına sahip merkezi yönetim sitesi sunucusu|8|16|-|  
|Merkezi yönetim sitesine ait uzak veritabanı sunucusu|16|96|90|  
|Aynı sunucuda veritabanı site rolüne sahip alt birincil site|16|96|80|  
|Uzak site veritabanına sahip alt birincil site sunucusu|8|16|-|  
|Alt birincil siteye ait uzak veritabanı sunucusu|16|72|90|  
|İkincil site sunucusu|8|16|-|  

<sup>1</sup> site sunucusu ve SQL Server aynı bilgisayara yüklendiğinde, dağıtım, siteler ve istemciler için en büyük [boyut ve ölçek numaralarını](size-and-scale-numbers.md) destekler. Ancak, bu yapılandırma SQL Server kümesi kullanma gibi [Configuration Manager için yüksek kullanılabilirlik seçeneklerini](../../servers/deploy/configure/high-availability-options.md)sınırlayabilir. Ayrıca, hem SQL Server hem de aynı bilgisayarda çalışırken Configuration Manager site sunucusunu desteklemek için gereken daha yüksek g/ç gereksinimleri nedeniyle, daha büyük bir dağıtımınız varsa, uzak SQL Server makinesiyle bir yapılandırma kullanmayı düşünmek iyi bir fikirdir.  

###  <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Uzak site sistemi sunucuları  
Aşağıdaki kılavuz, tek bir site sistem rolü tutan bilgisayarlar içindir. Aynı bilgisayara birden fazla site sistem rolü yüklemeye yönelik ayarları planlayın.  

|Site sistemi rolü|CPU (çekirdek)|Bellek (GB)|Disk alanı (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Yönetim noktası|4|8|50|  
|Dağıtım noktası|2|8|İşletim sisteminin gerektirdiği gibi, dağıttığınız içeriği depolamak için|  
|Yazılım güncelleştirme noktası<sup>1</sup>|8|16|İşletim sisteminin gerektirdiği gibi, dağıttığınız güncelleştirmeleri depolamak için|  
|Diğer tüm site sistem rolleri|4|8|50|  

<sup>1</sup> bir yazılım güncelleştirme noktası barındıran bılgısayar, IIS uygulama havuzları için aşağıdaki konfigürasyonları gerektirir:  

- **WsusPool kuyruğu uzunluğunu** **2000**olarak arttırın.  

- **WsusPool özel bellek sınırını** dört kez artırın veya **0** (sınırsız) olarak ayarlayın.  

###  <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Site sistemleri için disk alanı  
Disk ayırma ve yapılandırma Configuration Manager performansına katkıda bulunur. Her Configuration Manager ortamı farklı olduğundan, uyguladığınız değerler aşağıdaki kılavuzdan farklı olabilir.  

En iyi performans için, her bir nesneyi ayrılmış farklı bir RAID birimine yerleştirin. Tüm veri birimlerinde (Configuration Manager ve veritabanı dosyaları) en iyi performansı elde etmek için RAID 10 kullanın.  

|Veri kullanımı|En az disk alanı|25.000 istemci|50.000 istemci|100.000 istemci|150.000 istemci|700.000 istemci (merkezi yönetim sitesi)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|İşletim sistemi|İşletim sistemi kılavuzuna bakın.|İşletim sistemi kılavuzuna bakın.|İşletim sistemi kılavuzuna bakın.|İşletim sistemi kılavuzuna bakın.|İşletim sistemi kılavuzuna bakın.|İşletim sistemi kılavuzuna bakın.|  
|Uygulama ve günlük dosyaları Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Site veritabanı .mdf dosyası|Her 25.000 istemci için 75 GB|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Site veritabanı .ldf dosyası|Her 25.000 istemci için 25 GB|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Geçici veritabanı dosyaları (.mdf ve .ldf)|Gereken şekilde|Gereken şekilde|Gereken şekilde|Gereken şekilde|Gereken şekilde|Gereken şekilde|  
|İçerik (dağıtım noktası paylaşımları)|Gerektiği gibi<sup>1</sup>|Gerektiği gibi<sup>1</sup>|Gerektiği gibi<sup>1</sup>|Gerektiği gibi<sup>1</sup>|Gerektiği gibi<sup>1</sup>|Gerektiği gibi<sup>1</sup>|  

<sup>1</sup> disk alanı Kılavuzu, site sunucusunda veya dağıtım noktalarında içerik kitaplığında bulunan içerik için gereken alanı içermez. İçerik kitaplığını planlama hakkında bilgi için bkz. [İçerik kitaplığı](../../../core/plan-design/hierarchy/the-content-library.md).  

Disk alanı gereksinimleri için planlama yaparken, önceki kılavuza ek olarak aşağıdaki yönergeleri de dikkate alın:  

- Her istemci için yaklaşık 5 MB alan gerekir.  

- Birincil bir site için geçici veritabanının boyutunu planlarken, site veritabanı. mdf dosyasının %25 ' i oranında %30 ' una kadar bir Birleşik boyut planlayın. Gerçek Boyut önemli ölçüde küçüktür veya daha büyük olabilir. Bu, site sunucusunun performansına ve hem kısa hem de uzun süreler boyunca gelen verilerin hacmine bağlıdır.  

  > [!NOTE]  
  >  Bir sitede 50.000 veya daha fazla istemciniz olduğunda, dört veya daha fazla geçici veritabanı. mdf dosyası kullanmayı planlayın.  

- Bir merkezi yönetim sitesi için geçici veritabanı boyutu genellikle birincil bir siteden çok daha küçüktür.  

- İkincil site veritabanı aşağıdaki boyut kısıtlamalarına sahiptir:  

  - SQL Server 2012 Express: 10 GB  

  - SQL Server 2014 Express: 10 GB  

##  <a name="clients"></a><a name="bkmk_ScaleClient"></a>İstemcinin  
Bu bölümde, Configuration Manager istemci yazılımını kullanarak yönettiğiniz bilgisayarlar için önerilen donanım konfigürasyonları sağlanmaktadır.  

### <a name="client-for-windows-computers"></a>Windows bilgisayarları için istemciler  
Aşağıda, katıştırılmış işletim sistemleri dahil olmak üzere Configuration Manager kullanarak yönettiğiniz Windows tabanlı bilgisayarlar için en düşük gereksinimler verilmiştir:  

- **İşlemci ve bellek:** Bilgisayar işletim sistemi için işlemci ve RAM gereksinimlerine bakın.  

- **Disk alanı:** 500 MB kullanılabilir disk alanı, Configuration Manager istemci önbelleği IÇIN 5 GB önerilir. Configuration Manager istemcisini yüklemek için özelleştirilmiş ayarları kullanırsanız daha az disk alanı gerekir:  

    - Varsayılan 5120 MB değerinden daha küçük bir önbellek dosyası ayarlamak için SMSCACHESIZE Client.msi özelliğini kullanın. En düşük boyut 1 MB’tır. Örneğin, `CCMSetup.exe SMSCachesize=2` boyutu 2 MB olan bir önbellek oluşturur.  

    Bu istemci yükleme ayarları hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    > İstemciyi en az disk alanıyla yüklemeniz, genellikle standart Windows bilgisayarlarından daha küçük disk boyutlarına sahip Windows Embedded cihazları için faydalıdır.  

Aşağıda, Configuration Manager isteğe bağlı işlevlere yönelik ek en düşük donanım gereksinimleri verilmiştir.  

- **İşletim sistemi dağıtımı:** 384 MB RAM  

- **Software Center:** 500 MHz işlemci  

- **Uzaktan denetim:** En iyi deneyim için en az 1 GB RAM ile Pentium 4 hiper Iş parçacıklı 3 GHz (tek çekirdek) veya karşılaştırılabilir CPU  

### <a name="client-for-linux-and-unix"></a>Linux ve UNIX İstemcisi  
Configuration Manager ile yönettiğiniz Linux ve UNIX sunucuları için en düşük gereksinimler aşağıda verilmiştir.  

|Gereksinim|Ayrıntılar|  
|-----------------|-------------|  
|İşlemci ve bellek|Bilgisayarın işletim sistemi için işlemci ve RAM gereksinimlerine bakın.|  
|Disk alanı|500 MB kullanılabilir disk alanı, Configuration Manager istemci önbelleği için 5 GB önerilir.|  
|Ağ bağlantısı|Configuration Manager istemci bilgisayarlarının yönetimi etkinleştirmek için site sistemlerine Configuration Manager ağ bağlantısı olması gerekir.|  

##  <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Configuration Manager konsolu  
Aşağıdaki tabloda yer alan gereksinimler Configuration Manager konsolunu çalıştıran her bilgisayar için geçerlidir.  

**En düşük donanım yapılandırması:**  

- Intel i3 veya karşılaştırılabilir CPU  

- 2 GB RAM  

- 2 GB disk alanı  

|DPI ayarı|En düşük çözünürlük|  
|-----------------|------------------------|  
|%96/100|1024 x 768|  
|%120/125|1280 x 960|  
|%144/150|1600 x 1200|  
|%196/200|2500 x 1600|  

**PowerShell desteği:**  

Configuration Manager konsolunu çalıştıran bir bilgisayara PowerShell için destek yüklediğinizde, Configuration Manager yönetmek için söz konusu bilgisayarda PowerShell cmdlet 'lerini çalıştırabilirsiniz.

- PowerShell 3,0 veya üzeri destekleniyor

PowerShell 'e ek olarak Windows Management Framework (WMF) sürüm 3,0 veya sonrası desteklenmektedir.   


##  <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Laboratuvar dağıtımları  
Configuration Manager laboratuvar ve test dağıtımları için aşağıdaki en düşük donanım önerilerini kullanın. Bu öneriler, 100 istemciye kadar tüm site türleri için geçerlidir:  

|Rol|CPU (çekirdek)|Bellek (GB)|Disk alanı (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Site ve veritabanı sunucusu|2 - 4|8 - 12|100|  
|Site sistemi sunucusu|1 - 4|2 - 4|50|  
|İstemci|1 - 2|1 - 3|30|  
