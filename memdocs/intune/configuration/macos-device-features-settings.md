---
title: Microsoft Intune-Azure 'da macOS cihaz özelliği ayarları | Microsoft Docs
description: MacOS cihazlarını AirPrint için yapılandırma ayarlarına bakın ve Microsoft Intune içindeki güç düğmelerini göstermek veya gizlemek için oturum açma penceresini özelleştirin. Ağınızdaki bir AirPrint sunucusunun IP adresini, yolunu ve bağlantı noktası ayarlarını almak için adımlara bakın. MacOS cihaz özelliklerini yapılandırmak için bu ayarları bir cihaz yapılandırma profilinde kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
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
ms.openlocfilehash: 9d4bc2de9e16cfcf9322cf343badafe3c9a35c70
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428913"
---
# <a name="macos-device-feature-settings-in-intune"></a>Intune 'da macOS cihaz özelliği ayarları

Intune, macOS cihazlarınızdaki özellikleri özelleştirmek için yerleşik ayarlar içerir. Örneğin, Yöneticiler AirPrint yazıcıları ekleyebilir, kullanıcıların oturum açma biçimini seçebilir, güç denetimlerini yapılandırabilir, çoklu oturum açma kimlik doğrulaması kullanabilir ve daha fazlasını yapabilir.

Bu özellikleri, macOS cihazlarını mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak denetlemek için kullanın.

Bu makale, bu ayarları listeler ve her ayarın ne yaptığını açıklar. Ayrıca, Terminal uygulaması 'nı (öykünücü) kullanarak AirPrint yazıcılarının IP adresini, yolunu ve bağlantı noktasını almak için gereken adımları listeler. Cihaz özellikleri hakkında daha fazla bilgi için [iOS/ıpados veya macOS cihaz özelliği ayarları ekle](device-features-configure.md)' ye gidin.

> [!NOTE]
> Kullanıcı arabirimi bu makaledeki kayıt türleriyle eşleşmeyebilir. Bu makaledeki bilgiler doğru. Kullanıcı arabirimi yaklaşan bir sürümde güncelleştiriliyor.

## <a name="before-you-begin"></a>Başlamadan önce

[MacOS cihaz özellikleri profili oluşturun](device-features-configure.md).

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

## <a name="login-items"></a>Oturum açma öğeleri

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Oturum açma sırasında başlatılacak dosyaları, klasörleri ve özel uygulamaları ekleyin**: kullanıcılar cihazlarında oturum açtıklarında açmak istediğiniz bir dosya, klasör, özel uygulama veya sistem uygulamasının yolunu **ekleyin** . Şunları da girin:

  - **Öğenin yolu**: dosya, klasör veya uygulamanın yolunu girin. Kuruluşunuz için oluşturulmuş veya özelleştirilmiş olan sistem uygulamaları veya uygulamalar genellikle `Applications` klasöründe, şuna benzer bir yol ile yapılır `/Applications/AppName.app` .

    Birçok dosya, klasör ve uygulama ekleyebilirsiniz. Örneğin şunu girin:   
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Herhangi bir uygulama, klasör veya dosya eklerken doğru yolu girdiğinizden emin olun. Tüm öğeler `Applications` klasörde değil. Kullanıcılar bir öğeyi bir konumdan diğerine taşıdıysanız yol değişir. Bu taşınan öğe, Kullanıcı oturum açtığında açılmaz.

  - **Gizle**: uygulamayı göstermeyi veya gizlemeyi seçin. Seçenekleriniz şunlardır:
    - **Yapılandırılmadı**: bu varsayılandır. Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcılar & gruplar oturum açma öğeleri listesindeki öğeleri gizleme seçeneği işaretsiz olarak gösterir.
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

