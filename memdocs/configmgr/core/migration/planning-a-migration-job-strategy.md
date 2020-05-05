---
title: Geçiş işi planlaması
titleSuffix: Configuration Manager
description: Configuration Manager geçerli dal ortamınıza geçirmek istediğiniz verileri yapılandırmak için geçiş işlerini kullanın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87aac20a2ac70e843bf17982375c92804de2b20e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719676"
---
# <a name="plan-a-migration-job-strategy-in-configuration-manager"></a>Configuration Manager bir geçiş işi stratejisi planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dal ortamınıza geçirmek istediğiniz belirli verileri yapılandırmak için geçiş işlerini kullanın. Geçiş işleri geçirmeyi planladığınız nesneleri belirler ve hedef hiyerarşinizdeki en üst düzey sitede çalışır. Her kaynak site için bir veya daha fazla geçiş işi ayarlayabilirsiniz. Bu, her bir iş ile tüm nesneleri tek seferde geçirmenize veya sınırlı veri alt kümelerine geçirebilmenizi sağlar.  

 Configuration Manager, kaynak hiyerarşisinden bir veya daha fazla siteden başarıyla veri topladıktan sonra geçiş işleri oluşturabilirsiniz. Toplanan verilerin olduğu kaynak sitelerden verileri istediğiniz sırayla geçirebilirsiniz. Configuration Manager 2007 kaynak sitesiyle, yalnızca bir nesnenin oluşturulduğu siteden veri geçirebilirsiniz. System Center 2012 Configuration Manager veya üstünü çalıştıran kaynak sitelerde, geçirebileceğiniz tüm veriler kaynak hiyerarşinin en üst düzey sitesinde bulunabilir.  

 Hiyerarşiler arasında istemcileri geçirmeden önce, istemciler tarafından kullanılan nesnelerin geçirildiğinden ve bu nesnelerin hedef hiyerarşide kullanılabildiğinden emin olun. Örneğin, bir Configuration Manager 2007 SP2 kaynak hiyerarşisinden geçiş yaptığınızda, istemci içeren özel bir koleksiyona dağıtılan içerik için bir tanıtıma sahip olabilirsiniz. Bu senaryoda, istemciyi geçirmeden önce koleksiyonu, tanıtımı ve ilişkili içeriği geçirmeniz önerilir. İçerik, koleksiyon ve tanıtım istemci geçirilmeden önce geçirildiyse, bu veriler hedef hiyerarşisinde istemciyle ilişkilendirilemez. Bir istemci daha önce çalışan tanıtım ve içerikle ilgili verilerle ilişkilendirilmezse, istemciye hedef hiyerarşide yüklenmek üzere içerik teklif edilebilir ve bu da gereksiz olabilir. Veriler geçirildikten sonra istemci geçirilirse, istemci bu içerik ve tanıtımla ilişkilendirilir ve tanıtım tekrarlanan türde değilse, geçirilen tanıtım için bu içerik istemciye tekrar teklif edilmez.  

 Bazı nesneler verilerin kaynak hiyerarşiden hedef hiyerarşiye geçirilmesini gerektirir. Örneğin, istemcileriniz için yazılım güncelleştirmelerini hedef hiyerarşinize başarıyla geçirmek için etkin bir yazılım güncelleştirme noktası dağıtmanız, ürün kataloğunu yapılandırmanız ve yazılım güncelleştirme noktasını hedef hiyerarşisinde Windows Server Update Services (WSUS) ile eşitlemeniz gerekir.  

