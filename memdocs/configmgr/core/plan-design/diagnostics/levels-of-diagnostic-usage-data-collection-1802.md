---
title: 1802 için tanılama ve kullanım verileri
titleSuffix: Configuration Manager
description: Sürüm 1802 ' de toplanan tanılama ve kullanım verilerinin düzeyleri hakkında bilgi edinin.
ms.date: 05/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 29dd51b8-6576-4010-81ba-3129ed2c3421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c2edff394e915273fb34f4627e3636ea6e20237c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710877"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1802-of-configuration-manager"></a>Configuration Manager sürüm 1802 için tanılama kullanım verileri toplama düzeyleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager sürüm 1802, üç düzeyde tanılama ve kullanım verisi toplar: **temel**, **Gelişmiş**ve **tam**. Varsayılan olarak, bu özellik Gelişmiş düzeye ayarlanmıştır. Aşağıdaki bölümler her düzeyde toplanan veriler hakkında ek ayrıntılar sağlar.

Önceki sürümlerden yapılan değişiklikler ***[yeni]***, ***[güncelleştirildi]***, ***[kaldırıldı]*** veya ***[taşındı]*** ile belirtilmiştir.


> [!IMPORTANT]
>  Configuration Manager, temel veya gelişmiş düzeylerde site kodlarını, site adlarını, IP adreslerini, Kullanıcı adlarını, bilgisayar adlarını, fiziksel adresleri ya da e-posta adreslerini toplamaz. Bu bilgilerin tam düzeyinde toplanması herhangi bir amaca bağlı değildir. Büyük olasılıkla günlük dosyaları veya bellek anlık görüntüleri gibi gelişmiş tanılama bilgilerine dahildir. Microsoft bu bilgileri sizi tanımlamak, sizinle iletişim kurmak veya reklam geliştirmek için kullanmaz.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Düzeyi değiştirme
 **Site** nesne sınıfında **değiştirme** izinlerini içeren rol tabanlı yönetim kapsamına sahip yöneticiler, Configuration Manager konsolundaki tanılama ve kullanım verileri ayarlarında toplanan veri düzeyini değiştirebilir.

**Yönetim** > **genel bakış** > **site yapılandırma** > **siteleri**' ne giderek veri toplama düzeyini konsolunun içinden değiştirirsiniz. **Hiyerarşi ayarları**' nı açın ve ardından kullanmak istediğiniz veri düzeyini seçin.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Düzey 1 - Temel
Temel düzey, hiyerarşiniz hakkındaki verileri, yüklemenizin veya yükseltme deneyiminizin artırılmasına yardımcı olması gereken verileri ve hiyerarşiniz için geçerli Configuration Manager güncelleştirmelerinin belirlenmesine yardımcı olan verileri içerir.

Configuration Manager sürüm 1802 için, bu düzey aşağıdaki verileri içerir:

- Configuration Manager konsol bağlantılarıyla ilgili istatistikler: işletim sistemi sürümü, dil, SKU ve mimari, sistem belleği, mantıksal işlemci sayısı, bağlantı site KIMLIĞI, yüklü .NET sürümleri ve konsol dil paketleri

- Temel uygulama ve dağıtım türü sayıları: Toplam uygulama, birden çok dağıtım türüne sahip toplam uygulama, bağımlılıklara sahip toplam uygulama, yenisiyle değiştirilen Toplam uygulama sayısı ve kullanımdaki dağıtım teknolojilerinin sayısı

- Temel Configuration Manager site hiyerarşisi verileri: site listesi, türü, sürümü, durumu, istemci sayısı ve saat dilimi

- Temel veritabanı yapılandırması: işlemciler, küme yapılandırması ve dağıtılmış görünümlerin yapılandırması

- Temel bulma İstatistikleri: bulma sayısı, en düşük/en yüksek/ortalama Grup boyutları ve site tamamen Azure Active Directory hizmetleriyle çalışırken

- Kötü amaçlı yazılımdan koruma istemci sürümleri hakkında temel Endpoint Protection bilgileri

- Temel işletim sistemi dağıtım görüntülerinin sayısı

- Temel site sistemi sunucusu bilgileri: kullanılan site sistem rolleri, internet ve SSL durumu, işletim sistemi, işlemciler, fiziksel veya sanal makine ve site sunucusu yüksek kullanılabilirliği kullanımı

