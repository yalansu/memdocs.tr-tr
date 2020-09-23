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
ms.openlocfilehash: c427d6aa57220fed4e5a16db94985f449298d32f
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91008364"
---
# <a name="using-windows-10-virtual-machines-with-intune"></a>Intune ile Windows 10 sanal makinelerini kullanma

Intune, Windows 10 Enterprise çalıştıran sanal makinelerin belirli sınırlamalara sahip olarak yönetilmesini destekler. Intune yönetimi, aynı sanal makinenin Windows sanal masaüstü yönetimini etkilemez veya buna engel olmaz.

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
Intune, sanal makineleri otomatik olarak algılar ve **cihazlar**tüm cihazlarda "sanal makine" olarak raporlar  >  **All devices** > bir cihaz > **genel bakış**  >  **modeli** alanı seçin. 

Serbest bırakılmış sanal makineler [, Intune hizmetine iade](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)kuramadığı için uyumsuz cihaz raporlarına katkıda bulunabilir.

## <a name="retirement"></a>Devre dışı bırakma
Yalnızca RDP erişiminiz varsa [silme eylemini](../remote-actions/devices-wipe.md#wipe)kullanmayın. Silme eylemi, sanal makinenin RDP ayarlarını silecek ve yeniden bağlanmanızı engelleyecek.

## <a name="next-steps"></a>Sonraki adımlar
[Intune ile Windows sanal masaüstü kullanımı hakkında bilgi edinin](windows-virtual-desktop.md)
