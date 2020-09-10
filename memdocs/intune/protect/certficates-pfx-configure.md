---
title: Microsoft Intune-Azure 'da özel ve ortak anahtar sertifikaları kullanma | Microsoft Docs
description: Microsoft Intune ile ortak anahtar şifreleme standartları (PKCS) sertifikaları kullanın, kök sertifikalar ve sertifika şablonları ile çalışın, Microsoft Intune bağlayıcısını (NDES) yükleyip, bir PKCS sertifikası için cihaz yapılandırma profillerini kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28ca32bc65ee0c4647c22b10b6b5d47a25efa202
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643614"
---
# <a name="configure-and-use-pkcs-certificates-with-intune"></a>Intune ile PKCS sertifikalarını yapılandırma ve kullanma

Intune, özel ve ortak anahtar çifti (PKCS) sertifikalarının kullanımını destekler. Bu makale, şirket içi sertifika bağlayıcıları gibi gerekli altyapıyı yapılandırmanıza, PKCS sertifikasını dışarı aktarmaya ve sonra sertifikayı bir Intune cihaz yapılandırma profiline eklemenize yardımcı olabilir.

Microsoft Intune, kuruluşların kaynaklarına erişim ve kimlik doğrulama için PKCS sertifikaları kullanmak üzere yerleşik ayarları içerir. Sertifikalar, VPN veya WiFi ağı gibi şirket kaynaklarınıza kimlik doğrular ve erişimi güvenli hale getirin. Bu ayarları Intune 'daki cihaz yapılandırma profillerini kullanarak cihazlara dağıtırsınız.

İçeri aktarılan PKCS sertifikalarını kullanma hakkında daha fazla bilgi için bkz. [Içeri AKTARıLMıŞ PFX sertifikaları](certificates-imported-pfx-configure.md).


## <a name="requirements"></a>Gereksinimler

PKCS sertifikalarını Intune ile kullanmak için aşağıdaki altyapıya sahip olmanız gerekir:

- **Active Directory etki alanı**:  
  Bu bölümde listelenen tüm sunucular Active Directory etki alanına katılmalıdır.

  Active Directory Domain Services (AD DS) yükleme ve yapılandırma hakkında daha fazla bilgi için bkz. [AD DS tasarım ve planlama](/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning).

- **Sertifika yetkilisi**:  
   Bir kuruluş sertifika yetkilisi (CA).

  Active Directory Sertifika Hizmetleri 'ni (AD CS) yükleme ve yapılandırma hakkında daha fazla bilgi için bkz. [Active Directory Sertifika Hizmetleri adım adım Kılavuzu](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772393(v=ws.10)).

  > [!WARNING]  
  > Intune, AD CS'yi, Tek Başına bir CA yerine bir Kurumsal Sertifika Yetkilisi (CA) ile çalıştırmanızı gerektirir.

- **İstemci**:  
  Kurumsal CA 'ya bağlanmak için.

- **Kök sertifika**:  
  Kök sertifikanızın Kurumsal CA'ndan dışa aktarılmış bir kopyası.

- **Microsoft Intune Için PFX Sertifika Bağlayıcısı**:

  Önkoşullar ve yayın sürümleri dahil olmak üzere PFX Sertifika Bağlayıcısı hakkında daha fazla bilgi için bkz. [sertifika bağlayıcıları](certificate-connectors.md).

  > [!IMPORTANT]
  > PFX Sertifika Bağlayıcısı sürüm 6.2008.60.607 sürümünden itibaren, Microsoft Intune Bağlayıcısı artık PKCS sertifika profilleri için gerekli değildir. 
  
## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>Kök sertifikayı Kurumsal CA'dan dışa aktarın

VPN, WiFi veya diğer kaynaklarla bir cihazın kimliğini doğrulamak için bir cihazın kök veya ara CA sertifikası olması gerekir. Aşağıdaki adımlar, Kurumsal CA'nızdan gerekli sertifikayı nasıl alacağınızı açıklar.

**Komut satırı kullanın**:  

1. Kök sertifika yetkilisi sunucusunda yönetici hesabıyla oturum açın.

