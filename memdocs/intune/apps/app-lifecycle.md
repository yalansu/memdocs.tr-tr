---
title: Microsoft Intune için uygulama yaşam döngüsüne genel bakış
description: Microsoft Intune'da yönetilen uygulamaların yaşam döngüsü hakkında bilgi edinin. Uygulama yaşam döngüsü uygulamaların dağıtımı, yapılandırması, korunması ve kullanım dışı bırakılmasını içerir.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60347012-bc3f-4b9a-a4f4-6d3c5021a6e6
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: apps; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8605b33d8fb83fb4537182127860f0cbb098e620
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428606"
---
# <a name="overview-of-the-app-lifecycle-in-microsoft-intune"></a>Microsoft Intune'da uygulama yaşam döngüsüne genel bakış

Microsoft Intune uygulama yaşam döngüsü, bir uygulama eklendiğinde başlar, ek aşamalardan geçerek siz uygulamayı kaldırana kadar devam eder. Bu aşamaları inceleyerek, Intune 'da uygulama yönetimi ile çalışmaya başlamak için ihtiyacınız olan ayrıntılara sahip olacaksınız.

![Uygulama yaşam döngüsü-ekleme, dağıtma, yapılandırma, koruma ve devre dışı bırakma.](./media/app-lifecycle/app-lifecycle.png "Intune uygulama yaşam döngüsü")

## <a name="add"></a>Ekle

Uygulama dağıtımında ilk adım, yönetmek ve atamak istediğiniz uygulamayı Intune’a eklemektir. Birçok farklı uygulama türüyle çalışabilecek olmanıza karşın, temel yordamlar aynıdır. Intune ile, şirket içinde yazılmış uygulamalar (iş kolu), mağazadan uygulamalar, yerleşik uygulamalar ve Web üzerinde uygulamalar dahil farklı uygulama türleri ekleyebilirsiniz. Bu uygulama türlerinden her biri hakkında daha fazla bilgi için bkz. [Microsoft Intune’a uygulama ekleme](apps-add.md).

## <a name="deploy"></a>Dağıtma

Uygulamayı Intune’a ekledikten sonra, [yönettiğiniz kullanıcılara ve cihazlara atayabilirsiniz](apps-deploy.md). Intune bu işlemi kolaylaştırır ve uygulama dağıtıldıktan sonra, Azure portal içinde Intune 'dan dağıtım [başarısını izleyebilirsiniz](apps-monitor.md) . Buna ek olarak, [Apple](vpp-apps-ios.md) ve [Windows](windows-store-for-business.md) uygulama mağazaları gibi bazı uygulama mağazalarında şirketinize toplu uygulama lisansları satın alabilirsiniz. Bu tür uygulamalarda doğrudan Intune yönetim konsolundan lisans dağıtımı yapabilmeniz ve lisans kullanımını izleyebilmeniz için Intune verileri bu mağazalarla eşitleyebilir.

## <a name="configure"></a>Yapılandırma

Uygulama yaşam döngüsü kapsamında, uygulamaların yeni sürümleri düzenli olarak kullanıma sunulur. Intune, dağıtmış olduğunuz uygulamaları kolayca yeni sürüme [güncelleştirmeniz](apps-add.md) için araçlar sağlar. Buna ek olarak, bazı uygulamalar için fazladan işlevsellik yapılandırabilirsiniz; örneğin:

- [iOS/ıpados uygulama yapılandırma ilkeleri](app-configuration-policies-use-ios.md) , uygulama çalıştırıldığında kullanılan uyumlu IOS/ıpados uygulamalarına yönelik ayarları sağlar. Örneğin, uygulama için belirli marka ayarları veya bağlanması gereken sunucunun adı gerekiyor olabilir.
- [Yönetilen tarayıcı ilkeleri](app-configuration-managed-browser.md) , varsayılan cihaz tarayıcısının yerini alan ve kullanıcılarınızın ziyaret edebileceği web sitelerini kısıtlamanızı sağlayan [Microsoft Edge](apps-supported-intune-apps.md#microsoft-apps)ayarlarını yapılandırmanıza yardımcı olur.

## <a name="protect"></a>Koruma

Intune, uygulamalarınızdaki verileri korumaya yardımcı olmanın yollarını sağlar. Ana yöntemler şunlardır:

- Belirttiğiniz koşullara bağlı olarak e-posta ve diğer hizmetlere erişimi denetleyen [koşullu erişim](../protect/conditional-access.md). Bu koşullara cihaz türleri veya dağıttığınız bir [cihaz uyumluluk ilkesi](../protect/device-compliance-get-started.md) ile uyumluluk dahildir.
- [Uygulama koruma ilkeleri](app-protection-policy.md), tek tek uygulamalarla çalışarak bunların kullandığı şirket verilerinin korunmasına yardımcı olur. Örneğin, yönetilmeyen uygulamalarla sizin yönettiğiniz uygulamalar arasında veri kopyalamayı kısıtlayabilir ya da uygulamaların yazılım kilidi kırılmış veya kök erişimine izin verilmiş cihazlarda çalıştırılmasını önleyebilirsiniz.

## <a name="retire"></a>Devre Dışı Bırakma

Sonunda, büyük olasılıkla dağıttığınız uygulamalar eskir ve kaldırılmaları gerekir. Intune, uygulamaları kaldırmayı kolaylaştırır. Daha fazla bilgi için bkz. [uygulamayı kaldırma](../apps/apps-add.md#uninstall-an-app).

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune'da uygulama yönetimini](app-management.md) öğrenin
