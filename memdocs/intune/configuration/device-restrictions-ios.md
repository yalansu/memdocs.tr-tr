---
title: Microsoft Intune-Azure 'da iOS/ıpados cihaz ayarları | Microsoft Docs
titleSuffix: ''
description: İOS/ıpados cihazlarında ayarlar ekleme, yapılandırma veya oluşturma; parola gereksinimlerini ayarlama, kilitli ekranı denetleme, yerleşik uygulamalar kullanma, kısıtlı veya onaylanan uygulamalar ekleme, Bluetooth cihazlarını işleme, yedekleme ve depolama için buluta bağlanma, bilgi noktası modunu etkinleştirme, etki alanı ekleme ve kullanıcıların Microsoft Intune ' de Safari web tarayıcısıyla nasıl etkileşime gireceğini denetleme.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa3cf14b6afd8504a0918b5d61d2a7cae0c308b9
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093670"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune kullanarak özelliklere izin vermek veya erişimi kısıtlamak için iOS ve ıpados cihaz ayarları

Bu makalede iOS ve ıpados cihazlarında denetleyebileceğinizi belirten farklı ayarlar listelenir. Mobil cihaz yönetimi (MDM) çözümünüz kapsamında bu ayarları kullanabilir ve bu sayede özellikleri etkinleştirip devre dışı bırakabilir, parola kuralları uygulayabilir, belirli uygulamalara izin verebilir veya bunları kısıtlayabilir ve çok daha fazlasını yapabilirsiniz.

Bu ayarlar, Intune 'da bir cihaz yapılandırma profiline eklenir ve sonra iOS/ıpados cihazlarınıza atanır veya dağıtılır.

> [!TIP]
> Bu ayarlar Apple MDM ayarlarını kullanır. Bu ayarlar hakkında daha fazla bilgi için bkz. [Apple 'ın mobil cihaz yönetimi ayarları](https://support.apple.com/guide/mdm/welcome/web) (Apple 'ın Web sitesini açar).

## <a name="before-you-begin"></a>Başlamadan önce

[Cihaz kısıtlamaları yapılandırma profili oluşturma](device-restrictions-configure.md).

> [!NOTE]
> Bu ayarlar, bazı ayarların tüm kayıt seçeneklerine uygulanmasıyla farklı kayıt türleri için geçerlidir. Farklı kayıt türleri hakkında daha fazla bilgi için bkz. [iOS/ıpados kaydı](../enrollment/ios-enroll.md).

## <a name="general"></a>Genel

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Kullanım verilerini paylaşma**: **blok** cihazların Apple 'a tanılama ve kullanım verileri göndermesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu verilerin gönderilmesine izin verebilir.

- **Ekran yakalama**: **blok** , cihazlarda ekran görüntülerini veya ekran yakalamalarını engeller. İOS/ıpados 9,0 ve üzeri sürümlerde, ekran kayıtlarını da engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların ekran içeriğini bir görüntü veya video olarak yakalamasına izin verebilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **GÜVENILMEYEN TLS sertifikaları**: **engelleme** , cihazlarda güvenilmeyen Aktarım Katmanı Güvenliği (TLS) sertifikalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi TLS sertifikalarına izin verebilir.
- **Kablosuz PKI güncelleştirmelerini engelleyin**: **blok** , cihazların bir bilgisayara bağlı olmadığı durumlar dışında yazılım güncelleştirmelerini almasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bir bilgisayara bağlı kalmadan bir cihazın yazılım güncelleştirmelerini almasına izin verebilir.
- **Ad Izlemeyi sınırla**: **sınır** , cihaz reklam tanımlayıcısını devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi etkin durumda kalabilir.
- **Kurumsal Uygulama güveni**: **blok** , ayarlar > genel > profillerinin cihaz yönetimi & cihazlarda **Kurumsal Geliştirici güven** düğmesini kaldırır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların uygulama mağazasından indirilmemiş uygulamalara güvenmeyi seçebilmesine izin verebilir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Tanılama gönderme ayarları değişikliği**: **blok** kullanıcıların tanılama **ve kullanım** (cihaz ayarları) içindeki tanılama gönderme ve uygulama analizi ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu cihaz ayarlarını değiştirmesine izin verebilir.

  Bu ayarı kullanmak için, **kullanım verilerini paylaşma** ayarını **Engelle**olarak ayarlayın.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 9.3.2 ve üzeri
  - ıpados 13,0 ve üzeri

- **Sınıf uygulamasına göre uzak ekran**izleme: **blok** , sınıf uygulamasının cihazlarda ekranı uzaktan görüntülemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Apple derslik uygulamasının ekranı görüntülemesine izin verebilir.

  Bu ayarı kullanmak için **ekran yakalama** ayarını **Engelle**olarak ayarlayın.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 9,3 ve üzeri
  - ıpados 13,0 ve üzeri

- **Sınıf uygulamasına göre sorulmadan ekran izleme**: **izin ver** , öğretmenleri bilmeden ders uygulamasını kullanarak öğrencilerinin iOS/ıpados ekranlarını sessizce gözlemlemeye olanak tanır. Sınıf uygulamasını kullanan bir sınıfa kayıtlı öğrenci cihazları otomatik olarak bu kurs öğretme için izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği önleyebilir.

  Bu ayarı kullanmak için **ekran yakalama** ayarını **Engelle**olarak ayarlayın.

- **Hesap değişikliği**: **blok** , kullanıcıların iOS/ıpados ayarları uygulamasındaki cihaza özgü ayarları güncelleştirmesini engeller. Örneğin, kullanıcılar yeni cihaz hesapları oluşturamaz veya Kullanıcı adını veya parolayı değiştirebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarları değiştirmesine izin verebilir.

  Bu özellik ayrıca, e-posta, kişiler, takvim, Twitter ve daha fazlası gibi iOS/ıpados ayarları uygulamasından erişilebilen ayarlar için de geçerlidir. Bu özellik, Microsoft Outlook uygulaması gibi iOS/ıpados ayarları uygulamasından yapılandırılamayan hesap ayarlarına sahip uygulamalar için geçerlidir.

- **Ekran süresi**: **blok** kullanıcıların ekran zamanında (cihaz ayarları) kendi kısıtlamalarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda cihaz kısıtlamalarını (ebeveyn denetimleri veya içerik ve gizlilik kısıtlamaları gibi) yapılandırmasına izin verebilir.

  Bu ayar **Cihaz ayarlarında kısıtlamaları etkinleştirme** ayarının yeniden adlandırılmış halidir. Bu değişikliğin etkisi:  
  
  - iOS 11.4.1 ve üzeri: **Block** , kullanıcıların cihaz ayarlarında kendi kısıtlamalarını değiştirmesini engeller. Davranış aynıdır; ve kullanıcılar için herhangi bir değişiklik yoktur.
  - iOS 12,0 ve üzeri: **Block** , kullanıcıların, içerik ve gizlilik kısıtlamaları dahil cihaz ayarları 'Nda (ayarlar > genel > ekran süresi) kendi **ekran süresini** ayarlamalarına engel olur. iOS 12.0'dan yükseltilen cihazlar artık cihaz ayarlarında kısıtlamalar sekmesini (Ayarlar > Genel > Cihaz Yönetimi > Yönetim Profili > Kısıtlamalar) görmez. Bu ayarlar **Ekran Saati** altındadır.
  
- **Cihazdaki tüm içeriği ve ayarları silme seçeneğinin kullanımı**: **blok** cihazlarda tüm içeriği ve ayarları silme seçeneğinin kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcılara bu ayarlara erişim verebilir.
- **Cihaz adı değişikliği**: **blok** cihaz adının değiştirilmesini engelliyor. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazların adını değiştirmesine izin verebilir.
- **Bildirim ayarlarının değiştirilmesi**: **engelleme** , bildirim ayarlarının değiştirilmesini engelliyor. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihaz bildirim ayarlarını değiştirmesine izin verebilir.
- **Duvar kağıdı değişikliği**: **blok** duvar kağıdının değiştirilmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda duvar kağıdını değiştirmesine izin verebilir.
- **Yapılandırma profili değişiklikleri**: **blok** , cihazlarda yapılandırma profili değişikliklerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların yapılandırma profillerini yüklemelerine izin verebilir.
- **Etkinleştirme Kilidi**: **izin ver** , denetimli iOS/ıpados cihazlarında Etkinleştirme Kilidi olanak tanır. Etkinleştirme Kilidi, kaybolan veya çalınan bir cihazın yeniden etkinleştirilmesini zorlaştırır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Uygulama kaldırmayı engelle**: **blok** uygulamaların kaldırılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlardan uygulama kaldırmasına izin verebilir.
- **Cihaz KILITLIYKEN USB donatılara Izin ver**: **ızın ver** , USB aksesuarları 'nin bir saatten daha fazla kilitlenmiş cihazlarla veri alışverişi yapmasına olanak sağlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda USB kısıtlı modunu güncelleştirmeyebilir ve USB aksesuarları bir saatten daha fazla kilitliyse verileri cihazlardan aktarmaya engellenir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS/ıpados 11.4.1 ve daha yeni

