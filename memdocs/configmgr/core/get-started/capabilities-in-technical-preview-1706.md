---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1706 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 79258786b56cc3e7fe4971391903772700768a89
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126765"
---
# <a name="capabilities-in-technical-preview-1706-for-configuration-manager"></a>Configuration Manager için Technical Preview 1706 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1706 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanma, sürümler arasında güncelleştirme yapma ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlama hakkında bilgi almak üzere [Configuration Manager Için Teknik önizlemeyi](../../core/get-started/technical-preview.md) gözden geçirin.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Bu teknik önizlemede bilinen sorunlar:**

- **Dağıtım noktasını taşı** -tek bir birincil sitenin Technical Preview sınırı nedeniyle, bir dağıtım noktasını siteler arasında taşımak için konsolundaki seçenekler bu sürümle kullanılamaz.

- **Cihaz uyumluluk ayarları** -yeni cihaz uyumluluk ayarlarının ikisini de kullanırken ters davranışla karşılaşabilirsiniz:
  - **Cihazda USB hata ayıklamayı engelle**
  - **Bilinmeyen kaynaklardan gelen uygulamaları engelle**

    Örneğin, Yöneticiler **CIHAZDA USB hata ayıklamayı engelle** seçeneğini **true**olarak ayarlandıysa, USB hata ayıklaması etkinleştirilmemiş olan tüm cihazlar uyumlu değil olarak işaretlenir.

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Yazılım güncelleştirme noktaları için iyileştirilmiş sınır grupları
<!-- 1324591 -->
Bu sürüm, yazılım güncelleştirme noktalarının sınır gruplarıyla nasıl çalıştığı hakkında iyileştirmeler içerir. Aşağıda yeni geri dönüş davranışı özetlenmektedir:
- Yazılım güncelleştirme noktaları için geri dönüş, en az 120 dakikalık süre içinde komşu sınır gruplarına geri dönüş için yapılandırılabilir bir zaman kullanır.

- Geri dönüş yapılandırmasından bağımsız olarak, bir istemci 120 dakika boyunca kullanılan son yazılım güncelleştirme noktasına ulaşmaya çalışır. Bu sunucuya 120 dakika boyunca ulaşamadıktan sonra istemci, kullanılabilir yazılım güncelleştirme noktası havuzunu denetleyerek yeni bir tane bulabilir.

  - İstemcinin geçerli sınır grubundaki tüm yazılım güncelleştirme noktaları, istemcinin havuzuna hemen eklenir.

  - Bir istemci yeni bir arama yapmadan önce 120 dakika boyunca özgün sunucusunu kullanmaya çalıştığından, iki saat geçtikten sonra ek sunucu ile bağlantı kurulamadı.

  - Bir komşu grubuna geri dönüş en az 120 dakikalık bir yapılandırılmışsa, bu komşu sınır grubundaki yazılım güncelleştirme noktaları, istemcinin kullanılabilir sunucular havuzunun bir parçası olur.

- İki saat boyunca özgün sunucusuna ulaşamadıktan sonra istemci, yeni bir yazılım güncelleştirme noktasıyla iletişim kurmaya yönelik daha kısa bir döngüye geçer.

  Bu, bir istemcinin yeni bir sunucuyla bağlantı kuramamasıdır, bir sonraki sunucuyu kullanılabilir sunucu havuzundan hızlıca seçer ve bununla iletişim kurmayı dener.

  - Bu geçiş, istemci tarafından kullanılabilecek bir yazılım güncelleştirme noktasına bağlanana kadar devam eder.
  - İstemci bir yazılım güncelleştirme noktası bulana kadar, her bir komşu sınır grubu için geri dönüş süresi karşılandığında kullanılabilir sunucular havuzuna ek sunucular eklenir.

