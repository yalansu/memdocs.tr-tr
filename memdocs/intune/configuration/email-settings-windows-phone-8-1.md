---
title: Windows Phone 8.1 için Microsoft Intune e-posta ayarları
titleSuffix: ''
description: Windows Phone 8.1 çalıştıran cihazlarda e-posta bağlantılarını yapılandırmak için kullanabileceğiniz Intune ayarlarını öğrenin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 369e856b26ecbf8a7d6d7f8c0a87a9bfdf69e318
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086922"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>Windows Phone 8.1 çalıştıran cihazlar için Microsoft Intune'da e-posta profili ayarları

Bu makalede, Windows Phone 8.1 çalıştıran cihazlarınız için yapılandırabileceğiniz e-posta profili ayarları gösterilmektedir.

>[!IMPORTANT]
>Windows Phone 8,1 e-posta profilleri Windows 10 cihazlarına da uygulanır.

## <a name="before-you-begin"></a>Başlamadan önce

[Windows Phone 8,1 e-posta profili oluşturun](email-settings-configure.md).

## <a name="email-settings"></a>E-posta ayarları

- **E-posta sunucusu**: Exchange sunucunuzun konak adını girin. Örneğin, şunu girin: `outlook.office365.com`.
- **Hesap adı**: E-posta hesabı için görünen adı girin. Bu ad, cihazlarda kullanıcılara gösterilir.
- **AAD’den kullanıcı adı özniteliği**: Bu ad, Intune’un Azure Active Directory’den (AAD) aldığı özniteliktir. Intune, bu profil tarafından kullanılan kullanıcı adını dinamik olarak oluşturur. Seçenekleriniz şunlardır:
  - **Kullanıcı asıl adı**: `user1` veya `user1@contoso.com`gibi adı alır.
  - **BIRINCIL SMTP adresi**: `user1@contoso.com`gibi, e-posta adresi biçimindeki adı alır.
  - **sAM Hesap Adı**: Etki alanı gerektirir; örneğin `domain\user1`. Şunları da girin:
    - **Kullanıcı etki alanı adı kaynağı**: seçenekleriniz:
      - **AAD** (Azure Active Directory): **AAD 'den Kullanıcı etki alanı adı özniteliğini**girin. Kullanıcının **tam etki alanı adını** veya **NetBIOS adı** özniteliğini almayı seçin.
      - **Özel**: **kullanılacak özel etki alanı adını**girin. Intune 'un `contoso.com` veya `contoso`gibi etki alanı adı için kullandığı bir değer girin.

- **AAD 'Den e-posta adresi özniteliği**: Intune bu özniteliği Azure ACTIVE DIRECTORY (AAD) öğesinden alır. Kullanıcının e-posta adresinin nasıl oluşturulduğunu seçin. Seçenekleriniz şunlardır:
  - **Kullanıcı asıl adı**: `user1@contoso.com` veya `user1`gibi, e-posta adresi olarak tam asıl adı kullanır.
  - **BIRINCIL SMTP adresi**: `user1@contoso.com`gibi Exchange 'de oturum açmak IÇIN birincil SMTP adresini kullanır.

## <a name="security-settings"></a>Güvenlik ayarları

- **SSL**: **Etkinleştir** olarak belirlenirse e-posta gönderirken, alırken ve Exchange sunucusuyla iletişim kurulurken Güvenli Yuva Katmanı (SSL) iletişimi kullanılır. **Devre dışı bırak** , SSL gerektirmez.

## <a name="synchronization-settings"></a>Eşitleme ayarları

- **Eşitlenecek e-posta miktarı**: Eşitlemek istediğiniz e-posta için gün sayısını seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Tüm kullanılabilir e-postaları eşleştirmek için **sınırsız** seçeneğini belirleyin.
- **Eşitleme zamanlaması**: Cihazların Exchange sunucusundan veri eşitleyeceği zamanlamayı seçin. Ayrıca, verileri geldikçe, verileri eşitleyen **ileti geldikçe**seçeneğini de belirleyebilirsiniz. Ya da, cihaz kullanıcısının eşitlemeyi başlattığı şekilde **el ile** ' yi seçin.

## <a name="content-sync-settings"></a>İçerik eşitleme ayarları

- **Eşitlenecek içerik türü**: cihazlara eşitlemek istediğiniz içerik türlerini seçin:
  - **Kişiler**: **ilgili** kişileri eşitler. **Kapalı** , kişileri otomatik olarak eşitetmez. Kullanıcılar el ile eşitleniyor.
  - **Takvim**: **tarihinde** takvimi eşitler. **Kapalı** , kişileri otomatik olarak eşitetmez. Kullanıcılar el ile eşitleniyor.
  - **Görevler**: **üzerinde** görevleri eşitler. **Kapalı** , görevleri otomatik olarak eşitetmez. Kullanıcılar el ile eşitleniyor.

## <a name="next-steps"></a>Sonraki adımlar

[Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), [IOS/ıpados](email-settings-ios.md)ve [Windows 10](email-settings-windows-10.md)' da e-posta ayarlarını da yapılandırabilirsiniz.

[Intune 'da e-posta ayarlarını yapılandırın](email-settings-configure.md).
