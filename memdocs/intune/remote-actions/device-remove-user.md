---
title: Microsoft Intune ile bir iOS/ıpados aygıtından Kullanıcı kaldırma
titleSuffix: ''
description: Intune ile paylaşılan iOS/ıpados cihazından bir kullanıcıyı nasıl kaldıracağınızı öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed91d31a7085d023ef012e1dd30d86c833819ecc
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983073"
---
# <a name="remove-a-user-from-a-shared-iosipados-device"></a>Paylaşılan iOS/ıpados cihazından Kullanıcı kaldırma


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**Kullanıcı kaldır** eylemi, paylaşılan bir iPad cihazındaki yerel önbellekten seçtiğiniz kullanıcıyı siler. Bir [iOS/ıpados eğitim profili](../fundamentals/education-settings-configure-ios.md)kullanılarak IOS/ıpados sınıf uygulamasını yönetmek için iPad cihazı ayarlanmalıdır. 

## <a name="supported-platforms"></a>Desteklenen platformlar

- Windows - Desteklenmiyor
- Windows Phone - Desteklenmiyor
- iOS/ıpados-iOS/ıpados 9,3 ve üzeri sürümlerde desteklenir (yalnızca paylaşılan iPad cihazları)
- macOS - Desteklenmiyor
- Android - Desteklenmiyor

## <a name="remove-a-user"></a>Kullanıcıyı kaldırma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihazlar**  >  **tüm cihazlar**' ı seçin.
3. Yönettiğiniz cihazların listesinde bir iOS/ıpados cihazı seçin.
4. Cihazın bölmesinde **Kullanıcılar**'ı seçin.
5. Listede, kaldırmak istediğiniz kullanıcıya sağ tıklayın ve **Kullanıcıyı kaldır**'ı seçin.

## <a name="next-steps"></a>Sonraki adımlar

- **Kullanıcıyı kaldır** eyleminin durumunu görmek için **Cihazlar** > **Cihaz eylemleri**'ni seçin.
