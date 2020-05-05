---
title: Yüksek kullanılabilirlik
titleSuffix: Configuration Manager
description: Yüksek düzeyde kullanılabilir hizmeti koruma seçeneklerini kullanarak Configuration Manager dağıtmayı öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf8714aff7235736628d44238561eea82b896698
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073322"
---
# <a name="high-availability-options-for-configuration-manager"></a>Configuration Manager için yüksek kullanılabilirlik seçenekleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager yüksek düzeyde kullanılabilir hizmeti olan seçenekleri kullanarak nasıl dağıtılacağı açıklanır.

Aşağıdaki Configuration Manager seçenekleri yüksek kullanılabilirliği destekler:

- Pasif modda ek bir site sunucusu ile herhangi bir tek başına birincil siteyi yapılandırın.  

- Birincil sitelerde ve merkezi yönetim sitesinde site veritabanı için SQL Server Always on kullanılabilirlik grubu yapılandırın.

- Siteleri, istemcilere önemli hizmetler sağlayan birden çok site sistem rolü örneğini destekler. Örneğin, yönetim noktaları ve dağıtım noktaları.  

- Merkezi yönetim siteleri ve birincil siteler, site veritabanının yedeklemesini destekler. Site veritabanı, siteler ve istemciler için tüm konfigürasyonları depolar. Bir hiyerarşideki siteler bu yapılandırma verilerini paylaşır.  

- Yerleşik site kurtarma seçenekleri, sunucu kapalı kalma süresini azaltabilir. Bu gelişmiş seçenekler, merkezi yönetim sitesi içeren bir hiyerarşiniz olduğunda kurtarmayı basitleştirir.  

- İstemciler, normal sorunları yönetim müdahalesi olmadan otomatik olarak düzeltebilir.  

- Siteler, yöneticilerin olası sorunlara yönelik uyarıları izleyen son verileri gönderemeyecek istemciler hakkında uyarı oluşturur.  

- Configuration Manager, çeşitli yerleşik raporlar ve panolar sağlar. Sorunları ve eğilimleri, sunucu veya istemci işlemleri için sorun haline gelmeden önce belirlemek için bunları kullanın.  

Configuration Manager, neredeyse gerçek zamanlı hizmet sağlayan çeşitli özellikler içerir. Bu özellikler iş gereksinimlerinizi karşılamak için önemliyse, siteleriniz ve hiyerarşilerinizi yüksek kullanılabilirlik için planlayın ve yapılandırın. Örneğin:  

- Yeniden başlatma, Windows Defender taramaları başlatma veya uzak masaüstü gibi [istemci bildirim eylemleri](../../../clients/manage/manage-clients.md).  

- Yazılım güncelleştirmeleri ve Endpoint Protection gibi izleme özelliklerine yönelik durum tabanlı iletiler.

