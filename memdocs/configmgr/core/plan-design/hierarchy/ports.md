---
title: Bağlantılar için kullanılan bağlantı noktaları
titleSuffix: Configuration Manager
description: Configuration Manager bağlantılar için kullandığı gerekli ve özelleştirilebilir ağ bağlantı noktaları hakkında bilgi edinin.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2495c0d7b5b19b5d6f7741d3b28b6a9a0e213fc3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700155"
---
# <a name="ports-used-in-configuration-manager"></a>Configuration Manager kullanılan bağlantı noktaları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede Configuration Manager kullandığı ağ bağlantı noktaları listelenir. Bazı bağlantılar, yapılandırılabilir olmayan bağlantı noktaları kullanır ve bazıları sizin belirttiğiniz özel bağlantı noktalarını destekler. Herhangi bir bağlantı noktası filtreleme teknolojisi kullanırsanız, gerekli bağlantı noktalarının kullanılabilir olduğunu doğrulayın. Bu bağlantı noktası filtreleme teknolojileriyle güvenlik duvarları, yönlendiriciler, proxy sunucuları veya IPSec bulunur.

> [!NOTE]  
> Internet tabanlı istemcileri SSL köprülemesi kullanarak desteklemeniz, bağlantı noktası gereksinimlerine ek olarak, bazı HTTP fiillerine ve üstbilgilere güvenlik duvarınızdan geçiş yapmasına izin vermeniz de gerekebilir.

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Yapılandırabileceğiniz bağlantı noktaları

Configuration Manager, aşağıdaki iletişim türleri için bağlantı noktalarını yapılandırmanızı sağlar:  

- Uygulama Kataloğu web sitesi noktası Uygulama Kataloğu Web hizmeti noktasına  

- Kayıt proxy noktasından kayıt noktasına  

- IIS çalıştıran istemci-site sistemleri  

- İstemciden internete (proxy sunucusu ayarları olarak)  

- Internet 'e yazılım güncelleştirme noktası (proxy sunucusu ayarları olarak)  

- Yazılım güncelleştirme noktasından WSUS sunucusuna  

- Site sunucusundan site veritabanı sunucusuna  

- Site sunucusundan WSUS veritabanı sunucusuna

- Raporlama hizmetleri noktaları  

  > [!NOTE]  
  > Raporlama Hizmetleri noktası site sistemi rolü için kullanılmakta olan bağlantı noktaları SQL Server Reporting Services ' de yapılandırılır. Bu bağlantı noktaları daha sonra Raporlama Hizmetleri noktası iletişimleri sırasında Configuration Manager tarafından kullanılır. IPSec ilkeleri veya güvenlik duvarlarını yapılandırmak için IP filtresi bilgilerini tanımlayan bu bağlantı noktalarını gözden geçirdiğinizden emin olun.  

Varsayılan olarak, istemciden siteye sistem iletişimi için kullanılan HTTP bağlantı noktası 80 bağlantı noktasıdır ve varsayılan HTTPS bağlantı noktası 443 ' dir. HTTP veya HTTPS üzerinden istemciden siteye sistem iletişimine yönelik bağlantı noktaları, kurulum sırasında veya Configuration Manager sitenizin site özelliklerinde değiştirilebilir.  

Raporlama Hizmetleri noktası site sistemi rolü için kullanılmakta olan bağlantı noktaları SQL Server Reporting Services ' de yapılandırılır. Bu bağlantı noktaları daha sonra Raporlama Hizmetleri noktası iletişimleri sırasında Configuration Manager tarafından kullanılır. IPSec ilkelerine veya güvenlik duvarlarını yapılandırmaya yönelik IP filtresi bilgilerini tanımlarken bu bağlantı noktalarını gözden geçirdiğinizden emin olun.  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Yapılandırılabilir olmayan bağlantı noktaları  

Configuration Manager, aşağıdaki iletişim türleri için bağlantı noktalarını yapılandırmanıza izin vermez:  

- Siteden siteye  

- Site sunucusundan site sistemine  

- Configuration Manager konsolunu SMS sağlayıcısına  

- Configuration Manager konsolunu internet 'e  

