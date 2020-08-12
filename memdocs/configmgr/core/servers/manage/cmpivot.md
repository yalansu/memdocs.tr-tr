---
title: Gerçek zamanlı veriler için CMPivot
titleSuffix: Configuration Manager
description: Configuration Manager 'de CMPivot kullanarak istemcileri gerçek zamanlı olarak sorgulama hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 06e2a90e8c481fba834cbd1b6b1f5233572e4b17
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128349"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>Configuration Manager içindeki gerçek zamanlı veriler için CMPivot

<!--1358456-->

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, müşterilerin raporlama amacıyla kullanacağı, cihaz verilerinin büyük merkezi bir deposunu sağlamıştır. Site genellikle bu verileri haftalık olarak toplar. Sürüm 1806 ' den başlayarak, CMPivot artık ortamınızdaki cihazların gerçek zamanlı durumuna erişim sağlayan yeni bir konsol içi yardımcı programdır. Hedef koleksiyondaki Şu anda bağlı olan tüm cihazlarda bir sorguyu hemen çalıştırır ve sonuçları döndürür. Ardından bu verileri aracında filtreleyin ve gruplandırın. Çevrimiçi istemcilerden gerçek zamanlı veriler sunarak, iş sorularını daha hızlı bir şekilde yanıtlayabilir, sorun giderebilir ve güvenlik olaylarına yanıt verebilirsiniz.

Örneğin, [kurgusal yürütme tarafı kanalı güvenlik açıklarını azaltıcı](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)bir şekilde, gereksinimlerden biri sistem BIOS 'unu güncelleştirmelerdir. CMPivot kullanarak sistem BIOS bilgilerini hızlı bir şekilde sorgulayabilir ve uyumlu olmayan istemcileri bulabilirsiniz.

 > [!IMPORTANT]  
 > - Bazı güvenlik yazılımları c:\windows\ccm\scriptstorekonumundan çalıştırılan betikleri engelleyebilir. Bu, CMPivot sorgularının başarıyla yürütülmesini engelleyebilir. Bazı güvenlik yazılımları, CMPivot PowerShell çalıştırılırken denetim olayları ya da uyarılar oluşturabilir.
 > - Bazı kötü amaçlı yazılımdan koruma yazılımları yanlışlıkla Configuration Manager çalıştırmak betiklerine veya CMPivot özelliklerine karşı olayları tetikleyemeyebilir. Kötü amaçlı yazılımdan koruma yazılımının bu özelliklerin girişim olmadan çalışmasına izin vermesi için%windir%\CCM\ScriptStore hariç tutulması önerilir.


## <a name="prerequisites"></a>Ön koşullar

CMPivot kullanmak için aşağıdaki bileşenler gereklidir:

- Hedef cihazları Configuration Manager istemcisinin en son sürümüne yükseltin.  

- Hedef istemciler en az PowerShell sürüm 4 gerektirir.

- Aşağıdaki varlıklara veri toplamak için, hedef istemciler PowerShell sürüm 5,0 gerektirir:  
  - Yöneticiler
  - Bağlantı
  - Komutunu
  - SMBConfig

- CMPivot ve [Microsoft Edge](../../../apps/deploy-use/deploy-edge.md) yükleyicisi, **Microsoft kod imzalama** sertifikasıyla imzalanır. Bu sertifika, **Güvenilen Yayımcılar** deposunda listelenmemişse, eklemeniz gerekir. Aksi halde, PowerShell yürütme ilkesi **AllSigned**olarak ayarlandığında CMPivot ve Microsoft Edge yükleyicisi çalışmaz. <!--7585106-->

## <a name="permissions"></a>İzinler

CMPivot için aşağıdaki izinler gereklidir:

- **SMS betikleri** nesnesinde **Oku** izni
- **Koleksiyonda** **betikleri Çalıştır** izni
   - Alternatif olarak, sürüm 1906 ' den başlayarak, **CMPivot Run** on the **Collection**kullanabilirsiniz.
- **Envanter raporlarında** **okuma** izni
- Varsayılan kapsam.

> [!NOTE]
> - **Çalıştırma betikleri** , **Run CMPivot** izninin bir süper kümesidir.
> - Sürüm 1906 ' den başlayarak, [CMPivot için izinler](cmpivot-changes.md#bkmk_cmpivot_secadmin1906) Configuration Manager yerleşik **Güvenlik Yöneticisi** rolüne eklenmiştir.
 
## <a name="limitations"></a>Sınırlamalar

