---
title: Microsoft Intune-Azure 'da e-posta profillerinin sorunlarını giderme | Microsoft Docs
description: Yinelenen e-posta profilleri ve Samsung KNOX Standard Android cihazlarda hatalar da dahil olmak üzere Microsoft Intune içindeki e-posta profilleriyle ilgili yaygın sorunlar ve çözümleri görün.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d011d6111ede4bb5879e53e771d20b792bf00d3
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995135"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Microsoft Intune 'daki e-posta profilleriyle ilgili yaygın sorunlar ve çözümler

Bazı genel e-posta profili sorunlarını gözden geçirin ve bunları nasıl giderebileceğiniz ve giderebilirim.

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>Kullanıcıların parolasını girmesi için sürekli olarak istenir

Kullanıcıların e-posta profili için parolasını girmesi sürekli olarak istenir. Kullanıcı kimliğini doğrulamak ve yetkilendirmek için sertifikalar kullanılıyorsa, tüm Sertifika profillerinin atamalarını denetleyin. Genellikle, bu sertifika profilleri, cihaz gruplarına değil, Kullanıcı gruplarına atanır. Sertifika profillerinden biri bir kullanıcıya hedeflenmemişse, Intune e-posta profilini dağıtmayı yeniden denemeye devam eder.

E-posta profili zinciri Kullanıcı gruplarına atanırsa, sertifika profillerinizin da Kullanıcı gruplarına atandığından emin olun.

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>Cihaz gruplarına dağıtılan profiller hataları ve gecikme süresini gösterir

E-posta profilleri genellikle kullanıcı gruplarına atanır. Cihaz gruplarına atandıklarında bazı durumlar olabilir.

- Örneğin, aygıtlara değil yalnızca Surface cihazlarına sertifika tabanlı bir e-posta profili dağıtmak istiyorsunuz. Bu senaryoda, cihaz grupları anlamlı hale gelebilir. Bu cihazların uyumsuz olarak gösterileceğini, hata döndürebileceklerini ve e-posta profillerinizi hemen alamıyoruz olabileceğini öğrenin.

  Bu örnekte, e-posta profilini oluşturur ve profili cihaz gruplarına atarsınız. Cihaz yeniden başlatılır ve Kullanıcı oturum açmadan önce bir gecikme vardır. Bu gecikme sırasında, Kullanıcı gruplarına atanan PKCS sertifika profiliniz dağıtılır. Henüz Kullanıcı olmadığından, PKCS sertifika profili cihazın uyumlu olmasına neden olur. Olay Görüntüleyicisi cihazdaki hataları da gösterebilir.

  Uyumluluk sağlamak için Kullanıcı cihazda oturum açar ve ilkeleri almak için Intune ile eşitlenir. Kullanıcılar el ile yeniden eşitleme yapabilir veya bir sonraki eşitlemeyi bekleyebilir.

- Örneğin, dinamik grupları kullanıyorsunuz. Azure AD dinamik grupları hemen güncelleştirmezse, bu cihazlar uyumlu değil olarak gösterilebilir.

Bu senaryolarda, cihaz gruplarını kullanmak için daha fazla önemli olup olmadığını veya tüm ilkeleri uyumlu olarak göstermek için daha fazla önemli olduğuna karar verirsiniz.

## <a name="device-already-has-an-email-profile-installed"></a>Cihazda zaten yüklü bir e-posta profili var

Kullanıcılar Intune 'A veya MDM Microsoft 365 kaydedilmeden önce bir e-posta profili oluşturmazsa, Intune tarafından dağıtılan e-posta profili beklendiği gibi çalışmayabilir:

- **iOS/ıpados**: Intune, ana bilgisayar adı ve e-posta adresine dayalı mevcut, yinelenen bir e-posta profili Kullanıcı tarafından oluşturulan e-posta profili, Intune tarafından oluşturulan profilin dağıtımını engeller. Bu senaryo, iOS/ıpados kullanıcıları tipik olarak bir e-posta profili oluştururken ve ardından kaydolmasına neden olan yaygın bir sorundur. Şirket Portalı uygulama, kullanıcının uyumlu olmadığını ve kullanıcıdan e-posta profilini kaldırmasını isteyebilir.

  Intune profilinin dağıtılması için kullanıcının e-posta profilini kaldırması gerekir. Bu sorunu engellemek için kullanıcılarınıza kaydolmasını ve Intune 'un e-posta profilini dağıtmasına izin vermesini isteyin. Ardından, kullanıcılar e-posta profilini oluşturabilir.

- **Windows**: Intune, konak adına ve e-posta adresine bağlı olarak var olan ve yinelenen bir e-posta profili olduğunu algılar. Intune kullanıcı tarafından oluşturulmuş, var olan e-posta profilinin üzerine yazar.

- **Samsung KNOX Standard**: Intune, e-posta adresini temel alan yinelenen bir e-posta hesabı tanımlar ve Intune profiliyle üzerine yazar. Kullanıcı bu hesabı yapılandırırsa, Intune profili tarafından yeniden yazılır. Bu davranış, hesap yapılandırması geçersiz kılınmasına neden olan kullanıcıya bazı karışıklıklara neden olabilir.

Samsung KNOX, profili tanımlamak için konak adı kullanmaz. Farklı konaklarda aynı e-posta adresine dağıtmak üzere birden çok e-posta profili oluşturmanıza gerek kalmaz, birbirlerinin üzerine yazılır.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>KNOX Standard cihazı için 0x87D1FDE8 hatası

**Sorun**: farklı Android cıhazlarda Samsung KNOX Standard için bir Exchange Active Sync e-posta profili oluşturup dağıttıktan sonra, cihazın Özellikler > Ilkesi sekmesinde **0X87d1fde8** veya **düzeltme başarısız** hatası gösterilir.

Samsung KNOX için EAS profili yapılandırmanızı ve kaynak ilkeyi gözden geçirin. Samsung Notes eşitleme seçeneği artık desteklenmiyor ve bu seçenek profilinizde seçilmemelidir. Cihazların ilkeyi işlemek için yeterli zamana sahip olduğundan emin olun, 24 saate kadar.

## <a name="unable-to-send-images-from--email-account"></a>E-posta hesabından resim gönderilemedi

E-posta hesapları otomatik olarak yapılandırılmış kullanıcılar, cihazlarından resim veya resim gönderemez. Bu senaryo, **üçüncü taraf uygulamalardan e-posta gönderilmesine Izin ver** etkinleştirilmemişse gerçekleşebilir.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profillerini**seçin.
3. E-posta profilinizi > **Özellikler**  >  **ayarları**' nı seçin.
4. **Etkinleştirmek**için **üçüncü taraf uygulamalardan e-posta gönderilmesine izin ver** ayarını belirleyin.

## <a name="next-steps"></a>Sonraki adımlar

[Microsoft 'un destek yardımına](../fundamentals/get-support.md)ulaşın veya [topluluk forumlarını](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune)kullanın.
