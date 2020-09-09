---
title: Sürüm 2006’daki yenilikler
titleSuffix: Configuration Manager
description: Geçerli dalın Configuration Manager sürüm 2006 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 09/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f46f3ee92854a6509d168134490e79a2d314b95f
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564236"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Geçerli dalın Configuration Manager sürüm 2006 ' deki yenilikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme 2006, konsol içi bir güncelleştirme olarak sunulmaktadır. Sürüm 1810 veya üstünü çalıştıran sitelerde bu güncelleştirmeyi uygulayın. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->Bu makalede Configuration Manager, sürüm 2006 ' deki değişiklikler ve yeni özellikler özetlenmektedir.

Bu güncelleştirmeyi yüklemek için her zaman en son denetim listesini gözden geçirin. Daha fazla bilgi için bkz. [güncelleştirme 2006 yükleme denetim listesi](../../servers/manage/checklist-for-installing-update-2006.md). Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist)de gözden geçirin.

Yeni Configuration Manager özelliklerinden tam olarak yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme de güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

> [!TIP]
> Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Microsoft Uç Nokta Yöneticisi kiracı iliştirme

### <a name="device-timeline-in-the-admin-center"></a><a name="bkmk_timeline"></a> Yönetim merkezinde cihaz zaman çizelgesi
<!--7220536, CM7141381-->
Configuration Manager, kiracı iliştirme aracılığıyla bir cihazı Microsoft Uç Nokta Yöneticisi ile eşitlediğinde, olayların bir zaman çizelgesini görebileceksiniz. Bu zaman çizelgesi, cihazdaki sorunları gidermenize yardımcı olabilecek geçmiş etkinlikleri gösterir. Daha fazla bilgi için bkz. [yönetim merkezindeki cihaz zaman çizelgesi](../../../tenant-attach/timeline.md).

### <a name="resource-explorer-in-the-admin-center"></a><a name="bkmk_hinv"></a> Yönetim merkezinde kaynak Gezgini
<!--6479284-->
Microsoft uç nokta Yönetimi yönetim merkezinden, kaynak Gezgini 'ni kullanarak karşıya yüklenen Configuration Manager cihazları için donanım envanterini görüntüleyebilirsiniz. Daha fazla bilgi için bkz. [Yönetim merkezinde kiracı iliştirme: kaynak Gezgini](../../../tenant-attach/resource-explorer.md).

### <a name="cmpivot-from-the-admin-center"></a><a name="bkmk_cmpivot"></a> Yönetim merkezinden CMPivot
<!--6024392-->
CMPivot 'in gücünü Microsoft Endpoint Manager yönetim merkezine taşıyın. Yardım masası gibi ek kişilerin buluttan, tek bir ConfigMgr tarafından yönetilen cihaza karşı gerçek zamanlı sorgular başlatabilmesini ve sonuçları yönetim merkezine geri döndürmesini sağlar. Bu, CMPivot 'in tüm geleneksel avantajlarından yararlanmanızı sağlar. Bu, BT yöneticilerinin ve diğer belirlenen kişilerin, ortamlarında cihazların durumunu hızlıca değerlendirebilme ve işlem yapması için sahip olduğu bir işlemdir.

Yönetim merkezinden CMPivot hakkında daha fazla bilgi için bkz. [CMPivot önkoşulları](../../../tenant-attach/cmpivot-start.md), [CMPivot genel bakış](../../../tenant-attach/cmpivot-overview-attached.md)ve [CMPivot örnek komut dosyaları](../../../tenant-attach/cmpivot-samples-attached.md).

