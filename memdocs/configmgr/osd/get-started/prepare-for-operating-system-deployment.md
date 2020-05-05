---
title: İşletim sistemi dağıtımına hazırlanma
titleSuffix: Configuration Manager
description: Configuration Manager işletim sistemi dağıtımlarını hazırlama hakkında bilgi edinin
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724086"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Configuration Manager işletim sistemi dağıtımı için hazırlanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İşletim sistemlerini dağıtabilmeniz için Configuration Manager birkaç şey yapmanız gerekir. İşletim sistemi dağıtımına hazırlanmak için aşağıdaki makaleleri kullanın:  

-   [Önyükleme görüntülerini yönetme](manage-boot-images.md)  

-   [İşletim sistemi görüntülerini yönetme](manage-operating-system-images.md)  

-   [İşletim sistemi yükseltme paketlerini yönetme](manage-operating-system-upgrade-packages.md)  

-   [Sürücüleri yönetme](manage-drivers.md)  

-   [Kullanıcı durumunu yönetme](manage-user-state.md)  

-   [Bilinmeyen bilgisayar dağıtımlarına hazırlanma](prepare-for-unknown-computer-deployments.md)  

-   [Kullanıcıları bir hedef bilgisayarla ilişkilendirme](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>İşletim sistemi görüntü boyutu  

İşletim sistemi görüntülerinin boyutu büyük. Örneğin, Windows 7 için görüntü boyutu 3 GB veya daha fazla. Görüntü boyutu ve işletim sistemini aynı anda dağıttığınız bilgisayarların sayısı ağ performansını ve kullanılabilir bant genişliğini etkiler. Ağ performansını test ettiğinizden emin olun. Etkiyi test etmek, görüntü dağıtımının sahip olabileceği etkiyi ve dağıtımın tamamlanma süresini daha iyi ölçerler. Ağ performansını etkileyen Configuration Manager etkinlikler, görüntüyü bir dağıtım noktasına dağıtmayı, görüntüyü bir siteden diğerine dağıtmayı ve görüntünün istemciye indirilmesini içerir.  

Ayrıca, işletim sistemi görüntülerini barındıran dağıtım noktalarında yeterli disk depolama alanı planladığınızdan emin olun.  

Daha fazla bilgi için bkz. [dağıtım noktaları Için ek planlama değerlendirmeleri](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>İstemci önbellek boyutu  

Configuration Manager istemcileri içeriği indirdiklerinde, varsa otomatik olarak Arka Plan Akıllı Aktarım Hizmeti (BITS) kullanır. İşletim sistemini yükleyen bir görev dizisi dağıttığınızda, dağıtım üzerinde bir seçenek belirleyebilirsiniz. böylece, Configuration Manager istemcileri, görev sırası çalıştırılmadan önce tam görüntüyü yerel bir önbelleğe indirir.  

Bir Configuration Manager istemci bir işletim sistemi görüntüsünü indirmeli, ancak önbellekte yeterli alan kalmadığında, istemci önbelleğinde alanı temizleyebilir. En eski paketleri silmenin, görüntüye uyum sağlamak için yeterli disk alanına sahip olup olmadığını anlamak için önbellekteki diğer paketleri kontrol eder. Paketlerin silinmesi yeterli alan boşaltmazsa, istemci görüntüyü indirmez ve dağıtım başarısız olur. Bu davranış, önbelleğin önbellekte kalıcı olacak şekilde yapılandırdığınız büyük bir paketi varsa meydana gelebilir. Paketlerin silinmesi önbellekte yeterli boş disk alanı açıyorsa istemci onları siler ve sonra görüntüyü önbelleğe indirir.  

Configuration Manager istemcilerindeki varsayılan önbellek boyutu çoğu işletim sistemi görüntüsü dağıtımı için yeterince büyük olmayabilir. İstemci önbelleğine tam görüntüyü indirmeyi planlıyorsanız, hedef bilgisayarlardaki istemci önbelleği boyutunu dağıttığınız görüntünün boyutuna uyacak şekilde ayarlayın.  

Daha fazla bilgi için bkz. [istemci önbelleğini yapılandırma](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  


