---
title: Hiyerarşiyi izleme
titleSuffix: Configuration Manager
description: Konsolundaki Izleme çalışma alanını kullanarak Configuration Manager altyapınızı nasıl izleyeceğinizi öğrenin.
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66fc6744ef7d1aaf90a5e7339cc9a5174c0d33f6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713705"
---
# <a name="monitor-the-hierarchy"></a>Hiyerarşiyi izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hiyerarşinizi Configuration Manager izlemek için Configuration Manager konsolundaki **izleme** çalışma alanını kullanın.  

> [!NOTE]  
> Bu konumun özel durumu, siteleri geçirirken olur. Bu işlem, **Yönetim** çalışma alanının **geçiş** düğümünde izleniyor. Daha fazla bilgi için bkz. [Configuration Manager geçerli dala geçiş işlemleri](../../migration/operations-for-migration.md).  

İzleme için Configuration Manager konsolunun kullanımıyla birlikte, aşağıdaki özellikleri kullanın:

- [Raporlamaya giriş](introduction-to-reporting.md)
- [Günlük dosyaları](../../plan-design/hierarchy/log-files.md).  

Siteleri izlerken, harekete geçmenizi gerektiren sorunlar olduğunu gösteren emarelere bakın. Örneğin:  

- Site sunucularında ve site sistemlerindeki dosyaların biriktirme listesi.  

- Bir hata ya da sorun olduğunu gösteren durum iletileri.  

- Başarısız olan site içi iletişim.  

- Sunuculardaki sistem olay günlüğünde yer alan hata ve uyarı iletileri.  

- Microsoft SQL Server hata günlüğünde yer alan hata ve uyarı iletileri.  

- Durumu uzun bir süre bildirilmeyen siteler veya istemciler.  

- SQL Server veritabanından yavaş yanıt alınması.  

- Donanım hatası belirtileri.  

İzleme görevleri herhangi bir sorun işaretini açığa çıkarsa, sorunun kaynağını araştırın. Daha sonra bir site hatasının riskini en aza indirmek için hızlı bir şekilde onarın.  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a>Ortak yönetim görevlerini izleme

Configuration Manager, Configuration Manager konsolunun içinden yerleşik izleme sağlar.

### <a name="alerts"></a>Uyarılar

Daha fazla bilgi için bkz. [Uyarıları izleme](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts).  

### <a name="compliance-settings"></a>Uyumluluk ayarları

Daha fazla bilgi için bkz. [Uyumluluk ayarlarını izleme](../../../compliance/deploy-use/monitor-compliance-settings.md).

### <a name="content"></a>İçerik

İçeriği izleme hakkında genel bilgi için bkz. [içeriği ve içerik altyapısını yönetme](../deploy/configure/manage-content-and-content-infrastructure.md).  

Belirli içerik türlerini izleme hakkında daha fazla bilgi için:

- [Uygulamaları izleme](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Paketleri ve programları izleme](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Yazılım güncelleştirmeleri için içeriği izleme](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [İşletim sistemi dağıtımları için içeriği izleme](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Uç Nokta Koruma

Daha fazla bilgi için bkz. [izleme Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).  

### <a name="os-deployment"></a>İşletim sistemi dağıtımı

Daha fazla bilgi için bkz. [işletim sistemi dağıtımlarını izleme](../../../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="monitor-power-management"></a>Güç yönetimini izleme

Daha fazla bilgi için bkz. [güç yönetimini izleme ve plan yapma](../../clients/manage/power/monitor-and-plan-for-power-management.md).  

### <a name="monitor-software-metering"></a> Yazılım kullanım ölçümünü izleme

Daha fazla bilgi için bkz. [yazılım kullanım ölçümü ile uygulama kullanımını izleme](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

### <a name="monitor-software-updates"></a>Yazılım güncelleştirmelerini izleme

Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini izleme](../../../sum/deploy-use/monitor-software-updates.md).  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a>Site hiyerarşisini izleme

**İzleme** çalışma alanının **site hiyerarşisi** düğümü, Configuration Manager hiyerarşinize ve siteler arası bağlantılarınızda bir genel bakış sağlar. İki görünümü kullanabilirsiniz:  

- **Hiyerarşi diyagramı**: hiyerarşinizi yalnızca önemli bilgileri gösteren basitleştirilmiş bir topoloji haritası olarak görüntüler. Daha fazla bilgi için bkz. [hiyerarşi diyagramı](#hierarchy-diagram).  

- **Coğrafi görünüm**: siteleriniz, yapılandırdığınız site konumlarını gösteren bir coğrafi harita üzerinde görüntüler. Daha fazla bilgi için bkz. [coğrafi görünüm](#geographical-view).  

Her sitenin sistem durumunu izlemek için **site hiyerarşisi** düğümünü kullanın. Ayrıca, siteler arası çoğaltma bağlantılarını ve bunların coğrafi konum gibi dış faktörlerle ilişkilerini izleyin.  

Site durumu ve siteler arası bağlantı durumu, genel veriler değil site verileri olarak çoğaltılır. Configuration Manager konsolunuzu bir alt birincil siteye bağladığınızda, diğer birincil sitelere veya onların alt ikincil sitelerine ilişkin site veya bağlantı durumunu görüntüleyemezsiniz. Örneğin, birden çok birincil siteye sahip bir hiyerarşide, konsolunu bir birincil siteye bağladığınızda, alt ikincil sitelerin, birincil sitenin ve merkezi yönetim sitesinin durumunu görüntüleyebilirsiniz. Bu görünümden, merkezi yönetim sitesinin altındaki diğer sitelerin durumunu göremezsiniz.  

Görünümü **site hiyerarşisi** düğümünde denetlemek Için **Ayarları Yapılandır** eylemini kullanın. Hiyerarşi, bu düğümde yapılandırdığınız ayarları çoğaltır.  

### <a name="hierarchy-diagram"></a>Hiyerarşi Diyagramı

Hiyerarşi diyagramı, sitelerinizi bir topoloji haritasında gösterir. Bir site seçin ve bu siteden bir durum iletisi özeti görüntüleyin. Durum iletilerini görüntülemek ve site **özelliklerine**erişmek için detaya gidin.  

Siteler arasındaki bir sitenin veya çoğaltma bağlantısının üst düzey durumunu görüntülemek için fare işaretçinizi nesnenin üzerine getirin. Çoğaltma bağlantısı durumu genel olarak çoğaltılmaz. Bir hiyerarşideki tüm birincil siteler arasındaki çoğaltma bağlantısı ayrıntılarını görüntülemek için, konsolu merkezi yönetim sitesine bağlayın.  

Aşağıdaki seçenekler hiyerarşi diyagramını değiştirir:  

#### <a name="groups"></a>Gruplar

Hiyerarşi diyagramında bir değişikliği tetikleyen birincil sitelerin ve ikincil sitelerin sayısını yapılandırın. Ekranda bu değişiklik, siteleri tek bir nesne halinde birleştirir. Sonra toplam site sayısını ve durum iletilerinin üst düzey bir toplu toplamasını ve site durumunu görürsünüz. Grup yapılandırması coğrafi görünümü etkilemez.  

#### <a name="favorite-sites"></a>Sık kullanılan siteler

Bağımsız siteleri bir sık kullanılan site olarak belirtin. Hiyerarşi diyagramında sık kullanılan bir site yıldız simgesiyle belirtilir. Grupları kullandığınızda, sık kullanılan siteler diğer sitelerle birleştirilmez. Her zaman tek ayrı görüntülenirler.  

### <a name="geographical-view"></a>Coğrafi Görünüm

Coğrafi görünüm, her sitenin konumunu coğrafi bir haritada gösterir. Yalnızca bir konumla yapılandırdığınız siteleri görüntüler. Bu görünümde bir site seçtiğinizde, üst veya alt sitelere yönelik çoğaltma bağlantıları gösterilir. Hiyerarşi diyagramı görünümünden farklı olarak, bu görünümde site durumu iletisini veya çoğaltma bağlantısı ayrıntılarını görüntüleyemezsiniz.  

> [!NOTE]  
> Coğrafi görünümü kullanmak için, Configuration Manager konsolunuzun bağlandığı bilgisayarda Internet Explorer yüklü olmalıdır ve HTTP protokolünü kullanarak Bing Haritalar 'a erişebiliyor olması gerekir.  

Aşağıdaki seçenek coğrafi görünümü değiştirir:  

#### <a name="site-location"></a>Site konumu

Aşağıdaki türlerden birini kullanarak her site için bir coğrafi konum belirtin:

- Sokak adresi
- Şehir adı gibi bir yer adı
- Enlem ve boylam koordinatları

Örneğin, Redmond, Istanbul 'un Enlem ve boylalarını kullanmak için sitenin konumu olarak **N 47 40 26,3572 W 122 7 17,4432** belirtin. Enlem veya boylam derece, dakika veya saniye simgeleri belirtmeniz gerekmez. Configuration Manager, coğrafi görünümde konumu görüntülemek için Bing Haritalar 'ı kullanır. Daha sonra hiyerarşinizi coğrafi konumlara göre görüntüleyebilirsiniz. Bu görünüm, belirli siteleri veya siteler arası çoğaltmayı etkileyebilecek bölgesel sorunlar hakkında öngörüler sağlar.  

Bir konumu belirttiğinizde, hiyerarşinizde belirli bir siteyi aramak için **Konum** kutusunu kullanabilirsiniz. Site seçiliyken, konumu **Konum** sütununa şehir adı veya posta adresi olarak girin. Configuration Manager, konumu çözümlemek için Bing Haritalar 'ı kullanır.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>Sonraki adımlar

[Veritabanı çoğaltmasını izleme](monitor-replication.md)
