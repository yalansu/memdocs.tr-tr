---
title: Sürümler arasında birlikte çalışabilirlik
titleSuffix: Configuration Manager
description: Aynı ağ üzerinde birden çok Configuration Manager hiyerarşisi arasındaki çakışmaların nasıl önleneceğini öğrenin.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713089"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Configuration Manager'ın farklı sürümlerinin birlikte çalışabilirliği

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Aynı ağda birden çok bağımsız Configuration Manager hiyerarşisi yükleyebilir ve çalıştırabilirsiniz. Ancak, farklı Configuration Manager hiyerarşileri geçiş işlemi dışında birlikte çalışmadığından, her hiyerarşinin aralarında çakışmaları engellemek için yapılandırmaların olması gerekir. Ayrıca, yönettiğiniz kaynakların doğru hiyerarşideki site sistemleriyle etkileşime geçmesini sağlamak için belirli yapılandırmalarda de oluşturabilirsiniz.  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a>Geçerli dal ve önceki sürümler arasında birlikte çalışabilirlik  

Farklı sürümlerin siteleri aynı Configuration Manager hiyerarşisinde birlikte bulunamaz. Yalnızca aşağıdaki yükseltme senaryolarındaki işlemler sırasında özel durumlar geçerlidir:

- System Center 2012 Configuration Manager ' den geçerli dalı Configuration Manager
- Konsol içi güncelleştirmeleri kullanarak bir Configuration Manager geçerli dal sürümünden daha yeni bir sürüme

Mevcut Configuration Manager bir dal sitesini ve hiyerarşiyi, var olan System Center 2012 Configuration Manager sitesi veya hiyerarşisi ile yan yana dağıtabilirsiniz. Her iki sürümden da istemcilerin bir siteye diğer sürümden katılmayı denemeye çalışmasını önlemeye yönelik plan yapın.

Örneğin, iki veya daha fazla Configuration Manager hiyerarşisi aynı ağ konumlarını içeren [çakışan sınırlar](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries) içeriyorsa, her yeni istemciyi otomatik site ataması kullanmak yerine belirli bir siteye atayın. Daha fazla bilgi için bkz. [istemcileri bir siteye atama](../../clients/deploy/assign-clients-to-a-site.md).  

Ayrıca, Configuration Manager geçerli dalından bir site sistem rolü barındıran bir bilgisayara System Center 2012 Configuration Manager 'den istemci yükleyemezsiniz. Ayrıca, System Center 2012 Configuration Manager bir site sistemi rolü barındıran bir bilgisayara Configuration Manager geçerli bir dal istemcisi yükleyemezsiniz.  

Aşağıdaki istemciler ve bağlantılar desteklenmez:  

- Tüm System Center 2012 Configuration Manager veya önceki bir bilgisayar istemci sürümü  

- Herhangi bir System Center 2012 Configuration Manager veya önceki bir cihaz yönetim istemcisi  

- Windows CE Platform Builder cihaz yönetimi istemcisi (herhangi bir sürüm)  

- System Center Mobil Cihaz Yöneticisi VPN bağlantısı  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> İstemci site atama konuları  

Configuration Manager istemcileri yalnızca tek bir birincil siteye atanabilir. Aşağıdaki koşulların tümü doğru olduğunda bir istemcinin gerçek site atamasını tahmin edemiyoruz:

- İstemci yüklemesi sırasında bir siteye istemcileri atamak için otomatik site atamasını kullanın
- Birden fazla sınır grubu aynı sınırı içeriyor
- Sınır grupları farklı atanmış sitelere sahip

Sınırlar birden çok Configuration Manager sitesi ve hiyerarşilerde çakışırsa, istemciler istediğiniz siteye atanmayabilir veya hiçbir siteye atanmayabilir.  

Geçerli dal istemcilerinin Configuration Manager site atamasını tamamlamadan önce sitenin sürümünü kontrol edin. Site sınırları çakışırsa, istemcileri önceki bir sürüme sahip bir siteye atayamazsınız. Ancak, daha önceki System Center 2012 Configuration Manager istemcileri daha sonra güncel bir Configuration Manager dalı sitesine atanabilir.  

İki hiyerarşinin çakışan sınırları olduğunda istemcilerin yanlışlıkla yanlış siteye atanmasını engellemek için istemci yükleme parametrelerini, istemcileri belirli bir siteye atayacak şekilde yapılandırın.  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a>Karma sürümlü bir hiyerarşide Configuration Manager sınırlamaları  

Configuration Manager geçerli bir dal hiyerarşisini yükselttiğinizde, farklı sitelerin farklı sürümlere sahip olacağı zamanlar vardır. Örneğin, ilk olarak merkezi yönetim sitesini yükseltirsiniz. Site bakım pencereleri nedeniyle, birincil siteleri daha sonra bir saat ve tarihe kadar yükseltmezsiniz.  

Tek bir hiyerarşideki farklı siteler farklı sürümler çalıştırırken bazı işlevler kullanılamaz. Bu davranış, Configuration Manager konsolundaki Configuration Manager nesneleri nasıl yönetebileceğinizi ve istemcilerin hangi işlevselliğe kullanılabildiğini etkileyebilir. Genellikle, Configuration Manager yeni sürümünün işlevselliği, sitelerde veya daha düşük hizmet paketi sürümü çalıştıran istemcilerde erişilebilir değildir.  

### <a name="network-access-account"></a>Ağ erişim hesabı

