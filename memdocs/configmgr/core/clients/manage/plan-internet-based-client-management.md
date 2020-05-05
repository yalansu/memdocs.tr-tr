---
title: Internet tabanlı istemci yönetimi
titleSuffix: Configuration Manager
description: Configuration Manager 'de Internet tabanlı istemcileri yönetmek için bir plan oluşturun.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587227"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Configuration Manager 'de Internet tabanlı istemci yönetimini planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcilerini iç ağınıza bağlı olmadıkları sırada yönetmek için Internet tabanlı istemci yönetimi (IBCM) kullanın. ICM kullanmanın avantajları:

- Hizmeti sağlayan sunucuların ve rollerin tam denetimi
- Bulut hizmeti bağımlılığı yok
- Sanal özel ağ (VPN) gerektirmeyebilir
- Tüm ücretler şirket içi hizmetle ilişkilidir

Ortak ağdaki istemci bilgisayarlarını yönetmenin daha yüksek güvenlik gereksinimleri nedeniyle, IBCM PKI sertifikalarının kullanılmasını gerektirir. Bu yapılandırma, bağlantıların kimliğinin bağımsız bir yetkili tarafından doğrulanmasını sağlar. IBCM istemcileri ve site sunucuları veri gönderdiğinde, şifrelenir ve güvenlidir.  

## <a name="client-communications"></a>İstemci iletişimleri

Birincil sitelerdeki aşağıdaki site sistem rolleri güvenilmeyen konumlarda olan istemcilerden gelen bağlantıları destekler:

> [!NOTE]
> IBCM öncelikli olarak Internet tabanlı senaryoya odaklanırken, güvenilmeyen Active Directory ormanındaki istemciler için de aynı davranışlar geçerlidir. İkincil siteler güvenilmeyen konumlardan gelen istemci bağlantılarını desteklemez.

- Configuration Manager ilkesi modülü (NDES) için sertifika kayıt noktası

- Dağıtım noktası

- Bulut tabanlı dağıtım noktası

- Kayıt proxy noktası

- Geri dönüş durumu noktası

- Yönetim noktası

- Yazılım güncelleştirme noktası

> [!NOTE]
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erdi. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). Hala destek olan 1906 ve önceki sürümlerde Configuration Manager sürümleri için, Uygulama Kataloğu web sitesi noktası, internet tabanlı istemcilerden gelen bağlantıları kabul edebilir.

### <a name="about-internet-facing-site-systems"></a>İnternet 'e yönelik site sistemleri hakkında

Bir istemcinin ormanı ile site sistemi sunucusunun ormanı arasında güven olması gerekmez. Ancak, internet 'e yönelik bir site sistemi içeren bir orman, Kullanıcı hesapları içeren bir ormana güvendiğinde, **Istemci ilkesi** istemci ayarını **İnternet istemcilerinden gelen Kullanıcı ilkesi isteklerini etkinleştir**olarak etkinleştirdiğinizde, bu yapılandırma internet 'teki cihazlar için Kullanıcı tabanlı ilkeleri destekler.

Örneğin, aşağıdaki yapılandırmalarda, ICM 'nin internet 'teki cihazlar için kullanıcı ilkelerini ne zaman desteklediği gösterilmektedir:

- Internet tabanlı yönetim noktası çevre ağındadır. Bu ağın Ayrıca, kullanıcının kimliğini doğrulamak için salt bir etki alanı denetleyicisi de vardır. Çevre ve iç ağlar arasındaki bir güvenlik duvarı Active Directory paketlerine izin verir.

- Kullanıcı hesabı, intranet tabanlı ormandadır. Internet tabanlı yönetim noktası, çevre tabanlı ormandadır. Çevre ormanı iç ormana güvenir. Çevre ve iç ağlar arasındaki bir güvenlik duvarı, kimlik doğrulama paketlerine izin verir.

- Kullanıcı hesabı ve Internet tabanlı yönetim noktası, her ikisi de intranet tabanlı ormandadır. Yönetim noktasını bir Web ara sunucusu ile internet 'e yayımlayabilirsiniz.