Daha fazla bilgi için, Güncel Dalı için sınır grupları konusundaki [yazılım güncelleştirme noktaları](../servers/deploy/configure/boundary-groups.md#bkmk_sup) bölümüne bakın.


## <a name="site-server-role-high-availability"></a>Site sunucusu rolü yüksek kullanılabilirlik
<!-- 1128774 -->
Site sunucusu rolü için yüksek kullanılabilirlik, *Pasif* modda ek bir birincil site sunucusu yüklemek için Configuration Manager tabanlı bir çözümdür. Pasif mod site sunucusu, *etkin* modda olan mevcut birincil site sunucunuza ek niteliğindedir. Bir Pasif mod site sunucusu, gerektiğinde hemen kullanılmak üzere kullanılabilir.

Pasif moddaki bir birincil site sunucusu:
- , Etkin site sunucunuz ile aynı site veritabanını kullanır.
- Etkin site sunucuları içerik kitaplığının, daha sonra eşitlenmiş olarak tutulan bir kopyasını alır.
- , Pasif modda olduğu sürece site veritabanına veri yazmıyor.
- , Pasif modda olduğu sürece isteğe bağlı site sistemi rollerinin yüklenmesini veya kaldırılmasını desteklemez.

Pasif mod site sunucusunu etkin mod site sunucusuna getirmek için, bunu el ile yükseltebilirsiniz. Bu, etkin site sunucusunu pasif site sunucusu olacak şekilde geçirir. Özgün etkin mod sunucusunda bulunan site sistem rolleri, bilgisayar erişilebilir olduğu sürece kullanılabilir kalır. Yalnızca site sunucusu rolü etkin ve Pasif mod arasında geçiş yaptı.

Pasif mod site sunucusu yüklemek için **site sistemi sunucusu oluşturma Sihirbazı 'nı** kullanarak, bir **birincil site sunucusu** ve bir **Pasif**mod ile yeni bir site sunucusu yapılandırabilirsiniz. Daha sonra sihirbaz, yeni site sunucusunu pasif modda yüklemek için belirtilen sunucuda kurulum Configuration Manager çalıştırır. Yükleme tamamlandıktan sonra, etkin mod site sunucusu, Pasif mod site sunucusunu ve içerik kitaplığını, etkin site sunucusunda yaptığınız değişikliklerle veya konfigürasyonlarla eşitlenmiş halde tutar.

### <a name="prerequisites-and-limitations"></a>Önkoşullar ve sınırlamalar
- Pasif moddaki tek bir site sunucusu her birincil sitede desteklenir.

- Pasif moddaki site sunucusu, Azure 'da şirket içi veya bulut tabanlı olabilir.

- Hem etkin mod hem de Pasif mod site sunucuları aynı etki alanında olmalıdır.

- Hem etkin mod hem de Pasif mod site sunucularının aynı site veritabanını kullanması gerekir. Bu, her site sunucusunun bilgisayarlarının uzak olması gerekir.

    - Veritabanını barındıran SQL Server, örnek, SQL Server kümesi veya Always on kullanılabilirlik grubu adlı bir varsayılan örnek kullanabilir.

    - Pasif moddaki site sunucusu, etkin mod site sunucusuyla aynı site veritabanını kullanacak şekilde yapılandırılmıştır. Ancak Pasif mod site sunucusu, etkin moda yükseltilene kadar bu veritabanını kullanmaz.

- Pasif mod site sunucusunu çalıştıracak bilgisayar:

    - [Birincil bir siteyi yükleme önkoşulları](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site)ile Buluşmalıdır.

    - , Etkin mod site sunucusunun sürümüyle eşleşen kaynak dosyalarını kullanarak yüklenir.

    - Pasif mod sitesini yüklemeden önce herhangi bir siteden bir site sistem rolü olamaz.

- Etkin ve Pasif mod site sunucusu bilgisayarları, farklı işletim sistemlerini veya hizmet paketi sürümlerini çalıştırabilir, bu nedenle her ikisi de Configuration Manager sürümünüz tarafından desteklendiğinden kalır.

- Pasif mod site sunucusunun etkin mod sunucusuna yükseltilmesi el ile yapılır. Otomatik yük devretme yok.

- Site sistem rolleri yalnızca etkin modda olan site sunucusuna yüklenebilir.

    - Etkin moddaki bir site sunucusu tüm site sistem rollerini destekler. Site sistemi rollerini pasif moddayken sunucuya yükleyemezsiniz.

    - Veritabanı kullanan site sistem rollerinin (Raporlama noktası gibi), hem etkin mod hem de Pasif mod site sunucularından uzak bir sunucuda bu veritabanına sahip olması gerekir.

    - SMS_Provider, site sunucusuna pasif modda yüklenmez. Pasif mod site sunucusunu etkin moda el ile yükseltmek üzere site için bir SMS_Provider bağlanmanız gerektiğinden, ek bir bilgisayara [sağlayıcının en az bir ek örneğini yüklemeniz](../plan-design/hierarchy/plan-for-the-sms-provider.md) önerilir.

**Bilinen sorun**:   
Bu sürümle birlikte, aşağıdaki koşulların **durumu** konsolunda okunabilir metin yerine sayısal değerler olarak görünür:
- 131071 – site sunucusu yüklemesi başarısız oldu
- 720895 – site sunucusu rolü kaldırma başarısız oldu
- 851967 – yük devretme başarısız oldu

### <a name="add-a-site-server-in-passive-mode"></a>Pasif modda site sunucusu ekleme
1. Konsolunda **Yönetim**  >  **Site yapılandırması**  >  **siteler** ' e gidin ve [site sistemi rolleri ekleme Sihirbazı](../servers/deploy/configure/install-site-system-roles.md)' nı başlatın. **Site sistemi sunucusu oluşturma Sihirbazı 'nı**da kullanabilirsiniz.

2. **Genel** sayfasında, Pasif mod site sunucusunu barındıracak sunucuyu belirtin. Belirttiğiniz sunucu, site sunucusunu pasif modda yüklemeden önce herhangi bir site sistemi rolünü barındıramıyor.

3. **Sistem rolü seçimi** sayfasında, yalnızca **pasif modda birincil site sunucusu**' nu seçin.

4. Sihirbazı tamamladığınızda, kurulum 'U çalıştırmak ve site sunucusu rolünü belirtilen sunucuya yüklemek için kullanılan aşağıdaki bilgileri sağlamanız gerekir:
    - Yükleme dosyalarını etkin site sunucusundan yeni pasif mod site sunucusuna kopyalamayı seçin ya da etkin site sunucusunun CD içeriğini içeren bir konumun yolunu belirtin **. En son** klasör.

    - Etkin mod site sunucusu tarafından kullanılan aynı site veritabanı sunucusunu ve veritabanı adını belirtin.

5. Configuration Manager daha sonra site sunucusunu belirtilen sunucuda pasif modda yükleyecek.

Ayrıntılı yükleme durumu için **Yönetim**  >  **Site yapılandırması**  >  **siteler**' e gidin.
- Pasif moddaki site sunucusunun durumu **yükleme**olarak görüntülenir.

- Daha ayrıntılı bilgi için sunucuyu seçin ve ardından **site sunucusu yükleme durumunu** açmak Için **durumu göster** ' e tıklayın.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Pasif mod site sunucusunu etkin moda yükselt
Pasif mod site sunucusunu etkin moda değiştirmek istediğinizde, **Nodes** **Yönetim**  >  **sitesi yapılandırma**  >  **siteleri**' nde düğümler bölmesinden bunu yapabilirsiniz. SMS_Provider bir örneğine erişebileceğiniz sürece, bu değişikliği yapmak için sitesine erişebilirsiniz.
1. Configuration Manager konsolunun **düğümler** bölmesinde, site sunucusunu pasif modda seçin ve ardından şeritten **etkin 'e Yükselt**' i seçin.

2. Yükseltmekte olduğunuz sunucunun basit **durumu** , **yükseltme**olarak **düğümler** bölmesinde görüntülenir.

3. Yükseltme tamamlandıktan sonra, **durum** sütunu hem yeni *etkin* mod site sunucusu hem de yeni *Pasif* mod site sunucusu için **Tamam** ' ı gösterir.

4. **Yönetim**  >  **sitesi yapılandırma**  >  **sitelerinde**, birincil site sunucusunun adı artık yeni *etkin* mod site sunucusunun adını görüntüler.
Ayrıntılı durum için, **Monitoring**  >  **site sunucusu durumunu**izleme ' ye gidin.
    - **Mod** sütunu, hangi sunucunun *etkin* veya *Pasif*olduğunu tanımlar.

    - Bir sunucuyu pasif moddan etkin moda yükseltirken, etkin duruma yükselttiğiniz site sunucusunu seçin ve ardından Şeritteki **durumu göster** ' i seçin. Bu işlem hakkında ek ayrıntılar görüntüleyen **site sunucusu yükseltme durumu** penceresini açar.

Etkin moddaki bir site sunucusu pasif moda geçtiğinde, yalnızca site sistem rolü pasif hale getirilir. Bu bilgisayarda yüklü olan diğer tüm site sistem rolleri etkin ve istemciler tarafından erişilebilir durumda kalır.


### <a name="daily-monitoring"></a>Günlük izleme
Pasif modda bir birincil siteniz varsa, etkin mod site sunucusuyla eşitlenmiş ve kullanıma hazırsa emin olmak için günlük olarak izleyin. Bunu yapmak için, **Monitoring**  >  **site sunucusu durumunu**izleme ' ye gidin. Burada hem etkin modu hem de Pasif mod site sunucularını görüntüleyebilirsiniz.

**Özet** sekmesi:
- **Mod** sütunu, hangi sunucunun etkin veya pasif olduğunu tanımlar.
- Pasif mod sunucusu etkin mod sunucusuyla eşitlenmiş olduğunda **durum** sütunu **Tamam ' ı** listeler.
- İçerik eşitlemesinin durumu hakkında ek ayrıntıları görüntülemek için Içerik eşitleme durumundan **durumu göster** ' e tıklayın. Bu, içerik eşitleme sorunlarını gidermeyi deneyebileceğiniz Içerik Kitaplığı sekmesini açar.

**Içerik kitaplığı** sekmesi:
- Etkin site sunucusundan Pasif mod site sunucusuna eşitlenen içeriğin **durumunu** görüntüleyin.
- Durumu **başarısız**olan içerik ' i seçip Şeritteki **Seçili öğeleri eşitle** ' yi seçin. Bu eylem içeriği içeriğin kaynağından Pasif mod site sunucusuna yeniden eşitlemeyi dener. Kurtarma sırasında durum **devam ediyor**olarak görüntülenir ve eşitlenmiş olduğunda **başarılı**olarak görüntülenir.

### <a name="try-it-out"></a>Deneyin!
Aşağıdaki görevleri tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için şeridin **giriş** sekmesinden bize **geri bildirim** gönderin:
- Bir birincil siteyi pasif modda yükleyebiliyorum.
- Etkin mod site sunucusu yapmak üzere Pasif mod site sunucusunu yükseltmek için konsolunu kullanabilir ve her iki site sunucusu için durum değişikliğini doğrulayabilirsiniz.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Bir Device Guard ilkesindeki belirli dosya ve klasörler için güven Ekle
<!-- 1324676 -->
Bu sürümde, [Device Guard](../../protect/deploy-use/use-device-guard-with-configuration-manager.md) ilke yönetimine daha fazla özellik ekledik

Artık isteğe bağlı olarak, bir Device Guard ilkesindeki klasörler için belirli dosyalar için güven ekleyebilirsiniz. Bu şunları yapmanızı sağlar:

1. Yönetilen yükleyici davranışları ile ilgili sorunları aşmak
2. Configuration Manager ile dağıtılabilecek iş kolu uygulamalarına güvenin
3. Bir işletim sistemi dağıtım görüntüsüne dahil olan uygulamalara güvenin.

### <a name="try-it-out"></a>Deneyin!

1. Bir Device Guard ilkesi oluştururken, cihaz koruyucu ilkesi oluşturma Sihirbazı 'nın Içermeler sekmesinde **Ekle**' ye tıklayın.
2. **Güvenilen dosya veya klasör ekle** iletişim kutusunda, güvenmek istediğiniz dosya veya klasör hakkındaki bilgileri belirtin. Yerel bir dosya veya klasör yolu belirtebilir veya bağlama izninizin olduğu uzak bir cihaza bağlanabilir ya da bu cihazda bir dosya veya klasör yolu belirtebilirsiniz.
3. Sihirbazı tamamlayın.


## <a name="hide-task-sequence-progress"></a>Görev sırası ilerlemesini gizle
<!-- 1354291 -->
Bu sürümde, yeni bir değişken kullanarak görev sırası ilerleme durumunun son kullanıcılara ne zaman görüntüleneceğini kontrol edebilirsiniz. Görev dizisinde, görev sırası ilerleme durumunu gizlemek veya göstermek için **TSDisableProgressUI** değişkeninin değerini ayarlamak Için **görev dizisi değişkenini ayarla** adımını kullanın. Değişkenin değerini değiştirmek için görev dizisi değişkenini birden çok kez bir görev dizisinde kullanabilirsiniz. Bu, görev dizisinin farklı bölümlerinde görev dizisi ilerlemesini gizleme veya görüntüleme olanağı sağlar.

#### <a name="to-hide-task-sequence-progress"></a>Görev sırası ilerlemesini gizlemek için
Görev dizisi ilerlemesini gizlemek için görev sırası Düzenleyicisi 'nde, **TSDisableProgressUI** değişkeninin değerini **true** olarak ayarlamak Için [görev dizisi değişkenini ayarla](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) adımını kullanın.

#### <a name="to-display-task-sequence-progress"></a>Görev sırası ilerlemesini görüntüleme
Görev sırası Düzenleyicisi ' nde, görev sırası ilerlemesini göstermek için **TSDisableProgressUI** değişkeninin değerini **false** olarak ayarlamak Için [görev dizisi değişkenini ayarla](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) adımını kullanın.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>İçerik yükleme ve içeriği kaldırma için farklı bir içerik konumu belirtin
<!-- 1097546 -->
Bugün Configuration Manager, bir uygulamanın kurulum dosyalarını içeren yükleme konumunu belirtirsiniz. Bir yükleme konumu belirttiğinizde, bu, uygulama içeriği için kaldırma konumu olarak da kullanılır.
Geri bildirimlerinize bağlı olarak, dağıtılan bir uygulamayı kaldırmak istediğinizde ve uygulama içeriği istemci bilgisayarda değilse, istemci, uygulama kaldırılmadan önce tüm uygulama kurulum dosyalarını yeniden indirirler.
Bu sorunu çözmek için artık hem yükleme içeriği konumunu hem de isteğe bağlı bir kaldırma içeriği konumunu belirtebilirsiniz. Ayrıca, kaldırma içeriği konumunu belirtmemelidir.

### <a name="try-it-out"></a>Deneyin!

1. Uygulamanın dağıtım türü özelliklerinde **içerik** sekmesine tıklayın.
2. **Yüklemeyi içerik konumunu** normal olarak yapılandırın.
3. **Içerik kaldırma ayarları**için aşağıdakilerden birini seçin:
   - **Yükleme Içeriğiyle aynı** -aynı içerik konumu, uygulamayı yükleyip yüklemeinizden bağımsız olarak kullanılacaktır.
   - **Kaldırma Içeriği yok** -uygulama için kaldırma içeriği konumu sağlamak istemiyorsanız bunu seçin.
   - **Yükleme Içeriğinden farklı** -yükleme içeriği konumundan farklı bir kaldırma içeriği konumu belirtmek istiyorsanız bunu seçin.
5. **Yükleme Içeriğinden farklı**seçeneğini belirlediyseniz, uygulamayı kaldırmak için kullanılacak uygulama içeriğinin konumuna gidin veya konumunu girin.
6. Dağıtım türü Özellikler iletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.


## <a name="accessibility-improvements"></a>Erişilebilirlik geliştirmeleri  
<!--1253000 -->
Bu önizleme Configuration Manager konsolundaki [erişilebilirlik özelliklerine](../understand/accessibility-features.md) yönelik çeşitli geliştirmeler sunar. Bu modüller şunlardır:     

**Konsol etrafında gezinmek için yeni klavye kısayolları:**
- CTRL + a-ana (orta) bölmedeki odağı ayarlar.
- CTRL + T-odağı gezinti bölmesindeki üst düğüme ayarlar. Odak zaten bu bölmesdeyse, odak ziyaret ettiğiniz son düğüme ayarlanır.
- CTRL + I-odağı, şerit 'in altında bulunan içerik haritası çubuğuna ayarlar.
- CTRL + L-kullanılabilir olduğunda odağı **arama** alanına ayarlar.
- CTRL + D-kullanılabilir olduğunda odağı Ayrıntılar bölmesine ayarlar.
- Alt: değişiklikler Şeridin içine ve dışına odaklanmaktadır.

**Genel geliştirmeler:**
- Bir düğüm adının harflerini yazdığınızda gezinti bölmesinde geliştirilmiş gezinme.
- Ana görünüm ve şerit aracılığıyla klavye gezintisi artık dairesel.
- Ayrıntılar bölmesindeki klavye gezintisi artık dairesel. Önceki nesneye veya bölmeye dönmek için CTRL + D, ardından SHIFT + TAB tuşlarını kullanın.
- Çalışma alanı görünümünü yenilemeden sonra odak, bu çalışma alanının ana bölmesine ayarlanır.
- Ekran okuyucularının liste öğelerinin adlarını duyurduğunu sağlayan bir sorun düzeltildi.
- Sayfada, ekran okuyucularının önemli bilgileri duyurmalarını sağlayan birden çok denetim için erişilebilir adlar eklendi.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Azure Hizmetleri Sihirbazı 'Nda Yükseltme Hazırlığı desteklemek için yapılan değişiklikler
<!-- 1353331 -->
Bu sürümden itibaren, Configuration Manager bir bağlantıyı Yükseltme Hazırlığı olarak yapılandırmak için Azure Hizmetleri Sihirbazı 'Nı kullanın. Sihirbazın kullanımı, ilgili Azure hizmetleri için ortak bir sihirbaz kullanarak bağlayıcının yapılandırılmasını basitleştirir.   

Bağlantıyı yapılandırma yöntemi değişmiş olsa da, bağlantı için Önkoşullar ve Yükseltme Hazırlığı nasıl kullanılır, değişmeden kalır.   

### <a name="prerequisites-for-upgrade-readiness"></a>Yükseltme Hazırlığı önkoşulları
Yükseltme Hazırlığı bağlantısının önkoşulları, Configuration Manager Güncel Dalı açısından ayrıntılananlardan değiştirilmez. Daha kolay bir şekilde tekrarlanırlar:  

**Önkoşullar**
- Bağlantıyı eklemek için, Configuration Manager ortamınızın bir [çevrimiçi modda](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)bir [hizmet bağlantı noktası](../servers/deploy/configure/about-the-service-connection-point.md) yapılandırması gerekir. Bağlantıyı ortamınıza eklediğinizde, bu site sistem rolünü çalıştıran makineye Microsoft Monitoring Agent de yükler.
- Configuration Manager bir "Web uygulaması ve/veya Web API" yönetim aracı olarak kaydedin ve [ISTEMCI kimliğini bu kayıttan](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/)alın.
- Azure Active Directory ' de kayıtlı yönetim aracı için bir istemci anahtarı oluşturun.
- Azure portal, kayıtlı Web uygulamasına OMS 'ye erişim izni verin.

> [!IMPORTANT]       
> OMS 'ye erişim izni yapılandırırken, **katkıda bulunan** rolünü seçtiğinizden emin olun ve bu izinleri kayıtlı uygulamanın kaynak grubuna atayın.

Önkoşullar yapılandırıldıktan sonra, bağlantıyı oluşturmak için Sihirbazı kullanmaya hazırlanın.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Yükseltme Hazırlığı yapılandırmak için Azure Hizmetleri Sihirbazı 'Nı kullanın
1. Konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **Azure hizmetleri**' ne gidin ve ardından Şeritteki **giriş** sekmesinden **Azure hizmetlerini yapılandır** ' ı seçerek **Azure Hizmetleri Sihirbazı 'nı**başlatın.

2. **Azure hizmetleri** sayfasında **yükseltme hazırlığı bağlayıcısını**seçin ve ardından **İleri**' ye tıklayın.

3. **Uygulama** sayfasında, **Azure ortamınızı** belirtin (Technical Preview yalnızca genel bulutu destekler). Ardından **Içeri aktar** ' a tıklayarak **uygulamalar içeri aktar** penceresini açın.

4. **Uygulamaları Içeri aktar** penceresinde, Azure AD 'de zaten var olan bir Web uygulamasının ayrıntılarını belirtin.
    - Azure AD kiracı adı için kolay bir ad sağlayın. Ardından kiracı KIMLIĞINI, uygulama adını, Istemci KIMLIĞINI, Azure Web uygulaması için gizli anahtarı ve uygulama KIMLIĞI URI 'sini belirtin.
    - **Doğrula**' yı tıklatın ve başarılı olursa devam etmek için **Tamam** ' ı tıklatın.

5.  **Yapılandırma** sayfasında, yükseltme hazırlığı için bu bağlantıyla birlikte kullanmak istediğiniz aboneliği, kaynak grubunu ve Windows Analytics çalışma alanını belirtin.  

6. **İleri** ' ye tıklayarak **Özet** sayfasına gidin ve bağlantıyı oluşturmak için Sihirbazı tamamlayın.


## <a name="new-client-settings-for-cloud-services"></a>Bulut hizmetleri için yeni istemci ayarları
<!-- 1319883 -->

Bu sürümde, Configuration Manager için iki yeni istemci ayarı ekledik. Bunları **Cloud Services** bölümünde bulabilirsiniz.  Bu ayarlar size aşağıdaki olanakları sağlar:

- Hangi Configuration Manager istemcilerinin yapılandırılmış bir bulut yönetimi ağ geçidine erişebileceğini denetleyin.
- Windows 10 etki alanına katılmış Yapılandırma Yöneticisi istemcilerini Azure Active Directory otomatik olarak kaydeder.

Bu yeni ayarlar [Configuration Manager 1705 Technical Preview](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)sürümünde açıklanan özellikleri gerçekleştirmenize yardımcı olur.

### <a name="before-you-start"></a>Başlamadan önce

Şirket içi Active Directory ve Azure AD kiracınız arasında Azure AD Connect yüklemiş ve yapılandırmış olmanız gerekir.

Bağlantıyı kaldırırsanız, cihazların kaydı geri alınmaz, ancak hiçbir yeni cihaz kayda alınmaz.

### <a name="try-it-out"></a>Deneyin!

1. [İstemci ayarlarını yapılandırma](../clients/deploy/configure-client-settings.md)bölümündeki bilgileri kullanarak aşağıdaki istemci ayarlarını yapılandırın (Cloud Services) bölümünde bulunur.
   - **Azure Active Directory ile yeni Windows 10 etki alanına katılmış cihazları otomatik olarak kaydet** – **Evet** (varsayılan) veya **Hayır**olarak ayarlayın.
   - **İstemcilerin bir bulut yönetimi ağ geçidi kullanmasını etkinleştirin** – **Evet** (varsayılan) veya **Hayır**olarak ayarlayın.
2. İstemci ayarlarını gerekli cihaz koleksiyonuna dağıtın.

Cihazın Azure AD 'ye katıldığını onaylamak için, bir komut istemi penceresinde **/statusdsregcmd.exe** komutunu çalıştırın. Cihazın Azure AD 'ye katılmış olması durumunda, sonuçlarda **Azureadkatılmış** alanı **Evet** olarak gösterilir.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Configuration Manager konsolundan PowerShell betikleri oluşturun ve çalıştırın
<!-- 1236459 -->

Configuration Manager, paketleri ve programları kullanarak istemci cihazlarına komut dosyaları dağıtabilirsiniz. Bu teknik önizlemede, aşağıdaki eylemleri gerçekleştirmenizi sağlayan yeni işlevler ekledik:

- PowerShell betiklerini Configuration Manager içeri aktar
- Configuration Manager konsolundan betikleri düzenleme (yalnızca imzasız betikler için)
- Güvenliği artırmak için betikleri onaylanmış veya reddedildi olarak işaretle
- Windows istemci bilgisayarlarının ve şirket içi yönetilen Windows bilgisayarlarının koleksiyonlarında betikleri çalıştırın. Betikleri dağıtmazsınız, bunun yerine istemci cihazlarda neredeyse gerçek zamanlı olarak çalıştırılır.
- Configuration Manager konsolundaki komut dosyası tarafından döndürülen sonuçları inceleyin.


### <a name="prerequisites"></a>Ön koşullar

Betikleri kullanmak için uygun Configuration Manager güvenlik rolünün bir üyesi olmanız gerekir.

- **Betikleri içeri ve dışarı yazmak için** -hesabınız **tam yönetici** güvenlik rolünde **SMS betikleri** için **oluşturma** izinlerine sahip olmalıdır.
- **Betikleri onaylamak veya reddetmek için** -hesabınız **tam yönetici** güvenlik rolündeki **SMS betikleri** için izinleri **onaylama** olmalıdır.
- **Betikleri çalıştırmak için** -hesabınızın, **Uyumluluk Ayarları Yöneticisi** güvenlik rolündeki **koleksiyonlar** için **komut dosyası çalıştırma** izinlerine sahip olması gerekir.

Configuration Manager Güvenlik rolleri hakkında daha fazla bilgi için bkz. [rol tabanlı yönetimin temelleri](../understand/fundamentals-of-role-based-administration.md).

Varsayılan olarak, kullanıcılar yazdığı bir betiği onaylayamaz. Betikler güçlü, çok yönlü ve birçok cihaza dağıtılabildiği için, bir betiği yazar ve betiği onaylayan kişi arasında rolleri ayırma özelliği sunan yeni bir kavram sunuyoruz. Bu, daha fazla bakış olmadan bir betiği çalıştırmaya karşı ek güvenlik düzeyi sağlar. Özellikle de teknik önizleme sürümü sırasında test kolaylığı için bu ikincil onayı kapatabilirsiniz.

Kullanıcıların kendi komut dosyalarını onaylamasını sağlamak için:

1. Configuration Manager konsolunda, **Yönetim**’e tıklayın.
2. **Yönetim** çalışma alanında, **Site Yapılandırması**'nı genişletin ve **Siteler**'e tıklayın.
3. Site listesinde, sitenizi seçin ve ardından **giriş** sekmesinde, **siteler** grubunda, **Hiyerarşi ayarları**' na tıklayın.
4. **Hiyerarşi ayarları özellikleri** Iletişim kutusunun **genel** sekmesinde, **betik yazarlarının kendi betiklerini onaylamasını izin verme**onay kutusunu temizleyin.


### <a name="try-it-out"></a>Deneyin!

#### <a name="import-and-edit-a-script"></a>Betiği içeri ve dışarı aktarma

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.
2. **Yazılım kitaplığı** çalışma alanında **betikler**' e tıklayın.
3. **Giriş** sekmesinde, **Oluştur** grubunda, **komut dosyası oluştur**' a tıklayın.
4. **Betik oluşturma** sihirbazının **komut dosyası** sayfasında, aşağıdakileri yapılandırın:
   - **Betik adı** -betik için bir ad girin. Aynı ada sahip birden çok komut dosyası oluşturabilseniz de, bu, Configuration Manager konsolunda ihtiyacınız olan betiği bulmanızı zorlaştırır.
   - **Betik dili** -Şu anda yalnızca **PowerShell** betikleri desteklenir.
   - **Içeri aktarma** -bir PowerShell betiğini konsoluna aktarın. Betik, **betik** alanında görüntülenir.
   - **Temizle** - **komut dosyası** alanından geçerli betiği kaldırır.
   - **Betik** -Şu anda alınmış olan betiği görüntüler. Bu alandaki betiği gereken şekilde düzenleyebilirsiniz.
5. Sihirbazı tamamlayın. Yeni komut dosyası, **onay bekleniyor**durumuyla birlikte **betik** listesinde görüntülenir. Bu betiği istemci cihazlarda çalıştırmadan önce, bunu onaylamanız gerekir.


#### <a name="approve-or-deny-a-script"></a>Betiği onaylama veya reddetme



Bir betiği çalıştırmadan önce, onaylanmış olmalıdır. Bir betiği onaylamak için:

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.
2. **Yazılım kitaplığı** çalışma alanında **betikler**' e tıklayın.
3. **Betik** listesinde, onaylamak veya reddetmek istediğiniz betiği seçin ve ardından **giriş** sekmesinde, **komut dosyası** grubunda, **onayla/reddet**' e tıklayın.
4. **Betiği onayla veya Reddet** iletişim kutusunda betiği **onaylayın**veya **reddedin** ve isteğe bağlı olarak kararınız hakkında bir yorum girin. Bir komut dosyasını reddederseniz, istemci cihazlarda çalıştırılamaz.
5. Sihirbazı tamamlayın. **Komut dosyası** listesinde, yaptığınız eyleme göre **onay durumu** sütununun değiştirilmesini görürsünüz.

#### <a name="run-a-script"></a>Betik çalıştırma

Bir komut dosyası onaylandığında, seçtiğiniz bir koleksiyon için çalıştırılabilir.

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.
2. **Varlıklar ve Uyum** çalışma alanında, **Aygıt Koleksiyonları**'nı tıklatın.
3. **Cihaz Koleksiyonları** listesinde, komut dosyasını çalıştırmak istediğiniz cihaz koleksiyonuna tıklayın.
3. **Giriş** sekmesinde, **Tüm sistemler** grubunda **Betiği Çalıştır**' ı tıklatın.
4. **Betiği Çalıştır** sihirbazının **komut dosyası** sayfasında listeden bir komut dosyası seçin. Yalnızca onaylanan betikler gösterilir. **İleri**' ye tıklayın ve Sihirbazı doldurun.

#### <a name="monitor-a-script"></a>Betiği izleme

İstemci cihazlarına bir komut dosyası çalıştırdıktan sonra, işlemin başarısını izlemek için bu yordamı kullanın.

1. Configuration Manager konsolunda, **izleme**' yi tıklatın.
2. **İzleme** çalışma alanında **betik sonuçları**' na tıklayın.
3. **Betik sonuçları** listesinde, istemci cihazlarında çalıştırdığınız her komut dosyası için sonuçları görüntüleyebilirsiniz. Bir komut dosyası çıkış kodu **0**, genellikle betiğin başarıyla çalıştığını gösterir.

## <a name="pxe-network-boot-support-for-ipv6"></a>IPv6 için PXE ağ önyükleme desteği
<!-- 1269793 -->
Artık, bir görev dizisi işletim sistemi dağıtımını başlatmak üzere IPv6 için PXE ağ önyükleme desteğini etkinleştirebilirsiniz. Bu ayarı kullandığınızda, PXE 'yi destekleyen dağıtım noktaları hem IPv4 hem de IPv6 'Yı destekleyecektir. Bu seçenek WDS gerektirmez ve varsa WDS 'yi durdurur.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>IPv6 için PXE önyükleme desteğini etkinleştirmek için
PXE için IPv6 desteği seçeneğini etkinleştirmek için aşağıdaki yordamı kullanın.

1. Configuration Manager konsolunda, **Yönetim**  >  **genel bakış**  >  **dağıtım noktaları**' na gidin ve PXE 'yi destekleyen dağıtım noktaları için **Özellikler** ' e tıklayın.
2. **PXE sekmesinde,** PXE için IPv6 desteğini etkinleştirmek üzere **IPv6 desteği** ' ni seçin.

## <a name="manage-microsoft-surface-driver-updates"></a>Microsoft Surface sürücü güncelleştirmelerini yönetme
<!-- 1098490 -->
Artık, Microsoft Surface sürücü güncelleştirmelerini yönetmek için Configuration Manager kullanabilirsiniz.

### <a name="prerequisites"></a>Ön koşullar
Tüm yazılım güncelleştirme noktalarında Windows Server 2016 çalışmalıdır.

### <a name="try-it-out"></a>Deneyin!
Aşağıdaki görevleri tamamlamayı deneyin ve nasıl çalıştığını bize bildirmek için şeridin **giriş** sekmesinden bize **geri bildirim** gönderin:
1. Microsoft Surface sürücüleri için eşitlemeyi etkinleştirin. Surface sürücülerini etkinleştirmek için sınıflandırmaların [ve ürünlerin yapılandırma](../../sum/get-started/configure-classifications-and-products.md) bölümündeki yordamı kullanın ve **sınıflandırmalar** sekmesine **Microsoft Surface sürücülerini ve bellenim güncelleştirmelerini dahil et** ' i seçin.
2. [Microsoft Surface sürücülerini eşitler](../../sum/get-started/synchronize-software-updates.md).
3. [Eşitlenmiş Microsoft Surface sürücüleri dağıtma](../../sum/deploy-use/deploy-software-updates.md)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Iş erteleme ilkeleri için Windows Update yapılandırma
<!-- 1290890 -->
Artık Windows 10 için Windows 10 özellik güncelleştirmeleri veya kalite güncelleştirmeleri için erteleme ilkelerini, doğrudan Windows Update Iş tarafından yönetilen Windows 10 cihazları için yapılandırabilirsiniz. **Yazılım kitaplığı**Windows 10 bakımı altındaki **iş için yeni Windows Update ilke** düğümünde erteleme ilkelerini yönetebilirsiniz  >  **Windows 10 Servicing**.

### <a name="prerequisites"></a>Ön koşullar
Iş için Windows Update tarafından yönetilen Windows 10 cihazlarının Internet bağlantısı olmalıdır.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Iş erteleme ilkesi için Windows Update oluşturmak için
1. **Yazılım kitaplığı**'nda  >  iş ilkeleri için**Windows 10 Bakımı**  >  **Windows Update**
2. Iş için Windows Update oluşturma Sihirbazı 'Nı açmak için **Oluştur** grubunun **giriş** sekmesinde **iş ilkesi Windows Update oluştur** ' u seçin.
3. **Genel** sayfasında, ilke için bir ad ve açıklama girin.
4. Erteleme Ilkeleri sayfasında, özellik güncelleştirmelerini **ertelemeyi** veya duraklatmayı yapılandırın.    
    Özellik Güncelleştirmeleri genellikle Windows’un yeni özellikleridir. **Dal hazırlık düzeyi** ayarını yapılandırdıktan sonra, özellik güncelleştirmelerini Microsoft 'un kullanılabilirliğine göre ertelemek için ne kadar süre ertelemenizi istediğinizi tanımlayabilirsiniz.
    - **Dal hazırlık düzeyi**: cihazın Windows güncelleştirmelerini alacağı dalı ayarlayın (Güncel Dalı veya iş için güncel dalı).
    - **Erteleme süresi (gün)**: Özellik güncelleştirmelerinin ertelenmesi gereken gün sayısını belirtin. Bu Özellik Güncelleştirmelerini almayı yayımlanmalarından sonra 180 güne kadar erteleyebilirsiniz.
    - **Güncelleştirme özellikleri güncelleştirmeleri başlatılıyor**: cihazların, güncelleştirmeleri duraklatmadan 60 güne kadar bir süre Için özellik güncelleştirmelerini almasını isteyip istemediğinizi seçin. En fazla gün sayısı kadar bir süre geçtikten sonra duraklatma işlevi otomatik olarak sona erer ve cihaz, kullanılabilecek güncelleştirmeleri bulmak için Windows Güncelleştirmelerini tarar. Bu taramanın ardından güncelleştirmeleri yeniden duraklatabilirsiniz. Onay kutusunu temizleyerek Özellik güncelleştirmelerinin duraklamasını geri alabilirsiniz.   
5. Kalite güncelleştirmelerini ertelemenizi veya duraklatmayı seçin.     
    Kalite Güncelleştirmeleri, genellikle mevcut Windows işlevselliğine yönelik düzeltme ve iyileştirmelerdir. Normal olarak her ayın ilk salı günü yayımlanırlar ancak Microsoft tarafından herhangi bir zamanda yayımlanmaları mümkündür. Kullanıma sunulduktan sonra Kalite Güncelleştirmelerinin alınmasını ertelemek isteyip istemediğinizi ve ne kadar süreyle erteleyeceğinizi tanımlayabilirsiniz.
    - **Erteleme süresi (gün)**: Özellik güncelleştirmelerinin ertelenmesi gereken gün sayısını belirtin. Bu Özellik Güncelleştirmelerini almayı yayımlanmalarından sonra 180 güne kadar erteleyebilirsiniz.
    - **Kalite güncelleştirmelerini duraklatma başlangıcı**: cihazların, güncelleştirmeleri duraklatmadan 35 güne kadar bir dönem Için kalite güncelleştirmeleri almasını isteyip istemediğinizi seçin. En fazla gün sayısı kadar bir süre geçtikten sonra duraklatma işlevi otomatik olarak sona erer ve cihaz, kullanılabilecek güncelleştirmeleri bulmak için Windows Güncelleştirmelerini tarar. Bu taramanın ardından güncelleştirmeleri yeniden duraklatabilirsiniz. Onay kutusunu temizleyerek kalite güncelleştirmelerinin duraklamasını geri alabilirsiniz.
6. Microsoft Update için geçerli olan ve Windows güncelleştirmelerinin yanı sıra **diğer Microsoft ürünlerinden güncelleştirme yüklemeyi** seçin.
7. Sürücüleri Windows güncelleştirmelerinden otomatik olarak güncelleştirmek için **Windows Update sürücüleri dahil et** ' i seçin. Bu ayarı temizlerseniz, sürücü güncelleştirmeleri Windows Updates 'ten indirilmez.
8. Yeni erteleme ilkesini oluşturmak için Sihirbazı doldurun.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Windows Update Iş erteleme ilkesini dağıtmak için
1. **Yazılım kitaplığı**'nda  >  iş ilkeleri için**Windows 10 Bakımı**  >  **Windows Update**
2. **Giriş** sekmesinde, **dağıtım** grubunda, **Windows Update iş ilkesi için dağıt**' ı seçin.
3. Aşağıdaki ayarları yapılandırın:
    - **Dağıtılacak yapılandırma ilkesi**: dağıtmak istediğiniz iş ilkesi Windows Update seçin.
    - **Koleksiyon**: ilkeyi dağıtmak istediğiniz koleksiyonu seçmek Için, **Araştır** ' a tıklayın.
    - **Desteklendiğinde uyumsuz kuralları düzelt**: WINDOWS YÖNETIM araçları (WMI), kayıt defteri, komut dosyaları ve Configuration Manager tarafından kaydedilen mobil cihazların tüm ayarları için uyumsuz olan tüm kuralları otomatik olarak düzeltmek için seçin.
    - **Bakım süresi dışında düzeltmeye Izin ver**: ilkeyi dağıtmakta olduğunuz koleksiyon için bir bakım penceresi yapılandırıldıysa, uyumluluk ayarlarının bakım penceresi dışındaki değeri düzeltmesine izin vermek için bu seçeneği etkinleştirin. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../clients/manage/collections/use-maintenance-windows.md).
    - **Uyarı oluştur**: yapılandırma temeli uyumluluğu, belirtilen tarih ve saate göre belirtilen yüzdeden küçük olduğunda oluşturulan bir uyarı yapılandırır. System Center Operations Manager'a bir uyarının ne zaman gönderilmesini istediğinizi de belirtebilirsiniz.
    - **Rastgele gecikme (saat)**: ağ aygıtı kayıt hizmeti 'nde aşırı işleme engel olmak için bir gecikme penceresi belirtir. Varsayılan değer 64 saattir.
    - **Zamanlama**: dağıtılan profilin istemci bilgisayarlarda değerlendirildiği uyumluluk değerlendirmesi zamanlamasını belirtin. Bu zamanlama basit veya özel bir zamanlama olabilir. Kullanıcı oturum açtığında, profil istemci bilgisayarlar tarafından değerlendirilir.
