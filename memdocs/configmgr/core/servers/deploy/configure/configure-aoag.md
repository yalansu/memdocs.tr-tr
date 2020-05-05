---
title: Kullanılabilirlik gruplarını yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager ile SQL Server Always on kullanılabilirlik grupları ayarlama ve yönetme
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12753b3800b3b304bd13c992b57d22bf9e1bfad8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721083"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configuration Manager için SQL Server Always on kullanılabilirlik grupları yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ile kullandığınız kullanılabilirlik gruplarını yapılandırmak ve yönetmek için bu makaledeki bilgileri kullanın.

Başlamadan önce:  

- [Configuration Manager Ile her zaman açık kullanılabilirlik grupları SQL Server kullanmaya hazırlanma](sql-server-alwayson-for-a-highly-available-site-database.md)hakkında bilgi sahibi olun.
- Kullanılabilirlik gruplarının ve ilgili yordamların kullanımını içeren SQL Server belgeleri hakkında bilgi sahibi olun. Aşağıdaki senaryolar için bu bilgiler gereklidir.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a>Kullanılabilirlik grubu oluşturma ve yapılandırma

Bir kullanılabilirlik grubu oluşturmak için aşağıdaki yordamı kullanın ve ardından site veritabanının bir kopyasını bu kullanılabilirlik grubuna taşıyın.

