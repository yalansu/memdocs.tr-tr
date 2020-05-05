---
title: 1606 için denetim listesi
titleSuffix: Configuration Manager
description: 1511 veya 1602 sürümünü 1606 sürümüne Configuration Manager güncelleştirmeden önce gerçekleştirilecek eylemler hakkında bilgi edinin.
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 95da730a6978c235fcae6a1d05b7984486abdaeb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723085"
---
# <a name="checklist-for-installing-update-1606-for-configuration-manager"></a>Configuration Manager için güncelleştirme 1606 yükleme denetim listesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için sürüm 1606, sürüm 1511 ' den veya 1602 ' den güncelleştirmek için kullanabileceğiniz bir güncelleştirmedir.

Güncelleştirme olarak 1606 sürümünü yüklemeden önce, güncelleştirmeyi başlatmadan önce gerçekleştirilecek eylemler için aşağıdaki bilgileri ve denetim listesini gözden geçirin.

Temel sürümler hakkında daha fazla bilgi için, [Configuration Manager güncelleştirmelerde](../../../core/servers/manage/updates.md) [temel ve güncelleştirme sürümleri](../../../core/servers/manage/updates.md#bkmk_Baselines) bölümüne bakın.

## <a name="about-installing-update-1606"></a>Güncelleştirme 1606 ' i yükleme hakkında

*Güncelleştirme*olarak, 1606 yalnızca hiyerarşinizin en üst düzey sitesine yüklenebilir. Bu, bir veya tek başına birincil siteniz varsa merkezi yönetim sitenizden yüklemeyi başlattığınız anlamına gelir.  

- Alt birincil siteler güncelleştirmeyi merkezi yönetim sitesi yüklemeyi tamamladıktan sonra otomatik olarak yükler. Bir sitenin güncelleştirmeleri ne zaman yüklediğinden denetlemek için hizmet pencerelerini kullanabilirsiniz. Sürüm 1606 ' den önce, hizmet pencereleri bakım pencereleri olarak adlandırılmıştı. Daha fazla bilgi için bkz. [site sunucuları Için hizmet pencereleri](service-windows.md).  

- İkincil siteleri, birincil üst site güncelleştirmeyi yüklemeyi tamamladıktan sonra Configuration Manager konsolunun içinden el ile güncelleştirmeniz gerekir. İkincil site sunucularının otomatik güncelleştirilmesi desteklenmemektedir.  

Site sunucusu güncelleştirmeyi yüklediğinde, site sunucusunda yüklü olan ve uzak bilgisayarlara yüklenen site sistem rolleri otomatik olarak güncelleştirilir. Bu nedenle, güncelleştirmeyi yüklemeden önce, her site sistem sunucusunun yeni güncelleştirme sürümüne sahip işlemler için yeni önkoşulları karşıladığından emin olun.  

Güncelleştirme yüklendikten sonra Configuration Manager konsolunu ilk kez kullandığınızda, bu konsolu güncelleştirmeniz istenir.  Bunu yapmak için, konsolunu barındıran bilgisayarda Configuration Manager kurulumunu çalıştırmanız ve ardından Konsolu güncelleştirme seçeneğini seçmeniz gerekir. Konsolu güncelleştirmeyi ertelememenizi öneririz.

**Bu güncelleştirme için bilinen sorunlar**   
Güncelleştirme paketi yükleme durumunu görüntülediğinizde aşağıdaki sorunlar geçerlidir:
- Sürüm 1602 ' den 1606 ' ye güncelleştirme yaparken, **güncelleştirme paketi yük Ayıkla** adımı, yükleme tamamlansa bile **başlatılmamış**durumunu gösterir.
- 1511 sürümünden 1606 sürümüne güncelleştirme yaparken bazı adımlarda **tamamlandı** durumu gösterilir ancak **son güncelleştirme zamanı**için bir değer görüntülenmez.


## <a name="checklist"></a>Denetim Listesi  

**Tüm sitelerin Configuration Manager desteklenen bir sürümünü çalıştırdığından emin olun:**  Güncelleştirme 1606 ' yi yüklemeye başlamadan önce, hiyerarşideki her site sunucusunun aynı Configuration Manager sürümünü çalıştırması gerekir: sürüm 1511 veya 1602.

**Site sistem sunucularındaki yüklü Microsoft.NET sürümlerini gözden geçirin:** Bir site güncelleştirme 1606 ' yi yüklediğinde, Configuration Manager aşağıdaki site sistemi rollerinin birini barındıran her bilgisayara otomatik olarak .NET Framework 4.5.2 yüklenir (.NET Framework 4,5 veya daha sonraki bir sürümü zaten yüklenmemişse):  

- Kayıt proxy noktası  

- Kayıt noktası  

- Yönetim noktası  

- Hizmet bağlantı noktası  

Bu yükleme, site sistem sunucusunu bir önyükleme bekleme durumuna alabilir ve hataları Configuration Manager bileşeni durum görüntüleyicisine bildirebilir. Ayrıca, sunucudaki .NET uygulamalarında sunucu yeniden başlatılana kadar düzensiz hatalar oluşabilir.  

Daha fazla bilgi için bkz. [site ve site sistemi önkoşulları](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

**Siteyi ve hiyerarşi durumunu gözden geçirin ve çözülmemiş hiçbir sorun kalmadığından emin olun** : Bir siteyi güncelleştirmeden önce site sunucusunun, site veritabanı sunucusunun ve uzak bilgisayarlara yüklü site sistem rollerinin tüm çalışma sorunlarını çözün. Bir site güncelleştirmesi mevcut çalışma sorunları nedeniyle başarısız olabilir.

Daha fazla bilgi için bkz. [Configuration Manager uyarıları ve durum sistemini kullanma](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

**Siteler arasında dosya ve veri çoğaltmayı gözden geçirin**  :  Siteler arasında dosya ve veritabanı çoğaltmasının çalışır durumda ve güncel olduğundan emin olun. Her iki durumda da gecikme veya biriktirme listesi sorunsuz, başarılı bir güncelleştirmeyi engelleyebilir.    

Veritabanı çoğaltmasında, güncelleştirmeyi başlatmadan önce sorunları çözmeye yardımcı olması için Çoğaltma Bağlantısı Analizcisi’ni kullanabilirsiniz. Daha fazla bilgi için [Çoğaltma Bağlantısı Çözümleyicisi hakkında](monitor-replication.md#BKMK_RLA)bölümüne bakın.  


**Siteyi, site veritabanı sunucusunu ve uzak site sistemi rollerini barındıran bilgisayarlara işletim sistemleri için geçerli tüm kritik güncelleştirmeleri yükler:** Configuration Manager için bir güncelleştirme yüklemeden önce, ilgili her site sistemi için tüm kritik güncelleştirmeleri yükleyebilirsiniz. Yüklediğiniz bir güncelleştirme yeniden başlatma gerektirirse, yükseltmeyi başlatmadan önce ilgili bilgisayarları yeniden başlatın.  

**Birincil sitelerdeki yönetim noktaları için veritabanı çoğaltmalarını devre dışı bırak:** Configuration Manager, etkin yönetim noktaları için bir veritabanı çoğaltması olan bir birincil siteyi başarıyla güncelleştiremiyor. Configuration Manager için bir güncelleştirme yüklemeden önce veritabanı çoğaltmasını devre dışı bırakın.  

Daha fazla bilgi için bkz. [Configuration Manager için yönetim noktaları Için veritabanı çoğaltmaları](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**SQL Server AlwaysOn kullanılabilirlik grupları 'nı el ile yük devretmeye ayarla:**  
Sürüm 1606 gibi güncelleştirmeleri yüklemeden önce kullanılabilirlik grubunun el ile yük devretmeye ayarlandığından emin olun. Site güncelleştirildikten sonra, yük devretmeyi otomatik olarak geri yükleyebilirsiniz. Daha fazla bilgi için bkz. [site veritabanı Için AlwaysOn SQL Server](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**NLBs kullanan yazılım güncelleştirme noktalarını yeniden yapılandırın:** Configuration Manager, yazılım güncelleştirme noktalarını barındırmak için Ağ Yükü Dengeleme (NLB) kümesi kullanan bir siteyi güncelleştiremez.  

Yazılım güncelleştirme noktaları için NLB kümeleri kullanıyorsanız, NLB kümesini kaldırmak için Windows PowerShell 'i kullanın.    

Daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md).  

**Bu sitede güncelleştirme yüklemesi süresince her bir sitedeki tüm site bakım görevlerini devre dışı bırakın:** Güncelleştirmeyi yüklemeden önce güncelleştirme işleminin etkin olduğu süre boyunca çalışabilecek tüm site bakım görevlerini devre dışı bırakın. Bunlara diğerlerinin yanında aşağıdakiler dahildir:  

- Site Sunucusunu Yedekle  

- Eski İstemci İşlemlerini Sil  

- Eski Bulma Verilerini Sil  

Bir site veritabanı bakım görevi güncelleştirme yüklemesi sırasında çalıştığında güncelleştirme yüklemesi başarısız olabilir. Bir görevi devre dışı bırakmadan önce, güncelleştirme yüklendikten sonra yapılandırmasını geri yükleyebilmek için görevin zamanlamasını kaydedin.  

Daha fazla bilgi için bkz. [Configuration Manager Için bakım görevleri](../../../core/servers/manage/maintenance-tasks.md) ve [Configuration Manager bakım görevleri için başvuru](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Configuration Manager sunucularındaki tüm virüsten koruma yazılımlarını geçici olarak durdurun:** Bir siteyi güncelleştirmeden önce, Configuration Manager sunucularında virüsten koruma yazılımını durdurduğundan emin olun. <!--SMS.503481--> 

**Merkezi yönetim sitesinde ve birincil sitelerden site veritabanının bir yedeğini oluşturun** : Bir siteyi güncelleştirmeden önce, olağanüstü durum kurtarmasında kullanacak başarılı bir yedeğiniz olduğundan emin olmak için site veritabanını yedekleyin.   

Daha fazla bilgi için bkz. [Configuration Manager Için Yedekleme ve kurtarma](backup-and-recovery.md).  

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

- You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

- Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

- A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

- Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

- If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**İstemci pilleyici Için plan yapın:** İstemciyi güncelleştiren bir güncelleştirme yüklediğinizde, bu yeni istemci güncelleştirmesini, tüm etkin istemcilerinizi dağıtmadan ve yükseltibir ön üretim ortamında test edebilirsiniz.   

Bu seçenekten yararlanmak için, güncelleştirme yüklemesine başlamadan önce sitenizi üretim öncesi için Otomatik yükseltmeleri destekleyecek şekilde yapılandırmanız gerekir. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../../../core/clients/manage/upgrade/upgrade-clients.md) ve   
[Bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**Site sunucularının güncelleştirmeleri ne zaman yükleyeceğini denetlemek için hizmet pencerelerini kullanmayı planlayın:** Site sunucusu güncelleştirmelerinin yüklenebileceği bir dönem tanımlamak için hizmet pencerelerini kullanabilirsiniz.

Bu olanak, hiyerarşinizdeki sitelerin güncelleştirmeyi yükleme zamanını kontrol etmenizi sağlar.
Sürüm 1606 ' den önce, hizmet pencereleri bakım pencereleri olarak adlandırılmıştı. Daha fazla bilgi için bkz. [site sunucuları Için hizmet pencereleri](service-windows.md).  

**Kurulum önkoşul denetleyicisi 'Ni çalıştırın:**  Güncelleştirme 1606 ' yi yüklemeden önce, önkoşul denetleyicisi 'ni güncelleştirme yüklemesinden bağımsız olarak çalıştırabilirsiniz. Güncelleştirmeyi siteye yüklediğinizde, önkoşul denetleyicisi yeniden çalışır.  

Daha fazla bilgi için bkz. **Adım 3: güncelleştirme yüklemeden önce Önkoşul denetleyicisini çalıştırma** [Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) konu başlığı.  

> [!IMPORTANT]  
> Önkoşul denetleyicisi bağımsız olarak veya bir güncelleştirme yüklemesinin parçası olarak çalıştırıldığında, işlem, site bakım görevlerinde kullanılan bazı ürün kaynak dosyalarını güncelleştirir. Bu nedenle, Önkoşul denetleyicisini çalıştırdıktan sonra ancak 1606 güncelleştirmesini yüklemeden önce, bir site bakım görevi gerçekleştirmeniz gerekirse, CD 'den **setupwpf. exe dosyasını** (Configuration Manager Kurulum) çalıştırın. Site sunucusundaki en son klasör.  

**Güncelleştirme siteleri** : Artık hiyerarşinizin güncelleştirme yüklemesine hazırsınız.  
Güncelleştirmeyi yükleme işlemi ve site bileşenlerini ve site sistem rollerini yeniden yükleme eylemlerinin iş operasyonlarınız üzerinde en az etkisi olacağı durumlarda, her site için normal iş saatleri dışında güncelleştirme yüklemeyi planlamanız önerilir.

Daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](../../../core/servers/manage/updates.md).  
