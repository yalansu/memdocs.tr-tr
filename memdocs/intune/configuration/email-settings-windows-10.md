---
title: Microsoft Intune - Azure’da Windows 10 cihazlar için e-posta ayarları | Microsoft Docs
description: Exchange sunucularını kullanan ve Azure Active Directory’den öznitelik alan bir cihaz yapılandırma e-posta profili oluşturun. Microsoft Intune kullanarak SSL’yi de etkinleştirebilir ve Windows 10 cihazlarda e-posta ve zamanlamaları eşitleyebilirsiniz.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0cd3505d0a0067adfe9082d7aa3882f3421a2183
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429598"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>Microsoft Intune 'de Windows 10 çalıştıran cihazlar için e-posta profili ayarları

Windows 10 ve daha yeni çalıştıran cihazlarınızda posta uygulamasını yapılandırmak için e-posta profili ayarlarını kullanın.

## <a name="before-you-begin"></a>Başlamadan önce

[Profili oluşturun](email-settings-configure.md).

## <a name="email-settings"></a>E-posta ayarları

- **E-posta sunucusu**: Exchange sunucunuzun konak adını girin. Örneğin, `outlook.office365.com` girin.
- **Hesap adı**: E-posta hesabı için görünen adı girin. Bu ad, cihazlarda kullanıcılara gösterilir.
- **AAD’den kullanıcı adı özniteliği**: Bu ad, Intune’un Azure Active Directory’den (AAD) aldığı özniteliktir. Intune, bu profil tarafından kullanılan kullanıcı adını dinamik olarak oluşturur. Seçenekleriniz şunlardır:
  - **Kullanıcı asıl adı**: veya gibi adı alır `user1` `user1@contoso.com` .
  - **BIRINCIL SMTP adresi**: adı gibi e-posta adresi biçiminde alır `user1@contoso.com` .
  - **sAM Hesap Adı**: Etki alanı gerektirir; örneğin `domain\user1`. Şunları da girin:  
    - **Kullanıcı etki alanı adı kaynağı**: **AAD** (Azure Active Directory) veya **özel**seçeneğini belirleyin.

      **AAD**'den öznitelikleri alırken, şunu da girin:
      - **AAD 'Den Kullanıcı etki alanı adı özniteliği**: kullanıcının **tam etki alanı adını** veya **NetBIOS adı** özniteliğini almayı seçin.

      **Özel** öznitelikleri kullanırken, şunu da girin:
      - **Kullanılacak özel etki alanı adı**: Intune 'un veya gibi etki alanı adı için kullandığı bir değer girin `contoso.com` `contoso` .

- **AAD 'Den e-posta adresi özniteliği**: Intune bu özniteliği Azure ACTIVE DIRECTORY (AAD) öğesinden alır. Kullanıcının e-posta adresinin nasıl oluşturulduğunu seçin. Seçenekleriniz şunlardır:
  - **Kullanıcı asıl adı**: veya gibi, e-posta adresi olarak tam asıl adı kullanır `user1@contoso.com` `user1` .
  - **BIRINCIL SMTP adresi**: Exchange 'de oturum açmak IÇIN birincil SMTP adresini kullanır `user1@contoso.com` .

### <a name="security"></a>Güvenlik

- **SSL**: **Etkinleştir** olarak belirlenirse e-posta gönderirken, alırken ve Exchange sunucusuyla iletişim kurulurken Güvenli Yuva Katmanı (SSL) iletişimi kullanılır. **Devre dışı bırak** , SSL gerektirmez.

### <a name="synchronization"></a>Eşitleme

- **Eşitlenmesi gereken e-posta miktarı**: e-postanın eşitlenmesini istediğiniz gün sayısını seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Tüm kullanılabilir e-postaları eşleştirmek için **sınırsız** seçeneğini belirleyin.
- **Eşitleme zamanlaması**: Cihazların Exchange sunucusundan veri eşitleyeceği zamanlamayı seçin. Ayrıca, verileri geldikçe, verileri eşitleyen **ileti geldikçe**seçeneğini de belirleyebilirsiniz. Ya da, cihaz kullanıcısının eşitlemeyi başlattığı şekilde **el ile** ' yi seçin.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

### <a name="content-sync"></a>İçerik eşitleme

- **Eşitlenecek içerik türü**: cihazlara eşitlemek istediğiniz içerik türlerini seçin. Seçenekleriniz şunlardır:
  - **Kişiler**: **ilgili** kişileri eşitler. **Kapalı** , kişileri otomatik olarak eşitetmez. Kullanıcılar el ile eşitleniyor.
  - **Takvim**: **tarihinde** takvimi eşitler. **Kapalı** , kişileri otomatik olarak eşitetmez. Kullanıcılar el ile eşitleniyor.
  - **Görevler**: **üzerinde** görevleri eşitler. **Kapalı** , görevleri otomatik olarak eşitetmez. Kullanıcılar el ile eşitleniyor.

## <a name="next-steps"></a>Sonraki adımlar

[Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md)ve [iOS/ıpados](email-settings-ios.md)'daki e-posta ayarlarını da yapılandırabilirsiniz. 

[Intune 'da e-posta ayarları hakkında daha fazla bilgi edinin](email-settings-configure.md).

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).
