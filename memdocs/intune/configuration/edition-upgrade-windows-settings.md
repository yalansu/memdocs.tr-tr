---
title: Microsoft Intune-Azure 'da Windows 10 yükseltme ve S modu ayarları | Microsoft Docs
description: Tüm ayarların bir listesini ve bir cihazda Windows 10 sürümünü yükseltirken ne yaptığını ve Microsoft Intune bir cihaz yapılandırma profili kullanan bir cihazda S modunu etkinleştir ' i inceleyin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a91a84ece833bf893395e494a0e99fa675f14c2a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429651"
---
# <a name="windows-10-and-newer-device-settings-to-upgrade-editions-or-enable-s-mode-in-intune"></a>Windows 10 (ve daha yeni) cihazları yükseltmek veya Intune 'da S modunu etkinleştirmek için cihaz ayarları

Microsoft Intune cihazlarınızı yönetmenize ve korumanıza yardımcı olacak birçok ayar içerir. Bu makalede, Windows 10 cihazlarında sürümlerini yükseltmek veya S modunu etkinleştirmek için ayarların listesi ve açıklanmaktadır. Bu ayarlar, Intune 'da gönderilen veya cihazlara dağıtılan bir yükseltme yapılandırma profilinde oluşturulur.

Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu ayarları, Windows 10 cihazlarınızın sürümü ve S mod seçeneklerini denetlemek için kullanın.

Bu özellik hakkında daha fazla bilgi için bkz. [Windows 10 sürümlerini yükseltme veya S modunu etkinleştirme](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Başlamadan önce

[Profili oluşturun](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Sürüm yükseltme

- **Yükseltilecek sürüm**: Yükseltme yaptığınız Windows 10 sürümünü seçin. Bu ilke tarafından hedeflenen cihazlar seçtiğiniz sürüme yükseltilir.
- **Ürün Anahtarı**: Microsoft'tan aldığınız ürün anahtarını girin. Ürün anahtarıyla bir ilke oluşturulduktan sonra anahtar güncelleştirilemez ve güvenlik nedeniyle gizlenir. Ürün anahtarını değiştirmek için tüm anahtarı yeniden girin.
- **Lisans Dosyası**: **İş için Windows 10 Holographic** veya **Windows 10 Mobile sürümü**'nde, seçmek üzere **Gözat** ile Microsoft'tan aldığınız dosyaya gidin. Bu lisans dosyası, cihazları yükselttiğiniz sürümlerin lisans bilgilerini içerir.

## <a name="mode-switch"></a>Mod anahtarı

- **S modundan geçiş**: aygıtı s modundan geçirir. Seçenekleriniz şunlardır:

  - **Yapılandırma yok**: Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, S modu cihaz modunda kalabilir. Kullanıcı, cihazı S modundan dışarı değiştirebilir.
  - **S modunda tut**: kullanıcıların cihazı s modundan çıkmadan değiştirmesini engeller.
  - **Anahtar**: kullanıcıların cihazı S modundan dışarı değiştirmesine izin verir.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

Ayrıca, [Windows holographic for Business](holographic-upgrade.md) cihazları için sürüm yükseltme profilleri oluşturabilirsiniz.