1. Configuration Manager sitesini durdurmak için aşağıdaki komutu kullanın:

    `preinst.exe /stopsite`

    Daha fazla bilgi için bkz. [hiyerarşi bakım aracı](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Site veritabanının yedekleme modelini **basit** iken **tam**' a değiştirin:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Kullanılabilirlik grupları yalnızca tam yedekleme modelini destekler. Daha fazla bilgi için bkz. [bir veritabanının kurtarma modelini görüntüleme veya değiştirme](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Site veritabanınızın tam yedeklemesini oluşturmak için SQL Server kullanın. Aşağıdaki seçeneklerden birini belirleyin:

    - **Kullanılabilirlik grubunuzun üyesi olacaktır**: Bu sunucuyu kullanılabilirlik grubunun ilk birincil çoğaltma üyesi olarak kullanırsanız, site veritabanının bir kopyasını bu sunucuya veya gruptaki başka bir gruba geri yüklemeniz gerekmez. Veritabanı, birincil çoğaltmada zaten var. SQL Server sonraki bir adım sırasında veritabanını ikincil çoğaltmalara çoğaltır.  

    - **Kullanılabilirlik grubunun bir üyesi**olmayacaktır: site veritabanının bir kopyasını grubun birincil çoğaltmasını barındıracak olan sunucuya geri yükleyin.

    Daha fazla bilgi için SQL Server belgelerinde aşağıdaki makalelere bakın:

    - [Tam bir veritabanı yedeklemesi oluşturma](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [SSMS kullanarak veritabanı yedeklemesini geri yükleme](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Bir kullanılabilirlik grubundan mevcut bir çoğaltmada tek başına kadar taşımayı planlıyorsanız, önce veritabanını kullanılabilirlik grubundan kaldırın.

4. Grubun ilk birincil çoğaltmasını barındıracak sunucuda, kullanılabilirlik grubunu oluşturmak için [Yeni kullanılabilirlik Grubu Sihirbazı](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) ' nı kullanın. Sihirbazda:

    - **Veritabanı Seç** sayfasında, Configuration Manager siteniz için veritabanını seçin.  

    - **Çoğaltmaları Belirle** sayfasında şunları yapılandırın:

        - **Çoğaltmalar:** İkincil çoğaltmaları barındıracak sunucuları belirtin.

        - **Dinleyici:** Örneğin `<listener_server>.fabrikam.com`, **dinleyici DNS adını** tam bir DNS adı olarak belirtin. Kullanılabilirlik grubundaki veritabanını kullanmak üzere Configuration Manager yapılandırdığınızda, bu adı kullanır.

    - **İlk Veri Eşitlemesini Seç** sayfasında **Tam**seçeneğini belirleyin. Sihirbaz, kullanılabilirlik grubunu oluşturduktan sonra, birincil veritabanını ve işlem günlüğünü yedekler. Daha sonra sihirbaz, ikincil bir çoğaltma barındıran her sunucuya onları geri yükler.

        > [!Note]  
        > Bu adımı kullanmazsanız, site veritabanının bir kopyasını bir ikincil çoğaltma barındıran her sunucuya geri yükleyin. Ardından bu veritabanını el ile gruba katın.

5. Her yinelemede yapılandırmayı denetleyin:

    1. Site sunucusunun bilgisayar hesabının, kullanılabilirlik grubunun üyesi olan her bilgisayarda yerel **Yöneticiler** grubunun bir üyesi olduğundan emin olun.  

    2. Her bir çoğaltmada site veritabanının doğru şekilde yapılandırıldığını doğrulamak için [doğrulama betiğini](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites) çalıştırın.

    3. İkincil çoğaltmalarda yapılandırmaların ayarlanması gerekiyorsa, devam etmeden önce, birincil çoğaltmanın yükünü ikincil çoğaltmaya el ile devreder. Yalnızca birincil çoğaltmanın veritabanını yapılandırabilirsiniz. Daha fazla bilgi için, SQL Server belgelerindeki [bir kullanılabilirlik grubunun planlı el ile yük devretmesini gerçekleştirme](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) konusuna bakın.

6. Tüm çoğaltmalar gereksinimleri karşıladıktan sonra, kullanılabilirlik grubu Configuration Manager birlikte kullanılmak üzere hazır olur.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a>Bir siteyi kullanılabilirlik grubunu kullanacak şekilde yapılandırma

[Kullanılabilirlik grubunu oluşturup yapılandırdıktan](#bkmk_create)sonra, siteyi kullanılabilirlik grubunun barındırdığı veritabanını kullanacak şekilde yapılandırmak için Configuration Manager Site Bakımı ' nı kullanın.

Bir kullanılabilirlik grubunda veritabanına sahip yeni bir site yüklemek desteklenmez. Örneğin, temel medya kullanıyorsanız, SQL Server tek bir örneğini kullanarak siteyi yükleyebilirsiniz. Site yüklendikten sonra, site veritabanını kullanılabilirlik grubuna taşıyın.

1. **Configuration Manager Kurulum**: `\BIN\X64\setup.exe` Configuration Manager site yükleme klasöründen çalıştırın.

2. **Başlarken** sayfasında, **Site bakımı yap veya bu siteyi sıfırla**' yı seçin ve ardından **İleri**' yi seçin.

3. **SQL Server yapılandırmayı Değiştir**' i seçin ve ardından **İleri**' yi seçin.

4. Site veritabanı için aşağıdaki ayarları yeniden yapılandırın:

    - **SQL Server adı**: kullanılabilirlik grubu *dinleyicisinin*sanal adını girin. Kullanılabilirlik grubunu oluştururken dinleyiciyi yapılandırdınız. Sanal ad, gibi `<Listener_Server>.fabrikam.com`BIR tam DNS adı olmalıdır.  

    - **Örnek:** Kullanılabilirlik grubu *dinleyicisinin* varsayılan örneğini belirtmek için bu değer boş olmalıdır. Geçerli site veritabanı adlandırılmış bir örnek üzerinde çalışıyorsa, geçerli adlı örneği temizleyin.

    - **Veritabanı** : Adı göründüğü gibi bırakın. Bu ad, geçerli site veritabanıdır.

5. Yeni veritabanı konumu bilgilerini girdikten sonra, kurulum 'u normal işlem ve konfigürasyonlarınızla doldurun.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a>Zaman uyumlu çoğaltma üyeleri  

Site veritabanınız bir kullanılabilirlik grubunda barındırılıyorsa, zaman uyumlu çoğaltma üyelerini eklemek veya kaldırmak için aşağıdaki yordamları kullanın. Desteklenen tür ve çoğaltma sayısı hakkında daha fazla bilgi için bkz. [kullanılabilirlik grubu yapılandırması](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations).

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a>Yeni bir zaman uyumlu çoğaltma üyesi ekleyin

<!--3127336-->
Sürüm 1906 ' den başlayarak yeni bir zaman uyumlu çoğaltma üyesi eklemek için Configuration Manager Kurulum 'u çalıştırın.

1. SQL Server yordamlarını kullanarak bir ikincil çoğaltma ekleyin.

    1. [Her zaman açık kullanılabilirlik grubuna ikincil çoğaltma ekleyin](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. SQL Management Studio 'de durumu izleyin. Kullanılabilirlik grubunun tam sistem durumuna dönmesi için bekleyin.

1. Configuration Manager kurulumunu çalıştırın ve siteyi değiştirme seçeneğini belirleyin.

1. Kullanılabilirlik grubu dinleyicisi adını veritabanı adı olarak belirtin. Dinleyici standart olmayan bir ağ bağlantı noktası kullanıyorsa, bunu da belirtin. Bu eylem, kurulumun her bir düğümün uygun şekilde yapılandırıldığından emin olmasına neden olur. Ayrıca bir veritabanı kurtarma işlemi başlatır.

Configuration Manager Kurulum, SQL veritabanı taşıma işlemini kullanır ve düğümlerin doğru şekilde yapılandırıldığından emin olur.

Bu işlemi sürüm 1902 veya önceki sürümlerde el ile yapma hakkında daha fazla bilgi için bkz. [ConfigMgr 1702: var olan BIR SQL Ao AG 'ye yeni düğüm ekleme (Ikincil çoğaltma)](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960).

### <a name="remove-a-replica-member"></a>Çoğaltma üyesini kaldırma

Sürüm 1906 ' den başlayarak, bir çoğaltma üyesini kaldırmak için Configuration Manager kurulumunu kullanabilirsiniz. [Yeni bir zaman uyumlu çoğaltma üyesi eklemek](#bkmk_sync-add)için aynı işlemi kullanın.

Bu işlemi sürüm 1902 veya önceki sürümlerde el ile yapma hakkında daha fazla bilgi için bkz. [kullanılabilirlik grubundan ikincil çoğaltmayı kaldırma](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server).  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a>Zaman uyumsuz çoğaltmalar

Configuration Manager ile kullandığınız kullanılabilirlik grubunda zaman uyumsuz bir çoğaltma kullanabilirsiniz. Zaman uyumsuz çoğaltma, site veritabanı için desteklenmediğinden zaman uyumlu bir çoğaltma yapılandırmak için gereken yapılandırma betiklerini çalıştırmanız gerekmez.

### <a name="configure-an-asynchronous-commit-replica"></a>Zaman uyumsuz bir kayıt çoğaltması yapılandırma

Daha fazla bilgi için bkz. [kullanılabilirlik grubuna ikincil çoğaltma ekleme](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Sitenizi kurtarmak için zaman uyumsuz çoğaltmayı kullanın

Site veritabanınızı kurtarmak için zaman uyumsuz çoğaltmayı kullanın.

1. Site veritabanına ek yazma işlemlerini engellemek için etkin birincil siteyi durdurun. Siteyi durdurmak için [Hiyerarşi Bakımı aracını](../../manage/hierarchy-maintenance-tool-preinst.exe.md)kullanın:`preinst.exe /stopsite`

1. Siteyi durdurduktan sonra, [el ile kurtarılan bir veritabanı](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered)yerine zaman uyumsuz çoğaltmayı kullanın.


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a>Kullanılabilirlik grubu kullanmayı durdur

Site veritabanınızı artık bir kullanılabilirlik grubunda barındırmak istemediğinizde aşağıdaki yordamı kullanın. Bu işlemle, site veritabanını SQL Server tek bir örneğine geri taşıyacaksınız.

1. Aşağıdaki komutu kullanarak Configuration Manager sitesini durdurun: `preinst.exe /stopsite`. Daha fazla bilgi için bkz. [hiyerarşi bakım aracı](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. SQL Server’ı kullanarak birincil çoğaltmadan site veritabanınızın tam bir yedeklemesini oluşturun. Daha fazla bilgi için bkz. [tam bir veritabanı yedeklemesi oluşturma](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. SQL Server’ı kullanarak site veritabanı yedeklemesini, site veritabanını barındıracak sunucuya geri yükleyin. Daha fazla bilgi için bkz. [SSMS kullanarak veritabanı yedeklemesini geri yükleme](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > Kullanılabilirlik grubu için birincil çoğaltma sunucusu, site veritabanının tek örneğini barındıracaktır, bu adımı atlayın.

4. Site veritabanını barındıracak sunucuda, site veritabanı için yedekleme modelini **tam** iken **basit**olarak değiştirin. Daha fazla bilgi için bkz. [bir veritabanının kurtarma modelini görüntüleme veya değiştirme](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. **Configuration Manager Kurulum**: `\BIN\X64\setup.exe` Configuration Manager site yükleme klasöründen çalıştırın.

6. **Başlarken** sayfasında, **Site bakımı yap veya bu siteyi sıfırla**' yı seçin ve ardından **İleri**' yi seçin.  

7. **SQL Server yapılandırmayı Değiştir**' i seçin ve ardından **İleri**' yi seçin.  

8. Site veritabanı için aşağıdaki ayarları yeniden yapılandırın:

    - **SQL Server adı** : Şimdi site veritabanını barındıran sunucunun adını girin.

    - **Örnek:** Site veritabanını barındıran adlandırılmış örneği belirtin. Veritabanı varsayılan örnekte ise, bu alanı boş bırakın.

    - **Veritabanı** : Adı göründüğü gibi bırakın. Bu ad, geçerli site veritabanıdır.

9. Yeni veritabanı konumu bilgilerini girdikten sonra, kurulum 'u normal işlem ve konfigürasyonlarınızla doldurun. Kurulum tamamlandığında, site yeniden başlatılır ve yeni veritabanı konumunu kullanmaya başlar.

10. Kullanılabilirlik grubunun üyesi olan sunucuları temizlemek için, [kullanılabilirlik grubunu kaldırma](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server)bölümündeki yönergeleri izleyin.
