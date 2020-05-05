---
title: Site hiyerarşisi tasarlama
titleSuffix: Configuration Manager
description: Site hiyerarşinizi planlamak için Configuration Manager kullanılabilir topolojilerini ve yönetim seçeneklerini anlayın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e14cf57e962d7bc90cc39db9ecfea68d9c5b00e
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073356"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Configuration Manager için bir site hiyerarşisi tasarlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yeni bir Configuration Manager hiyerarşisinin ilk sitesini yüklemeden önce, anlaşılması iyi bir fikirdir:  

- Configuration Manager için kullanılabilir topolojiler  

- Kullanılabilir sitelerin ve bunların birbirleriyle ilişkilerinin türleri  

- Her bir site türünün sağladığı yönetim kapsamı  

- Yüklemeniz gereken site sayısını azaltabilirler içerik yönetimi seçenekleri  

Ardından, geçerli iş gereksinimlerinize etkin bir şekilde hizmet veren bir topoloji planlayın ve daha sonra gelecekteki büyümeyi yönetmek için genişletebilirsiniz.  

Planlarken, bir hiyerarşiye veya bağımsız siteye ek siteler eklemeye yönelik sınırlamalar göz önünde bulundurun:  

- Hiyerarşi için [desteklenen sayıda birincil](../configs/size-and-scale-numbers.md) siteye kadar bir merkezi yönetim sitesinin altına yeni bir birincil site yükler.  

- [Yeni bir merkezi yönetim sitesi yüklemek için tek başına birincil siteyi genişletin](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)ve daha sonra ek birincil siteleri yükleme.  

- Birincil site ve genel hiyerarşi [için desteklenen sınıra](../configs/size-and-scale-numbers.md) kadar, yeni ikincil siteleri bir birincil sitenin altına yükler.  

- İki bağımsız siteyi birleştirmek için önceden yüklenmiş bir siteyi var olan bir hiyerarşiye ekleyemezsiniz. Configuration Manager, yalnızca mevcut bir site hiyerarşisine yeni sitelerin yüklenmesini destekler.  


> [!NOTE]  
> Yeni bir Configuration Manager yüklemesi planlarken, etkin sürümlerdeki geçerli sorunları ayrıntılandıran [sürüm notlarına](../../servers/deploy/install/release-notes.md)göz önünde bulundurun. Sürüm notları tüm Configuration Manager dalları için geçerlidir. [Technical Preview dalını](../../get-started/technical-preview.md)kullanırken, Technical Preview 'un her sürümü için belgelerde bu dala özgü sorunlar bulun.  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a>Hiyerarşi topolojisi  

Hiyerarşi topolojileri aralığı:  

- En basit: tek bir tek başına birincil site  

- En karmaşık: hiyerarşinin üst düzey sitesinde merkezi yönetim sitesi olan bağlı birincil ve ikincil sitelerin bir grubu  

Hiyerarşide kullandığınız sitelerin türü ve sayısı için anahtar sürücü genellikle desteklemeniz gereken cihaz sayısı ve türüdür.   

### <a name="standalone-primary-site"></a>Tek başına birincil site

Tüm cihazların ve kullanıcıların yönetimini destekleyebileceği tek başına birincil site kullanın. Daha fazla bilgi için bkz. [boyutlandırma ve ölçek sayıları](../configs/size-and-scale-numbers.md). Bu topoloji, şirketinizin coğrafi konumları tek bir birincil site tarafından sunulabildiğinde de başarılı olur. Ağ trafiğini yönetmeye yardımcı olmak için sınır gruplarında birden çok yönetim noktası ve dikkatle planlanmış bir içerik altyapısı kullanın. Daha fazla bilgi için bkz. [içerik yönetimi için](fundamental-concepts-for-content-management.md) [sınır gruplarını](../../servers/deploy/configure/boundary-groups.md) ve temel kavramları yapılandırma.  

Bu topoloji aşağıdaki avantajları sağlar:  

