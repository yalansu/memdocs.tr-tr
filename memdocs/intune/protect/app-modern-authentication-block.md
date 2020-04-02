---
title: Intune’da modern kimlik doğrulaması olmayan uygulamaları engelleme
titleSuffix: Microsoft Intune
description: Microsoft Intune kullanarak uygulamalar ve modern kimlik doğrulaması (ADAL) hakkında bilgi edinin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f529a80403d27cf9d12c03c6090670095bf569fa
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329970"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Modern kimlik doğrulaması (ADAL) kullanmayan uygulamaları engelleme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Uygulama koruma ilkeleriyle uygulama tabanlı koşullu erişim, OAuth2 uygulamasının bir uygulaması olan [modern kimlik doğrulaması](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)kullanan uygulamalara güvenir. Şu anda çoğu Office mobil ve masaüstü uygulaması modern kimlik doğrulaması kullanmaktadır. Ancak, temel kimlik doğrulaması ve form tabanlı kimlik doğrulaması gibi diğer kimlik doğrulama yöntemlerini kullanan üçüncü taraf uygulamaları ve eski Office uygulamaları vardır.

## <a name="block-access-to-apps"></a>Uygulama erişimini engelleme

Modern kimlik doğrulaması kullanmayan uygulamalara erişimi engellemek için Intune uygulama koruması ilkelerini kullanarak koşullu erişimi yapılandırın. Daha fazla bilgi için bkz. [Intune Ile uygulama tabanlı koşullu erişim](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Ek bilgiler

Azure AD Koşullu Erişim hakkında daha fazla bilgi için aşağıdaki konulara bakın:
- [Azure Active Directory Koşullu erişim nedir?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Uygulama tabanlı Koşullu erişimin nasıl çalıştığı](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Azure Active Directory Koşullu erişim için SharePoint Online ve Exchange Online 'ı ayarlama](https://docs.microsoft.com/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Sonraki adımlar

- [Intune ile uygulama tabanlı koşullu erişim](app-based-conditional-access-intune.md)