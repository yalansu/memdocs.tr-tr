---
title: Gelişmiş HTTP
titleSuffix: Configuration Manager
description: PKI sertifikalarına gerek olmadan istemci iletişimini güvenli hale getirmek için modern kimlik doğrulaması kullanın.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1a6ec98bd350eb0ac8643254f64a9480f156bb13
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86239768"
---
# <a name="enhanced-http"></a>Gelişmiş HTTP

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1356889,1358460-->

> [!Tip]  
> Bu özellik ilk olarak sürüm 1806 ' de [yayın öncesi özelliği](../../servers/manage/pre-release-features.md)olarak sunulmuştur. Sürüm 1810 ' den başlayarak, bu özellik artık yayın öncesi bir özellik değildir.  

Microsoft tüm Configuration Manager iletişim yolları için HTTPS iletişimi kullanılmasını önerir, ancak PKI sertifikalarını yönetme yükü nedeniyle bazı müşteriler zor olur.

Configuration Manager sürüm 1806, istemcilerin site sistemleriyle iletişim kurmasına yönelik iyileştirmeler içerir. Bu geliştirmelerin iki birincil hedefi vardır:  

- PKI sunucusu kimlik doğrulama sertifikalarına gerek olmadan hassas istemci iletişimini güvenli hale getirebilirsiniz.  

- İstemciler, bir ağ erişim hesabı, istemci PKI sertifikası ve Windows kimlik doğrulaması gerekmeden dağıtım noktalarından içeriğe güvenli bir şekilde erişebilir.  

Diğer tüm istemci iletişimleri HTTP üzerinden yapılır. Gelişmiş HTTP, istemci iletişimi veya bir site sistemi için HTTPS 'yi etkinleştirme ile aynı değildir.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> PKI sertifikaları, aşağıdaki gereksinimlere sahip müşteriler için hala geçerli bir seçenektir:  
>
> - Tüm istemci iletişimi HTTPS üzerinden  
> - İmzalama altyapısının gelişmiş denetimi
>
> Ayrıca, zaten PKI kullanıyorsanız, IIS 'deki PKI sertifikası, gelişmiş HTTP açık olsa bile kullanılacaktır.



## <a name="scenarios"></a><a name="bkmk_scenario"></a>Larla

Aşağıdaki senaryolar bu geliştirmelerden faydalanır:  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a>Senaryo 1: Istemciden yönetim noktasına

<!--1356889-->
[Azure Active Directory (Azure AD) ile birleştirilmiş cihazlar](/azure/active-directory/devices/concept-azure-ad-join) , http için yapılandırılmış bir yönetim noktasıyla iletişim kurabilir. Site sunucusu yönetim noktası için güvenli bir kanal üzerinden iletişim kurmasına izin veren bir sertifika oluşturur.