- Basitleştirilmiş yönetim yükü  

- Basitleştirilmiş istemci site ataması ve kullanılabilir kaynak ve hizmet keşfi  

- Siteler arasında veritabanı çoğaltmasıyla tanıtılan olası gecikmelerin eleme  

- Tek başına birincil siteyi merkezi yönetim sitesiyle daha büyük bir hiyerarşiye genişletme seçeneği. Bu seçenek, dağıtımınızın ölçeğini genişletmek üzere yeni birincil siteler yüklemenizi sağlar.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Bir veya daha fazla alt birincil sitesi olan merkezi yönetim sitesi 

Tüm cihazlarınızın ve kullanıcılarınızın yönetimini desteklemek için birden fazla birincil siteye ihtiyacınız olduğunda bu topolojiyi kullanın. Tek bir birincil site kullanmanız gerektiğinde bu gereklidir. 

Bu topoloji aşağıdaki avantajları sağlar:  

- Hiyerarşinizin ölçeğini genişletmenizi sağlayan en fazla 25 birincil siteyi destekler.    

- Sitelerini yeniden yüklemediğiniz takdirde, her zaman merkezi yönetim sitesini kullanırsınız. Bu seçenek kalıcıdır. Bir alt birincil siteyi tek başına birincil site haline getirmek için ayıramazsınız.  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a>Bir merkezi yönetim sitesinin ne zaman kullanılacağını belirleme  

Hiyerarşi genelinde ayarları yapılandırmak ve hiyerarşideki tüm siteleri ve nesneleri izlemek için bir merkezi yönetim sitesi kullanın. Bu site türü istemcileri doğrudan yönetmez. Hiyerarşi genelinde sitelerin ve istemcilerin yapılandırılmasını içeren siteden siteye veri çoğaltmasını koordine eder.  

Aşağıdaki bilgiler merkezi yönetim sitesinin ne zaman yükleneceğine karar vermenize yardımcı olabilir:  

- Merkezi Yönetim sitesi bir hiyerarşideki en üst düzey sitedir.  

- Birden fazla birincil siteye sahip bir hiyerarşiyi yapılandırdığınızda bir merkezi yönetim sitesi yüklersiniz.  

     - İki veya daha fazla birincil siteye hemen ihtiyacınız varsa, önce merkezi yönetim sitesini yüklemeniz gerekir.  

     - Zaten bir birincil siteniz varsa ve bir merkezi yönetim sitesi yüklemek istediğinizde, merkezi yönetim sitesini yüklemek için [tek başına birincil siteyi genişletin](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) .  

- Merkezi Yönetim sitesi alt site olarak yalnızca birincil siteleri destekler.  

- Merkezi yönetim sitesine atanmış istemciler olamaz.  

- Merkezi Yönetim sitesi, yönetim noktaları ve dağıtım noktaları gibi istemcileri doğrudan destekleyen site sistemi rollerini desteklemez.  

- Hiyerarşideki tüm istemcileri yönetin ve merkezi yönetim sitesine bağlı Configuration Manager konsolundan tüm site yönetim görevlerini gerçekleştirin. Bu görevler, alt birincil veya ikincil sitelerdeki yönetim noktalarını veya diğer site sistem rollerini yüklemeyi içerir.  

- Bir merkezi yönetim sitesi kullandığınızda, hiyerarşinizdeki tüm sitelerden site verilerini görebileceğiniz tek yerdir. Bu veriler, envanter verileri ve durum iletileri gibi bilgileri içerir.  

- Hiyerarşi genelinde bulma işlemlerini merkezi yönetim sitesinden yapılandırın. Merkezi yönetim sitesinden, tek tek birincil sitelerde çalışacak bulma yöntemleri atayın.  

- Farklı yönetim kullanıcılarına farklı güvenlik rolleri, güvenlik kapsamları ve koleksiyonlar atayarak hiyerarşinin tamamında güvenliği yönetin. Bu yapılandırma hiyerarşideki her bir sitede geçerlidir.  

