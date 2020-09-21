---
title: Microsoft Intune - Azure'da macOS ayarlarını kullanma | Microsoft Docs
titleSuffix: ''
description: Microsoft Intune özellikleri kısıtlamak için macOS cihazlarındaki ayarları ekleyin, yapılandırın veya oluşturun. Parola gereksinimlerini ayarlama, kilitli ekranı denetleme, yerleşik uygulamalar kullanma, kısıtlı veya onaylanan uygulamalar ekleme, Bluetooth cihazlarını işleme, yedekleme ve depolama için buluta bağlanma, bilgi noktası modunu etkinleştirme, etki alanlarını ekleme ve kullanıcıların Safari Web tarayıcısı ile nasıl etkileşime gireceğini denetleme.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d762f3729f104bedc992c93f1a445ab00b547841
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813668"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune'u kullanarak özelliklere izin vermeyi veya bunları kısıtlamayı sağlayan macOS cihaz ayarları

Bu makalede macOS cihazlarda denetleyebileceğiniz farklı ayarlar listelenmekte ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüz kapsamında bu ayarları kullanabilir ve bu sayede özellikleri etkinleştirip devre dışı bırakabilir, parola kuralları uygulayabilir, belirli uygulamalara izin verebilir veya bunları kısıtlayabilir ve çok daha fazlasını yapabilirsiniz.

Bu ayarlar, Intune'da bir cihaz yapılandırma profiline eklenir ve daha sonra macOS cihazlarınıza atanır veya dağıtılır.

> [!NOTE]
> Kullanıcı arabirimi bu makaledeki kayıt türleriyle eşleşmeyebilir. Bu makaledeki bilgiler doğru. Kullanıcı arabirimi yaklaşan bir sürümde güncelleştiriliyor.

## <a name="before-you-begin"></a>Başlamadan önce

[MacOS cihaz kısıtlamaları yapılandırma profili](device-restrictions-configure.md)oluşturun.

> [!NOTE]
> Bu ayarlar farklı kayıt türleri için geçerlidir. Farklı kayıt türleri hakkında daha fazla bilgi için bkz. [MacOS kaydı](../enrollment/macos-enroll.md).

## <a name="built-in-apps"></a>Yerleşik Uygulamalar

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Safari Safari otomatik doldurma**: **Evet** , cihazlarda Safari içindeki otomatik doldurma özelliğini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Web tarayıcısında otomatik tamamlama ayarlarını değiştirmesine izin verebilir.
- **Kameranın kullanımını engelle**: **Evet** seçeneği cihazlarda kameraya erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz kamerasına erişime izin verebilir.

  Intune yalnızca cihaz kamerasına erişimi yönetir. Resimlere veya videolara erişimi yoktur.
  
- **Engelle Apple Music**: **Evet** , müzik uygulamasını klasik moda geri döndürür ve müzik hizmetini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Apple Music uygulamasının kullanılmasına izin verebilir.
- **Spotlight önerilerini engelle**: **Evet** , projektörün bir Internet aramasından herhangi bir sonuç döndürmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Spotlight aramasının Internet 'e bağlanmasına ve arama sonuçları almaya izin verebilir.
- **Finder veya iTunes kullanarak dosya aktarımını engelle**: **Evet** , uygulama dosya paylaşımı hizmetlerini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi uygulama dosya paylaşım hizmetlerine izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - macOS 10,13 ve üzeri

