---
title: VDI istemcilerini yönetme
titleSuffix: Configuration Manager
description: Bir sanal masaüstü altyapısında (VDı) Configuration Manager istemcilerini yönetin.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01348695ac5b3b64ca87a9b42aa52ac235b533d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713327"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Bir sanal masaüstü altyapısında (VDı) Configuration Manager istemcilerini yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, aşağıdaki sanal masaüstü altyapısı (VDı) senaryolarında Configuration Manager istemcisinin yüklenmesini destekler:  

- **Kişisel sanal makineler** -kişisel sanal makineler genellikle kullanıcı verilerinin ve ayarlarının oturumlar arasındaki sanal makinede korunduğundan emin olmak istediğinizde kullanılır.  

- **Uzak Masaüstü Hizmetleri oturumlar** -Uzak Masaüstü Hizmetleri, bir sunucunun birden çok, eşzamanlı istemci oturumunu barındırmalarını sağlar. Kullanıcılar bir oturuma bağlanabilir ve ardından bu sunucuda uygulamaları çalıştırabilir.  

- **Havuza alınmış sanal makineler** -havuza alınmış sanal makineler, oturumlar arasında kalıcı olmaz. Bir oturum kapatıldığında tüm veriler ve ayarlar atılır. Havuza alınmış sanal makineler, gerekli bir iş uygulaması istemci oturumlarını barındıran Windows Server 'da çalışmadığından Uzak Masaüstü Hizmetleri kullanılamaz olduğunda faydalıdır.  

  Aşağıdaki tabloda, bir sanal masaüstü altyapısında Configuration Manager istemcisinin yönetimiyle ilgili konular listelenmektedir.  

|Sanal makine türü|Dikkat edilmesi gerekenler|  
|--------------------------|--------------------|  
|Kişisel sanal makineler|Configuration Manager, kişisel sanal makinelere fiziksel bir bilgisayarla aynı şekilde davranır. Configuration Manager istemcisi sanal makine görüntüsüne önceden yüklenebilir veya sanal makine sağlandıktan sonra dağıtılabilir.|  
|Uzak Masaüstü Hizmetleri|Configuration Manager istemcisi bağımsız uzak masaüstü oturumları için yüklü değil. Bunun yerine, istemci Uzak Masaüstü Hizmetleri sunucuda yalnızca bir kez yüklenir. Tüm Configuration Manager Özellikler Uzak Masaüstü Hizmetleri sunucusunda kullanılabilir.|  
|Havuza alınmış sanal makineler|Havuza alınmış bir sanal makine kullanımdan çalıştırıldığında, Configuration Manager kullanarak yaptığınız tüm değişiklikler kaybedilir.<br /><br /> Donanım envanteri, yazılım envanteri ve yazılım kullanım ölçümü gibi Configuration Manager özelliklerden döndürülen veriler, sanal makine yalnızca kısa bir süre boyunca çalışır durumda olabileceğinden gereksinimlerinize uygun olmayabilir. Havuza alınmış sanal makineleri envanter görevlerinden dışlayarak göz önünde bulundurun.|  

 Sanallaştırma, aynı fiziksel bilgisayarda birden çok Configuration Manager istemcisini çalıştırmayı desteklediğinden, çok sayıda istemci işlemi donanım ve yazılım envanteri, kötü amaçlı yazılımdan taramalar, yazılım yüklemeleri ve yazılım güncelleştirme taramaları gibi zamanlanmış eylemler için yerleşik rastgele gecikmeye sahiptir. Bu gecikme, Configuration Manager istemcisini çalıştıran birden çok sanal makineye sahip bir bilgisayar için CPU işleme ve veri aktarımını dağıtmaya yardımcı olur.  

> [!NOTE]  
>  Bakım modundaki Windows Embedded istemcileri dışında, sanallaştırılmış ortamlarda çalıştırmayan Configuration Manager istemcileri bu rastgele gecikmeyi de kullanır. Birden çok dağıtılan istemciniz olduğunda, bu davranış ağ bant genişliğinden en üst düzeye kaçınmanıza yardımcı olur ve yönetim noktası ve site sunucusu gibi Configuration Manager site sistemlerinde CPU işlem gereksinimini azaltır. Gecikme aralığı Configuration Manager özelliğine göre farklılık gösterir.  
>   
>  Aşağıdaki istemci ayarı kullanılarak gerekli yazılım güncelleştirmeleri için varsayılan olarak rastgele gecikme devre dışı bırakılır: **Bilgisayar Aracısı**: **rastgele son tarih seçimini devre dışı bırak**.
