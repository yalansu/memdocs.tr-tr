---
title: LTSB 'ye giriş
titleSuffix: Configuration Manager
description: Configuration Manager uzun süreli bakım dalı hakkında bilgi edinin.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1370c1bf80283ff30ad54378ad58ecd9a5d24d47
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699373"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Configuration Manager uzun vadeli bakım dalına giriş

*Uygulama hedefi: System Center Configuration Manager (uzun süreli bakım dalı)*

Configuration Manager uzun süreli bakım dalı (LTSB), tüm müşteriler için kullanılabilir bir Install seçeneği olarak tasarlanan ayrı bir daldır. Bununla birlikte, yazılım güvencesi (SA) veya Configuration Manager için eşdeğer abonelik haklarını ayırt edebilen müşteriler için tek seçenektir.

Configuration Manager sürüm 1606 temelinde, LTSB, Configuration Manager geçerli dalı ile karşılaştırıldığında işlevselliği düşürür.

> [!TIP]   
> Configuration Manager LTSB, System Center Suite uzun süreli bakım kanalı (LTSC) ile ilgili değildir. Daha fazla bilgi için bkz. [System Center sürüm seçeneklerine genel bakış](/system-center/ltsc-and-sac-overview).

## <a name="features-that-arent-available"></a>Kullanılamayan özellikler

Configuration Manager geçerli dalı, LTSB kullandığınızda kullanılamayan aşağıdaki işlevleri destekler:

- Yeni özellikler ve geliştirmeler ekleyen konsol içi güncelleştirmeler.
- Site sunucuları ve istemciler olarak kullanılmak üzere yeni yayınlanan işletim sistemleri için destek.
- Şirket içi MDM
- Son Windows 10 sürümleri için destek de dahil olmak üzere Windows 10 bakım panosu ve bakım planları.  
- Windows Server ve Windows 10 LTSB 'nin gelecek sürümleri için destek
- Varlık Yönetim Bilgileri
- Bulut tabanlı dağıtım noktaları
- Exchange Connector olarak Exchange Online    

Bu özellikler için destek LTSB ile kullanılamaz, ancak bazı özellikler Configuration Manager konsolunda görünür halde kalır, ancak seçilemez veya kullanılmaz.

Bulut tümleştirmelerine ek olarak Configuration Manager geçerli şube 1610 veya üzeri sürümlerde bulunan tüm özellikler, LTSB tarafından kullanılamaz. Bu özellikler şunları içerir, ancak bunlarla sınırlı değildir:<!--SCCMDocs#1823-->

- Ortak yönetim
- Desktop Analytics
- Bulut yönetimi ağ geçidi
- Azure Active Directory tümleştirmesi
- Iş Microsoft Store uygulamalar

## <a name="find-ltsb-documentation"></a>LTSB belgelerini bulun

LTSB, geçerli dal sürüm 1606 ' i temel alır. LTSB 'ye özgü uyarılar ve sınırlamalar ile [geçerli dal belgelerini](../../index.yml)kullanın. Bu uyarılar ve sınırlamalar aşağıdaki makalelerde tanımlanmıştır:

- [LTSB’yi yükleme](install-the-ltsb.md)
- [LTSB’yi güncel dala yükseltme](convert-to-current-branch.md)
- [LTSB için desteklenen yapılandırmalar](supported-configurations-for-ltsb.md)
- [LTSB Configuration Manager yönetme](manage-the-ltsb.md)

LTSB için geçerli dal belgelerine başvurduğunuzda, 1606 veya daha önceki sürümleri için geçerli olan ayrıntılar LTSB 'ye de uygulanır. Sürüm 1610 veya üzeri ile tanıtılan özellikler veya Ayrıntılar LTSB tarafından desteklenmez.

## <a name="licensing-overview-for-the-ltsb"></a>LTSB için lisanslamaya genel bakış   

Configuration Manager lisanslarında etkin yazılım güvencesi (SA) olan veya 1 Ekim 2016 itibariyle eşit abonelik haklarıyla olan müşteriler, Configuration Manager Ekim 2016 sürüm 1606 sürümünü kullanma hakkına sahiptir. 1 Ekim 2016 ' de veya sonrasında Configuration Manager hakları olan müşteriler, yükleme sonrasında iki lisanslı seçenek bulur: geçerli dal ve uzun süreli bakım dalı (LTSB).

System Center Configuration Manager için kalıcı haklara sahip olan ya da SA veya aboneliğin 1 Ekim 'den sonra bulunmasına izin veren müşteriler, atlama sırasında geçerli olan System Center Configuration Manager LTSB sürümünü yükleyebilir.

Bu lisanslar hakkında daha fazla bilgi için [Microsoft Toplu Lisanslama programları aracılığıyla satın aldığınız ürünlerin hüküm ve koşullarına](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)bakın.

Configuration Manager dalları için lisanslama hakkında daha fazla bilgi için bkz. [Configuration Manager lisanslama ve dallar](learn-more-editions.md).

## <a name="next-steps"></a>Sonraki Adımlar

Configuration Manager LTSB 'nin ortamınız için doğru dalı olduğuna, yeni bir hiyerarşinin parçası olarak [Yeni BIR LTSB sitesi yüklemeye](install-the-ltsb.md#install-a-new-site) veya [bir System Center 2012 Configuration Manager sitesini](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager) ve hiyerarşisini yükseltmeye karar verirseniz.