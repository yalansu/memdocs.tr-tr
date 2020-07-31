---
title: Azure’da Configuration Manager
titleSuffix: Configuration Manager
description: Azure ortamında Configuration Manager kullanımı hakkında bilgiler.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9d398d7fddab61014547fc0f8f64cd180e58ab6
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438571"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Azure 'da Configuration Manager-sık sorulan sorular

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aşağıdaki sorular ve yanıtlar, ne zaman kullanılacağını ve Microsoft Azure Configuration Manager nasıl yapılandırılacağını anlamanıza yardımcı olabilir.

## <a name="general-questions"></a>Genel Sorular
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Şirketim Microsoft Azure için olabildiğince fazla fiziksel sunucu taşımaya çalışıyor, Configuration Manager sunucularını Azure 'a taşıyabilir miyim?
Kesinlikle, bu desteklenen bir senaryodur.  Bkz. [Configuration Manager Için sanallaştırma ortamları desteği](../plan-design/configs/support-for-virtualization-environments.md).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Harika! Ortamım birden çok site gerektiriyor. Tüm alt birincil siteler, merkezi yönetim sitesi veya şirket içi Azure 'da olmalıdır mi? İkincil siteler ne kadar?
Siteden siteye iletişimler (dosya tabanlı ve veritabanı çoğaltma) Azure 'da barındırılmanın yakınından faydalanır. Ancak, istemci ile ilgili tüm trafik site sunucularından ve Site sistemlerinden uzak olur. Sınırsız bir veri planıyla Azure ile intranetiniz arasında hızlı ve güvenilir bir ağ bağlantısı kullanıyorsanız, tüm altyapınızı Azure 'da barındırmak bir seçenektir.

Ancak, ölçülen bir veri planı kullanırsanız ve kullanılabilir bant genişliği veya maliyeti sorun oluşturacaksa ya da Azure ile intranetiniz arasındaki ağ bağlantısı hızlı değilse veya güvenilir değilse, belirli siteleri (ve site sistemlerini) şirket içine yerleştirmeyi ve sonra Configuration Manager yerleşik bant genişliği denetimlerini kullanmayı düşünün.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Azure 'da bir SaaS senaryosunda (hizmet olarak yazılım) Configuration Manager yaşıyor musunuz?
Hayır, Azure sanal makinelerinde Configuration Manager altyapı sunucularınızı barındırmanıza yönelik bir IaaS (hizmet olarak altyapı).

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>Configuration Manager altyapımın Azure 'a taşınmasını düşünürken hangi alanlara dikkat çekmem gerekir?
Harika soru, bu kararı verirken en önemli alanlardır, her biri bu konunun ayrı bir bölümünde keşfedilir:
1. Ağ
2. Kullanılabilirlik
3. Performans
4. Maliyet
5. Kullanıcı Deneyimi

## <a name="networking"></a>Ağ
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>Ağ gereksinimleri hakkında ne kadar ExpressRoute veya bir Azure VPN Gateway kullanmalıyım?
Ağ iletişimi çok önemli bir karardır. Ağ hızları ve gecikme süresi, site sunucusu ile uzak site sistemleri ile site sistemlerine yapılan istemci iletişimi arasındaki işlevselliği etkileyebilir. Önerimiz ExpressRoute kullanmaktır. Ancak Azure VPN Gateway 'yi kullanmayı durdurmak için Configuration Manager sınırlaması yoktur. Gereksinimlerinizi (performans, düzeltme eki uygulama, yazılım dağıtımı, işletim sistemi dağıtımı) bu altyapıdan dikkatle gözden geçirmeniz ve sonra kararlarınızı yapmanız gerekir. Her çözüm için göz önünde bulundurmanız gereken bazı noktalar şunlardır:

- **ExpressRoute** (önerilir)
  - Veri merkezinize doğal uzantı (birden çok veri merkezini bağlayabilir)
  - Azure veri merkezleri ve altyapınız arasındaki özel bağlantılar
  - Genel internet üzerinden geçmiyor
  - Güvenilirlik, hızlı hız, daha düşük gecikme süresi, yüksek güvenlik sağlar
  - En fazla 10 Gbps hız ve sınırsız veri planı seçeneği sunar
