---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle saldırı hesabı koruma ayarlarını yönetme | Microsoft Docs
description: Microsoft Endpoint Manager 'daki Endpoint Security hesabı koruma ilkesi ayarlarıyla yönettiğiniz cihazlar için ilkeleri yapılandırın ve dağıtın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f08282fe6bd8675474415290d50c0b07b4e1fc25
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915067"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Intune 'da Endpoint Security için hesap koruma ilkesi

Kullanıcılarınızın kimliğini ve hesaplarını korumak için hesap koruması için Intune uç nokta güvenlik ilkelerini kullanın. Hesap koruma ilkesi, Windows kimlik ve erişim yönetiminin bir parçası olan Windows Hello ve Credential Guard ayarlarına odaklanır.

- *İş Için Windows Hello* , bilgisayarlarda ve mobil cihazlarda güçlü iki öğeli kimlik doğrulama ile parolaları değiştirir.
- *Credential Guard* , cihazlarınızla birlikte kullandığınız kimlik bilgilerini ve gizli dizileri korumanıza yardımcı olur.

Daha fazla bilgi edinmek için bkz. Windows kimlik ve erişim yönetimi belgelerindeki [kimlik ve erişim yönetimi](/windows/security/identity-protection/) .

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin **uç nokta güvenlik** düğümünde *Yönet* bölümünde hesap koruması için uç nokta güvenlik ilkelerini bulun.

[Hesap koruma profillerinin ayarlarını](../protect/endpoint-security-asr-profile-settings.md)görüntüleyin.

## <a name="prerequisites-for-account-protection-profiles"></a>Hesap koruma profillerinin önkoşulları

- Windows 10 veya üzeri

## <a name="account-protection-profiles"></a>Hesap koruma profilleri

*Hesap koruma profilleri önizlemededir*.

**Windows 10 profilleri**:

- **Hesap koruması** *(Önizleme)* – hesap koruma ilkeleri ayarları, Kullanıcı kimlik bilgilerini korumanıza yardımcı olur.

## <a name="next-steps"></a>Sonraki adımlar

[Uç nokta güvenlik ilkelerini yapılandırma](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)