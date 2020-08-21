---
title: Sürüm 1902’deki yenilikler
titleSuffix: Configuration Manager
description: Geçerli dalın Configuration Manager sürüm 1902 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f758456ad75c4acde1b050be75d653cc0e1dcfa1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700376"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Geçerli dalın Configuration Manager sürüm 1902 ' deki yenilikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme 1902, konsol içi bir güncelleştirme olarak sunulmaktadır. 1802, 1806 veya 1810 sürümünü çalıştıran sitelerde bu güncelleştirmeyi uygulayın. <!-- baseline only statement:-->Yeni bir site yüklerken, taban çizgisi sürümü olarak da kullanılabilir. Bu makalede Configuration Manager, sürüm 1902 ' deki değişiklikler ve yeni özellikler özetlenmektedir.  

Bu güncelleştirmeyi yüklemek için her zaman en son denetim listesini gözden geçirin. Daha fazla bilgi için bkz. [güncelleştirme 1902 yükleme denetim listesi](../../servers/manage/checklist-for-installing-update-1902.md). Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist)de gözden geçirin.

Yeni Configuration Manager özelliklerinden tam olarak yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme de güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Kullanımdan kaldırılan özellikler ve işletim sistemleri

[Kaldırılan ve kullanımdan kaldırılan öğelerde](deprecated/removed-and-deprecated.md)uygulanmadan önce yapılan değişiklikler hakkında bilgi edinin.

- Azure 'dan içerik paylaşmaya yönelik uygulama değişti. **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin verme ve Azure depolama 'dan içerik**sunma seçeneğini etkinleştirerek, içerik özellikli bir bulut yönetimi ağ geçidi kullanın. Gelecekte geleneksel bir bulut dağıtım noktası oluşturamayacak.

Sürüm 1902 aşağıdaki ürünler için desteği bırakır:  

- İstemci olarak Linux ve UNIX. [Sürüm 1802](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support)ile kullanımdan kaldırma duyurulmuştur. Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site altyapısı

### <a name="client-health-dashboard"></a>İstemci sistem durumu panosu

<!--3599209-->
Ortamınızın güvenliğini sağlamaya yardımcı olmak için yazılım güncelleştirmelerini ve diğer uygulamaları dağıtırsınız, ancak bu dağıtımlar yalnızca sağlıklı istemcilere ulaşın. Sağlıksız Configuration Manager istemcileri genel uyumluluğu olumsuz etkiler. İstemci durumunun belirlenmesi, paydaya bağlı olarak, kaç tane toplam cihazın yönetim kapsamınızda olması gerektiği konusunda zor olabilir mi? Örneğin, Active Directory tüm sistemleri keşfetseniz, bu kayıtlardan bazıları kullanımdan kaldırılan makineler için olsa bile, bu işlem paydayı arttırır.

Artık ortamınızdaki Configuration Manager istemcilerinin sistem durumu hakkında bilgi içeren bir panoyu görüntüleyebilirsiniz. İstemci sistem durumunu, senaryo sistem durumunu ve sık karşılaşılan hataları görüntüleyin. İşletim sistemi ve istemci sürümlerine göre olası sorunları görmek için görünümü birkaç özniteliğe göre filtreleyin.

Configuration Manager konsolunda **izleme** çalışma alanına gidin. **İstemci durumu**' nu genişletin ve **istemci sistem durumu panosu** düğümünü seçin.

![İstemci sistem durumu panosunun ekran görüntüsü](media/3599209-client-health-dashboard.png)

