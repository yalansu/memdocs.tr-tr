---
title: Intune’da veri depolama ve işleme
titleSuffix: Microsoft Intune
description: Intune’da kişisel verilerin nasıl depolanıp işlendiğini öğrenin.
keywords: veri, gizlilik
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c7c597a6d196ab5f8c3170cd5880682a280e73
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076072"
---
# <a name="data-storage-and-processing-in-intune"></a>Intune’da veri depolama ve işleme

### <a name="storing-customer-data"></a>Müşteri verilerini depolama

Intune [verileri topladıktan](privacy-data-collect.md)sonra Intune, müşteri verilerinin nasıl depolandığını ve işlendiğini belirten Microsoft 365 Için veri işleme standart ilkesini izler. [Microsoft 365 müşteri verilerinizin nerede depolandığını](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations)görün. Kişisel veriler, [Microsoft Online Services koşulları 'nda (OST)](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)bulunan teknik güvenlik önlemleri altında Intune hizmetinin denetlenen uyumluluk sınırında işlenir.

### <a name="storage-locations"></a>Depolama konumları

Microsoft, Intune hizmetlerini dünya çapında birçok bölgede sunmakta ve yönetmektedir. Intune, yönetici tarafından Müşteri Verileri için yapılan depolama konumu seçimlerine saygı duyar.

Daha fazla bilgi için bkz. [veri merkezi konumları](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations?view=o365-worldwide#data-center-locations)

### <a name="personal-data-retention"></a>Kişisel verilerin saklanması

Microsoft 365 veri Işleme standart ilkesi, müşteri verilerinin silindikten sonra ne kadar süreyle korunacağını belirtir. Müşteri verilerinin silindiği iki senaryo vardır:

-**Etkin silme**: kiracıda etkin bir abonelik vardır ve bir Kullanıcı ya da yönetici verileri siler ya da yöneticiler bir kullanıcıyı siler.
-**Pasif silme**: kiracı aboneliği sona erer.

Her silme senaryosunda, bkz. [Microsoft 365 veri saklama, silme ve yok etme](https://docs.microsoft.com/microsoft-365/enterprise/microsoft-365-data-retention-deletion-and-destruction-overview?view=o365-worldwide).  

Genel olarak, Intune tarafından toplanan kişisel veriler, silinmeden sonra 30 gün içinde kaldırılır. Denetim günlükleri, güvenlik amacıyla bir yıla kadar tutulur. 


## <a name="processing-personal-data"></a>Kişisel verilerin işlenmesi

Intune, kişisel verileri ISO sertifikalı sistemlerle işler. Daha fazla bilgi için bkz. [Hizmet Güveni Portalı](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="profiling-and-marketing"></a>Profil oluşturma ve pazarlama

Microsoft Intune, hizmet sağlama işleminin parçası olarak toplanan hiçbir kişisel veriyi profil oluşturma veya pazarlama amacıyla kullanmaz. 

## <a name="next-steps"></a>Sonraki adımlar

Intune’un verileri nasıl [güvenlik altına aldığı ve paylaştığı](privacy-data-secure-share.md) hakkında daha fazla bilgi edinin. 
