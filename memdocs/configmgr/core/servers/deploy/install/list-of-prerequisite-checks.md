---
title: Önkoşul denetimleri
titleSuffix: Configuration Manager
description: Configuration Manager güncelleştirmeleri için belirli önkoşul denetimlerinin başvurusu.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2dd722ddcf0e5ea6e944a76366204ac83ede05ec
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698965"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Configuration Manager için önkoşul denetimleri listesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede Configuration Manager yüklediğinizde veya güncelleştirdiğinizde çalıştırılan önkoşul denetimleri ayrıntılı olarak açıklanır. Daha fazla bilgi için bkz. [önkoşul denetleyicisi](prerequisite-checker.md).  



## <a name="errors"></a>Hatalar

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Hedef birincil sitede etkin geçiş eşlemeleri

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteler için etkin geçiş eşlemesi yok.

### <a name="active-replica-mp"></a>Etkin çoğaltma MP

*Uygulama hedefi: birincil site*

Etkin bir yönetim noktası çoğaltması var.

### <a name="administrative-rights-on-expand-primary-site"></a>Genişletme birincil sitesinde yönetim hakları

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, Kurulumu çalıştıran kullanıcı hesabının tek başına birincil site sunucusunda **yönetici** hakları vardır.

### <a name="administrative-rights-on-site-system"></a>Site sisteminde yönetici hakları

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Configuration Manager kurulumu 'nu çalıştıran kullanıcı hesabı, site sunucusunda **yönetici** haklarına sahiptir.

### <a name="administrator-rights-on-central-administration-site"></a>Merkezi yönetim sitesinde yönetici hakları

*Uygulama hedefi: birincil site*

Configuration Manager kurulumu 'nu çalıştıran kullanıcı hesabı, merkezi yönetim site sunucusunda **yönetici** haklarına sahiptir.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Genişletilmiş birincil sitede eşitleme noktası Varlık Yönetim Bilgileri

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, Varlık Yönetim Bilgileri eşitleme noktası rolü tek başına birincil sitede yüklü değildir.

### <a name="bits-enabled"></a>BITS etkin

*Uygulama hedefi: yönetim noktası*

Arka Plan Akıllı Aktarım Hizmeti (BITS) yönetim noktasına yüklendi. Bu denetim, aşağıdakilerden biri nedeniyle başarısız olabilir:

- BITS yüklü değil  

- IIS 7,0 için IIS 6,0 WMI uyumluluk bileşeni sunucuda veya uzak IIS ana bilgisayarında yüklü değil  

- Kurulum, uzak IIS ayarlarını doğrulayamadı. IIS ortak bileşenleri site sunucusuna yüklenmez.  

### <a name="case-insensitive-collation-on-sql-server"></a>SQL Server için büyük/küçük harfe duyarsız harmanlama

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server yüklemesi, **SQL_Latin1_General_CP1_CI_AS**gibi büyük/küçük harfe duyarsız harmanlama kullanır.

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Genişletme birincil sitesinde merkezi yönetim sitesi sunucusu yönetim hakları

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, merkezi yönetim site sunucusunun bilgisayar hesabı tek başına birincil site sunucusunda **yönetici** haklarına sahiptir.

### <a name="client-version-on-management-point-computer"></a>Yönetim noktası bilgisayarındaki istemci sürümü

*Uygulama hedefi: yönetim noktası*

Yönetim noktasını, Configuration Manager istemcisinin farklı bir sürümü yüklü olmayan bir sunucuya yüklüyorsunuz.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Genişletilmiş birincil sitede bulut yönetimi ağ geçidi

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, bulut yönetimi ağ geçidi rolü tek başına birincil sitede yüklü değildir.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Merkezi yönetim sitesindeki SQL Server bağlantı

*Uygulama hedefi: birincil site*

Birincil sitede var olan bir hiyerarşiye katılması için Configuration Manager Kurulumu çalıştıran kullanıcı hesabı, merkezi yönetim sitesi için SQL Server örneğinde **sysadmin** rolüne sahiptir.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>Özel istemci Aracısı ayarlarında NAP etkin

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Ağ erişim koruması 'nı (NAP) etkinleştiren özel istemci ayarları yoktur.

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Genişletilen birincil sitede veri ambarı hizmet noktası

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, veri ambarı hizmet noktası rolü tek başına birincil sitede yüklü değildir.

### <a name="dedicated-sql-server-instance"></a>Adanmış SQL Server örneği

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Configuration Manager site veritabanını barındırmak için SQL Server adanmış bir örneğini yapılandırdınız.

Örneği başka bir site kullanıyorsa, yeni site için farklı bir örnek seçmeniz gerekir. Ayrıca, diğer siteyi kaldırabilir veya veritabanını SQL Server 'ın farklı bir örneğine taşıyabilirsiniz.

### <a name="default-client-agent-settings-have-nap-enabled"></a>Varsayılan istemci Aracısı ayarlarında NAP etkin

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Varsayılan istemci ayarları, ağ erişim koruması 'nı (NAP) etkinleştirmez.

### <a name="domain-membership-error"></a>Etki alanı üyeliği (hata)

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site, SMS sağlayıcısı, SQL Server*

