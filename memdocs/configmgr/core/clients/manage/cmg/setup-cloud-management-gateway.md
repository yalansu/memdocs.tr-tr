---
title: Bulut yönetimi ağ geçidini kurma
titleSuffix: Configuration Manager
description: Bir bulut yönetimi ağ geçidi (CMG) ayarlamak için bu adım adım işlemi kullanın.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 8c585473ec80ad4c6dfe49d22e527e99175bfbb4
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877425"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configuration Manager için bulut yönetimi ağ geçidi ayarlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu işlem, bir bulut yönetimi ağ geçidi (CMG) ayarlamak için gerekli olan adımları içerir.

> [!Note]  
> Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="before-you-begin"></a>Başlamadan önce

[Bulut yönetimi ağ geçidi için makale planını](plan-cloud-management-gateway.md)okuyarak başlayın. CMG tasarımınızı öğrenmek için bu makaleyi kullanın.

Bir CMG oluşturmak için gerekli bilgilere ve önkoşullara sahip olduğunuzdan emin olmak için aşağıdaki denetim listesini kullanın:  

- Kullanılacak Azure ortamı. Örneğin, Azure genel bulutu veya Azure ABD kamu bulutu.  

- Tasarımınıza bağlı olarak CMG için bir veya daha fazla sertifikaya ihtiyacınız vardır. Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidi Için sertifikalar](certificates-for-cloud-management-gateway.md).  

- CMG 'nin [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) dağıtımı için aşağıdaki gereksinimlere ihtiyacınız vardır:  

    - **Bulut yönetimi**IÇIN [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) ile tümleştirme. Azure AD Kullanıcı keşfi gerekli değildir.  

    - **Microsoft. classiccompute**  &  **Microsoft. Storage** kaynak sağlayıcılarının Azure aboneliği içinde kayıtlı olması gerekir. Daha fazla bilgi için bkz. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services).

    - Abonelik yöneticisinin oturum açması gerekir.  

