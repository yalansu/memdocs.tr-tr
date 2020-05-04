---
title: Veritabanı çoğaltmasını izleme
titleSuffix: Configuration Manager
description: Configuration Manager hiyerarşinizde SQL Server çoğaltmanın nasıl izleneceğini öğrenin.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 96cce5d4aaa352177b1c24ff78cf15e90ea6e823
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713712"
---
# <a name="monitor-database-replication"></a>Veritabanı çoğaltmasını izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager konsolunun **izleme** çalışma alanındaki **veritabanı çoğaltma** düğümü ile veritabanı çoğaltmasının ayrıntılarını izleyin. Siteler arasındaki çoğaltma bağlantılarının durumunu izleyebilirsiniz. Ayrıca, bağlandığınız site için çoğaltma gruplarının başlatılmasını ve çoğaltılmasını da gösterir.  

> [!TIP]  
> Ayrıca, **Yönetim** çalışma alanındaki **Hiyerarşi Yapılandırması** düğümünün altında bir **veritabanı çoğaltma** düğümü görünse de, bu konumdan veritabanı çoğaltması bağlantıları için çoğaltma durumunu görüntüleyemezsiniz.  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> Çoğaltma bağlantısı durumu  

Siteler arasında veritabanı çoğaltması, *çoğaltma grupları*adı verilen çeşitli bilgi kümelerinin çoğaltılmasını içerir. Her çoğaltma grubu, verileri farklı önceliklerle gönderir ve alır. Varsayılan olarak, bir çoğaltma grubunda bulunan verileri ve çoğaltma sıklığını değiştiremezsiniz.  

Bir çoğaltma bağlantısı etkin olduğunda ve durumu başarısız veya düşürülmüş olmadığında, tüm gruplar hızlı bir şekilde çoğaltılır. Bir veya daha fazla grup çoğaltmayı beklenen sürede tamamlayamazsa, bağlantı *düşürülmüş*olarak görüntülenir. Düşürülmüş bağlantılar hala çalışabilir, ancak etkin duruma döndiklerinden emin olmak için bunları izlemeniz gerekir. Ek düşme veya çoğaltma hatalarının gerçekleşmeyecek olduğundan emin olmak için bunları araştırın.  

Her bir çoğaltma bağlantısı için, başarısız bir çoğaltılan grubun kaç kez yeniden deneyeceğini belirtin. Bu sayıda yeniden denemeden sonra, site bağlantının durumunu düşürülmüş veya başarısız olarak ayarlar. Biri ancak bir grup başarıyla çoğaltılsa bile, site bağlantının durumunu düşürülmüş veya başarısız olarak ayarlar. Bu durum, bir çoğaltma grubu belirtilen sayıda denemeden çoğaltmayı tamamlayamadığından bu durumu ayarlar. Daha fazla bilgi için [veritabanı çoğaltma eşiklerine](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds)bakın.  

Daha fazla araştırma gerektirebilen çoğaltma bağlantılarının durumunu anlamak için aşağıdaki bilgileri kullanın:  

### <a name="link-is-active"></a>Bağlantı etkin

Herhangi bir sorun algılanmadı ve bağlantı üzerinde iletişim geçerli.

Bir üst site yeni bir sürüme güncelleştirilirken ve bağlantı durumunu alt siteden görüntülediğinizde, bağlantı durumu etkin olarak görüntülenir. Güncelleştirme sonrasında, alt site üst siteyle aynı sürüme gelinceye kadar, bağlantı durumu üst siteden görüntülendiğinde etkin olarak görüntülenir. Alt siteden görüntülendiğinde, yapılandırıldığı gibi görüntülenir.  

### <a name="link-is-degraded"></a>Bağlantı düşürülmüş

Çoğaltma çalışır; ancak en az bir çoğaltma nesnesi veya grubu gecikmiştir. Bu durumdaki bağlantıları izleyin. Bağlantının başarısız olabileceğini belirten göstergeler için bağlantı üzerindeki her iki sitedeki bilgileri gözden geçirin.

Çoğaltılmış verileri alan site bu verileri hızlı bir şekilde veritabanına işleyemediğinde de bağlantı, düşürülmüş durumunu gösterebilir. Bu davranış, büyük hacimler veri çoğaltmasından oluşur. Örneğin, bir yazılım güncelleştirmesini çok sayıda bilgisayara dağıtırsınız. Bağlantıdaki üst site, bu çoğaltılan veri hacminin işlenmesi biraz zaman alabilir. Üst sitedeki bir işleme gecikmesi, veri biriktirme listesini başarılı bir şekilde işleyeünceye kadar bağlantı durumunun düşürülmüş olarak ayarlanmasına neden olur.

