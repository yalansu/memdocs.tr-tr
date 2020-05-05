---
title: Şirket içi MDM
titleSuffix: Configuration Manager
description: Configuration Manager 'da şirket içi mobil cihaz yönetimi (MDM) hakkında bilgi edinin
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721839"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>Configuration Manager Şirket içi MDM

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Şirket içi mobil cihaz yönetimi (MDM), Windows 'un yerleşik yönetim özelliklerine dayanan bir cihaz yönetimi çözümüdür. Bu özellik, Open Mobile Alliance (OMA) cihaz yönetimi (DM) standardını temel alır. Cihazları yönetmek ve sürdürmek için kuruluşunuzun Configuration Manager altyapısını kullanır. Kuruluşunuz bu özelliği kullanmak için Microsoft Intune lisans gerektirir, ancak herhangi bir bulut bağlantısı gerektirmez. Configuration Manager, şirket içi site veritabanınızdaki cihazlarınızla ilgili tüm verileri depolar.

Şirket içi MDM, yerleşik OMA DM özelliklerine de dayanan Microsoft Intune farklıdır. Intune 'daki tüm yönetim işlevleri, bulut hizmetleri aracılığıyla dağıtılır. Şirket içi MDM Ayrıca, Configuration Manager tarafından sağlanan istemci tabanlı yönetim çözümünden da farklıdır. Benzer altyapıyı kullanır, ancak yönettiği cihazlarda ayrı olarak yüklü istemci yazılımlarını kullanmaz.  

## <a name="comparison"></a>Karşılaştırma

Aşağıdaki bölümlerde, geleneksel istemci tabanlı yönetime kıyasla şirket içi MDM 'nin avantajları ve dezavantajları listelenmektedir:  

### <a name="advantages"></a>Yararları

- **Basitleştirilmiş altyapı**: daha az site sistemi rolü gereklidir.

- **Bakım daha kolay**: yönetim işlevleri cihaz işletim sisteminde yerleşik olduğundan, siteye yeni yönetim özellikleri sunulduğundan Configuration Manager istemcisinin yeni sürümleri gerekli değildir.

- Şirket **içi**:-tüm yönetim ve veriler şirket içinde tutulur.

### <a name="disadvantages"></a>Dezavantajlar

**Daha az istemci yönetimi işlevselliği**: düzenleme, yazılım kullanım ölçümü, üçüncü taraf tümleştirme, görev sıralama veya yazılım merkezi desteği yoktur.

- **Sınırlı cihaz desteği**: ŞIRKET içi MDM, Configuration Manager istemcisi olarak pek çok işletim sistemi sürümünü desteklemez. Daha fazla bilgi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemi sürümleri](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="next-step"></a>Sonraki adım

Configuration Manager altyapısını ayarlarken ve şirket içi MDM 'de cihaz kaydı için planlama yaparken göz önünde bulundurmanız gerekenler hakkında bilgi edinin.

> [!div class="nextstepaction"]
> [Şirket içi MDM’i planlama](../plan-design/plan-on-premises-mdm.md)  
