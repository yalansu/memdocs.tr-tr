---
title: 2006 için tanılama ve kullanım verileri
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 2006 ' deki her düzeyde toplanan belirli veriler hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: ae8b48f8-391e-49d6-bb1a-9205378acef8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78f662fe6d4d9f348d94788628328ca8b3aeb55c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129707"
---
# <a name="diagnostic-and-usage-data-for-version-2006"></a>Sürüm 2006 için tanılama ve kullanım verileri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşağıdaki bölümler her düzeyde toplanan veriler hakkında ek ayrıntılar sağlar. Düzeyler ve bunların nasıl değiştirileceği hakkında daha fazla bilgi için bkz. [Tanılama kullanım verileri düzeyleri](levels-overview.md).

Önceki sürümlerden yapılan değişiklikler ***[yeni]***, ***[güncelleştirildi]***, ***[kaldırıldı]*** veya ***[taşındı]*** ile belirtilmiştir.

> [!IMPORTANT]
> Configuration Manager, temel veya gelişmiş düzeylerde site kodlarını, site adlarını, IP adreslerini, Kullanıcı adlarını, bilgisayar adlarını, fiziksel adresleri ya da e-posta adreslerini toplamaz. Bu bilgilerin tam düzeyinde toplanması herhangi bir amaca bağlı değildir. Büyük olasılıkla günlük dosyaları veya bellek anlık görüntüleri gibi gelişmiş tanılama bilgilerine dahildir. Microsoft bu bilgileri sizi tanımlamak, sizinle iletişim kurmak veya reklam geliştirmek için kullanmaz.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Düzey 1 - Temel

Configuration Manager sürüm 2006 için, bu düzey aşağıdaki verileri içerir:

- Configuration Manager konsol bağlantılarıyla ilgili istatistikler: işletim sistemi sürümü, dil, SKU ve mimari, sistem belleği, mantıksal işlemci sayısı, bağlantı site KIMLIĞI, yüklü .NET sürümleri, konsol dil paketleri ve yetenekli kimlik doğrulama düzeyi

- Temel uygulama ve dağıtım türü sayıları: Toplam uygulama, birden çok dağıtım türüne sahip toplam uygulama, bağımlılıklara sahip toplam uygulama, yenisiyle değiştirilen Toplam uygulama sayısı ve kullanımdaki dağıtım teknolojilerinin sayısı

- Temel Configuration Manager site hiyerarşisi verileri: site listesi, türü, sürümü, durumu, istemci sayısı, saat dilimi ve sağlık durumu

- Temel veritabanı yapılandırması: işlemciler, bellek boyutu, bellek ayarları, Configuration Manager veritabanı yapılandırması, Configuration Manager veritabanı boyutu, küme yapılandırması, dağıtılmış görünümlerin yapılandırılması ve değişiklik izleme sürümü  

- Temel bulma İstatistikleri: bulma sayısı, en düşük/en yüksek/ortalama Grup boyutları ve site tamamen Azure Active Directory hizmetleriyle çalışırken

- Kötü amaçlı yazılımdan koruma istemci sürümleri hakkında temel Endpoint Protection bilgileri

- Temel işletim sistemi dağıtım görüntülerinin sayısı

- Temel site sistemi sunucusu bilgileri: kullanılan site sistem rolleri, internet ve SSL durumu, işletim sistemi, işlemciler, fiziksel veya sanal makine ve site sunucusu yüksek kullanılabilirliği kullanımı

- Configuration Manager veritabanı şeması (tüm nesne tanımlarının karması)

- Tanılama ve kullanım verileri, çevrimiçi veya çevrimdışı mod ve hızlı güncelleştirme yapılandırması için yapılandırılmış düzey

- İstemci dillerinin ve yerel ayarların sayısı

- Configuration Manager istemci sürümlerinin, işletim sistemi sürümlerinin ve Office sürümlerinin sayısı

