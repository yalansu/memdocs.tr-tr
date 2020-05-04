---
title: 1511 için tanılama verileri
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1511 tarafından toplanan tanılama ve kullanım verilerinin düzeyleri hakkında bilgi edinin.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: eaebab1e3c03ad2ffbcebf57bbccf88ce151923e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715602"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-configuration-manager"></a>Configuration Manager sürüm 1511 için tanılama kullanım verileri toplama düzeyleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager sürüm 1511, üç düzeyde tanılama ve kullanım verisi toplar: **temel**, **Gelişmiş**ve **tam**. Varsayılan olarak, bu özellik Gelişmiş düzeye ayarlanmıştır. Aşağıdaki bölümler, her bir düzeyin topladığı veriler hakkında ek ayrıntılar sağlar.  

> [!IMPORTANT]  
>  Configuration Manager, temel veya gelişmiş düzeylerde site kodlarını, site adlarını, IP adreslerini, Kullanıcı adlarını, bilgisayar adlarını, fiziksel adresleri ya da e-posta adreslerini toplamaz. Bu bilgilerin tam düzeyinde toplanması, büyük olasılıkla günlük dosyaları veya bellek anlık görüntüleri gibi gelişmiş tanılama bilgilerine dahil değildir. Microsoft bu bilgileri sizi tanımlamak, sizinle iletişim kurmak veya reklam geliştirmek için kullanmaz.  

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Düzeyi değiştirme  
 **Site** nesne sınıfında **değiştirme** izinlerini içeren rol tabanlı yönetim kapsamına sahip yöneticiler, Configuration Manager konsolundaki tanılama ve kullanım verileri ayarlarında toplanan veri düzeyini değiştirebilir.

 Bunu yapmak için, konsolunda, Backstage sekmesine (açılan menü oku ile sol üst sekmeye) gidin, **kullanım verileri**' ni seçin ve ardından kullanmak istediğiniz veri düzeyini seçin.  


##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Düzey 1 - Temel  
 Temel düzey, hiyerarşiniz hakkındaki verileri, yüklemenizin veya yükseltme deneyiminizin artırılmasına yardımcı olması gereken verileri ve hiyerarşiniz için geçerli Configuration Manager güncelleştirmelerinin belirlenmesine yardımcı olan verileri içerir.  

 Configuration Manager sürüm 1511 ' den başlayarak bu düzey aşağıdakileri içerir:  


-   Kurulum bilgileri
    - Etkinleştirdiğiniz derleme, install türü, dil paketleri ve Özellikler

    - Güncelleştirme paketi dağıtım durumu ve hataları  

-   Veritabanı performans ölçümleri (çoğaltma işleme bilgileri, işlemciye göre en çok depolanan yordamlar SQL Server ve disk kullanımı)  

-   Temel veritabanı yapılandırması (işlemciler, küme yapılandırması ve dağıtılmış görünümlerin yapılandırması)  

-   Configuration Manager veritabanı şeması (tüm nesne tanımlarının karması)  

-   Configuration Manager istemci sürümleri ve işletim sistemi sürümleri sayısı  

-   Exchange Connector tarafından ayarlanan yönetilen cihazlar ve ilkeler için işletim sistemi sayısı  

-   İstemci dillerinin ve yerel ayarların sayısı

-   Dala ve derlemeye göre Windows 10 cihazlarının sayısı  

-   Temel Configuration Manager site hiyerarşisi verileri (site listesi, türü, sürümü, durumu, istemci sayısı ve saat dilimi)  

-   Temel site sistemi sunucusu bilgileri (kullanılan site sistemi rolleri, Internet ve SSL durumu, işletim sistemi, işlemciler, fiziksel veya sanal makine)  

-   Temel Kullanıcı bulma istatistikleri (Kullanıcı bulma sayısı ve en düşük/en yüksek/ortalama Grup boyutları)  

-   Temel Endpoint Protection bilgileri (kötü amaçlı yazılımdan koruma istemci sürümleri)  

