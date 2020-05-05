---
title: Güncel dala yükselt
titleSuffix: Configuration Manager
description: System Center 2012 Configuration Manager çalıştıran bir siteden ve hiyerarşide başarılı bir yerinde yükseltme çalıştırmaya yönelik adımları öğrenin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717968"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Güncel dala Configuration Manager yükseltin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

System Center 2012 Configuration Manager çalıştıran bir siteden ve hiyerarşide güncel dala Configuration Manager yerinde yükseltme yapın. System Center 2012 Configuration Manager yükseltmeden önce siteleri hazırlamanız gerekir. Bu hazırlık, başarılı bir yükseltmeyi engelleyebilecek belirli konfigürasyonları kaldırmanızı gerektirir. Daha sonra bir tek site dahil edildiğinde yükseltme sırasını izleyin.  

> [!TIP]  
> Configuration Manager sitesi ve hiyerarşi altyapısını yönetirken, *yükseltme*, *güncelleştirme ve güncelleştirme*terimleri, üç *install* ayrı kavram tanımlanmasında kullanılır. Her bir terimin nasıl kullanıldığını öğrenmek için bkz. [yükseltme, güncelleştirme ve yüklemeyi](../../../understand/upgrade-update-install.md)öğrenme.

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a>Yerinde yükseltme yolları  

Aşağıdaki seçenekler şu anda desteklenen yerinde yükseltme yollarıdır:

### <a name="upgrade-to-version-2002"></a>Sürüm 2002 ' e yükseltme

Aşağıdaki ürünleri Configuration Manager *tam lisanslı* bir sürümüne yükseltebilirsiniz, güncel dal sürümü 2002:

- Configuration Manager bir *değerlendirme* yüklemesi, geçerli dal sürümü 2002
- System Center 2012 Configuration Manager hizmet paketi 1
- System Center 2012 Configuration Manager Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager Service Pack 1

Daha fazla bilgi için bkz. [Configuration Manager dalları ve lisanslama hakkında sık sorulan sorular](../../../understand/product-and-licensing-faq.md).

