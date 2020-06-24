---
title: CMG SSS
titleSuffix: Configuration Manager
description: Bulut yönetimi ağ geçidi ile ilgili sık sorulan soruları yanıtlamak için bu makaleyi kullanın
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: bd846b0155a0baddad76d6027ffbd239d7dbf26f
ms.sourcegitcommit: 5f15a3abf33ce7bfd6855ffeef2ec3cd4cd48a7f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721899"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi hakkında sık sorulan sorular

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, bulut yönetimi ağ geçidi hakkında sık sorulan sorularınızı yanıtlar. Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidini planlayın](plan-cloud-management-gateway.md).

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

### <a name="what-certificates-do-i-need"></a>Hangi sertifikalara ihtiyacım var?

Daha ayrıntılı bilgi için bkz. [bulut yönetimi ağ geçidi için sertifikalar](certificates-for-cloud-management-gateway.md).

### <a name="do-i-need-azure-expressroute"></a>Azure ExpressRoute 'a ihtiyacım var mı?

Hayır. [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) , şirket Içi ağınızı Microsoft bulutuna genişletmenizi sağlar. ExpressRoute veya bu tür sanal ağ bağlantıları Configuration Manager bulut yönetimi ağ geçidi için gerekli değildir. Bulut yönetimi ağ geçidinin tasarımı, internet tabanlı istemcilerin Azure hizmetinden şirket içi site sistemlerine ek ağ yapılandırması olmadan iletişim kurmasına olanak tanır. Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidini planlayın](plan-cloud-management-gateway.md)

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Azure sanal makinelerini sürdürmem gerekir mi?

