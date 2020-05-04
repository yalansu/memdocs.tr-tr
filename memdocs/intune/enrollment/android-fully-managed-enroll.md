---
title: Android kurumsal tam olarak yönetilen cihazlar için Intune kaydını kurma
titleSuffix: Microsoft Intune
description: Android kurumsal tam yönetilen cihazları Intune 'a kaydetmeyi öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8830d0c18bb4ef257abcffd75d001b9d8af5f502
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81220592"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-fully-managed-devices"></a>Android kurumsal tam olarak yönetilen cihazların Intune kaydını ayarlama 

Android Kurumsal tam olarak yönetilen cihazları, tek kullanıcıyla ilişkilendirilmiş ve yalnızca iş için kullanılan (kişisel amaçlarla kullanılmayan) şirkete ait cihazlardır. Yöneticiler cihazı tümüyle yönetebilir ve ilke denetimlerini iş profilleri için kullanılamaz hale uygulayabilir, örneğin:
- Yalnızca yönetilen Google Play uygulama yüklemeye izin verin.
- Yönetilen uygulamaların kaldırılmasını engelleyin.
- Kullanıcıların cihazların fabrika ayarlarına sıfırlamasını ve bu şekilde devam etmelerini önleyin.

Intune, Android kurumsal tam olarak yönetilen cihazlar dahil olmak üzere Android kurumsal cihazlara uygulama ve ayarlar dağıtmanıza yardımcı olur. Android Enterprise hakkında ayrıntılı bilgi için bkz. [Android Enterprise Requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="technical-requirements"></a>Teknik gereksinimler

Android kurumsal tam olarak yönetilen cihazları yönetmek için tek başına Intune kiracısına sahip olmanız gerekir. Tam olarak yönetilen cihaz yönetimi eski Silverlight Yönetim konsolunda kullanılamıyor.

Cihazların, Android kurumsal tam olarak yönetilen bir cihaz olarak yönetilmesi için bu gereksinimleri karşılaması gerekir:

- Android OS sürüm 6,0 ve üzeri.
- Cihazların Google Mobile Services (GMS) bağlantısı olan bir Android derlemesi çalıştırması gerekir. Cihazlarda GMS kullanılabilir olmalı ve cihazlar GMS’ye bağlanabilmelidir.

Yukarıdaki gereksinimler karşılanıyorsa cihaz üreticisi/OEM üzerinde bir kısıtlama yoktur.

## <a name="set-up-android-enterprise-fully-managed-device-management"></a>Android kurumsal tam yönetilen cihaz yönetimini ayarlama

Android kurumsal tam olarak yönetilen cihaz yönetimini ayarlamak için aşağıdaki adımları izleyin:

1. Mobil cihazları yönetmeye hazırlanmak için [mobil cihaz yönetimi (MDM) yetkilisini **Microsoft Intune**olarak ayarlamanız](../fundamentals/mdm-authority-set.md)gerekir. Bu öğeyi yalnızca mobil cihaz yönetimi için Intune’u ilk defa kurduğunuzda ayarlarsınız.
2. [Intune kiracı Hesabınızı Android Kurumsal hesabınıza bağlayın](connect-intune-android-enterprise.md).
3. [Şirkete ait Kullanıcı cihazlarını etkinleştir](#enable-corporate-owned-user-devices)
4. [Tam olarak yönetilen cihazları kaydedin](#enroll-the-fully-managed-devices).

### <a name="enable-corporate-owned-user-devices"></a>Şirkete ait Kullanıcı cihazlarını etkinleştir

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde oturum açın ve **cihazlar** > **Android** > **Android kayıt**  > **şirkete ait, tam olarak yönetilen Kullanıcı cihazları ' nı**seçin.
2. **Kullanıcıların şirkete ait Kullanıcı cihazlarını kaydetmesine Izin ver**altında **Evet**' i seçin.

> [!NOTE]
> Bir cihazın uyumlu izin denetimi veya bir engelleme ilkesi *olarak işaretlenmesini gerektir* ve **tüm bulut uygulamaları**, **Android**ve **TARAYıCıLAR**Için geçerli olmasını gerektiren bir Azure AD koşullu erişim ilkeniz varsa, bu ilkeden **Microsoft Intune** Cloud App 'i dışarıda bırakmanız gerekir. Bunun nedeni, Android Kurulum işleminin kayıt sırasında kullanıcılarınızın kimliğini doğrulamak için bir Chrome sekmesi kullanmamasıdır. Daha fazla bilgi için bkz. [Azure AD koşullu erişim belgeleri](https://docs.microsoft.com/azure/active-directory/conditional-access/).

Bu ayar **Evet**olarak ayarlandığında, Intune kiracınız için bir kayıt belirteci (rastgele bir dize) ve QR kodu sağlar. Bu tek kayıt belirteci tüm kullanıcılarınız için geçerlidir ve sona ermez. Cihazın Android işletim sistemine ve sürümüne bağlı olarak, cihazı kaydetmek için belirteci veya QR kodunu kullanabilirsiniz.

## <a name="enroll-the-fully-managed-devices"></a>Tam olarak yönetilen cihazları kaydetme
Artık [tam olarak yönetilen cihazlarınızı](android-dedicated-devices-fully-managed-enroll.md) (dem hesapları kullanırken değil) kaydedebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
- [Android kurumsal tam yönetilen cihaz yapılandırma ilkeleri ekleme](../configuration/device-restrictions-android-for-work.md#device-owner-only)
- [Android kurumsal tam olarak yönetilen cihazlar için uygulama yapılandırma ilkelerini yapılandırma](../apps/app-configuration-policies-use-android.md)