> [!TIP]  
> System Center 2012 Configuration Manager sürümünden güncel dala yükselttiğinizde, Yükseltme işleminizi kolaylaştırabilir. Daha fazla bilgi için, aşağıdakilere bakın:  
>
> - [Temel ve güncelleştirme sürümleri](../../manage/updates.md#bkmk_Baselines)  
> - [CD.Latest klasörü](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>Desteklenmeyen yollar

Aşağıdaki yollar desteklenmez:

- Teknik Önizleme dalını tam lisanslı bir yüklemeye yükseltmek desteklenmez. Technical Preview sürümü yalnızca Technical Preview 'un sonraki bir sürümüne yükseltilebilir.  

- Technical Preview 'dan tam lisanslı bir sürüme geçiş desteklenmez.  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a> Yükseltme denetim listeleri  

Aşağıdaki denetim listeleri, Configuration Manager başarılı bir yükseltme planlaması yapmanıza yardımcı olabilir.  

### <a name="before-you-upgrade"></a>Yükseltmeden önce  

Configuration Manager yükseltmeden önce bu adımları gözden geçirin.

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>System Center 2012 Configuration Manager ortamınızı gözden geçirin

Aşağıdaki Microsoft Desteği makalesinde açıklanan sorunları çözün: [yinelenen yeniden deneme görevi nedeniyle Configuration Manager istemciler her beş saatte bir yeniden yüklenir ve yanlışlıkla istemci yükseltmesine neden olabilir](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Ortamınızın desteklenen konfigürasyonları karşıladığından emin olun

- Site sistem rollerini barındırmak için kullanımdaki sunucu işletim sistemi sürümünü gözden geçirin:  

  - System Center 2012 Configuration Manager tarafından desteklenen bazı eski işletim sistemleri, Configuration Manager geçerli dalı tarafından desteklenmez. Yükseltmeden önce, bu işletim sistemi sürümlerindeki site sistem rollerini kaldırın. Daha fazla bilgi için bkz. [site sistemi sunucuları Için desteklenen işletim sistemleri](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

  - Configuration Manager için önkoşul denetleyicisi, site sunucusunda veya uzak site sistemlerinde site sistem rolleri için önkoşulları doğrulamaz  

- Bir site sistem rolü barındıran her bilgisayar için gerekli önkoşulları gözden geçirin. Örneğin, bir işletim sistemini dağıtmak için, Configuration Manager Windows 10 değerlendirme ve dağıtım seti 'ni (Windows ADK) kullanır. Kurulumu çalıştırmadan önce, site sunucusuna ve SMS Sağlayıcısı örneği çalıştıran her bilgisayara Windows 10 ADK indirmeniz ve kurmanız gerekir.  

Desteklenen platformlar ve önkoşul konfigürasyonları hakkında daha fazla bilgi için bkz. [desteklenen konfigürasyonlar](../../../plan-design/configs/supported-configurations.md).  

Configuration Manager ile Windows ADK kullanma hakkında daha fazla bilgi için bkz. [OS dağıtımı Için altyapı gereksinimleri](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Site ve hiyerarşi durumunu gözden geçirin ve çözümlenmemiş bir sorun olmadığından emin olun

Bir siteyi yükseltmeden önce site sunucusuna, site veritabanı sunucusuna ve uzak bilgisayarlara yüklenen site sistem rollerine ilişkin tüm çalışma sorunlarını çözün. Bir site yükseltmesi mevcut çalışma sorunları nedeniyle başarısız olabilir.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Siteyi, site veritabanı sunucusunu ve uzak site sistemi rollerini barındıran bilgisayarlardaki işletim sistemleri için geçerli tüm kritik güncelleştirmeleri yükler

Bir siteyi yükseltmeden önce tüm ilgili site sistemlerinde kritik güncelleştirmeleri yükleyin. Yüklediğiniz bir güncelleştirme yeniden başlatma gerektirirse, hizmet paketi güncellemesini başlatmadan önce ilgili bilgisayarları yeniden başlatın.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Configuration Manager tarafından desteklenmeyen site sistem rollerini kaldırın

Aşağıdaki site sistem rolleri artık Configuration Manager kullanılmıyor. System Center 2012 Configuration Manager 'den yükseltmeden önce bunları kaldırın:  

- Bant Dışında Yönetim noktası  

- Sistem Durumu Doğrulayıcı noktası  

- Uygulama Kataloğu web sitesi noktası ve Web hizmeti noktası

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Birincil sitelerde yönetim noktaları için veritabanı çoğaltmalarını devre dışı bırak

Configuration Manager, yönetim noktaları için veritabanı çoğaltması olan bir birincil siteyi yükseltemez. Şunları yapmadan önce veritabanı çoğaltmasını devre dışı bırakın:  

- Veritabanı yükseltmesini test etmek için site veritabanının bir yedeğini oluşturmak  

- Üretim sitesini güncel dala Configuration Manager yükseltin  

Daha fazla bilgi için aşağıdaki makalelere bakın:  

- System Center 2012 Configuration Manager: [Yönetim noktaları için veritabanı çoğaltmalarını yapılandırma](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager, geçerli dal: [Yönetim noktaları Için veritabanı çoğaltmaları](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>NLB kullanan yazılım güncelleştirme noktalarını yeniden yapılandırın

Configuration Manager, yazılım güncelleştirme noktalarını barındırmak için Ağ Yükü Dengeleme (NLB) kümesi kullanan bir siteyi yükseltemez.  

Yazılım güncelleştirme noktaları için NLB kümeleri kullanıyorsanız PowerShell kullanarak NLB kümesini kaldırın. (System Center 2012 Configuration Manager SP1 'den itibaren, bir NLB kümesini yapılandırmak için Configuration Manager konsolunda bir seçenek yoktu.)  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Site yükseltmesinin süresi boyunca her bir sitedeki tüm site bakım görevlerini devre dışı bırakın

Configuration Manager ' a yükseltmeden önce, yükseltme işleminin etkin olduğu süre boyunca çalışabilecek tüm site bakım görevlerini devre dışı bırakın. Bu liste aşağıdaki görevlerle sınırlı değildir ancak bunlarla sınırlı değildir:  

- Site Sunucusunu Yedekle  
- Eski İstemci İşlemlerini Sil  
- Eski Bulma Verilerini Sil  

Yükseltme işlemi sırasında bir site veritabanı bakım görevi çalıştırılıyorsa, site yükseltmesi başarısız olabilir.  

Bir görevi devre dışı bırakmadan önce, site yükseltmesi tamamlandıktan sonra yapılandırmasını geri yükleyebilmek için görevin zamanlamasını kaydedin.

Site bakım görevleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:  

- System Center 2012 Configuration Manager: [site işlemleri Için planlama](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager, geçerli dal: [bakım görevleri Için başvuru](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>Kurulum önkoşul denetleyicisi 'ni Çalıştır

Bir siteyi yükseltmeden önce sitenizin önkoşulları karşıladığını doğrulamak için **önkoşul denetleyicisi** ' ni kurulumdan bağımsız olarak çalıştırın. Daha sonra, Siteyi yükselttiğinizde Önkoşul Denetleyicisi tekrar çalışır.  

Bağımsız önkoşul denetimi, siteyi hem geçerli dala hem de uzun vadeli bakım dalına (LTSB) yükseltme için, Configuration Manager değerlendirir. Bazı özellikler LTSB tarafından desteklenmediğinden, **ConfigMgrPrereq. log** dosyasında aşağıdaki örneklerde olduğu gibi girdileri görebilirsiniz:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Güncel dala yükseltmeyi planlıyorsanız, LTSB sürümü için hatalar güvenle yoksayılabilir. Bunlar yalnızca LTSB 'ye yükseltmeyi planlıyorsanız geçerlidir.

Daha sonra, yükseltmeyi yapmak için Configuration Manager Kurulum 'u çalıştırdığınızda, önkoşul denetimi yeniden çalışır. Sitenizi, yüklemeyi seçtiğiniz Configuration Manager dalına (geçerli dal veya LTSB) göre değerlendirir. Geçerli dala yükseltmeyi seçerseniz, LTSB tarafından desteklenmeyen özellikler için denetimi çalıştırmaz.

Daha fazla bilgi için önkoşul [denetleyicisi](prerequisite-checker.md) ve [önkoşul denetimleri listesine](list-of-prerequisite-checks.md)bakın.  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Configuration Manager için önkoşul dosyalarını ve yeniden dağıtılabilir dosyaları indirin

Önkoşul olan yeniden dağıtılabilir dosyaları, dil paketlerini ve Configuration Manager için en son ürün güncelleştirmelerini indirmek için **Kurulum Yükleyici** 'yi kullanın.  

Bilgi için bkz. [Kurulum Yükleyici](setup-downloader.md).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Sunucu ve istemci dillerini yönetmeyi planlayın

Bir siteyi yükselttiğinizde, site yükseltmesi tarafından yalnızca yükseltme sırasında seçtiğiniz dil paketi sürümleri yüklenir.  

- Kurulum, sitenizin geçerli dil yapılandırmasını inceler. Daha sonra, daha önce indirilen önkoşul dosyalarını depoladığınız klasörde bulunan dil paketlerini tanımlar.  

- Geçerli sunucu ve istemci dil paketlerinin seçimini onaylayabilir veya dilleri destek eklemek veya kaldırmak için seçimleri değiştirebilirsiniz.  

- Yalnızca kurulum 'U çalıştırdığınızda kullanılabilen dil paketleri seçilebilir.  

> [!NOTE]  
> Configuration Manager geçerli bir dal sitesi için dilleri etkinleştirmek üzere System Center 2012 Configuration Manager dil paketlerini kullanamazsınız.  

Dil paketleri hakkında daha fazla bilgi için bkz. [dil paketleri](language-packs.md).  

#### <a name="review-considerations-for-site-upgrades"></a>Site yükseltmeleri için gözden geçirme konuları

Bir siteyi yükselttiğinizde, bazı özellikler ve yapılandırmalar varsayılan yapılandırmaya sıfırlanır. Bu ve ilgili değişikliklere hazırlanmanıza yardımcı olması için bkz. [yükseltme konuları](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Merkezi yönetim sitesinde ve birincil sitelerde site veritabanının bir yedeğini oluşturun

Bir siteyi yükseltmeden önce, olağanüstü durum kurtarma için kullanmak üzere başarılı bir yedeğiniz olduğundan emin olmak için site veritabanını yedekleyin.  

Daha fazla bilgi için bkz. [yedekleme ve kurtarma](../../manage/backup-and-recovery.md).  

#### <a name="back-up-a-customized-configurationmof-file"></a>Özelleştirilmiş bir Configuration. mof dosyasını yedekleyin

Donanım envanteri ile kullandığınız veri sınıflarını tanımlamak için özelleştirilmiş bir Configuration. mof dosyası kullanırsanız, bu dosyanın bir yedeğini oluşturun. Yükseltmeden sonra bu dosyayı sitenize geri yükleyin. Daha fazla bilgi için bkz. [donanım envanterini genişletme](../../../clients/manage/inventory/extend-hardware-inventory.md).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Veritabanı yükseltme işlemini en son site veritabanı yedeklemesinin bir kopyasında test etme

Bir Configuration Manager merkezi yönetim sitesini veya birincil siteyi yükseltmeden önce, site veritabanı yükseltme işlemini site veritabanının bir kopyası üzerinde test edin.  

- Site veritabanı yükseltme işlemini test edin. Bir siteyi yükselttiğinizde, site veritabanı değiştirilebilir.  

- Veritabanı yükseltmesini test etme gerekli olmasa da, üretim veritabanınız etkilenmeden önce yükseltme sorunlarını tanımlayabilir  

- Başarısız bir site veritabanı yükseltmesi site veritabanınızı kullanılamaz hale getirebilir ve işlevlerin geri yüklenmesi için site kurtarması gerekebilir  

- -Site veritabanının bir hiyerarşideki siteler arasında paylaşılmasına karşın, o siteyi yükseltmeden önce her geçerli sitedeki veritabanını sınamayı planlayın  

- Bir birincil sitede yönetim noktaları için veritabanı çoğaltmaları kullanıyorsanız, site veritabanı yedeğini almadan önce çoğaltmayı devre dışı bırakın  

Configuration Manager ikincil sitelerin yedeklenmesini veya ikincil site veritabanının test yükseltmesini desteklemez.  

Üretim sitesi veritabanında bir test veritabanı yükseltmesi çalıştırmak desteklenmez. Bunu yaptığınızda site veritabanı yükseltilir ve çalışamaz durumdaki siteniz işlenebilir.  

Daha fazla bilgi için bkz. [Site veritabanı yükseltmesini test etme](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Site sunucusunu ve bir site sistem rolü barındıran her bilgisayarı yeniden başlatın

Son bir güncelleştirme yüklemesinden veya ön koşullardan bekleyen bir eylem olmadığından emin olmak için bu eylemi gerçekleştirin.  

#### <a name="upgrade-sites"></a>Siteleri yükseltin

Hiyerarşideki en üst düzey siteden başlayarak, Configuration Manager kaynak medyasından Setup. exe ' yi çalıştırın.  

En üst düzey site yükseltildikten sonra, her bir alt sitenin yükseltmesine başlayabilirsiniz. Bir sonraki siteyi yükseltmeye başlamadan önce her bir sitenin yükseltmesini doldurun.  

Hiyerarşinizdeki tüm siteler Configuration Manager 'e yükseltilene kadar hiyerarşiniz karma sürüm modunda çalışır.  

Yükseltmenin nasıl çalıştırılacağı hakkında bilgi için bkz. [yükseltme siteleri](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Yükselttikten sonra  

Configuration Manager yükselttikten sonra bu adımları gözden geçirin.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Tek başına Configuration Manager konsolları yükseltme

Varsayılan olarak, bir merkezi yönetim sitesini veya birincil siteyi yükselttiğinizde, yükleme, site sunucusunda yüklü olan Configuration Manager konsolunu da yükseltir. Site sunucusu dışında bir bilgisayarda yüklü olan her konsolu el ile yükseltin.  

> [!TIP]  
> Yükseltme işlemine başlamadan önce tüm açık konsolları kapatın.  

Daha fazla bilgi için bkz. [ınstall Configuration Manager konsolları](install-consoles.md).  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Birincil sitelerdeki yönetim noktaları için veritabanı çoğaltmalarını yeniden yapılandırın

Birincil sitelerde yönetim noktaları için veritabanı çoğaltmaları kullanıyorsanız, siteyi yükseltmeden önce veritabanı çoğaltmalarını kaldırın. Bir birincil siteyi yükselttikten sonra yönetim noktalarının veritabanı çoğaltmalarını yeniden yapılandırın.

Daha fazla bilgi için bkz. [Yönetim noktaları Için veritabanı çoğaltmaları](../configure/database-replicas-for-management-points.md).  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Yükseltmeden önce devre dışı bıraktığınız tüm veritabanı bakım görevlerini yeniden yapılandırın

Yükseltmeden önce bir sitede veritabanı [bakım görevlerini](../../manage/reference-for-maintenance-tasks.md) devre dışı bırakırsanız, yükseltmeden önce yerinde olan ayarların aynısını kullanarak sitedeki bu görevleri yeniden yapılandırın.  

#### <a name="upgrade-clients"></a>İstemcileri yükseltin

Tüm siteleriniz Configuration Manager sürümüne yükselttikten sonra, istemcileri yükseltmeyi planlayın.  

Bir istemciyi yükselttiğinizde geçici istemci yazılımı kaldırılır ve yeni istemci yazılımı sürümü yüklenir. İstemcileri yükseltmek için Configuration Manager tarafından desteklenen herhangi bir yöntemi kullanabilirsiniz.  

> [!TIP]  
> Bir hiyerarşinin en üst düzey sitesini yükselttiğinizde, hiyerarşinin her bir dağıtım noktasındaki istemci yükleme paketi de güncelleştirilir. Birincil bir siteyi yükselttiğinizde, birincil siteden kullanılabilen istemci yükseltme paketi güncelleştirilir.  

Daha fazla bilgi için bkz. [Windows bilgisayarları için istemcileri yükseltme](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a>Yükseltme konuları  

### <a name="automatic-actions"></a>Otomatik eylemler

Configuration Manager yükselttiğinizde, aşağıdaki eylemler otomatik olarak gerçekleşir:  

- Bir site sıfırlaması. Bu eylem tüm site sistem rollerinin yeniden yüklenmesini içerir.  

- Site bir hiyerarşinin en üst düzey sitesiyse hiyerarşideki her dağıtım noktasının istemci yükleme paketini güncelleştirir. Site ayrıca varsayılan önyükleme görüntülerini, Windows değerlendirme ve dağıtım seti 10 ' da yer alan yeni Windows PE sürümünü kullanacak şekilde güncelleştirir. Ancak yükseltme, mevcut medyayı görüntü dağıtımıyla birlikte kullanılmak üzere yükseltmez.  

- Site bir birincil siteyse, o sitenin istemci yükseltme paketini güncelleştirir.  

### <a name="manual-actions-after-an-upgrade"></a>Yükseltmeden sonra el ile gerçekleştirilen eylemler

Bir siteyi yükselttikten sonra aşağıdaki eylemleri gerçekleştirdiğinizden emin olun:  

- İstemcilerin her birincil site yükseltmesine atandığından ve yeni istemci sürümünü yüklediğinizden emin olun  

- Siteye bağlanan ve site sunucusundan uzakta olan bir bilgisayarda çalışan her bir Configuration Manager konsolunu yükseltin  

- Yönetim noktaları için veritabanı çoğaltmaları kullandığınız birincil sitelerde veritabanı çoğaltmalarını yeniden yapılandırın  

- Site yükseltildikten sonra, CD, DVD veya USB flash sürücüler için ISO dosyaları gibi fiziksel medyayı el ile yükseltin. Ayrıca, donanım satıcılarına sunulan önceden hazırlanan medyayı içerir. Site yükseltmesi varsayılan önyükleme görüntülerini güncelleştirir, Configuration Manager dışında kullanılan bu medya dosyalarını veya cihazları yükseltemez.  

- Eski Windows PE sürümüne ihtiyacınız olmadığında özel önyükleme görüntülerini güncelleştirmeyi planlayın.  

### <a name="actions-that-affect-configurations-and-settings"></a>Yapılandırma ve ayarları etkileyen eylemler

Bir site Configuration Manager yükselttiğinde, bazı yapılandırma ve ayarlar yükseltme sonrasında kalıcı olmaz. Bazı konfigürasyonlar yeni bir varsayılan olarak ayarlanır. Aşağıdaki liste, kalıcı olmayan veya değişen bazı ayarları içerir:  

- **Yazılım Merkezi**  
    Aşağıdaki Yazılım Merkezi öğeleri varsayılan değerlerine sıfırlanır:  

  - **İş bilgileri** , **5:00:00:00** ila **10:00Pm** Pazartesi-Cuma arası iş saatlerine sıfırlanır.  

  - **Bilgisayar bakımı** değeri **Bilgisayarım sunu modundayken Software Center etkinliklerini askıya al** olarak sıfırlanır.  

  - **Uzaktan denetim** değeri, bilgisayara atanmış istemci ayarlarındaki değere ayarlanır.  

- **Yazılım güncelleştirme özetleme zamanlamaları**: yazılım güncelleştirmeleri veya yazılım güncelleştirme grupları için özel özetleme zamanlamaları 1 saatlik varsayılan değere sıfırlanır. Yükseltme tamamlandıktan sonra özel özetleme değerlerini gerekli sıklığa sıfırlayın.  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a> Site veritabanı yükseltmesini test etme  

Aşağıdaki bilgiler yalnızca System Center 2012 Configuration Manager gibi önceki bir sürümü yükseltirken geçerli dalı Configuration Manager için geçerlidir.

Bir siteyi yükseltmeden önce, bu sitenin veritabanının bir kopyasını yükseltme için test edin.  

Veritabanını bir yükseltme için test etmek üzere, önce site veritabanının bir kopyasını bir Configuration Manager sitesi barındırmaz bir SQL Server örneğine geri yükleyin. Veritabanı kopyasını barındırmak için kullandığınız SQL Server sürümü Configuration Manager desteklediği bir SQL Server sürümü olmalıdır.  

Site veritabanını geri yükledikten sonra, SQL Server bilgisayarda, Configuration Manager için kaynak medya klasöründen Configuration Manager Kurulum ' u çalıştırın. `/TESTDBUPGRADE` Komut satırı seçeneğini kullanın.  

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Bir Configuration Manager sitesinin yedeğini alma](../../manage/backup-and-recovery.md)  

- [Kurulum için komut satırı seçenekleri](command-line-options-for-setup.md#bkmk_setup)  

- [SQL Server sürümleri desteği](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Microsoft Intune Configuration Manager ile tümleştirirseniz:  
>
> 5 gün veya daha önce oluşturulan site veritabanının kopyasında bir test veritabanı çalıştırdığınızda şu iletilerden birini görebilirsiniz:  
>
> - UYARI: Yükseltme, buluta tam eşitlemeye zorlayacak.  
> - HATA: Veritabanı yükseltmesi buluta tam eşitlemeye zorlayacak.  
>
> Her ikisi de, bir veritabanı yükseltmesi testi sırasında güvenle yoksayılabilir. Test yükseltmesinde bir hata veya sorun göstermez. Bunun yerine, gerçek yükseltme sırasında **bulut** veritabanı çoğaltma grubundaki verilerin Microsoft Intune ile eşitlenebileceğini gösterir.  

### <a name="test-a-site-database-for-upgrade"></a>Site veritabanını yükseltme için test etme  

Yükseltmeyi planladığınız her bir merkezi yönetim sitesi ve birincil site üzerinde aşağıdaki yordamı kullanın:  

1. Site veritabanının bir kopyasını oluşturun. Daha sonra bu kopyayı, site veritabanınız ile aynı sürümü kullanan bir SQL Server örneğine geri yükleyin ve bir Configuration Manager sitesi barındırmaz. Örneğin, site veritabanı SQL Server'ın Enterprise sürümündeki bir örneğinde çalışıyorsa, veritabanını SQL Server'ın aynı zamanda SQL Server Enterprise sürümünü de çalıştıran bir örneğine geri yüklediğinizden emin olun.  

2. Veritabanı kopyasını geri yükledikten sonra, Configuration Manager geçerli dalı için kaynak medyasından kurulum 'U çalıştırın. Kurulum 'U çalıştırdığınızda, `/TESTDBUPGRADE` komut satırı seçeneğini kullanın. Veritabanı kopyasını barındıran SQL Server örneği varsayılan örnek değilse, site veritabanı kopyasını barındıran örneği tanımlamak için komut satırı bağımsız değişkenleri de sağlar.  

    Örneğin, bir site veritabanını SMS_ABC veritabanı adıyla yükseltmeyi planlıyorsunuz. Bu site veritabanının bir kopyasını SQL Server'ın örnek adı DBTest olan desteklenen bir örneğine geri yüklüyorsunuz. Site veritabanının bu kopyasının yükseltmesini test etmek için şu komut satırını kullanın:`Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Setup. exe, Configuration Manager kaynak medyasında aşağıdaki konumdadır:`SMSSETUP\BIN\X64`  

3. Veritabanı yükseltme testini çalıştırdığınız SQL Server örneğinde, sistem sürücüsünün kökündeki ConfigMgrSetup.log dosyasında ilerleme ve başarı durumunu izleyin:  

    - Test yükseltmesi başarısız olursa, site veritabanı yükseltme hatasıyla ilgili tüm sorunları çözün. Ardından, site veritabanının yeni bir yedeğini oluşturun ve site veritabanının yeni kopyasının yükseltmesini test edin.  

    - İşlem başarılı olduktan sonra, veritabanı kopyasını silebilirsiniz.  

        > [!NOTE]  
        > Herhangi bir sitede site veritabanı olarak kullanmak üzere test yükseltmesi için kullandığınız site veritabanının kopyasının geri yüklenmesi desteklenmez.  

Site veritabanının bir kopyasını başarıyla yükselttikten sonra, Configuration Manager sitesinin ve site veritabanının yükseltilmesiyle devam edin.  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a>Siteleri yükselt  

Aşağıdaki görevleri tamamladıktan sonra Configuration Manager sitenizi yükseltmeye hazırsınız:

- Siteniz için yükseltme öncesi yapılandırma
- Site veritabanının yükseltmesini bir veritabanı kopyasında test etme
- Yüklemeyi planladığınız sürüme yönelik önkoşul dosyalarını ve dil paketlerini indirin

Bir hiyerarşideki bir dosyayı yükselttiğinizde, önce hiyerarşinin en üst düzey sitesini yükseltirsiniz. Bu üst düzey site bir merkezi yönetim sitesidir ya da tek başına bir birincil sitedir. Bir merkezi yönetim sitesinin yükseltmesini tamamladıktan sonra, alt birincil siteleri istediğiniz sırayla yükseltebilirsiniz. Bir birincil siteyi yükselttikten sonra, ikincil siteleri yükseltmeden önce bu sitenin alt ikincil sitelerini yükseltebilir veya ek birincil siteleri yükseltebilirsiniz.  

Bir merkezi yönetim sitesini veya birincil siteyi yükseltmek için Configuration Manager kaynak medyasından kurulum 'U çalıştırın. İkincil siteleri yükseltmek için kurulum 'U çalıştırmayın. Bunun yerine, birincil üst sitesini yükseltmeyi tamamladıktan sonra ikincil bir siteyi yükseltmek için Configuration Manager konsolunu kullanırsınız.  

Bir siteyi yükseltmeden önce, site yükseltmesi tamamlanana kadar site sunucusundaki Configuration Manager konsolunu kapatın. Ayrıca, site sunucusu dışındaki bilgisayarlarda çalışan her bir Configuration Manager konsolunu da kapatın. Site yükseltmesi tamamlandıktan sonra konsolu yeniden bağlayabilirsiniz. Ancak, bir Configuration Manager konsolunu yeni Configuration Manager sürümüne yükseltene kadar, bu konsol Configuration Manager yeni sürümünde bulunan bazı nesneleri ve bilgileri görüntüleyemez.  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Bir merkezi yönetim sitesini veya birincil siteyi yükseltme  

1. Kurulumu çalıştıran kullanıcının aşağıdaki güvenlik haklarına sahip olduğunu doğrulayın:  

    - Site sunucusunda yerel **yönetici** hakları  

    - Site veritabanı sunucusu, site sunucusundan uzakta ise, üzerinde yerel **yönetici** hakları vardır.  

2. Site sunucusunda, aşağıdaki programı açın: `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Bu eylem Configuration Manager Kurulum Sihirbazı ' nı açar.  

3. **Başlamadan önce** sayfasındaki bilgileri okuyun ve ardından **İleri**' yi seçin.  

4. **Başlarken** sayfasında **Bu Configuration Manager sitesini Yükselt**' i seçin ve ardından **İleri**' yi seçin.  

5. **Ürün anahtarı** sayfasında:  

    Daha önce Configuration Manager değerlendirmesi yüklediyseniz, **Bu ürünün lisanslı sürümünü yükleme**' yi seçebilirsiniz. Ardından Configuration Manager tam yüklemesi için ürün anahtarınızı girin. Bu eylem, siteyi tam sürüme dönüştürür.  

    Ayrıca, lisans sözleşmenizin **yazılım güvencesi sona erme tarihi** ' ni bu tarih için uygun bir anımsatıcı olarak belirtebilirsiniz. Kurulum sırasında bu değeri girmezseniz, daha sonra Configuration Manager konsolunun içinden belirtebilirsiniz.  

    > [!NOTE]  
    > Microsoft, girdiğiniz sona erme tarihini doğrulamaz ve bu tarihi lisans doğrulaması için kullanmaz. Bunu, sona erme tarihinin bir anımsatıcısı olarak kullanabilirsiniz. Configuration Manager, çevrimiçi olarak sunulan yeni yazılım güncelleştirmelerini düzenli olarak denetler ve yazılım güvencesi lisans durumunuz, bu ek güncelleştirmeleri kullanmaya uygun olması için güncel olmalıdır.

    Daha fazla bilgi için bkz. [lisanslama ve dallar](../../../understand/learn-more-editions.md).

6. **Microsoft yazılımı lisans koşulları** sayfasında, lisans koşullarını okuyup kabul edin ve ardından **İleri**' yi seçin.  

7. **Önkoşul lisanslar** sayfasında, önkoşul olan yazılımın lisans koşullarını okuyup kabul edin ve ardından **İleri**' yi seçin. Kurulum, yazılım yükleme ve gerektiğinde yazılımı site sistemlerine veya istemcilerine otomatik olarak yükler. Sonraki sayfaya devam edebilmeniz için önce tüm koşulları kabul edin.  

8. **Önkoşul İndirmeleri** sayfasında, kurulumun Internet 'ten en son içeriği indirdiğini veya daha önce indirilen dosyaları kullanıp kullanmadığını belirtin. Bu içerik önkoşul yeniden dağıtılabilir dosyalarını, dil paketlerini ve en son ürün güncelleştirmelerini içerir. Kurulum Yükleyici'yi kullanarak dosyaları daha önce yüklediyseniz **Daha önce indirilen dosyaları kullan** 'ı seçip indirme klasörünü belirtin. Daha fazla bilgi için bkz. [Kurulum Yükleyici](setup-downloader.md).  

    > [!NOTE]  
    > Daha önce indirilen dosyaları kullandığınızda, indirme klasörü yolunda dosyaların en yeni sürümlerinin bulunduğunu doğrulayın.  

9. **Sunucu Dili Seçimi** sayfasında, site için halen yüklenmiş olan dillerin listesini görüntüleyin. Configuration Manager konsolu ve raporlar için bu sitede kullanılabilen ek dilleri seçin. Ayrıca, artık bu sitede desteklemek istemediğiniz dilleri temizleyebilirsiniz. Varsayılan olarak Ingilizce seçilidir ve kaldırılamaz.  

    > [!IMPORTANT]  
    > Configuration Manager her sürümü, Configuration Manager önceki bir sürümünden dil paketlerini kullanamaz. Yükselttiğiniz Configuration Manager bir sitede dil desteğini etkinleştirmek için, bu yeni sürüme ait dil paketi sürümünü kullanmanız gerekir. Örneğin, System Center 2012 Configuration Manager Configuration Manager geçerli dala yükseltme sırasında, bir dil paketinin güncel dal sürümü indirdiğiniz önkoşul dosyalarıyla kullanılamazsa, bu dil için destek yükleyemezsiniz.  

10. **İstemci Dili Seçimi** sayfasında, site için halen yüklenmiş olan dillerin listesini görüntüleyin. İstemci bilgisayarlar için bu sitede kullanılabilen diğer dilleri seçin veya bu sitede artık desteklemek istemediğiniz dilleri temizleyin. Mobil cihaz istemciler için tüm istemci dillerinin etkinleştirilip etkinleştirilmeyeceğini belirtin ve **İleri**'ye tıklayın. Varsayılan olarak Ingilizce seçilidir ve kaldırılamaz.  

11. **Ayarlar Özeti** sayfasında, yapılandırmayı gözden geçirin. Hazır olduğunuzda, site yükseltmesi için sunucu hazırlığını doğrulamak üzere önkoşul denetleyicisi ' ni başlatmak için **İleri** ' yi seçin.  

12. **Önkoşul yükleme denetimi** sayfasında, listelenen sorun yoksa siteyi ve site sistemi rollerini yükseltmek için **İleri** ' yi seçin.

    Önkoşul denetleyicisi bir sorun bulursa, sorunun nasıl çözümlendiğine ilişkin ayrıntılar için listeden bir öğe seçin. Kurulum'a devam etmeden önce listede **Hata** durumu gösteren tüm öğeleri düzeltin. Sorunu çözdükten sonra, önkoşul denetimini yeniden başlatmak için **Denetimi Çalıştır** 'a tıklayın. Önkoşul Denetleyicisi'nin sonuçlarını gözden geçirmek için sistem sürücüsünün kökünde bulunan ConfigMgrPrereq.log dosyasını da açabilirsiniz. Günlük dosyası, Kullanıcı arabiriminde görüntülenmeyen ek bilgiler içerebilir. Yükleme önkoşul kuralları ve açıklamalarının bir listesi için bkz. [önkoşul denetleyicisi](list-of-prerequisite-checks.md).

**Yükseltme** sayfasında, Kurulum genel ilerleme durumunu gösterir. Kurulum temel site sunucusu ve site sistemi yüklemesini tamamladığında sihirbazı kapatabilirsiniz. Site yapılandırması arka planda devam eder.  

### <a name="upgrade-a-secondary-site"></a>İkincil bir siteyi yükseltme  

1. Kurulumu çalıştıran yönetici kullanıcının aşağıdaki güvenlik haklarına sahip olduğunu doğrulayın:  

    - İkincil site sunucusunda yerel **yönetici** hakları  

    - Üst birincil sitede **Altyapı Yöneticisi** veya **tam yönetici** güvenlik rolü  

    - İkincil sitenin site veritabanında Sistem Yöneticisi (**sa**) hakları  

2. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

3. Yükseltmek istediğiniz ikincil siteyi seçin. Şeridin **giriş** sekmesinde, **site** grubunda, **Yükselt**' i seçin.  

4. Kararı doğrulamak ve ikincil sitenin yükseltmesini başlatmak için **Evet** ' i seçin.  

İkincil site yükseltmesi arka planda çalışır. Yükseltme tamamlandıktan sonra, Configuration Manager konsolundaki durumu onaylayın. İkincil site sunucusunu seçin, ardından şeridin **giriş** sekmesinde, **site** grubunda, **yüklenen durumu göster**' i seçin.  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a>Yükseltme sonrası görevler  

Bir siteyi yükselttikten sonra, yükseltmeyi tamamlaması veya siteyi yeniden yapılandırmak için ek görevleri gerçekleştirmeniz gerekebilir. Bu görevler aşağıdaki öğeleri içerebilir:

- Configuration Manager istemcilerini yükselt
- Configuration Manager konsolları yükselt
- Yönetim noktaları için veritabanı çoğaltmalarını yeniden etkinleştirin
- Kullandığınız ve yükseltmeden sonra kalıcı olmayan Configuration Manager işlevselliğine yönelik ayarları geri yükleme  