- Configuration Manager veritabanı şeması (tüm nesne tanımlarının karması)

- Yapılandırılmış telemetri düzeyi, çevrimiçi veya çevrimdışı mod ve hızlı güncelleştirme yapılandırması

- İstemci dillerinin ve yerel ayarların sayısı

- Configuration Manager istemci sürümlerinin, işletim sistemi sürümlerinin ve Office sürümlerinin sayısı

- Exchange Connector tarafından ayarlanan yönetilen cihazlar ve ilkeler için işletim sistemi sayısı

- Dala ve derlemeye göre Windows 10 cihazlarının sayısı

- ***[Taşındı]*** Iş için Windows Update kullanan Windows 10 istemcileri sayısı  

- Veritabanı performans ölçümleri: çoğaltma işleme bilgileri, işlemciye göre en çok depolanan yordamlar SQL Server ve disk kullanımı

- Dağıtım noktası ve yönetim noktası türleri ve temel yapılandırma bilgileri: korumalı, önceden hazırlanan, PXE, çok noktaya yayın, SSL durumu, çekme/eş dağıtım noktaları, MDM etkin ve SSL etkin

- Yönetici Konsolu Özellik sayfaları ve sihirbazları için, uzantıların karma listesi

- Kurulum bilgileri:
     - Yapı, install türü, dil paketleri, etkinleştirdiğiniz Özellikler   

     - Yayın öncesi kullanımı, kurulum medya türü, dal türü

     - Yazılım Güvencesi sona erme tarihi      

     - Güncelleştirme paketi dağıtım durumu ve hataları, İndirme ilerlemesi ve önkoşul hataları 

     - Güncelleştirme hızlı halkası kullanımı

     - Yükseltme sonrası betiği sürümü

- SQL sürümü, hizmet paketi düzeyi, sürüm, harmanlama KIMLIĞI ve karakter kümesi     

- Telemetri İstatistikleri: çalıştırma, çalışma zamanı, hatalar

- Ağ bulmanın etkin veya devre dışı olup olmadığı

- ***[Taşındı]*** Azure Active Directory katılmış istemci sayısı

- ***[Yeni]*** Türe göre oluşturulan aşamalı dağıtım sayısı

- ***[Yeni]*** Genişletilmiş birlikte çalışabilirlik istemcilerinin sayısı

- ***[Yeni]*** 255 karakterden uzun donanım envanteri özelliklerinin karma listesi



##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Düzey 2 - Gelişmiş
Gelişmiş düzey, Kurulum bittikten sonra varsayılandır. Bu düzey, temel düzeyde ve özelliğe özgü veriler (kullanım sıklığı ve süresi), Configuration Manager istemci ayarları (bileşen adı, durumu ve yoklama aralıkları gibi belirli ayarlar) ile yazılım güncelleştirmeleri hakkındaki temel bilgiler içinde toplanan verileri içerir.

Bu düzey, Microsoft 'un, ürün ve hizmetlerin gelecekteki sürümlerinde yararlı geliştirmeler yapmak için gereken en düşük verileri sağladığı için önerilir. Bu düzey, nesne adlarını (siteler, kullanıcılar, bilgisayarlar veya nesneler), güvenlikle ilgili nesnelerin ayrıntılarını veya yazılım güncelleştirmesi gerektiren sistem sayısı gibi güvenlik açıklarını toplamaz.

Configuration Manager sürüm 1802 için, bu düzey aşağıdaki verileri içerir:

### <a name="application-management"></a>Uygulama yönetimi  

- Uygulama gereksinimleri: dağıtım teknolojisi tarafından başvurulan yerleşik koşulların sayısı

- Uygulama yerine geçme, en yüksek zincir derinliği

- Uygulama onay istatistikleri ve kullanım sıklığı

- Uygulama içeriği boyut istatistikleri

- Uygulama dağıtım bilgileri: yükleme ve kaldırma için kullanma, onay, Kullanıcı etkileşimi etkin/devre dışı, bağımlılık, yenisiyle değiştirme ve yükleme davranışı özelliğinin kullanım sayısı  

- Uygulama ilkesi boyutu ve karmaşıklık istatistikleri

- Mevcut uygulama isteği istatistikleri

- Paketler ve programlar için temel yapılandırma bilgileri: dağıtım seçenekleri ve program bayrakları

