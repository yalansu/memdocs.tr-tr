---
title: Intune’da modern kimlik doğrulaması olmayan uygulamaları engelleme
titleSuffix: Microsoft Intune
description: Microsoft Intune kullanarak uygulamalar ve modern kimlik doğrulaması (ADAL) hakkında bilgi edinin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/22/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4703288faac219b40fae08c6551425d6f0d5e4f3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909423"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Modern kimlik doğrulaması (ADAL) kullanmayan uygulamaları engelleme

> [!NOTE]
> Azure Active Directory (Azure AD) kimlik doğrulama kitaplığı (ADAL) ve Azure AD Graph API kullanım dışı bırakılacak. Daha fazla bilgi için bkz. [Microsoft kimlik doğrulama kitaplığı 'nı (msal) ve Microsoft Graph API 'sini kullanacak şekilde uygulamalarınızı güncelleştirme](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Uygulama koruma ilkeleriyle uygulama tabanlı koşullu erişim, OAuth2 uygulamasının bir uygulaması olan [modern kimlik doğrulaması](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)kullanan uygulamalara güvenir. Şu anda çoğu Office mobil ve masaüstü uygulaması modern kimlik doğrulaması kullanmaktadır. Ancak, temel kimlik doğrulaması ve form tabanlı kimlik doğrulaması gibi diğer kimlik doğrulama yöntemlerini kullanan üçüncü taraf uygulamaları ve eski Office uygulamaları vardır.

## <a name="block-access-to-apps"></a>Uygulama erişimini engelleme

Modern kimlik doğrulaması kullanmayan uygulamalara erişimi engellemek için, koşullu erişim uygulamak üzere Intune uygulama koruma ilkelerini kullanın. Daha fazla bilgi için bkz. [Intune Ile uygulama tabanlı koşullu erişim](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Ek bilgiler

Azure AD Koşullu Erişim hakkında daha fazla bilgi için aşağıdaki konulara bakın:
- [Azure Active Directory Koşullu erişim nedir?](/azure/active-directory/conditional-access/overview)
- [Uygulama tabanlı Koşullu erişimin nasıl çalıştığı](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Azure Active Directory Koşullu erişim için SharePoint Online ve Exchange Online 'ı ayarlama](/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Sonraki adımlar

- [Intune ile uygulama tabanlı koşullu erişim](app-based-conditional-access-intune.md)