2. **Start**  >  **Çalıştır**' a gidin ve ardından komut istemi 'ni açmak için **cmd** girin.

3. Kök sertifikayı *CA_NAME. cer*adlı bir dosya olarak dışarı aktarmak için **certutil-ca. CERT CA_NAME. cer** belirtin.

## <a name="configure-certificate-templates-on-the-ca"></a>CA 'da sertifika şablonlarını yapılandırma

1. Yönetici ayrıcalıklarına sahip bir hesapla Kurumsal CA’nızda oturum açın.
2. **Sertifika Yetkilisi** konsolunu açın, **Sertifika Şablonları**'na sağ tıklayın ve **Yönet**'i seçin.
3. **Kullanıcı** sertifika şablonunu bulun, sağ tıklayın ve **Yinelenen şablon** ' u seçerek **yeni şablonun özelliklerini**açın.

    > [!NOTE]
    > S/MIME e-posta imzalama ve şifreleme senaryolarında, birçok yönetici imzalama ve şifreleme için ayrı sertifikalar kullanır. Microsoft Active Directory Sertifika Hizmetlerini kullanıyorsanız, S/MIME e-posta imzalama sertifikaları için **Yalnızca Exchange İmzası** şablonunu ve S/MIME şifreleme sertifikaları için de **Exchange Kullanıcısı** şablonunu kullanabilirsiniz.  3. taraf bir sertifika yetkilisi kullanıyorsanız, imzalama ve şifreleme şablonlarını ayarlamaya yönelik kendi kılavuzlarını gözden geçirmeniz önerilir.

4. **Uyumluluk** sekmesinde:

    - **Sertifika Yetkilisi**’ni **Windows Server 2008 R2**’ye ayarlayın
    - **Sertifika alıcısını**’nı **Windows Server 7/ 2008 R2**’ye ayarlayın

5. **Genel** sekmesinde **Şablon görünen adını** sizin için anlamı olan bir şeye ayarlayın.

    > [!WARNING]
    > **Şablon adı** varsayılan olarak **şablon görünen adı** ile *boşluksuz* aynıdır. Şablon adını not alın çünkü daha sonra gerekecektir.

6. **İstek İşleme**'de **Özel anahtar dışarı aktarılabilsin**'i seçin.

    > [!NOTE]
    > SCEP 'in aksine, PKCS, sertifika özel anahtarı bağlayıcının yüklendiği ve cihaza olmadığı sunucuda oluşturulur. Sertifika bağlayıcısının PFX sertifikasını dışarı aktarıp cihaza gönderebilmesi için, sertifika şablonunun özel anahtarın dışarı verilmesine izin verdiğinden emin olmanız gerekir. 
    >
    > Ancak, sertifikaların, dışarı aktarılabilir değil olarak işaretlenen özel anahtarla cihazın kendisinde yüklü olduğunu lütfen unutmayın.

7. **Şifreleme**'de **En az anahtar boyutu**’nun 2048 olarak ayarlandığını onaylayın.
8. **Konu Adı**'nda **İstekte sağla**'yı seçin.
9. **Uzantılar**'da, **Uygulama İlkeleri** altında Şifreleme Dosya Sistemi, Güvenli E-posta ve İstemci Kimlik Doğrulamasını gördüğünüzü onaylayın.

    > [!IMPORTANT]
    > İOS/ıpados sertifika şablonları için, **Uzantılar** sekmesine gidin, **anahtar kullanımı**' nı güncelleştirin ve **imzanın kaynak kanıtı** olduğunu onaylayın.

