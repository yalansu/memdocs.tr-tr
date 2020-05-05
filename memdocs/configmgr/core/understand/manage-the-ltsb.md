---
title: LTSB’yi yönetme
titleSuffix: Configuration Manager
description: LTSB System Center Configuration Manager için yönetim farkları.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86e7579832a5a59c3609d24744eb646e1a4c1fd1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722707"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Configuration Manager Uzun Süreli Bakım Dalı yönetin

*Uygulama hedefi: System Center Configuration Manager (uzun süreli bakım dalı)*

System Center Configuration Manager uzun süreli bakım dalı (LTSB) kullandığınızda aşağıdakiler, altyapınızı nasıl yöneteceğinizi etkileyen önemli değişiklikleri anlamanıza yardımcı olabilir.

LTSB, Güncel Dalı sürüm 1606 ' e (Intune tümleştirmesi ve bulutla ilgili özellikler gibi bazı özel durumlarla) eşdeğer olduğundan, planlama, dağıtım, yapılandırma ve günlük yönetimi için kullandığınız görevlerin çoğu aynıdır.

Örneğin, LTSB, Güncel Dalı aynı sayıda site, site türü, istemci ve genel altyapıyı destekler. Bu nedenle, Güncel Dalı için site ve hiyerarşi planlama ve tasarım konularında bulunan Kılavuzu kullanırsınız. Benzer şekilde, yazılım güncelleştirmeleri ya da Işletim sistemi dağıtımı gibi her iki dal tarafından desteklenen LTSB özellikleri için, Güncel Dalı sürüm 1606 ' den sonra sunulan özellik değişikliklerine erişimi olmayan uyarılar ile Güncel Dalı belgelerinin bu bölümlerinde bulunan kılavuzu kullanın.

Aşağıdaki bölümlerde, benzer olmayan görevleri yönetme hakkında bilgi sağlanmaktadır.

## <a name="updates-and-servicing"></a>Güncelleştirmeler ve bakım
LTSB 'de konsol içi güncelleştirmeler olarak yalnızca kritik güvenlik güncelleştirmeleri kullanılabilir hale getirilir.  

Sonraki Güncel Dalı sürümleri için düzenli güncelleştirmeler hakkında bilgiler konsolunda görünür, ancak LTSB tarafından kullanılamaz. Bunlar indirilmez ve yüklenemez.

Kritik güvenlik düzeltmeleriyle ilgili konsol içi güncelleştirmeleri desteklemek için, bir LTSB sitesi [hizmet bağlantı noktasının](../servers/deploy/configure/about-the-service-connection-point.md)kullanılmasını gerektirir. Güncel Dalı için yapıldığından, bu site sistem rolünü çevrimdışı veya çevrimiçi modda yapılandırabilirsiniz. LTSB, Güncel Dalı aynı telemetri ve kullanım verilerini toplar ve gönderir.

LTSB, Güncel Dalı makalesinde belgelenen düzeltme yükleyicisinin ve güncelleştirme kayıt aracının kullanımını destekler.

Güncelleştirmeler ve bakım hakkında genel bilgi için bkz. [güncelleştirmeler Configuration Manager](../servers/manage/updates.md).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Site genişletmesi ve CD için değişiklikler. En son klasör
LTSB 'yi çalıştırdığınızda ve yeni bir merkezi yönetim sitesi yükleyerek bağımsız bir birincil siteyi genişlettikten sonra, sürüm 1606 temel medyasından kurulum 'U ve kaynak dosyalarını kullanmanız gerekir. Güncel Dalı için kurulum 'U çalıştırın ve kaynak dosyalarını CD 'den kullanın. En son klasör.

Site genişletmesi için kurulum 'U CD 'den çalıştırmayın olsanız da. En son klasör, CD 'yi kullanmaya devam edersiniz. Site Recovery için en son klasör ve ilk LTSB siteniz bir merkezi yönetim sitesi olduğunda yeni bir alt birincil site yüklemek.

Site genişletmesi hakkında daha fazla bilgi için bkz. [tek başına birincil siteyi genişletme](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand). CD hakkında daha fazla bilgi için. En son klasör, [CD 'ye bakın. En son klasör](../servers/manage/the-cd.latest-folder.md).


## <a name="recovery"></a>Kurtarma
Bir siteyi kurtardığınızda, siteyi veya site veritabanını özgün dalına geri yüklemeniz gerekir. Bir Güncel Dalı site veritabanını bir LTSB yüklemesine kurtaramazsınız veya tam tersi de geçerlidir.
