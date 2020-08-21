---
title: Sürüm 1806’deki yenilikler
titleSuffix: Configuration Manager
description: Geçerli dalın Configuration Manager sürüm 1806 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3b153dad513107b118d11fa95e3feaa035a1bc90
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692647"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Geçerli dalın Configuration Manager sürüm 1806 ' deki yenilikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme 1806, konsol içi bir güncelleştirme olarak sunulmaktadır. 1706, 1710 veya 1802 sürümünü çalıştıran sitelerde bu güncelleştirmeyi uygulayın. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Bu güncelleştirmeyi yüklemek için her zaman en son denetim listesini gözden geçirin. Daha fazla bilgi için bkz. [güncelleştirme 1806 yükleme denetim listesi](../../servers/manage/checklist-for-installing-update-1806.md). Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist)de gözden geçirin.

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

Aşağıdaki bölümler, geçerli dalın Configuration Manager sürüm 1806 ' deki değişiklikler ve yeni özelliklerle ilgili ayrıntıları sağlar.  



## <a name="deprecated-features-and-operating-systems"></a>Kullanımdan kaldırılan özellikler ve işletim sistemleri

[Kaldırılan ve kullanımdan kaldırılan öğelerde](deprecated/removed-and-deprecated.md)uygulanmadan önce yapılan değişiklikler hakkında bilgi edinin.