4.  Profili dağıtmak için Sihirbazı doldurun.



## <a name="support-for-entrust-certification-authorities"></a>Güvenilen sertifika yetkilileri için destek
<!-- 1350740 -->
Configuration Manager artık güvenilen sertifika yetkililerini destekliyor; Bu, Microsoft Intune kayıtlı cihazlara PFX Sertifika teslimini sağlar.

Configuration Manager ' de bir sertifika kayıt noktası rolü eklerken, sertifika yetkilisi olarak Entrust 'ı yapılandırabilirsiniz. PFX sertifikaları veren yeni bir sertifika profili eklerken, bir Microsoft veya Entrust sertifika yetkilisi seçebilirsiniz.

**Bilinen sorun**: 1706 Technical Preview sürümünde, Microsoft sertifika YETKILILERI için PFX sertifikaları verilmez. Bu, içeri aktarılan PFX sertifikalarını veya SCEP profillerini etkilemez.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>İOS VPN profilleri için Cisco (IPSec) desteği
<!-- 1321367 -->

Bağlantı türü olarak Cisco (IPSec) ile bir iOS VPN profili oluşturabilirsiniz. Daha fazla bilgi için bkz. [VPN profilleri oluşturma](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile).


## <a name="new-windows-configuration-item-settings"></a>Yeni Windows yapılandırma öğesi ayarları
<!-- 1354715 -->

