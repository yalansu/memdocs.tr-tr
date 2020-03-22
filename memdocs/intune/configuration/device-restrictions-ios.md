---
title: Microsoft Intune-Azure 'da iOS/ıpados cihaz ayarları | Microsoft Docs
titleSuffix: ''
description: İOS/ıpados cihazlarında ayarlar ekleme, yapılandırma veya oluşturma; parola gereksinimlerini ayarlama, kilitli ekranı denetleme, yerleşik uygulamalar kullanma, kısıtlı veya onaylanan uygulamalar ekleme, Bluetooth cihazlarını işleme, yedekleme ve depolama için buluta bağlanma, bilgi noktası modunu etkinleştirme, etki alanı ekleme ve kullanıcıların Microsoft Intune ' de Safari web tarayıcısıyla nasıl etkileşime gireceğini denetleme.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea0968d15572fa9c3bde1e4d133dcb8b4c980274
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80087038"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune kullanarak özelliklere izin vermek veya erişimi kısıtlamak için iOS ve ıpados cihaz ayarları

Bu makalede iOS ve ıpados cihazlarında denetleyebileceğinizi belirten farklı ayarlar listelenir. Mobil cihaz yönetimi (MDM) yönteminizin bir parçası olarak bu ayarları kullanabilir ve bu sayede özellikleri etkinleştirip devre dışı bırakabilir, parola kuralları uygulayabilir, belirli uygulamalara izin verebilir veya bunları kısıtlayabilir ve çok daha fazlasını yapabilirsiniz.

Bu ayarlar, Intune 'da bir cihaz yapılandırma profiline eklenir ve sonra iOS/ıpados cihazlarınıza atanır veya dağıtılır.

> [!TIP]
> Bu ayarlar Apple MDM ayarlarını kullanır. Bu ayarlar hakkında daha fazla bilgi için bkz. [Apple 'ın mobil cihaz yönetimi ayarları](https://support.apple.com/guide/mdm/welcome/web) (Apple 'ın Web sitesini açar).

## <a name="before-you-begin"></a>Başlamadan önce

[Cihaz kısıtlamaları yapılandırma profili oluşturma](device-restrictions-configure.md).

> [!NOTE]
> Bu ayarlar, bazı ayarların tüm kayıt seçeneklerine uygulanmasıyla farklı kayıt türleri için geçerlidir. Farklı kayıt türleri hakkında daha fazla bilgi için bkz. [iOS/ıpados kaydı](../enrollment/ios-enroll.md).

## <a name="general"></a>Genel

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Kullanım verilerini paylaşma**: **blok** , cihazın Apple 'a tanılama ve kullanım verileri göndermesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu verilerin gönderilmesine izin verebilir.

- **Ekran yakalama**: **engelleme** , cihazdaki ekran görüntülerini veya ekran yakalamalarını engeller. İOS/ıpados 9,0 ve üzeri sürümlerde, ekran kayıtlarını da engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların ekran içeriğini bir görüntü veya video olarak yakalamasına izin verebilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **GÜVENILMEYEN TLS sertifikaları**: **engelleme** , cihazda güvenilmeyen Aktarım Katmanı Güvenliği (TLS) sertifikalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi TLS sertifikalarına izin verebilir.
- **Kablosuz PKI güncelleştirmelerini engelle**: **blok** , cihazın bir bilgisayara bağlı olmadığı durumlar dışında yazılım güncelleştirmelerini almasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bir bilgisayara bağlı kalmadan bir cihazın yazılım güncelleştirmelerini almasına izin verebilir.
- **Ad Izlemeyi sınırla**: cihaz reklam tanımlayıcısını devre dışı bırakmak için **sınır** ' ı seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi etkin durumda kalabilir.
- **Kurumsal Uygulama güveni**: **blok** , cihaz üzerindeki cihaz yönetimi & Genel > profilleri > ayarlar ' da **Kurumsal Geliştirici güven** düğmesini kaldırır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların uygulama mağazasından indirilmemiş uygulamalara güvenmeyi seçebilmesine izin verebilir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Tanılama gönderme ayarları değişikliği**: **blok** kullanıcıların tanılama **ve kullanım** (cihaz ayarları) içindeki tanılama gönderme ve uygulama analizi ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu cihaz ayarlarını değiştirmesine izin verebilir.

  Bu ayarı kullanmak için, **kullanım verilerini paylaşma** ayarını **Engelle**olarak ayarlayın.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 9.3.2 ve üzeri
  - ıpados 13,0 ve üzeri

- **Sınıf uygulamasına göre uzak ekran**izleme: **blok** , sınıf uygulamasının cihazda ekranı uzaktan görüntülemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Apple derslik uygulamasının ekranı görüntülemesine izin verebilir.

  Bu ayarı kullanmak için **ekran yakalama** ayarını **Engelle**olarak ayarlayın.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 9,3 ve üzeri
  - ıpados 13,0 ve üzeri

- **Sınıf uygulamasına göre istem dışı ekran izleme**: **izin ver**olarak ayarlanırsa, öğretmenler, öğrenciler hakkında bilgi sahibi olmadan ders uygulamasını kullanan iOS/ıpados cihazlarının ekranını sessizce gözlemleyebilirsiniz. Sınıf uygulamasını kullanan bir sınıfa kayıtlı öğrenci cihazları otomatik olarak bu kurs öğretme için izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği önleyebilir.

  Bu ayarı kullanmak için **ekran yakalama** ayarını **Engelle**olarak ayarlayın.

- **Hesap değişikliği**: **engelleme**olarak ayarlandığında, kullanıcılar cihaza özgü ayarları iOS/ıpados ayarları uygulamasından güncelleştiremez. Örneğin, kullanıcılar yeni cihaz hesapları oluşturamaz veya Kullanıcı adını veya parolayı değiştirebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarları değiştirmesine izin verebilir.

  Bu özellik ayrıca, e-posta, kişiler, takvim, Twitter ve daha fazlası gibi iOS/ıpados ayarları uygulamasından erişilebilen ayarlar için de geçerlidir. Bu özellik, Microsoft Outlook uygulaması gibi iOS/ıpados ayarları uygulamasından yapılandırılamayan hesap ayarlarına sahip uygulamalar için geçerlidir.

- **Ekran süresi**: **blok** kullanıcıların ekran zamanında (cihaz ayarları) kendi kısıtlamalarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların cihazda cihaz kısıtlamalarını (ebeveyn denetimleri veya içerik ve gizlilik kısıtlamaları gibi) yapılandırmasına izin verebilir.

  Bu ayar **Cihaz ayarlarında kısıtlamaları etkinleştirme** ayarının yeniden adlandırılmış halidir. Bu değişikliğin etkisi:  
  
  - iOS 11.4.1 ve üzeri: **Block** , kullanıcıların cihaz ayarlarında kendi kısıtlamalarını değiştirmesini engeller. Davranış aynıdır; ve kullanıcılar için herhangi bir değişiklik yoktur.
  - iOS 12,0 ve üzeri: **Block** , kullanıcıların, içerik ve gizlilik kısıtlamaları dahil cihaz ayarları 'Nda (Ayarlar > Genel > ekran süresi) kendi **ekran süresini** ayarlamalarına engel olur. iOS 12.0'dan yükseltilen cihazlar artık cihaz ayarlarında kısıtlamalar sekmesini (Ayarlar > Genel > Cihaz Yönetimi > Yönetim Profili > Kısıtlamalar) görmez. Bu ayarlar **Ekran Saati** altındadır.
  
