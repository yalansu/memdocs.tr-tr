---
title: Site boyutu ve performans hakkında SSS
titleSuffix: Configuration Manager
description: Site boyutlandırma ve performans hakkında yaygın Configuration Manager soruların yanıtları.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073271"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Configuration Manager site boyutlandırma ve performans hakkında SSS

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu belgede Configuration Manager site boyutlandırma Kılavuzu ve genel performans sorunları hakkında sıkça sorulan sorular ele alınmaktadır.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Makine ve disk yapılandırması SSS ve örnekler

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Site sunucum ve SQL Server diskleri nasıl biçimlendirmem gerekir?

Configuration Manager gelen kutularını ve SQL dosyalarını en az iki farklı birimde ayırın. Bu ayrım, gerçekleştirdikleri farklı g/ç türleri için küme ayırma boyutlarını iyileştirmenize olanak tanır. 

Siteleri sunucu gelen kutularınızı barındıran birimde, 4K veya 8K ayırma birimleri ile NTFS 'yi kullanın. ReFS küçük dosyalar için bile 64K yazar. Configuration Manager birçok küçük dosyaya sahiptir, bu nedenle ReFS gereksiz disk yükü oluşturabilir.

SQL veritabanı dosyalarını içeren diskler için, 64K ayırma birimleri ile NTFS veya ReFS biçimlendirme kullanın.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>SQL veritabanı dosyalarımı nasıl ve nerede yerleşmem gerekir?

Katı hal sürücüleri (SSD) ve Azure Premium Storage 'ın modern dizileri, birkaç disk ile tek bir birimde yüksek ıOPS sağlayabilir. Ek aktarım için değil, genellikle ek depolama için bir diziye daha fazla sürücü eklersiniz. Fiziksel Dingle tabanlı diskler kullanıyorsanız, tek bir birimde oluşturabileceğiniz sayıdan daha fazla ıOPS gerekebilir. *. Mdf* dosyası için ÖNERILEN toplam IOPS ve disk alanının %60 ' sini, *. ldf* dosyası için %20 ve günlük ve veri geçici dosyaları için %20 ' yi ayırmanız gerekir. *. Ldf* ve temp dosyalarının hepsi %40 ile tek bir birimde yer alabilir (%20 + %20) , ayrılmış ıOPS 'niz.

SQL Server 2016 ' den önceki SQL sunucuları varsayılan olarak yalnızca bir Temp veri dosyası tarafından oluşturulmuştur. SQL kilitlerinin önüne geçmek ve tek bir dosyaya erişim beklemek için daha fazla oluşturmanız gerekir. Topluluk eklentileri, oluşturulacak en iyi geçici veri dosyası sayısının dört ile sekiz arasında farklılık gösterir. Test dört ila sekiz arasında küçük bir farklılık gösterir, bu sayede *eşit ölçekli* geçici veri dosyası oluşturabilirsiniz. Tempdb veri dosyalarınız, tam veritabanınızın boyutu% 20-25 ' e kadar olmalıdır.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Disk kurulumu için başka bir öneri var mı?

Yapılandırılabilir olduğunda, RAID denetleyicisi belleğini yazma işlemleri için %70 ayırmayı ve okuma işlemleri için %30 ' a ayarlayın. Genel olarak, site veritabanı için bir RAID 10 dizi yapılandırması kullanın. RAID 1, düşük g/ç gereksinimlerine sahip küçük ölçekli siteler için veya hızlı SSD 'Ler kullanıyorsanız de kabul edilebilir. Daha büyük disk dizileri sayesinde, hatalı diskleri otomatik olarak değiştirmek için yedek diskler yapılandırın.

**Örnek: fiziksel disklere sahip fiziksel makine** 

Birlikte bulunan bir site sunucusu için [boyutlandırma yönergeleri](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) ve **100.000** istemcisi ile SQL Server, SQL Server dosyaları için site sunucusu gelen kutuları ve 5000 IOPS için 1200 IOPS ' dir.

