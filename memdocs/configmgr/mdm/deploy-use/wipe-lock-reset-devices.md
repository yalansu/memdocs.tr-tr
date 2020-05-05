---
title: Şirket içi MDM ile cihazları yönetme
titleSuffix: Configuration Manager
description: Şirket içi mobil cihaz yönetimi (MDM) Configuration Manager kullanarak tam Temizleme, seçmeli Temizleme, uzaktan kilitleme veya parola sıfırlama ile cihaz verilerini koruyun.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721874"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>Configuration Manager Şirket içi MDM ile cihazları yönetin ve verileri koruyun

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Mobil cihazlar hassas verileri saklayabilir ve birçok kuruluş kaynağına kolay erişim sağlayabilir. Cihazların ve verilerin korunmasına yardımcı olmak için aşağıdaki cihaz yönetim eylemleri için Configuration Manager kullanın:

- **Tam temizleme**: cihazı fabrika ayarlarına geri yükleme

- **Seçmeli Temizleme**: yalnızca kurumsal verileri Kaldır

- **Geçiş kodu sıfırlama**: Kullanıcı bunu unutursa geçiş kodunu kaldırın veya sıfırlayın

- **Uzaktan kilitleme**: kaybolmuş olabilecek bir cihazın güvenliğinin sağlanmasına yardımcı olma

## <a name="full-wipe"></a>Tam temizleme  

Kayıp bir cihazı güvenli hale getirmeniz gerektiğinde veya bir cihazı etkin kullanımdan devre dışı bırakadığınızda, üzerinde tam silme işlemi başlatabilirsiniz. Bu eylem, cihazı fabrika varsayılan ayarlarına geri yükler. Tüm kuruluş ve Kullanıcı verilerini ve ayarlarını kaldırır.

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. Ayrıca **Cihaz Koleksiyonları** ' nı seçebilir ve cihazın üye olduğu bir koleksiyon seçebilirsiniz.

1. Silmek istediğiniz cihazı seçin.

1. Şeritte, cihaz grubunda, **uzak cihaz eylemleri**' ni seçin ve ardından **devre dışı bırak/Sil**' i seçin.

1. **Configuration Manager devre dışı bırak** penceresinde, **mobil cihazı silme ve Configuration Manager kullanımdan**kaldırma seçeneğini belirleyin.

## <a name="selective-wipe"></a>Seçmeli temizleme

Yalnızca bir cihazdan kurumsal verileri kaldırmak için seçmeli silme başlatın.

### <a name="behaviors-by-os-version"></a>İşletim sistemi sürümüne göre davranışlar

Aşağıdaki tablolarda, seçmeli silme işleminden sonra, hangi verilerin kaldırıldığı ve cihazda kalan veriler üzerindeki etkisi açıklanır.

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10, Windows 8.1, Windows RT 8,1 ve Windows RT

|İçerik|Seçmeli silme davranışı|  
|-------|--------|
|Configuration Manager tarafından yüklenen uygulamalar ve ilişkili veriler|Uygulamaları kaldırır ve tüm dışarıdan yükleme anahtarlarını kaldırır. Windows seçmeli silme kullanan uygulamalar için şifreleme anahtarını iptal eder ve verilere artık erişilemez.|
|VPN ve Wi-Fi profilleri|Profilleri kaldırır|
|Sertifikalar|Sertifikaları kaldırır ve iptal eder|
|Ayarlar|Gereksinimleri kaldırır|
|E-posta profilleri|Windows e-posta ve ekleri için posta uygulamasını da içeren EFS özellikli e-postayı kaldırır.|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 Mobile, Windows Phone 8,0 ve Windows Phone 8,1

|İçerik|Seçmeli silme davranışı|  
|-------|--------|
|Configuration Manager tarafından yüklenen Şirket uygulamaları ve ilişkili veriler|Uygulamaları kaldırır ve kurumsal uygulama verilerini kaldırır.|
|VPN ve Wi-Fi profilleri|Windows 10 Mobile ve 8,1 Windows Phone için profilleri kaldırır|
|Sertifikalar|Windows Phone 8,1 için sertifikaları kaldırır|
|E-posta profilleri|Profilleri kaldırır (Windows Phone 8,0 dışında)|

Aşağıdaki ayarlar da Windows 10 Mobile ve Windows Phone 8,1 cihazlarından kaldırılmıştır:  

- **Mobil cihazların kilidini açmak için bir parola gerektir**  
- **Basit parolalara izin ver**  
- **Minimum parola uzunluğu**  
- **Gerekli parola türü**
- **Parola geçerlilik süresi (gün)**  
- **Parola geçmişini anımsa**  
- **Cihaz silinmeden önce izin verilen yinelenen oturum açma hatası sayısı**  
- **Parola gerekmeden önce etkin olmama süresi (dakika)**  
- **Gerekli parola türü – minimum karakter kümesi sayısı**  
- **Kameraya izin ver**
- **Cihazda şifrelemeyi gerektir**  
- **Çıkarılabilir depolama birimine izin ver**  
- **Web tarayıcısına izin ver**  
- **Uygulama depolamaya izin ver**  
- **Ekran yakalamaya izin ver**  
- **Coğrafi konuma izin ver**  
- **Microsoft Hesabına izin ver**  
- **Kopyalama ve yapıştırmaya izin ver**  
- **Wi-Fi İnternet paylaşımına izin ver**  
- **Ücretsiz Wi-Fi etkin noktalarına otomatik olarak bağlanmaya izin ver**  
- **Wi-Fi etkin noktası bildirimine izin ver**  
- **Fabrika sıfırlamasına izin ver**
- **Bluetooth'a izin ver**  
- **NFC'ye izin ver**
- **Wi-Fi'a izin ver**