- Exchange Connector tarafından ayarlanan yönetilen cihazlar ve ilkeler için işletim sistemi sayısı

- Dala, yapıya ve benzersiz Active Directory ormanına göre Windows 10 cihazlarının sayısı  

- Iş için Windows Update kullanan Windows 10 istemcileri sayısı  

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

- Tanılama ve kullanım verileri İstatistikleri: çalıştırma, çalışma zamanı, hatalar  

- Ağ bulmanın etkin veya devre dışı olup olmadığı  

- Azure Active Directory katılmış istemci sayısı  

- Türe göre oluşturulan aşamalı dağıtım sayısı  

- Genişletilmiş birlikte çalışabilirlik istemcilerinin sayısı  

- 255 karakterden uzun donanım envanteri özelliklerinin karma listesi  

- Ortak yönetim kayıt yöntemine göre istemci sayısı  

- Ortak yönetim kaydı için hata istatistikleri  

- Windows işletim sistemi yaşı ile en yakın üç aylık aralığa kadar istemci sayısı  

- İstemcilerde ve sunucularda kullanılan ilk 10 işlemci adı  

- Anahtar Configuration Manager nesnelerinin sayısı ve işleme oranları: veri bulgu kayıtları (DDR), durum iletileri, durum iletileri, donanım envanteri, yazılım envanteri ve gelen kutularındaki toplam dosya sayısı  

- Site sunucusu diski ve işlemci performansı bilgileri  

- Configuration Manager site sunucu işlemlerine yönelik çalışma süresi ve bellek kullanım bilgileri  

- Configuration Manager site sunucu işlemlerine yönelik çökmelerin sayısı ve varsa Watson imza KIMLIĞI  

- Bellek kullanımı ve kilit sayısı bazında popüler SQL sorgularının karma listesi  

- Ortak yönetim 'in toplu kullanım istatistikleri: şimdiye kadar kaydolan istemci sayısı, kayıtlı istemci sayısı, kayıt bekleyen istemci sayısı, ilke, iş yükü durumları, pilot/dışlama koleksiyon boyutları ve kayıt hataları  

- Microsoft BitLocker yönetim ve Izleme (MBAD) sunucu tarafı uzantılarının varlığı  

- Varlık yönetim bilgileri için kategorilere ayrılmamış ve kategorilere ayrılmamış uygulamalar sayısı

- Yönetim hizmetinin durumu ve durumu

- Anahtar site özniteliklerinin karması (site KIMLIĞI, SQL Aracısı KIMLIĞI ve site değişim anahtarı)

- Microsoft Edge yüklemelerinin sayısı

- Configuration Manager bağlı Azure Active Directory uygulama ve hizmet sayısı

- Site sistem durumu bilgileri

- Konsol kilitlenme konumları Configuration Manager

- Configuration Manager konsolu kullanım istatistikleri

- Bulut iliştirme ve ayır eylemleri

- Intune bulut hizmeti ile son eşitleme durumu

- Yönetim hizmetindeki hataların sayısı

- Toplu kayıt belirtecinin kullanımı

- Varsayılan ve tercih edilen tarayıcıya göre istemci sayısı

- ***[Taşındı]*** Bulut Yönetimi Ağ Geçidi yapılandırma ve kullanım istatistikleri: bölge ve ortam sayısı ve kimlik doğrulama/yetkilendirme istatistikleri  

- ***[Taşındı]*** SQL AlwaysOn çoğaltma bilgileri, kullanımı ve sistem durumu  

- ***[Yeni]*** Yönetici Konsolu bildirim yapılandırması ve durumu

- ***[Yeni]*** Site sistem durumu denetimi yapılandırması ve durumu

## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Düzey 2 - Gelişmiş

Configuration Manager sürüm 2006 için, bu düzey aşağıdaki verileri içerir:

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

- Bir görev dizisinde başvurulan uygulama sayısı  

- Uygulama Kataloğu için farklı marka sayısı  

