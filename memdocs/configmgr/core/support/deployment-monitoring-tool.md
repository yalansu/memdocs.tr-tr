---
title: Dağıtım İzleme Aracı
titleSuffix: Configuration Manager
description: Configuration Manager istemcisinde yazılım dağıtımlarının sorunlarını gidermek için dağıtım Izleme aracını kullanın.
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723379"
---
# <a name="deployment-monitoring-tool"></a>Dağıtım İzleme Aracı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Dağıtım Izleme aracı [Configuration Manager araçlarından](tools.md)biridir. Bu, Configuration Manager istemcisinde uygulama, yazılım güncelleştirmesi ve yapılandırma temeli dağıtımlarıyla ilgili sorunları gidermeye yardımcı olmak için tasarlanmış bir grafik kullanıcı arabirimidir. Araç, istemcide herhangi bir durumu değiştirmediğinden salt okunurdur. Bu uygulamayı, yaygın dağıtım senaryolarını tanılamak için güvenle kullanabilirsiniz.


## <a name="features"></a>Özellikler

- Yerel istemcideki dağıtımlarla ilgili sorunları gidermek için bunu yönetici olarak çalıştırın.  

- Uzak istemcideki dağıtımlarla ilgili sorunları giderin. Aracı başlatın ve bir uzak makineye yönetici olarak bağlanın.  

- Araçta toplanan tüm verileri XML 'e aktarın. XML dosyasını başkalarıyla paylaşıp, sorun giderme dağıtımları hakkında konuşmak için ortak bir platform olarak kullanın.  

- Daha önce dışarı aktarılan verileri farklı bir makineye aktarın ve aracı çevrimdışı modda çalıştırmak için kullanın.   


## <a name="usage"></a>Kullanım

Dağıtım Izleme aracı yalnızca grafik kullanıcı arabirimini destekler. Aracı başlatmak için, bir yönetici olarak **Deploymentmonitoringtool. exe** ' yi çalıştırın. Üç görünüm vardır:  

- **Istemci özellikleri**: cihaz ve Configuration Manager istemcisiyle ilgili yararlı özniteliklerin bir listesi. Bu görünüm varsayılandır.   

- **Dağıtımlar**: Şu anda hedeflenen dağıtımları görüntüleyin. Ayrıntılar bölmesinde daha fazla bilgi görüntülemek için sonuçlar bölmesinde bir dağıtım seçin.  

- **Tüm güncelleştirmeler**: tüm yazılım güncelleştirmelerini ve bunların durumlarını görüntüleyin.  

Verileri herhangi bir görünümde kopyalamak için bir hücre seçin ve **CTRL** + **C**tuşuna basın.


### <a name="actions-menu"></a>Eylemler menüsü

**Eylemler** menüsünde aşağıdaki eylemler kullanılabilir:  

- **Uzak makineye bağlan**: bağlanılacak bir bilgisayar seçin. Bir Kullanıcı adı ve parola belirtmezseniz, geçerli kimlik bilgilerini kullanır. Uzak bilgisayara bağlanmak için **Kaydet** ' e tıklayın.  

- **Verileri dışarı aktar**: Verilerin yazılacağı dosyayı seçin ve **Kaydet**' e tıklayın. Farklı bir bilgisayarda uzaktan sorun giderme için, aktarılmış XML dosyasını kullanın.  

- **Verileri Içeri aktar**: araca aktarmak için bir dosya seçin.  

- **Günlüğü görüntüle**: görünüme bağlı olarak ilişkili bir günlük dosyasını açar:  
    - İstemci özellikleri:`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Dağıtımlar`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Tüm güncelleştirmeler:`C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Ayrıca bkz.

- [Uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md)
- [Yazılım güncelleştirmelerini dağıtma](../../sum/deploy-use/deploy-software-updates.md)
- [Yapılandırma taban çizgilerini dağıtma](../../compliance/deploy-use/deploy-configuration-baselines.md)