- [Betikler](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Configuration Manager diğer özellikleri gerçek zamanlı hizmet sağlamaz. Bu özellikler, istemci ayarları, donanım ve yazılım envanteri, yazılım dağıtımları ve uyumluluk ayarlarını içerir, ancak bunlarla sınırlı değildir. Verilerin bir süre gecikmeyle çalışmasını bekler. Kritik bir sorun olması için geçici bir hizmet kesintisini içeren çoğu senaryo olağan dışı olur. Kapalı kalma süresini en aza indirmek, işlemlerin bağımsız çalışma sınırı bakımını yapmak ve yüksek düzeyde bir hizmet sunmak için siteleriniz ve hiyerarşilerinizi yüksek kullanılabilirliğe sahip bir şekilde yapılandırın.  

Örneğin, Configuration Manager istemciler genellikle işlemler için bilinen zamanlamaları ve konfigürasyonları kullanarak olarak çalışabilen işler ve işleme için verileri siteye göndermek için zamanlamalar yapar.  

- İstemciler siteyle iletişim kuramazlar, siteyle iletişim kurabilmesi için verileri önbelleğe alırlar.  

- Siteyle iletişim kuramadığınız istemciler çalışmaya devam eder. Bu kişiler, siteyle iletişim kurabilmesi ve yeni ilkeler alabilmesi için, bilinen son zamanlamaları ve önbelleğe alınmış bilgileri kullanır. Örneğin, bir istemci, çalıştırılması veya yüklemesi gereken daha önce indirilen bir uygulamayı tutabilir.

- Site, düzenli durum güncelleştirmeleri için site sistemlerini ve istemcilerini izler. Bu bileşenler kaydettirilemeyebilir, uyarılar oluşturabilir.  

- Yerleşik raporlar, devam eden işlemler, geçmiş işlemler ve geçerli eğilimler hakkında öngörüler sağlar. Configuration Manager ayrıca, devam eden işlemler için neredeyse gerçek zamanlı bilgiler sağlayan durum tabanlı iletileri destekler.  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a>Siteler ve Hiyerarşiler için yüksek kullanılabilirlik  

### <a name="use-a-site-server-in-passive-mode"></a>Pasif modda site sunucusu kullanma

Tek başına birincil site için *Pasif* modda ek bir site sunucusu yükleme. Pasif modda site sunucusu, mevcut site sunucunuza *etkin* modda ek olarak bulunur. Pasif moddaki bir site sunucusu, gerektiğinde hemen kullanılmak üzere kullanılabilir. Daha fazla bilgi için bkz. [site sunucusu yüksek kullanılabilirlik](site-server-high-availability.md).  

### <a name="use-a-remote-content-library"></a>Uzak içerik kitaplığı kullanma

Sitenin içerik kitaplığını yüksek oranda kullanılabilir depolama alanı sağlayan uzak bir konuma taşıyın. Bu özellik, site sunucusu yüksek kullanılabilirlik için bir gereksinimdir. Daha fazla bilgi için bkz. [içerik kitaplığı](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="centralize-content-sources"></a>İçerik kaynaklarını merkezileştirme

Configuration Manager ' deki tüm yazılım içerikleri, ağda bir paket kaynak konumu gerektirir. Tüm içerikler için ortak bir paket kaynak konumunu barındırmak üzere merkezi ve yüksek oranda kullanılabilir depolama alanı kullanın.

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Site veritabanını barındırmak için SQL Server Always on kullanılabilirlik grubu kullanma

Site veritabanını birincil sitelerde ve merkezi yönetim sitesinde SQL Server Always on kullanılabilirlik gruplarında barındırın. Daha fazla bilgi için, [yüksek oranda kullanılabilir site veritabanı için SQL Server her zaman açık ' a](sql-server-alwayson-for-a-highly-available-site-database.md)bakın.  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Site veritabanını barındırmak için SQL Server kümesi kullanma

Bir merkezi yönetim sitesinde veya birincil sitede veritabanı için SQL Server kümesi kullandığınızda, SQL Server yerleşik olarak bulunan yük devretme desteğini kullanırsınız.  

İkincil siteler SQL Server kümesini kullanamaz ve site veritabanlarının yedeklemesini veya geri yüklenmesini desteklemez. İkincil siteyi üst birincil sitesinden yeniden yükleyerek bir ikincil siteyi kurtarın.  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Bir merkezi yönetim sitesi ve bir veya daha fazla alt birincil site içeren bir site hiyerarşisi dağıtın

Bu yapılandırma, siteleriniz ağınızın çakışan segmentlerini yönettiğinizde hata toleransı sağlayabilir. Ayrıca, kurtarılan sitedeki site veritabanını yeniden oluşturmak için başka bir sitede bulunan paylaşılan veritabanında bulunan bilgileri kullanmak üzere ek bir kurtarma seçeneği sunar. Başarısız olan sitenin veritabanının başarısız veya kullanılamaz bir yedeklemesini değiştirmek için bu seçeneği kullanın.  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Merkezi Yönetim sitelerinde ve birincil sitelerde düzenli yedeklemeler oluşturma

Düzenli bir site yedeklemesi oluşturup test ettiğinizde, bir siteyi kurtarmak için gerekli verilere sahip olduğunuzdan emin olur. Ayrıca, bir siteyi en az bir süre içinde kurtararak da alıştırma yapabilirsiniz.  

### <a name="install-multiple-instances-of-site-system-roles"></a>Site sistemi rollerinin birden çok örneğini yükler

Kritik site sistemi rollerinin birden çok örneğini yüklediğinizde, istemciler için gereksiz iletişim noktaları sağlarsınız. Örneğin, birden çok yönetim noktası ve dağıtım noktası, belirli bir sunucunun çevrimdışı olduğu olayda yedekli hizmet sağlar.  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Bir siteye SMS sağlayıcısının birden çok örneğini yükler

SMS sağlayıcısı, bir veya daha fazla Configuration Manager konsolu için yönetim iletişim noktası sağlar. Site ve hiyerarşinizi yönetmek üzere iletişim noktaları için artıklık sağlamak üzere birden çok SMS sağlayıcısı kurun.  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a>Site sistemi rolleri için yüksek kullanılabilirlik

Her sitede, istemcilerin bu sitede kullanmasını istediğiniz hizmetleri sağlamak için site sistemi rolleri dağıtırsınız. Site veritabanı, site ve tüm istemciler için yapılandırma bilgilerini içerir. Site veritabanının yüksek oranda kullanılabilirliğini sağlamak için kullanılabilir seçeneklerden birini veya daha fazlasını kullanın ve gerekirse site ve site veritabanını kurtarın.  

### <a name="redundancy-for-important-site-system-roles"></a>Önemli site sistem rolleri için artıklık

- Uygulama Kataloğu Web hizmet noktası  

- Uygulama Kataloğu web sitesi noktası  

- Dağıtım noktası  

- Yönetim noktası  

- Yazılım güncelleştirme noktası  

- Durum Geçiş noktası  

Siteler ve istemcilerde raporlama için artıklık sağlamak üzere, Raporlama Hizmetleri noktasının birden çok örneğini yükler.

Yazılım güncelleştirme noktası ile yük devretme desteği için Windows PowerShell 'i kullanarak bu rolü bir Windows Ağ Yükü Dengeleme (NLB) kümesine yükleyin.  

### <a name="built-in-site-backup"></a>Yerleşik site yedeklemesi

Configuration Manager, sitenizi ve kritik bilgilerinizi düzenli bir zamanlamaya göre yedeklemenize yardımcı olacak yerleşik bir yedekleme görevi içerir. Ayrıca, Configuration Manager Kurulum Sihirbazı, bir siteyi işlemlere geri yüklemenize yardımcı olmak için site geri yükleme eylemlerini destekler.  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Active Directory Etki Alanı Hizmetlerine ve DNS'e Yayımlama

Her siteyi, site hakkındaki verileri Active Directory Domain Services ve DNS 'ye yayımlamak üzere yapılandırın. Bu yayımlama, istemcilerin ağ üzerinde en fazla erişilebilir sunucuyu belirlemesine olanak sağlar. İstemciler, yönetim noktaları gibi önemli hizmetleri sağlamak için yeni site sistemi sunucularının ne zaman kullanılabilir olduğunu belirlemek için de kullanır.  

### <a name="sms-provider-and-configuration-manager-console"></a>SMS sağlayıcısı ve Configuration Manager konsolu

Configuration Manager, konsol için birden çok erişim noktası olarak ayrı sunuculara birden çok SMS sağlayıcısı yüklemeyi destekler. Bir SMS sağlayıcı sunucusu çevrimdışıysa, siteleri ve istemcileri görüntülemeye ve yönetmeye devam edebilirsiniz.  

Bir Configuration Manager konsolu bir siteye bağlandığı zaman, bu sitedeki SMS sağlayıcısı örneğine bağlanır. SMS sağlayıcısının örneği rastgele seçilir. Seçilen SMS sağlayıcısı kullanılabilir değilse, aşağıdaki seçeneklere sahip olursunuz:  

- Konsolu siteye yeniden bağlayın. Her yeni bağlantı isteği, SMS sağlayıcısı 'nın bir örneğini rastgele atanır. Yeni bağlantıya kullanılabilir bir örnek atanması mümkündür.  

- Konsolunu farklı bir Configuration Manager sitesine bağlayın ve yapılandırmayı bu bağlantıdan yönetin. Bu seçenek birkaç dakikadan fazla olmayan yapılandırma değişikliklerinin hafif bir gecikmesini tanıtır. Site için SMS sağlayıcısı çevrimiçi olduktan sonra, Configuration Manager konsolunuzu doğrudan yönetmek istediğiniz siteye yeniden bağlayın.  

Configuration Manager konsolunu yöneticiler tarafından kullanılmak üzere birden çok bilgisayara yüklemeyin. Her SMS sağlayıcısı, birden çok konsoldan gelen bağlantıları destekler.  

### <a name="management-point"></a>Yönetim noktası

Her birincil siteye birden fazla yönetim noktası yükler ve sitelerin Active Directory altyapınıza ve DNS 'ye site verileri yayımlamasını etkinleştirin.  

Çoklu yönetim noktaları, tek bir yönetim noktasının kullanımını birden çok istemci tarafından yük dengelemeye yardımcı olur. Ayrıca yönetim noktaları için bir veya daha fazla veritabanı çoğaltması yüklemeyi göz önünde bulundurun. Bu yapılandırma, yönetim noktasının işlemci yoğunluklu işlemlerini azaltır. Ayrıca, bu kritik site sistem rolünün kullanılabilirliğini de artırır.  

İkincil siteler yalnızca, ikincil site sunucusunda bulunması gereken bir yönetim noktasının yüklenmesini destekler. İkincil sitelerdeki yönetim noktaları, yüksek oranda kullanılabilir bir yapılandırmaya sahip olduğu kabul edilmez.  

> [!NOTE]  
> Şirket içi mobil cihaz yönetimi tarafından yönetilen cihazlar birincil sitede yalnızca bir yönetim noktasına bağlanır. Yönetim noktası, kayıt sırasında mobil cihaza Configuration Manager atanır ve sonra değişmez. Birden çok yönetim noktası yüklediğinizde ve mobil cihazlar için birden fazla etkinleştirdiğinizde, bir mobil cihaz istemcisine atanan yönetim noktası belirleyici değildir.  
>
> Bir mobil aygıt istemcisinin kullandığı yönetim noktası kullanılamaz hale gelirse, bu yönetim noktasıyla ilgili sorunu gidermeniz veya mobil cihazı silip mobil cihaz için etkinleştirilen bir işletimsel yönetim noktasına atanabilmesi için mobil cihazı yeniden kaydetmeniz gerekir.  

### <a name="distribution-point"></a>Dağıtım noktası

Birden çok dağıtım noktası yükleyip içeriği birden çok dağıtım noktasına dağıtın. İstemcilerin içerik isteğinde çeşitli seçenekler almasını sağlamak için sınır grubu başına birden fazla dağıtım noktası ekleyin. Sınır grubu ilişkilerini, başka bir sınır grubuna veya bulut dağıtım noktasına öngörülebilir bir geri dönüş davranışına sahip olacak şekilde yapılandırın. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](boundary-groups.md).  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Uygulama Kataloğu Web hizmet noktası ve Uygulama Kataloğu web sitesi noktası

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Her site sistem rolünün birden fazla örneğini yükler. En iyi performans için, her biri aynı site sistemi sunucusunda bir tane dağıtın.  

Her uygulama Kataloğu site sistemi rolü, hiyerarşideki konumundan bağımsız olarak bu rolün diğer örnekleriyle aynı bilgileri sağlar. Bir istemci uygulama kataloğu için bir istek yaptığında ve istemcileri varsayılan uygulama Kataloğu web sitesi noktasını otomatik olarak algılayacak şekilde yapılandırmışsanız, istemci kullanılabilir bir örneğe yönlendirilir. İstemciler, istemcinin geçerli ağ konumuna bağlı olarak yerel uygulama kataloğu örneklerini tercih eder.  

Bu istemci ayarı ve otomatik algılamanın nasıl çalıştığı hakkında daha fazla bilgi için [Bilgisayar Aracısı](../../../clients/deploy/about-client-settings.md#computer-agent) istemci ayarları ' na bakın.  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a>İstemciler için yüksek kullanılabilirlik  

### <a name="client-operations-are-autonomous"></a>İstemci işlemleri otonom

Configuration Manager Client bağımsız çalışma sınırı aşağıdaki davranışları içerir:  

- İstemciler belirli site sistemi sunucularıyla sürekli iletişim gerektirmez. Önceden yapılandırılmış eylemleri bir zamanlamaya göre gerçekleştirmek için bilinen yapılandırmaların kullanılması.  

- İstemciler, istemcilere hizmet sağlayan bir site sistem rolünün herhangi bir kullanılabilir örneğini kullanabilir. Kullanılabilir bir sunucuyu bulana kadar bilinen sunucularla iletişim kurmayı dener.  

- İstemciler, site sistem sunucularıyla doğrudan kişiden bağımsız olarak envanteri, yazılım dağıtımlarını ve benzer zamanlanmış eylemleri çalıştırabilir.  

- Bir geri dönüş durum noktası kullanmak üzere yapılandırılmış istemciler, bir yönetim noktasıyla iletişim kuramadıklarında ayrıntıları geri dönüş durum noktasına gönderebilir.  

### <a name="clients-can-repair-themselves"></a>İstemciler kendilerini onarabilir

İstemciler doğrudan yönetim müdahalesi olmadan en yaygın sorunları otomatik olarak düzeltir.  

- Düzenli aralıklarla, istemciler durumlarını kendisi değerlendirmelidir. Bunlar, onarım için yerel bir düzeltme adımları ve kaynak dosyalar önbelleği kullanarak tipik sorunları düzeltmek için işlem görür.  

- Bir istemci, sitesine durum bilgilerini gönderemediğinde, site bir uyarı oluşturabilir. Bu uyarıları alan yönetici kullanıcılar, istemcinin normal işlemini geri yüklemek için anında işlem gerçekleştirebilir.  

### <a name="clients-cache-information-to-use-in-the-future"></a>İstemciler gelecekte kullanmak üzere bilgileri önbelleğe al

İstemci bir yönetim noktasıyla iletişim kurduğunda, istemci aşağıdaki bilgileri alabilir ve önbelleğe alabilir:  

- İstemci ayarları  

- İstemci zamanlamaları  

- Dağıtım Bu eylem için yapılandırıldığında, yazılım dağıtımları ve istemcinin yüklenmek üzere zamanlandığı yazılım ile ilgili bilgiler.  

İstemci bir yönetim noktasıyla iletişim kuramazlar, istemciler durum, durum ve istemci bilgilerini siteye raporlarsa yerel olarak önbelleğe alırlar. İstemci, bir yönetim noktasıyla iletişim kurduktan sonra bu verileri aktarır.  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>İstemci, bir geri dönüş durum noktasına durum gönderebilir

Bir istemciyi geri dönüş durum noktası kullanmak üzere yapılandırdığınızda, istemcinin, işlemi hakkında önemli ayrıntıları göndermesi için ek bir iletişim noktası sağlarsınız. Geri dönüş durum noktası kullanmak üzere yapılandırılmış istemciler, istemci bir yönetim noktasıyla iletişim kuramasa bile bu site sistem rolüne işlemleri hakkında durum gönderme işlemine devam eder.  

### <a name="central-management-of-client-data-and-client-identity"></a>İstemci verilerinin ve istemci kimliğinin merkezi yönetimi

Site veritabanı, bireysel istemci yerine, her bir istemcinin kimliği hakkındaki önemli bilgileri korur ve bu verileri belirli bir bilgisayar veya kullanıcıyla ilişkilendirir.  

- Bilgisayardaki istemci kaynak dosyaları, istemcinin yüklendiği bilgisayarın geçmiş kayıtlarını etkilemeden kaldırılabilir ve yeniden yüklenebilir.  

- İstemci bilgisayarda hata olması, veritabanında depolanan bilgilerin bütünlüğünü etkilemez. Bu bilgiler raporlama için kullanılabilir olmaya devam edebilir.  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a>Yüksek oranda kullanılabilir olmayan siteler ve site sistem rolleri için seçenekler

Birçok site sistemi, bir sitede veya hiyerarşide birden çok örneği desteklemez. Bu bilgiler, çevrimdışı duruma giderek bu site sistemlerine hazırlanmanıza yardımcı olabilir.  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Varlık yönetim bilgileri eşitleme noktası (hiyerarşi)

Bu site sistemi rolü, görev açısından kritik olarak kabul edilmez ve Configuration Manager isteğe bağlı işlevsellik sağlar. Bu site sistemi çevrimdışı kalırsa, aşağıdaki seçeneklerden birini kullanın:  

- Site sisteminin çevrimdışı olma nedenini çözümleyin.  

- Geçerli sunucudan rolü kaldırın ve rolü yeni bir sunucuya yükler.  

### <a name="endpoint-protection-point-hierarchy"></a>Endpoint Protection noktası (hiyerarşi)

Bu site sistemi rolü, görev açısından kritik olarak kabul edilmez ve Configuration Manager isteğe bağlı işlevsellik sağlar. Bu site sistemi çevrimdışı kalırsa, aşağıdaki seçeneklerden birini kullanın:  

- Site sisteminin çevrimdışı olma nedenini çözümleyin.  

- Geçerli sunucudan rolü kaldırın ve rolü yeni bir sunucuya yükler.  

### <a name="enrollment-point-site"></a>Kayıt noktası (site)

Bu site sistemi rolü, görev açısından kritik olarak kabul edilmez ve Configuration Manager isteğe bağlı işlevsellik sağlar. Bu site sistemi çevrimdışı kalırsa, aşağıdaki seçeneklerden birini kullanın:  

- Site sisteminin çevrimdışı olma nedenini çözümleyin.  

- Geçerli sunucudan rolü kaldırın ve rolü yeni bir sunucuya yükler.  

### <a name="enrollment-proxy-point-site"></a>Kaydolma proxy noktası (site)

Bu site sistemi rolü, görev açısından kritik olarak kabul edilmez ve Configuration Manager isteğe bağlı işlevsellik sağlar. Ancak, bu site sistem rolünün birden fazla örneğini bir siteye ve hiyerarşideki birden çok siteye yükleyebilirsiniz. Bu site sistemi çevrimdışı kalırsa, aşağıdaki seçeneklerden birini kullanın:  

- Site sisteminin çevrimdışı olma nedenini çözümleyin.  

- Geçerli sunucudan rolü kaldırın ve rolü yeni bir sunucuya yükler.  

Bir sitede birden fazla kayıt proxy sunucunuz olduğunda, sunucu adı için bir DNS diğer adı kullanın. Bu yapılandırmayı kullandığınızda, DNS hepsini bir kez deneme, kullanıcıların mobil cihazlarını kaydetmeleri sırasında bazı hata toleransı ve yük dengelemesi sağlar.  

### <a name="fallback-status-point-site-or-hierarchy"></a>Geri dönüş durum noktası (site veya hiyerarşi)

Bu site sistemi rolü, görev açısından kritik olarak kabul edilmez ve Configuration Manager isteğe bağlı işlevsellik sağlar. Bu site sistemi çevrimdışı kalırsa, aşağıdaki seçeneklerden birini kullanın:  

- Site sisteminin çevrimdışı olma nedenini çözümleyin.  

- Geçerli sunucudan rolü kaldırın ve rolü yeni bir sunucuya yükler. İstemci yüklemesi sırasında istemcilere geri dönüş durum noktası atandığından, mevcut istemcileri yeni site sistem sunucusunu kullanacak şekilde değiştirmeniz gerekir.  

### <a name="service-connection-point-hierarchy"></a>Hizmet bağlantı noktası (hiyerarşi)

Bu site sistemi rolü güncel dalı güncel Configuration Manager tutmak için kritik olsa da genellikle sık kullanılmaz. Bu sistem çevrimdışı kalırsa, aşağıdaki seçeneklerden birini kullanın:

- Site sisteminin çevrimdışı olma nedenini çözümleyin.  

- Geçerli sunucudan rolü kaldırın ve rolü yeni bir sunucuya yükler.  


## <a name="see-also"></a>Ayrıca bkz.

- [Desteklenen yapılandırmalar](../../../plan-design/configs/supported-configurations.md)  

- [Önerilen donanım](../../../plan-design/configs/recommended-hardware.md)  

- [Site sistem sunucuları için desteklenen işletim sistemleri](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Site ve site sistemi önkoşulları](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Site hatası etkileri](../../manage/site-failure-impacts.md)  
