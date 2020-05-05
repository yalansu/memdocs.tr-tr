---
title: Bulut dağıtım noktası
titleSuffix: Configuration Manager
description: Configuration Manager içindeki bulut dağıtım noktalarıyla Microsoft Azure aracılığıyla yazılım içeriğini dağıtmayı planlayın ve tasarlayın.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7a14b79a9e7fd91b6470836b4271a669725065bd
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771160"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Configuration Manager bir bulut dağıtım noktası kullanın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Azure 'dan içerik paylaşmaya yönelik uygulama değişti. **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin verme ve Azure depolama 'dan içerik**sunma seçeneğini etkinleştirerek, içerik özellikli bir bulut yönetimi ağ geçidi kullanın. Daha fazla bilgi için bkz. [CMG 'Yi değiştirme](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> Gelecekte geleneksel bir bulut dağıtım noktası oluşturamayacak. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Bulut dağıtım noktası, Microsoft Azure bir hizmet olarak platform (PaaS) olarak barındırılan bir Configuration Manager dağıtım noktasıdır. Bu hizmet aşağıdaki senaryoları destekler:  

- İnternet tabanlı istemcilere ek şirket içi altyapı olmadan yazılım içeriği sağlama  

- Bulut-içerik dağıtım sisteminizi etkinleştirin  

- Geleneksel dağıtım noktaları gereksinimini azaltma  

Bu makale, bulut dağıtım noktası hakkında bilgi edinmenize, kullanımını planlamanızı ve uygulamanızı tasarlamanıza yardımcı olur. Aşağıdaki bölümleri içerir:

