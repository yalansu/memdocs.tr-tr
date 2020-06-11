---
title: En iyi koleksiyonlar uygulamaları
titleSuffix: Configuration Manager
description: Configuration Manager içinde koleksiyonları ve koleksiyon değerlendirmesini yapılandırmaya yönelik öneriler alın.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ee640a70eea9f2e8470e852409911d28e542bc2
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663391"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Configuration Manager içindeki koleksiyonlar için en iyi yöntemler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bazı koleksiyon yönetim kılavuzları çelişkili olabilir. Örneğin, performans nedenleriyle, sık güncelleştiren koleksiyonların sayısını sınırlamanız gerekir. Ancak, çoğu Configuration Manager işlevselliği koleksiyonlara bağlı olduğundan, koleksiyonları sık sık güncelleştirmek kullanışlıdır. Koleksiyonlar ve koleksiyon değerlendirmesi tasarlarken ve yapılandırdığınızda hem performans etkilerini hem de iş gereksinimlerini dikkatle göz önünde bulundurun.

Configuration Manager içindeki koleksiyonlar için aşağıdaki en iyi yöntemleri kullanın.  

## <a name="configure-maintenance-window-for-updates"></a>Güncelleştirmeler için bakım penceresini yapılandırma

Cihaz Koleksiyonları için bakım pencerelerini, Configuration Manager bu cihazlara yazılım yükleyebileceği zamanları kısıtlamak üzere yapılandırabilirsiniz. Bakım penceresini çok küçük olacak şekilde yapılandırırsanız, istemci kritik yazılım güncelleştirmelerini yükleyemeyebilir, bu da istemciyi güncelleştirmenin güvenlik altına aldığı sorunlara karşı savunmasız bırakır.

Bakım pencerelerini planlarken göz önünde bulundurmanız gereken önemli noktalar:

- Varsayılan yazılım güncelleştirmesi en fazla çalışma süresi 60 dakikadır.
- Configuration Manager bir güncelleştirmenin yüklenip yüklenmediğini hesapladığında, yeniden başlatma için en fazla çalışma zamanına beş dakika ekler.
- Bakım penceresinin kalan süresi, yazılım güncelleştirmesinin en uzun çalışma zamanından ve beş dakikadan uzun olmalıdır.

## <a name="avoid-frequent-collection-evaluation"></a>Sık koleksiyon değerlendirmesinden kaçının

Tam koleksiyon değerlendirmesi yalnızca hedeflenen koleksiyonu değil, bir güncelleştirme gerçekleşirse koleksiyonun sınırlarını sınırlayan tüm koleksiyonları da değerlendirir. Ayrıca, zamanlaması olmayan bir koleksiyon, sınırlayan koleksiyon güncellemeleri hala değerlendirilir. Bu nedenle, bazı koleksiyonlar beklediğinizden daha sık değerlendirilebileceğinden mümkündür.

Yoğun bir Configuration Manager ortamında, yinelenen koleksiyon değerlendirmelerini önlemek için arka zamanlamaları ölçeklendirerek koleksiyon değerlendirme performansını geliştirebilirsiniz. Ayrıntılı bir ağaçta, Koleksiyonlar ağaçta daha derin bir şekilde daha derin bir şekilde azaltılacağı için koleksiyon değerlendirme sıklığını azaltabilirsiniz, çünkü daha yüksek düzeyde koleksiyon değerlendirmeleri de alt düzey koleksiyon değerlendirmelerini tetikler.

## <a name="understand-the-collection-evaluation-graph"></a>Koleksiyon değerlendirme grafiğini anlayın

