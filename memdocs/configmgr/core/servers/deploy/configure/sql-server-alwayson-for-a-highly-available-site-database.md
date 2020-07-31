---
title: SQL Server Always On
titleSuffix: Configuration Manager
description: Configuration Manager ile SQL Server Always on kullanılabilirlik grubu kullanmayı planlayın
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05553af3e973805eed62c68f13afc3cf7d3d2ee3
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438591"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Configuration Manager ile Always on kullanılabilirlik grupları SQL Server kullanmaya hazırlanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager SQL Server Always on kullanılabilirlik grupları 'nı kullanmak üzere hazırlamak için bu makaleyi kullanın. Bu özellik, site veritabanı için yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümü sağlar.  

Kullanılabilirlik gruplarının kullanımını Configuration Manager destekler:

- Birincil sitelerde ve merkezi yönetim sitesinde.
- Şirket içinde veya Microsoft Azure.

Microsoft Azure ' de kullanılabilirlik grupları kullandığınızda, *Azure kullanılabilirlik kümelerini*kullanarak site veritabanınızın kullanılabilirliğini daha da artırabilirsiniz. Azure Kullanılabilirlik Kümeleri hakkında daha fazla bilgi için bkz. [Sanal makinelerin kullanılabilirliğini yönetme](/azure/virtual-machines/windows/manage-availability).

> [!Important]
> Devam etmeden önce, SQL Server ve SQL Server kullanılabilirlik gruplarını yapılandırmaya rahat olun. Aşağıdaki bilgiler SQL Server belge kitaplığına ve yordamlarına başvurur.


## <a name="supported-scenarios"></a>Desteklenen senaryolar

Configuration Manager ile kullanılabilirlik gruplarının kullanılması için aşağıdaki senaryolar desteklenir. Her senaryoya ilişkin daha fazla bilgi ve yordam için bkz. [Configuration Manager için kullanılabilirlik gruplarını yapılandırma](configure-aoag.md).

