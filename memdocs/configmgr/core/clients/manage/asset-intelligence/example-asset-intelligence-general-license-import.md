---
title: Varlık Yönetim Bilgileri genel lisans içeri aktarma dosyası örneği
titleSuffix: Configuration Manager
description: Yazılım lisanslarını Configuration Manager içeri aktarmaya yardımcı olması için bir örnek Varlık Yönetim Bilgileri genel lisans dosyası kullanın.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e6258333-a783-440b-b1af-f8023b782fbc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 542a0e324056dfedbc1b84d75f1204f2488750c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713943"
---
# <a name="example-asset-intelligence-general-license-import-file-in-configuration-manager"></a>Configuration Manager Varlık Yönetim Bilgileri genel lisans içeri aktarma dosyası örneği

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konudaki örnek bilgiler, Yazılım Lisansını İçeri Aktarma Sihirbazı’nı kullanarak Varlık Yönetim Bilgileri kataloğuna yazılım lisanslarını aktarmak için örnek bir genel yazılım lisans dosyası oluşturmak üzere kullanılabilir. Aşağıdaki tabloyu yeni bir Microsoft Excel elektronik tablosuna kopyalayıp yapıştırabilir ve test amacıyla örnek bir genel yazılım lisans içeri aktarma dosyası olarak kullanılmak üzere .csv dosya adı uzantısıyla kaydedebilirsiniz. Lisans içeri aktarma dosyası oluştururken, elektronik tabloda yalnızca Ad, Yayımcı, Sürüm ve EffectiveQuantity veri değerleri gerekliyken tüm üst bilgi alanları zorunludur. Yazılım lisanslarını Varlık Yönetim Bilgileri kataloğuna aktarma hakkında daha fazla bilgi için bkz. [varlık yönetim bilgileri yapılandırma](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

|Adı|Yayımcı|Sürüm|Dil|EffectiveQuantity|PONumber|ResellerName|DateOfPurchase|SupportPurchased|SupportExpirationDate|Açıklamalar|  
|----------|---------------|-------------|--------------|-----------------------|--------------|------------------|--------------------|----------------------|---------------------------|--------------|  
|Yazılım Başlığı 1|Yazılım yayımcısı|1.01|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 2|Yazılım yayımcısı|1.02|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 3|Yazılım yayımcısı|1.03|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 4|Yazılım yayımcısı|1.04|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 5|Yazılım yayımcısı|1.05|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 6|Yazılım yayımcısı|1.06|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 7|Yazılım yayımcısı|1.07|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 8|Yazılım yayımcısı|1.08|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 9|Yazılım yayımcısı|1.09|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
|Yazılım başlığı 10|Yazılım yayımcısı|1.10|İngilizce|1|Satın alma numarası|Satıcı adı|10/10/2010|0|10/10/2012|Açıklama|  
