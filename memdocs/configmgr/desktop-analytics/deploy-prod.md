---
title: Üretime dağıtma
titleSuffix: Configuration Manager
description: Bir masaüstü Analizi üretim grubuna dağıtmaya yönelik nasıl yapılır Kılavuzu.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0a7ffe8eea1048e696ce7dd254d58364226efc58
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268802"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Masaüstü analizi ile üretime dağıtım

[Pilot 'a dağıtıldıktan](deploy-pilot.md) ve varlıklarınızın durumunu inceledikten sonra üretim ortamınızın geri kalanını güncelleştirmeye hazırsınız demektir.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Güncelleştirmelerin üretim cihazlarına dağıtımını yerine getirmeye yönelik üç ana bölüm vardır:

1. [Yükseltme kararı olması gereken varlıkları gözden geçirin](#bkmk_review): cihazları üretim dağıtımı için hazırlamak için, varlıklarının yükseltme kararının **hazırlık** veya **hazırlık**olarak ayarlanmış olması gerekir.  

2. [Kullanıma hazırlamış cihazlara dağıtın](#bkmk_deploy): kullanıma yönelik olan cihazları güncelleştirmek için Configuration Manager kullanın. Masaüstü analizi, üretim dağıtımı için hazırlanma cihazlarının listesini ve dağıtımın başarısını izlemeye yönelik raporları sağlar.  

3. [Güncelleştirilmiş cihazların sistem durumunu izleyin](#bkmk_monitor): güncelleştirme dağıtımı ilerledikçe, önemli varlıkların sistem durumunu izleyin. Dikkat etmeniz gerekiyorsa, bu sorunları giderin ve çözün. Sorunların düzeltilmeyeceğine karar verirseniz, yükseltme kararlarını ' ı ' a ayarlayarak etkilenen cihazlara dağıtımı **durdurun.**  

> [!NOTE]  
> Pilot dağıtım başarısından emin olduğunuzda, üretim dağıtımını istediğiniz zaman başlatın. Tüm pilot cihazların önce "tamamlandı" durumuna ulaşması gerekmez.  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a>Yükseltme kararı gerektiren varlıkları gözden geçirme

Masaüstü analizi, üretim dağıtımı için varlıklarınızı İnceleme sürecinde size rehberlik eder. Azure portal, **dağıtım planları**' na gidin, bir dağıtım planı seçin ve ardından sol menüden **üretimi hazırla** ' yı seçin.

![Masaüstü analizinden üretim görünümü hazırlama ekran görüntüsü](media/prepare-production.png)

Uygulamalarınızın durumunu gözden geçirin. Bu varlıkların her biri için yükseltme kararı ayarlamak üzere bu bilgileri kullanın.

Uygulamaların durumunu gözden geçirmek için sekmeleri kullanın. Her sekmeli görünümde, yükseltme için izlediğiniz cihazları göstermek, ilgilenmeniz, karma sonuçları olan cihazlar ve bu cihazların belirlenmeyen bir durumda olması için sonuçlara filtre uygulayabilirsiniz.

Aşağıdaki ölçütlere göre, görünümü üretim dağıtımı için olası olan varlıklara filtrelemek için **Toplantı hedeflerini** seçin:

- Risk: Bu varlığın yüklü olduğu cihazları güncelleştirmek için bilinen risklerin ön yükseltme öncesi değerlendirmesi  

- Sistem durumu: diğer dağıtımlardaki cihazların yükseltme sonrası değerlendirmesi ve güncelleştirme yüklendikten sonra sorunlarla karşılaşmaları gerekip gerekmediğini belirtir. Sistem durumu hakkında daha fazla bilgi için bkz. [güncelleştirilmiş cihazların sistem durumunu izleme](#bkmk_monitor).  

Bir varlığı yükseltme için onaylamak için, listeden adı seçin ve ardından **yükseltme kararı** listesinden aşağıdaki seçeneklerden birini seçin:

- İnceleme devam ediyor
- Hazır
- Ready (düzeltme ile)
- Başlatamadı
- Gözden geçirilmedi

Aynı anda birden çok uygulama için bu değeri ayarlamak üzere, **Bu öğeyi seçmek**için ilk sütunu kullanın ve ardından **yükseltme kararı ayarla**' yı seçin.

![Birden çok uygulama üzerinde yükseltme karar seçeneğini ayarla](media/prep-prod-set-upgrade-decision.png)

Sınıflandırılmayan varlıkları görüntülemek için **veri yok** ' u seçin. Bu varlıklar genellikle, masaüstü analizinin risk veya sistem durumu analizini yapması için yeterli kapsama sahip olmayan varlıklardır. Kapsamı geliştirmek için pilot 'a bu varlıklarla birlikte ek cihazlar ekleyin veya pilot kullanıcılardan bu varlıkları denemesini isteyin.

Ayrıca, **dikkat etmeniz gereken** ya da **karma sonuçlar** durumunda varlıklar da olabilir. Bu varlıklar, bunlar için bir yükseltme kararı vermeden önce ek İnceleme gerektirebilir.

Tüm uygulamaları gözden geçirin. Belirli bir cihazın tüm varlıklar için olumlu bir yükseltme kararı varsa, durumu "üretime hazırlanıyor" olarak değişir. Dağıtım planının ana sayfasındaki geçerli sayısına bkz. üçüncü dağıtım adımını seçin, **dağıtın**.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a>Ready cihazlara dağıtın

Configuration Manager, üretim dağıtımı için bir koleksiyon oluşturmak üzere masaüstü analizinden gelen verileri kullanır. Geleneksel bir dağıtım kullanarak görev sırasını dağıtmayın. Masaüstü analizi ile tümleşik bir dağıtım oluşturmak için aşağıdaki yordamı kullanın:

[Pilot cihazlara](deploy-pilot.md#deploy-to-pilot-devices)dağıtım için önerilen işlemi izlediyseniz, Configuration Manager aşamalı dağıtım hazırlanmaya devam eder. Varlıkları *hazırlık*olarak işaretlediğinizde, masaüstü analizi bu cihazları Configuration Manager ile otomatik olarak eşitler. Bu cihazlar daha sonra üretim koleksiyonuna eklenir. Aşamalı dağıtım ikinci aşamaya taşınırsa, bu üretim cihazları yükseltme dağıtımını alır.

Aşamalı dağıtımı **ikinci aşama dağıtımını el ile başlatmak**için yapılandırdıysanız, bunu bir sonraki aşamaya el ile taşımanız gerekir. Daha fazla bilgi için bkz. [aşamalı dağıtımları yönetme ve izleme](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move).

Pilot koleksiyonuna bir masaüstü analizi ile tümleşik tek dağıtım oluşturduysanız, bu işlemi üretim koleksiyonuna dağıtmak için yinelemeniz gerekir.


### <a name="address-deployment-alerts"></a>Adres dağıtım uyarıları

Pilot dağıtımda olduğu gibi, masaüstü analizi de üretim dağıtımı sırasında ilgilenmeniz gereken herhangi bir sorun olduğunu size önerir. Masaüstü Analizi ' nde dağıtım planına gidin ve sol menüden **dağıtım durumu** ' nu seçin. Dağıtım durumu görünümü aşağıdaki kategorilerdeki cihazları listeler:  

- Başlamadı
- Sürüyor
- Tamamlandı
- Dikkat edilmesi gereken (cihaz adına göre sıralanmış) cihazlar
- Dikkat edilmesi gereken noktalar (sorun türüne göre sıralanmış)

![Masaüstü Analizi üretim dağıtım durumunun ekran görüntüsü](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a>Güncelleştirilmiş cihazların sistem durumunu izleme

**Üretim hazırlama** sayfası, varlıklarınız için yükseltme kararları almanıza yardımcı olmaya odaklanır. Bu sayfa varsayılan olarak henüz **hazır** durumda olmayan varlıkları gösterir. **Durumu izle** sayfasında, **hazırlık**olarak işaretlenen varlıklar da dahil olmak üzere herhangi bir not, bu varlık üzerindeki sistem durumu sorunları gösterilir. Sorunları tespit ederseniz sorunu giderebilir ve düzeltir ya da yükseltme kararını hata olarak **değiştirebilirsiniz.** Yükseltme kararını değiştirdiğinizde bu eylem, bu varlık ile cihazlarda daha sonra yükseltmelere engel olur.

Aşağıdaki sistem durumlarına sahip bu sayfayı varlıklara göre filtreleyin:

| Sistem durumu Filtresi | Açıklama |
|----------------------|-------------|
| **İlgilenilmesi gerekiyor** | (Varsayılan filtre) Masaüstü analizi, söz konusu varlık için bazı sistem durumu ölçümüne istatistiksel olarak önemli bir gerileme algılar
| **Toplantı hedefleri** | Masaüstü analizi, davranışta hiçbir gerileme algılamıyor |
| **Yetersiz veri** | Masaüstü analizlerinin hiçbir önerisi yapması için bu varlıkla ilgili yeterli verileri yok |
| **Veri yok** | Bu varlık için henüz kullanılabilir kullanım verisi yok |

Tüm varlıkların filtrelenmemiş bir görünümünü göstermek için geçerli filtreyi seçin. Bu eylem, bu filtreyi kaldırır.

> [!NOTE]  
> Yetersiz verileri olan varlıkların sayısını azaltmak için, masaüstü analizi, dağıtım planınızda belirtilen hedef Windows sürümüne yükseltilen tüm cihazlarınızdaki varlıkları izler. Bu cihazlar, belirli dağıtım planına dahil olmayanları içerir.  

Varsayılan sıralama düzeni, söz konusu varlıkla bir olaya sahip olan cihazların sayısına göre belirlenir, bu sayede hangi sorunların neden olduğunu hızla görebilirsiniz. Örneğin, **uygulamaları**görüntülerken, **son iki haftada uygulama kilitlenmeleriyle cihazlara**göre sıralanır.

Tüm varlıklar için sistem durumuna bakmak isterseniz, masaüstü analizine yönelik yetersiz veri içeren varlıklar da istatistiksel olarak yapılır, aşağıdaki işlemi kullanın:

1. **Son iki hafta içinde olaylar Içeren cihazlarda** açılan eklentiyi seçin. Yalnızca bazı en az sayıda cihazda olay olan varlıklara ilgi çekici olması için bir filtre ekleyin. Örneğin, 100 **'den büyük** değerler içeren öğeleri gösterin.  

2. **Son iki hafta içinde olaylar içeren% cihazlar** açılan seçimini seçin ve **azalan düzende**sıralamayı seçin.  

    Sonuçta elde edilen görünüm, en yüksek düzeyde olaya sahip olan varlıkları minimum olay sayısına göre gösterir.  

3. Daha fazla ayrıntı edinmek veya yükseltme kararlarını değiştirmek için bir varlık seçin.  

Daha fazla bilgi için bkz. [sistem durumu izleme](health-status-monitoring.md).
