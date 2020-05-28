---
title: Office 365 ProPlus güncelleştirmelerini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager, güncelleştirmeleri istemcilere dağıtmak üzere kullanılabilir hale getirmek için, WSUS kataloğundaki Office 365 istemci güncelleştirmelerini site sunucusuna eşitler.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 09d8f0a37e9ed4308c5c8ffcf005c788612be235
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709511"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Configuration Manager ile Office 365 ProPlus’ı yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Note]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](https://docs.microsoft.com/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

Configuration Manager, Office 365 ProPlus uygulamalarını aşağıdaki yollarla yönetmenizi sağlar:

- [Office 365 uygulamalarını dağıtma](#deploy-office-365-apps): ilk Office 365 uygulama yükleme deneyimini kolaylaştırmak için Office [365 Istemci yönetimi panosundan](office-365-dashboard.md) Office 365 yükleyicisini başlatabilirsiniz. Sihirbaz, Office 365 yükleme ayarlarını yapılandırmanıza, Office Içerik teslim ağlarından (CDNs) dosya yüklemenize ve içerikle bir betik uygulaması oluşturmanıza ve dağıtmanıza olanak tanır.

- [Office 365 güncelleştirmelerini dağıtma](#deploy-office-365-updates): Office 365 istemci güncelleştirmelerini yazılım güncelleştirme yönetimi iş akışını kullanarak yönetebilirsiniz. Microsoft, Office İçerik Dağıtım Ağı’nda (CDN) yeni bir Office 365 istemcisi güncelleştirmesi yayımlarken, Windows Server Update Services’de (WSUS) de bir güncelleştirme paketi yayımlar. Configuration Manager, Office 365 istemci güncelleştirmesini WSUS kataloğundan site sunucusuna eşitledikten sonra, bu güncelleştirme istemcilere dağıtmak için kullanılabilir.

   > [!NOTE]
   > Configuration Manager sürüm 2002 ' den başlayarak, Office 365 güncelleştirmelerini bağlantısı kesilen ortamlara aktarabilirsiniz. Daha fazla bilgi için bkz. [Office 365 güncelleştirmelerini bağlantısı kesilen bir yazılım güncelleştirme noktasından Synchronize](../get-started/synchronize-office-updates-disconnected.md).   

- [Office 365 güncelleştirme indirmeleri için dil ekleme](#bkmk_o365_lang): Office 365 tarafından desteklenen tüm diller için güncelleştirmeleri indirmek üzere Configuration Manager için destek ekleyebilirsiniz. Configuration Manager, Office 365 ' i olduğu sürece dili desteklemek zorunda değildir. Configuration Manager sürüm 1610 ' den önce, güncelleştirmeleri Office 365 istemcilerinde yapılandırılmış aynı dillerde indirmeniz ve dağıtmanız gerekir.

- [Güncelleştirme kanalını değiştirme](#bkmk_channel): güncelleştirme kanalını değiştirmek için bir kayıt defteri anahtar değeri değişikliğini Office 365 istemcilerine dağıtmak üzere Grup İlkesi 'ni kullanabilirsiniz.

Office 365 istemci bilgilerini gözden geçirmek ve bu Office 365 Yönetim eylemlerinden bazılarını başlatmak için [office 365 Istemci yönetimi panosunu](office-365-dashboard.md)kullanın.

## <a name="deploy-office-365-apps"></a>Office 365 uygulamalarını dağıtma  
Office 365 Istemci yönetimi panosundan Office 365 yükleyicisini ilk Office 365 uygulama yüklemesi için başlatın. Sihirbaz, Office 365 yükleme ayarlarını yapılandırmanıza, Office Içerik teslim ağlarından (CDNs) dosya yüklemenize ve dosyalar için bir betik uygulaması oluşturmanıza ve dağıtmanıza olanak tanır. Office 365, istemcilere yüklenip [Office otomatik güncelleştirmeler görevi](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) çalıştırılıncaya kadar, Office 365 güncelleştirmeleri uygulanamaz. Test amacıyla, güncelleştirme görevini el ile çalıştırabilirsiniz.

Önceki Configuration Manager sürümler için, istemcilerde ilk kez Office 365 uygulamalarını yüklemek üzere aşağıdaki adımları uygulamanız gerekir:
- Office 365 dağıtım aracı 'Nı (ODT) indirin
- İhtiyaç duyduğunuz dil paketleri dahil olmak üzere Office 365 yükleme kaynak dosyalarını indirin.
- Doğru Office sürümünü ve kanalını belirten Configuration. xml dosyası oluşturun.
- Office 365 uygulamalarını yüklemek için istemciler için eski bir paket ya da bir betik uygulaması oluşturun ve dağıtın.

### <a name="requirements"></a>Gereksinimler
- Office 365 yükleyicisini çalıştıran bilgisayarın Internet erişimi olmalıdır.  
- Office 365 yükleyicisini çalıştıran kullanıcının, sihirbazda belirtilen içerik konumu paylaşımında **okuma** ve **yazma** erişimi olmalıdır.
- 404 indirme hatası alırsanız, şu dosyaları Kullanıcı% TEMP% klasörüne kopyalayın:
  - [releasehistory. xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit. xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Configuration Manager sürüm 1806 veya üstünü kullanarak Office 365 uygulamalarını dağıtın: 
Configuration Manager 1806 ' den başlayarak Office Özelleştirme Aracı, Configuration Manager konsolundaki Office 365 yükleyicisi ile tümleşiktir. Office 365 için bir dağıtım oluştururken, en yeni Office yönetilebilirlik ayarlarını dinamik olarak yapılandırabilirsiniz. <!--1358149-->

1. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **genel bakış**  >  **Office 365 istemci yönetimi**' ne gidin.
2. Sağ üst bölmedeki **Office 365 yükleyicisi** ' ne tıklayın. Office 365 Istemci Yükleme Sihirbazı açılır.
3. **Uygulama ayarları** sayfasında, uygulama için bir ad ve açıklama sağlayın, dosyalar için karşıdan yükleme konumunu girin ve ardından **İleri**' ye tıklayın. Konumun &#92;&#92;*server*&#92;*Share*olarak belirtilmesi gerekir.
4. **Office ayarları** sayfasında **Office özelleştirme aracına git ' e**tıklayın. Bu, tıkla- [Çalıştır Için Office Özelleştirme Aracı](https://config.office.com)açılır.
5. Office 365 yüklemeniz için istenen ayarları yapılandırın. Yapılandırmayı tamamladığınızda sayfanın sağ üst kısmındaki **Gönder** ' e tıklayın. 
6. **Dağıtım** sayfasında, şimdi mi yoksa daha sonra mı dağıtmak istediğinizi saptayın. Daha sonra dağıtmayı seçerseniz, uygulamayı **yazılım kitaplığı**  >  **uygulama yönetimi**  >  **uygulamalarında**bulabilirsiniz.  
7. **Özet** sayfasında ayarları onaylayın. 
8. **İleri** ' ye tıkladıktan sonra Office 365 Istemci Yükleme Sihirbazı tamamlandıktan sonra **Kapat** ' a tıklayın. 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Configuration Manager sürüm 1802 ve öncesi ile Office 365 uygulamalarını dağıtın:

1. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **genel bakış**  >  **Office 365 istemci yönetimi**' ne gidin.
2. Sağ üst bölmedeki **Office 365 yükleyicisi** ' ne tıklayın. Office 365 Istemci Yükleme Sihirbazı açılır.
3. **Uygulama ayarları** sayfasında, uygulama için bir ad ve açıklama sağlayın, dosyalar için karşıdan yükleme konumunu girin ve ardından **İleri**' ye tıklayın. Konumun &#92;&#92;*server*&#92;*Share*olarak belirtilmesi gerekir.
4. **Istemci ayarlarını Içeri aktar** sayfasında, mevcut bir XML yapılandırma dosyasından Office 365 istemci ayarlarını içeri aktarıp aktarmayacağını veya ayarları el ile belirtmek için seçin. İşiniz bittiğinde **İleri** ' ye tıklayın.  

    Varolan bir yapılandırma dosyanız varsa, dosyanın konumunu girin ve 7. adıma atlayın.  &#92;&#92;*sunucu*&#92;*Share*&#92;*filename*biçiminde bir konum belirtmeniz gerekir. 'Sini.
    > [!IMPORTANT]    
    > XML yapılandırma dosyası yalnızca [Office 365 ProPlus istemcisinin desteklediği dilleri](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016)içermelidir.

5. **Istemci ürünleri** sayfasında, kullandığınız Office 365 paketini seçin. Dahil etmek istediğiniz uygulamaları seçin. Dahil edilecek ek Office ürünlerini seçin ve ardından **İleri**' ye tıklayın.
6. **Istemci ayarları** sayfasında, dahil edilecek ayarları seçin ve ardından **İleri**' ye tıklayın.
7. **Dağıtım** sayfasında, uygulamayı dağıtıp dağıtmeyeceğinizi seçin ve ardından **İleri**' ye tıklayın. <br/>Paketi sihirbazda dağıtmamalıdır seçeneğini belirlerseniz adım 9 ' a atlayın.
8. Sihirbaz sayfalarının geri kalanını tipik bir uygulama dağıtımında yaptığınız gibi yapılandırın. Ayrıntılar için bkz. [uygulama oluşturma ve dağıtma](../../apps/get-started/create-and-deploy-an-application.md).
9. Sihirbazı tamamlayın.
10. Uygulamayı **yazılım kitaplığı**  >  **'na genel bakış**  >  **uygulama yönetimi**  >  **uygulamalarından**dağıtabilir veya düzenleyebilirsiniz.    

Office 365 yükleyicisini kullanarak Office 365 uygulamaları oluşturup dağıttıktan sonra, Configuration Manager Office güncelleştirmelerini varsayılan olarak yönetmez. Office 365 istemcilerinin Configuration Manager güncelleştirmeleri almasını etkinleştirmek için, bkz. [Configuration Manager Ile office 365 güncelleştirmelerini dağıtma](#deploy-office-365-updates).

Office 365 uygulamalarını dağıttıktan sonra, uygulamaları sürdürmek için otomatik dağıtım kuralları oluşturabilirsiniz. Office 365 uygulamaları için bir otomatik dağıtım kuralı oluşturmak üzere [office 365 Istemci yönetimi PANOSUNDAN](office-365-dashboard.md) **ADR oluştur** ' a tıklayın. Ürünü seçerken **Office 365 istemcisi** ' ni seçin. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](automatically-deploy-software-updates.md).


## <a name="drill-through-required-office-365-updates"></a>Gerekli Office 365 güncelleştirmelerinde detaya gitme
<!--4224414-->
*(Sürüm 1906 ' de tanıtılmıştır)*

Hangi cihazların belirli bir Office 365 yazılım güncelleştirmesi gerektirdiğini görmek için uyumluluk istatistikleri detayına gidebilirsiniz. Cihaz listesini görüntülemek için, cihazların ait olduğu güncelleştirmeleri ve koleksiyonları görüntülemek için izninizin olması gerekir. Cihaz listesinin detayına gitmek için:

1. **Yazılım kitaplığı**  >  **Office 365 istemci yönetimi**  >  **Office 365 güncelleştirmeleri**' ne gidin.
1. En az bir cihaz için gerekli olan herhangi bir güncelleştirmeyi seçin.
1. **Özet** sekmesine bakın ve **İstatistikler**altında Pasta grafiğini bulun.
1. Cihaz listesinin detayına gitmek için pasta grafiğinin yanındaki **gereken köprüyü görüntüle** ' yi seçin.
1. Bu eylem sizi, güncelleştirme gerektiren cihazları görebileceğiniz **cihazlarda** geçici bir düğüme götürür. Ayrıca, bir düğüm için, listeden yeni koleksiyon oluşturma gibi işlemler gerçekleştirebilirsiniz.


## <a name="deploy-office-365-updates"></a>Office 365 güncelleştirmelerini dağıtma

Configuration Manager ile Office 365 güncelleştirmelerini dağıtmak için aşağıdaki adımları kullanın:

1. Makalenin **office 365 istemci güncelleştirmelerini yönetmek için Configuration Manager kullanma gereksinimlerinde** Office 365 istemci güncelleştirmelerini yönetmek için Configuration Manager kullanma [gereksinimlerini doğrulayın](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) .  

2. [Yazılım güncelleştirme noktalarını](../get-started/configure-classifications-and-products.md) , Office 365 istemci güncelleştirmelerini eşitleyecek şekilde yapılandırın. Sınıflandırma için **güncelleştirmeleri** ayarlayın ve ürün için **Office 365 istemcisini** seçin. **Güncelleştirme** sınıflandırmasını kullanmak için yazılım güncelleştirme noktalarını yapılandırdıktan sonra yazılım güncelleştirmelerini eşitler.
3. Office 365 istemcilerinin Configuration Manager güncelleştirmeleri almasını etkinleştirin. İstemciyi etkinleştirmek için Configuration Manager istemci ayarları veya Grup İlkesi kullanın.

    **Yöntem 1**: Configuration Manager sürüm 1606 ' den başlayarak, Office 365 istemci aracısını yönetmek için Configuration Manager istemci ayarını kullanabilirsiniz. Bu ayarı yapılandırdıktan ve Office 365 güncelleştirmelerini dağıttıktan sonra, Configuration Manager istemci Aracısı, güncelleştirmeleri bir dağıtım noktasından indirmek ve onları yüklemek için Office 365 istemci aracısıyla iletişim kurar. Configuration Manager, Office 365 ProPlus Istemci ayarlarının envanterini alır.    

      1. Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **istemci ayarları**' na tıklayın.  

      2. İstemci aracısını etkinleştirmek için uygun cihaz ayarlarını açın. Varsayılan ve özel istemci ayarları hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).  

      3. **Yazılım güncelleştirmeleri** ' ne tıklayın ve **Office 365 istemci Aracısı ayarının yönetimini etkinleştirmek** için **Evet** ' i seçin.  

    **Yöntem 2**: Office dağıtım aracını veya Grup İlkesi kullanarak [office 365 istemcilerinin Configuration Manager güncelleştirmeleri almasını etkinleştirin](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) .  

4. [Office 365 güncelleştirmelerini Istemcilere dağıtın](deploy-software-updates.md) .

> [!Important]
> - Configuration Manager sürüm 1706 ' den başlayarak Office 365 istemci güncelleştirmeleri **Office 365 istemci yönetimi**  > **Office 365 Updates** düğümüne taşınmıştır. Bu taşıma geçerli ADR yapılandırmanızı etkilemez. 
> - Configuration Manager sürüm 1610 ' den önce, güncelleştirmeleri Office 365 istemcilerinde yapılandırılmış aynı dillerde indirmeniz ve dağıtmanız gerekir. Örneğin, en-US ve de aynı dillerde yapılandırılmış bir Office 365 istemciniz olduğunu varsayalım. Site sunucusunda, geçerli bir Office 365 güncelleştirmesi için yalnızca en-US içeriğini indirip dağıtırsınız. Kullanıcı bu güncelleştirme için yazılım merkezi 'nden yüklemeyi başlattığında güncelleştirme, içeriği de karşıdan yüklerken askıda kalır. 

> [!NOTE]  
>
> Office 365 ProPlus son zamanlarda yüklenmişse ve nasıl yüklendiğine bağlı olarak, güncelleştirme kanalının henüz ayarlanmamış olması mümkündür. Bu durumda, dağıtılan güncelleştirmeler geçerli değil olarak algılanır. Office 365 ProPlus yüklendiğinde, [Zamanlanmış bir otomatik güncelleştirmeler görevi](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) oluşturulur. Bu durumda, güncelleştirme kanalının ayarlanması ve güncelleştirmelerin uygun olarak algılanabilmesi için bu görevin en az bir kez çalışması gerekir.
>
> Office 365 ProPlus son zamanlarda yüklenmişse ve dağıtılan güncelleştirmeler algılanmamışsa, sınama amacıyla, Office otomatik güncelleştirmeler görevini el ile başlatabilir ve ardından istemcide [yazılım güncelleştirmeleri dağıtımı değerlendirme döngüsünü](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) başlatabilirsiniz. Bunu bir görev dizisinde nasıl yapacağınız hakkında yönergeler için bkz. [bir görev dizisinde Office 365 ProPlus 'ı güncelleştirme](manage-office-365-proplus-updates.md#updating-office-365-proplus-in-a-task-sequence).

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Office 365 güncelleştirmeleri için yeniden başlatma davranışı ve istemci bildirimleri
Office 365 istemcisine bir güncelleştirme dağıttığınızda, yeniden başlatma davranışı ve istemci bildirimleri Configuration Manager sürümüne bağlı olarak farklıdır. Aşağıdaki tabloda, istemci bir Office 365 güncelleştirmesi aldığında Son Kullanıcı deneyimi hakkında bilgi verilmektedir:

|Configuration Manager sürümü |Son kullanıcı deneyimi|  
|----------------|---------------------|
|1706, 1710|İstemci, güncelleştirmeyi yüklemeden önce açılır ve uygulama içi bildirimlerin yanı sıra geri sayım iletişim kutusunu da alır.|
|1802| İstemci, güncelleştirmeyi yüklemeden önce açılır ve uygulama içi bildirimlerin yanı sıra geri sayım iletişim kutusunu da alır. </br>Office 365 istemci güncelleştirme zorlaması sırasında Office 365 uygulamaları çalışıyorsa, Office uygulamaları kapanmaya zorlanmaz. Bunun yerine, güncelleştirme yüklemesi sistemin yeniden başlatılmasını gerektirir. <!--510006-->|


> [!Important]
>
>Configuration Manager sürüm 1706 ' de, aşağıdaki ayrıntılara göz önünde yer verilmiştir:
>
>- Son tarihin 48 saat içinde olduğu ve güncelleştirme içeriğinin indirileceği gerekli uygulamalar için görev çubuğundaki bildirim alanında bildirim simgesi görüntülenir. 
>- Son tarihin 7,5 saat içinde olduğu ve güncelleştirmenin indirileceği gerekli uygulamalar için bir geri sayım iletişim kutusu görüntülenir. Kullanıcı, geri sayım iletişim kutusunu son tarihten en fazla üç kez erteleyebilir. Ertelendiğinde geri sayım iki saat sonra yeniden görüntülenir. Ertelenmiyorsa, geri sayım süresi dolduğunda 30 dakikalık bir geri sayım ve güncelleştirme yüklenir.
>- Kullanıcı bildirim alanındaki simgeye tıklayana kadar bir açılır bildirim görüntülenmeyebilir. Ayrıca, bildirim alanında minimum alan varsa bildirim simgesi Kullanıcı bildirim alanını açana veya genişletmediği takdirde görünür olmayabilir. 
>- Kullanıcı cihazda etkin bir şekilde çalışmaması durumunda bildirim ve geri sayım iletişim kutusu başlatılabilir. Örneğin, cihaz kilitlendiğinde gece boyunca cihaz üzerinde çalışan olası Office uygulamaları, güncelleştirmeyi yüklemek için kapanmaya zorlanabilir. Office, uygulamayı kapatmadan önce veri kaybını engellemek için uygulama verilerini kaydeder. 
>- Son Tarih geçmişte veya en kısa sürede başlatılacak şekilde yapılandırıldıysa, çalışan Office uygulamaları, bildirim olmadan kapanmaya zorlanabilir. 
>- Kullanıcı son tarihten önce bir Office güncelleştirmesi yüklerse, son tarihe ulaşıldığında güncelleştirmenin yüklendiğini doğrular Configuration Manager. Güncelleştirme cihazda algılanmazsa, güncelleştirme yüklenir. 
>- Uygulama içi bildirim çubuğu, güncelleştirme indirilmeden önce çalıştıran bir Office uygulamasında görüntülenmez. Güncelleştirme indirildikten sonra, uygulama içi bildirim yalnızca yeni açılan uygulamalar için görüntülenir.
>- Bir hizmet penceresi tarafından tetiklenen veya iş dışı saatlere yönelik olarak zamanlanan Office güncelleştirmeleri için, Office uygulamalarını çalıştırmak, güncelleştirmeyi bildirim olmadan yüklemek için kapanmaya zorlanacaktır. 
>- Daha fazla bilgi için bkz. [Office 365 Için Son Kullanıcı güncelleştirme bildirimleri](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)


## <a name="add-languages-for-office-365-update-downloads"></a><a name="bkmk_o365_lang"></a>Office 365 güncelleştirme indirmeleri için dil ekleme
Office 365 tarafından desteklenen tüm diller için güncelleştirmeleri indirmek üzere Configuration Manager için destek ekleyebilirsiniz.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Sürüm 1902 ' de ek diller için güncelleştirmeleri indirin
<!--3555955-->

Configuration Manager sürüm 1902 ' den başlayarak güncelleştirme iş akışı, **Windows Update** için 38 dillerini **Office 365 istemci güncelleştirmesi**için çok sayıda ek dilde ayırır.

Gerekli dilleri seçmek için aşağıdaki konumlarda bulunan **Dil seçimi** sayfasını kullanın:
- Otomatik dağıtım kuralı oluşturma Sihirbazı
- Yazılım güncelleştirmelerini dağıtma Sihirbazı
- Yazılım güncelleştirmelerini indirme Sihirbazı
- Otomatik dağıtım kuralı özellikleri

**Dil seçimi** sayfasında, **Office 365 istemci güncelleştirmesi**' ni seçin ve ardından **Düzenle**' ye tıklayın. Office 365 için gereken dilleri ekleyin ve ardından **Tamam**' a tıklayın.

![Office 365 için ek dil ekleme ekran görüntüsü](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Sürüm 1810 ve önceki sürümlerde ek diller için güncelleştirmeleri indirme desteği eklemek için

Merkezi yönetim sitesindeki veya tek başına birincil sitedeki yazılım güncelleştirme noktasında aşağıdaki yordamı kullanın.

> [!IMPORTANT]  
> Ek Office 365 güncelleştirme dillerini yapılandırmak site genelinde bir ayardır. Aşağıdaki yordamı kullanarak dilleri ekledikten sonra, tüm Office 365 güncelleştirmeleri bu dillerde indirilir, ayrıca yazılım güncelleştirmelerini Indir veya yazılım güncelleştirmelerini dağıtma sihirbazları 'ndaki **Dil seçimi** sayfasında seçtiğiniz diller de bulunur.

1. Bir komut isteminden, Windows Yönetim Araçları test ediciyi açmak için yönetici kullanıcı olarak *WBEMTest* yazın.
2. **Bağlan**' a tıklayın ve *root\sms\ Site_ &lt; sitekodu &gt; *yazın.
3. **Sorgu**' ya tıklayın ve ardından şu sorguyu çalıştırın: *&#42; SMS_SCI_Component WHERE ComponentName = "SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![WMI sorgusu](../media/1-wmiquery.png)
4. Sonuçlar bölmesinde, merkezi yönetim sitesi veya tek başına birincil site için site kodu ile nesneye çift tıklayın.
5. **Props** özelliğini seçin, **özelliği Düzenle**' ye tıklayın ve ardından **gömülü görünüm**' e tıklayın.
   ![Özellik Düzenleyicisi](../media/2-propeditor.png)
6. İlk sorgu sonucundan başlayarak, **PropertyName** özelliği için **AdditionalUpdateLanguagesForO365** ile bulana kadar her bir nesneyi açın.
7. **Değer2** öğesini seçin ve **özelliği Düzenle**' ye tıklayın.  
   ![Değer2 özelliğini Düzenle](../media/3-queryresult.png)
8. **Değer2** özelliğine ek diller ekleyin ve **özelliği kaydet**' e tıklayın. <br/> Örneğin, pt-pt (Portekizce-Portekiz için), AF-za (Afriveçce-Güney Afrika için), NN-No (Norveççe (Nynorsk)-Norveç vb. gibi. `pt-pt,af-za,nn-no`Örnek dilleri yazmanız gerekir. Diller arasında boşluk kullanmayın.
 
   ![Özellik Düzenleyicisi 'nde dil ekleme](../media/4-props.png)  
9. **Kapat**' a tıklayın, **Kapat**' a tıklayın, **özelliği kaydet**' e tıklayın ve **nesneyi kaydet** ' e tıklayın (burada **Kapat** ' a tıkladığınızda değerler atılır). **Kapat**' a tıklayın ve ardından Windows Yönetim Araçları sınayıcıdan çıkmak için **Çıkış** ' a tıklayın.
10. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **genel bakış**  >  **Office 365 istemci yönetimi**  >  **Office 365 güncelleştirmeler**' e gidin.
11. Artık Office 365 güncelleştirmelerini indirdiğinizde güncelleştirmeler, sihirbazda seçtiğiniz dillerde indirilir ve bu yordamda yapılandırılır. Güncelleştirmelerin doğru dillerde indirildiğini doğrulamak için, güncelleştirmenin paket kaynağına gidin ve dosya adında dil koduna sahip dosyaları arayın.  
    ![Ek dillere sahip dosya adları](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>Bir görev dizisinde Office 365 ProPlus 'ı güncelleştirme
Office 365 güncelleştirmelerini yüklemek için [yazılım güncelleştirmelerini yükler](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) görev dizisi adımını kullanırken, dağıtılan güncelleştirmelerin geçerli değil olarak algılanabilmesi mümkündür.  Zamanlanan Office otomatik güncelleştirmeler görevi en az bir kez çalıştırılmadıysa bu durum oluşabilir (bkz. [Office 365 güncelleştirmelerini dağıtma](manage-office-365-proplus-updates.md#deploy-office-365-updates)bölümünde nota bakın). Örneğin, bu adım çalıştırılmadan önce Office 365 ProPlus yüklüyse bu durum oluşabilir.

Güncelleştirme kanalının dağıtılan güncelleştirmelerin düzgün algılanabilmesi için ayarlandığından emin olmak için aşağıdaki yöntemlerden birini kullanın:

**Yöntem 1:**
1. Aynı Office 365 ProPlus sürümüne sahip bir makinede Görev Zamanlayıcı (Taskschd. msc) öğesini açın ve Office 365 otomatik güncelleştirmeler görevini yapın. Genellikle, **Task Scheduler Library**  > **Microsoft** > **Office**Görev Zamanlayıcı Kitaplığı altında bulunur.
2. Otomatik Güncelleştirmeler görevine sağ tıklayın ve **Özellikler**' i seçin.
3. **Eylemler** sekmesine gidin ve **Düzenle**' ye tıklayın. Komutu ve tüm bağımsız değişkenleri kopyalayın. 
4. Configuration Manager konsolunda, görev dizinizi düzenleyin.
5. Görev dizisindeki **yazılım güncelleştirmelerini yükler** adımından önce yeni bir **komut satırı Çalıştır** adımı ekleyin. Office 365 ProPlus aynı görev dizisinin bir parçası olarak yüklenirse, Office yüklendikten sonra bu adımın çalıştığından emin olun.
6. Office otomatik güncelleştirmeleri zamanlanmış görevinden topladığınız komutta ve bağımsız değişkenlerde kopyalama yapın. 
7. **Tamam**'a tıklayın. 

**Yöntem 2:**
1. Aynı Office 365 ProPlus sürümüne sahip bir makinede Görev Zamanlayıcı (Taskschd. msc) öğesini açın ve Office 365 otomatik güncelleştirmeler görevini yapın. Genellikle, **Task Scheduler Library**  > **Microsoft** > **Office**Görev Zamanlayıcı Kitaplığı altında bulunur.
2. Configuration Manager konsolunda, görev dizinizi düzenleyin.
3. Görev dizisindeki **yazılım güncelleştirmelerini yükler** adımından önce yeni bir **komut satırı Çalıştır** adımı ekleyin. Office 365 ProPlus aynı görev dizisinin bir parçası olarak yüklenirse, Office yüklendikten sonra bu adımın çalıştığından emin olun.
4. Komut satırı alanına, zamanlanmış görevi çalıştıracak komut satırını girin. Tırnak içindeki dizenin, adım 1 ' de tanımlanan görevin yolu ve adıyla eşleştiğinden emin olmak için aşağıdaki örneğe bakın.  

    Örnek: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. **Tamam**'a tıklayın. 

## <a name="update-channels-for-microsoft-365-apps"></a><a name="bkmk_channel"></a>Microsoft 365 uygulamalar için kanalları güncelleştirme
<!--6298093-->
Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldığında güncelleştirme kanalları da yeniden adlandırıldı. Güncelleştirmeleri dağıtmak için bir otomatik dağıtım kuralı (ADR) kullanıyorsanız, ADRs 'de **başlık** özelliğini kullanan değişiklikler yapmanız gerekir. Çünkü Microsoft Update katalogdaki güncelleştirme paketlerinin adı değişiyor.

Şu anda, Office 365 ProPlus için bir güncelleştirme paketinin başlığı aşağıdaki örnekte görüldüğü gibi "Office 365 Istemci güncelleştirmesi" ile başlar:

&nbsp;&nbsp;Office 365 Istemci güncelleştirmesi-x64 tabanlı sürüm Için yarı yıllık kanal sürüm 1908 (derleme 11929,20648)

9 Haziran 'dan sonra ve sonrasında yayınlanan güncelleştirme paketleri için, başlık aşağıdaki örnekte görüldüğü gibi "Microsoft 365 Apps Update" ile başlar:

&nbsp;&nbsp;Microsoft 365 Apps Update-x64 tabanlı sürüm Için yarı yıllık kanal sürüm 1908 (derleme 11929,50000)
</br>
</br>

|Yeni kanal adı|Önceki kanal adı|
|--|--|
|Yarı yıllık kurumsal kanal|Yarı Yıllık Kanal|
|Yarı yıllık kurumsal kanal (Önizleme)|Yarı Yıllık Kanal (Hedefli)|
|Aylık kurumsal kanal|NA|
|Geçerli kanal|Aylık Kanal|
|Geçerli kanal (Önizleme)|Aylık kanal (hedefli)|
|Beta kanalı|'Dan|

ADRs 'nizi değiştirme hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](automatically-deploy-software-updates.md). Ad değişikliği hakkında daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](https://docs.microsoft.com/deployoffice/name-change).


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Office 365 istemcilerinin Configuration Manager güncelleştirmeleri almasını etkinleştirdikten sonra güncelleştirme kanalını değiştirme

Office 365 ProPlus 'ı dağıttıktan sonra, güncelleştirme kanalını grup ilkesi veya Office dağıtım aracı (ODT) ile değiştirebilirsiniz. Örneğin, bir cihazı yarı yıllık kanaldan yarı yıllık kanala (hedefli) taşıyabilirsiniz. Kanal değiştirilirken, Office, tam sürümü yeniden yüklemek veya indirmek zorunda kalmadan otomatik olarak güncelleştirilir. Daha fazla bilgi için bkz. [kuruluşunuzdaki cihazlar Için Office 365 ProPlus güncelleştirme kanalını değiştirme](https://docs.microsoft.com//deployoffice/change-update-channels).


## <a name="next-steps"></a>Sonraki adımlar

Office 365 istemci bilgilerini gözden geçirmek ve Office 365 uygulamalarını dağıtmak için Configuration Manager 'de Office 365 Istemci yönetimi panosunu kullanın. Daha fazla bilgi için bkz. [Office 365 Istemci yönetimi panosu](office-365-dashboard.md).
