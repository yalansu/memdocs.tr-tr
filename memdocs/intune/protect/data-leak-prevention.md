---
title: Yönetilmeyen cihazlarda veri sızıntılarını önleme
titleSuffix: Microsoft Intune
description: Microsoft Intune kullanarak cihazlardaki kurumsal verilere erişim izni verin ve verileri sızıntılara karşı koruyun.
keywords: veri koruma cihaz M365 sızıntılarını engelliyor Microsoft 365
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: b1512c3a-3bbd-4111-a0df-c874a0a335df
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c979d6cf35611a419c4e27605b696c6ad3d85cd9
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996189"
---
# <a name="prevent-data-leaks-on-non-managed-devices-using-microsoft-intune"></a>Microsoft Intune kullanarak yönetilmeyen cihazlarda veri sızıntılarını önleme

Microsoft 365 tarafından barındırılan şirket verilerine erişime izin verirseniz, kullanıcıların kasıtlı olarak veya yanlışlıkla veri sızıntılarını etkilemeden verileri nasıl paylaştığından ve kaydettiden kontrol edebilirsiniz. Microsoft Intune, kullanıcılara ait cihazlarda şirket verilerinizin güvenliğini sağlamak için ayarlayabileceğiniz uygulama koruma ilkeleri sağlar. Cihazların Intune hizmetine kaydedilmesi gerekmez. 

Intune ile ayarlanan uygulama koruma ilkeleri, Microsoft olmayan bir cihaz yönetim çözümü ile yönetilen cihazlarda da çalışır. BT departmanı cihazlardaki kişisel verilere dokunmaz; yalnızca şirket verilerini yönetir. 

Şirket verilerini korumak için Windows, iOS/ıpados veya Android çalıştıran cihazlarda Office mobil uygulamaları için uygulama koruma ilkeleri ayarlayabilirsiniz. Bu ilkeler uygulama tabanlı PIN veya şirket veri şifrelemesi gibi ilkeler belirlemenize veya kullanıcıların yönetilen ve yönetilmeyen uygulamalar arasında kesme, kopyalama ve yapıştırma özelliklerini kullanmasını sınırlamak için daha gelişmiş ayarlar yapmanıza izin verir. Ayrıca, kullanıcıların cihazlarını kaydetmesi gerekmeden şirket verilerini uzaktan silebilirsiniz.

Intune uygulama koruma ilkeleri, cihaz yönetiminden bağımsızdır. Uygulama koruma ilkeleri, Office mobil uygulamalarını gerek yönetilmeyen gerekse Intune tarafından yönetilen cihazların yanı sıra Microsoft olmayan MDM çözümleriyle yönetilen cihazlarda yönetmenize izin verir.

## <a name="before-you-begin"></a>Başlamadan önce

Aşağıdaki koşulları yerine getirdiğinizde aşağıdaki eylem planı kullanılabilir:

* Şirketiniz buluta güvenli bir şekilde geçiş yapmaya hazırdır.
* Şirketiniz Exchange Online, SharePoint Online, OneDrive Iş veya Yammer Microsoft 365 kullanıyor.
* Şirketinizin Microsoft 365, Enterprise Mobility + Security (EMS) veya Azure Information Protection lisansları vardır.
* Şirketiniz, kullanıcıların şirkete ait veya kişisel Windows, iOS/ıpados veya Android cihazlarından şirket verilerine erişmesini sağlar.
* Şirketiniz, kişisel cihazların bir cihaz yönetim hizmetine kaydedilmesini zorunlu kılmak istemiyordur.

## <a name="action-plan"></a>Eylem planı

İOS/ıpados ve Android cihazlar için:

1. [Uygulama koruma ilkelerinin](../apps/app-protection-policy.md) nasıl çalıştığını öğrenin.
2. Office mobil uygulamaları için nasıl [uygulama koruma ilkeleri oluşturulup dağıtılacağını](../apps/app-protection-policies.md) öğrenin.
3. Oluşturup dağıttığınız [uygulama koruma ilkelerini izleyin](../apps/app-protection-policies-monitor.md).

Windows 10 cihazları için:

1. [Windows Bilgi Koruması’nın (WIP) nasıl çalıştığını](/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) öğrenin.
2. [Windows 10 için uygulama koruma ilkelerini](../apps/app-protection-policies-configure-windows-10.md)yapılandırmaya hazırlanın.
3. [Intune ile WIP uygulama koruma ilkeleri oluşturun ve dağıtın](../apps/windows-information-protection-policy-create.md).

## <a name="what-to-tell-employees-and-students"></a>Çalışanlara ve öğrencilere söylenecekler

Gerektiğinde, ek bilgi sağlamak için aşağıdaki bağlantıları paylaşın:

* [İOS/ıpados uygulamanız uygulama koruma ilkeleriyle yönetildiğinde beklemeniz gerekenler](../fundamentals/end-user-mam-apps-ios.md)
* [Android uygulamanız uygulama koruma ilkeleriyle yönetildiğinde beklemeniz gerekenler](../fundamentals/end-user-mam-apps-android.md)

## <a name="next-steps"></a>Sonraki adımlar

Bu veya diğer EMS veya Microsoft 365 senaryolarını etkinleştirmeye yardım mı istiyorsunuz? Microsoft 365, Enterprise Mobility + Security veya Azure Active Directory Premium için en az 150 lisansınız varsa, [FastTrack avantajlarınızdan](/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program) yararlanın.
