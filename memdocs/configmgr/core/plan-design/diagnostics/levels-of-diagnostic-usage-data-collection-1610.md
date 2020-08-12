---
title: 1610 için tanılama verileri
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1610 tarafından toplanan tanılama ve kullanım verilerinin düzeyleri hakkında bilgi edinin.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 02b1eb010cc874e75b733b567ce4f41e59eab82e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128806"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-configuration-manager"></a>Configuration Manager sürüm 1610 için tanılama kullanım verileri toplama düzeyleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager sürüm 1610, üç düzeyde tanılama ve kullanım verisi toplar: **temel**, **Gelişmiş**ve **tam**. Varsayılan olarak, bu özellik Gelişmiş düzeye ayarlanmıştır. Aşağıdaki bölümler, her bir düzeyin topladığı veriler hakkında ek ayrıntılar sağlar.

Önceki sürümlerden yapılan değişiklikler ***[yeni]***, ***[güncelleştirildi]***, ***[kaldırıldı]*** veya ***[taşındı]*** ile belirtilmiştir.


> [!IMPORTANT]
>  Configuration Manager, temel veya gelişmiş düzeylerde site kodlarını, site adlarını, IP adreslerini, Kullanıcı adlarını, bilgisayar adlarını, fiziksel adresleri ya da e-posta adreslerini toplamaz. Bu bilgilerin tam düzeyinde toplanması, büyük olasılıkla günlük dosyaları veya bellek anlık görüntüleri gibi gelişmiş tanılama bilgilerine dahil değildir. Microsoft bu bilgileri sizi tanımlamak, sizinle iletişim kurmak veya reklam geliştirmek için kullanmaz.

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Düzeyi değiştirme
 **Site** nesne sınıfında **değiştirme** izinlerini içeren rol tabanlı yönetim kapsamına sahip yöneticiler, Configuration Manager konsolundaki tanılama ve kullanım verileri ayarlarında toplanan veri düzeyini değiştirebilir.

Sürüm 1610 ' den başlayarak, **Yönetim**  >  **genel bakış**  >  **site yapılandırma**  >  **siteleri**' ne giderek veri toplama düzeyini konsolunun içinden değiştirirsiniz. **Hiyerarşi ayarları**' nı açın ve ardından kullanmak istediğiniz veri düzeyini seçin.  

##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Düzey 1 - Temel
 Temel düzey, hiyerarşiniz hakkındaki verileri, yüklemenizin veya yükseltme deneyiminizin artırılmasına yardımcı olması gereken verileri ve hiyerarşiniz için geçerli Configuration Manager güncelleştirmelerinin belirlenmesine yardımcı olan verileri içerir.

 Configuration Manager sürüm 1610 için, bu düzey aşağıdakileri içerir:


- Kurulum bilgileri:
  - Yapı, install türü, dil paketleri, etkinleştirdiğiniz Özellikler  

  - Güncelleştirme paketi dağıtım durumu ve hataları, İndirme ilerlemesi ve önkoşul hataları    

  - Yükseltme sonrası betiği sürümü

  - Güncelleştirme hızlı halkası kullanımı

  - ***[Yeni]*** Yayın öncesi kullanımı, kurulum medya türü, dal türü

  - ***[Yeni]*** Yazılım Güvencesi sona erme tarihi

- Veritabanı performans ölçümleri (çoğaltma işleme bilgileri, işlemciye göre en çok kullanılan SQL Server saklı yordamları ve disk kullanımı)

- Temel veritabanı yapılandırması (işlemciler, küme yapılandırması ve dağıtılmış görünümlerin yapılandırması)

- Configuration Manager veritabanı şeması (tüm nesne tanımlarının karması)

- Configuration Manager istemci sürümleri ve işletim sistemi sürümleri sayısı

- Exchange Connector tarafından ayarlanan yönetilen cihazlar ve ilkeler için işletim sistemi sayısı

- İstemci dillerinin ve yerel ayarların sayısı

- Dala ve derlemeye göre Windows 10 cihazlarının sayısı

- Temel Configuration Manager site hiyerarşisi verileri (site listesi, türü, sürümü, durumu, istemci sayısı ve saat dilimi)

- Temel site sistemi sunucusu bilgileri (kullanılan site sistemi rolleri, Internet ve SSL durumu, işletim sistemi, işlemciler, fiziksel veya sanal makine)

