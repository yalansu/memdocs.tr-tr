---
title: 1706 için denetim listesi
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1706 ' e güncelleştirmeden önce gerçekleştirilecek eylemler hakkında bilgi edinin.
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7def067e-845c-4db3-9d56-fa1dcf2fd7c7
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a51eefa1362af0c15932d38cdff31e2c3777f303
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723309"
---
# <a name="checklist-for-installing-update-1706-for-configuration-manager"></a>Configuration Manager için güncelleştirme 1706 yükleme denetim listesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli Configuration Manager dalını kullandığınızda, hiyerarşinizi önceki bir sürümden güncelleştirmek için sürüm 1706 ' e yönelik konsol içi güncelleştirmeyi yükleyebilirsiniz.

Sürüm 1706 güncelleştirmesini almak için, hiyerarşinizin en üst düzey sitesinde bir hizmet bağlantı noktası site sistemi rolü kullanmanız gerekir. Bu, çevrimiçi veya çevrimdışı modda olabilir. Hiyerarşiniz Microsoft 'tan güncelleştirme paketini indirdikten sonra, bu dosyayı konsolunda **Yönetim &gt; genel bakış &gt; Cloud Services &gt; güncelleştirmeler ve bakım**altında bulabilirsiniz.

-   Güncelleştirme **kullanılabilir**olarak listelendiğinde güncelleştirme yüklenmeye hazırdır. Sürüm 1706 ' ü yüklemeden önce [güncelleştirme 1706](#about-installing-update-1706) ' yi yükleme ve güncelleştirme işlemine başlamadan önce yapılacak yapılandırmaların [Denetim listesi](#checklist) hakkında aşağıdaki bilgileri gözden geçirin.

-   Güncelleştirme, **indirme** olarak görüntüleniyorsa ve değişmezse, hata için **HMAN. log** ve **DMPDownloader. log** ' u gözden geçirin.

    -   DMPDownloader. log, DMPDownloader işleminin uyku modunda olduğunu ve güncelleştirmeleri denetlemeden önce bir Aralık bekleyip bekdiğini gösteriyorsa, güncelleştirme yeniden dağıtım dosyalarının indirilmesini yeniden başlatmak için site sunucusunda **SMS_Executive** hizmetini yeniden başlatabilirsiniz.

    -   Proxy sunucu ayarları, ve ' `silverlight.dlservice.microsoft.com` `download.microsoft.com`den indirmelere engel olduğunda başka bir yaygın yükleme sorunu oluşur.

Güncelleştirmeleri yükleme hakkında daha fazla bilgi için bkz. [konsol içi güncelleştirmeler ve bakım](updates.md#bkmk_inconsole).

Güncel Dalı sürümleri hakkında bilgi için, bkz. [Configuration Manager güncelleştirmelerinde](updates.md) [temel ve güncelleştirme sürümleri](updates.md#bkmk_Baselines) .

## <a name="about-installing-update-1706"></a>Güncelleştirme 1706 ' i yükleme hakkında

**Barındıra**  
Güncelleştirme 1706, hiyerarşinizin en üst düzeyindeki siteye yüklenir. Bu, bir veya tek başına birincil siteniz varsa merkezi yönetim sitenizden yüklemeyi başlattığınız anlamına gelir. Güncelleştirme üst katman sitesinde yüklendikten sonra, alt siteler aşağıdaki güncelleştirme davranışına sahiptir:

-   Alt birincil siteler güncelleştirmeyi merkezi yönetim sitesi yüklemeyi tamamladıktan sonra otomatik olarak yükler. Bir sitenin güncelleştirmeyi ne zaman yüklei denetlemek için hizmet pencerelerini kullanabilirsiniz. Daha fazla bilgi için bkz. [site sunucuları Için hizmet pencereleri](service-windows.md).

-   Birincil üst site güncelleştirme yüklemesini tamamladıktan sonra, tüm ikincil siteleri Configuration Manager konsolunun içinden el ile güncelleştirmeniz gerekir. İkincil site sunucularının otomatik güncelleştirilmesi desteklenmemektedir.

**Site sistemi rolleri:**  
Bir site sunucusu güncelleştirmeyi yüklediğinde, site sunucusu bilgisayarında yüklü olan ve uzak bilgisayarlara yüklenen site sistem rolleri otomatik olarak güncelleştirilir. Güncelleştirmeyi yüklemeden önce, her site sistem sunucusunun yeni güncelleştirme sürümüyle işlem önkoşullarını karşıladığından emin olun.

**Configuration Manager konsolları:**   
Güncelleştirme tamamlandıktan sonra Configuration Manager konsolunu ilk kez kullandığınızda, bu konsolu güncelleştirmeniz istenir. Bunu yapmak için, konsolunu barındıran bilgisayarda Configuration Manager kurulumunu çalıştırmanız ve ardından Konsolu güncelleştirme seçeneğini seçmeniz gerekir. Konsolu güncelleştirmeyi ertelememenizi öneririz.

> [!IMPORTANT]  
> Merkezi yönetim sitesinde bir güncelleştirme yüklediğinizde, tüm alt birincil siteler güncelleştirme yüklemesini de tamamlayana kadar aşağıdaki sınırlamalara ve gecikmelerden haberdar olun:    
> - **İstemci yükseltmeleri** başlamaz. Bu, istemcilerin ve ön üretim istemcilerinin otomatik güncelleştirmelerini içerir. Ayrıca, son site güncelleştirme yüklemesini tamamlana kadar üretim öncesi istemcileri üretime yükseltemede olursunuz. Son site güncelleştirme yüklemesini tamamladıktan sonra, istemci yükseltmeleri yapılandırma seçimlerinize bağlı olarak başlayacaktır.   
> - Güncelleştirme ile etkinleştirdiğiniz **yeni özellikler** kullanılamaz. Bunun nedeni, bu özellik ile ilgili verilerin çoğaltılmasını, bu özellik için henüz desteği yüklememiş bir siteye gönderilmesini önlemektir. Tüm birincil siteler güncelleştirmeyi yükledikten sonra özellik kullanıma sunulacaktır.   
> - Merkezi Yönetim sitesi ve alt birincil siteleri arasındaki **çoğaltma bağlantıları** yükseltilmeyen olarak görüntülenir. Bu, güncelleştirme paketi yükleme durumu ' nu, çoğaltma başlatmayı Izleme için uyarıyla tamamlandı durumu olarak gösterir. Konsolunun Izleme düğümünde bu, *bağlantı yapılandırılmakta*olarak görüntülenir.


## <a name="checklist"></a>Denetim Listesi

**Tüm sitelerin 1706 güncelleştirmesini destekleyen bir Configuration Manager sürümünü çalıştırdığından emin olun:**   
Güncelleştirme 1706 ' i yüklemeye başlayabilmeniz için hiyerarşideki her site sunucusu aynı Configuration Manager sürümünü çalıştırmalıdır. 1706 sürümüne güncelleştirmek için 1606, 1610 veya 1702 sürümünü kullanmanız gerekir.

**Yazılım Güvencesi veya eşdeğer abonelik haklarınızın durumunu gözden geçirin:**   
Güncelleştirme 1706 ' ü yüklemek için etkin bir yazılım güvencesi (SA) anlaşmanız olmalıdır. Bu güncelleştirmeyi yüklediğinizde **lisanslama** sekmesi, **yazılım güvencesi sona erme tarihini**onaylama seçeneğini sunar.

Bu, lisans sona erme tarihi için uygun bir anımsatıcı olarak belirtebileceğiniz isteğe bağlı bir değerdir. Gelecekteki güncelleştirmeleri yüklediğinizde bu tarih görülebilir. Daha önce bu değeri kurulum veya güncelleştirme yükleme sırasında veya **hiyerarşi ayarlarının** **lisans** sekmesini kullanarak Configuration Manager konsolundan belirtmiş olabilirsiniz.

Daha fazla bilgi için bkz. [Configuration Manager Için lisanslama ve dallar](../../understand/learn-more-editions.md).

**Site sistemi sunucularındaki yüklü Microsoft .NET sürümlerini gözden geçirin:** Bir site bu güncelleştirmeyi yüklediğinde Configuration Manager, .NET Framework 4,5 veya sonraki bir sürümü zaten yüklü olmadığında aşağıdaki site sistemi rollerinden birini barındıran her bilgisayara otomatik olarak .NET Framework 4.5.2 yüklenir:

-   Kayıt proxy noktası
-   Kayıt noktası
-   Yönetim noktası
-   Hizmet bağlantı noktası

Bu yükleme, site sistem sunucusunu bir önyükleme bekleme durumuna alabilir ve hataları Configuration Manager bileşeni durum görüntüleyicisine bildirebilir. Ayrıca, sunucu üzerinde .NET uygulamaları, sunucu yeniden başlatılana kadar rastgele hatalarla karşılaşabilir.

Daha fazla bilgi için bkz. [site ve site sistemi önkoşulları](../../plan-design/configs/site-and-site-system-prerequisites.md).

Windows **10 Için Windows değerlendirme ve dağıtım seti 'nin (ADK) sürümünü gözden geçirin** Windows 10 ADK sürüm 1703 veya üzeri olmalıdır. (Desteklenen Windows ADK sürümleri hakkında daha fazla bilgi için bkz. [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk).) Windows ADK 'yi güncelleştirmeniz gerekiyorsa, Configuration Manager güncelleştirmesine başlamadan önce bunu yapın. Bu, varsayılan önyükleme görüntülerinin Windows PE 'nin en son sürümüne otomatik olarak güncelleştirilmesini sağlar. (Özel önyükleme görüntülerinin el ile güncelleştirilmeleri gerekir.)

Siteyi Windows ADK 'yi güncelleştirmeden önce güncelleştirirseniz, Configuration Manager sürüm 1706 ' de bu işleme yönelik iyileştirmeler için [Önyükleme görüntüsüyle dağıtım noktalarını güncelleştirme](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image) bölümüne bakın.

**Siteyi ve hiyerarşi durumunu gözden geçirin ve çözülmemiş hiçbir sorun kalmadığından emin olun** : Bir siteyi güncelleştirmeden önce site sunucusunun, site veritabanı sunucusunun ve uzak bilgisayarlara yüklü site sistem rollerinin tüm çalışma sorunlarını çözün. Bir site güncelleştirmesi mevcut çalışma sorunları nedeniyle başarısız olabilir.

Daha fazla bilgi için bkz. [Configuration Manager uyarıları ve durum sistemini kullanma](use-alerts-and-the-status-system.md).

**Siteler arasında dosya ve veri çoğaltmayı gözden geçirin:**   
Siteler arasında dosya ve veritabanı çoğaltmasının çalışır durumda ve güncel olduğundan emin olun. Her iki durumda da gecikme veya biriktirme listesi sorunsuz, başarılı bir güncelleştirmeyi engelleyebilir.
Veritabanı çoğaltmasında, güncelleştirmeyi başlatmadan önce sorunları çözmeye yardımcı olması için Çoğaltma Bağlantısı Analizcisi’ni kullanabilirsiniz.

Daha fazla bilgi için bkz. [veritabanı çoğaltmasını](monitor-replication.md) izleme konusunda [Çoğaltma Bağlantısı Çözümleyicisi](monitor-replication.md#BKMK_RLA) .

**Siteyi, site veritabanı sunucusunu ve uzak site sistemi rollerini barındıran bilgisayarlara işletim sistemleri için geçerli tüm kritik güncelleştirmeleri yükler:** Configuration Manager için bir güncelleştirme yüklemeden önce, ilgili her site sistemi için tüm kritik güncelleştirmeleri yükleyebilirsiniz. Yüklediğiniz bir güncelleştirme yeniden başlatma gerektirirse, yükseltmeyi başlatmadan önce ilgili bilgisayarları yeniden başlatın.

**Birincil sitelerdeki yönetim noktaları için veritabanı çoğaltmalarını devre dışı bırak:**   
Configuration Manager, etkin yönetim noktaları için bir veritabanı çoğaltması olan bir birincil siteyi başarıyla güncelleştiremiyor. Configuration Manager için bir güncelleştirme yüklemeden önce veritabanı çoğaltmasını devre dışı bırakın.

Daha fazla bilgi için bkz. [Configuration Manager için yönetim noktaları Için veritabanı çoğaltmaları](../deploy/configure/database-replicas-for-management-points.md).

**SQL Server AlwaysOn kullanılabilirlik grupları 'nı el ile yük devretmeye ayarla:**   
Kullanılabilirlik grubu kullanıyorsanız, güncelleştirme yüklemesine başlamadan önce kullanılabilirlik grubunun el ile yük devretmeye ayarlandığından emin olun. Site güncelleştirildikten sonra, yük devretmeyi otomatik olarak geri yükleyebilirsiniz. Daha fazla bilgi için bkz. [site veritabanı için SQL Server AlwaysOn](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**NLBs kullanan yazılım güncelleştirme noktalarını yeniden yapılandırın:**   
Configuration Manager, yazılım güncelleştirme noktalarını barındırmak için Ağ Yükü Dengeleme (NLB) kümesi kullanan bir siteyi güncelleştiremez.

Yazılım güncelleştirme noktaları için NLB kümeleri kullanıyorsanız, NLB kümesini kaldırmak için Windows PowerShell 'i kullanın.
Daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md).

**Bu sitede güncelleştirme yüklemesi süresince her bir sitedeki tüm site bakım görevlerini devre dışı bırakın:**   
Güncelleştirmeyi yüklemeden önce güncelleştirme işleminin etkin olduğu süre boyunca çalışabilecek tüm site bakım görevlerini devre dışı bırakın. Bunlara diğerlerinin yanında aşağıdakiler dahildir:

-   Site Sunucusunu Yedekle
-   Eski İstemci İşlemlerini Sil
-   Eski Bulma Verilerini Sil

Bir site veritabanı bakım görevi güncelleştirme yüklemesi sırasında çalıştığında güncelleştirme yüklemesi başarısız olabilir. Bir görevi devre dışı bırakmadan önce, güncelleştirme yüklendikten sonra yapılandırmasını geri yükleyebilmek için görevin zamanlamasını kaydedin.

Daha fazla bilgi için bkz. [Configuration Manager Için bakım görevleri](maintenance-tasks.md) ve [Configuration Manager bakım görevleri için başvuru](reference-for-maintenance-tasks.md).

**Configuration Manager sunucularındaki tüm virüsten koruma yazılımlarını geçici olarak durdurun:** Bir siteyi güncelleştirmeden önce, Configuration Manager sunucularında virüsten koruma yazılımını durdurduğundan emin olun. <!--SMS.503481--> 

**Merkezi yönetim sitesinde ve birincil sitelerden site veritabanının bir yedeğini oluşturun** : Bir siteyi güncelleştirmeden önce, olağanüstü durum kurtarmasında kullanacak başarılı bir yedeğiniz olduğundan emin olmak için site veritabanını yedekleyin.

Daha fazla bilgi için bkz. [Configuration Manager Için Yedekleme ve kurtarma](backup-and-recovery.md).

**İstemci pilleyici için plan yapın:**   
İstemciyi güncelleştiren bir güncelleştirme yüklediğinizde, bu yeni istemci güncelleştirmesini, tüm etkin istemcilerinizi dağıtmadan ve yükseltibir ön üretim ortamında test edebilirsiniz.

Bu seçenekten faydalanmak için, güncelleştirmeyi yüklemeye başlamadan önce sitenizi üretim öncesi için Otomatik yükseltmeleri destekleyecek şekilde yapılandırmanız gerekir.

Daha fazla bilgi için bkz. [Istemcileri yükseltme](../../clients/manage/upgrade/upgrade-clients.md) ve [bir ön üretim koleksiyonundaki Istemci yükseltmelerini test etme](../../clients/manage/upgrade/test-client-upgrades.md).

**Site sunucularının güncelleştirmeleri ne zaman yükleyeceğini denetlemek için hizmet pencerelerini kullanmayı planlayın:**   
Site sunucusu güncelleştirmelerinin yüklenebileceği bir dönem tanımlamak için hizmet pencerelerini kullanın.

Bu olanak, hiyerarşinizdeki sitelerin güncelleştirmeyi yükleme zamanını kontrol etmenizi sağlar. Daha fazla bilgi için bkz. [site sunucuları Için hizmet pencereleri](service-windows.md).

**Kurulum önkoşul denetleyicisi 'ni çalıştırın:**   
Güncelleştirme konsolunda kullanılabilir olarak listelendiğinde **,** güncelleştirmeyi yüklemeden önce Önkoşul denetleyicisini bağımsız olarak çalıştırabilirsiniz. (Güncelleştirmeyi siteye yüklediğinizde, önkoşul denetleyicisi yeniden çalışır.)

Konsolundan bir önkoşul denetimi çalıştırmak için **yönetim > genel bakış > Cloud Services > güncelleştirmeler ve bakım** ' a gidin. Sonra, **Configuration Manager 1706 güncelleştirme paketi**' ne sağ tıkladıktan sonra **Önkoşul denetimini Çalıştır**' ı seçin.

Önkoşul denetimini başlatma ve izleme hakkında daha fazla bilgi için, bkz. **3. Adım: bir güncelleştirmeyi yüklemeden önce Önkoşul denetleyicisini çalıştırma** [Configuration Manager için konsol içi güncelleştirmeleri yükleme](install-in-console-updates.md).

> [!IMPORTANT]  
> Önkoşul denetleyicisi bağımsız olarak veya bir güncelleştirme yüklemesinin parçası olarak çalıştırıldığında, işlem, site bakım görevlerinde kullanılan bazı ürün kaynak dosyalarını güncelleştirir. Bu nedenle, Önkoşul denetleyicisini çalıştırdıktan sonra ancak güncelleştirmeyi yüklemeden önce, bir site bakım görevi gerçekleştirmeniz gerekirse, CD 'den **setupwpf. exe dosyasını** (Configuration Manager Kurulum) çalıştırın. Site sunucusundaki en son klasör.

**Güncelleştirme siteleri** : Artık hiyerarşinizin güncelleştirme yüklemesine hazırsınız. Güncelleştirmeyi yükleme hakkında daha fazla bilgi için bkz [. konsol içi güncelleştirmeleri yükleme.](install-in-console-updates.md#bkmk_install).

Güncelleştirmeyi yükleme işlemi ve site bileşenlerini ve site sistem rollerini yeniden yükleme eylemlerinin iş operasyonlarınız üzerinde en az etkisi olacak şekilde, her site için normal iş saatleri dışında güncelleştirme yüklemeyi planlamanız önerilir.

Daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](updates.md).

## <a name="post-update-checklist"></a>Güncelleştirme sonrası denetim listesi
Güncelleştirme yüklemesi tamamlandıktan sonra gerçekleştirilecek aşağıdaki eylemleri gözden geçirin.
1. Siteden siteye çoğaltmanın etkin olduğundan emin olun. Konsolunda, **izleme** > **sitesi hiyerarşisini**görüntüleyin ve çoğaltma bağlantılarının etkin olduğu sorun veya onay göstergeleri için**veritabanı çoğaltmasını** **izleme** > .
2. Her site sunucusu ve site sistemi rolünün 1706 sürümüne güncelleştirildiğinden emin olun. Konsolunda, **siteler** ve **dağıtım noktaları**dahil bazı düğümlerin görüntüsüne isteğe bağlı sütun **sürümünü** ekleyebilirsiniz.

   Gerektiğinde, bir site sistem rolü yeni sürüme güncelleştirmek için otomatik olarak yeniden yüklenir. Başarıyla güncelleştirmayan uzak site sistemlerini yeniden başlatmayı düşünün.
3. Güncelleştirmeyi başlatmadan önce devre dışı bıraktığınız birincil sitelerdeki yönetim noktaları için veritabanı çoğaltmalarını yeniden yapılandırın.
4. Güncelleştirmeyi başlatmadan önce devre dışı bıraktığınız veritabanı bakım görevlerini yeniden yapılandırın.
5. Güncelleştirmeyi yüklemeden önce istemci pilleyici 'yi yapılandırdıysanız, oluşturduğunuz plana göre istemcileri yükseltin.

## <a name="known-issues"></a>Bilinen sorunlar 
Sürüm 1706 ' e yükselttikten sonra, SMS_Executive her seferinde aşağıdaki uyarı iletisi oluşturulur SMS_CERTIFICATE_MANAGER:
-  Microsoft SQL Server bildirilen SQL iletisi 515, önem derecesi 16: [23000] [515] [Microsoft] [SQL Server Native Client 11.0] [SQL Server] NULL değeri ' RowVersion ' sütununa, ' CM_GF1. dbo. AAD_SecretChange_Notify ' tablosuna ekleyemiyor. sütun null değerlere izin vermiyor. EKLEME başarısız.

Bu ileti yoksayılabilir.  Sürüm 1706 ' e güncelleştirmeden önce hiçbir bulut hizmeti kullanılmak üzere yapılandırıldığında gerçekleşir. Bu sorun gelecek bir sürümde çözümlenir.
