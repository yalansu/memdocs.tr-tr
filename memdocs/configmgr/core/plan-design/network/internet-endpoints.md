---
title: İnternet erişimi gereksinimleri
titleSuffix: Configuration Manager
description: Configuration Manager özelliklerinin tam işlevselliğine izin vermek için İnternet uç noktaları hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a71fcd23977cc105a8d64f59edc45333cbd8c451
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068244"
---
# <a name="internet-access-requirements"></a>İnternet erişimi gereksinimleri

Bazı Configuration Manager özellikleri, tüm işlevler için internet bağlantısı kullanır. Kuruluşunuz ağ iletişimini bir güvenlik duvarı veya ara cihaz kullanarak internet ile kısıtlarsa, bu uç noktalara izin vermeyi unutmayın.

<!-- SCCMDocs-pr #3403 -->

Configuration Manager, ürün genelinde aşağıdaki Microsoft URL iletme hizmetlerini kullanır:

- `https://aka.ms`
- `https://go.microsoft.com`

Aşağıdaki bölümlerde açıkça listelenmese de, bu uç noktalara her zaman izin vermeniz gerekir.

## <a name="service-connection-point"></a><a name="bkmk_scp"></a> Hizmet bağlantı noktası

Bu yapılandırma, hizmet bağlantı noktasını barındıran bilgisayar ve bu bilgisayar ile internet arasında güvenlik duvarları için geçerlidir. Her ikisi de, HTTPS için giden bağlantı noktası **tcp 443** ve aşağıdaki Internet konumlarına http için **TCP 80** giden bağlantı noktası üzerinden iletişime izin vermelidir.

Hizmet bağlantı noktası, bu konumların kullanılması için bir Web proxy (kimlik doğrulaması olmadan veya olmayan) kullanmayı destekler. Daha fazla bilgi için bkz. [proxy sunucu desteği](proxy-server-support.md).

Hizmet bağlantı noktası hakkında daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../../servers/deploy/configure/about-the-service-connection-point.md).

Diğer Configuration Manager özellikleri, hizmet bağlantı noktasından ek uç noktalar gerektirebilir. Daha fazla bilgi için bu makaledeki diğer bölümlere bakın.

> [!TIP]  
> Hizmet bağlantı noktası, veya ' a bağlanırken Microsoft Intune hizmetini kullanır `go.microsoft.com` `manage.microsoft.com` . Tedarikçinin bağlayıcının, Baltimore CyberTrust kök sertifikası yüklü değilse, kullanım dolmuşsa veya hizmet bağlantı noktasında bozulması durumunda bağlantı sorunlarıyla karşılaşdığı bilinen bir sorun vardır. Daha fazla bilgi için bkz. [KB 3187516: hizmet bağlantı noktası güncelleştirmeleri indirmiyor](https://support.microsoft.com/help/3187516).  

Sürüm 2002 ' den başlayarak, Configuration Manager site bir bulut hizmeti için gerekli uç noktalara bağlanamazsa, kritik bir durum ileti KIMLIĞI 11488 oluşturur. Hizmete bağlanamadığınızda SMS_SERVICE_CONNECTOR bileşen durumu kritik olarak değişir. Configuration Manager konsolunun [Bileşen durumu](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) düğümünde ayrıntılı durumu görüntüleyin.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a> Güncelleştirmeler ve bakım

Bu işlev hakkında daha fazla bilgi için bkz. [güncelleştirmeler ve bakım Configuration Manager](../../servers/manage/updates.md).

> [!Tip]  
> Bu uç noktaları [Yönetim Insight](../../servers/manage/management-insights.md) kuralı için etkinleştirin, **siteyi Configuration Manager güncelleştirmeleri için Microsoft bulutuna bağlayın**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Windows 10 Bakımı