- Dağıtım türleri için temel kullanım/hedefleme bilgileri: kullanıcıya ve cihaz hedefli, gerekli ve kullanılabilir ve evrensel uygulamalara karşı

- App-V ortamları ve dağıtım özellikleri sayısı

- İşletim sistemine göre uygulama uygulanabilirliği sayısı  

- Bir görev dizisi tarafından başvurulan uygulama sayısı

- Uygulama Kataloğu için farklı marka sayısı

- Pano kullanılarak oluşturulan Office 365 uygulamalarının sayısı

- Türe göre paket sayısı  

- Paket/program dağıtımı sayısı  

- Windows 10 lisanslı uygulama lisansı sayısı  

- İçerik ayarlarını kaldırma Windows Installer dağıtım türü sayısı

- Iş uygulamaları ve eşitleme istatistikleri için Microsoft Store sayısı: özetlenen uygulama türleri, lisanslanmış uygulama durumu ve çevrimiçi ve çevrimdışı lisanslanmış uygulama sayısı  

- Bakım penceresi türü ve süresi  

- Her zaman süresi içinde Kullanıcı/cihaz başına en düşük/en yüksek/ortalama uygulama dağıtımı sayısı

- Dağıtım teknolojisine göre en sık kullanılan uygulama yükleme hatası kodları

- MSI yapılandırma seçenekleri ve sayıları

- Gerekli yazılım dağıtımları için bildirim ile son kullanıcı etkileşimi ile ilgili istatistikler   

- Evrensel veri erişimi kullanımı, oluşturma

- ***[Yeni]*** Toplu Kullanıcı cihaz benzeşimi istatistikleri 

- ***[Yeni]*** Cihaz başına en fazla ve ortalama birincil Kullanıcı


### <a name="client"></a>İstemci  

- Etkin yönetim teknolojisi (AMT) istemci sürümü

- Yıl içinde BIOS yaşı

- Güvenli önyükleme etkin cihazların sayısı

- TPM durumuna göre cihaz sayısı

- İstemci otomatik yükseltme: istemci pilolama ve dışlama kullanımı (genişletilmiş birlikte çalışabilirlik istemcisi) dahil dağıtım yapılandırması

- İstemci önbellek boyutu yapılandırması

- İstemci dağıtımı indirme hataları

- İstemci sistem durumu istatistikleri ve en önemli sorun Özeti

- İstemci bildirim işlemi eylem durumu: her birinin kaç kez çalıştığı, en fazla hedeflenen istemci sayısı ve ortalama başarı oranı

- Kaynak konum türlerinden gelen istemci yüklemelerinin sayısı  

- İstemci yüklemesi hatalarının sayısı  

- Hyper-V veya Azure tarafından sanallaştırılmış cihazların sayısı  

- Yazılım Merkezi eylemlerinin sayısı   

- UEFı özellikli cihazların sayısı

- Dağıtım yöntemi başına istemci ve istemci sayısı için kullanılan dağıtım yöntemleri

- Etkinleştirilmiş istemci aracıları listesi/sayısı  

- Ay içinde işletim sistemi yaşı

- Donanım envanteri sınıfları, yazılım envanteri kuralları ve dosya toplama kuralları sayısı

- Cihaz sistem durumu kanıtlama İstatistikleri: en yaygın hata kodları, şirket içi sunucu sayısı ve çeşitli durumlarda cihaz sayısı

- ***[Yeni]*** Varsayılan tarayıcı olarak cihaz sayısı


### <a name="cloud-services"></a>Cloud Services  

- Azure Active Directory bulma istatistikleri

- Bulut Yönetimi Ağ Geçidi yapılandırma ve kullanım istatistikleri: bölge ve ortam sayısı ve kimlik doğrulama/yetkilendirme istatistikleri

- Configuration Manager bağlı Azure Active Directory uygulama ve hizmet sayısı

- Azure Log Analytics eşitlenen koleksiyonların sayısı

- Upgrade Analytics Bağlayıcısı sayısı

- Azure Log Analytics Cloud Connector 'ın etkin olup olmadığı


### <a name="co-management"></a>Ortak yönetim  
- Ortak yönetimin toplu kullanım istatistikleri: kayıtlı istemci sayısı, ilke alan istemciler, iş yükü durumları, pilot/dışlama koleksiyon boyutları ve kayıt hataları  

- Ortak yönetim kayıt yöntemine göre istemci sayısı  