Uygun bir koleksiyon yapısını tasarlayabilmeniz için koleksiyon değerlendirme grafiğinin nasıl çalıştığını unutmayın. Tüm koleksiyonları her zaman güncelleştirmek için tam koleksiyon değerlendirmesine güvenmeyin. Bir zamanlamaya göre artımlı olarak güncelleştirilmiş bir koleksiyon güncelleştirmesi varsa, artımlı güncelleştirmeler için etkinleştirilmemiş koleksiyonlara başvuru güncelleştirilemeyebilir. Artımlı değerlendirme sırasında sık karşılaşılan güncelleştirmeler olduğundan, tam bir değerlendirme koleksiyonu güncelleştiremeyebilir ve bu döngüyle ilgili koleksiyon değerlendirme grafı sona eriyor. Bu durumda, başvuran bir koleksiyon değerlendirmesi gerçekleşmez. Daha fazla bilgi için bkz. [koleksiyon değerlendirme grafiği](collection-evaluation.md#collection-evaluation-graph).

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a>Artımlı güncelleştirmeleri sınırla

Birçok koleksiyon için artımlı güncelleştirmelerin etkinleştirilmesi değerlendirme gecikmelerine neden olabilir. Artımlı olarak güncellenen koleksiyonların sayısını 200 olarak sınırlamak en iyisidir. Tam sayı şunlara bağlıdır:

- Toplam koleksiyon sayısı
- Hiyerarşiye yeni kaynak eklenme ve kaynakların değiştirilme sıklığı
- Bir hiyerarşideki istemci sayısı
- Bir hiyerarşideki koleksiyon üyeliği kurallarının karmaşıklığı

Artımlı değerlendirme döngüsünün yapılandırılmış güncelleştirme sıklığından daha uzun sürmesi durumunda Configuration Manager, sistem performansını etkileyebilecek koleksiyon değerlendirmelerinin sürekli olarak işlenmesine devam edilir. Artımlı olarak güncellenen koleksiyonların sayısını azaltın veya artımlı değerlendirme döngüleri arasındaki süreyi artırın.

Artımlı koleksiyonların olası etkileri verildiğinde, koleksiyonları oluşturmaya ve güncelleştirme zamanlamaları atamaya yönelik bir ilke veya yordam olması önemlidir. İlke değerlendirmeleri örnekleri şunlar olabilir:

- Yalnızca güvenlik kapsamı, istemci ayarları ve bakım pencereleri için kullanılan koleksiyonlar için Artımlı güncelleştirmeleri kullanın. Bu koleksiyon güncelleştirmeleri, istemci davranışını ve kaynaklara erişimi etkiler.
- Lisanslama onayı olmayan uygulamalar için, uygulamaları var olan koleksiyonlara duyurun ve kullanılabilirliği kısıtlamak için genel koşulları kullanın.
- Tam koleksiyon güncelleştirmeleri zamanlanmış diğer koleksiyonlar için uygun dönemler ana hattı.

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>CA 'lardan büyük ağaçların değerlendirilmesinden kaçının

Configuration Manager ortamında, merkezi yönetim sitesi (CAS) koleksiyon üyeliğini değerlendirmez. Birincil siteler, koleksiyonları değerlendiren tek sitelerdir. İkincil siteler yalnızca birincil sitelerinden çoğaltılan verileri kullanan proxy 'ler gibi davranır.

CA 'LAR bir koleksiyon güncelleştirmesi istemek için her birincil siteye bir istek gönderir. Birincil siteler koleksiyonu değerlendirir ve sonuçları CA 'lara geri gönderir. Koleksiyon değerlendirme sonuçları yalnızca tüm koleksiyon değerlendirme yönergeleri tüm sitelere çoğaltıldıktan sonra görünür, tüm siteler tüm koleksiyonları değerlendirir ve tüm veriler CA 'lara döner ve birleştirir.

Aşağıdaki diyagramda, CAS el ile bir koleksiyon güncelleştirmesi istediğinde akış gösterilmektedir:

![CA 'lardan el ile koleksiyon güncelleştirmesi](media/manual-collection-update-from-cas.png)

Birden çok birincil siteye sahip bir CA 'dan bir koleksiyon güncelleştirmesi zaman alan olabilir. Bir koleksiyon zamanında değerlendirilemez, isteği yinelemek de mümkündür.

Bir koleksiyon değerlendirme iş parçacığı başladıktan ve değerlendirme grafiğini yükledikten sonra, değerlendirme, koleksiyon değerlendirme grafı boş olana kadar devam eder. Daha sonra iş parçacığı sonlanır ve sonraki değerlendirme için kullanılabilir hale gelir. Ancak, iş parçacığı koleksiyonları değerlendirirken başka bir koleksiyon değerlendirme döngüsünü sıraya alıyorsa, "unutulan" döngüsünün değerlendirilmesini denemek için iş parçacığı hemen yeniden başlatılır.

Her değerlendirme yöntemi kendi iş parçacığında çalışır. İş parçacığı içinde, Configuration Manager aynı koleksiyonu birden çok kez grafik oluşturmaya çalışmayabilir. Configuration Manager sonra ikinci ve sonraki istekleri bırakır.

Bu senaryolara engel olmak için, özellikle birden çok site içeren CA 'lardan çalışırken büyük ağaçların el ile toplanmasının önüne geçin.

## <a name="consider-collection-depth-and-cross-referencing"></a>Koleksiyon derinliğini ve çapraz başvuruyu göz önünde bulundurun

İş gereksinimleri ve performans arasındaki dengeyi oluşturmak için oluşturduğunuz koleksiyon yapısını ve diğer koleksiyonlardaki bağımlılıklarını anlamanız önemlidir. Aynı zamanda diğer koleksiyonlara başvuran bir veya daha fazla koleksiyona başvuruda bulunan kurallara sahip bir koleksiyon oluşturursanız, bu koleksiyonların hepsi koleksiyonun üyeliğini oluşturacak şekilde değerlendirilir.

Configuration Manager dahil etme ve hariç tutma kuralları, başvuran koleksiyonları özel bir WQL sorgusu yazmadan daha kolay hale getirir. Bununla birlikte, dahil etme ve hariç tutma koleksiyonları kullanmak yüksek performanslı bir performans elde eder, bunun yerine WQL sorgu yöntemini kullanabilirsiniz:

İçeriyor

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

Amaz

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>Toplama değerlendirmesini izlemek için CEViewer 'ı kullanma

[Koleksiyon değerlendirme Görüntüleyicisi 'ni (CEViewer)](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer) kullanarak kaç koleksiyonun değerlendirileceğini ve her koleksiyonun ne kadar süre güncelleyeceğinizi izleyebilirsiniz. CEViewer *CD 'de. Site sunucusundaki en son* klasör.

SQL ile benzer bir denetimi el ile gerçekleştirmek için aşağıdaki sorguyu kullanabilirsiniz:

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```


