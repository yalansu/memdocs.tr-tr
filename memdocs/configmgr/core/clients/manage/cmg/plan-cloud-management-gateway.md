---
title: Bulut yönetimi ağ geçidi planlama
titleSuffix: Configuration Manager
description: Internet tabanlı istemcilerin yönetimini basitleştirmek için bulut yönetimi ağ geçidini (CMG) planlayın ve tasarlayın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7c57e6568ce60680d9febc533c60533055595bc3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126942"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Configuration Manager 'de bulut yönetimi ağ geçidini planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1101764-->
Bulut yönetimi ağ geçidi (CMG), internet 'teki Configuration Manager istemcilerini yönetmek için basit bir yol sağlar. CMG 'yi Microsoft Azure bir bulut hizmeti olarak dağıtarak, internet üzerinde dolaşan geleneksel istemcileri ek şirket içi altyapı olmadan yönetebilirsiniz. Ayrıca, şirket içi altyapınızı Internet 'e sunmanıza gerek kalmaz.

> [!NOTE]
> Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Önkoşulları kurduktan sonra, CMG oluşturma Configuration Manager konsolunda aşağıdaki üç adımdan oluşur:

1. CMG bulut hizmetini Azure 'a dağıtın.
2. CMG bağlantı noktası rolünü ekleyin.
3. Hizmet için site ve Site rollerini yapılandırın.
Dağıtıldıktan ve yapılandırıldıktan sonra istemciler intranet veya Internet üzerinde olup olmadıklarına bakılmaksızın şirket içi site rollerine sorunsuz şekilde erişir.

Bu makalede, CMG hakkında bilgi edinmek, ortamınıza uygun olanı tasarlamak ve uygulamayı planlamak için temel bilgiler sağlanmaktadır.

## <a name="scenarios"></a>Senaryolar

CMG 'nin faydalı olduğu birkaç senaryo vardır. Aşağıdaki senaryolar daha yaygın olarak verilmiştir:  

- Active Directory etki alanına katılmış kimlik ile geleneksel Windows istemcilerini yönetin. Bu istemciler Windows 8.1 ve Windows 10 ' a dahildir. İletişim kanalını güvenli hale getirmek için PKI sertifikaları kullanır. Yönetim etkinlikleri şunları içerir:  

  - Yazılım güncelleştirmeleri ve Endpoint Protection
  - Envanter ve istemci durumu
  - Uyumluluk ayarları
  - Cihaza yazılım dağıtımı
  - Windows 10 yerinde yükseltme görev dizisi

- Azure Active Directory (Azure AD) ile Birleşik veya saf bulut etki alanına katılmış modern kimlik ile geleneksel Windows 10 istemcilerini yönetin. İstemciler, PKI sertifikaları yerine kimlik doğrulaması yapmak için Azure AD kullanır. Azure AD 'nin kullanılması daha basit PKI sistemlerini kurmak, yapılandırmak ve sürdürmek için daha basittir. Yönetim etkinlikleri, ilk senaryoyla aynı zamanda ve:  

  - Kullanıcıya yazılım dağıtımı  

- Configuration Manager istemcisini Internet üzerinden Windows 10 cihazlarına yükler. Azure AD 'nin kullanılması, cihazın istemci kaydı ve ataması için CMG 'ye kimlik doğrulaması yapmasına olanak sağlar. İstemciyi el ile veya Microsoft Intune gibi başka bir yazılım dağıtım yöntemi kullanarak yükleyebilirsiniz.  

- Ortak yönetim ile yeni cihaz sağlama. Mevcut istemcileri otomatik olarak kaydederken ortak yönetim için CMG gerekli değildir. Windows Autopilot, Azure AD, Microsoft Intune ve Configuration Manager içeren yeni cihazlar için gereklidir. Daha fazla bilgi için bkz. [ortak yönetime yönelik yollar](../../../../comanage/quickstart-paths.md).

### <a name="specific-use-cases"></a>Belirli kullanım örnekleri

Bu senaryolarda, aşağıdaki belirli cihaz kullanım örnekleri uygulanabilir:

- Dizüstü bilgisayarlar gibi dolaşım cihazları  

- İnternet üzerinden bir WAN veya VPN üzerinden yönetilmesi daha pahalı ve daha verimli olan uzak/şube ofisi cihazları.  

- Birleşmeler ve alımlar, cihazları Azure AD 'ye katmak ve CMG aracılığıyla yönetmek en kolay olabilir.  

- Çalışma grubu istemcileri. Bu cihazlar, sertifikalar gibi ek yapılandırma gerektirebilir.<!-- SCCMDocs#1925 -->

    Sürüm 2002 ' den başlayarak Configuration Manager, uzak çalışma grubu istemcilerinin yönetimine yardımcı olabilecek belirteç tabanlı kimlik doğrulamasını destekler. Daha fazla bilgi için bkz. [CMG Için belirteç tabanlı kimlik doğrulaması](../../deploy/deploy-clients-cmg-token.md).