Elde edilen disk yapılandırmanız şöyle görünebilir:

| Sürücüler<sup>1</sup> | MAKTAN | Biçimlendir | Birim içeriği | Gereken minimum ıOPS| Yaklaşık ıOPS sağlandı<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10.000          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | ConfigMgr gelen kutuları    |     1700            | 1751             |
| 12x15k         | 10        | 64K ReFS    | SQL. mdf             | %60 * 5000 = 3000     | 3476             |
| 8x15k          | 10        | 64K ReFS    | SQL. ldf, geçici dosyalar | 40% * 5000 = 2000     | 2322             |

1. Önerilen yedek diskler içermez. 
2. Bu değer, [örnek disk yapılandırmalarından](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)yapılır. 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Windows Server 'da Hyper-V kullanıyorum. En iyi performansı elde etmek için Configuration Manager sanal makinelerimin disklerini nasıl yapılandırmalıyım?

Hyper-V, donanım kaynakları (CPU çekirdekleri ve geçiş depolaması) sanal makineye (VM) ayrılmış %100 ise, fiziksel sunucuya benzer bir performans sağlar. Sabit boyutlu *. vhd* veya *. vhdx* disk dosyalarının kullanılması en az% 1-5 g/ç performans etkisi oluşmasına neden olur. Dinamik olarak genişleyen *. vhd* veya *. vhdx* disk dosyalarının kullanılması, Configuration Manager iş yükü için %25 g/ç performans etkisine neden olur. Diskleri dinamik olarak Genişlemeniz gerekiyorsa, diziye ek %25 ıOPS performansı ekleyerek telafi edin.

Configuration Manager site sunucunuzu veya SQL 'i bir VM içinde çalıştırırken, Hyper-V konağı işletim sistemi sürücüleri VM IŞLETIM sistemi ve veri sürücülerinden ayırın.

VM 'Leri iyileştirme hakkında daha fazla bilgi için bkz. [performans ayarlama Hyper-V sunucuları](/windows-server/administration/performance-tuning/role/hyper-v-server/).

**Örnek: Hyper-V VM tabanlı site sunucusu** 

Birlikte bulunan bir site sunucusu için [boyutlandırma yönergeleri](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) ve **150.000** istemcisi ile SQL Server, SQL Server dosyaları için site sunucusu gelen kutuları ve 7400 IOPS için 1800 IOPS ' dir.

Elde edilen disk yapılandırmanız şöyle görünebilir:

| Sürücüler<sup>1</sup> | MAKTAN | Biçim<sup>2</sup> | Birim içeriği | Gereken minimum ıOPS| Yaklaşık ıOPS sağlandı<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10.000          | 1         | -              | Hyper-V konağı işletim sistemi           | -                    | -                |
| 2x10.000          | 1         | -              | (VM) site sunucusu işletim sistemi       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | (VM) ConfigMgr gelen kutuları    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | 64K ReFS       | (VM) SQL ana bilgisayarı (tüm dosyalar) | 7400                 | 14346            |

1. Önerilen yedek diskler içermez. 
2. Temel alınan birime adanmış VM sürücüsü için sabit boyutlu, geçişli *. vhdx* . 
3. Bu değer, [örnek disk yapılandırmalarından](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)yapılır. 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Microsoft Azure Configuration Manager ortamlar için herhangi bir öneri var mı?

[Azure sıkça sorulan sorular hakkında Configuration Manager](configuration-manager-on-azure.md)okuyarak başlayın.

Premium depolama tabanlı disklerden yararlanan Azure hizmet olarak altyapı (IaaS) VM 'lerinin yüksek ıOPS 'si olabilir. Bu VM 'lerde, ek ıOPS yerine, beklenen disk alanı ihtiyaçları için ek diskler yapılandırın.

