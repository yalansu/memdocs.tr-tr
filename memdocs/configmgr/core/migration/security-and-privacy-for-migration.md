---
title: Geçiş güvenliği ve gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager geçerli dal ortamınıza geçiş için en iyi güvenlik yöntemlerini ve gizlilik bilgilerini alın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f219c6c6d4c9a5cbf04b1295c99184f345e68b83
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692868"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Güncel dala Configuration Manager geçişe yönelik güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konuda, Configuration Manager geçerli dal ortamınıza geçiş için en iyi güvenlik uygulamaları ve gizlilik bilgileri yer almaktadır.  

## <a name="security-best-practices-for-migration"></a>Geçiş için En Iyi güvenlik uygulamaları  
 Geçiş için aşağıdaki en iyi güvenlik uygulamasını kullanın.  

|En iyi güvenlik yöntemi|Daha fazla bilgi|  
|----------------------------|----------------------|  
|Kaynak site SMS sağlayıcı hesabı ve kaynak site SQL Server hesap için bir kullanıcı hesabı yerine bilgisayar hesabını kullanın.|Geçiş için bir kullanıcı hesabı kullanmanız gerekiyorsa, geçiş tamamlandığında hesap ayrıntılarını kaldırın.|  
|Kaynak sitedeki bir dağıtım noktasından hedef sitenizdeki bir dağıtım noktasına içerik geçirdiğinizde IPSec kullanın.|Geçirilen içerik, geçişi tespit etmek için karma hale gelse de veriler aktarılırken değiştirilirse geçiş başarısız olur.|  
|Geçiş işleri oluşturabileceğiniz yönetici kullanıcıları kısıtlayın ve izleyin.|Hedef hiyerarşinin veritabanının bütünlüğü, yönetici kullanıcının kaynak hiyerarşiden içeri aktarmayı seçtiği verilerin bütünlüğünden bağlıdır. Ayrıca, bu yönetici kullanıcı kaynak hiyerarşideki tüm verileri okuyabilir.|  

### <a name="security-issues-for-migration"></a>Geçiş için güvenlik sorunları  
Geçiş aşağıdaki güvenlik sorunlarına sahiptir:  

-   Bir kaynak siteden engellenen istemciler, istemci kayıtları geçirilmeden önce hedef hiyerarşiye başarıyla atayabilir.  

     Configuration Manager, geçiş yaptığınız istemcilerin engellenmiş durumunu koruyabilse de, istemci kaydının geçişi tamamlanmadan önce atama gerçekleşirse istemci hedef hiyerarşiye başarıyla atayabilir.  

-   Denetim iletileri geçirilmez.  

Bir kaynak siteden hedef siteye veri geçirdiğinizde, kaynak hiyerarşideki tüm denetim bilgilerini kaybedersiniz.  

## <a name="privacy-information-for-migration"></a>Geçiş için gizlilik bilgileri  
 Geçiş, kaynak altyapıda belirttiğiniz site veritabanlarından bilgileri bulur ve bu verileri hedef hiyerarşisindeki veritabanına depolar. Configuration Manager bir kaynak sitesinden veya hiyerarşiye bulabildiği bilgiler, kaynak ortamda gerçekleştirilen yönetim işlemlerinin yanı sıra kaynak ortamda etkinleştirilen özelliklere bağlıdır.  

 Güvenlik ve gizlilik bilgileri hakkında daha fazla bilgi için aşağıdaki konulardan birine bakın:  

-   Configuration Manager 2007 gizlilik bilgileri hakkında daha fazla bilgi için Configuration Manager 2007 belge kitaplığındaki [Configuration Manager 2007 Için güvenlik ve gizlilik](/previous-versions/system-center/configuration-manager-2007/bb680768(v=technet.10)) bölümüne bakın.  

-   System Center 2012 Configuration Manager gizlilik bilgileri hakkında daha fazla bilgi için System Center 2012 Configuration Manager belge kitaplığı 'nda  [System center 2012 Configuration Manager Için güvenlik ve gizlilik](/previous-versions/system-center/system-center-2012-R2/gg682033(v=technet.10)) bölümüne bakın.  

-   Configuration Manager gizlilik bilgileri hakkında daha fazla bilgi için bkz. [Configuration Manager Için güvenlik ve gizlilik](../../core/plan-design/security/security-and-privacy.md).  

Desteklenen verilerin bazılarını veya tümünü bir kaynak sitesinden hedef hiyerarşiye geçirebilirsiniz.  

Geçiş varsayılan olarak etkin değildir ve birkaç yapılandırma adımı gerektirir. Geçiş bilgileri Microsoft 'a gönderilmez.  

Bir kaynak hiyerarşisinden veri geçirmeden önce gizlilik gereksinimlerinizi göz önünde bulundurun.