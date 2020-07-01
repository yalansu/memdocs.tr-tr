---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590550"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a>Azure AD kimlik doğrulaması çalışmıyor
<!--7569264-->
Configuration Manager Azure Active Directory (Azure AD) güvenlik belirteci hizmeti 'nin kullanımı çalışmıyor. Yönetim noktasındaki **CCM_STS. log** Şu hataya benzer bir giriş içeriyor: `ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` Ayrıca HRESULT 0x80131040 de dahildir.

Başka bir belirti, bir bulut yönetimi ağ geçidi (CMG) ile ilgili sorunlardır. CMG bağlantı çözümleyici 'yi çalıştırırsanız şu hata ile yönetim noktası için CMG kanalını test etme işlemi başarısız olur:`Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

Bu sorun, destekleyen bir kitaplıkla bir sürüm uyuşmazlığı nedeniyle oluşur.

Bu sorunu geçici olarak çözmek için, site sunucusundaki yükleme dizininin \X64 klasöründen **System.IdentityModel.Tokens.JWT.dll** yönetim noktasındaki SMS_CCM \ CCM_STS \bin klasörüne kopyalayın.