- **Cihazdaki tüm içeriği ve ayarları Sil seçeneğinin kullanımı**: **Engelle** ' yi seçin, böylece kullanıcılar cihazdaki tüm içeriği ve ayarları silme seçeneğini kullanamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcılara bu ayarlara erişim verebilir.
- **Cihaz adı değişikliği**: cihaz adının değiştirilebilmesi için **Engelle** ' yi seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazın adını değiştirmesine izin verebilir.
- **Bildirim ayarlarının değiştirilmesi**: bildirim ayarlarının değiştirilenemez şekilde **blok** seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihaz bildirim ayarlarını değiştirmesine izin verebilir.
- **Duvar kağıdı değişikliği**: **blok** duvar kağıdının değiştirilmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazdaki duvar kağıdını değiştirmesine izin verebilir.
- **Yapılandırma profili değişiklikleri**: **blok** , cihazdaki yapılandırma profili değişikliklerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların yapılandırma profillerini yüklemelerine izin verebilir.
- **Etkinleştirme Kilidi**: denetimli IOS/ıpados cihazlarında Etkinleştirme Kilidi etkinleştirmek Için **izin ver** ' i seçin. Etkinleştirme Kilidi, kaybolan veya çalınan bir cihazın yeniden etkinleştirilmesini zorlaştırır.
- **Uygulama kaldırmayı engelle**: **blok** kullanıcıların uygulamaları kaldırmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazdan uygulama kaldırmasına izin verebilir.
- **Cihaz KILITLIYKEN USB donatılara Izin ver**: **ızın ver** , USB aksesuarları 'nin bir saatten daha fazla kilitlenmiş bir cihazla veri alışverişi yapmasına olanak sağlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda USB kısıtlı modunu güncelleştirmeyebilir ve USB aksesuarları bir saatten fazla kilitliyse verileri cihazdan aktarmaya engellenir.
- **Otomatik tarih ve saati zorla**: **gerekli** cihazların otomatik olarak tarih & zamanını ayarlamaya zorlar. Cihazın hücresel bağlantıları olduğunda veya konum hizmetleriyle arasında Wi-Fi etkinleştirildiğinde saat dilimi güncelleştirilir.
- **Öğrencilerden** **ayrılmaları için** öğrencilerin ders uygulamasını kullanarak yönetilmeyen bir kursa kaydolmaya izin istemesini gerektir: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğrenciye izin istemek üzere zoristememeyebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,3 ve üzeri
  - ıpados 13,0 ve üzeri

- **Sınıfa sormadan bir uygulamayı kilitlemesine ve cihazı kilitlemesine Izin ver**: **Enable** , öğretmenin uygulamaları kilitlemesine veya öğrenciye sormadan ders uygulamasını kullanarak cihazı kilitlemesine olanak tanır. Uygulamaların kilitlenmesi cihazın yalnızca öğretmenin belirttiği uygulamalara erişebileceği anlamına gelir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, öğretmenlerin öğrenciye sormadan sınıf uygulamasını kullanarak uygulamaları veya cihazları kilitlemesini engelleyebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **Sınıf sınıflarını sorulmadan otomatik olarak birleştir**: **Etkinleştir** otomatik olarak, öğrencilerin öğretme istenmeden ders uygulamasındaki bir sınıfa katılmasına izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğrencilerin ders uygulamasındaki bir sınıfa katılması istediğini öğretme isteyebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **VPN oluşturmayı engelle**: **blok** , kullanıcıların VPN yapılandırma ayarları oluşturmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazda VPN oluşturmalarına izin verebilir.
- **Esım ayarlarını değiştirme**: **Block** , kullanıcıların cihazdaki esım 'e bir hücresel plan kaldırmasını veya bu planı eklemesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarları değiştirmesine izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 12,1 ve üzeri
  - ıpados 13,0 ve üzeri

- **Yazılım güncelleştirmelerini ertele**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, Apple tarafından yayımlandığında Cihazdaki yazılım güncelleştirmelerini gösterebilir. Örneğin, bir iOS/ıpados güncelleştirmesi Apple tarafından belirli bir tarihte yayınlanmışsa, bu güncelleştirme doğal olarak cihazda yayın tarihinin etrafında görüntülenir.

  **Etkinleştir** ayarını kullanarak güncelleştirmelerin cihazlarda gösterilmesini 0-90 gün boyunca geciktirebilirsiniz. Bu ayar, güncelleştirmelerin yüklenme tarihini veya durumunu denetlemez. 

  - **Yazılım güncelleştirmeleri gecikmesi**: 0-90 günden bir değer girin. Gecikme süresi sona erdiğinde kullanıcılara gecikmenin tetiklendiği tarihte kullanılabilir durumda olan en eski işletim sistemi sürümüne güncelleştirme bildirimi gönderilir.

    Örneğin, iOS 12. a, **1 Ocak**'ta kullanılabilir ve **gecikme görünürlüğü** **5 güne**ayarlanmışsa, iOS 12. Kullanıcı cihazlarında kullanılabilir bir güncelleştirme olarak gösterilmez. Sürümden sonraki **altıncı gün** üzerinde, bu güncelleştirme kullanılabilir ve kullanıcılar uygulamayı yükleyebilir.

    Bu ayarın geçerli olduğu sürümler:  
    - iOS 11,3 ve üzeri
    - ıpados 13,0 ve üzeri

## <a name="password"></a>Parola

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Parola**: kullanıcıların cihaza erişmek için bir parola girmesini **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parola girmeden cihaza erişmesine izin verebilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

> [!IMPORTANT]
> Kullanıcı tarafından kaydedilen cihazlarda, herhangi bir parola ayarını yapılandırırsanız, **basit parolalar** ayarları otomatik olarak **engelleme**olarak ayarlanır ve 6 basamaklı bir PIN zorlanır.
>
> Örneğin, **parola süre sonu** ayarını yapılandırır ve bu ilkeyi Kullanıcı tarafından kaydedilen cihazlara gönderirsiniz. Cihazlarda aşağıdakiler olur:
>
> - **Parola süre sonu** ayarı yok sayılır.
> - `1111` veya `1234`gibi basit parolalara izin verilmez.
> - 6 basamaklı bir PIN zorlanır.

- **Basit parolalar**: **blok** daha karmaşık parolalar gerektirir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi `0000` ve `1234`gibi basit parolalara izin verebilir.

- **Gerekli parola türü**: kuruluşunuzun gerektirdiği parola türünü seçin. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı**
  - **Sayısal**
  - **Alfasayısal**
- **Paroladaki alfasayısal olmayan karakter sayısı**: `#` veya `@`gibi, parolada bulunması gereken simge karakterlerinin sayısını girin.

