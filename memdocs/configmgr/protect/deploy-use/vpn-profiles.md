---
title: VPN profilleri
titleSuffix: Configuration Manager
description: VPN ayarlarını kuruluşunuzdaki kullanıcılara dağıtmak için Configuration Manager 'da VPN profillerini nasıl kullanacağınızı öğrenin.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722259"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Configuration Manager'daki VPN profilleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1283610-->
Kuruluşunuzdaki kullanıcılara VPN ayarlarını dağıtmak için Configuration Manager ' deki VPN profillerini kullanın. Bu ayarları dağıtarak, şirket ağındaki kaynaklara bağlanmak için gereken son kullanıcı çabasını en aza indirirsiniz.  

Örneğin, tüm Windows 10 cihazlarını iç ağdaki bir dosya paylaşımıyla bağlantı kurmak için gereken ayarlarla yapılandırmak istiyorsunuz. İç ağa bağlanmak için gereken ayarlarla bir VPN profili oluşturun. Ardından bu profili Windows 10 çalıştıran cihazlara sahip olan tüm kullanıcılara dağıtın. Bu kullanıcılar, kullanılabilir ağlar listesindeki VPN bağlantısını görür ve az çaba ile bağlanabilir.

Bir VPN profili oluşturduğunuzda, çok çeşitli güvenlik ayarları ekleyebilirsiniz. Bu ayarlar, Configuration Manager sertifika profilleriyle sağladığınız sunucu doğrulaması ve istemci kimlik doğrulaması sertifikalarını içerir. Daha fazla bilgi için bkz. [sertifika profilleri](introduction-to-certificate-profiles.md).

> [!Note]
> Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="supported-platforms"></a>Desteklenen platformlar

Aşağıdaki tabloda, çeşitli cihaz platformları için yapılandırabileceğiniz VPN profilleri açıklanmaktadır.

|Bağlantı türü|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Yes|Hayır|Yes|Yes|
|**F5 Edge Client**|Yes|Hayır|Yes|Yes|
|**Dell SonicWALL Mobile Connect**|Yes|Hayır|Yes|Yes|
|**Check Point Mobile VPN**|Yes|Hayır|Yes|Yes|
|**Microsoft SSL (SSTP)**|Yes|Yes|Yes|Hayır|
|**Microsoft Automatic**|Yes|Yes|Yes|Hayır|
|**IKEv2**|Yes|Yes|Yes|Hayır|
|**PPTP**|Yes|Yes|Yes|Hayır|
|**L2TP**|Yes|Yes|Yes|Hayır|

## <a name="next-step"></a>Sonraki adım

> [!div class="nextstepaction"]
> [VPN profilleri oluşturma](create-vpn-profiles.md)

## <a name="see-also"></a>Ayrıca bkz.

- [VPN profilleri için önkoşullar](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [VPN profilleri için güvenlik ve Gizlilik](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
