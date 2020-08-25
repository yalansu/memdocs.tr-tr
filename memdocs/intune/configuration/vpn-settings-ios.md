---
title: Microsoft Intune-Azure 'da VPN ayarlarını iOS/ıpados cihazlarına yapılandırma | Microsoft Docs
description: Sanal özel ağ (VPN) yapılandırma ayarlarını kullanarak iOS/ıpados cihazlarına bir VPN yapılandırma profili ekleyin veya oluşturun. Bağlantı ayrıntılarını, kimlik doğrulama yöntemlerini, bölünmüş tüneli, özel VPN ayarlarını, bir yapılandırma betiği, IP veya FQDN adresi ve Microsoft Intune TCP bağlantı noktasını içerecek şekilde, anahtar ve değer çiftleri, uygulama başına VPN ayarlarını ve SSID veya DNS arama etki alanları ile isteğe bağlı VPN ayarlarını yapılandırın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 29ce01f9544db19757f58695eae624b2ac25995b
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819924"
---
# <a name="add-vpn-settings-on-ios-and-ipados-devices-in-microsoft-intune"></a>Microsoft Intune 'de iOS ve ıpados cihazlarına VPN ayarları ekleme

Microsoft Intune iOS/ıpados cihazlarınıza dağıtılabilecek birçok VPN ayarı içerir. Bu ayarlar, kuruluşunuzun ağına yönelik VPN bağlantıları oluşturmak ve yapılandırmak için kullanılır. Bu makalede bu ayarlar açıklanır. Bazı ayarlar yalnızca Citrix ve Zscaler gibi bazı VPN istemcileri için kullanılabilir.

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](vpn-settings-configure.md).