- Ortak yönetim kaydı için hata istatistikleri  

- Kayıt zamanlaması ve geçmiş istatistikleri  

- Ortak yönetim için uygun istemci sayısı  

- İlişkili Microsoft Intune kiracısı


### <a name="collections"></a>Koleksiyonlar  

- Koleksiyon KIMLIĞI kullanımı (kimlik dışı)

- Koleksiyon değerlendirme İstatistikleri: sorgu süresi, atanan ve atanmamış sayımlar, türe göre sayılar, KIMLIK geçişi ve kural kullanımı

- Dağıtım olmadan Koleksiyonlar


### <a name="compliance-settings"></a>Uyumluluk ayarları  

- Temel yapılandırma temel bilgileri: sayı, dağıtım sayısı ve başvuru sayısı

- Uyumluluk ilkesi hata istatistikleri

- Türe göre yapılandırma öğesi sayısı  

- Düzeltme ayarları da dahil olmak üzere yerleşik ayarlara başvuran dağıtım sayısı  

- Özel ayarlar için oluşturulan kuralların ve dağıtımların sayısı, düzeltme de dahil olmak üzere  

- Dağıtılan Basit Sertifika Kayıt Protokolü (SCEP), VPN, Wi-Fi, sertifika (. pfx) ve uyumluluk ilkesi şablonlarının sayısı

- Platforma göre SCEP sertifikası, VPN, Wi-Fi, sertifika (. pfx) ve uyumluluk ilkesi dağıtımları sayısı

- Iş için Windows Hello ilkesi (oluşturulan, dağıtılmış)


### <a name="content"></a>İçerik  

- ***[Güncelleştirilmiş]*** Sınır grubu istatistikleri: kaç hızlı, kaç tane yavaş, Grup başına sayı ve geri dönüş ilişkisi

- Sınır grubu bilgileri: her bir sınır grubuna atanan sınır ve site sistemi sayısı  

- Sınır grubu ilişkileri ve geri dönüş yapılandırması

- İstemci içeriği indirme istatistikleri

- Türe göre sınır sayısı  

- Eş önbellek istemcisi sayısı, kullanım istatistiği ve kısmi indirme istatistikleri

- Dağıtım Yöneticisi yapılandırma bilgileri: iş parçacıkları, yeniden deneme gecikmesi, yeniden deneme sayısı ve dağıtım noktası ayarlarını çekme  

- Dağıtım noktası yapılandırma bilgileri: dal önbelleğinin ve dağıtım noktası izlemenin kullanımı

- Dağıtım noktası grubu bilgileri: her bir dağıtım noktası grubuna atanan paket ve dağıtım noktası sayısı  


### <a name="endpoint-protection"></a>Uç Nokta Koruma  

- Microsoft Defender Gelişmiş tehdit koruması (ATP) ilkeleri (eski adıyla Windows Defender ATP): ilke sayısı ve ilkelerin dağıtılıp dağıtılmayacağı.

- Endpoint Protection özelliği için yapılandırılmış uyarı sayısı  

- Endpoint Protection panosunda görünmesi için seçilen koleksiyon sayısı  

- Windows Defender Exploit Guard ilkeleri, dağıtımları ve hedeflenen istemciler sayısı

- Dağıtım hatalarını Endpoint Protection, Endpoint Protection İlkesi dağıtımı hata kodlarının sayısı  

- Kötü amaçlı yazılımdan koruma ve Windows Güvenlik Duvarı İlkesi kullanımını Endpoint Protection (gruba atanan benzersiz ilkelerin sayısı)<br /><br /> Bu veriler, ilkede yer alan ayarlarla ilgili herhangi bir bilgi içermez.  


### <a name="migration"></a>Geçiş  

- Geçirilen nesne sayısı (geçiş sihirbazının kullanımı)


### <a name="mobile-device-management-mdm"></a>Mobil cihaz yönetimi (MDM)  

- Verilen mobil cihaz eylemlerinin sayısı: kilitleme, PIN Rest, Temizleme, devre dışı bırakma ve şimdi eşitleme komutları

- Mobil cihaz ilke sayısı  

- Configuration Manager ve Microsoft Intune tarafından yönetilen mobil cihaz sayısı ve nasıl kaydedildikleri (toplu, Kullanıcı tabanlı)  

- Birden çok kayıtlı mobil cihazı olan kullanıcı sayısı  

