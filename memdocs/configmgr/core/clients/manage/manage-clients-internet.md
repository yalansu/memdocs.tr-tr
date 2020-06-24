---
title: İnternetteki istemcileri yönetme
titleSuffix: Configuration Manager
description: Configuration Manager 'de, bulut yönetimi ağ geçidi ve internet tabanlı istemci yönetimiyle istemcileri yönetme hakkında bilgi edinin.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715603"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Configuration Manager ile internet 'te istemcileri yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Genellikle Configuration Manager, yönetilen bilgisayarların ve sunucuların çoğu, yönetim işlevlerini gerçekleştiren site sistem sunucularıyla fiziksel olarak aynı dahili ağ üzerinde bulunur. Ancak, internet 'e bağlıyken, iç ağınız dışındaki istemcileri yönetebilirsiniz. Bu özellik, istemcilerin site sistem sunucularına ulaşmak için VPN üzerinden bağlanmasını gerektirmez.

Configuration Manager, internet 'e bağlı istemcileri yönetmek için iki yol sunar:

- Bulut yönetimi ağ geçidi

- Internet tabanlı istemci yönetimi

> [!NOTE]
> Tek bir site için her iki hizmetin birleşimini kullanabilirsiniz. Bir cihaz hem ICM hem de CMG için siteden ilke alırsa, bu iletişim için bunlar arasında rastgele olur. İletişimi denetlemek için kullanılabilen tek mekanizma istemci kimlik doğrulamadır. Örneğin, Azure AD 'ye katılmış bir istemci, internet tabanlı yönetim noktasının sunucu kimlik doğrulama sertifikasına güvenmezse, yalnızca CMG kullanabilir. Etki alanına katılmış bir istemci, CMG 'nin sunucu kimlik doğrulama sertifikasına güvenmezse, yalnızca Internet tabanlı yönetim noktasını kullanabilir.<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>Bulut yönetimi ağ geçidi

Bulut yönetimi ağ geçidi, Internet tabanlı istemcilerin yönetimini sağlar. Microsoft Azure bulut hizmeti ve bu hizmetle iletişim kuran şirket içi site sistem rolü birleşimini kullanır. Internet tabanlı istemciler, şirket içi Configuration Manager iletişim kurmak için bulut hizmetini kullanır.

### <a name="cmg-advantages"></a>CMG avantajları

- Ek şirket içi altyapı yatırımı gerekli değildir.  

- Şirket içi altyapıyı Internet 'e sunmaz.  

- Hizmeti çalıştıran bulut sanal makineleri, Azure tarafından tam olarak yönetilir ve bakım gerektirmez.  

- Configuration Manager konsolunda kolayca ayarlanır ve yapılandırılır.  

### <a name="cmg-disadvantages"></a>CMG dezavantajları  

- Bulut aboneliği maliyeti.  

- Bulut hizmeti aracılığıyla gönderilen yönetim verileri.  

Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidini planlayın](cmg/plan-cloud-management-gateway.md).  

## <a name="internet-based-client-management"></a>Internet tabanlı istemci yönetimi

Bu yöntem, istemcilerin yönetim amaçlarıyla doğrudan iletişim kurduğu internet 'e yönelik site sistem sunucularına bağımlıdır. İstemcilerin ve site sistem sunucularının Internet tabanlı istemci yönetimi (IBCM) için yapılandırılmasını gerektirir.

### <a name="ibcm-advantages"></a>IBCM avantajları

- Bulut hizmeti bağımlılığı yok.  

- Bulut aboneliğiyle ilişkili ek maliyet yok.  

- Hizmeti sağlayan sunucuların ve rollerin tam denetimi.  

### <a name="ibcm-disadvantages"></a>IBCM dezavantajları

- Ek altyapı yatırımı gerektir.  

- Ek altyapının ek yükü ve operasyonel maliyeti.  

- Altyapı internet 'e açık olmalıdır.  

Daha fazla bilgi için bkz. [Internet tabanlı istemci yönetimi Için plan](plan-internet-based-client-management.md).  
