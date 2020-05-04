---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716176"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a>Donanım envanteri raporları

<!--5468413-->
Donanım envanterini temel alan bir rapor çalıştırmaya çalışırsanız bir hata döndürür. Örneğin, bir BitLocker raporu aşağıdaki iletiye benzer bir hata döndürür:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

Ayrıca, **veridr. log** dosyasında şu hatayı görebilirsiniz:

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Donanım envanterini kullanan konsol panoları da etkilenebilir.

Bu sorun, belirli donanım envanteri tablolarında bir veritabanı şeması değişikliği nedeniyle oluşur.

#### <a name="workaround"></a>Geçici çözüm

Geçici çözüm, önceden var olan özniteliği veritabanından bırakmaya yönelik bir çözümdür. Dataloader site bileşeni daha sonra yeni bir öznitelik oluşturabilir. Tablo şemasını onarmak için aşağıdaki SQL betiğini site veritabanı sunucusunda çalıştırın:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