> [!NOTE]
> Bu ayarlar, Kullanıcı kaydı dışında tüm kayıt türlerinde kullanılabilir. Kullanıcı kaydı, [uygulama BAŞıNA VPN](https://docs.microsoft.com/mem/intune/configuration/vpn-setting-configure-per-app)ile sınırlıdır. Kayıt türleri hakkında daha fazla bilgi için bkz. [iOS/ıpados kaydı](../enrollment/ios-enroll.md).

## <a name="connection-type"></a>Bağlantı türü

Aşağıdaki satıcı listesinden VPN bağlantı türünü seçin:

- **Check Point Capsule VPN**
- **Cisco Eski AnyConnect**: [Cisco Eski AnyConnect](https://itunes.apple.com/app/cisco-legacy-anyconnect/id392790924) uygulama sürümü 4.0.5x ve öncesi için geçerlidir.
- **Cisco AnyConnect**: [Cisco AnyConnect](https://itunes.apple.com/app/cisco-anyconnect/id1135064690) uygulama sürümü 4.0.7x ve sonrası için geçerlidir.
- **SonicWall Mobile Connect**
- **F5 Access Eski**: F5 Access uygulama sürümü 2.1 ve öncesi için geçerlidir.
- **F5 Access**: F5 Access uygulama sürümü 3.0 ve sonrası için geçerlidir.
- **Palo Alto Networks GlobalProtect (Eski)**: Palo Alto Networks GlobalProtect uygulama sürümü 4.1 ve öncesi için geçerlidir.
- **Palo Alto Networks GlobalProtect**: Palo Alto Networks GlobalProtect uygulama sürümü 5.0 ve sonrası için geçerlidir.
- **Pulse Secure**
- **Cisco (IPSec)**
- **Citrix VPN**
- **Citrix SSO**
- **Zscaler**: koşullu erişimi kullanmak veya kullanıcıların Zscaler oturum açma ekranını atlamasına izin vermek Için, Zscaler özel erişimini (ZPA) Azure AD hesabınızla tümleştirmeniz gerekir. Ayrıntılı adımlar için bkz. [Zscaler belgeleri](https://help.zscaler.com/zpa/configuration-guide-microsoft-azure-ad).
- **NetMotion Mobility**
- **Ikev2**: [Ikev2 ayarları](#ikev2-settings) (Bu makalede) özelliklerini açıklar.
- **Özel VPN**

> [!NOTE]
> Cisco, Citrix, F5 ve Palo Alto; eski istemcilerinin iOS 12 sürümünde çalışmadığını duyurdu. En kısa zamanda yeni uygulamalara geçmeniz gerekir. Daha fazla bilgi için bkz. [Microsoft Intune Destek Ekibi Blogu](https://go.microsoft.com/fwlink/?linkid=2013806&clcid=0x409).

## <a name="base-vpn-settings"></a>Temel VPN ayarları

Aşağıdaki listede gösterilen ayarlar, seçtiğiniz VPN bağlantı türüne göre belirlenir.  

- **Bağlantı adı**: Cihazlarındaki kullanılabilir VPN bağlantıları listesine göz atan son kullanıcılar bu adı görür.
- **Özel etki alanı adı** (yalnızca Zscaler): Zscaler uygulamasının oturum açma alanını kullanıcılarınızın ait olduğu etki alanı Ile önceden doldurun. Örneğin kullanıcı adı `Joe@contoso.net` ise uygulama açıldığında alanda `contoso.net` etki alanı statik olarak görünür. Bir etki alanı adı girmezseniz Azure Active Directory’deki (AD) UPN’nin etki alanı kısmı kullanılır.
- **IP adresi veya FQDN**: Cihazların bağlanırken kullandığı VPN sunucusunun IP adresi veya tam etki alanı adı (FQDN). Örneğin `192.168.1.1` veya `vpn.contoso.com` girin.
- **Kuruluşun bulut adı** (yalnızca Zscaler): Kuruluşunuzun sağlandığı bulutun adını girin. Bu ad, Zscaler’da oturum açarken kullandığınız URL’de mevcuttur.  
- **Kimlik doğrulama yöntemi**: Cihazların VPN sunucusunda kimliklerini nasıl doğrulayacaklarını seçin. 
  - **Sertifikalar**: **Kimlik doğrulama sertifikası** altında, bağlantının kimliğini doğrulamak için mevcut bir SCEP veya PKCS sertifika profilini seçin. [Sertifika yapılandırma](../protect/certificates-configure.md), sertifika profilleri hakkında rehberlik sağlar.
  - **Kullanıcı adı ve parola**: Son kullanıcıların VPN sunucusunda oturum açmak için kullanıcı adı ve parola girmesi gerekir.  

    > [!NOTE]
    > Cisco IPsec VPN için kimlik doğrulama yöntemi olarak kullanıcı adı ve parola kullanılacaksa bunlar, özel bir Apple Configurator profili ile SharedSecret’ı teslim etmelidir.

  - **Türetilmiş kimlik bilgileri**: kullanıcının akıllı kartından türetilmiş bir sertifika kullanın. Türetilmiş bir kimlik bilgisi veren yapılandırılmamışsa, Intune sizden bir tane eklemeniz istenir. Daha fazla bilgi için bkz. [Microsoft Intune türetilmiş kimlik bilgilerini kullanma](../protect/derived-credentials.md).

- **Dışlanan URL’ler** (yalnızca Zscaler): Zscaler VPN’e bağlıyken, listelenen URL’lere Zscaler bulutu dışında da erişilebilir. 

- **Bölünmüş tünel**: Trafiğe bağlı olarak hangi bağlantının kullanılacağına cihazların karar vermesini sağlamak için bu seçeneği **Etkinleştirin** veya **Devre Dışı Bırakın**. Örneğin, oteldeki bir kullanıcı çalışma dosyalarına erişmek için VPN bağlantısını, web’e göz atmak için ise otelin standart ağını kullanır.

- **VPN tanımlayıcısı** (özel VPN, Zscaler ve Citrix): kullanmakta olduğunuz VPN uygulaması için bir tanımlayıcı ve VPN sağlayıcınız tarafından sağlanır.
- Kuruluşunuzun özel VPN öznitelikleri (özel VPN, Zscaler ve Citrix) **için anahtar/değer çiftleri girin** : VPN bağlantınızı özelleştiren **anahtar** ve **değer** ekleme veya içeri aktarma. Bu değerlerin genelde VPN sağlayıcınız tarafından verildiğini unutmayın.

- **Ağ erişim denetimini etkinleştir (NAC)** (Cisco AnyConnect, Citrix SSO, F5 Access): **kabul ediyorum**' u SEÇTIĞINIZDE, cihaz kimliği VPN profiline dahildir. Bu KIMLIK, ağ erişimine izin vermek veya erişimi engellemek için VPN kimlik doğrulaması için kullanılabilir.

  **Ise Ile Cisco AnyConnect kullanırken**şunları yaptığınızdan emin olun:

  - Henüz yapmadıysanız, [Cisco kimlik hizmetleri altyapısı yönetici KıLAVUZUNDA](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) **MDM sunucusu olarak Microsoft Intune yapılandırma** bölümünde açıklandığı gibi NAC Için Ise 'yi Intune ile tümleştirin.
  - VPN profilinde NAC 'yi etkinleştirin.

  **CITRIX SSO 'Yu ağ geçidiyle kullanırken**şunları yaptığınızdan emin olun:

  - Citrix Gateway 12.0.59 veya üstünü kullandığınızı onaylayın.
  - Kullanıcılarınızın cihazlarında Citrix SSO 1.1.6 veya üzeri yüklü olduğunu doğrulayın.
  - NAC için Citrix Gateway 'i Intune ile tümleştirin. Bkz. [Microsoft Intune/Enterprise Mobility Suite 'ı NetScaler (LDAP + OTP senaryosu)](https://www.citrix.com/content/dam/citrix/en_us/documents/guide/integrating-microsoft-intune-enterprise-mobility-suite-with-netscaler.pdf) Citrix dağıtım kılavuzu ile tümleştirme.
  - VPN profilinde NAC 'yi etkinleştirin.

  **F5 erişimini kullanırken**şunları yaptığınızdan emin olun:

  - F5'e büyük IP 13.1.1.5 veya üstünü kullandığınızı onaylayın. 
  - NAC için büyük IP 'yi Intune ile tümleştirin. Bkz. [genel bakış: uç nokta yönetim sistemleri ile cihaz gönderme denetimleri IÇIN APM yapılandırma](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) F5 Kılavuzu.
  - VPN profilinde NAC 'yi etkinleştirin.

  Cihaz KIMLIĞINI destekleyen VPN ortakları için, Citrix SSO gibi VPN istemcisi KIMLIĞI alabilir. Daha sonra, cihazın kaydedildiğini ve VPN profilinin uyumlu veya uyumlu olmadığını doğrulamak için Intune 'U sorgulayabilir.

  - Bu ayarı kaldırmak için profili yeniden oluşturun ve **Kabul ediyorum**’u seçmeyin. Daha sonra profili yeniden atayın.

### <a name="ikev2-settings"></a>Ikev2 ayarları

Bu ayarlar, Ikev2 **bağlantı türünü**seçtiğinizde geçerlidir  >  **IKEv2**.

- **Her zaman-on VPN**: **Enable** VPN ISTEMCISINI otomatik olarak bağlanıp VPN 'ye yeniden bağlanacak şekilde ayarlar. Her Zaman Açık VPN bağlantıları; kullanıcı cihazı kilitlediğinde, cihaz yeniden başlatıldığında veya kablosuz ağ değiştiğinde bağlı durumda kalır veya hemen bağlanır. **Devre dışı** (varsayılan) olarak ayarlandığında, tüm VPN istemcileri için her zaman VPN devre dışı bırakılır. Etkinleştirildiğinde, şunları da yapılandırın:

  - **Ağ arabirimi**: tüm Ikev2 ayarları yalnızca seçtiğiniz ağ arabirimine uygulanır. Seçenekleriniz şunlardır:
    - **Wi-Fi ve hücresel** (varsayılan): Ikev2 ayarları, cihazdaki Wi-Fi ve hücresel arabirimler için geçerlidir.
    - **Hücresel**: Ikev2 ayarları yalnızca cihazdaki hücresel arabirim için geçerlidir. Wi-Fi arabirimi devre dışı bırakılmış veya kaldırılmış cihazlara dağıtım yapıyorsanız bu seçeneği belirleyin.
    - **Wi-Fi**: Ikev2 ayarları yalnızca cihazdaki Wi-Fi arabirimine uygulanır.
  - **VPN yapılandırmasını devre dışı bırakmak Için Kullanıcı**: **Etkinleştir** ayarı, kullanıcıların her zaman VPN 'yi kapatmasına izin verir. **Devre dışı bırak** (varsayılan), kullanıcıların bunu kapatmasını engeller. Bu ayar için varsayılan değer en güvenli seçenektir.
  - **Sesli mesaj**: her zaman VPN etkinleştirildiğinde sesli posta trafiğiyle ne olacağını seçin. Seçenekleriniz şunlardır:
    - **Ağ TRAFIĞINI VPN üzerinden zorla** (varsayılan): Bu ayar en güvenli seçenektir.
    - **Ağ trafiğinin VPN dışına geçmesine izin ver**
    - **Ağ trafiğini bırak**
  - **AirPrint**: her zaman VPN etkinleştirildiğinde AirPrint trafiğiyle ne olacağını seçin. Seçenekleriniz şunlardır:
    - **Ağ TRAFIĞINI VPN üzerinden zorla** (varsayılan): Bu ayar en güvenli seçenektir.
    - **Ağ trafiğinin VPN dışına geçmesine izin ver**
    - **Ağ trafiğini bırak**
  - **Hücresel hizmetler**: iOS 13.0 + ' da, her zaman VPN etkinleştirildiğinde hücresel trafiğe ne olacağını seçin. Seçenekleriniz şunlardır:
    - **Ağ TRAFIĞINI VPN üzerinden zorla** (varsayılan): Bu ayar en güvenli seçenektir.
    - **Ağ trafiğinin VPN dışına geçmesine izin ver**
    - **Ağ trafiğini bırak**
  - **Yerel olmayan açıklamalı ağ uygulamalarından gelen TRAFIĞIN VPN dışında geçmesine Izin ver**: bir captive ağı, genellikle restoranlar ve oteller Içinde bulunan Wi-Fi etkin noktalarına başvurur. Seçenekleriniz şunlardır:
    - **Hayır**: VPN tüneli üzerinden tüm captive ağ (CN) uygulama trafiğini zorlar.
    - **Evet, tüm uygulamalar**: tüm CN uygulama trafiğinin VPN 'i atlamasına izin verir.
    - **Evet, belirli uygulamalar**: trafiği VPN 'yi ATLAYABILECEĞI CN uygulamalarının bir listesini **ekleyin** . CN uygulamasının paket tanımlayıcılarını girin. Örneğin, `com.contoso.app.id.package` girin.

  - **Captive Web sayfası uygulamasından dış VPN 'den geçiş yapmak Için trafik**: captive Web sayfası, captive oturum açma 'yı işleyen yerleşik bir web tarayıcısıdır. **Etkinleştir** ayarı, tarayıcı uygulama trafiğinin VPN 'i atlamasına izin verir. **Devre dışı bırak** (varsayılan) Web sayfası trafiğini her zaman açık VPN 'yi kullanacak şekilde zorlar. Varsayılan değer en güvenli seçenektir.
  - **Ağ adresi çevirisi (NAT) canlı tutma aralığı (saniye)**: VPN 'ye bağlı kalmak için, cihaz ağ paketlerini etkin kalacak şekilde gönderir. Bu paketlerin ne sıklıkta gönderileceğini, 20-1440 adresinden saniye cinsinden bir değer girin. Örneğin, `60` ağ paketlerini her 60 saniyede BIR VPN 'ye göndermek için bir değer girin. Varsayılan olarak, bu değer saniye olarak ayarlanır `110` .
  - **Cihaz uykuda olduğunda NAT KeepAlive 'ı donanıma devretmek**: bir cihaz uykuda olduğunda, cihazın VPN 'ye bağlı KALMASı için NAT 'ın sürekli canlı tutma paketleri göndermesini **sağlar** . **Devre dışı bırak ayarı** bu özelliği kapatır.

- **Uzak tanımlayıcı**: Ikev2 sunucusunun ağ IP ADRESINI, FQDN 'Sini, userfqdn 'SINI veya ASN1DN girin. Örneğin `10.0.0.3` veya `vpn.contoso.com` girin. Genellikle [**bağlantı adı**](#base-vpn-settings) ile aynı değeri girersiniz (Bu makalede). Ancak, Ikev2 Sunucu ayarlarınıza göre değişir.

- **Istemci kimlik doğrulaması türü**: VPN istemcisinin VPN 'de kimlik doğrulamasını seçin. Seçenekleriniz şunlardır:
  - **Kullanıcı kimlik doğrulaması** (varsayılan): Kullanıcı KIMLIK bilgileri VPN 'de kimlik doğrular.
  - **Makine kimlik doğrulaması**: cihaz KIMLIK bilgileri VPN ile kimlik doğrular.

- **Kimlik doğrulama yöntemi**: sunucuya göndermek için istemci kimlik bilgilerinin türünü seçin. Seçenekleriniz şunlardır:
  - **Sertifikalar**: VPN 'de kimlik doğrulamak için mevcut bir sertifika profilini kullanır. Bu sertifika profilinin zaten Kullanıcı veya cihaza atanmış olduğundan emin olun. Aksi halde VPN bağlantısı başarısız olur.
    - **Sertifika türü**: sertifika tarafından kullanılan şifreleme türünü seçin. VPN sunucusunun bu tür bir sertifikayı kabul edecek şekilde yapılandırıldığından emin olun. Seçenekleriniz şunlardır:
      - **RSA** (varsayılan)
      - **ECDSA256**
      - **ECDSA384**
      - **ECDSA521**

  - **Kullanıcı adı ve parola** (yalnızca Kullanıcı kimlik doğrulaması): kullanıcılar VPN 'e bağlandıklarında, Kullanıcı adı ve parola istenir.
  - **Paylaşılan gizli** dizi (yalnızca makine kimlik doğrulaması): VPN sunucusuna göndermek için paylaşılan bir gizlilik girmenize olanak sağlar.
    - **Paylaşılan gizlilik**: önceden paylaşılan anahtar (PSK) olarak da bilinen paylaşılan parolayı girin. Değerin VPN sunucusunda yapılandırılmış paylaşılan gizli anahtar ile eşleştiğinden emin olun.

- **Sunucu sertifikası verenin ortak adı**: VPN sunucusunun VPN istemcisinde kimlik doğrulamasına izin verir. Cihazdaki VPN istemcisine gönderilen VPN sunucu sertifikasının sertifika verenin ortak adını (CN) girin. CN değerinin VPN sunucusundaki yapılandırmayla eşleştiğinden emin olun. Aksi halde VPN bağlantısı başarısız olur.
- **Sunucu sertifikası ortak adı**: sertifikanın kendısı için CN 'yi girin. Boş bırakılırsa, uzak tanımlayıcı değeri kullanılır.

- **Kullanılmayan eş algılama oranı**: VPN istemcisinin etkin olup OLMADıĞıNı, VPN istemcisinin ne sıklıkta denetleyeceğini seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı**: IOS/ıpados sistemi varsayılanını kullanır, bu da **Orta**seçim ile aynı olabilir.
  - **Hiçbiri**: kullanılmayan eşdüzey algılamayı devre dışı bırakır.
  - **Düşük**: her 30 dakikada bir canlı tutma iletisi gönderir.
  - **Orta** (varsayılan): 10 dakikada bir canlı tutma iletisi gönderir.
  - **Yüksek**: her 60 saniyede bir KeepAlive iletisi gönderir.

- **TLS sürüm aralığı en az**: kullanılacak en düşük TLS sürümünü girin. `1.0`, `1.1` Veya girin `1.2` . Boş bırakılırsa varsayılan değeri `1.0` kullanılır.
- **En yüksek TLS sürüm aralığı**: kullanılacak en fazla TLS sürümünü girin. `1.0`, `1.1` Veya girin `1.2` . Boş bırakılırsa varsayılan değeri `1.2` kullanılır.

> [!NOTE]
> Kullanıcı kimlik doğrulaması ve sertifikaları kullanılırken en düşük ve en yüksek TLS sürüm aralığı ayarlanmalıdır.

- **Kusursuz iletme gizliliği**: kusursuz iletme gizliliği 'NI (PFS) açmak için **Etkinleştir** ' i seçin. PFS, bir oturum anahtarının güvenliğinin tehlikeye girdiği etkiyi azaltan bir IP güvenlik özelliğidir. **Devre dışı bırak** (varsayılan) PFS kullanmaz.
- **Sertifika iptal denetimi**: VPN bağlantısının başarılı olmasına izin vermeden önce sertifikaların iptal edilmediğinden emin olmak için **Etkinleştir** ' i seçin. Bu denetim en iyi çabadır. Sertifikanın iptal edilip edilmediğini belirlemekten önce VPN sunucusu zaman aşımına uğrarsa, erişim izni verilir. **Devre dışı bırak** (varsayılan) iptal edilen sertifikaları denetlemez.

- **Güvenlik ilişkisi parametrelerini yapılandırma**: **Yapılandırılmadı** (varsayılan) iOS/ıpados Sistem varsayılanını kullanır. VPN sunucusuyla güvenlik ilişkilendirmeleri oluştururken kullanılan parametreleri girmek için **Etkinleştir** ' i seçin:
  - **Şifreleme algoritması**: istediğiniz algoritmayı seçin:
    - DES
    - 3DES
    - AES-128
    - AES-256 (varsayılan)
    - AES-128-GCM
    - AES-256-GCM
  - **Bütünlük algoritması**: istediğiniz algoritmayı seçin:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (varsayılan)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman grubu**: istediğiniz grubu seçin. Varsayılan grup `2` .
  - **Yaşam süresi** (dakika): anahtarlar döndürülünceye kadar güvenlik ilişkisinin ne kadar süreyle etkin kalacağını seçin. Ve arasında bir tam değer `10` girin `1440` (1440 dakika 24 saat). `1440` varsayılan değerdir.

- **Alt güvenlik ilişkilendirmeleri için ayrı bir parametre kümesi yapılandırın**: IOS/ıPADOS, Ike bağlantısı için ayrı parametreleri ve tüm alt bağlantıları yapılandırmanıza olanak tanır. 

  **Yapılandırılmadı** (varsayılan), önceki **güvenlik ilişkisi parametrelerini Yapılandır** ayarında girdiğiniz değerleri kullanır. VPN sunucusu ile *alt* güvenlik ilişkilendirmeleri oluştururken kullanılan parametreleri girmek için **Etkinleştir** ' i seçin:
  - **Şifreleme algoritması**: istediğiniz algoritmayı seçin:
    - DES
    - 3DES
    - AES-128
    - AES-256 (varsayılan)
    - AES-128-GCM
    - AES-256-GCM
  - **Bütünlük algoritması**: istediğiniz algoritmayı seçin:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (varsayılan)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman grubu**: istediğiniz grubu seçin. Varsayılan grup `2` .
  - **Yaşam süresi** (dakika): anahtarlar döndürülünceye kadar güvenlik ilişkisinin ne kadar süreyle etkin kalacağını seçin. Ve arasında bir tam değer `10` girin `1440` (1440 dakika 24 saat). `1440` varsayılan değerdir.

## <a name="automatic-vpn-settings"></a>Otomatik VPN ayarları

- **Uygulama başına VPN**: Uygulama başına VPN’i etkinleştirir. Belirli uygulamalar açıldığında VPN bağlantısının otomatik olarak tetiklenmesine izin verir. Ayrıca uygulamaları bu VPN profiliyle ilişkilendirir. Ikev2 üzerinde uygulama başına VPN desteklenmez. Daha fazla bilgi için bkz. [iOS/ıpados için uygulama BAŞıNA VPN ayarlama yönergeleri](vpn-setting-configure-per-app.md). 
  - **Sağlayıcı Türü**: Yalnızca Pulse Secure ve Özel VPN için kullanılabilir.
  - Pulse Secure veya Custom VPN ile iOS/ıpados **BAŞıNA VPN** profilleri kullanırken, uygulama katmanı Tüneli (App-proxy) veya paket düzeyinde tünel oluşturma (paket-tünel) seçeneğini belirleyin. Uygulama katmanı tünellemesi için **ProviderType** değerini **App-proxy** veya paket katmanı tünellemesi için **paket tüneli** olarak ayarlayın. Hangi değeri kullanmanız gerektiğini bilmiyorsanız VPN sağlayıcınızın belgelerine bakın.
  - **Bu VPN’i tetikleyecek Safari URL’leri**: Bir veya daha fazla web sitesi URL’si ekleyin. Bu URL’ler cihazda Safari tarayıcıyla ziyaret edildiğinde, VPN bağlantısı otomatik olarak kurulur.

- **İsteğe bağlı VPN**: VPN bağlantısının ne zaman başlatılacağını denetleyen koşullu kurallar yapılandırın. Örneğin, yalnızca cihaz şirketin Wi-Fi ağına bağlı olmadığında VPN bağlantısının kullanılacağı bir koşul oluşturun. Ya da bir koşul oluşturun. Örneğin, bir cihaz girdiğiniz DNS arama etki alanına erişemezse VPN bağlantısı başlatılmaz.

  - **SSID’ler veya DNS arama etki alanları**: Bu koşulun kablosuz ağ **SSID’lerini** mi yoksa **DNS arama etki alanlarını** mı kullanacağını seçin. Bir veya birden çok SSID veya arama etki alanı yapılandırmak için **Ekle**’yi seçin.
  - **URL dizesi araştırması**: İsteğe bağlıdır. Kuralın test olarak kullanacağı bir URL girin. Cihaz bu URL 'ye yeniden yönlendirmesiz erişirse VPN bağlantısı başlatılır. Cihaz hedef URL’ye bağlanır. Kullanıcı, URL dize araştırma sitesini görmez.

    Örneğin, URL dize araştırması, VPN 'i bağlamadan önce cihaz uyumluluğunu denetleyen bir denetim Web sunucusu URL 'sidir. Ya da URL, VPN aracılığıyla hedef URL 'ye bağlanmadan önce VPN 'in bir siteye bağlanma yeteneğini sınar.

  - **Etki alanı eylemi**: Aşağıdaki öğelerden birini seçin:
    - Gerekirse bağlan
    - Hiçbir zaman bağlanma
  - **Eylem**: Aşağıdaki öğelerden birini seçin:
    - Bağlan
    - Bağlantıyı değerlendir
    - Yoksayma
    - Bağlantıyı kes

## <a name="proxy-settings"></a>Proxy ayarları

Proxy kullanıyorsanız aşağıdaki ayarları yapılandırın. Proxy ayarları, Zscaler VPN bağlantıları için kullanılamaz.  

- **Otomatik yapılandırma betiği**: Proxy sunucusunu yapılandırmak için bir dosya kullanın. Yapılandırma dosyasını içeren **Proxy sunucu URL’si** (örneğin `http://proxy.contoso.com`) değerini girin.
- **Adres**: Proxy sunucusunun tam konak adına ait IP adresini girin.
- **Bağlantı noktası numarası**: Proxy sunucusuyla ilişkilendirilmiş bağlantı noktası numarasını girin.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulur ancak henüz herhangi bir işlem gerçekleştirmez. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).

[Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [MacOS](vpn-settings-macos.md)ve [Windows 10](vpn-settings-windows-10.md) cihazlarında VPN ayarlarını yapılandırın.
