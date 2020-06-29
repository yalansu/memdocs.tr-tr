---
title: Android Enterprise Security Configuration Framework için cihaz kaydı kısıtlamaları
titleSuffix: Microsoft Intune
description: Android kurumsal güvenlik yapılandırma çerçevesi için cihaz kaydı kısıtlamaları.
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
ms.openlocfilehash: d26040c5a009a9c3877abbc25512e317f584f114
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502876"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Android kurumsal cihaz kaydı kısıtlamaları

[Android kurumsal güvenlik yapılandırma çerçevesi]()için cihazları kaydetmeden önce, kuruluşların uygun kısıtlamaları yapılandırması gerekir. Bu kısıtlamalar, kullanıcıların yalnızca kayıt açabildiğinden emin olmanızı
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
Android kurumsal tam olarak yönetilen kaydı inceleyerek kuruluşun Android kurumsal tam olarak yönetilen cihaz kaydını desteklediğinden emin olun. 

## <a name="next-steps"></a>Sonraki adımlar

[Uygulama yapılandırma ilkelerini ayarlama](android-app-configuration-policies.md)
