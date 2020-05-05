---
title: Gerçek zamanlı veriler için CMPivot
titleSuffix: Configuration Manager
description: Configuration Manager 'de CMPivot kullanarak istemcileri gerçek zamanlı olarak sorgulama hakkında bilgi edinin.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcd441c7f35748f42adc8824c68ec703291a13e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719144"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>Configuration Manager içindeki gerçek zamanlı veriler için CMPivot

<!--1358456-->

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, müşterilerin raporlama amacıyla kullanacağı, cihaz verilerinin büyük merkezi bir deposunu sağlamıştır. Site genellikle bu verileri haftalık olarak toplar. Sürüm 1806 ' den başlayarak, CMPivot artık ortamınızdaki cihazların gerçek zamanlı durumuna erişim sağlayan yeni bir konsol içi yardımcı programdır. Hedef koleksiyondaki Şu anda bağlı olan tüm cihazlarda bir sorguyu hemen çalıştırır ve sonuçları döndürür. Ardından bu verileri aracında filtreleyin ve gruplandırın. Çevrimiçi istemcilerden gerçek zamanlı veriler sunarak, iş sorularını daha hızlı bir şekilde yanıtlayabilir, sorun giderebilir ve güvenlik olaylarına yanıt verebilirsiniz.

Örneğin, [kurgusal yürütme tarafı kanalı güvenlik açıklarını azaltıcı](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)bir şekilde, gereksinimlerden biri sistem BIOS 'unu güncelleştirmelerdir. CMPivot kullanarak sistem BIOS bilgilerini hızlı bir şekilde sorgulayabilir ve uyumlu olmayan istemcileri bulabilirsiniz.

 > [!IMPORTANT]  
 > - Bazı güvenlik yazılımları c:\windows\ccm\scriptstorekonumundan çalıştırılan betikleri engelleyebilir. Bu, CMPivot sorgularının başarıyla yürütülmesini engelleyebilir. Bazı güvenlik yazılımları, CMPivot PowerShell çalıştırılırken denetim olayları ya da uyarılar oluşturabilir.
 > - Bazı kötü amaçlı yazılımdan koruma yazılımları yanlışlıkla Configuration Manager çalıştırmak betiklerine veya CMPivot özelliklerine karşı olayları tetikleyemeyebilir. Kötü amaçlı yazılımdan koruma yazılımının bu özelliklerin girişim olmadan çalışmasına izin vermesi için%windir%\CCM\ScriptStore hariç tutulması önerilir.


## <a name="prerequisites"></a>Önkoşullar

CMPivot kullanmak için aşağıdaki bileşenler gereklidir:

- Hedef cihazları Configuration Manager istemcisinin en son sürümüne yükseltin.  

- Hedef istemciler en az PowerShell sürüm 4 gerektirir.

- Aşağıdaki varlıklara veri toplamak için, hedef istemciler PowerShell sürüm 5,0 gerektirir:  
  - Yöneticiler
  - Bağlantı
  - Komutunu
  - SMBConfig


- CMPivot için izinler:
  - **SMS betikleri** nesnesinde **Oku** izni
  - **Koleksiyonda** **betikleri Çalıştır** izni
    - Alternatif olarak, sürüm 1906 ' den başlayarak, **CMPivot Run** on the **Collection**kullanabilirsiniz.
  - **Envanter raporlarında** **okuma** izni
  - Varsayılan kapsam.

>[!NOTE]
> **Çalıştırma betikleri** , **Run CMPivot** izninin bir süper kümesidir.
 
## <a name="limitations"></a>Sınırlamalar

