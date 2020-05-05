---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720537"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1,2 varsayılan olarak etkindir. Bu nedenle, etkinleştirmek için bu tuşlara hiçbir değişiklik yapılması gerekmez. Bu makalelerdeki yönergelerin geri `Protocols` kalanını uyguladıktan sonra ve yalnızca TLS 1,2 etkinleştirildiğinde ortamın çalışıp çalışmadığını DOĞRULADıKTAN sonra TLS 1,0 ve TLS 1,1 ' yi devre dışı bırakmak için altında değişiklikler yapabilirsiniz.

`\SecurityProviders\SCHANNEL\Protocols` [.NET Framework ile birlikte aktarım KATMANı güvenliği (TLS) en iyi uygulamalarında](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)gösterildiği gibi kayıt defteri alt anahtarı ayarını doğrulayın.

