---
title: Günlük dosyası başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager istemci, sunucu ve bağımlı bileşenler için tüm günlük dosyalarına bir başvuru.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f8ad6827a1aa72c3aaa51e21fecbf639fbb405
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715586"
---
# <a name="log-file-reference"></a>Günlük dosyası başvurusu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, istemci ve site sunucusu bileşenleri işlem bilgilerini ayrı günlük dosyalarına kaydeder. Ortaya çıkabilecek sorunları gidermenize yardımcı olması için bu günlük dosyalarındaki bilgileri kullanabilirsiniz. Varsayılan olarak, Configuration Manager istemci ve sunucu bileşenleri için günlüğe kaydetmeye izin vermez.

Configuration Manager günlük dosyaları hakkında daha fazla genel bilgi için bkz. [günlük dosyaları hakkında](about-log-files.md). Bu makale, kullanılacak araçlar, günlüklerin nasıl yapılandırılacağı ve nerede bulunacağı hakkında bilgi içerir.

Aşağıdaki bölümler, size sunulan farklı günlük dosyaları hakkında ayrıntılar sağlar. İşlem ayrıntıları için istemci ve sunucu günlüklerini Configuration Manager izleyin ve sorun gidermek için hata bilgilerini görüntüleyin.  

- [İstemci günlük dosyaları](#BKMK_ClientLogs)  

  - [İstemci işlemleri](#BKMK_ClientOpLogs)  

  - [İstemci yüklemesi](#BKMK_ClientInstallLog)  

  - [Linux ve UNIX İstemcisi](#BKMK_LogFilesforLnU)  

  - [Mac bilgisayarlar için istemci](#BKMK_LogfilesforMac)  

- [Sunucu günlük dosyaları](#BKMK_ServerLogs)  

  - [Site sunucusu ve site sistemleri](#BKMK_SiteSiteServerLog)  

  - [Site sunucusu yüklemesi](#BKMK_SiteInstallLog)

  - [Veri ambarı hizmet noktası](#BKMK_DataWarehouse)

  - [Geri dönüş durumu noktası](#BKMK_FSPLog)  

  - [Yönetim noktası](#BKMK_MPLog)  

  - [Hizmet bağlantı noktası](#BKMK_WITLog)  

  - [Yazılım güncelleştirme noktası](#BKMK_SUPLog)  

- [İşlevlere göre günlük dosyaları](#BKMK_FunctionLogs)  

  - [Uygulama yönetimi](#BKMK_AppManageLog)  

  - [Varlık Yönetim Bilgileri](#BKMK_AILog)  

  - [Yedekleme ve kurtarma](#BKMK_BnRLog)  

  - [Sertifika kaydı](#BKMK_CertificateEnrollment)

  - [İstemci bildirimi](#BKMK_BGB)

  - [Bulut yönetimi ağ geçidi](#cloud-management-gateway)

  - [Uyumluluk ayarları ve şirket kaynağı erişimi](#BKMK_CompSettingsLog)  

  - [Configuration Manager konsolu](#BKMK_ConsoleLog)  

  - [İçerik yönetimi](#BKMK_ContentLog)  

  - [Desktop Analytics](#desktop-analytics)

  - [Keşfini](#BKMK_DiscoveryLog)  

  - [Endpoint Protection](#BKMK_EPLog)  

  - [Uzantılar](#BKMK_Extensions)  

  - [Sayım](#BKMK_InventoryLog)  

  - [Geçiş](#BKMK_MigrationLog)  

  - [Mobil cihazlar](#BKMK_MDMLog)  

  - [İşletim sistemi dağıtımı](#BKMK_OSDLog)  

  - [Güç yönetimi](#BKMK_PowerMgmtLog)  

  - [Uzaktan denetim](#BKMK_RCLog)  

  - [Raporlama](#BKMK_ReportLog)  

  - [Rol tabanlı yönetim](#BKMK_RBALog)  

  - [Yazılım kullanım ölçümü](#BKMK_MeteringLog)  

  - [Yazılım güncelleştirmeleri](#BKMK_SU_NAPLog)  

  - [LAN'da Uyandırma](#BKMK_WOLLog)  

  - [Windows 10 Bakımı](#BKMK_WindowsServicingLog)

  - [Windows Update Aracısı](#BKMK_WULog)  

  - [WSUS sunucusu](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a>İstemci günlük dosyaları

Aşağıdaki bölümlerde, istemci işlemleriyle ve istemci yüklemesiyle ilgili günlük dosyaları listelenmektedir.  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a>İstemci işlemleri

Aşağıdaki tabloda Configuration Manager istemcisinde bulunan günlük dosyaları listelenmektedir.  

|Günlük adı|Description|  
|--------------|-----------------|  
|ADALOperationProvider. log|Azure Active Directory (Azure AD) kimlik doğrulama kitaplığı (ADAL) ile istemci kimlik doğrulama belirteci istekleri hakkında bilgi.|
|BitLockerManagementHandler. log|BitLocker yönetim ilkeleriyle ilgili bilgileri kaydeder.|
|CAS.log|Içerik erişim hizmeti. İstemcideki yerel paket önbelleğini bulundurur.|  
|Ccm32BitLauncher.log|İstemci üzerinde *farklı çalıştır 32 bit olarak*işaretlenmiş uygulamaları başlatmaya yönelik eylemleri kaydeder.|  
|CcmEval.log|İstemci durumu değerlendirme etkinliklerini ve Configuration Manager istemcisinin gerektirdiği bileşenlere ilişkin ayrıntıları Configuration Manager kaydeder.|  
|CcmEvalTask.log|Zamanlanan değerlendirme görevi tarafından başlatılan Configuration Manager istemci durumu değerlendirme etkinliklerini kaydeder.|  
|CcmExec.log|İstemcinin ve SMS Aracı Ana Makinesi hizmetinin etkinliklerini kaydeder. Bu günlük dosyası, ayrıca uyandırma proxy'sini etkinleştirme ve devre dışı bırakma hakkında bilgiler içerir.|  
|CcmMessaging.log|İstemci ile yönetim noktaları arasındaki iletişimlerle ilgili etkinlikleri kaydeder.|  
|CCMNotificationAgent.log|İstemci bildirim işlemleriyle ilgili etkinlikleri kaydeder.|  
|Ccmperf.log|İstemci performans sayaçlarıyla ilgili verilerin bakımı ve yakalanmasıyla ilgili etkinlikleri kaydeder.|  
|CcmRestart.log|İstemci hizmet yeniden başlatma etkinliğini kaydeder.|  
|CCMSDKProvider.log|İstemci SDK arabirimleriyle ilgili etkinlikleri kaydeder.|  
|ccmsqlce. log|İstemcinin kullandığı SQL Compact Edition için etkinlikleri kaydeder. Bu günlük genellikle yalnızca hata ayıklama günlüğünü etkinleştirdiğinizde kullanılır veya bileşenle ilgili bir sorun vardır. İstemci sistem durumu görevi (ccmeval) genellikle bu bileşenle ilgili sorunları kendi kendine düzeltir.|
|CertificateMaintenance.log|Active Directory Etki Alanı Hizmetleri ve yönetim noktalarına yönelik sertifikaları bulundurur.|  
|CIDownloader.log|Yapılandırma öğesi tanım indirmeleri hakkındaki ayrıntıları kaydeder.|  
|CITaskMgr.log|İçerik indirme ve yükleme ya da kaldırma eylemleri gibi her uygulama ve dağıtım türü için görevleri kaydeder.|  
|ClientAuth.log|İstemci için imzalama ve kimlik doğrulama etkinliğini kaydeder.|  
|ClientIDManagerStartup.log|İstemci GUID 'sini oluşturur ve korur ve istemci kaydı ve ataması sırasında görevleri tanımlar.|  
|ClientLocation.log|İstemci site atamasıyla ilişkili görevleri kaydeder.|  
|CMHttpsReadiness.log|Configuration Manager HTTPS hazırlık değerlendirme aracı 'nı çalıştırmanın sonuçlarını kaydeder. Bu araç, bilgisayarların Configuration Manager ile kullanılabilecek bir ortak anahtar altyapısı (PKI) istemci kimlik doğrulama sertifikasına sahip olup olmadığını denetler.|  
|CmRcService.log|Uzaktan denetim hizmetine yönelik bilgileri kaydeder.|  
|CoManagementHandler. log|İstemcide ortak yönetimin sorunlarını gidermek için kullanın.|
|ContentTransferManager.log|Paketleri indirmek veya yüklenmek üzere Arka Plan Akıllı Aktarım Hizmeti (BITS) veya sunucu Ileti bloğu (SMB) zamanlar.|  
|DataTransferService.log|İlke veya paket erişimine ilişkin tüm BITS iletişimini kaydeder.|  
|DeltaDownload. log|Dağıtım Iyileştirmesi kullanılarak indirilen hızlı güncelleştirme ve güncelleştirmelerin indirilmesi hakkındaki bilgileri kaydeder.|  
|Diagnostics. log|İstemci tanılama eylemlerinin durumunu kaydeder.|
|EndpointProtectionAgent|System Center Endpoint Protection istemcisinin yüklenmesiyle ilgili bilgileri ve bu istemciye kötü amaçlı yazılımdan koruma İlkesi uygulamasını kaydeder.|  
|execmgr.log|İstemci üzerinde çalışan paketler ve görev dizileri ile ilgili ayrıntıları kaydeder.|  
|ExpressionSolver.log|Ayrıntılı veya hata ayıklama günlüğü açıldığında kullanılan gelişmiş algılama yöntemleriyle ilgili ayrıntıları kaydeder.|  
|ExternalEventAgent.log|Uç Nokta Koruma kötü amaçlı yazılım algılama geçmişini ve istemci durumu ile ilgili olayları kaydeder.|  
|FileBITS.log|Tüm SMB paketi erişim görevlerini kaydeder.|  
|FileSystemFile.log|Yazılım envanteri ve dosya koleksiyonuna yönelik Windows Yönetim Araçları (WMI) sağlayıcısının etkinliğini kaydeder.|  
|FSPStateMessage.log|İstemci tarafından geri dönüş durum noktasına gönderilen durum iletilerine yönelik etkinliği kaydeder.|  
|InternetProxy.log|İstemci için ağ proxy yapılandırmasını ve kullanım etkinliğini kaydeder.|  
|InventoryAgent.log|Donanım envanteri, yazılım envanteri etkinliklerini ve istemci üzerindeki sinyal bulma işlemlerini kaydeder.|  
|LocationCache.log|Konum önbelleği kullanımı ve istemci için bakım etkinliklerini kaydeder.|  
|LocationServices.log|Yönetim noktaları, yazılım güncelleştirme noktaları ve dağıtım noktalarına yönelik istemci etkinliğini kaydeder.|  
|M365AHandler. log|Masaüstü Analizi ayarları ilkesiyle ilgili bilgiler|
|MaintenanceCoordinator.log|İstemci için genel bakım görevlerine yönelik etkinliği kaydeder.|  
|Mifprovider.log|Yönetim bilgisi biçimi (MIF) dosyaları için WMI sağlayıcısı etkinliğini kaydeder.|  
|mtrmgr.log|Tüm yazılım kullanım ölçümü işlemlerini izler.|  
|PolicyAgent.log|Veri Aktarımı hizmeti kullanılarak yapılan ilkelere yönelik istekleri kaydeder.|  
|PolicyAgentProvider.log|İlke değişikliklerini kaydeder.|  
|PolicyEvaluator.log|Yazılım güncelleştirmelerindeki ilkeler dahil olmak üzere istemci bilgisayarlardaki ilkelerin değerlendirilmesiyle ilgili ayrıntıları kaydeder.|  
|PolicyPlatformClient.log|Dosya sağlayıcısı dışında \Program Files\Microsoft Policy platform ' da bulunan tüm sağlayıcılar için düzeltme ve uyumluluk sürecini kaydeder.|  
|PolicySdk.log|İlke sistemi SDK arabirimleriyle ilgili etkinlikleri kaydeder.|  
|Pwrmgmt.log|Uyandırma proxy'si istemci ayarlarını etkinleştirme veya devre dışı bırakma ve yapılandırma ile ilgili bilgileri kaydeder.|  
|PwrProvider.log|WMI hizmetinde barındırılan güç yönetimi sağlayıcısının (Pwrınvprovider) etkinliklerini kaydeder. Windows'un tüm desteklenen sürümlerinde, sağlayıcı, donanım envanter kaydı sırasında bilgisayarlardaki geçerli ayarların listesini oluşturur ve güç planı ayarlarını uygular.|  
|SCClient_ &lt; *etki alanı* \> @ &lt; *Kullanıcı adı* \> _1. log|İstemci bilgisayardaki belirtilen kullanıcı için Yazılım Merkezi'ndeki etkinliği kaydeder.|  
|SCClient_ &lt; *etki alanı* \> @ &lt; *Kullanıcı adı* \> _2. log|İstemci bilgisayardaki belirtilen kullanıcı için Yazılım Merkezi'ndeki etkinlik geçmişini kaydeder.|  
|Scheduler.log|Tüm istemci işlemlerine yönelik zamanlanmış görevlerin etkinliklerini kaydeder.|  
|SCNotify_ &lt; *etki alanı* \> @ &lt; *Kullanıcı adı* \> _1. log|Belirtilen kullanıcıya yönelik yazılımları kullanıcılara bildirme etkinliğini kaydeder.|  
|SCNotify_ &lt; *etki alanı* \> @ &lt; *Kullanıcı adı* \> _1- &lt; *date_time*>. log|Belirtilen kullanıcıya yönelik yazılımları kullanıcılara bildirmeye yönelik geçmiş bilgileri kaydeder.|  
|setuppolicyevaluator.log|WMI'de yapılandırma ve envanter ilkesi oluşturma bilgilerini kaydeder.|  
|SleepAgent_ &lt; *etki alanı*\>@SYSTEM_0.log|Uyandırma proxy 'si için ana günlük dosyası.|  
|smscliui.log|Denetim Masası 'nda Configuration Manager istemcisinin kullanımını kaydeder.|  
|SrcUpdateMgr.log|Geçerli dağıtım noktası kaynağı konumlarıyla güncelleştirilen yüklü Windows Installer uygulamalarına yönelik etkinliği kaydeder.|  
|StatusAgent.log|İstemci bileşenleri tarafından oluşturulan durum iletilerini kaydeder.|  
|SWMTRReportGen.log|Ölçüm Aracısı tarafından toplanan kullanım verileri raporunu oluşturur. Bu veriler Mtrmgr.log günlüğüne kaydedilir.|  
|UserAffinity.log|Kullanıcı aygıtı benzeşimi ile ilgili ayrıntıları kaydeder.|  
|VirtualApp.log|Application Virtualization (App-V) dağıtım türlerinin değerlendirmesine özgü bilgileri kaydeder.|  
|Wedmtrace.log|Windows Embedded istemcilerdeki yazma filtreleri ile ilgili işlemleri kaydeder.|  
|wakeprxy-install.log|İstemciler, uyandırma proxy 'sini açmak için istemci ayarı seçeneğini aldığınızda yükleme bilgilerini kaydeder.|  
|wakeprxy-uninstall.log|Uyandırma proxy 'si önceden açıldıysa uyandırma proxy 'sini devre dışı bırakmak için istemciler istemci ayarı seçeneğini aldıktan sonra uyandırma proxy 'sini kaldırma ile ilgili bilgileri kaydeder.|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a>İstemci yüklemesi

Aşağıdaki tabloda, Configuration Manager istemcisinin yüklenmesiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|  
|--------------|-----------------|  
|ccmsetup.log|İstemci kurulumu, istemci yükseltmesi ve istemci kaldırma için ccmsetup.exe görevleri kaydeder. İstemci yükleme sorunlarını gidermek için kullanılabilir.|  
|ccmsetup-ccmeval.log|İstemci durumu ve düzeltme için ccmsetup.exe görevleri kaydeder.|  
|CcmRepair.log|İstemci aracısının onarım etkinliklerini kaydeder.|  
|client.msi.log|client.msi tarafından gerçekleştirilen kurulum görevlerini kaydeder. İstemci yükleme veya kaldırma sorunlarını gidermek için kullanılabilir.|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a>Linux ve UNIX için istemcisi

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez.
>
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

Linux ve UNIX için Configuration Manager istemcisi, bilgileri aşağıdaki günlük dosyalarında kaydeder:  

> [!TIP]
> Linux ve UNIX için istemci günlük dosyalarını görüntülemek için CMTrace ' i kullanın.

|Günlük adı|Ayrıntılar|
|-------------------|-----------------------------------------------------------------|
|Scxcm. log| Linux ve UNIX için Configuration Manager istemcisinin çekirdek hizmetine yönelik günlük dosyası (Ccmexec. bin). Bu günlük dosyası, ccmexec.bin'in yüklenmesi ve devam eden işlemleri ile ilgili bilgileri içerir. Varsayılan olarak, bu günlük dosyası **/var/opt/microsoft/scxcm.log**adresinde bulunur. Günlük dosyasının konumunu değiştirmek için **/opt/microsoft/configmgr/etc/scxcm.conf** yolunu düzenleyin ve **YOL** alanını değiştirin. Değişikliğin etkili olması için istemci bilgisayarı veya hizmeti yeniden başlatmanız gerekmez. Günlük düzeyini dört farklı ayarlardan birine ayarlayabilirsiniz. |
| Scxcmprovider. log |Linux ve UNIX için Configuration Manager istemcisinin CıM hizmetine yönelik günlük dosyası (omiserver. bin). Bu günlük dosyası, nwserver.bin'in devam eden işlemleri ile ilgili bilgiler içerir. Bu günlük konumunda bulunur `/var/opt/microsoft/configmgr/scxcmprovider.log` . Günlük dosyasının konumunu değiştirmek için **/opt/microsoft/omi/etc/scxcmprovider.conf** dosyasını düzenleyin ve **YOL** alanını değiştirin. Değişikliğin etkili olması için istemci bilgisayarı veya hizmeti yeniden başlatmanız gerekmez. Günlük düzeyini üç ayarlardan birine ayarlayabilirsiniz.|

Her iki günlük dosyası da birkaç günlük tutma düzeyini destekler:  

- **scxcm. log**. Günlük düzeyini değiştirmek için **/opt/Microsoft/ConfigMgr/etc/scxcm.conf yolunu** düzenleyin ve **Modül** etiketinin her bir örneğini istediğiniz günlük düzeyine değiştirin:  

  - Hata: dikkat gerektiren sorunları gösterir  

  - Uyarı: istemci işlemlerinde olası sorunları gösterir  

  - BILGI: istemcideki çeşitli olayların durumunu gösteren daha ayrıntılı günlük kaydı  

  - Izleme: genellikle sorunları tanılamak için kullanılan ayrıntılı günlük  

- **scxcmprovider. log**. Günlük düzeyini değiştirmek için **/opt/Microsoft/Omi/etc/scxcmprovider.conf dosyasını** düzenleyin ve **Modül** etiketinin her bir örneğini istediğiniz günlük düzeyine değiştirin:  

  - Hata: dikkat gerektiren sorunları gösterir  

  - Uyarı: istemci işlemlerinde olası sorunları gösterir

  - BILGI: istemcideki çeşitli olayların durumunu gösteren daha ayrıntılı günlük kaydı  

Normal işletim koşulları altında hata günlüğü düzeyini kullanın. Bu günlük düzeyi en küçük günlük dosyasını oluşturur. Günlük düzeyi hata durumundan uyarı, BILGI ve sonra Izleme olarak arttığı için, dosyaya daha fazla veri yazıldığı için daha büyük bir günlük dosyası oluşturulur.  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a>Linux ve UNIX istemcisi için günlük dosyalarını yönetme

Linux ve UNIX için istemcisi, istemci günlük dosyalarının maksimum boyutunu sınırlamaz. Ayrıca,. log dosyalarının içeriğini. lo_ dosyasına gibi başka bir dosyaya da otomatik olarak kopyalamaz. Günlük dosyalarının en büyük boyutunu denetlemek istiyorsanız, günlük dosyalarını Linux ve UNIX için Configuration Manager istemcisinden bağımsız olarak yönetmek üzere bir işlem uygulayın.  

Örneğin, istemci günlük dosyalarının boyutunu ve döndürmesini yönetmek için **logrotate** standart LINUX ve UNIX komutunu kullanabilirsiniz. Linux ve UNIX için Configuration Manager istemcisinde, **logrotate** 'in, günlük döndürme işlemi tamamlandığında istemciye işaret etmesini sağlayan bir arabirimi bulunur, bu nedenle istemci günlük dosyasına kaydetmeye devam edebilir.  

**logrotate** hakkında daha fazla bilgi için kullandığınız Linux ve UNIX dağıtımlarının belgelerine bakın.  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a>Mac bilgisayarlar için istemci

Mac bilgisayarlar için Configuration Manager istemcisi, Mac bilgisayardaki aşağıdaki günlük dosyalarına bilgi kaydeder:  

|Günlük adı|Ayrıntılar|Konum|
|--------------|-------------|-------------|
|CCMClient- &lt; *date_time*>. log|Uygulama yönetimi, envanter ve hata günlüğü dahil olmak üzere Mac istemci işlemleriyle ilgili etkinlikleri kaydeder.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent- &lt; *date_time*>. log|Kullanıcı oturum açma ve oturumu kapatma işlemleri ve Mac bilgisayar etkinliği dahil olmak üzere istemci işlemleriyle ilgili bilgileri kaydeder.| `~/Library/Logs`|  
|CCMNotifications- &lt; *date_time*>. log|Mac bilgisayarda görüntülenen Configuration Manager bildirimleriyle ilgili etkinlikleri kaydeder.| `~/Library/Logs`|  
|CCMPrefPane- &lt; *date_time*>. log|Mac bilgisayardaki Configuration Manager tercihleri iletişim kutusuyla ilgili etkinlikleri kaydeder; bu, genel durum ve hata günlüğü içerir.| `~/Library/Logs`|  

Site sistem sunucusundaki **SMS_DM. log** dosyası, Mac bilgisayarlar ve mobil cihazlar ve Mac bilgisayarlar için ayarlanan yönetim noktası arasındaki iletişimi de kaydeder.  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a>Sunucu günlük dosyaları

Aşağıdaki bölümlerde, site sunucusunda bulunan veya belirli site sistemi rolleriyle ilişkili olan günlük dosyaları listelenmiştir.  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a>Site sunucusu ve site sistemleri

Aşağıdaki tabloda, Configuration Manager site sunucusunda ve site sistemi sunucularında bulunan günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Kayıt işleme etkinliğini kaydeder.|Site sunucusu|  
|ADForestDisc.log|Active Directory Orman Saptama eylemlerini kaydeder.|Site sunucusu|  
|adminservice. log|SMS Sağlayıcısı yönetim hizmeti REST API için eylemleri kaydeder|SMS Sağlayıcısı'nın bulunduğu bilgisayar|
|ADService.log|Active Directory'deki hesap oluşturma ve güvenlik grubu ayrıntılarını kaydeder.|Site sunucusu|  
|adsgdis.log|Active Directory Grup Saptama eylemlerini kaydeder.|Site sunucusu|  
|adsysdis.log|Active Directory Sistem Saptama eylemlerini kaydeder.|Site sunucusu|  
|adusrdis.log|Active Directory Kullanıcı Saptama eylemlerini kaydeder.|Site sunucusu|  
|BusinessAppProcessWorker. log|Iş uygulamaları için Microsoft Store işleme kaydeder.|Site sunucusu|
|ccm.log|İstemci gönderme yüklemesi için etkinlikleri kaydeder.|Site sunucusu|  
|CertMgr.log|Site içi iletişim için sertifika etkinliklerini kaydeder.|Site sistemi sunucusu|  
|chmgr.log|İstemci sistem durumu yöneticisinin etkinliklerini kaydeder.|Site sunucusu|  
|Cidm.log|İstemci Yükleme Verileri Yöneticisi (CIDM) tarafından istemci ayarlarına yapılan değişiklikleri kaydeder.|Site sunucusu|  
|CollectionAADGroupSyncWorker. log | Sürüm 2002 ' den başlayarak, koleksiyon üyeliği sonuçlarının Azure Active Directory ile eşitlenmesi için günlük dosyası. Sürüm 1910 ve önceki sürümlerde, bu özellik için günlüğe kaydetme SMS_AZUREAD_DISCOVERY_AGENT. log dosyasında birleştirilmiştir. | Site sunucusu|
|colleval.log|Koleksiyonların Koleksiyon Değerlendiricisi tarafından oluşturulduğu, değiştirildiği ve silindiği zamana dair ayrıntıları kaydeder.|Site sunucusu|  
|compmon.log|Site sunucusuna yönelik olarak izlenen bileşen iş parçacıklarının durumunu kaydeder.|Site sistemi sunucusu|  
|compsumm.log|Bileşen Durumu Özetleyicisi görevlerini kaydeder.|Site sunucusu|  
|ComRegSetup.log|Site sunucusunun ilk COM yükleme kaydı sonuçlarını kaydeder.|Site sistemi sunucusu|  
|dataldr.log|Configuration Manager veritabanındaki MIF dosyalarının ve donanım envanterinin işlenmesiyle ilgili bilgileri kaydeder.|Site sunucusu|  
|ddm.log|Discovery Data Manager'ın etkinliklerini kaydeder.|Site sunucusu|  
|despool.log|Siteler arası gelen iletişim aktarımlarını kaydeder.|Site sunucusu|  
|distmgr.log|Paket oluşturma, sıkıştırma, değişim çoğaltması ve bilgi güncelleştirmeleri ile ilgili bilgileri kaydeder. Ayrıca, dağıtım Yöneticisi bileşeninden diğer etkinlikleri de içerebilir. Örneğin, bir dağıtım noktası yükleme, bağlantı denemeleri ve bileşenleri yükleme. Bu günlüğü kullanan diğer işlevler hakkında daha fazla bilgi için bkz. [hizmet bağlantı noktası](#BKMK_WITLog) ve [işletim sistemi dağıtımı](#BKMK_OSDLog).|Site sunucusu|  
|EPCtrlMgr.log|Kötü amaçlı yazılım tehdit bilgilerinin Endpoint Protection site sistemi rol sunucusundan Configuration Manager veritabanıyla eşitlenmesi hakkındaki bilgileri kaydeder.|Site sunucusu|  
|EPMgr.log|Uç Nokta Koruma site sistemi rolünün durumunu kaydeder.|Site sistemi sunucusu|  
|EPSetup.log|Uç Nokta Koruma site sistemi rolünün yüklenmesiyle ilgili bilgileri sağlar.|Site sistemi sunucusu|  
|EnrollSrv.log|Kayıt hizmeti işleminin etkinliklerini kaydeder.|Site sistemi sunucusu|  
|EnrollWeb.log|Kayıt Web sitesi işleminin etkinliklerini kaydeder.|Site sistemi sunucusu|  
|fspmgr.log|Geri dönüş durum noktası site sistemi rolünün etkinliklerini kaydeder.|Site sistemi sunucusu|  
|hman.log|Site yapılandırma değişiklikleri ve site bilgilerinin Active Directory Domain Services Yayınlanma hakkındaki bilgileri kaydeder.|Site sunucusu|  
|Inboxast.log|Yönetim noktasından site sunucusundaki ilgili INBOXES klasörüne taşınan dosyaları kaydeder.|Site sunucusu|  
|inboxmgr.log|Gelen kutusu klasörleri arasındaki dosya taşıma etkinliklerini kaydeder.|Site sunucusu|  
|inboxmon.log|Gelen kutusu dosyalarının ve performans sayacı güncelleştirmelerinin işlenmesini kaydeder.|Site sunucusu|  
|invproc.log|MIF dosyalarının ikincil siteden üst siteye iletilmesini kaydeder.|Site sunucusu|  
|migmctrl.log|Geçiş işlerini, paylaşılan dağıtım noktalarını ve dağıtım noktası yükseltmelerini içeren geçiş eylemlerine yönelik bilgileri kaydeder.|Configuration Manager hiyerarşisindeki üst düzey site ve her alt birincil site. Çoklu birincil site hiyerarşisinde, merkezi yönetim sitesinde oluşturulan günlük dosyasını kullanın.|  
|mpcontrol.log|Yönetim noktasının kaydını Windows Internet ad hizmeti (WINS) ile kaydeder. Yönetim noktasının kullanılabilirliğini 10 dakikada bir kaydeder.|Site sistemi sunucusu|  
|mpfdm.log|İstemci dosyalarını site sunucusundaki ilgili INBOXES klasörüne taşıyan yönetim noktası bileşeni eylemlerini kaydeder.|Site sistemi sunucusu|  
|mpMSI.log|Yönetim noktası yüklemesiyle ilgili ayrıntıları kaydeder.|Site sunucusu|  
|MPSetup.log|Yönetim noktası yükleme sarmalayıcı işlemini kaydeder.|Site sunucusu|  
|netdisc.log|Ağ Bulma eylemlerini kaydeder.|Site sunucusu|  
|NotiCtrl. log|Uygulama isteği bildirimleri.|Site sunucusu|  
|ntsvrdis.log|Site sistemi sunucularının bulma etkinliğini kaydeder.|Site sunucusu|  
|Objreplmgr|Nesne değişikliği bildirimlerinin çoğaltma için işlenmesini kaydeder.|Site sunucusu|  
|offermgr.log|Tanıtım güncelleştirmelerini kaydeder.|Site sunucusu|  
|offersum.log|Dağıtım durumu iletilerinin özetini kaydeder.|Site sunucusu|  
|OfflineServicingMgr.log|İşletim sistemi görüntü dosyalarına güncelleştirme uygulama etkinliklerini kaydeder.|Site sunucusu|  
|outboxmon.log|Giden kutusu dosyalarının ve performans sayacı güncelleştirmelerinin işlenmesini kaydeder.|Site sunucusu|  
|PerfSetup.log|Performans sayaçlarının yüklenme sonuçlarını kaydeder.|Site sistemi sunucusu|  
|PkgXferMgr.log|Birincil siteden uzak dağıtım noktasına içerik göndermekten sorumlu SMS_Executive bileşeni eylemlerini kaydeder.|Site sunucusu|  
|policypv.log|İstemci ayarlarında veya dağıtımlarda yapılan değişiklikleri yansıtan istemci ilkesi güncelleştirmelerini kaydeder.|Birincil site sunucusu|  
|rcmctrl.log|Hiyerarşideki siteler arasında veritabanı çoğaltma etkinliklerini kaydeder.|Site sunucusu|  
|replmgr.log|Dosyaların site sunucusu bileşenleri ile Zamanlayıcı bileşeni arasında çoğaltılmasını kaydeder.|Site sunucusu|  
|ResourceExplorer.log|Hataları, uyarıları ve Kaynak Gezgini çalıştırma hakkındaki bilgileri kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  
|RESTPROVIDERSetup. log|SMS Sağlayıcısı yönetim hizmeti REST API yüklemesi|SMS Sağlayıcısı'nın bulunduğu bilgisayar|
|ruleengine.log|Tanımlama, içerik indirme ve yazılım güncelleştirme grubu ve dağıtım oluşturmaya yönelik otomatik dağıtım kurallarıyla ilgili ayrıntıları kaydeder.|Site sunucusu|  
|schedule.log|Siteler arası iş ve dosya çoğaltmayla ilgili ayrıntıları kaydeder.|Site sunucusu|  
|sender.log|Siteler arasında dosya tabanlı çoğaltma ile aktarılan dosyaları kaydeder.|Site sunucusu|  
|sinvproc.log|Yazılım envanteri verilerinin site veritabanına işlenmesiyle ilgili bilgileri kaydeder.|Site sunucusu|  
|sitecomp.log|Sitedeki tüm site sistemi sunucularındaki yüklü site bileşenlerinin bakımıyla ilgili ayrıntıları kaydeder.|Site sunucusu|  
|sitectrl.log|Veritabanındaki site denetim nesnelerinde yapılan site ayarı değişikliklerini kaydeder.|Site sunucusu|  
|sitestat.log|Tüm site sistemlerinin kullanılabilirliğini ve disk alanı izleme işlemini kaydeder.|Site sunucusu|
|SMS_AZUREAD_DISCOVERY_AGENT. log| Azure Active Directory (Azure AD) Kullanıcı ve Kullanıcı grubu bulma için günlük dosyası. Sürüm 1910 ve önceki sürümlerde, koleksiyon üyeliği sonuçlarının Azure AD 'ye eşitlenmesini de dahil edilmiştir.| Site sunucusu|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Iş için Microsoft Store uygulamaları eşitleyen bileşen için günlük dosyası.|Site sunucusu|
|SMS_ISVUPDATES_SYNCAGENT. log| Üçüncü taraf yazılım güncelleştirmelerinin eşitlenmesi için günlük dosyası.| Configuration Manager hiyerarşisindeki üst düzey yazılım güncelleştirme noktası.|
|SMS_OrchestrationGroup. log| Düzenleme grupları için günlük dosyası|Site sunucusu|
|SMS_PhasedDeployment. log| Aşamalı dağıtımlar için günlük dosyası|Configuration Manager hiyerarşisindeki üst düzey site|
|SMS_REST_PROVIDER. log|SMS Sağlayıcısı yönetim hizmeti REST API, sertifika bilgileri de dahil olmak üzere hizmet sistem durumu|SMS Sağlayıcısı'nın bulunduğu bilgisayar|
|SmsAdminUI.log|Konsol etkinliğine Configuration Manager kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  
|SMSAWEBSVCSetup.log|Uygulama Kataloğu Web hizmetinin yükleme etkinliklerini kaydeder.|Site sistemi sunucusu|  
|smsbkup.log|Site yedekleme işleminin çıktılarını kaydeder.|Site sunucusu|  
|smsdbmon.log|Veritabanı değişikliklerini kaydeder.|Site sunucusu|  
|SMSENROLLSRVSetup.log|Kayıt Web hizmetinin yükleme etkinliklerini kaydeder.|Site sistemi sunucusu|  
|SMSENROLLWEBSetup.log|Kayıt Web sitesinin yükleme etkinliklerini kaydeder.|Site sistemi sunucusu|  
|smsexec.log|Tüm site sunucusu bileşeni iş parçacıklarının işlenmesini kaydeder.|Site sunucusu veya site sistemi sunucusu|  
|SMSFSPSetup.log|Geri dönüş durum noktasının yüklenmesiyle oluşturulan iletileri kaydeder.|Site sistemi sunucusu|  
|SMSPORTALWEBSetup.log|Uygulama Kataloğu Web sitesinin yükleme etkinliklerini kaydeder.|Site sistemi sunucusu|  
|SMSProv.log|WMI sağlayıcısı erişimini site veritabanına kaydeder.|SMS Sağlayıcısı'nın bulunduğu bilgisayar|  
|srsrpMSI.log|MSI çıkışından raporlama noktası yükleme işleminin ayrıntılı sonuçlarını kaydeder.|Site sistemi sunucusu|  
|srsrpsetup.log|Raporlama noktası yükleme işleminin sonuçlarını kaydeder.|Site sistemi sunucusu|  
|statesys.log|Sistem durumu iletilerinin işlenmesini kaydeder.|Site sunucusu|  
|statmgr.log|Tüm durum iletilerinin veritabanına yazılmasını kaydeder.|Site sunucusu|  
|swmproc.log|Ölçüm dosyalarının ve ayarların işlenmesini kaydeder.|Site sunucusu|  

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a>Site sunucusu yüklemesi

Aşağıdaki tabloda, site yüklemeyle ilgili bilgileri içeren günlük dosyaları listelenmiştir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Önkoşul bileşen değerlendirmesi ve yükleme etkinliklerini kaydeder.|Site sunucusu|  
|ConfigMgrSetup.log|Site sunucusu kurulumundan ayrıntılı çıktıyı kaydeder.|Site Sunucusu|  
|ConfigMgrSetupWizard.log|Kurulum sihirbazındaki etkinlikle ilgili bilgileri kaydeder.|Site Sunucusu|  
|SMS_BOOTSTRAP.log|İkincil site yükleme işlemini başlatmanın ilerleme durumu ile ilgili bilgileri kaydeder. Gerçek kurulum işleminin ayrıntıları ConfigMgrSetup.log dosyasında bulunur.|Site Sunucusu|  
|smstsvc.log|Bir Windows hizmetini yükleme, kullanma ve kaldırma ile ilgili bilgileri kaydeder. Windows, ağ bağlantısını ve sunucular arasındaki izinleri sınamak için bu hizmeti kullanır. Bağlantıyı oluşturan sunucunun bilgisayar hesabını kullanır.|Site sunucusu ve site sistemi sunucusu|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a>Veri ambarı hizmet noktası

Aşağıdaki tabloda, veri ambarı hizmet noktasıyla ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|DWSSMSı. log|Veri ambarı hizmet noktası yüklemesi tarafından oluşturulan iletileri kaydeder.|Site sistemi sunucusu|  
|DWSSSetup. log|Veri ambarı hizmet noktası yüklemesi tarafından oluşturulan iletileri kaydeder.|Site sistemi sunucusu|  
|MgrDataWarehouse. log Microsoft.Config|Site veritabanı ve veri ambarı veritabanı arasındaki veri eşitleme hakkındaki bilgileri kaydeder.|Site sistemi sunucusu|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a>Geri dönüş durum noktası

Aşağıdaki tabloda, geri dönüş durum noktasıyla ilgili bilgileri içeren günlük dosyaları listelenmiştir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Eski mobil cihaz istemcilerinden ve istemci bilgisayarlardan geri dönüş durum noktasına yapılan iletişimlerle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|fspMSI.log|Geri dönüş durum noktasının yüklenmesiyle oluşturulan iletileri kaydeder.|Site sistemi sunucusu|  
|fspmgr.log|Geri dönüş durum noktası site sistemi rolünün etkinliklerini kaydeder.|Site sistemi sunucusu|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a>Yönetim noktası

Aşağıdaki tabloda, yönetim noktasıyla ilgili bilgileri içeren günlük dosyaları listelenmiştir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Uç noktadaki istemci mesajlaşma etkinliğini kaydeder.|Site sistemi sunucusu|
|CCM_STS. log|Azure Active Directory veya site tarafından verilen istemci belirteçlerinden kimlik doğrulama belirteçleri için etkinlikleri kaydeder.|Site sistemi sunucusu|
|ClientAuth.log|İmzalama ve kimlik doğrulama etkinliğini kaydeder.|Site sistemi sunucusu|
|MP_CliReg.log|Yönetim noktası tarafından işlenen istemci kayıt etkinliğini kaydeder.|Site sistemi sunucusu|  
|MP_Ddr.log|İstemcilerden XML. DDR kayıtlarının dönüştürülmesini kaydeder ve sonra bunları site sunucusuna kopyalar.|Site sistemi sunucusu|  
|MP_Framework.log|Temel yönetim noktası ve istemci Framework bileşenlerinin etkinliklerini kaydeder.|Site sistemi sunucusu|  
|MP_GetAuth.log|İstemci yetkilendirme etkinliğini kaydeder.|Site sistemi sunucusu|  
|MP_GetPolicy.log|İstemci bilgisayarlardan gelen ilke isteği etkinliğini kaydeder.|Site sistemi sunucusu|  
|MP_Hinv.log|İstemcilerden gelen XML donanım envanteri kayıtlarının dönüştürülmesi ve bu dosyaların site sunucusuna kopyalanması ile ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|MP_Location.log|İstemcilerin konum isteği ve yanıtlama etkinliklerini kaydeder.|Site sistemi sunucusu|  
|MP_OOBMgr.log|Bir istemciden OTP alma ile ilgili yönetim noktası etkinliklerini kaydeder.|Site sistemi sunucusu|  
|MP_Policy.log|İlke iletişimini kaydeder.|Site sistemi sunucusu|  
|MP_RegistrationManager. log|Sertifikaları, CRL 'leri ve belirteçleri doğrulamak gibi istemci kaydıyla ilgili etkinlikleri kaydeder.|Site sistemi sunucusu|
|MP_Relay.log|İstemciden toplanan dosyaların aktarılmasını kaydeder.|Site sistemi sunucusu|  
|MP_Retry.log|Donanım envanteri yeniden deneme süreçlerini kaydeder.|Site sistemi sunucusu|  
|MP_Sinv.log|İstemcilerden gelen XML yazılım envanteri kayıtlarının dönüştürülmesi ve bu dosyaların site sunucusuna kopyalanması ile ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|MP_SinvCollFile.log|Dosya toplama ile ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|MP_Status.log|İstemcilerden gelen XML.svf durum iletisi dosyalarının dönüştürülmesi ve bu dosyaların site sunucusuna kopyalanması ile ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|
|mpcontrol.log|Yönetim noktasının WINS ile kaydedilmesini kaydeder. Yönetim noktasının kullanılabilirliğini 10 dakikada bir kaydeder.|Site sunucusu|  
|mpfdm.log|İstemci dosyalarını site sunucusundaki ilgili INBOXES klasörüne taşıyan yönetim noktası bileşeni eylemlerini kaydeder.|Site sistemi sunucusu|  
|mpMSI.log|Yönetim noktası yüklemesiyle ilgili ayrıntıları kaydeder.|Site sunucusu|  
|MPSetup.log|Yönetim noktası yükleme sarmalayıcı işlemini kaydeder.|Site sunucusu|  
|UserService. log|Sunucudan Kullanıcı tarafından kullanılabilen uygulamaları alma/yükleme, yazılım merkezinden gelen kullanıcı isteklerini kaydeder.|Site sistemi sunucusu|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a>Hizmet bağlantı noktası

Aşağıdaki tabloda hizmet bağlantı noktasıyla ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Sertifika ve proxy hesabı bilgilerini kaydeder.|Site sunucusu|  
|CollEval.log|Koleksiyonların Koleksiyon Değerlendiricisi tarafından oluşturulduğu, değiştirildiği ve silindiği zamana dair ayrıntıları kaydeder.|Birincil site ve merkezi yönetim sitesi|  
|Cloudusersync.log|Kullanıcılar için lisans etkinleştirmelerini kaydeder.|Hizmet bağlantı noktası ile bilgisayar|  
|Dataldr.log|MIF dosyalarının işlenmesiyle ilgili bilgileri kaydeder.|Site sunucusu|  
|ddm.log|Discovery Data Manager'ın etkinliklerini kaydeder.|Site sunucusu|  
|Distmgr.log|İçerik dağıtımı istekleriyle ilgili ayrıntıları kaydeder.|Üst düzey site sunucusu|  
|Dmpdownloader.günlüğü|Microsoft Intune karşıdan yüklemeler hakkındaki ayrıntıları kaydeder.|Hizmet bağlantı noktası ile bilgisayar|  
|Dmpuploader.log|Microsoft Intune veritabanı değişikliklerini karşıya yüklemeyle ilgili ayrıntıları kaydeder.|Hizmet bağlantı noktası ile bilgisayar|  
|hman.log|İleti iletmeyle ilgili bilgileri kaydeder|Site sunucusu|  
|MSfBSyncWorker. log|Iş için Microsoft Store ile iletişim hakkındaki bilgileri kaydeder.|Hizmet bağlantı noktası ile bilgisayar|
|objreplmgr.log|İlke ve atama işlemeyi kaydeder.|Birincil site sunucusu|  
|PolicyPV.log|Tüm ilkelerin ilke oluşturmasını kaydeder.|Site sunucusu|  
|outgoingcontentmanager.log|Microsoft Intune karşıya yüklenen içeriği kaydeder.|Hizmet bağlantı noktası ile bilgisayar|  
|Sitecomp.log|Hizmeti bağlantı noktası yüklemesinin ayrıntılarını kaydeder.|Site sunucusu|  
|SmsAdminUI.log|Konsol etkinliğine Configuration Manager kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  
|SMS_CLOUDCONNECTION. log|Bulut hizmetleriyle ilgili bilgileri kaydeder.|Hizmet bağlantı noktası ile bilgisayar|
|Smsprov.log|SMS sağlayıcısının etkinliklerini kaydeder. Configuration Manager konsol etkinlikleri SMS sağlayıcısını kullanır.|SMS Sağlayıcısı'nın bulunduğu bilgisayar|  
|SrvBoot.log|Hizmeti bağlantı noktası yükleyici hizmetinin ayrıntılarını kaydeder.|Hizmet bağlantı noktası ile bilgisayar|  
|Statesys.log|Mobil cihaz yönetim iletilerinin işlenmesini kaydeder.|Birincil site ve merkezi yönetim sitesi|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a>Yazılım güncelleştirme noktası

Aşağıdaki tabloda, yazılım güncelleştirme noktasıyla ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Yazılım güncelleştirme bildirim dosyalarının üst siteden alt sitelere çoğaltılmasıyla ilgili ayrıntıları kaydeder.|Site sunucusu|  
|PatchDownloader.log|Yazılım güncelleştirmelerinin güncelleştirme kaynağından site sunucusundaki indirme hedefine indirilmesi işlemiyle ilgili ayrıntıları kaydeder.|Güncelleştirmeleri el ile indirdiğinizde, bu dosya, `%temp%` konsolunu kullandığınız bilgisayardaki dizininizde bulunur. Otomatik dağıtım kuralları için, Configuration Manager istemcisi site sunucusunda yüklüyse, bu dosya içindeki site sunucusudur `%windir%\CCM\Logs` .|  
|ruleengine.log|Tanımlama, içerik indirme ve yazılım güncelleştirme grubu ve dağıtım oluşturmaya yönelik otomatik dağıtım kurallarıyla ilgili ayrıntıları kaydeder.|Site sunucusu|
|SMS_ISVUPDATES_SYNCAGENT. log| Üçüncü taraf yazılım güncelleştirmelerinin eşitlenmesi için günlük dosyası.| Configuration Manager hiyerarşisindeki üst düzey yazılım güncelleştirme noktası.|
|SUPSetup.log|Yazılım güncelleştirme noktası yüklemesiyle ilgili ayrıntıları kaydeder. Yazılım güncelleştirme noktası yüklemesi tamamlandığında, bu günlük dosyasına **Yükleme başarılıydı** yazılır.|Site sistemi sunucusu|  
|WCM.log|Abone olunan güncelleştirme kategorileri, sınıflandırmalar ve diller için yazılım güncelleştirme noktası yapılandırması ve WSUS sunucusuna bağlantılarla ilgili ayrıntıları kaydeder.|WSUS sunucusuna bağlanan site sunucusu|  
|WSUSCtrl.log|Site WSUS sunucusunun durumu, yapılandırma ve veritabanı bağlantısıyla ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|wsyncmgr.log|Yazılım güncelleştirmeleri eşitleme işlemiyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|WUSSyncXML.log|Microsoft Updates eşitleme işlemi için Envanter Aracı hakkındaki ayrıntıları kaydeder.|Microsoft Updates için Envanter Aracı için eşitleme konağı olarak yapılandırılan istemci bilgisayar|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a>İşlevlere göre günlük dosyaları

Aşağıdaki bölümlerde Configuration Manager işlevlerle ilgili günlük dosyaları listelenmektedir.  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a>Uygulama yönetimi

Aşağıdaki tabloda, uygulama yönetimiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Uygulamaların mevcut ve amaçlanan durumları, uygulanabilirlikleri, gereksinimlerin karşılanıp karşılanmadığı, dağıtım türleri ve bağımlılıklar hakkındaki ayrıntıları kaydeder.|İstemci|  
|AppDiscovery.log|İstemci bilgisayarlardaki uygulamaların bulunması veya algılanması hakkındaki ayrıntıları kaydeder.|İstemci|  
|AppEnforce.log|İstemcideki uygulamalar için gerçekleştirilen zorlama eylemleri (yükleme ve kaldırma) hakkındaki ayrıntıları kaydeder.|İstemci|  
|AppGroupHandler. log|Sürüm 1906 ' den başlayarak uygulama grupları için algılama ve zorlama bilgileri|İstemci|
|awebsctl.log|Uygulama Kataloğu Web hizmeti noktası site sistemi rolü için izleme etkinliklerini kaydeder.|Site sistemi sunucusu|  
|awebsvcMSI.log|Uygulama Kataloğu web hizmeti noktası site sistemi rolü için ayrıntılı yükleme bilgilerini kaydeder.|Site sistemi sunucusu|  
|BusinessAppProcessWorker. log|Iş uygulamaları için Microsoft Store işleme kaydeder.|Site sunucusu|
|Ccmsdkprovider.log|Uygulama yönetimi SDK'sının etkinliklerini kaydeder.|İstemci|  
|colleval.log|Koleksiyonların Koleksiyon Değerlendiricisi tarafından oluşturulduğu, değiştirildiği ve silindiği zamana dair ayrıntıları kaydeder.|Site sistemi sunucusu|  
|ConfigMgrSoftwareCatalog.log|Uygulama Kataloğu etkinliğini kaydeder; buna onun Silverlight kullanımı dahildir.|İstemci|  
|MSfBSyncWorker. log|Iş için Microsoft Store ile iletişim hakkındaki bilgileri kaydeder.|Hizmet bağlantı noktası ile bilgisayar|
|NotiCtrl. log|Uygulama isteği bildirimleri.|Site sunucusu|  
|portlctl.log|Uygulama Kataloğu web sitesi noktası site sistemi rolü için izleme etkinliklerini kaydeder.|Site sistemi sunucusu|  
|portlwebMSI.log|Uygulama Kataloğu web sitesi rolü için MSI yükleme etkinliğini kaydeder.|Site sistemi sunucusu|  
|PrestageContent.log|ExtractContent.exe aracının, uzaktan hazırlanmış bir dağıtım noktasında kullanımıyla ilgili ayrıntıları kaydeder. Bu araç, bir dosyaya aktarılan içeriği ayıklar.|Site sistemi sunucusu|  
|ServicePortalWebService.log|Uygulama Kataloğu web hizmetinin etkinliğini kaydeder.|Site sistemi sunucusu|  
|ServicePortalWebSite.log|Uygulama Kataloğu web sitesinin etkinliğini kaydeder.|Site sistemi sunucusu|  
|SettingsAgent. log|Belirli uygulamaları zorlama, uygulama grubu değerlendirmesi düzenlemesini ve ortak yönetim ilkelerinin ayrıntılarını kaydeder.|İstemci|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Iş için Microsoft Store uygulamaları eşitleyen bileşen için günlük dosyası.|Site sunucusu|
|SMS_CLOUDCONNECTION. log|Bulut hizmetleriyle ilgili bilgileri kaydeder.|Hizmet bağlantı noktası ile bilgisayar|
|SMSdpmon.log|Dağıtım noktasında yapılandırılmış dağıtım noktası durumunu izleme zamanlanmış göreviyle ilgili ayrıntıları kaydeder.|Site sunucusu|  
|SoftwareCatalogUpdateEndpoint.log|Yazılım Merkezi 'nde gösterilen Uygulama Kataloğu için URL 'YI yönetmeye yönelik etkinlikleri kaydeder.|İstemci|  
|SoftwareCenterSystemTasks.log|Software Center Önkoşul bileşen doğrulaması ile ilgili etkinlikleri kaydeder.|İstemci|  
|TSDTHandler. log|Görev sırası dağıtım türü için. İşlem, görev dizisinin başlatılması için uygulama zorlamadaki (yükleme veya kaldırma) işlemi günlüğe kaydeder. Bunu AppEnforce. log ve Smsts. log ile birlikte kullanın.|İstemci|<!-- MEMDocs#336 -->

#### <a name="packages-and-programs"></a>Paketler ve programlar

Aşağıdaki tabloda, paketlerin ve programların dağıtımıyla ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|colleval.log|Koleksiyonların Koleksiyon Değerlendiricisi tarafından oluşturulduğu, değiştirildiği ve silindiği zamana dair ayrıntıları kaydeder.|Site sunucusu|  
|execmgr.log|Çalışan paketler ve görev dizileri hakkındaki ayrıntıları kaydeder.|İstemci|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a>Varlık Yönetim Bilgileri

Aşağıdaki tabloda, Varlık Yönetim Bilgileri ile ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük Adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Varlık Yönetim Bilgileri envanter eylemleri etkinliklerini kaydeder.|İstemci|  
|aikbmgr.log|Varlık Yönetim Bilgileri kataloğunu güncelleştirmek için gelen kutusundaki XML dosyalarının işlenmesiyle ilgili ayrıntıları kaydeder.|Site sunucusu|  
|AIUpdateSvc.log|Varlık Yönetim Bilgileri eşitleme noktasının etkileşimini bulut hizmetiyle kaydeder.|Site sistemi sunucusu|  
|AIUSMSI.log|Varlık Yönetim Bilgileri eşitleme noktası site sistemi rolünün yüklenmesiyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|AIUSSetup.log|Varlık Yönetim Bilgileri eşitleme noktası site sistemi rolünün yüklenmesiyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|ManagedProvider.log|İlişkili bir yazılım kimliği etiketiyle yazılım bulma hakkındaki ayrıntıları kaydeder. Ayrıca, donanım envanteriyle ilgili etkinlikleri kaydeder.|Site sistemi sunucusu|  
|MVLSImport.log|İçeri aktarılan lisans dosyalarının işlenmesiyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a>Yedekleme ve kurtarma

Aşağıdaki tabloda, site sıfırlamaları ve SMS sağlayıcısı 'nda yapılan değişiklikler dahil olmak üzere yedekleme ve kurtarma eylemleriyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Configuration Manager bir siteyi yedeklemeden kurtardığında kurulum ve kurtarma görevleriyle ilgili bilgileri kaydeder.|Site sunucusu|  
|Smsbkup.log|Site yedekleme etkinliğiyle ilgili ayrıntıları kaydeder.|Site sunucusu|  
|smssqlbkup.log|Site sunucusu olmayan bir sunucuya SQL Server yüklendiğinde site veritabanı yedekleme işleminden gelen çıktıyı kaydeder.|Site veritabanı sunucusu|  
|Smswriter.log|Yedekleme işlemi tarafından kullanılan Configuration Manager VSS yazıcısının durumuyla ilgili bilgileri kaydeder.|Site sunucusu|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a>Sertifika kaydı

Aşağıdaki tabloda, sertifika kaydıyla ilgili bilgileri içeren Configuration Manager günlük dosyaları listelenmektedir. Sertifika kaydı, ağ cihazı kayıt hizmeti 'ni (NDES) çalıştıran sunucuda sertifika kayıt noktasını ve Configuration Manager Ilkesi modülünü kullanır.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|Crp.log|Kayıt etkinliklerini kaydeder.|Sertifika kayıt noktası|  
|Crpctrl.log|Sertifika kayıt noktasının işletimsel durumunu kaydeder.|Sertifika kayıt noktası|  
|Crpsetup.log|Sertifika kayıt noktasının yüklenmesi ve yapılandırılmasıyla ilgili ayrıntıları kaydeder.|Sertifika kayıt noktası|  
|Crpmsi.log|Sertifika kayıt noktasının yüklenmesi ve yapılandırılmasıyla ilgili ayrıntıları kaydeder.|Sertifika kayıt noktası|  
|NDESPlugin.log|Sınama doğrulaması ve sertifika kaydı etkinliklerini kaydeder.|Configuration Manager Ilke modülü ve ağ cihazı kayıt hizmeti|  

Configuration Manager günlük dosyalarıyla birlikte, ağ cihazı kayıt hizmeti 'ni çalıştıran sunucuda ve sertifika kayıt noktasını barındıran sunucuda Olay Görüntüleyicisi Windows uygulama günlüklerini gözden geçirin. Örneğin, **AğCihazıKayıtHizmeti** kaynağından gelen iletilere bakın.

Ayrıca, aşağıdaki günlük dosyalarını da kullanabilirsiniz:  

- Ağ cihazı kayıt hizmeti için IIS günlük dosyaları: **%systemdrive%\ınetpub\logs\logfiles\w3svc1**  

- Sertifika kayıt noktası için IIS günlük dosyaları: **%systemdrive%\ınetpub\logs\logfiles\w3svc1**  

- Ağ Cihazı Kayıt İlkesi günlük dosyası: **mscep.log**  

    > [!NOTE]  
    > Bu dosya NDES hesap profilinin klasöründe (örneğin, C:\users\scepsvc) bulunur. NDES günlüğü 'nün nasıl etkinleştirileceği hakkında daha fazla bilgi için NDES wiki 'nin [günlüğü etkinleştirme](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) bölümüne bakın.  

### <a name="client-notification"></a><a name="BKMK_BGB"></a>İstemci bildirimi

Aşağıdaki tabloda, istemci bildirimiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|İstemci bildirim görevleriyle ilgili site sunucusu etkinlikleri ve çevrimiçi ve görev durumu dosyalarını işleme hakkındaki ayrıntıları kaydeder.|Site sunucusu|  
|BGBServer.log|Bildirim sunucusunun, istemci-sunucu iletişimi ve görevleri istemcilere iletme gibi etkinliklerini kaydeder. Ayrıca site sunucusuna gönderilecek çevrimiçi ve görev durumu dosyalarının üretilmesi hakkındaki bilgileri kaydeder.|Yönetim noktası|  
|BgbSetup.log|Yükleme ve kaldırma sırasında bildirim sunucusu yükleme sarmalayıcısı işleminin etkinliklerini kaydeder.|Yönetim noktası|  
|bgbisapiMSI.log|Bildirim sunucusu yükleme ve kaldırma ile ilgili ayrıntıları kaydeder.|Yönetim noktası|  
|BgbHttpProxy.log|HTTP kullanarak istemcilerin iletilerinin bildirim sunucusuna ve bildirim sunucusundan geçirilmesini sağlayan bildirim HTTP proxy'sinin etkinliklerini kaydeder.|İstemci|  
|CcmNotificationAgent.log|Bildirim aracısının, istemci-sunucu iletişimi ve alınan ve diğer istemci aracılarına gönderilen görevlerle ilgili bilgiler gibi etkinliklerini kaydeder.|İstemci|  

### <a name="cloud-management-gateway"></a>Bulut yönetimi ağ geçidi

Aşağıdaki tabloda, bulut yönetimi ağ geçidiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Bulut yönetimi Ağ Geçidi hizmetini dağıtma, devam eden hizmet durumu ve hizmetle ilişkili verileri kullanma hakkındaki ayrıntıları kaydeder. Günlüğe kaydetme düzeyini yapılandırmak için aşağıdaki kayıt defteri anahtarındaki **günlük düzeyi** değerini düzenleyin:`HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|Birincil site sunucusunda veya CA 'larda *InstallDir* klasörü.|
|CMGSetup. log <sup> [nonote 1](#bkmk_note1)</sup>|Bulut yönetimi ağ geçidi dağıtımının ikinci aşamasına ilişkin ayrıntıları kaydeder (Azure 'da yerel dağıtım). Günlüğe kaydetme düzeyini yapılandırmak için, **Azure portalı \ bulut Hizmetleri Yapılandırması** sekmesinde **izleme düzeyi** (**bilgi** (varsayılan), **ayrıntılı**, **hata**) ayarını kullanın.|Azure sunucunuzdaki **%AppRoot%\logs** veya site SISTEM sunucusundaki SMS/logs klasörü|
|CMGService. log <sup> [nonote 1](#bkmk_note1)</sup>|Azure 'daki bulut yönetimi ağ geçidi hizmeti çekirdek bileşeni hakkındaki ayrıntıları kaydeder. Günlüğe kaydetme düzeyini yapılandırmak için, **Azure portalı \ bulut Hizmetleri Yapılandırması** sekmesinde **izleme düzeyi** (**bilgi** (varsayılan), **ayrıntılı**, **hata**) ayarını kullanın.|Azure sunucunuzdaki **%AppRoot%\logs** veya site SISTEM sunucusundaki SMS/logs klasörü|
|SMS_Cloud_ProxyConnector. log|Bulut yönetimi ağ geçidi hizmeti ve bulut yönetimi ağ geçidi bağlantı noktası arasında bağlantıları ayarlamayla ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|
|CMGContentService. log <sup> [nonote 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->Bir CMG 'nin Azure Storage 'daki içeriklere de hizmet vermesini etkinleştirdiğinizde, bu günlük bu hizmetin ayrıntılarını kaydeder.|Azure sunucunuzdaki **%AppRoot%\logs** veya site SISTEM sunucusundaki SMS/logs klasörü|

- Dağıtım sorunlarını giderme için **CloudMgr. log** ve **cmgsetup. log** kullanın
- Hizmet durumu sorunlarını gidermek için **Cmgservice. log** ve **SMS_Cloud_ProxyConnector. log**kullanın.
- İstemci trafiği sorunlarını gidermek için **CMGHttpHandler. log**, **cmgservice. log**ve **SMS_Cloud_ProxyConnector. log**kullanın.

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a>Note 1: Azure 'dan eşitlenen Günlükler

Bunlar, bulut Service Manager 'ın her beş dakikada bir Azure depolama 'dan eşitlendiği yerel Configuration Manager günlük dosyalarıdır. Bulut yönetimi ağ geçidi, günlükleri her beş dakikada bir Azure depolama 'ya gönderir. Bu nedenle en fazla gecikme 10 dakikadır. Ayrıntılı anahtarlar hem yerel hem de uzak günlükleri etkiler. Gerçek dosya adları, hizmet adını ve rol örneği tanımlayıcısını içerir. Örneğin, CMG-*ServiceName* - *roleınstanceıd*-cmgsetup. log

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a>Uyumluluk ayarları ve şirket kaynağı erişimi

Aşağıdaki tabloda, uyumluluk ayarları ve şirket kaynağı erişimiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Uyumluluk ayarları, yazılım güncelleştirmeleri ve uygulama yönetimine ilişkin düzeltme ve uyumluluk işlemiyle ilgili ayrıntıları kaydeder.|İstemci|  
|CITaskManager.log|Yapılandırma öğesi görev zamanlamasıyla ilgili bilgileri kaydeder.|İstemci|  
|DCMAgent.log|Yapılandırma öğeleri ve uygulamalara ilişkin değerlendirme, çakışma raporlama ve düzeltme hakkındaki üst düzey bilgileri kaydeder.|İstemci|  
|DCMReporting.log|Yapılandırma öğeleri için ilke platformu sonuçlarını durum iletilerine raporlama hakkındaki bilgileri kaydeder.|İstemci|  
|DcmWmiProvider.log|WMI 'dan, yapılandırma öğesi eşitleme hakkındaki bilgileri kaydeder.|İstemci|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a>Configuration Manager konsolu

Aşağıdaki tabloda Configuration Manager konsoluyla ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Configuration Manager konsolunun yüklemesini kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  
|SmsAdminUI.log|Configuration Manager konsolunun işlemi hakkındaki bilgileri kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  
|Smsprov.log|SMS sağlayıcısının etkinliklerini kaydeder. Configuration Manager konsol etkinlikleri SMS sağlayıcısını kullanır.|Site sunucusu veya site sistemi sunucusu|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a>İçerik yönetimi

Aşağıdaki tabloda, içerik yönetimiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|CloudDP- &lt; Guid \> . log|Depolama ve içerik erişimi hakkındaki bilgiler dahil olmak üzere belirli bir bulut tabanlı dağıtım noktasıyla ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|CloudMgr.log|İçerik sağlama, depolama ve bant genişliği istatistiklerinin toplanması ve bulut tabanlı dağıtım noktası çalıştıran bulut hizmetini durdurmak veya başlatmak için yönetici tarafından başlatılan eylemler hakkındaki ayrıntıları kaydeder.|Site sistemi sunucusu|  
|DataTransferService.log|İlke veya paket erişimine ilişkin tüm BITS iletişimini kaydeder. Bu günlük, çekme dağıtım noktaları tarafından içerik yönetimi için de kullanılır.|Çekme dağıtım noktası olarak yapılandırılan bilgisayar|  
|PullDP.log|Çekme dağıtım noktasının kaynak dağıtım noktalarından aktardığı içerikle ilgili ayrıntıları kaydeder.|Çekme dağıtım noktası olarak yapılandırılan bilgisayar|  
|PrestageContent.log|ExtractContent.exe aracının kullanımı hakkındaki ayrıntıları, uzak, önceden hazırlanan bir dağıtım noktasında kaydeder. Bu araç, bir dosyaya aktarılan içeriği ayıklar.|Site sistemi rolü|  
|SMSdpmon.log|Dağıtım noktasında yapılandırılmış olan zamanlanmış görevlerle dağıtım noktası durumu izleme hakkındaki ayrıntıları kaydeder.|Site sistemi rolü|  
|smsdpprov.log|Birincil siteden alınan sıkıştırılmış dosyaların ayıklanmasıyla ilgili ayrıntıları kaydeder. Bu günlük, uzak dağıtım noktasının WMI sağlayıcısı tarafından oluşturulur.|Site sunucusuyla birlikte bulunmayan dağıtım noktası bilgisayarı|  
|smsdpusage. log|Çalıştıran smsdpusage.exe hakkındaki ayrıntıları kaydeder ve dağıtım noktası Kullanım Özeti raporu için verileri toplar.|Site sistemi rolü|  

### <a name="desktop-analytics"></a>Desktop Analytics

Configuration Manager ile tümleştirilmiş masaüstü analiziyle ilgili sorunları gidermeye yardımcı olması için aşağıdaki günlük dosyalarını kullanın.

Hizmet bağlantı noktasındaki günlük dosyaları şu dizinde: `%ProgramFiles%\Configuration Manager\Logs\M365A` .
Configuration Manager istemcisindeki günlük dosyaları şu dizinde: `%WinDir%\CCM\logs` .

| Günlük | Description |Günlük dosyası içeren bilgisayar|
|---------|---------|---------|
| M365ADeploymentPlanWorker. log | Masaüstü Analizi bulut hizmetinden şirket içi Configuration Manager dağıtım planı eşitlemesi hakkında bilgi |Hizmet bağlantı noktası|
| M365ADeviceHealthWorker. log | Configuration Manager 'den Microsoft buluta cihaz durumu yüklemesi hakkında bilgi |Hizmet bağlantı noktası|
| M365AHandler. log | Masaüstü Analizi ayarları ilkesiyle ilgili bilgiler |İstemci|
| M365AUploadWorker. log | Configuration Manager 'den Microsoft bulutuna koleksiyon ve cihaz yükleme hakkında bilgi |Hizmet bağlantı noktası|
| SmsAdminUI.log | Azure Cloud Services 'ı yapılandırma gibi Configuration Manager konsol etkinliği hakkında bilgi  |Hizmet bağlantı noktası|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a>Keşfini

Aşağıdaki tabloda, bulma ile ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Active Directory Güvenlik Grubu Saptama eylemlerini kaydeder.|Site sunucusu|  
|adsysdis.log|Active Directory Sistem Saptama eylemlerini kaydeder.|Site sunucusu|  
|adusrdis.log|Active Directory Kullanıcı Saptama eylemlerini kaydeder.|Site sunucusu|  
|ADForestDisc.Log|Active Directory Orman Saptama eylemlerini kaydeder.|Site sunucusu|  
|ddm.log|Discovery Data Manager'ın etkinliklerini kaydeder.|Site sunucusu|  
|InventoryAgent.log|Donanım envanteri, yazılım envanteri etkinliklerini ve istemci üzerindeki sinyal bulma işlemlerini kaydeder.|İstemci|  
|netdisc.log|Ağ Bulma eylemlerini kaydeder.|Site sunucusu|  

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a>Endpoint Protection

Aşağıdaki tabloda, Uç Nokta Koruma ile ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Uç Nokta Koruma istemcisinin yüklenmesi ve kötü amaçlı yazılımdan koruma ilkesinin o istemciye uygulanmasıyla ilgili ayrıntıları kaydeder.|İstemci|  
|EPCtrlMgr.log|Kötü amaçlı yazılım tehdit bilgilerinin Endpoint Protection rol sunucusundan Configuration Manager veritabanıyla eşitlenmesi hakkındaki ayrıntıları kaydeder.|Site sistemi sunucusu|  
|EPMgr.log|Uç Nokta Koruma site sistemi rolünün durumunu izler.|Site sistemi sunucusu|  
|EPSetup.log|Uç Nokta Koruma site sistemi rolünün yüklenmesiyle ilgili bilgileri sağlar.|Site sistemi sunucusu|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a>Uzantılardan

Aşağıdaki tabloda, uzantılarla ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Microsoft'tan uzantıların indirilmesi ile tüm uzantıların yüklenmesi ve kaldırılması hakkındaki bilgileri kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  
|FeatureExtensionInstaller.log|Configuration Manager konsolunda etkinleştirildiklerinde veya devre dışı bırakıldığında tek tek uzantıların yüklenmesi ve kaldırılması hakkındaki bilgileri kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  
|SmsAdminUI.log|Konsol etkinliğine Configuration Manager kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a>Envanteri

Aşağıdaki tabloda, envanter verilerinin işlenmesiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Configuration Manager veritabanındaki MIF dosyalarının ve donanım envanterinin işlenmesiyle ilgili bilgileri kaydeder.|Site sunucusu|  
|invproc.log|MIF dosyalarının ikincil siteden üst siteye iletilmesini kaydeder.|İkincil site sunucusu|  
|sinvproc.log|Yazılım envanteri verilerinin site veritabanına işlenmesiyle ilgili bilgileri kaydeder.|Site sunucusu|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a>Yazılım

Aşağıdaki tabloda, ölçümle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Tüm yazılım kullanım ölçümü işlemlerini izler.|İstemci|  
|SWMTRReportGen.log|Ölçüm Aracısı tarafından toplanan kullanım verileri raporunu oluşturur. Bu veriler Mtrmgr.log günlüğüne kaydedilir.|İstemci|
|swmproc.log|Ölçüm dosyalarının ve ayarların işlenmesini kaydeder.|Site sunucusu|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a>Geçiş

Aşağıdaki tabloda, geçişle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Geçiş işlerini, paylaşılan dağıtım noktalarını ve dağıtım noktası yükseltmelerini içeren geçiş eylemleriyle ilgili bilgileri kaydeder.|Configuration Manager hiyerarşisindeki üst düzey site ve her alt birincil site. Çok birincil siteli bir hiyerarşide, merkezi yönetim sitesinde oluşturulan günlük dosyasını kullanın.|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a>Mobil cihazlar

Aşağıdaki bölümlerde, mobil cihazların yönetimiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a>Kaydolmak

Aşağıdaki tabloda, mobil cihaz kaydıyla ilgili bilgiler içeren günlükler listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Mobil cihazlar için etkinleştirilmiş yönetim noktalarıyla yönetim noktası uç noktaları arasındaki iletişimi kaydeder.|Site sistemi sunucusu|  
|dmpmsi.log|Mobil cihazlar için etkinleştirilen yönetim noktasının yapılandırılmasıyla ilgili Windows Installer verilerini kaydeder.|Site sistemi sunucusu|  
|DMPSetup.log|Mobil cihazlar için etkinleştirildiğinde yönetim noktasının yapılandırmasını kaydeder.|Site sistemi sunucusu|  
|enrollsrvMSI.log|Kaydolma noktasının yapılandırılmasıyla ilgili Windows Installer verilerini kaydeder.|Site sistemi sunucusu|  
|enrollmentweb.log|Mobil cihazlarla kaydolma proxy noktası arasındaki iletişimi kaydeder.|Site sistemi sunucusu|  
|enrollwebMSI.log|Kaydolma proxy noktasının yapılandırılmasıyla ilgili Windows Installer verilerini kaydeder.|Site sistemi sunucusu|  
|enrollmentservice.log|Kaydolma proxy noktasıyla kaydolma noktasının arasındaki iletişimi kaydeder.|Site sistemi sunucusu|  
|SMS_DM.log|Mobil cihazlar, Mac bilgisayarlar ve mobil cihazlar ve Mac bilgisayarlar için etkinleştirilen yönetim noktası arasındaki iletişimi kaydeder.|Site sistemi sunucusu|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a>Exchange Server Bağlayıcısı

Aşağıdaki Günlükler Exchange Server Bağlayıcısı ile ilgili bilgiler içerir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Exchange Server bağlayıcısının etkinliklerini ve durumunu kaydeder.|Site sunucusu|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a>Mobil cihaz eski

Aşağıdaki tabloda, mobil cihaz eski istemcisiyle ilgili bilgiler içeren günlükler listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Mobil cihaz eski istemcilerindeki sertifika kaydı verileriyle ilgili ayrıntıları kaydeder.|İstemci|  
|DMCertResp.htm|Mobil cihaz eski istemci kaydedici programı bir PKI sertifikası istediğinde sertifika sunucusundan gelen HTML yanıtını kaydeder.|İstemci|  
|DmClientHealth.log|Mobil cihazlar için etkinleştirilen yönetim noktasıyla iletişim kuran tüm mobil cihaz eski istemcilerinin GUID 'Lerini kaydeder.|Site sistemi sunucusu|  
|DmClientRegistration.log|Kayıt isteklerini ve mobil cihaz eski istemcilerine verilen ve bu istemcilerin verdiği yanıtları kaydeder.|Site sistemi sunucusu|  
|DmClientSetup.log|Mobil cihaz eski istemcilerine ilişkin istemci kurulum verilerini kaydeder.|İstemci|  
|DmClientXfer.log|Mobil cihaz eski istemcileri ve ActiveSync dağıtımlarına ilişkin istemci aktarım verilerini kaydeder.|İstemci|  
|DmCommonInstaller.log|Mobil cihaz eski istemci aktarım dosyalarını yapılandırmaya ilişkin istemci aktarım dosyası yüklemesini kaydeder.|İstemci|  
|DmInstaller.log|Mobil cihaz eski istemcileri için DMInstaller'ın DmClientSetup'ı doğru bir şekilde çağırıp çağırmadığını ve DmClientSetup'ın başarıyla mı yoksa başarısızlıkla mı çıkış yaptığını kaydeder.|İstemci|  
|DmpDatastore.log|Mobil cihazlar için etkinleştirilmiş olan yönetim noktası tarafından yapılan tüm site veritabanı bağlantılarını ve sorguları kaydeder.|Site sistemi sunucusu|  
|DmpDiscovery.log|Mobil cihazlar için etkinleştirilmiş olan yönetim noktasındaki mobil cihaz eski istemcilerinden gelen bulma verilerinin tümünü kaydeder.|Site sistemi sunucusu|  
|DmpHardware.log|Mobil cihazlar için etkinleştirilmiş olan yönetim noktasındaki mobil cihaz eski istemcilerinden gelen donanım envanteri verileri kaydeder.|Site sistemi sunucusu|  
|DmpIsapi.log|Mobil cihaz eski istemcisiyle mobil cihazlar için etkinleştirilmiş bir yönetim noktası arasındaki iletişimi kaydeder.|Site sistemi sunucusu|  
|dmpmsi.log|Mobil cihazlar için etkinleştirilen yönetim noktasının yapılandırılmasıyla ilgili Windows Installer verilerini kaydeder.|Site sistemi sunucusu|  
|DMPSetup.log|Mobil cihazlar için etkinleştirildiğinde yönetim noktasının yapılandırmasını kaydeder.|Site sistemi sunucusu|  
|DmpSoftware.log|Mobil cihazlar için etkinleştirilmiş olan yönetim noktasındaki mobil cihaz eski istemcilerinden gelen yazılım dağıtımı verilerini kaydeder.|Site sistemi sunucusu|  
|DmpStatus.log|Mobil cihazlar için etkinleştirilmiş olan yönetim noktasındaki mobil cihaz istemcilerinden gelen durum iletileri verilerini kaydeder.|Site sistemi sunucusu|  
|DmSvc.log|Mobil cihaz eski istemcileriyle mobil cihazlar için etkinleştirilmiş bir yönetim noktası arasındaki iletişimi kaydeder.|İstemci|  
|FspIsapi.log|Eski mobil cihaz istemcilerinden ve istemci bilgisayarlardan geri dönüş durum noktasına yapılan iletişimlerle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a>İşletim sistemi dağıtımı

Aşağıdaki tabloda, işletim sistemi dağıtımıyla ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|CAS.log|Başvurulan içerik için dağıtım noktaları bulunduğunda ayrıntıları kaydeder.|İstemci|  
|ccmsetup.log|İstemci kurulumu, istemci yükseltmesi ve istemci kaldırma için ccmsetup görevlerini kaydeder. İstemci yükleme sorunlarını gidermek için kullanılabilir.|İstemci|  
|CreateTSMedia.log|Görev dizisi medya oluşturma işlemiyle ilgili ayrıntıları kaydeder.|Configuration Manager konsolunu çalıştıran bilgisayar|  
|Dism.log|Çevrimdışı bakım için sürücü yükleme eylemlerini kaydeder veya uygulama eylemlerini güncelleştirir.|Site sistemi sunucusu|  
|Distmgr.log|Ön önyükleme yürütme ortamı (PXE) için bir dağıtım noktasını etkinleştirme yapılandırmasıyla ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|DriverCatalog.log|Sürücü kataloğuna aktarılan cihaz sürücüleriyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|mcsisapi.log|Çok noktaya yayın paketi aktarımı ve istemci isteği yanıtlarıyla ilgili bilgileri kaydeder.|Site sistemi sunucusu|  
|mcsexec.log|Sistem durumu denetimi, ad alanı, oturum oluşturma ve sertifika denetimi eylemlerini kaydeder.|Site sistemi sunucusu|  
|mcsmgr.log|Yapılandırma, güvenlik modu ve kullanılabilirlik değişiklikleri kaydeder.|Site sistemi sunucusu|  
|mcsprv.log|Çok noktaya yayın sağlayıcısının Windows Dağıtım Hizmetleri (WDS) ile etkileşimini kaydeder.|Site sistemi sunucusu|  
|MCSSetup.log|Çok noktaya yayın sunucusu rolü yüklemesiyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|MCSMSI.log|Çok noktaya yayın sunucusu rolü yüklemesiyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|Mcsperf.log|Çok noktaya yayın performans sayacı güncelleştirmeleriyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|MP_ClientIDManager.log|Görev dizilerinin PXE 'den veya önyükleme medyasından başlamasını isteyen istemci KIMLIĞINE yönelik yönetim noktası yanıtlarını kaydeder.|Site sistemi sunucusu|  
|MP_DriverManager.log|Sürücüleri Otomatik Olarak Uygula görev dizisi eylem isteklerine verilen yönetim noktası yanıtlarını kaydeder.|Site sistemi sunucusu|  
|OfflineServicingMgr.log|Çevrimdışı bakım zamanlamalarının ayrıntılarını kaydeder ve işletim sistemi Windows Imaging Format (WıM) dosyalarında uygulama eylemlerini güncelleştirir.|Site sistemi sunucusu|  
|Setupact.log|Windows Sysprep ve kurulum günlükleriyle ilgili ayrıntıları kaydeder. Daha fazla bilgi için bkz. [günlük dosyaları](https://docs.microsoft.com/windows/deployment/upgrade/log-files).|İstemci|  
|Setupapi.log|Windows Sysprep ve kurulum günlükleriyle ilgili ayrıntıları kaydeder.|İstemci|  
|Setuperr.log|Windows Sysprep ve kurulum günlükleriyle ilgili ayrıntıları kaydeder.|İstemci|  
|smpisapi.log|İstemci durumu yakalama ve geri yükleme eylemleriyle ilgili ayrıntıları ve eşik bilgilerini kaydeder.|İstemci|  
|Smpmgr.log|Durum geçiş noktası sistem durumu denetimlerinin ve yapılandırma değişikliklerinin sonuçlarıyla ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|smpmsi.log|Durum geçiş noktasıyla ilgili yükleme ve yapılandırma ayrıntılarını kaydeder.|Site sistemi sunucusu|  
|smpperf.log|Durum geçiş noktası performans sayacı güncelleştirmelerini kaydeder.|Site sistemi sunucusu|  
|smspxe.log|PXE önyüklemesi kullanan istemcilere verilen yanıtlara ve önyükleme görüntülerinin ve önyükleme dosyalarının genişletilmesiyle ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|smssmpsetup.log|Durum geçiş noktasıyla ilgili yükleme ve yapılandırma ayrıntılarını kaydeder.|Site sistemi sunucusu|
| SMS_PhasedDeployment. log| Aşamalı dağıtımlar için günlük dosyası|Configuration Manager hiyerarşisindeki üst düzey site|
|Smsts.log|Görev dizisi etkinliklerini kaydeder.|İstemci|  
|TSAgent.log|Bir görev dizisini başlatmadan önce görev dizisi bağımlılıklarının sonucunu kaydeder.|İstemci|  
|TaskSequenceProvider.log|İçeri aktarıldığında, aktarıldığında veya düzenlendiklerinde görev dizileri hakkındaki ayrıntıları kaydeder.|Site sistemi sunucusu|  
|loadstate.log|Kullanıcı Durumu Geçirme Aracı (USMT) ve kullanıcı durumu verilerini geri yüklemeyle ilgili ayrıntıları kaydeder.|İstemci|  
|scanstate.log|Kullanıcı Durumu Geçirme Aracı (USMT) ve kullanıcı durumu verilerini yakalamayla ilgili ayrıntıları kaydeder.|İstemci|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a>Güç yönetimi

Aşağıdaki tabloda, güç yönetimiyle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|İstemci bilgisayardaki güç yönetimi etkinlikleriyle ilgili ayrıntıları, izleme ve ayarları güç yönetimi Istemci Aracısı tarafından zorlama dahil kaydeder.|İstemci|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a>Uzaktan denetim

Aşağıdaki tabloda, uzaktan denetimle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Uzaktan denetim görüntüleyicinin etkinliğiyle ilgili ayrıntıları kaydeder.|Uzaktan denetim görüntüleyicisini çalıştıran bilgisayarda,% Temp% klasöründe.|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a>Rapor

Aşağıdaki tabloda, raporlamayla ilgili bilgiler içeren Configuration Manager günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Raporlama hizmetleri noktasının etkinliği ve durumuyla ilgili bilgileri kaydeder.|Site sistemi sunucusu|  
|srsrpMSI.log|MSI çıktısından raporlama hizmetleri noktası yükleme işleminin ayrıntılı sonuçlarını kaydeder.|Site sistemi sunucusu|  
|srsrpsetup.log|Raporlama hizmetleri noktası yükleme işleminin sonuçlarını kaydeder.|Site sistemi sunucusu|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a>Rol tabanlı yönetim

Aşağıdaki tabloda, rol tabanlı yönetimi yönetmekle ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|hman.log|Site yapılandırma değişiklikleriyle ilgili bilgileri ve site bilgilerinin Active Directory Domain Services yayımlamasını kaydeder.|Site sunucusu|  
|SMSProv.log|WMI sağlayıcısı erişimini site veritabanına kaydeder.|SMS Sağlayıcısı'nın bulunduğu bilgisayar|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a>Yazılım kullanım ölçümü

Aşağıdaki tabloda, yazılım kullanım ölçümü ile ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Tüm yazılım kullanım ölçümü işlemlerini izler.|Site sunucusu|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a>Yazılım güncelleştirmeleri

Aşağıdaki tabloda yazılım güncelleştirmeleriyle ilgili bilgileri içeren günlük dosyaları listelenmiştir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|AlternateHandler. log|İstemci Office Tıkla-Çalıştır COM arabirimini çağırdığında, Kurumsal istemci güncelleştirmelerine yönelik Microsoft 365 uygulamalarını indirip yüklerken ayrıntıları kaydeder. Windows güncelleştirmelerini indirmek ve yüklemek üzere Windows Update Agent API 'sini çağırdığında WuaHandler kullanımı benzerdir.<!-- SCCMDocs#888 -->|İstemci|
|ccmperf.log|İstemci performans sayaçlarıyla ilgili verilerin bakımı ve yakalanmasıyla ilgili etkinlikleri kaydeder.|İstemci|
|DeltaDownload. log|Dağıtım Iyileştirmesi kullanılarak indirilen hızlı güncelleştirme ve güncelleştirmelerin indirilmesi hakkındaki bilgileri kaydeder.|İstemci|  
|PatchDownloader.log|Yazılım güncelleştirmelerinin güncelleştirme kaynağından site sunucusundaki indirme hedefine indirilmesi işlemiyle ilgili ayrıntıları kaydeder.|Güncelleştirmeler el ile indirilirken, bu günlük dosyası konsolunu çalıştırdığınız makinede konsolunu çalıştıran kullanıcının% Temp% dizininde bulunur. Otomatik dağıtım kuralları için, ConfigMgr istemcisi site sunucusunda yüklüyse, bu günlük dosyası%windir%\CCM\Logs içindeki site sunucusunda bulunur.|  
|PolicyEvaluator.log|Yazılım güncelleştirmelerindeki ilkeler dahil olmak üzere istemci bilgisayarlardaki ilkelerin değerlendirilmesiyle ilgili ayrıntıları kaydeder.|İstemci|  
|RebootCoordinator.log|Yazılım güncelleştirme yüklemelerinden sonra istemci bilgisayarlarda sistem yeniden başlatmalarının eşgüdümüyle ilgili ayrıntıları kaydeder.|İstemci|  
|ScanAgent.log|Yazılım güncelleştirmeleri için tarama istekleri, WSUS konumu ve ilgili eylemler hakkındaki ayrıntıları kaydeder.|İstemci|  
|SdmAgent.log|Düzeltme ve uyumluluk izlemeyle ilgili ayrıntıları kaydeder. Ancak, yazılım güncelleştirmeleri günlük dosyası, Updateshandler. log, uyumluluk için gereken yazılım güncelleştirmelerini yüklemeyle ilgili daha bilgilendirici ayrıntılar sağlar. Bu günlük dosyası uyumluluk ayarlarıyla paylaşılır.|İstemci|  
|ServiceWindowManager.log|Bakım pencerelerinin değerlendirilmesiyle ilgili ayrıntıları kaydeder.|İstemci|
|SMS_ISVUPDATES_SYNCAGENT. log| Üçüncü taraf yazılım güncelleştirmelerinin eşitlenmesi için günlük dosyası.| Configuration Manager hiyerarşisindeki üst düzey yazılım güncelleştirme noktası.|
|SMS_OrchestrationGroup. log| Düzenleme grupları için günlük dosyası|Site sunucusu|
|SmsWusHandler.log|Microsoft Updates için Envanter Aracı'na ilişkin tarama işlemiyle ilgili ayrıntıları kaydeder.|İstemci|  
|StateMessage.log|Oluşturulan ve yönetim noktasına gönderilen yazılım güncelleştirme durumu iletileriyle ilgili ayrıntıları kaydeder.|İstemci|  
|SUPSetup.log|Yazılım güncelleştirme noktası yüklemesiyle ilgili ayrıntıları kaydeder. Yazılım güncelleştirme noktası yüklemesi tamamlandığında, bu günlük dosyasına **Yükleme başarılıydı** yazılır.|Site sistemi sunucusu|  
|UpdatesDeployment.log|Yazılım güncelleştirme etkinleştirme, değerlendirme ve zorlama dahil olmak üzere istemcideki dağıtımlarla ilgili ayrıntıları kaydeder. Ayrıntılı günlük, istemci kullanıcı arabirimiyle etkileşim hakkındaki ek bilgileri gösterir.|İstemci|  
|UpdatesHandler.log|Yazılım güncelleştirme uyumluluk taraması ve yazılım güncelleştirmelerinin istemciye indirilmesi ve yüklenmesiyle ilgili ayrıntıları kaydeder.|İstemci|  
|UpdatesStore.log|Uyumluluk taraması döngüsü sırasında değerlendirilen yazılım güncelleştirmelerine ilişkin uyumluluk durumuyla ilgili ayrıntıları kaydeder.|İstemci|  
|WCM.log|Abone olunan güncelleştirme kategorileri, sınıflandırmalar ve diller için yazılım güncelleştirme noktası yapılandırmalarına ve WSUS sunucusuna bağlantılarla ilgili ayrıntıları kaydeder.|Site sunucusu|  
|WSUSCtrl.log|Site WSUS sunucusunun durumu, yapılandırma ve veritabanı bağlantısıyla ilgili ayrıntıları kaydeder.|Site sistemi sunucusu|  
|wsyncmgr.log|Yazılım güncelleştirme eşitleme işlemiyle ilgili ayrıntıları kaydeder.|Site sunucusu|  
|WUAHandler.log|İstemcideki Windows Update Aracısı yazılım güncelleştirmelerini aradığında onunla ilgili ayrıntıları kaydeder.|İstemci|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a>LAN'da Uyandırma

Aşağıdaki tabloda LAN'da Uyandırma kullanımı ile ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

> [!NOTE]  
> LAN'da Uyandırma, uyandırma proxy 'sini kullanarak eklediğinizde, bu etkinlik istemcide günlüğe kaydedilir. Örneğin, *domain* \> @SYSTEM_0.log Bu makalenin [istemci işlemleri](#BKMK_ClientOpLogs) bölümünde yer alan Ccmexec. log ve SleepAgent_<etki alanı ' na bakın.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Hangi istemcilere uyandırma paketi gönderilmesi gerektiği, gönderilen uyandırma paketi sayısı ve yeniden denenen uyandırma paketi sayısıyla ilgili ayrıntıları kaydeder.|Site sunucusu|  
|wolmgr.log|Uyandırma yordamlarıyla ilgili ayrıntıları (LAN'da Uyandırma için yapılandırılan dağıtımların ne zaman uyandırılacağı gibi) kaydeder.|Site sunucusu|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a>Windows 10 Bakımı

Aşağıdaki tabloda, Windows 10 Bakımı ile ilgili bilgiler içeren günlük dosyaları listelenmektedir.  
Bakım, yazılım güncelleştirmeleriyle aynı altyapıyı ve işlemi kullanır. Hizmet senaryosu için geçerli olan diğer Günlükler için bkz. [yazılım güncelleştirmeleri](#BKMK_SU_NAPLog).

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|CBS. log|Windows güncelleştirmeleri veya rolleri ve özellikleri değişiklikleriyle ilgili olarak bakım başarısızlıklarını kaydeder.|İstemci|
|DıSM. log|DıSM kullanarak tüm eylemleri kaydeder. Gerekirse, daha fazla ayrıntı için DıSM. log dosyası CBS. log dosyasına işaret eder.|İstemci|
|Setupact. log|Windows yükleme işlemi sırasında oluşan hataların çoğu için birincil günlük dosyası. Günlük dosyası% Windir% \$ Windows. ~ BT\sources\panther klasöründe bulunur.|İstemci|

Daha fazla bilgi için bkz. [çevrimiçi hizmet Ile Ilgili günlük dosyaları](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files).

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a>Windows Update Aracısı

Aşağıdaki tabloda, Windows Update Aracısı ile ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Windows Update aracısının WSUS sunucusuna ne zaman bağlanacağı ve uyumluluk değerlendirmesi için yazılım güncelleştirmelerini aldığı ve aracı bileşenlerinde güncelleştirmeler olup olmadığı hakkındaki ayrıntıları kaydeder.|İstemci|  

Daha fazla bilgi için bkz. [Windows Update günlük dosyaları](https://docs.microsoft.com/windows/deployment/update/windows-update-logs).

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a>WSUS sunucusu

Aşağıdaki tabloda, WSUS sunucusuyla ilgili bilgiler içeren günlük dosyaları listelenmektedir.  

|Günlük adı|Description|Günlük dosyası içeren bilgisayar|  
|--------------|-----------------|----------------------------|  
|Change.log|Değiştirilen WSUS sunucusu veritabanı bilgileriyle ilgili ayrıntıları kaydeder.|WSUS sunucusu|  
|SoftwareDistribution.log|Yapılandırılan güncelleştirme kaynağından WSUS sunucusu veritabanına eşitlenen yazılım güncelleştirmeleriyle ilgili ayrıntıları kaydeder.|WSUS sunucusu|  

Bu günlük dosyaları `%ProgramFiles%\Update Services\LogFiles` klasöründe bulunur.

## <a name="see-also"></a>Ayrıca bkz.

- [Günlük dosyaları hakkında](about-log-files.md)

- [Destek Merkezi OneTrace](../../support/support-center-onetrace.md)

- [Destek Merkezi günlük dosyası Görüntüleyici](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