##  <a name="types-of-migration-jobs"></a><a name="Types_of_Migration"></a>Geçiş işlerinin türleri  
 Configuration Manager, aşağıdaki geçiş işi türlerini destekler. Her iş türü, o işe dahil ettiğiniz nesneleri tanımlamaya yardımcı olacak şekilde tasarlanmıştır.  

 **Koleksiyon geçişi** (yalnızca CONFIGURATION Manager 2007 SP2 'den geçiş yaparken desteklenir): seçtiğiniz koleksiyonlarla Ilgili nesneleri geçirme. Varsayılan olarak, koleksiyon geçişi, koleksiyonun üyeleriyle ilişkilendirilmiş tüm nesneleri içerir. Koleksiyon geçiş işi kullanırken belirli nesne örneklerini hariç tutabilirsiniz.  

 **Nesne geçişi**: seçtiğiniz ayrı nesneleri geçirin. Geçirmek istediğiniz belirli verileri seçin.  

 **Daha önce geçirilen nesne geçişi**: son geçirildikten sonra kaynak hiyerarşisinde güncelleştirdiklerinde daha önce geçirdiğiniz nesneleri geçirin.  

###  <a name="objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a>Geçirebileceğiniz nesneler  
 Her nesne belirli bir geçiş işi türüyle geçirilemez. Aşağıdaki liste, geçiş işi türlerinin her biriyle geçirebileceğiniz nesne türlerini tanımlar.  

> [!NOTE]  
>  Koleksiyon geçiş işleri yalnızca Configuration Manager 2007 SP2 kaynak hiyerarşisinden nesne geçirdiğinizde kullanılabilir.  

 **Her nesneyi geçirmek için kullanabileceğiniz iş türleri**  

-   **Tanıtımlar** (desteklenen Configuration Manager 2007 kaynak sitelerinden geçiş için kullanılabilir)  

    -   Koleksiyon geçişi  


-   **Varlık Yönetim Bilgileri kataloğu**  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Varlık Yönetim Bilgileri donanım gereksinimleri**  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Varlık Yönetim Bilgileri yazılım listesi**  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Sınırlar**  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Yapılandırma temelleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Yapılandırma öğeleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Bakım pencereleri**  

    -   Koleksiyon geçişi  


-   **İşletim sistemi dağıtımı önyükleme görüntüleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **İşletim sistemi dağıtımı sürücü paketleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **İşletim sistemi dağıtımı sürücüleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **İşletim sistemi dağıtımı görüntüleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **İşletim sistemi dağıtım paketleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Yazılım dağıtım paketleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Yazılım kullanım ölçümü kuralları**  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Yazılım güncelleştirmesi dağıtım paketleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Yazılım güncelleştirmesi dağıtım şablonları**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Yazılım güncelleştirme dağıtımları**  

    -   Koleksiyon geçişi  


-   **Yazılım güncelleştirmesi listeleri**  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Görev dizileri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    -   Daha önce geçirilen nesne geçişi  

-   **Sanal uygulama paketleri**  

    -   Koleksiyon geçişi  

    -   Nesne geçişi  

    > [!IMPORTANT]  
    >  Sanal bir uygulama paketini nesne geçişini kullanarak geçirmeniz mümkün olmakla birlikte, paketler **Daha Önce Geçirilen Nesne Geçişi** geçiş işi türü kullanılarak geçirilemez. Geçirilen sanal uygulama paketini hedef siteden silmeniz ve sonra sanal uygulamayı geçirmek için yeni bir geçiş işi oluşturmanız gerekir.  

##  <a name="general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a>Tüm geçiş işleri için genel planlama  
 Nesneleri hedef hiyerarşinize geçirmek üzere bir geçiş işi oluşturmak için geçiş Işi oluşturma Sihirbazı 'nı kullanın. Oluşturduğunuz geçiş işinin türü geçişte hangi nesnelerin kullanılabileceğini belirler. Aynı kaynak siteden veya birden çok kaynak sitesinden veri geçirmek için birden fazla geçiş işi oluşturup kullanabilirsiniz. Bir geçiş işi türünün kullanılması, farklı bir tür geçiş işi kullanmayı engellemez.  

 Bir geçiş işi başarıyla çalıştıktan sonra, durumu **Tamamlandı** olarak listelenir ve tekrar çalıştırılamaz. Bununla birlikte, orijinal iş tarafından geçirilen nesnelerden herhangi birini geçirmek için yeni bir geçiş işi oluşturabilirsiniz ve yeni geçiş işi ek nesneler de içerebilir. Ek geçiş işleri oluşturduğunuzda, daha önce geçirilmiş nesneler **geçirilmiş**durumunu gösterir. Bu nesneleri yeniden geçirmek için seçebilirsiniz, ancak nesne kaynak hiyerarşisinde güncellenmemişse, bu nesneleri yeniden geçirmek gerekli değildir. Nesne ilk geçirildikten sonra kaynak hiyerarşide güncelleştirilmişse, **Geçiş sonrası değiştirilen nesneler** geçiş işi türünü kullandığınızda bu nesneyi tanımlayabilirsiniz.  

 Bir geçiş işini çalıştırılmadan önce silebilirsiniz. Ancak, bir geçiş işi tamamlandıktan sonra, Configuration Manager konsolunda görünür kalır ve silinemez. Tamamlanan veya henüz çalıştırılmayan her geçiş işi, geçiş işlemini tamamlayana ve geçiş verilerini temizleyene kadar Configuration Manager konsolunda görünür olmaya devam eder.  

> [!NOTE]  
>  **Geçiş verilerini temizle** eylemini kullanarak geçişi tamamladıktan sonra, daha önce geçirdiğiniz nesnelere görünürlüğü geri yüklemek için aynı hiyerarşiyi geçerli kaynak hiyerarşisiyle yeniden yapılandırabilirsiniz.  

 Configuration Manager konsolundaki herhangi bir geçiş işinde yer alan nesneleri, geçiş işini seçerek ve sonra **iş sekmesinde nesneler '** i seçerek görüntüleyebilirsiniz.  

 Tüm geçiş işlerini planlamanıza yardımcı olması için aşağıdaki bölümlerde yer alan bilgileri kullanın.  

### <a name="data-selection"></a>Veri seçimi  
 Bir koleksiyon geçiş işi oluşturduğunuzda bir veya daha fazla koleksiyon seçmeniz gerekir. Koleksiyonları seçtikten sonra, geçiş Işi oluşturma Sihirbazı koleksiyonlarla ilişkili nesneleri gösterir. Varsayılan olarak, seçili koleksiyonlarla ilişkili tüm nesneler geçirilir, ancak bu işle geçiş yapmak istemediğiniz nesnelerin işaretini kaldırabilirsiniz. Bağımlı nesneleri olan bir nesnenin işaretini kaldırdığınızda, bu bağımlı nesneler de işaretlenmemiştir. Tüm işaretlenmemiş nesneler bir dışlama listesine eklenir. Bir dışlama listesinde yer alan nesneler gelecekteki geçiş işleri için otomatik seçimden çıkarılır. Gelecekte oluşturacağınız geçiş işlerinde geçiş için otomatik olarak seçilmesini istediğiniz nesneleri kaldırmak için dışlama listesini manuel olarak düzenlemeniz gerekir.  

### <a name="site-ownership-for-migrated-content"></a>Geçirilen içerik için site sahipliği  
 Dağıtım için içerik geçişi yaparken, içerik nesnesini hedef hiyerarşisindeki bir siteye atamanız gerekir. Böylece bu site hedef hiyerarşisinde o içeriğin sahibi olur. Hedef hiyerarşinizdeki üst düzey site, fiili olarak o içeriğin meta verilerinin geçişini yapan site olsa da, ağ çapında içerik için orijinal kaynak dosyalarına erişen, atanmış sitedir.  

 Geçiş sırasında kullanılan ağ bant genişliğini en aza indirmek için, içeriğin sahipliğini kullanılabilir en yakın siteye aktarmayı düşünebilirsiniz. İçerikle ilgili bilgiler Configuration Manager ' de küresel olarak paylaşıldığından, her sitede kullanılabilir hale gelir.  

 İçerik hakkındaki bilgiler, veritabanı çoğaltma kullanılarak hedef hiyerarşideki tüm sitelerle paylaşılır. Bununla birlikte, birincil siteye atadığınız ve ardından diğer birincil sitelerdeki dağıtım noktalarına dağıttığınız tüm içerikler dosya tabanlı çoğaltma kullanarak aktarır. Bu aktarma, merkezi yönetim sitesi üzerinden ve sonra her ek birincil siteye yönlendirilir. Bir siteyi içerik sahibi olarak atadığınızda, geçiş sırasında birden fazla birincil siteye dağıtmayı planladığınız paketleri merkezileştirerek, düşük bant genişlikli ağlarda veri aktarımını azaltabilirsiniz.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Geçirilen veriler için rol tabanlı yönetim güvenlik kapsamları  
 Bir hedef hiyerarşiye veri geçirdiğinizde, verileri geçirilen nesnelere bir veya daha fazla rol tabanlı yönetim güvenlik kapsamı atamanız gerekir. Bu yalnızca uygun yönetici kullanıcıların geçiş sonrasında bu verilere erişimi olmasını sağlar. Belirttiğiniz güvenlik kapsamları geçiş işi tarafından tanımlanır ve bu iş tarafından geçirilen her nesneye uygulanır. Farklı nesne kümelerine farklı güvenlik kapsamları uygulanmasını gerektiriyorsa ve bu kapsamları geçiş sırasında atamak istiyorsanız farklı geçiş işleri kullanarak farklı nesne kümelerini geçirmeniz gerekir.  

 Bir geçiş işi ayarlamadan önce, rol tabanlı yönetimin Configuration Manager nasıl çalıştığını gözden geçirin. Gerekirse, hedef hiyerarşide geçirilen nesnelere kimlerin erişimi olacağını denetlemek için geçirdiğiniz veriler için bir veya daha fazla güvenlik kapsamı ayarlayın.  

 Güvenlik kapsamları ve rol tabanlı yönetim hakkında daha fazla bilgi için bkz. [Configuration Manager için rol tabanlı yönetimin temelleri](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Geçiş eylemlerini gözden geçirme  
 Bir geçiş işi ayarlarken, geçiş Işi oluşturma Sihirbazı, başarılı bir geçiş ve Configuration Manager seçili verilerin geçişi sırasında yapacağı eylemlerin bir listesini içeren bir işlem listesi gösterir. Beklenen sonucu denetlemek için bu bilgileri dikkatle gözden geçirin.  

### <a name="schedule-migration-jobs"></a>Geçiş işlerini zamanlama  
 Varsayılan olarak, bir geçiş işi oluşturulduktan hemen sonra çalışır. Ancak, işi oluştururken veya işin özelliklerini düzenleyerek geçiş işinin ne zaman çalışacağını belirtebilirsiniz. Geçiş işini şu şekilde çalışacak şekilde zamanlayabilirsiniz:  

-   İşi şimdi çalıştır  

-   İşi belirtilen başlama saatinde çalıştır  

-   İşi çalıştırma  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Geçirilen veriler için çakışma çözümü belirtme  
 Varsayılan olarak, geçiş işini daha önce hedef veritabanına geçirilmiş olan verileri atlayacak veya üzerine yazacak şekilde yapılandırmadığınız müddetçe geçiş işleri hedef veritabanındaki verilerin üzerine yazmaz.  

##  <a name="plan-for-collection-migration-jobs"></a><a name="About_Collection_Migration"></a>Koleksiyon geçiş işlerini planlayın  
 Koleksiyon geçiş işleri yalnızca, Configuration Manager 2007 ' nin desteklenen bir sürümünü çalıştıran bir kaynak hiyerarşisinden veri geçirdiğinizde kullanılabilir. Koleksiyonları geçirirken bir veya birden fazla koleksiyon belirtmeniz gerekir. Belirttiğiniz her koleksiyon için geçiş işi, geçirilecek tüm ilgili nesneleri otomatik olarak seçer. Örneğin, belirli bir kullanıcı koleksiyonunu belirtirseniz koleksiyon üyeleri belirlenir ve böylece bu koleksiyonla ilişkilendirilen dağıtımları geçirebilirsiniz. İsteğe bağlı olarak, bu üyelerle ilişkilendirilen geçirilecek diğer dağıtım nesnelerini seçebilirsiniz. Tüm bu seçilen öğeler, geçirilebilecek nesneler listesine eklenir.  

 Bir koleksiyonu geçirdiğinizde Configuration Manager, bakım pencereleri ve koleksiyon değişkenleri dahil olmak üzere koleksiyon ayarlarını da geçirir, ancak AMT istemci sağlaması için koleksiyon ayarlarını geçiremez.  

 Koleksiyon tabanlı geçiş işleri için uygulanabilecek ek konfigürasyonlar hakkında bilgi edinmek için aşağıdaki bölümlerde yer alan bilgileri kullanın.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Nesneleri koleksiyon geçiş işlerinin dışında tut  
 Belirli nesneleri bir koleksiyon geçiş işinin dışında tutabilirsiniz. Belirli bir nesneyi koleksiyon geçiş işinden dışlayabilirsiniz, bu nesne, geçerli kaynak hiyerarşisindeki tüm kaynak siteler için oluşturulan geçiş işlerinin dışında bıraktığınız tüm nesneleri içeren bir genel çıkarma listesine eklenir. Dışlama listesindeki nesneler hala gelecekteki işlerde geçiş için kullanılabilir, ancak yeni bir koleksiyon tabanlı geçiş işi oluşturduğunuzda otomatik olarak dahil edilmez.  

 Daha önceden dışarıda bıraktığınız nesneleri kaldırmak için çıkarma listesini düzenleyebilirsiniz. Çıkarma listesinden bir nesneyi kaldırmanızın ardından bu nesne, yeni bir geçiş işi oluşturma sırasında ilişkilendirilmiş bir koleksiyon belirtildiğinde otomatik olarak seçilir.  

### <a name="unsupported-collections"></a>Desteklenmeyen koleksiyonlar  
 Configuration Manager, varsayılan kullanıcı koleksiyonlarını, cihaz koleksiyonlarını ve birçok özel koleksiyonu Configuration Manager 2007 kaynak hiyerarşisinden geçirebilir. Ancak Configuration Manager, aynı koleksiyondaki kullanıcıları ve cihazları içeren koleksiyonları geçiremez.  

 Şu koleksiyonlar geçirilemez:  

-   Kullanıcıları ve cihazları olan bir koleksiyon.  

-   Farklı bir kaynak türü koleksiyonuna başvuru içeren bir koleksiyon. Örneğin, bir alt koleksiyon ya da Kullanıcı tabanlı bir koleksiyonun bağlantısı olan cihaz tabanlı bir koleksiyon. Bu örnekte, yalnızca en üst düzey koleksiyon geçirilir.  

-   Bilinmeyen bilgisayarları dahil etme kuralına sahip bir koleksiyon. Koleksiyon geçirilir, ancak bilinmeyen bilgisayarları dahil etme kuralı geçirilmez.  

### <a name="empty-collections"></a>Boş koleksiyonlar  
 Boş koleksiyon, kendisiyle ilişkilendirilen kaynağı olmayan bir koleksiyondur. Configuration Manager boş bir koleksiyonu geçirdiğinde, koleksiyonu Kullanıcı veya cihazı olmayan bir kurumsal klasöre dönüştürür. Bu klasör, Configuration Manager konsolundaki **varlıklar ve uyum** çalışma alanındaki **Kullanıcı koleksiyonları** veya **Cihaz Koleksiyonları** düğümü altında boş koleksiyonun adıyla oluşturulur.  

### <a name="linked-collections-and-subcollections"></a>Bağlı koleksiyonlar ve alt koleksiyonlar  
 Diğer koleksiyonlara bağlı olan veya alt koleksiyonlara sahip olan koleksiyonları geçirdiğinizde, Configuration Manager bağlı koleksiyonlar ve alt koleksiyonlara ek olarak **Kullanıcı koleksiyonları** veya **Cihaz Koleksiyonları** düğümü altında bir klasör oluşturur.  

### <a name="collection-dependencies-and-include-objects"></a>Koleksiyon bağımlılıkları ve nesneleri dahil etme  
 Geçiş Işi oluşturma Sihirbazı ' nda geçirilecek bir koleksiyon belirttiğinizde, tüm bağımlı koleksiyonlar işe eklenmek üzere otomatik olarak seçilir. Bu davranış, gereken tüm kaynakların geçişin ardından kullanılabilir olmasını sağlar.  

 Örneğin: Windows 10 çalıştıran ve **Win_10**olarak adlandırılan cihazlar için bir koleksiyon seçersiniz. Bu koleksiyon, tüm istemci işletim sistemlerinize sahip olan ve **All_Clients**adlı bir koleksiyonla sınırlıdır. Koleksiyon **All_Clients** , geçiş için otomatik olarak seçilir.  

### <a name="collection-limiting"></a>Koleksiyon sınırlandırma  
 Geçerli dalı Configuration Manager, Koleksiyonlar genel verilere sahiptir ve hiyerarşideki her bir sitede değerlendirilir. Bu nedenle, geçiş sonrasında koleksiyon kapsamının nasıl sınırlandırılacağını planlayın. Geçiş sırasında, geçirilen koleksiyonların beklenmeyen üyeleri dahil etmemesi amacıyla geçirdiğiniz koleksiyonun kapsamını sınırlandırmak için kullanmak üzere hedef hiyerarşisinden bir koleksiyon belirleyebilirsiniz.  

 Örneğin, Configuration Manager 2007 ' de koleksiyonlar kendilerini oluşturan sitede ve alt sitelerde değerlendirilir. Bir reklam yalnızca bir alt siteye dağıtılabilir, bu durum ise reklamın alt site için kapsamını sınırlandırır. Karşılaştırma, Configuration Manager geçerli Dalla birlikte her sitede değerlendirilir ve ilgili tanıtımlar her bir site için değerlendirilir. Koleksiyon sınırlandırma, beklenmeyen koleksiyon üyelerinin eklenmesini önlemek için diğer bir koleksiyona bağlı olarak koleksiyon üyelerini daraltmanızı sağlar.  

### <a name="site-code-replacement"></a>Site kodu değişimi  
 Configuration Manager 2007 sitesini tanımlayan ölçütlere sahip bir koleksiyonu geçirdiğinizde hedef hiyerarşisinde belirli bir site belirtmeniz gerekir. Bu, geçirilen koleksiyonun hedef hiyerarşinizde işlevsel kalmasını ve kapsamının genişlememesini sağlar.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Geçirilen tanıtımlar için davranış belirtme  
 Varsayılan olarak, koleksiyon tabanlı geçiş işleri hedef hiyerarşiye geçiş yapan reklamları devre dışı bırakır. Bu durum, reklamla ilişkilendirilen tüm programları içerir. Reklamları olan koleksiyon tabanlı bir geçiş işi oluşturduğunuzda, geçiş Işi oluşturma Sihirbazı 'nın **Ayarlar** sayfasında **bir tanıtım geçirildikten sonra programları Configuration Manager dağıtım için etkinleştir** seçeneğini görürsünüz. Bu seçeneği seçerseniz, reklamlarla ilişkilendirilen programlar geçirildikten sonra etkinleştirilir. En iyi uygulama olarak, bu seçeneği seçmeyin. Bunun yerine, programları, bunları alacak olan istemcileri doğrulayabilmeniz için geçirildikten sonra etkinleştirin.  

> [!NOTE]  
>  **Bir tanıtım geçirildikten sonra programları Configuration Manager dağıtım Için etkinleştir** seçeneğini yalnızca koleksiyon tabanlı bir geçiş işi oluştururken ve geçiş işi reklamlar içerdiğinde görürsünüz.  

 Geçişten sonra bir programı etkinleştirmek için program özelliklerinin **Gelişmiş** sekmesinde **Bu programı tanıtılan bilgisayarlarda devre dışı bırak** seçeneğini temizleyin.  

##  <a name="plan-for-object-migration-jobs"></a><a name="About_Object_Migration"></a>Nesne geçiş işlerini planlayın  
 Koleksiyon geçişinden faklı olarak, geçirmek istediğiniz her bir nesneyi ve nesne örneğini seçmeniz gerekir. Belirli bir geçiş işi için geçirilecek nesneler listesine eklemek üzere tek tek nesneleri (Configuration Manager 2007 hiyerarşisinin reklamları veya System Center 2012 Configuration Manager veya Configuration Manager geçerli dal hiyerarşisinden) seçebilirsiniz. Geçiş listesine eklemediğiniz hiçbir nesne, nesne geçiş işi tarafından hedef siteye geçirilmez.  

 Nesne tabanlı geçiş işleri, tüm geçiş işleri için geçerli olan işlerin ötesinde ek yapılandırmalara sahip değildir.  

##  <a name="plan-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a>Daha önce geçirilen nesne geçiş işlerini planlayın  
 Hedef hiyerarşisine çoktan geçirdiğiniz bir nesne kaynak hiyerarşisinde güncelleştirildiğinde **Geçiş sonrası değiştirilen nesneler** iş türünü kullanarak bu nesneyi tekrar geçirebilirsiniz. Örneğin, kaynak hiyerarşisindeki bir paket için kaynak dosyaları yeniden adlandırdığınızda veya güncelleştirdiğinizde, paket sürümü kaynak hiyerarşisinde artar. Paket sürümü arttırıldıktan sonra paket, bu iş türü tarafından geçiş için tanımlanabilir.  

 Bu iş türü nesne geçiş türüne benzerdir, ancak geçirilecek nesneleri seçerken yalnızca daha önceki bir geçiş işi tarafından geçirildikten sonra güncelleştirilen nesneleri seçebilirsiniz.   

 Bu iş türünü seçtiğinizde geçiş Işi oluşturma Sihirbazı 'nın **Ayarlar** sayfasındaki çakışma çözümleme davranışı, daha önce geçirilen nesnelerin üzerine yazılacak şekilde yapılandırılmıştır. Bu ayar değiştirilemez.  

> [!NOTE]  
>  Bu geçiş işi, kaynak hiyerarşisi tarafından otomatik olarak güncelleştirilen ve bir yönetici kullanıcının güncelleştirdiği nesneleri belirleyebilir.  