- **Minimum parola uzunluğu**: bir kullanıcının girmesi gereken minimum uzunluğu 4 ile 14 karakter arasında girin. Kullanıcı kayıtlı cihazlarda 4 ila 6 karakter uzunluğunda bir uzunluk girin.
  
  > [!NOTE]
  > Kullanıcı kayıtlı cihazlarda, kullanıcılar 6 basamaktan daha büyük bir PIN ayarlayabilir. Ancak cihazda 6 ' dan fazla basamak uygulanmaz. Örneğin, bir yönetici minimum uzunluğu `8`olarak ayarlar. Kullanıcı tarafından kaydedilen cihazlarda, kullanıcılardan yalnızca 6 basamaklı bir PIN ayarlaması gerekir. Intune, Kullanıcı tarafından kaydedilen cihazlarda 6 basamaktan daha büyük bir PIN 'ı zorlamaz.

- **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: cihaz temizlenmeden önce izin verilecek başarısız oturum açma işlemlerinin sayısını girin (4-11 arasında).
  
  iOS/ıpados, bu ayarı etkileyebilecek yerleşik güvenliğe sahiptir. Örneğin, iOS/ıpados, oturum açma hatalarının sayısına bağlı olarak ilkeyi tetikleyebilir. Aynı zamanda aynı geçiş kodunu bir girişimlerle tekrar girmeyi de düşünebilirsiniz. Apple 'ın [iOS/ıpados Güvenlik Kılavuzu](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) (Apple 'ın Web sitesini açar) iyi bir kaynaktır ve Passcodes hakkında daha ayrıntılı bilgiler sağlar.
  
- **Parola istenmeden önce ekran kilitlenmesinden sonraki en fazla dakika**<sup>1</sup>: kullanıcıların parolasını yeniden girmesi gerekmeden önce cihazın ne kadar süreyle boşta kalacağını girin. Girdiğiniz süre cihazda şu anda ayarlanmış olan süreden uzunsa, cihaz girdiğiniz süreyi yoksayar. İOS 8.0 + çalıştıran cihazlarda desteklenir ve ıpados 13.0 +.

- **Ekran kilitlenmeden önce geçmesi gereken en fazla dakika**sayısı<sup>1</sup>: ekran kilitlenmeden önce cihazda izin verilen en fazla dakika cinsinden süre sayısını girin.

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

  Bir değer iOS ve ıpados için uygulanmazsa, Apple en yakın *En düşük* değeri kullanır. Örneğin, `4` dakika girerseniz, ıpados cihazları `2` dakika kullanır. `10` dakika girerseniz, iOS cihazları `5` dakika kullanır. Bu bir Apple kısıtlamasıdır.
  
  > [!NOTE]
  > Bu ayar için Intune kullanıcı arabirimi iOS ve ıpados tarafından desteklenen değerleri birbirinden ayırır. Kullanıcı arabirimi gelecek bir sürümde güncelleştirilmiş olabilir.

- **Parola kullanım süresi (gün)** : cihaz parolasının değiştirilmesi gereken gün sayısını girin.
- **Önceki parolaların yeniden kullanılmasını engelle**: eski bir parolanın yeniden kullanılabilmesi için kullanılması gereken yeni parola sayısını girin.
- **Dokunma kimliği ve yüz kimliği kilit açma**: **blok** , cihazın kilidini açmak için parmak izi veya yüz kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların bu yöntemleri kullanarak cihazın kilidini açmalarına izin verebilir.

  Bu ayarı engellemek, cihazın kilidini açmak için çok yönlü kimlik doğrulamasının kullanılmasını da engeller.

  Yüz KIMLIĞI şu şekilde geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Geçiş kodu değişikliği**: **blok** geçiş kodunun değiştirilmesini, eklenmesini veya kaldırılmasını engeller. Bu özellik engellendikten sonra denetimli cihazlarda geçiş kodu kısıtlamalarında yapılan değişiklikler yoksayılır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, geçiş kodlarını 'in eklenmesine, değiştirilmesine veya kaldırılmasına izin verebilir.

  - **Dokunma kimliği ve yüz kimliği değişikliği**: **blok** kullanıcıların TouchID parmak izleri ve yüz kimliğini değiştirmesini, eklemesini veya kaldırmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların cihazdaki TouchID parmak izlerini ve yüz KIMLIĞINI güncelleştirmesine izin verebilir.

    Bu ayarı engellemek, kullanıcıların çok yönlü kimlik doğrulamasını değiştirmelerini, eklemesini veya kaldırmasını de engeller.

    Yüz KIMLIĞI şu şekilde geçerlidir:  
    - iOS 11,0 ve üzeri
    - ıpados 13,0 ve üzeri

- **Parola Otomatik doldurmayı engelle**: **Block** , iOS/ıpados üzerinde parolaları otomatik doldur özelliğinin kullanılmasını önler. **Engelle** ayarını seçmek şu sonuçlara da neden olur:

  - Safari'de veya diğer uygulamalarda kullanıcılara parolaları kaydetmek isteyip istemedikleri sorulmaz.
  - Otomatik Güçlü Parolalar devre dışı bırakılır ve kullanıcılara güçlü parola önerisi sunulmaz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliklere izin verebilir.

- **Parola yakınlık Isteklerini engelle**: bir kullanıcının cihazının yakındaki cihazlardan parola Isteyememesi için **Engelle** ' yi seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu parola isteklerine izin verebilir.
- **Parola paylaşmayı engelle**: **blok** , AirDrop kullanan cihazlar arasında parolaların paylaşılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parolaların paylaşılmasına izin verebilir.
- **Parola veya kredi kartı bilgileri Için dokunma kimliği veya yüz kimliği kimlik doğrulaması ıste otomatik doldurma**: **gerekli**olarak ayarlandığında, parolaların veya kredi kartı bilgilerinin otomatik olarak Safari ve diğer uygulamalarda otomatik olarak doldurulabilmesi için kullanıcıların TouchID veya çok yönlü kimliği kullanarak kimlik doğrulaması yapması gerekir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihaz ayarlarında bu özelliği denetlemesine izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri
  
<sup>1</sup> **parola istenmeden önce ekran kilitlenmesinden sonra ekran kilitlenmeden ve en fazla dakika geçtikten sonra** **işlem yapılmadan maksimum dakika** sayısını yapılandırdığınızda, bunlar sırayla uygulanır. Örneğin, her iki ayarın da değerini **5** dakikaya ayarlarsanız, ekran beş dakika sonra otomatik olarak kapanır ve cihazın kilitlenmesi için beş dakika daha geçmesi gerekir. Ancak, kullanıcılar ekranı el ile kapalarsa ikinci ayar hemen uygulanır. Aynı örnekte, kullanıcılar ekranı kapattıktan sonra cihaz beş dakika sonra kilitlenir.

## <a name="locked-screen-experience"></a>Kilit Ekranı Deneyimi

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Cihaz kilitliyken denetim merkezi erişimi**: **blok** , Cihaz kilitliyken Denetim Merkezi uygulamasına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, cihaz kilitlendiğinde kullanıcıların Denetim Merkezi uygulamasına erişmesine izin verebilir.
- **Cihaz kilitliyken bildirimler**: **blok** Cihaz kilitliyken bildirimlere erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kullanıcıların cihazın kilidini açmadan bildirimlere erişmelerine izin verebilir.
- **Cihaz kilitliyken bugün görünümü**: **blok** , Cihaz kilitliyken Bugün görünümüne erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, cihaz kilitlendiğinde kullanıcıların bugün görünümünü görmesine izin verebilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Cihaz kilitliyken cüzdan bildirimleri**: **blok** , Cihaz kilitliyken cüzdan uygulamasına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, Cihaz kilitliyken kullanıcıların cüzdan uygulamasına erişmesine izin verebilir.

