---
title: Şirket içi MDM için uygulamaları yönetme
titleSuffix: Configuration Manager
description: Configuration Manager ' de şirket içi mobil cihaz yönetimi (MDM) için uygulamaları yönetin.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 693f661f2a2db59335ec8e463842a0ad03c977f3
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721916"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager ' de şirket içi MDM için uygulamaları yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Şirket içi mobil cihaz yönetimi (MDM) ile cihazları yönetirken, aşağıdaki uygulama türlerini yönetebilirsiniz:

- Windows Phone uygulama paketi (*.xap dosyası)
- Windows Phone uygulama paketi (Windows Phone Mağazası'nda)
- MDM aracılığıyla Windows Installer
- Web Uygulaması

Configuration Manager uygulamaları ve dağıtım türlerini yönetme hakkında daha fazla genel bilgi için bkz. [Configuration Manager uygulamalar Için yönetim görevleri](../../apps/deploy-use/management-tasks-applications.md).

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Windows Phone uygulaması oluşturma

Bir Configuration Manager uygulamasının bir veya daha fazla dağıtım türü vardır. Dağıtım türü bir cihaza yazılım dağıtmak için gereken yükleme dosyalarını ve bilgilerini içerir. Dağıtım türü ayrıca yazılımın ne zaman ve nasıl dağıtıldığını belirten kurallara sahiptir.

Uygulama ve dağıtım türleri oluşturmak için genel adımlar için bkz. [uygulama oluşturma](../../apps/deploy-use/create-applications.md#bkmk_create).

Configuration Manager, Windows Mobile cihazları Için aşağıdaki uygulama dosya türlerini destekler:

|Cihaz Türü|Desteklenen dosya türleri|
|-----------------|---------------------|
|Windows Phone 8|XAP|
|Windows Phone 8.1|XAP, appx, appxdemeti|
|Windows 10 Mobile|XAP, appx, appxdemeti|

Windows Phone uygulamaları **kullanılabilir** veya **gerekli**olarak dağıtın. Ayrıca, uygulamaları kaldırmak için dağıtımları kullanın.

## <a name="deploy-and-monitor-apps"></a>Uygulamaları dağıtma ve izleme

Masaüstü bilgisayarlar ve sunucular gibi diğer cihazlarda yaptığınız gibi Configuration Manager mobil cihazlara yönelik uygulamaları dağıtın ve izleyin. Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md)
- [Uygulamaları izleme](../../apps/deploy-use/monitor-applications-from-the-console.md)

Mobil cihazlara özgü aşağıdaki sınırlamaları gözden geçirin:

- MDM 'ye kayıtlı cihazlar sanal dağıtımları, Kullanıcı deneyimini veya zamanlama ayarlarını desteklemez.

- Tek bir uygulamaya 100 taneden fazla yerel ayar eklemeyin. Bu eylem, uygulamanın cihaza yüklenmesini engeller.

## <a name="next-step"></a>Sonraki adım

Dağıtılan bir uygulamayı yeni bir uygulamayla değiştirmek, kaldırmak veya değiştirmek için, Configuration Manager ' deki herhangi bir uygulamayla aynı şekilde yönetin. Daha fazla bilgi için bkz. [uygulamaları güncelleştirme ve devre dışı bırakma](../../apps/deploy-use/update-and-retire-applications.md).
