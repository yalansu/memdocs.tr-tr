---
title: Microsoft Intune'a MTD uygulamaları ekleme ve atama
titleSuffix: Microsoft Intune
description: Azure portalında Intune kullanarak Mobile Threat Defense (MTD) uygulamalarını, Microsoft Authenticator uygulamasını ve iOS yapılandırma ilkesini ekleyin.
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
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b487b9f921e40df8730fab235a2ec2c0d3f0f788
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910868"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Intune ile Mobile Threat Defense (MTD) uygulamaları ekleme ve atama

Mobil tehdit savunma (MTD) uygulamalarını eklemek ve dağıtmak için Intune 'u kullanabilirsiniz. böylece, son kullanıcılar mobil cihazlarında bir tehdit tanımlandığında bildirim alabilir ve tehditleri düzeltmeye yönelik rehberlik elde edebilir.

> [!NOTE]
> Bu makale tüm Mobile Threat Defense iş ortakları için geçerlidir.

## <a name="before-you-begin"></a>Başlamadan önce

Intune 'da aşağıdaki adımları izleyin. İşlemini öğrendiğinizden emin olun:

- [Intune’a uygulama ekleme](../apps/apps-add.md).
- [Intune’a iOS uygulama yapılandırma ilkesi ekleme](../apps/app-configuration-policies-use-ios.md).
- [Intune ile uygulama atama](../apps/apps-deploy.md).

> [!TIP]
> Intune Şirket Portalı, kullanıcıların kimliklerinin Azure AD tarafından denetlenmesi için Android cihazlarda aracı olarak kullanılır.

## <a name="configure-microsoft-authenticator-for-ios"></a>iOS için Microsoft Authenticator’ı yapılandırma

