---
title: Microsoft Intune-Azure 'da Android Enterprise için VPN ayarlarını kullanma | Microsoft Docs
description: Microsoft Intune 'de Android kurumsal cihazlarda VPN bağlantıları oluşturmak için tüm ayarları görüntüleyin. VPN sunucusunun bağlantı adını, IP adresini veya FQDN 'sini girin, kullanıcıların kimlik doğrulamasını yapın ve Citrix, SonicWall, Check Point kapsül ve Pulse Secure bağlantı türlerini seçin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87e6484939324abc5566386ffbe48f04ddbbe100
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146465"
---
# <a name="android-enterprise-device-settings-to-configure-vpn-in-intune"></a>Intune 'da VPN yapılandırmak için Android kurumsal cihaz ayarları

Bu makalede, Android kurumsal cihazlarda denetleyebilmeniz için kullanabileceğiniz farklı VPN bağlantısı ayarları listelenir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, bu ayarları kullanarak bir VPN bağlantısı oluşturun, VPN 'in kimlik doğrulamasını yapın, bir VPN sunucusu türü seçin ve daha fazlasını yapın.

Bir Intune Yöneticisi olarak, Android kurumsal cihazlarına VPN ayarları oluşturabilir ve atayabilirsiniz. 

Intune 'da VPN profilleri hakkında daha fazla bilgi edinmek için bkz. [VPN profilleri](vpn-settings-configure.md).

> [!NOTE]
> Always on VPN 'yi yapılandırmak için, bir VPN profili oluşturmanız ve ayrıca her zaman açık VPN ayarıyla bir [cihaz kısıtlamaları](device-restrictions-android-for-work.md#connectivity) profili oluşturmanız gerekir.

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](vpn-settings-configure.md)ve **Android kurumsal**' i seçin.

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Tam olarak yönetilen, adanmış ve şirkete ait Iş profili

- **Bağlantı adı**: Bu bağlantı için bir ad girin. Cihazlarındaki kullanılabilir VPN bağlantılarına göz atan son kullanıcılar bu adı görür. Örneğin, `Contoso VPN` girin.
- **IP adresi veya FQDN**: Cihazların bağlandığı VPN sunucusunun IP adresini veya tam etki alanı adını (FQDN) girin. Örneğin, **192.168.1.1** veya **vpn.contoso.com** yazın.

  - **Kimlik doğrulama yöntemi**: Cihazların VPN sunucusunda kimliklerini nasıl doğrulayacaklarını seçin. Seçenekleriniz şunlardır:
  
    - **Sertifikalar**: Bağlantının kimliğini doğrulamak için mevcut bir SCEP veya PKCS sertifika profili seçin. [Sertifikaları yapılandırın](../protect/certificates-configure.md), sertifika profili oluşturma adımlarını listeler.
    - **Kullanıcı adı ve parola**: VPN sunucusunda oturum açarken son kullanıcılardan Kullanıcı adını ve parolasını girmesi istenir.

- **Bağlantı türü**: VPN bağlantısının türünü seçin. Seçenekleriniz şunlardır:

  - **Cisco AnyConnect**
  - **F5 Access**
  - **Pulse Secure**

## <a name="work-profile-only"></a>Yalnızca iş profili

- **Bağlantı adı**: Bu bağlantı için bir ad girin. Cihazlarındaki kullanılabilir VPN bağlantılarına göz atan son kullanıcılar bu adı görür. Örneğin, `Contoso VPN` girin.
- **IP adresi veya FQDN**: Cihazların bağlandığı VPN sunucusunun IP adresini veya tam etki alanı adını (FQDN) girin. Örneğin, **192.168.1.1** veya **vpn.contoso.com** yazın.

  - **Kimlik doğrulama yöntemi**: Cihazların VPN sunucusunda kimliklerini nasıl doğrulayacaklarını seçin. Seçenekleriniz şunlardır:
  
    - **Sertifikalar**: Bağlantının kimliğini doğrulamak için mevcut bir SCEP veya PKCS sertifika profili seçin. [Sertifikaları yapılandırın](../protect/certificates-configure.md), sertifika profili oluşturma adımlarını listeler.
    - **Kullanıcı adı ve parola**: VPN sunucusunda oturum açarken son kullanıcılardan Kullanıcı adını ve parolasını girmesi istenir.

- **Bağlantı türü**: VPN bağlantısının türünü seçin. Seçenekleriniz şunlardır:

  - **Cisco AnyConnect**
  - **F5 Access**
  - **Pulse Secure**
  - **SonicWall Mobile Connect**
  - **Check Point Capsule VPN**

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[Android](vpn-settings-android.md), [IOS/ıpados](vpn-settings-ios.md), [MacOS](vpn-settings-macos.md), [Windows 10 ve üzeri](vpn-settings-windows-10.md)ve [Windows 8.1](vpn-settings-windows-8-1.md)için de VPN profilleri oluşturabilirsiniz.
