---
title: Uç noktalar arasında iletişim
titleSuffix: Configuration Manager
description: Site sistemlerinin ve bileşenlerinin bir ağ üzerinden Configuration Manager nasıl iletişim kuracağını öğrenin.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f60d268e1f9bfad9c062041e810be2092da5508
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587243"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Configuration Manager uç noktaları arasındaki iletişim

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager site sistemleri ve istemcilerinin ağınız genelinde nasıl iletişim kurduğu açıklanmaktadır. Aşağıdaki bölümleri içerir:  

- [Bir sitedeki site sistemleri arasındaki iletişimler](#Planning_Intra-site_Com)  
  - [Site sunucusundan dağıtım noktasına](#bkmk_site2dp)  

- [İstemcilerden site sistemlerine ve hizmetlerine yönelik iletişimler](#Planning_Client_to_Site_System)  
  - [İstemciden yönetim noktasına iletişim](#bkmk_client2mp)  
  - [İstemciden dağıtım noktasına iletişim](#bkmk_client2dp)  
  - [İnternet 'ten veya güvenilmeyen bir ormandan gelen istemci iletişimleri ile ilgili konular](#BKMK_clientspan)  

- [Active Directory ormanlarda iletişim](#Plan_Com_X-Forest)  
  - [Site sunucunuzun ormanı tarafından güvenilmeyen bir ormandaki etki alanı bilgisayarlarını destekleme](#bkmk_noforesttrust)  
  - [Bir çalışma grubundaki bilgisayarları destekleme](#bkmk_workgroup)  
  - [Birden çok etki alanına ve ormana yayılan bir site veya hiyerarşiyi desteklemek için senaryolar](#bkmk_span)  

## <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a> Bir sitenin site sistemleri arasındaki iletişim  

Site sistemleri veya bileşenleri, ağ üzerinde diğer site sistemleri veya sitedeki bileşenlerle iletişim kurduğunda, siteyi nasıl yapılandırdığınıza bağlı olarak aşağıdaki protokollerden birini kullanırlar: Configuration Manager  

- Sunucu ileti bloğu (SMB)  

- HTTP  

- HTTPS  

Site sunucusundan bir dağıtım noktasına yönelik iletişim dışında, sitedeki sunucudan sunucuya iletişim herhangi bir zamanda gerçekleşebilir. Bu iletişimler ağ bant genişliğini denetlemek için mekanizmaları kullanmaz. Site sistemleri arasındaki iletişimi denetleyemediği için, site sistemi sunucularını hızlı ve iyi bağlanmış ağların bulunduğu konumlara yüklediğinizden emin olun.  

### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a>Site sunucusundan dağıtım noktasına

Site sunucusundan dağıtım noktalarına içerik aktarımını yönetmenize yardımcı olmak için aşağıdaki stratejileri kullanın:  

- Ağ bant genişliği denetimi ve zamanlama için dağıtım noktasını yapılandırın. Bu denetimler, siteler arası adresler tarafından kullanılan yapılandırmalara benzer. Uzak ağ konumlarına içerik aktarımı ana bant genişliğinizin dikkate alınması durumunda başka bir Configuration Manager sitesi yüklemek yerine bu yapılandırmayı kullanın.  

- Bir dağıtım noktasını, ön hazırlığı yapılan dağıtım noktası olarak yükleyebilirsiniz. Ön hazırlığı yapılan dağıtım noktası, dağıtım noktası sunucusuna el ile yerleştirilen içeriği kullanmanıza olanak sağlar ve içerik dosyalarını ağda aktarma gereksinimini ortadan kaldırır.  

Daha fazla bilgi için bkz. [içerik yönetimi için ağ bant genişliğini yönetme](manage-network-bandwidth.md).

## <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a> İstemcilerle site sistemleri ve hizmetleri arasındaki iletişimler

İstemciler, site sistem rolleri, Active Directory Domain Services ve çevrimiçi hizmetler iletişim başlatır. Bu iletişimleri etkinleştirmek için güvenlik duvarları istemciler ve iletişim uç noktaları arasındaki ağ trafiğine izin vermelidir. İstemciler tarafından bu uç noktalara iletişim kurduğunda kullanılan bağlantı noktaları ve protokoller hakkında daha fazla bilgi için, bkz. [Configuration Manager kullanılan bağlantı noktaları](ports.md).  

İstemcinin bir site sistem rolüyle iletişim kurabilmesi için, istemci, istemci protokolünü (HTTP veya HTTPS) destekleyen bir rol bulmak üzere hizmet konumunu kullanır. Varsayılan olarak, istemciler tarafından kullanılabilen en güvenli yöntemi kullanır. Daha fazla bilgi için bkz. [İstemcilerin site kaynaklarını ve hizmetleri nasıl bulduklarını anlama](understand-how-clients-find-site-resources-and-services.md).  

HTTPS kullanmak için aşağıdaki seçeneklerden birini yapılandırın:  

- Bir ortak anahtar altyapısı (PKI) kullanın ve PKI sertifikalarını istemcilere ve sunuculara yükler. Sertifikaların nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../network/pki-certificate-requirements.md).  

- Sürüm 1806 ' den başlayarak, siteyi **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanacak**şekilde yapılandırın. Daha fazla bilgi için bkz. [GELIŞMIŞ http](enhanced-http.md).  

Internet Information Services (IIS) kullanan ve istemcilerinden gelen iletişimi destekleyen bir site sistem rolü dağıttığınızda, istemcilerin site sistemine HTTP veya HTTPS kullanarak bağlandığını belirtmeniz gerekir. HTTP kullanırsanız imzalama ve şifreleme seçeneklerini de göz önünde bulundurmanız gerekir. Daha fazla bilgi için bkz. [imzalama ve şifrelemeyi planlama](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption).  

### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a>İstemciden yönetim noktasına iletişim

İstemci bir yönetim noktasıyla iletişim kurduğunda iki aşama vardır: kimlik doğrulaması (aktarım) ve yetkilendirme (ileti). Bu işlem, aşağıdaki faktörlere bağlı olarak farklılık gösterir:

- Site yapılandırması: yalnızca HTTPS, HTTP veya HTTPS 'ye izin verir veya gelişmiş HTTP özellikli HTTP veya HTTPS 'ye izin verir
- Yönetim noktası yapılandırması: HTTPS veya HTTP
- Cihaz merkezli senaryolar için cihaz kimliği
- Kullanıcı merkezli senaryolar için Kullanıcı kimliği

Bu işlemin nasıl çalıştığını anlamak için aşağıdaki tabloyu kullanın:  

| MP türü  | İstemci kimlik doğrulaması  | İstemci yetkilendirmesi<br>Cihaz kimliği  | İstemci yetkilendirmesi<br>Kullanıcı kimliği  |
|----------|---------|---------|---------|
| HTTP     | Anonim<br>Gelişmiş HTTP ile, site Azure AD *Kullanıcı* veya *cihaz* belirtecini doğrular. | Konum isteği: anonim<br>İstemci paketi: anonim<br>Kayıt, cihaz kimliğini kanıtlamak için aşağıdaki yöntemlerden birini kullanarak:<br> -Anonim (el ile onay)<br> -Windows-tümleşik kimlik doğrulaması<br> -Azure AD *cihaz* belirteci (Gelişmiş http)<br>Kayıt sonrasında istemci, cihaz kimliğini kanıtlamak için ileti imzalamayı kullanır | Kullanıcı merkezli senaryolar için, Kullanıcı kimliğini kanıtlamak üzere aşağıdaki yöntemlerden birini kullanarak:<br> -Windows-tümleşik kimlik doğrulaması<br> -Azure AD *Kullanıcı* belirteci (Gelişmiş http) |
| HTTPS    | Aşağıdaki yöntemlerden birini kullanarak:<br> -PKI sertifikası<br> -Windows-tümleşik kimlik doğrulaması<br> -Azure AD *Kullanıcı* veya *cihaz* belirteci | Konum isteği: anonim<br>İstemci paketi: anonim<br>Kayıt, cihaz kimliğini kanıtlamak için aşağıdaki yöntemlerden birini kullanarak:<br> -Anonim (el ile onay)<br> -Windows-tümleşik kimlik doğrulaması<br> -PKI sertifikası<br> -Azure AD *Kullanıcı* veya *cihaz* belirteci<br>Kayıt sonrasında istemci, cihaz kimliğini kanıtlamak için ileti imzalamayı kullanır | Kullanıcı merkezli senaryolar için, Kullanıcı kimliğini kanıtlamak üzere aşağıdaki yöntemlerden birini kullanarak:<br> -Windows-tümleşik kimlik doğrulaması<br> -Azure AD *Kullanıcı* belirteci |

> [!Tip]  
> Farklı cihaz kimlik türleri ve bulut yönetimi ağ geçidiyle yönetim noktası yapılandırması hakkında daha fazla bilgi için bkz. [https için yönetim noktasını etkinleştirme](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a>İstemciden dağıtım noktasına iletişim

Bir istemci bir dağıtım noktasıyla iletişim kurduğunda, içeriği indirmeden önce yalnızca kimlik doğrulaması gerekir. Bu işlemin nasıl çalıştığını anlamak için aşağıdaki tabloyu kullanın:

| DP türü  | İstemci kimlik doğrulaması  |
|----------|---------|
| HTTP     | -Anonim, izin veriliyorsa<br>-Bilgisayar hesabı veya ağ erişim hesabı ile Windows-tümleşik kimlik doğrulaması<br> -İçerik erişim belirteci (Gelişmiş HTTP) |
| HTTPS    | -PKI sertifikası<br> -Bilgisayar hesabı veya ağ erişim hesabı ile Windows-tümleşik kimlik doğrulaması<br> -İçerik erişim belirteci |

### <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a>İnternet 'ten veya güvenilmeyen bir ormandan gelen istemci iletişimleri ile ilgili konular

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Bulut yönetimi ağ geçidi planlama](../..//clients/manage/cmg/plan-cloud-management-gateway.md)

- [İnternet tabanlı istemci yönetimi için planlama](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a> Active Directory ormanları arası iletişim  

Configuration Manager, Active Directory ormanlara yayılan siteleri ve hiyerarşileri destekler. Ayrıca, site sunucusuyla aynı Active Directory ormanında olmayan etki alanı bilgisayarlarını ve çalışma gruplarındaki bilgisayarları destekler.  

### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a>Site sunucunuzun ormanı tarafından güvenilmeyen bir ormandaki etki alanı bilgisayarlarını destekleme

- Site sistemi rollerini, site bilgilerini ilgili Active Directory ormanında yayımlama seçeneğiyle birlikte bu güvenilmeyen ortama yükleme  

- Bu bilgisayarları çalışma grubu bilgisayarlıorlar gibi Yönet  

Site sistemi sunucularını güvenilmeyen bir Active Directory ormanına yüklediğinizde, bu ormandaki istemcilerden gelen istemciden sunucuya iletişim bu ormanda tutulur ve Configuration Manager Kerberos kullanarak bilgisayarın kimliğini doğrulayabilir. Site bilgilerini istemci ormanında yayımladığınızda, istemciler bu bilgileri atanan yönetim noktasından indirmek yerine, kullanılabilir yönetim noktaları gibi site bilgilerini Active Directory ormanından alma avantajlarından yararlanır.  

> [!NOTE]  
> İnternet üzerinde olan cihazları yönetmek istiyorsanız, site sistem sunucuları bir Active Directory ormanında olduğunda, çevre ağınıza Internet tabanlı site sistemi rolleri yükleyebilirsiniz. Bu senaryo, çevre ağı ile site sunucusunun ormanı arasında iki yönlü güven gerektirmez.  

### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a>Bir çalışma grubundaki bilgisayarları destekleme  

- Site sistemi rolleriyle HTTP istemci bağlantıları kullandığında çalışma grubu bilgisayarlarını el ile onaylayın. Configuration Manager, Kerberos kullanarak bu bilgisayarların kimliğini doğrulayamıyorum.  

- Bu bilgisayarların dağıtım noktalarından içerik alabilmeleri için bu çalışma grubu istemcilerini Ağ Erişim Hesabı kullanacak şekilde yapılandırın.  

- Çalışma grubu istemcilerinin yönetim noktalarını bulması için alternatif bir mekanizma belirtin. DNS yayımlama, WINS veya doğrudan bir yönetim noktası atama kullanın. Bu istemciler Active Directory Domain Services site bilgilerini alamıyor.  

Daha fazla bilgi için aşağıdaki makalelere bakın:  

- [Çakışan kayıtları yönetme](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

- [Ağ erişim hesabı](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [Çalışma grubu bilgisayarlarına Configuration Manager istemcileri nasıl yüklenir](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> Birden çok etki alanına ve ormana yayılan bir site veya hiyerarşiyi desteklemek için senaryolar  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Senaryo 1: ormana yayılan bir hiyerarşideki siteler arasındaki Iletişim

Bu senaryo, Kerberos kimlik doğrulamasını destekleyen iki yönlü bir orman güveni gerektirir.  Kerberos kimlik doğrulamasını destekleyen iki yönlü bir orman güveniniz yoksa Configuration Manager, uzak ormandaki bir alt siteyi desteklemez.  

Configuration Manager, üst sitenin ormanıyla gereken iki yönlü güvene sahip olan bir uzak ormana bir alt site yüklemeyi destekler. Örneğin, gereken güven mevcut olduğu sürece, ikincil bir siteyi birincil üst sitesinden farklı bir ormana yerleştirebilirsiniz.  

> [!NOTE]  
> Bir alt site, birincil site (merkezi yönetim sitesinin üst site olduğu yerde) veya ikincil bir site olabilir.  

Configuration Manager siteler arası iletişim, veritabanı çoğaltmasını ve dosya tabanlı aktarımları kullanır. Bir sitesi yüklediğinizde, sitenin belirtilen sunucuya yükleneceği bir hesap belirtmeniz gerekir. Bu hesap, siteler arasındaki iletişimi de kurup muhafaza eder. Site başarıyla yüklenip dosya tabanlı aktarımları ve veritabanı çoğaltmasını başlattıktan sonra, siteyle iletişim için başka bir şey yapılandırmanız gerekmez.  

İki yönlü bir orman güveni mevcut olduğunda, Configuration Manager ek yapılandırma adımları gerektirmez.  

Varsayılan olarak, yeni bir alt site yüklediğinizde Configuration Manager aşağıdaki bileşenleri yapılandırır:  

- Site sunucusu bilgisayar hesabını kullanan her sitede siteler arası dosya tabanlı çoğaltma yolu. Configuration Manager, her bilgisayarın bilgisayar hesabını hedef bilgisayardaki **&lt;SMS_SiteToSiteConnection_ sitekodu\> ** grubuna ekler.  

- Her sitedeki SQL Server 'Lar arasındaki veritabanı çoğaltması.  

Ayrıca aşağıdaki konfigürasyonları da ayarlayın:  

- Güvenlik duvarları ve ağ cihazları, Configuration Manager için gereken ağ paketlerine izin vermelidir.  

- Ad çözümlemesi ormanlar arasında çalışmalıdır.  

- Bir siteyi veya site sistemi rolünü yüklemek için, belirtilen bilgisayarda yerel yönetici izinlerine sahip olan bir hesap belirtmeniz gerekir.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Senaryo 2: ormanlara yayılan bir sitede Iletişim

Bu senaryo iki yönlü bir orman güveni gerektirmez.  

Birincil siteler, uzak ormanlardaki bilgisayarlara site sistem rolleri yüklemeyi destekler.  

- Uygulama Kataloğu web hizmeti noktası tek özel durumdur.  Yalnızca site sunucusuyla aynı ormanda desteklenir.  

- Bir site sistemi rolü internet 'ten gelen bağlantıları kabul ettiğinde, en iyi güvenlik uygulaması olarak, site sistemi rollerini orman sınırının site sunucusu için koruma sağladığı bir konuma (örneğin, bir çevre ağında) yükler.  

Site sistemi rolünü güvenilmeyen bir ormandaki bilgisayara yüklemek için:  

- Sitenin site sistem rolünü yüklemek için kullandığı bir **site sistemi yükleme hesabı**belirtin. (Bu hesap, bağlanmak için yerel yönetici kimlik bilgilerine sahip olmalıdır.) Ardından, belirtilen bilgisayara site sistem rollerini yükler.  

- Site **sunucusunun bu site sistemine yönelik bağlantıları başlatmasını gerektir**site sistemi seçeneğini belirleyin. Bu ayar, site sunucusunun veri aktarmak için site sistemi sunucusuyla bağlantı kurmasını gerektirir. Bu yapılandırma, güvenilmeyen konumdaki bilgisayarın, güvenilen ağınızda bulunan site sunucusuyla iletişim başlatmasını önler. Bu bağlantılar **Site Sistemi Yükleme Hesabı**’nı kullanır.  

Güvenilmeyen ormana yüklenmiş bir site sistemi rolünü kullanmak için site sunucusu veri aktarımını başlattığında bile güvenlik duvarlarının ağ trafiğine izin vermesi gerekir.  

Ek olarak, aşağıdaki site sistem rolleri site veritabanına doğrudan erişim gerektirir. Bu nedenle, güvenlik duvarları güvenilmeyen ormandan site SQL Server yönelik geçerli trafiğe izin vermelidir:  

- Varlık Yönetim Bilgileri eşitleme noktası  

- Uç Nokta Koruma noktası  

- Kayıt noktası  

- Yönetim noktası  

- Reporting services noktası  

- Durum Geçiş noktası  

Daha fazla bilgi için bkz. [Configuration Manager kullanılan bağlantı noktaları](ports.md).  

Yönetim noktasını ve kayıt noktası erişimini site veritabanına yapılandırmanız gerekebilir.

- Varsayılan olarak, bu rolleri yüklediğinizde Configuration Manager, yeni site sistemi sunucusunun bilgisayar hesabını site sistemi rolü için bağlantı hesabı olarak yapılandırır. Daha sonra hesabı uygun SQL Server veritabanı rolüne ekler.  

- Bu site sistemi rollerini güvenilmeyen bir etki alanına yüklediğinizde, site sistem rolünün veritabanından bilgi almasını sağlamak için site sistemi rolü bağlantı hesabını yapılandırın.  

Bir etki alanı kullanıcı hesabını bu site sistemi rollerinin bağlantı hesabı olacak şekilde yapılandırırsanız, etki alanı kullanıcı hesabının o sitedeki SQL Server veritabanına uygun erişime sahip olduğundan emin olun:  

- Yönetim noktası: **Yönetim Noktası Veritabanı Bağlantı Hesabı**  

- Kayıt noktası: **Kayıt Noktası Bağlantı Hesabı**  

Diğer ormanlardaki site sistemi rolleri için planlama yaparken aşağıdaki ek bilgileri göz önünde bulundurun:  

- Windows Güvenlik Duvarı 'nı çalıştırırsanız, site veritabanı sunucusu ile uzak site sistem rolleriyle yüklenen bilgisayarlar arasındaki iletişimleri geçirmek için ilgili Güvenlik Duvarı profillerini yapılandırın.

- Internet tabanlı yönetim noktası, Kullanıcı hesaplarını içeren ormana güvendiğinde, kullanıcı ilkeleri desteklenir. Hiçbir güven olmadığında, yalnızca bilgisayar ilkeleri desteklenir.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Senaryo 3: istemciler, site sunucusu ile aynı Active Directory ormanında olmadığında istemciler ve site sistemi rolleri arasındaki Iletişim

Configuration Manager, sitelerinin site sunucusuyla aynı ormanda bulunmayan istemciler için aşağıdaki senaryoları destekler:  

- İstemci ormanı ve site sunucusunun ormanı arasında iki yönlü bir orman güveni vardır.  

- Site sistemi rol sunucusu, istemcisiyle aynı ormanda bulunur.  

- İstemci, site sunucusuyla iki yönlü bir orman güvenine sahip olmayan bir etki alanı bilgisayarındaysa ve site sistem rolleri istemcinin ormanında yüklü değildir.  

- İstemci bir çalışma grubu bilgisayarsıdır.  

Etki alanına katılmış bir bilgisayardaki istemciler, siteleri Active Directory ormanında yayımlandığında hizmet konumu için Active Directory Domain Services kullanabilir.  

Site bilgilerini başka bir Active Directory ormanına yayımlamak için:  

- Ormanı belirtin ve ardından **Yönetim** çalışma alanının **Active Directory Ormanları** düğümünde ilgili ormanda yayımlamayı etkinleştirin.  

- Her bir siteyi Active Directory Etki Alanı Hizmetleri'nde veri yayımlamak üzere yapılandırın. Bu yapılandırma, söz konusu ormandaki istemcileri site bilgilerini almak ve yönetim noktalarını bulmak üzere etkinleştirir. Hizmet konumu için Active Directory Domain Services kullanmayan istemcilerde DNS, WINS veya istemcinin atanmış yönetim noktasını kullanabilirsiniz.  

#### <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a>Senaryo 4: Exchange Server bağlayıcısını uzak bir ormana yerleştirme  

Bu senaryoyu desteklemek için, ormanlar arasında ad çözümlemesinin çalıştığından emin olun. Örneğin, DNS iletiletme yapılandırma. Exchange Server bağlayıcısını yapılandırırken Exchange Server 'ın intranet FQDN 'sini belirtin. Daha fazla bilgi için bkz. [Configuration Manager ve Exchange ile mobil cihazları yönetme](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="see-also"></a>Ayrıca bkz.

- [Güvenliği planlama](../security/plan-for-security.md)  

- [Configuration Manager istemcileri için güvenlik ve Gizlilik](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
