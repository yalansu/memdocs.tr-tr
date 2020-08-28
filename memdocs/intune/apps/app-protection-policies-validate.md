---
title: Uygulama koruma ilkesi kurulumunuzu doğrulama
titleSuffix: Microsoft Intune
description: Microsoft Intune'da uygulama koruma ilkenizin kurulduğunu ve doğru şekilde çalıştığını sınamayı öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.topic: how-to
ms.technology: ''
ms.assetid: 15f8a838-0b69-412b-a42e-c6edb61f0cae
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02266ce355d4fc4b74487840a91b503d69bf7b2e
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996512"
---
# <a name="how-to-validate-your-app-protection-policy-setup-in-microsoft-intune"></a>Microsoft Intune'da uygulama koruma ilkesi kurulumunuzu doğrulama

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Uygulama koruma ilkenizin doğru kurulduğunu ve çalıştığını doğrulayın. Bu kılavuz, Azure portaldaki uygulama koruma ilkeleri için geçerlidir.

## <a name="checking-for-symptoms"></a>Belirtileri denetleme
Uygulama koruma bir veri koruması aracı olduğundan, kullanıcıların soruları bildirme olasılığı düşüktür. Uygulama koruma yapılandırmasında bir sorun varsa, kullanıcılar uygulama korumanın olmadığı durumlardaki gibi sınırsız erişime sahip olur ve bir sorun olduğunun farkına varmazlar. Bu nedenle uygulama koruma kısıtlamalarını bilinçli olarak sınayabilecek küçük bir grup kullanıcıya uygulama koruma ilkelerinizin pilot dağıtımını yaparak, uygulama koruma yapılandırmanızı doğrulamanızı öneririz.

## <a name="what-to-check"></a>Denetlenmesi gerekenler

Sınama, uygulama koruma ilkelerinizin davranışının beklendiği gibi çalışmadığını gösteriyorsa şu öğeleri kontrol etmenizi öneririz:

- Kullanıcılar uygulama koruma için lisanslı mı?
- Kullanıcılar Microsoft 365 lisanslı mi?
- Her kullanıcının uygulama koruma uygulamalarındaki durumu beklendiği gibi mi? Uygulamalar için olabilecek durumlar **İade edildi** ve **İade edilmedi** şeklindedir.

### <a name="user-app-protection-status"></a>Kullanıcı uygulama koruma durumu
1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Apps**  >  **Monitor**  >   **Uygulama koruma durumunu**izlemek için uygulamalar ' ı seçin ve ardından **atanan kullanıcılar** kutucuğunu seçin. 
4. **Uygulama raporlama** sayfasında **Kullanıcı seçin**'i belirterek kullanıcı ve grupların bulunduğu listeyi açın. 
5. Arama yapıp listeden bir kullanıcı seçin ve sonra **Kullanıcı seçin**’i belirtin. **Uygulama raporlama** bölmesinin en üstünde kullanıcının uygulama koruması için lisanslı olup olmadığını görebilirsiniz. Ayrıca kullanıcının Microsoft 365 lisansa sahip olup olmadığını ve kullanıcının tüm cihazları için uygulama durumunu görebilirsiniz.

## <a name="what-to-do"></a>Ne yapılmalı
Kullanıcı durumuna göre gerçekleştirilecek eylemler şunlardır:

- Kullanıcının uygulama koruma lisansı yoksa bir [Intune lisansı](../fundamentals/licenses.md) atayın.
- Kullanıcı Microsoft 365 için lisanslı değilse, Kullanıcı için bir [Lisans](../fundamentals/licenses.md) alın.
- Bir kullanıcının uygulaması **Iade edilmedi**olarak listeleniyorsa, bu uygulama için doğru bir [Uygulama koruma ilkesi](app-protection-policies-validate.md) yapılandırılıp yapılandırılmadığını denetleyin.
- Bu koşulların, [uygulama koruma ilkelerinin](app-protection-policies-monitor.md) geçerli olmasını istediğiniz tüm kullanıcılara uygulandığından emin olun.

## <a name="see-also"></a>Ayrıca bkz.

- [Intune uygulama koruma ilkesi nedir?](app-protection-policies.md)
- [Intune içeren lisanslar](../fundamentals/licenses.md)
- [Cihazlarını Intune’a kaydedebilmeleri için kullanıcılara lisans atama](../fundamentals/licenses-assign.md)
- [Uygulama koruma İlkesi kurulumunuzu doğrulama](app-protection-policies-validate.md)
- [Uygulama koruma ilkelerini izleme](app-protection-policies-monitor.md)

