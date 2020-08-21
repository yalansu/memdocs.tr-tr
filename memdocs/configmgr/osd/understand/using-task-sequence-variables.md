---
title: Görev dizisi değişkenlerini kullanma
titleSuffix: Configuration Manager
description: Configuration Manager bir görev dizisinde değişkenlerin nasıl kullanılacağı hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7013ae10de753cbcb664771bd30dc51b259aa390
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697560"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Configuration Manager 'de görev dizisi değişkenlerini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Configuration Manager işletim sistemi dağıtımı özelliğindeki görev dizisi altyapısı davranışlarını denetlemek için birçok değişken kullanır. Bu değişkenleri şu şekilde kullanın:

- Adımlarda koşulları ayarlama  
- Belirli adımlarla ilgili davranışları değiştirme  
- Daha karmaşık eylemler için betiklerin kullanımı  

Kullanılabilir tüm görev sırası değişkenlerinin bir başvurusu için bkz. [görev dizisi değişkenleri](task-sequence-variables.md).

## <a name="types-of-variables"></a><a name="bkmk_types"></a> Değişken türleri

Birçok değişken türü vardır:  

- [Yerleşik](#bkmk_built-in)  
- [Eylem](#bkmk_action)  
- [Özel](#bkmk_custom)  
- [Salt okunur](#bkmk_read-only)  
- [Dizide](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a> Yerleşik değişkenler

Yerleşik değişkenler, görev dizisinin çalıştığı ortam hakkında bilgiler sağlar. Değerleri, tüm görev sırası boyunca kullanılabilir. Genellikle, görev sırası altyapısı herhangi bir adımı çalıştırmadan önce yerleşik değişkenleri başlatır.

Örneğin, `_SMSTSLogPath` Configuration Manager bileşenlerinin günlük dosyalarını yazacağı yolu belirten bir ortam değişkenidir. Herhangi bir görev dizisi adımı, bu ortam değişkenine erişebilir.

Görev dizisi, her adımdan önce bazı değişkenleri değerlendirir. Örneğin, `_SMSTSCurrentActionName` geçerli adımın adını listeler.

### <a name="action-variables"></a><a name="bkmk_action"></a> Eylem değişkenleri

Görev dizisi eylem değişkenleri, tek bir görev dizisi adımının kullandığı yapılandırma ayarlarını belirtir. Varsayılan olarak, adım, çalıştırılmadan önce ayarlarını başlatır. Bu ayarlar yalnızca ilişkili görev dizisi adımı çalışırken kullanılabilir. Görev dizisi, adımı çalıştırmadan önce eylem değişkeni değerini ortama ekler. Ardından, adım çalıştıktan sonra değeri ortamdan kaldırır.

Örneğin, **komut satırını Çalıştır** adımını bir görev dizisine eklersiniz. Bu adım bir **Başlangıç** özelliği içerir. Görev sırası, bu özellik için değişken olarak varsayılan bir değer depolar `WorkingDirectory` . Görev sırası, **komut satırını Çalıştır** adımını çalıştırmadan önce bu değeri başlatır. Bu adım çalışırken, değerden **Başlangıç** özellik değerine erişin `WorkingDirectory` . Adım tamamlandıktan sonra görev dizisi, `WorkingDirectory` değişkenin değerini ortamdan kaldırır. Görev sırası başka bir **Çalıştır komut satırı** adımını içeriyorsa, yeni bir `WorkingDirectory` değişken başlatır. Bu sırada, görev sırası değişkeni geçerli adım için başlangıç değerine ayarlar. Daha fazla bilgi için bkz. [WorkingDirectory](task-sequence-variables.md#WorkingDirectory).  

Bir eylem değişkeni için *varsayılan* değer, adım çalıştığında vardır. *Yeni* bir değer ayarlarsanız, görev dizisinde birden çok adım vardır. Varsayılan bir değeri geçersiz kılarsınız, yeni değer ortamda kalır. Bu yeni değer, görev dizisindeki diğer adımlar için varsayılan değeri geçersiz kılar. Örneğin, görev dizisinin ilk adımı olarak bir **Ayarla görev sırası değişkeni** adımı eklersiniz. Bu adım `WorkingDirectory` değişkenini olarak ayarlar `C:\` . Görev dizisindeki herhangi bir **Çalıştır komut satırı** adımı, yeni başlangıç dizini değerini kullanır.  

Bazı görev sırası adımları belirli eylem değişkenlerini *Çıkış*olarak işaretler. Görev dizisinin ilerleyen adımları bu çıktı değişkenlerini okur.

> [!Note]  
> Tüm görev dizisi adımlarının eylem değişkenleri yok. Örneğin, **BitLocker 'ı etkinleştir** eylemiyle ilişkili değişkenler olsa da, **BitLocker 'ı devre dışı bırak** eylemiyle ilişkili değişken yoktur.  

### <a name="custom-variables"></a><a name="bkmk_custom"></a> Özel değişkenler

Bu değişkenler Configuration Manager oluşturmaz. Koşul olarak, komut satırlarında veya betikte kullanmak üzere kendi değişkenlerinizi başlatın.

Yeni bir görev dizisi değişkeni için bir ad belirttiğinizde aşağıdaki yönergeleri izleyin:  

- Görev sırası değişken adı harf, sayı, alt çizgi karakteri ( `_` ) ve kısa çizgi ( `-` ) içerebilir.  

- Görev dizisi değişken adları, en az bir karakter uzunluğunda ve en fazla 256 karakter uzunluğunda olabilir.  

- Kullanıcı tanımlı değişkenlerin bir harfle başlaması gerekir ( `A-Z` veya `a-z` ).  

- Kullanıcı tanımlı değişken adları alt çizgi karakteriyle başlayamaz. Yalnızca salt okuma görev dizisi değişkenlerine alt çizgi karakteri gelir.  

- Görev dizisi değişken adları büyük/küçük harfe duyarlı değildir. Örneğin, `OSDVAR` ve `osdvar` aynı görev sırası değişkenidir.  

- Görev dizisi değişken adları boşlukla başlayamaz veya bitemez. Ayrıca, gömülü boşluklar olamaz. Görev sırası, bir değişken adının başındaki veya sonundaki boşlukları yoksayar.  

Oluşturabileceğiniz görev sırası değişkenlerinin sayısı için bir sınır yoktur. Ancak, değişken sayısı, görev dizisi ortamının boyutuyla sınırlıdır. Görev dizisi ortamı için toplam boyut sınırı 8 KB 'tır. Daha fazla bilgi için bkz. [görev sırası ilkesi boyutunu azaltma](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize).

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a> Salt okuma değişkenleri

Salt okunurdur bazı değişkenlerin değerini değiştiremezsiniz. Genellikle ad bir alt çizgi karakteriyle () başlar `_` . Görev sırası bunları işlemleri için kullanır. Salt okuma değişkenleri, görev dizisi ortamında görünür.

Bu değişkenler betiklerin veya komut satırlarındaki yararlı olur. Örneğin, bir komut satırı çalıştırma ve çıktıyı diğer günlük dosyalarıyla içindeki bir günlük dosyasına boru `_SMSTSLogPath` .

> [!NOTE]  
> Salt okuma görev dizisi değişkenleri, bir görev dizisindeki adımlarla okunabilir, ancak bunlar ayarlanamaz. Örneğin, komut **satırı Çalıştır** adımı için komut satırının parçası olarak salt okunurdur bir değişken kullanın. **Görev sırası değişkenini ayarla** adımını kullanarak salt okunurdur bir değişken ayarlayamazsınız.  

### <a name="array-variables"></a><a name="bkmk_array"></a> Dizi değişkenleri

Görev dizisi bazı değişkenleri bir dizi olarak depolar. Dizideki her öğe, tek bir nesne için ayarları temsil eder. Bir cihazda yapılandırmak için birden fazla nesne olduğunda bu değişkenleri kullanın. Aşağıdaki görev dizisi adımları dizi değişkenlerini kullanır:

- [Ağ Ayarlarını Uygula](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [Diski Biçimlendir ve Bölümle](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a> Değişkenleri ayarlama

Salt okuma olmayan özel değişkenler veya değişkenler için, değişkenin değerini başlatmak ve ayarlamak için birkaç yöntem vardır:  

- [Görev dizisi değişkeni adımını ayarla](#bkmk_set-ts-step)
- [Dinamik değişkenleri ayarla](#bkmk_set-dyn-step) adımı
- [PowerShell komut dosyası adımını Çalıştır](#bkmk_run-ps)
- [Koleksiyon ve cihaz değişkenleri](#bkmk_set-coll-var)  
- [TSEnvironment COM nesnesi](#bkmk_set-com)  
- [Başlatma öncesi komutu](#bkmk_set-prestart)  
- [Görev sırası Sihirbazı](#bkmk_set-tswiz)
- [Görev sırası Medyası Sihirbazı](#bkmk_set-media)  

Değişken oluşturma ile aynı yöntemleri kullanarak ortamdan bir değişkeni silin. Bir değişkeni silmek için, değişken değerini boş bir dizeye ayarlayın.  

Aynı dizi için farklı değerlere bir görev dizisi değişkeni ayarlamak için yöntemleri birleştirebilirsiniz. Örneğin, görev dizisi düzenleyicisini kullanarak varsayılan değerleri ayarlayın ve ardından bir komut dosyası kullanarak özel değerleri ayarlayın.

Aynı değişkeni farklı yöntemlerle ayarlarsanız, görev sırası altyapısı aşağıdaki sırayı kullanır:  

1. Önce koleksiyon değişkenlerini değerlendirir.  

2. Cihaza özgü değişkenler, bir koleksiyonda ayarlanan aynı değişkeni geçersiz kılar.  

3. Görev sırası sırasında herhangi bir yöntemle ayarlanan değişkenler koleksiyon veya cihaz değişkenlerine göre önceliklidir.  

### <a name="general-limitations-for-task-sequence-variable-values"></a>Görev dizisi değişken değerleri için genel sınırlamalar

- Görev dizisi değişken değerleri 4.000 karakterden uzun olamaz.  

- Salt okunurdur bir görev sırası değişkenini değiştiremezsiniz. Salt okuma değişkenlerinde bir alt çizgi karakteriyle () başlayan adlar vardır `_` .  

- Görev dizisi değişken değerleri, değerin kullanımına bağlı olarak büyük/küçük harfe duyarlı olabilir. Çoğu durumda, görev dizisi değişken değerleri büyük/küçük harfe duyarlı değildir. Bir parola içeren bir değişken büyük/küçük harfe duyarlıdır.  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a> Görev sırası değişkenini ayarla

Tek bir değişkeni tek bir değere ayarlamak için görev dizisinde bu adımı kullanın.

Daha fazla bilgi için bkz. [görev dizisi değişkenini ayarlama](task-sequence-steps.md#BKMK_SetTaskSequenceVariable).

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a> Dinamik değişkenleri ayarla

Görev dizisinde bir veya daha fazla görev sırası değişkeni ayarlamak için bu adımı kullanın. Hangi değişkenlerin ve değerlerin kullanılacağını belirlemek için bu adımda kurallar tanımlarsınız.

Daha fazla bilgi için bkz. [dinamik değişkenleri ayarlama](task-sequence-steps.md#BKMK_SetDynamicVariables).

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a> PowerShell betiğini Çalıştır

<!-- 6315548 -->

Bir görev dizisi değişkeni ayarlamak üzere bir PowerShell betiği kullanmak için görev dizisinde bu adımı kullanın.

Bir paketten bir betik adı belirtebilir veya adımda doğrudan bir PowerShell betiği girebilirsiniz. Ardından, komut dosyası çıkışını özel bir görev dizisi değişkenine kaydetmek üzere **görev dizisi değişkenine çıkış** yapmak için step özelliğini kullanın.

Bu adımla ilgili daha fazla bilgi için bkz. [PowerShell betiğini çalıştırma](task-sequence-steps.md#BKMK_RunPowerShellScript).

> [!NOTE]
> Ayrıca, **TSEnvironment** nesnesiyle bir veya daha fazla değişken ayarlamak Için bir PowerShell betiği de kullanabilirsiniz. Daha fazla bilgi için bkz. Configuration Manager SDK 'da [çalışan bir görev dizisinde değişkenleri kullanma](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) .

#### <a name="example-scenario-with-run-powershell-script-step"></a>PowerShell Betiği Çalıştır adımını içeren örnek senaryo

Ortamınızda birden çok ülkede/bölgede kullanıcılar vardır. bu nedenle işletim sistemi dilini, dile özgü birden çok **uygulama** için bir koşul olarak ayarlanacak şekilde sorgulamak istemeniz gerekir.

1. **İşletim sistemi adımlarını uygulamadan** önce görev dizisine **Çalıştır PowerShell betiğini** bir örnek ekleyin.

1. Aşağıdaki komutu belirtmek için **bir PowerShell betiği girme** seçeneğini kullanın:

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    Cmdlet hakkında daha fazla bilgi için bkz. [Get-Culture](/powershell/module/microsoft.powershell.utility/get-culture). İki harfli ISO dili adları hakkında daha fazla bilgi için bkz. [ıso 639-1 kodlarının listesi](https://wikipedia.org/wiki/List_of_ISO_639-1_codes).

1. **Görev dizisi değişkenine çıkış**seçeneği için, belirtin `CurrentOSLanguage` .

    ![PowerShell betiği çalıştırma adımının örnek görüntüsü](media/run-powershell-script-example-language.png)

1. Ingilizce dil görüntüsünün **işletim sistemini Uygula** adımında, aşağıdaki koşulu oluşturun: `Task Sequence Variable CurrentOSLanguage equals "en"`

    ![İşletim sistemini Uygula adımında örnek durum ekran görüntüsü](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > Bir adımda koşul oluşturma hakkında daha fazla bilgi için bkz. [nasıl erişim değişkenleri-adım koşulu](#bkmk_access-condition).

1. Görev sırasını kaydedin ve dağıtın.

**PowerShell Betiği Çalıştır** adımı, Windows 'un İngilizce dil sürümü olan bir cihazda çalıştırıldığında, komut değeri döndürür `en` . Daha sonra bu değeri özel değişkenine kaydeder. Ingilizce dil görüntüsü için **işletim sistemi Uygula** adımı aynı cihazda çalıştırıldığında, koşul true olarak değerlendirilir. Farklı diller için **işletim sistemi Uygula** adımının birden çok örneği varsa, görev sırası, işletim sistemi diliyle eşleşen adımı dinamik olarak çalıştırır.

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a> Koleksiyon ve cihaz değişkenleri

Cihazlar ve koleksiyonlar için özel görev sırası değişkenlerini tanımlayabilirsiniz. Bir cihaz için tanımladığınız değişkenlere cihaz başına görev sırası değişkenleri denir. Bir koleksiyon için tanımlanan değişkenler koleksiyon başına görev sırası değişkenleri olarak bilinir. Bir çakışma varsa, cihaz başına değişkenler koleksiyon başına değişkenlere göre önceliklidir. Bu davranış, belirli bir cihaza atanan görev sırası değişkenlerinin otomatik olarak, cihazı içeren koleksiyona atanan değişkenlere göre daha yüksek önceliğe sahip olduğu anlamına gelir.  

Örneğin, XYZ cihazı ABC koleksiyonunun bir üyesidir. MyVariable değerini 1 değeri ile ABC koleksiyonuna atarsınız. Ayrıca, MyVariable değerini 2 değeri ile XYZ cihazına atayabilirsiniz. XYZ öğesine atanan değişken, ABC koleksiyonuna atanmış olan değişkenden daha yüksek önceliğe sahiptir. Bu değişkene sahip bir görev dizisi XYZ üzerinde çalışırken, MyVariable değeri 2 ' dir.

Cihaz başına ve koleksiyon başına değişkenleri, Configuration Manager konsolunda görünmemesi için gizleyebilirsiniz. **Bu değeri Configuration Manager konsolunda gösterme**seçeneğini kullandığınızda, değişkenin değeri konsolunda görüntülenmez. Görev sırası günlük dosyası (**Smsts. log**) veya görev sırası hata ayıklayıcı değişken değerini göstermez. Değişken, çalışma sırasında görev sırası tarafından hala kullanılıyor olabilir. Artık bu değişkenlerin gizli olmasını istemiyorsanız, önce bunları silin. Sonra değişkenleri gizleme seçeneğini seçmeden yeniden tanımlayın.  

> [!WARNING]  
> **Komut satırı** adımının komut satırını Çalıştır ' a değişkenler eklerseniz, görev sırası günlük dosyası değişken değerleri dahil olmak üzere tam komut satırını görüntüler. Potansiyel olarak gizli verilerin günlük dosyasında görünmesini engellemek için **Osddonotlogcommand** görev sırası değişkenini olarak ayarlayın `TRUE` .

Cihaz başına değişkenleri bir birincil sitede veya merkezi yönetim sitesinde yönetebilirsiniz. Configuration Manager, bir cihaz için 1.000 ' den fazla değişkeni desteklemez.  

> [!IMPORTANT]  
> Görev dizileri için koleksiyon başına değişkenleri kullandığınızda aşağıdaki davranışları göz önünde bulundurun:  
>
> - Koleksiyonlardaki değişiklikler her zaman hiyerarşi genelinde çoğaltılır. Koleksiyon değişkenlerinde yaptığınız tüm değişiklikler yalnızca geçerli sitenin üyeleri için değil, hiyerarşi genelindeki koleksiyonun tüm üyeleri için de geçerlidir.  
>  
> - Bir koleksiyonu sildiğinizde bu eylem aynı zamanda koleksiyon için yapılandırdığınız görev sırası değişkenlerini de siler.  

#### <a name="create-task-sequence-variables-for-a-device"></a>Bir *cihaz* için görev sırası değişkenleri oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin.  

2. Hedef cihazı seçin ve **Özellikler**' i seçin.  

3. **Özellikler** Iletişim kutusunda **değişkenler** sekmesine geçin.  

4. Oluşturmak istediğiniz her bir değişken için **Yeni** simgesini seçin. Görev sırası değişkeninin **adını** ve **değerini** belirtin. Değişkeni Configuration Manager konsolunda görünür olmaması için gizlemek istiyorsanız, **Bu değeri Configuration Manager konsolunda gösterme**seçeneğini belirleyin.  

5. Tüm değişkenleri cihaz özelliklerine ekledikten sonra **Tamam**' ı seçin.  

#### <a name="create-task-sequence-variables-for-a-collection"></a>Bir *koleksiyon* için görev dizisi değişkenleri oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Cihaz Koleksiyonları** düğümünü seçin. Hedef koleksiyonu seçin ve **Özellikler**' i seçin.  

2. **Özellikler** Iletişim kutusunda **koleksiyon değişkenleri** sekmesine geçin.  

3. Oluşturmak istediğiniz her bir değişken için **Yeni** simgesini seçin. Görev sırası değişkeninin **adını** ve **değerini** belirtin. Değişkeni Configuration Manager konsolunda görünür olmaması için gizlemek istiyorsanız, **Bu değeri Configuration Manager konsolunda gösterme**seçeneğini belirleyin.  

4. İsteğe bağlı olarak, görev sırası değişkenleri değerlendirildiğinde kullanılacak Configuration Manager önceliğini belirtin.  

5. Tüm değişkenleri koleksiyon özelliklerine ekledikten sonra **Tamam**' ı seçin.  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a> TSEnvironment COM nesnesi

Bir betikteki değişkenlerle çalışmak için **TSEnvironment** nesnesini kullanın.

Daha fazla bilgi için bkz. Configuration Manager SDK 'da [çalışan bir görev dizisinde değişkenleri kullanma](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) .

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a> Başlatma öncesi komutu

Başlatma öncesi komutu, Kullanıcı görev sırasını seçmeden önce Windows PE 'de çalışan bir betik veya yürütülebilir dosyadır. Başlatma öncesi komutu bir değişkeni sorgulayabilir veya kullanıcıdan bilgi isteyebilir ve sonra ortama kaydedebilir. Başlatma öncesi komutundan değişkenleri okumak ve yazmak için [TSEnvironment](#bkmk_set-com) com nesnesini kullanın.

Daha fazla bilgi için bkz. [görev dizisi medyası Için başlatma öncesi komutları](prestart-commands-for-task-sequence-media.md).

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a> Görev sırası Sihirbazı

Sürüm 1906 ' den başlayarak, görev dizisi Sihirbazı penceresinde bir görev sırası seçtikten sonra, görev sırası değişkenlerini düzenleme sayfası bir **Düzenle** düğmesi içerir. Değişkenleri düzenlemek için erişilebilir klavye kısayollarını kullanabilirsiniz. Bu değişiklik, fare kullanılamayan durumlarda yardımcı olur.<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a> Görev sırası Medyası Sihirbazı

Medyadan çalıştırılan görev dizileri için değişkenleri belirtin. İşletim sistemini dağıtmak için medya kullanırken, medya oluştururken görev sırası değişkenlerini ekler ve değerlerini belirtirsiniz. Değişkenler ve değerleri medyada depolanır.  

> [!NOTE]  
> Görev dizileri tek başına medyada depolanır. Ancak, önceden hazırlanan medya gibi diğer tüm medya türleri, görev sırasını bir yönetim noktasından alır.  

Medyadan bir görev dizisi çalıştırdığınızda, sihirbazın **Özelleştirme** sayfasına bir değişken ekleyebilirsiniz.

Koleksiyona göre ve bilgisayara göre değişkenlerin yerine medya değişkenlerini kullanın. Görev dizisi medyadan çalışıyorsa, bilgisayar başına ve koleksiyon başına değişkenler uygulanmaz ve kullanılmaz.  

> [!TIP]  
> Görev sırası, paket KIMLIĞINI ve başlatma öncesi komut satırını Configuration Manager konsolunu çalıştıran bilgisayardaki **CreateTsMedia. log** dosyasına yazar. Bu günlük dosyası, herhangi bir görev dizisi değişkeni için değer içerir. Görev dizisi değişkenlerinin değerini doğrulamak için bu günlük dosyasını gözden geçirin.  

Daha fazla bilgi için bkz. [görev dizisi medyası oluşturma](../deploy-use/create-task-sequence-media.md).

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a> Değişkenlere erişme

Önceki bölümde yer aldığı yöntemlerden birini kullanarak değişkeni ve değerini belirttikten sonra, görev dizilerinizde kullanın. Örneğin, yerleşik görev dizisi değişkenleri için varsayılan değerlere erişin veya bir değişkenin değerinde bir adım koşullu yapın.  

Görev dizisi ortamındaki değişken değerlerine erişmek için aşağıdaki yöntemleri kullanın:

- [Bir adımda kullanma](#bkmk_access-step)  
- [Adım koşulu](#bkmk_access-condition)  
- [Özel Betik](#bkmk_access-script)  
- [Windows kurulumu yanıt dosyası](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a> Bir adımda kullanma

Bir görev dizisi adımındaki ayar için bir değişken değeri belirtin. Görev sırası düzenleyicisinde, adımı düzenleyin ve alan değeri olarak değişken adını belirtin. Değişken adını yüzde işaretleri () içine alın `%` .

Örneğin, **komut satırı Çalıştır** adımının **komut satırı** alanının parçası olarak değişken adını kullanın. Aşağıdaki komut satırı, bilgisayar adını bir metin dosyasına yazar.

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a> Adım koşulu

Bir adım veya gruptaki koşulun bir parçası olarak yerleşik veya özel görev dizisi değişkenleri kullanın. Görev sırası, adımı veya grubu çalıştırmadan önce değişken değerini değerlendirir.

Bir değişken değerini değerlendiren bir koşul eklemek için aşağıdaki adımları uygulayın:  

1. Görev sırası düzenleyicisinde, koşulu eklemek istediğiniz adımı veya grubu seçin.  

2. Adım veya grup için **Seçenekler** sekmesine geçin. **Koşul Ekle**' ye tıklayın ve **görev dizisi değişkeni**' ni seçin.  

3. **Görev dizisi değişkeni** iletişim kutusunda, aşağıdaki ayarları belirtin:  

    - **Değişken**: değişkenin adı. Örneğin, `_SMSTSInWinPE`.  

    - **Koşul**: değişken değerini değerlendirmek için koşul. Örneğin, **eşittir**.  

    - **Değer**: denetlenecek değişkenin değeri. Örneğin, `false`.  

Yukarıdaki üç örnek, görev dizisinin Windows PE 'deki önyükleme görüntüsünden çalışıp çalışmadığını sınamak için ortak bir koşul oluşturur:

> **Görev sırası değişkeni**`_SMSTSInWinPE equals "false"`

Var olan bir işletim sistemi görüntüsünü yüklemek için varsayılan görev sırası şablonunun **yakalama dosyaları ve ayarlar** grubunda bu koşula bakın.

Koşullar hakkında daha fazla bilgi için bkz. [görev dizisi Düzenleyicisi-koşullar](task-sequence-editor.md#bkmk_conditions).

### <a name="custom-script"></a><a name="bkmk_access-script"></a> Özel Betik

Görev dizisi çalışırken **Microsoft. SMS. TSEnvironment** com nesnesini kullanarak değişkenleri okuyun ve yazın.

Aşağıdaki Windows PowerShell örneği, geçerli günlük konumunu almak için **_SMSTSLogPath** değişkenini sorgular. Komut dosyası ayrıca özel bir değişken ayarlar.

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a> Windows kurulumu yanıt dosyası

Sağladığınız Windows kurulumu yanıt dosyasında katıştırılmış görev sırası değişkenleri olabilir. Formunu kullanın `%varname%` , burada *varname* değişkenin adıdır. **Windows 'u ve ConfigMgr 'Yi Kur** adımı, gerçek değişken değeri için değişken adı dizesinin yerini alır. Bu katıştırılmış görev sırası değişkenleri bir unattend.xml yanıt dosyasındaki yalnızca sayısal alanlarda kullanılamaz.

Daha fazla bilgi için, bkz. [Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).

## <a name="see-also"></a>Ayrıca bkz.

- [Görev dizisi adımları](task-sequence-steps.md)

- [Görev dizisi değişkenleri](task-sequence-variables.md)

- [Otomatikleştirme görevlerini planlama konuları](../plan-design/planning-considerations-for-automating-tasks.md)

- [Görev sırası Düzenleyicisi](task-sequence-editor.md)