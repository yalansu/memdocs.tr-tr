---
title: Windows için yapılandırma öğeleri oluşturma
titleSuffix: Configuration Manager
description: Configuration Manager ' de şirket içi mobil cihaz yönetimi (MDM) ile Windows 10 bilgisayarlarının ayarlarını yönetmek için yapılandırma öğeleri oluşturun.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 26846066aa713d40fdacfe75810d43cafd1c3f04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693684"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Configuration Manager 'de şirket içi MDM ile Windows cihazları için yapılandırma öğeleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Şirket içi mobil cihaz yönetimi (MDM) ile yönettiğiniz Windows cihazlarının ayarlarını yönetmek için Configuration Manager **Windows 8.1 ve Windows 10** yapılandırma öğesini kullanın.

Configuration Manager uyumluluk ayarları hakkında daha fazla genel bilgi için aşağıdaki makalelere bakın:

- [Uyumluluk ayarlarını kullanmaya başlayın](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Uyumluluk ayarlarını planlayın ve yapılandırın](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Yapılandırma öğesi oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin ve ardından **yapılandırma öğeleri** düğümünü seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **yapılandırma öğesi oluştur**' u seçin.

1. **Yapılandırma öğesi oluşturma Sihirbazı**' nın **genel** sayfasında, aşağıdaki bilgileri belirtin:

    - **Ad**: Bu yapılandırma öğesini tanımlayacak benzersiz bir ad.

    - **Açıklama**: kullanımı hakkında daha fazla bilgi sağlayan isteğe bağlı bir açıklama.

    - **Configuration Manager istemcisi *olmadan* yönetilen cihazlar için ayarlar**altında **Windows 8.1 ve Windows 10**' u seçin.

    - **Kategoriler**: Configuration Manager konsolundaki yapılandırma öğelerini aramanıza ve filtrelemenize yardımcı olacak kategoriler oluşturabilir ve atayabilirsiniz.

1. Sihirbazın **Desteklenen platformlar** sayfasında, bu yapılandırma öğesini değerlendirmek Için belirli Windows platformlarını seçin.

1. **Cihaz ayarları** sayfasında, yapılandırmak istediğiniz ayar gruplarını seçin. Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Ayarlar başvurusu](#bkmk_setref).

    > [!TIP]
    > İstediğiniz ayar listelenmemişse **varsayılan ayar gruplarında olmayan ek ayarları yapılandırma**seçeneğini belirleyin. Bu seçenek, sihirbaza **ek ayarlar** sayfasını ekler.

1. Her ayar sayfasında, gerekli ayarları yapılandırın. Ayarları destekliyorsa, **uyumsuz ayarları**da düzeltebilirsiniz. Bir cihaz ayarı bu yapılandırma öğesiyle uyumlu değil olarak değerlendiriyorsa, bu ayar uyumlu olacak şekilde düzeltilecektir.

    Her ayar grubu için, ayar uyumsuz olduğunda rapor veren önem derecesini de yapılandırabilirsiniz. **Raporlar Için uyumsuzluk önem derecesi** için aşağıdaki değerlerden birini seçin:

    - **Hiçbiri**: Bu uyumluluk kuralında başarısız olan cihazlar Configuration Manager raporları için bir hata önem derecesi raporlamaz.

    - **Bilgi**

    - **Uyarı**

    - **Kritik**

    - **Kritik ve olayla**: Bu uyumluluk kuralında başarısız olan cihazlar Configuration Manager raporları için **kritik** hata önem derecesini raporlar. Ayrıca, uyumsuz durumu uygulama olay günlüğünde bir Windows olayı olarak günlüğe kaydeder.

1. Sihirbazın **Platform uygulanabilirliği** sayfasında, seçilen desteklenen platformlarla uyumlu olmayan tüm ayarları gözden geçirin. Geri dönüp bu ayarları kaldırın, destek platformlarını değiştirin veya devam edin.

    > [!IMPORTANT]
    > Cihazlar, desteklenmeyen ayarların uyumluluğunu değerlendirmeyin.

1. Sihirbazı tamamlayın.

Yeni yapılandırma öğesini, **Varlıklar ve Uyumluluk** çalışma alanındaki **Yapılandırma Öğeleri** düğümünde görüntüleyebilirsiniz.

## <a name="settings-reference"></a><a name="bkmk_setref"></a> Ayarlar başvurusu  

Aşağıdaki bölümler her bir grupta bulunan belirli ayarları ayrıntılandırır. Bu ayarları, Configuration Manager istemcisi *olmadan* yönetilen **Windows 8.1 ve Windows 10** cihazları Için **yapılandırma öğesi oluşturma Sihirbazı** ' nın **cihaz ayarları** sayfasında yapılandırın.

### <a name="password"></a>Parola

Bu ayarlar yalnızca Windows 10 ve üzeri sürümleri çalıştıran cihazlar içindir.

- **Cihazlarda parola ayarlarını gerektir**: desteklenen cihazlarda parola gerektir.
- **Minimum parola uzunluğu (karakter)**: parola için minimum uzunluk.
- **Gün cinsinden parola süre sonu**: kullanıcının parolasını değiştirmesi gereken gün sayısı.
- **Hatırlanan parola sayısı**: önceden kullanılan parolaların yeniden kullanılmasını önler.
- **Cihaz temizlenmeden önce başarısız oturum açma denemesi sayısı**: Bu sayıda oturum açma denemesi başarısız olursa, MDM cihazı siler
- **Cihazın kilitlenmesinden önce boşta kalma süresi**: bir cihazın kilitlenmeden önce boşta kalabileceği süreyi belirtin. Kullanıcı girişi olmadığında cihaz boşta kalır.
- **Parola karmaşıklığı**: gibi sayısal bir PIN belirtip belirtmeyeceğinizi `1234` ya da güçlü bir parola sağlamanız gerekip gerekmediğini seçin.
  - **Parolada gereken karmaşık karakter kümesi sayısı**: parola karmaşıklığı **güçlü**ise, parolanın kaç tane karakter türünü gerektirdiğini seçin: büyük harfler, küçük harfler, rakamlar veya semboller. Varsayılan olarak, bu değer `2` .
- **Parola kurtarma PIN'ini Exchange Server'a gönder**

### <a name="device"></a>Cihaz

- **Ekran yakalama**: kullanıcının cihaz görüntüsünün ekran görüntüsünü almaya izin vermek için bu ayarı etkinleştirin. (Yalnızca Windows 10)
- **Tanılama verileri gönderme**: Bu ayarı, analiz için Windows Tanılama verilerine izin vermek üzere etkinleştirin. (Yalnızca Windows 8.1)
- **Tanılama verisi göndermeye Izin ver (Windows 10)**: analizler için Windows Tanılama verilerinin düzeyini ayarlayın: Disable, BASIC, Enhanced veya Full. (Yalnızca Windows 10)
- **Coğrafi konum**: Cihazın konum hizmetleri bilgilerini kullanmasına izin vermek için bu ayarı etkinleştirin. (Yalnızca Windows 10)
- **Kopyala ve Yapıştır**: uygulamalar arasında veri aktarmak için kopyalama ve yapıştırmayı kullanmak üzere bu ayarı etkinleştirin. (Yalnızca Windows 10)
- **Fabrika Sıfırlaması**: kullanıcının cihazı ilk ayarlarına sıfırlamasına izin vermek için bu ayarı etkinleştirin. (Yalnızca Windows 10)
- **Bluetooth**: cihazın Bluetooth özelliğinin kullanımına izin verin veya bu özelliği yasaklaın.
- **Bluetooth bulunabilirlik modu**: cihazın diğer Bluetooth cihazları tarafından bulunmasına izin verin veya yasak olur. (Yalnızca Windows 10)
- **Bluetooth tanıtımı**: Bluetooth reklamcılık kullanımına izin verin veya bu özelliği yasakla. (Yalnızca Windows 10)
- **Ses kaydı**: cihazın ses kaydetme özelliklerinin kullanılmasına izin verin veya bu özelliği yasakla. (Yalnızca Windows 10)
- **Cortana**: Cortana sesli yardımcısının kullanımına izin verin veya bu kullanımı yasaklaın. (Yalnızca Windows 10)
- **Işlem merkezi bildirimleri**: Windows 10 ' da bildirim bölmesini etkinleştirin veya devre dışı bırakın. (Yalnızca Windows 10)
- **Bölge ayarlarının değiştirilmesi (yalnızca masaüstü)**: kullanıcının cihazdaki bölgesel ayarları değiştirmesine izin verin veya bunu yasaklayasaklayın.
- **Güç ve uyku ayarlarının değiştirilmesi (yalnızca masaüstü)**: kullanıcının cihazdaki güç ve uyku ayarlarını değiştirmesine izin verin veya bu ayarları yasakla.
- **Dil ayarlarının değiştirilmesi (yalnızca masaüstü)**: kullanıcının cihazdaki dil ayarlarını değiştirmesine izin verin veya bunu yasaklaın.
- **Sistem saati değişikliği**: kullanıcının cihaz tarih ve saatini değiştirmesini sağlar veya yasaklaın.
- **Cihaz adı değişikliği**: kullanıcının cihaz adını değiştirmesini sağlar veya yasaklaın.

### <a name="email-management"></a>E-posta yönetimi

Bu ayarlar, yalnızca Windows 8.1 ve Windows 10 çalıştıran cihazlara yöneliktir.  

- **Pop ve IMAP e-postası**: pop ve IMAP standartlarını kullanan e-posta hesaplarına bağlantılara izin verin veya bağlantıları yasakla.
- **E-postanın saklanacağı en uzun süre**: sunucu silinmeden önce e-posta saklama süresi.
- **Izin verilen ileti biçimleri**: e-postaların **düz metin** mi yoksa HTML mi yoksa **düz metin**mi olduğunu belirtin.
- **Düz metin e-postası Için maksimum boyut (otomatik olarak indirilen)**: otomatik olarak İndirildiklerinde düz metin e-postaların maksimum boyutunu ayarlayın.
- **HTML e-postası Için en büyük boyut (otomatik olarak indirilen)**: otomatik olarak INDIRILDIKLERINDE HTML e-postalarının en büyük boyutunu ayarlayın.
- **En büyük ek boyutu (otomatik olarak indirilen)**: otomatik olarak indirilen e-posta eklerinin maksimum boyutunu ayarlayın.
- **Takvim eşitleme**: takvimlere cihaz eşitlemesine izin verin veya bu cihazları yasakla.
- **Özel e-posta hesabı**: cihazda kurumsal olmayan bir e-posta hesabının kullanılmasına izin verin veya bu hesabı yasaklaın.
- **Microsoft hesabı 'Nı Windows Mail uygulamasında isteğe bağlı hale getir**: Windows Mail 'de bir Microsoft hesabı gerektirmeyen bu seçeneği etkinleştirin.

### <a name="store"></a>Depolama

Bu ayarlar yalnızca Windows 10 ve üzeri sürümleri çalıştıran cihazlar içindir.

- **Uygulama Mağazası**: cihazdaki Microsoft Store erişimine izin verin veya erişimi yasakla.
- **Uygulama deposuna erişmek için bir parola girin**: Bu seçeneği, kullanıcıların Microsoft Store uygulamasına erişmek için bir parola girmesini gerektirmek üzere etkinleştirin.
- **Uygulama içi satın almalar**: kullanıcıların uygulama içi satın alımlar yapmasına izin verin veya yasakla.
- **Mağaza kaynaklı uygulama başlatma**: cihazda önceden yüklenmiş olan veya Microsoft Store yüklü olan tüm uygulamaları devre dışı bırakın.
- **Mağaza 'dan uygulamaları otomatik güncelleştir**: Microsoft Store yüklenen uygulamaların otomatik olarak güncelleştirilmesini sağlar veya yasakla.
- **Uygulamaları sistem sürücüsüne yükler**: cihazın sistem sürücüsüne, genellikle sürücü olan uygulamaları yüklemesine izin verin veya bunu yasakla `C:` .
- **Uygulama verilerini sistem birimine yükler**: uygulamaların sistem sürücüsünde veri depolamasına izin vermek için bu seçeneği etkinleştirin.
- **Yalnızca özel mağazayı kullan**: kullanıcıların özel deponuzdan uygulama indirmesini gerektir.
- **Oyun DVR**: Windows oyun kaydını ve yayını devre dışı bırakma

### <a name="browser"></a>Tarayıcı

Bu ayarlar, yalnızca Windows 8.1 ve Windows 10 çalıştıran cihazlara yöneliktir.

- **Web tarayıcısına Izin ver**: cihazda Web tarayıcısının kullanılmasına izin verin veya bu tarayıcıyı yasaklaın.
- **Otomatik Doldur**: tarayıcıdaki otomatik tamamlama ayarlarının değiştirilmesine izin verin veya bu ayarları yasakla.
- **Etkin komut dosyası**: tarayıcının ActiveX betikleri gibi betikleri çalıştırıp çalıştıramayacağını izin verin veya yasakla.
- **Eklentiler: Internet**Explorer 'a eklentilerin eklenmesine izin verin veya bu eklentileri yasakla.
- **Açılır pencere engelleyicisi**: tarayıcı açılır pencere engelleyicisini izin verin veya yasakla.
- **Tanımlama bilgileri**: cihaza tanımlama bilgilerinin kaydedilmesine izin verin veya yasak olur.
- **Sahtekarlık uyarısı**: olası sahte web sitelerinin uyarılarını izin verin veya yasakla.

### <a name="internet-explorer"></a>Internet Explorer

Bu ayarlar, yalnızca Windows 8.1 ve Windows 10 çalıştıran cihazlara yöneliktir.

- **İzleme üst bilgisini her zaman gönder**: üçüncü taraf sitelere göz atma bilgileri gönderilmesine izin ver veya yasakla.
- **İntranet güvenlik bölgesi**: intranet güvenlik bölgesine güvenlik düzeyi atamaya izin verin veya bu izni yasakla.
- **Internet bölgesi Için güvenlik düzeyi**: yüksek, orta-yüksek veya orta internet bölgesi için güvenlik düzeyini ayarlayın.
- **İntranet bölgesi Için güvenlik düzeyi**: intranet bölgesi için güvenlik düzeyini ayarlayın: yüksek, orta-yüksek, orta, orta-düşük veya düşük.
- **Güvenilen siteler bölgesi Için güvenlik düzeyi**: güvenilir siteler bölgesi için güvenlik düzeyini ayarlayın: yüksek, orta-yüksek, orta, orta-düşük veya düşük.
- **Yasak siteler bölgesi Için güvenlik düzeyi**: Yasak siteler bölgesi için güvenlik düzeyini ayarlayın: yüksek.
- **İntranet bölgesi Için ad alanları**: Web sitelerini intranet bölgesine eklemek veya buradan kaldırmak için yapılandırın.
- **Tek sözcük girişi için intranet sitesine gidin**: Kullanıcı, önceki bir protokol olmadan geçerli bir site adı girerse, Internet Explorer 'ın bir intranet sitesine otomatik olarak gitmesini sağlar veya yasakla, örneğin `https://` .
- **Kuruluş modu menü seçeneği**: kullanıcıların Internet Explorer **Araçlar** menüsünden kuruluş modunu etkinleştirmesine ve devre dışı bırakmasına olanak sağlar.
  - **Rapor konumu günlüğe kaydediliyor (URL)**: kuruluş modu etkin olduğunda, ziyaret edilen Web sitelerini günlüğe kaydetmek IÇIN bir URL belirtin.
- **Kuruluş modu Site listesi konumu (URL)**: kuruluş modu etkin olduğunda, onu kullanan Web sitelerinin listesini belirtin.

### <a name="cloud"></a>Bulut

Bu ayarlar, yalnızca Windows 8.1 ve Windows 10 çalıştıran cihazlara yöneliktir.

- **Ayarları eşitleme**: cihazlar arasında ayarların eşitlenmesine izin ver veya yasakla.
- **Kimlik bilgileri eşitleme**: cihazlar arasında kimlik bilgilerinin eşitlenmesine izin verin veya yasakla.
- **Microsoft hesabı**: cihazda Microsoft hesabı kullanılmasına izin vermek için bu ayarı etkinleştirin.
- **Tarifeli bağlantılar üzerinden ayarları eşitleme**: ağ bağlantısı tarifeli olduğunda ayarların eşitlenmesine izin verin veya yasak olur.

### <a name="security"></a>Güvenlik

- **İmzasız dosya yüklemesi**: imzasız bir dosyayı kimlerin yükleyeerişebileceğini sağlar. (Yalnızca Windows 10)
- **İmzasız uygulamalar**: imzasız uygulamaların yüklenmesine izin verin veya bu uygulamaları yasakla. (Yalnızca Windows 10)
- **SMS ve MMS Mesajlaşma**: cihazda kısa mesaj protokollerine izin verin veya yasak. (Yalnızca Windows 10)
- **Çıkarılabilir depolama birimi**: SD kart gibi çıkarılabilir depolama biriminin kullanılmasına izin verin veya bunu yasaklayasaklayın. (Yalnızca Windows 10)
- **Kamera**: cihaz kamerasının kullanımına izin verin veya bu özelliği yasakla. (Yalnızca Windows 10)
- **Yakın alan iletişimi (NFC)**: NFC kullanarak iletişime izin verin veya erişimi yasakla. (Yalnızca Windows 10)
- **Hırsızlık önleme modu**: Windows 10 Anti hırsızlık modunun kullanılmasına izin verin veya bunu yasaklayasaklayın. (Yalnızca Windows 10)
- **USB bağlantısına Izin ver**: DIĞER cihazların USB bağlantısı kullanarak bu cihaza bağlanmasına izin verin veya bunu yasakla. (Yalnızca Windows 10)
- **WINDOWS RT VPN profili**: Windows RT cihazları IÇIN bir VPN profili sağlar (yalnızca Windows 8.1)

### <a name="peak-synchronization"></a>Yoğun eşitleme

Bu ayarlar yalnızca Windows 10 ve üzeri sürümleri çalıştıran cihazlar içindir.

- **Yoğun zamanı belirtin**: mobil cihaz eşitlemesi için haftanın yoğun saat ve günlerini ayarlayın.
- **Yoğun saatlerde eşitleme sıklığı**: en yoğun saatlerde eşitlemenin ne sıklıkta gerçekleşeceğini yapılandırın.
- **Yoğun olmayan saatlerde eşitleme sıklığı**: eşitlemenin yoğun saatlerin dışında ne sıklıkta gerçekleşeceğini yapılandırın.

### <a name="roaming"></a>Gezici

- **Dolaşım sırasında cihaz yönetimi**: Configuration Manager, dolaşım sırasında cihazı yönetmesini sağlar veya yasakla. (Yalnızca Windows 10)
- **Dolaşım sırasında yazılım indirme**: dolaşım sırasında uygulama ve yazılım indirmeye izin verin veya bunları yasakla. (Yalnızca Windows 10)
- **Dolaşım sırasında e-posta indirme**: dolaşım sırasında e-posta İndirmeleri sağlar veya yasakla. (Yalnızca Windows 10)
- **Veri dolaşımı**: verilere erişirken ağlar arasında dolaşıma izin verin veya yasakla.
- **Hücresel üzerinden VPN**: bir hücresel ağa BAĞLıYKEN cihazın VPN bağlantısı kullanmasına izin verin veya bu bağlantıyı yasakla. (Yalnızca Windows 10)
- **Hücresel üzerinden VPN dolaşımı**: cihazın hücresel ağda dolaşımda VPN bağlantısı kullanmasına izin verin veya bu bağlantıyı yasakla. (Yalnızca Windows 10)

### <a name="encryption"></a>Şifreleme

- **Depolama kartı şifrelemesi**: kullanıcının cihazda kullanılan herhangi bir depolama kartını şifrelemesini zorunlu kılmak için ' i ayarlayın. (Yalnızca Windows 10)
- **Cihazda dosya şifreleme**: cihazda depolanan dosyaları şifrelemek için üzerinde ayarlanır.
- **E-posta Imzalama gerektir**: Kullanıcı gönderilmeden önce e-postaları dijital olarak imzalayacağız.
  - **İmzalama algoritması**: e-postaları imzalama algoritmasını seçin: varsayılan, SHA veya MD5
- **E-posta şifrelemesi gerektir**: Kullanıcı gönderilmeden önce e-postaları şifrelemelidir.
  - **Şifreleme algoritması**: e-postaları şifrelemek için algoritmayı seçin: varsayılan, Üçlü DES, Des, RC2 128-BIT, RC2 64-BIT, RC2 40-bit

### <a name="wireless-communications"></a>Kablosuz iletişim

Bu ayarlar yalnızca Windows 10 ve üzeri sürümleri çalıştıran cihazlar içindir.

- **Kablosuz ağ bağlantısı**: Cihazın Wi-Fi özelliğine izin verin veya bu özelliği yasakla.
- **Wi-Fi internet paylaşımı**: kullanıcının cihazı bir mobil etkin nokta olarak kullanmasını etkinleştirin.
- **Mümkün olduğunda Wi-Fi ' y e veri boşaltma**: cihazı, Wi-Fi bağlantısını mümkün olduğunca kullanacak şekilde etkinleştirin.
- **Wi-Fi etkin nokta raporlama**: kullanıcının yakındaki bağlantıları bulmasına yardımcı olmak için Wi-Fi bağlantıları hakkında bilgi göndermesini sağlar.
- **El Ile Wi-Fi yapılandırması**: kullanıcının kablosuz bağlantıları el ile yapılandırmasını etkinleştirin.

#### <a name="configured-wireless-network-connections"></a>Yapılandırılmış kablosuz ağ bağlantıları

1. **Mobil cihaz kablosuz iletişim ayarlarını yapılandır** sayfasında **Ekle**' yi seçin.

1. **Kablosuz ağ bağlantısı** penceresinde, mobil cihazlarda sağlanacak kablosuz bağlantı hakkında aşağıdaki bilgileri belirtin:

    - **Ağ adı (SSID)**: Wi-Fi ağının adını girin.
    - **Ağ bağlantısı**: **Internet** veya **iş**seçeneklerinden birini belirleyin.
    - **Kimlik doğrulaması**: kablosuz bağlantı için kimlik doğrulama yöntemini seçin:
        - **Aç**
        - **Paylaşılan**
        - **WPA**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Veri şifreleme**: Bu bağlantı tarafından kullanılan şifreleme yöntemini seçin. Kullanılabilir değerler, seçtiğiniz **kimlik doğrulama** yöntemine göre değişir:
        - **Devre dışı**
        - **4**
        - **TKIP**
        - **AES**
    - **Anahtar dizini**: **WEP**'e **veri şifrelemesini** ayarladığınızda, **1** ile **4**arasında bir anahtar dizini seçin.
    - **Bu ağ internet 'e bağlanır**: bir kablosuz ağdaki mobil cihazların internet 'e bağlanmasına izin vermek için proxy ayarlarını sağlayın.
        - **Proxy sunucusu ayarları**: **http**, **WAP**ve **yuvalar** proxy 'leri için **sunucu** ve **bağlantı noktası** ayarlarını yapılandırın.
    - **802.1 x ayarları**:
        - **802.1 x ağ erişimini etkinleştir**: bir EAP türü belirterek bağlantıyı güvenli hale getirin.
        - **EAP türü**: aşağıdaki kimlik doğrulama protokollerinden birini seçin:
            - **PEAP**
            - **Akıllı kart veya sertifika**

### <a name="certificates"></a>Sertifikalar

Mobil cihazlara yüklenecek sertifikaları içeri aktarın.

**Içeri aktar**' ı seçin ve ardından aşağıdaki değerleri belirtin:

- **Sertifika dosyası**: içeri aktarılacak bir sertifika dosyasını (**. cer**) bulup seçin.
- **Hedef depo**: aşağıdaki sertifika mağazalarından birini veya daha fazlasını seçin:
  - **Asıl**
  - **CA**
  - **Olağan**
  - **Ayrıcalıklı**
  - **SPC**
  - **Eş**
- **Rol**: **SPC** (yazılım yayımcısı sertifikası) sertifika deposunu seçerseniz sertifikayla ilişkilendirilecek rolü seçin:
  - **Cep Telefonu Operatörü**
  - **Manager**
  - **Kimliği Doğrulanan Kullanıcı**
  - **BT Yöneticisi**
  - **Kimliği Doğrulanmayan Kullanıcı**
  - **Güvenilir Sağlama Sunucusu**

### <a name="system-security"></a>Sistem güvenliği

- **Kullanıcı hesabı denetimi**: cihazda Windows Kullanıcı hesabı denetimi davranışını yapılandırın.
- **Ağ güvenlik duvarı**: yerleşik güvenlik duvarını etkinleştirmek için Windows gerektir. (Windows 8.1)
- **Güncelleştirmeler**: Windows yazılım güncelleştirmelerinin davranışını yapılandırın. (Windows 8.1)
  - **Güncelleştirmelerin minimum sınıflandırması**: indirme ve yükleme için en düşük güncelleştirme sınıflandırmasını seçin: **hiçbiri**, **önemli**veya **Önerilen**.
- **Güncelleştirmeler (Windows 10)**: Windows yazılım güncelleştirmelerini davranışını yapılandırın. (Yalnızca Windows 10)
  - **Yükleme günü**: cihazın otomatik olarak güncelleştirme ve yeniden başlatma işlemlerini yüklediği zamanlanan günü seçin. (Yalnızca Windows 10)
  - **Yükleme saati**: cihazın otomatik olarak güncelleştirme ve yeniden başlatma işlemlerini yüklediği zamanlanan saati seçin. (Yalnızca Windows 10)
- **SmartScreen**: Windows akıllı ekranını etkinleştirin veya devre dışı bırakın.
- **Virüsten koruma**: Windows 'un virüsten koruma yazılımının olması gerekir.
- Virüsten **koruma imzaları**güncel: virüsten koruma imza dosyalarının güncel olduğundan emin olmanız gerekir.
- **Kilit ekranı bildirim görünümü**: kilit ekranında görüntülenecek bildirimleri etkinleştirir veya devre dışı bırakır.
- **Yayın öncesi Özellikler**: cihazın yayın öncesi ayarları ve özellikleri kabul edip etmediğini yapılandırın. (Yalnızca Windows 10)
- **El ile kök sertifika yükleme**: bir kök sertifikayı el ile yüklemek için kullanıcıyı etkinleştirin veya devre dışı bırakın. Bu, bu kök tarafından verilen tüm sertifikalar için güven sağlar. (Yalnızca Windows 10)
- **Elle kayıt kaldırmaya Izin ver**: Configuration Manager ile kullanıcının şirket içi mobil cihaz yönetiminden cihaz kaydını silme izni verin veya yasakla.

### <a name="windows-server-work-folders"></a>Windows Server İş Klasörleri

Bu ayarlar, yalnızca Windows 8.1 ve Windows 10 çalıştıran cihazlara yöneliktir.

- **Çalışma klasörleri URL 'si**: kullanıcıların cihazlarından bağlanabileceği bir Windows Server çalışma klasörünün konumunu belirtin.

### <a name="allowed-and-blocked-apps-list"></a>İzin verilen ve Engellenen uygulamalar listesi

Bu ayarlar yalnızca Windows Phone çalıştıran cihazlar içindir. Bu, şirket içi MDM Configuration Manager desteklemez. Daha fazla bilgi için bkz. [karma 'e ne oldu?](../understand/what-happened-to-hybrid.md).

### <a name="windows-10-team"></a>Windows 10 Team

Bu ayarlar yalnızca Windows 10 Team çalıştıran cihazlar içindir.

- **Sensörler odada birisini algıladığında ekranın otomatik olarak uyanmasına Izin ver**: algılayıcısı odada birisini algıladığında cihazın otomatik olarak uyanmasına izin ver veya yasakla.
- **Kablosuz Projeksiyon IÇIN PIN gerektir**: başka bir cihazın projeksiyon için kablosuz olarak BAĞLANABILMESI için PIN girmeniz gerekip gerekmediğini etkinleştirin veya devre dışı bırakın.
- **Bakım penceresi**: güncelleştirmeler cihaz yükleyip yeniden başlatıldığında pencereyi yapılandırmak için bu ayarı etkinleştirin.
  - **Başlangıç zamanı**: bakım penceresi için başlangıç saatini ayarlayın.
  - **Süre (saat)**: bakım penceresinin saat cinsinden uzunluğunu ayarlayın.
- **Azure operasyonel**içgörüler: [Azure operasyonel](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) Içgörüler, Windows 10 Team cihazlarından günlük dosyası verilerini toplama, depolama ve çözümleme için izin verir.
  - **Çalışma alanı kimliği**: geçerli bir çalışma alanı kimliği girin
  - **Çalışma alanı anahtarı**: ilişkili çalışma alanı için anahtarı girin
- **Miracast Kablosuz Projeksiyon**: Bu Windows 10 Team cihazında Miracast özellikli cihazlara proje yapmasına izin verin.
  - **Miracast kanalı**: içeriği proje Için bir Miracast kanalı seçin.
- **Karşılama ekranında görüntülenen toplantı bilgileri**: **hoş geldiniz** ekranının **toplantılar** kutucuğunda cihazın görüntülediği bilgi türünü seçin:
  - **Yalnızca düzenleyeni ve saati göster**
  - **Düzenleyeni, saati ve konuyu göster (özel toplantılar için konu gizlidir)**
- **Kilit ekranı arka plan resmi URL 'si**: bir Windows 10 Team cihazının **hoş geldiniz** ekranında özel bir arka plan göstermek için bir URL belirtin. URL 'YI ile başlatın `https://` ve PNG biçimini kullanın.

### <a name="windows-information-protection"></a>Windows Bilgi Koruması  

Configuration Manager ile kurumsal veri korumayı yapılandırma hakkında daha fazla bilgi için bkz. [Windows Information Protection (WIP) kullanarak kurumsal verilerinizi koruma](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### <a name="microsoft-edge-legacy"></a>Microsoft Edge eski

Bu ayarlar yalnızca Windows 10 ve üzeri sürümleri çalıştıran cihazlar içindir.  

- **Adres çubuğunda arama önerilerine Izin ver**: arama tümceciğe yazarken arama altyapısının siteler önermesine izin verin.
- **Izlememe Izin ver**: Web sitelerini ziyaret edip izlemelerinizi izlemesini istemediğiniz bildirin.
- **SmartScreen 'ı etkinleştir**: indirilen dosyaların kötü amaçlı kod içermediğini denetleyin.
- **Açılır pencerelere Izin ver**: tarayıcı açılır pencerelerini yapılandırın.
- **Tanımlama bilgilerine Izin ver**: tanımlama bilgilerinin kullanımını yapılandırın.
- **Otomatik doldurmaya Izin ver**: tarayıcının, formları ad, adres ve telefon gibi depolanan bilgileri otomatik olarak doldurmasına izin verin.
- **Parola yöneticisine Izin ver**: tarayıcının Web siteleri için parolaları depolayıp yönetmesine izin verin.
- **Geliştirici Araçları**: kenar geliştirici araçları 'nın özelliklerine izin verin veya bu özelliği yasakla.
- **Uzantılar**: kenar uzantılarına izin verin veya yasak.
- **InPrivate Gözatma**: geçmiş veya tanımlama bilgilerini Depolayameyen InPrivate gözatmaya izin verin veya yasakla.
- **WebRTC localhost IP adresi**: Kullanıcı Web RTC protokolünü kullanarak telefon araması yaptığında CIHAZıN localhost IP adresinin görüntülenmesini sağlar veya yasakla.
- **About: Flags öğesine erişimi engelle**: kullanıcının, `about:flags` Geliştirici ve deneysel ayarları içeren sayfaya erişmesine izin verin veya bunu engelleyin.
- **Dosyalar Için SmartScreen istemi geçersiz kılma**: kullanıcının kötü amaçlı olabilecek dosyaları Indirme hakkında SmartScreen Filtresi uyarılarını atlamasına izin verin veya bunu yasakla.
- **SmartScreen Prompt geçersiz kılma**: kullanıcının potansiyel olabilecek kötü amaçlı Web siteleri hakkında SmartScreen Filtresi uyarılarını atlamasına izin verin veya bunu yasakla.
- **İlk çalıştırma URL 'si**: bir Kullanıcı Ilk kez kenar açtığında görüntülenecek bir Web sitesi belirtin.

### <a name="windows-defender-antivirus"></a>Windows Defender Virüsten Koruma

Bu ayarlar yalnızca Windows 10 ve üzeri sürümleri çalıştıran cihazlar içindir.

- **Gerçek zamanlı Izlemeye Izin ver**: kötü amaçlı yazılım, casus yazılım ve diğer istenmeyen yazılım için gerçek zamanlı taramayı etkinleştirin.
- **Davranış Izlemeye Izin ver**: Defender, cihazlarda bazı bilinen şüpheli etkinlik düzenlerini denetler.
- **Ağ İnceleme sistemi etkinleştir**: ağ İnceleme SISTEMI (NIS), cihazları ağ tabanlı saldırılara karşı korumaya yardımcı olur. Kötü amaçlı trafiği algılamaya ve engellemeye yardımcı olmak için Microsoft Endpoint Protection Center’dan bilinen açıkların imzalarını kullanır.
- **Tüm Indirmeleri Tara**: Defender, internet 'ten indirdiği tüm dosyaları tarar.
- **Betik taramaya Izin ver**: Defender, Internet Explorer 'da kullanılan betikleri tarar.
- **Dosya ve program etkinliğini izle**: Defender, cihazlarda dosya ve program etkinliğini izler.
  - **Izlenen dosyalar**: İzlenecek dosyaların türünü seçin: tümü, gelen veya giden.
- **Çözümlenen kötü amaçlı yazılımın Izleneceği günler**: Defender, belirttiğiniz gün sayısı için çözümlenen kötü amaçlı yazılımları izlemeye devam eder. Bundan sonra, daha önce etkilenen cihazları el ile denetleyebilirsiniz. Gün sayısını 0 olarak ayarlarsanız, kötü amaçlı yazılım Karantina klasöründe kalır ve otomatik olarak kaldırılmaz. En büyük değer 90 ' dir.
- **ISTEMCI Kullanıcı arabirimi erişimine Izin ver**: Defender Kullanıcı arabiriminin kullanıcılardan gizlenmesi gerekip gerekmediğini denetler. Bu ayarı değiştirdiğinizde, cihaz bir dahaki sefer yeniden başlatıldığında etkili olur.
- **Sistem taraması zamanla**: seçtiğiniz gün ve saatte düzenli olarak gerçekleşen bir tam veya hızlı tarama seçin:
  - **Zamanlanan gün**: Defender 'ın taramayı çalıştırdığında zamanlanan günü seçin.
  - **Zamanlanan saat**: Defender 'ın taramayı çalıştırdığında zamanlanan saati seçin.
- **Günlük hızlı tarama zamanla**: Defender her gün bir hızlı tarama çalıştırdığında zamanlanan saati seçin.
- **Tarama SıRASıNDA CPU kullanımını sınırla**: bir tarama çalıştırıldığında, Defender 'ın kullandığı işlemcinin yüzdesini ayarlayın. 1 ile 100 arasında bir değer girin.
- **Arşiv dosyalarını Tara**: Defender,. zip veya. cab dosyaları gibi sıkıştırılmış arşivleri tarar.
- **E-posta Iletilerini Tara**: Defender, e-posta iletilerini cihaza geldikçe tarar.
- **Çıkarılabilir sürücüleri Tara**: Defender, USB sürücüleri gibi çıkarılabilir sürücüleri tarar.
- **Eşlenen sürücüleri Tara**: Defender, ağ paylaşımlarına eşlenmiş sürücüleri tarar. Örneğin, `H:` bir kullanıcının kişisel sürücüsüne eşlenir. Sürücüdeki dosyalar salt okunurdur, Defender bulduğu herhangi bir kötü amaçlı yazılımı kaldıramıyorum.
- Paylaşılan **Ağ klasörlerinden açılan dosyaları tara**: Defender, bir kullanıcı tarafından paylaşılan bir ağ yolundan açıldığında dosyaları tarar. Örneğin, `\\server\share\file.doc`. Paylaşımdaki dosya salt okunurdur, Defender bulduğu herhangi bir kötü amaçlı yazılımı kaldıramaz.
- **İmza güncelleştirme aralığı**: Defender 'ın yeni imza dosyalarını denetleyeceği zaman aralığını seçin.
- **Bulut korumasına Izin ver**: Defender, kötü amaçlı yazılım etkinliğiyle ilgili bilgi almak için Microsoft bulutunu kullanır ve ilk görüşnoktada blok gibi özellikleri etkinleştirir.
- **Örnek gönderimi için kullanıcılara sor**: dosyalar daha fazla analiz gerektirebilecek Defender için davranışı seçin. Örneğin, Defender kötü amaçlı olup olmadıklarını anlamak için dosyaları otomatik olarak Microsoft 'a gönderebilir.
- İstenmeyebilecek **uygulama algılaması**: cihazın, Defender tarafından olası istenmeyen olarak sınıflandırılan yazılımları çalıştırmaya karşı koruma sağlar. Çalıştıran bu uygulamalara karşı koruyabilirsiniz veya Kullanıcı, istenmeyebilecek bir uygulama yüklediğinde raporlamak için denetleme modunu kullanabilirsiniz.
- **Dosya ve klasör dışlamaları**: dışlamalar listesine bir veya daha fazla dosya ve klasör ekleyin. Örneğin `C:\Path` veya `%ProgramFiles%\Path\filename.exe` olabilir. Defender bu dosya ve klasörleri gerçek zamanlı veya zamanlanmış taramalara dahil etmez.
- **Dosya Uzantısı dışlamaları**: dışlamalar listesine bir veya daha fazla dosya uzantısı ekleyin. Örneğin `java` veya `exe` olabilir. Defender, hiçbir gerçek zamanlı veya zamanlanmış taramalarda bu uzantılara sahip herhangi bir dosya içermez.
- **İşlem Dışlamaları**: özel işlemleri dışlamalar listesine ekleyin. Örneğin, `C:\path\myproc.exe`. Bu dışlama türü yalnızca aşağıdaki uzantıları destekler: `exe` , `com` , veya `scr` . Defender, bu süreçler gerçek zamanlı veya zamanlanmış taramalara dahil etmez.

### <a name="additional-settings"></a>Ek ayarlar

Sihirbazın **cihaz ayarları** sayfasında, **varsayılan ayar gruplarında olmayan ek ayarları yapılandırma**seçeneğini belirlerseniz, bu ayarları yapılandırmak için bu **ek ayarlar** sayfasını kullanın. **Ekle** ' yi seçin ve kullanılabilir Mobil Ayarlar listesinden seçin. Yerleşik ayarını değiştirmek için **Seç** ' i veya özel bir kayıt defteri DEĞERI veya OMA URI ayarı türü oluşturmak Için **ayar oluştur** ' u seçin.

## <a name="next-steps"></a>Sonraki adımlar

[Uyumluluk ayarlarını izleme](../../compliance/deploy-use/monitor-compliance-settings.md)