---
title: Koleksiyon değerlendirme
titleSuffix: Configuration Manager
description: Koleksiyon değerlendirme işlemi, türleri ve Tetikleyicileri hakkında bilgi edinin. Koleksiyon değerlendirme grafiğini ve hiyerarşisini anlayın.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15b58b841ca87cf2b5e04c98dfd35c487c941e78
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693327"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Configuration Manager içinde koleksiyon değerlendirmesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, tanımladığınız toplama kurallarına göre koleksiyon üyeliğini güncelleştirmek için *koleksiyon değerlendirmesi* kullanır. Koleksiyon değerlendirme kapsamı ve zamanlaması, site ve koleksiyon yapılandırmasına ve değerlendirme türüne göre farklılık gösterir. 

Uygun koleksiyon tasarımı kararları almak için, koleksiyon değerlendirme davranışının anlaşılması önemlidir. Koleksiyon değerlendirme kılavuzu ve önerileri için bkz. [koleksiyonlar Için en iyi uygulamalar](best-practices-for-collections.md).

## <a name="evaluation-process"></a>Değerlendirme işlemi

Koleksiyon Değerlendiricisi koleksiyonları oluşturduğunda, değiştirdiğinde ve sildiğinde, [Colleval. log kayıtları kaydedilir](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs) .

Yüksek düzeyde, her bir koleksiyon değerlendirmesi ve güncelleştirmesi şu adımları izler:

![Üst düzey koleksiyon güncelleştirme işlemi](media/high-level-collection-update-process.png)

1. Koleksiyon sorgusunu yürütün.
1. Doğrudan üye olan tüm sistemleri ekleyin.
1. Tüm *dahil etme* koleksiyonlarını değerlendirin.
   
   Dahil etme koleksiyonlarının sorgu kuralları da varsa veya koleksiyonları dahil etme veya hariç tutma varsa, bunları da değerlendirin. Dahil edilen koleksiyonlar koleksiyonları sınırlandırırken, altındaki tüm koleksiyonları değerlendirin. Ağaç tamamen hesaplandıktan sonra, sonuçları çağıran koleksiyona döndürün.
   
1. `AND`Döndürülen sonuçlar ve sınırlandırma koleksiyonu arasında bir mantıksal durum gerçekleştirin.
1. *Dışlanan* koleksiyonları değerlendirin.
   
   Hariç tutma koleksiyonlarının sorgu kuralları da varsa veya koleksiyonları dahil etme veya hariç tutma varsa, bunları da değerlendirin. Bu koleksiyonların kendilerine ait koleksiyonları kısıtladıysanız, bunların altındaki tüm koleksiyonları değerlendirin. Ağaç tamamen hesaplandıktan sonra, sonuçları çağıran koleksiyona döndürün.
   
1. Sonuç kümesini doğrudan üyeleri değerlendirmeden karşılaştırın ve koleksiyonları, hariç tutma koleksiyonlarının değerlendirmesi sonuçlarıyla birlikte ekleyin.
1. Değişiklikleri veritabanına yazın ve güncelleştirmeleri gerçekleştirin.
1. Tüm bağımlı koleksiyonları da güncelleştirmek için tetikleyin. Bağımlı koleksiyonlar, geçerli koleksiyonun limitlerinin veya INCLUDE veya exclude kuralları kullanılarak geçerli koleksiyona başvuran koleksiyonlardır.

## <a name="collection-evaluation-types-and-triggers"></a>Koleksiyon değerlendirme türleri ve Tetikleyicileri

Bu iş parçacığı türleri, değerlendirme türüne bağlı olarak koleksiyon değerlendirmesini işler:

- Zamanlanan koleksiyon güncelleştirmeleri için **birincil**
- Bağımlı koleksiyonlarla koleksiyonları el ile güncelleştirmek için **yardımcı**
- Bağımlı koleksiyonlar olmadan koleksiyonları el ile güncelleştirmek için **tek**
- Artımlı koleksiyon güncelleştirmeleri için **Express**

Aşağıdaki tabloda, koleksiyon değerlendirme Tetikleyicileri ve bunlara karşılık gelen değerlendirme türleri açıklanmaktadır. 

