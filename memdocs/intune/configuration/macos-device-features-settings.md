---
title: Microsoft Intune-Azure 'da macOS cihaz özelliği ayarları | Microsoft Docs
description: MacOS cihazlarını AirPrint için yapılandırma ayarlarına bakın ve Microsoft Intune içindeki güç düğmelerini göstermek veya gizlemek için oturum açma penceresini özelleştirin. Ağınızdaki bir AirPrint sunucusunun IP adresini, yolunu ve bağlantı noktası ayarlarını almak için adımlara bakın. MacOS cihaz özelliklerini yapılandırmak için bu ayarları bir cihaz yapılandırma profilinde kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c117da3962e791fe1cf23b591085aba00969cbc0
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815098"
---
# <a name="macos-device-feature-settings-in-intune"></a>Intune 'da macOS cihaz özelliği ayarları

Intune, macOS cihazlarınızdaki özellikleri özelleştirmek için yerleşik ayarlar içerir. Örneğin, Yöneticiler AirPrint yazıcıları ekleyebilir, kullanıcıların oturum açma biçimini seçebilir, güç denetimlerini yapılandırabilir, çoklu oturum açma kimlik doğrulaması kullanabilir ve daha fazlasını yapabilir.

Bu özellikleri, macOS cihazlarını mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak denetlemek için kullanın.

Bu makale, bu ayarları listeler ve her ayarın ne yaptığını açıklar. Ayrıca, Terminal uygulaması 'nı (öykünücü) kullanarak AirPrint yazıcılarının IP adresini, yolunu ve bağlantı noktasını almak için gereken adımları listeler. Cihaz özellikleri hakkında daha fazla bilgi için [iOS/ıpados veya macOS cihaz özelliği ayarları ekle](device-features-configure.md)' ye gidin.

> [!NOTE]
> Kullanıcı arabirimi bu makaledeki kayıt türleriyle eşleşmeyebilir. Bu makaledeki bilgiler doğru. Kullanıcı arabirimi yaklaşan bir sürümde güncelleştiriliyor.

## <a name="before-you-begin"></a>Başlamadan önce

[MacOS cihaz özellikleri yapılandırma profili](device-features-configure.md)oluşturun.

