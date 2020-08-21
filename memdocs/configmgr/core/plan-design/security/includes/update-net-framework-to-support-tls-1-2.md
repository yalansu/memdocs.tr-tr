---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 0f91860ad591e20c6f199e098a8c957f50294386
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703295"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>.NET sürümünü belirleme

İlk olarak, yüklü .NET sürümlerini saptayın. Daha fazla bilgi için, [Microsoft .NET çerçevesinin hangi sürümlerinin ve hizmet paketi düzeylerinin yüklendiğini belirleme](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso)konusuna bakın.

### <a name="install-net-updates"></a>.NET güncelleştirmelerini yükler

Güçlü şifrelemeyi etkinleştirmek için .NET güncelleştirmelerini yükleyebilirsiniz. Bazı .NET Framework sürümleri, güçlü şifrelemeyi etkinleştirmek için güncelleştirmeler gerektirebilir. Bu yönergeleri kullanın:

- NET Framework 4.6.2 ve üzeri TLS 1,1 ve TLS 1,2 ' i destekler. Kayıt defteri ayarlarını onaylayın, ancak başka bir değişiklik yapmanız gerekmez.

- TLS 1,1 ve TLS 1,2 desteğini desteklemek için NET Framework 4,6 ve önceki sürümlerini güncelleştirin. Daha fazla bilgi için bkz. [.NET Framework sürümler ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies).

- Windows 8.1 veya Windows Server 2012 üzerinde .NET Framework 4.5.1 veya 4.5.2 kullanıyorsanız, ilgili güncelleştirmeler ve Ayrıntılar [Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=42883)'nden de kullanılabilir.


### <a name="configure-for-strong-cryptography"></a>Güçlü şifreleme için yapılandırma

Güçlü şifrelemeyi desteklemek için .NET Framework yapılandırın. `SchUseStrongCrypto`Kayıt defteri ayarını olarak ayarlayın `DWORD:00000001` . Bu değer, RC4 akış şifresi devre dışı bırakır ve yeniden başlatma gerektirir. Bu ayar hakkında daha fazla bilgi için bkz. [Microsoft Güvenlik Danışmanlığı 296038](/security-updates/SecurityAdvisories/2015/2960358).

Ağ üzerinden iletişim kuran herhangi bir bilgisayarda TLS 1,2 özellikli bir sistemle aşağıdaki kayıt defteri anahtarlarını ayarladığınızdan emin olun. Örneğin, Configuration Manager istemcileri, uzak site sistem rolleri site sunucusunda ve site sunucusunun kendisi için yüklü değildir.

32 bit OSs üzerinde çalışan 32 bitlik uygulamalar ve 64 bit OSs üzerinde çalışan 64 bit uygulamalar için aşağıdaki alt anahtar değerlerini güncelleştirin:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

64 bit OSs üzerinde çalışan 32 bitlik uygulamalar için aşağıdaki alt anahtar değerlerini güncelleştirin:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> `SchUseStrongCrypto`Ayar, .net 'ın tls 1,1 ve tls 1,2 kullanmasına izin verir. `SystemDefaultTlsVersions`Ayar .net 'in işletim sistemi yapılandırmasını kullanmasına izin verir. Daha fazla bilgi için, [.NET Framework En Iyi TLS uygulamaları](/dotnet/framework/network-programming/tls)bölümüne bakın.