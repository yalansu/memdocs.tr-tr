---
title: Site yönetimi güvenliği ve gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager 'de site yönetimi için güvenliği ve gizliliği iyileştirin
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182268"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Configuration Manager 'de site yönetimi için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale Configuration Manager siteler ve hiyerarşi için güvenlik ve gizlilik bilgilerini içerir.

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a>Site yönetimi için Güvenlik Kılavuzu

Configuration Manager siteleri ve hiyerarşiyi güvenli hale getirmenize yardımcı olması için aşağıdaki kılavuzu kullanın.  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>Kurulumu güvenilir bir kaynaktan çalıştırın ve güvenli iletişim

Bir kişinin kaynak dosyalar üzerinde oynanmasını önlemek için Configuration Manager Kurulum 'u güvenilir bir kaynaktan çalıştırın. Dosyaları ağda depolarsanız ağ konumunun güvenliğini sağlayın.  

Kurulum 'u bir ağ konumundan çalıştırırsanız, bir saldırganın ağ üzerinden aktarıldıkları dosyalar üzerinde oynanmasını önlemek için, kurulum dosyalarının kaynak konumu ve site sunucusu arasında IPSec veya SMB imzalama kullanın.  

Kurulum 'un gerektirdiği dosyaları indirmek için kurulum yükleyici 'yi kullanırsanız, bu dosyaların depolandığı konumun güvenli olduğundan emin olun. Ayrıca, kurulum 'u çalıştırdığınızda bu konum için iletişim kanalının güvenliğini sağlayın.  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Active Directory Şemayı genişletme ve siteleri etki alanına yayımlama  

Şema uzantıları Configuration Manager çalıştırmak için gerekli değildir, ancak daha güvenli bir ortam oluşturur. İstemciler ve site sunucuları, güvenilir bir kaynaktan bilgi alabilir.  

İstemciler güvenilmeyen bir etki alanındaysa, aşağıdaki site sistem rollerini istemcilerin etki alanlarına dağıtın:  

- Yönetim noktası  

- Dağıtım noktası  

> [!NOTE]  
> Configuration Manager için güvenilen bir etki alanı Kerberos kimlik doğrulaması gerektirir. İstemciler, site sunucusunun ormanıyla iki yönlü bir orman güvenine sahip olmayan başka bir ormandaysa, bu istemciler güvenilmeyen bir etki alanında olduğu kabul edilir. Bu amaçla bir dış güven yeterli değildir.  

### <a name="use-ipsec-to-secure-communications"></a>İletişimleri güvenli hale getirmek için IPSec kullanın

Configuration Manager, site sunucusu ile SQL Server çalıştıran bilgisayar arasındaki iletişimin güvenliğini sağlasa da Configuration Manager, site sistem rolleri ve SQL Server arasındaki iletişimin güvenliğini sağlamaz. Yalnızca bazı site sistemlerini, site içi iletişim için HTTPS ile yapılandırabilirsiniz.  

Bu sunucudan sunucuya kanalların güvenliğini sağlamak için ek denetimler kullanmıyorsanız saldırganlar, site sistemlerine karşı çeşitli sahtekarlık ve ortadaki adam saldırıları kullanabilir. IPSec 'i kullanamadığınızda SMB imzalamayı kullanın.  

> [!Important]  
> Site sunucusu ve paket kaynak sunucusu arasındaki iletişim kanalını güvenli hale getirin. Bu iletişimde SMB kullanılır. Bu iletişimin güvenliğini sağlamak için IPSec 'i kullanmanızın ardından, istemciler tarafından İndirilme ve çalıştırılmadan önce dosyaların değiştirilmediğinden emin olmak için SMB imzalamayı kullanın.  

### <a name="dont-change-the-default-security-groups"></a>Varsayılan güvenlik gruplarını değiştirmeyin

Configuration Manager, site sistem iletişimi için oluşturduğu ve yönettiği aşağıdaki güvenlik gruplarını değiştirmeyin:

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;sitekodu\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitekodu\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitekodu\>**  

Configuration Manager, bu güvenlik gruplarını otomatik olarak oluşturur ve yönetir. Bu davranış, bir site sistem rolü kaldırıldığında bilgisayar hesaplarının kaldırılmasını içerir.  

Hizmet devamlılığını ve en düşük ayrıcalıklara sahip olduğundan emin olmak için bu grupları el ile düzenlemeyin.  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>Güvenilen kök anahtar sağlama işlemini yönetme

İstemciler Configuration Manager bilgileri için genel kataloğu sorgulayamiyorsa, geçerli yönetim noktalarının kimliğini doğrulamak için güvenilen kök anahtara güvenmelidir. Güvenilen kök anahtar, istemci kayıt defterinde depolanır. Bu, Grup İlkesi veya el ile yapılandırma kullanılarak ayarlanabilir.  

