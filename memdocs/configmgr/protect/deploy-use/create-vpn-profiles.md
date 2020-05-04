---
title: VPN profilleri oluşturma
titleSuffix: Configuration Manager
description: Configuration Manager 'de VPN profilleri oluşturmayı öğrenin.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713600"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Configuration Manager 'de VPN profilleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager birden çok VPN bağlantı türünü destekler. Farklı cihaz platformları için kullanılabilen bağlantı türleri hakkında daha fazla bilgi için bkz. [VPN profilleri](vpn-profiles.md).

Üçüncü taraf VPN bağlantıları için VPN profilini dağıtmadan önce VPN uygulamasını dağıtın. Uygulamayı dağıtmazsanız, kullanıcılardan VPN 'e bağlanmayı denediğinde bunu yapması istenir. Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md).

## <a name="create-a-vpn-profile"></a>VPN profili oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin, **Şirket kaynağına erişim**' i genişletin ve **VPN profilleri** düğümünü seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **VPN profili oluştur**' u seçin.

1. VPN profili oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdaki bilgileri belirtin:

    - **Ad**: konsolunda VPN profilini tanımlamak için benzersiz bir ad girin.

        > [!NOTE]
        > VPN profili adında şu karakterleri kullanmayın: `\/:*?<>|; `. Windows VPN profili, bu özel karakterleri desteklemez.

    - **Açıklama**: isteğe bağlı olarak, VPN profili hakkında daha fazla bilgi sağlamak için bir açıklama girin.

    - **VPN profili türü**: uygun platformu seçin.

        **Windows 8.1** platformunu seçerseniz, **dosyadan de aktarabilirsiniz**. Bu eylem, bir XML dosyasından VPN profili bilgilerini içeri aktarır. Bu seçeneği belirlerseniz, sihirbazın geri kalanı aşağıdaki sayfalara basitleştirir: **Desteklenen platformlar** ve **VPN profili içeri aktarma**.

1. **Desteklenen platformlar** sayfasında, bu VPN profilinin desteklediği işletim sistemi sürümlerini seçin.

1. **Bağlantı** sayfasında, aşağıdaki bilgileri belirtin:

    - **Bağlantı türü**: VPN bağlantı türünü seçin. Desteklenen türler hakkında daha fazla bilgi için bkz. [VPN profilleri](vpn-profiles.md).

    - **Sunucu listesi**: VPN bağlantısı için kullanmak üzere yeni bir sunucu ekleyin. Bağlantı türüne bağlı olarak, bir veya daha fazla VPN sunucusu ekleyebilir ve hangi sunucunun varsayılan olduğunu belirtebilirsiniz.

    - **Şirket ağına BAĞLıYKEN VPN 'ı atla**: istemcileri iç AĞıNıZDA olduklarında VPN 'Yi kullanamayacak şekilde yapılandırın. Gerekirse, bağlantıya özgü bir DNS adı belirtin.