10. **Güvenlik**' te, Microsoft Intune bağlayıcısını yüklediğiniz sunucunun bilgisayar hesabını ekleyin. Bu hesabın izinleri **Okuma** ve **Kaydetme**’sine izin verin.
11. **Apply**  >  Sertifika şablonunu kaydetmek için Uygula**Tamam ' ı** seçin. **Sertifika Şablonları konsolunu**kapatın.
12. **Sertifika Yetkilisi** konsolunda **Sertifika Şablonları** > **Yeni** > **Yayımlanacak Sertifika Şablonu**’na sağ tıklayın. Önceki adımlarda oluşturduğunuz şablonu seçin. **Tamam**’ı seçin.
13. Sunucunun kayıtlı cihazlar ve kullanıcılar için sertifikaları yönetmesi için aşağıdaki adımları kullanın:

    1. Sertifika Yetkilisine sağ tıklayın ve ardından **Özellikler**’i seçin.
    2. Güvenlik sekmesinde, bağlayıcıları çalıştırdığınız sunucunun bilgisayar hesabını (Microsoft Intune için**Microsoft Intune Bağlayıcısı** veya **PFX Sertifika Bağlayıcısı**) ekleyin. 
    3. **Sertifikaları Yayımla ve Yönet** ve **Sertifikaları İste**’ye izin ver, bilgisayar hesabına izin verir.

14. Kurumsal CA'da oturumu kapatın.

## <a name="download-install-and-configure-the-pfx-certificate-connector"></a>PFX Sertifika bağlayıcısını indirme, yükleme ve yapılandırma

Başlamadan önce, [bağlayıcının gereksinimlerini gözden geçirin](certificate-connectors.md) ve ortamınız ile Windows Server 'ın bağlayıcıyı desteklemeye hazırlandığından emin olun.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **sertifika bağlayıcıları**  >  **+ Ekle**' yi seçin.

3. PKCS #12 Bağlayıcısı için *sertifika Bağlayıcısı yazılımını indir* ' e tıklayın ve dosyayı bağlayıcıyı yükleyeceğiniz sunucudan erişebileceğiniz bir konuma kaydedin.

   ![Microsoft Intune Bağlayıcısı indirme](./media/certficates-pfx-configure/download-connector.png)

4. İndirme tamamlandıktan sonra, sunucusunda oturum açın ve yükleyiciyi çalıştırın (PfxCertificateConnectorBootstrapper.exe).  
   - Varsayılan yükleme konumunu kabul ettiğinizde, bağlayıcı ' a yüklenir `Program Files\Microsoft Intune\PFXCertificateConnector` .
   - Bağlayıcı hizmeti yerel sistem hesabının altında çalışır. İnternet erişimi için bir proxy gerekliyse, yerel hizmet hesabının sunucudaki proxy ayarlarına erişediğini doğrulayın.

5. Microsoft Intune için PFX Sertifika Bağlayıcısı yüklendikten sonra **Kayıt** sekmesini açar. Intune bağlantısını etkinleştirmek için **Oturum Aç**'ı seçin ve Azure genel yöneticisi veya Intune yöneticisi izinleri olan bir hesap girin.

   > [!WARNING]
   > Varsayılan olarak, Windows Server **IE artırılmış güvenlik yapılandırması** **Açık** olarak ayarlanır ve bu, Office 365 ' de oturum açma sorunları oluşmasına neden olabilir.

6. **CA hesabı** sekmesini seçin ve ardından sertifika verme ve yönetme iznine sahip olan bir hesabın kimlik bilgilerini veren sertifika yetkiliniz üzerinde girin. Bu kimlik bilgileri, sertifika yetkilisinde sertifika iptali gerçekleştirmek için kullanılacaktır. 

    Yaptığınız değişiklikleri **uygulayın**.

7. Pencereyi kapatın.

8. Microsoft Endpoint Manager Yönetim merkezinde, **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **sertifika bağlayıcıları**' na geri dönün. Birkaç dakika içinde yeşil bir onay işareti görünür ve bağlantı durumu güncellenir. Bağlayıcı sunucusu artık Intune ile iletişim kurabilir.

## <a name="create-a-trusted-certificate-profile"></a>Güvenilen bir sertifika profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. Seçin ve **cihazlar**  >  **yapılandırma profilleri**  >  **Profil oluştur**' a gidin.

3. Aşağıdaki özellikleri girin:
   - **Platform**: Bu profili alacak cihazların platformunu seçin.
   - **Profil**: **Güvenilen sertifika** seçin
  
4. **Oluştur**’u seçin.

