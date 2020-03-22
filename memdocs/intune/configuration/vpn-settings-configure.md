---
title: Microsoft Intune-Azure 'da cihazlara VPN ayarları ekleme | Microsoft Docs
description: Android Cihaz Yöneticisi, Android Enterprise, iOS, ıpados, macOS ve Windows cihazlarında, Microsoft Intune 'de sanal özel ağ (VPN) bağlantıları oluşturmak için yerleşik ayarları kullanın.
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
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64356bf9be0c2c439c1f4fc296a9728a7937b001
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086569"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Intune 'da VPN sunucularına bağlanmak için VPN profilleri oluşturma

Sanal özel ağlar (VPN 'Ler), kullanıcılara kuruluş ağınıza güvenli uzaktan erişim olanağı sağlar. Cihazlar VPN sunucusuyla bir bağlantı başlatmak için bir VPN bağlantısı profili kullanır. Microsoft Intune ' deki **VPN profilleri** , kuruluşunuzun kullanıcılara ve cihazlarına VPN ayarları atayarak kurumsal ağınıza kolayca ve güvenli bir şekilde bağlanabilmelerini sağlar.

Örneğin, kuruluş ağındaki bir dosya paylaşımıyla bağlantı kurmak için tüm iOS/ıpados cihazlarını gerekli ayarlarla yapılandırmak istiyorsunuz. Bu ayarları içeren bir VPN profili oluşturursunuz. Ardından, bu profili iOS/ıpados cihazlarına sahip tüm kullanıcılara atarsınız. Kullanıcılar, VPN bağlantısını kullanılabilir ağlar listesinde görür ve ağa kolaylıkla bağlanabilir.

> [!NOTE]
> Aşağıdaki platformlar için VPN profilleri oluşturmak üzere [Intune özel yapılandırma ilkelerini](custom-settings-configure.md) kullanabilirsiniz:
>
> * Android 4 ve üzeri
> * Windows 8.1 ve üzeri çalıştıran kayıtlı cihazlar
> * Windows Phone 8.1 ve üzeri
> * Windows 10 masaüstü çalıştıran kayıtlı cihazlar
> * Windows 10 Mobile
> * Windows 10 Holographic for Business

## <a name="vpn-connection-types"></a>VPN bağlantısı türleri

VPN profillerini oluştururken aşağıdaki bağlantı türlerini kullanabilirsiniz:

- Otomatik
  - Windows 10

- Check Point Capsule VPN
  - Android Cihaz Yöneticisi
  - Android kurumsal iş profilleri
  - iOS/iPadOS
  - Mac OS
  - Windows 10
  - Windows 8.1
  - WVPN profillerinidows Phone 8.1

- Cisco AnyConnect
  - Android Cihaz Yöneticisi
  - Android kurumsal iş profilleri
  - Android kurumsal cihaz sahibi (tam olarak yönetilen)
  - iOS/iPadOS
  - Mac OS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Android Cihaz Yöneticisi
  - Android kurumsal iş profilleri: [uygulama yapılandırma Ilkesini](../apps/app-configuration-policies-use-android.md) kullanma
  - Android kurumsal cihaz sahibi (tamamen yönetilen): [uygulama yapılandırma Ilkesini](../apps/app-configuration-policies-use-android.md) kullanma
  - iOS/iPadOS
  - Windows 10

- Özel VPN
  - iOS/iPadOS
  - Mac OS

  [Özel ayarlarla profil oluşturma](custom-settings-configure.md)içindeki URI ayarlarını kullanarak özel VPN profilleri oluşturun.

- F5 Access
  - Android Cihaz Yöneticisi
  - Android kurumsal iş profilleri
  - Android kurumsal cihaz sahibi (tam olarak yönetilen)
  - iOS/iPadOS
  - Mac OS
  - Windows 10
  - Windows 8.1
  - WVPN profillerinidows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Android kurumsal iş profilleri: [uygulama yapılandırma Ilkesini](../apps/app-configuration-policies-use-android.md) kullanma
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Android Cihaz Yöneticisi
  - Android kurumsal iş profilleri
  - Android kurumsal cihaz sahibi (tam olarak yönetilen)
  - iOS/iPadOS
  - Mac OS
  - Windows 10
  - Windows 8.1
  - WVPN profillerinidows Phone 8.1

- SonicWall Mobile Connect
  - Android Cihaz Yöneticisi
  - Android kurumsal iş profilleri
  - iOS/iPadOS
  - Mac OS
  - Windows 10
  - Windows 8.1
  - WVPN profillerinidows Phone 8.1

- Zscaler
  - Android kurumsal iş profilleri: [uygulama yapılandırma Ilkesini](../apps/app-configuration-policies-use-android.md) kullanma
  - iOS/iPadOS

> [!IMPORTANT]
> Bir cihaza atanan VPN profillerini kullanmadan önce profil için geçerli VPN uygulamasını yüklemeniz gerekir. Uygulamayı Intune kullanarak atamanıza yardımcı olması için bkz. [Microsoft Intune 'da uygulama yönetimi nedir?](../apps/app-management.md).  

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:
      - **Android Cihaz Yöneticisi**
      - Yalnızca **Android kurumsal** > **cihaz sahibi**
      - Yalnızca **Android kurumsal** > **iş profili**
      - **iOS/ıpados**
      - **macOS**
      - **Windows 10 ve üzeri**
      - **Windows 8.1 ve üzeri**
      - **Windows Phone 8.1**
    - **Profil**: **VPN**' yi seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı **Şirket genelinde VPN profilidir**.
    - **Açıklama**: Profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**'yi seçin.
7. **Yapılandırma ayarları**' nda, seçtiğiniz platforma bağlı olarak, yapılandırabileceğiniz ayarlar farklıdır. Ayrıntılı ayarlar için platformunuzu seçin:

    - [Android Cihaz Yöneticisi](vpn-settings-android.md)
    - [Android Kurumsal](vpn-settings-android-enterprise.md)
    - [iOS/ıpados](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (Windows holographic for Business dahil)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. **İleri**'yi seçin.
9. **Kapsam etiketleri** ' nde (isteğe bağlı), profili `US-NC IT Team` veya `JohnGlenn_ITDepartment`gıbı belirli BT gruplarına filtrelemek için bir etiket atayın. Kapsam etiketleri hakkında daha fazla bilgi için bkz. [Dağıtılmış BT IÇIN RBAC ve kapsam etiketlerini kullanma](../fundamentals/scope-tags.md).

    **İleri**'yi seçin.

10. **Atamalar**' da, profilinizi alacak Kullanıcı veya grupları seçin. Profil atama hakkında daha fazla bilgi için bkz. [Kullanıcı ve cihaz profilleri atama](device-profile-assign.md).

    **İleri**'yi seçin.

11. **Gözden geçir + oluştur**bölümünde ayarlarınızı gözden geçirin. **Oluştur**' u seçtiğinizde değişiklikleriniz kaydedilir ve profil atanır. İlke ayrıca profiller listesinde gösterilir.

## <a name="secure-your-vpn-profiles"></a>VPN profillerinizin güvenliğini sağlama

VPN profilleri, farklı üreticilerden farklı bağlantı türleri ve farklı protokoller kullanabilir. Bu bağlantılar genellikle aşağıdaki yöntemlerle güvenli hale getirilir.

### <a name="certificates"></a>Sertifikalar

VPN profilini oluştururken, Intune’da önceden oluşturduğunuz bir SCEP veya PKCS sertifika profilini seçersiniz. Bu profil, kimlik sertifikası olarak bilinir. Kullanıcının cihazının bağlanmasına izin vermek için oluşturduğunuz bir güvenilir sertifika profiline (veya *kök sertifikaya*) göre kimlik doğrulaması yapmak için kullanılır. Güvenilir sertifika, VPN bağlantısının kimliğini doğrulayan bilgisayara atanır. Bu, genellikle VPN sunucusudur.

Intune’da sertifika profillerini oluşturma ve kullanma hakkında daha fazla bilgi için bkz. [Microsoft Intune ile sertifikaları yapılandırma](../protect/certificates-configure.md).

### <a name="user-name-and-password"></a>Kullanıcı adı ve parola

Kullanıcı, kullanıcı adı ve parola girerek VPN sunucusunda kimliğini doğrular.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulduğunda henüz herhangi bir işlem gerçekleştirmez. Sonra, [profili](device-profile-assign.md) bazı cihazlara atayın ve [durumunu izleyin](device-profile-monitor.md).

Ayrıca, [Android Cihaz Yöneticisi/Android Enterprise](android-pulse-secure-per-app-vpn.md) ve [IOS/ıpados](vpn-setting-configure-per-app.md) cihazlarında uygulama başına VPN 'ler oluşturabilir ve kullanabilirsiniz.
