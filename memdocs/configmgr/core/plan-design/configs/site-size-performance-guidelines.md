---
title: Site boyutu ve performansına ilişkin yönergeler
titleSuffix: Configuration Manager
description: Site boyutuyla ilgili performans testi sonuçları, metodolojisi ve Kılavuzu.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 9e5cc21e4fef60f64576a7b578b3616a7e37756d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073509"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Configuration Manager site boyutu ve performans yönergeleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, sektörde ölçeklenebilirlik ve performans doğurur. Diğer belgeler, en büyük ortam boyutlarında siteleri çalıştırmak için [desteklenen en yüksek ölçeklenebilirlik sınırlarını](size-and-scale-numbers.md) ve [donanım yönergelerini](recommended-hardware.md) içerir. Bu makale, her boyuttaki ortamlar için ek performans Kılavuzu sağlar. Bu kılavuz Configuration Manager dağıtmanız gereken donanımı daha doğru şekilde tahmin etmenize yardımcı olabilir.

Bu makale performans sorunlarını Configuration Manager için en büyük katkıda buluna odaklanmaktadır: disk giriş/çıkış alt sistemi veya ıOPS. Makale:

- IOPS 'ye odaklanan ayrıntıları ve test sonuçlarını gösterir
- Kendi ortamlarınızla ve donanımınızla testlerin nasıl yeniden üretemediğinin belgeleri
- Çeşitli boyut ortamları için disk ıOPS gereksinimleri önerir 

## <a name="performance-test-methodology"></a>Performans testi yöntemi

Configuration Manager birçok benzersiz şekilde dağıtabilirsiniz, ancak herhangi bir boyutlandırma tartışmasında birkaç değişkeni anlamak önemlidir. Bir değişken, bir envanter çevrimi gibi *özellik aralığıdır*. Başka bir değişken, sistem başvurularının veya dağıttığı kullanıcıların, yazılım dağıtımlarının veya diğer *nesnelerin* sayısıdır. Performans testi, bu değişkenleri bir *yükün*parçası olarak uygular. Yük, farklı boyuttaki ortamlarda üretim dağıtımlarını kullanan kurumsal müşteriler için tipik bir hızda nesneler oluşturur.

> [!NOTE] 
> Müşteri telemetri verileri, çoğu müşteri için en sık kullanılan senaryolar, yapılandırmalar ve ayarlarla güncel dal derlemelerini test etmenize olanak tanır. Bu makaledeki öneriler, bu ortalamaları temel alır. Deneyimleriniz, ortamınızın boyutuna ve yapılandırmasına göre farklılık gösterebilir. Genel olarak, Configuration Manager nesneler ve aralıklar için ortak anlamda gereklidir. Yalnızca bir sistemdeki her dosyayı toplayabilmeniz veya bir döngüdeki aralığı bir dakika olarak ayarlarsanız, yapmanız gereken anlamına gelmez.

Aşağıdaki bölümlerde, büyük kuruluşlar için test ve modelleme işleme ihtiyaçlarını yaparken kullanılacak bazı temel ayarlar ve Konfigürasyonlar vurgulanacak. Bu yönergeler, önerilen donanım boyutları için temel sistem performansı beklentilerini ayarlamanıza yardımcı olur.

### <a name="feature-intervals-settings"></a>Özellik aralıkları ayarları 
Çoğu sınamanın sistemdeki anahtar döngüleri için varsayılan aralıkları kullanması gerekir. Örneğin, varsayılan *. mof* dosyasından daha büyük olan donanım envanteri testi haftada bir kez gerçekleşir. Özellikle donanım ve yazılım envanteri döngülerinin bazı yinelenen özellik aralıkları, bir ortamın performans özellikleri üzerinde önemli etkilere sahip olabilir. Veri toplama için agresif varsayılan aralıkları etkinleştiren ortamlar, etkinliğin artışına göre büyük bir donanımdan doğrudan orantılı olmalıdır. Örneğin, 25.000 masaüstü istemcileriniz olduğunu ve varsayılan aralıktan iki kat daha hızlı donanım envanteri toplamak istediğinizi varsayalım. Sitenizin donanımını 50.000 istemcileriniz gibi boyutlandırarak başlatmanız gerekir.

