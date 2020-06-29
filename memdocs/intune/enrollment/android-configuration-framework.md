---
title: Android kurumsal güvenlik yapılandırma çerçevesi
titleSuffix: Microsoft Intune
description: Android kurumsal cihaz temel ve yüksek güvenlik için önerilen kısıtlamaları ve ayarları öğrenin.
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
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502877"
---
# <a name="android-enterprise-security-configuration-framework"></a>Android kurumsal güvenlik yapılandırma çerçevesi

Android Enterprise Security Configuration Framework, cihaz uyumluluğu ve yapılandırma ilkesi ayarlarına yönelik bir dizi öneridir. Bu öneriler, kuruluşunuzun mobil cihaz güvenlik korumasını özel gereksinimlerinize uyarlamanıza yardımcı olur.

Güvenlikle ilgili kuruluşlar, mobil cihazlardaki kurumsal verilerin korunmasını sağlamaya yönelik yöntemlere bakar. Bu verileri korumak için kullanılan bir yöntem, cihaz kaydı üzerinden yapılır. Cihaz kaydı, kuruluşlara yardımcı olur:
- Uyumluluk ilkelerini (PIN gücü, jailbreak/root doğrulaması vb. gibi) dağıtın.
- yapılandırma ilkelerini dağıtma (WIFI, sertifikalar, VPN gibi).
- uygulama yaşam döngüsünü yönetin.

Microsoft, tüm güvenlik senaryosunu ayarlamanıza yardımcı olmak için [Windows 10 ' da güvenlik yapılandırmalarına](https://aka.ms/secconframework)yönelik yeni bir taksonomi sunmuştur. Intune, Android kurumsal güvenlik yapılandırma çerçevesi için benzer bir taksonomi kullanıyor. Bunlar, temel, gelişmiş ve yüksek güvenlik için önerilen cihaz uyumluluğu ve cihaz kısıtlama ayarlarını içerir. Bu taksonomi aşağıdaki makalelerde açıklanmıştır:

1. [Android Enterprise Framework dağıtım yöntemi](framework-deployment-methodology.md): güvenlik yapılandırma çerçevesini dağıtmak için önerilen bir metodolojisi.
2. [Android cihaz kaydı kısıtlamaları](device-enrollment-restrictions.md): Android kurumsal cihazlar için ön kayıt öncesi cihaz kısıtlamaları.
3. [Android kurumsal cihazlar için uygulama yapılandırma Ilkelerini ayarlama](android-app-configuration-policies.md): cihazlardaki uygulamaları kişisel hesaplara izin vermeyecek şekilde yapılandırın.
4. [Android kurumsal iş profili güvenlik ayarları](android-work-profile-security-settings.md): iş profili cihazlarında temel ve yüksek güvenlik için belirli yapılandırma ayarları.
5. [Android kurumsal tam olarak yönetilen güvenlik ayarları](android-fully-managed-security-settings.md): tam olarak yönetilen cihazlarda temel, gelişmiş ve yüksek güvenlik için özel yapılandırma ayarları.

## <a name="android-enterprise-enrollment-modes"></a>Android kurumsal kayıt modları

Android 5,0 ile, Google, iki kayıt modu içeren Android Enterprise 'ı sunmuştur. Android kurumsal güvenlik yapılandırma çerçevesi her iki mod için de öneriler sağlar.
- [Tam olarak yönetilen cihazlar (cihaz sahibi)](android-fully-managed-enroll.md): tek bir kullanıcıyla ilişkili olan şirkete aittir. Bu tür cihazlar özel olarak çalışır ve kişisel kullanım içindir.
- İş [profili (profil sahibi)](android-work-profile-enroll.md): genellikle, iş ve kişisel veriler arasında net bir sınır istediğini, kişisel olarak sahip olduğu cihazlar için. BT tarafından denetlenen ilkeler, çalışma verilerinin kişisel profile aktarılmadığından emin olun.


## <a name="next-steps"></a>Sonraki adımlar

[Android Enterprise Framework dağıtım yöntemi](framework-deployment-methodology.md)