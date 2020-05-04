---
title: İstemciyi Azure AD 'ye yüklemeyin
titleSuffix: Configuration Manager
description: Kimlik doğrulaması için Azure Active Directory kullanarak Windows 10 cihazlarına Configuration Manager istemcisini yükleyip atama
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a55440e7ba61ec62d9f0c91c0a23b98bab5884c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713502"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Kimlik doğrulaması için Azure AD 'yi kullanarak Configuration Manager Windows 10 istemcileri yükleyip atama

Configuration Manager istemcisini Azure AD kimlik doğrulaması kullanarak Windows 10 cihazlarına yüklemek için, Configuration Manager Azure Active Directory (Azure AD) ile tümleştirin. İstemciler, HTTPS özellikli bir yönetim noktasıyla doğrudan iletişim kuran intranette veya gelişmiş HTTP için etkinleştirilmiş bir sitedeki herhangi bir yönetim noktasıyla iletişim kurmak olabilir. Ayrıca, CMG aracılığıyla veya Internet tabanlı bir yönetim noktasıyla internet tabanlı iletişim olabilir. Bu işlem, Configuration Manager sitesinde istemcilerin kimliğini doğrulamak için Azure AD kullanır. Azure AD, istemci kimlik doğrulama sertifikalarını yapılandırma ve kullanma gereksinimininin yerini almaktadır.

Azure AD 'nin kurulması, bazı müşterilerin sertifika tabanlı kimlik doğrulaması için ortak anahtar altyapısı ayarlamaktan daha kolay olabilir. Siteyi Azure AD 'ye eklemenize gerek kalmaz, ancak istemcilerin Azure AD 'ye katılmış olması gerekmez.<!-- SCCMDocs issue 1259 --> Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Azure Active Directory için plan yapın](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [Ortak yönetim için Azure AD kullanma](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>Başlamadan önce

- Bir Azure AD kiracısı bir önkoşuldur  

- Cihaz gereksinimleri:  

  - Windows 10  

  - Saf bulut etki alanına katılmış ya da karma Azure AD 'ye katılmış Azure AD 'ye katılmış  

- Kullanıcı gereksinimleri:  

  - Oturum açan kullanıcının bir Azure AD kimliği olması gerekir.

  - Kullanıcı federe veya eşitlenmiş bir kimlik ise, Configuration Manager [Active Directory Kullanıcı keşfi](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) ve [Azure AD Kullanıcı keşfi](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)' ni kullanmanız gerekir. Karma kimlikler hakkında daha fazla bilgi için bkz. [karma kimlik benimseme stratejisi tanımlama](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Yönetim noktası site sistemi rolü için [mevcut önkoşullara](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq) ek olarak, bu sunucuda **ASP.NET 4,5** de etkinleştirin. ASP.NET 4,5 etkinleştirilirken otomatik olarak seçilen diğer seçenekleri dahil edin.  

- Yönetim noktanağınızın HTTPS 'ye ihtiyacı olup olmadığını belirleme. Daha fazla bilgi için bkz. [https için yönetim noktasını etkinleştirme](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

- İsteğe bağlı olarak, Internet tabanlı istemcileri dağıtmak için bir [bulut yönetimi ağ geçidi](../manage/cmg/plan-cloud-management-gateway.md) (CMG) ayarlayın. Azure AD ile kimlik doğrulaması yapan şirket içi istemciler için CMG 'ye ihtiyacınız yoktur.  

> [!TIP]
> Sürüm 2002 ' den başlayarak,<!--5686290--> Configuration Manager, genellikle iç ağa bağlanmayan, Azure Active Directory (Azure AD) katılamaz ve PKI tarafından verilen bir sertifika yüklemek için bir yönteme sahip olmayan Internet tabanlı cihazlara yönelik desteğini uzatır. Daha fazla bilgi için bkz. [CMG Için belirteç tabanlı kimlik doğrulaması](deploy-clients-cmg-token.md).

## <a name="configure-azure-services-for-cloud-management"></a>Azure hizmetlerini bulut yönetimi için yapılandırma

Configuration Manager sitenizi ilk adım olarak Azure AD 'ye bağlayın. Bu işlemin ayrıntıları için bkz. [Azure hizmetlerini yapılandırma](../../servers/deploy/configure/azure-services-wizard.md). **Bulut yönetimi** hizmetine bir bağlantı oluşturun.

