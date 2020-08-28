---
title: Sürüm 1906’daki yenilikler
titleSuffix: Configuration Manager
description: Geçerli dalın Configuration Manager sürüm 1906 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3736e5343e10bdfc8d5be8abf79ee27e46749834
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995118"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Geçerli dalın Configuration Manager sürüm 1906 ' deki yenilikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme 1906, konsol içi bir güncelleştirme olarak sunulmaktadır. Sürüm 1802 veya üstünü çalıştıran sitelerde bu güncelleştirmeyi uygulayın. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Bu makalede Configuration Manager, sürüm 1906 ' deki değişiklikler ve yeni özellikler özetlenmektedir.  

Bu güncelleştirmeyi yüklemek için her zaman en son denetim listesini gözden geçirin. Daha fazla bilgi için bkz. [güncelleştirme 1906 yükleme denetim listesi](../../servers/manage/checklist-for-installing-update-1906.md). Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist)de gözden geçirin.

Yeni Configuration Manager özelliklerinden tam olarak yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme de güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

> [!Tip]  
> Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>Gereksinim değişiklikleri

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>Sürüm 1906 istemcisi, SHA-2 kod imzalama desteği gerektirir

<!--SCCMDocs-pr#3404-->
SHA-1 algoritmasındaki zayıf noktalar nedeniyle ve sektör standartlarına uyum sağlamak için, Microsoft artık yalnızca daha güvenli SHA-2 algoritmasını kullanarak Configuration Manager ikililerini imzalar. Aşağıdaki Windows işletim sistemi sürümleri, SHA-2 kod imzalama desteği için bir güncelleştirme gerektirir:

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

Daha fazla bilgi için bkz. [Windows istemcileri Için Önkoşullar](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2).


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site altyapısı

### <a name="site-server-maintenance-task-improvements"></a>Site sunucusu bakım görevi geliştirmeleri

<!--3555894-->
Site sunucusu bakım görevleri artık, bir site sunucusunun Ayrıntılar görünümünde kendi sekmesinden görüntülenebilir ve düzenlenebilir. Yeni **bakım görevleri** sekmesi, şunları gibi bilgiler sağlar:

- Görev etkinse
- Görev zamanlaması
- Son başlangıç zamanı
- Son tamamlanma zamanı
- Görev başarıyla tamamlanırsa

![Site sunucusunun ayrıntı görünümünde bakım görevleri için yeni sekme](./media/3555894-maintenance-tasks.png)

Daha fazla bilgi için bkz. [bakım görevleri](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906).

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Veritabanı yükseltme izlemeyi Configuration Manager güncelleştirme

<!--4200581-->
Configuration Manager Güncelleştirme uygulanırken, yükleme durumu penceresinde **ConfigMgr veritabanını Yükselt** görevinin durumunu görebilirsiniz.

- Veritabanı yükseltmesi engellenirse, uyarı, **devam ediyor, dikkat edilmesi gereken**bir uyarı verilir.
   - Cmupdate. log, veritabanı yükseltmesini engelleyen program adı ve SessionID 'yi SQL 'den günlüğe kaydeder.
- Veritabanı yükseltmesi artık engellenmemişse, durum **devam ediyor** veya **tamamlanmak**üzere sıfırlanacak.
   - Veritabanı yükseltmesi engellendiğinde, hala engellenip engellenmediğini görmek için her 5 dakikada bir bir denetim yapılır.

   ![Yükleme sırasında veritabanı yükseltme izlemesi](./media/4200581-database-upgrade-monitoring.png)

Daha fazla bilgi için bkz. [konsol içi güncelleştirmeleri yüklemeyi](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install).

### <a name="management-insights-rule-for-ntlm-fallback"></a>NTLM geri dönüşü için yönetim öngörüleri kuralı

<!--4572953-->
Yönetim öngörüleri, site için daha az güvenli NTLM kimlik doğrulama geri dönüş yöntemi etkinleştirilip etkinleştirilmediğini algılayan yeni bir kural içerir: **NTLM geri dönüş etkindir**.

