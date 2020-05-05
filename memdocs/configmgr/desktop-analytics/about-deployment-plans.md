---
title: Masaüstü analizinden dağıtım planları
titleSuffix: Configuration Manager
description: Masaüstü analizinden dağıtım planları hakkında bilgi edinin.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c14eb9127b096f7fc4e4680735867913ea877f54
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722539"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Masaüstü analizinden dağıtım planları hakkında

Masaüstü analizi, kuruluşunuzdaki cihaz, uygulama ve sürücü verilerini toplayıp analiz eder. Bu Analize ve girişinizi temel alarak, Windows 10 için dağıtım planları oluşturmak üzere hizmeti kullanabilirsiniz. Dağıtım planları aşağıdaki özelliklere sahiptir:  

- Pilotlar 'ye hangi cihazların ekleneceğini otomatik olarak öner  

- Uyumluluk sorunlarını belirleyip azaltmaları önerin  

- Güncelleştirmelerden önce, sırasında ve sonrasında dağıtımın sistem durumunu değerlendirin  

- Dağıtımınızın ilerlemesini izleme  

Dağıtım planınızın bir parçası olarak, aşağıdaki işlemleri yapabilirsiniz:  

- Hangi Windows 10 sürümlerini dağıtmak istediğinizi tanımlayın  

- Dağıtmak istediğiniz cihaz gruplarını seçin  

- Dağıtım için hazırlık kuralları oluşturma  

- Uygulamalarınızın önemini tanımlama  

- Otomatik önerilere göre pilot cihazları seçin  

- Masaüstü analizinden öneriler temelinde uygulamalarla ilgili sorunları nasıl giderecağınıza karar verme  

Varsayılan olarak, masaüstü Analizi dağıtım planı verilerini günlük olarak yeniler. Bir uygulama için önemli atama ya da pilot 'a eklenecek bir cihaz seçme gibi bir dağıtım planında yaptığınız tüm değişiklikler, işlenmesi 24 saate kadar sürer. Bu işlemi hızlandırmak için isteğe bağlı veri yenileme isteyin. Daha fazla bilgi için bkz. [Masaüstü analizi hakkında SSS](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Masaüstü analizlerini Configuration Manager 'e bağladıktan sonra dağıtım planlarındaki koleksiyonlarınızı seçin. Bu tümleştirme daha sonra Windows 'u masaüstü Analizi verilerine göre bir koleksiyona dağıtmanıza olanak tanır.



## <a name="readiness-rules"></a>Hazırlık kuralları

Aşağıdaki hazırlık kuralları dağıtım planlarında kullanılabilir:

- Cihazlarınızın Windows Update otomatik olarak sürücü alıp almamayacağı. Cihazlar Windows Update sürücü güncelleştirmelerini alıyorsa, hazırlık değerlendirmesinin bir parçası olarak tanımlanan tüm sürücü sorunları otomatik olarak **hazır**olarak işaretlenir.  

- Windows uygulamalarınız için düşük yüklemesi sayısı eşiği. Bir uygulama bu eşikten daha yüksek bir bilgisayar yüzdesine yüklenirse, dağıtım planı uygulamayı en **önemli şekilde işaretler**. Bu etiket, pilot aşamada uygulamanın ne kadar önemli olduğuna karar vermenize olanak sağlar.  


## <a name="plan-assets"></a>Varlıkları planla

<!-- 4670224 -->

[Varlıklar](about-assets.md) alanı Ayrıca cihazları ve uygulamaları gösterirken, belirli bir dağıtım planı altındaki **plan varlıkları** alanı ek bilgiler içerir.

### <a name="devices"></a>Cihazlar

Dağıtım planındaki her bir cihaz için **Windows yükseltme kararına** bakın.

**Cihazın yerini alacak** Windows yükseltme kararı aşağıdaki nedenlerden biri olabilir:

- Windows 10 gerekli bir işlemci denetiminde başarısız oldu. Daha fazla bilgi için bkz. [En düşük donanım gereksinimleri](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- BIOS bloğu vardır
- Yeterli belleğe sahip değil
- Sistemdeki bir önyükleme kritik bileşeni engellenmiş bir sürücüye sahip
- Belirli bir marka ve model yükseltilemiyor
- Aşağıdaki özniteliklere sahip bir sürücü bloğuna sahip bir görüntüleme sınıfı bileşeni vardır:
    - Geçersiz kılmazsınız
    - Yeni işletim sistemi sürümünde sürücü yok
    - Zaten açık Windows Update
- Sistemde yükseltmeyi engelleyen başka bir eklenti ve yürütme bileşeni var
- XP ile öykünülmüş bir sürücü kullanan bir kablosuz bileşen var
- Etkin bağlantısı olan bir ağ bileşeni, sürücüsünü kaybeder. Diğer bir deyişle, yükseltmeden sonra ağ bağlantısı kaybolabilir.

**Yeniden yüklemeye** yönelik Windows yükseltme kararı, yükseltmenin yerinde yükseltmenin aksine yeniden yükleme gerektireceğini gösterir. 

**Engellenen** bir Windows yükseltme kararı aşağıdaki nedenlerden kaynaklanıyor olabilir:

- Bir veya daha fazla **varlık için yükseltme**kararını bir veya daha fazla varlık olarak ayarlarsınız.

- Bu cihaz için envanter verileri eksik ve Masaüstü Analizi tam uyumluluk değerlendirmesi yapamıyor.

### <a name="apps"></a>Uygulamalar

Bu dağıtım planında bu uygulamanın **yükseltme kararlarını** ve **önemini** ayarlayın. Daha fazla bilgi için bkz. [dağıtım planları oluşturma](create-deployment-plans.md).

Uygulamanın ayrıntılarında aşağıdaki bilgileri de görebilirsiniz: öneriler, uyumluluk riski faktörleri ve Microsoft 'un bilinen sorunları. **Yükseltme kararlarını**ayarlamaya yardımcı olması için bu bilgileri kullanın. Daha fazla bilgi için bkz. [Uyumluluk değerlendirmesi](compat-assessment.md).

Masaüstü analizinin, dağıtım planının hazırlık kuralları için düşük kurulum sayısı eşiğine göre *gösterildiği gibi gösterdiği* uygulamalar. Daha fazla bilgi için bkz. [hazırlık kuralları](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > "Önemli değil" uygulama kategorisi hakkında daha fazla bilgi için bkz. [sistem ve Mağaza uygulamalarının otomatik yükseltme kararı](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->


### <a name="drivers"></a>Sürücüler

Bu dağıtım planına dahil edilen sürücü listesine bakın. **Yükseltme kararlarını**ayarlayın, Microsoft 'un önerisini inceleyin ve uyumluluk risk faktörleri ' ne bakın.


## <a name="importance"></a>Önem

Dağıtım planının bir parçası olarak, uygulamaların *önemini* ayarlayın. Masaüstü analizi, bu uygulamaları hedef cihazlarda yüklü olarak algılar. Bu ayar, masaüstü analizinin dağıtımın pilot aşamasında hangi cihazlara dahil olduğunu belirlemesine yardımcı olur.

Bir uygulama, hedeflenen cihazların %2 ' den daha düşük bir sürümüne yüklenmişse, bu, **düşük yükleme sayısı**olarak işaretlenir. Varsayılan değer yüzde iki değeridir. Hazırlık ayarlarındaki eşiği %0 ile %10 arasında bir şekilde ayarlayabilirsiniz. Masaüstü analizi, bu uygulamaları otomatik olarak **yükseltmeye hazırlamak üzere**işaretler.  

Uygulamalar için **kritik**, **önemli**veya **önemli**bir önem derecesi seçin. Bir tane kritik veya önemli olarak işaretlerseniz, masaüstü analizine bu uygulamayla birlikte pilot dağıtımı dahildir. Hizmet, kritik bir uygulamanın pilot daha fazla örneğine dahildir. Bir uygulamayı önemli değil olarak işaretlerseniz, masaüstü Analizi otomatik olarak **yükseltme Için hazırlık**yapar.



## <a name="pilot-devices"></a>Pilot cihazlar

Masaüstü analizi, önemli bilgilerinizi küresel pilot ayarlarıyla birleştirir. Daha sonra, hangi cihazların pilot dağıtım kapsamında olması gerektiğine yönelik bir öneri oluşturur. Önerilen pilot dağıtım, farklı donanım yapılandırmalarına sahip olan cihazları ve tüm kritik ve önemli uygulamaların bir veya daha fazla örneğini içerir. Bir uygulama kritik olarak işaretlenmişse, hizmet pilot ortamında bu uygulamayla daha fazla cihaz önerir.



## <a name="deployment-plans-in-configuration-manager"></a>Configuration Manager 'de dağıtım planları

Bir dağıtım planı oluşturduktan sonra, ürünleri dağıtmak için Configuration Manager kullanın. Dağıtım başladıktan sonra, masaüstü Analizi plandaki ayarları temel alarak dağıtımı izler.


## <a name="next-steps"></a>Sonraki adımlar

- [Masaüstü Analizi varlıkları hakkında bilgi edinin](about-assets.md): cihazlar, sürücüler ve uygulamalar  

- [Güvenlik ve özellik güncelleştirmeleri hakkında bilgi edinin](about-updates.md)  

- [Dağıtım planı oluşturma](create-deployment-plans.md)  
