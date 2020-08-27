---
title: Cihaz yönetimi olmadan Exchange
titleSuffix: Microsoft Intune
description: Microsoft Intune'u kullanarak, bir cihaz yönetim sistemi ayarlamadan çalışanlara Office 365 Exchange Online e-postalarına erişim verin.
keywords: Office 365 Exchange e-posta erişimi
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/31/2017
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.topic: archived
ms.technology: ''
ms.assetid: 88a0d3b9-2622-403b-8374-1396afd8066e
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41782c13e3e1cfb8b0c9952a52a60e2ee0baf7ca
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909168"
---
# <a name="protect-office-365-exchange-online-without-requiring-device-management"></a>Cihaz yönetimi gerektirmeden Office 365 Exchange Online’ı koruma

Bir cihaz yönetim sistemi ayarlama zahmetine katlanmaksızın çalışanların e-posta adreslerine erişimini sağlamak istiyorsanız, bu mümkündür. Intune aracılığıyla Office 365 Exchange Online’a erişim verebilirsiniz. Gerekli adımları tamamlamak için Microsoft 365 veya Azure Active Directory (premium) ve Intune lisanslarınızın olduğunu onaylayın. Çalışanların [desteklenen bir iOS/ıpados veya Android cihazı](../fundamentals/supported-devices-browsers.md)olması gerekir. 

Bir cihaz yönetim sistemi ayarlamak istiyorsanız, bu da mümkündür. Bu tür bir uygulama koruması, cihaz yönetiminden bağımsız olarak çalışır. 

## <a name="action-plan"></a>Eylem planı

1. [Koşullu erişim hakkında bilgi edinin](conditional-access.md). 
2. [Uygulama tabanlı koşullu erişim hakkında bilgi edinin](app-based-conditional-access-intune.md).
3. [Exchange Online için uygulama tabanlı koşullu erişim Ilkeleri ayarlayın](app-based-conditional-access-intune-create.md).
4. [Yönetilmeyen](app-modern-authentication-block.md)uygulamaları, özellikle de Azure Active Directory kimlik doğrulaması KITAPLıĞı (ADAL) veya Microsoft kimlik doğrulama kitaplığı 'Nı (msal) kullanmayan uygulamaları engelleyin.
5. Seçim [SharePoint Online için uygulama tabanlı koşullu erişim Ilkeleri ayarlayın](app-based-conditional-access-intune-create.md). Bu ilkeler, yönetilemeyen ve güvende olmayan uygulamalardan şirket verilerinize erişimi engeller. Ayrıca SharePoint Mobile’dan erişimi de sınırlar. 

## <a name="what-to-tell-employees-and-students"></a>Çalışanlara ve öğrencilere söylenecekler

* Çalışanlarınızın ve öğrencilerinizin, Apple App Store 'dan veya Android için Microsoft Outlook veya Microsoft SharePoint for iOS/ıpados ' i indirip Google Play Store. 
* Modern kimlik doğrulaması kullanmayan uygulamalara erişimi engellerseniz, çalışanlarınızı ve öğrencilerinizi bu kısıtlamadan haberdar edin. 

## <a name="next-steps"></a>Sonraki adımlar

Şirket verilerinin güvenliğini artırmak için uygulama tabanlı koşullu erişim kullandınız. Sonraki adımların parçası olarak, şirket verilerinizin güvenliğini arttırmak için aşağıdaki gibi diğer yollar hakkında bilgi edinebilirsiniz: 

* [Active Directory ve Azure Active Directory cihaz uyumluluğu, cihaz riski, konum ve Kullanıcı özniteliklerine dayalı koşullu erişimi](/azure/active-directory/active-directory-conditional-access-azure-portal)ayarlama.  
* Kasıtlı veya kasıtsız veri sızıntılarına karşı şirketinizi korumaya yardımcı olmak adına uygulama koruma ilkeleri ayarlamak. 
* Şirket verilerini ağınız dışında da korumak adına Azure Information Protection’dan yararlanmak. 

Bunu veya diğer EMS ya da Office 365 senaryolarını etkinleştirmek için yardıma mı ihtiyacınız var? Microsoft 365, Enterprise Mobility + Security veya Azure Active Directory Premium için en az 150 lisansınız varsa, [FastTrack avantajlarınızdan](/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program) yararlanın.