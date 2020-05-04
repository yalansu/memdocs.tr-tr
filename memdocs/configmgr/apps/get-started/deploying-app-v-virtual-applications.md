---
title: App-V sanal uygulamalarını dağıtma
titleSuffix: Configuration Manager
description: Sanal uygulamaları oluştururken ve dağıtırken dikkate almanız gereken noktalara göz atın.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bea7c2ef5c3d77932fcd91ca8d4d2b8baa62edd2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710478"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Configuration Manager ile App-V sanal uygulamalarını dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sanal uygulamaları yönetmek için Configuration Manager kullandığınızda, aşağıdaki avantajları elde edersiniz:  

-   Tek bir yönetim altyapısı  

-   Koleksiyonlar ve Kullanıcı cihaz benzeşimi gibi ölçeklenebilirlik, dağıtım ve içerik dağıtım özellikleri  

-   Gelişmiş uygulama yönetimi özellikleri  

-   Sanal uygulamaları desteklemek için işletim sistemi dağıtımı, yazılım ve donanım envanteri, yazılım ölçümü ve varlık yönetim bilgileri  

Microsoft Application Virtualization (App-V) ile uygulama oluşturma ve sıralama hakkında daha fazla bilgi için bkz. TechNet kitaplığındaki [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx) .  

Bir uygulama oluşturmaya yönelik diğer Configuration Manager gereksinimleri ve yordamlarına ek olarak, sanal uygulama oluştururken ve dağıtırken aşağıdaki noktaları dikkate almanız gerekir:

-   Bilgisayarlara sanal uygulamaları dağıtmak için, Configuration Manager Client ve App-V Istemcisinin bilgisayarlarınızda yüklü olması gerekir. İstemci cihazlar arasında masaüstü ve taşınabilir bilgisayarlar ve Sanal Masaüstü Altyapısı (VDI) istemcileri yer alabilir. Configuration Manager ve App-V Istemcisi yazılımı, sanal uygulama paketlerini teslim etmek, bulmak ve başlatmak için birlikte çalışır. Configuration Manager istemcisi, sanal uygulama paketlerinin App-V Istemcisine teslim edilmesini yönetir. App-V İstemcisi, sanal uygulamayı istemcide çalıştırır.  

-   Sanal bir uygulamayı dağıtmak için, önce App-V Application Virtualization Sequencer'ı kullanarak sanal uygulamayı oluşturmanız gerekir. Sıralayıcı, uygulama için yükleme ve kurulum işlemini izler ve uygulamanın sanal ortamda çalıştırılması için gerekli bilgileri kaydeder. Ayrıca, tüm kullanıcılar için hangi dosya ve yapılandırmaların uygulanacağını ve kullanıcıların özelleştirebileceği konfigürasyonları ayarlamak için sıralayıcı 'yı kullanabilirsiniz.  

-   Bir uygulamayı sıraladığınızda, paketi Configuration Manager erişebileceği bir konuma kaydetmeniz gerekir. Ardından bu sanal uygulamayı içeren bir uygulama dağıtımı oluşturabilirsiniz.  

-   Configuration Manager, App-V 4,6 ' nin paylaşılan salt okuma önbelleği özelliğinin kullanımını desteklemez.  

-   Configuration Manager, App-V 5 ' teki paylaşılan Içerik depolama özelliğini destekler.  

-   Sanal uygulama için bir dağıtım türü oluşturduğunuzda Configuration Manager, uygulama bildirim dosyasının içeriğini kullanarak dağıtım türünü oluşturur. Bu, sanal uygulama hakkında bilgi içeren bir XML dosyasıdır. Ayrıca, Configuration Manager, sanal uygulama için desteklenen işletim sistemleri hakkında bilgi içeren App-V. osd dosyasının içeriğine göre dağıtım türü için gereksinimler oluşturur.  

