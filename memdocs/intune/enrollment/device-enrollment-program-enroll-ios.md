---
title: İOS/ıpados cihazlarını kaydetme-otomatik cihaz kaydı
titleSuffix: Microsoft Intune
description: Otomatik cihaz kaydını kullanarak şirkete ait iOS/ıpados cihazlarını kaydetmeyi öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96f6c2a40fa373c73aac30061ddaaaa1ddf0c8a6
ms.sourcegitcommit: 37dc6b78de8bb904b83a9d571f3c9f414b54f321
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90848411"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>iOS/iPadOS cihazlarını Apple’ın Otomatik Cihaz Kayıt Anlaşması ile otomatik olarak kaydetme

> [!IMPORTANT]
> Apple, Apple Aygıt Kayıt Programı (DEP) ile Apple otomatik cihaz kaydı (ADE) arasında son zamanlarda değiştirilmiştir. Intune, Intune kullanıcı arabirimini bunu yansıtacak şekilde güncelleştirme sürecinden oluşur. Bu değişiklikler tamamlanana kadar, Intune portalında *aygıt kayıt programı* görmeye devam edersiniz. Gösterildiği her yerde, artık otomatik cihaz kaydını kullanır.

Intune 'u Apple 'ın [otomatik cihaz kaydı (ade)](https://deploy.apple.com)aracılığıyla satın alınan IOS/ıpados cihazlarını kaydedecek şekilde ayarlayabilirsiniz. Otomatik cihaz kaydı, çok sayıda cihazı hiç dokunmadan kaydetmenizi sağlar. IPhone, iPads ve MacBooks gibi cihazlar doğrudan kullanıcılara sevk edilebilir. Kullanıcı cihazı açtığında, Apple ürünleri için tipik kullanıma hazır deneyimi içeren Kurulum Yardımcısı, önceden yapılandırılmış ayarlarla çalışır ve cihaz yönetime kaydolur.

ADE 'yi etkinleştirmek için hem Intune hem de [Apple Business Manager (ABı)](https://business.apple.com/) veya [Apple Okul Yöneticisi (asm)](https://school.apple.com/) portallarını kullanın. Intune 'a, Apple portalında yönetim için cihaz atayabilmeniz için seri numaralarının bir listesi veya bir satın alma siparişi numarası gereklidir. Intune 'da, kayıt sırasında cihazlara uygulanan ayarları içeren ADE kayıt profilleri oluşturabilirsiniz. ADE, bir [Cihaz Kayıt Yöneticisi](device-enrollment-manager-enroll.md) hesabıyla birlikte kullanılamaz.

> [!NOTE]
> ADE, son kullanıcı tarafından kaldırılması gerekmeyen cihaz yapılandırmasını ayarlar. Bu nedenle, [Ade 'ye](../fundamentals/migration-guide-considerations.md)geçmeden önce cihazın bir kullanıma hazır (yeni) duruma dönmesi için temizlenmiş olması gerekir.

## <a name="automated-device-enrollment-and-the-company-portal"></a>Otomatik cihaz kaydı ve Şirket Portalı

ADE kayıtları, Şirket Portalı uygulamasının App Store sürümü ile uyumlu değildir. Kullanıcılara bir ADE cihazında Şirket Portalı uygulamasına erişim izni verebilirsiniz. Kullanıcıların cihazındaki hangi kurumsal uygulamaları kullanmasını istediğini veya kayıt işlemini tamamlaması için modern kimlik doğrulamasını kullanmasını sağlamak üzere bu erişimi sağlamak isteyebilirsiniz. 

Kayıt sırasında modern kimlik doğrulamayı etkinleştirmek için, ADE profilinde VPP 'yi (toplu satın alma programı) **yükleme Şirket portalı** kullanarak uygulamayı cihaza gönderin. Daha fazla bilgi için bkz. [Apple Ade Ile iOS/ıpados cihazlarını otomatik olarak kaydetme](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

Şirket Portalı otomatik olarak güncelleştirilmesini ve Şirket Portalı uygulamayı ADE ile zaten kaydedilmiş cihazlara sağlamak için, [uygulama yapılandırma ilkesi](../apps/app-configuration-policies-use-ios.md) uygulanmış bir gerekli toplu satın alma programı (VPP) uygulaması olarak ıntune aracılığıyla şirket portalı uygulamasını dağıtın.

## <a name="what-is-supervised-mode"></a>Denetimli mod nedir?

Apple, iOS/ıpados 5 ' te Denetimli mod sunmuştur. Denetimli modda bulunan bir iOS/ıpados cihazı, engelleme ekranı yakalama ve App Store 'dan uygulama yüklemeyi engelleme gibi daha fazla denetim ile yönetilebilir. O neden bu mod, özellikle şirkete ait cihazlar için kullanışlıdır. Intune, cihazların, ADE 'nin bir parçası olarak Denetimli mod için yapılandırılmasını destekler.

İOS/ıpados 11 ' de denetimli ADE cihazları için destek kullanımdan kaldırılmıştır. İOS/ıpados 11 ve üzeri sürümlerde, ADE yapılandırılmış cihazların her zaman denetimli olması gerekir. ADE *is_supervised* bayrağı IOS/ıpados 13,0 ve üzeri ile yok sayılır. Sürüm 13,0 ve üzeri olan tüm iOS/ıpados cihazları otomatik cihaz kaydıyla kaydolduğunda otomatik olarak denetimli hale getirilebilir. 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Önkoşullar
- [Apple 'ıN Ade](https://deploy.apple.com) 'de satın alınan cihazlar
- [Mobil Cihaz Yönetimi (MDM) Yetkilisi](../fundamentals/mdm-authority-set.md)
- [Apple MDM anında Iletme sertifikası](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>Desteklenen birim

- Belirteç başına en fazla kayıt profili: 1.000  
- Profil başına maksimum otomatik cihaz kayıt cihazları: sınır yok (belirteç başına en fazla cihaz sayısı içinde)
- Intune hesabı başına en fazla otomatik cihaz kaydı belirteçleri: 2.000
- Belirteç başına en yüksek otomatik cihaz kayıt cihazları: ilk eşitlemede olan sınır 75000-80000 cihazlarıdır. Intune, her seferinde daha fazla cihaz eklemek için her 12 saat iadede ABM veya ASM ile eşitlemeye devam edecektir. El ile eşitleme (15 dakikada bir tetiklenebilir), Intune 'a başka bir cihaz toplu işi de ekler. Eşitlemeler gerçekleşmeye devam eder ve cihazlar, büyük miktarlarda Intune 'a kadar ABM/ASM ile eşitlenmiş olmaya devam edecektir. 

## <a name="get-an-apple-automated-device-enrollment-token"></a>Apple otomatik cihaz kaydı belirteci al

İOS/ıpados cihazlarını ADE ile kaydedebilmeniz için önce Apple 'dan bir ADE belirteci (. p7m) dosyası gerekir. Bu belirteç, Intune 'un kuruluşunuzun sahip olduğu ADE cihazları hakkında bilgi eşitlemesini sağlar. Ayrıca Intune'un kayıt profilini Apple'a yüklemesine ve cihazları bu profillere atamasına izin verir.

Bir belirteç oluşturmak için [Apple Business Manager (ABA)](https://business.apple.com/) veya [Apple Okul Yöneticisi (asm)](https://school.apple.com/) portalını kullanın. Ayrıca, yönetim için Intune 'a cihaz atamak üzere aba/ASM portalını de kullanabilirsiniz.

> [!NOTE]
> Azure 'a geçiş yapmadan önce klasik Intune portalından belirteç silerseniz, Intune silinen bir Apple ADE belirtecini geri yükleyebilir. ADE belirtecini Azure portal yeniden silebilirsiniz.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Adım 1. Belirteci oluşturmak için gereken Intune ortak anahtar sertifikasını indirin.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS/ıpados**  >  **iOS/ıpados kaydı**' nı seçin.

    ![Bir kayıt programı belirteci alın.](./media/device-enrollment-program-enroll-ios/ios-enroll.png)

2. **Kayıt programı belirteçleri**  >  **Ekle**' yi seçin.

3. **Onaylıyorum**’u seçerek Microsoft’un Apple’a kullanıcı ve cihaz bilgilerini göndermesine izin verin.

   > [!NOTE]
   > Intune ortak anahtar sertifikasını indirmek için adım 2 ' den sonra devam ederseniz, Sihirbazı kapatmayın veya bu sayfadan uzaklaşmayın. Bunun yapılması, indirdiğiniz sertifikayı geçersiz kılar ve bu işlemi tekrar yinelemeniz gerekir. Bu durumla karşılaşırsanız, genellikle **İnceleme ve oluşturma** sekmesindeki **Oluştur** düğmesinin gri olduğunu ve işlemi tamamlayamazsınız.

   ![Apple Sertifikaları çalışma alanındaki Kayıt Programı Belirteci panelinde bulunan ortak anahtarı indirme öğesinin ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

4. Şifreleme dosyasını (.pem) indirmek ve yerel olarak kaydetmek için **Ortak anahtarınızı indirin** öğesini seçin. .pem dosyası Apple portalından güven ilişkisi sertifikası istemek için kullanılır.


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Adım 2. Anahtarınızı kullanarak Apple’dan bir belirteç indirin.

1. Apple Business **Manager aracılığıyla bir belirteç oluştur** ' u seçin ve ŞIRKETINIZIN Apple kimliğiyle oturum açın. Bu Apple KIMLIĞINI, ADE belirtecinizi yenilemek için kullanabilirsiniz.
2. Apple [iş portalında](https://business.apple.com) **aygıt kayıt programı**için **kullanmaya başlayın** ' ı seçin.

3. **Sunucuları Yönet** sayfasında **MDM Sunucusu Ekle**’yi seçin.
4. **MDM Sunucu Adı**'nı girin ve ardından **İleri**'yi seçin. Sunucu adı, mobil cihaz yönetimi (MDM) sunucusunu tanımlarken kullanmanız içindir. Microsoft Intune sunucusunun adı veya URL'si değildir.

5. **Ekle &lt;ServerName&gt;** iletişim kutusu açılır ve **Ortak Anahtarınızı Yükleyin** ifadesi yazar. **Dosya Seç…** öğesini seçin. .pem dosyasını karşıya yükleyin ve ardından **İleri**'yi seçin.

6. **Dağıtım Programları** &gt; **Cihaz Kayıt Programı** &gt; **Cihazları Yönet**'e gidin.
7. **Cihazları Şuna Göre Seç:** öğesinin altında cihazların nasıl tanımlanacağını belirtin:
    - **Seri Numarası**
    - **Sipariş Numarası**
    - **CSV Dosyası Yükle**.

   ![Cihazları seri numarasına göre seçme, eylem seç öğesini Sunucuya ata olarak seçme ve sunucu adını seçme ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. **Eylem Seç** işlemi için **Sunucuya Ata**’yı ve Microsoft Intune için belirtilen &lt;ServerName&gt; öğesini belirleyip **Tamam**'ı seçin. Apple portalı, belirtilen cihazları Intune sunucusunda yönetilmek üzere bu sunucuya atar ve **Atama Tamamlandı** ifadesini görüntüler.

   Apple portalında **Dağıtım Programları** &gt; **Aygıt Kayıt Programı** &gt; **Atama Geçmişini Görüntüle**’ye giderek cihazların listesi ile MDM sunucu atamalarına göz atabilirsiniz.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>3. Adım Bu belirteci oluşturmak için kullanılan Apple kimliğini kaydedin.

[Microsoft Uç Nokta Yöneticisi Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), daha sonra başvurmak üzere Apple kimliğini sağlayın.

![Kayıt programı belirtecini oluşturmak için kullanılan Apple kimliğini belirtme ve kayıt programı belirtecine gözatma işleminin ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>4. Adım: Belirtecinizi karşıya yükleyin ve kapsam etiketlerini seçin.

1. **Apple Token** kutusunda, sertifika (. p7m) dosyasına gidin, **Aç**' ı seçin.
2. Bu DEP belirtecine [kapsam etiketi](../fundamentals/scope-tags.md) uygulamak istiyorsanız **Kapsam (etiketler)** öğesini ve ardından istediğiniz kapsam etiketlerini seçin. Belirtece uygulanan kapsam etiketleri, bu belirtece eklenen profiller ve cihazlar tarafından devralınır.
3. **Oluştur**' a tıklayın.

Anında iletme sertifikası ile Intune, ilkeyi kayıtlı mobil cihazlara ileterek iOS/ıpados cihazlarını kaydedebilir ve yönetebilir. Intune, kayıt programı hesabınızı görmek için Apple ile otomatik olarak eşitlenir.

## <a name="create-an-apple-enrollment-profile"></a>Apple kayıt profili oluşturma

Belirtecinizi yüklemişseniz, artık ADE cihazları için bir kayıt profili oluşturabilirsiniz. Bir cihaz kayıt profili, kayıt sırasında bir grup cihaza uygulanan ayarları tanımlar. ADE belirteci başına 100 kayıt profili sınırı vardır.

> [!NOTE]
> Bir VPP belirteci için yeterli Şirket Portalı lisansı yoksa veya belirtecin süresi dolmuşsa cihazlar engellenir. Belirtecin süresinin dolmasına az zaman kaldığında veya lisans sayısı azaldığında Intune'da bir uyarı görüntülenir.
 

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS/ıpados**  >  **iOS/ıpados kayıt**  >  **kayıt programı belirteçleri**' ni seçin.
2. Bir belirteç seçin, **profiller**  >  iOS**profili oluştur**  >  **iOS/ıpados**' ı seçin.

    ![Profil oluşturma ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/image04.png)

3. **Temel bilgiler** sayfasında, yönetim amaçları için profil Için bir **ad** ve **Açıklama** girin. Kullanıcılar bu ayrıntıları göremez. 

    ![Profil adı ve açıklaması.](./media/device-enrollment-program-enroll-ios/image05.png)

4. **İleri ' yi seçin: cihaz yönetimi ayarları**.

5. **Kullanıcı Benzeşimi** için bu profile sahip cihazların atanan kullanıcıyla mı yoksa atanan kullanıcı olmadan mı kaydedilmesi gerektiğini seçin.
    - **Kullanıcı Benzeşimi ile Kaydet** - Uygulamaları yükleme gibi hizmetler için Şirket Portalı’nı kullanmak isteyen kullanıcılara ait cihazlar için bu seçeneği seçin. ADFS kullanıyorsanız ve [WS-Trust 1,3 Kullanıcı adı/karma uç nokta](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) kimlik doğrulaması Için Kurulum Yardımcısı 'nı kullanıyorsanız [daha fazla bilgi edinin](/powershell/module/adfs/get-adfsendpoint?view=win10-ps) .

    - **Kullanıcı Benzeşimi Olmadan Kaydetme** - Tek bir kullanıcıyla bağlantılı olmayan cihazlar için bu seçeneği seçin. Yerel Kullanıcı verilerine erişolmayan cihazlar için bu seçeneği kullanın. Son kullanıcının iOS Şirket Portalı oturum açmasını ve kendilerini cihazın birincil kullanıcısı olarak kurmasını sağlamak için, `IntuneUDAUserlessDevice` anahtarı, yönetilen cihazlar için bir uygulama yapılandırma Ilkesinde ios Şirket portalı 'ye gönderin. Birincil kullanıcı olarak yalnızca ilk oturum açan kullanıcının kurulduğu unutulmamalıdır. İlk Kullanıcı oturumu kapattığında ve ikinci Kullanıcı oturum açarsa, ilk Kullanıcı cihazın birincil kullanıcısı olarak kalır. Daha fazla bilgi için bkz. [Şirket Portalı uygulamasını iOS ve ıpados DEP cihazlarını destekleyecek şekilde yapılandırma](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices). 

6. **Kullanıcı Benzeşimi ile Kaydet**’i seçerseniz, kullanıcıların Şirket Portalı yerine Apple Kurulum Yardımcısı ile kimlik doğrulama gerçekleştirmelerini sağlayabilirsiniz.

    ![Şirket Portalı ile kimlik doğrulayın.](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Aşağıdakilerden birini yapmak istiyorsanız, kullanıcıların **Şirket portalı** **kimlik doğrulaması gereken yeri seçin** ' i belirleyin.
    >    - çok faktörlü kimlik doğrulaması kullanma
    >    - ilk kez oturum açarken parolalarını değiştirmesi gereken kullanıcılara bunu bildirme
    >    - kayıt sırasında kullanıcılardan süresi dolmuş parolalarını sıfırlamalarını isteme
    >
    > Apple Kurulum Yardımcısı ile kimliği doğrularken bunlar desteklenmez.

7. **Kullanıcıların kimliğini doğrulamak**için **Şirket Portalı** seçtiyseniz, Şirket portalı cihaza otomatik olarak yüklemek için bir VPP belirteci kullanabilirsiniz. Bu durumda kullanıcının bir Apple Kimliği sağlamasına gerek kalmaz. VPP belirteciyle Şirket Portalı'nı yüklemek için, **VPP ile Şirket Portalı yükle**'nin altında bir belirteç seçin. Şirket Portalı VPP belirtecine zaten eklenmiş olmasını gerektirir. Şirket Portalı uygulamasının kayıt sonrasında güncellenmeye devam etmesini sağlamak için, Intune 'da (Intune>Istemci uygulamaları) bir uygulama dağıtımı yapılandırdığınızdan emin olun. Kullanıcı etkileşimi gerekli olmadığı için, büyük olasılıkla bir iOS/ıpados VPP uygulaması olarak Şirket Portalı olması, gerekli bir uygulamayı yapmanız ve atama için cihaz lisansını kullanmanız gerekecektir. Belirtecin süresinin dolmadığından ve Şirket Portalı uygulaması için yeterli cihaz lisansınız olduğundan emin olun. Belirtecin süresi dolarsa veya yeterli lisans yoksa, Intune bunun yerine App Store Şirket Portalı’nı yükler ve Apple Kimliği ister. 

    > [!NOTE]
    > **Kullanıcıların kimlik doğrulaması yapması gereken yeri seçin** **Şirket portalı**, cihaz kayıt IŞLEMININ, Şirket portalının Ade cihaza indirilmekte olan ilk 24 saat içinde gerçekleştirildiğinden emin olun. Aksi takdirde kayıt başarısız olabilir ve cihazı kaydetmek için bir fabrika sıfırlaması gerekecektir.
    
    ![VPP ile şirket portalı yükle ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

8. **Kullanıcıların kimlik doğrulaması yapması gereken yeri seç**Için **Kurulum Yardımcısı** ' nı seçtiyseniz, ancak aynı zamanda koşullu erişimi kullanmak veya cihazlarda şirket uygulamaları dağıtmak istiyorsanız, Şirket portalı cihazlara yüklenmelidir. Bunu yapmak için, **Şirket portalı yüklemek**için **Evet** ' i seçin.  Kullanıcıların uygulama mağazasındaki kimlik doğrulaması yapmadan Şirket Portalı almasını istiyorsanız, **VPP ile şirket portalı yüklemeyi** seçin ve bir VPP belirteci seçin. Belirtecin kullanım süreleri dolana ve Şirket Portalı uygulamasının doğru bir şekilde dağıtılması için yeterli cihaz lisansına sahip olduğunuzdan emin olun.

9. **Şirket Portalı’nı VPP ile yükle** seçeneği için bir belirteç seçtiyseniz Kurulum Yardımcısı tamamlandıktan hemen sonra cihazı Tekli Uygulama Moduna (yani Şirket Portalı uygulaması için) kilitleyebilirsiniz. Bunun için **Kimlik doğrulaması tamamlanana kadar Şirket Portalı’nı Tekli Uygulama Modunda çalıştır** ayarını **Evet** olarak ayarlayın. Cihazı kullanmak için kullanıcının önce Şirket Portalı’nda oturum açarak kimliğini doğrulaması gerekir.

    Multi-Factor Authentication tek bir uygulama modunda kilitlenmiş tek bir cihazda desteklenmez. Bu sınırlama, cihazın ikinci kimlik doğrulama faktörünü tamamlaması için farklı bir uygulamaya geçiş yaptığından oluşur. Bu nedenle, tek bir App Mode cihazında çok faktörlü kimlik doğrulaması istiyorsanız ikinci faktör farklı bir cihazda olmalıdır.

    Bu özellik yalnızca iOS/ıpados 11.3.1 ve üzeri sürümlerde desteklenir.

   ![Tek uygulama modunun ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

10. Bu profili kullanan cihazların denetimli olmasını istiyorsanız, **denetimli**için **Evet** ' i seçin.

    ![Cihaz Yönetimi Ayarları ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    **Denetimli** cihazlar, varsayılan olarak size daha fazla yönetim seçeneği verir ve Etkinleştirme Kilidi’ni devre dışı bırakır. Microsoft, özellikle çok sayıda iOS/ıpados cihazı dağıtıyorsanız, denetimli modu etkinleştirme mekanizması olarak ADE kullanılmasını önerir. Iş için Apple paylaşılan iPad cihazlarının denetimli olması gerekir.

    Kullanıcılara cihazlarının denetimli olduğu iki yolla bildirilir:

   - Kilit ekranında “Bu iPhone, Contoso tarafından yönetilmektedir.” yazar.
   - **Ayarlar**  >  **genel**  >  **hakkında** ekranı şöyle diyor: "Bu iPhone denetimli. ifadesi ve

     > [!NOTE]
     > Denetim olmadan kaydedilen bir cihaz, yalnızca Apple Configurator kullanılarak sıfırlanıp denetimli yapılabilir. Bu şekilde cihazın sıfırlanması, bir iOS/ıpados cihazının USB kablosuyla bir Mac 'e bağlanmasını gerektirir. Bu konu hakkında daha fazla bilgi için [Apple Configurator belgelerine](http://help.apple.com/configurator/mac/2.3) bakın.

11. Bu profili kullanan cihazlarda kilitli kayıt isteyip istemediğinizi seçin. **Kilitli kayıt** , yönetim profilinin **Ayarlar** menüsünden kaldırılmasına Izin veren iOS/ıpados ayarlarını devre dışı bırakır. Cihazı kaydettikten sonra cihazı silmeden bu ayarı değiştiremezsiniz. Bu cihazlarda **Denetimli** Yönetim Modu *Evet* olarak ayarlı olmalıdır. 

    > [!NOTE]
    > Cihaz, **kilitli kayıt**ile kaydedildikten sonra, Şirket portalı uygulamasında, kullanıcılar **cihaz kaldırma** veya **fabrika sıfırlama** 'yı kullanamaz. Seçenekler Kullanıcı tarafından kullanılamaz. Kullanıcı da Şirket Portalı Web sitesinde ( https://portal.manage.microsoft.com) .
    > Ayrıca, bir KCG cihazı Apple otomatik cihaz kayıt cihazına dönüştürülürse ve **kilitli bir kayıt** etkin profille kaydedildiyse, kullanıcının **cihaz kaldırma** ve **fabrika sıfırlamasını** 30 gün sonra kullanmasına izin verilir ve sonra seçenekler devre dışı bırakılır veya kullanılamaz. Başvuru: https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859 .

12. **Kullanıcı benzeşimi olmadan kaydet** ' **i ve yukarıda denetimli '** ı seçtiyseniz, cihazların [Iş cihazları için Apple paylaşılan iPad](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web)olarak yapılandırıp yapılandırmamaya karar vermelisiniz. **Paylaşılan iPad**için **Evet** ' i seçerek birden çok kullanıcı aynı cihazda oturum açabiliyor. Kullanıcılar, yönetilen Apple KIMLIĞI ve federal kimlik doğrulama hesaplarıyla veya geçici bir oturum (konuk hesabı) aracılığıyla kimlik doğrulaması yapacak. Bu seçenek iOS/ıpados 13,4 veya üstünü gerektirir.

    Cihazlarınızı Iş cihazları için Apple paylaşılan iPad olacak şekilde yapılandırmayı seçerseniz, **en yüksek önbelleğe alınmış kullanıcıları**ayarlamanız gerekir. Bu değeri, paylaşılan iPad 'i kullanmayı düşündüğünüz kullanıcı sayısına ayarlayın. 32 GB veya 64 GB 'lik bir cihazda en fazla 24 Kullanıcı önbelleğe alabilirsiniz. Çok düşük bir sayı seçerseniz, oturum açma işleminden sonra kullanıcının verilerinin cihaza gelmesi biraz zaman alabilir. Çok yüksek bir sayı seçerseniz, kullanıcılarınız yeterli disk alanına sahip olmayabilir.  

    > [!NOTE]
    > Iş için Apple paylaşılan iPad 'i ayarlamak istiyorsanız aşağıdakileri ayarlayın: 
    > - **Kullanıcı benzeşimi**  =  **Kullanıcı benzeşimi olmadan kaydolun**. 
    > - **Denetimli**  =  **Evet**. 
    > - **Paylaşılan iPad** = * * Yes * *.
    > Geçici oturumlar varsayılan olarak etkindir ve kullanıcılarınızın yönetilen bir Apple KIMLIĞI hesabı olmadan paylaşılan iPad 'de oturum açmasına olanak tanır. İOS/ıpados paylaşılan iPad [cihaz kısıtlama ayarlarını](../configuration/device-restrictions-ios.md)yapılandırarak paylaşılan iPad üzerinde geçici oturumları devre dışı bırakabilirsiniz.  

13. Bu profili kullanan cihazların **Bilgisayarlarla eşitleme** imkanının olup olmayacağını seçin. **Sertifikaya göre Apple Configurator’a izin ver**’i seçerseniz, **Apple Configurator Sertifikaları**’nın altında bir sertifika seçmeniz gerekir. İOS/ıpados 13,0 ve üzeri için, bu ayar Apple tarafından kullanımdan kaldırılmıştır. 

     > [!NOTE]
     > **Bilgisayarlarla eşitleme** , **Tümünü Reddet**olarak ayarlandıysa, bağlantı noktası iOS ve ıpados cihazlarında sınırlı olur. Bağlantı noktası yalnızca dolduruluyor ve başka hiçbir şey için kullanılabilir. Bağlantı noktasının iTunes veya Apple Configurator 2 kullanılması engellenir.
     **Bilgisayarlarla eşitleme** , **sertifikaya göre Apple Configurator 'a izin ver**olarak ayarlandıysa, daha sonra erişebileceğiniz bir sertifikanın yerel kopyasına sahip olduğunuzdan emin olun. Karşıya yüklenen kopyada değişiklik yapamazsınız ve bu sertifikanın gelecekte erişilebilir olması için saklanması önemlidir. Bir macOS cihazından veya BILGISAYARDAN iOS/ıpados cihazına bağlanmak için, bu yapılandırma ve sertifikayla otomatik cihaz kayıt profiline kaydedilmiş iOS/ıpados cihazından bağlantı kuran cihazda aynı sertifikanın yüklü olması gerekir.

14. Önceki adımda **Sertifikaya göre Apple Configurator’a izin ver**’i seçtiyseniz içeri aktaracak bir Apple Configurator Sertifikası seçin.

15. Her bir arka arkaya iade edildiğinde otomatik olarak uygulanan cihazlar için bir adlandırma biçimi belirtebilirsiniz. Adlandırma şablonu oluşturmak için **Cihaz adı şablonu uygula** bölümünde **Evet**'i seçin. Ardından **Cihaz Adı Şablonu**'na bu profili kullanan cihazlar için kullanılacak şablonu girin. Cihaz türünü ve seri numarasını içeren bir şablon biçimi belirtebilirsiniz. Cihaz adı şablonu iPhone, iPad ve iPod Touch desteği içerir. 
16. **İleri ' yi seçin: Kurulum Yardımcısı özelleştirmesi**.

17. **Kurulum Yardımcısı özelleştirmesi** sayfasında, aşağıdaki profil ayarlarını yapılandırın: ![ Kurulum Yardımcısı özelleştirmesi.](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)


    | Departman ayarları | Açıklama |
    |---|---|
    | <strong>Bölüm Adı</strong> | Kullanıcı, etkinleştirme sırasında <strong>Yapılandırma Hakkında</strong> öğesine dokunduğunda görüntülenir. |
    |    <strong>Departman Telefonu</strong>     | Kullanıcı, etkinleştirme sırasında <strong>Yardım Gerekli</strong> düğmesine dokunduğunda görüntülenir. |

    Kullanıcı kurulum işlemleri sırasında cihazda Kurulum Yardımcısı ekranlarının gizlenmesini tercih edebilirsiniz.
    - **Gizle**'yi seçerseniz, kurulum sırasında ekran görüntülenmez. Cihaz kurulumu yapıldıktan sonra, kullanıcı yine **Ayarlar** menüsüne gidip özelliği ayarlayabilir.
    - **Göster**'i seçerseniz, kurulum sırasında ekran görüntülenir. Kullanıcı bazen hiçbir eylem yapmadan ekranı atlayabilir. Ama daha sonra cihazın **Ayarlar** menüsüne gidebilir ve özelliği ayarlayabilir. 


    | Kurulum Yardımcısı ekran ayarları | **Göster**'i seçerseniz, kurulum sırasında cihaz... |
    |------------------------------------------|------------------------------------------|
    | <strong>Geçiş kodu</strong> | Kullanıcıdan geçiş kodu ister. Güvenliği sağlanmayan veya erişim denetimi başka bir yolla (cihazı tek uygulamayla sınırlandıran bilgi noktası modu gibi) sağlanan cihazlar için her zaman geçiş kodu isteyin. İOS/ıpados 7,0 ve üzeri için. |
    | <strong>Konum Hizmetleri</strong> | Kullanıcıdan konum ister. MacOS 10,11 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Geri yükleme</strong> | Uygulamalar & veri ekranını görüntüleyin. Bu ekran kullanıcıya cihazı kurarken iCloud Backup'tan verileri geri yükleme veya aktarma seçeneği sağlar. MacOS 10,9 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>iCloud ve Apple Kimliği</strong> | Kullanıcıya Apple Kimliği ile oturum açma ve iCloud'u kullanma seçenekleri sağlar. MacOS 10,9 ve üzeri ve iOS/ıpados 7,0 ve üzeri için.   |
    | <strong>Hüküm ve Koşullar</strong> | Kullanıcının Apple'ın hüküm ve koşullarını kabul etmesini gerektirir. MacOS 10,9 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Touch ID</strong> | Kullanıcıya cihaz için parmak izi tanımlama özelliğini ayarlama seçeneği sağlar. MacOS 10.12.4 ve üzeri ve iOS/ıpados 8,1 ve üzeri için. |
    | <strong>Apple Pay</strong> | Kullanıcıya cihazda Apple Pay ayarlama seçeneği sağlar. MacOS 10.12.4 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Zoom</strong> | Kullanıcıya cihazı ayarlarken ekranı yakınlaştırma seçeneği sağlar. İOS/ıpados 8,3 ve üzeri için. |
    | <strong>Siri</strong> | Kullanıcıya Siri'yi ayarlama seçeneği sağlar. MacOS 10,12 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Tanılama Verileri</strong> | Kullanıcıya Tanılama ekranını görüntüler. Bu ekran kullanıcıya Apple'a tanılama verileri gönderme seçeneği sağlar. MacOS 10,9 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Görüntü Tonu</strong> | Kullanıcıya Görüntü Tonunu açma seçeneği sunar. MacOS 10.13.6 ve üzeri ve iOS/ıpados 9.3.2 ve üzeri için. |
    | <strong>Gizlilik</strong> | Kullanıcıya Gizlilik ekranını gösterir. MacOS 10.13.4 ve üzeri ve iOS/ıpados 11,3 ve üzeri için. |
    | <strong>Android Geçişi</strong> | Kullanıcıya Android cihazdan veri geçirme seçeneği sunar. İOS/ıpados 9,0 ve üzeri için.|
    | <strong>iMessage ve FaceTime</strong> | Kullanıcıya IMessage ve çok yönlü saat ayarlama seçeneği sunun. İOS/ıpados 9,0 ve üzeri için. |
    | <strong>Ekleme</strong> | Kapak Sayfası, Çok Görevli Çalışma ve Denetim Merkezi gibi kullanıcı eğitimine yönelik ekleme bilgi ekranlarının görüntülenmesini sağlar. İOS/ıpados 11,0 ve üzeri için. |
    | <strong>Watch Geçişi</strong> | Kullanıcıya Watch cihazından veri geçirme seçeneği sunar. İOS/ıpados 11,0 ve üzeri için.|
    | <strong>Ekran Süresi</strong> | Ekran Süresi ekranını görüntüler. MacOS 10,15 ve üzeri ve iOS/ıpados 12,0 ve üzeri için. |
    | <strong>Yazılım Güncelleştirmesi</strong> | Zorunlu yazılım güncelleştirmesi ekranı görüntüler. İOS/ıpados 12,0 ve üzeri için. |
    | <strong>SIM Ayarları</strong> | Kullanıcıya hücresel plan ekleme seçeneği sunar. İOS/ıpados 12,0 ve üzeri için. |
    | <strong>Görünüm</strong> | Kullanıcıya Görünüm ekranını gösterir. MacOS 10,14 ve üzeri ve iOS/ıpados 13,0 ve üzeri için. |
    | <strong>Hızlı dil</strong>| Kullanıcı için hızlı dil ekranını görüntüleyin. |
    | <strong>Tercih edilen dil</strong> | Kullanıcıya  **tercih edilen dilini**seçme seçeneğini sunun. |
    | <strong>Cihazdan cihaza geçişe</strong> | Kullanıcıya verileri eski cihazlarından bu cihaza geçirme seçeneğini sunun. İOS/ıpados 13,0 ve üzeri için. |
    | <strong>Kaydını</strong> | Kullanıcının kayıt ekranını görüntüleyin. MacOS 10,9 ve üzeri için. |
    | <strong>FileVault</strong> | Kullanıcının dosya Kasası 2 şifreleme ekranını görüntüleyin. MacOS 10,10 ve üzeri için. |
    | <strong>iCloud tanılama</strong> | Kullanıcıya iCloud Analytics ekranını görüntüleyin. MacOS 10.12.4 ve üzeri için. |
    | <strong>iCloud Depolama</strong> | Kullanıcıya iCloud belgelerini ve masaüstü ekranını görüntüleyin. MacOS 10.13.4 ve üzeri için. |
    

18. **İleri ' yi** seçerek **gözden geçir + oluştur** sayfasına gidin.

19. Profili kaydetmek için **Oluştur**’u seçin.

### <a name="dynamic-groups-in-azure-active-directory"></a>Azure Active Directory içindeki dinamik gruplar

Azure Active Directory içinde dinamik bir grup oluşturmak için kayıt **adı** alanını kullanabilirsiniz. Daha fazla bilgi için bkz. [dinamik grupları Azure Active Directory](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

Bu kayıt profiliyle cihazları atamak için [Kayıtlıprofilename parametresini](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) tanımlamak üzere profil adını kullanabilirsiniz.

Kullanıcı benzeşimi olan ADE cihazlarda en hızlı ilke teslimi için, kaydolan kullanıcının bir AAD Kullanıcı grubunun cihaz kurulumundan önce bir üye olduğundan emin olun. 

Kayıt profillerine dinamik gruplar atamak, kayıt sonrasında cihazlara uygulama ve ilke sunarken bir gecikmeye neden olabilir.


## <a name="sync-managed-devices"></a>Yönetilen cihazları eşitleme
Artık Intune’a cihazlarınızı yönetme izni verildiğine göre, yönetilen cihazlarınızı Intune’da Azure portalında görmek için Intune’u Apple ile eşitleyebilirsiniz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS/ıpados**  >  **iOS/ıpados kayıt**  >  **kayıt programı belirteçleri**' ni seçin.

2. Cihaz eşitleme > listede bir belirteç seçin **Devices** > **Sync**. ![ Kayıt programı cihazları düğümünün ve eşitleme bağlantısının ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/image06.png)

   Intune 'un kabul edilebilir kayıt programı trafiğine yönelik koşullarını izlemek için aşağıdaki kısıtlamaları uygular:
   - Tam eşitleme en sık yedi günde bir çalıştırılabilir. Tam eşitleme sırasında Intune, Intune’a bağlı Apple MDM sunucusuna atanan seri numaraların tam güncelleştirilmiş bir listesini alır. Bir ADE cihazı Intune portalından silinirse, bu, ADE portalındaki Apple MDM sunucusundan atanmamış olmalıdır. Atamanın kaldırılmaması durumunda bu cihazlar tam eşitleme çalıştırılana kadar Intune'a yeniden aktarılamaz.   
   - Her 12 saatte bir eşitleme otomatik olarak çalıştırılır. **Eşitle** düğmesine basarak da eşitleyebilirsiniz (en fazla 15 dakikada bir kez). Tüm eşitleme isteklerinin tamamlanması için 15 dakika verilir. Eşitleme tamamlanana kadar **Eşitle** düğmesi devre dışı kalır. Bu eşitleme, mevcut aygıt durumunu yeniler ve Apple MDM sunucusuna atanan yeni cihazları içeri aktarır.   


## <a name="assign-an-enrollment-profile-to-devices"></a>Cihazlara kayıt profili atama
Cihazların kaydedilmesi için bunlara bir kayıt programı profili atamalısınız.

>[!NOTE]
>Ayrıca, **Apple Seri Numaraları** dikey penceresinde profillere seri numaralar da atayabilirsiniz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS/ıpados**  >  **iOS/ıpados kayıt**  >  **kayıt programı belirteçleri** ' ni seçin > listeden bir belirteç seçin.
2. **Cihazlar** > listeden cihazları seçin > **Profil ata**’yı seçin.
3. **Profil ata**'nın altında cihazlar için bir profil seçin > **Ata**’ya tıklayın.

### <a name="assign-a-default-profile"></a>Varsayılan bir profil atama

Belirli bir belirteç ile kaydedilen tüm cihazlara uygulanacak varsayılan bir profil seçebilirsiniz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS/ıpados**  >  **iOS/ıpados kayıt**  >  **kayıt programı belirteçleri** ' ni seçin > listeden bir belirteç seçin.
2. **Varsayılan Profil Ayarla**’yı seçin, açılan listeden bir profil seçin ve daha sonra **Kaydet**’e tıklayın. Profil, bu belirteçle kaydedilen tüm cihazlara uygulanacaktır.

## <a name="distribute-devices"></a>Cihazları dağıtma
Apple ve Intune arasında yönetimi ve eşitlemeyi etkinleştirdiniz ve ADE cihazlarınızın kaydolmasına izin vermek için bir profil atadınız. Artık cihazları kullanıcılara dağıtabilirsiniz. Kullanıcı benzeşimli cihazlar, her kullanıcıya bir Intune lisansı atanmasını gerektirir. Kullanıcı benzeşimi olmayan cihazlar, cihaz lisansı gerektirir. Etkinleştirilmiş bir cihaz, silinene kadar bir kayıt profili uygulayamaz.

Bkz. [aygıt kayıt programı iOS/ıpados cihazınızı Intune 'A kaydetme](../user-help/enroll-your-device-dep-ios.md).

## <a name="renew-an-automated-device-enrollment-token"></a>Otomatik cihaz kayıt belirtecini yenileme  

> [!NOTE]
> ADE belirtecinizi yıllık olarak yenilemeye ek olarak, Apple Business Manager 'da belirtecini kuran kullanıcı için yönetilen Apple KIMLIĞI parolası değiştiğinde veya Apple Business Manager kuruluşunuzu terk ettiğinde, kayıt programı belirtecinizi Intune ve Apple Business Manager içinde yenilemeniz gerekir.

1. Business.apple.com adresine gidin.
2. **Ayarlar** ' a tıklayın (alt sol)
3.  **MDM sunucuları**' nın altında, YENILEMEK istediğiniz Ade/DEP BELIRTECIYLE ilişkili MDM sunucunuzu seçin.
4. **Belirteç yükle**' ye tıklayın.

    ![Yeni belirteç oluşturma ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

5. İstemde "sunucu belirtecini Indir" i seçin
> [!NOTE]
> **"Sunucu belirtecini indir"** seçeneğini tıklamayın, komut isteminde bahsedildiği gibi belirteci yenilemek için bu Işlem, Intune tarafından kullanılmakta olan belirteci (veya bu konuyla ilgili başka bir MDM çözümü) geçersiz kılar. Belirteci zaten indirdiyseniz, belirteç yenilenene kadar sonraki adımlara devam ettiğinizden emin olun.

6. Belirteci indirdikten sonra, [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) **cihazlar**  >  **iOS/ıpados**  >  **iOS/ıpados kayıt**  >  **kayıt programı belirteçleri** ' ni seçin > belirteci seçin.
    ![Kayıt programı belirteçlerinin ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

7. **Belirteci Yenile** ' yi seçin ve özgün belirteci oluşturmak Için kullanılan Apple kimliğini girin (otomatik olarak doldurulmamışsa).  
    ![Yeni belirteç oluşturma ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/renewtoken.png)

8. Yeni indirilen belirteci karşıya yükleyin.

9. **İleri ' yi** seçerek **kapsam etiketleri** sayfasına gidin ve isterseniz kapsam etiketleri atayın.

10. **Belirteci yenile**’yi seçin. Belirtecin yenilendiğine dair onayı görürsünüz.   
    ![Onay ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-automated-device-enrollment-token-from-intune"></a>Intune 'dan otomatik cihaz kayıt belirtecini silme

Kayıt profili belirteçlerini Intune 'dan olduğu sürece silebilirsiniz.
- belirtece hiçbir cihaz atanmadı
- varsayılan profile hiçbir cihaz atanmadı

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **iOS/MacOS**  >  **iOS/MacOS kaydı**  >  **kayıt programı belirteçleri** ' ni seçin > belirteci > **cihazları**seçin.
2. Belirtece atanan tüm cihazları silin.
3. **Cihazlar**  >  **iOS/MacOS**  >  **iOS/MacOS kayıt**  >  **kayıt programı belirteçleri** ' ne gidin > belirteç > **profilleri**' ni seçin.
4. Varsayılan bir profil varsa, silin.
5. Cihazlara git **Devices**  >  **iOS/MacOS**  >  **iOS/MacOS kayıt**  >  **programı belirteçleri** > > **Sil**belirtecini seçin.
