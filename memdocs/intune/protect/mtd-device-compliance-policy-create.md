---
title: Microsoft Intune ile Mobile Threat Defense (MTD) cihaz uyumluluk ilkesi oluşturma
titleSuffix: Microsoft Intune
description: Bir mobil cihazın şirket kaynaklarına erişip erişemeyeceğini belirlemek için MTD iş ortağı tehdit düzeylerinizi kullanan bir Intune cihaz uyumluluğu ilkesi oluşturun.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88f8a2ff04f536370f613341170e7fae0a808ff6
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365534"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Intune ile Mobile Threat Defense (MTD) cihaz uyumluluk ilkesi oluşturma

Intune ile MTD, mobil cihazlarda tehditleri algılayıp risk değerlendirmesi yapmanıza yardımcı olur. Bir cihazın uyumlu olup olmadığını belirlemek üzere risk değerlendirmesi yapan bir Intune cihaz uyumluluk ilkesi kuralı oluşturabilirsiniz. Daha sonra, cihaz uyumluluğuna göre hizmetlere erişimi engellemek için bir [koşullu erişim ilkesi](create-conditional-access-intune.md) kullanabilirsiniz.

> [!NOTE]
> Bu bilgiler, tüm Mobile Threat Defense iş ortakları için geçerlidir.

## <a name="before-you-begin"></a>Başlamadan önce

MTD kurulumunun parçası olarak, MTD iş ortağı konsolunda çeşitli tehditleri yüksek, orta ve düşük olarak sınıflandıran bir ilke oluşturdunuz. Daha sonra, Intune cihaz uyumluluk ilkesinde Mobile Threat Defense düzeyini ayarlayacaksınız.

MTD ile cihaz uyumluluk ilkesinin önkoşulları:

- Intune ile MTD tümleştirmesini ayarlama

## <a name="to-create-an-mtd-device-compliance-policy"></a>MTD cihaz uyumluluk ilkesi oluşturmak için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security**  >  **cihaz uyumluluğu**  >  **ilke oluştur**' u seçin.

3. **Platformu**seçin ve ardından **oluşturun**.

4. **Temel bilgiler**için bir cihaz uyumluluk ilkesi **adı**ve **Açıklama** (isteğe bağlı) belirtin. Devam etmek için **İleri** seçeneğini belirleyin.


5. **Uyumluluk ayarları**' nı genişletin ve **cihaz durumu**yapılandırın. **Cihazın cihaz tehdit düzeyinde veya altında olmasını gerektir ' in**açılan listesinden mobil tehdit düzeyini seçin.

   - **Güvenli**: En güvenli düzeydir. Cihazda herhangi bir tehdit yok ve şirket kaynaklarına erişmeye devam edemiyor. Herhangi bir tehdit bulunursa cihaz uyumsuz olarak değerlendirilir.

   - **Düşük**: Cihaz, yalnızca düşük düzeydeki tehditler varsa uyumludur. Daha yüksek bir tehdit düzeyi, cihazı uyumlu değil durumuna getirir.

   - **Orta**: Cihazda bulunan tehditler düşük veya orta düzeydeyse cihaz uyumludur. Yüksek düzeyde tehditler algılanırsa cihaz uyumsuz olarak değerlendirilir.

   - **Yüksek**: Bu tehdit düzeyi, tüm tehdit düzeylerine izin verdiği ve yalnızca raporlama amacıyla mobil tehdit savunması kullandığı için en az güvenlidir. Cihazlar, bu ayar ile MTD uygulamasının etkin olmasını gerektirir.

6. **Atamalar**' a Ilerlemek için **İleri ' yi** seçin. Bu profili alacak grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

   **İleri**’yi seçin.

7. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin. Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

> [!IMPORTANT]
> Office 365 veya diğer hizmetler için koşullu erişim ilkeleri oluşturursanız, cihaz uyumluluk değerlendirmesi değerlendirilir ve uyumlu olmayan cihazların, tehdit cihazda çözümlenene kadar kurumsal kaynaklara erişmesi engellenir.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>MTD cihaz uyumluluk ilkesini atamak için

Bir cihaz uyumluluk ilkesinin kullanıcılara atamasını atamak ya da değiştirmek için:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Endpoint Security**  >  **cihaz uyumluluğu**' nu seçin.

3. Kullanıcılara atamak istediğiniz ilkeyi seçin ve ardından **Özellikler**' i seçin.

4. Atamalar için **Düzenle** ' yi seçin ve ardından bu ilkeyi almak üzere grupları *dahil* etmek ve *dışlamak* için kullanılabilir seçenekleri kullanın.  

5. Atamayı tamamladıktan sonra **gözden geçir + kaydet** ' i seçin. Atamayı kaydettiğinizde, ilke seçili kullanıcılarınıza dağıtılır ve cihazları uyumluluk için değerlendirilir.

## <a name="next-steps"></a>Sonraki adımlar

[MTD'yi Intune ile etkinleştirme](mtd-connector-enable.md)