- Hiyerarşideki siteler arasındaki iletişimi denetlemek için çoğaltmayı yapılandırın. Site verileri için veritabanı çoğaltmasını zamanlayın ve siteler arasında dosya tabanlı verilerin aktarımı için bant genişliğini yönetin.  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a>Birincil sitenin ne zaman kullanılacağını belirleme  

İstemcileri yönetmek için birincil siteleri kullanın. Birincil siteyi bir merkezi yönetim sitesinin altına veya yeni bir hiyerarşinin ilk sitesi olarak bir alt site olarak yükler. Hiyerarşinin ilk sitesi olan bir birincil site tek başına bir birincil site oluşturur. Hem alt birincil siteler hem de tek başına birincil siteler ikincil siteleri destekler.  

Aşağıdaki nedenlerle başka birincil siteler eklemeyi göz önünde bulundurun:  

- Cihaz sayısını artırmak için tek bir hiyerarşiyle yönetin.  

- Organizasyon yönetimi gereksinimlerini karşılama. Örneğin, düşük bant genişliğine sahip bir ağda dağıtım içeriğinin aktarımını yönetmek için uzak bir konuma birincil site yükleyebilirsiniz.  

     - Bir dağıtım noktasına veri aktarırken ağ bant genişliğini azaltma seçeneklerini kullanmayı düşünün. Bu içerik yönetimi özelliği ek siteleri yüklemeye gerek gereksinimini değiştirebilir.  


Aşağıdaki bilgiler bir birincil sitenin ne zaman yükleneceğine karar vermenize yardımcı olabilir:  

- Birincil site bağımsız bir birincil site ya da büyük bir hiyerarşideki alt birincil site olabilir. Bir birincil site, merkezi yönetim sitesine sahip bir hiyerarşinin üyesiyse siteler arasındaki verileri yenilemek üzere veritabanı yinelemesi kullanılır. Tek bir birincil sitenin desteklediğinden daha fazla istemci ve cihazı desteklemeniz gerekmiyorsa, tek başına birincil site yüklemeyi düşünün. Tek başına bir birincil siteyi yükledikten sonra, daha sonra dağıtımınızı ölçeklendirmek üzere yeni bir merkezi yönetim sitesine rapor vermek için gerekliyse genişletin.  

- Birincil site, yalnızca bir merkezi yönetim sitesini üst site olarak destekler.  

- Birincil site, alt siteler olarak yalnızca ikincil siteleri destekler ve birden fazla ikincil siteyi destekler.  

- Birincil siteler, tüm istemci verilerini atanan istemcilerinden işlemekten sorumludur.  

- Birincil siteler, merkezi yönetim sitesiyle doğrudan iletişim kurmak için veritabanı çoğaltmasını kullanır. Bu davranış, yeni bir site yüklediğinde otomatik olarak yapılandırılır.  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a>İkincil bir sitenin ne zaman kullanılacağını belirleme  

İkincil siteleri, dağıtım içeriğinin ve istemci verilerinin düşük bant genişliğine sahip ağlarda aktarımını yönetmek için kullanın.  

İkincil bir siteyi bir merkezi yönetim sitesinden veya ikincil sitenin doğrudan üst birincil sitesinden yönetirsiniz. İkincil siteler bir birincil siteye iliştirilir. Bunları kaldırmadan farklı bir üst siteye taşıyamaz ve sonra yeni birincil sitenin altına alt site olarak yeniden yükleyebilirsiniz.

Ancak, dağıtım içeriğinin dosya tabanlı çoğaltmasını yönetmeye yardımcı olmak için iki eş ikincil site arasında içerik yönlendirebilirsiniz. İstemci verilerini bir birincil siteye aktarmak için ikincil site dosya tabanlı çoğaltmayı kullanır. İkincil bir site ayrıca üst birincil sitesiyle iletişim kurmak için veritabanı yinelemesi kullanır.  

