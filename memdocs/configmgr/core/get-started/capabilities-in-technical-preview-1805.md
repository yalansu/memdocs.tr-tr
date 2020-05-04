---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview sürüm 1805 ' de bulunan yeni özellikler hakkında bilgi edinin.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 88234bb3117850bc3280242671ae459308a5262e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714846"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Configuration Manager için Technical Preview 1805 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1805 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Technical Preview sitenize güncelleştirmek ve yeni özellikleri eklemek için yükleyebilirsiniz. 

Bu güncelleştirmeyi yüklemeden önce [Teknik Önizleme](technical-preview.md) makalesini gözden geçirin. Bu makalede, Technical Preview kullanımı, sürümler arasında nasıl güncelleştirme yapılacağı ve geri bildirimde bulunmak için genel gereksinimler ve sınırlamalar tamamladığınızda tercihinize.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Bir görev dizisi için el ile yapılandırılan aşamalarla aşamalı bir dağıtım oluşturma
<!--1358148-->
Artık, bir görev dizisi için el ile yapılandırılan aşamalarla [aşamalı bir dağıtım oluşturabilirsiniz](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) . Aşamalı dağıtım oluşturma Sihirbazı ' nın **aşamalar** sekmesinden en fazla 10 ek aşama ekleyebilirsiniz. 


### <a name="try-it-out"></a>Deneyin!
Tüm aşamaları el ile yapılandırdığınız bir aşamalı dağıtım oluşturmak için yönergeleri izleyin. Nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin. 

1. **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.  

2. Var olan bir görev dizisine sağ tıklayın ve **aşamalı dağıtım oluştur**' u seçin.  

3. **Genel** sekmesinde, aşamalı dağıtıma bir ad, açıklama (isteğe bağlı) verin ve **tüm aşamaları el ile yapılandır**' ı seçin.  

4. **Aşamalar** sekmesinde **Ekle**' ye tıklayın.  

5. Aşama için bir **ad** belirtin ve hedef **aşama koleksiyonuna**gidin.  

6. **Aşama ayarları** sekmesinde, zamanlama ayarlarının her biri için bir seçenek belirleyin ve tamamlandığında **İleri ' yi** seçin.  

    - Önceki aşamanın başarısı için ölçütler (Bu seçenek ilk aşama için devre dışıdır.)
        - **Dağıtım başarı yüzdesi**: önceki aşama başarı ölçütlerine yönelik olarak dağıtımı başarıyla tamamlayacak cihazların yüzdesini belirtin.  

    - Önceki aşamanın başarılı olduktan sonra dağıtımın bu aşamasına başlama koşulları  
        - **Bir erteleme döneminden (gün) sonra bu aşamayı otomatik olarak Başlat**: önceki aşamanın başarılı olduktan sonra sonraki aşamaya başlamadan önce beklenecek gün sayısını seçin. 
        - **Dağıtımın bu aşamasına el ile başla**: önceki aşamanın başarılı olduktan sonra bu aşamayı otomatik olarak başlatma.  

    - Bir cihaz hedeflendikten sonra yazılımı yükledikten sonra
        - **Mümkün olan en kısa sürede: cihaz hedeflendiğinde**cihaza yüklenmek üzere son tarihi ayarlar.
        - **Son tarih (cihazın hedeflediği zamana göre)**: cihaz hedeflendikten sonra yükleme son tarihini belirli bir gün sayısı olarak ayarlar.  
     
7. Aşama Ayarları Sihirbazı 'nı doldurun.

8. Aşamalı dağıtım oluşturma sihirbazının **aşamalar** sekmesinde artık bu dağıtımın aşamalarını ekleyebilir, kaldırabilir, yeniden sıralayabilir veya düzenleyebilirsiniz.  

