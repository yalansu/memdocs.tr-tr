---
title: Veri ambarı
titleSuffix: Configuration Manager
description: Configuration Manager için veri ambarı hizmet noktası ve veritabanı
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d5ff011c0d25e601ff6605edb49383e58f949203
ms.sourcegitcommit: 1edcfb3ce4350ba1a6f36a6150e86301d35c631b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86390900"
---
# <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Configuration Manager için veri ambarı hizmet noktası

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1277922-->
Configuration Manager dağıtımınız için uzun süreli geçmiş verileri depolamak ve raporlamak için veri ambarı hizmet noktasını kullanın.

> [!NOTE]
> Sürüm 1910 ' de, Configuration Manager Bu özelliği varsayılan olarak sunar. Sürüm 1906 veya önceki sürümlerde, bu isteğe bağlı özelliği varsayılan olarak etkinleştirmez Configuration Manager. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](install-in-console-updates.md#bkmk_options).<!--505213-->

Veri ambarı, değişiklik izleme zaman damgalarına sahip 2 TB 'a kadar veriyi destekler. Veri ambarı, verileri Configuration Manager site veritabanından veri ambarı veritabanına otomatik olarak eşitleyerek verileri depolar. Bu bilgilere daha sonra raporlama hizmet noktanınızdan erişilebilir. Veri ambarı veritabanıyla eşitlenen veriler üç yıl boyunca tutulur. Düzenli aralıklarla, yerleşik bir görev üç yıldan eski olan verileri kaldırır.

Eşitlenen veriler, genel veri ve site veri gruplarından şunları içerir:

- Altyapı durumu
- Güvenlik
- Uyumluluk
- Kötü Amaçlı Yazılımlar
- Yazılım dağıtımları
- Envanter ayrıntıları (ancak, stok geçmişi eşitlenmemiş)

Site sistemi rolü yüklediğinde, veri ambarı veritabanını yükleyip yapılandırır. Ayrıca, bu verileri kolayca arayabilmeniz ve rapor edebilmeniz için çeşitli raporlar da yüklenir.

## <a name="prerequisites"></a>Önkoşullar

- Veri ambarı site sistemi rolü yalnızca hiyerarşinizin üst katman sitesinde desteklenir. Örneğin, bir merkezi yönetim sitesi (CAS) veya tek başına birincil site.

- Site sistemi rolünü yüklediğiniz bilgisayar .NET Framework 4.5.2 veya üstünü gerektirir.

- **Raporlama Hizmetleri noktası hesabına** veri ambarı veritabanında **db_datareader** iznini verin.

- Veri ambarı veritabanı ile verileri eşzamanlı hale getirmek için Configuration Manager, site sistem rolünün bilgisayar hesabını kullanır. Bu hesap aşağıdaki izinleri gerektirir:

  - Veri ambarı veritabanını barındıran bilgisayarda **yönetici** .

  - Veri ambarı veritabanında **DB_Creator** izni.

  - **DB_owner** veya üst katman sitenin veritabanına yönelik **yürütme** izinlerine sahip **DB_reader** .

- Veri ambarı veritabanı, SQL Server 2012 veya üzeri bir sürümü gerektirir. Sürüm Standard, Enterprise veya Datacenter olabilir. Veri ambarının SQL Server sürümünün site veritabanı sunucusuyla aynı olması gerekmez.<!--SCCMDocs issue 662-->

- Ambar veritabanı aşağıdaki SQL Server konfigürasyonları destekler:

  - Varsayılan veya adlandırılmış örnek

  - SQL Server Always on kullanılabilirlik grubu

  - SQL Server yük devretme kümesi