Bu sürümde, aşağıdaki yeni ayarları Windows yapılandırma öğelerinde kullanabileceğiniz şekilde ekledik:

### <a name="password"></a>Parola

- **Cihaz şifreleme**

### <a name="device"></a>Cihaz

- **Bölge ayarlarının değiştirilmesi (yalnızca masaüstü)**
- **Güç ve uyku ayarlarının değiştirilmesi**
- **Dil ayarları değişikliği**
- **Sistem saati değişikliği**
- **Cihaz adı değişikliği**

### <a name="store"></a>Depolama

- **Mağazadan uygulamaları otomatik güncelleştir**
- **Yalnızca özel mağazayı kullan**
- **Mağaza kaynaklı uygulama başlatma**

### <a name="microsoft-edge"></a>Microsoft Edge

- **About: Flags sayfasına erişimi engelle**
- **SmartScreen istemi geçersiz kılma**
- **Dosyalar için SmartScreen istemi geçersiz kılma**
- **WebRTC localhost IP adresi**
- **Varsayılan arama altyapısı**
- **OpenSearch XML URL 'SI**
- **Homepages (yalnızca masaüstü)**

Uyumluluk ayarları hakkında daha fazla bilgi için bkz. [Cihaz uyumluluğunu doğrulayın](../../compliance/understand/ensure-device-compliance.md).


