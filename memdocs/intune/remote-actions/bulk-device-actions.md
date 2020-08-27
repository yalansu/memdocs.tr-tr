---
title: Microsoft Intune cihazında toplu cihaz eylemlerini kullanın.
titleSuffix: ''
description: Toplu uzak cihaz eylemlerini kullanın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c00e124c9f2741c3b94b08b51a6d1d897086087
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914421"
---
# <a name="use-bulk-device-actions"></a>Toplu cihaz eylemlerini kullanma

Aşağıdaki uzak eylemler için toplu cihaz eylemlerini kullanabilirsiniz:
- [Autopilot sıfırlaması](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Özel bildirimler](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Silme](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Yeniden Adlandır](device-rename.md)
- [Yeniden başlat](device-restart.md)
- [Eşitle](device-sync.md)
- [Silme](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Toplu cihaz eylemi kullanma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihazlar**  >  **tüm cihazlar**  >  **toplu cihaz eylemleri**' ni seçin.
![Toplu cihaz eylemleri](./media/bulk-device-actions/bulk-device-actions.png)
3. **Toplu cihaz eylemi** sayfasında bir **Işletim sistemi** ve **cihaz eylemi**seçin. Bazı cihaz eylemlerinin doldurulması için ek seçenekleri veya alanları vardır. **İleri**’yi seçin.
4. **Cihazlar** sayfasında, 1 ile 100 arasında cihazlar ' ı **seçin >.**
5. **Gözden geçir + oluştur** sayfasında **Oluştur**' u seçin.

## <a name="next-steps"></a>Sonraki adımlar
[Cihaz yönetimine genel bakış.](device-management.md)