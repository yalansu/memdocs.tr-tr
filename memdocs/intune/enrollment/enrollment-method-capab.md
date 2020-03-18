---
title: Windows cihazları için Intune kayıt yöntemi özellikleri
titleSuffix: Microsoft Intune
description: Windows cihazlarına yönelik kayıt yöntemlerinin özellikleri.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/21/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b9dca2303d960937a529a902391d6c05539fc9d4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331550"
---
# <a name="intune-enrollment-method-capabilities-for-windows-devices"></a>Windows cihazları için Intune kayıt yöntemi özellikleri
[!INCLUDE[azure_portal](../includes/azure_portal.md)]

İş gücünüzün cihazlarını Intune 'a kaydetmek için çeşitli yöntemler vardır. Aşağıdaki tabloda gösterildiği gibi her yöntemin farklı en iyi yöntemleri ve özellikleri vardır.

## <a name="best-practices-by-enrollment-method"></a>Kayıt yöntemine göre en iyi yöntemler
| **En iyi uygulamalar** | **[Azure AD'ye katılanlar](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Azure AD'ye Autopilot ile katılanlar (Kullanıcı sürümlü mod)](enrollment-autopilot.md)** |**[Azure AD'ye Autopilot ile katılanlar (Otomatik dağıtım modu)](enrollment-autopilot.md)** |**[Toplu](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[KCG](device-enrollment.md#bring-your-own-device)** | **[GPO](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Ortak yönetim](https://docs.microsoft.com/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Eğitimde yaygın olarak kullanılanlar|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Cihazlar, paylaşılan cihazlar olarak kullanılabilir|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Kişisel cihazlar şirket kaynaklarına erişmelidir|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Uygulamalara self servis bakım|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>Kayıt yöntemine göre özellikler

| **Yetenekler** | **[Azure AD'ye katılanlar](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Azure AD'ye Autopilot ile katılanlar (Kullanıcı sürümlü mod)](enrollment-autopilot.md)** |**[Azure AD'ye Autopilot ile katılanlar (Otomatik dağıtım modu)](enrollment-autopilot.md)** |**[Toplu](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[KCG](device-enrollment.md#bring-your-own-device)** | **[GPO](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Ortak yönetim](https://docs.microsoft.com/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Koşullu Erişim                                      |![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)\*\*|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|
|Kullanıcılar cihazla ilişkilendirilir                    |![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|
|Azure AD Premium gerektirir                               |![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|
|Cihaz CA tarafından korunan kaynakları değerlendirebilir             |![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|
|Kullanıcılar cihazlarında yönetici olmamalıdır               |![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Cihaz kurulum deneyimini yapılandırma olanağı        |![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Cihazları kullanıcı etkileşimi olmadan kaydetme olanağı      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|
|PowerShell betikleri çalıştırma olanağı                       |![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/checkmark.png)\*| 
|AD etki alanına katılmadan sonra otomatik kaydı destekler      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|
|Hibrit Azure AD'ye katılmadan sonra otomatik kaydı destekler|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|
|Hibrit Azure AD'ye katılmadan sonra otomatik kaydı destekler       |![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|

\* Istemci uygulamaları iş yüklerinin Configuration Manager Intune pilot 'a veya Intune 'a taşınması gerekir.

\** [cihaz, Windows 10 1803 + dışında koşullu erişim için engellenir.](device-enrollment-manager-enroll.md)

## <a name="next-steps"></a>Sonraki adımlar

[Windows için kayıt ayarlama](windows-enroll.md)

