---
title: Microsoft Intune 'de Android kurumsal cihazlarda sorun giderme
description: Intune 'A Android cihazları kaydettiğinizde en yaygın sorunların giderilmesi için öneriler.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/25/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f659197c8c1f9dac3f29c89f5c7676d1ae3a3f09
ms.sourcegitcommit: 81f6b4cac6c991d34bc864f950c82e5b57e906c3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90779570"
---
# <a name="troubleshoot-android-enterprise-device-problems-in-microsoft-intune"></a>Microsoft Intune 'de Android kurumsal cihaz sorunlarını giderme

Bu makale Intune yöneticilerinin Intune 'daki Android Kurumsal cihazları ile ilgili sorunları anlamalarına ve sorunlarını gidermelerine yardımcı olur.

## <a name="apps-on-android-enterprise-devices"></a>Android kurumsal cihazlarda uygulamalar

### <a name="managed-google-play-apps-that-arent-deployed-through-intune-are-displayed-in-the-work-profile"></a>Intune aracılığıyla dağıtılmamış yönetilen Google Play uygulamaları iş profilinde görüntülenir
Sistem uygulamaları, iş profili oluşturulduğu sırada cihaz OEM tarafından iş profilinde etkinleştirilebilir. Bu, MDM sağlayıcısı tarafından denetlenmez.

Sorunu gidermek için şu adımları izleyin:

  1. Şirket Portalı günlüklerini toplayın.
  2. İş profilinde beklenmedik şekilde görünen uygulamaları unutmayın.
  3. Cihazın Intune kaydını kaldırıp Şirket Portalı kaldırın.
  4. Test için EMM olmadan bir iş profili oluşturulmasına izin veren [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) uygulamasını yükler.
  5. Cihazda bir iş profili oluşturmak için [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) içindeki yönergeleri izleyin.
  6. İş profilinde görünen uygulamaları gözden geçirin. 
  7. Test DPC uygulamasında aynı uygulamalar gösteriliyorsa, uygulamalar bu cihaz için OEM tarafından beklenir.

### <a name="unapproved-managed-google-play-for-work-store-apps-arent-being-removed-from-the-client-apps-page-in-intune"></a>Iş Mağazası uygulamaları için onaylanmamış yönetilen Google Play, Intune 'daki Istemci uygulamaları sayfasından kaldırılmaz
Bu beklenen bir davranıştır.

### <a name="managed-google-play-apps-arent-being-reported-under-the-discovered-apps-blade-in-the-intune-portal"></a>Yönetilen Google Play uygulamalar, Intune portalındaki bulunan uygulamalar dikey penceresinde bildirilmiyor
Bu beklenen bir davranıştır. Yalnızca Iş profilinde yüklü olan sistem uygulamaları, bulunan uygulamalar dikey penceresinde envantere kaydedilir. Yüklü yönetilen Google Play uygulamalarını görmek için **yönetilen uygulamalar** dikey penceresini kullanın.