- Mobil cihaz yoklama zamanlaması ve mobil cihaz iade süresi istatistikleri  


### <a name="microsoft-intune-troubleshooting"></a>Microsoft Intune sorunlarını giderme  

- Microsoft Intune çoğaltılan cihaz eylemlerinin sayısı ve boyutu (silme, devre dışı bırakma, kilitleme), telemetri ve veri iletileri

- Microsoft Intune 'ten indirilen durum, durum, envanter, RDR, DDR, UDX, kiracı durumu, POL, LOG, CERT, CRP, yeniden eşitleme, CFD, RDO, BEX, ıSM ve uyumluluk iletilerinin sayısı ve boyutu

- Microsoft Intune için tam ve Delta Kullanıcı eşitleme istatistikleri


### <a name="on-premises-mobile-device-management-mdm"></a>Şirket içi mobil cihaz yönetimi (MDM)  

- Windows 10 toplu kayıt paketleri ve profillerinin sayısı  

- Şirket içi MDM uygulama dağıtımları için dağıtım başarı/hata istatistikleri  


### <a name="os-deployment"></a>İşletim sistemi dağıtımı  

- Önyükleme görüntüleri, sürücüler, sürücü paketleri, çok noktaya yayını destekleyen dağıtım noktaları, PXE özellikli dağıtım noktaları ve görev dizileri sayısı  

- Configuration Manager istemci sürümüne göre önyükleme görüntülerinin sayısı

- Windows PE sürümüne göre önyükleme görüntülerinin sayısı

- Sürüm yükseltme ilkelerinin sayısı

- PXE 'den dışlanan donanım tanımlayıcılarının sayısı

- İşletim sistemi sürümüne göre işletim sistemi dağıtımı sayısı

- Zaman içinde işletim sistemi yükseltmelerinin sayısı

- İçeriği önceden indirme seçeneğini kullanarak görev dizisi dağıtımları sayısı

- Görev dizisi adım kullanım sayısı

- Windows ADK 'nin yüklü sürümü


### <a name="site-updates"></a>Site güncelleştirmeleri  

- Yüklü Configuration Manager düzeltmelerinin sürümleri


### <a name="software-updates"></a>Yazılım Güncelleştirmeleri  

- Otomatik dağıtım kurallarında kullanılan kullanılabilir ve son tarih değişimleri  

- Güncelleştirme başına ortalama ve en yüksek atama sayısı  

- İstemci güncelleştirme değerlendirmesi ve tarama zaman çizelgeleri  

- Yazılım güncelleştirme noktası tarafından eşitlenen sınıflandırmalar

- Küme düzeltme eki uygulama istatistikleri  

- Windows 10 Express güncelleştirmelerinin yapılandırması

- Etkin Windows 10 bakım planları için kullanılan konfigürasyonlar  

- Dağıtılan Office 365 güncelleştirmeleri sayısı  

- Eşitlenmiş Microsoft Surface sürücü sayısı

- Güncelleştirme grupları ve atamalarının sayısı  

- Güncelleştirme paketi sayısı ve paketlerle hedeflenen dağıtım noktalarının en yüksek/en düşük/ortalama sayısı  

- System Center Update Publisher ile oluşturulan ve dağıtılan güncelleştirmelerin sayısı  

- Oluşturulan ve dağıtılan Iş ilkeleri için Windows Update sayısı

- ***[Yeni]*** Iş yapılandırmalarının Windows Update toplu istatistikleri

- Eşitlemeye bağlı otomatik dağıtım kuralları sayısı  

- Yeni bir grup oluşturan veya mevcut bir gruba güncelleştirme ekleyen otomatik dağıtım kuralları sayısı  

- Birden çok dağıtıma sahip otomatik dağıtım kuralları sayısı  

- Güncelleştirme grubu sayısı ve güncelleştirme grubu başına en düşük/en yüksek/ortalama güncelleştirme sayısı  

- Dağıtılan, zaman aşımına geçilen, yenisiyle değiştirilen, indirilen ve EULA 'Lar içeren güncelleştirmelerin güncelleştirme sayısı ve yüzdesi  

- Yazılım güncelleştirme noktası yük dengeleme istatistikleri

- Yazılım güncelleştirme noktası eşitleme zaman çizelgesi  

- Yazılım güncelleştirme dağıtımları olan koleksiyonların toplam/ortalama sayısı ve dağıtılan güncelleştirmelerin en yüksek/ortalama sayısı  