- **Otomatik tarih ve saati zorla**: **gerekli** cihazların otomatik olarak tarih & zamanını ayarlamaya zorlar. Cihazın hücresel bağlantıları olduğunda veya konum hizmetleriyle arasında Wi-Fi etkinleştirildiğinde saat dilimi güncelleştirilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Öğrencilerden** **ayrılmaları için** öğrencilerin ders uygulamasını kullanarak yönetilmeyen bir kursa kaydolmaya izin istemesini gerektir: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğrenciye izin istemek üzere zoristememeyebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,3 ve üzeri
  - ıpados 13,0 ve üzeri

- **Sınıfa sormadan bir uygulamaya kilitleme ve cihazı kilitleme**olanağı sağlar: **Etkinleştir** , öğretmenin istenmeden uygulamaları kilitlemesine veya sınıf uygulamasını kullanarak cihazları kilitlemesine olanak tanır. Uygulamaları kilitlemek, cihazların yalnızca öğretmenlere belirtilen uygulamalara erişebileceği anlamına gelir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, öğretmenlerin öğrenciye sormadan sınıf uygulamasını kullanarak uygulamaları veya cihazları kilitlemesini engelleyebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **Sınıf sınıflarını sorulmadan otomatik olarak birleştir**: **Etkinleştir** otomatik olarak, öğrenciye sormadan derslik uygulamasında bir sınıfa katılmasına olanak tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğrencilerin ders uygulamasındaki bir sınıfa katılması istediğini öğretme isteyebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **VPN oluşturmayı engelle**: **blok** , kullanıcıların VPN yapılandırma ayarları oluşturmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda VPN oluşturmalarına izin verebilir.
- **Esım ayarlarını değiştirme**: **blok** cihazlarda esım 'ye bir hücresel plan kaldırmayı veya bu planı eklemeyi önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarları değiştirmesine izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 12,1 ve üzeri
  - ıpados 13,0 ve üzeri

- **Yazılım güncelleştirmelerini ertele**: **Etkinleştir** ayarı, cihazlarda 0-90 günden itibaren yazılım güncelleştirmeleri gösterildiğinde gecikmenizi sağlar. Bu ayar, güncelleştirmelerin yüklenme tarihini veya durumunu denetlemez.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda yazılım güncelleştirmelerini Apple yayınları olarak gösterebilir. Örneğin, bir iOS/ıpados güncelleştirmesi Apple tarafından belirli bir tarihte yayınlanmışsa, bu güncelleştirme doğal olarak yayın tarihi etrafında cihazlarda görüntülenir.  

  - **Yazılım güncelleştirmeleri gecikmesi**: 0-90 günden bir değer girin. Gecikme süresi sona erdiğinde, kullanıcılar gecikme tetiklendiğinde mevcut olan en eski işletim sistemi sürümüne güncelleştirme hakkında bildirim alırlar.

    Örneğin, iOS 12. a, **1 Ocak**'ta kullanılabilir ve **gecikme görünürlüğü** **5 güne**ayarlanmışsa, iOS 12. Kullanıcı cihazlarında kullanılabilir bir güncelleştirme olarak gösterilmez. Sürümden sonraki **altıncı gün** üzerinde, bu güncelleştirme kullanılabilir ve kullanıcılar uygulamayı yükleyebilir.

    Bu ayarın geçerli olduğu sürümler:  
    - iOS 11,3 ve üzeri
    - ıpados 13,0 ve üzeri

## <a name="password"></a>Parola

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Parola**: kullanıcıların cihazlara erişmek için parola girmesini **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parola girmeden cihazlara erişmelerine izin verebilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

> [!IMPORTANT]
> Kullanıcı tarafından kaydedilen cihazlarda, herhangi bir parola ayarını yapılandırırsanız, **basit parolalar** ayarları otomatik olarak **engelleme**olarak ayarlanır ve 6 basamaklı bir PIN zorlanır.
>
> Örneğin, **parola süre sonu** ayarını yapılandırır ve bu ilkeyi Kullanıcı tarafından kaydedilen cihazlara gönderirsiniz. Cihazlarda aşağıdakiler olur:
>
> - **Parola süre sonu** ayarı yok sayılır.
> - Veya gibi basit parolalara `1111` `1234` izin verilmez.
> - 6 basamaklı bir PIN zorlanır.

- **Basit parolalar**: **blok** daha karmaşık parolalar gerektirir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, ve gibi basit parolalara izin verebilir `0000` `1234` .

- **Gerekli parola türü**: kuruluşunuzun gerektirdiği gerekli parola karmaşıklığı düzeyini girin. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı**
  - **Sayısal**: parola yalnızca sayı olmalıdır, örneğin 123456789.
  - **Alfasayısal**: büyük harfler, küçük harfler ve sayısal karakterler içerir.
- **Paroladaki alfasayısal olmayan karakter sayısı**: 1-4 adresinden, parolada bulunması gereken simge karakterlerinin sayısını girin `#` `@` . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Minimum parola uzunluğu**: parolanın, 4-16 karakterden fazla olması gereken minimum uzunluğu girin. Kullanıcı kayıtlı cihazlarda 4 ila 6 karakter uzunluğunda bir uzunluk girin.
  
  > [!NOTE]
  > Kullanıcı kayıtlı cihazlarda, kullanıcılar 6 basamaktan daha büyük bir PIN ayarlayabilir. Ancak cihazlarda 6 ' dan fazla basamak uygulanmaz. Örneğin, bir yönetici minimum uzunluğu olarak ayarlar `8` . Kullanıcı tarafından kaydedilen cihazlarda, kullanıcılardan yalnızca 6 basamaklı bir PIN ayarlaması gerekir. Intune, Kullanıcı tarafından kaydedilen cihazlarda 6 basamaktan daha büyük bir PIN 'ı zorlamaz.

- **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: Cihaz silinmeden önce başarısız oturum açma işlemlerinin sayısını 4-11 adresinden girin.
  
  iOS/ıpados, bu ayarı etkileyebilecek yerleşik güvenliğe sahiptir. Örneğin, iOS/ıpados, oturum açma hatalarının sayısına bağlı olarak ilkeyi tetikleyebilir. Aynı zamanda aynı geçiş kodunu bir girişimlerle tekrar girmeyi de düşünebilirsiniz. Apple 'ın [iOS/ıpados Güvenlik Kılavuzu](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) (Apple 'ın Web sitesini açar) iyi bir kaynaktır ve Passcodes hakkında daha ayrıntılı bilgiler sağlar.
  
- **Parola istenmeden önce ekran kilitlenmesinden sonra geçen en fazla dakika**<sup>1</sup>: kullanıcıların parolasını yeniden girmesi gerekmeden önce cihazın ne kadar süreyle boşta kalacağını girin. Girdiğiniz süre cihazda şu anda ayarlanmış olan süreden uzunsa, cihaz girdiğiniz süreyi yoksayar.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 8.0 +
  - Idos 13.0 +

