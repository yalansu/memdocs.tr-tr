---
title: İnternetteki istemcileri yönetme
titleSuffix: Configuration Manager
description: Configuration Manager 'de, bulut yönetimi ağ geçidi ve internet tabanlı istemci yönetimiyle istemcileri yönetme hakkında bilgi edinin.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c00d480b993498c5fa27e2a4d91a5f2a3bc130ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710632"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Configuration Manager ile internet 'te istemcileri yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Genellikle Configuration Manager, yönetilen bilgisayarların ve sunucuların çoğu, yönetim işlevlerini gerçekleştiren site sistem sunucularıyla fiziksel olarak aynı dahili ağ üzerinde bulunur. Ancak, internet 'e bağlıyken, iç ağınız dışındaki istemcileri yönetebilirsiniz. Bu özellik, istemcilerin site sistem sunucularına ulaşmak için VPN üzerinden bağlanmasını gerektirmez.

Configuration Manager, internet 'e bağlı istemcileri yönetmek için iki yol sunar:

-   Bulut yönetimi ağ geçidi

-   Internet tabanlı istemci yönetimi


## <a name="cloud-management-gateway"></a>Bulut yönetimi ağ geçidi

Bulut yönetimi ağ geçidi, Internet tabanlı istemcilerin yönetimini sağlar. Microsoft Azure bulut hizmeti ve bu hizmetle iletişim kuran yeni bir site sistemi rolü birleşimini kullanır. Internet tabanlı istemciler, şirket içi Configuration Manager iletişim kurmak için bulut hizmetini kullanır.

#### <a name="advantages"></a>Yararları  

-   Ek şirket içi altyapı yatırımı gerekli değildir.  

-   Şirket içi altyapıyı Internet 'e sunmaz.  

-   Hizmeti çalıştıran bulut sanal makineleri, Azure tarafından tam olarak yönetilir ve bakım gerektirmez.  

-   Configuration Manager konsolunda kolayca ayarlanır ve yapılandırılır.  

#### <a name="disadvantages"></a>Dezavantajlar  

-   Bulut aboneliği maliyeti.  

-   Bulut hizmeti aracılığıyla gönderilen yönetim verileri.  

Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidini planlayın](cmg/plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Internet tabanlı istemci yönetimi

Bu yöntem, istemcilerinin yönetim amaçlarıyla iletişim kurduğu internet 'e yönelik site sistem sunucularına bağımlıdır. İstemcilerin ve site sistem sunucularının Internet tabanlı yönetim için yapılandırılmasını gerektirir.

#### <a name="advantages"></a>Yararları  

-   Bulut hizmeti bağımlılığı yok.  

-   Bulut aboneliğiyle ilişkili ek maliyet yok.  

-   Hizmeti sağlayan sunucuların ve rollerin tam denetimi.  

#### <a name="disadvantages"></a>Dezavantajlar  

-   Ek altyapı yatırımı gerektir.  

-   Ek altyapının ek yükü ve operasyonel maliyeti.  

-   Altyapı internet 'e açık olmalıdır.  

Daha fazla bilgi için bkz. [Internet tabanlı istemci yönetimi Için plan](plan-internet-based-client-management.md).  
