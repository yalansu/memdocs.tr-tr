---
title: Microsoft Intune - Azure ile cihazları yeniden başlatma | Microsoft Docs
description: Uzak yeniden başlatma eylemini kullanarak Azure portal Microsoft Intune kullanarak Windows ve iOS/ıpados cihazlarını yeniden başlatın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 45317cc9c43f4f25f0adc043ce784a7b3dc4b9fd
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461785"
---
# <a name="remotely-restart-devices-with-intune"></a>Cihazları Intune ile uzaktan başlatma


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Cihazı **Yeniden Başlat** eylemi, seçtiğiniz cihazın yeniden başlatılmasını sağlar (5 dakika içinde). Yeniden başlatma işlemi cihaz sahibine otomatik olarak bildirilmez ve cihaz sahibi çalışmasını kaybedebilir.

## <a name="supported-platforms"></a>Desteklenen platformlar

- Windows - Windows 8.1 ve üzerinde desteklenir
- Windows Phone - Windows Phone 8.1 ve sonraki sürümlerde desteklenir
- Android kurumsal adanmış cihazlar-Android 7,0 ve üzeri sürümlerde desteklenir
- Android kurumsal tam yönetilen cihazlar-Android 6,0 ve üzeri sürümlerde desteklenir
- Android Enterprise şirkete ait iş profili cihazları-Android 8,0 ve üzeri sürümlerde desteklenir
- iOS/ıpados-destekleniyor

    > [!Note]  
    > Bu komut için, denetlenen bir cihaz ve **Cihaz Kilidi** erişim hakkı gerekir. Cihaz hemen yeniden başlatılır. Geçiş kodu-kilitli iOS/ıpados cihazları yeniden başlattıktan sonra Wi-Fi ağına yeniden katılmaz. Yeniden başlatma sonrasında, cihaz sunucuyla iletişim kuramayabilir.
- macOS - Desteklenmiyor
- Android ve Android iş profili cihazları - Desteklenmiyor

## <a name="restart-a-device"></a>Cihazı yeniden başlatma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Cihazlar**  >  **tüm cihazlar**' ı seçin.
4. Yönettiğiniz cihazların listesinde bir cihaz seçin > Evet ' i **yeniden başlatın**  >  **Yes**.

## <a name="next-steps"></a>Sonraki adımlar

- **Yeniden başlat** cihaz eyleminin durumunu görmek için **Cihazlar** > **Cihaz eylemleri**'ni seçin.
