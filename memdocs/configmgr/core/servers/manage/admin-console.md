---
title: Configuration Manager konsolu
titleSuffix: Configuration Manager
description: Configuration Manager konsolundan gezinme hakkında bilgi edinin.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ac5b3ca8e8e2231bb421838fa56b20253ddfcb74
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878368"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Configuration Manager konsolunu kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yöneticiler, Configuration Manager ortamını yönetmek için Configuration Manager konsolunu kullanır. Bu makalede, konsolunda gezinme temelleri ele alınmaktadır.  

## <a name="open-the-console"></a><a name="bkmk_open"></a>Konsolunu açın

Configuration Manager konsolu her zaman her site sunucusuna yüklenir. Ayrıca, diğer bilgisayarlara da yükleyebilirsiniz. Daha fazla bilgi için [Configuration Manager konsolunu yüklemeye](../deploy/install/install-consoles.md)bakın.

Konsolunu bir Windows 10 bilgisayarında açmak için en basit yöntem, **Başlat** ' a basın ve yazmaya başlayın `Configuration Manager console` . En iyi eşleşmeyi bulmak için Windows 'un tüm dizesini yazmanız gerekebilir.

Başlat menüsüne gözattığınızda, **Microsoft Endpoint Manager** grubunda **Configuration Manager konsolu** simgesini arayın.