-   Temel uygulama ve dağıtım türü sayıları (Toplam uygulama, birden çok dağıtım türüne sahip toplam uygulama, bağımlılıklara sahip toplam uygulama, yenisiyle değiştirilen Toplam uygulama sayısı ve kullanımdaki dağıtım teknolojilerinin sayısı)  

-   Temel işletim sistemi dağıtımı (OSD) sayıları (görüntüler)  

-   Dağıtım noktası ve yönetim noktası türleri ile temel yapılandırma bilgileri (korumalı, önceden hazırlanan, PXE, çok noktaya yayın, SSL durumu, çekme/eş dağıtım noktaları, MDM etkin, SSL etkin, vb.)  

-   Telemetri istatistikleri (çalıştırma, çalışma zamanı ve hatalar)  

##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Düzey 2 - Gelişmiş  
Gelişmiş düzey, Kurulum bittikten sonra varsayılandır. Bu düzey, temel düzeyde, özelliğe özgü veriler (kullanım sıklığı ve süresi), Configuration Manager istemci ayarları (bileşen adı, durumu ve yoklama aralıkları gibi belirli ayarlar) ile yazılım güncelleştirmeleri hakkındaki temel bilgiler ile toplanan verileri içerir.  

Bu düzey, Microsoft 'un, ürün ve hizmetlerin gelecekteki sürümlerinde yararlı geliştirmeler yapmak için gereken en düşük verileri sağladığı için önerilir. Bu düzey, nesne adlarını (siteler, kullanıcılar, bilgisayarlar veya nesneler), güvenlikle ilgili nesnelerle ilgili ayrıntıları veya yazılım güncelleştirmesi gerektiren sistem sayısı gibi güvenlik açıklarını toplamaz.  

Configuration Manager sürüm 1511 ' den başlayarak bu düzey aşağıdakileri içerir:  

-   **Uygulama Yönetimi:**  

    -   Kuruluş içinde kullanılan dağıtım türleri için temel kullanım/hedefleme bilgileri (Kullanıcı ve hedeflenen ve gerekli)  

    -   Uygulama dağıtım bilgileri (yükleme/kaldırma, onay gerekiyor ve Kullanıcı etkileşimi etkin/devre dışı)  

    -   Mevcut uygulama isteği istatistikleri  

    -   Türe göre paket sayısı  

    -   İşletim sistemine göre uygulama uygulanabilirliği sayısı  

    -   Paket/program dağıtımı sayısı  

    -   App-V ortamları ve dağıtım özellikleri sayısı  

    -   Windows 10 lisanslı uygulama lisansı sayısı  

    -   Kullanıcıya/cihaza göre en düşük/en yüksek/ortalama uygulama dağıtım sayısı  

    -   Bakım penceresi türü ve süresi  

-   **İstemcilerinin**  

    -   Etkinleştirilmiş istemci aracıları listesi/sayısı  

    -   Kaynak konum türlerinden gelen istemci yüklemelerinin sayısı  

    -   İstemci yüklemesi hatalarının sayısı  

-   **Uyumluluk ayarları:**  

    -   Türe göre yapılandırma öğesi sayısı  

    -   Temel yapılandırma temeli bilgileri (sayısı, dağıtım sayısı ve başvuru sayısı)  

    -   Yerleşik ayarlara başvuran dağıtımların sayısı (ayarın değeri yakalanmaz)  

    -   Özel ayarlar için oluşturulan kuralların ve dağıtımların sayısı  

    -   Dağıtılan Basit Sertifika Kayıt Protokolü şablonlarının sayısı  

-   **İçeriði**  

    -   Türe göre sınır sayısı  

    -   Sınır grubu bilgileri (her sınır grubuna atanan sınır ve site sistemi sayısı)  

    -   Dağıtım noktası grubu bilgileri (her dağıtım noktası grubuna atanan paket ve dağıtım noktası sayısı)  

    -   Dağıtım noktası yapılandırma bilgileri (dal önbelleği ve dağıtım noktası izlemenin kullanımı)  

    -   Dağıtım Yöneticisi yapılandırma bilgileri (iş parçacıkları, yeniden deneme gecikmesi, yeniden deneme sayısı ve istek temelli dağıtım noktası ayarları)  

