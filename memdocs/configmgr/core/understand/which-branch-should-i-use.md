---
title: Hangi dalı kullanmalıyım?
titleSuffix: Configuration Manager
description: Configuration Manager için kullanılabilir dallar arasındaki farkları öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c54648f1f98ad5fef8efd16d2abe53f204a38f5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700676"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Configuration Manager’ın hangi dalını kullanmalıyım?

*Uygulama hedefi: Configuration Manager (güncel dal & Technical Preview dalı) & System Center Configuration Manager (uzun süreli bakım dalı)*

Configuration Manager üç Dalı mevcuttur:

- Geçerli dal
- Uzun süreli bakım dalı
- Technical Preview dalı

Doğru dalı seçmenize yardımcı olması için bu makaleyi kullanın.

> [!TIP]  
> Bir hiyerarşideki tüm sitelerin aynı dalı çalıştırması gerekir. Farklı sitelerde farklı dallara sahip bir hiyerarşiye sahip olmak desteklenmez.

## <a name="current-branch"></a>Geçerli dal

Bu dal, bir üretim ortamında kullanılmak üzere lisanslanır. En son özellikleri ve işlevleri almak için bu dalı kullanın. Aşağıdaki lisanslardan birine sahipseniz, bu dalı kullanabilirsiniz:  

- System Center veri merkezi
- System Center Standart
- System Center Configuration Manager
- Eşdeğer abonelik hakları  

Yazılım Güvencesi ve lisanslama seçenekleri hakkında daha fazla bilgi için bkz. [Configuration Manager Için lisanslama ve dallar](learn-more-editions.md) ve [Configuration Manager dallar ve lisanslama hakkında sık sorulan sorular](product-and-licensing-faq.md).

