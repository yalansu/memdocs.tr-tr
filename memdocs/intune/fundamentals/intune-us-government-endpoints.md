---
title: ABD kamu dağıtımları için ağ uç noktaları-Microsoft Intune
titleSuffix: ''
description: Intune için ABD devlet bitiş noktalarını gözden geçirin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 032e6468ce326637e264b232cdd4e4d954ea70d8
ms.sourcegitcommit: dc2cca9eb70aef15037e8f7d18d671c513bfde85
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90081816"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>Microsoft Intune için ABD devlet uç noktaları

Bu sayfada, Intune dağıtımlarınızdaki ara sunucu ayarları için gereken ABD Kamu, ABD devlet topluluğu (GCC) yüksek ve Savunma Bakanlığı (DoD) uç noktaları listelenmektedir.

Güvenlik duvarı ve ara sunucular arkasındaki cihazları yönetmek için Intune iletişimini etkinleştirmeniz gerekir.

- Intune istemcileri iki protokolü de kullandığından, proxy sunucusu hem **HTTP (80)** hem de **HTTPS (443)** desteklemelidir
- Intune bazı görevler (yazılım güncelleştirmelerini indirme gibi) için manage.microsoft.com adresine kimliği doğrulanmamış ara sunucu erişimine ihtiyaç duyar.

Ara sunucu ayarlarını istemci bilgisayarlardan değiştirebilirsiniz. Belirtilen ara sunucu arkasında yer alan tüm istemci bilgisayarların ayarlarını değiştirmek için Grup İlkesi ayarlarını da kullanabilirsiniz.

Yönetilen cihazlar, **Tüm Kullanıcıların** güvenlik duvarları üzerinden hizmetlere erişmesine izin veren yapılandırmalar gerektirir.

ABD kamu müşterileri için Windows 10 otomatik kaydı ve cihaz kaydı hakkında daha fazla bilgi için bkz. [Windows cihazları için kayıt ayarlama](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

Aşağıdaki tabloda Intune istemcisinin eriştiği bağlantı noktaları ve hizmetler listelenir:

|**Uç Noktası**|**IP adresi**|
|---------------------|-----------|
|*. manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>ABD devlet müşteri tarafından belirlenen uç noktalar:
- Azure portal: https: \/ /Portal.Azure.us/ 
- Microsoft 365: https: \/ /Portal.office365.us/ 
- Intune Şirket Portalı: https: \/ /Portal.Manage.Microsoft.us/ 
- Microsoft Uç Nokta Yöneticisi Yönetim Merkezi: https: \/ /Endpoint.Microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Intune 'un bağımlı olduğu iş ortağı hizmeti uç noktaları:
- Azure AD Eşitleme hizmeti: https: \/ /SyncService.gov.us.microsoftonline.com/DirectoryService.svc
- EVO STS: https: \/ /login.microsoftonline.us
- Dizin proxy 'Si: https: \/ /directoryproxy.MicrosoftAzure.us/DirectoryProxy.svc
- Azure AD grafiği: https: \/ /Directory.MicrosoftAzure.us ve https: \/ /Graph.MicrosoftAzure.us
- MS Graph: https: \/ /Graph.Microsoft.us
- ADRS: https: \/ /enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Sonraki adımlar
[Microsoft Intune için ağ uç noktaları](intune-endpoints.md)

