---
title: Technical Preview 1612 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1612 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9cd0df25c64c4ca1e0d2ce98de5d2915f7564241
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693038"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Configuration Manager için Technical Preview 1612 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*



Bu makalede, sürüm 1612 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="the-data-warehouse-service-point"></a>Veri ambarı hizmet noktası
Technical Preview sürüm 1612 ' den başlayarak, veri ambarı hizmet noktası, Configuration Manager dağıtımınız için uzun süreli geçmiş verileri depolamanıza ve rapor etmenize olanak sağlar. Bu, Configuration Manager site veritabanından bir veri ambarı veritabanına otomatik eşitlemeler tarafından gerçekleştirilir. Bu bilgilere daha sonra Raporlama Hizmetleri noktanınızdan erişilebilir.

Varsayılan olarak, yeni site sistem rolünü yüklediğinizde Configuration Manager, sizin belirttiğiniz bir SQL Server örneğinde veri ambarı veritabanını oluşturur. Veri ambarı, değişiklik izleme zaman damgalarına sahip 2 TB 'a kadar veriyi destekler.  Varsayılan olarak, site veritabanından eşitlenen veriler, genel veriler, site verileri, Global_Proxy, bulut verileri ve veritabanı görünümleri için veri gruplarını içerir. Ayrıca, daha fazla tablo eklemek için eşitlenecek öğeleri değiştirebilir veya belirli tabloları varsayılan çoğaltma kümelerinden hariç tutun.
Eşitlenen varsayılan veriler aşağıdakiler hakkında bilgiler içerir:
- Altyapı durumu
- Güvenlik
- Uyumluluk
- Kötü Amaçlı Yazılımlar   
- Yazılım dağıtımları
- Stok ayrıntıları (ancak, envanter geçmişi eşitlenmemiş)

Veri ambarı veritabanını yüklemeye ve yapılandırmaya ek olarak, bu verileri kolayca arayabilmeniz ve rapor edebilmeniz için birkaç yeni rapor yüklenir.

### <a name="data-warehouse-dataflow"></a>Veri ambarı veri akışı   
![Datawarehouse_flow](./media/datawarehouse.png)

| Adım         | Ayrıntılar  |
|:------:|-----------|  
| **1** | Site sunucusu, verileri site veritabanına aktarır ve depolar.  |  
| **2** | Veri ambarı hizmet noktası, zamanlama ve yapılandırmaya bağlı olarak site veritabanından veri alır.  |  
| **3** | Veri ambarı hizmet noktası, eşitlenen verilerin bir kopyasını veri ambarı veritabanına aktarır ve depolar. |  
| **A** | Yerleşik raporları kullanarak, Raporlama Hizmetleri noktasına SQL Server Reporting Services kullanarak geçirilen bir veri isteği yapılır. |  
| **B** | Çoğu rapor güncel bilgiler içindir ve bu istekler site veritabanına karşı çalıştırılır. |  
| **,** | Bir rapor geçmiş verileri istediğinde **veri ambarı** *kategorisi* içeren raporlardan birini kullanarak, istek veri ambarı veritabanına karşı çalıştırılır.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Veri ambarı hizmet noktası ve veritabanı önkoşulları
- Hiyerarşinizde bir raporlama hizmetleri noktası site sistem rolü yüklü olmalıdır.
- Site sistemi rolünü yüklediğiniz bilgisayar .NET Framework 4.5.2 veya üstünü gerektirir.
- Site sistemi rolünü yüklediğiniz bilgisayarın bilgisayar hesabı, veri ambarı veritabanını barındıracak olan bilgisayarda yerel yönetici izinlerine sahip olmalıdır.
- Site sistemi rolünü yüklemek için kullandığınız yönetim hesabı, veri ambarı veritabanını barındıracak SQL Server örneğinde DBO olmalıdır.  
- Veritabanı destekleniyor:
  - SQL Server 2012 veya üzeri, Enterprise veya Datacenter Edition.
  - Varsayılan veya adlandırılmış bir örnekte
  - *SQL Server kümesinde*. Bu yapılandırmanın çalışması gerektiği halde test edilmemiştir ve destek en iyi çabadır.
  - Site veritabanı veya Raporlama Hizmetleri noktası veritabanıyla birlikte bulunur. Ancak, bunun ayrı bir sunucuya yüklenmesini öneririz.  
- *Raporlama Hizmetleri noktası hesabı* olarak kullanılan hesap, veri ambarı veritabanı için **db_datareader** iznine sahip olmalıdır.  
- Veritabanı, *SQL Server bir AlwaysOn kullanılabilirlik grubunda*desteklenmez.

