---
title: Uygulama dağıtımı teknik başvurusu sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager 'de uygulama dağıtımı sorunlarını gidermeye yönelik teknik başvuru.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709820"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Configuration Manager 'de uygulama dağıtımı için teknik başvuru

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, uygulama dağıtımlarının nasıl çalıştığını öğreneceksiniz.

## <a name="before-you-begin"></a>Başlamadan Önce

Uygulama dağıtımlarında sorun giderirken, istemci günlüklerini gözden geçirirken yararlı olabilecek birden çok öğe vardır. Bu öğeler şunları içerir:

- Uygulama CI KIMLIĞI
- Uygulamanın benzersiz KIMLIĞI
- Dağıtım türü benzersiz KIMLIĞI
- Uygulama dağıtımı benzersiz KIMLIĞI (atama benzersiz KIMLIĞI olarak da bilinir)
- Uygulama dağıtım amacı
- İçerik benzersiz KIMLIĞI
- Koleksiyon KIMLIĞI ve adı
- Koleksiyon türü

Sorun gidermeyi kolaylaştırmak için, yukarıda listelenen bilgileri elde etmek üzere Configuration Manager veritabanına benzer bir SQL sorgusu çalıştırabilirsiniz.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> Bu sorguyu yürüttüğünüzde, uygulama özelliklerinin Yazılım Merkezi sekmesinde listelenen yerelleştirilmiş uygulama adını kullanmak yerine uygulama özelliklerinin genel bilgiler sekmesinde listelenen uygulama adını kullanmanız **gerekir** .

## <a name="next-steps"></a>Sonraki Adımlar

- [Uygulama dağıtım Ilkesi](deployment-policy-technical-reference.md)