- Temel Kullanıcı bulma istatistikleri (Kullanıcı bulma sayısı ve en düşük/en yüksek/ortalama Grup boyutları)

- Temel Endpoint Protection bilgileri (kötü amaçlı yazılımdan koruma istemci sürümleri)

- Temel uygulama ve dağıtım türü sayıları (Toplam uygulama, birden çok dağıtım türüne sahip toplam uygulama, bağımlılıklara sahip toplam uygulama, yenisiyle değiştirilen Toplam uygulama sayısı ve kullanımdaki dağıtım teknolojilerinin sayısı)

- Temel işletim sistemi dağıtımı (OSD) sayıları (görüntüler)

- Dağıtım noktası ve yönetim noktası türleri ile temel yapılandırma bilgileri (korumalı, önceden hazırlanan, PXE, çok noktaya yayın, SSL durumu, çekme/eş dağıtım noktaları, MDM etkin, SSL etkin, vb.)

- Telemetri istatistikleri (çalışma sırasında, çalışma zamanı, hatalar)

- Yapılandırılan telemetri düzeyi, mod (çevrimiçi veya çevrimdışı) ve hızlı güncelleştirme yapılandırması

- Ağ bulma kullanımı (etkin veya devre dışı)
- Yönetici Konsolu:

  - Konsol bağlantıları (işletim sistemi sürümü, dil, SKU ve mimari, sistem belleği, mantıksal işlemci sayısı, bağlantı site KIMLIĞI, yüklü .NET sürümleri ve konsol dil paketleri) hakkında istatistikler    

- SQL sürümü, hizmet paketi düzeyi, sürüm, harmanlama KIMLIĞI ve karakter kümesi


##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Düzey 2 - Gelişmiş
Gelişmiş düzey, Kurulum bittikten sonra varsayılandır. Bu düzey, temel düzeyde ve özelliğe özgü veriler (kullanım sıklığı ve süresi), Configuration Manager istemci ayarları (bileşen adı, durumu ve yoklama aralıkları gibi belirli ayarlar) ile yazılım güncelleştirmeleri hakkındaki temel bilgiler içinde toplanan verileri içerir.

Bu düzey, Microsoft 'un, ürün ve hizmetlerin gelecekteki sürümlerinde yararlı geliştirmeler yapmak için gereken en düşük verileri sağladığı için önerilir. Bu düzey, nesne adlarını (siteler, kullanıcılar, bilgisayarlar veya nesneler), güvenlikle ilgili nesnelerin ayrıntılarını veya yazılım güncelleştirmesi gerektiren sistem sayısı gibi güvenlik açıklarını toplamaz.

Configuration Manager sürüm 1610 için, bu düzey aşağıdakileri içerir:

-   **Uygulama Yönetimi:**  

    -    Kuruluş içinde kullanılan dağıtım türleri için temel kullanım/hedefleme bilgileri (Kullanıcı ve cihaz hedefli, gerekli ve kullanılabilir ve evrensel uygulamalar)  

    -   Uygulama dağıtım bilgileri (yükleme/kaldırma, onay, Kullanıcı etkileşimi etkin/devre dışı, bağımlılık ve yerine geçme gerekir)  

    -   Mevcut uygulama isteği istatistikleri  

    -   Türe göre paket sayısı  

    -   İşletim sistemine göre uygulama uygulanabilirliği sayısı  

    -   Paket/program dağıtımı sayısı  

    -   App-V ortamları ve dağıtım özellikleri sayısı  

    -   Windows 10 lisanslı uygulama lisansı sayısı  

    -   Her zaman süresi içinde Kullanıcı/cihaz başına en düşük/en yüksek/ortalama uygulama dağıtımı sayısı

    -   Bakım penceresi türü ve süresi  

    -  Uygulama ilkesi boyutu ve karmaşıklık istatistikleri

    - ***[Güncelleştirilmiş]*** Iş uygulamaları için Windows Mağazası ve eşitleme istatistikleri (özetlenen uygulama türleri, lisanslanmış uygulama durumu ve çevrimiçi ve çevrimdışı lisanslanmış uygulama sayısı dahil)  

    - Sınır grubu istatistikleri (kaç hızlı, kaç tane yavaş ve grup başına sayı)

    - MSI yapılandırma seçenekleri ve sayıları

    - Uygulama gereksinimleri (dağıtım teknolojisi ile yerleşik koşulların sayısına başvurulur)

    - Uygulama yerine geçme, en yüksek zincir derinliği

    - Evrensel veri erişimi (UDA) kullanımı, nasıl oluşturulur

    - ***[Yeni]*** Uygulama onay istatistikleri ve kullanım sıklığı