### <a name="objects"></a>Nesneler 
Testler, büyük kuruluşların sistemle birlikte kullanılması için geçen nesnelerin *üst ortalamasını* kullanmalıdır. Tipik değerler, yüzlerce binlerce kullanıcıya veya sisteme dağıtılan binlerce koleksiyonlar ve uygulamalardır. Testlerin bu limitlerde sistemdeki *Tüm* nesnelerde aynı anda çalışması gerekir. Birçok müşteri birçok özellikten yararlanır, ancak genellikle ürünün tüm özelliklerini bu üst limitlerde kullanmaz. Tüm ürün özellikleriyle test etmek, en iyi sistem genelinde performansın sağlanmasına yardımcı olur ve bazı müşterilerin ortalamanın üzerinde kullanabileceği özellikler için bir arabelleğe izin verir. 

### <a name="loads"></a>Sayfam 
Testler ayrıca sistemde en yüksek kullanım taleplerini üreten simülasyonu gerçekleştirerek standart *Ortalama günde* bir yük üzerinde çalışmalıdır. Bir örnek, sistemin bu günler için bu günlerde güncelleştirme uyumluluk verilerini hemen döndürmesini sağlamak için piyasaya çıkarma Salı düzeltme ekinin benzetimini yapar. Diğer bir örnek, yaygın olarak karşılaşılan bir kötü amaçlı yazılımdan koruma sırasında site etkinliğinin benzetimini sağlar ve bunun zamanında bildirim ve yanıt olması gerekir. Önerilen boyutta dağıtılan makineler belirli bir gün içinde az kullanılabilir olsa da, daha fazla bilgi için bazı işlem arabelleği gerekir.

### <a name="configurations"></a>Yapılandırmalar
Desteklenen işletim sistemleri ve SQL Server sürümlerinin karışımı ile bir dizi fiziksel, Hyper-V ve Azure donanımı üzerinde test çalıştırın. Desteklenen yapılandırma için en kötü durumları her zaman doğrulayın. Genel olarak, Hyper-V ve Azure, benzer şekilde yapılandırıldığında benzer fiziksel donanımlara karşılık gelen performans sonuçlarını döndürür. Daha yeni sunucu işletim sistemleri, daha fazla desteklenen sunucu işletim sistemini eşit veya daha iyi gerçekleştirmeye eğilimlidir. Desteklenen tüm platformlar en düşük gereksinimleri karşılasa da, genellikle Windows ve SQL gibi destekleyici ürünlerin en son sürümleri daha iyi performans üretir. 

En büyük çeşitleme kullanılan SQL Server sürümlerinden gelir. SQL Server sürümleri hakkında daha fazla bilgi için bkz. [HANGI SQL sürümünün çalıştırılmalıyım?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run). 

## <a name="key-performance-determinants"></a>Önemli performans belirlemeleri

Farklı yollarla ve farklı site boyutlarında çeşitli ayarlarla Configuration Manager performansını test edebilir ve ölçebilirsiniz. Aşağıdaki ayarlar ve nesneler performansı ciddi şekilde etkileyebilir. Ortamınızda performansı test ederken ve modellediğinizden emin olun.

> [!CAUTION]
> Configuration Manager birkaç yönü fazla kullanımı önleyen resmi en yüksek düzeyde veya Kullanıcı arabirimi sınırlarına sahip olsa da, yönergelerin ötesinde bir sitenin performansı üzerinde önemli olumsuz etkileri olabilir. Önerilen düzeylerin aşılması veya boyutlandırma kılavuzunun, genellikle daha büyük donanımlar olması gerekir ve çeşitli nesnelerin sıklığını veya sayısını azaltana kadar ortamınızı sürdürülebilir şekilde işleyebilir.

