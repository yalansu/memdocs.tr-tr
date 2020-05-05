---
title: Microsoft Intune - Azure’daki Android cihazı uyumluluk ilkeleri | Microsoft Docs
description: Microsoft Intune'da Android cihazlarınızda uyumluluk ayarı yaparken kullanabileceğiniz tüm ayarların bulunduğu listeyi inceleyin. Parola kurallarını ayarlayın, en düşük veya en yüksek işletim sistemi sürümünü seçin, belirli uygulamaları kısıtlayın, parolaların yeniden kullanılmasını engelleyin ve çok daha fazlasını yapın.
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
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f8cb75907befaa747ebae1718815d9722ff7085
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729224"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Intune'u kullanarak cihazları uyumlu veya uyumlu değil şeklinde işaretlemek için kullanabileceğiniz Android ayarları

Bu makalede Intune'daki Android cihazları için yapılandırabileceğiniz farklı uyumluluk ayarları listelenmekte ve anlatılmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu ayarları kullanabilir ve bu sayede kök erişim izni verilmiş (jailbreak uygulanmış) cihazları uyumlu değil olarak işaretleyebilir, izin verilen tehdit düzeyi belirleyebilir, Google Play Koruması'nı etkinleştirebilir ve çok daha fazlasını yapabilirsiniz.

Bu özellik şu platformlarda geçerlidir:

- Android cihaz yöneticisi

