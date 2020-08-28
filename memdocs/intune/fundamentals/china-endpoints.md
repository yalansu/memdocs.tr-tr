---
title: Çin dağıtımları için ağ uç noktaları-Microsoft Intune
titleSuffix: ''
description: Intune için Çin uç noktalarını gözden geçirin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd52b34b70b71874a42486cbdc87cd3d7d2f9037
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994251"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Microsoft Intune Çin uç noktaları

Bu sayfada, Intune dağıtımlarınızdaki ara sunucu ayarları için gereken Çin uç noktaları listelenir.

Güvenlik duvarı ve ara sunucular arkasındaki cihazları yönetmek için Intune iletişimini etkinleştirmeniz gerekir.

- Intune istemcileri iki protokolü de kullandığından, proxy sunucusu hem **HTTP (80)** hem de **HTTPS (443)** desteklemelidir
- Intune bazı görevler (yazılım güncelleştirmelerini indirme gibi) için manage.microsoft.com adresine kimliği doğrulanmamış ara sunucu erişimine ihtiyaç duyar.

Ara sunucu ayarlarını istemci bilgisayarlardan değiştirebilirsiniz. Belirtilen ara sunucu arkasında yer alan tüm istemci bilgisayarların ayarlarını değiştirmek için Grup İlkesi ayarlarını da kullanabilirsiniz.

Yönetilen cihazlar, **Tüm Kullanıcıların** güvenlik duvarları üzerinden hizmetlere erişmesine izin veren yapılandırmalar gerektirir.

Windows 10 otomatik kaydı ve Çin müşterileri için cihaz kaydı hakkında daha fazla bilgi için bkz. [Windows cihazları için kayıt ayarlama](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

Aşağıdaki tabloda Intune istemcisinin eriştiği bağlantı noktaları ve hizmetler listelenir:

|**Uç Noktası**|**IP adresi**|
|---------------------|-----------|
|*. manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>Çin 'de Intune müşteri tarafından belirlenen uç noktalar
- Azure portal: https: \/ /Portal.Azure.cn/
- Microsoft 365: https: \/ /Portal.partner.microsoftonline.cn/
- Intune Şirket Portalı: https: \/ /Portal.Manage.microsoftonline.cn/
- Microsoft Uç Nokta Yöneticisi Yönetim Merkezi: https: \/ /Endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>İş ortağı hizmeti uç noktaları

21Vianet tarafından işletilen Intune, aşağıdaki iş ortağı hizmet uç noktalarına bağlıdır:
- Azure AD Eşitleme hizmeti: https: \/ /SyncService.partner.microsoftonline.cn/DirectoryService.svc
- EVO STS: https: \/ /login.chinacloudapi.cn/
- Azure AD grafiği: https: \/ /Graph.chinacloudapi.us
- MS Graph: https: \/ /microsoftgraph.chinacloudapi.cn
- ADRS: https: \/ /enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Sonraki adımlar
[Çin 'de 21Vianet tarafından işletilen Intune hakkında daha fazla bilgi edinin](china.md)

