---
title: Donanım envanterini yapılandırma
titleSuffix: Configuration Manager
description: Tüm istemciler veya Configuration Manager bir koleksiyon için donanım envanterini ayarlayın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714440"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>Configuration Manager 'da donanım envanterini yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu yordam, donanım envanteri için varsayılan istemci ayarlarını yapılandırır ve hiyerarşinizdeki tüm istemcilere uygulanır. Bu ayarların yalnızca bazı istemcilere uygulanmasını istiyorsanız bir özel cihaz istemci ayarı oluşturun ve bu ayarı, donanım envanterini kullanmak istediğiniz cihazları içeren bir koleksiyona atayın. Bkz. [istemci ayarlarını yapılandırma](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Bir istemci, birden fazla istemci ayarı kümesinden donanım envanteri ayarları alırsa, bu durumda istemci donanım envanterini bildirdiğinde her ayar kümesinden gelen donanım envanteri sınıfları birleştirilir. Buna ek olarak, bir özel istemci ayarında daha yüksek önceliğe sahip bir sınıfın denetlenmesi, istemcinin o sınıfı almasını önlemesinin devre dışı bırakmasına sahip değildir. 

Birkaç sistem dışındaki sistemlerin çoğunda belirli bir donanım envanteri sınıfını devre dışı bırakmak için, sınıfın varsayılan istemci ayarlarında işareti kaldırılmış olması gerekir. Ardından, sınıfı etkinleştirmek ve hedef sistemlere dağıtmak için özel bir istemci ayarı oluşturun.


### <a name="to-configure-hardware-inventory"></a>Donanım envanterini yapılandırmak için  

1.  Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan istemci ayarları**' nı seçin.  

4.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

5.  **Varsayılan ayarlar** iletişim kutusunda, **donanım envanteri**' ni seçin.  

6.  **Cihaz Ayarları** listesinde aşağıdakileri yapılandırın:  

    -   **İstemcilerde donanım envanterini etkinleştir** - **Evet**' i seçin.  

    -   **Donanım envanteri zamanlaması** -istemcilerin donanım envanterini toplayacağı aralığı belirtmek için **zamanlama** ' ya tıklayın.  

7.  İhtiyaç duyduğunuz diğer [donanım envanteri istemci ayarlarını](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) yapılandırın.  

İstemci cihazlar, daha sonra istemci ilkesini ilk indirmelerinde bu ayarlarla yapılandırılır. Tek bir istemci için ilke almayı başlatmak için bkz. [istemcileri yönetme](../../../../core/clients/manage/manage-clients.md).  