- Pano kullanılarak oluşturulan Microsoft 365 Apps uygulamalarının sayısı  

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

- Toplu Kullanıcı cihaz benzeşimi istatistikleri  

- Cihaz başına en fazla ve ortalama birincil Kullanıcı  

- Türe göre uygulama genel koşulu kullanımı  

- Software Center özelleştirme yapılandırması  

- Paket Dönüştürme Yöneticisi hazırlığı ve sayıları  

- Türe göre uygulama algılama yöntemlerinin sayısı  

- Uygulama zorlama hatalarının sayısı  

- MSI Yükleyicisi özellikleri  

- Kullanıcı yüklemesi isteklerinin istatistikleri  

- E-posta onayı özelliğinin kullanımıyla ilgili toplu istatistikler  

- Uygulama kataloğunda dosya sayısı, içerik boyutu, hizmet sayısı ve Mssıs özel eylem sayısı  

- Office ProPlus hazırlık durumuna göre cihaz sayısı

- Uygulama gruplarının kullanımıyla ilgili toplu istatistikler

- Office Eklentilerindeki toplu istatistikler, Office hazırlık araç seti kullanımı ve Microsoft 365 uygulamalarla istemci sayısı

- Office eklentisi sistem durumu ile ilgili toplu istatistikler

- Office Pro Plus pilot koleksiyonları sayısı ve boyutu

- Office sistem durumu verileri gönderen Office Pro Plus cihazlarının sayısı

### <a name="client"></a>İstemci  

- Etkin yönetim teknolojisi (AMT) istemci sürümü  

- Yıl içinde BIOS yaşı  

- Güvenli önyükleme etkin cihazların sayısı  

- TPM durumuna göre cihaz sayısı  

- İstemci otomatik yükseltme: istemci pilolama ve dışlama kullanımı (genişletilmiş birlikte çalışabilirlik istemcisi) dahil dağıtım yapılandırması  

- İstemci önbellek boyutu yapılandırması  

- İstemci dağıtımı indirme hataları  

- İstemci durumu istatistikleri ve istemci sürümüne, bileşene, işletim sistemine ve iş yüküne göre en önemli sorun Özeti  

- İstemci bildirim işlemi eylem durumu: her birinin kaç kez çalıştığı, en fazla hedeflenen istemci sayısı ve ortalama başarı oranı  

- Kaynak konum türlerinden gelen istemci yüklemelerinin sayısı  

- İstemci yüklemesi hatalarının sayısı  

- Hyper-V veya Azure tarafından sanallaştırılmış cihazların sayısı  

- Yazılım Merkezi eylemlerinin sayısı  

- UEFı özellikli cihazların sayısı  

- Dağıtım yöntemi başına istemci ve istemci sayısı için kullanılan dağıtım yöntemleri  

- Etkinleştirilmiş istemci aracıları listesi/sayısı  

- Ay içinde işletim sistemi yaşı  

- ***[Güncelleştirilmiş]***  -  ***[Yeni]*** yazılım envanter kuralları, dosya toplama kuralları ve genel sistem durumu

- Cihaz sistem durumu kanıtlama İstatistikleri: en yaygın hata kodları, şirket içi sunucu sayısı ve çeşitli durumlarda cihaz sayısı  

- Varsayılan tarayıcı olarak cihaz sayısı  

- Configuration Manager tarafından üretilen sunucu kimlik doğrulama sertifikalarının sayısı  

- Modele göre Microsoft Surface cihazlarının sayısı  

- Sorun türüne göre istemci sistem durumu denetimi hatalarının sayısı

- ***[Yeni]*** Uç nokta Analizi olayının özetlenen sayısı

### <a name="cloud-services"></a>Cloud Services  

- Azure Active Directory bulma istatistikleri  

- Azure Log Analytics eşitlenen koleksiyonların sayısı  

- Upgrade Analytics Bağlayıcısı sayısı  

- Azure Log Analytics Cloud Connector 'ın etkin olup olmadığı  