İstemci, bir yönetim noktasıyla ilk kez iletişim kurmadan önce güvenilen kök anahtarın bir kopyasına sahip değilse, iletişim kurduğu ilk yönetim noktasına güvenir. Saldırganların istemcileri yetkisiz bir yönetim noktasına yönlendirmesi riskini azaltmak için güvenilen kök anahtarı istemcilere önceden sağlayabilirsiniz. Daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="use-non-default-port-numbers"></a>Varsayılan olmayan bağlantı noktası numaralarını kullan

Varsayılan olmayan bağlantı noktası numaralarını kullanmak, ek güvenlik sağlayabilir. Saldırganlar, saldırganların bir saldırının hazırlanması için ortamı keşfetmenizi zorlaştırır. Varsayılan olmayan bağlantı noktalarını kullanmaya karar verirseniz, Configuration Manager yüklemeden önce bunları planlayın. Bunları hiyerarşideki tüm sitelerde tutarlı bir şekilde kullanın. İstemci istek bağlantı noktaları ve LAN'da Uyandırma, varsayılan olmayan bağlantı noktası numaralarını kullanabileceğiniz örneklerdir.  

### <a name="use-role-separation-on-site-systems"></a>Site sistemlerinde rol ayrımı kullanma

Tüm site sistem rollerini tek bir bilgisayara yükleyebilseniz de, bu uygulama üretim ağlarında nadiren kullanılır. Tek bir hata noktası oluşturur.  

### <a name="reduce-the-attack-profile"></a>Saldırı profilini azaltma

Her site sistemi rolünü farklı bir sunucuda yalıtmak, bir site sistemindeki güvenlik açıklarına karşı bir saldırının farklı bir site sistemine karşı kullanılabilme olasılığını azaltır. Birçok rol site sisteminde Internet Information Services (IIS) yüklenmesini gerektirir ve bu gereksinim saldırı yüzeyini artırır. Donanım harcamalarını azaltmak için rolleri birleştirmeniz gerekiyorsa, IIS rollerini yalnızca IIS gerektiren diğer rollerle birleştirin.  

> [!IMPORTANT]  
> Geri dönüş durum noktası rolü bir özel durumdur. Bu site sistemi rolü istemcilerden kimliği doğrulanmamış verileri kabul ettiğinden, geri dönüş durum noktası rolünü başka bir Configuration Manager site sistemi rolüne atamayın.  

### <a name="configure-static-ip-addresses-for-site-systems"></a>Site sistemleri için statik IP adresleri yapılandırma

Statik IP adresleri, ad çözümlemesi saldırılarına karşı daha kolay korunur.  

Statik IP adresleri IPSec yapılandırmasını da kolaylaştırır. IPSec kullanmak Configuration Manager içindeki site sistemleri arasındaki iletişimin güvenliğini sağlamaya yönelik en iyi güvenlik uygulamasıdır.  

### <a name="dont-install-other-applications-on-site-system-servers"></a>Diğer uygulamaları site sistemi sunucularına yüklemeyin

Site sistemi sunucularına diğer uygulamaları yüklediğinizde, Configuration Manager için saldırı yüzeyini artırırsınız. Ayrıca uyumsuzluk sorunlarıyla karşılaşırsınız.  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>İmzalama gerektir ve bir site seçeneği olarak şifrelemeyi etkinleştir

Site için imzalama ve şifreleme seçeneklerini etkinleştirin. Tüm istemcilerin SHA-256 karma algoritmasını destekleyediğinden emin olun ve ardından **SHA-256 gerektirme**seçeneğini etkinleştirin.  

### <a name="restrict-and-monitor-administrative-users"></a>Yönetici kullanıcılarını kısıtlama ve izleme

Yalnızca güvendiğiniz kullanıcılara Configuration Manager için yönetici erişimi verin. Ardından, yerleşik güvenlik rollerini kullanarak veya güvenlik rollerini özelleştirerek onlara minimum izinleri verin. Yazılım ve yapılandırmaların oluşturabileceğiniz, değiştirebileceği ve dağıtabilecek yönetici kullanıcılar Configuration Manager hiyerarşisindeki cihazları denetleyebilir.  

Gereken değişiklikleri doğrulamak için yönetim kullanıcısı atamalarını ve bunların yetki düzeyini belirli aralıklarla denetleyin.  