> [!NOTE]
> Bu ayarlar, bazı ayarların tüm kayıt seçeneklerine uygulanmasıyla farklı kayıt türleri için geçerlidir. Farklı kayıt türleri hakkında daha fazla bilgi için bkz. [MacOS kaydı](../enrollment/macos-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **AirPrint hedefleri**: kullanıcıların cihazlarından yazdırabileceği bir veya daha fazla AirPrint yazıcısı **ekleyin** . Şunları da girin:
  - **Bağlantı noktası** (iOS 11.0 +, ıpados 13.0 +): AirPrint hedefinin dinleme bağlantı noktasını girin. Bu özelliği boş bırakırsanız AirPrint varsayılan bağlantı noktasını kullanır.
  - **IP adresi**: yazıcının IPv4 veya IPv6 adresini girin. Örneğin, `10.0.0.1` girin. Yazıcıları tanımlamak için konak adlarını kullanıyorsanız, Terminal uygulamasındaki yazıcıya ping ekleyerek IP adresini alabilirsiniz. [IP adresini ve yolunu](#get-the-ip-address-and-path) (Bu makalede) almak için daha fazla ayrıntı vardır.
  - **Yol**: yazıcının kaynak yolunu girin. Yol, genellikle `ipp/print` ağınızdaki yazıcılar içindir. [IP adresini ve yolunu](#get-the-ip-address-and-path) (Bu makalede) almak için daha fazla ayrıntı vardır.
  - **TLS** (iOS 11.0 +, ıpados 13.0 +): seçenekleriniz:
    - **Hayır** (varsayılan): AirPrint yazıcılarına bağlanılırken aktarım katmanı GÜVENLIĞI (TLS) zorlanmaz.
    - **Evet**: Aktarım katmanı GÜVENLIĞI (TLS) Ile AirPrint bağlantılarının güvenliğini sağlar.

- AirPrint yazıcılarının listesini içeren bir virgülle ayrılmış dosyayı (. csv) **Içeri aktarın** . Ayrıca, Intune 'A AirPrint yazıcıları ekledikten sonra bu listeyi **dışarı aktarabilirsiniz** .

### <a name="get-the-ip-address-and-path"></a>IP adresini ve yolu al

AirPrinter sunucuları eklemek için, yazıcının IP adresi, kaynak yolu ve bağlantı noktası gerekir. Aşağıdaki adımlarda bu bilgilerin nasıl alınacağı gösterilmektedir.

1. AirPrint yazıcıları ile aynı yerel ağa (alt ağ) bağlı bir Mac üzerinde, açık **Terminal** ( **/Applications/Utilities**).
2. Terminal uygulamasında yazın `ippfind` ve ENTER ' u seçin.

    Yazıcı bilgilerini aklınızda edin. Örneğin, şuna benzer bir şey döndürebilir `ipp://myprinter.local.:631/ipp/port1` . İlk bölüm, yazıcının adıdır. Son Bölüm ( `ipp/port1` ) kaynak yoludur.

3. Terminalde yazın `ping myprinter.local` ve ENTER ' u seçin.

   IP adresini aklınızda edin. Örneğin, şuna benzer bir şey döndürebilir `PING myprinter.local (10.50.25.21)` .

4. IP adresi ve kaynak yolu değerlerini kullanın. Bu örnekte, IP adresi `10.50.25.21` ve kaynak yolu olur `/ipp/port1` .

## <a name="associated-domains"></a>İlişkili etki alanları

Intune 'da şunları yapabilirsiniz:

- Birçok uygulamadan etki alanı ilişkilendirmesi ekleyin.
- Birçok etki alanını aynı uygulamayla ilişkilendirin.

Bu özellik şu platformlarda geçerlidir:

- macOS 10,15 ve üzeri

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: Kullanıcı tarafından onaylanan cihaz kaydı ve otomatik cihaz kaydı

- **İlişkili etki alanları**: etki alanınız ve uygulamanız arasında bir ilişki **ekleyin** . Bu özellik bir contoso uygulaması ile contoso Web sitesi arasında oturum açma kimlik bilgilerini paylaşır. Şunları da girin:

  - **Uygulama kimliği**: bir Web sitesiyle ilişkilendirilecek uygulamanın uygulama tanımlayıcısını girin. Uygulama tanımlayıcısı, takım KIMLIĞINI ve paket KIMLIĞINI içerir: `TeamID.BundleID` .

    Takım KIMLIĞI, uygulama geliştiricileriniz için Apple tarafından oluşturulan 10 karakterlik alfasayısal bir dizedir (harfler ve rakamlar) `ABCDE12345` . [Takım kimliğinizi bulun](https://help.apple.com/developer-account/#/dev55c3c710c)   (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

    Paket KIMLIĞI, uygulamayı benzersiz şekilde tanımlar ve genellikle ters etki alanı adı gösteriminde biçimlendirilir. Örneğin, Finder 'ın paket KIMLIĞI `com.apple.finder` . Paket KIMLIĞINI bulmak için terminalde AppleScript kullanın:

    `osascript -e 'id of app "ExampleApp"'`

  - **Etki alanı**: bir uygulamayla ilişkilendirilecek Web sitesi etki alanını girin. Etki alanı, bir hizmet türü ve gibi tam konak adı içerir `webcredentials:www.contoso.com` .

    `*.`Etki alanının başlangıcından önce (bir yıldız joker karakteri ve bir nokta) girerek ilişkili bir etki alanının tüm alt etki alanlarını eşleştirebilirsiniz. Süre gereklidir. Tam etki alanları joker etki alanlarından daha yüksek önceliğe sahiptir. Bu nedenle, tam alt etki *alanında bir eşleşme* bulunmazsa üst etki alanlarından desenler eşleştirilir.

    Hizmet türü şu olabilir:

    - **authsrv**: çoklu oturum açma uygulama uzantısı
    - **AppLink**: evrensel bağlantı
    - **WebCredentials**: parola otomatik doldurma

> [!TIP]
> MacOS cihazınızda sorun gidermek için **Sistem Tercihleri**  >  **profilleri**' ni açın. Oluşturduğunuz profilin cihaz profilleri listesinde olduğunu onaylayın. Listeleniyorsa, **Ilişkili etki alanı yapılandırmasının** profilde olduğundan emin olun ve doğru uygulama kimliği ve etki alanlarını içerir.

## <a name="content-caching"></a>İçerik önbelleğe alma

İçerik önbelleğe alma, içeriğin yerel bir kopyasını kaydeder. Bu bilgiler, Internet 'e bağlanmadan diğer Apple cihazları tarafından alınabilir. Bu önbelleğe alma, yazılım güncelleştirmelerini, uygulamaları, fotoğrafları ve diğer içerikleri ilk İndirildiklerinde kaydederek İndirmeleri hızlandırır. Uygulamalar bir kez indirildiğinden ve diğer cihazlara paylaşıldığından, çok sayıda cihazı olan okullar ve kuruluş bant genişliğini kaydeder.

> [!NOTE]
> Bu ayarlar için yalnızca bir profil kullanın. Bu ayarlarla birden çok profil atarsanız bir hata oluşur.
>
> İçerik önbelleği izleme hakkında daha fazla bilgi için bkz. [içerik önbelleğe alma günlüklerini ve Istatistiklerini görüntüleme](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (Apple 'ın Web sitesini açar).

Bu özellik şu platformlarda geçerlidir:

- macOS 10.13.4 ve üzeri

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

Bu ayarlar hakkında daha fazla bilgi için bkz. [Content Caching yük ayarları](https://support.apple.com/guide/mdm/content-caching-mdm163612d39/1/web/1) (Apple 'ın Web sitesini açar).

**İçerik önbelleğe almayı etkinleştir**: **Evet** , içerik önbelleğe almayı açar ve kullanıcılar bunu devre dışı bırakamıyorum. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kapatabilir.

- **Önbelleğe eklenecek Içerik türü**: seçenekleriniz:
  - **Tüm içerikler**: iCloud içeriğini ve paylaşılan içeriği önbelleğe alır.
  - **Yalnızca Kullanıcı içeriği**: kullanıcıların fotoğraflar ve belgeler de dahil olmak üzere iCloud içeriğini önbelleğe alır.
  - **Yalnızca paylaşılan içerik**: uygulamaları ve yazılım güncelleştirmelerini önbelleğe alır.

- **En büyük önbellek boyutu**: içeriği önbelleğe almak için kullanılan maksimum disk alanı miktarını (bayt cinsinden) girin. Boş bırakılırsa (varsayılan), Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu değeri sıfır () bayt olarak ayarlayabilir, bu da `0` önbelleğe sınırsız disk alanı sağlar.

  Cihazlarda bulunan alanı aşmayın emin olun. Cihaz depolama kapasitesi hakkında daha fazla bilgi için bkz. [iOS ve macOS rapor depolama kapasitesi](https://support.apple.com/HT201402) (Apple 'ın Web sitesini açar).

- **Önbellek konumu**: önbelleğe alınan içeriğin depolandığı yolu girin. Varsayılan konum `/Library/Application Support/Apple/AssetCache/Data` . Bu konumu değiştirmemenizi öneririz.

  Bu ayarı değiştirirseniz, önbelleğe alınan içeriğiniz yeni konuma taşınmaz. Otomatik olarak taşımak için, kullanıcıların cihazdaki konumu değiştirmesi gerekir (**Sistem Tercihleri**  >  **Paylaşım**  >  **içeriği önbelleğe alma**).

- **Bağlantı noktası**: 0-65535 ' dan itibaren, önbelleğin indirme ve karşıya yükleme isteklerini kabul etmesi IÇIN cihazlarda TCP bağlantı noktası numarasını girin. `0`Hangi bağlantı noktasının kullanılabilir olduğunu kullanmak için sıfır () (varsayılan) girin.
- **İnternet bağlantısı ve önbellek içerik paylaşımını engelleyin**: tethered önbelleğe alma olarak da bilinir. **Evet** , Internet bağlantısı paylaşımını engeller ve IOS/ıpados cihazları USB ile Mac 'e bağlı olarak önbelleğe alınmış içerik paylaşımını önler. Kullanıcılar bu özelliği etkinleştiremez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Internet bağlantı paylaşımını etkinleştir**: tethered önbelleği olarak da bilinir. **Evet** seçeneği, Internet bağlantısı paylaşımına izin verir ve IOS/ıpados cihazları USB ile Mac 'e bağlı olarak önbelleğe alınmış içeriği paylaşmaya izin verir. Kullanıcılar bu özelliği devre dışı bırakamıyorum. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu devre dışı kalabilir.

  Bu özellik şu platformlarda geçerlidir:

  - macOS 10.15.4 ve üzeri

- **İstemci ayrıntılarını günlüğe kaydetmek için önbelleği etkinleştir**: **Evet** , içerik isteyen cihazların IP adresini ve bağlantı noktası numarasını günlüğe kaydeder.Cihaz sorunlarını giderirken, bu günlük dosyası size yardımcı olabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu bilgileri günlüğe içermemelidir.

- **Sistem diğer uygulamalar için disk alanına ihtiyaç duyduğunda bile, her zaman önbellekten içerik tut**: **Evet** , önbellek içeriğini korur ve disk alanı azaldığında bile hiçbir şeyin silinmemesine neden olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi diğer uygulamalar için depolama alanı gerektiğinde otomatik olarak önbellekten içerik temizedebilir.

  Bu özellik şu platformlarda geçerlidir:

  - macOS 10,15 ve üzeri

- **Durum uyarılarını göster**: **Evet** , sistem bildirimleri olarak uyarı olarak gösterilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, IŞLETIM sistemi bu uyarıları sistem bildirimleri olarak göstermeyebilir.

  Bu özellik şu platformlarda geçerlidir:

  - macOS 10,15 ve üzeri

- **Önbelleğe alma açıkken Cihazın uyumasını engelleyin**: **Evet** seçeneği, önbelleğe alma açık olduğunda bilgisayarın uyku moduna geçmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazın uyku moduna geçmesine izin verebilir.

  Bu özellik şu platformlarda geçerlidir:

  - macOS 10,15 ve üzeri

- **Önbelleğe eklenecek cihazlar**: içeriği önbelleğe alabilir cihazları seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. 
  - **Aynı yerel ağı kullanan cihazlar**: içerik önbelleği aynı anlık yerel ağdaki cihazlara içerik sunar. Diğer ağlardaki cihazlara, içerik önbelleği tarafından erişilebilen cihazlar da dahil olmak üzere hiçbir içerik sunulmaz.
  - **Aynı genel IP adresini kullanan cihazlar**: içerik önbelleği, aynı genel IP adresini kullanarak cihazlara içerik sunar. Diğer ağlardaki cihazlara, içerik önbelleği tarafından erişilebilen cihazlar da dahil olmak üzere hiçbir içerik sunulmaz.
  - **Özel yerel ağlar kullanan cihazlar**: içerik önbelleği, girdiğiniz IP aralıklarında cihazlara içerik sağlar.
    - **İstemci dinleme aralıkları**: içerik ÖNBELLEĞINI alabilen IP adresleri aralığını girin.
  - **Geri dönüş ile özel yerel ağlar kullanan cihazlar**: içerik önbelleği, dinleme aralıklarında, eş dinleme aralıklarından ve üst öğe IP adreslerindeki cihazlara içerik sağlar.
    - **İstemci dinleme aralıkları**: içerik ÖNBELLEĞINI alabilen IP adresleri aralığını girin.

- **Özel genel IP adresleri**: bir dızı genel IP adresi girin. Bulut sunucuları, istemci cihazlarını önbellekler ile eşleştirmek için bu aralığı kullanır.

- **İçeriği diğer önbellekler Ile paylaşma**: Ağınızda birden fazla içerik önbelleği olduğunda, diğer cihazlardaki içerik önbellekleri otomatik olarak eşler haline gelir. Bu cihazlar, önbelleğe alınmış yazılımlara danışmayı ve bunları paylaşabilir. 

  Bir içerik önbelleğinde istenen bir öğe yoksa, öğenin eşlerini denetler. Öğe kullanılabiliyorsa, eş cihazdaki içerik önbelleğinden indirilir. Hala kullanılamıyorsa, içerik önbelleği öğeyi şuradan indirir:

  - Varsa, bir üst IP adresi
  
    VEYA
    
  - Apple 'dan Internet üzerinden

  Birden çok içerik önbelleği kullanılabilir olduğunda, cihazlar doğru içerik önbelleğini otomatik olarak seçer. 

  Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Aynı yerel ağları kullanan içerik önbellekleri**: içerik önbelleği yalnızca aynı anlık yerel ağdaki diğer içerik önbelleğiyle eşler.
  - **Aynı genel IP adresini kullanan içerik önbellekleri**: içerik önbelleği yalnızca aynı genel IP adresindeki diğer içerik önbelleğiyle eşler.
  - **Özel yerel ağlar kullanarak içerik önbellekleri**: yalnızca içerik önbelleği, girdiğiniz IP adresi dinleme aralığındaki diğer içerik önbelleğiyle eşler şunlardır:

    - **Eş dinleme aralıkları**: aralığınız için IPv4 veya IPv6 başlangıç ve bitiş IP adreslerini girin. İçerik önbelleği yalnızca girdiğiniz IP adresi aralıklarında içerik Önbelleklerinden gelen eş önbellek isteklerine yanıt verir.
    - **Eş filtresi aralıkları**: aralığınız için IPv4 veya IPv6 başlangıç ve bitiş IP adreslerini girin. İçerik önbelleği, girdiğiniz IP adresi aralıklarını kullanarak eşler listesini filtreler.

- **Üst IP adresleri**: üst önbellek olarak eklenecek başka bir içerik ÖNBELLEĞININ yerel IP adresini girin. Önbelleğiniz, Apple ile doğrudan karşıya yüklemek/indirmek yerine bu önbelleklere içerik yükler ve indirir. Yalnızca bir üst IP adresini bir kez ekleyin.
- **Üst seçim ilkesi**: çok sayıda üst önbellek olduğunda, üst IP adresinin nasıl seçili olduğunu seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Hepsini bir kez deneme**: üst IP adreslerini sırasıyla kullanın. Bu seçenek, Yük Dengeleme senaryolarında iyidir.
  - **İlk kullanılabilir**: her zaman listedeki Ilk kullanılabilir IP adresini kullanın.
  - **Karma**: istenen URL 'nin yol bölümü için bir karma değer oluşturur. Bu seçenek aynı URL için her zaman aynı üst IP adresinin kullanıldığından emin olur.
  - **Rastgele**: listede rastgele bir IP adresi kullanın. Bu seçenek, Yük Dengeleme senaryolarında iyidir.
  - **Yapışkan kullanılabilir**: her zaman LISTEDEKI ilk IP adresini kullanın. Kullanılabilir değilse, listede ikinci IP adresini kullanın. Mevcut olmadığından ikinci IP adresini kullanmaya devam edin, vb.

## <a name="login-items"></a>Oturum açma öğeleri

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Oturum açma sırasında başlatılacak dosyaları, klasörleri ve özel uygulamaları ekleme**: kullanıcılar cihazlarında oturum açtığında açılan bir dosya, klasör, özel uygulama veya sistem uygulamasının yolunu **ekleyin** . Şunları da girin:

  - **Öğenin yolu**: dosya, klasör veya uygulamanın yolunu girin. Kuruluşunuz için oluşturulmuş veya özelleştirilmiş olan sistem uygulamaları veya uygulamalar genellikle `Applications` klasöründe, şuna benzer bir yol ile yapılır `/Applications/AppName.app` .

    Birçok dosya, klasör ve uygulama ekleyebilirsiniz. Örneğin şunu girin:   
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Herhangi bir uygulama, klasör veya dosya eklerken doğru yolu girdiğinizden emin olun. Tüm öğeler `Applications` klasörde değil. Kullanıcılar bir öğeyi bir konumdan diğerine taşıdıysanız yol değişir. Bu taşınan öğe, Kullanıcı oturum açtığında açılmaz.

  - **Gizle**: uygulamayı göstermeyi veya gizlemeyi seçin. Seçenekleriniz şunlardır:
    - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcılar & gruplar oturum açma öğeleri listesindeki öğeleri gizleme seçeneği işaretsiz olarak gösterebilir.
    - **Evet**: kullanıcılar & gruplar oturum açma öğeleri listesinde uygulamayı gizler.

## <a name="login-window"></a>Oturum açma penceresi

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Menü çubuğunda ek bilgileri göster**: menü çubuğundaki saat alanı seçildiğinde, **Evet** ana bilgisayar adını ve MacOS sürümünü gösterir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu bilgileri menü çubuğunda göstermeyebilir.
- **Başlık**: cihazlarda oturum açma ekranında gösterilen bir ileti girin. Örneğin, kuruluş bilgilerinizi, bir hoş geldiniz iletisini, kayıp ve bulunan bilgileri girin ve bu şekilde devam edin.
- **Kullanıcı adı ve parola iste metin alanları**: kullanıcıların cihazlarda oturum açmasını seçin. **Evet** seçeneği, kullanıcıların bir Kullanıcı adı ve parola girmesini gerektirir. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir listeden Kullanıcı adını seçmesini ve sonra parolalarını yazmalarına gerek alabilir.

  Şunları da girin:

  - **Yerel kullanıcıları Gizle**: **Evet** , yerel kullanıcı hesaplarını, standart ve yönetici hesaplarını içerebilecek Kullanıcı listesinde göstermez. Yalnızca ağ ve sistem kullanıcı hesapları gösterilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Kullanıcı listesindeki yerel kullanıcı hesaplarını gösterebilir.
  - **Mobil hesapları Gizle**: **Evet** seçeneği, Kullanıcı listesinde mobil hesapları göstermez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, mobil hesapları Kullanıcı listesinde gösterebilir. Bazı mobil hesaplar, ağ kullanıcıları olarak gösterilebilir.
  - **Ağ kullanıcılarını göster**: Kullanıcı listesindeki ağ kullanıcılarını listelemek için **Evet** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Kullanıcı listesindeki ağ kullanıcı hesaplarını göstermez.
  - **Bilgisayarın yöneticilerini Gizle**: **Evet** seçeneği, yönetici kullanıcı hesaplarını Kullanıcı listesinde göstermez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Kullanıcı listesinde Yönetici Kullanıcı hesaplarını gösterebilir.
  - **Diğer kullanıcıları göster**: Kullanıcı listesindeki **diğer...** kullanıcılarını listelemek için **Evet** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Kullanıcı listesindeki diğer Kullanıcı hesaplarını göstermeyebilir.

- **Kapat düğmesini Gizle**: **Evet** , oturum açma ekranında Kapat düğmesini göstermez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kapalı düğmesini gösterebilir.
- **Yeniden başlatma düğmesini Gizle**: **Evet** , oturum açma ekranında yeniden Başlat düğmesini göstermez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi yeniden Başlat düğmesini gösterebilir.
- **Uyku düğmesini Gizle**: **Evet** , oturum açma ekranında uyku düğmesini göstermez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi uyku düğmesini gösterebilir.
- **Konsoldan Kullanıcı oturumunu devre dışı bırak**: **Evet** , oturum açmak için kullanılan MacOS komut satırını gizler. Tipik kullanıcılar için bu ayarı **Evet**olarak ayarlayın. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, gelişmiş kullanıcıların macOS komut satırını kullanarak oturum açmalarına izin verebilir. Konsol modunu girmek için, kullanıcılar `>console` Kullanıcı adı alanına girer ve konsol penceresinde kimlik doğrulaması yapılmalıdır.
- **Oturum açıkken kapatmayı devre dışı bırak**: **Evet** seçeneği, kullanıcıların oturum açtıklarında **kapatma** seçeneğini seçmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda **kapalı** menü öğesini seçmesine izin verebilir.
- **Oturum açıkken yeniden başlatmayı devre dışı bırak**: **Evet** seçeneği, kullanıcıların oturum açtıktan sonra **yeniden başlatma** seçeneğini seçmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda **Yeniden Başlat** menü öğesini seçmesine izin verebilir.
- **Oturum açıkken kapatmayı devre dışı bırak**: **Evet** seçeneği, kullanıcıların oturum açtıktan sonra **güç kapatma** seçeneğini seçmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda **güç kapatma** menü öğesini seçmesine izin verebilir.
- Oturum **açıkken oturum açmayı devre dışı bırak** (macos 10,13 ve üzeri): **Evet** seçeneği, kullanıcıların oturum açtıklarında oturum **kapatma** seçeneğini seçmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda **oturum kapatma** menü öğesini seçmesine izin verebilir.
- **Oturum açıkken kilit ekranını devre dışı bırak** (macos 10,13 ve üzeri): **Evet** seçeneği, kullanıcıların oturum açtıklarında **kilit ekranı** seçeneğini seçmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda **kilit ekranı** menü öğesini seçmesine izin verebilir.

## <a name="single-sign-on-app-extension"></a>Çoklu oturum açma uygulama uzantısı

Bu özellik şu platformlarda geçerlidir:

- macOS 10,15 ve üzeri

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: Kullanıcı tarafından onaylanan cihaz kaydı ve otomatik cihaz kaydı

- **SSO uygulama uzantısı türü**: SSO uygulama uzantısının türünü seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı**: uygulama uzantıları kullanılmıyor. Bir uygulama uzantısını devre dışı bırakmak için, SSO uygulama uzantısı türünü **Yapılandırılmadı**olarak değiştirin.
  - **Microsoft Azure AD**: 

    > [!IMPORTANT]
    > Microsoft Azure AD SSO uzantısı hala geliştirilmeye devam ediyor. Intune kullanıcı arabiriminde listelenir, ancak beklendiği gibi çalışmaz. SSO uygulama uzantısı türü için **Microsoft Azure AD** kullanmayın.

    , Bir yeniden yönlendirme türü SSO uygulama uzantısı olan Microsoft Enterprise SSO eklentisini kullanır. Bu eklenti, [Apple 'ın Kurumsal Çoklu oturum açma](https://developer.apple.com/documentation/authenticationservices) özelliğini destekleyen tüm MacOS uygulamalarında Active Directory hesapları için SSO sağlar. Azure AD kullanarak kimlik doğrulaması yapan Microsoft uygulamalarında, kuruluş uygulamalarında ve web sitelerinde SSO 'yu etkinleştirmek için bu SSO uygulama uzantısı türünü kullanın.

    SSO eklentisi, güvenlik ve Kullanıcı deneyimi iyileştirmeleri sunan gelişmiş bir kimlik doğrulama Aracısı işlevi görür.

    > [!IMPORTANT]
    > Microsoft Azure AD SSO uygulama uzantısı türüyle SSO sağlamak için, macOS Şirket Portalı uygulamasını cihazlara yüklersiniz. Şirket Portalı uygulaması, cihazlara Microsoft Enterprise SSO eklentisini sunar. MDM SSO uygulama uzantısı ayarları eklentiyi etkinleştirir. Şirket Portalı uygulaması ve SSO uygulama uzantısı profili cihazlara yüklendikten sonra, kullanıcılar kimlik bilgileriyle oturum açıp cihazlarında bir oturum oluşturur. Bu oturum, kullanıcıların kimlik doğrulamasını yapmasına gerek kalmadan farklı uygulamalar arasında kullanılır.
    >
    > Şirket Portalı uygulaması hakkında daha fazla bilgi için, bkz. [Şirket Portalı uygulamasını yüklediğinizde ve macOS cihazınızı Intune 'a kaydederseniz ne olur?](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md) Şirket Portalı uygulamasını [indirin](https://go.microsoft.com/fwlink/?linkid=853070) .

  - **Yeniden yönlendir**: SSO 'yu modern kimlik doğrulama akışlarıyla kullanmak için genel, özelleştirilebilir bir yeniden yönlendirme uygulama uzantısı kullanın. Kuruluşunuzun uygulama uzantısının uzantısını ve takım KIMLIĞINI öğrendiğinizden emin olun.
  - **Kimlik bilgisi**: sınama ve yanıt kimlik doğrulama akışlarıyla SSO 'yu kullanmak için genel, özelleştirilebilir bir kimlik bilgisi uygulama uzantısı kullanın. Kuruluşunuzun SSO uygulaması uzantısının uzantı KIMLIĞINI ve takım KIMLIĞINI öğrendiğinizden emin olun.  
  - **Kerberos**: MacOS Catalina 10,15 ve daha yeni bir sürüme dahil edilen Apple 'ın yerleşik Kerberos uzantısını kullanın. Bu seçenek, **kimlik bilgisi** uygulama uzantısının Kerberos 'a özgü bir sürümüdür.

  > [!TIP]
  > **Yeniden yönlendirme** ve **kimlik bilgisi** türleriyle, uzantıdan geçirilecek kendi yapılandırma değerlerinizi eklersiniz. **Kimlik bilgisi**kullanıyorsanız, **Kerberos** türünde Apple tarafından sunulan yerleşik yapılandırma ayarlarını kullanmayı göz önünde bulundurun.

- **UZANTı kimliği** (yeniden yönlendirme, kimlik bilgisi): SSO uygulama uzantınızı tanımlayan paket tanımlayıcısını (gibi) girin `com.apple.ssoexample` .
- **Takım Kimliği** (yeniden yönlendirme, kimlik bilgisi): SSO uygulama uzantınızın ekip tanımlayıcısını girin. Takım tanımlayıcısı, Apple tarafından oluşturulan ve gibi 10 karakterlik alfasayısal bir dizedir (sayılar ve harfler) `ABCDE12345` . 

  [Takım kimliğinizi bulun](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

- **Bölge** (kimlik bilgileri, Kerberos): kimlik doğrulama Realm adını girin. Bölge adı, gibi büyük harfli olmalıdır `CONTOSO.COM` . Genellikle, bölge adınız DNS etki alanı adınızla aynıdır, ancak tümü büyük harfle aynıdır.

- **Etki alanları** (kimlik bilgileri, Kerberos): SSO aracılığıyla kimlik doğrulayabilecek sitelerin etki alanı veya ana bilgisayar adlarını girin. Örneğin, Web siteniz ise, `mysite.contoso.com` `mysite` ana bilgisayar adı ve `contoso.com` etki alanı adıdır. Kullanıcılar bu sitelerden birine bağlandıklarında, uygulama uzantısı kimlik doğrulama sınamasını işler. Bu kimlik doğrulaması, kullanıcıların oturum açmak için yüz KIMLIĞI, Touch ID veya Apple pincode/geçiş kodu kullanmasına izin verir.

  - Çoklu oturum açma uygulama uzantılarınızın Intune profillerindeki tüm etki alanları benzersiz olmalıdır. Farklı türlerde SSO uygulama uzantıları kullanıyor olsanız bile, bir etki alanını hiçbir oturum açma uygulama uzantısı profilinde tekrarlayamıyorum.
  - Bu etki alanları büyük/küçük harfe duyarlı değildir.

- **URL 'ler** (yalnızca yeniden yönlendir): kimlik SAĞLAYıCıLARıNıZıN URL öneklerini girin adına yeniden yönlendirme uygulama uzantısı SSO kullanır. Kullanıcılar bu URL 'lere yeniden yönlendirildiğinde, SSO uygulama uzantısı müdahale eder ve SSO istemlerini ister.

  - Intune çoklu oturum açma uygulama uzantısı profillerindeki tüm URL 'Lerin benzersiz olması gerekir. Farklı türlerde SSO uygulama uzantıları kullanıyor olsanız bile, hiçbir SSO uygulama uzantısı profilinde bir etki alanını tekrarlayabilirsiniz.
  - URL 'Ler veya ile başlamalıdır `http://` `https://` .

- **Ek yapılandırma** (Microsoft Azure AD, yeniden yönlendirme, kimlik bilgileri): SSO uygulama uzantısına geçirilecek uzantıya özgü ek veriler girin:
  - **Anahtar**: eklemek istediğiniz öğenin adını girin, örneğin `user name` .
  - **Tür**: veri türünü girin. Seçenekleriniz şunlardır:

    - Dize
    - Boole: **yapılandırma değerinde**, veya girin `True` `False` .
    - Tamsayı: **yapılandırma değeri**alanına bir sayı girin.

  - **Değer**: verileri girin.
  
  - **Ekle**: yapılandırma anahtarlarınızı eklemek için seçin.

- **Anahtarlık kullanımı** (yalnızca Kerberos): parolaların anahtarlıkta kaydedilmesini ve saklanmasını engellemek için **Engelle** ' yi seçin. Engellenirse, kullanıcılardan parolasını kaydetmesi istenmez ve Kerberos anahtarının süresi dolarsa parolayı yeniden girmesi gerekir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parolaların anahtarlıkta kaydedilmesine ve depolanmasına izin verebilir. Anahtarın süresi dolarsa kullanıcılardan parolasını yeniden girmesi istenmez.
- **Yüz kimliği, Touch ID veya geçiş kodu** (yalnızca Kerberos): Kerberos biletini yenilemek için kimlik bilgisi gerektiğinde KULLANıCıLARıN yüz kimliğini, Touch ID 'sini veya cihaz geçiş kodunu girmesini **zorunlu** kılar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, Kerberos biletini yenilemek için kullanıcıların biyometri veya cihaz geçiş kodu kullanmasını gerektirmeyebilir. **Anahtarlık kullanımı** engellenirse, bu ayar uygulanmaz.
- **Varsayılan bölge** (yalnızca Kerberos): Girdiğiniz **bölge** değerini varsayılan bölge olarak ayarlamak Için **Etkinleştir** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi varsayılan bir bölge ayarlayamayabilir.

  > [!TIP]
  > - Kuruluşunuzda birden çok Kerberos SSO uygulama uzantısını yapılandırıyorsanız, bu ayarı **etkinleştirin** .
  > - Birden çok bölge kullanıyorsanız bu ayarı **etkinleştirin** . Girdiğiniz **bölge** değerini varsayılan bölge olarak ayarlar.
  > - Yalnızca bir bölge varsa, **Yapılandırılmadı** (varsayılan) olarak bırakın.

- Otomatik **bulma** (yalnızca Kerberos): **blok**olarak ayarlandığında, Kerberos uzantısı Active Directory site adını BELIRLEYEBILMEK için OTOMATIK olarak LDAP ve DNS kullanmaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi uzantının Active Directory site adını otomatik olarak bulmasına izin verebilir.
- **Parola değişiklikleri** (yalnızca Kerberos): **Block** , kullanıcıların, girdiğiniz etki alanlarında oturum açmak için kullandıkları parolaları değiştirmelerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parola değişikliklerine izin verebilir.  
- **Parola eşitleme** (yalnızca Kerberos): kullanıcılarınızın yerel PAROLALARıNı Azure AD 'ye eşitlemek için **Etkinleştir** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Azure AD 'ye parola eşitlemeyi devre dışı bırakabilir. Bu ayarı, SSO için alternatif veya yedekleme olarak kullanın. Kullanıcılar bir Apple mobil hesabıyla oturum açmışsa bu ayar çalışmaz.
- **Windows Server Active Directory parola karmaşıklığı** (yalnızca Kerberos): kullanıcı parolalarının Active Directory parola karmaşıklığı gereksinimlerini karşılamasına zorlamak için **gerektir** ' i seçin. Daha fazla bilgi için bkz. [parolanın karmaşıklık gereksinimlerini karşılaması gerekir](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Active Directory parola gereksinimini karşılamasını gerektirmeyebilir.
- **Minimum parola uzunluğu** (yalnızca Kerberos): kullanıcıların parolalarını yapabilirler en az karakter sayısını girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcılara en az parola uzunluğu zorlayamayabilir.
- **Parola yeniden kullanım sınırı** (yalnızca Kerberos): etki alanında önceki bir parolanın yeniden kullanılabilmesi için kullanılan yeni parola sayısını 1-24 ' dan girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parola yeniden kullanım sınırını zorlayamayabilir.
- **En az parola yaşı** (yalnızca Kerberos): kullanıcıların değiştirebilmesi için, etki alanında bir parolanın kullanıldığı gün sayısını girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi değiştirilebilmesi için en az bir parola yaşı zorlamayamayabilir.
- **Parola süre sonu bildirimi** (yalnızca Kerberos): parolanın süresi dolmadan önce kullanıcıların parolasının süresinin dolacağını belirten gün sayısını girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi günleri kullanabilir `15` .
- **Parola kullanım süresi** (yalnızca Kerberos): cihaz parolasının değiştirilmesi gereken gün sayısını girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sisteminin hiç bir parola süre sonu yoktur.
- **Parola değiştirme URL 'si** (yalnızca Kerberos): kullanıcılar bir Kerberos parolası değişikliği başlatdığındaki AÇıLAN URL 'yi girin.
- **Asıl ad** (yalnızca Kerberos): Kerberos sorumlusunun Kullanıcı adını girin. Bölge adını eklemeniz gerekmez. Örneğin, içinde `user@contoso.com` `user` asıl addır ve `contoso.com` bölge adıdır.

  > [!TIP]
  > - Ayrıca, küme ayraçları girerek asıl ad içindeki değişkenleri de kullanabilirsiniz `{{ }}` . Örneğin, Kullanıcı adını göstermek için girin `Username: {{username}}` . 
  > - Ancak, değişkenler kullanıcı arabiriminde doğrulanmamış ve büyük/küçük harfe duyarlı olduğundan değişken değiştirme konusunda dikkatli olun. Doğru bilgileri girdiğinizden emin olun.
  
- **Active Directory site kodu** (yalnızca Kerberos): Kerberos uzantısının kullanması gereken Active Directory sitenin adını girin. Kerberos uzantısı Active Directory site kodunu otomatik olarak bulagerekebilmeniz için bu değeri değiştirmeniz gerekebilir.
- **Önbellek adı** (yalnızca Kerberos): Kerberos önbelleğinin genel güvenlik HIZMETLERI (GSS) adını girin. Büyük olasılıkla bu değeri ayarlamanız gerekmez.  
- **Parola gereksinimleri iletisi** (yalnızca Kerberos): kuruluşunuzun, kullanıcılara gösterilen parola gereksinimlerinin bir metin sürümünü girin. İleti, Active Directory parola karmaşıklığı gereksinimlerine ihtiyaç duymuyorsanız veya en az parola uzunluğu girmezseniz gösterir.  
- **Paylaşılan cihaz modunu etkinleştir** (yalnızca Microsoft Azure AD): Azure AD 'nin paylaşılan cihaz modu özelliği Için yapılandırılmış MacOS cihazlarına MICROSOFT Enterprise SSO eklentisini dağıtıyorsanız **Evet** ' i seçin. Paylaşılan moddaki cihazlar birçok kullanıcının paylaşılan cihaz modunu destekleyen uygulamaların genel olarak oturum açmasını ve çıkmasına izin verir. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. 

  **Evet**olarak ayarlandığında, mevcut tüm Kullanıcı hesapları cihazlardan silinir. Veri kaybını önlemek veya fabrika sıfırlamasını önlemek için bu ayarın cihazlarınızı nasıl değiştirdiğinize emin olun.

  Paylaşılan cihaz modu hakkında daha fazla bilgi için bkz. [paylaşılan cihaz moduna genel bakış](/azure/active-directory/develop/msal-shared-devices).

- **Uygulama paketi kimlikleri** (Microsoft Azure AD, Kerberos): cihazlarınızda çoklu oturum açmayı kullanması gereken uygulama paketi tanımlayıcılarını **ekleyin** . Bu uygulamalara Kerberos bilet verme bileti ve kimlik doğrulama bileti erişimi verilir. Uygulamalar, kullanıcıların erişim yetkisi oldukları hizmetler için de kimlik doğrular.
- **Etki alanı bölge eşlemesi** (yalnızca Kerberos): bölge ile eşleşmesi gereken etkı alanı DNS soneklerini **ekleyin** . Ana bilgisayarların DNS adları bölge adıyla eşleşmezse bu ayarı kullanın. Büyük olasılıkla bu özel etki alanı/bölge eşlemesini oluşturmanız gerekmez.
- **PKINIT sertifikası** (yalnızca Kerberos): Kerberos kimlik doğrulaması Için kullanılabilecek Ilk kimlik doğrulaması (PKI) sertifikası Için ortak anahtar şifrelemesini **seçin** . Intune 'A eklediğiniz [PKCS](../protect/certficates-pfx-configure.md) veya [SCEP](../protect/certificates-scep-configure.md) sertifikaları arasından seçim yapabilirsiniz. Sertifikalar hakkında daha fazla bilgi için bkz. [Microsoft Intune kimlik doğrulaması için sertifikaları kullanma](../protect/certificates-configure.md).

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[İOS/ıpados](ios-device-features-settings.md)üzerinde cihaz özelliklerini de yapılandırabilirsiniz.