- Hizmet için genel olarak benzersiz bir ad. Bu ad [CMG sunucusu kimlik doğrulama sertifikasıdır](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- CMG 'yi bulut dağıtım noktası olarak etkinleştirirseniz, aynı zamanda seçilen aynı genel benzersiz CMG hizmeti adının genel olarak benzersiz bir depolama hesabı adı olarak kullanılabilir olması gerekir. Bu ad [CMG sunucusu kimlik doğrulama sertifikasıdır](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- Bu CMG dağıtımının Azure bölgesi.  

- Ölçek ve artıklık için kaç tane VM örneğine ihtiyacınız vardır.  

- Hala Configuration Manager sürüm 1810 veya önceki sürümlerde klasik Azure hizmet dağıtımını kullanmanız gerekiyorsa, aşağıdaki gereksinimlere ihtiyacınız vardır:  

    > [!Important]  
    > Sürüm 1810 ' den başlayarak, Azure 'da klasik hizmet dağıtımları Configuration Manager kullanım dışıdır. Bulut yönetimi ağ geçidi için Azure Resource Manager dağıtımlarını kullanın. Daha fazla bilgi için [plan for CMG](plan-cloud-management-gateway.md#azure-resource-manager)konusuna bakın.  
    >
    > Configuration Manager sürüm 1902 ' den başlayarak, bulut yönetimi ağ geçidinin yeni örnekleri için tek dağıtım mekanizmasıdır Azure Resource Manager.<!-- 3605704 -->

    - Azure abonelik KIMLIĞI  

    - Azure Yönetim sertifikası  


## <a name="set-up-a-cmg"></a>CMG 'yi ayarlama

Bu yordamı en üst düzey sitede yapın. Bu site tek başına bir birincil site ya da merkezi yönetim sitesi.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **bulut yönetimi ağ geçidi**' yı seçin.  

2. Şeritte **bulut yönetimi ağ geçidi oluştur** ' u seçin.  

3. Sihirbazın Genel sayfasında **oturum aç**' ı seçin. Azure abonelik yönetici hesabıyla kimlik doğrulaması yapın. Sihirbaz, kalan alanları Azure AD tümleştirme önkoşulu sırasında depolanan bilgilerden otomatik olarak doldurur. Birden çok aboneliğiniz varsa, kullanılacak istenen aboneliğin **ABONELIK kimliğini** seçin.

    > [!Note]  
    > Sürüm 1810 ' den başlayarak, Azure 'daki klasik hizmet dağıtımları Configuration Manager kullanım dışıdır. Sürüm 1902 ve önceki sürümlerde, CMG dağıtım yöntemi olarak **Azure Resource Manager dağıtımı** ' nı seçin.
    >
    > Klasik hizmet dağıtımı kullanmanız gerekiyorsa, bu sayfada bu seçeneği belirleyin. İlk olarak Azure **ABONELIK kimliğinizi**girin. Ardından, **Araştır**' ı seçin ve öğesini seçin. Azure Yönetim sertifikası için PFX dosyası.

4. Bu CMG için **Azure ortamını** belirtin. Açılan listedeki seçenekler dağıtım yöntemine bağlı olarak değişiklik gösterebilir.  

5. **İleri**’yi seçin. Site Azure bağlantısını test etmek için bekleyin.  

6. Sihirbazın Ayarlar sayfasında, önce **Araştır** ' ı seçin ve öğesini seçin. CMG sunucusu kimlik doğrulama sertifikası için PFX dosyası. Bu sertifikadaki ad, gerekli **hizmet FQDN 'si** ve **hizmet adı** alanlarını doldurur.  

   > [!NOTE]  
   > CMG sunucusu kimlik doğrulama sertifikası joker karakterleri destekler. Joker karakter sertifikası kullanıyorsanız, `*` **hizmet FQDN 'si** alanındaki yıldız işaretini () CMG için istenen konak adı ile değiştirin.<!--491233-->  

7. Bu CMG için Azure bölgesini seçmek üzere **bölge** açılan listesini seçin.  

8. Bir **kaynak grubu** seçeneği belirleyin.
   1. **Mevcut olanı kullan**' ı seçerseniz, açılan listeden var olan bir kaynak grubunu seçin. Seçili kaynak grubu, adım 7 ' de seçtiğiniz bölgede zaten var olmalıdır. Var olan bir kaynak grubunu seçerseniz ve bu bölge daha önce seçilen bölgeden farklı bir bölgedeyse CMG sağlanması başarısız olur.
   2. **Yeni oluştur**' u seçerseniz, yeni kaynak grubu adını girin.

9. **VM örneği** alanında, bu hizmet için VM sayısını girin. Varsayılan değer bir, ancak CMG başına 16 VM 'ye kadar ölçeklendirebilirsiniz.  

10. İstemci güvenilen kök sertifikaları eklemek için **Sertifikalar** ' ı seçin. Güven zincirindeki tüm sertifikaları ekleyin.  

    > [!Note]  
    > Sürüm 1806 ' den başlayarak, bir CMG oluşturduğunuzda, artık ayarlar sayfasında güvenilen bir kök sertifikası sağlamanız gerekmez. İstemci kimlik doğrulaması için Azure Active Directory (Azure AD) kullanılırken bu sertifika gerekli değildir, ancak sihirbazda gerekli olması için kullanılır. PKI istemci kimlik doğrulama sertifikaları kullanıyorsanız, yine de CMG 'ye bir güvenilen kök sertifika eklemeniz gerekir.<!--SCCMDocs-pr issue #2872-->  
    >
    > Sürüm 1902 ve önceki sürümlerde yalnızca iki güvenilen kök CA ve dört ara (alt) CA ekleyebilirsiniz.<!-- SCCMDocs-pr#4022 -->

11. Varsayılan olarak, sihirbaz **Istemci sertifikası Iptalini doğrulama**seçeneğini sağlar. Bu doğrulamanın çalışması için bir sertifika iptal listesinin (CRL) herkese açık bir şekilde yayımlanması gerekir. Daha fazla bilgi için bkz. [sertifika iptal listesini yayımlama](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. Sürüm 1906 ' den başlayarak **TLS 1,2**' yi zorlayabilirsiniz. Bu ayar yalnızca Azure bulut hizmeti VM 'si için geçerlidir. Şirket içi Configuration Manager site sunucuları veya istemcileri için uygulanmaz. TLS 1,2 hakkında daha fazla bilgi için bkz. [tls 1,2 'yi etkinleştirme](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

13. Sürüm 1806 ' den başlayarak, sihirbaz varsayılan olarak aşağıdaki seçeneği sağlar: **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin verin ve Azure depolama 'dan içerik sunar**. Artık bir CMG, istemcilere içerik de sunabilir. Bu işlevsellik, Azure VM 'lerinin gerekli sertifikalarını ve maliyetini azaltır.  

14. **İleri**’yi seçin.  

15. CMG trafiğini 14 günlük bir eşiğe göre izlemek için, eşik uyarısını açmak üzere onay kutusunu seçin. Ardından, eşiği ve farklı uyarı düzeylerinin ne kadar yükseltebileceği yüzdeyi belirtin. İşiniz bittiğinde **İleri ' yi** seçin.  

16. Ayarları gözden geçirin ve **İleri**' yi seçin. Configuration Manager hizmeti ayarlamaya başlar. Sihirbazı kapattıktan sonra, hizmetin Azure 'da tamamen sağlanması beş ila 15 dakika sürer. Hizmetin ne zaman hazırlanmadığını öğrenmek için yeni CMG 'nin **durum** sütununu kontrol edin.  

    > [!Note]  
    > CMG dağıtımlarının sorunlarını gidermek için **CloudMgr. log** ve **cmgsetup. log**kullanın. Daha fazla bilgi için bkz. [günlük dosyaları](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-primary-site-for-client-certificate-authentication"></a>Birincil siteyi istemci sertifikası kimlik doğrulaması için yapılandırma

İstemciler için [istemci kimlik doğrulama sertifikalarını](certificates-for-cloud-management-gateway.md#bkmk_clientauth) CMG ile kimlik doğrulaması yapacak şekilde kullanıyorsanız, her birincil siteyi yapılandırmak için bu yordamı izleyin.  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler**' i seçin.  

2. İnternet tabanlı istemcilerinizin atandığı birincil siteyi seçin ve **Özellikler**' i seçin.  

3. Birincil site Özellik sayfasının **Istemci bilgisayar iletişimi** sekmesine geçin, **kullanılabilir olduğunda PKI istemci sertifikası (istemci kimlik doğrulaması) kullan**' ı işaretleyin.  

    > [!Note]
    > Sürüm 1906 ' den başlayarak bu sekmeye **Iletişim güvenliği**denir.<!-- SCCMDocs#1645 -->  

4. Bir CRL yayımlamazsanız, **istemciler site sistemleri için sertifika iptal listesini (CRL) denetleme**seçeneğinin işaretini kaldırın.  


## <a name="add-the-cmg-connection-point"></a>CMG bağlantı noktasını ekleme

CMG bağlantı noktası, CMG ile iletişim kurmak için site sistem rolüdür. CMG bağlantı noktasını eklemek için, [site sistemi rollerini yüklemek](../../../servers/deploy/configure/install-site-system-roles.md)üzere genel yönergeleri izleyin. Site sistemi rolü Ekleme Sihirbazı ' nın sistem rolü seçimi sayfasında, **bulut yönetimi ağ geçidi bağlantı noktası**' nı seçin. Sonra bu sunucunun bağlandığı **bulut yönetimi ağ geçidi adını** seçin. Sihirbaz seçili CMG 'nin bölgesini gösterir.

> [!Important]
> CMG bağlantı noktası, bazı senaryolarda [istemci kimlik doğrulama sertifikasına](certificates-for-cloud-management-gateway.md#bkmk_clientauth) sahip olmalıdır.

CMG hizmet durumu sorunlarını gidermek için **Cmgservice. log** ve **SMS_Cloud_ProxyConnector. log**kullanın. Daha fazla bilgi için bkz. [günlük dosyaları](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>CMG trafiği için istemciye yönelik rolleri yapılandırma

Yönetim noktası ve yazılım güncelleştirme noktası site sistemlerini CMG trafiğini kabul edecek şekilde yapılandırın. Bu yordamı, internet tabanlı istemcilere hizmet veren tüm yönetim noktaları ve yazılım güncelleştirme noktaları için birincil sitede yapın.  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **sunucular ve site sistemi rolleri** düğümünü seçin. Şeridin Giriş sekmesinde, Görünüm grubunda, **role sahip sunucular**' ı seçin. Sonra listeden **Yönetim noktası** ' nı seçin.  

2. CMG trafiği için yapılandırmak istediğiniz site sistem sunucusunu seçin. Ayrıntılar bölmesinde **Yönetim noktası** rolünü seçin ve ardından Şeritteki **Özellikler** ' i seçin.  

3. Istemci bağlantıları altındaki Yönetim noktası özellikleri sayfasında, **Configuration Manager bulut yönetimi ağ geçidi trafiğine Izin ver**' in yanındaki kutuyu işaretleyin.

    CMG tasarımınıza ve Configuration Manager sürümüne bağlı olarak, **https** seçeneğini etkinleştirmeniz gerekebilir. Daha fazla bilgi için bkz. [https için yönetim noktasını etkinleştirme](certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

4. Yönetim noktası Özellikler penceresini kapatmak için **Tamam ' ı** seçin.  

Gerektiğinde ek yönetim noktaları ve tüm yazılım güncelleştirme noktaları için bu adımları yineleyin.


## <a name="configure-boundary-groups"></a>Sınır gruplarını yapılandırma

<!--3640932-->
Sürüm 1902 ' den başlayarak bir CMG 'yi bir sınır grubuyla ilişkilendirebilirsiniz. Bu yapılandırma, istemcilerin sınır grubu ilişkilerine göre istemci iletişimi için varsayılan veya CMG 'ye geri dönüş yapmasına izin verir.

Sınır grupları hakkında daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../../../servers/deploy/configure/boundary-groups.md).

[Bir sınır grubu oluşturduğunuzda veya yapılandırdığınızda](../../../servers/deploy/configure/boundary-group-procedures.md), **Başvurular** sekmesinde bir bulut yönetimi ağ geçidi ekleyin. Bu eylem CMG 'yi bu sınır grubuyla ilişkilendirir.


## <a name="configure-clients-for-cmg"></a>CMG için istemcileri yapılandırma

CMG ve site sistem rolleri çalışırken istemciler, CMG hizmetinin konumunu bir sonraki konum isteğinde otomatik olarak alır. [Kimlik doğrulaması Için Azure AD 'yi kullanarak Windows 10 istemcileri yükleyip atamadığınız](../../deploy/deploy-clients-cmg-azure.md)müddetçe, istemcilerin CMG hizmetinin konumunu alabilmesi için intranette olması gerekir. Konum istekleri için yoklama döngüsünün her 24 saati vardır. Normal olarak zamanlanmış konum isteğini beklemek istemiyorsanız, bilgisayarda SMS Aracısı ana bilgisayar hizmeti 'ni (Ccmexec. exe) yeniden başlatarak isteği zorlayabilirsiniz.  

> [!Note]
> Varsayılan olarak tüm istemciler CMG ilkesi alır. Bu davranışı istemci ayarıyla denetleyin, [İstemcilerin bir bulut yönetimi ağ geçidini kullanmasına izin](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway)vermez.

Configuration Manager istemcisi, intranet veya Internet üzerinde olup olmadığını otomatik olarak belirler. İstemci bir etki alanı denetleyicisiyle veya şirket içi bir yönetim noktasıyla iletişim kurabildiğinden, bağlantı türünü **Şu anda intranet**olarak ayarlar. Aksi takdirde, **Şu anda Internet**'e geçer ve sitesiyle iletişim kurmak için CMG hizmetinin konumunu kullanır.

>[!NOTE]
> İstemci, intranet veya internet 'te olsun etmeksizin her zaman CMG 'yi kullanmaya zorlayabilirsiniz. Bu yapılandırma, test amacıyla veya her zaman CMG 'yi kullanmaya zorlamak istediğiniz istemciler için yararlıdır. İstemcide aşağıdaki kayıt defteri anahtarını ayarlayın:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Bu ayarı, istemci yüklemesi sırasında [Ccmalwaysinf](../../deploy/about-client-installation-properties.md#ccmalwaysinf) özelliğini kullanarak da belirtebilirsiniz.
>
> Bu ayar, istemci sınır grubu yapılandırmalarının yerel kaynaklardan yararlanabilecek bir konuma gezinse bile her zaman uygulanır.


İstemcilerin CMG 'yi belirten ilkeye sahip olduğunu doğrulamak için, istemci bilgisayarda yönetici olarak bir Windows PowerShell komut istemi açın ve aşağıdaki komutu çalıştırın:`Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Bu komut, istemcinin bildiği herhangi bir internet tabanlı yönetim noktasını görüntüler. CMG Teknik olarak Internet tabanlı bir yönetim noktası olmadığından, istemciler onu bir olarak görüntüler.

> [!Note]  
> CMG istemci trafiği sorunlarını gidermek için **CMGHttpHandler. log**, **cmgservice. log**ve **SMS_Cloud_ProxyConnector. log**kullanın. Daha fazla bilgi için bkz. [günlük dosyaları](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).

### <a name="install-off-premises-clients-using-a-cmg"></a>CMG kullanarak şirket içi istemcileri yükler

İstemci aracısını Şu anda intranetinize bağlı olmayan sistemlere yüklemek için aşağıdaki koşullardan biri doğru olmalıdır. Her durumda, hedef sistemlerdeki bir yerel yönetici hesabı gereklidir.

1. Configuration Manager site, istemci kimlik doğrulaması için PKI sertifikaları kullanacak şekilde doğru şekilde yapılandırılmıştır. Ayrıca, istemci sistemlerinin her biri, daha önce kendisine verilen geçerli, benzersiz ve güvenilir bir istemci kimlik doğrulama sertifikasına sahiptir.

2. Sistemler Azure AD etki alanına katılmış veya karma Azure AD etki alanına katılmış.

3. Site, sürüm 2002 veya sonraki bir sürümü Configuration Manager çalışıyor.

1 ve 2. seçenekler için, **CCMSetup. exe**' yi çağırırken CMG 'nin URL 'sini belirtmek için **/MP** parametresini kullanın. Daha fazla bilgi için bkz. [istemci yükleme parametreleri ve özellikleri hakkında](../../deploy/about-client-installation-properties.md#mp).

Seçenek 3 ' ten itibaren Configuration Manager sürüm 2002 ' den başlayarak, istemci aracısını toplu kayıt belirteci kullanarak intranetinize bağlı olmayan sistemlere yükleyebilirsiniz. Bu yöntem hakkında daha fazla bilgi için bkz. [toplu kayıt belirteci oluşturma](../../deploy/deploy-clients-cmg-token.md#create-a-bulk-registration-token).

### <a name="configure-off-premises-clients-for-cmg"></a>CMG için şirket dışı istemcileri yapılandırma

Aşağıdaki koşulların doğru olduğu durumlarda, son yapılandırılmış bir CMG 'ye sistemleri bağlayabilirsiniz:  

- Sistemlerde Configuration Manager istemci Aracısı zaten yüklü.

- Sistemler bağlı değil ve intranetinize bağlanamaz.

- Sistemler aşağıdaki koşullardan birini karşılar:

  - Her birinin önceden kendisine verilmiş geçerli, benzersiz ve güvenilir bir istemci kimlik doğrulama sertifikası vardır.

  - Azure AD etki alanına katılmış

  - Karma Azure AD etki alanına katılmış.

- Mevcut istemci aracısını tamamen yeniden yüklemeniz gerekmez.

- Bir makine kayıt defteri değerini değiştirme ve yerel yönetici hesabı kullanarak **SMS Aracısı ana bilgisayar** hizmetini yeniden başlatma yönteminiz vardır.

Bu sistemlerde bağlantıyı zorlamak için, **Hklm\software\microsoft\ccm**altında **cmgfqdn** (tür REG_SZ) kayıt defteri değerini oluşturun. Bu değeri CMG 'nin URL 'SI olarak ayarlayın (örneğin, `https://contoso-cmg.contoso.com` ). Ayarladıktan sonra, istemci sisteminde **SMS Aracısı ana bilgisayar** hizmetini yeniden başlatın.

Configuration Manager istemcisinde kayıt defterinde ayarlanmış geçerli bir CMG veya internet 'e yönelik bir yönetim noktası yoksa, **Cmgfqdn** kayıt defteri değerini otomatik olarak denetler. Bu denetim, **SMS aracı ana bilgisayar** hizmeti başlatıldığında veya bir ağ değişikliği algıladığında her 25 saatte bir gerçekleşir. İstemci sitesine bağlanıp bir CMG öğrendiğinde, bu değeri otomatik olarak güncelleştirir.

## <a name="modify-a-cmg"></a>CMG 'yi değiştirme

Bir CMG oluşturduktan sonra bazı ayarlarından bazılarını değiştirebilirsiniz. Configuration Manager konsolundaki CMG 'yi seçin ve **Özellikler**' i seçin. Aşağıdaki sekmelerde ayarları yapılandırın:  

#### <a name="general"></a>Genel

- **Azure Yönetim sertifikası**: CMG için Azure yönetim sertifikasını değiştirin. Bu seçenek, sertifikanın süresi dolmadan önce güncelleştirilirken faydalıdır.  

#### <a name="settings"></a>Ayarlar

- **Sertifika dosyası**: CMG için sunucu kimlik doğrulama sertifikasını değiştirin. Bu seçenek, sertifikanın süresi dolmadan önce güncelleştirilirken faydalıdır.  

- **VM örneği**: hizmetin Azure 'da kullandığı sanal makine sayısını değiştirin. Bu ayar, kullanım veya maliyet konularına göre hizmeti dinamik olarak ölçeklendirmenize veya değiştirmenize olanak sağlar.  

- **Sertifikalar**: güvenilen kök veya ara CA sertifikaları ekleyin veya kaldırın. Bu seçenek, yeni CA 'Lar eklenirken veya süre dolma sertifikaları devre dışı bırakıldığında faydalıdır.  

- **Istemci sertifikası Iptalini doğrulama**: Bu ayarı ilk olarak CMG oluştururken etkinleştirmediyseniz, CRL 'yi yayımladıktan sonra daha sonra etkinleştirebilirsiniz. Daha fazla bilgi için bkz. [sertifika iptal listesini yayımlama](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin verin ve Azure depolama 'dan içerik sunabilir**: 1806 sürümünden başlayarak, bu yeni seçenek varsayılan olarak etkindir. Artık bir CMG, istemcilere içerik de sunabilir. Bu işlevsellik, Azure VM 'lerinin gerekli sertifikalarını ve maliyetini azaltır.<!--1358651-->  

#### <a name="alerts"></a>Uyarılar

CMG 'yi oluşturduktan sonra her zaman uyarıları yeniden yapılandırın.


### <a name="redeploy-the-service"></a>Hizmeti yeniden dağıtın

Aşağıdaki yapılandırma gibi daha önemli değişiklikler, hizmetin yeniden dağıtılmasını gerektirir:

- Azure Resource Manager için klasik dağıtım yöntemi
- Abonelik
- Hizmet adı
- Genel PKI 'ya özel
- Bölge

Internet tabanlı istemciler için en az bir etkin CMG 'yi her zaman güncel tutun. Internet tabanlı istemciler, kaldırılan bir CMG ile iletişim kuramaz. İstemciler, intranete geri dolaşılana kadar yeni bir tane hakkında bilgi sahibi değildir. İlk olarak silmek için ikinci bir CMG örneği oluştururken başka bir CMG bağlantı noktası da oluşturun.

İstemciler ilkeyi varsayılan olarak her 24 saatte bir yeniler, bu nedenle eskisini silmeden önce yeni bir CMG oluşturduktan sonra en az bir gün bekleyin. İstemcileri kapalıysa veya bir internet bağlantısı yoksa, daha uzun süre beklemeniz gerekebilir.

Klasik dağıtım yönteminde mevcut bir CMG varsa, Azure Resource Manager dağıtım yöntemini kullanmak için yeni bir CMG dağıtmanız gerekir.<!--509753--> İki seçenek vardır:  

- Aynı hizmet adını yeniden kullanmak istiyorsanız:  

    1. İlk olarak klasik CMG 'yi silerek, internet tabanlı istemciler için her zaman en az bir etkin CMG 'ye sahip olmak üzere kılavuz hesaba katılarak.  

    2. Kaynak Yöneticisi dağıtımı kullanarak yeni bir CMG oluşturun. Aynı sunucu kimlik doğrulama sertifikasını yeniden kullanın.  

    3. CMG bağlantı noktasını yeni CMG örneğini kullanacak şekilde yeniden yapılandırın.  

- Yeni bir hizmet adı kullanmak istiyorsanız:  

    1. Kaynak Yöneticisi dağıtımı kullanarak yeni bir CMG oluşturun. Yeni bir sunucu kimlik doğrulama sertifikası kullanın.  

    2. Yeni bir CMG bağlantı noktası oluşturun ve yeni CMG ile bağlantı oluşturun.  

    3. Internet tabanlı istemciler için en az bir gün bekleyin ve yeni CMG hakkında ilke alır.  

    4. Klasik CMG 'yi silin.  

> [!Tip]  
> Bir CMG 'nin geçerli dağıtım modelini öğrenmek için:<!--SCCMDocs issue #611-->  
>
> 1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **bulut yönetimi ağ geçidi** düğümünü seçin.  
> 2. CMG örneğini seçin.  
> 3. Pencerenin alt kısmındaki Ayrıntılar bölmesinde **dağıtım modeli** özniteliği ' ni arayın. Kaynak Yöneticisi dağıtımı için bu öznitelik **Azure Resource Manager**. Azure Yönetim sertifikası olan eski dağıtım modeli **azure Service Manager**olarak görüntülenir.
>
> Ayrıca, **dağıtım modeli** özniteliğini liste görünümüne bir sütun olarak ekleyebilirsiniz.  

### <a name="modifications-in-the-azure-portal"></a>Azure portal değişiklikler

Yalnızca Configuration Manager konsolundan CMG 'yi değiştirin. Hizmette veya temel alınan VM 'Lerde doğrudan Azure 'da değişiklik yapma desteklenmez. Hiçbir değişiklik yapılmadan kaybolmuş olabilir. Her PaaS 'de olduğu gibi, hizmet VM 'Leri dilediğiniz zaman yeniden oluşturabilir. Bu yeniden uygulama, arka uç donanım bakımı için veya VM işletim sistemine güncelleştirmelerin uygulanması olabilir.

### <a name="delete-the-service"></a>Hizmeti Sil

CMG 'yi silmeniz gerekiyorsa Configuration Manager konsolundan da bunu yapın. Azure 'daki tüm bileşenleri el ile kaldırmak sistemin tutarsız olmasına neden olur. Bu durum yalnız bırakılmış bilgileri bırakır ve beklenmeyen davranışlar ortaya çıkabilir.


## <a name="next-steps"></a>Sonraki adımlar

- [Bulut yönetimi ağ geçidi için istemcileri izleme](monitor-clients-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidi hakkında sık sorulan sorular](cloud-management-gateway-faq.md)
