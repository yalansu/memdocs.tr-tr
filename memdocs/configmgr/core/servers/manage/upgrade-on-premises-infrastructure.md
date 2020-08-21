---
title: Şirket içi altyapıyı yükseltme
titleSuffix: Configuration Manager
description: SQL Server ve site sistemlerinin işletim sistemi gibi altyapıyı nasıl yükselteceğinizi öğrenin.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7efc775199a34a66a8cd4a83b85baccd4a3ab5cb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699492"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Configuration Manager destekleyen şirket içi altyapıyı yükseltme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager çalıştıran sunucu altyapısını yükseltmenize yardımcı olması için bu makaledeki bilgileri kullanın.  

- Önceki bir sürümden Configuration Manager, güncel dala *yükseltmek* istiyorsanız, bkz. [Configuration Manager yükseltme](../deploy/install/upgrade-to-configuration-manager.md).  

- Configuration Manager, geçerli dalınızı ve altyapınızı yeni bir sürüme *güncelleştirmek* istiyorsanız, bkz. [Configuration Manager güncelleştirmeleri](updates.md).  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Site sistemlerinin işletim sistemini yükseltme  

Configuration Manager, aşağıdaki durumlarda site sunucusunu ve herhangi bir site sistemi rolünü barındıran sunucu işletim sisteminin yerinde yükseltmesini destekler:  

- Configuration Manager, Windows 'un elde edilen hizmet paketi düzeyini hala destekliyorsa, sonraki bir Windows Server hizmet paketine yerinde yükseltmeyi destekler.  

- Şuradan yerinde yükseltme:  

    - Windows Server 2016 Windows Server 2019  

    - Windows Server 2012 R2 'den Windows Server 2019  

    - Windows Server 2012 R2 'den Windows Server 2016  

    - Windows Server 2012 Windows Server 2016  

    - Windows Server 2012 Windows Server 2012 R2 'ye  

    - Windows Server 2008 R2 'den Windows Server 2012 R2 'ye  

Bir sunucuyu yükseltmek için, yükseltmekte olduğunuz işletim sistemi tarafından sunulan yükseltme yordamlarını kullanın. Aşağıdaki makalelere bakın:  

