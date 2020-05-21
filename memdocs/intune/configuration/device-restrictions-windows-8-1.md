---
title: Microsoft Intune-Azure 'da cihaz kısıtlama ayarlarını Windows 8.1 | Microsoft Docs
titleSuffix: ''
description: Windows 8.1 çalıştıran cihazlarda cihaz ayarlarını ve işlevselliğini denetlemek için kullanabileceğiniz Intune ayarlarını öğrenin.
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
ms.openlocfilehash: 36a74e503f15fe982eeaf1addfed40d0c599cb2c
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556243"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Microsoft Intune Windows 8.1 cihaz kısıtlama ayarları

Bu makalede, Windows 8.1 çalıştıran cihazlar için yapılandırabileceğiniz cihaz kısıtlama ayarları Microsoft Intune gösterilmektedir.

## <a name="before-you-begin"></a>Başlamadan önce

[Windows 8.1 cihaz kısıtlamaları yapılandırma profili oluşturun](device-restrictions-configure.md#create-the-profile).

## <a name="general"></a>Genel

- **Kullanım verilerini paylaşma**: **blok** cihazların Microsoft 'a tanılama ve kullanım telemetri bilgilerini göndermesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Güvenlik duvarı**: Windows güvenlik duvarının açık olmasını **gerekli kılın** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Kullanıcı hesabı denetimi**: Kullanıcı hesabı denetimi 'NI (UAC) yapılandırır. Kullanıcıların cihazlarda değişiklikler hakkında nasıl bildirim alınacağını seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Her zaman bildir**
  - **Uygulama değişikliklerinde bildir**
  - **Uygulama değişikliklerini bilgilendir, ancak masaüstünü karartma**
  - **Hiçbir şekilde bildirme**

## <a name="password"></a>Parola

- **Gerekli parola türü**: kullanıcının cihaza erişmek için bir parola girmesi gerekiyorsa seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Alfasayısal**: parola sayıların ve harflerin karışımı olmalıdır.
  - **Sayısal**: parola yalnızca sayı olmalıdır.
- **Minimum parola uzunluğu**: 6-16 adresinden gereken en az karakter sayısını girin. Örneğin, `6` parola uzunluğu için en az altı sayı veya karakter gerektirmek için girin.
- **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: cihaz temizlenmeden önce izin verilen hatalı parola sayısını 1-14 adresinden girin.
- **Ekran kilitlenene kadar en fazla işlem yapılmayan dakika sayısı (dakika cinsinden)**: ekran otomatik olarak kilitlenmeden önce, 1-60 dakikadan itibaren bir cihazın boşta kalması gereken süreyi girin. Örneğin, `5 Minutes` 5 dakika boşta kaldıktan sonra cihazı kilitlemek için yazın. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Parola kullanım süresi (gün)**: cihaz parolasının değiştirilme tarihi olan 1-255 ' dan gün cinsinden süre uzunluğunu girin. Örneğin, `90` 90 gün sonra parolanın süresini dolacak şekilde girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Önceki parolaların yeniden kullanılmasını engelle**: daha önce kullanılan ve 1-24 'den kullanılamayan parolaların sayısını girin. Örneğin, `5` kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Resimli parola ve PIN**: bir resimli parola, kullanıcının bir resimdeki hareketlerle oturum açmasını sağlar. PIN, kullanıcıların dört basamaklı bir kodla hızla oturum açmalarına olanak tanır.

  **Blok** , parola olarak bir resım veya PIN kullanılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Şifreleme**: dosyalar dahil olmak üzere cihazlarda şifreleme **gerektir** . Tüm cihazlar şifrelemeyi desteklemez. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Bu ayarı yapılandırmak ve uyumluluğu doğru şekilde raporlamak için aşağıdakileri de yapılandırın:

  - **Gerekli parola türü**: en az **sayısal**olarak ayarlanır.
  - **Minimum parola uzunluğu**: en az olarak ayarlanır `6` .

  Windows 8.1 çalıştıran cihazlarda şifrelemeyi zorlamak için her bir cihaza [Windows için Aralık 2014 MDM istemci güncelleştirmesi](https://support.microsoft.com/kb/3013816) ’ni yüklemeniz gerekir.

  Windows 8.1 cihazları için bu ayarı etkinleştirirseniz, cihazın tüm kullanıcılarının bir Microsoft hesabı olmalıdır.

  Şifrelemenin çalışması için cihazların [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97) donanım sertifika gereksinimlerini karşılaması gerekir.

  Cihazda şifrelemeyi zorunlu tuttuğunuzda kurtarma anahtarına yalnızca kullanıcıların OneDrive hesabından eriştikleri Microsoft hesabından erişilebilir. Bir kullanıcı için bu anahtarı kurtaramazsınız.

## <a name="browser"></a>Tarayıcı

- **Otomatik Doldur**: **Engelle** , kullanıcıların tarayıcıdaki otomatik tamamlama ayarlarını değiştirmelerini ve form alanlarını otomatik olarak doldurmalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi otomatik doldurmaya izin verebilir.
- **Sahtekarlık uyarıları**: **gerektir** , olası sahte web siteleri için tarayıcıda sahtekarlık uyarılarını gösterir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Microsoft Edge Için SmartScreen**: **Block** , Microsoft Defender SmartScreen 'i kapatır. SmartScreen, sitelere ve dosya indirmelerine erişirken potansiyel kimlik avı dolandırıcılığı ve kötü amaçlı yazılım arar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi SmartScreen 'i açabilir.
- **JavaScript 'e Izin ver**: **Block** JavaScript gibi betiklerin tarayıcıda çalıştırılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi JavaScript 'e izin verebilir.
- **Açılır**pencereler: **blok** açılır pencere engelleyicisini açar ve Web tarayıcısında açılır pencereleri önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Do-Not-Track üstbilgileri**: **Block** cihazların izleme bilgilerini isteyen web sitelerine, izleme üst bilgileri göndermesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Eklentiler**: **Block** , kullanıcıların Internet Explorer 'da eklentiler eklemesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **İntranet sitesinde tek sözcüklü giriş**: tek sözcüklü giriş, kullanıcıların, veya gibi tek bir kelime girerek intranet sitesine gitmesini sağlar `hr` `benefits` . **Engelle** ayarı bu özelliği önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Intranet sitesini otomatik algıla**: **blok** tarayıcının intranet sitelerini otomatik olarak algılamasını önler. Intranet eşleme kuralları engellenir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **İnternet güvenlik düzeyi**: internet siteleri için güvenlik düzeyini ayarlar. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Geniş**
  - **Orta yüksek**
  - **Medium**
- **İntranet güvenlik düzeyi**: intranet siteleri için güvenlik düzeyini ayarlar. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Düşük**
  - **Orta-düşük**
  - **Medium**
  - **Orta yüksek**
  - **Geniş**
- **Güvenilen siteler güvenlik düzeyi**: güvenilen siteler bölgesi için güvenlik düzeyini yapılandırır. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Düşük**
  - **Orta-düşük**
  - **Medium**
  - **Orta yüksek**
  - **Geniş**
- **Kısıtlanmış siteler Için yüksek güvenlik**: Yasak siteler bölgesi için güvenlik düzeyini yapılandırır. **Yapılandırılmış** , kısıtlı siteler için yüksek güvenliği zorlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Kurumsal mod menü erişimi**: **blok** kullanıcıların Internet Explorer 'da Kurumsal mod menü seçeneklerine erişmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  **Yapılandırılmadı**olarak ayarlandığında, şunu da girin:

  - **Günlük raporu konum URL 'si**: Kurumsal mod erişimi açık olan Web sitelerini gösteren RAPORLARıN alınacağı URL konumunu girin.

- **Kuruluş modu Site listesi konumu (yalnızca masaüstü)**: Kurumsal modda açılabilen Web sitelerinin listesinin konumunu girin.

## <a name="cellular"></a>Hücresel

- **Veri dolaşımı**: **engelleme** , cihazlar hücresel ağ üzerindeyken veri dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="cloud-and-storage"></a>Bulut ve Depolama

- **Çalışma klasörleri URL 'si**: belgelerin cihazlar arasında eşitlenmesine izin vermek için iş klasörünün URL 'sini girin. **Yapılandırılmadı** (varsayılan) veya boş ol olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Microsoft hesabı olmadan Windows Mail uygulamasına erişim**: **Block** , Microsoft hesabı olmadan Windows Mail uygulamasına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="next-steps"></a>Sonraki adımlar

[Windows 10 ve daha yeni](device-restrictions-windows-10.md)bir cihaz kısıtlamaları profili oluşturun.
