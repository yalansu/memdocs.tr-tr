---
title: Technical Preview 1606 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1606 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 18ea44f662591a21750fb630425ddfb975678aa2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695605"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Configuration Manager için Technical Preview 1606 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1606 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz.      Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    

**Bu teknik önizlemede bilinen sorunlar:**  
*  Technical Preview 1604 ' den 1605 ' e ve ardından 1606 sürümüne güncelleştirdiğinizde, güncelleştirme başarısız olabilir ve **cmupdate. log**dosyasına aşağıdakine benzer bir hata kaydedilir:

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    Bu durumda, **güncelleştirmeler ve bakım** düğümünde **güncelleştirmeler için denetle**' ye tıklayın ve ardından güncelleştirme yüklemesini **yeniden deneyin** .
    ***

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a> Cihazları koleksiyonlara otomatik olarak kategorilere ayır
Microsoft Intune ile Configuration Manager kullanırken cihazları otomatik olarak cihaz koleksiyonlarına yerleştirmek için kullanılabilecek cihaz kategorileri oluşturabilirsiniz. Daha sonra kullanıcıların Intune 'A cihaz kaydettiğinde bir cihaz kategorisi seçmesi gerekir. Ayrıca, Configuration Manager konsolundan bir cihazın kategorisini de değiştirebilirsiniz.

**Önemli:** Bu özellik Microsoft Intune **haziran 2016** sürümüyle birlikte çalışarak. Bu yordamları denemeden önce bu sürüme güncelleştirildiğinden emin olun.

### <a name="try-it-out"></a>Deneyin!

### <a name="create-a-set-of-device-categories"></a>Cihaz kategorileri kümesi oluşturma
1.  Configuration Manager konsolunun **varlıklar ve uyum** çalışma alanında **genel bakış**' ı genişletin, sonra **Cihaz Koleksiyonları**' na tıklayın.
2.  **Giriş** sekmesinde, **Kategoriler** grubunda, **cihaz kategorilerini Yönet**' e tıklayın.
3.  **Cihaz kategorilerini Yönet** iletişim kutusunda kategorileri oluşturabilir, düzenleyebilir veya kaldırabilirsiniz. Yeni bir kategori oluşturmayı deneyin.

### <a name="associate-a-collection-with-a-device-category"></a>Bir koleksiyonu bir cihaz kategorisiyle ilişkilendir
Bir koleksiyonu bir cihaz kategorisiyle ilişkilendirdiğinizde, belirttiğiniz kategoride bulunan tüm cihazlar bu koleksiyona eklenir.
1.  Bir cihaz koleksiyonunun **Özellikler** iletişim kutusunda **kural**  >  **cihaz kategorisi kuralı**Ekle ' ye tıklayın.
2.  **Cihaz kategorisi üyelik kuralı oluştur** iletişim kutusunda koleksiyondaki tüm cihazlara uygulanacak kategoriyi seçin.
3.  **Cihaz kategorisi üyelik kuralı oluştur** iletişim kutusunu ve koleksiyon özellikleri iletişim kutusunu kapatın.

### <a name="change-the-category-of-a-device"></a>Bir cihazın kategorisini değiştirme
1.  Configuration Manager konsolunun **varlıklar ve uyum** çalışma alanında **genel bakış**' ı genişletin ve ardından **cihazlar**' a tıklayın.
2.  **Cihazlar** listesinden bir cihaz seçin ve ardından **giriş** sekmesinde, **cihaz** grubunda, **Kategoriyi Değiştir**' i tıklatın.
3.  **Cihaz kategorisini Düzenle** iletişim kutusunda, bu cihaza uygulanacak kategoriyi seçin ve ardından **Tamam**' a tıklayın.

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a> Gerekli uygulama ve yazılım güncelleştirme dağıtımları için zorlama yetkisiz kullanım süresi