Aşağıdaki koşullardan biri geçerliyse bir ikincil siteyi yüklemeyi düşünün:  

- Bir yönetici kullanıcı için yerel bağlantı noktası gerekli değildir.  

- Hiyerarşide daha düşük olan sitelere dağıtım içeriği aktarımını yönetmeniz gerekir.  

- Hiyerarşide daha yüksek olan sitelere gönderilen istemci bilgilerini yönetmeniz gerekir.  

İkincil bir site yüklemek istemiyorsanız ve uzak konumlarda istemcileriniz varsa, aşağıdaki seçenekleri göz önünde bulundurun:  

- Windows BranchCache gibi eşler arası teknolojiler kullanın  

- Bant genişliği denetimi ve zamanlama için dağıtım noktalarını etkinleştir   

Bu içerik yönetimi seçeneklerini ikincil sitelerle veya olmadan kullanın. Configuration Manager altyapınızın boyutunu azaltmaya yardımcı olurlar. Configuration Manager içerik yönetimi seçenekleri hakkında daha fazla bilgi için bkz. [içerik yönetimi seçeneklerinin ne zaman kullanılacağını belirleme](#BKMK_ChooseSecondaryorDP).  


Aşağıdaki bilgiler bir ikincil sitenin ne zaman yükleneceğine karar vermenize yardımcı olabilir:  

- SQL Server yerel bir örneği yoksa, ikincil site sunucuları, site yüklemesi sırasında SQL Server Express otomatik olarak yüklenir.  

- İkincil site yüklemesi, kurulumu doğrudan bir bilgisayarda çalıştırmak yerine Configuration Manager konsolundan başlatılır.  

- İkincil siteler, site veritabanındaki bilgilerin bir alt kümesini kullanır. Bu davranış, SQL 'in üst birincil site ile ikincil site arasında çoğaltılacağını veri miktarını azaltır.  

- İkincil siteler, dosya tabanlı içeriğin ortak bir üst birincil siteye sahip diğer ikincil sitelere yönlendirilmesini destekler.  

- İkincil site yüklemeleri, yönetim noktası ve dağıtım noktası site sistem rollerini ikincil site sunucusuna otomatik olarak yükler.  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a>İçerik yönetimi seçeneklerinin ne zaman kullanılacağını belirleme  

Uzak ağ konumlarında istemcileriniz varsa, birincil veya ikincil site yerine bir ya da daha fazla içerik yönetimi seçeneği kullanmayı deneyin. Aşağıdaki seçenekler genellikle bir site yüklemesi gereksinimini ortadan kaldırır:  

- Windows 10 için teslim Iyileştirmesi  

- Configuration Manager eş önbelleği  

- Windows BranchCache  

- Bant genişliği denetimi için dağıtım noktalarını yapılandırma  

- İçeriği dağıtım noktalarına el ile Kopyala (içeriği önceden hazırlama)  


Aşağıdaki koşullardan herhangi biri geçerliyse başka bir site yüklemek yerine bir dağıtım noktası dağıtımını göz önünde bulundurun:  

- Ağ bant genişliğiniz, uzak konumdaki istemci bilgisayarların birincil sitedeki bir yönetim noktasıyla iletişim kurması için yeterlidir. İstemciler, istemci ilkesini indirmek, envanter göndermek, raporlama durumunu göndermek ve bulma bilgilerini göndermek üzere bir yönetim noktasıyla iletişim kurar.  

- Arka Plan Akıllı Aktarım Hizmeti (BITS), ağ gereksinimleriniz için yeterli bant genişliği denetimi sağlamıyor.  

Configuration Manager içerik yönetimi seçenekleri hakkında daha fazla bilgi için bkz. [içerik yönetimi Için temel kavramlar](fundamental-concepts-for-content-management.md).  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a>Hiyerarşi topolojisinin ötesinde  

İlk hiyerarşi topolojinizle birlikte aşağıdaki soruları de göz önünde bulundurun:  

- Hangi site sistem rolleri hiyerarşideki farklı sitelerden hizmet veya özellik sağlar?  

- Altyapınızdaki hiyerarşi genelinde yapılandırmaların ve yeteneklerin nasıl yönetiyorsunuz?  


Aşağıdaki yaygın konular ayrı makalelerde ele alınmıştır. Bu bilgiler, hiyerarşi tasarımınızda etkilemek veya etkilenmesi için önemlidir:  

- [Bilgisayarları ve cihazları yönetmeye](../../clients/manage/manage-clients.md)hazırlanırken, cihazların şirket içinde, bulutta veya kullanıcıya ait cihazların (KCG) dahil olup olmadığını göz önünde bulundurun. Ayrıca, birden çok yönetim seçeneğini destekleyen cihazları nasıl yönetebileceğinizi göz önünde bulundurun. Örneğin, Configuration Manager ile Windows 10 cihazlarını yönetme veya Microsoft Intune tümleştirmesi. Daha fazla bilgi için bkz. [cihaz yönetimi çözümü seçme](../choose-a-device-management-solution.md).  

- Kullanılabilir ağ altyapınızın uzak konumlar arasındaki veri akışını nasıl etkileyebileceğini anlayın. Daha fazla bilgi için bkz. [ağ ortamınızı hazırlama](../network/configure-firewalls-ports-domains.md). Ayrıca kullanıcılarınızın ve cihazlarınızın coğrafi konumunu ve altyapınıza şirket içi ağınız veya internet üzerinden erişip erişmediğini göz önünde bulundurun.  

- Yönettiğiniz cihazlara dağıttığınız içeriği verimli bir şekilde dağıtmak için bir içerik altyapısı planlayın. Bu içerik, uygulamalar, yazılım güncelleştirmeleri veya işletim sistemleri olabilir. Daha fazla bilgi için bkz. [içeriği ve içerik altyapısını yönetme](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

- Kullanmayı planladığınız [Configuration Manager özelliklerini ve yeteneklerini](../changes/features-and-capabilities.md) saptayın. Farklı özellikler, farklı site sistem rolleri veya Windows altyapısı gerektirir. Birden çok site hiyerarşisinde, ağınızı ve sunucu kaynaklarınızın en verimli kullanımı için bunları nereye dağıtacağınıza karar verin.  

- Ortak anahtar altyapısının (PKI) kullanımı dahil olmak üzere veri ve cihazlar için güvenliği göz önünde bulundurun. Daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../network/pki-certificate-requirements.md).  


Siteye özgü yapılandırmalara yönelik olarak aşağıdaki makalelere göz atın:  

- [SMS Sağlayıcı planı](plan-for-the-sms-provider.md)  

- [Site veritabanı planlaması](plan-for-the-site-database.md)  

- [Site sistem sunucularını ve site sistem rollerini planlama](plan-for-site-system-servers-and-site-system-roles.md)  

- [Güvenliği planlama](../security/plan-for-security.md)  

- Site içinde içerik dağıtırken [Ağ bant genişliğini yönetme](manage-network-bandwidth.md)  


Siteleri ve hiyerarşileri kapsayan konfigürasyonları göz önünde bulundurun  

- Siteler ve Hiyerarşiler için [yüksek kullanılabilirlik seçenekleri](../../servers/deploy/configure/high-availability-options.md)

- [Site verilerini yayımlamak](../../servers/deploy/configure/publish-site-data.md) için [Active Directory Şemayı genişletme](../network/extend-the-active-directory-schema.md) ve siteleri yapılandırma  

- [Siteler arasında veri aktarımı](data-transfers-between-sites.md)  

- [Rol tabanlı yönetimin temelleri](../../understand/fundamentals-of-role-based-administration.md)  

- [İnternetteki istemcileri yönetme](../../clients/manage/manage-clients-internet.md)  

