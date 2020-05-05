---
title: Cihaz eylemi sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager için cihaz eylemleri teknik başvurusu sorunlarını giderme
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717597"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Configuration Manager cihazları için cihaz eylemleri sorunlarını giderme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager 2002 ' den başlayarak Configuration Manager istemcileri Microsoft Endpoint Manager Yönetim Merkezi ile eşitlenebilir. Bazı istemci eylemleri, eşitlenen istemcilerde Microsoft Endpoint Manager yönetim merkezinden çalıştırılabilir.

Kullanılabilir eylemler şunlardır:
- Makine Ilkesini Eşitle
- Kullanıcı Ilkesini eşitleme
- Uygulama değerlendirme çevrimi


[![Microsoft Endpoint Manager Yönetim Merkezi 'nde cihaza genel bakış](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
Bir yönetici Microsoft Endpoint Manager Yönetim Merkezi 'nden bir eylem çalıştırdığında, bildirim isteği Configuration Manager siteye ve siteden istemciye iletilir.

## <a name="configuration-manager-components"></a>Configuration Manager bileşenleri

- **SMS_SERVICE_CONNECTOR**: Microsoft Endpoint Manager yönetim merkezinden gelen bildirimi Işlemek Için ağ geçidi bildirim çalışanını kullanır.
- **SMS_NOTIFICATION_SERVER**: bildirimi alır ve bir istemci bildirimi oluşturur.
- **Bgbagent**: istemci görevi alır ve istenen eylemi çalıştırır.

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Microsoft Endpoint Manager yönetim merkezinden bir eylem başlatıldığında, **Cmgatewaynotificationworker. log** isteği işler.  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Microsoft Endpoint Manager Yönetim Merkezi 'nden bir bildirim alındı.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. Kullanıcı ve cihaz eylemleri onaylanır.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. Uzak görev SMS_NOTIFICATION_SERVER iletilir.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

İleti SMS_NOTIFICATION_SERVER gönderildikten sonra, yönetim noktasından karşılık gelen istemciye bir görev gönderilir. Aşağıda, yönetim noktasındaki **Bgbserver. log**dosyasında aşağıdaki noktaları görürsünüz:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

Son adım istemcisinde oluşur ve **CCMNotificationAgent. log**dosyasında görülebilir. Görev alındıktan sonra, eylemi gerçekleştirmek için Zamanlayıcı ister. Eylem gerçekleştirildiğinde, bir onay iletisi görürsünüz:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Genel sorunlar

Yönetici Configuration Manager için gerekli izinlere sahip değilse, **Cmgatewaynotificationworker. log**dosyasında `Unauthorized` bir yanıt görürsünüz.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Microsoft Endpoint Manager Yönetim Merkezi 'nden eylemi çalıştıran kullanıcının Configuration Manager sitesinde gerekli izinlere sahip olduğundan emin olun. Daha fazla bilgi için bkz. [Microsoft Endpoint Manager kiracı iliştirme önkoşulları](device-sync-actions.md#prerequisites).

## <a name="next-steps"></a>Sonraki adımlar

Koşullu erişim gibi ek bulut destekli yetenekler almak için [ortak Yönetimi etkinleştirin](../comanage/overview.md) .
