---
title: Pilot 'a dağıtım
titleSuffix: Configuration Manager
description: Bir masaüstü Analizi pilot grubuna dağıtmaya yönelik nasıl yapılır Kılavuzu.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 3aa722415248ad9275c6ad065f0120bfe78d3ce4
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311229"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Masaüstü analiziyle pilot 'a dağıtım

Masaüstü analizinin avantajlarından biri, en geniş çarpanların kapsamını sağlayan en küçük cihaz kümesini belirlemenize yardımcı olmak için kullanılır. Windows yükseltmelerinde ve güncelleştirmelerinde yapılan bir pilot için en önemli etkenlere odaklanır. Pilot uygulamanın daha başarılı olduğundan emin olmak, üretimde çok daha hızlı ve güvenli bir şekilde geçiş yapmanıza olanak sağlar.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>Cihazları tanımla

İlk adım pilot 'a eklenecek cihazları belirlemektir. Masaüstü analizi, bildirilen verileri temel alan cihazlar önerir ve bu listedeki cihazları dahil edebilir veya değiştirebilirsiniz.

1. [Masaüstü Analizi portalına](https://aka.ms/desktopanalytics)gidin ve grubu Yönet ' ın altında **dağıtım planları**' nı seçin.

1. Bir dağıtım planı seçin.

1. Dağıtım planı menüsündeki hazırlama grubunda **pilot öğesini tanımla**' yı seçin.

Masaüstü analizinden, en iyi kapsam için dahil edilen cihaz sayısını gösteren verileri görürsünüz. Bu algoritma öncelikle önemli ve kritik uygulamaların kullanımına ve donanım yapılandırmalarının kapsamını temel alır.

Önerilen ek cihazlar listesi için aşağıdaki eylemleri gerçekleştirin:

- **Tüm pilot sürümüne Ekle**: önerilen tüm cihazları pilot grubuna ekler
- **Pilot 'A Ekle**: yalnızca tek cihazları ekleyin
- Pilot bilgisayardan gelen belirli cihazları **değiştirme**

**Dahil edilen** pilot listesine cihaz ekleyerek **, pilot** ' daki kritik ve önemli varlıklarınızın kapsamı ve artıklığı. Daha yüksek artıklık, kapsanan varlıkların, pilot verilerinize istatistiksel olarak önemli sayıda cihaz içerdiği anlamına gelir.

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>Küresel pilot

Ayrıca, hangi Configuration Manager koleksiyonlarının, Pilots 'lerden dahil edileceğini veya hangilerinin dışlanacağını belirten sistem genelinde kararlar verebilirsiniz. Ana masaüstü Analizi menüsünde, genel ayarlar grubunda **küresel pilot**' u seçin.

Birden çok Configuration Manager hiyerarşisini aynı masaüstü Analizi örneğine bağladığınızda, hiyerarşinin görünen adı genel pilot yapılandırmasındaki koleksiyon adına ön ekler. Bu ad, Configuration Manager konsolundaki masaüstü Analizi bağlantısında **görünen ad** özelliğidir.<!-- 4814075 -->

> [!NOTE]
> Birden çok hiyerarşi için destek, Configuration Manager sürüm 1910 veya üstünü gerektirir.

- Masaüstü analizinden toplam kayıtlı cihazlarınızın %20 ' sini içeren koleksiyonlar eklemeyin. Büyük bir koleksiyon eklerseniz, Portal bir uyarı görüntüler. Uyarı vermeden birden çok küçük koleksiyon ekleyebilirsiniz, ancak pilot ortamınızdaki cihaz sayısı hakkında dikkatli olmaya devam edebilirsiniz. <!-- 6079184 -->

- Belirli bir Configuration Manager hiyerarşisinde dağıtım planlarına yönelik doğru pilot önerileri almak için, yalnızca bu hiyerarşiden koleksiyonları dahil edin.

### <a name="example"></a>Örnek

- Configuration Manager ' de masaüstü Analizi bağlantısını **Tüm sistemler** koleksiyonunu hedefleyecek şekilde yapılandırırsınız. Bu eylem tüm istemcileri hizmete kaydeder.

- Ayrıca, masaüstü analiziyle eşitlenecek ek koleksiyonlar da yapılandırabilirsiniz:

  - Tüm Windows 10 istemcileri (3.000 cihaz)

  - Tüm BT cihazları (200 toplam cihaz, Windows 10 çalıştıran 150)

  - CEO ofisi (20 cihaz)

- **Genel pilot** ayarları ' nda, **tüm Windows 10 istemcileri** koleksiyonlarını dahil edersiniz. **CEO Office** koleksiyonunu dışarıda bırakabilirsiniz.

- Bir dağıtım planı oluşturun ve **hedef grubunuz**olarak **tüm BT cihazları** koleksiyonunu seçin. Bu dağıtım planını yalnızca BT departmanındaki cihazlar için amaçlarsınız.

- **Pilot cihazlar dahil** olmak üzere, hem **hedef**GRUBUNUZDAKI hem de **tüm BT cihazları** ve genel pilot *ekleme* listesi: **tüm Windows 10 istemcileri**içindeki cihazların alt kümesini içerir. 150 cihaz bu listede olduğundan, yalnızca **tüm BT cihazları** koleksiyonundaki 150 cihaz Windows 10 ' u çalıştırdığından.

- **Önerilen ek cihaz** listeleri, önemli varlıklarınız için maksimum kapsam ve artıklık sağlayan **hedef grubunuza** ait bir cihaz kümesi içerir. Masaüstü analizi, genel pilot *hariç tutma* listenizdeki tüm cihazları bu listeden dışlar: **GM Office**.

## <a name="address-issues"></a>Adres sorunları

Dağıtımınızı engelleyebilen varlıklar ile bildirilen tüm sorunları gözden geçirmek için masaüstü Analizi portalını kullanın. Ardından önerilen düzeltmesini onaylayın, reddedin veya değiştirin. Pilot dağıtımı başlamadan önce tüm öğelerin **Ready** veya **Ready (düzeltme ile)** olarak işaretlenmesi gerekir.

1. [Masaüstü Analizi portalına](https://aka.ms/desktopanalytics)gidin ve grubu Yönet ' ın altında **dağıtım planları**' nı seçin.  

2. Bir dağıtım planı seçin.  

3. Dağıtım planı menüsündeki hazırlama grubunda **pilot hazırlama**' yı seçin.  

4. **Uygulamalar** sekmesinde, giriş yapmanız gereken uygulamaları gözden geçirin.  

5. Her uygulama için uygulama adını seçin. Bilgi bölmesinde, öneriyi gözden geçirin ve yükseltme kararını ' nı seçin. **Gözden geçirilmeyen veya uygulamadıysanız** , masaüstü Analizi pilot dağıtımda bu uygulamayla cihazları içermez. **Unable** **Ready (düzeltme ile)** seçeneğini belirlerseniz, bir sorunu gidermek için gerçekleştirilecek eylemleri *yakalamak veya* *üretici tarafından önerilen sürümü bulmak*gibi **Düzeltme notlarını** kullanın.

6. Bu incelemeyi diğer varlıklar için tekrarlayın.  

Bu gözden geçirme süreci hakkında daha fazla bilgi için bkz. [Uyumluluk değerlendirmesi](compat-assessment.md).

## <a name="create-software"></a>Yazılım oluştur

Windows 'u dağıtabilmeniz için önce Configuration Manager ' de yazılım nesneleri oluşturun. Daha fazla bilgi için bkz. [Windows 10 yerinde yükseltme görev dizisi](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

## <a name="deploy-to-pilot-devices"></a>Pilot cihazlara dağıtma

Configuration Manager, pilot ve üretim dağıtımları için Koleksiyonlar oluşturmak üzere masaüstü analizinden gelen verileri kullanır. Bu koleksiyonlar **varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları** düğümünde, **dağıtım planları** klasöründedir.

> [!IMPORTANT]
> Bu koleksiyonlar, masaüstü Analizi dağıtım planları için Configuration Manager tarafından yönetilir. El ile yapılan değişiklikler desteklenmez. Bu koleksiyonlardan birini silerseniz, masaüstü Analizi çalışmaz ve [Configuration Manager yeniden bağlanmanız](connect-configmgr.md) gerekir.<!--7208090-->

Cihazların her dağıtım aşamasından sonra sağlıklı olduğundan emin olmak için, masaüstü analizi ile tümleşik aşamalı dağıtım oluşturmak için aşağıdaki yordamı kullanın:

1. Configuration Manager konsolunda, **yazılım kitaplığı**' na gidin, **Masaüstü Analizi Bakımı**' nı genişletin ve **dağıtım planları** düğümünü seçin.  

2. Dağıtım planınızı seçin ve ardından şeritte **dağıtım planı ayrıntıları** ' nı seçin.  

3. Şeritte **aşamalı dağıtım oluştur** ' u seçin. Bu eylem, aşamalı dağıtım oluşturma Sihirbazı 'nı başlatır.

    > [!Tip]  
    > Yalnızca pilot koleksiyon için klasik bir görev sırası dağıtımı oluşturmak istiyorsanız, **pilot durum** kutucuğunda **Dağıt** ' ı seçin. Bu eylem, Yazılım Dağıtma Sihirbazı 'Nı başlatır. Daha fazla bilgi için, bkz. [Deploy a task sequence](../osd/deploy-use/deploy-a-task-sequence.md).  

4. Dağıtım için bir ad girin ve kullanılacak görev sırasını seçin. **Varsayılan iki aşamalı dağıtımı otomatik olarak oluşturmak**ve ardından aşağıdaki koleksiyonları yapılandırmak için seçeneğini kullanın:  

    - **Ilk koleksiyon**: Bu dağıtım planı için **pilot** koleksiyonu bulun ve seçin. Bu koleksiyon için standart adlandırma kuralı `<deployment plan name> (Pilot)` .

    - **Ikinci koleksiyon**: Bu dağıtım planı için **Üretim** koleksiyonunu bulun ve seçin. Bu koleksiyon için standart adlandırma kuralı `<deployment plan name> (Production)` .

    > [!Note]  
    > Masaüstü Analizi tümleştirmesiyle, Configuration Manager dağıtım planı için otomatik olarak pilot ve üretim koleksiyonları oluşturur. Bunları kullanabilmeniz için, bu koleksiyonların eşitlenmesi zaman alabilir. Daha fazla bilgi için bkz. [sorun giderme-veri gecikmesi](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Bu koleksiyonlar, masaüstü Analizi dağıtım planı cihazları için ayrılmıştır. Bu koleksiyonlardaki el ile yapılan değişiklikler desteklenmez.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Aşamalı dağıtımı yapılandırmak için Sihirbazı doldurun. Daha fazla bilgi için bkz. [aşamalı dağıtımlar oluşturma](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

    > [!Note]  
    > **Bir erteleme döneminden (gün) sonra bu aşamayı otomatik olarak başlatmak**için varsayılan ayarı kullanın. İkinci aşamanın başlaması için aşağıdaki kriterlerin karşılanması gerekir:
    >
    > 1. İlk aşama başarılı olması için **dağıtım başarı yüzdesi** ölçütlerine ulaşır. Bu ayarı aşamalı dağıtımda yapılandırırsınız.
    > 1. Önemli ve kritik varlıkları *hazırlık*olarak Işaretlemek Için masaüstü analizinde yükseltme kararlarını gözden geçirmeniz ve bu kararları yapmanız gerekir. Daha fazla bilgi için bkz. [yükseltme kararı gerektiren varlıkları gözden geçirme](deploy-prod.md#bkmk_review).
    > 1. Masaüstü analizi, Configuration Manager koleksiyonlara eşitlenir ve *Bu, hazırlama ölçütlerini karşılayan* tüm üretim cihazlarını karşılar.

> [!Important]  
> Bu koleksiyonlar, üyelik değişiklikleri olarak eşitlemeye devam eder. Örneğin, bir varlıkla ilgili bir sorun tespit ederseniz ve bunu **yapılamıyor**olarak işaretlerseniz, söz konusu varlığa sahip cihazlar artık *ücretsiz ölçütleri* karşılamaz. Bu cihazlar üretim dağıtım koleksiyonundan bırakılır.

## <a name="monitor"></a>İzleyici

### <a name="configuration-manager-console"></a>Configuration Manager konsolu

Dağıtım planını açın. **Yükseltme kararlarını hazırlama-genel durum** kutucuğu, dağıtım planının durumunun bir özetini sağlar. Bu durum hem pilot hem de üretim koleksiyonlarınız içindir. Cihazlar aşağıdaki kategorilerden birine denk olabilir:

- **Güncel: cihazlar**bu dağıtım planı Için hedef Windows sürümüne yükseltildi

- **Yükseltme kararı Tamam**: aşağıdaki durumlardan biri:

  - Düzeltmeye **hazırlanma** veya **düzeltme ile hazırlanma** konusunda, önemli varlıklar içeren cihazlar

  - Cihaz durumu **engellendi**, [**cihazı değiştir**](about-deployment-plans.md#plan-assets) veya **cihazı yeniden yükle**

- **Gözden geçirilmedi**: önemli varlıkların gözden **geçirilmemiş veya gözden geçirilmeyen** cihazlar **devam ediyor**

Cihaz durumu, **pilot durum** ve **Üretim durumu** kutucuklarında aşağıdaki eylemlerle güncelleştirilir:

- Uyumluluk değerlendirmesinde değişiklikler yaparsınız
- Cihazlar Windows 'un hedef sürümüne yükseltildi
- Dağıtımınız ilerleme

Configuration Manager dağıtım izlemeyi diğer görev sırası dağıtımıyla aynı zamanda da kullanabilirsiniz. Daha fazla bilgi için bkz. [işletim sistemi dağıtımlarını izleme](../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="desktop-analytics-portal"></a>Masaüstü Analizi portalı

Herhangi bir dağıtım planının durumunu görüntülemek için [Masaüstü Analizi portalını](https://aka.ms/desktopanalytics) kullanın. Dağıtım planını seçin ve ardından **plana genel bakış**' ı seçin.

![Masaüstü analizinden dağıtım planına genel bakış ekran görüntüsü](media/deployment-plan-overview.png)

**Pilot** kutucuğunu seçin. Pilot dağıtımın geçerli durumunu özetler. Bu kutucuk Ayrıca başlatılmamış cihaz sayısı, devam ediyor, tamamlandı veya geri dönme sorunları için verileri görüntüler.

Hataları veya diğer sorunları bildiren tüm cihazlar da sağdaki pilot ayrıntı alanında listelenir. Bildirilen sorunun ayrıntılarını almak için **gözden geçir**' i seçin. Bu eylem, görünümü **dağıtım durumu** sayfasına değiştirir

**Dağıtım durumu** sayfası aşağıdaki kategorilerdeki cihazları listeler:

- Başlamadı
- Sürüyor
- Tamamlandı
- İlgilenilmesi gerekiyor-cihazlar
- Dikkat edilmesi gereken noktalar-sorunlar

**Ilgilenilmesi gereken dikkat** kategorileri aynı bilgileri gösterir, ancak farklı şekilde sıralanır.

Algılanan sorun hakkında daha fazla ayrıntı edinmek için her iki görünümde belirli bir listeyi seçin.

Bu dağıtım sorunlarına yönelik olarak, pano cihazların ilerlemesini göstermeye devam eder. Cihazlar, **Ihtiyaç duymayla** **tamamlanana**kadar hareket etmek için BT güncellenir.

## <a name="next-steps"></a>Sonraki adımlar

İşletimsel verileri toplamada bir süre boyunca pilot çalıştırmaya izin verin. Pilot cihazların kullanıcılarını uygulamaları test etmek için teşvik edin.

Pilot dağıtımınız başarı ölçütlerinizi karşıladığında, üretime dağıtmak için sonraki makaleye gidin.
> [!div class="nextstepaction"]  
> [Üretime dağıtma](deploy-prod.md)  
