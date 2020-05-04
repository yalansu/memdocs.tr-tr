---
title: JAMF Pro bulut bağlayıcısını Microsoft Intune ile tümleştirme
titleSuffix: Microsoft Intune
description: JAMF ile yönetilen cihazları tümleştirmenize ve güvenli hale getirmeye yardımcı olmak için Azure Active Directory Koşullu erişim ile JAMF Cloud bağlayıcısını Microsoft Intune uyumluluk ilkeleriyle birlikte kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f86b418df46069b2a33dd56d06e0e82dbbbf8090
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81538406"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>JAMF bulut bağlayıcısını Microsoft Intune ile kullanma

Bu makale, JAMF Pro 'Yu Microsoft Intune ile tümleştirmek için JAMF bulut bağlayıcısını yüklemenize yardımcı olabilir. Bulut bağlayıcısı, [Uyumluluk Için JAMF Pro 'Yu Intune Ile tümleştirme](../protect/conditional-access-integrate-jamf.md)bölümünde belirtildiği gibi, tümleştirmeyi el ile yapılandırırken gereken birçok adımı otomatikleştirir.

Bulut bağlayıcısını ayarlarken:

- Kurulum, JAMF Pro uygulamalarını Azure 'da otomatik olarak oluşturur ve bunları el ile yapılandırma gereksinimini değiştirir.
- JAMF Pro 'nun birden çok örneğini Intune aboneliğinizi barındıran aynı Azure kiracısı ile tümleştirebilirsiniz.

Tek bir Azure kiracısıyla birçok JAMF Pro örneğini bağlamak yalnızca bulut bağlayıcısını kullandığınızda desteklenir. El ile yapılandırılmış bir bağlantı kullandığınızda bir JAMF yalnızca tek bir örneği Azure kiracısı ile tümleştirilebilir.

Bulut bağlayıcısının kullanımı isteğe bağlıdır:

- Artık JAMF ile tümleştirmeyen yeni kiracılar için, bu makalede açıklandığı gibi bulut bağlayıcısını yapılandırmayı seçebilirsiniz. İsterseniz, [Uyumluluk Için JAMF Pro 'Yu Intune Ile tümleştirme](../protect/conditional-access-integrate-jamf.md) bölümünde açıklandığı gibi tümleştirmeyi el ile yapılandırabilirsiniz
- El ile yapılandırması olan kiracılar için, bu tümleştirmeyi kaldırmayı ve ardından bulut bağlayıcısını ayarlamayı seçebilirsiniz. Hem mevcut bir tümleştirmenin kaldırılması hem de bulut bağlayıcısının ayarlanması bu makalede açıklanmıştır.

Önceki tümleştirmenizi JAMF Cloud Connector ile değiştirmeyi planlıyorsanız:

- JAMF Pro için kurumsal uygulamaları silmeyi ve el ile tümleştirmeyi devre dışı bırakmayı içeren [geçerli yapılandırmanızı kaldırma yordamını](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)kullanın. Ardından, [bulut bağlayıcısını yapılandırmak için yordamını](#configure-the-cloud-connector-for-a-new-tenant)kullanabilirsiniz.
- Cihazları yeniden kaydetmeniz gerekmez. Zaten kayıtlı olan cihazlar bulut bağlayıcısını ek yapılandırma olmadan kullanabilir.
- Kayıtlı cihazlarınızın durumlarını raporlamalarını sağlamak için el ile tümleştirmenizi kaldırmanın 24 saat içinde bulut bağlayıcısını yapılandırmayı unutmayın.

JAMF bulut Bağlayıcısı hakkında daha fazla bilgi için, docs.jamf.com adresindeki [bulut bağlayıcısını kullanarak macOS Intune tümleştirmesini yapılandırma](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html) konusuna bakın.

## <a name="prerequisites"></a>Önkoşullar

**Ürünler ve hizmetler**:  
- JAMF Pro 10,18 veya üzeri
- Koşullu erişim ayrıcalıklarına sahip bir JAMF Pro Kullanıcı hesabı  
- Microsoft Intune
- Microsoft Azure AD Premium
- [MacOS için Şirket Portalı uygulaması](https://aka.ms/macoscompanyportal)
- OS X 10,12 Yosemite veya üzeri olan macOS cihazları

**Ağ**:  
JAMF ve Intune 'un doğru tümleşmesini sağlamak için aşağıdaki bağlantı noktalarına ve uç noktalara erişilebilir olmalıdır:

- **Intune**: bağlantı noktası 443
- **Apple**: Ports 2195, 2196 ve 5223 (Intune 'a anında iletme bildirimleri)
- **JAMF**: bağlantı noktaları 80 ve 5223

- Uç Noktalar:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

APNS 'nin ağda düzgün çalışması için, giden bağlantıları ve aşağıdaki bağlantı noktalarından yeniden yönlendirmeyi etkinleştirmeniz gerekir:

- Tüm istemci ağlarından 5223 ve 443 TCP bağlantı noktaları üzerinde Apple 17.0.0.0/8 bloğu.
- JAMF Pro sunucularından 2195 ve 2196 bağlantı noktaları.

Bu bağlantı noktaları hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Intune ağ yapılandırma gereksinimleri ve bant genişliği](../fundamentals/network-bandwidth-use.md).
- Jamf.com üzerinde [JAMF Pro tarafından kullanılan ağ bağlantı noktaları](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) .
- Support.apple.com üzerinde [Apple yazılım ürünleri tarafından kullanılan TCP ve UDP bağlantı noktaları](https://support.apple.com/HT202944)

**Hesaplar**:  
Bu makaledeki yordamlar aşağıdaki izinlere sahip hesapların kullanılmasını gerektirir:

- **JAMF Pro konsolu**: JAMF Pro 'yu yönetme izinlerine sahip bir hesap
- **Microsoft uç nokta yönetimi Yönetim Merkezi**: genel yönetici
- **Azure Portal**: genel yönetici

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>Daha önce yapılandırılmış bir kiracı için JAMF Pro tümleştirmesini kaldırma

Bulut bağlayıcısını yapılandırmadan *önce* Azure kiracınızdan bir JAMF Pro 'nun el ile yapılandırılmış bir tümleştirmesini kaldırmak için aşağıdaki yordamı kullanın.

JAMF Pro ve Intune arasında daha önce bir bağlantı ayarlanmamışsa veya zaten bulut bağlayıcısını kullanan bir veya daha fazla bağlantınız varsa, bu yordamı atlayın ve [Yeni bir kiracı Için bulut bağlayıcısını yapılandırmaya](#configure-the-cloud-connector-for-a-new-tenant)başlayın.

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>El ile yapılandırılmış bir JAMF Pro tümleştirmesini kaldırma

1. JAMF Pro konsolunda oturum açın.

2. **Ayarlar** ' ı (sağ üst köşedeki dişli simgesi) seçin ve ardından **küresel yönetim** > **koşullu erişimi**' ne gidin.

   ![Koşullu erişime git](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. **Düzenle**' yi seçin.

4. **MacOS Için Intune Tümleştirmesini Etkinleştirme**onay kutusunu işaretleyin.

   Bu ayarı kaldırdığınızda, bağlantıyı devre dışı bırakır, ancak yapılandırmanız kaydedilir.

5. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431) ' nde oturum açın ve **kiracı yönetim** > **ortağı cihaz yönetimi**' ne gidin.

   **Iş ortağı cihaz yönetimi** düğümünde, **jamf IÇIN Azure Active Directory uygulama kimliğini BELIRTIN** alanında **uygulama kimliğini** silin ve ardından **Kaydet**' i seçin.

   Uygulama KIMLIĞI, JAMF Pro 'da el ile tümleştirme ayarladığınızda Azure 'da oluşturulan Azure Enterprise uygulamasının KIMLIĞIDIR.

6. [Azure Portal](https://portal.azure.com/) , genel yönetici izinlerine sahip bir hesapla oturum açın ve **Azure Active Directory** > **kurumsal uygulamalara**gidin.

   İki JAMF uygulaması bulun ve silin. Yeni uygulamalar, bir sonraki yordamda JAMF bulut bağlayıcısını yapılandırdığınızda otomatik olarak oluşturulacaktır.

   ![Silinecek JAMF uygulamalarını seçin](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   JAMF Pro 'da tümleştirmeyi devre dışı bırakmış ve kurumsal uygulamaları sildikten sonra, **Iş ortağı cihaz yönetimi** düğümü **sonlandırılan**bağlantı durumunu görüntüler.

   ![Sonlandırılan bağlantı durumu](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

JAMF Pro tümleştirmesinin el ile yapılandırmasını başarıyla kaldırmış olduğunuza göre, bulut bağlayıcısını kullanarak tümleştirmeyi ayarlayabilirsiniz. Bunu yapmak için, bu makaledeki [Yeni bir kiracı Için bulut bağlayıcısını yapılandırma](#configure-the-cloud-connector-for-a-new-tenant) konusuna bakın.

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>Yeni bir kiracı için bulut bağlayıcısını yapılandırma

JAMF bulut bağlayıcısını, JAMF Pro Microsoft Intune 'Yu bütünleştirmek üzere yapılandırmak için aşağıdaki yordamı kullanın:

- JAMF Pro ve Intune arasında Azure kiracınız için yapılandırılmış bir tümleştirmeniz yok.
- Azure kiracınızda JAMF Pro ve Intune arasında ayarlanmış bir bulut bağlayıcısı zaten var ve aboneliğiniz ile ek bir JAMF örneğini tümleştirmek istiyorsunuz.

Şu anda Intune ve JAMF Pro arasında el ile yapılandırılmış bir tümleştirmeye sahipseniz, devam etmeden önce Bu tümleştirmeyi kaldırmak için bu makaledeki [daha önce yapılandırılmış bir kiracı Için JAMF Pro tümleştirmesini kaldırma](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) bölümüne bakın. El ile yapılandırılan bir tümleştirmenin kaldırılması, bulut bağlayıcısını sorunsuz bir şekilde ayarlayabilmeniz için gereklidir.

### <a name="create-a-new-connection"></a>Yeni bağlantı oluşturma

1. JAMF Pro konsolunda oturum açın.

2. **Ayarlar** ' ı (sağ üst köşedeki dişli simgesi) seçin ve ardından **küresel yönetim** > **koşullu erişimi**' ne gidin.

   ![Koşullu erişime git](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. **Düzenle**' yi seçin.

4. **MacOS Için Intune Tümleştirmesini Etkinleştirme**onay kutusunu seçin.
   - JAMF Pro 'Nun Microsoft Intune envanter güncelleştirmelerini göndermesini sağlamak için bu ayarı seçin.
   - Bağlantıyı devre dışı bırakmak, ancak yapılandırmanızı kaydetmek için bu ayarın işaretini kaldırabilirsiniz.

   > [!IMPORTANT]
   > **MacOS Için Intune tümleştirmesini etkinleştir** zaten seçildiyse ve *bağlantı türü* **el ile**olarak ayarlandıysa, devam etmeden önce Bu tümleştirmeyi kaldırmanız gerekir. Devam etmeden önce bu makaledeki [daha önce yapılandırılmış bir kiracı Için JAMF Pro tümleştirmesini kaldırma](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) bölümüne bakın.

5. *Bağlantı türü*altında, **bulut bağlayıcısı**' nı seçin.

   ![JAMF Pro konsolundaki bulut bağlayıcısını seçin](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. **Sogeign Cloud** açılır menüsünde, Microsoft 'Tan Sovereign bulutunuzun konumunu seçin.

7. Microsoft Azure tarafından tanınmayan bilgisayarlar için aşağıdaki giriş sayfası seçeneklerinden birini seçin:
   - **Varsayılan JAMF Pro cihaz kayıt sayfası** -MacOS cihazının durumuna bağlı olarak, bu seçenek kullanıcıları JAMF Pro cihaz kayıt portalına (JAMF Pro 'ya kaydolmak için) veya Intune Şirket Portalı uygulamasına (Azure AD 'ye kaydolmak için) yönlendirir.
   - **Erişim engellendi sayfası**
   - **Özel URL**

8. **Bağlan**’ı seçin. JAMF Pro uygulamalarını Azure 'a kaydetmeye yönlendirilirsiniz.

   İstendiğinde, Microsoft Azure kimlik bilgilerinizi belirtin ve istenen izinleri vermek için ekrandaki yönergeleri izleyin. **Bulut bağlayıcısı**ve ardından **bulut bağlayıcısı Kullanıcı kaydı uygulaması**için izinler verirsiniz. Her iki uygulama da kurumsal uygulamalar olarak Azure 'a kaydedilir.

   Her iki uygulama için izinler verildikten sonra, **uygulama kimliği** sayfası açılır.

9. **Uygulama kimliği** sayfasında, Kopyala ' yı seçin **ve Intune 'u açın**.

   ![Uygulama Kimliği](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   *Uygulama kimliği* , sonraki adımda kullanılmak üzere sistem panonuza kopyalanır ve *Microsoft Endpoint Manager Yönetim Merkezi* 'ndeki **iş ortağı cihaz yönetimi** düğümü açılır. (**Kiracı yönetim** > **ortağı cihaz yönetimi**).

10. **Iş ortağı cihaz yönetimi** düğümünde, IÇINDEKI **uygulama kimliğini** **JAMF için Azure Active Directory uygulama kimliğini belirtin** alanına *yapıştırın* ve **Kaydet**' i seçin.

    ![İş ortağı cihaz yönetimini yapılandırma](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. JAMF Pro 'da uygulama KIMLIĞI sayfasına dönün ve **Onayla**' yı seçin.

12. JAMF Pro, yapılandırmayı tamamlar ve test eder ve koşullu erişim ayarları sayfasında bağlantının başarısını veya başarısızlığını görüntüler. Aşağıdaki görüntü başarı örneğidir:

    ![JAMF Pro 'da başarılı yapılandırma onaylandı](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. Microsoft Endpoint Manager Yönetim Merkezi 'nde **Iş ortağı cihaz yönetimi** düğümünü yenileyin. Bağlantı şimdi **etkin**olarak gösterilmelidir:

    ![Bağlantı durumu etkin](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

JAMF Pro ve Microsoft Intune arasındaki bağlantı başarıyla oluşturulduğunda, JAMF Pro, Azure AD 'ye kayıtlı her bilgisayar için envanter bilgilerini Microsoft Intune gönderir (Azure AD 'ye kaydolma, son kullanıcı iş akışıdır). Bir Kullanıcı ve bilgisayar için koşullu erişim envanteri durumunu bir bilgisayarın, JAMF Pro 'daki envanter bilgilerinin yerel kullanıcı hesabı kategorisinde görüntüleyebilirsiniz.

JAMF bulut bağlayıcısını kullanarak bir JAMF Pro örneğini tümleştirdikten sonra, Azure kiracınızda aynı Intune aboneliğiyle ek JAMF Pro örnekleri yapılandırmak için bu yordamı kullanabilirsiniz.  

## <a name="set-up-compliance-policies-and-register-devices"></a>Uyumluluk ilkelerini ayarlama ve cihazları kaydetme

Intune ve JAMF arasındaki tümleştirmeyi yapılandırdıktan sonra, [JAMF tarafından yönetilen cihazlara uyumluluk ilkeleri uygulamanız](../protect/conditional-access-assign-jamf.md)gerekir.

## <a name="disconnect-jamf-pro-and-intune"></a>JAMF Pro ve Intune bağlantısını kesme

JAMF Pro tümleştirmesini Intune ile kaldırmanız gerekir, bağlantıyı JAMF Pro konsolundan kaldırmak için aşağıdaki adımları kullanın. Bu bilgiler hem bulut bağlayıcısı hem de el ile yapılandırılmış bir tümleştirme için geçerlidir.

1. JAMF Pro 'da **küresel yönetim** > **koşullu erişimi**' ne gidin. **MacOS Intune tümleştirmesi** sekmesinde **Düzenle**' yi seçin.

2. **MacOS Için Intune tümleştirmesini etkinleştir** onay kutusunu temizleyin.

3. **Kaydet**’i seçin. JAMF Pro, yapılandırmanızı Intune 'a gönderir ve tümleştirme sonlandırılacak

4. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

5. Durumun şimdi **sonlandırıldığını**doğrulamak için **Kiracı Yönetimi** > **bağlayıcıları ve belirteçleri** > **iş ortağı cihaz yönetimi** ' ni seçin.

   > [!NOTE]
   > Kuruluşunuzun Mac cihazları konsolunda gösterilen tarihte (3 ay) kaldırılacaktır.

## <a name="get-support-for-the-cloud-connector"></a>Bulut bağlayıcısı için destek alın

Bulut bağlayıcısı, tümleştirme için gerekli olan Azure Kurumsal uygulamalarını otomatik olarak oluşturduğundan, destek için ilk iletişim noktası **JAMF**olmalıdır. Seçeneklere şunlar dahildir:

- E-posta desteği`support@jamf.com`
- JAMF 'de Destek portalını kullanın:https://www.jamf.com/support/ 


Desteğe başvurmadan önce:

- Kullandığınız bağlantı noktaları ve ürün sürümü gibi önkoşulları gözden geçirin.
- Azure 'da oluşturulan aşağıdaki iki JAMF Pro uygulaması için izinlerin değiştirilmediğini onaylayın. Uygulama izinlerinde yapılan değişiklikler Intune tarafından desteklenmez ve tümleştirmenin başarısız olmasına neden olabilir.

  **Bulut bağlayıcısı Kullanıcı kayıt uygulaması**:
  - API adı: Microsoft Graph
    - İzin: oturum açın ve kullanıcı profilini okuyun
    - Tür: temsilci
    - Verilen: yönetici onayı
    - Veren: bir yönetici

  **Bulut bağlayıcısı uygulaması**:
  - API adı: Microsoft Graph (örnek 1)
    - İzin: oturum açın ve kullanıcı profilini okuyun
    - Tür: temsilci
    - Verilen: yönetici onayı
    - Veren: bir yönetici

  - API adı: Microsoft Graph (örnek 2)
    - İzin: dizin verilerini okuma
    - Tür: uygulama
    - Verilen: yönetici onayı
    - Veren: bir yönetici

  - API adı: Intune API 'SI
    - İzin: cihaz özniteliğini Microsoft Intune gönder
    - Tür: uygulama
    - Verilen: yönetici onayı
    - Veren: bir yönetici

## <a name="common-questions-about-the-jamf-cloud-connector"></a>JAMF bulut Bağlayıcısı hakkında sık sorulan sorular

### <a name="what-data-is-shared-via-the-cloud-connector"></a>Bulut bağlayıcısı aracılığıyla hangi veriler paylaşılır?

Bulut bağlayıcısı Microsoft Azure kimliğini doğrular ve JAMF Pro 'dan Azure 'a cihaz envanter verileri gönderir. Ayrıca, bulut bağlayıcısı Azure 'da hizmet bulmayı, belirteç değişimini, iletişim hatalarını ve olağanüstü durum kurtarmayı yönetir.

### <a name="where-is-device-inventory-data-stored"></a>Cihaz envanteri verileri nerede depolanır?

Cihaz envanter verileri JAMF Pro veritabanında depolanır.

### <a name="what-credentials-are-stored"></a>Hangi kimlik bilgileri depolanıyor?

Depolanan kimlik bilgileri yok. Bulut bağlayıcısını yapılandırırken, yöneticilerin JAMF Multi-tenant uygulamasını ve yerel macOS bağlayıcı uygulamasını Azure AD kiracısına ekleme onayı gerekir. Çoklu kiracı uygulaması eklendikten sonra, bulut bağlayıcısı Azure API 'SI ile etkileşim kurmak için belirteçlere erişim ister. Erişimi kısıtlamak için herhangi bir zamanda uygulama erişimi Microsoft Azure iptal edilebilir.

### <a name="how-is-data-encrypted"></a>Veriler nasıl şifrelenir?

Bulut bağlayıcısı, JAMF Pro ve Microsoft Azure arasında gönderilen veriler için Aktarım Katmanı Güvenliği 'ni (TLS) kullanır.

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>JAMF hangi cihazı hangi JAMF Pro örneğiyle ilişkilendirildiğini nasıl bilir?

JAMF Pro, cihaz bilgilerini doğru örneğe doğru şekilde yönlendirmek için AWS 'deki mikro hizmetleri kullanır.

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>Bulut bağlayıcısını kullanarak el Ile bağlantı türüne geçiş yapabilir miyim?

Evet. Bağlantı türünü el ile olarak değiştirebilir ve el ile kurulum adımlarını izleyebilirsiniz. Sorularınız varsa, yardım için JAMF 'ye yönlendirilmelidir.

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>Gerekli uygulamalarda veya her ikisinde de izinler değiştirildi (*bulut bağlayıcısı* ve *bulut bağlayıcısı Kullanıcı kaydı uygulaması*) ve kayıt çalışmıyor, bu destekleniyor mu?

Uygulamalarda izinlerin değiştirilmesi desteklenmez.

## <a name="next-steps"></a>Sonraki adımlar

- [Jamf tarafından yönetilen cihazlar için uyumluluk ilkelerini uygula](../protect/conditional-access-assign-jamf.md)
- [Veri JAMF, Intune 'a gönderiyor](../protect/data-jamf-sends-to-intune.md)