- Microsoft Intune ve bulut dağıtım noktaları gibi bulut hizmetlerine yönelik bağlantılar  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Configuration Manager istemcileri ve site sistemleri tarafından kullanılan bağlantı noktaları  

Aşağıdaki bölümler Configuration Manager iletişim için kullanılan bağlantı noktalarını ayrıntılandırır. Bölüm başlığındaki oklar, iletişimin yönünü gösterir:  

- --> bir bilgisayarın iletişimi başladığını ve diğer bilgisayarın her zaman yanıt verdiğini gösterir  

- &lt;--> her iki bilgisayarın da iletişim başlatabileceğini belirtir  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> Varlık Yönetim Bilgileri eşitleme noktası--> Microsoft  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Varlık Yönetim Bilgileri eşitleme noktası--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Uygulama Kataloğu Web hizmet noktası--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Uygulama Kataloğu web sitesi noktası--> Uygulama Kataloğu Web hizmet noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> İstemci--> Uygulama Kataloğu web sitesi noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> İstemci--> Istemcisi  

Uyandırma proxy 'si aynı zamanda bir istemciden başka bir istemciye ıCMP yankı isteği iletileri de kullanır. İstemciler, diğer istemcinin ağda uyanık olup olmadığını doğrulamak için bu iletişimi kullanır. ICMP bazen ping komutları olarak adlandırılır. ICMP 'nin bir UDP veya TCP protokol numarası yoktur ve bu nedenle aşağıdaki tabloda listelenmez. Ancak, alt ağ içindeki müdahalede bulunan ağ aygıtlarındaki veya bu istemci bilgisayarlarındaki herhangi bir ana bilgisayar tabanlı güvenlik duvarı, uyandırma proxy'si iletişiminin başarılı olması için ICMP trafiğine izin vermelidir.  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|LAN'da Uyandırma|9 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|--|  
|Uyandırma proxy'si|25536 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|--|  
|Windows PE Eş Önbelleği yayını|8004|--|  
|Windows PE Eş Önbelleği indirmesi|--|8003|  

