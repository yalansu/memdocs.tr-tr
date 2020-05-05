---
title: 1602 için denetim listesi
titleSuffix: Configuration Manager
description: 1511 sürümü 1602 sürümüne Configuration Manager güncelleştirmeden önce gerçekleştirilecek eylemler hakkında bilgi edinin.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b330c4049dce06b1e47d1088993b09ec16e724a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717863"
---
# <a name="checklist-for-installing-update-1602-for-configuration-manager"></a>Configuration Manager için güncelleştirme 1602 yükleme denetim listesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Güncelleştirme 1511 ' Configuration Manager den sürüm 1602 ' ye güncelleştirmeden önce, güncelleştirmeye başlamadan önce gerçekleştirilecek eylemler için aşağıdaki bilgileri ve denetim listesini gözden geçirin.  

 **Güncelleştirme 1602’yi yükleme hakkında:**  

 Güncelleştirme 1602, hiyerarşinizin yalnızca en üst düzey sitesine yüklenebilir. Bu, bir veya tek başına birincil siteniz varsa merkezi yönetim sitenizden yüklemeyi başlattığınız anlamına gelir.  

-   Alt birincil siteler güncelleştirmeyi merkezi yönetim sitesi yüklemeyi tamamladıktan sonra otomatik olarak yükler. Bir sitenin güncelleştirmeleri ne zaman yüklediğini denetlemek için bakım pencerelerini kullanabilirsiniz. 1602 güncelleştirmesinin yayımlanmasından başlayarak, bakım pencereleri *hizmet pencereleri*olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [site sunucuları Için hizmet pencereleri](service-windows.md).  

-   İkincil siteleri, birincil üst site güncelleştirmeyi yüklemeyi tamamladıktan sonra Configuration Manager konsolunun içinden el ile güncelleştirmeniz gerekir. İkincil site sunucularının otomatik güncelleştirmeleri desteklenmiyor.  

Site sunucusu güncelleştirmeyi yüklediğinde, site sunucusunda yüklü olan ve uzak bilgisayarlara yüklenen site sistem rolleri otomatik olarak güncelleştirilir. Bu nedenle, güncelleştirmeyi yüklemeden önce, her site sistem sunucusunun yeni güncelleştirme sürümüne sahip işlemler için yeni önkoşulları karşıladığından emin olun.  

Güncelleştirme tamamlandıktan sonra Configuration Manager konsolunu ilk kez kullandığınızda, bu konsolu güncelleştirmeniz istenir. Bunu yapmak için, konsolunu barındıran bilgisayarda Configuration Manager kurulumunu çalıştırmanız ve Konsolu güncelleştirme seçeneğini seçmeniz gerekir. Konsolu güncelleştirmeyi ertelememenizi öneririz.  

 **Liste**  

 **Tüm sitelerin Configuration Manager desteklenen bir sürümünü çalıştırdığından emin olun:**  Güncelleştirme 1602 ' nin yüklemesine başlayabilmeniz için hiyerarşideki her site sunucusu Configuration Manager sürüm 1511 ' i çalıştırmalıdır.  

 **Site sistemi sunucularındaki yüklü Microsoft .NET sürümlerini gözden geçirin:** Bir site güncelleştirme 1602 ' yi yüklediğinde, Configuration Manager aşağıdaki site sistemi rollerinin birini barındıran her bilgisayara otomatik olarak .NET Framework 4.5.2 yüklenir (.NET Framework 4,5 veya daha sonraki bir sürümü zaten yüklenmemişse):  

-   Kayıt proxy noktası  

-   Kayıt noktası  

-   Yönetim noktası  

-   Hizmet bağlantı noktası  

Bu yükleme, site sistem sunucusunu bir önyükleme bekleme durumuna yerleştirebilir ve hata Configuration Manager bileşen durumu görüntüleyicisine bildirir. Ayrıca, sunucu üzerindeki .NET uygulamaları, sunucu yeniden başlatılana kadar rastgele hatalarla karşılaşabilir.  

 Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Siteyi ve hiyerarşi durumunu gözden geçirin ve çözülmemiş hiçbir sorun kalmadığından emin olun** : Bir siteyi güncelleştirmeden önce site sunucusunun, site veritabanı sunucusunun ve uzak bilgisayarlara yüklü site sistem rollerinin tüm çalışma sorunlarını çözün. Bir site güncelleştirmesi mevcut çalışma sorunları nedeniyle başarısız olabilir.  

