---
title: Raporlamayı yapılandırma
titleSuffix: Configuration Manager
description: SQL Server Reporting Services hakkında bilgiler de dahil olmak üzere Configuration Manager hiyerarşinizde raporlama ayarlama.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b7ada6f54a7642817a321937a4d7128994d5538
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823988"
---
# <a name="configure-reporting-in-configuration-manager"></a>Configuration Manager raporlamayı yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager konsolunda rapor oluşturmadan, değiştirmeden ve çalıştırmadan önce, tamamlanacak birkaç yapılandırma görevi vardır. Configuration Manager hiyerarşinizde raporlamayı yapılandırmanıza yardımcı olması için bu makaleyi kullanın.  

Hiyerarşinizdeki SQL Server Reporting Services yükleyip yapılandırmadan önce, aşağıdaki Configuration Manager raporlama makalelerini gözden geçirin:  

- [Raporlamaya giriş](introduction-to-reporting.md)  

- [Raporlama planı](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services, farklı türlerde veri kaynakları için kapsamlı raporlama işlevselliği sağlayan sunucu tabanlı bir raporlama platformudur. Configuration Manager Raporlama Hizmetleri noktası SQL Server Reporting Services ile iletişim kurar:

- Configuration Manager raporlarını belirtilen rapor klasörüne kopyala
- Reporting Services ayarlarını yapılandırma
- Reporting Services güvenlik ayarlarını yapılandırma

Bir raporu çalıştırdığınızda, Raporlama Hizmetleri bileşeni verileri almak için Configuration Manager site veritabanına bağlanır.  

Raporlama Hizmetleri noktasını bir Configuration Manager sitesine yükleyebilmek için önce hedef site sistemine SQL Server Reporting Services yükleyip yapılandırın. Daha fazla bilgi için bkz. [ınstall SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).  

### <a name="verify-sql-server-reporting-services-installation"></a>SQL Server Reporting Services yüklemeyi doğrulama

SQL Server Raporlama Hizmetleri'nin doğru şekilde yüklenip çalıştığını doğrulamak için aşağıdaki prosedürü kullanın.

1. Site sisteminin **Başlat** menüsüne gidin ve **Raporlama Hizmetleri Configuration Manager**açın. Bunu **Microsoft SQL Server** grubunun **yapılandırma araçları** bölümünde bulabilirsiniz.

2. **Raporlama Hizmetleri yapılandırma bağlantısı** penceresinde, SQL Server Reporting Services barındıran sunucunun adını girin. SQL Raporlama Hizmetleri 'ni yüklediğiniz SQL Server örneğini seçin. Ardından, Raporlama Hizmetleri Configuration Manager açmak için **Bağlan** ' ı seçin.  

3. **Rapor sunucusu durumu** sayfasında **rapor hizmeti durumunun** **başlatıldığını**doğrulayın. Bu durumda değilse, **Başlat**' ı seçin.  

4. **Web hizmeti URL 'si** sayfasında, **rapor hizmeti Web hizmeti URL 'lerinde**URL 'yi seçin. Bu eylem rapor klasörüyle olan bağlantıyı sınar. Tarayıcı sizden kimlik bilgileri isteyebilir. Web sayfasının başarıyla açıldığını doğrulayın.

5. **Veritabanı** sayfasında **rapor sunucusu modunun** **Yerel**olarak ayarlandığını doğrulayın.  

6. **Url Rapor Yöneticisi** sayfasında, **Rapor Yöneticisi site kimliği**' nde URL 'yi seçin. Bu eylem Rapor Yöneticisi sanal diziniyle olan bağlantıyı sınar. Tarayıcı sizden kimlik bilgileri isteyebilir. Web sayfasının başarıyla açıldığını doğrulayın.

    > [!NOTE]  
    > Configuration Manager Raporlama Hizmetleri Rapor Yöneticisi gerektirmez. Yalnızca Rapor Yöneticisi kullanarak raporları tarayıcıda çalıştırmak veya raporları yönetmek istiyorsanız bu gereklidir.  

7. Reporting Services Configuration Manager kapatmak için **Çıkış** ' ı seçin.  

## <a name="configure-reporting-to-use-report-builder-30"></a>Raporlamayı Rapor Oluşturucusu kullanacak şekilde yapılandırın 3,0

1. Configuration Manager konsolunu çalıştıran bilgisayarda Windows kayıt defteri düzenleyicisini açın.  

2. `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting` adresine gidin.

3. Değer verilerini düzenlemek için **ReportBuilderApplicationManifestName** anahtarını açın.  

4. Değerini olarak değiştirin `ReportBuilder_3_0_0_0.application` ve ardından kaydetmek Için **Tamam** ' ı seçin.

5. Windows Kayıt Defteri Düzenleyiciyi kapatın.  

## <a name="install-a-reporting-services-point"></a> Bir raporlama hizmetleri noktası yükleme

Sitedeki raporları yönetmek için raporlama hizmetleri noktasını yükler. Raporlama Hizmetleri noktası:

- Rapor klasörlerini ve raporları SQL Server Reporting Services kopyalar
- Raporlar ve klasörler için güvenlik ilkesini uygular
- Raporlama hizmetlerindeki yapılandırma ayarlarını belirler

### <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar

Configuration Manager konsolundaki raporları görüntüleyebilmeniz veya yönetebilmeniz için önce bir Raporlama Hizmetleri noktasına ihtiyacınız vardır. Bu site sistem rolünü Microsoft SQL Server Reporting Services bir sunucuda yapılandırın. Daha fazla bilgi için bkz. [Raporlama önkoşulları](prerequisites-for-reporting.md).  

- Raporlama Hizmetleri noktasını yüklemek için bir site seçtiğinizde, raporlara erişecek kullanıcıların rolü yüklediğiniz siteyle aynı güvenlik kapsamında olması gerekir.  

- Bir site sistemine bir raporlama hizmetleri noktası yükledikten sonra, rapor sunucusu için URL 'YI değiştirmeyin.

    Örneğin, raporlama hizmetleri noktasını oluşturursunuz. Daha sonra Raporlama Hizmetleri Configuration Manager rapor sunucusu URL 'sini değiştirirsiniz. Configuration Manager konsolu eski URL 'YI kullanmaya devam eder. Konsoldan rapor çalıştıramazsınız, düzenleyemez veya oluşturamazsınız.

    Rapor sunucusu URL 'sini değiştirmeniz gerekiyorsa, önce mevcut raporlama hizmetleri noktasını kaldırın. URL 'YI değiştirin ve ardından raporlama hizmetleri noktasını yeniden yükleyin.  

- Bir raporlama hizmetleri noktası yüklediğinizde, bir [Raporlama Hizmetleri noktası hesabı](../../plan-design/hierarchy/accounts.md#reporting-services-point-account)belirtin. Farklı bir etki alanındaki kullanıcıların bir raporu çalıştırması için, etki alanları arasında çift yönlü bir güven oluşturun. Aksi takdirde rapor çalıştırılamaz.

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" />Raporlama Hizmetleri noktasını bir site sistemine yükler  

Site sistemlerini yapılandırma hakkında daha fazla bilgi için bkz. [site sistemi rollerini yüklemeyi](../deploy/configure/install-site-system-roles.md).  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve ardından **sunucular ve site sistemi rolleri** düğümünü seçin.  

1. Raporlama Hizmetleri noktasını yeni veya var olan bir site sistemi sunucusuna ekleyin:  

    - *Yeni site sistemi*: şeridin **giriş** sekmesinde, **Oluştur** grubunda, **site sistemi sunucusu oluştur**' u seçin. **Site Sistemi Sunucusu Oluşturma Sihirbazı** açılır.  

    - *Var olan site sistemi*: hedef sunucuyu seçin. Şeridin **giriş** sekmesinde, **sunucu** grubunda, **site sistemi rolü Ekle**' yi seçin. **Site Sistemi Rolleri Ekleme Sihirbazı** açılır.  

1. **Genel** sayfasında, site sistemi sunucusu için genel ayarları belirtin. Raporlama Hizmetleri noktasını var olan bir sunucuya eklediğinizde, daha önce yapılandırdığınız değerleri doğrulayın.  

1. **Sistem rolü seçimi** sayfasında, kullanılabilir roller listesinden **Raporlama Hizmetleri noktası** ' nı seçin ve ardından **İleri**' yi seçin.  

1. **Raporlama Hizmetleri noktası** sayfasında, aşağıdaki ayarları yapılandırın:  

    - **Site veritabanı sunucu adı**: Configuration Manager site veritabanını barındıran sunucunun adını belirtin. Sihirbaz genellikle sunucu için tam etki alanı adını (FQDN) alır. Bir veritabanı örneği belirtmek için, &lt; *sunucu adı*, > \& lt;* biçimini kullanın. örnek adı*>. Örneğin, `sqlserver\named1`.

    - **Veritabanı adı**: Configuration Manager site veritabanı adını belirtin. Sihirbazın site veritabanına erişimi olduğunu doğrulamak için **Doğrula** ' yı seçin.  

        > [!IMPORTANT]  
        > Raporlama Hizmetleri noktasını oluşturmak için kullandığınız kullanıcı hesabı, site veritabanına **okuma** erişimine sahip olmalıdır. Bağlantı testi başarısız olursa, kırmızı bir uyarı simgesi görüntülenir. Simgenin üzerindeki bağlamsal vurgu metninde hatanın ayrıntıları bulunur. Hatayı düzeltip yeniden **Test** et ' i seçin.  

    - **Klasör adı**: Raporlama hizmetleri 'nde Configuration Manager raporları için oluşturulacak ve kullanılacak klasör adını belirtin.  

    - **Reporting Services sunucu örneği**: Reporting services için SQL Server örneğini seçin. Bu sayfa herhangi bir örnek listemezse, SQL Server Reporting Services yüklendiğini, yapılandırıldığını ve başlatıldığını doğrulayın.  

        > [!IMPORTANT]  
        > Configuration Manager, geçerli kullanıcı bağlamında Seçili site sistemindeki WMI 'ya bir bağlantı yapar. Raporlama Hizmetleri için SQL Server örneğini almak üzere bu bağlantıyı kullanır. Geçerli Kullanıcı, site sistemindeki WMI 'ya **okuma** erişimine sahip olmalıdır veya sihirbaz, Reporting Services örneklerini alamıyor.  

    - **Raporlama Hizmetleri noktası hesabı**: **Ayarla**' yı seçin ve ardından kullanılacak hesabı seçin. Raporlama Hizmetleri noktasındaki SQL Server Reporting Services, Configuration Manager site veritabanına bağlanmak için bu hesabı kullanır. Bu bağlantı, bir rapor için verileri almak içindir. Daha önce Configuration Manager hesabı olarak yapılandırdığınız bir Windows Kullanıcı hesabını belirtmek için **Mevcut hesap** ' ı seçin. Şu anda kullanılmak üzere yapılandırılmamış bir Windows Kullanıcı hesabı belirtmek için **Yeni hesap** ' ı seçin. Configuration Manager, belirtilen kullanıcının site veritabanına erişimini otomatik olarak verir.  

        Raporlama Hizmetleri 'ni çalıştıran hesap, etki alanı yerel güvenlik grubu **Windows yetkilendirme erişim grubuna**ait olmalıdır. Bu, hesap, etki alanı içindeki tüm Kullanıcı nesneleri için **TokenGroupsGlobalAndUniversal** özniteliğinde **Okuma izinlerine izin** verir. Raporlama Hizmetleri noktası hesabından farklı bir etki alanındaki kullanıcılar, raporları başarıyla çalıştırmak için etki alanları arasında çift yönlü bir güvene ihtiyaç duyar.

        Belirtilen Windows kullanıcı hesabı ve parolası şifrelenir ve Raporlama Hizmetleri veritabanında saklanır. Raporlama Hizmetleri bu hesabı ve parolayı kullanarak raporlarla ilgili verileri site veritabanından alır.  

        > [!IMPORTANT]  
        > Belirttiğiniz hesap, Raporlama Hizmetleri veritabanını barındıran sunucuda **yerel olarak oturum** aç iznine sahip olmalıdır.  

1. Sihirbazı tamamlayın.

Sihirbaz tamamlandıktan sonra, Configuration Manager Raporlama Hizmetleri 'nde rapor klasörlerini oluşturur. Daha sonra raporlarını belirtilen rapor klasörlerine kopyalar.  

> [!TIP]  
> Yalnızca raporlama hizmetleri noktası site rolünü barındıran site sistemlerini listelemek için, **sunucular ve site sistem rolleri**' ne sağ tıklayın ve **Raporlama Hizmetleri noktası**' nı seçin.  

### <a name="languages-for-reports"></a><a name="bkmk_languages" />Raporlar için Diller

<!-- SCCMDocs#1067 -->

Configuration Manager rapor klasörleri oluşturduğunda ve raporları rapor sunucusuna kopyaladığında, nesneler için uygun dili belirler.

- Rapor klasörleri oluşturma, raporları kopyalama

  - Site sunucusu işletim sisteminin yerel ayarını kullanarak nesne oluşturma

  - Belirli dil paketi kullanılamıyorsa, varsayılan olarak Ingilizce (TRK)

- Raporları bir Web tarayıcısında görüntüleme

  - Klasör ve rapor adları: site sunucusuyla aynı yerel ayar
  
  - Rapor içerikleri: tarayıcı yerel ayarına göre dinamik

- Configuration Manager konsolundaki raporları görüntüleme

  - Klasör ve rapor adları: konsolun yerel ayarına bağlı olarak dinamik
  
  - Rapor içerikleri: konsolun yerel ayarına bağlı olarak dinamik

Bir raporlama hizmetleri noktasını dil paketlerine sahip olmayan bir siteye yüklediğinizde, raporlar İngilizce yüklenir. Raporlama hizmetleri noktasını yükledikten sonra bir dil paketi yüklerseniz, raporların uygun dil paketi dilinde kullanılabilir olması için raporlama hizmetleri noktasını kaldırıp yeniden yüklemeniz gerekir.  

Daha fazla bilgi için bkz. [dil paketleri](../deploy/install/language-packs.md).

### <a name="file-installation-and-report-folder-security-rights"></a> Dosya yükleme ve rapor klasörü güvenlik hakları

Configuration Manager, raporlama hizmetleri noktasını yüklemek ve Raporlama Hizmetleri 'ni yapılandırmak için aşağıdaki eylemleri yapar:  

> [!IMPORTANT]  
> Site, bu eylemleri SMS_Executive hizmeti için yapılandırılan hesap bağlamında yapar. Genellikle bu hesap, site sunucusu yerel sistem hesabıdır.  

- Raporlama Hizmetleri noktası site rolünü yükler.  

- Raporlama Hizmetleri 'nde, sihirbazda belirttiğiniz depolanan kimlik bilgileriyle veri kaynağını oluşturun. Bu hesap, raporları çalıştırdığınızda Raporlama Hizmetleri 'nin site veritabanına bağlanmak için kullandığı Windows Kullanıcı hesabı ve parolasıdır.  

- Raporlama Hizmetleri 'nde Configuration Manager kök klasörünü oluşturun.  

- **ConfigMgr rapor kullanıcıları** ve **ConfigMgr rapor yöneticileri** güvenlik rollerini Raporlama Hizmetleri 'ne ekleyin.  

- Alt klasörler oluşturun ve `%ProgramFiles%\SMS_SRSRP` site sunucusundan Raporlama Hizmetleri 'ne Configuration Manager raporlarını dağıtın.  

- Raporlama Hizmetleri 'ndeki **ConfigMgr rapor kullanıcıları** rolünü, Configuration Manager **site okuma** haklarına sahip tüm Kullanıcı hesaplarının kök klasörlerine ekleyin.  

- Raporlama Hizmetleri 'ndeki **ConfigMgr rapor yöneticileri** rolünü, Configuration Manager **site değiştirme** haklarına sahip tüm Kullanıcı hesaplarının kök klasörlerine ekleyin.  

- Rapor klasörleri ve Configuration Manager güvenli nesne türleri arasındaki eşlemeyi alın. Configuration Manager, bu haritanın site veritabanında bakımını sağlar.  

- Raporlama Hizmetleri 'nde belirli rapor klasörlerine Configuration Manager yönetici kullanıcılar için aşağıdaki hakları yapılandırın:  

  - Kullanıcı ekleyin ve **ConfigMgr rapor kullanıcıları** rolünü, Configuration Manager nesnesi Için **rapor çalıştırma** izinlerine sahip yönetici kullanıcıların ilişkili rapor klasörüne atayın.  

  - Kullanıcıları ekleyin ve **ConfigMgr rapor yöneticileri** rolünü, Configuration Manager nesnesi Için **Raporu Değiştir** izinlerine sahip yönetici kullanıcıların ilişkili rapor klasörüne atayın.  

Configuration Manager, Raporlama Hizmetleri 'ne bağlanır ve Configuration Manager ve Raporlama Hizmetleri kök klasörleri ve belirli rapor klasörlerinde kullanıcıların izinlerini ayarlar. Raporlama Hizmetleri noktasının ilk yüklemesinden sonra, rapor klasörlerinde yapılandırılan kullanıcı haklarının Configuration Manager kullanıcılar için ayarlanan ilişkili haklar olduğunu doğrulamak üzere her 10 dakikada bir Raporlama Hizmetlerine bağlanır Configuration Manager. Raporlama Hizmetleri Rapor Yöneticisi kullanılarak kullanıcılar eklendiğinde veya Kullanıcı hakları değiştirildiğinde, Configuration Manager site veritabanında depolanan rol tabanlı atamaları kullanarak bu değişiklikleri geçersiz kılar. Configuration Manager ayrıca, Configuration Manager raporlama hakları olmayan kullanıcıları da kaldırır.  

### <a name="reporting-services-security-roles"></a>Reporting Services güvenlik rolleri

Configuration Manager, raporlama hizmetleri noktasını yüklediğinde, Raporlama Hizmetleri 'ne aşağıdaki güvenlik rollerini ekler:  

- **ConfigMgr rapor kullanıcıları**: Bu güvenlik rolüyle atanan kullanıcılar yalnızca Configuration Manager raporlarını çalıştırabilir.  

- **ConfigMgr rapor yöneticileri**: Bu güvenlik rolüyle atanan kullanıcılar, Configuration Manager raporlamayla ilgili tüm görevleri gerçekleştirebilir.  

## <a name="verify-installation"></a><a name="bkmk_verify"></a>Yüklemeyi doğrula

Belirli durum iletilerine ve günlük dosyası girişlerine bakarak Raporlama Hizmetleri noktası yüklemesini doğrulayın. Raporlama hizmetleri noktası yüklemesinin başarılı olduğunu doğrulamak için aşağıdaki yordamı kullanın.  

> [!Note]  
> Configuration Manager konsolundaki **izleme** çalışma alanındaki **Raporlama** düğümünün **raporlar** alt klasöründe raporlar görürseniz, bu yordamı atlayabilirsiniz.

### <a name="verify-installation-by-status-message"></a>Yüklemeyi durum iletisine göre doğrula

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **sistem durumu**' nu genişletin ve **Bileşen durumu** düğümünü seçin.  

1. **SMS_SRS_REPORTING_POINT** bileşeni seçin.  

1. Şeridin **giriş** sekmesinde, **bileşen** grubunda, **iletileri göster**' i seçin ve sonra **Tümü**' nü seçin.  

1. Raporlama Hizmetleri noktasını yüklemeden önce bir dönem için tarih ve saat belirtin ve ardından **Tamam**' ı seçin.  

1. Durum iletisi KIMLIĞINI doğrulayın **1015**. Bu durum iletisi, Raporlama Hizmetleri noktasının başarıyla yüklendiğini gösterir.

### <a name="verify-installation-by-log-file"></a>Yüklemeyi günlük dosyasına göre doğrula

Configuration Manager yükleme yolunun **logs** dizininde bulunan **Srsrp. log** dosyasını açın. Dizeyi bulun `Installation was successful` .

Bu günlük dosyasında, Raporlama Hizmetleri noktasının başarıyla yüklendiği zamandan itibaren ilerleyin. Rapor klasörlerinin oluşturulduğunu, raporların dağıtıldığını ve her klasördeki güvenlik ilkesinin onaylandığını doğrulayın. Güvenlik ilkesi teyitlerinin son satırından sonra, dizeyi arayın `Successfully checked that the SRS web service is healthy on server` .  

## <a name="configure-a-certificate-to-author-reports"></a>Raporları yazmak için bir sertifika yapılandırma

SQL Server Reporting Services raporları yazmak için kullanabileceğiniz birçok seçenek vardır. Configuration Manager konsolunda raporlar oluşturduğunuzda veya düzenlediğinizde, Configuration Manager yazma ortamı olarak kullanmak üzere Rapor Oluşturucusu açılır. Configuration Manager raporlarınızı nasıl yazarlarından bağımsız olarak, site veritabanı sunucusuna sunucu kimlik doğrulaması için otomatik olarak imzalanan bir sertifikaya ihtiyacınız vardır.

> [!NOTE]  
> SQL Server Reporting Services rapor yazma hakkında daha fazla bilgi için bkz. [Rapor Oluşturucusu yazma ortamı](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs).  

Configuration Manager, sertifikayı site sunucusuna ve SMS sağlayıcı rollerine otomatik olarak yüklenir. Bu sunuculardan birini çalıştırdığınızda Configuration Manager konsolundan raporlar oluşturabilir veya düzenleyebilirsiniz.

Farklı bir bilgisayardaki Configuration Manager konsolundan rapor oluştururken veya değiştirirken, sertifikayı site sunucusundan dışarı aktarın. Belirli bir sertifikanın kolay adı, yerel bilgisayar için **güvenilir kişiler** sertifika deposundaki site sunucusunun FQDN 'sidir. Bu sertifikayı Configuration Manager konsolunu çalıştıran bilgisayardaki **güvenilir kişiler** sertifika deposuna ekleyin.  

## <a name="modify-reporting-services-point-settings"></a>Raporlama Hizmetleri noktası ayarlarını değiştirme

Bu rolü yükledikten sonra, Raporlama Hizmetleri noktası özelliklerinde site veritabanı bağlantısını ve kimlik doğrulama ayarlarını değiştirebilirsiniz.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve ardından **sunucular ve site sistemi rolleri** düğümünü seçin.  

    > [!TIP]  
    > Yalnızca raporlama hizmetleri noktasını barındıran site sistemlerini listelemek için, **sunucular ve site sistemi rolleri** düğümüne sağ tıklayın ve **Raporlama Hizmetleri noktası**' nı seçin.  

1. Raporlama Hizmetleri noktasını barındıran site sistemini seçin. Daha sonra Ayrıntılar bölmesinde **raporlama hizmet noktası** site sistemi rolleri ' ni seçin.

1. Şerit 'in **site rolü** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

1. **Raporlama Hizmetleri noktası özelliklerinde**aşağıdaki ayarları değiştirebilirsiniz:  

    - **Site veritabanı sunucu adı**

    - **Veritabanı adı**

    - **Kullanıcı hesabı**

1. Değişiklikleri kaydetmek ve özellikleri kapatmak için **Tamam** ' ı seçin.  

Bu ayarlar hakkında daha fazla bilgi için, [Raporlama Hizmetleri noktasını bir site sistemine yüklemek](#bkmk_install)üzere bölümündeki açıklamalara bakın.

## <a name="power-bi-report-server"></a>Power BI Rapor Sunucusu

Sürüm 2002 ' den başlayarak raporlamayı Power BI Rapor Sunucusu ile tümleştirebilirsiniz. Yapılandırma hakkında daha fazla bilgi için bkz. [Power BI rapor sunucusu tümleştirme](powerbi-report-server.md).

## <a name="upgrade-sql-server"></a>SQL Server yükselt

SQL Server ve SQL Server Reporting Services yükseltmek için önce, siteden raporlama hizmetleri noktasını kaldırın. SQL Server yükselttikten sonra, raporlama hizmetleri noktasını Configuration Manager yeniden yükleyin.

Bu işlemi izlemeden, Configuration Manager konsolundan raporları çalıştırdığınızda veya düzenlerken hatalar görürsünüz. Raporları bir Web tarayıcısından başarıyla çalıştırmaya ve düzenlemeye devam edebilirsiniz.  

## <a name="configure-report-options"></a>Rapor seçeneklerini yapılandırma

Raporları yönetmek için kullandığınız varsayılan raporlama hizmetleri noktasını seçebilirsiniz. Site birden fazla Raporlama Hizmetleri noktasına sahip olabilir, ancak yalnızca varsayılan sunucuyu raporlarını yönetmek için kullanır. Sitenizin rapor seçeneklerini yapılandırmak için aşağıdaki yordamı kullanın.  

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin.  

1. Şeridin **giriş** sekmesinde, **Ayarlar** grubunda, **rapor seçenekleri**' ni seçin.  

1. Listeden varsayılan rapor sunucusunu seçin ve ardından **Tamam**' ı seçin.

Herhangi bir sunucu görünmüyorsa, sitede bir raporlama hizmetleri noktası yükleyip yapılandırdığınızdan emin olun. Daha fazla bilgi için bkz. [Yüklemeyi doğrulama](#bkmk_verify).

Bilgisayarınızda, rapor sunucunuz için kullandığınız SQL Server sürümü ile eşleşen bir SQL Server Rapor Oluşturucusu sürümü çalıştığından emin olun. Aksi halde bir hata görürsünüz, varsayılan rapor sunucusu kaydedilmez ve rapor oluşturamaz veya düzenleyemezsiniz.<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>Sonraki adımlar

[Raporlamaya yönelik işlemler ve bakım](operations-and-maintenance-for-reporting.md)