5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:
   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı *şirketin tamamına yönelik güvenilen sertifika profilidir*.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda, daha önce verdiğiniz. cer dosya kök CA sertifikasını belirtin.

   > [!NOTE]
   > **Adım 3**' te seçtiğiniz platforma bağlı olarak, sertifika için **Hedef depoyu** seçme seçeneğiniz olabilir veya olmayabilir.

   ![Bir profili oluşturun ve güvenilen bir sertifika yükleyin](./media/certficates-pfx-configure/certificates-pfx-configure-profile-fill.png)

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

   **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Bu sertifika profilini, PKCS sertifika profilini alan gruplara dağıtmayı planlayın. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

    **İleri**’yi seçin.

11. (*Yalnızca Windows 10 Için geçerlidir*) **Uygulanabilirlik kuralları**' nda, bu profilin atanmasını iyileştirmek için uygulanabilirlik kurallarını belirtin. Profili, bir cihazın işletim sistemi sürümüne veya sürümüne göre atamayı veya atamayı seçebilirsiniz.

  Daha fazla bilgi için *Microsoft Intune bir cihaz profili oluşturma*içindeki [uygulanabilirlik kuralları](../configuration/device-profile-create.md#applicability-rules) bölümüne bakın.

12. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. Oluştur ' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="create-a-pkcs-certificate-profile"></a>PKCS sertifika profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. Seçin ve **cihazlar**  >  **yapılandırma profilleri**  >  **Profil oluştur**' a gidin.

3. Aşağıdaki özellikleri girin:
   - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:
     - Android cihaz yöneticisi
     - Android kurumsal > tam olarak yönetilen, adanmış ve şirkete ait Iş profili
     - Yalnızca Android kurumsal > Iş profili
     - iOS/iPadOS
     - macOS
     - Windows 10 ve üzeri
   - **Profil**: **PKCS sertifikası** seçin

   > [!NOTE]
   > Android kurumsal profiline sahip cihazlarda, PKCS sertifika profili kullanılarak yüklenen sertifikalar cihazda görünmez. Başarılı sertifika dağıtımını onaylamak için, Intune konsolundaki profilin durumunu denetleyin.
4. **Oluştur**’u seçin.

5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:
   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı, *tüm şirket Için PKCS profilidir*.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.
7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:-Android Cihaz Yöneticisi-Android Enterprise-iOS/ıpados-Windows 10
   
   |Ayar     | Platform     | Ayrıntılar   |
   |------------|------------|------------|
   |**Yenileme eşiği (%)**        |<ul><li>Tümü         |Önerilen %20  | 
   |**Sertifika geçerlilik süresi**  |<ul><li>Tümü         |Sertifika şablonunu değiştirmediyseniz bu seçenek bir yıla ayarlanmış olabilir. |
   |**Anahtar depolama sağlayıcısı (KSP)**   |<ul><li>Windows 10  |Windows için, cihazdaki anahtarların depolanacağı yeri seçin. |
   |**Sertifika yetkilisi**      |<ul><li>Tümü         |Kuruluş sertifika yetkilinizin iç tam etki alanı adını (FQDN) görüntüler.  |
   |**Sertifika yetkilisi adı** |<ul><li>Tümü         |Kuruluş SERTIFIKA yetkilinizin adını (örneğin, "contoso sertifika yetkilisi") listeler. |
   |**Sertifika şablonu adı**    |<ul><li>Tümü         |Sertifika şablonunuzun adını listeler. |
   |**Sertifika türü**             |<ul><li>Android Enterprise (*Iş profili*)</li><li>iOS</li><li>macOS</li><li>Windows 10 ve üzeri|Bir tür seçin: <ul><li> **Kullanıcı** sertifikaları hem Kullanıcı hem de cihaz özniteliklerini, sertifikanın konu ve San 'ı içerebilir. </il><li>**Cihaz** sertifikaları, sertifikanın konu ve San 'ı yalnızca cihaz özniteliklerini içerebilir. Cihazı, bilgi noktaları veya diğer paylaşılan cihazlar gibi Kullanıcı-daha az cihazlar gibi senaryolar için kullanın.  <br><br> Bu seçim konu adı biçimini etkiler. |
   |**Konu adı biçimi**          |<ul><li>Tümü         |Konu adı biçiminin nasıl yapılandırılacağı hakkında ayrıntılı bilgi için bu makalenin ilerleyen kısımlarında yer alan [Konu adı biçimi](#subject-name-format) bölümüne bakın.  <br><br> Çoğu platformda, aksi belirtilmedikçe **ortak ad** seçeneğini kullanın. <br><br>Aşağıdaki platformlar için konu adı biçimi sertifika türü tarafından belirlenir: <ul><li>Android Enterprise (*Iş profili*)</li><li>iOS</li><li>macOS</li><li>Windows 10 ve üzeri</li></ul>  <p>  |
   |**Konu diğer adı**     |<ul><li>Tümü         |*Öznitelik*için, aksi belirtilmedikçe **Kullanıcı asıl adı (UPN)** seçeneğini belirleyin, karşılık gelen bir *değeri*yapılandırın ve ardından **Ekle**' ye tıklayın. <br><br>Daha fazla bilgi için bu makalenin ilerleyen kısımlarında [Konu adı biçimi](#subject-name-format) bölümüne bakın.|
   |**Genişletilmiş anahtar kullanımı**           |<ul><li> Android cihaz yöneticisi </li><li>Android Enterprise (*cihaz sahibi*, *iş profili*) </li><li>Windows 10 |Sertifikalar genellikle kullanıcı veya cihazın bir sunucuda kimliğini doğrulayabilmesi için *Istemci kimlik doğrulaması* gerektirir. |
   |**Tüm uygulamaların özel anahtara erişimine izin ver** |<ul><li>macOS  |İlişkili Mac cihaz için yapılandırılmış uygulamaların PKCS Certificates özel anahtarına erişimi **sağlamak için '** i ayarlayın. <br><br> Bu ayar hakkında daha fazla bilgi için Apple geliştirici belgelerindeki [yapılandırma profili başvurusunun](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf) sertifika yükü *bölümüne bakın.* |
   |**Kök sertifika**             |<ul><li>Android cihaz yöneticisi </li><li>Android Enterprise (*cihaz sahibi*, *iş profili*) |Daha önce atanmış olan bir kök CA sertifika profili seçin. |

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

   **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Bu sertifika profilini, güvenilen sertifika profilini alan gruplara dağıtmayı planlayın. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. Oluştur ' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.


### <a name="subject-name-format"></a>Konu adı biçimi

Aşağıdaki platformlar için bir PKCS sertifika profili oluşturduğunuzda, konu adı biçimi seçenekleri, seçtiğiniz sertifika türüne, **Kullanıcı** veya **cihaza**bağlıdır.  

Platform

- Android Enterprise (*Iş profili*)
- iOS
- macOS
- Windows 10 ve üzeri

> [!NOTE]
> Elde edilen sertifika Imzalama Isteğindeki (CSR) konu adı, kaçış karakteri olarak aşağıdaki karakterlerden birini içerdiğinde (bir ters eğik çizgiyle devam eder), [SCEP için görülen aynı sorun olan](certificates-profile-scep.md#avoid-certificate-signing-requests-with-escaped-special-characters) sertifikaları almak için PKCS kullanma konusunda bilinen bir sorun vardır \\ :
> - \+
> - ;
> - ,
> - =

- **Kullanıcı sertifika türü**  
  *Konu adı biçimi* için biçim seçenekleri iki değişken Içerir: **ortak ad (CN)** ve **e-posta (e)**. **Ortak Ad (CN)** şu iki değerden biri olarak ayarlanabilir:

  - **CN = {{username}}**: kullanıcının Kullanıcı asıl adı (gibi) janedoe@contoso.com .
  - **CN={{AAD_Device_ID}}**: Azure Active Directory’ye (AD) yeni bir cihaz kaydettiğinizde atanan bir kimlik. Bu kimlik genellikle Azure AD’de kimlik doğrulamak için kullanılır.
  - **CN = {{SERIALNUMBER}}**: genellikle üretici tarafından bir cihazı tanımlamak için kullanılan benzersiz seri numarası (sn).
  - **CN = {{ımekarmsayı}}**: bir cep telefonu tanımlamak Için kullanılan uluslararası mobil ekipman KIMLIĞI (IMEI) benzersiz numarası.
  - **CN = {{OnPrem_Distinguished_Name}}**: *CN = Gamze Etikan, OU = USERACCOUNTS, DC = Corp, DC = contoso, DC = com*gibi virgülle ayrılmış göreli ayırt edici adların sırası.

    *{{OnPrem_Distinguished_Name}}* değişkenini kullanmak Için, Azure AD 'nize [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) kullanarak *onpremisesdistinguishedname* Kullanıcı özniteliğini eşitlediğinizden emin olun.

  - **CN = {{onPremisesSamAccountName}}**: Yöneticiler, *adlı BIR*özniteliğe Azure AD connect kullanarak sAMAccountName ÖZNITELIĞINI Active Directory 'den Azure AD 'ye eşitleyebilir. Intune, bu değişkeni bir sertifika konusunun sertifika verme isteğinin bir parçası olarak kullanabilir. SamAccountName özniteliği, Windows 'un önceki bir sürümünden (Windows 2000 öncesi) istemcileri ve sunucuları desteklemek için kullanılan Kullanıcı oturum açma adıdır. Kullanıcı oturum açma adı biçimi: *EtkiAlanıAdı \ testuser*veya yalnızca *testuser*.

    *{{OnPremisesSamAccountName}}* değişkenini kullanmak Için, Azure AD 'nize [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) kullanarak *onPremisesSamAccountName* User özniteliğini eşitlediğinizden emin olun.

  Bu değişkenlerin ve statik dizelerin bir veya birkaç tanesinin bir bileşimini kullanarak aşağıdaki gibi özel bir konu adı biçimi oluşturabilirsiniz:  
  - **CN={{KullanıcıAdı}},E={{EpostaAdresi}},OU=Mobil,O=Finans Grubu,L=Redmond,ST=Washington,C=US**
  
  Bu örnekte, CN ve E değişkenlerini kullanan bir konu adı biçimi ve kuruluş birimi, kuruluş, konum, durum ve ülke değerleri için dizeler bulunur. [CertStrToName işlevi](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea), bu işlevi ve desteklenen dizelerini açıklar.

- **Cihaz sertifika türü**  
  Konu adı biçimi için biçim seçenekleri aşağıdaki değişkenleri içerir: 
  - **{{AAD_Device_ID}}**
  - **{{Device_Serial}}**
  - **{{Device_IMEI}}**
  - **{{SerialNumber}}**
  - **{{Imekarmsayı}}**
  - **{{Azureaddeviceıd}}**
  - **{{WiFiMacAddress}}**
  - **{{IMEı}}**
  - **{{Aygıtadı}}**
  - **{{Fullyıqualifieddomainname}}** *(yalnızca Windows ve etki alanına katılmış cihazlar için geçerlidir)*
  - **{{MEıD}}**

  Bu değişkenleri ve metin kutusu içinde değişkeni için metni belirtebilirsiniz. Örneğin, *Device1* adlı bir cihazın ortak adı **CN = {{aygıtadı}} Device1**olarak eklenebilir.

  > [!IMPORTANT]  
  > - Bir değişken belirttiğinizde, bir hatadan kaçınmak için, değişken adını örnekte görüldüğü gibi küme ayraçları {} içine alın.  
  > - **IMEI**, **SerialNumber**ve **fullyıqualifieddomainname**gibi bir cihaz sertifikasının *Konu* veya *San* 'ı üzerinde kullanılan cihaz özellikleri, cihaza erişimi olan bir kişi tarafından sızılmış özelliklerdir.
  > - Bir cihazın, bu cihaza yüklemek için bir sertifika profilinde belirtilen tüm değişkenleri desteklemesi gerekir.  Örneğin, bir SCEP profilinin konu adında **{{IMEI}}** kullanılıyorsa ve IMEI numarası olmayan bir cihaza atanırsa, profil yüklenemez.

## <a name="next-steps"></a>Sonraki adımlar

[Sertifikalar IÇIN SCEP kullanın](certificates-scep-configure.md)veya [bir Symantec PKI Manager Web hizmetinden PKCS sertifikaları verin](certificates-digicert-configure.md).

[PKCS sertifika profillerinin sorunlarını giderme](../protect/troubleshoot-pkcs-certificate-profiles.md)
