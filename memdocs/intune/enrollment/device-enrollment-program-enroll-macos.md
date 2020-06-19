---
title: MacOS cihazlarını kaydetme-Apple Business Manager veya Apple Okul Yöneticisi
titleSuffix: ''
description: Şirkete ait macOS cihazlarını nasıl kaydedeceğinizi öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/06/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: bfcc4a8e867041e0053697bbee605f9798e45bec
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093927"
---
# <a name="automatically-enroll-macos-devices-with-the-apple-business-manager-or-apple-school-manager"></a>MacOS cihazlarını Apple Business Manager veya Apple Okul Yöneticisi ile otomatik olarak kaydetme

> [!IMPORTANT]
> Apple, Apple Aygıt Kayıt Programı (DEP) ile Apple otomatik cihaz kaydı (ADE) arasında son zamanlarda değiştirilmiştir. Intune, Intune kullanıcı arabirimini bunu yansıtacak şekilde güncelleştirme sürecinden oluşur. Bu değişiklikler tamamlanana kadar, Intune portalında *aygıt kayıt programı* görmeye devam edersiniz. Gösterildiği her yerde, artık otomatik cihaz kaydını kullanır.

Apple [Apple Business Manager](https://business.apple.com/) veya [Apple Okul Yöneticisi](https://school.apple.com/)aracılığıyla satın alınan MacOS cihazları için Intune kaydını ayarlayabilirsiniz. Bu kayıtlardan birini kullanarak cihazlara hiç dokunmadan çok sayıda cihazı ayarlayabilirsiniz. macOS cihazlarını doğrudan kullanıcılara gönderebilirsiniz. Kullanıcı cihazı açtığında, önceden yapılandırılmış ayarları ile Kurulum Yardımcısı çalıştırılır ve cihaz Intune yönetimine kaydedilir.

Kaydı ayarlamak için hem Intune hem de Apple portallarını kullanırsınız. Kayıt sırasında cihazlara uygulanan ayarları içeren kayıt profilleri oluşturun.

Apple Business Manager kaydı veya Apple Okul Yöneticisi, [cihaz kayıt yöneticisiyle](device-enrollment-manager-enroll.md)birlikte çalışır.

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Ön koşullar

- [Apple Okul Yöneticisi](https://school.apple.com/) veya [Apple 'ın otomatik cihaz kaydında](http://deploy.apple.com) satın alınan cihazlar
- Seri numarası listesi veya satın alma sipariş numarası.
- [MDM yetkilisi](../fundamentals/mdm-authority-set.md)
- [Apple MDM anında Iletme sertifikası](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-ade-token"></a>Apple ADE belirteci al

MacOS cihazlarını ADE veya Apple Okul Yöneticisi ile kaydedebilmek için Apple 'dan bir belirteç (. p7m) dosyası gerekir. Bu belirteç, Intune'un kuruluşunuza ait olan cihazlar hakkındaki bilgileri eşitlemesini sağlar. Ayrıca Intune'un kayıt profillerini Apple’a yüklemesini ve bu profilleri cihazlara atamasını da sağlar.

Belirteci oluşturmak için Apple portalını kullanabilirsiniz. Cihazları yönetim için Intune’a atamak için de Apple portalını kullanabilirsiniz.

> [!NOTE]
> Belirteci Azure’a geçirmeden önce klasik Intune portalında silerseniz Intune, silinen bir Apple belirtecini geri yükleyebilir. Belirteci Azure portalından tekrar silebilirsiniz.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Adım 1. Belirteci oluşturmak için gereken Intune ortak anahtar sertifikasını indirin

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **MacOS**  >  **MacOS kaydı**' nı seçin. 
> **Kayıt programı belirteçleri**  >  **Ekleyin**.

    ![Get an enrollment program token.](./media/device-enrollment-program-enroll-macos/image01.png)

2. **Onaylıyorum**’u seçerek Microsoft’un Apple’a kullanıcı ve cihaz bilgilerini göndermesine izin verin.

   ![Apple Sertifikaları çalışma alanındaki Kayıt Programı Belirteci panelinde bulunan ortak anahtarı indirme öğesinin ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. Şifreleme dosyasını (.pem) indirmek ve yerel olarak kaydetmek için **Ortak anahtarınızı indirin** öğesini seçin. .pem dosyası Apple portalından güven ilişkisi sertifikası istemek için kullanılır.

### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Adım 2. Apple 'dan bir belirteç indirmek için anahtarınızı kullanın

1. Apple **Business Manager aracılığıyla bir belirteç oluştur** ' u seçin veya **Apple Okul Yöneticisi 'ni kullanarak bir belirteç oluşturun** ve uygun Apple portalını açın ve şirketinizin Apple kimliğiyle oturum açın. Belirtecinizi yenilemek için de bu Apple kimliğini kullanabilirsiniz.
2. DEP için Apple portalında **Kullanmaya Başlayın**, **Aygıt Kayıt Programı** > **Sunucuları Yönet** > **MDM Sunucusu Ekle** yolunu izleyin.
3. Apple Okul yönetimi için, Apple portalında **MDM sunucuları**  >  **MDM sunucusu Ekle**' yi seçin.
4. **MDM Sunucu Adı**'nı girin ve ardından **İleri**'yi seçin. Sunucu adı, mobil cihaz yönetimi (MDM) sunucusunu tanımlarken kullanmanız içindir. Microsoft Intune sunucusunun adı veya URL'si değildir.

5. **Ekle &lt;ServerName&gt;** iletişim kutusu açılır ve **Ortak Anahtarınızı Yükleyin** ifadesi yazar. **Dosya Seç…** öğesini seçin. .pem dosyasını karşıya yükleyin ve ardından **İleri**'yi seçin.

6. **Dağıtım Programları** &gt; **Cihaz Kayıt Programı** &gt; **Cihazları Yönet**'e gidin.
7. **Cihazları Şuna Göre Seç:** öğesinin altında cihazların nasıl tanımlanacağını belirtin:
    - **Seri Numarası**
    - **Sipariş Numarası**
    - **CSV Dosyası Yükle**.

   ![Cihazları seri numarasına göre seçme, eylem seç öğesini Sunucuya ata olarak seçme ve sunucu adını seçme ekran görüntüsü.](./media/device-enrollment-program-enroll-macos/enrollment-program-token-specify-serial.png)

8. **Eylem Seç** işlemi için **Sunucuya Ata**’yı ve Microsoft Intune için belirtilen &lt;ServerName&gt; öğesini belirleyip **Tamam**'ı seçin. Apple portalı, belirtilen cihazları Intune sunucusunda yönetilmek üzere bu sunucuya atar ve **Atama Tamamlandı** ifadesini görüntüler.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>3. Adım Bu belirteci oluşturmak için kullanılan Apple kimliğini kaydedin

[Microsoft Uç Nokta Yöneticisi Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), daha sonra başvurmak üzere Apple kimliğini sağlayın.

![Kayıt programı belirtecini oluşturmak için kullanılan Apple kimliğini belirtme ve kayıt programı belirtecine gözatma işleminin ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token"></a>4. Adım. Belirtecinizi karşıya yükleme
**Apple belirteci** kutusunda sertifika (.pem) dosyasına gözatın, **Aç**’ı ve daha sonra **Oluştur**’u seçin. Anında iletme sertifikasıyla, Intune ilkeyi kayıtlı cihazlara ileterek macOS cihazlarını kaydedebilir ve yönetebilir. Intune, kayıt programı hesabınızı görmek için Apple ile otomatik olarak eşitlenir.

## <a name="create-an-apple-enrollment-profile"></a>Apple kayıt profili oluşturma

Belirtecinizi yüklediğinize göre, cihazlar için kayıt profili oluşturabilirsiniz. Bir cihaz kayıt profili, kayıt sırasında bir grup cihaza uygulanan ayarları tanımlar.

1. [Microsoft Uç Nokta Yöneticisi Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **cihazlar**  >  **MacOS**  >  **MacOS kaydı**  >  **kayıt programı belirteçleri**' ni seçin.
2. Bir belirteç seçin, **Profiller**’e ve daha sonra **Profil oluştur**’a tıklayın.

    ![Profil oluşturma ekran görüntüsü.](./media/device-enrollment-program-enroll-macos/image04.png)

3. **Temel bilgiler** sayfasında, yönetim amaçları için profil Için bir **ad** ve **Açıklama** girin. Kullanıcılar bu ayrıntıları göremez. Azure Active Directory’de dinamik bir grup oluşturmak için **Ad** alanını kullanabilirsiniz. enrollmentProfileName parametresini, bu kayıt profiliyle cihazlara atamak amacıyla tanımlamak için profil adını kullanın. [Azure Active Directory dinamik grupları](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) hakkında daha fazla bilgi edinin.

    ![Profil adı ve açıklaması.](./media/device-enrollment-program-enroll-macos/createprofile.png)

4. **Platform** olarak **macOS** seçin.

5. **İleri ' yi** seçerek **yönetim ayarları** sayfasına gidin.

6. **Kullanıcı Benzeşimi** için bu profile sahip cihazların atanan kullanıcıyla mı yoksa atanan kullanıcı olmadan mı kaydedilmesi gerektiğini seçin.
    - **Kullanıcı Benzeşimi ile kaydet** - Uygulamaları yükleme gibi hizmetler için Şirket Portalı uygulamasını kullanmak isteyen kullanıcılara ait cihazlar için bu seçeneği belirtin. ADFS kullanılıyorsa kullanıcı benzeşimi, [WS-Trust 1.3 Kullanıcı adı/Karma uç noktası](https://technet.microsoft.com/library/adfs2-help-endpoints) gerektirir. [Daha fazla bilgi edinin](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint). Çok faktörlü kimlik doğrulaması, Kullanıcı benzeşimi olan macOS ADE cihazları için desteklenmez.

    - **Kullanıcı Benzeşimi Olmadan Kaydetme** - Tek bir kullanıcıyla bağlantılı olmayan cihazlar için bu seçeneği seçin. Yerel kullanıcı verilerine erişmeden görevleri yerine getiren cihazlar için bunu kullanın. Şirket Portalı uygulama gibi uygulamalar çalışmaz.

6. **Kullanıcı benzeşimi Ile kaydet**' i seçerseniz, **kimlik doğrulama yöntemi** altında, **modern kimlik doğrulamasıyla** **Kurulum Yardımcısı (eski)** veya Kurulum Yardımcısı ' nı seçin.

7. **Kilitli kayıt**için, bu profili kullanan cihazlar için kilitli kayıt isteyip istemediğinizi seçin. **Evet** seçeneği, yönetim profilinin **Sistem Tercihleri** menüsünden veya **Terminal**aracılığıyla kaldırılmasına izin veren MacOS ayarlarını devre dışı bırakır. Cihazı kaydettikten sonra cihazı silmeden bu ayarı değiştiremezsiniz.

8. **İleri ' yi** seçerek **Kurulum Yardımcısı** sayfasına gidin.

9. **Kurulum Yardımcısı** sayfasında, aşağıdaki profil ayarlarını yapılandırın:

    ![Kurulum Yardımcısı özelleştirme.](./media/device-enrollment-program-enroll-macos/setupassistantcustom-macos.png)

    | Departman ayarları | Açıklama |
    |---|---|
    | <strong>Bölüm Adı</strong> | Kullanıcı, etkinleştirme sırasında <strong>Yapılandırma Hakkında</strong> öğesine dokunduğunda görüntülenir. |
    | <strong>Departman Telefonu</strong> | Kullanıcı, etkinleştirme sırasında <strong>Yardım Gerekli</strong> düğmesine dokunduğunda görüntülenir. |

    Kullanıcı kurulum yaparken cihazda çeşitli Kurulum Yardımcısı ekranlarının gösterilmesini veya gizlenmesini seçebilirsiniz.
    - **Gizle**'yi seçerseniz, kurulum sırasında ekran görüntülenmez. Cihaz kurulumu yapıldıktan sonra, kullanıcı yine **Ayarlar** menüsüne gidip özelliği ayarlayabilir.
    - **Göster**'i seçerseniz, kurulum sırasında ekran görüntülenir. Kullanıcı bazen hiçbir eylem yapmadan ekranı atlayabilir. Ama daha sonra cihazın **Ayarlar** menüsüne gidebilir ve özelliği ayarlayabilir. 

    | Kurulum Yardımcısı ekran ayarları | **Göster**'i seçerseniz, kurulum sırasında cihaz... |
    |------------------------------------------|------------------------------------------|
    | <strong>Geçiş kodu</strong> | Kullanıcıdan geçiş kodu ister. Güvenliği sağlanmayan veya erişim denetimi başka bir yolla (cihazı tek uygulamayla sınırlandıran bilgi noktası modu gibi) sağlanan cihazlar için her zaman geçiş kodu isteyin. İOS/ıpados 7,0 ve üzeri için. |
    | <strong>Konum Hizmetleri</strong> | Kullanıcıdan konum ister. MacOS 10,11 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Geri Yükleme</strong> | Uygulamalar & veri ekranını görüntüleyin. Bu ekran kullanıcıya cihazı kurarken iCloud Backup'tan verileri geri yükleme veya aktarma seçeneği sağlar. MacOS 10,9 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Apple KIMLIĞI</strong> | Kullanıcıya Apple Kimliği ile oturum açma ve iCloud'u kullanma seçenekleri sağlar. MacOS 10,9 ve üzeri ve iOS/ıpados 7,0 ve üzeri için.   |
    | <strong>Hüküm ve Koşullar</strong> | Kullanıcının Apple'ın hüküm ve koşullarını kabul etmesini gerektirir. MacOS 10,9 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Touch ID</strong> | Kullanıcıya cihaz için parmak izi tanımlama özelliğini ayarlama seçeneği sağlar. MacOS 10.12.4 ve üzeri ve iOS/ıpados 8,1 ve üzeri için. |
    | <strong>Apple Pay</strong> | Kullanıcıya cihazda Apple Pay ayarlama seçeneği sağlar. MacOS 10.12.4 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Zoom</strong> | Kullanıcıya cihazı ayarlarken ekranı yakınlaştırma seçeneği sağlar. İOS/ıpados 8,3 ve üzeri için. |
    | <strong>Siri</strong> | Kullanıcıya Siri'yi ayarlama seçeneği sağlar. MacOS 10,12 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>Tanılama Verileri</strong> | Kullanıcıya Tanılama ekranını görüntüler. Bu ekran kullanıcıya Apple'a tanılama verileri gönderme seçeneği sağlar. MacOS 10,9 ve üzeri ve iOS/ıpados 7,0 ve üzeri için. |
    | <strong>FileVault</strong> | Kullanıcının dosya Kasası 2 şifreleme ekranını görüntüleyin. MacOS 10,10 ve üzeri için. |
    | <strong>iCloud tanılama</strong> | Kullanıcıya iCloud Analytics ekranını görüntüleyin. MacOS 10.12.4 ve üzeri için. |
    | <strong>iCloud Depolama</strong> | Kullanıcıya iCloud belgelerini ve masaüstü ekranını görüntüleyin. MacOS 10.13.4 ve üzeri için. |
    | <strong>Görüntü Tonu</strong> | Kullanıcıya Görüntü Tonunu açma seçeneği sunar. MacOS 10.13.6 ve üzeri ve iOS/ıpados 9.3.2 ve üzeri için. |
    | <strong>Görünüm</strong> | Kullanıcıya Görünüm ekranını gösterir. MacOS 10,14 ve üzeri ve iOS/ıpados 13,0 ve üzeri için. |
    | <strong>Kayıt</strong> | Kullanıcının kayıt ekranını görüntüleyin. MacOS 10,9 ve üzeri için. |
    | <strong>Ekran Süresi</strong> | Ekran Süresi ekranını görüntüler. MacOS 10,15 ve üzeri ve iOS/ıpados 12,0 ve üzeri için. |
    | <strong>Gizlilik</strong> | Kullanıcıya Gizlilik ekranını gösterir. MacOS 10.13.4 ve üzeri ve iOS/ıpados 11,3 ve üzeri için. |
    
10. **İleri ' yi** seçerek **gözden geçir + oluştur** sayfasına gidin.

11. Profili kaydetmek için **Oluştur**’u seçin.

## <a name="sync-managed-devices"></a>Yönetilen cihazları eşitleme

Artık Intune’a cihazlarınızı yönetme izni verildiğine göre, yönetilen cihazlarınızı Intune’da Azure portalında görmek için Intune’u Apple ile eşitleyebilirsiniz.

1. [Microsoft Uç Nokta Yöneticisi Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **cihazlar**  >  **MacOS**  >  **MacOS kaydı**  >  **kayıt programı belirteçleri**' ni seçin.

2. Cihaz eşitleme > listede bir belirteç seçin **Devices** > **Sync**. ![ Kayıt programı cihazları düğümünün seçili olduğu ve eşitleme bağlantısının seçildiği ekran görüntüsü.](./media/device-enrollment-program-enroll-macos/image06.png)

   Intune 'un kabul edilebilir kayıt programı trafiği koşullarına uymak için, Intune aşağıdaki kısıtlamaları uygular:
   - Tam eşitleme en sık yedi günde bir çalıştırılabilir. Tam eşitleme sırasında Intune, Intune’a bağlı Apple MDM sunucusuna atanan seri numaraların tam güncelleştirilmiş bir listesini alır. Bir kayıt programı cihazının Apple portalında Apple MDM sunucusundan atanmamış olması gerekmeden, Intune portalından silindikten sonra, tam eşitleme çalıştırılıncaya kadar Intune 'a yeniden içeri aktarılmaz.   
   - Eşitleme 24 saatte bir otomatik olarak çalıştırılır. **Eşitle** düğmesine basarak da eşitleyebilirsiniz (en fazla 15 dakikada bir kez). Tüm eşitleme isteklerinin tamamlanması için 15 dakika verilir. Eşitleme tamamlanana kadar **Eşitle** düğmesi devre dışı kalır. Bu eşitleme, mevcut aygıt durumunu yeniler ve Apple MDM sunucusuna atanan yeni cihazları içeri aktarır.

## <a name="assign-an-enrollment-profile-to-devices"></a>Cihazlara kayıt profili atama

Cihazların kaydedilmesi için bunlara bir kayıt programı profili atamalısınız.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **MacOS**  >  **MacOS kaydı**  >  **kayıt programı belirteçleri** ' ni seçin > listeden bir belirteç seçin.
2. **Cihazlar** > listeden cihazları seçin > **Profil ata**’yı seçin.
3. **Profil ata**'nın altında cihazlar için bir profil seçin > **Ata**’ya tıklayın.

### <a name="assign-a-default-profile"></a>Varsayılan bir profil atama

Belirli bir belirteçle kaydolan tüm cihazlara uygulanacak olan varsayılan macOS ve iOS/ıpados profilini seçebilirsiniz. 

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde **cihazlar**  >  **MacOS**  >  **MacOS kaydı**  >  **kayıt programı belirteçleri** ' ni seçin > listeden bir belirteç seçin.
2. **Varsayılan Profil Ayarla**’yı seçin, açılan listeden bir profil seçin ve daha sonra **Kaydet**’e tıklayın. Profil, bu belirteçle kaydedilen tüm cihazlara uygulanacaktır.

## <a name="distribute-devices"></a>Cihazları dağıtma

Apple ve Intune arasında eşitlemeyi ve yönetimi etkinleştirdiniz ve cihazlarınızın kaydolmasına izin vermek için bir profil atadınız. Artık cihazları kullanıcılara dağıtabilirsiniz. Kullanıcı benzeşimli cihazlar, her kullanıcıya bir Intune lisansı atanmasını gerektirir. Kullanıcı benzeşimi olmayan cihazlar, cihaz lisansı gerektirir. Etkinleştirilmiş bir cihaz, silinene kadar bir kayıt profili uygulayamaz.

## <a name="renew-an-ade-token"></a>Bir ADE belirtecini yenileme

1. deploy.apple.com adresine gidin.  
2. **Sunucuları Yönet** altında yenilemek istediğiniz belirteç dosyasıyla ilişkili MDM sunucunuzu seçin.
3. **Yeni Belirteç Oluştur**’u seçin.

    ![Yeni belirteç oluşturma ekran görüntüsü.](./media/device-enrollment-program-enroll-macos/generatenewtoken.png)

4. **Sunucu Belirteciniz**’i seçin.  
5. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431), **cihaz kaydı**  >  **Apple kaydı**  >  **kayıt programı belirteçleri** ' ni seçin > belirteci seçin.
    ![Kayıt programı belirteçlerinin ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. **Belirteci yenile**’yi seçin ve orijinal belirteci oluşturmak için kullanılan Apple kimliğini girin.  
    ![Yeni belirteç oluşturma ekran görüntüsü.](./media/device-enrollment-program-enroll-ios/renewtoken.png)

7. Yeni indirilen belirteci karşıya yükleyin.  
8. **Belirteci yenile**’yi seçin. Belirtecin yenilendiğine dair onayı görürsünüz.
    ![Onay ekran görüntüsü.](./media/device-enrollment-program-enroll-macos/confirmation.png)

## <a name="next-steps"></a>Sonraki adımlar

MacOS cihazlarını kaydettikten sonra, [bunları yönetmeye](../remote-actions/device-management.md)başlayabilirsiniz.
