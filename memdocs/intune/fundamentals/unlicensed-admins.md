---
title: Microsoft Intune 'de lisanssız Yöneticiler
description: Intune 'a erişim için lisanssız Yöneticiler izinleri verme hakkında bilgi edinin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: a5f479dcad0c293c547edec24f0f835a4fc987e1
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574839"
---
# <a name="unlicensed-admins"></a>Lisansı kaldırılan yöneticiler

> [!Important]
> Bu seçenek yalnızca yöneticilerin Microsoft Uç Nokta Yöneticisi 'ne erişmesi için lisans gereksinimini ortadan kaldırır. Azure Active Directory Premium gibi diğer özelliklerin veya hizmetlerin kullanımı yine de yönetici için lisans gerektirebilir.

Intune/Microsoft Endpoint Manager Yönetim Merkezi 'ne Intune lisansı olmadan Yöneticiler için erişim izni verebilirsiniz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **kiracı yönetim**  >  **rolleri**  >  **yönetici lisansı**' nda oturum açın.
2. **Lisanssız yöneticilere erişime izin ver**  >  **Evet**' i seçin.
    >[!WARNING]
    >**Evet**' i tıkladıktan sonra bu ayarı geri alamazsınız.

3. Artık, Microsoft Endpoint Manager Yönetim merkezinde oturum açan kullanıcılar bir Intune lisansı gerektirmez. Erişim kapsamları kendilerine atanan roller tarafından tanımlanır.

Intune, güvenlik grubu başına en fazla 350 lisanssız yönetici destekler ve yalnızca doğrudan Üyeler için geçerlidir. Bu sınırın üzerinde bulunan Yöneticiler öngörülemeyen davranışla karşılaşacaktır.




