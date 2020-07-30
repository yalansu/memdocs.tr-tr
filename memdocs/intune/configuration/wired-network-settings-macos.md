---
title: Microsoft Intune-Azure 'da macOS cihazları için kablolu ağ ayarlarını yapılandırma | Microsoft Docs
titleSuffix: ''
description: MacOS cihazları için kablolu ağ cihazı yapılandırma profili oluşturun veya ekleyin. Farklı ayarları görüntüleyin, sertifika ekleyin, bir EAP türü seçin ve Microsoft Intune bir kimlik doğrulama yöntemi seçin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1da738611dd5fe114054645170d2b49ef12f0523
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334615"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>Microsoft Intune 'de macOS cihazları için kablolu ağ ayarları ekleme

Belirli kablolu ağ ayarlarına sahip bir profil oluşturabilir ve ardından bu profili macOS cihazlarınıza dağıtabilirsiniz. Microsoft Intune, ağınızda kimlik doğrulaması, SCEP sertifikası ekleme ve daha fazlası dahil olmak üzere birçok özellik sunmaktadır.

Bu makalede, yapılandırabileceğiniz ayarlar açıklanmaktadır.

## <a name="before-you-begin"></a>Başlamadan önce

[Kablolu ağ aygıtı yapılandırma profili oluşturun](wired-networks-configure.md).

> [!NOTE]
> Bu ayarlar tüm kayıt türleri için kullanılabilir. Kayıt türleri hakkında daha fazla bilgi için bkz. [MacOS kaydı](../enrollment/macos-enroll.md).

## <a name="wired-network"></a>Kablolu ağ

- **Ağ arabirimi**: hizmet siparişi önceliğine bağlı olarak, profilin uygulandığı cihazdaki ağ arabirimlerini seçin. Seçenekleriniz şunlardır:
  
  - **İlk etkin Ethernet** (varsayılan)
  - **İkinci etkin Ethernet**
  - **Üçüncü etkin Ethernet**
  - **İlk Ethernet**
  - **İkinci Ethernet**
  - **Üçüncü Ethernet**
  - **Herhangi bir Ethernet**

  Başlıkta "etkin" olan seçenekler, cihazda etkin olarak çalışan arabirimler kullanır. Etkin arabirim yoksa, hizmet siparişi önceliğinde bir sonraki arabirim yapılandırılır. Varsayılan olarak, **ilk etkin Ethernet** seçilidir ve bu da MacOS tarafından yapılandırılan varsayılan ayardır.

- **EAP türü**: güvenli kablolu bağlantıların kimliğini doğrulamak Için Genişletilebilir Kimlik Doğrulama Protokolü (EAP) türünü seçin. Seçenekleriniz şunlardır:

  - **EAP-FAST**: **Korumalı Erişim Kimlik Bilgisi (PAC) Ayarları**’nı girin. Bu seçenek, istemci ile kimlik doğrulama sunucusu arasında kimliği doğrulanmış bir tünel oluşturmak için korumalı erişim kimlik bilgilerini kullanır. Seçenekleriniz şunlardır:
    - **(PAC) kullanma**
    - **(PAC) kullan**: Mevcut bir PAC dosyası varsa bunu kullanın.
    - **PAC’yi kullan ve sağla**: PAC dosyasını oluşturun ve cihazlarınıza sağlayın.
    - **PAC’yi anonim olarak kullan ve sağla**: PAC dosyasını sunucuda kimlik doğrulamadan oluşturun ve cihazlarınıza ekleyin.

  - **EAP-TLS**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sertifika sunucusu adları**: güvenilen sertifika yetkiliniz (CA) tarafından verilen sertifikalarda kullanılan bir veya daha fazla ortak ad **ekleyin** . Bu bilgileri girdiğinizde, bu ağa bağlandıklarında Kullanıcı cihazlarında gösterilen dinamik güven penceresini atlayabilirsiniz.
    - **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur. Bağlantının kimliğini doğrulamak için kullanılır.
    - **Istemci kimlik doğrulaması**  -  **Sertifikalar**: cihaza de dağıtılan SCEP istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir. PKCS sertifikaları desteklenmez.
    - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

  - **EAP-TTLS**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sertifika sunucusu adları**: güvenilen sertifika yetkiliniz (CA) tarafından verilen sertifikalarda kullanılan bir veya daha fazla ortak ad **ekleyin** . Bu bilgileri girdiğinizde, bu ağa bağlandıklarında Kullanıcı cihazlarında gösterilen dinamik güven penceresini atlayabilirsiniz.
    - **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur. Bağlantının kimliğini doğrulamak için kullanılır.
    - **Istemci kimlik doğrulaması**: bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:
      - Kullanıcı adı **ve parola**: kullanıcıdan bağlantının kimliğini doğrulamak için bir Kullanıcı adı ve parola ister. Şunları da girin:
        - **EAP olmayan Yöntem (iç kimlik)**: bağlantının kimliğini nasıl doğrulayacağınızı seçin. Ağınızda yapılandırılmış olan protokolü seçtiğinizden emin olun. Seçenekleriniz şunlardır:
          - **Şifrelenmemiş parola (PAP)**
          - **Karşılıklı Kimlik Doğrulama Protokolü (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Sürüm 2 (MS-CHAP v2)**
      - **Sertifikalar**: cihaza de dağıtılan SCEP istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir. PKCS sertifikaları desteklenmez.
      - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

  - **LEAP**

  - **PEAP**: Ayrıca şunları girin:

    - **Sunucu güveni**  -  **Sertifika sunucusu adları**: güvenilen sertifika yetkiliniz (CA) tarafından verilen sertifikalarda kullanılan bir veya daha fazla ortak ad **ekleyin** . Bu bilgileri girdiğinizde, bu ağa bağlandıklarında Kullanıcı cihazlarında gösterilen dinamik güven penceresini atlayabilirsiniz.
    - **Sunucu doğrulaması Için kök sertifika**: var olan bir güvenilen kök sertifika profilini seçin. İstemci ağa bağlandığı zaman, bu sertifika sunucuya sunulur. Bağlantının kimliğini doğrulamak için kullanılır.
    - **Istemci kimlik doğrulaması**: bir **kimlik doğrulama yöntemi**seçin. Seçenekleriniz şunlardır:
      - Kullanıcı adı **ve parola**: kullanıcıdan bağlantının kimliğini doğrulamak için bir Kullanıcı adı ve parola ister.
      - **Sertifikalar**: cihaza de dağıtılan SCEP istemci sertifikası profilini seçin. Bu sertifika, bağlantının kimliğini doğrulamak için cihaz tarafından sunucuya sunulan kimliktir. PKCS sertifikaları desteklenmez.
      - **Kimlik gizliliği (dış kimlik)**: EAP kimlik isteğine yanıt olarak gönderilen metni girin. Bu metin herhangi bir değer olabilir, örneğin `anonymous`. Kimlik doğrulaması sırasında başlangıçta bu anonim kimlik gönderilir ve ardından güvenli bir tünelde gerçek kimlik gönderilir.

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturuldu, ancak herhangi bir şey olmayabilir. [Bu profili atadığınızdan](device-profile-assign.md)emin olun ve [durumunu izleyin](device-profile-monitor.md).
