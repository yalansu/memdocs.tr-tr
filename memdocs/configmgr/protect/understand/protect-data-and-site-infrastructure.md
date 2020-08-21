---
title: Veri ve site altyapısını koruma
titleSuffix: Configuration Manager
description: Configuration Manager ile kuruluşunuzun kaynaklarını etkilenme veya kötü amaçlı saldırılara karşı nasıl koruyacağınızı öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2a73fff7fd2eb5d630d6047a7da6f131188f06c5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693497"
---
# <a name="protect-data-and-site-infrastructure"></a>Veri ve site altyapısını koruma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kullanıcılarınızın kuruluşunuzun kaynaklarına güvenli bir şekilde erişmesini istiyorsunuz. Hem altyapınızı hem de verilerinizi pozlama veya kötü amaçlı saldırılara karşı koruyun. Erişimi etkinleştirmek ve kuruluşunuzun kaynaklarını korumak için Configuration Manager kullanın.  

- [Endpoint Protection](../deploy-use/endpoint-protection.md) , istemci bilgisayarlar Için aşağıdaki Microsoft Defender ilkelerini yönetmenizi sağlar:

  - Microsoft Defender kötü amaçlı yazılımdan koruma
  - Microsoft Defender güvenlik duvarı
  - Microsoft Defender Gelişmiş Tehdit Koruması
  - Microsoft Defender Exploit Guard
  - Microsoft Defender Application Guard
  - Microsoft Defender uygulama denetimi

  > [!TIP]
  > Ortak yönetilen Windows 10 cihazlarında Endpoint Protection 'ı Microsoft Endpoint Manager bulut hizmetini kullanarak yönetmek için [ **Endpoint Protection** iş yükünü](../../comanage/workloads.md#endpoint-protection) Intune 'a geçirin. Daha fazla bilgi için bkz. [Microsoft Intune Için Endpoint Protection](/intune/endpoint-protection-windows-10).

- BitLocker Sürücü Şifrelemesi (BDE) ile şirket içi Windows istemcilerinde depolanan verileri koruyun. Configuration Manager, Microsoft BitLocker yönetim ve Izleme (MBAD) kullanımını değiştirecek tam BitLocker yaşam döngüsü yönetimi sağlar. Daha fazla bilgi için bkz. [plan for BitLocker Management](../plan-design/bitlocker-management.md).

- Geleneksel parolalar yerine, Iş için Windows Hello 'Yu kullanarak Windows 10 cihazlarında alternatif oturum açma yöntemlerini etkinleştirin. Daha fazla bilgi için bkz. [iş Için Windows Hello ayarları](../deploy-use/windows-hello-for-business-settings.md).

- VPN profillerini kullanarak VPN bağlantısını etkinleştirerek kullanıcılarınızın kaynaklara bağlanma çalışmalarını en aza indirin. Daha fazla bilgi için bkz. [VPN profilleri](../deploy-use/vpn-profiles.md).  

- Wi-Fi profilleri kuruluşunuzdaki cihazlarda kablosuz ağ ayarlarını yönetmenize yardımcı olacak bir araç ve kaynak kümesi sağlar. Bu ayarları dağıtarak, kablosuz ağlara bağlanmak için gereken son kullanıcı çabalarını en aza indirmiş olursunuz. Daha fazla bilgi için bkz. [Wi-Fi profilleri](../deploy-use/create-wifi-profiles.md).  

- Cihazları, kullanıcıların kaynaklara bağlanması için ihtiyaç duyduğu sertifikalarla sağlayın. Daha fazla bilgi için bkz. [sertifika profilleri](../deploy-use/introduction-to-certificate-profiles.md).