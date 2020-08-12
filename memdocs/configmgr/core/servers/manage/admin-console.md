---
title: Configuration Manager konsolu
titleSuffix: Configuration Manager
description: Configuration Manager konsolundan gezinme hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126520"
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

3. **Bağlan**’ı seçin.  

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


## <a name="next-steps"></a>Sonraki adımlar

- [Konsol bildirimleri](admin-console-notifications.md)
- [Konsol ipuçları](admin-console-tips.md)
- [Erişilebilirlik özellikleri](../../understand/accessibility-features.md)
- [Görev sırası Düzenleyicisi](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
