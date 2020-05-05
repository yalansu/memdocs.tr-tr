---
title: Ölçüm Özetleme Aracını Çalıştırma
titleSuffix: Configuration Manager
description: Configuration Manager ' de yazılım kullanım ölçümü özetleme görevlerini tetiklemek için ölçüm özetleme 'yi Çalıştır aracını kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723176"
---
# <a name="run-meter-summarization-tool"></a>Ölçüm Özetleme Aracını Çalıştırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Çalışma ölçümü özetleme Aracı, [Configuration Manager araçlarından](tools.md)biridir. Birincil sitelerde yazılım kullanım ölçümü özetlemesi için bakım görevlerini hemen tetiklemek üzere kullanın. Varsayılan olarak, bu görevler, her gün 12:00 ' den sonra başlayan, **site bakım** görevlerinde zamanlandığı gibi çalışır. 

Bu görevler, **MeterData** SQL tablosundaki verileri özetler ve özet sonuçları **fileusagesummary** ve **monthlyusagesummary** tablolarına yazar. Ardından, yazılım kullanım ölçümü raporlarında özetlenen sonucu görürsünüz. Birincil site veritabanına erişebilen Configuration Manager Yönetici Kullanıcı, özetlemeyi çalıştırmak için bu aracı kullanabilir. 

Bu araç, **Dosya Kullanım Özeti** ve **aylık kullanım Özeti** yazılım ölçümü veri özetleme görevlerini çalıştırır. Tüm mevcut ölçüm verilerini olağan 12 saatlik bekleme süresi olmadan özetler. Siteyi, site veritabanını barındıran SQL Server üzerinde çalıştırın. Özetleme başarılı olursa, çıkış kodu olarak `0`ayarlanır. Bir hata oluşursa, çıkış kodu olur `1`.



## <a name="usage"></a>Kullanım

### <a name="command-line"></a>Komut Satırı

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Seçenekler

#### <a name="database-name"></a>Veritabanı adı
SQL Server üzerindeki site veritabanının adı.

#### <a name="delay-in-hours-for-summarization"></a>Özetleme için saat cinsinden gecikme
Araç, gecikmeden önce oluşturulan yazılım kullanım ölçümü kullanımını özetler. Varsayılan olarak, bu gecikme sıfırdır.


### <a name="example"></a>Örnek

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>12 saat önce üretilen yazılım kullanım ölçümü kullanımını özetleyin

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Ayrıca bkz.

- [Bakım görevleri](../servers/manage/maintenance-tasks.md)
- [Yazılım kullanım ölçümü ile uygulama kullanımını izleme](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
