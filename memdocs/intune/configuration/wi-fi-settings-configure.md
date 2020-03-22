---
title: Microsoft Intune - Azure’da cihazlar için Wi-Fi profili oluşturma | Microsoft Docs
description: Microsoft Intune’da Wi-Fi cihaz yapılandırma profilleri oluşturmak için adımları inceleyin. Android Cihaz Yöneticisi, Android kurumsal, Android bilgi noktası, iOS, Idos, macOS, Windows 10 ve üzeri ve Windows holographic for Business için Profiller oluşturun. Bu profilleri kullanarak sertifika kullanmak için bir Wi-Fi bağlantısı oluşturmak, EAP türü seçmek, kimlik doğrulama yöntemi seçmek, proxy etkinleştirmek gibi pek çok şey yapabilirsiniz.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 235f5517c9968ba63b04fefa03d9486e5bd6e52d
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086401"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Microsoft Intune’da cihazlarınız için Wi-Fi ayarları ekleme ve kullanma

Wi-Fi, ağ erişimi sağlamak için birçok mobil cihaz tarafından kullanılan bir kablosuz ağ. Microsoft Intune, kuruluşunuzdaki kullanıcılara ve cihazlara dağıtılabilecek yerleşik Wi-Fi ayarlarını içerir. Bu ayar grubu "profil" olarak adlandırılır ve farklı kullanıcılara ve gruplara atanabilir. Atandıktan sonra kullanıcılarınız, kuruluşunuzun Wi-Fi ağına kendi kendilerini yapılandırmadan erişin.

Örneğin Contoso Wi-Fi adında yeni bir Wi-Fi ağı kurdunuz. Ardından, bu ağa bağlanmak için tüm iOS/ıpados cihazlarını ayarlamak istersiniz. İşlem şöyledir:

1. Contoso Wi-Fi kablosuz ağına bağlanan ayarları içeren bir Wi-Fi profili oluşturun.
2. Profili iOS/ıpados cihazlarının tüm kullanıcılarını içeren bir gruba atayın.
3. Kullanıcılar, cihazlarında yeni Contoso Wi-Fi ağını kablosuz ağ listesinde bulur. Daha sonra seçtiğiniz kimlik doğrulama yöntemini kullanarak ağa bağlanabilirler.

Bu makalede, Wi-Fi profili oluşturma adımları listelenir. Ayrıca, her platform için farklı ayarları tanımlayan bağlantıları da içerir.

## <a name="supported-device-platforms"></a>Desteklenen cihaz platformları

Wi-Fi profilleri aşağıdaki cihaz platformlarını destekler:

- Android 4 ve üzeri
- Android Kurumsal ve bilgi noktası
- iOS 8,0 ve üzeri
- ıpados 13,0 ve üzeri
- macOS X 10,11 ve üzeri
- Windows 10 ve üzeri, Windows 10 Mobile ve Windows holographic for Business

> [!NOTE]
> Windows 8.1 çalıştıran cihazlarda daha önce başka bir cihazdan dışarı aktarılmış olan bir Wi-Fi yapılandırmasını içeri aktarabilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:

      - **Android Cihaz Yöneticisi**
      - **Android Kurumsal**
      - **iOS/ıpados**
      - **macOS**
      - **Windows 10 ve üzeri**
      - **Windows 8.1 ve üzeri**

    - **Profil**: **Wi-Fi ' ı**seçin.

      > [!TIP]
      >
      > - Adanmış bir cihaz (bilgi noktası) olarak çalışan **Android kurumsal** cihazlarda **yalnızca cihaz sahibi** > **Wi-Fi**' y i seçin.
      > - **Windows 8.1 ve sonrasında** **Wi-Fi içeri aktar**’ı seçebilirsiniz. Bu seçenek, Wi-Fi ayarlarını daha önce başka cihazdan dışarı aktarmış olduğunuz bir XML dosyası olarak içeri aktarmanıza olanak tanır.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı **tüm şirket Için WiFi profilidir**.
    - **Açıklama**: Profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**'yi seçin.
7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:

    - [Android Cihaz Yöneticisi](wi-fi-settings-android.md)
    - Adanmış cihazlar dahil [Android Enterprise](wi-fi-settings-android-enterprise.md)
    - [iOS/ıpados](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 ve üzeri](wi-fi-settings-windows.md)
    - [Windows 8.1 ve sonrası](wi-fi-settings-import-windows-8-1.md), Windows Holographic for Business dahil

8. **İleri**'yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili `US-NC IT Team` veya `JohnGlenn_ITDepartment`gıbı belirli BT gruplarına filtrelemek için bir etiket atayın. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**'yi seçin.

10. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**'yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu ancak hiçbir şey yapmıyor. Sonra, [Bu profili atayın](device-profile-assign.md) ve [durumunu izleyin.](device-profile-monitor.md)

[Intune 'Da Troubles Wi-Fi profilleri](troubleshoot-wi-fi-profiles.md).
