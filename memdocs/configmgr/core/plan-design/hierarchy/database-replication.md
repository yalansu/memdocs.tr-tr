---
title: Veritabanı çoğaltması
titleSuffix: Configuration Manager
description: Configuration Manager veritabanı çoğaltmasının hiyerarşideki verileri aktarmak için SQL Server nasıl kullandığını öğrenin.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b495b02-c966-4eb3-92b9-52ebbf5c38ae
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d1a2c8baa349e6499aa483f947d94f7459357be4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720201"
---
# <a name="database-replication"></a>Veritabanı çoğaltması

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager veritabanı çoğaltması, verileri aktarmak için SQL Server kullanır. Site veritabanındaki değişiklikleri hiyerarşideki diğer sitelerdeki bilgilerle birleştirmek için bu yöntemi kullanır.

Veritabanı çoğaltmasıyla ilgili aşağıdaki noktalara göz önünde edin:

- Tüm siteler aynı bilgileri paylaşır.  

- Bir siteyi bir hiyerarşiye yüklediğinizde, Configuration Manager otomatik olarak yeni siteyle onun üst sitesi arasında veritabanı çoğaltması kurar.  

- Site yüklemesi tamamlandığında, veritabanı çoğaltması otomatik olarak başlatılır.  

Bir hiyerarşiye yeni bir site eklediğinizde, Configuration Manager yeni sitede genel bir veritabanı oluşturur. Üst site, veritabanında ilgili verilerin bir anlık görüntüsünü oluşturur. Ardından, [dosya tabanlı çoğaltma](file-based-replication.md)kullanarak anlık görüntüyü yeni siteye aktarır. Yeni site daha sonra SQL Server toplu kopyalama programı (BCP) kullanarak bilgileri Configuration Manager veritabanının yerel kopyasına yükler. Anlık görüntü yüklendikten sonra her site diğer siteyle veritabanı yinelemesi gerçekleştirir.  

Siteler arasında veri çoğaltmak için Configuration Manager kendi veritabanı yineleme hizmetini kullanır. Veritabanı çoğaltma hizmeti, değişiklikler için yerel site veritabanını izlemek üzere değişiklik izleme SQL Server kullanır. Daha sonra SQL Server Hizmet Aracısı (SSB) kullanarak değişiklikleri diğer sitelere çoğaltır. Bu işlem varsayılan olarak 4022 numaralı TCP bağlantı noktasını kullanır.  


## <a name="replication-groups"></a>Çoğaltma grupları

Configuration Manager, veritabanı çoğaltmasına göre çoğaltılan verileri farklı çoğaltma gruplarına gruplandırır. Her çoğaltma grubunun ayrı, sabit bir çoğaltma zamanlaması vardır. Site bu zamanlamayı, diğer sitelerdeki değişiklikleri ne sıklıkta çoğaltacağını öğrenmek için kullanır.  

Örneğin, rol tabanlı yönetim yapılandırmasında yapılan bir değişiklik, diğer sitelere hızlıca çoğaltılır. Bu davranış, diğer sitenin bu değişiklikleri hızlı bir şekilde zorlayabilmenizi sağlar. Yeni bir ikincil site yüklemek için bir istek gibi daha düşük öncelikli bir yapılandırma değişikliği, daha az acille çoğaltılır. Yeni site isteğinin hedef birincil siteye ulaşması birkaç dakika sürebilir.  


## <a name="settings"></a>Ayarlar

Veritabanı çoğaltması için aşağıdaki ayarları değiştirebilirsiniz:  

- **Veritabanı çoğaltma bağlantıları**: belirli bir trafiğin ağdan ne zaman geçeceğini denetleyin.  

- **Dağıtılmış görünümler**: bir merkezi yönetim SITESI (CAS) Seçili site verilerini istediğinde, verileri doğrudan bir alt birincil sitedeki veritabanından erişebilir.  

- **Zamanlamalar**: bir çoğaltma bağlantısının ne zaman kullanıldığını ve farklı site verisi türlerinin ne zaman çoğaltılacağını belirtin.  

