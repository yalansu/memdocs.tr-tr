---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126486"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Configuration Manager yönetilen cihazlar için gereken uç noktalar

Configuration Manager yönetilen cihazlar, Configuration Manager rolündeki bağlayıcı aracılığıyla Intune 'a veri gönderir ve doğrudan Microsoft genel bulutuna erişimine gerek kalmaz.

| Uç Noktası  | İşlev  |
|-----------|-----------|
| `https://graph.windows.net` | Hiyerarşinizi Configuration Manager sunucusu rolünde Endpoint Analytics 'e eklerken otomatik olarak ayarları almak için kullanılır. Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Yalnızca Configuration Manager sunucu rolündeki Endpoint Analytics ile cihaz toplamayı ve cihazları eşitleme için kullanılır. Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="endpoints-required-for-intune-managed-devices"></a>Intune tarafından yönetilen cihazlar için gereken uç noktalar

Cihazları Endpoint Analytics 'e kaydetmek için, gerekli işlevsel verileri Microsoft genel buluta göndermelidir. Endpoint Analytics, Intune tarafından yönetilen cihazlardan verileri toplamak için Windows 10 ve Windows Server bağlı kullanıcı deneyimleri ve telemetri bileşeni (DiagTrack) kullanır. Cihazdaki **bağlı kullanıcı deneyimlerinin ve telemetri** hizmetinin çalıştığından emin olun.

| Uç Noktası  | İşlev  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Intune tarafından yönetilen cihazlar tarafından, [gerekli işlevsel verileri](../../../../../analytics/data-collection.md#bkmk_datacollection) Intune veri toplama uç noktasına göndermek için kullanılır. |