Daha fazla bilgi için bkz. [WINDOWS PE Eş Önbelleği](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements).

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> İstemci--> Configuration Manager ağ cihazı kayıt hizmeti (NDES) ilke modülü

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> İstemci--> bulut dağıtım noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Daha fazla bilgi için bkz. [bağlantı noktaları ve veri akışı](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> İstemci--bulut yönetimi ağ geçidi > (CMG)  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Daha fazla bilgi için bkz. [CMG bağlantı noktaları ve veri akışı](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> İstemci--> dağıtım noktası, hem standart hem de çekme  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|
|Hızlı güncelleştirmeler|--|8005 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> Hızlı güncelleştirmeler için alternatif bağlantı noktasını yapılandırmak üzere istemci ayarlarını kullanın. Daha fazla bilgi için bkz. [istemcilerin Delta içeriği isteklerini almak için kullandığı bağlantı noktası](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content).

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> İstemci--> çok noktaya yayın için yapılandırılmış dağıtım noktası, hem standart hem de çekme  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|Çok noktaya yayın Protokolü|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> İstemci--> PXE için yapılandırılmış dağıtım noktası, hem standart hem de çekme  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 ve 68|--|  
|TFTP|69 <sup> [Note 4](#bkmk_note4)</sup> |--|  
|Önyükleme Bilgileri Anlaşma Katmanı (BINL)|4011|--|  

> [!Important]  
> Ana bilgisayar tabanlı bir güvenlik duvarını etkinleştirirseniz kuralların, bu bağlantı noktalarında sunucunun gönderilmesini ve almasına izin aldığından emin olun. PXE için bir dağıtım noktası etkinleştirdiğinizde Configuration Manager, Windows güvenlik duvarında gelen (alma) kuralları etkinleştirebilir. Giden (gönderme) kurallarını yapılandırmaz.<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> İstemci--> geri dönüş durumu noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> İstemci--> genel katalog etki alanı denetleyicisi

Configuration Manager istemcisi, bir çalışma grubu bilgisayarı olduğunda veya yalnızca internet iletişimi için yapılandırıldığında bir genel katalog sunucusuyla bağlantı kuramıyor.  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Genel Katalog LDAP|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a> İstemci--> yönetim noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|İstemci bildirimi (HTTP veya HTTPS'ye geri dönmeden önce  varsayılan iletişim)|--|10123 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|HTTP|--|80 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> İstemci--> yazılım güncelleştirme noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 veya 8530 <sup> [Note 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 veya 8531 <sup> [Note 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> İstemci--> durum geçiş noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|Sunucu İleti Bloğu (SMB)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> CMG bağlantı noktası--> CMG bulut hizmeti  

Configuration Manager CMG kanalını derlemek için bu bağlantıları kullanır. Daha fazla bilgi için bkz. [CMG bağlantı noktaları ve veri akışı](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (tercih edilen)|--|10140-10155|  
|HTTPS (bir VM ile geri dönüş)|--|443|  
|HTTPS (iki veya daha fazla VM ile geri dönüş)|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a> CMG bağlantı noktası--> yönetim noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Daha fazla bilgi için bkz. [CMG bağlantı noktaları ve veri akışı](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> CMG bağlantı noktası--> yazılım güncelleştirme noktası  

Belirli bir bağlantı noktası, yazılım güncelleştirme noktası yapılandırmasına bağlıdır.

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Daha fazla bilgi için bkz. [CMG bağlantı noktaları ve veri akışı](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Configuration Manager konsolu--> Istemci  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Uzaktan Denetim (denetim)|--|2701|  
|Uzaktan Yardım (RDP ve RTC)|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Configuration Manager konsolu--Internet >  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

Configuration Manager konsolu aşağıdaki eylemler için Internet erişimini kullanır:

- Dağıtım paketleri için Microsoft Update yazılım güncelleştirmeleri indiriliyor.
- Şeritteki geri bildirim öğesi.
- Konsolun içindeki belgelerin bağlantıları.
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Configuration Manager konsolu--> Reporting Services noktası  

|Açıklama|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|80 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Configuration Manager konsolu--> site sunucusu  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (sağlayıcı sistemini konumlamak için WMI'ya ilk bağlantı)|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Configuration Manager konsolu--> SMS sağlayıcısı  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager ağ cihazı kayıt hizmeti (NDES) ilke modülü--> sertifika kayıt noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> Veri ambarı hizmet noktası--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a> Dağıtım noktası, hem standart hem de çekme--> yönetim noktası

Bir dağıtım noktası aşağıdaki senaryolarda yönetim noktasıyla iletişim kurar:  

- Önceden hazırlanan içeriğin durumunu raporlamak için  

- Kullanım özeti verilerini bildirmek için  

- İçerik doğrulamayı bildirmek için  

- Paket indirmelerinin durumunu raporlamak için (yalnızca çekme dağıtım noktası)

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection noktası--Internet >  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection noktası--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Kayıt proxy noktası--> kayıt noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Kayıt noktası--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server Bağlayıcısı--Exchange Online >  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS üzerinden Windows Uzak Yönetimi|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server Bağlayıcısı--şirket Içi Exchange Server >  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP üzerinden Windows Uzak Yönetimi|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac bilgisayar--> kayıt proxy noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Yönetim noktası--> etki alanı denetleyicisi  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Hafif Dizin Erişim Protokolü (LDAP)|389|389|  
|Güvenli LDAP (LDAPS, imzalama ve bağlama için)|636|636|  
|Genel Katalog LDAP|--|3268|  
|RPC Bitiş Noktası Eşleştiricisi|--|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a> Yönetim noktası &lt; --> site sunucusu

<sup>[5. nota](#bkmk_note5)</sup>

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Bitiş Noktası Eşleştiricisi|--|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  
|Sunucu İleti Bloğu (SMB)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Yönetim noktası--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Mobil cihaz--> kayıt proxy noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Raporlama Hizmetleri noktası--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a> Hizmet bağlantı noktası--Azure > (CMG)  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|CMG hizmeti dağıtımı için HTTPS|--|443|

Daha fazla bilgi için bkz. [CMG bağlantı noktaları ve veri akışı](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Site sunucusu &lt; --> Uygulama Kataloğu Web hizmet noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Site sunucusu &lt; --> Uygulama Kataloğu web sitesi noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Site sunucusu &lt; --> varlık yönetim bilgileri eşitleme noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a> Site sunucusu--> Istemci  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|LAN'da Uyandırma|9 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Site sunucusu--> bulut dağıtım noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Daha fazla bilgi için bkz. [bağlantı noktaları ve veri akışı](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> Site sunucusu--> dağıtım noktası, hem standart hem de çekme

<sup>[5. nota](#bkmk_note5)</sup>  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Site sunucusu--> etki alanı denetleyicisi  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Hafif Dizin Erişim Protokolü (LDAP)|389|389|
|Güvenli LDAP (LDAPS, imzalama ve bağlama için)|636|636|
|Genel Katalog LDAP|--|3268|  
|RPC Bitiş Noktası Eşleştiricisi|--|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Site sunucusu &lt; --> sertifika kayıt noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a> Site sunucusu &lt; --> CMG bağlantı noktası

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Site sunucusu &lt; --> Endpoint Protection noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Site sunucusu &lt; --> kayıt noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Site sunucusu &lt; --> kayıt proxy noktası  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Site sunucusu &lt; --> geri dönüş durumu noktası

<sup>[5. nota](#bkmk_note5)</sup>  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> Site sunucusu--Internet >  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Note 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Site sunucusu &lt; --> sertifika yetkilisini (CA) verme

Bu iletişim, sertifika profillerini sertifika kayıt noktasını kullanarak dağıttığınızda kullanılır. İletişim, hiyerarşideki her site sunucusu için kullanılmaz. Bunun yerine, yalnızca hiyerarşinin en üstündeki site sunucusu için kullanılır.  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC (DCOM)|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> Site sunucusu--uzak içerik kitaplığı paylaşımının barındırıldığı sunucu >

Merkezi Yönetim veya birincil site sunucularınızda sabit disk alanı boşaltmak için içerik kitaplığını başka bir depolama konumuna taşıyabilirsiniz. Daha fazla bilgi için bkz. [site sunucusu için uzak içerik kitaplığı yapılandırma](the-content-library.md#bkmk_remote).

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a> Site sunucusu &lt; --> hizmet bağlantı noktası

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Site sunucusu &lt; --> Reporting Services noktası

<sup>[5. nota](#bkmk_note5)</sup>  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a> Site sunucusu &lt; --site sunucusu >  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Site sunucusu--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

Site veritabanını barındırmak için uzak bir SQL Server kullanan bir sitenin yüklenmesi sırasında, site sunucusu ve SQL Server arasında aşağıdaki bağlantı noktalarını açın:  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> Site sunucusu--WSUS için > SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 3](#bkmk_note3) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Site sunucusu--> SMS sağlayıcısı  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  
|RPC|--|DINAMIK <sup> [dekont 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Site sunucusu &lt; --> yazılım güncelleştirme noktası

<sup>[5. nota](#bkmk_note5)</sup>  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|HTTP|--|80 veya 8530 <sup> [Note 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 veya 8531 <sup> [Note 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Site sunucusu &lt; --> durum geçiş noktası

<sup>[5. nota](#bkmk_note5)</sup>  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  
|RPC Bitiş Noktası Eşleştiricisi|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> SMS sağlayıcısı--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Yazılım güncelleştirme noktası--Internet >  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Note 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Yazılım güncelleştirme noktası--yukarı akış WSUS sunucusu >  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 veya 8530 <sup> [Note 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 veya 8531 <sup> [Note 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server

Siteler arası veritabanı çoğaltması, bir sitedeki SQL Server, üst veya alt sitesindeki SQL Server doğrudan iletişim kurmasını gerektirir.  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server hizmeti|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  
|SQL Server Hizmet Aracısı|--|4022 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

> [!TIP]  
> Configuration Manager, UDP 1434 numaralı bağlantı noktasını kullanan SQL Server Browser gerektirmez.  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Durum geçiş noktası--> SQL Server  

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|TCP üzerinden SQL|--|1433 <sup> [Note 2](#bkmk_note2) alternatif bağlantı noktası kullanılabilir</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Configuration Manager istemcileri ve site sistemleri tarafından kullanılan bağlantı noktaları için notlar  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> Note 1: proxy sunucu bağlantı noktası

Bu bağlantı noktası yapılandırılamaz ancak yapılandırılmış bir ara sunucu aracılığıyla yönlendirilebilir.  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> 2. Note: alternatif bağlantı noktası kullanılabilir

Bu değer için Configuration Manager alternatif bir bağlantı noktası tanımlayabilirsiniz. Özel bir bağlantı noktası tanımlarsanız, IPSec ilkeleri için IP filtresi bilgilerinde bu özel bağlantı noktasını kullanın veya güvenlik duvarlarını yapılandırın.  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> Note 3: Windows Server Update Services (WSUS)

WSUS, istemci iletişimi için 80/443 veya bağlantı noktaları 8530/8531 olan bağlantı noktalarını kullanmak üzere yüklenebilir. WSUS 'i Windows Server 2012 veya Windows Server 2016 ' de çalıştırdığınızda, WSUS varsayılan olarak HTTP için bağlantı noktası 8530 ' i ve HTTPS için bağlantı noktası 8531 ' i kullanacak şekilde yapılandırılır.  

Yüklemeden sonra bu bağlantı noktasını değiştirebilirsiniz. Site hiyerarşisi genelinde aynı bağlantı noktası numarasını kullanmak zorunda değilsiniz.  

- HTTP bağlantı noktası 80 ise HTTPS bağlantı noktası 443 olmalıdır.  

- HTTP bağlantı noktası başka bir şeydir, HTTPS bağlantı noktası 1 veya daha yüksek olmalıdır, örneğin, 8530 ve 8531.

    > [!NOTE]  
    >  Yazılım güncelleştirme noktasını HTTPS kullanmak üzere yapılandırdığınızda HTTP bağlantı noktasının da açık olması gerekir. Belirli güncelleştirmeler için EULA gibi şifrelenmemiş veriler HTTP bağlantı noktasını kullanır.

- WSUS temizlemesi için aşağıdaki seçenekleri etkinleştirdiğinizde site sunucusu, SUSDB 'yi barındıran SQL Server ile bağlantı kurar:
  - WSUS temizleme performansını geliştirmek için, kümelenmiş olmayan dizinleri WSUS veritabanına ekleme
  - Eski güncelleştirmeleri WSUS veritabanından kaldır
  
  Varsayılan SQL Server bağlantı noktası SQL Server Yapılandırma Yöneticisi ile alternatif bir bağlantı noktasına değiştirilirse, site sunucusunun tanımlı bağlantı noktasını kullanarak bağlanabildiğinden emin olun. Configuration Manager, dinamik bağlantı noktalarını desteklemez. Varsayılan olarak, SQL Server adlandırılmış örnekler veritabanı altyapısına bağlantılar için dinamik bağlantı noktaları kullanır. Adlandırılmış bir örnek kullandığınızda, statik bağlantı noktasını el ile yapılandırın.

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> Note 4: önemsiz FTP (TFTP) arka plan programı

Önemsiz FTP (TFTP) arka plan programı sistem hizmeti, bir Kullanıcı adı veya parola gerektirmez ve Windows Dağıtım Hizmetleri 'nin (WDS) ayrılmaz bir parçasıdır. Önemsiz FTP arka plan programı hizmeti, aşağıdaki RFC 'Lerle tanımlanan TFTP protokolü için destek uygular:  

- RFC 1350: TFTP  

- RFC 2347: seçenek uzantısı  

- RFC 2348: blok boyutu seçeneği  

- RFC 2349: zaman aşımı aralığı ve aktarım boyutu seçenekleri  

TFTP, disksiz önyükleme ortamlarını destekleyecek şekilde tasarlanmıştır. TFTP Arka Plan Programları, UDP bağlantı noktası 69'dan dinleme yapar ancak dinamik olarak ayrılan bir yüksek bağlantı noktasından yanıt verir. Bu bağlantı noktasını etkinleştirirseniz, TFTP hizmeti gelen TFTP isteklerini alabilir, ancak seçilen sunucu bu isteklere yanıt veremez. TFTP sunucusunu 69 numaralı bağlantı noktasından yanıt verecek şekilde yapılandırmadığınız müddetçe, seçilen sunucunun gelen TFTP isteklerine yanıt vermesini etkinleştiremezsiniz.  

PXE 'yi destekleyen dağıtım noktası ve Windows PE 'deki istemci, TFTP aktarımları için dinamik olarak ayrılan yüksek bağlantı noktalarını seçin. Bu bağlantı noktaları, Microsoft tarafından 49152 ve 65535 arasında tanımlanır. Daha fazla bilgi için bkz. [Windows Için hizmet genel bakışı ve ağ bağlantı noktası gereksinimleri](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

Ancak, gerçek PXE önyüklemesi sırasında cihazdaki ağ kartı, TFTP aktarımı sırasında kullandığı dinamik olarak ayrılan yüksek bağlantı noktasını seçer. Cihazdaki ağ kartı, Microsoft tarafından tanımlanan, dinamik olarak ayrılan yüksek bağlantı noktalarına bağlı değildir. Yalnızca RFC 1350 ' de tanımlanan bağlantı noktalarına bağlanır. Bu bağlantı noktası 0 ile 65535 arasında olabilir. Ağ kartının kullandığı dinamik olarak ayrılan yüksek bağlantı noktaları hakkında daha fazla bilgi için, cihaz donanım üreticisine başvurun.

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> Note 5: site sunucusu ve site sistemleri arasındaki Iletişim

Varsayılan olarak, site sunucusu ve site sistemleri arasındaki iletişim çift yönlüdür. Site sunucusu, site sistemini yapılandırmak için iletişim başlatır ve ardından çoğu site sistemi, durum bilgilerini göndermek için site sunucusuna geri bağlanır. Raporlama hizmeti noktaları ve dağıtım noktaları durum bilgileri göndermez. Site sistemi yüklendikten sonra site sistem özelliklerinde site **sunucusunun bu site sistemine yönelik bağlantıları başlatmasını gerektir** ' i seçerseniz, site sistemi site sunucusuyla iletişimi başlatmaz. Bunun yerine, site sunucusu iletişimi başlatır. Site sistemi sunucusuna kimlik doğrulaması için site sistemi yükleme hesabını kullanır.  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> Note 6: dinamik bağlantı noktaları

Dinamik bağlantı noktaları, işletim sistemi sürümü tarafından tanımlanan bir dizi bağlantı noktası numarası kullanır. Bu bağlantı noktaları, kısa ömürlü bağlantı noktaları olarak da bilinir. Varsayılan bağlantı noktası aralıkları hakkında daha fazla bilgi için, bkz. [Windows için ağ bağlantı noktası koşulları ve hizmete genel bakış](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Bağlantı noktası ek listeleri  

Aşağıdaki bölümlerde, Configuration Manager tarafından kullanılan bağlantı noktaları hakkında ek bilgiler sağlanmaktadır.

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> İstemciden sunucuya paylaşımlar

İstemciler, UNC paylaşımlarına bağlandıklarında Sunucu İleti Bloğu (SMB) kullanır. Örnek:

- **/Source:** komut satırı özelliğini CCMSetup.exe belirten el ile istemci yüklemesi  

- Bir UNC yolundan tanım dosyalarını indirten istemciler Endpoint Protection

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|Sunucu İleti Bloğu (SMB)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Microsoft SQL Server bağlantılar

SQL Server veritabanı motoruna bağlantı ve siteler arası çoğaltma için, varsayılan SQL Server bağlantı noktasını kullanabilir veya özel bağlantı noktaları belirleyebilirsiniz:  

- Siteler arası iletişimler aşağıdakileri kullanır:  

  - TCP 4022 bağlantı noktasına varsayılan olan SQL Server Hizmet Aracısı.  

  - TCP 1433 bağlantı noktası varsayılan olarak SQL Server hizmet.  

- SQL Server veritabanı altyapısı ve çeşitli Configuration Manager site sistem rolleri arasındaki site içi iletişim, TCP 1433 bağlantı noktasına varsayılan olarak sahiptir.  

- Configuration Manager, site veritabanını barındıran her bir SQL kullanılabilirlik grubu çoğaltması ile iletişim kurmak için aynı bağlantı noktalarını ve protokolleri kullanır; bu, çoğaltma tek başına SQL Server örneğidir.

Azure kullandığınızda ve site veritabanı bir iç veya dış yük dengeleyicinin arkasında olduğunda, aşağıdaki bileşenleri yapılandırın:

- Her yinelemede güvenlik duvarı özel durumları
- Yük Dengeleme kuralları

Aşağıdaki bağlantı noktalarını yapılandırın:

- TCP üzerinden SQL: TCP 1433
- SQL Server Hizmet Aracısı: TCP 4022
- Sunucu Ileti bloğu (SMB): TCP 445
- RPC uç nokta Eşleyici: TCP 135

> [!WARNING]  
> Configuration Manager, dinamik bağlantı noktalarını desteklemez. Varsayılan olarak, SQL Server adlandırılmış örnekler veritabanı altyapısına bağlantılar için dinamik bağlantı noktaları kullanır. Adlandırılmış bir örnek kullandığınızda, site içi iletişim için statik bağlantı noktasını el ile yapılandırın.  

Aşağıdaki site sistem rolü, SQL Server veritabanıyla doğrudan iletişim kurar:  

- Uygulama Kataloğu web hizmet noktası  

- Sertifika kayıt noktası rolü  

- Kayıt noktası rolü  

- Yönetim noktası  

- Site sunucusu  

- Raporlama hizmetleri noktası  

- site veritabanı  

- SQL Server--> SQL Server  

Bir SQL Server birden fazla siteden bir veritabanı barındırdığınızda, her veritabanının ayrı bir SQL Server örneğini kullanması gerekir. Her örneği, benzersiz bir bağlantı noktası kümesiyle yapılandırın.  

SQL Server 'da ana bilgisayar tabanlı bir güvenlik duvarını etkinleştirirseniz, doğru bağlantı noktalarına izin vermek için yapılandırın. Ayrıca, SQL Server ile iletişim kuran bilgisayarlar arasında bulunan ağ güvenlik duvarlarını yapılandırın.  

Belirli bir bağlantı noktasını kullanmak üzere SQL Server nasıl yapılandırılacağı hakkında bir örnek için, bkz. [belirli BIR TCP bağlantı noktasını dinlemek için sunucu yapılandırma](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> Bulma ve yayımlama

Configuration Manager, site bilgilerini bulmak ve yayımlamak için aşağıdaki bağlantı noktalarını kullanır:

- Hafif Dizin Erişim Protokolü (LDAP): 389
- Güvenli LDAP (LDAPS, imzalama ve bağlama için): 636
- Genel Katalog LDAP: 3268
- RPC uç nokta Eşleyici: 135
- RPC: dinamik olarak ayrılan yüksek TCP bağlantı noktaları
- TCP: 1024:5000
- TCP: 49152:65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Configuration Manager tarafından yapılan dış bağlantılar

Şirket içi Configuration Manager istemcileri veya site sistemleri aşağıdaki harici bağlantıları yapabilir:  

- [Varlık Yönetim Bilgileri eşitleme noktası-- &gt; Microsoft](#BKMK_PortsAI)  

- [Endpoint Protection noktası-- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

- [İstemci-- &gt; genel katalog etki alanı denetleyicisi](#BKMK_PortsClient-GCDC)  

- [Configuration Manager Konsolu-- &gt; Internet](#BKMK_PortsConsole-Internet)  

- [Yönetim noktası-- &gt; etki alanı denetleyicisi](#BKMK_PortsMP-DC)  

- [Site sunucusu-- &gt; etki alanı denetleyicisi](#BKMK_PortsSite-DC)  

- [Site sunucusu &lt;  -- &gt; sertifika verme yetkilisi (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [Yazılım güncelleştirme noktası-- &gt; Internet](#BKMK_PortsSUP-Internet)  

- [Yazılım güncelleştirme noktası-- &gt; yukarı AKıŞ WSUS sunucusu](#BKMK_PortsSUP-WSUS)  

- [Hizmet bağlantı noktası--Azure >](#bkmk_scp-cmg)  

- [CMG bağlantı noktası--> CMG bulut hizmeti](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Internet tabanlı istemcileri destekleyen site sistemleri için Yükleme gereksinimleri

> [!Note]  
> Bu bölüm yalnızca İnternet tabanlı istemci yönetimi (IBCM) için geçerlidir. Bulut yönetimi ağ geçidi için uygulanmaz. Daha fazla bilgi için bkz. [İnternet 'te Istemcileri yönetme](../../clients/manage/manage-clients-internet.md).  

Internet tabanlı yönetim noktaları, Internet tabanlı istemcileri destekleyen dağıtım noktaları, yazılım güncelleştirme noktası ve geri dönüş durumu noktası yükleme ve onarım için aşağıdaki bağlantı noktalarını kullanır:  

- Site sunucusu--> site sistemi: UDP ve TCP bağlantı noktası 135 kullanarak RPC Bitiş Noktası Eşleştiricisi.  

- Site sunucusu--> site sistemi: RPC dinamik TCP bağlantı noktaları  

- Site sunucusu &lt; --> site sistemi: TCP bağlantı noktası 445 kullanan sunucu ileti blokları (SMB)

Dağıtım noktalarındaki uygulama ve paket yüklemeleri aşağıdaki RPC bağlantı noktalarını gerektirir:  

- Site sunucusu--> dağıtım noktası: UDP ve TCP bağlantı noktası 135 kullanarak RPC Bitiş Noktası Eşleştiricisi

- Site sunucusu--> dağıtım noktası: RPC dinamik TCP bağlantı noktaları  

Site sunucusu ve site sistemleri arasında trafiği güvenli hale getirmek için IPsec kullanın. RPC ile kullanılan dinamik bağlantı noktalarını kısıtlamanız gerekiyorsa, Microsoft RPC yapılandırma aracını (rpccfg.exe) kullanabilirsiniz. Bu RPC paketleri için sınırlı bir bağlantı noktası aralığı yapılandırmak için aracını kullanın. Daha fazla bilgi için bkz. [RPC 'nin belirli bağlantı noktalarını kullanacak şekilde yapılandırılması ve bu bağlantı noktalarının IPSec kullanarak güvenliğinin sağlanmasına yardımcı olma](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]
> Bu site sistemlerini yüklemeden önce, uzak kayıt defteri hizmetinin site sistem sunucusunda çalıştığından ve site sistemi, güven ilişkisi olmadan farklı bir Active Directory ormanındaysa bir site sistem yükleme hesabı belirttiğinizden emin olun. Örneğin, uzak kayıt defteri hizmeti, dağıtım noktaları (hem çekme hem de standart), uzak SQL Server ve Uygulama Kataloğu gibi site sistemlerini çalıştıran sunucularda kullanılır.

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Configuration Manager istemci yüklemesinin kullandığı bağlantı noktaları

Configuration Manager istemci yüklemesi sırasında kullanılan bağlantı noktaları, dağıtım yöntemine bağlıdır.

- Her istemci dağıtım yöntemi için bağlantı noktalarının listesi için bkz. [Configuration Manager istemci dağıtımı sırasında kullanılan bağlantı noktaları](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment)  

- İstemci yüklemesi ve yükleme sonrası iletişim için istemcide Windows Güvenlik Duvarı 'nı yapılandırma hakkında daha fazla bilgi için bkz. [istemciler Için Windows Güvenlik Duvarı ve bağlantı noktası ayarları](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md)  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Geçiş tarafından kullanılan bağlantı noktaları

Geçişi çalıştıran site sunucusu, kaynak hiyerarşisindeki ilgili sitelere bağlanmak için çeşitli bağlantı noktaları kullanır. Daha fazla bilgi için, bkz. [geçiş Için gereken yapılandırma](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations).  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Windows Server tarafından kullanılan bağlantı noktaları

Aşağıdaki tabloda, Windows Server tarafından kullanılan bazı anahtar bağlantı noktaları listelenmektedir.

|Açıklama|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 ve 68|--|  
|NetBIOS Ad Çözümlemesi|137|--|  
|NetBIOS Veri Birimi Hizmeti|138|--|  
|NetBIOS Oturum Hizmeti|--|139|  
|Kerberos kimlik doğrulaması|--|88|

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Windows Server sistemi için hizmet genel bakışı ve ağ bağlantı noktası gereksinimleri](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

- [Etki alanları ve güvenler için güvenlik duvarı yapılandırma](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)