14 Ağustos 2018 itibariyle, karma mobil cihaz yönetimi özelliği kullanım dışıdır. Daha fazla bilgi için bkz. [karma MDM 'ye ne oldu](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Site altyapısı

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager, müşterilerin raporlama amacıyla kullanacağı, cihaz verilerinin büyük merkezi bir deposunu sağlamıştır. Site genellikle bu verileri haftalık olarak toplar. CMPivot, artık ortamınızdaki cihazların gerçek zamanlı durumuna erişim sağlayan yeni bir konsol içi yardımcı programdır. Hedef koleksiyondaki Şu anda bağlı olan tüm cihazlarda bir sorguyu hemen çalıştırır ve sonuçları döndürür. Daha sonra bu verileri, araçta filtreleyebilir ve gruplandırabilirsiniz. Çevrimiçi istemcilerden gerçek zamanlı veriler sunarak, iş sorularını daha hızlı bir şekilde yanıtlayabilir, sorun giderebilir ve güvenlik olaylarına yanıt verebilirsiniz. 

Daha fazla bilgi için bkz. [CMPivot](../../servers/manage/cmpivot.md).  


### <a name="site-server-high-availability"></a>Site sunucusu yüksek kullanılabilirliği
<!--1128774-->
Tek başına birincil site sunucusu rolü için yüksek kullanılabilirlik, pasif modda ek bir site sunucusu yüklemek için Configuration Manager tabanlı bir çözümdür. Pasif modda site sunucusu, etkin modda olan var olan site sunucunuza ek niteliğindedir. Pasif moddaki bir site sunucusu, gerektiğinde hemen kullanılmak üzere kullanılabilir. 

Daha fazla bilgi için aşağıdaki makaleleri inceleyin: 
- [Site sunucusu yüksek kullanılabilirliği](../../servers/deploy/configure/site-server-high-availability.md) 
- [Akış çizelgesi-pasif modda bir site sunucusu ayarlama](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [Akış Çizelgesi - Site sunucusu yükseltme (planlı)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [Akış Çizelgesi - Site sunucusu yükseltme (plansız)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### <a name="improvements-to-management-insights"></a>Yönetim öngörülerine yönelik geliştirmeler
Bu sürüm, yönetim öngörülerine yönelik aşağıdaki geliştirmeleri içerir:  

- Bazı yönetim öngörüleri artık bir eylem alma seçeneğine sahiptir. Bu eylem, konsolundaki ilişkili düğüme gidiliyor ya da filtrelenmiş, sorgu tabanlı bir görünüm gösteriliyor.<!--1357930-->  

- Öngörülebilir bakım için yeni bir grup olan altı yeni kurala göre, düzenli bir koruma sayesinde olası yapılandırma sorunlarını vurgulamanıza yardımcı olur.<!--1352184-->  

Daha fazla bilgi için bkz. [Management Insights](../../servers/manage/management-insights.md).


### <a name="configuration-manager-tools"></a>Configuration Manager araçları
<!--1357145-->
Configuration Manager sunucusu ve istemci araçları artık sunucuya dahil edilmiştir. Bunları `CD.Latest\SMSSETUP\Tools` site sunucusundaki klasöründe bulabilirsiniz. Başka yükleme gerekli değildir. 

Daha fazla bilgi için bkz. [Configuration Manager araçları](../../support/tools.md).


### <a name="exclude-active-directory-containers-from-discovery"></a>Active Directory kapsayıcılarını keşifden hariç tut
<!--1358143-->
Bulunan nesnelerin sayısını azaltmak için, belirli kapsayıcıları Active Directory sistem bulağından dışlayın. 

Daha fazla bilgi için bkz. [Active Directory sistem bulmayı yapılandırma](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd).



## <a name="content-management"></a>İçerik yönetimi

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Site sunucusu için uzak içerik kitaplığı yapılandırma
<!--1357525-->
Site sunucusu yüksek kullanılabilirliği yapılandırmak veya merkezi yönetim veya birincil site sunucularınızda sabit disk alanı boşaltmak için, içerik kitaplığını başka bir depolama konumuna yeniden yerleştir. İçerik kitaplığını site sunucusundaki başka bir sürücüye, ayrı bir sunucuya veya bir depolama alanı ağında (SAN) hataya dayanıklı disklere taşıyın. 

Daha fazla bilgi için aşağıdaki makaleleri inceleyin: 
- [İçerik kitaplığı](../hierarchy/the-content-library.md)
- [Akış çizelgesi - İçerik kitaplığını yönetme](../hierarchy/manage-content-library-flowchart.md)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Azure Resource Manager için bulut dağıtım noktası desteği
<!--1322209-->
Bir bulut dağıtım noktası oluştururken, sihirbaz artık **Azure Resource Manager dağıtımı**oluşturma seçeneği sağlar. Azure Resource Manager, tüm çözüm kaynaklarının, kaynak grubu olarak adlandırılan tek bir varlık olarak yönetilmesine yönelik modern bir platformdur. Azure Resource Manager ile bulut dağıtım noktası dağıtımında, site kimlik doğrulaması yapmak ve gerekli bulut kaynaklarını oluşturmak için Azure Active Directory kullanır. Bu modernlanmış dağıtım, klasik Azure Yönetim sertifikası gerektirmez. 

Bulut dağıtım noktası için özellik belgeleri de düzeltilir ve geliştirilmiştir. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:
- [Bulut dağıtım noktası kullan](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [Bulut dağıtım noktası yükler](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Çekme dağıtım noktaları, bulut dağıtım noktalarını kaynak olarak destekler  
<!--1321554-->
Birçok müşteri, WAN genelindeki bir kaynak dağıtım noktasından içerik indirecek uzak veya şubelerde çekme dağıtım noktalarını kullanır. Uzak ofislerinizin internete daha iyi bağlantısı varsa veya WAN bağlantılarınızda yükü azaltmak için artık kaynak olarak Microsoft Azure bir bulut dağıtım noktası kullanabilirsiniz. Dağıtım noktası özelliklerinin **çekme dağıtım noktası** sekmesine bir kaynak eklediğinizde, sitedeki herhangi bir bulut dağıtım noktası artık kullanılabilir bir dağıtım noktası olarak listelenir. Site sistem rollerinin her ikisi de aynı şekilde kalır. 

Daha fazla bilgi için bkz. [çekme dağıtım noktaları kullanma](../hierarchy/use-a-pull-distribution-point.md).


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Ağ tıkanıklık denetimini kullanmak için dağıtım noktalarını etkinleştir
<!--1358112-->
Windows düşük ekstra gecikmeli arka plan taşıması (LEDBAT), arka plan ağ aktarımlarının yönetilmesine yardımcı olmak için Windows Server 'ın bir özelliğidir. Desteklenen Windows Server sürümlerinde çalışan dağıtım noktaları için, ağ trafiğini ayarlamanıza yardımcı olacak bir seçenek etkinleştirin. İstemciler yalnızca kullanılabilir olduğunda ağ bant genişliğini kullanır. 

Daha fazla bilgi için bkz. [Windows LEDBAT](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>WAN kullanımını azaltmak için istemci eş önbelleğinde kısmi indirme desteği
<!--1357346-->
İstemci eş önbelleği kaynakları artık içeriği parçalara bölebilir. Bu parçalar, WAN kullanımını azaltmak için Ağ aktarımını en aza indirir. Yönetim noktası, içerik bölümlerinin daha ayrıntılı bir şekilde izlenmesini sağlar. Aynı içeriğin her sınır grubu için birden fazla indirilmesini ortadan kaldırmaya çalışır. 

Daha fazla bilgi için bkz. [kısmi indirme desteği](../hierarchy/client-peer-cache.md#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Eş indirmeleri için sınır grubu seçenekleri
<!--1356193-->
Artık sınır grupları ortamınızda içerik dağıtımı üzerinde daha fazla denetim sağlamak için ek ayarlar içerir. Bu sürüm aşağıdaki seçenekleri ekler:  

- **Bu sınır grubunda eş indirmelere Izin ver**: yönetim noktası, istemcilere eş kaynakları içeren içerik konumlarının bir listesini sağlar. Bu ayar, teslim Iyileştirmesi için Grup kimliklerinin uygulanmasını da etkiler.  

- **Eş Indirmeleri sırasında yalnızca aynı alt ağdaki eşleri kullanın**: yönetim noktası yalnızca istemciyle aynı alt ağda bulunan içerik konumu listesi eş kaynaklarını içerir.  

Daha fazla bilgi için bkz. [eş İndirmeleri Için sınır grubu seçenekleri](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="improvement-to-peer-cache-source-location-status"></a>Eş önbellek kaynak konumu durumu iyileştirmesi
<!--SCCMDocs issue 850-->
Configuration Manager, eş önbellek kaynağının başka bir konuma dolaşıma alındığını belirlemede daha etkilidir. Bu davranış, yönetim noktasının, eski konumda değil, yeni konumdaki istemcilere içerik kaynağı olarak sunabilmesini sağlar. Eş önbellek özelliğini gezici eş önbellek kaynaklarıyla kullanıyorsanız, siteyi sürüm 1806 ' e güncelleştirdikten sonra tüm eş önbellek kaynaklarını en son istemci sürümüne de güncelleştirin. Yönetim noktası, en az sürüm 1806 ' e güncelleştirilene kadar bu eş önbellek kaynaklarını içerik konumları listesinde içermez.

Daha fazla bilgi için bkz. [eş önbellek gereksinimleri](../hierarchy/client-peer-cache.md#requirements).



<!-- ## Migration  -->



## <a name="client-management"></a>İstemci yönetimi

### <a name="improvement-to-client-push-security"></a>İstemci anında iletme güvenliğine iyileştirme
<!--1358204-->
Configuration Manager istemcisini yüklemek için Client Push yöntemini kullanırken, site artık Kerberos karşılıklı kimlik doğrulaması gerektirebilir. Bu geliştirme, sunucu ve istemci arasındaki iletişimin güvenliğini sağlamaya yardımcı olur. 

Daha fazla bilgi için bkz. [Client Push ile istemcileri yükleme](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


### <a name="enhanced-http-site-system"></a><a name="bkmk_ehttp"></a> Gelişmiş HTTP sitesi sistemi
<!--1356889,1358228-->
HTTPS iletişimini kullanmak tüm Configuration Manager iletişim yollarında önerilir, ancak PKI sertifikalarını yönetme yükü nedeniyle bazı müşteriler için zor olabilir.

Bu sürüm, istemcilerin site sistemleriyle iletişim kurmasına yönelik iyileştirmeler içerir. Site Özellikleri, **Istemci bilgisayar iletişimi** sekmesinde, **https veya http**seçeneğini belirleyin ve ardından yeni seçeneği **http site sistemleri Için Configuration Manager tarafından oluşturulan sertifikaları kullanma**seçeneğini etkinleştirin. Bu özellik, [yayın öncesi bir özelliktir](../../servers/manage/pre-release-features.md).

Daha fazla bilgi için bkz. [GELIŞMIŞ http](../hierarchy/enhanced-http.md).


### <a name="azure-ad-device-identity"></a>Azure AD cihaz kimliği 
<!--1358460-->
Azure AD Kullanıcı oturumu olmayan bir [Azure AD 'ye katılmış](/azure/active-directory/devices/concept-azure-ad-join) veya [hibrit Azure AD cihazı](/azure/active-directory/devices/concept-azure-ad-join-hybrid) , atanan sitesiyle güvenli bir şekilde iletişim kurabilir. Bulut tabanlı cihaz kimliği artık CMG ve yönetim noktasıyla kimlik doğrulaması için yeterlidir.  

Daha fazla bilgi için bkz. [GELIŞMIŞ http](../hierarchy/enhanced-http.md).


### <a name="cmtrace-installed-with-client"></a>İstemci ile CMTrace yüklendi
<!--1357971-->
CMTrace günlük görüntüleme aracı artık Configuration Manager istemcisiyle birlikte otomatik olarak yüklenir. Bu, varsayılan olarak olan istemci yükleme dizinine eklenir `%WinDir%\ccm\cmtrace.exe` . 

Daha fazla bilgi için bkz. [CMTrace](../../support/cmtrace.md).


### <a name="cloud-management-dashboard"></a>Bulut yönetimi panosu
<!--1358461-->
Yeni bulut yönetimi panosu, bulut yönetimi ağ geçidi (CMG) kullanımı için merkezi bir görünüm sağlar. Site, Azure AD ile eklendi olduğunda, bulut kullanıcıları ve cihazları hakkındaki verileri de görüntüler.   

Bu özellik ayrıca sorun gidermeye yardımcı olmak üzere gerçek zamanlı doğrulama için **CMG bağlantı çözümleyici** 'yi içerir. Konsol içi yardımcı programı hizmetin geçerli durumunu ve CMG bağlantı noktası üzerinden gelen iletişim kanalını CMG trafiğine izin veren herhangi bir yönetim noktasına denetler. 

Daha fazla bilgi için, [izleme CMG](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md) makalesinin aşağıdaki bölümlerine bakın:  
- [Bulut yönetimi panosu](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [Bağlantı çözümleyici](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi geliştirmeleri

Sürüm 1806, bulut yönetimi ağ geçidi (CMG) için aşağıdaki geliştirmeleri içerir:

#### <a name="simplified-client-bootstrap-command-line"></a>Basitleştirilmiş istemci önyükleme komut satırı
<!--1358215-->
Configuration Manager istemcisini bir CMG aracılığıyla internet 'e yüklerken, komut satırı artık daha az özellik gerektirir. Bu geliştirme, ortak yönetim için hazırlanırken Microsoft Intune ' de kullanılan komut satırının boyutunu azaltır. 

Daha fazla bilgi için bkz. [İnternet tabanlı cihazları ortak yönetim için hazırlama](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

#### <a name="download-content-from-a-cmg"></a>Bir CMG 'den içerik indirin
<!--1358651-->
Daha önce, bulut dağıtım noktası ve CMG 'yi ayrı roller olarak dağıtmanız gerekiyordu. Bir CMG artık istemcilere içerik de sunabilir. Bu işlevsellik, Azure VM 'lerinin gerekli sertifikalarını ve maliyetini azaltır. 

Daha fazla bilgi için bkz. [CMG 'Yi değiştirme](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Azure AD 'de güvenilen kök sertifika gerekli değildir
<!--503899-->
Bir CMG oluşturduğunuzda, artık ayarlar sayfasında [Güvenilen bir kök sertifika](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) sağlamanız gerekmez. İstemci kimlik doğrulaması için Azure Active Directory (Azure AD) kullanılırken bu sertifika gerekli değildir, ancak sihirbazda gerekli olması için kullanılır. PKI istemci kimlik doğrulama sertifikaları kullanıyorsanız, yine de CMG 'ye bir güvenilen kök sertifika eklemeniz gerekir.



## <a name="co-management"></a>Ortak yönetim

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Ortak yönetilen bir cihaz için Microsoft Intune MDM ilkesini eşitleme
<!--1357377-->
Ortak yönetim iş yükünü değiştirdiğinizde, ortak yönetilen cihazlar MDM ilkesini Microsoft Intune otomatik olarak eşitler. Bu eşitleme Ayrıca, Configuration Manager konsolundaki Istemci bildirimlerinden **bilgisayar Ilkesini indir** eylemini başlattığınızda de gerçekleşir. 

Daha fazla bilgi için bkz. [Configuration Manager iş yüklerini Intune 'a değiştirme](../../../comanage/how-to-switch-workloads.md).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Ortak yönetim kullanarak yeni iş yüklerini Intune 'a geçirme
Aşağıdaki iş yükleri artık ortak yönetim etkinleştirildikten sonra Configuration Manager Intune 'a geçiş yapabilir:  

- **Cihaz yapılandırması**<!--1357903-->: Bu iş yükü, uygulamaları dağıtmak için Configuration Manager kullanmaya devam ederken MDM ilkelerini dağıtmak için Intune 'U kullanmanıza olanak sağlar.  

- **Office 365**<!--1357841-->: Cihazlar Configuration Manager 'den Office 365 dağıtımlarını yüklemez.  

- **Mobil uygulamalar**<!--1357892-->: Intune 'dan dağıtılan tüm kullanılabilir uygulamalar Şirket Portalı kullanılabilir. Configuration Manager 'ten dağıttığınız uygulamalar yazılım merkezi 'nde kullanılabilir. Bu özellik, [yayın öncesi bir özelliktir](../../servers/manage/pre-release-features.md).  

Bu iş yüklerini taşımak için ortak yönetim özellikleri sayfasına gidin ve iş yükü kaydırıcı çubuğunu Configuration Manager 'den **pilot** 'A veya **tümüne**taşıyın. 

Daha fazla bilgi için bkz. [Windows 10 cihazlar Için ortak yönetim](../../../comanage/overview.md).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Tek bir Intune kiracısında birden çok hiyerarşi desteği
<!--1357944-->
Bazı müşteriler birkaç Configuration Manager hiyerarşilerine sahiptir ve gelecekte Azure Active Directory ve Microsoft Intune tek bir kiracıya birleştirmek ister. Ortak yönetim artık aynı Intune kiracısına birden fazla Configuration Manager ortamı bağlamayı desteklemektedir.

Daha fazla bilgi için bkz. [ortak yönetim önkoşulları](../../../comanage/overview.md#prerequisites).
 


## <a name="compliance-settings"></a>Uyumluluk ayarları

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Microsoft Edge için Windows Defender SmartScreen ayarlarını yapılandırma
<!--1353701-->
Microsoft Edge tarayıcı uyumluluk ayarları ilkesi, Windows Defender SmartScreen için aşağıdaki üç ayarı ekler: 
- SmartScreen 'e izin ver
- Kullanıcılar, siteler için SmartScreen istemi 'ni geçersiz kılabilir
- Kullanıcılar dosyalar için SmartScreen istemi 'ni geçersiz kılabilir

Daha fazla bilgi için bkz. [Microsoft Edge ayarlarını yapılandırma](../../../compliance/deploy-use/browser-profiles.md).


### <a name="scap-extensions"></a>SCAP Uzantıları
<!--1357552-->
Güvenlik Içeriği Otomasyon Protokolü (SCAP) içeriğini uyumluluk ayarları temellerine dönüştürün ve konsol uzantısı kullanarak SCAP raporları oluşturun. Bu özellik ayrıca, istemci uyumluluğunu ve XCCDF kural uyumluluğunu görselleştirmek için yeni bir pano da içerir. 





## <a name="application-management"></a>Uygulama yönetimi

### <a name="phased-deployment-of-applications"></a>Uygulamaların aşamalı dağıtımı
<!--1358147-->
Bir uygulama için aşamalı dağıtım oluşturun. Aşamalı dağıtımlar, özelleştirilebilir ölçütlere ve gruplara göre düzenlenmiş, sıralı bir yazılım dağıtımını düzenlemenize olanak tanır. Örneğin, uygulamayı bir pilot koleksiyonuna dağıtın ve ardından başarı ölçütlerine göre otomatik olarak piyasaya devam edin. 

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

- [Aşamalı dağıtım oluşturma](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

- [Aşamalı dağıtım izleme ve yönetme](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Bir cihazdaki tüm kullanıcılar için Windows uygulama paketleri sağlama
<!--1358310-->
Cihazdaki tüm kullanıcılar için Windows uygulama paketi ile bir uygulama sağlayın. Bu senaryonun yaygın bir örneği, bir okuldaki öğrenciler tarafından kullanılan tüm cihazlara Minecseft: eğitim sürümü gibi Iş ve eğitim Microsoft Store bir uygulama sağlamadır. Daha önce Configuration Manager yalnızca Kullanıcı başına bu uygulamaları yüklemeyi destekler. Yeni bir cihazda oturum açtıktan sonra bir öğrenciye bir uygulamaya erişmeniz gerekir. Artık uygulama tüm kullanıcılar için cihaza sağlandığında, daha hızlı bir şekilde üretken olabilirler. 

Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../../../apps/get-started/creating-windows-applications.md#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office Özelleştirme Aracı tümleştirmesiyle Office 365 yükleyicisi
<!--1358149-->
Office özelleştirme aracı artık Configuration Manager konsolundaki Office 365 yükleyicisiyle tümleşiktir. Office 365 için bir dağıtım oluştururken, en yeni Office yönetilebilirlik ayarlarını dinamik olarak yapılandırın. Microsoft, Office Özelleştirme Aracı 'nı yeni Office 365 derlemelerini yayınlarsa güncelleştirir. Bu tümleştirme, Office 365 ' deki yeni yönetilebilirlik ayarlarından yararlanarak kullanılabilir duruma gelir. 

Daha fazla bilgi için bkz. [Office 365 uygulamalarını dağıtma](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


### <a name="support-for-new-windows-app-package-formats"></a>Yeni Windows uygulama paketi biçimleri için destek
<!--1357427-->
Configuration Manager artık yeni Windows 10 uygulama paketi (. msix) ve uygulama paketi (. msixdemeti) biçimlerinin dağıtımını desteklemektedir. 

Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).


### <a name="uninstall-application-on-approval-revocation"></a>Onay iptalinde uygulamayı kaldır
<!--1357891-->
Bir uygulama için onayı iptal ettiğinizde davranış değişmiştir. Artık uygulama isteğini reddetmeniz durumunda, istemci uygulamayı kullanıcının cihazından kaldırır. Bu davranış, **cihaz başına kullanıcılara yönelik uygulama isteklerini Onayla** [özelliğini](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) etkinleştirmenizi gerektirir. 

Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).


### <a name="package-conversion-manager"></a>Paket Dönüştürme Yöneticisi 
<!--1357861-->
Paket Dönüştürme Yöneticisi artık eski paketleri Configuration Manager güncel dal uygulamalarına dönüştürmenize olanak sağlayan tümleşik bir araçtır. Daha sonra bağımlılıklar, gereksinim kuralları ve Kullanıcı cihaz benzeşimi gibi uygulamaların özelliklerini kullanabilirsiniz.

Daha fazla bilgi için bkz. [Paket Dönüştürme Yöneticisi](../../../apps/pcm/package-conversion-manager.md).



## <a name="os-deployment"></a>İşletim sistemi dağıtımı

### <a name="improvements-to-phased-deployments"></a>Aşamalı dağıtımlarda iyileştirmeler

Bu sürüm, aşamalı dağıtımlar için aşağıdaki geliştirmeleri içerir:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>El ile yapılandırılan aşamalarla aşamalı bir dağıtım oluşturma
<!--1358148-->
Bir görev dizisi için artık aşamalı dağıtım oluştururken aşamaları el ile yapılandırın. Aşamalı dağıtım oluşturma sihirbazının **aşamalar** sekmesinden 10 ' a kadar ek aşama ekleyin. Yine de otomatik olarak bir varsayılan iki aşamalı dağıtımı oluşturabilirsiniz. 

Daha fazla bilgi için bkz. [el ile yapılandırılan aşamalarla aşamalı dağıtım oluşturma](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual).

#### <a name="phased-deployment-status"></a>Aşamalı dağıtım durumu
<!--1358577-->
Aşamalı dağıtımlar artık yerel bir izleme deneyimine sahiptir. **İzleme** çalışma alanındaki **dağıtımlar** düğümünden aşamalı bir dağıtım seçin ve ardından şeritte **aşamalı dağıtım durumu** ' nu tıklatın. 

Daha fazla bilgi için bkz. [aşamalı dağıtımları yönetme ve izleme](../../../osd/deploy-use/manage-monitor-phased-deployments.md).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Aşamalı dağıtımlar sırasında aşamalı dağıtım
<!--1358578-->
Aşamalı bir dağıtım sırasında, her bir aşamadaki dağıtım artık aşamalı olarak gerçekleşebilir. Bu davranış, dağıtım sorunları riskini azaltmaya yardımcı olur ve içeriğin istemcilere dağıtılması nedeniyle ağdaki yükü azaltır. Site, her bir aşamanın yapılandırmasına bağlı olarak yazılımı aşamalı olarak kullanılabilir hale getirir. Bir aşamadaki her istemcinin, yazılımın kullanılabilir hale getirilme zamanına göre son tarihi vardır. Kullanılabilir saat ve son tarih arasındaki zaman penceresi, bir aşamadaki tüm istemciler için aynıdır. 

Daha fazla bilgi için bkz. [aşama ayarları](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 yerinde yükseltme görev dizisinde iyileştirmeler
<!--1358500-->
Windows 10 yerinde yükseltme için varsayılan görev sırası şablonu, yükseltme işleminin başarısız olması durumunda eklemek için önerilen eylemleri içeren başka bir yeni grup içerir. Bu eylemler, sorun gidermeyi kolaylaştırır. Bu tür bir araç Windows [Setupdiag](/windows/deployment/upgrade/setupdiag)'dir. Bir Windows 10 yükseltmesinin neden başarısız olduğuna ilişkin ayrıntıları almak için tek başına bir tanılama aracıdır. 

Daha fazla bilgi için bkz. [bir işletim sistemini yükseltmek için görev dizisi oluşturma](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>PXE 'yi destekleyen dağıtım noktalarında iyileştirmeler
<!--1357580-->
Dağıtım noktası özelliklerinin **PXE** sekmesinde, **Windows Dağıtım HIZMETI olmadan bir PXE yanıtlayıcısını etkinleştir**' i işaretleyin. Bu yeni seçenek, dağıtım noktasında Windows Dağıtım Hizmetleri (WDS) gerektirmeyen bir PXE yanıtlayıcıu sunar. WDS gerekli olmadığından, PXE 'yi destekleyen dağıtım noktası Windows Server Core dahil olmak üzere bir istemci veya sunucu işletim sistemi olabilir. Bu yeni PXE Yanıtlayıcı hizmeti IPv6 'yı destekler ve ayrıca uzak ofislerdeki PXE özellikli dağıtım noktalarının esnekliğini geliştirir. 

Daha fazla bilgi için bkz. [dağıtım NOKTASıNDA PXE 'yi etkinleştirme](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Bazı senaryolar için ağ erişim hesabı gerekli değildir
<!--1358278,1358279-->
[GELIŞMIŞ http site sistemi](#bkmk_ehttp) özelliği, ağ erişim hesabındaki bazı bağımlılıkları da kaldırır. Yeni site seçeneğini **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanmak**üzere etkinleştirdiğinizde, aşağıdaki senaryolar bir dağıtım noktasından içerik indirmek için bir ağ erişim hesabı gerektirmez:  

- Önyükleme medyasından veya PXE 'den çalışan görev dizileri
- Yazılım merkezinden çalıştırılan görev dizileri  

Bu görev dizileri işletim sistemi dağıtımı veya özel olabilir. Çalışma grubu bilgisayarları için de desteklenir.

Daha fazla bilgi için bkz. [görev dizileri ve ağ erişim hesabı](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).


### <a name="other-improvements-to-os-deployment"></a>İşletim sistemi dağıtımına yönelik diğer geliştirmeler

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Görev sırası değişkenlerinde depolanan hassas verileri maskeleme
 <!--1358330-->
 **Görev sırası değişkenini ayarla** adımında, **Bu değeri gösterme**yeni seçeneğini belirleyin. 

 Daha fazla bilgi için bkz. [görev dizisi değişkenini ayarlama](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Görev dizisinin komut adımını Çalıştır sırasında program adını maskele
 <!--1358493-->
 Büyük olasılıkla hassas verilerin görüntülenmesini veya günlüğe kaydedilmesini engellemek için, **Osddonotlogcommand**görev dizisi değişkenini yapılandırın.  

 Daha fazla bilgi için bkz. [görev dizisi değişkenleri](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand). 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Sürücüler yüklenirken DıSM parametreleri için görev sırası değişkeni
 <!--516679/2840016-->
 DıSM için ek komut satırı parametreleri belirtmek üzere, **Osdınstalldriversaddıtionaloptions**adlı yeni görev dizisi değişkenini kullanın. 

 Daha fazla bilgi için bkz. [görev dizisi değişkenleri](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions). 

#### <a name="option-to-use-full-disk-encryption"></a>Tam disk şifrelemesi kullanma seçeneği
 <!--SCCMDocs-pr issue 2671-->
 Hem **BitLocker 'ı etkinleştir** hem de **önceden sağlama BitLocker** adımları artık **tam disk şifrelemesi kullanma**seçeneği içerir. Varsayılan olarak, bu adımlar sürücüdeki kullanılan alanı şifreler. Bu varsayılan davranış, daha hızlı ve daha verimli olduğu için önerilir. 

 Daha fazla bilgi için bkz. [BitLocker 'ı etkinleştirme](../../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker) ve [BitLocker 'ın ön sağlamasını](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker)kaldırma. 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>Windows 10 yükseltme uyumluluğu taraması ile istemci sağlama modu etkin değil
 <!--SCCMDocs-pr issue 2812-->
 Şimdi **yükseltme işlemini başlatmadan Windows Kurulumu uyumluluk taraması gerçekleştirme**seçeneğini etkinleştirdiğinizde, **işletim sistemini Yükselt** görev dizisi adımı, Configuration Manager istemcisini sağlama moduna yerleştirmez.

 Daha fazla bilgi için bkz. [Işletim sistemini yükseltme](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).

#### <a name="revised-documentation-for-task-sequence-variables"></a>Görev dizisi değişkenleri için düzeltilen belgeler
Görev sırası değişkenlerini anlamak için şu iki yeni makale kullanıma sunulmuştur:  

- [Görev dizisi değişkenlerini kullanma](../../../osd/understand/using-task-sequence-variables.md) , farklı değişken türlerini, değişkenleri ayarlamaya yönelik yöntemleri ve bunlara nasıl erişebileceğinizi açıklayan yeni bir makaledir.  

- [Görev dizisi değişkenleri](../../../osd/understand/task-sequence-variables.md) , kullanılabilir tüm görev dizisi değişkenlerine yönelik bir başvurudur. Bu makale, yerleşik değişkenleri eylem değişkenleriyle birleştiren önceki makaleleri birleştirir. 



## <a name="software-center"></a>Yazılım Merkezi

> [!Important]  
> Yeni Configuration Manager özelliklerinden yararlanmak için önce istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.


### <a name="software-center-infrastructure-improvements"></a>Software Center altyapı geliştirmeleri
<!--1358309-->
Uygulama Kataloğu rollerinin artık yazılım merkezi 'nde Kullanıcı tarafından kullanılabilen uygulamaları görüntülemesi gerekmez. Bu değişiklik, kullanıcılara uygulama sunmak için gereken sunucu altyapısını azaltmanıza yardımcı olur. Yazılım Merkezi artık, bu bilgileri almak için yönetim noktasına dayanır ve bu da daha büyük ortamların [sınır gruplarına](../../servers/deploy/configure/boundary-groups.md#management-points)atayarak daha iyi ölçeklendirilmesine yardımcı olur.

Daha fazla bilgi için bkz. [yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)  

> [!Note]  
> Uygulama Kataloğu web sitesi noktası ve Web hizmeti noktası rolleri artık 1806 ' de *gerekli* değildir, ancak yine de *desteklenmiş* rollerdir. 
> 
> Uygulama Kataloğu web sitesi noktası için **Silverlight Kullanıcı deneyimi** artık desteklenmiyor. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Yazılım Merkezi 'nde Uygulama Kataloğu web sitesi bağlantısının görünürlüğünü belirtin
<!--1358214-->
**Uygulama Kataloğu Web sitesini açma** bağlantısının yazılım merkezi 'nin **yükleme durumu** düğümünde görüntülenip görüntülenmeyeceğini denetlemek için istemci ayarlarını kullanın.  

Daha fazla bilgi için bkz. [Software Center istemci ayarları](../../clients/deploy/about-client-settings.md#software-center).

> [!Note]  
> Uygulama Kataloğu web sitesi noktası için **Silverlight Kullanıcı deneyimi** artık desteklenmiyor. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Yazılım Merkezi 'nde Web sayfası için özel sekme
<!--1358132-->
Yazılım Merkezi 'nde bir Web sayfası açmak için özelleştirilmiş bir sekme oluşturmak üzere istemci ayarlarını kullanın. Bu özellik, son kullanıcılarınıza yönelik içeriği tutarlı ve güvenilir bir şekilde gösterbırakmanıza olanak tanır. Aşağıdaki listede birkaç örnek verilmiştir:  

- BT ile iletişim kurun: kuruluşunuzun BT departmanınızla iletişim kurma hakkında bilgi  

- BT Destek Merkezi: Bilgi Bankası araması veya destek bileti açma gibi self servis eylemleri.  

- Son Kullanıcı belgeleri: kuruluşunuzdaki kullanıcılar için uygulamalar kullanma veya Windows 10 ' a yükseltme gibi çeşitli BT konularına yönelik makaleler.  

Daha fazla bilgi için bkz. [Software Center istemci ayarları](../../clients/deploy/about-client-settings.md#software-center) ve [Yazılım Merkezi Kullanıcı Kılavuzu](../../understand/software-center.md).


### <a name="maintenance-windows-in-software-center"></a>Yazılım Merkezi 'nde bakım pencereleri
<!--1358131-->
Yazılım Merkezi artık bir sonraki zamanlanmış bakım penceresini görüntülüyor. Yükleme durumu sekmesinde, görünümü tümü ' nden yakında olacak şekilde değiştirin. Zamanlanan zaman aralığını ve dağıtım listesini görüntüler. Gelecek bakım pencereleri yoksa, liste boştur. 

Daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../clients/manage/collections/use-maintenance-windows.md) ve [Yazılım Merkezi Kullanıcı Kılavuzu](../../understand/software-center.md).



## <a name="software-updates"></a>Yazılım güncelleştirmeleri

### <a name="third-party-software-updates"></a>Üçüncü taraf yazılım güncelleştirmeleri
<!--1357605, 1352101, 1358714-->
Üçüncü taraf yazılım güncelleştirmeleri, Configuration Manager konsolundaki iş ortağı kataloglarına abone olmanızı ve güncelleştirmeleri WSUS 'e yayımlamanıza olanak sağlar. Ardından, mevcut yazılım güncelleştirme yönetimi işlemini kullanarak bu güncelleştirmeleri dağıtabilirsiniz. 

Daha fazla bilgi için bkz. [üçüncü taraf güncelleştirmelerini etkinleştirme](../../../sum/deploy-use/third-party-software-updates.md).


### <a name="deploy-software-updates-without-content"></a>Yazılım güncelleştirmelerini içerik olmadan dağıtma
<!--1357933-->
Yazılım güncelleştirmelerini, ilk olarak içerik indirip dağıtım noktalarına dağıtmadan cihazlara dağıtın. Bu özellik son derece büyük güncelleştirme içeriğiyle ilgilenirken veya istemcilerin Microsoft Update bulut hizmetinden her zaman içerik almasını istediğinizde faydalıdır. Bu senaryodaki istemciler, gerekli içeriğe zaten sahip olan eşlerden içerik de indirebilir. Configuration Manager istemcisi içerik indirmeyi yönetmeye devam eder, bu nedenle Configuration Manager eş önbellek özelliğini veya teslim Iyileştirme gibi diğer teknolojileri kullanabilir. Bu özellik, Windows ve Office güncelleştirmeleri de dahil olmak üzere Configuration Manager yazılım güncelleştirme yönetimi tarafından desteklenen tüm güncelleştirme türlerini destekler. 

Daha fazla bilgi için, [yazılım güncelleştirmelerini el ile dağıtırken](../../../sum/deploy-use/manually-deploy-software-updates.md) veya [yazılım güncelleştirmelerini otomatik olarak](../../../sum/deploy-use/automatically-deploy-software-updates.md)dağıttığınızda **dağıtım paketi yok** seçeneğine bakın.


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Otomatik dağıtım kurallarını yazılım güncelleştirme mimarisine göre filtrele
 <!--1322266-->
Artık Itanium ve ARM64 gibi mimarileri hariç tutmak için otomatik dağıtım kuralları (ADR) filtreleyerek filtre uygulayabilirsiniz. Otomatik dağıtım kuralı oluşturma Sihirbazı ' nın **yazılım güncelleştirmeleri** sayfasında, **mimari** özelliği filtresi artık kullanılabilir. 

Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### <a name="improved-wsus-maintenance"></a>Geliştirilmiş WSUS Bakımı 
<!--1357898-->
WSUS Temizleme Sihirbazı artık, yazılım güncelleştirme noktası bileşen özelliklerinde tanımlanan yenisiyle değiştirme kurallarına göre zaman aşımına uğradığı güncelleştirmeleri reddeder. 

Daha fazla bilgi için bkz. [yazılım güncelleştirmeleri Bakımı](../../../sum/deploy-use/software-updates-maintenance.md).



## <a name="reporting"></a>Raporlama

### <a name="new-software-updates-compliance-report"></a>Yeni yazılım güncelleştirmeleri uyumluluk raporu
<!--1357775-->
Yazılım güncelleştirmeleri uyumluluğuna ilişkin raporları görüntülemek, genellikle sitesiyle en son iletişim kurmayan istemcilerden gelen verileri içerir. **Uyumluluk 9 genel durumu ve uyumluluğu**olan yeni bir rapor, belirli bir yazılım güncelleştirme grubu için uyumluluk sonuçlarını "sağlıklı" istemcilere göre filtrelemenize izin verir. Bu rapor, ortamınızdaki etkin istemcilerin daha gerçekçi uyumluluk durumunu gösterir. 

Daha fazla bilgi için bkz. [yazılım güncelleştirmeleri raporları](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports).



## <a name="inventory"></a>Envanter

### <a name="improvement-to-hardware-inventory-for-large-integer-values"></a><a name="bkmk_bigint"></a> Büyük tamsayı değerleri için donanım envanterine iyileştirme
<!--1357880-->
Donanım envanteri daha önce 4.294.967.296 'den büyük tamsayılar için sınıra sahipti (2 ^ 32). Bayt cinsinden sabit sürücü boyutları gibi öznitelikler için bu sınıra ulaşılırsa. Yönetim noktası bu sınırın üstünde tamsayı değerlerini işlemedi, bu nedenle veritabanında hiçbir değer depolanmadı. Şimdi bu yayında sınır 18446744073709551616 (2 ^ 64) olarak artar. 

Daha fazla bilgi için bkz. [büyük tamsayı değerlerinin kullanımı](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Donanım envanteri varsayılan birim düzeltmesi
<!--514442-->
[Configuration Manager sürüm 1710](whats-new-in-version-1710.md#site-infrastructure)' de, birçok raporlama görünümünde kullanılan varsayılan birim MEGABAYT (MB) ila GIGABAYT (GB) olarak değiştirildi. [Büyük tamsayı değerleri için donanım envanterinde iyileştirmeler](#bkmk_bigint)ve müşteri geri bildirimlerine bağlı olarak, bu varsayılan bırım artık MB 'dir.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Configuration Manager konsolu

### <a name="product-lifecycle-dashboard"></a>Ürün yaşam döngüsü panosu
<!--1319632-->
Ürün yaşam döngüsü panosu, Configuration Manager ile yönetilen cihazlarda yüklü Microsoft ürünleri için Microsoft yaşam döngüsü Ilkesinin durumunu gösterir. Ayrıca ortamınızdaki Microsoft ürünleriyle ilgili bilgiler, desteklenebilirlik State ve bitiş tarihlerini DESTEKDE sağlar. Her ürün için desteğin kullanılabilirliğini anlamak için panoyu kullanın. Bu bilgiler, geçerli destek sonuna ulaşılmadan önce kullandığınız Microsoft ürünlerini ne zaman güncelleştirebileceğini planlamanızı sağlar.   

Daha fazla bilgi için bkz. [ürün yaşam döngüsü panosu](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="copy-asset-details-from-monitoring-views"></a>İzleme görünümlerinden varlık ayrıntılarını Kopyala
<!--1357856-->
**İzleme** çalışma alanının aşağıdaki alanlarında artık metnin kopyalanması desteklenir:  

- **Dağıtımlar** düğümünde bir dağıtım seçin ve **durumu görüntüle**' ye tıklayın. Dağıtım durumu görünümünün **varlık ayrıntıları** bölmesinde bir veya daha fazla cihaz seçin.  

- **Dağıtım durumu** düğümünü genişletin ve **İçerik durumu**' nu seçin. Bir yazılım parçası seçin ve **durumu görüntüle**' ye tıklayın. Içerik durumu görünümünün **varlık ayrıntıları** bölmesinde bir veya daha fazla dağıtım noktası seçin. 

Varlığa sağ tıklayın ve **Kopyala**' yı seçin. Bu eylem, seçili varlıkları tam ayrıntıları içeren virgülle ayrılmış bir liste olarak kopyalar. **CTRL**  +  **C** klavye kısayolu Bu görünümlerde de kullanılabilir. 

Daha fazla bilgi için bkz. [sürüm 1806 ' de konsol geliştirmeleri](../../servers/manage/admin-console-tips.md#copy-details-in-monitoring-views).


### <a name="improvements-to-the-surface-dashboard"></a>Yüzey panosu geliştirmeleri
<!--1358654-->
Bu sürüm, yüzey panosu için aşağıdaki geliştirmeleri içerir:  

- Yüzey panosu artık belirli grafik bölümlerini seçtiğinizde ilgili cihazların bir listesini görüntüler:  

   - **Surface cihazlarının yüzdesi** kutucuğuna tıkladığınızda Surface cihazlarının bir listesi açılır.  

   - **En üstteki beş bellenim** sürümü kutucuğunda bir çubuğa tıkladığınızda, bu ilgili bellenim sürümüne sahip Surface cihazlarının bir listesi açılır.  

- Bu cihaz listeleri yüzey panosundan görüntülenirken ortak eylemleri gerçekleştirmek için bir cihaza sağ tıklayın.  

Daha fazla bilgi için bkz. [yüzey panosu](../../clients/manage/surface-device-dashboard.md).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Bir cihaz için şu anda oturum açmış olan kullanıcıyı görüntüleme
<!--1358202-->
Artık varsayılan olarak, **varlıklar ve uyum** çalışma alanının **cihazlar** düğümü, **Şu anda oturum açmış olan Kullanıcı**için bir sütun görüntüler. Ayrıca, koleksiyona özgü herhangi bir cihaz listesi için de görüntülenir. Bu değer, [istemci durumu](../../clients/manage/monitor-clients.md#bkmk_indStatus)olarak geçerli olur. Kullanıcı oturumu kapattığında, istemci bu değeri temizler. Oturum açmış bir kullanıcı yoksa değer boştur. 

Daha fazla bilgi için bkz. [sürüm 1806 ' de konsol geliştirmeleri](../../servers/manage/admin-console-tips.md#view-users-for-a-device).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Configuration Manager konsolundan geri bildirim gönderin  
<!--1357542-->

Gülümseme Gönder! Artık Configuration Manager ekibine deneyimleriniz hakkında doğrudan bilgi verebilirsiniz. Geri bildirimin gönderilmesi Configuration Manager konsolundan kolaydır. Tüm geri bildirimlerinizi duymak istiyoruz: Praise, sorunlar ve öneriler. Configuration Manager konsolunda, şeridin üstündeki sağ üst köşedeki gülümseme düğmesine tıklayın. Bu geri bildirim, Configuration Manager için doğrudan Microsoft ürün ekibine gider. Windows 10 Geri Bildirim Hub 'ı kullanılırken, yine de desteklenirken konsol içi geri bildirim mekanizmasını kullanmanız önerilir.  

Daha fazla bilgi için bkz. sürüm 1806 ve [ürün geri bildirimi](../../understand/find-help.md#BKMK_1806Feedback) ['ndeki konsol geliştirmeleri](../../servers/manage/admin-console-tips.md#send-feedback) .



## <a name="other-updates"></a>Diğer güncelleştirmeler

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 1806](https://support.microsoft.com/help/4459701).

Configuration Manager için Windows PowerShell cmdlet 'lerinde yapılan değişiklikler hakkında daha fazla bilgi için bkz. [PowerShell 1806 sürüm notları](/powershell/sccm/1806_release_notes?view=sccm-ps).

Aşağıdaki güncelleştirme paketi (4462978) konsolunda 24 Ekim 2018 ' de başlayan: [güncel dalı Için güncelleştirme paketi, sürüm 1806 Configuration Manager](https://support.microsoft.com/help/4462978).


### <a name="hotfixes"></a>Düzeltmeler

Aşağıdaki ek düzeltmeler belirli sorunları ele almak için kullanılabilir:

| ID | Başlık | Tarih | Konsol içi |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Configuration Manager sürüm 1806 için güncelleştirme, ilk dalga | 31 Ağustos 2018 | Evet |
| [4465865](https://support.microsoft.com/help/4465865) | Yazılım güncelleştirmeleri, WSUS bağlantısı kesildiğinde Configuration Manager ortamda indirmez<br><br>Bu güncelleştirme ayrıca güncelleştirme paketi 'nde (4462978) | 01 Ekim 2018 | Evet |
| [4471892](https://support.microsoft.com/help/4471892) | PXE Yanıtlayıcısı Configuration Manager 1806 ' deki alt ağlarda çalışmıyor | 23 Kasım 2018 | Hayır |
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune bağlayıcı sertifikası Configuration Manager yenilemez | 18 Ocak 2019 | Evet |


## <a name="next-steps"></a>Sonraki adımlar

Bu sürümü yüklemeye hazırsanız, [güncelleştirme 1806 ' i yüklemek için](../../servers/manage/checklist-for-installing-update-1806.md) [Configuration Manager güncelleştirmeleri](../../servers/manage/updates.md) ve denetim listesini yükleme bölümüne bakın.

> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanın.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:    
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)

Bilinen, önemli sorunlar için bkz. [sürüm notları](../../servers/deploy/install/release-notes.md).

Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist)de gözden geçirin.