- **VPN Gateway**
  - Siteden siteye/Noktadan siteye VPN 'Leri
  - Trafik, genel İnternet üzerinden gider
  - Internet Protokolü güvenliği (IPSec) ve İnternet Anahtar Değişimi (ıKE) kullanır

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute, sınırsız ve tarifeli, farklı hız seçenekleri ve Premium eklenti gibi birçok farklı seçeneğe sahiptir. Hangisini seçmeliyim?
Seçtiğiniz seçenekler, uyguladığınız senaryoya ve ne kadar veri dağıtmayı planladığınıza bağlıdır. Configuration Manager verilerinin aktarımı site sunucuları ile dağıtım noktaları arasında denetlenebilir, ancak siteden siteye sunucu iletişimi denetlenemez.   Tarifeli bir veri planı kullandığınızda, belirli siteleri (ve site sistemlerini) şirket içinde yerleştirmek ve [Configuration Manager yerleşik bant genişliği denetimlerini](../plan-design/hierarchy/fundamental-concepts-for-content-management.md) kullanmak, Azure kullanma maliyetini denetlemenize yardımcı olabilir.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Active Directory etki alanları gibi yükleme gereksinimleri nelerdir? Hala site sunucularımı bir Active Directory etki alanına birleştirmem gerekir mi?
Evet. Azure 'a geçtiğinizde, [desteklenen yapılandırma](../plan-design/configs/supported-configurations.md) Configuration Manager yüklemek için Active Directory gereksinimleri de dahil olmak üzere aynı kalır.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Site sunucularımı bir Active Directory etki alanına ekleme gereksinimini anladım, ancak Azure Active Directory kullanabilir miyim?
Hayır, Azure Active Directory şu anda desteklenmiyor. Site sunucularınızın hala bir [Windows Active Directory etki alanı](../plan-design/configs/support-for-active-directory-domains.md)üyesi olması gerekir.



## <a name="availability"></a>Kullanılabilirlik
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Altyapıyı Azure 'a taşıma nedenlerinden biri, yüksek kullanılabilirlik taahhüdüne sahiptir. Configuration Manager için kullanacağım VM 'Ler için Azure VM kullanılabilirlik kümeleri gibi yüksek kullanılabilirlik seçeneklerinden yararlanabilir miyim?
Evet! Azure VM kullanılabilirlik kümeleri, dağıtım noktaları veya yönetim noktaları gibi yedekli site sistem rolleri için kullanılabilir.

Bunları Configuration Manager site sunucuları için de kullanabilirsiniz. Örneğin, merkezi yönetim siteleri ve birincil siteler aynı Kullanılabilirlik kümesinde olabilir, bu da aynı anda yeniden önyükleme olmamasını sağlamanıza yardımcı olabilir.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Veritabanımı yüksek oranda kullanılabilir hale getirebilirsiniz? Azure SQL veritabanı 'nı kullanabilir miyim? Ya da bir VM 'de Microsoft SQL Server kullanmak zorunda mıyım?
Bir VM 'de Microsoft SQL Server kullanmanız gerekir. Configuration Manager şu anda Azure SQL Server desteklemiyor. Ancak SQL sunucunuz için AlwaysOn Kullanılabilirlik Grupları gibi işlevleri de kullanabilirsiniz. [AlwaysOn kullanılabilirlik grupları](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) önerilir ve Configuration Manager sürüm 1602 ' den başlayarak resmi olarak desteklenir.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Yönetim noktaları veya yazılım güncelleştirme noktaları gibi site sistem rolleriyle Azure yük dengeleyiciler kullanabilir miyim?
Configuration Manager Azure yük dengeleyiciler ile sınanmasa da, işlevler uygulama için saydamsa, normal işlemlerde olumsuz etkileri olmamalıdır.


