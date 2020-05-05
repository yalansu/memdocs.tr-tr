---
title: Şifreleme denetimleri teknik başvurusu
titleSuffix: Configuration Manager
description: İmzalama ve şifrelemenin, Configuration Manager içindeki verileri okumaktan nasıl yardımcı olabileceğini öğrenin.
ms.date: 12/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df289c284774a4e0bb3a379853f31f8d6f5bd44d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720600"
---
# <a name="cryptographic-controls-technical-reference"></a>Şifreleme denetimleri teknik başvurusu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Configuration Manager hiyerarşisindeki cihazların yönetimini korumaya yardımcı olmak üzere imzalama ve şifrelemeyi kullanır. İmzalama ile veriler aktarım sırasında değiştirilmişse, atılır. Şifreleme, bir saldırganın bir ağ protokolü Çözümleyicisi kullanarak verileri okumasını önlemeye yardımcı olur.  

 Configuration Manager imza için kullanılan birincil karma algoritması SHA-256 ' dir. İki Configuration Manager sitesi birbirleriyle iletişim kurduğunda, SHA-256 ile iletişimlerini imzalarlar. Configuration Manager uygulanan birincil şifreleme algoritması 3DES 'dir. Bu, Configuration Manager veritabanında ve istemci HTTP iletişimi için veri depolamak için kullanılır. HTTPS üzerinden istemci iletişimini kullandığınızda, ortak anahtar altyapınızı (PKI), [PKI sertifika gereksinimleri](../network/pki-certificate-requirements.md)' nde belgelenen maksimum karma algoritmalarla ve anahtar uzunluklarına sahip RSA sertifikalarını kullanacak şekilde yapılandırabilirsiniz.  

 Windows tabanlı işletim sistemlerine yönelik çoğu şifreleme işlemi için Configuration Manager, Windows Cryptoapı kitaplığı Rsaenh. dll dosyasından SHA-2, 3DES ve AES ve RSA algoritmalarını kullanır.  