-   **Endpoint Protection:**  

    -   Kötü amaçlı yazılımdan koruma ve Windows Güvenlik Duvarı İlkesi kullanımını Endpoint Protection (gruba atanan benzersiz ilkelerin sayısı)<br /><br />Bu, ilkeye dahil olan ayarlar hakkında hiçbir bilgi içermez.  

    -   Endpoint Protection dağıtım hataları (Endpoint Protection İlkesi dağıtımı hata kodlarının sayısı)  

    -   Endpoint Protection panosunda görünmesi için seçilen koleksiyonların sayısı  

    -   Endpoint Protection özelliği için yapılandırılmış uyarı sayısı  

-   **Mobil uygulama yönetimi (MAM):**  

    -   İşletim sistemine göre MAM özellikli Office uygulamalarının, iş kolu uygulamalarının ve ilkelerin sayısı  

    -   MAM uygulama/ilke dağıtımı sayısı  

    -   MAM ayarı başına oluşturulan kural sayısı  

-   **Mobil cihaz yönetimi (MDM):**  

    -   Verilen mobil cihaz eylemlerinin sayısı: kilitleme, PIN Rest, temizleme ve devre dışı bırakma komutları

    -   Configuration Manager ve Microsoft Intune tarafından yönetilen mobil cihaz sayısı ve nasıl kaydedildikleri (toplu veya Kullanıcı tabanlı)  

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

-   **SQL/performans verileri:**  

    -   En büyük veritabanı tablolarının sayısı  

    -   Her Zaman Açık SQL çoğaltma bilgileri  

    -   Türe göre koleksiyon sayısı  

##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Düzey 3 - Tam  
Tam düzey, temel ve gelişmiş düzeylerdeki tüm verileri içerir. Aynı zamanda Uç Nokta Koruma, güncelleştirme uyumluluğu yüzdeleri ve yazılım güncelleştirme bilgileri hakkında ek bilgiler de içerir. Bu düzey, yakalama sırasında bellekte veya günlük dosyalarında bulunan kişisel bilgileri içerebilen sistem dosyaları ve bellek anlık görüntüleri gibi gelişmiş tanı bilgilerini de içerebilir.  

Configuration Manager sürüm 1511 ' den başlayarak bu düzey aşağıdakileri içerir:  

-   Koleksiyon değerlendirme ve yenileme istatistikleri  

-   Uç Nokta Koruma durum özeti (korunan, risk altında olan, bilinmeyen ve desteklenmeyen istemci sayısı dahil)  

-   Uç Nokta Koruma ilkesi yapılandırma  

-   Yazılım güncelleştirme dağıtım bilgileri (istemci ile UTC zamanına göre hedeflenen dağıtım yüzdesi, gerekli ve isteğe bağlı ve sessiz ve yeniden başlatma gizleme)  

-   Yazılım güncelleştirme dağıtımlarının genel uyumluluğu  

-   Otomatik dağıtım kuralı değerlendirmesi zaman çizelgesi bilgileri  

-   Ağ erişimi koruma ilkelerine sahip istemci sayısı  

-   Yazılım güncelleştirme dağıtımı hata kodları ve sayısı  

-   Yazılım güncelleştirme dağıtımı koleksiyonlarında etkin olmayan istemcilerin en düşük/en yüksek/ortalama sayısı  

-   Zaman aşımına uğradı yazılım güncelleştirmeleri olan grupların sayısı  

-   Yazılım güncelleştirmelerinin paket başına en düşük/en yüksek/ortalama sayısı  

-   Yazılım güncelleştirme taraması başarı yüzdeleri  

-   Son güncelleştirmeden bu yana geçen en düşük/en yüksek/ortalama saat sayısı  
