---
title: Konsol içi güncelleştirmeler
titleSuffix: Configuration Manager
description: Microsoft bulutundaki Configuration Manager güncelleştirmeleri yüklemesi
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fee0cdf72ae8975d26bebd4da765941116421c25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713838"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Configuration Manager için konsol içi güncelleştirmeleri yükler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager güncelleştirmeleri almak için Microsoft bulut hizmeti ile eşitlenir. Sonra bu güncelleştirmeleri Configuration Manager konsolundan yüklersiniz.

## <a name="get-available-updates"></a>Kullanılabilir güncelleştirmeleri alma

Site yalnızca altyapınız ve sürümünüz için uygulanan güncelleştirmeleri indirir. Bu eşitleme, hiyerarşinizin hizmet bağlantı noktasını nasıl yapılandırdığınıza bağlı olarak otomatik veya manuel olabilir:

- **Çevrimiçi modda**, hizmet bağlantı noktası Microsoft bulut hizmetine otomatik olarak bağlanır ve ilgili güncelleştirmeleri yükler.  

    Varsayılan olarak, Configuration Manager her 24 saatte bir yeni güncelleştirmeleri denetler. Configuration Manager konsolundaki güncelleştirmeleri el ile denetleyin. **Yönetim** çalışma alanına gidin, **güncelleştirmeler ve bakım** düğümünü seçin ve Şeritteki **Güncelleştirmeleri denetle** ' yi seçin.  

- **Çevrimdışı modda**, hizmet bağlantı noktası Microsoft bulut hizmetine bağlanmaz. Kullanılabilir güncelleştirmeleri indirmek ve sonra içeri aktarmak için [hizmet bağlantı aracını kullanın](use-the-service-connection-tool.md).  

> [!NOTE]  
> Gerekirse, bant dışı düzeltmeleri konsolunuza alın. Bunu yapmak için [güncelleştirme kayıt aracını](use-the-update-registration-tool-to-import-hotfixes.md)kullanın. Bu bant dışı düzeltmeler, Microsoft bulut hizmetiyle eşitlerken aldığınız güncelleştirmeleri tamamlar.  

Güncelleştirmeler eşitlendikten sonra, bunları Configuration Manager konsolunda görüntüleyin. **Yönetim** çalışma alanına gidin ve **güncelleştirmeler ve bakım** düğümünü seçin.  

- Yüklediğiniz güncelleştirmeler **kullanılabilir**olarak görüntülenir.  

- Yüklediğiniz güncelleştirmeler **yüklü**olarak görüntülenir. Yalnızca en son yüklenen güncelleştirme gösterilir. Daha önce yüklenen güncelleştirmeleri görüntülemek için şeritte **Geçmiş** ' i seçin.  

Hizmet bağlantı noktasını yapılandırmadan önce, ek kullanımları anlayın ve planlayın. Aşağıdaki kullanımlar, bu site sistemi rolünü nasıl yapılandırabileceğini etkileyebilir:  

