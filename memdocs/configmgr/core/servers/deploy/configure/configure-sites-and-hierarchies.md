---
title: Siteleri ve hiyerarşileri yapılandırma
titleSuffix: Configuration Manager
description: Hem siteleri hem de hiyerarşileri etkileyen en yaygın yapılandırmaların göz önünde bulundurtığınızdan emin olmak için bu denetim listesine başvurun.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720999"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Configuration Manager için siteleri ve hiyerarşileri yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İlk Configuration Manager sitenizi yükledikten veya hiyerarşinize başka siteler ekledikten sonra, hem siteleri hem de hiyerarşileri etkileyen en yaygın yapılandırmaların göz önünde bulundurtığınızdan emin olmak için bu denetim listesini kullanın.  

Aşağıdaki yapılandırma notları çoğu dağıtım için geçerlidir:  

- Active Directory Orman Saptama, sınırlar ve sınır grupları gibi bazı seçenekler birbirine göre derleme yapılır.  

- Bazı yapılandırmalar, en azından başlayacak şekilde, yapılandırma değişiklikleri olmadan kullanılacak varsayılan değerlere sahiptir.  

- Sınır grupları ve dağıtım noktası grupları gibi diğer yapılandırmalarda, kullanmadan önce bunları yapılandırmanız gerekir.  

| Eylem | Ayrıntılar |  
|------------|-------------|  
| Rol tabanlı yönetimi yapılandırma | Hangi yönetici kullanıcıların Configuration Manager ortamınızda farklı nesne ve verileri görüntüleyip yönetebileceğini denetlemek üzere yönetim atamalarını ayırt edin.<br /><br /> Rol tabanlı yönetim yapılandırmaları bir hiyerarşideki tüm sitelerle paylaşılır.   <br/><br/>Daha fazla bilgi için bkz. [rol tabanlı yönetimi yapılandırma](configure-role-based-administration.md). |  
| Site verilerini Active Directory Domain Services yayımlama | İstemcilerin Hizmetleri bulmasını ve site kaynaklarını verimli bir şekilde kullanmasını kolaylaştırın.<br /><br /> Önce [Active Directory şemasını genişletin](../../../plan-design/network/extend-the-active-directory-schema.md). Sonra her siteyi [site verilerini yayımlayacak](publish-site-data.md) şekilde ayrı ayrı yapılandırın |  
| Hizmet bağlantı noktası yapılandırma | Hizmet bağlantı noktasını, hiyerarşinizin en üst düzey sitesinde yüklemeyi ve yapılandırmayı planlayın. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](about-the-service-connection-point.md). |  
| Site sistemi rolleri ekleme | Ayrı siteler için bir veya daha fazla ek site sistemi rolü yükler. Daha fazla bilgi için bkz. [site sistemi rolleri ekleme](add-site-system-roles.md). |  
| Site sınırlarını ve sınır gruplarını yapılandırma | İntranetteki, yönetmek istediğiniz cihazları içerebilen ağ konumlarını tanımlayan sınırları belirtin. Ardından, bu ağ konumlarındaki istemcilerin Configuration Manager kaynaklarını bulabilmesi için sınır gruplarını yapılandırın. Daha fazla bilgi için bkz. [site sınırlarını ve sınır gruplarını tanımlama](define-site-boundaries-and-boundary-groups.md). |  
| Dağıtım noktası gruplarını yapılandırma | Dağıtımları yönetmeyi kolaylaştırmak için dağıtım noktalarının mantıksal gruplarını yapılandırın. Daha fazla bilgi için bkz. [dağıtım noktası gruplarını yönetme](install-and-configure-distribution-points.md#bkmk_manage). |  
| Bulmayı çalıştırma | Ağ altyapısı, cihazlar ve kullanıcılar dahil olmak üzere ağınızdaki kaynakları bulmak için bulma işlemini çalıştırın.<br /><br /> Daha fazla bilgi için bkz. [bulmayı çalıştırma](run-discovery.md). |  
| Yöneticiler için yedeklilik ve kapasite ekleme | Yöneticilerin altyapınızı yönetme kapasitesini genişletmek için ek SMS sağlayıcıları ve Configuration Manager konsolları yükleyebilirsiniz:<br /><br /> Konsol ve siteye yönelik API bağlantıları için artıklık sağlamak üzere **ek SMS sağlayıcıları yükleyebilirsiniz** . Daha fazla bilgi için bkz. [SMS sağlayıcısını yönetme](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).<br /><br /> Ek Yönetici kullanıcılara erişim sağlamak için **ek Configuration Manager konsolları yükler** . Daha fazla bilgi için bkz. [ınstall Configuration Manager konsolları](../install/install-consoles.md). |  
| Site bileşenlerini yapılandırma | Site sistem rolleri ve site durumu raporlama davranışını değiştirmek için her sitedeki site bileşenlerini yapılandırın. Daha fazla bilgi için bkz. [site bileşenleri](site-components.md). |  
| Özel koleksiyonlar oluşturma | Sitenin cihazlar ve kullanıcılar hakkında bulduğu bilgileri kullanarak, gelecekteki yönetim görevlerini basitleştirmek için özel nesne koleksiyonları oluşturun. Daha fazla bilgi için bkz. [koleksiyonlar oluşturma](../../../clients/manage/collections/create-collections.md). |  
| Yüksek riskli dağıtımları yönetmek için ayarları yapılandırma | Bir sitedeki ayarları, yüksek riskli bir dağıtım oluşturduklarında yöneticileri uyaracak şekilde yapılandırın. Daha fazla bilgi için bkz. [yüksek riskli dağıtımları yönetme ayarları](../../manage/settings-to-manage-high-risk-deployments.md). |  
| Yönetim noktaları için veritabanı çoğaltmalarını yapılandırma | İstemcilerden gelen istekleri sunan yönetim noktaları tarafından site veritabanı sunucusuna yerleştirilmiş işlemci yükünü azaltmak için bir veritabanı çoğaltması yapılandırın. Daha fazla bilgi için bkz. [Yönetim noktaları Için veritabanı çoğaltmaları](database-replicas-for-management-points.md). |  
| SQL Server Always on kullanılabilirlik grubu yapılandırma | Site veritabanını birincil sitelerde ve merkezi yönetim sitesinde barındırmak için yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümleri olarak kullanılabilirlik grupları yapılandırın. Daha fazla bilgi için bkz. [yüksek oranda kullanılabilir site veritabanı Için AlwaysOn SQL Server](sql-server-alwayson-for-a-highly-available-site-database.md). |  
| Siteler arasında çoğaltmayı değiştirme | Aşağıdaki konular hakkında bilgi edinmek için [siteler arasındaki veri aktarımlarını](../../../plan-design/hierarchy/data-transfers-between-sites.md) inceleyin:<br /><br /> İkincil siteler arasında [dosya tabanlı çoğaltmayı](../../../plan-design/hierarchy/file-based-replication.md) yapılandırma<br /><br /> [Veritabanı çoğaltma bağlantılarını](../../../plan-design/hierarchy/database-replication.md) yapılandırma<br /><br /> [Dağıtılmış görünümleri](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) yapılandırma |  
| Site sunucularını pasif modda yapılandırma | Sürüm 1806 ' den başlayarak, her birincil site ve merkezi yönetim sitesi için pasif modda bir site sunucusunu yapılandırın. Bu özellik, yüksek oranda kullanılabilir bir site sunucusu sağlar. Daha fazla bilgi için bkz. [site sunucusu yüksek kullanılabilirlik](site-server-high-availability.md). |  