| Tetikleyici | Değerlendirme türü | Açıklama |
|---------|-----------------|-------------|
|El ile|Tek veya yardımcı|El ile en yüksek öncelikli koleksiyon değerlendirmesi. Yönetici el ile toplama değerlendirmesi istediğinde, koleksiyon Değerlendiricisi bir sonraki kullanılabilir değerlendirme iş parçacığını değerlendirmeye atar.|
|Zamanlanan|Birincil|Zamanlanan değerlendirme işlemi, değerlendirme, olay odaklı yerine zaman odaklı olması dışında, el ile değerlendirmesiyle aynıdır.|
|Hazırlama|Tek veya yardımcı|Tüm Koleksiyonlar doğrudan veya dolaylı olarak tüm **sistemlere** veya **tüm kullanıcılara ve Kullanıcı gruplarına**bağımlıdır. Bu koleksiyonların her ikisi de günde 4:00 ' de tam bir toplama değerlendirmesi yapılır. Bu koleksiyonlardan birine yapılan bir değişiklik, bağımlı koleksiyonların güncelleştirmelerini [tam bir koleksiyon grafiğine](#collection-evaluation-graph)göre tetikler.
|Artımlı|Express|Artımlı değerlendirme, artımlı koleksiyon üyeliğine yönelik bir güncelleştirme değişirse bağımlı koleksiyonları değerlendirmek ve güncelleştirmek için bir koleksiyon değerlendirme grafiği kullanır. Configuration Manager, artımlı güncelleştirmeler için yapılandırılmış tüm koleksiyonlardaki kaynak nesnelerini izler ve güncelleştirir.<br /><br />Bir koleksiyon sorgusu, donanım envanteri gibi daha sonra güncelleştirilecek bilgileri temel alıyorsa, Configuration Manager zamanlanan koleksiyon güncelleştirmesi sırasında kaynağı yalnızca koleksiyondan ekler veya kaldırır.|

## <a name="collection-evaluation-graph"></a>Koleksiyon değerlendirme grafiği

*Koleksiyon değerlendirme grafiği* , değerlendirme için hedeflenen koleksiyonla ilgili tüm koleksiyonları eşler. Koleksiyon değerlendirmesi, koleksiyon değerlendirme grafiğinde hedeflenen koleksiyonu ve ilgili koleksiyonları içerir.

Koleksiyon değerlendirmesi başladığında Configuration Manager, hedefteki en yüksek düzeyden başlayarak, hedef koleksiyondaki değişikliklerin sonucu olarak değerlendirilmesi gerekebilecek tüm koleksiyonları içeren bir grafik oluşturur. Daha sonra koleksiyon Değerlendiricisi, her koleksiyon üyeliğini sırayla değerlendirmek için sırasıyla grafiğe gider. Koleksiyon tam olarak değerlendirildikten sonra, koleksiyon Değerlendiricisi Bu döngüden etkilenmeyen alt düzey koleksiyonları koleksiyon değerlendirme grafiğinden kaldırır.

Değerlendirilen bir veya daha fazla koleksiyonun içerme veya dışlama kuralı varsa, koleksiyon Değerlendiricisi dahil edilen veya dışlanan koleksiyonu, koleksiyon limitlerinin bulunduğu tüm koleksiyonlarla birlikte grafiğe ekler. Dahil etme ve hariç tutma koleksiyonları değerlendirmesi sırasında herhangi bir değişiklik varsa, grafik Ana dala dönüşmeden önce o dalda devam eder.

Configuration Manager, *artımlı* veya *tam*olmak üzere iki tür değerlendirme grafiği oluşturur.

### <a name="incremental-collection-evaluation"></a>Artımlı koleksiyon değerlendirmesi

Tablo verileri değiştiğinde, bir SQL tetikleyicisi **Collectionnotifications** tablosuna bir satır ekler. Bir koleksiyon değerlendirme zamanlaması tetiklendiğinde, `AND` kaynak kimliği var olan koleksiyon sorgusuna göre oluşturulur ve *artımlı* koleksiyonlar için etkinleştirilen koleksiyonlardaki güncelleştirmeleri tetikler.

