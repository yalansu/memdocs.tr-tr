---
title: Microsoft Intune - Azure’daki Android Kurumsal uyumluluk ayarları | Microsoft Docs
description: Microsoft Intune'da Android Kurumsal cihazlarınızda uyumluluk ayarı yaparken kullanabileceğiniz tüm ayarların bulunduğu listeyi inceleyin. Parola kurallarını ayarlayın, en düşük veya en yüksek işletim sistemi sürümünü seçin, belirli uygulamaları kısıtlayın, parolaların yeniden kullanılmasını engelleyin ve çok daha fazlasını yapın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 9da89713-6306-4468-b211-57cfb4b51cc6
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d419eb341d3d15a8307396d1bcf13235201606f4
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729236"
---
# <a name="android-enterprise-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Intune'u kullanarak cihazları uyumlu veya uyumlu değil şeklinde işaretlemek için kullanabileceğiniz Android Kurumsal ayarları

Bu makalede Intune'daki Android Kurumsal cihazları için yapılandırabileceğiniz farklı uyumluluk ayarları listelenmekte ve anlatılmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu ayarları kullanabilir ve bu sayede kök erişim izni verilmiş (jailbreak uygulanmış) cihazları uyumlu değil olarak işaretleyebilir, izin verilen tehdit düzeyi belirleyebilir, Google Play Koruması'nı etkinleştirebilir ve çok daha fazlasını yapabilirsiniz.

Bu özellik şu platformlarda geçerlidir:

- Android Kurumsal

Intune yöneticisi olarak bu uyumluluk ayarlarını kullanarak kuruluşunuzun kaynaklarının korunmasına yardımcı olabilirsiniz. Uyumluluk ilkeleri ve işlevleri hakkında daha fazla bilgi için bkz. [Cihaz uyumluluğunu kullanmaya başlama](device-compliance-get-started.md).

> [!IMPORTANT]
> Uyumluluk ilkeleri, ayrılmış Android Kurumsal cihazları için de geçerlidir. Bir cihaza uyumluluk ilkesinin atanması durumunda cihaz **Uyumlu değil** şeklinde görünebilir. Koşullu erişim ve uyumluluk zorlama adanmış cihazlarda kullanılamaz. Ayrılmış cihazların atanan ilkelerinizle uyumlu olmasını sağlamak için gerekli görevleri veya eylemleri gerçekleştirdiğinizden emin olun.

## <a name="before-you-begin"></a>Başlamadan önce