- **Ekran kilitlenmeden önce geçmesi gereken işlem yapılmayan dakika**sayısı<sup>1</sup>: ekran kilitlenmeden önce cihazlarda izin verilen en fazla dakika sayısını girin.

  **iOS/ıpados seçenekleri**:  

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Hemen**: 30 saniyelik işlem yapılmadan sonra ekran kilitleri.
  - **1**: 1 dakikalık bir işlem yapılmadan sonra ekran kilitleri.
  - **2**: 2 dakikalık bir işlem yapılmadan sonra ekran kilitleri.
  - **3**: 3 dakikalık bir işlem yapılmadan sonra ekran kilitleri.
  - **4**: 4 dakikalık bir işlem yapılmadan sonra ekran kilitleri.
  - **5**: 5 dakikalık bir işlem yapılmadan sonra ekran kilitleniyor.

  **ıpados seçenekleri**:  

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Hemen**: 2 dakikalık bir işlem yapılmadan sonra ekran kilitleri.
  - **2**: 2 dakikalık bir işlem yapılmadan sonra ekran kilitleri.
  - **5**: 5 dakikalık bir işlem yapılmadan sonra ekran kilitleniyor.
  - **10**: 10 dakikalık bir işlem yapılmadan sonra ekran kilitleniyor.
  - **15**: 15 dakika etkin olmadığında ekran kilitleri.

  Bir değer iOS ve ıpados için uygulanmazsa, Apple en yakın *En düşük* değeri kullanır. Örneğin, `4` dakika girerseniz, ıpados cihazları `2` dakika kullanır. `10`Dakikalar girerseniz, iOS cihazlarının `5` dakikaları kullanılır. Bu davranış bir Apple kısıtlamasıdır.
  
  > [!NOTE]
  > Bu ayar için Intune kullanıcı arabirimi iOS ve ıpados tarafından desteklenen değerleri birbirinden ayırır. Kullanıcı arabirimi gelecek bir sürümde güncelleştirilmiş olabilir.

- **Parola kullanım süresi (gün)**: cihaz parolasının, 1-65535 tarihinden önce değiştirilmesi gereken gün sayısını girin.
- **Önceki parolaların yeniden kullanılmasını engelle**: kullanıcıların daha önce kullanılan parolaları oluşturmasını kısıtlamak için bu ayarı kullanın. 1-24 adresinden, daha önce kullanılmış olan parolaların sayısını girin. Örneğin, kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için 5 girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Dokunma kimliği ve yüz kimliği kilit açma**: **blok** cihazların kilidini açmak için parmak izi veya yüz kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların biyometri kullanarak cihazların kilidini açmaya izin verebilir.

  Bu ayarı engellemek, cihazların kilidini açmak için çok yönlü kimlik doğrulamanın kullanılmasını da engeller.

  Yüz KIMLIĞI şu şekilde geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Geçiş kodu değişikliği**: **blok** geçiş kodunun değiştirilmesini, eklenmesini veya kaldırılmasını engeller. Bu özellik engellendikten sonra, denetimli cihazlarda geçiş kodu kısıtlamalarına yapılan değişiklikler yok sayılır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, geçiş kodlarını 'in eklenmesine, değiştirilmesine veya kaldırılmasına izin verebilir.

  - **Dokunma kimliği ve yüz kimliği değişikliği**: **blok** kullanıcıların TouchID parmak izleri ve yüz kimliğini değiştirmesini, eklemesini veya kaldırmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda TouchID parmak izlerini ve yüz KIMLIĞINI güncelleştirmesine izin verebilir.

    Bu ayarı engellemek, kullanıcıların çok yönlü kimlik doğrulamasını değiştirmelerini, eklemesini veya kaldırmasını de engeller.

    Yüz KIMLIĞI şu şekilde geçerlidir:  
    - iOS 11,0 ve üzeri
    - ıpados 13,0 ve üzeri

- **Parola Otomatik doldurmayı engelle**: **Block** , iOS/ıpados üzerinde parolaları otomatik doldur özelliğinin kullanılmasını önler. **Engelle** ayarını seçmek şu sonuçlara da neden olur:

  - Safari'de veya diğer uygulamalarda kullanıcılara parolaları kaydetmek isteyip istemedikleri sorulmaz.
  - Otomatik Güçlü Parolalar devre dışı bırakılır ve kullanıcılara güçlü parola önerisi sunulmaz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliklere izin verebilir.

- **Parola yakınlık Isteklerini engelle**: **blok** cihazların yakındaki cihazlardan parola istemelerine engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu parola isteklerine izin verebilir.
- **Parola paylaşmayı engelle**: **blok** , AirDrop kullanan cihazlar arasında parolaların paylaşılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parolaların paylaşılmasına izin verebilir.
- **Parola veya kredi kartı bilgileri Için dokunma kimliği veya yüz kimliği kimlik doğrulamasını gerektir otomatik doldurma**: parolaların veya kredi kartı bilgilerinin, Safari ve diğer uygulamalarda otomatik olarak doldurulabilmesi için, kullanıcıların TouchID veya çok yönlü kimliği kullanarak kimlik **doğrulaması yapmasını zorlar** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihaz ayarlarında bu özelliği denetlemesine izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri
  
<sup>1</sup> **parola istenmeden önce ekran kilitlenmesinden sonra ekran kilitlenmeden ve en fazla dakika geçtikten sonra** **işlem yapılmadan maksimum dakika** sayısını yapılandırdığınızda, bunlar sırayla uygulanır. Örneğin, her iki ayar için değeri **5** dakikaya ayarlarsanız ekran, beş dakika sonra otomatik olarak kapanır ve cihazlar ek beş dakikadan sonra kilitlenir. Ancak, kullanıcılar ekranı el ile kapalarsa ikinci ayar hemen uygulanır. Aynı örnekte, kullanıcılar ekranı kapattıktan sonra cihaz beş dakika sonra kilitlenir.

## <a name="locked-screen-experience"></a>Kilit Ekranı Deneyimi

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Cihaz kilitliyken denetim merkezi erişimi**: **blok** , Cihaz kilitliyken Denetim Merkezi uygulamasına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlar kilitlendiğinde Denetim Merkezi uygulamasına erişime izin verebilir.
- **Cihaz kilitliyken bildirimler**: **blok** , cihazlar kilitliyken bildirimlere erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazların kilidini açmadan bildirimlere erişime izin verebilir.
- **Cihaz kilitliyken bugün görünümü**: **blok** , cihazlar kilitliyken Bugün görünümüne erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, cihazlar kilitlendiğinde kullanıcıların bugün görünümünü görmesine izin verebilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Cihaz kilitliyken cüzdan bildirimleri**: **blok** , cihazlar kilitliyken cüzdan uygulamasına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, cihazlar kilitliyken cüzdan uygulamasına erişime izin verebilir.

