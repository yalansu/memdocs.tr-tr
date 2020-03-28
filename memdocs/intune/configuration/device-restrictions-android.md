---
title: Microsoft Intune'da Android için cihaz kısıtlama ayarları - Azure | Microsoft Docs
description: Microsoft Intune denetleyebilmeniz ve sınırlandırdığınız tüm Android Cihaz Yöneticisi ayarlarının listesini görüntüleyin. Parolayı denetlemek, Google Play'e erişmek, uygulamalara izin vermek veya bunları yasaklamak, tarayıcı ayarlarını denetlemek, uygulamaları engellemek, Google bulutuna yedekleme yapmak ve mesaj, ses, veri dolaşımı, Wi-Fi ve Bluetooth bağlantı seçeneklerini denetlemek için bu ayarları kullanın.
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
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea84544223d890be7e61fafa5de082c242250403
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359342"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Intune 'da Android ve Samsung KNOX Standard cihaz kısıtlama ayarları listeleri

Bu makalede, Android çalıştıran cihazlar için yapılandırabileceğiniz tüm Microsoft Intune cihaz kısıtlama ayarları gösterilir.

>[!TIP]
>İstediğiniz ayarlar mevcut değilse cihazlarınızı bir [özel profil](custom-settings-android.md) kullanarak yapılandırabilirsiniz.

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](device-restrictions-configure.md).

## <a name="general"></a>Genel

- **Kamera**: **blok** kameraya erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz kamerasına erişime izin verebilir.
- **Kopyala ve Yapıştır (yalnızca Samsung KNOX)** : **blok** kopyalama ve yapıştırmayı önler. **Yapılandırılmadı** , cihazlarda kopyalama ve yapıştırma işlevlerine izin verir.
- **Uygulamalar arasında Pano paylaşımı (yalnızca Samsung KNOX)** : **blok** , uygulamalar arasında kopyalama ve yapıştırma için panonun kullanılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda kopyalama ve yapıştırma işlevlerine izin verebilir.
- **Tanılama verileri gönderme (yalnızca Samsung KNOX)** : **Block** , kullanıcıların cihazlardan hata raporları göndermesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların verileri göndermesine izin verebilir.
- **Temizleme (yalnızca Samsung KNOX)** : kullanıcıların cihazlarda [silme](../remote-actions/devices-wipe.md) eylemi çalıştırmasına izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Coğrafi konum (yalnızca Samsung KNOX)** : **blok** cihazların konum bilgilerini kullanmasını devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazların konum bilgilerini kullanmasına izin verebilir.
- **Kapatma (yalnızca Samsung KNOX)** : **Block** , kullanıcıların cihazı kapatmasına engel olur. Ayrıca, cihaz ayarının yapılandırılmasını ve çalışmayı **kaldırmadan önce oturum açma hatalarının sayısını** da engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazların gücünü kapatmasına izin verebilir.
- **Ekran yakalama (yalnızca Samsung KNOX)** : **engelleme** ekran görüntülerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların ekran içeriğini görüntü olarak yakalamasına izin verebilir.
- **Sesli yardımcı (yalnızca Samsung KNOX)** : **blok** , S Ses hizmetini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda S Voice Service ve App kullanılmasına izin verebilir. Bu ayar, Bıxby için veya ekran içeriğini yüksek sesle okuyan erişilebilirlik için ses Yardımcısı 'na uygulanmaz.
- **YouTube (yalnızca Samsung KNOX)** : **Block** , kullanıcıların YouTube uygulamasını kullanmalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda YouTube uygulamasının kullanılmasına izin verebilir.
- **Paylaşılan cihazlar (yalnızca Samsung KNOX)** : yönetilen bir Samsung KNOX Standard cihazını paylaşılan olarak yapılandırın. **Izin ver** , KULLANıCıLARıN Azure AD kimlik bilgileriyle cihazların oturum açmasını ve tükenmelerini sağlar. Cihazlar, kullanımda olup olmadıkları zaman yönetilmeye devam ediyor.

  Bir SCEP sertifika profili ile birlikte kullanıldığında, bu özellik kullanıcıların tüm kullanıcılar için aynı uygulamalarla bir cihaz paylaşmasına izin verir. Ancak, her kullanıcının kendi SCEP Kullanıcı sertifikası vardır. Kullanıcılar oturumu kapattığında tüm veriler silinir. Bu özellik yalnızca LOB uygulamalarıyla sınırlıdır.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi birden çok kullanıcının Azure AD kimlik bilgilerini kullanarak cihazlarda Şirket Portalı uygulamasında oturum açmasını önleyebilir.