- [Windows Server yükseltme Merkezi](https://aka.ms/upgradecenter)  

- [Windows Server 2016 için yükseltme ve dönüştürme seçenekleri](/windows-server/get-started/supported-upgrade-paths)  

- [Windows Server 2012 R2 için yükseltme seçenekleri](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> Windows Server 2016 veya 2019 ' ye yükseltme

Aşağıdaki yükseltme senaryolarından herhangi biri için bu bölümdeki adımları kullanın:  

- Windows Server 2012 R2 veya Windows Server 2016 ' ü Windows Server 'a yükseltin 2019  

- Windows Server 2012 veya Windows Server 2012 R2 'yi Windows Server 2016 sürümüne yükseltin  

#### <a name="before-upgrade"></a>Yükseltmeden önce

- (Windows Server 2012 veya Windows Server 2012 R2): System Center Endpoint Protection (SCEP) istemcisini kaldırın. Windows Server 'da artık SCEP istemcisinin yerini alan Windows Defender yerleşik olarak bulunur. SCEP istemcisinin varlığı Windows Server yükseltmesine engel olabilir.  

- Yüklüyse WSUS rolünü sunucudan kaldırın. WSUS yeniden yüklendikten sonra SUSDB 'yi koruyabilir ve yeniden iliştirebilirsiniz.  

- Site sunucusunun işletim sistemini yükseltiyorsanız, site için [dosya tabanlı çoğaltmanın](../../plan-design/hierarchy/file-based-replication.md) sağlıklı olduğundan emin olun. Hem gönderme hem de alma sitelerindeki biriktirme listesinin tüm gelen kutularını kontrol edin. Çok sayıda takılı veya bekleyen çoğaltma işi varsa, bu işlerin bitmesini bekleyin.<!-- SCCMDocs#1792 -->
    - Gönderen sitede **Sender. log**' u gözden geçirin.
    - Alıcı sitede, **biriktiriciden çıkartma günlüğünü**gözden geçirin.

#### <a name="after-upgrade"></a>Yükseltmeden sonra

- Windows Defender 'ın etkinleştirildiğinden, otomatik başlatma için ayarlandığından ve çalıştığından emin olun.  

- Aşağıdaki Configuration Manager hizmetlerinin çalıştığından emin olun:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- **Windows Işlem etkinleştirme** ve **www/W3SVC** hizmetlerinin etkinleştirildiğinden ve otomatik başlatma için ayarlandığından emin olun. Yükseltme işlemi bu hizmetleri devre dışı bırakır, bu nedenle aşağıdaki site sistem rolleri için çalıştığından emin olun:  

    - Site sunucusu  

    - Yönetim noktası  

    - Uygulama Kataloğu web hizmet noktası  

    - Uygulama Kataloğu web sitesi noktası  

- Bir site sistem rolü barındıran her sunucunun tüm [önkoşulları](../../plan-design/configs/site-and-site-system-prerequisites.md)karşılayacak şekilde devam ettiğinden emin olun. Örneğin, BITS 'yi, WSUS 'u yeniden yüklemeniz veya IIS için belirli ayarları yapılandırmanız gerekebilir.  

- Eksik önkoşulları geri yükledikten sonra hizmetlerin başlatılmış ve çalışır durumda olduğundan emin olmak için sunucuyu bir kez daha yeniden başlatın.  

- Birincil site sunucusunu yükseltiyorsanız [bir site sıfırlaması çalıştırın](modify-your-infrastructure.md#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Uzaktan Configuration Manager konsolları için bilinen sorun

Site sunucusunu veya SMS sağlayıcısı 'nın bir örneğini yükselttikten sonra Configuration Manager konsoluna bağlanamazsınız. Bu sorunu geçici olarak çözmek için WMI 'da **SMS yöneticileri** grubunun izinlerini el ile geri yükleyin. Site sunucusunda ve SMS sağlayıcısı 'nın bir örneğini barındıran her uzak sunucuda izinlerin ayarlanması gerekir:

1. İlgili sunucularda, Microsoft Yönetim Konsolu 'Nu (MMC) açın ve  **WMI denetimi**için ek bileşenini ekleyin ve ardından **Yerel bilgisayar**' ı seçin.  

2. MMC ' de, **WMI denetimi (yerel)** **özelliklerini** açın ve **güvenlik** sekmesini seçin.  

3. Kök altındaki ağacı genişletin, **SMS** düğümünü seçin ve ardından **güvenlik**' i seçin.  **SMS yöneticileri** grubunun aşağıdaki izinlere sahip olduğundan emin olun:  

    - Hesabı etkinleştir  

    - Uzaktan Etkinleştir  

4. **SMS** düğümünün altındaki **güvenlik sekmesinde** , **Site_ &lt; Sitekodu**> düğümünü seçin ve ardından **güvenlik**' i seçin. **SMS yöneticileri** grubunun aşağıdaki izinlere sahip olduğundan emin olun:  

    - Çalıştırma yöntemleri  

    - Sağlayıcı yazma  

    - Hesabı etkinleştir  

    - Uzaktan Etkinleştir  

5. Configuration Manager konsoluna erişimi geri yüklemek için izinleri kaydedin.  

#### <a name="known-issue-for-remote-site-systems"></a>Uzak site sistemleri için bilinen sorun

Bir site sistem rolü barındıran bir sunucuyu yükselttikten sonra, bu değer `Software\Microsoft\SMS` aşağıdaki kayıt defteri anahtarında eksik olabilir: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

Windows 'u sunucuda yükselttikten sonra bu değer eksikse, el ile ekleyin. Aksi takdirde, site sistem rollerinin, site sunucusu gelen kutularına dosya yükleme sorunları olabilir.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Windows Server 2012 R2 'ye yükseltme

Windows Server 2008 R2 veya Windows Server 2012 ' den Windows Server 2012 R2 'ye yükselttiğinizde aşağıdaki koşullar geçerli olabilir:

#### <a name="before-upgrade"></a>Yükseltmeden önce

- Windows Server 2012: yüklüyse WSUS rolünü sunucudan kaldırın. WSUS yeniden yüklendikten sonra SUSDB 'yi koruyabilir ve yeniden iliştirebilirsiniz.  

- Windows Server 2008 R2 'de: Windows Server 2012 R2 'ye yükseltmeden önce, WSUS 3,2 'ı sunucudan kaldırmanız gerekir. WSUS yeniden yüklendikten sonra SUSDB 'yi koruyabilir ve yeniden iliştirebilirsiniz. Daha fazla bilgi için bkz. [Windows Server Update Services 'A genel bakış](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

- Site sunucusunun işletim sistemini yükseltiyorsanız, site için [dosya tabanlı çoğaltmanın](../../plan-design/hierarchy/file-based-replication.md) sağlıklı olduğundan emin olun. Hem gönderme hem de alma sitelerindeki biriktirme listesinin tüm gelen kutularını kontrol edin. Çok sayıda takılı veya bekleyen çoğaltma işi varsa, bu işlerin bitmesini bekleyin.<!-- SCCMDocs#1792 -->
    - Gönderen sitede **Sender. log**' u gözden geçirin.
    - Alıcı sitede, **biriktiriciden çıkartma günlüğünü**gözden geçirin.

#### <a name="after-upgrade"></a>Yükseltmeden sonra

- Yükseltme işlemi Windows Dağıtım Hizmetleri 'ni devre dışı bırakır. Aşağıdaki site sistem rolleri için bu hizmetin başlatıldığından ve çalıştığından emin olun:  

    - Site sunucusu  

    - Yönetim noktası  

    - Uygulama Kataloğu web hizmet noktası  

    - Uygulama Kataloğu web sitesi noktası  

- **Windows Işlem etkinleştirme** ve **www/W3SVC** hizmetlerinin etkinleştirildiğinden ve otomatik başlatma için ayarlandığından emin olun. Yükseltme işlemi bu hizmetleri devre dışı bırakır, bu nedenle aşağıdaki site sistem rolleri için çalıştığından emin olun:  

    - Site sunucusu  

    - Yönetim noktası  

    - Uygulama Kataloğu web hizmet noktası  

    - Uygulama Kataloğu web sitesi noktası  

- Bir site sistem rolü barındıran her sunucunun tüm [önkoşulları](../../plan-design/configs/site-and-site-system-prerequisites.md)karşılayacak şekilde devam ettiğinden emin olun. Örneğin, BITS 'yi, WSUS 'u yeniden yüklemeniz veya IIS için belirli ayarları yapılandırmanız gerekebilir.  

    Eksik önkoşulları geri yükledikten sonra hizmetlerin başlatılmış ve çalışır durumda olduğundan emin olmak için sunucuyu bir kez daha yeniden başlatın.  

### <a name="unsupported-upgrade-scenarios"></a>Desteklenmeyen yükseltme senaryoları

Aşağıdaki Windows Server yükseltme senaryoları genellikle Configuration Manager, ancak desteklenmez:  

- Windows Server 2008 ile Windows Server 2012 veya üzeri  

- Windows Server 2008 R2 'den Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> İstemcilerin işletim sistemini yükseltme  

Configuration Manager, aşağıdaki durumlarda işletim sisteminin Configuration Manager istemcileri için yerinde yükseltmesini destekler:  

- Configuration Manager, elde edilen hizmet paketi düzeyini destekliyorsa, daha sonraki bir Windows hizmet paketine yerinde yükseltmeyi destekler.  

- Windows 'un desteklenen bir sürümünden Windows 10 ' a yerinde yükseltme. Daha fazla bilgi için bkz. [Windows 'u en son sürüme yükseltme](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Windows 10 ' un derleme için hizmet yükseltmeleri. Daha fazla bilgi için bkz. [Windows 'u hizmet olarak yönetme](../../../osd/deploy-use/manage-windows-as-a-service.md).  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> SQL Server yükselt  

Configuration Manager, site veritabanı sunucusunda SQL Server yerinde yükseltmesini destekler.

Configuration Manager tarafından desteklenen SQL Server sürümleri hakkında bilgi için bkz. [SQL Server sürümleri Için destek](../../plan-design/configs/support-for-sql-server-versions.md).  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>SQL Server’ın hizmet paketi sürümünü yükseltme

Elde edilen SQL Server hizmet paketi düzeyini Configuration Manager hala destekliyorsa, daha sonraki bir hizmet paketine SQL Server yerinde yükseltmeyi destekler.

Hiyerarşide birden fazla Configuration Manager siteniz olduğunda, her site SQL Server farklı bir hizmet paketi sürümünü çalıştırabilir. Site SQL Server hizmet paketi sürümünü yükseltme sırasında herhangi bir sınırlama yoktur.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Yeni bir SQL Server sürümüne yükselt

Configuration Manager, SQL Server aşağıdaki sürümlere yerinde yükseltmesini destekler:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Bu, SQL Server Express SQL Server Express ikincil sitelerde daha yeni bir sürüme yükseltmesini içerir.

Site veritabanını barındıran SQL Server sürümünü yükselttiğinizde, sitelerde kullanılan SQL Server sürümünü aşağıdaki sırayla yükseltmeniz gerekir:

1. Önce merkezi yönetim sitesindeki SQL Server yükseltin  

2. İkincil bir sitenin üst birincil sitesini yükseltmeden önce ikincil siteleri yükseltme  

3. Ana birincil siteleri en son yükseltin. Bu siteler, bir merkezi yönetim sitesine rapor veren alt birincil siteleri ve bir hiyerarşinin en üst düzey sitesi olan tek başına birincil siteleri içerir.  

### <a name="sql-server-cardinality-estimation-level"></a>SQL Server kardinalite tahmin düzeyi

Bir site veritabanını SQL Server önceki bir sürümünden yükselttiğinizde, veritabanı var olan SQL kardinalite tahmin düzeyini, bu SQL Server örneği için izin verilen en düşük düzeyde tutar. Uyumluluk düzeyindeki bir veritabanı ile SQL Server yükseltme, izin verilen düzeyinden daha düşük olan veritabanını, SQL Server tarafından izin verilen en düşük uyumluluk düzeyine otomatik olarak ayarlar.

Aşağıdaki tablo Configuration Manager site veritabanları için önerilen uyumluluk düzeylerini tanımlar:

|SQL Server sürümü | Desteklenen uyumluluk düzeyleri | Önerilen düzey |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Site veritabanınız için kullanımdaki SQL Server kardinalite tahmini uyumluluk düzeyini belirlemek için, site veritabanı sunucusunda aşağıdaki SQL sorgusunu çalıştırın:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

SQL CE Uyumluluk düzeyleri ve bunların nasıl ayarlanacağı hakkında daha fazla bilgi için bkz. [ALTER DATABASE Compatibility Level (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).

SQL Server yükseltme hakkında daha fazla bilgi için aşağıdaki SQL Server makalelerine bakın:  

- [SQL Server 2017 ' ye yükseltin](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [SQL Server 2016 ' ye yükseltin](/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [SQL Server 2014’e yükseltme](/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Site veritabanı sunucusundaki SQL Server’ı yükseltmek için  

1. Sitedeki tüm Configuration Manager hizmetlerini durdur  

2. SQL Server desteklenen bir sürüme yükseltin  

3. Configuration Manager hizmetlerini yeniden başlatın  

> [!NOTE]  
> Merkezi yönetim sitesinde kullanılan SQL Server sürümünü standart bir veri merkezine ya da kuruluşa değiştirdiğinizde, veritabanı bölümü değişmez. Bu veritabanı bölümü, hiyerarşinin desteklediği istemci sayısını sınırlar.