- Kaynak konumu olarak bulut dağıtım noktası olan çekme dağıtım noktalarının sayısı

- Cloud Services Ekleme Sihirbazı 'nın kullanımı

### <a name="cmpivot"></a>CMPivot

- CMPivot kullanım istatistikleri  

- Kaydedilen CMPivot sorgularının sayısı  

- Varlık türüne göre sorgu sayısı  

### <a name="co-management"></a>Ortak yönetim  

- Kayıt zamanlaması ve geçmiş istatistikleri  

- Ortak yönetim için uygun istemci sayısı  

- İlişkili Microsoft Intune kiracısı  

### <a name="collections"></a>Koleksiyonlar  

- Koleksiyon KIMLIĞI kullanımı (kimlik dışı)  

- Koleksiyon değerlendirme İstatistikleri: sorgu süresi, atanan ve atanmamış sayımlar, türe göre sayılar, KIMLIK geçişi ve kural kullanımı  

- Dağıtım olmadan Koleksiyonlar  

- Azure Active Directory eşitlenen koleksiyon sayısı

### <a name="compliance-settings"></a>Uyumluluk ayarları  

- Temel yapılandırma temel bilgileri: sayı, dağıtım sayısı ve başvuru sayısı  

- Uyumluluk ilkesi hata istatistikleri  

- Türe göre yapılandırma öğesi sayısı  

- Düzeltme ayarları da dahil olmak üzere yerleşik ayarlara başvuran dağıtım sayısı  

- Özel ayarlar için oluşturulan kuralların ve dağıtımların sayısı, düzeltme de dahil olmak üzere  

- Dağıtılan Basit Sertifika Kayıt Protokolü (SCEP), VPN, Wi-Fi, sertifika (. pfx) ve uyumluluk ilkesi şablonlarının sayısı  

- Platforma göre SCEP sertifikası, VPN, Wi-Fi, sertifika (. pfx) ve uyumluluk ilkesi dağıtımları sayısı  

- Iş için Windows Hello ilkesi (oluşturulan, dağıtılmış)  

- Dağıtılan Microsoft Edge eski tarayıcı ilkelerinin sayısı  

- OneDrive ilkelerinin sayısı (oluşturulan, dağıtılmış)

- ***[Yeni]*** Kategori, işletim sistemi ve kaynak tarafından dağıtılan uyumluluk ayarlarının sayısı (bulut ile şirket içi)

### <a name="configuration-manager-console"></a>Configuration Manager konsolu

- Kritik olmayan konsol bildirimleri sayısı

- Klasör sayısı

- Konsol performans bilgileri

- konsolda erişilen en sık kullanılan işlem, sihirbaz, özellik sayfası ve ağaç düğümleri

### <a name="content"></a>İçerik  

- Sınır grubu istatistikleri: kaç hızlı, kaç tane yavaş, Grup başına sayı ve geri dönüş ilişkisi  

- Sınır grubu bilgileri: her bir sınır grubuna atanan sınır ve site sistemi sayısı  

- Sınır grubu ilişkileri ve geri dönüş yapılandırması  

- İstemci içeriği indirme istatistikleri  

- Türe göre sınır sayısı  

- Eş önbellek istemcisi sayısı, kullanım istatistiği ve kısmi indirme istatistikleri  

- Dağıtım Yöneticisi yapılandırma bilgileri: iş parçacıkları, yeniden deneme gecikmesi, yeniden deneme sayısı ve dağıtım noktası ayarlarını çekme  

- Dağıtım noktası yapılandırma bilgileri: dal önbelleğinin ve dağıtım noktası izlemenin kullanımı  

- Dağıtım noktası grubu bilgileri: her bir dağıtım noktası grubuna atanan paket ve dağıtım noktası sayısı  

- İçerik kitaplığı türü, yerel veya uzak  

- Yapılandırmaya göre sınır grupları sayısı

- Eş önbellekten dışlanan alt ağların sayısı

