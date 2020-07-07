---
title: Intune ile Wandera Mobile Threat Protection tümleştirmesi ayarlama
titleSuffix: Intune on Azure
description: Şirket kaynaklarınıza mobil cihaz erişimini denetlemek için Microsoft Intune ile Wandera mobil tehdit koruması çözümünü ayarlama.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc44bb114d6ff9089a01da2d0b7db7aa7527f4b5
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.contentlocale: tr-TR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972156"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Wandera Mobile Threat Protection 'ı Intune ile tümleştirme  

Wandera Mobile Threat Defense çözümünü Intune ile bütünleştirmek için aşağıdaki adımları izleyin.  

## <a name="before-you-begin"></a>Başlamadan önce  

Wandera 'yı Intune ile tümleştirme işlemine başlamadan önce, aşağıdaki önkoşulların yerine geldiğinden emin olun:

- Intune aboneliği
- Azure Active Directory yönetici kimlik bilgileri ve atanan rol aşağıdaki izinleri verebilir:

    - Oturum açma ve kullanıcı profilini okuma
    - Dizine oturum açmış kullanıcı olarak erişin
    - Dizin verilerini oku
    - Cihaz risk bilgilerini Intune 'a gönderme
 
- Geçerli bir Wandera aboneliği
    - Süper yönetici ayrıcalıklarına sahip bir yönetici hesabı

## <a name="integration-overview"></a>Tümleştirmeye genel bakış

Wandera ve Intune arasında mobil tehdit savunması tümleştirmesini etkinleştirmek şunları gerektirir:

- Wandera 'nın UıEM Connect hizmetini etkinleştirerek Azure ve Intune ile bilgileri eşitlemesini sağlayabilirsiniz. Bu, Mobile Threat Defense (MTD) cihaz tehdit düzeyiyle birlikte Kullanıcı ve cihaz yaşam döngüsü yönetimi (LCM) meta verilerini içerir.
- Bir cihaz kaydı davranışını tanımlamak için Wandera 'da etkinleştirme profilleri oluşturun.
- İOS ve Android cihazları için Wandera Over-AIR ' i dağıtın.
- Yönetilmeyen iOS ve Android cihazlarda MAM-WE kullanarak Son Kullanıcı self servis için Wandera 'ı yapılandırın.

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Wandera Mobile Threat Defense tümleştirmesi ayarlama

Wandera ve Intune arasında tümleştirmeyi ayarlamak, Wandera personelinden destek gerektirmez ve birkaç dakika içinde kolayca gerçekleştirilebilir.

