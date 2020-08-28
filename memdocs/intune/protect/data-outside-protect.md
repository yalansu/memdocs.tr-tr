---
title: Şirket verilerine yetkisiz erişimi engelleme
titleSuffix: Microsoft Intune
description: Microsoft Intune kullanarak şirket ağı dışında paylaşılan şirket verilerine yetkisiz erişimi engelleyin.
keywords: Microsoft 365 M365 Azure Information Protection verileri dış ağ şirket verilerini koruma
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6a88573a-aa60-455c-858c-74562798246b
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24d0ed7b9111e54c4912cf23cd5b52072253c931
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996155"
---
# <a name="prevent-unauthorized-access-to-company-data-using-microsoft-intune"></a>Microsoft Intune kullanarak şirket verilerine yetkisiz erişimi engelleme

Microsoft 365 belgelerini ve e-postaları sınıflandırabilir, etiketleyebilir ve koruyabilir ve yalnızca yetkili kullanıcıların verilere erişimi vardır. Ayarlar, BT yöneticileri veya kullanıcılar kurallar ve koşullar koyduktan sonra otomatik olarak yönetilir. Alternatif olarak BT ekibi, kullanıcıların izlemesi için önerilen ayarlar sağlayabilir. Ayrıca yöneticiler ve kullanıcılar daha önceden başkalarıyla paylaşılan verilere erişimi başka bir yetkilinin yardımı gerekmeden iptal edebilir. Bu işlemlerin sonucu, şirket ağının dışına çıktıklarında bile korumalı verileri kimin açtığını veya güncelleştirdiğini denetlemektir. 

## <a name="before-you-begin"></a>Başlamadan önce

Aşağıdaki koşulları yerine getirdiğinizde aşağıdaki eylem planı kullanılabilir:
* Şirketiniz buluta güvenli bir şekilde geçiş yapmaya hazırdır.
* Şirketiniz Exchange Online, SharePoint Online, OneDrive Iş veya Yammer Microsoft 365 kullanıyor.
* Şirketinizin Microsoft 365, Enterprise Mobility + Security (EMS) veya Azure Information Protection lisansları vardır.
* Şirketiniz Windows 7 Service Pack 1 veya üzerini çalıştıran cihazlarla çalışıyordur.
* Şirketiniz, 2016 uygulama veya 2013 uygulama, Office Professional Plus 2016, Office Professional 2013 Plus with Service Pack 1 veya Office Professional Plus 2010 ile Microsoft 365 uygulamalar kullanır.

## <a name="action-plan"></a>Eylem planı

[Azure Information Protection için hızlı başlangıç öğreticisi](/information-protection/get-started/infoprotect-quick-start-tutorial)'ni tamamlayın.  

## <a name="what-to-tell-employees-and-students"></a>Çalışanlara ve öğrencilere söylenecekler

[Hassas bilgiler içeren belge ve e-postaları nasıl ve ne zaman koruyacağınızın](/information-protection/deploy-use/help-users) ayrıntılarını paylaşabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

Sonraki adımların parçası olarak, şirket verilerinizin güvenliğini arttırmak için aşağıdaki gibi diğer yollar hakkında bilgi edinebilirsiniz: 

* [İOS/ıpados ve Android cihazlarda Azure Information Protection](/information-protection/rms-client/mobile-app-faq)kullanmayı öğrenin.
* Mac bilgisayarlar için [Microsoft Rights Management Sharing uygulaması](/previous-versions/msdn10/dn451248(v=msdn.10))hakkında bilgi edinin.
