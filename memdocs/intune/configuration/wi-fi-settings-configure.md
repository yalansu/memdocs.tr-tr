---
title: Microsoft Intune - Azure’da cihazlar için Wi-Fi profili oluşturma | Microsoft Docs
description: Microsoft Intune’da Wi-Fi cihaz yapılandırma profilleri oluşturmak için adımları inceleyin. Android Cihaz Yöneticisi, Android kurumsal, Android bilgi noktası, iOS, Idos, macOS, Windows 10 ve üzeri ve Windows holographic for Business için Profiller oluşturun. Bu profilleri kullanarak sertifika kullanmak için bir Wi-Fi bağlantısı oluşturmak, EAP türü seçmek, kimlik doğrulama yöntemi seçmek, proxy etkinleştirmek gibi pek çok şey yapabilirsiniz.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a92abc89dca291cd42a66c284bee5f1f4007836b
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88145887"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Microsoft Intune’da cihazlarınız için Wi-Fi ayarları ekleme ve kullanma

Wi-Fi, ağ erişimi sağlamak için birçok mobil cihaz tarafından kullanılan bir kablosuz ağ. Microsoft Intune, kuruluşunuzdaki kullanıcılara ve cihazlara dağıtılabilecek yerleşik Wi-Fi ayarlarını içerir. Bu ayar grubu "profil" olarak adlandırılır ve farklı kullanıcılara ve gruplara atanabilir. Atandıktan sonra kullanıcılarınız, kuruluşunuzun Wi-Fi ağına kendi kendilerini yapılandırmadan erişin.

Örneğin Contoso Wi-Fi adında yeni bir Wi-Fi ağı kurdunuz. Ardından, bu ağa bağlanmak için tüm iOS/ıpados cihazlarını ayarlamak istersiniz. Süreç şu şekildedir:

1. Contoso Wi-Fi kablosuz ağına bağlanan ayarları içeren bir Wi-Fi profili oluşturun.
2. Profili iOS/ıpados cihazlarının tüm kullanıcılarını içeren bir gruba atayın.
3. Kullanıcılar, cihazlarında yeni Contoso Wi-Fi ağını kablosuz ağ listesinde bulur. Daha sonra seçtiğiniz kimlik doğrulama yöntemini kullanarak ağa bağlanabilirler.

Bu makalede, Wi-Fi profili oluşturma adımları listelenir. Ayrıca, her platform için farklı ayarları tanımlayan bağlantıları da içerir.

## <a name="supported-device-platforms"></a>Desteklenen cihaz platformları

Wi-Fi profilleri aşağıdaki cihaz platformlarını destekler:

- Android 5 ve üzeri
- Android Kurumsal ve bilgi noktası
- iOS 11,0 ve üzeri
- ıpados 13,0 ve üzeri
- macOS X 10,12 ve üzeri
- Windows 10 ve üzeri ve Windows holographic for Business

> [!NOTE]
> Windows 8.1 çalıştıran cihazlarda daha önce başka bir cihazdan dışarı aktarılmış olan bir Wi-Fi yapılandırmasını içeri aktarabilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:

      - **Android cihaz yöneticisi**
      - **Android Kurumsal**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 ve üzeri**
      - **Windows 8.1 ve üzeri**

    - **Profil**: **Wi-Fi ' ı**seçin.

      > [!TIP]
      >
      > - Adanmış bir cihaz (bilgi noktası) olarak çalışan **Android kurumsal** cihazlarda, **tam olarak yönetilen, adanmış ve şirkete ait iş profili**  >  **Wi-Fi**' y i seçin.
      > - **Windows 8.1 ve daha yeni bir sürümü**için **Wi-Fi içeri aktarmayı**seçebilirsiniz. Bu seçenek, Wi-Fi ayarlarını daha önce başka cihazdan dışarı aktarmış olduğunuz bir XML dosyası olarak içeri aktarmanıza olanak tanır.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı **tüm şirket Için WiFi profilidir**.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.
7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:

    - [Android cihaz yöneticisi](wi-fi-settings-android.md)
    - Adanmış cihazlar dahil [Android Enterprise](wi-fi-settings-android-enterprise.md)
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 ve üzeri](wi-fi-settings-windows.md)
    - Windows holographic for Business dahil [Windows 8.1 ve daha yeni](wi-fi-settings-import-windows-8-1.md)

8. **İleri**’yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili, veya gıbı belirli BT gruplarına filtrelemek için bir etiket atayın `US-NC IT Team` `JohnGlenn_ITDepartment` . Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**’yi seçin.

10. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**’yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

> [!TIP]
> Wi-Fi profiliniz için sertifika tabanlı kimlik doğrulaması kullanıyorsanız, her bir cihazın sertifika yetkilinizin yasallığını algılayabilmesi için Wi-Fi profilini, sertifika profilini ve güvenilen kök profilini aynı gruplara dağıtın.  Daha fazla bilgi için bkz. [Microsoft Intune sertifikaları yapılandırma](../protect/certificates-configure.md).

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu, ancak hiçbir şey gerçekleştirmeyebilir. Sonra, [Bu profili atayın](device-profile-assign.md) ve [durumunu izleyin.](device-profile-monitor.md)

[Intune 'Da Troubles Wi-Fi profilleri](troubleshoot-wi-fi-profiles.md).