> [!Important]
> Varsayılan olarak, tüm istemciler bir CMG için ilke alır ve internet tabanlı olduklarında kullanmaya başlar. Kuruluşunuz için geçerli olan senaryoya ve kullanım örneğine bağlı olarak, CMG 'nin kullanım kapsamını belirlemeniz gerekebilir. Daha fazla bilgi için bkz. [istemcileri bir bulut yönetimi ağ geçidi istemci ayarını kullanacak şekilde etkinleştirme](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway) .

## <a name="topology-design"></a>Topoloji tasarımı

### <a name="cmg-components"></a>CMG bileşenleri

CMG 'nin dağıtımı ve işlemi aşağıdaki bileşenleri içerir:  

- Azure 'daki **CMG bulut hizmeti** kimlik doğrulaması yapar ve Configuration Manager istemci isteklerini CMG bağlantı noktasına iletir.  

- **CMG bağlantı noktası** site sistemi rolü, şirket Içi ağdan Azure 'daki CMG hizmetine tutarlı ve yüksek performanslı bir bağlantı sağlar. Ayrıca, bağlantı bilgileri ve güvenlik ayarları dahil olmak üzere CMG 'ye ayarları yayımlar. CMG bağlantı noktası, istemci isteklerini, URL eşlemelerine göre CMG 'den şirket içi rollere iletir.

- [**Hizmet bağlantı noktası**](../../../servers/deploy/configure/about-the-service-connection-point.md) site sistemi rolü, tüm CMG dağıtım görevlerini işleyen Cloud Service Manager bileşenini çalıştırır. Ayrıca, Azure AD 'den hizmet durumu ve günlüğe kaydetme bilgilerini izler ve raporlar. Hizmet bağlantı noktanız [çevrimiçi modda](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)olduğundan emin olun.  

- **Yönetim noktası** site sistemi Rol Hizmetleri istemci isteklerini normal başına ister.

- **Yazılım güncelleştirme noktası** site sistemi Rol Hizmetleri istemci isteklerini normal başına ister.

    > [!NOTE]
    > Yönetim noktaları ve yazılım güncelleştirme noktaları için boyutlandırma Kılavuzu, şirket içi veya internet tabanlı istemcilere hizmet verip etmeyeceklerini değiştirmez. Daha fazla bilgi için bkz. [boyut ve ölçek numaraları](../../../plan-design/configs/size-and-scale-numbers.md#management-point).

- **Internet tabanlı istemciler** , CMG 'ye bağlanarak şirket içi Configuration Manager bileşenlerine erişir.

- CMG, istemcilerle ağ iletişimine güvenli hale getirmek için **sertifika tabanlı BIR https** Web hizmeti kullanır.  

- Internet tabanlı istemciler, kimlik ve kimlik doğrulaması için **PKI sertifikaları veya Azure AD** kullanır.  

- [**Bulut dağıtım noktası**](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) gerektiğinde internet tabanlı istemcilere içerik sağlar.  

  - Bir CMG, istemcilere içerik de sunabilir. Bu işlevsellik, Azure VM 'lerinin gerekli sertifikalarını ve maliyetini azaltır. Daha fazla bilgi için bkz. [CMG 'Yi değiştirme](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
**Azure Resource Manager dağıtımı**kullanarak CMG 'yi oluşturun. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) , tüm çözüm kaynaklarının, [kaynak grubu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)olarak adlandırılan tek bir varlık olarak yönetilmesine yönelik modern bir platformdur. Azure Resource Manager ile CMG 'yi dağıttığınızda, site kimlik doğrulaması yapmak ve gerekli bulut kaynaklarını oluşturmak için Azure Active Directory (Azure AD) kullanır. Bu modernlanmış dağıtım, klasik Azure Yönetim sertifikası gerektirmez.  

> [!NOTE]
> Bu özellik, Azure bulut hizmeti sağlayıcıları (CSP) için desteği etkinleştirmez. Azure Resource Manager ile CMG dağıtımı, CSP 'nin desteklemediği klasik bulut hizmetini kullanmaya devam eder. Daha fazla bilgi için bkz. [Azure CSP 'de kullanılabilir Azure hizmetleri](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).

Configuration Manager sürüm 1902 ' den başlayarak, bulut yönetimi ağ geçidinin yeni örnekleri için tek dağıtım mekanizmasıdır Azure Resource Manager. Mevcut dağıtımlar çalışmaya devam eder.<!-- 3605704 -->

