---
title: Yönetim noktası veritabanı çoğaltmaları
titleSuffix: Configuration Manager
description: Yönetim noktaları tarafından site veritabanı sunucusuna yerleştirilmiş CPU yükünü azaltmak için bir veritabanı çoğaltması kullanın.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db1e0d78263d264c66eed7258db800397baad735
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607590"
---
# <a name="database-replicas-for-management-points-for-configuration-manager"></a>Configuration Manager için yönetim noktaları için veritabanı çoğaltmaları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager birincil siteler, istemcilerden gelen istekleri hizmet eden yönetim noktaları tarafından site veritabanı sunucusuna yerleştirilmiş CPU yükünü azaltmak için bir veritabanı çoğaltması kullanabilir.  

-   Bir yönetim noktası bir veritabanı çoğaltması kullandığında, o yönetim noktası verileri site veritabanı sunucusu yerine veritabanı çoğaltmasını barındıran SQL Server bilgisayarından ister.  

-   Bunun yapılması, istemcilerle ilgili sık işleme görevlerini boşaltarak site veritabanı sunucusundaki CPU işleme gereksinimlerini azaltmaya yardımcı olabilir.  İstemci ilkesi için sık istekler yapan çok sayıda istemcinin bulunduğu siteler, istemciler için sık işleme görevlerinin bir örneğidir.  


##  <a name="prepare-to-use-database-replicas"></a><a name="bkmk_Prepare"></a> Veritabanı çoğaltmalarını kullanmaya hazırlanma  
**Yönetim noktaları için veritabanı çoğaltmaları hakkında:**  

-   Çoğaltmalar ayrı bir SQL Server örneğine çoğaltılan site veritabanı kısmi kopyasıdır:  

    -   Birincil siteler, sitedeki her yönetim noktası için ayrılmış bir veritabanı çoğaltmasını destekler (Ikincil siteler veritabanı çoğaltmalarını desteklemez)  

    -   Tek veritabanı çoğaltması aynı siteden birden çok yönetim noktası tarafından kullanılabilir  

    -   Bir SQL sunucusu, her biri ayrı bir SQL Server örneğinde çalıştığı sürece farklı yönetim noktaları tarafından kullanılmak üzere birden çok veritabanı çoğaltma barındırabilir  

-   Çoğaltmalar, bu amaçla site veritabanı sunucusu tarafından yayımlanan verilerden sabit bir zamanlama ile site veritabanının bir kopyasını eşitler.  

-   Yönetim noktaları, bir yönetim noktasını yüklediğinizde ya da daha önce yüklenmiş bir yönetim noktasını veritabanı çoğaltması kullanacak şekilde yeniden yapılandırarak daha sonra, çoğaltma kullanacak şekilde yapılandırılabilir  

-   Çoğaltmanın aralarında gerçekleştiğinden ve veritabanı çoğaltması sunucusunun performansının gerek duyduğunuz site ve istemci performansı için yeterli olduğundan emin olmak amacıyla site veritabanı sunucusu ile her veritabanı çoğaltması sunucusunu düzenli olarak izleyin  

**Veritabanı çoğaltmaları için önkoşullar:**  

-   **SQL Server gereksinimleri:**  

    -   Veritabanı çoğaltmasını barındıran SQL Server, site veritabanı sunucusuyla aynı gereksinimleri karşılamalıdır. Ancak, desteklenen bir SQL Server sürümünü çalıştırdığı sürece çoğaltma sunucusunun, site veritabanı sunucusuyla anı SQL Server sürümünü çalıştırması gerekmez. Bilgi için bkz. [Configuration Manager için SQL Server sürümleri desteği](../../../../core/plan-design/configs/support-for-sql-server-versions.md)  

    -   Çoğaltma veritabanını barındıran bilgisayardaki SQL Server hizmeti, **sistem** hesabı olarak çalıştırılmalıdır.  

    -   Hem site veritabanı sunucusunu barındıran hem de bir veritabanı çoğaltması barındıran SQL Server’da **SQL Server çoğaltması** yüklü olmalıdır.  

    -   Site veritabanı, veritabanı çoğaltmasını **yayımlamalıdır** ve her uzak veritabanı çoğaltma sunucusu yayımlanan verilere **abone** olmalıdır.  

    -   Hem site veritabanını barındıran hem de bir veritabanı çoğaltması barındıran SQL Server, 2 GB’lik **En Büyük Metin Çoğaltma Boyutu** ’nu destekleyecek şekilde yapılandırılmalıdır. Bunun SQL Server 2012 için nasıl yapılandırılacağına dair bir örnek için, bkz. [En büyük metin çoğaltma boyutu Sunucu Yapılandırma Seçeneğini yapılandırma](/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option).  

-   **Otomatik olarak imzalanan sertifika:** Bir veritabanı çoğaltmasını yapılandırmak için, veritabanı çoğaltması sunucusunda otomatik olarak imzalanan bir sertifika oluşturmalı ve bu sertifikayı veritabanı çoğaltması sunucusunu kullanacak yönetim noktalarının her biri için kullanılabilir hale getirebilirsiniz.  

    -   Bu sertifika, veritabanı çoğaltması sunucusunda yüklü bir yönetim noktası tarafından otomatik olarak kullanılabilir.  

    -   Bu sertifikanın uzak yönetim noktalarına kullanılabilir kılınabilmesi için, sertifikayı dışa vermeli ve ardından uzak yönetim noktasında **Güvenilir Kişiler** sertifika deposuna eklemelisiniz.  

