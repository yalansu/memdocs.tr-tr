---
title: VPN ayarlarını Microsoft Intune-Azure 'da macOS cihazlarına yapılandırma | Microsoft Docs
description: Microsoft Intune bir sanal özel ağ (VPN) yapılandırma profili ekleyin veya oluşturun. MacOS çalıştıran cihazlarda bağlantı ayrıntılarını, bölünmüş tüneli, özel VPN ayarlarını tanımlayıcı, anahtar ve değer çiftleri, bir yapılandırma betiği, IP veya FQDN adresi ve TCP bağlantı noktası ile birlikte Microsoft Intune ekleyin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 581e39ddbd50d4c2aeb4001b73c1492a3a799f90
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814765"
---
# <a name="add-vpn-settings-on-macos-devices-in-microsoft-intune"></a>Microsoft Intune 'de macOS cihazlarına VPN ayarları ekleme

Bu makale, macOS çalıştıran cihazlarda VPN bağlantılarını yapılandırmak için kullanabileceğiniz Intune ayarları hakkında bilgi sağlar.

Seçtiğiniz ayarlara bağlı olarak, aşağıdaki listede yer alan değerlerden bazıları yapılandırılamaz.

## <a name="before-you-begin"></a>Başlamadan önce

[MacOS VPN cihaz yapılandırma profili](vpn-settings-configure.md)oluşturun.

> [!NOTE]
> Bu ayarlar tüm kayıt türleri için kullanılabilir. Kayıt türleri hakkında daha fazla bilgi için bkz. [MacOS kaydı](../enrollment/macos-enroll.md).

## <a name="base-vpn-settings"></a>Temel VPN ayarları

**Bağlantı adı**: Bu bağlantı için bir ad girin. Cihazlarındaki kullanılabilir VPN bağlantılarına göz atan son kullanıcılar bu adı görür.

- **IP adresi veya FQDN**: CIHAZLARıN bağlanacağı VPN sunucusunun IP adresini veya tam etki alanı adını girin. Örneğin `192.168.1.1` veya `vpn.contoso.com` girin.
- **Kimlik doğrulama yöntemi**: Cihazların VPN sunucusunda kimliklerini nasıl doğrulayacaklarını seçin. Seçenekleriniz şunlardır:
  - **Sertifikalar**: **kimlik doğrulama sertifikası**altında, bağlantının kimliğini doğrulamak için daha önce oluşturduğunuz bir SCEP veya PKCS sertifika profilini seçin. Sertifika profilleri hakkındaki daha fazla bilgi için bkz. [Sertifikaları yapılandırma](../protect/certificates-configure.md).
  - **Kullanıcı adı ve parola**: son kullanıcılar VPN sunucusunda oturum açmak için bir Kullanıcı adı ve parola sağlamalıdır.
- **Bağlantı türü**: Aşağıdaki satıcı listesinden VPN bağlantı türünü seçin:
  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **NetMotion Mobility**
  - **Pulse Secure**
  - **Özel VPN**: VPN satıcınız listede yoksa bu seçeneği belirleyin. Ayrıca şunları yapılandırın:

    - **VPN tanımlayıcısı**: kullanmakta olduğunuz VPN uygulaması için bir tanımlayıcı girin. Bu tanımlayıcı, VPN sağlayıcınız tarafından sağlanır.
    - **Özel VPN öznitelikleri için anahtar ve değer çiftlerini girin**: VPN bağlantınızı özelleştiren **Anahtarlar** ve **Değerler**’i ekleyin veya içeri aktarın. Bu değerler genellikle VPN sağlayıcınız tarafından sağlanır.

- **Bölünmüş tünel**: cihazların trafiğe bağlı olarak hangi bağlantının kullanılacağına karar vermesine olanak sağlayan bu seçeneği **etkinleştirin** veya **devre dışı bırakın** . Örneğin, oteldeki bir kullanıcı çalışma dosyalarına erişmek için VPN bağlantısını, web’e göz atmak için ise otelin standart ağını kullanır.

## <a name="automatic-vpn"></a>Otomatik VPN

