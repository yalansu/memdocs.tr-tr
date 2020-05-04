---
title: Sorgular için güvenlik ve gizlilik
titleSuffix: Configuration Manager
description: Site veritabanından bilgi sorgulayıp güvenlik ve gizlilik için en iyi uygulamaları anlayın.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714615"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Configuration Manager sorgularda güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager sorguları, belirttiğiniz ölçütlere göre site veritabanından bilgi almanızı sağlar. Configuration Manager, standart işlem sırasında site veritabanı bilgilerini toplar. Örneğin, bulma veya envanter sırasında toplanan bilgileri kullanarak, belirtilen ölçütlere uyan cihazları tanımlamak için bir sorgu yapılandırabilirsiniz.  

 Sorgular hakkında daha fazla bilgi için bkz. [sorgulara giriş](../../../core/servers/manage/introduction-to-queries.md). Sorgu kullanarak alabileceğiniz verileri toplayacak Configuration Manager işlemlerle ilgili en iyi güvenlik uygulamaları ve gizlilik bilgileri için bkz. [Configuration Manager Için güvenlik ve gizlilik](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Sorgular için en iyi güvenlik yöntemleri

 Sorgular için bu en iyi güvenlik uygulamasını kullanın.  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Ağ konumuna kaydedilen bir sorguyu dışarı veya dışarı aktardığınızda, konumu ve ağ kanalını güvenli hale getirin.|Ağ klasörüne erişebilecek kişileri kısıtlayın.<br /><br /> Bir saldırganın içeri aktarılmadan önce sorgu verilerinin üzerinde değişiklik yapmasını engellemek için ağ konumu ile site sunucusu arasında sunucu Ileti bloğu (SMB) imzası veya Internet Protokolü güvenliği (IPSec) kullanın.|  

## <a name="next-steps"></a>Sonraki adımlar
  
[Configuration Manager için güvenlik ve gizlilik](../../../core/plan-design/security/security-and-privacy.md)
