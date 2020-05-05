---
title: İstemcilerde Aktarım Katmanı Güvenliği (TLS) 1,2 nasıl etkinleştirilir
titleSuffix: Configuration Manager
description: Configuration Manager istemcileri için TLS 1,2 ' i etkinleştirme hakkında bilgiler.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720558"
---
# <a name="how-to-enable-tls-12-on-clients"></a>İstemcilerde TLS 1,2 nasıl etkinleştirilir

*Uygulama hedefi: Configuration Manager (Güncel Dalı)*

Configuration Manager ortamınız için TLS 1,2 ' i etkinleştirirken, istemcilerin TLS 1,2 'ı etkinleştirmeden ve site sunucularındaki ve uzak site sistemlerindeki eski protokolleri devre dışı bırakmadan önce TLS 1,2 ' yi kullanacak şekilde ve doğru şekilde yapılandırıldığından emin olarak başlayın. İstemcilerde TLS 1,2 ' i etkinleştirmek için üç görev vardır:

- Windows ve WinHTTP 'yi güncelleştirme
- TLS 1,2 'nin işletim sistemi düzeyinde SChannel için protokol olarak etkinleştirildiğinden emin olun
- .NET Framework TLS 1,2 ' i destekleyecek şekilde güncelleştirin ve yapılandırın

Belirli Configuration Manager Özellikler ve senaryolar için bağımlılıklar hakkında daha fazla bilgi için bkz. [TLS 1,2 etkinleştirme hakkında](enable-tls-1-2.md).

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a>Windows ve WinHTTP 'yi güncelleştirme

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 ve sonraki Windows sürümleri, WinHTTP üzerinden istemci-sunucu iletişimleri için TLS 1,2 ' i yerel olarak destekler. 

Windows 7 veya Windows Server 2012 gibi önceki Windows sürümleri, WinHTTP kullanarak güvenli iletişimler için varsayılan olarak TLS 1,1 veya TLS 1,2 ' ı etkinleştirmez. Önceki Windows sürümleri için, aşağıdaki kayıt defteri değerini etkinleştirmek üzere [3140245 güncelleştirmesini](https://support.microsoft.com/help/3140245) yükleyerek, WinHTTP için varsayılan güvenli protokoller listesine TLS 1,1 ve TLS 1,2 eklemek üzere ayarlanabilir. Düzeltme Eki yüklüyken aşağıdaki kayıt defteri değerlerini oluşturun:

> [!IMPORTANT]
> TLS 1,2 ' i etkinleştirmeden ve Configuration Manager sunucularındaki eski protokolleri devre dışı bırakmadan *önce* , Windows 'un önceki sürümlerini çalıştıran tüm istemcilerde bu ayarları etkinleştirin. Aksi takdirde, istemeden artık sahipsiz olabilirsiniz.

`DefaultSecureProtocols` Kayıt defteri ayarının değerini doğrulayın, örneğin:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Bu değeri değiştirirseniz, bilgisayarı yeniden başlatın.

Yukarıdaki örnekte, WinHTTP `0xAA0` `DefaultSecureProtocols` ayarının değeri gösterilmektedir. [KB 3140245: Windows 'Ta WinHTTP 'de varsayılan güvenli protokoller IÇIN tls 1,1 ve tls 1,2 ' i etkinleştirmek üzere güncelleştirme](https://support.microsoft.com/help/3140245) , her protokol için onaltılı değeri listeler. Windows 'da varsayılan olarak bu değer `0x0A0` , WINHTTP için SSL 3,0 ve TLS 1,0 ' i etkinleştirmek içindir. Yukarıdaki örnekte bu varsayılanlar tutulur ve ayrıca, WinHTTP için TLS 1,1 ve TLS 1,2 de etkinleştirilir. Bu yapılandırma, değişikliğin hala SSL 3,0 veya TLS 1,0 ' i kullanan başka bir uygulamayı bozmamasını sağlar. Değerini yalnızca TLS 1,1 ve TLS `0xA00` 1,2 ' i etkinleştirmek için kullanabilirsiniz. Configuration Manager, Windows 'un her iki cihaz arasında görüşen güvenli protokolü destekler.

 SSL 3,0 ve TLS 1,0 ' yi tamamen devre dışı bırakmak istiyorsanız, Windows 'daki SChannel devre dışı protokolleri ayarını kullanın. Daha fazla bilgi için bkz. [Schannel. dll ' de belirli şifreleme algoritmalarının ve protokollerin kullanımını kısıtlama](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>TLS 1,2 'nin işletim sistemi düzeyinde SChannel için protokol olarak etkinleştirildiğinden emin olun

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>.NET Framework TLS 1,2 ' i destekleyecek şekilde güncelleştirin ve yapılandırın

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Sonraki adımlar

- [Site sunucularında ve uzak site sistemlerinde TLS 1,2 'yi etkinleştirme](enable-tls-1-2-server.md)
- [TLS 1.2’yi etkinleştirmeye yönelik sık karşılaşılan sorunlar](enable-tls-1-2-troubleshoot.md)

