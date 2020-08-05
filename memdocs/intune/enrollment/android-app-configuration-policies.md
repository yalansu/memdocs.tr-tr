---
title: Android kurumsal güvenlik yapılandırma ilkeleri
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
ms.openlocfilehash: 3735a37d4572454968638d29ab2646d6fda943ad
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546595"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>Android Enterprise Security Configuration Framework uygulama yapılandırma ilkeleri

[Android kurumsal güvenlik yapılandırma çerçevesinin](android-configuration-framework.md)bir parçası olarak, Android Kurumsal cihazları için uygulama yapılandırma ilkelerini düzgün şekilde ayarlamanız gerekir.

Android kurumsal iş profili cihazları, iş ve kişisel verileri diğerinden yalıtmak için tasarlanmıştır. Android kurumsal tam olarak yönetilen cihazlar yalnızca iş veya okul verilerini tasarlamıştır. Bu nedenle, bu cihazlarda dağıtılan Microsoft uygulamalarının kişisel hesaplara izin vermeyecek şekilde yapılandırılması gerekir.

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>Android kurumsal cihazlarda Microsoft uygulamaları için kişisel hesaplara izin verme

1. Uygulamaları yönetilen Google Play ekleyin. Daha fazla bilgi için bkz. [Intune Ile Android Enterprise cihazlarına yönetilen Google Play uygulamaları ekleme](../apps/apps-add-android-for-work.md).
2. Yönetilen [Android Kurumsal cihazları için uygulama yapılandırma Ilkeleri ekleme]()başlığı altında açıklandığı gibi, her yönetilen Google Play uygulaması için bir ilke oluşturun.
3. Her ilkede aşağıdaki tek anahtarı oluşturun:

    | Anahtar | Değerler |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | Bir veya daha fazla; ayrılmış UPN 'ler.<br>Yalnızca bu anahtar ile tanımlanan yönetilen kullanıcı hesaplarına izin verilir.<br>Intune 'a kayıtlı cihazlar için, {{userPrincipalName}} belirteci kayıtlı Kullanıcı hesabını temsil etmek için kullanılabilir. |


## <a name="next-steps"></a>Sonraki adımlar
[Android kurumsal iş profili güvenlik ayarlarını](android-work-profile-security-settings.md) veya [Android kurumsal tam yönetilen güvenlik ayarlarını](android-fully-managed-security-settings.md)uygulayın.