Configuration Manager sürüm 1810 ve önceki sürümlerde CMG Sihirbazı yine de Azure Yönetim sertifikası kullanan **Klasik hizmet dağıtımı** için seçenek sağlar. Kaynakların dağıtımını ve yönetimini basitleştirmek için, tüm yeni CMG örnekleri için Azure Resource Manager dağıtım modeli önerilir. Mümkünse, var olan CMG örneklerini Kaynak Yöneticisi aracılığıyla yeniden dağıtın. Daha fazla bilgi için bkz. [CMG 'Yi değiştirme](setup-cloud-management-gateway.md#modify-a-cmg).

> [!IMPORTANT]
> Azure 'daki klasik hizmet dağıtımı Configuration Manager kullanımı için kullanım dışıdır. Sürüm 1810, bu Azure dağıtımlarını oluşturmayı desteklemeye yönelik son bir sürümdür. Bu işlev gelecekteki bir Configuration Manager sürümünde kaldırılacak.<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>Hiyerarşi tasarımı

Hiyerarşinizin üst katman sitesinde CMG 'yi oluşturun. Bu bir merkezi yönetim sitesi ise alt birincil sitelerde CMG bağlantı noktaları oluşturun. Bulut Service Manager bileşeni, merkezi yönetim sitesinde de olan hizmet bağlantı noktasıdır. Bu tasarım, gerekirse farklı birincil sitelerde hizmeti paylaşabilir.

Azure 'da birden çok CMG hizmeti oluşturabilir ve birden çok CMG bağlantı noktası oluşturabilirsiniz. Birden çok CMG bağlantı noktası, CMG 'den şirket içi rollere istemci trafiği yük dengelemesi sağlar.

Sürüm 1902 ' den başlayarak bir CMG 'yi bir sınır grubuyla ilişkilendirebilirsiniz. Bu yapılandırma, istemcilerin [sınır grubu ilişkilerine](../../../servers/deploy/configure/boundary-groups.md)göre istemci iletişimi için varsayılan veya CMG 'ye geri dönüş yapmasına izin verir. Bu davranış özellikle şube ofisi ve VPN senaryolarında yararlı olur. İstemci trafiğini pahalı ve yavaş WAN bağlantılarından, bunun yerine Microsoft Azure ' de daha hızlı bir şekilde kullanabilirsiniz.<!--3640932-->

Sürüm 2006 ' den başlayarak, intranet istemcileri bir sınır grubuna atandığında bir CMG yazılım güncelleştirme noktasına erişebilir. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup). <!--7102873-->

> [!NOTE]
> Internet tabanlı istemciler herhangi bir sınır grubuna düşmez.
>
> Configuration Manager sürüm 1810 ve önceki sürümlerde CMG hiçbir sınır grubuna düşmez.

Yönetilecek istemci sayısı gibi diğer faktörler de CMG tasarımınızı etkiler. Daha fazla bilgi için bkz. [performans ve ölçek](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Örnek 1: tek başına birincil site

Contoso, bir şirket içi veri merkezinde yeni York şehrinde yer alan bir tek başına birincil siteye sahiptir.

- Ağ gecikmesini azaltmak için Doğu ABD Azure bölgesinde bir CMG oluşturamazlar.
- Her ikisi de tek CMG hizmetiyle bağlantılı iki CMG bağlantı noktası oluşturur.  

İstemciler İnternet üzerinde dolaşırken, Doğu ABD Azure bölgesindeki CMG ile iletişim kurar. CMG bu iletişimi CMG bağlantı noktaları üzerinden iletir.

#### <a name="example-2-hierarchy"></a>Örnek 2: hiyerarşi

Dördüncü kahve, bir şirket içi veri merkezinde Seattle 'daki merkezi yönetim sitesine sahiptir. Bir birincil site aynı veri merkezinde ve diğer birincil site ise Paris 'teki ana Avrupa ofisinde.

- Merkezi yönetim sitesinde, Azure bölgesinde Batı ABD bir CMG hizmeti oluşturamazlar. Tüm hiyerarşideki beklenen dolaşım istemcileri yükünün VM sayısını ölçeklendirecektir.
- Seattle tabanlı birincil sitede, tek CMG 'ye bağlı bir CMG bağlantı noktası oluşturamazlar.
- Paris tabanlı birincil sitede, tek CMG 'ye bağlı bir CMG bağlantı noktası oluşturamazlar.

İstemciler İnternet üzerinde dolaşırken, Batı ABD Azure bölgesindeki CMG ile iletişim kurar. CMG bu iletişimi istemcinin atanan birincil sitesindeki CMG bağlantı noktasına iletir.

> [!TIP]
> Coğrafi konum amacıyla birden fazla bulut yönetim ağ geçidi dağıtmanız gerekmez. Configuration Manager istemci, coğrafi olarak uzak zaman bile, bulut hizmeti ile oluşabilen hafif gecikme süresinden daha etkilenmemiştir.

### <a name="test-environments"></a>Test ortamları
<!-- SCCMDocs#1225 -->
Birçok kuruluşun üretim, test, geliştirme veya kalite güvencesi için ayrı ortamları vardır. CMG dağıtımınızı planlarken, aşağıdaki soruları göz önünde bulundurun:

- Kuruluşunuz kaç Azure AD kiracısın?
  - Test için ayrı bir kiracı var mı?
  - Kullanıcı ve cihaz kimlikleri aynı kiracıda mı?

- Her kiracıda kaç abonelik var?
  - Test için özel abonelikler var mı?

**Bulut yönetimi** için Azure hizmeti Configuration Manager birden çok kiracıyı destekler. Birden çok Configuration Manager site aynı kiracıya bağlanabilir. Tek bir site, farklı aboneliklerde birden çok CMG hizmetini dağıtabilir. Birden çok site CMG hizmetlerini aynı aboneliğe dağıtabilir. Configuration Manager ortamınıza ve iş gereksinimlerinize bağlı olarak esneklik sağlar.

Daha fazla bilgi için aşağıdaki SSS bölümüne bakın: [Kullanıcı hesaplarının CMG bulut hizmetini barındıran abonelikle ilişkili kiracı ile aynı Azure AD kiracısında olması gerekir mi?](cloud-management-gateway-faq.md#bkmk_tenant)

## <a name="requirements"></a>Gereksinimler

- CMG 'yi barındırmak için bir **Azure aboneliği** .

    > [!IMPORTANT]
    > CMG, bir Azure bulut hizmeti sağlayıcısı (CSP) ile abonelikleri desteklemez.<!-- MEMDocs#320 -->

- Kullanıcı hesabınızın Configuration Manager bir **tam yönetici** veya **Altyapı Yöneticisi** olması gerekir.<!-- SCCMDocs#2146 -->

- Bir **Azure yöneticisinin** , tasarımınıza bağlı olarak belirli bileşenlerin ilk oluşturmaya katılması gerekir. Bu kişi, Configuration Manager yöneticisiyle aynı veya ayrı olabilir. Ayrı ise, Configuration Manager izin gerektirmez.

  - CMG 'yi dağıtmak için **abonelik sahibine** ihtiyacınız vardır
  - Siteyi Azure Resource Manager kullanarak CMG dağıtmaya yönelik Azure AD ile tümleştirmek için **genel yönetici** gerekir

- **CMG bağlantı noktasını**barındırmak için en az bir şirket içi Windows Server. Bu rolü diğer Configuration Manager site sistem rolleriyle birlikte kullanabilirsiniz.  

- **Hizmet bağlantı noktası** [çevrimiçi modda](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)olmalıdır.  

- Hizmeti Azure Resource Manager ile dağıtmak için **Azure AD** ile tümleştirme. Daha fazla bilgi için bkz. [Azure hizmetlerini yapılandırma](../../../servers/deploy/configure/azure-services-wizard.md).  

- CMG için bir [**sunucu kimlik doğrulama sertifikası**](certificates-for-cloud-management-gateway.md#bkmk_serverauth) .  

- İstemci işletim sistemi sürümüne ve kimlik doğrulama modelinize bağlı olarak **diğer sertifikalar** gerekli olabilir. Daha fazla bilgi için bkz. [CMG sertifikaları](certificates-for-cloud-management-gateway.md).  

    **Http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanmak**üzere site seçeneğini kullandığınızda, YÖNETIM noktası http olabilir. Daha fazla bilgi için bkz. [GELIŞMIŞ http](../../../plan-design/hierarchy/enhanced-http.md).

- Configuration Manager sürüm 1810 veya önceki sürümlerde, Azure klasik dağıtım yöntemi kullanılıyorsa bir [**Azure Yönetim sertifikası**](certificates-for-cloud-management-gateway.md#bkmk_azuremgmt)kullanmanız gerekir.  

    > [!TIP]  
    > **Azure Resource Manager** dağıtım modelini kullanın. Bu yönetim sertifikası gerekmez.
    >
    > Klasik dağıtım yöntemi 1810 sürümünden itibaren kullanımdan kaldırılmıştır.  

- İstemcilerin **IPv4**kullanması gerekir.  

## <a name="specifications"></a>Belirtimler

- [İstemciler ve cihazlar Için desteklenen işletim sistemlerinde](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) listelenen tüm Windows sürümleri CMG için desteklenir.  

- CMG yalnızca yönetim noktası ve yazılım güncelleştirme noktası rollerini destekler.  

- CMG, yalnızca IPv6 adresleriyle iletişim kuran istemcileri desteklemez.<!--495606-->  

- Ağ Yük dengeleyici kullanan yazılım güncelleştirme noktaları CMG ile çalışmaz. <!--505311-->  

- Azure kaynak modeli kullanılarak gerçekleştirilen CMG dağıtımları, Azure bulut hizmeti sağlayıcıları (CSP) için desteği etkinleştirmez. Azure Resource Manager ile CMG dağıtımı, CSP 'nin desteklemediği klasik bulut hizmetini kullanmaya devam eder. Daha fazla bilgi için bkz. [Azure CSP programında bulunan Azure hizmetleri](https://docs.microsoft.com/partner-center/azure-plan-available).

### <a name="support-for-configuration-manager-features"></a>Configuration Manager özellikleri için destek

Aşağıdaki tabloda Configuration Manager özellikleri için CMG desteği listelenmektedir:

|Özellik  |Destek  |
|---------|---------|
| Yazılım güncelleştirmeleri     | ![Desteklenir](media/green_check.png) |
| Endpoint protection     | ![Desteklenen ](media/green_check.png) <sup> [notta &nbsp; 1](#bkmk_note1)</sup> |
| Donanım ve yazılım envanteri     | ![Desteklenir](media/green_check.png) |
| İstemci durumu ve bildirimleri     | ![Desteklenir](media/green_check.png) |
| Betikleri Çalıştır     | ![Desteklenir](media/green_check.png) |
| CMPivot     | ![Desteklenir](media/green_check.png) |
| Uyumluluk ayarları     | ![Desteklenir](media/green_check.png) |
| İstemci yüklemesi<br>( [Azure AD tümleştirmesi](../../deploy/deploy-clients-cmg-azure.md)ile) | ![Desteklenir](media/green_check.png) |
| İstemci yüklemesi<br>( [belirteç kimlik doğrulaması](../../deploy/deploy-clients-cmg-token.md)ile) | ![Desteklenir](media/green_check.png) (2002) |
| Yazılım dağıtımı (cihaz hedefli)     | ![Desteklenir](media/green_check.png) |
| Yazılım dağıtımı (kullanıcı hedefli, gerekli)<br>(Azure AD tümleştirmesi ile)     | ![Desteklenir](media/green_check.png) |
| Yazılım dağıtımı (kullanıcı hedefli, kullanılabilir)<br>([tüm gereksinimler](../../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)) | ![Desteklenir](media/green_check.png) |
| Windows 10 [yerinde yükseltme görev dizisi](../../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) | ![Desteklenir](media/green_check.png) |
| **Görev sırasını başlatmadan önce tüm içeriği yerel olarak indirme** seçeneğiyle dağıtılan önyükleme görüntüsü olmayan görev dizisi | ![Desteklenir](media/green_check.png) |
| Önyükleme görüntüsü olmayan görev dizisi, [indirme seçeneğiyle](../../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg) dağıtıldı | ![Desteklenir](media/green_check.png) (1910) |
| Yazılım merkezinden başlatılan önyükleme görüntüsüne sahip görev dizisi | ![Desteklenir](media/green_check.png) (2006) |
| Diğer herhangi bir görev sırası senaryosu     | ![Desteklenmez](media/Red_X.png) |
| İstemci gönderme     | ![Desteklenmez](media/Red_X.png) |
| Otomatik site ataması     | ![Desteklenmez](media/Red_X.png) |
| Yazılım onay istekleri     | ![Desteklenmez](media/Red_X.png) |
| Configuration Manager konsolu     | ![Desteklenmez](media/Red_X.png) |
| Uzak araçlar     | ![Desteklenmez](media/Red_X.png) |
| Raporlama Web sitesi     | ![Desteklenmez](media/Red_X.png) |
| LAN'da Uyandırma     | ![Desteklenmez](media/Red_X.png) |
| Mac, Linux ve UNIX istemcileri     | ![Desteklenmez](media/Red_X.png) |
| Eş önbellek     | ![Desteklenmez](media/Red_X.png) |
| Şirket içi MDM     | ![Desteklenmez](media/Red_X.png) |
| BitLocker Yönetimi     | ![Desteklenmez](media/Red_X.png) |

|Anahtar|
|--|
|![Desteklenir](media/green_check.png) = Bu özellik tüm desteklenen Configuration Manager sürümleriyle CMG ile desteklenir  |
|![Desteklenen ](media/green_check.png) (*yymm*) = bu özellik, Configuration Manager *yymm* sürümü ile başlayarak CMG ile desteklenir  |
|![Desteklenmez](media/Red_X.png) = Bu özellik CMG ile desteklenmiyor |

#### <a name="note-1-support-for-endpoint-protection"></a><a name="bkmk_note1"></a>Note 1: Endpoint Protection için destek

Sürüm 2006 ' den başlayarak, bir CMG aracılığıyla iletişim kuran istemciler, Active Directory için etkin bir bağlantı olmadan Endpoint Protection ilkelerini hemen uygulayabilir.<!--4773948-->

<!-- 4350561 -->
Sürüm 2002 ve önceki sürümlerde, etki alanına katılmış cihazların Endpoint Protection ilkesini uygulaması için etki alanına erişmesi gerekir. İç ağa sık erişimli erişimi olan cihazlar Endpoint Protection ilkesini uygularken gecikmeler yaşar. Cihazların, alındıktan sonra Endpoint Protection ilkesini hemen uygulamasını istiyorsanız, aşağıdaki seçeneklerden birini göz önünde bulundurun:

- Siteyi ve istemcileri 2006 sürümüne güncelleştirin.

- Ortak yönetimi kullanın ve [Endpoint Protection iş yükünü](../../../../comanage/workloads.md#endpoint-protection) Intune 'a geçirin ve [Microsoft Defender virüsten koruma](https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#microsoft-defender-antivirus) 'yı buluttan yönetin.

- Endpoint Protection ilkesini uygulamak için yerel [kötü amaçlı yazılımdan koruma ilkeleri](../../../../protect/deploy-use/endpoint-antimalware-policies.md) özelliği yerine [yapılandırma öğelerini](../../../../compliance/deploy-use/create-configuration-items.md) kullanın.


## <a name="cost"></a>Maliyet

> [!IMPORTANT]  
> Aşağıdaki maliyet bilgileri yalnızca tahmin amaçlıdır. Ortamınızın CMG kullanmanın genel maliyetini etkileyen başka değişkenleri olabilir.

CMG, Azure abonelik hesabına ücretlendirieden aşağıdaki Azure bileşenlerini kullanır:

### <a name="virtual-machine"></a>Sanal makine

- CMG, hizmet olarak platform (PaaS) olarak Azure Cloud Services kullanır. Bu hizmet, işlem maliyetlerine tabi olan sanal makineleri (VM) kullanır.  

- CMG standart bir a2 v2 VM kullanır.  

- Kaç tane sanal makine örneğinin CMG 'yi desteklediğini seçersiniz. Biri varsayılandır ve 16 en yüksek değer olur. Bu sayı CMG oluşturulurken ayarlanır ve daha sonra gerektiğinde hizmeti ölçeklendirmek için değiştirilebilir.

- İstemcilerinizi desteklemek için ihtiyaç duyduğunuz VM 'Lerin sayısı hakkında daha fazla bilgi için bkz. [performans ve ölçek](#performance-and-scale).

- Olası maliyetleri belirlemede yardımcı olması için bkz. [Azure Fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) .

    > [!NOTE]  
    > Sanal makine maliyetleri bölgeye göre farklılık gösterir.

### <a name="outbound-data-transfer"></a>Giden veri aktarımı

- Ücretler, Azure 'dan (çıkış veya indirme) veri akışını temel alır. Azure 'daki tüm veri akışları ücretsizdir (giriş veya karşıya yükleme). CMG verileri, Azure 'dan, istemci bildirimlerine ve CMG tarafından Siteye iletilen istemci yanıtlarına olan istemci, istemci bildirimleri ve istemci yanıtlarını içerir. Bu yanıtlar, envanter raporlarını, durum iletilerini ve uyumluluk durumunu içerir.  

- CMG ile iletişim kuran hiçbir istemci olmasa bile, bazı arka plan iletişimleri CMG ve şirket içi site arasında ağ trafiğine neden olur.  

- Configuration Manager konsolundaki **giden veri aktarımını (GB)** görüntüleyin. Daha fazla bilgi için bkz. [CMG 'de Istemcileri izleme](monitor-clients-cloud-management-gateway.md).  

- Olası maliyetleri belirlemede yardımcı olması için bkz. [Azure bant genişliği fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/bandwidth/) . Veri aktarımı fiyatlandırması katmanlı. Ne kadar çok kullanırsanız, gigabayt başına ödeme yaparsınız.  

- *Yalnızca tahmin etmek için*, internet tabanlı istemciler için aylık olarak YAKLAŞıK 100-300 MB bekler. Düşük tahmin, varsayılan istemci yapılandırmasına yöneliktir. Üst tahmin, daha Agresif istemci yapılandırmasına yöneliktir. Gerçek kullanımınız, istemci ayarlarını nasıl yapılandırdığınıza bağlı olarak değişebilir.  

    > [!NOTE]  
    > Yazılım güncelleştirmelerini veya uygulamaları dağıtma gibi diğer eylemler gerçekleştirmek, Azure 'dan giden veri aktarımı miktarını arttırır.

- Internet tabanlı istemciler, Microsoft yazılım güncelleştirme içeriğini Windows Update 'tan ücretsiz olarak alır. Güncelleştirme paketlerini Microsoft Update içeriğiyle bir bulut dağıtım noktasına dağıtmayın, aksi takdirde depolama ve veri çıkış maliyetlerine tabi olabilirsiniz.  

- **İstemci sertifikası Iptalini doğrulamak** için CMG seçeneğinin yanlış yapılandırılması, istemcilerden CMG 'ye ek trafik oluşmasına neden olabilir. Bu ek trafik Azure çıkış verilerini artırabilir ve bu da Azure maliyetlerinizi artırabilir.<!-- SCCMDocs#1434 --> Daha fazla bilgi için bkz. [sertifika iptal listesini yayımlama](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

### <a name="content-storage"></a>İçerik depolama

- Internet tabanlı istemciler, Microsoft yazılım güncelleştirme içeriğini Windows Update 'tan ücretsiz olarak alır. Güncelleştirme paketlerini Microsoft Update içeriğiyle bir bulut dağıtım noktasına dağıtmayın, aksi takdirde depolama ve veri çıkış maliyetlerine tabi olabilirsiniz.  

- Uygulamalar veya üçüncü taraf yazılım güncelleştirmeleri gibi diğer gerekli içerikler için bir bulut dağıtım noktasına dağıtmanız gerekir. Şu anda CMG, yalnızca istemcilere içerik göndermek için bulut dağıtım noktasını destekler.
   - İçerik depolaması için bir CMG kullanırken, kullanılabilir [istemci ayarı](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) etkinleştirildiğinde **Delta içeriğini indir** , üçüncü taraf güncelleştirmeler için içerik istemcilere indirmez. <!--6598587--> 

- Daha fazla bilgi için bkz. [bulut dağıtım noktalarını](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost)kullanma maliyeti.  

- Bir CMG, istemcilere içerik sunacak bir bulut dağıtım noktası da olabilir. Bu işlevsellik, Azure VM 'lerinin gerekli sertifikalarını ve maliyetini azaltır. Daha fazla bilgi için bkz. [CMG 'Yi değiştirme](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

- CMG, Azure yerel olarak yedekli depolama (LRS) kullanır. Daha fazla bilgi için bkz. [yerel olarak yedekli depolama](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

### <a name="other-costs"></a>Diğer maliyetler

- Her bulut hizmetinin dinamik bir IP adresi vardır. Her farklı CMG yeni bir dinamik IP adresi kullanır. CMG başına ek VM 'Ler eklemek bu adresleri artırmaz.  

## <a name="performance-and-scale"></a>Performans ve ölçeklendirme

CMG ölçeği hakkında daha fazla bilgi için bkz. [boyut ve ölçek numaraları](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg).

Aşağıdaki öneriler CMG performansını iyileştirmenize yardımcı olabilir:

- Configuration Manager istemcisiyle CMG arasındaki bağlantı bölge ile uyumlu değildir. İstemci iletişimi gecikme süresi/coğrafi ayrım tarafından büyük ölçüde etkilenmez. Coğrafi yakınlık amacıyla birden çok CMG dağıtmak gerekli değildir. Hiyerarşinizdeki üst düzey sitede CMG 'yi dağıtın ve ölçeği artırmak için örnekler ekleyin.

- Hizmetin yüksek kullanılabilirliği için, en az iki CMG örneği ve site başına iki CMG bağlantı noktası ile bir CMG oluşturun.  

- Daha fazla VM örneği ekleyerek CMG 'yi daha fazla istemciyi destekleyecek şekilde ölçeklendirin. Azure yük dengeleyici, hizmete istemci bağlantılarını denetler.  

- Yükü aralarında dağıtmak için daha fazla CMG bağlantı noktası oluşturun. CMG, trafiği bağlantı CMG bağlantı noktalarına, hepsini bir kez deneme biçimde dağıtır.  

- CMG, desteklenen sayıda istemciden daha fazla yüksek yük altında olduğunda, hala istekleri işler, ancak gecikme olabilir.  

> [!NOTE]
> Configuration Manager, bir CMG bağlantı noktası için istemci sayısı üzerinde sabit sınır olmadığından, Windows Server varsayılan en yüksek TCP dinamik bağlantı noktası aralığı olan 16.384 ' dir. Bir Configuration Manager sitesi tek bir CMG bağlantı noktası ile 16.384 ' den fazla istemciyi yönetirse, Windows Server sınırını artırmanız gerekir. Tüm istemciler, CMG bağlantı noktasında açık bir bağlantı noktasını tutan istemci bildirimleri için bir kanal tutar. Bu sınırı artırmak üzere Netsh komutunu kullanma hakkında daha fazla bilgi için, [Microsoft desteği makalesi 929851](https://support.microsoft.com/help/929851)' e bakın.

## <a name="ports-and-data-flow"></a>Bağlantı noktaları ve veri akışı

Şirket içi ağınıza gelen bağlantı noktalarını açmanıza gerek yoktur. Hizmet bağlantı noktası ve CMG bağlantı noktası tüm Azure ve CMG ile iletişimi başlatır. Bu iki site sistem rolünün, Microsoft bulutuna giden bağlantılar oluşturması gerekir. Hizmet bağlantı noktası, hizmeti Azure 'da dağıtır ve izler, bu nedenle çevrimiçi mod olmalıdır. CMG bağlantı noktası CMG ve şirket içi site sistem rolleri arasındaki iletişimi yönetmek için CMG 'ye bağlanır.

Aşağıdaki diyagram CMG için temel ve kavramsal bir veri akışıdır:

[![CMG veri akışı](media/cmg-data-flow.png)](media/cmg-data-flow.png#lightbox)

1. Hizmet bağlantı noktası, HTTPS bağlantı noktası 443 üzerinden Azure 'a bağlanır. Azure AD veya Azure Yönetim sertifikası kullanarak kimlik doğrulaması gerçekleştirir. Hizmet bağlantı noktası, Azure 'da CMG 'yi dağıtır. CMG, sunucu kimlik doğrulama sertifikasını kullanarak HTTPS bulut hizmetini oluşturur.  

2. CMG bağlantı noktası, Azure 'daki CMG 'ye TCP-TLS veya HTTPS üzerinden bağlanır. Bağlantıyı açık tutar ve gelecekteki iki yönlü iletişim için kanalı oluşturur.  

3. İstemci, HTTPS bağlantı noktası 443 üzerinden CMG 'ye bağlanır. Azure AD veya istemci kimlik doğrulama sertifikası kullanarak kimlik doğrular.  

    > [!NOTE]
    > CMG 'yi içeriğe sunabilir veya bir bulut dağıtım noktası kullanmak üzere etkinleştirirseniz, istemci HTTPS bağlantı noktası 443 üzerinden doğrudan Azure Blob depolamaya bağlanır. Daha fazla bilgi için bkz. [bulut tabanlı dağıtım noktası kullanma](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).<!-- SCCMDocs#2332 -->

4. CMG, istemci iletişimini mevcut bağlantı üzerinden şirket içi CMG bağlantı noktasına iletir. Herhangi bir gelen güvenlik duvarı bağlantı noktasını açmanıza gerek yoktur.  

5. CMG bağlantı noktası, istemci iletişimini şirket içi yönetim noktasına ve yazılım güncelleştirme noktasına iletir.  

Azure 'da içerik barındırdığınızda daha fazla bilgi için bkz. [bulut tabanlı dağıtım noktası kullanma](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="required-ports"></a>Gerekli bağlantı noktaları

Bu tabloda gerekli ağ bağlantı noktaları ve protokoller listelenmektedir. *İstemci* , bağlantıyı başlatan cihazdır ve giden bağlantı noktası gerektirir. *Sunucu* , bağlantıyı kabul eden ve bir gelen bağlantı noktası gerektiren cihazdır.

| İstemci | Protokol | Bağlantı noktası | Sunucu | Açıklama |
|--------|----------|------|--------|-------------|
| Hizmet bağlantı noktası | HTTPS | 443 | Azure | CMG dağıtımı |
| CMG bağlantı noktası | TCP-TLS | 10140-10155 | CMG hizmeti | CMG kanalı oluşturmak için tercih edilen protokol <sup> [nonote 1](#bkmk_port-note1)</sup> |
| CMG bağlantı noktası | HTTPS | 443 | CMG hizmeti | CMG kanalını yalnızca bir VM örneğine derlemek için geri dönüş Protokolü <sup> [Note 2](#bkmk_port-note2)</sup> |
| CMG bağlantı noktası | HTTPS | 10124-10139 | CMG hizmeti | CMG kanalını iki veya daha fazla VM örneğine derlemek için geri dönüş Protokolü <sup> [Note 3](#bkmk_port-note3)</sup> |
| İstemci | HTTPS | 443 | CMG | Genel istemci iletişimi |
| İstemci | HTTPS | 443 | Blob depolama | Bulut tabanlı içeriği indirme |
| CMG bağlantı noktası | HTTPS veya HTTP | 443 veya 80 | Yönetim noktası | Şirket içi trafik, bağlantı noktası yönetim noktası yapılandırmasına bağımlıdır |
| CMG bağlantı noktası | HTTPS veya HTTP | 443 veya 80 | Yazılım güncelleştirme noktası | Şirket içi trafik, bağlantı noktası yazılım güncelleştirme noktası yapılandırmasına bağlıdır |

#### <a name="note-1-cmg-connection-point-tcp-tls-ports"></a><a name="bkmk_port-note1"></a>Note 1: CMG bağlantı noktası TCP-TLS bağlantı noktaları

CMG bağlantı noktası ilk olarak her CMG VM örneğiyle uzun süreli bir TCP-TLS bağlantısı kurmaya çalışır. Bağlantı noktası 10140 ' deki ilk sanal makine örneğine bağlanır. İkinci VM örneği 10141 numaralı bağlantı noktasını 16. bağlantı noktası 10155 ' de kullanır. TCP-TLS bağlantısı en iyi şekilde çalışır, ancak Internet proxy 'yi desteklemez. CMG bağlantı noktası TCP-TLS aracılığıyla bağlanamıyorsa, HTTPS<sup>[Note 2](#bkmk_port-note2)</sup>' ye geri döner.

#### <a name="note-2-cmg-connection-point-https-ports-for-one-vm"></a><a name="bkmk_port-note2"></a>2. Note: bir VM için CMG bağlantı noktası HTTPS bağlantı noktaları

CMG bağlantı noktası, CMG 'yi TCP-TLS<sup>[Not1](#bkmk_port-note1)</sup>aracılığıyla bağlanamıyorsa, yalnızca bir VM örneği IÇIN, https 443 üzerinden Azure ağ yükü dengeleyiciye bağlanır.  

#### <a name="note-3-cmg-connection-point-https-ports-for-two-or-more-vms"></a><a name="bkmk_port-note3"></a>3. notta, iki veya daha fazla VM için CMG bağlantı noktası HTTPS bağlantı noktaları

İki veya daha fazla VM örneği varsa, CMG bağlantı noktası https 443 değil ilk VM örneğine HTTPS 10124 kullanır. HTTPS bağlantı noktası 10139 ' de 16 ' ya kadar HTTPS 10125 ' deki ikinci sanal makine örneğine bağlanır.

### <a name="internet-access-requirements"></a>İnternet erişimi gereksinimleri

Kuruluşunuz ağ iletişimini bir güvenlik duvarı veya ara cihaz kullanarak internet ile kısıtlarsa, CMG bağlantı noktası ve hizmet bağlantı noktasının İnternet uç noktalarına erişmesine izin vermeniz gerekir.

Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../../../plan-design/network/internet-endpoints.md#bkmk_cloud).

## <a name="next-steps"></a>Sonraki adımlar

- [Bulut yönetimi ağ geçidine yönelik sertifikalar](certificates-for-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidi için güvenlik ve gizlilik](security-and-privacy-for-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidi boyutu ve ölçek numaraları](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
- [Bulut yönetimi ağ geçidi hakkında sık sorulan sorular](cloud-management-gateway-faq.md)
- [Bulut yönetimi ağ geçidini kurma](setup-cloud-management-gateway.md)
