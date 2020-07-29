---
title: Microsoft Intune-Azure 'da Android Cihaz Yöneticisi için özel uygulama başına VPN profili | Microsoft Docs
description: Android Cihaz Yöneticisi 'nde, Microsoft Intune 'de Pulse Secure veya Citrix VPN bağlantı türleriyle uygulama başına VPN profilleri için özel bir profil kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2020
ms.topic: how-to
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
ms.openlocfilehash: 3c8e09b6010f7fc846fd81281053eaaa722e5ef4
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262804"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Microsoft Intune özel profili kullanarak Android cihazları için uygulama başına VPN profili oluşturma

Intune tarafından yönetilen Android 5.0 ve üzeri cihazlar için uygulama başına VPN profili oluşturabilirsiniz. İlk olarak, Pulse Secure veya Citrix bağlantı türlerinden birini kullanan bir VPN profili oluşturun. Ardından, VPN profilini belirli uygulamalarla ilişkilendiren özel bir yapılandırma ilkesi oluşturun.

Bu özellik şu platformlarda geçerlidir:

- Android cihaz yöneticisi

Android kurumsal cihazlarda uygulama başına VPN kullanmak için bir [uygulama yapılandırma ilkesi](../apps/app-configuration-vpn-ae.md)kullanın. Uygulama yapılandırma ilkeleri, daha fazla VPN istemci uygulaması destekler. Android kurumsal cihazlarda, bu makaledeki adımları kullanabilirsiniz. Ancak, önerilmez ve yalnızca Pulse Secure ve Citrix VPN bağlantılarıyla sınırlandırılırsınız.

İlkeyi Android cihazınıza veya kullanıcı gruplarına atadıktan sonra kullanıcılar, Pulse Secure veya Citrix VPN istemcisini başlatmalıdır. Ardından, VPN istemcisi yalnızca belirtilen uygulamalardan gelen trafiğin açık VPN bağlantısını kullanmasına izin verir.

> [!NOTE]
>
> Android Cihaz Yöneticisi için yalnızca Pulse Secure ve Citrix bağlantı türleri desteklenir. Android kurumsal cihazlarda bir [uygulama yapılandırma ilkesi](../apps/app-configuration-vpn-ae.md)kullanın.

## <a name="step-1-create-a-vpn-profile"></a>1. Adım: VPN profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
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
2. **Cihaz**  >  **yapılandırma profilleri**  >  **Profil oluştur**' u seçin.
3. Aşağıdaki özellikleri girin:

    - **Ad**: özel profil için açıklayıcı bir ad girin. Profillerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir profil adı, **tüm şirket Için özel OMA-URI ANDROID VPN profilidir**.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Platform**: **Android Cihaz Yöneticisi**' ni seçin.
    - **Profil türü**: **özel**' i seçin.

4. **Ayarları**  >  **Yapılandır**' ı seçin.
5. **Özel OMA-URI Ayarları** bölmesinde **Ekle**’yi seçin.
    - **Ad**: ayarınız için bir ad girin.
    - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **OMA-URI**: ENTER `./Vendor/MSFT/VPN/Profile/*Name*/PackageList` , burada *Name* , 1. adımda not ettiğiniz bağlantı adıdır. Bu örnekte, dize olur `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList` .
    - **Veri türü**: **dize**girin.
    - **Değer**: profille ilişkilendirilecek paketlerin noktalı virgülle ayrılmış bir listesini girin. Örneğin, Excel 'In ve Google Chrome tarayıcısının VPN bağlantısını kullanmasını istiyorsanız, girin `com.microsoft.office.excel;com.android.chrome` .

    :::image type="content" source="./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png" alt-text="Android Cihaz Yöneticisi uygulama başına VPN özel ilkesi Microsoft Intune":::

### <a name="set-your-blocked-and-allowed-app-list-optional"></a>Engellenen ve izin verilen uygulama listenizi ayarlama (isteğe bağlı)

VPN bağlantısını *kullanamaz* uygulamaların bir listesini girmek için **kara** liste değerini kullanın. Diğer tüm uygulamalar VPN üzerinden bağlanır. Ya da, VPN bağlantısını kullanan uygulamaların bir listesini girmek için **beyaz liste** değerini *kullanın.* Listede olmayan uygulamalar VPN üzerinden bağlanmazlar.

1. **Özel OMA-URI Ayarları** bölmesinde **Ekle**’yi seçin.
2. Bir ayar adı girin.
3. **OMA-URI**' de girin `./Vendor/MSFT/VPN/Profile/*Name*/Mode` , burada *Name* , 1. adımda not ettiğiniz VPN profili adıdır. Örneğimizde, dize olur `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode` .
4. **Veri türü**' nde **dize**girin.
5. **Değer** alanına **KARA LİSTE** veya **BEYAZ LİSTE** girin.

## <a name="step-3-assign-both-policies"></a>3. Adım: Her iki ilkeyi de atama

Gerekli kullanıcılara veya cihazlara [her iki cihaz profilini de atayın](device-profile-assign.md) .

## <a name="next-steps"></a>Sonraki adımlar

- Tüm Android Cihaz Yöneticisi VPN ayarlarının listesi için bkz. [VPN 'yi yapılandırmak Için Android cihaz ayarları](vpn-settings-android.md).
- VPN ayarları ve Intune hakkında daha fazla bilgi için bkz. [MICROSOFT INTUNE VPN ayarlarını yapılandırma](vpn-settings-configure.md).
