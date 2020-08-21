---
title: Konsol değişiklikleri ve ipuçları Configuration Manager
titleSuffix: Configuration Manager
description: Configuration Manager konsolundaki değişiklikler ve bu uygulamayı kullanmaya yönelik ipuçları hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0a434f013da48d660efa78f5e2cdca6ced0826d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700727"
---
# <a name="configuration-manager-console-changes-and-tips"></a>Konsol değişiklikleri ve ipuçları Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager konsolundaki değişiklikler hakkında bilgi edinmek için aşağıdaki bilgileri kullanın ve konsolu kullanmaya yönelik ipuçlarına gidin:

## <a name="general-tips"></a>Genel ipuçları

### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Konsol aramasında iyileştirmeler
<!--4640570-->
*(Sürüm 1910 ' de tanıtılmıştır)*

- **Sürücü paketleri** ve **sorgular** düğümlerinde **tüm alt klasörler** arama seçeneğini kullanabilirsiniz.<!--2841181,5424892--> Sürüm 2002 ' den başlayarak, **yapılandırma öğeleri** ve **yapılandırma temelleri** düğümlerinden da bu seçeneği kullanın.<!--5891241-->

- Bir arama 1.000 'den fazla sonuç döndürdüğünde, daha fazla sonuç görüntülemek için bildirim çubuğunda **Tamam** düğmesini seçin.<!--4640570-->

    ![Çok fazla arama sonucu için bildirim çubuğunun ekran görüntüsü](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > Arama sonuçlarındaki varsayılan sınır 1.000 ' dir. Bu varsayılan değeri değiştirebilirsiniz. Configuration Manager konsolunda, şeridin **arama** sekmesine gidin. **Seçenekler** grubunda **Arama ayarları**' nı seçin. **Arama sonuçları** değerini değiştirin. Daha fazla sayıda arama sonucu görüntülenmesi daha uzun sürebilir.
    >
    > Varsayılan olarak en büyük sınır 100.000 ' dir. Bu sınırı değiştirmek için, aşağıdaki kayıt defteri anahtarında **Queryresultcountmaximum** DWORD değerini ayarlayın:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > Konsol içi ayarı aynı anahtardaki **Queryresultcountlimit** değerine karşılık gelir. Yönetici, bu değerleri, tüm cihaz kullanıcıları için HKLM Hive içinde yapılandırabilir. HKCU değeri, HKLM ayarını geçersiz kılar.

### <a name="role-based-administration-for-folders"></a>Klasörler için rol tabanlı yönetim
<!--3600867-->
*(Sürüm 1906 ' de tanıtılmıştır)*

Klasörler üzerinde güvenlik kapsamları ayarlayabilirsiniz. Klasör içindeki bir nesneye erişiminiz varsa ancak klasöre erişiminiz yoksa, nesneyi göremezsiniz. Benzer şekilde, bir klasöre erişiminiz varsa ancak içinde bir nesne yoksa, bu nesneyi görmezsiniz. Bir klasöre sağ tıklayın, **güvenlik kapsamlarını ayarla**' yı seçin ve ardından uygulamak istediğiniz güvenlik kapsamlarını seçin.

### <a name="views-sort-by-integer-values"></a>Görünümler tamsayı değerlerine göre sıralanır

*(Sürüm 1902 ' de tanıtılmıştır)*

Çeşitli görünümlerin verileri nasıl sıraladığımızda geliştirmeler yaptık. Örneğin, **izleme** çalışma alanının **dağıtımlar** düğümünde aşağıdaki sütunlar artık dize değerleri yerine sayı olarak sıralanır:  

- Hata sayısı
- Devam eden sayı
- Diğer sayı
- Başarı sayısı
- Bilinmeyen sayı  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Uyarıyı çok sayıda sonuç için taşıma

*(Sürüm 1902 ' de tanıtılmıştır)*

Konsolda 1.000 'den fazla sonuç döndüren bir düğüm seçtiğinizde, Configuration Manager aşağıdaki uyarıyı gösterir:

> Configuration Manager çok sayıda sonuç döndürdü. Aramayı kullanarak sonuçlarınızı daraltabilirsiniz. Veya en fazla 100000 sonucu görüntülemek için buraya tıklayın.

Bu uyarı ve arama alanı arasında artık ek boş alan var. Bu taşıma, daha fazla sonuç göstermek için uyarının yanlışlıkla seçilmesine engel olmaya yardımcı olur.

### <a name="send-feedback"></a>Geri bildirim gönder

*(Sürüm 1806 ' de tanıtılmıştır)*
<!--1357542-->

Konsolundan ürün geri bildirimi gönderin.  

- **Gülümseme Gönder**: beğendikleriniz hakkında geri bildirim gönderin  

- **Kaş çatma Gönder**: beğendikleriniz hakkında geri bildirim gönderin  

- **Öneri gönderin**: fikrinizi paylaşmak Için sizi UserVoice 'a götürür  

Daha fazla bilgi için bkz. [ürün geri bildirimi](../../understand/find-help.md#BKMK_1806Feedback).


## <a name="assets-and-compliance-workspace"></a>Varlıklar ve uyum çalışma alanı

### <a name="real-time-actions-from-device-lists"></a>Cihaz listelerinden gerçek zamanlı eylemler
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**Varlıklar ve uyum** çalışma alanındaki **cihazlar** düğümü altında cihazların listesini görüntülemenin çeşitli yolları vardır.

- **Varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları** düğümünü seçin. Bir cihaz koleksiyonu seçin ve **üyeleri göstermek**için eylemi seçin. Bu eylem, bu koleksiyon için bir cihaz listesi olan **Devices** düğümünün bir alt düğümünü açar.  

  - Koleksiyon alt düğümü ' nü seçtiğinizde, artık şeridin koleksiyon grubundan **CMPivot** başlatabilirsiniz.  

- **İzleme** çalışma alanında, **dağıtımlar** düğümünü seçin. Bir dağıtım seçin ve Şeritteki **durumu görüntüle** eylemini seçin. Dağıtım durumu bölmesinde, bir cihaz listesine gitmek için toplam varlıklara çift tıklayın.  

  - Bu listede bir cihaz seçtiğinizde, artık **CMPivot** başlatabilir ve şerit 'in cihaz grubundan **betikleri çalıştırabilirsiniz** .  


### <a name="collections-tab-in-devices-node"></a>Cihazlar düğümünde koleksiyonlar sekmesi
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**Varlıklar ve uyum** çalışma alanında, **cihazlar** düğümüne gidin ve bir cihaz seçin. Ayrıntılar bölmesinde, yeni **koleksiyonlar** sekmesine geçin. Bu sekme, bu cihazı içeren koleksiyonları listeler. 

> [!Note]  
> - Bu sekme şu anda **Cihaz Koleksiyonları** düğümünün altındaki cihazlar alt düğümünden kullanılamaz. Örneğin, bir koleksiyondaki **üyeleri gösterme** seçeneğini belirlediğinizde.
> - Bu sekme bazı kullanıcılar için beklendiği gibi doldurulamayabilir. Bir cihazın ait olduğu koleksiyonların tam listesini görmek için, **tam yönetici** güvenlik rolüne sahip olmanız gerekir. Bu bilinen bir sorundur. <!--5107309--> <!--5107309-->


### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Cihaz ve cihaz koleksiyonu düğümlerine SMBıOS GUID sütunu Ekle

*(Sürüm 1906 ' de tanıtılmıştır)*

<!--4526580-->
Hem **cihazlarda** hem de **Cihaz Koleksiyonları** DÜĞÜMLERINDE, artık **SMBIOS GUID**için yeni bir sütun ekleyebilirsiniz. Bu değer, sistem kaynak sınıfının **BIOS GUID** özelliği ile aynıdır. Cihaz donanımı için benzersiz bir tanımlayıcıdır.

### <a name="search-device-views-using-mac-address"></a>MAC adresini kullanarak cihaz görünümlerini ara

<!--3600878-->
*(Sürüm 1902 ' de tanıtılmıştır)*

Bir MAC adresini Configuration Manager konsolunun bir cihaz görünümünde arayabilirsiniz. Bu özellik, PXE tabanlı dağıtımlarda sorun giderirken işletim sistemi dağıtımı yöneticileri için yararlıdır. Cihazların listesini görüntülediğinizde, **Mac adresi** sütununu görünüme ekleyin. **Mac adresi** arama ölçütlerini eklemek için arama alanını kullanın.

### <a name="view-users-for-a-device"></a>Bir cihaz için kullanıcıları görüntüleme

Sürüm 1806 ' den başlayarak, **cihazlar** düğümünde aşağıdaki sütunlar mevcuttur:  

- **Birincil Kullanıcı (ler)** <!--1357280-->  

- **Şu anda oturum açmış Kullanıcı** <!--1358202-->  

    > [!NOTE]  
    > Şu anda oturum açmış olan kullanıcının görüntülenmesi için [Kullanıcı keşfi](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) ve [Kullanıcı cihaz benzeşimi](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)gerekir.  

Varsayılan olmayan bir sütunun nasıl gösterileceği hakkında daha fazla bilgi için bkz. [Yönetim Konsolu nasıl kullanılır](admin-console.md#columns).

### <a name="improvement-to-device-search-performance"></a>Cihaz arama performansı iyileştirmesi

<!-- 3614690 -->
Sürüm 1806 ' den başlayarak, bir cihaz koleksiyonunda arama yaparken, anahtar sözcüğü tüm nesne özellikleriyle aramaz. Ne arayacağını bilmiyorsanız, aşağıdaki dört Özellik genelinde arama yapar:

- Ad
- Birincil Kullanıcı (ler)
- Şu anda oturum açmış Kullanıcı
- Son oturum açma Kullanıcı adı

Bu davranış, özellikle büyük bir ortamda ada göre arama yapmak için gereken süreyi önemli ölçüde artırır. Belirli ölçütlere göre özel aramalar bu değişiklikten etkilenmez.


## <a name="software-library-workspace"></a>Yazılım Kitaplığı çalışma alanı

### <a name="order-by-program-name-in-task-sequence"></a>Görev dizisinde program adına göre sırala
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin. Bir görev dizisini düzenleyin ve [paketi Kur](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) adımını seçin ya da ekleyin. Bir pakette birden fazla program varsa, açılan liste artık programları alfabetik olarak sıralar.

### <a name="task-sequences-tab-in-applications-node"></a>Uygulamalar düğümündeki görev dizileri sekmesi
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin, **uygulamalar** düğümüne gidin ve bir uygulama seçin. Ayrıntılar bölmesinde, yeni **görev dizileri** sekmesine geçin. Bu sekmede, bu uygulamaya başvuran görev sıraları listelenmektedir.

### <a name="drill-through-required-updates"></a>Gerekli güncelleştirmeler arasında detaya gitme
<!--4224414-->
*(Sürüm 1906 ' de tanıtılmıştır)*

1. Configuration Manager konsolunda aşağıdaki yerlerden birine gidin:

   - **Yazılım kitaplığı**  >  **Yazılım güncelleştirmeleri**  >  **Tüm yazılım güncelleştirmeleri**
   - **Yazılım kitaplığı**  >  **Windows 10 Bakımı**  >  **Tüm Windows 10 güncelleştirmeleri**
   - **Yazılım kitaplığı**  >  **Office 365 Istemci yönetimi**  >  **Office 365 güncelleştirmeleri**

1. En az bir cihaz için gerekli olan herhangi bir güncelleştirmeyi seçin.
1. **Özet** sekmesine bakın ve **İstatistikler**altında Pasta grafiğini bulun.
1. Cihaz listesinin detayına gitmek için pasta grafiğinin yanındaki **gereken köprüyü görüntüle** ' yi seçin.
1. Bu eylem sizi, güncelleştirme gerektiren cihazları görebileceğiniz **cihazlarda** geçici bir düğüme götürür. Ayrıca, bir düğüm için, listeden yeni koleksiyon oluşturma gibi işlemler gerçekleştirebilirsiniz.

> [!NOTE]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

### <a name="maximize-the-browse-registry-window"></a>Kayıt Defteri penceresini en üst düzeye çıkarın

<!--3594151 includes all MMS 1902 console changes-->
*(Sürüm 1902 ' de tanıtılmıştır)*

1. **Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.
1. Bir algılama yöntemi olan dağıtım türüne sahip bir uygulama seçin. Örneğin, bir Windows Installer algılama yöntemi.
1. Ayrıntılar bölmesinde, **dağıtım türleri** sekmesine geçin.
1. Bir dağıtım türünün özelliklerini açın ve **algılama yöntemi** sekmesine geçin. **yan tümce Ekle**' yi seçin.
1. **Ayar türünü** **kayıt defteri** olarak değiştirin ve gözden geçirme **kayıt defteri** penceresini açmak için **Araştır** ' ı seçin. Artık bu pencereyi en üst düzeye çıkarabilirsiniz.  

### <a name="edit-a-task-sequence-by-default"></a>Varsayılan olarak bir görev sırasını düzenleme

*(Sürüm 1902 ' de tanıtılmıştır)*

**Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin. Şimdi **Düzenle** , bir görev dizisi açılırken varsayılan eylemdir. Daha önce varsayılan eylem **özelliklerdir**.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Uygulama dağıtımından koleksiyona git

*(Sürüm 1902 ' de tanıtılmıştır)*

1. **Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.
1. Bir uygulama seçin. Ayrıntılar bölmesinde **dağıtımlar** sekmesine geçin.
1. Bir dağıtım seçin ve ardından dağıtım sekmesindeki şeritte yeni **koleksiyon** seçeneğini belirleyin. Bu eylem, görünümü dağıtımın hedefi olan koleksiyona geçirir.
   - Bu eylem Ayrıca bu görünümdeki dağıtımda bulunan sağ tıklama bağlam menüsünde de kullanılabilir.


## <a name="monitoring-workspace"></a>İzleme çalışma alanı

### <a name="correct-names-for-client-operations"></a>İstemci işlemleri için doğru adlar
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**İzleme** çalışma alanında **istemci işlemleri**' ni seçin. **Sonraki yazılım güncelleştirme noktasına geçiş** işlemi artık düzgün şekilde adlandırılmış.

### <a name="show-collection-name-for-scripts"></a>Betikler için koleksiyon adını göster
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**İzleme** çalışma alanında **betik durumu** düğümünü seçin. Artık, KIMLIĞE ek olarak **koleksiyon adını** listeler.

### <a name="remove-content-from-monitoring-status"></a>İzleme durumundan içeriği kaldır

*(Sürüm 1902 ' de tanıtılmıştır)*

1. **İzleme** çalışma alanında **dağıtım durumu**' nu genişletin ve **İçerik durumu**' nu seçin.
1. Listeden bir öğe seçin ve Şeritteki **durumu görüntüle** seçeneğini belirleyin.
1. Varlık ayrıntıları bölmesinde, bir dağıtım noktasına sağ tıklayın ve **Kaldır**seçeneğini belirleyin. Bu eylem, bu içeriği seçili dağıtım noktasından kaldırır.

### <a name="copy-details-in-monitoring-views"></a>İzleme görünümlerinde ayrıntıları Kopyala

*(Sürüm 1806 ' de tanıtılmıştır)*
<!--1357856-->
Aşağıdaki izleme düğümleri için **varlık ayrıntıları** bölmesinden bilgileri kopyalayın:  

- **İçerik dağıtım durumu**  

- **Dağıtım Durumu**  

![Dağıtım durumu görünümü, varlık ayrıntılarını Kopyala](media/1810-deployment-status.PNG)

## <a name="administration-workspace"></a>Yönetim çalışma alanı

<!--4223683-->
Sürüm 1906 ' den başlayarak, Yönetim hizmetini kullanmak için **güvenlik** düğümü altındaki bazı düğümleri etkinleştirebilirsiniz. Bu değişiklik, konsolunun WMI üzerinden değil, HTTPS üzerinden SMS sağlayıcısıyla iletişim kurmasını sağlar. Daha fazla bilgi için bkz. [Yönetim hizmetini ayarlama](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Sonraki adımlar

- [Konsolu kullanma](admin-console.md)
- [Konsol bildirimleri](admin-console-notifications.md)
- [Erişilebilirlik özellikleri](../../understand/accessibility-features.md)