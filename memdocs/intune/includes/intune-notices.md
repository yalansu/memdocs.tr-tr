---
title: dosya dahil etme
description: dosya dahil etme
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/10/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 7027eac119ef36adfdb9a0057a74d276696620b3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820078"
---
Bu bildirimler, gelecekteki Intune değişiklik ve özelliklerine hazırlanmanıza yardımcı olabilecek önemli bilgiler sağlar.

### <a name="microsoft-intune-ends-support-for-windows-phone-81-and-windows-10-mobile---3544938-3544909---"></a>Microsoft Intune Windows Phone 8,1 ve Windows 10 Mobile desteğini sonlandırır<!-- 3544938, 3544909 -->
Windows Phone 8,1 için Microsoft temel desteği 2017 Temmuz 'da sona erdi ve genişletilmiş destek, Haziran 2019 ' de sona erdi. Windows Phone 8,1 için Şirket Portalı uygulaması, 2017 ' den bu yana bir moda sahip. Ayrıca, Microsoft Intune Windows Phone 8,1 ' de 20 Şubat 2020 ' de desteği sona ermiştir. 

Windows 10 Mobile için Microsoft temel desteği Aralık 2019 ' de sona erdi. Destek bildiriminde bahsedildiği gibi, Windows 10 Mobile kullanıcıları artık yeni güvenlik güncelleştirmeleri, güvenlikle ilgili olmayan düzeltmeler, ücretsiz yardımlı destek seçenekleri veya Microsoft 'tan çevrimiçi teknik içerik güncelleştirmeleri almaya uygun olmayacaktır. Microsoft Intune, tüm mobil işletim sistemi desteğine bağlı olarak, Windows 10 Mobile uygulaması ve 10 Ağustos 2020 ' de Windows 10 Mobile Işletim sistemi için Şirket Portalı desteğini sonlandırır.

10 Ağustos 'tan itibaren, Windows Phone 8,1 ve Windows 10 Mobile cihazlarının kayıtları başarısız olur ve Windows mobil profil türleri Intune kullanıcı arabiriminden kaldırılır. Zaten kayıtlı cihazlar artık Intune hizmetini iade etmeyecektir ve cihaz ve ilke verilerini silecağız.

### <a name="end-of-support-for-legacy-pc-management"></a>Eski PC yönetimi için destek sonu

Eski PC yönetimi, 15 Ekim 2020 ' de destek altına geçiyor. Cihazları Windows 10 ' a yükseltin ve Intune tarafından yönetilmek üzere bunları mobil cihaz yönetimi (MDM) cihazları olarak yeniden kaydedin.

