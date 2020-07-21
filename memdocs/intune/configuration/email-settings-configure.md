---
title: Microsoft Intune'da e-posta ayarlarını yapılandırma - Azure | Microsoft Docs
titleSuffix: ''
description: Microsoft Intune ' de bir e-posta profili oluşturun ve bu profili Android Cihaz Yöneticisi, Android Enterprise, iOS, ıpados ve Windows cihazlarına dağıtın. Yönettiğiniz cihazlarda şirket e-postasına bağlanmak için bir e-posta sunucusu ve kimlik doğrulama yöntemleri dahil olmak üzere genel e-posta ayarlarını yapılandırmak için e-posta profilleri
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5bb01770909192b17f0e72b852e4094ff7ad3a04
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565657"
---
# <a name="add-email-settings-to-devices-using-intune"></a>Intune kullanarak cihazlara e-posta ayarları ekleme

Microsoft Intune, kuruluşunuzdaki cihazlara dağıtabileceğiniz farklı e-posta ayarları içerir. BT Yöneticisi, Office 365 ve Gmail gibi bir posta sunucusuna bağlanmak için belirli ayarlarla e-posta profilleri oluşturur. Son kullanıcılar daha sonra mobil cihazlarındaki kurumsal e-posta hesaplarını bağlayıp, kimlik doğrulaması yapar ve eşitler. Bir e-posta profili oluşturup dağıtarak, ayarların birçok cihazda standart olduğunu doğrulayabilirsiniz. Ayrıca doğru e-posta ayarlarını bilmeyen son kullanıcılardan gelen destek çağrılarını azaltabilirsiniz.

Aşağıdaki cihazlarda yerleşik e-posta ayarlarını yapılandırmak için e-posta profillerini kullanabilirsiniz:

- Samsung KNOX Standard 5,0 ve üzeri üzerinde Android Cihaz Yöneticisi
- Android Kurumsal
- iOS 11,0 ve üzeri
- ıpados 13,0 ve üzeri
- Windows Phone 8,1 ve üzeri
- Windows 10 (masaüstü) ve Windows 10 Mobile

Bu makalede, Microsoft Intune’da e-posta profili oluşturma işlemi gösterilir. Ayrıca daha özel ayarlar için farklı platformlara bağlantılar içerir.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:  

        - **Android Cihaz Yöneticisi** (yalnızca Samsung Android Knox Standard)
        - **Android Kurumsal**
        - **iOS/iPadOS**
        - **Windows 10 ve üzeri**
        - **Windows Phone 8.1**

    - **Profil**: **e-posta**' yı seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **Windows 10: tüm Windows 10 cihazları Için e-posta ayarları**.
    - **Açıklama**: ilke için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.

7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:

    - [Android Cihaz Yöneticisi (Samsung KNOX Standard)](email-settings-android.md)
    - [Android Kurumsal](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)
    - [Windows Phone 8.1](email-settings-windows-phone-8-1.md)