### <a name="hardware-inventory"></a>Donanım envanteri
Temel performansı test etmek için, varsayılan *. mof* dosya boyutu ve yaklaşık %20 ek özellik ile, donanım envanteri toplamayı haftada bir kez ayarlayın. Tüm özellikleri etkinleştirmeyin ve yalnızca gerçekten ihtiyacınız olan özellikleri toplayın. Her zaman *Stok* döngüsüyle *her zaman* değişen kullanılabilir sanal bellek gibi özellikleri toplarken özel bir dikkat ödeyin. Bu özelliklerin toplanması, her bir istemciden her envanter döngüsünün aşırı dalgalanmasına neden olabilir.

### <a name="software-inventory"></a>Yazılım envanteri
Temel performansı test etmek için yazılım envanteri koleksiyonunu haftada bir kez, *yalnızca ürün* ayrıntıları ile ayarlayın. Birçok dosya toplama, envanter alt sistemine önemli bir gerilim yerleştirebilir. . Exe veya * \*. dll*gibi birçok istemcide binlerce dosya toplamayı izleyen filtreler belirtmekten kaçının. * \**

### <a name="collections"></a>Koleksiyonlar
Temel performans testi, çeşitli kapsam, boyut, karmaşıklık ve güncelleştirme ayarlarını içeren binlerce koleksiyonu içerebilir. Site performansı, bir sitede bulunan koleksiyon sayısının doğrudan bir işlevi değildir. Ayrıca, koleksiyonlar ' ın bir çapraz ürünü olan sorgu karmaşıklığı, tam ve artımlı güncelleştirmeler ve değişiklik sıklığı, Koleksiyonlar arasındaki bağımlılıklar ve koleksiyonlardaki istemci sayısı.

Mümkün olduğunda, pahalı veya karmaşık dinamik kural sorguları olan koleksiyonları en aza indirin. Bu tür kurallar gerektiren koleksiyonlar için, sistem üzerinde koleksiyon yeniden değerlendirmesinin etkilerini en aza indirmek için uygun güncelleştirme aralıklarını ve güncelleştirme zamanlarını ayarlayın. Örneğin, 8:00 yerine gece yarısı güncelleştirin.

Koleksiyonlarda artımlı güncelleştirmelerin etkinleştirilmesi, koleksiyon üyeliğine hızlı ve zamanında güncelleştirmelerin yapılmasını sağlar. Ancak artımlı güncelleştirmeler verimli olsa da, yine de sisteme yük yerleştirirler. Üyelik üzerinde neredeyse gerçek zamanlı güncelleştirmeler gereksinimini tahmin ettiğiniz değişiklik sıklığını dengeleyin. Örneğin, koleksiyon üyelerinde ağır karmaşıklığın beklendiğini varsayalım, ancak neredeyse gerçek zamanlı üyelik güncelleştirmelerine ihtiyacınız yoktur. Bu daha verimlidir ve daha az yük oluşturur ve bu, Artımlı güncelleştirmeleri etkinleştirmek yerine, koleksiyonu bir zaman aralığında zamanlanmış bir tam güncelleştirme ile güncelleştirmek için sistemde daha az yük üretir. 

Artımlı güncelleştirmeleri etkinleştirdiğinizde, aynı koleksiyonlardaki zamanlanan tüm güncelleştirmeleri azaltın. Artımlı güncelleştirmeler koleksiyon üyeliğinizi neredeyse gerçek zamanlı olarak güncel tutmaları gerektiğinden, yalnızca bir yedekleme yöntemi vardır. [Koleksiyonlar Için en iyi uygulamalar](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental) , artımlı güncelleştirmeler için en fazla toplam koleksiyon sayısını önerir, ancak makalede işaret ettiği için deneyim birçok etkene göre farklılık gösterebilir.

