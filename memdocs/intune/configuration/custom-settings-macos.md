---
title: Microsoft Intune - Azure’da macOS cihazlara özel ayarlar ekleme | Microsoft Docs
titleSuffix: ''
description: Apple Configurator veya Apple Profile Manager araçlarından macOS ayarlarını dışarı aktarın ve daha sonra bu ayarları Microsoft Intune’a aktarın. Bu ayarlar, macOS cihazlarında özel ayarları ve özellikleri oluşturabilir, kullanabilir ve denetleyebilir. Daha sonra bu özel profil, bir ana hat veya standart oluşturmak için kuruluşunuzdaki macOS cihazlara atanabilir veya dağıtılabilir.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 689c87f6362c4d369ad7e968aebb139ef2560b99
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814928"
---
# <a name="use-custom-settings-for-macos-devices-in-microsoft-intune"></a>Microsoft Intune’da macOS cihazlar için özel ayarlar kullanma

Microsoft Intune’u kullanarak, bir “özel profil” kullanan macOS cihazlarınız için özel ayarlar ekleyebilir veya oluşturabilirsiniz. Özel profiller, bir Intune özelliğidir. Intune’da yerleşik olarak bulunmayan cihaz ayarları ve özelliklerini eklemek için tasarlanmıştır.

macOS cihazlarda Intune’a özel ayarlar eklemenin iki yolu vardır:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple Profile Manager](https://support.apple.com/profile-manager)

Bir yapılandırma profiline ayar aktarmak için bu araçları kullanabilirsiniz. Intune’da bu dosyayı içeri aktarır ve sonra profili, macOS kullanıcılarınıza ve cihazlarınıza atarsınız. Atandıktan sonra ayarlar dağıtılır. Ayrıca, kuruluşunuzda macOS için bir taban çizgisi veya standart oluşturur.

Bu makalede, Apple Configurator ve Apple Profile Manager kullanımı hakkında bazı yönergeler sağlanır ve yapılandırabileceğiniz özellikler açıklanmaktadır.

## <a name="before-you-begin"></a>Başlamadan önce

[MacOS özel cihaz yapılandırma profili](custom-settings-configure.md)oluşturun.

## <a name="what-you-need-to-know"></a>Bilmeniz gerekenler

- Yapılandırma profilini oluşturmak için **Apple Configurator** kullanırken, dışarı aktarma yaptığınız ayarların cihazlardaki MacOS sürümüyle uyumlu olduğundan emin olun. Uyumsuz ayarların çözümlenmesi hakkında bilgi için [Apple Developer](https://developer.apple.com/) web sitesinde **Configuration Profile Reference** ve **Mobile Device Management Protocol Reference** başlıklarını arayın.

- **Apple Profile Manager**’ı kullanırken şunları yapmayı unutmayın:

  - Profile Manager’da [mobil cihaz yönetimini](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) etkinleştirin.
  - Profile Manager’a [macOS cihazlar](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) ekleyin.
  - Profil Yöneticisi 'ne bir cihaz ekledikten sonra, **kitaplık**  >  **cihazları** ' na gidin > cihaz > **ayarlarınızı**seçin. Cihaz için genel ayarlar ile güvenlik, gizlilik, dizin ve sertifika ayarlarını girin.

    Bu dosyayı indirin ve kaydedin. Intune profilinde bu dosyayı girmeniz istenir. 

  - Apple Profile Manager 'dan dışarı verdiğiniz ayarların cihazlardaki macOS sürümüyle uyumlu olduğundan emin olun. Uyumsuz ayarların çözümlenmesi hakkında bilgi için [Apple Developer](https://developer.apple.com/) web sitesinde **Configuration Profile Reference** ve **Mobile Device Management Protocol Reference** başlıklarını arayın.

## <a name="custom-configuration-profile-settings"></a>Özel yapılandırma profili ayarları

- **Yapılandırma profili adı**: ilke için bir ad girin. Bu ad, cihazda ve Intune durumunda gösterilir.
- **Yapılandırma profili dosyası**: `.xml` `.mobileconfig` Apple Configurator veya Apple Profile Manager 'ı kullanarak oluşturduğunuz veya dosyaya gidin. En büyük dosya boyutu 1000000 bayttır (yalnızca 1 MB 'nin altında). İçeri aktardığınız dosya gösterilir. Ayrıca, bir dosyayı eklendikten sonra da **kaldırabilirsiniz** .

  Ayrıca, dosyalarınıza cihaz belirteçleri ekleyebilirsiniz `.mobileconfig` . Cihaz belirteçleri cihaza özgü bilgileri eklemek için kullanılır. Örneğin, seri numarasını göstermek için girin `{{serialnumber}}` . Cihazda, metin, `123456789ABC` her bir cihaz için benzersiz olan öğesine benzer şekilde görünür. Değişken girerken, küme ayraçları kullandığınızdan emin olun `{{ }}` . [Uygulama yapılandırma belirteçleri](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) , kullanılabilecek değişkenlerin bir listesini içerir. Ayrıca, `deviceid` herhangi bir cihaza özgü değeri de kullanabilirsiniz.

  > [!NOTE]
  > Değişkenler kullanıcı arabiriminde doğrulanmaz ve büyük/küçük harfe duyarlıdır. Sonuç olarak, yanlış girişle kaydedilmiş profiller görebilirsiniz. Örneğin, `{{DeviceID}}` yerine girdiğinizde `{{deviceid}}` , CIHAZıN benzersiz kimliği yerine değişmez dize gösterilir. Doğru bilgileri girdiğinizden emin olun.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[İOS/ıpados cihazlarında özel bir profil](custom-settings-ios.md)oluşturun.
