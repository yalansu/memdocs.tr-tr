---
title: Görünüm ve doğru kişisel veriler
titleSuffix: Microsoft Intune
description: Kişisel verileri görüntülemeyi ve düzeltmeyi öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6cddd94400874c508a31b11b22fa4417798e2da
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084769"
---
# <a name="view-and-correct-personal-data"></a>Görünüm ve doğru kişisel veriler

Intune yöneticileri, erişim izinlerine bağlı olarak bazı kişisel verileri görüntüleyebilir ancak yalnızca son kullanıcılar kendi cihazlarındaki kişisel verileri değiştirebilir.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>Kişisel verileri görüntüleme

Yöneticiler, Intune kullanıcı arabirimindeki çeşitli dikey pencerelerde son kullanıcı kişisel bilgilerini görebilir. Aşağıdaki makalelerde, yöneticilerin hangi bilgileri yaptığını ve erişimi yok açıklanmaktadır:
- Intune 'da [cihaz ayrıntılarına bakın](../remote-actions/device-inventory.md) son kullanıcının cihazına ilişkin ayrıntıları nasıl gözden geçirebileceğinizi açıklar.
- [Uygulama bilgilerini ve atamalarını izleme,](../apps/apps-monitor.md) son kullanıcının cihazında yüklü olan uygulamalarla ilgili ayrıntıları nasıl görebileceğinizi açıklar.
- [Cihazımı kaydettiğimde şirketim hangi bilgileri görebilir? makalesi](https://docs.microsoft.com/mem/intune/user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) , son kullanıcılara, şirketlerinin görebileceği ve görebilecekleri verilerin bir listesini sağlar. Kullanıcılarınıza ne tür verileri topladığınızı ve neden topladığınızı açıkça söylemek en iyisidir. Bu şeffaflığın sağlanması için bu makale ilk adımınız olabilir.

### <a name="who-can-view-the-data"></a>Verileri kim görebilir?

Microsoft, müşteri verilerine erişimi yönetmek için katı denetimler kullanır; önemli görevleri tamamlamaya yetecek en düşük erişim düzeyini verip ihtiyaç kalmadığında erişimi iptal eder. 

Rol tabanlı yönetim denetimini (RBAC) kullanarak son kullanıcının kişisel verilerine erişimi güvenlik altına alabilir ve denetleyebilirsiniz. Daha fazla bilgi için bkz. [Microsoft Intune ile RBAC](../fundamentals/role-based-access-control.md).

Online Services Hükümleri ve [Microsoft Online Services Gizlilik Bildirimi](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409)’ni okuyarak Microsoft veri uygulamaları hakkında daha fazla bilgi edinebilirsiniz. 

## <a name="correct-end-user-personal-data"></a>Son kullanıcı kişisel bilgilerini düzeltme

Yöneticiler cihaz veya uygulamaya özgü bilgileri güncelleştiremez. Bir son kullanıcı herhangi bir kişisel veriyi düzeltmek istiyorsa (örneğin cihaz adı), bunu doğrudan kendi cihazında yapmalıdır. Bu tür değişiklikler, kullanıcı Intune’a bağlandığı zaman eşitlenir.


## <a name="next-steps"></a>Sonraki adımlar

Intune’da kişisel verileri [denetleme, dışarı aktarma ve silme](privacy-data-audit-export-delete.md) hakkında bilgi edinin.
