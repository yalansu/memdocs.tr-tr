---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/26/2020
ms.openlocfilehash: c450cff20df5dd45daa8097b8132f00d51bf713d
ms.sourcegitcommit: 0d2f6132428b5fa994e5b770ab1d2bf7d78ac179
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84226695"
---
<!--This file is shared by the CMPivot script samples articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->


## <a name="operating-system"></a>İşletim sistemi

İşletim sistemi bilgilerini alır.

```kusto
// Sample query for OS information
OperatingSystem
```

## <a name="recently-used-applications"></a>Son kullanılan uygulamalar

Aşağıdaki sorgu son kullanılan uygulamaları alır (son 2 saat):

```kusto
CCMRecentlyUsedApplications
| where (LastUsedTime > ago(2h))
| project CompanyName, ProductName, ProductVersion, LastUsedTime
```

## <a name="device-start-times"></a>Cihaz başlangıç zamanları

Aşağıdaki sorgu, son yedi gün içinde cihazların ne zaman başlatıldığını gösterir:

```kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
```

## <a name="free-disk-space"></a>Boş disk alanı

Aşağıdaki sorgu boş disk alanını gösterir:

```kusto
LogicalDisk
| project Device, DeviceID, Name, Description, FileSystem, Size, FreeSpace
| order by DeviceID asc
```

## <a name="device-information"></a>Cihaz bilgileri

Cihazı, üreticiyi, modeli ve OSVersion 'yi göster:

```kusto 
ComputerSystem
| project Device, Manufacturer, Model
| join (OperatingSystem | project Device, OSVersion=Caption)
```

## <a name="boot-times-for-a-device"></a>Bir cihazın önyükleme zamanları

Cihazların önyükleme zamanlarını göster:

```kusto
SystemBootData
| project Device, SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
| order by SystemStartTime desc
```

## <a name="authentication-failures"></a>Kimlik doğrulaması hataları

Olay günlüklerinde kimlik doğrulama hatalarıyla ilgili arama yapın.

```kusto
EventLog('Security')
| where  EventID == 4673
```

## <a name="processmoduleprocessname"></a>ProcessModule ( \<processname> )  

Belirli bir işlem tarafından yüklenen tüm modülleri (dll 'ler) numaralandırır. ProcessModule, meşru işlemlerde gizlemekte olan kötü amaçlı yazılımlara yönelik arama yaparken yararlıdır.  

```kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

## <a name="antimalware-software-status"></a>Kötü amaçlı yazılımdan koruma yazılımı durumu

Bilgisayarda yüklü olan kötü amaçlı yazılımdan koruma yazılımının durumunu alır.

```kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
```

## <a name="find-bios-manufacturer-that-contains-any-word-like-micro"></a>Mikro gibi herhangi bir sözcük içeren BIOS üreticisini bulun

```kusto
Bios
// Find BIOS Manufacturer that contains any word like Micro, such as Microsoft
| where Manufacturer like '%Micro%'
```

## <a name="find-file-by-its-hash"></a>Karma olarak dosya bul

Karma olarak bir dosya arayın.

```kusto
Device
| join kind=leftouter ( File('%windir%\\system32\\*.exe')
| where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
| project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
```

## <a name="find-scripts-in-the-ccm-logs-in-the-last-hour"></a>Son saatteki CCM günlüklerinde ' betikleri ' bulma

Aşağıdaki sorgu son 1 saat içindeki olaylara bakacaktır:

```kusto
CcmLog('Scripts',1h)
```

