---
title: Sürüm 2002’deki yenilikler
titleSuffix: Configuration Manager
description: Geçerli dalın Configuration Manager sürüm 2002 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 07/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c5107ffe26c72852cbc1dbaa15eb19a990c7939
ms.sourcegitcommit: 034226b5a60de49a75c7b54e856814f81c03a112
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86422857"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Geçerli dalın Configuration Manager sürüm 2002 ' deki yenilikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme 2002, konsol içi bir güncelleştirme olarak sunulmaktadır. Sürüm 1810 veya üstünü çalıştıran sitelerde bu güncelleştirmeyi uygulayın. <!-- baseline only statement:-->Yeni bir site yüklerken, taban çizgisi sürümü olarak da kullanılabilir. Bu makalede Configuration Manager, sürüm 2002 ' deki değişiklikler ve yeni özellikler özetlenmektedir.

Bu güncelleştirmeyi yüklemek için her zaman en son denetim listesini gözden geçirin. Daha fazla bilgi için bkz. [güncelleştirme 2002 yükleme denetim listesi](../../servers/manage/checklist-for-installing-update-2002.md). Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist)de gözden geçirin.

Yeni Configuration Manager özelliklerinden tam olarak yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme de güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

> [!TIP]
> Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a>Microsoft Uç Nokta Yöneticisi kiracı iliştirme

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Cihaz eşitleme ve cihaz eylemleri
<!--3555758-->
Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U **Microsoft Endpoint Manager Yönetim Merkezi**adlı tek bir konsolda bir araya getirir. Bu sürümden itibaren, Configuration Manager cihazlarınızı bulut hizmetine yükleyebilir ve yönetim merkezindeki **cihazlar** dikey penceresinden eylemler gerçekleştirebilirsiniz.

Daha fazla bilgi için bkz. [Microsoft Endpoint Manager kiracı iliştirme](../../../tenant-attach/device-sync-actions.md).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Site altyapısı

### <a name="remove-a-central-administration-site"></a>Merkezi yönetim sitesini kaldırma
<!-- 3607277 -->

Hiyerarşiniz bir merkezi yönetim sitesinden (CAS) ve tek bir alt birincil siteden oluşuyorsa, artık CA 'ları kaldırabilirsiniz. Bu eylem, Configuration Manager altyapınızı tek bir tek başına birincil siteye basitleştirir. Siteden siteye çoğaltmanın karmaşıklıklarını ortadan kaldırır ve yönetim görevlerinizi tek birincil siteye odaklanır.

