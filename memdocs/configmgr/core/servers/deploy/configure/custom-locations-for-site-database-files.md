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
ms.openlocfilehash: e8e4bf4eb11502d798ffa97500436494bc639aae
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607607"
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

-   Kullanıcı veritabanını taşıma hakkında daha fazla bilgi için bkz. [Kullanıcı veritabanlarını taşıma](/sql/relational-databases/databases/move-user-databases).  

-   Veritabanı dosyası taşımayı tamamladıktan sonra, Configuration Manager site sunucusunda **SMS_Executive** hizmetini yeniden başlatın.