---
title: Uyumsuzluk kodları
titleSuffix: Configuration Manager
description: BitLocker ilkesiyle uyumlu olmayan bir Configuration Manager istemcisinden olası kodlar için teknik başvuru
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722056"
---
# <a name="non-compliance-codes"></a>Uyumsuzluk kodları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3601034-->

İstemcideki WMI aşağıdaki uyumsuzluk kodlarını sağlar. Ayrıca, belirli bir cihazın uyumsuz olarak raporlamamasının nedenleri açıklanmaktadır.

WMI 'yi görüntülemek için çeşitli yöntemler vardır. Örneğin, aşağıdaki PowerShell komutunu kullanın:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Cihaz uyumluysa, bu komut hiçbir şey döndürmez.
>
> Ayrıca, bu sınıfın, `Compliant` cihaz uyumluysa olan `1` özniteliğini de denetleyebilirsiniz.

|Uyumsuzluk kodu|Uyumsuzluğun nedeni|
|--- |--- |
|0|Şifreleme düzeyi AES 256 değil.|
|1|BitLocker ilkesi, bu birimin şifrelenmesini gerektirir, ancak böyle değildir.|
|2|BitLocker ilkesi, bu birimin şifrelenmesini *not* gerektirir, ancak.|
|3|BitLocker ilkesi için bu birimin TPM koruyucusu kullanması gerekir, ancak bunu yapmaz.|
|4|BitLocker ilkesi, bu birimin TPM + PIN koruyucusu kullanmasını gerektirir, ancak bunu yapmaz.|
|5|BitLocker ilkesi TPM olmayan makinelerin uyumlu olarak raporbağlanmasına izin vermez.|
|6|Birimde bir TPM koruyucusu bulunur, ancak TPM görünür değildir.|
|7|BitLocker ilkesi, bu birimin parola koruyucusu kullanmasını gerektirir, ancak bir tane yoktur.|
|8|BitLocker ilkesi için *Bu birimin parola* koruyucusu kullanması gerekir, ancak bir tane vardır.|
|9|BitLocker ilkesi, bu birimin bir otomatik kilit açma koruyucusu kullanmasını gerektirir, ancak bir tane yoktur.|
|10|BitLocker ilkesi, *Bu birimin bir* otomatik kilit açma koruyucusu kullanmasını gerektirir, ancak bir tane vardır.|
|11|BitLocker, bu birimin uyumlu olduğunu raporlamasını önleyen bir ilke çakışması algılar.|
|12|Bir sistem birimi, işletim sistemi birimini şifrelemek için gereklidir, ancak mevcut değildir.|
|13|Birim için koruma askıya alındı.|
|14|İşletim sistemi birimi şifrelenmemişse otomatik kilit açma koruyucusu güvenli değildir.|
|15|İlke en düşük şifresi üzerinde anlaşılamadı kuvveti için XTS-AES-128 bit, gerçek şifresi üzerinde anlaşılamadı gücü daha zayıf.|
|16|İlke en düşük şifresi üzerinde anlaşılamadı kuvveti için XTS-AES-256 bit, gerçek şifresi üzerinde anlaşılamadı gücü daha zayıf.|