[Bir uyumluluk Ilkesi oluşturun](create-compliance-policy.md#create-the-policy). **Platform**Için **Android kurumsal**' i seçin.


## <a name="device-owner"></a>Cihaz sahibi

### <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

- **Cihazın makine risk puanı üzerinde veya altında olmasını gerektir**  

  Microsoft Defender ATP tarafından değerlendirilen cihazlar için izin verilen en yüksek makine risk Puanını seçin. Bu puanı aşan cihazlar uyumsuz olarak işaretlenir.
  - **Yapılandırılmadı** (*varsayılan*)
  - **Temizle**
  - **Düşük**
  - **Medium**
  - **Geniş**

### <a name="device-health"></a>Cihaz Sistem Durumu

- **Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir**  
  [Mobil tehdit savunması hizmetiniz](mobile-threat-defense.md)tarafından değerlendirilen izin verilen maksimum cihaz tehdit düzeyini seçin. Bu tehdit düzeyini aşan cihazlar uyumsuz olarak işaretlenir. Bu ayarı kullanmak için izin verilen tehdit düzeyini seçin:

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Güvenli** -Bu seçenek en güvenli seçenektir ve cihazın herhangi bir tehdit olamayacağı anlamına gelir. Herhangi bir tehdit düzeyi algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Düşük**:-cihaz, yalnızca düşük düzeyde tehditler varsa uyumlu olarak değerlendirilir. Daha yüksek bir tehdit düzeyi, cihazı uyumlu değil durumuna getirir.
  - **Orta** -cihazda bulunan tehditler düşük veya orta düzeydeyse cihaz uyumlu olarak değerlendirilir. Yüksek düzeyde tehditler algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Yüksek** -Bu seçenek, tüm tehdit düzeylerine izin verdiği için en az güvenli seçenektir. Bu çözüm, yalnızca raporlama amacıyla kullanıyorsanız kullanışlı olabilir.
  
> [!NOTE]
> Tüm Mobile Threat Defense (MTD) sağlayıcıları, uygulama yapılandırması kullanılarak Android kurumsal cihaz sahibi dağıtımlarında desteklenir. Intune 'da Android kurumsal cihaz sahibi platformlarını desteklemek için gereken tam yapılandırma için MTD sağlayıcınızla görüşün.

#### <a name="google-play-protect"></a>Google Play Koruması

- **SafetyNet cihaz kanıtı**  
  Uyulması gereken [SafetyNet kanıtı](https://developer.android.com/training/safetynet/attestation.html) düzeyini ayarlayın. Seçenekleriniz şunlardır:
  - Yapılandırılmadı (*varsayılan*)-ayar, uyumluluk veya uyumsuzluk Için **değerlendirilmez** .
  - **Temel bütünlük denetimi**
  - **Temel bütünlük ve sertifikalı cihaz denetimi**

### <a name="device-properties"></a>Cihaz Özellikleri

#### <a name="operating-system-version"></a>İşletim Sistemi Sürümü

- **En düşük işletim sistemi sürümü**  
  Bir cihaz en düşük işletim sistemi sürümü gereksinimini karşılamadığında uyumsuz olarak bildirilir. Yükseltme hakkında bilgi içeren bir bağlantı gösterilir. Son kullanıcı, cihazını yükselttikten sonra kuruluş kaynaklarına erişebilir.

  *Varsayılan olarak, sürüm yapılandırılmaz*.

- **En yüksek işletim sistemi sürümü**  
  Cihaz kuralda belirtilenden sonraki bir işletim sistemi sürümünü kullandığında, kuruluş kaynaklarına erişim engellenir. Kullanıcıdan BT yöneticisine başvurması istenir. İşletim sistemine izin veren bir kural değişikliği oluncaya kadar bu cihaz kuruluş kaynaklarına erişemez.

  *Varsayılan olarak, sürüm yapılandırılmaz*.

- **En düşük güvenlik düzeltme eki düzeyi**  
  Bir cihazda olabilecek en eski güvenlik düzeltme eki düzeyini seçin. Bu yama düzeyinin altındaki cihazlar uyumsuz kabul edilir. Tarihin YYYY-AA-GG biçiminde girilmesi gerekir.

  *Varsayılan olarak, bir tarih yapılandırılmaz*.

### <a name="system-security"></a>Sistem Güvenliği

- **Mobil cihazların kilidini açmak için bir parola gerektir**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -kullanıcıların cihazına erişebilmeleri için önce bir parola girmesi gerekir.

- **Gerekli parola türü**  
  Parolanın yalnızca sayısal karakterlerden mi yoksa sayı ve diğer karakterlerin karışımından mı oluşacağını seçin. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı** -parola uyumluluğunu değerlendirmek Için, *cihaz varsayılanı*dışında bir parola gücü seçtiğinizden emin olun.
  - **Parola gerekli, kısıtlama yok**
  - **Zayıf biyometrik** - [güçlü ve zayıf Biyometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (Android 'in Web sitesini açar)
  - **Sayısal** (*varsayılan*): parola yalnızca sayı olmalıdır, örneğin `123456789`. Kullanıcının girmesi gereken **parolanın uzunluk alt sınırını** girin (4 ile 16 karakter arasında).
  - "1111" veya "1234" gibi **sayısal karmaşık** yinelenen veya ardışık sayılara izin verilmez. Kullanıcının girmesi gereken **parolanın uzunluk alt sınırını** girin (4 ile 16 karakter arasında).
  - Alfabede **alfabetik** harfler gereklidir. Rakamlar ve simgeler zorunlu tutulmaz. Kullanıcının girmesi gereken **parolanın uzunluk alt sınırını** girin (4 ile 16 karakter arasında).
  - **Alfasayısal** -büyük harfler, küçük harfler ve sayısal karakterler içerir. Kullanıcının girmesi gereken **parolanın uzunluk alt sınırını** girin (4 ile 16 karakter arasında).
  - **Simgelerle alfasayısal** -büyük harfler, küçük harfler, sayısal karakterler, noktalama işaretleri ve semboller içerir.

  Seçtiğiniz *parola türüne* bağlı olarak, aşağıdaki ayarlar kullanılabilir:
  - **Minimum parola uzunluğu**  
    Parola uzunluğu alt sınırını girin (4 ile 16 karakter arasında).  

  - **Gerekli karakter sayısı**  
    Parolada bulunması gereken karakter sayısını girin (0 ile 16 karakter arasında).

  - **Gereken küçük harfli karakter sayısı**  
    Parolada bulunması gereken küçük harf karakteri sayısını girin (0 ile 16 karakter arasında).

  - **Gereken büyük harfli karakter sayısı**  
    Parolada bulunması gereken büyük harf karakteri sayısını girin (0 ile 16 karakter arasında).

  - **Gereken harf olmayan karakter sayısı**  
    Parolada bulunması gereken harf dışı karakter sayısını (alfabedeki harflerin dışındaki karakterler, 0 ile 16 karakter arasında) girin.

  - **Gerekli sayısal karakter sayısı**  
    Parolada bulunması gereken sayısal karakter sayısını (`1`, `2`, `3` gibi, 0 ile 16 karakter arasında) girin.

  - **Gerekli simge karakter sayısı**  
    Parolada bulunması gereken simge karakter sayısını (`&`, `#`, `%` gibi, 0 ile 16 karakter arasında) girin.

  - **Parola istenmeden önce geçen işlem yapılmayan dakika sayısı**  
    Kullanıcı parolasını yeniden girmeden önce boşta geçen süreyi girin. Seçenekler, *Yapılandırılmadı*ve *1 dakikadan* *8 saate*kadar varsayılan değer içerir.

  - **Parolanın süresi dolana kadar geçen gün sayısı**  
    Cihaz parolasının değiştirilmesi gerekmeden önce geçmesi gereken gün sayısını (1 ile 365 arasında) girin. Örneğin parolanın 60 gün sonra değiştirilmesi için `60` girin. Parola geçerlilik süresi dolduğunda kullanıcıların yeni bir parola oluşturması istenir.

    *Varsayılan olarak, hiçbir değer yapılandırılmaz*.

  - **Kullanıcının bir parolayı yeniden kullanabilmesi için gereken parola sayısı**  
    Yeniden kullanılamayacak parolalar için 1 ile 24 arasında bir sayı girin. Son kullanıcının daha önce kullanılmış parolalar oluşturmasını önlemek için bu ayarı kullanın.  

    *Varsayılan olarak, sürüm yapılandırılmaz*.

#### <a name="encryption"></a>Şifreleme

- **Cihazda veri depolamanın şifrelenmesi**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - , Cihazlarınızda veri depolamayı **ister** .

  Android Kurumsal cihazlarında şifreleme zorunlu olduğundan bu ayarı yapılandırmanız gerekmez.

## <a name="work-profile"></a>İş profili

### <a name="microsoft-defender-atp---for-work-profile"></a>Microsoft Defender ATP- *for Work Profili*

- **Cihazın makine risk puanı üzerinde veya altında olmasını gerektir**  
  Microsoft Defender ATP tarafından değerlendirilen cihazlar için izin verilen en yüksek makine risk Puanını seçin. Bu puanı aşan cihazlar uyumsuz olarak işaretlenir.
  - **Yapılandırılmadı** (*varsayılan*)
  - **Temizle**
  - **Düşük**
  - **Medium**
  - **Geniş**

### <a name="device-health---for-work-profile"></a>Cihaz Durumu- *for Work Profili*

- **Kökü belirtilmiş cihazlar**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Block** -root (Jailbreak uygulanmış) cihazlarını uyumsuz olarak işaretle.

- **Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir**  
  [Mobil tehdit savunması hizmetiniz](mobile-threat-defense.md)tarafından değerlendirilen izin verilen maksimum cihaz tehdit düzeyini seçin. Bu tehdit düzeyini aşan cihazlar uyumsuz olarak işaretlenir. Bu ayarı kullanmak için izin verilen tehdit düzeyini seçin:
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Güvenli** -Bu seçenek en güvenli seçenektir ve cihazın herhangi bir tehdit olamayacağı anlamına gelir. Herhangi bir tehdit düzeyi algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Düşük** -cihaz, yalnızca düşük düzeyde tehditler varsa uyumlu olarak değerlendirilir. Daha yüksek bir tehdit düzeyi, cihazı uyumlu değil durumuna getirir.
  - **Orta** -cihazda bulunan tehditler düşük veya orta düzeydeyse cihaz uyumlu olarak değerlendirilir. Yüksek düzeyde tehditler algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Yüksek** -Bu seçenek, tüm tehdit düzeylerine izin verdiği için en az güvenli seçenektir. Bu çözüm, yalnızca raporlama amacıyla kullanıyorsanız kullanışlı olabilir.

#### <a name="google-play-protect---for-work-profile"></a>Google Play koruma- *for Work Profili*

- **Google Play Hizmetleri yapılandırıldı**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -Google Play Services uygulamasının yüklü ve etkin olmasını gerektirir. Google Play hizmetleri, güvenlik güncelleştirmelerine olanak sağlar ve sertifikalı Google cihazlarında birçok güvenlik özelliği için temel düzeyde bir bağımlılıktır.
  
- **Güncel güvenlik sağlayıcısı**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -güncel bir güvenlik sağlayıcısının bir cihazı bilinen güvenlik açıklarına karşı koruyabilmesini gerektir.
  
- **SafetyNet cihaz kanıtı**  
  Uyulması gereken [SafetyNet kanıtı](https://developer.android.com/training/safetynet/attestation.html) düzeyini ayarlayın. Seçenekleriniz şunlardır:
  - Yapılandırılmadı (*varsayılan*)-ayar, uyumluluk veya uyumsuzluk Için **değerlendirilmez** .
  - **Temel bütünlük denetimi**
  - **Temel bütünlük ve sertifikalı cihaz denetimi**

> [!NOTE]
> Android Kurumsal cihazlardaki **Uygulamalarda tehdit taraması**, bir cihaz yapılandırma ilkesidir. Yöneticiler, yapılandırma ilkesini kullanarak bu ayarı cihazlarda etkinleştirebilir. Bkz. [Android için Intune cihaz kısıtlama ayarları](../configuration/device-restrictions-android-for-work.md).

### <a name="device-properties---for-work-profile"></a>Cihaz özellikleri- *iş profili için*

#### <a name="operating-system-version---for-work-profile"></a>İşletim sistemi sürümü- *iş profili için*

- **En düşük işletim sistemi sürümü**  
Bir cihaz en düşük işletim sistemi sürümü gereksinimini karşılamadığında uyumsuz olarak bildirilir. Yükseltme hakkında bilgi içeren bir bağlantı gösterilir. Son kullanıcı, cihazını yükselttikten sonra kuruluş kaynaklarına erişebilir.

  *Varsayılan olarak, sürüm yapılandırılmaz*.

- **En yüksek işletim sistemi sürümü**  
Cihaz kuralda belirtilenden sonraki bir işletim sistemi sürümünü kullandığında, kuruluş kaynaklarına erişim engellenir. Kullanıcıdan BT yöneticisine başvurması istenir. İşletim sistemine izin veren bir kural değişikliği oluncaya kadar bu cihaz kuruluş kaynaklarına erişemez.

  *Varsayılan olarak, sürüm yapılandırılmaz*.

### <a name="system-security---for-work-profile"></a>Sistem güvenliği- *iş için güvenlik profili*

- **Mobil cihazların kilidini açmak için bir parola gerektir**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -kullanıcıların cihazına erişebilmeleri için önce bir parola girmesi gerekir.  

  Bu ayar cihaz düzeyinde geçerlidir. Yalnızca iş profili düzeyinde parola kullanılmasını istiyorsanız bir yapılandırma ilkesi kullanabilirsiniz. Bkz. [Android için Intune cihaz yapılandırma ayarları](../configuration/device-restrictions-android-for-work.md).

- **Gerekli parola türü**  
  Parolanın yalnızca sayısal karakterlerden mi yoksa sayı ve diğer karakterlerin karışımından mı oluşacağını seçin. Seçenekleriniz şunlardır:
  - **Cihaz Varsayılanı**
  - **Düşük güvenlik biyometriği**
  - En **az sayısal** (*varsayılan*): kullanıcının, 4 ile 16 karakter arasında girmesi gereken **Minimum parola uzunluğunu** girin.
  - **Sayısal karmaşık**: kullanıcının, 4 ile 16 karakter arasında girmesi gereken **Minimum parola uzunluğunu** girin.
  - En **azından alfabetik**: kullanıcının, 4 ile 16 karakter arasında girmesi gereken **Minimum parola uzunluğunu** girin.
  - En **az alfasayısal**: kullanıcının, 4 ile 16 karakter arasında girmesi gereken **Minimum parola uzunluğunu** girin.
  - **Semboller ile en az alfasayısal**: bir kullanıcının girmesi gereken **Minimum parola uzunluğunu** 4 ile 16 karakter arasında girin.

  Seçtiğiniz *parola türüne* bağlı olarak, aşağıdaki ayarlar kullanılabilir:

  - **Parola istenmeden önce geçen işlem yapılmayan dakika sayısı**  
    Kullanıcı parolasını yeniden girmeden önce boşta geçen süreyi girin. Seçenekler, *Yapılandırılmadı*ve *1 dakikadan* *8 saate*kadar varsayılan değer içerir.

  - **Parolanın süresi dolana kadar geçen gün sayısı**  
    Cihaz parolasının değiştirilmesi gerekmeden önce geçmesi gereken gün sayısını (1 ile 365 arasında) girin. Örneğin parolanın 60 gün sonra değiştirilmesi için `60` girin. Parola geçerlilik süresi dolduğunda kullanıcıların yeni bir parola oluşturması istenir.

  - **Minimum parola uzunluğu**  
    Parola uzunluğu alt sınırını girin (4 ile 16 karakter arasında).

  - **Yeniden kullanılmasını önleyen önceki parola sayısı**  
    Yeniden kullanılamayacak parolalar için bir sayı girin. Son kullanıcının daha önce kullanılmış parolalar oluşturmasını önlemek için bu ayarı kullanın.

#### <a name="encryption---for-work-profile"></a>Şifreleme- *for Work Profili*

- **Cihazda veri depolamanın şifrelenmesi**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - , Cihazlarınızda veri depolamayı **ister** .  

  Android Kurumsal cihazlarında şifreleme zorunlu olduğundan bu ayarı yapılandırmanız gerekmez.

#### <a name="device-security---for-work-profile"></a>Cihaz Güvenliği- *iş profili için*

- **Bilinmeyen kaynaklardan gelen uygulamaları engelle**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Blok** - **güvenlik** > **Bilinmeyen kaynakların** etkinleştirildiği kaynakları engelleyin (Android*4,0 üzerinden Android 7. x aracılığıyla desteklenir). Android 8,0 ve üzeri tarafından desteklenmez*).  

  Uygulamaları dışarıdan yüklemek için bilinmeyen kaynaklara izin verilmesi gerekir. Cihazlara dışarıdan Android uygulaması yüklemiyorsanız bu uyumluluk ilkesini etkinleştirmek için bu özelliği **Engelle** olarak ayarlayın.

  > [!IMPORTANT]
  > Dışarıdan uygulama yükleme, **Bilinmeyen kaynaklardan gelen uygulamaları engelle** ayarının etkinleştirilmesini gerektirir. Bu uyumluluk ilkesini yalnızca cihazlara dışarıdan Android uygulaması yüklemiyorsanız zorunlu kılın.

  Android Kurumsal cihazları bilinmeyen kaynaklardan yüklemeyi her zaman kısıtladığından, bu ayarı yapılandırmanız gerekmez.

- **Şirket portalı uygulaması çalışma zamanı bütünlüğü**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -Şirket portalı uygulamanın, aşağıdaki tüm gereksinimleri karşıladığından emin olmak *için gerektir ' i seçin:*
    - Varsayılan çalışma zamanı ortamı yüklü
    - Doğru şekilde imzalanmış
    - Hata ayıklama modunda değil
    - Bilinen bir kaynaktan yüklenmiş

- **Cihazda USB hata ayıklamayı engelle**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Engelle** -cihazların USB hata ayıklama özelliğini kullanmasını engelleyin.  

  Android Kurumsal cihazlarında USB hata ayıklama zaten devre dışı olduğundan bu ayarı yapılandırmanız gerekmez.

- **En düşük güvenlik düzeltme eki düzeyi**  
  Bir cihazda olabilecek en eski güvenlik düzeltme eki düzeyini seçin. Bu yama düzeyinin altındaki cihazlar uyumsuz kabul edilir. Tarihin YYYY-AA-GG biçiminde girilmesi gerekir.

  *Varsayılan olarak, bir tarih yapılandırılmaz*.

## <a name="next-steps"></a>Sonraki adımlar

- [Uyumlu olmayan cihazlara uygulanacak eylemleri ekleyin](actions-for-noncompliance.md) ve [ilkeleri filtrelemek için kapsam etiketlerini kullanın](../fundamentals/scope-tags.md).
- [Uyumluluk ilkelerinizi izleyin](compliance-policy-monitor.md).
- Bkz. [Android cihazları için uyumluluk ilkesi ayarları](compliance-policy-create-android.md).
