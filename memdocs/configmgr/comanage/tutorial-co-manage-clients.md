---
title: Öğretici&#58; mevcut istemciler için ortak yönetimi etkinleştirme
titleSuffix: Configuration Manager
description: Windows 10 cihazlarını Configuration Manager ile yönettiğinizde, Microsoft Intune ile ortak yönetimi yapılandırın.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 918df2cded3fad48352fff6a2617b1133540c0eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712431"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Öğretici: mevcut Configuration Manager istemcileri için ortak yönetimi etkinleştirme

Ortak yönetim sayesinde, kuruluşunuzdaki bilgisayarları yönetmek için Configuration Manager kullanmaya yönelik iyi bir işlem yapabilirsiniz. Aynı zamanda, güvenlik ve modern sağlama için Intune 'U kullanarak buluta yatırım yapmanız gerekir.  

Bu öğreticide, zaten Configuration Manager kayıtlı olan Windows 10 cihazlarınızın ortak yönetimini ayarlarsınız. Bu öğretici, Windows 10 cihazlarınızı yönetmek için Configuration Manager zaten kullandığınız şirket içi ile başlar.

Şu durumlarda bu öğreticiyi kullanın:  

- Karma bir Azure AD yapılandırmasında Azure Active Directory (Azure AD) ile bağlantı kurmak için kullanabileceğiniz bir şirket içi Active Directory vardır.

  Şirket içi AD 'nizi Azure AD ile birleştiren bir karma Azure Active Directory (AD) dağıtabiyorsanız, [Yeni internet tabanlı Windows 10 cihazları için ortak yönetimi etkinleştirmek üzere](tutorial-co-manage-new-devices.md)yardımcı Öğreticimizi takip etmenizi öneririz.
- Bulutta iliştirmek istediğiniz Configuration Manager istemcileriniz var.

**Bu öğreticide şunları yapmanız gerekir:**  
> [!div class="checklist"]
> * Azure ve şirket içi ortamınız için önkoşulları gözden geçirin
> * Hibrit Azure AD’yi ayarlama  
> * Configuration Manager istemci aracılarını Azure AD 'ye kaydetmek üzere yapılandırma  
> * Intune 'U cihazları otomatik kaydedecek şekilde yapılandırma  
> * Configuration Manager içinde ortak yönetimi etkinleştirme  

## <a name="prerequisites"></a>Önkoşullar  

### <a name="azure-services-and-environment"></a>Azure hizmetleri ve ortamı

