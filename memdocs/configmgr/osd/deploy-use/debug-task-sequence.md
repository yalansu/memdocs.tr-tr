---
title: Görev dizisinde hata ayıklama
titleSuffix: Configuration Manager
description: Görev dizisinde sorun gidermek için görev dizisi hata ayıklama aracını kullanın.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66f460b7ba5c870a9ee81d10835ceb9f660cba89
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711038"
---
# <a name="debug-a-task-sequence"></a>Görev dizisinde hata ayıklama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--3612274-->

Sürüm 1906 ' den başlayarak, görev dizisi hata ayıklayıcı yeni bir sorun giderme aracıdır. Bir görev dizisini hata ayıklama modunda küçük bir koleksiyona dağıtırsınız. Sorun giderme ve araştırmaya yardımcı olmak için görev dizisini denetimli bir şekilde adım adım gerçekleştirmenizi sağlar. Hata ayıklayıcı Şu anda görev sırası altyapısı ile aynı cihazda çalışıyor, uzak bir hata ayıklayıcı değil.

> [!Note]  
> Bu Configuration Manager sürümünde, görev sırası hata ayıklayıcı bir ön sürüm özelliğidir. Etkinleştirmek için bkz. [yayın öncesi Özellikler](../../core/servers/manage/pre-release-features.md).  


## <a name="prerequisites"></a>Önkoşullar

- Hedef cihazdaki Configuration Manager istemcisini güncelleştirme

- Hedef cihazda yerel **Yöneticiler** grubundaki bir kullanıcı olarak oturum açın. Hata ayıklayıcı yalnızca Yöneticiler için çalışır.

- En son istemci sürümüne sahip olduğundan emin olmak için görev dizisiyle ilişkili önyükleme görüntüsünü güncelleştirin


## <a name="start-the-tool"></a>Aracı Başlat

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.

1. Bir görev sırası seçin. Şeridin Dağıtım grubunda **Hata Ayıkla**' yı seçin.

    > [!Tip]  
    > Alternatif olarak, **Tsdebugmode** değişkenini görev dizisinin `TRUE` dağıtıldığı bir koleksiyon veya bilgisayar nesnesi üzerinde olarak ayarlayın. Bu değişken kümesine sahip herhangi bir cihaz, kendisine dağıtılan herhangi bir görev dizisini hata ayıklama moduna koyar.

1. Hata ayıklama dağıtımı oluşturun. Dağıtım ayarları, normal bir görev sırası dağıtımıyla aynıdır. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md#process).

    > [!Note]  
    > Hata ayıklama dağıtımı için yalnızca küçük bir koleksiyon seçebilirsiniz. Yalnızca 10 veya daha az üye içeren cihaz koleksiyonlarını görüntüler.

Sürüm 1910 ' den başlayarak, görev dizisi bir hata döndürdüğünde hata ayıklayıcıyı otomatik olarak başlatmak için **Tsdebughatayeni** görev dizisi değişkenini kullanın.<!-- 5012536 --> Daha fazla bilgi için bkz. [görev dizisi değişkenleri-Tsdebughata.](../understand/task-sequence-variables.md#TSDebugOnError)

## <a name="use-the-tool"></a>Aracı kullanma

Görev dizisi cihazda çalıştırıldığında, görev sırası hata ayıklayıcı penceresi aşağıdaki ekran görüntüsüne benzer şekilde açılır:

![Görev sırası hata ayıklayıcısı ekran görüntüsü](media/3612274-tsdebug.png)

Hata ayıklayıcı aşağıdaki denetimleri içerir:

- **Adım**: *geçerli* konumdan yalnızca görev dizisindeki bir sonraki adımı çalıştırın.  

    > [!Note]  
    > Görev sırası hata ayıklama modundayken, bir adım önemli bir hata döndürürse, görev sırası normal olarak başarısız olmaz. Bu davranış, dış değişiklik yaptıktan sonra bir adımı yeniden deneme seçeneği sunar.

- **Çalıştır**: *geçerli* konumdan, görev sırasını normal olarak son, sonraki *kesme* noktası veya bir adım başarısız olursa çalıştırın. Bu eylemi kullanmadan önce, kesme noktalarını **Ayarla** eylemini kullanarak bir kesme noktası ayarladığınızdan emin olun.

