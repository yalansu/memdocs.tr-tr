---
title: CMPivot üzerinde yapılan değişiklikler
titleSuffix: Configuration Manager
description: Configuration Manager sürümleri arasında CMPivot üzerinde yapılan değişiklikler hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a49a9564-0863-44c3-991e-a8e271fed586
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 32800284c415de6a36e856abf473bc6d8d729e6f
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608253"
---
# <a name="changes-to-cmpivot"></a>CMPivot üzerinde yapılan değişiklikler

Configuration Manager sürümleri arasında [CMPivot](cmpivot.md) üzerinde yapılan değişiklikler hakkında bilgi edinmek için aşağıdaki bilgileri kullanın:

## <a name="cmpivot-changes-for-version-2006"></a><a name="bkmk_2006"></a> 2006 sürümü için CMPivot değişiklikleri
<!--6518631-->

Sürüm 2006 ' den başlayarak, CMPivot için aşağıdaki iyileştirmeler yapılmıştır:

- Yönetici konsolundan başlatılan [CMPivot tek başına](cmpivot.md#bkmk_standalone) ve CMPivot, yakınsama. Yönetici konsolundan CMPivot başlattığınızda, size senaryo eşliği sağlamak için aynı temel teknolojiyi CMPivot tek başına teknolojisini kullanır.

- CMPivot ' de klavye gezintisi geliştirmeleri.

- Bir cihaz koleksiyonu seçmek zorunda kalmadan, Cihazlar düğümünden tek bir cihazdan veya birden fazla cihazdan CMPivot çalıştırabilirsiniz. Bu geliştirme, yardım masası gibi çalışan kişilerin, önceden oluşturulmuş bir koleksiyon dışında belirli cihazlar için CMPivot sorguları oluşturmasını kolaylaştırır.
   - Bir cihaz koleksiyonundaki tek bir cihazı veya çoklu seçim cihazlarını seçin veya **Başlat CMPivot**' ı seçin.

- Bir sorgu listesi görünümünde cihazları döndürürken, bir veya daha fazla cihazda **cihaz Özeti** ' ni seçip daha sonra detaya gitmek için bu cihazlarda Özet ve sorgu yapabilirsiniz. Bu değişiklik, özgün koleksiyondan daha büyük cihaz kümesini sorgulamadan detaya gitmeyi sağlar. **Pivot olarak**bulunan **cihaz Özeti** .
   - Mevcut bir CMPivot işlemi içinde, tek bir cihaz seçin veya çıktısından çok sayıda cihaz seçin. Sağ tıklayıp **cihaz Özeti** seçeneğini kullanarak pivot. Bu eylem yalnızca seçtiğiniz cihazlara kapsamlı ayrı bir CMPivot örneği başlatır. Bu, özetlemeyi kolaylaştırır ve yalnızca bir koleksiyon oluşturmaya gerek kalmadan istenen cihazlarda sorgulama yapar.

- Tek bir cihaz için CMPivot çalıştırdığınızda cihaz adı pencerenin en üstünde listelenir. Birden çok cihaz için, seçilen cihazların sayısı pencerenin en üstünde listelenir.
- Sorgu Özeti sekmesindeki **koleksiyon oluştur** seçeneği, CMPivot artık bir koleksiyona yönelik sorgu sorgulaması gerektirdiğinden kaldırılmıştır. Yalnızca sorgulamak istediğiniz cihazlara bir CMPivot kapsamına sahip yeni bir örnek açmak için bir **cihaz Özeti** gerçekleştirin. **Koleksiyon oluştur** ana menüde hala kullanılabilir.

![CMPivot kullanarak birden çok cihaz için cihaz Özeti](./media/6518631-cmpivot-multi-select.png)


## <a name="cmpivot-changes-for-version-2002"></a><a name="bkmk_2002"></a> 2002 sürümü için CMPivot değişiklikleri
<!--5870934-->
CMPivot varlıklarından gezinmeyi kolaylaştırdık. Configuration Manager sürüm 2002 ' den başlayarak CMPivot varlıklarda arama yapabilirsiniz. Varlıkları ve varlık nesne türlerini kolayca ayırt etmek için de yeni simgeler eklenmiştir.

![CMPivot varlıklarını arama](./media/5870934-search-cmpivot-entities.png)


## <a name="cmpivot-changes-for-version-1910"></a><a name="bkmk_cmpivot1910"></a> 1910 sürümü için CMPivot değişiklikleri
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


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a> CMPivot altyapısına iyileştirmeler
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

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent ( \<logname> , [ \<timespan> ])

Bu varlık olay günlüklerinden ve olay izleme günlük dosyalarından olayları almak için kullanılır. Varlık, Windows olay günlüğü teknolojisi tarafından oluşturulan olay günlüklerinden verileri alır. Varlık Ayrıca, Windows için olay Izleme tarafından oluşturulan günlük dosyalarındaki olayları alır (ETW). WinEvent, son 24 saat içinde varsayılan olarak gerçekleşen olaylara bakar. Ancak, 24 saatlik varsayılan değer bir TimeSpan eklenerek geçersiz kılınabilir.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> FileContent ( \<filename> )

Dosya Içeriği, bir metin dosyasının içeriğini almak için kullanılır.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule ( \<processname> )  

Bu varlık, belirli bir işlem tarafından yüklenen modülleri (dll 'ler) numaralandırmak için kullanılır. ProcessModule, meşru işlemlerde gizlemekte olan kötü amaçlı yazılımlara yönelik arama yaparken yararlıdır.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a> AadStatus

Bu varlık, bir cihazdan geçerli Azure Active Directory kimlik bilgilerini almak için kullanılabilir.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a> EPStatus

EPStatus, bilgisayarda yüklü olan kötü amaçlı yazılımdan koruma yazılımının durumunu almak için kullanılır.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a> CMPivot tek başına kullanarak yerel cihaz sorgusu değerlendirmesi
<!--3197353-->
Configuration Manager konsolunun dışında CMPivot kullanırken, Configuration Manager altyapısına gerek duymadan yalnızca yerel cihazı sorgulayabilirsiniz. Artık yerel cihazdaki WMI bilgilerini hızlıca görüntülemek için CMPivot Azure Log Analytics sorgularından yararlanabilirsiniz. Bu Ayrıca, daha büyük bir ortamda çalıştırılmadan önce CMPivot sorgularının doğrulanmasını ve yeniden kullanılmasını da mümkün bir şekilde sunar. CMPivot tek başına yalnızca Ingilizce olarak kullanılabilir. Tek başına CMPivot hakkında daha fazla bilgi için bkz. [tek başına CMPivot](#bkmk_standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Yerel aygıt sorgu değerlendirmesi için bilinen sorunlar

 - **Bu bilgisayarda** , KILITLI bir WMI sınıfı gibi erişiminiz olmayan bir WMI varlığı için sorgulama yaparsanız, CMPivot 'de bir kilitlenme görebilirsiniz. Bu varlıkları sorgulamak için yükseltilmiş ayrıcalıklara sahip bir hesabı kullanarak CMPivot çalıştırın. <!--5753242-->
- **Bu bılgısayarda**WMI olmayan varlıkları Sorguladıysanız **geçersiz bir ad alanı** veya belirsiz bir özel durum görürsünüz.
- Doğrudan yürütülebilir dosyanın yolundan değil, Başlat menüsü kısayolundan CMPivot tek başına Çalıştır. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> Diğer geliştirmeler

- Yeni işleci kullanarak normal ifade türü sorguları yapabilirsiniz `like` . Örneğin:<!--3056858-->
  
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
    > Bu bağlantının çalışması için [tek başına CMPivot 'yi yükleme](#bkmk_standalone).

- Sorgu sonuçlarında, cihaz Microsoft Defender Gelişmiş tehdit koruması (ATP) ' ye kaydedildiyse, **Microsoft Defender Güvenlik Merkezi** çevrimiçi portalı ' nı başlatmak için cihaza sağ tıklayın.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>1910 sürümündeki CMPivot için bilinen sorunlar

- Sınıra ulaşıldığında en fazla sonuç başlığı görüntülenmeyebilir. <!--5431427-->
  - Her istemci, sorgu başına 128 KB değer ile sınırlıdır.
  - Sorgunun sonuçları 128 KB 'yi aşarsa sonuçlar kesilebilir.

## <a name="cmpivot-changes-for-version-1906"></a><a name="bkmk_cmpivot1906"></a> 1906 sürümü için CMPivot değişiklikleri

Sürüm 1906 ' den başlayarak, şu öğeler CMPivot 'ye eklenmiştir:

- [Birleşimler, ek işleçler ve toplayıcısını değiştirme](#bkmk_cmpivot_joins)
- [Güvenlik Yöneticisi rolüne CMPivot izinleri eklendi](#bkmk_cmpivot_secadmin1906)
- [Tek başına CMPivot](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a> CMPivot içinde birleştirmeler, ek işleçler ve aggregekleyin
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

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a> Örnekler

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

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a> Güvenlik Yöneticisi rolüne CMPivot izinleri eklendi
<!--4683130-->

Sürüm 1906 ' den başlayarak, Configuration Manager yerleşik **Güvenlik Yöneticisi** rolüne aşağıdaki izinler eklenmiştir:

 - SMS komut dosyasında **Oku**
 - Koleksiyonda **CMPivot Çalıştır**
 - Envanter raporunda **Oku**

>[!NOTE]
> **Çalıştırma betikleri** , **Run CMPivot** izninin bir süper kümesidir.

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> Tek başına CMPivot

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)] 

## <a name="cmpivot-changes-for-version-1902"></a><a name="bkmk_cmpivot1902"></a> 1902 sürümü için CMPivot değişiklikleri
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
1. SPN 'nin CAS SQL dinleyicisi adı ve her birincil SQL dinleyicisi adı için [yayımlandığından](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover#SPNs) emin olun.
1. Birincil SQL sunucularını yeniden başlatın.
1. CAS site sunucusunu ve CAS SQL sunucularını yeniden başlatın.


## <a name="cmpivot-changes-for-version-1810"></a><a name="bkmk_cmpivot"></a> 1810 sürümü için CMPivot değişiklikleri
<!--1359068, 3607759-->

CMPivot, Configuration Manager sürüm 1810 ' den başlayarak aşağıdaki geliştirmeleri içerir:

- [CMPivot yardımcı programı ve performansı](#bkmk_cmpivot-perf)
- [Skaler işlevler](#bkmk_cmpivot-functions)  
- [Görselleştirmeler işleniyor](#bkmk_cmpivot-charts)  
- [Donanım envanteri](#bkmk_cmpivot-hinv)  
- [Skaler işleçler](#bkmk_cmpivot-operators)  
- [Sorgu Özeti](#bkmk_cmpivot-summary)  
- [Denetim durumu iletileri](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a> CMPivot yardımcı programı ve performansı

- CMPivot, 20.000 satır yerine 100.000 hücre döndürür.
  - Varlığın 5 özelliği varsa, anlamı 5 sütun, en fazla 20.000 satır gösterilir.
  - 10 özelliklerine sahip bir varlık için en fazla 10.000 satır gösterilir.
  - Gösterilen toplam veri 100.000 hücreden küçük veya buna eşit olacaktır.
- Sorgu Özeti sekmesinde, başarısız veya çevrimdışı cihazların sayısını seçin ve ardından **koleksiyon oluşturma**seçeneğini belirleyin. Bu seçenek, bu cihazların bir düzeltme dağıtımı ile hedeflemesini kolaylaştırır.
   - Bu seçenek, CMPivot artık bir koleksiyonun sorgulanmasını gerektirdiğinden, sürüm 2006 ' den kaldırılmıştır.
- Klasör simgesine tıklayarak **sık kullanılan** sorguları kaydedin.
   ![CMPivot içinde sık kullanılan bir sorgu kaydetme örneği](media/cmpivot-favorite.png)

- İstemciler, hızlı bir iletişim kanalı üzerinden siteye 80 KB 'tan daha az 1810 sürümüne güncelleştirilmiş bir bağlantı verir.
  - Bu değişiklik, betik veya sorgu çıkışını görüntüleme performansını artırır.
  - Betik veya sorgu çıkışı 80 KB 'tan büyükse, istemci verileri bir durum iletisi aracılığıyla gönderir.
  - İstemci, 1810 istemci sürümüne güncelleştirilmemiş durum iletilerini kullanmaya devam eder.

- CMPivot ' i başlattığınızda şu hatayı görebilirsiniz:  **uyumsuz bir betik sürümü nedeniyle, şu anda CMPivot 'yi kullanamazsınız. Bu sorun, hiyerarşinin bir siteyi yükseltme sürecinde olması olabilir. Yükseltme tamamlanana kadar bekleyip yeniden deneyin.**

  - Bu iletiyi görürseniz, bunun anlamı:
    - Güvenlik kapsamı düzgün ayarlanmadı.
    - İşlemde yükseltmeyle ilgili sorunlar var.
    - Temel alınan CMPivot betiği uyumsuz.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a> Skaler işlevler
CMPivot Aşağıdaki skaler işlevleri destekler:
- **önce ()**: verilen TimeSpan DEĞERI geçerli UTC saat zamanından çıkartır  
- **datetime_diff ()**: iki tarih saat değeri arasındaki takvim farkını hesaplar  
- **Now ()**: geçerli UTC saat saatini döndürür  
- **bin ()**: değerleri, belirli bir bin boyutunun bir tam sayıya yuvarlar  

> [!Note]  
> Tarih saat veri türü, genellikle günün tarih ve saati olarak ifade edilen bir anlık zamanı temsil eder. Zaman değerleri 1 saniyelik birimlerde ölçülür. Tarih saat değeri her zaman UTC saat dilimlidir. ISO 8601 biçiminde her zaman Express tarih zaman rakamları, örneğin `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Örnekler
- `datetime(2015-12-31 23:59:59.9)`: Belirli bir tarih saat değişmez değeri   
- `now()`: Geçerli saat  
- `ago(1d)`: Geçerli saat eksi bir gün  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a> Görselleştirmeler işleniyor

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


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a> Donanım envanteri
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


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a> Skaler işleçler
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
|contains|RHS bir LHS alt sırası olarak gerçekleşir|`"FabriKam" contains "BRik"`|
|! Contains|LHS 'te RHS gerçekleşmiyor|`"Fabrikam" !contains "xyz"`|
|StartsWith|RHS bir başlangıç alt dizisi olan LHS|`"Fabrikam" startswith "fab"`|
|! StartsWith|RHS, LHS 'in bir başlangıç alt dizisi değildir|`"Fabrikam" !startswith "kam"`|
|EndsWith|RHS, LHS 'in bir kapanış alt sırasıdır|`"Fabrikam" endswith "Kam"`|
|! EndsWith|RHS, LHS 'in bir kapanış alt dizisi değildir|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a> Sorgu Özeti

CMPivot penceresinin alt kısmındaki **Sorgu Özeti** sekmesini seçin. Bu durum, çevrimdışı olan istemcileri tanımlamanızı veya oluşabilecek hataların sorunlarını gidermenize yardımcı olur. Bu duruma sahip belirli cihazların bir listesini açmak için say sütununda bir değer seçin. 

Örneğin, hata durumundaki cihaz sayısını seçin. Belirli bir hata iletisine bakın ve bu cihazların listesini dışarı aktarın. Hata belirli bir cmdlet 'in tanınmıyorsa, bir Windows PowerShell güncelleştirmesi dağıtmak için, dışarıya aktarılmış cihaz listesinden bir koleksiyon oluşturun.  

### <a name="cmpivot-audit-status-messages"></a>CMPivot denetim durumu iletileri

Sürüm 1810 ' den başlayarak, CMPivot çalıştırdığınızda **messageıd 40805**ile bir denetim durumu iletisi oluşturulur. Durum iletilerini **izleme**  >  **sistem durumu**  >  **durum iletisi sorguları**' na giderek görüntüleyebilirsiniz. Belirli **bir Kullanıcı Için tüm denetim durum iletilerini**, **belirli bir site için tüm denetim durum iletilerini**çalıştırabilir veya kendi durum iletisi sorgunuzu oluşturabilirsiniz.

İleti için aşağıdaki biçim kullanılır:

MessageID 40805: Kullanıcı &lt; Kullanıcı adı> komut dosyası &lt; betiği çalıştı-Guid> karma &lt; betiği- &lt; kimliği> toplama>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14, CMPivot için komut dosyası GUID 'Sidir.
- Betik karması, istemcinin betikleri. log dosyasında görülebilir.
- İstemcinin komut dosyası deposunda depolanan karmayı da görebilirsiniz. İstemcideki dosya adı &lt; komut dosyası-guıd>_ &lt; betik-karma>.
    - Örnek dosya adı: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123. PS
   

![CMPivot Audit durum iletisi örneği](media/cmpivot-audit-status-message.png)

## <a name="next-steps"></a>Sonraki adımlar
 
[CMPivot sorunlarını giderme](cmpivot-tsg.md)