## <a name="new-device-compliance-policy-rules"></a>Yeni cihaz uyumluluk ilkesi kuralları

* **Gerekli parola türü**. Kullanıcının alfasayısal parola mı yoksa sayısal parola mı oluşturması gerektiğini belirtin. Alfasayısal parolalar için parolanın sahip olması gereken karakter kümesi sayısı alt sınırını da belirtirsiniz. Dört karakter kümesi şunlardır: küçük harf, büyük harfler, semboller ve sayılar.

  **Şu platformlarda desteklenir:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
<br></br>
* **CIHAZDA USB hata ayıklamayı engelleyin**. Bu ayarları, Android for Work cihazlarında USB hata ayıklama zaten devre dışı bırakıldığı için yapılandırmanız gerekmez.

  **Şu platformlarda desteklenir:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Bilinmeyen kaynaklardan gelen uygulamaları engelleyin**. Cihazların bilinmeyen kaynaklardan uygulama yüklenmesini engellemesini gerektir. Android for Work cihazları her zaman bilinmeyen kaynaklardan yüklemeyi kısıtlayabileceğinden bu ayarı yapılandırmanız gerekmez.

  **Şu platformlarda desteklenir:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Uygulamalarda tehdit taraması gerektir**. Bu ayar, cihazda uygulamaları doğrula özelliğinin etkinleştirildiğini belirtir.

  **Şu platformlarda desteklenir:**
  * Android 4,2 ila 4,4
  * Samsung KNOX Standard 4.0+


