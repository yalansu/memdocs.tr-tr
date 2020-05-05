---
title: İçerik Sahipliği Aracı
titleSuffix: Configuration Manager
description: Configuration Manager ' deki yalnız bırakılmış paketlerin sahipliğini değiştirmek için Içerik sahipliği aracını kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723393"
---
# <a name="content-ownership-tool"></a>İçerik Sahipliği Aracı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İçerik sahipliği aracı [Configuration Manager araçlarından](tools.md)biridir. Configuration Manager yalnız bırakılmış paketlerin sahipliğini değiştirir. Yalnız bırakılmış paketlerde sahip bir site sunucusu yok. Paketler, site sunucusu hala bu site sunucusuna ait olduğu sırada kaldırılarak, sahipsiz hale gelebilir.

Configuration Manager hiyerarşisindeki herhangi bir site sunucusunda Içerik sahipliği aracını çalıştırın. Yeterli paket izinlerine sahip bir yönetici kullanıcı olarak oturum açın.  

> [!Tip]  
> Bir dağıtım noktasından yalnız bırakılmış içeriği *kaldırmak* Için Içinde **contentlibrarycleanup. exe** ' `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` yi kullanın. Daha fazla bilgi için bkz. [içerik kitaplığı Temizleme Aracı](../plan-design/hierarchy/content-library-cleanup-tool.md).  



## <a name="features"></a>Özellikler

- Yalnız bırakılmış tüm paketleri görüntüle  

- Yalnız bırakılmış olmasalar bile tüm paketleri görüntüle  

- Bir site bağlantısının durumunu görüntüleme  

- Paketleri ada, site koduna veya paket türüne göre filtrele  

- Görünen sütunlara göre sırala  

- Tek bir eylemle bir veya daha fazla paketin atamasını değiştirme  

- Sahiplik aktarma etkinliğinin ilerlemesini görüntüleme  



## <a name="usage"></a>Kullanım

Aracı başlatmak için **Contenentownershiptool. exe dosyasını** çalıştırın. Bilgisayarda yerel yönetici izinleri, aracı çalıştırmak için gerekli değildir.

Komut satırı parametresi yok.

> [!Important]   
> Bu araç, yalnız bırakılmış paketin sahipliğini değiştirir. Paketin kendisi üzerinde depolandığı dağıtım noktasından geçiş yapmaz. Bu sahiplik değişikliği paketin dağıtım noktalarında güncelleştirilmesine neden olmaz. Ayrıca, istemcilerin paketin dağıtımı için ilkeyi yeniden değerlendirmesine neden olmaz. Sahiplik değiştirildikten sonra, yeni site sunucusunun kaynak dosyalara erişe, emin olun. Her paketin kaynak dosyaları için en azından **okuma** izinlerine sahip olmalıdır. 



## <a name="see-also"></a>Ayrıca bkz.

- [İçerik yönetimi için temel kavramlar](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [İçerik kitaplığı](../plan-design/hierarchy/the-content-library.md)