iOS cihazlarında, Azure AD'nin kullanıcıların kimlikleri denetleyebilmesi için [Microsoft Authenticator](/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) olması gerekir. Ayrıca, Intune ile kullandığınız MTD iOS uygulamasını ayarlayan bir iOS uygulama yapılandırma ilkesine ihtiyacınız vardır.

Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **Uygulama bilgilerini**yapılandırırken bu [Microsoft Authenticator App Store URL 'sini](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) kullanın.

## <a name="configure-your-mtd-apps-with-an-app-configuration-policy"></a>MTD uygulamalarınızı bir uygulama yapılandırma ilkesiyle yapılandırma

Kullanıcı ekleme işlemini basitleştirmek için, MDM ile yönetilen cihazlarda Mobile Threat Defense uygulamaları uygulama yapılandırması kullanır. Kayıtlı olmayan cihazlar için MDM tabanlı uygulama yapılandırması mevcut değildir, bu nedenle lütfen [kayıtlı olmayan cihazlara mobil tehdit savunma uygulamaları ekleme](../protect/mtd-add-apps-unenrolled-devices.md)bölümüne bakın.

### <a name="lookout-for-work-app-configuration-policy"></a>Lookout for Work uygulama yapılandırma ilkesi

İOS uygulama yapılandırma ilkesini [iOS uygulama yapılandırma ilkesi kullanma](../apps/app-configuration-policies-use-ios.md) makalesinde açıklandığı gibi oluşturun.

### <a name="sep-mobile-app-configuration-policy"></a>SEP Mobile uygulama yapılandırma ilkesi

[Symantec Endpoint Protection yönetim konsolunda](https://aad.skycure.com)önceden yapılandırılmış aynı Azure AD hesabını kullanın. Bu, Intune 'da oturum açmak için kullanılan hesap olmalıdır.

- İOS uygulama yapılandırma ilkesi dosyasını **indirin** :
  - [Symantec Endpoint Protection Yönetim konsoluna](https://aad.skycure.com) gidin ve yönetici kimlik bilgilerinizle oturum açın.

  - **Ayarlar**'a gidin ve **Tümleştirmeler**'in altında **Intune**'u seçin. **EMM Tümleştirme Seçimi**'ni seçin. **Microsoft**'u seçin ve ardından seçiminizi kaydedin.

  - **Tümleştirme kurulum dosyaları** bağlantısına tıklayın ve oluşturulan \*.zip dosyasını kaydedin. Bu .zip dosyası, Intune’da iOS uygulama yapılandırma ilkesini oluşturmak için kullanılacak olan ***.plist** dosyasını içerir.

  - SEP Mobile iOS uygulama yapılandırma ilkesini eklemek için [iOS için Microsoft Intune uygulama yapılandırma ilkeleri kullanma](../apps/app-configuration-policies-use-ios.md) yönergelerine bakın.

    - **Yapılandırma ayarları biçimi**IÇIN, **XML verisi gir**' i seçin, içeriği ***. plist** dosyasından kopyalayın ve içeriğini yapılandırma ilkesi gövdesine yapıştırın.

> [!NOTE]
> Dosyaları alamıyorsanız, [Symantec Endpoint Protection Mobile Enterprise Desteği](https://support.symantec.com/en_US/contact-support.html)'ne başvurun.

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Check Point SandBlast Mobile uygulaması yapılandırma ilkesi

Check Point SandBlast Mobile iOS uygulama yapılandırma ilkesini eklemek için [iOS için Microsoft Intune uygulama yapılandırma ilkelerini kullanma](../apps/app-configuration-policies-use-ios.md) yönergelerine bakın.

- **Yapılandırma ayarları biçimi**IÇIN, **XML verisi gir**' i seçin, aşağıdaki içeriği kopyalayın ve yapılandırma ilkesi gövdesine yapıştırın.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### <a name="zimperium-app-configuration-policy"></a>Zimperium uygulama yapılandırma ilkesi

Zimperium iOS uygulama yapılandırma ilkesini eklemek için [iOS için Microsoft Intune uygulama yapılandırma ilkeleri kullanma](../apps/app-configuration-policies-use-ios.md) yönergelerine bakın.

- **Yapılandırma ayarları biçimi**IÇIN, **XML verisi gir**' i seçin, aşağıdaki içeriği kopyalayın ve yapılandırma ilkesi gövdesine yapıştırın.

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### <a name="pradeo-app-configuration-policy"></a>Pradeo uygulama yapılandırma ilkesi

Pradeo, iOS/ıpados üzerinde uygulama yapılandırma ilkesini desteklemez.  Bunun yerine, yapılandırılmış bir uygulama almak için, tercih ettiğiniz ayarlarla önceden yapılandırılmış özel IPA veya APK dosyalarını uygulamak üzere Pradeo ile birlikte çalışın.

### <a name="better-mobile-app-configuration-policy"></a>Better Mobile uygulama yapılandırma ilkesi

Better Mobile iOS uygulama yapılandırma ilkesini eklemek için [iOS için Microsoft Intune uygulama yapılandırma ilkeleri kullanma](../apps/app-configuration-policies-use-ios.md) yönergelerine bakın.

- **Yapılandırma ayarları biçimi**IÇIN, **XML verisi gir**' i seçin, aşağıdaki içeriği kopyalayın ve yapılandırma ilkesi gövdesine yapıştırın. `https://client.bmobi.net` URL'sini uygun konsol URL'siyle değiştirin.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### <a name="sophos-mobile-app-configuration-policy"></a>Sophos mobil uygulama yapılandırma ilkesi

İOS uygulama yapılandırma ilkesini [iOS uygulama yapılandırma ilkesi kullanma](../apps/app-configuration-policies-use-ios.md) makalesinde açıklandığı gibi oluşturun. Daha fazla bilgi için, Sophos Bilgi Bankası 'ndaki [mobil iOS Için kullanılabilir yönetilen ayarlar Için Sophos KESMENOKTASI X](https://community.sophos.com/kb/133963) bölümüne bakın.

### <a name="wandera-app-configuration-policy"></a>Wandera uygulama yapılandırma ilkesi

> [!NOTE]
> İlk test için yapılandırma ilkesinin atamalar bölümüne Kullanıcı ve cihaz atarken bir test grubu kullanın. 

- **Android**
  - Sorulduğunda aşağıdaki bilgileri kullanarak Wandera Android uygulama yapılandırma ilkesini eklemek için [Android için Microsoft Intune uygulama yapılandırma ilkeleri kullanma](../apps/app-configuration-policies-use-android.md) yönergelerine bakın.

1. **Radar bir portalda**, **yapılandırma ayarları** biçimi altında **Ekle** düğmesine tıklayın.
2. **Yapılandırma anahtarları**listesinden **etkinleştirme profili URL 'sini** seçin. **Tamam** düğmesine tıklayın.
3. **Etkinleştirme profili URL 'si** için **değer türü** menüsünden **dize** ' yi seçin ve ardından, **paylaşılabilir bağlantı URL 'sini** radar içindeki istenen etkinleştirme profilinden kopyalayın.
4. **Intune yönetici konsolu uygulama yapılandırması Kullanıcı arabiriminde**, **Ayarlar**' ı seçin, **yapılandırma ayarlarını tanımlayın > yapılandırma TASARıMCıSıNı kullanın** ve **paylaşılabilir bağlantı URL**'sini yapıştırın.  

> [!NOTE] 
> İOS 'ın aksine, her bir Wandera etkinleştirme profili için benzersiz bir Android kurumsal uygulama yapılandırma ilkesi tanımlamanız gerekir. Birden çok Wandera etkinleştirme profili gerekmiyorsa, tüm hedef cihazlar için tek bir Android uygulama yapılandırması kullanabilirsiniz. Wandera 'da etkinleştirme profilleri oluştururken, Wandera 'nın cihazı UıEM Connect aracılığıyla Intune ile eşitlemesini sağlamak için Ilişkili Kullanıcı Yapılandırması altında "Azure Active Directory" seçeneğini belirlediğinizden emin olun.

- **iOS**
  - İstendiğinde aşağıdaki bilgileri kullanarak Wandera iOS uygulama yapılandırma ilkesini eklemek için [iOS için Microsoft Intune uygulama yapılandırma ilkeleri kullanma](../apps/app-configuration-policies-use-ios.md) yönergelerine bakın.

1. **Radar**bölümünde, **cihazlar > etkinleştirmeleri** ' a gidin ve herhangi bir etkinleştirme profili seçin. **Yönetilen cihazlar > > Microsoft Intune dağıtım stratejileri** ' ne tıklayın ve **iOS uygulama yapılandırma ayarlarını**bulun.  
2. İOS uygulama yapılandırması XML 'sini göstermek ve sistem panonuza kopyalamak için kutuyu genişletin.  
3. **Intune yönetici konsolu uygulama yapılandırması kullanıcı arabirimi ayarları ' nda,** **yapılandırma ayarları BIÇIMINI tanımlayın > XML verisi girin**. 
4. XML 'yi uygulama yapılandırması metin kutusuna yapıştırın.

> [!NOTE]
> Tek bir iOS yapılandırma ilkesi, Wandera ile sağlanacak tüm cihazlarda kullanılabilir.  

## <a name="assigning-mobile-threat-defense-apps-to-end-users-via-intune"></a>Intune aracılığıyla mobil tehdit savunma uygulamalarını son kullanıcılara atama

Mobile Threat Defense uygulamasını Son Kullanıcı cihazına yüklemek için Azure portal aşağıdaki adımları izleyebilirsiniz. İşlemini öğrendiğinizden emin olun:

- [Intune ile gruplara uygulama atama](../apps/apps-deploy.md)

MTD sağlayıcınızı kapsayan bölümü seçin:

- [Lookout for Work](#assigning-lookout-for-work)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [Check Point SandBlast Mobile](#assigning-check-point-sandblast-mobile)
- [Zimperium](#assigning-zimperium)
- [Pradeo](#assigning-pradeo)
- [Better Mobile](#assigning-better-mobile)
- [Sophos Mobile](#assigning-sophos)
- [Wandera](#assigning-wandera)

### <a name="assigning-lookout-for-work"></a>Lookout for Work atama

- **Android**
  - Yönergeler için bkz. [Microsoft Intune'a Android mağazası uygulamaları ekleme](../apps/store-apps-android.md). **AppStore URL 'si**Için bu [Gevbir iş Google App Store URL 'si](https://play.google.com/store/apps/details?id=com.lookout.enterprise) kullanın.

- **iOS**
  - Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **AppStore URL 'si**için bu [Lookout for Work IOS uygulama mağazası URL](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) 'sini kullanın.

- **Apple mağazası dışında Lookout for Work uygulaması**
  - Lookout for Work iOS uygulamasını yeniden imzalamanız gerekir. Lookout, Lookout for Work iOS uygulamasını iOS App Store dışında dağıtır. Uygulamayı dağıtmadan önce, iOS Enterprise Developer Certificate ile yeniden imzalamanız gerekir.  
  - Lookout for Work iOS uygulamalarını yeniden imzalama hakkında ayrıntılı yönergeler için Lookout web sitesinde [Lookout for Work iOS uygulamasını yeniden imzalama işlemine](https://personal.support.lookout.com/hc/articles/114094038714) bakın.

  - **Azure AD kimlik doğrulamasını Lookout for Work iOS uygulaması kullanıcıları için etkinleştirin.**

    1. [Azure portalı](https://portal.azure.com)'na gidin, kimlik bilgilerinizle oturum açın, sonra uygulama sayfasına gidin.

    2. **** Lookout for Work iOS uygulamasını yerel istemci uygulaması**** olarak ekleyin.

    3. IPA’yı imzaladığınızda seçtiğiniz müşteri paketi kimliğini **com.lookout.enterprise.yourcompanyname** ile değiştirin.

    4. Ek yeniden yönlendirme URI 'si ekleyin: ** &lt; CompanyPortal://Code/>** ve ardından özgün yeniden YÖNLENDIRME URI 'nizin URL kodlamalı bir sürümü.

    5. Uygulamanıza **Temsilci İzinleri** ekleyin.

    > [!NOTE]
    > Daha fazla ayrıntı için bkz. [Azure AD ile yerel istemci uygulaması yapılandırma](/azure/app-service/configure-authentication-provider-aad#optional-configure-a-native-client-application).

  - **Lookout for Work ipa dosyasını ekleyin.**

    - Yeniden imzalanan. ipa dosyasını [Intune Ile IOS LOB uygulamaları ekleme](../apps/lob-apps-ios.md) makalesinde açıklandığı gibi karşıya yükleyin. Ayrıca en düşük işletim sistemi sürümünü iOS 8.0 veya üstüne ayarlamanız gerekir.

### <a name="assigning-symantec-endpoint-protection-mobile"></a>Symantec Endpoint Protection Mobile atama

- **Android**
  - Yönergeler için bkz. [Microsoft Intune'a Android mağazası uygulamaları ekleme](../apps/store-apps-android.md). **AppStore URL 'si**Için bu [Sep mobil uygulama mağazası URL 'sini](https://play.google.com/store/apps/details?id=com.skycure.skycure) kullanın.  **En düşük işletim sistemi** için **Android 4.0 (Ice Cream Sandwich)** öğesini seçin.

- **iOS**
  - Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **AppStore URL 'si**Için bu [Sep mobil uygulama mağazası URL 'sini](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) kullanın.

### <a name="assigning-check-point-sandblast-mobile"></a>Check Point SandBlast Mobile atanıyor

- **Android**  
  - Yönergeler için bkz. [Microsoft Intune'a Android mağazası uygulamaları ekleme](../apps/store-apps-android.md). **AppStore URL 'si**Için bu [Check Point sandblast MOBIL uygulama mağazası URL](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) 'sini kullanın.

- **iOS**
  - Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **AppStore URL 'si**Için bu [Check Point sandblast MOBIL uygulama mağazası URL](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) 'sini kullanın.  

### <a name="assigning-zimperium"></a>Zyium atama

- **Android**
  - Yönergeler için bkz. [Microsoft Intune'a Android mağazası uygulamaları ekleme](../apps/store-apps-android.md). **AppStore URL 'si**Için bu [zkusurum uygulama mağazası URL](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) 'sini kullanın.

- **iOS**
  - Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **AppStore URL 'si**Için bu [zkusurum uygulama mağazası URL](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) 'sini kullanın.  
 
### <a name="assigning-pradeo"></a>Pradeo atanıyor

- **Android**
  - Yönergeler için bkz. [Microsoft Intune'a Android mağazası uygulamaları ekleme](../apps/store-apps-android.md). **AppStore URL 'si**Için bu [pradeo uygulama mağazası URL 'sini](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) kullanın.

- **iOS**
  - Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **AppStore URL 'si**Için bu [pradeo uygulama mağazası URL 'sini](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) kullanın.

### <a name="assigning-better-mobile"></a>Daha Iyi mobil atama

- **Android**
  - Yönergeler için bkz. [Microsoft Intune'a Android mağazası uygulamaları ekleme](../apps/store-apps-android.md). **AppStore URL 'si**Için bu [etkin kalkan uygulama mağazası URL 'sini](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) kullanın.

- **iOS**
  - Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **AppStore URL 'si**Için bu [ActiveShield App Store URL 'sini](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) kullanın.

### <a name="assigning-sophos"></a>Sophos atama

- **Android**
  - Yönergeler için bkz. [Microsoft Intune'a Android mağazası uygulamaları ekleme](../apps/store-apps-android.md). **AppStore URL 'si**Için bu [Sophos App Store URL](https://play.google.com/store/apps/details?id=com.sophos.smsec) 'sini kullanın.

- **iOS**
  - Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **AppStore URL 'si**Için bu [ActiveShield App Store URL 'sini](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) kullanın.

### <a name="assigning-wandera"></a>Wandera atanıyor

- **Android**
  - Yönergeler için bkz. [Microsoft Intune'a Android mağazası uygulamaları ekleme](../apps/store-apps-android.md). **AppStore URL 'si**Için bu [Wandera mobil uygulama mağazası URL 'sini](https://play.google.com/store/apps/details?id=com.wandera.android) kullanın. **En düşük işletim sistemi**için **Android 5,0**' i seçin.

- **iOS**
  - Yönergeler için bkz. [Microsoft Intune'a iOS mağazası uygulamaları ekleme](../apps/store-apps-ios.md). **AppStore URL 'si**Için bu [Wandera mobil uygulama mağazası URL 'sini](https://itunes.apple.com/app/wandera/id605469330) kullanın.

## <a name="next-steps"></a>Sonraki adımlar

- [MTD için cihaz uyumluluk ilkesini yapılandırma](mtd-device-compliance-policy-create.md)