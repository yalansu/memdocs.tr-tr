---
title: Microsoft Intune - Azure ile cihazları yeniden başlatma | Microsoft Docs
description: Uzak yeniden başlatma eylemini kullanarak Azure portal Microsoft Intune kullanarak Windows ve iOS/ıpados cihazlarını yeniden başlatın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: adbc96dade5b6da134fa8a22f2cb613fc0baa923
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326319"
---
# <a name="remotely-restart-devices-with-intune"></a>Cihazları Intune ile uzaktan başlatma


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Cihazı **Yeniden Başlat** eylemi, seçtiğiniz cihazın yeniden başlatılmasını sağlar (5 dakika içinde). Yeniden başlatma işlemi cihaz sahibine otomatik olarak bildirilmez ve cihaz sahibi çalışmasını kaybedebilir.

## <a name="supported-platforms"></a>Desteklenen platformlar

- Windows - Windows 8.1 ve üzerinde desteklenir
- Windows Phone - Windows Phone 8.1 ve sonraki sürümlerde desteklenir
- Android bilgi noktası cihazları-Android 7,0 ve üzeri sürümlerde desteklenir
- iOS/ıpados-destekleniyor

    > [!Note]  
    > Bu komut için, denetlenen bir cihaz ve **Cihaz Kilidi** erişim hakkı gerekir. Cihaz hemen yeniden başlatılır. Geçiş kodu-kilitli iOS/ıpados cihazları yeniden başlattıktan sonra Wi-Fi ağına yeniden katılmaz. Yeniden başlatma sonrasında, cihaz sunucuyla iletişim kuramayabilir.
- macOS - Desteklenmiyor
- Android ve Android iş profili cihazları - Desteklenmiyor

## <a name="restart-a-device"></a>Cihazı yeniden başlatma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Cihazlar** > **Tüm cihazlar**’ı seçin.
4. Yönettiğiniz cihazların listesinde bir cihaz seçin > **yeniden başlat** ** > .**

## <a name="next-steps"></a>Sonraki adımlar

- **Yeniden başlat** cihaz eyleminin durumunu görmek için **Cihazlar** > **Cihaz eylemleri**'ni seçin.