## <a name="new-mobile-application-management-policy-settings"></a>Yeni mobil uygulama yönetimi ilke ayarları
Bu sürümden itibaren, üç yeni mobil uygulama yönetimi (MAM) ilkesi ayarı kullanabilirsiniz:

- **Ekran yakalamayı engelle (yalnızca Android cihazlar):** Bu uygulama kullanılırken cihazın ekran yakalama yeteneklerinin engellendiğini belirtir.

- **Kişi eşitlemesini devre dışı bırak:** Uygulamanın cihazdaki yerel Kişiler uygulamasına veri kaydetmesini önler.

- **Yazdırmayı devre dışı bırak:** Uygulamanın iş veya okul verilerini yazdırmasını önler.

## <a name="android-and-ios-enrollment-restrictions"></a>Android ve iOS kayıt kısıtlamaları
<!-- 1290826 -->
Bu sürümden itibaren Yöneticiler artık kullanıcıların, karma ortamlarında kişisel Android veya iOS cihazlarını kaydedemeyecek olduğunu belirtebilir. Bu, kayıtlı cihazları önceden tanımlanmış, şirkete ait cihazlara veya yalnızca Aygıt Kayıt Programı kaydedilmiş iOS cihazlarına sınırlamanıza olanak tanır.

### <a name="try-it-out"></a>Deneyin
1. **Yönetim** çalışma alanındaki Configuration Manager konsolunda **Bulut Hizmetleri** > **Microsoft Intune Aboneliği**'ne gidin.
2. **Abonelik** grubundaki **giriş** sekmesinde **platformları Yapılandır** ' ı seçin ve ardından **Android** veya **iOS**' u seçin.
3. **Kişisel cihazları engelle**' yi seçin.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Kopyala-Yapıştır için Android for Work uygulama yönetimi ilkesi
**İş ve kişisel profil arasında veri paylaşımına Izin ver**için Android for Work yapılandırma öğelerinin ayar açıklamalarını güncelleştirdik.

