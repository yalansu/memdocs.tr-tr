---
title: Windows Phone 8.1 için Microsoft Intune cihaz kısıtlama ayarları
titleSuffix: ''
description: Windows Phone 8.1 çalıştıran cihazlarda cihaz ayarlarını ve işlevselliğini denetlemek için kullanabileceğiniz Intune ayarlarını öğrenin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24fd2085839df35a486fcfa4cf817944b0d19944
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556260"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Microsoft Intune Windows Phone 8.1 cihaz kısıtlama ayarları

Bu makalede, Windows Phone 8.1 çalıştıran cihazlar için yapılandırabileceğiniz Microsoft Intune cihaz kısıtlama ayarları gösterilir.

## <a name="before-you-begin"></a>Başlamadan önce

[Windows Phone 8,1 cihaz kısıtlamaları profili oluşturun](device-restrictions-configure.md).

## <a name="general"></a>Genel

- **Kamera**: **blok** cihaz kamerasına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Intune yalnızca cihaz kamerasına erişimi yönetir. Resimlere veya videolara erişimi yoktur.

- **Kopyala ve Yapıştır**: **blok** , cihazdaki uygulamalar arasında kopyalama ve yapıştırmayı önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Çıkarılabilir depolama**: **blok** , cihazlarda SD kartlar gibi dış depolama cihazlarının kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Coğrafi konum**: **blok** cihazlarda konum hizmetlerini açmayı önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Microsoft hesabı**: **Block** , kullanıcıların bir Microsoft hesabı cihazla ilişkilendirilmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Ekran yakalama**: **blok** , cihazlarda ekran görüntülerinin alınmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Tanılama veri gönderimi**: **blok** cihazların Microsoft 'a tanılama ve kullanım telemetri verileri göndermesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Özel e-posta hesapları eşitleme**: **blok** cihazların Microsoft olmayan e-posta hesaplarına bağlanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="password"></a>Parola

- **Parola**: kullanıcıların cihazlara erişmek için parola **girmesini zorunlu kılar** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Yalnızca yerel hesaplar için geçerlidir. Etki alanı hesabı parolaları Active Directory (AD) ve Azure AD tarafından yapılandırılmış olarak kalır.
  - **Gerekli parola türü**: parola türünü seçin. Seçenekleriniz şunlardır:
    - **Cihaz varsayılanı**: parola rakam ve harf içerebilir.
    - **Alfasayısal**: parola sayıların ve harflerin karışımı olmalıdır.
    - **Sayısal**: parola yalnızca sayı olmalıdır.
  - **Minimum parola uzunluğu**: 4-16 adresinden gereken en az karakter sayısını girin. Örneğin, `6` parola uzunluğunun en az altı karakter gerektirmek için girin.
  - **Basit parolalar**: **blok** , kullanıcıların veya gibi basit parolalar oluşturmasını engeller `1234` `1111` . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: cihazlar temizlenmeden önce izin verilen hatalı parola sayısını girin.
  - **Ekran kilitlenmeden önce geçen işlem yapılmayan dakika sayısı**: ekran otomatik olarak kilitlenmeden önce cihazın boşta kalması gereken süreyi girin. Örneğin, `5` 5 dakika çalıştıktan sonra cihazları kilitlemek için yazın. **Yapılandırılmadı** veya boş ol olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Parola kullanım süresi (gün)**: cihaz parolasının değiştirilme tarihi olan 1-255 ' dan gün cinsinden süre uzunluğunu girin. Örneğin, `90` 90 gün sonra parolanın süresini dolacak şekilde girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Önceki parolaların yeniden kullanılmasını engelle**: daha önce kullanılan ve 1-24 'den kullanılamayan parolaların sayısını girin. Örneğin, `5` kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Şifreleme**: dosyalar dahil olmak üzere cihazda şifreleme **gerektir** . Tüm cihazlar şifrelemeyi desteklemez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Bu ayarı yapılandırmak ve uyumluluğu doğru şekilde raporlamak için aşağıdakileri de yapılandırın:
  - **Parola gerektir**: **gerektir**olarak ayarlayın.
  - **Gerekli parola türü**: en az **sayısal**olarak ayarlanır.
  - **Minimum parola uzunluğu**: en az olarak ayarlanır `4` .

## <a name="app-store"></a>App Store

- **App Store**: **Block** , kullanıcıların uygulama deposuna erişmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="restricted-apps"></a>Kısıtlı uygulamalar

Kısıtlı uygulamalar listesinde, aşağıdaki listelerden birini yapılandırabilirsiniz:

- **Engellenen uygulamalar**: Kullanıcıların yüklemesine ve çalıştırmasına izin verilmeyen uygulamaları (Intune tarafından yönetilmeyen) listeleyin.
- **Izin verilen uygulamalar**: Kullanıcıların yüklemesine izin verilen uygulamaları listeleyin. Intune tarafından yönetilen uygulamalara otomatik olarak izin verilir.

Listeyi yapılandırmak için **Ekle**’ye tıklayın, sonra da tercih ettiğiniz bir ad (isteğe bağlı olarak uygulama yayımcısı) ve uygulamanın uygulama mağazasındaki URL'sini belirtin.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Mağazadaki uygulamanın URL’sini belirtme

İzin verilen veya engellenen uygulamalar listesinde bir uygulama URL'si belirtmek için aşağıdaki biçimi kullanın:

[Windows Phone Mağazası](https://www.microsoft.com/store/apps/windows-phone) sayfasında, kullanmak istediğiniz uygulamayı arayın.

Uygulamanın sayfasını açın ve URL 'YI panoya kopyalayın. Artık bu URL 'YI izin verilen veya engellenen uygulamalar listesinde URL olarak kullanabilirsiniz.

Örnek: Mağazada Skype uygulamasını arayın. Kullandığınız URL `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51` olacaktır.

### <a name="additional-options"></a>Ek seçenekler

Ayrıca, **Içeri aktar** ' a tıklayarak listeyi <*uygulama URL 'si*>, uygulama *adı*> <uygulama *yayımcısı* <veya aynı biçimde kısıtlanmış uygulamalar listesinin Içeriğini içeren bir CSV dosyası oluşturmak için **dışarı aktar** ' a tıklayabilirsiniz.

## <a name="browser"></a>Tarayıcı

- **Web tarayıcısı**: **Engelle** , cihazlarda yerleşik web tarayıcısını kapatır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="cellular-and-connectivity"></a>Hücresel ve Bağlantı

- **Wi-Fi**: **Block** cihazlarda Wi-Fi işlevini devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Wi-Fi internet paylaşımı**: **blok** , cihazlarda Wi-Fi internet paylaşımı kullanımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Wi-Fi etkin noktalarına otomatik olarak bağlan**: cihazların ücretsiz Wi-Fi etkin noktalarına otomatik olarak bağlanmasına ve tüm kullanım koşullarını otomatik olarak kabul etmesine olanak sağlar.
- **Wi-Fi etkin nokta raporlama**: **blok** cihazların Wi-Fi etkin nokta bağlantı bilgilerini göndermesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **NFC**: **Block** , kendisini destekleyen cihazlarda yakın alan iletişimi (NFC) kullanan işlemleri devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Bluetooth**: **blok** kullanıcıların Bluetooth 'u etkinleştirmelerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="next-steps"></a>Sonraki adımlar

Cihaz kısıtlamaları profiline genel bir bakış için, bkz. [Microsoft Intune cihaz kısıtlama ayarlarını yapılandırma](device-restrictions-configure.md).
