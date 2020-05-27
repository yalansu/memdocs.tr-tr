---
title: Microsoft Intune-Azure 'da içeri aktarılan PFX sertifikalarını kullanma | Microsoft Docs
description: Microsoft Intune ile içeri aktarılan ortak anahtar şifreleme standartları (PKCS) sertifikalarını kullanın. Sertifikaları içeri aktarın, sertifika şablonlarını yapılandırın, Intune Içeri aktarılmış PFX Sertifika bağlayıcısını yükler ve Içeri aktarılan bir PKCS sertifika profili oluşturun.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda; rimarram
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 13824c82b426e1efb00dce2db7c9f4a2dd5bb9ee
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990341"
---
# <a name="configure-and-use-imported-pkcs-certificates-with-intune"></a>Intune ile içeri aktarılan PKCS sertifikalarını yapılandırma ve kullanma

Microsoft Intune, genellikle e-posta profilleriyle S/MIME şifrelemesi için kullanılan içeri aktarılan ortak anahtar çifti (PKCS) sertifikalarının kullanımını destekler. Intune 'daki belirli e-posta profilleri, s/MIME imzalama sertifikası ve S/MIME şifreleme sertifikası tanımlayabileceğiniz S/MIME 'yi etkinleştirme seçeneğini destekler.

E-posta belirli bir sertifika ile şifrelendiğinden, S/MIME şifrelemesi zor olur:

- Şifresinin çözülmesi için e-postayı okuduğunuz cihazda e-postayı şifreleyen sertifikanın özel anahtarına sahip olmanız gerekir.
- Cihazdaki bir sertifikanın süresi dolmadan önce, cihazların yeni e-postanın şifresini çözmeye devam edebilmesi için yeni bir sertifika içeri aktarmanız gerekir. Bu sertifikaların yenilenmesi desteklenmiyor.
- Şifreleme sertifikaları düzenli olarak yenilenir, bu da eski e-postaların şifresinin çözülmesi devam edebilmesini sağlamak için cihazlarınızda geçmiş sertifikayı tutmak isteyebileceğiniz anlamına gelir.  

Aynı sertifikanın cihazlarda kullanılması gerektiğinden, bu sertifika teslim mekanizmaları cihaz başına benzersiz sertifikalar sunduğundan, bu amaçla [SCEP](certificates-scep-configure.md) veya [PKCS](certficates-pfx-configure.md) sertifika profillerini kullanmak mümkün değildir.

Intune ile S/MIME kullanma hakkında daha fazla bilgi için, [e-postayı şifrelemek üzere s/MIME kullanın](certificates-s-mime-encryption-sign.md).

## <a name="supported-platforms"></a>Desteklenen platformlar

Intune, aşağıdaki platformlar için PFX sertifikalarının içeri aktarımını destekler:

- Android-Cihaz Yöneticisi
- Android kurumsal-tam yönetilen
- Android kurumsal Iş profili
- iOS/iPadOS
- macOS
- Windows 10

## <a name="requirements"></a>Gereksinimler

İçeri aktarılmış PKCS sertifikalarını Intune ile kullanmak için aşağıdaki altyapıya sahip olmanız gerekir:

- **Microsoft Intune Için PFX Sertifika Bağlayıcısı**:

  Her Intune kiracısı, bu bağlayıcının tek bir örneğini destekler. Bu bağlayıcıyı, Microsoft Intune sertifika bağlayıcısının bir örneğiyle aynı sunucuya yükleyebilirsiniz.

  Bu bağlayıcı, belirli bir kullanıcı için S/MIME e-posta şifrelemesi için Intune 'a içeri aktarılan PFX dosyaları isteklerini işler.

  Bu bağlayıcı, yeni sürümler kullanılabilir hale geldiğinde kendisini otomatik olarak güncelleştirebilir. Güncelleştirme özelliğini kullanmak için, bağlayıcının **443**numaralı bağlantı noktasında **AutoUpdate.msappproxy.net** ile iletişim kurabildiğinden emin olmanız gerekir.

  Daha fazla bilgi için bkz. [Microsoft Intune Için ağ uç noktaları](../fundamentals/intune-endpoints.md)ve [Intune ağ yapılandırma gereksinimleri ve bant genişliği](../fundamentals/network-bandwidth-use.md).

