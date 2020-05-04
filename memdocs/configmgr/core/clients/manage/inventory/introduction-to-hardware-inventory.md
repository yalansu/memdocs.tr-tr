---
title: 'Donanım envanteri '
titleSuffix: Configuration Manager
description: Configuration Manager 'da donanım envanterine giriş alın.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714412"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Configuration Manager donanım envanterine giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kuruluşunuzdaki istemci cihazların donanım yapılandırması hakkında bilgi toplamak için Configuration Manager 'de donanım envanterini kullanın. Donanım envanterini toplamak için istemci ayarlarındaki **istemcilerde donanım envanterini etkinleştir** ayarını seçmeniz gerekir.  

 Donanım envanteri etkinleştirildikten ve istemci bir donanım envanteri döngüsünü çalıştırdıktan sonra istemci, bilgileri istemcinin sitesindeki bir yönetim noktasına gönderir. Daha sonra yönetim noktası, envanter bilgilerini site veritabanında depolayan Configuration Manager site sunucusuna iletir. Donanım envanteri istemciler üzerinde, istemci ayarlarında belirttiğiniz zamanlamaya göre çalıştırılır.  
## <a name="view-hardware-inventory"></a>Donanım envanterini görüntüleme 

 Aşağıdaki yöntemler de dahil olmak üzere Configuration Manager tarafından toplanan donanım envanteri verilerini görüntülemek için çeşitli yöntemler kullanabilirsiniz:  

- [Belirli bir donanım yapılandırmasını temel alan cihazlar döndüren sorgular oluşturun](../../../../core/servers/manage/introduction-to-queries.md).  

- [Belirli bir donanım yapılandırmasını temel alan sorgu tabanlı Koleksiyonlar oluşturun](../../../../core/clients/manage/collections/introduction-to-collections.md). Sorgu tabanlı koleksiyon üyelikleri, bir zamanlamaya göre otomatik olarak güncelleştirilir. Koleksiyonları, yazılım dağıtımı dahil olmak üzere çeşitli görevler için kullanabilirsiniz.

- [Kuruluşunuzdaki donanım yapılandırmalarının belirli ayrıntılarını görüntüleyen raporlar çalıştırın](../../../servers/manage/introduction-to-reporting.md).

- İstemci cihazlardan toplanan donanım envanteri hakkında ayrıntılı bilgileri görüntülemek için [Kaynak Gezgini kullanın](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) .

Bir istemci cihaz üzerinde donanım envanteri çalıştırıldığında, istemci her zaman için ilk olarak tam envanter verileri döndürür. Sonraki envanter verileri yalnızca delta envanter bilgilerini içerir. Site sunucusu, delta envanter bilgilerini alınan sıraya göre işler. Bir istemci için değişim bilgileri eksikse, site sunucusu ek Delta bilgilerini reddeder ve istemciyi tam envanter döngüsünü çalıştırmaya yönlendirir.  

 Configuration Manager, Çift önyükleme bilgisayarları için sınırlı destek sağlar. Configuration Manager çift önyükleme bilgisayarlarını bulabilir, ancak yalnızca envanter çevrimi çalıştırıldığında etkin olan işletim sisteminden envanter bilgilerini döndürür.  

> [!NOTE]  
>  Linux ve UNIX çalıştıran istemcilerle donanım envanterini kullanma hakkında bilgi için bkz. [Linux ve UNIX Için donanım envanteri](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Configuration Manager donanım envanterini genişletme  
 Configuration Manager içindeki yerleşik donanım envanterine ek olarak, daha fazla bilgi toplamak üzere donanım envanterini genişletmek için aşağıdaki yöntemlerden birini de kullanabilirsiniz:  

- Configuration Manager konsolundan donanım envanteri için envanter sınıflarını etkinleştirin, devre dışı bırakın, ekleyin ve kaldırın.  
- Configuration Manager tarafından envantere alınmayan istemci cihazları hakkında bilgi toplamak için NOıDMıF dosyalarını kullanın. Örneğin, yalnızca cihaz üzerindeki bir etikette bulunan cihaz varlık numarası bilgilerini toplamak isteyebilirsiniz. NOIDMIF envanteri, toplandığı istemci cihaz ile otomatik olarak ilişkilendirilir.  
- Bir Configuration Manager istemcisiyle ilişkili olmayan varlıklar (projektörler, fotokopi makineleri ve ağ yazıcıları gibi) hakkında bilgi toplamak için ıDMıF dosyalarını kullanın.


## <a name="next-steps"></a>Sonraki adımlar
Configuration Manager donanım envanterini genişletmek için bu yöntemleri kullanma hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
