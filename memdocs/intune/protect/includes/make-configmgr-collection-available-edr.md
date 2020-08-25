---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823445"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Üst düzey sitenize bağlı bir Configuration Manager konsolundan, Microsoft Endpoint Manager Yönetim Merkezi 'ne eşitlediğiniz bir cihaz koleksiyonuna sağ tıklayıp **Özellikler**' i seçin.

2. **Bulut eşitleme** sekmesinde, **Bu koleksiyonun Microsoft Endpoint Manager Yönetim Merkezi ' nden Endpoint Security ilkeleri atamasını sağlama**seçeneğini etkinleştirin.

   - Configuration Manager hiyerarşiniz kiracı ekli değilse bu seçeneği seçemezsiniz.
   - Bu seçenek için kullanılabilir koleksiyonlar, [kiracı iliştirme yüklemesi için seçilen koleksiyon kapsamıyla](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit)sınırlıdır. <!--CM7423168-->
  
   ![Bulut eşitlemesini yapılandırma](../media/tenant-attach-intune/cloud-sync.png)

3. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.

   Bu koleksiyondaki cihazlar artık Microsoft Defender ATP ile birlikte bulunabilir ve Intune Endpoint Security ilkelerinin kullanımını destekler.