1. Sihirbazın **kimlik doğrulama yöntemi** sayfasında, bağlantı türü tarafından desteklenen bir yöntem seçin. Bu sayfadaki ayarlar ve kullanılabilir seçenekler, seçilen bağlantı türüne bağlı olarak değişir. Daha fazla bilgi için bkz. [kimlik doğrulama yöntemi başvurusu](#bkmk_auth).

1. **Proxy ayarları** SAYFASıNDA, VPN 'niz bir ara sunucu kullanıyorsa, ortamınız için uygun olan seçeneklerden birini seçin. Ardından, proxy için yapılandırma bilgilerini sağlayın.

1. **Uygulamalar** sayfası yalnızca Windows 10 profilleri için geçerlidir. Bu VPN 'e otomatik olarak bağlanan masaüstü ve evrensel uygulamalar ekleyin. Uygulamanın türü uygulama tanımlayıcısını belirler:

    - Bir *Masaüstü uygulaması*için, uygulamanın dosya yolunu sağlayın.

    - Bir *evrensel uygulama*için paket aile adını (PFN) sağlayın. Bir uygulama için PFN 'yi bulma hakkında bilgi edinmek için bkz. [uygulama BAŞıNA VPN için paket aile adı bulma](find-a-pfn-for-per-app-vpn.md).

    Ayrıca **, yalnızca listelenen uygulamaların bu VPN 'yi kullanabilmesi için**bir seçenek yapılandırabilirsiniz.

    > [!IMPORTANT]
    > Uygulama başına VPN 'yi yapılandırmak için derleyebileceğiniz ilişkili tüm uygulamalar listesini güvenli hale getirin. Yetkisiz bir kullanıcı listenizi değiştirirse ve uygulamayı uygulama başına VPN uygulama listesine aktarırsanız, erişimi olmayan uygulamalara VPN erişimini yetkilendirebilirsiniz.

1. **Sınırlar** sayfası VPN sınırlarını yapılandırmak Için yalnızca Windows 10 profilleri için geçerlidir. Aşağıdaki seçenekleri ekleyebilirsiniz:

    - **Ağ trafiği kuralları**: VPN bağlantısı için etkinleştirmek üzere protokolleri, yerel bağlantı noktasını, uzak bağlantı noktasını ve adres aralıklarını ayarlayın.  

        > [!Note]
        > Bir ağ trafiği kuralı oluşturmazsanız, tüm protokoller, bağlantı noktaları ve adres aralıkları etkinleştirilir. Bir kural oluşturduktan sonra, VPN bağlantısı tarafından yalnızca bu kuralda veya ek kurallarda belirttiğiniz protokoller, bağlantı noktaları ve adres aralıkları kullanılır.

    - **DNS adları ve sunucuları**: cihaz bağlantıyı KURDUKTAN sonra VPN bağlantısı tarafından kullanılan DNS sunucuları.

    - **Rotalar**: VPN bağlantısını kullanan ağ yolları. 60 ' den fazla yolun oluşturulması ilkenin başarısız olmasına neden olabilir.

1. Sihirbazı tamamlayın.

Yeni VPN profili **Varlıklar ve Uyum** çalışma alanında **VPN Profilleri** düğümünde görüntülenir.

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a>Kimlik doğrulama yöntemi başvurusu

Kullanılabilir VPN kimlik doğrulama yöntemleri bağlantı türüne bağlıdır:

### <a name="certificates"></a>Sertifikalar

İstemci sertifikası, bir ağ Ilkesi sunucusu gibi bir RADIUS sunucusunda kimlik doğrulaması gerçekleştiriyorsa, sertifikadaki Konu Alternatif adını Kullanıcı asıl adına ayarlayın.

Desteklenen bağlantı türleri:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="username-and-password"></a>Kullanıcı adı ve Parola

Desteklenen bağlantı türleri:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

Desteklenen bağlantı türleri:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Microsoft Korumalı EAP (PEAP

Desteklenen bağlantı türleri:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Microsoft güvenli parola (EAP-MSCHAP v2)

Desteklenen bağlantı türleri:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Akıllı Kart veya başka sertifika

Desteklenen bağlantı türleri:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Desteklenen bağlantı türleri:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Makine sertifikalarını kullan

Desteklenen bağlantı türleri:

- IKEv2

### <a name="additional-authentication-options"></a>Ek kimlik doğrulama seçenekleri

Windows istemci sürümü destekliyorsa, kimlik doğrulama yöntemini **yapılandırma** seçeneği kullanılabilir. Bu seçenek, kimlik doğrulama yöntemini yapılandırmak için Windows özellikleri penceresini açar.

Seçilen seçeneklere bağlı olarak, daha fazla bilgi belirtmeniz istenebilir, örneğin:

- **Her oturum açmada kullanıcı kimlik bilgilerini hatırla**: Kullanıcı kimlik bilgileri hatırlanır, böylece kullanıcılar her bağlandıklarında onları girmeye gerek kalmaz.  

- **İstemci kimlik doğrulaması için bir istemci sertifikası seçin**: VPN bağlantısının kimliğini doğrulamak için önceden oluşturulmuş BIR istemci SCEP sertifika profili seçin. Daha fazla bilgi için bkz. [PFX Sertifika profilleri oluşturma](create-certificate-profiles.md).

## <a name="next-steps"></a>Sonraki adımlar

- Üçüncü taraf VPN bağlantıları için VPN profilini dağıtmadan önce VPN uygulamasını dağıtın. Uygulamayı dağıtmazsanız, kullanıcılardan VPN 'e bağlanmayı denediğinde bunu yapması istenir. Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md).

- VPN profilini dağıtın. Daha fazla bilgi için bkz. [profilleri dağıtma](deploy-wifi-vpn-email-cert-profiles.md).