![Microsoft Uç Nokta Yöneticisi başlangıç menüsü simgeleri](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Sürüm 1910 ' de Başlat menüsü yolu değişti. Sürüm 1906 ve önceki sürümlerde, klasör adı **System Center**olur. Configuration Manager sürüm 1910 veya üzeri sürümüne güncelleştirdiğinizde, bu yeni konumu dahil etmek için tuttuğunuz tüm dahili belgeleri güncelleştirdiğinizden emin olun.

## <a name="connect-to-a-site-server"></a>Site sunucusuna bağlan

Konsol, merkezi yönetim site sunucunuza veya birincil site sunucularınıza bağlanır. Configuration Manager konsolunu ikincil bir siteye bağlanamazsınız. Yükleme sırasında, konsolunun bağlandığı site sunucusunun tam etki alanı adını (FQDN) belirttiniz.

Farklı bir site sunucusuna bağlanmak için aşağıdaki adımları kullanın:

1. [Şeridin](#ribbon)en üstündeki oku seçin ve **Yeni bir siteye Bağlan**' ı seçin.  

    ![Konsolunu yeni bir siteye bağlama](media/connect-to-a-new-site.png)  

2. Site sunucusunun FQDN 'sini yazın. Daha önce site sunucusuna bağlandıysanız, açılan listeden sunucuyu seçin.  

    ![Site bağlantısı penceresinde, site sunucusunun FQDN 'sini girin](media/site-server-fqdn.png)  

3. **Bağlan**'ı seçin.  

Sürüm 1810 ' den başlayarak, yöneticilerin Configuration Manager sitelere erişmesi için en düşük kimlik doğrulama düzeyini belirtebilirsiniz. Bu özellik, yöneticilerin Windows 'da gerekli düzeyiyle oturum açmasını zorlar. Daha fazla bilgi için bkz. [plan for SMS Provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  

## <a name="navigation"></a>Gezinti

Konsolun bazı bölgeleri, atanan güvenlik rolüne bağlı olarak görünür olmayabilir. Roller hakkında daha fazla bilgi için bkz. [rol tabanlı yönetimin temelleri](../../understand/fundamentals-of-role-based-administration.md).

### <a name="workspaces"></a>Çalışma alanları

Configuration Manager konsolunun dört **çalışma alanı**vardır:  

- **Varlıklar ve uyumluluk**  

- **Yazılım Kitaplığı**  

- **İzleme**  

- **Yönetim**  

![Bağlam menüsüyle Configuration Manager çalışma alanları](media/configuration-manager-workspaces.png)  

Aşağı oku seçerek ve **Gezinti Bölmesi seçeneklerini**belirleyerek çalışma alanı düğmelerini yeniden sıralayın. **Taşımak** veya **aşağı taşımak**için bir öğe seçin. Varsayılan düğme sırasını geri yüklemek için **Sıfırla** ' yı seçin.  

![Çalışma alanlarını yeniden sıralamak için gezinti bölmesi seçenekleri penceresi](media/navigation-pane-options.png)  

**Daha az düğme göster**' i seçerek çalışma alanı düğmesini simge durumuna küçültün. Listedeki son çalışma alanı ilk olarak en aza indirilir. Simge durumuna küçültülmüş bir düğme seçin ve düğmeyi özgün boyutuna geri yüklemek için **daha fazla düğme göster** ' i seçin.

![Configuration Manager konsolundaki küçültülmüş çalışma alanları](media/workspace-buttons.png)  

### <a name="nodes"></a>Düğümler

Çalışma alanları **düğümlerin**koleksiyonudur. Bir düğüm örneği, **yazılım kitaplığı** çalışma alanındaki **yazılım güncelleştirme grupları** düğümüdür.

Düğümde olduktan sonra, gezinti bölmesini en aza indirmek için oku seçebilirsiniz.  

![Örnek düğüm ve vurgu küçültme oku](media/software-update-groups-node.png)  

Gezinti bölmesini en aza indirgetüğünüzde konsol etrafında gezinmek için **Gezinti çubuğunu** kullanın.  

![Configuration Manager küçültülmüş Gezinti Bölmesi](media/minimized-navigation-pane.png)  

Konsolunda düğümler bazen klasörler halinde düzenlenir. Klasörünü seçtiğinizde, genellikle bir **Gezinti dizinini** veya **panoyu**görüntüler.  

![Yazılım güncelleştirmeleri gezinti dizinini Configuration Manager](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Şeridi

Şerit Configuration Manager konsolunun en üstünde bulunur. Şeritte birden fazla sekme olabilir ve sağdaki ok kullanılarak simge durumuna küçültülmüş olabilir. Şeritteki düğmeler düğüm temelinde değişir. Şeritteki düğmelerin çoğu bağlam menülerinde de mevcuttur.  

![Örnek şerit, birden çok sekmeyi vurgulama ve oku Küçült](media/ribbon.png)

### <a name="details-pane"></a>Ayrıntılar bölmesi

Ayrıntılar bölmesini inceleyerek öğeler hakkında daha fazla bilgi edinebilirsiniz. Ayrıntılar bölmesinde bir veya daha fazla sekme olabilir. Sekmeler düğüme bağlı olarak değişir.  

![Configuration Manager örnek ayrıntıları bölmesi](media/details-pane.png)

### <a name="columns"></a>Sütunlar

Sütunları ekleyebilir, kaldırabilir, yeniden sıralayabilir ve yeniden boyutlandırabilirsiniz. Bu eylemler, tercih ettiğiniz verileri görüntülemenizi sağlar. Kullanılabilir sütunlar, düğüme göre farklılık gösterir. Görünüminizden bir sütun eklemek veya bir sütunu kaldırmak için, varolan bir sütun başlığına sağ tıklayıp bir öğe seçin. Sütunları, istediğiniz sütun başlığını sürükleyerek yeniden sıralayın.  

![Yapılandırma yöneticileri sütun Ekle](media/add-columns.png)  

Sütun bağlam menüsünün en altında, bir sütuna göre sıralama veya gruplama yapabilirsiniz. Ayrıca, üst bilgisini seçerek bir sütuna göre sıralama yapabilirsiniz.  

![Sütuna göre gruplandırma Configuration Manager](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a>Nesneleri düzenlemenin geri kazanma kilidi

<!--4786915-->

Configuration Manager konsolu yanıt vermeyi durdurursa, kilit 30 dakika sonra sona erene kadar daha fazla değişiklik yapmaktan ayrılabilir. Bu kilit Configuration Manager SEDO (dağıtılmış nesnelerin serileştirilmiş düzenlemesi) sisteminin bir parçasıdır. Daha fazla bilgi için bkz. [Configuration Manager SEDO](../../../develop/core/understand/sedo.md).

[Geçerli dal sürüm 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)' den başlayarak, bir görev dizisinde kilidi temizleyebilirsiniz. Sürüm 1910 ' den başlayarak, Configuration Manager konsolundaki herhangi bir nesne üzerindeki kilidi temizleyebilirsiniz.

Bu eylem yalnızca kilidi olan Kullanıcı hesabınız için ve sitenin kilidi tarafından verilen aynı cihazda geçerlidir. Kilitli bir nesneye erişmeye çalıştığınızda artık **değişiklikleri atabilir**ve nesneyi düzenlemeyle devam edebilirsiniz. Kilidin süre dolduğunda bu değişiklikler kaybedilir.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a>Son bağlantılı konsolları görüntüle

<!--3699367-->
Sürüm 1902 ' den başlayarak, Configuration Manager konsolunun en son bağlantılarını görüntüleyebilirsiniz. Görünüm etkin bağlantıları ve yakın zamanda bağlanan bağlantıları içerir. Geçerli konsol bağlantınızı listede her zaman görürsünüz ve yalnızca Configuration Manager konsolundan bağlantıları görürsünüz. SMS sağlayıcısına PowerShell veya SDK tabanlı diğer bağlantıları görmezsiniz. Site, 30 günden eski olan listeden örnekleri kaldırır.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a>Bağlı konsolları görüntüleme önkoşulları

- Hesabınız **SMS_Site** nesnesi üzerinde **okuma** iznine sahip olmalıdır

- REST API Yönetim hizmetini yapılandırın. Daha fazla bilgi için bkz. [Yönetim hizmeti nedir?](../../../develop/adminservice/overview.md)

### <a name="view-connected-consoles"></a>Bağlı konsolları görüntüleme

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin.  

2. **Güvenlik** ' i genişletin ve **konsol bağlantıları** düğümünü seçin.  

3. Son bağlantıları aşağıdaki özelliklerle görüntüleyin:  

    - Kullanıcı adı
    - Makine adı
    - Bağlı site kodu
    - Konsol sürümü
    - Son bağlantı zamanı: Kullanıcı konsolu en son *açtığı* zaman
    - Sürüm 1910 ' den başlayarak, **son konsol sinyal** sütunu **son bağlantı saati** sütununu değiştirdi. <!--4923997-->
       - Ön planda bulunan açık bir konsol 10 dakikada bir sinyal gönderir.

![Configuration Manager konsolu bağlantılarını görüntüle](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a>Konsol bağlantılarından Microsoft ekipleri sohbetini Başlat
<!--4923997-->
*(Sürüm 1910 ' de tanıtılmıştır)*

Sürüm 1910 ' den başlayarak, Microsoft ekipleri ' nı kullanarak **konsol bağlantıları** düğümünden diğer Configuration Manager yöneticilerine ileti gönderebilirsiniz. **Microsoft ekiplerinin** bir yönetici Ile sohbet başlamasını seçtiğinizde, Microsoft ekipleri başlatılır ve kullanıcıyla bir sohbet açılır.

### <a name="prerequisites"></a>Ön koşullar

- Bir yönetici ile sohbet başlatmak için, sohbet etmek istediğiniz hesabın [Azure AD veya ad Kullanıcı keşfi](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)ile bulunması gerekir.
- Konsolunu çalıştırdığınız cihaza yüklü Microsoft ekipleri.
Not
- [Bağlı konsolları görüntülemek için tüm Önkoşullar](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Microsoft ekipleri sohbetini Başlat

1. **Yönetim**  >  **güvenlik**  >  **konsolu bağlantıları**' na gidin.
1. Kullanıcının konsol bağlantısına sağ tıklayın ve **Microsoft ekipleri sohbetini Başlat**' ı seçin.
    - Seçilen yönetici için Kullanıcı asıl adı bulunmazsa, **Microsoft ekipleri sohbeti** ' nı başlatın.
    - Konsolu çalıştırdığınız cihazda Microsoft ekipleri yüklü değilse, indirme bağlantısı dahil bir hata iletisi görüntülenir.
    - Konsolu çalıştırdığınız cihazda Microsoft ekipleri yüklüyse, kullanıcıyla bir sohbet açar.

### <a name="known-issues"></a>Bilinen sorunlar

Aşağıdaki kayıt defteri anahtarı yoksa Microsoft ekiplerinin yüklenmediğini bildiren hata iletisi gösterilmez:

Bilgisayar \ HKEY_CURRENT_USER \SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Sorunu geçici olarak çözmek için kayıt defteri anahtarını el ile oluşturun.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a>Configuration Manager konsol bildirimleri

<!--3556016, fka 1318035-->
Configuration Manager sürüm 1902 ' den başlayarak, konsolu aşağıdaki olayları size bildirir:

- Configuration Manager için bir güncelleştirme kullanılabilir olduğunda
- Ortamda yaşam döngüsü ve bakım olayları gerçekleştiğinde

Bu bildirim, şeridin altındaki konsol penceresinin en üstünde yer aldığı bir çubukdur. Configuration Manager güncelleştirmeler kullanılabilir olduğunda önceki deneyimin yerini alır. Bu konsol içi bildirimlerde hala kritik bilgiler görüntülenir, ancak konsolda çalışmalarınız kesintiye uğramaz. Kritik bildirimleri yok sayabilirsiniz. Konsol, tüm bildirimleri başlık çubuğunun yeni bir bildirim alanında görüntüler.

![Konsolda bildirim çubuğu ve bayrak](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Bir siteyi kritik olmayan bildirimleri gösterecek şekilde yapılandırma

Her bir siteyi, sitenin özelliklerinde kritik olmayan bildirimler gösterecek şekilde yapılandırabilirsiniz.

1. **Yönetim** çalışma alanında, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.
1. Kritik olmayan bildirimler için yapılandırmak istediğiniz siteyi seçin.
1. Şeritte **Özellikler**' i seçin.
1. **Uyarılar** sekmesinde, **kritik olmayan site sistem durumu değişiklikleri Için konsol bildirimlerini etkinleştirme**seçeneğini belirleyin.
   - Bu ayarı etkinleştirirseniz, tüm konsol kullanıcıları kritik, uyarı ve bilgi bildirimlerini görür. Bu ayar, varsayılan olarak etkinleştirilmiştir.  
   - Bu ayarı devre dışı bırakırsanız, konsol kullanıcıları yalnızca kritik bildirimleri görür.  

Çoğu konsol bildirimi oturum başına alınır. Konsol, bir kullanıcı tarafından başlatıldığında sorguları değerlendirir. Bildirimlerde değişiklikleri görmek için konsolunu yeniden başlatın. Bir kullanıcı kritik olmayan bir bildirimi geri alıyorsa, hala uygunsa konsol yeniden başlatıldığında yeniden bildirir.

Aşağıdaki bildirimler beş dakikada bir yeniden değerlendirmeye sahiptir:

- Site bakım modunda  
- Site kurtarma modunda  
- Site yükseltme modunda  

Bildirimler rol tabanlı yönetimin izinlerini izler. Örneğin, bir kullanıcının Configuration Manager güncelleştirmelerini görme izni yoksa, bu bildirimleri görmez.

Bazı bildirimlerin ilgili bir eylemi vardır. Örneğin, konsol sürümü site sürümüyle eşleşmiyorsa, **Yeni konsol sürümünü yükler**' i seçin. Bu eylem konsol yükleyicisini başlatır.

Aşağıdaki bildirimler, en çok Technical Preview dalı için geçerlidir:  

- Değerlendirme sürümü süre sonu 30 gün içinde (uyarı): geçerli tarih, değerlendirme sürümünün son kullanma tarihinden itibaren 30 gün içinde  
- Değerlendirme sürümünün süresi doldu (kritik): geçerli tarih, değerlendirme sürümünün sona erme tarihinden geçti  
- Konsol sürümü uyumsuzluğu (kritik): konsol sürümü site sürümüyle eşleşmiyor  
- Site yükseltme kullanılabilir (uyarı): yeni bir güncelleştirme paketi var  

Daha fazla bilgi ve sorun giderme yardımı için konsol bilgisayarındaki **Smsadminuı. log** dosyasına bakın. Varsayılan olarak, bu günlük dosyası şu yolda olur: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log` .


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a>Konsol içi belge panosu

<!--3556019 FKA 1357546-->
Configuration Manager sürüm 1902 ' den başlayarak, yeni **topluluk** çalışma alanında bir **belge** düğümü vardır. Bu düğüm Configuration Manager belge ve destek makaleleri hakkında güncel bilgiler içerir. Aşağıdaki bölümleri içerir:  

### <a name="product-documentation-library"></a>Ürün belge kitaplığı

- **Önerilen**: önemli makalelerin el ile seçkin bir listesi.
- **Popüler: geçen**aya ait en popüler makaleler.
- Son **güncelleme**: geçen aya yönelik makaleler düzeltildi.

### <a name="support-articles"></a>Destek makaleleri

- **Sorun giderme makaleleri**: Configuration Manager bileşenleri ve özellikleri sorun gidermeye yardımcı olacak Kılavuzlu yönergeler.
- **Yeni ve güncelleştirilmiş destek makaleleri**: son iki ay içinde yeni veya güncelleştirilmiş makaleler.

### <a name="troubleshooting-connection-errors"></a>Bağlantı hatalarını giderme
**Belge** düğümünün açık proxy yapılandırması yok. **Internet seçenekleri** Denetim Masası uygulamasında herhangi bir işletim sistemi tanımlı ara sunucu kullanır. Bir bağlantı hatasından sonra yeniden denemek için **belge** düğümünü yenileyin.


## <a name="command-line-options"></a>Komut satırı seçenekleri

Configuration Manager konsolu aşağıdaki komut satırı seçeneklerine sahiptir:

|Seçenek|Açıklama|  
|------------|-----------------|  
|`/sms:debugview=1`|Bir DebugView, bir görünümü belirten tüm ResultViews 'a dahildir. DebugView ham özellikleri gösterir (adlar ve değerler).|  
|`/sms:NamespaceView=1`|Konsolda ad alanı görünümünü gösterir.|  
|`/sms:ResetSettings`|Konsol, Kullanıcı tarafından kalıcı bağlantıyı yoksayar ve durumları görüntüler. Pencere boyutu sıfırlanmıyor.|  
|`/sms:IgnoreExtensions`|Tüm Configuration Manager uzantılarını devre dışı bırakır.|  
|`/sms:NoRestore`|Konsol, önceki kalıcı düğüm gezintisini yoksayar.|  


## <a name="tips"></a>İpuçları

### <a name="general"></a>Genel

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a>Konsol aramasında iyileştirmeler
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

#### <a name="role-based-administration-for-folders"></a>Klasörler için rol tabanlı yönetim
<!--3600867-->
*(Sürüm 1906 ' de tanıtılmıştır)*

Klasörler üzerinde güvenlik kapsamları ayarlayabilirsiniz. Klasör içindeki bir nesneye erişiminiz varsa ancak klasöre erişiminiz yoksa, nesneyi göremezsiniz. Benzer şekilde, bir klasöre erişiminiz varsa ancak içinde bir nesne yoksa, bu nesneyi görmezsiniz. Bir klasöre sağ tıklayın, **güvenlik kapsamlarını ayarla**' yı seçin ve ardından uygulamak istediğiniz güvenlik kapsamlarını seçin.

#### <a name="views-sort-by-integer-values"></a>Görünümler tamsayı değerlerine göre sıralanır

*(Sürüm 1902 ' de tanıtılmıştır)*

Çeşitli görünümlerin verileri nasıl sıraladığımızda geliştirmeler yaptık. Örneğin, **izleme** çalışma alanının **dağıtımlar** düğümünde aşağıdaki sütunlar artık dize değerleri yerine sayı olarak sıralanır:  

- Hata sayısı
- Devam eden sayı
- Diğer sayı
- Başarı sayısı
- Bilinmeyen sayı  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>Uyarıyı çok sayıda sonuç için taşıma

*(Sürüm 1902 ' de tanıtılmıştır)*

Konsolda 1.000 'den fazla sonuç döndüren bir düğüm seçtiğinizde, Configuration Manager aşağıdaki uyarıyı gösterir:

> Configuration Manager çok sayıda sonuç döndürdü. Aramayı kullanarak sonuçlarınızı daraltabilirsiniz. Veya en fazla 100000 sonucu görüntülemek için buraya tıklayın.

Bu uyarı ve arama alanı arasında artık ek boş alan var. Bu taşıma, daha fazla sonuç göstermek için uyarının yanlışlıkla seçilmesine engel olmaya yardımcı olur.

#### <a name="send-feedback"></a>Geri bildirim gönder

*(Sürüm 1806 ' de tanıtılmıştır)*
<!--1357542-->

Konsolundan ürün geri bildirimi gönderin.  

- **Gülümseme Gönder**: beğendikleriniz hakkında geri bildirim gönderin  

- **Kaş çatma Gönder**: beğendikleriniz hakkında geri bildirim gönderin  

- **Öneri gönderin**: fikrinizi paylaşmak Için sizi UserVoice 'a götürür  

Daha fazla bilgi için bkz. [ürün geri bildirimi](../../understand/find-help.md#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Varlıklar ve uyum çalışma alanı

#### <a name="real-time-actions-from-device-lists"></a>Cihaz listelerinden gerçek zamanlı eylemler
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**Varlıklar ve uyum** çalışma alanındaki **cihazlar** düğümü altında cihazların listesini görüntülemenin çeşitli yolları vardır.

- **Varlıklar ve uyum** çalışma alanında, **Cihaz Koleksiyonları** düğümünü seçin. Bir cihaz koleksiyonu seçin ve **üyeleri göstermek**için eylemi seçin. Bu eylem, bu koleksiyon için bir cihaz listesi olan **Devices** düğümünün bir alt düğümünü açar.  

  - Koleksiyon alt düğümü ' nü seçtiğinizde, artık şeridin koleksiyon grubundan **CMPivot** başlatabilirsiniz.  

- **İzleme** çalışma alanında, **dağıtımlar** düğümünü seçin. Bir dağıtım seçin ve Şeritteki **durumu görüntüle** eylemini seçin. Dağıtım durumu bölmesinde, bir cihaz listesine gitmek için toplam varlıklara çift tıklayın.  

  - Bu listede bir cihaz seçtiğinizde, artık **CMPivot** başlatabilir ve şerit 'in cihaz grubundan **betikleri çalıştırabilirsiniz** .  


#### <a name="collections-tab-in-devices-node"></a>Cihazlar düğümünde koleksiyonlar sekmesi
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**Varlıklar ve uyum** çalışma alanında, **cihazlar** düğümüne gidin ve bir cihaz seçin. Ayrıntılar bölmesinde, yeni **koleksiyonlar** sekmesine geçin. Bu sekme, bu cihazı içeren koleksiyonları listeler. 

> [!Note]  
> - Bu sekme şu anda **Cihaz Koleksiyonları** düğümünün altındaki cihazlar alt düğümünden kullanılamaz. Örneğin, bir koleksiyondaki **üyeleri gösterme** seçeneğini belirlediğinizde.
> - Bu sekme bazı kullanıcılar için beklendiği gibi doldurulamayabilir. Bir cihazın ait olduğu koleksiyonların tam listesini görmek için, **tam yönetici** güvenlik rolüne sahip olmanız gerekir. Bu bilinen bir sorundur. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Cihaz ve cihaz koleksiyonu düğümlerine SMBıOS GUID sütunu Ekle

*(Sürüm 1906 ' de tanıtılmıştır)*

<!--4526580-->
Hem **cihazlarda** hem de **Cihaz Koleksiyonları** DÜĞÜMLERINDE, artık **SMBIOS GUID**için yeni bir sütun ekleyebilirsiniz. Bu değer, sistem kaynak sınıfının **BIOS GUID** özelliği ile aynıdır. Cihaz donanımı için benzersiz bir tanımlayıcıdır.

#### <a name="search-device-views-using-mac-address"></a>MAC adresini kullanarak cihaz görünümlerini ara

<!--3600878-->
*(Sürüm 1902 ' de tanıtılmıştır)*

Bir MAC adresini Configuration Manager konsolunun bir cihaz görünümünde arayabilirsiniz. Bu özellik, PXE tabanlı dağıtımlarda sorun giderirken işletim sistemi dağıtımı yöneticileri için yararlıdır. Cihazların listesini görüntülediğinizde, **Mac adresi** sütununu görünüme ekleyin. **Mac adresi** arama ölçütlerini eklemek için arama alanını kullanın.

#### <a name="view-users-for-a-device"></a>Bir cihaz için kullanıcıları görüntüleme

Sürüm 1806 ' den başlayarak, **cihazlar** düğümünde aşağıdaki sütunlar mevcuttur:  

- **Birincil Kullanıcı (ler)** <!--1357280-->  

- **Şu anda oturum açmış Kullanıcı** <!--1358202-->  

    > [!NOTE]  
    > Şu anda oturum açmış olan kullanıcının görüntülenmesi için [Kullanıcı keşfi](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) ve [Kullanıcı cihaz benzeşimi](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)gerekir.  

Varsayılan olmayan bir sütunun nasıl gösterileceği hakkında daha fazla bilgi için bkz. [sütunlar](#columns).

#### <a name="improvement-to-device-search-performance"></a>Cihaz arama performansı iyileştirmesi

<!-- 3614690 -->
Sürüm 1806 ' den başlayarak, bir cihaz koleksiyonunda arama yaparken, anahtar sözcüğü tüm nesne özellikleriyle aramaz. Ne arayacağını bilmiyorsanız, aşağıdaki dört Özellik genelinde arama yapar:

- Name
- Birincil Kullanıcı (ler)
- Şu anda oturum açmış Kullanıcı
- Son oturum açma Kullanıcı adı

Bu davranış, özellikle büyük bir ortamda ada göre arama yapmak için gereken süreyi önemli ölçüde artırır. Belirli ölçütlere göre özel aramalar bu değişiklikten etkilenmez.


### <a name="software-library-workspace"></a>Yazılım Kitaplığı çalışma alanı

#### <a name="order-by-program-name-in-task-sequence"></a>Görev dizisinde program adına göre sırala
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin. Bir görev dizisini düzenleyin ve [paketi Kur](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) adımını seçin ya da ekleyin. Bir pakette birden fazla program varsa, açılan liste artık programları alfabetik olarak sıralar.

#### <a name="task-sequences-tab-in-applications-node"></a>Uygulamalar düğümündeki görev dizileri sekmesi
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin, **uygulamalar** düğümüne gidin ve bir uygulama seçin. Ayrıntılar bölmesinde, yeni **görev dizileri** sekmesine geçin. Bu sekmede, bu uygulamaya başvuran görev sıraları listelenmektedir.

#### <a name="drill-through-required-updates"></a>Gerekli güncelleştirmeler arasında detaya gitme
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
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](https://docs.microsoft.com/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

#### <a name="maximize-the-browse-registry-window"></a>Kayıt Defteri penceresini en üst düzeye çıkarın

<!--3594151 includes all MMS 1902 console changes-->
*(Sürüm 1902 ' de tanıtılmıştır)*

1. **Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.
1. Bir algılama yöntemi olan dağıtım türüne sahip bir uygulama seçin. Örneğin, bir Windows Installer algılama yöntemi.
1. Ayrıntılar bölmesinde, **dağıtım türleri** sekmesine geçin.
1. Bir dağıtım türünün özelliklerini açın ve **algılama yöntemi** sekmesine geçin. **yan tümce Ekle**' yi seçin.
1. **Ayar türünü** **kayıt defteri** olarak değiştirin ve gözden geçirme **kayıt defteri** penceresini açmak için **Araştır** ' ı seçin. Artık bu pencereyi en üst düzeye çıkarabilirsiniz.  

#### <a name="edit-a-task-sequence-by-default"></a>Varsayılan olarak bir görev sırasını düzenleme

*(Sürüm 1902 ' de tanıtılmıştır)*

**Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin. Şimdi **Düzenle** , bir görev dizisi açılırken varsayılan eylemdir. Daha önce varsayılan eylem **özelliklerdir**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Uygulama dağıtımından koleksiyona git

*(Sürüm 1902 ' de tanıtılmıştır)*

1. **Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.
1. Bir uygulama seçin. Ayrıntılar bölmesinde **dağıtımlar** sekmesine geçin.
1. Bir dağıtım seçin ve ardından dağıtım sekmesindeki şeritte yeni **koleksiyon** seçeneğini belirleyin. Bu eylem, görünümü dağıtımın hedefi olan koleksiyona geçirir.
   - Bu eylem Ayrıca bu görünümdeki dağıtımda bulunan sağ tıklama bağlam menüsünde de kullanılabilir.


### <a name="monitoring-workspace"></a>İzleme çalışma alanı

#### <a name="correct-names-for-client-operations"></a>İstemci işlemleri için doğru adlar
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**İzleme** çalışma alanında **istemci işlemleri**' ni seçin. **Sonraki yazılım güncelleştirme noktasına geçiş** işlemi artık düzgün şekilde adlandırılmış.

#### <a name="show-collection-name-for-scripts"></a>Betikler için koleksiyon adını göster
<!--4616810-->
*(Sürüm 1906 ' de tanıtılmıştır)*

**İzleme** çalışma alanında **betik durumu** düğümünü seçin. Artık, KIMLIĞE ek olarak **koleksiyon adını** listeler.

#### <a name="remove-content-from-monitoring-status"></a>İzleme durumundan içeriği kaldır

*(Sürüm 1902 ' de tanıtılmıştır)*

1. **İzleme** çalışma alanında **dağıtım durumu**' nu genişletin ve **İçerik durumu**' nu seçin.
1. Listeden bir öğe seçin ve Şeritteki **durumu görüntüle** seçeneğini belirleyin.
1. Varlık ayrıntıları bölmesinde, bir dağıtım noktasına sağ tıklayın ve **Kaldır**seçeneğini belirleyin. Bu eylem, bu içeriği seçili dağıtım noktasından kaldırır.

#### <a name="copy-details-in-monitoring-views"></a>İzleme görünümlerinde ayrıntıları Kopyala

*(Sürüm 1806 ' de tanıtılmıştır)*
<!--1357856-->
Aşağıdaki izleme düğümleri için **varlık ayrıntıları** bölmesinden bilgileri kopyalayın:  

- **İçerik dağıtım durumu**  

- **Dağıtım durumu**  

![Dağıtım durumu görünümü, varlık ayrıntılarını Kopyala](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Yönetim çalışma alanı

<!--4223683-->
Sürüm 1906 ' den başlayarak, Yönetim hizmetini kullanmak için **güvenlik** düğümü altındaki bazı düğümleri etkinleştirebilirsiniz. Bu değişiklik, konsolunun WMI üzerinden değil, HTTPS üzerinden SMS sağlayıcısıyla iletişim kurmasını sağlar. Daha fazla bilgi için bkz. [Yönetim hizmetini ayarlama](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Sonraki adımlar

[Erişilebilirlik özellikleri](../../understand/accessibility-features.md)

[Görev sırası Düzenleyicisi](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