Yalnızca doğrudan üyelik kuralları olan ve artımlı güncelleştirme gerçekleştirolmayan bir sınırlandırma koleksiyonu olan koleksiyonlar için tam güncelleştirmeler zamanlanması gerekmez. Sistemde gereksiz yükü engellemek için bu tür koleksiyonlar için güncelleştirme zamanlamalarını devre dışı bırakın. Sınırlama koleksiyonu artımlı güncelleştirmeler kullanıyorsa, yalnızca doğrudan üyelik kuralları olan koleksiyonlar, üyelik güncelleştirmelerini 24 saate kadar yansıtmayabilir veya zamanlanan bir yenileme gerçekleşmez.

En iyi yöntem olmasa da, bazı kuruluşlar çeşitli iş işlemlerinin bir parçası olarak yüzlerce veya hatta binlerce koleksiyon oluşturur. Koleksiyon oluşturmak için Otomasyon kullanırsanız, gerekli artımlı güncelleştirmelerin doğru şekilde etkinleştirilmesi önemlidir. Tek bir dönemde koleksiyon değerlendirmesinin etkin noktaları önlemek için tüm tam güncelleştirme zamanlamalarını simge durumuna küçültün ve yayma yapın. Kullanılmayan koleksiyonları silmek için düzenli bir temizlik süreci oluşturun, özellikle de bir süre sonra ihtiyaç duyulmayan koleksiyonlar otomatik olarak oluşturulur.

Configuration Manager, bunlara dağıtımlar gibi görevleri hedeflediğinizde Koleksiyonlarınızdaki tüm nesneler için ilkeler oluşturduğunu unutmayın. Zamanlanan yenileme veya artımlı güncelleştirmeler aracılığıyla üyelik değişiklikleri, tüm sistem için çok sayıda iş oluşturabilir. En son geçerli dal derlemeleri tüm sistemler ve tüm kullanıcılar koleksiyonları için özel ilke iyileştirmeleri içerir. Tüm kuruluşunuzu hedeflerken, yerleşik koleksiyonları bu yerleşik koleksiyonların bir kopyası yerine kullanın.