- **SSO uygulama uzantısı türü**: KIMLIK bilgisi SSO uygulaması uzantısının türünü seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı**: uygulama uzantıları kullanılmıyor. Bir uygulama uzantısını devre dışı bırakmak için, SSO uygulama uzantısı türünü **Yapılandırılmadı**olarak değiştirin.
  - **Yeniden yönlendir**: SSO 'yu modern kimlik doğrulama akışlarıyla kullanmak için genel, özelleştirilebilir bir yeniden yönlendirme uygulama uzantısı kullanın. Kuruluşunuzun uygulama uzantısının uzantısını ve takım KIMLIĞINI öğrendiğinizden emin olun.
  - **Kimlik bilgisi**: sınama ve yanıt kimlik doğrulama akışlarıyla SSO 'yu kullanmak için genel, özelleştirilebilir bir kimlik bilgisi uygulama uzantısı kullanın. Kuruluşunuzun SSO uygulaması uzantısının uzantı KIMLIĞINI ve takım KIMLIĞINI öğrendiğinizden emin olun.  
  - **Kerberos**: MacOS Catalina 10,15 ve daha yeni bir sürüme dahil edilen Apple 'ın yerleşik Kerberos uzantısını kullanın. Bu seçenek, **kimlik bilgisi** uygulama uzantısının Kerberos 'a özgü bir sürümüdür.

  > [!TIP]
  > **Yeniden yönlendirme** ve **kimlik bilgisi** türleriyle, uzantıdan geçirilecek kendi yapılandırma değerlerinizi eklersiniz. **Kimlik bilgisi**kullanıyorsanız, **Kerberos** türünde Apple tarafından sunulan yerleşik yapılandırma ayarlarını kullanmayı göz önünde bulundurun.