- Güncelleştirme taraması hata kodları ve makine sayısı  

- Windows 10 panosu içerik sürümleri  


### <a name="sqlperformance-data"></a>SQL/performans verileri  

- Site özetlemesinin yapılandırması ve süresi

- En büyük veritabanı tablolarının sayısı  

- Bulgu işlem istatistikleri (bulunan nesne sayısı)

- Bulma türleri, etkin ve zamanlama (tam, artımlı)

- SQL AlwaysOn çoğaltma bilgileri, kullanımı ve sistem durumu

- SQL değişiklik izleme performansı sorunları, saklama süresi ve otomatik temizleme durumu

- SQL değişiklik izleme tutma süresi

- En yaygın ve en pahalı ileti türlerini içeren durum ve durum iletisi performans istatistikleri


### <a name="miscellaneous"></a>Çeşitli  

- Eşitleme zamanlaması ve ortalama süre dahil olmak üzere veri ambarı hizmet noktası yapılandırması

- Komut dosyası sayısı ve istatistikleri Çalıştır

- LAN'da Uyandırma (WOL) ile site sayısı

- Raporlama kullanımı ve performans istatistikleri

- ***[Yeni]*** Aşamalı dağıtım kullanım istatistikleri



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Düzey 3 - Tam
Tam düzey, temel ve gelişmiş düzeylerdeki tüm verileri içerir. Aynı zamanda Uç Nokta Koruma, güncelleştirme uyumluluğu yüzdeleri ve yazılım güncelleştirme bilgileri hakkında ek bilgiler de içerir. Bu düzey, yakalama sırasında bellekte veya günlük dosyalarında bulunan kişisel bilgileri içerebilen sistem dosyaları ve bellek anlık görüntüleri gibi gelişmiş tanı bilgilerini de içerebilir.

Configuration Manager sürüm 1802 için, bu düzey aşağıdaki verileri içerir:

- Otomatik dağıtım kuralı değerlendirmesi zaman çizelgesi bilgileri

- ATP sistem durumu Özeti

- Koleksiyon değerlendirme ve yenileme istatistikleri

- Uyumluluk ve hatalarda uyumluluk ilkesi istatistikleri

- Uyumluluk ayarları: SCEP, VPN, Wi-Fi ve uyumluluk ilkesi şablonu yapılandırma ayrıntıları

- Configuration Manager kullanımı için DCM yapılandırma paketi

- Ayrıntılı istemci dağıtımı yükleme hataları

- Endpoint Protection sistem durumu Özeti: korunan, riskli, bilinmeyen ve desteklenmeyen istemcilerin sayısı dahil

- Uç Nokta Koruma ilkesi yapılandırma

- Uygulamalar için yükleme davranışı ile yapılandırılan işlemlerin listesi

- Son güncelleştirmeden bu yana geçen en düşük/en yüksek/ortalama saat sayısı

- Yazılım güncelleştirme dağıtımı koleksiyonlarında etkin olmayan istemcilerin en düşük/en yüksek/ortalama sayısı

- Yazılım güncelleştirmelerinin paket başına en düşük/en yüksek/ortalama sayısı

- ***[Güncelleştirilmiş]*** MSI ürün kodu dağıtım istatistikleri 

- Yazılım güncelleştirme dağıtımlarının genel uyumluluğu

- Zaman aşımına uğradı yazılım güncelleştirmeleri olan grupların sayısı

- Yazılım güncelleştirme dağıtımı hata kodları ve sayısı

- Yazılım güncelleştirme dağıtım bilgileri: istemci ile UTC zamanına karşılık gelen dağıtım yüzdesi, gerekli ve isteğe bağlı ve sessiz ve yeniden başlatma gizleme

- Yazılım güncelleştirme noktası tarafından eşitlenen yazılım güncelleştirme ürünleri

- Yazılım güncelleştirme taraması başarı yüzdeleri

- Ortamda en iyi 50 CPU

- Microsoft Intune yönettiği cihazlar için Exchange Active Sync (EAS) koşullu erişim ilkelerinin (blok veya karantina) türü

- Iş için Microsoft Store ayrıntıları: uygulama kimliği, çevrimiçi durum veya çevrimdışı durum ve toplam satın alınan lisans sayısı dahil eşitlenmiş uygulamaların toplu olmayan listesi