Daha fazla bilgi için bkz. [Management Insights](../../servers/manage/management-insights.md#security).

### <a name="improvements-to-support-for-sql-always-on"></a>SQL her zaman açık için desteğe yönelik iyileştirmeler

- Kurulumdan yeni bir zaman uyumlu çoğaltma ekleme<!--3127336-->: Artık var olan bir SQL Always on kullanılabilirlik grubuna yeni bir ikincil çoğaltma düğümü ekleyebilirsiniz. El ile gerçekleştirilen bir işlem yerine, bu değişikliği yapmak için Configuration Manager Kurulum kullanın. Daha fazla bilgi için bkz. [SQL Server Always on kullanılabilirlik grupları yapılandırma](../../servers/deploy/configure/configure-aoag.md#bkmk_sync).

- Çoklu alt ağ yük devretme<!-- SCCMDocs-pr#3734 -->: Artık SQL Server ' de [MultiSubnetFailover Bağlantı dizesi anahtar sözcüğünü](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) etkinleştirebilirsiniz. Ayrıca, site sunucusunu el ile yapılandırmanız gerekir. Daha fazla bilgi için bkz. [Çoklu alt ağ yük devretme](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover) önkoşulu.

- Dağıtılmış görünümler için destek<!-- SCCMDocs-pr#3792 -->: Site veritabanı SQL Server Always on kullanılabilirlik grubunda barındırılabilir ve [dağıtılmış görünümleri](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep)kullanmak için veritabanı çoğaltması bağlantılarını etkinleştirebilirsiniz.

    > [!Note]  
    > Bu değişiklik SQL Server kümelerine uygulanmaz.

- Site Recovery, veritabanını bir SQL Always on grubunda yeniden oluşturabilir. Bu işlem hem el ile hem de otomatik dengeli çalışma ile birlikte çalışabilir.<!-- SCCMDocs-pr#3846 -->

- Yeni kurulum önkoşul denetimleri:<!-- SCCMDocs-pr#3899 -->  

    - SQL kullanılabilirlik grubu çoğaltmalarının hepsi aynı dengeli dağıtım moduna sahip olmalıdır
    - SQL kullanılabilirlik grubu çoğaltmaları sağlıklı olmalıdır

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Buluta bağlı yönetim

### <a name="azure-active-directory-user-group-discovery"></a>Kullanıcı grubu bulmayı Azure Active Directory

<!--3611956-->

Artık Azure Active Directory (Azure AD) ' dan bu grupların Kullanıcı gruplarını ve üyelerini bulabilirsiniz. Azure AD gruplarında bulunan, sitenin daha önce keşfedilmemiş olduğu kullanıcılar Configuration Manager Kullanıcı kaynakları olarak eklenir. Grup bir güvenlik grubu olduğunda, bir Kullanıcı grubu kaynak kaydı oluşturulur. Bu özellik, [yayın öncesi bir özelliktir](../../servers/manage/pre-release-features.md) ve etkinleştirilmesi gerekir.

Daha fazla bilgi için bkz. [keşif yöntemlerini yapılandırma](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco).

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>Koleksiyon üyeliği sonuçlarını Azure Active Directory gruplarıyla eşitler

<!--3607475-->

Artık koleksiyon üyeliklerinin Azure Active Directory (Azure AD) grubuna eşitlenmesini etkinleştirebilirsiniz. Bu eşitleme, yayın öncesi bir özelliktir. Etkinleştirmek için bkz. [yayın öncesi Özellikler](../../servers/manage/pre-release-features.md).

Eşitleme, koleksiyon üyeliği sonuçlarına göre Azure AD grup üyelikleri oluşturarak mevcut şirket içi gruplandırma kurallarınızı bulutta kullanmanıza olanak sağlar. Yalnızca Azure Active Directory kaydına sahip cihazlar Azure AD grubuna yansıtılır. Karma Azure AD 'ye katılmış ve Azure Active Directory katılmış cihazların her ikisi de desteklenir.

Daha fazla bilgi için bkz. [koleksiyon oluşturma](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync).


## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Masaüstü Analizi

### <a name="readiness-insights-for-desktop-apps"></a>Masaüstü uygulamaları için hazırlık öngörüleri

<!-- 4021225 -->

Artık, iş kolu uygulamaları da dahil olmak üzere masaüstü uygulamalarınız hakkında daha ayrıntılı bilgiler edinebilirsiniz. Eski uygulama durumu Çözümleyicisi araç seti artık Configuration Manager istemcisiyle tümleşiktir. Bu tümleştirme, masaüstü Analizi portalında uygulama hazırlığı öngörülerinin dağıtımını ve yönetilebilirliğini basitleştirir.

Daha fazla bilgi için bkz. [Masaüstü Analizi 'Nde uyumluluk değerlendirmesi](../../../desktop-analytics/compat-assessment.md#advanced-insights).


### <a name="dalogscollector-tool"></a>DALogsCollector aracı

<!--4622989-->
Masaüstü Analizi sorunlarını gidermeye yardımcı olması için Configuration Manager install dizinindeki DesktopAnalyticsLogsCollector.ps1 aracını kullanın. Bazı temel sorun giderme adımlarını çalıştırır ve ilgili günlükleri tek bir çalışma dizininde toplar.

Daha fazla bilgi için bkz. [Günlükler toplayıcısı](../../../desktop-analytics/log-collector.md).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Gerçek zamanlı yönetim

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>CMPivot içinde birleştirmeler, ek işleçler ve aggregekleyin

<!--4054074-->

CMPivot için artık ek aritmetik işleçler, aggregators 'lar ve kayıt defteri ve dosya kullanma gibi sorgu birleştirmeleri ekleme imkanına sahip olursunuz.

Daha fazla bilgi için bkz. [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1906).

### <a name="cmpivot-standalone"></a>Tek başına CMPivot

<!--3555890, 4619340, 4692885 -->

Artık CMPivot 'yi tek başına uygulama olarak kullanabilirsiniz. CMPivot tek başına, **yayın öncesi bir özelliktir** ve yalnızca İngilizce olarak kullanılabilir. Ortamınızdaki cihazların gerçek zamanlı durumunu görüntülemek için Configuration Manager konsolunun dışında CMPivot çalıştırın. Bu değişiklik, konsolu yüklemeden önce bir cihazda CMPivot kullanmanıza olanak sağlar.

CMPivot 'in gücünden birini, yardım masası veya güvenlik yöneticileri gibi diğer kişilerle paylaşabilirsiniz. Bu kişiler, geleneksel olarak kullandıkları diğer araçlarla birlikte Configuration Manager sorgulamak için CMPivot kullanabilir. Bu zengin yönetim verilerini paylaşarak, roller arası iş sorunlarını önceden çözmek için birlikte çalışabilirsiniz.

Daha fazla bilgi için bkz. [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) ve [yayın öncesi özellikleri](../../servers/manage/pre-release-features.md#bkmk_table).

### <a name="added-permissions-to-the-security-administrator-role"></a>Güvenlik Yöneticisi rolüne izinler eklendi

<!--4683130-->

Configuration Manager yerleşik [**Güvenlik Yöneticisi**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) rolüne aşağıdaki izinler eklenmiştir:

- SMS komut dosyasında oku
- Koleksiyonda CMPivot Çalıştır
- Envanter raporunda oku

Daha fazla bilgi için bkz. [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot_secadmin1906).


## <a name="content-management"></a><a name="bkmk_content"></a> İçerik yönetimi

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>İstemci veri kaynakları panosundaki teslim Iyileştirme indirme verileri

<!--3555759-->
İstemci veri kaynakları panosu artık [teslim iyileştirme](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) verilerini içerir. Bu Pano, istemcilerin ortamınızda içerik elde ettiği yeri anlamanıza yardımcı olur.

Daha fazla bilgi için bkz. [Istemci veri kaynakları panosu](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>Dağıtım Iyileştirmeye yönelik bir ağ önbelleği sunucusu olarak dağıtım noktanızı kullanın

<!--3555764-->
Dağıtım noktalarınıza artık teslim Iyileştirmesi için ağ önbellek sunucusu yükleyebilirsiniz. Bu içeriği şirket içinde önbelleğe alarak istemcileriniz teslim Iyileştirme özelliğinden yararlanabilir, ancak WAN bağlantılarını korumaya yardımcı olabilirsiniz.

Bu önbellek sunucusu teslim Iyileştirmesi tarafından indirilen içerik için isteğe bağlı bir saydam önbellek işlevi görür. Bu sunucunun yalnızca yerel Configuration Manager sınır grubunun üyelerine sunulmakta olduğundan emin olmak için istemci ayarlarını kullanın.

Daha fazla bilgi için, bkz. [Configuration Manager Içindeki ağ önbelleğinde teslim iyileştirmesi](../hierarchy/microsoft-connected-cache.md).


## <a name="client-management"></a><a name="bkmk_client"></a> İstemci yönetimi

### <a name="support-for-windows-virtual-desktop"></a>Windows sanal masaüstü desteği

<!--3556025-->
[Windows sanal masaüstü](/azure/virtual-desktop/) Microsoft Azure ve Microsoft 365 bir önizleme özelliğidir. Artık, Azure 'da Windows çalıştıran bu sanal cihazları yönetmek için Configuration Manager kullanabilirsiniz.

Terminal sunucusuna benzer şekilde, bu sanal cihazlar Çoklu eşzamanlı etkin kullanıcı oturumlarına izin verir. İstemci performansına yardımcı olmak için Configuration Manager artık bu çoklu kullanıcı oturumlarına izin veren her cihazda kullanıcı ilkelerini devre dışı bırakır. Kullanıcı ilkelerini etkinleştirseniz bile, istemci Windows sanal masaüstü ve terminal sunucuları 'nı içeren bu cihazlarda varsayılan olarak devre dışı bırakır.

Daha fazla bilgi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemi sürümleri](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers).

### <a name="support-center-onetrace-preview"></a>Destek Merkezi OneTrace (Önizleme)

<!--3555962-->
OneTrace, Destek Merkezi 'nin bulunduğu yeni bir günlük görüntüleyicisine sahiptir. Aşağıdaki geliştirmelerle CMTrace 'e benzer şekilde çalışır:

- Sekmeli Görünüm
- Dockable Windows
- Geliştirilmiş arama özellikleri
- Günlük görünümünden çıkmadan filtreleri etkinleştirebilme
- Hata kümelerini hızlı bir şekilde tanımlamak için kaydırma çubuğu ipuçları
- Büyük dosyalar için hızlı günlük açma

![OneTrace günlük görüntüleyicisinin ekran görüntüsü](./media/3555962-onetrace.png)

Daha fazla bilgi için bkz. [Destek Merkezi OneTrace](../../support/support-center-onetrace.md).

### <a name="configure-client-cache-minimum-retention-period"></a>İstemci önbelleği en düşük saklama süresini yapılandırma

<!--4485509-->
Artık Configuration Manager istemcisinin önbelleğe alınmış içeriği tutabilmeniz için en kısa süreyi belirtebilirsiniz. Bu istemci ayarı, daha fazla alana ihtiyaç duyulmanız durumunda Configuration Manager aracısının önbellekten içerik kaldırabilmesi için bekleyeceği en az süreyi tanımlar. İstemci ayarları **istemci önbellek ayarları** grubunda, aşağıdaki ayarı yapılandırın: **önbelleğe alınan Içeriğin kaldırılabilmesi için en kısa süre (dakika)**.

> [!Note]  
> Aynı istemci ayarı grubunda, **tam işletim sistemindeki Configuration Manager istemcisinin içerik paylaşmasını sağlamak** için var olan ayar artık **eş önbellek kaynağı olarak etkinleştirilecek**şekilde yeniden adlandırıldı. Ayarın davranışı değişmez.  

Daha fazla bilgi için bkz. [istemci önbellek ayarları](../../clients/deploy/about-client-settings.md#client-cache-settings).


## <a name="co-management"></a><a name="bkmk_comgmt"></a> Ortak yönetim

### <a name="improvements-to-co-management-auto-enrollment"></a>Ortak yönetim otomatik kayıt geliştirmeleri

- Yeni bir ortak yönetilen cihaz artık, Azure Active Directory (Azure AD) *cihaz* belirtecine göre Microsoft Intune hizmetine otomatik olarak kaydeder. Kullanıcının otomatik kayıt işleminin başlaması için cihazda oturum açmasını beklemesi gerekmez. Bu [değişiklik,](../../../comanage/how-to-monitor.md#co-management-enrollment-status) *kullanıcının oturum açmasını bekleyen*cihaz sayısını azaltmaya yardımcı olur.<!-- 4454491 -->

- Zaten cihazların ortak yönetimine kaydolduğu müşteriler için, yeni cihazlar artık önkoşulları karşıladıktan hemen sonra kaydolur. Örneğin, cihaz Azure AD 'ye katıldığında ve Configuration Manager istemcisi yüklendikten sonra.<!--4321130-->

Daha fazla bilgi için bkz. [ortak yönetimi etkinleştirme](../../../comanage/how-to-enable.md).

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>Ortak yönetim iş yükleri için birden çok pilot grubu

<!--3555750-->
Artık ortak yönetim iş yüklerinin her biri için farklı pilot koleksiyonları yapılandırabilirsiniz. Farklı pilot koleksiyonları kullanmak, iş yüklerini değiştirirken daha ayrıntılı bir yaklaşım almanıza olanak sağlar.

- **Etkinleştirme** sekmesinde artık bir **Intune otomatik kayıt** koleksiyonu belirtebilirsiniz.
    - **Intune otomatik kayıt** koleksiyonu, ortak yönetime eklemek istediğiniz tüm istemcileri içermelidir. Bu aslında diğer tüm hazırlama koleksiyonlarının bir üst kümesidir.

- **Hazırlama** sekmesinde, tüm iş yükleri için tek bir pilot koleksiyon kullanmak yerine, her iş yükü için tek bir koleksiyon seçebilirsiniz.

    ![Ortak yönetim hazırlama sekmesi her iş yükü için bir koleksiyon seçmenizi sağlar](./media/3555750-co-management-staging-tab.png)

Bu seçenekler, ortak yönetimi ilk defa etkinleştirdiğinizde da kullanılabilir.

Daha fazla bilgi için bkz. [ortak yönetimi etkinleştirme](../../../comanage/how-to-enable.md).

### <a name="co-management-support-for-government-cloud"></a>Kamu Bulutu için ortak yönetim desteği

<!--4075452-->
ABD devlet müşterileri artık Azure ABD kamu bulutu (portal.azure.us) ile birlikte ortak yönetimi kullanabilir. Daha fazla bilgi için bkz. [ortak yönetimi etkinleştirme](../../../comanage/how-to-enable.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Uygulama yönetimi

### <a name="filter-applications-deployed-to-devices"></a>Cihazlara dağıtılan uygulamaları filtrele

<!--4451056-->
Cihaz hedefli uygulama dağıtımları için Kullanıcı kategorileri artık yazılım merkezi 'nde filtre olarak gösterilir. Özelliklerine ait **Yazılım Merkezi** sayfasında bir uygulama için **Kullanıcı kategorisi** belirtin. Ardından, uygulamayı Yazılım Merkezi 'nde açın ve kullanılabilir filtrelere bakın.

Daha fazla bilgi için bkz. [uygulama bilgilerini el ile belirtme](../../../apps/deploy-use/create-applications.md#bkmk_manual-app).

### <a name="application-groups"></a>Uygulama grupları

<!--3555907-->
Bir kullanıcı veya cihaz koleksiyonuna tek bir dağıtım olarak gönderebilmeniz için bir uygulama grubu oluşturun. Uygulama grubu hakkında belirttiğiniz meta veriler yazılım merkezi 'nde tek bir varlık olarak görülür. Bu uygulamaları, istemcinin belirli bir sırada yüklemesi için Grup içindeki sıraya alabilirsiniz.

Bu özellik ön sürümdür. Etkinleştirmek için bkz. [yayın öncesi Özellikler](../../servers/manage/pre-release-features.md).

Daha fazla bilgi için bkz. [uygulama grupları oluşturma](../../../apps/deploy-use/create-app-groups.md).

### <a name="retry-the-install-of-pre-approved-applications"></a>Önceden onaylanan uygulamalar yüklemesini yeniden deneyin

<!--4336307-->
Artık bir kullanıcı veya cihaz için daha önce onayladınız bir uygulamanın yüklemesini yeniden deneyebilirsiniz. Onay seçeneği yalnızca kullanılabilir dağıtımlar içindir. Kullanıcı uygulamayı kaldırırsa veya ilk yükleme işlemi başarısız olursa, Configuration Manager durumunu yeniden değerlendirmez ve yeniden yüklemez. Bu özellik destek teknisyeninin, yardım için çağıran bir kullanıcı için uygulama yüklemeyi hızlı bir şekilde yeniden denemesini sağlar.

Daha fazla bilgi için bkz. [uygulamaları onaylama](../../../apps/deploy-use/app-approval.md).

### <a name="install-an-application-for-a-device"></a>Bir cihaz için uygulama yüklemesi

<!--4402180-->
Configuration Manager konsolundan, artık uygulamaları gerçek zamanlı olarak bir cihaza yükleyebilirsiniz. Bu özellik, her uygulama için ayrı koleksiyonlar gereksinimini azaltmaya yardımcı olabilir.

Daha fazla bilgi için bkz. [cihaz için uygulama yüklemesi](../../../apps/deploy-use/install-app-for-device.md).

### <a name="improvements-to-app-approvals"></a>Uygulama onayları geliştirmeleri

<!--4224910-->
Bu sürüm, uygulama onayları için aşağıdaki geliştirmeleri içerir:

- Konsolda bir uygulama isteğini onaylar ve sonra bunu engellerseniz, artık yeniden onaylayabilirsiniz. Uygulamayı onayladıktan sonra, uygulama istemciye yeniden yüklenir.  

- Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanındaki **uygulama yönetimi**altında, **onay istekleri** düğümü, **Uygulama istekleri**olarak yeniden adlandırılır.<!-- SCCMDocs-pr#4028 -->

- Bir uygulama onay isteğini kaldırmak için yeni bir WMI yöntemi olan **DeleteInstance** vardır. Bu eylem cihazdaki uygulamayı kaldırmaz. Henüz yüklenmemişse, Kullanıcı uygulamayı Yazılım Merkezi 'nden yükleyemez.

- Bir cihazda uygulama için önceden onaylanmış bir istek oluşturmak için **Createapproisteyiste istek** API 'sini çağırın. Uygulamayı istemcide otomatik olarak yüklemeyi engellemek için, otomatik **yükleme** parametresini olarak ayarlayın `FALSE` . Kullanıcı uygulamayı Yazılım Merkezi 'nde görür, ancak otomatik olarak yüklenmez.

Daha fazla bilgi için bkz. [uygulamaları onaylama](../../../apps/deploy-use/app-approval.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> İşletim sistemi dağıtımı

### <a name="task-sequence-debugger"></a>Görev sırası hata ayıklayıcısı

<!--3612274-->
Görev sırası hata ayıklayıcı yeni bir sorun giderme aracıdır. Bir görev dizisini hata ayıklama modunda bir cihaz koleksiyonuna dağıtırsınız. Sorun giderme ve araştırmaya yardımcı olmak için görev dizisini denetimli bir şekilde adım adım gerçekleştirmenizi sağlar.

![Görev sırası hata ayıklayıcısı ekran görüntüsü](./media/3612274-tsdebug.png)

Bu özellik ön sürümdür. Etkinleştirmek için bkz. [yayın öncesi Özellikler](../../servers/manage/pre-release-features.md).

Daha fazla bilgi için bkz. [görev dizisinde hata ayıklama](../../../osd/deploy-use/debug-task-sequence.md).

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>Görev sırası sırasında istemci önbelleğinden uygulama içeriğini temizle

<!--4485675-->
**Uygulamayı yükler** görev sırası adımında, artık adım çalıştıktan sonra istemci önbelleğinden uygulama içeriğini silebilirsiniz.

Daha fazla bilgi için bkz. [görev dizisi adımları hakkında](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication).

> [!Important]  
> Bu yeni özelliği desteklemek için hedef istemciyi en son sürüme güncelleştirin.

### <a name="reclaim-sedo-lock-for-task-sequences"></a>Görev dizileri için SEDO kilidini geri kazan

<!--3699337-->
Configuration Manager konsolu yanıt vermeyi durdurursa, bir görev dizisinde daha fazla değişiklik yapmanın dışında bırakabilirsiniz. Artık kilitli bir görev dizisine erişmeye çalıştığınızda, artık **değişiklikleri atabilir**ve nesneyi düzenlemeyle devam edebilirsiniz.

Daha fazla bilgi için bkz. [görev dizisi düzenleyicisini kullanma](../../../osd/understand/task-sequence-editor.md#bkmk_sedo).

### <a name="pre-cache-driver-packages-and-os-images"></a>Sürücü paketlerini ve işletim sistemi görüntülerini ön belleğe al

<!--4224642-->
Görev sırası ön önbelleği artık ek içerik türlerini içerir. Ön önbellek içeriği daha önce yalnızca işletim sistemi yükseltme paketlerine uygulanır. Artık bant genişliği tüketimini azaltmak için önceden önbelleğe alma kullanabilirsiniz:

- İşletim sistemi görüntüleri
- Sürücü paketleri
- Paketler

Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../../../osd/deploy-use/configure-precache-content.md).

### <a name="improvements-to-os-deployment"></a>İşletim sistemi dağıtımına yönelik iyileştirmeler

Bu sürüm, işletim sistemi dağıtımına yönelik aşağıdaki geliştirmeleri içerir:

- [Görev dizisi Çalıştır](../../../osd/understand/task-sequence-steps.md#child-task-sequence) adımını oluşturmak ve düzenlemek için aşağıdaki iki PowerShell cmdlet 'ini kullanın:<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- Bir görev dizisini çalıştırdığınızda değişkenleri düzenlemek artık daha kolay. Görev sırası Sihirbazı penceresinde bir görev sırası seçtikten sonra, görev sırası değişkenlerini düzenlemek için sayfa bir **düzenleme** düğmesi içerir.<!-- 4668846 --> Daha fazla bilgi için bkz. [görev dizisi değişkenlerini kullanma](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz).

- **BitLocker 'ı devre dışı bırak** görev dizisi adımının yeni bir yeniden başlatma sayacı vardır. BitLocker 'ın devre dışı bırakılması için yeniden başlatma sayısını belirtmek üzere bu seçeneği kullanın. Bu değişiklik, görev dizinizi basitleştirmenize yardımcı olur. Bu adımın birden çok örneğini eklemek yerine tek bir adım kullanabilirsiniz. <!--4512937--> Daha fazla bilgi için, bkz. [Disable BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker).

- **SMSTSRebootDelayNext** yeni görev dizisi değişkenini mevcut [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) değişkeniyle birlikte kullanın. Daha sonraki yeniden başlatmaların birinciden farklı bir zaman aşımı ile gerçekleşmesini istiyorsanız, bu yeni değişkeni saniye cinsinden farklı bir değere ayarlayın. <!--4447680--> Daha fazla bilgi için bkz. [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext).

- Görev sırası yeni bir salt okunurdur **_SMSTSLastContentDownloadLocation**değişken ayarlar. Bu değişken, görev sırasının indirildiği veya içeriği indirmeye çalıştığı son konumu içerir. İstemci günlüklerini ayrıştırmak yerine bu değişkeni inceleyin.<!-- 2840337 -->

- Görev sırası medyası oluşturduğunuzda Configuration Manager Autorun. inf dosyası eklemez. Bu dosya genellikle kötü amaçlı yazılımdan koruma ürünleri tarafından engelleniyor. Senaryonuz için gerekirse dosyayı yine de ekleyebilirsiniz.<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>PXE geliştirmeleri

PXE DHCP el sıkışması sırasında 82 seçeneği artık WDS olmadan PXE Yanıtlayıcı ile desteklenmektedir. 82 seçeneği WDS ile desteklenmez.


## <a name="software-center"></a><a name="bkmk_userxp"></a> Yazılım Merkezi

### <a name="improvements-to-software-center-tab-customizations"></a>Software Center sekme özelleştirmelerinde geliştirmeler

<!--4063773-->
Artık yazılım merkezi 'ne beş adede kadar özel sekme ekleyebilirsiniz. Ayrıca, bu sekmelerin yazılım merkezi 'nde görünme sırasını düzenleyebilirsiniz.

Daha fazla bilgi için bkz. [Software Center istemci ayarları](../../clients/deploy/about-client-settings.md#software-center).

### <a name="software-center-infrastructure-improvements"></a>Software Center altyapı geliştirmeleri

<!--3555950-->

Bu sürüm, yazılım merkezi 'Nde aşağıdaki altyapı geliştirmelerini içerir:

- Yazılım Merkezi artık kullanıcılara hedeflenen uygulamalara yönelik bir yönetim noktasıyla iletişim kurar. Artık uygulama kataloğunu kullanmaz. Bu değişiklik, uygulama kataloğunu siteden kaldırmanızı kolaylaştırır.

- Daha önce yazılım merkezi, kullanılabilir sunucular listesinden ilk yönetim noktasını çekildi. Bu sürümden itibaren, istemcinin kullandığı yönetim noktasını kullanır. Bu değişiklik, yazılım merkezi 'nin istemci olarak atanan birincil siteden aynı yönetim noktasını kullanmasına olanak sağlar.

> [!Important]  
> Yazılım Merkezi ve yönetim noktası için bu yinelemeli geliştirmeler, uygulama kataloğu rollerinin devre dışı bırakılması.
>
> - Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez.
> - Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz.
> - Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  

Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat) ve [Yazılım Merkezi planı](../../../apps/plan-design/plan-for-software-center.md).

### <a name="redesigned-notification-for-newly-available-software"></a>Yeni kullanılabilir yazılımlar için yeniden tasarlanan bildirim

<!--3555904-->
**Yeni yazılım kullanılabilir** bildirimi, bir kullanıcı için belirli bir uygulama ve düzeltme için bir kez görünür. Kullanıcı artık her oturum açtıklarında bildirimi görmez. Yalnızca değiştirilmiş veya yeniden dağıtılan bir uygulama için başka bir bildirim görür.

Daha fazla bilgi için bkz. [uygulama oluşturma ve dağıtma](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience).

### <a name="more-frequent-countdown-notifications-for-restarts"></a>Yeniden başlatmalar için daha sık geri sayım bildirimleri

<!--3976435-->

Son kullanıcılar artık zaman aralıklı geri sayım bildirimleri ile bekleyen bir yeniden başlatmanın daha sık hatırlatılacak. **Bilgisayar yeniden başlatma** sayfasında **istemci ayarlarındaki** aralıklı bildirimlerin zaman aralığını tanımlayabilirsiniz. Son geri sayım bildirimi gerçekleşene kadar bir kullanıcının bekleyen bir yeniden başlatma hakkında ne kadar süre boyunca anımsatılması gerektiğini yapılandırmak için **bilgisayar yeniden başlatma geri sayım bildirimleri (dakika) için erteleme süresini belirtin** değerini değiştirin.

Ayrıca, için en büyük değer, kullanıcıya **Kullanıcı oturumu kapatmadan önceki aralığı belirten geçici bir bildirim görüntüler veya bilgisayar yeniden başlatılır (dakika)** , 1440 dakikadan (24 saat) 20160 dakikaya (iki hafta) artar.

Daha fazla bilgi için bkz. [cihaz yeniden başlatma bildirimleri](../../clients/deploy/device-restart-notifications.md) ve [istemci ayarları hakkında](../../clients/deploy/about-client-settings.md#computer-restart).

### <a name="direct-link-to-custom-tabs-in-software-center"></a>Yazılım Merkezi 'nde özel sekmelere doğrudan bağlantı

<!--4655176-->

Artık kullanıcılara yazılım merkezi 'nde [özel bir sekmeye](../../clients/deploy/about-client-settings.md#software-center-tab-visibility) doğrudan bağlantı sağlayabilirsiniz.

Yazılım merkezini belirli bir sekmeye açmak için aşağıdaki URL biçimini kullanın:

`softwarecenter:page=CustomTab1`

Dize, `CustomTab1` sırayla ilk özel sekmedir.

Örneğin, bu URL 'YI Windows **çalıştırma** penceresine yazın.

Software Center 'da varsayılan sekmeleri açmak için de bu söz dizimini kullanabilirsiniz:

|Komut satırı  |Tab  |
|---------|---------|
|`AvailableSoftware`|Uygulamalar|
|`Updates`|Güncelleştirmeler|
|`OSD`|İşletim Sistemleri|
|`InstallationStatus`|Yükleme durumu|
|`Compliance`|Cihaz uyumluluğu|
|`Options`|Seçenekler|

Daha fazla bilgi için bkz. [Software Center sekme görünürlüğü](../../clients/deploy/about-client-settings.md#software-center-tab-visibility).

## <a name="software-updates"></a><a name="bkmk_sum"></a> Yazılım güncelleştirmeleri

### <a name="additional-options-for-wsus-maintenance"></a>WSUS bakımı için ek seçenekler

<!--4110109-->
Artık Configuration Manager, sağlıklı yazılım güncelleştirme noktalarını sürdürmek için çalıştırılabilir ek WSUS bakım görevlerinize sahipsiniz. WSUS Bakımı her eşitlemeden sonra oluşur. WSUS 'de, zaman aşımına uğradı güncelleştirmeleri reddetmeye ek olarak, Configuration Manager artık şunları yapabilir:

- Eski güncelleştirmeleri WSUS veritabanından kaldırın.
- WSUS temizleme performansını geliştirmek için, kümelenmiş olmayan dizinleri WSUS veritabanına ekleyin.

Daha fazla bilgi için bkz. [yazılım güncelleştirmeleri Bakımı](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906).

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>Yazılım güncelleştirmeleri için varsayılan en uzun çalışma süresini yapılandırın

<!--3734426-->

Artık bir yazılım güncelleştirmesi yüklemesinin tamamlaması için en fazla süreyi belirtebilirsiniz. Yazılım güncelleştirme noktasındaki **Maksimum çalıştırma süresi** sekmesinde aşağıdaki öğeleri belirtebilirsiniz:

- **Windows özellik güncelleştirmeleri için maksimum çalışma süresi (dakika)**
- **Windows için Office 365 güncelleştirmeleri ve Özellik dışı güncelleştirmeleri için maksimum çalışma süresi (dakika)**

Daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime).

### <a name="configure-dynamic-update-during-feature-updates"></a>Özellik güncelleştirmeleri sırasında dinamik güncelleştirme 'yi yapılandırma

<!--4062619-->

Windows 10 özellik güncelleştirme yüklemeleri sırasında [dinamik güncelleştirme](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) 'yi yapılandırmak için yeni bir istemci ayarı kullanın. Dinamik güncelleştirme, istemciyi Internet 'ten bu güncelleştirmeleri indirmek üzere yönlendirerek Windows kurulumu sırasında dil paketlerini, istek üzerine, sürücüleri ve toplu güncelleştirmeleri yükler.

Daha fazla bilgi için bkz. [yazılım güncelleştirme istemci ayarları](../../clients/deploy/about-client-settings.md#software-updates) ve [hizmet olarak Windows 'u yönetme](../../../osd/deploy-use/manage-windows-as-a-service.md).

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Yeni Windows 10, sürüm 1903 ve üzeri ürün kategorisi

<!--4682946-->

**Windows 10, sürüm 1903 ve üzeri,** **Windows 10**  ürününün önceki sürümleri gibi bir parçası olmak yerine kendi ürünü olarak Microsoft Update eklenmiştir. Bu değişiklik, istemcilerinizin bu güncelleştirmeleri görmesini sağlamak için birkaç el ile adım uygulamanızı sağlar. Yeni ürün için gerçekleştirmeniz gereken el ile adımların sayısını azaltmaya yardımcı oluk.

Configuration Manager sürüm 1906 ' e güncelleştirdiğinizde ve eşitleme için **Windows 10** ürününün seçili olması halinde, aşağıdaki eylemler otomatik olarak gerçekleşir:

- Eşitleme için **Windows 10, sürüm 1903 ve sonraki** bir ürün eklenmiştir.
- **Windows 10** ürününü Içeren otomatik dağıtım kuralları **, Windows 10, sürüm 1903 ve üstünü**içerecek şekilde güncelleştirilecektir.
- Bakım planları, **Windows 10, sürüm 1903 ve sonraki** bir ürünü içerecek şekilde güncelleştirilir.

Daha fazla bilgi için bkz. eşitlenmek, [bakım planlarını](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)ve [Otomatik dağıtım kurallarını](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) [yapılandırmak için sınıflandırmaları ve ürünleri yapılandırma](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="drill-through-required-updates"></a>Gerekli güncelleştirmeler arasında detaya gitme

<!--4224414-->
Artık belirli bir yazılım güncelleştirmesi gerektiren cihazları görmek için uyumluluk istatistikleri detayına gidebilirsiniz. Cihaz listesini görüntülemek için, cihazların ait olduğu güncelleştirmeleri ve koleksiyonları görüntülemek için izninizin olması gerekir. Cihaz listesinin detayına gitmek için, bir güncelleştirme için **Özet** sekmesinde bulunan pasta grafiğinin yanındaki **istenen köprüyü görüntüle** ' yi seçin. Köprüye tıkladığınızda, güncelleştirme gerektiren cihazları görebileceğiniz **cihazlar** altındaki geçici bir düğüme gidersiniz.

**Gerekli görünüm** Köprüsü aşağıdaki konumlarda kullanılabilir:

   - **Yazılım kitaplığı**  >  **Yazılım güncelleştirmeleri**  >  **Tüm yazılım güncelleştirmeleri**
   - **Yazılım kitaplığı**  >  **Windows 10 Bakımı**  >  **Tüm Windows 10 güncelleştirmeleri**
   - **Yazılım kitaplığı**  >  **Office 365 Istemci yönetimi**  >  **Office 365 güncelleştirmeleri**

Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini izleme](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates), [Windows 'u hizmet olarak yönetme](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates)ve [Microsoft 365 Apps güncelleştirmelerini yönetme](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


## <a name="office-management"></a><a name="bkmk_o365"></a> Office yönetimi

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Office 365 ProPlus yükseltme hazırlığı panosu

<!--4021125-->

Hangi cihazların kuruluş için Microsoft 365 uygulamalarına yükseltilmeye hazır olduğunu belirlemenize yardımcı olmak için, yeni bir hazır olma panosu vardır. Bu, geçerli sürüm 1902 Configuration Manager yayınlanan **Office 365 ProPlus yükseltme hazırlığı** kutucuğunu içerir. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **Office 365 istemci yönetimi**' ni genişletin ve **Office 365 ProPlus yükseltme hazırlığı** düğümünü seçin.

Pano, Önkoşullar ve bu verileri kullanma hakkında daha fazla bilgi için bkz. [Office 365 ProPlus hazırlığı Için tümleştirme](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).


## <a name="protection"></a><a name="bkmk_protect"></a> Korunmasına

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Windows Defender Application Guard dosya güven ölçütleri

<!--3555858-->

Kullanıcıların normalde Windows Defender Application Guard (WDAG) içinde açık olan dosyalara güvenmesini sağlayan yeni bir ilke ayarı vardır. Başarıyla tamamlandıktan sonra dosyalar, WDAG yerine ana bilgisayar cihazında açılır.

Daha fazla bilgi için bkz. [Windows Defender Application Guard Ilkesi oluşturma ve dağıtma](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager konsolu

### <a name="role-based-access-for-folders"></a>Klasörler için rol tabanlı erişim

<!--3600867-->

Artık klasörlerde güvenlik kapsamları ayarlayabilirsiniz. Klasör içindeki bir nesneye erişiminiz varsa ancak klasöre erişiminiz yoksa, nesneyi göremezsiniz. Benzer şekilde, bir klasöre erişiminiz varsa ancak içinde bir nesne yoksa, bu nesneyi görmezsiniz. Bir klasöre sağ tıklayın, **güvenlik kapsamlarını ayarla**' yı seçin ve ardından uygulamak istediğiniz güvenlik kapsamlarını seçin.

Daha fazla bilgi için bkz. [Configuration Manager konsol ipuçları](../../servers/manage/admin-console-tips.md) ve [rol tabanlı yönetimi yapılandırma](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder).

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Cihaz ve cihaz koleksiyonu düğümlerine SMBıOS GUID sütunu Ekle

<!--4526580-->
Hem **cihazlarda** hem de **Cihaz Koleksiyonları** DÜĞÜMLERINDE, artık **SMBIOS GUID**için yeni bir sütun ekleyebilirsiniz. Bu değer, sistem kaynak sınıfının **BIOS GUID** özelliği ile aynıdır. Cihaz donanımı için benzersiz bir tanımlayıcıdır.

### <a name="administration-service-support-for-security-nodes"></a>Güvenlik düğümleri için yönetim hizmeti desteği

<!--4223683-->
Artık Configuration Manager konsolunun bazı düğümlerini Yönetim hizmetini kullanacak şekilde etkinleştirebilirsiniz. Bu değişiklik, konsolunun WMI üzerinden değil, HTTPS üzerinden SMS sağlayıcısıyla iletişim kurmasını sağlar.

Daha fazla bilgi için bkz. [Yönetim hizmeti](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).

> [!Note]
> Sürüm 1906 ' den başlayarak, site özelliklerindeki **Istemci bilgisayar iletişimi** sekmesine artık **iletişim güvenliği**denir.<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>Cihazlar düğümünde koleksiyonlar sekmesi

<!--4616810-->
**Varlıklar ve uyum** çalışma alanında, **cihazlar** düğümüne gidin ve bir cihaz seçin. Ayrıntılar bölmesinde, yeni **koleksiyonlar** sekmesine geçin. Bu sekme, bu cihazı içeren koleksiyonları listeler.

> [!Note]  
> - Bu sekme şu anda **Cihaz Koleksiyonları** düğümünün altındaki cihazlar alt düğümünden kullanılamaz. Örneğin, bir koleksiyondaki **üyeleri gösterme** seçeneğini belirlediğinizde.
> - Bu sekme bazı kullanıcılar için beklendiği gibi doldurulamayabilir. Bir cihazın ait olduğu koleksiyonların tam listesini görmek için, **tam yönetici** güvenlik rolüne sahip olmanız gerekir. Bu bilinen bir sorundur. <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>Uygulamalar düğümündeki görev dizileri sekmesi

<!--4616810-->
**Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin, **uygulamalar** düğümüne gidin ve bir uygulama seçin. Ayrıntılar bölmesinde, yeni **görev dizileri** sekmesine geçin. Bu sekmede, bu uygulamaya başvuran görev sıraları listelenmektedir.

### <a name="show-collection-name-for-scripts"></a>Betikler için koleksiyon adını göster

<!--4616810-->
**İzleme** çalışma alanında **betik durumu** düğümünü seçin. Artık, KIMLIĞE ek olarak **koleksiyon adını** listeler.

### <a name="real-time-actions-from-device-lists"></a>Cihaz listelerinden gerçek zamanlı eylemler

<!--4616810-->
**Varlıklar ve uyum** çalışma alanındaki **cihazlar** düğümü altında cihazların listesini görüntülemenin çeşitli yolları vardır.

- **Varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları** düğümünü seçin. Bir cihaz koleksiyonu seçin ve **üyeleri göstermek**için eylemi seçin. Bu eylem, bu koleksiyon için bir cihaz listesi olan **Devices** düğümünün bir alt düğümünü açar.  

  - Koleksiyon alt düğümü ' nü seçtiğinizde, artık şeridin koleksiyon grubundan **CMPivot** başlatabilirsiniz.  

- **İzleme** çalışma alanında, **dağıtımlar** düğümünü seçin. Bir dağıtım seçin ve Şeritteki **durumu görüntüle** eylemini seçin. Dağıtım durumu bölmesinde, bir cihaz listesine gitmek için toplam varlıklara çift tıklayın.  

  - Bu listede bir cihaz seçtiğinizde, artık **CMPivot** başlatabilir ve şerit 'in cihaz grubundan **betikleri çalıştırabilirsiniz** .  

### <a name="order-by-program-name-in-task-sequence"></a>Görev dizisinde program adına göre sırala

<!--4616810-->
**Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin. Bir görev dizisini düzenleyin ve [paketi Kur](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) adımını seçin ya da ekleyin. Bir pakette birden fazla program varsa, açılan liste artık programları alfabetik olarak sıralar.

### <a name="correct-names-for-client-operations"></a>İstemci işlemleri için doğru adlar

<!--4616810-->
**İzleme** çalışma alanında **istemci işlemleri**' ni seçin. **Sonraki yazılım güncelleştirme noktasına geçiş** işlemi artık düzgün şekilde adlandırılmış.


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Kullanımdan kaldırılan özellikler ve işletim sistemleri

[Kaldırılan ve kullanımdan kaldırılan öğelerde](deprecated/removed-and-deprecated.md)uygulanmadan önce yapılan değişiklikler hakkında bilgi edinin.

Sürüm 1906 aşağıdaki özellikler için desteği bırakır:  

- Yeni Uygulama Kataloğu rolleri yükleyemezsiniz. Güncelleştirilmiş istemciler, Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Daha fazla bilgi için bkz. [plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).

Sürüm 1906 aşağıdaki ürünler için desteği kullanımdan kaldırır:  

- Windows CE 7,0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>Diğer güncelleştirmeler

Bu sürümden itibaren, aşağıdaki özellikler artık ön sürüm değildir:

- [SMS Sağlayıcısı yönetim hizmeti](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Windows Defender Uygulama Denetimi yönetimi](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 1906](https://support.microsoft.com/help/4514258).

Configuration Manager için Windows PowerShell cmdlet 'lerinde yapılan değişiklikler hakkında daha fazla bilgi için bkz. [PowerShell sürüm 1906 sürüm notları](/powershell/sccm/1906-release-notes?view=sccm-ps).

Aşağıdaki güncelleştirme paketi (4517869) konsolunda 1 Ekim 2019 ' den başlayarak sunulmaktadır: [Configuration Manager geçerli dalı, sürüm 1906 Için güncelleştirme paketi](https://support.microsoft.com/help/4517869).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Sonraki adımlar

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
16 Ağustos 2019 itibariyle, sürüm 1906 tüm müşterilerin yüklemesi için genel kullanıma sunulmuştur.

Bu sürümü yüklemeye hazırsanız, [güncelleştirme 1906 ' i yüklemek için](../../servers/manage/checklist-for-installing-update-1906.md) [Configuration Manager güncelleştirmeleri](../../servers/manage/updates.md) ve denetim listesini yükleme bölümüne bakın.

> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanın.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:
>
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)  

Bilinen, önemli sorunlar için bkz. [sürüm notları](../../servers/deploy/install/release-notes.md).

Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist)de gözden geçirin.