8. **İleri**’yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak olan kullanıcı veya cihaz gruplarını seçin. Profil atama hakkında daha fazla bilgi için bkz. [bilmeniz](#what-you-need-to-know) gerekenler (Bu makalede). [Kullanıcı ve cihaz profillerini](device-profile-assign.md) de bir miktar kılavuza atayın.

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="what-you-need-to-know"></a>Bilmeniz gerekenler

- E-posta profilleri, cihazı kaydeden Kullanıcı için dağıtılır. Intune, e-posta profilini yapılandırmak için kayıt sırasında kullanıcının e-posta profilindeki Azure Active Directory (AD) özelliklerini kullanır.

- İOS için Microsoft Outlook/ıpados ve Android cihazları e-posta profillerini desteklemez. Bunun yerine, bir uygulama yapılandırma ilkesi dağıtın. Daha fazla bilgi için bkz. [Outlook yapılandırma ayarı](../apps/app-configuration-policies-outlook.md).

  Android kurumsal cihazlarda, yönetilen Google Play Store kullanarak Gmail veya dokuz Iş için dağıtım yapın. [Yönetilen Google Play uygulamaları ekleme](../apps/apps-add-android-for-work.md) adımları listeler.

- E-posta, kimlik ve Kullanıcı ayarlarını temel alır. E-posta profilleri, genellikle cihaz gruplarına değil Kullanıcı gruplarına atanır. Bazı hususlar:

  - E-posta profili Kullanıcı sertifikaları içeriyorsa, e-posta profilini Kullanıcı gruplarına atayın. Atanmış birden çok kullanıcı sertifikası profiliniz olabilir. Bu birden çok profil, bir profil dağıtımları zinciri oluşturur. Bu profil zincirini Kullanıcı gruplarına dağıtın.

    Bu zincirdeki bir profil bir cihaz grubuna dağıtılırsa, kullanıcılardan sürekli olarak parolasını girmesi istenebilir.

  - Cihaz grupları genellikle birincil kullanıcı olmadığında veya kullanıcının kim olacağını bilmiyorsanız kullanılır. Cihaz gruplarına (Kullanıcı grupları değil) hedeflenmiş e-posta profilleri cihaza teslim edilemeyebilir.

    Örneğin, e-posta profiliniz tüm iOS/ıpados cihazları grubunu hedefliyorsa, tüm bu cihazların bir kullanıcıya sahip olduğundan emin olun. Herhangi bir cihazda Kullanıcı yoksa, e-posta profili dağıtılamayabilir. Ardından, profili sınırlandırabilir ve bazı cihazları kaçırırdınız. Cihazın birincil kullanıcısı varsa, cihaz gruplarına dağıtım çalışması gerekir.

    Cihaz gruplarını kullanmayla ilgili olası sorunlar hakkında daha fazla bilgi için bkz. [e-posta profilleriyle Ilgili genel sorunlar](troubleshoot-email-profiles-in-microsoft-intune.md).

## <a name="remove-an-email-profile"></a>E-posta profilini kaldırma

Cihazda sadece bir e-posta profili olduğunda bile e-posta profilini kaldırmanın farklı yolları vardır:

- **Seçenek 1**: e-posta profilini açın (**cihaz**  >  **yapılandırma profilleri** > profilinizi seçin) ve **atamalar**' ı seçin. **Ekle** sekmesi, profil atanmış grupları gösterir. Gruba sağ tıklayın ve **Kaldır**’ı seçin. Değişikliklerinizi kaydetmek için **Kaydet**’e tıklamayı unutmayın.

- **2. Seçenek**: [Cihazı devre dışı bırakın veya silin](../remote-actions/devices-wipe.md). Veri ve ayarları seçmeli olarak veya tamamen kaldırmak için bu eylemleri kullanabilirsiniz.

## <a name="secure-email-access"></a>E-posta erişimini güvenli hale getirme

E-posta profillerinin güvenliği sağlamaya yardımcı olmak için aşağıdaki seçenekleri kullanabilirsiniz:

- **Sertifikalar**: E-posta profilini oluştururken, daha önce Intune’da oluşturulan bir sertifika profilini seçersiniz. Bu sertifika, kimlik sertifikası olarak bilinir. Kullanıcının cihazının bağlanmasına izin verildiğini doğrulamak için güvenilir bir sertifika profilinde veya kök sertifikada kimlik doğrulaması gerçekleştirir. Güvenilir sertifika, e-posta bağlantısının kimliğini doğrulayan bilgisayara atanır. Bu bilgisayar genellikle yerel posta sunucusudur.

  E-posta profiliniz için sertifika tabanlı kimlik doğrulaması kullanıyorsanız, e-posta profilini, sertifika profilini ve güvenilen kök profilini aynı gruplara dağıtın. Bu dağıtım, her cihazın sertifika yetkilinizin yasallığını tanıyabileceği şekilde sağlar.

  Intune’da sertifika profillerini oluşturma ve kullanma hakkında daha fazla bilgi için bkz. [Intune ile sertifikaları yapılandırma](../protect/certificates-configure.md).

- **Kullanıcı adı ve parola**: Son Kullanıcı, bir Kullanıcı adı ve parola girerek Yerel posta sunucusunda kimliğini doğrular. Parola e-posta profilinde bulunmaz. Bu nedenle, son kullanıcı e-postaya bağlanırken parolayı girer.

## <a name="how-intune-handles-existing-email-accounts"></a>Intune mevcut e-posta hesaplarını nasıl işler?

Kullanıcı zaten bir e-posta hesabı yapılandırılmışsa e-posta profili platforma bağlı olarak farklı şekilde atanır.

- **iOS/ıpados**: Ana bilgisayar adı ve e-posta adresine bağlı olarak var olan, yinelenen bir e-posta profili algılanır. Yinelenen e-posta profili, Intune profilinin atamasını engeller. Bu durumda, Şirket Portalı uygulama kullanıcıya uyumlu olmadıkları konusunda bilgilendirir ve son kullanıcıdan yapılandırılmış profili el ile kaldırmasını ister. Bu senaryoyu önlemeye yardımcı olmak için son kullanıcılarınıza Intune 'un profili ayarlamasına izin veren bir e-posta profili yüklemeden *önce* kaydolmalarını söyleyin.

- **Windows:** Ana bilgisayar adı ve e-posta adresine bağlı olarak mevcut, yinelenen bir e-posta profili algılanır. Intune, son kullanıcı tarafından oluşturulan mevcut e-posta profilinin üzerine yazar.

- **Android Samsung KNOX Standard**: e-posta adresine bağlı olarak var olan, yinelenen bir e-posta profili algılanır ve Intune profiliyle üzerine yazılır. Android, profili tanımlamak için ana bilgisayar adı kullanmaz. Farklı ana bilgisayarlarda aynı e-posta adresini kullanarak birden çok e-posta profili oluşturmayın. Profiller birbirinin üzerine yazılır.

- **Android iş profilleri**: Intune, Gmail uygulaması için bir diğeri Ise dokuz iş uygulaması için olmak üzere iki Android iş e-posta profili sağlar. Bu uygulamalar Google Play Store kullanılabilir ve cihaz iş profiline yüklenir. Bu uygulamalar Yinelenen profiller oluşturmaz. Her iki uygulama da Exchange bağlantılarını destekler. E-posta bağlantısını kullanmak için, bu e-posta uygulamalarından birini Kullanıcı cihazlarınıza dağıtın. Sonra, e-posta profilini oluşturun ve dağıtın. Iş profili için çalışan Gmail ve dokuz e-posta yapılandırma profillerini, her iki e-posta yapılandırma türündeki sertifika profillerini kullanma dahil olmak üzere, tam olarak yönetilen, adanmış ve şirkete ait Iş profili kayıt türlerini kullanabilirsiniz. Iş profillerine yönelik cihaz yapılandırmasında oluşturduğunuz Gmail veya dokuz ilke cihaza uygulanmaya devam eder. Bunları uygulama yapılandırma ilkelerine taşımak gerekli değildir. Dokuz Iş gibi e-posta uygulamaları ücretsiz olmayabilir. Uygulamanın lisanslama ayrıntılarını gözden geçirin veya herhangi bir soru ile uygulama şirketiyle iletişim kurun.

## <a name="changes-to-assigned-email-profiles"></a>Atanan e-posta profillerindeki değişiklikler

Önceden atanmış bir e-posta profilinde değişiklik yaparsanız, son kullanıcılara e-posta ayarlarının yeniden yapılandırmasını onaylamalarını isteyen bir ileti gösterilebilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulduğunda henüz herhangi bir işlem gerçekleştirmez. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).
