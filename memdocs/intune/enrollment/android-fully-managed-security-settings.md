---
title: Android kurumsal tam olarak yönetilen güvenlik yapılandırması
titleSuffix: Microsoft Intune
description: Android kurumsal tam olarak yönetilen temel, gelişmiş ve yüksek güvenlik için önerilen ayarları öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
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
ms.openlocfilehash: a4c2a9aa48d17b9cb2b386a4e4cb4df8fb36caac
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502881"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Android kurumsal tam olarak yönetilen güvenlik yapılandırması

[Android kurumsal güvenlik yapılandırma çerçevesinin](android-configuration-framework.md)bir parçası olarak, Android kurumsal tam olarak yönetilen mobil kullanıcılar için aşağıdaki ayarları uygulayın. Her ilke ayarı hakkında daha fazla bilgi için bkz. Android kurumsal cihaz sahibi ayarları Intune ve Android kurumsal cihaz ayarları [kullanılarak cihazları uyumlu veya uyumsuz olarak işaretlemek Için](../protect/compliance-policy-create-android-for-work.md#device-owner) [Intune 'u kullanarak özelliklere izin verme veya bu özellikleri kısıtlama](../configuration/device-restrictions-android-for-work.md#device-owner-only).

Ayarlarınızı seçerken, kullanım senaryolarını gözden geçirdiğinizden ve sınıflandırdığınızdan emin olun. Ardından, seçilen güvenlik düzeyi için kılavuzdan sonra kullanıcıları yapılandırın. Önerilen ayarları kuruluşunuzun ihtiyaçlarına göre ayarlayabilirsiniz. Güvenlik takımınızın tehdit ortamını değerlendirdiğinden, risk altında olduğundan ve kullanışlılığın etkisini belirttiğinizden emin olun.

Şirkete ait tam yönetilen cihazlar için önerilen üç güvenlik yapılandırması çerçevesi vardır:

- [Tam olarak yönetilen temel güvenlik (düzey 1)](#fully-managed-basic-security) 
- [Tam olarak yönetilen gelişmiş güvenlik (düzey 2)](#fully-managed-enhanced-security)
- [Tam olarak yönetilen yüksek güvenlik (düzey 3)](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>Tam olarak yönetilen temel güvenlik

Düzey 1, kuruluşa ait mobil cihazlar için önerilen en düşük güvenlik yapılandırmadır.

Düzey 1 ' deki ilkeler, kullanıcılara etkisini en aza indirerek makul bir veri erişim düzeyini zorlar. Bu, parola ilkeleri, en düşük işletim sistemi sürümü, Safnetnet cihaz kanıtlaması ve belirli cihaz işlevlerini devre dışı bırakarak (USB dosya aktarımları gibi) yapılır. 

### <a name="device-compliance"></a>Cihaz uyumluluğu

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Cihazın makine risk puanı üzerinde veya altında olmasını gerektir | Yapılandırılmamış ||
| Cihaz Sistem Durumu | Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir | Yapılandırılmamış||
| Cihaz Sistem Durumu | SafetyNet cihaz kanıtı | Sertifikalı cihazların & temel bütünlüğünü denetleme | Bu ayar, Son Kullanıcı cihazlarında Google 'ın SafetyNet kanıtlamasını yapılandırır. Temel bütünlük, cihazın bütünlüğünü doğrular. Köklü cihazlar, Öykünücüler, sanal cihazlar ve değişiklik işaretlerine sahip cihazlar temel bütünlüğü başarısız oluyor.<br>Temel bütünlük ve sertifikalı cihazlar, Google 'ın hizmetleriyle cihazın uyumluluğunu doğrular. Yalnızca Google tarafından sertifikalı değiştirilmemiş cihazlar bu denetimi geçirebilir. |
| Cihaz Özellikleri | En düşük işletim sistemi sürümü | Biçim: Ana. Ikincil<br>Örnek: 8,0| Microsoft, en düşük Android ana sürümünün Microsoft uygulamaları için desteklenen Android sürümleriyle eşleşecek şekilde yapılandırılmasını önerir. Android kurumsal gereksinimleri olan OEM 'Ler ve cihazlar, geçerli sevkiyat sürümü + bir mektup yükseltmesi desteklemelidir. Android, bilgi çalışanları için Android 8,0 ve üstünü öneriyor. Android 'in en son önerileri için bkz. [Android Enterprise önerilen gereksinimleri](https://www.android.com/enterprise/recommended/requirements/). |
| Cihaz Özellikleri | En yüksek işletim sistemi sürümü | Yapılandırılmamış ||
| Cihaz Özellikleri | En düşük güvenlik düzeltme eki düzeyi | Yapılandırılmamış | Android cihazlar aylık güvenlik düzeltme ekleri alabilir, ancak yayın OEM 'Lere ve/veya taşıyıcılar 'e bağımlıdır. Kuruluşlar, bu ayarı uygulamadan önce dağıtılmış Android cihazlarının güvenlik güncelleştirmelerini aldığından emin olmalıdır. En son düzeltme eki sürümleri için bkz. [Android güvenlik bültenleri](https://source.android.com/security/bulletin/). |
| Sistem Güvenliği | Mobil cihazların kilidini açmak için bir parola gerektir | Gerektirme ||
| Sistem Güvenliği | Gerekli parola türü | Sayısal karmaşık | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Sistem Güvenliği | Minimum parola uzunluğu | 6 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Sistem Güvenliği | Parola istenmeden önce geçen işlem yapılmayan dakika sayısı| 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir.|
| Sistem Güvenliği | Parolanın süresi dolana kadar geçen gün sayısı| Yapılandırılmamış ||
| Sistem Güvenliği |    Kullanıcının bir parolayı yeniden kullanabilmesi için gereken parola sayısı | Yapılandırılmamış ||
| Sistem Güvenliği | Cihazda veri depolamanın şifrelenmesi | Gerektirme ||
| Uyumsuzluk eylemleri | Cihazı uyumsuz olarak işaretle | Hemen | Varsayılan olarak, ilke cihazı uyumsuz olarak işaretlemek üzere yapılandırılır. Ek eylemler kullanılabilir. Daha fazla bilgi için bkz. [Intune 'da uyumlu olmayan cihazlar için eylemleri yapılandırma](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Cihaz kısıtlamaları

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| Genel | Ekran yakalama | Yapılandırılmadı ||
| Genel | Kamera | Yapılandırılmadı ||
| Genel | Varsayılan izin ilkesi | Cihaz Varsayılanı ||
| Genel | Tarih ve saat değişiklikleri | Yapılandırılmadı ||
| Genel | Birim değişiklikleri | Yapılandırılmadı ||
| Genel | Fabrika sıfırlaması | Blok ||
| Genel | Güvenli önyükleme | Blok ||
| Genel | Durum çubuğu | Yapılandırılmadı ||
| Genel | Dolaşım veri Hizmetleri | Yapılandırılmadı ||
| Genel | Wi-Fi ayarı değişiklikleri | Yapılandırılmadı ||
| Genel | Bluetooth yapılandırması | Yapılandırılmadı ||
| Genel | İnternet paylaşımı ve etkin noktalara erişim | Yapılandırılmadı ||
| Genel | USB depolama | Yapılandırılmadı ||
| Genel | USB dosya aktarımı | Blok ||
| Genel | Dış medya | Blok ||
| Genel | NFC kullanarak Kirme verileri | Yapılandırılmadı ||
| Genel | Hata ayıklama özellikleri | Yapılandırılmadı ||
| Genel | Mikrofon ayarlaması | Yapılandırılmadı ||
| Genel | Fabrika ayarlarına sıfırlama koruması e-postaları | Yapılandırılmadı ||
| Genel | Ağ çıkış tarama | Yapılandırılmadı ||
| Genel | Sistem Güncelleştirmesi | Automatic ||
| Genel | Bildirim pencereleri | Yapılandırılmadı ||
| Genel | İlk kullanım ipuçlarını atla | Yapılandırılmadı ||
| Sistem güvenliği | Uygulamalarda tehdit taraması |Gerektirme ||
| Cihaz deneyimi | Kayıt profili türü | Tam olarak yönetilir ||
| Cihaz deneyimi | Microsoft başlatıcısı 'nı varsayılan başlatıcısını yap | Yapılandırılmamış | Kuruluşlar, tam olarak yönetilen cihazlarda tutarlı bir giriş ekranı deneyimi sağlamak için Microsoft başlatıcısı 'nı uygulamayı seçebilir. Daha fazla bilgi için bkz. [Intune Ile Android kurumsal tam yönetilen cihazlarda Microsoft başlatıcısı kurma](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) |
| Parola | Kilit ekranını devre dışı bırak | Yapılandırılmadı ||
| Parola | Kilit ekranı özellikleri devre dışı | 0 seçili ||
| Parola | Gerekli parola türü | Sayısal karmaşık ||
| Parola | Minimum parola uzunluğu | 6 ||
| Parola | Parolanın süresi dolana kadar geçen gün sayısı | Yapılandırılmamış ||
| Parola | Kullanıcının bir parolayı yeniden kullanabilmesi için gereken parola sayısı | Yapılandırılmamış ||
| Parola | Cihaz silinmeden önceki oturum açma hatası sayısı | 10 ||
| Güç ayarları | Kilitleme süresi ekranı | 5 ||
| Güç ayarları | Cihaz prize takılıyken ekranda açık ekran | Yapılandırılmamış ||
| Kullanıcılar ve hesaplar | Yeni kullanıcı ekle | Yapılandırılmamış ||
| Kullanıcılar ve hesaplar | Kullanıcı kaldırma | Yapılandırılmamış ||
| Kullanıcılar ve hesaplar | Hesap değişiklikleri (yalnızca adanmış cihazlar) | Yapılandırılmamış ||
| Kullanıcılar ve hesaplar | Kişisel Google hesapları | Yapılandırılmamış ||
| Kullanıcılar ve hesaplar | Kullanıcı, kimlik bilgilerini yapılandırabilir | Blok ||
| Uygulamalar | Bilinmeyen kaynaklardan yüklemeye izin ver | Yapılandırılmamış ||
| Uygulamalar | Google Play Store 'daki tüm uygulamalara erişime izin ver | Yapılandırılmamış | Varsayılan olarak kullanıcılar, tam olarak yönetilen cihazlarda Google Play Store kişisel uygulamalar yükleyemez. Kuruluşlar, kişisel kullanım için tam olarak yönetilen cihazların kullanılmasına izin vermek istiyorsanız, bu ayarı değiştirmeyi göz önünde bulundurun. |
| Uygulamalar | Uygulama otomatik güncelleştirmeleri | Yalnızca Wi-Fi | Kuruluşlar, cep telefonu ağı üzerinde uygulama güncelleştirmeleri gerçekleştiğinde veri planı ücretleri gerçekleşebildiği sürece bu ayarı ayarlamamalıdır. |

## <a name="fully-managed-enhanced-security"></a>Tam olarak yönetilen gelişmiş güvenlik

Düzey 2, kullanıcıların daha hassas bilgilere erişebileceği şirkete ait cihazlar için önerilen yapılandırmadır. Bu cihazlar, günümüzde kuruluşlarda doğal bir hedeftir. Bu ayarlar, yüksek düzeyde güvenlik personeli olan büyük bir personeli varsaymaz. Bu nedenle, kurumsal kuruluşların çoğu tarafından erişilebilir olmaları gerekir. Bu yapılandırma, daha güçlü parola ilkeleri gerçekleştirerek ve Kullanıcı/hesap yeteneklerini devre dışı bırakarak, düzey 1 ' deki yapılandırmanın üzerine genişletilir.

Düzey 2 ayarları, 1. düzey için önerilen tüm ilke ayarlarını içerir. Ancak, aşağıda listelenen ayarlar yalnızca eklenmiş veya değiştirilmiş olan ayarları içerir. Bu ayarlar, kullanıcılar veya uygulamalar için biraz daha yüksek bir etkiye sahip olabilir. Mobil cihazlarda hassas bilgilere erişimi olan riskler için daha uygun bir güvenlik düzeyi uygular.

### <a name="device-compliance"></a>Cihaz uyumluluğu

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| Sistem Güvenliği | Parolanın süresi dolana kadar geçen gün sayısı | 365 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Sistem Güvenliği |    Kullanıcının bir parolayı yeniden kullanabilmesi için gereken parola sayısı | 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |

### <a name="device-restrictions"></a>Cihaz kısıtlamaları

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| Genel | Fabrika ayarlarına sıfırlama koruması e-postaları | Google hesabı e-posta adresleri ||
| Genel | E-posta adresleri listesi (yalnızca Google hesabı e-posta adresleri seçeneği) | example@gmail.com | Bu ilkeyi, cihaz yöneticilerinin temizlenmeden sonra cihazların kilidini açabilebileceği Google e-posta adreslerini belirtmek için el ile güncelleştirin. |
| Cihaz parolası | Parolanın süresi dolana kadar geçen gün sayısı | 365 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Cihaz parolası | Kullanıcının bir parolayı yeniden kullanabilmesi için gereken parola sayısı | 5 | Kuruluşların bu ayarı parola ilkesiyle eşleşecek şekilde güncelleştirmesi gerekebilir. |
| Cihaz parolası | Cihaz silinmeden önceki oturum açma hatası sayısı | 5 ||
| Kullanıcılar ve hesaplar | Yeni kullanıcı ekle | Blok ||
| Kullanıcılar ve hesaplar | Kullanıcı kaldırma | Blok ||
| Kullanıcılar ve hesaplar | Kişisel Google hesapları | Blok ||

## <a name="fully-managed-high-security"></a>Tam olarak yönetilen yüksek güvenlik

3. düzey, her ikisi için önerilen yapılandırmadır:
- büyük ve gelişmiş güvenlik kuruluşları olan kuruluşlar.
- belirli kullanıcılar ve Grup, reklam işlemleri tarafından benzersiz bir şekilde hedeflenecek.
Bu tür kuruluşlar genellikle iyi ifade edilen ve gelişmiş duyuru işlemleri tarafından hedeflenmiştir. Bu nedenle, aşağıda listelenen ek kısıtlamaları ve denetimleri birleşirler.

Bu yapılandırma düzey 2 ' den sonra genişletilir:
- En düşük işletim sistemi sürümünü artırma.
- en güvenli Microsoft Defender ATP veya Mobile Threat Defense düzeyini zorlayarak cihazın uyumlu olduğundan emin olma.
- En düşük işletim sistemi sürümünü artırma.
- ek cihaz kısıtlamalarını zorunlu tutma (kilit ekranında redaksiyonu kaldırma bildirimleri devre dışı bırakma gibi).
- uygulamaların her zaman güncel olmasını gerektirin. 

Düzey 3 ' te zorlanan ilke ayarları, düzey 2 için önerilen tüm ilke ayarlarını içerir. Aşağıda listelenen ayarlar yalnızca eklenmiş veya değiştirilmiş olan ayarları içerir. Bu ayarlar, kullanıcılar veya uygulamalar üzerinde önemli bir etkiye sahip olabilir. Hedeflenmiş kuruluşlara yönelik riskler için daha uygun bir güvenlik düzeyi uygular.


### <a name="device-compliance"></a>Cihaz uyumluluğu

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Cihazın makine risk puanı üzerinde veya altında olmasını gerektir | Temizle | Bu ayar Microsoft Defender ATP gerektirir. Daha fazla bilgi için bkz. [Intune 'Da koşullu erişimle Microsoft Defender ATP](../protect/advanced-threat-protection.md)Için uyumluluğu zorlama.<p> Müşteriler, Microsoft Defender ATP veya bir mobil tehdit savunması çözümü uygulamayı düşünmelidir. Her ikisini de dağıtmak gerekli değildir. |
| Cihaz Sistem Durumu | Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir | Korunmalıdır | Bu ayar bir mobil tehdit savunma ürünü gerektirir. Daha fazla bilgi için bkz. [Kayıtlı cihazlar Için mobil tehdit savunması](../protect/mtd-device-compliance-policy-create.md).<p>Müşteriler, Microsoft Defender ATP veya bir mobil tehdit savunması çözümü uygulamayı düşünmelidir. Her ikisini de dağıtmak gerekli değildir.|
| Cihaz Özellikleri | En düşük işletim sistemi sürümü | Biçim: Ana. Ikincil<br>Örnek: 10,0| Microsoft, en düşük Android ana sürümünün Microsoft uygulamaları için desteklenen Android sürümleriyle eşleşecek şekilde yapılandırılmasını önerir. Android kurumsal gereksinimleri olan OEM 'Ler ve cihazlar, geçerli sevkiyat sürümü + bir mektup yükseltmesi desteklemelidir. Android, bilgi çalışanları için Android 8,0 ve üstünü öneriyor. Android 'in en son önerileri için bkz. Android Enterprise önerilen gereksinimleri |

### <a name="device-restrictions"></a>Cihaz kısıtlamaları

| Section | Ayar | Değer | Notlar |
| ----- | ----- | ----- | ----- |
| Genel | Tarih ve saat değişiklikleri | Blok ||
| Genel | İnternet paylaşımı ve etkin noktalara erişim | Blok ||
| Genel | NFC kullanarak Kirme verileri | Blok ||
| Cihaz parolası | Kilit ekranı özellikleri devre dışı | Güven aracıları, redaksiyonu kaldırma bildirimleri ||
| Uygulamalar | Uygulama otomatik güncelleştirmeleri | Her zaman | Kuruluşlar, cep telefonu ağı üzerinde uygulama güncelleştirmeleri gerçekleştiğinde veri planı ücretleri gerçekleşebildiği sürece bu ayarı ayarlamamalıdır. |


## <a name="next-steps"></a>Sonraki adımlar

Yöneticiler, [Intune 'un PowerShell betikleri](https://github.com/microsoftgraph/powershell-intune-samples)Ile örnek [Android Enterprise SECURITY Configuration Framework JSON şablonlarını](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) içe aktararak, test ve üretim kullanımı için, yukarıdaki yapılandırma düzeylerini, test ve üretim kullanımı için dahil edebilir.
