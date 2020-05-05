---
title: Geçiş verileri
titleSuffix: Configuration Manager
description: Bir kaynak hiyerarşisinden Configuration Manager hedef hiyerarşisine veri aktarmayı öğrenin.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718906"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Configuration Manager hiyerarşiler arasında veri geçirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Desteklenen bir kaynak hiyerarşisinden Configuration Manager (geçerli dal) hedef hiyerarşinize veri aktarmak için geçişi kullanın. Bir kaynak hiyerarşisinden veri geçirdiğinizde:  

- Kaynak altyapıdaki site veritabanlarından verilere erişir ve bu verileri geçerli ortamınıza aktarırsınız.  

- Geçiş, kaynak hiyerarşisindeki verileri değiştirmez. Bunun yerine, verileri bulur ve hedef hiyerarşinin veritabanında bir kopyasını depolar.  

Geçiş stratejinizi planlarken aşağıdaki noktaları göz önünde bulundurun:  

- Mevcut bir Configuration Manager 2007 SP2 altyapısını Configuration Manager (geçerli dal) olarak geçirebilirsiniz.  

- Desteklenen verilerin bazılarını veya tümünü bir kaynak sitesinden geçirebilirsiniz.  

- Verileri tek bir kaynak sitesinden hedef hiyerarşisindeki birkaç farklı siteye geçirebilirsiniz.  

- Verileri birden çok kaynak sitesinden hedef hiyerarşisindeki tek bir siteye taşıyabilirsiniz.  


