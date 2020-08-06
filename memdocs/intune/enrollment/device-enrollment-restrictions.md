---
title: Android Enterprise Security Configuration Framework için cihaz kaydı kısıtlamaları
titleSuffix: Microsoft Intune
description: Android kurumsal güvenlik yapılandırma çerçevesi için cihaz kaydı kısıtlamaları.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/02/2020
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
ms.openlocfilehash: 5c2689e010c0ec75340e1a96952cf6ac162322da
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758287"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Android kurumsal cihaz kaydı kısıtlamaları

[Android kurumsal güvenlik yapılandırma çerçevesi](android-configuration-framework.md)için cihazları kaydetmeden önce, kuruluşların uygun kısıtlamaları yapılandırması gerekir. Bu kısıtlamalar, kullanıcıların yalnızca kayıt açabildiğinden emin olmanızı

- onaylanan cihazlar.
- Belirtilen sayıda cihaz.
- Belirtilen platformlarla cihazlar.
- belirtilen işletim sistemlerine sahip cihazlar.
- Belirtilen üreticilerin cihazları.

Cihaz Kayıt kısıtlamaları hakkında daha fazla bilgi için bkz. [kayıt kısıtlamalarını ayarlama](enrollment-restrictions-set.md).

## <a name="work-profile-basic-level-1-security-restrictions"></a>İş profili temel (düzey 1) güvenlik kısıtlamaları

Android kurumsal iş profili temel güvenliği (düzey 1) için aşağıdaki cihaz kısıtlamalarının uygulanması gerekir:

| Tür | Platform | Sürüm | Kişisel cihazlara izin verir |
|--------|--------|--------|--------|
| Android Kurumsal | İzin Ver | Android 5,0 ve üzeri.<p>Microsoft, en düşük Android ana sürümünün Microsoft uygulamaları için desteklenen Android sürümleriyle eşleşecek şekilde yapılandırılmasını önerir. Android kurumsal gereksinimleri olan OEM 'Ler ve cihazlar, geçerli sevkiyat sürümü + bir mektup yükseltmesi desteklemelidir.   Android, bilgi çalışanları için Android 8,0 ve üstünü öneriyor. Daha fazla bilgi için bkz. [Android Enterprise önerilen gereksinimleri](https://www.android.com/enterprise/recommended/requirements/). | Yes |
| Android cihaz yöneticisi| Blok | Tüm sürümler | Yes |

## <a name="work-profile-high-level-3-security-restrictions"></a>İş profili yüksek (düzey 3) güvenlik kısıtlamaları
Android kurumsal iş profili yüksek güvenlik (düzey 3) için aşağıdaki cihaz kısıtlamalarının uygulanması gerekir:

| Tür | Platform | Sürüm | Kişisel cihazlara izin verir |
|--------|--------|--------|--------|
| Android Kurumsal | İzin Ver | Android 8,0 ve üzeri | Yes |
| Android cihaz yöneticisi| Blok | Tüm sürümler | Yes |

## <a name="fully-managed-security-restrictions"></a>Tam olarak yönetilen güvenlik kısıtlamaları
Kuruluşun, [tam olarak yönetilen cihazları kaydetmeyi](android-fully-managed-enroll.md#enroll-the-fully-managed-devices)Inceleyerek Android kurumsal tam olarak yönetilen cihaz kaydını desteklediğinden emin olun. 

## <a name="conditional-access-policies"></a>Koşullu erişim ilkeleri
Kuruluşlar, kullanıcıların yalnızca kayıtlı Android cihazlarda iş veya okul içeriğine erişebildiğinden emin olmak için Azure AD koşullu erişim ilkelerini kullanabilir. Bunu yapmak için tüm olası kullanıcıları hedefleyen bir koşullu erişim ilkesine ihtiyacınız olacaktır. Bu ilkeyi oluşturma hakkındaki ayrıntılar, [bulut uygulaması için yönetilen cihazlar Için koşullu erişimle erişim gerektir](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)bölümünde bulunabilir. 

Senaryodaki adımları izleyin [: iOS ve Android cihazlar için cihaz kaydı gerektir](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices)ve yalnızca uyumlu olan kayıtlı mobil cihazların Office 365 uç noktalarına bağlanabilmesini sağlar.

## <a name="next-steps"></a>Sonraki adımlar

[Uygulama yapılandırma ilkelerini ayarlama](android-app-configuration-policies.md)
