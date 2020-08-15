---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: 13a5b771f712420939f87073854faab3c38270c9
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252482"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-the-sms-provider-is-remote-from-the-cas-you-may-encounter-an-internal-server-error-from-the-admin-console"></a><a name="bkmk_dblhop"></a> SMS sağlayıcısı CA 'lardan uzak olduğunda, Yönetici konsolundan bir iç sunucu hatasıyla karşılaşabilirsiniz

**Hata iletisi:** Şirket içi hata kodu: 500 iç sunucu hatası

**Senaryo 1:** Configuration Manager sürüm 2002 çalıştırılırken ve CA 'LAR için uzak bir sağlayıcı varsa, Yönetici konsolundan bir iç sunucu hatasıyla karşılaşabilirsiniz.

**Senaryo 2:** Configuration Manager sürüm 2006 ' i çalıştırırken, hizmet bağlantı noktası birincil sitede sağlayıcıya bağlanamazsa ve CA 'lara geri dönmek için bu hatayla karşılaşabilirsiniz. 

**Senaryo 3:** CA 'LAR sürüm 2006 ' e yükseltildiyse ancak birincil sunucu henüz yükseltilmemişse, istekler CAS sağlayıcısı aracılığıyla yönlendirilir. Sağlayıcı uzak ise, yönetim konsolundan bir iç sunucu hatasıyla karşılaşabilirsiniz. 

**Geçici çözüm:** Bu "çift atlama" senaryosuna geçici çözüm için CMPivot makalesinde bulunan [CA 'ların uzak sağlayıcı](../../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) senaryosuna yönelik yönergeleri izleyin.

### <a name="when-multi-factor-authentication-is-enabled-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Multi-Factor Authentication etkin olduğunda, çoğu kiracı iliştirme özelliği çalışmaz
<!--7986450, 7988266-->
**Senaryo:** [Hizmet bağlantı noktasıyla](../../core/servers/deploy/configure/about-the-service-connection-point.md) Iletişim kuran [SMS sağlayıcı](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) makinesi Multi-Factor Authentication kullanmak üzere yapılandırıldıysa, uygulamaları yükleye, CMPivot sorguları çalıştıra, ve Yönetici konsolundan başka işlemler gerçekleştirebileceksiniz. 403 hata kodunu alacaksınız, yasak.  

**Geçici çözüm:** Geçerli geçici çözüm, hiyerarşiyi **Windows kimlik**doğrulamasının varsayılan kimlik doğrulama düzeyine yapılandırmaktır. Daha fazla bilgi için [SMS sağlayıcısı makalesindeki kimlik doğrulama bölümüne](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)bakın.