## <a name="app-store-doc-viewing-gaming"></a>Uygulama Mağazası, Belge Görüntüleme, Oyun

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Yönetilmeyen uygulamalarda kurumsal belgeleri görüntüleme**: **blok** , şirket belgelerinin yönetilmeyen uygulamalarda görüntülenmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi şirket belgelerinin herhangi bir uygulamada görüntülenmesine izin verebilir.

  Örneğin kullanıcıların OneDrive uygulamasından Dropbox’a dosya kaydetmesini engellemek istiyorsunuz. Bu ayarı **Engelle** olarak yapılandırın. Cihazlar ilkeyi aldıktan sonra (örneğin, bir yeniden başlatmadan sonra), artık kaydetmeye izin vermez.

  > [!NOTE]
  > Bu ayar engellendiğinde, App Store 'dan yüklenen üçüncü taraf klavyeler de engellenir.

  - **Yönetilmeyen uygulamaların yönetilen kişiler hesaplarından okumasına Izin ver**: **izin ver** , yerleşik IOS/ıpados kişileri uygulaması gibi yönetilmeyen uygulamaların Outlook mobil uygulaması da dahil olmak üzere yönetilen uygulamalardan okuma ve bunlara erişme olanağı sağlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazlarda bulunan yerleşik Kişiler uygulamasında bulunan yinelenenleri kaldırma dahil olmak üzere okumayı önleyebilir.  
  
    Bu ayar, iletişim bilgilerinin okunmasına izin verir veya bunu engeller. Uygulamalar arasındaki kişileri eşitlemeyi denetlemez.
  
    Bu ayarı kullanmak için **Yönetilmeyen uygulamalarda kurumsal belgeleri görüntüleme** ayarını **Engelle** olarak belirtin.

  Bu iki ayar hakkında daha fazla bilgi edinmek ve iOS/ıpados 'a yönelik Outlook 'a yönelik etkileri için Outlook 'ta etkileri için bkz. [destek İpucu: iOS/ıpados yerel kişiler uygulamasıyla Intune özel profil ayarlarını kullanma](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **AirDrop 'u yönetilmeyen hedef olarak değerlendir**: **gerektir** AirDrop, yönetilmeyen bir bırakma hedefi olarak değerlendirilir. Yönetilen uygulamaların Airdrop'u kullanarak veri göndermesini durdurur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- Kurumsal **olmayan belgeleri kurumsal uygulamalarda görüntüleme**: **blok** kurumsal uygulamalarda kurumsal olmayan belgelerin görüntülenmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi şirket tarafından yönetilen uygulamalarda herhangi bir belgenin görüntülenmesine izin verebilir.

  **Block** Ayrıca, IOS için Outlook 'Ta/ıpados 'a yönelik kişileri dışarı aktarma eşitlemesini engeller. Daha fazla bilgi için bkz. [destek İpucu: IOS12 MDM denetimleriyle Outlook iOS/ıpados Iletişim eşitlemesini etkinleştirme](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Tüm satın alımlarda ITunes mağazası parolası gerektir**: kullanıcıların her uygulama Içi veya iTunes satın alma IÇIN Apple kimlik parolasını girmesini **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi her seferinde parola istemeden satın alma işlemlerine izin verebilir.
- **Uygulama içi satın alımlar**: **blok** uygulama içi satın alımlara engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, çalışan bir uygulama içinde mağaza satın alımlara izin verebilir.
- **IBook mağazasından ' erotik ' olarak işaretlenen Içerik indir**: **Block** , kullanıcıların, Erotika olarak etiketlenmiş IBook mağazasından medya indirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların "Erotika" kategorisiyle kitap indirmesine izin verebilir.
- **Yönetilen uygulamaların kişileri yönetilmeyen kişiler hesaplarına yazmalarına Izin ver**: **izin ver** , şirket Içi IOS/ıpados kişileri uygulamasına iş ve şirket kişileri de dahil olmak üzere, Outlook Mobile uygulaması gibi yönetilen uygulamaların yerleşik IOS/ıpados Kişiler uygulamasına kaydedilmesini sağlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, yönetilen uygulamaların cihazlardaki yerleşik iOS/ıpados kişileri uygulamasına iletişim bilgilerini kaydetmesini veya eşitlemesini önleyebilir.
  
  Bu ayarı kullanmak için **Yönetilmeyen uygulamalarda kurumsal belgeleri görüntüleme** ayarını **Engelle** olarak belirtin.

- **Derecelendirme bölgesi**: izin verilen İndirilenler için kullanmak istediğiniz derecelendirme bölgesini seçin. Ardından, **filmler**, **TV programları**ve **uygulamalar**için izin verilen derecelendirmeleri seçin.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **App Store**: **Block** , denetimli cihazlarda uygulama deposuna erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi erişime izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

  - **App Store 'dan uygulama yükleme**: **blok** , uygulama mağazasını cihaz giriş ekranında göstermez. Kullanıcılar, uygulamaları yüklemek için iTunes 'u veya Apple Configurator 'ı kullanmaya devam edebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi ana ekranda uygulama deposuna izin verebilir.
  - **Otomatik uygulama indirmeleri**: **blok** , diğer cihazlarda satın alınan uygulamaların otomatik olarak indirilmesini ve yeni uygulamalara otomatik güncelleştirme yapılmasını engeller. Mevcut uygulamalarında yapılan güncelleştirmeler bundan etkilenmez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, diğer iOS/ıpados cihazlarında satın alınan uygulamaların cihazda indirilip güncelleştirmesine izin verebilir.

- **Açık iTunes Music, podcast veya News içeriği**: **Block** açık iTunes Music, podcast veya News içeriğini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazın mağazadan yetişkinlere yönelik olarak derecelendirilmiş içeriğe erişmesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Game Center arkadaş ekleme**: **blok** kullanıcıların Game Center arkadaş eklemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Game Center arkadaş eklemesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Game Center**: Game Center uygulamasını kullanarak **engelleyin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda Game Center uygulamasının kullanılmasına izin verebilir.
- Çok **oyunculu oyunlar**: **blok** çok oyunculu oyunları önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda çok oyunculu oyunları oynamasına izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Dosyalar uygulamasında ağ sürücüsüne erişim**: sunucu ileti bloğu (SMB) protokolünü kullanarak, cihazlar bir ağ sunucusundaki dosyalara veya diğer kaynaklara erişebilir. **Devre dışı bırak ayarı** , BIR ağ SMB sürücüsündeki dosyalara erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi erişime izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="built-in-apps"></a>Yerleşik Uygulamalar

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Siri**: **Block** Siri 'e erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda Siri Voice Yardımcısı ile kullanılmasına izin verebilir.
  - **Siri Cihaz kilitliyken**: **blok** , cihazlar kilitliyken Siri 'e erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kilitlendiklerinde cihazlarda Siri Voice yardımcısını kullanmaya izin verebilir.

- **Safari sahtekarlık uyarıları**: cihazlarda Web tarayıcısında sahtekarlık uyarılarının gösterilmesi **gerekir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)


- **Internet 'ten sonuçları döndürmek Için Spotlight araması**: **Block** , projektörün bir Internet aramasından herhangi bir sonuç döndürmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Spotlight aramasının arama sonuçları sağlamak için Internet 'e bağlanmasına izin verebilir.

  Bu ayar Kullanıcı arabiriminde yinelenir ve yaklaşan bir sürümde düzeltilecektir. Şu anda bu ayar denetimli cihazlar için geçerlidir. Gelecekteki bir sürümde, bu ayar cihaz kayıtlı ve otomatik cihaz kayıtlı cihazları için geçerlidir ve gözetim gerektirmez.

- **Safari tanımlama bilgileri**: cihazlarda tanımlama bilgilerinin nasıl işlendiğini seçin. Seçenekleriniz şunlardır:
  - İzin Ver
  - Tüm tanımlama bilgilerini engelle
  - Ziyaret edilen web sitelerinin tanımlama bilgilerine izin ver
  - Geçerli web sitesinin tanımlama bilgilerine izin ver

- **Safari JavaScript**: **Block** tarayıcıda Java betikleri 'nin cihazlarda çalıştırılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Java betiklerine izin verebilir.

- **Safari açılır pencereleri**: **blok** , Safari Web tarayıcısında tüm açılır pencereleri engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi açılır pencere engelleyiciye izin verebilir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Kamera**: **blok** cihazdaki kameraya erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz kamerasına erişime izin verebilir.

  Intune yalnızca cihaz kamerasına erişimi yönetir. Resimlere veya videolara erişimi yoktur.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

  - Çok **yönlü saat**: **blok** , çok yönlü uygulamaya erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda çok yönlü bir zaman uygulamasına erişime izin verebilir.

    İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Siri küfür filtresi**: **gerektir** , Siri 'ın dikte etmesini veya küfürlü dilini kullanmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Bu ayarı kullanmak için **Siri** ayarını **Engelle**olarak ayarlayın.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri

- **Siri Kullanıcı tarafından oluşturulan içeriği Internet 'ten sorgulamak için**: **Block** , soruların yanıt vermesi için Web sitelerine erişmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Siri 'ın Kullanıcı tarafından oluşturulan içeriğe internet 'ten erişmesine izin verebilir.

  Bu ayarı kullanmak için **Siri** ayarını **Engelle**olarak ayarlayın.