### <a name="install-the-data-warehouse"></a>Veri ambarını yükler
**Site sistemi rolleri ekleme Sihirbazı 'nı** veya **site sistemi sunucusu oluşturma Sihirbazı 'nı**kullanarak bir merkezi yönetim sitesine veya birincil siteye veri ambarı site sistemi rolünü yüklersiniz. Daha fazla bilgi için bkz. [site sistemi rollerini yüklemeyi](../servers/deploy/configure/install-site-system-roles.md) . Bir hiyerarşi bu rolün birden çok örneğini destekler, ancak her sitede yalnızca bir örnek desteklenir.  

Rolü yüklediğinizde Configuration Manager, belirttiğiniz SQL Server örneğinde sizin için veri ambarı veritabanını oluşturur. Varolan bir veritabanının adını belirtirseniz ( [veri ambarı veritabanını yeni bir SQL Server taşırsanız](#move-the-data-warehouse-database)yaptığınız gibi), Configuration Manager yeni bir veritabanı oluşturmaz, bunun yerine belirttiğiniz birini kullanır.

#### <a name="configurations-used-during-installation"></a>Yükleme sırasında kullanılan yapılandırma
Site sistemi rolünü yüklemeyi tamamladıktan sonra aşağıdaki bilgileri kullanın:

**Sistem rolü seçim** sayfası:  
Sihirbaz, veri ambarı hizmet noktasını seçip yüklemeye yönelik bir seçenek görüntülemeden önce bir raporlama hizmetleri noktası yüklemiş olmanız gerekir.

**Genel** sayfa: aşağıdaki genel bilgiler gereklidir:
- **Configuration Manager veritabanı ayarları:**   
  - **Sunucu adı** -site veritabanını BARıNDıRAN sunucunun FQDN 'sini belirtin. SQL Server varsayılan bir örneğini kullanmıyorsanız, aşağıdaki biçimde FQDN 'den sonra örneği belirtmeniz gerekir: *** &lt; Sqlserver_FQDN>\& lt; Instance_name>***
  - **Veritabanı adı** -site veritabanının adını belirtin.
  - **Doğrula** -site veritabanına olan bağlantının başarılı olduğundan emin olmak için **Doğrula** ' ya tıklayın.
</br></br>
- **Veri ambarı veritabanı ayarları:**
  - **Sunucu adı** -veri ambarı hizmet noktasını ve veritabanını BARıNDıRAN sunucunun FQDN 'sini belirtin. SQL Server varsayılan bir örneğini kullanmıyorsanız, aşağıdaki biçimde FQDN 'den sonra örneği belirtmeniz gerekir: *** &lt; Sqlserver_FQDN>\& lt; Instance_name>***
  - **Veritabanı adı** -veri ambarı VERITABANı için FQDN 'yi belirtin.  Configuration Manager, bu adı taşıyan veritabanını oluşturacak. SQL Server örneğinde zaten var olan bir veritabanı adı belirtirseniz, Configuration Manager Bu veritabanını kullanacaktır.
  - **Doğrula** -site veritabanına olan bağlantının başarılı olduğundan emin olmak için **Doğrula** ' ya tıklayın.

**Eşitleme ayarları** sayfası:   
- **Veri ayarları:**
  - **Eşitlemeye yönelik çoğaltma grupları** – eşitlenmesini istediğiniz veri gruplarını seçin. Farklı türlerdeki veri grupları hakkında daha fazla bilgi için bkz. [siteler arasındaki veri aktarımları](../plan-design/hierarchy/data-transfers-between-sites.md)içindeki [veritabanı çoğaltması](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) ve **Dağıtılmış görünümler** .
  - **Eşitlemeye eklenen tablolar** – eşitlenmesini istediğiniz her ek tablonun adını belirtin. Birden çok tabloyu virgül kullanarak ayırın. Bu tablolar, seçtiğiniz çoğaltma gruplarına ek olarak site veritabanından eşitlenir.
  - **Eşitlemeye dışlanan tablolar** -her bir tablo adını eşitlediğiniz çoğaltma gruplarından belirleyin. Belirttiğiniz tabloların dışında tutulacak. Birden çok tabloyu virgül kullanarak ayırın.
- **Eşitleme ayarları:**
  - **Eşitleme aralığı (dakika)** -dakika cinsinden bir değer belirtin. Aralığa ulaşıldığında, yeni bir eşitleme başlatılır. Bu, 60 ile 1440 dakika (24 saat) arasında bir Aralık destekler.
  - **Zamanlama** -eşitlemenin çalışmasını istediğiniz günleri belirtin.

**Raporlama noktası erişimi**:   
Veri ambarı rolü yüklendikten sonra, *Raporlama Hizmetleri noktası hesabı* olarak kullanılan hesabın veri ambarı veritabanı için **db_datareader** iznine sahip olduğundan emin olun.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Yükleme ve veri eşitleme sorunlarını giderme
Veri ambarı hizmet noktası yüklemesiyle ilgili sorunları araştırmak veya verilerin eşitlenmesi için aşağıdaki günlükleri kullanın:
- **Dwssmsı. log** ve **dwsssetup. log**  -veri ambarı hizmet noktasını yüklerken hataları araştırmak için bu günlükleri kullanın.
- ** MgrDataWarehouse. logMicrosoft.Config** – bu günlüğü, site veritabanı arasındaki veri ambarı veritabanına veri eşitlemesini araştırmak için kullanın.

### <a name="reporting"></a>Raporlama
Bir veri ambarı site sistem rolünü yükledikten sonra, Raporlama Hizmetleri noktanınızda bir **veri ambarı** *kategorisi* ile aşağıdaki raporlar mevcuttur:

|Rapor                   | Ayrıntılar                                  |
|-------------------------|------------------------------------------|
| **Uygulama dağıtım raporu** | Belirli bir uygulama ve makine için uygulama dağıtımına ilişkin ayrıntıları görüntüleyin.|
| **Endpoint Protection ve Yazılım Güncelleştirme Uyumluluğu raporu**   | Eksik yazılım güncelleştirmeleri olan bilgisayarları görüntüleyin.|
| **Genel donanım envanteri raporu**  | Belirli bir makine için tüm donanım envanterini görüntüleyin.|
| **Genel Yazılım envanteri raporu**  | Belirli bir makine için tüm yazılım envanterini görüntüleyin.|
| **Altyapı sistem durumuna genel bakış**  |Configuration Manager altyapınızın sistem durumuna genel bir bakış görüntüler.|
| **Algılanan kötü amaçlı yazılım listesi**  |Kuruluşta algılanan kötü amaçlı yazılımları görüntüleyin.|
| **Yazılım dağıtımı özet raporu** | Belirli bir tanıtım ve makine için yazılım dağıtımının Özeti.|

### <a name="move-the-data-warehouse-database"></a>Veri ambarı veritabanını taşıma
Veri ambarı veritabanını yeni bir SQL Server taşımak için aşağıdaki adımları kullanın:

1. Geçerli veritabanı yapılandırmasını gözden geçirin ve aşağıdakiler dahil olmak üzere yapılandırma ayrıntılarını kaydedin:  
   - Eşitlediğiniz veri grupları
   - Eşitlemeye dahil ettiğiniz veya hariç çıkardığınız tablolar       

   Veritabanını yeni bir sunucuya geri yükledikten sonra ve site sistem rolünü yeniden yükledikten sonra bu veri gruplarını ve tabloları yeniden yapılandıracaksınız.  

2. Veri ambarı veritabanını yedeklemek için SQL Server Management Studio kullanın ve ardından bu veritabanını veri ambarını barındıracak yeni bilgisayardaki bir SQL Server 'a geri yüklemek için yeniden yükleyin.

   Veritabanını yeni sunucuya geri yükledikten sonra, veritabanı erişim izinlerinin özgün veri ambarı veritabanında olduğu gibi yeni veri ambarı veritabanında aynı olduğundan emin olun.

3. Veri ambarı hizmet noktası site sistemi rolünü geçerli sunucudan kaldırmak için Configuration Manager konsolunu kullanın.

4. Yeni bir veri ambarı hizmet noktası yükleme ve geri yüklediğiniz veri ambarı veritabanını barındıran yeni SQL Server ve örneğin adını belirtin.

5. Site sistemi rolü yüklendikten sonra taşıma işlemi tamamlanır.

Site sistem rolünün başarıyla yeniden yüklendiğini onaylamak için aşağıdaki Configuration Manager günlüklerini gözden geçirebilirsiniz:  
- **Dwssmsı. log** ve **dwsssetup. log**  -veri ambarı hizmet noktasını yüklerken hataları araştırmak için bu günlükleri kullanın.
- ** MgrDataWarehouse. logMicrosoft.Config** – bu günlüğü, site veritabanı arasındaki veri ambarı veritabanına veri eşitlemesini araştırmak için kullanın.


## <a name="content-library-cleanup-tool"></a>İçerik kitaplığı Temizleme Aracı
Technical Preview sürüm 1612 ' den başlayarak, bir dağıtım noktasından (yalnız bırakılmış içerik) herhangi bir paket veya uygulamayla ilişkili olmayan içeriği kaldırmak için yeni bir komut satırı aracı (**ContentLibraryCleanup.exe**) kullanabilirsiniz. Bu araç, içerik kitaplığı temizleme aracı olarak adlandırılır.

Bu araç yalnızca, aracı çalıştırdığınızda belirttiğiniz dağıtım noktasındaki içeriği etkiler ve site sunucusundaki içerik kitaplığından içerik kaldıramaz.

Technical Preview 1612 ' i yükledikten sonra, **ContentLibraryCleanup.exe** \* Technical Preview site sunucusundaki *% CM_Installation_Path% \ CD. latest\SMSSETUP\TOOLS\ContentLibraryCleanup klasöründeContentLibraryCleanup.exebulabilirsiniz.

Bu teknik önizleme ile yayınlanan araç, geçmiş Configuration Manager ürünleri için sunulan benzer araçların eski sürümlerini değiştirmek üzere tasarlanmıştır. Bu araç sürümü 1 Mart 2017 ' den sonra işlevi durdursa da, bu araç Güncel Dalı bir parçası olarak yayınlanana veya bir üretime hazır bant dışı yayın sürümü olarak yayınlanana kadar, gelecekteki teknik önizlemelerle yeni sürümler yayımlanacak.

### <a name="requirements"></a>Gereksinimler  
- Araç, dağıtım noktasını barındıran bilgisayarda doğrudan veya başka bir sunucudan uzaktan çalıştırılabilir. Araç aynı anda yalnızca tek bir dağıtım noktası için çalıştırılabilir.
- Aracı çalıştıran kullanıcı hesabı, Configuration Manager hiyerarşisinde tam yöneticiye eşit olan rol tabanlı yönetim izinlerine doğrudan sahip olmalıdır.  Kullanıcı hesabına, tam yönetici izinlerine sahip bir Windows güvenlik grubunun üyesi olarak izin verildiğinde araç çalışmaz.

### <a name="modes-of-operation"></a>İşlem modları
Araç iki modda çalıştırılabilir:
1. **Durum modu**:   
   **/Delete** anahtarını belirtmezseniz, araç, durum modu ' nda çalışır ve dağıtım noktasından silinecek içeriği tanımlar, ancak gerçekten verileri silmez.

   - Araç bu modda çalıştığında, silinecek içerikle ilgili bilgiler otomatik olarak araçlar günlük dosyasına yazılır. Kullanıcının olası her silme işlemini onaylamasını istenmez.
   - Varsayılan olarak, günlük dosyası aracı çalıştırdığınız bilgisayardaki Users Temp klasörüne yazılır, ancak günlük dosyasını başka bir konuma yönlendirmek için/log anahtarını kullanabilirsiniz.  
   </br>

   Aracı/Delete anahtarıyla çalıştırmadan önce aracı bu modda çalıştırmanızı ve elde edilen günlük dosyasını incelemenizi öneririz.  

2. **Silme modu**: aracı **/Delete** anahtarıyla çalıştırıldığında, araç silme modunda çalışır.

   - Araç bu modda çalıştığında, belirtilen dağıtım noktasında bulunan yalnız bırakılmış içerikler dağıtım noktasının içerik kitaplığından silinebilir.
   -  Her bir dosyayı silmeden önce, kullanıcıdan dosyanın silinmesi gerektiğini onaylamasını istenir.  Daha fazla komut istemini atlamak ve yalnız bırakılmış tüm içeriği silmek için **Evet,** **Hayır, hayır** veya **Evet olarak tümünü** seçebilirsiniz.  
   </br>

   Aracı/Delete anahtarıyla çalıştırmadan önce aracı, durum modunda çalıştırmanızı ve elde edilen günlük dosyasını incelemenizi öneririz.  

İçerik kitaplığı Temizleme Aracı herhangi bir modda çalıştığında, otomatik olarak aracın çalıştığı modu, dağıtım noktası adını, tarihi ve işlem saatini içeren bir adı olan bir günlük oluşturur. Araç tamamlandığında günlük dosyası otomatik olarak açılır. Varsayılan olarak, bu günlük, aracı çalıştırdığınız bilgisayardaki Users **Temp** klasörüne yazılır. ancak, günlük dosyasını bir ağ paylaşımının dahil olduğu başka bir konuma yönlendirmek için bir komut satırı anahtarı kullanabilirsiniz.   


### <a name="run-the-tool"></a>Aracı çalıştırma
Aracı çalıştırmak için:
1. **ContentLibraryCleanup.exe**içeren bir klasöre bir yönetim komut istemi açın.  
2. Ardından, gerekli komut satırı anahtarlarını ve kullanmak istediğiniz isteğe bağlı anahtarları içeren bir komut satırı girin.

**Bilinen sorun** Araç çalıştırıldığında, herhangi bir paket veya dağıtım başarısız olduğunda veya devam ederken aşağıdakine benzer bir hata döndürülür:
-  *System. InvalidOperationException: paket tam olarak yüklenmediğinden bu içerik kitaplığı şu anda temizlenemez \<packageID> .*

**Geçici çözüm:** Yok. İçerik devam ederken veya dağıtımı başarısız olduğunda, araç yalnız bırakılmış dosyaları tanımlayamıyor. Bu nedenle, araç, bu sorun çözülene kadar içeriği temizleyemeyecektir.



### <a name="command-line-switches"></a>Komut satırı anahtarları  
Aşağıdaki komut satırı anahtarları herhangi bir sırada kullanılabilir.   

|Anahtar|Ayrıntılar|
|---------|-------|
|**/Delete**  |**İsteğe bağlı** </br> Dağıtım noktasından içerik silmek istediğinizde bu anahtarı kullanın. İçerik silinmeden önce sorulur. </br></br> Bu anahtar kullanılmazsa araç, hangi içeriğin silineceği hakkındaki sonuçları günlüğe kaydeder, ancak dağıtım noktasından herhangi bir içerik silmez. </br></br> Örnek: ***ContentLibraryCleanup.exe/dp server1.contoso.com/Delete*** |
| **anahtarın**       |**İsteğe bağlı** </br> Aracı tüm istemleri (içerik silinirken istemler gibi) ve günlük dosyasını otomatik olarak açmayın sessiz modda çalıştırın. </br></br> Örnek: ***ContentLibraryCleanup.exe/q/dp server1.contoso.com*** |
| **/DP &lt; dağıtım noktası FQDN>**  | **Gerekli** </br> Temizlemek istediğiniz dağıtım noktasının tam etki alanı adını (FQDN) belirtin. </br></br> Örnek:  ***ContentLibraryCleanup.exe/dp server1.contoso.com***|
| **/PS &lt; birincil SITE FQDN 'si>**       | Birincil sitedeki bir dağıtım noktasından içerik temizlenirken **Isteğe bağlıdır** .</br>İkincil sitedeki bir dağıtım noktasından içerik temizlenirken **gereklidir** . </br></br> Dağıtım noktasının ikincil bir sitede olması durumunda, dağıtım noktasının ait olduğu birincil sitenin FQDN 'sini veya üst birincil üst öğeyi belirtin. </br></br> Örnek: ***ContentLibraryCleanup.exe/dp server1.contoso.com/PS siteserver1.contoso.com*** |
| **/SC &lt; birincil site kodu>**  | Birincil sitedeki bir dağıtım noktasından içerik temizlenirken **Isteğe bağlıdır** .</br>İkincil sitedeki bir dağıtım noktasından içerik temizlenirken **gereklidir** . </br></br> Dağıtım noktasının ikincil bir sitede olması durumunda, dağıtım noktasının ait olduğu birincil sitenin veya üst birincil sitenin site kodunu belirtin.</br></br> Örnek: ***ContentLibraryCleanup.exe/dp server1.contoso.com/SC ABC*** |
| **/log \<log file directory>**       |**İsteğe bağlı** </br> Günlük dosyalarını yerleştirmek için bir dizin belirtin. Bu, yerel bir sürücü veya bir ağ paylaşımında olabilir.</br></br> Bu anahtar kullanılmazsa, günlük dosyaları otomatik olarak kullanıcılar geçici klasörüne yerleştirilir.</br></br> Yerel sürücü örneği: ***ContentLibraryCleanup.exe/dp server1.contoso.com/log C:\users\\administrators \ Desktop*** </br></br>Ağ paylaşımının örneği: ***ContentLibraryCleanup.exe/dp server1.contoso.com/log \\ &lt; Share>\& lt; klasör>***|


## <a name="improvements-for-in-console-search"></a>Konsol içi aramada iyileştirmeler
Kullanıcı sesli geri bildirimlerine göre, konsol içi aramaya aşağıdaki geliştirmeleri ekledik:
- **Nesne yolu:**  
  Birçok nesne artık **nesne yolu**adlı yeni bir sütunu destekliyor.  Bu sütunu arama ve görüntüleme sonuçlarınıza dahil ettiğinizde her nesnenin yolunu görüntüleyebilirsiniz. Örneğin, Uygulamalar düğümünde uygulamalar için bir arama çalıştırırsanız ve ayrıca alt düğümleri arıyorsanız, sonuçlar bölmesindeki *nesne yolu* sütunu döndürülen her nesnenin yolunu gösterir.   

- **Arama metninin korunması:**  
  Arama metin kutusuna metin girdiğinizde ve sonra bir alt düğüm ve geçerli düğüm arama arasında geçiş yaptığınızda, yazdığınız metin artık devam eder ve yeniden yazmak zorunda kalmadan yeni bir arama için kullanılabilir kalır.

- **Alt düğümleri arama kararının korunması:**  
  *Geçerli düğümü* veya *tüm alt düğümleri* aramak için belirlediğiniz seçenek, artık üzerinde çalıştığınız düğümü değiştirdiğinizde devam ediyor.   Bu yeni davranış, konsolda hareket eden kararı sürekli olarak sıfırlamanız gerekmediği anlamına gelir.  Varsayılan olarak, konsolunu açtığınızda bu seçenek yalnızca geçerli düğümde arama yapmak için kullanılır.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Belirtilen program çalışıyorsa uygulamanın yüklenmesini engelleyin.
Artık, çalışıyorsa, bir uygulamanın yüklenmesini engelleyebileceği dağıtım türü özelliklerinde çalıştırılabilir dosyaların bir listesini yapılandırabilirsiniz. Yükleme denendikten sonra, kullanıcılar tarafından yüklemeyi engelleyen işlemlerin kapatılmasını isteyen bir iletişim kutusu görüntülenir.

### <a name="try-it-out"></a>Deneyin
Yürütülebilir dosyaların bir listesini yapılandırmak için
1. Herhangi bir dağıtım türünün Özellikler sayfasında, **Yükleyici işleme** sekmesini seçin.
2. Listeye daha fazla yürütülebilir dosyadan birini eklemek için **Ekle**' ye tıklayın (örneğin **Edge.exe**)
3. Dağıtım türü Özellikler iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.

Artık, bu uygulamayı bir kullanıcıya veya cihaza dağıttığınızda ve eklediğiniz yürütülebilir dosyalardan biri çalışıyorsa, Son Kullanıcı bir uygulama çalıştığı için yüklemenin başarısız olduğunu belirten bir yazılım merkezi iletişim kutusu görür.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Son kullanıcılar için yeni Iş için Windows Hello bildirimi

Yeni bir Windows 10 bildirimi, son kullanıcılara Iş için Windows Hello kurulumunu tamamlamaya yönelik ek eylemler gerçekleştirmeleri gerektiğini bildirir (örneğin, bir PIN ayarlama).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Configuration Manager 'de Iş için Windows Mağazası desteği

Artık çevrimiçi lisanslı uygulamaları, Iş için Windows **Mağazası 'ndan Configuration Manager** Istemcisini çalıştıran bilgisayarlara dağıtabilirsiniz.
Daha ayrıntılı bilgi için bkz. [iş Için Windows Mağazası 'ndan uygulamaları Configuration Manager yönetme](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

Bu özellik için destek şu anda yalnızca Windows 10 RS2 Preview derlemesini çalıştıran bilgisayarlarda kullanılabilir.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Bir görev dizisi başarısız olduğunda önceki sayfaya dön
Artık bir görev dizisini çalıştırdığınızda ve bir hata olduğunda önceki sayfaya geri dönebilirsiniz. Bu sürümden önce, bir hata oluştuğunda görev sırasını yeniden başlatmanız gerekiyordu. Örneğin, **önceki** düğmeyi aşağıdaki senaryolarda kullanabilirsiniz:

- Bir bilgisayar Windows PE 'de başlatıldığında, görev dizisi önyükleme iletişim kutusu görev dizisi kullanılabilir olmadan önce görüntülenebilir. Bu senaryoda Ileri ' ye tıkladığınızda, görev dizisinin son sayfası, kullanılabilir görev dizileri olmadığını belirten bir iletiyle birlikte görüntülenir. Şimdi, kullanılabilir görev dizileri için yeniden aramak üzere **geri** ' ye tıklayabilirsiniz. Görev dizisi kullanılabilir olana kadar bu işlemi yineleyebilirsiniz.
- Bir görev dizisini çalıştırdığınızda, ancak bağımlı içerik paketleri dağıtım noktalarında henüz yoksa, görev sırası başarısız olur. Artık eksik içeriği dağıtabilir (henüz dağıtılmamışsa) veya içeriğin dağıtım noktalarında kullanılabilir olmasını bekleyebilir ve ardından görev dizisinin içerik için tekrar aramasını sağlamak üzere **önceki** ' ye tıklayın.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Windows 10 güncelleştirmeleri için hızlı yükleme dosyaları desteği
Windows 10 güncelleştirmeleri için Configuration Manager için hızlı yükleme dosyaları desteği ekledik. Windows 10 ' un desteklenen bir sürümünü kullandığınızda, artık yalnızca geçerli ayın Windows 10 toplu güncelleştirmesi ve önceki ayın güncelleştirmesi arasındaki Delta indirmek için Configuration Manager ayarlarını kullanabilirsiniz. Şu anda Configuration Manager Güncel Dalı, tüm Windows 10 toplu güncelleştirmesi (önceki aydan tüm güncelleştirmeler dahil) her ay indirilir. Hızlı yükleme dosyalarının kullanılması, istemcilerde daha küçük indirmeler ve daha hızlı yükleme süreleri sağlar.

> [!IMPORTANT]
> Hızlı yükleme dosyalarının kullanımını desteklemeye yönelik ayarlar Configuration Manager ' de kullanıma sunulurken, bu işlevsellik yalnızca 10 Ocak 2017 ' de yayınlanan güncelleştirmelere (Salı Düzeltme Eki) eklenen Windows Update aracı güncelleştirmesiyle birlikte Windows 10 sürüm 1607 ' de desteklenir. Bu güncelleştirmeler hakkında daha fazla bilgi için bkz. [Destek makalesi 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Sonraki güncelleştirme kümesi 14 Şubat 2017 ' de yayınlanıyorsa hızlı yükleme dosyalarından yararlanabilirsiniz. Güncelleştirme ve önceki sürümler olmadan Windows 10 sürüm 1607, hızlı yükleme dosyalarını desteklemez.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Sunucuda Windows 10 güncelleştirmeleri için hızlı yükleme dosyalarının indirilmesini etkinleştirmek için
Windows 10 Express yükleme dosyaları için meta verileri eşitlemeye başlamak üzere, yazılım güncelleştirme noktası özelliklerinde etkinleştirmelisiniz.
1. Configuration Manager konsolunda, **Yönetim**  >  **Site yapılandırması**  >  **siteler**' e gidin.
2. Merkezi yönetim sitesini veya tek başına birincil siteyi seçin.
3. **Giriş** sekmesindeki **Ayarlar** grubunda **Site Bileşenlerini Yapılandır**’a, ardından da **Yazılım Güncelleştirme Noktası**’na tıklayın. **Güncelleştirme dosyaları** sekmesinde, **Windows 10 için tüm onaylanan güncelleştirmeler ve hızlı yükleme dosyaları Için tam dosyaları indir**' i seçin.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>İstemcilerin hızlı yükleme dosyalarını indirmesi ve yüklemesi için desteği etkinleştirmek üzere
İstemcilerde hızlı yükleme dosyaları desteğini etkinleştirmek için istemci ayarlarının yazılım güncelleştirmeleri bölümünde istemcilerde hızlı yükleme dosyalarını etkinleştirmeniz gerekir. Bu, belirttiğiniz bağlantı noktasına hızlı yükleme dosyalarını indirme isteklerinin dinlediği yeni bir HTTP dinleyicisi oluşturur. İstemci ayarlarını, istemcide bu işlevselliği etkinleştirmek üzere dağıttıktan sonra, geçerli ayın Windows 10 toplu güncelleştirmesi ile önceki ayın güncelleştirmesi arasındaki Delta 'yı indirmeye çalışır (istemciler, Express yükleme dosyalarını destekleyen bir Windows 10 sürümü çalıştırmalıdır).
1. Yazılım güncelleştirme noktası bileşen özelliklerindeki hızlı yükleme dosyaları desteğini etkinleştirin (önceki yordam).
2. Configuration Manager konsolunda **Yönetim**  >  **istemci ayarları**' na gidin.
3. Uygun istemci ayarlarını seçin, sonra **giriş** sekmesinde **Özellikler**' e tıklayın.
4. **Yazılım güncelleştirmeleri** sayfasını seçin, **istemcilerde hızlı güncelleştirmeleri yüklemeyi etkinleştir** **ayarını yapılandırın ve** **Hızlı güncelleştirmeler için içerik ındırmek için kullanılan bağlantı noktası** için istemcideki http dinleyicisi tarafından kullanılan bağlantı noktasını yapılandırın.


## <a name="odata-endpoint-data-access"></a>OData uç noktası veri erişimi

 Configuration Manager artık Configuration Manager verilere erişmek için bir daha fazla OData uç noktası sağlar. Uç nokta, Excel ve Power BI gibi araçların tek bir uç nokta aracılığıyla Configuration Manager verilere kolayca erişmesini sağlayan OData sürüm 4 ile uyumludur. Technical Preview 1612 yalnızca Configuration Manager içindeki nesnelere okuma erişimini destekler.  

[CONFIGURATION Manager WMI sağlayıcısında](../../develop/reference/configuration-manager-reference.md) Şu anda kullanılabilir olan veriler artık yeni OData yeniden uç noktası ile de erişilebilir. OData uç noktası tarafından açığa çıkarılan varlık kümeleri, WMI sağlayıcısıyla sorgulayabilmeniz için aynı verileri listeletmanızı sağlar.

### <a name="try-it-out"></a>Deneyin

OData uç noktasını kullanabilmeniz için, bunu site için etkinleştirmeniz gerekir.

1.  **Yönetim**  >  **sitesi yapılandırma**  >  **siteleri**' ne gidin.
2.  Birincil siteyi seçin ve **Özellikler**' e tıklayın.
3.  Birincil site özellikleri sayfasının Genel sekmesinde, **Bu sitedeki tüm sağlayıcılar IÇIN REST uç noktasını etkinleştir**' e tıklayın ve ardından **Tamam**' a tıklayın.

En sevdiğiniz OData sorgu görüntüleyiciniz içinde, Configuration Manager çeşitli nesneleri döndürmek için aşağıdaki örneklere benzer sorguları deneyin:

| Amaç | OData sorgusu |
|---|---|
| Tüm koleksiyonları al | `http://localhost/CMRestProvider/Collection` |
| Koleksiyon al | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Koleksiyondaki ilk 100 cihazı al | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Koleksiyonda kaynak KIMLIĞI olan bir cihaz alın | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Koleksiyondaki cihazın işletim sistemini al | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Koleksiyondaki kullanıcıları al | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> Tabloda gösterilen örnek sorgular, URL 'de konak adı olarak *localhost* KULLANıR ve SMS sağlayıcısı 'nı çalıştıran bilgisayarda kullanılabilir. Sorgularınızı farklı bir bilgisayardan çalıştırıyorsanız, localhost değerini, SMS sağlayıcısı yüklü olan sunucu FQDN 'siyle değiştirin.

## <a name="azure-active-directory-onboarding"></a>Azure Active Directory ekleme

Azure Active Directory (AD) ekleme, diğer bulut Hizmetleri tarafından kullanılacak Configuration Manager ve Azure Active Directory arasında bir bağlantı oluşturur. Bu, şu anda Bulut Yönetimi Ağ Geçidi için gereken bağlantıyı oluşturmak için kullanılabilir.

Azure yönetici kimlik bilgilerine ihtiyacınız olacağı için bu görevi bir Azure Yöneticisi ile gerçekleştirin.

#### <a name="to-create-the-connection"></a>Bağlantıyı oluşturmak için:

2. **Yönetim** çalışma alanında, **Cloud Services**  >  **Azure Active Directory**  >  **Azure Active Directory Ekle**' yi seçin.
2. Azure AD ile bağlantı oluşturmak için **oturum aç '** ı seçin.

#### <a name="configuration-manager-client-requirements"></a>Configuration Manager istemci gereksinimleri

Bulut Yönetimi Ağ Geçidi Kullanıcı ilkesi oluşturulmasını etkinleştirmeye yönelik çeşitli gereksinimler vardır.

- Azure AD ekleme işlemi tamamlanmış olmalıdır ve bağlantı bilgilerini almak için istemcinin başlangıçta kurumsal ağa bağlanması gerekir.
- İstemcilerin hem etki alanına katılmış (Active Directory kayıtlı) hem de bulut etki alanına katılmış olması (Azure AD 'de kayıtlı) olması gerekir.
- [Kullanıcı keşfi Active Directory](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)çalıştırmanız gerekir.
- Configuration Manager istemcisini Internet üzerinden Kullanıcı ilkesi isteklerine izin verecek şekilde değiştirmeniz ve değişikliği istemciye dağıtmanız gerekir. İstemci *cihazında*istemcinin bu değişikliği gerçekleştiğinden, Kullanıcı ilkesi için gereken yapılandırma değişikliklerini tamamlamadınız da bulut yönetimi ağ geçidi aracılığıyla dağıtılabilir.
- Yönetim noktanız, ağdaki belirtecin güvenliğini sağlamak için HTTPS kullanacak şekilde yapılandırılmış olmalıdır ve .NET 4,5 yüklü olmalıdır.

Bu yapılandırma değişikliklerini yaptıktan sonra, ilkeyi test etmek için bir Kullanıcı ilkesi oluşturabilir ve istemcileri Internet 'e taşıyabilirsiniz. Bulut Yönetimi Ağ Geçidi üzerinden Kullanıcı ilkesi isteklerinin kimliği, Azure AD belirteç tabanlı kimlik doğrulaması ile doğrulanır.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Cihaz kaydı için Multi-Factor Authentication 'ı yapılandırma değiştirme

Azure portal cihaz kaydı için Multi-Factor Authentication (MFA) ayarlayabilmeniz artık, MFA seçeneği Configuration Manager konsolundan kaldırılmıştır. [Bu Microsoft Intune konu başlığında](../../../intune/enrollment/multi-factor-authentication.md), kayıt için MFA ayarlama hakkında daha fazla bilgi bulabilirsiniz.