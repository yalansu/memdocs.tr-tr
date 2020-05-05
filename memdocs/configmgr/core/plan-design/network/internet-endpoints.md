---
title: İnternet erişimi gereksinimleri
titleSuffix: Configuration Manager
description: Configuration Manager özelliklerinin tam işlevselliğine izin vermek için İnternet uç noktaları hakkında bilgi edinin.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58afaf564a8afaba4569755575fcc7c1757c5529
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110143"
---
# <a name="internet-access-requirements"></a>İnternet erişimi gereksinimleri

Bazı Configuration Manager özellikleri, tüm işlevler için internet bağlantısı kullanır. Kuruluşunuz ağ iletişimini bir güvenlik duvarı veya ara cihaz kullanarak internet ile kısıtlarsa, bu uç noktalara izin vermeyi unutmayın.

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a>Hizmet bağlantı noktası

Bu yapılandırma, hizmet bağlantı noktasını barındıran bilgisayar ve bu bilgisayar ile internet arasında güvenlik duvarları için geçerlidir. Her ikisi de, HTTPS için giden bağlantı noktası **tcp 443** ve aşağıdaki Internet konumlarına http için **TCP 80** giden bağlantı noktası üzerinden iletişime izin vermelidir.

Hizmet bağlantı noktası, bu konumların kullanılması için bir Web proxy (kimlik doğrulaması olmadan veya olmayan) kullanmayı destekler. Daha fazla bilgi için bkz. [proxy sunucu desteği](proxy-server-support.md).

Hizmet bağlantı noktası hakkında daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../../servers/deploy/configure/about-the-service-connection-point.md).

Diğer Configuration Manager özellikleri, hizmet bağlantı noktasından ek uç noktalar gerektirebilir. Daha fazla bilgi için bu makaledeki diğer bölümlere bakın.

> [!TIP]  
> Hizmet bağlantı noktası, `go.microsoft.com` veya `manage.microsoft.com`' a bağlanırken Microsoft Intune hizmetini kullanır. Tedarikçinin bağlayıcının, Baltimore CyberTrust kök sertifikası yüklü değilse, kullanım dolmuşsa veya hizmet bağlantı noktasında bozulması durumunda bağlantı sorunlarıyla karşılaşdığı bilinen bir sorun vardır. Daha fazla bilgi için bkz. [KB 3187516: hizmet bağlantı noktası güncelleştirmeleri indirmiyor](https://support.microsoft.com/help/3187516).  

Sürüm 2002 ' den başlayarak, Configuration Manager site bir bulut hizmeti için gerekli uç noktalara bağlanamazsa, kritik bir durum ileti KIMLIĞI 11488 oluşturur. Hizmete bağlanamadığınızda SMS_SERVICE_CONNECTOR bileşen durumu kritik olarak değişir. Configuration Manager konsolunun [Bileşen durumu](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) düğümünde ayrıntılı durumu görüntüleyin.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"/>Güncelleştirmeler ve bakım

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

- `management.azure.com`  

## <a name="co-management"></a>Ortak yönetim

