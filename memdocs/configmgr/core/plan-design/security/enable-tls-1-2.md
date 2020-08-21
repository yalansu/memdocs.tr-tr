---
title: Aktarım katmanı güvenliğini etkinleştir (TLS) 1,2 genel bakış
titleSuffix: Configuration Manager
description: Configuration Manager için TLS 1,2 ' i etkinleştirme konusuna genel bakış.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e1334603bcf60ea3eb8c3d18b73d511570cdc5d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699747"
---
# <a name="how-to-enable-tls-12"></a>TLS 1,2 nasıl etkinleştirilir

*Uygulama hedefi: Configuration Manager (Güncel Dalı)*

Güvenli Yuva Katmanı (SSL) gibi Aktarım Katmanı Güvenliği (TLS), bir ağ üzerinden aktarılırken verilerin güvende tutulması amaçlanan bir şifreleme protokolüdür. Bu makaleler, Configuration Manager güvenli iletişimin TLS 1,2 protokolünü kullandığından emin olmak için gerekli adımları anlatmaktadır. Bu makaleler Ayrıca yaygın olarak kullanılan bileşenlere yönelik güncelleştirme gereksinimlerini ve sık karşılaşılan sorunları gidermeye yöneliktir.

## <a name="enabling-tls-12"></a>TLS 1.2'yi etkinleştirme

Configuration Manager, güvenli iletişim için bir dizi farklı bileşeni kullanır. Belirli bir bağlantı için kullanılan protokol, hem istemci hem de sunucu tarafında ilgili bileşenlerin özelliklerine bağlıdır. Herhangi bir bileşen güncel değilse veya düzgün yapılandırılmamışsa, iletişim daha eski, daha az güvenli bir protokol kullanabilir. Configuration Manager tüm güvenli iletişimler için TLS 1,2 ' i destekleyecek şekilde etkinleştirmek için tüm gerekli bileşenler için TLS 1,2 ' i etkinleştirmeniz gerekir. Gerekli bileşenler ortamınıza ve kullandığınız Configuration Manager özelliklere bağımlıdır.

> [!IMPORTANT]
> Bu işlemi, özellikle Windows 'un önceki sürümleriyle, istemcilerle başlatın. TLS 1,2 ' i etkinleştirmeden ve Configuration Manager sunucularındaki eski protokolleri devre dışı bırakmadan önce tüm istemcilerin TLS 1,2 ' yi desteklemesini sağlayın. Aksi takdirde, istemciler sunucularla iletişim kuramaz ve yalnız bırakılmış olabilir.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Configuration Manager istemcileri, site sunucuları ve uzak site sistemleri için görevler

Configuration Manager, güvenli iletişim için bağlı olan bileşenler için TLS 1,2 ' i etkinleştirmek için hem istemcilerde hem de site sunucularında birden çok görev yapmanız gerekir.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Configuration Manager istemcileri için TLS 1,2 'yi etkinleştirme

