---
title: Koleksiyonlar önkoşulları
titleSuffix: Configuration Manager
description: Configuration Manager içinde koleksiyonları kullanmaya yönelik önkoşulları alın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714503"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Configuration Manager içindeki koleksiyonlar için Önkoşullar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager koleksiyonlar yalnızca ürün içinde bağımlılıklar içerir.  

## <a name="configuration-manager-dependencies"></a>Configuration Manager bağımlılıkları  

|Bağımlılık|Daha fazla bilgi|  
|----------------|----------------------|  
|Raporlama hizmetleri noktası|Koleksiyonlar için raporları çalıştırmadan önce raporlama hizmetleri noktası site sistemi rolünün yüklenmesi gerekir. Daha fazla bilgi için bkz. [raporlamaya giriş](../../../servers/manage/introduction-to-reporting.md).|  
|Koleksiyonları yönetmek için belirli güvenlik izinleri verilmiş olması gerekir.|Uyumluluk ayarlarını yönetmek için aşağıdaki güvenlik izinlerine sahip olmanız gerekir:<br /><br /> -Koleksiyonlar oluşturmak ve yönetmek için: **koleksiyon** nesnesi için **Oluştur**, **Sil**, **Değiştir**, **klasörü Değiştir**, **nesne taşı**, **Oku** ve **kaynağı oku** .<br /><br /> -Koleksiyon ayarlarını yönetmek için: **koleksiyon nesnesi Için** **koleksiyon ayarını değiştirin** .<br /><br /> **Klasörü Değiştir** izni, kök klasörü dahil olmak üzere tüm koleksiyon klasörleri için gereklidir.|  
