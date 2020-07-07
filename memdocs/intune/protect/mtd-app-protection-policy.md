---
title: Intune ile Mobile Threat Defense (MTD) uygulama koruma ilkesi oluşturma
titleSuffix: Microsoft Intune
description: Microsoft Intune ile Mobile Threat Defense (MTD) uygulama koruma ilkesi oluşturun.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92d57fe2c63789c6e9f97c8ec835f6ded784ebad
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.contentlocale: tr-TR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972122"
---
# <a name="create-mobile-threat-defense-app-protection-policy-with-intune"></a>Intune ile Mobile Threat Defense uygulama koruma ilkesi oluşturma

Mobile Threat Defense (MTD) ile Intune, tehditleri algılamanıza ve mobil cihazlarda riski değerlendirmenize yardımcı olur. Cihazın şirket verilerine erişmesine izin verilip verilmeyeceğini belirleme riskini değerlendirir eden bir Intune uygulama koruma ilkesi oluşturabilirsiniz.

> [!NOTE]
> Bu makale, uygulama koruma ilkelerini destekleyen tüm Mobile Threat Defense iş ortakları için geçerlidir:
>
> - Daha iyi mobil (Android, iOS/ıpados)
> - Lookout for Work (Android, iOS/ıpados)
> - Wandera (Android, iOS/ıpados)
> - Zyium (Android, iOS/ıpados)

## <a name="before-you-begin"></a>Başlamadan önce

MTD kurulumunun parçası olarak, MTD iş ortağı konsolunda çeşitli tehditleri yüksek, orta ve düşük olarak sınıflandıran bir ilke oluşturdunuz. Artık, Intune uygulama koruma ilkesinde Mobile Threat Defense düzeyini ayarlamanız gerekir.

MTD ile uygulama koruma ilkesi önkoşulları:

- Intune ile MTD tümleştirmesini ayarlayın. Bu tümleştirme olmadan MTD uygulama koruma ilkesinin hiçbir etkisi olmayacaktır.

## <a name="to-create-an-mtd-app-protection-policy"></a>MTD uygulama koruma ilkesi oluşturmak için

[İOS/ıpados veya Android için bir uygulama koruma ilkesi oluşturmak](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps)üzere yordamını kullanın ve *uygulamalar*, *koşullu başlatma*ve *atamalar* sayfalarında aşağıdaki bilgileri kullanın:

- **Uygulamalar**: uygulama koruma ilkeleri tarafından hedefleneceğini istediğiniz uygulamaları seçin. Bu özellik kümesi için, bu uygulamalar engellenir veya seçtiğiniz mobil tehdit savunma satıcınızdan cihaz risk değerlendirmesi temel alınarak seçmeli olarak temizlenir.
- **Koşullu başlatma**: *cihaz koşullarının*altında, **izin verilen en fazla cihaz tehdit düzeyini**seçmek için açılan kutuyu kullanın.

  Tehdit düzeyi **değeri**için seçenekler:

  - **Güvenli**: En güvenli düzeydir. Cihazda herhangi bir tehdit yok ve şirket kaynaklarına erişmeye devam edemiyor. Herhangi bir tehdit bulunursa cihaz uyumsuz olarak değerlendirilir.
  - **Düşük**: Cihaz, yalnızca düşük düzeydeki tehditler varsa uyumludur. Daha yüksek bir tehdit düzeyi, cihazı uyumlu değil durumuna getirir.
  - **Orta**: Cihazda bulunan tehditler düşük veya orta düzeydeyse cihaz uyumludur. Yüksek düzeyde tehditler algılanırsa cihaz uyumsuz olarak değerlendirilir.
  - **Yüksek**: Bu düzey en az güvenlidir ve yalnızca raporlama amacıyla mobil tehdit savunması kullanılarak tüm tehdit düzeylerine izin verir. Cihazlar, bu ayar ile MTD uygulamasının etkin olmasını gerektirir.

  **Eylem**seçenekleri:

  - **Hizmete erişimi**
  - **Verileri silme**

- **Atamalar**: ilkeyi Kullanıcı gruplarına atayın.  Grubun üyeleri tarafından kullanılan cihazlar, Intune uygulama koruması aracılığıyla hedeflenen uygulamalardaki şirket verilerine erişim için değerlendirilir.

## <a name="next-steps"></a>Sonraki adımlar

- Microsoft Intune 'de [Mobile Threat](mobile-threat-defense.md) Defense hakkında daha fazla bilgi edinin.