Aşağıdaki videoda, iki genel [geçiş senaryosu](#BKMK_MigrationScenarios)açıklanmaktadır ve gösterilmektedir. Ayrıca, geçiş planlarına Microsoft Azure ekleme seçenekleri de içerir.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a>Tiren  

 Configuration Manager, geçiş sırasında aşağıdaki kavramları ve koşulları kullanır.  

#### <a name="source-hierarchy"></a>Kaynak hiyerarşisi
Configuration Manager desteklenen bir sürümünü çalıştıran ve geçirmek istediğiniz verileri içeren bir hiyerarşi. Geçişi ayarlarken, kaynak hiyerarşinin en üst düzey sitesini belirttiğinizde kaynak hiyerarşisini belirlersiniz. Bir kaynak hiyerarşisi belirledikten sonra hedef hiyerarşisinin en üst düzey sitesi, geçirebileceğiniz verileri belirlemek için belirtilen kaynak sitelerin veritabanından veriler toplar. 

Daha fazla bilgi için bkz. [Kaynak hiyerarşileri](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Kaynak siteler
Hedef hiyerarşinize geçirebileceğiniz verileri içeren kaynak hiyerarşisindeki siteler. 

Daha fazla bilgi için bkz. [kaynak siteler](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Hedef hiyerarşisi
Bir kaynak hiyerarşisinden verilerin içeri aktarılması için geçişin çalıştırıldığı Configuration Manager (geçerli dal) hiyerarşisi.

#### <a name="data-gathering"></a>Veri toplama
Hedef hiyerarşinize geçirebileceğiniz kaynak hiyerarşisindeki bilgilerin belirlenmesini içeren devam eden işlem. Configuration Manager bir zamanlamaya göre kaynak hiyerarşisini denetler. Bu işlem, daha önce geçirdiğiniz ve hedef hiyerarşisinde güncelleştirmek isteyebileceğiniz kaynak hiyerarşisindeki bilgilerin tüm değişikliklerini tanımlar.

Daha fazla bilgi için bkz. [veri toplama](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Geçiş işleri
Geçirilecek belirli nesnelerin yapılandırılması ve daha sonra bu nesnelerin hedef hiyerarşisine geçişinin yönetilmesi işlemi.

Daha fazla bilgi için bkz. [geçiş işi stratejisi planlama](planning-a-migration-job-strategy.md).

#### <a name="client-migration"></a>İstemci geçişi
İstemcilerin kullandığı bilgilerin kaynak site veritabanından hedef hiyerarşisi veritabanına aktarılması işlemi. Bu verilerin geçişinin ardından, cihazlarda istemci yazılımı, hedef hiyerarşisinden istemci yazılımı sürümüne yükseltilir.

Daha fazla bilgi için bkz. [istemci geçiş stratejisi planlama](planning-a-client-migration-strategy.md).

#### <a name="shared-distribution-points"></a>Paylaşılan dağıtım noktaları
Kaynak hiyerarşisinden, geçiş dönemi boyunca hedef hiyerarşiyle paylaştığı Configuration Manager dağıtım noktaları.

Geçiş süresi boyunca, hedef hiyerarşideki sitelere atanan istemciler paylaşılan dağıtım noktalarından içerik alabilir.

Daha fazla bilgi için bkz. [kaynak ve hedef hiyerarşiler arasında dağıtım noktalarını paylaşma](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Geçiş izleme
Geçiş etkinliklerini izleme işlemi. Geçiş ilerlemesini ve başarısını **Yönetim** çalışma alanındaki **geçiş** düğümünden izleyebilirsiniz.

Daha fazla bilgi için bkz. [geçiş etkinliğini Izlemeyi planlama](planning-to-monitor-migration-activity.md).

#### <a name="stop-gathering-data"></a>Veri toplamayı durdur
Kaynak sitelerden veri toplamanın durdurulması işlemi. Kaynak hiyerarşisinden geçiş yapmak için artık verileriniz yoksa veya geçişle ilgili etkinlikleri duraklatmak istiyorsanız, hedef hiyerarşiyi kaynak hiyerarşisinden veri toplamayı durduracak şekilde yapılandırabilirsiniz.

Daha fazla bilgi için bkz. [veri toplama](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Geçiş verilerini temizle
Hedef hiyerarşileri veritabanında bulunan geçiş bilgilerini kaldırarak bir kaynak hiyerarşisinden geçişi sonlandırma işlemi.

Daha fazla bilgi için bkz. [taşımayı tamamlamayı planlama](planning-to-complete-migration.md).



## <a name="typical-workflow"></a>Tipik iş akışı  

Geçiş için bir iş akışı ayarlamak için:

1.  Desteklenen bir kaynak hiyerarşisi belirtin.  

2.  Veri toplamayı ayarlayın. Veri toplama Configuration Manager, kaynak hiyerarşisinden geçirebilen veriler hakkında bilgi toplamasına olanak sağlar.  

     Configuration Manager, veri toplama işlemini durdurana kadar basit bir zamanlamada veri toplama işlemini otomatik olarak tekrarlar. Varsayılan olarak, veri toplama işlemi her dört saatte bir yinelenir, böylece Configuration Manager kaynak hiyerarşisindeki verilerde yapılan değişiklikleri tanımlayabilir. Dağıtım noktalarını paylaşmak için veri toplama de gereklidir.  

3.  Kaynak ve hedef hiyerarşileri arasında veri geçişini sağlamak için geçiş işleri oluşturun.  

4.  Veri toplamayı **Durdur** eylemini kullanarak istediğiniz zaman veri toplama işlemini durdurabilirsiniz. Veri toplamayı durdurduğunuzda Configuration Manager artık kaynak hiyerarşideki verilerde yapılan değişiklikleri tanımlamaz ve artık dağıtım noktalarını paylaşamaz. Genelde bu eylemi, artık kaynak hiyerarşisinden veri geçirmeyi veya dağıtım noktaları paylaşmayı planlamadığınızda kullanırsınız.  

5.  İsteğe bağlı olarak, veri toplama işlemi kaynak hiyerarşisi için tüm sitelerde durdurulduktan sonra, geçiş **verilerini temizle** eylemini kullanarak geçiş verilerini temizleyebilirsiniz. Bu eylem, kaynak hiyerarşisinden hedef hiyerarşinin veritabanından geçiş hakkındaki geçmiş verileri siler.  

Verileri taşıdıktan sonra ortamınızda cihazları yönetmek için kaynak hiyerarşisine ihtiyacınız kalmadığında, kaynak hiyerarşisinin ve altyapının yetkisini alabilirsiniz.  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a>Larla  

 Configuration Manager aşağıdaki geçiş senaryolarını destekler:
- [Configuration Manager 2007 hiyerarşilerinden geçiş](#bkmk_2007)  
- [Configuration Manager 2012 veya başka bir Configuration Manager hiyerarşisinden geçiş](#bkmk_2012)

> [!NOTE]  
>  Tek başına sitesi olan bir hiyerarşinin, merkezi yönetim sitesine sahip bir hiyerarşiye genişletilmesi, geçiş olarak sınıflandırilmez. Hiyerarşi genişletme hakkında bilgi için bkz. [tek başına birincil siteyi genişletme](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a>Configuration Manager 2007 hiyerarşilerinden geçiş  

 Configuration Manager 2007 ' den veri geçirmek için geçiş kullandığınızda, yatırımınızı var olan site altyapınızda tutabilir ve aşağıdaki avantajları elde edebilirsiniz:  

#### <a name="site-database-improvements"></a>Site veritabanı geliştirmeleri
Configuration Manager (geçerli dal) veritabanı tam Unicode 'U destekler.

#### <a name="database-replication-between-sites"></a>Siteler arasında veritabanı çoğaltma
Configuration Manager (geçerli dal) çoğaltma Microsoft SQL Server tabanlıdır. Bu davranış, siteden siteye veri aktarımı performansını geliştirir.

#### <a name="user-centric-management"></a>Kullanıcı merkezli yönetim
Kullanıcılar Configuration Manager (geçerli dal) içindeki yönetim görevlerinin odaklanmaktadır. Örneğin, bu kullanıcının cihaz adını bilmiyor olsanız bile, bir kullanıcıya yazılım dağıtabilirsiniz. Ayrıca, Configuration Manager kullanıcılara cihazlara hangi yazılımların yüklendiği ve bu yazılımın ne zaman yüklendiği hakkında daha fazla denetim sağlar.

#### <a name="hierarchy-simplification"></a>Hiyerarşi basitleştirmesi
Configuration Manager (geçerli dal) daha basit bir site hiyerarşisi oluşturmanızı sağlar. Bu geliştirme, merkezi yönetim sitesi türünün ve birincil ve ikincil sitelerin davranışında yapılan değişikliklerin sunumundan kaynaklanır. Configuration Manager (geçerli dal), daha az ağ bant genişliği kullanır ve önceki sürümlerden daha az sunucu gerektirir.

#### <a name="role-based-administration"></a>Rol tabanlı yönetim
Configuration Manager (geçerli dal) içindeki bu merkezi güvenlik modeli, yönetim ve iş gereksinimlerinize karşılık gelen hiyerarşi genelinde güvenlik ve yönetim sunar.

> [!NOTE]  
>  System Center 2012 Configuration Manager 'da ilk olarak tanıtılan tasarım değişiklikleri nedeniyle, Configuration Manager 2007 ' i Configuration Manager (geçerli dal) sürümüne yükseltemezsiniz. Yerinde yükseltme, System Center 2012 Configuration Manager Configuration Manager (geçerli dal) tarafından desteklenir.  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a>Configuration Manager 2012 veya başka bir Configuration Manager hiyerarşisinden geçiş  
 System Center 2012 Configuration Manager veya Configuration Manager hiyerarşisinden veri geçirme işlemi aynıdır. Bu işlem, birden çok kaynak hiyerarşideki verilerin tek bir hedef hiyerarşiye geçirilmesini içerir. Şirketiniz zaten Configuration Manager tarafından yönetilen ek kaynakları aldığında bu işlemi kullanabilirsiniz. Ayrıca, bir test ortamından Configuration Manager üretim ortamınıza veri geçirebilirsiniz. Bu işlem, Configuration Manager test ortamında yatırımınızı korumanıza olanak sağlar.  



## <a name="see-also"></a>Ayrıca bkz.  

-   [Configuration Manager geçiş planlaması](planning-for-migration.md)  

-   [Geçiş için kaynak hiyerarşileri ve kaynak siteleri yapılandırma](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Geçiş işlemleri](operations-for-migration.md)  

-   [Geçiş için güvenlik ve gizlilik](security-and-privacy-for-migration.md)  

-   [Configuration Manager kullanmaya başlama](../servers/deploy/start-using.md)
