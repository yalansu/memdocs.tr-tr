---
title: CMG sertifikaları
titleSuffix: Configuration Manager
description: Bulut yönetimi ağ geçidi ile kullanılacak farklı dijital sertifikalar hakkında bilgi edinin.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: a2e032e2aecfd53dc3a92cfb9c40798b4dcd1db9
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692783"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi için sertifikalar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bulut yönetimi ağ geçidi (CMG) ile internet 'te istemcileri yönetmek için kullandığınız senaryoya bağlı olarak, aşağıdaki dijital sertifikalardan birine veya daha fazlasına ihtiyacınız vardır:  

- [CMG sunucusu kimlik doğrulama sertifikası](#bkmk_serverauth)  
  - [CMG güvenilen kök sertifikayı istemcilere](#bkmk_cmgroot)  
  - [Ortak sağlayıcı tarafından verilen sunucu kimlik doğrulama sertifikası](#bkmk_serverauthpublic)  
  - [Kurumsal PKI 'dan verilen sunucu kimlik doğrulama sertifikası](#bkmk_serverauthpki)  

- [İstemci kimlik doğrulama sertifikası](#bkmk_clientauth)
  - [CMG bağlantı noktası](#bkmk_cmgcp)
  - [İstemci güvenilen kök sertifikası CMG 'ye](#bkmk_clientroot)  

- [HTTPS için yönetim noktasını etkinleştir](#bkmk_mphttps)  

- [Azure Yönetim sertifikası](#bkmk_azuremgmt)  

Farklı senaryolar hakkında daha fazla bilgi için bkz. [plan for Cloud Management Gateway](plan-cloud-management-gateway.md).

## <a name="general-information"></a>Genel bilgiler

<!--SCCMDocs issue #779-->
Bulut yönetimi ağ geçidi için sertifikalar aşağıdaki konfigürasyonları destekler:  

- 2048 bit veya 4096 bit anahtar uzunluğu

- Sertifika özel anahtarları için anahtar depolama sağlayıcıları. Daha fazla bilgi için bkz. [CNG sertifikalarına genel bakış](../../../plan-design/network/cng-certificates-overview.md).  

- Windows 'u şu ilkeyle yapılandırdığınızda: **Sistem şifrelemesi: şifreleme, karma ve imzalama IÇIN FIPS ile uyumlu algoritmalar kullanın**  

- **TLS 1,2**. Daha fazla bilgi için bkz. [TLS 1,2 'yi etkinleştirme](../../../plan-design/security/enable-tls-1-2.md).  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a> CMG sunucusu kimlik doğrulama sertifikası

*Bu sertifika tüm senaryolarda gereklidir.*

Bu sertifikayı, Configuration Manager konsolunda CMG oluştururken sağlarsınız.

CMG, internet tabanlı istemcilerin bağlandığı bir HTTPS hizmeti oluşturur. Sunucu, güvenli kanalı oluşturmak için bir sunucu kimlik doğrulama sertifikası gerektirir. Bir ortak sağlayıcıdan bu amaçla bir sertifika alın veya bunu ortak anahtar altyapınızdan (PKI) verin. Daha fazla bilgi için bkz. [Istemcilere CMG güvenilen kök sertifikası](#bkmk_cmgroot).

> [!NOTE]
> CMG sunucusu kimlik doğrulama sertifikası joker karakterleri destekler. Bazı sertifika yetkilileri, ana bilgisayar adı için bir joker karakter kullanarak sertifika verebilir. Örneğin, `*.contoso.com`. Bazı kuruluşlar, PKI 'sını basitleştirmek ve bakım maliyetlerini azaltmak için joker karakter sertifikaları kullanır.<!--491233-->  
>
> CMG ile bir joker karakter sertifikası kullanma hakkında daha fazla bilgi için bkz. [CMG ayarlama](setup-cloud-management-gateway.md#set-up-a-cmg).<!--SCCMDocs issue #565-->  

Bu sertifika, Azure 'da hizmeti belirlemek için genel olarak benzersiz bir ad gerektirir. Bir sertifika istenmeden önce, istediğiniz Azure etki alanı adının benzersiz olduğunu doğrulayın. Örneğin, *GraniteFalls.cloudapp.net*.

1. [Azure portalında](https://portal.azure.com) oturum açın.
1. **Tüm kaynaklar**' ı ve ardından **Ekle**' yi seçin.
1. **Bulut hizmeti**araması yapın. **Oluştur**’u seçin.
1. **DNS adı** alanına istediğiniz öneki yazın, örneğin, *granteden*. Arabirim, etki alanı adının kullanılabilir olduğunu veya başka bir hizmet tarafından zaten kullanımda olduğunu yansıtır.

    > [!Important]  
    > Hizmeti portalda oluşturma bu işlemi, adın kullanılabilirliğini denetlemek için kullanmanız yeterlidir.

Ayrıca, CMG 'yi içerik için etkinleştirirseniz CMG hizmeti adının de benzersiz bir Azure depolama hesabı adı olduğunu doğrulayın. CMG bulut hizmeti adı benzersizdir, ancak depolama hesabı adı değilse Configuration Manager Azure 'da hizmeti sağlayamaz. Aşağıdaki değişikliklerle Azure portal yukarıdaki işlemi yineleyin:

- **Depolama hesabı** ara
- Adınızı **depolama hesabı adı** alanında test edin

DNS adı ön eki, örneğin *Granıse*, 3 ile 24 karakter uzunluğunda olmalı ve yalnızca alfasayısal karakterler kullanmalıdır. Tire () gibi özel karakterler kullanmayın `-` .<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a> CMG güvenilen kök sertifikayı istemcilere

İstemcilerin CMG sunucusu kimlik doğrulama sertifikasına güvenmesi gerekir. Bu güveni gerçekleştirmenin iki yöntemi vardır:

- Ortak ve genel olarak güvenilen bir sertifika sağlayıcısından bir sertifika kullanın. Örneğin, DigiCert, Thawte veya VeriSign ile sınırlı değildir. Windows istemcileri, bu sağlayıcılardan güvenilen kök sertifika yetkililerini (CA 'Lar) içerir. Bu sağlayıcılardan biri tarafından verilen bir sunucu kimlik doğrulama sertifikası kullanarak istemcileriniz otomatik olarak ona güvenir.  

- Ortak anahtar altyapınızdan (PKI) kuruluş CA 'sı tarafından verilen bir sertifika kullanın. Çoğu Kurumsal PKI uygulaması, güvenilen kök CA 'Ları Windows istemcilerine ekler. Örneğin, Active Directory Sertifika Hizmetleri 'ni Grup İlkesi ile kullanma. İstemcilerinizin otomatik olarak güvendiği bir CA 'dan CMG sunucusu kimlik doğrulama sertifikası verirseniz, CA güvenilen kök sertifikayı Internet tabanlı istemcilere ekleyin.  

  - İstemcilerdeki sertifikaları sağlamak için Configuration Manager sertifika profillerini de kullanabilirsiniz. Daha fazla bilgi için bkz. [sertifika profillerine giriş](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).

  - [Configuration Manager Istemcisini Intune 'dan yüklemeyi](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)planlıyorsanız, istemcilerdeki sertifikaları sağlamak için Intune sertifika profillerini de kullanabilirsiniz. Daha fazla bilgi için bkz. [sertifika profili yapılandırma](../../../../../intune/protect/certificates-configure.md).

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a> Ortak sağlayıcı tarafından verilen sunucu kimlik doğrulama sertifikası

Bir üçüncü taraf sertifika sağlayıcısı, bu etki alanının Microsoft tarafından sahiplendiğinden, CloudApp.net için bir sertifika oluşturamaz. Yalnızca sahip olduğunuz bir etki alanı için verilen bir sertifika edinebilirsiniz. Bir üçüncü taraf sağlayıcıdan sertifika almak için başlıca neden, istemcilerinizin o sağlayıcının kök sertifikasına zaten güveneceğidir.

Bir DNS diğer adı oluşturmak için aşağıdaki işlemi kullanın:

1. Kuruluşunuzun ortak DNS ' de kurallı bir ad kaydı (CNAME) oluşturun. Bu kayıt, CMG için ortak sertifikada kullandığınız kolay bir ad için bir diğer ad oluşturur.

    Örneğin, contoso CMG **Granılarını**adlandırır. Bu ad Azure 'da **GraniteFalls.cloudapp.net** olur. Contoso 'nun genel DNS contoso.com ad alanında, DNS Yöneticisi gerçek ana bilgisayar adı olan **GraniteFalls.cloudapp.net**için **GraniteFalls.contoso.com** için yeni bir CNAME kaydı oluşturur.  

2. CNAME diğer adının ortak adını (CN) kullanarak ortak sağlayıcıdan bir sunucu kimlik doğrulama sertifikası isteyin.
Örneğin, contoso, GraniteFalls.Contoso.com sertifikası için **GraniteFalls.Contoso.com** kullanır.  

3. Bu sertifikayı kullanarak Configuration Manager konsolunda CMG 'yi oluşturun. Bulut Yönetimi Ağ Geçidi Oluşturma sihirbazının **Ayarlar** sayfasında:  

    - Bu bulut hizmeti için sunucu sertifikasını eklediğinizde ( **sertifika dosyasından**), sihirbaz ana bilgisayar adını hizmet adı olarak CN sertifikasından ayıklar.  

    - Daha sonra bu ana bilgisayar adını Azure ABD Kamu Bulutu için **cloudapp.net**veya **usgovcloudapp.net** 'e ekler. Bu, hizmeti Azure 'Da oluşturmak için kullanılan hizmet FQDN 'sidir.  

    - Örneğin, contoso CMG 'yi oluşturduğunda Configuration Manager ana bilgisayar adı **Granıı** sertifikasını CN 'den ayıklar. Azure, gerçek hizmeti **GraniteFalls.cloudapp.net**olarak oluşturur.  

Configuration Manager içinde CMG örneğini oluşturduğunuzda, sertifikanın Configuration Manager GraniteFalls.Contoso.com sahip olması durumunda, yalnızca ana bilgisayar adını ayıklar, örneğin: Granıda. Bu ana bilgisayar adını, Azure 'un bir bulut hizmeti oluştururken gerektirdiği CloudApp.net 'e ekler. Etki alanınız için DNS ad alanındaki CNAME diğer adı, Contoso.com, bu iki FQDN 'yi birlikte eşler. Configuration Manager istemcilere bu CMG 'ye erişmek için bir ilke verir; DNS eşlemesi, Azure 'daki hizmete güvenli bir şekilde erişebilmeleri için bir araya gelir.<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a> Kurumsal PKI 'dan verilen sunucu kimlik doğrulama sertifikası

CMG için bir bulut dağıtım noktasıyla aynı şekilde özel bir SSL sertifikası oluşturun. [Bulut tabanlı dağıtım noktaları için hizmet sertifikası dağıtma](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) yönergelerini izleyin, ancak şunları farklı yapın:

- Özel Web sunucusu sertifikası istenirken, sertifikanın ortak adı için bir FQDN belirtin. Bu ad sahip olduğunuz bir ortak etki alanı adı olabilir veya cloudapp.net etki alanını kullanabilirsiniz. Kendi ortak etki alanınızı kullanıyorsanız, kuruluşunuzun ortak DNS ' de bir DNS diğer adı oluşturmak için yukarıdaki işleme bakın.  

- CMG Web sunucusu sertifikası için cloudapp.net genel etki alanını kullanırken:  

  - Azure genel bulutunda, **cloudapp.net** ile biten bir ad kullanın  

  - Azure ABD Kamu Bulutu için **usgovcloudapp.net** ile biten bir ad kullanın  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a> İstemci kimlik doğrulama sertifikası

İstemci kimlik doğrulama sertifikası gereksinimleri:

- Bu sertifika, Windows 8.1 çalıştıran İnternet tabanlı istemciler ve Azure Active Directory (Azure AD) ile katılmamış Windows 10 cihazları için gereklidir.
- CMG bağlantı noktasında bu gerekli olabilir. Daha fazla bilgi için bkz. [CMG bağlantı noktası](#bkmk_cmgcp).
- Azure AD 'ye katılmış Windows 10 istemcileri için bu gerekli değildir.
- Siteniz sürüm 2002 veya üzeri ise, cihazlar site tarafından verilen bir belirteci kullanabilir. Daha fazla bilgi için bkz. [CMG Için belirteç tabanlı kimlik doğrulaması](../../deploy/deploy-clients-cmg-token.md).

İstemciler, CMG ile kimlik doğrulamak için bu sertifikayı kullanır. Karma veya bulut etki alanına katılmış Windows 10 cihazlarında kimlik doğrulaması yapmak için Azure AD kullandıkları için bu sertifika gerekmez.

Bu sertifikayı Configuration Manager bağlamı dışında sağlayın. Örneğin, istemci kimlik doğrulama sertifikaları vermek için Active Directory Sertifika Hizmetleri ve Grup İlkesi kullanın. Daha fazla bilgi için bkz. [Windows bilgisayarları için istemci sertifikasını dağıtma](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

> [!NOTE]
> Microsoft, cihazların Azure AD 'ye katılmasını öneriyor. Internet tabanlı cihazlar Configuration Manager kimlik doğrulaması yapmak için Azure AD kullanabilir. Ayrıca, cihazın İnternet üzerinde veya iç ağa bağlı olup olmadığı hem cihaz hem de Kullanıcı senaryolarına olanak sağlar. Daha fazla bilgi için bkz. [Azure AD kimlik kullanarak Istemciyi yükleyip kaydetme](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).
>
> Sürüm 2002 ' den başlayarak,<!--5686290--> Configuration Manager, genellikle dahili ağa bağlanmayan, Azure AD 'ye katılmadan ve PKI tarafından verilen bir sertifika yüklemek için bir yönteme sahip olmayan Internet tabanlı cihazlara yönelik desteğini uzatır. Daha fazla bilgi için bkz. [CMG Için belirteç tabanlı kimlik doğrulaması](../../deploy/deploy-clients-cmg-token.md).

### <a name="cmg-connection-point"></a><a name="bkmk_cmgcp"></a> CMG bağlantı noktası

İstemci isteklerini güvenli bir şekilde iletmek için CMG bağlantı noktası yönetim noktasıyla güvenli bir bağlantı gerektirir. Cihazlarınızı ve yönetim noktalarınızı nasıl yapılandırdığınıza bağlı olarak, CMG bağlantı noktası yapılandırmasını belirler.

- Yönetim noktası HTTPS 'dir

  - İstemcilerin istemci kimlik doğrulama sertifikası vardır: CMG bağlantı noktası, HTTPS yönetim noktasındaki sunucu kimlik doğrulama sertifikasına karşılık gelen bir istemci kimlik doğrulama sertifikası gerektirir.

  - İstemciler Azure AD kimlik doğrulamasını veya Configuration Manager belirtecini kullanır: Bu sertifika gerekli değildir.

- Gelişmiş HTTP için yönetim noktasını yapılandırırsanız: Bu sertifika gerekli değildir.

Daha fazla bilgi için bkz. [https için yönetim noktasını etkinleştirme](#bkmk_mphttps).

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a> İstemci güvenilen kök sertifikası CMG 'ye

*Bu sertifika, istemci kimlik doğrulama sertifikaları kullanılırken gereklidir. Tüm istemciler kimlik doğrulaması için Azure AD 'yi kullandıklarında, bu sertifika gerekli değildir.*

Bu sertifikayı, Configuration Manager konsolunda CMG oluştururken sağlarsınız.

CMG, istemci kimlik doğrulama sertifikalarına güvenmelidir. Bu güveni başarmak için, güvenilen kök sertifika zincirini sağlayın. Güven zincirindeki tüm sertifikaları eklediğinizden emin olun. Örneğin, istemci kimlik doğrulama sertifikası bir ara CA tarafından verildiyse, hem ara hem de kök CA sertifikalarını ekleyin.

> [!NOTE]  
> Bir CMG oluşturduğunuzda, artık ayarlar sayfasında güvenilen bir kök sertifika sağlamanız gerekmez. Bu sertifika, istemci kimlik doğrulaması için Azure AD kullanılırken gerekli değildir, ancak sihirbazda gerekli olması için kullanılır. PKI istemci kimlik doğrulama sertifikaları kullanıyorsanız, yine de CMG 'ye bir güvenilen kök sertifika eklemeniz gerekir.<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> Sürüm 1902 ve önceki sürümlerde yalnızca iki güvenilen kök CA ve dört ara (alt) CA ekleyebilirsiniz.

#### <a name="export-the-client-certificates-trusted-root"></a>İstemci sertifikasının güvenilen kökünü dışarı aktarma

Bir bilgisayara istemci kimlik doğrulama sertifikası verdikten sonra bu işlemi, güvenilen kökü dışarı aktarmak için bu bilgisayarda kullanın.

1. Başlat menüsünü açın. Çalıştır penceresini açmak için "Çalıştır" yazın. `mmc` dosyasını açın.  

2. Dosya menüsünde, **ek bileşen Ekle/Kaldır**' ı seçin...  

3. Ek bileşen Ekle veya Kaldır iletişim kutusunda **Sertifikalar**' ı seçin ve **Ekle**' yi seçin.  

    1. Sertifikalar ek bileşeni iletişim kutusunda **bilgisayar hesabı**' nı seçin ve ardından **İleri**' yi seçin.  

    1. Bilgisayar Seç iletişim kutusunda, **Yerel bilgisayar**' ı seçin ve ardından **son**' u seçin.  

    1. Ek bileşenler Ekle veya Kaldır iletişim kutusunda **Tamam**' ı seçin.  

4. **Sertifikalar**' ı genişletin, **Kişisel**' i genişletin ve **sertifikaları**seçin.  

5. Hedeflenen amacı **Istemci kimlik doğrulaması**olan bir sertifika seçin.  

    1. Eylem menüsünden **Aç**' ı seçin.  

    1. **Sertifika yolu** sekmesine gidin.  

    1. Zincirdeki sonraki sertifikayı seçin ve **sertifikayı görüntüle**' yi seçin.  

6. Bu yeni sertifika iletişim kutusunda **Ayrıntılar** sekmesine gidin. **Dosyaya Kopyala...** seçeneğini belirleyin.  

7. Sertifika Verme Sihirbazı ' nı, **der kodlamalı Ikili X. 509.440 (varsayılan sertifika biçimi) kullanarak doldurun. CER)**. Verdiğiniz sertifikanın adını ve konumunu unutmayın.  

8. Özgün istemci kimlik doğrulama sertifikasının sertifika yolundaki tüm sertifikaları dışarı aktarın. Hangi sertifika veren sertifikaların ara CA 'Ları olduğunu ve hangilerinin güvenilen kök CA 'Ları olduğunu unutmayın.  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a> HTTPS için yönetim noktasını etkinleştir

Bu sertifikayı Configuration Manager bağlamı dışında sağlayın. Örneğin, bir Web sunucusu sertifikası vermek için Active Directory Sertifika Hizmetleri ve Grup İlkesi kullanın. Daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md) ve [IIS çalıştıran site sistemleri için Web sunucusu sertifikasını dağıtma](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).

**Http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanmak**üzere site seçeneğini kullanırken, YÖNETIM noktası http olabilir. Daha fazla bilgi için bkz. [GELIŞMIŞ http](../../../plan-design/hierarchy/enhanced-http.md).

> [!TIP]
> Gelişmiş HTTP kullanmıyorsanız ve ortamınız birden fazla yönetim noktasına sahipse, tüm CMG 'ler için HTTPS 'yi etkinleştirmeniz gerekmez. CMG etkin yönetim noktalarını **yalnızca Internet**olarak yapılandırın. Daha sonra şirket içi istemcileriniz bunları kullanmayı denemez.<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>Yönetim noktaları için geliştirilmiş HTTP sertifikası

Gelişmiş HTTP 'yi etkinleştirdiğinizde, site sunucusu, kök SMS veren sertifika tarafından verilen **SMS rol SSL sertifikası**adlı kendinden imzalı bir sertifika oluşturur. Yönetim noktası, bu sertifikayı 443 numaralı bağlantı noktasına göre IIS varsayılan Web sitesine ekler.

### <a name="management-point-client-connection-mode-summary"></a>Yönetim noktası istemci bağlantı modu Özeti

Bu tablolar, istemci ve site sürümünün türüne bağlı olarak yönetim noktasının HTTP veya HTTPS gerektirip gerektirmediğini özetler.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi ile iletişim kuran Internet tabanlı istemciler için

Şirket içi yönetim noktasını CMG 'den aşağıdaki istemci bağlantı moduyla bağlantılara izin verecek şekilde yapılandırın:

| İstemci türü   | Yönetim noktası |
|------------------|------------------|
| Çalışma grubu        | E-HTTP<sup>[Note 1](#bkmk_note1)</sup>, https |
| AD etki alanına katılmış | E-HTTP<sup>[Note 1](#bkmk_note1)</sup>, https |
| Azure AD 'ye katılmış  | E-HTTP, HTTPS |
| Karma olarak katılmış    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Note 1**: Bu yapılandırma istemcinin [istemci kimlik doğrulama sertifikasına](#bkmk_clientauth)sahip olmasını gerektirir ve yalnızca cihaz merkezli senaryoları destekler.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Şirket içi yönetim noktasıyla iletişim kuran şirket içi istemciler için

Şirket içi yönetim noktasını aşağıdaki istemci bağlantı moduyla yapılandırın:

| İstemci türü   | Yönetim noktası |
|------------------|------------------|
| Çalışma grubu        | HTTP, HTTPS |
| AD etki alanına katılmış | HTTP, HTTPS |
| Azure AD 'ye katılmış  | HTTPS       |
| Karma olarak katılmış    | HTTP, HTTPS |

> [!NOTE]  
> AD alanına katılmış istemciler, bir HTTP veya HTTPS yönetim noktasıyla iletişim kuran cihaz ve Kullanıcı merkezli senaryoları destekler.  
>
> Azure AD 'ye katılmış ve hibriya katılmış istemciler cihaz merkezli senaryolar için HTTP üzerinden iletişim kurabilir, ancak kullanıcı merkezli senaryoları etkinleştirmek için E-HTTP veya HTTPS gerekir. Aksi takdirde, çalışma grubu istemcileriyle aynı şekilde davranır.  

#### <a name="legend-of-terms"></a>Koşulların göstergesi

- *Çalışma grubu*: cihaz bir etki alanına veya Azure AD 'ye katılmamış, ancak [istemci kimlik doğrulama sertifikasına](#bkmk_clientauth)sahip.
- *Ad etki alanına katılmış*: cihazı şirket içi Active Directory etki alanına katabilirsiniz.
- *Azure AD 'ye katılmış*: bulut etki alanına katılmış olarak da bilinen, cihazı BIR Azure AD kiracısına birleştirmelisiniz. Daha fazla bilgi için bkz. [Azure AD 'ye katılmış cihazlar](/azure/active-directory/devices/concept-azure-ad-join).
- *Karma olarak katıldı*: cihazı şirket içi Active Directory birleştirir ve Azure AD 'nize kaydedersiniz. Daha fazla bilgi için bkz. [karma Azure AD 'ye katılmış cihazlar](/azure/active-directory/devices/concept-azure-ad-join-hybrid).
- *Http*: yönetim noktası özelliklerinde, Istemci bağlantılarını **http**olarak ayarlarsınız.
- *Https*: yönetim noktası özelliklerinde, Istemci bağlantılarını **https**olarak ayarlarsınız.
- *E-http*: site özellikleri, **iletişim güvenliği** sekmesinde, site SISTEMI ayarlarını **https veya http**olarak ayarlarsınız ve **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanma**seçeneğini etkinleştirirsiniz. Http yönetim noktası http için yönetim noktasını yapılandırırsanız http ve HTTPS iletişimi (belirteç kimlik doğrulama senaryoları) için de kullanılır.

    > [!Note]
    > Sürüm 1902 ve önceki sürümlerde bu sekmeye **Istemci bilgisayar iletişimi**adı verilir.<!-- SCCMDocs#1645 -->

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a> Azure Yönetim sertifikası

*Bu sertifika, klasik hizmet dağıtımları için gereklidir. Azure Resource Manager dağıtımları için gerekli değildir.*

> [!Important]  
> Sürüm 1810 ' den başlayarak, Azure 'da klasik hizmet dağıtımları Configuration Manager kullanım dışıdır. Bulut yönetimi ağ geçidi için Azure Resource Manager dağıtımlarını kullanmaya başlayın. Daha fazla bilgi için [plan for CMG](plan-cloud-management-gateway.md#azure-resource-manager)konusuna bakın.
>
> Configuration Manager sürüm 1902 ' den başlayarak, bulut yönetimi ağ geçidinin yeni örnekleri için tek dağıtım mekanizmasıdır Azure Resource Manager. Bu sertifika, Configuration Manager sürüm 1902 veya sonraki sürümlerde gerekli değildir.<!-- 3605704 -->

Bu sertifikayı Azure portal ve Configuration Manager konsolunda CMG oluştururken sağlarsınız.

Azure 'da CMG 'yi oluşturmak için Configuration Manager hizmet bağlantı noktasının öncelikle Azure aboneliğinize kimlik doğrulaması yapması gerekir. Klasik hizmet dağıtımı kullanılırken bu kimlik doğrulaması için Azure yönetim sertifikasını kullanır. Azure Yöneticisi bu sertifikayı aboneliğinize yükler. Configuration Manager konsolunda CMG 'yi oluşturduğunuzda, bu sertifikayı sağlayın.

Bir yönetim sertifikasını karşıya yükleme hakkında daha fazla bilgi ve yönergeler için, Azure belgelerinde aşağıdaki makalelere bakın:

- [Cloud Services ve yönetim sertifikaları](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Azure hizmet yönetimi sertifikasını karşıya yükleme](/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Yönetim sertifikasıyla ilişkili abonelik KIMLIĞINI kopyalamadığınızdan emin olun. Bunu, Configuration Manager konsolunda CMG oluşturmak için kullanırsınız.

## <a name="next-steps"></a>Sonraki adımlar

- [Bulut yönetimi ağ geçidini kurma](setup-cloud-management-gateway.md)  

- [Bulut yönetimi ağ geçidi hakkında sık sorulan sorular](cloud-management-gateway-faq.md)  

- [Bulut yönetimi ağ geçidi için güvenlik ve gizlilik](security-and-privacy-for-cloud-management-gateway.md)