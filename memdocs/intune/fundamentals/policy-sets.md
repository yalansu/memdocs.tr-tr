---
title: İlke kümeleri
titleSuffix: Microsoft Intune
description: Microsoft Intune içindeki yönetim nesneleri koleksiyonlarını gruplamak için ilke kümelerini kullanın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: craigma
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09da822557e27eca29da2afc342c93a76d698d6c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909933"
---
# <a name="use-policy-sets-to-group-collections-of-management-objects"></a>Yönetim nesnelerinin koleksiyonlarını gruplamak için ilke kümelerini kullanma

İlke kümeleri, önceden tanımlanmış, hedeflenen ve tek bir kavramsal birim olarak izlenmesi gereken yönetim varlıklarının başvuruları için bir paket oluşturmanıza olanak sağlar. İlke kümesi, oluşturduğunuz uygulamalar, ilkeler ve diğer yönetim nesnelerinin atanabilir bir koleksiyonudur. İlke kümesi oluşturma, aynı anda birçok farklı nesneyi seçmenizi ve bunları tek bir yerden atamanızı sağlar. Kuruluşunuz değiştikçe, nesne ve atamalarını eklemek veya kaldırmak için bir ilke kümesini tekrar ziyaret edebilirsiniz. Tek bir pakette bulunan uygulamalar, ilkeler ve VPN 'Ler gibi mevcut nesneleri ilişkilendirmek ve atamak için bir ilke kümesi kullanabilirsiniz. 