## <a name="app-store-doc-viewing-gaming"></a>Uygulama Mağazası, Belge Görüntüleme, Oyun

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Yönetilmeyen uygulamalarda kurumsal belgeleri görüntüleme**: **blok** , şirket belgelerinin yönetilmeyen uygulamalarda görüntülenmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi şirket belgelerinin herhangi bir uygulamada görüntülenmesine izin verebilir. Örneğin kullanıcıların OneDrive uygulamasından Dropbox’a dosya kaydetmesini engellemek istiyorsunuz. Bu ayarı **Engelle** olarak yapılandırın. Cihaz ilkeyi aldıktan sonra (örneğin, yeniden başlatıldıktan sonra) artık kaydetmeye izin vermez.


  > [!NOTE]
  > Bu ayar engellendiğinde, App Store 'dan yüklenen üçüncü taraf klavyeler de engellenir.

  - **Yönetilmeyen uygulamaların yönetilen kişiler hesaplarından okumasına Izin ver**: **izin ver**olarak ayarlandığında, yerleşik IOS/ıpados kişileri uygulaması gibi yönetilmeyen uygulamalar, Outlook mobil uygulaması da dahil olmak üzere yönetilen uygulamalardaki iletişim bilgilerini okuyabilir ve bunlara erişebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazdaki yerleşik Kişiler uygulamasından yinelenenleri kaldırma dahil olmak üzere okumayı önleyebilir.  
  
    Bu ayar, iletişim bilgilerinin okunmasına izin verir veya bunu engeller. Uygulamalar arasındaki kişileri eşitlemeyi denetlemez.
  
    Bu ayarı kullanmak için **Yönetilmeyen uygulamalarda kurumsal belgeleri görüntüleme** ayarını **Engelle** olarak belirtin.

  Bu iki ayar hakkında daha fazla bilgi edinmek ve iOS/ıpados 'a yönelik Outlook 'a yönelik etkileri için Outlook 'ta etkileri için bkz. [destek İpucu: iOS/ıpados yerel kişiler uygulamasıyla Intune özel profil ayarlarını kullanma](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **AirDrop 'u yönetilmeyen hedef olarak değerlendir**: **gerektir** AirDrop, yönetilmeyen bir bırakma hedefi olarak değerlendirilir. Yönetilen uygulamaların Airdrop'u kullanarak veri göndermesini durdurur. 
