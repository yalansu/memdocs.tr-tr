---
title: Hizmet pencereleri
titleSuffix: Configuration Manager
description: Configuration Manager siteleri güncelleştirmeleri yüklerken denetlemek için hizmet pencerelerini kullanın.
ms.date: 01/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 669da2a04fe4e94b08fc426c32e0dbcc804a21d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719116"
---
#  <a name="service-windows-for-site-servers"></a>Site sunucuları için bakım pencereleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yönetim Merkezi siteleri ve birincil sitelerde hizmet pencerelerini, konsol içi güncelleştirmelerin ne zaman yükleneceğini denetlemek üzere yapılandırabilirsiniz.  Birden çok pencereyi, bu site sunucusu için tüm hizmet pencerelerinin bir birleşimiyle belirlenen güncelleştirmeleri yüklemeye izin verilen pencereyle birlikte yapılandırabilirsiniz.

Hizmet penceresi yapılandırılmadığında:
- **En üst katman sitenizde** (bir merkezi yönetim sitesi veya tek başına birincil site) güncelleştirme yüklemesinin ne zaman başlatılacağını seçin.
- **Alt birincil sitede**güncelleştirme, merkezi yönetim sitesinde güncelleştirme tamamlandıktan sonra otomatik olarak yüklenir.
- **İkincil bir sitede**güncelleştirmeler hiçbir şekilde otomatik olarak başlamaz. Bunun yerine, ana birincil site güncelleştirmeyi yükledikten sonra, güncelleştirme yüklemesini konsolunun içinden el ile başlatmanız gerekir.

Bir hizmet penceresi yapılandırıldığında:
- **En üst katman sitenizde**, Configuration Manager konsolundan herhangi bir yeni güncelleştirmenin yüklemesini başlatamacaksınız. Bir hizmet penceresi yapılandırılmış olsa bile, site yüklenmeye hazırlarsa güncelleştirmeleri otomatik olarak indirir.  
- Bir **alt birincil sitede**, bir merkezi yönetim sitesinde yüklü olan güncelleştirmeler birincil siteye indirilir, ancak otomatik olarak başlatılmaz. Bir hizmet penceresi kullanılarak engellenen bir süre boyunca güncelleştirme yüklemesini el ile başlatamazsınız. Hizmet pencerelerinin artık güncelleştirme yüklemesini engellememe sırasında, güncelleştirme yüklemesi otomatik olarak başlatılır.
- **İkincil siteler** , hizmet pencerelerini desteklemez ve güncelleştirmeleri otomatik olarak yüklemez. İkincil bir sitenin birincil üst sitesi bir güncelleştirme yükledikten sonra, İkincil sitenin güncelleştirmesini konsolunun içinden başlatabilirsiniz.

## <a name="to-configure-a-service-window"></a>Bir hizmet penceresi yapılandırmak için

1.  Configuration Manager konsolunda **Yönetim** > **sitesi yapılandırma** > **siteleri**' ni açın ve ardından bir hizmet penceresi yapılandırmak istediğiniz site sunucusunu seçin.  

2.  Daha sonra, site sunucuları **Özellikleri** ’ni düzenleyin ve **Bakım Süresi** sekmesini seçin. Bu sekmede, site sunucusu için bir veya daha fazla bakım süresi ayarlayabilirsiniz.  
