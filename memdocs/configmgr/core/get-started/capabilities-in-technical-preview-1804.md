---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview sürüm 1804 ' de bulunan yeni özellikler hakkında bilgi edinin.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b30386745244900e7f525f8f45b25a598628bf43
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078745"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Configuration Manager için Technical Preview 1804 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1804 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Technical Preview sitenize güncelleştirmek ve yeni özellikleri eklemek için yükleyebilirsiniz. 

Bu güncelleştirmeyi yüklemeden önce [Teknik Önizleme](technical-preview.md) makalesini gözden geçirin. Bu makalede, Technical Preview kullanımı, sürümler arasında nasıl güncelleştirme yapılacağı ve geri bildirimde bulunmak için genel gereksinimler ve sınırlamalar tamamladığınızda tercihinize.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Bu Technical Preview 'da bilinen sorunlar

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a>Güncelleştirmeleri indirmek için Kurulum bağlantısı çalışmıyor
<!--514334-->
Kurulumu medyadan çalıştırırsanız, ilk sayfa bu sürümde çalışmayan **en son Configuration Manager güncelleştirmelerini al**başlıklı bir bağlantı içerir. Bu bağlantı, kurulum için gerekli dosyaları indirmek içindir.

#### <a name="workaround"></a>Geçici çözüm
Kurulum için gerekli dosyaları indirmek için Kurulum Sihirbazı 'nı çalıştırın. Önkoşul Indirmeleri sayfasında, **gerekli dosyaları indirme**seçeneğini kullanın. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a>Uygulama Kataloğu Web hizmet noktası HTTPS etkin olamaz
<!--512637-->
Uygulama Kataloğu Web hizmet noktası HTTPS etkinse:

- Kullanıcılara kullanılabilir olarak dağıtılan uygulamalar, yazılım merkezi 'nde gösterilmez  

- Awebsctl. log dosyasında şu hata görüntülenir:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Geçici çözüm
HTTP bağlantılarını kullanarak iletişim kurmak için Uygulama Kataloğu Web hizmeti noktasını yeniden yapılandırın.  




</br>

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Site sunucusu için uzak içerik kitaplığı yapılandırma  
<!--1357525-->
Birincil site sunucunuzda sabit disk alanı boşaltmak için, [içerik kitaplığını](../plan-design/hierarchy/the-content-library.md) başka bir depolama konumuna yeniden yerleştir. İçerik kitaplığını site sunucusundaki başka bir sürücüye, ayrı bir sunucuya veya bir depolama alanı ağında (SAN) hataya dayanıklı disklere taşıyabilirsiniz. Değişen içerik gereksinimlerinizi karşılamak için zaman içinde büyüyerek veya küçüldüğü esnek depolama sağladığından bir SAN önerilir. 

Bu uzak içerik kitaplığı, [site sunucusu rolü yüksek kullanılabilirliği](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)için yeni bir önkoşuldur. 

> [!Note]  
> Bu eylem yalnızca site sunucusundaki içerik kitaplığını hareket ettirir. Dağıtım noktalarındaki içerik kitaplığının konumunu etkilemez. 

### <a name="prerequisites"></a>Önkoşullar  
- Site sunucusu bilgisayar hesabının, içerik kitaplığını taşıdığınız ağ yoluna **okuma** ve **yazma** izinleri olması gerekir. Uzak sistemde yüklü bileşen yok. 

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına geçin. **Site yapılandırması** ' nı genişletin ve **siteler**' i seçin. Ayrıntılar bölmesinin alt kısmındaki **Özet** sekmesinde, **içerik kitaplığı**için yeni bir sütuna dikkat edin.  

2. Şeritte **içerik kitaplığını Yönet** ' e tıklayın.  

3. **Bir ağ paylaşımında** seçin ve geçerli bir ağ yolu girin. Bu yol, sitenin içerik kitaplığını taşıdıkları konumdur. **Tamam**'a tıklayın.  

4. Ayrıntılar bölmesindeki Içerik kitaplığı sütununda **Status** özelliğini aklınızda edin. Sitenin, içerik kitaplığını taşırken ilerlemesini göstermek için güncelleştirir. Devam ederken, tamamlanma yüzdesini görüntüler. Bir hata durumu varsa, hatayı görüntüler. Yaygın hatalar şunlardır `access denied` `disk full`. Tamamlandığında, görüntülenir `OK`. Ayrıntılar için **Distmgr. log dosyasına** bakın. Daha fazla bilgi için bkz. [site sunucusu ve site sistemi sunucu günlükleri](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog).  