-   **İstemcilerinin**  

    -   Etkinleştirilmiş istemci aracıları listesi/sayısı  

    -   Kaynak konum türlerinden gelen istemci yüklemelerinin sayısı  

    -   İstemci yüklemesi hatalarının sayısı  

    -  ***[Güncelleştirilmiş]*** İstemci otomatik yükseltme: istemci pilolama ve dışlama kullanımı (genişletilmiş birlikte çalışabilirlik istemcisi) dahil dağıtım yapılandırması

    -  İstemci sistem durumu istatistikleri ve en önemli sorun Özeti

    - Yıl içinde BIOS yaşı

    - Ay içinde işletim sistemi yaşı

    - Yazılım Merkezi eylemlerinin sayısı

    - Etkin yönetim teknolojisi (AMT) istemci sürümü

    - İstemci dağıtımı indirme hataları

    - İstemci bildirim işlemi eylem durumu (her birinin kaç kez çalıştığı, en fazla hedeflenen istemci sayısı ve ortalama başarı oranı)

    - Dağıtım yöntemi başına istemci ve istemci sayısı için kullanılan dağıtım yöntemleri

    - İstemci önbellek boyutu yapılandırması

    - ***[Yeni]***  Donanım envanteri sınıfları, yazılım envanteri kuralları ve dosya toplama kuralları sayısı




- **Cloud Services:**

  - Operations Management Suite ile eşitlenen koleksiyonların sayısı

  -  Operations Management Suite Bulut bağlayıcısının etkin olup olmadığı

  - ***[Yeni]*** Bulut Yönetimi Ağ Geçidi yapılandırma ve kullanım istatistikleri

  - ***[Yeni]*** Upgrade Analytics Bağlayıcısı sayısı




- **Koleksiyonlarıyla**

    -  Koleksiyon değerlendirme istatistikleri (sorgu süresi, atanan ve atanmamış sayımlar, türe göre sayılar, KIMLIK geçişi ve kural kullanımı)

    - Dağıtım olmadan Koleksiyonlar

    - Koleksiyon KIMLIĞI kullanımı (kimlik dışı)



-   **Uyumluluk ayarları:**  

    -   Türe göre yapılandırma öğesi sayısı  

    -   Temel yapılandırma temeli bilgileri (sayısı, dağıtım sayısı ve başvuru sayısı)  

    -   Yerleşik ayarlara başvuran dağıtımların sayısı (Şu anda düzeltme ayarları)  

    -   Özel ayarlar için oluşturulan kuralların ve dağıtımların sayısı (Şimdi, düzeltme için yakalama)  
    -   Dağıtılan Basit Sertifika Kayıt Protokolü (SCEP), VPN, Wi-Fi, sertifika (. pfx) ve uyumluluk Ilkesi şablonlarının sayısı

    -  Platforma göre SCEP sertifikası, VPN, Wi-Fi, sertifika (. pfx) ve uyumluluk Ilkesi dağıtımları sayısı

    - Iş için Passport ilkesi (oluşturuldu, dağıtıldı)



-   **İçeriði**  

    -   Türe göre sınır sayısı  

    -   Sınır grubu bilgileri (her sınır grubuna atanan sınır ve site sistemi sayısı)  

    - ***[Yeni]*** Sınır grubu ilişkileri ve geri dönüş yapılandırması

    -   Dağıtım noktası grubu bilgileri (her dağıtım noktası grubuna atanan paket ve dağıtım noktası sayısı)  

    -   Dağıtım noktası yapılandırma bilgileri (dal önbelleği ve dağıtım noktası izlemenin kullanımı)  

    -   Dağıtım Yöneticisi yapılandırma bilgileri (iş parçacıkları, yeniden deneme gecikmesi, yeniden deneme sayısı ve istek temelli dağıtım noktası ayarları)  

    - ***[Yeni]*** Eş önbellek istemcisi sayısı ve kullanım istatistikleri

    - ***[Yeni]*** İstemci içeriği indirme istatistikleri


