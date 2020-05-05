---
title: Microsoft Intune ile Windows 10 sanal makinelerini kullanma
titleSuffix: ''
description: Microsoft Intune ile Windows 10 sanal makinelerini kullanma yönergeleri
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 944b3d98dc59dcae69f72fef5dfdb1793701f67a
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126186"
---
# <a name="using-windows-10-virtual-machines-with-intune"></a>Intune ile Windows 10 sanal makinelerini kullanma

Intune, Windows 10 Enterprise çalıştıran sanal makinelerin belirli sınırlamalara sahip olarak yönetilmesini destekler. Intune yönetimi, aynı sanal makinenin Windows sanal masaüstü yönetimini etkilemez veya buna engel olmaz.

Intune ile Windows 10 VM 'Leri yönetirken aşağıdaki noktaları göz önünde bulundurun:

- Windows sanal masaüstü 'nde kullanılan Windows 10 Enterprise çoklu oturum (sanal cihazlar için Enterprise) Şu anda Intune yönetimini desteklememektedir.

## <a name="enrollment"></a>Kayıt
- Intune ile isteğe bağlı, oturum ana bilgisayar sanal makinelerini yönetmeyi önermiyoruz. Her sanal makinenin oluşturulduğu zaman kayıtlı olması gerekir. Ayrıca, sanal makineleri düzenli olarak silmek, [temizlenene](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules)kadar yalnız bırakılmış cihaz kayıtlarını Intune 'da bırakır. 
- Windows Autopilot kendi kendine dağıtma ve teknik bakış dağıtım türleri, fiziksel Güvenilir Platform Modülü (TPM) gerektirdiğinden desteklenmez. 
- Kullanıma hazır deneyim (OOBE) kaydı, yalnızca RDP kullanılarak erişilebilen VM 'lerde desteklenmez (Azure üzerinde barındırılan VM 'Ler gibi). Bu kısıtlama şu anlama gelir:
    - Windows Autopilot ve ticari OOBE desteklenmez.
    - Cihaz bağlamı ilkeleri için kayıt durumu sayfası seçenekleri desteklenmez.


## <a name="configuration"></a>Yapılandırma
Intune, aşağıdakiler de dahil olmak üzere Güvenilir Platform Modülü veya donanım yönetimi kullanan herhangi bir yapılandırmayı desteklemez:
- [BitLocker ayarları](../configuration/device-profiles.md#endpoint-protection)
- [Cihaz üretici yazılımı yapılandırma arabirimi ayarları](../configuration/device-profiles.md#device-firmware-configuration-interface)

## <a name="reporting"></a>Raporlama
Intune, sanal makineleri otomatik olarak algılar ve **cihazlar** > **tüm cihazlarda** "sanal makine" olarak raporlar > bir cihaz > **genel bakış** > **modeli** alanı seçin. 

Serbest bırakılmış sanal makineler [, Intune hizmetine iade](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)kuramadığı için uyumsuz cihaz raporlarına katkıda bulunabilir.

## <a name="retirement"></a>Devre dışı bırakma
Yalnızca RDP erişiminiz varsa [silme eylemini](../remote-actions/devices-wipe.md#wipe)kullanmayın. Silme eylemi, sanal makinenin RDP ayarlarını silecek ve yeniden bağlanmanızı engelleyecek.


