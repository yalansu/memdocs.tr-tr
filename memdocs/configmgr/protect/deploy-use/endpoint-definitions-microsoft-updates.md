---
title: Tanımları Microsoft 'tan indirin
titleSuffix: Configuration Manager
description: Configuration Manager için Microsoft Updates Endpoint Protection kötü amaçlı yazılım tanımlarının indirilmesini nasıl etkinleştirebileceğinizi öğrenin.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715693"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Microsoft Updates 'den indirmek için Endpoint Protection kötü amaçlı yazılım tanımlarını etkinleştirin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Microsoft Update tanım güncelleştirmelerini indirmeyi seçtiğinizde, istemciler kötü amaçlı yazılımdan koruma ilkesi iletişim kutusunun **Güvenlik Zekası güncelleştirmeleri** bölümünde tanımlanan aralıkta Microsoft Update sitesini kontrol eder.

 Bu yöntem, istemcinin Configuration Manager sitesiyle bağlantısı olmadığında veya kullanıcıların tanım güncelleştirmelerini başlatabilmesini istediğinizde yararlı olabilir.

> [!IMPORTANT]
> - İstemcilerin tanım güncelleştirmelerini indirirken bu yöntemi kullanabilmesi için Microsoft Update sitesine İnternet üzerinden erişimi olmalıdır.
> - **Tanım güncelleştirmeleri** bölümü, Configuration Manager sürüm 1902 ' den başlayarak **Güvenlik Zekası güncelleştirmeleriyle** yeniden adlandırıldı.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Microsoft Kötü Amaçlı Yazılımdan Koruma Merkezi’ni Kullanarak Tanımları İndirme
 İstemcileri, Microsoft Kötü Amaçlı Yazılımdan Koruma Merkezi’nden tanım güncelleştirmelerini indirecek şekilde yapılandırabilirsiniz. Bu seçenek, Endpoint Protection istemcileri tarafından, güncelleştirmeleri başka bir kaynaktan indirebiliyorlarsa, tanım güncelleştirmelerini indirmek için kullanılır. Bu güncelleştirme yöntemi, Configuration Manager altyapınızla güncelleştirmelerin teslimini engelleyen bir sorun varsa yararlı olabilir.

> [!IMPORTANT]
>  İstemcilerin tanım güncelleştirmelerini indirirken bu yöntemi kullanabilmesi için Microsoft Update sitesine İnternet üzerinden erişimi olmalıdır.
> 
> 
> [!div class="button"]
> [Sonraki adım >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Geri >](endpoint-configure-alerts.md)
