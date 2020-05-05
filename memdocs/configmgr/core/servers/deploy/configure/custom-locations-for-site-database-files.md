---
title: Özel veritabanı dosya konumları
titleSuffix: Configuration Manager
description: SQL Server veritabanı dosyaları için özel konumlar belirtmeyi öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc7eb1a8ba721545bdee50d45887ab9d3aa8e952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721013"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Configuration Manager site veritabanı dosyaları için özel konumlar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Configuration Manager, SQL Server veritabanı dosyaları için özel konumları destekler.  

> [!NOTE]  
>  Bir SQL Server kümesi kullandığınızda varsayılan olmayan dosya konumlarını belirtme seçeneği kullanılamaz.  

 Yeni bir birincil sitenin veya merkezi yönetim sitesinin **kurulumu sırasında** şunları yapabilirsiniz:  

-   **Site veritabanı için varsayılan olmayan dosya konumlarını belirtin**: Configuration Manager Kurulum daha sonra bu konumları kullanarak site veritabanını oluşturur.  

-   **Özel dosya konumlarını kullanan önceden oluşturulmuş bir SQL Server veritabanının kullanımını belirtin**: Configuration Manager Kurulum, önceden oluşturulmuş bu veritabanını ve önceden yapılandırılmış dosya konumlarını kullanır.  

**Kurulumdan sonra**site veritabanı dosyalarının konumunu değiştirebilirsiniz. Bu, siteyi durdurmanız ve SQL Server dosya konumunu düzenlemeniz gerekir:  

-   Configuration Manager site sunucusunda **SMS_Executive** hizmetini durdurun.  

-   Kullanıcı veritabanını taşıma konusunda size rehberlik etmek için SQL Server sürümünüze yönelik belgeleri kullanın. Örneğin, SQL Server 2014 kullanıyorsanız, bkz. TechNet 'teki [Kullanıcı veritabanlarını taşıma](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) .  

-   Veritabanı dosyası taşımayı tamamladıktan sonra, Configuration Manager site sunucusunda **SMS_Executive** hizmetini yeniden başlatın.  