- **Özetleme**: çoğaltma bağlantılarından geçen ağ trafiğiyle ilgili veri özetleme ayarlarını değiştirin. Varsayılan olarak, özetleme her 15 dakikada bir gerçekleşir. Veritabanı çoğaltmasıyla ilgili raporlarda kullanılır.  

- **Veritabanı çoğaltma eşikleri**: sitenin ne zaman düşürülmüş veya başarısız olarak rapor raporlamadığı tanımlar. Ayrıca, Configuration Manager düşürülmüş veya başarısız durumuna sahip çoğaltma bağlantıları hakkında ne zaman uyarı vereceğini yapılandırabilirsiniz.  


## <a name="types-of-data"></a>Veri türleri

Configuration Manager birincil olarak, çoğaltılan verileri *genel veri* veya *site verileri*olarak sınıflandırır. Veritabanı çoğaltması gerçekleştiğinde, site veritabanı çoğaltma bağlantısı genelinde genel verilere ve site verilerine yapılan değişiklikleri aktarır. Genel veriler bir üst veya alt siteye çoğaltılır. Site verileri yalnızca bir üst siteye çoğaltılır. Üçüncü veri türü, *yerel veriler*diğer sitelere çoğaltılmaz. Yerel veriler, diğer sitelerin gerekli olmadığı bilgiler.  

### <a name="global-data"></a>Genel veriler

Genel veriler, hiyerarşi genelinde tüm sitelere çoğaltılan, yönetici tarafından oluşturulmuş nesnelerdir. İkincil siteler genel proxy verileri olarak yalnızca bir genel veri alt kümesini alır. CAS ve birincil sitelerde genel veriler oluşturursunuz. Bu tür aşağıdaki verileri içerir:

- Yazılım dağıtımları
- Yazılım güncelleştirmeleri
- Koleksiyon tanımları
- Rol tabanlı yönetim güvenlik kapsamları

### <a name="site-data"></a>Site verileri

Site verileri, Configuration Manager birincil siteler ve kendilerine atanan istemciler tarafından oluşturulan işletimsel bilgiler. Site verileri, CA 'lara çoğaltılır, ancak diğer birincil sitelere uygulanmaz. Site verileri yalnızca CA 'larda ve verilerin kaynaklandığı birincil sitede görüntülenebilir. Site verilerini yalnızca sizin oluşturduğunuz birincil sitede değiştirebilirsiniz. Bu tür aşağıdaki verileri içerir:

- Donanım envanteri
- Durum iletileri
- Uyarılar
- Sorgu tabanlı koleksiyonların sonuçları

Tüm site verileri CA 'lara çoğaltılır. CA 'LAR tüm site hiyerarşisi için yönetim ve raporlama yapar.  


## <a name="database-replication-links"></a><a name="bkmk_Dblinks"></a>Veritabanı çoğaltma bağlantıları

Bir hiyerarşiye yeni bir site yüklediğinizde, Configuration Manager otomatik olarak üst siteyle yeni site arasında bir veritabanı çoğaltma bağlantısı oluşturur. İki siteyi bağlamak için tek bir bağlantı oluşturur.  

Çoğaltma bağlantısı genelinde verilerin aktarımını denetlemek için, her bir bağlantı için ayarları değiştirin. Her yineleme bağlantısı ayrı yapılandırmaları destekler. Her veritabanı çoğaltma bağlantısı aşağıdaki denetimleri içerir:  

- Seçilen site verilerinin birincil siteden CA 'lara çoğaltılmasını durdurun. Bu eylem, CA 'ların bu verilere doğrudan birincil sitenin veritabanından erişmesine neden olur.  

- Seçili site verilerini bir alt birincil siteden CA 'lara aktarılacak şekilde zamanlayın.

- Bir veritabanı çoğaltma bağlantısının ne zaman düşürülmüş veya başarısız durumuna sahip olduğunu belirleyen ayarları tanımlayın.

- Başarısız bir çoğaltma bağlantısı için ne zaman uyarı verileceğini belirtin.

