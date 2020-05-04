---
title: Ortak yönetim iş yüklerini değiştirme
titleSuffix: Configuration Manager
description: Configuration Manager tarafından şu anda yönetilen iş yüklerini Microsoft Intune olarak nasıl değiştireceğinizi öğrenin.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 4874d12149f213351740c9e5b300bf04fc536571
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711367"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Configuration Manager iş yüklerini Intune 'a değiştirme

Ortak yönetimin avantajlarından biri, Configuration Manager iş yüklerini Microsoft Intune olarak değiştirme. Bir Windows 10 cihazının Configuration Manager istemcisi olduğunda ve Intune 'a kaydolduğu zaman, her iki hizmetin de avantajlarına sahip olursunuz. Varsa, yetkiyi Configuration Manager olan iş yüklerini Intune 'a geçirebilirsiniz. Configuration Manager, Intune 'a geçiş gerçekleştirmeyen iş yükleri ve ortak yönetimin desteklemediği diğer tüm Configuration Manager özellikleri de dahil tüm diğer iş yüklerini yönetmeye devam eder.

Bir iş yükünü Intune 'a geçerseniz, ancak daha sonra fikrinizi değiştirirseniz, tekrar Configuration Manager dönebilirsiniz.

Desteklenen iş yükleri hakkında daha fazla bilgi için bkz. [Iş yükleri](workloads.md).

## <a name="switch-workloads-starting-in-version-1906"></a>Sürüm 1906 ' den başlayarak iş yüklerini değiştirme
<!--3555750 FKA 1357954 -->
Sürüm 1906 ' den başlayarak, ortak yönetim iş yüklerinin her biri için farklı pilot koleksiyonları yapılandırabilirsiniz. Farklı pilot koleksiyonları kullanabilmek, iş yüklerini değiştirirken daha ayrıntılı bir yaklaşım almanıza olanak sağlar. Ortak yönetimi etkinleştirdiğinizde veya daha sonra hazırsanız iş yüklerini değiştirebilirsiniz. Ortak yönetimi zaten etkinleştirmediyseniz, önce bunu yapın. Daha fazla bilgi için bkz. [ortak yönetimi etkinleştirme](how-to-enable.md). Ortak yönetimi etkinleştirdikten sonra, ortak yönetim özelliklerindeki ayarları değiştirin.

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **ortak yönetim** düğümünü seçin.  
2. Ortak yönetim nesnesini seçin ve ardından şeritte **Özellikler** ' i seçin.  
3. **Iş yükleri** sekmesine geçin. Varsayılan olarak, tüm iş yükleri **Configuration Manager** ayarına ayarlanır. Bir iş yükünü değiştirmek için, bu iş yükünün kaydırıcı denetimini istenen ayara taşıyın.  

    ![Ortak yönetim özellikleri sayfasında Iş yükleri sekmesinin ekran görüntüsü](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**: Configuration Manager Bu iş yükünü yönetmeye devam eder.  

    - **Pilot Intune**: Bu iş yükünü yalnızca pilot koleksiyondaki cihazlar için değiştirin. **Pilot koleksiyonları** , ortak yönetim özellikleri sayfasının **hazırlama** sekmesinde değiştirebilirsiniz.  

    - **Intune**: ortak yönetime kayıtlı tüm Windows 10 cihazları için bu iş yükünü değiştirin.  

4. **Hazırlama** sekmesine gidin ve gerekirse, iş yüklerinden herhangi birinin **pilot koleksiyonunu** değiştirin.
  
   ![Ortak yönetim özellikleri sayfasında Iş yükleri sekmesinin ekran görüntüsü](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Herhangi bir iş yükünü değiştirmeden önce, Intune 'da ilgili iş yükünü doğru şekilde yapılandırıp dağıttığınızdan emin olun. İş yüklerinin her zaman cihazlarınızın yönetim araçlarından biri tarafından yönetildiğinden emin olun.
> - Configuration Manager sürüm 1806 ' den başlayarak, bir ortak yönetim iş yükünü değiştirdiğinizde ortak yönetilen cihazlar MDM ilkesini Microsoft Intune otomatik olarak eşitler. Bu eşitleme Ayrıca, Configuration Manager konsolundaki istemci bildirimlerinden **bilgisayar Ilkesini indir** eylemini başlattığınızda de gerçekleşir. Daha fazla bilgi için bkz. [istemci bildirimini kullanarak istemci ilkesi almayı başlatma](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Sürüm 1902 ve önceki sürümlerde iş yüklerini değiştirin

Ortak yönetimi etkinleştirdiğinizde veya daha sonra hazırsanız iş yüklerini değiştirebilirsiniz. Ortak yönetimi zaten etkinleştirmediyseniz, önce bunu yapın. Daha fazla bilgi için bkz. [ortak yönetimi etkinleştirme](how-to-enable.md). Ortak yönetimi etkinleştirdikten sonra, ortak yönetim özelliklerindeki ayarları değiştirin.

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **ortak yönetim** düğümünü seçin.  

2. Ortak yönetim nesnesini seçin ve ardından şeritte **Özellikler** ' i seçin.
   - Azure AD 'de oturum açmanız istenir. İstem, ekleme alanınızı güncelleştirmenizi engellemez. Ancak, oturum açana kadar **Özellikler** sayfasını her açışınızda sorulur.

3. **Iş yükleri** sekmesine geçin. Varsayılan olarak, tüm iş yükleri **Configuration Manager** ayarına ayarlanır. Bir iş yükünü değiştirmek için, bu iş yükünün kaydırıcı denetimini istenen ayara taşıyın.  

    ![Ortak yönetim özellikleri sayfasında Iş yükleri sekmesinin ekran görüntüsü](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager Bu iş yükünü yönetmeye devam eder.  

    - **Pilot Intune**: Bu iş yükünü yalnızca pilot koleksiyondaki cihazlar için değiştirin. **Pilot koleksiyonunu** ortak yönetim özellikleri sayfasının **hazırlama** sekmesinde değiştirebilirsiniz.  

    - **Intune**: ortak yönetime kayıtlı tüm Windows 10 cihazları için bu iş yükünü değiştirin.  

4. Ortak yönetim özellikleri sayfasının **hazırlama** sekmesinde, gerekirse iş yüklerinizin **pilot koleksiyonunu** değiştirin.

5. Ortak yönetim özelliklerini kaydetmek ve çıkmak için **Tamam** ' ı tıklatın.

> [!Important]  
> - Herhangi bir iş yükünü değiştirmeden önce, Intune 'da ilgili iş yükünü doğru şekilde yapılandırıp dağıttığınızdan emin olun. İş yüklerinin her zaman cihazlarınızın yönetim araçlarından biri tarafından yönetildiğinden emin olun. 
> - Configuration Manager sürüm 1806 ' den başlayarak, bir ortak yönetim iş yükünü değiştirdiğinizde ortak yönetilen cihazlar MDM ilkesini Microsoft Intune otomatik olarak eşitler. Bu eşitleme Ayrıca, Configuration Manager konsolundaki istemci bildirimlerinden **bilgisayar Ilkesini indir** eylemini başlattığınızda de gerçekleşir. Daha fazla bilgi için bkz. [istemci bildirimini kullanarak istemci ilkesi almayı başlatma](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="next-steps"></a>Sonraki adımlar

[Ortak yönetimi izleme](how-to-monitor.md)