9. Aşamalı dağıtım oluşturma Sihirbazı 'nı doldurun.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Azure Resource Manager için bulut dağıtım noktası desteği
<!--1322209-->
[Bulut dağıtım noktasının](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)bir örneğini oluştururken, sihirbaz artık **Azure Resource Manager dağıtımı**oluşturma seçeneği sağlar. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) , tüm çözüm kaynaklarının, [kaynak grubu](/azure/azure-resource-manager/resource-group-overview#resource-groups)olarak adlandırılan tek bir varlık olarak yönetilmesine yönelik modern bir platformdur. Azure Resource Manager ile bulut dağıtım noktası dağıtımında, site kimlik doğrulaması yapmak ve gerekli bulut kaynaklarını oluşturmak için Azure Active Directory (Azure AD) kullanır. Bu modernlanmış dağıtım, klasik Azure Yönetim sertifikası gerektirmez.  

Bulut dağıtım noktası Sihirbazı hala bir Azure Yönetim sertifikası kullanan **Klasik hizmet dağıtımı** için seçenek sağlar. Kaynakların dağıtımını ve yönetimini basitleştirmek için, tüm yeni bulut dağıtım noktaları için Azure Resource Manager dağıtım modelini kullanmanızı öneririz. Mümkünse, mevcut bulut dağıtım noktalarını Kaynak Yöneticisi aracılığıyla yeniden dağıtın.

Configuration Manager var olan klasik bulut dağıtım noktalarını Azure Resource Manager dağıtım modeline geçirmez. Azure Resource Manager dağıtımlarını kullanarak yeni bulut dağıtım noktaları oluşturun ve ardından klasik bulut dağıtım noktalarını kaldırın. 

> [!IMPORTANT]  
> Bu özellik, Azure bulut hizmeti sağlayıcıları (CSP) için desteği etkinleştirmez. Azure Resource Manager ile bulut dağıtım noktası dağıtımı, CSP 'nin desteklemediği klasik bulut hizmetini kullanmaya devam eder. Daha fazla bilgi için bkz. [Azure CSP 'de kullanılabilir Azure hizmetleri](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Önkoşullar  
- [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md)ile tümleştirme. Azure AD Kullanıcı keşfi gerekli değildir.  

- Azure Yönetim sertifikası haricinde [bir bulut dağıtım noktası için aynı gereksinimler](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements).  


### <a name="try-it-out"></a>Deneyin!  
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda, **Yönetim** çalışma alanında, **Cloud Services**' ı genişletin ve **bulut dağıtım noktaları**' nı seçin. Şeritte **bulut dağıtım noktası oluştur** ' a tıklayın.   

2. **Genel** sayfasında, **Azure Resource Manager dağıtımı**' nı seçin. Azure abonelik yönetici hesabıyla kimlik doğrulamak için **oturum aç** ' a tıklayın. Sihirbaz, geri kalan alanları tümleştirme önkoşulu sırasında depolanan Azure AD abonelik bilgilerini otomatik olarak doldurur. Birden çok aboneliğiniz varsa, kullanılacak istediğiniz aboneliği seçin. **İleri**’ye tıklayın.  

3. **Ayarlar** sayfasında, sunucu PKI **sertifika dosyasını** her zamanki gibi sağlayın. Bu sertifika, Azure tarafından kullanılan bulut dağıtım noktası **HIZMETI FQDN** 'sini tanımlar. **Bölgeyi**seçin ve ardından **Yeni oluştur** veya **mevcut olanı kullan**' ı seçerek bir kaynak grubu seçeneğini belirleyin. Yeni kaynak grubu adını girin veya açılan listeden var olan bir kaynak grubunu seçin.  

4. Sihirbazı tamamlayın.  

> [!NOTE]  
> Seçili Azure AD Server uygulaması için, Azure abonelik **katılımcısı** iznini atar.  

Hizmet bağlantı noktasındaki **CloudMgr. log** ile hizmet dağıtımı ilerlemesini izleyin.



## <a name="take-actions-based-on-management-insights"></a>Yönetim öngörülerine göre eylemler gerçekleştirin
<!--1357930-->
Bazı [Yönetim öngörüleri](../servers/manage/management-insights.md) artık bir eylem alma seçeneğine sahiptir. Kurala bağlı olarak, bu eylem aşağıdaki davranışlardan birini sergiler:  

- Konsolda daha fazla işlem gerçekleştirebileceğiniz düğüme otomatik olarak gidin. Örneğin, yönetim öngörüleri bir istemci ayarının değiştirilmesini önerse, işlem gerçekleşmesi Istemci ayarları düğümüne gider. Varsayılan veya özel bir istemci ayarları nesnesini değiştirerek daha fazla işlem yapabilirsiniz.  

- Sorgu temelinde filtrelenmiş görünüme gidin. Örneğin, boş koleksiyonlar kuralında işlem gerçekleştirmek koleksiyonlar listesinde yalnızca bu koleksiyonları gösterir. Burada, bir koleksiyonu silme veya üyelik kurallarını değiştirme gibi işlemleri gerçekleştirebilirsiniz.  

Aşağıdaki yönetim öngörüleri kuralları bu sürümde eylemlere sahiptir:
- Güvenlik
    - Desteklenmeyen kötü amaçlı yazılımdan koruma istemci sürümleri
- Yazılım Merkezi
    - Yazılım Merkezi 'nin yeni sürümünü kullan
- Uygulamalar
    - Dağıtımlar olmadan uygulamalar
- Basitleştirilmiş Yönetim
    - CB olmayan Istemci sürümleri
- Koleksiyonlar
    - Boş Koleksiyonlar 
- Cloud Services
    - İstemcileri en son Windows 10 sürümüne güncelleştirme



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Ortak yönetim kullanarak cihaz yapılandırma iş yükünü Intune 'a geçirme
<!--1357903-->

Artık ortak yönetimi etkinleştirdikten sonra cihaz yapılandırma iş yükünü Configuration Manager 'den Intune 'a geçiş yapabilirsiniz. Bu iş yükünü dengelemek, uygulamaları dağıtmak için Configuration Manager kullanmaya devam ederken MDM ilkelerini dağıtmak için Intune 'U kullanmanıza olanak sağlar. 

Bu iş yükünü dengelemek için ortak yönetim özellikleri sayfasına gidin ve kaydırıcı çubuğunu Configuration Manager 'den **pilot** 'A veya **tümüne**taşıyın. Daha fazla bilgi için bkz. [Windows 10 cihazlar Için ortak yönetim](../../comanage/overview.md).

> [!Note]  
> Bu iş yükünü taşımak Ayrıca, cihaz yapılandırması iş yükünün bir alt kümesi olan **kaynak erişimini** ve **Endpoint Protection** iş yüklerini taşır.

Bu iş yükünü geçirdiğinde, Intune 'un cihaz yapılandırma yetkilisi olmasına rağmen Configuration Manager ayarları ortak yönetilen cihazlara dağıtabilirsiniz. Bu özel durum, kuruluşunuz için gereken ancak henüz Intune 'da kullanılamayan ayarları yapılandırmak için kullanılabilir. Bu özel durumu bir Configuration Manager yapılandırma temeli üzerinde belirtin. Temeli oluştururken veya var olan bir taban çizgisinin özelliklerinin **genel** sekmesinde, **Bu temeli her zaman ortak yönetilen istemciler için de uygulama** seçeneğini etkinleştirin. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Ağ tıkanıklık denetimini kullanmak için dağıtım noktalarını etkinleştir
<!--1358112-->

Windows düşük ekstra gecikmeli arka plan taşıması (LEDBAT), arka plan ağ aktarımlarının yönetilmesine yardımcı olmak için Windows Server 'ın bir özelliğidir. Desteklenen Windows Server sürümlerinde çalışan dağıtım noktaları için, ağ trafiğini ayarlamanıza yardımcı olacak bir seçenek belirleyebilirsiniz. İstemciler yalnızca kullanılabilir olduğunda ağ bant genişliğini kullanır. 

Windows LEDBAT hakkında daha fazla bilgi için [yeni aktarım](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) geliştirmeleri blog gönderisine bakın.


### <a name="prerequisites"></a>Önkoşullar
- Windows Server, sürüm 1709 üzerinde bir dağıtım noktası.  

- İstemci önkoşulu yok.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Dağıtım noktaları** düğümünü seçin. Hedef dağıtım noktasını seçin ve Şeritteki **Özellikler** ' e tıklayın.  

2. **Genel** sekmesinde, **kullanılmayan ağ bant GENIŞLIĞINI (Windows ledbat) kullanmak Için indirme hızını ayarlama**seçeneğini etkinleştirin.  



## <a name="cloud-management-dashboard"></a>Bulut yönetimi panosu
<!--1358461-->
Yeni **bulut yönetimi panosu** , bulut yönetimi ağ geçidi (CMG) kullanımı için merkezi bir görünüm sağlar. Site, Azure AD ile eklendi olduğunda, bulut kullanıcıları ve cihazları hakkındaki verileri de görüntüler.  

Aşağıdaki ekran görüntüsü, kullanılabilir kutucukların ikisini gösteren bulut yönetimi panosunun bir bölümüdür:  
![Bulut yönetimi Pano kutucukları CMG trafiği ve geçerli çevrimiçi istemcileri](media/1358461-cmg-dashboard.png)

Bu özellik ayrıca sorun gidermeye yardımcı olmak üzere gerçek zamanlı doğrulama için **CMG bağlantı çözümleyici** 'yi içerir. Konsol içi yardımcı programı hizmetin geçerli durumunu ve CMG bağlantı noktası üzerinden gelen iletişim kanalını CMG trafiğine izin veren herhangi bir yönetim noktasına denetler.


### <a name="prerequisites"></a>Önkoşullar
- Internet tabanlı istemciler tarafından kullanılan etkin bir [bulut yönetimi ağ geçidi](../clients/manage/cmg/plan-cloud-management-gateway.md) .  

- Site, bulut yönetimi için [Azure hizmetlerine](../servers/deploy/configure/azure-services-wizard.md) eklendi.  


### <a name="try-it-out"></a>Deneyin!
Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

#### <a name="cloud-management-dashboard"></a>Bulut yönetimi panosu

Configuration Manager konsolunda **izleme** çalışma alanına gidin. **Bulut yönetimi** düğümünü seçin ve Pano kutucuklarını görüntüleyin.  

#### <a name="cmg-connection-analyzer"></a>CMG bağlantı Çözümleyicisi

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Cloud Services** genişletin ve **bulut yönetimi ağ geçidi**' ni seçin.  

2. Hedef CMG örneğini seçin ve ardından şeritte **bağlantı Çözümleyicisi** ' ni seçin.  

3. CMG bağlantı çözümleyici penceresinde, hizmet ile kimlik doğrulamak için aşağıdaki seçeneklerden birini belirleyin:  

     1. **Azure AD kullanıcısı**: Azure AD 'ye katılmış bir Windows 10 cihazında oturum açmış bulut tabanlı bir kullanıcı kimliğiyle iletişimin benzetimini yapmak için bu seçeneği kullanın. Bu Azure AD Kullanıcı hesabının kimlik bilgilerini güvenli bir şekilde girmek için **oturum aç** ' a tıklayın.  

     2. **İstemci sertifikası**: [istemci kimlik doğrulama sertifikasıyla](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth)Configuration Manager istemcisiyle aynı iletişimin benzetimini yapmak için bu seçeneği kullanın.  

4. Çözümlemeyi başlatmak için **Başlat** ' a tıklayın. Sonuçlar çözümleyici penceresinde görüntülenir. Açıklama alanında daha fazla ayrıntı görmek için bir giriş seçin.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager, müşterilerin raporlama amacıyla kullanacağı, cihaz verilerinin büyük merkezi bir deposunu sağlamıştır. Ancak, bu veriler yalnızca istemcilerden en son toplandığında iyi olur. 

CMPivot, ortamınızdaki cihazların gerçek zamanlı durumuna erişim sağlayan yeni bir konsol içi yardımcı programdır. Hedef koleksiyondaki Şu anda bağlı olan tüm cihazlarda bir sorguyu hemen çalıştırır ve sonuçları döndürür. Daha sonra bu verileri, araçta filtreleyebilir ve gruplandırabilirsiniz. Çevrimiçi istemcilerden gerçek zamanlı veriler sunarak, iş sorularını daha hızlı bir şekilde yanıtlayabilir, sorun giderebilir ve güvenlik olaylarına yanıt verebilirsiniz.

Örneğin, [kurgusal yürütme tarafı kanalı güvenlik açıklarını azaltıcı](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)bir şekilde, gereksinimlerden biri sistem BIOS 'unu güncelleştirmelerdir. CMPivot kullanarak sistem BIOS bilgilerini hızlı bir şekilde sorgulayabilir ve uyumlu olmayan istemcileri bulabilirsiniz. 

Bu ekran görüntüsünde, CMPivot her birinin cihaz sayısıyla iki ayrı BIOS sürümü görüntüler. CMPivot çalıştığınızda bu örnek sorguyu kullanabilirsiniz:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![Örnek CMPivot bir pencere testten biosversion](media/1358456-cmpivot-biosversion.png)

Belirli cihazları görmek için ayrıntılara gitmek üzere cihaz sayısına tıklayabilirsiniz. Cihazları CMPivot ' de görüntülerken, bir cihaza sağ tıklayıp aşağıdaki [İstemci bildirimi eylemlerini](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)seçebilirsiniz:
- Betiği Çalıştır
- Uzaktan Denetim
- Kaynak Gezgini

Belirli bir cihaza sağ tıklandığında, belirli bir cihazın görünümünü aşağıdaki özniteliklerden birine de özetleyebilirsiniz.
- Autostart komutları
- Yüklü ürünler
- İşlemler
- Hizmetler
- Kullanıcılar
- Etkin bağlantılar
- Eksik güncelleştirmeler

### <a name="prerequisites"></a>Önkoşullar
- Hedef istemciler en son sürüme güncelleştirilmeleri gerekir.  

- Configuration Manager yöneticisinin betikleri çalıştırmak için izinleri olması gerekir. Daha fazla bilgi için bkz. [betikler Için güvenlik rolleri](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Deneyin!
Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Cihaz Koleksiyonları**' nı seçin. Bir hedef koleksiyon seçin ve aracı başlatmak için Şeritteki **CMPivot Başlat** ' a tıklayın.  

2. Arabirim, aracı kullanma hakkında daha fazla bilgi sağlar. 
     - En üst kısımdaki Sorgu dizelerini el ile girebilir veya çevrimiçi belgelerdeki bağlantılara tıklayabilirsiniz.
     - Sorgu dizesine eklemek için **varlıklardan** birine tıklayın. 
     - **Tablo işleçleri**, **toplama Işlevleri**ve **skaler işlevler** bağlantıları, Web tarayıcısında dil başvurusu belgelerini açar. CMPivot, [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/)ile aynı sorgu dilini kullanır.



## <a name="improved-secure-client-communications"></a>Gelişmiş güvenli istemci iletişimleri
<!--1356889,1358228,1358460-->
HTTPS iletişimini kullanmak tüm Configuration Manager iletişim yollarında önerilir, ancak PKI sertifikalarını yönetme yükü nedeniyle bazı müşteriler için zor olabilir. Azure Active Directory (Azure AD) Tümleştirmesi 'nin tanıtımı, sertifika gereksinimlerinin tümünü değil, bazılarını azaltır. 

Bu sürüm, istemcilerin site sistemleriyle iletişim kurmasına yönelik iyileştirmeler içerir. Bu geliştirmelerin iki birincil hedefi vardır:  

- PKI sunucusu kimlik doğrulama sertifikalarına gerek olmadan istemci iletişimini güvenli hale getirebilirsiniz.  

- İstemciler, bir ağ erişim hesabına gerek duymadan dağıtım noktalarından içeriğe güvenli bir şekilde erişebilir.  

> [!Note]  
> PKI sertifikaları, kullanmak isteyen müşteriler için de geçerli bir seçenektir.  


### <a name="scenarios"></a><a name="bkmk_token"></a>Larla
Aşağıdaki senaryolar bu geliştirmelerden faydalanır:  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a>Senaryo 1: Istemciden yönetim noktasına
<!--1356889-->
[Azure AD 'ye katılmış cihazlar](/azure/active-directory/devices/concept-azure-ad-join) , http için yapılandırılmış bir yönetim noktasıyla bir bulut yönetimi ağ geçidi (CMG) üzerinden iletişim kurabilir. Site sunucusu yönetim noktası için güvenli bir kanal üzerinden iletişim kurmasına izin veren bir sertifika oluşturur.   

> [!Note]  
> Bu davranış, bu senaryo için HTTPS özellikli bir yönetim noktası gerektiren geçerli Configuration Manager dalı sürümü 1802 ' den değiştirilir. Daha fazla bilgi için bkz. [https için yönetim noktasını etkinleştirme](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a>Senaryo 2: Istemciden dağıtım noktasına
<!--1358228-->
Bir çalışma grubu veya Azure AD 'ye katılmış istemci, HTTP için yapılandırılmış bir dağıtım noktasından güvenli bir kanal üzerinden içerik indirebilir.   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a>Senaryo 3 Azure AD cihaz kimliği 
<!--1358460-->
Azure AD Kullanıcı oturumu olmayan bir Azure AD 'ye katılmış veya [hibrit Azure AD cihazı](/azure/active-directory/devices/concept-azure-ad-join-hybrid) , atanan sitesiyle güvenli bir şekilde iletişim kurabilir. Bulut tabanlı cihaz kimliği artık CMG ve yönetim noktasıyla kimlik doğrulaması için yeterlidir.  


### <a name="prerequisites"></a>Önkoşullar  

- HTTP istemci bağlantıları için yapılandırılmış bir yönetim noktası. Bu seçeneği, site sistemi rolü özelliklerinin **genel** sekmesinde ayarlayın.  

- HTTP istemci bağlantıları için yapılandırılmış bir dağıtım noktası. Bu seçeneği, site sistemi rolü özelliklerinin **genel** sekmesinde ayarlayın. **İstemcilerin anonim olarak bağlanmasına Izin ver**seçeneğini etkinleştirmeyin.  

- Bulut yönetimi ağ geçidi.  

- Siteyi, bulut yönetimi için Azure AD 'ye ekleyin.  

    - Siteniz için bu önkoşulu zaten karşıladıysanız Azure AD uygulamasını güncelleştirmeniz gerekir. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure Active Directory kiracılar**' ı seçin. Azure AD kiracısını seçin, **uygulamalar** bölmesinde Web uygulamasını seçin ve ardından Şeritteki **uygulama ayarını Güncelleştir** ' e tıklayın.  

- Windows 10 sürüm 1803 çalıştıran ve Azure AD 'ye katılmış bir istemci. (Bu gereksinim Teknik olarak yalnızca [Senaryo 3](#bkmk_token3)için geçerlidir.) 


### <a name="try-it-out"></a>Deneyin!
Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler**' i seçin. Siteyi seçin ve Şeritteki **Özellikler** ' e tıklayın.  

2. **Istemci bilgisayar iletişimi** sekmesine geçin. **https veya http** seçeneğini belirleyin ve ardından yeni seçeneği **http site sistemleri Için Configuration Manager tarafından oluşturulan sertifikaları kullanma**seçeneğini etkinleştirin.  

Doğrulanacak [senaryolar listesine](#bkmk_token) bakın.

> [!Tip]
> Bu sürümde, yönetim noktasının siteden yeni sertifikayı alması ve yapılandırması için 30 dakikaya kadar bekleyin.

Bu sertifikaları Configuration Manager konsolunda görebilirsiniz. **Yönetim** çalışma alanına gidin, **güvenlik**' i genişletin ve **Sertifikalar** düğümünü seçin. SMS **veren kök sertifikayı** ve SMS veren kök tarafından verilen site sunucusu rolü sertifikalarını bulun.


### <a name="known-issues"></a>Bilinen sorunlar
- Kullanıcı, yazılım merkezi 'nde bunları hedeflenen tüm uygulamaları kullanılabilir olarak görüntüleyemez.  

- İşletim sistemi dağıtım senaryolarında ağ erişim hesabı hala gereklidir.  

- **Http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanma** seçeneğini hızlı ve sürekli olarak etkinleştirme ve devre dışı bırakma, sertifikanın site sistem rollerine düzgün şekilde bağlanmamasına neden olabilir. "SMS verme" sertifikası tarafından verilen sertifika, Windows Server Internet Information Services (IIS) içindeki bir Web sitesine bağlanır. Bu sorunu geçici olarak çözmek için Windows 'daki **SMS** sertifika DEPOSUNDAN "SMS verme" tarafından verilen tüm sertifikaları silin ve ardından Smsexec hizmetini yeniden başlatın.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Üçüncü taraf yazılım güncelleştirme desteğini etkinleştirmeye yönelik iyileştirmeler
<!--1357605-->
[Üçüncü taraf yazılım güncelleştirme desteğiyle](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)ilgili UserVoice geri bildirimlerinizin bir sonucu olarak, bu sürüm System Center Updates Publisher (scup) Tümleştirmesi üzerinde daha da yinelenir. Configuration Manager Technical Preview [sürüm 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) , üçüncü taraf GÜNCELLEŞTIRMELER için WSUS 'tan sertifikayı okuma ve ardından bu sertifikayı istemcilere dağıtma özelliğini ekledi. Ancak yine de, üçüncü taraf yazılım güncelleştirmelerini imzalamak için sertifika oluşturmak ve yönetmek üzere SCUP aracını kullanmanız gerekir.

Bu sürümde, Configuration Manager sitesinin sertifikayı otomatik olarak yapılandırmasını sağlayabilirsiniz. Site, bu amaçla bir sertifika oluşturmak için WSUS ile iletişim kurar. Configuration Manager daha sonra bu sertifikayı istemcilere dağıtmaya devam eder. Bu yineleme, sertifikayı oluşturmak ve yönetmek için SCUP aracını kullanma gereksinimini ortadan kaldırır. 

SCUP aracının genel kullanımı hakkında daha fazla bilgi için bkz. [System Center Updates Publisher](../../sum/tools/updates-publisher.md).

### <a name="prerequisites"></a>Önkoşullar
- İstemci ayarını etkinleştirin ve dağıtın **yazılım güncelleştirmeleri** grubundaki **üçüncü taraf yazılım güncelleştirmelerini etkinleştirin** .
- WSUS, yazılım güncelleştirme noktasındaki ayrı bir sunucu üzerinde bulunuyorsa, uzak WSUS sunucusunda aşağıdaki seçeneklerden birini yapmanız gerekir:
    - Windows 'da uzak kayıt defteri hizmetini etkinleştirme  
    or
    - Kayıt defteri anahtarında `HKLM\Software\Microsoft\Update Services\Server\Setup`, bir değeri olan **Enableselfsignedcertificates** adlı yeni bir DWORD oluşturun `1`. 

### <a name="try-it-out"></a>Deneyin!
Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması** ' nı genişletin ve **siteler**' i seçin. Üst düzey siteyi seçin, Şeritteki **site bileşenlerini Yapılandır** ' a tıklayın ve **yazılım güncelleştirme noktası**' nı seçin.  

2. **Üçüncü taraf güncelleştirmeleri** sekmesine geçin. **üçüncü taraf yazılım güncelleştirmelerini etkinleştirme**seçeneğini belirleyin ve ardından **Configuration Manager, sertifikayı otomatik olarak yönetme**seçeneğini belirleyin.

3. Üçüncü taraf yazılım güncelleştirme kataloğunu içeri aktarmak için tipik bir artırma iş akışının geri kalanı ile devam edin ve ardından güncelleştirmeleri istemcilere dağıtın.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 yerinde yükseltme görev dizisinde iyileştirmeler
<!--1358500-->

Windows 10 yerinde yükseltme için varsayılan görev sırası şablonu, yükseltme işleminin başarısız olması durumunda eklemek için önerilen eylemleri içeren başka bir yeni grup içerir. Bu eylemler, sorun gidermeyi kolaylaştırır.

### <a name="new-groups-under-run-actions-on-failure"></a>**Hata durumunda çalıştırma eylemleri** altındaki yeni gruplar
- **Günlükleri topla**: istemciden günlükleri toplamak için bu gruba adımlar ekleyin. 
    - Ortak bir uygulama, günlük dosyalarını bir ağ paylaşımında kopyalamadır. Bu bağlantıyı kurmak için, [ağ klasörüne Bağlan](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) adımını kullanın. 
    - Kopyalama işlemini gerçekleştirmek için [komut satırı Çalıştır](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) veya [PowerShell Betiği Çalıştır](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) adımla özel bir betik veya yardımcı program kullanın.
    - Toplanacak dosyalar aşağıdaki günlükleri içerebilir:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Setupact. log ve diğer Windows Kurulumu günlükleri hakkında daha fazla bilgi için bkz. [Windows Kurulumu günlük dosyaları](/windows/deployment/upgrade/log-files).
    - Configuration Manager istemci günlükleri hakkında daha fazla bilgi için bkz. [Configuration Manager istemci günlükleri](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs)
    - _SMSTSLogPath ve diğer yararlı değişkenler hakkında daha fazla bilgi için bkz. [görev dizisi yerleşik değişkenleri](../../osd/understand/task-sequence-variables.md)

- **Tanılama araçlarını Çalıştır**: ek tanılama araçları çalıştırmak için bu gruba adımlar ekleyin. Bu araçlar, mümkün olduğunca kısa sürede sistemden daha fazla bilgi toplamak için otomatikleştirilir.
    - Bu tür bir araç Windows [Setupdiag](/windows/deployment/upgrade/setupdiag)'dir. Bu, Windows 10 yükseltmesinin neden başarısız olduğuna ilişkin ayrıntıları almak için kullanabileceğiniz tek başına bir tanılama aracıdır.
         - Configuration Manager, araç için [bir paket oluşturun](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) .
         - Görev sıralarınızın bu grubuna [komut satırı Çalıştır](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) adımı ekleyin. Araca başvurmak için **paket** seçeneğini kullanın. Aşağıdaki dize örnek bir **komut satırı**örneğidir:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>İstemci ile CMTrace yüklendi
<!--1357971-->

CMTrace günlük görüntüleme aracı artık Configuration Manager istemcisiyle birlikte otomatik olarak yüklenir. Bu, varsayılan olarak olan istemci yükleme dizinine eklenir `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> CMTrace,. log dosya uzantısını açmak için Windows 'a otomatik olarak kayıtlı *değildir* .



## <a name="improvement-to-the-configuration-manager-console"></a>Configuration Manager konsoluna iyileştirme
<!--1358202-->
Configuration Manager konsoluna aşağıdaki geliştirmeyi yaptık:

- Artık varsayılan olarak şu anda oturum açmış olan kullanıcıyı görüntüleyen varlıklar ve uyumluluk altındaki cihaz listeleri. Bu değer, [istemci durumu](../clients/manage/monitor-clients.md#bkmk_indStatus)olarak geçerli olur. Kullanıcı oturumu kapattığında değer temizlenir. Oturum açmış bir kullanıcı yoksa değer boştur. 

### <a name="known-issues"></a>Bilinen sorunlar
Şu anda oturum açmış olan kullanıcı değeri, cihazlar düğümünde veya Cihaz Koleksiyonları düğümü altında bir cihaz listesi görüntülenirken boştur. Bu sorunu geçici olarak çözmek için bu [SQL betiğini](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c)indirin. Site veritabanı sunucusunda sp_BgbUpdateLiveData. SQL ' i çalıştırın ve ardından Yönetim noktasındaki Smsexec ve sms_notification_server hizmetlerini yeniden başlatın.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Konsol geri bildirimlerine yönelik iyileştirmeler
<!--1357542-->
Bu sürüm, Configuration Manager konsolundaki Yeni [görüş](capabilities-in-technical-preview-1804.md#bkmk_feedback) mekanizmasına yönelik aşağıdaki geliştirmeleri içerir:  

- Geri bildirim iletişim kutusu artık, seçilen seçenekler ve e-posta adresiniz gibi önceki ayarları anımsar.  

- Artık çevrimdışı geri bildirimi desteklemektedir. Konsolunuzun geri bildiriminizi kaydedin ve ardından İnternet 'e bağlı bir sistemden Microsoft 'a yükleyin. İçinde `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`bulunan yeni çevrimdışı geri bildirim yükleyicisi aracını kullanın. Kullanılabilir ve gerekli komut satırı seçeneklerini görmek için aracını `--help` seçeneğiyle çalıştırın. Bağlı sistemin **petrol.Office.Microsoft.com**için erişimi olması gerekir.

### <a name="known-issues"></a>Bilinen sorunlar
İnternet bağlantısı olan bir makinede bir **gülümseme Gönder** veya konsolundan bir **kaş çatma Gönder** ' i kullanırken şu iletiyle birlikte dönebilir: "geri bildirim gönderme hatası." **Daha fazla ayrıntıya**tıkladığınızda şu metni gösterir: `{"Message":""}`. Bu hata, arka uç geri bildirim sisteminden gelen yanıttaki bilinen bir sorundan kaynaklanır. Hatayı kapatabilirsiniz. Microsoft geri bildirimlerinizi hala aldı. (Ayrıntılar farklı bir ileti görüntüleriz, geri bildirimlerinizi daha sonra göndermeyi yeniden denemek için çevrimdışı geri bildirim seçeneğini kullanın.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>PXE 'yi destekleyen dağıtım noktalarında iyileştirmeler
<!--1357580-->

Bu sürüm, bir dağıtım noktasında [**Windows dağıtım hizmeti olmayan BIR PXE Yanıtlayıcının etkinleştirilmesi**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) için seçeneğini kullandığınızda aşağıdaki ek geliştirmeleri içerir:  

- Bu seçeneği etkinleştirdiğinizde, dağıtım noktasında Windows güvenlik duvarı kuralları otomatik olarak oluşturulur  
- Bileşen günlüğe kaydetme geliştirmeleri



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Büyük tamsayı değerleri için donanım envanterine iyileştirme
<!--1357880-->
Donanım envanterinde Şu anda 4.294.967.296 'den büyük tamsayılar sınırı vardır (2 ^ 32). Bu sınıra, sabit sürücü boyutları gibi öznitelikler için bayt cinsinden ulaşılabilir. Yönetim noktası bu sınırın üzerindeki tamsayı değerlerini işlemez, bu nedenle veritabanında hiçbir değer depolanmaz. Şimdi bu yayında sınır 18446744073709551616 (2 ^ 64) olarak artar. 

Toplam disk boyutu gibi değişmeyen bir değer içeren bir özellik için, siteyi yükselttikten sonra değeri hemen görmeyebilirsiniz. Çoğu donanım envanteri bir Delta rapordur. İstemci yalnızca değişen değerleri gönderir. Bu davranışı geçici olarak çözmek için, aynı sınıfa başka bir özelliği ekleyin. Bu eylem, istemcinin değiştirilen sınıftaki tüm özellikleri güncelleştirmesine neden olur. 



## <a name="improvement-to-wsus-maintenance"></a>WSUS bakım geliştirmesi
<!--1357898-->

WSUS Temizleme Sihirbazı artık geçmiş veya yenisiyle değiştirilen güncelleştirmeleri yenisiyle değiştirme kurallarına göre reddeder. Bu kurallar, yazılım güncelleştirme noktası bileşen özellikleri üzerinde tanımlanmıştır.

### <a name="try-it-out"></a>Deneyin!
Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması** ' nı genişletin ve **siteler**' i seçin. Üst düzey siteyi seçin, Şeritteki **site bileşenlerini Yapılandır** ' a tıklayın ve **yazılım güncelleştirme noktası**' nı seçin.  

2. **Yerine geçme kuralları** sekmesine geçIn. **WSUS Temizleme Sihirbazı 'Nı çalıştırma**seçeneğini etkinleştirin. İstenen yenisiyle değiştirme davranışını belirtin.  

3. WSyncMgr. log dosyasını gözden geçirin.



## <a name="improvement-to-support-for-cng-certificates"></a>CNG sertifikaları için destek geliştirme
<!--1357314-->
Bu sürümde, aşağıdaki ek HTTPS etkin sunucu rolleri için [CNG sertifikalarını](../plan-design/network/cng-certificates-overview.md) kullanın:  
- Configuration Manager ilkesi modülüyle NDES sunucusu dahil olmak üzere sertifika kayıt noktası



## <a name="next-steps"></a>Sonraki adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).    