-   **Endpoint Protection:**  

    -   Kötü amaçlı yazılımdan koruma ve Windows Güvenlik Duvarı İlkesi kullanımını Endpoint Protection (gruba atanan benzersiz ilkelerin sayısı)<br /><br /> Bu, ilkede yer alan ayarlarla ilgili herhangi bir bilgi içermez.  

    -   Endpoint Protection dağıtım hataları (Endpoint Protection İlkesi dağıtımı hata kodlarının sayısı)  

    -   Endpoint Protection panosunda görünmesi için seçilen koleksiyon sayısı  

    -   Endpoint Protection özelliği için yapılandırılmış uyarı sayısı  

    -   Gelişmiş tehdit koruması (ATP) Ilkeleri (ilke sayısı ve ilkelerin dağıtılıp dağıtılmayacağı)


- **Geçiş**

  -   Geçirilen nesne sayısı (geçiş sihirbazının kullanımı)



-   **Mobil cihaz yönetimi (MDM):**  

    -   ***[Güncelleştirilmiş]*** Verilen mobil cihaz eylemlerinin sayısı: kilitleme, PIN Rest, Temizleme, devre dışı bırakma ve şimdi eşitleme komutları  

    -   Configuration Manager ve Microsoft Intune tarafından yönetilen mobil cihaz sayısı ve nasıl kaydedildikleri (toplu, Kullanıcı tabanlı)  

    -   Mobil cihaz yoklama zamanlaması ve mobil cihaz iade süresi istatistikleri  

    -   Mobil cihaz ilke sayısı  

    -   Birden çok kayıtlı mobil cihazı olan kullanıcı sayısı  

-   **Microsoft Intune sorun giderme:**

    -   Microsoft Intune 'ten indirilen durum, durum, envanter, RDR, DDR, UDX, kiracı durumu, POL, LOG, CERT, CRP, yeniden eşitleme, CFD, RDO, BEX, ıSM ve uyumluluk iletilerinin sayısı ve boyutu

    -   Microsoft Intune çoğaltılan cihaz eylemlerinin sayısı ve boyutu (silme, devre dışı bırakma, kilitleme), telemetri ve veri iletileri

    -   Microsoft Intune için tam ve Delta Kullanıcı eşitleme istatistikleri


-   **Şirket içi mobil cihaz yönetimi (MDM):**  

    -   Şirket içi MDM uygulama dağıtımları için dağıtım başarı/hata istatistikleri  

    -   Windows 10 toplu kayıt paketleri ve profillerinin sayısı  



-   **İşletim sistemi dağıtımı:**  

    -   Önyükleme görüntüleri, sürücüler, sürücü paketleri, çok noktaya yayını destekleyen dağıtım noktaları, PXE özellikli dağıtım noktaları ve görev dizileri sayısı  

    -   Görev dizisi adım kullanım sayısı

    - ***[Yeni]*** Sürüm yükseltme ilkelerinin sayısı



-   **Site güncelleştirmeleri:**

    - Yüklü Configuration Manager düzeltmelerinin sürümleri




-   **Yazılım güncelleştirmeleri:**  

    -   Yazılım güncelleştirme dağıtımları olan koleksiyonların toplam/ortalama sayısı ve dağıtılan güncelleştirmelerin en yüksek/ortalama sayısı  

    -   Eşitlemeye bağlı otomatik dağıtım kuralları sayısı  

    -   Yeni bir grup oluşturan veya mevcut bir gruba güncelleştirme ekleyen otomatik dağıtım kuralları sayısı  

    -   Otomatik dağıtım kurallarında kullanılan kullanılabilir ve son tarih değişimleri  

    -   Güncelleştirme başına ortalama ve en yüksek atama sayısı  

    -   System Center Update Publisher ile oluşturulan ve dağıtılan güncelleştirmelerin sayısı  

    -   Güncelleştirme grupları ve atamalarının sayısı  

    -   Güncelleştirme paketi sayısı ve paketlerle hedeflenen dağıtım noktalarının en yüksek/en düşük/ortalama sayısı  

    -   Güncelleştirme grubu sayısı ve güncelleştirme grubu başına en düşük/en yüksek/ortalama güncelleştirme sayısı  

    -   Dağıtılan, zaman aşımına geçilen, yenisiyle değiştirilen, indirilen ve EULA 'Lar içeren güncelleştirmelerin güncelleştirme sayısı ve yüzdesi  

    -   Güncelleştirme taraması hata kodları ve makine sayısı  

    -   İstemci güncelleştirme değerlendirmesi ve tarama zaman çizelgeleri  

    -   Yazılım güncelleştirme noktası eşitleme zaman çizelgesi  

    -   Birden çok dağıtıma sahip otomatik dağıtım kuralları sayısı  

    -   Etkin Windows 10 bakım planları için kullanılan konfigürasyonlar  

    -   Windows 10 panosu içerik sürümleri  

    -   Iş için Windows Update kullanan Windows 10 istemcileri sayısı  

    -   Küme düzeltme eki uygulama istatistikleri  

    -   Dağıtılan Office 365 güncelleştirmeleri sayısı  

    -   Yazılım güncelleştirme noktası tarafından eşitlenen sınıflandırmalar

    -   Yazılım güncelleştirme noktası yük dengeleme istatistikleri

    -  ***[Yeni]*** Windows 10 Express güncelleştirmelerinin yapılandırması