- [Dağıtılmış görünümler](../../plan-design/hierarchy/database-replication.md#bkmk_distviews)kullanıyorsanız, veri ambarı HIZMET noktasını CAS veritabanını barındıran aynı sunucuya yükleyebilirsiniz.

SQL Server Lisanslama hakkında daha fazla bilgi için bkz. [ürün ve lisanslama hakkında SSS](../../understand/product-and-licensing-faq.md).<!-- sms500967 -->

Veri ambarı veritabanını, site veritabanınızla aynı şekilde boyutlandırın. Veri ambarı ilk başta daha küçük olsa da zaman içinde büyüyecektir. <!--SCCMDocs issue 756-->

## <a name="install"></a>Yükleme

Her hiyerarşi, en üst katman sitenin herhangi bir site sisteminde bu rolün tek bir örneğini destekler. Ambar için veritabanını barındıran SQL Server, site sistem rolü veya uzak için yerel olabilir. Veri ambarı, aynı sitede yüklü olan Raporlama Hizmetleri noktasıyla birlikte kullanılabilir. İki site sistem rolünü aynı sunucuya yüklemeniz gerekmez.

Rolü yüklemek için, **site sistemi rolleri ekleme Sihirbazı** ' nı veya **site sistemi sunucusu oluşturma Sihirbazı**' nı kullanın. Daha fazla bilgi için bkz. [site sistemi rollerini yüklemeyi](../deploy/configure/install-site-system-roles.md). Sihirbazın **sistem rolü seçimi** sayfasında, **veri ambarı hizmet noktası** rolünü seçin.

Rolü yüklediğinizde Configuration Manager, belirttiğiniz SQL Server örneğinde sizin için veri ambarı veritabanını oluşturur. Var olan bir veritabanının adını belirtirseniz Configuration Manager yeni bir veritabanı oluşturmaz. Bunun yerine, belirttiğiniz birini kullanır. Bu işlem, [veri ambarı veritabanını yeni bir SQL Server taşırken](#move-the-database)olduğu gibidir.

### <a name="configure-properties"></a>Özellikleri Yapılandır

#### <a name="general-page"></a>Genel sayfa

- **Tam etki alanı adı SQL Server**: veri ambarı hizmet noktası veritabanını barındıran sunucunun tam etki alanı adını (FQDN) belirtin.

- **SQL Server örnek adı uygunsa**: varsayılan bir SQL Server örneği kullanmıyorsanız, adlandırılmış örneği belirtin.

- **Veritabanı adı**: veri ambarı veritabanı için bir ad belirtin. Configuration Manager, bu adla veri ambarı veritabanını oluşturur. SQL Server örneğinde zaten var olan bir veritabanı adı belirtirseniz, Configuration Manager Bu veritabanını kullanır.

- **Bağlantı için kullanılan SQL Server bağlantı noktası**: veri ambarı veritabanını barındıran SQL Server tarafından kullanılan TCP/IP bağlantı noktası numarasını belirtin. Veri ambarı eşitleme hizmeti, veri ambarı veritabanına bağlanmak için bu bağlantı noktasını kullanır. Varsayılan olarak, iletişim için **1433** SQL Server bağlantı noktasını kullanır.

- **Veri ambarı hizmet noktası hesabı**: SQL Server Reporting Services veri ambarı veritabanına bağlanırken kullandığı **Kullanıcı adını** ayarlayın.

#### <a name="synchronization-settings-page"></a>Eşitleme ayarları sayfası

- **Veri eşitleme özel ayarı**: **tabloları seçme**seçeneğini belirleyin. Veritabanı tabloları penceresinde, veri ambarı veritabanıyla eşitlenmek üzere tablo adlarını seçin. Ada göre aramak için filtreyi kullanın veya belirli grupları seçmek için açılan listeyi seçin. Kaydetmek için tamamlandığında **Tamam ' ı** seçin.

    > [!NOTE]
    > Rolün varsayılan olarak seçtiği tabloları kaldıramazsınız.

- **Başlangıç zamanı**: veri ambarı eşitlemesinin başlamasını istediğiniz saati belirtin.

- **Yinelenme dönemi**

  - **Günlük**: eşitlemenin her gün çalışacağını belirtin.

  - **Haftalık**: her hafta tek bir gün ve eşitleme için Haftalık yinelenme belirtin.

## <a name="reporting"></a>Raporlama

Bir veri ambarı hizmet noktası yükledikten sonra, site için Raporlama Hizmetleri noktasında birkaç rapor kullanılabilir hale gelir. Bir raporlama hizmetleri noktası yüklemeden önce veri ambarı hizmet noktasını yüklerseniz, raporlama hizmetleri noktasını daha sonra yüklediğinizde raporlar otomatik olarak eklenir.

> [!NOTE]
> Veri ambarı noktası alternatif kimlik bilgilerini destekler.<!--507334--> SQL Server Reporting Services veri ambarı veritabanına bağlanmak için kullandığı kimlik bilgilerini belirtin. Veri ambarı raporları, kimlik bilgileri eklenene kadar açılmaz.
>
> Hesap belirtmek için, rol özelliklerindeki veri ambarı hizmet noktası hesabı için **Kullanıcı adı** ' nı ayarlayın. Daha fazla bilgi için bkz. [özellikleri yapılandırma](#configure-properties).

Veri ambarı site sistemi rolü, **veri ambarı** kategorisi altında aşağıdaki raporları içerir:

- **Uygulama dağıtımı-geçmiş**: belirli bir uygulama ve makine için uygulama dağıtımına ilişkin ayrıntıları görüntüleyin.

- **Endpoint Protection ve yazılım güncelleştirme uyumluluğu-geçmiş**: eksik yazılım güncelleştirmeleri olan bilgisayarları görüntüleyin.

- **Genel donanım envanteri-geçmiş**: belirli bir makine için tüm donanım envanterini görüntüleyin.

- **Genel yazılım envanteri-geçmiş**: belirli bir makine için tüm yazılım envanterini görüntüleyin.

- **Altyapı durumu genel bakış-geçmiş**: Configuration Manager altyapınızın sistem durumuna genel bir bakış görüntüler.

- **Algılanan kötü amaçlı yazılım listesi-geçmiş**: kuruluşta algılanan kötü amaçlı yazılımları görüntüleyin.

- **Yazılım dağıtımı Özeti-geçmiş**: belirli bir tanıtım ve makine için yazılım dağıtımının bir özeti.

## <a name="site-expansion"></a>Site genişletmesi

Mevcut bir tek başına birincil siteyi genişletmek için bir CA yüklemeden önce, önce veri ambarı hizmet noktası rolünü kaldırın. CA 'ları yükledikten sonra, CA 'larda site sistem rolünü yükleyebilirsiniz.

Veri ambarı veritabanının taşınmasına farklı olarak, bu değişiklik daha önce birincil sitede eşitlediğiniz geçmiş verilerin kaybedilmesine neden olur. Birincil siteden veritabanını yedeklemek ve CA 'lara geri yüklemek desteklenmez.

## <a name="move-the-database"></a>Veritabanını taşıma

Veri ambarı veritabanını yeni bir SQL Server taşımak için aşağıdaki adımları kullanın:

1. Veri ambarı veritabanını yedeklemek için SQL Server Management Studio kullanın. Daha sonra bu veritabanını, veri ambarını barındıran yeni bilgisayardaki bir SQL Server geri yükleyin.

    > [!NOTE]
    > Veritabanını yeni sunucuya geri yükledikten sonra, veritabanı erişim izinlerinin özgün veri ambarı veritabanında olduğu gibi yeni veri ambarı veritabanında aynı olduğundan emin olun.

2. Geçerli sunucudan veri ambarı hizmet noktası rolünü kaldırmak için Configuration Manager konsolunu kullanın.

3. Veri ambarı hizmet noktasını yeniden yükleyin. Geri yüklenen veri ambarı veritabanını barındıran yeni SQL Server ve örneğin adını belirtin.

4. Site sistemi rolü yüklendikten sonra taşıma işlemi tamamlanır.

## <a name="troubleshoot"></a>Sorun giderme

### <a name="log-files"></a>Günlük dosyaları

Veri ambarı hizmet noktası yüklemesiyle ilgili sorunları araştırmak veya verilerin eşitlenmesi için aşağıdaki günlükleri kullanın:

- **Dwssmsı. log** ve **dwsssetup. log**: veri ambarı hizmet noktasını yüklerken hataları araştırmak için bu günlükleri kullanın.

- **MgrDataWarehouse. logMicrosoft.Config**: Bu günlüğü, site veritabanı arasındaki veri ambarı veritabanına veri eşitlemesini araştırmak için kullanın.

### <a name="set-up-failure"></a>Hata ayarlama

Veri ambarı hizmet noktası rolü, uzak bir sunucuya yüklediğiniz ilk sunucu olduğunda, veri ambarı için yükleme başarısız olur.  

Bu sorunu geçici olarak çözmek için, veri ambarı hizmet noktasını yüklediğiniz bilgisayarın, en az bir başka rol barındırtığından emin olun.

### <a name="synchronization-failed-to-populate-schema-objects"></a>Eşitleme, şema nesnelerini dolduramadı

Eşitleme, **Microsoft.ConfigMgrDataWarehouse. log**dosyasında aşağıdaki iletiyle başarısız olur:`failed to populate schema objects`

Bu sorunu geçici olarak çözmek için, site sistem rolünün bilgisayar hesabının, veri ambarı veritabanında bir **db_owner** olduğundan emin olun.

### <a name="reports-fail-to-open"></a>Raporlar açılamıyor

Veri ambarı raporları, veri ambarı veritabanı ve raporlama hizmeti noktası farklı site sistemlerlerde olduğunda açılmaz.

Bu sorunu geçici olarak çözmek için, **Raporlama Hizmetleri noktası hesabına** veri ambarı veritabanında **db_datareader** iznini verin.

### <a name="error-opening-reports"></a>Raporlar açılırken hata oluştu

Bir veri ambarı raporu açtığınızda, şu hatayı döndürür:

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

Bu sorunu geçici olarak çözmek için, sertifikaları yapılandırmak için aşağıdaki adımları kullanın:

1. Veri ambarı veritabanını barındıran sunucuda:

    1. Kendinden imzalı bir sertifika oluşturun. IIS 'yi açın, **sunucu sertifikaları**' nı seçin ve ardından **otomatik olarak imzalanan sertifika oluştur** eylemini seçin. Sertifika adının "kolay adı" nı **veri ambarı SQL Server kimlik sertifikası**olarak belirtin. Sertifika deposunu **Kişisel**olarak seçin.

      > [!TIP]
      > Bu sunucuda zaten IIS yoksa, önce bunu yüklemeniz gerekir.

    1. Sertifikayı yönetin. Microsoft Yönetim Konsolu 'Nu (MMC) açın ve **Sertifikalar** ek bileşenini ekleyin. Yerel makinenin **bilgisayar hesabını** seçin. **Kişisel** klasörünü genişletin ve **Sertifikalar**' ı seçin.

        1. Sertifika için SQL Server hizmet hesabına okuma izinleri verin. **Veri ambarı SQL Server kimlik sertifikası** sertifikası ' nı seçin, sonra **eylem** menüsüne gidin, **Tüm görevler**' i seçin ve **özel anahtarları Yönet**' i seçin. SQL Server hizmeti hesabını ekleyin ve **okuma** izni verin.<!-- SCCMDocs#1805 -->

        1. **Veri ambarı SQL Server kimlik sertifikasını** **der kodlu bir ikili X. 509.440 (.) olarak dışarı aktarın. CER)** dosyası.

    1. SQL 'i yeniden yapılandırın. **SQL Server Configuration Manager**’ı açın.

        1. **SQL Server ağ yapılandırması**altında, **MSSQLSERVER protokolleri**altındaki **özellikleri** seçmek için sağ tıklayın. **Sertifika** sekmesine geçin, sertifika olarak **veri ambarı SQL Server kimlik sertifikası** ' nı seçin ve ardından değişiklikleri kaydedin.

        1. **SQL Server hizmetler**' in altında **SQL Server hizmetini**yeniden başlatın. Veri ambarı veritabanını barındıran sunucuda SQL Raporlama Hizmetleri de yüklüyse, **Raporlama hizmeti** hizmetlerini de yeniden başlatın.

1. SQL Server Reporting Services barındıran sunucuda, MMC 'yi açın ve **Sertifikalar** ek bileşenini ekleyin. **Bilgisayar hesabı**' nı seçin. **Güvenilen kök sertifika yetkilileri** klasörü altında, **veri ambarını SQL Server kimlik sertifikasını**içeri aktarın.

## <a name="data-flow"></a>Veri akışı

:::image type="content" source="media/datawarehouse.png" alt-text="Veri ambarı için site bileşenleri arasındaki mantıksal veri akışını gösteren diyagram" lightbox="media/datawarehouse.png":::

### <a name="data-storage-and-synchronization"></a>Veri depolama ve eşitleme

| Adım   | Ayrıntılar  |
|--------|----------|
| **1**  | Site sunucusu, verileri site veritabanına aktarır ve depolar. |
| **2**  | Veri ambarı hizmet noktası, zamanlama ve yapılandırmaya bağlı olarak site veritabanından veri alır. |
| **3**  | Veri ambarı hizmet noktası, eşitlenen verilerin bir kopyasını veri ambarı veritabanına aktarır ve depolar. |

### <a name="reporting-flow"></a>Raporlama akışı

| Adım   | Ayrıntılar  |
|--------|----------|
| **A**  | Yerleşik raporları kullanarak bir kullanıcı veri ister. Bu istek, raporlama hizmet noktasına SQL Server Reporting Services kullanılarak geçirilir. |
| **Kenarı**  | Çoğu rapor güncel bilgiler içindir ve bu istekler site veritabanına karşı çalıştırılır. |
| **,**  | Bir rapor **veri ambarı** *kategorisi* içeren raporlardan birini kullanarak geçmiş verileri istediğinde, istek veri ambarı veritabanına göre çalışır. |