Daha fazla bilgi için bkz. [istemcileri izleme](../../clients/manage/monitor-clients.md#bkmk_health).

### <a name="new-management-insight-rules"></a>Yeni yönetim Insight kuralları

Yönetim öngörüleri özelliği aşağıdaki yeni kurallara sahiptir:

- Koleksiyonları yönetmeye yönelik önerilere sahip birden çok kural. Yönetimi basitleştirmek ve performansı artırmak için bu öngörüleri kullanın. **Koleksiyonlar** grubundaki bu yeni kuralları gözden geçirin.<!--3555752-->  

- İstemcileri **basitleştirilmiş yönetim** grubundaki **desteklenen bir Windows 10 sürüm kuralına güncelleştirin** . Bu kural, artık desteklenmeyen bir Windows 10 sürümünü çalıştıran istemcilerde raporlar. Hizmet sonuna yakın bir Windows 10 sürümü olan istemcileri de içerir (üç ay).<!--3897268-->  

Daha fazla bilgi için bkz. [Management Insights](../../servers/manage/management-insights.md).

### <a name="improvement-to-enhanced-http"></a>Gelişmiş HTTP 'ye geliştirme

<!--3798957-->

Artık birincil site başına veya merkezi yönetim sitesi için gelişmiş HTTP 'yi etkinleştirebilirsiniz.

Merkezi yönetim sitesinin özelliklerinde, **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanma**seçeneğini belirleyin. Bu ayar yalnızca merkezi yönetim sitesindeki site sistem rolleri için geçerlidir. Hiyerarşi için genel bir ayar değildir.

Daha fazla bilgi için bkz. [GELIŞMIŞ http](../hierarchy/enhanced-http.md).

### <a name="improvement-to-setup-prerequisites"></a>Kurulum önkoşullarını geliştirme

1902 sürümünü yüklediğinizde veya sürümüne güncelleştirdiğinizde Configuration Manager Kurulum artık aşağıdaki önkoşul denetimini içerir:

- **Uzak SQL Server sistem yeniden başlatması bekleniyor**: Bu önkoşul denetimi, **bekleyen sistem yeniden başlatma** kuralına benzerdir, ancak uzak bir SQL Server denetler. Daha fazla bilgi için bkz. [önkoşul denetimleri listesi](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Buluta bağlı yönetim

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Eşiği aştığında bulut hizmetini durdur

<!--3735092-->
Configuration Manager, artık toplam veri aktarımı sınırınızı geçtiğinde bir bulut yönetimi ağ geçidi (CMG) hizmetini durdurabilir. CMG, kullanım uyarısı veya kritik düzeylerine ulaştığında bildirimleri tetiklemek için her zaman uyarı içeriyordu. Kullanımda olan bir ani artış nedeniyle beklenmeyen Azure maliyetlerini azaltmaya yardımcı olmak için, bu yeni seçenek bulut hizmetini devre dışı bırakır.

Daha fazla bilgi için bkz. [eşiği aştığında CMG 'Yi durdurma](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop).

### <a name="use-azure-resource-manager-for-cloud-services"></a>Cloud Services için Azure Resource Manager kullanma

<!--3605704-->
Sürüm 1810 ' den başlayarak, Azure 'daki klasik hizmet dağıtımı Configuration Manager kullanım için kullanım dışıdır. Bu sürüm, bu Azure dağıtımlarını oluşturmayı desteklemeye yönelik son sürümdür.

Mevcut dağıtımlar çalışmaya devam eder. Bu geçerli dal sürümünden itibaren, bulut yönetimi ağ geçidi ve bulut dağıtım noktasının yeni örnekleri için tek dağıtım mekanizmasıdır Azure Resource Manager.

Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidi için Azure Resource Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Sınır gruplarına bulut yönetimi ağ geçidi ekleme

<!--3640932-->
Artık bir bulut yönetimi ağ geçidini (CMG) bir sınır grubuyla ilişkilendirebilirsiniz. Bu yapılandırma, istemcilerin sınır grubu ilişkilerine göre istemci iletişimi için varsayılan veya CMG 'ye geri dönüş yapmasına izin verir. Bu davranış özellikle şube ofisi ve VPN senaryolarında yararlı olur. İstemci trafiğini pahalı ve yavaş WAN bağlantılarından, bunun yerine Microsoft Azure için daha hızlı internet bağlantıları kullanmak üzere yönlendirebilirsiniz.

Daha fazla bilgi için bkz. [CMG hiyerarşi tasarımı](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design) ve [CMG 'yi ayarlama](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Gerçek zamanlı yönetim

### <a name="run-cmpivot-from-the-central-administration-site"></a>Merkezi yönetim sitesinden CMPivot çalıştırma

<!--3610960-->
Configuration Manager artık hiyerarşide merkezi yönetim sitesinden CMPivot çalıştırılmasını desteklemektedir. Birincil site, istemci iletişimini hala işler. Merkezi yönetim sitesinden CMPivot çalıştırılırken, yüksek hızlı ileti abonelik kanalının birincil sitesiyle iletişim kurar. Bu iletişim, siteler arasında standart SQL çoğaltmasına bağlı değildir.

Daha fazla bilgi için bkz. [CMPivot for Real Time Data](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1902).

### <a name="edit-or-copy-powershell-scripts"></a>PowerShell betikleri düzenleme veya kopyalama

<!--3705507-->
Artık betikleri Çalıştır özelliği ile kullanılan mevcut bir PowerShell betiğini **düzenleyebilir** veya **kopyalayabilirsiniz** . Değiştirmeniz gereken bir betiği yeniden oluşturmak yerine, şimdi doğrudan düzenleyin. Her iki eylem de yeni bir komut dosyası oluştururken kullandığınız sihirbaz deneyimini kullanır. Bir betiği düzenlerken veya kopyaladığınızda, Configuration Manager onay durumunu kalıcı durumdan tutmaz.

Daha fazla bilgi için bkz. [betikleri çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit).


## <a name="content-management"></a><a name="bkmk_content"></a> İçerik yönetimi

### <a name="distribution-point-maintenance-mode"></a>Dağıtım noktası bakım modu

<!--3555754-->

Artık bakım modunda bir dağıtım noktası ayarlayabilirsiniz. Yazılım güncelleştirmelerini yüklerken veya sunucuda donanım değişiklikleri yaparken bakım modunu etkinleştirin.

Dağıtım noktası bakım modundayken aşağıdaki davranışlara sahiptir:

- Site herhangi bir içerik dağıtmaz.  

- Yönetim noktaları, bu dağıtım noktasının konumunu istemcilere döndürmez.

- Siteyi güncelleştirdiğinizde bakım modundaki bir dağıtım noktası hala güncellenir.

- Dağıtım noktası özellikleri salt okunurdur. Örneğin, sertifikayı değiştiremez veya sınır grupları ekleyemezsiniz.  

- İçerik doğrulama gibi herhangi bir zamanlanmış görev hala aynı zamanlamaya göre çalışır.

Bu özellik hakkında daha fazla bilgi için bkz. [bakım modu](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint).

Configuration Manager SDK ile bu işlemi otomatikleştirme hakkında daha fazla bilgi için, bkz. [SetDPMaintenanceMode Method in class SMS_DistributionPointInfo](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="client-management"></a><a name="bkmk_client"></a> İstemci yönetimi

### <a name="client-provisioning-mode-timeout"></a>İstemci sağlama modu zaman aşımı

<!--3197824-->
Görev sırası, istemciyi sağlama moduna geçirir zaman damgası ayarlar. Sağlama modundaki bir istemci, zaman damgasından bu yana geçen süreyi her 60 dakikada bir denetler. 48 saatten uzun bir süredir sağlama modundayken istemci, sağlama modundan otomatik olarak çıkar ve işlemini yeniden başlatır.

Daha fazla bilgi için bkz. [sağlama modu](../../../osd/understand/provisioning-mode.md).

### <a name="view-first-screen-only-during-remote-control"></a>Yalnızca uzaktan denetim sırasında ilk ekranı görüntüle

<!--3231732-->
İki veya daha fazla izleyici içeren bir istemciye bağlanırken, bunların tümünü Configuration Manager uzak denetim görüntüleyicisinde görüntülemek zor olabilir. Bir uzak Araçlar işleci artık **tüm ekranları** veya yalnızca **ilk ekranı** görmek arasında seçim yapabilir.

Daha fazla bilgi için bkz. [bir Windows istemci bilgisayarını uzaktan yönetme](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="specify-a-custom-port-for-peer-wakeup"></a>Eş Uyandırma için özel bir bağlantı noktası belirtin

<!--3605925-->
Artık, uyandırma proxy 'si için özel bir bağlantı noktası numarası belirtebilirsiniz. İstemci ayarları ' nda, **güç yönetimi** grubunda, **LAN'da Uyandırma bağlantı noktası numarası (UDP)** ayarını yapılandırın.  

Daha fazla bilgi için bkz. [LAN 'Da uyandırma yapılandırma](../../clients/deploy/configure-wake-on-lan.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Uygulama yönetimi

### <a name="improvements-to-application-approvals-via-email"></a>Uygulama onayları ile e-posta aracılığıyla iyileştirmeler

<!--3594063-->
Bu sürüm, uygulama isteklerine yönelik e-posta bildirimleri almak için özellik geliştirmeleri içerir. Kullanıcılar, yazılım merkezi 'nden isteğe her zaman bir yorum ekleyebilir. Bu açıklama Configuration Manager konsolundaki uygulama isteğini gösterir. Artık bu açıklama e-postada de gösteriliyor. Bu yorumu e-postaya eklemek, onaylayanlara isteği onaylama veya reddetme konusunda daha iyi bir karar vermesini sağlar.

Daha fazla bilgi için bkz. [e-posta bildirimleri](../../../apps/deploy-use/app-approval.md#bkmk_email-approve).

### <a name="improvements-to-package-conversion-manager"></a>Paket Dönüştürme Yöneticisi geliştirmeleri

<!-- SCCMDocs-pr issue #3357 -->
Bu sürüm, [Paket Dönüştürme Yöneticisi](../../../apps/pcm/package-conversion-manager.md)için aşağıdaki geliştirmeleri içerir:

- Zamanlanan paket analizi varsayılan olarak 7 günde bir çalışır
- Paketleri çözümlemek ve dönüştürmek için PowerShell cmdlet 'leri
- Genel hata düzeltmeleri ve geliştirmeleri


## <a name="os-deployment"></a><a name="bkmk_osd"></a> İşletim sistemi dağıtımı

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Yerinde yükseltme görev sırası sırasında ilerleme durumu

<!--3747129-->
Artık Windows 10 yerinde yükseltme görev sırası sırasında daha ayrıntılı bir ilerleme çubuğu görürsünüz. Bu çubuk, görev sırası sırasında başka bir şekilde sessiz olan Windows kurulumunun ilerlemesini gösterir. Kullanıcılar artık temeldeki ilerleme için bazı görünürlüğe sahiptir. İlerleme durumu gösterimi nedeniyle yükseltme işleminin askıya alınması kaygılarıyla yardımcı olur.  

![Windows yükseltme ilerleme durumuyla örnek görev sırası ilerlemesi](media/3747129-installation-progress.png)

Bu özellik, Windows 10 ' un desteklenen herhangi bir sürümüyle ve yalnızca yerinde yükseltme görev dizisiyle birlikte kullanılabilir.

### <a name="improvements-to-task-sequence-media-creation"></a>Görev dizisi medya oluşturma geliştirmeleri

<!--3556027, fka 1359388-->
Bu sürüm, görev sırası medyasını daha iyi oluşturup yönetmenize yardımcı olmak için çeşitli geliştirmeler içerir. Daha fazla bilgi için, belirli medya türleri için aşağıdaki makalelere bakın:

- [Tek başına medya oluşturma](../../../osd/deploy-use/create-stand-alone-media.md)
- [Önceden hazırlanan ortam oluşturma](../../../osd/deploy-use/create-prestaged-media.md)
- [Önyüklenebilir ortam oluşturma](../../../osd/deploy-use/create-bootable-media.md)
- [Yakalama ortamı oluşturma](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>Geçici depolama belirtin

Görev sırası medyası oluşturduğunuzda, artık sitenin geçici veri depolaması için kullandığı konumu özelleştirin. Bu işlem, çok fazla sayıda geçici sürücü alanı gerektirebilir. Bu değişiklik, bu geçici dosyaları nerede depolayabileceğiniz hakkında daha fazla esneklik sağlar.

**Görev sırası medyası oluşturma Sihirbazı**'Nda, **hazırlama klasörü**için bir konum belirtin. Varsayılan olarak, bu konum şu yola benzer: `%UserProfile%\AppData\Local\Temp` .

#### <a name="add-a-label-to-the-media"></a>Medyaya bir etiket ekleyin

Artık, görev sırası medyasına bir etiket ekleyebilirsiniz. Bu etiket, medyayı oluşturduktan sonra daha iyi tanımanıza yardımcı olur. **Görev sırası medyası oluşturma Sihirbazı**'Nda bir **medya etiketi**belirtin.

### <a name="import-a-single-index-of-an-os-image"></a>Bir işletim sistemi görüntüsünün tek bir dizinini içeri aktarma

<!--3719699-->
Configuration Manager için bir Windows resim (WıM) dosyası içeri aktarılırken, dosyadaki tüm görüntü dizinleri yerine otomatik olarak tek bir dizin içeri aktarmayı belirtebilirsiniz. Bu seçenek aşağıdaki avantajları sağlar:

- Küçük resim dosyası  
- Daha hızlı çevrimdışı bakım  
- Çevrimdışı bakımın ardından daha küçük bir görüntü dosyası için görüntü bakımını iyileştirme

Bir işletim sistemi görüntüsünü içeri aktardığınızda, **BELIRTILEN WIM dosyasından belirli bir görüntü dizinini ayıklama**seçeneğini belirleyin. Sonra listeden görüntü dizini ' ni seçin.  

Daha fazla bilgi için bkz. [işletim sistemi görüntüsü ekleme](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages).

### <a name="optimized-image-servicing"></a>İyileştirilmiş görüntü Bakımı

<!--3555951-->
Yazılım güncelleştirmelerini bir işletim sistemi görüntüsüne uyguladığınızda, yenisiyle değiştirilen tüm güncelleştirmeleri kaldırarak çıktıyı iyileştirmek için yeni bir seçenek vardır. Çevrimdışı hizmet verme iyileştirmesi yalnızca tek bir dizine sahip görüntüler için geçerlidir.

Bir işletim sistemi görüntüsünü güncelleştirmek için bir zamanlama oluşturduğunuzda, **görüntü güncelleştirildikten sonra yenisiyle değiştirilen güncelleştirmeleri kaldırma**seçeneğini belirleyin.

Daha fazla bilgi için bkz. [bir görüntüye yazılım güncelleştirmelerini uygulama](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase).

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>PowerShell betiği çalıştırma geliştirmeleri görev dizisi adımı

<!--3556028, fka 1359389-->
**PowerShell betiğini Çalıştır** görev dizisi adımı artık aşağıdaki geliştirmeleri içerir:  

- Artık Windows PowerShell kodunu bu adımda doğrudan girebilirsiniz. Bu değişiklik, bir görev sırası sırasında, komut dosyası ile bir paket oluşturmadan ve dağıtmadan PowerShell komutlarını çalıştırmanızı sağlar.

- **PowerShell betiği gir** seçeneğini belirlediğinizde **betiği Düzenle**' yi seçin. Yeni PowerShell betiği penceresi aşağıdaki eylemleri sağlar:  

    - Betiği doğrudan Düzenle  

    - Dosyadan var olan bir betiği aç  

    - Configuration Manager ' de var olan bir onaylanan betiğe gidin

- Betik çıkışını özel bir görev dizisi değişkenine kaydetme  

- Komut dosyası parametrelerini görev sırası günlüğüne eklemek için, **Osdlogpowershellparameters** görev sırası değişkenini **true**olarak ayarlayın. Varsayılan olarak parametreler günlükte değildir.  

- [Komut satırını Çalıştır](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) adımı olarak benzer işlevler sağlayan diğer geliştirmeler. Örneğin, Alternatif Kullanıcı kimlik bilgilerini belirtin veya bir zaman aşımı belirtin.

> [!Important]  
> Bu yeni Configuration Manager özelliğinden yararlanmak için, siteyi güncelleştirdikten sonra da istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

Daha fazla bilgi için bkz. [PowerShell betiğini çalıştırma](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

### <a name="other-improvements-to-os-deployment"></a>İşletim sistemi dağıtımına yönelik diğer geliştirmeler

<!--3633146,3641475,3654172,3734270-->
Bu sürüm, işletim sistemi dağıtımına yönelik aşağıdaki geliştirmeleri içerir:

- Görev sıralarında yeni bir varsayılan **görüntüleme** eylemi vardır. <!--3633146-->  

- Görev dizisi hatası iletişim penceresi artık daha fazla bilgi görüntülüyor. Başarısız olan görev dizisi adımının adını gösterir. <!--3641475-->  

- **Osddonotlogcommand** görev dizisi değişkenini true olarak ayarladığınızda, artık günlük dosyasındaki komut satırını Çalıştır adımından komut satırını da gizler. Daha önce, program adını yalnızca Smsts. log dosyasındaki paketi Kur adımından maskeleyordu.<!--3654172-->  

- Windows dağıtım hizmeti olmadan bir dağıtım noktasında bir PXE Yanıtlayıcı 'yı etkinleştirdiğinizde, artık DHCP hizmetiyle aynı sunucuda olabilir. <!--3734270--> Daha fazla bilgi için bkz. [PXE isteklerini kabul etmek için en az bir dağıtım noktasını yapılandırma](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


## <a name="software-center"></a><a name="bkmk_userxp"></a> Yazılım Merkezi

### <a name="replace-toast-notifications-with-dialog-window"></a>Bildirim bildirimlerini iletişim kutusu penceresiyle değiştirme

<!--3555947-->
Bazen kullanıcılar, bir yeniden başlatma veya gerekli dağıtım hakkındaki Windows bildirim bildirimini görmez. Ardından, anımsatıcıyı erteleme deneyimini görmez. Bu davranış, istemci son tarihe ulaştığında kötü bir kullanıcı deneyimine yol açabilir.

Artık dağıtımlar için yeniden başlatma veya yazılım değişikliği yapılması gerektiğinde, daha zorlayıcı bir iletişim kutusu penceresi kullanma seçeneğiniz vardır.

Daha fazla bilgi için bkz. [plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)

### <a name="configure-user-device-affinity-in-software-center"></a>Yazılım Merkezi 'nde Kullanıcı cihaz benzeşimini yapılandırma

<!--3485366-->
Sürüm 1806 ' den başlayarak [yazılım merkezi altyapı geliştirmeleri](whats-new-in-version-1806.md#software-center-infrastructure-improvements) sayesinde, çoğu senaryo için Uygulama Kataloğu site sunucusu rolleri artık gerekli değildir. Bazı müşteriler, kullanıcıların Kullanıcı cihaz benzeşimi için birincil cihazlarını ayarlamaya izin veren uygulama kataloğu 'na hala güvenmektedir.

Artık kullanıcılar, yazılım merkezi 'nde birincil cihazlarını ayarlayabilir. Bu eylem, Configuration Manager ' de cihazın birincil kullanıcısı yapar.

Daha fazla bilgi için bkz. [kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi Ile bağlama](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="configure-default-views-in-software-center"></a>Yazılım Merkezi 'nde varsayılan görünümleri yapılandırma

<!--3612112-->
Configuration Manager bu sürümü, yazılım merkezi 'ni nasıl özelleştirebileceğinizi daha da yineler:

- Uygulamaların varsayılan yerleşimini kutucuk veya liste olarak ayarlayın  

    - Bir Kullanıcı bu yapılandırmayı değiştirirse, yazılım merkezi kullanıcının gelecekte tercih ettiği tercihi sürdürür  

- Varsayılan uygulama filtresini ya da yalnızca gerekli uygulamaları yapılandırın  

    - Software Center her zaman varsayılan ayarınızı kullanır. Kullanıcılar bu filtreyi değiştirebilir, ancak yazılım merkezi 'nin tercih etmesi devam etmez.

Bu ayarları istemci ayarları **Yazılım Merkezi** grubunda belirtin.

Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults).


## <a name="software-updates"></a><a name="bkmk_sum"></a> Yazılım güncelleştirmeleri

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Windows 10 Bakımı 'nda özellik güncelleştirmeleri için öncelik belirtme

<!--3734525-->
[Windows 10 Bakımı](../../../osd/deploy-use/manage-windows-as-a-service.md)aracılığıyla istemcilerin bir özellik güncelleştirmesini yükleyen önceliği ayarlayın. Varsayılan olarak, istemciler artık daha yüksek işlem önceliğine sahip Özellik güncelleştirmelerini yükler.

Bu seçeneği yapılandırmak için istemci ayarlarını kullanın. **Yazılım güncelleştirmeleri** grubunda, aşağıdaki ayarı yapılandırın: **özellik güncelleştirmeleri için Iş parçacığı önceliği belirtin**.

Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../clients/deploy/about-client-settings.md#software-updates).


## <a name="office-management"></a><a name="bkmk_o365"></a> Office yönetimi

### <a name="redirect-windows-known-folders-to-onedrive"></a>Windows bilinen klasörlerini OneDrive 'a yönlendir

<!--3556021-->
Windows bilinen klasörlerini OneDrive Iş 'e taşımak için Configuration Manager kullanın. Bu klasörler Masaüstü, belgeler ve resimleri içerir. Windows 10 yükseltmelerinizi basitleştirmek için, bir görev dizisini dağıtmadan önce bu ayarları Windows 7 istemcilerine dağıtın.

OneDrive Iş 'in bu özelliği hakkında daha fazla bilgi için bkz. [yeniden yönlendirme ve Windows bilinen klasörlerini OneDrive 'a taşıma](/onedrive/redirect-known-folders).

İlk olarak, [Office 365 KIRACı kimliğinizi bulun](/onedrive/find-your-office-365-tenant-id). Ardından OneDrive Sync Client sürüm 18.111.0603.0004 veya üstünü dağıtın. Daha fazla bilgi için bkz. [Configuration Manager kullanarak OneDrive uygulamaları dağıtma](/onedrive/deploy-on-windows).  

Bir OneDrive Iş profili oluşturup dağıtmak için, Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Uyumluluk ayarları**' nı genişletin ve **OneDrive iş profilleri** düğümünü seçin.  

Daha fazla bilgi için [OneDrive Iş profilleri](../../../compliance/deploy-use/onedrive-profile.md) makalesindeki Windows bilinen klasörleri OneDrive 'A yeniden yönlendir bölümüne bakın.

### <a name="integration-for-office-365-proplus-readiness"></a>Office 365 ProPlus hazırlığı için tümleştirme

<!--3735402-->
Office 365 ProPlus 'a yükseltmeye hazırlanma ve yüksek güvenilirlikli cihazları tanımlamak için Configuration Manager kullanın. Tümleştirme, ortamınızda kullanılan Office eklentileri ve makroları ile ilgili olası uyumluluk sorunları hakkında öngörüler sağlar. Ardından Configuration Manager kullanarak Office 'i kullanıma hazırlamış cihazlara dağıtın.

Mevcut Office 365 istemci yönetimi panosu artık yeni bir kutucuk içerir, **office 365 ProPlus yükseltme hazırlığı**.

Daha fazla bilgi için bkz. [Office 365 istemci yönetimi panosu](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness)

### <a name="additional-languages-for-office-365-updates"></a>Office 365 güncelleştirmeleri için ek diller

<!--3555955-->
Configuration Manager artık Office 365 istemci güncelleştirmeleri için desteklenen tüm dilleri desteklemektedir. Güncelleştirme iş akışı artık **Office 365 Istemci güncelleştirmesi**için çok sayıda dilde **Windows Update** için 38 dillerini ayırır.

Daha fazla bilgi için bkz. [Office 365 güncelleştirmelerini yönetme](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang)

### <a name="office-products-on-lifecycle-dashboard"></a>Yaşam döngüsü panosundaki Office ürünleri

<!--3556026-->
Ürün yaşam döngüsü panosu artık Office 2016 ' nin yüklü Office 2003 sürümleriyle ilgili bilgileri içerir. Veriler, her 24 saatte bir olan yaşam döngüsü özetleme görevini çalıştırdıktan sonra görüntülenir.

Daha fazla bilgi için bkz. [ürün yaşam döngüsü panosunu kullanma](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


## <a name="phased-deployments"></a><a name="bkmk_pod"></a> Aşamalı dağıtımlar

### <a name="dedicated-monitoring-for-phased-deployments"></a>Aşamalı dağıtımlar için adanmış izleme

<!--3555949-->
Aşamalı dağıtımlar artık kendi adanmış izleme düğümüne sahiptir. Bu düğüm, oluşturduğunuz aşamalı dağıtımları belirlemeyi kolaylaştırır ve ardından aşamalı dağıtım izleme görünümüne gidin. Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **aşamalı dağıtımlar** düğümünü seçin. Aşamalı dağıtımlar listesini gösterir.

Daha fazla bilgi için bkz. [aşamalı dağıtım izleme görünümü](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor).

### <a name="improvement-to-phased-deployment-success-criteria"></a>Aşamalı dağıtım başarı ölçütlerine iyileştirme

<!--3555946-->
Aşamalı dağıtımda bir aşamanın başarısı için ek ölçüt belirtin. Yalnızca bir yüzde değeri yerine bu ölçüt artık başarıyla dağıtılan cihazların sayısı da olabilir. Bu seçenek, koleksiyonun boyutu değişken olduğunda ve sonraki aşamaya geçmeden önce başarıyı göstermek için belirli sayıda cihaza sahip olduğunuzda yararlıdır.

Bir görev dizisi, yazılım güncelleştirmesi veya uygulama için aşamalı dağıtım oluşturun. Sihirbazın Ayarlar sayfasında, ilk aşamanın başarısı için ölçüt olarak şu seçeneği belirleyin: **başarıyla dağıtılan cihaz sayısı**.

Daha fazla bilgi için bkz. [aşamalı dağıtımlar oluşturma](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager konsolu

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a> Configuration Manager konsolundaki iyileştirmeler

<!--3594151-->
Orta Batı yönetim Zirvesi sürüm 2018 ' de müşteri geri bildirimlerine bağlı olarak, bu sürüm Configuration Manager konsoluna aşağıdaki geliştirmeleri içerir:

- Uygulama algılama yöntemlerine ait kayıt defteri penceresini en üst düzeye çıkarın
- Uygulama dağıtımından koleksiyona git
- İzleme durumundan içeriği kaldır
- Görünümler, **izleme** çalışma alanının **dağıtımlar** düğümündeki tamsayı değerlerine göre sıralanır
- Uyarıyı çok sayıda sonuç için taşıma

Daha fazla bilgi için bkz. [Configuration Manager konsol ipuçları](../../servers/manage/admin-console-tips.md).

### <a name="configuration-manager-console-notifications"></a>Configuration Manager konsol bildirimleri

<!--3556016, fka 1318035-->
Uygun eylemi gerçekleştirebileceğiniz için daha iyi bilgilendirilmek için Configuration Manager konsolu artık aşağıdaki olayları size bildirir:

- Configuration Manager için bir güncelleştirme kullanılabilir olduğunda
- Ortamda yaşam döngüsü ve bakım olayları gerçekleştiğinde

Bu bildirim, şeridin altındaki konsol penceresinin en üstünde yer aldığı bir çubukdur. Configuration Manager güncelleştirmeler kullanılabilir olduğunda önceki deneyimin yerini alır. Bu konsol içi bildirimlerde hala kritik bilgiler görüntülenir, ancak konsolda çalışmalarınız kesintiye uğramaz. Kritik bildirimleri yok sayabilirsiniz. Konsol, tüm bildirimleri başlık çubuğunun yeni bir bildirim alanında görüntüler.

Daha fazla bilgi için bkz. [Configuration Manager konsol bildirimleri](../../servers/manage/admin-console-notifications.md).

### <a name="confirmation-of-console-feedback"></a>Konsol geri bildirimi onayı

<!--3556010-->
Configuration Manager konsolunda [geri bildirim](../../understand/find-help.md#product-feedback) gönderdiğinizde, şimdi bir onay iletisi görüntülenir. Bu ileti, izleme tanımlayıcısı olarak Microsoft 'a verebileceğiniz bir **geri BILDIRIM kimliği**içerir.

Daha fazla bilgi için bkz. [ürün geri bildirimi](../../understand/find-help.md#bkmk_feedbackid).

### <a name="view-recently-connected-consoles"></a>Son bağlantılı konsolları görüntüle

<!--3699367-->
Artık Configuration Manager konsolunun en son bağlantılarını görüntüleyebilirsiniz. Görünüm etkin bağlantıları ve yakın zamanda bağlanan konsolları içerir. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **güvenlik**' i genişletin ve **konsol bağlantıları** düğümünü seçin.

Daha fazla bilgi için, bkz. [Configuration Manager konsolunu kullanma](../../servers/manage/admin-console.md#bkmk_viewconnected).

### <a name="in-console-documentation-dashboard"></a>Konsol içi belge panosu

<!--3556019, fka 1357546-->
Yeni **topluluk** çalışma alanında yeni bir **belge** düğümü vardır. Bu düğüm Configuration Manager belge ve destek makaleleri hakkında güncel bilgiler içerir.

Daha fazla bilgi için, bkz. [Configuration Manager konsolunu kullanma](../../servers/manage/admin-console.md#bkmk_doc-dashboard).

### <a name="search-device-views-using-mac-address"></a>MAC adresini kullanarak cihaz görünümlerini ara

<!--3600878-->
Artık Configuration Manager konsolunun bir cihaz görünümünde bir MAC adresi araması yapabilirsiniz. Bu özellik, PXE tabanlı dağıtımlarda sorun giderirken işletim sistemi dağıtımı yöneticileri için yararlıdır. Cihazların listesini görüntülediğinizde, **Mac adresi** sütununu görünüme ekleyin. **Mac adresi** arama ölçütlerini eklemek için arama alanını kullanın.

Daha fazla bilgi için bkz. [Configuration Manager konsol ipuçları](../../servers/manage/admin-console-tips.md).

### <a name="use-net-47-for-improved-console-accessibility"></a>Geliştirilmiş konsol erişilebilirliği için .NET 4,7 kullanma

<!-- SCCMDocs-pr issue #3228 -->
Configuration Manager konsolunun erişilebilirlik özelliklerini geliştirmek için, konsolunu çalıştıran bilgisayarda .NET 'i 4,7 veya sonraki bir sürüme güncelleştirin.

Daha fazla bilgi için bkz. [Configuration Manager erişilebilirlik özellikleri](../../understand/accessibility-features.md).

### <a name="changes-to-console-setup-process"></a>Konsol kurulum işlemindeki değişiklikler

<!-- 3612513 -->
Configuration Manager konsolu yüklenirken gerekli yeni bileşenler vardır. Konsolunu başka bilgisayarlara yüklemek için bir paket oluşturursanız, paketin aşağıdaki dosyaları içerdiğinden emin olun:

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

Bir site sunucusu yüklediğinizde veya güncelleştirdiğinizde, bu yükleme dosyalarını ve site için desteklenen dil paketlerini **Tools\consolesetup** alt klasörüne kopyalar. Daha fazla bilgi için [Configuration Manager konsolunu yüklemeye](../../servers/deploy/install/install-consoles.md)bakın.


## <a name="other-updates"></a>Diğer güncelleştirmeler

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 1902](https://support.microsoft.com/help/4498910).

Configuration Manager için Windows PowerShell cmdlet 'lerinde yapılan değişiklikler hakkında daha fazla bilgi için bkz. [PowerShell sürüm 1902 sürüm notları](/powershell/sccm/1902-release-notes?view=sccm-ps).

Aşağıdaki güncelleştirme paketi (4500571) konsolunda 17 Haziran 2019 tarihinden itibaren kullanılabilir: [güncelleştirme paketi Configuration Manager geçerli dalı, sürüm 1902](https://support.microsoft.com/help/4500571).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Sonraki adımlar

Bu sürümü yüklemeye hazırsanız, [güncelleştirme 1902 ' i yüklemek için](../../servers/manage/checklist-for-installing-update-1902.md) [Configuration Manager güncelleştirmeleri](../../servers/manage/updates.md) ve denetim listesini yükleme bölümüne bakın.

> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanın.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:    
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)  

Bilinen, önemli sorunlar için bkz. [sürüm notları](../../servers/deploy/install/release-notes.md).

Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist)de gözden geçirin.