- Kurumsal **olmayan belgeleri kurumsal uygulamalarda görüntüleme**: **blok** kurumsal uygulamalarda kurumsal olmayan belgelerin görüntülenmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi şirket tarafından yönetilen uygulamalarda herhangi bir belgenin görüntülenmesine izin verebilir.

  **Block** Ayrıca, IOS için Outlook 'Ta/ıpados 'a yönelik kişileri dışarı aktarma eşitlemesini engeller. Daha fazla bilgi için bkz. [destek İpucu: IOS12 MDM denetimleriyle Outlook iOS/ıpados Iletişim eşitlemesini etkinleştirme](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Tüm satın alımlarda ITunes mağazası parolası gerektir**: kullanıcıların her uygulama Içi veya iTunes satın alma IÇIN Apple kimlik parolasını girmesini **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi her seferinde parola istemeden satın alma işlemlerine izin verebilir.
- **Uygulama içi satın alımlar**: **blok** uygulama içi satın alımlara engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, çalışan bir uygulama içinde mağaza satın alımlara izin verebilir.
- **IBook mağazasından ' erotik ' olarak işaretlenen Içerik indir**: **Block** , kullanıcıların IBook mağazasından Erotika olarak etiketlenmiş bir medya indirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların "Erotika" kategorisiyle kitap indirmesine izin verebilir.
- **Yönetilen uygulamaların yönetilmeyen kişiler hesaplarına kişi yazmasına Izin ver**: **izin ver**olarak ayarlandığında, Outlook Mobile uygulaması gibi yönetilen uygulamalar, iş ve şirket kişileri dahil iletişim bilgilerini yerleşik IOS/ıpados kişileri uygulamasına kaydedebilir veya eşitleyebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, yönetilen uygulamaların cihazdaki yerleşik iOS/ıpados kişileri uygulamasına iletişim bilgilerini kaydetmesini veya eşitlemesini önleyebilir.
  
  Bu ayarı kullanmak için **Yönetilmeyen uygulamalarda kurumsal belgeleri görüntüleme** ayarını **Engelle** olarak belirtin.

- **Derecelendirme bölgesi**: izin verilen İndirilenler için kullanmak istediğiniz derecelendirme bölgesini seçin. Ardından, **filmler**, **TV programları**ve **uygulamalar**için izin verilen derecelendirmeleri seçin.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **App Store**: **Block** , denetimli cihazlarda uygulama deposuna erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi erişime izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

  - **App Store 'dan uygulama yükleme**: cihaz ana ekranından uygulama mağazasını engellemek için **Engelle** ' yi seçin. Kullanıcılar, uygulamaları yüklemek için iTunes 'u veya Apple Configurator 'ı kullanmaya devam edebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi ana ekranda uygulama deposuna izin verebilir.
  - **Otomatik uygulama indirmeleri**: **engelleme** , diğer cihazlarda satın alınan uygulamaların otomatik olarak indirilmesini engeller. Mevcut uygulamalarında yapılan güncelleştirmeler bundan etkilenmez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, diğer iOS/ıpados cihazlarında satın alınan uygulamaların cihaza indirilmesine izin verebilir.

- **Açık iTunes Music, podcast veya News içeriği**: **Block** açık iTunes Music, podcast veya News içeriğini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazın mağazadan yetişkinlere yönelik olarak derecelendirilmiş içeriğe erişmesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Game Center arkadaş ekleme**: **blok** kullanıcıların Game Center arkadaş eklemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Game Center arkadaş eklemesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Game Center**: Game Center uygulamasının kullanımını **engelleyin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda Game Center uygulamasının kullanılmasına izin verebilir.
- Çok **oyunculu oyunlar**: **blok** çok oyunculu oyunları önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazda çok oyunculu oyunlar oynamasına izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Dosyalar uygulamasında ağ sürücüsüne erişim**: sunucu ileti bloğu (SMB) protokolünü kullanarak, cihazlar bir ağ sunucusundaki dosyalara veya diğer kaynaklara erişebilir. **Devre dışı bırak ayarı** , BIR ağ SMB sürücüsündeki dosyalara erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi erişime izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="built-in-apps"></a>Yerleşik Uygulamalar

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Siri**: **Block** Siri 'e erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda Siri Voice Yardımcısı ile kullanılmasına izin verebilir.
  - **Siri Cihaz kilitliyken**: **blok** , Cihaz kilitliyken Siri 'e erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kilitli olduğunda cihazda Siri Voice Yardımcısı 'nı kullanmaya izin verebilir.

- **Safari sahtekarlık uyarıları**: cihazdaki Web tarayıcısında sahtekarlık uyarılarının gösterilmesi **gerekir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Internet 'ten sonuçları döndürmek Için Spotlight araması**: **Block** , projektörün bir Internet aramasından herhangi bir sonuç döndürmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Spotlight aramasının arama sonuçları sağlamak için Internet 'e bağlanmasına izin verebilir.

- **Safari tanımlama bilgileri**: cihazda tanımlama bilgilerinin nasıl işleneceğini seçin. Seçenekleriniz şunlardır:
  - İzin ver
  - Tüm tanımlama bilgilerini engelle
  - Ziyaret edilen web sitelerinin tanımlama bilgilerine izin ver
  - Geçerli web sitesinin tanımlama bilgilerine izin ver

- **Safari JavaScript**: **Block** tarayıcıda Java betiklerinin çalıştırılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Java betiklerine izin verebilir.

- **Safari açılır pencereleri**: Web tarayıcısında açılır pencere engelleyicisini devre dışı bırakma **bloğu** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi açılır pencere engelleyiciye izin verebilir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Kamera**: **blok** cihazdaki kameraya erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz kamerasına erişime izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

  - Çok **yönlü saat**: çok yönlü uygulama erişimini engelleme **bloğu** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda çok yönlü bir zaman uygulamasına erişime izin verebilir.

    İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Siri küfür filtresi**: **gerektir** , Siri 'ın dikte etmesini veya küfürlü dilini kullanmasını önler.

  Bu ayarı kullanmak için **Siri** ayarını **Engelle**olarak ayarlayın.

- **Siri Kullanıcı tarafından oluşturulan içeriği Internet 'ten sorgulamak için**: **Block** , soruların yanıt vermesi için Web sitelerine erişmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Siri 'ın Kullanıcı tarafından oluşturulan içeriğe internet 'ten erişmesine izin verebilir.

  Bu ayarı kullanmak için **Siri** ayarını **Engelle**olarak ayarlayın.

- **Apple News**: **blok** cihazdaki Apple News uygulamasına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Apple News uygulamasının kullanılmasına izin verebilir.
- **IBOOKS Store**: **Block** , iBooks deposuna erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların IBook Store 'dan kitaplar 'a gözatmasına ve satın almaya izin verebilir.
- **Cihazdaki iletiler uygulaması**: **blok** , kullanıcıların IMessage için iletiler uygulamasını kullanmalarını engeller. Cihaz metin iletilerini destekliyorsa, kullanıcılar SMS kullanarak SMS mesajları gönderip alabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iletileri Internet üzerinden göndermek ve okumak için Iletiler uygulamasının kullanılmasına izin verebilir.
- **Pod yayınları**: **blok** , kullanıcıların Pod yayınları uygulamasını kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Pod yayınları uygulamasının kullanılmasına izin verebilir.
- **Müzik hizmeti**: **blok** , müzik uygulamasını klasik moda geri döndürür ve müzik hizmetini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Apple Music uygulamasının kullanılmasına izin verebilir.
- **ITunes Radio hizmeti**: **Block** , kullanıcıların iTunes radyo uygulamasını kullanmalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iTunes Radio uygulamasının kullanılmasına izin verebilir.
- **iTunes Mağazası**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda iTunes 'a izin verebilir. **Blok** , kullanıcıların cihazda iTunes kullanmasını engeller.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 4,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **İPhone 'umu bul**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazın yaklaşık konumunu almak için bu uygulama Bul özelliğini kullanmaya izin verebilir. **Block** , bu özelliğin uygulamamda Bul özelliğini engelliyor. 

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **Arkadaşlarımı bul**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, bir Apple cihazından veya iCloud.com aile ve arkadaşlar bulmak için bu uygulamamı Bul özelliğini kullanmaya izin verebilir. **Block** , bu özelliğin uygulamamda Bul özelliğini engelliyor.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **Arkadaşlarımı bul uygulama ayarlarında yapılan değişiklikler**: **Block** Arkadaşlarımı bul uygulama ayarlarında değişiklik yapılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Arkadaşlarımı Bul uygulamasının ayarlarını değiştirmesine izin verebilir.

- **Internet 'ten sonuçları döndürmek Için Spotlight araması**: **Block** , projektörün bir Internet aramasından herhangi bir sonuç döndürmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Spotlight aramasının arama sonuçları sağlamak için Internet 'e bağlanmasına izin verebilir.

- **Cihazdan sistem uygulamalarının kaldırılmasını engelle**: **blok** seçme, sistem uygulamalarını cihazdan kaldırma yeteneğini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların sistem uygulamalarını kaldırmasına izin verebilir.

- **Safari**: cihazda Safari tarayıcısını kullanmayı **engelleyin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Safari tarayıcısını kullanmasına izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **Safari otomatik doldurma**: **blok** cihazdaki otomatik doldurma özelliğini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Web tarayıcısında otomatik tamamlama ayarlarını değiştirmesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

## <a name="restricted-apps"></a>Kısıtlı uygulamalar

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Kısıtlanmış uygulamalar listesi türü**: Kullanıcıların yüklemesine veya kullanmasına izin verilmeyen uygulamaların bir listesini oluşturun. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Kullanıcıların atadığınız uygulamalara ve yerleşik uygulamalarına erişimi vardır.
  - **Yasaklanmış uygulamalar**: Intune tarafından yönetilmeyen ve cihaza yüklenmesini istemediğiniz uygulamalar. Kullanıcıların yasaklanmış bir uygulamayı yüklemesi engellenmiyor. Ancak bir Kullanıcı bu listeden bir uygulama yüklerse Intune 'da raporlanır.
  - **Onaylanan uygulamalar**: Kullanıcıların yüklemesine izin verilen uygulamalar. Kullanıcılar listelenmeyen uygulamaları yüklememelidir. Intune tarafından yönetilen uygulamalara otomatik olarak izin verilir. Kullanıcıların onaylı uygulamalar listesinde olmayan bir uygulamayı yüklenmesi engellenmez. Ancak bunu yaptıysanız Intune 'da raporlanır.

Bu listelere uygulama eklemek için şunları yapabilirsiniz:

- İstediğiniz uygulamanın iTunes App mağazası URL'sini **ekleyin**. Örneğin, Microsoft çalışma klasörleri uygulamasını eklemek için `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` veya `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`girin.

  Uygulamanın URL'sini bulmak için, iTunes App Store'u açın ve uygulamayı arayın. Örneğin `Microsoft Remote Desktop` veya `Microsoft Word` için arama yapın. Uygulamayı seçin ve URL'sini kopyalayın.

  iTunes kullanarak da uygulamayı bulabilir ve ardından **Bağlantıyı Kopyala** görevini kullanıp uygulama URL’sini alabilirsiniz.

- URL 'SI dahil olmak üzere uygulamayla ilgili ayrıntılarla bir CSV dosyasını **Içeri aktarın** . `<app url>, <app name>, <app publisher>` biçimini kullanın. Veya, kısıtlanmış uygulamalar listesini içeren mevcut bir listeyi aynı biçimde **dışarı aktarın** .

> [!IMPORTANT]
> Kısıtlı uygulama ayarlarını kullanan cihaz profilleri kullanıcı gruplarına atanmalıdır.

## <a name="show-or-hide-apps"></a>Uygulamaları gösterme veya gizleme

İOS 9,3 + ve ıpados 13.0 + çalıştıran cihazlar için geçerlidir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Uygulama türü listesi**: gösterilecek veya gizlenecek uygulamaların bir listesini oluşturun. Yerleşik uygulamaları ve iş kolu uygulamalarını gösterebilir veya gizleyebilirsiniz. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur. Seçenekleriniz şunlardır:

  - **Gizli uygulamalar**: kullanıcılardan gizlenen uygulamaların listesini girin. Kullanıcılar bu uygulamaları görüntüleyemez veya açamaz.
  
    Apple, bazı yerel uygulamaların gizlenmelerini önler. Örneğin, cihazdaki **Ayarlar** uygulamasını gizleyemezsiniz. [Yerleşik Apple uygulamalarını silme](https://support.apple.com/HT208094) , gizli olabilecek uygulamaları listeler.
  
  - **Görünür uygulamalar**: kullanıcıların görüntüleyebileceği ve başlatabileceği uygulamaların bir listesini girin. Başka hiçbir uygulama görüntülenemez veya başlatılamaz.

- **Uygulama URL 'si**: göstermek veya gizlemek istediğiniz uygulamanın Mağaza uygulama URL 'sini girin. Örneğin:

  - Microsoft çalışma klasörleri uygulamasını eklemek için `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` veya `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`girin. 

  - Microsoft Word uygulamasını eklemek için `https://itunes.apple.com/de/app/microsoft-word/id586447913` veya `https://apps.apple.com/de/app/microsoft-word/id586447913`girin.

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

Veri dolaşımı için gereken Not (müşteri karışıklığına yardımcı olması için Ipucu veya önemli not): Bu ayar hedeflenen cihazın yönetim profilinde gösterilmez. Bunun nedeni, bu ayarın uzak bir cihaz eylemi olarak kabul edilmesidir ve cihazdaki veri dolaşımı durumu her değiştirildiğinde, Intune hizmeti tarafından yeniden engellenir. Yönetim profilinde olmasa dahi, yönetim konsolundaki raporlamadan başarı olarak gösterilse de çalışır. 
- **Veri dolaşımı**: **blok** , hücresel ağ üzerinde veri dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz hücresel ağ üzerindeyken veri dolaşımına izin verebilir.

  > [!IMPORTANT]
  > Bu ayar uzak cihaz eylemi olarak değerlendirilir. Bu nedenle, bu ayar cihazdaki yönetim profilinde gösterilmez. Cihazda veri dolaşımı durumu her değiştiğinde **veri dolaşımı** , Intune hizmeti tarafından engellenir. Intune 'da, raporlama durumu bir başarı gösteriyorsa, bu ayar cihazdaki yönetim profilinde gösterilmese de, çalıştığını öğrenin.

- **Dolaşım sırasında genel arka plan getirme**: **blok** , hücresel ağ üzerinde dolaşımda genel arka plan getirme özelliğinin kullanılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazın bir hücresel ağda dolaşımda olduğu gibi verileri (e-posta gibi) getirmeye izin verebilir.
- **Sesli arama**: **Block** , kullanıcıların cihazda sesli arama özelliğini kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda sesli aramaya izin verebilir.
- **Ses dolaşımı**: **blok** , hücresel ağ üzerinde ses dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, cihaz hücresel ağ üzerindeyken ses dolaşımına izin verebilir.
- **Kişisel etkin nokta**: **blok** her cihaz eşitlemesine sahip cihazlarda kişisel etkin noktayı kapatır. Bu ayar bazı taşıyıcılar ile uyumlu olmayabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kişisel etkin nokta yapılandırmasını varsayılan olarak kullanıcılar tarafından ayarlanmış olarak tutabilir.

  > [!IMPORTANT]
  > Bu ayar uzak cihaz eylemi olarak değerlendirilir. Bu nedenle, bu ayar cihazdaki yönetim profilinde gösterilmez. Kişisel etkin nokta durumu cihazda her değiştiğinde **Kişisel etkin nokta** , Intune hizmeti tarafından engellenir. Intune 'da, raporlama durumu bir başarı gösteriyorsa, bu ayar cihazdaki yönetim profilinde gösterilmese de, çalıştığını öğrenin.

- **Hücresel kullanım kuralları (yalnızca yönetilen uygulamalar)** : yönetilen uygulamaların hücresel ağlarda ne zaman kullanabileceği veri türlerini tanımlayın. Seçenekleriniz şunlardır:
  - **Hücresel veri kullanımını engelleyin**: **tüm yönetilen uygulamalar** için hücresel veri kullanmayı engelleyin veya **belirli uygulamaları seçin**.
  - **Dolaşım sırasında hücresel veri kullanımını engelle**: **tüm yönetilen uygulamalar** için Dolaşımda hücresel veri kullanmayı engelleyin veya **belirli uygulamaları seçin**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Uygulama hücresel veri kullanım ayarlarında yapılan değişiklikler**: **blok** , uygulama hücresel veri kullanımı ayarlarında değişiklik yapılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların hangi uygulamaların hücresel veri kullanmasına izin verileceğini denetlemesine izin verebilir.
- **Hücresel plan ayarlarındaki değişiklikler**: **blok** , kullanıcıların hücresel plandaki ayarları değiştirmelerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların değişiklik yapmasına izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 11,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **Kişisel etkin noktanın Kullanıcı değişikliği**: **engelleme**olarak ayarlandığında, kullanıcılar kişisel etkin nokta ayarını değiştiremezler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların kişisel etkin kullanımlarını etkinleştirmesine veya devre dışı bırakmasına izin verebilir.

  Bu ayarı engellerseniz ve **Kişisel etkin nokta** ayarını engellerseniz kişisel etkin nokta kapalıdır.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 12,2 ve üzeri
  - ıpados 13,0 ve üzeri

- **Yalnızca yapılandırma profillerini kullanarak Wi-Fi ağlarına katılarak**: **gerektir** ayarı, cihazı yalnızca Intune yapılandırma profilleri aracılığıyla ayarlanan Wi-Fi ağlarını kullanmaya zorlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazın diğer Wi-Fi ağlarını kullanmasına izin verebilir.

  **Gerektir**olarak ayarlandığında, cihazda bir Wi-Fi profili bulunduğundan emin olun. Bir Wi-Fi profili atamadıysanız, bu ayar cihazın İnternet 'e bağlanmasını engelleyebilir. Diğer bir deyişle, bu cihaz kısıtlama profili bir Wi-Fi profilinden önce atanırsa cihazın İnternet 'e bağlanması engellenebilir.
  
  Bağlanamıyorsa, cihazın kaydını kaldırın ve bir Wi-Fi profiliyle yeniden kaydedin. Ardından, bu ayarı cihaz kısıtlamaları profilinde **gerekli** olacak şekilde ayarlayın ve profili cihaza atayın.

- **Wi-Fi her zaman açık**: **gerektir**olarak ayarlandığında, Ayarlar uygulamasında Wi-Fi açık kalır. Cihaz uçak modundayken bile ayarlarda veya denetim merkezinde devre dışı bırakılamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Wi-Fi açmayı veya kapatmayı denetlemesine izin verebilir.

  Bu ayarın yapılandırılması, kullanıcıların bir Wi-Fi ağı seçmesini engellemez.

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="connected-devices"></a>Bağlı Cihazlar

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Eşleştirilmiş Apple Watch Için bilek algılama**: **gerektir** , eşleştirilmiş bir Apple Watch 'un bilek algılamayı kullanmasına zorlar. Gerekli seçilirse, Apple Watch takılmadığında bildirim görüntülemez. 

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **AirPlay giden istek eşleştirme parolasını gerektir**: kullanıcılar, diğer Apple cihazlarına içerik akışı sağlamak Için AirPlay kullandığında eşleştirme parolası **gerektir** . **Yapılandırılmadı** (varsayılan), kullanıcıların bir parola girmeden AirPlay kullanarak içerik akışına olanak sağlar.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **AirDrop**: **Block** cihazda AirDrop kullanımını engelliyor. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, Yakındaki cihazlarla içerik değişimi için AirDrop özelliğinin kullanılmasına izin verebilir.
- **Apple Watch eşleştirme**: **blok** bir Apple Watch eşlemeyi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazın bir Apple Watch eşleştirmeye izin verebilir.
- **Bluetooth değişikliği**: **engelleme** , kullanıcıların cihazdaki Bluetooth ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarları değiştirmesine izin verebilir.
- **İOS/ıpados cihazının eşleşebileceği cihazları denetlemek Için konak eşleştirme**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, yöneticinin bir iOS/ıpados cihazının hangi cihazlara eşlenebileceğini denetlemesine olanak tanımak için konak eşleştirmeye izin verebilir. **Engelle** ayarı konak eşleştirmeyi önler.
- **AirPrint 'ı engelle**: **blok** cihazdaki AirPrint özelliğinin kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların AirPrint kullanmasına izin verebilir.
  - **Anahtarlıkta AirPrint kimlik bilgilerinin depolanmasını engelle**: **blok** , cihazdaki Kullanıcı adı ve parola için Anahtarlık depolamanın kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, anahtar zinciri uygulamasında AirPrint Kullanıcı adını ve parolasını depolamaya izin verebilir.
  - **AirPrint için güvenilir BIR TLS sertifikası gerektir**: **gerektır** , cihazın TLS yazdırma iletişimi için güvenilir sertifikaları kullanmasını zorlar.
  - **AirPrint yazıcıları bloğunu engelle**: **blok** , ağ trafiği için kimlik avından kötü amaçlı AirPrint Bluetooth işaretlerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazdaki AirPrint yazıcılarına izin verebilir.
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

- **Sözcük tanımı arama**: **blok** , kullanıcının bir sözcüğü vurgulamasını ve sonra da cihazda tanımını aramasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi tanım arama özelliğine erişime izin verebilir.
- Tahmine **dayalı klavyeler**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların istedikleri sözcükleri önermek için tahmine dayalı klavyeler kullanılmasına izin verebilir. **Engelle** ayarı bu özelliği önler.
- **Otomatik Düzeltme**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazın yanlış yazılan sözcükleri otomatik olarak düzeltmesini sağlayabilir. **Engelle** ayarı otomatik düzeltme kullanılmasını önler.
- **Klavye yazım denetimi**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda SpellChecker kullanılmasına izin verebilir. **Engelle** ayarı yazım denetleyicisine izin verir.
- **Klavye kısayolları**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda klavye kısayollarının kullanılmasına izin verebilir. **Blok** , kullanıcıların klavye kısayollarını kullanmasını engeller.
- **Dikte**: **blok** , kullanıcıların metin girmek için ses girişi kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların dikte girişi kullanmasına izin verebilir.
- **Hızlı yol**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların, cihazın klavyesinde sürekli bir giriş sağlayan hızlı yol kullanmasına izin verebilir. Kullanıcılar, sözcükler oluşturmak için anahtarlar arasında çekerek yazı yazabilir. **Block** , kullanıcıların hızlı yol kullanmasını engeller. 

  Bu özellik şu platformlarda geçerlidir:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="cloud-and-storage"></a>Bulut ve Depolama

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Şifrelenmiş yedekleme**: **gerekli** olduğundan cihaz yedeklemelerinin şifrelenmesi gerekir.
- **Yönetilen uygulamalar buluta eşitlenir**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Intune 'a, uygulamaların kullanıcının iCloud hesabıyla veri eşitlemesine izin verebilir. **Engelle** ayarı iCloud'a bu veri eşitlemesini engeller.
- **Kurumsal kitap yedeklemesini engelle**: **Block** , kullanıcıların kurumsal kitaplar yedeklemesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu kitapları yedeklemelerine izin verebilir.
- **Kurumsal kitap meta verileri eşitlemesini engelleyin (notlar ve vurgular)** : **blok** , kurumsal kitaplar 'da notların ve vurguların eşitlenmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi eşitlemeye izin verebilir.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **İCloud 'A fotoğraf akışı eşitleniyor**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların cihazlarındaki **fotoğraf akışımı** iCloud 'a eşitlemesine ve tüm kullanıcıların cihazlarında fotoğraflar kullanmasına olanak sağlayabilir. **Engelle** ayarı iCloud'a fotoğraf akışının eşitlenmesini önler. Bu özelliğin engellenmesi veri kaybına neden olabilir. 
- **ICloud Fotoğraf Kitaplığı**: **blok** fotoğraflar ve videoları bulutta depolamak için iCloud Fotoğraf Kitaplığı kullanmayı devre dışı bırakır. iCloud Fotoğraf Arşivi'nden cihaza tamamen indirilmeyen tüm fotoğraflar cihazdan kaldırılır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud Fotoğraf Kitaplığı kullanımına izin verebilir.
- **Paylaşılan fotoğraf akışı**: **blok** , cihazda **iCloud Fotoğraf paylaşımını** devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi paylaşılan fotoğraf akışına izin verebilir.
- **İletim**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir iOS/ıpados cihazında çalışmaya başlamasını sağlayabilir ve sonra başka bir iOS/ıpados veya macOS cihazında başlatıldıklarında çalışmaya devam edebilir. **Engelle** ayarı bu iletimi önler.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **İCloud 'A yedekleme**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazı iCloud 'a yedeklemesine izin verebilir. **Blok** , kullanıcıların cihazı iCloud 'a yedeklemesini engeller.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **ICloud belge eşitlemesini engelle**: **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud depolama alanınızda belge ve anahtar-değer eşitlemeye izin verebilir. **Engelle** ayarı, iCloud'ın belgeleri ve verileri eşitlemesini engeller.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

- **ICloud anahtar zinciri eşitlemesini engelle**: **blok** , anahtarlıkta depolanan kimlik bilgilerinin iCloud 'a eşitlenmesini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu kimlik bilgilerini eşitlemesine izin verebilir.

  İOS/ıpados 13,0 ile başlayarak, bu ayar denetimli cihazlar gerektirir.

## <a name="autonomous-single-app-mode"></a>Otonom tek uygulama modu

İOS/ıpados cihazlarını, belirli uygulamaları otonom tek uygulama modunda çalıştıracak şekilde yapılandırmak için bu ayarları kullanın. Bu mod yapılandırıldığında ve kullanıcılar yapılandırılmış uygulamalardan birini başlatdıklarında, cihaz bu uygulamaya kilitlenir. Uygulama/görev değiştirme, kullanıcılar izin verilen uygulamadan çıkana kadar devre dışı bırakıldı.

Örneğin, okul veya üniversite ortamında, kullanıcıların cihazda bir test geçirmesine imkan tanıyan bir uygulama ekleyin. Ya da, Kullanıcı kimlik doğrulamasından çıkana kadar cihazı Şirket Portalı uygulamasına kilitleyin. Uygulamalar eylemleri kullanıcılar tarafından tamamlandığında veya bu ilkeyi kaldırdığınızda cihaz normal durumuna geri döner.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Uygulama adı**: istediğiniz uygulamanın adını girin.
- **Uygulama PAKETI kimliği**: istediğiniz UYGULAMANıN [paket kimliğini](bundle-ids-built-in-ios-apps.md) girin.
- **Ekle**: uygulama listenizi oluşturmak için seçin.

Ayrıca, uygulama adlarının ve paket kimliklerinin listesini içeren bir CSV dosyasını **Içeri aktarabilirsiniz** . Alternatif olarak uygulamaları içeren mevcut listeyi **dışarı aktarabilirsiniz**.

## <a name="kiosk"></a>Bilgi Noktası

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- **Bilgi noktası modunda çalıştırılacak uygulama**: bilgi noktası modunda çalıştırmak istediğiniz uygulama türlerini seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bilgi noktası ayarlarını uygulamayamayabilir. Cihaz bilgi noktası modunda çalışmıyor.
  - **Mağaza uygulaması**: iTunes App Store 'da bir uygulamanın URL 'sini girin.
  - **Yönetilen uygulama**: Intune 'a eklediğiniz bir uygulamayı seçin.
  - **Yerleşik uygulama**: yerleşik UYGULAMANıN [paket kimliğini](bundle-ids-built-in-ios-apps.md) girin.

- **Yardımcı dokunma**: cihazda yardımcı dokunma erişilebilirlik ayarının olması **gerekir** . Bu özellik kullanıcılara zorlanabilecekleri ekran hareketlerinde yardımcı olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Renkleri ters çevir**: görsel sorunları olan kullanıcıların ekran ekranını değiştirebilmeleri Için renkleri ters çevir erişilebilirlik ayarını **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Mono ses**: cihazda mono ses erişilebilirlik ayarının olması **gerekir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Voice Control**: **gerektir** , cihazda ses denetimi sağlar ve kullanıcıların Siri komutlarını kullanarak işletim sistemini tam olarak denetlemesine olanak tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda ses denetimini devre dışı bırakabilir.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri
  
  > [!TIP]
  > Kuruluşunuz için kullanılabilir LOB uygulamalarınız varsa ve iOS 13,0 yayımları olduğunda gün 0 ' da hazır bir **ses denetimi** yoksa, bu ayarı **yapılandırılmamış**olarak bırakmanız önerilir.

- **VoiceOver**: ekrandaki metin okumak için VoiceOver erişilebilirlik ayarının cihazda olması **gerekir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Yakınlaştır**: kullanıcıların ekranda yakınlaştırmak için dokunmatik kullanmasına izin vermek üzere yakınlaştırma ayarının cihazda olmasını **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği bilgi noktası modunda çalıştırmayabilir veya etkinleştiremeyebilir.
- **Otomatik kilit**: **engelleme** cihazın otomatik olarak kilitlenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Zil düğmesi**: **blok** cihazdaki zil (sessiz) geçiş devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Ekran döndürme**: **engelleme** , kullanıcılar Cihazı döndürürken ekran yönünün değiştirilmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Ekran uyku düğmesi**: **blok** cihazdaki ekran uyku modundan çıkarma düğmesini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.
- **Touch**: **Block** cihazdaki dokunmatik ekranı devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların dokunmatik ekranı kullanmasına izin verebilir.
- **Ses düğmeleri**: **blok** , cihazdaki ses düğmelerinin kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi ses düğmelerine izin verebilir.
- **Yardımcı dokunma denetimi**: kullanıcıların yardımcı Touch işlevini kullanmasına **izin ver** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.
- **Renkleri ters çevir denetimi**: kullanıcıların renkleri ters çevirme işlevini ayarlamasına izin vermek için renk değişikliklerine ters çevirmeyi **izin verin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.
- **Seçili metinde konuş**: konuşma seçimine **izin ver** erişilebilirlik ayarları cihazda olmalıdır. Bu özellik, kullanıcıların seçolduğu sesli metni okur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.
- **Ses denetimi değişikliği**: kullanıcıların cihazlarındaki ses denetimi durumunu değiştirmesine **izin verin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarındaki ses denetimi durumunu değiştirmelerini engelleyebilir.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 13,0 ve üzeri
  - ıpados 13,0 ve üzeri

- **VoiceOver Control**: kullanıcıların, ekran metinlerin hızlı bir şekilde okunması gibi VoiceOver işlevini güncelleştirmesine olanak tanımak için VoiceOver değişikliklere **izin verin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi VoiceOver değişikliğini engelleyebilir.
- **Yakınlaştırma denetimi**: kullanıcılara göre değişikliklere **izin ver** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi yakınlaştırılmış değişiklikleri engelleyebilir.

> [!NOTE]
> İOS/ıpados cihazını bilgi noktası modu için yapılandırmadan önce, Apple Configurator aracını veya Apple Aygıt Kayıt Programı kullanarak cihazı denetimli moda almanız gerekir. Apple Configurator aracını kullanma konusunda Apple'ın kılavuzuna bakın.
> Girdiğiniz iOS/ıpados uygulaması profili atadıktan sonra yüklendiyse, cihaz yeniden başlatılana kadar cihaz bilgi noktası moduna girmez.

## <a name="domains"></a>Etki alanları

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **İşaretlenmemiş e-** posta etki alanları > **eposta etki alanı URL 'si**: listeye bir veya daha fazla URL ekleyin. Kullanıcılar girdiğiniz etki alanlarından başka bir etki alanından e-posta aldığınızda, bu e-posta iOS/ıpados Mail uygulamasında güvenilmeyen olarak işaretlenir.

- **Yönetilen web etki alanları** > **Web Etki Alanı URL'si**; Listeye bir veya daha fazla URL ekleyin. Belgeler girdiğiniz etki alanlarından indirildiğinde yönetilen belgeler olarak değerlendirilir. Bu ayar yalnızca Safari tarayıcısı kullanılarak indirilen belgeler için geçerlidir.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı (denetimli)

- Safari parolası etki **alanı URL 'si** > **otomatik doldurma etki alanları** : listeye bir veya daha fazla URL ekleyin. Kullanıcılar yalnızca bu listedeki URL’lerdeki parolaları kaydedebilir. Bu ayar yalnızca Safari tarayıcısı ve denetimli moddaki cihazlar için geçerlidir. Herhangi bir URL girmezseniz, parolalar tüm Web sitelerinden kaydedilebilir.

  Bu ayarın geçerli olduğu sürümler:  
  - iOS 9,3 ve üzeri
  - ıpados 13,0 ve üzeri

## <a name="settings-that-require-supervised-mode"></a>Denetimli mod gerektiren ayarlar

iOS/ıpados Denetimli mod yalnızca Apple Aygıt Kayıt Programı aracılığıyla veya Apple Configurator kullanılarak ilk cihaz kurulumu sırasında etkinleştirilebilir. Denetimli mod etkinleştirildikten sonra, Intune şu işlevleri kullanarak bir cihazı yapılandırabilir:

- Uygulama Kilidi (Tek Uygulama Modu) 
- Genel HTTP Proxy’si 
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
- News 
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
> - Oyun Merkezi Arkadaşları Ekleyin
> - Siri

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[macOS](device-restrictions-macos.md) cihazlarındaki özellikleri ve ayarları da kısıtlayabilirsiniz.
