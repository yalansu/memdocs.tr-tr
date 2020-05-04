---
title: Kaynak Gezgini kullanma
titleSuffix: Configuration Manager
description: Configuration Manager ' de donanım envanterini görüntülemek için Kaynak Gezgini kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710681"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Configuration Manager ' de donanım envanterini görüntülemek için Kaynak Gezgini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Donanım envanteri hakkındaki bilgileri görüntülemek için Configuration Manager Kaynak Gezgini kullanın. Site bu bilgileri hiyerarşinizdeki istemcilerden toplar.  

> [!Tip]  
>  Kaynak Gezgini, bağlandığınız istemcide donanım envanteri çevrimi çalıştırana kadar herhangi bir veri görüntülemez.  



## <a name="overview"></a>Genel Bakış

Kaynak Gezgini, donanım envanteriyle ilgili aşağıdaki bölümlere sahiptir:  

- **Donanım**: belirtilen istemci cihazından toplanan en son donanım envanterini gösterir.  

    - **Iş Istasyonu durumu** düğümü, cihazdaki son donanım envanterinin saat ve tarihini gösterir.  

- **Donanım geçmişi**: son donanım envanteri döngüsünden bu yana değiştirilen envantere kaydedilmiş öğelerin geçmişi.  

    - **Geçerli** bir düğümü ve geçmiş tarihi olan bir veya daha fazla düğümü görmek için bir öğeyi genişletin. Geçerli düğümdeki bilgileri, değiştirilen öğeleri görmek için geçmiş düğümlerinden biriyle karşılaştırın.  

> [!NOTE]  
> Varsayılan olarak, Configuration Manager 90 gün boyunca etkin olmayan donanım envanteri verilerini siler. **Eski envanter geçmişini sil** site bakım görevinde bu gün sayısını ayarlayın. Daha fazla bilgi için bkz. [bakım görevleri](../../../servers/manage/maintenance-tasks.md).  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a>Kaynak Gezgini açma   

1.  Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. **Cihaz Koleksiyonları** düğümünde herhangi bir koleksiyonu da seçebilirsiniz.  

2.  Cihaz seçin. Şeritte, **giriş** sekmesinde ve **cihazlar** grubunda, **Başlat**' a tıklayın ve ardından **Kaynak Gezgini**' yi seçin.   

> [!Tip]  
> Kaynak Gezgini, ek eylemler için sağ Sonuçlar bölmesindeki bir öğeye sağ tıklayın. Bu öğeyi farklı bir biçimde görüntülemek için **Özellikler** ' e tıklayın.  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a>Büyük tamsayı değerlerinin kullanımı
<!--1357880-->
1802 ve daha önceki sürümleri Configuration Manager, donanım envanterinin 4.294.967.296 ' den büyük tamsayılar sınırı vardır (2 ^ 32). Bu sınıra, sabit sürücü boyutları gibi öznitelikler için bayt cinsinden ulaşılabilir. Yönetim noktası bu sınırın üzerindeki tamsayı değerlerini işlemez, bu nedenle veritabanında hiçbir değer depolanmaz. 

Sürüm 1806 ' den başlayarak, sınır 18446744073709551616 artar (2 ^ 64). 

Toplam disk boyutu gibi değişmeyen bir değer içeren bir özellik için, siteyi yükselttikten sonra değeri hemen görmeyebilirsiniz. Çoğu donanım envanteri bir Delta rapordur. İstemci yalnızca değişen değerleri gönderir. Bu davranışı geçici olarak çözmek için, aynı sınıfa başka bir özelliği ekleyin. Bu eylem, istemcinin değiştirilen sınıftaki tüm özellikleri güncelleştirmesine neden olur. 



## <a name="see-also"></a>Ayrıca bkz.

Linux ve UNIX çalıştıran istemcilerden donanım envanterini görüntüleme hakkında daha fazla bilgi için bkz. [Linux ve UNIX sunucuları için istemcileri izleme](../monitor-clients-for-linux-and-unix-servers.md).  

Kaynak Gezgini Ayrıca yazılım envanterini gösterir. Daha fazla bilgi için bkz. [yazılım envanterini görüntülemek için kaynak Gezgini kullanma](use-resource-explorer-to-view-software-inventory.md).