## <a name="cloud-and-storage"></a>Bulut ve depolama

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **ICloud anahtar zinciri eşitlemesini engelle**: **Evet** , anahtarlıkta depolanan kimlik bilgilerinin iCloud 'a eşitlenmesini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu kimlik bilgilerini eşitlemesine izin verebilir.
- **ICloud masaüstü ve belge eşitlemesini engelle**: **Evet** , iCloud 'ın belge ve verileri eşitlemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud depolama alanınızda belge ve anahtar-değer eşitlemeye izin verebilir.
- **ICloud posta yedeklemesini engelle**: **Evet** , ICloud 'ın MacOS posta uygulamasıyla eşitlenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a posta eşitlemeye izin verebilir.
- **İCloud 'La Iletişim yedeklemeyi engelle**: **Evet** , iCloud 'ın cihaz kişilerini eşitlemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud kullanarak kişi eşitlemesine izin verebilir.
- **ICloud takvim yedeklemesini engelle**: **Evet** , ICloud 'ın MacOS Takvim uygulamasıyla eşitlenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a takvim eşitlemesine izin verebilir.
- **ICloud anımsatıcı yedeklemesini engelle**: **Evet** , ICloud 'ın MacOS anımsatıcıları uygulamasıyla eşitlenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a anımsatıcılar eşitlemeye izin verebilir.
- **ICloud yer Işareti yedeklemesini engelle**: **Evet** , ICloud 'ın cihaz yer imlerini eşitlemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a yer Işareti eşitlemeye izin verebilir.
- **ICloud notları yedeklemesini engelle**: **Evet** , iCloud 'ın cihaz notlarını eşitlemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a notlara eşitlemeye izin verebilir.
- **İCloud Fotoğraf yedeklemesini engelleyin**: **Evet** iCloud Fotoğraf kitaplığını devre dışı bırakır ve iCloud 'ın cihaz fotoğraflarını eşitlemesini önler. İCloud fotoğraf kitaplığından tamamen indirilmeyen tüm fotoğraflar, cihazlardaki yerel depolama alanından kaldırılır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz ile iCloud Fotoğraf Kitaplığı arasında fotoğraflar eşitlemeye izin verebilir.
- **Iletimi engelle**: Bu özellik, kullanıcıların bir MacOS cihazında çalışmaya başlamasını sağlar ve sonra başka bir IOS/ıpados veya MacOS cihazında başlatıldıklarında çalışmaya devam eder. **Evet** , cihazlarda iletim özelliğini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda bu özelliğe izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - macOS 10,15 ve üzeri

## <a name="connected-devices"></a>Bağlı cihazlar

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **AirDrop engelle**: **Evet** , cihazlarda AirDrop kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, Yakındaki cihazlarla içerik değişimi için AirDrop özelliğinin kullanılmasına izin verebilir.
- **Apple Watch otomatik kilit açma engelle**: **Evet** seçeneği, kullanıcıların MacOS cihazını Apple Watch kilidini açmalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların macOS cihazını Apple Watch kilidini açmalarına izin verebilir.

## <a name="domains"></a>Etki Alanları

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Işaretlenmemiş e-posta etki alanları**: listeye bir veya daha fazla **e-posta etki alanı URL 'si** Kullanıcılar eklediğiniz etki alanları dışında bir etki alanından e-posta gönderdiklerinde veya aldığı zaman, macOS Mail uygulamasında e-posta güvenilir değil olarak işaretlenir.

