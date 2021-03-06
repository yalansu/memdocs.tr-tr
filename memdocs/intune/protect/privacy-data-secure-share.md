---
title: Intune’da veri güvenliği ve paylaşımı
titleSuffix: Microsoft Intune
description: Intune’da kişisel verilerin nasıl güvenlik altına alınıp paylaşıldığını öğrenin.
keywords: Gizlilik, veriler
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 68921fd6-5f50-456c-a3af-83d7bc4b134b
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34e99a53165afdccd5ee9a2f3f190c78f673a507
ms.sourcegitcommit: 15450a1e92d9f67f74ae619ffe192c15948107c5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516265"
---
# <a name="data-security-and-sharing-in-intune"></a>Intune’da veri güvenliği ve paylaşımı


## <a name="data-security"></a>Veri güvenliği

Microsoft Intune, Microsoft Enterprise Mobility ve Security Suite bulut hizmeti teklifinin önemli bir bileşenidir. [Veri yönetimi stratejisini](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) desteklemek için tüm Microsoft bulut hizmetleri [Microsoft Gizliliği](https://www.microsoft.com/en-us/trustcenter/privacy) ve [Microsoft Güvenliği](https://www.microsoft.com/en-us/trustcenter/security/) metodolojileri ile geliştirilmiştir.  

Microsoft Intune, Microsoft Azure hizmet ekiplerinin veri güvenliği ihlali işlemlerine karşı güvenliği sağlamak için aldığı teknik ve organizasyonel önlemleri alır.

Daha fazla bilgi için bkz. [Hizmet Güveni Portalı](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="data-breach-reporting"></a>Veri ihlalini raporlama

Müşterinin Raporlayabildiği Güvenlik Olayı (CRSI) tanımlandığında müşteriler bilgilendirilir. Bu işlem, Intune kullanarak tüm Microsoft 365 müşterileri için ihlal bildirimine iletişim kurmak üzere Microsoft 365 ekibiyle çalışmayı içerir.

## <a name="data-sharing"></a>Veri paylaşımı

Kiracı yöneticileri bazı işlevleri (Apple Aygıt Kayıt Programı gibi) açtığında, Microsoft Intune uygun üçüncü taraflarla veri paylaşımı için yönetici onayı alır. Böyle durumlarda Intune, şu taraflarla kişisel verileri paylaşabilir:

- Microsoft 'un aracıları gibi davranan üçüncü taraflar.
- Üçüncü taraflar, Microsoft 'un aracıları olarak davranmayan, ancak yalnızca kiracı yöneticilerinin Intune iznini açıkça izin vermesi durumunda.

Microsoft aracıları olarak davranan tüm üçüncü taraflar, [çevrimiçi hizmetler taşeronları listesine](https://aka.ms/Online_Serv_Subcontractor_List)dahil edilmiştir.

Bu varlıklarla veri paylaşmanın amacı müşteri desteğine ve teknik desteğe, hizmet bakımına ve diğer işlemlere yardımcı olmaktır.

Üçüncü tarafa sahip bir kiracının sözleşmesi, üçüncü tarafın hizmetinde tutulan Intune kişisel verilerini yönetir. Bu anlaşma ayrıca Intune’a üçüncü taraf hizmete veri iletme izni verir.  

Belirli üçüncü taraflarla paylaşılan veriler hakkında daha fazla bilgi için aşağıdaki makalelere bakın:
- [Intune’un Apple’a gönderdiği veriler](data-intune-sends-to-apple.md)
- [Intune’un Google’a gönderdiği veriler](data-intune-sends-to-google.md)
- [Apple’ın Intune’a gönderdiği veriler](data-apple-sends-to-intune.md)
- [Google’ın Intune’a gönderdiği veriler](data-google-sends-to-intune.md)
- [Jamf Pro’nun Intune’a gönderdiği veriler](data-jamf-sends-to-intune.md)

### <a name="microsoft-endpoint-configuration-manager-data-sharing"></a>Microsoft uç noktası Configuration Manager veri paylaşımı

Microsoft Intune Configuration Manager hiçbir veri paylaşmaz. Configuration Manager, doğrudan müşteri tarafından dağıtılan, yönetilen ve çalıştırılan şirket içi bir üründür. Configuration Manager tarafından toplanan tanılama ve kullanım verileri yalnızca gelecek sürümlerin yükleme deneyimini, kalitesini ve güvenliğini geliştirmek için kullanılır.

Daha fazla bilgi için bkz. [Configuration Manager Için tanılama ve kullanım verileri](/configmgr/core/plan-design/diagnostics/diagnostics-and-usage-data). 


## <a name="next-steps"></a>Sonraki adımlar

Intune’da kişisel verileri [görüntülemeyi ve düzeltmeyi](privacy-data-view-correct.md) öğrenin.