-   **İstemci bildirimi** : Bir yönetim noktası için veritabanı çoğaltmasıyla istemci bildirimini desteklemek için, site veritabanı sunucusuyla **SQL Server Hizmet Aracısı**için veritabanı çoğaltma sunucusu arasında iletişimi yapılandırmanız gerekir. Bunun yapılması şunları gerektirir:  

    -   Her veritabanını diğer veritabanıyla ilgili bilgilerle yapılandırma  

    -   Güvenli iletişim için iki veritabanı arasında sertifika alışverişi  

**Veritabanı çoğaltmalarını kullanmaya ilişkin sınırlamalar:**  

-   Siteniz veritabanı çoğaltmaları yayınlayacak şekilde yapılandırıldığında, normal yönergeler yerine aşağıdaki yordamlar kullanılmalıdır:  

    -   [Veritabanı çoğaltması yayımlayan bir site sunucusunu kaldırma](#BKMK_DBReplicaOps_Uninstall)  

    -   [Veritabanı çoğaltması yayımlayan bir site sunucusu veritabanını taşıma](#BKMK_DBReplicaOps_Move)  

-   **Güncel dala Configuration Manager yükseltmeler**: bir siteyi yükseltmeden önce, System Center 2012 Configuration Manager güncel dalı Configuration Manager veya geçerli dalı son sürüme güncelleştiren Configuration Manager, yönetim noktaları için veritabanı çoğaltmalarını devre dışı bırakmanız gerekir.  Siteniz yükseltildikten sonra yönetim noktalarının veritabanı çoğaltmalarını yeniden yapılandırabilirsiniz.  

-   **Tek bir SQL Server birden çok çoğaltma:**  Bir veritabanı çoğaltma sunucusunu yönetim noktaları için birden çok veritabanı çoğaltmasını barındıracak şekilde yapılandırırsanız (her çoğaltma ayrı bir örnekte olmalıdır), bu sunucuda daha önce yapılandırılmış veritabanı çoğaltmalarının kullanıldığı otomatik olarak imzalanan sertifikanın üzerine yazılmasını engellemek için, değiştirilen bir yapılandırma betiği (aşağıdaki bölümde 4. adımdan) kullanmanız gerekir.  

- Yazılım merkezindeki Kullanıcı dağıtımları bir SQL çoğaltması kullanarak yönetim noktasına karşı çalışmaz. <!--sccmdocs-1011-->

##  <a name="configure-database-replicas"></a><a name="BKMK_DBReplica_Config"></a> Veritabanı çoğaltmalarını yapılandırma  
Bir veritabanı çoğaltmasını yapılandırmak için aşağıdaki adımlar gereklidir:  

-   [Adım 1 - Veritabanı çoğaltmasını Yayımlamak için site veritabanı sunucusunu yapılandırma](#BKMK_DBReplica_ConfigSiteDB)  

-   [2. adım-veritabanı çoğaltma sunucusunu yapılandırma](#BKMK_DBReplica_ConfigSrv)  

-   [Adım 3 - Veritabanı çoğaltmasını kullanmak için yönetim noktalarını yapılandırma](#BKMK_DBReplica_ConfigMP)  

-   [4. adım-veritabanı çoğaltma sunucusu için otomatik olarak imzalanan sertifika yapılandırma](#BKMK_DBReplica_Cert)  

-   [5. adım-veritabanı çoğaltma sunucusu için SQL Server Hizmet Aracısı yapılandırma](#BKMK_DBreplica_SSB)  

###  <a name="step-1---configure-the-site-database-server-to-publish-the-database-replica"></a><a name="BKMK_DBReplica_ConfigSiteDB"></a> Adım 1-veritabanı çoğaltmasını yayımlamak için site veritabanı sunucusunu yapılandırma  
 Veritabanı çoğaltmasını yayınlamak için Windows Server 2008 R2 bilgisayarında site veritabanı sunucusunun nasıl yapılandırılacağına dair bir örnek olarak aşağıdaki yordamı kullanın. Farklı bir işletim sistemi sürümüne sahipseniz, işletim sistemi belgelerinize başvurun ve bu yordamdaki adımları gereken şekilde ayarlayın.  

##### <a name="to-configure-the-site-database-server"></a>Site veritabanı sunucusunu yapılandırmak için  

1.  Site veritabanı sunucusunda SQL Server Aracısı uygulamasını otomatik başlayacak şekilde ayarlayın.  

2.  Site veritabanı sunucusunda, **ConfigMgr_MPReplicaAccess**adında bir yerel kullanıcı grubu oluşturun. Söz konusu veritabanı çoğaltması sunucularının yayınlanan veritabanı çoğaltmasıyla eş zamanlanmasını sağlamak için, bu sitede kullandığınız her veritabanı çoğaltması sunucusu bilgisayar hesabını bu gruba eklemeniz gerekir.  

3.  Site veritabanı sunucusunda, **ConfigMgr_MPReplica**adıyla bir dosya paylaşma yapılandırın.  

4.  **ConfigMgr_MPReplica** paylaşıma aşağıdaki izinleri ekleyin:  

    > [!NOTE]  
    >  SQL Server Aracı yerel sistem hesabı dışında bir hesap kullanıyorsa, aşağıdaki listede SİSTEM öğesini o hesap adıyla değiştirin.  

    -   **Paylaşma İzinleri**:  

        -   SİSTEM: **Yazma**  

        -   ConfigMgr_MPReplicaAccess: **okuma**  

    -   **NTFS İzinleri**:  

        -   SİSTEM: **Tam Denetim**  

        -   ConfigMgr_MPReplicaAccess: **okuma**, **okuma & yürütme**, **klasör içeriğini listeleme**  

5.  Bu site veritabanına bağlanmak ve aşağıdaki saklı yordamı bir sorgu olarak çalıştırmak için **SQL Server Management Studio** uygulamasını kullanın: **spCreateMPReplicaPublication**  

Saklı yordam tamamlandığında, site veritabanı sunucusu veritabanı çoğaltmasını yayınlayacak şekilde yapılandırılır.  

###  <a name="step-2---configuring-the-database-replica-server"></a><a name="BKMK_DBReplica_ConfigSrv"></a> Adım 2 - Veritabanı çoğaltma sunucusunu yapılandırma  
Veritabanı çoğaltması sunucusu, SQL Server çalıştıran ve yönetim noktalarının kullanacağı site veritabanının çoğaltmasını barındıran bir bilgisayardır. Veritabanı çoğaltması sunucusu sabit bir zamanlamada veritabanı kopyasını site veritabanı sunucusu tarafından yayınlanan veritabanı çoğaltmasıyla eş zamanlar.  

Veritabanı çoğaltması sunucusu, site veritabanı sunucusuyla aynı gereksinimleri karşılamalıdır. Ancak, veritabanı çoğaltması sunucusu, site veritabanı sunucusunun kullandığından farklı bir SQL Server sürümünü çalıştırabilir. Desteklenen SQL Server sürümleri hakkında daha fazla bilgi için [Configuration Manager için SQL Server sürümleri Için destek](../../../../core/plan-design/configs/support-for-sql-server-versions.md) konusuna bakın.  

> [!IMPORTANT]  
>  Veritabanı çoğaltmasını barındıran bilgisayardaki SQL Server Hizmeti, Sistem hesabı olarak çalıştırılmalıdır.  

Windows Server 2008 R2 bilgisayarında site veritabanı çoğaltması sunucusunun nasıl yapılandırılacağına dair bir örnek olarak aşağıdaki yordamı kullanın. Farklı bir işletim sistemi sürümüne sahipseniz, işletim sistemi belgelerinize başvurun ve bu yordamdaki adımları gereken şekilde ayarlayın.  

##### <a name="to-configure-the-database-replica-server"></a>Veritabanı çoğaltması sunucusunu yapılandırmak için  

1. Veritabanı çoğaltması sunucusunda SQL Server Aracı uygulamasını otomatik başlayacak şekilde ayarlayın.  

2. Veritabanı çoğaltması sunucusunda, yerel sunucuya bağlanmak için **SQL Server Management Studio** uygulamasını kullanın, **Çoğaltma** klasörüne göz atın, Yerel Abonelikler'i tıklatın ve **Yeni Abonelikler** öğesini seçerek **Yeni Abonelik Sihirbazı**'nı başlatın:  

   1. **Yayın** sayfasında, **Yayıncı** liste kutusunda, **SQL Server Yayıncısını Bul**’u seçin, sitelerin veritabanı sunucusunun adını girip, ardından **Bağlan**’ı tıklatın.  

   2. **ConfigMgr_MPReplica**öğesini seçin ve ardından **İleri**' ye tıklayın.  

   3. **Dağıtım Aracısı konumu** sayfasında, **her aracıyı abonede (çekme abonelikleri) Çalıştır**' ı seçin ve **İleri**' ye tıklayın.  

   4. **Abonelikler** sayfasında, aşağıdakilerden birini yapın:  

      -   Veritabanı çoğaltması için kullanmak amacıyla veritabanı çoğaltması sunucusundan var olan bir veritabanını seçip, ardından **Tamam**'a tıklayın.  

      -   Veritabanı çoğaltması için yeni bir veritabanı oluşturmak amacıyla **Yeni veritabanı** öğesini seçin. **Yeni Veritabanı** sayfasında bir veritabanı adı belirleyip, ardından **Tamam**'a tıklayın.  

   5. Devam etmek için **İleri**'ye tıklayın.  

   6. **Dağıtım Aracısı güvenliği** sayfasında, iletişim kutusunun abone bağlantısı satırında bulunan özellikler düğmesine **(...)** tıklayın ve ardından bağlantının güvenlik ayarlarını yapılandırın.  

      > [!TIP]  
      >  Özellikler düğmesi **(...)**, görüntüleme kutusunun dördüncü sütunundadır.  

      **Güvenlik ayarları:**  

      - Dağıtım Aracısı işlemini çalıştıran hesabı yapılandırın (işlem hesabı):  

        -   SQL Server Agent yerel sistem olarak çalışıyorsa, **SQL Server Agent hizmet hesabı altında Çalıştır ' ı seçin (Bu önerilen bir güvenlik uygulaması değildir.)**  

        -   SQL Server Aracısı farklı bir hesap kullanılarak çalıştırılıyorsa, **Aşağıdaki Windows hesabı altında çalıştır**’ı seçip, ardından o hesabı yapılandırın. Bir Windows hesabı veya SQL Server hesabı belirleyebilirsiniz.  

        > [!IMPORTANT]  
        >  Dağıtım Aracısını çalıştıran hesaba yayıncıya abonelik çekme izinlerini vermelisiniz. Bu izinleri yapılandırma hakkında daha fazla bilgi için bkz. [Dağıtım Aracısı güvenliği](/sql/relational-databases/replication/distribution-agent-security).  

      - **Dağıtıcıya Bağlan**için, **İşlem hesabı kimliğine bürünerek**seçeneğini belirleyin.  

      - **Aboneye Bağlan**için, **İşlem hesabı kimliğine bürünerek**seçeneğini belirleyin.  

        Bağlantı güvenliği ayarlarını yapılandırdıktan sonra, bunları kaydetmek için **Tamam** 'ı tıklatıp, ardından **İleri**'yi tıklatın.  

   7. **Eşitleme Zamanlaması** sayfasında, **Aracı Zamanlaması** liste kutusunda, **Zamanlama tanımla**’yı seçip, ardından **Yeni İş Zamanlaması**’nı yapılandırın. Sıklığı **günlük**olarak gerçekleşecek şekilde, **5 dakikada**bir Yinele ve süreyi **bitiş tarihi**olmayacak şekilde ayarlayın. Zamanlamayı kaydetmek için **İleri** 'yi tıklatıp, ardından yeniden **İleri** 'ye tıklayın.  

   8. **Sihirbaz eylemleri** sayfasında, **abonelikleri oluştur**onay kutusunu seçin ve ardından **İleri**' ye tıklayın.  

   9. **Sihirbazı Tamamlama** sayfasında, **Bitir**'i tıklattıktan sonra Sihirbazı tamamlamak için **Kapat** 'ı tıklatın.  

3. Yeni Abonelik Sihirbazı’nı tamamlar tamamlamaz, **SQL Server Management Studio** ’yu kullanarak veritabanı çoğaltma sunucusu veritabanına bağlanın ve TRUSTWORTHY veritabanı özelliğini etkinleştirmek üzere şu sorguyu çalıştırın:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. Aboneliğin başarılı olduğunu doğrulamak için eş zamanlama durumunu gözden geçirin:  

   -   Abone bilgisayarda:  

       -   **SQL Server Management Studio**uygulamasında veritabanı çoğaltması sunucuna bağlanın ve **Çoğaltma**’yı genişletin.  

       -   **Yerel abonelikler**' i genişletin, site veritabanı yayınına olan aboneliği sağ tıklatın ve ardından **eşitleme durumunu görüntüle**' yi seçin.  

   -   Yayıncı bilgisayarda:  

       -   **SQL Server Management Studio**, site veritabanı bilgisayarına bağlanın, **çoğaltma** klasörüne sağ tıklayın ve ardından **çoğaltma İzleyicisini Başlat**' ı seçin.  

5. Veritabanı çoğaltması için ortak dil çalışma zamanı (CLR) tümleştirmesini etkinleştirmek için, veritabanı çoğaltma sunucusundaki veritabanı çoğaltmasına bağlanmak üzere **SQL Server Management Studio** kullanın ve şu saklı yordamı sorgu olarak çalıştırın: **Exec sp_configure ' CLR Enabled ', 1; GEÇERSIZ KıLMA Ile YENIDEN YAPıLANDıR**  

6. Bir veritabanı çoğaltması sunucusu kullanan her yönetim noktası için, söz konusu yönetim noktaları bilgisayar hesabını o veritabanı çoğaltması sunucusundaki yerel **Yöneticiler** grubuna ekleyin.  

   > [!TIP]  
   >  Bu adım, veritabanı çoğaltması sunucusunda çalışan bir yönetim noktası için gerekli değildir.  

   Veritabanı çoğaltması artık bir yönetim noktasının kullanımı için hazırdır.  

###  <a name="step-3---configure-management-points-to-use-the-database-replica"></a><a name="BKMK_DBReplica_ConfigMP"></a> 3. adım-veritabanı çoğaltmasını kullanmak için yönetim noktalarını yapılandırma  
 Birincil sitedeki bir yönetim noktasını veritabanı çoğaltmasını kullanması için yönetim noktası rolünü yüklediğinizde yapılandırabilir veya var olan bir yönetim noktasını bir veritabanı çoğaltması kullanmak üzere yeniden yapılandırabilirsiniz.  

 Bir yönetim noktasını bir veritabanı çoğaltması kullanması için yapılandırmak amacıyla aşağıdaki bilgileri kullanın:  

-   **Yeni bir yönetim noktası yapılandırmak için** : Yönetim noktasını yüklemek için kullandığınız sihirbazın **Yönetim Noktası Veritabanı** sayfasında **Veritabanı çoğaltması kullan**'ı seçin ve veritabanı çoğaltmasını barındıran bilgisayarın FQDN'sini belirleyin. Ardından **ConfigMgr site veritabanı adı**için o bilgisayarda veritabanı çoğaltmasının veritabanı adını belirleyin.  

-   **Daha önce yüklenmiş bir yönetim noktasını yapılandırmak için**: Yönetim noktasının özellikler sayfasını açın, **Yönetim Noktası Veritabanı** sekmesini seçin, **Bir veritabanı çoğaltması kullan**öğesini seçip, ardından veritabanı çoğaltmasını barındıran bilgisayarın FQDN'sini belirleyin. Ardından **ConfigMgr site veritabanı adı**için o bilgisayarda veritabanı çoğaltmasının veritabanı adını belirleyin.  

-   **Bir veritabanı çoğaltması kullanan her yönetim noktası için**, yönetim noktası sunucusunun bilgisayar hesabını veritabanı çoğaltmasının **db_datareader** rolüne el ile eklemeniz gerekir.  

Yönetim noktasını veritabanı çoğaltması sunucusunu kullanmak üzere yapılandırmanın yanı sıra, yönetim noktasında **IIS** 'de **Windows Kimlik Doğrulama** özelliğini etkinleştirmeniz gerekir:  

1.  **Internet Information Services (IIS) Yöneticisi 'ni**açın.  

2.  Yönetim noktası tarafından kullanılan Web sitesini seçip, **Kimlik Doğrulama**öğesini açın.  

3.  **Windows kimlik doğrulamasını** **etkin**olarak ayarlayın ve ardından **Internet Information Services (IIS) Yöneticisi 'ni**kapatın.  

###  <a name="step-4--configure-a-self-signed-certificate-for-the-database-replica-server"></a><a name="BKMK_DBReplica_Cert"></a> Adım 4 - Veritabanı çoğaltma sunucusu için otomatik olarak imzalanan sertifika yapılandırma  
 Veritabanı çoğaltması sunucusunda otomatik olarak imzalanan bir sertifika oluşturmalı ve bu sertifikayı veritabanı çoğaltması sunucusunu kullanacak yönetim noktalarının her biri için kullanılabilir hale getirebilirsiniz.  

 Bu sertifika, veritabanı çoğaltması sunucusunda yüklü bir yönetim noktası tarafından otomatik olarak kullanılabilir. Ancak bu sertifikanın uzak yönetim noktalarına kullanılabilir kılınabilmesi için, sertifikayı dışa vermeli ve ardından uzak yönetim noktasında Güvenilir Kişiler sertifika deposuna eklemelisiniz.  

 Windows Server 2008 R2 bilgisayarı için veritabanı çoğaltma sunucusunda otomatik olarak imzalanan sertifikanın nasıl yapılandırılacağı hakkında bir örnek olarak aşağıdaki yordamları kullanın. Farklı bir işletim sistemi sürümüne sahipseniz, işletim sistemi belgelerinize başvurun ve bu yordamlardaki adımları gereken şekilde ayarlayın.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>Veritabanı çoğaltması sunucusu için otomatik olarak imzalanan sertifika yapılandırmak için  

1.  Veritabanı Çoğaltma sunucusunda, yönetici ayrıcalıklarıyla bir PowerShell komut istemi açın ve şu komutu çalıştırın: **set-executionpolicy Kısıtlamasız**  

2.  Aşağıdaki PowerShell komut dosyasını kopyalayıp, **CreateMPReplicaCert.ps1**adlı bir dosya olarak kaydedin. Bu dosyanın bir kopyasını, veritabanı çoğaltması sunucusunun sistem bölümü kök dizinine yerleştirin.  

    > [!IMPORTANT]  
    >  Tek bir SQL Server üzerinde birden fazla veritabanı çoğaltması yapılandırıyorsanız, daha sonra yapılandırdığınız her çoğaltma için bu yordamda bu komut dosyasının değiştirilmiş bir sürümünü kullanmanız gerekir. Bkz.  [Tek bir SQL Server üzerinde ek veritabanı çoğaltmaları için ek komut dosyası](#bkmk_supscript)  

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  Veritabanı çoğaltması sunucusunda SQL Server yapılandırmanız için geçerli olan aşağıdaki komutu çalıştırın:  

    -   SQL Server varsayılan örneği için: dosya **CreateMPReplicaCert.ps1** sağ tıklayın ve **PowerShell ile Çalıştır**' ı seçin. Betik çalıştırıldığında, otomatik olarak imzalanan sertifikayı oluşturur ve sertifikayı kullanmak için SQL Server yapılandırır.  

    -   SQL Server adlandırılmış bir örneği için: **% Path% \CreateMPReplicaCert.ps1 xxxxxx** komutunu çalıştırmak Için PowerShell kullanın; burada **xxxxxx** SQL Server örneğinin adıdır.  

    -   Komut dosyası tamamlandıktan sonra, SQL Server Aracısı'nın çalıştığını doğrulayın. Çalışmıyorsa, SQL Server Aracısı'nı yeniden başlatın.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>Uzak yönetim noktalarını veritabanı çoğaltması sunucusunun otomatik imzalı sertifikasını kullanacak şekilde yapılandırmak için  

1.  Veritabanı Çoğaltma sunucusunda, sunucunun otomatik imzalı sertifikasını dışarı aktarmak için aşağıdaki adımları gerçekleştirin:  

    1.  **Başlat**, **Çalıştır**’a tıklayın ve **mmc.exe**yazın. Boş konsolda **Dosya**'yı tıklatın ve **Ek Bileşen Ekle/Kaldır**'ı tıklatın.  

    2.  **Ek Bileşenler Ekle/Kaldır** iletişim kutusunda **Kullanılabilir ek bileşenler** listesinden **Sertifikalar**'ı seçin ve **Ekle**'yi tıklatın.  

    3.  **Sertifika ek bileşeni** iletişim kutusunda **Bilgisayar hesabı**'nı seçin ve **İleri**'yi tıklatın.  

    4.  **Bilgisayar Seç** iletişim kutusunda, **Yerel bilgisayar: (bu konsolun üzerinde çalıştığı bilgisayar)** seçeneğinin belirlenmiş olduğundan emin olarak **Son**'a tıklayın.  

    5.  **Ek Bileşenler Ekle/Kaldır** iletişim kutusunda **Tamam**'ı tıklatın.  

    6.  Konsolda, **Sertifikalar (Yerel Bilgisayar)**'ı ve **Kişisel**'i genişlettikten sonra **Sertifikalar**'ı seçin.  

    7.  **ConfigMgr SQL Server kimlik sertifikasının**kolay adına sahip sertifikaya sağ tıklayın, **Tüm görevler**' e ve ardından **dışarı aktar**' ı seçin.  

    8.  **Sertifika Verme Sihirbazı** 'nı varsayılan seçenekleri kullanarak tamamlayın ve sertifikayı **.cer** dosya adı uzantısıyla kaydedin.  

2.  Veritabanı çoğaltması sunucusunun otomatik imzalı sertifikasını yönetim noktasındaki güvenilir kişiler sertifika deposuna eklemek için yönetim noktası bilgisayarında aşağıdaki adımları gerçekleştirin:  

    1.  Yönetim noktası bilgisayarında Yönetim noktası bilgisayarında **sertifika** ek bileşeni MMC 'yi yapılandırmak için.  

    2.  Konsolda, **Sertifikalar (yerel Bilgisayar)**'ı genişletin, **Güvenilir Kişiler**'i genişletin, **Sertifikalar**'ı sağ tıklatın, **Tüm Görevler**'i seçin ve **İçeri Aktar**'ı tıklatarak **Sertifika Alma Sihirbazı**'nı başlatın.  

    3.  **İçeri Aktarılan Dosya** sayfasında, 1.h adımında kaydedilen sertifikayı seçin ve sonra **İleri**'yi tıklatın.  

    4.  **Sertifika Depolama Alanı** sayfasında, **Sertifika depolama alanı**seçeneği **Güvenilir Kişiler** 'e ayarlanmış olarak **Tüm sertifikaları aşağıdaki depolama alanına yerleştir**'i seçin ve **İleri**'yi tıklayın.  

    5.  Sihirbazı kapatmak ve yönetim noktasında sertifika yapılandırmasını tamamlamak için **Son** 'u tıklatın.  

###  <a name="step-5---configure-the-sql-server-service-broker-for-the-database-replica-server"></a><a name="BKMK_DBreplica_SSB"></a> Adım 5 - Veritabanı çoğaltma sunucusu için SQL Server Hizmet Aracısı'nı yapılandırma  
Bir yönetim noktası için veritabanı çoğaltmasıyla istemci bildirimini desteklemek için, site veritabanı sunucusuyla SQL Server Hizmet Aracısı için veritabanı çoğaltma sunucusu arasında iletişimi yapılandırmanız gerekir. Bu, her veritabanını diğer veritabanıyla ilgili bilgilerle yapılandırmanızı ve güvenli iletişim için iki veritabanı arasında sertifika takası yapmanızı gerektirir.  

> [!NOTE]  
>  Aşağıdaki yordamı kullanabilmeniz için önce, veritabanı çoğaltma sunucusunun site veritabanı sunucusuyla ilk eşitleme işlemini başarıyla tamamlaması gerekir.  

 Aşağıdaki yordam SQL Server'da site veritabanı sunucusu veya veritabanı çoğaltma sunucusu için yapılandırılan Hizmet Aracısı bağlantı noktasını değiştirmez. Bu yordam her veritabanını, doğru Hizmet Aracısı bağlantı noktasını kullanarak diğer veritabanıyla iletişim kuracak şekilde yapılandırır.  

 Site veritabanı sunucusu ve veritabanı çoğaltma sunucusu için Hizmet Aracısı'nı yapılandırmak için aşağıdaki yordamı kullanın.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>Bir veritabanı çoğaltması için hizmet aracısını yapılandırmak için  

1. Veritabanı çoğaltma sunucusu veritabanına bağlanmak için **SQL Server Management Studio** kullanın ve ardından veritabanı çoğaltma sunucusunda hizmet Aracısı etkinleştirmek için aşağıdaki sorguyu çalıştırın: **ALTER DATABASE &lt; replication Database Name \> set enable_broker, WITH Rollback ımwith HONOR_BROKER_PRIORITY**  

2. Ardından, veritabanı çoğaltma sunucusunda, Hizmet Aracısı'nı istemci bildirimi için yapılandırın ve Hizmet Aracısı sertifikasını dışarı aktarın. Bunu yapmak için, tek bir eylem Hizmet Aracısı'nı yapılandıran ve sertifikayı dışarı aktaran bir SQL Server saklı yordamını çalıştırın. Saklı yordamı çalıştırdığınızda, veritabanı çoğaltma sunucusunun FQDN'sini, veritabanı çoğaltmaları veritabanının adını belirtmeniz ve sertifika dosyasının dışarı aktarılacağı konumu belirtmeniz gerekir.  

    Veritabanı Çoğaltma sunucusunda gerekli ayrıntıları yapılandırmak ve veritabanı çoğaltma sunucusunun sertifikasını dışarı aktarmak için aşağıdaki sorguyu çalıştırın: **EXEC sp_BgbConfigSSBForReplicaDB ' &lt; çoğaltma SQL Server FQDN \> ', ' &lt; çoğaltma veritabanı adı \> ', ' &lt; sertifika yedekleme dosyası yolu \> '**  

   > [!NOTE]  
   >  Veritabanı çoğaltma sunucusu varsayılan SQL Server örneğinde değilse, bu adım için çoğaltma veritabanı adından başka örnek adını da belirtmeniz gerekir. Bunu yapmak için, ** &lt; çoğaltma veritabanı adı \> ** ' nı ** &lt; örnek adı \\ çoğaltma veritabanı adıyla \> **değiştirin.  

    Veritabanı çoğaltma sunucusundan sertifikayı dışarı aktardıktan sonra, sertifikanın bir kopyasını birincil siteler veritabanı sunucusuna yerleştirin.  

3. Birincil site veritabanına bağlanmak için **SQL Server Management Studio** 'yu kullanın. Birincil siteler veritabanına bağlandıktan sonra, sertifikayı içeri aktaracak ve veritabanı çoğaltma sunucunda kullanılan Hizmet Aracısı'nı, veritabanı çoğaltma sunucusunun FQDN'sini ve veritabanı çoğaltmaları veritabanının adını belirtecek bir sorgu çalıştırın. Bu, birincil site veritabanlarını, veritabanı çoğaltma sunucusunun veritabanıyla iletişim kurmak üzere Hizmet Aracısı'nı kullanacak şekilde yapılandırır.  

    Sertifikayı veritabanı çoğaltma sunucusundan almak ve gerekli ayrıntıları belirtmek için aşağıdaki sorguyu çalıştırın: **EXEC sp_BgbConfigSSBForRemoteService ' çoğaltma ', ' &lt; SQL Hizmet Aracısı bağlantı noktası \> ', ' &lt; sertifika dosyası yolu \> ', ' &lt; çoğaltma SQL Server FQDN \> ', ' &lt; çoğaltma veritabanı adı \> '**  

   > [!NOTE]  
   >  Veritabanı çoğaltma sunucusu varsayılan SQL Server örneğinde değilse, bu adım için çoğaltma veritabanı adından başka örnek adını da belirtmeniz gerekir. Bunu yapmak için, ** &lt; çoğaltma veritabanı adını \> ** **\ınstance Name \\ çoğaltma veritabanı adıyla \> **değiştirin.  

4. Ardından, site veritabanı sunucusunda, site veritabanı sunucusunun sertifikasını dışarı aktarmak için aşağıdaki komutu çalıştırın: **EXEC sp_BgbCreateAndBackupSQLCert ' &lt; sertifika yedekleme dosyası yolu \> '**  

    Site veritabanı sunucusundan sertifikayı dışarı aktardıktan sonra, sertifikanın bir kopyasını veritabanı çoğaltma sunucusuna yerleştirin.  

5. Veritabanı çoğaltma sunucusu veritabanına bağlanmak için **SQL Server Management Studio** 'yu kullanın. Veritabanı çoğaltma sunucusu veritabanına bağlandıktan sonra, sertifikayı içeri aktaracak ve birincil sitenin site kodunu ve site veritabanı sunucusunda kullanılan Hizmet Aracısı bağlantı noktasını belirtecek bir sorgu çalıştırın. Bu, veritabanı çoğaltma sunucusunu, birincil sitenin veritabanıyla iletişim kurmak üzere Hizmet Aracısı'nı kullanacak şekilde yapılandırır.  

    Sertifikayı site veritabanı sunucusundan içeri aktarmak için şu sorguyu çalıştırın: **EXEC sp_BgbConfigSSBForRemoteService ' &lt; site kodu \> ', ' &lt; SQL Hizmet Aracısı bağlantı noktası \> ', ' &lt; sertifika dosyası yolu \> '**  

   Site veritabanının ve veritabanı çoğaltma veritabanının yapılandırmasını tamamladıktan birkaç dakika sonra, birincil sitedeki bildirim yöneticisi birincil site veritabanından veritabanı çoğaltmaya istemci bildirimi için Hizmet Aracısı sohbeti ayarlar.  

###  <a name="supplemental-script-for-additional-database-replicas-on-a-single-sql-server"></a><a name="bkmk_supscript"></a> Tek bir SQL Server üzerinde ek veritabanı çoğaltmaları için ek komut dosyası  
 Kullanmaya devam etmeyi planladığınız bir veritabanı çoğaltmasına zaten sahip olan bir SQL Server veritabanı çoğaltması sunucusu için otomatik olarak imzalanan bir sertifika yapılandırmak üzere adım 4 ' teki komut dosyasını kullandığınızda, özgün betiğin değiştirilmiş bir sürümünü kullanmanız gerekir. Aşağıdaki değişiklikler, komut dosyasının sunucuda var olan bir sertifikayı silmesini engeller ve benzersiz Kolay adlarla sonraki sertifikaları oluşturur.  Özgün komut dosyasını aşağıdaki gibi düzenleyin:  

-   Komut dosyası girişleri arasındaki her bir satır için açıklama (çalıştırmayı engelle) **# var olan sertifikayı Sil** ve **# yeni sertifikayı oluştur**. Bunu yapmak için,  **#**  geçerli her satırın ilk karakteri olarak bir ekleyin.  

-   Yapılandırmak üzere bu komut dosyasını kullandığınız sonraki her veritabanı çoğaltması için sertifikanın Kolay adını güncelleştirin.  Bunu yapmak için $enrollment satırı düzenleyin **. CertificateFriendlyName = "ConfigMgr SQL Server kimlik sertifikası"** ve **ConfigMgr SQL Server kimlik sertifikasını**  **ConfigMgr SQL Server tanımlama Certificate1**gibi yeni bir adla değiştirin.  

##  <a name="manage-database-replica-configurations"></a><a name="BKMK_DBReplicaOps"></a> Veritabanı çoğaltması yapılandırmasını yönetme  
 Bir sitede veritabanı çoğaltması kullandığınızda, bir veritabanı çoğaltmasını kaldırma, veritabanı çoğaltması kullanan bir siteyi kaldırma veya site veritabanını yeni bir SQL Server yüklemesine taşıma sürecine katkı olarak aşağıdaki bölümlerde verilen bilgileri kullanın. Yayınları silmek üzere aşağıdaki bölümlerde verilen bilgileri kullanırken, veritabanı çoğaltması için kullandığınız SQL Server sürümü için işlem çoğaltmasını silme yönergelerini kullanın. Daha fazla bilgi için bkz. [yayını silme](/sql/relational-databases/replication/publish/delete-a-publication).  

> [!NOTE]  
>  Veritabanı çoğaltmaları için yapılandırılmış bir site veritabanını geri yükledikten sonra, veritabanı çoğaltmalarını kullanabilmek için her veritabanı çoğaltmasını yeniden yapılandırarak hem yayımları hem de abonelikleri tekrar oluşturmanız gerekir.  

###  <a name="uninstall-a-database-replica"></a><a name="BKMK_UninstallDbReplica"></a> Veritabanı çoğaltmasını kaldırma  
 Bir yönetim noktası için veritabanı çoğaltması kullanırken, veritabanı çoğaltmasını bir süreliğine kaldırıp, sonra kullanım için yeniden yapılandırmanız gerekebilir. Örneğin, bir Configuration Manager sitesini yeni bir hizmet paketine yükseltmeden önce veritabanı çoğaltmalarını kaldırmanız gerekir. Site yükseltmesi tamamlandıktan sonra, veritabanı çoğaltmasını kullanım için geri yükleyebilirsiniz.  

 Veritabanı çoğaltmasını kaldırmak için aşağıdaki adımları kullanın.  

1.  Configuration Manager konsolunun **Yönetim** çalışma alanında, **Site yapılandırması**' nı genişletin, **sunucular ve site sistemi rolleri**' ni seçin ve ardından Ayrıntılar bölmesinde, kaldırabileceğiniz veritabanı çoğaltmasını kullanan yönetim noktasını barındıran site sistem sunucusunu seçin.  

2.  **Site Sistemi Rolleri** bölmesinde, **Yönetim noktası** 'nı sağ tıklatıp **Özellikler**'i seçin.  

3.  **Yönetim Noktası Veritabanı** sekmesinde, yönetim noktasını veritabanı çoğaltması yerine site veritabanını kullanacak şekilde yapılandırmak için **Site veritabanını kullan** 'ı seçin. Ardından, yapılandırmayı kaydetmek için **Tamam** 'ı tıklatın.  

4.  Sonra, aşağıdaki görevleri gerçekleştirmek üzere **SQL Server Management Studio** 'yu kullanın:  

    -   Site sunucusu veritabanından veritabanı çoğaltmasının yayınını silin.  

    -   Veritabanı çoğaltma sunucusundan veritabanı çoğaltmasının aboneliğini silin.  

    -   Veritabanı çoğaltma sunucusundan çoğaltma veritabanını silin.  

    -   Site veritabanı sunucusunda yayınlama ve dağıtımı devre dışı bırakın. Yayımlamayı ve dağıtımı devre dışı bırakmak için, çoğaltma klasörüne sağ tıklayın ve ardından **yayımlamayı ve dağıtımı devre dışı bırak**' a tıklayın.  

5.  Site veritabanı sunucusunda yayını, aboneliği, çoğaltma veritabanını sildikten ve yayını devre dışı bıraktıktan sonra, veritabanı çoğaltması kaldırılır.  

###  <a name="uninstall-a-site-server-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Uninstall"></a> Veritabanı çoğaltması yayımlayan bir site sunucusunu kaldırma  
 Veritabanı çoğaltması yayınlayan bir siteyi kaldırmadan önce, aşağıdaki adımları kullanarak yayını ve tüm abonelikleri temizleyin.  

1.  Site sunucusu veritabanından veritabanı çoğaltma yayınını silmek için **SQL Server Management Studio** 'yu kullanın.  

2.  Bu site için bir veritabanı çoğaltması barındıran her uzak SQL Sunucusundan veritabanı çoğaltma aboneliğini silmek için **SQL Server Management Studio** 'yu kullanın.  

3.  Siteyi kaldırın.  

###  <a name="move-a-site-server-database-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Move"></a> Veritabanı çoğaltması yayımlayan bir site sunucusu veritabanını taşıma  
 Site veritabanını yeni bir bilgisayara taşıdığınızda, aşağıdaki adımları uygulayın:  

1.  Site sunucusu veritabanından veritabanı çoğaltmasının yayınını silmek için **SQL Server Management Studio** 'yu kullanın.  

2.  Bu sitenin her veritabanı sunucusundan veritabanı çoğaltmasının aboneliğini silmek için **SQL Server Management Studio** 'yu kullanın.  

3.  Veritabanını yeni SQL Server bilgisayarına taşıyın. Daha fazla bilgi için [Configuration Manager altyapınızı değiştirme](../../../../core/servers/manage/modify-your-infrastructure.md) konusundaki [site veritabanı yapılandırmasını değiştirme](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) bölümüne bakın.  

4.  Site veritabanı sunucusunda veritabanı çoğaltmasının yayınını yeniden oluşturun. Daha fazla bilgi için bu konuda bulunan [Adım 1 - Veritabanı çoğaltmasını Yayımlamak için site veritabanı sunucusunu yapılandırma](#BKMK_DBReplica_ConfigSiteDB) bölümüne bakın.  

5.  Her veritabanı çoğaltma sunucusunda veritabanı çoğaltmasının aboneliklerini yeniden oluşturun. Daha fazla bilgi için bu konudaki [Adım 2 - Veritabanı çoğaltma sunucusunu yapılandırma](#BKMK_DBReplica_ConfigSrv) bölümüne bakın.