## <a name="performance"></a>Performans
### <a name="what-factors-affect-performance-in-this-scenario"></a>Bu senaryodaki performansı etkileyen etmenler nelerdir?
[Azure VM boyutu ve türü](/azure/virtual-machines/sizes), Azure VM diskleri (Premium Depolama önerilir, özellikle SQL Server için), ağ gecikmesi ve hız en önemli alanlardır.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Bu nedenle, Azure sanal makineleri hakkında daha fazla bilgi verin. VM 'Leri hangi boyutta kullanmalıyım?
Genel olarak, işlem gücünün (CPU ve bellek) [Configuration Manager için önerilen donanımları](../plan-design/configs/recommended-hardware.md)karşılaması gerekir. Ancak, özellikle bu VM 'Lerin kullanıldığı disklere geldiğinde, normal bilgisayar donanımı ve Azure VM 'Leri arasında bazı farklılıklar vardır.  Kullandığınız sanal makinelerin boyutu, ortamınızın boyutuna bağlıdır ancak bazı öneriler aşağıda verilmiştir:
- Önemli boyuttaki üretim dağıtımları için, "**S**" sınıfı Azure VM 'leri önerilir. Bunun nedeni, Premium Depolama disklerinden faydalanabilir.  "S" olmayan sınıf VM 'Leri BLOB depolama alanı kullanır ve genel olarak, kabul edilebilir bir üretim deneyimi için gereken performans gereksinimlerini karşılamıyor.
- Daha yüksek ölçek için birden fazla Premium Depolama diski kullanılmalıdır ve en yüksek ıOPS için Windows Disk Yönetimi konsolunda dizili olmalıdır.  
- İlk site dağıtımınız sırasında daha iyi veya birden fazla Premium disk kullanmanızı öneririz (P20 yerine P30 gibi ve 1 Xp30 yerine dizili bir birimde 2xP30). Daha sonra, sitenizin daha sonra ek yük nedeniyle VM boyutunda daha fazla büyütülebilmeniz gerekiyorsa, daha büyük bir VM boyutunun sağladığı ek CPU ve bellekten yararlanabilirsiniz. Ayrıca, daha büyük VM boyutunun izin verdiği ek ıOPS iş hızından faydalanabilir disklere sahip olursunuz.



Aşağıdaki tablolarda, çeşitli boyut yüklemeleri için birincil ve merkezi yönetim sitelerinde kullanmak üzere önerilen ilk disk sayısı listelenmektedir:

Site sunucusundaki site veritabanıyla birlikte, **birlikte bulunan site veritabanı** -birincil veya merkezi yönetim sitesi:

| Masaüstü Istemcileri    |Önerilen VM boyutu|Önerilen diskler|
|--------------------|-------------------|-----------------|
|**25k 'a kadar**       |   DS4_V2          |2xP30 (dizili)  |
|**25k-50.000**      |   DS13_V2         |2xP30 (dizili)  |
|**50.000-100.000**     |   DS14_V2         |3xP30 (dizili)  |


Uzak **site veritabanı** -uzak bir sunucuda site veritabanıyla birincil veya merkezi yönetim sitesi:

| Masaüstü Istemcileri    |Önerilen VM boyutu|Önerilen diskler |
|--------------------|-------------------|------------------|
|**25k 'a kadar**       | Site sunucusu: F4S </br>Veritabanı sunucusu: DS12_V2 | Site sunucusu: 1xP30 </br>Veritabanı sunucusu: 2xP30 (dizili)  |
|**25k-50.000**      | Site sunucusu: F4S </br>Veritabanı sunucusu: DS13_V2 | Site sunucusu: 1xP30 </br>Veritabanı sunucusu: 2xP30 (dizili)   |
|**50.000-100.000**     | Site sunucusu: F8S </br>Veritabanı sunucusu: DS14_V2 | Site sunucusu: 2xP30 (dizili)   </br>Veritabanı sunucusu: 3xP30 (dizili)   |

Aşağıda, Configuration Manager yüklemesi ve veritabanı dosyaları: ![ VM) diskleri için ayrı mantıksal birimler içeren bir şeritli birimde 3xp30 disk ile DS14_V2 50.000 ila 100.000 istemcileri ile ilgili bir örnek yapılandırma gösterilmektedir.](media/vm_disks.png)  



