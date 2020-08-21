---
title: Yedekleme siteleri
titleSuffix: Configuration Manager
description: Configuration Manager hata veya veri kaybı olmadan önce sitelerinizi yedeklemeyi öğrenin.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8d766a172f934e27398ec2633ef0ec23ba4ade5e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700693"
---
# <a name="back-up-a-configuration-manager-site"></a>Bir Configuration Manager sitesinin yedeğini alma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Veri kaybını önlemek için yedekleme ve kurtarma yaklaşımları hazırlayın. Configuration Manager siteler için, bir yedekleme ve kurtarma yaklaşımı siteleri ve hiyerarşileri daha hızlı ve en az veri kaybıyla kurtarmanıza yardımcı olabilir.  

Bu makaledeki bölümler, sitelerinizi yedeklemelerinizde size yardımcı olabilir. Bir siteyi kurtarmak için bkz. [kurtarma Configuration Manager](recover-sites.md).  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> Configuration Manager Site Recovery için desteklenen iki yedekleme yöntemi şunlardır:
>
> - **Site Sunucusunu Yedekle** bakım görevinin başarılı bir yedeklemesi
> - El ile kurtarılan bir site veritabanı yedeklemesi


## <a name="considerations-before-creating-a-backup"></a>Yedekleme oluşturmadan önce dikkat edilecek noktalar  

-   Site veritabanını barındırmak için SQL Server Always on kullanılabilirlik grubu kullanıyorsanız: yedekleme ve kurtarma planlarınızı [her zaman açık SQL Server kullanmaya hazırlanma](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)bölümünde açıklandığı gibi değiştirin.  

-   Configuration Manager, Configuration Manager yedekleme görevinden site veritabanını kurtarabilir. Ayrıca, başka bir işlemle oluşturduğunuz site veritabanının bir yedeklemesini de kullanabilir.   

     Örneğin, site veritabanını bir Microsoft SQL Server bakım planının parçası olarak oluşturulan bir yedekten geri yükleyebilirsiniz. Site veritabanınızı yedeklemek için Data Protection Manager kullanılarak oluşturulan bir yedeklemeyi de kullanabilirsiniz.  

-   Sürüm 1806 ' den başlayarak, *Pasif* modda ek bir site sunucusu yükler. Pasif modda site sunucusu, mevcut site sunucunuza *etkin* modda ek olarak bulunur. Pasif moddaki bir site sunucusu, gerektiğinde hemen kullanılmak üzere kullanılabilir. Daha fazla bilgi için bkz. [site sunucusu yüksek kullanılabilirlik](../deploy/configure/site-server-high-availability.md). Bu rol, yedekleme ve kurtarma işlemlerini planlamaya ve uygulamaya yönelik gerekli işlemleri kaldırmadığı sürece, gerektiğinde bir siteyi kurtarmaya yönelik çabaları önemli ölçüde azaltır.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Site veritabanınızın yedeğini almak için Data Protection Manager'ı kullanma
Configuration Manager site veritabanınızı yedeklemek için System Center Data Protection Manager (DPM) kullanabilirsiniz.

Site veritabanı bilgisayarı için DPM 'de yeni bir koruma grubu oluşturun. Oluştur Yeni Koruma Grubu Sihirbazı **Grup üyelerini seçin** sayfasında, veri kaynağı listesinden SMS Yazıcı hizmetini seçersiniz. Ardından, uygun bir üye olarak site veritabanını seçin. DPM kullanma hakkında daha fazla bilgi için [Data Protection Manager](/system-center/dpm) belge kitaplığı ' na bakın.  

> [!IMPORTANT]  
>  Configuration Manager, adlandırılmış bir örnek kullanan bir SQL Server kümesi için DPM yedeklemesini desteklemez. Varsayılan SQL Server örneğini kullanan bir SQL Server kümesinde DPM yedeklemesini destekler.  

