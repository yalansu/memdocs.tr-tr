---
title: Microsoft Intune - Azure’da sertifika profilleri oluşturma | Microsoft Docs
description: Microsoft Intune ile Basit Sertifika Kayıt Protokolü (SCEP) veya ortak anahtar şifreleme standartları (PKCS) sertifikaları ve sertifika profillerini kullanma hakkında bilgi edinin.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1db36b0ea3d2ba691811958a01043a606b4681a
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251981"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>Microsoft Intune kimlik doğrulaması için sertifikaları kullanma

VPN, Wi-Fi veya e-posta profilleri aracılığıyla kullanıcılarınızın uygulamalar ve Şirket kaynakları için kimlik doğrulaması yapmak üzere Intune ile sertifikaları kullanın. Bu bağlantıların kimliğini doğrulamak için sertifikaları kullandığınızda, son kullanıcılarınızın erişimleri sorunsuz hale getirmek için Kullanıcı adları ve parolalar girmesi gerekmez. Sertifikalar Ayrıca, S/MIME kullanarak e-posta imzalama ve şifreleme için de kullanılır.

## <a name="intune-supported-certificates-and-usage"></a>Intune tarafından desteklenen sertifikalar ve kullanım

| Tür              | Kimlik Doğrulaması | S/MIME Imzalama | S/MIME şifrelemesi  |
|--|--|--|--|
| Ortak anahtar şifreleme standartları (PKCS) içeri aktarılan sertifika |  | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png)|
| PKCS#12 (veya PFX)    | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) |  |
| Basit Sertifika Kayıt Protokolü (SCEP)  | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) | |

Bu sertifikaları dağıtmak için cihazlara sertifika profilleri oluşturup atayacaksınız.

Oluşturduğunuz her ayrı sertifika profili tek bir platformu destekler. Örneğin, PKCS sertifikaları kullanıyorsanız, Android için PKCS sertifika profili ve iOS/ıpados için ayrı bir PKCS sertifika profili oluşturacaksınız. Bu iki platform için SCEP sertifikaları da kullanıyorsanız, Android için bir SCEP sertifika profili ve iOS/ıpados için bir tane oluşturun.

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>Bir Microsoft sertifika yetkilisi kullanırken Genel hususlar

Bir Microsoft sertifika yetkilisi (CA) kullandığınızda:

