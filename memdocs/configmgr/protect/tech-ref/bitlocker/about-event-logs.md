---
title: BitLocker olay günlükleri
titleSuffix: Configuration Manager
description: Sorunları gidermek için Windows olay günlüğü 'nde BitLocker bilgileriyle nasıl çalışacağınızı öğrenin
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: troubleshooting
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef1d5f9a7e8f3c009d1993b82ddef22ce22e235d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128010"
---
# <a name="bitlocker-event-logs"></a>BitLocker olay günlükleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

BitLocker yönetim Aracısı ve Web Hizmetleri, iletileri kaydetmek için Windows olay günlüklerini kullanır. Olay Görüntüleyicisi, **uygulamalar ve hizmetler günlükleri**, **Microsoft**, **Windows**' a gidin. Günlük kanalı (düğüm) bilgisayar ve bileşene bağlı olarak değişir:

- **Mbaı**: istemci bilgisayarda BitLocker yönetim Aracısı
- **Mbaa-Web**:
  - Yönetim noktasındaki kurtarma hizmeti
  - Self servis portalı
  - Yönetim ve web sitesini izleme

Bu günlüklerdeki belirli iletiler hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [İstemci olay günlükleri](client-event-logs.md)
- [Sunucu olay günlükleri](server-event-logs.md)

Her düğümde varsayılan olarak iki günlük kanalı görürsünüz: **yönetici** ve **çalışır**. Daha ayrıntılı sorun giderme bilgileri için [analiz ve hata ayıklama günlüklerini](#bkmk_debug)de gösterebilirsiniz.

## <a name="log-properties"></a>Günlük özellikleri

Windows Olay Görüntüleyicisi 'de belirli bir günlük seçin. Örneğin, **admin**. **Eylem** menüsüne gidin ve **Özellikler**' i seçin. Aşağıdaki ayarları yapılandırın:

- **En büyük günlük boyutu (KB)**: varsayılan olarak, bu ayar `1028` Tüm Günlükler için (1 MB).
- **En yüksek olay günlüğü boyutuna ulaşıldığında**: varsayılan olarak, **yönetici** ve **işletimsel** Günlükler **olayların üzerine yazılacak şekilde ayarlanır (önce en eski olay)**.

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a>Analitik ve hata ayıklama günlükleri

Sorun giderme amacıyla daha ayrıntılı Günlükler sağlayabilirsiniz. Olay Görüntüleyicisi, **Görünüm** menüsüne gidin ve **analitik ve hata ayıklama günlüklerini göster**' i seçin. Artık günlük kanalına gözattığınızda, iki ek günlük görürsünüz: **analitik** ve **hata ayıklama**.

> [!TIP]
> Varsayılan olarak, bu Günlükler aşağıdaki özelliklere sahiptir:
>
> - **Maksimum günlük boyutu (KB)**: `1028` (1 MB)
> - **Olayların üzerine yazma (günlükleri el ile temizle)**

## <a name="export-logs-to-text"></a>Günlükleri metne aktar

Özellikle [analitik ve hata ayıklama günlükleri](#bkmk_debug)ile, tek bir metin dosyasındaki Günlükler girişlerini incelemeyi daha kolay bulabilirsiniz. Olay günlüğü girdilerini metin dosyalarına aktarmak için aşağıdaki PowerShell komutlarını kullanın:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
