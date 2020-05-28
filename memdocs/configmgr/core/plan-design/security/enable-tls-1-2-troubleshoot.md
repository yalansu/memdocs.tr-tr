---
title: Aktarım Katmanı Güvenliği etkinleştirilirken yaygın sorunlar (TLS) 1,2
titleSuffix: Configuration Manager
description: Aktarım Katmanı Güvenliği (TLS 1,2) etkinleştirilirken yaygın sorunları açıklar.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720530"
---
# <a name="common-issues-when-enabling-tls-12"></a>TLS 1.2’yi etkinleştirmeye yönelik sık karşılaşılan sorunlar

Bu makalede, Configuration Manager 'de TLS 1,2 desteğini etkinleştirdiğinizde gerçekleşen yaygın sorunlara yönelik öneriler sunulmaktadır.

## <a name="unsupported-platforms"></a>Desteklenmeyen platformlar

Aşağıdaki istemci platformları Configuration Manager tarafından desteklenir ancak TLS 1,2 ortamında desteklenmez:

- Windows CE
- Apple OS X
- Şirket içi MDM ile yönetilen Windows 10 cihazları

## <a name="reports-dont-show-in-the-console"></a>Raporlar konsolda gösterilmez

Raporlar Configuration Manager konsolunda gösterilmezseniz, konsolunu çalıştırdığınız bilgisayarı güncelleştirdiğinizden emin olun. [.NET Framework güncelleştirin](enable-tls-1-2-client.md#bkmk_net)ve güçlü şifrelemeyi etkinleştirin.

## <a name="fips-security-policy-enabled"></a>FIPS güvenlik ilkesi etkin

İstemci veya sunucu için FIPS güvenlik ilkesi ayarını etkinleştirirseniz, güvenli kanal (Schannel) anlaşması, TLS 1,0 kullanmasına neden olabilir. Bu davranış, kayıt defterindeki protokolü devre dışı bıraksanız bile gerçekleşir.

Araştırmak için güvenli kanal olay günlüğünü etkinleştirin ve Sistem günlüğündeki Schannel olaylarını gözden geçirin. Daha fazla bilgi için bkz. [Schannel. dll ' de belirli şifreleme algoritmalarının ve protokollerin kullanımını kısıtlama](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="sql-server-communication-failure"></a>SQL Server iletişim hatası

SQL Server iletişim başarısız olursa ve bir **Sslsecurityerror** hatası döndürürse, aşağıdaki ayarları doğrulayın:

- [.NET Framework güncelleştirin](enable-tls-1-2-server.md#bkmk_net)ve her makinede güçlü şifrelemeyi etkinleştirin
- Konak sunucusundaki [SQL Server güncelleştirme](enable-tls-1-2-server.md#bkmk_sql)
- SQL [istemci BILEŞENLERINI](enable-tls-1-2-server.md#bkmk_sql-client) SQL ile iletişim kuran tüm sistemlerde güncelleştirin. Örneğin, site sunucuları, SMS sağlayıcısı ve site rolü sunucuları.

## <a name="configuration-manager-client-communication-failures"></a>İstemci iletişim başarısızlıklarını Configuration Manager

Configuration Manager istemcisi site rolleriyle iletişim kurmazsa, Windows 'u WinHTTP kullanarak istemci-sunucu iletişimi için TLS 1,2 ' i destekleyecek şekilde [güncelleştirdiğinizi](enable-tls-1-2-client.md#bkmk_winhttp) doğrulayın. Ortak site rolleri dağıtım noktaları, yönetim noktaları ve durum geçiş noktaları içerir.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Raporlama Hizmetleri noktası başarısız olur ve beklenen bir hata döndürür

Raporlama Hizmetleri noktası raporları yapılandırmazsa, aşağıdaki hata girişi için **Srsrp. log dosyasına** bakın:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Bu sorunu çözmek için şu adımları izleyin:

1. [.NET Framework güncelleştirin](enable-tls-1-2-client.md#bkmk_net)ve ilgili tüm bilgisayarlarda güçlü şifrelemeyi etkinleştirin.

1. Herhangi bir güncelleştirme yükledikten sonra SMS_Executive hizmetini yeniden başlatın.

## <a name="application-catalog-doesnt-initialize"></a>Uygulama Kataloğu başlatılamadı

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Uygulama Kataloğu başlamazsa, aşağıdaki hata girişi için **Serviceportalwebsite. svcgünlük** dosyasını denetleyin:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Bu sorunu çözmek için şu adımları izleyin:

1. [.NET Framework güncelleştirin](enable-tls-1-2-client.md#bkmk_net)ve ilgili tüm bilgisayarlarda güçlü şifrelemeyi etkinleştirin.

1. `%WinDir%\System32\InetSrv`Uygulama Kataloğu sunucusunun klasöründe aşağıdaki içeriğe sahip bir **W2SP. exe. config** dosyası oluşturun:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Bu dosya, uygulamanın .NET Framework 4.6.3 kullanılarak oluşturulması durumunda oluşturulan varsayılan dosyadır.

1. Uygulama Kataloğu rolleri için HTTPS aktarım güvenliği kullanın.

    > [!Important]
    > Uygulama Kataloğu rolleri için HTTP ileti güvenliği kullandığınızda, WCF yalnızca SSL 3,0 ve TLS 1,0 kullanmak üzere sabit olarak kodlanmıştır. Bu, TLS 1,2 kullanımını engeller.

1. Herhangi bir değişiklik yaptıysanız bilgisayarı yeniden başlatın.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Yazılım Merkezi veya tarayıcı uygulama kataloğu ile iletişim kurmıyor

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Bir TLS 1,2 özellikli sitede Kullanıcı tarafından kullanılabilir uygulamalar için yazılım merkezi 'nin birlikte çalışması için en iyi yöntem, uygulama kataloğu rolünü kaldırın. Ardından, yazılım merkezi 'nin doğrudan bir yönetim noktasıyla iletişim kurmasına izin verin. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).

Uygulama Kataloğu ve yazılım merkezi arasındaki iletişim başarısızlıklarını çözmeniz gerekiyorsa, aşağıdaki koşulları doğrulayın:

- [.NET Framework güncelleştirin](enable-tls-1-2-client.md#bkmk_net)ve her bilgisayarda güçlü şifrelemeyi etkinleştirin.

- Değişiklikleri yaptıktan sonra, etkilenen tüm bilgisayarları yeniden başlatın.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Hizmet bağlantı noktası karşıya yükleme sorunları

Hizmet bağlantı noktası, SCCMConnectedService 'e veri yüklememezse, [.NET Framework güncelleştirin](enable-tls-1-2-server.md#bkmk_net)ve her bilgisayarda güçlü şifrelemeyi etkinleştirin. Değişiklikleri yaptıktan sonra bilgisayarları yeniden başlatmayı unutmayın.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager konsolu Intune ekleme iletişim kutusunu görüntüler

Konsol Intune portalına bağlanmayı denediğinde Intune ekleme iletişim kutusu görüntülenirse, [.NET Framework güncelleştirin](enable-tls-1-2-client.md#bkmk_net)ve her bilgisayarda güçlü şifrelemeyi etkinleştirin. Değişiklikleri yaptıktan sonra bilgisayarları yeniden başlatmayı unutmayın.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Configuration Manager konsolu Azure 'da oturum açma hatası görüntülüyor

Azure Active Directory (Azure AD) içinde uygulamalar oluşturmaya çalıştığınızda, **oturum aç**' ı seçtikten sonra Azure hizmetleri ekleme iletişim kutusu hemen başarısız olursa, [.NET Framework güncelleştirin](enable-tls-1-2-server.md#bkmk_net)ve güçlü şifrelemeyi etkinleştirin. Değişiklikleri yaptıktan sonra bilgisayarları yeniden başlatmayı unutmayın.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager Cloud Services ve TLS 1,2

Bulut yönetimi ağ geçidi ve bulut dağıtım noktaları tarafından kullanılan Azure sanal makineleri TLS 1,2 ' i destekler. Desteklenen istemci sürümleri otomatik olarak TLS 1,2 kullanır.

**Smsadminuı. log** , aşağıdaki örneğe benzer bir hata içerebilir:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

Sistem olay günlüğüne aşağıdaki açıklamayla SChannel EventID 36874 kaydedilebilir:`An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Ek kaynaklar

- [.NET Framework ile Aktarım Katmanı Güvenliği (TLS) en iyi uygulamaları](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: Microsoft SQL Server için TLS 1,2 desteği](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Şifreleme denetimleri teknik başvurusu](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Sonraki adımlar

- [TLS 1.2’yi istemcilerde etkinleştirme](enable-tls-1-2-client.md)
- [Site sunucularında ve uzak site sistemlerinde TLS 1,2 'yi etkinleştirme](enable-tls-1-2-server.md)