Microsoft, her yıl Configuration Manager geçerli dal için güncelleştirmeleri serbest bırakmaya yönelik planlar. Her güncelleştirme sürümü, genel kullanılabilirlik (GA) yayın tarihinden itibaren 18 ay destek içinde kalır. Destek döneminin tamamına yönelik teknik destek sağlanır. Ancak, destek yapınız, en son geçerli dal sürümünün kullanılabilirliğine bağlı olarak iki ayrı hizmet aşamasında gelişen dinamik bir sürümdür. (Daha fazla bilgi için bkz. [Configuration Manager geçerli dal sürümleri Için destek](../servers/manage/current-branch-versions-supported.md). Yeni sürümlere yönelik güncelleştirmeler, konsol içi güncelleştirmeler olarak kullanılabilir.

Geçerli dalı yeni bir site olarak yüklemek için, [temel medyayı](../servers/manage/updates.md#bkmk_Baselines)kullanın. Ayrıca, System Center 2012 Configuration Manager Service Pack 2 veya System Center 2012 R2 Configuration Manager Service Pack 1 ' den yükseltmek için temel medyayı kullanın. Bu medyaya erişim, kuruluşunuzun Configuration Manager lisanslarına bağlıdır.

Ayrıca, geçerli dalın değerlendirme sürümü olan yeni bir site yüklemek için temel medyayı de kullanabilirsiniz. Değerlendirme sürümü için bir lisans gerekmez. Değerlendirme sürümünü 180 gün boyunca kullanabilirsiniz. Geçerli dalın lisanslı bir sürümüne yükseltmeyi destekler. Yalnızca bir değerlendirme sürümünü yüklemek için [değerlendirme merkezi](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)'nden alın.

> [!NOTE]
> Yeni bir Configuration Manager hiyerarşisi için site yüklemek üzere temel medyayı kullanın. Daha önce bir temel sürümü yüklediyseniz, sitelerinizi yeni bir sürüme güncelleştirmek için konsol içi güncelleştirmeleri kullanın.  
>
> Konsol içi güncelleştirmeler kullanılarak güncellenen siteler, temel medya kullanılarak yüklenen yeni siteyle aynı olan sitelerde ortaya bulunur.
>
> Daha fazla bilgi için bkz. [Configuration Manager güncelleştirmeleri](../servers/manage/updates.md).  

### <a name="features-of-the-current-branch"></a>Geçerli dalın özellikleri

- Yeni özellikleri kullanıma hazır hale getirmek için [konsol içi güncelleştirmeleri](../servers/manage/install-in-console-updates.md) alır.
- Mevcut özelliklere güvenlik ve kalite düzeltmeleri sağlayan konsol içi güncelleştirmeleri alır.
- Gerektiğinde bant dışı güncelleştirmeleri destekler. Daha fazla bilgi için bkz. [güncelleştirme kayıt aracını kullanma](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) veya [Düzeltme yükleyicisini kullanma](../servers/manage/use-the-hotfix-installer-to-install-updates.md).
- Bulut tabanlı hizmetlerle tümleştirilir.
- , [Verilerin](../migration/migrate-data-between-hierarchies.md) diğer Configuration Manager yüklemelerine geçirilmesini destekler.
- , Önceki Configuration Manager sürümlerinden yükseltmeyi destekler.
- , Daha sonra tam lisanslı bir yüklemeye yükseltebilmeniz için bir değerlendirme sürümü olarak yüklemeyi destekler.

Microsoft, sürümünden sonra en yeni sürüme güncelleştirmenizi önerir. Daha yeni bir sürüme güncelleştirmeden önce 18 aya kadar bekleyebilirsiniz. Ayrıca, kullanılabilir en yeni sürümü yüklemek için bir güncelleştirmeyi atlayabilirsiniz. Her sürüm birikimli olduğundan, bir güncelleştirmeyi atlayıp en yeni sürümü yüklerseniz, önceki sürümlere ait tüm özelliklere ve geliştirmelere erişmeye devam edersiniz.

Daha fazla bilgi için bkz. [geçerli dal sürümleri Için destek](../servers/manage/current-branch-versions-supported.md).

### <a name="current-branch-update-options"></a>Güncel dal güncelleştirme seçenekleri

- Etkin yazılım güvencesi sayesinde, güncel dal sürümleri için konsol içi güncelleştirmeleri yükleyebilirsiniz.  
- Geçerli dalı Technical Preview dalına dönüştürme seçeneği yoktur. Teknik Önizleme dalları, lisans gerektirmeyen ayrı yüklemelerdir.
- Geçerli dalınızı uzun vadeli bakım dalına (LTSB) dönüştürme seçeneği yoktur. Geçerli dalı kaldırmalı ve ardından LTSB 'yi yeni bir yükleme olarak yüklemeniz gerekir.

## <a name="long-term-servicing-branch"></a>Uzun süreli bakım dalı

Bu dal, geçerli dalı kullanan ve Configuration Manager yazılım güvencesi (SA) veya eşdeğer abonelik haklarının 1 Ekim 2016 ' den sonra dolmasına izin veren Configuration Manager müşterileri için üretimde kullanılmak üzere lisanslanır. Yazılım Güvencesi ve lisanslama seçenekleri hakkında daha fazla bilgi için bkz. [Configuration Manager Için lisanslama ve dallar](learn-more-editions.md) ve [Configuration Manager dallar ve lisanslama hakkında sık sorulan sorular](product-and-licensing-faq.md).

LTSB, sürüm 1606 ' i temel alır. Bu dal yeni özellikler sunan veya mevcut özellikleri güncelleştiren konsol içi güncelleştirmeleri almaz. Ancak kritik güvenlik düzeltmeleri sağlanır. LTSB 'yi yüklemek için System Center 2016 ile aldığınız sürüm 1606 [temel medyasını](../servers/manage/updates.md#bkmk_Baselines) kullanmanız gerekir. Daha sonraki temel sürümler LTSB 'nin yüklenmesini desteklemez.

LTSB 'yi yeni bir site olarak veya desteklenen bir System Center 2012 Configuration Manager sitesinden yükseltme olarak yüklemek için System Center 2016 ile aldığınız sürüm 1606 [temel medyasını](../servers/manage/updates.md#bkmk_Baselines) kullanın. Temel medyayı kullanarak geçerli dalın 1606 sürümünü çalıştıran yeni bir site veya uzun süreli bakım dalını çalıştıran yeni bir site yükleyebilirsiniz.

> [!TIP]  
> System Center 2016 hakkında bilgi edinmek için bkz. [System center 2016 belgeleri](/system-center/index). Bu belgede Ayrıca, bir Microsoft Lisans Sözleşmesi veya benzer haklar gerektiren System Center 2016 'nin nasıl alınacağı de tanımlanmaktadır.  
>  
> Toplu Lisanslama hizmeti Merkezi 'nde (VLSC) Configuration Manager sürüm 1606 ' yı bulmak için, [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx)'nin **indirmeler ve anahtarlar** sekmesine gidin, arama `System Center 2016` yapın ve ardından **System center 2016 Datacenter** veya **System Center 2016 Standard**' ı seçin.  
>  
> Ayrıca, [değerlendirme merkezinden](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview)System Center 2016 değerlendirme sürümünü edinebilirsiniz.  

### <a name="features-of-the-ltsb"></a>LTSB özellikleri

- Kritik güvenlik düzeltmeleri sunan konsol içi güncelleştirmeleri alır.
- SA anlaşmanızın veya Configuration Manager eşdeğer haklarınızın geçerliliği dolduğunda bir yükleme seçeneği sağlar.
- Configuration Manager için geçerli bir SA anlaşmanız veya eşdeğer haklara sahip olduğunuzda, geçerli dala yükseltmeyi (dönüştürme) destekler.

### <a name="ltsb-limitations"></a>LTSB sınırlamaları

LTSB, geçerli şube 1606 sürümünü temel alır ve aşağıdaki sınırlamalara sahiptir:

- LTSB, genel kullanıma sunulduktan sonra 10 yıllık kritik güvenlik güncelleştirmesi için desteklenir (2016 Ekim), bu dal için destek süresi dolar. Destek yaşam döngüsü hakkında daha fazla bilgi için bkz. [Microsoft yaşam döngüsü ilkesi](https://support.microsoft.com/lifecycle).
- , SQL Server sürümler gibi, sunucu ve istemci işletim sistemlerinin ve ilgili teknolojilerin sınırlı kümesini destekler. Daha fazla bilgi için bkz. [uzun süreli bakım dalı Için desteklenen konfigürasyonlar](supported-configurations-for-ltsb.md).
- Yeni özellikler için güncelleştirmeleri almaz
- Aşağıdaki özellikleri desteklemez:
  - Ortak yönetim veya masaüstü analizi gibi buluta bağlı özellikler
  - Şirket içi MDM
  - Windows 10 bakım panosu, bakım planları veya Windows 10 yarı yıllık Kanal
  - Windows 10 LTSB ve Windows Server 'ın gelecek sürümleri
  - Varlık yönetim bilgileri
  - Tüm yayın öncesi Özellikler

### <a name="ltsb-update-options"></a>LTSB Güncelleştirme seçenekleri

- LTSB yüklemenizi geçerli bir dal yüklemesine dönüştürebilirsiniz. Geçerli dala dönüştürme işlemi, LTSB süresi dolmadan önce veya sonra desteklenir.

  Dönüştürmek için, Microsoft ile etkin bir yazılım güvencesi anlaşmanız olması gerekir. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

  - [Uzun süreli bakım dalını geçerli dala yükseltme](convert-to-current-branch.md)
  - [Configuration Manager için lisanslama ve dallar](learn-more-editions.md)
  - [Temel ve güncelleştirme sürümleri](../servers/manage/updates.md#bkmk_Baselines)

- LTSB 'yi bir Technical Preview dalına dönüştürme seçeneği yoktur. Teknik Önizleme dalları, lisans gerektirmeyen ayrı yüklemelerdir.

- Geçerli dalın bir değerlendirme sürümünü LTSB yüklemesine yükseltemezsiniz.

## <a name="technical-preview-branch"></a>Technical Preview dalı

Technical Preview dalı, laboratuar ortamında kullanım içindir. Configuration Manager için geliştirilen en yeni özellikleri öğrenin ve deneyin. Üretim ortamında desteklenmez ve yazılım güvencesi lisans sözleşmenize sahip olmanızı gerektirmez.

Technical Preview dalını çalıştıran yeni bir site yüklemek için, [Technical Preview dalı için en son temel medyayı](../get-started/technical-preview.md#bkmk_install)kullanın. Technical Preview dalını yükledikten sonra, yeni sürümler her ay konsol içi güncelleştirmeler olarak kullanılabilir.

### <a name="features-of-the-technical-preview-branch"></a>Technical Preview dalının özellikleri

- Geçerli dalın en son temel sürümlerine göre
- Yüklemenizi en son Technical Preview şube sürümüne güncelleştiren konsol içi güncelleştirmeleri alır
- , Geliştirmekte olan yeni özellikleri ve Microsoft 'un geri bildiriminizi istediğini belirten özellikler içerir
- Yalnızca Technical Preview dalı için uygulanan güncelleştirmeleri alır

### <a name="technical-preview-limitations"></a>Teknik Önizleme sınırlamaları

- Yalnızca tek bir birincil site ve en fazla 10 istemci dahil olmak üzere [destek sınırlıdır](../get-started/technical-preview.md#bkmk_reqs).  
- Bunu yükseltmez veya geçerli bir dala veya LTSB yüklemesine geçiremezsiniz.
- Aşağıdaki davranışları desteklemez:
  - Verileri başka bir Configuration Manager yüklemesine içeri veya dışarı aktarmak için geçişi kullanın
  - Configuration Manager önceki bir sürümünden yükseltme
  - Değerlendirme sürümü olarak yükleyin

Bir Technical Preview dalında ilk olarak sunulan özellikler, genellikle sonraki bir güncelleştirmedeki güncel dala eklenir. Her yeni Technical Preview dalı sürümü, bu özellikler geçerli dala eklendikten sonra bile önceki Technical Preview dallarındaki özellikleri içerir.

Daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](../get-started/technical-preview.md).

### <a name="technical-preview-update-options"></a>Technical Preview güncelleştirme seçenekleri

- Yeni bir Technical Preview dalı sürümü için konsol içi tüm güncelleştirmeleri yükleyebilirsiniz.

- Technical Preview dalını geçerli dala veya LTSB 'ye dönüştürme seçeneği yoktur.

## <a name="identify-your-version-and-branch"></a>Sürümünüzü ve dalınızı tanımla

### <a name="version"></a>Sürüm

Sitenizin sürümünü denetlemek için konsolun sol üst köşesindeki **Configuration Manager hakkında** bölümüne gidin. Bu iletişim kutusu **site sürümünü**görüntüler. Site sürümlerinin listesi için bkz. [temel ve güncelleştirme sürümleri](../servers/manage/updates.md#bkmk_Baselines).

### <a name="branch"></a>Dal

Sitenizin dalını onaylamak için, konsolunda **Yönetim**  >  **Site yapılandırması**  >  **siteler**' e gidin ve **Hiyerarşi ayarları**' nı açın. Geçerli dala dönüştürmek için etkin bir seçenek varsa, site LTSB sürümünü çalıştırır. Site geçerli dalı çalıştırdığında, konsol bu seçeneği devre dışı bırakır.

Configuration Manager farklı sürümleri hakkında daha fazla bilgi için bkz. [temel ve güncelleştirme sürümleri](../servers/manage/updates.md#bkmk_Baselines).