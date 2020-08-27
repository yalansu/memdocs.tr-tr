---
title: Microsoft Intune koşullu erişim
titleSuffix: Microsoft Intune
description: Kullanıcıların, cihazların ve uygulamaların Microsoft Intune içindeki şirket kaynaklarına erişmek için karşılaması gereken koşulları nasıl tanımlayacağınızı öğrenin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/06/2018
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1973f38-ea55-43eb-a151-505fb34a8afb
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: c28bda5aa1733bb7dfe3062d24fac27f103ebb48
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915135"
---
# <a name="learn-about-conditional-access-and-intune"></a>Koşullu erişim ve Intune hakkında bilgi edinin

Koşullu erişimle, e-postanıza ve şirket kaynaklarınıza bağlanabilecek cihazları ve uygulamaları kontrol edebilirsiniz. 

Enterprise Mobility + Security (EMS) tek başına bir ürün değildir. Bu, EMS 'nin parçası olan tüm hizmet ve ürünlerin parçası olan bir çözümdür. Koşullu erişim, kullanıcılara herhangi bir cihazdan ve herhangi bir konumdan en iyi iş yapmasına izin veren bir deneyim sunarak kurumsal verilerinizi güvende tutmaya yönelik ayrıntılı erişim denetimi sağlar.

Kurumsal verilerinize erişim için konum, cihaz, kullanıcı durumu ve uygulama hassaslığı temelinde bir geçit oluşturan koşullar tanımlayabilirsiniz.

> [!NOTE]
> Koşullu Erişim, sahip olduğu özellikleri [Office 365 hizmetlerine](/office365/enterprise/office-365-client-support-conditional-access) de yayar.

![Koşullu erişim diyagramı](./media/conditional-access/ca-diagram-1.png)

## <a name="use-conditional-access-with-intune"></a>Intune ile koşullu erişim kullanma

Koşullu erişim, bir Azure Active Directory Premium lisansıyla birlikte sunulan bir Azure Active Directory özelliğidir. Intune, çözüme mobil cihaz uyumluluğu ve mobil uygulama yönetimi ekleyerek bu özelliği geliştirir. 

![EMS kullanırken Intune ve koşullu erişim](./media/conditional-access/intune-with-ca-1.png)

Intune ile koşullu erişim kullanmanın yolları:

- **Cihaz tabanlı koşullu erişim**

  - Şirket içi Exchange için koşullu erişim

  - Ağ erişim denetimi tabanlı koşullu erişim

  - Cihaz riskine dayalı koşullu erişim

  - Windows bilgisayarları için koşullu erişim

    - Şirkete ait

    - Kendi cihazını getir (KCG)

- **Uygulamaya bağlı koşullu erişim**

## <a name="next-steps"></a>Sonraki adımlar

[Intune ile koşullu erişim kullanmanın yaygın yolları](conditional-access-intune-common-ways-use.md)