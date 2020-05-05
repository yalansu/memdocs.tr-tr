---
title: Endpoint Protection'ı yapılandırma
titleSuffix: Configuration Manager
description: Windows Defender için kötü amaçlı yazılım tanımlarını güncelleştirmek ve dağıtmak üzere Configuration Manager ayarlamayı öğrenin.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720887"
---
# <a name="configure-endpoint-protection"></a>Endpoint Protection'ı yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemci bilgisayarlarındaki güvenlik ve kötü amaçlı yazılımları yönetmek için Endpoint Protection kullanabilmeniz için, bu makalede ayrıntılı yapılandırma adımlarını gerçekleştirmeniz gerekir.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Configuration Manager'da Endpoint Protection’ı yapılandırma  
 Configuration Manager Endpoint Protection üründe dış bağımlılıkları ve bağımlılıkları vardır.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Configuration Manager Endpoint Protection yapılandırma adımları  
 Endpoint Protection’ın nasıl yapılandırılacağına dair adımlar, ayrıntılar ve daha fazla bilgi için aşağıdaki tabloyu kullanın.  

> [!IMPORTANT]  
>  Windows 10 bilgisayarları için Endpoint Protection 'ı yönetiyorsanız, Windows Defender için kötü amaçlı yazılım tanımlarını güncelleştirmek ve dağıtmak üzere Configuration Manager yapılandırmanız gerekir. Windows Defender, Windows 10 ' a dahildir ancak Scepınstall ' ın hala yüklü olması ve Endpoint Protection için özel istemci ayarları (aşağıdaki**5. adım** ) hala gereklidir. </br> </br>
> Configuration Manager 1802 ' den başlayarak, Windows 10 cihazlarının Endpoint Protection aracısının (SCEPInstall) yüklü olması gerekmez. Windows 10 cihazlarında zaten yüklüyse Configuration Manager kaldırmaz. Yöneticiler, en az 1802 istemci sürümünü çalıştıran Windows 10 cihazlarında Endpoint Protection aracısını kaldırabilir. SCEPInstall. exe, bazı makinelerde C:\Windows\ccmsetup içinde yine de mevcut olabilir, ancak yeni istemci yüklemelerine İNDİRİLMEMELİDİR. Endpoint Protection için özel istemci ayarları (aşağıdaki**5. adım** ) hala gereklidir. <!--503654-->

|Adımlar|Ayrıntılar|  
|-----------|-------------|  
|**1. Adım:** [Endpoint Protection noktası site sistemi rolü oluşturma](endpoint-protection-site-role.md)|Endpoint Protection’ı kullanabilmeniz için Endpoint Protection noktası site sistemi rolü yüklenmelidir. Yalnızca bir site sistemi sunucusuna yüklenmelidir ve bir merkezi yönetim sitesinde veya bağımsız bir birincil sitede hiyerarşinin en üstüne yüklenmelidir. |  
|**2. Adım:** [Endpoint Protection uyarılarını yapılandırma](endpoint-configure-alerts.md)|Uyarılar kötü amaçlı yazılım bulaşması gibi belirli olaylar oluştuğunda yöneticiyi bilgilendirir. Uyarılar, **İzleme** çalışma alanının **Uyarılar** düğümünde gösterilir veya isteğe bağlı olarak belirli kullanıcılara e-posta ile gönderilebilir. |  
|**3. Adım:** [Endpoint Protection istemcileri için tanım güncelleştirme kaynaklarını yapılandırma](endpoint-definition-updates.md)|Endpoint Protection, tanım güncelleştirmelerini indirmek için çeşitli kaynakları kullanacak şekilde yapılandırılabilir. |  
|**Adım 4:** [varsayılan kötü amaçlı yazılımdan koruma ilkesini yapılandırma ve özel kötü amaçlı yazılımdan koruma ilkeleri](endpoint-antimalware-policies.md)|Endpoint Protection istemcisi yüklendiğinde varsayılan kötü amaçlı yazılımdan koruma ilkesi uygulanır. Dağıttığınız tüm özel ilkeler, istemcinin dağıtılmasından sonraki 60 dakika içinde varsayılan olarak uygulanır. Endpoint Protection istemcisini dağıtmadan önce kötü amaçlı yazılımdan koruma ilkeleri yapılandırdığınızdan emin olun. |  
|**5. Adım:** [Endpoint Protection için özel istemci ayarlarını yapılandırma](endpoint-protection-configure-client.md)|Hiyerarşinizdeki bilgisayar koleksiyonları için Endpoint Protection ayarlarını yapılandırmak üzere özel istemci ayarlarını kullanın.<br /><br /> Not: Bu ayarların hiyerarşinizdeki tüm bilgisayarlara uygulanmasını istediğinizden emin olmadığınız için, varsayılan Endpoint Protection istemci ayarlarını yapılandırmayın. |  