İçerik kitaplığını site sunucusuna geri taşımanız gerekiyorsa, bu işlemi tekrarlayın, ancak **site sunucusuna yerel**seçeneğini belirleyin.  

> [!Tip]  
> İçeriği site sunucusundaki başka bir sürücüye taşımak için, **Içerik kitaplığı aktarma** aracını kullanın. Daha fazla bilgi için bkz. [Configuration Manager araç seti](#configuration-manager-toolkit).  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a>Configuration Manager konsolundan geri bildirim gönderin  
<!--1357542-->

Gülümseme Gönder! Artık Configuration Manager ekibine deneyimleriniz hakkında doğrudan bilgi verebilirsiniz. Geri bildirimin gönderilmesi Configuration Manager konsolundan kolaydır. Tüm geri bildirimlerinizi duymak istiyoruz: Praise, sorunlar ve öneriler.  

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için **geri bildirim** gönderin.  

1. Configuration Manager konsolunda, şeridin üstündeki sağ üst köşedeki gülümseme düğmesine tıklayın.  

2. Aşağı açılan listeden, kullanılabilir seçeneklerden birini seçin:  

   - **Gülümseme gönderin**: gerçekten bir şey beğendim! Bu seçenek için geri bildirimlerinizin ayrıntılarını girin. Sonra isteğe bağlı olarak bir ekran görüntüsü ve e-posta adresinizi ekleyin.  

   - **Kaş çatma Gönder**: konsolda bir sorunla karşılaştık veya beklendiği gibi çalışmadı. Bu seçenek için olası ürün sorununun ayrıntılarını girin. Daha sonra isteğe bağlı olarak bir ekran görüntüsü, e-posta adresiniz ve Tanılama verileri ekleyin.  

   - **Öneri gönderin**: Configuration Manager değiştirme ve geliştirme fikriniz var. Bu seçenek, Web tarayıcınızda [UserVoice](https://configurationmanager.uservoice.com) sitemizi açar.  

Bu geri bildirim, Configuration Manager için doğrudan Microsoft ürün ekibine gider. Windows 10 Geri Bildirim Hub 'ı kullanılırken, yine de desteklenirken konsol içi geri bildirim mekanizmasını kullanmanız önerilir.  

Aşağıdaki anonim bilgiler, bağlam için geri bildirimde her zaman dahil edilmiştir:  

- Configuration Manager konsolu sürümü ve dili  

- Configuration Manager sitesi sürümü  

- Hiyerarşi KIMLIĞI olarak da bilinen destek KIMLIĞI  

- Konsolun çalıştığı sistem için işletim sistemi sürümü ve dili  

- Katmadan tıklandığı konsolundaki tam konum  

Bu veriler, tanılama ve kullanım verilerimizin koleksiyonuyla tutarlıdır. Daha fazla bilgi için bkz. [Tanılama ve kullanım verileri](../plan-design/diagnostics/diagnostics-and-usage-data.md).

### <a name="known-issues"></a>Bilinen sorunlar

İnternet 'e erişemeyecek bir cihazdan geri bildirim göndermeye çalışırsanız, uygulama beklenmedik şekilde kapatılabilir. Gülümseme ya da kaş çatma göndermek için cihazın petrol.office.microsoft.com 'e erişebilmesini sağlayın.



## <a name="support-center"></a>Destek Merkezi
<!--1357489-->

İstemci sorunlarını giderme, gerçek zamanlı günlük görüntüleme veya Configuration Manager istemci bilgisayarının durumunu daha sonra analiz edilmek üzere yakalama için destek merkezi 'ni kullanın. Destek Merkezi, birçok yönetici sorun giderme aracını birleştiren tek bir araçtır. Destek Merkezi 'nin en son sürümünün hata düzeltmeleri, iyileştirmeleri ve yeni günlük görüntüleyicimizin önizlemesi, Technical Preview 'da sunulmaktadır. Site sunucusunda, **CD. latest\SMSSETUP\Tools\SupportCenter** klasöründe bulunan destek merkezi yükleyicisini bulun.

 > [!Tip]  
 > Destek Merkezi 'ndeki mevcut işlevlere yönelik eski belgeler [TechNet](https://technet.microsoft.com/library/dn688621.aspx)'te bulunabilir. İlgili bilgiler, docs.microsoft.com kitaplığına geçiş yapmak için kullanılır.  

### <a name="new-support-center-features"></a>Yeni Destek Merkezi özellikleri  

- Yeni bir günlük Görüntüleyici, OneTrace. CMTrace 'e benzer ve sekmeli Görünüm ve yerleştirilebilir Windows gibi iyileştirmeler içerir.  

- Yeni bir veri toplayıcı özelliği, yerel veya uzak Configuration Manager istemcisinden tanılama günlüklerini toplar. Envanterin gerçek zamanlı tanılaması sağlar (Istemci Spy yerini alır), ilke (Ilke Spy yerini alır) ve istemci önbelleği.  



## <a name="configuration-manager-toolkit"></a>Configuration Manager araç seti
<!--1357145-->

Configuration Manager sunucusu ve istemci araçları artık Technical Preview 'a dahildir. Bunları site sunucusundaki **CD. latest\SMSSETUP\Tools** klasöründe bulabilirsiniz. Başka yükleme gerekli değildir.

#### <a name="server-tools"></a>Sunucu araçları  

- **DP Iş Yöneticisi**: içerik dağıtım işlerine dağıtım noktalarına sorun giderir  

- **Koleksiyon değerlendirme Görüntüleyicisi**: koleksiyon değerlendirmesi ayrıntılarını görüntüleme  

- **Içerik kitaplığı Gezgini**: içerik kitaplığı tek örnek deposunun içeriğini görüntüleme  

- **Içerik kitaplığı aktarımı**: içerik kitaplığını sürücüler arasında aktarır  

- **Içerik sahipliği aracı**: yalnız bırakılmış paketlerin sahipliğini değiştirir. Bu paketler sitede sahip olan bir site sunucusu olmadan bulunur.  

- **Rol tabanlı yönetim ve Denetim Aracı**: yöneticilerin rol yapılandırmasını denetlemenize yardımcı olur  

#### <a name="client-tools"></a>İstemci araçları

- **CMTrace**: günlükleri görüntüleme  

- **Dağıtım Izleme aracı**: uygulamalarda, güncelleştirmelerde ve temel dağıtımların sorunlarını giderme  

- **Ilke Spy**: ilke atamalarını görüntüleme  

- **Power Viewer aracı**: güç yönetimi özelliğinin durumunu görüntüleme  

- **Zamanlama aracı gönder**: DCM temellerinin zamanlamalarını ve değerlendirmesini tetikleme  

> [!Important]  
> Aşağıdaki araçlar için aynı veya geliştirilmiş işlevleri içerdiğinden, çoğu kullanım durumu için [Destek Merkezi](#support-center) önerilir:  
> - İstemci Gözetleme
> - CMTrace<sup>1</sup> 
> - Dağıtım İzleme Aracı
> - İlke Gözetleme
> - Gönderme Zamanlaması Aracı
> 
> <sup>1</sup> CMTrace, .net veya WINDOWS PRESENTATION FOUNDATION (WPF) öğesine bağlı değildir, bu nedenle Windows PE önyükleme görüntülerinde kullanılmaya devam etmektedir.

### <a name="known-issues"></a>Bilinen sorunlar
Bazı istemci ve sunucu araçları, başlatılırken beklenmedik şekilde çıkabilir. Bu sorun, medyadaki bir dosyanın eksik olmasından kaynaklanır. Geçici bir çözüm olarak, **Microsoft. Diagnostics. Tracing. EventSource. dll** dosyasını AdminConsole\bin dizininden hem SMSSETUP\Tools\ClientTools hem de servertools dizinlerine kopyalayın. Bu dosya, Configuration Manager Konsolu tarafından kullanılan sürümle aynı olmalıdır. Diğer sürümler çalışmayabilir. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Onay iptalinde uygulamayı kaldır
<!--1357891-->

Bir uygulama için onayı iptal ettiğinizde davranış değişmiştir. Artık uygulama isteğini reddetmeniz durumunda, istemci uygulamayı kullanıcının cihazından kaldırır. 

### <a name="prerequisites"></a>Önkoşullar
- **Cihaz başına Kullanıcı için uygulama Isteklerini Onayla**özelliğini etkinleştirin.

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda, bir kullanıcıya onay gerektiren bir uygulama dağıtın. Dağıtımın **dağıtım ayarları** sekmesinde **bir yöneticinin cihazdaki bu uygulama için bir isteği onaylaması gereken**seçeneği etkinleştirin.  

2. Yazılım merkezindeki Configuration Manager istemcisinde, Kullanıcı uygulamayı yüklemeye onay ister.  

3. Configuration Manager konsolunda, uygulamayı cihaza yüklemek için bu kullanıcıya yönelik isteği onaylayın. Uygulama onay istekleri, **yazılım kitaplığı** çalışma alanında, **uygulama yönetimi**altında, **onay istekleri** düğümünde görüntülenir.  

4. Yazılım Merkezi 'nde istemcisinde Kullanıcı, uygulamayı yüklüyor.  

5. Configuration Manager konsolunda, kullanıcının cihazdaki uygulama isteğini reddedin.  

### <a name="known-issues"></a>Bilinen sorunlar
- Kullanıcı uygulamayı istemciye yükledikten sonra, kullanıcı ilkesini güncelleştirin. Yazılım Merkezi 'nde, **Seçenekler** sekmesine geçin, **Bilgisayar Bakımı** ' nı genişletin ve **ilkeyi Eşitle**' ye tıklayın.<!--480609-->  

- Uygulama Kataloğu Web hizmet noktası HTTP olmalıdır. Daha fazla bilgi için [Bu teknik önizlemede bilinen sorunlar](#bkmk_appcathttps)bölümüne bakın.<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Active Directory kapsayıcılarını keşifden hariç tut
<!--1358143-->
Bulunan nesnelerin sayısını azaltmak için artık Active Directory sistem bulağından belirli kapsayıcıları dışarıda bırakabilirsiniz. Bu özellik [UserVoice geri bildirimlerinizin](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery)bir sonucudur.

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Hiyerarşi Yapılandırması** ' nı genişletin ve **keşif yöntemleri**' ni seçin. **Active Directory sistem bulma** ' yı seçin ve Şeritteki **Özellikler** ' e tıklayın.  

2. Yeni bir Active Directory kapsayıcısı belirtmek için yeni simgesine tıklayın.   

3. Bulma işlemini başlatmak için Active Directory kapsayıcı iletişim kutusunda konum bölümüne gidin veya **yola** girin.  

4. Arama seçenekleri bölümünde, **alt kapsayıcıları Active Directory yinelemeli olarak arama**seçeneğini etkinleştirin. Ardından **Ekle** ' ye tıklayarak bu bulmadan dışlanacak alt kapsayıcıları seçin.  

5. Yeni kapsayıcı Seç iletişim kutusunda, dışlanacak bir alt kapsayıcı seçin. Yeni kapsayıcı Seç iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.  

6. Active Directory kapsayıcı iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.  

7. Active Directory sistem keşfi Özellikler penceresi, bulmanın başladığı Active Directory kapsayıcısının yoluna bakın. **Özyinelemeli** sütun **Evet**' i gösterir ve yeni **Dışlamalar** sütunu da **Evet**' i gösterir. Active Directory sistem bulma Özellikler penceresi kapatmak için **Tamam** ' ı tıklatın.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Yazılım Merkezi 'nde Uygulama Kataloğu web sitesi bağlantısının görünürlüğünü belirtin
<!--1358214-->

Artık, **Uygulama Kataloğu Web sitesini açma** bağlantısının, yazılım merkezi 'nin **yükleme durumu** düğümünde görünüp başlatılmayacağını kontrol edebilirsiniz.  

> [!Note]  
> Uygulama Kataloğu web sitesi kullanıcı deneyimi için destek, 1 Haziran 2018 ' den sonra yayımlanan ilk güncelleştirmeyle sona erer. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](#bkmk_feedback) gönderin.

1. Configuration Manager konsolu, **Yönetim** çalışma alanı, **istemci ayarları** düğümünde özel bir istemci cihaz ayarları ilkesi oluşturun.  

2. **Yazılım Merkezi** grubunu seçin.  

3. **Yazılım Merkezi ayarları**için **Özelleştir**' e tıklayın.  

4. **Yazılım merkezindeki Uygulama Kataloğu web sitesi bağlantısını gizleme**seçeneğini etkinleştirin.   

İstemci ayarları hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../clients/deploy/configure-client-settings.md).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Otomatik dağıtım kurallarını yazılım güncelleştirme mimarisine göre filtrele
 <!--1322266-->
Artık Itanium ve ARM64 gibi mimarileri hariç tutmak için otomatik dağıtım kurallarını filtreleyebilirsiniz.

### <a name="try-it-out"></a>Deneyin!
Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına geçin. **Yazılım güncelleştirmeleri** ' ni genişletin ve **Otomatik dağıtım kuralları**' nı seçin. Şeritte **Otomatik dağıtım kuralı oluştur**' u seçin.  

2. **Genel** sekmesi ve **dağıtım ayarları** sekmesi için uygun ayarları girin.  

3. **Yazılım güncelleştirmeleri** sekmesinde **mimari** ' i seçin ve **arama ölçütlerinde** **bulunacak öğeler ' e** tıklayın.  

4. Otomatik Dağıtım kuralına eklemek istediğiniz mimarileri seçin.  

5. **İleri** ' ye tıklayın ve otomatik dağıtım kuralının oluşturulmasına devam edin.  

> [!IMPORTANT]  
> 64 bit (x64) sistemlerde çalışan 32-bit (x86) uygulamaları ve bileşenleri olduğunu unutmayın. X86 gerekmediği sürece, x64 ' u seçtiğinizde de etkinleştirin.  

### <a name="known-issues"></a>Bilinen sorunlar
Mimari ölçütlerini ekledikten sonra, otomatik dağıtım kuralı Özellikler sayfasında arama ölçütlerinde **başlık** görüntülenir. Otomatik dağıtım kuralı hala beklendiği gibi çalışır ve doğru yazılım güncelleştirmelerini seçer. Ancak, şu anda hem **mimari** hem de **başlık** ölçütünü dahil edebilirsiniz. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>İşletim sistemi dağıtımına yönelik iyileştirmeler
İşletim sistemi dağıtımı için, bazıları Kullanıcı sesli geri bildirimlerinizin sonucu olan aşağıdaki geliştirmeleri yaptık.  

- [Görev sırası değişkenlerinde depolanan hassas verileri maskeleme](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): [görev dizisi değişkenini ayarla](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) adımında, **Bu değeri gösterme**yeni seçeneğini belirleyin. Örneğin, bir parola belirtirken.<!--1358330--> Bu seçeneği etkinleştirdiğinizde aşağıdaki davranışlar geçerlidir:
  - Değişkenin değeri Smsts. log dosyasında gösterilmez.
  - Configuration Manager konsolu ve SMS sağlayıcısı, bu değeri parolalar gibi diğer gizli bilgilerle aynı şekilde işler.
  - Görev sırasını dışarı aktardığınızda değer dahil değildir.
  - Adımı düzenlerken görev sırası Düzenleyicisi bu değeri okumaz. Değişiklik yapmak için tüm değeri yeniden yazın.

  > [!Important]  
  > Değişkenler ve değerleri, görev dizisiyle XML olarak kaydedilir ve veritabanında karıştırılmış şekilde işlenir. İstemci, yönetim noktasından bir görev sırası ilkesi istediğinde, aktarım sırasında ve istemcide depolandığında şifrelenir. Ancak, tüm değişken değerleri, istemci üzerinde çalışma zamanı sırasında bellekteki görev dizisi ortamında düz metindir. Görev sırası, değişkenin değerini çıkış için bir adım içeriyorsa, bu çıkış düz metin biçiminde olur. Bu davranış, yönetici tarafından görev dizisine böyle bir adım eklemek için açık bir eylem gerektirir. 


- [Görev dizisinin komut adımını Çalıştır sırasında program adını maskele](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): büyük olasılıkla hassas verilerin görüntülenmesini veya günlüğe kaydedilmesini engellemek Için **Osddonotlogcommand** görev sırası değişkenini olarak `TRUE`ayarlayın. Bu değişken, [komut satırını Çalıştır](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) görev dizisi adımı sırasında Smsts. log dosyasındaki program adını maskeler. <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager konsolundaki geliştirmeler
- Birincil Kullanıcı bilgileri artık **varlıklar ve uyumluluk**, **Cihaz Koleksiyonları**altında bir koleksiyonun üyeleri görüntülenirken görünür.<!--510252-->  



## <a name="next-steps"></a>Sonraki adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).    