- **Tarih ve saat değişikliklerini engelle (Samsung KNOX)** : **Block** , kullanıcıların cihazlarda tarih ve saat ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların tarih ve saat ayarlarını değiştirmesine izin verebilir.

## <a name="password"></a>Parola

- **Parola**: kullanıcıların cihazlara erişmek için parola girmesini **gerektir** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parola girmeden cihazlara erişmelerine izin verebilir.

    > [!NOTE]
    > Samsung Knox cihazlar, MDM kaydı sırasında otomatik olarak 4 basamaklı bir PIN gerektirir. Yerel Android cihazlar, koşullu erişimle uyumlu hale gelmesi için otomatik olarak bir PIN gerektirebilir.

- **Minimum parola uzunluğu**: 4-16 adresinden gereken en az karakter sayısını girin. Örneğin, parola uzunluğu için en az altı sayı veya karakter gerektirmek üzere `6` girin.
- **Ekran kilitlenmeden önce geçen işlem yapılmayan dakika sayısı**: ekran otomatik olarak kilitlenmeden önce cihazın boşta kalması gereken süreyi girin. Örneğin, 5 dakika boşta kaldıktan sonra cihazları kilitlemek için `5` girin. Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Bir cihazda, kullanıcılar profilde yapılandırılan süreden daha büyük bir zaman değeri ayarlayamamakta. Kullanıcılar, daha düşük bir saat değeri ayarlayabilir. Örneğin, profil `15` dakika olarak ayarlandıysa, kullanıcılar değeri 5 dakikaya ayarlayabilir. Kullanıcılar değeri 30 dakika olarak ayarlayamıyorum.