- Configuration Manager, çoğaltma bağlantısını kullanan çoğaltma trafiği hakkındaki verileri ne sıklıkta özetleyeceğini belirtin. Bu verileri raporlarda kullanır.

Veritabanı çoğaltması bağlantısını yapılandırmak için, Configuration Manager konsolunda **izleme** çalışma alanına gidin. **Veritabanı çoğaltma** düğümünü seçin ve bağlantının özelliklerini düzenleyin. Bu düğüm, **Hiyerarşi Yapılandırması** düğümü altındaki **Yönetim** çalışma alanında da bulunur. Çoğaltma bağlantısının üst sitesinden veya alt sitesinden bir çoğaltma bağlantısı düzenleyin.  

> [!TIP]  
> Veritabanı çoğaltma bağlantılarını herhangi bir çalışma alanının **Veritabanı Çoğaltma** düğümünden düzenleyebilirsiniz. Ancak, **izleme** çalışma alanındaki **veritabanı çoğaltması** düğümünü kullandığınızda, veritabanı çoğaltmasının durumunu da görüntüleyebilirsiniz. Ayrıca [Çoğaltma Bağlantısı Çözümleyicisi](../../servers/manage/monitor-replication.md#BKMK_RLA) aracına erişim sağlar. Veritabanı çoğaltmasıyla ilgili sorunları araştırmaya yardımcı olması için bu aracı kullanın.  

Çoğaltma bağlantılarını yapılandırma hakkında daha fazla bilgi için bkz. [site veritabanı çoğaltma denetimleri](#BKMK_DBRepControls). Çoğaltmanın nasıl izleneceği hakkında daha fazla bilgi için bkz. [veritabanı çoğaltmasını izleme](../../servers/manage/monitor-replication.md).  


## <a name="distributed-views"></a><a name="bkmk_distviews"></a> Dağıtılmış görünümler  

Dağıtılmış görünümler aracılığıyla, Seçili site verileri için CA 'larda bir istek yaptığınızda, alt birincil sitedeki veritabanına doğrudan erişir. Bu doğrudan erişim, site verilerini birincil siteden CA 'lara çoğaltma gereksinimini ortadan kaldırır. Her çoğaltma bağlantısı diğer çoğaltma bağlantılarından bağımsız olduğu için, seçtiğiniz çoğaltma bağlantılarında dağıtılmış görünümleri kullanabilirsiniz. Bir birincil site ile ikincil site arasında dağıtılmış görünümleri kullanamazsınız.  

Dağıtılmış görünümler aşağıdaki avantajları sağlar:  

- CA 'larda ve birincil sitelerde veritabanı değişikliklerini işlemek için CPU yükünü azaltma

- Ağ üzerinden CA 'lara aktarılan veri miktarını azaltma

- CAS veritabanını barındıran SQL Server performansını geliştirme

- CAS veritabanı tarafından kullanılan disk alanını azaltın

Bir birincil site, ağdaki CA 'lara yakından eklendiğinde, iki site her zaman açık ve her zaman bağlı olduğunda dağıtılmış görünümleri kullanmayı göz önünde bulundurun. Dağıtılmış görünümler, her sitedeki SQL Server 'lar arasında doğrudan bağlantıya sahip siteler arasındaki seçili verilerin çoğaltılmasını değiştirir. CAS, bu verileri her istediğinizde doğrudan bir bağlantı oluşturur.

Site, aşağıdaki örnek senaryolarda dağıtılmış görünüm verileri ister:

- Raporları veya sorguları çalıştırdığınızda
- Kaynak Gezgini bilgileri görüntülediğinizde
- Site veri tabanlı kuralları içeren koleksiyonlar için koleksiyon değerlendirmesi

Varsayılan olarak, Dağıtılmış görünümler her bir çoğaltma bağlantısı için kapalıdır. Dağıtılmış görünümleri açtığınızda, bu bağlantı genelindeki CA 'lara çoğaltılmayacak site verilerini seçersiniz. CAS bu verilere bağlantıyı paylaşan alt birincil sitenin veritabanından doğrudan erişir. Dağıtılmış görünümler için aşağıdaki site verisi türlerini yapılandırabilirsiniz:  

- İstemcilerden **donanım envanteri** verileri
- İstemcilerden **yazılım envanteri ve yazılım kullanım ölçümü** verileri
- İstemcilerden, birincil siteden ve tüm ikincil sitelerden **durum iletileri**

Configuration Manager konsolundaki veya raporlardaki verileri görüntülediğinizde, Dağıtılmış görünümler sizin için de görünmez hale gelir. Dağıtılmış görünümler için etkinleştirilen verileri istediğinizde, CAS site veritabanı sunucusu, bilgileri almak için alt birincil sitenin veritabanına doğrudan erişir.

Örneğin, CA 'lara bağlı bir Configuration Manager konsolu kullanırsınız. İki birincil siteden donanım envanteri hakkında bilgi isteğinde bulabilirsiniz: ABC ve XYZ. Yalnızca ABC sitesindeki Dağıtılmış görünümler için donanım envanterini etkinleştirdiniz. CAS, XYZ istemcilerinin envanter bilgilerini kendi veritabanından alır. CAS, ABC istemcilerinin envanter bilgilerini doğrudan ABC sitesindeki veritabanından alır. Bu bilgiler Configuration Manager konsolunda veya kaynak tanımlanmaksızın bir raporda görüntülenir.  

Bir çoğaltma bağlantısında dağıtılmış görünümler için etkinleştirilmiş bir veri türü varsa, alt birincil site bu verileri CA 'lara çoğaltmaz. Bir veri türü için dağıtılmış görünümleri kapattığınızda, alt birincil site, CA 'lara normal veri çoğaltmayı sürdürür. Bu verilerin CA 'larda kullanılabilmesi için, bu veriler için çoğaltma gruplarının birincil site ile CA 'LAR arasında yeniden başlatılması gerekir. Dağıtılmış görünümleri açık olan bir birincil siteyi kaldırdıktan sonra, CA 'larda Dağıtılmış görünümler için etkinleştirilen verilere erişebilmeniz için CA 'ların verilerinin yeniden başlatılması gerekir.  

> [!IMPORTANT]  
> Site hiyerarşisindeki herhangi bir çoğaltma bağlantısında dağıtılmış görünümleri kullandığınızda herhangi bir birincil siteyi kaldırmadan önce, tüm çoğaltma bağlantıları için dağıtılmış görünümleri kapatın. Daha fazla bilgi için bkz. [Dağıtılmış görünümler kullanan bir birincil siteyi kaldırma](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews).  

### <a name="prerequisites-and-limitations-for-distributed-views"></a>Dağıtılmış görünümler için Önkoşullar ve sınırlamalar  

- Yalnızca CA 'LAR ve birincil site arasındaki çoğaltma bağlantılarında dağıtılmış görünümleri kullanın.

- CA 'LAR SQL Server Enterprise sürümünü kullanmalıdır. Birincil sitede bu gereksinim yoktur.

- CAS, SMS sağlayıcısı 'nın yalnızca bir örneğini içerebilir. Bu tek örneği site veritabanı sunucusuna yükler. Bu yapılandırma Kerberos kimlik doğrulamasını destekler. CA 'larda SQL Server, alt birincil sitedeki SQL Server 'a erişmek için Kerberos gerektirir. Alt birincil sitedeki SMS Sağlayıcısı ile ilgili bir sınırlama yoktur.

- CAS 'ye yalnızca bir raporlama hizmetleri noktası yükleyebilirsiniz. SQL Server Reporting Services site veritabanı sunucusuna yükler. Bu yapılandırma Kerberos kimlik doğrulamasını destekler. CA 'larda SQL Server, alt birincil sitedeki SQL Server 'a erişmek için Kerberos gerektirir.

- Site veritabanını bir [SQL Server kümesinde](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)barındıralamazsınız.

- Sürüm 1902 ve önceki sürümlerde, site veritabanını [SQL Server Always on kullanılabilirlik grubunda](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)barındıralamazsınız. Bu yapılandırmayı desteklemek için sürüm 1906 veya sonraki bir sürüme güncelleştirin.<!-- SCCMDocs-pr#3792 -->

- CAS veritabanı sunucusunun bilgisayar hesabı, birincil site veritabanında **okuma** izinleri gerektirir.

> [!IMPORTANT]  
> Verilerin çoğaltılacağı durum için Dağıtılmış görünümler ve [zamanlamalar](#BKMK_schedules) , bir veritabanı yineleme bağlantısı için birbirini dışlamalı ayarlar.  


## <a name="schedule-transfers-of-site-data"></a><a name="BKMK_schedules"></a>Site verilerinin aktarımlarını zamanlama

Site verilerini bir alt birincil siteden CA 'lara çoğaltmak için kullanılan ağ bant genişliğini denetlemenize yardımcı olması için, bir çoğaltma bağlantısının ne zaman kullanıldığını zamanlayın. Ardından farklı site verisi türlerinin ne zaman çoğaltılacağını belirtin. Birincil sitenin durum iletilerini, envanteri ve ölçüm verilerini ne zaman çoğaltacağını denetleyebilirsiniz. İkincil sitelerden veritabanı çoğaltması bağlantıları, site verileri için zamanlamaları desteklemez. Genel verilerin aktarımını zamanlayamazsınız.  

Bir veritabanı çoğaltması bağlantı zamanlaması yapılandırdığınızda, seçilen site verilerinin birincil siteden CA 'lara aktarılmasını kısıtlayabilirsiniz. Ayrıca farklı site verisi türlerini çoğaltmak için farklı zamanlar yapılandırabilirsiniz.  

> [!IMPORTANT]  
> Verilerin çoğaltılacağı durum için [Dağıtılmış görünümler](#bkmk_distviews) ve zamanlamalar, bir veritabanı çoğaltma bağlantısı için birbirini dışlayan yapılandırmalara sahiptir.  


## <a name="summarization-of-traffic"></a><a name="BKMK_SummarizeDBReplication"></a>Trafik Özeti  

Her site, site için veritabanı çoğaltma bağlantılarını geçen ağ trafiği hakkındaki verileri düzenli aralıklarla özetler. Site, veritabanı çoğaltması için raporlarda özetlenen verileri kullanır. Çoğaltma bağlantısındaki her iki site de, çoğaltma bağlantısını çapraz geçen ağ trafiğini özetler. Site veritabanı sunucusu, verileri özetler. Veriler özetledikten sonra, bilgiler diğer sitelere genel veri olarak çoğaltılır.  

Varsayılan olarak, özetleme her 15 dakikada bir gerçekleşir. Ağ trafiği için Özetleme sıklığını değiştirmek üzere, veritabanı çoğaltması bağlantısının özelliklerinde **özetleme aralığı**' nı düzenleyin. Özetleme sıklığı, veritabanı çoğaltmasıyla ilgili raporlarda görüntülediğiniz bilgileri etkiler. 5 ila 60 dakika arasında bir Aralık seçebilirsiniz. Özetleme sıklığını arttırdığınızda, çoğaltma bağlantısındaki her bir sitede SQL Server'daki işleme yükünü arttırmış olursunuz.  

## <a name="database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a>Veritabanı çoğaltma eşikleri

Veritabanı çoğaltma eşikleri Configuration Manager, bir veritabanı çoğaltması bağlantısının durumunu düşürülmüş veya başarısız olarak ne zaman raporluyor tanımlar. Varsayılan olarak, herhangi bir çoğaltma grubu art arda 12 deneme için çoğaltmayı tamamlayamazsa, bir bağlantı *düşürülmüş* olarak ayarlanır. Herhangi bir çoğaltma grubu, art arda oluşan 24 girişimde çoğaltılamazsa bağlantıyı *başarısız* olarak ayarlar.  

Düşürülmüş veya başarısız durumu için özel değerler belirtebilirsiniz. Bu değerleri ayarlarsanız, bağlantılar arasında veritabanı çoğaltmasının durumunu daha doğru bir şekilde izleyebilirsiniz.  

Diğer çoğaltma grupları başarıyla çoğaltılmaya devam edilirken, bir veya daha fazla çoğaltma grubu çoğaltılamaz. Bağlantının çoğaltma durumunu, ilk olarak düşürülmüş olarak rapor edildiğinde gözden geçirmeyi planlayın.

Aşağıdaki durumlarda bağlantının düşürülmüş veya başarısız durumu için yeniden deneme değerlerini değiştirmeyi göz önünde bulundurun:

- Belirli çoğaltma grupları için yinelenen gecikmeler var ve bu gecikme bir sorun değil

- Siteler arasındaki ağ bağlantısının kullanılabilir bant genişliği düşük

Site bağlantının düşürülmüş veya başarısız olarak ayarlanmadan önce yeniden deneme sayısını arttırdığınızda, bilinen sorunlar için yanlış uyarıları ortadan kaldırabilirsiniz. Bu eylem bağlantının durumunu daha doğru bir şekilde izlemenize olanak sağlar.  

Bu grubun ne sıklıkta çoğaltılmasını anlamak için, her bir çoğaltma grubu için çoğaltma eşitleme aralığını göz önünde bulundurun. Çoğaltma gruplarının **eşitleme aralığını** görüntülemek için Configuration Manager konsolundaki **izleme** çalışma alanına gidin. **Veritabanı çoğaltması** düğümünde bir çoğaltma bağlantısının **çoğaltma ayrıntısı** sekmesini seçin.  

Çoğaltma durumunun nasıl görüntüleneceği dahil olmak üzere veritabanı çoğaltmasının nasıl izleneceği hakkında daha fazla bilgi için bkz. [veritabanı çoğaltmasını izleme](../../servers/manage/monitor-replication.md).  


## <a name="site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> Site veritabanı çoğaltması denetimleri  

Veritabanı çoğaltması için kullanılan ağ bant genişliğini denetlemenize yardımcı olması için, her site veritabanı için ayarları değiştirin. Ayarlar yalnızca ayarları yapılandırdığınız site veritabanı için geçerlidir. Bu ayarlar her zaman site herhangi bir veriyi veritabanı çoğaltması tarafından başka bir siteye çoğalttığında kullanılır.  

Her site veritabanı için aşağıdaki çoğaltma denetimlerini değiştirebilirsiniz:  

- SSB bağlantı noktası  

- Çoğaltma hatalarından önce, site veritabanının kopyasını yeniden başlatmak için beklenecek süre  

- Bir sitenin çoğaltılacağını verileri sıkıştırın. Yalnızca siteler arasında aktarım için verileri sıkıştırır, her iki sitede de site veritabanında depolama için değildir.  

Bir site veritabanının çoğaltma denetimlerinin ayarlarını değiştirmek için, **veritabanı çoğaltma** düğümündeki Configuration Manager konsolunda, site veritabanının özelliklerini düzenleyin. Bu düğüm, **Yönetim** çalışma alanındaki **Hiyerarşi Yapılandırması** düğümünün altında görüntülenir ve **izleme** çalışma alanında da görünür. Site veritabanının özelliklerini düzenlemek için siteler arasındaki çoğaltma bağlantısını seçin ve ardından **üst veritabanı özellikleri** ' ni ya da **alt veritabanı özellikleri**' ni açın.  

> [!TIP]  
> Her iki çalışma alanında **Veritabanı Çoğaltması** düğümünden veritabanı çoğaltması denetimlerini yapılandırabilirsiniz. Ancak, **izleme** çalışma alanındaki **veritabanı çoğaltması** düğümünü kullandığınızda, çoğaltma bağlantısı için veritabanı çoğaltmasının durumunu da görüntüleyebilir ve çoğaltmayla ilgili sorunları araştırmanıza yardımcı olması için çoğaltma bağlantısı Çözümleyicisi aracına erişebilirsiniz.  


## <a name="see-also"></a>Ayrıca bkz.

[Çoğaltmayı izleme](../../servers/manage/monitor-replication.md)

[SQL çoğaltma sorunlarını giderme](../../servers/manage/replication/overview.md)
