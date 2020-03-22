---
title: Microsoft Intune - Azure'da özel cihaz ayarlarını kullanma | Microsoft Docs
description: Microsoft Intune kullanan Windows Phone, Windows 8.1, Windows 10 ve üzeri, Android Cihaz Yöneticisi, Android Enterprise, macOS ve iOS/ıpados cihazları için özel ayarları kullanmak üzere bir profil ekleyin veya oluşturun.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083994"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Intune'da özel ayarlarla profil oluşturma

Microsoft Intune, bir cihazdaki farklı özellikleri denetlemek için pek çok yerleşik ayar içerir. Ayrıca, yerleşik profillere benzer şekilde oluşturulan özel profiller de oluşturabilirsiniz. Özel profiller, Intune’da yerleşik olarak bulunmayan cihaz ayarları ve özelliklerini kullanabilmenizi sağlar. Bu profiller, kuruluşunuzdaki cihazlarda denetleyebileceğiniz bazı özellik ve ayarlar içerir. Örneğin, her iOS/ıpados cihazı için aynı özelliği ayarlayan özel bir profil oluşturabilirsiniz.

Özel ayarlar her platform için ayrı yapılandırılır. Örneğin Android ve Windows cihazlarındaki özellikleri denetlemek için, Open Mobile Alliance Tekdüzen Kaynak Tanımlayıcısı (OMA-URI) değerleri girebilirsiniz. Apple cihazlar için [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) veya [Apple Profile Manager](https://support.apple.com/profile-manager) ile oluşturduğunuz bir dosyayı içeri aktarabilirsiniz.

Yapılandırma profilleri hakkında daha fazla bilgi için bkz. [Microsoft Intune cihaz profili nedir?](device-profiles.md).

Bu makalede, Android Cihaz Yöneticisi, Android Enterprise, iOS/ıpados, macOS ve Windows için nasıl özel bir profil oluşturacağınız gösterilmektedir. Farklı platformlar için kullanılabilir tüm ayarları da görebilirsiniz.

## <a name="create-the-profile"></a>Profili oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Profil oluşturma** > **yapılandırma profilleri** > **cihazları** seçin.
3. Aşağıdaki özellikleri girin:

    - **Ad**: ilke için açıklayıcı bir ad girin. İlkelerinizi daha sonra kolayca tanıyacak şekilde adlandırın. Örneğin, iyi bir ilke adı **Windows 10: Allowvpnoverhücresel özel OMA-URI ' y i sağlayan özel profildir**.
    - **Açıklama**: Profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    - **Platform**: cihazlarınızın platformunu seçin. Seçenekleriniz şunlardır:

      - **Android Cihaz Yöneticisi**
      - **Android Kurumsal**
      - **iOS/ıpados**
      - **macOS**
      - **Windows 10 ve üzeri**
      - **Windows 8.1 ve üzeri**

    - **Profil türü**: **özel**' i seçin.

4. Ayarlar her platform için farklıdır. Belirli bir platformun ayarlarını görmek için platformunuzu seçin:

    - [Android Cihaz Yöneticisi](custom-settings-android.md)
    - [Android Kurumsal](custom-settings-android-for-work.md)
    - [iOS/ıpados](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. İşiniz bittiğinde, **oluştur** > **Profil oluştur** ' u seçin.

Profil oluşturulur ve profiller listesinde gösterilir (**cihaz yapılandırma** > **profilleri**).

## <a name="next-steps"></a>Sonraki adımlar

Profil oluşturulduktan sonra atanmak için hazırlanın. Ardından [profili atayın](device-profile-assign.md) ve [durumunu izleyin](device-profile-monitor.md).