- SCEP sertifika profillerini kullanmak için, Intune ile kullanmak üzere [bir ağ cihazı kayıt hizmeti (NDES) sunucusu ayarlamanız](certificates-scep-configure.md#set-up-ndes) gerekir.
- Aşağıdaki sertifika profili türlerini kullanmak için [Microsoft Intune sertifika Bağlayıcısı yüklemelisiniz](certificates-scep-configure.md#install-the-intune-certificate-connector):
  - SCEP sertifika profili
  - PKCS sertifika profili

- PKCS içeri aktarılan sertifikalarını kullanmak için:
  - [Microsoft Intune IÇIN PFX Sertifika bağlayıcısını yükler](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune).
  - Sertifikaları sertifika yetkilisinden dışarı aktarın ve ardından Microsoft Intune içeri aktarın. Bkz. [Pfxımport PowerShell projesi](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

- Aşağıdaki mekanizmaları kullanarak sertifikaları dağıtın:
  - Kök veya ara (veren) CA 'dan cihazlara güvenilen kök CA sertifikası dağıtmaya yönelik [Güvenilen sertifika profilleri](certificates-configure.md#create-trusted-certificate-profiles)
  - SCEP sertifika profilleri
  - PKCS sertifika profilleri
  - PKCS içeri aktarılan sertifika profilleri

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>Üçüncü taraf sertifika yetkilisini kullanırken Genel hususlar

Üçüncü taraf (Microsoft dışı) sertifika yetkilisi (CA) kullandığınızda:

- SCEP sertifika profillerini kullanmak için:
  - [Desteklenen iş ortaklarımızın birinden bir](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners)üçüncü taraf CA ile tümleştirmeyi ayarlayın. Kurulumu, üçüncü taraf CA 'dan gelen ve Intune ile CA tümleştirmesini tamamlamaya yönelik yönergeleri izleyerek içerir.
  - [Azure AD 'de,](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration) SCEP sertifikası sınama doğrulaması yapmak için Intune 'a haklar veren bir uygulama oluşturun.

- PKCS içeri aktarılan Sertifikalar [, Microsoft Intune IÇIN PFX Sertifika bağlayıcısını yüklemenizi](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune)gerektirir.

- Aşağıdaki mekanizmaları kullanarak sertifikaları dağıtın:
  - Kök veya ara (veren) CA 'dan cihazlara güvenilen kök CA sertifikası dağıtmaya yönelik [Güvenilen sertifika profilleri](certificates-configure.md#create-trusted-certificate-profiles)
  - SCEP sertifika profilleri
  - PKCS sertifika profilleri *(yalnızca [DigiCert PKI platformunda](certificates-digicert-configure.md)desteklenir)*
  - PKCS içeri aktarılan sertifika profilleri

## <a name="supported-platforms-and-certificate-profiles"></a>Desteklenen platformlar ve sertifika profilleri

| Platform              | Güvenilen sertifika profili | PKCS sertifika profili | SCEP sertifika profili | PKCS içeri aktarılan sertifika profili  |
|--|--|--|--|---|
| Android cihaz yöneticisi | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png)|  ![Desteklenir](./media/certificates-configure/green-check.png) |
| Android Kurumsal <br> -Tam olarak yönetilen (cihaz sahibi)   | ![Desteklenir](./media/certificates-configure/green-check.png) |   | ![Desteklenir](./media/certificates-configure/green-check.png) |  ![Desteklenir](./media/certificates-configure/green-check.png)  |
| Android Kurumsal <br> -Adanmış (cihaz sahibi)   | ![Desteklenir](./media/certificates-configure/green-check.png)  | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png)  | ![Desteklenir](./media/certificates-configure/green-check.png)|
| Android Kurumsal <br> -Şirkete ait Iş profili   | ![Desteklenir](./media/certificates-configure/green-check.png)  |  | ![Desteklenir](./media/certificates-configure/green-check.png)  | ![Desteklenir](./media/certificates-configure/green-check.png)  |
| Android Kurumsal <br> -İş profili    | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) |
| macOS                 | ![Desteklenir](./media/certificates-configure/green-check.png) |  ![Desteklenir](./media/certificates-configure/green-check.png) |![Desteklenir](./media/certificates-configure/green-check.png)|![Desteklenir](./media/certificates-configure/green-check.png)|
| Windows 8.1 ve üzeri |![Desteklenir](./media/certificates-configure/green-check.png)  |  |![Desteklenir](./media/certificates-configure/green-check.png) |   |
| Windows 10 ve üzeri  | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) | ![Desteklenir](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>Güvenilen kök CA sertifikasını dışarı aktarma

PKCS, SCEP ve PKCS içeri aktarılan sertifikaları kullanmak için cihazların kök sertifika yetkilinizle güvenmesi gerekir. Güven oluşturmak için, güvenilen kök CA sertifikasını ve tüm ara veya sertifika verme yetkilisi sertifikalarını ortak bir sertifika (. cer) olarak dışarı aktarın. Bu sertifikaları, veren CA 'dan veya veren CA 'nıza güvenen herhangi bir cihazdan alabilirsiniz.

Sertifikayı dışarı aktarmak için, sertifika yetkilinizin belgelerine bakın. Ortak sertifikayı bir. cer dosyası olarak dışarı aktarmanız gerekir.  Bir. pfx dosyası olan özel anahtarı dışarı aktarmayın.

Bu. cer dosyasını, bu sertifikayı cihazlarınıza dağıtmak için [Güvenilen sertifika profilleri oluştururken](#create-trusted-certificate-profiles) kullanacaksınız.

## <a name="create-trusted-certificate-profiles"></a>Güvenilen sertifika profilleri oluşturma

Bir SCEP, PKCS veya PKCS içeri aktarılan sertifika profili oluşturmadan önce güvenilen bir sertifika profili oluşturun ve dağıtın. Güvenilen bir sertifika profilini diğer sertifika profili türlerini alan gruplara dağıtmak, her cihazın CA 'nızın yasallığını tanımasını sağlar. Buna VPN, Wi-Fi ve e-posta gibi profiller dahildir.

SCEP sertifika profilleri doğrudan bir güvenilen sertifika profiline başvurur. PKCS sertifika profilleri, güvenilen sertifika profiline doğrudan başvurmazlar, ancak CA 'nizi barındıran sunucuya doğrudan başvurur. PKCS içeri aktarılan sertifika profilleri güvenilen sertifika profiline doğrudan başvurmazlar, ancak bunu cihazda kullanabilir. Güvenilen bir sertifika profilinin cihazlara dağıtımı, bu güvenin kurulabilmesini sağlar. Bir cihaz kök CA 'ya güvenmezse, SCEP veya PKCS sertifika profili ilkesi başarısız olur.

Desteklemek istediğiniz her cihaz platformu için, SCEP, PKCS ve PKCS içeri aktarılan sertifika profillerinde yaptığınız gibi ayrı bir güvenilen sertifika profili oluşturun.

> [!IMPORTANT]
> Platform *Windows 10 ve üzeri*için oluşturduğunuz güvenilen kök profiller, Microsoft Endpoint Manager Yönetim merkezinde Platform *Windows 8.1 ve üzeri*için profiller olarak görüntülenir. 
>
> Bu, güvenilen sertifika profilleri için platform sunumuyla ilgili bilinen bir sorundur. Profil bir Windows 8.1 platformunu ve daha sonrasını görüntülediğinde, Windows 10 ve üzeri sürümlerde çalışır.

> [!NOTE]
> Intune 'daki *Güvenilen sertifika* profili yalnızca kök ya da ara sertifikaları sağlamak için kullanılabilir. Bu tür sertifikaları dağıtmanın amacı, bir güven zinciri sağlamaktır. Kök veya ara sertifikalar dışında sertifikalar sağlamak için güvenilen sertifika profili kullanmak Microsoft tarafından desteklenmez. Intune portalında güvenilen sertifika profilini seçerken kök veya ara sertifika olarak kabul edilen sertifikaları içeri aktarma işlemi engellenmiş olabilir. Bu profil türünü kullanan bir kök veya ara sertifika olmayan bir sertifikayı içeri aktarıp dağıtabseniz bile, iOS ve Android gibi farklı platformlar arasında beklenmedik sonuçlarla karşılaşacaksınız.

### <a name="to-create-a-trusted-certificate-profile"></a>Güvenilen bir sertifika profili oluşturmak için

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. Seçin ve **cihazlar**  >  **yapılandırma profilleri**  >  **Profil oluştur**' a gidin.

   ![Intune 'a gidin ve güvenilen bir sertifika için yeni bir profil oluşturun](./media/certificates-configure/certificates-configure-profile-new.png)

3. Aşağıdaki özellikleri girin:
   - **Platform**: Bu profili alacak cihazların platformunu seçin.
   - **Profil**: **Güvenilen sertifika** seçin
  
4. **Oluştur**’u seçin.

5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:
   - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı *şirketin tamamına yönelik güvenilen sertifika profilidir*.
   - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda, önceden verdiğiniz GÜVENILEN kök CA sertifikası için. cer dosyasını belirtin. 

   Yalnızca Windows 8.1 ve Windows 10 cihazları için, güvenilen sertifika için **Hedef Depo** olarak şunlardan birini seçin:

   - **Bilgisayar sertifika deposu - Kök**
   - **Bilgisayar sertifika deposu-ara**
   - **Kullanıcı sertifika deposu - Ara**

   ![Bir profili oluşturun ve güvenilen bir sertifika yükleyin](./media/certificates-configure/certificates-configure-profile-fill.png)

8. **İleri**’yi seçin.

9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

   **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](../configuration/device-profile-assign.md).

    **İleri**’yi seçin.

11. (*Yalnızca Windows 10 Için geçerlidir*) **Uygulanabilirlik kuralları**' nda, bu profilin atanmasını iyileştirmek için uygulanabilirlik kurallarını belirtin. Profili, bir cihazın işletim sistemi sürümüne veya sürümüne göre atamayı veya atamayı seçebilirsiniz.

  Daha fazla bilgi için *Microsoft Intune bir cihaz profili oluşturma*içindeki [uygulanabilirlik kuralları](../configuration/device-profile-create.md#applicability-rules) bölümüne bakın.

12. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. Oluştur ' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="additional-resources"></a>Ek kaynaklar

- [Cihaz profillerini atama](../configuration/device-profile-assign.md)  
- [E-postaları imzalamak ve şifrelemek için S/MIME kullanma](certificates-s-mime-encryption-sign.md)  
- [Üçüncü taraf sertifika yetkilisini kullanma](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>Sonraki adımlar

Kullanmak istediğiniz her platform için SCEP, PKCS veya PKCS içeri aktarılmış sertifika profilleri oluşturun. Devam etmek için aşağıdaki makalelere bakın:

- [Intune ile SCEP sertifikalarını destekleyecek altyapıyı yapılandırma](certificates-scep-configure.md)  
- [Intune ile PKCS sertifikalarını yapılandırma ve yönetme](certficates-pfx-configure.md)  
- [PKCS içeri aktarılmış sertifika profili oluşturma](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