- **Apple News**: **Block** cihazlarda Apple News uygulamasına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Apple News uygulamasının kullanılmasına izin verebilir.
- **IBOOKS Store**: **Block** , iBooks deposuna erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların IBook Store 'dan kitaplar 'a gözatmasına ve satın almaya izin verebilir.
- **Cihazdaki iletiler uygulaması**: **blok** , kullanıcıların IMessage için iletiler uygulamasını kullanmalarını engeller. Cihazlar SMS mesajlaşma 'yı destekliyorsa, kullanıcılar SMS kullanarak SMS mesajları gönderip alabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iletileri Internet üzerinden göndermek ve okumak için Iletiler uygulamasının kullanılmasına izin verebilir.
- **Pod yayınları**: **blok** , kullanıcıların Pod yayınları uygulamasını kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Pod yayınları uygulamasının kullanılmasına izin verebilir.
- **Müzik hizmeti**: **blok** , müzik uygulamasını klasik moda geri döndürür ve müzik hizmetini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Apple Music uygulamasının kullanılmasına izin verebilir.
- **ITunes Radio hizmeti**: **blok** iTunes Radyo uygulamasının kullanılmasını engelliyor. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iTunes Radio uygulamasının kullanılmasına izin verebilir.
- **iTunes Mağazası**: **blok** cihazlarda iTunes kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iTunes 'a izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 4,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **İPhone 'umu bul**: **Block** uygulamamda bu özelliği engelliyor. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazın yaklaşık konumunu almak için bu uygulama Bul özelliğini kullanmaya izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **Arkadaşlarımı bul**: **blok** , uygulamamda Bul özelliğini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, bir Apple cihazından veya iCloud.com aile ve arkadaşlar bulmak için bu uygulamamı Bul özelliğini kullanmaya izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **Arkadaşlarımı bul uygulama ayarlarında yapılan değişiklikler**: **Block** Arkadaşlarımı bul uygulama ayarlarında değişiklik yapılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Arkadaşlarımı Bul uygulamasının ayarlarını değiştirmesine izin verebilir.

- **Internet 'ten sonuçları döndürmek Için Spotlight araması**: **Block** , projektörün bir Internet aramasından herhangi bir sonuç döndürmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Spotlight aramasının arama sonuçları sağlamak için Internet 'e bağlanmasına izin verebilir.

  Bu ayar Kullanıcı arabiriminde yinelenir ve yaklaşan bir sürümde düzeltilecektir. Şu anda bu ayar denetimli cihazlar için geçerlidir. Gelecekteki bir sürümde, bu ayar cihaz kayıtlı ve otomatik cihaz kayıtlı cihazları için geçerlidir ve gözetim gerektirmez.

- **Cihazdan sistem uygulamalarının kaldırılmasını engelle**: **bloğu** , sistem uygulamalarını cihazlardan kaldırma yeteneğini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların sistem uygulamalarını kaldırmasına izin verebilir.

- **Safari**: cihazlarda Safari tarayıcısını kullanmayı **engelleyin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Safari tarayıcısını kullanmasına izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Safari otomatik doldurma**: **blok** cihazlarda otomatik doldurma özelliğini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Web tarayıcısında otomatik tamamlama ayarlarını değiştirmesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

## <a name="restricted-apps"></a>Kısıtlı uygulamalar

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Kısıtlanmış uygulamalar listesi türü**: Kullanıcıların yüklemesine veya kullanmasına izin verilmeyen uygulamaların bir listesini oluşturun. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi atadığınız uygulamalara ve yerleşik uygulamalara erişime izin verebilir.
  - **Yasaklanmış uygulamalar**: Kullanıcıların yüklemesine ve çalıştırmasına izin verilmeyen uygulamaları (Intune tarafından yönetilmeyen) listeleyin. Kullanıcıların yasaklanmış bir uygulamayı yüklemesi engellenmiyor. Bir Kullanıcı bu listeden bir uygulama yüklerse Intune 'da raporlanır.
  - **Onaylanan uygulamalar**: Kullanıcıların yüklemesine izin verilen uygulamaları listeleyin. Uyumluluğun korunması için kullanıcılar diğer uygulamaları yüklememelidir. Şirket Portalı uygulaması da dahil olmak üzere Intune tarafından yönetilen uygulamalara otomatik olarak izin verilir. Kullanıcıların onaylı uygulamalar listesinde olmayan bir uygulamayı yüklenmesi engellenmez. Ancak bunu yaptıysanız Intune 'da raporlanır.

Bu listelere uygulama eklemek için şunları yapabilirsiniz:

- İstediğiniz uygulamanın iTunes App mağazası URL'sini **ekleyin**. Örneğin, Microsoft çalışma klasörleri uygulamasını eklemek için `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` veya girin `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` .

  Uygulamanın URL'sini bulmak için, iTunes App Store'u açın ve uygulamayı arayın. Örneğin `Microsoft Remote Desktop` veya `Microsoft Word` için arama yapın. Uygulamayı seçin ve URL'sini kopyalayın.

  iTunes kullanarak da uygulamayı bulabilir ve ardından **Bağlantıyı Kopyala** görevini kullanıp uygulama URL’sini alabilirsiniz.

- URL 'SI dahil olmak üzere uygulamayla ilgili ayrıntılarla bir CSV dosyasını **Içeri aktarın** . `<app url>, <app name>, <app publisher>` biçimini kullanın. Veya, kısıtlanmış uygulamalar listesini içeren mevcut bir listeyi aynı biçimde **dışarı aktarın** .

> [!IMPORTANT]
> Kısıtlı uygulama ayarlarını kullanan cihaz profilleri kullanıcı gruplarına atanmalıdır.

## <a name="shared-ipad"></a>Paylaşılan iPad

Bu özellik şu platformlarda geçerlidir:

- ıpados 13,4 ve üzeri
- Paylaşılan iPad

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Paylaşılan iPad geçici oturumlarını engelle**: geçici oturumlar kullanıcıların Konuk olarak oturum açmasını sağlar ve kullanıcıların yönetilen BIR Apple kimliği veya parola girmesi gerekmez.

  **Evet**olarak ayarlandığında:

  - Paylaşılan iPad kullanıcıları geçici oturumları kullanamaz.
  - Kullanıcıların cihazda yönetilen Apple KIMLIĞI ve parolası ile oturum açması gerekir.
  - Konuk hesabı seçeneği cihazlarda kilit ekranında gösterilmez.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, paylaşılan bir iPad kullanıcısına Konuk hesabıyla cihazda oturum açmasını sağlar. Kullanıcı oturumu kapattığında, kullanıcının verilerinin hiçbiri iCloud 'a kaydedilmez veya eşitlenmez.

## <a name="show-or-hide-apps"></a>Uygulamaları gösterme veya gizleme

Bu özellik şu platformlarda geçerlidir:

- iOS 9,3 ve üzeri
- ıpados 13,0 ve üzeri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Uygulama türü listesi**: gösterilecek veya gizlenecek uygulamaların bir listesini oluşturun. Yerleşik uygulamaları ve iş kolu uygulamalarını gösterebilir veya gizleyebilirsiniz. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur. Seçenekleriniz şunlardır:

  - **Gizli uygulamalar**: kullanıcılardan gizlenen uygulamaların listesini girin. Kullanıcılar bu uygulamaları görüntüleyemez veya açamaz.
  
    Apple, bazı yerel uygulamaların gizlenmelerini önler. Örneğin, cihazdaki **Ayarlar** uygulamasını gizleyemezsiniz. [Yerleşik Apple uygulamalarını silme](https://support.apple.com/HT208094) , gizli olabilecek uygulamaları listeler.
  
  - **Görünür uygulamalar**: kullanıcıların görüntüleyebileceği ve başlatabileceği uygulamaların bir listesini girin. Başka hiçbir uygulama görüntülenemez veya başlatılamaz.

- **Uygulama URL 'si**: göstermek veya gizlemek istediğiniz uygulamanın Mağaza uygulama URL 'sini girin. Örneğin:

  - Microsoft çalışma klasörleri uygulamasını eklemek için `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` veya girin `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` . 

  - Microsoft Word uygulamasını eklemek için `https://itunes.apple.com/de/app/microsoft-word/id586447913` veya girin `https://apps.apple.com/de/app/microsoft-word/id586447913` .

  Uygulamanın URL'sini bulmak için, iTunes App Store'u açın ve uygulamayı arayın. Örneğin `Microsoft Remote Desktop` veya `Microsoft Word` için arama yapın. Uygulamayı seçin ve URL'sini kopyalayın.

  iTunes kullanarak da uygulamayı bulabilir ve ardından **Bağlantıyı Kopyala** görevini kullanıp uygulama URL’sini alabilirsiniz.

- **Uygulama PAKETI kimliği**: istediğiniz uygulamanın uygulama [paket kimliğini](bundle-ids-built-in-ios-apps.md) girin. Yerleşik uygulamaları ve iş kolu uygulamalarını gösterebilir veya gizleyebilirsiniz. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur.
- **Uygulama adı**: istediğiniz uygulamanın uygulama adını girin. Yerleşik uygulamaları ve iş kolu uygulamalarını gösterebilir veya gizleyebilirsiniz. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur.
- **Yayımcı**: istediğiniz uygulamanın yayımcısını girin.

Uygulamaları eklemek için şunları yapabilirsiniz:

- **Ekle**: uygulama listenizi oluşturmak için seçin.
- URL 'SI dahil olmak üzere uygulamayla ilgili ayrıntılarla bir CSV dosyasını **Içeri aktarın** . `<app url>, <app name>, <app publisher>` biçimini kullanın. Ya da, aynı biçimde eklediğiniz kısıtlı uygulamaların bir listesini oluşturmak için **dışa aktarın** .

## <a name="wireless"></a>Kablosuz

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Veri dolaşımı**: **blok** , hücresel ağ üzerinde veri dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz hücresel ağ üzerindeyken veri dolaşımına izin verebilir.

  > [!IMPORTANT]
  > Bu ayar uzak cihaz eylemi olarak değerlendirilir. Bu nedenle, bu ayar cihazlarda yönetim profilinde gösterilmez. Cihazda veri dolaşımı durumu her değiştiğinde **veri dolaşımı** , Intune hizmeti tarafından engellenir. Intune 'da, raporlama durumu bir başarı gösteriyorsa, bu ayar cihazdaki yönetim profilinde gösterilmese de, çalıştığını öğrenin.

- **Dolaşım sırasında genel arka plan getirme**: **blok** , hücresel ağ üzerinde dolaşımda genel arka plan getirme özelliğinin kullanılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazların bir hücresel ağda dolaşımda olduğu gibi, e-posta gibi verileri getirmeye izin verebilir.
- **Sesli arama**: **blok** , cihazlarda sesli arama özelliğinin kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda sesli aramaya izin verebilir.
- **Ses dolaşımı**: **blok** , hücresel ağ üzerinde ses dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, cihazlar hücresel ağ üzerindeyken ses dolaşımına izin verebilir.
- **Kişisel etkin nokta**: **blok** her cihaz eşitlemesine sahip cihazlarda kişisel etkin noktayı kapatır. Bu ayar bazı taşıyıcılar ile uyumlu olmayabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kişisel etkin nokta yapılandırmasını varsayılan olarak kullanıcılar tarafından ayarlanmış olarak tutabilir.

  > [!IMPORTANT]
  > Bu ayar uzak cihaz eylemi olarak değerlendirilir. Bu nedenle, bu ayar cihazlarda yönetim profilinde gösterilmez. Kişisel etkin nokta durumu cihazda her değiştiğinde **Kişisel etkin nokta** , Intune hizmeti tarafından engellenir. Intune 'da, raporlama durumu bir başarı gösteriyorsa, bu ayar cihazdaki yönetim profilinde gösterilmese de, çalıştığını öğrenin.

- **Hücresel kullanım kuralları (yalnızca yönetilen uygulamalar)**: **izin ver** , yönetilen uygulamaların hücresel ağlarda ne zaman kullanabileceği veri türlerini tanımlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Seçenekleriniz şunlardır:
  - **Hücresel veri kullanımını engelleyin**: **tüm yönetilen uygulamalar** için hücresel veri kullanmayı engelleyin veya **belirli uygulamaları seçin**.
  - **Dolaşım sırasında hücresel veri kullanımını engelle**: **tüm yönetilen uygulamalar** için Dolaşımda hücresel veri kullanmayı engelleyin veya **belirli uygulamaları seçin**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Uygulama hücresel veri kullanım ayarlarında yapılan değişiklikler**: **blok** , uygulama hücresel veri kullanımı ayarlarında değişiklik yapılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların hangi uygulamaların hücresel veri kullanmasına izin verileceğini denetlemesine izin verebilir.
- **Hücresel plan ayarlarındaki değişiklikler**: **blok** , hücresel plandaki ayarların değiştirilmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların değişiklik yapmasına izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **Kişisel etkin noktanın Kullanıcı değişikliği**: **blok** , kişisel etkin nokta ayarının değiştirilmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların kişisel etkin kullanımlarını etkinleştirmesine veya devre dışı bırakmasına izin verebilir.

  Bu ayarı engellerseniz ve **Kişisel etkin nokta** ayarını engellerseniz kişisel etkin nokta kapalıdır.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 12,2 ve üzeri
  - ıpados 13,0 ve üzeri

- **Yalnızca yapılandırma profillerini kullanarak Wi-Fi ağlarını birleştirin**: cihazların yalnızca Intune yapılandırma profilleri aracılığıyla ayarlanmış Wi-Fi ağlarını **kullanmasını zorunlu kılar** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazların diğer Wi-Fi ağlarını kullanmasına izin verebilir.

  **Gerektir**olarak ayarlandığında, cihazda bir Wi-Fi profili bulunduğundan emin olun. Bir Wi-Fi profili atamadıysanız, bu ayar cihazların internet 'e bağlanmasını engelleyebilir. Diğer bir deyişle, bu cihaz kısıtlama profili bir Wi-Fi profilinden önce atanırsa cihazın İnternet 'e bağlanması engellenebilir.
  
  Bağlanamıyorsa, cihazın kaydını kaldırın ve bir Wi-Fi profiliyle yeniden kaydedin. Ardından, bu ayarı cihaz kısıtlamaları profilinde **gerekli** olacak şekilde ayarlayın ve profili cihaza atayın.

- **Wi-Fi her zaman açık**: **gerekli** Ayarlar uygulamasında Wi-Fi ' ı devam ediyor. Cihaz uçak modundayken bile ayarlarda veya denetim merkezinde devre dışı bırakılamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Wi-Fi ' ı açıp kapatmasına izin verebilir.

  Bu ayarın yapılandırılması, kullanıcıların bir Wi-Fi ağı seçmesini engellemez.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="connected-devices"></a>Bağlı Cihazlar

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Eşleştirilmiş Apple Watch Için bilek algılama**: **gerektir** , eşleştirilmiş bir Apple Watch 'un bilek algılamayı kullanmasına zorlar. Gerekli seçilirse, Apple Watch takılmadığında bildirim görüntülemez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **AirPlay giden istek eşleştirme parolasını gerektir**: diğer Apple cihazlarına içerik akışı sağlamak Için AirPlay kullanırken eşleştirme parolası **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parola girmeden AirPlay 'i kullanarak içerik akışına izin verebilir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **AirDrop**: **Block** cihazlarda AirDrop kullanımına engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, Yakındaki cihazlarla içerik değişimi için AirDrop özelliğinin kullanılmasına izin verebilir.
- **Apple Watch eşleştirme**: **blok** bir Apple Watch eşlemeyi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazların bir Apple Watch eşleştirmeye izin verebilir.
- **Bluetooth değişikliği**: **blok** kullanıcıların cihazlarda Bluetooth ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarları değiştirmesine izin verebilir.
- **İOS/ıpados cihazının eşleşebileceği cihazları denetlemek Için konak eşleştirme**: **Block** , konak eşleşmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, yöneticinin bir iOS/ıpados cihazının hangi cihazlara eşlenebileceğini denetlemesine olanak tanımak için konak eşleştirmeye izin verebilir.
- **AirPrint 'ı engelle**: **blok** cihazlarda AirPrint özelliğinin kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların AirPrint kullanmasına izin verebilir.
  - **Anahtarlıkta AirPrint kimlik bilgilerinin depolanmasını engelle**: **blok** , cihazlarda Kullanıcı adı ve parola için Anahtarlık depolamanın kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, anahtar zinciri uygulamasında AirPrint Kullanıcı adını ve parolasını depolamaya izin verebilir.
  - **AirPrint için güvenilir BIR TLS sertifikası gerektir**: cihazların TLS yazdırma iletişimi için güvenilen sertifikaları **kullanmalarını zorunlu kılar** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **AirPrint yazıcıları bloğunu engelle**: **blok** , ağ trafiği için kimlik avından kötü amaçlı AirPrint Bluetooth işaretlerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda AirPrint yazıcılarına izin verebilir.
- **Yeni yakındaki cihazları ayarlamayı engelle**: **blok** yakında yeni cihazları ayarlamaya yönelik istemi devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kullanıcıların diğer yakındaki Apple cihazlarına bağlanmasına yönelik istemlere izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **USB sürücüsündeki dosyalara erişim**: cihazlar, dosyaları bir USB sürücüsünde bağlayıp açabilir. **Devre dışı bırak ayarı** , cihaza USB bağlandığında dosyalar uygulamasında USB sürücüsüne cihaz erişimini engeller. Bu özelliğin devre dışı bırakılması, kullanıcıların dosyaları bir iPad 'e bağlı USB sürücüsüne aktarmasına de engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi dosyalar uygulamasında USB sürücüsüne erişime izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="keyboard-and-dictionary"></a>Klavye ve Sözlük

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Sözcük tanımı arama**: **blok** bir sözcüğün vurgulanmasını ve tanımını aramasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi tanım arama özelliğine erişime izin verebilir.
- Tahmine **dayalı klavyeler**: **blok** , kullanıcıların istedikleri sözcükleri önermek için tahmine dayalı klavyeler kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Otomatik Düzeltme**: **blok** otomatik düzeltme kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazların yanlış yazılan sözcükleri otomatik olarak düzeltmesini sağlayabilir.
- **Klavye yazım denetimi**: **blok** yazım denetimcisini engelliyor. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi SpellChecker kullanılmasına izin verebilir.
- **Klavye kısayolları**: **blok** kullanıcıların klavye kısayollarını kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda klavye kısayollarının kullanılmasına izin verebilir.
- **Dikte**: **blok** , kullanıcıların metin girmek için ses girişi kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların dikte girişi kullanmasına izin verebilir.
- **QuickPath**: **Block** , kullanıcıların hızlı yol kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların, cihazın klavyesinde sürekli bir giriş sağlayan hızlı yol kullanmasına izin verebilir. Kullanıcılar, sözcükler oluşturmak için anahtarlar arasında çekerek yazı yazabilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="cloud-and-storage"></a>Bulut ve Depolama

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Şifrelenmiş yedekleme**: **gerekli** olduğundan cihaz yedeklemelerinin şifrelenmesi gerekir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Yönetilen uygulamalar buluta eşitlenir**: **blok** , Intune tarafından yönetilen uygulamaların kullanıcının iCloud hesabıyla veri eşitlemesine engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu verilerin iCloud 'a eşitlenmesine izin verebilir.
- **Kurumsal kitap yedeklemesini engelle**: **blok** , kurumsal kitapların yedeklenmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu kitapları yedeklemelerine izin verebilir.
- **Kurumsal kitap meta verileri eşitlemesini engelleyin (notlar ve vurgular)**: **blok** , kurumsal kitaplar 'da notların ve vurguların eşitlenmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi eşitlemeye izin verebilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **İCloud 'A fotoğraf akışı eşitlemesi**: **blok** , iCloud 'a fotoğraf akışı eşitlemesini önler. Bu özelliğin engellenmesi veri kaybına neden olabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların cihazlarındaki **fotoğraf akışımı** iCloud 'a eşitlemesine ve tüm kullanıcıların cihazlarında fotoğraflar kullanmasına olanak sağlayabilir.
- **ICloud Fotoğraf Kitaplığı**: **blok** fotoğraflar ve videoları bulutta depolamak için iCloud Fotoğraf Kitaplığı kullanmayı devre dışı bırakır. İCloud Fotoğraf Kitaplığı 'ndan cihazlara tam olarak indirilmeyen tüm fotoğraflar cihazdan kaldırılır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud Fotoğraf Kitaplığı kullanımına izin verebilir.
- **Paylaşılan fotoğraf akışı**: **blok** , cihazlarda **iCloud Fotoğraf paylaşımını** devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi paylaşılan fotoğraf akışına izin verebilir.
- **İletim**: **Block** , kullanıcıların bir iOS/ıpados cihazında iş başlatmasını ve sonra başka bir iOS/ıpados veya MacOS cihazında çalışmaya devam etmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu iletime izin verebilir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **İCloud 'A yedekleme**: **blok** , kullanıcıların cihazları iCloud 'a yedeklemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazları iCloud 'a yedeklemesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **ICloud belge eşitlemesini engelle**: **blok** , iCloud 'ın belge ve verileri eşitlemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud depolama alanınızda belge ve anahtar-değer eşitlemeye izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **ICloud anahtar zinciri eşitlemesini engelle**: **blok** , anahtarlıkta depolanan kimlik bilgilerinin iCloud 'a eşitlenmesini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu kimlik bilgilerini eşitlemesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

## <a name="autonomous-single-app-mode-asam"></a>Otonom tek uygulama modu (ASAM)

İOS/ıpados cihazlarını, otonom tek uygulama modunda (ASAM) belirli uygulamaları çalıştıracak şekilde yapılandırmak için bu ayarları kullanın. Bu mod yapılandırıldığında ve kullanıcılar yapılandırılmış uygulamalardan birini başlatdıklarında, cihaz bu uygulamaya kilitlenir. Uygulama/görev değiştirme, kullanıcılar izin verilen uygulamadan çıkana kadar devre dışı bırakıldı.

- Örneğin, okul veya üniversite ortamında, kullanıcıların cihazda bir test geçirmesine imkan tanıyan bir uygulama ekleyin. Ya da, Kullanıcı kimlik doğrulamasından çıkana kadar cihazı Şirket Portalı uygulamasına kilitleyin. Uygulamalar eylemleri kullanıcılar tarafından tamamlandığında veya bu ilkeyi kaldırdığınızda cihaz normal durumuna geri döner.

- Tüm uygulamalar otonom tek uygulama modunu desteklemez. Bir uygulamayı otonom tek uygulama modunda yerleştirmek için, bir paket KIMLIĞI veya bir uygulama yapılandırma ilkesi tarafından teslim edilen anahtar değer çifti genellikle gereklidir. Daha fazla bilgi için Apple MDM belgelerindeki [ `autonomousSingleAppModePermittedAppIDs` kısıtlamaya](https://developer.apple.com/documentation/devicemanagement/restrictions) bakın. Yapılandırmakta olduğunuz uygulama için gereken belirli ayarlar hakkında daha fazla bilgi için satıcı belgelerine bakın.

  Örneğin, ölçek odalarını otonom tek uygulama modunda yapılandırmak için, yakınlaştırma paket KIMLIĞINI kullanmak üzere diyor `us.zoom.zpcontroller` . Bu örnekte, yakınlaştırma web portalında da bir değişiklik yaparsınız. Daha fazla bilgi için bkz. [zoom yardım merkezi](https://support.zoom.us/hc/articles/360021322632-Autonomous-Single-App-Mode-for-Zoom-Rooms-with-a-Third-Party-MDM).

- İOS/ıpados cihazlarında Şirket Portalı uygulaması ASAM 'yi destekler. Şirket Portalı uygulaması ASAM 'da olduğunda, Kullanıcı kimlik doğrulamasından çıkana kadar cihaz Şirket Portalı uygulamada kilitlenir. Kullanıcılar Şirket Portalı uygulamasında oturum açtıklarında, cihazdaki diğer uygulamaları ve giriş ekranı düğmesini kullanabilirler. Şirket Portalı uygulamasında oturum açtıklarında, cihaz tek uygulama moduna geri döner ve Şirket Portalı uygulamasındaki kilitler.

  Şirket Portalı uygulamayı bir ' oturum aç/oturumu Kapat ' uygulamasına açmak için (ASAM 'yı etkinleştirin), `Microsoft Intune Company Portal` Bu ayarlarda, ve paket kimliği () gibi şirket portalı uygulama adını girin `com.microsoft.CompanyPortal` . Bu profil atandıktan sonra, kullanıcıların oturum açmasını ve oturumunuzu açmasını sağlamak üzere uygulamayı kilitlemek için Şirket Portalı uygulamasını açmanız gerekir.
  
  Cihaz yapılandırma profili kaldırıldığında ve Kullanıcı oturumu kapattığında, cihaz Şirket Portalı uygulamasında kilitlenmez.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Uygulama adı**: istediğiniz uygulamanın adını girin.
- **Uygulama PAKETI kimliği**: istediğiniz UYGULAMANıN [paket kimliğini](bundle-ids-built-in-ios-apps.md) girin.
- **Ekle**: uygulama listenizi oluşturmak için seçin.

Ayrıca, uygulama adlarının ve paket kimliklerinin listesini içeren bir CSV dosyasını **Içeri aktarabilirsiniz** . Alternatif olarak uygulamaları içeren mevcut listeyi **dışarı aktarabilirsiniz**.

## <a name="kiosk"></a>Bilgi noktası

[Tek uygulama modu](https://support.apple.com/guide/mdm/mdm80a981/web) , Intune 'Da bilgi noktası modu olarak adlandırılır.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Bilgi noktası modunda çalıştırılacak uygulama**: bilgi noktası modunda çalıştırmak istediğiniz uygulama türlerini seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bilgi noktası ayarlarını uygulamayamayabilir. Cihaz bilgi noktası modunda çalışmıyor.
  - **Mağaza uygulaması**: iTunes App Store 'da bir uygulamanın URL 'sini girin.
  - **Yönetilen uygulama**: daha önce Intune 'a eklemiş olduğunuz bir uygulamayı seçin.
  - **Yerleşik uygulama**: yerleşik UYGULAMANıN [paket kimliğini](bundle-ids-built-in-ios-apps.md) girin.

- **Yardımcı dokunma**: cihazlarda yardımcı dokunma erişilebilirlik ayarının olması **gerekir** . Bu özellik kullanıcılara zorlanabilecekleri ekran hareketlerinde yardımcı olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Renkleri ters çevir**: görsel sorunları olan kullanıcıların ekran ekranını değiştirebilmeleri Için renkleri ters çevir erişilebilirlik ayarını **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Mono ses**: cihazlarda mono ses erişilebilirlik ayarının olması **gerekir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Voice Control**: **gerektir** , cihazlarda ses denetimi yapmanızı sağlar ve kullanıcıların Siri komutlarını kullanarak işletim sistemini tam olarak denetlemesine olanak tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi ses denetimini devre dışı bırakabilir.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri
  
  > [!TIP]
  > Kuruluşunuz için kullanılabilir LOB uygulamalarınız varsa ve iOS 13,0 yayımları olduğunda gün 0 ' da hazır bir **ses denetimi** yoksa, bu ayarı **yapılandırılmamış**olarak bırakmanız önerilir.

- **VoiceOver**: ekrandaki metni okumak için VoiceOver erişilebilirlik ayarının yüksek sesle **kullanılmasını gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Yakınlaştır**: kullanıcıların ekranda yakınlaştırmak için yakınlaştırabilmesi için yakınlaştırma ayarını **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Otomatik kilit**: **engelleme** cihazların otomatik olarak kilitlenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Zil düğmesi**: **blok** cihazlarda zil devre dışı bırakır (sessiz). **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Ekran döndürme**: **engelleme** , kullanıcılar Cihazı döndürürken ekran yönünün değiştirilmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Ekran uyku düğmesi**: **blok** cihazlarda ekran uyku modundan çıkarma düğmesini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Touch**: **Block** cihazlarda dokunmatik ekranı devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların dokunmatik ekranı kullanmasına izin verebilir.
- **Ses düğmeleri**: **blok** , cihazlarda ses düğmelerinin kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi ses düğmelerine izin verebilir.
- **Yardımcı dokunma denetimi**: **izin ver** , kullanıcıların yardımcı Touch işlevini kullanmasına izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.
- **Renkleri ters çevir denetimi**: kullanıcıların renkleri ters çevirme işlevini ayarlamasına olanak tanımak için evirmelerin renk değişikliklerine **izin verin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.
- **Seçili metinde konuş**: konuş seçimi erişilebilirlik ayarlarının cihazlarda **bulunmasına izin ver** . Bu özellik, kullanıcıların seçolduğu sesli metni okur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.
- **Ses denetimi değişikliği**: kullanıcıların cihazlarındaki ses denetimi durumunu değiştirmesine **izin verin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarındaki ses denetimi durumunu değiştirmelerini engelleyebilir.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **VoiceOver Control**: kullanıcıların, ekran metinlerin hızlı bir şekilde okunması gibi VoiceOver işlevini güncelleştirmesine olanak tanımak için VoiceOver değişikliklere **izin verin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi VoiceOver değişikliğini engelleyebilir.
- **Yakınlaştırma denetimi**: kullanıcılara göre değişikliklere **izin ver** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi yakınlaştırılmış değişiklikleri engelleyebilir.

> [!NOTE]
> İOS/ıpados cihazını bilgi noktası modu için yapılandırmadan önce, cihazları denetimli moda yerleştirmek için Apple Configurator aracını veya Apple Aygıt Kayıt Programı kullanmanız gerekir. Apple Configurator aracını kullanma konusunda Apple'ın kılavuzuna bakın.
> Girdiğiniz iOS/ıpados uygulaması profili atadıktan sonra yüklendiyse, cihaz yeniden başlatılana kadar cihaz bilgi noktası moduna girmez.

## <a name="domains"></a>Etki Alanları

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **İşaretlenmemiş e-posta etki alanları**  >  **E-posta etki alanı URL 'si**: listeye bir veya daha fazla URL ekleyin. Kullanıcılar girdiğiniz etki alanlarından başka bir etki alanından e-posta aldığınızda, bu e-posta iOS/ıpados Mail uygulamasında güvenilmeyen olarak işaretlenir.

- **Yönetilen Web etki alanları**  >  **Web etki alanı URL 'si**; Listeye bir veya daha fazla URL ekleyin. Belgeler girdiğiniz etki alanlarından indirildiğinde yönetilen belgeler olarak değerlendirilir. Bu ayar yalnızca Safari tarayıcısı kullanılarak indirilen belgeler için geçerlidir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Safari parola otomatik doldurma etki alanları**  >  **Etki alanı URL 'si**: listeye bir veya daha fazla URL ekleyin. Kullanıcılar yalnızca bu listedeki URL’lerdeki parolaları kaydedebilir. Bu ayar yalnızca Safari tarayıcısı ve denetimli moddaki cihazlar için geçerlidir. Herhangi bir URL girmezseniz, parolalar tüm Web sitelerinden kaydedilebilir.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 9,3 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="settings-that-require-supervised-mode"></a>Denetimli mod gerektiren ayarlar

iOS/ıpados Denetimli mod yalnızca Apple Aygıt Kayıt Programı aracılığıyla veya Apple Configurator kullanılarak ilk cihaz kurulumu sırasında etkinleştirilebilir. Denetimli mod etkinleştirildikten sonra, Intune şu işlevleri kullanarak bir cihazı yapılandırabilir:

- Bilgi noktası modu (tek uygulama modu): [Apple geliştirici belgelerinde](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf)"uygulama kilidi" olarak adlandırılır.
- Etkinleştirme Kilidini Devre Dışı Bırakma 
- Otonom Tek Uygulama Modu 
- Web İçeriği Filtresi 
- Arka plan ve kilit ekranı ayarlama 
- Uygulamaları Sessiz Gönderme 
- Her Zaman Açık VPN 
- Yönetilen uygulama yüklemesine özel olarak izin verme 
- iBookstore 
- iMessages 
- Oyun Merkezi 
- AirDrop 
- AirPlay 
- Konak eşleştirme 
- Bulut Eşitleme 
- Spotlight arama 
- İletim 
- Cihaz silme 
- Kısıtlamalar kullanıcı arabirimi 
- Kullanıcı arabirimine göre yapılandırma profili yüklemesi 
- Haberler 
- Klavye kısayolları 
- Geçiş kodu değişiklikleri 
- Cihaz adı değişiklikleri 
- Otomatik uygulama indirme 
- Apple Music 
- Posta bırakma 
- Apple Watch ile eşleştirme 

> [!NOTE]
> Apple, 2019’da bazı ayarların yalnızca denetimli hale geleceğini doğruladı. Apple’ın bu ayarları yalnızca denetimli moda aktarmasını beklemek yerine ayarları kullanırken bu durumu göz önünde bulundurmanızı öneririz:
>
> - Son kullanıcılar tarafından uygulama yükleme
> - Uygulama kaldırma
> - FaceTime
> - Safari
> - iTunes
> - Müstehcen içerik
> - iCloud belgeleri ve verileri
> - Çok oyunculu oyun
> - Oyun Merkezi arkadaşları ekleme
> - Siri

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[macOS](device-restrictions-macos.md) cihazlarındaki özellikleri ve ayarları da kısıtlayabilirsiniz.
