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
ms.openlocfilehash: 701794ba476f87aaf079e39c834f3e8e3f2c280d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913894"
---
# <a name="intune-enrollment-method-capabilities-for-windows-devices"></a>Windows cihazları için Intune kayıt yöntemi özellikleri
[!INCLUDE[azure_portal](../includes/azure_portal.md)]

İş gücünüzün cihazlarını Intune 'a kaydetmek için çeşitli yöntemler vardır. Aşağıdaki tabloda gösterildiği gibi her yöntemin farklı en iyi yöntemleri ve özellikleri vardır.

## <a name="best-practices-by-enrollment-method"></a>Kayıt yöntemine göre en iyi yöntemler
| **En iyi uygulamalar** | **[Azure AD'ye katılanlar](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Azure AD'ye Autopilot ile katılanlar (Kullanıcı sürümlü mod)](../../autopilot/enrollment-autopilot.md)** |**[Azure AD'ye Autopilot ile katılanlar (Otomatik dağıtım modu)](../../autopilot/enrollment-autopilot.md)** |**[Toplu](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[KCG](device-enrollment.md#bring-your-own-device)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Ortak yönetim](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Eğitimde yaygın olarak kullanılanlar|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Cihazlar, paylaşılan cihazlar olarak kullanılabilir|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Kişisel cihazlar şirket kaynaklarına erişmelidir|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Uygulamalara self servis bakım|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|![Onay işareti](./media/enrollment-method-capab/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>Kayıt yöntemine göre özellikler

| **Özellikler** | **[Azure AD'ye katılanlar](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Azure AD'ye Autopilot ile katılanlar (Kullanıcı sürümlü mod)](../../autopilot/enrollment-autopilot.md)** |**[Azure AD'ye Autopilot ile katılanlar (Otomatik dağıtım modu)](../../autopilot/enrollment-autopilot.md)** |**[Toplu](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[KCG](device-enrollment.md#bring-your-own-device)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Ortak yönetim](/configmgr/core/clients/manage/co-management-overview)** |
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

\* Configuration Manager içindeki istemci uygulamaları iş yükleri, Intune pilot veya Intune 'a taşınmalıdır.

\** [Cihazlar Windows 10 1803 + dışında koşullu erişim için engellenir.](device-enrollment-manager-enroll.md)

## <a name="next-steps"></a>Sonraki adımlar

[Windows için kaydı ayarlama](windows-enroll.md)