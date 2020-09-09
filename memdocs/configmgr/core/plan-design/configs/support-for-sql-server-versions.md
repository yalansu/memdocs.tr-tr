---
title: Desteklenen SQL Server sürümleri
titleSuffix: Configuration Manager
description: Configuration Manager site veritabanını barındırmak için SQL Server sürümü ve yapılandırma gereksinimleri alın.
ms.date: 06/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5043967a640b937784c22ea2b74269a2f2043ba9
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607628"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Configuration Manager için desteklenen SQL Server sürümleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Her Configuration Manager sitesi, site veritabanını barındırmak için desteklenen bir SQL Server sürümü ve yapılandırması gerektirir.  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server örnekleri ve konumları

### <a name="central-administration-site-and-primary-sites"></a>Merkezi Yönetim sitesi ve birincil siteler

Site veritabanının tam SQL Server yüklemesini kullanması gerekir.  

SQL Server şu konumda bulunabilir:  

- Site sunucusu bilgisayar.  
- Site sunucusundan uzakta olan bir bilgisayar.  

Aşağıdaki örnekler desteklenir:  

- SQL Server varsayılan veya adlandırılmış örneği.  
- Birden çok örnek yapılandırması.  
- SQL Server kümesi. Bkz. [site veritabanını barındırmak için SQL Server kümesi kullanma](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- SQL Server bir AlwaysOn kullanılabilirlik grubu. Daha fazla bilgi için bkz. [yüksek oranda kullanılabilir site veritabanı Için AlwaysOn SQL Server](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="secondary-sites"></a>İkincil siteler

Site veritabanı SQL Server veya SQL Server Express tam yüklemesinin varsayılan örneğini kullanabilir.  

SQL Server, site sunucusu bilgisayarında bulunmalıdır.  

### <a name="limitations-to-support"></a>Destek sınırlamaları

Aşağıdaki konfigürasyonlar desteklenmez:

- Ağ Yükü Dengeleme (NLB) küme yapılandırmasındaki SQL Server kümesi
- Bir Küme Paylaşılan Birimi (CSV) SQL Server kümesi
- SQL Server veritabanı yansıtma teknolojisi ve eşler arası çoğaltma

SQL Server işlemsel çoğaltma yalnızca [veritabanı çoğaltmaları](../../servers/deploy/configure/database-replicas-for-management-points.md)kullanmak üzere yapılandırılmış yönetim noktalarına nesne çoğaltmak için desteklenir.  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Desteklenen SQL Server sürümleri

Birden çok sitesi olan bir hiyerarşide, farklı siteler, site veritabanını barındırmak için farklı SQL Server sürümleri kullanabilir. Aşağıdaki öğeler doğru olduğu sürece:

- Configuration Manager, kullandığınız SQL Server sürümlerini destekler.
- Kullandığınız SQL Server sürümleri Microsoft tarafından destede kalır.
- SQL Server iki SQL Server sürümü arasında çoğaltmayı destekler. Daha fazla bilgi için bkz. [çoğaltma geri uyumluluğu SQL Server](/sql/relational-databases/replication/replication-backward-compatibility).

SQL Server 2016 ve öncesi için, her SQL sürümü ve hizmet paketi için destek, [Microsoft yaşam döngüsü ilkesini](https://aka.ms/sqllifecycle)izler. Belirli bir SQL Server hizmet paketine yönelik destek, temel hizmet paketi sürümüne geriye dönük uyumluluğu bırakmadığı müddetçe toplu güncelleştirmeleri içerir. SQL Server 2017 ' den başlayarak, hizmet paketleri, [modern bir hizmet modelini](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)takip eden bir şekilde yayınlanmayacak. SQL Server ekibi, kullanılabilir hale geldiğinde [toplu güncelleştirmelerin devam eden ve proaktif yüklemesini](/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism) öneriyor.

Aksi belirtilmediği takdirde, aşağıdaki SQL Server sürümleri tüm Configuration Manager etkin sürümleriyle desteklenir. Yeni bir SQL Server sürümü için destek eklenirse, bu desteği ekleyen Configuration Manager sürümü belirtilmiştir. Benzer şekilde, destek kullanım dışı ise, Configuration Manager etkilenen sürümleri hakkında ayrıntılı bilgi için bkz..

> [!IMPORTANT]  
> Merkezi yönetim sitesinde veritabanı için SQL Server Standard kullandığınızda, bir hiyerarşinin destekleyebileceği toplam istemci sayısını sınırlandıracak. Bkz. [Boyutlandırma ve ölçek rakamları](size-and-scale-numbers.md).

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019: Standart, kurumsal

Configuration Manager sürüm 1910 ' den başlayarak, toplu güncelleştirme 5 ' i (CU5) veya sonraki bir sürümünü kullanarak, toplu güncelleştirme sürümünüz SQL yaşam döngüsü tarafından desteklendiği sürece bu sürümü kullanabilirsiniz. CU5, [SKALAR UDF](/sql/relational-databases/user-defined-functions/scalar-udf-inlining)ile ilgili bir sorunu çözen SQL Server 2019 için en düşük gereksinimdir.

Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- Bir merkezi yönetim sitesi
- Birincil site
- İkincil site

<!--
#### Known issue with SQL Server 2019

There's a known issue<!--6436234 with the new [scalar UDF inlining](/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature in SQL 2019. To work around this issue and disable UDF lining, run the following script on the SQL 2019 server:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

While not always necessary, you may need to restart the SQL server after you run this script. For more information, see [Disabling Scalar UDF Inlining without changing the compatibility level](/sql/relational-databases/user-defined-functions/scalar-udf-inlining#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

You can safely disable this SQL feature for the site database server because Configuration Manager doesn't use it.

If you don't disable scalar UDF inlining in SQL 2019, the site server will randomly fail to query the site database. For example, you'll see the following errors in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

You may see similar errors in other logs, such as **SmsAdminUI.log**.

SQL Server version 2019 logs the following error:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

You'll also see crash dumps (`.mdump` files) from SQL in its log directory, which by default is `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.
-->

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standart, kurumsal

Toplu güncelleştirme sürümünüz SQL yaşam döngüsü tarafından desteklendiği sürece bu sürümü [toplu güncelleştirme sürümü 2](https://support.microsoft.com/help/4052574) veya üzeri ile kullanabilirsiniz. Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- Bir merkezi yönetim sitesi  
- Birincil site  
- İkincil site  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standart, kurumsal  
<!--514985-->
Bu sürümü, SQL yaşam döngüsü tarafından desteklenen en düşük hizmet paketi ve toplu güncelleştirme ile birlikte kullanabilirsiniz. Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- Bir merkezi yönetim sitesi  
- Birincil site  
- İkincil site  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: Standart, kurumsal

Bu sürümü, SQL yaşam döngüsü tarafından desteklenen en düşük hizmet paketi ve toplu güncelleştirme ile birlikte kullanabilirsiniz. Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- Bir merkezi yönetim sitesi  
- Birincil site  
- İkincil site

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: Standart, kurumsal

Bu sürümü, SQL yaşam döngüsü tarafından desteklenen en düşük hizmet paketi ve toplu güncelleştirme ile birlikte kullanabilirsiniz. Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- Bir merkezi yönetim sitesi  
- Birincil site  
- İkincil site  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

Toplu güncelleştirme sürümünüz SQL yaşam döngüsü tarafından desteklendiği sürece bu sürümü [toplu güncelleştirme sürümü 2](https://support.microsoft.com/help/4052574) veya üzeri ile kullanabilirsiniz. Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- İkincil site
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

Bu sürümü, SQL yaşam döngüsü tarafından desteklenen en düşük hizmet paketi ve toplu güncelleştirme ile birlikte kullanabilirsiniz. Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- İkincil site

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

Bu sürümü, SQL yaşam döngüsü tarafından desteklenen en düşük hizmet paketi ve toplu güncelleştirme ile birlikte kullanabilirsiniz. Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- İkincil site  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

Bu sürümü, SQL yaşam döngüsü tarafından desteklenen en düşük hizmet paketi ve toplu güncelleştirme ile birlikte kullanabilirsiniz. Bu SQL sürümü aşağıdaki siteler için kullanılabilir:

- İkincil site  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> SQL Server için gerekli yapılandırmalar

SQL Server Express dahil olmak üzere, bir site veritabanı için kullandığınız tüm SQL Server yüklemeleri için aşağıdaki yapılandırma gerekir. Configuration Manager, ikincil site yüklemesinin bir parçası olarak SQL Server Express yüklediğinde, bu konfigürasyonları otomatik olarak oluşturur.  

### <a name="sql-server-architecture-version"></a>SQL Server mimari sürümü

Configuration Manager, site veritabanını barındırmak için SQL Server 64 bitlik bir sürümünü gerektirir.  

### <a name="database-collation"></a>Veritabanı harmanlaması

Her sitede, site ve site veritabanı için kullanılan SQL Server örneği şu harmanlamayı kullanmalıdır: **SQL_Latin1_General_CP1_CI_AS**.  

Configuration Manager, Çin GB18030 standardı için bu harmanlamada iki özel durumu destekler. Daha fazla bilgi için bkz. [Uluslararası destek](../hierarchy/international-support.md).  

### <a name="database-compatibility-level"></a>Veritabanı uyumluluk düzeyi

Configuration Manager, site veritabanının uyumluluk düzeyinin Configuration Manager sürümünüz için desteklenen en düşük SQL Server sürümden az olmaması gerekir. Örneğin, sürüm 1702 ' den başlayarak, 110 ' e eşit veya daha büyük bir [veritabanı uyumluluk düzeyine](/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) sahip olmanız gerekir. <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server özellikleri

Her site sunucusu için yalnızca **Veritabanı Altyapısı Hizmetleri** özelliği gereklidir.  

Configuration Manager veritabanı çoğaltması **SQL Server çoğaltma** özelliği gerektirmez. Ancak, [Yönetim noktaları için veritabanı çoğaltmaları](../../servers/deploy/configure/database-replicas-for-management-points.md)kullandığınızda bu SQL Server yapılandırması gerekir.  

### <a name="windows-authentication"></a>Windows kimlik doğrulaması

Configuration Manager, veritabanı bağlantılarını doğrulamak için **Windows kimlik doğrulaması** gerektirir.  

### <a name="sql-server-instance"></a>SQL Server örneği

Her site için adanmış bir SQL Server örneğini kullanın. Örnek, **adlandırılmış bir örnek** veya **varsayılan örnek**olabilir.  

### <a name="sql-server-memory"></a>SQL Server belleği

SQL Server Management Studio kullanarak SQL Server için bellek ayırın. **Sunucu belleği seçenekleri**altındaki **En düşük sunucu belleği** ayarını belirleyin. Bu ayarı yapılandırma hakkında daha fazla bilgi için bkz. [SQL Server Memory Server yapılandırma seçenekleri](/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **Site sunucusuyla aynı bilgisayara yüklediğiniz bir veritabanı sunucusu için**: belleği, kullanılabilir adreslenebilir sistem belleğinin yüzde 80 50 ' i ile SQL Server sınırlayın.  

- **Site sunucusundan uzakta olan adanmış bir veritabanı sunucusu için**: belleği, kullanılabilir adreslenebilir sistem belleğinin yüzde 90 80 ' i ile SQL Server sınırlayın.  

- **Kullanılan her bir SQL Server örneğinin arabellek havuzu için ayrılan bellek için**:  

  - Bir merkezi yönetim sitesi için: en az 8 GB ayarlayın.  
  - Birincil site için: en az 8 GB ayarlayın.  
  - İkincil site için: en az 4 GB ayarlayın.  

### <a name="sql-nested-triggers"></a>SQL iç içe Tetikleyicileri

SQL iç içe tetikleyicilerinin etkinleştirilmesi gerekir. Daha fazla bilgi için bkz [. iç içe Tetikleyiciler sunucu yapılandırma seçeneğini](/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option) yapılandırma

### <a name="sql-server-clr-integration"></a>SQL Server CLR tümleştirmesi

Site veritabanı, SQL Server ortak dil çalışma zamanının (CLR) etkin olmasını gerektirir. Configuration Manager yüklendiğinde bu seçenek otomatik olarak etkinleştirilir. CLR hakkında daha fazla bilgi için bkz. [SQL Server clr tümleştirmesine giriş](/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Hizmet Aracısı (SSB)

SQL Server Hizmet Aracısı hem siteler arası çoğaltma hem de tek bir birincil site için gereklidir.

### <a name="trustworthy-setting"></a>GÜVENILIR ayar

Configuration Manager, SQL [güvenilir veritabanı özelliğine](/sql/relational-databases/security/trustworthy-database-property)otomatik olarak izin vermez. Configuration Manager için bu özellik **gereklidir.**

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> SQL Server için isteğe bağlı yapılandırmalar

Aşağıdaki yapılandırmalar tam bir SQL Server yüklemesi kullanan her veritabanı için isteğe bağlıdır.  

### <a name="sql-server-service"></a>SQL Server hizmeti

SQL Server hizmetini aşağıdakileri kullanarak çalışacak şekilde yapılandırabilirsiniz:  

- *Düşük haklar etki alanı kullanıcı* hesabı:  

  - Bu yapılandırma en iyi uygulamadır ve hesabın hizmet asıl adı 'nı (SPN) el ile kaydetmenizi gerektirebilir.  

- SQL Server çalıştıran bilgisayarın **yerel sistem** hesabı:  

  - Yapılandırma işlemini basitleştirmek için yerel sistem hesabını kullanın.  
  - Yerel sistem hesabını kullandığınızda Configuration Manager, SPN 'YI SQL Server hizmeti için otomatik olarak kaydeder.  
  - SQL Server hizmeti için yerel sistem hesabını kullanmak en iyi SQL Server bir uygulamadır.  

SQL Server çalıştıran bilgisayar SQL Server hizmetini çalıştırmak için yerel sistem hesabını kullanmıyorsa, Active Directory Domain Services 'de SQL Server hizmetini çalıştıran hesabın SPN 'sini yapılandırın. (Sistem hesabı kullanıldığında, SPN sizin için otomatik olarak kaydedilir.)

Site veritabanı için SPN 'Ler hakkında bilgi için bkz. [site veritabanı sunucusu için SPN 'Yi yönetme](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN).  

SQL Server hizmeti tarafından kullanılan hesabın nasıl değiştirileceği hakkında bilgi için bkz. [SCM Hizmetleri-hizmet başlatma hesabını değiştirme](/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Raporları çalıştırmanıza olanak tanıyan bir Raporlama Hizmetleri kurmak için SQL Server Reporting Services gereklidir. Configuration Manager, site veritabanı için yaptığı gibi raporlama için SQL Server aynı sürümlerini destekler.

Daha fazla bilgi için bkz. [Configuration Manager raporlama önkoşulları](../../servers/manage/prerequisites-for-reporting.md).

> [!IMPORTANT]  
> Önceki sürümden SQL Server yükselttikten sonra, şu hatayı görebilirsiniz: *Rapor Oluşturucusu yok*.  
> Bu hatayı çözmek için, Raporlama Hizmetleri noktası site sistemi rolünü yeniden yüklemeniz gerekir.  

### <a name="data-warehouse-service-point"></a>Veri ambarı hizmet noktası

Veri ambarı ayrı bir veritabanı kullanır. Bunu site veritabanı sunucusunda veya ayrı bir SQL Server barındırabilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager için veri ambarı hizmet noktası](../../servers/manage/data-warehouse.md).

### <a name="sql-server-ports"></a>SQL Server bağlantı noktaları

SQL Server veritabanı motoruna iletişim ve siteler arası çoğaltma için, varsayılan SQL Server bağlantı noktası yapılandırmasını kullanabilir veya özel bağlantı noktaları belirleyebilirsiniz:  

- **Siteler arası iletişimler** , varsayılan olarak TCP 4022 bağlantı noktasını kullanan SQL Server hizmet Aracısı kullanır.  
- SQL Server veritabanı altyapısı ve çeşitli Configuration Manager site sistem rolleri arasındaki **site içi iletişimler** , varsayılan olarak TCP 1433 bağlantı noktasını kullanır. Aşağıdaki site sistem rolü, SQL Server veritabanıyla doğrudan iletişim kurar:  

  - Yönetim noktası  
  - SMS Sağlayıcısı bilgisayarı  
  - Raporlama hizmetleri noktası  
  - Site sunucusu  

SQL Server çalıştıran bir bilgisayar, birden fazla siteden bir veritabanı barındırıyorsa, her veritabanı ayrı bir SQL Server örneği kullanmalıdır. Ayrıca, her örnek benzersiz bir bağlantı noktası kümesi kullanacak şekilde yapılandırılmalıdır.  

> [!WARNING]  
> Configuration Manager, dinamik bağlantı noktalarını desteklemez. SQL Server adlandırılmış örnekleri, veritabanı altyapısına bağlantılar için dinamik bağlantı noktaları kullandığından, adlandırılmış bir örnek kullandığınızda, site içi iletişim için kullanmak istediğiniz statik bağlantı noktasını el ile yapılandırmanız gerekir.  

SQL Server çalıştıran bilgisayarda etkin bir güvenlik duvarınız varsa, dağıtımınızın kullandığı bağlantı noktalarına ve SQL Server iletişim kuran bilgisayarlar arasındaki ağ konumlarına izin verecek şekilde yapılandırıldığından emin olun.  

Belirli bir bağlantı noktasını kullanmak üzere SQL Server nasıl yapılandırılacağı hakkında bir örnek için, bkz. [belirli BIR TCP bağlantı noktasını dinlemek için sunucu yapılandırma](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

## <a name="upgrade-options-for-sql-server"></a>SQL Server için yükseltme seçenekleri

SQL Server sürümünüzü yükseltmeniz gerekiyorsa, daha kolay ve daha karmaşık olan aşağıdaki yöntemlerden birini kullanın:  

- [SQL Server yerinde yükseltme](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (önerilir)  

- Yeni bir bilgisayara yeni bir SQL Server sürümünü yükleyip Configuration Manager Kurulum 'un [veritabanı taşıma seçeneğini kullanarak](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) site sunucunuzu yeni SQL Server taşıyın  

- [Yedekleme ve kurtarma](../../servers/manage/backup-and-recovery.md)kullanın. SQL yükseltme senaryosu için yedekleme ve kurtarma kullanılması desteklenir. [Bir siteyi kurtarmadan önce dikkat edilmesi gereken konuları](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site)gözden geçirirken SQL sürüm oluşturma gereksinimini yoksayabilirsiniz.