- [Özellikler ve avantajlar](#bkmk_features)
- [Topoloji tasarımı](#bkmk_topology)
- [Gereksinimler](#bkmk_requirements)
- [Belirtimler](#bkmk_spec)
- [Maliyet](#bkmk_cost)
- [Performans ve ölçeklendirme](#bkmk_perf)
- [Bağlantı noktaları ve veri akışı](#bkmk_dataflow)
- [Sertifikalar](#bkmk_certs)
- [Sık sorulan sorular (SSS)](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a>Özellikler ve avantajlar

### <a name="features"></a>Özellikler

Bulut dağıtım noktası, şirket içi dağıtım noktaları tarafından da sunulan çeşitli özellikleri destekler:  

- Bulut dağıtım noktalarını ayrı ayrı veya dağıtım noktası gruplarının üyeleri olarak yönetin  

- Bir bulut dağıtım noktasını geri dönüş içerik konumu olarak kullan  

- Hem intranet hem de internet tabanlı istemcileri destekler  

### <a name="benefits"></a>Avantajlar

Bulut dağıtım noktası aşağıdaki ek avantajları sağlar:  

- Site, içeriği Azure 'daki bulut dağıtım noktasına göndermeden önce şifreler.  

- İstemcilere yönelik içerik isteklerine yönelik değişiklik taleplerini karşılamak için, Azure 'da bulut hizmetini manuel olarak ölçeklendirin. Bu eylem, Configuration Manager ek dağıtım noktaları yüklemenizi ve sağlamanızı gerektirmez.  

- Windows BranchCache ve alternatif içerik sağlayıcıları gibi diğer içerik teknolojileri için yapılandırılmış istemcilerden içerik indirmeyi destekler.  

- Sürüm 1806 ' den başlayarak, çekme dağıtım noktaları için bulut dağıtım noktalarını kaynak konumları olarak kullanın.  


## <a name="topology-design"></a><a name="bkmk_topology"></a>Topoloji tasarımı

Bulut dağıtım noktasının dağıtımı ve işlemi aşağıdaki bileşenleri içerir:  

- Azure 'da bir **bulut hizmeti** . Site, içeriği bu hizmete dağıtır ve Azure Bulut depolamada depolar. Yönetim noktası, istemcilerin bu içerik konumunu kullanılabilir kaynaklar listesinde uygun şekilde sağlar.  

- Bir **Yönetim noktası** site sistemi Rol Hizmetleri istemci isteklerini normal başına ister.  

    - Şirket içi istemciler genellikle şirket içi yönetim noktası kullanır.  

    - Internet tabanlı istemciler bir [bulut yönetimi ağ geçidi](../../clients/manage/cmg/plan-cloud-management-gateway.md)ya da [İnternet tabanlı bir yönetim noktası](../../clients/manage/plan-internet-based-client-management.md)kullanır.  

- Bulut dağıtım noktası, istemcilerle ağ iletişimine güvenli hale getirmek için **sertifika tabanlı BIR https** Web hizmeti kullanır. İstemcilerin bu sertifikaya güvenmesi gerekir.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
Sürüm 1806 ' den başlayarak bir **Azure Resource Manager dağıtımı**kullanarak bir bulut dağıtım noktası oluşturun. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) , tüm çözüm kaynaklarının, [kaynak grubu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)olarak adlandırılan tek bir varlık olarak yönetilmesine yönelik modern bir platformdur. Azure Resource Manager ile bulut dağıtım noktası dağıtımında, site kimlik doğrulaması yapmak ve gerekli bulut kaynaklarını oluşturmak için Azure Active Directory (Azure AD) kullanır. Bu modernlanmış dağıtım, klasik Azure Yönetim sertifikası gerektirmez.  

> [!Note]  
> Bu özellik, Azure bulut hizmeti sağlayıcıları (CSP) için desteği etkinleştirmez. Azure Resource Manager ile bulut dağıtım noktası dağıtımı, CSP 'nin desteklemediği klasik bulut hizmetini kullanmaya devam eder. Daha fazla bilgi için bkz. [Azure CSP 'de kullanılabilir Azure hizmetleri](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

Configuration Manager sürüm 1902 ' den başlayarak, Azure Resource Manager bulut dağıtım noktasının yeni örnekleri için tek dağıtım mekanizmasıdır. Mevcut dağıtımlar çalışmaya devam eder.<!-- 3605704 -->

Configuration Manager sürüm 1810 ve önceki sürümlerde, bulut dağıtım noktası Sihirbazı yine de bir Azure Yönetim sertifikası kullanan **Klasik hizmet dağıtımı** için seçenek sağlar. Kaynakların dağıtımını ve yönetimini basitleştirmek için, tüm yeni bulut dağıtım noktaları için Azure Resource Manager dağıtım modelini kullanın. Mümkünse, mevcut bulut dağıtım noktalarını Kaynak Yöneticisi aracılığıyla yeniden dağıtın.

> [!Important]  
> Sürüm 1810 ' den başlayarak, Azure 'daki klasik hizmet dağıtımı Configuration Manager kullanım dışıdır. Bu sürüm, bu Azure dağıtımlarını oluşturmayı desteklemeye yönelik son sürümdür. Bu işlev gelecekteki bir Configuration Manager sürümünde kaldırılacak.<!--SCCMDocs-pr issue #2993-->  

Configuration Manager var olan klasik bulut dağıtım noktalarını Azure Resource Manager dağıtım modeline geçirmez. Azure Resource Manager dağıtımlarını kullanarak yeni bulut dağıtım noktaları oluşturun ve ardından klasik bulut dağıtım noktalarını kaldırın.

### <a name="hierarchy-design"></a>Hiyerarşi tasarımı

Bulut dağıtım noktasını oluşturduğunuz yerde, hangi istemcilerin içeriğe erişmesi gerektiği üzerine bağlıdır. Sürüm 1806 ' den başlayarak, üç tür bulut dağıtım noktası bulunur:  

- Azure Resource Manager dağıtımı: Bu türü bir birincil sitede veya merkezi yönetim sitesinde oluşturun.  

- Klasik hizmet dağıtımı: Bu türü yalnızca bir birincil sitede oluşturun.  

- Bulut yönetimi ağ geçidi, istemcilere içerik de sunabilir. Bu işlevsellik, Azure VM 'lerinin gerekli sertifikalarını ve maliyetini azaltır. Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidini planlayın](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!--1358651-->  

Bulut dağıtım noktalarının sınır gruplarına eklenip eklenmeyeceğini anlamak için aşağıdaki davranışları göz önünde bulundurun:  

- Internet tabanlı istemciler sınır gruplarına bağlı değildir. Yalnızca İnternet 'e yönelik dağıtım noktalarını veya bulut dağıtım noktalarını kullanırlar. Yalnızca bu tür istemcilere hizmet vermek için bulut dağıtım noktaları kullanıyorsanız, bunları sınır gruplarına eklemeniz gerekmez.  

- İç ağınızdaki istemcilerin bir bulut dağıtım noktası kullanmasını istiyorsanız istemcilerle aynı sınır grubunda olması gerekir. İstemciler, Azure 'dan içerik indirmeyle ilişkili bir maliyet olduğundan, içerik kaynakları listesinde son olarak bulut dağıtım noktalarını önceliklendirdi. Bu nedenle, bulut dağıtım noktası genellikle intranet tabanlı istemciler için bir geri dönüş kaynağı olarak kullanılır. Önce bir bulut tasarımını istiyorsanız, bu iş gereksinimini karşılamak için sınır gruplarınızı tasarlayın. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../../servers/deploy/configure/boundary-groups.md).  

Bulut dağıtım noktalarını Azure 'un belirli bölgelerine yükleseniz de, istemciler Azure bölgelerinin farkında değildir. Rastgele bir bulut dağıtım noktası seçer. Bulut dağıtım noktalarını birden çok bölgeye yüklerseniz ve bir istemci içerik konumu listesinde birden fazla alırsa, istemci aynı Azure bölgesinden bir bulut dağıtım noktası kullanmayabilir.  

### <a name="backup-and-recovery"></a>Yedekleme ve kurtarma  

Hiyerarşinizde bir bulut dağıtım noktası kullandığınızda, yedekleme ve kurtarma için plan yapmanıza yardımcı olması için aşağıdaki bilgileri kullanın:  

- **Site Sunucusunu Yedekle** bakım görevini kullandığınızda, Configuration Manager otomatik olarak bulut dağıtım noktası için yapılandırma ekler.  

- Sunucu kimlik doğrulama sertifikasının bir kopyasını yedekleyin ve kaydedin. Klasik hizmet dağıtımını Azure 'da kullanıyorsanız, Azure yönetim sertifikasının bir kopyasını da yedekleyin ve kaydedin. Configuration Manager birincil sitesini farklı bir sunucuya geri yüklediğinizde, sertifikaları yeniden içeri aktarmanız gerekir.  


## <a name="requirements"></a><a name="bkmk_requirements"></a>Gereklilik

- Hizmeti barındırmak için bir **Azure aboneliğine** ihtiyacınız vardır.  

    - Bir **Azure yöneticisinin** , tasarımınıza bağlı olarak belirli bileşenlerin ilk oluşturmaya katılması gerekir. Bu kişi Configuration Manager izinler gerektirmez.  

- Site sunucusu, bulut hizmetini dağıtmak ve yönetmek için **İnternet erişimi** gerektirir.  

- **Azure Resource Manager** dağıtım yöntemini kullanırken, **bulut yönetimi**için Configuration Manager [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) ile tümleştirin. Azure AD *Kullanıcı keşfi* gerekli değildir.  

- **Sunucu kimlik doğrulama sertifikası**. Daha fazla bilgi için aşağıdaki [Sertifikalar](#bkmk_certs) bölümüne bakın.  

    - Karmaşıklığı azaltmak için, sunucu kimlik doğrulama sertifikası için bir ortak sertifika sağlayıcısı kullanın. Bunu yaparken, istemcilerin bulut hizmeti adını çözümlemesi için bir **DNS CNAME diğer adına** de ihtiyacınız vardır.  

- Configuration Manager sürüm 1810 veya önceki sürümlerde, klasik Azure dağıtım yöntemi kullanılıyorsa bir **Azure Yönetim sertifikasına**ihtiyacınız vardır. Daha fazla bilgi için aşağıdaki [Sertifikalar](#bkmk_certs) bölümüne bakın.  

    > [!TIP]  
    > Configuration Manager sürüm 1806 ' den başlayarak **Azure Resource Manager** dağıtım modelini kullanın. Bu yönetim sertifikası gerekmez.  
    >
    > Klasik dağıtım yöntemi 1810 sürümünden itibaren kullanımdan kaldırılmıştır.  

- **Cloud Services** grubunda, istemci ayarını, **bulut dağıtım noktalarına erişime izin ver**' i **Evet** olarak ayarlayın. Varsayılan olarak bu değer **Hayır**olarak ayarlanır.  

- İstemci cihazları için **İnternet bağlantısı**gerekir ve **IPv4**kullanılmalıdır.  


## <a name="specifications"></a><a name="bkmk_spec"></a>Lerinize

- Bulut dağıtım noktası, [istemciler ve cihazlar Için desteklenen işletim sistemlerinde](../configs/supported-operating-systems-for-clients-and-devices.md)listelenen tüm Windows sürümlerini destekler.  

- Bir yönetici, aşağıdaki desteklenen yazılım içeriği türlerini dağıtır:  
  - Uygulamalar
  - Paketler
  - İşletim sistemi yükseltme paketleri
  - Üçüncü taraf yazılım güncelleştirmeleri  

    > [!Important]  
    > - Configuration Manager konsolu, Microsoft yazılım güncelleştirmelerinin bir bulut dağıtım noktasına dağıtımını engellememesine karşın, istemcilerin desteklemediği içeriği depolamak üzere Azure maliyetleri ödeiyoruz. Internet tabanlı istemciler Microsoft Update bulut hizmetinden her zaman Microsoft yazılım güncelleştirme içeriği alır. Microsoft yazılım güncelleştirmelerini bir bulut dağıtım noktasına dağıtmayın.
    > - İçerik depolaması için bir CMG kullanırken, kullanılabilir [istemci ayarı](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) etkinleştirildiğinde **Delta içeriğini indir** , üçüncü taraf güncelleştirmeler için içerik istemcilere indirmez. <!--6598587--> 

- Sürüm 1806 ' den başlayarak bir istek temelli dağıtım noktasını bir bulut dağıtım noktasını kaynak olarak kullanacak şekilde yapılandırın. Daha fazla bilgi için bkz. [kaynak dağıtım noktaları hakkında](use-a-pull-distribution-point.md#about-source-distribution-points).<!--1321554-->  

### <a name="deployment-settings"></a>Dağıtım ayarları

- **Görev dizisini çalıştırarak içeriği gerektiğinde yerel olarak indirme**seçeneğiyle bir görev dizisi dağıttığınızda, yönetim noktası bir bulut dağıtım noktasını içerik konumu olarak içermez. İstemcilerin bir bulut dağıtım noktası kullanabilmesi için **görev sırasını başlatmadan önce tüm içeriği yerel olarak indirme** seçeneğiyle birlikte görev sırasını dağıtın.  

- Bulut dağıtım noktası, **dağıtım noktasından program çalıştırma**seçeneğiyle paket dağıtımlarını desteklemez. Dağıtım **noktasından Içerik indirmek ve yerel olarak çalıştırmak**için dağıtım seçeneğini kullanın.  

### <a name="limitations"></a>Sınırlamalar  

- PXE veya çok noktaya yayın özellikli dağıtımlar için bulut dağıtım noktası kullanamazsınız.  

- Bulut dağıtım noktası App-V akış uygulamalarını desteklemez.  

- İçeriği bir bulut dağıtım noktasında [önceden hazırlayabilirsiniz](manage-network-bandwidth.md#BKMK_PrestagingContent) . Bulut dağıtım noktasını yöneten birincil sitenin dağıtım Yöneticisi tüm içeriği aktarır.  

- Bir bulut dağıtım noktasını çekme dağıtım noktası olarak yapılandıramazsınız.  


## <a name="cost"></a><a name="bkmk_cost"></a>YT

<!--501018-->
> [!IMPORTANT]  
> Aşağıdaki maliyet bilgileri yalnızca tahmin amaçlıdır. Ortamınız, bir bulut dağıtım noktası kullanmanın genel maliyetini etkileyen başka değişkenlere sahip olabilir.  

Configuration Manager, maliyetleri denetlemeye ve veri erişimini izlemeye yardımcı olmak için aşağıdaki seçenekleri içerir:  

- Bir bulut hizmetinde depoladığınız içerik miktarını denetleyin ve izleyin. Daha fazla bilgi için bkz. [bulut dağıtım noktalarını izleme](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- İstemci indirmeleri için eşikler aylık limitleri karşılıyorsa veya aştığında sizi uyarmak için Configuration Manager yapılandırın. Daha fazla bilgi için bkz. [veri aktarımı eşik uyarıları](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts).

- İstemcilere göre bulut dağıtım noktalarından veri aktarımı sayısını azaltmaya yardımcı olmak için aşağıdaki eş önbelleğe alma teknolojilerinden birini kullanın:  
  - Configuration Manager eş önbelleği
  - Windows BranchCache
  - Windows 10 teslim Iyileştirmesi  

    Daha fazla bilgi için bkz. [içerik yönetimi Için temel kavramlar](fundamental-concepts-for-content-management.md).  

### <a name="components"></a>Bileşenler

Bulut dağıtım noktası, Azure abonelik hesabına ücretlendirieden aşağıdaki Azure bileşenlerini kullanır:  

> [!Tip]  
> Sürüm 1806 ' den başlayarak, bulut yönetimi ağ geçidi istemcilere içerik de sunabilir. Bu işlevsellik, Azure VM 'lerini birleştirerek maliyeti azaltır. Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidi Için maliyet](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost).  

#### <a name="virtual-machine"></a>Sanal makine

- Bulut dağıtım noktası, hizmet olarak platform (PaaS) olarak Azure Cloud Services kullanır. Bu hizmet, işlem maliyetlerine tabi olan sanal makineleri (VM) kullanır.  

- Her bulut dağıtım noktası hizmeti iki standart a0 VM kullanır.  

- Olası maliyetleri belirlemede yardımcı olması için bkz. [Azure Fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) .

    > [!NOTE]  
    > Sanal makine maliyetleri bölgeye göre farklılık gösterir.

#### <a name="outbound-data-transfer"></a>Giden veri aktarımı

- Azure 'daki tüm veri akışları ücretsizdir (giriş veya karşıya yükleme). Siteden bulut dağıtım noktasına içerik dağıtımı Azure 'a yükleniyor.  

- Ücretler, Azure 'dan (çıkış veya indirme) veri akışını temel alır. Azure 'dan bulut dağıtım noktası veri akışları, istemcilerin indirtığı yazılım içeriğinden oluşur.  

- Daha fazla bilgi için bkz. [bulut dağıtım noktalarını izleme](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Olası maliyetleri belirlemede yardımcı olması için bkz. [Azure bant genişliği fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/bandwidth/) . Veri aktarımı fiyatlandırması katmanlı. Ne kadar çok kullanırsanız, gigabayt başına ödeme yaparsınız.  

#### <a name="content-storage"></a>İçerik depolama

- Internet tabanlı istemciler, Microsoft yazılım güncelleştirme içeriğini Microsoft Update bulut hizmetinden ücretsiz olarak alır. Yazılım güncelleştirme dağıtım paketlerini, Microsoft yazılım güncelleştirmeleriyle bir bulut dağıtım noktasına dağıtmayın. Aksi takdirde, istemcilerin hiçbir şekilde kullanmadığı içerikler için veri depolama maliyetlerine tabi olursunuz.  

- Bulut dağıtım noktaları, dağıtım modeline bağlı olarak aşağıdaki standart BLOB depolama alanını kullanır:  

    - Azure Resource Manager dağıtımı Azure yerel olarak yedekli depolama (LRS) kullanır. Bu değişiklik, depolama hesabının maliyetini azaltır. Klasik dağıtım, GRS 'nin ek özelliklerini kullanmıyor. Daha fazla bilgi için bkz. [yerel olarak yedekli depolama](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

    - Configuration Manager sürüm 1810 veya önceki sürümleriyle klasik bir dağıtım, Azure coğrafi olarak yedekli depolama (GRS) kullanır. Daha fazla bilgi için bkz. [coğrafi olarak yedekli depolama](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

#### <a name="other-costs"></a>Diğer maliyetler

- Her bulut hizmetinin dinamik bir IP adresi vardır. Her farklı bulut dağıtım noktası yeni bir dinamik IP adresi kullanır. Bulut hizmeti başına ek VM 'Ler eklemek bu adresleri artırmaz.  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a>Bağlantı noktaları ve veri akışı

Bulut dağıtım noktası için iki birincil veri akışı vardır:  

- Site sunucusu, bulut dağıtım noktası hizmetini ayarlamak için Azure 'a bağlanır  

- İstemci, içerik indirmek için bulut dağıtım noktasına bağlanır  

### <a name="site-server-to-azure"></a>Site sunucusundan Azure 'a

Şirket içi ağınıza gelen bağlantı noktalarını açmanıza gerek yoktur. Site sunucusu, bulut hizmetini dağıtmak, güncelleştirmek ve yönetmek için Azure ile tüm iletişimi ve bulut dağıtım noktasını başlatır. Site sunucusunun Microsoft bulutuna giden bağlantılar oluşturması gerekir. Bu eylem, dağıtım noktası site sistem rolünün belirli bir siteye yüklenmesine eşdeğerdir.  

### <a name="client-to-cloud-distribution-point"></a>İstemciden buluta dağıtım noktası

Şirket içi ağınıza gelen bağlantı noktalarını açmanıza gerek yoktur. Internet tabanlı istemciler doğrudan Azure hizmeti ile iletişim kurar. Bulut dağıtım noktası kullanan iç ağınızdaki istemcilerin Microsoft bulutuna bağlanması gerekir.

İçerik konumu önceliği hakkında daha fazla bilgi edinmek ve intranet tabanlı istemciler bir bulut dağıtım noktası kullanırken, bkz. [içerik kaynağı önceliği](fundamental-concepts-for-content-management.md#content-source-priority).

İstemci, bir bulut dağıtım noktasını içerik konumu olarak kullandığında:  

1. Yönetim noktası istemciye, içerik kaynakları listesiyle birlikte bir erişim belirteci verir. Bu belirteç 24 saat için geçerlidir ve istemciye bulut dağıtım noktasına erişim sağlar.  

2. Yönetim noktası, istemcinin konum isteğine bulut dağıtım noktasının **hizmet FQDN 'si** ile yanıt verir. Bu özellik, sunucu kimlik doğrulama sertifikasının ortak adıyla aynıdır.  

    Etki alanı adınızı (örneğin, WallaceFalls.contoso.com) kullanıyorsanız, istemci ilk olarak bu FQDN 'yi çözümlemeye çalışır. İstemcilerin Azure hizmet adını çözebilmek için etki alanı internete yönelik DNS DNS 'de CNAME diğer adına ihtiyacınız vardır, örneğin: WallaceFalls.cloudapp.net.  

3. İstemci daha sonra Azure hizmet adını (örneğin, WallaceFalls.cloudapp.net) geçerli bir IP adresine çözümler. Bu yanıt, Azure 'un DNS tarafından işlenmelidir.  

4. İstemci, bulut dağıtım noktasına bağlanır. Azure Yük, sanal makine örneklerinden birine bağlantıyı dengeler. İstemci, erişim belirtecini kullanarak kendi kimliğini doğrular.  

5. Bulut dağıtım noktası istemcinin erişim belirtecinin kimliğini doğrular ve ardından istemciye Azure Storage 'da tam içerik konumunu verir.  

6. İstemci, bulut dağıtım noktasının sunucu kimlik doğrulama sertifikasına güveniyorsa, içeriği indirmek için Azure depolama 'ya bağlanır.


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a>Performans ve ölçek

<!--494872-->

Herhangi bir dağıtım noktası tasarımında olduğu gibi, aşağıdaki faktörleri göz önünde bulundurun:  

- Eş zamanlı istemci bağlantısı sayısı
- İstemcilerin indirme içeriğinin boyutu
- İş gereksinimlerinizi karşılamak için izin verilen sürenin uzunluğu

[Topoloji tasarımınıza](#bkmk_topology)bağlı olarak, istemciler belirli bir içerik için birden fazla bulut dağıtım noktası seçeneği içeriyorsa, bu bulut hizmetlerinde doğal olarak rastgele hale getirin. Yalnızca belirli bir içerik parçasını tek bir bulut dağıtım noktasına dağıtırsanız ve çok sayıda istemci bu içeriği aynı anda indirmeyi deniyorsa, bu etkinlik bu tek bulut dağıtım noktasında daha fazla yük koyar. Ek bir bulut dağıtım noktası eklemek ayrıca ayrı bir Azure Storage hizmeti içerir. İstemcinin bulut dağıtım noktası bileşenleriyle nasıl iletişim kurduğu ve içerik yüklediği hakkında daha fazla bilgi için bkz. [bağlantı noktaları ve veri akışı](#bkmk_dataflow).  

Bulut dağıtım noktası, Azure depolama 'ya ön uç olarak iki Azure VM kullanır. Bu varsayılan dağıtım çoğu müşterinin ihtiyaçlarını karşılar. Çok sayıda eş zamanlı istemci bağlantısı (örneğin, 150.000 istemci) sayesinde bazı Extreme durumlarda, Azure VM 'lerinin işleme kapasitesi istemci istekleriyle devam edemiyor. Bulut dağıtım noktası için kullanılan Azure VM 'lerini yeniden boyutlandıramazsınız. Configuration Manager içindeki bulut dağıtım noktası için sanal makine örneği sayısını yapılandıramıyorum, gerekirse bulut hizmetini Azure portal yeniden yapılandırın. El ile daha fazla sanal makine örneği ekleyin veya hizmeti otomatik olarak ölçeklendirilecek şekilde yapılandırın.

> [!Important]  
> Configuration Manager güncelleştirdiğinizde site, bulut hizmetini yeniden dağıtır. Bulut hizmetini Azure portal el ile yeniden yapılandırırsanız, örnek sayısı iki ' un varsayılan değere sıfırlanır.  

Azure depolama hizmeti, tek bir dosya için saniye başına 500 isteği destekler. Tek bir bulut dağıtım noktasının performans testi, 24 saat içinde tek 100 MB 'lık bir dosyanın 50.000 istemciye dağıtımını destekliyordu.<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a>Sertifika  

Bulut dağıtım noktası tasarımınıza bağlı olarak, bir veya daha fazla dijital sertifikaya ihtiyacınız vardır.  

### <a name="general-information"></a>Genel bilgiler

<!--SCCMDocs issue #779-->
Bulut dağıtım noktaları için sertifikalar aşağıdaki konfigürasyonları destekler:  

- 4096-bit anahtar uzunluğu

- Sürüm 3 sertifikaları. Daha fazla bilgi için bkz. [CNG sertifikalarına genel bakış](../network/cng-certificates-overview.md).  

- Sürüm 1802 ' den başlayarak, Windows 'u şu ilkeyle yapılandırdığınızda: **Sistem şifrelemesi: şifreleme, karma ve imzalama IÇIN FIPS ile uyumlu algoritmalar kullanın**  

- Sürüm 1802 ' den başlayarak, TLS 1,2 desteği. Daha fazla bilgi için bkz. [şifreleme denetimleri teknik başvurusu](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities).  

### <a name="server-authentication-certificate"></a>Sunucu kimlik doğrulama sertifikası

*Bu sertifika tüm bulut dağıtım noktası dağıtımları için gereklidir.*

Daha fazla bilgi için, bkz. [CMG Server kimlik doğrulama sertifikası](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth)ve aşağıdaki alt bölümleri gerektiği gibi:  

- CMG güvenilen kök sertifikayı istemcilere
- Ortak sağlayıcı tarafından verilen sunucu kimlik doğrulama sertifikası
- Kurumsal PKI 'dan verilen sunucu kimlik doğrulama sertifikası

Bulut dağıtım noktası, bu tür sertifikayı bulut yönetimi ağ geçidiyle aynı şekilde kullanır. İstemcilerin Ayrıca bu sertifikaya güvenmesi gerekir. Microsoft, karmaşıklığı azaltmak için genel bir sağlayıcı tarafından verilen bir sertifikanın kullanılmasını önerir.

Joker bir sertifika kullanmadığınız takdirde, aynı sertifikayı yeniden kullanmayın. Bulut dağıtım noktası ve bulut yönetimi ağ geçidinin her örneği için benzersiz bir sunucu kimlik doğrulama sertifikası gerekir.

Bu sertifikayı bir PKI 'dan oluşturma hakkında daha fazla bilgi için bkz. [bulut dağıtım noktaları için hizmet sertifikası dağıtma](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).  

### <a name="azure-management-certificate"></a>Azure Yönetim sertifikası

*Bu sertifika, klasik hizmet dağıtımları için gereklidir. Azure Resource Manager dağıtımları için gerekli değildir.*

> [!Important]  
> Configuration Manager sürüm 1806 ' den başlayarak **Azure Resource Manager** dağıtım modelini kullanın. Bu yönetim sertifikası gerekmez.  
>
> Klasik dağıtım yöntemi 1810 sürümünden itibaren kullanımdan kaldırılmıştır.  
>
> Configuration Manager sürüm 1902 ' den başlayarak, Azure Resource Manager bulut dağıtım noktasının yeni örnekleri için tek dağıtım mekanizmasıdır. Bu sertifika, Configuration Manager sürüm 1902 veya sonraki sürümlerde gerekli değildir.<!-- 3605704 -->

Configuration Manager sürüm 1810 veya önceki bir sürümü ile klasik Azure dağıtım yöntemini kullanıyorsanız bir **Azure Yönetim sertifikasına**ihtiyacınız vardır. Daha fazla bilgi için, bulut yönetimi ağ geçidi sertifikaları makalesinin [Azure Yönetim sertifikası](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt) bölümüne bakın. Configuration Manager site sunucusu, klasik dağıtımı oluşturmak ve yönetmek için Azure ile kimlik doğrulaması yapmak üzere bu sertifikayı kullanır.  

Karmaşıklığı azaltmak için tüm Azure abonelikleri ve tüm Configuration Manager siteleri genelinde tüm klasik bulut dağıtım noktaları ve bulut yönetimi ağ geçitleri dağıtımları için aynı Azure yönetim sertifikasını kullanın.


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a>Sık sorulan sorular (SSS)

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Bir istemcinin bir bulut dağıtım noktasından içerik indirmesi için bir sertifikaya ihtiyacı var mı?

İstemci kimlik doğrulama sertifikası gerekli değildir. İstemcinin, bulut dağıtım noktası tarafından kullanılan sunucu kimlik doğrulama sertifikasına güvenmesi gerekir. Bu sertifika bir ortak sertifika sağlayıcısı tarafından verildiyse, çoğu Windows cihazı Bu sağlayıcılar için güvenilen kök sertifikaları zaten içerir. Kuruluşunuzun PKI 'ınızdan bir sunucu kimlik doğrulama sertifikası verildiyse, istemcilerinizin tüm zincirde veren sertifikalara güvenmesi gerekir. Bu zincir, kök sertifika yetkilisini ve tüm ara sertifika yetkililerini içerir. PKI tasarımınıza bağlı olarak, bu sertifika bulut dağıtım noktasının dağıtımına ek karmaşıklık getirebilir. Bu karmaşıklığın önüne geçmek için, Microsoft, istemcilerinizin zaten güvendiği bir ortak sertifika sağlayıcısı kullanılmasını önerir.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Şirket içi İstemcilerim bir bulut dağıtım noktası kullanıyor mu?

Evet. İç ağınızdaki istemcilerin bir bulut dağıtım noktası kullanmasını istiyorsanız istemcilerle aynı sınır grubunda olması gerekir. İstemciler, Azure 'dan içerik indirmeyle ilişkili bir maliyet olduğundan, içerik kaynakları listesinde son olarak bulut dağıtım noktalarını önceliklendirdi. Bu nedenle, bulut dağıtım noktası genellikle intranet tabanlı istemciler için bir geri dönüş kaynağı olarak kullanılır. Önce bir bulut tasarımını istiyorsanız sınır gruplarınızı uygun şekilde tasarlayın. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../../servers/deploy/configure/boundary-groups.md).  

### <a name="do-i-need-azure-expressroute"></a>Azure ExpressRoute 'a ihtiyacım var mı?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) , şirket Içi ağınızı Microsoft bulutuna genişletmenizi sağlar. ExpressRoute veya bu tür sanal ağ bağlantıları Configuration Manager bulut dağıtım noktası için gerekli değildir.  

Kuruluşunuz ExpressRoute kullanıyorsa, ExpressRoute kullanan aboneliğden bulut dağıtım noktası için Azure aboneliğini yalıtın. Bu yapılandırma, bulut dağıtım noktasının yanlışlıkla bu şekilde bağlı olmamasını sağlar.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Azure sanal makinelerini sürdürmem gerekir mi?

Bakım gerekli değildir. Bulut dağıtım noktasının tasarımı bir hizmet olarak Azure platformu (PaaS) kullanır. Sağladığınız aboneliği kullanarak, Configuration Manager gerekli VM 'Leri, depolamayı ve ağı oluşturur. Azure, sanal makineleri güvenlik altına alır ve günceller. Bu VM 'Ler, hizmet olarak altyapı (IaaS) gibi durumlarda şirket içi ortamınızın bir parçası değildir. Bulut dağıtım noktası, Configuration Manager ortamınızı buluta genişleten PaaS 'dir. Daha fazla bilgi için bkz. [PaaS bulut hizmeti modelinin güvenlik avantajları](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>Bulut dağıtım noktası Azure CDN kullanıyor mu?

Azure Content Delivery Network (CDN), yüksek bant genişliğine sahip içeriği dünya genelinde stratejik olarak yerleştirilmiş fiziksel düğümlerde önbelleğe alarak hızlı bir şekilde sunan genel bir çözümdür. Daha fazla bilgi için bkz. [Azure CDN nedir?](https://docs.microsoft.com/azure/cdn/cdn-overview).

Configuration Manager bulut dağıtım noktası şu anda Azure CDN desteklemiyor.


## <a name="next-steps"></a>Sonraki adımlar

[Bulut dağıtım noktalarını yükler](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
