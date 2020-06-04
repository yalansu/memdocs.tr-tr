---
title: include dosyası
description: include dosyası
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347279"
---
## <a name="apple-device-network-information"></a>Apple cihaz ağ bilgileri

|**Kullanıldığı yerler**|**Ana bilgisayar adı (IP adresi/alt ağ)**|**Protokol**|**Bağ**|
|------------|-----------|------------|-----------|
|Apple sunucularından içerik alma ve görüntüleme|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|APNS sunucularıyla iletişim|#-courier.push.apple.com<br>"#", 0 ile 50 arasında rastgele bir sayıdır.|TCP|5223 ve 443|
|Internet, iTunes Mağazası, macOS App Store, iCloud, mesajlaşma vb. gibi çeşitli işlevler|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 veya 443|

Daha fazla bilgi için bkz.

- [Apple yazılım ürünleri tarafından kullanılan TCP ve UDP bağlantı noktaları](https://support.apple.com/HT202944)
- [MacOS, iOS/ıpados ve iTunes Server ana bilgisayar bağlantıları ve iTunes arka plan işlemi hakkında](https://support.apple.com/HT201999)
- [MacOS ve iOS/ıpados istemcileriniz Apple anında iletme bildirimleri almıyorsanız](https://support.apple.com/HT203609)