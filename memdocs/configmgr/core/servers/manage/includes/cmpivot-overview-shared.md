---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 8e95fce122a3e153f2aa391dcd5e40439f8e5820
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703544"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>Sorgular

Sorgular terimleri aramak, eğilimleri belirlemek, desenleri analiz etmek ve verilerinize göre birçok diğer öngörü sağlamak için kullanılabilir. CMPivot tablosal ifadesi deyimi için [Azure Log Analytics](/azure/kusto/query) veri akışı modelinin bir alt kümesini kullanır. Tablosal ifade deyiminin tipik yapısı, istemci varlıklarının ve tablo veri işleçlerinin (filtreler ve projeksiyonlar gibi) bir kompozisyonlarıdır. Birleşim, dikey çizgi karakteri (|) ile temsil edilir ve bu ifadeye, tablo verilerinin soldan sağa akışını görsel olarak temsil eden normal bir form verir. Her operatör, "kanaldan" tablosal veri kümesini ve işlecin gövdesinden ek girdileri (diğer tablolu veri kümeleri dahil) kabul eder, ardından aşağıdaki bir sonraki işlece bir tablo verisi kümesi yayar: `entity | operator1 | operator2 | ...`

Aşağıdaki örnekte, varlık `CCMRecentlyUsedApplications` (son kullanılan uygulamalara bir başvurudur) ve işleci ise (kayıt başına bazı koşula göre kayıtları filtreleyerek kaydedilir):

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>Varlıklar

Varlıklar, istemciden sorgulanabilen nesnelerdir. Şu anda şu varlıkları destekliyoruz:


|Varlık|Açıklama|
|---|---|
|AadStatus|Azure Active Directory durumu|
|Yöneticiler|Yerel Yöneticiler grubunun üyeleri|
|AppCrash|En son uygulama kilitlenme raporları|
|AppVClientApplication|AppV Istemci uygulaması|
|AppVClientPackage|AppV Istemci paketi|
|Oto yazılım|İşletim sistemi ile otomatik olarak veya hemen sonrasında başlayan yazılımlar|
|Kart|Kart|
|Pil|Pil|
|'Taki|Sistem BIOS bilgileri|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|BitLocker şifreleme ayrıntıları|
|BitLockerPolicy|BitLocker Ilkesi|
|BootConfiguration|Önyükleme yapılandırması|
|BrowserHelperObject|Tarayıcı Yardımcısı nesnesi|
|BrowserUsage|Tarayıcı kullanımı|
|CcmLog ()|Bir CCM günlük dosyasından 24 saat içindeki satırlar (varsayılan olarak)|
|CCMRAYX|CCM_RAX|
|CCMRecentlyUsedApplications|Son kullanılan uygulamalar|
|Ccmwebappınstallinınfo|Web Uygulamaları|
|ROM|CDROM sürücüsü|
|ClientEvents|İstemci olayları|
|ComputerSystem|Bilgisayar Sistemi|
|ComputerSystemEx|Bilgisayar sistemi EX|
|ComputerSystemProduct|Bilgisayar Sistemi Ürünü|
|ConnectedDevice|Bağlı cihaz|
|Bağlantı|Cihazın içinde veya dışında etkin bir TCP bağlantısı|
|Masaüstü|Masaüstü|
|DesktopMonitor|Masaüstü Izleyicisi|
|Cihaz|Cihazla ilgili temel bilgiler|
|Disk|Windows çalıştıran bir bilgisayar sistemindeki yerel depolama cihazı bilgileri|
|DMA|DMA|
|DMA kanalı|DMA kanalı|
|DriverVxD|Sürücü-VxD|
|Embeddeddeviceınformation|Katıştırılmış cihaz bilgileri|
|Ortam|Ortam|
|EPStatus|Bilgisayardaki kötü amaçlı yazılımdan koruma yazılımının durumu|
|EventLog ()|Bir olay günlüğünden 24 saat içindeki olaylar (varsayılan olarak)|
|Dosya ()|Belirli bir dosya hakkında bilgi|
|Dosya Paylaşımı|Etkin dosya paylaşma bilgileri|
|Üretici yazılımı|Üretici yazılımı|
|Idecontroller|IDE denetleyicisi|
|Instaltadexecutable|Yüklenen yürütülebilir|
|Instalınstalsoftware|Cihaza yüklenmiş bir uygulama|
|Komutunu|Kullanılabilir arabirimler, IP adresleri ve DNS sunucuları dahil ağ yapılandırmasını alır|
|Irqtable|IRQ Tablosu|
|Klavye|Klavye|
|LoadOrderGroup|Yükleme sırası grubu|
|MantıksalDisk|Mantıksal disk|
|MDMDevDetail|Cihaz Bilgileri|
|Bellek|Bellek|
|Modemi|Modemi|
|Kartı|Kartı|
|NetworkAdapter|Ağ bağdaştırıcısı|
|NetworkAdapterConfiguration|Ağ bağdaştırıcısı yapılandırması|
|NetworkClient|Ağ Istemcisi|
|NetworkLoginProfile|Ağ oturum açma profili|
|NTEventlogFile|NT EventLog dosyası|
|Office365ProPlusConfigurations|Office 365 ProPlus yapılandırması|
|Officeeklentisi|Office eklentileri|
|OfficeClientMetric|Office Istemci ölçümü|
|OfficeDeviceSummary|Office cihaz Özeti|
|OfficeDocumentMetric|Office belge ölçümleri|
|OfficeDocumentSolution|Office belge çözümü|
|Officemakrohatası|Office makro hatası|
|Officeproductınfo|Office ürün bilgileri|
|Officevbarulet Ihlali|Office VBA kural Ihlali|
|Officeveli|Office VBA tarama Özeti|
|OperatingSystem|İşletim Sistemi|
|OperatingSystemEx|İşletim sistemi EX|
|OperatingSystemRecoveryConfiguration|İşletim sistemi kurtarma yapılandırması|
|OptionalFeature|İsteğe bağlı özellik|
|İşletim Sistemi|İşletim sistemiyle ilgili temel bilgiler|
|Pagesetting ayarı|Sayfa dosyası ayarı|
|Paralellport|Paralel bağlantı noktası|
|Bölüm|Disk bölümleri|
|PCMCIAController|PCMCIA denetleyicisi|
|Fiziksel|Fiziksel|
|PhysicalMemory|Fiziksel Bellek|
|PNPDEVICEDRIVER|PNP cihaz sürücüsü|
|PointingDevice|İşaret eden cihaz|
|Portablepili|Taşınabilir pil|
|Bağlantı noktaları|Bağlantı noktaları|
|PowerCapabilities|Güç özellikleri|
|PowerClientOptOutSettings|Güç yönetimi dışlama ayarları|
|PowerConfigurations|Güç yapılandırması|
|Her gün PowerManagement|Güç yönetimi günlük verileri|
|Powermanagementinsomniareadönemleri|Power Insomnia Nedenleri|
|PowerManagementMonthly|Güç yönetimi aylık verileri|
|PowerSettings|Güç ayarları|
|Yazıcıyapılandırma|Yazıcı yapılandırması|
|PrinterDevice|Yazıcı cihazı|
|PrintJobs|Yazdırma Işleri|
|İşlem|İşletim sisteminde bir işlem|
|ProcessModule ()|Belirtilen süreçler tarafından yüklenen modüller|
|İşlemci|İşlemci|
|Protectedvolumeınformation|Korumalı birim bilgileri|
|Protokol|Protokol|
|QuickFixEngineering|Hızlı düzelme Mühendisliği|
|SCSIController|SCSI denetleyicisi|
|SerialPortConfiguration|Seri bağlantı noktası yapılandırması|
|Seri bağlantı noktaları|Seri bağlantı noktaları|
|ServerFeature|Sunucu Özelliği|
|Hizmet|Windows çalıştıran bir bilgisayar sisteminde bir hizmet|
|Hizmetler|Hizmetler|
|Paylaşımlar|Paylaşımlar|
|SMBConfig|Bir cihazın SMB yapılandırması|
|SMSAdvancedClientPorts|Configuration Manager Istemci bağlantı noktaları|
|SMSAdvancedClientSSLConfigurations|Configuration Manager Istemci SSL yapılandırması|
|SMSAdvancedClientState|Configuration Manager Istemci durumu|
|SMSDefaultBrowser|Varsayılan tarayıcı|
|SMSSoftwareTag|Yazılım etiketi|
|SMSWindows8Application|Windows uygulaması|
|SMSWindows8ApplicationUserInfo|Windows uygulaması Kullanıcı bilgisi|
|SoftwareShortcut|Yazılım kısayolu|
|SoftwareUpdate|Bir yazılım güncelleştirmesi uygulanabilir ancak cihazda yüklü değil|
|SoundDevices cihazları|Ses cihazları|
|SWLicensingProduct|Yazılım lisanslama ürünü|
|SWLicensingService|Yazılım Lisanslama hizmeti|
|SystemAccount|Sistem Hesabı|
|SystemBootData|Sistem önyükleme verileri|
|SystemBootSummary|Sistem önyükleme Özeti|
|SystemConsoleUsage|Sistem konsolu kullanımı|
|SystemConsoleUser|Sistem konsolu kullanıcısı|
|SystemDevices|Sistem cihazları|
|SystemDrivers|Sistem sürücüleri|
|Systemenkapanış|Sistem Kutusu|
|TapeDrive|Bant sürücüsü|
|TimeZone|Saat Dilimi|
|TPM|TPM|
|TPMStatus|TPM durumu|
|Tsıssuedlicense|TS verilen lisans|
|TSLicenseKeyPack|TS lisans anahtarı paketi|
|Kesintisiz güç kaynağı|Kesintisiz güç kaynağı|
|USBController|USB denetleyicisi|
|USBDevice|USB cihazı|
|Kullanıcı|Cihaza etkin bağlantısı olan bir kullanıcı hesabı|
|USMFolderRedirectionHealth|Klasör yeniden yönlendirme sistem durumu|
|USMUserProfile|Kullanıcı profili sistem durumu|
|VideoController|Video denetleyicisi|
|VirtualMachine|Sanal Makine|
|VirtualMachine64|Sanal makine (64)|
|Birim|Birim|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Windows Update Aracısı sürümü|
|WinEvent ()|Bir Windows olay günlüğünden 24 saat içindeki olaylar (varsayılan olarak)|
|WriteFilterState|Filtre durumunu yaz|