Intune yöneticisi olarak bu uyumluluk ayarlarını kullanarak kuruluşunuzun kaynaklarının korunmasına yardımcı olabilirsiniz. Uyumluluk ilkeleri ve işlevleri hakkında daha fazla bilgi için bkz. [Cihaz uyumluluğunu kullanmaya başlama](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Başlamadan önce

[Bir uyumluluk Ilkesi oluşturun](create-compliance-policy.md#create-the-policy). **Platform**için **Android Cihaz Yöneticisi**' ni seçin.

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

- **Cihazın makine risk puanı üzerinde veya altında olmasını gerektir**  

  Microsoft Defender ATP tarafından değerlendirilen cihazlar için izin verilen en yüksek makine risk Puanını seçin. Bu puanı aşan cihazlar uyumsuz olarak işaretlenir.
  - **Yapılandırılmadı** (*varsayılan*)
  - **Temizle**
  - **Düşük**
  - **Medium**
  - **Geniş**

## <a name="device-health"></a>Cihaz Sistem Durumu

- **Cihaz yöneticisiyle yönetilen cihazlar**  
  *Cihaz Yöneticisi* özellikleri yerine Android Enterprise.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Blok** engelleme Cihaz Yöneticisi, kullanıcılara, erişimi yeniden kazanmak Için Android kurumsal iş profili yönetimine geçiş yapmak üzere rehberlik edecektir.

- **Kökü belirtilmiş cihazlar**  
  Kök cihazların şirket erişimine sahip olmasını engelle. (Bu uyumluluk denetimi, Android 4,0 ve üzeri için desteklenir.)

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Block** -root (Jailbreak uygulanmış) cihazlarını uyumsuz olarak işaretle.

- **Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir**  
  Bu ayarı, bağlı bir mobil tehdit savunma hizmetinden bir uyumluluk koşulu olarak risk değerlendirmesi almak için kullanın.

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Güvenli** -Bu seçenek, cihazın herhangi bir tehdit sahibi olmadığı için en güvenli seçenektir. Herhangi bir tehdit düzeyi algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Düşük** -cihaz, yalnızca düşük düzeyde tehditler varsa uyumlu olarak değerlendirilir. Daha yüksek bir tehdit düzeyi, cihazı uyumlu değil durumuna getirir.
  - **Orta** -cihazdaki mevcut tehditler düşük veya orta düzeydeyse cihaz uyumlu olarak değerlendirilir. Yüksek düzeyde tehditler algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Yüksek** -Bu seçenek en az güvenlidir ve tüm tehdit düzeylerine izin verir. Bu çözüm, yalnızca raporlama amacıyla kullanıyorsanız kullanışlı olabilir.

### <a name="google-play-protect"></a>Google Play Koruması

- **Google Play Hizmetleri yapılandırıldı**  
  Google Play hizmetleri, güvenlik güncelleştirmelerine olanak sağlar ve sertifikalı Google cihazlarında birçok güvenlik özelliği için temel düzeyde bir bağımlılıktır.

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.  
  - **Gerektir** -Google Play Services uygulamasının yüklü ve etkin olmasını gerektirir.  

- **Güncel güvenlik sağlayıcısı**

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -güncel bir güvenlik sağlayıcısının bir cihazı bilinen güvenlik açıklarına karşı koruyabilmesini gerektir.

- **Uygulamalarda tehdit taraması**

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -Android **uygulamaları doğrula** özelliğinin etkinleştirilmesini gerektirir.

  > [!NOTE]
  > Eski Android platformunda bu özellik bir uyumluluk ayarıdır. Intune yalnızca bu ayarın cihaz düzeyinde etkinleştirilip etkinleştirilmediğini denetleyebilir.

- **SafetyNet cihaz kanıtı**  
  Uyulması gereken [SafetyNet kanıtı](https://developer.android.com/training/safetynet/attestation.html) düzeyini ayarlayın. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Temel bütünlük denetimi**
  - **Temel bütünlük ve sertifikalı cihaz denetimi**

> [!NOTE]
> Uygulama koruma ilkelerini kullanarak Google Play Koruması ayarlarını yapılandırmak için bkz. [Android için Intune uygulama koruması ilkesi ayarları](../apps/app-protection-policy-settings-android.md#conditional-launch).

## <a name="device-properties"></a>Cihaz Özellikleri

### <a name="operating-system-version"></a>İşletim Sistemi Sürümü

- **En düşük işletim sistemi sürümü**  
  Bir cihaz en düşük işletim sistemi sürümü gereksinimini karşılamadığında uyumsuz olarak bildirilir. Yükseltmenin nasıl gerçekleştirileceği hakkında bilgi içeren bir bağlantı gösterilir. Son kullanıcı, cihazını yükseltmeyi seçip şirket kaynaklarına erişebilir.

  *Varsayılan olarak, sürüm yapılandırılmaz*.

- **En yüksek işletim sistemi sürümü**  
  Cihaz kuralda belirtilenden sonraki bir işletim sistemi sürümünü kullandığında, şirket kaynaklarına erişim engellenir. Kullanıcıdan BT yöneticisine başvurması istenir. Bir kural, işletim sistemi sürümüne izin verecek şekilde değiştirilene kadar bu cihaz şirket kaynaklarına erişemez.

  *Varsayılan olarak, sürüm yapılandırılmaz*.

## <a name="system-security"></a>Sistem Güvenliği

### <a name="password"></a>Parola

- **Mobil cihazların kilidini açmak için bir parola gerektir**  
  *Android 4,0 ve üzeri sürümlerde veya KNOX 4,0 ve üzeri sürümlerde desteklenir.*

  Bu ayar, kullanıcılara mobil cihazlarındaki bilgilere erişim verilmeden önce bu kullanıcılardan parola istenip istenmeyeceğini belirtir. Önerilen değer: gerektir  

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -kullanıcıların cihazına erişebilmeleri için önce bir parola girmesi gerekir.

- **Gerekli parola türü**  
  *Android 4,0 ve üzeri sürümlerde veya KNOX 4,0 ve üzeri sürümlerde desteklenir.*

  Parolanın yalnızca sayısal karakterlerden mi yoksa sayı ve diğer karakterlerin karışımından mı oluşacağını seçin.

  - **Cihaz varsayılanı** -parola uyumluluğunu değerlendirmek Için, **cihaz varsayılanı**dışında bir parola gücü seçtiğinizden emin olun.
  - **Düşük güvenlik biyometriği**
  - **En az sayısal**
  - Ya da gibi sayısal karmaşık yinelenen veya ardışık sayıların kullanımına izin verilmez. **Numeric complex** `1111` `1234`
  - **En az alfabetik**
  - **En az alfasayısal**
  - **Simgelerle en az alfasayısal**

  Bu ayarın yapılandırmasına bağlı olarak, aşağıdaki seçeneklerden biri veya birkaçı kullanılabilir:

  - **Minimum parola uzunluğu**  
    *Android 4,0 ve üzeri sürümlerde veya KNOX 4,0 ve üzeri sürümlerde desteklenir.*

    Kullanıcı parolasının sahip olması gereken minimum rakam veya karakter sayısını girin.

  - **Parola istenmeden önce geçen işlem yapılmayan dakika sayısı**  
    *Android 4,0 ve üzeri sürümlerde veya KNOX 4,0 ve üzeri sürümlerde desteklenir.*

    Kullanıcı parolasını yeniden girmeden önce boşta geçen süreyi girin. **Yapılandırılmadı** (varsayılan) seçeneğini belirtirseniz bu ayar uyumluluk veya uyumsuzluk açısından değerlendirilmez.

  - **Parolanın süresi dolana kadar geçen gün sayısı**  
  *Android 4,0 ve üzeri sürümlerde veya KNOX 4,0 ve üzeri sürümlerde desteklenir.*

  Kullanıcı parolasının süresi dolup yeni bir parola oluşturulması gerekmeden önce geçmesi gereken gün sayısını seçin.

  - **Yeniden kullanılmasını önleyen önceki parola sayısı**  
    Yeniden kullanılamayacak parolalar için bir sayı girin. Son kullanıcının daha önce kullanılmış parolalar oluşturmasını önlemek için bu ayarı kullanın. (Android 4,0 ve üzeri ya da KNOX 4,0 ve üzeri için desteklenir.)

### <a name="encryption"></a>Şifreleme

- **Cihazda veri depolamanın şifrelenmesi**  
  *Android 4,0 ve üzeri sürümlerde veya KNOX 4,0 ve üzeri sürümlerde desteklenir.*

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - , Cihazlarınızda veri depolamayı **ister** . **Mobil cihazların kilidini açmak için parola iste** ayarını seçtiğinizde cihazlar şifrelenir.

### <a name="device-security"></a>Cihaz Güvenliği

- **Bilinmeyen kaynaklardan gelen uygulamaları engelle**  
  *Android 4,0 ' de Android 7. x için desteklenir. Android 8,0 ve üzeri tarafından desteklenmez*

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Blok** - **güvenlik > bilinmeyen kaynakların** etkinleştirildiği kaynakları engelleyin (Android*4,0 üzerinden Android 7. x aracılığıyla desteklenir). Android 8,0 ve üzeri sürümlerde desteklenmez.*).

  Uygulamaları dışarıdan yüklemek için bilinmeyen kaynaklara izin verilmesi gerekir. Cihazlara dışarıdan Android uygulaması yüklemiyorsanız bu uyumluluk ilkesini etkinleştirmek için bu özelliği **Engelle** olarak ayarlayın.

  > [!IMPORTANT]
  > Dışarıdan uygulama yükleme, **Bilinmeyen kaynaklardan gelen uygulamaları engelle** ayarının etkinleştirilmesini gerektirir. Bu uyumluluk ilkesini yalnızca cihazlara dışarıdan Android uygulaması yüklemiyorsanız zorunlu kılın.

- **Şirket portalı uygulaması çalışma zamanı bütünlüğü**
  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Gerektir** -Şirket portalı uygulamanın, aşağıdaki tüm gereksinimleri karşıladığından emin olmak *için gerektir ' i seçin:*

    - Varsayılan çalışma zamanı ortamı yüklü
    - Doğru şekilde imzalanmış
    - Hata ayıklama modunda değil
    - Bilinen bir kaynaktan yüklenmiş

- **Cihazda USB hata ayıklamayı engelle**  
  *(Android 4,2 veya üzeri sürümlerde desteklenir)*

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar uyumluluk veya uyumsuzluk için değerlendirilmez.
  - **Engelle** -cihazların USB hata ayıklama özelliğini kullanmasını engelleyin.

- **En düşük güvenlik düzeltme eki düzeyi**  
  *(Android 6,0 veya üzeri sürümlerde desteklenir)*

  Bir cihazda olabilecek en eski güvenlik düzeltme eki düzeyini seçin. Bu yama düzeyinin altındaki cihazlar uyumsuz kabul edilir. Tarihin `YYYY-MM-DD` biçiminde girilmesi gerekir.

  *Varsayılan olarak, bir tarih yapılandırılmaz*.

- **Kısıtlanmış uygulamalar**  
  Kısıtlanması gereken uygulamalar için **uygulama adı** ve **uygulama paketi kimliği** ' ni girin ve ardından **Ekle**' yi seçin. Kısıtlı uygulamalardan en az birinin yüklü olduğu cihaz uyumsuz olarak işaretlenir.

## <a name="next-steps"></a>Sonraki adımlar

- [Uyumlu olmayan cihazlara uygulanacak eylemleri ekleyin](actions-for-noncompliance.md) ve [ilkeleri filtrelemek için kapsam etiketlerini kullanın](../fundamentals/scope-tags.md).
- [Uyumluluk ilkelerinizi izleyin](compliance-policy-monitor.md).
- Bkz. [Android Kurumsal cihazlar için uyumluluk ilkesi ayarları](compliance-policy-create-android-for-work.md).