Configuration Manager bilgisayar bir Windows etki alanının üyesidir.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Genişletilen birincil sitede Endpoint Protection noktası

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, Endpoint Protection noktası rolü tek başına birincil sitede yüklü değildir.

### <a name="existing-configuration-manager-server-components-on-server"></a>Sunucuda var olan Configuration Manager Server bileşenleri

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Site yüklemesi için seçilen sunucuda bir site sunucusu veya site sistemi rolü zaten yüklü değil.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Sürüm ve site kodu için mevcut tek başına birincil site

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Genişletmeyi planladığınız birincil site tek başına bir birincil sitedir. Aynı Configuration Manager sürümüne, ancak yüklenecek merkezi yönetim sitesinden farklı bir site koduna sahiptir.

### <a name="firewall-exception-for-sql-server"></a>SQL Server için güvenlik duvarı özel durumu

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site, yönetim noktası*

Windows güvenlik duvarı devre dışı bırakıldı veya SQL Server için ilgili bir Windows Güvenlik Duvarı özel durumu var.

Sqlservr.exe veya gerekli TCP bağlantı noktalarına uzaktan erişilmesine izin verin. Varsayılan olarak, SQL Server TCP bağlantı noktası 1433 ' i dinler ve SQL Server Hizmet Aracısı (SSB) TCP bağlantı noktası 4022 ' i kullanır.

### <a name="free-disk-space-on-site-server"></a>Site sunucusundaki boş disk alanı

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Site sunucusunu yüklemek için en az 15 GB boş disk alanına sahip olması gerekir. SMS sağlayıcısını aynı sunucuya yüklerseniz, ek 1 GB boş alan gerekir.

### <a name="iis-service-running"></a>IIS hizmeti çalışıyor

*Uygulama hedefi: yönetim noktası, dağıtım noktası*

Yönetim noktası veya dağıtım noktası için sunucusunda IIS yüklü ve çalışır.

### <a name="incompatible-collection-references"></a>Uyumsuz koleksiyon başvuruları

*Uygulama hedefi: merkezi yönetim sitesi*

Bir yükseltme sırasında koleksiyonlar yalnızca aynı türdeki diğer koleksiyonlara başvurur.

### <a name="match-collation-of-expand-primary-site"></a>Genişletme birincil sitesinin harmanlamasını Eşleştir

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, tek başına birincil sitenin site veritabanı merkezi yönetim sitesindeki Site veritabanı ile aynı harmanlamaya sahiptir.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>SQL Server Always on kullanılabilirlik grupları için maksimum metin çoğaltma boyutu

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server Always on 'U kullanırken, **en büyük metin REPL boyutu** ayarı doğru şekilde yapılandırılmalıdır. Daha fazla bilgi için bkz. [Configuration Manager Ile Always on kullanılabilirlik grupları SQL Server kullanmaya hazırlanma](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Genişletilen birincil sitede bağlayıcı Microsoft Intune

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, Microsoft Intune bağlayıcı rolü tek başına birincil sitede yüklü değildir.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Microsoft uzaktan değişiklikleri sıkıştırma (RDC) kitaplığı kaydedildi

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

RDC kitaplığı Configuration Manager site sunucusuna kaydedilir.

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Windows Installer sürümünü doğrular.

Bu denetim başarısız olduğunda, kurulum sürümü doğrulayamadı veya yüklü sürüm 4,5 Windows Installer en düşük gereksinimini karşılamıyor.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Configuration Manager konsolunun en düşük .NET Framework sürümü

*Uygulama hedefi: Configuration Manager konsolu*

Microsoft .NET Framework 4,0, Configuration Manager konsol bilgisayarında yüklüdür.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Configuration Manager site sunucusu için en düşük .NET Framework sürümü

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

.NET Framework 3,5, Configuration Manager site sunucusunda yüklü veya etkin.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Configuration Manager ikincil site için SQL Server Express Edition yüklemesi için en düşük .NET Framework sürümü

*Uygulama hedefi: Ikincil site*

.NET Framework 4,0, Configuration Manager ikincil site sunucusunda yüklü veya etkin. SQL Server Express için bu sürüm gereklidir.

### <a name="parent-database-collation"></a>Üst veritabanı harmanlaması

*Uygulama hedefi: birincil site, ikincil site*

Site veritabanının harmanlaması, üst sitenin veritabanı harmanlamasıyla eşleşir. Hiyerarşideki tüm siteler aynı veritabanı harmanlamasını kullanmalıdır.

### <a name="parent-site-replication-status"></a>Üst site çoğaltma durumu

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Üst sitenin çoğaltma durumu **çoğaltma etkin** (durum **125**).

### <a name="pending-system-restart"></a>Sistem yeniden başlatma bekleniyor

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Kurulumu çalıştırmadan önce, başka bir program sunucunun yeniden başlatılmasını gerektiriyor.

Sürüm 1810 ' den başlayarak bu denetim daha esnektir. Bilgisayarın bekleyen bir yeniden başlatma durumunda olup olmadığını görmek için, aşağıdaki kayıt defteri konumlarını denetler:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>Birincil FQDN

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site, site veritabanı sunucusu*