[Daha fazla bilgi edinin](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>Tüm Intune yöneti, Microsoft Endpoint Manager yönetim merkezine gidin
MC208118 son Mart sürümünde, Microsoft Endpoint Manager için yeni ve basit bir URL sunuyoruz – Intune yönetimi: [https://endpoint.microsoft.com](https://endpoint.microsoft.com) . Microsoft Uç Nokta Yöneticisi, Microsoft Intune ve Configuration Manager içeren Birleşik bir platformdur. **1 ağustos 2020**' den itibaren, ' de Intune yönetimini kaldıracağız [https://portal.azure.com](https://portal.azure.com) ve bunun yerine [https://endpoint.microsoft.com](https://endpoint.microsoft.com) tüm uç nokta yönetiminiz için kullanmanızı öneririz. 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>Android Cihaz Yöneticisi desteğini azaltma<!--7371518-->
Android Cihaz Yöneticisi yönetimi, Android 2,2 ' de Android cihazlarını yönetmenin bir yolu olarak yayımlanmıştır. Daha sonra Android 5 ' ten itibaren, [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 'ın daha modern yönetim çerçevesi yayımlanmıştır (Google Mobile Services 'e güvenilir bir şekilde bağlanabilme cihazları için). Google, yeni Android sürümlerindeki yönetim desteğini azaltarak Cihaz Yöneticisi yönetiminden teşvik.

#### <a name="how-does-this-affect-me"></a>Bu değişiklik beni nasıl etkileyecek?
Google tarafından sunulan bu değişiklikler nedeniyle, 2020 Ekim 'de, etkilenen cihaz yönetici tarafından yönetilen cihazlarda artık kapsamlı yönetim özelliklerine sahip olmayacaktır. 

> [!NOTE]
> Bu tarih daha önce 2020 dördüncü çeyrekte, ancak [Google 'daki en son bilgilere](https://www.blog.google/products/android-enterprise/da-migration/)göre taşınmıştır.

##### <a name="device-types-that-will-be-impacted"></a>Etkilenecek cihaz türleri
Azalan Cihaz Yöneticisi desteğinden etkilenecek cihazlar aşağıdaki üç koşulun uygulandığı olanlardır:
- Cihaz Yöneticisi yönetimine kaydolmuş.
- Android 10 veya üstünü çalıştırma.
- Samsung cihazı değil.

Cihazlar aşağıdakilerden biri olursa etkilenmeyecektir:
- Cihaz yönetici yönetimine kaydolmadı.
- Android 10 ' un altında Android sürümü çalıştırma.
- Samsung cihazları. Bu zaman diliminde, Intune 'un Knox platformuyla tümleştirilmesi aracılığıyla genişletilmiş destek sağlandığı için Samsung KNOX cihazları etkilenmez. Bu, Samsung cihazları için Cihaz Yöneticisi yönetiminin kapatılmasını planlamak için ek bir zaman sağlar.

##### <a name="settings-that-will-be-impacted"></a>Etkilenecek ayarlar
[Google 'ın azaltılmış cihaz yöneticisi desteği](https://developers.google.com/android/work/device-admin-deprecation) , bu ayarların yapılandırmasının etkilenen cihazlara uygulanmasını önler.

###### <a name="configuration-profile-device-restriction-settings"></a>Yapılandırma profili cihaz kısıtlama ayarları

- **Kamerayı** engelle
- **Minimum parola uzunluğunu** ayarla
- **Cihaz silinmeden önceki oturum açma hatalarının sayısını** ayarla (parola kümesi olmayan cihazlarda uygulanmayacak, ancak parola içeren cihazlara uygulanacaktır)
- **Parola süre sonu (gün)** ayarla
- **Gerekli parola türünü** ayarla
- **Önceki parolaların kullanımını engelle**
- **Akıllı kilit ve diğer güven aracılarını** engelle

###### <a name="compliance-policy-settings"></a>Uyumluluk ilkesi ayarları

- **Gerekli parola türünü** ayarla
- **Minimum parola uzunluğunu** ayarla
- **Parolanın süresi dolana kadar geçen gün sayısını** ayarla
- **Yeniden kullanmayı engellemek için önceki parolaların sayısını** ayarla


![Android uyumluluk ilkesi sayfasının ekran ucu](../fundamentals/media/notices/android-compliance-settings.png)

###### <a name="additional-impacts-based-on-android-os-version"></a>Android işletim sistemi sürümüne dayalı ek etkiler

**Android 10**: Android 10 ve üzeri çalıştıran tüm cihaz yönetici tarafından yönetilen cihazlar (Samsung dahil) Için, Google Şirket portalı cihaz kimliği bilgilerine erişmek için cihaz yönetici yönetim aracılarıyla sınırlı değildir. Bu kısıtlama, bir cihaz Android 10 veya sonraki bir sürüme güncelleştirildikten sonra aşağıdaki Intune özelliklerini etkiler:
- VPN için ağ erişim denetimi artık çalışmayacak
- Cihazları bir ıMEı veya seri numarası ile şirkete ait olarak tanımlamak cihazları şirkete ait olarak otomatik olarak işaretlemez
- IMEı ve seri numarası artık Intune 'da BT yöneticileri için görünür olmayacaktır

**Android 11**: Cihaz yönetici tarafından yönetilen cihazlarda etkiye neden olup olmadığını değerlendirmek için en son Geliştirici Beta sürümünde Android 11 desteğini test ediyoruz.

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>Etkilenen cihazlarda etkilenen ayarların Kullanıcı deneyimi

Etkilenen yapılandırma ayarları:
- Ayarları uygulanmış olan zaten kayıtlı cihazlar için, etkilenen yapılandırma ayarları zorlanmaya devam eder.
- Yeni kaydedilen cihazlar, yeni atanan ayarlar ve güncelleştirilmiş ayarlar için etkilenen yapılandırma ayarları zorlanmaz (ancak diğer tüm yapılandırma ayarları yine de zorlanır).

Etkilenen uyumluluk ayarları:
- Ayarları uygulanmış olan zaten kayıtlı olan cihazlarda, etkilenen uyumluluk ayarları "cihaz ayarlarını güncelleştirme" sayfasında uyumsuzluk nedeniyle yine de görünür, cihazın uyumsuz olacağı ve parola gereksinimleri Ayarlar uygulamasında zorlanacaktır.
- Yeni kaydedilen cihazlar, yeni atanan ayarlar ve güncelleştirilmiş ayarlar için, etkilenen uyumluluk ayarları "cihaz ayarlarını güncelleştirme" sayfasında uyumsuzluğa neden olmaya devam eder ve cihaz uyumsuz olacaktır, ancak Ayarlar uygulamasında daha sıkı parola gereksinimleri zorlanmaz.

#### <a name="cause-of-impact"></a>Etki nedeni 
Cihazlar 2020 Ekim ayının başında etkilenecektir. Bu sırada, Şirket Portalı API hedefini, 28 düzeyinden düzey 29 düzeyine ([Google 'ın gerektirdiği gibi](https://www.blog.google/products/android-enterprise/da-migration/)) artıracak Şirket portalı bir uygulama güncelleştirmesi olacaktır. 

Bu noktada, Kullanıcı bu eylemleri tamamladıktan sonra, Samsung tarafından üretilmediği Cihaz Yöneticisi tarafından yönetilen cihazlar etkilenecektir:
- Android 10 veya sonraki sürümleri için güncelleştirmeler.
- Şirket Portalı uygulamasını, API düzeyi 29 ' i hedefleyen sürüme güncelleştirir.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Bu değişikliğe hazırlanmak için ne yapmam gerek?
2020 Ekim 'de gerçekleştirilen işlevsellikten kaçınmak için şunları yapmanızı öneririz:
- **Yeni**kayıtlar: [Android kurumsal](../enrollment/connect-intune-android-enterprise.md) yönetimine yeni cihazlar ekleme (varsa) ve/veya [Uygulama koruma ilkeleri](../apps/app-protection-policies.md). Cihaz Yöneticisi yönetimine yeni cihaz ekleme kullanmaktan kaçının. 
- **Daha önce kaydedilen cihazlar**: Cihaz yönetici tarafından yönetilen bir cihaz Android 10 veya üzerini çalıştırıyorsa ya da Android 10 veya sonraki bir sürüme (özellikle bir Samsung cihaz değilse) güncelleştirebilir, Cihaz Yöneticisi yönetiminin dışına [Android kurumsal](../enrollment/connect-intune-android-enterprise.md) yönetim ve/veya [Uygulama koruma ilkelerine](../apps/app-protection-policies.md)taşıyın. [Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşımak](../enrollment/android-move-device-admin-work-profile.md)için kolaylaştırılmış akıştan yararlanabilirsiniz.

#### <a name="additional-information"></a>Ek bilgiler
- [Android cihazlarını cihaz yöneticisinden iş profili yönetimine taşıma](../enrollment/android-move-device-admin-work-profile.md)
- [Android Kurumsal iş profili cihazların kaydını ayarlama](../enrollment/android-work-profile-enroll.md)
- [Android Kurumsal ayrılmış cihazlarının kaydını ayarlama](../enrollment/android-kiosk-enroll.md)
- [Android kurumsal tam olarak yönetilen cihazların kaydını ayarlama](../enrollment/android-fully-managed-enroll.md)
- [Uygulama koruma ilkeleri atama ilkesi oluşturma](../apps/app-protection-policies.md)
- [Intune 'u Google Mobile Services olmayan ortamlarda kullanma](../apps/manage-without-gms.md)
- [Android kurumsal cihazlarda uygulama koruma ilkelerini ve iş profillerini anlama](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [Google 'ın Cihaz Yöneticisi kullanımdan kaldırılması hakkında bilmeniz gerekenler hakkında](https://www.blog.google/products/android-enterprise/da-migration/)
- [Google 'ın cihaz yöneticisinden Android kuruluşa geçiş kılavuzu](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google 'ın kullanım dışı Cihaz Yöneticisi API 'Leri belgeleri](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>Değişiklik planı: Apple 'ın iOS/ıpados için otomatik cihaz kaydına yönelik Intune kayıt akışı güncelleştirmesi
Temmuz Şirket Portalı sürümünde, Apple 'ın otomatik cihaz kaydı (eski adıyla DEP) için iOS/ıpados kayıt akışını değiştireceksiniz. Kayıt akışı değişikliğine yalnızca "Kullanıcı benzeşimi ile kaydetme" akışı sırasında karşılaşıldı. Daha önce, "Install Şirket Portalı" öğesini yapılandırmanızın bir parçası olarak "Hayır" olarak ayarlarsanız, kullanıcılar Şirket Portalı uygulamayı mağazadan yüklemeye devam edebilir ve kullanıcının uygun seri numarasına eklemesi için kayıt tetikleyebiliyordu. Yakında bu Şirket Portalı piyasaya çıkmasıyla ilgili seri numarası onay ekranını kaldıracağız. Bunun yerine, kullanıcıların başarıyla kayıt yapabilmesi veya yapılandırmanızın bir parçası olarak "Install Şirket Portalı" ayarını "Evet" olarak ayarlayabilmesi için Şirket Portalı birlikte göndermek üzere ilgili bir uygulama yapılandırma ilkesi oluşturmanız gerekir. 
 - Daha fazla bilgi için [buraya](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629) gönderin bölümüne bakın.