Daha fazla bilgi için bkz. [rol tabanlı yönetimi yapılandırma](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="secure-configuration-manager-backups"></a>Güvenli Configuration Manager yedeklemeleri

Configuration Manager yedekleme sırasında bu bilgiler, bir saldırgan tarafından kimliğe bürünme için kullanılabilecek sertifikaları ve diğer hassas verileri içerir.  

Bu verileri ağ üzerinden aktardığınızda SMB imzalama veya IPsec kullanın ve yedekleme konumunun güvenliğini sağlayın.  

### <a name="secure-locations-for-exported-objects"></a>İçe aktarılmış nesneler için güvenli konumlar

Configuration Manager konsolundan bir ağ konumuna nesne aktardığınızda veya içeri aktardığınızda, konumun güvenliğini sağlayın ve ağ kanalının güvenliğini sağlayın.

Ağ klasörüne erişebilecek kişileri kısıtlayın.  

Bir saldırganın, dışarıya aktarılmış verileri izinsiz almasını engellemek için ağ konumu ile site sunucusu arasında SMB imzalama veya IPSec kullanın. Ayrıca, Configuration Manager konsolunu ve site sunucusunu çalıştıran bilgisayar arasındaki iletişimin güvenliğini sağlayın. Bilgilerin açığa çıkmasını önlemek amacıyla ağdaki verileri şifrelemek için IPsec kullanın.  

### <a name="manually-remove-certificates-from-failed-servers"></a>Hatalı sunuculardan sertifikaları el ile kaldırma

Bir site sistemi düzgün şekilde kaldırılamıyorsa veya çalışmayı durdurmazsa ve geri yüklenemezse, bu sunucunun Configuration Manager sertifikalarını diğer Configuration Manager sunucularından el ile kaldırın.

Site sistemi ve site sistemi rolleriyle başlangıçta kurulan eş güvenini kaldırmak için, diğer site sistem sunucularındaki **güvenilir kişiler** sertifika deposundaki başarısız sunucuya yönelik Configuration Manager sertifikalarını el ile kaldırın. Sunucuyu yeniden biçimlendirmeden tekrar kullanırsanız bu eylem önemlidir.  

Daha fazla bilgi için bkz. [sunucu iletişimi Için şifreleme denetimleri](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication).  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>Internet tabanlı site sistemlerini çevre ağı köprülemek için yapılandırmayın

Site sistemi sunucularını, çevre ağına ve intranete bağlanacak şekilde birden çok bağlantılı olacak şekilde yapılandırmayın. Bu yapılandırma, Internet tabanlı site sistemlerinin Internet ve intranet 'ten gelen istemci bağlantılarını kabul etmesine izin verse de, çevre ağı ile intranet arasındaki güvenlik sınırını ortadan kaldırır.  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>Site sunucusunu çevre ağlarına bağlantıları başlatacak şekilde yapılandırma

Bir site sistemi, çevre ağı gibi güvenilmeyen bir ağdaysa, site sunucusunu site sistemine bağlantıları başlatacak şekilde yapılandırın.

Varsayılan olarak, site sistemleri veri aktarmak için site sunucusuna bağlantıları başlatır. Bu yapılandırma, bağlantı başlatma güvenilmeyen bir ağdan güvenilir ağa geldiğinde bir güvenlik riski oluşturabilir. Site sistemleri Internet 'ten gelen bağlantıları kabul ettiğinde veya güvenilmeyen bir ormanda bulunuyorsa, site **sunucusunun bu site sistemine yönelik bağlantıları başlatmasını gerektirmek**için site sistemi seçeneğini yapılandırın. Site sistemi ve herhangi bir rolün yüklenmesinden sonra, tüm bağlantılar site sunucusu tarafından güvenilen ağdan başlatılır.  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>Kimlik doğrulamasıyla SSL köprülemeyi ve sonlandırmayı kullanma

Internet tabanlı istemci yönetimi için bir Web proxy sunucusu kullanıyorsanız, kimlik doğrulamasıyla sonlandırma kullanarak SSL 'ye SSL köprülemesi kullanın.

Proxy Web sunucusunda SSL sonlandırmasını yapılandırdığınızda, Internet 'ten gelen paketler iç ağa iletilmeden önce inceme tabidir. Proxy Web sunucusu istemciden bağlantının kimliğini doğrular, sonlandırır ve ardından Internet tabanlı site sistemlerine yeni bir kimliği doğrulanmış bağlantı açar.  

Configuration Manager istemci bilgisayarları, Internet tabanlı site sistemlerine bağlanmak için bir proxy Web sunucusu kullandıklarında, istemci kimliği (GUID), paket yükünün içinde güvenli bir şekilde bulunur. Daha sonra yönetim noktası, proxy Web sunucusunu istemci olarak kabul etmez.

Proxy Web sunucunuz SSL köprüleme gereksinimlerini destekleyemiyorum, SSL tüneli de desteklenir. Bu seçenek daha az güvenlidir. İnternet 'ten gelen SSL paketleri sonlandırma olmadan site sistemlerine iletilir. Daha sonra kötü amaçlı içerik için denetlenemiyor.  

> [!WARNING]  
> Configuration Manager tarafından kaydedilen mobil cihazlar SSL köprülemesini kullanamaz. Yalnızca SSL tüneli kullanmaları gerekir.  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>Siteyi yazılım yüklemek üzere bilgisayarları uyandırmak için yapılandırırsanız kullanılacak yapılandırma

- Geleneksel uyandırma paketleri kullanıyorsanız, alt ağa yönelik yayınlar yerine tek noktaya yayın kullanın.  

- Alt ağa yönelik yayınlar kullanmanız gerekiyorsa, yönlendiricileri yalnızca site sunucusundan ve yalnızca varsayılan olmayan bir bağlantı noktası numarasından IP 'ye yönelik yayınlara izin verecek şekilde yapılandırın.  

Farklı LAN'da Uyandırma teknolojileri hakkında daha fazla bilgi için bkz. [istemcileri uyandırmayı planlama](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>E-posta bildirimi kullanırsanız, SMTP posta sunucusuna kimlik doğrulamalı erişimi yapılandırın

Mümkün olduğunda, kimlik doğrulamalı erişimi destekleyen bir posta sunucusu kullanın. Kimlik doğrulaması için site sunucusunun bilgisayar hesabını kullanın. Kimlik doğrulaması için bir kullanıcı hesabı belirtmeniz gerekiyorsa, en az ayrıcalığa sahip bir hesabı kullanın 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>LDAP kanalı bağlamayı ve LDAP imzalamayı zorla

Active Directory etki alanı denetleyicilerinin güvenliği, sunucuyu imzalama isteğinde bulunmayan Basit Kimlik Doğrulama ve Güvenlik Katmanı (SASL) LDAP bağlamalarını reddedecek şekilde yapılandırarak veya şifresiz bir metin bağlantısında gerçekleştirilen LDAP basit bağlamalarını reddedecek şekilde yapılandırılarak artırılabilir. Sürüm 1910 ' den başlayarak, Configuration Manager LDAP kanalı bağlamayı ve LDAP imzalamayı zorlamayı destekler. Daha fazla bilgi için bkz. [Windows için 2020 LDAP kanalı bağlama ve LDAP imzalama gereksinimleri](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows). <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a>Site sunucusu için Güvenlik Kılavuzu

Configuration Manager site sunucusunu güvenli hale getirmenize yardımcı olması için aşağıdaki kılavuzu kullanın.  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>Configuration Manager etki alanı denetleyicisi yerine üye sunucuya yükler

Configuration Manager site sunucusu ve site sistemleri, bir etki alanı denetleyicisine yükleme gerektirmez. Etki alanı denetleyicilerinin, etki alanı veritabanı dışında bir yerel güvenlik hesapları yönetimi (SAM) veritabanı yoktur. Bir üye sunucuya Configuration Manager yüklediğinizde, Configuration Manager hesaplarını etki alanı veritabanı yerine yerel SAM veritabanında koruyabilirsiniz.  

Bu uygulama, etki alanı denetleyicilerinizdeki saldırı yüzeyini de azaltır.  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>Dosyaları ağ üzerinden kopyalamadan ikincil siteleri yükler

Kurulum 'u çalıştırdığınızda ve ikincil site oluşturduğunuzda, dosyaları üst siteden ikincil siteye kopyalama seçeneğini seçmeyin. Ayrıca bir ağ kaynağı konumu kullanmayın. Dosyaları ağ üzerinden kopyaladığınızda, nitelikli bir saldırgan ikincil site yükleme paketini verebilir ve yüklenmeden önce dosyalarla oynayabilir. Bu saldırının zamanlaması zor olabilir. Bu saldırı, dosyaları aktarırken IPsec veya SMB kullanılarak azaltılabilir.  

Dosyaları ağ üzerinden kopyalamak yerine, ikincil site sunucusunda, kaynak dosyaları medya klasöründen yerel bir klasöre kopyalayın. Ardından, bir ikincil site oluşturmak üzere kurulum 'u çalıştırdığınızda, **yükleme kaynak dosyaları** sayfasında, **ikincil site bilgisayarında aşağıdaki konumdaki kaynak dosyaları kullan (en güvenli)** öğesini seçin ve bu klasörü belirtin.  

Daha fazla bilgi için bkz. [ikincil site yüklemesi](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary).

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>Site rolü yüklemesi, sürücü kökünden izinleri devralır

<!-- SCCMDocs#1380 -->
İlk site sistem rolünü herhangi bir sunucuya yüklemeden önce sistem sürücüsü izinlerini doğru şekilde yapılandırdığınızdan emin olun. Örneğin, `C:\SMS_CCM` öğesinden `C:\`izinleri devralır. Sürücünün kökü düzgün bir şekilde güvenli değilse, düşük haklara sahip kullanıcılar Configuration Manager klasöre erişebilir veya içeriği değiştirebilir.


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a>SQL Server için Güvenlik Kılavuzu

Configuration Manager, arka uç veritabanı olarak SQL Server kullanır. Veritabanı tehlikeye girerse, saldırganlar Configuration Manager atlayabilir. SQL Server doğrudan erişim altına alıyorsa, Configuration Manager aracılığıyla saldırıları başlatabilir. SQL Server karşı saldırıları, yüksek riskli ve uygun şekilde hafifletmeye karşı düşünün.  

Configuration Manager için SQL Server güvenli hale getirmenize yardımcı olması için aşağıdaki güvenlik kılavuzunu kullanın.  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>Configuration Manager site veritabanı sunucusunu diğer SQL Server uygulamalarını çalıştırmak için kullanmayın

Configuration Manager site veritabanı sunucusuna erişimi artırdığınızda, bu eylem Configuration Manager verilerinize yönelik riski artırır. Configuration Manager site veritabanı tehlikeye atılırsa, aynı SQL Server bilgisayardaki diğer uygulamalar da riske konur.  

### <a name="configure-sql-server-to-use-windows-authentication"></a>Windows kimlik doğrulamasını kullanmak için SQL Server yapılandırma

Configuration Manager, site veritabanına bir Windows hesabı ve Windows kimlik doğrulaması kullanarak erişse de, SQL Server karma mod SQL Server kullanmak üzere yapılandırmak yine de mümkündür. SQL Server karışık mod, veritabanına erişmek için ek SQL oturum açma işlemlerinin yapılmasına izin verir. Bu yapılandırma gerekli değildir ve saldırı yüzeyini artırır.  

### <a name="update-sql-server-express-at-secondary-sites"></a>İkincil sitelerde güncelleştirme SQL Server Express

Bir birincil site yüklediğinizde, Microsoft Indirme merkezi 'nden SQL Server Express indirir Configuration Manager. Ardından, dosyaları birincil site sunucusuna kopyalar. Bir ikincil site yüklediğinizde ve SQL Server Express yükleyen seçeneği seçtiğinizde, Configuration Manager daha önce indirilen sürümü yükler. Yeni sürümlerin kullanılabilir olup olmadığını denetlemez. İkincil sitenin en son sürümlere sahip olduğundan emin olmak için aşağıdaki görevlerden birini yapın:  

- İkincil siteyi yükledikten sonra, ikincil site sunucusunda Windows Update çalıştırın.  

- İkincil siteyi yüklemeden önce, ikincil site sunucusuna SQL Server Express el ile yükleyebilirsiniz. En son sürümü ve tüm yazılım güncelleştirmelerini yüklediğinizden emin olun. Ardından ikincil siteyi yükledikten sonra var olan bir SQL Server örneğini kullanma seçeneğini belirleyin.  

Tüm yüklü SQL Server sürümleri için Windows Update düzenli olarak çalıştırın. Bu uygulama, en son yazılım güncelleştirmelerine sahip olduklarından emin olmanızı sağlar.  

### <a name="follow-general-guidance-for-sql-server"></a>SQL Server için genel yönergeleri izleyin

SQL Server sürümünüz için genel yönergeleri belirleyip izleyin. Ancak, Configuration Manager için aşağıdaki gereksinimleri dikkate alın:  

- Site sunucusunun bilgisayar hesabının, SQL Server çalıştıran bilgisayarda Yöneticiler grubunun bir üyesi olması gerekir. "Yönetici sorumlularını açık olarak sağla" SQL Server önerisini izlerseniz, site sunucusunda kurulum 'u çalıştırmak için kullandığınız hesabın SQL kullanıcıları grubunun bir üyesi olması gerekir.  

- SQL Server bir etki alanı kullanıcı hesabı kullanarak yüklerseniz, site sunucusu bilgisayar hesabının Active Directory Domain Services yayımlanan bir hizmet asıl adı (SPN) için yapılandırıldığından emin olun. SPN olmadan, Kerberos kimlik doğrulaması başarısız olur ve Configuration Manager Kurulum başarısız olur.  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a>IIS çalıştıran site sistemleri için Güvenlik Kılavuzu

Configuration Manager içindeki çeşitli site sistem rolleri IIS gerektirir. IIS güvenliğini sağlama işlemi Configuration Manager düzgün şekilde çalışmasını sağlar ve güvenlik saldırılarına karşı risk düzeyini azaltır. Pratik olduğunda, IIS gerektiren sunucu sayısını en aza indirin. Örneğin, internet tabanlı istemci yönetimi için yüksek kullanılabilirlik ve Ağ yalıtımını dikkate alarak, yalnızca istemci tabanınızı desteklemek için ihtiyaç duyduğunuz yönetim noktası sayısını çalıştırın.  

IIS çalıştıran site sistemlerini güvenli hale getirmenize yardımcı olması için aşağıdaki kılavuzu kullanın.  

### <a name="disable-iis-functions-that-you-dont-require"></a>İhtiyacınız olmayan IIS işlevlerini devre dışı bırakma

Yüklediğiniz site sistem rolü için yalnızca en az IIS özelliklerini yükleyin. Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../configs/site-and-site-system-prerequisites.md).  

### <a name="configure-the-site-system-roles-to-require-https"></a>Site sistem rollerini HTTPS gerektirecek şekilde yapılandırma

İstemciler HTTPS yerine HTTP kullanarak bir site sistemine bağlandığında Windows kimlik doğrulaması kullanırlar. Bu davranış, Kerberos kimlik doğrulaması yerine NTLM kimlik doğrulaması kullanmaya geri dönebilir. NTLM kimlik doğrulaması kullanıldığında, istemciler yanlış bir sunucuya bağlanabilir.  

Bu kılavuzun özel durumu dağıtım noktaları olabilir. Dağıtım noktası HTTPS için yapılandırıldığında paket erişim hesapları çalışmaz. Paket erişim hesapları, içeriğe kimlik doğrulama sağlar, böylelikle içeriğe hangi kullanıcıları erişebileceği kısıtlaması yapabilirsiniz. Daha fazla bilgi için bkz. [içerik yönetimi için En Iyi güvenlik uygulamaları](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>IIS 'de site sistem rolleri için bir sertifika güven listesi (CTL) yapılandırma

Site sistemi rolleri:  

- HTTPS için yapılandırdığınız bir dağıtım noktası  

- HTTPS için yapılandırdığınız ve mobil cihazları destekleyecek şekilde etkinleştiren bir yönetim noktası

CTL, güvenilen kök sertifika yetkililerinin (CAs) tanımlı bir listesidir. Grup İlkesi ve ortak anahtar altyapısı (PKI) dağıtımı ile bir CTL kullandığınızda, bir CTL, ağınızda yapılandırılmış var olan güvenilen kök CA 'Ları kullanmanıza olanak sağlar. Örneğin, Microsoft Windows ile otomatik olarak yüklenen veya Windows kuruluş kök CA 'ları üzerinden eklenen CA 'Lar. Bir CTL, IIS içinde yapılandırıldığında, bu güvenilen kök CA 'Ların bir alt kümesini tanımlar.  

Bu alt küme, güvenlik üzerinde daha fazla denetim sağlar. CTL, kabul edilen istemci sertifikalarını, yalnızca CTL 'deki CA 'Lar listesinden verilen sertifikalara kısıtlar. Örneğin, Windows, VeriSign ve Thawte gibi çok sayıda tanınmış, üçüncü taraf CA sertifikalarıyla birlikte gelir.

Varsayılan olarak, IIS çalıştıran bilgisayar, bu iyi bilinen CA 'Lara zincirlenen sertifikalara güvenir. IIS 'yi listelenen site sistem rolleri için bir CTL ile yapılandırmadığınızda, site geçerli bir istemci olarak kabul eder ve bu CA 'lardan bir sertifikaya sahip olan herhangi bir cihaz vardır. IIS 'yi bu CA 'Ları içermeyen bir CTL ile yapılandırırsanız, sertifika bu CA 'Lara zincirde olursa site istemci bağlantılarını reddeder. Configuration Manager istemcilerin listelenen site sistem rolleri için kabul edilmesi için, IIS 'yi, Configuration Manager istemcileri tarafından kullanılan CA 'Ları belirten bir CTL ile yapılandırmanız gerekir.  

> [!NOTE]  
> Yalnızca listelenen site sistem rolleri, IIS 'de bir CTL yapılandırmanızı gerektirir. Configuration Manager yönetim noktaları için kullandığı sertifika verenler listesi, istemci bilgisayarlar için HTTPS yönetim noktalarına bağlandıklarında aynı işlevselliği sağlar.  

IIS 'de güvenilen CA 'Ların listesini yapılandırma hakkında daha fazla bilgi için bkz. IIS belgeleri.  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>Site sunucusunu IIS ile bir bilgisayara yerleştirmeyin

Rol ayırma, saldırı profilini azaltmaya ve kurtarılabilirliği iyileştirmeye yardımcı olur. Site sunucusunun bilgisayar hesabı genellikle tüm site sistem rollerinde yönetim ayrıcalıklarına sahiptir. İstemci anında yükleme kullanıyorsanız, Configuration Manager istemcilerinde da bu ayrıcalıklara sahip olabilir.  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Configuration Manager için adanmış IIS sunucuları kullanma

Configuration Manager tarafından da kullanılan IIS sunucularında birden çok Web tabanlı uygulamayı barındırabilseniz de, bu uygulama saldırı yüzeyinizi önemli ölçüde artırabilir. Kötü yapılandırılmış bir uygulama, bir saldırganın Configuration Manager site sisteminin denetimini sağlamasına izin verebilir. Bu ihlal, bir saldırganın hiyerarşinin denetimini sağlamasına izin verebilir.  

Configuration Manager site sistemlerinde başka web tabanlı uygulamalar çalıştırmanız gerekiyorsa, Configuration Manager site sistemleri için özel bir Web sitesi oluşturun.  

### <a name="use-a-custom-website"></a>Özel bir Web sitesi kullanma

IIS çalıştıran site sistemleri için Configuration Manager varsayılan Web sitesi yerine özel bir Web sitesi kullanacak şekilde yapılandırın. Site sisteminde başka web uygulamaları çalıştırmanız gerekiyorsa, özel bir Web sitesi kullanmanız gerekir. Bu ayar, belirli bir site sistemi için bir ayar yerine site genelinde bir ayardır.  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>Özel Web siteleri kullandığınızda, varsayılan sanal dizinleri kaldırın

Varsayılan Web sitesini kullanarak özel bir Web sitesi kullanmayı seçtiğinizde, eski sanal dizinleri kaldırmaz Configuration Manager. Configuration Manager ilk olarak varsayılan Web sitesi altında oluşturulan sanal dizinleri kaldırın.  

Örneğin, bir dağıtım noktası için aşağıdaki sanal dizinleri kaldırın:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>IIS sunucusu güvenlik kılavuzunu izleyin

IIS Server sürümünüz için genel yönergeleri belirleyip izleyin. Configuration Manager belirli site sistem rolleri için sahip olduğu tüm gereksinimleri dikkate alın. Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../configs/site-and-site-system-prerequisites.md).  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a>Yönetim noktası için Güvenlik Kılavuzu

Yönetim noktaları, aygıtlar ve Configuration Manager arasındaki birincil arabirimdir. Yönetim noktasına ve üzerinde çalıştığı sunucuya karşı saldırıları, yüksek riskli ve uygun şekilde azaltacak şekilde düşünün. Olağan dışı etkinlikler için uygun olan tüm güvenlik kılavuzlarını ve izleyiciyi uygulayın.  

Configuration Manager bir yönetim noktasının güvenliğini sağlamaya yardımcı olması için aşağıdaki kılavuzu kullanın.  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>İstemciyi bir yönetim noktasına aynı siteye atama

Yönetim noktasındaki Configuration Manager istemcisini yönetim noktasının sitesi dışında bir siteye atadığınız senaryodan kaçının.  

Önceki bir sürümden Configuration Manager geçerli dala geçiş yaparsanız, istemciyi yönetim noktasındaki yeni siteye en kısa sürede geçirin.  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a>Geri dönüş durum noktası için Güvenlik Kılavuzu

Configuration Manager bir geri dönüş durum noktası yüklerseniz aşağıdaki güvenlik kılavuzunu kullanın:

Bir geri dönüş durum noktası yüklerken güvenlik konuları hakkında daha fazla bilgi için, bkz. [geri dönüş durum noktası gerekip gerekmediğini belirleme](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>Aynı site sisteminde başka bir rol çalıştırmayın

Geri dönüş durum noktası, herhangi bir bilgisayardan kimliği doğrulanmamış iletişimi kabul etmek üzere tasarlanmıştır. Bu site sistem rolünü diğer rollerle veya bir etki alanı denetleyicisiyle çalıştırırsanız, bu sunucu riski büyük ölçüde artar.  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>PKI sertifikaları olan istemcileri yüklemeden önce geri dönüş durumu noktasını yükler

Configuration Manager site sistemleri HTTP istemci iletişimini kabul etmez, PKI ile ilgili sertifika sorunları nedeniyle istemcilerin yönetilmediğini bilmiyor olabilirsiniz. İstemcileri bir geri dönüş durum noktasına atarsanız, bu sertifika sorunlarını geri dönüş durum noktası üzerinden raporlarlar.  

Güvenlik nedenleriyle, bir geri dönüş durum noktasını, istemcilere yüklendikten sonra atayamazsınız. Bu rolü yalnızca istemci yüklemesi sırasında atayabilirsiniz.  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>Çevre ağında geri dönüş durum noktasını kullanmaktan kaçının

Tasarım olarak geri dönüş durum noktası tüm istemcilerden gelen verileri kabul eder. Çevre ağındaki bir geri dönüş durum noktası, Internet tabanlı istemcilerin sorunlarını gidermenize yardımcı olabilir, ancak, genel olarak erişilebilen bir ağda kimliği doğrulanmamış verileri kabul eden bir site sistemi riski ile sorun giderme avantajlarının dengesini sağlayabilirsiniz.  

Geri dönüş durum noktasını çevre ağına veya güvenilmeyen herhangi bir ağa yüklerseniz, site sunucusunu veri aktarımlarını başlatacak şekilde yapılandırın. Geri dönüş durum noktasının site sunucusuyla bir bağlantı başlatmasını sağlayan varsayılan ayarı kullanmayın.  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a>Site yönetimi için güvenlik sorunları

Configuration Manager için aşağıdaki güvenlik sorunlarını gözden geçirin:  

- Configuration Manager, ağa saldırmak için Configuration Manager kullanan yetkili bir yönetici kullanıcıya karşı savunması yoktur. Yetkisiz yönetici kullanıcılar yüksek bir güvenlik riskidir. Aşağıdaki stratejileri içeren birçok saldırı başlatabilir:  

    - Kuruluştaki tüm Configuration Manager istemci bilgisayarlarına otomatik olarak kötü amaçlı yazılım yüklemek ve çalıştırmak için yazılım dağıtımını kullanın.  

    - İstemci izni olmadan Configuration Manager istemcisini uzaktan denetleme.  

    - Hızlı yoklama aralıklarını ve çok büyük miktarlarda envanter yapılandırın. Bu eylem, istemcilere ve sunuculara karşı hizmet reddi saldırıları oluşturur.  

    - Diğer bir sitenin Active Directory verilerine veri yazmak için hiyerarşideki bir siteyi kullanın.  

    Site hiyerarşisi güvenlik sınırı. Siteleri yalnızca yönetim sınırları olacak şekilde düşünün.  

    Tüm yönetici kullanıcı etkinliğini denetleyin ve düzenli aralıklarla denetim günlüklerini gözden geçirin. Tüm Configuration Manager yönetici kullanıcıların, işe alınmadan önce bir arka plan denetimi olmasını gerektir. Çalışma koşulu olarak düzenli aralıklarla yeniden denetim gerektir.  

- Kayıt noktası tehlikeye girerse, bir saldırgan kimlik doğrulaması için sertifikalar alabilir. Mobil cihazlarını kaydeden kullanıcıların kimlik bilgilerini çalabilir.  

    Kayıt noktası bir CA ile iletişim kurar. Active Directory nesneleri oluşturabilir, değiştirebilir ve silebilir. Kayıt noktasını çevre ağına hiçbir şekilde yüklemeyin. Olağan dışı etkinlik için her zaman izleyin.  

- Internet tabanlı istemci yönetimi için Kullanıcı ilkelerine izin verirseniz, saldırı profilinizi artırabilirsiniz.  

    İstemci-sunucu bağlantıları için PKI sertifikalarının kullanılmasına ek olarak, bu yapılandırmalarda Windows kimlik doğrulaması gerekir. Kerberos yerine NTLM kimlik doğrulaması kullanmaya geri dönebilirler. NTML kimlik doğrulaması, kişiselleştirmeye ve yeniden gönderme saldırılarına açıktır. Internet 'teki bir kullanıcının kimliğini başarıyla doğrulamak için Internet tabanlı site sisteminden bir etki alanı denetleyicisine bağlantıya izin vermeniz gerekir.  

- **Yönetim $** paylaşımının site sistem sunucularında olması gerekir.  

    Configuration Manager site sunucusu, site sistemlerinde hizmet işlemlerine bağlanmak ve bu işlemleri yapmak için admin $ Share ' i kullanır. Bu paylaşıma devre dışı bırakma veya kaldırma.  

- Configuration Manager diğer bilgisayarlara bağlanmak için ad çözümleme hizmetleri 'ni kullanır. Bu hizmetler aşağıdaki güvenlik saldırılarına karşı güvenli hale getirmek için zordur:
    - Kandırma
    - İzinsiz Değişiklik
    - Kar
    - Bilgilerin açığa çıkması
    - Hizmet reddi
    - Ayrıcalık yükselmesi

    Ad çözümlemesi için kullandığınız DNS sürümüne ilişkin tüm güvenlik kılavuzlarını belirleyip izleyin.  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a>Bulma için gizlilik bilgileri

Keşif, ağ kaynakları için kayıtlar oluşturur ve bunları Configuration Manager veritabanında depolar. Bulgu veri kayıtları, IP adresleri, işletim sistemi sürümleri ve bilgisayar adları gibi bilgisayar bilgilerini içerir. Active Directory bulma yöntemlerini, kuruluşunuzun Active Directory Domain Services depoladığı tüm bilgileri döndürecek şekilde de yapılandırabilirsiniz.  

Configuration Manager varsayılan olarak tarafından izin veren tek bulma yöntemi, sinyal keşfi 'dir. Bu yöntem yalnızca Configuration Manager istemci yazılımının zaten yüklü olduğu bilgisayarları bulur.  

Bulma bilgileri doğrudan Microsoft 'a gönderilmez. Configuration Manager veritabanında depolanır. Configuration Manager, verileri silinceye kadar veritabanındaki bilgileri korur. Bu işlem, site bakım görevi **eski bulma verilerini sil**ile her 90 günde bir gerçekleşir.  