## <a name="general"></a>Genel

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Arama engelle**: **Evet** seçeneği, kullanıcının bir sözcüğü vurgulamasını ve sonra cihazda tanımını aramasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi tanım arama özelliğine izin verebilir.
- **Dikte etmeyi engelle**: **Evet** seçeneği, kullanıcıların metin girmek için sesli giriş kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların dikte girişi kullanmasına izin verebilir.
- **İçerik önbelleğe almayı engelle**: **Evet** , içerik önbelleğe almayı engeller. İçerik önbelleğe alma, uygulama verilerini, Web tarayıcısı verilerini, indirmeleri ve daha fazlasını cihazlarda yerel olarak depolar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi içerik önbelleğe almayı etkinleştirebilir.

  macOS cihazlarda içeriği önbelleğe alma özelliği hakkında daha fazla bilgi için bkz. [Mac'te içeriği önbelleğe almayı yönetme](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (başka bir web sitesini açar).

  Bu özellik şu platformlarda geçerlidir:  
  - macOS 10,13 ve üzeri

- Ekran **görüntülerini ve ekran kaydını engelle**: cihazın Apple 'ın otomatik cihaz kaydı 'NDA (DEP) kayıtlı olması gerekir. **Evet** seçeneği, kullanıcıların ekran ekran görüntülerini kaydetmelerini engeller. Ayrıca, derslik uygulamasının uzak ekranları gözlemmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların ekran görüntülerini yakalamasına izin verebilir ve derslik uygulamasının uzak ekranları görüntülemesine olanak tanır.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment-supervised"></a>Ayarlar için geçerlidir: Kullanıcı tarafından onaylanan cihaz kaydı, otomatik cihaz kaydı (denetimli)

- **Yazılım güncelleştirmelerini ertele**: **Evet** , cihazlar üzerinde işletim sistemi güncelleştirmeleri ve işletim sistemi olmayan güncelleştirmeler gösterildiğinde gecikme yapmanıza izin verir. Bu ayar, güncelleştirmelerin yüklenme tarihini veya durumunu denetlemez. Hiçbir şey seçili olmadığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Varsayılan olarak, işletim sistemi cihazlarda güncelleştirmeleri Apple yayınları olarak gösterebilir. Varsayılan olarak, yazılım güncelleştirmeleri gecikmez. Bu ayarı yapılandırırsanız, seçtiğiniz seçeneklere bağlı olarak işletim sistemi ve işletim sistemi olmayan yazılım güncelleştirmeleri gecikir. Açılan liste, tam olarak seçtiğiniz şeydir. Her ikisini de geciktirebilir, erteleyebilir ya da onlardan birini erteleyebilir.

  Örneğin, bir macOS güncelleştirmesi Apple tarafından belirli bir tarihte yayımlanmışsa, bu güncelleştirme doğal olarak yayın tarihi etrafında cihazlarda görüntülenir. Çekirdek derleme güncelleştirmelerine gecikme olmadan izin verilir.  

  - **Yazılım güncelleştirmeleri gecikmesi**: 0-90 günden bir değer girin. Güncelleştirmeler varsayılan olarak günler için gecikmiştir `30` . Bu değer, seçtiğiniz **yazılım güncelleştirmelerini ertele** seçeneklerini uygular. Yalnızca **işletim sistemi güncelleştirmelerini**seçerseniz, 30 gün boyunca yalnızca işletim sistemi güncelleştirmeleri gecikir. **İşletim sistemi güncelleştirmeleri** ve **işletim sistemi olmayan güncelleştirmeler**' i seçerseniz, her ikisi de 30 gün gecikmiştir.

    Gecikme süresi sona erdiğinde, kullanıcılar gecikme tetiklendiğinde kullanılabilir olan en eski sürümü güncelleştirme hakkında bir bildirim alır.

    Örneğin, bir macOS güncelleştirmesi **1 Ocak**'ta kullanılabiliyorsa ve **gecikme görünürlüğü** **5 güne**ayarlanırsa, güncelleştirme kullanılabilir bir güncelleştirme olarak gösterilmez. Sürümden sonraki **altıncı gün** üzerinde, bu güncelleştirme kullanılabilir ve kullanıcılar uygulamayı yükleyebilir.

    Bu özellik şu platformlarda geçerlidir:  
    - macOS 10.13.4 ve üzeri

### <a name="settings-apply-to-automated-device-enrollment"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı

- **AirPlay 'ı devre dışı bırakın, derslik uygulamasına göre ekranı görüntüleyin ve ekran paylaşımı**: **Evet** , AirPlay 'i engeller ve diğer cihazlara ekran paylaşımını önler. Ayrıca, öğretmenlerin öğrencilerin ekranlarını görmek için ders uygulamasını kullanmalarını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğretmenlerin öğrencilerinin ekranlarını görmesine izin verebilir.

  Bu ayarı kullanmak için, **blok ekran görüntülerini ve ekran kaydı** ayarını **Yapılandırılmadı** olarak ayarlayın (ekran görüntülerine izin verilir).

- **Sınıf uygulamasının, sormadan AirPlay ve görüntüleme ekranı gerçekleştirmesine Izin ver**: **Evet: Evet** , öğretmenlere öğrenci 'nin anlaşmasına gerek kalmadan öğrencilerinin ekranlarını görmesine izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğretmenler ekranları görebilmesi için öğrencilerinin kabul etmesini gerektirebilir.

  Bu ayarı kullanmak için, **blok ekran görüntülerini ve ekran kaydı** ayarını **Yapılandırılmadı** olarak ayarlayın (ekran görüntülerine izin verilir).

- **Sınıf uygulaması yönetilmeyen sınıflarının ayrılmaları için öğretmen Izni gerektir**: **Evet** , bir yönetilmeyen sınıfta kayıtlı öğrencileri, kursu bırakmaya yönelik öğretmen onayı almak üzere zorlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğrencilerin öğrenciye her seçişinde kursa ayrılmalarını sağlayabilir.

- **Sınıfa sormadan cihazı kilitlemesine Izin ver**: **Evet** , öğretmenlerin öğrencinin onayını almadan bir öğrencinin cihazını veya uygulamasını kilitlemesine olanak tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, öğretmenler cihazı veya uygulamayı kilitleyebilmesi için önce öğrencilerden uyuşmayı gerektirebilir.

- **Öğrenciler, ders sınıfına sormadan otomatik olarak katılabilir**: **Evet** , öğrencilerin öğretmeden bir sınıfa katılmasına izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bir sınıfa katılması için öğretmen onayı gerektirebilir.

## <a name="password"></a>Parola

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Parola gerektir**: **Evet** seçeneği, kullanıcıların cihazlara erişmek için bir parola girmesini gerektirir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bir parola gerektirmeyebilir. Ayrıca basit parolaları engelleme veya minimum uzunluğu ayarlama gibi herhangi bir kısıtlamayı zorlamaz.
  - **Gerekli parola türü**: kuruluşunuzun gerektirdiği gerekli parola karmaşıklığı düzeyini girin. Boş bırakılırsa, Intune bu ayarı değiştirmez veya güncelleştirmez. Seçenekleriniz şunlardır:
    - **Yapılandırılmadı**: cihaz varsayılanını kullanır.
    - **Alfasayısal**: büyük harfler, küçük harfler ve sayısal karakterler içerir.
    - **Sayısal**: parola yalnızca sayı olmalıdır, örneğin 123456789.

    Bu özellik şu platformlarda geçerlidir:  
    - macOS 10.10.3 ve üzeri

  - **Paroladaki alfasayısal olmayan karakter sayısı**: 0-4 adresinden, parolada gereken karmaşık karakter sayısını girin. Karmaşık bir karakter, gibi bir simgedir `?` . Boş bırakılırsa veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Minimum parola uzunluğu**: parolanın, 4-16 karakterden fazla olması gereken minimum uzunluğu girin. Boş bırakılırsa, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Basit parolaları engelle**: **Evet** , veya gibi basit parolaların kullanılmasını önler `0000` `1234` . Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi basit parolalara izin verebilir.
  - Ekran **kilitlenmeden önce geçen işlem yapılmayan dakika sayısı**: ekran otomatik olarak kilitlenmeden önce cihazların boşta olması gereken sürenin uzunluğunu girin. Örneğin, `5` 5 dakika çalıştıktan sonra cihazları kilitlemek için yazın. Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Parola istenmeden önce ekran kilitlenmesinden sonra geçen en fazla dakika**: kilidini açmak için bir parola istenmeden önce cihazların etkin olmaması gereken sürenin uzunluğunu girin. Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Parola kullanım süresi (gün)**: cihaz parolasının, 1-65535 adresinden sonra değiştirilmesi gereken gün sayısını girin. Örneğin, `90` 90 gün sonra parolanın süresini dolacak şekilde girin. Parola geçerlilik süresi dolduğunda kullanıcıların yeni bir parola oluşturması istenir. Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Önceki parolaların yeniden kullanılmasını engelle**: kullanıcıların daha önce kullanılmış parolalar oluşturmasını kısıtla. 1-24 adresinden, daha önce kullanılmış olan parolaların sayısını girin. Örneğin, kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için 5 girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Kullanıcının geçiş kodunu değiştirmesini engelle**: **Evet** , geçiş kodunun değiştirilmesini, eklenmesini veya kaldırılmasını bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, geçiş kodlarını 'in eklenmesine, değiştirilmesine veya kaldırılmasına izin verebilir.

- **Cihazın kilidini açmak Için dokunma kimliğini engelle**: **Evet** seçeneği, cihazların kilidini açmak için parmak izi kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parmak izi kullanarak cihazın kilidini açmalarını sağlayabilir.

- **Parola Otomatik doldurmayı engelle**: **Evet** , MacOS 'ta parolaları otomatik doldur özelliğinin kullanılmasını önler. **Evet** ' in belirlenmesi aşağıdaki etkiye de sahiptir:

  - Safari'de veya diğer uygulamalarda kullanıcılara parolaları kaydetmek isteyip istemedikleri sorulmaz.
  - Otomatik Güçlü Parolalar devre dışı bırakılır ve kullanıcılara güçlü parola önerisi sunulmaz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliklere izin verebilir.

- **Parola yakınlık Isteklerini engelle**: **Evet** seçeneği cihazların yakındaki cihazlardan parola istememelerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu parola isteklerine izin verebilir.

- **Parola paylaşımını engelle**: **Evet** , AirDrop kullanan cihazlar arasında parolaların paylaşılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parolaların paylaşılmasına izin verebilir.

## <a name="privacy-preferences"></a>Gizlilik Tercihleri

MacOS cihazlarında, uygulamalar ve süreçler genellikle kullanıcılardan kamera, mikrofon, takvim, Belgeler klasörü gibi cihaz özelliklerine izin vermeyi veya erişimi reddetmesini ister. Bu ayarlar, yöneticilerin bu cihaz özelliklerine erişimi önceden onaylamasını veya ön reddetmesini sağlar. Bu ayarları yapılandırdığınızda, kullanıcılarınız adına veri erişimi onayını yönetirsiniz. Ayarlarınız önceki kararlarını geçersiz kılar.

Bu ayarların amacı, uygulama ve işlemlere göre istem sayısını azaltmaktır.

Bu özellik şu platformlarda geçerlidir:

- macOS 10,14 ve üzeri
- Bazı ayarlar macOS 10,15 ve üzeri için geçerlidir.
- Bu ayarlar yalnızca, yükseltmeden önce gizlilik tercihleri profili yüklü olan cihazlara uygulanır.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Ayarlar için geçerlidir: Kullanıcı tarafından onaylanan cihaz kaydı, otomatik cihaz kaydı

- **Uygulamalar ve süreçler**: erişimi yapılandırmak için uygulama veya işlem **ekleyin** . Şunları da girin:
  - **Ad**: uygulamanız veya işleminiz için bir ad girin. Örneğin `Microsoft Remote Desktop` veya `Microsoft 365` girin.
  
  - **Tanımlayıcı türü**: seçenekleriniz:
    - **Paket kimliği**: uygulamalar için bu seçeneği belirleyin.
    - **Yol**: bir işlem veya çalıştırılabilir olmayan, paketlenmiş ikili dosyalar için bu seçeneği belirleyin.

    Bir uygulama paketi içine katıştırılmış yardımcı araçlar, kapsayan uygulama paketi izinlerini otomatik olarak alır.

  - **Tanımlayıcı**: uygulama paketi kimliğini veya işlemin veya yürütülebilir dosyanın yükleme dosya yolunu girin. Örneğin, `com.contoso.appname` girin.

    Uygulama paketi KIMLIĞINI almak için, Terminal uygulamasını açın ve `codesign` komutunu çalıştırın. Bu komut kod imzasını tanımlar. Bu nedenle paket KIMLIĞI ve kod imzasını eşzamanlı olarak alabilirsiniz.

  - **Kod gereksinimi**: uygulama veya işlem için kod imzasını girin.

    Bir uygulama veya ikili bir geliştirici sertifikası tarafından imzalandığında bir kod imzası oluşturulur. Atamasını bulmak için, `codesign` komutu Terminal uygulamasında el ile çalıştırın: `codesign --display -r - /path/to/app/binary` . Kod imzası, sonrasında görüntülenen şeydir `=>` .

  - **Statik kod doğrulamasını etkinleştir**: uygulama veya işlemin kod gereksinimini statik olarak doğrulaması için **Evet** ' i seçin. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

    Bu ayarı yalnızca işlem dinamik kod imzasını geçersiz kılmak durumunda etkinleştirin. Aksi takdirde, **öğesini kullanın.**  

  - **Kamerayı engelle**: **Evet** seçeneği, uygulamanın sistem kameraya erişmesini önler. Kameraya erişime izin alamazsınız. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  - **Mikrofonu engelle**: **Evet** , uygulamanın sistem mikrofonuna erişmesini önler. Mikrofona erişime izin vermiyoruz. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  - **Ekran kaydını engelle**: **Evet** seçeneği, uygulamanın sistem ekranının içeriğini yakalanmasını engeller. Ekran kaydetmeye ve ekran yakalamaya erişime izin vermiyoruz. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

    MacOS 10,15 ve üstünü gerektirir.

  - **Giriş Izlemeyi engelle**: **Evet** seçeneği, UYGULAMANıN Coregraphics ve HID API 'Lerini kullanarak tüm işlemlerden cgevents ve HID olaylarını dinlemesini engeller. **Evet** Ayrıca, uygulama ve işlemlerin fare, klavye veya tekerleksiz gibi giriş cihazlarından veri dinlemesini ve verileri toplamasını engeller. CoreGraphics ve HID API 'Lerine erişime izin vermiyoruz.

    **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

    MacOS 10,15 ve üstünü gerektirir.

  - **Konuşma tanıma**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın sistem konuşma tanıma erişimine erişmesini sağlar ve Apple 'a konuşma verileri göndermeye izin verir.
    - **Engelle**: uygulamanın sistem konuşma tanıma 'ya erişmesini önler ve Apple 'a konuşma verileri gönderilmesini engeller.

    MacOS 10,15 ve üstünü gerektirir.

  - **Erişilebilirlik**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın sistem erişilebilirlik uygulamasına erişmesine izin verir. Bu uygulama kapalı açıklamalı altyazı, üzerine gelme metni ve ses denetimi içerir.
    - **Engelle**: uygulamanın sistem erişilebilirlik uygulamasına erişmesini önler.

  - **Kişiler**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın, sistem kişileri uygulaması tarafından yönetilen kişi bilgilerine erişmesine izin verir.  
    - **Engelle**: uygulamanın bu iletişim bilgilerine erişmesini önler.

  - **Takvim**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın, sistem takvimi uygulaması tarafından yönetilen takvim bilgilerine erişmesine izin verir.
    - **Engelle**: uygulamanın bu takvim bilgilerine erişmesini önler.

  - **Anımsatıcılar**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın sistem anımsatıcıları uygulaması tarafından yönetilen anımsatıcı bilgilerine erişmesine izin verir.
    - **Engelle**: uygulamanın bu anımsatıcı bilgilerine erişmesini önler.

  - **Fotoğraflar**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın Içindeki sistem fotoğrafları uygulaması tarafından yönetilen resimlere erişmesine izin verir `~/Pictures/.photoslibrary` .
    - **Engelle**: uygulamanın bu resimlere erişmesini önler.

  - **Medya Kitaplığı**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın Apple Music, müzik ve video etkinliğine ve Medya kitaplığına erişmesine izin verir.  
    - **Engelle**: uygulamanın bu medyaya erişmesini önler.

    MacOS 10,15 ve üstünü gerektirir.

  - **Dosya sağlayıcısı varlığı**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın dosya sağlayıcısı uygulamasına erişmesine izin verir ve kullanıcıların dosya sağlayıcısı tarafından yönetilen dosyaları ne zaman kullandığını bilir. Bir dosya sağlayıcısı uygulaması, diğer dosya sağlayıcısı uygulamalarının, kapsayan uygulama tarafından depolanan ve yönetilen belgelere ve dizinlere erişmesine olanak sağlar.
    - **Engelle**: uygulamanın dosya sağlayıcısı uygulamasına erişmesini önler.

    MacOS 10,15 ve üstünü gerektirir.

  - **Tam disk erişimi**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın sistem yönetimi dosyaları da dahil olmak üzere tüm korumalı dosyalara erişmesine izin verir. Bu ayarı dikkatli uygulayın.
    - **Engelle**: uygulamanın bu korumalı dosyalara erişmesini önler.

  - **Sistem Yöneticisi dosyaları**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın sistem yönetiminde kullanılan bazı dosyalara erişmesine izin verir.
    - **Engelle**: uygulamanın bu dosyalara erişmesini önler.

  - **Masaüstü klasörü**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın, kullanıcının masaüstü klasöründeki dosyalara erişmesine izin verir.
    - **Engelle**: uygulamanın bu dosyalara erişmesini önler.

    MacOS 10,15 ve üstünü gerektirir.

  - **Belgeler klasörü**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın kullanıcının Belgeler klasöründeki dosyalara erişmesine izin verir.
    - **Engelle**: uygulamanın bu dosyalara erişmesini önler.

    MacOS 10,15 ve üstünü gerektirir.

  - **İndirmeler klasörü**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın, kullanıcının indirmeler klasöründeki dosyalara erişmesine izin verir.
    - **Engelle**: uygulamanın bu dosyalara erişmesini önler.

    MacOS 10,15 ve üstünü gerektirir.

  - **Ağ birimleri**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın ağ birimlerindeki dosyalara erişmesine izin verir.
    - **Engelle**: uygulamanın bu dosyalara erişmesini önler.

    MacOS 10,15 ve üstünü gerektirir.

  - **Çıkarılabilir birimler**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın sabit disk gibi çıkarılabilir birimlerde dosyalara erişmesine izin verir.
    - **Engelle**: uygulamanın bu dosyalara erişmesini önler.

    MacOS 10,15 ve üstünü gerektirir.

  - **Sistem olayları**: seçenekleriniz:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Izin ver**: uygulamanın, sistem olay akışına CGEvents göndermek Için Coregraphics API 'lerini kullanmasına izin verir.
    - **Engelle**: uygulamanın, CGEvents 'i sistem olay akışına göndermek Için Coregraphics API 'lerini kullanmasını önler.

  - **Apple olayları**: Bu ayar, uygulamaların başka bir uygulama veya işleme kısıtlı bir Apple olayı göndermesini sağlar. Alıcı uygulama veya işlem eklemek için **Ekle** ' yi seçin. Alan uygulamanın veya işlemin aşağıdaki bilgilerini girin:

    - **Tanımlayıcı türü**: alma tanımlayıcısı bir uygulama Ise, **paket kimliği** ' ni seçin. Alma tanımlayıcısı bir işlem veya yürütülebilir ise **yolu** seçin.

    - **Tanımlayıcı**: uygulama paketi kimliğini veya bir Apple olayı alan işlemin yükleme yolunu girin.  

    - **Kod gereksinimi**: alıcı uygulama veya işlem için kod imzasını girin.

      Bir uygulama veya ikili bir geliştirici sertifikası tarafından imzalandığında bir kod imzası oluşturulur. Atamasını bulmak için, `codesign` komutu Terminal uygulamasında el ile çalıştırın: `codesign --display -r -/path/to/app/binary` . Kod imzası, sonrasında görüntülenen şeydir `=>` .

    - **Erişim**: bir MacOS Apple olayının alıcı uygulamaya veya işleme gönderilmesine izin verin. Seçenekleriniz şunlardır:
      - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
      - **Izin ver**: uygulamanın veya işlemin, alan uygulamaya veya Işleme kısıtlı Apple olayını göndermesini sağlar.
      - **Engelle**: uygulamanın veya işlemin, alıcı uygulama veya işleme kısıtlı bir Apple olayı göndermesini önler.

  - Değişikliklerinizi **kaydedin** .

## <a name="restricted-apps"></a>Kısıtlı uygulamalar

### <a name="settings-apply-to-all-enrollment-types"></a>Ayarlar için geçerlidir: tüm kayıt türleri

- **Kısıtlanmış uygulamalar listesi türü**: Kullanıcıların yüklemesine veya kullanmasına izin verilmeyen uygulamaların bir listesini oluşturun. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, kullanıcıların atadığınız uygulamalara ve yerleşik uygulamalara erişimi olabilir.
  - **Onaylanan uygulamalar**: Kullanıcıların yüklemesine izin verilen uygulamaları listeleyin. Uyumluluğun korunması için kullanıcılar diğer uygulamaları yüklememelidir. Şirket Portalı uygulaması da dahil olmak üzere Intune tarafından yönetilen uygulamalara otomatik olarak izin verilir. Kullanıcıların onaylı uygulamalar listesinde olmayan bir uygulamayı yüklenmesi engellenmez. Ancak bunu yaptıysanız Intune 'da raporlanır.
  - **Yasaklanmış uygulamalar**: Kullanıcıların yüklemesine ve çalıştırmasına izin verilmeyen uygulamaları (Intune tarafından yönetilmeyen) listeleyin. Kullanıcıların yasaklanmış bir uygulamayı yüklemesi engellenmiyor. Bir Kullanıcı bu listeden bir uygulama yüklerse Intune 'da raporlanır.

- **Uygulamalar listesi**: listenize uygulama **ekleme** :
  - **Uygulama PAKETI kimliği**: UYGULAMANıN [paket kimliğini](bundle-ids-built-in-ios-apps.md) girin. Yerleşik uygulamalar ve iş kolu uygulamaları ekleyebilirsiniz. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur.

    Uygulamanın URL'sini bulmak için, iTunes App Store'u açın ve uygulamayı arayın. Örneğin `Microsoft Remote Desktop` veya `Microsoft Word` için arama yapın. Uygulamayı seçin ve URL'sini kopyalayın. iTunes kullanarak da uygulamayı bulabilir ve ardından **Bağlantıyı Kopyala** görevini kullanıp uygulama URL’sini alabilirsiniz.

  - **Uygulama Adı**: Paket kimliğini ayırt etmenize yardımcı olacak bir kolay ad ekleyin. Örneğin, `Intune Company Portal app` girin.
  - **Yayımcı**: uygulamanın yayımcısını girin.

- URL 'SI dahil olmak üzere uygulamayla ilgili ayrıntılarla bir CSV dosyasını **Içeri aktarın** . `<app bundle ID>, <app name>, <app publisher>` biçimini kullanın. Ya da, eklediğiniz uygulamaların bir listesini aynı biçimde oluşturmak için **dışa aktarın** .

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

Ayrıca, [iOS/ıpados](device-restrictions-ios.md) cihazlarında cihaz özelliklerini ve ayarlarını kısıtlayabilirsiniz.