### <a name="use-a-web-proxy-server"></a>Web proxy sunucusu kullanma

Internet tabanlı site sistemlerini bir Web proxy sunucusu ile internet 'te yayımladığınızda intranet 'e yerleştirebilirsiniz. Bu site sistemlerini yalnızca İnternet 'ten gelen istemci bağlantıları için veya internet ve intranet 'ten istemci bağlantıları için yapılandırın. Bir Web proxy sunucusu kullandığınızda, bunu SSL veya SSL tünellemesi Güvenli Yuva Katmanı (SSL) için yapılandırabilirsiniz.

#### <a name="ssl-bridging-to-ssl"></a>SSL 'e SSL köprüleme

SSL 'e SSL köprüleme, kimlik doğrulamasıyla SSL sonlandırması kullandığından önerilen ve daha güvenli bir yapılandırmadır. Bilgisayar kimlik doğrulaması ile istemci bilgisayarlarının kimliğini doğrular. Configuration Manager ile kaydolettiğiniz mobil cihazlar SSL köprülemeyi desteklemez.

Proxy 'de SSL sonlandırmasıyla, paketi iç ağa iletmeden önce internet 'ten gelen paketleri inceler. Proxy istemciden bağlantının kimliğini doğrular, sonlandırır ve ardından Internet tabanlı site sistemlerine yeni bir kimliği doğrulanmış bağlantı açar. Configuration Manager istemcileri bir proxy kullandıklarında, istemci, paket yükünde kimliğini (GUID) güvenli bir şekilde içerir. Yönetim noktası proxy 'yi istemci olarak kabul etmez. Configuration Manager, HTTP 'den HTTPS 'ye veya HTTPS 'den HTTP 'ye köprü oluşturmayı desteklemez.

> [!NOTE]
> Configuration Manager, üçüncü taraf SSL köprü oluşturma yapılandırmalarının ayarlanmasını desteklemez. Örneğin, Citrix NetScaler veya F5 BIG-IP. Configuration Manager ile kullanmak üzere yapılandırmak için lütfen cihaz satıcınızla birlikte çalışın.

#### <a name="tunneling"></a>Tünel

Proxy Web sunucunuz SSL köprüleme gereksinimlerini destekleyemiyorum, Configuration Manager SSL tünelini de destekler. Ayrıca, Configuration Manager ile kaydolmasını istediğiniz mobil cihazları desteklemek için SSL tüneli de kullanabilirsiniz. Bu, proxy, SSL paketlerini internet 'ten SSL sonlandırma olmadan site sistemlerine ilettiğinden, daha az güvenli bir seçenektir. Proxy, kötü amaçlı içerik için paketleri inceetmez. SSL tünelleme kullandığınızda proxy web sunucusu için sertifika gereksinimi yoktur.

## <a name="plan-for-internet-based-clients"></a>Internet tabanlı istemciler için plan

Internet tabanlı istemcilerinizi, hem intranet hem de internet 'te yönetim için ya da yalnızca Internet istemci yönetimi için yapılandırmak istediğinize karar verin. Bu yönetim seçeneğini, istemci yüklemesi sırasında yalnızca yapılandırabilirsiniz. Daha sonra değiştirmek için istemcisini yeniden yükleyin.

> [!NOTE]
> Bir yönetim noktasını Internet tabanlı istemcileri destekleyecek şekilde yapılandırırsanız, bu yönetim noktasına bağlanan istemciler, kullanılabilir yönetim noktaları listesini bir sonraki yenilediklerinde internet uyumlu olur.
>
> Yalnızca Internet istemci yönetiminin yapılandırmasını Internet ile kısıtlamak zorunda değilsiniz. Bunu intranette de kullanabilirsiniz.

Yalnızca Internet yönetimi için yapılandırdığınız istemciler yalnızca Internet 'ten gelen istemci bağlantıları için yapılandırdığınız site sistemleriyle iletişim kurar. Bu yapılandırmayı aşağıdaki senaryolarda kullanın:

- Bildiğiniz bilgisayarlar için intranetinize hiçbir şekilde bağlanamacaksınız. Örneğin, uzak konumlardaki satış noktası bilgisayarları.
- İstemci iletişimini yalnızca HTTPS ile kısıtlamak için. Örneğin, güvenlik duvarını ve kısıtlanmış güvenlik ilkelerini desteklemek için.
- Internet tabanlı site sistemlerini bir çevre ağına yüklediğinizde ve bu sunucuları Configuration Manager istemcileri olarak yönetmek istiyorsanız.

> [!NOTE]
> Internet üzerindeki çalışma grubu istemcilerini yönetmek istediğinizde bunları yalnızca Internet olarak yükleyebilirsiniz.
>
> Bir mobil cihazı Internet tabanlı bir yönetim noktası kullanacak şekilde yapılandırdığınızda, otomatik olarak yalnızca Internet olarak yapılandırılır.

İnternet ve intranet istemci yönetimi için diğer istemcileri yapılandırabilirsiniz. Ağ değişikliğini algılarsa, otomatik olarak IBCM ile intranet istemci yönetimi arasında geçiş yapar. Bu istemciler intranet üzerindeki istemci bağlantılarını destekleyen bir yönetim noktasını bulup bağlanabiliyorsa, bu istemciler intranet istemcileri olarak yönetilir. Intranet istemcilerinin tam Configuration Manager işlevselliği vardır. İstemciler intranet üzerindeki istemci bağlantılarını destekleyen bir yönetim noktası bulamazsa veya bağlanamıyorsa, Internet tabanlı bir yönetim noktasına bağlanmaya çalışırlar. Bu eylem başarılı olursa bu istemciler, kendilerine atanan sitelerindeki Internet tabanlı site sistemleri tarafından yönetilir.

Otomatik geçiş içindeki avantaj, istemcilerin intranete bağlandıklarında tüm özellikleri kullanabilmesi ve internet 'te olduklarında gerekli yönetimi almasıdır. Internet üzerinde başlayan içerik indirme, intranette ve diğer yollardan sorunsuz bir şekilde sürdürülür.

## <a name="prerequisites"></a>Önkoşullar

Configuration Manager IBCM Aşağıdaki bağımlılıklara sahiptir:

- İstemciler Internet bağlantısı gerektirir. Configuration Manager, cihazın var olan internet bağlantısını kullanır. Mobil cihazların doğrudan internet bağlantısı olması gerekir. Tam istemci bilgisayarların doğrudan internet bağlantısı olabilir veya bir proxy Web sunucusu kullanarak bağlanabilirsiniz.

- IBCM 'yi destekleyen site sistemleri Internet bağlantısı gerektirir ve Active Directory bir etki alanında olmalıdır. Internet tabanlı site sistemleri, site sunucusunun Active Directory ormanı ile bir güven ilişkisi gerektirmez. Ancak, internet tabanlı yönetim noktası Windows kimlik doğrulamasını kullanarak kullanıcının kimliğini doğrulayabilirler, kullanıcı ilkelerini destekler. Windows kimlik doğrulaması başarısız olursa, yalnızca cihaz ilkelerini destekler.

    > [!NOTE]
    > Kullanıcı ilkelerini desteklemek için, **Istemci ilke** grubunda aşağıdaki istemci ayarlarını da etkinleştirin:
    >
    > - **İstemcilerde kullanıcı ilkesi yoklamayı etkinleştir**
    > - **İnternet istemcilerinden kullanıcı ilkesi isteklerini etkinleştir**  

- İnternet tabanlı istemciler ve site sistemi sunucuları için gereken sertifikaları dağıtmak ve yönetmek için bir ortak anahtar altyapısı (PKI). Daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../plan-design/network/pki-certificate-requirements.md).

- ICM 'yi destekleyen site sistemlerinin Internet tam etki alanı adları (FQDN) için genel DNS ana bilgisayar girişlerini kaydedin.

### <a name="client-communication-requirements"></a>İstemci iletişim gereksinimleri