> [!Note]  
> Bu davranış, bir bulut yönetimi ağ geçidi üzerinden iletişim kuran Azure AD 'ye katılmış istemciler için HTTPS özellikli bir yönetim noktası gerektiren Configuration Manager geçerli dal sürümü 1802 ' den değiştirilmiştir. Daha fazla bilgi için bkz. [https için yönetim noktasını etkinleştirme](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a>Senaryo 2: Istemciden dağıtım noktasına

<!--1358228-->
Bir çalışma grubu veya Azure AD 'ye katılmış istemci, HTTP için yapılandırılmış bir dağıtım noktasından güvenli bir kanal üzerinden içerik doğrulayabilir ve indirebilir. Bu cihaz türleri, istemcide bir PKI sertifikası gerektirmeden, HTTPS için yapılandırılmış bir dağıtım noktasından içerik doğrulayabilir ve indirebilir. Bir çalışma grubuna veya Azure AD 'ye katılmış istemciye istemci kimlik doğrulama sertifikası eklemek zor olabilir.

Bu davranış, önyükleme medyasından, PXE 'den veya yazılım merkezi 'nden çalışan bir görev sırası ile işletim sistemi dağıtım senaryolarını içerir. Daha fazla bilgi için bkz. [ağ erişim hesabı](accounts.md#network-access-account).<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a>Senaryo 3: Azure AD cihaz kimliği

<!--1358460-->
Azure AD Kullanıcı oturumu olmayan bir Azure AD 'ye katılmış veya [hibrit Azure AD cihazı](/azure/active-directory/devices/concept-azure-ad-join-hybrid) , atanan sitesiyle güvenli bir şekilde iletişim kurabilir. Bulut tabanlı cihaz kimliği, artık cihaz merkezli senaryolar için CMG ve yönetim noktasıyla kimlik doğrulaması yapmak için yeterlidir. (Kullanıcı merkezli senaryolar için hala bir kullanıcı belirteci gereklidir.)  


## <a name="features"></a>Özellikler

Aşağıdaki Configuration Manager özellikleri, gelişmiş HTTP 'yi destekler veya gerektirir:

- [Bulut yönetimi ağ geçidi](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Ağ erişim hesabı olmayan işletim sistemi dağıtımı](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [İnternet tabanlı yeni Windows 10 cihazları için ortak yönetimi etkinleştirme](../../../comanage/tutorial-co-manage-new-devices.md)
- [E-posta aracılığıyla uygulama onayları](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Yönetim hizmeti](../../../develop/adminservice/overview.md)
- [Son bağlantılı konsolları görüntüle](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> Yazılım güncelleştirme noktası ve ilgili senaryolar, her zaman istemciler ve bulut yönetimi ağ geçidi ile güvenli HTTP trafiği de destekliyordu. Bu, yönetim noktası ile sertifika veya belirteç tabanlı kimlik doğrulamasından farklı bir mekanizma kullanır.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Önkoşullar  

- HTTP istemci bağlantıları için yapılandırılmış bir yönetim noktası. Yönetim noktası rol özelliklerinin **genel** sekmesinde bu seçeneği ayarlayın.  

- HTTP istemci bağlantıları için yapılandırılmış bir dağıtım noktası. Dağıtım noktası rol özelliklerinin **iletişim** sekmesinde bu seçeneği ayarlayın. **İstemcilerin anonim olarak bağlanmasına Izin verme**seçeneğini etkinleştirmeyin.  

- Siteyi, bulut yönetimi için Azure AD 'ye ekleyin.  

- *Yalnızca [Senaryo 3](#bkmk_scenario3) *: Windows 10 sürüm 1803 veya üstünü çalıştıran ve Azure AD 'ye katılmış bir istemci. İstemci, Azure AD cihaz kimlik doğrulaması için bu yapılandırmayı gerektirir.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Siteyi yapılandırma

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Siteyi seçin ve şeritte **Özellikler** ' i seçin.  

2. **Istemci bilgisayar iletişimi** sekmesine geçin.

    > [!Note]
    > Sürüm 1906 ' den başlayarak bu sekmeye **Iletişim güvenliği**denir.<!-- SCCMDocs#1645 -->  

    **Https veya http**seçeneğini belirleyin. Ardından, **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanma**seçeneğini etkinleştirin.

> [!Tip]
> Yönetim noktasının siteden yeni sertifikayı alması ve yapılandırması için 30 dakikaya kadar bekleyin.

<!--3798957-->
Sürüm 1902 ' den başlayarak, merkezi yönetim sitesi için gelişmiş HTTP 'yi de etkinleştirebilirsiniz. Aynı işlemi kullanın ve merkezi yönetim sitesinin özelliklerini açın. Bu eylem, merkezi yönetim sitesindeki SMS sağlayıcısı rolleri için yalnızca gelişmiş HTTP 'yi sunar. Hiyerarşideki tüm siteler için geçerli olan genel bir ayar değildir.

Bu sertifikaları Configuration Manager konsolunda görebilirsiniz. **Yönetim** çalışma alanına gidin, **güvenlik**' i genişletin ve **Sertifikalar** düğümünü seçin. SMS **veren kök sertifikayı** ve SMS veren kök tarafından verilen site sunucusu rolü sertifikalarını bulun.

İstemcinin yönetim noktası ve dağıtım noktasıyla Bu yapılandırmayla nasıl iletişim kurduğu hakkında daha fazla bilgi için bkz. [istemcilerden site sistemlerine ve hizmetlere yönelik iletişimler](communications-between-endpoints.md#Planning_Client_to_Site_System).


## <a name="see-also"></a>Ayrıca bkz.

- [Güvenliği planlama](../security/plan-for-security.md)  

- [Configuration Manager istemcileri için güvenlik ve Gizlilik](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Güvenliği yapılandırma](../security/configure-security.md)  

- [Uç noktalar arasında iletişim](communications-between-endpoints.md)  