### <a name="are-web-applications-supported-for-work-profile-enrolled-devices"></a>İş profili kayıtlı cihazlar için desteklenen Web uygulamaları var mı?
Evet. Daha fazla bilgi için bkz. [yönetilen Google Play web bağlantıları](../apps/apps-add-android-for-work.md#managed-google-play-web-links)

## <a name="device-management"></a>Cihaz yönetimi

### <a name="file-path-internal-storageandroiddatacommicrosoftwindowsintunecompanyportalfiles-missing-on-work-profile-enrolled-devices"></a>Dosya yolu Iç depolama/Android/Data. com. Microsoft. windowsinayarla. CompanyPortal/dosyalar eksik iş profili kayıtlı cihazlarda yok

  **Cevap**: Bu beklenen davranıştır. Bu yol yalnızca Cihaz Yöneticisi (eski Android kayıt) senaryosu için oluşturulur.

  Şirket Portalı günlüklerini toplamak için aşağıdaki adımları izleyin:

  1. Rozet ile şirket portalı uygulamasında, **menü**  >  **Help**  >  **e-posta desteği**' ne dokunun, ardından **e-posta gönder & karşıya yükleme günlükleri**' ne dokunun. 
  2. **Yardım Isteği göndermek**isteyip istemediğiniz sorulduğunda, e-posta uygulamalarından birini seçin.
  3. BT yöneticinize, Microsoft ürün desteği 'ne sağlanacak bir olay KIMLIĞI ile bir e-posta oluşturulur.

### <a name="managed-google-play-last-sync-time--hasnt-been-updated-in-days"></a>Yönetilen Google Play son eşitleme saati, gün cinsinden güncelleştirilmedi
Bu beklenen bir davranıştır. Eşitleme yalnızca el ile yaptığınız zaman tetiklenir.

### <a name="encryption-is-required-when-a-device-is-enrolled-can-it-be-turned-off"></a>Bir cihaz kaydolduğunda şifreleme gereklidir. Kapatılabilir mi?
Hayır, Google, cihazın bir iş profili oluşturmak için şifrelenmesini gerektirir. 

### <a name="samsung-devices-are-blocking-the-use-of-third-party-keyboards-like-swiftkey"></a>Samsung cihazlar, SwiftKey gibi üçüncü taraf klavyeleri kullanmayı engelliyor
Samsung, Android 8.0 + cihazlarında bu kısıtlamayı zorlamaya başladı. Microsoft şu anda bu sorun üzerinde Samsung ile çalışmaktadır ve kullanılabilir olduğunda yeni bilgiler göndermeyecektir.

## <a name="remote-actions"></a>Uzak eylemler

### <a name="wipe-factory-reset-option-isnt-available-for-work-profile-enrolled-device"></a>Sil (fabrika sıfırlaması) seçeneği, iş profili kayıtlı cihazı için kullanılamaz
Bu beklenen bir davranıştır. İş profili senaryosunda, MDM sağlayıcısı cihaz üzerinde tam denetime sahip değildir. Kullanılabilir tek seçenek, tüm iş profilini ve tüm içeriğini kaldıran (şirket verilerini Kaldır) devre dışı.

Silme işlemi, [Android kurumsal şirkete ait iş profili cihazlarında](android-corporate-owned-work-profile-enroll.md)desteklenir.

### <a name="is-device-passcode-reset-supported"></a>Cihaz geçiş kodu sıfırlaması destekleniyor mu?
İş profili kayıtlı cihazlar için, şu durumlarda yalnızca Android 8,0 veya üzeri cihazlarda iş profili geçiş kodunu sıfırlayabilirsiniz:
- iş profili geçiş kodu yönetiliyor
- Son Kullanıcı onu sıfırlamanıza izin verildi.

Adanmış cihazlar (COSU) ve tam olarak yönetilen cihaz geçiş kodu sıfırlaması desteklenir.

## <a name="duo-devices"></a>Duo cihazlar

### <a name="company-portal-not-prompting-users-to-enroll"></a>Şirket Portalı kullanıcıların kaydolmasını isteme
Bazı durumlarda, kullanıcılar Şirket Portalı uygulamasını başlattığında kayıt denetim listesi beklendiği gibi görüntülenmeyebilir.

Kullanıcılar kayıt denetim listesini görmemişse, Şirket Portalı uygulamasının sağ üst köşesindeki bildirim zili ' na dokunarak ve kayıt denetim listesini getirecek olan Bildirime dokunarak, her zaman bu sayfaya gidebilirler.

### <a name="users-unable-to-find-the-microsoft-launcher-app"></a>Kullanıcılar Microsoft Başlatıcı uygulamasını bulamıyor
Kullanıcılar Microsoft başlatıcı uygulaması iş profilini bulamıyor veya başlatamıyor. 

Microsoft başlatıcısı uygulaması, Duo cihazlarda varsayılan Başlatıcı uygulamasıdır, bu nedenle uygulama simgesi uygulamalar listesinden ve kişisel ve iş yürütme mağazalarında gizlenir. Bu, gelecek bir güncelleştirmede düzeltilecektir.

### <a name="edge-sign-in-prompt-during-enrollment"></a>Kayıt sırasında Edge oturum açma istemi
Kayıtlı olmayan bir Kullanıcı, koşullu erişim (CA) tarafından korunan bir uygulamadaki kurumsal verilere erişmeyi denediğinde, Kullanıcı cihazını kaydetmeye kılavuzluk eder. Bu kayıt akışı sırasında, Edge uygulaması Şirket Portalı Web sitesini açmak için başlatılır. Bazı durumlarda, uç uygulama kullanıcıdan oturum açmasını isteyebilir ve kullanıcıyı kayıt akışından ayırır.

Bunu tamamen önlemek için, kullanıcıların kuruluş verilerine erişmeyi denemeden önce Şirket Portalı kaydolmalarını söyleyin. Bir Kullanıcı kaydedilmeden önce kuruluşunuzun verilerine erişmeyi denerseniz, uç kullanıcıdan oturum açmasını isterse, kayıt akışına devam etmek için Edge oturum açma adımını atlarlar. Kullanıcılar, her zaman önceden yüklenmiş Şirket Portalı uygulamasında kayıt başlatabilir.



## <a name="next-steps"></a>Sonraki adımlar

- [Intune'da cihaz kaydıyla ilgili sorunları giderme](troubleshoot-device-enrollment-in-intune.md)
- [Intune forumundan soru sorun](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Microsoft Intune destek ekibi blogunu denetleyin](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Microsoft Enterprise Mobility ve Security blogunu denetleyin](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)