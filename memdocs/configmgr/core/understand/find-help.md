---
title: Yardım bulma
titleSuffix: Configuration Manager
description: Configuration Manager hakkında daha fazla bilgi için kaynakları bulun.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bae98a8df1d8b8ff843bd333083c4c6ad68848c
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343193"
---
# <a name="find-help-for-using-configuration-manager"></a>Configuration Manager kullanmaya yönelik yardım bulun

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager kullanmaya yönelik yardım bulmak için birden çok kaynakla birlikte aşağıdaki bölümler sunulmaktadır:  

- [Ürün belgeleri](#bkmk_Info)  

- [Ürün geri bildirimi paylaşılıyor](#product-feedback)  

- [Configuration Manager ekip blogunu takip edin](#BKMK_ProductGroupBlog)  

- [Destek seçenekleri ve topluluk kaynakları](#BKMK_SupportOptions)  

Ürün erişilebilirliği hakkında yardım için bkz. [erişilebilirlik özellikleri](accessibility-features.md).  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a>Ürün belgeleri  

En güncel ürün belgelerine erişmek için [kitaplık dizininden](https://docs.microsoft.com/sccm/)başlayın.  

<a name="BKMK_SearchTips"></a>  

Arama hakkında ipuçları, geri bildirim sağlama ve ürün belgelerini kullanma hakkında daha fazla bilgi için bkz. [belgeleri kullanma](use-docs.md).  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a>Sürüm 1806 ile başlayan ürün geri bildirimi

Configuration Manager sürüm 1806 ' den başlayarak, ürün geri bildirimini doğrudan konsolundan gönderebilirsiniz. Günlükleri iliştirmeye ihtiyacınız varsa, [Geri Bildirim Hub 'ını](#BKMK_FeedbackHub)kullanın. Aşağıdaki işlemleri yapabilirsiniz: <!--1357542-->

- **Gülümseme gönderin**: beğendikleriniz hakkında geri bildirim gönderin.
- **Kaş çatma Gönder**: beğendikleriniz hakkında geri bildirim gönderin.
- **Öneri gönderin**: fikrinizi paylaşmak Için sizi [UserVoice Web sitesine](https://configurationmanager.uservoice.com/) götürür.

  ![Configuration Manager 1806 ' de geri bildirim gönderin](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>Gülümseme Gönder veya kaş çatma Gönder

Beğendiğiniz bir şey hakkında geri bildirim göndermek için aşağıdaki yönergeleri izleyin:

1. Konsolun sağ üst köşesinde gülen yüz düğmesine tıklayın.
2. Aşağı açılan menüden **gülümseme Gönder** veya **kaş çatma Gönder**' i seçin.
3. Beğendiklerinizi veya neleri beğenmediğinizi açıklamak için metin kutusunu kullanın. 
4. E-posta adresinizi ve ekran görüntüsünü paylaşmak istiyorsanız seçin.
5. **Geri bildirim gönder** ' e tıklayın
     - İnternet bağlantınız yoksa, alt kısımdaki **Kaydet** ' e tıklayın. Daha sonra Microsoft 'a göndermek için [kaydettiğiniz geri bildirim gönder](#BKMK_NoInternet) bölümünde yer alan yönergeleri izleyin. 

![Configuration Manager 1806 ' de geri bildirim formu gönder](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>Gülümseme Gönder için durum iletileri
<!--5891852-->
Configuration Manager 2002 ' den başlayarak, **gülümseme gönderdiğinizde** veya **kaş çatma gönderdiğinizde**, geri bildirim gönderildiğinde bir durum iletisi oluşturulur. Bu iyileştirme şunları bir kayıt sağlar:
- Geri bildirim gönderildiğinde
- Geri bildirimi gönderen kişi
- Geri bildirim KIMLIĞI
- Geri bildirim gönderimi başarılı olduysa veya
   - Başarılı bir gönderim için 53900 ileti KIMLIĞI.
   - Başarısız bir gönderim için 53901 ileti KIMLIĞI.

**İzleme**  >  **sistem durumu**  >  **durum iletisi sorgularının**durum iletilerini görüntüleyin. **Tüm durum iletileri** sorgusuna başlayın ve zaman çerçevesini seçin. İletiler yüklendiğinde **Iletileri filtrele** düğmesine tıklayın ve ileti kimliği 53900 veya 53901 için filtre uygulayın.

[Daha sonra gönderilmek üzere kaydettiğiniz geri bildirimleri gönderirseniz](find-help.md#BKMK_NoInternet)durum iletileri oluşturulmaz.

[![Geri bildirimin başarıyla gönderilmesi için durum iletisi](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>Öneri gönderin

**Bir öneri gönderdiğinizde**, fikrinizi paylaşmak için bir üçüncü taraf web sitesi olan [UserVoice](https://configurationmanager.uservoice.com/)'a yönlendirilirsiniz. Configuration Manager ürün ekibi aşağıdaki UserVoice durum değerlerini kullanır:

- **Not** -isteği anladık ve anlamlı hale getiriyor. Kapsamımızı ekledik.
- **Planlanmış** -bu özellik için kodlama başladık ve önümüzdeki birkaç ay içinde bir teknik önizleme derlemesinde gösterilmesini bekledik.
- **Başlatıldı** -özellik artık bir teknoloji önizlemededir. Göz atın ve bize geri bildirimde bulunun. Özelliğin doğru parçada olduğunu bize bildirmek. Başkalarının görmesi ve açıklama koymak için özgün isteğin Comments bölümüne ek geri bildirim koyun. Bu bilgileri okuyup, özelliği geliştirmeyi denemek için geri bildirimi kullanacaksınız.
- **Tamamlandı** -özelliğin ilk sürümü bir üretim derlemesinde. Bu durum, özellikle %100 olan ve artık geliştirmeyen bir değer değildir. Ancak, özelliklerin v1 bir üretim derlemesinde olduğu ve gerçek için kullanmaya başlayabileceği anlamına gelir. Şu nedenle tamamlandı olarak işaretliyoruz:
  - Üretime hazırlanma özelliğinin olduğunu bilmeniz istiyoruz.
  - Diğer öğelerde kullanabilmeniz için UserVoice oylarınızı geri vermek istiyoruz.
  - Bu özelliğe yönelik en önemli geliştirme hakkında bilgi sahibi olmak için yeni tasarım değişikliği Isteklerini bu özelliğe kaydedebilirsiniz.

### <a name="information-sent-with-feedback"></a>Geri bildirimde gönderilen bilgiler

**Gülümseme gönderdiğinizde** veya **kaş çatma gönderdiğinizde**, geri bildirimle aşağıdaki bilgiler gönderilir:

- İşletim sistemi derleme bilgileri
- Configuration Manager hiyerarşi KIMLIĞI
- Ürün derleme bilgileri
- Dil bilgileri
- Cihaz tanımlayıcısı 
    - HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SQMClient: MachineID



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a>Daha sonra gönderilmek üzere kaydettiğiniz geri bildirimleri gönderin

1. **Geri bildirim sağla** penceresinin altındaki **Kaydet** ' e tıklayın. 
2. . Zip dosyasını kaydedin. Yerel makinenin internet erişimi yoksa, dosyayı internet 'e bağlı bir makineye kopyalayın. 
3. Gerekirse, şurada bulunan UploadOfflineFeedback klasörünü kopyalayın:`cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`
    - CD. Latest klasörü hakkında daha fazla bilgi için [CD 'ye bakın. En son klasör](../servers/manage/the-cd.latest-folder.md)

4. İnternet 'e bağlı bir makinede, bir komut istemi açın. 
5. Şu komutu çalıştırın:`UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - İsteğe bağlı olarak, aşağıdaki parametreleri belirtebilirsiniz:
        -  `-t, --timeout`Verilerin gönderilmesi için saniye cinsinden zaman aşımı. 0 sınırsızdır. Varsayılan değer 30 ' dur.
        - `-s --silent`Konsolda günlüğe kaydetme yok (--verbose ile birleştirilemez)
        - `-v, --verbose`Konsola ayrıntılı günlük kaydı çıkar (--Silent ile birleştirilemez)
        - `--help`Yardım ekranını görüntüler
    
    - Sürüm 1910 ' den başlayarak, UploadOfflineFeedback yardımcı programı bir proxy sunucu kullanımını destekler. Aşağıdaki parametreleri belirtebilirsiniz:
        - `-x, --proxy`İnternet 'e bağlanmak için bir proxy sunucusu belirtir.
        - `-o, --port`İnternet 'e bağlanacak ara sunucu bağlantı noktasını belirtir.
        - `-u, --user`İnternet 'e bağlanmak için proxy sunucusu kullanıcı adını belirtir.
        - `-w, --password`İnternet 'e bağlanmak için proxy sunucusu parolasını belirtir. Parola istemi oluşturmak için bir yıldız işareti (&#42;) yazın. Parolayı parola istemine yazdığınızda bu parola görüntülenmez. Komut satırında düz metin daha az güvenli olduğundan parola girişi için bir istem oluşturmak üzere bir yıldız işareti (&#42;) kullanmanız önemle önerilir.
        - `-i`Bağlantı denetimini atla: ağ bağlantısı denetimini atlar, yalnızca belirtilen ayarlarla geri bildirim yükler.

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a>Konsol geri bildirimi onayı

<!--3556010-->
Sürüm 1902 ' den başlayarak, Configuration Manager konsolu veya UploadOfflineFeedback. exe aracılığıyla geri bildirim gönderdiğinizde, bir onay iletisi gösterir. Bu ileti, izleme tanımlayıcısı olarak Microsoft 'a verebileceğiniz bir **geri BILDIRIM kimliği**içerir.

- **Geri bildirim kimliğini**kopyalamak için, kimliğin yanındaki Kopyala simgesini seçin veya **CTRL**  +  **C** tuş kısayolunu kullanın.
  - Bu KIMLIK bilgisayarınızda depolanmaz, bu nedenle pencereyi kapatmadan önce kopyayı kopyalamadığınızdan emin olun.
- **Bu iletiyi bir daha gösterme** ' ye tıkladığınızda iletişim kutusu bastırılır ve gelecekte görünmesini önlenir.

   ![Configuration Manager 1902 ' de konsolundan geri bildirim onayı](media/1902-feedback-id-example.png)
- **UploadOfflineFeedback** komut Aracı,-s veya--Silent kullanılmadığı takdirde **feedbackıd** 'yi konsola yazar.

  ![Configuration Manager 1902 ' de UploadOfflineFeedback. exe ' den geri bildirim onayı](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a>1802 ve önceki sürümler için ürün geri bildirimi

Windows 10 ' a yerleşik olarak bulunan [geri bildirim Merkezi uygulaması](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) aracılığıyla olası ürün Hatalarını bildirin. **Yeni geri bildirim eklediğinizde** **Kurumsal Yönetim** kategorisini seçtiğinizden emin olun ve ardından aşağıdaki alt kategorilerinden birini seçin:
- Configuration Manager İstemcisi
- Configuration Manager Konsolu
- Configuration Manager işletim sistemi dağıtımı
- Configuration Manager sunucusu

Configuration Manager yeni özellik fikirlerini Oylamak için [UserVoice sayfasını](https://configurationmanager.uservoice.com/) kullanmaya devam edin. Configuration Manager ürün ekibi aşağıdaki UserVoice durum değerlerini kullanır:

- **Not** -isteği anladık ve anlamlı hale getiriyor. Kapsamımızı ekledik.
- **Planlanmış** -bu özellik için kodlama başladık ve önümüzdeki birkaç ay içinde bir teknik önizleme derlemesinde gösterilmesini bekledik.
- **Başlatıldı** -özellik artık bir teknoloji önizlemededir. Göz atın ve bize geri bildirimde bulunun. Özelliğin doğru parçada olduğunu bize bildirmek. Başkalarının görmesi ve açıklama koymak için özgün isteğin Comments bölümüne ek geri bildirim koyun. Bu bilgileri okuyup, özelliği geliştirmeyi denemek için geri bildirimi kullanacaksınız.
- **Tamamlandı** -özelliğin ilk sürümü bir üretim derlemesinde. Bu durum, özellikle %100 olan ve artık geliştirmeyen bir değer değildir. Ancak, özelliklerin v1 bir üretim derlemesinde olduğu ve gerçek için kullanmaya başlayabileceği anlamına gelir. Şu nedenle tamamlandı olarak işaretliyoruz:
  - Üretime hazırlanma özelliğinin olduğunu bilmeniz istiyoruz.
  - Diğer öğelerde kullanabilmeniz için UserVoice oylarınızı geri vermek istiyoruz.
  - Bu özelliğe yönelik en önemli geliştirme hakkında bilgi sahibi olmak için yeni tasarım değişikliği Isteklerini bu özelliğe kaydedebilirsiniz.

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a>Ekip Blogu Configuration Manager  

Configuration Manager mühendislik ve iş ortağı takımları, size Configuration Manager ve ilgili teknolojiler hakkında teknik bilgiler ve diğer haberleri sağlamak için [Enterprise Mobility + Security blogu](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) kullanır. Web günlüğü postalarımız ürün belgelerini tamamlar ve bilgileri destekler.  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a> Destek seçenekleri ve topluluk kaynakları  

Aşağıdaki bağlantılar destek seçenekleri ve topluluk kaynakları hakkında bilgi sağlar:  

-   [Microsoft desteği](https://aka.ms/cmcbsupport)  

-   [Configuration Manager Community: Configuration Manager (Güncel Dalı) acil değer Kılavuzu](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Configuration Manager forumları sayfası](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