Bilgisayarın NetBIOS adı, tam etki alanı adı (FQDN) içindeki yerel ana bilgisayar adıyla eşleşir.

### <a name="read-only-domain-controller"></a>Salt okunur etki alanı denetleyicisi

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Site veritabanı sunucuları ve ikincil site sunucuları, salt okunurdur bir etki alanı denetleyicisinde (RODC) desteklenmez.

Daha fazla bilgi için, [bir etki alanı denetleyicisine SQL Server yüklerken sorun](https://support.microsoft.com/help/2032911)hakkında Microsoft desteği makalesine bakın.

### <a name="required-sql-server-collation"></a>Gerekli SQL Server harmanlama

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

SQL Server örneği **SQL_Latin1_General_CP1_CI_AS** harmanlamasını kullanacak şekilde yapılandırılmıştır.

Configuration Manager site veritabanı zaten yüklüyse, bu denetim veritabanı için de geçerli olur. SQL Server örneğinizi ve veritabanı harmanlamalarını değiştirme hakkında daha fazla bilgi için bkz. [SQL harmanlama ve Unicode desteği](/sql/relational-databases/collations/collation-and-unicode-support).

Bir Çince işletim sistemi kullanıyorsanız ve GB18030 desteği gerektiriyorsa, bu denetim uygulanmaz. GB18030 desteğini etkinleştirme hakkında daha fazla bilgi için bkz. [Uluslararası destek](../../../plan-design/hierarchy/international-support.md).

### <a name="server-service-is-running"></a>Sunucu hizmeti çalışıyor

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Sunucu hizmeti başlatılmış ve çalışıyor.

### <a name="setup-source-folder"></a>Kurulum kaynak klasörü

*Uygulama hedefi: Ikincil site*

İkincil sitenin bilgisayar hesabı, kurulum kaynak klasörü ve paylaşma için aşağıdaki izinlere sahiptir:

- **Oku** NTFS dosya sistemi izinleri  

- Paylaşma izinlerini **Oku**  

> [!Note]  
> Yönetim paylaşımları kullanıyorsanız, örneğin, C $ ve D $, ikincil site bilgisayar hesabının sunucuda **yönetici** olması gerekir.  

### <a name="setup-source-version"></a>Kurulum kaynak sürümü

*Uygulama hedefi: Ikincil site*

İkincil site yüklemesi için belirtilen kaynak klasördeki Configuration Manager sürümü, birincil sitenin Configuration Manager sürümüyle eşleşiyor.

### <a name="site-code-in-use"></a>Site Kodu kullanımda

*Uygulama hedefi: birincil site*

Belirtilen site kodu Configuration Manager hiyerarşisinde zaten kullanımda değil. Bu site için benzersiz bir site kodu belirtin.

### <a name="site-server-computer-account-administrative-rights"></a>Site sunucusu bilgisayar hesabı yönetici hakları

*Uygulama hedefi: birincil site, site veritabanı sunucusu*

Site sunucusu bilgisayar hesabının, SQL Server ve yönetim noktası üzerinde **yönetici** hakları vardır.

### <a name="site-server-fqdn-length"></a>Site sunucusu FQDN uzunluğu

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Site sunucusunun FQDN 'sinin uzunluğu.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Genişletilmiş birincil sitede pasif modda site sunucusu

*Uygulama hedefi: merkezi yönetim sitesi*

Birincil siteyi bir hiyerarşiye genişlettiğinizde, Pasif mod rolündeki site sunucusu tek başına birincil sitede yüklü değildir.

### <a name="sms-provider-in-same-domain-as-site-server"></a>Site sunucusuyla aynı etki alanında bulunan SMS sağlayıcısı

*Uygulama hedefi: SMS sağlayıcısı*

SMS sağlayıcısı 'nın herhangi bir örneği, site sunucusuyla aynı etki alanında bulunur.

### <a name="software-update-point-in-nlb-configuration"></a>NLB yapılandırmasındaki yazılım güncelleştirme noktası

*Uygulama hedefi: yazılım güncelleştirme noktası*

Site, etkin yazılım güncelleştirme noktaları için herhangi bir sanal konum ile Ağ Yükü Dengeleme (NLB) kullanmıyor.

### <a name="software-update-point-using-a-load-balancer"></a>Yük dengeleyici kullanan yazılım güncelleştirme noktası

*Uygulama hedefi: yazılım güncelleştirme noktası*

Configuration Manager, ağ (NLB) veya donanım yük dengeleyicileri (HLB) yazılım güncelleştirme noktalarını desteklemez.

### <a name="sql-server-always-on-availability-groups"></a>SQL Server Always On kullanılabilirlik grupları

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server her zaman açık olduğunda, bir kullanılabilirlik grubu barındırmak için en düşük gereksinimleri karşılaması gerekir. Daha fazla bilgi için bkz. [Configuration Manager Ile Always on kullanılabilirlik grupları SQL Server kullanmaya hazırlanma](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>SQL Server okunabilir ikincil öğeler için yapılandırılmış kullanılabilirlik grubu

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server Always on 'U kullanırken, kullanılabilirlik grubu çoğaltmalarının ikincil okuma durumunu kontrol edin.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>El ile yük devretme için yapılandırılan SQL Server kullanılabilirlik grubu

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server Always on kullanıldığında, kullanılabilirlik grubu çoğaltmaları el ile yük devretme için yapılandırılır.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>Varsayılan örnekteki kullanılabilirlik Grubu çoğaltmalarını SQL Server

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server Always on kullanıldığında, kullanılabilirlik grubu çoğaltmaları varsayılan örnekten yapılır.

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>SQL kullanılabilirlik grubu çoğaltmalarının hepsi aynı dengeli dağıtım moduna sahip olmalıdır

<!-- SCCMDocs-pr#3899 -->
*Uygulama hedefi: site veritabanı sunucusu*

Sürüm 1906 ' den başlayarak, her zaman açık SQL Server kullanırken, kullanılabilirlik Grubu çoğaltmalarını aynı [dengeli dağıtım moduyla](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)yapılandırmanız gerekir.

### <a name="sql-availability-group-replicas-must-be-healthy"></a>SQL kullanılabilirlik grubu çoğaltmaları sağlıklı olmalıdır

<!-- SCCMDocs-pr#3899 -->
*Uygulama hedefi: site veritabanı sunucusu*

Sürüm 1906 ' den başlayarak, her zaman açık SQL Server kullanıldığında, kullanılabilirlik grubu çoğaltmaları sağlıklı bir durumdur.

### <a name="sql-server-configuration-for-site-upgrade"></a>Site yükseltme için SQL Server yapılandırması

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server, site yükseltme için en düşük gereksinimleri karşılar. Daha fazla bilgi için bkz. [desteklenen SQL Server sürümleri](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="sql-server-edition"></a>SQL Server yayını

*Uygulama hedefi: site veritabanı sunucusu*

Sitedeki SQL Server SQL Server Express.

### <a name="sql-server-express-on-secondary-site"></a>İkincil sitede SQL Server Express

*Uygulama hedefi: Ikincil site*

SQL Server Express ikincil site sunucusuna başarıyla yüklenebilir.

### <a name="sql-server-on-the-secondary-site-server"></a>İkincil site sunucusunda SQL Server

*Uygulama hedefi: Ikincil site*

SQL Server, ikincil site sunucusuna yüklenir. İkincil bir site için uzak site sistemine SQL Server yükleyemezsiniz.

> [!Warning]  
> Bu denetim yalnızca kurulumun mevcut bir SQL Server örneğini kullanmasını seçtiğinizde geçerlidir.  

### <a name="sql-server-service-running-account"></a>SQL Server hizmet çalıştıran hesap

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

SQL Server hizmeti için oturum açma hesabı yerel bir kullanıcı hesabı veya **yerel hizmet**değil.

SQL Server hizmetini geçerli bir etki alanı hesabı, **ağ hizmeti**veya **yerel sistem**kullanacak şekilde yapılandırın.

### <a name="sql-server-site-database-consistency"></a>Site veritabanı tutarlılığını SQL Server

*Uygulama hedefi: site veritabanı sunucusu*

Veritabanı tutarlılığını doğrulayın.

### <a name="sql-server-sysadmin-rights"></a>SQL Server sysadmin hakları

*Uygulama hedefi: site veritabanı sunucusu*

Configuration Manager kurulumu 'nu çalıştıran kullanıcı hesabı, site veritabanı yüklemesi için seçtiğiniz SQL Server örneğinde **sysadmin** rolüne sahiptir. Kurulum, izinleri doğrulamak için SQL Server örneğine erişemediğinde bu denetim de başarısız olur.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Başvuru sitesi için sysadmin haklarını SQL Server

*Uygulama hedefi: site veritabanı sunucusu*

Configuration Manager kurulumu 'nu çalıştıran kullanıcı hesabının, başvuru sitesi veritabanı olarak seçtiğiniz SQL Server rol örneğinde **sysadmin** rolü vardır. Site veritabanını değiştirmek için **sysadmin** rolü izinleri SQL Server gerekir.

### <a name="sql-server-tcp-port"></a>SQL Server TCP bağlantı noktası

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server örneği için TCP etkinleştirilir ve statik bir bağlantı noktası kullanmak üzere ayarlanır.

### <a name="sql-server-version"></a>SQL Server sürümü

*Uygulama hedefi: site veritabanı sunucusu*

Desteklenen bir SQL Server sürümü belirtilen site veritabanı sunucusuna yüklendi.

Daha fazla bilgi için bkz. [SQL Server sürümleri Için destek](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="unsupported-os-for-configuration-manager-console"></a>Configuration Manager konsolu için desteklenmeyen işletim sistemi

*Uygulama hedefi: Configuration Manager konsolu*

Desteklenen bir işletim sistemi sürümünü çalıştıran bilgisayarlara Configuration Manager konsolunu yükler.

Daha fazla bilgi için, [Configuration Manager konsolunun desteklenen işletim sistemi sürümleri](../../../plan-design/configs/supported-operating-systems-consoles.md)bölümüne bakın.

### <a name="unsupported-os-for-site-server"></a>Site sunucusu için desteklenmeyen işletim sistemi

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site, Configuration Manager konsolu, yönetim noktası, dağıtım noktası*

Sunucu desteklenen bir işletim sistemi sürümünü çalıştırıyor.

Daha fazla bilgi için bkz. [Configuration Manager site sistemi sunucuları Için desteklenen işletim sistemi sürümleri](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Desteklenmeyen site sistemi rolü: bant dışı hizmet noktası

*Uygulama hedefi: birincil site*

Bant dışı hizmet noktası site sistemi rolü yüklü değil.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Desteklenmeyen site sistemi rolü: sistem durumu doğrulama noktası

*Uygulama hedefi: birincil site*

Sistem durumu doğrulama noktası site sistemi rolü yüklü değil.

### <a name="unsupported-upgrade-path"></a>Desteklenmeyen yükseltme yolu

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Hiyerarşideki tüm site sunucuları, yükseltme için gereken en düşük Configuration Manager sürümünü karşılar.

### <a name="usmt-installed"></a>USMT yüklendi

*Uygulama hedefi: merkezi yönetim sitesi, birincil site (yalnızca tek başına)*

Windows için Windows değerlendirme ve dağıtım seti 'nin (ADK) Kullanıcı Durumu Taşıma Aracı (USMT) bileşeni yüklüdür.

### <a name="validate-fqdn-of-sql-server"></a>SQL Server FQDN 'sini doğrula

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server bilgisayarı için geçerli bir FQDN belirttiniz.

### <a name="verify-central-administration-site-version"></a>Merkezi Yönetim sitesi sürümünü doğrula

*Uygulama hedefi: birincil site*

Merkezi yönetim sitesinin aynı Configuration Manager sürümü vardır.

### <a name="verify-database-consistency"></a>Veritabanı tutarlılığını doğrulama

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

SQL Server site veritabanının tutarlılığını doğrular.  

### <a name="windows-deployment-tools-installed"></a>Windows dağıtım araçları yüklendi

*Uygulama hedefi: SMS sağlayıcısı*

Windows ADK 'nin Windows Dağıtım Araçları bileşeni yüklüdür.

### <a name="windows-failover-cluster"></a>Windows Yük Devri Kümesi

*Uygulama hedefi: site sunucusu, yönetim noktası, dağıtım noktası*

Site sunucusu, yönetim noktası veya dağıtım noktası rollerine sahip sunucu bir Windows kümesinin parçası değildir.

Sürüm 1810 ' den başlayarak, Configuration Manager Kurulum işlemi artık site sunucusu rolünün yük devretme kümelemesi için Windows rolü olan bir bilgisayara yüklenmesini engeller. SQL Always on bu rolü gerektirir, bu nedenle daha önce site sunucusundaki site veritabanını birlikte bulunduramıyorsunuz. Bu değişiklik ile, SQL Always on ve site sunucusu ' nu pasif modda kullanarak daha az sunucu ile yüksek oranda kullanılabilir bir site oluşturabilirsiniz. Daha fazla bilgi için bkz. [yüksek kullanılabilirlik seçenekleri](../configure/high-availability-options.md). <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE yüklendi

*Uygulama hedefi: SMS sağlayıcısı*

Windows ADK 'nin Windows Önyükleme Ortamı (PE) bileşeni yüklüdür.



## <a name="warnings"></a>Uyarılar

### <a name="active-directory-domain-functional-level"></a>Active Directory etki alanı işlev düzeyi

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Active Directory etki alanı ve orman işlev düzeyi en az Windows Server 2008 R2 'dir. Daha fazla bilgi için bkz. [Active Directory etki alanları Için destek](../../../plan-design/configs/support-for-active-directory-domains.md).

### <a name="administrative-rights-on-distribution-point"></a>Dağıtım noktasında yönetim hakları

*Uygulama hedefi: dağıtım noktası*

Kurulumu çalıştıran kullanıcı hesabının dağıtım noktasında **yönetici** hakları vardır.

### <a name="administrative-rights-on-management-point"></a>Yönetim noktasında yönetim hakları

*Uygulama hedefi: yönetim noktası, dağıtım noktası*

Site sunucusunun bilgisayar hesabı, yönetim noktası ve dağıtım noktası üzerinde **yönetici** haklarına sahiptir.

### <a name="administrative-share-site-system"></a>Yönetimsel paylaşma (site sistemi)

*Uygulama hedefi: yönetim noktası*

Site sistemi bilgisayarında gerekli yönetim paylaşımları vardır.

### <a name="application-compatibility"></a>Uygulama uyumluluğu

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Geçerli uygulamalar uygulama şeması ile uyumludur.

### <a name="backlogged-inboxes"></a>Biriktirme listesindeki gelen kutuları

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Site sunucusu kritik gelen kutularını zamanında işliyor. Gelen kutuları bir günden daha eski dosyalar içermiyor.

Aşağıdaki gelen kutusu klasörlerini denetler:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Bu uyarıyı çözmek için, biriktiriciden çıkartma ve Scheduler site sistemi bileşenlerinin çalışıp çalışmadığını denetleyin.

### <a name="bits-installed"></a>BITS yüklendi

*Uygulama hedefi: yönetim noktası*

Arka Plan Akıllı Aktarım Hizmeti (BITS) IIS 'de yüklenir ve etkinleştirilir.

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>Sitenin Yükseltme Hazırlığı Cloud Service bağlayıcısını kullanıp kullanmadığını denetleyin

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Yükseltme Hazırlığı hizmeti 31 Ocak 2020 itibariyle kullanımdan kalkmışsa. Daha fazla bilgi için bkz. [KB 4521815: Windows Analytics emekli on 31 ocak 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Masaüstü analizi, Windows Analytics 'in gelişmidir. Daha fazla bilgi için bkz. [Masaüstü analizi nedir?](../../../../desktop-analytics/overview.md)

Configuration Manager sitenizin Yükseltme Hazırlığı bağlantısı varsa, bunu kaldırmanız ve istemcileri yeniden yapılandırmanız gerekir. Daha fazla bilgi için bkz. [yükseltme hazırlığı bağlantısını kaldırma](../../../clients/manage/upgrade-readiness.md#bkmk_remove).

Bu önkoşul uyarısını yoksayarsanız, Configuration Manager Kurulum Yükseltme Hazırlığı bağlayıcısını otomatik olarak kaldırır.<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>Bulut yönetimi ağ geçidi, belirteç tabanlı kimlik doğrulaması veya HTTPS yönetim noktası gerektirir

*Uygulama hedefi: bulut yönetimi ağ geçidi*

Bazı Configuration Manager sürümleriyle, bulut yönetimi ağ geçidi (CMG) ile HTTP yönetim noktası kullanamazsınız. HTTPS için CMG 'yi yapılandırın ya da siteyi gelişmiş HTTP için yapılandırın. Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidini planlayın](../../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="configuration-for-sql-server-memory-usage"></a>SQL Server bellek kullanımı yapılandırması

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server, sınırsız bellek kullanımı için yapılandırılır. SQL Server belleği, en yüksek sınıra sahip olacak şekilde yapılandırın.

### <a name="distribution-point-package-version"></a>Dağıtım noktası paket sürümü

*Uygulama hedefi: dağıtım noktaları*

Sitedeki tüm dağıtım noktaları yazılım dağıtım paketlerinin en son sürümüne sahiptir.

### <a name="domain-membership-warning"></a>Etki alanı üyeliği (uyarı)

*Uygulama hedefi: yönetim noktası, dağıtım noktası*

Configuration Manager bilgisayar bir Windows etki alanının üyesidir.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>SQL Server için güvenlik duvarı özel durumu (tek başına birincil site)

*Uygulama hedefi: birincil site (yalnızca tek başına)*

Windows güvenlik duvarı devre dışı bırakıldı veya SQL Server için ilgili bir Windows Güvenlik Duvarı özel durumu var.

Sqlservr.exe veya gerekli TCP bağlantı noktalarına uzaktan erişilmesine izin verin. Varsayılan olarak, SQL Server TCP bağlantı noktası 1433 ' i dinler ve sunucu Hizmet Aracısı (SSB), TCP bağlantı noktası 4022 ' i kullanır.

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Yönetim noktası SQL Server için güvenlik duvarı özel durumu

*Uygulama hedefi: yönetim noktası*

Windows güvenlik duvarı devre dışı bırakıldı veya SQL Server için ilgili bir Windows Güvenlik Duvarı özel durumu var.

### <a name="iis-https-configuration"></a>IIS HTTPS yapılandırması

*Uygulama hedefi: yönetim noktası, dağıtım noktası*

IIS Web sitesinde HTTPS iletişim protokolü bağlamaları vardır.

HTTPS gerektiren site rolleri yüklediğinizde, belirtilen sunucuda IIS site bağlamalarını geçerli bir ortak anahtar altyapısı (PKI) sertifikasıyla yapılandırın.

### <a name="invalid-discovery-records"></a>Geçersiz bulma kayıtları

*Uygulama hedefi: merkezi yönetim sitesi*

Artık geçerli olmayan bulma kayıtları var. Bu kayıtlar silinmek üzere işaretlenir.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Çekirdek Hizmetleri 6,0 (MSXML60)

*Merkezi Yönetim sitesi, birincil site, ikincil site, Configuration Manager konsolu, yönetim noktası, dağıtım noktası için geçerlidir.*

MSXML 6,0 veya sonraki bir sürümün yüklü olduğunu doğrular.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>Ağ Erişim Koruması (NAP) artık desteklenmiyor

*Uygulama hedefi: birincil site*

NAP için etkinleştirilmiş yazılım güncelleştirmesi yok.

### <a name="ntfs-drive-on-site-server"></a>Site sunucusundaki NTFS sürücüsü

*Uygulama hedefi: birincil site*

Disk sürücüsü NTFS dosya sistemiyle biçimlendirilir. Daha iyi güvenlik için site sunucusu bileşenlerini NTFS dosya sistemiyle biçimlendirilen disk sürücülerine yüklersiniz.

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a> Bekleyen yapılandırma öğesi İlkesi güncelleştirmeleri

<!--SCCMDocs-pr issue 2814-->

*Uygulama hedefi: birincil site*

Sürüm 1806 ' den başlayarak, sürüm 1706 veya sonraki bir sürümden güncelleştiriyorsanız, çok sayıda uygulama dağıtımınız varsa ve bunlardan en az biri onay gerektiriyorsa bu uyarıyı görebilirsiniz.

İki seçeneğiniz vardır:  

- Uyarıyı yoksayın ve güncelleştirmeye devam edin. Bu eylem, ilkeleri işlerken güncelleştirme sırasında site sunucusunda daha yüksek işleme oluşmasına neden olur. Ayrıca, güncelleştirmeden sonra yönetim noktasında daha fazla işlemci yükü görebilirsiniz.  

- Gereksinim olmayan uygulamalardan birini veya belirli bir işletim sistemi gereksinimini gözden geçirin. Site sunucusundaki bazı yükün bu sırada ön işlemesi. **Objreplmgr. log**öğesini gözden geçirin ve ardından Yönetim noktasındaki işlemciyi izleyin. İşlem tamamlandıktan sonra siteyi güncelleştirin. Güncelleştirmeden sonra bazı ek işlemler olmaya devam eder, ancak ilk seçenekle uyarıyı yoksaymanız durumunda küçüktür.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Uzak SQL Server sistem yeniden başlatması bekleniyor

*Uygulama hedefi: sürüm 1902 ve üzeri, uzak SQL Server*

Kurulumu çalıştırmadan önce, başka bir program sunucunun yeniden başlatılmasını gerektiriyor.

Bilgisayarın bekleyen bir yeniden başlatma durumunda olup olmadığını görmek için, aşağıdaki kayıt defteri konumlarını denetler:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>Site sunucusunda PowerShell 2,0

*Uygulama hedefi: Exchange Connector ile birincil site*

Windows PowerShell 2,0 veya sonraki bir sürümü, site sunucusuna Configuration Manager Exchange Bağlayıcısı için yüklendi.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>İkincil sitede uzaktan WMI bağlantısı

*Uygulama hedefi: Ikincil site*

Kurulum, ikincil site sunucusunda WMI ile uzak bağlantı kurabilir.

### <a name="schema-extensions"></a>Şema uzantıları

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Active Directory şeması genişletildi. Genişletilmişse, kullanılan şema uzantılarının sürümü.

Configuration Manager, site sunucusu yüklemesi için Active Directory şema uzantıları gerektirmez. Microsoft, tüm Configuration Manager özelliklerinin tam kullanımını önerir. Şemayı genişletmenin avantajları hakkında daha fazla bilgi için bkz. [site yayımlama için Active Directory hazırlama](../../../plan-design/network/extend-the-active-directory-schema.md).

### <a name="share-name-in-package"></a>Paketteki paylaşma adı

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Paketler, gibi, paylaşma adında geçersiz karakterler içermez `#` .

### <a name="site-system-to-sql-server-communication"></a>SQL Server iletişim için site sistemi

*Uygulama hedefi: Ikincil site, yönetim noktası*

Site veritabanı örneği için SQL Server hizmetini çalıştırmak üzere yapılandırdığınız hesabın, Active Directory Domain Services geçerli bir hizmet asıl adı (SPN) vardır. Kerberos kimlik doğrulamasını desteklemek için Active Directory geçerli bir SPN kaydedin.

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a> Değişiklik izleme temizlemeyi SQL Server

*Uygulama hedefi: site veritabanı sunucusu*

Sürüm 1810 ' den başlayarak, site veritabanının SQL değişiklik izleme verileri biriktirme listesine sahip olup olmadığını denetleyin.<!--SCCMDocs-pr issue 3023-->  

Site veritabanında bir tanılama saklı yordamı çalıştırarak bu denetimi el ile doğrulayın. İlk olarak, site veritabanınıza bir [Tanılama bağlantısı](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) oluşturun. En kolay yöntem SQL Server Management Studio Veritabanı Altyapısı sorgu düzenleyicisini kullanmak ve ' a bağlanmak `admin:<instance name>` .

Adanmış yönetici bağlantısı sorgu penceresinde aşağıdaki komutları çalıştırın:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

Veritabanınızın boyutuna ve biriktirme listesi boyutuna bağlı olarak, bu saklı yordam birkaç dakika veya birkaç saat içinde çalışabilir. Sorgu tamamlandığında, biriktirme listesi ile ilgili verilerin iki bölümünü görürsünüz. **CT_Days_Old**ilk bakış. Bu değer, syscommittab tablonuzda en eski girdinin yaşını (gün) bildirir. Bu, Configuration Manager varsayılan değer olan beş gün olmalıdır. Bu varsayılan değeri değiştirmeyin. Ağır veri işleme veya çoğaltma sırasında, syscommittab 'daki en eski giriş beş günden fazla olabilir. Bu değer yedi günden daha üstündeyse, değişiklik izleme verilerini el ile temizleme işlemini çalıştırın.  

Değişiklik izleme verilerini temizlemek için adanmış yönetim bağlantısında aşağıdaki komutu çalıştırın:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Bu komut syscommittab ve tüm ilişkili yan tabloları temizleme işlemini başlatır. Bu, birkaç dakika veya birkaç saat içinde çalışabilir. İlerleme durumunu izlemek için, **Vlogs** görünümünü sorgulayın. Geçerli ilerlemeyi görmek için aşağıdaki sorguyu çalıştırın:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. SQL Server Native Client güncelleştirme, site yüklemesi işlemini etkileyebilecek bir yeniden başlatma gerektirebilir.

Bu denetim, site sunucusunun SQL Native Client desteklenen bir sürümüne sahip olduğundan emin olmanızı sağlar. Önkoşul denetimi, uzak site sistemlerindeki SQL Native Client sürümünü doğrulamaz.

En düşük sürüm SQL 2012 SP4 () ' dir `11.*.7001.0` . Bu SQL Native Client sürümü TLS 1,2 ' i destekler. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Microsoft SQL Server için TLS 1,2 desteği](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Configuration Manager için TLS 1,2 nasıl etkinleştirilir](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager aşağıdaki site sistem rollerinde SQL Server Native Client kullanır:<!-- SCCMDocs issue 1150 -->

- Site veritabanı sunucusu
- Site sunucusu: merkezi yönetim sitesi, birincil site veya ikincil site
- Yönetim noktası
- Cihaz yönetim noktası
- Durum Geçiş noktası
- site veritabanı
- Yazılım güncelleştirme noktası
- Çok noktaya yayını destekleyen dağıtım noktası
- Varlık Yönetim Bilgileri güncelleştirme hizmet noktası
- Raporlama hizmetleri noktası
- Uygulama Kataloğu Web hizmeti
- Kayıt noktası
- Uç Nokta Koruma noktası
- Hizmet bağlantı noktası
- Sertifika kayıt noktası
- Veri ambarı hizmet noktası

### <a name="sql-server-process-memory-allocation"></a>İşlem belleği ayırmayı SQL Server

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server, merkezi yönetim sitesi ve birincil site için en az 8 GB bellek ve ikincil site için en az 4 GB bellek ayırır.

Daha fazla bilgi için bkz. [SQL Server Management Studio kullanarak bellek seçeneklerini yapılandırma](/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-).

> [!NOTE]  
> Bu denetim, ikincil bir sitede SQL Server Express için geçerli değildir. Bu sürüm, 1 GB ayrılmış bellekle sınırlıdır.  

### <a name="sql-server-security-mode"></a>SQL Server güvenlik modu

*Uygulama hedefi: site veritabanı sunucusu*

SQL Server, Windows kimlik doğrulaması güvenliği için yapılandırılmıştır.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Yükseltme için desteklenmeyen site sistemi işletim sistemi sürümü

*Uygulama hedefi: birincil site, ikincil site*

Dağıtım noktaları dışındaki site sistem rolleri, Windows Server 2012 veya üstünü çalıştıran sunuculara yüklenir.

Daha fazla bilgi için bkz. [Configuration Manager site sistemi sunucuları Için desteklenen işletim sistemleri](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

> [!NOTE]  
> Bu denetim, Azure 'da yüklü olan site sistem rollerinin durumunu veya Microsoft Intune tarafından kullanılan bulut depolama alanı için çözemez. Bu rollere yönelik uyarıları hatalı pozitif sonuçlar olarak yoksayın.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>Yükseltme değerlendirmesi araç seti desteklenmiyor

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Yükseltme değerlendirmesi Araç Seti yüklü değil. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Active Directory yayımlamak için site sunucusu izinlerini doğrulayın

*Uygulama hedefi: merkezi yönetim sitesi, birincil site, ikincil site*

Site sunucusunun bilgisayar hesabı, Active Directory etki alanındaki **sistem yönetimi** kapsayıcısı Için **tam denetim** izinlerine sahiptir.

Daha fazla bilgi için bkz. [site yayımlama için Active Directory hazırlama](../../../plan-design/network/extend-the-active-directory-schema.md).

> [!NOTE]  
> İzinleri el ile doğrularsınız, bu uyarıyı yoksayabilirsiniz.

### <a name="windows-remote-management-winrm-v11"></a>Windows Uzaktan Yönetimi (WinRM) v 1.1

*Uygulama hedefi: birincil site, Configuration Manager konsolu*

WinRM 1,1, bant dışı yönetim konsolunu çalıştırmak için birincil site sunucusunda veya Configuration Manager konsol bilgisayarında yüklüdür.

WinRM, Windows 'un şu anda desteklenen tüm sürümleriyle otomatik olarak yüklenir. Daha fazla bilgi için bkz. [Windows Uzaktan Yönetimi Için yükleme ve yapılandırma](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### <a name="wsus-on-site-server"></a>Site sunucusundaki WSUS

*Uygulama hedefi: merkezi yönetim sitesi, birincil site*

Site sunucusunda Windows Server Update Services 'in (WSUS) desteklenen bir sürümü yüklü.

Site sunucusu dışında bir sunucuda yazılım güncelleştirme noktası kullandığınızda, WSUS Yönetim konsolunu site sunucusuna yüklemelisiniz. WSUS hakkında daha fazla bilgi için bkz. [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).