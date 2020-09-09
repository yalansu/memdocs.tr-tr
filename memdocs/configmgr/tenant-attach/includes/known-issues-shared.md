---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: 8d456185e39df8d76b949baf26de755970a9a89b
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564000"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-multi-factor-authentication-is-enabled-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Multi-Factor Authentication etkin olduğunda, çoğu kiracı iliştirme özelliği çalışmaz
<!--7986450, 7988266-->
**Senaryo:** [Hizmet bağlantı noktasıyla](../../core/servers/deploy/configure/about-the-service-connection-point.md) Iletişim kuran [SMS sağlayıcı](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) makinesi Multi-Factor Authentication kullanmak üzere yapılandırıldıysa, uygulamaları yükleye, CMPivot sorguları çalıştıra, ve Yönetici konsolundan başka işlemler gerçekleştirebileceksiniz. 403 hata kodunu alacaksınız, yasak.  

**Geçici çözüm:** Geçerli geçici çözüm, hiyerarşiyi **Windows kimlik**doğrulamasının varsayılan kimlik doğrulama düzeyine yapılandırmaktır. Daha fazla bilgi için [SMS sağlayıcısı makalesindeki kimlik doğrulama bölümüne](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)bakın.