- Hiyerarşide, CMPivot çalıştırmak için Configuration Manager konsolunu *birincil siteye* bağlayın. **Start CMPivot** eylemi, bir merkezi yönetim sıtesıne (CAS) bağlıyken konsolunda görüntülenmez.
  - Configuration Manager sürüm 1902 ' den başlayarak, bir CA 'dan CMPivot çalıştırabilirsiniz. Bazı ortamlarda ek izinler gerekir. Daha fazla bilgi için bkz. [sürüm 1902 ' den başlayarak CMPivot](#bkmk_cmpivot1902).

- CMPivot yalnızca geçerli siteye bağlı istemciler için verileri döndürür.  

- Bir koleksiyon başka bir siteden cihazlar içeriyorsa, CMPivot sonuçları yalnızca geçerli sitedeki cihazlardan alınır.  

- Varlık özelliklerini, sonuçlar için sütunları veya cihazlardaki eylemleri özelleştiremezsiniz.  

- Yalnızca bir CMPivot örneği, Configuration Manager konsolunu çalıştıran bir bilgisayarda aynı anda çalışabilir.  

- Sürüm 1806 ' de, **Yöneticiler** varlığına yönelik sorgu yalnızca Grup "Administrators" olarak adlandırılmışsa işe yarar. Grup adı yerelleştirildiği takdirde bu çalışmaz. Örneğin, Fransızca 'da "Yönettemi".<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>CMPivot Başlat

1. Configuration Manager konsolunda, birincil siteye bağlanın. **Varlıklar ve uyum** çalışma alanına gidin ve **Cihaz Koleksiyonları** düğümünü seçin. Bir hedef koleksiyon seçin ve aracı başlatmak için Şeritteki **CMPivot Başlat** ' a tıklayın.  

    > [!Tip]  
    > Bu seçeneği görmüyorsanız, aşağıdaki konfigürasyonları kontrol edin:  
    > 
    > - Hesabınızın gerekli izinlere sahip olduğunu bir site yöneticisiyle onaylayın. Daha fazla bilgi için bkz. [Önkoşullar](#prerequisites).  
    > 
    > - Konsolunu bir *birincil siteye*bağlayın.  

2. Arabirim, aracı kullanma hakkında daha fazla bilgi sağlar.  

     - Sorgu dizelerini en üste el ile girin veya çevrimiçi belgelerde bağlantıları tıklatın.  

     - Sorgu dizesine eklemek için **varlıklardan** birine tıklayın.  

     - **Tablo işleçleri**, **toplama Işlevleri**ve **skaler işlevler** bağlantıları, Web tarayıcısında dil başvurusu belgelerini açar. CMPivot, [kusto sorgu dilini (KQL)](https://docs.microsoft.com/azure/kusto/query/)kullanır.  

3. İstemcilerdeki sonuçları görüntülemek için CMPivot penceresini açık tutun. CMPivot penceresini kapattığınızda oturum tamamlanmıştır.  

    > [!Note]  
    > Sorgu gönderilmişse, istemciler hala sunucuya bir durum iletisi yanıtı gönderir.  



## <a name="how-to-use-cmpivot"></a>CMPivot kullanma

![CMPivot pencere örneği](media/1358456-cmpivot-sample.png)

CMPivot penceresi aşağıdaki öğeleri içerir:  

1. CMPivot Şu anda hedeflediği koleksiyon üstteki başlık çubuğunda ve pencerenin alt kısmındaki durum çubuğudur. Örneğin, yukarıdaki ekran görüntüsünde "PM_Team_Machines".  

2. Sol taraftaki bölmede, istemcilerde kullanılabilen **varlıklar** listelenir. Bazı varlıklar WMI 'yi kullanır, diğer bir deyişle, istemcileri istemcilerden veri almak için PowerShell kullanır.   

    - Aşağıdaki eylemler için bir varlığa sağ tıklayın:  

       - **Ekle**: varlığı, geçerli imleç konumundaki sorguya ekleyin. Sorgu otomatik olarak çalıştırılmaz. Bir varlığa çift tıkladığınızda bu eylem varsayılandır. Bir sorgu oluştururken bu eylemi kullanın.  

       - **Tümünü sorgula**: Bu varlık için tüm özellikler dahil bir sorgu çalıştırın. Tek bir varlığı hızlıca sorgulamak için bu eylemi kullanın.  

       - **Cihaza göre sorgula**: Bu varlık için bir sorgu çalıştırın ve sonuçları gruplandırın. Örneğin, `Disk | summarize dcount( Device ) by Name`  

    - Her varlık için kullanılabilen belirli özellikleri görmek için bir varlığı genişletin. Geçerli imleç konumundaki sorguya eklemek için bir özelliğe çift tıklayın.  

3. **Giriş** sekmesinde, örnek sorgular ve destekleyici belgelerin bağlantıları dahil olmak üzere CMPivot hakkındaki genel bilgiler gösterilmektedir.  

4. **Sorgu** sekmesi, sorgu bölmesini, sonuçlar bölmesini ve durum çubuğunu görüntüler. Yukarıdaki ekran görüntüsü örneğinde sorgu sekmesi seçilidir.  

5. Sorgu bölmesi, koleksiyondaki istemcilerde çalıştırmak için bir sorgu oluşturabileceğiniz veya yazdığınız yerdir.  

    - CMPivot, [kusto sorgu dilinin (KQL)](https://docs.microsoft.com/azure/kusto/query/)bir alt kümesini kullanır.  

    - Sorgu bölmesinde içeriği kesin, Kopyala veya Yapıştır.  
    <!-- markdownlint-disable MD038 -->
    - Varsayılan olarak, bu bölme IntelliSense kullanır. Örneğin, yazmaya `D`başladıysanız, IntelliSense Bu harfle başlayan tüm varlıkları önerir. Bir seçenek belirleyin ve eklemek için SEKME tuşuna basın. Bir kanal karakteri ve bir boşluk `| `yazıp IntelliSense tüm tablo işleçlerini önerir. Bir `summarize` boşluk ekleyin ve yazın ve IntelliSense tüm toplama işlevlerini önerir. Bu işleçler ve işlevler hakkında daha fazla bilgi için CMPivot içindeki **giriş** sekmesine tıklayın.  

    - Sorgu bölmesi aşağıdaki seçenekleri de sağlar:  

        - Sorguyu çalıştırın.  

        - Sorgu geçmişi listesinde geri ve ileri doğru taşı.  

        - Doğrudan üyelik koleksiyonu oluşturun.  

        - Sorgu sonuçlarını CSV 'ye veya panoya dışarı aktarın.  

6. Sonuçlar bölmesinde, etkin istemciler tarafından sorgu için döndürülen veriler görüntülenir.  

   - Kullanılabilir sütunlar, varlığa ve sorguya göre farklılık gösterir.  

   - Sonuçları bu özelliğe göre sıralamak için bir sütun adına tıklayın.  

   - Sonuçları ilgili sütunda aynı bilgilere göre gruplandırmak için herhangi bir sütun adına sağ tıklayın veya sonuçları sıralayın.  

   - Cihazda aşağıdaki ek eylemleri gerçekleştirmek için bir cihaz adına sağ tıklayın:  

      - **Pivot**: Bu cihazdaki başka bir varlık için sorgu.  

      - **Betiği Çalıştır**: Bu cihazda mevcut bir PowerShell betiğini çalıştırmak Için Betiği Çalıştır Sihirbazı 'nı başlatın. Daha fazla bilgi için bkz. [komut dosyası çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Uzaktan denetim**: Bu cihazda bir Configuration Manager uzaktan denetim oturumu başlatın. Daha fazla bilgi için bkz. [bir Windows istemci bilgisayarını uzaktan yönetme](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Kaynak Gezgini**: Bu cihaz için Configuration Manager kaynak Gezgini başlatın. Daha fazla bilgi için bkz. [donanım envanterini görüntüleme](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) veya [yazılım envanterini görüntüleme](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Cihaz olmayan hücrelere sağ tıklayarak aşağıdaki ek eylemleri gerçekleştirin:  

     - **Kopyala**: hücrenin metnini panoya kopyalayın.  

     - Şu **olan cihazları göster**: Bu özellik için bu değere sahip cihazlar için sorgu. Örneğin, `OS` sorgunun sonuçlarından, sürüm satırındaki bir hücrede bu seçeneği belirleyin:`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Cihazları olmadan göster**: Bu özellik için bu değer olmadan cihazları sorgula. Örneğin, `OS` sorgunun sonuçlarından, sürüm satırındaki bir hücrede bu seçeneği belirleyin:`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing BT**: varsayılan Web tarayıcısını https://www.bing.com sorgu dizesi olarak bu değerle başlatın.  

   - Herhangi bir Köprülü metne tıklayarak görünümü bu belirli bilgilere özetleyin.  

   - Sonuçlar bölmesi 20.000 'den fazla satır göstermez. Verileri daha fazla filtrelemek için sorguyu ayarlayın ya da daha küçük bir koleksiyonda CMPivot 'i yeniden başlatın.  

7. Durum çubuğunda aşağıdaki bilgiler gösterilir (soldan sağa):  

   - Hedef koleksiyonun geçerli sorgusunun durumu. Bu durum şunları içerir:  
     - Sorguyu tamamlayan etkin istemcilerin sayısı (3)  
     - Toplam istemci sayısı (5)  
     - Çevrimdışı istemci sayısı (2)  
     - Hata döndüren tüm istemciler (0)  

       Örneğin, `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - İstemci işleminin KIMLIĞI. Örneğin, `id(16780221)`  

   - Geçerli koleksiyon. Örneğin, `PM_Team_Machines`  

   - Sonuçlar bölmesindeki toplam satır sayısı. Örneğin, `1 objects`  



## <a name="example-scenarios"></a>Örnek senaryolar

Aşağıdaki bölümler, ortamınızda CMPivot nasıl kullanabileceğinizi gösteren örnekler sağlar:


### <a name="example-1-stop-a-running-service"></a>Örnek 1: çalışan bir hizmeti durdur

Güvenlik yöneticiniz, bilgisayar tarayıcısı hizmetini, hesap departmanındaki tüm cihazlarda mümkün olduğunca hızlı bir şekilde durdurup devre dışı bırakmanızı ister. CMPivot ' i tüm cihazlar için bir koleksiyonda başlatın ve **hizmet** varlığında **Tümünü sorgula** ' yı seçin. 

`Service`

Sonuç olarak, **ad** sütununa sağ tıklayıp **Gruplandır**' ı seçin. 

`Service | summarize dcount( Device ) by Name`

**Tarayıcı** hizmetinin satırında, **dcount_** sütununda köprü numarasını tıklayın. 

`Service | where (Name == 'Browser') | summarize count() by Device`

Tüm cihazları çoklu seç, seçime sağ tıklayın ve **Betiği Çalıştır**' ı seçin. Bu eylem, bir hizmeti durdurup devre dışı bırakacağınız mevcut bir betiği çalıştırdığınız komut dosyası çalıştırma Sihirbazı 'nı başlatır. CMPivot ile tüm etkin bilgisayarlarda güvenlik olayına hızlı bir şekilde yanıt verin ve sonuçları komut dosyası çalıştırma Sihirbazı 'nda görüntüleyebilirsiniz. Daha sonra, gelecekte etkin hale geldiği sürece koleksiyondaki diğer bilgisayarları düzeltmek için bir yapılandırma temeli oluşturmak üzere daha sonra oluşturacaksınız. 

![Tarayıcı hizmeti için CMPivot örneği ve Betik Çalıştır eylemi](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Örnek 2: uygulama başarısızlıklarını önceden çözümleme  

İşlem Bakımı ile proaktif olmak için, yönettiğiniz bir sunucu koleksiyonuna karşı CMPivot çalıştırırsanız ve **APPCRASH** varlığındaki **Tümünü sorgula** ' yı seçin. **Dosya adı** sütununa sağ tıklayıp **artan düzende sırala**' yı seçin. Bir cihaz, sqlsqm. exe için her gün yaklaşık 03:00 zaman damgasıyla yedi sonuç döndürür. Dosya adını satırlardan birinde seçin, sağ tıklayın ve **Bing BT**' i seçin. Arama sonuçlarına göz atma Web tarayıcısında, daha fazla bilgi ve çözümleme ile ilgili bu sorun için bir Microsoft Destek makalesi bulabilirsiniz. 


### <a name="example-3-bios-version"></a>Örnek 3: BIOS sürümü

Öngörülebilir [yürütme tarafı kanalları güvenlik açıklarını azaltmak](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)için, gereksinimlerinden biri sistem BIOS 'unu güncelleştirmedir. **BIOS** varlığı için bir sorgu ile başlayabilirsiniz. Sonra **Sürüm** özelliğine **göre gruplandırabilirsiniz** . Ardından, "LENOVO-1140" gibi belirli bir değere sağ tıklayın ve **cihazları göster**' i seçin.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Örnek 4: boş disk alanı

Büyük bir dosyayı ağ dosya sunucusuna geçici olarak depolamanız gerekir, ancak hangisinin yeterli kapasiteye sahip olduğundan emin değilseniz. Bir dosya sunucuları koleksiyonuna karşı CMPivot başlatın ve **disk** varlığını sorgulayın. Gerçek zamanlı Depolama verileriyle etkin sunucuların bir listesini hızlıca döndürmek için CMPivot sorgusunu değiştirin:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-starting-in-version-1810"></a><a name="bkmk_cmpivot"></a>CMPivot sürüm 1810 ' den başlayarak
<!--1359068, 3607759-->

CMPivot, Configuration Manager sürüm 1810 ' den başlayarak aşağıdaki geliştirmeleri içerir:

- [CMPivot yardımcı programı ve performansı](#bkmk_cmpivot-perf)
- [Skaler işlevler](#bkmk_cmpivot-functions)  
- [Görselleştirmeler işleniyor](#bkmk_cmpivot-charts)  
- [Donanım envanteri](#bkmk_cmpivot-hinv)  
- [Skaler işleçler](#bkmk_cmpivot-operators)  
- [Sorgu Özeti](#bkmk_cmpivot-summary)  
- [Denetim durumu iletileri](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a>CMPivot yardımcı programı ve performansı

- CMPivot, 20.000 satır yerine 100.000 hücre döndürür.
  - Varlığın 5 özelliği varsa, anlamı 5 sütun, en fazla 20.000 satır gösterilir.
  - 10 özelliklerine sahip bir varlık için en fazla 10.000 satır gösterilir.
  - Gösterilen toplam veri 100.000 hücreden küçük veya buna eşit olacaktır.
- Sorgu Özeti sekmesinde, başarısız veya çevrimdışı cihazların sayısını seçin ve ardından **koleksiyon oluşturma**seçeneğini belirleyin. Bu seçenek, bu cihazların bir düzeltme dağıtımı ile hedeflemesini kolaylaştırır.
- Klasör simgesine tıklayarak **sık kullanılan** sorguları kaydedin.
   ![CMPivot içinde sık kullanılan bir sorgu kaydetme örneği](media/cmpivot-favorite.png)

- İstemciler, hızlı bir iletişim kanalı üzerinden siteye 80 KB 'tan daha az 1810 sürümüne güncelleştirilmiş bir bağlantı verir.
  - Bu değişiklik, betik veya sorgu çıkışını görüntüleme performansını artırır.
  - Betik veya sorgu çıkışı 80 KB 'tan büyükse, istemci verileri bir durum iletisi aracılığıyla gönderir.
  - İstemci, 1810 istemci sürümüne güncelleştirilmemiş durum iletilerini kullanmaya devam eder.

- CMPivot ' i başlattığınızda şu hatayı görebilirsiniz: **uyumsuz bir betik sürümü nedeniyle, şu anda CMPivot 'yi kullanamazsınız. Bu sorun, hiyerarşinin bir siteyi yükseltme sürecinde olması olabilir. Yükseltme tamamlanana kadar bekleyip yeniden deneyin.**

  - Bu iletiyi görürseniz, bunun anlamı:
    - Güvenlik kapsamı düzgün ayarlanmadı.
    - İşlemde yükseltmeyle ilgili sorunlar var.
    - Temel alınan CMPivot betiği uyumsuz.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a>Skaler işlevler
CMPivot Aşağıdaki skaler işlevleri destekler:
- **önce ()**: verilen TimeSpan DEĞERI geçerli UTC saat zamanından çıkartır  
- **datetime_diff ()**: iki tarih saat değeri arasındaki takvim farkını hesaplar  
- **Now ()**: geçerli UTC saat saatini döndürür  
- **bin ()**: değerleri, belirli bir bin boyutunun bir tam sayıya yuvarlar  

> [!Note]  
> Tarih saat veri türü, genellikle günün tarih ve saati olarak ifade edilen bir anlık zamanı temsil eder. Zaman değerleri 1 saniyelik birimlerde ölçülür. Tarih saat değeri her zaman UTC saat dilimlidir. ISO 8601 biçiminde her zaman Express tarih zaman rakamları, örneğin`yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Örnekler
- `datetime(2015-12-31 23:59:59.9)`: Belirli bir tarih saat değişmez değeri   
- `now()`: Geçerli saat  
- `ago(1d)`: Geçerli saat eksi bir gün  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a>Görselleştirmeler işleniyor

CMPivot artık KQL [render işleci](https://docs.microsoft.com/azure/kusto/query/renderoperator)için temel desteği içerir. Bu destek aşağıdaki türleri içerir:  
- **bargrafik**: ilk sütun x eksentir ve metin, tarih saat veya sayısal olabilir. İkinci sütunlar sayısal olmalıdır ve yatay bir şerit olarak görüntülenir.  
- **columnChart**: Yatay şeritler yerine dikey şeritler içeren bargrafik gibi.  
- **piechart**: ilk sütun renk eksenindedir, ikinci sütun ise sayısaldır.  
- **timechart**: çizgi grafik. İlk sütun x eksendir ve DateTime olmalıdır. İkinci sütun y eksenindedir.  

#### <a name="example-bar-chart"></a>Örnek: çubuk grafik
Aşağıdaki sorgu, en son kullanılan uygulamaları çubuk grafik olarak işler:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![CMPivot Bar grafik görselleştirmesi örneği](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Örnek: zaman grafiği
Zaman grafiklerini işlemek için yeni **bin ()** işlecini kullanarak olayları zamanında gruplayın. Aşağıdaki sorgu, son yedi gün içinde cihazların ne zaman başlatıldığını gösterir:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![CMPivot Time grafik görselleştirmesi örneği](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Örnek: pasta grafik
Aşağıdaki sorgu, bir pasta grafiğindeki tüm işletim sistemi sürümlerini görüntüler:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![CMPivot pasta grafik görselleştirmesi örneği](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a>Donanım envanteri
Herhangi bir donanım envanteri sınıfını sorgulamak için CMPivot kullanın. Bu sınıflar, donanım envanterinde yaptığınız özel uzantıları içerir. CMPivot hemen, site veritabanında depolanan son donanım envanteri taramasının önbellekteki sonuçları döndürür. Aynı zamanda, herhangi bir çevrimiçi istemciden canlı verilerle gerekirse sonuçları günceller.

Sonuçlar tablosu veya grafikteki verilerin renk doygunluğu, verilerin canlı veya önbelleğe alınıp alınmayacağını gösterir. Örneğin, koyu mavi, çevrimiçi bir istemciden gerçek zamanlı veriler. Açık mavi, önbelleğe alınmış veriler.

#### <a name="example"></a>Örnek

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Sütun grafik görselleştirmesi ile CMPivot Inventory Query örneği](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Sınırlamalar
- Aşağıdaki donanım envanteri varlıkları desteklenmez:  
    - Dizi özellikleri, örneğin IP adresi  
    - Real32/Real64 <!--example?-->  
    - Katıştırılmış nesne özellikleri <!--example?-->  
- Envanter varlık adları bir karakterle başlamalıdır
- Aynı ada sahip bir envanter varlığı oluşturarak yerleşik varlıkların üzerine yazılmaz  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a>Skaler işleçler
CMPivot, aşağıdaki skaler işleçleri içerir:  

> [!Note]  
> - LHS: işlecin sol tarafında bulunan dize  
> - RHS: işlecin sağ tarafındaki dize  


|İşleç|Açıklama|Örnek (true verir)|
|--------|-----------|---------------------|
|==|Eşittir|`"aBc" == "aBc"`|
|!=|Eşit değildir|`"abc" != "ABC"`|
|Like|LHS, RHS için bir eşleşme içerir|`"FabriKam" like "%Brik%"`|
|! Beğen|LHS, RHS için eşleşme içermiyor|`"Fabrikam" !like "%xyz%"`|
|içerir|RHS bir LHS alt sırası olarak gerçekleşir|`"FabriKam" contains "BRik"`|
|! Contains|LHS 'te RHS gerçekleşmiyor|`"Fabrikam" !contains "xyz"`|
|StartsWith|RHS bir başlangıç alt dizisi olan LHS|`"Fabrikam" startswith "fab"`|
|! StartsWith|RHS, LHS 'in bir başlangıç alt dizisi değildir|`"Fabrikam" !startswith "kam"`|
|EndsWith|RHS, LHS 'in bir kapanış alt sırasıdır|`"Fabrikam" endswith "Kam"`|
|! EndsWith|RHS, LHS 'in bir kapanış alt dizisi değildir|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a>Sorgu Özeti

CMPivot penceresinin alt kısmındaki **Sorgu Özeti** sekmesini seçin. Bu durum, çevrimdışı olan istemcileri tanımlamanızı veya oluşabilecek hataların sorunlarını gidermenize yardımcı olur. Bu duruma sahip belirli cihazların bir listesini açmak için say sütununda bir değer seçin. 

Örneğin, hata durumundaki cihaz sayısını seçin. Belirli bir hata iletisine bakın ve bu cihazların listesini dışarı aktarın. Hata belirli bir cmdlet 'in tanınmıyorsa, bir Windows PowerShell güncelleştirmesi dağıtmak için, dışarıya aktarılmış cihaz listesinden bir koleksiyon oluşturun.  

### <a name="cmpivot-audit-status-messages"></a>CMPivot denetim durumu iletileri

Sürüm 1810 ' den başlayarak, CMPivot çalıştırdığınızda **messageıd 40805**ile bir denetim durumu iletisi oluşturulur. Durum iletilerini **izleme** > **sistem durumu** > **durum iletisi sorguları**' na giderek görüntüleyebilirsiniz. Belirli **bir Kullanıcı Için tüm denetim durum iletilerini**, **belirli bir site için tüm denetim durum iletilerini**çalıştırabilir veya kendi durum iletisi sorgunuzu oluşturabilirsiniz.

İleti için aşağıdaki biçim kullanılır:

MessageID 40805: Kullanıcı &lt;kullanıcı adı> komut &lt;dosyası betiği çalıştı-Guid> &lt;karma betiği-kimliği> toplama &lt;>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14, CMPivot için komut dosyası GUID 'Sidir.
- Betik karması, istemcinin betikleri. log dosyasında görülebilir.
- İstemcinin komut dosyası deposunda depolanan karmayı da görebilirsiniz. İstemcideki dosya adı &lt;komut dosyası-GUID>_&lt;betik-karma>.
    - Örnek dosya adı: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123. PS
   

![CMPivot Audit durum iletisi örneği](media/cmpivot-audit-status-message.png)

## <a name="cmpivot-starting-in-version-1902"></a><a name="bkmk_cmpivot1902"></a>CMPivot sürüm 1902 ' den başlayarak
<!--3610960-->
Configuration Manager sürüm 1902 ' den başlayarak, bir hiyerarşide merkezi yönetim sitesinden (CAS) CMPivot çalıştırabilirsiniz. Birincil site, istemci iletişimini hala işler. Merkezi yönetim sitesinden CMPivot çalıştırılırken, yüksek hızlı ileti abonelik kanalının birincil sitesiyle iletişim kurar. Bu iletişim, siteler arasında standart SQL çoğaltmasına bağlı değildir.

CMPivot çalıştıran CA 'larda, SQL veya sağlayıcı aynı makinede olmadığında veya SQL her zaman açık yapılandırma durumunda ek izinler gerektirecektir. Bu uzak yapılandırmalarda, CMPivot için bir "çift atlama senaryosu" vardır.

Bu tür bir "çift atlama senaryosunda" CAS üzerinde çalışmak üzere CMPivot almak için kısıtlanmış temsili tanımlayabilirsiniz. Bu yapılandırmanın güvenlik etkilerine ilişkin etkilerini anlamak için, [Kerberos kısıtlanmış temsili](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) makalesini okuyun. Kerberos, makineler arasındaki tüm atlamalarla çalışmalıdır.<!--5746133--> SQL veya SMS sağlayıcısı gibi birden fazla uzak yapılandırmaya sahip CA 'LAR veya birden çok güvenilen orman varsa, izin ayarları birleşimine ihtiyacınız olabilir. Aşağıda gerçekleştirmeniz gerekebilecek adımlar verilmiştir:

### <a name="cas-has-a-remote-sql-server"></a>CAS uzak bir SQL Server 'a sahip

1. Her birincil sitenin SQL Server 'a gidin.
   1. CAS uzak SQL Server ve CAS site sunucusunu [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) grubuna ekleyin.
   ![Birincil sitenin SQL Server 'daki Configmgr_DviewAccess grubu](media/cmpivot-dviewaccess-group.png)
1. Active Directory Kullanıcıları ve Bilgisayarları ' na gidin.
   1. Her birincil site sunucusu için, sağ tıklayın ve **Özellikler**' i seçin.
      1. Temsili sekmesinde üçüncü seçeneği belirleyin, **Bu bilgisayara yalnızca belirtilen hizmetlere atamak üzere güvenin**. 
      1. **Yalnızca Kerberos kullan**' ı seçin.
      1. CA 'ların SQL Server hizmetini bağlantı noktası ve örneği ile ekleyin.
      1. Bu değişikliklerin şirketinizin güvenlik ilkenize göre hizalanmasına dikkat edin!
   1. CAS sitesi için sağ tıklayıp **Özellikler**' i seçin.
      1. Temsili sekmesinde üçüncü seçeneği belirleyin, **Bu bilgisayara yalnızca belirtilen hizmetlere atamak üzere güvenin**. 
      1. **Yalnızca Kerberos kullan**' ı seçin.
      1. Her birincil sitenin SQL Server hizmetini bağlantı noktası ve örneğiyle ekleyin.
      1. Bu değişikliklerin şirketinizin güvenlik ilkenize göre hizalanmasına dikkat edin!

   ![İki atlama için CMPivot AD temsili örneği](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CA 'LAR uzak bir sağlayıcıya sahiptir

1. Her birincil sitenin SQL Server 'a gidin.
   1. CAS sağlayıcısı makine hesabını ve CAS site sunucusunu [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) grubuna ekleyin.
1. Active Directory Kullanıcıları ve Bilgisayarları ' na gidin.
   1. CAS sağlayıcısı makinesini seçin, sağ tıklayın ve **Özellikler**' i seçin.
      1. Temsili sekmesinde üçüncü seçeneği belirleyin, **Bu bilgisayara yalnızca belirtilen hizmetlere atamak üzere güvenin**. 
      1. **Yalnızca Kerberos kullan**' ı seçin.
      1. Her birincil sitenin SQL Server hizmetini bağlantı noktası ve örneğiyle ekleyin.
      1. Bu değişikliklerin şirketinizin güvenlik ilkenize göre hizalanmasına dikkat edin!
   1. CAS site sunucusunu seçin, sağ tıklayın ve **Özellikler**' i seçin.
      1. Temsili sekmesinde üçüncü seçeneği belirleyin, **Bu bilgisayara yalnızca belirtilen hizmetlere atamak üzere güvenin**. 
      1. **Yalnızca Kerberos kullan**' ı seçin.
      1. Her birincil sitenin SQL Server hizmetini bağlantı noktası ve örneğiyle ekleyin.
      1. Bu değişikliklerin şirketinizin güvenlik ilkenize göre hizalanmasına dikkat edin!
1. CAS uzak sağlayıcı makinesini yeniden başlatın.

### <a name="sql-always-on"></a>SQL Always on

1. Her birincil sitenin SQL Server 'a gidin.
   1. CAS site sunucusunu [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) grubuna ekleyin.
1. Active Directory Kullanıcıları ve Bilgisayarları ' na gidin.
   1. Her birincil site sunucusu için, sağ tıklayın ve **Özellikler**' i seçin.
      1. Temsili sekmesinde üçüncü seçeneği belirleyin, **Bu bilgisayara yalnızca belirtilen hizmetlere atamak üzere güvenin**. 
      1. **Yalnızca Kerberos kullan**' ı seçin.
      1. Bağlantı noktası ve örneği olan SQL düğümlerine yönelik CA 'ların SQL Server hizmet hesaplarını ekleyin.
      1. Bu değişikliklerin şirketinizin güvenlik ilkenize göre hizalanmasına dikkat edin!
   1. CAS site sunucusunu seçin, sağ tıklayın ve **Özellikler**' i seçin.
      1. Temsili sekmesinde üçüncü seçeneği belirleyin, **Bu bilgisayara yalnızca belirtilen hizmetlere atamak üzere güvenin**. 
      1. **Yalnızca Kerberos kullan**' ı seçin.
      1. Her birincil sitenin SQL Server hizmetini bağlantı noktası ve örneğiyle ekleyin.
      1. Bu değişikliklerin şirketinizin güvenlik ilkenize göre hizalanmasına dikkat edin!
1. SPN 'nin CAS SQL dinleyicisi adı ve her birincil SQL dinleyicisi adı için [yayımlandığından](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) emin olun.
1. Birincil SQL sunucularını yeniden başlatın.
1. CAS site sunucusunu ve CAS SQL sunucularını yeniden başlatın.

## <a name="cmpivot-starting-in-version-1906"></a><a name="bkmk_cmpivot1906"></a>CMPivot sürüm 1906 ' den başlayarak

Sürüm 1906 ' den başlayarak, şu öğeler CMPivot 'ye eklenmiştir:

- [Birleşimler, ek işleçler ve toplayıcısını değiştirme](#bkmk_cmpivot_joins)
- [Güvenlik Yöneticisi rolüne CMPivot izinleri eklendi](#bkmk_cmpivot_secadmin1906)
- [Tek başına CMPivot](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a>CMPivot içinde birleştirmeler, ek işleçler ve aggregekleyin
<!--4054074-->
Artık ek aritmetik işleçleri, aggregators 'lar ve kayıt defteri ve dosya kullanma gibi sorgu birleştirmeleri ekleme imkanına sahipsiniz. Şu öğeler Eklendi:

#### <a name="table-operators"></a>Tablo işleçleri

|Tablo işleçleri| Açıklama|
|-----|-----|
| [ayrılma](https://docs.microsoft.com/azure/kusto/query/joinoperator)| Aynı cihazla eşleşen satıra göre yeni bir tablo oluşturmak için iki tablo satırını birleştirin|
|işlenecek|Sonuçları grafik çıkış olarak işler|

Render işleci CMPivot içinde zaten var. Birden çok seri ve **WITH** ifadesiyle ilgili destek eklendi. Daha fazla bilgi için bkz. [örnekler](#bkmk_cmpivot_examples1906) bölümü ve kusto 'in [JOIN işleci](https://docs.microsoft.com/azure/kusto/query/joinoperator) makalesi.

#### <a name="limitations-for-joins"></a>Birleşimler için sınırlamalar

1. Birleştir sütunu her zaman **cihaz** alanında örtük olarak yapılır.
1. Sorgu başına en fazla 5 birleşim kullanabilirsiniz.
1. En fazla 64 Birleşik sütun kullanabilirsiniz.

#### <a name="scalar-operators"></a>Skaler işleçler

|İşleç| Açıklama|Örnek|
|-----|-----|-----|
| + | Ekle| `2 + 1, now() + 1d`|
| - |  Çıkar| `2 - 1, now() - 1d`|
| * | Çarp| `2 * 2`|
| / | Böl | `2 / 1`|
| % | Mod | `2 % 1`

#### <a name="aggregation-functions"></a>Toplama işlevleri

|İşlev| Açıklama|
|-----|-----|
| yüzdebirlik ()| Ifadenin belirttiği popülasyon için belirtilen en yakın derecelendirme yüzdelik değeri için bir tahmin döndürür|
| sumif() | Koşulun true olarak değerlendirilen bir Ifade toplamı döndürür|

#### <a name="scalar-functions"></a>Skaler işlevler

|İşlev| Açıklama|
|-----|-----|
| case()| Koşulların bir listesini değerlendirir ve koşulu karşılanan ilk sonuç ifadesini döndürür |
| FF () | İlk bağımsız değişkeni değerlendirir ve koşulun doğru (ikinci) ya da yanlış (üçüncü) olarak değerlendirildiğine bağlı olarak ikinci veya üçüncü bağımsız değişkenlerin değerini döndürür|
 | indexof() | İşlev, giriş dizesinde belirtilen bir dizenin ilk oluşumunun sıfır tabanlı dizinini bildirir|
| strcat() | 1 ile 64 arasında bağımsız değişken arasına ekler |
| strlen()| Giriş dizesinin karakter cinsinden uzunluğunu döndürür|
| substring() | Bir kaynak dizeden, dizenin sonuna kadar bir dizinden başlayarak bir alt dize ayıklar |
| tostring() | Girişi dize işlemine dönüştürür |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a>Örnekler

- Cihazı, üreticiyi, modeli ve OSVersion 'yi göster:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- Bir cihaz için önyükleme saatlerinin grafiğini göster:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![MS 'de bir cihazın önyükleme zamanlarını gösteren yığılmış çubuk grafiği](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a>Güvenlik Yöneticisi rolüne CMPivot izinleri eklendi
<!--4683130-->

Sürüm 1906 ' den başlayarak, Configuration Manager yerleşik **Güvenlik Yöneticisi** rolüne aşağıdaki izinler eklenmiştir:

 - SMS komut dosyasında **Oku**
 - Koleksiyonda **CMPivot Çalıştır**
 - Envanter raporunda **Oku**

>[!NOTE]
> **Çalıştırma betikleri** , **Run CMPivot** izninin bir süper kümesidir.
 

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a>Tek başına CMPivot
<!--3555890, 4619340, 4683130 -->

Sürüm 1906 ' den başlayarak, tek başına bir uygulama olarak CMPivot kullanabilirsiniz. CMPivot tek başına yalnızca Ingilizce olarak kullanılabilir. Ortamınızdaki cihazların gerçek zamanlı durumunu görüntülemek için Configuration Manager konsolunun dışında CMPivot çalıştırın. Bu değişiklik, konsolu yüklemeden önce bir cihazda CMPivot kullanmanıza olanak sağlar.

> [!Tip]  
> Bu özellik ilk olarak sürüm 1906 ' de [yayın öncesi özelliği](pre-release-features.md)olarak sunulmuştur. Sürüm 2002 ' den başlayarak, artık yayın öncesi bir özellik değildir.  

CMPivot 'in gücünden birini, yardım masası veya güvenlik yöneticileri gibi diğer kişilerle paylaşabilirsiniz. Bu kişiler, geleneksel olarak kullandıkları diğer araçlarla birlikte Configuration Manager sorgulamak için CMPivot kullanabilir. Bu zengin yönetim verilerini paylaşarak, roller arası iş sorunlarını önceden çözmek için birlikte çalışabilirsiniz.

#### <a name="install-cmpivot-standalone"></a>CMPivot tek başına yükleme

1. CMPivot çalıştırmak için gereken izinleri ayarlayın. Daha fazla bilgi için bkz. [Önkoşullar](#prerequisites). İzinler kullanıcıya uygunsa [Güvenlik Yöneticisi rolünü](#bkmk_cmpivot_secadmin1906) de kullanabilirsiniz.
2. Aşağıdaki yolda CMPivot uygulama yükleyicisini bulun: `<site install path>\tools\CMPivot\CMPivot.msi`. Bu yoldan çalıştırabilir veya başka bir konuma kopyalayabilirsiniz.
3. CMPivot tek başına uygulamasını çalıştırdığınızda bir siteye bağlanmanız istenir. Merkezi Yönetim veya birincil site sunucusunun tam etki alanı adını ya da bilgisayar adını belirtin.
   - Tek başına CMPivot her açışınızda bir site sunucusuna bağlanmanız istenir.
4. CMPivot çalıştırmak istediğiniz koleksiyona gidin ve sorgunuzu çalıştırın.

   ![Sorgunuzu çalıştırmak istediğiniz koleksiyona gidin](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> **Komut dosyalarını çalıştır**, **Kaynak Gezgini**ve Web araması gibi sağ tıklama eylemleri CMPivot tek başına kullanılamaz. CMPivot tek başına 'ın birincil kullanımı Configuration Manager altyapısından bağımsız olarak sorgulama yapılır. Güvenlik yöneticilerine yardım için, CMpivot tek başına, Microsoft Defender Güvenlik Merkezi 'ne bağlanma özelliğini içerir. <!--5605358-->

## <a name="cmpivot-starting-in-version-1910"></a><a name="bkmk_cmpivot1910"></a>CMPivot sürüm 1910 ' den başlayarak
<!--5410930, 3197353-->
Sürüm 1910 ' den başlayarak, CMPivot ağ trafiğini ve sunucularınızdaki yükü azaltmak için önemli ölçüde iyileştirilmiştir. Ayrıca, sorun giderme ve aramaya yardımcı olmak için birçok varlık ve varlık geliştirmesi eklenmiştir. 1910 sürümünde CMPivot için aşağıdaki değişiklikler yapılmıştır:

- [CMPivot altyapısına iyileştirmeler](#bkmk_optimization)
- Ek varlıklar ve varlık geliştirmeleri:
  - Windows olay günlükleri ([WinEvent](#bkmk_WinEvent))
  - Dosya içeriği ([FileContent](#bkmk_File))
  - Süreçler tarafından yüklenen dll 'ler ([ProcessModule](#bkmk_ProcessModule))
  - Azure Active Directory bilgileri ([Aadstatus](#bkmk_AadStatus))
  - Uç nokta koruma durumu ([Epstatus](#bkmk_EPStatus))
- [CMPivot tek başına kullanarak yerel cihaz sorgusu değerlendirmesi](#bkmk_local-eval)
- [CMPivot için diğer geliştirmeler](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a>CMPivot altyapısına iyileştirmeler
<!--3197353-->
Sunucularınızdaki ağ trafiğini ve yükünü azaltmak için CMPivot 1910 ' de iyileştirildi. Birçok sorgu işlemi artık sunucular yerine doğrudan istemcide gerçekleştirilir. Bu değişiklik Ayrıca bazı CMPivot işlemlerinin ilk sorgudan en az miktarda veri döndürdüğü anlamına gelir. Daha fazla bilgi için verilere detaya gitmeye karar verirseniz, istemciden ek verileri getirmek için yeni bir sorgu çalıştırılabilir. Örneğin, daha önce bir "özetlenen sayım" sorgusu çalıştırdığınızda sunucuya büyük bir veri kümesi döndürülür.  Büyük bir veri kümesi geri alınırken hemen ayrıntıya inme, çok sayıda yalnızca özetlenen sayı gerekiyordu. 1910 ' de, belirli bir istemcide detaya gitmeyi seçtiğinizde, istediğiniz ek verileri döndürmek için başka bir veri koleksiyonu oluşur. Bu değişiklik, çok sayıda istemciye karşı sorgulara daha iyi performans ve ölçeklenebilirlik sunar. <!--3197353, 5458337-->

#### <a name="examples"></a>Örnekler

CMPivot iyileştirmeleri, CMPivot sorgularını çalıştırmak için gereken ağ ve sunucu CPU yükünü önemli ölçüde azaltır. Bu iyileştirmelere göre, artık gigabayt 'tan fazla istemci verisi gerçek zamanlı olarak bulunabilir. Aşağıdaki sorgularda bu iyileştirmeler gösterilmektedir:

- Kimlik doğrulama hatalarıyla kuruluşunuzdaki tüm istemcilerde tüm olay günlüklerinde arama yapın.

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Karma olarak bir dosya arayın.

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a>WinEvent (\<günlük adı>, [\<TimeSpan>])

Bu varlık olay günlüklerinden ve olay izleme günlük dosyalarından olayları almak için kullanılır. Varlık, Windows olay günlüğü teknolojisi tarafından oluşturulan olay günlüklerinden verileri alır. Varlık Ayrıca, Windows için olay Izleme tarafından oluşturulan günlük dosyalarındaki olayları alır (ETW). WinEvent, son 24 saat içinde varsayılan olarak gerçekleşen olaylara bakar. Ancak, 24 saatlik varsayılan değer bir TimeSpan eklenerek geçersiz kılınabilir.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a>Dosya Içeriği (\<filename>)

Dosya Içeriği, bir metin dosyasının içeriğini almak için kullanılır.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a>ProcessModule (\<processname>)  

Bu varlık, belirli bir işlem tarafından yüklenen modülleri (dll 'ler) numaralandırmak için kullanılır. ProcessModule, meşru işlemlerde gizlemekte olan kötü amaçlı yazılımlara yönelik arama yaparken yararlıdır.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a>AadStatus

Bu varlık, bir cihazdan geçerli Azure Active Directory kimlik bilgilerini almak için kullanılabilir.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a>EPStatus

EPStatus, bilgisayarda yüklü olan kötü amaçlı yazılımdan koruma yazılımının durumunu almak için kullanılır.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a>CMPivot tek başına kullanarak yerel cihaz sorgusu değerlendirmesi
<!--3197353-->
Configuration Manager konsolunun dışında CMPivot kullanırken, Configuration Manager altyapısına gerek duymadan yalnızca yerel cihazı sorgulayabilirsiniz. Artık yerel cihazdaki WMI bilgilerini hızlıca görüntülemek için CMPivot Azure Log Analytics sorgularından yararlanabilirsiniz. Bu Ayrıca, daha büyük bir ortamda çalıştırılmadan önce CMPivot sorgularının doğrulanmasını ve yeniden kullanılmasını da mümkün bir şekilde sunar. CMPivot tek başına yalnızca Ingilizce olarak kullanılabilir. Tek başına CMPivot yükleme hakkında daha fazla bilgi için bkz. [Install CMPivot standalone](#install-cmpivot-standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Yerel aygıt sorgu değerlendirmesi için bilinen sorunlar

 - **Bu bilgisayarda** , KILITLI bir WMI sınıfı gibi erişiminiz olmayan bir WMI varlığı için sorgulama yaparsanız, CMPivot 'de bir kilitlenme görebilirsiniz. Bu varlıkları sorgulamak için yükseltilmiş ayrıcalıklara sahip bir hesabı kullanarak CMPivot çalıştırın. <!--5753242-->
- **Bu bılgısayarda**WMI olmayan varlıkları Sorguladıysanız **geçersiz bir ad alanı** veya belirsiz bir özel durum görürsünüz.
- Doğrudan yürütülebilir dosyanın yolundan değil, Başlat menüsü kısayolundan CMPivot tek başına Çalıştır. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a>Diğer geliştirmeler

- Yeni `like` işleci kullanarak normal ifade türü sorguları yapabilirsiniz. Örneğin:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- **Ccmlog ()** ve **EventLog ()** varlıklarını, varsayılan olarak yalnızca son 24 saat içindeki iletilere bakmak üzere güncelleştirdik. Bu davranış, isteğe bağlı bir TimeSpan değeri geçirerek geçersiz kılınabilir. Örneğin, aşağıdaki sorgu son 1 saat içindeki olaylara bakar:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- **Dosya ()** varlığı gizli ve sistem dosyaları hakkında bilgi toplamak ve MD5 karmasını dahil etmek için güncelleştirilmiştir. MD5 karması SHA256 karması kadar doğru olmadığından, çoğu kötü amaçlı bültende yaygın olarak bildirilen karma değer olarak eğilimi gösterir.  

- Sorgularda yorum ekleyebilirsiniz.<!-- 5431463 --> Bu davranış, sorgu paylaşımında yararlıdır. Örneğin:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot, son siteye otomatik olarak bağlanır.<!-- 5420395 --> CMPivot başlattıktan sonra, gerekirse yeni bir siteye bağlanabilirsiniz.

- **Dışarı aktarma** menüsünde, **panoya bağlantıyı sorgulamak**için yeni seçeneğini belirleyin.<!-- 5431577 --> Bu eylem, diğer kullanıcılarla paylaşabileceğiniz panoya bir bağlantı kopyalar. Örneğin:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    Bu bağlantı aşağıdaki sorguyla birlikte CMPivot tek başına açılır:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > Bu bağlantının çalışması için [tek başına CMPivot 'yi yükleme](#install-cmpivot-standalone).

- Sorgu sonuçlarında, cihaz Microsoft Defender Gelişmiş tehdit koruması (ATP) ' ye kaydedildiyse, **Microsoft Defender Güvenlik Merkezi** çevrimiçi portalı ' nı başlatmak için cihaza sağ tıklayın.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>1910 sürümündeki CMPivot için bilinen sorunlar

- Sınıra ulaşıldığında en fazla sonuç başlığı görüntülenmeyebilir. <!--5431427-->
  - Her istemci, sorgu başına 128 KB değer ile sınırlıdır.
  - Sorgunun sonuçları 128 KB 'yi aşarsa sonuçlar kesilebilir.
  
## <a name="cmpivot-starting-in-version-2002"></a><a name="bkmk_2002"></a>CMPivot sürüm 2002 ' den başlayarak
<!--5870934-->
CMPivot varlıklarından gezinmeyi kolaylaştırdık. Configuration Manager sürüm 2002 ' den başlayarak CMPivot varlıklarda arama yapabilirsiniz. Varlıkları ve varlık nesne türlerini kolayca ayırt etmek için de yeni simgeler eklenmiştir.

![CMPivot varlıklarını arama](./media/5870934-search-cmpivot-entities.png)

 
## <a name="inside-cmpivot"></a>CMPivot içinde

CMPivot, Configuration Manager "hızlı kanal" kullanarak istemcilere sorgu gönderir. Sunucudan istemciye olan bu iletişim kanalı, istemci bildirim eylemleri, istemci durumu ve Endpoint Protection gibi diğer özellikler tarafından da kullanılır. İstemciler benzer hızlı durum ileti sistemi aracılığıyla sonuçları döndürür. Durum iletileri geçici olarak veritabanında depolanır. İstemci bildirimi için kullanılan bağlantı noktaları hakkında daha fazla bilgi için bkz. [bağlantı noktaları](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP) makalesi.

Sorgular ve sonuçlar yalnızca metindir. **Installsoftware** ve **Process** varlıkları en büyük sonuç kümelerinden bazılarını döndürür. Performans testi sırasında, bu sorgular için bir istemciden en büyük durum iletisi dosya boyutu **1 KB**'tan az. 50.000 etkin istemcilerle büyük bir ortama ölçeklenirse, bu tek seferlik sorgu ağ genelinde 50 MB 'tan az veri oluşturur. Hoş geldiniz sayfasındaki tüm öğeler, altı çizili olan ve istemci başına en fazla 1000 bilgi döndürür.

![CMPivot altı çizili varlıklar örneği](media/cmpivot-underlined-entities.png)

Configuration Manager 1810 ' den başlayarak CMPivot, genişletilmiş donanım envanteri sınıfları dahil donanım envanteri verilerini sorgulayabilir. Bu yeni varlıklar (hoş geldiniz sayfasında altı çizili olmayan varlıklar), belirli bir donanım envanteri özelliği için ne kadar veri tanımlandığına bağlı olarak çok daha büyük veri kümeleri döndürebilir. Örneğin, "ınstallandexecutable" varlığı, sorgu yaptığınız belirli verilere bağlı olarak istemci başına birden fazla MB veri döndürebilir. CMPivot kullanarak daha büyük bir donanım envanteri veri kümesi döndürürken sistemlerinizdeki performansı ve ölçeklenebilirliği en az bir şekilde kullanın.

Bir saatten sonra bir sorgu zaman aşımına uğrar. Örneğin, bir koleksiyon 500 cihaza sahiptir ve istemcilerin Şu anda 450 ' i çevrimiçi durumda. Bu etkin cihazlar sorguyu alır ve neredeyse anında sonuçları döndürür. Diğer 50 istemcileri çevrimiçi olduğunda, CMPivot penceresini açık bırakırsanız, sorgu da alır ve sonuçları döndürür. 

## <a name="log-files"></a>Günlük dosyaları

 CMPivot etkileşimleri aşağıdaki günlük dosyalarına kaydedilir:

**Sunucu tarafı:**
- SmsProv. log
- BgbServer. log
- StateSys. log

**İstemci tarafı:**
- CcmNotificationAgent.log
- Betikler. log
- StateMessage.log

Daha fazla bilgi için bkz. [günlük dosyaları](../../plan-design/hierarchy/log-files.md) ve [sorun giderme CMPivot](cmpivot-tsg.md).

## <a name="next-steps"></a>Sonraki adımlar
 
[CMPivot sorunlarını giderme](cmpivot-tsg.md)

[PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md)


