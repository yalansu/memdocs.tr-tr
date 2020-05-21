---
title: Intune Endpoint Security hesabı koruma ilkesi ayarları | Microsoft Docs
description: Microsoft Intune uç nokta güvenlik hesabı koruma ilkesi ayarları
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431412"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Intune 'da Endpoint Security için hesap koruma ilkesi ayarları

[Endpoint Security ilkesinin](../protect/endpoint-security-policy.md)bir parçası olarak, Intune 'un uç nokta güvenlik düğümündeki *Hesap koruma* ilkesi için profillerde yapılandırabileceğiniz ayarları görüntüleyin.

Desteklenen platformlar ve profiller:

- **Windows 10 ve üzeri**:
  - Profil: **hesap koruması** *(Önizleme)*


## <a name="account-protection-profile"></a>Hesap koruma profili

### <a name="account-protection"></a>Hesap koruması

- **Iş için Windows Hello 'Yu engelle**

  Iş için Windows Hello, parolaları, akıllı kartları ve sanal akıllı kartları değiştirerek Windows 'da oturum açmak için alternatif bir yöntemdir.
  - **Yapılandırılmadı** (*varsayılan*)-cihazlar Iş için Windows Hello 'yu temin etmez.
  - **Devre dışı** -cihazlar Iş Için Windows Hello 'yu temin edin.
  - **Etkin** -cihazlar herhangi bir kullanıcı için Iş Için Windows Hello 'yu sağlamalardır
  
- **Oturum açma için güvenlik anahtarlarını kullanmak üzere etkinleştirin**

  Kiracıdaki tüm bilgisayarlar için oturum açma kimlik bilgileri olarak Windows Hello güvenlik anahtarını etkinleştirin.
  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**

- **Credential Guard 'ı aç**  
  [CSP: [] DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard, korumalar sağlamak için Windows Hiper Yöneticisi 'ni kullanır. Credential Guard, güvenli önyükleme ve DMA korumaları için donanım desteği gerektirir. Bu ayar yalnızca donanım gereksinimlerini karşılayan cihazlarda başarılı olur.
  - **Yapılandırılmadı** (*varsayılan*)-Windows varsayılan olan Credential Guard 'ın kullanımını devre dışı bırakın.
  - **UEFI kilidi Ile etkinleştirin** -Credential Guard 'ı ETKINLEŞTIRIN ve UEFI kalıcı yapılandırma el ile temizlendiğinden uzaktan kapatılmasını engelleyin.
  - **UEFI kilidi olmadan etkinleştirin** -Credential Guard 'ı etkinleştirin ve makinenin makineye fiziksel erişimi olmadan kapatılmış olmasını sağlayın.

## <a name="next-steps"></a>Sonraki adımlar

[Hesap koruması için uç nokta güvenlik ilkesi](../protect/endpoint-security-account-protection-policy.md)
