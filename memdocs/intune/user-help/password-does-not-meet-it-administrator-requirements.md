---
title: Intune 'a kayıtlı cihazlar için parola gereksinimleri | Microsoft Docs
description: Bu makalede, ağınıza erişebilmek için kuruluşunuzun parola gereksinimlerini nasıl karşılamanız açıklanmaktadır.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: efb3c261-1f6c-4d39-bfa4-18661f8c59c7
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: b9bdada31e280c7fdc8a5d7a5a0a4a7ab7d36ae3
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057296"
---
# <a name="device-password-requirements"></a>Cihaz parolası gereksinimleri  

Cihazınızın parolası kuruluşunuzun güvenlik gereksinimlerini karşılamıyorsa Şirket Portalı bir ileti alırsınız. Sizi ve kuruluşunuzun verilerini yetkisiz erişimden korumak için parola gereksinimleri yerinde konur. Daha güvenli bir parola oluşturana kadar, kuruluşunuzun ağına erişiminizi engellemiş olabilirsiniz.  

Şirket Portalı, her parola gereksinimi için bir ileti gönderir, bu nedenle aynı anda birden fazla ileti alabilirsiniz. Daha fazla ayrıntı görmek için herhangi bir iletiye dokunun (sağlanmışsa).  

Bu makalede, aldığınız parolayla ilgili tüm iletiler listelenmekte ve işletim sistemi platformuna göre her gereksinimle ilgili ek ayrıntılar sağlanmaktadır.     

## <a name="change-password-passcode-pin"></a>Parola değiştirme, geçiş kodu, PIN  

Genellikle, parola ayarlarına erişmek için, Ayarlar uygulamasını cihazınızda açabilir ve *kilit ekranı* veya *güvenlik ayarları*için arama yapabilirsiniz.  

Aşağıdaki makalelerde, işletim sistemi platformunda cihaz parolasının nasıl güncelleştirilmesi anlatılmaktadır. Belirli cihazınıza yönelik en güncel yönergeleri almak için, cihaz üreticisinin yardım belgelerine bakın.  