- Site, sitenizin kullanım bilgilerini karşıya yüklemek için hizmet bağlantı noktasını kullanır. Bu bilgiler, geçerli altyapı sürümünüz için mevcut güncelleştirmelerin Microsoft bulut hizmeti tarafından belirlenmesini sağlar. Daha fazla bilgi için bkz. [Tanılama ve kullanım verileri](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Güncelleştirmeler indirildiğinde ne olacağını daha iyi anlamak için aşağıdaki akış çizelgeleriyle bakın:  

- [Akış Grafiği - Güncelleştirmeleri indir](download-updates-flowchart.md)  

- [Akış Çizelgesi - Çoğaltmayı güncelleştirme](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Güncelleştirmeleri ve özellikleri görüntüleme ve Yönetme izinlerini atama

Konsolunda güncelleştirmeleri görüntülemek için, kullanıcının güvenlik sınıfı **güncelleştirme paketlerini**içeren rol tabanlı bir yönetim güvenlik rolüne sahip olması gerekir. Bu sınıf, Configuration Manager konsolundaki güncelleştirmeleri görüntüleme ve yönetme erişimine izin verir.

### <a name="about-the-update-packages-class"></a>Güncelleştirme paketleri sınıfı hakkında

Varsayılan olarak, **güncelleştirme paketleri** sınıfı (SMS_CM_Updatepackages) listelenen izinlere sahip aşağıdaki yerleşik güvenlik rollerinin bir parçasıdır:  

- **Değiştirme** ve **Okuma** izinlerine sahip **Tam Yönetici** :  

  - Bu güvenlik rolüne sahip ve **Tüm** güvenlik kapsamına erişimi olan bir kullanıcı güncelleştirmeleri görüntüleyebilir ve yükleyebilir. Ayrıca, Kullanıcı yükleme sırasında özellikleri etkinleştirebilir ve site güncelleştirmelerinden sonra tek tek özellikleri etkinleştirebilir.  

  - Bu güvenlik rolüne sahip ve **varsayılan** güvenlik kapsamına erişimi olan bir kullanıcı güncelleştirmeleri görüntüleyebilir ve yükleyebilir. Kullanıcı ayrıca yükleme sırasında özellikleri etkinleştirebilir ve site güncelleştirmelerinden sonra özellikleri görüntüleyebilir. Ancak bu kullanıcı, site güncelleştirildikten sonra özellikleri etkinleştiremez.  

- **Okuma** izinlerine sahip **Salt Okunur Çözümleyici** :  

  - Bu güvenlik rolüne sahip ve **varsayılan** kapsama erişimi olan bir kullanıcı güncelleştirmeleri görüntüleyebilir, ancak yüklemez. Bu Kullanıcı ayrıca, site güncelleştirmelerinden sonra özellikleri görüntüleyebilir, ancak etkinleştirebilirler.  

### <a name="permissions-required-for-updates-and-servicing"></a>Güncelleştirmeler ve bakım için gereken izinler

- Hem **değiştirme** hem de **okuma** izinlerine sahip **güncelleştirme paketleri** sınıfını içeren bir güvenlik rolü atadığınız bir hesap kullanın.  

- Hesabı **varsayılan** kapsama atayın.  

### <a name="permissions-to-only-view-updates"></a>Yalnızca güncelleştirmeleri görüntülemek için izinler

- Yalnızca **okuma** Iznine sahip **güncelleştirme paketleri** sınıfını içeren bir güvenlik rolü atadığınız bir hesap kullanın.  

- Hesabı **varsayılan** kapsama atayın.  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Site güncelleştirmelerinden sonra özellikleri etkinleştirmek için gereken izinler

- Hem **değiştirme** hem de **okuma** izinlerine sahip **güncelleştirme paketleri** sınıfını içeren bir güvenlik rolü atadığınız bir hesap kullanın.  

- Hesabı **Tüm** kapsama atayın.  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Konsol içi bir güncelleştirmeyi yüklemeden önce  

Configuration Manager konsolundan bir güncelleştirmeyi yüklemeden önce aşağıdaki adımları gözden geçirin.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> 1. Adım: Güncelleştirme denetim listesini inceleyin  

Güncelleştirme başlamadan önce gerçekleştirilecek eylemler için geçerli güncelleştirme denetim listesini gözden geçirin:

- [Güncelleştirme 2002’yi yüklemek için denetim listesi](checklist-for-installing-update-2002.md)

- [Güncelleştirme 1910’u yüklemek için denetim listesi](checklist-for-installing-update-1910.md)  

- [Güncelleştirme 1906’yı yüklemek için denetim listesi](checklist-for-installing-update-1906.md)  

- [Güncelleştirme 1902’yı yüklemek için denetim listesi](checklist-for-installing-update-1902.md)

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a>2. Adım: bir güncelleştirmeyi yüklemeden önce Önkoşul denetleyicisini çalıştırma  

Bir güncelleştirmeyi yüklemeden önce o güncelleştirmenin önkoşul denetimini çalıştırmayı deneyin. Bir güncelleştirmeyi yüklemeden önce önkoşulu çalıştırırsanız:  

- Site, güncelleştirmeyi yüklemeden önce güncelleştirme dosyalarını diğer sitelere çoğaltır.  

- Güncelleştirmeyi yüklemeyi seçtiğinizde, önkoşul denetimi otomatik olarak yeniden çalışır.  

> [!NOTE]  
> Bir önkoşul denetimi başlatıp durumu görüntülediğinizde, **yükleme** aşaması etkin olarak görünür. Ancak, site gerçekten güncelleştirmeyi yüklememez. Önkoşul denetimini çalıştırmak için, güncelleştirme işlemi paketi içerik kitaplığından ayıklar. Ardından, paketi geçerli önkoşul denetimlerine erişebilen bir hazırlama klasörüne koyar. Bir güncelleştirme yüklediğinizde, aynı işlem çalışır. Bu davranış, yükleme aşamasının **devam ediyor**gibi gösterdiği nedendir. Yükleme kategorisinde yalnızca *güncelleştirme paketi Ayıkla* adımı gösterilir.  

Daha sonra, güncelleştirmeyi yüklediğinizde, güncelleştirmeyi önkoşul denetimi uyarılarını yoksayacak şekilde yapılandırabilirsiniz.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Güncelleştirmeyi yüklemeden önce önkoşul denetleyiciyi çalıştırmak için  

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **güncelleştirmeler ve bakım** düğümünü seçin.  

2. Önkoşul denetimini çalıştırmak istediğiniz güncelleştirme paketini seçin.  

3. Şeritte **Önkoşul denetimini Çalıştır** ' ı seçin.  

    Önkoşul denetimini çalıştırdığınızda, güncelleştirmenin içeriği alt sitelere çoğaltılır. İçeriğin başarıyla çoğaltıldığını doğrulamak için site sunucusunda **Distmgr. log dosyasına** bakın.  

4. Önkoşul denetiminin sonuçlarını görüntülemek için:  

    1. Configuration Manager konsolunda **izleme** çalışma alanına gidin.  

    2. **Güncelleştirmeler ve bakım durumu** düğümünü seçin ve önkoşul durumunu arayın.  

    3. Daha fazla bilgi için site sunucusunda **ConfigMgrPrereq. log dosyasına** bakın.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a>Konsol içi güncelleştirmeleri yükler  

Configuration Manager konsolundan güncelleştirme yüklemeye hazırsanız, hiyerarşinizin en üst düzey sitesiyle başlayın. Bu site, merkezi yönetim sitesi ya da tek başına birincil sitedir.  

İş işlemlerinde etkiyi en aza indirmek için, güncelleştirmeyi her bir site için normal iş saatleri dışında indirin. Güncelleştirme yüklemesi, site bileşenlerini ve site sistem rollerini yeniden yükleme gibi eylemler içerebilir.  

- Alt birincil siteler güncelleştirmeyi, merkezi yönetim sitesi güncelleştirmeyi yüklemeyi tamamladıktan sonra otomatik olarak başlatır. Bu işlem varsayılan olarak ve önerilir. Birincil bir sitenin güncelleştirmeleri ne zaman yüklediğini denetlemek için, [site sunucuları Için hizmet pencerelerini](service-windows.md)kullanın.  

- Birincil üst site güncelleştirmesi tamamlandıktan sonra, ikincil siteleri Configuration Manager konsolunun içinden el ile güncelleştirin. İkincil site sunucularının otomatik güncelleştirilmesi desteklenmiyor.  

- Site güncelleştirildikten sonra bir Configuration Manager konsolu kullandığınızda, konsolunu güncelleştirmeniz istenir.  

- Site sunucusu bir güncelleştirmeyi yüklemeyi başarıyla tamamladıktan sonra, ilgili tüm site sistem rollerini otomatik olarak güncelleştirir. Ancak, tüm dağıtım noktaları aynı anda yeniden yüklenmez ve güncelleştirme için çevrimdışı duruma geçer. Bunun yerine, site sunucusu, güncelleştirmeyi tek seferde bir dağıtım noktaları alt kümesine dağıtmak için sitenin içerik dağıtım ayarlarını kullanır. Sonuç olarak, güncelleştirmeyi yüklemek için yalnızca bazı dağıtım noktaları çevrimdışı olur. Güncelleştirmeye başlamış veya güncelleştirmeyi tamamlamış olan dağıtım noktaları çevrimiçi kalır ve istemcilere içerik sağlayabilir.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Konsol içi güncelleştirme yüklemeye genel bakış  

#### <a name="1-when-the-update-installation-starts"></a>1. Güncelleştirme yüklemesi başladığında

Güncelleştirme, güncelleştirmenin geçerli olduğu ürün alanlarının bir listesini görüntüleyen güncelleştirmeler Sihirbazı ile karşılaşırsınız.  

- Sihirbazın **genel** sayfasında, **Önkoşul uyarılarını** gerektiği şekilde yapılandırın:  

  - Önkoşul hataları güncelleştirme yüklemesini her zaman durdurur. Güncelleştirme yüklemesini başarıyla yeniden denemeden önce hataları düzeltir. Daha fazla bilgi için bkz. [başarısız bir güncelleştirme yüklemesini yeniden deneme](#bkmk_retry).  

  - Önkoşul uyarıları, ayrıca, güncelleştirme yüklemesini durdurabilir. Güncelleştirme yüklemesini yeniden denemeden önce uyarıları onarın. Daha fazla bilgi için bkz. [başarısız bir güncelleştirme yüklemesini yeniden deneme](#bkmk_retry).  

  - **Önkoşul denetimi uyarılarını yoksay ve eksik gereksinimlere bakılmaksızın bu güncelleştirmeyi yükler**: güncelleştirme yüklemesi için önkoşul uyarılarını yoksaymak üzere bir koşul ayarlayın. Bu seçenek, güncelleştirme yüklemesinin devam etmesine izin verir. Bu seçeneği seçmezseniz, işlem bir uyarıyla karşılaştığında güncelleştirme yüklemesi duraklar. Bir site için önkoşul denetimini ve düzeltilmiş önkoşul uyarılarını daha önce çalıştırmadığınız takdirde, bu seçeneği kullanmayın.  

    Hem **Yönetim** hem de **izleme** çalışma alanlarında, güncelleştirmeler ve bakım düğümü, şeritte **Önkoşul uyarılarını yoksay**adlı bir düğme içerir. Bu düğme, önkoşul denetimi uyarıları nedeniyle güncelleştirme paketi yüklemesi tamamlanamazsa kullanılabilir hale gelir. Örneğin, önkoşul uyarılarını yok say (güncelleştirmeler Sihirbazı içinden) seçeneğini kullanmadan bir güncelleştirmeyi yüklersiniz. Güncelleştirme yüklemesi bir önkoşul uyarısı durumuyla durduruluyor, ancak hata yok. Daha sonra Şeritteki **Önkoşul uyarılarını yoksay** ' ı seçin. Bu eylem, bu güncelleştirme yüklemesinin önkoşul uyarılarını gözardı eden otomatik devamlılığını tetikler. Bu seçeneği kullandığınızda, güncelleştirme yüklemesi birkaç dakika sonra otomatik olarak devam eder.  

- Configuration Manager istemcisi için bir güncelleştirme geçerliyse, istemci güncelleştirmesini sınırlı bir istemci kümesiyle sınamayı seçin. Daha fazla bilgi için bkz. [bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme](../../clients/manage/upgrade/test-client-upgrades.md).  

#### <a name="2-during-the-update-installation"></a>2. Güncelleştirme yüklemesi sırasında

Güncelleştirme yüklemesinin bir parçası olarak Configuration Manager aşağıdaki eylemleri yapar:  

- Etkilenen tüm bileşenleri (site sistem rolleri veya Configuration Manager konsolu gibi) yeniden yükler.  

- İstemci pilot ve [otomatik istemci yükseltmeleri](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)için yaptığınız seçimlere bağlı olarak istemcilerin güncelleştirmelerini yönetir.  

- Site sistemi sunucularının genellikle güncelleştirmenin bir parçası olarak yeniden başlatılması gerekmez. Bir rol .NET kullanıyorsa ve paket bu önkoşul bileşenini Güncelleştir, sonra site sistemi yeniden başlatılabilir.  

> [!TIP]  
> Configuration Manager güncelleştirmelerini yüklediğinizde, site CD 'yi de güncelleştirir. En son klasör. Daha fazla bilgi için [CD 'ye bakın. En son klasör](the-cd.latest-folder.md).  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Yüklendikçe güncelleştirmelerin ilerlemesini izleme

İlerlemeyi izlemek için aşağıdaki adımları kullanın:  

- Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **güncelleştirmeler ve bakım** düğümünü seçin. Bu düğüm tüm güncelleştirme paketlerinin yüklenme durumunu gösterir.  

- Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **güncelleştirmeler ve bakım durumu** düğümünü seçin. Bu düğüm, yalnızca sitenin yüklendiği geçerli güncelleştirme paketinin yükleme durumunu gösterir.  

    Güncelleştirme yüklemesi daha kolay izleme için birkaç aşamaya bölünmüştür. Aşağıdaki aşamaların her biri için, yükleme durumundaki ek ayrıntılar, daha fazla bilgi için hangi günlük dosyasının görüntüleneceği içerir:  

  - **İndir**: Bu aşama yalnızca hizmet bağlantı noktası olan en üst düzey site için geçerlidir.

  - **Çoğaltma**

  - **Önkoşul Denetimi**

  - **Yükleme**

  - **Yükleme sonrası**: daha fazla bilgi için bkz. [yükleme sonrası görevler](#post-installation-tasks).  

- Site sunucusundaki **Cmupdate. log** dosyasını `<ConfigMgr_Installation_Directory>\Logs` görüntüleyin.  

>[!NOTE]
> Sürüm 1906 ' den başlayarak, **yükleme** aşamasında **ConfigMgr veritabanını Yükselt** görevinin durumunu görebilirsiniz.
>
> - Veritabanı yükseltmesi engellenirse, **devam eden uyarı, dikkat edilmesi gerekir**.
>   - Cmupdate. log, veritabanı yükseltmesini engelleyen program adı ve SessionID 'yi SQL 'den günlüğe kaydeder.
> - Veritabanı yükseltmesi artık engellenmemişse, durum **devam ediyor** veya **tamamlanmak**üzere sıfırlanacak.
>   - Veritabanı yükseltmesi engellendiğinde, hala engellenip engellenmediğini görmek için her 5 dakikada bir bir denetim yapılır.

#### <a name="4-when-the-update-installation-completes"></a>4. Güncelleştirme yüklemesi tamamlandığında

İlk site güncelleştirmesi yüklemeyi tamamladıktan sonra:  

- Alt birincil siteler güncelleştirmeyi otomatik olarak yükler. Başka bir eylem gerekli değildir.  

- İkincil siteleri Configuration Manager konsolunun içinden el ile güncelleştirin. Daha fazla bilgi için bkz. [güncelleştirme yüklemesini ikincil bir sitede başlatma](#bkmk_secondary).  

- Hiyerarşinizdeki tüm siteler yeni sürüme güncelleştirilinceye kadar hiyerarşiniz karışık sürümlü bir modda çalışır. Daha fazla bilgi için bkz. [farklı sürümler arasında birlikte çalışabilirlik](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### <a name="5-update-configuration-manager-consoles"></a>5. Configuration Manager konsolları güncelleştirme

Bir merkezi yönetim sitesi veya birincil site güncelleştirildikten sonra, siteye bağlanan her bir Configuration Manager konsolunun da güncelleştirilmesi gerekir. Bir konsolu güncelleştirmeniz istenir:  

- Konsolu açtığınızda  

- Açık bir konsolda yeni bir düğüme gittiğinizde  

Site güncelleştirmelerinden sonra konsolu hemen güncelleştirin.  

Konsol güncelleştirmesi tamamlandıktan sonra, konsolunun ve site sürümlerinin doğru olduğunu doğrulayın. Konsolun sol üst köşesindeki **Configuration Manager hakkında** bölümüne gidin.  

> [!Note]  
> Konsol sürümü, site sürümünden biraz farklıdır. Konsolun ikincil sürümü Configuration Manager yayın sürümüne karşılık gelir. Örneğin, Configuration Manager sürüm 1802 ' de ilk site sürümü 5.0.8634.1000 ve ilk konsol sürümü 5 ' tir. **1802**. 1082,1700. Derleme (1082) ve düzeltme (1700) numaraları gelecekteki düzeltmelerle birlikte değişebilir.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a>En üst düzey sitede güncelleştirme yüklemesini başlatmak için  

Hiyerarşinizin en üst düzey sitesinde, Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **güncelleştirmeler ve bakım** düğümünü seçin. **Kullanılabilir**durumuna sahip bir güncelleştirme seçin ve ardından Şeritteki **güncelleştirme paketini yükler** ' i seçin.  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> İkincil bir sitede güncelleştirme yüklemesini başlatmak için  

İkincil bir sitenin üst birincil sitesi güncelleştirildikten sonra, ikincil siteyi Configuration Manager konsolunun içinden güncelleştirin. Bunun için **İkincil Site Yükseltme Sihirbazı**’nı kullanırsınız.  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Güncelleştirmek istediğiniz ikincil siteyi seçin ve ardından şeritte **Yükselt** ' i seçin.  

2. İkincil sitenin güncelleştirilmesini başlatmak için **Evet** ' i seçin.  

İkincil bir sitede güncelleştirme yüklemesini izlemek için, ikincil siteyi seçin ve şeritte **yükleme durumunu göster** ' i seçin. Ayrıca, her ikincil sitenin sürümünü görüntüleyebilmeniz için **Sürüm** sütununu siteler düğümüne ekleyin.  

Bazı örneklerde, konsolundaki durum yenilemez veya güncelleştirme başarısız oldu. İkincil bir site başarıyla güncelleştirildikten sonra, **yeniden deneme yükleme** seçeneğini kullanın. Bu seçenek, güncelleştirmeyi başarıyla yükleyen bir ikincil sitenin güncelleştirmesini yeniden oluşturmaz, ancak konsolu durumu güncelleştirmeye zorlar.

### <a name="post-installation-tasks"></a>Yükleme sonrası görevler

Bir site bir güncelleştirmeyi yüklediğinde, güncelleştirme site sunucusundaki yüklemeyi tamamladıktan sonra başlayamıyorum birkaç görev vardır. Bu liste, site ve hiyerarşi işlemleri için kritik olan yükleme sonrası görevleri içerir. Bunlar kritik olduklarından, etkin olarak izlenir. Doğrudan izlenmeyen ek görevler, site sistemi rollerinin yeniden yüklenmesini içerir. Kritik yükleme sonrası görevlerinin durumunu görüntülemek için, bir sitenin güncelleştirme yüklemesini izlerken **yükleme sonrası** görevi ' ni seçin.

Tüm görevler hemen tamamlanmaz. Bazı görevler, her site güncelleştirme yüklemesini tamamlayana kadar başlamaz. Bu görevler tamamlanana kadar beklemeniz gerekebilecek yeni işlevler gecikiyor olabilir. Yeni özellikleri açmak, tüm siteler güncelleştirme yüklemesini tamamlana kadar başlatılmaz, bu nedenle yeni özellikler bir süre için görünür olmayabilir.

Yükleme sonrası görevleri şunları içerir:

- **SMS_EXECUTIVE hizmeti yükleniyor**

  - Site sunucusunda çalışan kritik hizmet.
  - Bu hizmetin yeniden yüklenmesi hızla tamamlanmalıdır.

- **SMS_DATABASE_NOTIFICATION_MONITOR bileşen yükleniyor**

  - SMS_EXECUTIVE hizmetinin kritik site bileşeni iş parçacığı.
  - Bu hizmetin yeniden yüklenmesi hızla tamamlanmalıdır.

- **SMS_HIERARCHY_MANAGER bileşen yükleniyor**

  - Site sunucusunda çalışan kritik site bileşeni.
  - Site sistemi sunucularındaki rolleri yeniden yükleme sorumludur. Ayrı bir site sistem rolü yeniden yükleme durumu görüntülemiyor.
  - Bu hizmetin yeniden yüklenmesi hızla tamamlanmalıdır.

    > [!Note]
    > Bazı Configuration Manager site rolleri istemci çerçevesini paylaşır. Örneğin, yönetim noktası ve çekme dağıtım noktası. Bu roller güncelleştirilişinde, bu sunuculardaki istemci sürümü aynı anda güncellenir. Daha fazla bilgi için bkz. [istemcileri yükseltme](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **SMS_REPLICATION_CONFIGURATION_MONITOR bileşen yükleniyor**

  - Site sunucusunda çalışan kritik site bileşeni.
  - Bu hizmetin yeniden yüklenmesi hızla tamamlanmalıdır.

- **SMS_POLICY_PROVIDER bileşen yükleniyor**

  - Yalnızca birincil sitelerde çalışan kritik site bileşeni.
  - Bu hizmetin yeniden yüklenmesi hızla tamamlanmalıdır.

- **Çoğaltma başlatma işlemi izleniyor**

  - Bu görev yalnızca merkezi yönetim sitesinde ve alt birincil sitelerde görüntülenir.
  - SMS_REPLICATION_CONFIGURATION_MONITOR bağımlıdır.
  - Hızlı bir şekilde tamamlanmalıdır.

- **Configuration Manager Istemci ön üretim paketi güncelleştiriliyor**

  - Bu görev, istemci ön üretimi (istemci pilot adı da denir) kullanım için etkin olmadığında bile görüntülenir.
  - Hiyerarşideki tüm siteler güncelleştirmeyi yüklemeyi bitirene kadar başlamaz.

- **Site sunucusundaki Istemci klasörü güncelleştiriliyor**

  - Bu görev, istemciyi ön üretimde kullanıyorsanız görüntülenmez.  
  - Hızlı bir şekilde tamamlanmalıdır.

- **Configuration Manager Istemci paketi güncelleştiriliyor**

  - Bu görev, istemciyi ön üretimde kullanıyorsanız görüntülenmez.  
  - Yalnızca tüm siteler güncelleştirmeyi yükledikten sonra biter.  

- **Özellikleri açma**

  - Bu görev yalnızca hiyerarşinin üst katman sitesinde görüntülenir.
  - Hiyerarşideki tüm siteler güncelleştirmeyi yüklemeyi bitirene kadar başlamaz.
  - Ayrı özellikler görüntülenmez.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Başarısız bir güncelleştirme yüklemesini yeniden deneme  

Bir güncelleştirme yüklemesi başarısız olduğunda, uyarı ve hataların çözümünü belirlemek için konsol içi geri bildirimi inceleyin. Daha fazla ayrıntı için site sunucusunda **ConfigMgrPrereq. log dosyasına** bakın. Bir güncelleştirmeyi yüklemeyi yeniden denemeden önce hataları çözmeniz ve uyarıları çözmeniz gerekir.  

> [!TIP]  
> Bir güncelleştirmede indirme veya çoğaltma sorunları varsa, [güncelleştirme sıfırlama aracını](update-reset-tool.md)kullanın.  

Bir güncelleştirmeyi yüklemeyi yeniden denemeye hazırsanız, başarısız güncelleştirmeyi seçin ve ardından uygun seçeneği belirleyin. Güncelleştirme yüklemesini yeniden deneme davranışı, yeniden denemeyi başlattığınız düğüme ve kullandığınız yeniden deneme seçeneğine bağlıdır.  

### <a name="retry-installation-for-the-hierarchy"></a>Hiyerarşiyi yükleme işlemini yeniden deneyin

Bu güncelleştirme aşağıdaki durumlardan birinde olduğunda tüm hiyerarşi için bir güncelleştirme yüklemesini yeniden deneyin:  

- Önkoşul denetimleri bir veya daha fazla uyarıyla geçti ve güncelleştirme sihirbazında önkoşul denetimi uyarılarını yok say seçeneği ayarlanmadı. ( **Güncelleştirmeler ve bakım** düğümündeki **Prereq uyarısını yoksay** için güncelleştirme değeri **Hayır**' dır.)

- Önkoşul başarısız oldu

- Yükleme başarısız oldu  

- İçeriğin siteye çoğaltılması başarısız oldu

**Yönetim** çalışma alanına gidin ve **güncelleştirmeler ve bakım** düğümünü seçin. Güncelleştirmeyi seçin ve aşağıdaki seçeneklerden birini belirleyin:  

- **Yeniden deneme**: **güncelleştirmeler ve bakım**için yeniden **deneme** yaptığınızda güncelleştirme yüklemesi yeniden başlar ve önkoşul uyarılarını otomatik olarak yoksayar. İçerik çoğaltma daha önce başarısız olduysa, güncelleştirme içeriği tekrar çoğaltılır.  

- **Önkoşul uyarılarını yoksay**: güncelleştirme yüklemesi bir uyarı nedeniyle durdurulduğunda, **Önkoşul uyarılarını yoksay**' ı seçebilirsiniz. Bu eylem, güncelleştirme yüklemesinin birkaç dakika sonra devam etmesine olanak sağlar ve önkoşul uyarılarını yok saymak için seçeneğini kullanır.

### <a name="retry-installation-for-the-site"></a>Site için yüklemeyi yeniden dene

Söz konusu güncelleştirme aşağıdaki durumlardan birinde olduğunda, bir güncelleştirmeyi belirli bir siteye yüklemeyi yeniden deneyin:  

- Önkoşul denetimleri bir veya daha fazla uyarıyla geçti ve güncelleştirme sihirbazında önkoşul denetimi uyarılarını yok say seçeneği ayarlanmadı. (Güncelleştirmeler ve bakım düğümündeki **Prereq uyarısını yoksay** için güncelleştirmeler değeri **Hayır**' dır.)  

- Önkoşul başarısız oldu

- Yükleme başarısız oldu

**İzleme** çalışma alanına gidin ve **site bakım durumu** düğümünü seçin. Güncelleştirmeyi seçin ve aşağıdaki seçeneklerden birini belirleyin:  

- **Yeniden deneme**: **site bakım durumundan** **yeniden** çalıştığınızda güncelleştirme yüklemesini yalnızca bu sitede yeniden başlatın. **Yeniden denemeyi** **güncelleştirmeler ve bakım** düğümünden çalıştırmanın aksine, bu yeniden deneme önkoşul uyarılarını gözardı etmez.  

- **Önkoşul uyarılarını yoksay**: güncelleştirme yüklemesi bir uyarı nedeniyle durdurulduğunda, **Önkoşul uyarılarını yoksay**' ı seçebilirsiniz. Bu eylem, güncelleştirme yüklemesinin birkaç dakika sonra devam etmesine olanak sağlar ve önkoşul uyarılarını yok saymak için seçeneğini kullanır.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Site bir güncelleştirmeyi yükledikten sonra  

Site güncelleştirildikten sonra, geçerli sürüm için güncelleştirme sonrası denetim listesini gözden geçirin:  

- [Sürüm 2002 için güncelleştirme sonrası denetim listesi](checklist-for-installing-update-2002.md#post-update-checklist)

- [Sürüm 1910 için güncelleştirme sonrası denetim listesi](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Sürüm 1906 için güncelleştirme sonrası denetim listesi](checklist-for-installing-update-1906.md#post-update-checklist)  

- [Sürüm 1902 için güncelleştirme sonrası denetim listesi](checklist-for-installing-update-1902.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Güncelleştirmelerin isteğe bağlı özelliklerini etkinleştirme  

Bir güncelleştirme bir veya daha fazla isteğe bağlı özellik içerdiğinde, bu özellikleri hiyerarşinizde etkinleştirme şansınız vardır. Güncelleştirme yüklendiğinde özellikleri etkinleştirin veya daha sonra isteğe bağlı özellikleri etkinleştirmek için konsola geri dönün.

Kullanılabilir özellikleri ve bunların durumunu görüntülemek için, konsolunda **Yönetim** çalışma alanına gidin, **güncelleştirmeler ve bakım**' ı genişletin ve **Özellikler** düğümünü seçin.

Bir özellik isteğe bağlı olmadığında otomatik olarak yüklenir. **Özellikler** düğümünde görünmez.  

> [!Important]  
> Çok siteli bir hiyerarşide, yalnızca merkezi yönetim sitesinden isteğe bağlı veya yayın öncesi özellikleri etkinleştirin. Bu davranış, hiyerarşide çakışma olmamasını sağlar. <!--507197-->  

Yeni bir özellik veya yayın öncesi özelliğini etkinleştirdiğinizde, bu özellik kullanılabilir hale gelmeden önce Configuration Manager hiyerarşi Yöneticisi (HMAN) değişikliği işlemesi gerekir. Değişikliğin işlenmesi genellikle anında gerçekleşir. HMAN işleme döngüsüne bağlı olarak, tamamlanması 30 dakika kadar sürebilir. Değişiklik işlendikten sonra, özelliği kullanabilmeniz için konsolunu yeniden başlatın.

Sürüm 2002 ' den başlayarak,<!--5834830--> Microsoft Endpoint Manager Yönetim merkezinde yeni bulut tabanlı özellikler veya şirket içi Configuration Manager yüklemeniz için diğer bağlı bulut hizmetleri kullanılabilir olduğunda, artık Configuration Manager konsolundaki bu yeni özellikleri tercih edebilirsiniz.

### <a name="list-of-optional-features"></a>İsteğe bağlı özelliklerin listesi

Aşağıdaki özellikler Configuration Manager en son sürümünde isteğe bağlıdır:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [BitLocker yönetimi](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Koleksiyon üyeliği sonuçlarını Azure Active Directory ile eşitler](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Kullanıcı grubu bulmayı Azure Active Directory](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Uygulama grupları](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Görev sırası hata ayıklayıcısı](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Paket Dönüştürme Yöneticisi](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [Ortak yönetilen cihazlar Için istemci uygulamaları](../../../comanage/workloads.md#client-apps) (daha önce *ortak yönetilen cihazlar için mobil uygulamalar*olarak bilinir) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C-->
- [Üçüncü taraf yazılım güncelleştirmeleri](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Cihaz başına Kullanıcı için uygulama isteklerini Onayla](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Betik oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Surface sürücü güncelleştirmeleri](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Bulut yönetimi ağ geçidi](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [PFX oluştur](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Azure Log Analytics Bağlayıcısı](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Windows Defender Exploit Guard ilkesi](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [Windows 10 için VPN](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Küme durumunu algılayan bir koleksiyona hizmet verme (sunucu grupları)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [İş Için Windows Hello](../../../protect/deploy-use/windows-hello-for-business-settings.md) (önceden *Passport for Work*olarak bilinirdi) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!Tip]  
> Etkinleştirme onayı gerektiren özellikler hakkında daha fazla bilgi için bkz. [yayın öncesi Özellikler](pre-release-features.md).  
>
> Yalnızca Technical Preview dalında bulunan özellikler hakkında daha fazla bilgi için bkz. [Technical Preview](../../get-started/technical-preview.md).

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Güncelleştirmelerdeki yayın öncesi özellikleri kullanma

Geçerli dal, bir üretim ortamında erken test için yayın öncesi özellikleri içerir. Daha fazla bilgi için bkz. [yayın öncesi Özellikler](pre-release-features.md).

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a>Sık sorulan sorular

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>Bazı güncelleştirmeleri konsolumda neden göremiyorum?

Microsoft bulut hizmeti ile başarılı bir eşitlemeden sonra konsolunuzda belirli bir güncelleştirme bulamazsanız, bu davranış aşağıdakilerden biri olabilir:  

- Güncelleştirme, altyapınızın kullandığı bir yapılandırma gerektirir veya geçerli ürün sürümünüz güncelleştirmeyi almak için bir önkoşulu karşılamıyor.  

    Eksik bir güncelleştirme için gerekli yapılandırmalara ve önkoşullara sahip olduğunu düşünüyorsanız, hizmet bağlantı noktasının çevrimiçi modda olduğunu doğrulayın. Ardından, bir denetimi zorlamak için **güncelleştirmeler ve bakım** düğümündeki **Güncelleştirmeleri denetle** seçeneğini kullanın. Hizmet bağlantı noktanız çevrimdışı modda ise, bulut hizmetiyle el ile eşitleme yapmak için hizmet bağlantı aracını kullanın.  

- Hesabınız, Configuration Manager konsolundaki güncelleştirmeleri görüntülemek için doğru rol tabanlı yönetim izinlerine sahip değildir. Daha fazla bilgi için bkz. [güncelleştirmeleri yönetme izinleri](#assign-permissions-to-view-and-manage-updates-and-features).  