- **Windows Server**:

  Microsoft Intune için PFX Sertifika bağlayıcısını barındırmak üzere bir Windows Server kullanın.  Bağlayıcı, Intune 'a içeri aktarılan sertifikalara yönelik istekleri işlemek için kullanılır.
  
  Bağlayıcının, [cihaz uç noktası içeriklerimizde](https://docs.microsoft.com/intune/fundamentals/intune-endpoints#access-for-managed-devices)bulunan yönetilen cihazlar için ayrıntılı bağlantı noktalarına erişimi olması gerekir.

  Intune, *Microsoft Intune Için PFX Sertifika Bağlayıcısı*ile aynı sunucuya *Microsoft Intune sertifika Bağlayıcısı* yüklenmesini destekler.

  Bağlayıcıyı desteklemek için, sunucunun .NET 4,6 Framework veya üstünü çalıştırması gerekir. Bağlayıcıyı yüklemeye başladığınızda .NET 4,6 çerçevesi yüklenmemişse, bağlayıcı yüklemesi otomatik olarak yüklenir.

- **Visual Studio 2015 veya üzeri** (isteğe bağlı):

  Microsoft Intune için PFX sertifikalarını içeri aktarmaya yönelik cmdlet 'lerle birlikte yardımcı PowerShell modülünü oluşturmak için Visual Studio 'Yu kullanabilirsiniz. Yardımcı PowerShell cmdlet 'lerini almak için bkz. [GitHub 'Da Pfxımport PowerShell projesi](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

## <a name="how-it-works"></a>Nasıl çalışır?

Bir kullanıcıya **içeri aktarılan BIR PFX sertifikasını** dağıtmak için Intune 'u kullandığınızda, cihaza ek olarak iki bileşen oynatılır:

- **Intune hizmeti**: PFX sertifikalarını şifreli bir durumda depolar ve sertifikanın Kullanıcı cihazına dağıtımını işler.  Sertifikaların özel anahtarlarını koruyan parolalar, Intune 'un özel anahtara herhangi bir zamanda erişemeyeceğinden emin olmak için bir donanım güvenlik modülü (HSM) veya Windows şifrelemesi kullanılarak karşıya yüklenmeden önce şifrelenir.

- **Microsoft Intune Için PFX Sertifika Bağlayıcısı**: bir cihaz Intune 'a AKTARıLMıŞ bir PFX sertifikası istediğinde, şifreli parola, sertifika ve cihazın ortak anahtarı bağlayıcıya gönderilir.  Bağlayıcı, şirket içi özel anahtarı kullanarak parolanın şifresini çözer ve sertifikayı Intune 'a geri göndermeden önce, parolayı (ve iOS kullanılıyorsa tüm plist profillerini) cihaz anahtarıyla yeniden şifreler.  Intune daha sonra sertifikayı cihaza gönderir ve cihaz cihazın özel anahtarıyla şifresini çözebilir ve sertifikayı yükler.

## <a name="download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune"></a>Microsoft Intune için PFX Sertifika bağlayıcısını indirin, yükleyin ve yapılandırın

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **sertifika bağlayıcıları**  >  **Ekle**' yi seçin.

   ![Microsoft Intune indirmek için PFX Sertifika Bağlayıcısı](./media/certificates-imported-pfx-configure/download-imported-pfxconnector.png)

3. *Microsoft Intune Için PFX Sertifika bağlayıcısını* , bağlayıcıyı yükleyeceğiniz sunucudan erişilebilen bir konuma indirmek için yönergeleri izleyin.

4. İndirme tamamlandıktan sonra, sunucusunda oturum açın ve yükleyiciyi (PfxCertificateConnectorBootstrapper. exe) çalıştırın.  
   - Varsayılan yükleme konumunu kabul ettiğinizde, bağlayıcı ' a yüklenir `Program Files\Microsoft Intune\PFXCertificateConnector` .
   - Bağlayıcı hizmeti yerel sistem hesabının altında çalışır. İnternet erişimi için bir proxy gerekliyse, yerel hizmet hesabının sunucudaki proxy ayarlarına erişediğini doğrulayın.

5. Microsoft Intune için PFX Sertifika Bağlayıcısı yüklendikten sonra **Kayıt** sekmesini açar. Intune bağlantısını etkinleştirmek için **Oturum Aç**'ı seçin ve Azure genel yöneticisi veya Intune yöneticisi izinleri olan bir hesap girin.

   > [!WARNING]
   > Varsayılan olarak, Windows Server **IE artırılmış güvenlik yapılandırması** **Açık** olarak ayarlanır ve bu, Office 365 ' de oturum açma sorunları oluşmasına neden olabilir.

6. Pencereyi kapatın.

7. Microsoft Endpoint Manager Yönetim merkezinde, **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **sertifika bağlayıcıları**' na geri dönün. Birkaç dakika içinde yeşil bir onay işareti görünür ve bağlantı durumu güncellenir. Bağlayıcı sunucusu artık Intune ile iletişim kurabilir.

## <a name="import-pfx-certificates-to-intune"></a>PFX sertifikalarını Intune 'a aktarma

Kullanıcılarınızın PFX sertifikalarını Intune 'a aktarmak için [Microsoft Graph](https://docs.microsoft.com/graph) kullanırsınız. GitHub 'da yardımcı [Pfxiçeri aktarma PowerShell projesi](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell) , işlemleri kolay bir şekilde yapmak için cmdlet 'ler sağlar.

Graph kullanarak kendi özel çözümünüzü kullanmayı tercih ediyorsanız, [Userpfxsertifikası kaynak türünü](https://docs.microsoft.com/graph/api/resources/intune-raimportcerts-userpfxcertificate?view=graph-rest-beta)kullanın.

### <a name="build-pfximport-powershell-project-cmdlets"></a>Derleme ' Pfxımport PowerShell projesi ' cmdlet 'leri

PowerShell cmdlet 'lerini kullanmak için, Visual Studio kullanarak projeyi kendiniz derleyebilirsiniz. İşlem düz bir işlemdir ve sunucuda çalıştırılabileceği sürece, iş istasyonunuzda çalıştırmanızı öneririz.  

1. GitHub 'daki [Intune-kaynak erişimi](https://github.com/microsoft/Intune-Resource-Access) deposunun köküne gidin ve sonra da depoyu makinenize git ile indirin veya kopyalayın.

   ![GitHub indirme düğmesi](./media/certificates-imported-pfx-configure/github-download.png)

2. ' A gidin `.\Intune-Resource-Access-develop\src\PFXImportPowershell\` ve **Pfxımportps. sln**dosyasını kullanarak Visual Studio ile projeyi açın.

3. Üstteki sayfada **hata ayıklamanın** **sürümüne**geçin.

4. **Derleme** bölümüne gidin ve **derleme pfxımportps**' yi seçin. Birkaç dakika içinde, Visual Studio 'nun sol alt kısmında bulunan **Derleme başarılı** onay onayını görürsünüz.

   ![Visual Studio derleme seçeneği](./media/certificates-imported-pfx-configure/vs-build-release.png)

5. Yapı işlemi, üzerinde PowerShell modülü ile yeni bir klasör oluşturur `.\Intune-Resource-Access-develop\src\PFXImportPowershell\PFXImportPS\bin\Release` .

   Bu **Sürüm** klasörünü sonraki adımlar için kullanacaksınız.

### <a name="create-the-encryption-public-key"></a>Şifreleme ortak anahtarını oluşturma

PFX sertifikalarını ve özel anahtarlarını Intune 'a içeri aktarırsınız. Özel anahtarı koruyan parola, şirket içinde depolanan bir ortak anahtarla şifrelenir. Ortak/özel anahtar çiftlerini oluşturmak ve depolamak için Windows şifrelemesi, bir donanım güvenlik modülü ya da başka bir şifreleme türü kullanabilirsiniz.  Kullanılan şifrelemenin türüne bağlı olarak, ortak/özel anahtar çifti, yedekleme amacıyla bir dosya biçiminde aktarılabilir.

PowerShell modülü, Windows şifrelemesi kullanarak bir anahtar oluşturmak için yöntemler sağlar. Ayrıca, bir anahtar oluşturmak için diğer araçları da kullanabilirsiniz.  

#### <a name="to-create-the-encryption-key-using-windows-cryptography"></a>Windows şifrelemesi kullanarak şifreleme anahtarını oluşturmak için

1. Visual Studio tarafından oluşturulan *Sürüm* klasörünü **Microsoft Intune Için PFX Sertifika bağlayıcısını**yüklediğiniz sunucuya kopyalayın. Bu klasör PowerShell modülünü içerir.

2. Sunucusunda, *PowerShell* 'i yönetici olarak açın ve ardından PowerShell modülünü içeren *yayın* klasörüne gidin.

3. Modülünü içeri aktarmak için, `Import-Module .\IntunePfxImport.psd1` modülünü içeri aktarmak üzere öğesini çalıştırın.

4. Sonra, Çalıştır`Add-IntuneKspKey -ProviderName "Microsoft Software Key Storage Provider" -KeyName "PFXEncryptionKey"`

   > [!TIP]
   > PFX sertifikalarını içeri aktardığınızda kullandığınız sağlayıcının yeniden seçilmesi gerekir. Farklı bir sağlayıcı kullanılması desteklenmekle birlikte, **Microsoft yazılım anahtarı depolama sağlayıcısını**kullanabilirsiniz. Anahtar adı da örnek olarak sağlanır ve tercih ettiğiniz farklı bir anahtar adı kullanabilirsiniz.

   Sertifikayı iş istasyonunuzdan içeri aktarmayı planlıyorsanız, bu anahtarı aşağıdaki komutla bir dosyaya dışarı aktarabilirsiniz:`Export-IntunePublicKey -ProviderName "<ProviderName>" -KeyName "<KeyName>" -FilePath "<File path\Filename.PFX>"`

   Özel anahtar, içeri aktarılan PFX sertifikalarının başarıyla işlenebilmesi için, Microsoft Intune için PFX Sertifika bağlayıcısını barındıran sunucuda içeri aktarılmalıdır.

#### <a name="to-use-a-hardware-security-module-hsm"></a>Donanım güvenlik modülünü (HSM) kullanmak için

Ortak/özel anahtar çiftini oluşturmak ve depolamak için bir donanım güvenlik modülü (HSM) kullanabilirsiniz. Daha fazla bilgi için bkz. HSM sağlayıcısının belgeleri.

### <a name="import-pfx-certificates"></a>PFX sertifikalarını içeri aktar

Aşağıdaki işlem, PFX sertifikalarının nasıl içeri aktarılacağını gösteren bir örnek olarak PowerShell cmdlet 'lerini kullanır. Gereksinimlerinize bağlı olarak farklı seçenekler seçebilirsiniz.

Seçeneklere şunlar dahildir:

- Amaçlanan amaç (bir etiketi temel alarak sertifikaları gruplandırır):
  - atanmadı
  - SMIME şifreleme
  - SMIME imzalama

- Doldurma şeması:
  - oaepSha256
  - oaepSha384
  - oaepSha512

Anahtarı oluşturmak için kullandığınız sağlayıcıyla eşleşen anahtar depolama sağlayıcısını seçin.

#### <a name="to-import-the-pfx-certificate"></a>PFX sertifikasını içeri aktarmak için  

1. Sağlayıcıdan alınan belgeleri izleyerek herhangi bir sertifika yetkilisinden (CA) sertifikaları dışarı aktarın.  Microsoft Active Directory Sertifika Hizmetleri için [Bu örnek komut dosyasını](https://gallery.technet.microsoft.com/Export-CMPfxCertificatesFro-d55f687b)kullanabilirsiniz.

2. Sunucusunda, *PowerShell* 'i yönetici olarak açın ve ardından PowerShell modülünü içeren *yayın* klasörüne gidin.

3. Modülünü içeri aktarmak için şunu çalıştırın`Import-Module .\IntunePfxImport.psd1`

4. Intune grafiğinde kimlik doğrulaması yapmak için şunu çalıştırın`Set-IntuneAuthenticationToken  -AdminUserName "<Admin-UPN>"`

   > [!NOTE]
   > Kimlik doğrulaması, grafiğe karşı çalıştırıldığı için, AppID için izinler sağlamalısınız. Bu yardımcı programı ilk kez kullandıysanız, *genel yönetici* gerekir. PowerShell cmdlet 'leri [PowerShell Intune örnekleri](https://github.com/microsoftgraph/powershell-intune-samples)ile birlikte kullanılan AppID 'yi kullanır.

5. İçeri aktardığınız her PFX dosyası için parolayı çalıştırarak güvenli bir dizeye dönüştürün `$SecureFilePassword = ConvertTo-SecureString -String "<PFXPassword>" -AsPlainText -Force` .

6. **Userpfxsertifika** nesnesi oluşturmak için şunu çalıştırın`$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>"`

   Örneğin, `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "C:\temp\userA.pfx" $SecureFilePassword "userA@contoso.com" "Microsoft Software Key Storage Provider" "PFXEncryptionKey" "smimeEncryption"`

   > [!NOTE]
   > Sertifikayı bağlayıcının yüklü olduğu sunucudan başka bir sistemden içeri aktardığınızda, Use anahtar dosya yolunu içeren aşağıdaki komutu kullanmalıdır:`$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>" "<PaddingScheme>" "<File path to public key file>"`
   >
   > *VPN* , bir amaç olarak desteklenmez. 


7. **Userpfxsertifikası** nesnesini çalıştırarak Intune 'a aktarın`Import-IntuneUserPfxCertificate -CertificateList $userPFXObject`

8. Sertifikanın içeri aktarıldığını doğrulamak için şunu çalıştırın`Get-IntuneUserPfxCertificate -UserList "<UserUPN>"`

9.  AAD belirteci önbelleğinin kendi üzerinde süre sonu beklemeden temizlenmesi için en iyi uygulama olarak, şunu çalıştırın`Remove-IntuneAuthenticationToken`

Kullanılabilir diğer komutlar hakkında daha fazla bilgi için, [GitHub 'da, Pfxımport PowerShell projesinde](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell)bulunan Benioku dosyasına bakın.

## <a name="create-a-pkcs-imported-certificate-profile"></a>PKCS içeri aktarılmış sertifika profili oluşturma

Sertifikaları Intune’da içeri aktardıktan sonra bir **PKCS içeri aktarılmış sertifikası** profili oluşturun ve bu profili Azure Active Directory gruplarına atayın.

> [!NOTE]
> PKCS içeri aktarılan sertifika profilini oluşturduktan sonra, profildeki **Hedeflenen amaç** ve **anahtar depolama sağlayıcısı** (KSP) değerleri salt okunurdur ve düzenlenemez. Bu ayarlardan herhangi biri için farklı bir değere ihtiyacınız varsa yeni bir profil oluşturun ve dağıtın. 

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. Seçin ve **cihazlar**  >  **yapılandırma profilleri**  >  **Profil oluştur**' a gidin.

3. Aşağıdaki özellikleri girin:
   - **Platform**: cihazlarınızın platformunu seçin.
   - **Profil**: **PKCS içeri aktarılan sertifikası** seçin

4. **Oluştur**’u seçin.

5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:
   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı, *tüm şirket Için PKCS içeri aktarılmış sertifika profilidir*.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda, aşağıdaki özellikleri girin:

   - **Amaçlanan amaç**: Bu profil için içeri aktarılan sertifikaların amaçlanan amacını belirtin. Yöneticiler, sertifikaları farklı amaçlanan amaçlarla (S/MIME imzalama veya S/MIME Şifrelemesi gibi) içeri aktarabilir. Sertifika profilinde seçilen kullanım amacı, sertifika profilini doğru içeri aktarılmış sertifikalarla eşleştirir. Amaçlanan amaç, içeri aktarılan sertifikaları gruplamak için bir etikettir ve bu etiketle içeri aktarılan sertifikaların amaçlanan amacı karşıladığını garanti etmez.  

   <!-- Not in new UI:
   - **Certificate validity period**: Unless the validity period was changed in the certificate template, this option defaults to one year.
   -->
   - **Anahtar depolama sağlayıcısı (KSP)**: Windows için, cihazdaki anahtarları nereye depolayacağınızı seçin.

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

   **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

    **İleri**’yi seçin.

11. (*Yalnızca Windows 10 Için geçerlidir*) **Uygulanabilirlik kuralları**' nda, bu profilin atanmasını iyileştirmek için uygulanabilirlik kurallarını belirtin. Profili, bir cihazın işletim sistemi sürümüne veya sürümüne göre atamayı veya atamayı seçebilirsiniz.

    Daha fazla bilgi için *Microsoft Intune bir cihaz profili oluşturma*içindeki [uygulanabilirlik kuralları](../configuration/device-profile-create.md#applicability-rules) bölümüne bakın.

    **İleri**’yi seçin.

12. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. Oluştur ' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="support-for-third-party-partners"></a>Üçüncü taraf iş ortakları için destek

Aşağıdaki iş ortakları, PFX sertifikalarını Intune 'a aktarmak için kullanabileceğiniz desteklenen yöntemleri veya araçları sağlar.

### <a name="digicert"></a>DigiCert

DigiCert PKI platform hizmetini kullanıyorsanız, PFX sertifikalarını Intune 'a aktarmak için, **Intune S/MIME sertifikaları Için DigiCert Içeri aktarma aracını** kullanabilirsiniz. Bu aracın kullanımı, bu makalenin önceki kısımlarında açıklandığı şekilde [PFX sertifikalarını Intune 'A aktarma](#import-pfx-certificates-to-intune) bölümündeki yönergeleri izlemeye yönelik gereksinimi değiştirir.

Aracının nasıl edinileceği dahil olmak üzere DigiCert Içeri aktarma aracı hakkında daha fazla bilgi için bkz https://knowledge.digicert.com/tutorials/microsoft-intune.html . DigiCert Bilgi Bankası 'nda.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulur ancak henüz herhangi bir işlem gerçekleştirmez. Yeni cihaz profilini [atayın](../configuration/device-profile-assign.md) .