> [!IMPORTANT]  
>  SSL güvenlik açıklarına yanıt olarak önerilen değişiklikler için [About SSL Vulnerabilities](#about-ssl-vulnerabilities)içindeki bilgilere bakın.  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Configuration Manager işlemler için şifreleme denetimleri  
 Configuration Manager bilgiler, Configuration Manager ile PKI sertifikaları kullanıp kullanmayacağınızı, imzalanıp şifrelenmeyeceğini ve şifrelenebilir.  

### <a name="policy-signing-and-encryption"></a>İlke imzalama ve şifreleme  
 İstemci ilke atamaları, kurcalanmış riskli yönetim noktası gönderme ilkelerinin güvenlik riskini önlemeye yardımcı olarak otomatik imzalı site sunucusu imzalama sertifikası tarafından imzalanır. Bu ortam Internet iletişimine açık bir yönetim noktası gerektirdiğinden Internet tabanlı istemci yönetimi kullanıyorsanız bu önemlidir.  

 İlke duyarlı veriler içerdiğinde 3DES ile şifrelenir. Duyarlı veriler içeren ilke yalnızca yetkili istemcilere gönderilir. Duyarlı veriler içermeyen ilke şifrelenmez.  

 İlke istemcilerde depolandığında, veri koruma uygulama programlama arabirimi (DPAPI) ile şifrelenir.  

### <a name="policy-hashing"></a>İlke karması  
 Configuration Manager istemcileri ilke talep edildiğinde, bu ilkeler, hangi ilkelerin uygulanacağını bilmeleri için öncelikle bir ilke ataması alırlar ve ardından yalnızca bu ilke gövdelerini ister. Her ilke ataması ilgili ilke gövdesi için hesaplanmış karmayı içerir. İstemci ilgili ilke gövdelerini alır ve ardından o gövde üzerinde karmayı hesaplar. İndirilen ilke gövdesindeki karma ile ilke atamasındaki karma eşleşmezse istemci, ilke gövdesini iptal eder.  

 İlkenin karma algoritması SHA-1 ve SHA-256'dır.  

### <a name="content-hashing"></a>İçerik karması  

Site sunucusundaki dağıtım yöneticisi hizmeti tüm paketler için içerik dosyalarının karmasını oluşturur. İlke sağlayıcısı, yazılım dağıtım ilkesine karmayı dahil eder. Configuration Manager istemcisi içeriği indirdiğinde istemci, karmayı yerel olarak yeniden oluşturur ve ilkede belirtilen bir ile karşılaştırır. Karmalar eşleşiyorsa içerik değiştirilmemiştir ve istemci tarafından yüklenir. İçeriğin tek bir baytı değiştirildiyse karmalar eşleşmez ve yazılım yüklenmez. Geçerli içerik ilkeyle çapraz denetimden geçirildiği için bu denetim doğru yazılımın yüklenmesini sağlamaya yardımcı olur.  

İçerik için varsayılan karma algoritması SHA-256’dır.

İçerik karmasını tüm cihazlar destekleyemez. Özel durumlar şunları içerir:  

- App-V içeriği yayınlayan Windows istemcileri.  

- İstemciler Windows Phone, ancak bu istemciler güvenilir bir kaynak tarafından imzalanan bir uygulamanın imzasını doğrular.  

- Bu istemciler güvenilen bir kaynak tarafından imzalanmış bir uygulamanın imzasını doğrular ve ayrıca paket tam adı (PFN) doğrulamasını kullanır.  

- Linux ve UNIX sürümlerinde çalışan istemciler SHA-256’yı desteklemez. Daha fazla bilgi için bkz. [Linux ve UNIX bilgisayarlara istemci dağıtımını planlama](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

### <a name="inventory-signing-and-encryption"></a>Envanter imzalama ve şifreleme  
 İstemcilerin yönetim noktalarına gönderdiği envanter, HTTP veya HTTPS üzerinden yönetim noktalarıyla iletişim kurup kurmadıklarına bakılmaksızın her zaman cihazlar tarafından imzalanır. HTTP kullanılıyorsa bir güvenlik en iyi uygulaması olarak bu verileri şifrelemeyi seçebilirsiniz.  

### <a name="state-migration-encryption"></a>Durum geçişi şifrelemesi  
 İşletim sistemi dağıtımı için durum geçiş noktalarına depolanan veriler her zaman 3DES kullanılarak Kullanıcı Durumu Taşıma Aracı (USMT) tarafından şifrelenir.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>İşletim sistemlerini dağıtmak için çok noktaya yayın paketleri için şifreleme  
 Her işletim sistemi dağıtım paketi için paket çok noktaya yayın kullanılarak bilgisayarlara aktarıldığında şifrelemeyi etkinleştirebilirsiniz. Şifreleme, Gelişmiş Şifreleme Standardı (AES) kullanır. Şifrelemeyi etkinleştirirseniz ek bir sertifika yapılandırması gerekmez. Çok noktaya yayın özelliği etkinleştirilmiş dağıtım noktası, paketi şifrelemek için simetrik anahtarları otomatik olarak oluşturur. Her pakette farklı bir şifreleme anahtarı mevcuttur. Anahtar, standart Windows API'ları kullanarak çok noktaya yayın özelliği etkinleştirilmiş dağıtım noktasına depolanır. İstemci çok noktaya yayın oturumuna bağlandığında PKI ile verilen istemci kimlik doğrulaması sertifikası (istemci HTTPS kullandığında) veya otomatik imzalı sertifika (istemci HTTP kullandığında) ile şifrelenmiş bir kanal üzerinden anahtar değişimi gerçekleştirilir. İstemci, anahtarı yalnızca çok noktaya yayın oturumu süresince belleğe depolar.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>İşletim sistemlerini dağıtmak için medya şifreleme  
 İşletim sistemlerine dağıtmak üzere medya kullandığınızda ve medyayı korumak için bir parola belirttiğinizde, ortam değişkenleri Gelişmiş Şifreleme Standardı (AES) kullanılarak şifrelenir. Medya üzerindeki paketler ve uygulama içerikleri dahil diğer veriler şifrelenmez.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Bulut tabanlı dağıtım noktalarında barındırılan içerik için şifreleme  
 System Center 2012 Configuration Manager SP1 'den itibaren, bulut tabanlı dağıtım noktaları kullandığınızda, bu dağıtım noktalarına yüklediğiniz içerik 256 bit anahtar boyutuyla Gelişmiş Şifreleme Standardı (AES) kullanılarak şifrelenir. İçerik her güncelleştirdiğinizde yeniden şifrelenir. İstemciler içeriği indirdiklerinde HTTPS bağlantısıyla şifrelenip korunur.  

### <a name="signing-in-software-updates"></a>Yazılım güncelleştirmelerinde oturum açma  
 Tüm yazılım güncelleştirmeleri, kurcalanmaya karşı koruma sağlamak üzere güvenilen bir yayımcı tarafından imzalanmalıdır. İstemci bilgisayarlarda Windows Update Aracısı (WUA) katalogdaki güncelleştirmeleri tarar, ancak yerel bilgisayardaki Güvenilen Yayımcılar deposunda dijital sertifikayı bulamazsa güncelleştirmeyi yüklemez. Güncelleştirme kataloğunu yayımlamak için WSUS Publishers Self-signed gibi otomatik imzalı bir sertifika kullanıldıysa, sertifikanın geçerliliğinin onaylanabilmesi için yerel bilgisayardaki Güvenilen Kök Sertifika Yetkilileri sertifika deposunda da sertifikanın olması gerekir. WUA ayrıca yerel bilgisayarda **İntranet Microsoft güncelleştirme hizmeti konumu Grup İlkesinden imzalanmış içeriğe izin ver** ayarının etkinleştirilip etkinleştirilmediğini denetler. Updates Publisher ile oluşturulup yayımlanan güncelleştirmeleri taramak üzere WUA için bu ilke ayarı etkinleştirilmelidir.  

 Yazılım güncelleştirmeleri System Center Updates Publisher'da yayımlandığında, bir güncelleştirme sunucusuna yayımlanan yazılım güncelleştirmeleri dijital bir sertifika tarafından imzalanır. Bir PKI sertifikası belirtebilir veya Updates Publisher'ı yazılım güncelleştirmelerinin imzalanması için otomatik imzalı bir sertifika oluşturacak şekilde yapılandırabilirsiniz.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Uyumluluk ayarları için imzalanmış yapılandırma verileri  
 Yapılandırma verilerini içeri aktardığınızda Configuration Manager dosyanın dijital imzasını doğrular. Dosyalar imzalanmamışsa veya dijital yapı doğrulama denetimi başarısız olursa bir uyarı alırsınız ve içeri aktarmaya devam etmek isteyip istemediğiniz sorulur. Yapılandırma verilerini içeri aktarmaya yalnızca yayımcıya ve dosyaların bütünlüğüne açıkça güveniyorsanız devam edin.  

### <a name="encryption-and-hashing-for-client-notification"></a>İstemci bildirimi için şifreleme ve karma oluşturma  
 İstemci bildirimi kullanıyorsanız tüm iletişimlerde TLS'yi ve sunucu ile istemci işletim sistemlerinin anlaşabileceği en yüksek şifrelemeyi kullanır. Örneğin, Windows 7 çalıştıran bir istemci bilgisayar ve Windows Server 2008 R2 çalıştıran bir yönetim noktası 128 bit AES şifrelemesini destekleyebilir, ancak aynı yönetim noktasına Vista çalıştıran bir istemci bilgisayar 3DES şifrelemesine göre anlaşacaktır. Aynı anlaşma, SHA-1 veya SHA-2 kullanan istemci bildirimi sırasında aktarılan paketlerin karmasını oluştururken meydana gelir.  

##  <a name="certificates-used-by-configuration-manager"></a>Configuration Manager tarafından kullanılan sertifikalar  
 Configuration Manager tarafından kullanılabilen ortak anahtar altyapısı (PKI) sertifikalarının bir listesi, tüm özel gereksinimler veya sınırlamalar ve sertifikaların nasıl kullanıldığı hakkında bilgi için bkz. [PKI sertifikası gereksinimleri](../network/pki-certificate-requirements.md). Bu liste desteklenen karma algoritmaları ve anahtar uzunluklarını içerir. Birçok sertifika SHA-256 ve 2048 bit anahtar uzunluğunu destekler.  

> [!NOTE]  
>  Configuration Manager tarafından kullanılan tüm sertifikalar, konu adı veya konu diğer adı içinde yalnızca tek baytlık karakterler içermelidir.  

 PKI sertifikaları aşağıdaki senaryolar için gereklidir:  

- Configuration Manager istemcileri Internet 'te yönettiğinizde.  

- Mobil cihazlarda Configuration Manager istemcilerini yönetirken.  

- Mac bilgisayarları yönettiğinizde.  

- Bulut tabanlı dağıtım noktaları kullandığınızda.  

  Kimlik doğrulaması, imzalama veya şifreleme için sertifika gerektiren diğer Configuration Manager iletişimleri için Configuration Manager, kullanılabilir olmaları durumunda otomatik olarak PKI sertifikaları kullanır. Bunlar yoksa, Configuration Manager otomatik olarak imzalanan sertifikalar oluşturur.  

  Configuration Manager, Exchange Server bağlayıcısını kullanarak mobil cihazları yönettiğinde PKI sertifikaları kullanmaz.  

### <a name="mobile-device-management-and-pki-certificates"></a>Mobil cihaz yönetimi ve PKI sertifikaları  
 Mobil cihaz mobil operatör tarafından kilitlenmediyse, bir istemci sertifikası istemek ve yüklemek için Configuration Manager veya Microsoft Intune kullanabilirsiniz. Bu sertifika, mobil cihazdaki istemci Configuration Manager ile site sistemleri veya Microsoft Intune hizmetleri arasında karşılıklı kimlik doğrulaması sağlar. Mobil cihazınız kilitliyse, sertifikaları dağıtmak için Configuration Manager veya Intune 'u kullanamazsınız.  

 Mobil cihazlar için donanım envanterini etkinleştirirseniz Configuration Manager veya Intune, mobil cihazda yüklü olan sertifikaları da envanterler.   

### <a name="operating-system-deployment-and-pki-certificates"></a>İşletim sistemi dağıtımı ve PKI sertifikaları  
 İşletim sistemlerini dağıtmak için Configuration Manager kullandığınızda ve bir yönetim noktası HTTPS istemci bağlantıları gerektirdiğinde, görev sırası medyasından veya PXE özellikli bir dağıtım noktasından önyükleme gibi bir geçiş aşamasında olsa bile istemci bilgisayarın yönetim noktasıyla iletişim kurmak için bir sertifikası olması gerekir. Bu senaryoyu desteklemek için bir PKI istemci kimlik doğrulama sertifikası oluşturmanız ve özel anahtarla dışarı aktardıktan sonra site sunucusu özelliklerine aktarmanız ve ayrıca yönetim noktasının güvenilen kök CA sertifikasını eklemeniz gerekir.  

 Önyüklenebilir medya oluşturmak için, önyüklenebilir medya oluştururken istemci kimlik doğrulama sertifikasını içe aktarın. Özel anahtarı ve görev sırasında yapılandırılmış diğer duyarlı verileri korumaya yardımcı olmak üzere önyüklenebilir medyada bir parola yapılandırın. Önyüklenebilir medyadan başlatılan her bilgisayar, yönetim noktasına istemci ilkesini isteme gibi istemci işlevleri için gereken sertifikanın aynısını sunar.  

 PXE önyüklemesi kullanıyorsanız, istemci kimlik doğrulama sertifikasını PXE özellikli dağıtım noktasına aktarırsınız ve bu PXE özellikli dağıtım noktasından başlatılan her istemci için aynı sertifika kullanılır. En iyi güvenlik uygulaması olarak, bilgisayarlarını bir PXE hizmetine bağlayan kullanıcıların özel anahtarı ve görev sırasındaki diğer duyarlı verileri korumaya yardımcı olmak üzere bir parola belirtmesini isteyin.  

 Bu istemci kimlik doğrulama sertifikalarından biri riske girerse, **Yönetim** çalışma alanındaki **Güvenlik** düğümü, **Sertifikalar** düğümünde bulunan sertifikaları engelleyin. Bu sertifikaları yönetmek için **İşletim sistemi dağıtım sertifikasını yönet** hakkına sahip olmanız gerekir.  

 İşletim sistemi dağıtıldıktan ve Configuration Manager yüklendikten sonra istemci, HTTPS istemci iletişimi için kendi PKI istemci kimlik doğrulama sertifikasını gerektirir.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>ISV proxy çözümleri ve PKI sertifikaları  
 Bağımsız yazılım satıcıları (ISV 'Ler), Configuration Manager genişleten uygulamalar oluşturabilir. Örneğin, bir ISV Macintosh veya UNIX bilgisayarlar gibi Windows dışı istemci platformlarını destekleyen uzantılar oluşturabilir. Ancak, site sistemleri HTTPS istemci bağlantıları gerektiriyorsa bu istemciler siteyle iletişim için PKI sertifikalarını da kullanmalıdır. Configuration Manager, ISV proxy istemcileri ile yönetim noktası arasında iletişimi sağlayan ISV proxy 'sine bir sertifika atama özelliğini içerir. ISV proxy sertifikaları gerektiren uzantılar kullanıyorsanız ilgili ürünün belgelerine başvurun. ISV proxy sertifikaları oluşturma hakkında daha fazla bilgi için bkz. Configuration Manager Software Developer Kit (SDK).  

 ISV sertifikası riske girerse, **Yönetim** çalışma alanındaki **Güvenlik** düğümü, **Sertifikalar** düğümünde bulunan sertifikayı engelleyin.  

### <a name="asset-intelligence-and-certificates"></a>Varlık yönetim bilgileri ve sertifikaları  
 Configuration Manager, Varlık Yönetim Bilgileri eşitleme noktasının Microsoft 'a bağlanmak için kullandığı bir X. 509.440 sertifikası ile yüklenir. Configuration Manager, Microsoft sertifika hizmetinden bir istemci kimlik doğrulama sertifikası istemek için bu sertifikayı kullanır. İstemci kimlik doğrulama sertifikası, Varlık Yönetim Bilgileri eşitleme noktası site sistem sunucusuna yüklenir ve sunucunun kimliğini Microsoft'ta doğrulamak için kullanılır. Configuration Manager, Varlık Yönetim Bilgileri kataloğunu indirmek ve yazılım başlıklarını karşıya yüklemek için istemci kimlik doğrulama sertifikasını kullanır.  

 Bu sertifika 1024 bit anahtar uzunluğuna sahiptir.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Bulut tabanlı dağıtım noktaları ve sertifikalar  
 System Center 2012 Configuration Manager SP1 'den itibaren bulut tabanlı dağıtım noktaları, Microsoft Azure yüklediğiniz bir yönetim sertifikası (otomatik imzalı veya PKI) gerektirir. Bu yönetim sertifikası, sunucu kimlik doğrulama özelliğini ve 2048 bit sertifika anahtarı uzunluğunu gerektirir. Bunun yanında, her bulut tabanlı dağıtım noktası için otomatik imzalı olamayacak, ancak ayrıca sunucu kimlik doğrulama özelliğine ve 2048 bit en küçük sertifika anahtar uzunluğuna sahip bir hizmet sertifikası yapılandırmanız gerekir.  

> [!NOTE]  
>  Otomatik imzalı yönetim sertifikası yalnızca sınama amaçlıdır ve üretim ağlarında kullanıma yönelik değildir.  

 İstemciler bulut tabanlı dağıtım noktalarını kullanmak için bir istemci PKI sertifikası gerektirmez; otomatik imzalı bir sertifika veya bir istemci PKI sertifikası kullanarak yönetim kimliğini doğrularlar. Yönetim noktası daha sonra istemci için istemcinin bulut tabanlı dağıtım noktasına sunduğu Configuration Manager erişim belirteci yayınlar. Belirteç 8 saat boyunca geçerlidir.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Microsoft Intune Bağlayıcısı ve sertifikaları  
 Microsoft Intune mobil cihazları kaydettiğinde, bu mobil cihazları bir Microsoft Intune Bağlayıcısı oluşturarak Configuration Manager yönetebilirsiniz. Bağlayıcı, Microsoft Intune Configuration Manager kimliğini doğrulamak ve aralarındaki tüm bilgileri SSL kullanarak aktarmak için istemci kimlik doğrulama özelliğine sahip bir PKI sertifikası kullanır. Sertifika anahtar boyutu 2048 bittir ve SHA-1 karma algoritmasını kullanır.  

 Bağlayıcıyı yüklediğinizde bir imzalama sertifikası oluşturulur ve dışarıdan yükleme anahtarları için site sunucusuna depolanır ve Basit Sertifika Kayıt Protokolü (SCEP) sınamasını şifrelemek üzere bir şifreleme sertifikası oluşturulup sertifika kayıt noktasına depolanır. Bu sertifikalar da 2048 bit anahtar boyutuna sahiptir ve SHA-1 karma algoritmasını kullanır.  

 Intune mobil cihazları kaydettiğinde mobil cihaza bir PKI sertifikası yükler. Bu sertifika, istemci kimlik doğrulama özelliğine sahiptir, 2048 bit anahtar boyutu ve SHA-1 karma algoritmasını kullanır.  

 Bu PKI sertifikaları Microsoft Intune tarafından otomatik olarak istenir, oluşturulur ve yüklenir.  

### <a name="crl-checking-for-pki-certificates"></a>PKI sertifikaları için CRL denetleme  
 Bir PKI sertifika iptal listesi (CRL) yönetim ve işleme yüklerini artırmasına karşın daha güvenlidir. Ancak, CRL denetlemesinin etkinleştirilmesine rağmen CRL'ye erişilemiyorsa PKI bağlantısı başarısız olur. Daha fazla bilgi için bkz. [Configuration Manager Için güvenlik ve gizlilik](security-and-privacy.md).  

 Sertifika iptal listesi (CRL) denetimi IIS 'de varsayılan olarak etkindir, bu nedenle PKI dağıtımınızla birlikte bir CRL kullanıyorsanız, IIS çalıştıran çoğu Configuration Manager site sisteminde yapılandırma için başka bir şey yoktur. Buradaki özel durum, yazılım güncelleştirme dosyalarındaki imzaları doğrulamak için CRL denetlemeyi elle etkinleştirmeyi gerektiren yazılım güncelleştirmeleridir.  

 CRL denetlemesi, HTTPS istemci bağlantıları kullanan istemci bilgisayarlar için varsayılan olarak etkindir. Configuration Manager SP1 veya sonraki sürümlerde Mac bilgisayarlarda istemciler için CRL denetimini devre dışı bırakabilirsiniz.  

 CRL denetlemesi Configuration Manager ' deki aşağıdaki bağlantılar için desteklenmez:  

-   Sunucudan sunucuya bağlantılar.  

-   Configuration Manager tarafından kaydedilen mobil cihazlar.  

-   Microsoft Intune tarafından kaydedilen mobil cihazlar.  

##  <a name="cryptographic-controls-for-server-communication"></a>Sunucu iletişimi için şifreleme denetimleri  
 Configuration Manager, sunucu iletişimi için aşağıdaki şifreleme denetimlerini kullanır.  

### <a name="server-communication-within-a-site"></a>Bir site içindeki sunucu iletişimi  
 Her site sistemi sunucusu, aynı Configuration Manager sitesindeki diğer site sistemlerine veri aktarmak için bir sertifika kullanır. Bazı site sistem rolleri ayrıca kimlik doğrulaması için sertifikalar kullanır. Örneğin, bir sunucuya kayıt proxy noktası, diğer bir sunucuya ise kayıt noktası yüklerseniz bu kimlik sertifikasını kullanarak birbirlerinin kimliğini doğrulayabilirler. Configuration Manager Bu iletişim için bir sertifika kullandığında, sunucu kimlik doğrulama özelliğine sahip bir PKI sertifikası varsa, Configuration Manager otomatik olarak bunu kullanır; Aksi takdirde, Configuration Manager kendinden imzalı bir sertifika oluşturur. Bu otomatik olarak imzalanan sertifika, sunucu kimlik doğrulama özelliğine sahiptir, SHA-256 kullanır ve 2048 bit anahtar uzunluğuna sahiptir. Configuration Manager, sertifikayı site sistemine güvenmesi gerekebilecek diğer site sistem sunucularındaki güvenilir kişiler deposuna kopyalar. Site sistemleri bu durumda bu sertifikaları ve PeerTrust'ı kullanarak birbirine güvenebilir.  

 Her site sistem sunucusu için bu sertifikaya ek olarak Configuration Manager, çoğu site sistem rolü için otomatik olarak imzalanan bir sertifika oluşturur. Aynı sitede site sistem rolünün birden çok örneği olduğunda aynı sertifikayı paylaşırlar. Örneğin, aynı sitede birden çok yönetim noktanız veya birden çok kayıt noktanız olabilir. Bu otomatik imzalı sertifika da SHA-256 kullanır ve 2048 bit anahtar uzunluğuna sahiptir. Ayrıca site sistem sunucularında buna güvenmesi gerekebilen Güvenilir Kişiler Deposuna kopyalanır. Aşağıdaki site sistem rolleri şu sertifikayı oluşturur:  

- Uygulama Kataloğu web hizmet noktası  

- Uygulama Kataloğu web sitesi noktası  

- Varlık Yönetim Bilgileri eşitleme noktası  

- Sertifika kayıt noktası  

- Uç Nokta Koruma noktası  

- Kayıt noktası  

- Geri dönüş durumu noktası  

- Yönetim noktası  

- Çok noktaya yayını destekleyen dağıtım noktası  

- Raporlama hizmetleri noktası  

- Yazılım güncelleştirme noktası  

- Durum Geçiş noktası  

- Microsoft Intune bağlayıcısı  

Bu sertifikalar Configuration Manager tarafından otomatik olarak yönetilir ve gerektiğinde otomatik olarak oluşturulur.  

Configuration Manager ayrıca, dağıtım noktasından yönetim noktasına durum iletileri göndermek için bir istemci kimlik doğrulama sertifikası kullanır. Yönetim noktası yalnızca HTTPS istemci bağlantıları için yapılandırıldığında bir PKI sertifikası kullanmanız gerekir. Yönetim noktası HTTP bağlantılarını kabul ediyorsa bir PKI sertifikası kullanabilir veya istemci kimlik doğrulama özelliğine sahip, SHA-256 kullanan ve anahtar uzunluğu 2048 bit olan otomatik imzalı bir sertifika kullanma seçeneğini belirleyebilirsiniz.  

### <a name="server-communication-between-sites"></a>Siteler arasındaki sunucu iletişimi  
 Configuration Manager, veritabanı çoğaltmasını ve dosya tabanlı çoğaltmayı kullanarak verileri siteler arasında aktarır. Daha fazla bilgi için bkz. [uç noktalar arasındaki iletişimler](../hierarchy/communications-between-endpoints.md).  

 Configuration Manager, siteler arasındaki veritabanı çoğaltmasını otomatik olarak yapılandırır ve varsa sunucu kimlik doğrulama özelliğine sahip PKI sertifikalarını kullanır; Aksi takdirde, Configuration Manager sunucu kimlik doğrulaması için otomatik olarak imzalanan sertifikalar oluşturur. Her iki durumda da siteler arasındaki kimlik doğrulaması, PeerTrust kullanan Güvenilir Kişiler Deposundaki sertifikalar kullanılarak gerçekleştirilir. Bu sertifika depolama alanı, yalnızca Configuration Manager hiyerarşisi tarafından kullanılan SQL Server bilgisayarların siteden siteye çoğaltmaya katılmasını sağlamak için kullanılır. Birincil siteler ve merkezi yönetim sitesi yapılandırma değişikliklerini hiyerarşideki tüm sitelere kopyalarken, ikincil siteler yapılandırma değişikliklerine yalnızca üst sitelerine kopyalayabilir.  

 Site sunucuları otomatik olarak gerçekleşen bir güvenli anahtar değişimini kullanarak siteden siteye iletişim kurar. Gönderen site sunucusu bir karma oluşturur ve özel anahtarıyla imzalar. Alan site sunucusu ortak anahtar kullanarak imzayı denetler ve karmayı yerel olarak oluşturulmuş bir değerle karşılaştırır. Eşleşiyorlarsa alıcı site çoğaltılan verileri kabul eder. Değerler eşleşmiyorsa, Configuration Manager çoğaltma verilerini reddeder.  

 Configuration Manager veritabanı çoğaltması, aşağıdaki mekanizmalardan yararlanarak siteler arasında veri aktarmak için SQL Server Hizmet Aracısı kullanır:  

- SQL Server’dan SQL Server’a bağlantı: Bu seçenek Gelişmiş Şifreleme Standardı (AES) kullanarak verileri imzalamak ve şifrelemek üzere sunucu kimlik doğrulaması için Windows kimlik bilgilerini ve 1024 bitle otomatik imzalı sertifikaları kullanır. Sunucu kimlik doğrulama özelliğine sahip PKI sertifikaları mevcutsa bunlar kullanılır. Sertifika, Bilgisayar sertifika deposunun Kişisel deposunda bulunmalıdır.  

- SQL Server Aracısı: Bu seçenek, Gelişmiş Şifreleme Standardı (AES) kullanarak kimlik doğrulaması yapmak ve verileri imzalamak ve şifrelemek üzere kimlik doğrulaması için 2048 bitle otomatik imzalı sertifikaları kullanır. Sertifika SQL Server ana veritabanında olmalıdır.  

  Dosya tabanlı çoğaltma özelliği, şifrelenmemiş ancak herhangi bir duyarlı veri içermeyen bu verileri imzalamak için Sunucu İleti Bloğu (SMB) protokolü ve SHA-256 kullanır. Bu verileri şifrelemek isterseniz IPSec kullanabilirsiniz ve bunu Configuration Manager bağımsız olarak uygulamanız gerekir.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Site sistemleriyle HTTPS iletişimi kullanan istemciler için şifreleme denetimleri  
 Site sistem rolleri istemci bağlantılarını kabul ettiğinde, bunları HTTPS ve HTTP bağlantılarını ya da yalnızca HTTPS bağlantılarını kabul edecek şekilde yapılandırabilirsiniz. Internet bağlantılarını kabul eden site sistem rolleri yalnızca HTTPS üzerinden istemci bağlantılarını kabul eder.  

 HTTPS üzerinden kurulan istemci bağlantıları, istemciden sunucuya iletişimi korumak üzere ortak anahtar altyapısı (PKI) ile bütünleşerek daha yüksek düzeyde güvenlik sunar. Ancak, HTTPS istemci bağlantılarının PKI planlama, dağıtım ve işlemleri iyice anlaşılmadan yapılandırılması sizi güvenlik açıklarına maruz bırakabilir. Örneğin, kök sertifika yetkilinizin güvenliğini sağlamazsanız saldırganlar tüm PKI altyapınızın güvenini riske sokabilir. Denetimli ve güvenli işlemler kullanılarak PKI sertifikalarının dağıtılamaması ve yönetilememesi, kritik yazılım güncelleştirmelerini veya paketlerini alamayan, yönetilmeyen istemcilerle sonuçlanabilir.  

> [!IMPORTANT]  
>  İstemci iletişimi için kullanılan PKI sertifikaları yalnızca istemci ile bazı site sistemleri arasındaki iletişimi korur. Bunlar site sunucusu ile site sistemleri veya site sunucuları arasındaki iletişim kanalını korumaz.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>İstemciler HTTPS iletişimi kullanırken şifrelenmemiş iletişim  
 İstemciler HTTPS kullanarak site sistemleriyle iletişim kurduğunda bu iletişimler genellikle SSL üzerinden şifrelenir. Ancak, aşağıdaki durumlarda istemciler, site sistemleriyle şifreleme olmadan iletişim kurarlar:  

- İstemci intranet üzerinde bir HTTPS bağlantısı oluşturamaz ve site sistemleri bu yapılandırmaya izin verdiğinde HTTP kullanmaya geri döner  

- Aşağıdaki site sistem rolleriyle iletişim:  

  -   İstemci geri dönüş durum noktasına durum iletileri gönderir  

  -   İstemci PXE özellikli bir dağıtım noktasına PXE istekleri gönderir  

  -   İstemci bir yönetim noktasına bildirim verileri gönderir  

  Raporlama hizmetleri noktaları HTTP veya HTTPS'yi istemci iletişim modundan bağımsız olarak kullanmak üzere yapılandırılmıştır.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>İstemciler için şifreleme denetimleri sohbet ile site sistemleriyle HTTP iletişimi kullanma  
 İstemciler site sistem rolleriyle HTTP iletişimi kullandığında, istemci kimlik doğrulaması için PKI sertifikaları veya Configuration Manager üreten otomatik imzalı sertifikalar kullanabilirler. Configuration Manager otomatik olarak imzalanan sertifikalar oluşturduğunda, imzalama ve şifreleme için özel bir nesne tanımlayıcısına sahiptir ve bu sertifikalar istemciyi benzersiz şekilde tanımlamak için kullanılır. Windows Server 2003 hariç desteklenen tüm işletim sistemlerinde bu otomatik imzalı sertifikalar SHA-256 ve 2048 bit anahtar uzunluğu kullanır. Windows Server 2003'te ise 1024 bit anahtar uzunluğuyla SHA1 kullanılır.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>İşletim sistemi dağıtımı ve otomatik olarak imzalanan sertifikalar  
 Otomatik olarak imzalanan sertifikalarla işletim sistemlerini dağıtmak için Configuration Manager kullandığınızda, bilgisayar, görev sırası medyasından veya PXE özellikli bir dağıtım noktasından önyükleme gibi bir geçiş aşamasında olsa bile, istemci bilgisayarın yönetim noktasıyla iletişim kurmak için bir sertifikası olması gerekir. HTTP istemci bağlantılarında bu senaryoyu desteklemek için Configuration Manager, imzalama ve şifreleme için özel bir nesne tanımlayıcısına sahip otomatik olarak imzalanan sertifikalar oluşturur ve bu sertifikalar istemciyi benzersiz şekilde tanımlamak için kullanılır. Windows Server 2003 hariç desteklenen tüm işletim sistemlerinde bu otomatik imzalı sertifikalar SHA-256 ve 2048 bit anahtar uzunluğu kullanır. Windows Server 2003'te ise 1024 bit anahtar uzunluğuyla SHA1 kullanılır. Otomatik olarak imzalanan bu sertifikaların güvenliği aşılırsa saldırganların güvenilen istemcilerin kimliğine bürünmek üzere onları kullanmasına engel olmak için sertifikaları **Yönetim** çalışma alanındaki **Sertifikalar** düğümünde ve **Güvenlik** düğümünde engelleyin.  

### <a name="client-and-server-authentication"></a>İstemci ve sunucu kimlik doğrulaması  
 İstemciler HTTP üzerinden bağlandıklarında, Active Directory Domain Services veya Configuration Manager güvenilen kök anahtarını kullanarak yönetim noktalarının kimliğini doğrular. İstemciler, durum geçiş noktaları veya yazılım güncelleştirme noktaları gibi diğer site sistemi rollerinin kimliğini doğrulamaz.  

 Bir yönetim noktası otomatik olarak imzalanan sertifikayı kullanarak istemcinin kimliğini ilk kez doğruladığında, her bilgisayar otomatik olarak imzalanan sertifika oluşturabileceği için bu düzenek en düşük güvenliği sağlar. Bu senaryoda, istemci kimliği işlemi onay yoluyla yükseltilmelidir. Yönetici Kullanıcı tarafından yalnızca güvenilen bilgisayarların Configuration Manager veya el ile otomatik olarak onaylanması gerekir. Daha fazla bilgi için [uç noktalar arasındaki iletişimlerdeki](../hierarchy/communications-between-endpoints.md)onay bölümüne bakın.  

## <a name="about-ssl-vulnerabilities"></a>SSL hakkında güvenlik açıkları
Configuration Manager istemcileriniz ve sunucularınızın güvenliğini artırmak için aşağıdakileri yapın:

- TLS 1.2’yi etkinleştirme

  Configuration Manager için TLS 1,2 ' i etkinleştirmek için bkz. [Configuration Manager IÇIN tls 1,2 nasıl etkinleştirilir](enable-tls-1-2.md).
- SSL 3,0, TLS 1,0 ve TLS 1,1 'ı devre dışı bırakın 
- TLS ile ilgili şifre paketlerini yeniden sıralama 

Daha fazla bilgi için bkz. [Schannel. dll ' de belirli şifreleme algoritmalarının ve protokollerin kullanımını kısıtlama](https://support.microsoft.com/en-us/kb/245030/) ve [Schannel şifre paketlerinin önceliklerini belirleme](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx). Bu yordamlar Configuration Manager işlevselliğini etkilemez.