### <a name="link-has-failed"></a>Bağlantı başarısız oldu

Çoğaltma çalışmıyor. Bir çoğaltma bağlantısının başka bir eylem olmadan kurtarılması mümkündür. Bu bağlantıdaki çoğaltmayı araştırmak ve düzeltmeye yardımcı olması için Çoğaltma Bağlantısı Çözümleyicisi (RLA) kullanın.

Bu durum, çoğaltma bağlantısındaki üst ve alt site arasındaki fiziksel ağla ilgili bir sorun olduğu anlamına da gelebilir.


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a>Çoğaltma durumunu izleme

Bir çoğaltma bağlantısının durumunu görüntülemek için **izleme** çalışma alanındaki **veritabanı çoğaltması** düğümünü kullanın. Çoğaltma bağlantısındaki her bir sitede veritabanıyla ilgili ayrıntıları görüntüleyin. Çoğaltma gruplarıyla ilgili ayrıntıları da görüntüleyebilirsiniz. Bu ayrıntıları görüntülemek için bir çoğaltma bağlantısı seçin ve ardından görüntülemek istediğiniz çoğaltma durumu için uygun sekmeyi seçin.

Aşağıdaki bölümler, çoğaltma durumunun farklı sekmeleri hakkında ayrıntılar verir:

### <a name="summary"></a>Özet

Bir bağlantı üzerindeki iki site arasında site verilerinin ve genel verilerin çoğaltılmasıyla ilgili üst düzey bilgileri görüntüleyin.  

Bağlantı genelinde çoğaltma tarafından kullanılan ağ bant genişliğiyle ilgili ayrıntıları gösteren bir raporu görüntülemek için **geçmiş trafik verileri için raporları görüntüle** ' yi seçin.  

### <a name="parent-site"></a>Üst Site

Çoğaltma bağlantısındaki üst site için, veritabanıyla ilgili aşağıdaki ayrıntıları görüntüleyin:  

- SQL Server için güvenlik duvarı bağlantı noktaları  

- Boş disk alanı  

- Veritabanı dosyası konumları  

- Sertifikalar  

### <a name="child-site"></a>Alt Site

Çoğaltma bağlantısındaki alt site için, veritabanıyla ilgili aşağıdaki ayrıntıları görüntüleyin:  

- SQL Server için güvenlik duvarı bağlantı noktaları  

- Boş disk alanı  

- Veritabanı dosyası konumları  

- Sertifikalar  

### <a name="initialization-detail"></a>Başlatma Ayrıntısı

Bağlantı genelinde çoğaltılan gruplar için başlatma durumunu görüntüleyin. Bu bilgiler, çoğaltma verilerinin başlatılmasının sürdüğünü veya başarısız olduğunu belirlemenize yardımcı olabilir.  

Bir sitenin *birlikte çalışabilirlik modunda*ne zaman olabileceğini belirlemek için bu bilgileri kullanın. Birlikte çalışabilirlik modu, alt site üst siteyle aynı Configuration Manager sürümünü çalıştırmazsa.  

### <a name="replication-detail"></a>Çoğaltma Ayrıntısı

