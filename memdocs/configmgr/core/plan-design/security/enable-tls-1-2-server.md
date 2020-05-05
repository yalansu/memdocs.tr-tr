---
title: Site sunucularında ve uzak site sistemlerinde Aktarım Katmanı Güvenliği (TLS) 1,2 ' i etkinleştir
titleSuffix: Configuration Manager
description: Configuration Manager site sunucuları için TLS 1,2 ' i etkinleştirme hakkında bilgiler.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720551"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>Site sunucularında ve uzak site sistemlerinde TLS 1,2 'yi etkinleştirme

*Uygulama hedefi: Configuration Manager (Güncel Dalı)*

Configuration Manager ortamınız için TLS 1,2 ' i etkinleştirirken önce [istemciler IÇIN tls 1,2](enable-tls-1-2-client.md) ' yi etkinleştirmeye başlayın. Daha sonra, site sunucularında ve uzak site sistemlerinde TLS 1,2 'yi etkinleştirin. Son olarak, sunucu tarafında daha eski protokolleri devre dışı bırakamadan önce istemcisini site sistem iletişimlerinde test edin. Site sunucularında ve uzak site sistemlerinde TLS 1,2 ' i etkinleştirmek için aşağıdaki görevler gereklidir:

- TLS 1,2 'nin işletim sistemi düzeyinde SChannel için protokol olarak etkinleştirildiğinden emin olun
- .NET Framework TLS 1,2 ' i destekleyecek şekilde güncelleştirin ve yapılandırın
- SQL Server ve istemci bileşenlerini güncelleştirme
- Windows Server Update Services 'ı (WSUS) güncelleştirme

Belirli Configuration Manager Özellikler ve senaryolar için bağımlılıklar hakkında daha fazla bilgi için bkz. [TLS 1,2 etkinleştirme hakkında](enable-tls-1-2.md). 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>TLS 1,2 'nin işletim sistemi düzeyinde SChannel için protokol olarak etkinleştirildiğinden emin olun

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>.NET Framework TLS 1,2 ' i destekleyecek şekilde güncelleştirin ve yapılandırın

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a>SQL Server ve istemci bileşenlerini güncelleştirme

Microsoft SQL Server 2016 ve üzeri TLS 1,1 ve TLS 1,2. Önceki sürümler ve bağımlı kitaplıklar güncelleştirme gerektirebilir. Daha fazla bilgi için bkz. [KB 3135244: TLS 1,2 Microsoft SQL Server için destek](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

İkincil site sunucularının en az SQL Server 2016 Express Service Pack 2 ' ye (13.2.50.26) veya sonraki bir sürüme kullanması gerekir.

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a>SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) Ayrıca SQL Server istemci bileşenleri için gereksinimleri açıklar.

SQL Server Native Client en az sürüm SQL 2012 SP4 (11. *. 7001.0) sürümüne de güncelleştirdiğinizden emin olun. Sürüm 1810 ' den başlayarak, bu gereksinim bir [Önkoşul denetimi (uyarı)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Configuration Manager aşağıdaki site sistem rollerinde SQL Server Native Client kullanır:

- Site veritabanı sunucusu
- Site sunucusu: merkezi yönetim sitesi, birincil site veya ikincil site
- Yönetim noktası
- Cihaz yönetim noktası
- Durum Geçiş noktası
- site veritabanı
- Yazılım güncelleştirme noktası
- Çok noktaya yayını destekleyen dağıtım noktası
- Varlık Yönetim Bilgileri güncelleştirme hizmet noktası
- Raporlama hizmetleri noktası
- Uygulama Kataloğu Web hizmeti
- Kayıt noktası
- Uç Nokta Koruma noktası
- Hizmet bağlantı noktası
- Sertifika kayıt noktası
- Veri ambarı hizmet noktası


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a>Windows Server Update Services 'ı (WSUS) güncelleştirme

WSUS 'un önceki sürümlerinde TLS 1,2 ' i desteklemek için aşağıdaki güncelleştirmeyi WSUS sunucusuna yüklersiniz:

- Windows Server 2012 çalıştıran WSUS sunucusu için [güncelleştirme 4022721](https://support.microsoft.com/help/4022721) veya sonraki bir toplu güncelleştirmeyi yükler.
- Windows Server 2012 R2 çalıştıran WSUS sunucusu için [güncelleştirme 4022720](https://support.microsoft.com/help/4022720) veya sonraki bir toplu güncelleştirmeyi yükler.

Windows Server 2016 ' den başlayarak, WSUS için varsayılan olarak TLS 1,2 desteklenir.  TLS 1,2 güncelleştirmeleri yalnızca Windows Server 2012 ve Windows Server 2012 R2 WSUS sunucularında gereklidir.

## <a name="next-steps"></a>Sonraki adımlar

- [TLS 1.2’yi etkinleştirmeye yönelik sık karşılaşılan sorunlar](enable-tls-1-2-troubleshoot.md)