- **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: cihazların temizlenmeden önce izin verilen hatalı parola sayısını 4-11 adresinden girin. `0` (sıfır) cihaz temizleme işlevini devre dışı bırakabilir. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Parola kullanım süresi (gün)** : cihaz parolasının, 1-365 adresinden değiştirilinceye kadar gün sayısını girin. Örneğin, 90 gün sonra parolayı sona erdirmek için `90` girin. Parola geçerlilik süresi dolduğunda kullanıcıların yeni bir parola oluşturması istenir. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Gerekli parola türü**: gerekli parola karmaşıklığı düzeyini ve biyometrik cihazların kullanılıp kullanılamayacağını girin. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı**
  - **Düşük güvenlik Biyometri**: [güçlü ve zayıf Biyometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (Android 'in Web sitesini açar)
  - **En az sayısal**: `123456789`gibi sayısal karakterler içerir.
  - **Sayısal karmaşık**: "1111" veya "1234" gibi yinelenen veya ardışık numaralara izin verilmez. Bu ayarı cihazlara atamadan önce, Şirket Portalı uygulamasını bu cihazlarda en son sürüme güncelleştirdiğinizden emin olun.

    **Sayısal karmaşık**olarak ayarlandığında ve ayarı 5,0 ' den önceki bir Android sürümünü çalıştıran cihazlara atarsanız, aşağıdaki davranış geçerlidir:

    - Şirket Portalı uygulaması 1704 'den önceki bir sürümü çalıştırıyorsa, cihazlara bir PIN ilkesi uygulanmaz ve Microsoft Uç Nokta Yöneticisi Yönetim merkezinde bir hata görüntülenir.
    - Şirket Portalı uygulaması 1704 veya üzeri bir sürüm çalıştırıyorsa yalnızca basit bir PIN uygulanabilir. 5,0 'den önceki Android sürümü bu ayarı desteklemiyor. Microsoft Endpoint Manager Yönetim merkezinde herhangi bir hata gösterilmez.

  - En **az alfabetik**: alfabede harfler içerir. Rakamlar ve simgeler zorunlu tutulmaz.
  - En **az alfasayısal**: büyük harfler, küçük harfler ve sayısal karakterler içerir.
  - **Semboller ile en az alfasayısal**: büyük harfler, küçük harfler, sayısal karakterler, noktalama işaretleri ve semboller içerir.

- **Önceki parolaların yeniden kullanılmasını engelle**: kullanıcıların daha önce kullanılan parolaları oluşturmasını kısıtlamak için bu ayarı kullanın. 1-24 adresinden, daha önce kullanılmış olan parolaların sayısını girin. Örneğin, kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için `5` girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Parmak iziyle kilit açma (yalnızca Samsung KNOX)** : **blok** cihazların kilidini açmak için parmak izi kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parmak izi kullanarak cihazların kilidini açmaya izin verebilir.
- **Akıllı kilit ve diğer güven aracıları**: **blok** akıllı kilit veya diğer güven aracılarının kilit ekranı ayarlarını değiştirmesine engel olur. Cihaz güvenilir bir konumdayken, güven aracısı olarak da bilinen bu özellik, cihaz kilit ekranı parolasını devre dışı bırakmanıza veya atlamanıza izin verir. Örneğin, cihazlar belirli bir Bluetooth cihazına bağlıyken veya cihazlar bir NFC etiketine yakın olduğunda bu özelliği kullanın. Bu ayarı kullanıcıların Akıllı Kilitleme’yi yapılandırmasını önlemek için kullanabilirsiniz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Bu ayarın geçerli olduğu sürümler:

  - Samsung KNOX Standard 5.0 +

- **Şifreleme**: cihazdaki dosyaların şifrelenmesi için **gerektir** ' i seçin. Tüm cihazlar şifrelemeyi desteklemez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Bu ayarı yapılandırmak ve uyumluluğu doğru şekilde raporlamak için aşağıdakileri de yapılandırın:
  1. **Password**: **gerektir**olarak ayarlayın.
  2. **Gerekli parola türü**: **en az sayısal**olarak ayarlanır.
  3. **Minimum parola uzunluğu**: en az `4`olarak ayarlanır.

  > [!NOTE]
  > Bir şifreleme ilkesi uygulanırsa Samsung Knox cihazlar, kullanıcıların cihaz parolası olarak 6 karakterli karmaşık bir parola ayarlamasını gerektirir.

## <a name="google-play-store"></a>Google Play Store

- **Google Play Store (yalnızca Samsung KNOX)** : **Block** , kullanıcıların Google Play deposunu kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazlarda Google Play deposuna erişmelerine izin verebilir.

## <a name="restricted-apps"></a>Kısıtlı uygulamalar

Cihazlarda belirli uygulamalara izin vermek veya bunları engellemek için bu ayarları kullanın. Bu özellik Android ve Samsung KNOX Standard cihazlarında desteklenir.

- **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Yasaklanmış uygulamalar**: Kullanıcıların yüklemesine ve çalıştırmasına izin verilmeyen uygulamaları (Intune tarafından yönetilmeyen) listeleyin. Kullanıcı bu listedeki bir uygulamayı yüklerse, Intune bunu size bildirir.
- **Onaylanan uygulamalar**: Kullanıcıların yüklemesine izin verilen uygulamaları listeleyin. Uyumluluğun korunması için kullanıcılar diğer uygulamaları yüklememelidir.  Şirket Portalı uygulaması da dahil olmak üzere Intune tarafından yönetilen uygulamalara otomatik olarak izin verilir.
- **Uygulamalar listesi**: uygulamanızı **ekleyin** :
  - **Uygulama PAKETI kimliği**: uygulama paket kimliğini girin.
  - **App Store URL 'si**: istediğiniz uygulamanın Google Play Store URL 'sini girin. Örneğin, Android için Microsoft Uzak Masaüstü uygulamasını eklemek için `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`girin.

    Bir uygulamanın URL 'sini bulmak için [Google Play Store](https://play.google.com/store/apps)' u açın ve uygulamayı arayın. Örneğin `Microsoft Remote Desktop Play Store` veya `Microsoft Planner` için arama yapın. Uygulamayı seçin ve URL'sini kopyalayın.
  
  - **Uygulama adı**: istediğiniz adı girin. Bu ad kullanıcılara gösterilir.
  - **Yayımcı** (isteğe bağlı): `Microsoft`gibi uygulamanın yayımcısını girin.

Ayrıca, URL de dahil olmak üzere uygulamayla ilgili ayrıntılarla bir CSV dosyasını **Içeri aktarabilirsiniz** . < App*url*> <*uygulama adı*>, <*uygulama yayımcısı*> biçimini kullanın. Veya, kısıtlanmış uygulamalar listesini içeren mevcut bir listeyi aynı biçimde **dışarı aktarın** .

> [!IMPORTANT]
> Kısıtlı uygulama ayarlarını kullanan cihaz profillerinin, cihaz gruplarına değil Kullanıcı gruplarına atanması gerekir.

## <a name="browser"></a>Tarayıcı

- **Web tarayıcısı (yalnızca Samsung KNOX)** : **Block** varsayılan Web tarayıcısının cihazlarda kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazın varsayılan Web tarayıcısının kullanılmasına izin verebilir.
- **Otomatik doldurma (yalnızca Samsung KNOX)** : **Block** tarayıcının otomatik olarak metin doldurmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi otomatik doldurmaya izin verebilir.
- **Tanımlama bilgileri (yalnızca Samsung KNOX)** : cihazlarda web sitelerinden tanımlama bilgilerini nasıl işleyeceğinizi seçin. Seçenekleriniz şunlardır:
  - İzin ver
  - Tüm tanımlama bilgilerini engelle
  - Ziyaret edilen web sitelerinin tanımlama bilgilerine izin ver
  - Geçerli web sitesinin tanımlama bilgilerine izin ver
- **JavaScript (yalnızca Samsung KNOX)** : **blok** , JavaScript 'in tarayıcıda çalıştırılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu betiklerine izin verebilir.
- **Açılır pencereler (yalnızca Samsung KNOX)** : **blok** , Web tarayıcısında açılır pencereleri engellemek için açılır pencere engelleyicisini açar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi açılır pencerelere izin verebilir.

## <a name="allow-or-block-apps"></a>Uygulamalara izin verme veya uygulamaları engelleme

Samsung KNOX Standard cihazlarında belirli uygulamalara izin vermek, bunları engellemek veya gizlemek için bu ayarları kullanın. Gizli olan uygulamalar, kullanıcılar tarafından açılamaz veya çalıştırılmamalıdır.

Seçenekleriniz şunlardır:

- **Yüklenmesine izin verilen uygulamalar (yalnızca Samsung KNOX Standard)** : kullanıcıların yükleyebileceği uygulamaları ekleyin. Kullanıcılar listede olmayan uygulamaları yükleyemez.
- **Uygulamanın başlatılması engellenen uygulamalar (yalnızca Samsung KNOX Standard)** : kullanıcıların cihazlarından çalıştıramadıkları uygulamaları girin.
- **Kullanıcıdan gizlenen uygulamalar (yalnızca Samsung KNOX Standard)** : cihazlarda gizlenen uygulamaları girin. Kullanıcılar bu uygulamaları bulamaz veya çalıştıramıyor.

Her ayar için uygulamalarınızı ekleyin:

- **Paket adına göre uygulama ekleme**: uygulama adını ve uygulama paketinin adını girin. Birincil olarak iş kolu uygulamaları için kullanılır. 
- **URL 'ye göre uygulama ekleme**: uygulama adını ve Google Play deposuna URL 'sini girin.
- **Mağaza uygulaması ekleme**: Intune 'da yönettiğiniz mevcut uygulamalar listesinden bir uygulama seçin.

## <a name="cloud-and-storage"></a>Bulut ve Depolama

- **Google yedekleme (yalnızca Samsung KNOX)** : **blok** cihazların Google yedekleme 'ye eşitlenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Google Backup 'ı kullanmaya izin verebilir.
- **Google hesabı otomatik eşitlemesi (yalnızca Samsung KNOX)** : **blok** , cihazlarda Google hesabı otomatik eşitleme özelliğini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Google hesabı ayarlarının otomatik olarak eşitlenmesine izin verebilir.
- **Çıkarılabilir depolama birimi (yalnızca Samsung KNOX)** : **blok** cihazların çıkarılabilir depolama alanını kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazların SD kartı gibi çıkarılabilir depolama birimi kullanmasına izin verebilir.
- **Depolama kartlarında şifreleme (yalnızca Samsung KNOX)** : **gerektir** , depolama kartlarının şifrelenmesini zorunlu tutar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi şifrelenmemiş depolama kartlarının kullanılmasına izin verebilir. Tüm cihazlar depolama kartı şifrelemesini desteklemez. Doğrulamak için cihaz üreticisine danışın.

## <a name="cellular-and-connectivity"></a>Hücresel ve Bağlantı

- **Veri dolaşımı (yalnızca Samsung KNOX)** : **blok** , hücresel ağ üzerinde veri dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi veri dolaşımına izin verebilir.
- **SMS/MMS Mesajlaşma (yalnızca Samsung KNOX)** : **blok** cihazlarda metin mesajlaşma yapılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi SMS ve MMS Mesajlaşma kullanımına izin verebilir.
- **Sesli arama (yalnızca Samsung KNOX)** : **Block** , kullanıcıların cihazlarda sesli arama özelliğini kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi sesli aramaya izin verebilir.
- **Ses dolaşımı (yalnızca Samsung KNOX)** : **blok** , hücresel ağ üzerinde ses dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi sesli dolaşıma izin verebilir.
- **Bluetooth (yalnızca Samsung KNOX)** : **blok** cihazlarda Bluetooth kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Bluetooth kullanmaya izin verebilir.
- **NFC (yalnızca Samsung KNOX)** : **blok** , kendisini destekleyen cihazlarda yakın alan iletişimi (NFC) kullanan işlemleri devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi NFC işlemlerine izin verebilir.
- **Wi-Fi (yalnızca Samsung KNOX)** : **blok** , cihazlarda Wi-Fi kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Wi-Fi kullanılmasına izin verebilir.
- **Wi-Fi internet paylaşımı (yalnızca Samsung KNOX)** : **blok** , cihazlarda Wi-Fi internet paylaşımı kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Wi-Fi internet paylaşımı kullanımına izin verebilir.

## <a name="kiosk"></a>Bilgi noktası

Bilgi noktası ayarları yalnızca Samsung Knox Standard cihazlarda ve Intune ile yönettiğiniz uygulamalarda geçerlidir.

- Cihaz bilgi noktası modundayken çalıştırmak istediğiniz uygulamaları ekleyin. Bilgi noktası modunda, yalnızca eklediğiniz uygulamalar çalışır; eklenmemiş uygulamalar çalışmaz. Cihaz bilgi noktası modunda olduğunda, önceden yüklenmiş tarayıcılar uygulama olarak çalışmaz. Bir tarayıcı gerekliyse [Managed Browser](../apps/app-configuration-managed-browser.md) kullanabilirsiniz.

  Uygulama seçenekleriniz:

  - **Paket adına göre uygulama ekleme**: öncelikle iş kolu uygulamaları için kullanılır. Uygulamanın ve uygulama paketinin adını girin.
  - **URL 'ye göre uygulama ekleme**: uygulama adını ve Google Play deposuna URL 'sini girin.
  - **Mağaza uygulaması ekleme**: Intune 'da yönettiğiniz mevcut uygulamalar listesinden bir uygulama seçin.

- **Ekran uyku düğmesi**: **blok** ekran uyku düğmesini engeller veya gizler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda ekran uyku modundan çıkma düğmesine izin verebilir.
- **Ses düğmeleri**: **blok** kullanıcıların ses düğmelerini devre dışı bırakarak birimi değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazlarda ses düğmelerinin kullanılmasına izin verebilir.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

Ayrıca, [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) ve [Windows 10](kiosk-settings.md) cihazları için bilgi noktası profilleri oluşturabilirsiniz.