- **Geçerli ayarla**: hata ayıklayıcıda bir adım seçin ve ardından **geçerli ayarla**' yı seçin. Bu eylem *geçerli* işaretçiyi bu adıma hareket ettirir. Bu eylem, adımları atlamanızı veya geriye doğru taşımanızı sağlar.  

    > [!Warning]  
    > Hata ayıklayıcı, dizideki geçerli konumu değiştirdiğinizde adımın türünü göz önünde bulundurmaz. Bazı adımlar, daha sonraki adımlarla koşul değerlendirmesi için gereken görev sırası değişkenlerini ayarlayabilir. Çalışma sırası tükendiğine göre bazı adımlar başarısız olabilir veya bir cihaza önemli bir hasar oluşmasına neden olabilir. Bu seçeneği, sizin sorumluluğunuzdadır.  

- **Kesmeyi ayarla**: hata ayıklayıcıda bir adım seçin ve sonra **kesmeyi ayarla**' yı seçin. Bu eylem, hata ayıklayıcıya bir *kesme* noktası ekler. Görev dizisini **çalıştırdığınızda** , bir *kesme*sırasında duraklar.  

    - **Çalıştırma** eylemini kullanmadan önce, kesme noktaları ayarlayın.

    - Sürüm 1910 ' den başlayarak, hata ayıklayıcıda bir kesme noktası oluşturursanız ve ardından görev sırası bilgisayarı yeniden başlattığında, hata ayıklayıcı yeniden başlattıktan sonra kesme noktalarınızı korur.<!-- 5012509 -->

    - Sürüm 1906 ' de, bilgisayar yeniden başlatıldıktan sonra, [Bilgisayarı yeniden Başlat](../understand/task-sequence-steps.md#BKMK_RestartComputer) adımı gibi kesme noktaları kaydedilmez. Örneğin, bir görüntüleme görev sırası için hata ayıklayıcıyı yazılım merkezinden başlatırsanız Windows PE aşamasında kesmeler ayarlamazsanız. Bilgisayar Windows PE 'de yeniden başlatıldığında, hata ayıklayıcı, kesmeler ayarlayabilmeniz için görev dizisini duraklatır.

- **Tüm sonları temizle**: tüm kesme noktalarını kaldır.

- **Günlük dosyası**: [CMTrace](../../core/support/cmtrace.md)ile **Smsts. log**adlı geçerli görev dizisi günlük dosyasını açar. Görev sırası altyapısı "hata ayıklayıcı için bekleniyor" olduğunda günlük girişlerini görebilirsiniz.

- **Cmd Prompt**: Windows PE 'de, bir komut istemi açar.

- **İptal**: hata ayıklayıcıyı kapatın ve görev sırasını başarısız yapın.

- **Çıkış**: hata ayıklayıcıyı ayırın ve kapatın, ancak görev dizisi normal olarak çalışmaya devam eder.

**Görev dizisi değişkenleri** penceresi, görev dizisi ortamındaki tüm değişkenlerin geçerli değerlerini gösterir. Daha fazla bilgi için bkz. [görev dizisi değişkenleri](../understand/task-sequence-variables.md). **Bu değeri gösterme**seçeneği Ile [görev dizisi değişkenini ayarla](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) adımını kullanırsanız, hata ayıklayıcı değişken değerini görüntülemez. Hata ayıklayıcıda değişken değerlerini düzenleyemezsiniz.

> [!Note]
> Bazı görev dizisi değişkenleri yalnızca dahili kullanım içindir ve başvuru belgelerinde listelenmez.

Görev sırası hata ayıklayıcı bir [Bilgisayarı yeniden Başlat](../understand/task-sequence-steps.md#BKMK_RestartComputer) adımından sonra çalışmaya devam eder, ancak herhangi bir kesme noktası oluşturmanız gerekir. Hata ayıklayıcı Kullanıcı etkileşimi gerektirdiğinden görev sırası gerektirmese de, devam etmek için Windows 'da oturum açmanız gerekir. Hata ayıklamaya devam etmek için bir saatten sonra oturum açmanız gerekmiyorsa, görev sırası başarısız olur.

Ayrıca [görev dizisi Çalıştır](../understand/task-sequence-steps.md#child-task-sequence) adımını içeren bir alt görev sırası için de adım adım. Hata ayıklayıcı penceresinde, ana görev dizisinin birlikte alt görev dizisinin adımları gösterilir.


## <a name="known-issues"></a>Bilinen sorunlar

Aynı cihaza birden çok dağıtım aracılığıyla hem normal dağıtım hem de hata ayıklama dağıtımı hedefliyorsanız, görev sırası hata ayıklayıcı başlatılamayabilir.


## <a name="see-also"></a>Ayrıca bkz.

- [Görev dizisi adımları hakkında](../understand/task-sequence-steps.md)
- [Görev dizisi değişkenleri](../understand/task-sequence-variables.md)
- [Görev dizisi değişkenlerini kullanma](../understand/using-task-sequence-variables.md)
- [Görev dizisini dağıtma](deploy-a-task-sequence.md)
