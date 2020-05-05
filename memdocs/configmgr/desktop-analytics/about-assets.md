---
title: Masaüstü analizinden varlıklar
titleSuffix: Configuration Manager
description: Masaüstü Analizi 'nde cihazlar, sürücüler ve uygulamalar hakkında bilgi edinin.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722553"
---
# <a name="assets-in-desktop-analytics"></a>Masaüstü analizinden varlıklar

Cihazlar, verileri masaüstü analizine rapor ettikten sonra, aşağıdaki varlıkların envanterini sağlar:

- Cihazlar
- Yüklenen uygulamalar  

Hizmet portalında, masaüstü Analizi menüsünde **varlıklar** ' ı seçin.

## <a name="devices"></a>Cihazlar

**Cihazlar** sekmesi, kuruluşunuzda masaüstü analizine kaydolmasını istediğiniz tüm cihazlar hakkındaki önemli bilgileri görüntüler. Belirli değerler için herhangi bir sütun veya filtre üzerinde sıralama yapabilirsiniz.

> [!NOTE]  
> Pano, ortamınız için görmeyi düşündüğünüz cihaz sayısını bildirmezse, bkz. [Masaüstü Analizi sorun giderme](troubleshooting.md).  

Bir dağıtım planında, cihazlar hakkında daha fazla ayrıntı vardır. Daha fazla bilgi için bkz. [varlıkları planlayın](about-deployment-plans.md#plan-assets)

## <a name="apps"></a>Uygulamalar

**Uygulamalar** sekmesi, Windows cihazlarınızda hizmetin algıladığı tüm yüklü uygulamaları gösterir.

En **önemli uygulamalar,** kayıtlı cihazların %2 ' inden fazlasına yüklendi.

Aşağıdaki kategorilerden birini ayarlayarak uygulamaların **önemini** yapılandırın:

- Kritik
- Önemli
- Yoksayma
- Gözden geçirilmedi
- Önemli değil<!-- 3587232 -->

Listeden uygulamayı seçin ve **Düzenle**' yi seçin. Bu eylem, uygulamanın ayrıntılarını görüntüler. **Önem** açılan menüsünü seçin ve bir değer ayarlayın. Ayrıca, bir **sahip**atayabilirsiniz. Herhangi bir değişiklik yaparsanız **Kaydet**' i seçin.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" />Sistem ve Mağaza uygulamalarının otomatik yükseltme kararı

<!-- 3587232 -->
Masaüstü Analizi iş akışındaki tüm önemli uygulamalarda **önem** ve **yükseltme kararının** belirlenmesi önemlidir. Bu uygulamalara not ekleme çabalarınızı azaltmaya yardımcı olmak için bazı uygulama türleri otomatik olarak *önemli değildir*olarak işaretlenir. Bu uygulamalar için dağıtım planı yükseltme kararı Ayrıca, *hazırlık*olarak işaretlenir. Aşağıdaki uygulamalar uyumludur ve Windows yükseltildikten sonra çalışmaya devam etmelidir:

- Microsoft tarafından yayınlanan sistem uygulamaları ve bileşenleri

- Microsoft Store yönetilen ve güncelleştirilmiş uygulamalar

> [!TIP]
> Tüm uygulamalar için girişleri genel düzeyde veya dağıtım planına göre yönetin.
>
> 1. Masaüstü Analizi portalında, **Yönet** menüsünde, **varlıklar**' ı seçin. Ardından **uygulamalar**' ı seçin.
>
> 2. Bu uygulama kategorilerini yönetmek için **tür** ve **Kategori** sütunlarını kullanın:
>
>    - Mağaza uygulamaları için **türü** **modern** olarak filtrele
>    - Sistem uygulamaları için **kategoriyi** **arka plan işlemi** veya **Windows bileşeni** olarak filtreleyin

Bir dağıtım planında, **yükseltme kararlarını**da ayarlayabilirsiniz. Daha fazla bilgi için bkz. [varlıkları planlayın](about-deployment-plans.md#plan-assets)

### <a name="usage"></a>Kullanım

<!-- 5533890 -->

- **Toplam yükleme**sayısı: Bu değer, Seçilen uygulamanın tüm masaüstü Analizi kayıtlı cihazlarda yükleme sayısıdır.

- **Yüklemeyi yüzde**: Bu değer, Seçilen uygulamanın toplam masaüstü Analizi kayıtlı cihazlara karşı yüklemesi yüzdesidir.

- **Bu uygulamayı son 30 gün içinde Başlatan cihazlar**: Bu değer, bir kullanıcının seçili uygulamayı başlatıldığı cihazların sayısıdır. Yalnızca son 30 gün içinde kullanımı bildirilen cihazları içerir. Bu sayı, Windows 10 ' un herhangi bir sürümünde çalışan masaüstü analiziyle kaydedilen tüm cihazlarınızda bulunur. Bu sayı, bir dağıtım planı için değişebiliyor olabilir.

## <a name="next-steps"></a>Sonraki adımlar

- [Masaüstü Analizi dağıtım planları hakkında bilgi edinin](about-deployment-plans.md)  

- [Güvenlik ve özellik güncelleştirmeleri hakkında bilgi edinin](about-updates.md)  

- [Masaüstü Analizi 'nde uyumluluk değerlendirmesi](compat-assessment.md)  