Bazı durumlarda, yapılandırdığınız son tarihlerden sonra kullanıcılara gerekli uygulama dağıtımlarını veya yazılım güncelleştirmelerini yüklemek için daha fazla zaman vermek isteyebilirsiniz. Bu, genellikle bir bilgisayar uzun bir süre kapatılmış ve çok sayıda uygulama veya güncelleştirme dağıtımı yüklemesi gerektiğinde gerekli olabilir.
Örneğin, bir son kullanıcı tatilden yeni döndürülürse, süresi geçmiş uygulama dağıtımları yüklenirken uzun süredir beklemek zorunda kalabilir.
Bu sorunu çözmeye yardımcı olmak için artık Configuration Manager istemci ayarlarını bir koleksiyona dağıtarak bir zorlama yetkisiz kullanım süresi tanımlayabilirsiniz.

### <a name="try-it-out"></a>Deneyin!

Yetkisiz kullanım süresini yapılandırmak için aşağıdaki işlemleri gerçekleştirin:

1.  İstemci ayarları ' nın **Bilgisayar Aracısı** sayfasında, **dağıtım son tarihi (saat) sonra** , **1** ila **120** saat arasında bir değere sahip zorlama için yeni özellik yetkisiz kullanım süresini yapılandırın.
2.  Yeni bir gerekli uygulama dağıtımında veya var olan bir dağıtımın özelliklerinde, **zamanlama** sayfasında, istemci ayarlarında tanımlanan yetkisiz kullanım süresine kadar, **kullanıcı tercihlerine göre bu dağıtımın uygulanmasını geciktir**onay kutusunu seçin.
Bu onay kutusunun seçili olduğu ve istemci ayarını dağıttığınız cihazlara hedeflenen tüm dağıtımlar zorlama yetkisiz kullanım süresini kullanır.

Bir zorlama yetkisiz kullanım süresi yapılandırır ve onay kutusunu seçerseniz, uygulama yükleme son tarihine ulaşıldığında, kullanıcının bu yetkisiz kullanım süresine yapılandırdığı ilk iş dışı penceresine yüklenir. Ancak, Kullanıcı hala yazılım merkezini açabilir ve uygulamayı istedikleri zaman yükleyebilir. Yetkisiz kullanım süresi dolduktan sonra, zorlama süresi dolan dağıtımlar için normal davranışa geri döner.
Yazılım güncelleştirmeleri dağıtım sihirbazına, otomatik dağıtım kuralları sihirbazına ve özellikler sayfalarına benzer seçenekler eklenmiştir.

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a>Device Guard ile yönetilen bir yükleyici olarak Configuration Manager kullanma

Device Guard, cihazda çalışmasına izin verilen öğeleri tamamen denetlemek için donanım ve yazılım özelliklerini kullanan bir Windows 10 özelliğidir.

Daha fazla bilgi için bkz. [Device Guard 'A giriş](/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control).

Bu sürümde, Configuration Manager ile dağıtılan yürütülebilir ve DLL dosyalarının yönetilen bir yükleyiciden geldiği şekilde otomatik olarak güvenilir olması için, Configuration Manager Device Guard ve [Windows AppLocker](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd723678(v=ws.10)) ile birlikte çalışabilir, yani hedef cihazda çalışmasına izin verilecek ve diğer yazılım, açıkça diğer AppLocker kuralları tarafından çalışmasına izin verilmediği sürece çalışmasına izin verilmeyecektir.  

Mevcut olduğunda, bu özellik Configuration Manager konsolundan yapılandırılamaz. İlkeyi yapılandırmak için, her istemcide bir kayıt defteri anahtarı yapılandırıp istemci üzerinde Windows hizmetlerini yapılandırmanız gerekir.
Bu işlem tamamlandıktan sonra, AppLocker ilke dosyasını yapılandırın. İlke dosyasını yapılandırdıktan sonra, herhangi bir uyumlu istemci cihazına dağıtabilirsiniz.


Tüm AppLocker ilkeleri gibi, yönetilen yükleyici kuralları olan ilkeler iki modda çalışabilir:

- Denetim modu – uygulamaların, notların çalışması engellenir, ancak engellenmiş olabilecek tüm uygulamalar bir günlük dosyasında bildirilir (Bu, Configuration Manager sonraki bir sürümünde desteklenecektir).
- Zorlama etkin – uygulamaların çalışması engellenir.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Device Guard tanıtımı](/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control)

