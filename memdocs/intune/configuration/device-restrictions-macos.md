---
title: Microsoft Intune - Azure'da macOS ayarlarını kullanma | Microsoft Docs
titleSuffix: ''
description: Parola gereksinimlerini belirleme, kilit ekranını denetleme, yerleşik uygulamaları kullanma, kısıtlanmış veya onaylı uygulamalar ekleme, Bluetooth cihazlarını yönetme, yedekleme ve depolama amacıyla buluta bağlanma, bilgi noktası modunu etkinleştirme, etki alanı ekleme ve kullanıcıların Safari web tarayıcısıyla etkileşim kurma şeklini denetleme gibi özellikleri kısıtlama amacıyla Microsoft Intune'daki macOS cihazlar için ayar ekleme, yapılandırma veya oluşturma işlemlerini gerçekleştirin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7054cb658314d00c3e10388c50c2309038c8a15b
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359123"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune'u kullanarak özelliklere izin vermeyi veya bunları kısıtlamayı sağlayan macOS cihaz ayarları

Bu makalede macOS cihazlarda denetleyebileceğiniz farklı ayarlar listelenmekte ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) yönteminizin bir parçası olarak bu ayarları kullanabilir ve bu sayede özellikleri etkinleştirip devre dışı bırakabilir, parola kuralları uygulayabilir, belirli uygulamalara izin verebilir veya bunları kısıtlayabilir ve çok daha fazlasını yapabilirsiniz.

Bu ayarlar, Intune'da bir cihaz yapılandırma profiline eklenir ve daha sonra macOS cihazlarınıza atanır veya dağıtılır.

## <a name="before-you-begin"></a>Başlamadan önce

[Cihaz kısıtlamaları yapılandırma profili oluşturma](device-restrictions-configure.md).

> [!NOTE]
> Bu ayarlar farklı kayıt türleri için geçerlidir. Farklı kayıt türleri hakkında daha fazla bilgi için bkz. [MacOS kaydı](../enrollment/macos-enroll.md).

## <a name="general"></a>Genel

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: cihaz kaydı ve otomatik cihaz kaydı

