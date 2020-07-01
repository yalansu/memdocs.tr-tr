---
title: Masaüstü Analizi 'ndeki güncelleştirmeler
titleSuffix: Configuration Manager
description: Masaüstü analizinden güvenlik ve özellik güncelleştirmeleri hakkında bilgi edinin.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 96a014f4919480854b57bae82e982ce783f5f59b
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590975"
---
# <a name="updates-in-desktop-analytics"></a>Masaüstü Analizi 'ndeki güncelleştirmeler

Masaüstü Analizi portalında, güvenlik ve özellik güncelleştirmelerinin durumunu görüntüleyin. Masaüstü Analizi ana menüsünün Izleyici grubunda bu düğümleri seçin. Bu düğümler, ortamınızdaki bu güncelleştirmelerin durumu hakkında bilgiler sağlar.

<!--7362999-->

> [!IMPORTANT]
> Masaüstü analizi, masaüstü Analizi çalışma alanınız ile ilişkili ticari KIMLIĞE sahip cihazlara yönelik güvenlik ve özellik güncelleştirme durumunu görüntüler. Bu davranış, cihazları Configuration Manager ile kaydetmeksizin kaydolmadığınız bir durum oluşur. Bu kutucukların toplam cihaz sayısı [**bağlı hizmetlerde**](monitor-connection-health.md#commercial-id-configuration)kayıtlı cihazların sayısıyla eşleşmeyebilir.

## <a name="security-updates"></a>Güvenlik güncelleştirmeleri

Güvenlik güncelleştirmelerinin geçerli durumunu gözden geçirmek için, masaüstü Analizi 'nin **izleme** bölümünde **güvenlik güncelleştirmeleri** ' ni seçin:

![Masaüstü analizinin güvenlik güncelleştirmeleri düğümü](media/security-updates.png)

Bu görünüm Windows 10 çalıştıran cihazlar için *güvenlik* güncelleştirmelerini özetler. Çubuk grafikteki cihazlar aşağıdaki etiketlere göre kategorize edilir:

#### <a name="latest"></a>En son

Cihazlar bu sürüm ve kanal için en son güvenlik güncelleştirmesini çalıştırıyor.

#### <a name="latest-1"></a>En son-1

Cihazlarda bir güvenlik güncelleştirmesi, bu kanaldaki en son kullanılabilir güncelleştirmeden daha eski bir sürümü çalıştırıyor.

#### <a name="older"></a>Daha eski

Cihazlarda en son-1 ' den daha eski bir güvenlik güncelleştirmesi çalışmaktadır.

#### <a name="not-measured"></a>Ölçülmedi

Masaüstü Analizi cihazı değerlendirmedi. Bu durum Windows 7, Windows 8.1 veya Windows Insider programı için kayıtlı Windows 10 cihazlarını çalıştıran cihazları içerir.  

Güvenlik güncelleştirmelerine yönelik benimseme eğilimlerini görmek için, belirli bir Windows sürümü için **daha fazla görüntüle** ' yi seçin. Yığılmış alan grafiği, cihazları zamana göre yüklemiş oldukları güvenlik güncelleştirmesine göre kategorilere ayırır.

Güvenlik güncelleştirmelerinin dağıtım durumunu gözden geçirmek için **Tümünü görüntüle**' yi seçin. Bu görünüm aşağıdaki kategorilerdeki cihazları listeler:

- Başlamadı
- Sürüyor
- Tamamlandı
- Dikkat edilmesi gereken (cihaz adına göre sıralanmış) cihazlar
- Dikkat edilmesi gereken noktalar (sorun türüne göre sıralanmış)

Hizmetin hala işlediği yeni bilgilerle cihazları göstermek için **son verileri görüntüle**' yi seçin. Masaüstü analizi, bir sonraki tam veri yenilemesinin ardından bu bilgileri gösterir.

  > [!IMPORTANT]
  > **Son verileri görüntülemek** Için masaüstü Analizi seçeneği kullanım dışıdır. Bu eylem, daha sonraki bir masaüstü Analizi hizmeti sürümünde kaldırılacaktır. Daha fazla bilgi için bkz. [kullanımdan kaldırılan özellikler](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

## <a name="feature-updates"></a>Özellik güncelleştirmeleri

Özellik güncelleştirmelerinin geçerli durumunu gözden geçirmek için, masaüstü Analizi 'nin **izleme** bölümünde **özellik güncelleştirmeleri** ' ni seçin:

![Masaüstü analizinin özellik güncelleştirmeleri düğümü](media/feature-updates.png)

Bu görünüm, Windows 10 çalıştıran cihazlar için *özellik* güncelleştirmelerini özetler.

Hizmet dönemleri hakkında daha fazla bilgi için bkz. [Windows yaşam döngüsü olgu sayfası](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Çubuk grafikteki cihazlar aşağıdaki etiketlere göre kategorize edilir:

#### <a name="in-service"></a>Hizmette

Cihazlar, bu sürüm ve kanal için en son özellik güncelleştirmesini çalıştırıyor.  

#### <a name="near-end-of-service"></a>Hizmetin sonuna yakın

Cihazlarda hizmet sonuna ulaşmak için 90 gün içinde olan bir özellik güncelleştirmesi çalışmaktadır.

#### <a name="end-of-service"></a>Hizmet sonu

Cihazlar, hizmet bitiş tarihinin ötesinde bir özellik güncelleştirmesi çalıştırıyor. Bu tarihler Windows 'un Enterprise ve eğitim sürümlerine özeldir. Bunlar Home, Pro, Pro eğitim veya Iş Istasyonları için Pro sürümleri için geçerlidir. Daha fazla bilgi için bkz. [Windows yaşam döngüsü olgu sayfası](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>Ölçülmedi

Masaüstü Analizi cihazı değerlendirmedi. Bu durum Windows 7, Windows 8.1 veya Windows Insider programı için kayıtlı Windows 10 cihazlarını çalıştıran cihazları içerir.

Özellik güncelleştirmelerine yönelik benimseme eğilimlerini görmek için kutucuğu seçin. Yığılmış alan grafiği, cihazları zamana göre yüklemiş oldukları Özellik güncelleştirmesine göre kategorilere ayırır.

## <a name="next-steps"></a>Sonraki adımlar

- [Masaüstü Analizi varlıkları hakkında bilgi edinin](about-assets.md): cihazlar, sürücüler ve uygulamalar  

- [Dağıtım planları hakkında bilgi edinin](about-deployment-plans.md)  
