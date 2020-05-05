---
title: BitLocker sorunlarını giderme
titleSuffix: Configuration Manager
description: Configuration Manager 'de BitLocker yönetimiyle ilgili sorunları nasıl giderebileceğinizi öğrenin
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723925"
---
# <a name="troubleshoot-bitlocker"></a>BitLocker sorunlarını giderme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager 'de BitLocker yönetimiyle ilgili sorunları gidermenize yardımcı olması için bu makaledeki bilgileri kullanın.

## <a name="server-error-in-self-service"></a>Self Servis 'te sunucu hatası

Self Servis Portalı 'nı (`https://webserver.contoso.com/SelfService`) ilk kez açmaya çalışırken şu hata iletisini görürsünüz:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Bu sorunu gidermeye yönelik **MICROSOFT ASP.NET MVC 4,0** için [önkoşulları](../../plan-design/bitlocker-management.md#prerequisites) Web sunucusuna yüklediğinizden emin olun.

## <a name="see-also"></a>Ayrıca bkz.

BitLocker olay günlüklerini kullanma hakkında daha fazla bilgi için bkz. [BitLocker olay günlükleri](about-event-logs.md).

Bilinen hataların listesi ve olay günlüğü girdilerinin olası nedenleri için aşağıdaki makalelere bakın:

- [İstemci olay günlükleri](client-event-logs.md)
- [Sunucu olay günlükleri](server-event-logs.md)

İstemcilerin BitLocker yönetim ilkesiyle uyumlu olmadığını bildiren nedenleri anlamak için, bkz. [uyumsuzluk kodları](non-compliance-codes.md).
