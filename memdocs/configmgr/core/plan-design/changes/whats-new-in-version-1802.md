---
title: Yeni sürüm 1802
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1802 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 11066470347db0f3ffbfadda9897aed92baa645b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073611"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Configuration Manager sürüm 1802 ' deki yenilikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme 1802, konsol içi bir güncelleştirme olarak sunulmaktadır. 1702, 1706 veya 1710 sürümünü çalıştıran sitelerde bu güncelleştirmeyi uygulayın. <!-- baseline only statement: -->Yeni bir site yüklerken, taban çizgisi sürümü olarak da kullanılabilir.

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 1802](https://support.microsoft.com/help/4101375).

Bu sürüm için aşağıdaki ek güncelleştirmeler de kullanılabilir:
- [Geçerli Configuration Manager dalı için güncelleştirme paketi, sürüm 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanmanız gerekir.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:    
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Sitelere güncelleştirme yükleme](../../servers/manage/updates.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)

Aşağıdaki bölümlerde, Configuration Manager sürüm 1802 ' deki değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi sağlanmaktadır.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Site altyapısı

### <a name="reassign-distribution-point"></a>Dağıtım noktasını yeniden ata
<!-- 1306937 -->
Birçok müşterinin büyük Configuration Manager altyapıları vardır ve bunların ortamlarını basitleştirmek için birincil veya ikincil siteleri azaltmaktadır. Ayrıca, yönetilen istemcilere içerik sağlamak için şube konumlarında dağıtım noktalarını korumaları gerekir. Bu dağıtım noktaları genellikle birden çok terabayt veya daha fazla içerik içerir. Bu içerik, bu uzak sunuculara dağıtılacak zaman ve ağ bant genişliği açısından maliyetlidir. Bu özellik, içeriği yeniden dağıtmadan bir dağıtım noktasını başka bir birincil siteye yeniden atamanıza olanak tanır. Bu eylem, sunucudaki tüm içeriği kalıcı hale yaparken site sistem atamasını güncelleştirir. Daha fazla bilgi için bkz. [bir dağıtım noktasını yeniden atama](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Windows Dağıtım Iyileştirmesini Configuration Manager sınır grupları kullanacak şekilde yapılandırma
<!-- 1324696 -->
Şirket ağınızda ve Uzak ofislerde içerik dağıtımını tanımlamak ve düzenlemek için Configuration Manager sınır gruplarını kullanırsınız. [Windows teslim iyileştirme](/windows/deployment/update/waas-delivery-optimization) , Windows 10 cihazları arasında içerik paylaşmak için bulut tabanlı ve eşler arası bir teknolojidir. Bu sürümden başlayarak, eşler arasında içerik paylaşırken sınır gruplarınızı kullanmak için teslim Iyileştirmesini yapılandırın. Yeni bir istemci ayarı, sınır grubu tanımlayıcısını istemcideki teslim Iyileştirme grubu tanımlayıcısı olarak uygular. İstemci, teslim Iyileştirme bulut hizmeti ile iletişim kurduğunda, istenen içeriğe sahip eşleri bulmak için bu tanımlayıcıyı kullanır. Daha fazla bilgi için bkz. [içerik yönetimi Için temel kavramlar](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="support-for-windows-10-arm64-devices"></a>Windows 10 ARM64 cihazları için destek
<!-- 1353704 -->
Bu sürümden itibaren Configuration Manager istemcisi Windows 10 ARM64 cihazlarında desteklenir. Mevcut istemci yönetimi özellikleri bu yeni cihazlarla çalışmalıdır. Örneğin, donanım ve yazılım envanteri, yazılım güncelleştirmeleri ve uygulama yönetimi. İşletim sistemi dağıtımı şu anda desteklenmiyor. 

### <a name="improved-support-for-cng-certificates"></a>CNG sertifikaları için geliştirilmiş destek
<!-- 1357314 -->
Configuration Manager (geçerli dal) sürüm 1710, [şifreleme: yeni nesil (CNG) sertifikaları](../network/cng-certificates-overview.md)destekler. Sürüm 1710, çeşitli senaryolarda istemci sertifikalarına yönelik desteği kısıtlar. 

Bu sürümden itibaren, aşağıdaki HTTPS etkin sunucu rolleri için CNG sertifikalarını kullanın:
- Yönetim noktası
- Dağıtım noktası
- Yazılım güncelleştirme noktası
- Durum Geçiş noktası  


### <a name="boundary-group-fallback-for-management-points"></a>Yönetim noktaları için sınır grubu geri dönüşü
<!-- 1324594 -->
[Sınır grupları](../../servers/deploy/configure/boundary-groups.md)arasındaki yönetim noktaları için geri dönüş ilişkilerini yapılandırın. Bu davranış, istemcilerin kullandığı yönetim noktaları için daha fazla denetim sağlar. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../../servers/deploy/configure/boundary-groups.md#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Bulut dağıtım noktası site benzeşimi
<!--503719-->
Bu özellik, müşterilerin bulut dağıtım noktalarını kullanarak çok siteli, coğrafi olarak dağınık bir hiyerarşiye faydalanır. Internet tabanlı bir istemci içeriği aradığında, daha önce istemci tarafından alınan bulut dağıtım noktaları listesine hiçbir sıralama yapılmaz. Bu davranış, Internet tabanlı istemcilerin coğrafi olarak uzak bulut dağıtım noktalarından içerik almasına yol açabilir. Bu tür bir uzak sunucudan içerik indirilmesi genellikle daha yakın bir sunucudan daha yavaştır.
 
Bulut dağıtım noktası site benzeşimi ile, Internet tabanlı bir istemci sıralı bir liste alır. Bu liste, bulut dağıtım noktalarını istemcinin atanan sitesinden önceliklendirir. Bu davranış, yöneticinin site kaynaklarından içerik indirmeleri için tasarım amacını korumalarına olanak sağlar.
 

## <a name="management-insights"></a>Yönetim içgörüleri
<!-- 1353967 -->
Configuration Manager yönetim öngörüleri ortamınızın geçerli durumu hakkında bilgi sağlar. Bilgiler, site veritabanındaki verilerin analizini temel alır. Öngörüler, ortamınızı daha iyi anlamanıza ve öngörülere göre işlem yapmanıza yardımcı olur. Ayrıntılar için bkz. [Yönetim öngörüleri](../../servers/manage/management-insights.md)

Configuration Manager 1802 ' de aşağıdaki Öngörüler mevcuttur:
- Uygulamalar:
    - Dağıtımlar olmadan uygulamalar
- Cloud Services: <!--1356412-->
    - Ortak yönetim hazırlığını değerlendirme 
    - Cihazlarınızın karma Azure Active Directory katılmış olmasını sağlama
    - Kimlik ve erişim altyapınızı modernleştirin
    -  İstemcilerinizi Windows 10, sürüm 1709 veya üzeri sürümlere yükseltin 
- Koleksiyonlarıyla
    - Boş Koleksiyonlar
- Basitleştirilmiş Yönetim:  <!--1355148-->
    - Güncel olmayan istemci sürümleri  
- Software Center: 
    - Kullanıcıları Uygulama Kataloğu yerine yazılım merkezine doğrudan yönlendirin  
    - Yazılım Merkezi 'nin yeni sürümünü kullan 
- Windows 10: <!--1357421-->
    - Windows telemetri ve ticari KIMLIK anahtarını yapılandırma 
    - Configuration Manager Yükseltme Hazırlığı bağlama 
   
<!-- ## Migration  -->



## <a name="client-management"></a>İstemci yönetimi

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Azure Resource Manager için bulut yönetimi ağ geçidi desteği
<!-- 1324735 -->
[Bulut yönetimi ağ geçidinin](../../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) bir örneğini oluştururken, sihirbaz artık **Azure Resource Manager dağıtımı**oluşturma seçeneği sağlar. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) , tüm çözüm kaynaklarının, [kaynak grubu](/azure/azure-resource-manager/resource-group-overview#resource-groups)olarak adlandırılan tek bir varlık olarak yönetilmesine yönelik modern bir platformdur. Azure Resource Manager ile CMG 'yi dağıttığınızda, site kimlik doğrulaması yapmak ve gerekli bulut kaynaklarını oluşturmak için Azure Active Directory (Azure AD) kullanır. Bu modernlanmış dağıtım, klasik Azure Yönetim sertifikası gerektirmez. Daha fazla bilgi için bkz. [CMG topoloji tasarımı](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

> [!IMPORTANT]
> Bu özellik, Azure bulut hizmeti sağlayıcıları (CSP) için desteği etkinleştirmez. Azure Resource Manager ile CMG dağıtımı, CSP 'nin desteklemediği klasik bulut hizmetini kullanmaya devam eder. Daha fazla bilgi için bkz. [Azure CSP 'de kullanılabilir Azure hizmetleri](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi geliştirmeleri  

- Bu sürümden itibaren, **bulut yönetimi ağ geçidi** artık yayın öncesi bir özellik değildir.  

- Özellik belgeleri düzeltilir ve geliştirilmiştir. Daha fazla bilgi için aşağıdaki makalelere bakın:
    - [Bulut yönetimi ağ geçidini planlayın](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [Bulut yönetimi ağ geçidi boyutu ve ölçek numaraları](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [Bulut yönetimi ağ geçidi için güvenlik ve gizlilik](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [Bulut yönetimi ağ geçidi hakkında sık sorulan sorular](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [Bulut yönetimi ağ geçidine yönelik sertifikalar](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [Bulut yönetimi ağ geçidini kurma](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Donanım envanterini 255 karakterden daha büyük dizeler toplayacak şekilde yapılandırma
<!-- 1357389 -->
Dizelerin uzunluğunu donanım envanteri özellikleri için 255 karakterden daha fazla olacak şekilde yapılandırabilirsiniz. Bu değişiklik yalnızca yeni eklenen sınıflar ve anahtarlar olmayan donanım envanteri özellikleri için geçerlidir. Ayrıntılar için bkz. [donanım envanterini genişletme](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255) makalesi. 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Linux ve UNIX istemci desteği için kullanımdan kaldırma duyurusu
 <!--510139-->
Microsoft, Linux ve UNIX istemci desteğini bundan böyle Configuration Manager kabaca bir yılda kullanımdan kaldırmayı amaçlıklaştırır. bu nedenle, istemcilerin erken takvim 2019 ' de sürüm 1902 ' e eklenmeyecektir. Configuration Manager 1810 sürümü, geç takvim 2018 ' de, Linux ve UNIX istemcilerini kapsayan son sürüm olacak ve Configuration Manager 1810 tam yaşam döngüsü için desteklenecektir. Configuration Manager 1810 sonrasında, müşteriler Linux sunucularının yönetilmesi için Microsoft Azure yönetimini düşünmelidir. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

### <a name="surface-device-dashboard"></a>Surface cihazı panosu
<!--1355788-->
Surface cihaz panosu, ortamınızda bulunan yüzey cihazları hakkında bilgi sağlar. Konsolunda, **izleme** > **yüzeyi cihazları**' na gidin. Öğeleri görüntüleyebilirsiniz:
- Yüzey yüzdesi
- Yüzey modellerinin yüzdesi
- En popüler beş bellenim sürümü

Ayrıntılar için bkz. [yüzey panosu](../../clients/manage/surface-device-dashboard.md) makalesi.

### <a name="change-in-the-configuration-manager-client-install"></a>Configuration Manager istemci yüklemede değişiklik
<!--1356195-->
Bu sürümden itibaren, Silverlight artık istemci cihazlarına otomatik olarak yüklenmez. Daha fazla bilgi için bkz. [Windows bilgisayarlarına istemci dağıtma önkoşulları](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies)

## <a name="co-management"></a>Ortak yönetim

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Ortak yönetim kullanarak Intune 'a iş yükünü Endpoint Protection geçiş
<!-- 1357365 -->
 Endpoint Protection iş yükü, ortak yönetimi etkinleştirildikten sonra Intune 'a geçirilebilirler. Endpoint Protection iş yükünü dengelemek için ortak yönetim özellikleri sayfasına gidin ve kaydırıcı çubuğu Configuration Manager ' dan **pilot** ' a veya **tümüne**taşıyın. İş yükleri hakkında daha fazla bilgi için bkz. [ortak yönetim iş yükleri](../../../comanage/workloads.md). Ortak yönetim hakkında daha fazla bilgi için bkz. [Windows 10 cihazlar Için ortak yönetim](../../../comanage/overview.md).
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Configuration Manager ortak Yönetim Panosu
<!--1356648-->
Bu sürümden itibaren ortak yönetim hakkında bilgi içeren bir panoyu görüntüleyebilirsiniz. Pano, ortamınızda ortak yönetilen makineleri incelemenizi sağlar. Grafikler ilgilenilmesi gerekebilecek cihazları belirlemenize yardımcı olabilir. Ayrıntılar için bkz. [Ortak Yönetim Panosu](../../../comanage/how-to-monitor.md#co-management-dashboard) makalesi. 


## <a name="compliance-settings"></a>Uyumluluk ayarları

### <a name="microsoft-edge-browser-policies"></a>Microsoft Edge tarayıcı ilkeleri
<!-- 1357310 -->
Windows 10 istemcilerinde [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web tarayıcısını kullanan müşteriler için, birkaç Microsoft Edge ayarını yapılandırmak üzere bir Configuration Manager uyumluluk ayarları ilkesi oluşturun. Daha fazla bilgi için bkz. [Microsoft Edge tarayıcı profili oluşturma](../../../compliance/deploy-use/browser-profiles.md). 



## <a name="application-management"></a>Uygulama Yönetimi

### <a name="allow-user-interaction-when-installing-an-application"></a>Uygulama yüklenirken kullanıcı etkileşimine izin ver
<!-- 1356976 -->
Son kullanıcının, görev dizisinin çalıştırılması sırasında bir uygulama yüklemesiyle etkileşime girmesine izin verin. Örneğin, son kullanıcıya çeşitli seçenekler için istemde bulunan bir kurulum işlemi çalıştırın. Bazı uygulama yükleyicileri Kullanıcı istemlerini sessizmez veya yükleme işlemi yalnızca Kullanıcı tarafından bilinen belirli yapılandırma değerlerini gerektirebilir. Bu özellik, bu yükleme senaryolarını idare etmenizi sağlar. Daha fazla bilgi için bkz. [dağıtım türü için Kullanıcı deneyimi seçeneklerini belirtme](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Yenisiyle değiştirilen uygulamaları otomatik olarak yükseltme
<!-- 1351266 -->
Bir uygulama dağıtımını, yenisiyle değiştirilen sürümleri otomatik olarak yükseltmemelidir şekilde yapılandırın. Artık dağıtımı oluştururken, **Yazılım Dağıtma Sihirbazı**'Nın **dağıtım ayarları** sayfasında, **kullanılabilir** Kurulum amacı için, **Bu uygulamanın yenisiyle değiştirilen sürümlerini otomatik olarak yükseltme**seçeneğini etkinleştirebilir veya devre dışı bırakabilirsiniz. Daha fazla bilgi için bkz. [dağıtım ayarlarını belirtme](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Cihaz başına Kullanıcı için uygulama isteklerini Onayla
<!-- 1357015 -->
Bu sürümden itibaren, Kullanıcı onay gerektiren bir uygulama istediğinde, belirli cihaz adı artık isteğin bir parçasıdır. Yönetici isteği onayladığında, Kullanıcı yalnızca bu cihaza uygulamayı kurabilir. Kullanıcı başka bir cihaza uygulamayı yüklemek için başka bir istek göndermesi gerekir. Daha fazla bilgi için bkz. [dağıtım ayarlarını belirtme](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

 > [!Note]  
 > Bu, isteğe bağlı bir özelliktir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).  


### <a name="run-scripts-improvements"></a>Betikleri Çalıştır iyileştirmeleri 
<!-- 1236459 -->
 Bu sürümden itibaren, **betikleri Çalıştır** özelliği artık yayın öncesi bir özellik değildir. Betik çıktısı artık JSON biçimini kullanarak döndürüyor. Daha fazla bilgi için, bkz. [Configuration Manager konsolundan PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md).


## <a name="operating-system-deployment"></a>İşletim sistemi dağıtımı

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi aracılığıyla Windows 10 yerinde yükseltme görev dizisi
<!-- 1357149 -->
Windows 10 [yerinde yükseltme görev sırası](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) artık, [bulut yönetimi ağ geçidi](../../clients/manage/cmg/plan-cloud-management-gateway.md)aracılığıyla yönetilen internet tabanlı istemcilere dağıtımı desteklemektedir. Bu özellik, uzak kullanıcıların şirket ağına bağlanmasına gerek kalmadan Windows 10 ' a daha kolay yükseltme yapmasına olanak sağlar. Daha fazla bilgi için, bkz. [Deploy a task sequence](../../../osd/deploy-use/deploy-a-task-sequence.md).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 yerinde yükseltme görev dizisinde iyileştirmeler
<!-- 1357425 -->
Windows 10 yerinde yükseltme için varsayılan görev sırası şablonu, yükseltme işleminden önce ve sonra eklemek için önerilen eylemleri içeren ek gruplar içerir. Bu eylemler, cihazları Windows 10 ' a başarıyla yükselten birçok müşteri arasında ortaktır. Daha fazla bilgi için bkz. [bir işletim sistemini yükseltmek için görev dizisi oluşturma](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>İşletim sistemi dağıtımı geliştirmeleri
Bu sürüm, işletim sistemi dağıtımına yönelik aşağıdaki geliştirmeleri içerir:
- Windows PE 'de CMTrace. exe ' yi başlatırken, bu programın günlük dosyaları için varsayılan görüntüleyici yapıp yapmayacağını seçmeniz istenmez. <!-- SMS 500897 -->
- [Paket Içeriğini indirme](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent) görev dizisi adımına önyükleme görüntüleri ekleyin.
- [Görev sırasını Çalıştır](../../../osd/understand/task-sequence-steps.md#child-task-sequence) adımındaki geliştirmeler: <!-- 1261338 -->   
  - Yazılım Merkezi, PXE ve medyadan tüm işletim sistemi dağıtım senaryoları için destek.
  - Nesne silme sırasında kopyalama, içeri aktarma, dışarı aktarma ve uyarı gibi konsol eylemlerine yönelik geliştirmeler.
  - [Önceden hazırlanan Içerik dosyası oluşturma](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) Sihirbazı desteği.
  - Dağıtım doğrulama ile tümleştirme. Daha fazla bilgi için bkz. [yüksek riskli görev dizisi dağıtımları](../../../osd/deploy-use/deploy-a-task-sequence.md). 
  - Görev sırasını Çalıştır adımı artık yalnızca tek bir üst-alt ilişkisi değil birden çok görev dizisi düzeyinde kullanılabilir. Çok düzeyli ilişkiler karmaşıklığı artırır, bu nedenle dikkatli olun. Bu ilişkiler hala döngüsel başvurular için denetlenir.

### <a name="deployment-templates-for-task-sequences"></a>Görev dizileri için dağıtım şablonları
<!-- 1357391 -->
[Görev dizileri için Dağıtım Sihirbazı](../../../osd/deploy-use/deploy-a-task-sequence.md) artık bir dağıtım şablonu oluşturabilir. Dağıtım şablonu, dağıtım oluşturmak için var olan veya yeni bir görev dizisine kaydedilip uygulanabilir. 

### <a name="phased-deployments-for-task-sequences"></a>Görev dizileri için aşamalı dağıtımlar
<!--1356837-->
 Aşamalı dağıtımlar, [yayın öncesi bir özelliktir](../../servers/manage/pre-release-features.md). Aşamalı dağıtımlar, birden çok koleksiyonda bir görev dizisinin Eşgüdümlü, sıralı bir şekilde dağıtımını otomatik hale getirir. Varsayılan iki aşamadan oluşan [aşamalı dağıtımlar oluşturabilir](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) veya birden çok aşamayı el ile yapılandırabilirsiniz. Görev dizilerinin aşamalı dağıtımı PXE veya medya yüklemesini desteklemez.




## <a name="software-center"></a>Yazılım Merkezi

### <a name="install-multiple-applications-in-software-center"></a>Yazılım Merkezi 'nde birden çok uygulama yükler
<!-- 1357126 -->
Bir son kullanıcının veya masaüstü teknisyenin bir cihaza birden çok uygulama yüklemesi gerekiyorsa, Yazılım Merkezi artık birden fazla seçili uygulamayı yüklemeyi desteklemektedir. Bu davranış, bir sonraki başlatmadan önce bir yükleme işleminin bitmesini beklemirken kullanıcının daha verimli olmasını sağlar. Daha fazla bilgi için, bkz. yeni yazılım merkezi kullanıcı kılavuzunda [birden çok uygulama yüklemeyi](../../understand/software-center.md#install-multiple-applications) .

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Azure AD 'ye katılmış cihazlarda Kullanıcı tarafından kullanılabilen uygulamalara gözatıp yüklemek için yazılım merkezi 'ni kullanma
<!-- 1322613 -->
Uygulamaları kullanıcılara kullanılabilir olarak dağıtırsanız, artık Azure Active Directory (Azure AD) cihazlarındaki Yazılım Merkezi aracılığıyla bunlara göz atabilir ve bunları yükleyebilirler. Daha fazla bilgi için bkz. [Azure AD 'ye katılmış cihazlarda Kullanıcı tarafından kullanılabilen uygulamaları dağıtma](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Yüklü uygulamaları yazılım merkezi 'nde gizle
<!--1357592-->
Yüklü uygulamalar artık yazılım merkezi 'nde gizlenebilir. Zaten yüklü olan uygulamalar, bu seçenek istemci ayarları altında etkinleştirildiğinde, uygulamalar sekmesinde artık gösterilmez. Configuration Manager 1802 ' ye yüklediğinizde veya yükselttiğinizde Bu seçenek varsayılan olarak ayarlanır.  Yüklenen uygulamalar, yükleme durumu sekmesi altında hala gözden geçirilmek üzere kullanılabilir. [Yazılım Merkezi 'nde yüklü uygulamaları gizleme](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled) ek ayrıntılara sahiptir.   

### <a name="hide-unapproved-applications-in-software-center"></a>Yazılım merkezindeki onaylanmamış uygulamaları gizle
 <!--1355146-->
Bu istemci ayarı seçeneği etkin olduğunda, onay gerektiren Kullanıcı kullanılabilir uygulamaları yazılım merkezi 'nde gizlenir.  [Yazılım merkezindeki onaylanmamış uygulamaları Gizle](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved) ek ayrıntılara sahiptir.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Yazılım Merkezi Kullanıcı ek uyumluluk bilgilerini gösterir
<!-- 1235616 -->
 Şirket kaynaklarına koşullu erişim için bir uyumluluk ilkesi kuralı olarak Cihaz Sistem Durumu Kanıtlama durumu kullanılırken, Yazılım Merkezi artık kullanıcıya uyumlu olmayan Cihaz Sistem Durumu Kanıtlama ayarını gösterir.


 ## <a name="software-updates"></a>Yazılım güncelleştirmeleri 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Otomatik dağıtım kuralı değerlendirmesini temel bir günden aşağı kaydıracak şekilde zamanlayın. 
<!--1357133-->
Otomatik dağıtım kuralları, bir temel günden itibaren sapmayı değerlendirmek için zamanlanabilir. Anlamı olarak Salı düzeltme eki, sizin için Çarşamba günü geliyorsa, değerlendirme zamanlaması bir güne kadar ayın ikinci Salı değeri için ayarlanabilir. Ayrıntılar için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Raporlama

### <a name="report-for-default-browser-counts"></a>Varsayılan tarayıcı sayıları için rapor
<!-- 1357830 -->
Artık Windows varsayılan olarak belirli bir Web tarayıcısına sahip istemcilerin sayısını gösteren yeni bir rapor var. **Yazılım-şirketler ve ürünler** raporları grubundaki **varsayılan tarayıcı sayısı** raporuna bakın. Daha fazla bilgi için bkz. [rapor listesi](../../servers/manage/list-of-reports.md#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Windows Autopilot cihaz bilgileri hakkında rapor
<!-- 1351442 -->
Windows Autopilot, yeni Windows 10 cihazlarını modern bir şekilde ekleme ve yapılandırma çözümüdür. Daha fazla bilgi için bkz. [Windows Autopilot 'e genel bakış](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Windows Autopilot ile var olan cihazları kaydetmenin bir yöntemi, cihaz bilgilerini Iş ve eğitim için Microsoft Store karşıya yüklemedir. Bu bilgilere cihaz seri numarası, Windows ürün tanımlayıcısı ve bir donanım tanımlayıcısı dahildir. Bu cihaz bilgilerini toplamak ve yeni raporla, **Windows Autopilot cihaz bilgileri**, **donanım-genel** raporlar düğümünde bildirmek için Configuration Manager kullanın. Daha fazla bilgi için bkz. ortak yönetime hazırlanma bölümünde [İnternet tabanlı cihazları ortak yönetim için hazırlama](../../../comanage/how-to-prepare-Win10.md#windows-autopilot) .

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Belirli bir koleksiyon için Windows 10 Bakımı Ayrıntıları raporu
<!--1357653-->
**Belirli bir koleksiyon raporu Için Windows 10 Bakımı ayrıntıları** belirli bir koleksiyon için Windows 10 bakımı hakkında genel bilgileri görüntüler. Bu rapor, Windows 10 cihazlarının kaynak KIMLIĞI, NetBIOS adı, IŞLETIM sistemi adı, işletim sistemi sürüm adı, derleme, işletim sistemi dalı ve bakım durumunu gösterir. Daha fazla bilgi için bkz. [rapor listesi](../../servers/manage/list-of-reports.md#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Cihazları koruma

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Windows Defender Exploit Guard için Configuration Manager Ilkelerine yönelik iyileştirmeler
<!-- 1356220 -->
[Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction)Için Configuration Manager [saldırı yüzeyi azaltma](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR) ve [denetimli klasör erişim](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA) bileşenleri için ek ilke ayarları eklenmiştir.

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Windows Defender Application Guard için yeni konak etkileşim ayarları
<!-- 1356256 -->
Windows 10 sürüm 1709 ve üzeri cihazlarda, [Windows Defender Application Guard](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS)için iki yeni ana bilgisayar etkileşimi ayarı vardır: 
- Web sitelerine, konağın sanal grafik işlemcisine erişim verilebilir. 
- Kapsayıcı içinde indirilen dosyalar konakta kalıcı olabilir. 




## <a name="configuration-manager-console"></a>Configuration Manager konsolu

### <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager konsolundaki geliştirmeler 
Bu sürüm Configuration Manager konsoluna aşağıdaki geliştirmeleri içerir.
- Varlıklar ve uyumluluk, cihazlar altındaki cihaz listeleri artık birincil kullanıcıyı varsayılan olarak görüntüler. Bu sütun yalnızca cihazlar düğümünde görüntülenir. Oturum açan Son Kullanıcı, isteğe bağlı bir sütun olarak da eklenebilir.<!-- 1357280 --> Site için [Kullanıcı ve cihaz benzeşimi](../../clients/deploy/about-client-settings.md#user-and-device-affinity) istemci ayarlarını etkinleştirerek birincil kullanıcıyı bir cihazla ilişkilendirin.
- Bir koleksiyon başka bir koleksiyonun üyesiyse ve yeniden adlandırıldığında, yeni ad Üyelik kuralları altında güncelleştirilir.<!--1357282--> 
- Farklı DPı ölçekinde birden çok monitöre sahip bir istemcide uzaktan denetim kullanırken, fare imleci artık aralarında doğru şekilde eşlenir. <!--433170-->
- [Office 365 Istemci yönetimi panosu](../../../sum/deploy-use/office-365-dashboard.md) , grafik bölümleri seçildiğinde ilgili cihazların bir listesini görüntüler. <!--1357281 --> 



## <a name="next-steps"></a>Sonraki Adımlar
Bu sürümü yüklemeye hazırsanız, [Configuration Manager Için güncelleştirmeler](../../servers/manage/updates.md)bölümüne bakın.
