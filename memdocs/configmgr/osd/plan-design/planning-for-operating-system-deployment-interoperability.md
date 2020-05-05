---
title: İşletim sistemi dağıtımı birlikte çalışabilirliği
titleSuffix: Configuration Manager
description: Tek bir hiyerarşideki farklı Configuration Manager siteleri farklı sürümler kullanırken birlikte çalışabilirlik sorunlarını anlayın.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723554"
---
# <a name="plan-for-os-deployment-interoperability"></a>İşletim sistemi dağıtımı birlikte çalışabilirliği için plan

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Tek bir hiyerarşideki farklı Configuration Manager siteleri farklı sürümler kullanırken, bazı Configuration Manager işlevleri kullanılamaz. Genellikle, Configuration Manager yeni sürümünün işlevselliğine, sitelerde veya daha düşük bir sürüm çalıştıran istemcilerden erişilemez. Daha fazla bilgi için bkz. [Configuration Manager farklı sürümleri arasında birlikte çalışabilirlik](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


## <a name="objects"></a>Nesneler

Hiyerarşinizdeki üst düzey siteyi ve hiyerarşinizdeki diğer sitelere yükselttiğinizde aşağıdaki nesneleri göz önünde bulundurun Configuration Manager daha düşük bir sürümle çalışır:  

### <a name="client-installation-package"></a>İstemci yükleme paketi  

- Varsayılan istemci yükleme paketinin kaynağı otomatik olarak yükseltilir. Hiyerarşideki tüm dağıtım noktaları yeni istemci yükleme paketiyle güncelleştirilir. Bu davranış, hiyerarşide daha düşük bir sürümde bulunan sitelerdeki dağıtım noktalarında bile olur.  

- Henüz yeni sürüme yükseltmemiş olan sitelere yeni sürüm istemcileri atayamazsınız. Atama, yönetim noktasında engellenir.  

### <a name="boot-images"></a>Önyükleme görüntüleri  

- En üst düzey siteyi Configuration Manager en son sürümüne yükselttiğinizde, varsayılan önyükleme görüntülerini (x86 ve x64) otomatik olarak güncelleştirir. Güncelleştirme, Windows PE 10 içeren Windows 10 için Windows ADK 'yi kullanır. Varsayılan önyükleme görüntüleriyle ilişkilendirilmiş dosyalar, dosyaların en son Configuration Manager sürümüyle güncelleştirilir. Site özel önyükleme görüntülerini otomatik olarak güncelleştirmez. Eski Windows PE sürümlerini içeren özel önyükleme görüntülerini el ile güncelleştirmeniz gerekir.  

- Site hiyerarşiniz farklı Configuration Manager sürümleriyle siteler içerdiğinde, dinamik medya kullanımını önleyin. Bunun yerine, belirli bir yönetim noktasıyla iletişim kurmak için site tabanlı medyayı kullanın. Tüm siteleri aynı Configuration Manager sürümüne güncelleştirdikten sonra, dinamik medyayı yeniden kullanabilirsiniz.

- En son Configuration Manager önyükleme görüntülerinin özelleştirmelerinizi içerdiğini doğrulayın. Ardından yeni sürüm sitelerindeki tüm dağıtım noktalarını yeni önyükleme görüntülerinin en son sürümüne güncelleştirin.  

### <a name="user-state-migration-tool-usmt"></a>Kullanıcı Durumu Taşıma Aracı (USMT)  

En üst düzey siteyi Configuration Manager en son sürümüne yükselttiğinizde, varsayılan USMT paketini otomatik olarak en son sürüme güncelleştirir. Özel USMT paketlerini otomatik olarak güncelleştirmez. Bu paketleri el ile güncelleştirmeniz gerekir.  

### <a name="new-task-sequence-steps"></a>Yeni görev dizisi adımları  

Yeni görev dizisi adımları düzenli aralıklarla yeni Configuration Manager sürümleriyle tanıtılmıştır. Yeni bir adımla bir görev dizisini eski istemcilere dağıttığınızda görev dizisi adımı başarısız olur. Bir görev dizisini yeni bir adımla dağıtırken, hedef koleksiyondaki istemcilerin yeni sürüme güncelleştirildiğinden emin olun.  

### <a name="os-deployment-media"></a>İşletim sistemi dağıtım medyası  

Site yeni bir sürüme güncelleştirildiği zaman, tüm medyayı yeni Configuration Manager istemci paketiyle güncelleştirin. Bu medya türleri önyüklenebilir, yakalama, önceden hazırlanmış ve tek başına ' i içerir.

### <a name="third-party-extensions-to-os-deployment"></a>İşletim sistemi dağıtımı için üçüncü taraf uzantıları  

İşletim sistemi dağıtımı için üçüncü taraf uzantılarınız olduğunda ve Configuration Manager siteleri veya Configuration Manager istemcileri farklı sürümleriniz varsa, uzantılarla ilgili sorunlar olabilir.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Karma hiyerarşide Configuration Manager sitelerin en son sürümü  

Bir siteyi Configuration Manager en son sürümüne yükselttiğinizde, varsayılan istemci yükleme paketine başvuruda bulunan görev dizileri otomatik olarak en son Configuration Manager istemci sürümünü dağıtmaya başlar.

Özel bir istemci yükleme paketine başvuruda bulunan görev dizileri, özel pakette yer alan istemci sürümünü dağıtmaya devam eder. Özel paketler büyük olasılıkla Configuration Manager istemcisinin önceki bir sürümünü içerir. Görev sırası dağıtım başarısızlıklarını önlemek için, tüm özel istemci yükleme paketlerini en son sürüme güncelleştirin.

Bir görev dizisini özel bir istemci yükleme paketini kullanacak şekilde yapılandırdığınızda, aşağıdaki eylemlerden birini yapın:

- Görev dizisi adımını, istemci yükleme paketinin en son Configuration Manager sürümünü kullanacak şekilde güncelleştirin
- Özel paketi en son Configuration Manager istemci yükleme kaynağını kullanacak şekilde Güncelleştir

> [!IMPORTANT]  
> Daha eski bir Configuration Manager sitesindeki istemcilere en son Configuration Manager istemci yükleme paketine başvuruda bulunan bir görev dizisi dağıtmayın. Daha eski bir Configuration Manager sitesine atanan istemciler en son Configuration Manager istemci sürümüne yükseltildiğinde Configuration Manager, daha eski Configuration Manager sitesine atamayı engeller. Bu istemciler artık hiçbir siteye atanmaz. İstemciyi en son Configuration Manager sitesine el ile atamaz veya istemcinin eski Configuration Manager sürümünü bilgisayara yeniden yükleyene kadar, bu istemciler yönetilmez.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Karma bir hiyerarşide daha eski Configuration Manager sürümleri  

Merkezi Yönetim sitenizi Configuration Manager en son sürümüne yükselttiğinizde, dağıttığınız işletim sistemi dağıtımı görev sıralarının bu istemcileri yönetilmeyen bir durumda bırakmadığınızdan emin olun. Örneğin, henüz Configuration Manager en son sürümüne yükseltmemiş olduğunuz eski bir Configuration Manager sitesine atanmış istemcilere dağıtırsanız.

Configuration Manager sitesinin en son sürümündeki istemcilere dağıtmak için kullandığınız görev dizisinin bir kopyasını oluşturun. Ardından, daha eski bir Configuration Manager sitesindeki istemcilere dağıtabilmek için görev dizisini değiştirin. Görev dizisini, eski Configuration Manager istemci yükleme kaynağını kullanan bir özel istemci yükleme paketine başvuracak şekilde yapılandırın. Daha eski Configuration Manager istemci yükleme kaynağına başvuruda bulunan özel bir istemci yükleme paketiniz yoksa, el ile oluşturun.  

> [!Important]  
> Sürüm 1902 ' den başlayarak, bir paket veya görev dizisini bir istemci sürümüne 5,7730 veya daha önceki bir sürüme dağıtamazsınız. Bu sınırlamaya geçici bir çözüm bulmak için istemciyi daha sonraki bir sürüme yükseltin.<!-- SCCMDocs-pr issue #3493 -->
