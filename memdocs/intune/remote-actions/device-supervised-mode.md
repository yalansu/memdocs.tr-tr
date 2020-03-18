---
title: İOS/ıpados denetimli modu Microsoft Intune açın
titleSuffix: ''
description: Intune ile iOS/ıpados denetimli modu açma hakkında bilgi edinin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/15/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8190814-07f0-42d8-9b3a-87c67dd2b7ed
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d9b147a9a2c201cde798abcee30a212176cf268
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325006"
---
# <a name="turn-on-iosipados-supervised-mode"></a>iOS/iPadOS denetimli modunu açma


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Apple iOS/ıpados Denetimli mod yöneticilere Apple cihazlarını yönetirken daha fazla seçenek sunar ve bu sayede, ölçekli olarak dağıtılan şirkete ait cihazlar için yararlıdır. Örneğin AirDrop’u kısıtlayabilir veya kullanıcıların cihaz adını değiştirmesini önleyebilirsiniz. Denetimli mod gerektiren ayarlar listesi için bkz. [Intune’da iOS cihaz kısıtlama ayarları](../configuration/device-restrictions-ios.md).

Intune, [Apple Aygıt Kayıt Programı](../enrollment/device-enrollment-program-enroll-ios.md)’nın (DEP) bir parçası olarak denetimli modu destekler.

Denetim gerektiren Apple denetimleri listesi için Apple’ın [Yük ayarları başvurusuna](http://help.apple.com/configurator/mac/2.4/#/cad5370d089) bakın.

## <a name="turn-on-supervised-mode-during-enrollment"></a>Denetimli modu kayıt sırasında açma

[Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'NDE, [DEP 'de bir Apple kayıt profili oluştururken](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile)cihazlar için denetimli modu açabilirsiniz. **Cihaz Yönetim Ayarları** altında **Denetimli** kutusunu işaretleyin.

## <a name="turn-on-supervised-mode-after-enrollment"></a>Denetimli modu kayıt sonrasında açma

Kayıt sonrasında denetimli modu açmak için tek yol, bir iOS/ıpados cihazını Mac 'e bağlamak ve [Apple Configurator](../enrollment/apple-configurator-enroll-ios.md) 'ı (cihazı sıfırlayacaktır) kullanmaktır. Kayıttan sonra bir cihazı Intune’da Denetimli mod için yapılandıramazsınız.

## <a name="identify-a-supervised-device"></a>Denetimli bir cihazı tanımlama

Bir cihazın denetimli olup olmadığına karar vermek için kilit ekranına veya **Hakkında** sayfasına bakın:
- Cihazın kilit ekranında **Bu iPhone “Şirket Adı” tarafından yönetilmektedir** yazar.
- Cihazın **hakkında** sayfasında **Bu iPhone 'un denetimli olduğunu söylecektir. Şirket adı, Internet trafiğinizi izleyebilir ve bu cihazı bulabilir.**

## <a name="next-steps"></a>Sonraki adımlar

Diğer cihaz yönetim seçenekleri için bkz. [Microsoft Intune cihaz yönetimi nedir?](device-management.md)