## <a name="user-experience"></a>Kullanıcı Deneyimi
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Kullanıcı deneyiminin önem derecesine ait ana alanlardan biri olduğunu bahsettiğinizde, bunun nedeni nedir?
Ağ, kullanılabilirlik, performans ve Configuration Manager site sunucularınızın yerleştirileceği kararlar, kullanıcılarınızı doğrudan etkileyebilir. Azure 'a yapılan bir taşımanın kullanıcılarınız için saydam olması gerektiğine inandık. bu sayede, Configuration Manager ile gündelik etkileşimlerinde değişiklik karşılaşmazlar.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>Tamam, bunu aldım. Azure sanal makinesine tek bir tek başına birincil site yüklemeyi planlıyorum ve maliyetlerimin düşük olduğundan emin olmak istiyorum. (Uzak) site sistemlerini (yönetim noktaları, dağıtım noktaları ve yazılım güncelleştirme noktaları gibi) Azure sanal makinelerinde da veya şirket içinde yerleştirmem gerekir mi?
Site sunucusundan bir dağıtım noktasına yönelik iletişim dışında, bir sitedeki bu sunucudan sunucuya iletişimler herhangi bir zamanda gerçekleşebilir ve ağ bant genişliği kullanımını denetlemek için mekanizmalar kullanmaz. Site sistemleri arasındaki iletişimi denetleyemediği için, bu iletişimlerle ilişkili tüm ücretler göz önünde bulundurulmalıdır.

Ağ hızları ve gecikme süreleri de göz önünde bulundurmanız gereken diğer faktörlerdir. Yavaş veya güvenilir olmayan ağlar, site sunucusu ile uzak site sistemleri arasındaki işlevselliği ve site sistemlerine yönelik istemci iletişimini etkileyebilir. Belirli bir site sistemi kullanan yönetilen istemci sayısı ve etkin olarak kullandığınız özellikler de göz önünde bulundurulmalıdır.
Genel olarak, WAN bağlantılarıyla ve site sistemleriyle bir başlangıç noktası olarak ilişkili olduğundan normal kılavuzdan yararlanabilirsiniz. İdeal olarak, Azure ile intranetiniz arasında seçtiğiniz ve aldığınız ağ aktarım hızı, hızlı bir ağla iyi bağlanmış bir WAN ile tutarlı olacaktır.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>İçerik dağıtımı ve içerik yönetimi hakkında ne olacak? Standart dağıtım noktaları Azure 'da veya şirket içinde olmalıdır ve şirket içi BranchCache veya çekme dağıtım noktaları kullanmalıdır mi? Ya da bulut dağıtım noktalarından özel olarak kullanılması gerekir mi?
İçerik yönetimine yönelik yaklaşım, site sunucuları ve site sistemleri için çok benzer.
- Sınırsız bir veri planıyla Azure ile intranetiniz arasında hızlı ve güvenilir bir ağ bağlantısı kullanıyorsanız, Azure 'da standart dağıtım noktalarını barındırmak bir seçenek olabilir.
- Tarifeli bir veri planı kullanırsanız ve bant genişliği maliyeti bir sorun olduğunda veya Azure ile intranetiniz arasındaki ağ bağlantısı hızlı değilse veya güvenilir değilse, diğer yaklaşımları göz önünde bulundurmanız gerekebilir. Bunlar, şirket içi standart veya çekme dağıtım noktalarının yanı sıra BranchCache 'i kullanmayı da içerir. Bulut tabanlı dağıtım noktalarının kullanımı da bir seçenektir, ancak desteklenen içerik türlerinde bazı sınırlar vardır (örneğin, yazılım güncelleştirme paketleri desteği yoktur).