- **Tanım arama**: **blok** , kullanıcının bir sözcüğü vurgulamasını ve sonra da cihazda tanımını aramasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi tanım arama özelliğine izin verebilir.
- **Dikte**: **blok** , kullanıcıların metin girmek için ses girişi kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların dikte girişi kullanmasına izin verebilir.
- **İçerik önbelleğe alma**: **engelleme** , içerik önbelleğe almayı engeller. İçerik önbelleğe alma, uygulama verilerini, Web tarayıcısı verilerini, indirmeleri ve daha fazlasını cihazlarda yerel olarak depolar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi içerik önbelleğe almayı etkinleştirebilir.

  macOS cihazlarda içeriği önbelleğe alma özelliği hakkında daha fazla bilgi için bkz. [Mac'te içeriği önbelleğe almayı yönetme](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (başka bir web sitesini açar).

  Bu özellik şu platformlarda geçerlidir:  
  - macOS 10,13 ve üzeri

- **Yazılım güncelleştirmelerini ertele**: **Etkinleştir** ayarı, cihazlarda 0-90 günden itibaren yazılım güncelleştirmeleri gösterildiğinde gecikmenizi sağlar. Bu ayar, güncelleştirmelerin yüklenme tarihini veya durumunu denetlemez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda güncelleştirmeleri Apple yayınları olarak gösterebilir. Örneğin, bir macOS güncelleştirmesi Apple tarafından belirli bir tarihte yayımlanmışsa, bu güncelleştirme doğal olarak yayın tarihi etrafında cihazlarda görüntülenir. Çekirdek derleme güncelleştirmelerine gecikme olmadan izin verilir.  

  - **Yazılım güncelleştirmeleri gecikmesi**: 0-90 günden bir değer girin. Gecikme süresi sona erdiğinde kullanıcılara gecikmenin tetiklendiği tarihte kullanılabilir durumda olan en eski işletim sistemi sürümüne güncelleştirme bildirimi gönderilir.

    Örneğin, bir macOS güncelleştirmesi **1 Ocak**'ta kullanılabiliyorsa ve **gecikme görünürlüğü** **5 güne**ayarlanırsa, güncelleştirme kullanılabilir bir güncelleştirme olarak gösterilmez. Sürümden sonraki **altıncı gün** üzerinde, bu güncelleştirme kullanılabilir ve kullanıcılar uygulamayı yükleyebilir.

    Bu özellik şu platformlarda geçerlidir:  
    - macOS 10.13.4 ve üzeri

- **Ekran görüntüleri**: cihazın Apple 'ın otomatik cihaz kaydı 'NDA (DEP) kayıtlı olması gerekir. **Block** , kullanıcıların ekran ekran görüntülerini kaydetmelerini engeller. Ayrıca, derslik uygulamasının uzak ekranları gözlemmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların ekran görüntülerini yakalamasına izin verebilir ve derslik uygulamasının uzak ekranları görüntülemesine olanak tanır.

### <a name="settings-apply-to-automated-device-enrollment"></a>Ayarlar için geçerlidir: otomatik cihaz kaydı

- **Sınıf uygulaması aracılığıyla uzak ekran**izleme: **devre dışı bırakma** , öğretmenlerin öğrencilerin ekranlarını görmek için sınıf uygulamasını kullanmalarını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğretmenlerin öğrencilerinin ekranlarını görmesine izin verebilir.

  Bu ayarı kullanmak için **ekran görüntüleri** ayarını **Yapılandırılmadı** olarak ayarlayın (ekran görüntülerine izin verilir).

- **Sınıf uygulamasına göre sorulmadan ekran izleme**: **izin ver** , öğretmenlere öğrenci 'nin kabul etmesini gerektirmeden öğrencilerinin ekranlarını görmesine imkan tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğretmenler ekranları görebilmesi için öğrencilerinin kabul etmesini gerektirebilir.

  Bu ayarı kullanmak için **ekran görüntüleri** ayarını **Yapılandırılmadı** olarak ayarlayın (ekran görüntülerine izin verilir).

- **Öğrenciler sınıf sınıfına ayrılmak için izin istemelidir**: bir yönetilmeyen sınıfta kayıtlı öğrencileri, kursu bırakmaya yönelik öğretmen onayı almak için **ister** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi öğrencilerin öğrenciye her seçişinde kursa ayrılmalarını sağlayabilir.

- **Öğretmenler, sınıf uygulamasındaki cihazları veya uygulamaları otomatik olarak kilitleyebilir**: **izin ver** öğretmenlerin öğrencinin onayını almadan bir öğrencinin cihazını veya uygulamasını kilitlemesine olanak tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, öğretmenler cihazı veya uygulamayı kilitleyebilmesi için önce öğrencilerden uyuşmayı gerektirebilir.

- **Öğrenciler ders sınıfına otomatik olarak katılabilir**: **izin ver** , öğrenciye sormadan bir sınıfa katılmasına olanak sağlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bir sınıfa katılması için öğretmen onayı gerektirebilir.

## <a name="password"></a>Parola

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: cihaz kaydı ve otomatik cihaz kaydı

- **Parola**: kullanıcıların cihazlara erişmek için parola girmesini **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bir parola gerektirmeyebilir. Ayrıca basit parolaları engelleme veya minimum uzunluğu ayarlama gibi herhangi bir kısıtlamayı zorlamaz.
  - **Gerekli parola türü**: kuruluşunuzun gerektirdiği gerekli parola karmaşıklığı düzeyini girin. Seçenekleriniz şunlardır:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Sayısal**: parola yalnızca sayı olmalıdır, örneğin 123456789.
    - **Alfasayısal**: büyük harfler, küçük harfler ve sayısal karakterler içerir.

    Bu özellik şu platformlarda geçerlidir:  
    - macOS 10.10.3 ve üzeri

  - **Paroladaki alfasayısal olmayan karakter sayısı**: 0-4 adresinden, parolada gereken karmaşık karakter sayısını girin. Karmaşık bir karakter, `?` gibi bir simgedir
  - **Minimum parola uzunluğu**: parolanın, 4-16 karakterden fazla olması gereken minimum uzunluğu girin.
  - **Basit parolalar**: `0000` veya `1234`gibi basit parolalar kullanılmasına izin verin.
  - **Parola istenmeden önce ekran kilitlenmesinden sonra geçen en fazla dakika**: kilidini açmak için bir parola istenmeden önce cihazların etkin olmaması gereken sürenin uzunluğunu girin. Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - Ekran **kilitlenmeden önce geçen işlem yapılmayan dakika sayısı**: ekran otomatik olarak kilitlenmeden önce cihazların boşta olması gereken sürenin uzunluğunu girin. Örneğin, 5 dakika boşta kaldıktan sonra cihazları kilitlemek için 5 girin. Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Parola kullanım süresi (gün)** : cihaz parolasının, 1-65535 adresinden sonra değiştirilmesi gereken gün sayısını girin. Örneğin, 90 gün sonra parolayı sona erdirmek için `90` girin. Parola geçerlilik süresi dolduğunda kullanıcıların yeni bir parola oluşturması istenir. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Önceki parolaların yeniden kullanılmasını engelle**: kullanıcıların daha önce kullanılan parolaları oluşturmasını kısıtlamak için bu ayarı kullanın. 1-24 adresinden, daha önce kullanılmış olan parolaların sayısını girin. Örneğin, kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için 5 girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Kullanıcının geçiş kodunu değiştirmesini engelle**: **blok** , geçiş kodunun değiştirilmesini, eklenmesini veya kaldırılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, geçiş kodlarını 'in eklenmesine, değiştirilmesine veya kaldırılmasına izin verebilir.
- **Blok Parmak Izi kilidini açma**: **blok** cihazların kilidini açmak için parmak izlerinin kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parmak izi kullanarak cihazın kilidini açmalarını sağlayabilir.

- **Parola Otomatik doldurmayı engelle**: **blok** , MacOS üzerinde parolaları otomatik doldur özelliğinin kullanılmasını önler. **Engelle** ayarını seçmek şu sonuçlara da neden olur:

  - Safari'de veya diğer uygulamalarda kullanıcılara parolaları kaydetmek isteyip istemedikleri sorulmaz.
  - Otomatik Güçlü Parolalar devre dışı bırakılır ve kullanıcılara güçlü parola önerisi sunulmaz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliklere izin verebilir.

- **Parola yakınlık Isteklerini engelle**: **blok** cihazların yakındaki cihazlardan parola istemelerine engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu parola isteklerine izin verebilir.

- **Parola paylaşmayı engelle**: **blok** , AirDrop kullanan cihazlar arasında parolaların paylaşılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parolaların paylaşılmasına izin verebilir.

## <a name="built-in-apps"></a>Yerleşik Uygulamalar

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: cihaz kaydı ve otomatik cihaz kaydı

- **Safari Safari otomatik doldurma**: **blok** cihazlarda otomatik doldurma özelliğini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Web tarayıcısında otomatik tamamlama ayarlarını değiştirmesine izin verebilir.
- **Kamerayı engelle**: **blok** cihazlarda kameraya erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz kamerasına erişime izin verebilir.
- **Engelle Apple Music**: **blok** , müzik uygulamasını klasik moda geri döndürür ve müzik hizmetini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Apple Music uygulamasının kullanılmasına izin verebilir.
- **Spotlight Internet araması sonuçlarını engelle**: **blok** , projektörün bir Internet aramasından sonuçları döndürmesini durduruyor. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Spotlight aramasının Internet 'e bağlanmasına ve arama sonuçları almaya izin verebilir.
- **İTunes kullanarak dosya aktarımını engelle**: **blok** uygulama dosya paylaşımı hizmetlerini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi uygulama dosya paylaşım hizmetlerine izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - macOS 10,13 ve üzeri

## <a name="restricted-apps"></a>Kısıtlı uygulamalar

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: cihaz kaydı ve otomatik cihaz kaydı

- **Kısıtlanmış uygulamalar listesi türü**: Kullanıcıların yüklemesine veya kullanmasına izin verilmeyen uygulamaların bir listesini oluşturun. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, kullanıcıların atadığınız uygulamalara ve yerleşik uygulamalara erişimi olabilir.
  - **Yasaklanmış uygulamalar**: Kullanıcıların yüklemesine ve çalıştırmasına izin verilmeyen uygulamaları (Intune tarafından yönetilmeyen) listeleyin. Kullanıcıların yasaklanmış bir uygulamayı yüklemesi engellenmiyor. Bir Kullanıcı bu listeden bir uygulama yüklerse Intune 'da raporlanır.
  - **Onaylanan uygulamalar**: Kullanıcıların yüklemesine izin verilen uygulamaları listeleyin. Uyumluluğun korunması için kullanıcılar diğer uygulamaları yüklememelidir. Şirket Portalı uygulaması da dahil olmak üzere Intune tarafından yönetilen uygulamalara otomatik olarak izin verilir. Kullanıcıların onaylı uygulamalar listesinde olmayan bir uygulamayı yüklenmesi engellenmez. Ancak bunu yaptıysanız Intune 'da raporlanır.

- **Uygulama PAKETI kimliği**: istediğiniz uygulamanın uygulama [paket kimliğini](bundle-ids-built-in-ios-apps.md) girin. Yerleşik uygulamaları ve iş kolu uygulamalarını gösterebilir veya gizleyebilirsiniz. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur.
- **Uygulama adı**: istediğiniz uygulamanın uygulama adını girin. Yerleşik uygulamaları ve iş kolu uygulamalarını gösterebilir veya gizleyebilirsiniz. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur.
- **Yayımcı**: uygulamanın yayımcısını girin.

Bu listelere uygulama eklemek için şunları yapabilirsiniz:

- **Ekle**: uygulama listenizi oluşturmak için seçin.
- URL 'SI dahil olmak üzere uygulamayla ilgili ayrıntılarla bir CSV dosyasını **Içeri aktarın** . `<app bundle ID>, <app name>, <app publisher>` biçimini kullanın. Ya da, eklediğiniz uygulamaların bir listesini aynı biçimde oluşturmak için **dışa aktarın** .

## <a name="connected-devices"></a>Bağlı cihazlar

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: cihaz kaydı ve otomatik cihaz kaydı

- **AirDrop bloğu**: **Block** cihazlarda AirDrop kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, Yakındaki cihazlarla içerik değişimi için AirDrop özelliğinin kullanılmasına izin verebilir.
- **Apple Watch otomatik kilit açma engelle**: **Block** , kullanıcıların MacOS cihazını Apple Watch kilidini açmalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların macOS cihazını Apple Watch kilidini açmalarına izin verebilir.

## <a name="cloud-and-storage"></a>Bulut ve depolama

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: cihaz kaydı ve otomatik cihaz kaydı

- **ICloud anahtar zinciri eşitlemesini engelle**: **blok** , anahtarlıkta depolanan kimlik bilgilerinin iCloud 'a eşitlenmesini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu kimlik bilgilerini eşitlemesine izin verebilir.
- **ICloud belge eşitlemesini engelle**: **blok** , iCloud 'ın belge ve verileri eşitlemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud depolama alanınızda belge ve anahtar-değer eşitlemeye izin verebilir.
- **ICloud posta yedeklemesini engelle**: **blok** , ICloud 'ın MacOS posta uygulamasıyla eşitlenmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a posta eşitlemeye izin verebilir.
- **İCloud 'La Iletişim yedeklemeyi engelle**: **blok** , iCloud 'ın cihaz kişilerini eşitlemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud kullanarak kişi eşitlemesine izin verebilir.
- **ICloud takvim yedeklemesini engelle**: **blok** , ICloud 'ın MacOS Takvim uygulamasıyla eşitlenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a takvim eşitlemesine izin verebilir.
- **ICloud anımsatıcı yedeklemesini engelle**: **blok** , ICloud 'ın MacOS anımsatıcıları uygulamasıyla eşitlenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a anımsatıcılar eşitlemeye izin verebilir.
- **ICloud yer Işareti yedeklemesini engelle**: **blok** , ICloud 'ın cihaz yer imlerini eşitlemesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a yer Işareti eşitlemeye izin verebilir.
- **ICloud notları yedeklemesini engelle**: **blok** , iCloud 'ın cihaz notlarını eşitlemesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iCloud 'a notlara eşitlemeye izin verebilir.
- **ICloud Fotoğraf kitaplığını engelle**: **blok** iCloud Fotoğraf kitaplığını devre dışı bırakır ve iCloud 'ın cihaz fotoğraflarını eşitlemesini önler. İCloud fotoğraf kitaplığından tamamen indirilmeyen tüm fotoğraflar, cihazlardaki yerel depolama alanından kaldırılır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz ile iCloud Fotoğraf Kitaplığı arasında fotoğraflar eşitlemeye izin verebilir.
- **İletim**: Bu özellik, kullanıcıların bir MacOS cihazında çalışmaya başlamasını sağlar ve sonra başka bir IOS/ıpados veya MacOS cihazında başlattıkları işleri devam eder. **Blok** , cihazlarda iletim özelliğini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda bu özelliğe izin verebilir.

  Bu özellik şu platformlarda geçerlidir:  
  - macOS 10,15 ve üzeri

## <a name="domains"></a>Domains

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Ayarlar için geçerlidir: cihaz kaydı ve otomatik cihaz kaydı

- **E-posta etki alanı URL 'si**: listeye bir veya daha fazla URL **ekleyin** . Kullanıcılar, yapılandırdığınız sunucudan farklı bir etki alanından e-posta aldıklarında, macOS Mail uygulamasında e-posta güvenilir değil olarak işaretlenir.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

Ayrıca, [iOS/ıpados](device-restrictions-ios.md) cihazlarında cihaz özelliklerini ve ayarlarını kısıtlayabilirsiniz.
