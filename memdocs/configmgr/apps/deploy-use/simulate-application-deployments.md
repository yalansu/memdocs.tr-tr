---
title: Uygulama dağıtımlarının simülasyonunu yapma
titleSuffix: Configuration Manager
description: Uygulamayı yüklemeden bir dağıtım türü için algılama yöntemini, gereksinimleri ve bağımlılıkları değerlendirin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710597"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Configuration Manager ile uygulama dağıtımlarının benzetimini yapma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Uygulamayı yüklemeden veya kaldırmadan bir uygulama dağıtımını test etmek için sanal dağıtımları kullanabilirsiniz. Sanal dağıtım, bir dağıtım türü için algılama yöntemini, gereksinimleri ve bağımlılıkları değerlendirir. Sonuçları **izleme** çalışma alanının **dağıtımlar** düğümünde raporlar. Configuration Manager ' de bir uygulama dağıtımının benzetimini yapmak için bu konudaki yordamı kullanın.  

> [!NOTE]  
> Mobil cihaz koleksiyonları için sanal dağıtımları kullanamazsınız.  
>   
> Dağıtım amacı **Kaldır** olan bir uygulamayı, aynı uygulamanın sanal dağıtımı aktifse dağıtamazsınız.  

## <a name="configure-a-simulated-application-deployment"></a>Sanal uygulama dağıtımını yapılandırma

1.  Configuration Manager konsolunda, aşağıdakilerden birini seçin:  
    -   Bir kullanıcı koleksiyonu.  
    -   Bir cihaz koleksiyonu.  
    -   Bir Configuration Manager uygulaması.  

2.  **Giriş** sekmesinde, **dağıtım** grubunda, **dağıtımı Benzet**' i seçin.  

3.  Uygulama dağıtımını benzetim Sihirbazı 'nda, sanal dağıtımınız için aşağıdaki ayrıntıları ayarlayın:  

    -   **Uygulama**. **Araştır**' ı seçin ve ardından sanal dağıtımı oluşturmak istediğiniz uygulamayı seçin.  

    -   **Koleksiyon**. **Araştır**' ı seçin ve ardından sanal dağıtım için kullanmak istediğiniz koleksiyonu seçin.  

    -   **Eylem**. Aşağı açılan listeden, Seçili uygulamanın yüklemesinin veya kaldırılmasının benzetimini yapmak isteyip istemediğinizi seçin.  

    -   **Kullanıcı oturumu açma ile veya olmadan otomatik olarak dağıtın**. Bu seçenek işaretliyse istemciler, istemcilerin oturum açıp açmamadığı, sanal dağıtımı değerlendirir.  

4.  **İleri**' ye tıklayın, **Özet** sayfasındaki bilgileri gözden geçirin ve ardından sanal uygulama dağıtımını oluşturmak için Sihirbazı sona erdirin.  

5.  Sanal uygulamalar, **izleme** çalışma alanının **dağıtımlar** düğümünde, **Benzetim**amacıyla görünür. Uygulama dağıtımlarını izleme hakkında daha fazla bilgi için bkz. [Configuration Manager konsolundan uygulamaları izleme](../../apps/deploy-use/monitor-applications-from-the-console.md).  