## <a name="table-operators"></a>Tablo işleçleri

Tablo işleçleri, veri akışlarını filtrelemek, özetlemek ve dönüştürmek için kullanılabilir. Şu anda aşağıdaki işleçler desteklenir:

|Tablo işleçleri|Açıklama|
|---|---|
|count|Kayıt sayısını içeren tek bir kayıt içeren bir tablo döndürür|
|distinct|Giriş tablosunun belirtilen sütunlarının ayrı bir birleşimini içeren bir tablo oluşturur|
|join|Aynı cihazla eşleşen satıra göre yeni bir tablo oluşturmak için iki tablo satırını birleştirin|
|sıralama ölçütü|Giriş tablosunun satırlarını bir veya daha fazla sütuna göre sıraya göre sırala|
|proje|Dahil edilecek, yeniden adlandırılacak veya bırakılacak sütunları seçin ve yeni hesaplanmış sütunları ekleyin|
|ölçütü|Giriş tablosunun içeriğini toplayan bir tablo oluşturur|
|take|Belirtilen sayıda satıra dön|
|top|Belirtilen sütunlara göre sıralanan ilk N kaydı döndürür|
|where|Bir tabloyu bir koşula uyan satır alt kümesiyle filtreler|

## <a name="scalar-operators"></a>Skaler Işleçler

Aşağıdaki tabloda işleçler özetlenmektedir:

|İşleçler|Açıklama|Örnek
|---|---|---|
|==|Eşittir|`1 == 1, 'aBc' == 'AbC'`|
|!=|Eşit değildir|`1 != 2, 'abc' != 'abcd'`|
|< |Büyüktür|`1 < 2, 'abc' < 'DEF'`|
|> |İlerisi|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Daha az veya eşit|`1 <= 2, 'abc' <= 'abc'`|
|>=|Daha büyük veya eşit|`2 >= 1, 'abc' >= 'ABC'`|
|+|Ekle|`2 + 1, now() + 1d`|
|-|Çıkar|`2 - 1, now() - 1h`|
|*|Çarp|`2 * 2`|
|/|Böl|`2 / 1`|
|%|Mod|`2 % 1`|
|Like|Sol taraftaki (LHS) sağ taraftaki (RHS) bir eşleşme içerir|`'abc' like '%B%'`|
|! Beğen|LHS, RHS için eşleşme içermiyor|`'abc' !like '_d_'`|
|contains|RHS bir LHS alt sırası olarak gerçekleşir|`'abc' contains 'b'`|
|! Contains|LHS 'te RHS gerçekleşmiyor|`'team' !contains 'i'`|
|StartsWith|RHS bir başlangıç alt dizisi olan LHS|`'team' startswith 'tea'`|
|! StartsWith|RHS, LHS 'in bir başlangıç alt dizisi değildir|`'abc' !startswith 'bc'`|
|EndsWith|RHS, LHS 'in bir kapanış alt sırasıdır|`'abc' endswith 'bc'`|
|! EndsWith|RHS, LHS 'in bir kapanış alt dizisi değildir|`'abc' !endswith 'a'`|
|ve|Yalnızca RHS ve LHS true ise doğru|`(1 == 1) and (2 == 2)`|
|veya|Yalnızca RHS veya LHS true ise doğru|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>Toplama işlevleri