Azure depolama, doğal olarak yedekli ve kullanılabilirlik için birden çok disk gerektirmez. Ek alan ve performans sağlamak için Disk Yöneticisi veya depolama alanlarında disk şeritli bir disk oluşturabilirsiniz.

Premium depolama performansını en üst düzeye çıkarmaya ve Azure IaaS VM 'lerinde SQL Server çalıştırmaya ilişkin daha fazla bilgi ve öneriler için bkz.:

- [Uygulama performansını iyileştirme](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Diskler Kılavuzu](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Örnek: Azure tabanlı site sunucusu** 

Birlikte bulunan bir site sunucusu ve **50.000** istemcilerle SQL Server için [boyutlandırma yönergeleri](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) , site sunucusu gelen kutuları için sekız çekirdek, 32 GB ve 1200 IOPS, SQL Server dosyaları için 2800 IOPS 'dir.

Elde edilen Azure makineniz, aşağıdaki disk yapılandırmasına sahip bir DS13v2 (sekiz çekirdek, 56 GB) olabilir:

| Sürücüler | Biçimlendir | Contains | Gereken minimum ıOPS| Yaklaşık ıOPS sağlandı<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Stand&gt; | -             | Site sunucusu işletim sistemi     | -                    | -                |
| 1xP20 (512 GB)    | NTFS 8k       | ConfigMgr gelen kutuları  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | 64K ReFS      | SQL (tüm dosyalar<sup>2</sup>) | 2800                 | 3112             |

1. Bu değer, [örnek disk yapılandırmalarından](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)yapılır.
2. [Azure Kılavuzu](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) , tempdb 'yi yerel, SSD tabanlı *D:* sürücüsüne, kullanılabilir alanı aşmayacak ve ek disk g/ç dağıtımına izin veren bir sürücüye yerleştirmelerine olanak tanır.

**Örnek: Azure tabanlı site sunucusu (hızlı performans artışı için)** 

Azure disk aktarım hızı, VM 'nin boyutuyla sınırlıdır. Önceki Azure örneğinde bulunan yapılandırma gelecekteki genişleme veya ek performansı sınırlayabilir. Azure VM 'nizin ilk dağıtımı sırasında ek diskler eklerseniz, daha düşük bir ön yatırım ile gelecekte daha fazla işlem gücü için Azure VM 'nizi yükseltebilirsiniz. Daha karmaşık bir geçiş yapmak zorunda kalmadan, gereksinimler değiştikçe site performansını artırmaya yönelik daha basit bir işlemdir.

IOPS 'nin nasıl değiştirileceğini görmek için yukarıdaki Azure örneğinde bulunan diskleri değiştirin.

**DS13v2** 

| Sürücüler<sup>1</sup> | Biçimlendir | Contains | Gereken minimum ıOPS| Yaklaşık ıOPS sağlandı<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Stand&gt; | -             | Site sunucusu işletim sistemi     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | ConfigMgr gelen kutuları  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | 64K ReFS      | SQL (tüm dosyalar<sup>3</sup>) | 2800                 | 3984             |

1. Diskler depolama alanları kullanılarak şeritlenmiştir.
2. Bu değer, [örnek disk yapılandırmalarından](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)yapılır. VM boyutu performansı kısıtlar.
3. [Azure Kılavuzu](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) , tempdb 'yi yerel, SSD tabanlı *D:* sürücüsüne, kullanılabilir alanı aşmayacak ve ek disk g/ç dağıtımına izin veren bir sürücüye yerleştirmelerine olanak tanır.

Daha sonra daha fazla performansa ihtiyacınız varsa, VM 'nizi çift CPU ve bellek olacak bir DS14v2 yükseltebilirsiniz. Bu VM boyutu tarafından izin verilen ek disk bant genişliği, daha önce yapılandırılmış disklerinizde kullanılabilir disk ıOPS 'nı anında da artırır.

**DS14v2**

| Sürücüler<sup>1</sup> | MAKTAN | Biçimlendir | Contains | Gereken minimum ıOPS| Yaklaşık ıOPS sağlandı<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Stand&gt; | -             | Site sunucusu işletim sistemi     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | ConfigMgr gelen kutuları  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | 64K ReFS      | SQL (tüm dosyalar<sup>3</sup>) | 2800                 | 6182             |

1. Diskler depolama alanları kullanılarak şeritlenmiştir.
2. Bu değer, [örnek disk yapılandırmalarından](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)yapılır. VM boyutu performansı kısıtlar.
3. [Azure Kılavuzu](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) , tempdb 'yi yerel, SSD tabanlı *D:* sürücüsüne, kullanılabilir alanı aşmayacak ve ek disk g/ç dağıtımına izin veren bir sürücüye yerleştirmelerine olanak tanır.

## <a name="other-common-sql-server-related-performance-questions"></a>Diğer yaygın SQL Server ilgili performans soruları 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>Site sunucusuyla SQL birlikte çalışmak veya uzak bir sunucuda çalıştırmak daha iyi mı?

Her ikisi de, tek bir sunucunun uygun şekilde boyutlandırıldığını varsayarak veya iki sunucu arasında ağ bağlantısı yeterince gerçekleştirilebilir.

Uzak SQL, ek bir sunucunun ön ve operasyonel maliyetini gerektirir, ancak büyük ölçekli müşterilerin çoğunluğu arasında tipik bir davranıştır. Bu yapılandırmanın avantajları şunlardır:

- SQL Always on gibi daha fazla site kullanılabilirliği seçenekleri
- Site işlemeye daha az sayıda fazla duymak ile ağır raporlama çalıştırma olanağı
- Bazı durumlarda daha basit olağanüstü durum kurtarma
- Daha kolay güvenlik yönetimi
- Ayrı bir DBA ekibi ile gibi SQL yönetimi için rol ayrımı

Birlikte bulunan SQL tek bir sunucu gerektirir ve genellikle küçük ölçekli müşterilerin çoğu için tipik bir davranıştır. Bu yapılandırmanın avantajları şunlardır:

- Makineler, lisanslar ve bakım için düşük maliyetler
- Sitede daha az başarısızlık noktası
- Planlama kapalı kalma süresi için daha iyi denetim

### <a name="how-much-ram-should-i-allocate-for-sql"></a>SQL için ne kadar RAM ayıramalıyım?

Varsayılan olarak, SQL sunucunuzdaki kullanılabilir tüm belleği kullanır, bu da işletim sistemini ve makinedeki diğer süreçlerini de bozabilir. Olası performans sorunlarından kaçınmak için, SQL 'e açık bir şekilde bellek ayırmak önemlidir. SQL sunucularıyla birlikte bulunan site sunucularında, işletim sisteminin dosya önbelleği ve diğer işlemler için yeterli RAM 'e sahip olduğundan emin olun. SMSExec ve diğer Configuration Manager işlemlerinde kalan miktarda RAM bulunduğundan emin olun. SQL 'i uzak bir sunucuda çalıştırırken, belleğin *çoğunluğunu* SQL 'e ayırabilirsiniz ancak hepsini kullanamazsınız. İlk kılavuz için [boyutlandırma kılavuzunu](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) gözden geçirin. 

SQL Server bellek ayırma tam GB 'a yuvarlanır. Ayrıca, büyük miktarlarda RAM arttıkça SQL 'in daha yüksek bir yüzdesine sahip olmasına izin verebilirsiniz. Örneğin, 256 GB veya daha fazla RAM varsa, işletim sistemi için çok sayıda belleği koruyan için SQL 'i %95 ' e varan bir şekilde yapılandırabilirsiniz. Sayfa dosyasını izlemek, işletim sistemi ve Configuration Manager işlemleriyle ilgili yeterli bellek olduğundan emin olmanın iyi bir yoludur.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Çekirdekler bu günlerde tek bir şeçlardır. SQL Server 'larıma yalnızca bir grup eklemem gerekiyor mu?

16 ' dan fazla fiziksel çekirdek varsa ve SQL Server 'da yeterli RAM yoksa, bellek çekişmesi sorunları yaşayabilirsiniz. SQL için çekirdek başına en az 3-4 GB RAM kullanılabilir olduğunda Configuration Manager iş yükü daha iyi çalışır. SQL sunucularınıza çekirdek eklerken, MIKTARı orantılı tutarlarda arttırdığınızdan emin olun.

### <a name="will-sql-always-on-impact-my-performance"></a>SQL her zaman performansumu etkiler mi?

Genel olarak, SQL çoğaltma sunucuları arasında yeterli ağ varsa, SQL her zaman açık, sistemin performansı üzerinde etkisiz bir etkiye sahiptir. Yoğun bir SQL Always on ortamında hızlı veritabanı günlüğü *. ldf* dosyası büyümesini sağlayabilirsiniz. Ancak, başarılı bir veritabanı yedeklemesinden sonra günlük dosyası alanı otomatik olarak serbest bırakılır. Bir yedekleme gerçekleştirmek için Configuration Manager veritabanı için bir SQL işi ekleyin, örneğin her 24 saatte bir ve altı saatte bir *. ldf* yedeklemesi. SQL yedekleme stratejileri hakkında daha fazla bilgi için bkz. SQL her zaman açık ve Configuration Manager hakkında daha fazla bilgi için, [yüksek oranda kullanılabilir site veritabanı için SQL Server her zaman açık](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="should-i-enable-sql-compression-on-my-database"></a>Veritabanımda SQL sıkıştırmasını etkinleştirmem gerekir mi?

Configuration Manager veritabanı için SQL sıkıştırması önerilmez. Configuration Manager veritabanında sıkıştırmayı etkinleştirme konusunda işlevsel bir sorun olmadığından, test sonuçları sisteme olası boyutlandırılabilir performans etkisi ile karşılaştırıldığında çok fazla boyut tasarrufu göstermez.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>Veritabanımda SQL şifrelemeyi etkinleştirmem gerekir mi?

Configuration Manager veritabanındaki tüm gizli dizileri zaten güvenli bir şekilde depolanır, ancak SQL şifrelemesi eklendiğinde başka bir güvenlik katmanı da eklenebilir. Veritabanınızda şifrelemeyi etkinleştirmekle ilgili işlevsel bir sorun yoktur, ancak şifrelemeyi seçtiğiniz tablolara ve kullanmakta olduğunuz SQL sürümüne bağlı olarak %25 oranında bir performans düşüşü olabilir. Bu nedenle, özellikle büyük ölçekli ortamlarda dikkatli bir şekilde şifreleyin. Ayrıca, şifrelenmiş verileri başarıyla Kurtaracağınızdan emin olmak için yedekleme ve kurtarma planlarınızı güncelleştirmeyi unutmayın.

### <a name="what-version-of-sql-should-i-run"></a>Hangi SQL sürümünü çalıştırmalıyım?

SQL 'in desteklenen sürümleri için bkz. [SQL Server sürümleri Için destek](../plan-design/configs/support-for-sql-server-versions.md). Performans açısından, tüm desteklenen SQL sürümleri gerekli performans ölçütlerini karşılar. Bununla birlikte, SQL 2012 ve SQL 2016 ya da daha yeni bir sürümü, Configuration Manager iş yükünün bazı yönlerini SQL 2014 olarak gerçekleştirmeye eğilimlidir. Ayrıca, SQL 2012 uyumluluk düzeyinde (110) SQL 2014 çalıştırmak genel olarak performansı geliştirir. Yükleme zamanında, SQL 2012 ve SQL 2014 ' de çalışan Configuration Manager veritabanları uyumluluk düzeyi 110 olarak ayarlanmıştır. SQL 2016 veya daha yeni bir sürümü, SQL sürümünün varsayılan uyumluluk düzeyine ayarlanmıştır (örneğin, SQL 2016 için 130). SQL 'in yerinde yükseltilmesi, geçerli dal sürümünü bir sonraki ana Configuration Manager yükleyene kadar uyumluluk düzeylerini güncelleştirmez. 

SQL 2016 veya sonraki sürümleri üzerinde, yönetim konsolunda RBAC kullanırken olduğu gibi olağan dışı zaman aşımları veya yavaşlarsa, Configuration Manager veritabanındaki SQL uyumluluk düzeyini 110 olarak değiştirmeyi deneyin. SQL 2014 ' de SQL uyumluluk düzeyi 110 ' de çalışıyor ve SQL 'in daha yeni sürümleri tam olarak desteklenmektedir. Daha fazla bilgi için bkz. [SQL sorgu zaman aşımı veya konsol, bazı Configuration Manager veritabanı sorgularında yavaş](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d).

Bazı bilinen performansla ilgili veya diğer olası sorunlar nedeniyle, Ocak 2018 itibariyle aşağıdaki SQL sürümlerinden *kaçının* :

- SQL 2012 SP3 CU1 to CU5
- SQL 2014 SP1 CU6 SP2 CU2 UYGULAMAZSANıZ
- SQL 2016 RTM-CU3, SP1 CU3 to CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>Herhangi bir ek SQL dizin oluşturma görevi uygulamam gerekir mi?

Evet, bir hafta ve istatistiklerin her sıklıkta, SQL performansını geliştirmek için günde bir kez ve istatistikleri güncelleştirin. Configuration Manager ve SQL topluluklarında sunulan üçüncü taraf betikler ve ek bilgiler bu görevlerin iyileştirmenize yardımcı olabilir.

Büyük sitelerde, kullanım modellerinize bağlı olarak, CI\_currentkarmaşıkancestatusdetails, Htuchangelog gıbı bazı SQL tabloları büyük olabilir. Bakım yaklaşımınızı tek tek azaltmanız veya değiştirmeniz gerekebilir.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>İkincil sitemdeki SQL Express yerine tam SQL Server ne zaman kullanmalıyım?

SQL Express ikincil sitelerde önemli performans etkilerine sahip değildir ve çoğu müşteri için yeterlidir. Dağıtımı ve yönetimi de kolaydır ve neredeyse tüm müşteriler için herhangi bir boyuttaki önerilen yapılandırma vardır.

Tam SQL Server yüklemesi gerekebilecek bir durum vardır. Ortamınızda çok sayıda dağıtım noktası ve paket veya kaynak varsa, SQL Express 'in 10 GB 'lık boyut sınırını aşmanız mümkündür. Paket sayısı, dağıtım noktası sayısının 4.000.000 ' den fazla olması halinde, 2.000 2.000 ' den fazla içerik SQL Server, ikincil siteleriniz üzerinde tam kullanmayı göz önünde bulundurun. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>My veritabanındaki MaxDOP ayarlarını değiştirmem gerekir mi?

Ayarınızı 0 ' da bırakmak (tüm kullanılabilir işlemcileri kullan) çoğu durumda genel işlem performansı için idealdir.

Birçok Configuration Manager yöneticisi, [SQL Server ' de "en yüksek paralellik derecesi" yapılandırma seçeneği Için öneriler ve yönergeler](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi)konusundaki yönergeleri izler. Çoğu modern büyük donanımda Bu kılavuz, önerilen en yüksek ayar olan sekiz ' a yol açar. Ancak, işlemci sayısından karşılaştırıldığında çok daha küçük bir sorgu çalıştırırsanız, bu, daha yüksek bir sayıya ayarlamaya yardımcı olabilir. Kendinizi sekiz ile sınırlamak, daha fazla çekirdek kullanılabilir olduğunda daha büyük sitelerde en iyi ayar değildir. 

Sekiz ' dan fazla çekirdeği olan SQL sunucularında, 0 ayarıyla başlayın ve yalnızca performans sorunları veya aşırı kilit yaşarsanız değişiklikler yapın. 0 ' da performans sorunlarından karşılaşdığı için MaxDOP 'yi değiştirmeniz gerekiyorsa, bu sitenin SQL Server boyutlandırması için önerilen en düşük çekirdek sayısına eşit veya daha büyük olan yeni bir değerle başlayın. Bu değerden düşük olacak şekilde neredeyse her zaman olumsuz performans olumsuz etkileri vardır. Örneğin, bir 100.000 İstemci sitesinin uzak SQL Server 'ı için en az 12 çekirdek gerekir. SQL Server 'da 16 çekirdek varsa, MaxDOP ayarınızı 12 değeriyle test etmeye başlayın.

## <a name="other-common-performance-related-questions"></a>Diğer yaygın performansla ilgili sorular

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Site sunucusundaki (veya diğer rollerdeki) klasörler virüsten koruma yazılımı için dışlanmalıyım?

Herhangi bir sistemde virüsten koruma korumasını devre dışı bırakırken dikkatli olunması gerçekleştirin. Yüksek hacimli ve güvenli ortamlarda, en iyi performans için *etkin izlemeyi* devre dışı bırakmayı öneririz.

Önerilen virüsten koruma dışlamaları hakkında daha fazla bilgi için, [Configuration Manager 2012 ve güncel dalı site sunucuları, site sistemleri ve istemciler Için önerilen virüsten koruma dışlamaları](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu)bölümüne bakın.

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>Configuration Manager ile kullanıldığında WSUS daha iyi hale getirmek için ne yapabilirim?

WsusPool kuyruk uzunluğu ve WsusPool özel bellek sınırı gibi birkaç temel IIS ayarını değiştirmek, daha küçük yüklemelerde bile WSUS performansını iyileştirebilir. Daha fazla bilgi için bkz. [Önerilen donanım](../plan-design/configs/recommended-hardware.md).

Ayrıca, WSUS çalıştıran işletim sistemi için en son güncelleştirmelerin yüklü olduğundan emin olun:

- Windows Server 2012:2017 veya üzeri sürümlerde yayınlanan "yalnızca güvenlik" toplu güncelleştirmesi yayınlandı. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2:2017 veya üzeri sürümlerde yayınlanan "yalnızca güvenlik" toplu güncelleştirmesi. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Window Server 2016:2017 veya üzeri bir sürümde yayınlanan "yalnızca güvenlik" olmayan toplu güncelleştirme. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>WSUS sunucularıma ne tür bir bakım çalıştırmalıyım?

[MICROSOFT WSUS ve CONFIGURATION Manager SUP bakımı için tüm kılavuzu](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)inceleyin.

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Sitem için temel performans izleme ayarlamak istiyorum. Ne seyretmek gerekir?

Geleneksel sunucu performansı izleme, genel Configuration Manager için etkin bir şekilde kullanılabilir. Sunucularınızın temel sistem durumunu izlemek için Configuration Manager, SQL Server ve Windows Server için çeşitli System Center Operations Manager yönetim paketlerinden da yararlanabilirsiniz. Ayrıca, Configuration Manager Windows performans Izleyicisi (PerfMon) sayaçlarını doğrudan izleyebilirsiniz. Olası site performansı sorunlarının veya biriktirme listelerinin erken uyarı işaretleri için çeşitli gelen kutularındaki biriktirme listeleri izleyin.

## <a name="see-also"></a>Ayrıca bkz.

- [Site boyutlandırma ve performans yönergeleri](../plan-design/configs/site-size-performance-guidelines.md)
- [Configuration Manager Azure hakkında sık sorulan sorular](configuration-manager-on-azure.md)