Site veritabanını geri yükledikten sonra, siteyi kurtarmak için kurulum 'daki adımları izleyin. Data Protection Manager ile yedeklediğiniz site veritabanını kullanmak için, **el ile kurtarılmış bir site veritabanını kullanmak**üzere kurtarma seçeneğini belirleyin.  



## <a name="backup-maintenance-task"></a>Yedek bakım görevi
Önceden tanımlı Site Sunucusunu Yedekle bakım görevini zamanlayarak Configuration Manager siteleri için yedeklemeyi otomatik hale getirebilirsiniz. Bu görev aşağıdaki özelliklere sahiptir:

-   Bir zamanlamaya göre çalışan
-   Site veritabanını yedekleyen
-   Belirli kayıt defteri anahtarlarını yedekleyen
-   Belirli klasörleri ve dosyaları yedekleyen
-   [CD 'yi yedekler. En son klasör](the-cd.latest-folder.md)   

Varsayılan site yedekleme görevini en az beş günde bir çalıştırmayı planlayın. Bu zamanlama, Configuration Manager beş güne ait bir *SQL Server değişiklik izleme saklama süresi* kullandığından kaynaklanır. Daha fazla bilgi için bkz. [değişiklik izleme saklama süresi SQL Server](recover-sites.md#sql-server-change-tracking-retention-period).

Yedekleme işlemini basitleştirmek için bir **AfterBackup.bat** dosyası oluşturabilirsiniz. Bu betik yedekleme görevi başarıyla tamamlandıktan sonra yedekleme sonrası eylemleri otomatik olarak çalıştırır. Yedekleme anlık görüntüsünü güvenli bir konuma arşivlemek için AfterBackup.bat dosyasını kullanın. Dosyaları yedekleme klasörünüze kopyalamak veya diğer yedekleme görevlerini başlatmak için AfterBackup.bat dosyasını da kullanabilirsiniz.  

Bir merkezi yönetim sitesini ve birincil siteyi yedekleyebilirsiniz. İkincil siteler veya site sistem sunucuları yedekleme görevlerine sahip değildir.

Configuration Manager yedekleme hizmeti çalıştığında, yedekleme denetim dosyasında tanımlanan talimatları izler: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl` . Yedekleme hizmetinin davranışını değiştirmek için yedekleme kontrol dosyasını değiştirebilirsiniz.  
> [!NOTE]
> **Smsdk. ctl** ' nin değişiklikleri, SITE sunucusundaki bir hizmetin yeniden başlatıldıktan sonra uygulanacak SMS_SITE_VSS_WRITER.

Site yedekleme durum bilgileri **Smsbkup.log** dosyasına yazılır. Bu dosya, Site Sunucusunu Yedekle bakım görevinin özelliklerinde belirttiğiniz hedef klasörde oluşturulur.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Site yedekleme bakım görevini etkinleştirmek için  
1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2.  Site yedekleme bakım görevini etkinleştirmek istediğiniz siteyi seçin.  

3.  Şeritteki **site bakım görevleri** ' ne tıklayın.  

4.  **Site Sunucusunu Yedekle** görevini seçin ve **Düzenle**' ye tıklayın.  

5.  **Bu görevi etkinleştirme**seçeneğini belirleyin. Yedekleme hedefini belirtmek için **yolları ayarla** ' ya tıklayın. Aşağıdaki seçenekler mevcuttur:  

    > [!IMPORTANT]  
    >  Yedekleme dosyalarında değişiklik yapılmasını önlemeye yardımcı olmak için dosyaları güvenli bir yerde saklayın. En güvenli yedekleme yolu yerel bir sürücüdür, bu sayede klasörde NTFS dosya izinleri ayarlayabilirsiniz. Configuration Manager, yedekleme yolunda saklanan yedekleme verilerini şifrelemez.  

    -   Site **verileri ve veritabanı için site sunucusundaki yerel sürücü**: görevin, site sunucusunun yerel disk sürücüsünde belirtilen yoldaki site ve site veritabanı için yedekleme dosyalarını depolayıp depoladığını belirtir. Yedekleme görevinin çalışması için önce yerel klasörü oluşturun. Site sunucusundaki yerel sistem hesabının, site sunucusu yedeklemesi için yerel klasörde **yazma** NTFS dosya izinlerine sahip olması gerekir. SQL Server çalıştıran bilgisayardaki yerel sistem hesabı, site veritabanı yedeklemesinin klasörü için **yazma** NTFS izinlerine sahip olmalıdır.  

    -   **Site verileri ve veritabanı Için ağ yolu (UNC adı)**: görevin, belirtilen ağ yolundaki site ve site veritabanı için yedekleme dosyalarını depolayıp depoladığını belirtir. Yedekleme görevinin çalışması için önce paylaşma oluşturun. Site sunucusunun bilgisayar hesabı, paylaşılan ağ klasörü için **yazma** NTFS ve paylaşım izinlerine sahip olmalıdır. SQL Server başka bir bilgisayarda yüklüyse, SQL Server bilgisayar hesabı aynı izinlere sahip olmalıdır.  

    -   **Site sunucusundaki yerel sürücüler ve SQL Server**: görevin, site sunucusunun yerel sürücüsündeki belirtilen yoldaki sitenin yedekleme dosyalarını depoladığını belirtir. Görev, site veritabanı sunucusunun yerel sürücüsündeki belirtilen yoldaki site veritabanının yedekleme dosyalarını depolar. Yedekleme görevi çalışmadan önce yerel klasörleri oluşturun. Site sunucusunun bilgisayar hesabı, site sunucusunda oluşturduğunuz klasörde **Yazma** NTFS izinlerine sahip olmalıdır. SQL Server'ın bilgisayar hesabı, site veritabanı sunucusunda oluşturduğunuz klasörde **Yazma** NTFS izinlerine sahip olmalıdır. Bu seçenek yalnızca site veritabanı site sunucusunda yüklü olmadığında kullanılabilir.  

    > [!NOTE]  
    > Yedekleme hedefine gözatmaya yönelik seçenek yalnızca yedekleme hedefinin ağ yolunu belirttiğinizde kullanılabilir.  
    >  
    > Yedekleme hedefi için kullanılan klasör adı veya paylaşma adı, Unicode karakterlerin kullanılmasını desteklemez.  

6.  Site yedekleme görevi için bir zamanlama yapılandırın. Etkin çalışma saatlerinin dışında bir yedekleme zamanlaması düşünün. Bir hiyerarşiniz varsa, haftada en az iki kez çalışan bir zamanlama düşünün. Site başarısız olursa, bu zamanlama maksimum veri bekletmesini sağlar.  

    Yedekleme için yapılandırdığınız aynı site sunucusunda Configuration Manager konsolunu çalıştırdığınızda, yedekleme görevi zamanlama için yerel saati kullanır. Başka bir bilgisayardan Configuration Manager konsolunu çalıştırdığınızda, yedekleme görevi zamanlama için Eşgüdümlü Evrensel Saat (UTC) kullanır.  

7.  Site yedekleme görevi başarısız olursa bir uyarı oluşturulup oluşturulmayacağını seçin. Seçildiğinde, Configuration Manager yedekleme hatası için kritik bir uyarı oluşturur. Bu uyarıları **izleme** çalışma alanının **Uyarılar** düğümünde gözden geçirebilirsiniz.  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Site Sunucusunu Yedekle bakım görevinin çalıştığını doğrulama  

-   Görevin oluşturduğu yedekleme hedef klasöründeki dosyalardaki zaman damgasını denetleyin. Zaman damgasının, görevin çalıştırılmak üzere en son zamanlandığı zaman için güncelleşdiğini doğrulayın.  

-   **İzleme** çalışma alanının **Bileşen durumu** düğümüne gidin. **SMS_SITE_BACKUP**için durum iletilerini gözden geçirin. Site yedeklemesi başarıyla tamamlandığında, **5035**ileti kimliğini görürsünüz. Bu ileti, site yedeklemesinin herhangi bir hata olmadan tamamlandığını gösterir.  

-   Yedekleme görevini başarısız olduğunda bir uyarı oluşturacak şekilde yapılandırdığınızda, **izleme** çalışma alanının **Uyarılar** düğümünde yedekleme hatası uyarıları ' nı arayın.  

-   Site sunucusunda Windows Gezgini ' ni açın ve konumuna gidin `<ConfigMgrInstallationFolder>\Logs` . Uyarılar ve hatalar için **Smsdk. log dosyasına** bakın. Site yedeklemesi başarıyla tamamlandığında, günlük `Backup completed` ILETI kimliği ile gösterilir `STATMSG: ID=5035` .  

    > [!TIP]  
    >  Yedekleme bakım görevi başarısız olduğunda, **SMS_SITE_BACKUP** Windows hizmetini durdurup yeniden başlatarak yedekleme görevini yeniden başlatın.  



## <a name="archive-the-backup-snapshot"></a>Yedekleme anlık görüntüsünü Arşivle  
Yedekleme görevi, ilk çalıştırıldığında bir yedek anlık görüntüsü oluşturur. Bu anlık görüntüyü, başarısız olursa site sunucunuzu kurtarmak için kullanabilirsiniz. Yedekleme görevi zamanlamaya göre yeniden çalıştığında, önceki anlık görüntünün üzerine yazılan yeni bir yedek anlık görüntüsü oluşturur. Sonuç olarak, site yalnızca tek bir yedek anlık görüntüsüne sahiptir ve önceki bir yedek anlık görüntüsünü alma yönteminiz yoktur.  

Aşağıdaki nedenlerle yedekleme anlık görüntüsünün birden çok arşivini saklayın:  

-   Yedekleme medyasının başarısız olması, yanlış yerleştirilmesi veya yalnızca kısmi bir yedekleme içermesi yaygındır. Başarısız bir bağımsız birincil sitenin daha eski bir yedeklemeden kurtarılması, herhangi bir yedekleme olmadan kurtarmadan daha iyidir. Bir hiyerarşideki site sunucusu için, yedekleme SQL Server değişiklik izleme tutma süresinde olmalıdır veya yedekleme gerekli değildir.  

-   Sitedeki bir bozukluk birkaç yedekleme döngüsü boyunca algılanmayabilir. Sitenin bozulması için ' den bir yedek anlık görüntüsü kullanmanız gerekebilir. Bu nedenle, tek başına birincil site ve yedeklemenin SQL Server değişiklik izleme tutma süresinde olduğu bir hiyerarşideki siteler için geçerlidir.  

-   Sitede hiç yedekleme anlık görüntüsü olmayabilir. Örneğin, Site Sunucusunu Yedekle bakım görevi başarısız olursa. Yedekleme görevi, geçerli verileri yedeklemeye başlamadan önce önceki yedekleme anlık görüntüsünü kaldırdığı için geçerli bir yedekleme anlık görüntüsü olmayacaktır.  



## <a name="using-the-afterbackupbat-file"></a>AfterBackup.bat dosyasını kullanma  
Siteyi başarıyla yedekledikten sonra, yedekleme görevi otomatik olarak **AfterBackup.bat**adlı bir betiği çalıştırmayı dener. İçindeki site sunucusunda AfterBackup.bat dosyasını el ile oluşturun `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box` . Doğru klasörde bir AfterBackup.bat dosyası varsa, yedekleme görevi tamamlandıktan sonra otomatik olarak çalışır.

AfterBackup.bat dosyası her yedekleme işleminin sonunda yedekleme anlık görüntüsünü arşivlemenize imkan tanır. Site Sunucusunu Yedekle bakım görevinin parçası olmayan diğer yedekleme sonrası görevleri otomatik olarak gerçekleştirebilir. AfterBackup.bat dosyası arşive ve yedekleme işlemlerini bütünleştirir, böylece her yeni yedekleme anlık görüntüsünün arşivlenmesini sağlar.

AfterBackup.bat dosyası yoksa yedekleme görevi, yedekleme işlemini etkilemeden onu atlar. Yedekleme görevinin bu betiği başarıyla çalıştırdığını doğrulamak için **izleme** çalışma alanındaki **Bileşen durumu** düğümüne gidin ve **SMS_SITE_BACKUP**durum iletilerini gözden geçirin. Görev AfterBackup.bat komut dosyasını başarıyla başlattığında, ileti KIMLIĞI **5040**' i görürsünüz.  

> [!TIP]  
>  Site sunucusu yedekleme dosyalarınızı AfterBackup.bat arşivlemek için Batch dosyasında bir kopyalama komut aracını kullanmanız gerekir. Bu tür bir araç Windows Server 'da [Robocopy](/windows-server/administration/windows-commands/robocopy) 'dir. Örneğin, aşağıdaki komutla AfterBackup.bat dosyasını oluşturun: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

AfterBackup.bat kullanım amacı yedekleme anlık görüntülerini arşivlemek olsa da, her yedekleme işleminin sonunda ek görevleri çalıştırmak için bir AfterBackup.bat dosyası oluşturabilirsiniz.  



##  <a name="supplemental-backup-tasks"></a>Ek yedekleme görevleri  
Site Sunucusunu Yedekle bakım görevi, site sunucusu dosyaları ve site veritabanı için bir yedekleme anlık görüntüsü sağlar. Yedekleme stratejinizi oluştururken göz önünde bulundurmanız gereken başka öğeler de vardır. Configuration Manager yedekleme stratejinizi tamamlamanıza yardımcı olması için bu bölümleri kullanın.  

### <a name="back-up-custom-reports"></a>Özel raporları yedekleme   
SQL Server Reporting Services önceden tanımlı veya oluşturulmuş özel raporları değiştirirseniz, rapor sunucusu veritabanı dosyaları için bir yedek oluşturun. Rapor sunucusu yedeklemesi aşağıdaki bileşenleri içermelidir:
- Raporlar ve modeller için kaynak dosyaları
- Şifreleme anahtarları
- Özel derlemeler veya uzantılar
- Yapılandırma dosyaları
- Özel raporlarda kullanılan özel SQL Server görünümleri
- Özel saklı yordamlar  

> [!IMPORTANT]  
>  Configuration Manager daha yeni bir sürüme güncelleştirdiğinde, önceden tanımlanmış raporların üzerine yeni raporlar yazılabilir. Önceden tanımlı bir raporu değiştirirseniz, raporu yedeklediğinizden emin olun ve ardından Raporlama Hizmetleri 'ne geri yükleyin.  

Raporlama hizmetlerinde özel raporlarınızı yedekleme hakkında daha fazla bilgi için bkz. [Reporting Services Için Yedekleme ve geri yükleme işlemleri](/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>İçerik dosyalarını yedekleme  
Configuration Manager içerik kitaplığı tüm yazılım dağıtımları için tüm içerik dosyalarının depolandığı yerdir. İçerik Kitaplığı site sunucusunda ve her dağıtım noktasında bulunur. Site Sunucusunu Yedekle bakım görevi, içerik kitaplığı veya paket kaynak dosyalarını yedeketmez. Bir site sunucusu başarısız olduğunda, içerik kitaplığıyla ilgili bilgiler site veritabanına geri yüklenir, ancak içerik kitaplığı ve paket kaynak dosyalarını geri yüklemeniz gerekir.  

-   İçeriği dağıtım noktalarına yeniden dağıtabilmeniz için içerik kitaplığı geri yüklenmelidir. İçerik yeniden dağıtımı başlattığınızda, Configuration Manager dosyaları site sunucusunun içerik kitaplığından dağıtım noktalarına kopyalar. Daha fazla bilgi için bkz. [içerik kitaplığı](../../plan-design/hierarchy/the-content-library.md).  

-   Dağıtım noktalarındaki içeriği güncelleştirebilmeniz için önce paket kaynak dosyaları geri yüklenmelidir. Bir içerik güncelleştirmesini başlattığınızda, yeni veya değiştirilmiş dosyaları paket kaynağından içerik kitaplığına kopyalar Configuration Manager. Ardından dosyaları ilişkili dağıtım noktalarına kopyalar. Tüm paketler ve uygulamalar için paket kaynağı konumunu bulmak üzere site veritabanında aşağıdaki SQL Server sorguyu çalıştırın: `SELECT * FROM v_Package` . Paket kimliğinin ilk üç karakterine bakarak paket kaynak sitesini tanımlayabilirsiniz. Örneğin, paket kimliği CEN00001 ise kaynak sitenin site kodu CEN’dir. Paket kaynak dosyalarını geri yüklediğinizde, bunlar hatadan önce oldukları konuma geri yüklenmelidir.  

Site sunucusu için dosya sistemi yedeğine hem içerik kitaplığını hem de paket kaynak dosyalarını dahil ettiğini doğrulayın.  

### <a name="back-up-custom-software-updates"></a>Özel yazılım güncelleştirmelerini yedekleme  
System Center Updates Publisher, özel yazılım güncelleştirmelerini yönetmenize olanak tanıyan tek başına bir araçtır. Updates Publisher, yazılım güncelleştirme deposu için yerel bir veritabanı kullanır. Özel yazılım güncelleştirmelerini yönetmek için Updates Publisher 'ı kullandığınızda, yedekleme planınıza Updates Publisher veritabanını dahil etmeniz gerekip gerekmediğini saptayın. Daha fazla bilgi için bkz. [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).  

Updates Publisher veritabanını yedeklemek için aşağıdaki yordamı kullanın.  

#### <a name="back-up-the-updates-publisher-database"></a>Updates Publisher veritabanını yedekleme  

1.  Updates Publisher çalıştıran bilgisayarda, içindeki **Scupdb. sdf** Updates Publisher veritabanı dosyasına gidin `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` . Updates Publisher çalıştıran her kullanıcı için farklı bir veritabanı dosyası vardır.  

2.  Veritabanı dosyasını yedekleme hedefinize kopyalayın. Örneğin, yedekleme hedefinizin olması halinde, `E:\ConfigMgr_Backup` Updates Publisher veritabanı dosyasını uygulamasına kopyalayabilirsiniz `E:\ConfigMgr_Backup\SCUP` .  

    > [!TIP]  
    >  Bir bilgisayarda birden çok veritabanı dosyası olduğunda, dosyayı veritabanı dosyasıyla ilişkili kullanıcı profilini gösteren bir alt klasöre depolamayı düşünün. Örneğin, içinde bir veritabanı dosyanız `E:\ConfigMgr_Backup\SCUP\User1` ve içindeki başka bir veritabanı dosyası olabilir `E:\ConfigMgr_Backup\SCUP\User2` .  



## <a name="user-state-migration-data"></a>Kullanıcı durumu taşıma verileri  
İşletim sistemi dağıtım senaryolarında Kullanıcı durumu verilerini yakalamak ve geri yüklemek için Configuration Manager görev dizilerini kullanabilirsiniz. Durum geçiş noktası özellikleri, Kullanıcı durumu verilerini depolayan klasörleri listeler. Bu veriler, site sunucusu yedekleme bakım görevinin bir parçası olarak yedeklenmez. Yedekleme planınızın bir parçası olarak, kullanıcı durumu taşıma verilerini depolamak için belirttiğiniz klasörleri el ile yedeklemeniz gerekir.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Kullanıcı durumu taşıma verilerini depolamak için kullanılan klasörleri belirleme  

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **sunucular ve site sistemi rolleri** düğümünü seçin.  

2.  Durum geçiş rolünü barındıran site sistemini seçin. Ardından, **site sistemi rolleri** bölmesinde **durum geçiş noktası** ' nı seçin.  

3.  Şeritteki **Özellikler** ' e tıklayın.  

4.  Kullanıcı durumu taşıma verilerini depolayan klasörler **Genel** sekmesinin **Klasör ayrıntıları** bölümünde listelenir.  



## <a name="about-the-sms-writer-service"></a>SMS Yazıcı hizmeti hakkında  
SMS Yazıcı, yedekleme işlemi sırasında Windows Birim Gölge Kopyası Hizmeti (VSS) ile etkileşimde bulunan bir hizmettir. Configuration Manager site yedeklemesi başarıyla tamamlanmak üzere SMS Yazıcı hizmeti 'nin çalışıyor olması gerekir.  

### <a name="process"></a>İşlem  
1. SMS Yazıcı, VSS hizmetine kaydolur ve bu hizmetin arabirimleri ile olaylarını bağlar. 
2. VSS olayları yayınladığında veya SMS Yazıcıya belirli bildirimleri gönderdiğinde, SMS Yazıcı bildirime yanıt verir ve uygun tedbiri alır. 
3. SMS Yazıcı, içinde bulunan **smsdk. ctl** yedekleme denetim dosyasını okur `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` ve yedeklenecek dosyaları ve verileri belirler. 
4. SMS Yazıcı, SMS kayıt defteri anahtarından ve alt anahtarlarından belirli veriler de dahil olmak üzere çeşitli bileşenlerden oluşan meta verileri oluşturur. 
    a. İstendiğinde meta verileri VSS 'ye gönderir. 
    b. VSS daha sonra, Configuration Manager Yedekleme Yöneticisi olan istek yapan uygulamaya verileri gönderir. 
5. Yedekleme Yöneticisi yedeklenecek verileri seçer ve bu verileri VSS aracılığıyla SMS Yazıcı 'ya gönderir. 
6. SMS Yazıcı yedekleme için hazırlamak amacıyla uygun tedbirleri alır. 
7. Daha sonra VSS anlık görüntüyü almaya hazırsa: a. B olayını gönderir. SMS Yazıcı, tüm Configuration Manager hizmetlerini durduruyor. Anlık görüntü oluşturulurken Configuration Manager etkinliklerinin dondurulmuş olmasını sağlar. 
8. Anlık görüntü tamamlandıktan sonra SMS Yazıcı hizmetleri ve etkinlikleri yeniden başlatır.

SMS Yazıcı hizmeti otomatik olarak yüklenir. VSS uygulaması bir yedekleme veya kurtarma istediğinde bu çalışır durumda olmalıdır.  

### <a name="writer-id"></a>Yazıcı Kimliği  
SMS yazıcısının yazıcı KIMLIĞI **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>İzinler  
SMS Yazıcı hizmeti Yerel Sistem hesabı altında çalışmalıdır.  

### <a name="volume-shadow-copy-service"></a>Birim Gölge Kopyası hizmeti  
VSS, bir sistemdeki uygulamalar birimlere yazmayı sürdürürken, birim yedeklemelerinin yapılmasına olanak veren bir çerçeveyi uygulayan COM API kümesidir. VSS, disk üzerindeki verileri güncelleştiren kullanıcı uygulamaları (SMS Yazıcı hizmeti) ile yedekleme uygulamaları (Yedekleme Yöneticisi hizmeti) arasında eşgüdüme olanak tanıyan tutarlı bir arayüz sağlar. Daha fazla bilgi için [birim gölge kopyası hizmeti](/windows-server/storage/file-server/volume-shadow-copy-service)bakın.  



## <a name="next-steps"></a>Sonraki adımlar
Bir yedekleme oluşturduktan sonra, [Site Recovery](recover-sites.md) 'yi bu yedekleme ile alıştırma yapın. Bu uygulama, bir kurtarma işlemini kullanabilmeniz için bilmeniz gereken bir işlem yapmanıza yardımcı olabilir. Ayrıca, hedeflenen amacı için yedeklemenin başarılı olduğunu onaylamaya de yardımcı olabilir.