Daha fazla bilgi için bkz. [CA 'Ları kaldırma](../../servers/deploy/install/remove-central-administration-site.md).

### <a name="new-management-insight-rules"></a>Yeni yönetim Insight kuralları

Bu sürüm aşağıdaki yönetim Insight kurallarını içerir:

- Microsoft Premier alan Mühendisliği **Configuration Manager değerlendirme** grubunda dokuz kural. Bu kurallar, Microsoft Premier 'in hizmet hub 'ında sağladığı pek çok daha fazla denetim örneğidir.<!-- 3607758 -->

  - Active Directory güvenlik grubu bulma işlemi çok sık çalışacak şekilde yapılandırıldı
  - Active Directory sistem keşfi çok sık çalışacak şekilde yapılandırıldı
  - Active Directory Kullanıcı keşfi çok sık çalışacak şekilde yapılandırıldı
  - Tüm sistemler veya tüm kullanıcılar ile sınırlı Koleksiyonlar
  - Sinyal keşfi devre dışı
  - Artımlı güncelleştirmeler için etkinleştirilen uzun süre çalışan koleksiyon sorguları
  - Dağıtım noktalarındaki uygulama ve paket sayısını azaltma
  - İkincil site yükleme sorunları
  - Tüm siteleri aynı sürüme Güncelleştir

- Güvenli HTTPS iletişimi eklemek için sitenizi yapılandırmanıza yardımcı olmak üzere **Cloud Services** grubunda iki ek kural:<!-- 6268489 -->

  - Doğru HTTPS yapılandırmasına sahip olmayan siteler
  - Cihazlar Azure AD 'ye yüklenmedi

Daha fazla bilgi için bkz. [Management Insights](../../servers/manage/management-insights.md).

### <a name="improvements-to-administration-service"></a>Yönetim hizmeti geliştirmeleri

<!-- 5728365 -->

Yönetim hizmeti, SMS sağlayıcısı için bir REST API. Daha önce, aşağıdaki bağımlılıklardan birini uygulamanız gerekiyordu:

- Tüm site için gelişmiş HTTP 'yi etkinleştirin
- SMS sağlayıcısı rolünü barındıran sunucuda, PKI tabanlı bir sertifikayı IIS 'ye el ile bağlama

Bu sürümden itibaren, yönetim hizmeti otomatik olarak sitenin otomatik olarak imzalanan sertifikasını kullanır. Bu değişiklik, yönetim hizmetinin daha kolay kullanılması için bir savunma azaltmaya yardımcı olur. Site her zaman bu sertifikayı oluşturur. **Http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanmak** üzere geliştirilmiş http sitesi ayarı, yalnızca site sistemlerinin kullanıp kullanmadığını denetler. Artık yönetim hizmeti bu site ayarını yoksayar, çünkü başka bir site sistemi, gelişmiş HTTP kullanmıyor olsa bile her zaman sitenin sertifikasını kullanır. PKI tabanlı bir sunucu kimlik doğrulama sertifikası kullanmaya devam edebilirsiniz.

Daha fazla bilgi için aşağıdaki yeni makalelere bakın:

- [Yönetim hizmeti nedir?](../../../develop/adminservice/overview.md)
- [Yönetim hizmetini ayarlama](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Azure Active Directory bulma ve grup eşitleme için ara sunucu desteği

<!-- 5913817 -->

Kimlik doğrulaması da dahil olmak üzere site sisteminin ara sunucu ayarları şu şekilde kullanılır:

- Azure Active Directory (Azure AD) Kullanıcı keşfi
- Azure AD Kullanıcı grubu bulma
- Koleksiyon üyeliği sonuçlarını Azure Active Directory gruplarıyla eşitleme

Daha fazla bilgi için bkz. [proxy sunucu desteği](../network/proxy-server-support.md#bkmk_other).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>Buluta bağlı yönetim

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>Kritik durum iletisi gerekli uç noktalara sunucu bağlantı hatalarını gösterir

<!-- 5566763 -->

Configuration Manager site sunucusu bir bulut hizmeti için gerekli uç noktalara bağlanamazsa, kritik bir durum ileti KIMLIĞI 11488 oluşturur. Site sunucusu hizmete bağlanamıyorsa, SMS_SERVICE_CONNECTOR bileşen durumu kritik olarak değişir. Configuration Manager konsolunun bileşen durumu düğümünde ayrıntılı durumu görüntüleyin.

### <a name="token-based-authentication-for-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi için belirteç tabanlı kimlik doğrulaması

<!-- 5686290 -->

Bulut yönetimi ağ geçidi (CMG) birçok tür istemciyi destekler, ancak gelişmiş HTTP ile birlikte bu istemciler istemci kimlik doğrulama sertifikası gerektirir. Bu sertifika gereksinimi, genellikle dahili ağa bağlanmayan, Azure Active Directory (Azure AD) kalamamayan ve PKI tarafından verilen bir sertifika yüklemek için bir yönteme sahip olmayan Internet tabanlı istemcilere sağlanması zor olabilir.

Configuration Manager, aşağıdaki yöntemlerle cihaz desteğini genişletir:

- Benzersiz bir belirteç için iç ağa kaydolun
- Internet tabanlı cihazlar için toplu kayıt belirteci oluşturma

Daha fazla bilgi için bkz. [CMG Için belirteç tabanlı kimlik doğrulaması](../../clients/deploy/deploy-clients-cmg-token.md).

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Microsoft uç nokta Configuration Manager bulut özellikleri

<!--5834830-->

Microsoft Endpoint Manager Yönetim merkezinde yeni bulut tabanlı özellikler veya şirket içi Configuration Manager yüklemeniz için diğer bağlı bulut hizmetleri kullanılabilir olduğunda, artık Configuration Manager konsolundaki bu yeni özellikleri tercih edebilirsiniz. Configuration Manager konsolundaki özellikleri etkinleştirme hakkında daha fazla bilgi için bkz. [güncelleştirmelerden isteğe bağlı özellikleri etkinleştirme](../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Masaüstü Analizi

Masaüstü Analizi bulut hizmetindeki aylık değişiklikler hakkında daha fazla bilgi için bkz. [Masaüstü](../../../desktop-analytics/whats-new.md)analizine ilişkin yenilikler.

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>Bağlantı sistem durumu panosu istemci bağlantı sorunlarını gösterir

İstemcilerin bağlantı durumunu izlemek için Configuration Manager 'deki masaüstü Analizi bağlantı sistem durumu panosunu kullanın. Artık iki alanda istemci ara sunucu yapılandırma sorunlarını daha kolay bir şekilde tanımanıza yardımcı olur:

- **Uç nokta bağlantısı denetimleri**: istemciler gerekli bir uç noktaya ulaşamazsa, panoda bir yapılandırma uyarısı görürsünüz. Proxy yapılandırma sorunları nedeniyle istemcilerin bağlanamadığı uç noktaları görmek için detaya gidin.<!-- 4963230 -->

- **Bağlantı durumu**: Istemcileriniz, masaüstü Analizi bulut hizmetine erişmek için bir proxy sunucusu kullanıyorsa, Configuration Manager artık istemcilerden gelen proxy kimlik doğrulama sorunlarını gösterir. Ara sunucu kimlik doğrulaması nedeniyle kaydedemeyecek istemcileri görmek için detaya gidin.<!-- 4963383 -->

Daha fazla bilgi için bkz. [bağlantı durumunu izleme](../../../desktop-analytics/monitor-connection-health.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a>Gerçek zamanlı yönetim

### <a name="improvements-to-cmpivot"></a>CMPivot geliştirmeleri

<!-- 5870934 -->

CMPivot varlıklarından gezinmeyi kolaylaştırdık. Artık CMPivot varlıklarda arama yapabilirsiniz. Varlıkları ve varlık nesne türlerini kolayca ayırt etmek için de yeni simgeler eklenmiştir.

Daha fazla bilgi için bkz. [CMPivot](../../servers/manage/cmpivot.md#bkmk_2002).

## <a name="content-management"></a><a name="bkmk_content"></a>İçerik yönetimi

### <a name="exclude-certain-subnets-for-peer-content-download"></a>Eş içerik indirme için bazı alt ağları hariç tut

<!-- 3555777 -->

Sınır grupları, eş indirmeleri için aşağıdaki seçeneği içerir: **eş Indirmeleri sırasında, yalnızca aynı alt ağ içindeki eşleri kullanın**. Bu seçeneği etkinleştirirseniz, yönetim noktasındaki içerik konumu listesi yalnızca istemciyle aynı alt ağda ve sınır grubunda olan eş kaynakları içerir. Ağınızın yapılandırmasına bağlı olarak, artık belirli alt ağları eşleştirme için hariç bırakabilirsiniz. Örneğin, bir sınır eklemek, ancak belirli bir VPN alt ağını dışlamak istiyorsunuz.

Daha fazla bilgi için bkz. [sınır grubu seçenekleri](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

### <a name="proxy-support-for-microsoft-connected-cache"></a>Microsoft bağlı önbelleği için ara sunucu desteği

<!-- 5856396 -->

Ortamınız internet erişimi için kimliği doğrulanmamış bir ara sunucu kullanıyorsa, artık Microsoft bağlı önbelleği için bir Configuration Manager dağıtım noktası etkinleştirdiğinizde, proxy üzerinden iletişim kurabilir. Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği](../hierarchy/microsoft-connected-cache.md).

## <a name="client-management"></a><a name="bkmk_client"></a>İstemci yönetimi

### <a name="client-log-collection"></a>İstemci günlüğü koleksiyonu

<!-- 4226618 -->

Artık Configuration Manager konsolundan bir istemci bildirim eylemi göndererek istemci günlüklerini site sunucusuna yüklemek için bir istemci cihazı tetikleyebilirsiniz.

Daha fazla bilgi için bkz. [İstemci bildirimi](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="wake-up-a-device-from-the-central-administration-site"></a>Merkezi yönetim sitesinden bir cihazı uyandırma

<!-- 6030715 -->

Merkezi yönetim sitesinden (CAS), cihazlar veya cihaz koleksiyonları düğümünde, artık cihazları uyandırmak için istemci bildirim eylemini kullanabilirsiniz. Bu eylem daha önce yalnızca birincil sitede kullanılabilir.

Daha fazla bilgi için bkz. [LAN 'Da uyandırma yapılandırma](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810).

### <a name="improvements-to-support-for-arm64-devices"></a>ARM64 cihazlar için desteğe yönelik iyileştirmeler

<!--5954175-->

**Tüm Windows 10 (ARM64)** platformu, gereksinim kuralları veya uygulanabilirlik listeleri olan nesnelerde desteklenen işletim sistemi sürümleri listesinde bulunur.

> [!NOTE]
> En üst düzey **Windows 10** platformunu daha önce seçtiyseniz, bu eylem hem **tüm windows 10 (64-bit)** hem de **tüm Windows 10 (32-bit)**' i otomatik olarak seçti. Bu yeni platform otomatik olarak seçilmedi. **Tüm Windows 10 (ARM64)** eklemek istiyorsanız, listeden el ile seçin.

Configuration Manager ARM64 cihazları için destek hakkında daha fazla bilgi için bkz. [Windows 10, ARM64](../configs/support-for-windows-10.md#bkmk_arm64).

### <a name="track-configuration-item-remediations"></a>Yapılandırma öğesi değişikliklerini izle
<!--4261411-->
Artık yapılandırma öğesi uyumluluk kurallarınızın **desteklenmesinden sonra düzeltme geçmişini izleyebilirsiniz** . Bu seçenek etkinleştirildiğinde, yapılandırma öğesi için istemcide gerçekleşen tüm düzeltme bir durum iletisi oluşturur. Geçmiş Configuration Manager veritabanında depolanır.

Bu ayar hakkında daha fazla bilgi için bkz. [Configuration Manager istemcisiyle yönetilen Windows Masaüstü ve sunucu bilgisayarları için özel yapılandırma öğeleri oluşturma](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track).

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a>Uygulama yönetimi

### <a name="microsoft-edge-management-dashboard"></a>Microsoft Edge Yönetim Panosu

<!-- 3871913 -->

Microsoft Edge yönetimi panosu, Microsoft Edge ve diğer tarayıcıların kullanımı hakkında öngörüler sağlar. Bu panoda şunları yapabilirsiniz:

- Cihazlarınızdan kaç tane Microsoft Edge yüklü olduğunu görün
- Kaç istemcinin Microsoft Edge 'in farklı sürümlerine sahip olduğunu görün
- Cihazlarda yüklü tarayıcıların bir görünümüne sahip olmak
- Cihaza göre tercih edilen tarayıcı görünümüne sahip olmak

Panoyu görmek için, yazılım Kitaplığı çalışma alanında Microsoft Edge Yönetimi ' ne tıklayın. Araştır ' a tıklayıp başka bir koleksiyon seçerek Grafik verilerinin koleksiyonunu değiştirin. Varsayılan olarak, beş en büyük koleksiyonunuz açılan listede bulunur. Listede olmayan bir koleksiyon seçtiğinizde, yeni seçilen koleksiyon, aşağı açılan listenizde en alttaki noktayı alır.

Daha fazla bilgi için bkz. [Microsoft Edge yönetimi](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash).

### <a name="improvements-to-microsoft-edge-management"></a>Microsoft Edge Yönetimine yönelik iyileştirmeler

<!-- 4561024 -->

Artık otomatik güncelleştirmeleri devre dışı bırakmak yerine otomatik güncelleştirmeleri alacak şekilde ayarlanmış bir Microsoft Edge uygulaması oluşturabilirsiniz. Bu değişiklik, Microsoft Edge için güncelleştirmeleri Configuration Manager yönetmeyi veya Microsoft Edge 'in otomatik olarak güncelleştirmesine izin vermeyi seçmenizi sağlar. Uygulamayı oluştururken Microsoft Edge ayarları sayfasında, son kullanıcının cihazında istemcinin sürümünü otomatik olarak güncelleştirmesine Izin ver ' i seçin.

Daha fazla bilgi için bkz. [Microsoft Edge yönetimi](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate).

### <a name="task-sequence-as-an-app-model-deployment-type"></a>Uygulama modeli dağıtım türü olarak görev dizisi

<!-- 3555953 -->

Artık uygulama modeli aracılığıyla görev dizilerini kullanarak karmaşık uygulamaları yükleyebilirsiniz. Uygulamayı yüklemek ya da kaldırmak için, bir görev dizisi olan bir uygulamaya dağıtım türü ekleyin. Bu özellik aşağıdaki davranışları sağlar:

- Uygulama görev dizisini yazılım merkezi 'nde bir simgeyle görüntüleyin. Bir simge, kullanıcıların uygulama görev sırasını bulmasını ve belirlemesini kolaylaştırır.

- Yerelleştirilmiş bilgiler dahil olmak üzere uygulama görev sırası için ek meta veri tanımlayın

Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

## <a name="os-deployment"></a><a name="bkmk_osd"></a>İşletim sistemi dağıtımı

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>İstemci kaydından hemen sonra bir görev dizisini önyükleyebilirsiniz

<!-- 5526972 -->

Yeni bir Configuration Manager istemcisini yükleyip kaydettiğinizde ve ayrıca buna bir görev sırası dağıttığınızda, bu işlem, görev dizisini çalıştırmanın ne kadar süre sonra yapılacağını belirlemek zordur. Bu sürümde, bir istemcide, bir görev dizisini, siteye başarıyla kaydedildikten sonra başlatmak için kullanabileceğiniz yeni bir istemci kurulum özelliği tanıtılmıştır.

Daha fazla bilgi için bkz. [istemci yükleme özellikleri-PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts).

### <a name="improvements-to-check-readiness-task-sequence-step"></a>Hazırlık durumunu denetlemeye yönelik iyileştirmeler görev dizisi adımı

<!-- 6005561 -->

Artık **hazırlığı denetle** görev sırası adımında daha fazla cihaz özelliği doğrulayabilirsiniz. Hedef bilgisayarın önkoşul koşullarınızı karşıladığından emin olmak için bu adımı bir görev dizisinde kullanın.

- Geçerli işletim sisteminin mimarisi
- En düşük işletim sistemi sürümü
- En yüksek işletim sistemi sürümü
- En düşük istemci sürümü
- Geçerli işletim sisteminin dili
- AC güç takıldı
- Ağ bağdaştırıcısı bağlı ve kablosuz değil

Daha fazla bilgi için bkz. [görev dizisi adımları-kullanıma hazır olup olmadığını denetleyin](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness).

### <a name="improvements-to-task-sequence-progress"></a>Görev dizisi ilerleme durumu geliştirmeleri

<!-- 5932692 -->

Görev sırası ilerleme durumu penceresi artık aşağıdaki geliştirmeleri içerir:

- Geçerli adım numarasını, toplam adım sayısını ve tamamlanma yüzdesini gösterecek şekilde etkinleştirebilirsiniz
- Kuruluş adını tek bir satırda daha iyi göstermek için daha fazla alan sağlamak üzere pencerenin genişliği artırılmıştır

Daha fazla bilgi için bkz. [işletim sistemi dağıtımı Için kullanıcı deneyimleri](../../../osd/understand/user-experience.md#task-sequence-progress).

### <a name="improvements-to-os-deployment"></a>İşletim sistemi dağıtımına yönelik iyileştirmeler

Bu sürüm, işletim sistemi dağıtımına yönelik aşağıdaki geliştirmeleri içerir:

- Görev sırası ortamı, yeni bir salt okunurdur değişkeni içerir `_TSSecureBoot` .<!--5842295--> UEFı özellikli bir cihazda güvenli önyükleme durumunu öğrenmek için bu değişkeni kullanın. Daha fazla bilgi için bkz. [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot).

- **Komut satırı Çalıştır** ve **PowerShell betik adımlarını Çalıştır** için kullanıcı bağlamını yapılandırmak üzere görev dizisi değişkenlerini ayarlayın.<!-- 5573175 --> Daha fazla bilgi için bkz. [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) and [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser).

- **PowerShell betiğini Çalıştır** adımında, artık **Parameters** özelliğini bir değişken olarak ayarlayabilirsiniz.<!-- 5690481 --> Daha fazla bilgi için bkz. [PowerShell betiğini çalıştırma](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- Configuration Manager PXE Yanıtlayıcısı artık durum iletilerini site sunucusuna gönderiyor. Bu değişiklik, bu hizmeti kullanan işletim sistemi dağıtımlarının sorunlarını gidermeyi kolaylaştırır.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>Yazılım güncelleştirmeleri

### <a name="orchestration-groups"></a>Düzenleme grupları

<!-- 3098816 -->

Cihazlara yazılım güncelleştirmelerinin dağıtımını daha iyi denetlemek için bir Orchestration grubu oluşturun. Birçok sunucu yöneticisi, belirli iş yükleri için güncelleştirmeleri dikkatle Yönetmeli ve arasındaki davranışları otomatikleştiremelidir.

Bir Orchestration grubu, cihazları bir yüzdeye, belirli bir sayıya veya açık bir sıraya göre güncelleştirme esnekliği sağlar. Ayrıca, cihazlar güncelleştirme dağıtımını çalıştırmadan önce ve sonra bir PowerShell betiği de çalıştırabilirsiniz.

Bir Orchestration grubunun üyeleri yalnızca sunucular değil Configuration Manager istemci olabilir. Düzenleme grubu kuralları, bir düzenleme grubu üyesi içeren herhangi bir koleksiyondaki tüm yazılım güncelleştirme dağıtımları için cihazlara uygulanır. Diğer dağıtım davranışları hala geçerlidir. Örneğin, bakım pencereleri ve dağıtım zamanlamaları.

Daha fazla bilgi için bkz. [düzenleme grupları](../../../sum/deploy-use/orchestration-groups.md).

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>Bakım yığını güncelleştirmesinden sonra yazılım güncelleştirmelerini değerlendir

<!-- 4639943 -->

Configuration Manager artık bir bakım yığını güncelleştirmesinin (SSU) birden çok güncelleştirme için bir yüklemenin parçası olup olmadığını algılar. Bir SSU algılandığında, önce yüklenir. SSU 'yı yükledikten sonra, kalan güncelleştirmeleri yüklemek için bir yazılım güncelleştirme değerlendirme çevrimi çalışır. Bu değişiklik, bakım yığını güncelleştirmesinden sonra bağımlı bir toplu güncelleştirmenin yüklenmesine izin verir. Cihazın yüklemeler arasında yeniden başlatılması gerekmez ve ek bir bakım penceresi oluşturmanız gerekmez. SSUs öncelikle yalnızca Kullanıcı tarafından başlatılan yüklemeler için yüklenir. Örneğin, bir kullanıcı yazılım merkezinden birden çok güncelleştirme için bir yükleme başlatırsa, önce SSU yüklenmemiş olabilir.

Daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu).

### <a name="office-365-updates-for-disconnected-software-update-points"></a>Office 365 bağlantısı kesilen yazılım güncelleştirme noktaları için güncelleştirmeler

<!-- 4065163 -->

Office 365 güncelleştirmelerini Internet 'e bağlı bir WSUS sunucusundan bağlantısı kesilen Configuration Manager ortamına aktarmak için yeni bir araç kullanabilirsiniz. Daha önce, bağlantısı kesilen ortamlarda güncelleştirilmiş yazılım için meta verileri verdiğinizde ve içeri aktardığınızda, Office 365 güncelleştirmelerini dağıtamazsınız. Office 365 güncelleştirmeleri Office API 'sinden ve Office CDN 'den indirilen, bağlantısı kesilen ortamlar için mümkün olmayan ek meta veriler gerektirir.

Daha fazla bilgi için bkz. [Office 365 güncelleştirmelerini bağlantısı kesilen bir yazılım güncelleştirme noktasından Synchronize](../../../sum/get-started/synchronize-office-updates-disconnected.md).

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a>Korunmasına

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Microsoft Defender Gelişmiş tehdit koruması (ATP) ekleme 'yi Genişlet
 
<!-- 5229962 -->
Configuration Manager, cihazları Microsoft Defender ATP 'ye ekleme desteğini genişletti. Daha fazla bilgi için bkz. [Microsoft Defender Gelişmiş tehdit koruması](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a>Microsoft Endpoint Manager Yönetim Merkezi aracılığıyla Microsoft Defender ATP 'ye Configuration Manager istemcileri ekleme
<!--5691658-->
Artık, yönetilen istemcileri Configuration Manager için Microsoft Defender ATP uç noktası algılama ve yanıt (EDR) ekleme ilkelerini dağıtabilirsiniz. Bu istemciler Azure AD veya MDM kaydı gerektirmez ve ilke, Azure AD grupları yerine ConfigMgr koleksiyonlarına hedeflenmiş olur.

Bu özellik, müşterilerin hem Intune Configuration Manager MDM 'yi hem de istemci EDR/ATP ekleme 'yi tek bir yönetim deneyiminden yönetmesine olanak tanır-Microsoft Uç Nokta Yöneticisi Yönetim Merkezi. Daha fazla bilgi için bkz. [Intune 'da Endpoint Security Için Endpoint Detection ve yanıt ilkesi](../../../../intune/protect/endpoint-security-edr-policy.md).

> [!Important]
> Bu özellik için ortamınızda yüklü olan [KB4563473](https://support.microsoft.com/help/4563473)düzeltme toplaması gerekir.

### <a name="improvements-to-bitlocker-management"></a>BitLocker yönetimine yönelik iyileştirmeler

- BitLocker yönetim ilkesi artık sabit ve çıkarılabilir sürücülere yönelik ilkeler de dahil olmak üzere ek ayarlar içerir.<!-- 5925683 --> Daha fazla bilgi için bkz. [BitLocker ayarları başvurusu](../../../protect/tech-ref/bitlocker/settings.md).

- Configuration Manager geçerli dal sürümü 1910 ' de, BitLocker kurtarma hizmeti 'ni bütünleştirmek için, bir yönetim noktasını HTTPS olarak etkinleştirmeniz gerekir. HTTPS bağlantısı, ağ üzerindeki kurtarma anahtarlarını Configuration Manager istemcisinden yönetim noktasına şifrelemek için gereklidir. Yönetim noktasını yapılandırma ve HTTPS için tüm istemciler birçok müşteri için zor olabilir.

    Bu sürümden itibaren, HTTPS gereksinimi, tüm yönetim noktası rolünü değil kurtarma hizmetini barındıran IIS Web sitesi içindir. Bu değişiklik, sertifika gereksinimlerini andırmakta ve aktarım içindeki kurtarma anahtarlarını şifreler.<!-- 5925660 --> Daha fazla bilgi için bkz. [kurtarma verilerini şifreleme](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md).

## <a name="reporting"></a><a name="bkmk_report"></a>Rapor

### <a name="integrate-with-power-bi-report-server"></a>Power BI Rapor Sunucusu ile tümleştirme

<!-- 3721603 -->

Artık Power BI Rapor Sunucusu Configuration Manager raporlama ile tümleştirebilirsiniz. Bu tümleştirme size modern görselleştirme ve daha iyi performans sağlar. Bu, SQL Server Reporting Services zaten mevcut olana benzer Power BI raporlar için konsol desteği ekler.

Daha fazla bilgi için bkz. [Power BI rapor sunucusu tümleştirme](../../servers/manage/powerbi-report-server.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Configuration Manager konsolu

### <a name="show-boundary-groups-for-devices"></a>Cihazların sınır gruplarını gösterme

<!--6521835-->

Sınır gruplarıyla cihaz davranışlarına daha iyi sorun giderme konusunda yardımcı olmak için, artık belirli cihazların sınır gruplarını görüntüleyebilirsiniz. **Cihazlar** düğümünde veya bir **cihaz koleksiyonunun**üyelerini gösterdiğinizde, yeni **sınır grupları** sütununu liste görünümüne ekleyin.

Daha fazla bilgi için bkz. [sınır grupları](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary).

### <a name="send-a-smile-improvements"></a>Gülümseme iyileştirmeleri gönderin

<!-- 5891852 -->

Gülümseme gönderdiğinizde veya kaş çatma gönderdiğinizde, geri bildirim gönderildiğinde bir durum iletisi oluşturulur. Bu iyileştirme şunları bir kayıt sağlar:

- Geri bildirim gönderildiğinde
- Geri bildirimi gönderen kişi
- Geri bildirim KIMLIĞI
- Geri bildirim gönderimi başarılı olduysa veya

KIMLIĞI 53900 olan bir durum iletisi başarılı bir gönderim ve 53901 başarısız bir gönderim.

Daha fazla bilgi için bkz. [ürün geri bildirimi](../../understand/find-help.md#BKMK_1806Feedback).

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>Tüm alt klasörlerde yapılandırma öğeleri ve yapılandırma temelleri ara

<!--5891241-->

Önceki sürümlerde geliştirmelere benzer şekilde, artık **yapılandırma öğeleri** ve **yapılandırma temelleri** düğümlerinden **tüm alt klasörler** arama seçeneğini kullanabilirsiniz.

### <a name="community-hub"></a>Topluluk merkezi

<!--3555935, 3555936-->

_İlk tanıtılan Haziran 2020_

BT Yöneticisi topluluğu, yıllar boyunca çok fazla bilgi geliştirmiştir. Komut dosyaları ve raporlar gibi öğeleri sıfırdan yeniden oluşturmanız yerine, birbirleriyle paylaşabileceğiniz bir Configuration Manager **Community hub** 'ı oluşturduk. Başkalarının çalışmasını izleyerek iş saatlerini tasarrufu sağlayabilirsiniz. Topluluk hub 'ı, diğerlerinin çalışmasına ve diğer kişilerin kendi üzerinde derlenerek yaratıcıkilerin oluşturulmasını ister. GitHub zaten, paylaşım için tasarlanmış sektör genelinde işlemlere ve araçlara sahiptir. Artık topluluk hub 'ı, bu yeni topluluğu yönlendiren temel parçalar halinde doğrudan Configuration Manager konsolundaki bu araçlardan faydalanır.

Daha fazla bilgi için bkz. [Community hub ve GitHub](../../servers/manage/community-hub.md).

## <a name="tools"></a><a name="bkmk_tools"></a>Aracı

### <a name="onetrace-log-groups"></a>OneTrace günlük grupları

<!-- 5559993 -->

OneTrace artık destek merkezi 'ndeki özelliğe benzer şekilde özelleştirilebilir günlük gruplarını desteklemektedir. Günlük grupları, tek bir senaryo için tüm günlük dosyalarını açmanıza olanak tanır. OneTrace Şu anda aşağıdaki senaryolar için gruplar içermektedir:

- Uygulama yönetimi
- Uyumluluk ayarları (Istenen yapılandırma yönetimi olarak da adlandırılır)
- Yazılım güncelleştirmeleri

Daha fazla bilgi için bkz. [Destek Merkezi OneTrace](../../support/support-center-onetrace.md).

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a>Şirket içi sitede genişletme ve geçirme geliştirmeleri Microsoft Azure
<!--5665775, 6307931-->
Şirket içi Microsoft Azure siteyi genişletmeye ve geçirmeye yönelik araç artık tek bir Azure sanal makinesinde birden çok site sistemi rolü sağlamayı desteklemektedir. İlk Azure sanal makine dağıtımı tamamlandıktan sonra site sistemi rolleri ekleyebilirsiniz.

Daha fazla bilgi için bkz. [Şirket içi siteleri Microsoft Azure Için genişletme ve geçirme](../../support/azure-migration-tool.md#bkmk_add_role).

## <a name="other-updates"></a>Diğer güncelleştirmeler

Bu sürümden itibaren, aşağıdaki özellikler artık [ön sürüm](../../servers/manage/pre-release-features.md)değildir:

- [Kullanıcı grubu bulmayı Azure Active Directory](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Koleksiyon üyeliği sonuçlarını Azure Active Directory ile eşitler](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [Tek başına CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [Ortak yönetilen cihazlar Için istemci uygulamaları](../../../comanage/workloads.md#client-apps) (daha önce *ortak yönetilen cihazlar için mobil uygulamalar*olarak bilinir)<!-- 1357892/3600959 -->

Configuration Manager için Windows PowerShell cmdlet 'lerinde yapılan değişiklikler hakkında daha fazla bilgi için bkz. [PowerShell sürüm 2002 sürüm notları](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps).

Yönetim hizmeti REST API değişiklikler hakkında daha fazla bilgi için bkz. [Yönetim hizmeti sürüm notları](../../../develop/adminservice/release-notes.md#bkmk_2002).

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 2002](https://support.microsoft.com/help/4556203).

Aşağıdaki güncelleştirme paketi (4560496) konsolunda 15 Temmuz 2020 tarihinden itibaren kullanılabilir: [Microsoft uç noktası Configuration Manager sürüm 2002 Için güncelleştirme paketi](https://support.microsoft.com/help/4560496).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Sonraki adımlar

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

11 Mayıs 2020 itibariyle, sürüm 2002 tüm müşterilerin yüklemesi için genel kullanıma sunulmuştur.

Bu sürümü yüklemeye hazırsanız, [güncelleştirme 2002 ' i yüklemek için](../../servers/manage/checklist-for-installing-update-2002.md) [Configuration Manager güncelleştirmeleri](../../servers/manage/updates.md) ve denetim listesini yükleme bölümüne bakın.

> [!TIP]
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanın.
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:
>
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)

Bilinen önemli sorunlar için bkz. [sürüm notları](../../servers/deploy/install/release-notes.md).

Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist)de gözden geçirin.
