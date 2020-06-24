---
title: Masaüstü analizinden varlıklar
titleSuffix: Configuration Manager
description: Masaüstü Analizi 'nde cihazlar, sürücüler ve uygulamalar hakkında bilgi edinin.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: f87c4cc1bcbe8039acb5876dc8e26ac597f12e59
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107297"
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

**Uygulama sürümleri ayrıntıları** ayarı varsayılan olarak kapalıdır, bu nedenle bu sekme, tüm uygulama sürümlerini aynı ad ve yayımcıya birleştirir.<!-- 5542186 --> Varsayılan davranış, gördüğünüz toplam uygulama sayısını azaltmaya yardımcı olur ve bu da uygulamalara açıklama ekleme çabalarınızı azaltmaya yardımcı olur. Önemli **uygulamalar** kutucuğunda uygulama sayısı da bu ayarı yansıtır. Örneğin, Microsoft Edge 'in yüzlerce örneğini listelemek yerine, tüm sürümler için bir örnek vardır. Tüm sürümler için kararları bir kez daha yapabilirsiniz. Bir uygulamanın belirli sürümleri hakkında kararlar almanız gerekiyorsa, bu ayarı açın. Bu ayarı, bir dağıtım planıyla çalışırken da yapılandırabilirsiniz. Daha fazla bilgi için bkz. [varlıkları planlayın](about-deployment-plans.md#plan-assets).

Listeden uygulamayı seçin ve **Düzenle**' yi seçin. Bu eylem, uygulamanın ayrıntılarını görüntüler. **Önem** açılan menüsünü seçin ve bir değer ayarlayın. Ayrıca, bir **sahip**atayabilirsiniz. Herhangi bir değişiklik yaparsanız **Kaydet**' i seçin.

Aşağıdaki kategorilerden birini ayarlayarak uygulamaların **önemini** yapılandırın:

- Kritik
- Önemli
- Yoksayma
- Gözden geçirilmedi
- Önemli değil<!-- 3587232 -->

**Uygulama sürümleri ayrıntıları** ayarı kapalıyken, uygulama ayrıntıları bölmesi, birleştirilagösterdiği uygulama sürümlerinin ve dillerin sayısını gösterir. Uygulama ayrıntılarına değişiklikler kaydederseniz, tüm sürümler için geçerlidir. Örneğin, **önem derecesini** veya **sahibini**ayarlayın. Bazı değerlerde "çoklu" görüntülenir, bu da tüm sürümlerde tutarlı bir değer olmadığı anlamına gelir.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp"> </a> Sistem ve Mağaza uygulamalarının otomatik yükseltme kararı

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

Bir dağıtım planında, **yükseltme kararlarını**da ayarlayabilirsiniz. Daha fazla bilgi için bkz. [varlıkları planlayın](about-deployment-plans.md#plan-assets).

### <a name="usage"></a>Kullanım

<!-- 5533890 -->

- **Toplam yükleme**sayısı: Bu değer, Seçilen uygulamanın tüm masaüstü Analizi kayıtlı cihazlarda yükleme sayısıdır.

- **Yüklemeyi yüzde**: Bu değer, Seçilen uygulamanın toplam masaüstü Analizi kayıtlı cihazlara karşı yüklemesi yüzdesidir.

- **Bu uygulamayı son 30 gün içinde Başlatan cihazlar**: Bu değer, bir kullanıcının seçili uygulamayı başlatıldığı cihazların sayısıdır. Yalnızca son 30 gün içinde kullanımı bildirilen cihazları içerir. Bu sayı, Windows 10 ' un herhangi bir sürümünde çalışan masaüstü analiziyle kaydedilen tüm cihazlarınızda bulunur. Bu sayı, bir dağıtım planı için değişebiliyor olabilir.

## <a name="next-steps"></a>Sonraki adımlar

- [Masaüstü Analizi dağıtım planları hakkında bilgi edinin](about-deployment-plans.md)  

- [Güvenlik ve özellik güncelleştirmeleri hakkında bilgi edinin](about-updates.md)  

- [Masaüstü Analizi 'nde uyumluluk değerlendirmesi](compat-assessment.md)  
