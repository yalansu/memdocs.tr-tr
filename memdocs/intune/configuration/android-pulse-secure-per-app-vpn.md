---
title: Microsoft Intune-Azure 'da Android için özel uygulama başına VPN profili | Microsoft Docs
description: Microsoft Intune tarafından yönetilen Android Cihaz Yöneticisi cihazları için uygulama başına VPN profili oluşturmayı öğrenin.
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
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d58ab666929e1e28cab4e19f2e2cec668f428452
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80083881"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Microsoft Intune özel profili kullanarak Android cihazları için uygulama başına VPN profili oluşturma

Intune tarafından yönetilen Android 5.0 ve üzeri cihazlar için uygulama başına VPN profili oluşturabilirsiniz. İlk olarak, Pulse Secure veya Citrix bağlantı türlerinden birini kullanan bir VPN profili oluşturun. Ardından, VPN profilini belirli uygulamalarla ilişkilendiren özel bir yapılandırma ilkesi oluşturun.

> [!NOTE]
> Android kurumsal cihazlarda uygulama başına VPN kullanmak için de bu adımları kullanabilirsiniz. Ancak, VPN istemci uygulamanız için bir [uygulama yapılandırma ilkesi](../apps/app-configuration-policies-use-android.md) kullanmanız önerilir.

İlkeyi Android cihazınıza veya kullanıcı gruplarına atadıktan sonra kullanıcılar, Pulse Secure veya Citrix VPN istemcisini başlatmalıdır. Ardından, VPN istemcisi yalnızca belirtilen uygulamalardan gelen trafiğin açık VPN bağlantısını kullanmasına izin verir.

> [!NOTE]
>
> Bu profil için yalnızca Pulse Secure ve Citrix bağlantı türleri desteklenir.

## <a name="step-1-create-a-vpn-profile"></a>1. Adım: VPN profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Platform**: **Android Cihaz Yöneticisi**' ni seçin.
    - **Profil**: **VPN**' yi seçin.

4. **Oluştur**’u seçin.
5. **Temel bilgiler**bölümünde aşağıdaki özellikleri girin:

    - **Ad**: profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı, **tüm şirket Için Android Cihaz Yöneticisi uygulama BAŞıNA VPN profili**olur.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.

6. **İleri**’yi seçin.
7. **Yapılandırma ayarları**' nda, profilde istediğiniz ayarları yapılandırın:

    - [Android Cihaz Yöneticisi cihazları Için VPN ayarları](vpn-settings-android.md).

    VPN profilini oluştururken girdiğiniz **bağlantı adı** değerini bir yere göz atın. Bu ad bir sonraki adımda gereklidir. Bu örnekte, bağlantı adı **Myappvpnprofile**' dir.

8. **İleri**' yi seçin ve profilinizi oluşturmaya devam edin. Daha fazla bilgi için bkz. [VPN profili oluşturma](vpn-settings-configure.md#create-the-profile).

## <a name="step-2-create-a-custom-configuration-policy"></a>2. Adım: Özel yapılandırma ilkesi oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz** > **yapılandırma profilleri** > **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Ad**: özel profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı, **tüm şirket Için özel OMA-URI ANDROID VPN profilidir**.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Platform**: **Android Cihaz Yöneticisi**' ni seçin.
    - **Profil türü**: **özel**' i seçin.

4. **Ayarları** > **Yapılandır**' ı seçin.
5. **Özel OMA-URI Ayarları** bölmesinde **Ekle**’yi seçin.
    - **Ad**: ayarınız için bir ad girin.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **OMA-URI**: ENTER `./Vendor/MSFT/VPN/Profile/*Name*/PackageList`, burada *Name* , 1. adımda not ettiğiniz bağlantı adıdır. Bu örnekte, dize olur `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`.
    - **Veri türü**: **dize**girin.
    - **Değer**: profille ilişkilendirilecek paketlerin noktalı virgülle ayrılmış bir listesini girin. Örneğin, Excel 'In ve Google Chrome tarayıcısının VPN bağlantısını kullanmasını istiyorsanız, girin `com.microsoft.office.excel;com.android.chrome`.

    > [!div class="mx-imgBorder"]
    >![Örnek Android Cihaz Yöneticisi uygulama başına VPN özel ilkesi](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Uygulama listenizi kara liste veya beyaz liste olarak ayarlama (isteğe bağlı)

VPN bağlantısını *kullanamaz* uygulamaların bir listesini girmek için **kara** liste değerini kullanın. Diğer tüm uygulamalar VPN üzerinden bağlanır. Ya da, VPN bağlantısını kullanan uygulamaların bir listesini girmek için **beyaz liste** değerini *kullanın.* Listede olmayan uygulamalar VPN üzerinden bağlanmazlar.

1. **Özel OMA-URI Ayarları** bölmesinde **Ekle**’yi seçin.
2. Bir ayar adı girin.
3. **OMA-URI**' de girin `./Vendor/MSFT/VPN/Profile/*Name*/Mode`, burada *Name* , 1. adımda not ettiğiniz VPN profili adıdır. Örneğimizde, dize olur `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`.
4. **Veri türü**' nde **dize**girin.
5. **Değer** alanına **KARA LİSTE** veya **BEYAZ LİSTE** girin.

## <a name="step-3-assign-both-policies"></a>3. Adım: Her iki ilkeyi de atama

Gerekli kullanıcılara veya cihazlara [her iki cihaz profilini de atayın](device-profile-assign.md) .

## <a name="next-steps"></a>Sonraki adımlar

- Tüm Android Cihaz Yöneticisi VPN ayarlarının listesi için bkz. [VPN 'yi yapılandırmak Için Android cihaz ayarları](vpn-settings-android.md).
- VPN ayarları ve Intune hakkında daha fazla bilgi için bkz. [MICROSOFT INTUNE VPN ayarlarını yapılandırma](vpn-settings-configure.md).