Bağlantı genelinde çoğaltılan her grup için çoğaltma durumunu görüntüleyin. Belirli verilerin çoğaltılmasıyla ilgili sorunları veya gecikmeleri belirlemenize yardımcı olması için bu bilgileri kullanın. Bu bağlantının uygun veritabanı çoğaltma eşiklerini belirlemesine yardımcı olabilir. Daha fazla bilgi için bkz. [veritabanı çoğaltma eşikleri](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

> [!TIP]  
> Site verilerine yönelik çoğaltma grupları yalnızca alt siteden üst siteye gönderilir. Genel verilere yönelik çoğaltma grupları her iki yönde çoğaltma yapar.  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a>Çoğaltma Bağlantısı Çözümleyicisi

Configuration Manager, çoğaltma sorunlarını çözümlemek ve onarmak için kullandığınız **Çoğaltma Bağlantısı Çözümleyicisi** (rla) içerir. Çoğaltma başarısız olduğunda bağlantı hatalarının düzeltilmesi için RLA 'yı kullanın. Çoğaltma çalışmayı durdurulduğunda ancak site henüz başarısız olarak bildirilmediyse de yararlıdır.

Hiyerarşideki aşağıdaki bilgisayarlar arasındaki çoğaltma sorunlarını düzeltmek için RLA 'yı kullanın:  

- Site sunucusu ile site veritabanı sunucusu arasında  

- Sitenin veritabanı sunucusu ile başka bir sitenin veritabanı sunucusu arasında, siteler arası çoğaltma olarak da bilinen  

> [!Note]  
> Çoğaltma hatasının yönü ne kadar önemlidir.

RLA 'yı Configuration Manager konsolunda veya bir komut isteminde çalıştırın:  

- Configuration Manager konsolunda çalıştırmak için: **izleme** çalışma alanına gidin ve **veritabanı çoğaltması** düğümünü seçin. Çözümlemek istediğiniz çoğaltma bağlantısını seçin ve ardından şeritte **Çoğaltma Bağlantısı Çözümleyicisi**' yi seçin.  

- Komut isteminde çalıştırmak için aşağıdaki komutu yazın:`%ProgramFiles(x86)%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

RLA çalıştırdığınızda, bir dizi tanı kuralını ve denetimini kullanarak sorunları algılar. Aracın tanımladığı sorunları görüntüleyebilirsiniz. Bir sorunu çözmeye yönelik yönergeler olduğunda, bunları görüntüler. RLA bir sorunu otomatik olarak düzeltebiliyorsa, size bu seçeneği sunar.

RLA tamamlandığında, sonuçları aşağıdaki XML tabanlı rapora ve aracı çalıştıran kullanıcının masaüstündeki bir günlük dosyasına kaydeder:  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA, bazı sorunları düzeltirken aşağıdaki hizmetleri durduruyor. Düzeltme tamamlandığında bu hizmetleri yeniden başlatır:  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

RLA düzeltmeyi tamamlayamazsa, gerekirse site sunucusunda bu hizmetleri yeniden başlatın.  

RLA, sihirbazda görüntülememe hakkında ek ayrıntılar sağlamak için tüm araştırma ve düzeltme eylemlerini günlüğe kaydeder.  

### <a name="rla-prerequisites"></a>RLA önkoşulları

RLA 'yı çalıştırmak için kullandığınız hesabın şu izinlere sahip olması gerekir:

- Çoğaltma bağlantısına katılan her bilgisayarda yerel yönetici hakları.

- Çoğaltma bağlantısında yer alan her bir SQL Server veritabanında sysadmin hakları.  

> [!Note]  
> Hesap, belirli bir rol tabanlı yönetim güvenlik rolü Configuration Manager gerektirmez. **Veritabanı çoğaltma** düğümüne erişimi olan bir yönetici kullanıcı, aracı Configuration Manager konsolunda çalıştırabilir. Her bilgisayar için yeterli haklara sahip bir sistem yöneticisi, aracı komut isteminde çalıştırabilir.  

### <a name="rla-known-issue"></a>RLA bilinen sorunu

RLA, System Center 2012 Configuration Manager yükseltilen birincil siteler için SQL Server Hizmet Aracısı (SSB) sertifika hataları oluşturur. Bu sorun, geçerli dalda Configuration Manager sertifikaların adlarındaki değişiklikler nedeniyle oluşur. Bu hataları güvenle yoksayabilirsiniz.  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a>Veritabanı çoğaltmasını izleme  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>Üst düzey siteden siteye veritabanı çoğaltma durumunu izleme

1. Configuration Manager konsolunda **izleme** çalışma alanına gidin.  

2. **Hiyerarşi diyagramı** görünümünü açmak Için **site hiyerarşisi** düğümünü seçin.  

3. Fare işaretçisini iki site arasındaki çizginin üzerine getirin. Bu siteler için genel ve site veri çoğaltmasının durumunu görüntüleyin.  

### <a name="monitor-the-status-of-a-replication-link"></a>Çoğaltma bağlantısının durumunu izleme

1. Configuration Manager konsolunda **izleme** çalışma alanına gidin.  

2. **Veritabanı çoğaltma** düğümünü seçin ve ardından izlemek istediğiniz çoğaltma bağlantısını seçin. Sonra bu bağlantının çoğaltma durumuyla ilgili farklı ayrıntıları görüntülemek için uygun sekmeyi seçin.  