Windows 10 cihazlarını ortak yönetim için Microsoft Intune kaydederseniz, bu cihazların Intune için gereken uç noktalara erişebildiğinizden emin olun. Daha fazla bilgi için bkz. [Microsoft Intune Için ağ uç noktaları](https://docs.microsoft.com/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Iş için Microsoft Store

[İş için Microsoft Store](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)Configuration Manager tümleştirirseniz, hizmet bağlantı noktasının ve hedeflenen cihazların bulut hizmetine erişebildiğinden emin olun. Daha fazla bilgi için bkz. [iş proxy yapılandırması için Microsoft Store](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="cloud-services"></a><a name="bkmk_cloud"></a>Bulut Hizmetleri

<!-- SCCMDocs-pr #3402 -->

Bu bölüm aşağıdaki özellikleri içerir:

- Bulut yönetimi ağ geçidi (CMG)
- Bulut dağıtım noktası (CDP)
- Azure Active Directory (Azure AD) Tümleştirmesi
- Azure AD tabanlı bulma

CMG/CDP hizmet dağıtımı için **hizmet bağlantı noktasının** erişimi olması gerekir:

- Belirli Azure uç noktaları, yapılandırmaya bağlı olarak ortam başına farklıdır. Configuration Manager bu uç noktaları site veritabanında depolar. Azure uç noktaları listesi için SQL Server **AzureEnvironments** tablosunu sorgulayın.  

**CMG bağlantı noktasının** aşağıdaki hizmet uç noktalarına erişmesi gerekir:

- Hizmet yönetimi uç noktası:`https://management.core.windows.net/`  

- Depolama uç noktası `<name>.blob.core.windows.net` : ve`<name>.table.core.windows.net`

    Burada `<name>` CMG 'NIZ veya CDP 'nizin bulut hizmeti adıdır. Örneğin, CMG 'niz ise `GraniteFalls.CloudApp.Net`, izin verilecek ilk depolama uç noktası olur. `GraniteFalls.blob.core.windows.net`<!-- SCCMDocs#2288 -->

**Configuration Manager konsolu** ve **ISTEMCISI**tarafından Azure AD belirteci alımı için:

- ActiveDirectoryEndpoint`https://login.microsoftonline.com/`  

Azure AD Kullanıcı keşfi için **hizmet bağlantı noktasının** erişimi olması gerekir:

- Sürüm 1810 ve önceki sürümler: Azure AD Graph uç noktası`https://graph.windows.net/`  

- Sürüm 1902 ve üzeri: Microsoft Graph uç noktası`https://graph.microsoft.com/`

Bulut yönetim noktası (CMG) bağlantı noktası site sistemi, bir Web proxy kullanımını destekler. Bu rolü bir proxy için yapılandırma hakkında daha fazla bilgi için bkz. [proxy sunucu desteği](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). CMG bağlantı noktasının yalnızca CMG hizmet uç noktalarına bağlanması gerekir. Diğer Azure uç noktalarına erişmesi gerekmez.

CMG hakkında daha fazla bilgi için bkz. [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).

## <a name="software-updates"></a><a name="bkmk_sum"></a>Yazılım güncelleştirmeleri

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

- `http://test.stats.update.microsoft.com`  

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

## <a name="manage-office-365"></a>Office 365’i yönetme

> [!NOTE]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](https://docs.microsoft.com/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

Microsoft 365 uygulamalarını kurumsal olarak dağıtmak ve güncelleştirmek için Configuration Manager kullanıyorsanız aşağıdaki uç noktalara izin verin:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com`yazılım güncelleştirme noktasını Kurumsal istemci güncelleştirmelerine yönelik Microsoft 365 uygulamalar için eşitlemeye yönelik

- `config.office.com`kurumsal dağıtımlar için Microsoft 365 uygulamalar için özel yapılandırma oluşturma

## <a name="configuration-manager-console"></a>Configuration Manager konsolu

Configuration Manager konsoluna sahip bilgisayarlar belirli özellikler için aşağıdaki Internet uç noktalarına erişim gerektirir:

### <a name="in-console-feedback"></a>Konsol içi geri bildirim

- `http://petrol.office.microsoft.com`

Bu özellik hakkında daha fazla bilgi için bkz. [ürün geri bildirimi](../../understand/find-help.md#product-feedback).

### <a name="community-workspace-documentation-node"></a>Topluluk çalışma alanı, belge düğümü

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Bu konsol düğümü hakkında daha fazla bilgi için, bkz. [Configuration Manager konsolunu kullanma](../../servers/manage/admin-console.md).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>İzleme çalışma alanı, site hiyerarşisi düğümü

**Coğrafi görünümü**kullanırsanız aşağıdaki uç noktaya erişime izin verin:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Masaüstü Analizi bulut hizmeti için gerekli uç noktalar hakkında daha fazla bilgi için bkz. [veri paylaşımını etkinleştirme](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="microsoft-public-ip-addresses"></a>Microsoft genel IP adresleri

Microsoft IP adresi aralıkları hakkında daha fazla bilgi için bkz. [Microsoft genel IP alanı](https://www.microsoft.com/download/details.aspx?id=53602). Bu adresler düzenli olarak güncelleştirin. Hizmete göre ayrıntı düzeyi yoktur, bu aralıklardaki IP adresleri kullanılabilir.

## <a name="see-also"></a>Ayrıca bkz.

- [Configuration Manager kullanılan bağlantı noktaları](../hierarchy/ports.md)

- [Configuration Manager 'de proxy sunucu desteği](proxy-server-support.md)