### <a name="enable-support-for-wandera-in-intune"></a>Intune 'da Wandera desteğini etkinleştir

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Kiracı Yönetimi**  >  **bağlayıcıları ve belirteçleri**  >  **Mobil tehdit savunması**  >  **Ekle**' yi seçin.
3. **Bağlayıcı Ekle** sayfasında, açılan menüyü kullanın ve **wandera**' yı seçin. Sonra **Oluştur**' u seçin.  
4. Mobil tehdit savunması bölmesinde bağlayıcı listesinden **Wandera** MTD bağlayıcısını seçerek **bağlayıcı düzenleme** bölmesini açın. [Radar](https://radar.wandera.com/login), wandera Yönetici Konsolu 'nu açmak ve oturum açmak Için **wandera yönetici konsolunu aç** ' ı seçin. 
5. Wandera RADAR konsolunda, **tümleştirme > Uıem tümleştirmesi**' ne gidin ve **uıem Connect** sekmesini seçin. EMM satıcı açılan listesini kullanın ve **Microsoft Intune**' ı seçin.
6. Aşağıda gösterilene benzer bir ekran sunulacaktır ve bu, tümleştirmeyi tamamlamaya yönelik iznin gerekli olduğunu gösterir:

   ![Tümleştirmeler ve izinler](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. Intune kullanıcı ve cihaz eşitleme ' nin yanında, Azure ve Intune ile yaşam döngüsü yönetimi (LCM) işlevlerini gerçekleştirmek üzere Wandera onayını sağlamak için Izin ver düğmesine tıklayın.
8. İstendiğinde, Azure yönetici kimlik bilgilerinizi seçin veya girin. İstenen izinleri gözden geçirin ve ardından kuruluşunuzun adına onay kutusunu seçin. Son olarak, LCM tümleştirmesini yetkilendirmek için kabul et ' e tıklayın.

   ![İzinleri kabul et](./media/wandera-mtd-connector-integration/permissions.png)

10. Otomatik olarak RADAR Yönetici konsoluna geri döndürülecektir.  Yetkilendirme başarılı olduysa, Izin ver düğmesinin yanında yeşil bir onay işareti görürsünüz.
11. Her birinin yanında yeşil onay işaretlerine gelene kadar ilgili Izin düğmelerine tıklayarak, kalan listelenen tümleştirmelerin onay işlemini tekrarlayın.

    ![Eşitleme grubu](./media/wandera-mtd-connector-integration/sync-group-name.png)

12. Intune konsoluna dönün ve Wandera MTD bağlayıcısını düzenlemeyle çalışmaya geri edin. Tüm kullanılabilir ' ı açık olarak ayarlayın ve ardından yapılandırmayı kaydedin.

    ![Wandera 'yi etkinleştir](./media/wandera-mtd-connector-integration/enable-wandera.png)

Intune ve Wandera artık bağlı.

## <a name="create-activation-profiles-in-wandera"></a>Wandera 'da etkinleştirme profilleri oluşturma

Intune tabanlı dağıtımlar, RADAR içinde tanımlanan Wandera etkinleştirme profilleri kullanılarak kolaylaştırılır.  Her etkinleştirme profili, kimlik doğrulama gereksinimleri, hizmet özellikleri ve ilk grup üyeliği gibi belirli yapılandırma seçeneklerini tanımlar.

Wandera 'da etkinleştirme profili oluşturduktan sonra Intune 'daki kullanıcılara ve cihazlara "atarsınız".  Bir etkinleştirme profili, cihaz platformları ve yönetim stratejileri arasında Universal olsa da aşağıdaki adımlarda, bu farklılıklara göre Intune 'un nasıl yapılandırılacağı tanımlanır.

Buradaki adımlarda, Wandera 'da, Intune aracılığıyla hedef cihazlarınıza dağıtmak istediğiniz bir etkinleştirme profili oluşturdunuz. Lütfen Wandera etkinleştirme profilleri oluşturma ve kullanma hakkında daha fazla bilgi için bkz. [etkinleştirme profilleri Kılavuzu](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links) .

> [!NOTE]
> Intune veya MAM-WE aracılığıyla dağıtım için etkinleştirme profilleri oluştururken, en yüksek güvenlik, platformlar arası uyumluluk ve kolaylaştırılmış bir son kullanıcı deneyimi için > kimlik sağlayıcısı tarafından kimliği doğrulanmış bir Kullanıcı Azure Active Directory seçeneğini ayarladığınızdan emin olun.

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>Wandera Over-Air ile MDM yönetimli cihazlara dağıtım

Intune tarafından yönetilen iOS ve Android cihazlarda, hızlı gönderim tabanlı etkinleştirmeler için Wandera, kablosuz olarak dağıtılabilir. Bu bölüme geçmeden önce ihtiyacınız olan etkinleştirme profilini zaten oluşturmuş olduğunuzdan emin olun. Wandera 'nın yönetilen cihazlara dağıtımı şunları içerir:
- Intune 'a Wandera yapılandırma profilleri ekleme ve hedef cihazlara atama.
- Wandera uygulamasını ve ilgili uygulama yapılandırmasını Intune 'a ekleme ve hedef cihazlara atama.

### <a name="configure-and-deploy-ios-configuration-profiles"></a>İOS yapılandırma profillerini yapılandırma ve dağıtma 

Bu bölümde, **gerekli** iOS cihaz yapılandırma dosyalarını indirecek ve ardından bunları MDM aracılığıyla Intune yönetilen cihazlarınıza sunacaktır.

1. **Radar**' de, dağıtmak Istediğiniz etkinleştirme profiline gidin (cihazlar > etkinleştirmeleri), ardından **yönetilen cihazlar > Microsoft uç nokta yöneticisi ' ne > dağıtım stratejileri sekmesine**tıklayın.
2. **Apple iOS** denetimli veya **Apple iOS** denetimli bölümlerini cihaz filo yapılandırmanıza göre genişletin.
3. Belirtilen yapılandırma profillerini indirin ve aşağıdaki bir adımda onları karşıya yüklemeye hazırlanın.
4. **Microsoft Intune yönetici konsolu 'nu** açın ve **cihazlar > IOS/ıpados > yapılandırma profilleri**' ne gidin.  **Profil oluştur**’a tıklayın.
5. Görüntülenen panelde, **Platform**altında **IOS/ıpados** ' ı seçin ve ardından profil altında **özel** ' i seçin. Sonra **Oluştur**' a tıklayın.
6. **Ad** alanına, yapılandırma için bir açıklama başlığı sağlayın ve bu, en iyi şekılde, radar 'de etkinleştirme profilini adlandırdıklarınızı eşleştirir. Bu, gelecekte çapraz başvurmayı kolaylaştırmak için yardımcı olur. Alternatif olarak, isterseniz etkinleştirme profili kodunu sağlayın. Adı bu şekilde düzelterek, yapılandırmanın denetimli veya denetimli cihazlar için olup olmadığını belirten bir değer kullanmanızı öneririz.
7. İsteğe bağlı olarak, yapılandırmanın amacı/kullanımı hakkında diğer yöneticiler için daha fazla ayrıntı sağlayan bir **Açıklama** sağlayın. **İleri**’ye tıklayın.
8. **Dosya Seç** ' e tıklayın ve adım 3 ' te Indirilen uygun etkinleştirme profiline karşılık gelen indirilen yapılandırma profilini bulun. Her ikisini de indirdiyseniz ilgili denetimli veya denetlenmeyen profili seçmek için dikkatli olmanız gerekir. **İleri**’ye tıklayın.
   <!-- image placeholder - ending future availability -->
9.  **Kapsam etiketlerini** Intune RBAC uygulamalarınızın gerektirdiği şekilde tanımlayın.  **İleri**’ye tıklayın.
10. Yapılandırma profilini, Wandera yüklenmiş olması gereken kullanıcı veya cihaz gruplarına **atayın** .  Etkinleştirmeleri doğruladıktan sonra, bir test grubu ile başlayıp daha sonra genişletmeyi öneririz. **İleri**’ye tıklayın.
11. Yapılandırma **profilini oluşturmak ve dağıtmak için ' a** tıklayın, gerektiğinde doğruluğu doğru düzenlemeyle ilgili yapılandırmayı gözden geçirin.

> [!NOTE]
> Wandera, denetimli iOS cihazları için gelişmiş bir dağıtım profili sunar. Denetimli ve denetlenen ve denetlenmediğini karışık cihazlar varsa, diğer profil türü için yukarıdaki adımları gerektiği şekilde tekrarlayın. Bu adımların, Intune aracılığıyla dağıtılacak sonraki etkinleştirme profillerinin izlenmesi gerekir. Önceden denetlenen ve denetimli iOS cihazlarından oluşan karma bir filo varsa ve denetimli mod tabanlı ilke atamalarıyla ilgili yardıma ihtiyacınız varsa lütfen wandera desteğine başvurun. 

## <a name="deploying-wandera-to-mam-we-devices"></a>MAM-WE cihazlarına Wandera dağıtma
Intune tarafından yönetilmeyen ve (MAM-WE) cihazlarından oluşan cihazlarda, Wandera, MAM özellikli uygulamalarda şirket verilerini etkinleştirmek ve korumak için tümleşik bir kimlik doğrulama tabanlı ekleme deneyimi kullanır. 

Aşağıdaki bölümlerde, son kullanıcıların şirket verilerine erişmeden önce Wandera 'nın sorunsuz bir şekilde etkinleştirmesini sağlamak üzere Wandera ve Intune 'un nasıl yapılandırılacağı açıklanır. 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>Bir Wandera etkinleştirme profilinde Azure cihaz sağlamayı yapılandırma
MAM ile kullanılacak etkinleştirme profilleri-kimlik sağlayıcısı tarafından kimliği doğrulanmış > Azure Active Directory seçeneği ile Ilişkili Kullanıcı olmalıdır.
1. **Wandera radar** portalında, mevcut bir SEÇIN veya mam-we cihazlarının cihazlarda kayıt sırasında kullanacağı yeni bir etkinleştirme profili oluşturun > etkinleştirmeleri. 
2. **Dağıtım stratejileri sekmesine ve yönetilmeyen cihazlar** ' a tıklayıp **Azure cihaz sağlama** bölümüne gidin.
3. Uygun metin alanına **Azure AD KIRACı kimliğinizi** girin. Kiracı KIMLIĞINIZ elinizin altında değilse, bu değeri panonuza kolayca kopyalayabileceğiniz yeni bir sekmede Azure AD 'yi açmak için **KIRACı kimliği Al** bağlantısına tıklayın.
4. Seçim Kullanıcı etkinleştirmelerini belirli gruplar ile sınırlamak için **grup kimliklerini** belirtin.
   - Bir veya daha fazla **Grup Kimliği** tanımlanmışsa, BIR kullanıcı mam etkinleştirdiğinde, bu etkinleştirme profilini kullanarak etkinleştirmek için belirtilen gruplardan en az birinin üyesi olması gerekir.
   - Aynı Azure kiracı KIMLIĞIYLE, ancak farklı grup kimlikleriyle yapılandırılmış birden çok etkinleştirme profili ayarlayabilirsiniz. Bu, cihazları Azure grup üyeliğine göre Wandera 'a kaydetmenize izin verir ve etkinleştirme sırasında gruba göre farklı özellikleri etkinleştirir.
   - Herhangi bir grup kimliği belirtmeyen tek bir "varsayılan" etkinleştirme profili yapılandırabilirsiniz.  Bu grup, kimliği doğrulanmış kullanıcının başka bir etkinleştirme profiliyle ilişkisi olan bir grubun üyesi olmadığı tüm etkinleştirmeler için bir catch-all işlevi görür.
5. Sayfanın sağ üst köşesindeki **Kaydet** ' e tıklayın.

## <a name="next-steps"></a>Sonraki Adımlar
- Android ve iOS/ıpados cihazlarına Wandera etkinleştirme profilleriniz, RADAR 'e yüklenmiş olarak iOS ve iOS için Intune 'da istemci uygulamalar oluşturun. Wandera uygulama yapılandırması, gönderilen cihaz yapılandırma profillerini karmaşıklama etmek için gerekli işlevleri sağlar ve tüm dağıtımlar için önerilir. Yordamlar ve Wandera uygulamalarına özgü özel ayrıntılar için bkz. [MTD uygulamaları ekleme](mtd-apps-ios-app-configuration-policy-add-assign.md) . 
- Endpoint Manager ile tümleştirmiş olduğunuza göre artık yapılandırmanızı ayarlayabilir, raporları görüntüleyebilir ve mobil cihazlarınız arasında daha geniş bir dağıtım yapabilirsiniz. Ayrıntılı yapılandırma kılavuzlarında, Wandera belgelerindeki [Destek Merkezi Başlarken Kılavuzu](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started) ' na bakın.
