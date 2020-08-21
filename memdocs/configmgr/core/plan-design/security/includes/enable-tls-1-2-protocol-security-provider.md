---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: f14713431c71c1f3625d13ea4be1d919b072e273
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703322"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1,2 varsayılan olarak etkindir. Bu nedenle, etkinleştirmek için bu tuşlara hiçbir değişiklik yapılması gerekmez. `Protocols`Bu makalelerdeki yönergelerin geri kalanını uyguladıktan sonra ve yalnızca TLS 1,2 etkinleştirildiğinde ortamın çalışıp çalışmadığını doğruladıktan sonra tls 1,0 ve tls 1,1 ' yi devre dışı bırakmak için altında değişiklikler yapabilirsiniz.

`\SecurityProviders\SCHANNEL\Protocols` [.NET Framework Ile birlikte aktarım katmanı GÜVENLIĞI (TLS) en iyi uygulamalarında](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)gösterildiği gibi kayıt defteri alt anahtarı ayarını doğrulayın.