> [!NOTE]
>  PXE veya çok noktaya yayın desteği gerekliyse, önyükleme isteklerine yanıt vermek için şirket içi dağıtım noktalarını (Standart veya çekme) kullanmanız gerekir.


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Bulut tabanlı dağıtım noktalarının sınırlamalarıyla karşılaştığım halde, internet tabanlı istemcilerinizi desteklemek için gerekli olsa bile yönetim noktamı bir DMZ 'e koymak istemiyorum. Başka bir seçenek var mı?
Evet! Configuration Manager sürüm 1610 ile [bulut yönetimi ağ geçidi](../clients/manage/manage-clients-internet.md#cloud-management-gateway) bir ön sürüm özelliği olarak tanıtıldık. (Bu özellik önce, [bulut proxy hizmeti](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)olarak Technical Preview sürüm 1606 ' de göründü).

**Bulut yönetimi ağ geçidi** , ınternet 'teki Configuration Manager istemcilerini yönetmek için basit bir yol sağlar. Microsoft Azure dağıtılan ve bir Azure aboneliği gerektiren hizmet, bulut yönetimi ağ geçidi bağlayıcı noktası adlı yeni bir rol kullanarak şirket içi Configuration Manager altyapınıza bağlanır. Dağıtıldıktan ve yapılandırıldıktan sonra istemciler, iç özel ağa mı yoksa internet 'e mi bağlı olduklarına bakılmaksızın şirket içi Configuration Manager site sistem rollerine erişebilirler.

Ortamınızda bulut yönetimi ağ geçidini kullanmaya başlayabilir ve bunu daha iyi hale getirmek için bize geri bildirimde bulunun. Yayın öncesi özellikler hakkında daha fazla bilgi için bkz. [güncelleştirmelerden yayın öncesi özellikleri kullanma](../servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Ayrıca, sürüm 1610 ' de yayın öncesi özelliği olarak sunulan eş önbellek adlı başka bir yeni özelliğe sahip olduğumu duydum. BranchCache 'den farklı mi? Hangisini seçmem gerekir?
Evet, tamamen farklıdır. [Eş önbellek](../plan-design/hierarchy/client-peer-cache.md) , BranchCache 'In bir Windows özelliği olduğu %100 yerel bir Configuration Manager teknolojisidir. Her ikisi de yararlı olabilir; BranchCache, gerekli içeriği bulmak için bir yayın kullanır, ancak eş önbelleği Configuration yöneticileri düzenli dağıtım iş akışı ve sınır grubu ayarlarını kullanır.

Herhangi bir istemciyi eş önbellek kaynağı olacak şekilde yapılandırabilirsiniz. Ardından, yönetim noktaları, içerik kaynak konumları hakkında istemci bilgileri sunduklarında, hem dağıtım noktaları hem de istemcinin gerektirdiği içeriğe sahip tüm eş önbellek kaynakları hakkında ayrıntılar sağlar.


## <a name="cost"></a>Maliyet
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>Tamam, maliyetle ilgili bir bit bilgi verin. Bu, benim için uygun maliyetli bir çözüm olacak mı?
Her ortam farklı olduğundan, zor olacak. En iyi şey, ortamınız Microsoft Azure Fiyatlandırma Hesaplayıcı kullanarak maliyetlidir:https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Ek Kaynaklar
**Temel bilgiler:**https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Azure VM makine türleri:**
- Azure makine boyutları:https://docs.microsoft.com/azure/virtual-machines/sizes  
- VM fiyatlandırması:https://azure.microsoft.com/pricing/details/virtual-machines/  
- Depolama fiyatlandırması:https://azure.microsoft.com/pricing/details/storage/

**Disk performansı konuları:**    
- Premium disk girişi:https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Daha derin Premium disk bilgileri:https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- Depolama için maksimum boyut ve performans hedefleri için kullanışlı grafik koleksiyonu:https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- Diğer bir giriş ve Premium depolamanın her bir arka planda nasıl çalıştığı ile ilgili bazı seyrek erişimli veriler:https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Sonrası**
- Azure IaaS çalışma süresi SLA 'Sı:https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- Açıklanan kullanılabilirlik kümeleri:https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability

**Bilirlik**
- Express Route ile Azure VPN:https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- Express Route fiyatlandırması:https://azure.microsoft.com/pricing/details/expressroute/
- Express Route hakkında daha fazla bilgi:https://azure.microsoft.com/documentation/articles/expressroute-introduction/