- Azure aboneliği ([ücretsiz deneme](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune aboneliği
  > [!TIP]  
  > Enterprise Mobility + Security (EMS) aboneliği hem Azure Active Directory Premium hem de Microsoft Intune içerir. EMS aboneliği ([ücretsiz deneme](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Ortamınızda henüz yoksa, bu öğreticide şunları yapmanız gerekir:

- Şirket içi Active Directory ve Azure Active Directory (AD) kiracınız arasında [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) yapılandırın.

> [!TIP]
> Artık kullanıcılarınıza tek tek Intune veya EMS lisansı satın almanız ve atamanız gerekmez. Daha fazla bilgi için bkz. [ürün ve lisanslama hakkında SSS](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Şirket içi altyapı

- Configuration Manager geçerli dalının [desteklenen bir sürümü](../core/servers/manage/updates.md#supported-versions)
- Mobil cihaz yönetimi (MDM) yetkilisi, Intune olarak ayarlanmalıdır.  

### <a name="permissions"></a>İzinler

Bu öğreticide, görevleri gerçekleştirmek için aşağıdaki izinleri kullanın:

- Azure Active Directory *genel yönetici* olan bir hesap (Azure AD) 
- Şirket içi altyapınızda *etki alanı yöneticisi* olan bir hesap  
- Configuration Manager içindeki *Tüm* kapsamlar için *tam yönetici* olan bir hesap

## <a name="set-up-hybrid-azure-ad"></a>Hibrit Azure AD’yi ayarlama

Hibrit bir Azure AD ayarladığınızda, Azure AD Connect ve Active Directory Federasyon Hizmetleri (ADFS) kullanarak Azure AD ile şirket içi AD tümleştirmesini son derece ayarlamakta olursunuz. Başarılı yapılandırma sayesinde, çalışanlarınız şirket içi AD kimlik bilgilerini kullanarak dış sistemlerde sorunsuzca oturum açabilir.

> [!IMPORTANT]  
> Bu öğreticide, yönetilen bir etki alanı için karma Azure AD ayarlama ile ilgili bir işlem ayrıntılı bir şekilde yapılır. Hibrit Azure AD 'yi anlama ve dağıtma kılavuzunuz olarak Bu öğreticiye yönelik bilgi sahibi olmanız önerilir.
>
> Hibrit Azure AD hakkında daha fazla bilgi için Azure Active Directory belgelerinde aşağıdaki makalelerle başlayın:
>
> - [Azure AD katılımınızı uygulamayı planlama](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> - [Hibrit Azure AD katılımınızı uygulamayı planlama](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Cihazlarınızın hibrit Azure AD katılımını denetleme](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Federasyon etki alanları için hibrit Azure AD katılımını yapılandırma](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Azure AD Connect ayarlama

Hibrit Azure AD, bilgisayar hesaplarını şirket içi Active Directory (AD) ve Azure AD 'deki cihaz nesnesini eşitlenmiş halde tutmak için Azure AD Connect yapılandırmasını gerektirir.

1.1.819.0 sürümünden itibaren Azure AD Connect hibrit Azure AD'ye katılımı yapılandırmak için bir sihirbaz sağlar. Bu sihirbazın kullanılması yapılandırma işlemini basitleştirir.  

Azure AD Connect yapılandırmak için, Azure AD için genel bir yöneticinin kimlik bilgilerine ihtiyacınız vardır.  

> [!TIP]  
> Aşağıdaki yordam Azure AD Connect kurulumu için yetkili olarak düşünülmemelidir, ancak Intune ile Configuration Manager arasında ortak yönetim yapılandırmasını kolaylaştırmak için burada verilmiştir. Azure AD 'nin kurulumu için bu ve ilgili yordamlarda bulunan yetkili içerik için bkz. Azure AD belgelerinde [yönetilen etki alanları için karma Azure AD birleştirmesini yapılandırma](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) .  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Azure AD Connect kullanarak karma Azure AD katılımı yapılandırma

1. Azure AD Connect (1.1.819.0 veya üzeri) [en son sürümünü](https://www.microsoft.com/download/details.aspx?id=47594) alın ve yükler.  
2. Azure AD Connect başlatın ve ardından **Yapılandır**' ı seçin.
3. **Ek görevler** sayfasında **cihaz seçeneklerini yapılandır**' ı seçin ve ardından **İleri**' yi seçin.
4. **Genel bakış** sayfasında **İleri**' yi seçin.
5. **Azure AD 'ye Bağlan** sayfasında, Azure AD için genel bir yöneticinin kimlik bilgilerini girin.
6. **Cihaz seçenekleri** sayfasında, **karma Azure AD birleştirmesini Yapılandır**' ı seçin ve ardından **İleri**' yi seçin.
7. **Cihaz işletim sistemleri** sayfasında, Active Directory ortamınızda cihazlar tarafından kullanılan işletim sistemlerini seçin ve ardından **İleri**' yi seçin.  

   Windows alt etki alanına katılmış cihazları destekleme seçeneğini belirleyebilirsiniz, ancak cihazların ortak yönetiminin yalnızca Windows 10 için desteklendiğini aklınızda bulundurun.
8. **SCP** sayfasında, hizmet bağlantı noktasını (SCP) yapılandırmak Azure AD Connect istediğiniz her şirket içi orman için aşağıdaki adımları uygulayın ve ardından **İleri**' yi seçin:  
   1. Ormanı seçin.  
   2. Kimlik doğrulama hizmetini seçin.  Bir Federasyon etki alanınız varsa, kuruluşunuz özel olarak Windows 10 istemcileri olmadığından ve bilgisayar/cihaz eşitlemesini yapılandırdıysanız veya kuruluşunuz [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)kullanıyorsa, AD FS Server ' ı seçin.  
   3. Kuruluş yöneticisinin kimlik bilgilerini girmek için **Ekle** seçeneğine tıklayın.  
9. Yönetilen bir etki alanınız varsa, bu adımı atlayın.  

   **Federasyon yapılandırması** sayfasında, AD FS yöneticinizin kimlik bilgilerini girin ve ardından **İleri**' yi seçin.
10. **Yapılandırmaya hazırlanma** sayfasında **Yapılandır**' ı seçin.
11. **Yapılandırma Tamam** sayfasında **Çıkış**' ı seçin.

Etki alanına katılmış Windows cihazları için karma Azure AD JOIN 'i tamamlamada sorunlarla karşılaşırsanız bkz. [Windows için karma Azure AD 'ye katılma sorunlarını giderme geçerli cihazlar](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>İstemcileri Azure AD 'ye kaydolmak üzere yönlendirmek için Istemci ayarlarını yapılandırma

Configuration Manager istemcilerini Azure AD 'ye otomatik olarak kaydedecek şekilde yapılandırmak için Istemci ayarlarını kullanın.  

1. **Configuration Manager konsolu** > **yönetimine** > **genel bakış** > **istemci ayarlarını**açın ve **varsayılan istemci ayarlarını**düzenleyin.  

2. **Cloud Services**seçin.  

3. **Varsayılan ayarlar** sayfasında, **Yeni Windows 10 etki alanına katılmış cihazları Azure Active Directory ile otomatik olarak kaydet** ' i = **Evet**olarak ayarlayın.  

4. Bu yapılandırmayı kaydetmek için **Tamam**’ı seçin.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Cihazların otomatik kaydını Intune 'a yapılandırma

Daha sonra, Intune ile cihazların otomatik kaydını ayarlayacağız. Otomatik kayıt ile yönettiğiniz cihazlar Configuration Manager otomatik olarak Intune 'a kaydolur.

Otomatik kayıt, kullanıcıların Windows 10 cihazlarını Intune 'a kaydetmelerini de sağlar. Cihazlar, bir Kullanıcı kendi iş hesabını kişisel cihazına eklediğinde veya şirkete ait bir cihaz Azure Active Directory katıldığında kaydeder.  

1. [Azure Portal](https://portal.azure.com/) oturum açın ve **Azure Active Directory** > **Mobility (MDM ve MAM)** > **Microsoft Intune**öğesini seçin.  

2. **MDM Kullanıcı kapsamını**yapılandırın. Hangi kullanıcıların cihazlarının Microsoft Intune tarafından yönetileceğini yapılandırmak için aşağıdakilerden birini belirtin ve URL değerleri için varsayılanları kabul edin.  

   - **Bazıları**: Windows 10 cihazlarını otomatik olarak kaydedebilen **grupları** seçin  

   - **Tümü**: tüm kullanıcılar Windows 10 cihazlarını otomatik olarak kaydedebilir

   - **Hiçbiri**: MDM otomatik kaydını devre dışı bırak

   > [!IMPORTANT]  
   > Bir grup için hem **MAM kullanıcı kapsamı** hem de MDM kaydı (**MDM kullanıcı kapsamı**) etkinse yalnızca MAM etkinleştirilir. Yalnızca mobil uygulama yönetimi (MAM), bu gruptaki kullanıcılar kişisel cihaz katılırsanız bu gruptaki kullanıcılar için eklenir. Cihazlar otomatik olarak MDM kaydı yapılır.  

3. Otomatik kayıt yapılandırmasını gerçekleştirmek için **Kaydet** ' i seçin.  

4. **Mobility (MDM ve MAM)** öğesine dönüp **Microsoft Intune kaydı**' nı seçin.  

    > [!NOTE]
    > Bazı kiracıların yapılandırmak için bu seçeneklere sahip olmayabilir.<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** , Azure AD için MDM uygulamasını nasıl yapılandıracaksınız. **Microsoft Intune kaydı** , IOS ve Android kaydı için Multi-Factor Authentication ilkelerini uyguladığınızda oluşturulan belirli BIR Azure AD uygulamasıdır. Daha fazla bilgi için bkz. [Intune cihaz kayıtları için çok faktörlü kimlik doğrulaması gerektirme](https://docs.microsoft.com/intune/enrollment/multi-factor-authentication).

5. MDM Kullanıcı kapsamı için **Tümü**' nü ve ardından **Kaydet**' i seçin.  

## <a name="enable-co-management-in-configuration-manager"></a>Configuration Manager içinde ortak yönetimi etkinleştirme

Karma Azure AD kurulumu ve Configuration Manager istemci yapılandırması sayesinde, anahtarı çevirmek ve Windows 10 cihazlarınızın ortak yönetimini etkinleştirmek için hazırsınız demektir.  

> [!TIP]
> - Ortak yönetimi etkinleştirdiğinizde, bir koleksiyonu *pilot grubu*olarak atayacaksınız. Bu, ortak yönetim yapılandırmalarınızı test etmek için az sayıda istemci içeren bir gruptur. Yordamı başlamadan önce uygun bir koleksiyon oluşturmanızı öneririz. Daha sonra bu koleksiyonu, bunu yapmak için yordamdan çıkmadan seçebilirsiniz.
> - Configuration Manager sürüm 1906 ' den başlayarak, her iş yükü için farklı bir *pilot grubu* atayabileceğinizden bu yana birden çok koleksiyona ihtiyacınız olabilir.

### <a name="enable-co-management-starting-in-version-1906"></a>Sürüm 1906 ' den başlayarak ortak yönetimi etkinleştirme

Ortak yönetimi Configuration Manager sürüm 1906 ' den başlayarak etkinleştirmek için aşağıdaki yönergeleri izleyin:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Sürüm 1902 ve önceki sürümlerde ortak yönetimi etkinleştirme

Configuration Manager sürüm 1902 ve önceki sürümleri için ortak yönetimi etkinleştirmek üzere aşağıdaki yönergeleri izleyin:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Sonraki adımlar

- Ortak [Yönetim Panosu](how-to-monitor.md) ile birlikte yönetilen cihazların durumunu gözden geçirme
- Ortak yönetimden [anında değer](quickstarts.md#immediate-value) almaya başlayın
- Şirket kaynaklarına Kullanıcı erişimini yönetmek için [koşullu erişim](quickstart-conditional-access.md) ve Intune Uyumluluk kurallarını kullanma
