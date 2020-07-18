---
title: Cihazınızı kaydederken şirketiniz hangi bilgileri görebilir?
description: BT'nin yönetilen cihazınızda ne görüp göremeyeceğini açıklar.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/11/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: bc3ff7b10d3b0ae5779db26fae711bc335c8ec62
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461683"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>Cihazımı kaydettiğimde kuruluşum hangi bilgileri görebilir?

Bir cihazı Microsoft Intune’a kaydettiğinizde kuruluşunuz kişisel bilgilerinizi göremez. Bir cihaz kaydettiğinizde kuruluşunuza cihazınızdaki cihaz modeli ve seri numarası gibi bazı bilgileri görüntüleme izni vermiş olursunuz. Kuruluşunuz, cihazdaki şirket bilgilerini korumaya yardımcı olması için bu bilgileri kullanır.

**Kuruluşunuzun asla göremeyeceği şeyler:**

- Arama ve web tarama geçmişi
- E-posta ve kısa mesajlar
- Kişiler
- Takvim
- Parolalar
- Fotoğraflar uygulamasında veya film rulosunda yer alanları da içeren resimler
- Dosyalar
- İş profili olan şirkete ait cihazlarda, kişisel profilinizde bulunan uygulamalar ve veriler için. 

**Kuruluşunuzun her zaman görebileceği şeyler:**

- Google Pixel gibi cihaz modeli
- Cihaz üreticisi, örneğin Microsoft
- İşletim sistemi ve sürümü, örneğin iOS 12.0.1
- Uygulama envanteri ve Microsoft Word gibi uygulama adları. Kişisel cihazlarda, kuruluşunuz yalnızca yönetilen uygulama envanterinizi görebilir. Şirkete ait tam olarak yönetilen ve ayrılmış cihazlarda, kuruluşunuz tüm uygulama envanterinizi görebilir. Bir iş profili olan şirkete ait cihazlarda, kuruluşunuz yalnızca iş profilinizde uygulama envanterini görebilir.
- Cihaz sahibi
- Cihaz adı
- Cihaz seri numarası
- IMEI

 > [!NOTE]
 > Android kurumsal tam yönetilen ve ayrılmış cihazlarda, tüm uygulama envanterini göremezsiniz.
 
 > [!NOTE]
 > Uygulama, aşağıdaki yollarla yüklendiğinde **yönetilen uygulama** olarak kabul edilir:
 > 1. Bir Kullanıcı, Intune Yöneticisi tarafından **kullanılabilir** olarak yayımlandıktan sonra uygulamayı şirket portalı uygulamasından yüklerse.
 > 2. Uygulama, Intune Yöneticisi tarafından **gerekli** olduğu gibi yayımlanır ve cihaza yüklenir. 
 >
 > Kuruluşunuzdaki bir BT yöneticisiyseniz veya destek sorumlusu varsa ve Intune 'da uygulama yönetimi hakkında daha fazla bilgi istiyorsanız bkz. [yönetilmeyen uygulamaların, yönetilen uygulamaların ve Mam uygulamaların yeteneklerini anlama](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164).
    
**Kuruluşunuzun görme olasılığı olan şeyler:**

- Telefon numarası: şirkete ait cihazlar Için, tam telefon numaranız görünebilirler. Kişisel cihazlarda ise numaranızın yalnızca son dört hanesi kuruluşunuz tarafından görülebilir. Her bir aygıtın sahiplik türünü, **cihaz ayrıntıları** sayfasında görebilirsiniz.
- Cihaz depolama alanı: Gerekli bir uygulamayı yükleyemiyorsanız kuruluşunuz, yeterli alan olup olmadığını anlamak için cihazınızın depolama alanına bakabilir.  
- Konum: şirkete ait cihazlarda, kuruluşunuz kayıp bir cihazın konumunu görebilir. Şirkete ait cihazlar için, kayıp, denetimli bir iOS cihazı bulmaya çalışmadıkça kuruluşunuz hiçbir şekilde cihaz konumunu göremez. Denetimli cihazlar hakkında daha fazla bilgi edinmek için [Apple iOS belgelerini](https://go.microsoft.com/fwlink/?linkid=853816) ziyaret edin.  
- Uygulama envanteri ayrıntıları: Kuruluşunuz mobil tehdit savunması kullanıyorsa, iOS cihazınızda bulunan uygulamalarla ilgili ayrıntıları görüntüleyebilecektir. [Mobil Tehdit Savunması](set-up-mobile-threat-defense.md) hakkında daha fazla bilgi edinin. Aksi halde, kişisel cihazlarda kuruluşunuz yalnızca yönetilen uygulama envanterinizi görebilir. Şirkete ait cihazlar için kuruluşunuz tüm uygulama envanterinizi görebilir.
- Ağ bilgisi: Android cihazlar için ağ bağlantılarıyla ilgili bazı bilgiler kuruluşunuzun destek birimi tarafından görülebilir. Örneğin kuruluşunuz cihazların belli bir bina içerisinde kalmasını gerektiriyorsa cihazınız, bağlı olduğu şebekeyi tanımlar. 