Toplama işlevleri, Özet Tablo işleci ile hesaplanan özetlenen değerler ile kullanılabilir. Şu anda aşağıdaki toplama işlevleri desteklenir:

|İşlev|Açıklama|
|---|---|
|avg()|Grup genelindeki değerlerin ortalamasını döndürür|
|count()|Özetleme grubu başına kayıt sayısını döndürür|
|countif()|Koşulun true olarak değerlendirildiği satır sayısını döndürür|
|dcount()|Gruptaki ayrı değerlerin sayısını döndürür|
|max()|Grup genelindeki en büyük değeri döndürür|
|min()|Grup genelindeki en küçük değeri döndürür|
|yüzdebirlik ()|Ifadenin belirttiği popülasyon için belirtilen en yakın derecelendirme yüzdelik değeri için bir tahmin döndürür|
|sum()|Grup genelindeki değerlerin toplamını döndürür|
|sumif()|Koşulun true olarak değerlendirilen bir Ifade toplamı döndürür|

## <a name="scalar-functions"></a>Skaler işlevler

Skaler işlevler ifadelerde kullanılabilir. Şu anda aşağıdaki skaler işlevler desteklenir:

|İşlev|Açıklama|
|---|---|
|ago()|Verilen TimeSpan değeri geçerli UTC saat zamanından çıkartır|
|bin()|Değerleri, belirli bir bin boyutunun bir tarih/saatteki bir sayısına yuvarlar|
|case()|Koşulların bir listesini değerlendirir ve koşulu karşılanan ilk sonuç ifadesini döndürür|
|datetime_add()|Belirtilen bir tarih saat değerine eklenen belirtilen bir datepart 'ın yeni bir tarih/saat değerini belirtilen miktarda hesaplar|
|datetime_diff()|İki tarih saat değeri arasındaki farkı hesaplar|
|iif()|İlk bağımsız değişkeni değerlendirir ve koşulun doğru (ikinci) ya da yanlış (üçüncü) olarak değerlendirildiğine bağlı olarak ikinci veya üçüncü bağımsız değişkenlerin değerini döndürür|
|indexof()|İşlev, giriş dizesinde belirtilen bir dizenin ilk oluşumunun sıfır tabanlı dizinini bildirir|
|isnotnull ()|Tek bağımsız değişkenini değerlendirir ve bağımsız değişkenin null olmayan bir değer olarak değerlendirilip değerlendirilmediğini gösteren bir Boole değeri döndürür|
|isnull()|Tek bağımsız değişkenini değerlendirir ve bağımsız değişkenin null değer olarak değerlendirilip değerlendirilmediğini gösteren bir Boole değeri döndürür|
|now()|Geçerli UTC saat saatini döndürür|
|strcat()|1 ile 64 arasında bağımsız değişken arasına ekler|
|strlen()|Giriş dizesinin karakter cinsinden uzunluğunu döndürür|
|substring()|Bir kaynak dizeden, dizenin sonuna kadar bir dizinden başlayarak bir alt dize ayıklar|
|tostring()|Girişi dize gösterimine dönüştürür|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Configuration Manager 'den CMPivot için ek varlıklar, işleçler ve işlevler

> [!Important]
> Microsoft Endpoint Manager Yönetim Merkezi 'nden CMPivot çalıştırdığınızda bu öğeler desteklenmez.

|Tür|Öğe|Açıklama|
|--|--|---|
|Varlık|AccountSID|Hesap SID'si|
|Varlık|FileContent ()|Belirli bir dosyanın içeriği|
|Varlık|NAPClient|NAP Istemcisi|
|Varlık|NAPSystemHealthAgent|NAP sistem durumu Aracısı|
|Varlık|Kayıt defteri ()|Belirli bir kayıt defteri anahtarı için tüm değerler<!--7371183-->|
|Table işleci|işlenecek|Sonuçları grafik çıkış olarak işler|