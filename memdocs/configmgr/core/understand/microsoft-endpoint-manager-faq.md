---
title: Microsoft Endpoint Configuration Manager hakkında SSS
titleSuffix: Configuration Manager
description: Microsoft uç noktası Configuration Manager hakkında sık sorulan sorular
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f6c7321301e5705c4188012ba53b50f4c37b57
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906027"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Microsoft Endpoint Configuration Manager hakkında SSS

*Uygulama hedefi: Configuration Manager (güncel dal, Technical Preview dalı)*

Sürüm 1910 ' den başlayarak Configuration Manager artık Microsoft Endpoint Manager 'ın bir parçasıdır. Bu makalede, sık sorulan soruların yanıtları sağlanmaktadır.

## <a name="summary"></a>Özet

Atacan Anderson, Microsoft Kurumsal Başkan Yardımcısı Microsoft 365 için aşağıdaki iki dakikalık videoyu izleyerek başlayın:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>SSS

### <a name="what-is-microsoft-endpoint-manager"></a>Microsoft Uç Nokta Yöneticisi nedir?

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U Basitleştirilmiş lisanslama ile birlikte sunar. Mevcut Configuration Manager yatırımlarınızdan yararlanmaya devam edin, Microsoft bulutun gücünden kendi hızınızda yararlanın.

Aşağıdaki Microsoft yönetim çözümleri artık **Microsoft Endpoint Manager** markasının bir parçasıdır:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- [Cihaz yönetimi yönetici konsolundaki](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760) diğer özellikler

Daha fazla bilgi için, Microsoft Kurumsal Başkan Yardımcısı Microsoft 365 atacan Anderson 'tan aşağıdaki gönderilere bakın:

- [Duyuru blog gönderisi](https://aka.ms/cmannounce)
- [Vizyon kağıdı](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Microsoft Uç Nokta Yöneticisi ile Configuration Manager hangi şeyler değişir?

Sürüm 1910 ' de, ad değişikliğinden ayrılan Configuration Manager hala aynı işlevleri görür.

Çoğu bilinen olarak, [Configuration Manager konsolu](../servers/manage/admin-console.md#bkmk_open) ve [Yazılım Merkezi](software-center.md#bkmk_open)gibi ortak bileşenler için Başlat menüsü klasör adları değişmiştir.

### <a name="how-do-we-refer-to-the-product-now"></a>Ürüne şimdi nasıl başvuruyoruz?

- Tüm bileşenlerin bulunduğu tüm çözüme başvurulduğunda: **Microsoft Uç Nokta Yöneticisi**

- Şirket içi bileşene başvururken:
  - İlk başvuru için, tam marka adını kullanın: **Microsoft uç noktası Configuration Manager**
  - Genel kullanım için: **Configuration Manager**
  - Boşlukla kısıtlanmış kullanım için: **ConfigMgr**, yalnızca genel kullanım adının sığmadığı örneklerde

### <a name="are-there-any-licensing-changes"></a>Herhangi bir lisans değişikliği var mı?

Evet! Microsoft Ignite 2019 ' de duyurulduğu gibi, Configuration Manager için lisanslandıysanız, artık Intune 'un Windows bilgisayarlarınızı [birlikte yönetmesi](../../comanage/overview.md) için de lisans lisanslanır. Daha fazla bilgi için bkz. [ürün ve lisanslama hakkında SSS](product-and-licensing-faq.md#bkmk_mem).

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>Neden hala "System Center Configuration Manager" bazı yerleri görüyorum?

Belgeler gibi tüm ürünler, hizmetler ve destekleyici malzemelerde değişiklik yapmak zaman alır.

Hiçbir şekilde değişmeyebilir bazı temel bileşenler de vardır. Site sunucularındaki ana Windows hizmeti hala **SMS_Executive**. Bu belgeleri destekleyen GitHub deposu **Sccmdocs**olmaya devam edecektir.

## <a name="next-steps"></a>Sonraki adımlar

[Configuration Manager artımlı sürümlerindeki](../plan-design/changes/whats-new-incremental-versions.md)yenilikler hakkında bilgi edinin.