Koleksiyon performansını daha da ayrıntılı bir şekilde araştırmak için [Configuration Manager araç setinde](https://www.microsoft.com/download/details.aspx?id=50012)koleksiyon değerlendirme görüntüleyicisini (ceviewer) kullanabilirsiniz.

### <a name="discovery-methods"></a>Bulma yöntemleri
Temel performans testi için, sunucu tabanlı bulma yöntemlerini haftada bir kez çalıştırın, Delta keşfini, verileri hafta içinde güncel tutmak için uygun şekilde etkinleştirin. Testler, sanal kuruluş boyutuyla orantılı bir nesne miktarı bulmalıdır. Sinyal bulmanın performans temeli testi haftada bir kez çalışmalıdır.

Bulgu verileri genel verilere sahiptir. Performansla ilgili yaygın bir sorun, bir hiyerarşideki sunucu tabanlı bulma yöntemlerinin yanlış yapılandırılması ve aynı kaynakların birden fazla birincil siteden yinelenmesine neden olur. Birden çok birincil sitede aynı bulma kapsamının çoğaltılmasını önleyerek, Active Directory etki alanı denetleyicileri gibi hedef hizmetle iletişimi iyileştirmek için bulma yöntemlerini dikkatle yapılandırın.

## <a name="general-sizing-guidelines"></a>Genel boyutlandırma yönergeleri 

Önceki [performans testi metodolojisini](#performance-test-methodology)temel alarak, aşağıdaki tablo, belirli sayıda yönetilen istemci için genel *En düşük* donanım gereksinimleri kılavuzunu vermektedir. Bu değerler, belirtilen siteyi yönetmek için gerekli sayıda istemcinin, nesneleri hızlı bir şekilde işlemesini sağlar. Bilgi işlem gücü her yıl fiyatı azaltmaya devam eder ve aşağıdaki bazı gereksinimler modern sunucu donanım yapılandırmalarına göre küçüktür. Aşağıdaki yönergeleri aşan donanımlar, ek işlem gücü gerektiren veya özel ürün kullanım desenlerine sahip olan sitelerin performansını orantılı şekilde artırır. 

| Masaüstü istemcileri  | Site türü/rolü  | Çekirdekler<sup>1</sup>   | Bellek (GB)   | SQL bellek ayırma  | IOPS: gelen kutuları<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Gereken depolama alanı (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25k  | Aynı sunucuda veritabanı site rolüne sahip birincil veya CA 'LAR   | 6   | 24  | %65 | 600  | 1700 | 350  |
| 25k  | Birincil veya CA 'LAR                                              | 4   | 8   |     | 600  |      | 100  |
|      | Uzak SQL                                                  | 4   | 16  | %70 |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50.000  | Aynı sunucuda veritabanı site rolüne sahip birincil veya CA 'LAR   | 8   | 32  | %70 | 1200 | 2800 | 600  |
| 50.000  | Birincil veya CA 'LAR                                              | 4   | 8   |     | 1200 |      | 200  |
|      | Uzak SQL                                                  | 8   | 24  | %70 |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100.000 | Aynı sunucuda veritabanı site rolüne sahip birincil veya CA 'LAR   | 12  | 64  | %70 | 1200 | 5000 | 1100 |
| 100.000 | Birincil veya CA 'LAR                                              | 6   | 12  |     | 1200 |      | 300  |
|      | Uzak SQL                                                  | 12  | 48  | %80 |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150k | Aynı sunucuda veritabanı site rolüne sahip birincil veya CA 'LAR   | 16  | 96  | %70 | 1800 | 7400 | 1600 |
| 150k | Birincil veya CA 'LAR                                   | 8   | 16   |     | 1800  |         | 400   |
|      | Uzak SQL                                       | 16  | 72   | %90 |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700k dili | Aynı sunucuda veritabanı site rolü olan CA 'LAR   | 20+ | 128 + | %80 | 1800 + | 9000 +   | 5000 + |
| 700k dili | CAS                                              | 8 +  | 16  |     | 1800 + |         | 500 +  |
|      | Uzak SQL                                       | 16 | 96 +  | %90 |       | 9000 +   | 4500 + |
|      |                                                             |     |     |     |      |      |      |
| 5k   | İkincil site                                   | 4   | 8    |     | 500   | -       | 200   |
| 15K  | İkincil site                                   | 8   | 16   |     | 500   | -       | 300   |

**Notlar**

1. **Çekirdekler**: Configuration Manager çok sayıda eşzamanlı işlem gerçekleştirir, bu nedenle çeşitli site boyutları için en az sayıda CPU çekirdeğinin olması gerekir. Çekirdekler her yıl daha hızlı sürer, ancak belirli bir minimum çekirdek sayısının paralel olarak çalışmasını sağlamak önemlidir. Genel olarak, 2015 sonrasında üretilen sunucu düzeyi CPU, tabloda belirtilen çekirdekler için temel performans ihtiyaçlarını karşılar. Configuration Manager önerilerin ötesinde ek çekirdeklerden faydalanır, ancak genellikle önerilen en düşük çekirdekler bittikten sonra, mevcut çekirdekler hızını artırmak için CPU kaynak yatırımınızı önceliklendirmelisiniz, daha fazla çekirdek eklemeyin. Örneğin, Configuration Manager, 16 hızlı çekirdekle, daha yavaş çekirdekler ile önemli işlem görevlerinde daha iyi gerçekleştirilir ve bu da disk ıOPS gibi diğer sistem kaynaklarının kullanılabilir olduğunu varsayar.
   
   Çekirdeklerle bellek arasındaki ilişki da önemlidir. Genel olarak, çekirdek başına 3-4 GB 'den az RAM 'e sahip olmak, SQL sunucularınızda toplam işleme yeteneğini azaltır. SQL site sunucusu bileşenleriyle birlikte kullanıldığında çekirdek başına daha fazla RAM gerekir.
   
   > [!NOTE]
   > Tüm testler, en yüksek CPU güç tüketimine ve performansına izin vermek için makine güç planlarını belirler.
   
2. **IOPS: gelen kutuları ve IOPS: SQL** , CONFIGURATION Manager ve SQL mantıksal SÜRÜCÜLERINE yönelik IOPS ihtiyaçlarına yöneliktir. **IOPS: gelen** kutusu sütunu, Configuration Manager gelen kutusu dizinlerinin bulunduğu mantıksal sürücü için IOPS gereksinimlerini gösterir. **IOPS: SQL** sütunu, çeşitli SQL dosyalarının kullandığı mantıksal sürücü (ler) IÇIN toplam IOPS gereksinimlerini gösterir. İki sürücü farklı biçimlendirmeye sahip olması gerektiğinden, bu sütunlar farklıdır. Daha fazla bilgi ve önerilen SQL disk yapılandırmalarına ve dosya en iyi uygulamalarına örnek olarak, dosyaları birden çok birime bölme hakkındaki ayrıntılar da dahil olmak üzere, [site boyutlandırma ve performans hakkında SSS](../../understand/site-size-performance-faq.md)bölümüne bakın.
   
   Bu ıOPS sütunlarının her ikisi de, sektör standardı aracından *DiskSpd*verileri kullanır. Bu ölçümleri çoğaltma yönergeleri için bkz. [disk performansını ölçme](#how-to-measure-disk-performance) . Genel olarak, temel CPU ve bellek gereksinimlerini karşıladıktan sonra, depolama alt sistemi site performansı üzerinde en büyük etkiye sahiptir ve buradaki geliştirmeler, en fazla ödeyerek yatırım sağlar.
   
3.  **Gereken depolama alanı:** Bu gerçek dünya değerleri, belgelenen diğer önerilerden farklı olabilir. Bu numaraları yalnızca genel bir kılavuz olarak sağlıyoruz; tek tek gereksinimler farklılık gösterebilir. Site yüklemeden önce disk alanı ihtiyaçlarını dikkatle planlayın. Bu depolamanın bazı miktarının, zaman içinde boş disk alanı olarak kaldığını varsayın. Bu arabellek alanını bir kurtarma senaryosunda veya kurulum paketi genişletmesi için boş disk alanı gerektiren yükseltme senaryolarında kullanabilirsiniz. Siteniz, büyük miktarlarda veri toplama, daha uzun veri saklama süreleri ve büyük miktarda yazılım dağıtım içeriği için ek depolama alanı gerektirebilir. Ayrıca, bu öğeleri ayrı, düşük işleme hacimleri üzerinde de saklayabilirsiniz.

## <a name="how-to-measure-disk-performance"></a>Disk performansını ölçme 

Çeşitli boyutlardaki Configuration Manager ortamlarının gerektirdiği ıOPS için standartlaştırılmış öneriler sağlamak üzere sektör standardı aracı *DiskSpd* 'yi kullanabilirsiniz. Ayrıntılı olmasa da, aşağıdaki test adımları ve komut satırları, sunucularınızın disk alt sistemi verimini tahmin etmek için basit ve tekrarlanabilir bir yol sağlar. Sonuçlarınızı [genel boyutlandırma yönergeleri](#general-sizing-guidelines) tablosunda önerilen en düşük IOPS ile karşılaştırabilirsiniz. 

Laboratuvar ortamlarında çeşitli donanım yapılandırmalarının test sonuçları için bkz. [örnek disk yapılandırması](#example-disk-configurations) . Sıfırdan yeni bir ortam için depolama alt sistemi tasarlarken, verileri kaba bir başlangıç noktası için kullanabilirsiniz.

### <a name="to-test-disk-iops"></a>Disk ıOPS 'yi test etmek için  
1. *DiskSpd* yardımcı programını şuradan indirin: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. En az 100 GB boş disk alanı olduğundan emin olun. Dizinde, SQL veya SMSExec 'nin etkin virüsten koruma taraması gibi ek yükün kesintiye uğratabilecek veya neden olabileceği uygulamaları devre dışı bırakın.
   
1. Yükseltilmiş bir komut isteminden *DiskSpd* ' i çalıştırın. 
   
   Test etmek istediğiniz birim için, aracın iki çalıştırmasını sırayla gerçekleştirin. İlk test, bir dakika boyunca 64K boyutunda, rastgele yazma işlemleri gerçekleştirir. Bu test, birimin dinamik olarak genişletilmesi durumunda denetleyici önbelleği yükleme ve disk alanı ayırmayı sağlar. İlk testin sonuçlarını atın. İkinci test ilk testi *hemen* izlemelidir ve beş dakika boyunca aynı yükü gerçekleştirmelidir.
   
   Örneğin, G:\\ birimini test etmek için aşağıdaki özel komut satırlarını kullanın.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. **Her s sütununda g/ç** 'de toplam IOPS 'yi bulmak için ikinci testten alınan çıktıyı gözden geçirin. Aşağıdaki örnekte, toplam ıOPS **3929,18**' dir.

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Örnek disk yapılandırması

Aşağıdaki tablolarda, çeşitli test laboratuvarı yapılandırmalarında [disk performansını ölçme](#how-to-measure-disk-performance) bölümünde test adımlarının çalıştırılmasının sonuçları gösterilmektedir. Sıfırdan yeni bir ortam için depolama alt sistemini tasarlarken *kaba* bir başlangıç noktası için bu verileri kullanın. 

### <a name="physical-machines-and-hyper-v"></a>Fiziksel makineler ve Hyper-V 
Donanım her zaman geliştirir. Aşağıda belirtilen performansı aşmamak için, SSD 'Ler ve San 'Lar gibi yeni nesil donanım ve farklı donanım birleşimleri beklenir. Bu sonuçlar, bir sunucu tasarlarken veya donanım satıcınızla tartışırken dikkate alınması gereken temel bir başlangıç noktasıdır.

Aşağıdaki tabloda, çeşitli test laboratuvarı yapılandırmalarında, Dingle ve SSD tabanlı sabit sürücüler dahil olmak üzere çeşitli disk alt sistemlerinde test sonuçları gösterilmektedir. Tüm yapılandırmalarda diskler 64K küme ile biçimlendirilir ve bunları bir kurumsal sınıf disk denetleyicisine ekler. RAID dizi disk sayısına ek olarak, her birinin en az bir yedek diski vardır.

| Disk türü   | Disk sayısı, + 1 yedek disk dahil değildir | MAKTAN     | Ölçülen ıOPS  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15K SAS          | 2                                                  |           1   | 620           |
| 15K SAS          | 4                                                  |           10  | 1206          |
| 15K SAS          | 6                                                  |           10  | 1751          |
| 15K SAS          | 8                                                  |           10  | 2322          |
| 15K SAS          | 10                                                 |           10  | 2882          |
| 15K SAS          | 12                                                 |           10  | 3476          |
| 15K SAS          | 16                                                 |           10  | 4236          |
| 15K SAS          | 20                                                 |           10  | 5148          |
| 15K SAS          | 30                                                 |           10  | 7398          |
| 15K SAS          | 40                                                 |           10  | 9913          |
| SSD SATA         | 2                                                  |           1   | 3300          |
| SSD SATA         | 4                                                  |           10  | 5542          |
| SSD SATA         | 6                                                  |           10  | 7201          |
| SSD SAS          | 2                                                  |           1   | 7539          |
| SSD SAS          | 4                                                  |           10  | 14346         |
| SSD SAS          | 6                                                  |           10  | 15607         |

Bu, örneğin kullanılan cihazlardır. Bu bilgiler, belirli bir donanım modeli veya üreticisi için bir öneri değildir. 

| Disk türü    | Model      | RAID denetleyicisi | Önbellek belleği ve yapılandırma |
|-------------------|-----------------|----------------------|-------------------------------------|
| 15K RPM SAS HD    | HP EH0300JDYTH  | Akıllı dizi P822     | 2 GB, %20 okuma/%80 yazma           |
| SSD SATA          | ATA MK0200GCTYV | Akıllı dizi P420i    | 1 GB, %20 okuma/%80 yazma           |
| SSD SAS           | HP MO0800 JEFPB | Akıllı dizi P420i    | 1 GB, %20 okuma/%80 yazma           |

### <a name="azure-machine-and-disk-performance"></a>Azure makinesi ve disk performansı 
Azure disk performansı, Azure VM 'nin boyutu ve kullandığı disklerin sayısı ve türü gibi çeşitli faktörlere bağlıdır. Azure Ayrıca, aşağıdaki grafikten farklı yeni makine türleri ve disk hızları de ekliyor. Azure 'da çalışan Configuration Manager hakkında daha fazla bilgi ve Azure 'da disk g/ç 'yi anlama hakkında ek bilgiler için, bkz. [Azure hakkında sık sorulan sorular hakkında Configuration Manager](../../understand/configuration-manager-on-azure.md).

Tüm diskler NTFS 64K küme boyutu olarak biçimlendirilir ve birden fazla diske sahip satırlar Windows disk yönetimi yardımcı programı aracılığıyla şeritli birimler olarak yapılandırılır.

| Azure VM| Azure diski| Disk sayısı | Kullanılabilir alan | Ölçülen ıOPS   | Kısıtlama faktörü   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Azure sanal makinesi boyutu   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Azure sanal makinesi boyutu   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Azure sanal makinesi boyutu   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Azure sanal makinesi boyutu   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 MB                    | 1994  | Azure sanal makinesi boyutu   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1024 MB                   | 1992  | Azure sanal makinesi boyutu   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1024 MB                   | 1993  | Azure sanal makinesi boyutu   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2048 MB                   | 1992  | Azure sanal makinesi boyutu   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 MB                    | 2334  | P20 diski        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1024 MB                   | 3984  | Azure sanal makinesi boyutu   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1536 MB                   | 3984  | Azure sanal makinesi boyutu   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1024 MB                   | 3112  | P30 diski        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2048 MB                   | 3984  | Azure sanal makinesi boyutu   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3072 MB                   | 3996  | Azure sanal makinesi boyutu   |
| **'DEN DS5/DS14/F16S**                         | P20                     | 1                   | 512 MB                    | 2335  | P20 diski        |
| **'DEN DS5/DS14/F16S**                         | P20                     | 2                   | 1024 MB                   | 4639  | P20 diski        |
| **'DEN DS5/DS14/F16S**                         | P20                     | 3                   | 1536 MB                   | 6913  | P20 diski        |
| **'DEN DS5/DS14/F16S**                         | P20                     | 4                   | 2048 MB                   | 7966  | Azure sanal makinesi boyutu   |
| **'DEN DS5/DS14/F16S**                         | P30                     | 1                   | 1024 MB                   | 3112  | P30 diski        |
| **'DEN DS5/DS14/F16S**                         | P30                     | 2                   | 2048 MB                   | 6182  | P30 diski        |
| **'DEN DS5/DS14/F16S**                         | P30                     | 3                   | 3072 MB                   | 7963  | Azure sanal makinesi boyutu   |
| **'DEN DS5/DS14/F16S**                         | P30                     | 4                   | 4096 MB                   | 7968  | Azure sanal makinesi boyutu   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | P30 diski        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | P30 diski        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | P30 diski        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Azure sanal makinesi boyutu   |

## <a name="see-also"></a>Ayrıca bkz.

- [Site boyutlandırma ve performans hakkında SSS](../../understand/site-size-performance-faq.md)
- [Configuration Manager Azure hakkında sık sorulan sorular](../../understand/configuration-manager-on-azure.md)
- [Boyut ve ölçek sayıları](size-and-scale-numbers.md)
- [Önerilen donanım](recommended-hardware.md)