Artımlı koleksiyon değerlendirmesi makine başına bir sorgu yürütür. Artımlı koleksiyon değerlendirmesi için varsayılan site yapılandırması her beş dakikada bir olur.

Artımlı koleksiyon değerlendirme grafiği, başvurulan koleksiyonları yalnızca artımlı değerlendirme için etkinleştirildiklerinde eşler. Artımlı değerlendirme, artımlı değerlendirme için etkinleştirilmemiş bir koleksiyonla sınırlı ise, grafik, sınırlandırılan koleksiyonun mevcut üyeliklerine göre koleksiyonu değerlendirir. 

Örneğin, aşağıdaki diyagramda tüm koleksiyonlar için geçerli olan yeni keşfedilen kaynaklar gösterilmektedir. Ancak, koleksiyon değerlendirmesi yalnızca **tüm sunucuları** ve **tüm etki alanı denetleyicileri** koleksiyonlarını güncelleştirir. **Tüm üye sunucular** koleksiyonu artımlı değerlendirme için etkinleştirilmediğinden, koleksiyon Değerlendiricisi diğer koleksiyonları değerlendirmez.

![Artımlı koleksiyon değerlendirme grafiği örneği](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>Tam koleksiyon değerlendirmesi

El ile veya zamanlanmış koleksiyon değerlendirmeleri, tüm bağımlı koleksiyonların *tam* bir koleksiyon değerlendirme grafiği oluşturur. Grafik, güncelleştirilen ve sonraki koleksiyonları içeren koleksiyona başvuran tüm koleksiyonları içerir. Configuration Manager, işlenen koleksiyonlara yönelik güncelleştirmeler olduğu sürece grafiği değerlendirmeye devam eder.

Aşağıdaki diyagramda **tüm sunucular** koleksiyonu için zamanlanan veya el ile yapılan bir koleksiyon Güncelleştirme isteğinin tüm ilgili koleksiyonları içeren tam bir grafik nasıl oluşturulduğu gösterilmektedir. Yeni DNS sunucusu ve etki alanı denetleyicisi kaynakları tüm koleksiyonların üyelik sorgularının kapsamındadır, bu nedenle tüm koleksiyonlar güncelleştirilir.

![Tam koleksiyon değerlendirme grafiği örnek 1](media/full-collection-evaluation-graph-1.png)

Tam değerlendirme her zaman tüm koleksiyonları değerlendirmez. Koleksiyon değerlendirme grafiği yalnızca geçerli başvurulan koleksiyonda bir güncelleştirme gerçekleşirse bağımlı koleksiyonları değerlendirmeye devam eder. Zamanlanmış artımlı değerlendirmeler sırasında artımlı olarak güncelleştirilmiş bir koleksiyon güncelleştirmesi varsa, artımlı güncelleştirmeler için etkinleştirilmemiş koleksiyonlara başvuru güncelleştirilemeyebilir. Tam değerlendirme, koleksiyon değerlendirme grafiğini ve bu döngüyle ilgili tüm başvuru toplama değerlendirmelerini izleyen koleksiyonu güncelleştirmez. 

Aşağıdaki örnekte, var olan sunucuya DNS yükleme, **DNS sunucuları** koleksiyonunun bir üyesi haline gelir, ancak **tüm üye sunucular** koleksiyonunu sınırlayan bir güncelleştirme olmadığından, tam değerlendirme **DNS sunucuları** koleksiyonunu değerlendirmez. Bir sonraki artımlı değerlendirme döngüsünün, artımlı bir koleksiyon olduğundan, **DNS sunucuları** koleksiyonunu değerlendirmesi gerekir.

![Tam koleksiyon değerlendirme grafiği örneği 2](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>Sonraki adımlar
- [Koleksiyon oluşturma](create-collections.md)
- [Koleksiyonlar için en iyi yöntemler](best-practices-for-collections.md)
- [Koleksiyon Değerlendirme Görüntüleyicisi](../../../support/ceviewer.md)
- [Configmgrdogs TechEd Avustralya 'Da ConfigMgr 2012 oturumunda sorun giderme](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411)