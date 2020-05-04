---
title: Yazılım envanteri
titleSuffix: Configuration Manager
description: Configuration Manager ' de yazılım envanterine giriş alın.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714398"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Configuration Manager yazılım envanterine giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İstemci cihazlarındaki dosyalar hakkında bilgi toplamak için yazılım envanterini kullanın. Yazılım envanteri Ayrıca, istemci aygıtlarından dosya toplayabilir ve bunları site sunucusunda saklayabilir. Yazılım envanteri, istemci ayarlarındaki **istemcilerde yazılım envanterini etkinleştir** ayarını seçtiğinizde toplanır. İşlemi istemci ayarları ' nda da zamanlayabilirsiniz.  

Yazılım envanterini etkinleştirdikten ve istemciler bir yazılım envanteri döngüsünü çalıştırdıktan sonra istemci, bilgileri istemcinin sitesindeki bir yönetim noktasına gönderir. Yönetim noktası daha sonra envanter bilgilerini, bilgileri site veritabanında depolayan Configuration Manager site sunucusuna iletir.

 Yazılım envanteri verilerini görüntülemenin birkaç yolu vardır:  

- Belirtilen dosyalarla cihazları döndüren [sorgular oluşturun](../../../../core/servers/manage/create-queries.md) .   

- Belirtilen dosyaları içeren cihazları içeren [sorgu tabanlı koleksiyonlar](../../../../core/clients/manage/collections/introduction-to-collections.md) oluşturun.   

- Cihazlarda dosyalarla ilgili ayrıntıları sağlayan [raporları çalıştırın](../../../servers/manage/introduction-to-reporting.md) .

- İstemci cihazlardan envantere alınan ve toplanan dosyalar hakkındaki ayrıntılı bilgileri incelemek için [Kaynak Gezgini](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) kullanın.   

 Yazılım envanteri bir istemci cihazda çalıştırıldığında, ilk rapor tam envanterdir. Sonraki raporlar yalnızca delta envanter bilgilerini içerir. Site sunucusu, Delta bilgilerini alındı sırasına göre işler. Bir istemci için değişim bilgileri eksikse, site sunucusu diğer Delta bilgilerini reddeder ve istemciyi tam envanter çalıştıracak şekilde yönlendirir.  

 Configuration Manager çift önyükleme bilgisayarlarını bulabilir, ancak yalnızca envanter sırasında etkin olan işletim sisteminden envanter bilgilerini döndürür.  
