---
title: Tanılama verilerinin kullanımı
titleSuffix: Configuration Manager
description: Microsoft 'un Configuration Manager topladığı tanılama ve kullanım verilerini nasıl kullandığını öğrenin.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715616"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Microsoft 'un tanılama ve kullanım verilerini Configuration Manager kullanımı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager topladığı tanılama ve kullanım verileri, Microsoft 'un ürünün nasıl çalıştığı ve gelecekteki güncelleştirmeleri ayarlamak için nasıl kullanıldığı hakkında neredeyse anında geri bildirim sağlar. Microsoft ayrıca, üretimde kullandığınız yapılandırmaların mühendisine ve test etmesine yardımcı olan yapılandırma verilerini de görebilir. Örneğin:

- Site sunucularında kullanılan Windows Server sürümleri

- Yüklü dil paketleri

- Ürün varsayılanına göre SQL şeması değişimi

Bu veriler, en yaygın yapılandırmaların en iyi deneyiminden emin olmak için mühendislik ekibinin gelecekteki testleri planına yardımcı olur. Bu veriler, sık sık bir yayın döngüsünü hızla ayarlamak ve uyum sağlamak için önemlidir.

Tanılama ve kullanım verilerinin kullanılma biçimi de aynı şekilde önemlidir. Microsoft bu verileri için kullanmaz:

- Lisans denetimleri; örneğin, müşteri kullanımını lisans sözleşmeleriyle karşılaştırma

- Desteklenmeyen ürünlerin denetlenmesi

- Özellik kullanımı veya coğrafi konum (saat dilimi) gibi kullanılabilir verileri temel alan reklam

Microsoft, ürünü geliştirmek için kullanılabilir verileri kullanır. Örneğin:

- Geçerli dalı tarafından sunulan ilk destek, Windows Server 2008 R2 için destek zaman çizelgesine sınırlı Configuration Manager. Microsoft, Configuration Manager geçerli dalına yükselten müşterilerin kullanım verilerini inceledi. Daha sonra bu işletim sistemini kullanmaya devam eden müşterileri desteklemek için bu zaman çizelgesini düzeltme ve genişletme gereksinimini tanımlamıştır.

- Microsoft, bir güncelleştirmeyi yüklemek için önkoşul denetimlerini geliştirmiştir. Artık kullanılmayan kuralları kaldırırlar, ek durumlar için hesaba katılmaz ve bazı sorunlar otomatik olarak düzeltildi.  

> [!div class="nextstepaction"]
> [Configuration Manager’ın veri toplama şekli](how-diagnostics-and-usage-data-is-collected.md)
