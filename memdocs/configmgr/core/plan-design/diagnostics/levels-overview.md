---
title: Tanılama kullanım verileri düzeyleri
titleSuffix: Configuration Manager
description: Configuration Manager topladığı tanılama ve kullanım verilerinin düzeyleri hakkında bilgi edinin
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0d27e4a2f82de75cde853f3ce95c98ea8a12c465
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126519"
---
# <a name="levels-of-diagnostic-usage-data"></a>Tanılama kullanım verileri düzeyleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager üç düzeyde tanılama ve kullanım verisi toplar: **temel**, **Gelişmiş**ve **tam**. Varsayılan olarak, bu özellik Gelişmiş düzeye ayarlanmıştır.

> [!IMPORTANT]
> Configuration Manager, temel veya gelişmiş düzeylerde site kodlarını, site adlarını, IP adreslerini, Kullanıcı adlarını, bilgisayar adlarını, fiziksel adresleri ya da e-posta adreslerini toplamaz. Bu bilgilerin tam düzeyinde toplanması herhangi bir amaca bağlı değildir. Büyük olasılıkla günlük dosyaları veya bellek anlık görüntüleri gibi gelişmiş tanılama bilgilerine dahil edilmiştir. Microsoft bu bilgileri sizi tanımlamak, sizinle iletişim kurmak veya reklam geliştirmek için kullanmaz.

## <a name="levels"></a>Düzeyler

### <a name="basic"></a>Temel

Temel düzey, hiyerarşiniz hakkındaki verileri içerir. Yüklemenizin veya yükseltme deneyiminizin iyileştirilmesine yardımcı olmak için gereklidir. Bu veriler, hiyerarşiniz için geçerli Configuration Manager güncelleştirmelerinin belirlenmesine de yardımcı olur.

### <a name="enhanced"></a>Gelişmiş

Gelişmiş düzey, Kurulum bittikten sonra varsayılandır. Bu düzey, temel düzeyde ve özelliğe özgü verilerde toplanan verileri içerir. Farklı özelliklerin sıklığını ve kullanım süresini gösterir. Ayrıca, Configuration Manager istemci ayarları verilerini içerir: bileşen adı, durumu ve yoklama aralıkları gibi belirli ayarlar. Yazılım güncelleştirmeleri hakkında bilgi, özellik kullanımı temel alınarak bu düzeyde güncelleştirme uyumluluğu hakkında veri içermez.

Microsoft, ürün ve hizmet iyileştirmeleri yapmak için en düşük verileri sağladığından bu düzeyi önerir.

Bu düzeyin toplamayacak bazı veri örnekleri şunlardır:

- Sitelerin, kullanıcıların, bilgisayarın veya diğer nesnelerin adları

- Güvenlikle ilgili nesnelerin ayrıntıları

- Yazılım güncelleştirmeleri gerektiren sistem sayısı gibi güvenlik açıkları

### <a name="full"></a>Tam

Tam düzey, temel ve gelişmiş düzeylerdeki tüm verileri içerir. Aynı zamanda Uç Nokta Koruma, güncelleştirme uyumluluğu yüzdeleri ve yazılım güncelleştirme bilgileri hakkında ek bilgiler de içerir. Bu düzey, sistem dosyaları ve bellek anlık görüntüleri gibi gelişmiş tanı bilgilerini de içerebilir. Bu gelişmiş veriler, yakalama sırasında bellekte veya günlük dosyalarında bulunan kişisel bilgileri içerebilir.

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Düzeyi değiştirme

Veri toplama düzeyini değiştirmek için, **site** nesnesi sınıfında **değiştirme** izinlerine sahip olmanız gerekir.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.
1. Şeritte **Hiyerarşi ayarları** ' nı seçin.
1. **Tanılama ve kullanım verileri** sekmesine geçin, sonra veri düzeyini seçin.

## <a name="version-specific-details"></a><a name="bkmk_versions"></a>Sürüme özgü ayrıntılar

Aşağıdaki makalelerde, desteklenen her sürümle Configuration Manager her düzeyde toplanan belirli veriler ayrıntılı olarak verilmiştir:

- [2006 için tanılama ve kullanım verileri](levels-of-diagnostic-usage-data-collection-2006.md)
- [2002 için tanılama ve kullanım verileri](levels-of-diagnostic-usage-data-collection-2002.md)
- [1910 için tanılama ve kullanım verileri](levels-of-diagnostic-usage-data-collection-1910.md)
- [1906 için tanılama ve kullanım verileri](levels-of-diagnostic-usage-data-collection-1906.md)
- [1902 için tanılama ve kullanım verileri](levels-of-diagnostic-usage-data-collection-1902.md)

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Sık sorulan sorular](frequently-asked-questions.md)