- [Windows 10 cihaz parolasını ayarla](set-or-change-your-password-windows.md)  
- [İOS cihaz geçiş kodunu ayarla](set-or-change-your-passcode-ios.md)  
- [Android cihaz PIN 'ini veya parolasını ayarlama](set-your-pin-or-password-android.md)  


> [!IMPORTANT]
> Parolanızı gereksinimlerini karşılayacak şekilde değiştirdiyseniz ancak hala bildirimler alıyorsanız, cihazınızı yeniden başlatın.  

Kuruluşunuzun parola gereksinimleriyle ilgili belirli sorular için BT destek sorumlunuza başvurun.  

## <a name="windows-10-password-requirements"></a>Windows 10 parola gereksinimleri

| İleti | Nasıl düzeltilir |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Parola gereklidir. | Parola ayarlayın. Kuruluşunuz cihazınızın kilidini açmak için bir parola girmenizi gerektiriyor. |
| Parola çok basit. |  Parolanızın 1234 veya 1111 gibi sıralı veya yinelenen numaralar içermediğinden emin olun. |
| Parola çok kısa.| Daha fazla karakter içeren bir parola güncelleştirin veya ayarlayın. Kuruluşunuz parolanızın belirli bir uzunlukta olmasını gerektirir. Gerçekte seçtikleri Özellikler farklılık gösterir, ancak ihtiyaç duydukları en düşük uzunluk 4 karakterdir ve üst sınır 16 ' dır. |
| Parola yalnızca sayı içermelidir. | Yalnızca sayı içeren bir parola ayarlayın.|
| Parola yalnızca alfasayısal karakterlerden oluşmalıdır. | Sayıların ve harflerin karışımını içeren bir parola ayarlayın.|
| Parola karmaşık karakterler içermelidir. | Sayılar, büyük harfler ve, ve gibi semboller gibi karmaşık karakterler ekleyin `$` `%` `#` . Kuruluşunuz, diğerlerinin parolayı tahmin etmelerini zorlaştırmak için harf, sayı ve alfasayısal olmayan karakterlerin bir karışımını gerektirir.|  
| Parolanın süresi doldu. | Yeni bir parola ayarlayın. Kuruluşunuz, parolanızın belirli bir süre geçtikten sonra değiştirilmesini gerektirir. |
| Parolanız çok kısa süre önce kullanıldı. | Daha önce kullanılmayan bir parola seçin. Bir parolayı yeniden kullanmadan önce kuruluşunuz belirli bir süre geçiş yapılmasını gerektirir. |

## <a name="ios-passcode-requirements"></a>iOS geçiş kodu gereksinimleri

| İleti | Nasıl düzeltilir |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Geçiş kodu gerekiyor.| Bir geçiş kodu ayarlayın. Kuruluşunuz, cihazınızın kilidini açmak için bir geçiş kodu girmenizi gerektiriyor. |
| Geçiş kodu çok basit. |  Geçiş kodu, 1234 veya 1111 gibi sıralı veya yinelenen sayılar içermediğinden emin olun. |
| Geçiş kodu çok kısa. | Bir geçiş kodunu daha fazla karakterle güncelleştirin veya ayarlayın. Kuruluşunuz, geçiş kodunun belirli bir uzunlukta olmasını gerektiriyor. Gerçekte seçtikleri Özellikler farklılık gösterir, ancak ihtiyaç duydukları en düşük uzunluk 4 karakterdir ve üst sınır 14 ' tür. Geçiş kodunuzu değiştirdiğinizde, Apple 'dan 6 veya daha fazla karakter girebileceğini söyleyen bir istem görürsünüz. Bu ileti yalnızca bir Apple sistem önerisi olur. Kuruluşunuz yalnızca 4 veya 5 karakterden oluşan bir geçiş kodu gerektiriyorsa, 6 basamaklı bir geçiş kodu girmeniz gerekmez.|  
| Geçiş kodu yalnızca sayı içermelidir. | Yalnızca sayı içeren bir geçiş kodu ayarlayın.|
| Geçiş kodu yalnızca alfasayısal karakterlerden oluşmalıdır.| Sayı ve harf karışımı içeren bir geçiş kodu ayarlayın.|
| Geçiş kodu, alfasayısal olmayan karakterler içermelidir. | ,,, Ve gibi özel karakterler ekleyin `&` `!` `$` `%` `#` . Kuruluşunuz, başkalarının geçiş kodunu tahmin etmelerini zorlaştırmak için harf, sayı ve alfasayısal olmayan karakterlerin bir karışımını gerektirir.|
| Geçiş kodunun süresi doldu. | Yeni bir parola ayarlayın. Kuruluşunuz, parolanızın belirli bir süre geçtikten sonra değiştirilmesini gerektirir. |
| Geçiş kodu çok kısa süre önce kullanıldı.| Daha önce kullanmadığınız bir geçiş kodu seçin. Bir geçiş kodunu yeniden kullanmadan önce kuruluşunuz belirli bir süre için geçiş yapılmasını gerektirir. |
|Dokunma KIMLIĞI veya yüz KIMLIĞI kimlik doğrulaması gerekiyor. | Touch ID veya yüz KIMLIĞI ayarlayın. Kuruluşunuz, parolalar veya kredi kartı bilgileri için otomatik doldurma kullanmadan önce bu yöntemlerden biriyle kimlik doğrulaması yapmanızı gerektirir. | 

## <a name="macos-password-requirements"></a>macOS parola gereksinimleri
| İleti | Nasıl düzeltilir |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Parola gereklidir. | Parola ayarlayın. Kuruluşunuz cihazınızın kilidini açmak için bir parola girmenizi gerektiriyor. |
| Parola çok basit.|  Parolanızın 1234 veya 1111 gibi sıralı veya yinelenen numaralar içermediğinden emin olun. |
| Parola çok kısa. | Daha fazla karakter içeren bir parola güncelleştirin veya ayarlayın. Kuruluşunuz parolanızın belirli bir uzunlukta olmasını gerektirir.|
| Parola yalnızca sayı içermelidir. | Yalnızca sayı içeren bir parola ayarlayın.|
| Parola yalnızca alfasayısal karakterlerden oluşmalıdır. | Sayıların ve harflerin karışımını içeren bir parola ayarlayın.|
| Parola, alfasayısal olmayan karakterler içermelidir. | ,,, Ve gibi özel karakterler ekleyin `&` `!` `$` `%` `#` . Kuruluşunuz, diğerlerinin parolayı tahmin etmelerini zorlaştırmak için harf, sayı ve alfasayısal olmayan karakterlerin bir karışımını gerektirir.|
| Parolanın süresi doldu. | Yeni bir parola ayarlayın. Kuruluşunuz, parolanızın belirli bir süre geçtikten sonra değiştirilmesini gerektirir. |
| Parolanız çok kısa süre önce kullanıldı. | Daha önce kullanılmayan bir parola seçin. Bir parolayı yeniden kullanmadan önce kuruluşunuz belirli bir süre geçiş yapılmasını gerektirir. |

## <a name="android-password-requirements"></a>Android parola gereksinimleri
| İleti | Nasıl düzeltilir |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Parola gereklidir. | Bir parola veya PIN ayarlayın. Kuruluşunuz cihazınızın kilidini açmak için bir parola girmenizi gerektiriyor. |
| Parola çok basit. |  Parolanızın veya PIN 'inizin 1234 veya 1111 gibi sıralı veya yinelenen numaralar içermediğinden emin olun. |
| Parola çok kısa. | Daha fazla karakter içeren bir parola güncelleştirin veya ayarlayın. Kuruluşunuz parolanızın belirli bir uzunlukta olmasını gerektirir.|
| Parola sayı içermelidir. | Sayı içeren bir parola veya PIN kodu ayarlayın.|
| Parola harf içermelidir. | Alfabeden harfler içeren bir parola ayarlayın.|
| Parola alfasayısal karakterlerden oluşmalıdır. | Sayıların ve harflerin karışımını içeren bir parola ayarlayın.|
| Parola alfasayısal karakterler ve semboller içermelidir. | ,,, Ve gibi harflerin, sayıların ve özel karakterlerin bir karışımını içeren bir parola ayarlayın `&` `!` `$` `%` `#` . |
| Parola, biyometrik teknolojiyi kullanmalıdır.| Cihazınızı parmak izi veya yüz tanıma gibi biyometrik kimlik doğrulaması kullanacak şekilde ayarlayın.
| Parolanın süresi doldu. | Yeni bir parola ayarlayın. Kuruluşunuz, parolanızın belirli bir süre geçtikten sonra değiştirilmesini gerektirir. |
| Parolanız çok kısa süre önce kullanıldı. | Daha önce kullanılmayan bir parola seçin. Bir parolayı yeniden kullanmadan önce kuruluşunuz belirli bir süre geçiş yapılmasını gerektirir. |

## <a name="next-steps"></a>Sonraki adımlar
Parolanızı güncelleştirdikten sonra parolayla ilgili iletiler almaya devam ederseniz cihazınızı yeniden başlatmayı deneyin. 

Bu bilgiler yardımcı olmadı mı? BT destek sorumlunuza başvurun. Kişi bilgileri için [Şirket Portalı Web sitesine](https://go.microsoft.com/fwlink/?linkid=2010980) bakın.  