### <a name="endpoint-protection"></a>Uç Nokta Koruma  

- Microsoft Defender Gelişmiş tehdit koruması (ATP) ilkeleri (eski adıyla Windows Defender ATP): ilke sayısı ve ilkelerin dağıtılıp dağıtılmayacağı.

- Endpoint Protection özelliği için yapılandırılmış uyarı sayısı  

- Endpoint Protection panosunda görünmesi için seçilen koleksiyon sayısı  

- Windows Defender Exploit Guard ilkeleri, dağıtımları ve hedeflenen istemciler sayısı  

- Dağıtım hatalarını Endpoint Protection, Endpoint Protection İlkesi dağıtımı hata kodlarının sayısı  

- Kötü amaçlı yazılımdan koruma ve Windows güvenlik duvarı ilkesi kullanımı (gruba atanan benzersiz ilkelerin sayısı) Endpoint Protection. Bu veriler, ilkede yer alan ayarlarla ilgili herhangi bir bilgi içermez.

- Microsoft Defender Gelişmiş tehdit koruması ilkeleri için toplu istatistikler

### <a name="migration"></a>Geçiş  

- Geçirilen nesne sayısı (geçiş sihirbazının kullanımı)  

### <a name="mobile-device-management-mdm"></a>Mobil cihaz yönetimi (MDM)  

- Verilen mobil cihaz eylemlerinin sayısı: kilitleme, PIN Rest, Temizleme, devre dışı bırakma ve şimdi eşitleme komutları  

- Mobil cihaz ilke sayısı  

- Configuration Manager yönetilen mobil cihaz sayısı ve bunları nasıl kaydettiğiniz (toplu, Kullanıcı tabanlı)  

- Birden çok kayıtlı mobil cihazı olan kullanıcı sayısı  

- Mobil cihaz yoklama zamanlaması ve mobil cihaz iade süresi istatistikleri  

### <a name="microsoft-intune-troubleshooting"></a>Microsoft Intune sorunlarını giderme  

- Microsoft Intune çoğaltılan cihaz eylemlerinin sayısı ve boyutu (silme, devre dışı bırakma, kilitleme), kullanım verileri ve veri iletileri  

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

- Görüntü bakım görevlerinin sayısı  

- İçeri aktarılan makinelerin sayısı  

- PXE ve istemci kaydından dışlanan yinelenen donanım tanımlayıcılarının (MAC adresi ve SMBıOS GUID) sayısı

- Türe göre görev sırası sayısı (işletim sistemi dağıtımı veya genel görev dizisi)

- Ön önbelleğe içerik ayarları olan paket sayısı

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

- Dağıtılan Microsoft 365 Apps güncelleştirmelerinin sayısı  

- Eşitlenmiş Microsoft Surface sürücü sayısı  

- Güncelleştirme grupları ve atamalarının sayısı  

- Güncelleştirme paketi sayısı ve paketlerle hedeflenen dağıtım noktalarının en yüksek/en düşük/ortalama sayısı  

- System Center Update Publisher ile oluşturulan ve dağıtılan güncelleştirmelerin sayısı  

- Oluşturulan ve dağıtılan Iş ilkeleri için Windows Update sayısı  

- Iş yapılandırmalarının Windows Update toplu istatistikleri  

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

- Üçüncü taraf yazılım güncelleştirme kataloğu aboneliklerinin ve kullanımının sayısı  

- İçerikle ve içerik olmadan dağıtılan yazılım güncelleştirmelerinin sayısı  

- Gerekli, dağıtılmış, süre dolma, yenisiyle değiştirilen ve indirilen toplu güncelleştirme sayısı hakkında toplanmış istatistikler  

- UUP ürün kategorilerinin kullanımı  

- En az bir adet dağıtılmış kalite güncelleştirmesi veya güncelleştirme özelliği olan istemcilerin sayısı  

- En yüksek hata kodları ve etkilenen cihaz sayısı  