> [!IMPORTANT]
> İlke kümeleriyle ilgili bilinen sorunların listesi için, [ilke bilinen sorunları ayarlar](policy-sets.md#policy-sets-known-issues).

İlke kümeleri varolan kavramları veya nesneleri değiştirmez. Tek tek nesneleri atamaya devam edebilir ve bir ilke kümesinin parçası olarak tek tek nesnelere de başvurabilirsiniz. Bu nedenle, bağımsız nesnelerde yapılan tüm değişiklikler ilke kümesine yansıtılır.

İlke kümelerini kullanarak şunları yapabilirsiniz:

- Birlikte atanması gereken nesneleri gruplandırma
- Kuruluşunuzun tüm yönetilen cihazlarda en düşük yapılandırma gereksinimlerini atama
- Tüm kullanıcılara yaygın olarak kullanılan veya ilgili uygulamaları atama

Aşağıdaki yönetim nesnelerini bir ilke kümesine dahil edebilirsiniz:

- Uygulamalar
- Uygulama yapılandırma ilkeleri
- Uygulama koruma ilkeleri
- Cihaz yapılandırma profilleri
- Cihaz uyumluluğu ilkeleri
- Cihaz türü kısıtlamaları
- Windows Autopilot dağıtım profilleri
- Kayıt durumu sayfası

Bir ilke kümesi oluşturduğunuzda, tek bir atama birimi oluşturur ve farklı nesneler arasındaki ilişkilendirmeleri yönetebilirsiniz. İlke kümesi, onun dış nesnelerine bir başvuru olacaktır. Dahil edilen nesnelerdeki tüm değişiklikler ilke kümesini de etkileyecektir. Bir ilke kümesi oluşturduktan sonra, nesnelerini ve atamalarını art arda görüntüleyebilir ve düzenleyebilirsiniz. 

> [!NOTE]
> İlke kümeleri Windows, Android, macOS ve iOS/ıpados ayarlarını destekler ve platformlar arası bir şekilde atanabilir.

## <a name="how-to-create-a-policy-set"></a>İlke kümesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihazlar**  >  **ilke kümeleri**  >  **ilke kümelerini**Seç  >  **Oluştur**' u seçin.
3. **Temel bilgiler** sayfasında, aşağıdaki değerleri ekleyin:
    - **İlke kümesi adı** -Bu ilke kümesi için bir ad sağlayın.
    - **Açıklama** -isteğe bağlı olarak, ilke kümesi için bir açıklama sağlayın.
   <p>
      <img alt="Create policy set - Basics" src="./media/policy-sets/policy-sets-01.png">

4. **İleri**' ye tıklayın.<br>
   **Uygulama yönetimi** sayfasında isteğe bağlı olarak, ilke kümesine uygulamalar, [uygulama yapılandırma ilkeleri](../apps/app-configuration-policies-overview.md)ve [Uygulama koruma ilkeleri](../apps/app-protection-policy.md) [ekleyebilirsiniz](../apps/apps-add.md). Uygulama yönetimi hakkında bilgi için bkz. [uygulama yönetimi Microsoft Intune nedir?](../apps/app-management.md).
5. **İleri**' ye tıklayın.<br>
   Cihaz **yönetimi** sayfası, ilke kümesine cihaz [yapılandırma profilleri](../configuration/device-profiles.md) ve [cihaz uyumluluk ilkeleri](../protect/device-compliance-get-started.md)gibi cihaz yönetimi nesneleri eklemenize olanak tanır. Diğer ilkeler, sertifikalar ve güvenlik temel profilleri gibi tüm ilişkili nesneleri eklediğinizden emin olun.
6. Ileri ' ye tıklayın **: cihaz kaydı**.<br>
   Cihaz **kayıt** sayfası, ilke kümesine [cihaz türü kısıtlamaları](../enrollment/enrollment-restrictions-set.md), [Windows Autopilot dağıtım profilleri](../../autopilot/enrollment-autopilot.md)ve [kayıt durumu sayfa profilleri](../enrollment/windows-enrollment-status.md)gibi cihaz kayıt nesneleri eklemenize olanak tanır.
7. **İleri: atamalar**' a tıklayın.<br>
   **Atamalar** sayfası, ilke kümesini kullanıcılara ve cihazlara atamanıza olanak tanır. Cihazın Intune tarafından yönetilip yönetilmediğini bir cihaza bir ilke kümesi atayabileceğinizi unutmayın.
8. Ileri ' ye tıklayın, profil için girdiğiniz değerleri gözden geçirmek için **+ Oluştur** ' a tıklayın.
9. İşiniz bittiğinde, Intune 'da ilke kümesini oluşturmak için **Oluştur** ' a tıklayın.

## <a name="policy-sets-known-issues"></a>İlke bilinen sorunları ayarlıyor

1910 ' de yeni ilke kümelerinde aşağıdaki bilinen sorunlar vardır.

- Bir ilke kümesi oluştururken, kapsamlı bir yönetici hiçbir kapsam etiketi seçmeden bir ilke kümesi oluşturmayı denediğinde, **Gözden geçirme ve oluşturma** sayfasına ulaştıktan sonra doğrulama başarısız olur ve durum çubuğunda bir hata görüntülenir. Yönetici, işlemdeki farklı bir sayfaya geçiş yapmak ve ardından **gözden geçir + oluştur** sayfasına geri dönmelidir. Bu, **Oluştur** seçeneğini etkinleştirir.  

- Aşağıdaki uygulama türleri şu anda ilke kümeleri tarafından destekleniyor:
  - iOS/ıpados Mağazası uygulaması
  - iOS/ıpados iş kolu uygulaması
  - Yönetilen iOS/ıpados iş kolu uygulaması
  - Android mağazası uygulaması
  - Android iş kolu uygulaması
  - Yönetilen Android iş kolu uygulaması
  - Microsoft 365 uygulamalar (Windows 10)
  - Web bağlantısı
  - Yerleşik iOS/ıpados uygulaması
  - Yerleşik Android uygulaması

- **Tüm kullanıcıların** bir ilke kümesi atamasını **Autopilot profiline** ayarlama desteklenmez.

- İlke kümelerinde aşağıdaki kayıt kısıtlamaları ve kayıt durumu sayfası (ESP) sorunları vardır:
  - Kısıtlamalar ve ESP, sanal grup atamalarını desteklemez.
  - Kısıtlamalar ve ESP dışlama grubu atamalarını kesinlikle desteklemez. 
  - Kısıtlamalar ve ESP, öncelik tabanlı çakışma çözümü kullanır. Kısıtlamalar ve ESP de daha yüksek bir öncelik kısıtlaması ve ESP tarafından hedeflenirse, kısıtlamalar ve ESP, ilke kümesinin yükleri ile aynı kullanıcılara uygulanamayabilir.
  - Varsayılan kısıtlamalar ve ESP bir ilke kümesine eklenemez.

- İlke kümelerini destekleyen MAM ilke türleri şunları içerir: 
  - MAM WıP (Windows) MDM hedeflenen yönetilen uygulama koruması 
  - MAM iOS/ıpados hedeflenen yönetilen uygulama korumasını
  - MAM Android hedeflenen yönetilen uygulama koruması
  - MAM iOS/ıpados hedeflenen yönetilen uygulama yapılandırması
  - MAM Android hedeflenen yönetilen uygulama yapılandırması

- İlke kümelerini desteklemeyen MAM ilke türleri şunları içerir: 
  - MAM WıP (Windows) hedeflenen yönetilen uygulama koruması

- MAM, ilkeyi aşağıdaki ilke türleri için doğrudan atamalar olarak ayarlar.
  - MAM iOS/ıpados hedeflenen yönetilen uygulama korumasını
  - MAM Android hedeflenen yönetilen uygulama koruması
  - MAM iOS/ıpados hedeflenen yönetilen uygulama yapılandırması
  - MAM Android hedeflenen yönetilen uygulama yapılandırması

    Bir gruba dağıtılan bir ilke kümesine bir ilke eklenirse, Grup "ilke kümesi ile atanmamış" değil, iş yükünde doğrudan atanmış olarak gösterilir. Bunun sonucunda, MAM, ilke kümelerinden gelen grup atama silme işlemlerini işlemez.

- MAM herhangi bir ilke türü için **tüm kullanıcılara** ve **tüm cihazlar** sanal gruplarına dağıtımı desteklemez.
- "Yönetim Şablonları" türündeki cihaz yapılandırma profili, ilke kümesinin bir parçası olarak seçilemez.

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune’da cihazları kaydetme](../enrollment/index.yml)