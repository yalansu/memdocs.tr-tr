---
title: İş profiliyle şirkete ait Android Kurumsal cihazları için Intune kaydını kurma
titleSuffix: Microsoft Intune
description: Intune 'da iş profiliyle Android kurumsal şirkete ait cihazları kaydetme hakkında bilgi edinin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4934115915c41d696258aa54ee8f4b7c84d1809c
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86464949"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>İş profiliyle şirkete ait Android kurumsal cihazların Intune kaydını ayarlama

İş profiline sahip Android kurumsal şirkete ait cihazlar, kurumsal ve kişisel kullanım için tasarlanan tek kullanıcı cihazlarıdır.

Son kullanıcılar çalışmalarını ve kişisel verilerini ayrı tutabilir ve kişisel verilerinin ve uygulamalarının özel kalacağından garanti edilir. Yöneticiler, aşağıdakiler dahil olmak üzere tüm cihaz için bazı ayarları ve özellikleri denetleyebilir:

- Cihaz parolası için gereksinimleri ayarlama
- Bluetooth ve veri dolaşımını denetleme
- Fabrika sıfırlama korumasını yapılandırma

Intune, iş profiliyle şirkete ait Android kurumsal cihazlara uygulama ve ayarlar dağıtmanıza yardımcı olur. Android Enterprise hakkında ayrıntılı bilgi için bkz. [Android Enterprise Requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="device-requirements"></a>Cihaz gereksinimleri

Cihazların Android kurumsal şirkete ait iş profili cihazları olarak yönetilmesi için bu gereksinimleri karşılaması gerekir:

- Android OS sürüm 8,0 ve üzeri.
- Cihazlar Android’in Google Mobile Services (GMS) bağlantısı olan bir dağıtımını çalıştırmalıdır. Cihazlarda GMS kullanılabilir olmalı ve cihazlar GMS’ye bağlanabilmelidir.

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>Android Enterprise şirkete ait iş profili cihaz yönetimini ayarlama

Android kurumsal şirkete ait iş profili cihaz yönetimini ayarlamak için aşağıdaki adımları izleyin:

1. Mobil cihazların yönetimine hazırlık olarak, yönergeler için [**Microsoft Intune**’a mobil cihaz yönetimi (MDM) yetkilisi ayarlamanız](../fundamentals/mdm-authority-set.md) gerekir. Bu öğeyi yalnızca mobil cihaz yönetimi için Intune’u ilk defa kurduğunuzda ayarlarsınız.
2. [Intune kiracı hesabınızı Yönetilen Google Play hesabınıza bağlayın](connect-intune-android-enterprise.md).
3. [Kayıt profili oluşturun.](#create-an-enrollment-profile)
4. [Bir cihaz grubu oluşturun](#create-a-device-group).
5. [Şirkete ait iş profili cihazlarını kaydedin](#enroll-the-corporate-owned-work-profile-devices).

### <a name="create-an-enrollment-profile"></a>Kayıt profili oluşturma

> [!NOTE]
> İş profiline sahip şirkete ait cihazların belirteçleri otomatik olarak sona ermeyecektir. Bir yönetici bir belirteci iptal etmeye karar verirse, onunla ilişkili profil, **Devices**  >  **Android**  >  **Android enrollment**  >  **iş profili (Önizleme) ile Android Android kayıt şirkete ait cihazlarda**gösterilmez. Hem etkin hem de etkin olmayan belirteçlerle ilişkili tüm profilleri görmek için **filtre** ' ye tıklayın ve hem "etkin" hem de "etkin olmayan" ilke durumlarının onay kutularını işaretleyin. 

Kullanıcıların şirkete ait iş profili cihazlarını kaydedebilmesi için bir kayıt profili oluşturmanız gerekir. Profil oluşturulduktan sonra size bir kayıt belirteci (rastgele dize) ve QR kodu sağlar. Cihazın Android işletim sistemi ve cihazın sürümüne bağlı olarak [ayrılmış cihazı kaydetmek](#enroll-the-corporate-owned-work-profile-devices) için belirteci veya QR kodunu kullanabilirsiniz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde oturum açın ve **cihazlar**  >  **Android**  >  **Android**  >  **iş profili (Önizleme) ile şirkete ait cihazlar**kayıt ' yi seçin.
2. **Profil oluştur** ' a tıklayın ve alanları doldurun.
    - **Ad**: Profili dinamik cihaz grubuna atarken kullanacağınız bir ad yazın.
    - **Açıklama**: profil açıklaması ekleyin (isteğe bağlı).
3. **İleri**’yi seçin.
5. İlkeyi oluşturmak için **gözden geçir + oluştur** sayfasında **Oluştur** ' u seçin.

### <a name="create-a-device-group"></a>Cihaz grubu oluşturma

Uygulama ve ilkeleri, atanmış veya dinamik cihaz gruplarına hedefleyebilirsiniz. Aşağıdaki adımları izleyerek, belirli bir kayıt profiliyle kaydedilmiş cihazları otomatik olarak doldurmak için dinamik Azure AD cihaz gruplarını yapılandırabilirsiniz:

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde oturum açın ve **gruplar**  >  **tüm gruplar**  >  **Yeni Grup**' ı seçin.
2. **Grup** dikey penceresinde gerekli alanları aşağıdaki gibi doldurun:
    - **Grup türü**: Güvenlik
    - **Grup adı**: Kullanımı kolay bir ad yazın (Fabrika 1 cihazlar gibi)
    - **Üyelik türü**: Dinamik cihaz
3. **Dinamik sorgu ekle**’yi seçin.
4. **Dinamik üyelik kuralları** dikey penceresindeki alanları aşağıdaki gibi doldurun:
    - **Dinamik üyelik kuralı ekle**: Basit kural
    - **Cihaz eklenecek konum**: enrollmentProfileName
    - Ortadaki kutuda **eşittir**' i seçin.
    - Son alana ise daha önce oluşturduğunuz kayıt profili adını girin.
    Dinamik üyelik kuralları hakkında daha fazla bilgi için bkz: [AAD grupları için dinamik üyelik kuralları](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. **Add sorgu**  >  **Oluştur**' a tıklayın.

### <a name="revoke-tokens"></a>Belirteçleri iptal et

Belirtecin/QR kodunun süresinin hemen dolmasını sağlayabilirsiniz. Bu noktadan itibaren belirteç/QR kodu kullanılabilir olmaktan çıkar. Şu durumlarda bu seçeneği kullanmak isteyebilirsiniz:
  - belirteci/QR kodunu yanlışlıkla yetkisiz taraflarla paylaşırsanız
  - tüm kayıtları tamamlayıp belirtece/QR koduna artık ihtiyaç duymazsanız

Belirteç/QR kodunun iptali, zaten kayıtlı olan cihazlar üzerinde hiçbir etkiye sahip olmayacaktır.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde oturum açın ve **cihazlar**  >  **Android**  >  **Android**  >  **iş profili (Önizleme) ile şirkete ait cihazlar**kayıt ' yi seçin.
2. Çalışmak istediğiniz profili seçin.
3. **Belirteç**’i seçin.
5. Belirteci iptal etmek için **belirteci iptal et**  >  **Evet**' i seçin.

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>Şirkete ait iş profili cihazlarını kaydetme

Kullanıcılar artık [şirkete ait iş profili cihazlarını kaydedebilir](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> **Microsoft Intune** uygulaması, şirkete ait bir iş profili cihazının kaydı sırasında otomatik olarak yüklenir.  Bu uygulama kayıt için gereklidir ve kaldırılamaz. 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>Android kurumsal şirkete ait iş profili cihazlarındaki uygulamaları yönetme

Yalnızca atama türü [gerekli olarak ayarlanmış](../apps/apps-deploy.md#assign-an-app) olan uygulamalar, Android kurumsal şirkete ait iş profili cihazlarına yüklenebilir. Uygulamalar, Android Kurumsal iş profili cihazlarında olduğu gibi Yönetilen Google Play mağazasından yüklenir.

Yönetilen cihazlarda uygulamalar, uygulama geliştiricisi Google Play’e bir güncelleştirme yayımladığında otomatik olarak güncelleştirilir.

Android kurumsal şirkete ait iş profili aygıtlarından bir uygulamayı kaldırmak için aşağıdakilerden birini yapabilirsiniz:
- Gerekli uygulama dağıtımını silin.
- Uygulama için bir kaldırma dağıtımı oluşturun.

## <a name="next-steps"></a>Sonraki adımlar
- [Android uygulamalarını dağıtma](../apps/apps-deploy.md)
- [Android yapılandırma ilkelerini ekleme](../configuration/device-profiles.md)
