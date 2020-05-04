---
title: En iyi koleksiyonlar uygulamaları
titleSuffix: Configuration Manager
description: Configuration Manager içindeki koleksiyonlar için en iyi yöntemleri alın.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714293"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Configuration Manager içindeki koleksiyonlar için en iyi yöntemler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager içindeki koleksiyonlar için aşağıdaki en iyi yöntemleri kullanın.  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a>Birçok koleksiyon ile artımlı güncelleştirme kullanmayın

**Bu koleksiyon için artımlı güncelleştirme kullan** seçeneğini etkinleştirdiğinizde bu yapılandırma, seçeneği birçok koleksiyon için etkinleştirdiğinizde değerlendirme gecikmelerine neden olabilir. Eşik, hiyerarşinizdeki yaklaşık 200 koleksiyon kadardır. Tam sayı aşağıdaki etkenlere bağlıdır:  

- Toplam koleksiyon sayısı  

- Hiyerarşiye yeni kaynak eklenme ve kaynakların değiştirilme sıklığı  

- Hiyerarşinizdeki istemci sayısı  

- Hiyerarşinizdeki koleksiyon üyeliği kurallarının karmaşıklığı  

## <a name="maintenance-window-size-for-software-updates"></a>Yazılım güncelleştirmeleri için bakım penceresi boyutu

Cihaz Koleksiyonları için bakım pencerelerini, Configuration Manager bu cihazlara yazılım yükleyebileceği zamanları kısıtlamak üzere yapılandırabilirsiniz. Bakım penceresini çok küçük olacak şekilde yapılandırırsanız, istemci kritik yazılım güncelleştirmelerini yükleyemeyebilir, bu da istemciyi yazılım güncelleştirmesi tarafından azaltılan saldırılara karşı savunmasız bırakır.

> [!Tip]
> Bakım pencerelerini planlarken göz önünde bulundurmanız gereken önemli noktalar:
>
> - Varsayılan yazılım güncelleştirmesi en fazla çalışma süresi 60 dakikadır.
> - Configuration Manager bir güncelleştirmenin yüklenip yüklenmediğini hesapladığında, yeniden başlatma için en fazla çalışma zamanına beş dakika ekler.
> - Bakım penceresinin kalan süresi, yazılım güncelleştirmesinin en uzun çalışma zamanından ve beş dakikadan uzun olmalıdır.