Aradaki güvenlik duvarları veya proxy sunucular, internet tabanlı site sistemleri için istemci iletişimine izin vermelidir:

- HTTP 1.1 desteği  

- Çok parçalı MIME bağlantısının HTTP içerik türüne izin verme (çok parçalı/karışık ve uygulama/octet-stream)  

#### <a name="verbs"></a>Fiiller

Internet tabanlı site sistem sunucusu rolleri için aşağıdaki fiillere izin verin:

| Rol | Fiiller |
|------|-------|
| Yönetim noktası | -HEAD<br>-CCM_POST<br>-BITS_POST<br>- GET<br>-PROPFIND |
| Dağıtım noktası | -HEAD<br>- GET<br>-PROPFIND |
| Geri dönüş durumu noktası | POST |
| Uygulama Kataloğu web sitesi noktası | -GÖNDERI<br>-Al |

#### <a name="http-headers"></a>HTTP üstbilgileri

Internet tabanlı site sistem sunucusu rolleri için aşağıdaki HTTP üst bilgilerine izin ver:

| Rol | HTTP üstbilgileri |
|------|--------------|
| Yönetim noktası | Aralığı<br>-Ccmclientıd:<br>-Ccmclienentidsignature:<br>-CCMClientTimestamp:<br>-Ccmclienttimestamp Ssignature: |
| Dağıtım noktası | Aralık: |

Internet 'ten istemci bağlantıları için yazılım güncelleştirme noktasını kullandığınızda benzer iletişim gereksinimleri için Windows Server Update Services (WSUS) belgelerine bakın.

## <a name="unsupported-features"></a>Desteklenmeyen özellikler

İstemci yönetimi işlevlerinin tümü Internet için uygun değildir. Configuration Manager, internet üzerindeki istemciler için bazı özellikleri desteklemez. Bu desteklenmeyen özellikler genellikle Active Directory Domain Services kullanır veya ortak bir ağ için uygun değildir.

Internet 'teki istemcileri ıCMLE yönetirken aşağıdaki özellikler desteklenmez:

- Internet üzerinden istemci dağıtımı (örneğin, istemci gönderme ve yazılım güncelleştirme tabanlı istemci dağıtımı). El ile istemci yükleme kullanın.

- Otomatik site ataması

- LAN 'da uyandırma

- İşletim sistemi dağıtımı. Ancak, bir işletim sistemini dağıtmayan görev dizilerini dağıtabilirsiniz.

- Uzaktan denetim

- Kullanıcılara yazılım dağıtımı. Bu özellik kullanım dışı olan uygulama Kataloğu ' na bağımlıdır.

- İstemci dolaşımı. Dolaşım, istemcilerin, içerik indirmek için daima en yakın dağıtım noktalarını bulmasına olanak sağlar. İstemciler, bant genişliği veya fiziksel konum ne olursa olsun, Internet tabanlı site sistemlerinden birini belirleyici olmayan şekilde seçer.

Bir yazılım güncelleştirme noktasını Internet 'ten gelen bağlantıları kabul edecek şekilde yapılandırdığınızda, Internet tabanlı istemciler hangi yazılım güncelleştirmelerinin gerektiğini öğrenmek için her zaman bu yazılım güncelleştirme noktasını tarar. Bu istemciler Internet üzerinde olduğunda, önce yazılım güncelleştirmelerini Internet tabanlı bir dağıtım noktasından değil Microsoft Update karşıdan yüklemeye çalışır. Bu davranış başarısız olursa, gerekli yazılım güncelleştirmelerini Internet tabanlı bir dağıtım noktasından indirmeyi denerler.

> [!TIP]
> Configuration Manager istemcisi, intranet veya Internet üzerinde olup olmadığını otomatik olarak belirler. İstemci bir etki alanı denetleyicisiyle veya şirket içi bir yönetim noktasıyla iletişim kurabildiğinden, bağlantı türünü "Şu an *intranet*" olarak ayarlar. Aksi halde, "Şu anda *İnternet*" e geçiş yapar ve sitesine atanan site sistemleriyle iletişim kurar.