Bakım gerekli değildir. Bulut yönetimi ağ geçidinin tasarımı bir hizmet olarak Azure platformu (PaaS) kullanır. Sağladığınız aboneliği kullanarak, Configuration Manager gerekli sanal makineleri (VM 'Ler), depolamayı ve ağı oluşturur. Azure, sanal makinenin güvenliğini sağlar ve güncelleştirir. Bu VM 'Ler, hizmet olarak altyapı (IaaS) gibi durumlarda şirket içi ortamınızın bir parçası değildir. Bulut yönetimi ağ geçidi, Configuration Manager ortamınızı buluta genişleten bir PaaS 'dir. Daha fazla bilgi için bkz. [PaaS dağıtımlarını güvenli hale getirme](/azure/security/security-paas-deployments).

### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Hizmet güncelleştirmeleri sırasında hizmet devamlılığını nasıl güvence altına alabilirim?

CMG 'yi iki veya daha fazla örnek içerecek şekilde ölçeklendirerek, Azure 'daki güncelleştirme etki alanlarından otomatik olarak yararlanabilirsiniz. Bkz. [bulut hizmetini güncelleştirme](/azure/cloud-services/cloud-services-update-azure-service).

### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Zaten IBCM kullanıyorum. CMG 'yi eksem istemciler nasıl davranır?

Zaten [Internet tabanlı istemci yönetimini](../plan-internet-based-client-management.md) (ibcm) dağıttıysanız, bulut yönetimi ağ geçidini de dağıtabilirsiniz. İstemciler her iki hizmet için de ilke alır. İnternet üzerinde dolaşırken, bu internet tabanlı hizmetlerden birini rastgele seçip kullanın.

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a>Kullanıcı hesaplarının CMG bulut hizmetini barındıran abonelikle ilişkili kiracı ile aynı Azure AD kiracısında olması gerekir mi?
<!--SCCMDocs-pr issue #2873-->
Hayır, CMG 'yi Azure bulut hizmetleri 'ni barındırabilmeniz gereken herhangi bir aboneliğe dağıtabilirsiniz.

Koşulları açıklığa kavuşturmak için:

- _Kiracı_ , Kullanıcı hesaplarının ve uygulama kayıtlarının dizinidir. Bir kiracının birden çok aboneliği olabilir.
- _Abonelik_ , kaynakları ve hizmetleri birbirinden ayırır. Tek bir kiracı ile ilişkilendirilir.

Bu soru, aşağıdaki senaryolarda ortaktır:  

- Farklı test ve üretim Active Directory ve Azure AD ortamlarınız, ancak tek bir merkezi Azure barındırma aboneliğiniz olduğunda.

- Azure kullanımı, farklı ekipler genelinde dağıtılır

Kaynak Yöneticisi dağıtımı kullanırken, abonelikle ilişkili Azure AD kiracısını ekleyin. Bu bağlantı, Configuration Manager CMG oluşturmak, dağıtmak ve yönetmek için Azure 'da kimlik doğrulamasına olanak tanır.  

CMG üzerinden yönetilen kullanıcılar ve cihazlar için Azure AD kimlik doğrulaması kullanıyorsanız, bu Azure AD kiracısını ekleyin. Bulut yönetimi için Azure hizmetleri hakkında daha fazla bilgi için bkz. [Azure hizmetlerini yapılandırma](../../../servers/deploy/configure/azure-services-wizard.md). Her bir Azure AD kiracısını eklediğinizde, tek bir CMG, barındırma konumundan bağımsız olarak birden çok kiracı için Azure AD kimlik doğrulaması sağlayabilir.

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>Örnek 1: birden çok aboneliğe sahip bir kiracı

Kullanıcı kimlikleri, cihaz kayıtları ve uygulama kayıtları aynı kiracıda bulunur. CMG 'nin hangi abonelikte kullanacağını seçebilirsiniz. Birden çok CMG hizmetini bir siteden ayrı aboneliklere dağıtabilirsiniz. Sitenin kiracı ile bire bir ilişkisi vardır. Faturalandırma veya mantıksal ayırma gibi çeşitli nedenlerle hangi aboneliklerin kullanılacağına karar verirsiniz.

#### <a name="example-2-multiple-tenants"></a>Örnek 2: birden çok kiracı

Diğer bir deyişle, ortamınızda birden çok Azure AD vardır. Her iki kiracıda Kullanıcı ve cihaz kimliklerini desteklemeniz gerekiyorsa, siteyi her kiracıya bağlamanız gerekir. Bu işlem, bu Kiracıdaki uygulama kayıtlarını oluşturmak için her kiracıdan bir yönetim hesabı gerektirir. Bir site daha sonra CMG hizmetlerini birden fazla kiracıda barındırabilir. Kiracıda herhangi bir kullanılabilir abonelikte CMG oluşturabilirsiniz. Azure AD 'ye katılmış veya karma cihazlar bir CMG kullanabilir.

Kullanıcı ve cihaz kimlikleri tek bir kiracıda ise, ancak CMG 'nin aboneliği başka bir kiracıda varsa, siteyi her iki kiracıya bağlamanız gerekir. Teknik olarak, istemci uygulaması yalnızca CMG hizmetine sahip ikinci kiracı için gerekli değildir. İstemci uygulaması yalnızca CMG hizmetini kullanan istemciler için Kullanıcı ve cihaz kimlik doğrulaması sağlar.<!-- SCCMDocs#1902 -->

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>CMG, istemcilerimin VPN üzerinden bağlı olduğunu nasıl etkiler?

Ortamınıza VPN aracılığıyla bağlanan gezici istemciler genellikle intranet 'e yönelik olarak algılanır. Yönetim noktaları ve dağıtım noktaları gibi şirket içi altyapınızla bağlantı kurmayı dener. Bazı müşteriler, VPN aracılığıyla bağlandığında bile bulut Hizmetleri tarafından yönetilen bu gezici istemcileri kullanmayı tercih eder. Sürüm 1902 ' den başlayarak CMG 'yi bir sınır grubuyla ilişkilendirin. Bu eylem, bu istemcileri şirket içi site sistemlerini kullanmamaya zorlar. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](setup-cloud-management-gateway.md#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Bir CMG 'yi etkinleştirdiğimde, İstemcilerim yalnızca intranete bağlandığında CMG etkin yönetim noktasına bağlanır mi?

Bir CMG üzerinden gönderilen hassas trafiğin güvenliğini sağlamak için bir HTTPS yönetim noktası yapılandırın veya geliştirilmiş HTTP kullanın.

Bir CMG dağıtmayı tercih ederseniz ve CMG etkin yönetim noktasında HTTPS iletişimi için PKI sertifikaları kullanıyorsanız, yönetim noktası özelliklerindeki **yalnızca İnternet Istemcilerine Izin verme** seçeneğini belirleyin. Bu ayar, iç istemcilerin ortamınızda HTTP yönetim noktalarını kullanmaya devam etmelerini sağlar.

Gelişmiş HTTP kullanıyorsanız, bu ayarı yapılandırmanız gerekmez. İstemciler, doğrudan CMG etkin yönetim noktasıyla iletişim kurarken HTTP kullanmaya devam eder. Daha fazla bilgi için bkz. [GELIŞMIŞ http](../../../plan-design/hierarchy/enhanced-http.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Bulut yönetimi ağ geçidi planlama](plan-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidini kurma](setup-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidine yönelik sertifikalar](certificates-for-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidi için güvenlik ve gizlilik](security-and-privacy-for-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidi boyutu ve ölçek numaraları](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
