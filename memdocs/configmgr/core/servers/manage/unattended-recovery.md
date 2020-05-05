---
title: Katılımsız kurtarma
titleSuffix: Configuration Manager
description: Configuration Manager sitelerinizi kurtarmak için bir komut dosyası kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a12de673776817330a80cb68588faf225922e241
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720803"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Configuration Manager için katılımsız site kurtarma   

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Bir Configuration Manager merkezi yönetim sitesi veya birincil sitesinin [Katılımsız kurtarmasını](recover-sites.md#site-recovery-procedures) gerçekleştirmek için, katılımsız bir yükleme betiği oluşturabilir ve ardından Kurulum 'u **/Script** komut seçeneğiyle kullanabilirsiniz. Betik, Kurulum sihirbazının varsayılan ayar olmaması dışında, aynı türde bilgileri sağlar. Kullanmakta olduğunuz kurtarma türü için geçerli olan kuruluş anahtarlarına ilişkin tüm değerler belirtilmelidir.

 /Script kurulum komut satırı seçeneğini kullanmak için bir başlatma dosyası oluşturmanız gerekir. Ardından,/SCRIPT seçeneğinden sonra bu dosya adını belirtin. Dosyanın adı, **. ini** dosya adı uzantısına sahip olduğu sürece önemli değildir. Kurulum başlatma dosyasına komut satırından başvurduğunuzda dosyanın tam yolunu belirtmeniz gerekir. Örneğin, Kurulum başlatma dosyanızın adı *Setup. ini*ise ve *c:\setup klasöründe*depolanıyorsa, komut satırlarınız şöyle olur:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Kurulumu çalıştırmak için yönetici haklarına sahip olmanız gerekir. Kurulumu Katılımsız komut dosyasıyla çalıştırdığınızda yönetici **olarak çalıştır**seçeneğini kullanarak komut Istemi 'ni yönetici bağlamında başlatın.

 Betik, bölüm adlarını, anahtar adlarını ve değerleri içerir. Gerekli bölüm anahtarı adları, komut dosyasını oluşturduğunuz kurtarma türüne bağlı olarak farklılık gösterir. Anahtarların bölümler içindeki sırası ve bölümlerin dosya içindeki sırası önemli değildir. Anahtarlar büyük/küçük harfe duyarlı değildir. Anahtarlar için değer belirttiğinizde, anahtarın adının ardından bir eşittir işareti (=) ve anahtar değeri gelmelidir.

 Katılımsız site kurtarma için komut dosyanızı oluşturmaya yardımcı olmak üzere aşağıdaki bölümleri kullanın. Tablolarda kullanılabilir kurulum komut dosyası anahtarları, bunlara karşılık gelen değerler, gerekli olup olmadıkları, hangi tür yükleme için kullanıldıkları ve anahtarın kısa bir açıklaması listelenmektedir.

## <a name="recover-a-central-administration-site-unattended"></a>Merkezi yönetim sitesini katılımsız olarak kurtarma
 Bir merkezi yönetim sitesini kurtarmak üzere katılımsız bir Kurulum betik dosyası yapılandırmak için aşağıdaki bilgileri kullanın.

 **Kimlik**

-   **Anahtar Adı:** Eylem

    -   **Gerekli:** Evet
    -   **Değerler:** RecoverCCAR
    -   **Ayrıntılar:** Merkezi bir yönetim sitesini kurtarır


-   **Anahtar adı:** CDLatest

    -   **Gerekli:** Evet – yalnızca CD 'den medya kullanılırken. En son klasör.
    -   **Değerler:** 1 ' den başka bir değer, CD kullanmayan olarak kabul edilir. Sürümü.
    -   **Ayrıntılar:** Bir CD 'deki medyadan Kurulum çalıştırdığınızda betiğinizin bu anahtarı ve değeri içermesi gerekir. Birincil veya merkezi yönetim sitesi yükleme veya birincil veya merkezi yönetim sitesini kurtarma amacıyla en son klasör. Bu değer, kurulum 'u medya formu CD 'si ile bilgilendirir. En son kullanılıyor.

**KurtarmaSeçenekleri**   
-   **Anahtar adı:** ServerRecoveryOptions   

    -   **Gerekli:** Evet
    -   **Değerler:** 1, 2 veya 4  
         1 = Site sunucusunu ve SQL Server'ı kurtarın.   
         2 = Yalnızca site sunucusunu kurtarın.  
         4 = Yalnızca SQL Server'ı kurtarın.
    -   **Ayrıntılar:** Kurulumun site sunucusunu, SQL Server veya her ikisini de kurtarıp kurtarmayacağını belirtir. SunucuKurtarmaSeçenekleri ayarı için aşağıdaki değeri ayarladığınızda ilişkilendirilmiş anahtarlar gerekir:  
        -   **Değer = 1** Siteyi bir site yedeklemesini kullanarak kurtarmak üzere **SiteServerBackupLocation** anahtarı için bir değer belirtebilirsiniz. Bir değer belirlemezseniz, site bir yedekleme kümesinden geri yüklenmeden yeniden yüklenir.

             Site veritabanını yedeklemeden geri yüklemek için olan **DatabaseRecoveryOptions** için **10** değerini belirlediğinizde **BackupLocation** anahtarı gerekir.

        -   **Değer = 2** Siteyi bir site yedeklemesini kullanarak kurtarmak üzere **SiteServerBackupLocation** anahtarı için bir değer belirtebilirsiniz. Bir değer belirlemezseniz, site bir yedekleme kümesinden geri yüklenmeden yeniden yüklenir.

        -   **Değer = 4****DatabaseRecoveryOptions** anahtarı için site veritabanını yedekten geri yükleyen **10** değerini yapılandırırsanız, **BackupLocation** anahtarı gereklidir.

-   **Anahtar Adı:** DatabaseRecoveryOptions

    -   **Gerekli:** Olabilir
    -   **Değerler:**   
         - **10** = site veritabanını yedekten geri yükleyin.  
         - **20** = başka bir yöntem kullanılarak el ile kurtarılmış bir site veritabanı kullanın.   
         - **40** = site için yeni bir veritabanı oluşturun. Bu seçeneği kullanılabilir bir site veritabanı yedeklemesi bulunmadığında kullanın. Genel veriler ve site verileri diğer sitelerden çoğaltmayla kurtarılır.  
         - **80** = veritabanı kurtarmayı atlayın.
    -   **Ayrıntılar:** Kurulumun SQL Server site veritabanını nasıl kurtaracağını belirtir. **ServerRecoveryOptions** ayarı **1** veya **4**değerine sahip olduğunda bu anahtar gerekir.


-   **Anahtar Adı:** ReferenceSite  

    -   **Gerekli:** Olabilir
    -   **Değerler:** &lt;referencesitefqdn\>
    -   **Ayrıntılar:** Başvuru birincil sitesini belirtir. Veritabanı yedeklemesi değişiklik izleme saklama süresinden eskiyse veya siteyi bir yedekleme olmadan kurtarırsanız, merkezi yönetim sitesi genel verileri kurtarmak için başvuru sitesini kullanır.

         Bir başvuru sitesi belirtmezseniz ve yedekleme değişiklik izleme tutma süresinden eskiyse, tüm birincil siteler merkezi yönetim sitesinden geri yüklenen verilerle yeniden başlatılır.

         Bir başvuru sitesi belirtmezseniz ve yedekleme değişiklik izleme tutma süresi içinde olduğunda, yalnızca yedekleme birincil sitelerden çoğaltılmasından sonra değişiklikler yapılır. Farklı birincil sitelerin değişiklikleri çakıştığında merkezi yönetim sitesi aldığı ilk siteyi kullanır.

         **DatabaseRecoveryOptions** ayarının **40**değerine sahip olduğu durumda bu anahtar gerekir.

-   **Anahtar adı:** SiteServerBackupLocation

    -   **Gerekli:** Hayır
    -   **Değerler:** &lt;pathtositeserverbackupset\>
    -   **Ayrıntılar:** Site sunucusu yedekleme kümesinin yolunu belirtir. **ServerRecoveryOptions** ayarı **1** veya **2**değerine sahip olduğunda bu anahtar isteğe bağlıdır. Bir site yedeklemesini kullanarak siteyi kurtarmak için **SiteServerBackupLocation** anahtarı için bir değer belirleyin. Bir değer belirlemezseniz, site bir yedekleme kümesinden geri yüklenmeden yeniden yüklenir.


-   **Anahtar adı:** BackupLocation

    -   **Gerekli:** Olabilir
    -   **Değerler:** &lt;pathtositedatabasebackupset\>
    -   **Ayrıntılar:** Site veritabanı yedekleme kümesinin yolunu belirtir. **ServerRecoveryOptions** anahtarı için **1** veya **4** değerini yapılandırdığınızda ve **DatabaseRecoveryOptions** anahtarı için **10** değerini yapılandırdığınızda **BackupLocation** anahtarı gerekir.


**Seçenekler**

- **Anahtar Adı:** ProductID
  -   **Gerekli:** Evet
  -   **Değerler:**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - Dğer
  -   **Ayrıntılar:** Tireler dahil Configuration Manager yüklemesi ürün anahtarı. Değerlendirme **Configuration Manager** değerlendirme sürümünü yükleyebilir.  


- **Anahtar Adı:** SiteCode

  -   **Gerekli:** Evet
  -   **Değerler:** &lt;site kodu\>
  -   **Ayrıntılar:** Hiyerarşinizde siteyi benzersiz şekilde tanımlayan üç alfa sayısal karakter. Hata öncesinde site tarafından kullanılan site kodunu belirtin.


- **Anahtar adı:** SiteName

  -   **Gerekli:** Evet
  -   **Değerler:** SiteName
  -   **Ayrıntılar:** Bu sitenin açıklaması.


- **Anahtar Adı:** SMSInstallDir

  - **Gerekli:** Evet
  - **Değerler:** &lt;*ConfigMgrInstallationPath*>
  - **Ayrıntılar:** Configuration Manager program dosyaları için yükleme klasörünü belirtir.
    > [!NOTE]   
    >  Configuration Manager yüklemesi için kullanılacak özgün yolu veya yeni bir yolu belirtebilirsiniz.

- **Anahtar Adı:** SDKServer

  -   **Gerekli:** Evet
  -   **Değerler:** &lt;*FQDN of SMS Provider*>
  -   **Ayrıntılar:** SMS sağlayıcısını barındıran sunucunun FQDN 'sini belirtir. Hatadan önce SMS sağlayıcısını barındıran sunucuyu belirtin.

       İlk yüklemeden sonra site için ek SMS Sağlayıcılarını yapılandırabilirsiniz.

- **Anahtar Adı:** PrerequisiteComp

  -   **Gerekli:** Evet
  -   **Değerler:** 0 veya 1  
       0 = indir   
       1 = zaten indirilmiş
  -   **Ayrıntılar:** Kurulum önkoşul dosyalarının daha önce indirilip indirilmediğini belirtir. Örneğin, 0 değerini kullanırsanız, kurulum dosyaları indirir.  


- **Anahtar Adı:** PrerequisitePath

  -   **Gerekli:** Evet
  -   **Değerler:** &lt;*PathToSetupPrerequisiteFiles*>
  -   **Ayrıntılar:** Kurulum önkoşul dosyalarının yolunu belirtir. **ÖnkoşullarBu** değerine bağlı olarak, kurulum bu yolu indirilen dosyaları depolamak veya daha önce indirilen dosyaları bulmak için kullanır.

- **Anahtar adı:** AdminConsole

  -   **Gerekli:** Olabilir
  -   **Değerler:** 0 veya 1 0 = yüklemeyin   
       1 = yükle
  -   **Ayrıntılar:** Configuration Manager konsolunun yüklenip yüklenmeyeceğini belirtir. **ServerRecoveryOptions** ayarının **4**değerine sahip olduğu durum dışında bu anahtar gerekir.


- **Anahtar Adı:** JoinCEIP   
  > [!Note]  
  > Configuration Manager sürüm 1802 ' den başlayarak CEIP özelliği üründen kaldırılır.

  -   **Gerekli:** Evet
  -   **Değerler:** 0 veya 1  
       0 = katılma  
       1 = katıl
  -   **Ayrıntılar:** Müşteri Deneyimi Geliştirme Programı'na katılınıp katılınmayacağını belirtir.

**SQLYapılandırmaSeçenekleri**

-   **Anahtar adı:** SQLServerName

    -   **Gerekli:** Evet
    -   **Değerler:** * &lt;SqlServerName\>*
    -   **Ayrıntılar:** Site veritabanını barındıran SQL Server çalıştıran sunucunun adı veya kümelenmiş örnek adı. Hatadan önce site veritabanını barındıran aynı sunucuyu belirtin.


-   **Anahtar adı:** DatabaseName

    -   **Gerekli:** Evet
    -   **Değerler:** * &lt;sitedatabasename\> * veya * &lt;InstanceName\>*\\*sitedatabasename&lt;\> *
    -   **Ayrıntılar:** Merkezi yönetim sitesi veritabanını yüklemek üzere oluşturulacak ya da kullanılacak SQL Server veritabanı adı. Hata öncesi kullanılan aynı veritabanı adını belirtin.

        > [!IMPORTANT]  
        >  Varsayılan örneği kullanmıyorsanız, örnek adını ve site veritabanı adını belirtmeniz gerekir.

-   **Anahtar adı:** SQLSSBPort

    -   **Gerekli:** Hayır
    -   **Değerler:** &lt;*SSBPortNumber*>
    -   **Ayrıntılar:** SQL Server tarafından kullanılan SQL Server Hizmet Aracısı (SSB) bağlantı noktasını belirtir. Normalde SSB, 4022 numaralı TCP bağlantı noktasını kullanmak üzere yapılandırılmıştır ancak diğer bağlantı noktaları da desteklenir. Hatadan önce kullanılan SSB bağlantı noktasını belirtin.

## <a name="recover-a-primary-site-unattended"></a>Birincil Siteyi Katılımsız Olarak Kurtarma
 Bir merkezi yönetim sitesini kurtarmak üzere katılımsız bir Kurulum betik dosyası yapılandırmak için aşağıdaki bilgileri kullanın.

 **Kimlik**

-   **Anahtar Adı:** Eylem

    -   **Gerekli:** Evet
    -   **Değerler:** RecoverPrimarySite
    -   **Ayrıntılar:** Birincil bir siteyi kurtarır


-   **Anahtar adı:** CDLatest

    -   **Gerekli:** Evet – yalnızca CD 'den medya kullanılırken. En son klasör.
    -   **Değerler:** 1 ' den başka bir değer, CD kullanmayan olarak kabul edilir. Sürümü.
    -   **Ayrıntılar:** Bir CD 'deki medyadan Kurulum çalıştırdığınızda betiğinizin bu anahtarı ve değeri içermesi gerekir. Birincil veya merkezi yönetim sitesi yükleme veya birincil veya merkezi yönetim sitesini kurtarma amacıyla en son klasör. Bu değer, kurulum 'u medya formu CD 'si ile bilgilendirir. En son kullanılıyor.

**KurtarmaSeçenekleri**

-   **Anahtar adı:** ServerRecoveryOptions

    -   **Gerekli:** Evet
    -   **Değerler:** 1, 2 veya 4    
         1 = Site sunucusunu ve SQL Server'ı kurtarın.   
         2 = Yalnızca site sunucusunu kurtarın.  
         4 = Yalnızca SQL Server'ı kurtarın.
    -   **Ayrıntılar:** Kurulumun site sunucusunu, SQL Server veya her ikisini de kurtarıp kurtarmayacağını belirtir. SunucuKurtarmaSeçenekleri ayarı için aşağıdaki değeri ayarladığınızda ilişkilendirilmiş anahtarlar gerekir:

        -   **Değer = 1** Siteyi bir site yedeklemesini kullanarak kurtarmak üzere **SiteServerBackupLocation** anahtarı için bir değer belirtebilirsiniz. Bir değer belirlemezseniz, site bir yedekleme kümesinden geri yüklenmeden yeniden yüklenir.

             Site veritabanını yedeklemeden geri yüklemek için olan **DatabaseRecoveryOptions** için **10** değerini belirlediğinizde **BackupLocation** anahtarı gerekir.

        -   **Değer = 2** Siteyi bir site yedeklemesini kullanarak kurtarmak üzere **SiteServerBackupLocation** anahtarı için bir değer belirtebilirsiniz. Bir değer belirlemezseniz, site bir yedekleme kümesinden geri yüklenmeden yeniden yüklenir.

        -   **Değer = 4****DatabaseRecoveryOptions** anahtarı için site veritabanını yedekten geri yükleyen **10** değerini yapılandırırsanız, **BackupLocation** anahtarı gereklidir.

-   **Anahtar Adı:** DatabaseRecoveryOptions

    -   **Gerekli:** Olabilir
    -   **Değerler:**   
         - **10** = site veritabanını yedekten geri yükleyin.  
         - **20** = başka bir yöntem kullanılarak el ile kurtarılmış bir site veritabanı kullanın.     
         - **40** = site için yeni bir veritabanı oluşturun. Bu seçeneği kullanılabilir bir site veritabanı yedeklemesi bulunmadığında kullanın. Genel veriler ve site verileri diğer sitelerden çoğaltmayla kurtarılır.  
         - **80** = veritabanı kurtarmayı atlayın.
    -   **Ayrıntılar:** Kurulumun SQL Server site veritabanını nasıl kurtaracağını belirtir. **ServerRecoveryOptions** ayarı **1** veya **4**değerine sahip olduğunda bu anahtar gerekir.


-   **Anahtar adı:** SiteServerBackupLocation

    -   **Gerekli:** Hayır
    -   **Değerler:** &lt;pathtositeserverbackupset\>
    -   **Ayrıntılar:** Site sunucusu yedekleme kümesinin yolunu belirtir. **ServerRecoveryOptions** ayarı **1** veya **2**değerine sahip olduğunda bu anahtar isteğe bağlıdır. Bir site yedeklemesini kullanarak siteyi kurtarmak için **SiteServerBackupLocation** anahtarı için bir değer belirleyin. Bir değer belirlemezseniz, site bir yedekleme kümesinden geri yüklenmeden yeniden yüklenir.     


-   **Anahtar adı:** BackupLocation

    -   **Gerekli:** Olabilir
    -   **Değerler:** &lt;pathtositedatabasebackupset\>
    -   **Ayrıntılar:** Site veritabanı yedekleme kümesinin yolunu belirtir. **ServerRecoveryOptions** anahtarı için **1** veya **4** değerini yapılandırdığınızda ve **DatabaseRecoveryOptions** anahtarı için **10** değerini yapılandırdığınızda **BackupLocation** anahtarı gerekir.

**Seçenekler**

-   **Anahtar Adı:** ProductID

    -   **Gerekli:** Evet
    -   **Değerler:**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Dğer     
    -   **Ayrıntılar:** Tireler dahil Configuration Manager yüklemesi ürün anahtarı. Değerlendirme **Configuration Manager** değerlendirme sürümünü yükleyebilir.  


-   **Anahtar Adı:** SiteCode

    -   **Gerekli:** Evet
    -   **Değerler:** &lt;site kodu\>
    -   **Ayrıntılar:** Hiyerarşinizde siteyi benzersiz şekilde tanımlayan üç alfa sayısal karakter. Hata öncesinde site tarafından kullanılan site kodunu belirtin.


-   **Anahtar adı:** SiteName

    -   **Gerekli:** Evet
    -   **Değerler:** SiteName
    -   **Ayrıntılar:** Bu sitenin açıklaması.


-   **Anahtar Adı:** SMSInstallDir

    -   **Gerekli:** Evet
    -   **Değerler:** &lt;*ConfigMgrInstallationPath*>
    -   **Ayrıntılar:** Configuration Manager program dosyaları için yükleme klasörünü belirtir.

        > [!NOTE]   
        >  Configuration Manager yüklemesi için kullanılacak özgün yolu veya yeni bir yolu belirtebilirsiniz.

-   **Anahtar Adı:** SDKServer

    -   **Gerekli:** Evet
    -   **Değerler:** &lt;*FQDN of SMS Provider*>
    -   **Ayrıntılar:** SMS sağlayıcısını barındıran sunucunun FQDN 'sini belirtir. Hatadan önce SMS sağlayıcısını barındıran sunucuyu belirtin.

         İlk yüklemeden sonra site için ek SMS Sağlayıcılarını yapılandırabilirsiniz.

-   **Anahtar Adı:** PrerequisiteComp

    -   **Gerekli:** Evet
    -   **Değerler:** 0 veya 1    
         0 = indir   
         1 = zaten indirilmiş   
    -   **Ayrıntılar:** Kurulum önkoşul dosyalarının daha önce indirilip indirilmediğini belirtir. Örneğin, 0 değerini kullanırsanız, kurulum dosyaları indirir.


-   **Anahtar Adı:** PrerequisitePath

    -   **Gerekli:** Evet
    -   **Değerler:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Ayrıntılar:** Kurulum önkoşul dosyalarının yolunu belirtir. **ÖnkoşullarBu** değerine bağlı olarak, kurulum bu yolu indirilen dosyaları depolamak veya daha önce indirilen dosyaları bulmak için kullanır.


-   **Anahtar adı:** AdminConsole

    -   **Gerekli:** Olabilir
    -   **Değerler:** 0 veya 1  
         0 = yükleme   
         1 = yükle  
    -   **Ayrıntılar:** Configuration Manager konsolunun yüklenip yüklenmeyeceğini belirtir. **ServerRecoveryOptions** ayarının **4**değerine sahip olduğu durum dışında bu anahtar gerekir.

-   **Anahtar Adı:** JoinCEIP  
    > [!Note]  
    > Configuration Manager sürüm 1802 ' den başlayarak CEIP özelliği üründen kaldırılır.

    -   **Gerekli:** Evet
    -   **Değerler:** 0 veya 1    
         0 = katılma  
         1 = katıl
    -   **Ayrıntılar:** Müşteri Deneyimi Geliştirme Programı'na katılınıp katılınmayacağını belirtir.


**SQLYapılandırmaSeçenekleri**

-   **Anahtar adı:** SQLServerName

    -   **Gerekli:** Evet
    -   **Değerler:** * &lt;SqlServerName\>*
    -   **Ayrıntılar:** Site veritabanını barındıran SQL Server çalıştıran sunucunun adı veya kümelenmiş örnek adı. Hatadan önce site veritabanını barındıran aynı sunucuyu belirtin.


-   **Anahtar adı:** DatabaseName

    -   **Gerekli:** Evet
    -   **Değerler:** * &lt;sitedatabasename\> * veya * &lt;InstanceName\>*\\*sitedatabasename&lt;\> *
    -   **Ayrıntılar:** Merkezi yönetim sitesi veritabanını yüklemek üzere oluşturulacak ya da kullanılacak SQL Server veritabanı adı. Hata öncesi kullanılan aynı veritabanı adını belirtin.

        > [!IMPORTANT]    
        >  Varsayılan örneği kullanmıyorsanız, örnek adını ve site veritabanı adını belirtmeniz gerekir.

-   **Anahtar adı:** SQLSSBPort

    -   **Gerekli:** Hayır
    -   **Değerler:** &lt;*SSBPortNumber*>
    -   **Ayrıntılar:** SQL Server tarafından kullanılan SQL Server Hizmet Aracısı (SSB) bağlantı noktasını belirtir. Normalde SSB, 4022 numaralı TCP bağlantı noktasını kullanmak üzere yapılandırılmıştır ancak diğer bağlantı noktaları da desteklenir. Hatadan önce kullanılan SSB bağlantı noktasını belirtin.

**Hiyerarşi Genişletme Seçeneği**

-   **Anahtar Adı:** CCARSiteServer

    -   **Gerekli:** Olabilir
    -   **Değerler:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Ayrıntılar:** Birincil bir sitenin Configuration Manager hiyerarşisine katıldığında, iliştirme merkezi yönetim sitesini belirtir. Birincil site hata öncesinde bir merkezi yönetim sitesine bağlıysa bu ayar gereklidir. Hatadan önce merkezi yönetim sitesi için kullanılan site kodunu belirtin.

-   **Anahtar adı:** CASRetryInterval

    -   **Gerekli:** Hayır
    -   **Değerler:** &lt;*Interval*>
    -   **Ayrıntılar:** Bağlantı kurulamadıktan sonra merkezi yönetim sitesine bağlanmaya çalışmayı yeniden deneme aralığını (dakika olarak) belirtir. Örneğin, merkezi yönetim sitesiyle bağlantı başarısız olursa, birincil site CASRetryInterval için belirttiğiniz dakika sayısını bekler ve ardından bağlantıyı yeniden durdurur.


-   **Anahtar adı:** WaitForCASTimeout

    -   **Gerekli:** Hayır
    -   **Değerler:** &lt;*Timeout*>
    -   **Ayrıntılar:** Birincil bir sitenin merkezi yönetim sitesine bağlanmak için en uzun zaman aşımı süresini (dakika olarak) belirtir. Örneğin, birincil site bir merkezi yönetim sitesine bağlanamazsa WaitForCASTimeout süresine ulaşılana kadar CASRetryInterval değerine göre merkezi yönetim sitesiyle bağlantı kurmayı yeniden dener. 0 ile 100 arası bir değer belirleyebilirsiniz.
