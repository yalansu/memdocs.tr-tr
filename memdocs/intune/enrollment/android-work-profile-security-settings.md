---
title: Android Enterprise güvenlik yapılandırma altyapısı
titleSuffix: Microsoft Intune
description: Android kurumsal cihaz temel ve yüksek güvenlik için önerilen kısıtlamaları ve ayarları öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05d0cb3db60ed0f54a66bc4128e5528e789537a8
ms.sourcegitcommit: d647eefa23c8849f49584442df568284d51d7525
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86195710"
---
# <a name="android-enterprise-work-profile-security-configurations"></a>Android kurumsal iş profili güvenlik yapılandırması

[Android Enterprise Security Configuration Framework](android-configuration-framework.md)'ün bir parçası olarak, Android Enterprise iş profili mobil kullanıcıları için aşağıdaki ayarları uygulayın. Her ilke ayarı hakkında daha fazla bilgi için bkz. Intune ve [Android kurumsal cihaz ayarlarını](../configuration/device-restrictions-android-for-work.md#work-profile-only) [kullanarak cihazları uyumlu veya uyumsuz olarak Işaretlemek için Android kurumsal ayarları](../protect/compliance-policy-create-android-for-work.md#work-profile) ' na bakın.

Ayarlarınızı seçerken, kullanım senaryolarını gözden geçirdiğinizden ve sınıflandırdığınızdan emin olun. Ardından, seçilen güvenlik düzeyi için kılavuzdan sonra kullanıcıları yapılandırın. Önerilen ayarları kuruluşunuzun ihtiyaçlarına göre ayarlayabilirsiniz. Güvenlik takımınızın tehdit ortamını değerlendirdiğinden, risk altında olduğundan ve kullanışlılığın etkisini belirttiğinizden emin olun.

Kişisel olarak sahip olunan iş profili cihazlarında, önerilen iki güvenlik yapılandırması çerçevesi vardır:

- [İş profili temel güvenlik (düzey 1)](#work-profile-basic-security) 
- [İş profili yüksek güvenlik (düzey 3)](#work-profile-high-security) 

> [!Note]
> Android kurumsal iş profili cihazlarında kullanılabilen ayarlar nedeniyle, gelişmiş güvenlik (düzey 2) teklifi yoktur. Kullanılabilir ayarlar düzey 1 ile düzey 2 arasındaki farkı aşmayın.

## <a name="work-profile-basic-security"></a>İş profili temel güvenlik

Düzey 1, kullanıcıların iş veya okul verilerine erişebileceği kişisel cihazlar için önerilen en düşük güvenlik yapılandırmadır. Bu yapılandırma, çoğu mobil kullanıcı için uygulanabilir. Bazı denetimler Kullanıcı deneyimini etkileyebilir.

### <a name="device-compliance"></a>Cihaz uyumluluğu

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Cihazın makine risk puanı üzerinde veya altında olmasını gerektir | Yapılandırılmamış ||
| Cihaz Sistem Durumu | Kökü belirtilmiş cihazlar | Blok ||
| Cihaz Sistem Durumu | Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir | Yapılandırılmamış||
| Cihaz Sistem Durumu | Google Play Hizmetleri yapılandırıldı | Gerektirme ||
| Cihaz Sistem Durumu | Güncel güvenlik sağlayıcısı | Gerektirme ||
| Cihaz Sistem Durumu | SafetyNet cihaz kanıtı | Sertifikalı cihazların & temel bütünlüğünü denetleme | Bu ayar, Son Kullanıcı cihazlarında Google 'ın SafetyNet kanıtlamasını yapılandırır. Temel bütünlük, cihazın bütünlüğünü doğrular. Köklü cihazlar, Öykünücüler, sanal cihazlar ve değişiklik işaretlerine sahip cihazlar temel bütünlüğü başarısız oluyor.<p>Temel bütünlük ve sertifikalı cihazlar, Google 'ın hizmetleriyle cihazın uyumluluğunu doğrular. Yalnızca Google tarafından sertifikalı değiştirilmemiş cihazlar bu denetimi geçirebilir. |
| Cihaz Özellikleri | En düşük işletim sistemi sürümü | Biçim: Ana. Ikincil<br>Örnek: 5,0| Microsoft, en düşük Android ana sürümünün Microsoft uygulamaları için desteklenen Android sürümleriyle eşleşecek şekilde yapılandırılmasını önerir. Android kurumsal gereksinimleri olan OEM 'Ler ve cihazlar, geçerli sevkiyat sürümü + bir mektup yükseltmesi desteklemelidir. Android, bilgi çalışanları için Android 8,0 ve üstünü öneriyor. Android 'in en son önerileri için bkz. [Android Enterprise önerilen gereksinimleri](https://www.android.com/enterprise/recommended/requirements/). |
| Cihaz Özellikleri | En yüksek işletim sistemi sürümü | Yapılandırılmamış ||
| Sistem Güvenliği | Mobil cihazların kilidini açmak için bir parola gerektir | Gerektirme ||
| Sistem Güvenliği | Gerekli parola türü | Sayısal karmaşık | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Sistem Güvenliği | Minimum parola uzunluğu | 6 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Sistem Güvenliği | Parola istenmeden önce geçen işlem yapılmayan dakika sayısı| 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir.|
| Sistem Güvenliği | Parolanın süresi dolana kadar geçen gün sayısı| Yapılandırılmamış | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Sistem Güvenliği | Kullanılması önleneceği önceki parola sayısı | Yapılandırılmamış | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Sistem Güvenliği | Cihazda veri depolamanın şifrelenmesi | Gerektirme ||
| Sistem Güvenliği | Bilinmeyen kaynaklardan gelen uygulamaları engelle | Blok ||
| Sistem Güvenliği | Şirket Portalı uygulama çalışma zamanı bütünlüğü | Gerektirme ||
| Sistem Güvenliği | Cihazda USB hata ayıklamayı engelle | Blok | Bu ayar, bir USB cihazı kullanarak hata ayıklamayı engellediğinde, sorun giderme amacıyla yararlı olabilecek Günlükler toplama özelliğini de devre dışı bırakır. |
| Sistem Güvenliği | En düşük güvenlik düzeltme eki düzeyi | Yapılandırılmamış | Android cihazlar aylık güvenlik düzeltme ekleri alabilir, ancak yayın OEM 'Lere ve/veya taşıyıcılar 'e bağımlıdır. Kuruluşlar, bu ayarı uygulamadan önce dağıtılmış Android cihazlarının güvenlik güncelleştirmelerini aldığından emin olmalıdır. En son düzeltme eki sürümleri için bkz. [Android güvenlik bültenleri](https://source.android.com/security/bulletin/). |
| Uyumsuzluk eylemleri | Cihazı uyumsuz olarak işaretle | Hemen | Varsayılan olarak, ilke cihazı uyumsuz olarak işaretlemek üzere yapılandırılır. Ek eylemler kullanılabilir. Daha fazla bilgi için bkz. [Intune 'da uyumlu olmayan cihazlar için eylemleri yapılandırma](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Cihaz kısıtlamaları

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| İş profili ayarları | İş ve kişisel profiller arasında kopyalama ve yapıştırma | Blok ||
| İş profili ayarları | İş ve kişisel profiller arasında veri paylaşımı | İş profilindeki uygulamalar kişisel profilden gelen paylaşım isteklerini işleyebilir ||
| İş profili ayarları | Cihaz kilitliyken iş profili bildirimleri | Yapılandırılmamış | Bu ayarı engellemek, iş profili bildirimlerinde önemli verilerin açığa çıkmamasını sağlar ve bu durum kullanılabilirliği etkileyebilir. |
| İş profili ayarları | Varsayılan uygulama izinleri | Cihaz Varsayılanı | Yöneticiler, dağıttıkları uygulamalar tarafından verilen izinleri gözden geçirmeniz ve ayarlamamız gerekir. |
| İş profili ayarları | Hesap ekleme ve kaldırma | Blok ||
| İş profili ayarları | Bluetooth ile kişi paylaşımı | Etkinleştir | Varsayılan olarak, iş kişilerine erişim, Bluetooth tümleştirmesi aracılığıyla otomobil gibi diğer cihazlarda kullanılamaz. Bu ayarın etkinleştirilmesi, eller ücretsiz kullanıcı deneyimlerini geliştirir. Ancak Bluetooth cihazı, ilk bağlantı sırasında kişileri önbelleğe alabilir. Kuruluşlar, bu ayarı uygularken veri koruma sorunlarını kabul eden kullanılabilirlik senaryolarına karşı dengelemelidir. |
| İş profili ayarları | Ekran yakalama | Blok ||
| İş profili ayarları | Kişisel profilde iş kişisi arayan kimliğini görüntüleme | Yapılandırılmamış ||
| İş profili ayarları | Kişisel profilden iş kişilerini ara | Yapılandırılmamış | Kullanıcıların kişisel profilden iş kişilerine erişmesini engellemek, kişisel profilde metin mesajlaşma ve çevirici deneyimleri gibi bazı kullanılabilirlik senaryolarını etkileyebilir. Kuruluşlar, bu ayarı uygularken veri koruma sorunlarını kabul eden kullanılabilirlik senaryolarına karşı dengelemelidir. |
| İş profili ayarları | Kamera | Yapılandırılmamış ||
| İş profili ayarları | İş profili uygulamalarından Pencere öğelerinin kullanılmasına izin ver | Etkinleştir ||
| İş profili ayarları | Iş profili parolası gerektir | Gerektirme ||
| İş profili ayarları | Minimum parola uzunluğu | 6 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| İş profili ayarları | İş profili kilitlenmeden önce geçmesi gereken işlem yapılmayan dakika sayısı| 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| İş profili ayarları | İş profili silinmeden önce oturum açma hatalarının sayısı| 10 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| İş profili ayarları | Parola geçerlilik süresi (gün) | Yapılandırılmamış | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| İş profili ayarları | Gerekli parola türü | Sayısal karmaşıklık ||
| İş profili ayarları | Önceki parolaların yeniden kullanılmasını engelleme | Yapılandırılmamış | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir.|
| İş profili ayarları | Parmak izi ile kilit açma | Yapılandırılmamış ||
| İş profili ayarları | Akıllı Kilitleme ve diğer güven aracıları | Yapılandırılmamış |||
| Cihaz parolası | Minimum parola uzunluğu | 6 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Cihaz parolası | Ekran kilitlenmeden önce geçmesi gereken, işlem yapılmayan dakika sayısı | 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Cihaz parolası | Cihaz silinmeden önceki oturum açma hatası sayısı | 10 | Bu ayar, cihazın silinmesini değil, bir iş profili silme işlemi tetikler. |
| Cihaz parolası | Parola geçerlilik süresi (gün) | Yapılandırılmamış | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Cihaz parolası | Gerekli parola türü | Sayısal karmaşıklık ||
| Cihaz parolası | Önceki parolaların yeniden kullanılmasını engelleme | Yapılandırılmamış | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Cihaz parolası | Parmak izi ile kilit açma | Yapılandırılmamış ||
| Cihaz parolası | Akıllı Kilitleme ve diğer güven aracıları | Yapılandırılmamış ||
| Sistem Güvenliği | Uygulamalarda tehdit taraması | Gerektirme | Bu ayar, Son Kullanıcı cihazlarında Google 'ın uygulama taramasını doğrulama özelliğinin açık olmasını sağlar. Yapılandırıldıysa, son kullanıcının Android cihazında Google 'ın uygulama taramasını açana kadar erişim engellenir. |
| Sistem Güvenliği | Kişisel profilde bilinmeyen kaynaklardan uygulama yüklemelerini engelleyin | Blok ||

> [!Note]
> Android kurumsal iş profili etkinleştirildiğinde, "bir kilit" varsayılan olarak cihaz ve iş profili şifreleri birleştirilecek şekilde yapılandırılır. İş profili ve cihaz geçiş kodlarının, gerekirse iş profili ayarları altında ayrılması için bir kilit devre dışı bırakılabilir.

## <a name="work-profile-high-security"></a>İş profili yüksek güvenlik

Düzey 3, kullanıcılar veya gruplar tarafından benzersiz derecede yüksek riskli olan cihazlar için önerilen yapılandırmadır. Örneğin, yetkisiz kullanım açısından çok önemli olan verileri işleyen kullanıcılar önemli ölçüde malzeme kaybına neden olur. Bir kuruluş, iyi bir şekilde ele alınan ve Gelişmiş reklam işlemleri tarafından hedeflenmek için aşağıda açıklanan ek kısıtlamalara sahiptir. Bu yapılandırma, düzey 1 ' deki yapılandırmayı şu şekilde genişletir:
- Mobil tehdit savunması veya Microsoft Defender ATP uygulama.
- iş profili veri senaryolarını kısıtlama.
- daha güçlü parola ilkeleri ayarlama.

Düzey 3 ' te zorlanan ilke ayarları, 1. düzey için önerilen tüm ilke ayarlarını içerir. Ancak, aşağıda listelenen ayarlar yalnızca eklenmiş veya değiştirilmiş olan ayarları içerir. Bu ayarlar, kullanıcılar veya uygulamalar için biraz daha yüksek bir etkiye sahip olabilir. Mobil cihazlarda hassas bilgilere erişimi olan riskler için daha uygun bir güvenlik düzeyi uygular.

### <a name="device-compliance"></a>Cihaz uyumluluğu

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Cihazın makine risk puanı üzerinde veya altında olmasını gerektir | Temizle | Bu ayar Microsoft Defender ATP gerektirir. Daha fazla bilgi için bkz. [Intune 'Da koşullu erişimle Microsoft Defender ATP](../protect/advanced-threat-protection.md)Için uyumluluğu zorlama.<p>Müşteriler, Microsoft Defender ATP veya bir mobil tehdit savunması çözümü uygulamayı düşünmelidir. Her ikisini de dağıtmak gerekli değildir. |
| Cihaz Sistem Durumu | Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir | Korunmalıdır | Bu ayar bir mobil tehdit savunma ürünü gerektirir. Daha fazla bilgi için bkz. [Kayıtlı cihazlar Için mobil tehdit savunması](../protect/mtd-device-compliance-policy-create.md).<p>Müşteriler, Microsoft Defender ATP veya bir mobil tehdit savunması çözümü uygulamayı düşünmelidir. Her ikisini de dağıtmak gerekli değildir.|
| Cihaz Özellikleri | En düşük işletim sistemi sürümü | Biçim: Ana. Ikincil<br>Örnek: 8,0| Microsoft, en düşük Android ana sürümünün Microsoft uygulamaları için desteklenen Android sürümleriyle eşleşecek şekilde yapılandırılmasını önerir. Android kurumsal gereksinimleri olan OEM 'Ler ve cihazlar, geçerli sevkiyat sürümü + bir mektup yükseltmesi desteklemelidir. Android, bilgi çalışanları için Android 8,0 ve üstünü öneriyor. Android 'in en son önerileri için bkz. Android Enterprise önerilen gereksinimleri |
| Sistem Güvenliği | Parolanın süresi dolana kadar geçen gün sayısı | 365 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Sistem Güvenliği | Kullanılması önleneceği önceki parola sayısı | 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |


### <a name="device-restrictions"></a>Cihaz kısıtlamaları

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| İş profili ayarları | Cihaz kilitliyken iş profili bildirimleri | Blok | Bu ayarı engellemek, iş profili bildirimlerinde önemli verilerin açığa çıkmamasını sağlar ve bu durum kullanılabilirliği etkileyebilir. |
| İş profili ayarları | Bluetooth ile kişi paylaşımı | Yapılandırılmamış | Varsayılan olarak, iş kişilerine erişim, Bluetooth tümleştirmesi aracılığıyla otomobil gibi diğer cihazlarda kullanılamaz. Bu ayarın etkinleştirilmesi, eller ücretsiz kullanıcı deneyimlerini geliştirir. Ancak Bluetooth cihazı, ilk bağlantı sırasında kişileri önbelleğe alabilir. Kuruluşlar, bu ayarı uygularken veri koruma sorunlarını kabul eden kullanılabilirlik senaryolarına karşı dengelemelidir. |
| İş profili ayarları | Kişisel profilden iş kişilerini ara | Blok | Kullanıcıların kişisel profilden iş kişilerine erişmesini engellemek, kişisel profilde metin mesajlaşma ve çevirici deneyimleri gibi bazı kullanılabilirlik senaryolarını etkileyebilir. Kuruluşlar, bu ayarı uygularken veri koruma sorunlarını kabul eden kullanılabilirlik senaryolarına karşı dengelemelidir. |
| İş profili ayarları | İş profili uygulamalarından Pencere öğelerinin kullanılmasına izin ver | Yapılandırılmamış ||
| İş profili ayarları | İş profili silinmeden önce oturum açma hatalarının sayısı | 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| İş profili ayarları | Parola geçerlilik süresi (gün) | 365 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| İş profili ayarları | Önceki parolaların yeniden kullanılmasını engelleme | 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| İş profili ayarları | Akıllı Kilitleme ve diğer güven aracıları | Blok ||
| Cihaz parolası | Cihaz silinmeden önceki oturum açma hatası sayısı | 5 | Bu ayar, cihazın silinmesini değil, bir iş profili silme işlemi tetikler. |
| Cihaz parolası | Parola geçerlilik süresi (gün) | 365 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Cihaz parolası | Önceki parolaların yeniden kullanılmasını engelleme | 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |

## <a name="next-steps"></a>Sonraki adımlar

Yöneticiler, [Intune 'un PowerShell betikleri](https://github.com/microsoftgraph/powershell-intune-samples)Ile örnek [Android Enterprise SECURITY Configuration Framework JSON şablonlarını](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) içe aktararak, test ve üretim kullanımı için, yukarıdaki yapılandırma düzeylerini, test ve üretim kullanımı için dahil edebilir.