- [Configuration Manager ile kullanmak için bir kullanılabilirlik grubu oluşturun](configure-aoag.md#bkmk_create)  
- [Bir siteyi kullanılabilirlik grubunu kullanacak şekilde yapılandırma](configure-aoag.md#bkmk_configure)  
- [Site veritabanını barındıran bir kullanılabilirlik grubundan zaman uyumlu çoğaltma üyeleri ekleme veya kaldırma](configure-aoag.md#bkmk_sync)  
- [Bir siteyi zaman uyumsuz bir kayıt Çoğaltmalarından yapılandırma veya kurtarma](configure-aoag.md#bkmk_async)  
- [Site veritabanını bir kullanılabilirlik grubunun dışına, tek başına SQL Server varsayılan veya adlandırılmış bir örneğine taşıyın](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>Ön koşullar

Aşağıdaki Önkoşullar tüm senaryolar için geçerlidir. Belirli bir senaryoya ek önkoşullar uygulandıklarında, bu senaryoya göre ayrıntılandırılmıştır.

### <a name="configuration-manager-accounts-and-permissions"></a>Configuration Manager hesapları ve izinleri

#### <a name="installation-account"></a>Yükleme hesabı

Configuration Manager kurulumu 'nu çalıştırmak için kullandığınız hesap şu olmalıdır:

- Kullanılabilirlik grubunun üyesi olan her bilgisayarda yerel **Yöneticiler** grubunun bir üyesi.
- Site veritabanını barındıran SQL Server her bir örneğinde **sysadmin** .

#### <a name="site-server-to-replica-member-access"></a>Site sunucusundan çoğaltma üyesine erişim

Site sunucusunun bilgisayar hesabı, kullanılabilirlik grubunun üyesi olan her bilgisayarda yerel **Yöneticiler** grubunun bir üyesi olmalıdır.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Sürüm

Kullanılabilirlik grubundaki her çoğaltmanın, Configuration Manager sürümünüz tarafından desteklenen bir SQL Server sürümü çalıştırması gerekir. SQL Server tarafından desteklenerek, bir kullanılabilirlik grubunun farklı düğümleri SQL Server farklı sürümlerini çalıştırabilir. Daha fazla bilgi için bkz. [Configuration Manager Için desteklenen SQL Server sürümleri](../../../plan-design/configs/support-for-sql-server-versions.md).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Sürüm

SQL Server *Enterprise* sürümünü kullanın.

#### <a name="account"></a>Hesap

Her SQL Server örneği, bir etki alanı kullanıcı hesabı (**hizmet hesabı**) veya etki alanı olmayan bir hesap altında çalıştırılabilir. Bir gruptaki her çoğaltmanın farklı bir yapılandırması olabilir.

- Mümkün olan en düşük izinlere sahip bir hesap kullanın. Daha fazla bilgi için bkz. [SQL Server yükleme Için güvenlik konuları](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- SQL Server için hizmet hesaplarını ve izinleri yapılandırma hakkında daha fazla bilgi için bkz. [Windows hizmet hesaplarını ve Izinlerini yapılandırma](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Etki alanı olmayan bir hesabı kullanmak için sertifikaları kullanmanız gerekir. Daha fazla bilgi için bkz. [veritabanı yansıtma uç noktası için sertifikaları kullanma (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Daha fazla bilgi için bkz. [Always on kullanılabilirlik grupları için veritabanı yansıtma uç noktası oluşturma](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="database"></a>Veritabanı

#### <a name="configure-the-database-on-a-new-replica"></a>Veritabanını yeni bir çoğaltmada yapılandırma

Her çoğaltmanın veritabanını aşağıdaki ayarlarla yapılandırın:  

- **Clr tümleştirmesini**etkinleştir:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Daha fazla bilgi için bkz. [clr tümleştirmesi](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- **En büyük metin REPL boyutunu** ayarla `2147483647` :  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Veritabanı sahibini *sa hesabı*olarak ayarlayın. Bu hesabı etkinleştirmeniz gerekmez.

- **Güvenilir** **ayarı açın:**

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Daha fazla bilgi için [güvenilir veritabanı özelliğine](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property)bakın.

- **Hizmet Aracısı**etkinleştirin:  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > Kullanılabilirlik grubunun zaten bir parçası olan bir veritabanında Hizmet Aracısı seçeneğini etkinleştiremezsiniz. Kullanılabilirlik grubuna eklemeden önce bu seçeneği etkinleştirmeniz gerekir.<!-- SCCMDocs#1432 -->

- Hizmet Aracısı önceliğini yapılandırın:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Bu konfigürasyonları yalnızca birincil çoğaltma üzerinde yapın. İkincil bir çoğaltmayı yapılandırmak için öncelikle birincili ikinciye yük devreder. Bu eylem, ikincili yeni birincil çoğaltmayı yapar.

#### <a name="database-verification-script"></a>Veritabanı doğrulama betiği

Birincil ve ikincil çoğaltmalara yönelik veritabanı yapılandırmasını doğrulamak için aşağıdaki SQL betiğini çalıştırın. İkincil bir çoğaltmada bir sorunu çözebilmeniz için önce söz konusu ikincil çoğaltmanın birincil çoğaltma olacak şekilde değiştirin.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Kullanılabilirlik grubu konfigürasyonları

#### <a name="replica-members"></a>Çoğaltma üyeleri

- Kullanılabilirlik grubu bir birincil çoğaltmaya sahip olmalıdır.  

- SQL Server sürümlerinizin desteklediği bir kullanılabilirlik grubundaki çoğaltmaların aynı sayısını ve türünü kullanın.

- Zaman uyumsuz bir kayıt çoğaltmasını, zaman uyumlu çoğaltmanızı kurtarmak için kullanabilirsiniz. Daha fazla bilgi için bkz. [site veritabanı kurtarma seçenekleri](../../manage/recover-sites.md#site-database-recovery-options).  

    > [!Warning]  
    > Configuration Manager, site veritabanınız olarak zaman uyumsuz tamamlama çoğaltmasını kullanmak için *Yük devretmeyi* desteklemez. Daha fazla bilgi için bkz. [Yük devretme ve yük devretme modları (Always on kullanılabilirlik grupları)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

Configuration Manager, zaman uyumsuz tamamlama çoğaltmasının geçerli olduğunu doğrulamak için durumunu doğrulamaz. Site veritabanı olarak zaman uyumsuz bir kayıt çoğaltmasının kullanımı sitenizin bütünlüğünü ve verilerinizi riske koyabilirler. Bu çoğaltma, tasarım ile eşitlenmemiş olabilir. Daha fazla bilgi için bkz. [SQL Server Always on kullanılabilirlik gruplarına genel bakış](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Her çoğaltma üyesinin aşağıdaki yapılandırması olmalıdır:

- *Varsayılan örneği* veya *adlandırılmış bir örneği* kullanın  

- **Birincil roldeki bağlantılar** ayarı **tüm bağlantılara izin ver**  

- **Okunabilir ikincil** ayar **Evet** ' tir  

- **El Ile yük devretme** için etkinleştirildi

    > [!Note]
    > Sürüm 1902 ve önceki sürümlerde, el ile yük devretme için SQL Server tüm kullanılabilirlik gruplarını yapılandırmanız gerekir. Bu yapılandırma, site veritabanını barındırmasa bile gereklidir.
    >
    > Sürüm 1906 ' den başlayarak, Configuration Manager **otomatik yük devretme**için ayarlandığında kullanılabilirlik grubu zaman uyumlu çoğaltmalarının kullanılmasını destekler. Şu durumlarda **El Ile yük devretme** ayarla:
    >
    > - Kullanılabilirlik grubundaki site veritabanının kullanımını belirtmek için Configuration Manager kurulumunu çalıştırırsınız.  
    > - Configuration Manager için herhangi bir güncelleştirmeyi yüklersiniz. (Yalnızca site veritabanı için uygulanan güncelleştirmeler değil).  

- Tüm üyelerin aynı [dengeli dağıtım moduna](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)ihtiyacı vardır.<!-- SCCMDocs-pr#3899 --> Configuration Manager Kurulum, yükleme veya kurtarma aracılığıyla bir veritabanı oluştururken bu yapılandırmayı doğrulamak için bir önkoşul denetimi içerir.

    > [!Note]  
    > Kurulum veritabanını oluşturduğunda ve **Otomatik** dengeli dağıtım yapılandırdığınızda, kullanılabilirlik grubunun veritabanını oluşturmak için izinleri olması gerekir. Bu gereksinim, hem yeni bir veritabanı ya da kurtarma için geçerlidir. Daha fazla bilgi için bkz. [ikincil çoğaltma Için otomatik dengeli dağıtım](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security).<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Çoğaltma üyesi konumu

Tüm çoğaltmaları şirket içinde bir kullanılabilirlik grubunda barındırın veya Microsoft Azure tümünü barındırın. Şirket içi bir üyeyi ve Azure 'daki bir üyeyi içeren bir grup desteklenmez.

> [!NOTE]
> SQL Server için bir Azure sanal makinesi kullanıyorsanız, **kayan IP**'yi etkinleştirin. Daha fazla bilgi için bkz. [Azure sanal makinelerinde SQL Server Always on kullanılabilirlik grubu için yük dengeleyici yapılandırma](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/availability-group-load-balancer-portal-configure).<!-- SCCMDocs#1928 -->

Configuration Manager Kurulum 'un her bir çoğaltmaya bağlanması gerekiyor. Azure 'da bir kullanılabilirlik grubu ayarladığınızda ve grup bir iç veya dış yük dengeleyicinin arkasında olduğunda, aşağıdaki varsayılan bağlantı noktalarını açın:

- RPC uç nokta Eşleyici: **TCP 135**

- SQL Server Hizmet Aracısı: **TCP 4022**  

- TCP üzerinden SQL: **tcp 1433**

Kurulum tamamlandıktan sonra, bu bağlantı noktalarının Configuration Manager ve çoğaltma bağlantısı Çözümleyicisi için açık kalması gerekir.<!-- MEMDocs#375 -->

Bu yapılandırmalarda özel bağlantı noktalarını kullanabilirsiniz. Uç nokta ve kullanılabilirlik grubundaki tüm çoğaltmalarda aynı özel bağlantı noktalarını kullanın.

SQL 'in siteler arasında veri çoğaltması için, Azure Yük dengeleyicideki her bağlantı noktası için bir yük dengeleme kuralı oluşturun. Daha fazla bilgi için bkz. [bir iç yük dengeleyici Için yüksek kullanılabilirlik bağlantı noktalarını yapılandırma](https://docs.microsoft.com/azure/load-balancer/load-balancer-configure-ha-ports).<!-- MEMDocs#252 -->

#### <a name="listener"></a>Dinleyici

Kullanılabilirlik grubunun en az bir *kullanılabilirlik grubu dinleyicisi*olmalıdır. Kullanılabilirlik grubundaki site veritabanını kullanmak üzere Configuration Manager yapılandırdığınızda, bu dinleyicinin sanal adını kullanır. Bir kullanılabilirlik grubu birden çok dinleyici içerebilse de Configuration Manager yalnızca birini kullanabilir. Daha fazla bilgi için bkz. [SQL Server kullanılabilirlik grubu dinleyicisi oluşturma veya yapılandırma](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Dosya yolları

Bir siteyi bir kullanılabilirlik grubundaki veritabanını kullanacak şekilde yapılandırmak için Configuration Manager kurulumunu çalıştırdığınızda, her ikincil çoğaltma sunucusunun, geçerli birincil çoğaltmadaki site veritabanı dosyaları için dosya yoluyla aynı olan bir SQL Server dosya yoluna sahip olması gerekir. Özdeş bir yol yoksa, kurulum, site veritabanının yeni konumu olarak kullanılabilirlik grubuna ilişkin örneği ekleyemez.  

Yerel SQL Server hizmet hesabının bu klasörde **tam denetim** izni olmalıdır.

Bu dosya yolu, ikincil çoğaltma sunucularına yalnızca kullanılabilirlik grubundaki veritabanı örneğini belirtmek için Configuration Manager Kurulum 'u kullanırken gereklidir. Kullanılabilirlik grubundaki site veritabanının yapılandırmasını tamamladıktan sonra, kullanılmayan yolu ikincil çoğaltma grubundan silebilirsiniz.

Örneğin, aşağıdaki senaryoları düşünün:

- Üç SQL Server kullanan bir kullanılabilirlik grubu oluşturursunuz.  

- Birincil çoğaltma sunucunuz, SQL Server 2014’ün yeni bir yüklemesi olsun. Varsayılan olarak, veritabanını depolar. MDF ve. İçindeki LDF dosyaları `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` .  

- İkincil çoğaltma sunucularınızın her ikisini de önceki sürümlerden SQL Server 2014 sürümüne yükselttiniz. Bu sunucular, yükseltme ile veritabanı dosyalarını depolamak için özgün dosya yolunu tutar: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA` .  

- Site veritabanını bu kullanılabilirlik grubuna taşımadan önce, her bir ikincil çoğaltma sunucusunda şu dosya yolunu oluşturun: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` . Bu yol, ikincil çoğaltmalar bu dosya konumunu kullanmasa bile, birincil Çoğaltmada kullanılan yolun bir yinelemesi olur.  

- Ardından, her bir ikincil çoğaltmada SQL Server hizmet hesabına, bu sunucudaki yeni oluşturulan dosya konumuna tam denetim erişimi verirsiniz.  

- Artık siteyi kullanılabilirlik grubundaki site veritabanını kullanacak şekilde yapılandırmak için Configuration Manager kurulumunu başarıyla çalıştırabilirsiniz.  

#### <a name="multi-subnet-failover"></a>Çoklu alt ağ yük devretme

<!-- SCCMDocs-pr#3734 -->
Sürüm 1906 ' den başlayarak [MultiSubnetFailover Bağlantı dizesi anahtar sözcüğünü](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) SQL Server etkinleştirebilirsiniz. Ayrıca, aşağıdaki değerleri site sunucusundaki Windows kayıt defterine el ile eklemeniz gerekir:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> [Site sunucusu yüksek kullanılabilirlik](site-server-high-availability.md) kullanımı ve çoklu alt ağ yük devretmesi her zaman açık SQL Server, olağanüstü durum kurtarma senaryoları için otomatik yük devretmenin tam yeteneklerini sağlamaz.

Uzak bir konumda bir üyeye sahip bir kullanılabilirlik grubu oluşturmanız gerekiyorsa, en düşük ağ gecikme süresine göre öncelik verir. Yüksek ağ gecikmesi çoğaltma hatalara neden olabilir.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Sınırlamalar ve bilinen sorunlar

Aşağıdaki sınırlamalar tüm senaryolar için geçerlidir.

### <a name="unsupported-sql-server-options-and-configurations"></a>Desteklenmeyen SQL Server seçenekleri ve yapılandırmalar

- **Temel kullanılabilirlik grupları**: SQL Server 2016 Standard Edition ile birlikte sunulan temel kullanılabilirlik grupları, ikincil çoğaltmalara okuma erişimini desteklemez. Yapılandırma bu erişimi gerektirir. Daha fazla bilgi için bkz. [temel SQL Server kullanılabilirlik grupları](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Yük devretme kümesi örneği**: Configuration Manager ile kullandığınız bir çoğaltma için yük devretme kümesi örnekleri desteklenmez. Daha fazla bilgi için bkz. [SQL Server her zaman yük devretme kümesi örnekleri](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: sürüm 1902 ve önceki sürümlerde, birden çok alt ağ yapılandırmasında Configuration Manager olan bir kullanılabilirlik grubu kullanılması desteklenmez. Ayrıca, [Mutlısubnetfailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) anahtar sözcük bağlantı dizesini de kullanamazsınız.

    Bu yapılandırmayı desteklemek için Configuration Manager sürüm 1906 veya sonraki bir sürüme güncelleştirin. Daha fazla bilgi için bkz. [Çoklu alt ağ yük devretme](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover) önkoşulu.

### <a name="sql-servers-that-host-additional-availability-groups"></a>Ek kullanılabilirlik grupları barındıran SQL Server 'Lar

<!--SCCMDocs issue 649-->
SQL Server, Configuration Manager için kullandığınız gruba ek olarak bir veya daha fazla kullanılabilirlik grubu barındırdığınızda, Configuration Manager Kurulum 'u çalıştırdığınız zaman belirli ayarlara ihtiyaç duyuyor. Bu ayarlar, Configuration Manager için bir güncelleştirme yüklemek için de gereklidir. Her bir kullanılabilirlik grubundaki her çoğaltmanın aşağıdaki yapılandırmalara sahip olması gerekir:

- El ile yük devretme  
- Tüm salt okunurdur bağlantıya izin ver  

> [!Note]
> Sürüm 1902 ve önceki sürümlerde, el ile yük devretme için SQL Server tüm kullanılabilirlik gruplarını yapılandırmanız gerekir. Bu yapılandırma, site veritabanını barındırmasa bile gereklidir.
>
> Sürüm 1906 ' den başlayarak, Configuration Manager **otomatik yük devretme**için ayarlandığında kullanılabilirlik grubu zaman uyumlu çoğaltmalarının kullanılmasını destekler. Şu durumlarda **El Ile yük devretme** ayarla:
>
> - Kullanılabilirlik grubundaki site veritabanının kullanımını belirtmek için Configuration Manager kurulumunu çalıştırırsınız.  
> - Configuration Manager için herhangi bir güncelleştirmeyi yüklersiniz. (Yalnızca site veritabanı için uygulanan güncelleştirmeler değil).  

### <a name="unsupported-database-use"></a>Desteklenmeyen veritabanı kullanımı

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager, yalnızca bir kullanılabilirlik grubundaki site veritabanını destekler

Aşağıdaki veritabanları Configuration Manager tarafından SQL Server Always on kullanılabilirlik grubunda desteklenmez:  

- Raporlama veritabanı  
- WSUS veritabanı  

#### <a name="pre-existing-database"></a>Önceden var olan veritabanı

Çoğaltmada oluşturulan yeni bir veritabanını kullanamazsınız. Bir kullanılabilirlik grubu yapılandırdığınızda, mevcut bir Configuration Manager veritabanının bir kopyasını birincil çoğaltmaya geri yükleyin.  

#### <a name="distributed-views"></a>Dağıtılmış görünümler

<!-- SCCMDocs-pr#3792 -->
Sürüm 1902 ve önceki sürümlerde, site veritabanını SQL Server Always on kullanılabilirlik grubunda barındırdıysanız, veritabanı çoğaltması için [dağıtılmış görünümleri](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) etkinleştiremezsiniz. Bu yapılandırmayı desteklemek için sürüm 1906 veya sonraki bir sürüme güncelleştirin.


### <a name="setup-errors-in-configmgrsetuplog"></a>ConfigMgrSetup. log dosyasında kurulum hataları

Bir site veritabanını bir kullanılabilirlik grubuna taşımak için Configuration Manager kurulumu çalıştırdığınızda, kullanılabilirlik grubunun ikincil çoğaltmalarındaki veritabanı rollerini işlemeye çalışır. **ConfigMgrSetup. log** dosyası aşağıdaki hatayı gösterir:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Bu hataların yok sayılacağını güvende.

### <a name="site-expansion"></a>Site genişletmesi

<!--SCCMDocs issue 568-->
Tek başına birincil sitenin site veritabanını SQL Always on kullanacak şekilde yapılandırırsanız siteyi bir merkezi yönetim sitesi içerecek şekilde genişletemez. Bu işlemi denerseniz, başarısız olur. Siteyi genişletmek için, birincil site veritabanını geçici olarak kullanılabilirlik grubundan kaldırın.

İkincil site eklerken yapılandırmada herhangi bir değişiklik yapmanız gerekmez.


## <a name="changes-for-site-backup"></a>Site yedekleme değişiklikleri

### <a name="backup-database-files"></a>Veritabanı dosyalarını yedekleme
  
Bir site veritabanı bir kullanılabilirlik grubu kullandığında, ortak Configuration Manager ayarlarını ve dosyalarını yedeklemek için yerleşik **yedekleme site sunucusu** bakım görevini çalıştırın. Kullanmayın. MDF veya. Bu yedekleme tarafından oluşturulan LDF dosyaları. Bunun yerine, SQL Server kullanarak bu veritabanı dosyalarının doğrudan yedeklerini yapın.

### <a name="transaction-log"></a>İşlem günlüğü  

Site veritabanının kurtarma modelini **tam**olarak ayarlayın. Bu yapılandırma, bir kullanılabilirlik grubunda Configuration Manager kullanımı için gereksinimdir. Site veritabanı işlem günlüğünün boyutunu izlemeyi ve korumayı planlayın. Tam kurtarma modelinde, veritabanının veya işlem günlüğünün tam yedeklemesini yapana kadar işlemler sağlamolmaz. Daha fazla bilgi için bkz. [SQL Server veritabanlarının yedeklenmesi ve geri yüklenmesi](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).


## <a name="changes-for-site-recovery"></a>Site Recovery değişiklikleri

Kullanılabilirlik grubunun en az bir düğümü hala çalışır durumda ise, veritabanı kurtarmayı atlamak için Site Recovery seçeneğini kullanın **(site veritabanı etkilenmediyse bu seçeneği kullanın)**.

Sürüm 1906 ' den başlayarak, Site Recovery veritabanını bir SQL Always on grubunda yeniden oluşturabilir. Bu işlem hem el ile hem de otomatik dengeli çalışma ile birlikte çalışabilir.<!-- SCCMDocs-pr#3846 -->

Sürüm 1902 veya önceki sürümlerde, bir kullanılabilirlik grubunun tüm düğümlerini kaybederseniz, siteyi kurtarabilmeniz için önce kullanılabilirlik grubunu yeniden oluşturun. Configuration Manager kullanılabilirlik düğümünü yeniden oluşturamıyor veya geri yükleyemiyor. Grubu yeniden oluşturun, yedeklemeyi geri yükleyin ve SQL 'i yeniden yapılandırın. Ardından, veritabanı kurtarmayı atlamak için Site Recovery seçeneğini kullanın **(site veritabanı etkilenmediyse bu seçeneği kullanın)**.

Daha fazla bilgi için bkz. [yedekleme ve kurtarma](../../manage/backup-and-recovery.md).


## <a name="changes-for-reporting"></a>Raporlama değişiklikleri

### <a name="install-the-reporting-service-point"></a>Raporlama hizmet noktasını yükler

Raporlama Hizmetleri noktası, kullanılabilirlik grubunun dinleyici sanal adının kullanımını desteklemiyor. Ayrıca, veritabanını SQL Server Always on kullanılabilirlik grubunda barındırmayı desteklemez.  

- Varsayılan olarak, Raporlama Hizmetleri noktası yüklemesi, **site veritabanı sunucu adını** dinleyici olarak belirtilen sanal ad olarak ayarlar. Kullanılabilirlik grubundaki bir çoğaltmanın bir bilgisayar adını ve örneğini belirtmek için bu ayarı değiştirin.  

- Raporlamayı devretmek ve bir çoğaltma düğümü çevrimdışıyken kullanılabilirliği artırmak için, her bir çoğaltma düğümüne ek raporlama hizmetleri noktaları yüklemeyi göz önünde bulundurun. Sonra her bir raporlama hizmetleri noktasını kendi bilgisayar adını kullanacak şekilde yapılandırın. Kullanılabilirlik grubunun her çoğaltmasına bir raporlama hizmeti noktası yüklediğinizde, raporlama her zaman etkin bir Raporlama noktası sunucusuna bağlanabilir.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Konsol tarafından kullanılan raporlama hizmetleri noktasını değiştirme

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin.

1. Şeritte **rapor seçenekleri**' ni seçin.  

1. Rapor Seçenekleri iletişim kutusunda, kullanmak istediğiniz raporlama hizmetleri noktasını seçin.  


## <a name="next-steps"></a>Sonraki adımlar

Bu makalede, kullanılabilirlik grupları kullanırken Configuration Manager gereken yaygın görevlere yönelik önkoşullar, sınırlamalar ve değişiklikler açıklanmaktadır. Sitenizi kullanılabilirlik grupları kullanacak şekilde ayarlamaya ve yapılandırmaya yönelik yordamlar için bkz. [kullanılabilirlik gruplarını yapılandırma](configure-aoag.md).
