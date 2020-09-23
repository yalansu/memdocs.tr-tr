---
title: Microsoft Intune ile Windows sanal masaüstü 'Nü kullanma
titleSuffix: ''
description: Microsoft Intune ile Windows sanal masaüstü kullanımı için yönergeler
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 9/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: madakeva
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64594332514004fbf75dfb1a86f1b0f346a336c9
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017742"
---
# <a name="using-windows-virtual-desktop-with-intune"></a>Windows sanal masaüstü 'Nü Intune ile kullanma

[Windows sanal masaüstü](https://docs.microsoft.com/azure/virtual-desktop/)   , Microsoft Azure üzerinde çalışan bir masaüstü ve uygulama sanallaştırma hizmetidir.Son kullanıcıların herhangi bir cihazdan tam bir masaüstüne güvenli bir şekilde bağlanmasına olanak sağlar. Microsoft Intune, Windows Sanal Masaüstü sanal makinelerinizi, ilke ve uygulamalarla, kaydolduktan sonra, ölçeklendirerek güvenli hale getirebilirsiniz ve yönetebilirsiniz. 

## <a name="prerequisites"></a>Önkoşullar 

Intune Şu anda Windows sanal masaüstü VM 'lerini destekler: 

- Windows 10 Enterprise, sürüm 1809 veya üstünü çalıştırma.
- [Karma Azure AD 'ye katılmış](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).
- Azure 'da [kişisel uzak masaüstü](https://docs.microsoft.com/azure/virtual-desktop/configure-host-pool-personal-desktop-assignment-type) olarak ayarlayın. 
- Intune 'A aşağıdaki yöntemlerden birine kayıtlı: 
    - Karma Azure AD 'ye katılmış cihazları otomatik olarak kaydetmek için [Active Directory Grup İlkesi](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) 'ni yapılandırın.
    - [Ortak yönetim Configuration Manager](https://docs.microsoft.com/configmgr/comanage/overview).
    - [Azure AD JOIN aracılığıyla Kullanıcı kendi kendine kayıt](../enrollment/windows-enrollment-methods.md#user-self-enrollment-in-intune).

Windows Sanal Masaüstü lisans gereksinimleri hakkında daha fazla bilgi için bkz. [Windows sanal masaüstü nedir?](https://docs.microsoft.com/azure/virtual-desktop/overview#requirements).

Intune, Windows sanal masaüstü kişisel VM 'Leri Windows 10 kurumsal fiziksel masaüstü ile aynı şekilde davranır. Bu işleme, mevcut yapılandırmalardan bazılarını kullanmanıza ve VM 'Lerin uyumluluk ilkesiyle ve koşullu erişime karşı korunmasına olanak tanır. Intune yönetimi, aynı sanal makinenin Windows sanal masaüstü yönetimine bağlı değildir veya bu yönetime engel olmaz. 

## <a name="limitations"></a>Sınırlamalar

Windows 10 Enterprise uzak masaüstlerini yönetirken aklınızda bulundurmanız gereken bazı sınırlamalar vardır: 

### <a name="configuration"></a>Yapılandırma

[Windows 10 sanal makineleri kullanılarak](windows-10-virtual-machines.md) LISTELENEN tüm VM sınırlamaları Windows sanal masaüstü VM 'leri için de geçerlidir.

Ayrıca, aşağıdaki profiller Şu anda desteklenmemektedir:
- [Etki alanına ekleme](../configuration/device-profiles.md#domain-join)
- [Wi-Fi](../configuration/device-profiles.md#wi-fi)

[RemoteDesktopServices/AllowUsersToConnectRemotely ilkesinin](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-allowuserstoconnectremotely) devre dışı olmadığından emin olun.

### <a name="remote-actions"></a>Uzak eylemler

Windows sanal masaüstü VM 'Leri için aşağıdaki Windows 10 Masaüstü cihaz uzak eylemleri desteklenmez/önerilmez:

- Autopilot sıfırlaması
- BitLocker anahtar döndürme
- Yeni Başlangıç
- Uzaktan kilitleme
- Parola sıfırlama
- Silme

### <a name="retirement"></a>Devre dışı bırakma

Azure 'dan VM 'Leri silmek, yalnız bırakılmış cihaz kayıtlarını Intune 'da bırakır. Kiracı için yapılandırılan Temizleme kurallarına göre otomatik olarak [temizlenir](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules) .

### <a name="windows-10-enterprise-multi-session"></a>Windows 10 Enterprise çoklu oturum

Intune Şu anda Windows 10 Enterprise çoklu oturum yönetimini desteklememektedir.

## <a name="next-steps"></a>Sonraki adımlar

[Windows sanal masaüstleri hakkında daha fazla bilgi edinin](https://docs.microsoft.com/azure/virtual-desktop/).