Merkezi yönetim sitesini güncel dalı Configuration Manager yükseltirsiniz. Bu güncelleştirilmiş siteye bağlı bir Configuration Manager konsolundan ağ erişim hesabı ayrıntılarını görüntüleyebilirsiniz. Hala System Center 2012 Configuration Manager çalıştıran sitelerden hesap ayrıntılarını görüntülemez.

Birincil siteyi merkezi yönetim sitesiyle aynı sürüme yükselttikten sonra hesap ayrıntıları konsolda görünür.

Configuration Manager sürümleri arasında güncelleştirme yaptığınızda aynı davranış geçerlidir.

### <a name="boot-images-for-os-deployment"></a>İşletim sistemi dağıtımı için önyükleme yansımaları

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>System Center 2012 Configuration Manager Configuration Manager güncel dala yükseltirken

Bir hiyerarşinin en üst düzey sitesi geçerli dalı Configuration Manager yükselttiğinde, varsayılan önyükleme görüntülerini otomatik olarak Windows değerlendirme ve Dağıtım Seti (ADK) sürüm 10 ' u kullanacak şekilde güncelleştirir. Bu önyükleme görüntülerini yalnızca Configuration Manager geçerli şube sitelerindeki istemcilere dağıtımlar için kullanın. Daha fazla bilgi için bkz. [işletim sistemi dağıtımı birlikte çalışabilirliği Için planlama](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>Configuration Manager geçerli dal sürümleri arasında yükseltirken

Yeni Configuration Manager sürümleri kullanımda olan Windows ADK sürümünü güncelleştirmedikçe önyükleme görüntüleri üzerinde hiçbir etkisi yoktur.

### <a name="new-task-sequence-steps"></a>Yeni görev dizisi adımları

Önceki bir sürümde kullanılamayan bir Configuration Manager sürümünde tanıtılan bir adımla bir görev dizisi oluşturduğunuzda aşağıdaki sorunlarla karşılaşabilirsiniz:

- Bir Configuration Manager önceki bir sürümünü çalıştıran bir siteden görev sırasını düzenlemeye çalıştığınızda bir hata oluşur.

- Görev sırası, Configuration Manager istemcisinin önceki bir sürümünü çalıştıran bir bilgisayarda çalışmıyor.

### <a name="client-to-down-level-management-point-communications"></a>İstemciden alt düzey yönetim noktası iletişimleri

İstemciden daha düşük bir sürüm çalıştıran bir sitedeki yönetim noktasıyla iletişim kuran bir Configuration Manager istemcisi, yalnızca Configuration Manager alt düzey sürümünün desteklediği işlevleri kullanabilir. Örneğin, yakın zamanda o sürüme yükseltilmemiş bir yönetim noktasıyla iletişim kuran bir istemciye yükseltilen bir Configuration Manager geçerli dal sitesinden içerik dağıtırsanız, bu istemci en son sürümdeki yeni işlevselliği kullanamaz.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Eski istemcilere paket ve görev dizisi dağıtımları

<!-- SCCMDocs-pr issue #3493 -->

Sürüm 1902 ' den başlayarak, bir paket veya görev dizisini bir istemci sürümüne 5,7730 veya daha önceki bir sürüme dağıtamazsınız. Bu sınırlamaya geçici bir çözüm bulmak için istemciyi daha sonraki bir sürüme yükseltin.

## <a name="software-updates"></a>Yazılım güncelleştirmeleri

### <a name="orchestration-groups"></a>Düzenleme grupları

Sürüm 2002 ' de tanıtılan düzenleme grupları, Karma sürümlü bir hiyerarşide kullanılamaz. <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a>Configuration Manager konsolu için birlikte çalışabilirlik  

Bu bölüm, Configuration Manager sürümlerinin karışımına sahip bir ortamda Configuration Manager konsolunun kullanımı hakkında bilgiler içerir.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>System Center 2012 Configuration Manager ve geçerli dalı Configuration Manager bir ortam

Bir Configuration Manager sitesini yönetmek için hem konsol hem de konsolun bağlandığı site aynı Configuration Manager sürümünü çalıştırmalıdır. Örneğin, bir Configuration Manager güncel dal sitesini veya başka bir şekilde yönetmek için bir System Center 2012 Configuration Manager konsolu kullanamazsınız.

Hem System Center 2012 Configuration Manager Configuration Manager konsolunun hem de geçerli dal konsolunun aynı bilgisayara yüklenmesi desteklenmez.

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>Configuration Manager birden çok sürümü olan ortam

Configuration Manager geçerli dal, bir bilgisayara birden fazla Configuration Manager konsolunun yüklenmesini desteklemez. Configuration Manager farklı sürümlerine özel birden çok konsol kullanmak için ayrı bilgisayarlara farklı konsolları yüklersiniz.

Bir hiyerarşideki siteleri yeni bir sürüme güncelleştirme işlemi sırasında, bir konsolu daha yeni bir sürüm çalıştıran bir siteye bağlayabilirsiniz ve bu hiyerarşideki diğer sitelerle ilgili bilgileri görüntüleyebilirsiniz. Ancak bu yapılandırma önerilmez. Konsol sürümü ve Configuration Manager site sürümü arasındaki farklılıklar, veri sorunlarına yol açabilir. En son ürün sürümünde kullanılabilen bazı özellikler konsolunda kullanılamayacak.

Site sürümüyle eşleşmeyen bir sürümle konsolu kullanırken bir siteyi yönetmek desteklenmez. Bunun yapılması, veri kaybına neden olabilir ve sitenizi riske koyabilirler. Örneğin, sürüm 1606 ' den çalışan bir siteyi yönetmek için sürüm 1610 ' den bir konsol kullanılması desteklenmez.