Daha fazla bilgi için bkz. [Configuration Manager uyarıları ve durum sistemini kullanma](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Siteler arasında dosya ve veri çoğaltmayı gözden geçirin**  :  Siteler arasında dosya ve veritabanı çoğaltmasının çalışır durumda ve güncel olduğundan emin olun. Her iki durumda da gecikme veya biriktirme listesi sorunsuz, başarılı bir güncelleştirmeyi engelleyebilir.    

Veritabanı çoğaltmasında, güncelleştirmeyi başlatmadan önce sorunları çözmeye yardımcı olması için Çoğaltma Bağlantısı Analizcisi’ni kullanabilirsiniz.    

 Daha fazla bilgi için [Çoğaltma Bağlantısı Çözümleyicisi hakkında](monitor-replication.md#BKMK_RLA)bölümüne bakın.  

 **Siteyi, site veritabanı sunucusunu ve uzak site sistemi rollerini barındıran bilgisayarlara işletim sistemleri için geçerli tüm kritik güncelleştirmeleri yükler:** Configuration Manager için bir güncelleştirme yüklemeden önce, ilgili her site sistemi için tüm kritik güncelleştirmeleri yükleyebilirsiniz. Yüklediğiniz bir güncelleştirme yeniden başlatma gerektirirse, yükseltmeyi başlatmadan önce ilgili bilgisayarları yeniden başlatın.  

 **Birincil sitelerdeki yönetim noktaları için veritabanı çoğaltmalarını devre dışı bırak:** Configuration Manager, etkin yönetim noktaları için bir veritabanı çoğaltması olan bir birincil siteyi başarıyla güncelleştiremiyor. Şunları yapmadan önce veritabanı çoğaltmasını devre dışı bırakın:  

-   Veritabanı yükseltmesini test etmek için site veritabanının bir yedeğini oluşturun.  

-   Configuration Manager için bir güncelleştirme yükler.  

Daha fazla bilgi için bkz. [Configuration Manager için yönetim noktaları Için veritabanı çoğaltmaları](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **NLBs kullanan yazılım güncelleştirme noktalarını yeniden yapılandırın:** Configuration Manager, yazılım güncelleştirme noktalarını barındırmak için Ağ Yükü Dengeleme (NLB) kümesi kullanan bir siteyi güncelleştiremez.  Yazılım güncelleştirme noktaları için NLB kümeleri kullanıyorsanız, NLB kümesini kaldırmak için Windows PowerShell 'i kullanın.    

 Daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md).  

 **Bu sitede güncelleştirme yüklemesi süresince her bir sitedeki tüm site bakım görevlerini devre dışı bırakın:** Güncelleştirmeleri yüklemeden önce güncelleştirme işleminin etkin olduğu süre boyunca çalışabilecek tüm site bakım görevlerini devre dışı bırakın. Bu görevler aşağıdakileri içerir (ancak bunlarla sınırlı değildir):  

-   Site Sunucusunu Yedekle  

-   Eski İstemci İşlemlerini Sil  

-   Eski Bulma Verilerini Sil  

Bir site veritabanı bakım görevi güncelleştirme yüklemesi sırasında çalıştığında güncelleştirme yüklemesi başarısız olabilir. Bir görevi devre dışı bırakmadan önce, güncelleştirme yüklendikten sonra yapılandırmayı geri yükleyebilmek için görevin zamanlamasını kaydedin.  

 Daha fazla bilgi için bkz. [Configuration Manager Için bakım görevleri](../../../core/servers/manage/maintenance-tasks.md) ve [Configuration Manager bakım görevleri için başvuru](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Configuration Manager sunucularındaki tüm virüsten koruma yazılımlarını geçici olarak durdurun:** Bir siteyi güncelleştirmeden önce, Configuration Manager sunucularında virüsten koruma yazılımını durdurduğundan emin olun. <!--SMS.503481--> 

 **Merkezi yönetim sitesinde ve birincil sitelerde site veritabanının bir yedeğini oluşturun:** Bir siteyi güncelleştirmeden önce, olağanüstü durum kurtarma için kullanmak üzere başarılı bir yedeğiniz olduğundan emin olmak için site veritabanını yedekleyin.   

Daha fazla bilgi için bkz. [Configuration Manager Için Yedekleme ve kurtarma](backup-and-recovery.md).  

 **Özelleştirilmiş bir Configuration. mof dosyasını yedekleyin:** Donanım envanteri ile kullandığınız veri sınıflarını tanımlamak için özelleştirilmiş bir Configuration. mof dosyası kullanıyorsanız, siteyi güncelleştirmeden önce Bu dosyanın bir yedeğini oluşturun. Güncelleştirmeden sonra bu dosyayı sürüm 1602 sitenize geri yükleyin. Bir siteyi güncelleştirdiğinizde geçerli dosyanın üzerine dosyanın özgün (varsayılan) sürümü yazılır. Bu dosyayı kullanma hakkında daha fazla bilgi için bkz. [donanım envanterini genişletme](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Veritabanı yükseltmesini en son site veritabanı yedeklemesinin bir kopyasında test edin:** Bir Configuration Manager merkezi yönetim sitesini veya birincil siteyi güncelleştirmeden önce, site veritabanı yükseltme işlemini site veritabanının bir kopyası üzerinde test edin.  

-   Bir siteyi yükselttiğinizde site veritabanı değiştirilebildiğinden, site veritabanı yükseltme işlemini test etmelisiniz.  

-   Test veritabanı yükseltmesi gerekli olmamasına rağmen, üretim veritabanınız etkilenmeden önce yükseltme sorunlarını tanımlayabilir.  

-   Başarısız bir site veritabanı yükseltmesi site veritabanınızı kullanılamaz hale getirebilir ve işlevlerin geri yüklenmesi için site kurtarması gerekebilir.  

-   Site veritabanı bir hiyerarşideki siteler arasında paylaşılsa da, siteyi yükseltmeden önce her geçerli sitede veritabanını sınamayı planlayın.  

-   Birincil sitede yönetim noktaları için veritabanı çoğaltmaları kullanıyorsanız, site veritabanının yedeğini oluşturmadan önce çoğaltmayı devre dışı bırakın.  

Configuration Manager ikincil sitelerin yedeklenmesini desteklemez veya ikincil site veritabanının test yükseltmesini desteklemez.   
Üretim sitesi veritabanında bir test veritabanı yükseltmesi çalıştırmayın. Bunun yapılması site veritabanını güncelleştirir ve sitenizi çalışamaz duruma getirebilir. Daha fazla bilgi için bkz. 2. Adım: **konsol içi bir güncelleştirmeyi**yüklemeden önce [bir güncelleştirmeyi yüklemeden önce veritabanı yükseltmesini test](install-in-console-updates.md#bkmk_step2) etme.  

 **İstemci pilleyici Için plan yapın:** İstemciyi güncelleştiren bir güncelleştirme yüklediğinizde, bu yeni istemci güncelleştirmesini, tüm etkin istemcilerinizi dağıtmadan ve yükseltibir ön üretim ortamında test edebilirsiniz.   

 Bu seçenekten faydalanmak için, güncelleştirmeyi yüklemeye başlamadan önce sitenizi üretim öncesi için Otomatik yükseltmeleri destekleyecek şekilde yapılandırmanız gerekir. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../../../core/clients/manage/upgrade/upgrade-clients.md) ve   
[Bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Site sunucularının güncelleştirmeleri ne zaman yükleyeceğini denetlemek Için bakım pencerelerini kullanmayı planlayın:** Bakım pencerelerini, site sunucusundaki güncelleştirmelerin yüklenebileceği bir süre tanımlamak için kullanabilirsiniz. Bu olanak, hiyerarşinizdeki sitelerin güncelleştirmeyi yükleme zamanını kontrol etmenizi sağlar.   

1602 güncelleştirmesinin yayımlanmasından başlayarak, bakım pencereleri *hizmet pencereleri*olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [site sunucuları Için hizmet pencereleri](service-windows.md).  

 **Kurulum önkoşul denetleyicisi 'Ni çalıştırın:**  Güncelleştirme 1602 ' yi yüklemeden önce, önkoşul denetleyicisi 'ni güncelleştirme yüklemesinden bağımsız olarak çalıştırabilirsiniz. Güncelleştirmeyi siteye yüklediğinizde, önkoşul denetleyicisi yeniden çalışır.  

Daha fazla bilgi için bkz. **Adım 3: güncelleştirme yüklemeden önce Önkoşul denetleyicisini çalıştırma** [Configuration Manager](../../../core/servers/manage/updates.md) konu başlığı.  

> [!IMPORTANT]  
>  Önkoşul denetleyicisi bağımsız olarak veya bir güncelleştirme yüklemesinin parçası olarak çalıştırıldığında, işlem, site bakım görevlerinde kullanılan bazı ürün kaynak dosyalarını güncelleştirir. Bu nedenle, Önkoşul denetleyicisini çalıştırdıktan sonra ancak 1602 güncelleştirmesini yüklemeden önce, bir site bakım görevi gerçekleştirmeniz gerekirse, CD 'den **Setupwfe. exe dosyasını** (Configuration Manager Kurulum) çalıştırın. Site sunucusundaki en son klasör.  

 **Güncelleştirme siteleri** : Artık hiyerarşinizin güncelleştirme yüklemesine hazırsınız. Güncelleştirmeyi yükleme işlemi ve site bileşenlerini ve site sistem rollerini yeniden yükleme eylemlerinin iş operasyonlarınız üzerinde en az etkisi olacağı durumlarda, her site için normal iş saatleri dışında güncelleştirme yüklemeyi planlamanız önerilir.

Daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Ayrıca bkz.  
 [Configuration Manager güncelleştirmeleri](../../../core/servers/manage/updates.md)
