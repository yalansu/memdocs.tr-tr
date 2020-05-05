---
title: Ağ altyapısı
titleSuffix: Configuration Manager
description: Configuration Manager iletişimleri için hazırlanmak üzere güvenlik duvarları, bağlantı noktaları ve etki alanları ayarlayın.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719844"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Configuration Manager için ağ altyapısı konuları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Ağınızı Configuration Manager destekleyecek şekilde hazırlamak için bazı altyapı bileşenlerini yapılandırmanız gerekebilir. Örneğin, Configuration Manager tarafından kullanılan iletişimleri geçirmek için güvenlik duvarı bağlantı noktalarını açın.  

## <a name="ports-and-protocols"></a>Bağlantı noktaları ve protokoller

Farklı Configuration Manager özellikleri farklı ağ bağlantı noktaları kullanır. Bazı bağlantı noktaları gereklidir ve bazıları özelleştirebilirsiniz.

Çoğu Configuration Manager iletişim, HTTPS için bağlantı noktası 80 veya HTTPS için 443 gibi ortak bağlantı noktalarını kullanır. Bazı site sistem rolleri özel Web siteleri ve özel bağlantı noktaları kullanımını destekler. Daha fazla bilgi için bkz. [site sistemi sunucuları Için Web siteleri](websites-for-site-system-servers.md).

Configuration Manager dağıtmadan önce, kullanmayı planladığınız bağlantı noktalarını belirleyin ve gerektiğinde güvenlik duvarlarını ayarlayın.

Configuration Manager yükledikten sonra, bir bağlantı noktasını değiştirmeniz gerekiyorsa, cihazlarda ve ağda güvenlik duvarlarını güncelleştirmeyi unutmayın. Ayrıca Configuration Manager bağlantı noktasının yapılandırmasını değiştirin.

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [İstemci iletişim bağlantı noktalarını yapılandırma](../../clients/deploy/configure-client-communication-ports.md)
- [Configuration Manager kullanılan bağlantı noktaları](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>İnternet erişimi gereksinimleri

Bazı Configuration Manager özellikleri, tüm işlevler için internet bağlantısı kullanır. Kuruluşunuz ağ iletişimini bir güvenlik duvarı veya ara cihaz kullanarak internet ile kısıtlarsa gerekli uç noktalara izin vermeyi unutmayın.

Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](internet-endpoints.md)


## <a name="proxy-servers"></a>Ara sunucular

Farklı site sistem sunucuları ve istemcileri için ayrı proxy sunucuları belirtebilirsiniz. Bu konfigürasyonları, bir site sistem rolü veya istemcisi yüklerken veya daha sonra gerektiği şekilde değiştirdiğinizde yaparsınız.

Daha fazla bilgi için bkz. [proxy sunucu desteği](proxy-server-support.md).
