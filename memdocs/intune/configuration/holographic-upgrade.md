---
title: Microsoft Intune-Azure 'da Windows holographic for Business 'a yükseltme | Microsoft Docs
description: Microsoft Intune bir cihaz yapılandırma profili kullanarak Windows 10 holographic for Business 'a yükseltin.
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65a45b13a91671c1de9bcf04f23156d75313285f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907778"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Windows Holographic çalıştıran cihazları Windows Holographic for Business’a yükseltme

Microsoft Intune cihazlarınızı yönetmenize ve korumanıza yardımcı olacak birçok ayar içerir. Bu makalede Windows holographic cihazlarını Windows holographic for Business 'a yükseltme ayarlarını listeler ve açıklanmaktadır.

Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, Windows holographic cihazlarınızı yükseltmek için bu ayarları kullanın. Microsoft HoloLens için, yükseltme için gerekli lisansı almak üzere ticari paketi satın alabilirsiniz. Daha fazla bilgi için bkz. [Windows Holographic for Business özelliklerini etkinleştirme](/hololens/hololens1-upgrade-enterprise).

Bir Intune Yöneticisi olarak bu ayarları oluşturabilir ve cihazlarınıza atayabilirsiniz.

Bu özellik hakkında daha fazla bilgi için bkz. [Windows 10 sürümlerini yükseltme veya S modunu etkinleştirme](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Başlamadan önce

[Bir Windows 10 sürüm yükseltme ve mod anahtar cihazı yapılandırma profili oluşturun](edition-upgrade-configure-windows-10.md#create-the-profile).

Bir Windows 10 sürüm yükseltme ve mod anahtar cihazı yapılandırma profili oluşturduğunuzda, bu makalede listelenenden daha fazla ayar bulunur. Bu makaledeki ayarlar Windows holographic for Business cihazlarında desteklenir.

## <a name="edition-upgrade"></a>Sürüm yükseltme

- **Yükseltilecek sürüm**: **iş Için Windows 10 holographic**' u seçin.
- **Lisans dosyası**: sıze sunulan XML Lisans dosyasına gidin ve seçin.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="Intune 'da, Holographic for Business lisans bilgilerini içeren XML dosyası adını girin.":::

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

Ayrıca, [Windows 10 ve üzeri](edition-upgrade-windows-settings.md) cihazlar için sürüm yükseltme profilleri de oluşturabilirsiniz.