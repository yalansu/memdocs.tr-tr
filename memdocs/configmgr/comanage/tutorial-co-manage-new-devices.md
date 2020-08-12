---
title: Eğitim&#58; Internet cihazları için ortak yönetimi etkinleştirme
titleSuffix: Configuration Manager
description: Configuration Manager ve Microsoft Intune yeni Internet tabanlı Windows 10 cihazları için ortak yönetimi nasıl yapılandıracağınızı öğrenin.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 0d7122942fe6a1455518b56159b48a11a2519d3e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127333"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Öğretici: yeni internet tabanlı cihazlar için ortak yönetimi etkinleştirme

Ortak yönetim sayesinde, kuruluşunuzdaki bilgisayarları yönetmek için Configuration Manager kullanmaya yönelik iyi bir işlem yapabilirsiniz. Aynı zamanda, güvenlik ve modern sağlama için Intune 'U kullanarak buluta yatırım yapmanız gerekir.

Bu öğreticide, Windows 10 cihazlarının hem Azure Active Directory (AD) hem de şirket içi AD kullandığınız ancak [karma Azure Active Directory](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (ad) bulunmayan bir ortamda ortak yönetimini ayarlarsınız. Configuration Manager ortamı, site sunucusu aynı sunucuda bulunan tüm site sistem rollerine sahip tek bir birincil site içerir. Bu öğretici, Windows 10 cihazlarınızın Intune 'a zaten kayıtlı olduğu şirket içinde başlar. 

Şirket içi AD 'nizi Azure AD ile birleştiren bir karma Azure AD 'niz varsa, yardımcı Öğreticimizi izleyerek [Configuration Manager istemcileri için ortak yönetimi etkinleştirmenizi](tutorial-co-manage-clients.md)öneririz.

Şu durumlarda bu öğreticiyi kullanın:
  
- Ortak yönetime getirmek için Windows 10 cihazlarınızın olması gerekir. Bu cihazlar Windows Autopilot aracılığıyla sağlanmış olabilir veya doğrudan donanım OEM 'ınızdan sağlanabilir.
- Internet üzerinde, Configuration Manager istemcisini eklemek istediğiniz Intune ile yönettiğiniz Windows 10 cihazlarınızın olması gerekir.

**Bu öğreticide şunları yapmanız gerekir:**  
> [!div class="checklist"]  
> * Azure ve şirket içi ortamınız için önkoşulları gözden geçirin
> * Bulut yönetimi ağ geçidi (CMG) için genel SSL sertifikası isteme
> * Configuration Manager 'de Azure hizmetlerini etkinleştirme
> * Bulut yönetimi ağ geçidi dağıtma ve yapılandırma  
> * Yönetim noktasını ve istemcileri CMG 'yi kullanacak şekilde yapılandırma
> * Configuration Manager içinde ortak yönetimi etkinleştirme
> * Intune 'U Configuration Manager istemcisini yükleyecek şekilde yapılandırma

## <a name="prerequisites"></a>Ön koşullar  

### <a name="azure-services-and-environment"></a>Azure hizmetleri ve ortamı

- Azure aboneliği ([ücretsiz deneme](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune aboneliği
  > [!TIP]  
  > Enterprise Mobility and Security (EMS) aboneliği hem Azure Active Directory Premium hem de Microsoft Intune içerir. EMS aboneliği ([ücretsiz deneme](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- Intune, [cihazları otomatik kaydetmek](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune) üzere yapılandırılmıştır  

> [!TIP]
> Artık kullanıcılarınıza tek tek Intune veya EMS lisansı satın almanız ve atamanız gerekmez. Daha fazla bilgi için bkz. [ürün ve lisanslama hakkında SSS](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Şirket içi altyapı

- Geçerli dalı, sürüm 1810 veya üstünü Configuration Manager.
  
  Sürüm 1810, daha karmaşık PKI gereksinimlerine engel olmak için bu öğreticide kullanılan [GELIŞMIŞ http](../core/plan-design/hierarchy/enhanced-http.md)'yi tanıtır. Gelişmiş HTTP kullanımı sayesinde, istemcileri yönetmek için kullandığınız birincil site, HTTP site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanacak şekilde yapılandırılmalıdır.  

  Sürüm 1810 Ayrıca Configuration Manager istemcisinin Internet tabanlı yüklemesi için daha basit bir komut satırı sunar.

- MDM yetkilisi, Intune olarak ayarlanmalıdır  

### <a name="external-certificates"></a>Dış Sertifikalar

- CMG sunucusu kimlik doğrulama sertifikası. Bu sertifika, genel ve genel olarak güvenilen bir sertifika sağlayıcısından gelen bir SSL sertifikasıdır. Örneğin, DigiCert, Thawte veya VeriSign ile sınırlı değildir. Bu sertifikayı olarak dışarı aktaracaksınız. Özel anahtara sahip PFX dosyası.  

- Bu öğreticide daha sonra bu sertifika için isteğin nasıl yapılandırılacağı hakkında rehberlik sağlıyoruz.

### <a name="permissions"></a>İzinler

Bu öğreticide, görevleri gerçekleştirmek için aşağıdaki izinleri kullanın:

- Azure Active Directory için *genel yönetici* olan bir hesap (Azure AD)
- Şirket içi altyapınızda *etki alanı yöneticisi* olan bir hesap  
- Configuration Manager içindeki *Tüm* kapsamlar için *tam yönetici* olan bir hesap

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi için genel bir sertifika isteme

Cihazlarınız Internet üzerinde olduğunda, ortak yönetim Configuration Manager bulut yönetim ağ geçidi (CMG) gerektirir. CMG, Internet tabanlı Windows 10 cihazlarınızın şirket içi Configuration Manager dağıtımıyla iletişim kurmasını sağlar. Cihazlar ve Configuration Manager ortamınız arasında bir güven oluşturmak için CMG bir SSL sertifikası gerektirir.

Bu öğreticide, genel olarak güvenilen bir sertifika sağlayıcısından yetki türeten **CMG sunucu kimlik doğrulama sertifikası** adlı bir genel sertifika kullanılmaktadır. Şirket içi Microsoft Sertifika yetkilinizden yetkili türeten sertifikaları kullanarak ortak yönetimi yapılandırmak mümkün olsa da, otomatik olarak imzalanan sertifikaların kullanılması Bu öğreticinin kapsamı dışındadır.

**CMG sunucusu kimlik doğrulama sertifikası** , Configuration Manager istemcisiyle CMG arasındaki iletişim trafiğini şifrelemek için kullanılır. Sertifika, sunucunun kimliğini istemciye doğrulamak için güvenilir bir köke geri izler. Ortak sertifika, Windows istemcilerinin zaten güvendiği bir güvenilen kök içerir.

Bu sertifika hakkında: 

- Azure 'da CMG hizmetiniz için benzersiz bir ad tanımlayabilir ve ardından bu adı Sertifika isteğiniz içinde belirtirsiniz.  
- Sertifika isteğinizi belirli bir sunucuda oluşturur ve sonra gerekli SSL sertifikasını almak için isteği bir ortak sertifika sağlayıcısına gönderebilirsiniz.  
- Sağlayıcıdan geri aldığınız sertifikayı isteği oluşturan sisteme içeri aktarırsınız. Daha sonra CMG 'yi Azure 'a dağıtırken kullanmak üzere sertifikayı dışarı aktarmak için aynı bilgisayarı kullanırsınız.  
- CMG 'nin yüklemesi sırasında, sertifikada belirttiğiniz adı kullanarak Azure 'da bir CMG hizmeti oluşturur.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Azure 'da bulut yönetimi ağ geçidiniz için benzersiz bir ad belirler

CMG sunucusu kimlik doğrulama sertifikasını istediğinizde, Azure 'da *bulut hizmetinizi (klasik)* tanımlamak için benzersiz bir ad olması gerektiğini belirtirsiniz. Varsayılan olarak, Azure genel bulutu *cloudapp.net*kullanır ve cmg, cloudapp.net etki alanı içinde * \<YourUniqueDnsName> . cloudapp.net*olarak barındırılır.  

> [!TIP]  
> Bu öğreticide, **CMG sunucusu kimlik doğrulama sertifikası** *contoso.com*ile biten bir FQDN kullanır.  CMG 'yi oluşturduktan sonra, kuruluşunuzun ortak DNS 'si içinde kurallı bir ad kaydı (CNAME) yapılandıracağız. Bu kayıt, CMG için ortak sertifikada kullandığımız adla eşleşen bir diğer ad oluşturur.  

Genel sertifikanızı girmeden önce, kullanmak istediğiniz adı Azure 'da bulabilirsiniz. Hizmeti doğrudan Azure 'da oluşturmazsınız. Bunun yerine, isteğiniz ortak sertifikada belirtilen ad, CMG 'yi yüklerken bulut hizmetini oluşturmak için Configuration Manager tarafından kullanılır.  

1. [Microsoft Azure portalda](https://portal.azure.com/) oturum açın.  

2. **Kaynak oluştur**' u seçin, **işlem** kategorisini seçin ve ardından **bulut hizmeti**' ni seçin. Bulut hizmeti (klasik) sayfası açılır.

3. **DNS adı**için, kullanacağınız bulut hizmeti için önek adını belirtin. Bu ön ek, CMG sunucusu kimlik doğrulama sertifikası için bir yayımlama sertifikası istediğinizde, daha sonra kullandığınız ile aynı olmalıdır. *MyCSG.cloudapp.net*ad alanını oluşturan *mycsg*kullanırız. Arabirim, adın kullanılabilir veya başka bir hizmet tarafından zaten kullanımda olduğunu onaylar.  
 Kullanmak istediğiniz adı doğruladıktan sonra, sertifika Imzalama Isteği 'ni (CSR) göndermeye hazır olursunuz.

### <a name="request-the-certificate"></a>Sertifikayı iste

Bir ortak sertifika sağlayıcısına CMG 'niz için bir sertifika imzalama isteği göndermek üzere aşağıdaki bilgileri kullanın. Aşağıdaki değerleri ortamınıza uygun olacak şekilde değiştirin.  

- Bulut yönetimi ağ geçidinin hizmet adını belirlemek için *Mycmg*
- Şirket adı olarak *contoso*
- Genel etki alanı olarak *contoso.com*

Sertifika imzalama isteklerini (CSR) oluşturmak için birincil site sunucunuzu kullanmanızı öneririz. Sertifikayı aldığınızda, bunu CSR 'yi oluşturan sunucuya kaydetmeniz veya sertifika özel anahtarını dışarı aktarmanız gerekir, bu da gereklidir.  

Bir CSR oluşturduğunuzda sürüm 2 anahtar sağlayıcısı türü isteyin. Yalnızca sürüm 2 sertifikaları desteklenir.  

> [!TIP]  
> CMG 'yi dağıtırken aynı anda bir bulut dağıtım noktası (CDP) de yükleyeceğiz. Varsayılan olarak, bir CMG dağıttığınızda, **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin ver ve Azure Storage 'dan içerik** sunma seçeneği seçilidir. Sunucu üzerindeki CDP 'yi CMG ile birlikte bulmak, CDP 'yi desteklemeye yönelik ayrı sertifikalara ve yapılandırmalara gereksinimi ortadan kaldırır. CDP ortak yönetimi kullanmak için gerekli olmamasına rağmen, çoğu ortamda faydalıdır.  
>
> Ek, ayrı bir CDPs kullanıyorsanız, her ek CDP için ayrı sertifikalar istemeniz gerekir. Bir CDP için ortak bir sertifika istemek üzere, bulut yönetimi ağ geçidi CSR 'si için aynı ayrıntıları kullanın. Yalnızca ortak adı, her CDP için benzersiz olacak şekilde değiştirmeniz gerekir.
>
> Ek, ayrı bir CDP kullanılması kullanım dışıdır ve artık önerilmez. Daha fazla bilgi için bkz. [kullanımdan kaldırılan özellikler](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).

#### <a name="details-for-the-cloud-management-gateway-csr"></a>Bulut yönetimi ağ geçidi CSR ayrıntıları

- **Ortak ad**: CloudServiceNameCMG.YourCompanyPubilcDomainName.com  
Örnek: MyCSG.contoso.com  
- **Konu diğer adı**: ortak ad (CN) ile aynı  
- **Kuruluş**: kuruluşunuzun adı  
- **Departman**: kuruluşunuza göre  
- **Şehir**: kuruluşunuza göre  
- **Durum**: kuruluşunuza göre  
- **Ülke**: kuruluşunuza göre  
- **Anahtar boyutu: 2048**  
- **Sağlayıcı: Microsoft RSA SChannel Şifreleme sağlayıcısı**  

### <a name="import-the-certificate"></a>Sertifikayı içeri aktar

Ortak sertifikayı aldıktan sonra, bunu CSR 'yi oluşturan bilgisayarın yerel sertifika deposuna aktarın. Ardından sertifikayı olarak dışarı aktarın. Azure 'da CMG 'niz için kullanabilmeniz için PFX dosyası.  

Ortak sertifika sağlayıcıları genellikle sertifikanın içeri aktarılması için yönergeler sağlar. Sertifikayı içeri aktarma işlemi aşağıdaki kılavuza benzer olmalıdır:  

1. Sertifikanın aktarılacağı bilgisayarda, Certificate. pfx dosyasını bulun.  

2. Dosyaya sağ tıklayın ve ardından **PFX 'ı yükler** ' i seçin.  

3. Sertifika Içeri aktarma Sihirbazı başladığında **İleri**' yi seçin.  

4. **Içeri aktarılacak dosya** sayfasında **İleri**' yi seçin.

5. **Parola** sayfasında, parola kutusuna özel anahtar için parola girin ve ardından **İleri**' yi seçin.  
  
   Anahtarı dışa aktarılabilir hale getirme seçeneğini belirleyin.

6. **Sertifika deposu sayfasında**, sertifika **türüne bağlı olarak sertifika deposunu otomatik olarak Seç**' i seçin ve ardından **İleri**' yi seçin.  

7. **Son**’u seçin.

### <a name="export-the-certificate"></a>Sertifikayı dışarı aktarma

*CMG sunucusu kimlik doğrulama sertifikasını* sunucusundan dışarı aktarın. Sertifikayı yeniden dışarı aktarmak, Azure 'daki bulut yönetimi ağ geçidiniz için kullanılabilir hale getirir.  

1. Ortak SSL sertifikasını içeri aktardığınız sunucuda, Sertifika Yöneticisi konsolunu açmak için **Certlm. msc** ' yi çalıştırın.  

2. Sertifika Yöneticisi konsolunda **kişisel > sertifikaları**' nı seçin. Ardından, önceki yordama kaydettiğiniz *CMG sunucusu kimlik doğrulama sertifikasına* sağ tıklayın ve ardından **dışarı aktar > tüm görevler**' i seçin.  

3. Sertifika dışarı aktarma sihirbazında, **İleri**' yi seçin, **Evet ' i seçin, özel anahtarı dışarı aktarın**ve ardından **İleri**' ye tıklayın.  

4. Dışarı aktarma dosyası biçimi sayfasında **kişisel bilgi değişimi-PKCS #12 (. PFX)**, **İleri**' yi seçin ve bir parola sağlayın. Dosya adı için **C:\configmgrcloudmgserver**gibi bir ad belirtin. Azure 'da CMG oluştururken bu dosyaya başvurabileceksiniz.  

5. **İleri**' yi seçin ve ardından dışarı aktarmayı tamamladıktan sonra **son** ' u seçmeden önce aşağıdaki ayarları onaylayın:  

   - Dışarı aktarma anahtarları = Evet  
   - Sertifika yolundaki tüm sertifikaları dahil et = Evet  
   - Dosya biçimi = kişisel bilgi değişimi (*. pfx)  

6. Dışarı aktarmayı tamamladıktan sonra,. pfx dosyasını bulun ve bu dosyanın bir kopyasını, internet tabanlı istemcileri yönetecek Configuration Manager birincil site sunucusuna **C:\Cert dizinine** yerleştirin. Sertifikalar klasörü, sertifikaları sunucular arasında taşırken kullanılacak geçici bir klasördür. Bulut yönetimi ağ geçidini Azure 'a dağıtırken, sertifika dosyasına birincil site sunucusundan erişirsiniz.  

Sertifikayı birincil site sunucusuna kopyaladıktan sonra, sertifikayı üye sunucudaki kişisel sertifika deposundan silebilirsiniz.

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Configuration Manager 'de Azure bulut hizmetleri 'ni etkinleştirme

Azure hizmetlerini Configuration Manager konsolundan yapılandırmak için, Azure hizmetlerini Yapılandırma Sihirbazı 'nı kullanın ve iki Azure Active Directory (Azure AD) uygulaması oluşturursunuz.  

- **Sunucu uygulaması** – Azure AD 'de bir *Web uygulaması*  
- **İstemci uygulaması** – Azure AD 'de *yerel bir istemci* uygulaması  

Birincil site sunucusundan aşağıdaki yordamı çalıştırın.  

1. Birincil site sunucusundan Configuration Manager konsolunu açın ve **yönetim > Cloud Services Azure hizmetleri >**' ne gidin ve **Azure hizmetlerini yapılandır**' ı seçin.  

   Azure hizmetini yapılandır sayfasında, yapılandırmakta olduğunuz bulut yönetimi hizmeti için bir kolay ad belirtin. Örneğin: *bulut yönetimi hizmetim*.

   Ardından **bulut yönetimi**' ni seçin ve ardından **İleri**' yi seçin.  

   > [!TIP]  
   > Sihirbazda yaptığınız yapılandırma hakkında daha fazla bilgi için bkz [. Azure Hizmetleri Sihirbazı 'Nı başlatma](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard)

2. **Uygulama özellikleri** sayfasında, **Web uygulaması**için, **sunucu uygulaması** iletişim kutusunu açmak üzere **Araştır** ' ı seçin ve ardından **Oluştur**' u seçin. Aşağıdaki alanları yapılandırın:

   - **Uygulama adı**: uygulama Için *bulut yönetimi Web uygulaması*gibi bir kolay ad belirtin.  

   - **Giriş sayfası URL 'si**: bu değer Configuration Manager tarafından kullanılmaz, ancak Azure AD için gereklidir. Varsayılan olarak, bu değer `https://ConfigMgrService` .  

   - **Uygulama kimliği URI 'si**: Bu DEĞERIN Azure AD kiracınızda benzersiz olması gerekir. Hizmete erişim istemek için Configuration Manager istemcisi tarafından kullanılan erişim belirtecidir. Varsayılan olarak, bu değer `https://ConfigMgrService` .  

   Sonra **oturum aç**' ı seçin ve bır Azure AD Genel yönetici hesabı belirtin. Bu kimlik bilgileri Configuration Manager tarafından kaydedilmez. Bu kişi, Configuration Manager izin gerektirmez ve Azure Hizmetleri Sihirbazı 'Nı çalıştıran hesap için aynı hesaba gerek kalmaz.

   Oturum açtıktan sonra sonuçlar görüntülenir. Sunucu uygulaması oluştur iletişim kutusunu kapatmak ve uygulama özellikleri sayfasına dönmek için **Tamam ' ı** seçin.

3. **Yerel istemci uygulaması**Için, **istemci uygulaması** Iletişim kutusunu açmak üzere **Araştır** ' ı seçin.

4. **Oluştur** ' u seçerek **istemci uygulaması oluştur** iletişim kutusunu açın ve aşağıdaki alanları yapılandırın:  

   - **Uygulama adı**: uygulama Için *bulut yönetimi yerel istemci uygulaması*gibi bir kolay ad belirtin.

   - **Yanıt URL 'si**: bu değer Configuration Manager tarafından kullanılmaz, ancak Azure AD tarafından gerekli değildir. Varsayılan olarak, bu değer `https://ConfigMgrClient` .
   Sonra **oturum aç**' ı seçin ve bır Azure AD Genel yönetici hesabı belirtin. Web uygulaması gibi, bu kimlik bilgileri kaydedilmez ve Configuration Manager izinler gerektirmez.

   Oturum açtıktan sonra sonuçlar görüntülenir. Istemci uygulaması oluştur iletişim kutusunu kapatmak ve uygulama özellikleri sayfasına dönmek için **Tamam ' ı** seçin. Sonra, devam etmek için **İleri** ' yi seçin.

5. **Bulma ayarlarını yapılandır** sayfasında, **Kullanıcı bulmayı Azure Active Directory etkinleştir**' i işaretleyin, **İleri**' yi seçin ve ardından ortamınız için bulma iletişim kutularının yapılandırmasını Tamam ' ı seçin.  

6. Özet, Ilerleme ve tamamlama sayfalarında ilerleyin ve ardından Sihirbazı kapatın.  

   Azure AD Kullanıcı keşfi için Azure hizmetleri artık Configuration Manager etkinleştirilmiştir.  Konsolunu şimdilik açık bırakın.  

7. Bir tarayıcı açın ve [Azure Portal](https://portal.azure.com/)oturum açın.  

8. **Tüm hizmetler > Azure Active Directory > uygulama kayıtları**seçin ve ardından:

   1. Oluşturduğunuz Web uygulamasını seçin.

   2. **API izinleri** ' ne gidin > **yönetici onayı ver** <your tenant> ' i seçin ve ardından **Evet**' i seçin.  

   3. Oluşturduğunuz yerel Istemci uygulamasını seçin.

   4. **API izinleri** ' ne gidin > **yönetici onayı ver** <your tenant> ' i seçin ve ardından **Evet**' i seçin.

9. Configuration Manager konsolunda, **yönetim > genel bakış > > Cloud Services Azure Hizmetleri ' ne**gidin ve Azure hizmetinizi seçin. Ardından **Azure Active Directory Kullanıcı bul** ' a sağ tıklayın ve **tam bulmayı Şimdi Çalıştır**' ı seçin. Eylemi onaylamak için **Evet** ' i seçin.  

10. Birincil site sunucusunda, bulma 'nın çalıştığını onaylamak için Configuration Manager **SMS_AZUREAD_DISCOVERY_AGENT. log** dosyasını açın ve aşağıdaki girdiyi arayın: *Azure Active Directory kullanıcılar Için udx başarıyla yayımlandı*  

    Günlük dosyası varsayılan olarak *% Program_Files% \ Microsoft Configuration Manager\Logs*konumundadır.  

## <a name="create-the-cloud-services-in-azure"></a>Azure 'da bulut hizmetleri oluşturma

**Öğreticinin bu bölümünde şunları yapmanız gerekir**:

- CMG bulut hizmetini oluşturma  
- Her iki hizmet için de DNS CNAME kayıtları oluştur  

### <a name="create-the-cmg"></a>CMG oluşturma

Azure 'da hizmet olarak bir bulut yönetimi ağ geçidi yüklemek için bu yordamı kullanın. CMG, hiyerarşinin üst katman sitesine yüklenir. Bu öğreticide, sertifikaların kaydedildiği ve verildiği birincil siteyi kullanmaya devam ediyoruz.

1. Birincil site sunucusunda Configuration Manager konsolunu açın ve ardından **yönetim > genel bakış > Cloud Services > bulut yönetimi ağ geçidi**' a gidin ve ardından **Oluştur bulut yönetimi ağ geçidi**' ı seçin.  

2. **Genel** sayfası üzerinde:  

   1. **Azure ortamı**için bulut ortamınızı seçin. Bu öğretici **AzurePublicCloud**kullanır.  

   2. **Azure Resource Manager dağıtım**seçin.  
  
   3. Azure aboneliğinizde **oturum açın** . Configuration Manager, Configuration Manager için Azure bulut hizmetleri 'ni etkinleştirdiğinizde yapılandırdığınız bilgilere göre ek bilgiler doldurur.  

   Devam etmek için **İleri** seçeneğini belirleyin.  

3. **Ayarlar** sayfasında, CMG sunucusu kimlik doğrulama sertifikasını içeri aktardıktan sonra, verdiğiniz dosya olan **Configmgrcloudmgserver. pfx**adlı dosyayı seçin. Parolayı belirttikten sonra,. pfx Sertifika dosyasındaki ayrıntılara göre **hizmet adı** ve **dağıtım adı** otomatik olarak doldurulur.

4. **Bölgenizi**ayarlayın.

5. **Kaynak grubu**için, var olan bir kaynak grubunu kullanın veya bir kolay ada sahip, **Cofigmgrcloudservices**gibi bir boşluk kullanmayan bir grup oluşturun. Bir grup oluşturmayı seçerseniz, Grup Azure 'da bir kaynak grubu olarak eklenir.  

6. Ölçekli yapılandırmaya hazırsanız, **sanal makine örneklerinin**sayısı için bir (1) kullanın. Sanal makine örneklerinin sayısı, tek bir Bulut Yönetimi Ağ Geçidi (CMG) bulut hizmetinin daha fazla istemci bağlantısını desteklemek üzere ölçeğini değiştirmesine izin verir. Daha sonra, kullandığınız VM örneği sayısını döndürmek ve düzenlemek için Configuration Manager konsolunu kullanabilirsiniz.  

7. **Istemci sertifikası Iptalini doğrula**onay kutusunu etkinleştirin.

8. **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin ver** onay kutusunu etkinleştirin ve CMG ile bir bulut dağıtım noktası dağıtmak istiyorsanız Azure Storage 'dan içerik sunar.

9. Devam etmek için **İleri** seçeneğini belirleyin.

10. **Uyarı** sayfasındaki değerleri gözden geçirin ve ardından **İleri**' yi seçin.

11. **Özet** sayfasını gözden geçirin ve **İleri** ' ye tıklayarak bulut yönetimi ağ geçidi bulut hizmetini oluşturun. Sihirbazı **kapatmak Için kapat** ' ı seçin.  

12. Configuration Manager konsolunun Bulut Yönetimi Ağ Geçidi düğümünde artık yeni hizmeti görüntüleyebilirsiniz.  

### <a name="create-dns-cname-records"></a>DNS CNAME kayıtları oluşturma

CMG için bir DNS girişi oluşturduğunuzda, şirket ağınızın içindeki ve dışındaki Windows 10 cihazlarınızı Azure 'da CMG bulut hizmetini bulmak için ad çözümlemesi kullanacak şekilde etkinleştirirsiniz.

CNAME kaydı örneğimiz aşağıdaki ayrıntıları kullanır:  

- Şirket adı, ***contoso.com***Genel DNS ad alanı ile **contoso** 'ya sahiptir.  

- CMG hizmet adı, Azure 'da ***MyCMG.cloudapp.net*** haline gelen **mycmg**' dir.  

CNAME kaydı örneği: *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Yönetim noktasını ve istemcileri CMG 'yi kullanacak şekilde yapılandırma

Şirket içi yönetim noktalarının ve istemcilerinin bulut yönetimi ağ geçidini kullanmasını sağlayan ayarları yapılandırın.

İstemci iletişimleri için gelişmiş HTTP 'yi kullandığımızda, HTTPS yönetim noktası kullanmanız gerekmez.  

### <a name="create-the-cmg-connection-point"></a>CMG bağlantı noktasını oluşturma

Siteyi gelişmiş HTTP 'yi destekleyecek şekilde yapılandırın.  

1. Configuration Manager konsolunda **yönetim > genel bakış > site yapılandırması > siteleri ' ne**gidin ve birincil sitenin özelliklerini açın.  

2. **Istemci bilgisayar iletişimi** SEKMESINDE, **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullan**için *https veya http* seçeneğini belirleyin ve ardından yapılandırmayı kaydetmek için **Tamam** ' ı seçin.

    > [!Note]
    > Sürüm 1906 ' den başlayarak bu sekmeye **Iletişim güvenliği**denir.<!-- SCCMDocs#1645 -->  

3. Artık **yönetim > genel bakış > site yapılandırması > sunucular ve site sistemi rolleri ' ne** gidin ve bulut yönetimi ağ geçidi bağlantı noktasını yüklemek istediğiniz yönetim noktası olan sunucuyu seçin.  

4. **Site sistemi rolleri ekle**' yi ve ardından **İleri**' yi seçin >  **Next**.  

5. **Bulut yönetimi ağ geçidi bağlantı noktasını** seçin ve ardından devam etmek için **İleri** ' yi seçin.  

6. **Bulut yönetimi ağ geçidi bağlantı noktası** sayfasındaki varsayılan seçimleri gözden geçirin ve doğru CMG 'nin seçili olduğundan emin olun. Birden çok bulut yönetimi ağ geçidine sahipseniz, farklı bir CMG belirtmek için açılan listeyi kullanabilirsiniz. Ayrıca, yükleme sırasında CMG 'yi de değiştirebilirsiniz. Devam etmek için **İleri** seçeneğini belirleyin.

7. Yüklemeyi başlatmak için **İleri** ' yi seçin ve ardından sonuçları tamamlama sayfasında görüntüleyin.  Bağlantı noktasının yüklenmesini gerçekleştirmek için **Kapat** ' ı seçin.

8. Artık **yönetim > genel bakış > site yapılandırması > sunucular ve site sistemi rolleri ' ne** gidin ve bağlantı noktasını yüklediğiniz yönetim noktasının **özelliklerini** açın. **Genel** sekmesinde, **bulut yönetimi ağ geçidi trafiğine izin ver Configuration Manager**onay kutusunu işaretleyin ve ardından yapılandırmayı kaydetmek için **Tamam** ' ı seçin.
   > [!TIP]  
   > Ortak yönetimin etkinleştirilmesi gerekmediği sürece, aynı düzenleme özelliğini tüm yazılım güncelleştirme noktaları için yapmanızı öneririz.

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>İstemcileri CMG 'yi kullanacak şekilde yönlendirmek için Istemci ayarlarını yapılandırma

Configuration Manager istemcilerini CMG ile iletişim kuracak şekilde yapılandırmak için Istemci ayarlarını kullanın.  

1. **Configuration Manager konsolunu > yönetim > genel bakış > Istemci ayarları**' nı açın ve ardından **varsayılan istemci ayarlarını**düzenleyin.  

2. **Cloud Services**seçin.

3. **Varsayılan ayarlar** sayfasında, aşağıdaki ayarları = **Evet**olarak ayarlayın.  

   - **Azure Active Directory ile yeni Windows 10 etki alanına katılmış cihazları otomatik olarak kaydet**  

   - **İstemcilerin bulut yönetimi ağ geçidi kullanmasını sağlama**

   - **Bulut dağıtım noktasına erişime izin ver**

4. **İstemci ilkesi** sayfasında, **İnternet istemcilerinden gelen Kullanıcı ilkesi isteklerini etkinleştir**  =  **Evet**olarak ayarlayın.

5. Bu yapılandırmayı kaydetmek için **Tamam**’ı seçin.

## <a name="enable-co-management-in-configuration-manager"></a>Configuration Manager içinde ortak yönetimi etkinleştirme

Azure yapılandırmalarının, site sistem rollerinin ve istemci ayarlarının yerinde, ortak yönetimi etkinleştirmek için Configuration Manager yapılandırabilirsiniz. Ancak, bu öğretici tamamlanmadan önce ortak yönetimi etkinleştirdikten sonra Intune 'da birkaç yapılandırma yapmanız gerekir. Bu görevlerden biri, Intune 'U Configuration Manager istemcisini dağıtmak üzere yapılandırmaktır. Bu görev, ortak yönetim Yapılandırma Sihirbazı içinden kullanılabilir olan istemci dağıtımı için komut satırı kaydederek daha kolay hale getirilir. Intune için yapılandırma tamamlamadan önce ortak yönetimi şimdi etkinleştirdik.

> [!TIP]
> - Ortak yönetimi etkinleştirdiğinizde, bir koleksiyonu *pilot grubu*olarak atayacaksınız. Bu, ortak yönetim yapılandırmalarınızı test etmek için az sayıda istemci içeren bir gruptur. Yordamı başlamadan önce uygun bir koleksiyon oluşturmanızı öneririz. Daha sonra bu koleksiyonu, bunu yapmak için yordamdan çıkmadan seçebilirsiniz.
> - Configuration Manager sürüm 1906 ' den başlayarak, her iş yükü için farklı bir *pilot grubu* atayabileceğinizden bu yana birden çok koleksiyona ihtiyacınız olabilir.

### <a name="enable-co-management-starting-in-version-1906"></a>Sürüm 1906 ' den başlayarak ortak yönetimi etkinleştirme

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Sürüm 1902 ve önceki sürümlerde ortak yönetimi etkinleştirme

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Configuration Manager istemcisini dağıtmak için Intune 'U kullanma

Configuration Manager istemcisini, şu anda yalnızca Intune ile yönetilen Windows 10 cihazlarına yüklemek için Intune 'u kullanabilirsiniz.  

Daha sonra, daha önce yönetilmeyen bir Windows 10 cihazı Intune 'a kaydolduktan sonra, Configuration Manager istemcisini otomatik olarak yüklenir.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Configuration Manager istemcisini yüklemek için bir Intune uygulaması oluşturma

1. Birincil site sunucusundan [Microsoft Endpoint Manager Yönetim Merkezi](https://endpoint.microsoft.com) ' nde oturum açın ve tüm **uygulamalar**  >  **All Apps**  >  **Ekle**' ye gidin.

2. Uygulama türü için, **diğer**bölümünde **iş kolu uygulaması** ' nı seçin.

3. **Uygulama paketi dosyası**için **ccmsetup.msi**Configuration Manager dosyanın konumuna gidin ve ardından **Aç > Tamam**' ı seçin.
Örneğin, *C:\Program Files\Microsoft yapılandırma Manager\bin\i386\ccmsetup.msi*

4. **Uygulama bilgileri**' ni seçin ve ardından aşağıdaki ayrıntıları belirtin:
   - **Açıklama**: Configuration Manager istemci  

   - **Yayımcı**: Microsoft  

   - **Komut satırı bağımsız değişkenleri**:*\<Specify the **CCMSETUPCMD** command line. You can use the command line you saved from the* Enablement *page of the Co-management Configuration Wizard. This command line includes the names of your cloud service and additional values that enable devices to install the Configuration Manager client software.>*  

     Komut satırı yapısı, yalnızca CCMSETUPCMD ve Smssitekodu parametreleri kullanılarak bu örneğe benzemelidir:  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > Komut satırı kullanılabilir değilse, komut satırının bir kopyasını almak için Configuration Manager konsolundaki *CoMgmtSettingsProd* özelliklerini görüntüleyebilirsiniz.

5. **Ekle > Tamam ' ı**seçin.  Uygulama oluşturulur ve Intune konsolunda kullanılabilir hale gelir. Uygulama kullanılabilir olduktan sonra, Intune 'U Windows 10 cihazlarına atamak üzere yapılandırmak için aşağıdaki bölümü kullanabilirsiniz.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Configuration Manager istemcisini yüklemek için Intune uygulamasını atama

Aşağıdaki yordam, önceki yordamda oluşturduğunuz Configuration Manager istemcisini yüklemek için uygulamayı dağıtır.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://endpoint.microsoft.com)oturum açın. **Uygulamalar**  >  **tüm uygulamalar** ' ı seçin ve ardından Configuration Manager istemcisini dağıtmak için oluşturduğunuz uygulamayı **ConfigMgr istemci kurulumu önyüklemesi**' ni seçin.  

2. **Özellikler** ' i seçin ve **atamalar**için **düzenleyin** . Ortak yönetime katılmasını istediğiniz kullanıcıların ve cihazların bulunduğu Azure Active Directory (AD) gruplarını ayarlamak için **gerekli** atamalar altında **Grup Ekle** ' yi seçin.  

3. **Gözden geçir + kaydet** ' i seçin ve ardından yapılandırmayı **kaydedin** .
Uygulama artık sizin atadığınız kullanıcılar ve cihazlar için gereklidir. Uygulama bir cihaza Configuration Manager istemcisini yükledikten sonra ortak yönetim tarafından yönetilir.

## <a name="summary"></a>Özet

Bu öğreticinin yapılandırma adımlarını tamamladıktan sonra, cihazlarınızı birlikte yönetmeye başlayabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

- Ortak [Yönetim Panosu](how-to-monitor.md) ile birlikte yönetilen cihazların durumunu gözden geçirme
- Yeni cihaz sağlamak için [Windows Autopilot](quickstart-autopilot.md) kullanma
- Şirket kaynaklarına Kullanıcı erişimini yönetmek için [koşullu erişim](quickstart-conditional-access.md) ve Intune Uyumluluk kurallarını kullanma
