---
title: Microsoft 365 Apps güncelleştirmelerini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager, güncelleştirmeleri istemcilere dağıtmak üzere kullanılabilir hale getirmek için WSUS kataloğundaki Microsoft 365 Apps istemci güncelleştirmelerini site sunucusuna eşitler.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: d2a7f5ec31359cdd1a69bad3204d5119f8998e92
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129180"
---
# <a name="manage-microsoft-365-apps-with-configuration-manager"></a>Configuration Manager ile Microsoft 365 uygulamalarını yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Note]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](https://docs.microsoft.com/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager konsolunda ve destekleyici belgelerde eski adın başvurularını görmeye devam edebilirsiniz.

Configuration Manager, Microsoft 365 uygulamalarını aşağıdaki yollarla yönetmenizi sağlar:

- [Microsoft 365 uygulamalarını dağıtma](#bkmk_deploy): Ilk Microsoft 365 uygulamalar yükleme deneyimini kolaylaştırmak için [Office 365 istemci yönetimi panosundan](office-365-dashboard.md) Microsoft 365 Apps Installer 'ı başlatabilirsiniz. Sihirbaz, Microsoft 365 Apps yükleme ayarlarını yapılandırmanıza, Office Içerik teslim ağlarından (CDNs) dosya yüklemenize ve içerikle bir betik uygulaması oluşturmanıza ve dağıtmanıza olanak tanır.

- [Microsoft 365 Apps güncelleştirmelerini dağıtma](#bkmk_update): yazılım güncelleştirme yönetimi iş akışını kullanarak Microsoft 365 Apps istemci güncelleştirmelerini yönetebilirsiniz. Microsoft, Office Content Delivery Network (CDN) yeni bir Microsoft 365 Apps güncelleştirmesi yayımladığında, Microsoft, Windows Server Update Services (WSUS) için de bir güncelleştirme paketi yayımlar. Configuration Manager, WSUS kataloğundaki Microsoft 365 Apps güncelleştirmelerini site sunucusuna eşitledikten sonra, güncelleştirme istemcilere dağıtılabilir.

   > [!NOTE]
   > Configuration Manager sürüm 2002 ' den başlayarak, Microsoft 365 Apps güncelleştirmelerini, bağlantısı kesilen ortamlara aktarabilirsiniz. Daha fazla bilgi için bkz. [Microsoft 365 Apps güncelleştirmelerini bağlantısı kesilen yazılım güncelleştirme noktasından eşitlemesi](../get-started/synchronize-office-updates-disconnected.md).   

- [Microsoft 365 uygulamalar güncelleştirme indirmeleri için dil ekleme](#bkmk_o365_lang): Microsoft 365 uygulamaları tarafından desteklenen dillere yönelik güncelleştirmeleri indirmek için Configuration Manager desteği ekleyebilirsiniz. Configuration Manager Microsoft 365 uygulamalar olduğu sürece dili desteklemek zorunda değildir. Configuration Manager sürüm 1610 ' den önce, güncelleştirmeleri Microsoft 365 Apps istemcilerinde yapılandırılmış aynı dillerde indirmeniz ve dağıtmanız gerekir.

- [Güncelleştirme kanalını değiştirme](#bkmk_channel): güncelleştirme kanalını değiştirmek için bir kayıt defteri anahtarı değer değişikliğini Microsoft 365 Apps istemcilerine dağıtmak üzere Grup İlkesi 'ni kullanabilirsiniz.

Microsoft 365 Apps istemci bilgilerini gözden geçirmek ve bu Microsoft 365 uygulamalar yönetim eylemlerinden bazılarını başlatmak için [Office 365 Istemci yönetimi panosunu](office-365-dashboard.md)kullanın.

## <a name="deploy-microsoft-365-apps"></a><a name="bkmk_deploy"></a>Microsoft 365 uygulamalarını dağıtma
İlk Microsoft 365 uygulamalar yüklemesi için Office 365 Istemci yönetimi panosundan Microsoft 365 Apps yükleyicisini başlatın. Sihirbaz, Microsoft 365 Apps yükleme ayarlarını yapılandırmanıza, Office Içerik teslim ağlarından (CDNs) dosya yüklemenize ve dosyalar için bir betik uygulaması oluşturmanıza ve dağıtmanıza olanak tanır. Microsoft 365 uygulamalar istemcilere yüklenene ve [Microsoft 365 Apps otomatik güncelleştirmeleri görevinin](https://docs.microsoft.com/deployoffice/overview-update-process-microsoft-365-apps) çalışmalarından Microsoft 365 uygulama güncelleştirmeleri uygulanmaz. Test amacıyla, güncelleştirme görevini el ile çalıştırabilirsiniz.

Önceki Configuration Manager sürümler için, istemcilerde Microsoft 365 uygulamaları ilk kez yüklemek üzere aşağıdaki adımları uygulamanız gerekir:
- Office dağıtım aracı 'Nı (ODT) İndir
- İhtiyaç duyduğunuz tüm dil paketleri de dahil olmak üzere Microsoft 365 Apps yükleme kaynak dosyalarını indirin.
- Doğru Microsoft 365 uygulamalar sürümünü ve kanalını belirten Configuration.xml oluşturun.
- Microsoft 365 uygulamaları yüklemek için istemciler için eski bir paket ya da bir betik uygulaması oluşturun ve dağıtın.

### <a name="requirements"></a>Gereksinimler
- Yükleyiciyi çalıştıran bilgisayarın Internet erişimi olmalıdır.  
- Yükleyiciyi çalıştıran kullanıcının, sihirbazda belirtilen içerik konumu paylaşımında **okuma** ve **yazma** erişimi olmalıdır.
- 404 indirme hatası alırsanız, şu dosyaları Kullanıcı% TEMP% klasörüne kopyalayın:
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1806-or-higher"></a>Microsoft 365 uygulamalarını Configuration Manager sürüm 1806 veya üstünü kullanarak dağıtın: 
Configuration Manager 1806 ' den başlayarak, Office özelleştirme aracı Configuration Manager konsolundaki yükleyiciyle tümleşiktir. Microsoft 365 uygulamalar için bir dağıtım oluştururken, en son yönetilebilirlik ayarlarını dinamik olarak yapılandırabilirsiniz. <!--1358149-->

1. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **genel bakış**  >  **Office 365 istemci yönetimi**' ne gidin.
2. Sağ üst bölmedeki **Office 365 yükleyicisi** ' ne tıklayın. Yükleme Sihirbazı açılır.
3. **Uygulama ayarları** sayfasında, uygulama için bir ad ve açıklama sağlayın, dosyalar için karşıdan yükleme konumunu girin ve ardından **İleri**' ye tıklayın. Konumun &#92;&#92;*server*&#92;*Share*olarak belirtilmesi gerekir.
4. **Office ayarları** sayfasında **Office özelleştirme aracına git ' e**tıklayın. Bu, tıkla- [Çalıştır Için Office Özelleştirme Aracı](https://config.office.com)açılır.
5. Microsoft 365 Apps yüklemeniz için istenen ayarları yapılandırın. Yapılandırmayı tamamladığınızda sayfanın sağ üst kısmındaki **Gönder** ' e tıklayın. 
6. **Dağıtım** sayfasında, şimdi mi yoksa daha sonra mı dağıtmak istediğinizi saptayın. Daha sonra dağıtmayı seçerseniz, uygulamayı **yazılım kitaplığı**  >  **uygulama yönetimi**  >  **uygulamalarında**bulabilirsiniz.  
7. **Özet** sayfasında ayarları onaylayın. 
8. **İleri** ' ye tıklayın, Sihirbaz tamamlandıktan sonra **Kapat** ' a tıklayın. 

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1802-and-prior"></a>Configuration Manager 1802 ve önceki sürümlerini kullanarak Microsoft 365 uygulamaları dağıtın:

1. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **genel bakış**  >  **Office 365 istemci yönetimi**' ne gidin.
2. Sağ üst bölmedeki **Office 365 yükleyicisi** ' ne tıklayın. Yükleme Sihirbazı açılır.
3. **Uygulama ayarları** sayfasında, uygulama için bir ad ve açıklama sağlayın, dosyalar için karşıdan yükleme konumunu girin ve ardından **İleri**' ye tıklayın. Konumun &#92;&#92;*server*&#92;*Share*olarak belirtilmesi gerekir.
4. **Istemci ayarlarını Içeri aktar** sayfasında, mevcut bir XML yapılandırma dosyasından Microsoft 365 Apps istemci ayarlarını içeri aktarıp aktarmayacağını veya ayarları el ile belirtmek için seçin. İşiniz bittiğinde **İleri** ' ye tıklayın.  

    Varolan bir yapılandırma dosyanız varsa, dosyanın konumunu girin ve 7. adıma atlayın.  &#92;&#92;*sunucu*&#92;*Share*&#92;*filename*biçiminde bir konum belirtmeniz gerekir. 'Sini.
    > [!IMPORTANT]    
    > XML yapılandırma dosyası yalnızca [Office 2016 tarafından desteklenen diller](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016)içermelidir.

5. **Istemci ürünleri** sayfasında, kullandığınız Microsoft 365 Apps Suite ' i seçin. Dahil etmek istediğiniz uygulamaları seçin. Dahil edilecek ek ürünleri seçin ve ardından **İleri**' ye tıklayın.
6. **Istemci ayarları** sayfasında, dahil edilecek ayarları seçin ve ardından **İleri**' ye tıklayın.
7. **Dağıtım** sayfasında, uygulamayı dağıtıp dağıtmeyeceğinizi seçin ve ardından **İleri**' ye tıklayın. <br/>Paketi sihirbazda dağıtmamalıdır seçeneğini belirlerseniz adım 9 ' a atlayın.
8. Sihirbaz sayfalarının geri kalanını tipik bir uygulama dağıtımında yaptığınız gibi yapılandırın. Ayrıntılar için bkz. [uygulama oluşturma ve dağıtma](../../apps/get-started/create-and-deploy-an-application.md).
9. Sihirbazı tamamlayın.
10. Uygulamayı **yazılım kitaplığı**  >  **'na genel bakış**  >  **uygulama yönetimi**  >  **uygulamalarından**dağıtabilir veya düzenleyebilirsiniz.

Yükleyiciyi kullanarak Microsoft 365 uygulamaları oluşturup dağıttıktan sonra, Configuration Manager, varsayılan olarak Microsoft 365 uygulama güncelleştirmelerini yönetmez. Microsoft 365 Apps istemcilerinin Configuration Manager güncelleştirmeleri almasını sağlamak için, bkz. [Microsoft 365 uygulama güncelleştirmelerini Configuration Manager Ile dağıtma](#bkmk_update).

Microsoft 365 uygulamaları dağıttıktan sonra, uygulamaları sürdürmek için otomatik dağıtım kuralları oluşturabilirsiniz. Microsoft 365 uygulamalar için bir otomatik dağıtım kuralı oluşturmak için, [Office 365 Istemci yönetimi PANOSUNDAN](office-365-dashboard.md) **ADR oluştur** ' a tıklayın. Ürünü seçerken **Office 365 istemcisi** ' ni seçin. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](automatically-deploy-software-updates.md).


## <a name="drill-through-required-microsoft-365-apps-updates"></a>Gerekli Microsoft 365 Apps güncelleştirmelerinin detayına gitme
<!--4224414-->
*(Sürüm 1906 ' de tanıtılmıştır)*

Hangi cihazların belirli bir Microsoft 365 Apps yazılım güncelleştirmesi gerektirdiğini görmek için uyumluluk istatistikleri detayına gidebilirsiniz. Cihaz listesini görüntülemek için, cihazların ait olduğu güncelleştirmeleri ve koleksiyonları görüntülemek için izninizin olması gerekir. Cihaz listesinin detayına gitmek için:

1. **Yazılım kitaplığı**  >  **Office 365 istemci yönetimi**  >  **Office 365 güncelleştirmeleri**' ne gidin.
1. En az bir cihaz için gerekli olan herhangi bir güncelleştirmeyi seçin.
1. **Özet** sekmesine bakın ve **İstatistikler**altında Pasta grafiğini bulun.
1. Cihaz listesinin detayına gitmek için pasta grafiğinin yanındaki **gereken köprüyü görüntüle** ' yi seçin.
1. Bu eylem sizi, güncelleştirme gerektiren cihazları görebileceğiniz **cihazlarda** geçici bir düğüme götürür. Ayrıca, bir düğüm için, listeden yeni koleksiyon oluşturma gibi işlemler gerçekleştirebilirsiniz.


## <a name="deploy-microsoft-365-apps-updates"></a><a name="bkmk_update"></a>Microsoft 365 Apps güncelleştirmelerini dağıtma

Microsoft 365 Apps güncelleştirmelerini Configuration Manager ile dağıtmak için aşağıdaki adımları kullanın:

1. Makalenin **Microsoft 365 Apps istemci güncelleştirmelerini yönetmek için Configuration Manager kullanma gereksinimleri** bölümünde Microsoft 365 Apps istemci güncelleştirmelerini yönetmek için Configuration Manager kullanma [gereksinimlerini doğrulayın](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) .  

2. Microsoft 365 Apps istemci güncelleştirmelerini eşitleyecek [yazılım güncelleştirme noktalarını yapılandırın](../get-started/configure-classifications-and-products.md) . Sınıflandırma için **güncelleştirmeleri** ayarlayın ve ürün için **Office 365 istemcisini** seçin. **Güncelleştirme** sınıflandırmasını kullanmak için yazılım güncelleştirme noktalarını yapılandırdıktan sonra yazılım güncelleştirmelerini eşitler.
3. Microsoft 365 Apps istemcilerinin Configuration Manager güncelleştirmeleri almasını etkinleştirin. İstemciyi etkinleştirmek için Configuration Manager istemci ayarları veya Grup İlkesi kullanın.

    **Yöntem 1**: Configuration Manager sürüm 1606 ' den başlayarak Microsoft 365 Apps istemci aracısını yönetmek için Configuration Manager istemci ayarını kullanabilirsiniz. Bu ayarı yapılandırıp Microsoft 365 Apps güncelleştirmelerini dağıttıktan sonra, Configuration Manager istemci Aracısı, güncelleştirmeleri bir dağıtım noktasından indirmek ve onları yüklemek için Microsoft 365 Apps istemci aracısıyla iletişim kurar. Configuration Manager Microsoft 365 Apps istemci ayarlarının envanterini alır.    

      1. Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **istemci ayarları**' na tıklayın.  

      2. İstemci aracısını etkinleştirmek için uygun cihaz ayarlarını açın. Varsayılan ve özel istemci ayarları hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).  

      3. **Yazılım güncelleştirmeleri** ' ne tıklayın ve **Office 365 istemci Aracısı ayarının yönetimini etkinleştirmek** için **Evet** ' i seçin.  

    **Yöntem 2**: Office dağıtım aracını veya grup ilkesi kullanarak Configuration Manager [güncelleştirmeleri almak için Microsoft 365 Apps istemcilerinin etkinleştirin](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) .  

4. [Microsoft 365 Apps güncelleştirmelerini Istemcilere dağıtın](deploy-software-updates.md) .

> [!NOTE]  
>
> Microsoft 365 uygulamalar yakın zamanda yüklenmişse ve nasıl yüklendiğine bağlı olarak, güncelleştirme kanalının henüz ayarlanmamış olması mümkündür. Bu durumda, dağıtılan güncelleştirmeler geçerli değil olarak algılanır. Microsoft 365 uygulamalar yüklediğinde, [Zamanlanmış bir otomatik güncelleştirmeler görevi](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) oluşturulur. Bu durumda, güncelleştirme kanalının ayarlanması ve güncelleştirmelerin uygun olarak algılanabilmesi için bu görevin en az bir kez çalışması gerekir.
>
> Microsoft 365 uygulamalar yakın zamanda yüklenmişse ve dağıtılan güncelleştirmeler algılanmazsa, sınama amacıyla, Office otomatik güncelleştirmeler görevini el ile başlatabilir ve ardından istemcide [yazılım güncelleştirmeleri dağıtımı değerlendirme döngüsünü](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) başlatabilirsiniz. Bunu bir görev dizisinde nasıl yapacağınız hakkında yönergeler için bkz. [bir görev dizisindeki Microsoft 365 uygulamalarını güncelleştirme](manage-office-365-proplus-updates.md#bkmk_ts).

## <a name="restart-behavior-and-client-notifications-for-microsoft-365-apps-updates"></a>Microsoft 365 Apps güncelleştirmeleri için yeniden başlatma davranışı ve istemci bildirimleri
Bir Microsoft 365 Apps istemcisine bir güncelleştirme dağıttığınızda, yeniden başlatma davranışı ve istemci bildirimleri, Configuration Manager sürümüne bağlı olarak farklıdır. Aşağıdaki tabloda, istemci bir Microsoft 365 Apps güncelleştirmesi aldığında Son Kullanıcı deneyimi hakkında bilgi verilmektedir:

|Configuration Manager sürümü |Son kullanıcı deneyimi|  
|----------------|---------------------|
|1706, 1710|İstemci, güncelleştirmeyi yüklemeden önce açılır ve uygulama içi bildirimlerin yanı sıra geri sayım iletişim kutusunu da alır.|
|1802| İstemci, güncelleştirmeyi yüklemeden önce açılır ve uygulama içi bildirimlerin yanı sıra geri sayım iletişim kutusunu da alır. </br>İstemci güncelleştirme zorlaması sırasında herhangi bir Microsoft 365 uygulaması çalışıyorsa, Microsoft 365 uygulamalar kapanmaya zorlanmaz. Bunun yerine, güncelleştirme yüklemesi sistemin yeniden başlatılmasını gerektirir. <!--510006-->|


> [!Important]
>
>Configuration Manager sürüm 1706 ' de, aşağıdaki ayrıntılara göz önünde yer verilmiştir:
>
>- Son tarihin 48 saat içinde olduğu ve güncelleştirme içeriğinin indirileceği gerekli uygulamalar için görev çubuğundaki bildirim alanında bildirim simgesi görüntülenir. 
>- Son tarihin 7,5 saat içinde olduğu ve güncelleştirmenin indirileceği gerekli uygulamalar için bir geri sayım iletişim kutusu görüntülenir. Kullanıcı, geri sayım iletişim kutusunu son tarihten en fazla üç kez erteleyebilir. Ertelendiğinde geri sayım iki saat sonra yeniden görüntülenir. Ertelenmiyorsa, geri sayım süresi dolduğunda 30 dakikalık bir geri sayım ve güncelleştirme yüklenir.
>- Kullanıcı bildirim alanındaki simgeye tıklayana kadar bir açılır bildirim görüntülenmeyebilir. Ayrıca, bildirim alanında minimum alan varsa bildirim simgesi Kullanıcı bildirim alanını açana veya genişletmediği takdirde görünür olmayabilir. 
>- Kullanıcı cihazda etkin bir şekilde çalışmaması durumunda bildirim ve geri sayım iletişim kutusu başlatılabilir. Örneğin, cihaz kilitlendiğinde Microsoft 365 gece boyunca cihaz üzerinde çalışan uygulamalar, güncelleştirmeyi yüklemek için kapanmaya zorlanabilir. Office, uygulamayı kapatmadan önce veri kaybını engellemek için uygulama verilerini kaydeder. 
>- Son Tarih geçmişte ise veya en kısa sürede başlayacak şekilde yapılandırıldıysa, Microsoft 365 uygulamalar çalışır duruma girmeden kapanmaya zorlanabilir. 
>- Kullanıcı son tarihten önce bir Microsoft 365 Apps güncelleştirmesi yüklerse, son tarihe ulaşıldığında güncelleştirmenin yüklendiğini doğrular Configuration Manager. Güncelleştirme cihazda algılanmazsa, güncelleştirme yüklenir. 
>- Uygulama içi bildirim çubuğu, güncelleştirme indirilmeden önce çalıştıran bir uygulama üzerinde görüntülenmez. Güncelleştirme indirildikten sonra, uygulama içi bildirim yalnızca yeni açılan uygulamalar için görüntülenir.
>- Bir hizmet penceresi tarafından tetiklenen veya iş dışı saatlere yönelik olarak zamanlanan Microsoft 365 uygulama güncelleştirmeleri için, Office uygulamalarını çalıştırmak, güncelleştirmeyi bildirim olmadan yüklemek için kapanmaya zorlanacaktır. 
>- Daha fazla bilgi için bkz. [Microsoft 365 uygulamalar Için Son Kullanıcı güncelleştirme bildirimleri](https://docs.microsoft.com/deployoffice/end-user-update-notifications-microsoft-365-apps)


## <a name="add-languages-for-microsoft-365-apps-update-downloads"></a><a name="bkmk_o365_lang"></a>Microsoft 365 uygulamalar güncelleştirme indirmeleri için dil ekleme
Microsoft 365 uygulamalar tarafından desteklenen tüm diller için güncelleştirmeleri indirmek üzere Configuration Manager için destek ekleyebilirsiniz.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Sürüm 1902 ' de ek diller için güncelleştirmeleri indirin
<!--3555955-->

Configuration Manager sürüm 1902 ' den başlayarak güncelleştirme iş akışı, **Windows Update** için 38 dillerini **Office 365 istemci güncelleştirmesi**için çok sayıda ek dilde ayırır.

Gerekli dilleri seçmek için aşağıdaki konumlarda bulunan **Dil seçimi** sayfasını kullanın:
- Otomatik dağıtım kuralı oluşturma Sihirbazı
- Yazılım güncelleştirmelerini dağıtma Sihirbazı
- Yazılım güncelleştirmelerini indirme Sihirbazı
- Otomatik dağıtım kuralı özellikleri

**Dil seçimi** sayfasında, **Office 365 istemci güncelleştirmesi**' ni seçin ve ardından **Düzenle**' ye tıklayın. Microsoft 365 uygulamalar için gerekli dilleri ekleyin ve ardından **Tamam**' a tıklayın.

![Microsoft 365 uygulamalar için ek dil ekleme ekran görüntüsü](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Sürüm 1810 ve önceki sürümlerde ek diller için güncelleştirmeleri indirme desteği eklemek için

Merkezi yönetim sitesindeki veya tek başına birincil sitedeki yazılım güncelleştirme noktasında aşağıdaki yordamı kullanın.

> [!IMPORTANT]  
> Ek Microsoft 365 uygulamalar yapılandırmak güncelleştirme dilleri site genelinde bir ayardır. Aşağıdaki yordamı kullanarak dilleri ekledikten sonra, tüm Microsoft 365 Apps güncelleştirmeleri bu dillerde indirilir, ayrıca yazılım güncelleştirmelerini Indir veya yazılım güncelleştirmelerini dağıtma sihirbazları 'ndaki **Dil seçimi** sayfasında seçtiğiniz diller de bulunur.

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
11. Artık Microsoft 365 Apps güncelleştirmelerini indirdiğinizde güncelleştirmeler, sihirbazda seçtiğiniz dillerde indirilir ve bu yordamda yapılandırılır. Güncelleştirmelerin doğru dillerde indirildiğini doğrulamak için, güncelleştirmenin paket kaynağına gidin ve dosya adında dil koduna sahip dosyaları arayın.  
    ![Ek dillere sahip dosya adları](../media/5-verification.png)

## <a name="updating-microsoft-365-apps-in-a-task-sequence"></a><a name="bkmk_ts"></a>Bir görev dizisindeki Microsoft 365 uygulamalarını güncelleştirme
Microsoft 365 Apps güncelleştirmelerini yüklemek için [yazılım güncelleştirmelerini yükler](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) görev dizisi adımını kullanırken, dağıtılan güncelleştirmelerin geçerli değil olarak algılanabilmesi mümkündür.  Zamanlanan Office otomatik güncelleştirmeler görevi en az bir kez çalıştırılmadıysa bu durum oluşabilir ( [Microsoft 365 uygulama güncelleştirmelerini dağıtma](manage-office-365-proplus-updates.md#bkmk_update)bölümündeki nota bakın). Örneğin, bu adımı çalıştırmadan önce Microsoft 365 uygulamalar hemen yüklenmişse bu durum oluşabilir.

Güncelleştirme kanalının dağıtılan güncelleştirmelerin düzgün algılanabilmesi için ayarlandığından emin olmak için aşağıdaki yöntemlerden birini kullanın:

**Yöntem 1:**
1. Aynı Microsoft 365 uygulamalarla aynı sürüme sahip bir makinede Görev Zamanlayıcı (Taskschd. msc) açın ve Microsoft 365 Apps otomatik güncelleştirmeler görevini yapın. Genellikle, **Task Scheduler Library**  > **Microsoft** > **Office**Görev Zamanlayıcı Kitaplığı altında bulunur.
2. Otomatik Güncelleştirmeler görevine sağ tıklayın ve **Özellikler**' i seçin.
3. **Eylemler** sekmesine gidin ve **Düzenle**' ye tıklayın. Komutu ve tüm bağımsız değişkenleri kopyalayın. 
4. Configuration Manager konsolunda, görev dizinizi düzenleyin.
5. Görev dizisindeki **yazılım güncelleştirmelerini yükler** adımından önce yeni bir **komut satırı Çalıştır** adımı ekleyin. Microsoft 365 uygulamalar aynı görev dizisinin bir parçası olarak yüklenirse, Office yüklendikten sonra bu adımın çalıştığından emin olun.
6. Office otomatik güncelleştirmeleri zamanlanmış görevinden topladığınız komutta ve bağımsız değişkenlerde kopyalama yapın. 
7. **Tamam**’a tıklayın. 

**Yöntem 2:**
1. Aynı Microsoft 365 uygulamalarla aynı sürüme sahip bir makinede Görev Zamanlayıcı (Taskschd. msc) açın ve Microsoft 365 Apps otomatik güncelleştirmeler görevini yapın. Genellikle, **Task Scheduler Library**  > **Microsoft** > **Office**Görev Zamanlayıcı Kitaplığı altında bulunur.
2. Configuration Manager konsolunda, görev dizinizi düzenleyin.
3. Görev dizisindeki **yazılım güncelleştirmelerini yükler** adımından önce yeni bir **komut satırı Çalıştır** adımı ekleyin. Microsoft 365 uygulamalar aynı görev dizisinin bir parçası olarak yüklenirse, Office yüklendikten sonra bu adımın çalıştığından emin olun.
4. Komut satırı alanına, zamanlanmış görevi çalıştıracak komut satırını girin. Tırnak içindeki dizenin, adım 1 ' de tanımlanan görevin yolu ve adıyla eşleştiğinden emin olmak için aşağıdaki örneğe bakın.  

    Örnek: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. **Tamam**’a tıklayın. 

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


## <a name="change-the-update-channel-after-you-enable-microsoft-365-apps-clients-to-receive-updates-from-configuration-manager"></a>Microsoft 365 Apps istemcilerinin Configuration Manager güncelleştirmelerini almasını etkinleştirdikten sonra güncelleştirme kanalını değiştirin

Microsoft 365 uygulamaları dağıttıktan sonra, güncelleştirme kanalını grup ilkesi veya Office dağıtım aracı (ODT) ile değiştirebilirsiniz. Örneğin, bir cihazı yarı yıllık kanaldan yarı yıllık kanala (hedefli) taşıyabilirsiniz. Kanal değiştirilirken, Office, tam sürümü yeniden yüklemek veya indirmek zorunda kalmadan otomatik olarak güncelleştirilir. Daha fazla bilgi için bkz. [kuruluşunuzdaki cihazlar için Microsoft 365 Apps güncelleştirme kanalını değiştirme](https://docs.microsoft.com//deployoffice/change-update-channels).


## <a name="next-steps"></a>Sonraki adımlar

Microsoft 365 Apps istemci bilgilerini gözden geçirmek ve Microsoft 365 uygulamaları dağıtmak için Configuration Manager 'de Office 365 Istemci yönetimi panosunu kullanın. Daha fazla bilgi için bkz. [Office 365 Istemci yönetimi panosu](office-365-dashboard.md).