- **UZANTı kimliği** (yeniden yönlendirme ve kimlik bilgisi): SSO uygulama uzantınızı tanımlayan paket tanımlayıcısını (gibi) girin `com.apple.ssoexample` .
- **Takım Kimliği** (yeniden yönlendirme ve kimlik bilgisi): SSO uygulama uzantınızın ekip tanımlayıcısını girin. Takım tanımlayıcısı, Apple tarafından oluşturulan ve gibi 10 karakterlik alfasayısal bir dizedir (sayılar ve harfler) `ABCDE12345` . 

  [Takım kimliğinizi bulun](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple 'ın Web sitesini açar) daha fazla bilgi içerir.

- **Bölge** (kimlik bilgileri ve Kerberos): kimlik doğrulama Realm adını girin. Bölge adı, gibi büyük harfli olmalıdır `CONTOSO.COM` . Genellikle, bölge adınız DNS etki alanı adınızla aynıdır, ancak tümü büyük harfle aynıdır.

- **Etki alanları** (kimlik bilgileri ve Kerberos): SSO aracılığıyla kimlik doğrulayabilecek sitelerin etki alanı veya ana bilgisayar adlarını girin. Örneğin, Web siteniz ise, `mysite.contoso.com` `mysite` ana bilgisayar adı ve `contoso.com` etki alanı adıdır. Kullanıcılar bu sitelerden birine bağlandıklarında, uygulama uzantısı kimlik doğrulama sınamasını işler. Bu kimlik doğrulaması, kullanıcıların oturum açmak için yüz KIMLIĞI, Touch ID veya Apple pincode/geçiş kodu kullanmasına izin verir.

  - Çoklu oturum açma uygulama uzantılarınızın Intune profillerindeki tüm etki alanları benzersiz olmalıdır. Farklı türlerde SSO uygulama uzantıları kullanıyor olsanız bile, bir etki alanını hiçbir oturum açma uygulama uzantısı profilinde tekrarlayamıyorum.
  - Bu etki alanları büyük/küçük harfe duyarlı değildir.

- **URL 'ler** (yalnızca yeniden yönlendir): kimlik SAĞLAYıCıLARıNıZıN URL öneklerini girin adına yeniden yönlendirme uygulama uzantısı SSO kullanır. Kullanıcılar bu URL 'lere yeniden yönlendirildiğinde, SSO uygulama uzantısı müdahale eder ve SSO istemlerini ister.

  - Intune çoklu oturum açma uygulama uzantısı profillerindeki tüm URL 'Lerin benzersiz olması gerekir. Farklı türlerde SSO uygulama uzantıları kullanıyor olsanız bile, hiçbir SSO uygulama uzantısı profilinde bir etki alanını tekrarlayabilirsiniz.
  - URL 'Lerin http://veya https://ile başlaması gerekir.

- **Ek yapılandırma** (yeniden yönlendirme ve kimlik bilgileri): SSO uygulama uzantısına geçirilecek uzantıya özgü ek veriler girin:
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
- **Windows Server Active Directory parola karmaşıklığı** (yalnızca Kerberos): kullanıcı parolalarının Active Directory parola karmaşıklığı gereksinimlerini karşılamasına zorlamak için **gerektir** ' i seçin. Daha fazla bilgi için bkz. [parolanın karmaşıklık gereksinimlerini karşılaması gerekir](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Active Directory parola gereksinimini karşılamasını gerektirmeyebilir.
- **Minimum parola uzunluğu** (yalnızca Kerberos): kullanıcıların parolalarını yapabilirler en az karakter sayısını girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcılara en az parola uzunluğu zorlayamayabilir.
- **Parola yeniden kullanım sınırı** (yalnızca Kerberos): etki alanında önceki bir parolanın yeniden kullanılabilmesi için kullanılması gereken yeni parola sayısını 1-24 ' dan girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parola yeniden kullanım sınırını zorlayamayabilir.
- **En az parola yaşı** (yalnızca Kerberos): kullanıcıların değiştirebilmesi için, etki alanında bir parolanın kullanılması gereken gün sayısını girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi değiştirilebilmesi için en az bir parola yaşı zorlamayamayabilir.
- **Parola süre sonu bildirimi** (yalnızca Kerberos): parolanın süresi dolmadan önce kullanıcıların parolasının süresinin dolacağını belirten gün sayısını girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi günleri kullanabilir `15` .
- **Parola kullanım süresi** (yalnızca Kerberos): cihaz parolasının değiştirilmesi gereken gün sayısını girin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sisteminin hiç bir parola süre sonu yoktur.
- **Parola değiştirme URL 'si** (yalnızca Kerberos): kullanıcılar bir Kerberos parolası değişikliği başlatdığındaki AÇıLAN URL 'yi girin.
- **Asıl ad** (yalnızca Kerberos): Kerberos sorumlusunun Kullanıcı adını girin. Bölge adını eklemeniz gerekmez. Örneğin, içinde `user@contoso.com` `user` asıl addır ve `contoso.com` bölge adıdır.

  > [!TIP]
  > - Ayrıca, küme ayraçları girerek asıl ad içindeki değişkenleri de kullanabilirsiniz `{{ }}` . Örneğin, Kullanıcı adını göstermek için girin `Username: {{username}}` . 
  > - Ancak, değişkenler kullanıcı arabiriminde doğrulanmamış ve büyük/küçük harfe duyarlı olduğundan değişken değiştirme konusunda dikkatli olun. Doğru bilgileri girdiğinizden emin olun.
  
- **Active Directory site kodu** (yalnızca Kerberos): Kerberos uzantısının kullanması gereken Active Directory sitenin adını girin. Kerberos uzantısı Active Directory site kodunu otomatik olarak bulagerekebilmeniz için bu değeri değiştirmeniz gerekebilir.
- **Önbellek adı** (yalnızca Kerberos): Kerberos önbelleğinin genel güvenlik HIZMETLERI (GSS) adını girin. Büyük olasılıkla bu değeri ayarlamanız gerekmez.  
- **Parola gereksinimleri iletisi** (yalnızca Kerberos): kuruluşunuzun, kullanıcılara gösterilen parola gereksinimlerinin bir metin sürümünü girin. İleti, Active Directory parola karmaşıklığı gereksinimlerine gerek duymuyorsanız veya en az parola uzunluğu girmezseniz görüntülenir.  
- **Uygulama paketi kimlikleri** (yalnızca Kerberos): cihazlarınızda çoklu oturum açma kullanması gereken uygulama paketi tanımlayıcılarını **ekleyin** . Bu uygulamalara Kerberos bilet verme bileti ve kimlik doğrulama bileti erişimi verilir. Uygulamalar, kullanıcıların erişim yetkisi oldukları hizmetler için de kimlik doğrular.
- **Etki alanı bölge eşlemesi** (yalnızca Kerberos): bölge ile eşleşmesi gereken etkı alanı DNS soneklerini **ekleyin** . Ana bilgisayarların DNS adları bölge adıyla eşleşmezse bu ayarı kullanın. Büyük olasılıkla bu özel etki alanı/bölge eşlemesini oluşturmanız gerekmez.
- **PKINIT sertifikası** (yalnızca Kerberos): Kerberos kimlik doğrulaması Için kullanılabilecek Ilk kimlik doğrulaması (PKI) sertifikası Için ortak anahtar şifrelemesini **seçin** . Intune 'A eklediğiniz [PKCS](../protect/certficates-pfx-configure.md) veya [SCEP](../protect/certificates-scep-configure.md) sertifikaları arasından seçim yapabilirsiniz. Sertifikalar hakkında daha fazla bilgi için bkz. [Microsoft Intune kimlik doğrulaması için sertifikaları kullanma](../protect/certificates-configure.md).

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[İOS/ıpados](ios-device-features-settings.md)üzerinde cihaz özelliklerini de yapılandırabilirsiniz.