|1706 Technical Preview öncesi | Yeni seçenek adı | Davranış|
|-|-|-|
|Sınırlar arasında tüm paylaşımları engelle| Varsayılan paylaşım kısıtlamaları| Kişisel çalışma: varsayılan (tüm sürümlerde engellenmesi bekleniyor) <br>Kişisel-iş: varsayılan (6. x + üzerinde izin verilir, 5. x üzerinde engellenmiştir)|
|Kısıtlama yok| Kişisel profildeki uygulamalar, iş profilinden gelen paylaşım isteklerini işleyebilir| Kişisel çalışma: Izin verildi  <br>Kişisel-iş: Izin verildi|
|İş profilindeki uygulamalar, kişisel profilden gelen paylaşım isteklerini işleyebilir |İş profilindeki uygulamalar, kişisel profilden gelen paylaşım isteklerini işleyebilir |Kişisel çalışma: varsayılan<br>Kişisel-iş: Izin verildi<br>(Yalnızca kişisel-iş 'nin engellediği 5. x üzerinde faydalıdır)|

Bu seçeneklerden hiçbiri kopyalama Yapıştır davranışını doğrudan engellemez. Hizmete ve Şirket Portalı 1704 uygulamasına kopyalama-yapıştırmayı engelleyecek şekilde yapılandırılabilen bir özel ayar ekledik. Bu, özel URI aracılığıyla ayarlanabilir.

- OMA-URI:./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Değer türü: Boolean

Disallowcrossprofilecopycopy değeri true olarak ayarlandığında, Android for Work kişisel ve iş profilleri arasında kopyalama-yapıştırma davranışı engellenir.

### <a name="try-it-out"></a>Deneyin
1. Configuration Manager konsolunda **varlıklar ve uyum**  >  **genel bakış**  >  **Uyumluluk ayarları**  >  **yapılandırma öğeleri**' ni seçin.
2. Yeni bir yapılandırma öğesi oluşturmak için **Oluştur** ' u seçin ve **iş Için** **ad** ve Android ' i belirtin.
3. Yapılandırılacak cihaz ayarı grupları ' nda **Iş profili**' ni seçin ve **İleri**' yi seçin.
4. **İş ve kişisel profiller arasında veri paylaşımına Izin ver**için değeri seçin ve ardından Sihirbazı doldurun.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Koşullu erişim için uyumluluk ilkeleri değerlendirmesi Cihaz Sistem Durumu Kanıtlama
<!-- 1097546 -->
Bu sürümden itibaren, şirket kaynaklarına koşullu erişim için uyumluluk ilkesi kuralı olarak Cihaz Sistem Durumu Kanıtlama durumunu kullanabilirsiniz.

### <a name="try-it-out"></a>Deneyin
Uyumluluk ilkesi değerlendirmesinin bir parçası olarak bir Cihaz Sistem Durumu Kanıtlama kuralı seçin.