- Hiyerarşide, CMPivot çalıştırmak için Configuration Manager konsolunu *birincil siteye* bağlayın. **Start CMPivot** eylemi, bir merkezi yönetim sıtesıne (CAS) bağlıyken konsolunda görüntülenmez.
  - Configuration Manager sürüm 1902 ' den başlayarak, bir CA 'dan CMPivot çalıştırabilirsiniz. Bazı ortamlarda ek izinler gerekir. Daha fazla bilgi için bkz. [sürüm 1902 Için CMPivot değişiklikleri](cmpivot-changes.md#bkmk_cmpivot1902).

- CMPivot yalnızca geçerli siteye bağlı istemciler için verileri döndürür.  

- Bir koleksiyon başka bir siteden cihazlar içeriyorsa, CMPivot sonuçları yalnızca geçerli sitedeki cihazlardan alınır.  

- Varlık özelliklerini, sonuçlar için sütunları veya cihazlardaki eylemleri özelleştiremezsiniz.  

- Yalnızca bir CMPivot örneği, Configuration Manager konsolunu çalıştıran bir bilgisayarda aynı anda çalışabilir.  

- Sürüm 1806 ' de, **Yöneticiler** varlığına yönelik sorgu yalnızca Grup "Administrators" olarak adlandırılmışsa işe yarar. Grup adı yerelleştirildiği takdirde bu çalışmaz. Örneğin, Fransızca 'da "Yönettemi".<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>CMPivot Başlat

1. Configuration Manager konsolunda, birincil siteye bağlanın. **Varlıklar ve uyum** çalışma alanına gidin ve **Cihaz Koleksiyonları** düğümünü seçin. Bir hedef koleksiyon seçin ve aracı başlatmak için Şeritteki **CMPivot Başlat** ' a tıklayın. Bu seçeneği görmüyorsanız, aşağıdaki konfigürasyonları kontrol edin:  
   - Hesabınızın gerekli izinlere sahip olduğunu bir site yöneticisiyle onaylayın. Daha fazla bilgi için bkz. [Önkoşullar](#prerequisites).  
   - Konsolunu bir *birincil siteye*bağlayın.  

2. Arabirim, aracı kullanma hakkında daha fazla bilgi sağlar.  

     - Sorgu dizelerini en üste el ile girin veya çevrimiçi belgelerde bağlantıları tıklatın.  

     - Sorgu dizesine eklemek için **varlıklardan** birine tıklayın.  

     - **Tablo işleçleri**, **toplama Işlevleri**ve **skaler işlevler** bağlantıları, Web tarayıcısında dil başvurusu belgelerini açar. CMPivot, [kusto sorgu dilini (KQL)](https://docs.microsoft.com/azure/kusto/query/)kullanır.  

3. İstemcilerdeki sonuçları görüntülemek için CMPivot penceresini açık tutun. CMPivot penceresini kapattığınızda oturum tamamlanmıştır.
   - Sorgu gönderilmişse, istemciler hala sunucuya bir durum iletisi yanıtı gönderir.  



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
    - Varsayılan olarak, bu bölme IntelliSense kullanır. Örneğin, yazmaya başladıysanız `D` , IntelliSense Bu harfle başlayan tüm varlıkları önerir. Bir seçenek belirleyin ve eklemek için SEKME tuşuna basın. Bir kanal karakteri ve bir boşluk yazıp `| ` IntelliSense tüm tablo işleçlerini önerir. `summarize`Bir boşluk ekleyin ve yazın ve IntelliSense tüm toplama işlevlerini önerir. Bu işleçler ve işlevler hakkında daha fazla bilgi için CMPivot içindeki **giriş** sekmesine tıklayın.  

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
         - Sürüm 2006 ' den başlayarak, **Pivot** **cihaz Özeti**ile değiştirilmiştir. Daha fazla bilgi için bkz. [sürüm 2006 Için CMPivot değişiklikleri](cmpivot-changes.md#bkmk_2006).

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

       Örnek: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - İstemci işleminin KIMLIĞI. Örnek: `id(16780221)`  

   - Geçerli koleksiyon. Örnek: `PM_Team_Machines`  

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

İşlem Bakımı ile proaktif olmak için, yönettiğiniz bir sunucu koleksiyonuna karşı CMPivot çalıştırırsanız ve **APPCRASH** varlığındaki **Tümünü sorgula** ' yı seçin. **Dosya adı** sütununa sağ tıklayıp **artan düzende sırala**' yı seçin. Bir cihaz her gün 03:00 zaman damgasıyla sqlsqm.exe için yedi sonuç döndürür. Dosya adını satırlardan birinde seçin, sağ tıklayın ve **Bing BT**' i seçin. Arama sonuçlarına göz atma Web tarayıcısında, daha fazla bilgi ve çözümleme ile ilgili bu sorun için bir Microsoft Destek makalesi bulabilirsiniz. 


### <a name="example-3-bios-version"></a>Örnek 3: BIOS sürümü

Öngörülebilir [yürütme tarafı kanalları güvenlik açıklarını azaltmak](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)için, gereksinimlerinden biri sistem BIOS 'unu güncelleştirmedir. **BIOS** varlığı için bir sorgu ile başlayabilirsiniz. Sonra **Sürüm** özelliğine **göre gruplandırabilirsiniz** . Ardından, "LENOVO-1140" gibi belirli bir değere sağ tıklayın ve **cihazları göster**' i seçin.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Örnek 4: boş disk alanı

Büyük bir dosyayı ağ dosya sunucusuna geçici olarak depolamanız gerekir, ancak hangisinin yeterli kapasiteye sahip olduğundan emin değilseniz. Bir dosya sunucuları koleksiyonuna karşı CMPivot başlatın ve **disk** varlığını sorgulayın. Gerçek zamanlı Depolama verileriyle etkin sunucuların bir listesini hızlıca döndürmek için CMPivot sorgusunu değiştirin:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a>Tek başına CMPivot

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
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

- [CMPivot üzerinde yapılan değişiklikler](cmpivot-changes.md)
- [CMPivot sorunlarını giderme](cmpivot-tsg.md)
- [PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md)


