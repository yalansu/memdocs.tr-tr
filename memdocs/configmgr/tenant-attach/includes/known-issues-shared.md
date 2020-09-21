---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: e6023808f60d0ac7753745d5882516dda0f85be2
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90802937"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-the-configuration-manager-site-is-configured-to-require-multi-factor-authentication-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Configuration Manager sitesi çok faktörlü kimlik doğrulaması gerektirecek şekilde yapılandırıldığında, çoğu kiracı iliştirme özelliği çalışmaz
<!--7986450, 7988266-->
**Senaryo:** [Hizmet bağlantı noktasıyla](../../core/servers/deploy/configure/about-the-service-connection-point.md) Iletişim kuran [SMS sağlayıcı](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) makinesi Multi-Factor Authentication kullanmak üzere yapılandırıldıysa, uygulamaları yükleye, CMPivot sorguları çalıştıra, ve Yönetici konsolundan başka işlemler gerçekleştirebileceksiniz. 403 hata kodunu alacaksınız, yasak.  

**Geçici çözüm:** Geçerli geçici çözüm, şirket içi hiyerarşiyi **Windows kimlik**doğrulamasının varsayılan kimlik doğrulama düzeyine yapılandırmaktır. Daha fazla bilgi için [SMS sağlayıcısı makalesindeki kimlik doğrulama bölümüne](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)bakın.