-   Configuration Manager ' de sanal uygulamaları dağıtmak için, istemci bilgisayarlarda minimum App-V 4,6 SP1 veya istemcinin sonraki bir sürümü yüklü olmalıdır.  

-   Sanal uygulamaları başarıyla dağıtabilmeniz için önce App-V Istemcisini, Bilgi Bankası makalesi [2645225](https://support.microsoft.com/kb/2645225)' de açıklanan düzeltmeyle güncelleştirmeniz gerekir.  

-   App-V 5,0 ' de bağlantı gruplarını kullandığınızda, dağıtılmış sanal uygulamalarınız istemci bilgisayarlarda aynı dosya sistemini ve kayıt defterini paylaşabilir. Standart sanal uygulamalardan farklı olarak, bu uygulamalar birbiriyle veri paylaşabilir. Bu ek olarak, bağlantı grupları içerdikleri uygulamalar için kullanıcı ayarlarını korurlar. Configuration Manager içindeki App-V sanal ortamları, istemci bilgisayarlarda bağlantı grupları kurmak için kullanılır. Sanal ortamlar, uygulama yüklendiğinde veya sonraki istemciler yüklü uygulamalarını değerlendirdiğinde istemci bilgisayarlarda oluşturulur veya değiştirilir. Bu uygulamaları, birden fazla uygulama bir dosya sistemini veya kayıt defteri değerini değiştirmeye çalıştığında en yüksek önceliğe sahip uygulama öncelikli olarak biçimde öncelik sırasına koyabilirsiniz. Daha fazla bilgi için bkz. [App-V sanal ortamları oluşturma](../../apps/deploy-use/create-app-v-virtual-environments.md).  

##  <a name="supported-app-v-versions"></a>Desteklenen App-V sürümleri  
 Configuration Manager aşağıdaki App-V sürümlerini destekler:  

-   **App-v 4,6**: Configuration Manager sanal uygulamaları kullanmak için, Istemci bilgisayarlarda App-v 4,6 SP1, App-v 4,6 SP2 veya App-v 4,6 SP3 istemcisinin yüklü olması gerekir.  

     Sanal uygulamaları başarıyla dağıtabilmeniz için, App-V 4,6 SP1 istemcisini Ayrıca Bilgi Bankası makalesi [2645225](https://go.microsoft.com/fwlink/p/?LinkId=237322)' de açıklanan düzeltmeyle güncelleştirmeniz gerekir.  

-   **App-v 5, App-v 5,0 SP1, App-v 5,0 SP2, App-v 5,0 SP3 ve App-v 5,1**: App-v 5,0 SP2 Için [düzeltme paketi 5](https://support.microsoft.com/en-us/kb/2963211) ' i yüklemeli veya App-v 5,0 SP3 kullanmanız gerekir.  
-   **App-V 5,2**: Bu, Windows 10 eğitimi (1607 ve üzeri), Windows 10 Enterprise (1607 ve üzeri) ve windows Server 2016 içinde yerleşiktir.

Windows 10 ' da App-V hakkında daha fazla bilgi için aşağıdaki konulara bakın:

- [App-V ' d a yenilikler](https://technet.microsoft.com/itpro/windows/manage/appv-about-appv)
- [Windows 10 için App-V ile çalışmaya başlama](https://technet.microsoft.com/itpro/windows/manage/appv-getting-started)
- [Mevcut bir yüklemeden Windows 10 için App-V ' d e yükseltme](https://technet.microsoft.com/itpro/windows/manage/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>App-V sanal uygulamalarını yönetme adımları  
 App-V sanal uygulamalarını yönetmek için aşağıdaki adımları izleyin:  

1.   **Sıra**: sıralama, App-V Sıralayıcısı 'nı kullanarak bir uygulamayı sanal bir uygulamaya dönüştürme işlemidir.

2.   **Oluştur**: sıralı uygulamayı daha sonra bir uygulamaya ekleyebileceğiniz Configuration Manager dağıtım türüne aktarmak Için dağıtım türü oluşturma Sihirbazı ' nı kullanın. Ayrıca, birden fazla sanal uygulamanın ayarları paylaşmasına olanak sağlayan sanal ortamlar da oluşturabilirsiniz.

3.   **Dağıtma**: dağıtım, App-V uygulamalarını Configuration Manager dağıtım noktalarında kullanılabilir hale getirme işlemidir.

4.   **Dağıtma**: dağıtım, uygulamayı istemci bilgisayarlarda kullanılabilir hale getirme işlemidir. Bu, App-V tam altyapısında yayımlama ve akış olarak adlandırılır.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Configuration Manager sanal uygulama teslim yöntemleri  
Configuration Manager, istemcilere sanal uygulama teslimi için iki yöntemi destekler: akış teslimi ve yerel teslimat (indir ve Yürüt).

Hangi teslim yöntemini kullanacağınızı seçerken, akış teslimi için azaltılmış disk alanı gereksinimini, yerel teslimdeki App-V uygulamalarının garantili kullanılabilirliğine göre karşılaştırın. Yerel teslimde kullanıcıların uygulamayı her zaman herhangi bir konumdan kullanabileceği göz önünde bulundurulduğunda, daha fazla istemci disk alanı gerektirmesine bu teslim yöntemi tercih edilebilir.  

###  <a name="streaming-delivery"></a>Akışla teslim
App-V Istemcisini yönetmek için Configuration Manager kullandığınızda, sanal uygulamaların bir dağıtım noktasından HTTP veya HTTPS aracılığıyla akışını destekler. HTTP veya HTTPS aracılığıyla akış varsayılan olarak etkindir ve dağıtım noktası özellikleri iletişim kutusunda ayarlanır. İstemci bilgisayarlara bir sanal uygulama dağıtırken ve bir Kullanıcı sanal uygulamayı çalıştırdığında, Configuration Manager istemci bir yönetim noktasıyla iletişim kurarak hangi dağıtım noktasının kullanılacağını belirlemektir. Ardından, uygulama dağıtım noktasından akışla kaydedilir.  

Akış tesliminin sizin için en iyi teslim yöntemi olup olmadığına karar vermenize yardımcı olması için bu tablodaki bilgileri kullanın:

|Yararları|Dezavantajlar|  
|----------------|-------------------|  
|Bu yöntemde, dağıtım noktalarından paket içeriğinin akışını gerçekleştirmek için standart ağ protokolleri kullanılır.<br /><br /> Sanal uygulamalara ilişkin program kısayolları, dağıtım noktasına yönelik bir bağlantı başlatır; dolayısıyla sanal uygulama teslimi isteğe bağlı olur.<br /><br /> Bu yöntem, dağıtım noktalarıyla yüksek bant genişlikli bağlantıları olan istemcilerde iyi işler.<br /><br /> İstemciler, geçerli sürümün eski sürümün yerini aldığını bildiren ilkeyi aldıklarında kuruluş genelinde dağıtılan güncelleştirilmiş sanal uygulamalar kullanılabilir olur ve istemciler yalnızca eski sürümden farklılıkları indirirler.<br /><br /> Kullanıcıların yetkisiz uygulamalara veya paketlere erişimini önlemek için izin erişimleri dağıtım noktasında tanımlanır.|Kullanıcı uygulamayı ilk defa çalıştırana kadar sanal uygulamaların akışı gerçekleştirilmez. Bu senaryoda, kullanıcı sanal uygulamalar için program kısayollarını alabilir ve ardından sanal uygulamaları ilk defa çalıştırmadan önce ağ bağlantısını kesebilir. İstemci çevrimdışıyken Kullanıcı sanal uygulamayı çalıştırmaya çalışırsa, Kullanıcı bir hata görür ve sanallaştırılmış uygulamayı çalıştıramıyor çünkü Configuration Manager bir dağıtım noktası, uygulamanın akışını sağlamak için kullanılabilir değildir. Kullanıcı ağa yeniden bağlanıp uygulamayı çalıştırana kadar uygulama kullanılamaz.<br /><br /> Bundan kaçınmak amacıyla, istemcilere sanal uygulama teslimi için yerel teslim yöntemini kullanabilirsiniz veya akışla teslim için Internet tabanlı istemci yönetimini etkinleştirebilirsiniz.|  

###  <a name="local-delivery-download-and-execute"></a>Yerel teslim (indir ve yürüt)  
Bu yaklaşım, diğer uygulama biçimlerinin Configuration Manager ile nasıl teslim edildiğini yakından taklit ettiğinden Configuration Manager kullanılırken indirme ve yürütme yaygın yaklaşımda bulunur. Yerel teslim yöntemini kullandığınızda, Configuration Manager istemcisi önce sanal uygulama paketinin tamamını Configuration Manager istemci önbelleğine indirir. Configuration Manager ardından App-V Istemcisine uygulamayı Configuration Manager önbelleğinden App-V önbelleğine akışı için yönlendirir. Bir sanal uygulamayı istemci bilgisayarlara dağıtırsanız ve içeriği App-V önbelleğinde yoksa, App-V Istemcisi Configuration Manager istemci önbelleğinden uygulama içeriğini App-V önbelleğine akıp uygulamayı çalıştırır. Uygulama başarıyla çalıştıktan sonra, Configuration Manager istemcisini bir sonraki silme döngüsündeki paketin eski sürümlerini silecek şekilde veya Configuration Manager istemci önbelleğinde kalıcı hale getirmek için ayarlayabilirsiniz. Kalıcı içerik yerel olarak, BranchCache ve PeerCache gibi paket içeriği teslim iyileştirme yöntemlerinden yararlanabilir.

Yerel teslimin sizin için en iyi teslim yöntemi olup olmadığına karar vermenize yardımcı olması için bu tablodaki bilgileri kullanın:   

|Yararları|Dezavantajlar|  
|----------------|-------------------|  
|Arka Plan Akıllı Aktarım Hizmeti (BITS) kullanılarak paketi indirmek için standart dağıtım noktası işlevselliği kullanılır.<br /><br /> Sanal uygulama paketi içerikleri istemciye yerel olarak dağıtılır. Bu, kullanıcıların bilgisayarlarını ağa bağlı olmadığında çalıştırabileceği anlamına gelir.<br /><br /> Bu yöntem, yavaş ve güvenilmeyen ağ bağlantıları için ve nadiren ağa bağlanan bilgisayarlar için uygundur.<br /><br /> Configuration Manager, yalnızca sanal uygulama paketi içeriği güncelleştirilirken değiştirilen dosyalardaki baytları istemcilere göndermek için uzaktan değişiklikleri sıkıştırma (RDC) kullanır. Configuration Manager istemcisi, paketin geçerli sürümüne ve istemciye gönderilen değişikliklere dayalı olarak bir sanal uygulama paketinin yeni bir sürümünü oluşturmak için RDC 'yi kullanır.<br /><br /> Bu yöntem, mobil kullanıcılar veya bağlantısı kesilmiş kullanıcılar için uygulama dayanıklılığı sağlar. Yöneticiler, sanal uygulama bir Install eylemiyle dağıtılmışsa, dağıtım sonrasında paketi Configuration Manager önbellekte kalıcı hale getirmek için seçim yapabilir. Configuration Manager istemci önbelleğindeki paket, App-V Istemcisinin paketini önbelleğine çekmek için yerel, güvenilir bir akış kaynağı işlevi görür.|Sanal uygulama Configuration Manager önbelleğinde kalıcı olduğunda, istemcide sanal uygulama paketinin boyutunun iki katına eşit olan disk alanı gerekir.|  

###  <a name="deployment-from-an-image"></a>Görüntüden dağıtım

Ayrıca, sanal uygulamaları bir bilgisayara önceden yükleyebilir ve ardından diğer bilgisayarlara dağıtım için o bilgisayarın görüntüsünü oluşturabilirsiniz. Ancak, sanal uygulama paketi farklı bir sitede oluşturulduysa, uygulama güncelleştirmelerini indirmek için ikili değişim çoğaltması kullanılmaz. Kullanıcı oturum açtıktan sonra uygulamaların indirilmesi yerine uygulamaların hemen kullanılabilir olmasını istiyorsanız bu seçenek sanal masaüstü altyapısında faydalı olabilir.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>App-V altyapısından Configuration Manager ve App-V altyapısına geçiş yapma  
Mevcut bir App-V altyapısından Configuration Manager ile sanal uygulama yönetimine geçiş planlaması yapmanıza yardımcı olması için aşağıdaki tabloyu kullanın.  

|Adım|Daha fazla bilgi|  
|----------|----------------------|  
|Configuration Manager altyapınıza geçirmek istediğiniz uygulamaları seçmek için mevcut sanal uygulamalarınızı inceleyin.|Ek bilgi yok.|  
|Sanal uygulamaların dağıtılacağı kullanıcıları ve cihazları değerlendirin.|Sanal uygulamaları dağıtmak istediğiniz kullanıcıları ve cihazları gruplamak için Configuration Manager koleksiyonları oluşturun. Bkz. [koleksiyonlara giriş](../../core/clients/manage/collections/introduction-to-collections.md).|  
|App-V 5 bağlantı gruplarını Configuration Manager sanal ortamlara geçirin.|Bu konudaki [App-V 5 bağlantı gruplarını Configuration Manager sanal ortamlara geçirme](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments) bölümüne bakın.|  
|Sanal uygulamalarınızın herhangi birinin Configuration Manager altyapınızda tam uygulama olarak mevcut olup olmadığını araştırın.|Daha kolay yönetim için, sanal uygulamayı var olan tam uygulamaya yeni bir dağıtım türü olarak ekleyebilirsiniz. Bkz. [uygulama oluşturma](../../apps/deploy-use/create-applications.md).|  
|Var olan App-V uygulamalarınızın yerini alacak uygulamaları oluşturun.|Bkz. [uygulama yönetimine giriş](../understand/introduction-to-application-management.md) ve uygulama [oluşturma](../../apps/deploy-use/create-applications.md).|  
|Configuration Manager, bir sanal uygulamanın ilk dağıtımından sonra bir istemcideki sanal uygulamaları yönetmeye başlar. Bundan sonra, Configuration Manager bilgisayardaki tüm App-V uygulamalarını yönetmesi gerekir.|Ek bilgi yok.|  
|Uygulamaların yerel teslimine olanak sağlamak için içeriği uygun dağıtım noktalarına dağıtın.|Bkz. [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Uygulamayı Configuration Manager istemcilere dağıtın.<br /><br /> App-V uygulaması Sıralayıcı 'nın bildirim XML dosyası oluşturmayan daha eski bir sürümüyle oluşturulduysa, dosyayı oluşturmak için onu açabilir ve Sıralayıcı 'nın daha yeni bir sürümüne kaydedebilirsiniz. Configuration Manager ile sanal uygulamaları dağıtmak için bu dosya gereklidir.<br /><br /> App-V, Sıralayıcı 'nın SoftGrid 4,1 SP1 veya 4,2 sürümleriyle oluşturulan sanal uygulama paketlerini destekler.<br /><br /> Uygulamalar daha önce yerel olarak yüklenmişse, uygulamanın sanal sürümünü dağıtmadan önce bunları kaldırmanız gerekir.|Bkz. [uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md).|  
|Configuration Manager artık sanal uygulamaları içeren paketlerin ve programların kullanılmasını desteklememektedir. Configuration Manager 2007 ' den Configuration Manager güncel dala geçirdiğinizde Configuration Manager bu paketleri uygulamalara dönüştürür.<br /><br /> Configuration Manager 2007 reklamları aşağıdaki dağıtım türlerine dönüştürülür:<br /><br /> -Uygulama-V paketleri tanıtım olmadan geçiriliyor: varsayılan dağıtım türü ayarlarını kullanan bir dağıtım türü.<br /><br /> -Tek bir tanıtımla App-V paketleri geçiriliyor: ile aynı ayarları kullanan bir dağıtım türü <br />                Configuration Manager 2007 tanıtımı.<br /><br /> -Birden çok tanıtım içeren App-V paketlerini geçirme: her biri için bir dağıtım türü <br />                Configuration Manager 2007 tanıtımı, bu tanıtım için ayarları kullanır.|[Geçerli dala Configuration Manager nesnelerin geçişini planlama](../../core/migration/planning-for-the-migration-of-objects.md)konusuna bakın.|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrating App-V 5 connection groups to Configuration Manager virtual environments  
Configuration Manager ' deki App-V sanal ortamları, dağıttığınız sanal uygulamaların, istemci bilgisayarlarda aynı dosya sistemini ve kayıt defterini paylaşmasına izin verir. Bu, standart sanal uygulamalardan farklı olarak, bu uygulamaların birbirleriyle veri paylaşabileceği anlamına gelir. Sanal ortamlar, uygulama yüklendiğinde veya sonraki istemciler yüklü uygulamalarını değerlendirdiğinde istemci bilgisayarlarda oluşturulur veya değiştirilir. Sanal ortamlar, tek başına App-V 5 ' teki bağlantı gruplarına benzer.  

Bağlantı gruplarını tek başına App-V 5 ' ten Configuration Manager sanal ortamlara geçirdiğinizde, Configuration Manager istemci bilgisayarlarda zaten var olan bağlantı gruplarını doğru şekilde yönettiğinden ve bu bağlantı gruplarındaki Kullanıcı ortamının korunduğundan emin olmanız gerekir.  

App-V 5 bağlantı gruplarını Configuration Manager sanal ortamlara dönüştürmek için:  

1.  App-V ' d a var olan tüm uygulamalar için Configuration Manager uygulamalar oluşturun.  

2.  Uygulamaları, **Gerekli**dağıtım amaçlı kullanıcılara veya cihazlara dağıtın. Kullanıcılara yapılan dağıtımlar App-V ' d e uygulamayı kullanan kullanıcılara dağıtılmalıdır. Bilgisayarlara yapılan dağıtımlar App-V ' d e uygulamanın bulunduğu bilgisayarlara dağıtılmalıdır.  

3.  Dağıtım tamamlandıktan sonra, tek başına App-V ' d a yayınlanan bağlantı gruplarıyla eşleşen sanal ortamlar oluşturun. Sanal ortamda aynı paketlere (özellikle App-V 5 dağıtım türleri) aynı şekilde sahip olması gerekir.  

App-V sanal ortamının nasıl oluşturulacağı hakkında daha fazla bilgi için bkz. [App-v sanal ortamları oluşturma](../../apps/deploy-use/create-app-v-virtual-environments.md).  

Alternatif olarak, Configuration Manager ile uygulama dağıtmaya başlamadan önce tüm bağlantı gruplarını App-V Istemcisinden silebilirsiniz. Ancak, kullanıcıların App-V bağlantı gruplarına kaydetmiş olabileceği tüm ayarlar kaybedilir.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a> App-V 4.6'da Dinamik Paket Oluşturma  
Dinamik paket oluşturma, bir sanal uygulama paketini başka bir sanal uygulama paketine bağımlılığı olacak şekilde tanımlamanıza olanak sağlayan bir özelliktir. Uygulama çalıştırıldığında App-V İstemcisi birincil paketi ve bağımlı paketi uygulamaya ait aynı sanal ortamda barındırır.  

Bu özelliği Configuration Manager birlikte kullanabilmeniz için her iki paketin de App-V Istemcisine dağıtılması ve kaydedilmesi gerekir. Bağımlı paket içeriğinin istemci bilgisayarında yerel olarak barındırıldığından emin olmak için, uygulama dağıtımını yerel teslimat (indir ve Yürüt) olarak ayarlayın.  

App-V Dynamic Suite Composition hakkında daha fazla bilgi edinmek için App-V belgelerinize bakın.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a> App-V 4.6 uygulamalarını App-V 5 uygulamalarına dönüştürme  
App-V 4.6 ve App-V 5 arasındaki uygulama paket biçimi değişmiştir. App-V 4.6 kullanılarak sıralanmış olan uygulamalar artık desteklenmez. Ancak App-V 5, uygulamaları dönüştürmek için kullanabileceğiniz bir paket dönüştürücü aracına sahiptir. Daha fazla bilgi edinmek için [App-V 5 belgelerinize](https://technet.microsoft.com/library/jj713472.aspx)bakın.  

App-V 4.6 uygulamalarını App-V 5 uygulamalarına dönüştürmek için aşağıdaki adımları kullanın:  

1.  App-V 4,6 paketlerini App-V 5 biçimine dönüştürün veya yeniden sıralayın.  

2.  App-V 5 istemcisini hiyerarşinizdeki bilgisayarlara dağıtın.  

3.  App-V 5 uygulamalarınız için dağıtım türlerini içeren yeni uygulamalar oluşturun ve App-V 4.6 uygulamalarının yerini alması için yenisiyle değiştirme kuralları oluşturun.  

4.  Sanal ortamları gerektiği şekilde oluşturun.  

5.  Yeni App-V 5 uygulamalarını bilgisayarlara dağıtın.  

##  <a name="user-and-deployment-configuration-files"></a>Kullanıcı ve dağıtım yapılandırma dosyaları  
Kullanıcı ve dağıtım yapılandırma dosyaları, bir uygulamanın nasıl davrandığını denetleyen ayarlara sahiptir. Uygulamayı yeniden sıralama yapmadan uygulama ayarlarını değiştirmek için bu dosyaları kullanabilirsiniz.  

Tipik bir App-V 5 uygulaması şu dosyaları içerebilir:  

-   Bir uygulama paketi (. appv) dosyası  

-   Bir Kullanıcı yapılandırma dosyası  

-   Bir dağıtım yapılandırma dosyası  

Kullanıcı yapılandırma dosyası, yalnızca oturum açan kullanıcı için uygulanan ayarlara sahiptir. Örneğin, kullanıcılara dağıtılacak uygulama kısayoluyla ilgili bilgileri değiştirmek üzere yapılandırma dosyalarını düzenleyebilirsiniz. Ayrıca, birden çok dağıtım türüyle Configuration Manager bir uygulama oluşturabilirsiniz. Her dağıtım türü, farklı bir Kullanıcı yapılandırma dosyası içerebilir ve bunların ilgili kullanıcılar için yüklendiğinden emin olmak için gereksinim kurallarını kullanabilir.  

Dağıtım yapılandırma dosyası, kayıt defteri ayarları gibi, bilgisayara uygulanan ayarlara sahiptir. Bu dosya, tüm kullanıcılara uygulanan kullanıcı ayarlarına de sahip olabilir.  

App-V 5 sanal uygulamalarını Configuration Manager dağıtmak istiyorsanız, App-V 5 dağıtım türünü oluşturduğunuzda üç dosyanın tümünün aynı klasörde mevcut olması gerekir. Klasörde birden fazla dosya varsa Configuration Manager en güncel olanı kullanır.  

Daha fazla bilgi edinmek için [App-V 5 belgelerinize](https://technet.microsoft.com/library/jj713466.aspx)bakın.  

##  <a name="app-v-local-interaction"></a>App-V yerel etkileşimi  
Bazı uygulama dağıtım senaryolarında, uygulamalar istemci bilgisayarlarına yerel olarak yüklenir ve diğer uygulamalar aynı istemci bilgisayarına sanal uygulamalar olarak dağıtılır. Varsayılan olarak, yerel olarak yüklenen uygulamalar sanal uygulamaları doğrudan görüntüleyemez veya bağlanamaz. Bu, App-V tarafından sağlanan uygulama yalıtımının amaçlanan davranışıdır. Yerel etkileşim, bir App-V Istemcisinin, bir istemci bilgisayarda çalışan yerel olarak yüklenen uygulamalara, sanallaştırılmış uygulamalarla ilgili ve iletişim kurmasına izin vermek için etkinleştirebilen bir özelliktir. Configuration Manager ve App-V yerel etkileşimi tam olarak destekler.  

App-V yerel etkileşim özelliği hakkında daha fazla bilgi için App-V belgelerinize bakın.  

##  <a name="app-v-5-shared-content-store"></a> App-V 5 Paylaşılan İçerik Deposu  
Configuration Manager App-V 5 paylaşılan Içerik depolama özelliğini destekler. Daha fazla bilgi için bkz. [App-V 5.0 Paylaşılan İçerik Deposu (SCS) Planlaması](https://technet.microsoft.com/library/jj713431.aspx).  

##  <a name="monitoring-virtual-applications"></a>Sanal uygulamaları izleme  

### <a name="virtual-application-reports"></a>Sanal uygulama raporları  
Configuration Manager ortamınızda App-V ' i izlemek için aşağıdaki raporları kullanabilirsiniz:  

|Rapor adı|Açıklama|  
|-----------------|-----------------|  
|App-V Sanal Ortam Sonuçları|Seçili bir koleksiyon için belirli bir durumda olan seçili bir sanal ortam hakkındaki bilgileri gösterir (yalnızca App-V 5).|  
|Varlık için App-V Sanal Ortam Sonuçları|Belirtilen bir varlık için seçili sanal ortam ve seçili sanal ortam için herhangi bir dağıtım türü (yalnızca App-V 5) hakkındaki bilgileri gösterir.|  
|App-V Sanal Ortam Durumu|Seçili bir koleksiyon için seçili sanal ortam için uyumluluk bilgilerini gösterir. Bu rapordaki **tutulan** sütun, daha önce ayarlanan bir sanal ortamın artık geçerli olmadığı, ancak sanal ortamda (yalnızca App-V 5) çalışan uygulamalarda Kullanıcı ayarlarını kalıcı hale getirmek için korunan varlıkları gösterir.|  
|Belirli bir sanal uygulamaya sahip bilgisayarlar|Uygulama sanallaştırma yönetimi Sıralayıcı 'nın oluşturduğu belirtilen App-V kısayoluna sahip bilgisayarların özetini gösterir (yalnızca App-V 4,6).|  
|Belirli bir sanal uygulama paketine sahip bilgisayarlar|Belirtilen App-V uygulama paketinin yüklü olduğu bilgisayarların listesini gösterir (yalnızca App-V 4,6).|  
|Tüm sanal uygulama paket örneklerini say|Algılanan tüm App-V uygulama paketlerinin (yalnızca App-V 4,6) sayısını gösterir.|  
|Tüm sanal uygulama örneklerinin say|Algılanan tüm App-V uygulamalarının (yalnızca App-V 4,6) sayısını gösterir.|  

### <a name="log-files"></a>Günlük dosyaları  
Configuration Manager, günlük dosyalarındaki sanal uygulama dağıtımlarıyla ilgili bilgileri kaydeder. Sanal uygulamaların ve Configuration Manager uygulama yönetiminin kullandığı günlük dosyaları hakkında bilgi için bkz. [günlük dosyaları](../../core/plan-design/hierarchy/log-files.md).  

Windows 8.1 için C:\ProgramData\Microsoft\Application Virtualization Istemcisinde App-V istemcisine ait günlükleri bulun.  