- [Windows Defender uygulama denetimi dağıtım işlemini Planlama ve kullanmaya başlama](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a> Şirket içi mobil cihaz yönetimi için birden çok cihaz yönetim noktası  
  Technical Preview 1606 ile, \- Şirket Içi mobil cihaz yönetimi (MDM), kayıtlı bir cihazı, kullanılabilir birden fazla cihaz yönetim noktasına sahip olacak şekilde otomatik olarak yapılandıran, Windows 10 yıldönümü güncelleştirmesi 'nde yeni bir özelliği destekler. Bu özellik, normal kullandığı bir cihaz kullanılabilir olmadığında cihazın başka bir cihaz yönetim noktasına geri yüklenmesine izin verir. Bu özellik yalnızca Windows 10 yıldönümü güncelleştirmesi yüklü olan bilgisayarlarda kullanılabilir.  

### <a name="try-it-out"></a>Deneyin!  

1.  Hiyerarşinize birden fazla cihaz yönetim noktası yükler.  

2.  Şirket içi mobil cihaz yönetimi için bir Windows 10 yıldönümü güncelleştirme cihazı kaydedin \- .  

Şirket içi mobil cihaz yönetimi için sitenizi hazırlama ve cihazları kaydetme hakkında bilgi için \- bkz. Şirket [içi altyapıyla mobil cihazları yönetme](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>Internet 'te istemcileri yönetmeye yönelik bulut proxy hizmeti

Bulut proxy hizmeti, Internet 'teki Configuration Manager istemcilerini yönetmek için basit bir yol sağlar. Microsoft Azure dağıtılan ve bir Azure aboneliği gerektiren hizmet, bulut proxy bağlayıcı noktası adlı yeni bir rol kullanarak şirket içi Configuration Manager altyapınıza bağlanır. Tamamen dağıtıldıktan ve yapılandırıldıktan sonra istemciler, iç özel ağa veya Internet 'e bağlı olup olmadıklarına bakılmaksızın şirket içi Configuration Manager site sistem rollerine erişebilir.

Hizmeti Azure 'a dağıtmak, bulut proxy bağlayıcı noktası rolünü eklemek ve site sistem rollerini bulut proxy trafiğine izin verecek şekilde yapılandırmak için Configuration Manager konsolunu kullanırsınız. Bulut proxy hizmeti şu anda yalnızca yönetim noktasını, dağıtım noktasını ve yazılım güncelleştirme noktası rollerini destekler.

İstemci sertifikaları ve Güvenli Yuva Katmanı (SSL) sertifikaları, bilgisayarların kimliğini doğrulamak ve hizmetin farklı katmanları arasındaki iletişimleri şifrelemek için gereklidir. İstemci bilgisayarlar genellikle Grup İlkesi zorlaması aracılığıyla bir istemci sertifikası alırlar. Rolleri barındıran istemcilerle site sistem sunucusu arasındaki trafiği şifrelemek için CA 'dan özel bir SSL sertifikası oluşturmanız gerekir. Bu iki tür sertifikaya ek olarak, Azure 'da bulut proxy hizmeti dağıtmaya Configuration Manager izin veren bir yönetim sertifikası da ayarlamanız gerekir.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>TP 1606 ' de bulut proxy hizmeti gereksinimleri
- İstemci bilgisayarlar ve bulut proxy bağlayıcı noktasını çalıştıran site sistem sunucusu.
- İç CA 'dan özel SSL sertifikaları-istemci bilgisayarlardan gelen iletişimi şifrelemek ve bulut proxy hizmeti kimliğinin kimliğini doğrulamak için kullanılır.
- Bulut hizmetleri için Azure aboneliği.
- Azure Yönetim sertifikası-Azure ile Configuration Manager kimlik doğrulaması yapmak için kullanılır.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>TP 1606 ' de bulut proxy hizmeti sınırlamaları

- Yalnızca yönetim noktasını, dağıtım noktasını ve yazılım güncelleştirme noktası rollerini destekler.
- Kullanıcı ilkeleri desteklenmez.
- Configuration Manager ' de [Şirket Içi mobil cihaz yönetimi](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) ile birlikte kullanılamaz.
- Yalnızca Azure 'un genel bulut platformunda desteklenir.


### <a name="try-it-out"></a>Deneyin!

Bulut proxy hizmetini dağıtma işlemi aşağıdaki adımları içerir:

1. Bulut proxy hizmeti için özel bir SSL sertifikası oluşturun ve yayınlayın.
1. İstemci sertifikasının kökünü dışarı aktarın.
2. Yönetim sertifikasını Azure 'a yükleyin.
3. Configuration Manager konsolunda bulut proxy hizmetini ayarlayın.
4. Birincil siteyi istemci sertifikası kimlik doğrulamasını kullanacak şekilde yapılandırın.
5. Bulut proxy Bağlayıcısı noktasını sitenize ekleyin.
6. Site sistem rollerini, bulut proxy trafiğini kabul edecek şekilde yapılandırın.

Aşağıdaki bölümlerde bu adımları tamamlamaya yönelik daha fazla bilgi sağlanmaktadır.

#### <a name="create-a-custom-ssl-certificate"></a>Özel bir SSL sertifikası oluşturma

Bulut proxy hizmeti için, bulut tabanlı bir dağıtım noktası için yaptığınız gibi özel bir SSL sertifikası oluşturabilirsiniz. [Bulut tabanlı dağıtım noktaları Için hizmet sertifikası dağıtma](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) yönergelerini izleyin, ancak şunları farklı yapın:

* Yeni sertifika şablonunu ayarlarken, Configuration Manager sunucuları için ayarladığınız güvenlik grubuna **okuma** ve **kaydetme** izinleri verin.

#### <a name="export-the-client-certificates-root"></a>İstemci sertifikasının kökünü dışarı aktarma

Ağda kullanılan istemci sertifikalarının kökünü dışarı aktarmanın en kolay yolu, bir istemci sertifikasını bir tane içeren ve etki alanına katılmış makinelerden birinde açmak ve kopyalamak.

>[!NOTE]
>Bulut proxy hizmeti ile yönetmek istediğiniz tüm bilgisayarlarda ve bulut proxy bağlayıcı noktasını barındıran site sistemi sunucusunda istemci sertifikaları gereklidir. Bu makinelerden birine bir istemci sertifikası eklemeniz gerekiyorsa, bkz. [Windows bilgisayarları Için Istemci sertifikasını dağıtma](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).

1. Çalıştır penceresinde, **MMC** yazın ve Return tuşuna basın.
2. Yönetim konsolundaki Dosya menüsünde, **ek bileşen Ekle/Kaldır..**. öğesine tıklayın.
3. Ek bileşen Ekle veya Kaldır iletişim kutusunda, **Sertifikalar**' a, **>Ekle **' ye, **bilgisayar hesabı**' na, **İleri**' ye, **Yerel bilgisayar**' a ve ardından **son**' a tıklayın. **Tamam**’a tıklayarak iletişim kutusunu kapatın.
4. **Sertifikalar > kişisel > sertifikaları**' na gidin.
5. Bilgisayarda istemci kimlik doğrulaması sertifikasına çift tıklayın, sertifika yolu sekmesine tıklayın ve kök yetkiliye (yolun en üstünde) çift tıklayın.
6.  Ayrıntılar sekmesine tıklayın ve **Dosyaya Kopyala... öğesine**tıklayın.
7. Sertifika Verme Sihirbazı ' nı varsayılan sertifika biçimini kullanarak doldurun. Oluşturduğunuz kök sertifikanın adını ve konumunu unutmayın. Daha sonraki bir adımda bulut proxy hizmetini yapılandırmak için buna ihtiyaç duyarsınız.

#### <a name="upload-the-management-certificate-to-azure"></a>Yönetim sertifikasını Azure 'a yükleme

Configuration Manager Azure API 'sine erişmek ve bulut proxy hizmetini yapılandırmak için bir Azure Yönetim sertifikası gereklidir. Bir yönetim sertifikasını karşıya yükleme hakkında daha fazla bilgi ve yönergeler için, Azure belgelerinde aşağıdaki makalelere bakın:
- [Azure Cloud Services’da sertifikalara genel bakış](/azure/cloud-services/cloud-services-certs-create)
- [Azure yönetim API Management sertifikasını karşıya yükleyin](/previous-versions/azure/azure-api-management-certs).

Yönetim sertifikasıyla ilişkili abonelik KIMLIĞINI kopyalamadığınızdan emin olun. Bulut proxy hizmetini Configuration Manager konsolunda yapılandırmak için buna ihtiyacınız olacaktır.

#### <a name="set-up-cloud-proxy-service"></a>Bulut proxy hizmetini ayarlama

1. Configuration Manager konsolunda, **yönetim > Cloud Services > bulut proxy hizmeti**' ne gidin.
2. **Bulut proxy hizmeti oluştur**' a tıklayın.
3. Bulut proxy hizmeti oluşturma Sihirbazı ' nda Azure abonelik KIMLIĞINIZI girin (Azure Yönetim portalından kopyalanmış), Araştır ' a tıklayın ve Azure Yönetim sertifikası olarak yüklemek için kullandığınız sertifika dosyasını seçin. **İleri**’ye tıklayın. Konsolun Azure 'a bağlanması için birkaç dakika bekleyin.
4. Sihirbazdaki ek ayrıntıları doldurun:
    - Özel SSL sertifikasından verdiğiniz özel anahtarı (. pfx dosyası) belirtin.
    - İstemci sertifikasından aktarılmış kök sertifikayı belirtin.
    - Yeni sertifika şablonunu oluştururken kullandığınız hizmet adı FQDN 'sini belirtin.
    - **Istemci sertifikası Iptalini doğrula** ' nın yanındaki kutuyu TEMIZLEYIN (CRL bilgilerinizi herkese yayınmadığınız takdirde).
    - İşiniz bittiğinde **İleri** ' ye tıklayın.
5. Ayarları gözden geçirin ve **İleri**' ye tıklayın. Configuration Manager hizmeti ayarlamaya başlar. Sihirbaz tamamlandığında **Kapat**' a tıklayabilirsiniz, ancak hizmeti Azure 'da tamamen sağlamak için 5 ila 15 dakika arasında sürer. Hizmetin ne zaman hazırlanmadığını öğrenmek için yeni kurulum bulutu Proxy hizmetinin **durum** sütununu kontrol edin.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>İstemci sertifikası kimlik doğrulaması için birincil siteyi yapılandırma

1. Configuration Manager konsolunda **yönetim > site yapılandırması > siteleri**' ne gidin.
2. Bulut proxy hizmeti aracılığıyla yönetmek istediğiniz istemcilerin birincil sitesini seçin ve **Özellikler**' e tıklayın.
3. Birincil site Özellik sayfasının Istemci bilgisayar Iletişimleri sekmesinde, **kullanılabilir olduğunda PKI istemci sertifikası (istemci kimlik doğrulaması)** seçeneğinin yanındaki kutuyu işaretleyin.
4. **İstemciler site sistemleri için sertifika iptal listesini (CRL) kontrol edin ' in**yanındaki kutuyu temizlediğinizden emin olun. Bu seçenek yalnızca CRL 'YI herkese açık bir şekilde yayımlıyorsanız gereklidir.
5. **Tamam** düğmesine tıklayın.

#### <a name="add-the-cloud-proxy-connector-point"></a>Bulut proxy Bağlayıcısı noktasını ekleyin

Bulut proxy Bağlayıcısı noktası, bulut proxy hizmeti ile iletişim kurmak için yeni bir site sistem rolüdür. Bulut proxy Bağlayıcısı noktasını eklemek için, [Configuration Manager için site sistemi rolleri ekleme](../../core/servers/deploy/configure/add-site-system-roles.md)bölümündeki yönergeleri izleyin.

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Bulut proxy trafiği için rolleri yapılandırma

Bulut proxy hizmetini ayarlamanın son adımı, site sistem rollerini, bulut proxy trafiğini kabul edecek şekilde yapılandırmaktır. Teknik Önizleme 1606 için, bulut proxy hizmeti için yalnızca yönetim noktası, dağıtım noktası ve yazılım güncelleştirme noktası rolleri desteklenir. Her bir rolü ayrı ayrı yapılandırmanız gerekir.

1. Configuration Manager konsolunda **yönetim > site yapılandırması > sunucular ve site sistemi rolleri**' ne gidin.
2. Bulut proxy trafiği için yapılandırmak istediğiniz rolün site sistem sunucusuna tıklayın.
3. Role tıklayın ve ardından **Özellikler**' e tıklayın.
4. Rol özellikleri sayfasında, Istemci bağlantıları altında **https**' yi seçin, **bulut proxy trafiğinin Configuration Manager izin ver**' in yanındaki onay kutusunu işaretleyin ve ardından **Tamam**' a tıklayın. Kalan roller için bu adımları tekrarlayın.

#### <a name="check-status-on-a-client-on-the-internet"></a>Internet 'teki bir istemcideki durumu denetleme

Hizmet ve roller tamamen yapılandırıldıktan sonra, iç istemciler bulut proxy hizmeti 'nin konumunu bir sonraki konum isteğiyle alır. Güncelleştirilmiş konum bilgileri olan istemciler daha sonra Internet 'teki Configuration Manager ile iletişim kurabilir. Konum istekleri için yoklama döngüsünün her 24 saati vardır. Normal olarak zamanlanmış konum isteğini beklemek istemiyorsanız, bilgisayarda SMS Aracısı ana bilgisayar hizmeti 'ni (ccmexec.exe) yeniden başlatarak isteği zorlayabilirsiniz.

İstemciler bulut proxy hizmeti için yeni konum bilgilerine sahip olduktan sonra, artık iç özel ağda olmayan ancak Internet erişimi olan istemcilerin durumunu denetlemeyi deneyin. Ayrıca, bulut proxy hizmetindeki trafiği **yönetim > Cloud Services > bulut proxy hizmeti**' ne giderek, liste bölmesinde hizmeti seçerek ve trafik bilgilerini Ayrıntılar bölmesinde görüntüleyerek de izleyebilirsiniz.   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>Configuration Manager’da Office 365 istemci aracısını yönetme  

Technical Preview 1606 ' den itibaren, Office 365 istemcilerinin Configuration Manager güncelleştirmelerini almasını sağlamak için Grup ilkesi yerine bir Configuration Manager istemci Aracısı ayarı kullanabilirsiniz. Bu ayarı yapılandırdıktan ve Office 365 güncelleştirmelerini dağıttıktan sonra, Configuration Manager istemci Aracısı, Office 365 güncelleştirmelerini bir dağıtım noktasından indirmek ve onları yüklemek için Office 365 istemci aracısında iletişim kurar. Configuration Manager, istemci Aracısı ayarının envanterini de alır.

Daha fazla bilgi için bkz. [Office 365 ProPlus güncelleştirmelerini yönetme](../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Office 365 istemci Aracısı 'nı yönetmek için Configuration Manager istemci ayarını ayarlayın
1.  Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **istemci ayarları**' na tıklayın.
2. İstemci aracısını etkinleştirmek için uygun cihaz ayarlarını açın. Varsayılan ve özel istemci ayarları hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).
3. **Yazılım güncelleştirmeleri** ' ne tıklayın ve **Office 365 istemci Aracısı ayarının yönetimini etkinleştirmek** için **Evet** ' i seçin.  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter görev dizisi değişkeni kullanım dışı bırakıldı
OSDPreserveDriveLetter görev dizisi değişkeni, bu görüntüyü bir hedef bilgisayara uygularken, görev dizisinin, işletim sistemi görüntüsü WıM dosyasında yakalanan sürücü harfini kullanıp kullanmadığını belirler.
- Bu görev dizisi değişkeni, Technical Preview 1606 ' de kullanımdan kaldırılmıştır.

Bir işletim sistemi dağıtımı sırasında, varsayılan olarak Windows Kurulumu artık kullanılacak en iyi sürücü harfini (genellikle C:) ' i belirler. Kullanmak için farklı bir sürücü belirtmek istiyorsanız, Işletim sistemini Uygula görev dizisi adımında konumu değiştirebilirsiniz. **Bu işletim sistemini uygulamak istediğiniz konumu seçin** bölümüne gidin, **belirli bir mantıksal sürücü harfi**seçin ve kullanmak istediğiniz sürücüyü seçin. Hedef bilgisayarda seçtiğiniz harfle atanmış bir sürücü olmalıdır. 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>Güncelleştirmeler ve Bakım Düğümündeki Değişiklikler
Technical Preview 1606 ile Configuration Manager konsolundaki güncelleştirmeler ve bakım için uygulanan birkaç değişiklik yapılmıştır:
- **Düğüm adı değişikliği:**

    **İzleme** çalışma alanında, **site bakım durumu** düğümü **güncelleştirmeler ve bakım durumu**olarak yeniden adlandırıldı.
- **Daha fazla yükleme durumu:**

    Bir sitenin güncelleştirme yükleme durumunu görüntülediğinizde, konsol artık aşağıdaki eylemler için ayrı Ayrıntılar görüntüler:
    - **İndir**  (Bu yalnızca hizmet bağlantı noktası site sistem rolünün yüklü olduğu en üst katman sitesi için geçerlidir)
    - **Çoğaltma**
    - **Önkoşul Denetimi**
    - **Yükleme**

  Ayrıca, daha fazla bilgi için görüntüleyebileceğiniz günlük dosyası dahil olmak üzere her bir adımla ilgili daha ayrıntılı bilgiler de mevcuttur.  
-   **Önkoşul başarısızlıklarını yeniden deneme için yeni seçenek:**

    Hem **Yönetim** hem de **izleme** çalışma alanlarında, **güncelleştirmeler ve bakım** düğümü, şeritte **Önkoşul uyarılarını yoksay**adlı yeni bir düğme içerir.

    Önkoşul uyarılarını yok say (güncelleştirmeler Sihirbazı 'ndan) seçeneğini kullanmadan güncelleştirmeleri yüklediğinizde ve bu güncelleştirme yüklemesi ön koşul **uyarısı**durumuyla durursa, bu güncelleştirme yüklemesinin önkoşul uyarılarını gözardı eden otomatik devamlılık tetiklenmesi için Şeritteki **Önkoşul uyarılarını yoksay** seçeneğini belirleyebilirsiniz.  



- **Güncelleştirmelerin temizleyici görünümü:**

    **Güncelleştirmeler ve bakım** düğümünü görüntülediğinizde, artık yalnızca en son yüklenen güncelleştirmeyi ve yükleyebileceğiniz yeni güncelleştirmeleri görürsünüz. Daha önce yüklenen güncelleştirmeleri görüntülemek için şeritte görüntülenen yeni **Geçmiş** düğmesine tıklayın.  

-   **Ön üretim için yeniden adlandırılan seçenek:**

    Güncelleştirmeler ve bakım düğümünde, **istemci seçenekleri** adlı düğme artık **ön üretim istemcisini yükseltmek**için yeniden adlandırıldı.