**Bulut yönetimine**ekleme Işlemi KAPSAMıNDA [Azure AD Kullanıcı keşfi](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) 'ni etkinleştirin.

Bu eylemleri tamamladıktan sonra Configuration Manager siteniz Azure AD 'ye bağlanır.

## <a name="configure-client-settings"></a>İstemci ayarlarını yapılandırma

Bu istemci ayarları, Windows 10 cihazlarının Azure AD ile katılılabilmesi için yardımcı olur. Ayrıca, Internet tabanlı istemcilerin CMG ve bulut dağıtım noktasını kullanmasına de olanak tanır.

1. [İstemci ayarlarını yapılandırma](configure-client-settings.md)bölümündeki bilgileri kullanarak **Cloud Services** bölümünde aşağıdaki istemci ayarlarını yapılandırın.  

    - **Bulut dağıtım noktasına erişime Izin ver**: Internet tabanlı cihazların Configuration Manager istemcisini yüklemek için gerekli içeriği almasını sağlamak için bu ayarı etkinleştirin. İçerik, bulut dağıtım noktasında yoksa, cihazlar CMG 'den içeriği alabilir. İstemci yükleme önyüklemesi, CMG 'ye geri dönmek için bulut dağıtım noktasını dört saat boyunca yeniden dener.<!--495533-->  

    - **Azure Active Directory ile yeni Windows 10 etki alanına katılmış cihazları otomatik olarak kaydet**: **Evet** veya **Hayır**olarak ayarlayın. Varsayılan ayar **Evet**' tir. Bu davranış, Windows 10, sürüm 1709 ' de de varsayılandır.

    - **İstemcilerin bulut yönetimi ağ geçidi kullanmasını etkinleştir**: **Evet** (varsayılan) veya **Hayır**olarak ayarlayın.  

2. İstemci ayarlarını gerekli cihaz koleksiyonuna dağıtın. Bu ayarları kullanıcı koleksiyonlarına dağıtmayın.

Cihazın Azure AD 'ye katıldığını doğrulamak için bir komut isteminde çalıştırın `dsregcmd.exe /status` . Sonuçlarda **Azureadkatılmış** alanı, CIHAZıN Azure AD 'ye katılmış olması halinde **Evet 'i** gösterir.

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Azure AD kimlik kullanarak istemciyi yükleyip kaydetme

Azure AD kimlik kullanarak istemciyi el ile yüklemek için, önce [Istemcileri nasıl el ile yükleyeceğiniz](deploy-clients-to-windows-computers.md#BKMK_Manual)hakkında genel işlemi gözden geçirin.

 > [!Note]  
 > Cihazın Azure AD 'ye başvurması için internet 'e erişmesi gerekir, ancak internet tabanlı olması gerekmez.

Aşağıdaki örnek, komut satırının genel yapısını gösterir:`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Daha fazla bilgi için bkz. [istemci yükleme özellikleri](about-client-installation-properties.md).

**/MP** parametresi ve **CCMHOSTNAME** özelliği, senaryoya bağlı olarak aşağıdakilerden birini belirtir:

- Şirket içi yönetim noktası. Yalnızca **/MP** parametresini belirtin. **CCMHOSTNAME** özelliği gerekli değildir.
- Bulut yönetimi ağ geçidi
- Internet tabanlı yönetim noktası

**SMSMP** özelliği, şirket içi ya da internet tabanlı yönetim noktasını belirtir.

Bu örnek, bir bulut yönetimi ağ geçidi kullanır. Örnek değerleri yerine koyar:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Site, bulut yönetimi ağ geçidine (CMG) ek Azure AD bilgileri yayımlar. Azure AD 'ye katılmış bir istemci, bu bilgileri Ccmsetup işlemi sırasında, katıldığı aynı kiracıyı kullanarak CMG 'den alır. Bu davranış, istemcinin birden fazla Azure AD kiracısı olan bir ortama yüklenmesini kolaylaştırır. Yalnızca iki zorunlu CCMSetup özelliği **CCMHOSTNAME** ve **smssitekodu**.<!--3607731-->

Azure AD kimlik kullanarak istemci yüklemesini Microsoft Intune aracılığıyla otomatik hale getirmek için bkz. [İnternet tabanlı cihazları ortak yönetim için hazırlama](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

## <a name="next-steps"></a>Sonraki adımlar

Tamamlandıktan sonra, [istemcileri izlemeye ve yönetmeye](../manage/monitor-clients.md)devam edebilirsiniz.