Bu işlev hakkında daha fazla bilgi için bkz. [Windows 'u hizmet olarak yönetme](../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Azure hizmetleri

Bu işlev hakkında daha fazla bilgi için bkz. [Azure hizmetlerini Configuration Manager ile kullanım Için yapılandırma](../../servers/deploy/configure/azure-services-wizard.md).

- `management.azure.com` (Azure genel bulutu)
- `management.usgovcloudapi.net` (Azure ABD kamu bulutu)

## <a name="co-management"></a>Ortak yönetim

Windows 10 cihazlarını ortak yönetim için Microsoft Intune kaydederseniz, bu cihazların Intune için gereken uç noktalara erişebildiğinizden emin olun. Daha fazla bilgi için bkz. [Microsoft Intune Için ağ uç noktaları](/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Iş için Microsoft Store

[İş için Microsoft Store](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)Configuration Manager tümleştirirseniz, hizmet bağlantı noktasının ve hedeflenen cihazların bulut hizmetine erişebildiğinden emin olun. Daha fazla bilgi için bkz. [iş proxy yapılandırması için Microsoft Store](/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="delivery-optimization"></a>Teslim iyileştirme

Teslim iyileştirme kullanıyorsanız, istemcilerin bulut hizmetiyle iletişim kurması gerekir: `*.do.dsp.mp.microsoft.com`

Microsoft bağlı önbelleğini destekleyen dağıtım noktaları da bu uç noktaları gerektirir.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Teslim iyileştirme hakkında SSS](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Configuration Manager 'de içerik yönetimi için temel kavramlar](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Configuration Manager 'de Microsoft bağlı önbelleği](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> Bulut Hizmetleri

<!-- SCCMDocs-pr #3402 -->

Bu bölüm aşağıdaki özellikleri içerir:

- Bulut yönetimi ağ geçidi (CMG)
- Bulut dağıtım noktası (CDP)
- Azure Active Directory (Azure AD) Tümleştirmesi
- Azure AD tabanlı bulma

CMG hakkında daha fazla bilgi için bkz. [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).

Aşağıdaki bölümlerde, uç noktalar role göre listelenmektedir. Bazı uç noktalar `<name>` , CMG veya CDP 'nin bulut hizmeti adı olan bir hizmete başvurur. Örneğin, CMG 'niz ise `GraniteFalls.CloudApp.Net` gerçek depolama uç noktası olur `GraniteFalls.blob.core.windows.net` .<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>Hizmet bağlantı noktası

CMG/CDP hizmet dağıtımı için hizmet bağlantı noktasının erişimi olması gerekir:

- Belirli Azure uç noktaları, yapılandırmaya bağlı olarak ortam başına farklıdır. Configuration Manager bu uç noktaları site veritabanında depolar. Azure uç noktaları listesi için SQL Server **AzureEnvironments** tablosunu sorgulayın.

- [Azure hizmetleri](#azure-services)

- Azure AD Kullanıcı keşfi için:

  - Sürüm 1902 ve üzeri: Microsoft Graph uç noktası `https://graph.microsoft.com/`

  - Sürüm 1810 ve önceki sürümler: Azure AD Graph uç noktası `https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>CMG bağlantı noktası

CMG bağlantı noktasının aşağıdaki hizmet uç noktalarına erişmesi gerekir:

- Bulut hizmeti adı (CMG veya CDP için):
  - `<name>.cloudapp.net` (Azure genel bulutu)
  - `<name>.usgovcloudapp.net` (Azure ABD kamu bulutu)

- Hizmet yönetimi uç noktası: `https://management.core.windows.net/`  

- Depolama uç noktası (içerik etkinleştirilmiş CMG veya CDP için):
  - `<name>.blob.core.windows.net` (Azure genel bulutu)
  - `<name>.blob.core.usgovcloudapi.net` (Azure ABD kamu bulutu)
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

CMG bağlantı noktası site sistemi, bir Web proxy 'si kullanmayı destekler. Bu rolü bir proxy için yapılandırma hakkında daha fazla bilgi için bkz. [proxy sunucu desteği](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). CMG bağlantı noktasının yalnızca CMG hizmet uç noktalarına bağlanması gerekir. Diğer Azure uç noktalarına erişmesi gerekmez.

### <a name="configuration-manager-client"></a>Configuration Manager istemcisi

- Bulut hizmeti adı (CMG veya CDP için):
  - `<name>.cloudapp.net` (Azure genel bulutu)
  - `<name>.usgovcloudapp.net` (Azure ABD kamu bulutu)

- Depolama uç noktası (içerik etkinleştirilmiş CMG veya CDP için):
  - `<name>.blob.core.windows.net` (Azure genel bulutu)
  - `<name>.blob.core.usgovcloudapi.net` (Azure ABD kamu bulutu)

- Azure AD belirteç alımı için Azure AD uç noktası:
  - `login.microsoftonline.com` (Azure genel bulutu)
  - `login.microsoftonline.us` (Azure ABD kamu bulutu)

### <a name="configuration-manager-console"></a>Configuration Manager konsolu

- Azure AD belirteç alımı için Azure AD uç noktası:

  - Azure genel bulutu
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Azure ABD kamu bulutu
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a> Yazılım güncelleştirmeleri

WSUS ve otomatik güncelleştirmelerin Microsoft Update bulut hizmetiyle iletişim kurabilmesi için etkin yazılım güncelleştirme noktasının aşağıdaki uç noktalara erişmesine izin verin:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://ntservicepack.microsoft.com`  

Yazılım güncelleştirmeleri hakkında daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md).

### <a name="intranet-firewall"></a>Intranet güvenlik duvarı

Aşağıdaki durumlarda iki site sistemi arasındaki bir güvenlik duvarına uç noktalar eklemeniz gerekebilir:

- Alt sitelerde bir yazılım güncelleştirme noktası varsa
- Bir sitede uzak bir etkin İnternet tabanlı yazılım güncelleştirme noktası varsa

#### <a name="software-update-point-on-the-child-site"></a>Alt sitede yazılım güncelleştirme noktası

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-microsoft-365-apps"></a>Microsoft 365 uygulamalarını yönetme

> [!NOTE]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

Microsoft 365 uygulamalarını kurumsal olarak dağıtmak ve güncelleştirmek için Configuration Manager kullanıyorsanız aşağıdaki uç noktalara izin verin:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` yazılım güncelleştirme noktasını Kurumsal istemci güncelleştirmelerine yönelik Microsoft 365 uygulamalar için eşitlemeye yönelik

- `config.office.com` kurumsal dağıtımlar için Microsoft 365 uygulamalar için özel yapılandırma oluşturma

- `contentstorage.osi.office.net` Office eklentisi hazırlığını desteklemek için<!-- MEMDocs#410 -->

## <a name="configuration-manager-console"></a>Configuration Manager konsolu

Configuration Manager konsoluna sahip bilgisayarlar belirli özellikler için aşağıdaki Internet uç noktalarına erişim gerektirir:

### <a name="in-console-feedback"></a>Konsol içi geri bildirim

- `http://petrol.office.microsoft.com`

Bu özellik hakkında daha fazla bilgi için bkz. [ürün geri bildirimi](../../understand/find-help.md#product-feedback).

### <a name="community-workspace"></a>Topluluk çalışma alanı

#### <a name="documentation-node"></a>Belge düğümü

Bu konsol düğümü hakkında daha fazla bilgi için, bkz. [Configuration Manager konsolunu kullanma](../../servers/manage/admin-console.md).

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>Topluluk merkezi

Bu özellik hakkında daha fazla bilgi için bkz. [Community hub](../../servers/manage/community-hub.md).

- `https://github.com`

- `https://communityhub.microsoft.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Daha fazla bilgi için bkz. [veri paylaşımını etkinleştirme](../../../desktop-analytics/enable-data-sharing.md#endpoints).

[!INCLUDE [Internet endpoints for Desktop Analytics](includes/internet-endpoints-desktop-analytics.md)]

## <a name="tenant-attach"></a>Kiracı ekleme

Daha fazla bilgi için bkz. [kiracı eklemeyi etkinleştirme](../../../tenant-attach/device-sync-actions.md).

[!INCLUDE [Internet endpoints for tenant attach](includes/internet-endpoints-tenant-attach.md)]

## <a name="endpoint-analytics"></a>Uç nokta analizi

Daha fazla bilgi için bkz. [Endpoint Analytics proxy yapılandırması](../../../../analytics/troubleshoot.md#bkmk_endpoints).

[!INCLUDE [Internet endpoints for Endpoint analytics](includes/internet-endpoints-endpoint-analytics.md)]

## <a name="asset-intelligence"></a>Varlık yönetim bilgileri

<!-- memdocs#470 -->
[Varlık yönetim bilgileri](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)kullanıyorsanız, hizmetin eşitlenmesi için aşağıdaki uç noktalara izin verin:

- `https://sc.microsoft.com`
- `https://ssu2.manage.microsoft.com`

## <a name="microsoft-public-ip-addresses"></a>Microsoft genel IP adresleri

Microsoft IP adresi aralıkları hakkında daha fazla bilgi için bkz. [Microsoft genel IP alanı](https://www.microsoft.com/download/details.aspx?id=53602). Bu adresler düzenli olarak güncelleştirin. Hizmete göre ayrıntı düzeyi yoktur, bu aralıklardaki IP adresleri kullanılabilir.

## <a name="see-also"></a>Ayrıca bkz.

- [Configuration Manager kullanılan bağlantı noktaları](../hierarchy/ports.md)

- [Configuration Manager 'de proxy sunucu desteği](proxy-server-support.md)