-   **SQL/performans verileri:**  

    -   En büyük veritabanı tablolarının sayısı  

    -   ***[Güncelleştirilmiş]***  SQL AlwaysOn çoğaltma bilgileri, kullanımı ve sistem durumu

    -  SQL değişiklik izleme tutma süresi

    - Bulma türleri, etkin ve zamanlama (tam, artımlı)

    - Bulgu işlem istatistikleri (bulunan nesne sayısı)

    - SQL değişiklik izleme performansı sorunları, saklama süresi ve otomatik temizleme durumu



- **Çeşitli**

    - LAN 'da uyandırma (WOL) ile site sayısı

    - ***[Yeni]*** Raporlama kullanımı ve performans istatistikleri  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Düzey 3 - Tam
Tam düzey, temel ve gelişmiş düzeylerdeki tüm verileri içerir. Aynı zamanda Uç Nokta Koruma, güncelleştirme uyumluluğu yüzdeleri ve yazılım güncelleştirme bilgileri hakkında ek bilgiler de içerir.  Bu düzey, yakalama sırasında bellekte veya günlük dosyalarında bulunan kişisel bilgileri içerebilen sistem dosyaları ve bellek anlık görüntüleri gibi gelişmiş tanı bilgilerini de içerebilir.

Configuration Manager sürüm 1610 için, bu düzey aşağıdakileri içerir:

-   Koleksiyon değerlendirme ve yenileme istatistikleri

-   Uç Nokta Koruma durum özeti (korunan, risk altında olan, bilinmeyen ve desteklenmeyen istemci sayısı dahil)

-   Uç Nokta Koruma ilkesi yapılandırma

-   Yazılım güncelleştirme dağıtım bilgileri (istemci ile UTC zamanına göre hedeflenen dağıtım yüzdesi, gerekli ve isteğe bağlı ve sessiz ve yeniden başlatma gizleme)

-   Yazılım güncelleştirme dağıtımlarının genel uyumluluğu

-   Otomatik dağıtım kuralı değerlendirmesi zaman çizelgesi bilgileri

-   Yazılım güncelleştirme dağıtımı hata kodları ve sayısı

-   Yazılım güncelleştirme dağıtımı koleksiyonlarında etkin olmayan istemcilerin en düşük/en yüksek/ortalama sayısı

-   Zaman aşımına uğradı yazılım güncelleştirmeleri olan grupların sayısı

-   Yazılım güncelleştirmelerinin paket başına en düşük/en yüksek/ortalama sayısı

-   Yazılım güncelleştirme taraması başarı yüzdeleri

-   Son güncelleştirmeden bu yana geçen en düşük/en yüksek/ortalama saat sayısı

-    Yazılım güncelleştirme noktası tarafından eşitlenen yazılım güncelleştirme ürünleri
-    Uyumluluk ayarları: SCEP, VPN, Wi-Fi ve uyumluluk Ilkesi şablonu yapılandırma ayrıntıları

-    Intune tarafından yönetilen cihazlar için EAS koşullu erişim ilkelerinin (blok veya karantina) türü

-   Ortamda en iyi 50 CPU

-   Configuration Manager kullanımı için DCM yapılandırma paketi

-   MSI ürün kodu (müşterilerin dağıtabolduğu ortak uygulamalar)

-   ATP sistem durumu Özeti

-   Ayrıntılı istemci dağıtımı yükleme hataları

- ***[Yeni]*** Iş için Windows Mağazası uygulama ayrıntıları (AppID, çevrimiçi durum veya çevrimdışı durum ve toplam satın alınan lisans sayısı dahil eşitlenmiş uygulamaların toplama olmayan listesi)