- Üçüncü taraf yazılım güncelleştirme kataloglarının aboneliklerinin listesi

- WSUS bakım ayarlarının kullanımı

- Düzenleme grubu kullanımı

- Geri dönüş yapılandırma ayarlarını Windows Update

### <a name="sqlperformance-data"></a>SQL/performans verileri  

- Site özetlemesinin yapılandırması ve süresi  

- En büyük veritabanı tablolarının sayısı  

- Bulgu işlem istatistikleri (bulunan nesne sayısı)  

- Bulma türleri, etkin ve zamanlama (tam, artımlı)  

- SQL değişiklik izleme performansı sorunları, saklama süresi ve Oto Temizleme durumu  

- SQL değişiklik izleme tutma süresi  

- En yaygın ve en pahalı ileti türlerini içeren durum ve durum iletisi performans istatistikleri  

- Yönetim noktası trafik istatistikleri (uç nokta tarafından gönderilen ve alınan toplam bayt)  

- Yönetim noktası performans sayacı ölçümleri  

- Yönetim noktasındaki yazılım merkezi uç noktalarına yapılan çağrıların toplu performans istatistikleri

- SQL bakım görevi yapılandırması ve durumu

- Son yeniden başlatma isteklerinin durumu

### <a name="miscellaneous"></a>Çeşitli  

- Eşitleme zamanlaması, ortalama süre ve özelleştirilmiş tablolar özelliğinin kullanımı dahil olmak üzere veri ambarı hizmet noktası yapılandırması  

- Komut dosyası sayısı ve istatistikleri Çalıştır/Düzenle  

- LAN'da Uyandırma (WOL) ile site sayısı  

- Raporlama kullanımı ve performans istatistikleri  

- Aşamalı dağıtım kullanım istatistikleri  

- Yönetim öngörüleri öğe sayıları ve ilerleme durumu  

- Site sunucusundaki benzersiz Configuration Manager olmayan işlemlere yönelik çökme sayısı ve varsa Watson imza KIMLIĞI  

- Masaüstü Analizi kayıt hataları ve kullanımı ile ilgili toplu istatistikler

- IŞLETIM sistemi, form faktörü ve sürücü türüne göre toplanan sistem önyükleme süresi istatistikleri

- Masaüstü analizinin kullanımıyla ilgili toplu istatistikler

- Azure geçiş aracının kullanımı

- Tarayıcı kullanımı olan istemci sayısı

## <a name="level-3---full"></a><a name="bkmk_level3"></a> Düzey 3 - Tam

Configuration Manager sürüm 2006 için, bu düzey aşağıdaki verileri içerir:

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

- MSI ürün kodu dağıtım istatistikleri  

- Yazılım güncelleştirme dağıtımlarının genel uyumluluğu  

- Zaman aşımına uğradı yazılım güncelleştirmeleri olan grupların sayısı  

- Yazılım güncelleştirme dağıtımı hata kodları ve sayısı  

- Yazılım güncelleştirme dağıtım bilgileri: istemci ile UTC zamanına karşılık gelen dağıtım yüzdesi, gerekli ve isteğe bağlı ve sessiz ve yeniden başlatma gizleme  

- Yazılım güncelleştirme noktası tarafından eşitlenen yazılım güncelleştirme ürünleri  

- Yazılım güncelleştirme taraması başarı yüzdeleri  

- Ortamda en iyi 50 CPU  

- Microsoft Intune yönettiği cihazlar için Exchange Active Sync (EAS) koşullu erişim ilkelerinin (blok veya karantina) türü  

- Iş için Microsoft Store ayrıntıları: uygulama kimliği, çevrimiçi durum veya çevrimdışı durum ve toplam satın alınan lisans sayısı dahil eşitlenmiş uygulamaların toplu olmayan listesi  

- NTLM 'ye geri dönüşe izin verme seçeneği ile gönderilen istemci sayısı  

- Configuration Manager konsol uzantılarının listesi