- [Windows 8,0, Windows Server 2012 (R2 dışı) ve önceki sürümlerde Windows ve WinHTTP 'yi güncelleştirme](enable-tls-1-2-client.md#bkmk_winhttp)
- [TLS 1,2 'nin işletim sistemi düzeyinde SChannel için protokol olarak etkinleştirildiğinden emin olun](enable-tls-1-2-client.md#bkmk_protocol)
- [.NET Framework TLS 1,2 ' i destekleyecek şekilde güncelleştirin ve yapılandırın](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Configuration Manager site sunucuları ve uzak site sistemleri için TLS 1,2 'yi etkinleştirme

- [TLS 1,2 'nin işletim sistemi düzeyinde SChannel için protokol olarak etkinleştirildiğinden emin olun](enable-tls-1-2-server.md#bkmk_protocol)
- [.NET Framework TLS 1,2 ' i destekleyecek şekilde güncelleştirin ve yapılandırın](enable-tls-1-2-server.md#bkmk_net)
- [Güncelleştirme SQL Server ve SQL Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [Windows Server Update Services 'ı (WSUS) güncelleştirme](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Özellikler ve senaryo bağımlılıkları

Bu bölümde, belirli Configuration Manager özellikleri ve senaryoları için bağımlılıklar açıklanmaktadır. Sonraki adımları belirlemek için ortamınıza uygulanan öğeleri bulun.

|Özellik veya senaryo|Güncelleştirme görevleri|
|--- |--- |
|Site sunucuları (Merkezi, birincil veya ikincil)| - [Güncelleştirme .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> -Güçlü şifreleme ayarlarını doğrulama|
|Site veritabanı sunucusu|[SQL Server ve istemci bileşenlerini Güncelleştir](enable-tls-1-2-server.md#bkmk_sql)|
|İkincil site sunucuları|[SQL Server ve istemci BILEŞENLERINI](enable-tls-1-2-server.md#bkmk_sql) SQL Express 'in uyumlu bir sürümüne güncelleştirme|
|Site sistemi rolleri| - [.NET Framework güncelleştirme](enable-tls-1-2-server.md#bkmk_net) ve güçlü şifreleme ayarlarını doğrulama <br/> - [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client) de dahil olmak üzere [SQL Server ve onun istemci bileşenlerini güncelleştirme](enable-tls-1-2-server.md#bkmk_sql)|
|Raporlama hizmetleri noktası|- Site sunucusunda, SQL Raporlama Hizmetleri sunucularında ve konsolu olan herhangi bir bilgisayarda [.NET Framework güncelleştirme](enable-tls-1-2-server.md#bkmk_net)<br/> -SMS_Executive hizmetini gerektiği şekilde yeniden başlatın|
|Yazılım güncelleştirme noktası|[WSUS güncelleştirme](enable-tls-1-2-server.md#bkmk_wsus)|
|Bulut yönetimi ağ geçidi|[TLS 1.2’yi zorlama](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Configuration Manager konsolu| - [Güncelleştirme .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> -Güçlü şifreleme ayarlarını doğrulama|
|HTTPS site sistem rolleriyle Configuration Manager istemci|[Windows Update, WinHTTP kullanarak istemci-sunucu iletişimleri için TLS 1,2 desteği](enable-tls-1-2-client.md#bkmk_winhttp)|
|Yazılım Merkezi| - [Güncelleştirme .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> -Güçlü şifreleme ayarlarını doğrulama|
|Windows 7 istemcileri| Herhangi bir sunucu bileşeni üzerinde TLS 1,2 ' i etkinleştirmeden *önce* , Windows 'U, [WinHTTP kullanarak istemci-sunucu iletişimleri için TLS 1,2 desteği olacak şekilde güncelleştirin](enable-tls-1-2-client.md#bkmk_winhttp). Önce sunucu bileşenlerinde TLS 1,2 ' i etkinleştirirseniz, daha eski istemcilerin sürümlerini kullanabilirsiniz.|

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

### <a name="why-use-tls-12-with-configuration-manager"></a>Configuration Manager TLS 1,2 neden kullanılmalıdır?

TLS 1,2, SSL 2,0, SSL 3,0, TLS 1,0 ve TLS 1,1 gibi önceki şifreleme protokollerinden daha güvenlidir. Esas olarak, TLS 1,2 ağ üzerinden aktarılan verileri daha güvenli tutar.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Configuration Manager TLS 1,2 gibi şifreleme protokollerini kullanır?

Configuration Manager TLS 1,2 gibi şifreleme protokollerini kullanan temel beş alan vardır:

- Rol HTTPS kullanacak şekilde yapılandırıldığında IIS tabanlı site sunucu rollerine istemci iletişimleri. Bu rollere örnek olarak dağıtım noktaları, yazılım güncelleştirme noktaları ve yönetim noktaları dahildir.
- Yönetim noktası, SMS Executive ve SMS sağlayıcısı iletişimleri SQL ile. Configuration Manager her zaman SQL iletişimlerini şifreler.
- WSUS HTTPS kullanacak şekilde yapılandırıldıysa, site sunucusundan WSUS iletişimine iletişim.
- SSRS, HTTPS kullanacak şekilde yapılandırıldıysa, SQL Raporlama Hizmetleri 'ne (SSRS) Configuration Manager konsolu.
- İnternet tabanlı hizmetlere yönelik bağlantılar. Bulut yönetimi ağ geçidini (CMG), hizmet bağlantı noktası eşitlemesini ve Microsoft Update güncelleştirme meta verilerinin eşitlenmesini örnekler de vardır.

### <a name="what-determines-which-encryption-protocol-is-used"></a>Hangi şifreleme protokolünün kullanıldığını belirler?

HTTPS, hem istemci hem de sunucu tarafından şifrelenmiş bir konuşmada desteklenen en yüksek protokol sürümüne her zaman anlaşacaktır. Bir bağlantı kurulurken, istemci sunucuya en yüksek protokolü ile bir ileti gönderir. Sunucu aynı sürümü destekliyorsa, bu sürümü kullanarak bir ileti gönderir. Bu anlaşmalı sürüm, bağlantı için kullanılan bir sürümdür. Sunucu, istemci tarafından sunulan sürümü desteklemiyorsa, sunucu iletisi kullanabileceği en yüksek sürümü belirler. TLS El Sıkışma Protokolü hakkında daha fazla bilgi için bkz. [TLS kullanarak güvenli bir oturum oluşturma](/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>İstemci ve sunucunun hangi protokol sürümünü kullanabileceğinizi belirler?

Genellikle, aşağıdaki öğeler hangi protokol sürümünün kullanıldığını tespit edebilir:

- Uygulama, hangi belirli protokol sürümlerinin anlaşacak şekilde dikte edebilir.
  - En iyi yöntem, belirli protokol sürümlerini uygulama düzeyinde sabit kodlamaya ve bileşen ve işletim sistemi protokol düzeyinde tanımlanan yapılandırmayı izlemeye engel olarak belirler.
  - Configuration Manager Bu en iyi yöntemi izler.
- .NET Framework kullanılarak yazılan uygulamalar için varsayılan protokol sürümleri, üzerine derlendikleri Framework sürümüne bağlıdır.  
  - 4.6.3 öncesi .NET sürümleri, varsayılan olarak, anlaşma için protokoller listesine TLS 1,1 ve 1,2 içermemelidir.
- Configuration Manager istemcisi gibi HTTPS iletişimleri için WinHTTP kullanan uygulamalar, işletim sistemi sürümüne, düzeltme eki düzeyine ve protokol sürümü desteği yapılandırmasına bağlıdır.


## <a name="additional-resources"></a>Ek kaynaklar

- [Şifreleme denetimleri teknik başvurusu](cryptographic-controls-technical-reference.md)
- [.NET Framework ile Aktarım Katmanı Güvenliği (TLS) en iyi uygulamaları](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: Microsoft SQL Server için TLS 1,2 desteği](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>Sonraki adımlar

- [TLS 1.2’yi istemcilerde etkinleştirme](enable-tls-1-2-client.md)
- [Site sunucularında TLS 1,2 'yi etkinleştirme](enable-tls-1-2-server.md)