### <a name="start-a-selective-wipe"></a>Seçmeli silme Başlat

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. Ayrıca **Cihaz Koleksiyonları** ' nı seçebilir ve cihazın üye olduğu bir koleksiyon seçebilirsiniz.

1. Silmek istediğiniz cihazı seçin.

1. Şeritte, cihaz grubunda, **uzak cihaz eylemleri**' ni seçin ve ardından **devre dışı bırak/Sil**' i seçin.

1. **Configuration Manager devre dışı bırak** penceresinde, şu seçeneği belirleyin: **Şirket içeriğini Sil ve mobil cihazı Configuration Manager devre dışı bırak**.

### <a name="recommendations-for-selective-wipe"></a>Seçmeli Temizleme için öneriler

- E-postanın başarıyla temizlenmesi için e-posta profillerini Windows Phone 8,1 cihazlarına ayarlayın.

- Uygulamaların başarıyla temizlenmesi için, uygulamaların mobil cihaz uygulama yönetimi üzerinden dağıtıldığından emin olun.

## <a name="passcode-reset"></a>Geçiş kodu sıfırlama

Bir kullanıcı geçiş kodunu unutursa, cihazda yeni bir geçici geçiş kodu zorlamak için bu eylemi kullanın. Geçiş kodunu tamamen de kaldırabilirsiniz. Aşağıdaki tabloda, farklı mobil platformlarda parola sıfırlama işleminin nasıl çalıştığı listelenmiştir.

| İşletim sistemi sürümü | Geçiş kodu sıfırlama |
|------------|----------------|
| Windows 10 | Desteklenmiyor |
| Windows 10 mobile | Desteklenen, Azure Active Directory katılmış cihazlar hariç |
| Windows Phone 8 ve Windows Phone 8.1 | Destekleniyor |
| Windows RT 8.1 | Desteklenmiyor |
| Windows 8.1 | Desteklenmiyor |

> [!Note]
> Üst düzey siteden geçiş kodu sıfırlama eylemini başlatın. Örneğin, bir merkezi yönetim sitesi kullanıyorsanız, bu eylemi yalnızca bu sitede gerçekleştirebilirsiniz. Tek başına bir birincil site kullanıyorsanız, bu eylemi yalnızca ilgili siteden yapabilirsiniz.

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>Bir mobil cihazda geçiş kodunu uzaktan sıfırlama

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. Ayrıca **Cihaz Koleksiyonları** ' nı seçebilir ve cihazın üye olduğu bir koleksiyon seçebilirsiniz.

1. Geçiş kodunun sıfırlanacağı cihaz veya cihazları seçin.

1. Şeritte, cihaz grubunda, **uzak cihaz eylemleri**' ni seçin ve ardından **geçiş kodu sıfırlama**' yı seçin.  

### <a name="show-the-state-of-the-passcode-reset"></a>Geçiş kodu sıfırlama durumunu göster  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. Ayrıca **Cihaz Koleksiyonları** ' nı seçebilir ve cihazın üye olduğu bir koleksiyon seçebilirsiniz.

1. Geçiş kodu sıfırlama durumunun gösterileceği cihaz veya cihazları seçin.

1. Şeritte, cihaz grubunda, **uzak cihaz eylemleri**' ni seçin ve ardından **geçiş kodu durumunu göster**' i seçin.  

## <a name="remote-lock"></a>Uzaktan kilitleme

Bir kullanıcı cihazını kaybederse, cihazı uzaktan kilitleyebilmeniz gerekir. Aşağıdaki tabloda, farklı mobil platformlarda uzaktan kilitleme işleminin nasıl çalıştığı listelenmiştir.  

|İşletim sistemi sürümü|Uzaktan kilitleme|
|----------|-----------|
|Windows 10|Desteklenmiyor|
|Windows Phone 8 ve Windows Phone 8.1|Destekleniyor|
|Windows RT 8.1|Cihazın geçerli kullanıcısı, cihazı kaydeden Kullanıcı ile aynıysa desteklenir.|
|Windows 8.1|Cihazın geçerli kullanıcısı, cihazı kaydeden Kullanıcı ile aynıysa desteklenir.|

> [!Note]
> Üst düzey siteden uzaktan kilitleme eylemini başlatın. Örneğin, bir merkezi yönetim sitesi kullanıyorsanız, bu eylemi yalnızca bu sitede gerçekleştirebilirsiniz. Tek başına bir birincil site kullanıyorsanız, bu siteden eylemi yapın.

### <a name="remotely-lock-a-mobile-device"></a>Bir mobil cihazı uzaktan kilitleme

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. Ayrıca **Cihaz Koleksiyonları** ' nı seçebilir ve cihazın üye olduğu bir koleksiyon seçebilirsiniz.

1. Kilitlenecek cihaz veya cihazları seçin.

1. Şeritte, cihaz grubunda, **uzak cihaz eylemleri**' ni seçin ve ardından **Uzaktan kilitleme**' ı seçin. Eylemi onaylayın.

### <a name="show-the-state-of-the-remote-lock"></a>Uzaktan kilitleme durumunu göster

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. Ayrıca **Cihaz Koleksiyonları** ' nı seçebilir ve cihazın üye olduğu bir koleksiyon seçebilirsiniz.

1. Uzaktan kilitleme durumunun gösterileceği cihazı seçin.

1. Şeritte, cihaz grubunda, **uzak cihaz eylemleri**' ni seçin ve ardından **Uzaktan kilitleme durumunu göster**' i seçin.
