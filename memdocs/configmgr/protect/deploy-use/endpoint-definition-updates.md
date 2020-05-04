---
title: Tanım güncelleştirmelerini yapılandırma
titleSuffix: Configuration Manager
description: Kötü amaçlı yazılımdan koruma tanımlarını istemci bilgisayarlarda güncel tutmak için Configuration Manager Endpoint Protection ile yöntemleri seçme ve yapılandırma hakkında bilgi edinin.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce11ba0cbe4298d32a11de409910ebc3e14c097b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715770"
---
# <a name="configure-definition-updates-for-endpoint-protection"></a>Endpoint Protection için tanım güncelleştirmelerini yapılandırma  

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Configuration Manager Endpoint Protection ile, hiyerarşinizdeki istemci bilgisayarlarda kötü amaçlı yazılımdan koruma tanımlarını güncel tutmak için birkaç kullanılabilir yöntemden herhangi birini kullanabilirsiniz. Bu konudaki bilgiler, bu yöntemleri seçip yapılandırmanıza yardımcı olabilir.

 Kötü amaçlı yazılım tanımlarını güncelleştirmek için aşağıdaki yöntemlerden bir veya daha fazlasını kullanabilirsiniz:

- [Configuration Manager dağıtılan güncelleştirmeler](endpoint-definitions-configmgr.md) -bu yöntem, hiyerarşinizdeki bilgisayarlara tanım ve altyapı güncelleştirmeleri sunmak için Configuration Manager yazılım güncelleştirmelerini kullanır.

- [Windows Server Update Services (WSUS) üzerinden dağıtılan güncelleştirmeler](endpoint-definitions-wsus.md) -bu yöntem, bilgisayarlara tanım ve altyapı güncelleştirmelerini ILETMEK için WSUS altyapınızı kullanır.

- [Microsoft Update dağıtılan güncelleştirmeler](endpoint-definitions-microsoft-updates.md) -bu yöntem, bilgisayarların tanım ve altyapı güncelleştirmelerini indirmek için doğrudan Microsoft Update bağlanmasına izin verir. Bu yöntem iş ağına sık bağlanmayan bilgisayarlar için yararlı olabilir.

- [Microsoft kötü amaçlı yazılımdan koruma merkezi 'nden dağıtılan güncelleştirmeler](endpoint-definitions-protection-center.md) -bu yöntem, Microsoft kötü amaçlı yazılımdan koruma merkezi 'nden tanım güncelleştirmelerini indirecek.

- [UNC dosya paylaşımlarından güncelleştirmeler](endpoint-definitions-network.md) -bu yöntemle, en son tanım ve altyapı güncelleştirmelerini ağdaki bir paylaşıma kaydedebilirsiniz. İstemciler daha sonra güncelleştirmeleri yüklemek üzere ağa erişebilir.

  Birden çok tanım güncelleştirme kaynağını yapılandırabilir ve bunların değerlendirilip uygulandığı sırayı denetleyebilirsiniz. Bu işlem bir kötü amaçlı yazılımdan koruma ilkesi oluşturulurken **Tanım Güncelleştirme Kaynaklarını Yapılandır** iletişim kutusundan yapılabilir.

> [!IMPORTANT]
>  Windows 10 bilgisayarları için, Windows Defender için kötü amaçlı yazılım tanımlarını güncelleştirmek üzere Endpoint Protection yapılandırmanız gerekir.

## <a name="how-to-configure-definition-update-sources"></a>Tanım Güncelleştirme Kaynaklarını Yapılandırma
 Her bir kötü amaçlı yazılımdan koruma ilkesi için kullanılacak tanım güncelleştirme kaynaklarını yapılandırmak üzere aşağıdaki yordamı kullanın.

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.

2.  **Varlıklar ve Uyum** çalışma alanında **Endpoint Protection**’ı genişletin ve **Kötü Amaçlı Yazılımdan Koruma İlkeleri**’ne tıklayın.

3.  **Varsayılan Kötü Amaçlı Yazılımdan Koruma İlkesi** ’nin özellikler sayfasını açın veya yeni bir kötü amaçlı yazılımdan koruma ilkesi oluşturun. Kötü amaçlı yazılımdan koruma ilkeleri oluşturma hakkında daha fazla bilgi için bkz. [Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](endpoint-antimalware-policies.md).

4.  Kötü amaçlı yazılımdan koruma özellikleri iletişim kutusunun **Güvenlik Zekası güncelleştirmeleri** bölümünde **kaynağı ayarla**' ya tıklayın.
    - **Tanım güncelleştirmeleri** bölümü, Configuration Manager sürüm 1902 ' den başlayarak **Güvenlik Zekası güncelleştirmeleriyle** yeniden adlandırıldı.

5.  **Tanım Güncelleştirme Kaynaklarını Yapılandır** iletişim kutusunda tanım güncelleştirmeleri için kullanılacak kaynakları seçin. Bu kaynakların kullanıldığı sırayı değiştirmek için **Yukarı** veya **Aşağı** öğesine tıklayabilirsiniz.

6.  **Tamam** ’a tıklayarak **Tanım Güncelleştirme Kaynaklarını Yapılandır** iletişim kutusunu kapatın.

## <a name="configure-endpoint-protection-definitions"></a>Endpoint Protection tanımlarını Yapılandır

-   [Configuration Manager dağıtılan güncelleştirmeler](endpoint-definitions-configmgr.md) -bu yöntem, hiyerarşinizdeki bilgisayarlara tanım ve altyapı güncelleştirmeleri sunmak için Configuration Manager yazılım güncelleştirmelerini kullanır.

-   [Windows Server Update Services (WSUS) üzerinden dağıtılan güncelleştirmeler](endpoint-definitions-wsus.md) -bu yöntem, bilgisayarlara tanım ve altyapı güncelleştirmelerini ILETMEK için WSUS altyapınızı kullanır.

-   [Microsoft Update dağıtılan güncelleştirmeler](endpoint-definitions-microsoft-updates.md) -bu yöntem, bilgisayarların tanım ve altyapı güncelleştirmelerini indirmek için doğrudan Microsoft Update bağlanmasına izin verir. Bu yöntem iş ağına sık bağlanmayan bilgisayarlar için yararlı olabilir.

-   Microsoft kötü amaçlı yazılımdan koruma merkezi 'nden dağıtılan güncelleştirmeler-bu yöntem, Microsoft kötü amaçlı yazılımdan koruma merkezi 'nden tanım güncelleştirmelerini indirecek.

-   [UNC dosya paylaşımlarından güncelleştirmeler](endpoint-definitions-network.md) -bu yöntemle, en son tanım ve altyapı güncelleştirmelerini ağdaki bir paylaşıma kaydedebilirsiniz. İstemciler daha sonra güncelleştirmeleri yüklemek üzere ağa erişebilir.
