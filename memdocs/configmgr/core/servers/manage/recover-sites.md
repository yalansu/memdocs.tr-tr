---
title: Site kurtarma
titleSuffix: Configuration Manager
description: Configuration Manager ' de sitelerinizi kurtarmayı öğrenin.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 14f319cfa1d09cf21cc5da5ed4a9fde9b9b9799b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723869"
---
# <a name="recover-a-configuration-manager-site"></a>Bir Configuration Manager sitesini kurtarma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir site hata verdiğinde veya site veritabanında veri kaybı oluştuktan sonra Configuration Manager bir Site Recovery çalıştırın. Verilerin onarımı ve yeniden eşitlenmesi, site kurtarmasının temel görevleridir ve işlemlerin kesintiye uğramasını önlemek için gereklidir.

Bu makaledeki bölümler bir Configuration Manager sitesini kurtarmanıza yardımcı olabilir. Bir yedekleme oluşturmak için bkz. [yedekleme Configuration Manager](backup-and-recovery.md).

## <a name="considerations-before-recovering-a-site"></a>Bir siteyi kurtarmadan önce dikkat edilecek noktalar

> [!Important]  
> Bu bilgiler yalnızca Site Recovery senaryolarında geçerlidir. Şirket içi altyapınızı yükselttiğinizde ve başarısız bir siteyi etkin bir şekilde kurtarırken, aşağıdaki makalelerde yer alan bilgileri gözden geçirin:
>
> - [Şirket içi altyapıyı yükseltme](upgrade-on-premises-infrastructure.md)
> - [Altyapınızı değiştirme](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>Sunucu donanımını hazırlama

<!-- 2841893 -->

Site sunucusunda mevcut yapılandırmaların mevcut olmadığından emin olun. Önceki tüm konfigürasyonlar, Site Recovery işlemi sırasında çakışmalara neden olabilir. Sunucu donanımı için aşağıdaki seçeneklerden birini kullanın:

- Genel ve kurtarma gereksinimlerini karşılayan yeni bir sunucu kullanın.

- Diskleri biçimlendirin ve işletim sistemini mevcut sunucuya yeniden yükleyin. Genel ve kurtarma gereksinimlerini karşıladığından emin olun.

- Temizlediğiniz var olan bir sunucuyu yeniden kullanma

Var olan bir sunucuyu temizlemek için aşağıdaki yordamlardan birini kullanın:

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>Var olan bir sunucuyu yalnızca site sunucusu kurtarması için temizle

1. SMS kayıt defteri anahtarlarını silme:`HKLM\Software\Microsoft\SMS`
2. İle `SMS` başlayan tüm kayıt defteri girdilerini silin `HKLM\System\CurrentControlSet\Services`. Örneğin:
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. Configuration Manager konsolunu kaldırma
4. Sunucuyu yeniden başlatın
5. Yukarıdaki tüm kayıt defteri anahtarlarının silindiğini doğrulayın.

Sunucu artık Configuration Manager restore yordamı için hazırdır.

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>Var olan bir sunucuyu yalnızca site veritabanı kurtarması için temizle

1. Site veritabanını yedekleyin. Ayrıca, WSUS gibi diğer destekleyici veritabanlarını da yedekleyin.
2. SQL Server adını ve örnek adını aklınızda olduğunuzdan emin olun
3. Site veritabanını SQL Server el ile silin
4. SQL Server yeniden başlatın

Sunucu artık Configuration Manager restore yordamı için hazırdır.

#### <a name="clean-an-existing-server-for-full-recovery"></a>Tam kurtarma için mevcut bir sunucuyu Temizleme

1. Site veritabanını yedekleyin. Ayrıca, WSUS gibi diğer destekleyici veritabanlarını da yedekleyin.
2. İçerik kitaplığının bir kopyasını oluşturun
3. Site veritabanını SQL Server el ile silin
4. Configuration Manager sitesini kaldırma
5. Configuration Manager yükleme klasörünü ve diğer Configuration Manager klasörlerini el ile silin
6. Sunucuyu yeniden başlatın
7. İçerik kitaplığını ve WSUS gibi diğer veritabanlarını geri yükleme

Sunucu artık Configuration Manager restore yordamı için hazırdır.

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>Desteklenen bir sürümü ve aynı SQL Server sürümünü kullanın

<!-- SCCMDocs#751 -->

Mümkünse, SQL Server aynı sürümünü kullanın. Ancak, bir veritabanının daha yeni bir sürüme geri yüklenmesi desteklenir.

SQL Server sürümünü değiştirmeyin. Bir site veritabanının Standard Edition 'dan Enterprise Edition 'a geri yüklenmesi desteklenmez.

Ek SQL Server yapılandırma gereksinimleri:

- SQL Server, **tek kullanıcılı moda**ayarlanamaz.
- MDF ve LDF dosyalarının geçerli olduğundan emin olun. Bir siteyi kurtardığınızda, dosyaların durumunu kontrol edebilirsiniz.  

### <a name="sql-server-always-on-availability-groups"></a>SQL Server Always On kullanılabilirlik grupları

Site veritabanını barındırmak için Always on kullanılabilirlik grupları SQL Server kullanıyorsanız, kurtarma planlarınızı [SQL Server kullanmaya hazırlanma](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery)bölümünde açıklandığı gibi değiştirin.

### <a name="database-replicas"></a>Veritabanı çoğaltmaları

Veritabanı çoğaltmaları için yapılandırdığınız bir site veritabanını geri yükledikten sonra, her bir çoğaltmayı yeniden yapılandırın. Veritabanı çoğaltmalarını kullanabilmeniz için, hem yayınları hem de abonelikleri yeniden oluşturun.

## <a name="determine-your-recovery-options"></a>Kurtarma seçeneklerinizi belirleme

Configuration Manager birincil site sunucusu ve merkezi yönetim sitesi (CAS) kurtarması için göz önünde bulundurmanız gereken iki ana alan vardır: **site sunucusu** ve **site veritabanı**.
Aşağıdaki bölümler, Kurtarma senaryonuz için en iyi seçenekleri seçmenize yardımcı olabilir.

> [!NOTE]  
> Configuration Manager Kurulum sunucuda var olan bir siteyi algıladığında, bir site kurtarması başlatabilirsiniz, ancak site sunucusunun kurtarma seçenekleri sınırlı olabilir. Örneğin, Kurulumu mevcut bir site sunucusunda çalıştırırsanız, kurtarmayı seçtiğinizde site veritabanı sunucusunu kurtarabilirsiniz, ancak site sunucusunu kurtarma seçeneği devre dışı bırakılır.

### <a name="site-server-recovery-options"></a>Site sunucusu kurtarma seçenekleri

Kurulum 'u CD 'nin bir kopyasından Configuration Manager başlatın **. **Configuration Manager yükleme klasörü dışında oluşturduğunuz en son klasör.  

- Site sunucusundaki **Başlangıç** menüsünden kurulum 'u çalıştırırsanız **Site kurtar** seçeneği kullanılamaz.  

- Yedeklemenizi yapmadan önce Configuration Manager konsolundan herhangi bir güncelleştirme yüklediyseniz, aşağıdaki konumlardan kurulumu kullanarak siteyi yeniden yükleyebilirsiniz:

  - Yükleme medyası
  - Configuration Manager yükleme yolu

Sonra **Site kurtar** seçeneğini belirleyin. Hatalı site sunucusu için aşağıdaki kurtarma seçeneklerine sahipsiniz:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Site sunucusunu mevcut bir yedekleme kullanarak kurtar

Site hatasından önce site sunucusunun Configuration Manager yedeğine sahip olduğunuzda bu seçeneği kullanın. Site, **Site Sunucusunu Yedekle** bakım görevinin bir parçası olarak bu yedeklemeyi oluşturur. Site yeniden yüklenir ve site ayarları yedeklenen siteye göre yapılandırılır.  

#### <a name="reinstall-the-site-server"></a>Site sunucusunu yeniden yükleme

Site sunucusunun bir yedeği olmadığında bu seçeneği kullanın. Site sunucusu yeniden yüklenir ve ilk yükleme sırasında yaptığınız gibi site ayarlarını belirtmeniz gerekir.  

- Hatalı site ilk kez yüklendiğinde kullandığınız site kodunu ve site veritabanı adını kullanın.  

- Siteyi yeni bir işletim sistemi sürümünü çalıştıran yeni bir bilgisayara yeniden yükleyebilirsiniz.  

- Sunucunun, özgün site sunucusunun ana bilgisayar adını ve tam etki alanı adını (FQDN) kullanması gerekir.

### <a name="site-database-recovery-options"></a>Site veritabanı kurtarma seçenekleri

Configuration Manager Kurulum 'u çalıştırdığınızda, site veritabanı için aşağıdaki kurtarma seçeneklerine sahip olursunuz:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Site veritabanını bir yedekleme kümesi kullanarak kurtarma

Veritabanı hatasından önce site veritabanının Configuration Manager yedeğine sahip olduğunuzda bu seçeneği kullanın. Site, **Site Sunucusunu Yedekle** bakım görevinin bir parçası olarak bu yedeklemeyi oluşturur. Bir hiyerarşide, birincil bir siteyi geri yüklerken kurtarma işlemi, son yedeklemeden sonra site veritabanında yapılan herhangi bir değişikliği CA 'dan alır. CAS geri yüklenirken, kurtarma işlemi bu değişiklikleri bir başvuru birincil sitesinden alır. Tek başına birincil sitenin site veritabanını kurtardığınızda, son yedeklemeden sonraki site değişikliklerini kaybedersiniz.  

Hiyerarşideki bir sitenin site veritabanını kurtardığınızda, bir CA ve birincil site için kurtarma davranışı farklıdır. Ayrıca, son yedekleme SQL Server değişiklik izleme tutma süresi içinde veya dışında olduğunda davranış da farklıdır. Daha fazla bilgi için bu makaledeki [site veritabanı kurtarma senaryoları](#site-database-recovery-scenarios) bölümüne bakın.  

> [!NOTE]  
> Site veritabanını bir yedekleme kümesi kullanarak geri yüklemeyi seçerseniz, ancak site veritabanı zaten varsa, kurtarma başarısız olur.  

#### <a name="create-a-new-database-for-this-site"></a>Bu site için yeni bir veritabanı oluştur

Site veritabanının yedeğine sahip olmadığınız durumlarda bu seçeneği kullanın. Bir hiyerarşide, kurtarma işlemi yeni bir site veritabanı oluşturur. Bir alt birincil siteyi geri yüklerken, CA 'lardan çoğaltılan verileri kurtarır. CAS geri yüklenirken, verileri bir başvuru birincil sitesinden çoğaltır. Tek başına birincil siteyi veya birincil siteleri olmayan bir CA 'ları kurtarırken Bu seçenek kullanılamaz.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>El ile kurtarılmış bir site veritabanı kullan

Configuration Manager site veritabanını zaten kurtardığınızda bu seçeneği kullanın, ancak kurtarma işlemini doldurmanız gerekir.  

- Configuration Manager, aşağıdaki işlemlerden herhangi birinden site veritabanını kurtarabilir:  

  - Configuration Manager yedekleme bakım görevi  
  - Data Protection Manager kullanarak bir site veritabanı yedeklemesi (DPM)  
  - Başka bir yedekleme işlemi  

    Configuration Manager dışında bir yöntem kullanarak site veritabanını geri yükledikten sonra, kurulum 'U çalıştırın ve site veritabanı kurtarmayı gerçekleştirmek için bu seçeneği belirleyin.  

    > [!NOTE]  
    > Site veritabanınızı yedeklemek için DPM kullandığınızda, Configuration Manager geri yükleme işlemine devam etmeden önce site veritabanını belirtilen bir konuma geri yüklemek için DPM yordamlarını kullanın. DPM hakkında daha fazla bilgi için [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) belge kitaplığı ' na bakın.  

- Bir hiyerarşide, birincil site veritabanını kurtardığınızda kurtarma işlemi, son yedeklemeden sonra site veritabanında yapılan herhangi bir değişikliği CA 'dan alır. CAS geri yüklenirken, kurtarma işlemi bu değişiklikleri bir başvuru birincil sitesinden alır. Tek başına birincil sitenin site veritabanını kurtardığınızda, son yedeklemeden sonraki site değişikliklerini kaybedersiniz.  

#### <a name="skip-database-recovery"></a>Veritabanı kurtarmayı atla

Configuration Manager site veritabanı sunucusunda bir veri kaybı oluşmadığında bu seçeneği kullanın. Bu seçenek yalnızca site veritabanı, kurtardığınız site sunucusundan farklı bir bilgisayarda olduğunda geçerlidir.  

### <a name="sql-server-change-tracking-retention-period"></a>SQL Server değişiklik izleme tutma süresi

Configuration Manager, SQL Server site veritabanı için değişiklik izleme imkanı sunar. Değişiklik izleme, zaman içinde önceki bir noktadan sonra veritabanı tablolarında yapılan değişiklikler hakkında bilgi için sorguya Configuration Manager olanak tanır. Saklama süresi, değişiklik izleme bilgilerinin ne kadar süreyle tutulacağını belirtir. Varsayılan olarak, site veritabanı beş günlük bir bekletme dönemine sahip olacak şekilde yapılandırılmıştır. Bir site veritabanını kurtardığınızda, yedeklemenin tutma süresi içinde veya dışında olmasına bağlı olarak kurtarma işlemi farklı şekilde devam eder. Örneğin, SQL sunucunuz başarısız olursa ve son yedeklemeniz yedi gün daha eski ise, bu, bekletme döneminin dışındadır.

SQL Server değişiklik izleme iç işlevleri hakkında daha fazla bilgi için, SQL Server ekibinin şu blog gönderilerine bakın: [değişiklik izleme temizleme-Bölüm 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) ve [değişiklik izleme temizleme-Bölüm 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Siteyi veya genel verileri yeniden başlatma

Siteyi veya genel verileri yeniden başlatma işlemi, site veritabanındaki mevcut verileri başka bir site veritabanından verilerle değiştirir. Örneğin, ABC sitesi XYZ sitesinden verileri yeniden başlattığında aşağıdaki adımlar oluşur:

- Veriler XYZ sitesinden ABC sitesine kopyalanır.
- XYZ sitesinin mevcut verileri ABC sitesindeki site veritabanından kaldırılır.
- XYZ sitesinden kopyalanan veriler, ABC sitesinin site veritabanına eklenir.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>Örnek Senaryo 1: birincil site, CAS 'den genel verileri yeniden başlatır

Kurtarma işlemi, birincil sitenin birincil site veritabanında mevcut olan genel verilerini kaldırır ve verileri CA 'lardan kopyalanmış Global verilerle değiştirir.

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>Örnek Senaryo 2: CAS site verilerini birincil siteden yeniden başlatır

Kurtarma işlemi, CAS veritabanında ilgili birincil sitenin mevcut site verilerini kaldırır. Birincil siteden kopyalanmış site verileriyle verileri değiştirir. Diğer birincil sitelerin site verileri etkilenmez.

### <a name="site-database-recovery-scenarios"></a>Site veritabanı kurtarma senaryoları

Bir site veritabanı yedeklemeden geri yüklendikten sonra, Configuration Manager son veritabanı yedeklemesinden sonra site ve genel verilerde yapılan değişiklikleri geri yüklemeye çalışır. Configuration Manager, bir site veritabanı yedekten geri yüklendikten sonra aşağıdaki eylemleri başlatır:  

#### <a name="recovered-site-is-a-cas"></a>Kurtarılan site bir CA

- Değişiklik izleme tutma süresi içinde veritabanı yedekleme  

  - **Genel veriler**: yedekleme sonrasında genel verilerde yapılan değişiklikler tüm birincil sitelerden çoğaltılır.  

  - **Site verileri**: yedekleme sonrasında site verilerinde yapılan değişiklikler tüm birincil sitelerden çoğaltılır.  

- Değişiklik izleme tutma süresi öncesinde veritabanı yedekleme  

  - **Genel veriler**: CA 'lar belirtirseniz, genel verileri referans birincil sitesinden yeniden başlatır. Daha sonra diğer tüm birincil siteler CA 'lardan genel verileri yeniden başlatın. Bir başvuru sitesi belirtmezseniz, tüm birincil siteler CA 'lardan genel verileri yeniden başlatın. Bu veriler, yedeklemeden geri yüklediğiniz şeydir.  

  - **Site verileri**: CAS her birincil sitenin site verilerini yeniden başlatır.  

#### <a name="recovered-site-is-a-primary-site"></a>Kurtarılan site bir birincil sitedir

- Değişiklik izleme tutma süresi içinde veritabanı yedekleme  

  - **Genel veriler**: yedekleme sonrasında genel verilerde YAPıLAN değişiklikler CA 'lardan çoğaltılır.  

  - **Site verileri**: CAS site verilerini birincil siteden yeniden başlatır. Yedekleme kaybedildikten sonra değişiklikler. İstemciler birincil siteye bilgi gönderdiklerinde verilerin çoğunu yeniden üretin.  

- Değişiklik izleme tutma süresi öncesinde veritabanı yedekleme  

  - **Genel veriler**: birincil SITE, CA 'lardan genel verileri yeniden başlatır.  

  - **Site verileri**: CAS site verilerini birincil siteden yeniden başlatır. Yedekleme kaybedildikten sonra değişiklikler. İstemciler birincil siteye bilgi gönderdiklerinde verilerin çoğunu yeniden üretin.  

## <a name="site-recovery-procedures"></a>Site kurtarma yordamları

Site sunucunuzu ve site veritabanınızı kurtarmanıza yardımcı olması için aşağıdaki yordamlardan birini kullanın:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Kurulum sihirbazında bir Site Recovery başlatma

1. [CD 'yi kopyalayın. ](the-cd.latest-folder.md)Configuration Manager yükleme klasörü dışında bir konuma en son klasör. CD 'nin kopyasıdır. En son klasör Configuration Manager Kurulum Sihirbazı 'nı çalıştırın.  

2. **Başlarken** sayfasında, **Site kurtar**' ı seçin ve ardından **İleri**' yi seçin.  

3. Site kurtarmanıza uygun seçenekleri kullanarak sihirbazı tamamlayın.  

     - Kurtarma sırasında kurulum, SQL Server tarafından kullanılan SQL Server Hizmet Aracısı (SSB) bağlantı noktasını tanımlar. Kurtarma işlemi sırasında bu bağlantı noktası ayarını değiştirmeyin veya veri çoğaltma, Kurtarma tamamlandıktan sonra düzgün çalışmaz.  

     - Kurulum sihirbazında Configuration Manager yüklemesi için kullanılacak özgün veya yeni bir yolu belirtebilirsiniz.  

### <a name="start-an-unattended-site-recovery"></a>Katılımsız site kurtarması başlatma

1. Katılımsız yükleme komut dosyasını site kurtarması için gereken seçenekler için hazırlayın. Daha fazla bilgi için bkz. [Katılımsız Site Recovery](unattended-recovery.md).  

2. Configuration Manager Kurulum 'u `/script` komut satırı seçeneğini kullanarak çalıştırın. Örneğin, **ConfigMgrUnattend. ini**Kurulum başlatma dosyası oluşturursunuz. Bu dosyayı, kurulumu çalıştırdığınız `C:\Temp` bilgisayarın dizinine kaydedersiniz. Aşağıdaki komutu kullanın:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> CA 'ları kurtardıktan sonra bazı site verilerinin alt sitelerden çoğaltılması başarısız olabilir. Bu veriler donanım envanteri, yazılım envanteri ve durum iletileri içerebilir.
>
> Bu sorun oluşursa, veritabanı çoğaltması için **ConfigMgrDRSSiteQueue** öğesini yeniden başlatın. CA 'LAR için site veritabanında aşağıdaki sorguyu çalıştırmak için **SQL Server Yöneticisi** 'ni kullanın:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>Kurtarma sonrası görevler

Sitenizi kurtardıktan sonra, Site Recovery 'nin tamamlanabilmesi için göz önünde bulundurmanız gereken birkaç kurtarma sonrası görev vardır. Site kurtarma işleminizi tamamlamanıza yardımcı olması için aşağıdaki bölümleri kullanın.

### <a name="reenter-user-account-passwords"></a>Kullanıcı hesabı parolalarını yeniden girin

Bir site sunucusu kurtarmasından sonra, sitedeki herhangi bir kullanıcı hesabının parolalarını yeniden girin. Bu parolalar, Site Recovery sırasında sıfırlanır. Hesaplar, Site Recovery tamamlandıktan sonra Kurulum sihirbazının **bitti** sayfasında listelenir. Liste ayrıca kurtarılan site sunucusuna da `C:\ConfigMgrPostRecoveryActions.html` kaydedilir.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Site kurtarmasından sonra Kullanıcı hesabı parolalarını yeniden girin

1. Configuration Manager konsolunu açın ve kurtarılan siteye bağlanın.  

2. **Yönetim** çalışma alanına gidin, **güvenlik**' i genişletin ve **hesaplar**' ı seçin.  

3. Her hesap için, parolayı yeniden girmek üzere aşağıdaki adımları uygulayın:  

     1. Site kurtarma işleminden sonra tanımlanan listeden hesabı seçin.  

     2. Şeritte **Özellikler** ' i seçin.  

     3. **Genel** sekmesinde **Ayarla**' yı seçin ve ardından hesabın parolasını yeniden girin.  

     4. **Doğrula**' yı seçin, seçili kullanıcı hesabı için uygun veri kaynağını seçin ve ardından **Bağlantıyı Sına**' yı seçin. Bu adım kullanıcı hesabının veri kaynağına bağlanabildiğini sınar ve kimlik bilgilerini doğrular.  

     5. **Tamam** ' ı seçerek parola değişikliklerini kaydedin ve ardından **Tamam** ' ı seçerek hesap özellikleri sayfasını kapatın.  

#### <a name="reenter-pxe-passwords"></a>PXE parolalarını yeniden girin

<!-- SCCMDocs#1683 -->

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **dağıtım noktaları** düğümünü seçin. **PXE** sütununda **Evet** olan tüm ŞIRKET içi dağıtım noktaları PXE için etkinleştirilmiştir ve yeniden girmek için bir parolaya sahip olabilir.

1. PXE 'yi destekleyen bir dağıtım noktası seçin ve şeritte **Özellikler** ' i seçin.

1. **PXE** sekmesine geçin.

1. **BILGISAYARLAR PXE kullanırken parola gerektirme** seçeneği etkinken parolayı girin ve onaylayın.

1. Özellikleri kaydetmek ve kapatmak için **Tamam ' ı** seçin.

PXE 'yi destekleyen diğer tüm şirket içi dağıtım noktaları için bu işlemi tekrarlayın.

#### <a name="reenter-task-sequence-passwords"></a>Görev sırası parolalarını yeniden girin

<!-- SCCMDocs#1683 -->

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin.

1. Bir görev dizisi seçin ve ardından şeritte **Düzenle**' yi seçin.

1. Parolaların yeniden girmesi için aşağıdaki adımları gözden geçirin:

    - **Windows ayarlarını uygula**: yerel yönetici parolasını etkinleştirip belirtirseniz, parolayı yeniden girin ve onaylayın.

    - **Ağ ayarlarını uygula**: etki alanına ekleme izni olan hesap için **Ayarla**' yı seçin. Parolayı girip onaylayın ve **Doğrula**' yı seçin.

    - **Işletim sistemi görüntüsünü yakala**: hedefe erişmek için kullanılan hesap için **Ayarla**' yı seçin. Parolayı girip onaylayın ve **Doğrula**' yı seçin.

    - **Ağ klasörüne Bağlan**: bir ağ klasörünü bağlamak için kullanılan hesap için **Ayarla**' yı seçin. Parolayı girip onaylayın ve **Doğrula**' yı seçin.

    - **BitLocker 'ı etkinleştir**: anahtar yönetim seçeneğini **TPM ve PIN**olarak kullanırsanız, PIN 'i yeniden girin.

    - **Etki alanına veya çalışma grubuna katıl**: etki alanına katılma izni olan hesap için **Ayarla**' yı seçin. Parolayı girip onaylayın ve **Doğrula**' yı seçin.

    - **Komut satırını Çalıştır**: **Bu adımı aşağıdaki hesap olarak çalıştırmak**Için seçeneğini kullanırsanız, **Ayarla**' yı seçin. Parolayı girip onaylayın ve **Doğrula**' yı seçin.

    - **PowerShell betiğini Çalıştır**: **Bu adımı aşağıdaki hesap olarak çalıştırmak**Için seçeneğini kullanırsanız, **Ayarla**' yı seçin. Parolayı girip onaylayın ve **Doğrula**' yı seçin.

Tüm görev dizileri için bu işlemi tekrarlayın.

### <a name="reenter-sideloading-keys"></a>Dışarıdan yükleme anahtarlarını yeniden girin

Bir site sunucusu kurtarmasından sonra, site için belirtilen Windows dışarıdan yükleme anahtarlarını yeniden girin. Bu anahtarlar Site Recovery sırasında sıfırlanır. Dışarıdan yükleme anahtarlarını yeniden girdikten sonra, site Windows dışarıdan yükleme anahtarları için **kullanılan etkinleştirmeler** sütunundaki sayıyı sıfırlar.

Örneğin, site hatası **Toplam etkinleştirme** sayısı **100**olarak gösterilmiştir. Cihazların kullandığı anahtarların sayısı veya **kullanılan etkinleştirmeler** **90**' dir. Site kurtarma işleminden sonra, **Toplam etkinleştirmeler** değeri hala **100**' i görüntülüyor, ancak **kullanılan etkinleştirmeler** sütunu yanlış bir şekilde **0**görüntülüyor. 10 yeni cihaz dışarıdan yükleme anahtarı kullandıktan sonra, başka dışarıdan yükleme anahtarı yoktur ve 11. cihaz bir dışarıdan yükleme anahtarı uygulayamaz.

### <a name="recreate-azure-services"></a>Azure hizmetlerini yeniden oluşturma

<!-- SCCMDocs#1022 -->

Configuration Manager sürüm 1806 ' de, Site kurtarmasından sonra CloudMgr. log dosyasında şu hatayı görürsünüz:

`Index (zero-based) must be greater than or equal to zero`

Bu sorunu çözmek için, her bir Azure kiracı bağlantısı için [gizli anahtarı yenileyin](../deploy/configure/azure-services-wizard.md#bkmk_renew) .

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>IIS Kullanan site sistem rolleri için SSL yapılandırma

IIS çalıştıran ve HTTPS için yapılandırdığınız site sistemlerini kurtardığınızda, IIS 'yi Web sunucusu sertifikasını kullanacak şekilde yeniden yapılandırın.

### <a name="reinstall-hotfixes"></a>Düzeltmeleri yeniden yükle

Site kurtarmasından sonra, site sunucusuna uygulanan tüm [bant dışı düzeltmeleri](updates.md#bkmk_outofband) yeniden yüklemeniz gerekir. Site kurtarmasından sonra, Kurulum sihirbazının **bitti** sayfasında, daha önce yüklenmiş düzeltmelerin listesini görüntüleyin. Bu liste, kurtarılan site sunucusuna `C:\ConfigMgrPostRecoveryActions.html` da kaydedilir.

### <a name="recover-custom-reports"></a>Özel raporları kurtarma

Bazı müşteriler SQL Server Reporting Services özel raporlar oluşturur. Bu bileşen başarısız olduğunda, raporları rapor sunucusunun bir yedeklemesinden kurtarın. Raporlama hizmetlerinde özel raporlarınızı geri yükleme hakkında daha fazla bilgi için bkz. [Reporting Services Için Yedekleme ve geri yükleme işlemleri](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### <a name="recover-content-files"></a>İçerik dosyalarını geri yükleme

Site veritabanı, site sunucusunun içerik dosyalarını nerede depoladığını izler. İçerik dosyaları yedekleme ve kurtarma sürecinin bir parçası olarak yedeklenmez veya geri yüklenmez. İçerik dosyalarını tamamen kurtarmak için, içerik kitaplığı ve paket kaynak dosyalarını özgün konuma geri yükleyin. İçerik dosyalarınızı kurtarmaya yönelik çeşitli yöntemler vardır. En kolay yöntem, dosyaları site sunucusunun bir dosya sistemi yedeğinden geri yüklemektir.

Paket kaynak dosyaları için bir dosya sistemi yedeğiniz yoksa, bunları el ile kopyalayın veya indirin. Bu işlem, paketi ilk oluşturduğunuzda ile benzerdir. Tüm paketler ve uygulamalar için paket kaynağı konumunu bulmak üzere SQL Server aşağıdaki sorguyu çalıştırın: `SELECT * FROM v_Package`. Paket KIMLIĞININ ilk üç karakterine bakarak paket kaynak sitesini belirler. Örneğin, paket kimliği CEN00001 ise kaynak sitenin site kodu CEN’dir. Paket kaynak dosyalarını geri yüklediğinizde bunlar arızadan önce bulundukları konuma geri yüklenmelidir.

İçerik kitaplığını içeren bir dosya sistemi yedeğiniz yoksa, aşağıdaki geri yükleme seçenekleriniz vardır:  

- **Önceden hazırlanan içerik dosyasını Içeri aktar**: bir Configuration Manager hiyerarşisinde, başka bir konumdan tüm paket ve uygulamalarla önceden hazırlanan bir içerik dosyası oluşturabilirsiniz. Daha sonra, site sunucusundaki içerik kitaplığını kurtarmak için önceden hazırlanan içerik dosyasını içeri aktarın.  

- **Içeriği Güncelleştir**: Configuration Manager içeriği paket kaynağından içerik kitaplığına kopyalar. Bu eylemin başarıyla tamamlanabilmesi için, paket kaynak dosyalarının özgün konumda bulunması gerekir. Bu eylemi her paket ve uygulama üzerinde yapın.

### <a name="recover-custom-software-updates"></a>Özel yazılım güncelleştirmelerini kurtarma

System Center Updates Publisher veritabanı dosyalarını yedekleme planınıza dahil ettiğinizde, Updates Publisher bilgisayarı başarısız olursa veritabanlarını kurtarabilirsiniz. Updates Publisher hakkında daha fazla bilgi için bkz. [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

#### <a name="restore-the-updates-publisher-database"></a>Updates Publisher veritabanını geri yükleme

1. Updates Publisher 'ı kurtarılan bilgisayara yeniden yükleyin.  

2. **Scupdb. sdf** veritabanı dosyasını yedekleme hedefinizden `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` , Updates Publisher 'ı çalıştıran bilgisayara kopyalayın.  

3. Bilgisayar üzerinde Updates Publisher 'ı birden fazla Kullanıcı çalıştırıyorsa, her veritabanı dosyasını ilgili Kullanıcı profili konumuna kopyalayın.  

### <a name="user-state-migration-data"></a>Kullanıcı durumu taşıma verileri

Durum geçiş noktası özellikleri kapsamında, Kullanıcı durumu verilerini depolayan klasörleri belirtirsiniz. Bir durum geçiş noktasını kurtardıktan sonra, sunucuda Kullanıcı durumu verilerini el ile geri yükleyin. Hatadan önce verileri depoladığınız klasörlere geri yükleyin.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Dağıtım noktaları için sertifikaları yeniden oluşturma

Bir siteyi geri yükledikten sonra, **Distmgr. log** bir veya daha fazla dağıtım noktası için şu girdiyi listeleyebilir: `Failed to decrypt cert PFX data`. Bu giriş, dağıtım noktası sertifika verilerinin, site tarafından çözülemediğini belirtir. Bu sorunu çözmek için sertifikayı etkilenen dağıtım noktaları için yeniden oluşturun veya yeniden içeri aktarın. [Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) PowerShell cmdlet 'ini kullanın.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Bulut tabanlı dağıtım noktaları için kullanılan sertifikaları güncelleştirme

Configuration Manager, site sunucusunun bulut tabanlı dağıtım noktalarıyla iletişim kurması için bir Azure Yönetim sertifikası gerektirir. Site kurtarmasından sonra, bulut tabanlı dağıtım noktaları için sertifikaları güncelleştirin.

## <a name="recover-a-secondary-site"></a>Bir ikincil siteyi kurtarma

Configuration Manager, veritabanının yedeğini ikincil bir sitede desteklemez, ancak ikincil siteyi yeniden yükleyerek kurtarmayı destekler. İkincil site kurtarma, Configuration Manager bir ikincil site başarısız olduğunda gereklidir.

### <a name="requirements"></a>Gereksinimler

- Sunucunun tüm ikincil site önkoşullarını karşılaması ve uygun güvenlik haklarının yapılandırılmış olması gerekir.  

- Başarısız olan site için kullanılan yükleme yolunu kullanın.  

- Hatalı sunucuyla aynı yapılandırmaya sahip bir sunucu kullanın. Bu yapılandırma, tam etki alanı adını (FQDN) içerir.  

- Sunucu, başarısız olan siteyle aynı SQL Server yapılandırmasına sahip olmalıdır.  

  - İkincil site kurtarma sırasında, Configuration Manager bilgisayarda zaten yüklü değilse SQL Server Express yüklemez.  

  - Hatadan önce ikincil site veritabanı için kullandığınız SQL Server aynı sürümünü ve aynı SQL Server örneğini kullanın.  

### <a name="procedure"></a>Yordam

Configuration Manager konsolundaki **siteler** düğümünden **ikincil site kurtar** eylemini kullanın. Diğer site türlerinden farklı olarak, ikincil bir siteye yönelik kurtarma bir yedekleme dosyası kullanmaz. Bu işlem, ikincil site dosyalarını başarısız sunucuya yeniden yükler. Site yeniden yüklendikten sonra, ikincil site verileri üst birincil siteden yeniden başlatılır.

Kurtarma işlemi sırasında, içerik kitaplığının ikincil site sunucusunda mevcut olup olmadığını doğrular Configuration Manager. Ayrıca uygun içeriğin kullanılabilir olup olmadığını denetler. İkincil site, uygun içeriği içeriyorsa, var olan içerik kitaplığını kullanır. Aksi takdirde, ikincil bir sitenin içerik kitaplığını kurtarmak için, içeriği sunucuya yeniden dağıtır veya önceden hazırlayabilirsiniz.

İkincil site sunucusunda olmayan bir dağıtım noktanız varsa, İkincil sitenin kurtarılması sırasında dağıtım noktasını yeniden yüklemeniz gerekmez. İkincil site kurtarma işleminden sonra, site dağıtım noktasıyla otomatik olarak eşitleme yapar.

Configuration Manager konsolundaki **siteler** düğümünden, **yüklemeyi durumunu göster** eylemini kullanarak ikincil site kurtarma durumunu doğrulayabilirsiniz.
