---
title: Microsoft Intune’da Windows cihazları için Wi-Fi ayarlarını içeri aktarma - Azure | Microsoft Docs
description: Netsh wlan kullanarak Wi-Fi ayarlarını bir Windows cihazından dışarı aktarın. Ardından, Windows 8.1, Windows 10 ve Windows Holographic for Business çalıştıran cihazlara Wi-Fi profili oluşturmak için bu dosyayı Intune’da içeri aktarın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d17614424cdb20d2d88d818fcdd015c229150d66
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556345"
---
# <a name="import-wi-fi-settings-for-windows-devices-in-intune"></a>Intune’da Windows cihazları için Wi-Fi ayarlarını içeri aktarma

Windows çalıştıran cihazlar için daha önce bir dosyaya aktarılmış Wi-Fi yapılandırma profilini içeri aktarabilirsiniz. **Windows 10 ve sonrası cihazlar için doğrudan Intune’da [Wi-Fi profili de oluşturabilirsiniz](wi-fi-settings-windows.md)**.

Bu özellik şu platformlarda geçerlidir:

- Windows 8.1 ve üzeri
- Windows 10 ve üzeri
- Windows 10 masaüstü veya mobil
- Windows 10 Holographic for Business

## <a name="before-you-begin"></a>Başlamadan önce

[Cihaz profili oluşturma](wi-fi-settings-configure.md). Profil adı, Wi-Fi profili xml dosyasındaki Name özniteliğiyle aynı **olmalıdır** . Yoksa işlem başarısız olur.

## <a name="import-the-wi-fi-settings-into-intune"></a>Wi-Fi ayarlarını Intune'da içeri aktarma

- **Bağlantı adı**: Wi-Fi bağlantısı için bir ad girin. Bu ad, kullanılabilir Wi-Fi ağlarına gözatarken kullanıcılara gösterilir.
- **PROFIL XML**'i: tarayıcı düğmesini seçin ve içeri aktarmak istediğiniz Wi-Fi profili AYARLARıNı içeren XML dosyasını seçin.
- **Dosya içeriği**: Seçtiğiniz yapılandırma profili için XML kodunu görüntüler.

## <a name="export-wi-fi-settings-from-a-windows-device"></a>Windows cihazından Wi-Fi ayarlarını dışarı aktarma

Windows’ta `netsh wlan` kullanarak mevcut bir Wi-Fi profilini Intune tarafından okunabilen bir XML dosyasına aktarın. Profili başarıyla kullanmak için anahtarın düz metin olarak dışarı aktarılması gerekir.

Gerekli WiFi profilinin zaten yüklü olduğu bir Windows bilgisayarda aşağıdaki adımları kullanın:

1. **C:\wifi**gibi, aktarılmış Wi-Fi profilleri için yerel bir klasör oluşturun.
2. Yönetici olarak bir komut istemi açın.
3. `netsh wlan show profiles` komutunu çalıştırın. Dışarı aktarmak istediğiniz profilin adını aklınızda edin. Bu örnekte, profil adı **Wifiname**' dır.
4. `netsh wlan export profile name="ProfileName" folder=c:\Wifi` komutunu çalıştırın. Bu komut, hedef klasörünüzde **Wi-Fi-WiFiName.xml** adlı bir Wi-Fi profil dosyası oluşturur.

> [!IMPORTANT]
>
> - Önceden paylaşılan anahtar içeren bir Wi-Fi profilini dışarı aktarıyorsanız komuta eklemeniz **gerekir** `key=clear` . Örneğin şunu girin: 
>
>   `netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi`
>
> - Windows 10 ile önceden paylaşılan bir anahtar kullanılması, Intune 'da bir düzeltme hatasına neden olur. Bu durumda, Wi-Fi profili cihaza düzgün bir şekilde atanır ve profil beklendiği gibi çalışır.
> - Önceden paylaşılan anahtar içeren bir Wi-Fi profilini dışarı aktarıyorsanız dosyanın korumalı olduğundan emin olun. Anahtar düz metin biçimindedir, yani anahtarı korumak sizin sorumluluğunuzdadır.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

Diğer kullanılabilir platformlar da dahil olmak üzere [Wi-Fi ayarlarına genel bakış](wi-fi-settings-configure.md)bölümüne bakın.