- **İsteğe bağlı VPN**: Isteğe bağlı VPN, VPN bağlantısını otomatik olarak bağlamak veya bağlantısını kesmek için kuralları kullanır. Cihazlarınız VPN 'e bağlanmayı denediklerinde, eşleşen bir IP adresi veya etki alanı adı gibi, oluşturduğunuz parametrelerde ve kurallarda eşleşme arar. Bir eşleşme varsa, seçtiğiniz eylem çalışır.

  Örneğin, yalnızca cihaz şirketin Wi-Fi ağına bağlı olmadığında VPN bağlantısının kullanılacağı bir koşul oluşturun. Ya da bir cihaz, girdiğiniz bir DNS arama etki alanına erişemezse VPN bağlantısı başlatılmaz.

  - **Ekle**: bir kural eklemek için bu seçeneği belirleyin.

  - **Şunları yapmak istiyorum**: cihaz değeri ile isteğe bağlı kuralınız arasında bir eşleşme varsa, eylemi seçin. Seçenekleriniz şunlardır:

    - VPN oluşturma
    - VPN bağlantısını kes
    - Her bağlantı denemesini değerlendir
    - Yoksayma

  - **Kısıtlamak**istiyorum: kuralın karşılaması gereken koşulu seçin. Seçenekleriniz şunlardır:

    - **Belirli SSID**'ler: kuralın uygulanacağı bir veya daha fazla kablosuz ağ adı girin. Bu ağ adı hizmet kümesi tanımlayıcısıdır (SSID). Örneğin, `Contoso VPN` girin.
    - **Belırlı DNS etki alanları**: kuralın uygulanacağı bir veya daha fazla DNS etki alanı girin. Örneğin, `contoso.com` girin.
    - **Tüm etki alanları**: kuralınızı kuruluşunuzdaki tüm etki alanlarına uygulamak için bu seçeneği belirleyin.

  - **Ancak, yalnızca bu URL araştırması başarılı**olursa: isteğe bağlı. Kuralın test olarak kullanacağı bir URL girin. Cihaz bu URL 'ye yeniden yönlendirmesiz erişirse VPN bağlantısı başlatılır. Cihaz hedef URL’ye bağlanır. Kullanıcı, URL dize araştırma sitesini görmez.

    Örneğin, URL dize araştırması, VPN 'i bağlamadan önce cihaz uyumluluğunu denetleyen bir denetim Web sunucusu URL 'sidir. Ya da URL, VPN aracılığıyla hedef URL 'ye bağlanmadan önce VPN 'in bir siteye bağlanma yeteneğini sınar.

- **Kullanıcıların OTOMATIK VPN 'yi devre dışı bırakmasını engelle**: seçenekleriniz:

  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Evet**: KULLANıCıLARıN otomatik VPN 'yi kapatmasını engeller. Kullanıcıları otomatik VPN 'nin etkin ve çalışır durumda tutmaya zorlar.
  - **Hayır**: KULLANıCıLARıN otomatik VPN 'yi kapatmasına izin verir.

  Bu ayarın geçerli olduğu sürümler:  
  - macOS 11 ve üzeri (büyük sur)

- **Uygulama BAŞıNA VPN**: Bu VPN bağlantısını bir MacOS uygulamasıyla ilişkilendirerek uygulama başına VPN 'yi sunar. Uygulama çalıştığında VPN bağlantısı başlar. Yazılımı atarken VPN profilini bir uygulamayla ilişkilendirebilirsiniz. Daha fazla bilgi için bkz. [uygulamaları atama ve izleme](../apps/apps-deploy.md).

  - **Bu VPN’i tetikleyecek Safari URL’leri**: Bir veya daha fazla web sitesi URL’si ekleyin. Bu URL’ler cihazda Safari tarayıcıyla ziyaret edildiğinde, VPN bağlantısı otomatik olarak kurulur.

  - **Ilişkili etki alanları**: VPN profilindeki ilişkili etkı alanlarını VPN bağlantısını otomatik olarak başlatacak şekilde girin. Örneğin, `contoso.com` girin. `contoso.com`Etki alanındaki CIHAZLAR VPN bağlantısını otomatik olarak başlatır.

    Daha fazla bilgi için bkz. [ilişkili etki alanları](device-features-configure.md#associated-domains).

  - **Dışlanan etki alanları**: uygulama başına VPN bağlıyken VPN bağlantısını atlayabileceğiniz etki alanlarını girin. Örneğin, `contoso.com` girin. `contoso.com`Etki alanındaki cihazlar, uygulama BAŞıNA VPN bağlantısını başlatamaz veya kullanmaz. `contoso.com`Etki alanındaki cihazlar, genel Internet 'i kullanacaktır.

  - **Kullanıcıların OTOMATIK VPN 'yi devre dışı bırakmasını engelle**: seçenekleriniz:

    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Evet**: KULLANıCıLARıN otomatik VPN 'yi kapatmasını engeller. Kullanıcıları otomatik VPN 'nin etkin ve çalışır durumda tutmaya zorlar.
    - **Hayır**: KULLANıCıLARıN otomatik VPN 'yi kapatmasına izin verir.

    Bu ayarın geçerli olduğu sürümler:  
    - macOS 11 ve üzeri (büyük sur)

## <a name="proxy-settings"></a>Proxy ayarları

- **Otomatik yapılandırma betiği**: Proxy sunucusunu yapılandırmak için bir dosya kullanın. Yapılandırma dosyasını içeren **Proxy sunucu URL'sini** girin. Örneğin, `http://proxy.contoso.com` girin.
- **Adres**: proxy sunucu adresini (bir IP adresi olarak) girin.
- **Bağlantı noktası numarası**: Proxy sunucusuyla ilişkilendirilmiş bağlantı noktası numarasını girin.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu, ancak henüz bir şey yapmamış olabilir. [Profili atadığınızdan](device-profile-assign.md)emin olun ve [durumunu izleyin](device-profile-monitor.md).

[Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [IOS/ıpados](vpn-settings-ios.md)ve [Windows 10](vpn-settings-windows-10.md) cihazlarında VPN ayarlarını yapılandırın.