### <a name="tenant-attach-microsoft-defender-antivirus-policies-in-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Kiracı iliştirme: Microsoft Endpoint Manager Yönetim merkezinde Microsoft Defender virüsten koruma ilkeleri
<!--4812909-->
Artık Microsoft Endpoint Manager konsolunda Microsoft Defender virüsten koruma ilkeleri oluşturabilir ve bunları Configuration Manager koleksiyonlara dağıtabilirsiniz. Ayrıntılı yönergeler ve kullanılabilir ayarlar dahil daha fazla bilgi için aşağıdaki makalelere bakın:
- [Kiracı iliştirme: Yönetim Merkezi 'nden Microsoft Defender ATP 'ye Configuration Manager istemcileri ekleme (Önizleme)](../../../tenant-attach/atp-onboard.md)
- [Kiracı iliştirme: yönetim merkezinden Endpoint Security virüsten koruma ilkesini dağıtma (Önizleme)](../../../tenant-attach/deploy-antivirus-policy.md)
- [Microsoft Intune 'deki kiracı ekli cihazlar Için Microsoft Defender virüsten koruma Ilkesi ayarları](../../../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).

### <a name="install-applications-from-the-admin-center"></a>Yönetim merkezinden uygulama yüklemesi
<!--7518897, 6024389-->
Microsoft Endpoint Manager yönetim merkezinden bir kiracıya bağlı cihaz için bir uygulama yüklemeyi gerçek zamanlı olarak başlatabilirsiniz. Configuration Manager sürüm 2006 ' den başlayarak, cihaz için kullanılabilen uygulamaların listesi, cihazın Şu anda oturum açmış olan kullanıcısına dağıtılan uygulamalar da içerir. Daha fazla bilgi için bkz. [kiracı iliştirme: yönetim merkezinden uygulama yüklemesi](../../../tenant-attach/applications.md).  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a>Kiracı ekleme ekleme sırasında önceden oluşturulmuş Azure AD uygulamasını içeri aktarma
<!--6479246-->
Yeni bir ekleme sırasında, yönetici Kiracı ekleme sırasında daha önce oluşturulmuş bir uygulama belirtebilir. Daha fazla bilgi için bkz. [Microsoft Endpoint Manager kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> Uç nokta Analizi

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>Varsayılan olarak etkinleştirilen Endpoint Analytics veri koleksiyonu
<!--7065447, 7741111-->
**Endpoint Analytics veri toplamayı etkinleştir** istemci ayarı artık varsayılan olarak etkinleştirilmiştir. Bu ayar, yönetilen uç noktalarınızın, Configuration Manager site sunucunuza başlangıç performans öngörüleri gibi verileri göndermesini sağlar. Bu değişiklik yalnızca yerel veri toplamayı etkiler. [Configuration Manager ' de karşıya veri yüklemeyi](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload)etkinleştirene kadar Endpoint Analytics verileri Microsoft Endpoint Manager yönetim merkezine yüklenemez. Varsayılan istemci ayarları ve sürüm 2006 ' e yükseltildikten sonra oluşturulan tüm özel istemci ayarları için yeni varsayılan değer geçerlidir.

- Sürüm 2002 ' den sürüm 2006 ' ye yükseltiyorsanız, mevcut özel istemci ayarları değerleri korunur. Configuration Manager sürüm 2002 ' deki **Endpoint Analytics veri toplamayı etkinleştir** için varsayılan değer **Hayır**' dır.
- Sürüm 1910 Configuration Manager 2006 ' e yükseltme yapıyorsanız, bu ayarların **Bilgisayar Aracısı** grubunu içeren önceden var olan özel istemci ayarları, **Endpoint Analytics veri toplamayı etkinleştir** **için yeni** varsayılan değerini devralır.

Daha fazla bilgi için bkz. [Configuration Manager Endpoint Analytics veri toplamayı yapılandırma](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site altyapısı

### <a name="vpn-boundary-type"></a>VPN sınır türü

<!--7020519-->

Uzak istemcileri yönetmeyi basitleştirmek için artık VPN 'Ler için yeni bir sınır türü oluşturabilirsiniz. Daha önce, IP adresini veya alt ağı temel alan VPN istemcileri için sınır oluşturmanız gerekiyordu. Bu yapılandırma, alt ağ yapılandırması veya VPN tasarımı nedeniyle zor veya mümkün olmayabilir.

Artık bir istemci bir konum isteği gönderdiğinde, ağ yapılandırması hakkında ek bilgiler içerir. Bu bilgilere bağlı olarak, sunucu istemcinin VPN üzerinde olup olmadığını belirler.

Daha fazla bilgi için bkz. [sınırları tanımlama](../../servers/deploy/configure/boundaries.md).

### <a name="management-insights-to-optimize-for-remote-workers"></a>Uzak çalışanları iyileştirmek için yönetim öngörüleri

<!--6982226-->

Bu sürüm, yeni bir yönetim öngörüleri grubu ekler ve **uzak çalışanlar Için iyileştirin**. Bu Öngörüler, uzak çalışanlar için daha iyi deneyimler oluşturmanıza ve altyapınızın yükünü azaltmanıza yardımcı olur. Bu sürümdeki Öngörüler birincil olarak VPN 'ye odaklanmaktadır:

- **VPN sınır gruplarını tanımlama**
- **Bulut tabanlı içerik kaynaklarını tercih etmek için VPN bağlantılı istemcileri yapılandırma**
- **VPN bağlantılı istemciler için eşler arası içerik paylaşımını devre dışı bırakma**

Daha fazla bilgi için bkz. [Management Insights](../../servers/manage/management-insights.md).

### <a name="improved-support-for-windows-virtual-desktop"></a>Windows sanal masaüstü için geliştirilmiş destek

<!--6527576-->

**Windows 10 Enterprise çoklu oturum** platformu, gereksinim kuralları veya uygulanabilirlik listeleri olan nesnelerde desteklenen işletim sistemi sürümleri listesinde bulunur.

Configuration Manager Windows sanal masaüstü desteği hakkında daha fazla bilgi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemi sürümleri](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>Intranet istemcileri bir CMG yazılım güncelleştirme noktası kullanabilir
<!--7102873-->
Intranet istemcileri artık bir sınır grubuna atandığında bir CMG yazılım güncelleştirme noktasına erişebilir. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Buluta bağlı yönetim

### <a name="use-the-company-portal-app-on-co-managed-devices"></a>Ortak yönetilen cihazlarda Şirket Portalı uygulamasını kullanma

<!--CMADO-3601237,INADO-4297660-->

Şirket Portalı artık Microsoft Endpoint Manager için platformlar arası uygulama portalı deneyimidir. Ortak yönetilen cihazları Şirket Portalı de kullanacak şekilde yapılandırarak tüm cihazlarda tutarlı bir kullanıcı deneyimi sağlayabilirsiniz.

Daha fazla bilgi için bkz. [ortak yönetilen cihazlarda şirket portalı uygulamasını kullanma](../../../comanage/company-portal.md).

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>Ortak yönetim için Microsoft Azure Çin 21Vianet kullanın
<!--7133238-->
Ortak yönetimi etkinleştirirken artık Azure ortamınız olarak Azure Çin bulutu 'nı seçebilirsiniz. Daha fazla bilgi için bkz. [ortak yönetimi etkinleştirme](../../../comanage/how-to-enable.md).

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Azure AD uygulama gizli anahtarı süre sonu bildirimi

<!--6386392-->

Sitenizi buluta eklemek için Azure hizmetleri 'ni yapılandırırsanız, Configuration Manager konsolu artık aşağıdaki koşullara ilişkin bildirimleri görüntüler:

- Bir veya daha fazla Azure AD uygulama gizli anahtarı yakında dolacak
- Bir veya daha fazla Azure AD uygulama gizli anahtarının geçerliliği bitti

Daha fazla bilgi için bkz. [gizli anahtarı yenileme](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="desktop-analytics"></a>Desktop Analytics

Masaüstü Analizi bulut hizmetindeki aylık değişiklikler hakkında daha fazla bilgi için bkz. [Masaüstü](../../../desktop-analytics/whats-new.md)analizine ilişkin yenilikler.

#### <a name="change-to-diagnostic-data-labels"></a>Tanılama veri etiketlerine Dönüştür

<!-- 7363467 -->

Windows Tanılama verilerine yönelik masaüstü Analizi gereksinimleriyle daha iyi uyum sağlamak için, bu ayarlar yeni etiketlere sahiptir:

| Sürüm 2006 ve üzeri | Sürüm 2002 ve öncesi |
|---------|---------|
| Gerekli | Temel |
| İsteğe bağlı (sınırlı) | Gelişmiş (sınırlı) |
| Yok | Gelişmiş |
| İsteğe Bağlı | Tam |

Daha önce **Gelişmiş** düzeyde herhangi bir cihaz yapılandırdıysanız, sürüm 2006 ' e yükselttiğinizde bu kullanıcılar **isteğe bağlı (sınırlı)** olarak döndürülür. Böylece daha az veri Microsoft 'a gönderilir. Bu değişiklik, masaüstü analizinden gördüklerinizi etkilemez.

Daha fazla bilgi için bkz. [Masaüstü analizi için veri paylaşımını etkinleştirme](../../../desktop-analytics/enable-data-sharing.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Gerçek zamanlı yönetim

### <a name="improvements-to-cmpivot"></a>CMPivot geliştirmeleri
<!--6518631-->
CMPivot ' de aşağıdaki iyileştirmeler yapılmıştır:

- Konsolundan CMPivot ve CMPivot tek başına yakınsama
- Bir koleksiyon seçmek veya oluşturmak zorunda kalmadan tek bir cihazdan veya birden fazla cihazdan CMPivot çalıştırma
- CMPivot sorgu sonuçlarından, tek bir cihaz veya birden çok cihaz seçebilir ve sonra seçiminizle ilgili olarak ayrı bir CMPivot örneği başlatabilirsiniz.

Daha fazla bilgi için bkz. [sürüm 2006 ' den başlayarak CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_2006).

## <a name="client-management"></a><a name="bkmk_client"></a> İstemci yönetimi

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a>Tarifeli bir bağlantıda istemciyi yükleyip yükseltin

<!--6976145-->

Daha önce, cihaz tarifeli bir ağa bağlıysa yeni istemciler yüklenmez. Mevcut istemciler yalnızca tüm istemci iletişimine izin verildiyse yükseltilir. Tarifeli bir ağ üzerinde sık sık dolaşım olan cihazlar için yönetilmeyen veya daha eski bir istemci sürümü üzerinde. Bu sürümden itibaren, **Tarifeli İnternet bağlantılarında istemci Iletişimini** **Izin ver** veya **sınırla**olarak ayarlarken istemciyi yükleyebilir ve yükseltebilirsiniz. Bu ayarla, istemcinin geçerli kalmasına izin verebilir, ancak tarifeli bir ağda istemci iletişimini yine de yönetebilir.

Yeni bir istemci yüklemesinin davranışını tanımlamak için **/Allowtarifeli**adlı yeni bir CCMSetup parametresi vardır. CCMSetup için tarifeli bir ağda istemci iletişimine izin gönderdiğinizde, içerik indirilir, siteye kaydolur ve ilk ilkeyi indirir. Diğer istemci iletişimleri, bu ilkeden istemci ayarının yapılandırmasını izler.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [İstemci ayarları hakkında](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [İstemci yükleme parametreleri ve özellikleri hakkında](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>Cihaz yeniden başlatmalarının yönetilmesi iyileştirmeleri

<!--3601213-->

Configuration Manager, cihaz yeniden başlatmaları yönetmek ve bildirimleri yeniden başlatmak için birçok seçenek sunar. Artık, bir dağıtım gerektirdiğinde cihazların otomatik olarak yeniden başlatılmasını engellemek için bir istemci ayarı yapılandırabilirsiniz. Bu ayar, benzersiz durumlarda daha fazla denetim sağlar. Varsayılan olarak, Configuration Manager istemci ayarı **bir cihazı yeniden başlamaya zorlayabilir** , böylece Configuration Manager cihazları yeniden başlamaya zorlayabilir. Bu ayar yalnızca bir yeniden başlatma gerektiren uygulama, yazılım güncelleştirmesi ve paket dağıtımları için geçerlidir.

Daha fazla bilgi için bkz. [cihaz yeniden başlatma bildirimleri](../../clients/deploy/device-restart-notifications.md).

## <a name="application-management"></a><a name="bkmk_app"></a> Uygulama yönetimi

### <a name="improvements-to-available-apps-via-cmg"></a>CMG aracılığıyla kullanılabilir uygulamalarda iyileştirmeler

<!--6935376-->
Bu sürüm, yazılım merkezi ve Azure Active Directory (Azure AD) kimlik doğrulamasıyla ilgili bir sorunu düzeltir. İntranette olduğu gibi algılanan ve bulut yönetimi ağ geçidi (CMG) üzerinden iletişim kuran bir istemci için, daha önce Yazılım Merkezi Windows kimlik doğrulamasını kullanır. Kullanıcı tarafından kullanılabilir uygulamaların listesini almayı denediğinde başarısız olur. Artık Azure AD 'ye katılmış cihazlar için Azure Active Directory (Azure AD) kimliğini kullanır. Bu cihazlar, buluta katılmış veya karma olarak birleştirilmiş olabilir.

Daha fazla bilgi için bkz. [Kullanıcı tarafından kullanılabilen uygulamaları dağıtma](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).

### <a name="microsoft-365-apps-for-enterprise"></a>Enterprise için Microsoft 365 uygulamalar
<!--6298093-->
Office 365 ProPlus, 21 Nisan 2020 tarihinde Kurumsal Microsoft 365 uygulamalar olarak yeniden adlandırıldı. Sürüm 2006 ' den başlayarak, aşağıdaki değişiklikler yapılmıştır:

- Configuration Manager konsolu yeni adı kullanacak şekilde güncelleştirilmiştir.
  - Bu değişiklik ayrıca Microsoft 365 uygulamalar için güncelleştirme kanalı adlarını da içerir.
- Bir veya daha fazla otomatik dağıtım kuralı, Microsoft 365 Apps güncelleştirmeleri için **başlık** ölçütlerinde Kullanımdan kaldırılmış kanal adlarına başvurulacağını bildirmek üzere konsola bir başlık bildirimi eklendi.

Daha fazla bilgi için bkz. [Microsoft 365 Apps kanal adları](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) ve [Microsoft 365 uygulamalar hazır olma panosu](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> İşletim sistemi dağıtımı

### <a name="task-sequence-media-support-for-cloud-based-content"></a>Bulut tabanlı içerik için görev dizisi medya desteği

<!--6209223-->

Görev sırası medyası artık bulut tabanlı içeriği indirebilir. Örneğin, cihazlarını yeniden görüntüetmek için uzak ofisteki bir kullanıcıya USB anahtarı gönderirsiniz. Ya da yerel bir PXE sunucusuna sahip olan bir Office, ancak cihazların bulut hizmetlerini mümkün olduğunca önceliklendirmesine olanak tanır. Önyükleme medyası ve PXE dağıtımları büyük işletim sistemi dağıtım içeriğini indirmek için WAN kullanımı yerine artık bulut tabanlı kaynaklardan içerik alabilir. Örneğin, içerik paylaşmak için etkinleştirdiğiniz bir bulut yönetimi ağ geçidi (CMG).

> [!NOTE]
> Cihazın hala yönetim noktasına bir intranet bağlantısı olması gerekir.

Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak için önyüklenebilir medya kullanma](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

### <a name="improvements-to-task-sequences-via-cmg"></a>CMG aracılığıyla görev dizileriyle geliştirmeler

Bu sürüm, bir bulut yönetimi ağ geçidi (CMG) aracılığıyla iletişim kuran cihazlara görev dizilerini dağıtmak için aşağıdaki geliştirmeleri içerir:

- İşletim sistemi dağıtımı desteği<!--6997525-->: Bir işletim sistemini dağıtmak için önyükleme görüntüsü kullanan bir görev dizisi ile, bunu CMG aracılığıyla iletişim kuran bir cihaza dağıtabilirsiniz. Kullanıcının görev dizisini yazılım merkezinden başlatması gerekir. Daha fazla bilgi için bkz. [plan for CMG-belirtimleri](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications).

- Bu sürüm, geçerli Configuration Manager dalı sürüm 2002 ' den [bilinen iki sorunu](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg) düzeltir.<!-- 6983320 --> Artık aşağıdaki koşullarda CMG aracılığıyla iletişim kuran bir cihazda görev dizisi çalıştırabilirsiniz:

  - [Toplu kayıt belirteciyle](../../clients/deploy/deploy-clients-cmg-token.md) kaydettiğinizde bir çalışma grubu cihazı

  - Siteyi [GELIŞMIŞ http](../hierarchy/enhanced-http.md) için yapılandırırsınız ve YÖNETIM noktası http 'dir

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>BitLocker için geliştirmeler görev dizisi adımları

<!--6995601-->

Artık **BitLocker 'ı etkinleştir** ve **BitLocker 'ı önceden sağla** görev dizisi adımlarında disk şifreleme modunu belirtebilirsiniz. Varsayılan olarak, adımlar işletim sistemi sürümü için varsayılan şifreleme yöntemini kullanmaya devam eder.

**BitLocker 'ı etkinleştir** adımı ayrıca, **TPM olmayan BILGISAYARLAR için veya TPM etkinleştirilmediğinde bu adımı atlama**ayarını da içerir. Bu ayarı etkinleştirdiğinizde adım, bir TPM veya başlatılmamış TPM olmadan bir cihazdaki hatayı günlüğe kaydeder ve görev dizisi devam eder. Bu ayar, BitLocker 'ı tam olarak desteklemeyen cihazlarda görev sırası davranışını yönetmeyi kolaylaştırır.

Daha fazla bilgi için bkz. [görev dizisi adımları](../../../osd/understand/task-sequence-steps.md).

### <a name="management-insight-rules-for-os-deployment"></a>İşletim sistemi dağıtımı için yönetim öngörüleri kuralları

<!--6982275-->

Görev dizisi ilkesinin boyutu 32 MB 'yi aşarsa, istemci büyük ilkeyi işleyemez. İstemci daha sonra görev dizisi dağıtımını çalıştıramazsa. Bu sürüm, Görev sıralarının ilke boyutunu yönetmenize yardımcı olmak için aşağıdaki yönetim öngörülerini içerir:

- **Büyük görev dizileri maksimum ilke boyutunu aşarak katkıda bulunabilir**

- **Görev dizileri için toplam ilke boyutu ilke sınırını aşıyor**

> [!TIP]
> Bu kurallar, **Işletim sistemi dağıtımı**için yeni bir gruptur. **Kullanılmayan önyükleme görüntülerinin** mevcut kuralı artık bu grupta de vardır.

Daha fazla bilgi için bkz. [Yönetim öngörüleri](../../servers/manage/management-insights.md#operating-system-deployment).

### <a name="improvements-to-os-deployment"></a>İşletim sistemi dağıtımına yönelik iyileştirmeler

Bu sürüm, işletim sistemi dağıtımına yönelik aşağıdaki ek geliştirmeleri içerir:

- [Biçim ve Bölüm diski](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) adımının hedefini belirtmek için bir görev dizisi değişkeni kullanın. Bu yeni değişken seçeneği, dinamik davranışlarla daha karmaşık görev dizilerini destekler. Örneğin, özel bir betik diski algılayabilir ve değişkeni donanım türüne göre ayarlayabilir. Daha sonra farklı donanım türlerini ve bölümlerini yapılandırmak için bu adımın birden fazla örneğini kullanabilirsiniz.<!--6610288-->

- [Hazırlık kontrolü](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) adımı artık cihazın UEFI kullanıp kullanmadığını belirlemede bir denetim içerir. Ayrıca, yeni bir salt okunurdur **_TS_CRUEFI**bir görev dizisi değişkeni de içerir.<!--6452769-->

- Daha ayrıntılı ilerleme bilgileri göstermek için [görev sırası ilerleme penceresi](../../../osd/understand/user-experience.md#task-sequence-progress) ' ni etkinleştirirseniz, artık devre dışı bırakılmış bir gruptaki etkin adımları saymaz. Bu değişiklik, ilerlemenin daha hassas olmasına yardımcı olur.<!--6448412-->

- Daha önce, bir cihazı Windows 10 ' a yükseltmek için bir görev dizisi sırasında, son Windows yapılandırma aşamalarının biri sırasında açılan bir komut istemi penceresi. Pencere, Windows ilk çalıştırma deneyimi 'nin (OOBE) en üstünde yer aldığı ve kullanıcılar yükseltme işlemini kesintiye uğratan etkileşime girebilen. Şimdi SetupCompleteTemplate. cmd ve SetupRollbackTemplate. cmd betikleri Configuration Manager, bu komut istemi penceresini gizlemek için bir değişiklik içerir.<!--2837795-->

- Bazı müşteriler **ıprogressuı:: ShowMessage** metodunu kullanarak özel görev sırası arabirimleri oluşturur, ancak kullanıcının yanıtı için bir değer döndürmez. Bu sürüm, [ıprogressuı:: ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md) metodunu ekler. Bu yeni yöntem, var olan yönteme benzerdir, ancak aynı zamanda yeni bir tamsayı sonuç değişkeni olan **pResult**içerir.<!--6448458-->

## <a name="protection"></a>Koruma

### <a name="cmg-support-for-endpoint-protection-policies"></a>Endpoint Protection ilkeleri için CMG desteği

<!--4773948-->

Bulut yönetimi ağ geçidi (CMG), uç nokta koruma ilkelerini destekliyordu, ancak cihazların şirket içi etki alanı denetleyicilerine erişimi olması gerekir. Bu sürümden itibaren, bir CMG aracılığıyla iletişim kuran istemciler, Active Directory için etkin bir bağlantı olmadan Endpoint Protection ilkelerini hemen uygulayabilir.

Daha fazla bilgi için bkz. [Configuration Manager özellikleri Için CMG desteği](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features).

### <a name="bitlocker-management-support-for-hierarchies"></a>Hiyerarşiler için BitLocker yönetim desteği

<!-- 5925693 -->

Artık, merkezi yönetim sitesinde BitLocker Self-Service Portal ve yönetim ve izleme Web sitesini yükleyebilirsiniz.

Daha fazla bilgi için bkz. [BitLocker portallarını ayarlama](../../../protect/deploy-use/bitlocker/setup-websites.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager konsolu

### <a name="community-hub-and-github"></a>Topluluk hub 'ı ve GitHub
<!--3555935, 3555936, deep link included 4224406-->

*(İlk 2020 Haziran 'da tanıtılan)*

BT Yöneticisi topluluğu, yıllar boyunca çok fazla bilgi geliştirmiştir. Komut dosyaları ve raporlar gibi öğeleri sıfırdan yeniden oluşturmanız yerine, birbirleriyle paylaşabileceğiniz bir Configuration Manager **Community hub** 'ı oluşturduk. Başkalarının çalışmasını izleyerek iş saatlerini tasarrufu sağlayabilirsiniz. Topluluk hub 'ı, diğerlerinin çalışmasına ve diğer kişilerin kendi üzerinde derlenerek yaratıcıkilerin oluşturulmasını ister. GitHub zaten, paylaşım için tasarlanmış sektör genelinde işlemlere ve araçlara sahiptir. Artık topluluk hub 'ı, bu yeni topluluğu yönlendiren temel parçalar halinde doğrudan Configuration Manager konsolundaki bu araçlardan faydalanır. İlk sürüm için, topluluk hub 'ında kullanılabilir hale getirilen içerik yalnızca Microsoft tarafından karşıya yüklenir. 

Daha fazla bilgi için bkz. [Community hub ve GitHub](../../servers/manage/community-hub.md).

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Topluluk hub 'ı öğelerine doğrudan bağlantılar
<!--4224406-->
Doğrudan bağlantı ile Configuration Manager konsolu topluluk hub düğümündeki öğelere kolayca gidebilirsiniz ve başvurabilirsiniz. Daha fazla bilgi için bkz. [topluluk hub öğelerine doğrudan bağlantılar](../../servers/manage/community-hub.md#bkmk_deeplink).

### <a name="notifications-from-microsoft"></a>Microsoft 'un bildirimleri
<!--3953121-->
Artık Configuration Manager konsolunda Microsoft 'tan bildirim almayı tercih edebilirsiniz. Bu bildirimler yeni veya güncelleştirilmiş özellikler, Configuration Manager ve ekli hizmetlerde yapılan değişiklikler ve Düzeltme eylemi gerektiren sorunlar hakkında bilgi almanıza yardımcı olur.

Daha fazla bilgi için bkz. [Microsoft 'tan ileti almak için bir site yapılandırma](../../servers/manage/admin-console-notifications.md#bkmk_msft).

### <a name="power-bi-sample-reports"></a>Power BI örnek raporlar
<!--5679791-->

*(İlk 2020 Haziran 'da tanıtılan)*

Power BI Rapor Sunucusu Configuration Manager raporlama ile tümleştirdiğinizde, artık kullanılabilir örnek Power BI raporları vardır. Aşağıdaki örnek raporları indirip yükleyin:

- Yazılım Güncelleştirme Uyumluluğu durumu
- Yazılım güncelleştirmesi dağıtım durumu

Daha fazla bilgi için bkz. [ınstall Power BI Sample Reports](../../servers/manage/powerbi-sample-reports.md).

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> Kullanım dışı işletim sistemleri

[Kaldırılan ve kullanımdan kaldırılan öğelerde](deprecated/removed-and-deprecated.md)uygulanmadan önce yapılan değişiklikler hakkında bilgi edinin.

Sürüm 1906 ' de ilk duyurulduğu gibi, sürüm 2006 aşağıdaki istemci işletim sistemi sürümleri için desteği bırakır:  

- Windows CE 7,0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise

## <a name="other-updates"></a>Diğer güncelleştirmeler

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

Configuration Manager için Windows PowerShell cmdlet 'lerinde yapılan değişiklikler hakkında daha fazla bilgi için bkz. [PowerShell sürüm 2006 sürüm notları](/powershell/sccm/2006-release-notes?view=sccm-ps).

Yönetim hizmeti REST API değişiklikler hakkında daha fazla bilgi için bkz. [Yönetim hizmeti sürüm notları](../../../develop/adminservice/release-notes.md#bkmk_2006).

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 2006](https://support.microsoft.com/help/4578830).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

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

<!-- At this time, version 2006 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring). -->

31 Ağustos 2020 itibariyle, sürüm 2006 tüm müşterilerin yüklemesi için genel kullanıma sunulmuştur.

Bu sürümü yüklemeye hazırsanız, [güncelleştirme 2006 ' i yüklemek için](../../servers/manage/checklist-for-installing-update-2006.md) [Configuration Manager güncelleştirmeleri](../../servers/manage/updates.md) ve denetim listesini yükleme bölümüne bakın.

> [!TIP]
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanın.
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:
>
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)

Bilinen önemli sorunlar için bkz. [sürüm notları](../../servers/deploy/install/release-notes.md).

Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist)de gözden geçirin.
