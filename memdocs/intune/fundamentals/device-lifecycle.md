---
title: Microsoft Intune MDM yaşam döngüsüne genel bakış
description: Kayıt, yapılandırma ve son olarak kullanımdan kaldırma süreçleri boyunca Intune’un cihazları yönetmenize nasıl yardımcı olduğu konusunda bilgi edinin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64e15e05ba7613b8bf2941d00a48c19292fafc90
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909763"
---
# <a name="overview-of-the-microsoft-intune-mobile-device-management-mdm-lifecycle"></a>Microsoft Intune mobil cihaz yönetimi (MDM) yaşam döngüsüne genel bakış

Yönettiğiniz tüm cihazlarda *yaşam döngüsü* adı verilen bir unsur vardır. Intune, kayıt işleminden başlanarak, yapılandırma ve korumadan tutun artık gerekli olmadığında cihazın kullanımdan kaldırılmasına kadarki süreçte bu yaşam döngüsünü yönetmenize yardımcı olabilir. İşte bir örnek: şirketiniz tarafından satın alınan bir iPad, şirketinizin onu yönetmesine izin vermek için Microsoft Intune hesabınızla kaydolmalıdır; ardından, şirketinizin sizin için yapılandırılmış olması gerekir; daha sonra, üzerinde depolanan verilerin bir kullanıcı tarafından korunması gerekir; son olarak, iPad 'e artık gerek duyulmadığında, üzerinde tüm hassas verileri [devre dışı bırakmanız veya](../remote-actions/devices-wipe.md) silmelisiniz.

![Cihaz yaşam döngüsü](./media/device-lifecycle/device-lifecycle.png "Intune cihaz yaşam döngüsü")

## <a name="enroll"></a>Kaydetme

Günümüzün mobil cihaz yönetimi (MDM) stratejileri, çeşitli telefonlar, tabletler ve bilgisayarlar (iOS/ıpados, Android, Windows ve Mac OS X) ile ilgilenir. Şirkete ait cihazlarda çoğunlukla söz konusu olduğu gibi cihazı yönetebilmeniz gerekiyorsa, ilk adım [cihaz kaydını ayarlamaktır](../enrollment/device-enrollment.md). Windows bilgisayarları da Intune’a (MDM) kaydederek veya [Intune istemci yazılımını yükleyerek](manage-windows-pcs-with-microsoft-intune.md) yönetebilirsiniz.

## <a name="configure"></a>Yapılandırma

Cihazlarınızın kaydını yaptırmak yalnızca ilk adımdır. Tüm bu Intune tekliflerinden yararlanmak, ayrıca cihazlarınızın güvenli ve şirket standartlarıyla uyumlu olduğundan emin olmak için birçok farklı ilke arasından seçim yapabilirsiniz. Bu ilkeler, yönetilen cihazların nasıl çalışacağını neredeyse her açıdan yapılandırmanıza imkan tanır. Örneğin, kullanıcılar şirket verilerini içeren cihazlarda parola kullanmalı mı? Bir parola gerektirebilirsiniz. Kurumsal Wi-Fi bağlantınız var mı? Otomatik olarak yapılandırabilirsiniz. Aşağıdaki türlerde yapılandırma seçenekleri sağlanır:

- [**Cihaz yapılandırması**](../configuration/device-profiles.md). Bu ilkeler, yönettiğiniz cihazların özelliklerini ve yeteneklerini yapılandırmanıza imkan sağlar. Örneğin, Android telefonlarında parola kullanımını gerektirebilir veya kameranın kullanımını devre dışı bırakabilirsiniz IPhone.
- [**Şirket kaynağına erişim**](../configuration/device-profiles.md). Kullanıcılarınıza kişisel cihazlarını kullanarak işlerine erişme izni verirseniz karşınıza bazı zorluklar çıkarabilir. Örneğin, şirket e-postasına erişmesi gereken tüm cihazların doğru yapılandırıldığından nasıl emin olursunuz? Kullanıcıların karmaşık ayarları bilmek zorunda kalmadan, VPN bağlantısıyla şirket ağına erişebilmelerini nasıl sağlayabilirsiniz? Intune, yönettiğiniz cihazları ortak şirket kaynaklarına erişecek şekilde otomatik olarak yapılandırarak bu yükü azaltmaya yardımcı olabilir.
- [**Windows bilgisayarı yönetim ilkeleri (Intune istemci yazılımıyla)**](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md). Windows bilgisayarlarını Intune’a kaydetmek size en kapsamlı cihaz yönetim özelliklerini getirirken, Intune Windows bilgisayarlarının yönetimini desteklemeye Intune istemci yazılımıyla devam eder. Bilgisayarlarla gerçekleştirebileceğiniz görevlerden bazıları hakkında bilgi almanız gerekiyorsa buradan başlayın.

## <a name="protect"></a>Koruma

Modern BT dünyasında cihazları yetkisiz erişime karşı korumak, en önemli görevlerinizden biridir. Cihaz yaşam döngüsünün **Yapılandırma** adımındaki öğelere ek olarak, Intune yönettiğiniz cihazları yetkisiz erişime veya kötü amaçlı saldırılara karşı korumaya yardımcı olmak için şu özellikleri sağlar:

- [**Multi-Factor Authentication**](../enrollment/multi-factor-authentication.md). Kullanıcı oturum açma işlemlerine fazladan bir kimlik doğrulama katmanı daha eklemek cihazların daha da güvenli olmasına yardım edebilir. Birçok cihaz çok faktörlü kimlik doğrulamasını destekler. Bu, kullanıcılar erişim kazanmadan önce telefonla arama veya kısa mesaj gibi ikinci bir kimlik doğrulama düzeyini gerektirir.
- [**İş Için Windows Hello ayarları**](../protect/windows-hello.md). İş İçin Microsoft Hello, kullanıcıların parolaya gerek kalmadan parmak izi gibi bir *hareket* veya Windows Hello kullanarak oturum açmalarına olanak tanıyan alternatif bir oturum açma yöntemidir.
- [**Windows bilgisayarlarını korumaya yönelik ilkeler (Intune istemci yazılımıyla)**](policies-to-protect-windows-pcs-in-microsoft-intune.md). Windows bilgisayarlarını Intune istemci yazılımını kullanarak yönetirken, yönettiğiniz bilgisayarlarda Endpoint Protection’ın, yazılım güncelleştirmelerinin ve Windows Güvenlik Duvarı’nın ayarlarını denetlemenize olanak tanıyan ilkeler sağlanır.

## <a name="retire"></a>Devre Dışı Bırakma

Cihaz kaybolduğunda veya çalındığında, değiştirilmesi gerektiğinde veya kullanıcılar başka bir pozisyona geçtiğinde, çoğunlukla cihazı [devre dışı bırakmanın veya temizlemenin](../remote-actions/device-management.md) zamanı gelmiştir. Cihazı sıfırlamak, yönetimden kaldırmak veya üzerindeki şirket verilerini temizlemek dahil olmak üzere birçok farklı yolla bunu yapabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune 'de cihaz yönetimi](../remote-actions/device-management.md) hakkında bilgi edinin