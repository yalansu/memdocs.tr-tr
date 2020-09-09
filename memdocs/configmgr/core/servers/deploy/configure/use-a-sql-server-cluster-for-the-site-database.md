---
title: SQL Server kümesi
titleSuffix: Configuration Manager
description: Configuration Manager site veritabanını barındırmak için SQL Server kümesi kullanma
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 90e4c0dfd2b55ec5acf943cd591ba45c719a68ff
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607508"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Site veritabanı için SQL Server kümesi kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager site veritabanını barındırmak için SQL Server yük devretme kümesi kullanabilirsiniz. Bir küme, yük devretme desteği sağlar ve site veritabanının güvenilirliğini geliştirir. Ancak, ek işleme veya yük dengeleme avantajları sağlamaz. Ayrıca, bir SQL Server yük devretme kümesi paylaşılan depolama alanı kullanır ve tek bir hata noktası sunar. Site sunucusunun site veritabanına bağlanmadan önce SQL Server kümesinin etkin düğümünü bulması gerektiğinden, performans düşüşü meydana gelebilir.  

> [!IMPORTANT]  
> SQL Server kümelerinin başarılı bir şekilde ayarlanması, SQL Server belge kitaplığında sunulan belge ve yordamlara bağımlıdır.  


Configuration Manager yüklemeden önce SQL Server kümesini Configuration Manager destekleyecek şekilde hazırlayın. Daha fazla bilgi için bkz. [kümelenmiş SQL Server örneği hazırlama](#bkmk_prepare).

Configuration Manager Kurulum sırasında Windows Birim Gölge Kopyası Hizmeti yazıcı, Microsoft Windows Server kümesinin her bir fiziksel bilgisayar düğümüne yüklenir. Bu hizmet, **Site Sunucusunu Yedekle** bakım görevini destekler.  

Site yüklendikten sonra, her saat küme düğümündeki değişiklikleri denetler Configuration Manager. Configuration Manager, bileşen yüklemelerini etkileyen bulunan tüm değişiklikleri otomatik olarak yönetir. Örneğin, düğüm yük devretmesi veya SQL Server kümesine yeni bir düğümün eklenmesi.  



## <a name="supported-options"></a>Desteklenen seçenekler

Aşağıdaki seçenekler, site veritabanı olarak kullanılan SQL Server yük devretme kümeleri için desteklenir:

- Tek örnekli küme  

- Birden çok örnek yapılandırması  

- Birden çok etkin düğüm  

- Hem adlandırılmış hem de varsayılan örnek  



## <a name="prerequisites"></a>Önkoşullar

Aşağıdaki önkoşulları göz önünde bulundurun:  

- Site veritabanının site sunucusundan uzakta olması gerekir. Küme, site sistemi sunucusunu içeremez.  

    > [!Note]  
    > Sürüm 1810 ' den başlayarak, Configuration Manager Kurulum işlemi artık site sunucusu rolünün yük devretme kümelemesi için Windows rolü olan bir bilgisayara yüklenmesini engeller. Daha önce site sunucusundaki site veritabanını birlikte bulunduramadık. Bu değişiklik ile, pasif modda bir SQL kümesi ve site sunucusu kullanarak daha az sunucu ile yüksek oranda kullanılabilir bir site oluşturabilirsiniz. Daha fazla bilgi için bkz. [yüksek kullanılabilirlik seçenekleri](high-availability-options.md). <!--3607761, fka 1359132-->  

- Site sunucusunun bilgisayar hesabını kümedeki her sunucunun yerel **Yöneticiler** grubuna ekleyin.  

- Kerberos kimlik doğrulamasını desteklemek için, her bir SQL Server küme düğümünün ağ bağlantısı için **TCP/IP** ağ iletişim protokolünü etkinleştirin. **Adlandırılmış kanallar** protokolü gerekli değildir, ancak Kerberos kimlik doğrulaması sorunlarını gidermek için kullanılabilir. Ağ protokolü ayarları, **SQL Server ağ yapılandırması**altında **SQL Server Yapılandırma Yöneticisi**yapılandırılır.  

- Site veritabanı için SQL Server kümesi kullandığınızda belirli sertifika gereksinimleri vardır. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:
  - [Bir SQL yük devretme kümesi yapılandırmasına sertifika yükler](/sql/database-engine/configure-windows/manage-certificates#provision-failover-cluster-cert)
  - [Configuration Manager için PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers)

  > [!NOTE]
  > SQL 'de bir sertifikayı önceden sağlamadıysanız, Configuration Manager SQL için otomatik olarak imzalanan bir sertifika oluşturur ve hazırlar.<!-- 7099499 -->

## <a name="limitations"></a>Sınırlamalar

Aşağıdaki sınırlamaları göz önünde bulundurun:  


### <a name="installation-and-configuration"></a>Yükleme ve yapılandırma

- İkincil siteler SQL Server kümesini kullanamaz.  

- Bir SQL Server kümesi belirttiğinizde, site veritabanı için varsayılan olmayan dosya konumlarını belirtme seçeneği kullanılamaz.  


### <a name="sms-provider"></a>site veritabanı

SMS sağlayıcısı 'nın bir örneğini SQL Server kümesine yükleyemezsiniz. Ayrıca, kümelenmiş bir SQL Server düğümü olarak çalışan bir bilgisayarda da desteklenmez.  


### <a name="data-replication-options"></a>Veri çoğaltma seçenekleri

**Dağıtılmış görünümler**kullanıyorsanız, site veritabanını barındırmak için SQL Server kümesi kullanamazsınız.  


### <a name="backup-and-recovery"></a>Yedekleme ve kurtarma

Configuration Manager, adlandırılmış bir örnek kullanan bir SQL Server kümesi için Data Protection Manager (DPM) yedeklemesini desteklemez. Varsayılan SQL Server örneğini kullanan bir SQL Server kümesinde DPM yedeklemesini destekler.  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a> Kümelenmiş SQL Server örneği hazırlama  

Site veritabanınızı hazırlamak için tamamlanacak ana görevler şunlardır:

- Mevcut Windows Server küme ortamında, site veritabanını barındıracak sanal SQL Server kümesini oluşturun. SQL Server kümesi yüklemek ve ayarlamak için özel adımlar için, SQL Server sürümünüze özgü belgelere bakın. Daha fazla bilgi için bkz. [yeni SQL Server yük devretme kümesi oluşturma](/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup).  

- SQL Server kümesindeki her bilgisayarda, Configuration Manager site bileşenlerini yüklemesini istemediğiniz her sürücünün kök klasörüne bir dosya yerleştirin. Dosyayı `NO_SMS_ON_DRIVE.SMS` olarak adlandırın. Varsayılan olarak Configuration Manager, yedekleme gibi işlemleri desteklemek için her bir fiziksel düğüme bazı bileşenleri yüklüyor.  

- Site sunucusunun bilgisayar hesabını, her bir Windows Server küme düğümü bilgisayarının yerel **Yöneticiler** grubuna ekleyin.  

- Sanal SQL Server örneğinde, **sysadmin** SQL Server rolünü Configuration Manager Kurulumu çalıştıran kullanıcı hesabına atayın.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Kümelenmiş SQL Server kullanarak yeni bir site yüklemek için  

Kümelenmiş site veritabanı kullanan bir siteyi yüklemek için, bir siteyi yüklemeye yönelik normal işleminizi izleyen Configuration Manager Kurulum programını aşağıdaki değişiklik ile gerçekleştirin:  

- **Veritabanı Bilgileri** sayfasında, site veritabanını barındıracak sanal SQL Server kümesi örneğinin adını belirtin. Sanal örnek, SQL Server çalıştıran bilgisayarın adını değiştirir.  

    > [!IMPORTANT]  
    > Sanal SQL Server kümesi örneğinin adını girerken, Windows Server kümesi tarafından oluşturulan sanal Windows Server adını girmeyin. Sanal Windows Server adını kullanırsanız, site veritabanı, etkin Windows Server küme düğümünün yerel sabit sürücüsüne yüklenir. Söz konusu düğüm başarısız olursa, bu durum yük devretmenin başarıyla tamamlanmasını engeller.