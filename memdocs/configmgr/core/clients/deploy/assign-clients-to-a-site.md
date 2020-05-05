---
title: İstemcileri bir siteye atama
titleSuffix: Configuration Manager
description: İstemcileri Configuration Manager bir siteye atayın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2270435ac13585cb0b7d3271f1faa02cc728d3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075753"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Configuration Manager ' de bir siteye istemci atama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir Configuration Manager istemcisi yüklendikten sonra, yönetebilmeniz için bir Configuration Manager birincil sitesine katılması gerekir. Bir istemcinin katıldığı site, *atanan sitesi*olarak adlandırılır. İstemciler merkezi bir yönetim sitesine veya ikincil bir siteye atanamaz.  

Atama işlemi, istemci başarıyla yüklendikten sonra gerçekleşir ve istemci bilgisayarını hangi sitenin yönettiğini belirler. İstemciyi doğrudan bir siteye atayabilir veya istemcinin geçerli ağ konumuna ya da hiyerarşi için yapılandırılmış bir geri dönüş sitesine göre uygun bir siteyi otomatik olarak bulduğu otomatik site atamasını kullanabilirsiniz.

Mobil cihaz istemcisini Configuration Manager kaydı sırasında yüklediğinizde, cihaz her zaman otomatik olarak bir siteye atanır. İstemciyi bir bilgisayara yüklediğinizde, istemcinin bir siteye atayıp atamamayacağını seçebilirsiniz. Ancak, istemci, yüklenip atanmadığında, site ataması başarılı olana kadar yönetilmez.  
 

> [!NOTE]  
>  İstemcileri her zaman aynı Configuration Manager sürümünü çalıştıran sitelere atayın. Daha yeni bir sürümden bir Configuration Manager istemcisini eski bir sürümden bir siteye atamaktan kaçının.   Gerekirse, birincil siteyi istemciler için kullandığınız Configuration Manager sürümüne güncelleştirin.  

İstemci bir siteye atandıktan sonra, istemci IP adresini değiştirse ve başka bir siteye gezinse bile, o siteye atanmış kalır. Yalnızca bir yönetici, istemciyi el ile başka bir siteye atayabilir veya istemci atamasını kaldırabilir.  

> [!WARNING]  
>  Bir siteye atanmış kalan bir istemci için bir istisna, istemciyi, yazma filtreleri etkinleştirildiğinde Windows Katıştırılmış bir aygıta atamaktır. İstemciyi atamadan önce yazma filtrelerini devre dışı bırakmazsanız, istemcinin site ataması durumu, aygıt sonra ilk kez yeniden başlatıldığında orijinal durumuna geri döner.  
>   
>  Örneğin, istemci otomatik site ataması için yapılandırılmamışsa, başlangıçta yeniden atanır ve farklı bir siteye atanabilir. İstemci otomatik site ataması için yapılandırılmamışsa ancak el ile site ataması gerektiriyorsa, Configuration Manager kullanarak bu istemciyi yeniden yönetebilmeniz için önce başlangıçtan sonra istemciyi el ile yeniden atamanız gerekir.  
>   
>  Bu davranışı önlemek için, istemciyi katıştırılmış aygıtlara atamadan önce yazma filtrelerini devre dışı bırakın ve ardından site atamasının başarılı olduğunu doğruladıktan sonra yazma filtrelerini etkinleştirin.  

İstemci ataması başarısız olursa, istemci yazılımı yüklü kalır, ancak yönetilmez. Bir istemci, bir siteye yüklenip atanmadığında veya bir siteye atanmış olup bir yönetim noktasıyla iletişim kuramadığında yönetilmeyen olarak değerlendirilir.  

##  <a name="using-manual-site-assignment-for-computers"></a>Bilgisayarlar için El İle Site Atamasını Kullanma  
 Aşağıdaki iki yöntemi kullanarak, istemci bilgisayarlarını el ile bir siteye atayabilirsiniz:  

-   Site kodunu belirten bir istemci yükleme özelliği kullanın.  

-   Denetim Masası’nda, **Configuration Manager**’da, site kodunu belirtin.  

> [!NOTE]  
>  Bir istemci bilgisayarını, varolmayan bir Configuration Manager site koduna el ile atarsanız, site ataması başarısız olur.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a> Bilgisayarlar için Otomatik Site Atamasını Kullanma  
 Otomatik site ataması, istemci dağıtımı sırasında veya Denetim Masası’nda **Configuration Manager Özellikleri** ’nin **Gelişmiş** sekmesinde **Site Bul** ’a tıkladığınızda gerçekleşebilir. Configuration Manager istemcisi kendi ağ konumunu Configuration Manager hiyerarşisinde yapılandırılan sınırlarla karşılaştırır. İstemcinin ağ konumu, site ataması için etkinleştirilmiş bir sınır grubu içine düşerse veya hiyerarşi bir geri dönüş sitesi için yapılandırılmışsa, istemci, bir site kodu belirtmenize gerek kalmadan otomatik olarak o siteye atanır.  

 Aşağıdakilerin bir veya daha fazlasını kullanarak sınırları yapılandırabilirsiniz:  

-   IP alt ağı  

-   Active Directory sitesi  

-   IP v6 öneki  

-   IP adresi aralığı  

> [!NOTE]  
>  Bir Configuration Manager istemcisinde birden çok ağ bağdaştırıcısı varsa ve bu nedenle birden çok IP adresi varsa, istemci site atamasını değerlendirmek için kullanılan IP adresi rastgele atanır.  

 Site ataması için sınır gruplarının nasıl yapılandırılacağı ve otomatik site ataması için bir geri dönüş sitesinin nasıl yapılandırılacağı hakkında bilgi için, bkz. [Configuration Manager için site sınırlarını ve sınır gruplarını tanımlama](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Otomatik site ataması kullanan istemciler Configuration Manager Active Directory Domain Services yayımlanan site sınır gruplarını bulmayı dener. Bu başarısız olursa (örneğin, Active Directory şeması Configuration Manager için genişletilmemişse veya istemciler çalışma grubu bilgisayarlardır), istemcileri bir yönetim noktasından sınır grubu bilgilerini alabilir.  

 İstemci bilgisayarları için, yüklendiklerinde kullanmaları için bir yönetim noktası belirtebilirsiniz veya istemciler DNS yayımlaması veya WINS kullanarak bir yönetim noktası bulabilir.  

 İstemci, ağ konumunu içeren bir sınır grubuyla ilişkili bir site bulamazsa ve hiyerarşide bir geri dönüş sitesi yoksa, istemci bir siteye atanabilene kadar 10 dakikada bir yeniden dener.  

 Configuration Manager istemci bilgisayarları aşağıdakilerden biri uygulandıklarında otomatik olarak bir siteye atanamaz ve bu koşulların el ile atanması gerekir:  

-   Şu anda bir siteye atanmışlarsa.  

-   İnternette isteler veya yalnızca İnternet istemcileri olarak yapılandırılmışlarsa.  

-   Ağ konumları, Configuration Manager hiyerarşisinde yapılandırılmış sınır gruplarının biri içine düşmüyorsa ve hiyerarşi için bir geri dönüş sitesi yoksa.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Site Uyumluluğunu Kontrol Ederek Site Atamasını Tamamlama  
 İstemci atanmış sitesini bulduktan sonra, istemcinin sürümü ve işletim sistemi, bir Configuration Manager sitesinin yönetebilmek için denetlenir. Örneğin, Configuration Manager Configuration Manager 2007 istemcisini, System Center 2012 Configuration Manager istemcilerini veya Windows 2000 çalıştıran istemcileri yönetemez.  

 Windows 2000 çalıştıran bir istemciyi Configuration Manager sitesine atarsanız site ataması başarısız olur. Bir Configuration Manager 2007 istemcisi veya bir System Center 2012 Configuration Manager istemcisini Configuration Manager (geçerli dal) sitesine atadığınızda, site ataması otomatik istemci yükseltmesini desteklemede başarılı olur. Ancak, eski nesil istemciler Configuration Manager (geçerli dal) istemcisine yükseltilene kadar Configuration Manager istemci ayarları, uygulamalar veya yazılım güncelleştirmeleri kullanarak bu istemciyi yönetemez.  

> [!NOTE]  
>  Bir Configuration Manager 2007 veya bir System Center 2012 Configuration Manager istemcisinin site atamasını Configuration Manager (geçerli dal) sitesine desteklemek için, hiyerarşi için otomatik istemci yükseltmesini yapılandırmanız gerekir. Daha fazla bilgi için bkz. [Windows bilgisayarları için istemcileri yükseltme](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Configuration Manager ayrıca, Configuration Manager (geçerli dal) istemcisini onu destekleyen bir siteye atadığınızdan da kontrol eder. Önceki Configuration Manager sürümlerinden geçiş sırasında aşağıdaki senaryolar meydana gelebilir.  

- Senaryo: otomatik site atamasını kullandınız ve sınırlarınız Configuration Manager önceki bir sürümünde tanımlananlarla örtüşüyor.  

   Bu durumda, istemci otomatik olarak bir Configuration Manager (geçerli dal) sitesi bulmaya çalışır.  

   İstemci önce Active Directory Domain Services denetler ve yayımlanmış bir Configuration Manager (geçerli dal) sitesi bulursa, site ataması başarılı olur. Bu başarısız olursa (örneğin, Configuration Manager site yayınlanmamışsa veya bilgisayar bir çalışma grubu istemcuysa), istemci daha sonra atanan yönetim noktasından site bilgilerini denetler.  

  > [!NOTE]  
  >  İstemci yüklemesi sırasında, **SMSMP =&lt;SERVER_NAME>** Client. msi özelliğini kullanarak istemciye bir yönetim noktası atayabilirsiniz.  

   Bu yöntemlerin ikisi de başarısız olursa, site ataması başarısız olur ve istemciyi el ile atamanız gerekir.  

- Senaryo: Configuration Manager (geçerli dal) istemcisini otomatik site ataması yerine belirli bir site kodu kullanarak atadınız ve yanlışlıkla System Center 2012 R2 Configuration Manager 'den önceki bir Configuration Manager sürümü için bir site kodu belirttiniz.  

   Bu durumda, site ataması başarısız olur ve istemciyi el ile bir Configuration Manager (geçerli dal) sitesine yeniden atamanız gerekir.  

  Site uyumluluk denetimi için aşağıdaki koşulların biri gerekir:  

- İstemci, Active Directory Etki Alanı Hizmetleri'ne yayımlanan site bilgilerine erişebilmelidir.  

- İstemci sitedeki bir yönetim noktasıyla iletişim kurabilmelidir.  

  Site uyumluluğu denetimi başarılı bir şekilde tamamlanamazsa, site ataması başarısız olur ve site uyumluluk denetimi yeniden çalışmaya ve başarılı olana kadar istemci yönetilmeyen halde kalır.  

  Site uyumluluk denetimini gerçekleştirmenin istisnası, istemci bir İnternet tabanlı yönetim noktası için yapılandırıldığında gerçekleşir. Bu durumda, site uyumluluk denetimi yapılmaz. İstemcileri İnternet tabanlı site sistemleri içeren bir siteye atıyorsanız ve İnternet tabanlı bir yönetim noktası belirlerseniz, istemciyi doğru siteye atadığınızdan emin olun. İstemcisini yanlışlıkla bir Configuration Manager 2007 sitesine, System Center 2012 Configuration Manager sitesine veya Internet tabanlı site sistem rollerine sahip olmayan bir Configuration Manager sitesine atarsanız, istemci yönetilecektir.  

##  <a name="locating-management-points"></a>Yönetim Noktalarını Bulma  
 Bir istemci bir siteye başarılı şekilde atandıktan sonra, sitede bir yönetim noktası bulur.  

 İstemci bilgisayarları, sitede bağlandıkları yönetim noktalarının bir listesini indirir. Bu durum, istemci her yeniden başlatıldığında veya 25 saatte bir veya istemci, bilgisayarın bağlantısı kesildiğinde veya ağ üzerinde yeniden bağlandığında veya yeni bir IP adresi alırsa oluşur. Listede, intranetteki yönetim noktaları ve HTTP veya HTTPS üzerinden istemci bağlantıları kabul edip etmedikleri yer alır. İstemci bilgisayar Internet üzerinde olduğunda ve istemcide henüz bir yönetim noktaları listesi yoksa, yönetim noktalarının bir listesini almak için belirtilen Internet tabanlı yönetim noktasına bağlanır. İstemcide, atanmış sitesi için bir yönetim noktaları listesi olduğunda, bağlanmak üzere birini seçer:  

-   İstemci intranette olduğunda ve kullanabileceği geçerli bir PKI sertifikası bulunduğunda, istemci HTTP yönetim noktalarından önce HTTPS yönetim noktalarını seçer. Ardından, orman üyeliğine göre en yakın yönetim noktasını bulur.  

-   İstemci Internet üzerinde olduğunda, Internet tabanlı yönetim noktalarından birini rastgele seçer.  

Configuration Manager tarafından kaydedilen mobil aygıt istemcileri, atandığı sitelerde yalnızca bir yönetim noktasına bağlanır ve ikincil sitelerdeki yönetim noktalarına hiçbir şekilde bağlanmazlar. Bu istemciler daima HTTPS üzerinden bağlanır ve yönetim noktasının, İnternet üzerinde istemci bağlantılarını kabul etmek üzere yapılandırılması gerekir. Birincil sitede mobil aygıt istemcileri için birden çok yönetim noktası olduğunda, Configuration Manager atama sırasında bu yönetim noktalarından birini rastgele seçer ve mobil aygıt istemcisi aynı yönetim noktasını kullanmaya devam eder.  

İstemci, sitedeki bir yönetim noktasından istemci ilkesini indirdikten sonra, istemci yönetilen bir istemci olur.  

##  <a name="downloading-site-settings"></a>Site Ayarlarını İndirme  
 Site ataması başarılı olduktan ve istemci bir yönetim noktası bulduktan sonra, site uyumluluk denetimi için Active Directory Etki Alanı Hizmetleri'ni kullanan bir istemci bilgisayarı, atanmış sitesi için istemciyle ilgili site ayarlarını indirir. Bu ayarlar, istemci sertifika seçim kriterleri, bir sertifika iptal listesi kullanılıp kullanılmayacağı ve istemcinin istediği bağlantı noktası numaralarını içerir. İstemci bu ayarları düzenli aralıklarla denetlemeye devam eder.  

 İstemci bilgisayarları Active Directory Etki Alanı Hizmetleri'nden site ayarlarını alamadığında, bunları kendi yönetim noktalarından indirirler. İstemci bilgisayarlar ayrıca, istemci gönderimi kullanılarak yüklendiklerinde site ayarlarını edinebilir veya CCMSetup. exe ve istemci yükleme özelliklerini kullanarak el ile belirtebilirsiniz. İstemci yükleme özellikleri hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>İstemci Ayarlarını İndirme  
 Tüm istemciler, varsayılan istemci ayarları ilkesini ve herhangi bir geçerli özel istemci ayarları ilkesini indirir. Yazılım Merkezi, Windows bilgisayarları için bu istemci yapılandırma ilkelerine güvenir ve kullanıcılara, Yazılım Merkezi'nin bu yapılandırma bilgisi indirilene kadar başarılı bir şekilde çalıştırılamayacağı bilgisini verir. Yapılandırılan istemci ayarlarına bağlı olarak, istemci ayarlarının ilk indirmesi biraz vakit alabilir ve bu işlem tamamlanana kadar bazı istemci yönetimi görevleri çalışmayabilir.  

##  <a name="verifying-site-assignment"></a>Site Atamasını Doğrulama  
 Aşağıdaki yöntemlerin herhangi biriyle, site ataması başarısını doğrulayabilirsiniz:  

-   Windows bilgisayarlarındaki istemciler için Denetim Masası 'nda Configuration Manager ' yi kullanın ve site kodunun **site** sekmesinde doğru şekilde görüntülendiğini doğrulayın.  

-   İstemci bilgisayarlar için, **varlıklar ve uyum** çalışma alanı > **cihazlar** düğümünde, bilgisayarın **istemci** sütunu Için **Evet** ' i, **site kodu** sütunu için ise doğru birincil site kodunu görüntülediğini doğrulayın.  

-   Mobil cihaz istemcilerinde mobil cihazın **İstemci** sütunu için **Evet** ’i, **Site Kodu** sütunu için ise doğru birincil site kodunu görüntülediğini doğrulamak üzere **Varlıklar ve Uyum** çalışma alanındaki **Tüm Mobil Cihazlar** koleksiyonunu kullanın.  

-   İstemci ataması ve mobil aygıt kaydı için raporları kullanın.  

-   İstemci bilgisayarları için istemcideki LocationServices.log dosyasını kullanın.  

##  <a name="roaming-to-other-sites"></a>Başka Sitelere Gezinme  
 Intranetteki istemci bilgisayarları birincil siteye atanmışsa ancak başka bir site için yapılandırılan sınır grubunda yer alması için ağ konumu değiştirilirse, başka bir siteye dolaşır. Atanmış siteleri ikincil bir siteyse istemciler, istemci ilkesini indirmek ve istemci verilerini yüklemek için ikincil sitedeki bir yönetim noktasını kullanabilir, böylece bu verilerin olası bir yavaş ağ üzerinden gönderilmesi engellenir. Ancak, atanan sitelerinin alt sitesi olmayan bir diğer birincil veya ikincil sitenin sınırları içinde dolaşırsa bu istemciler, istemci ilkesini indirmek ve sitelerine verileri yüklemek için atanmış sitelerinde her zaman bir yönetim noktası kullanırlar.  

 Diğer sitelere (tüm birincil ve ikincil siteler) dolaşan bu istemci bilgisayarları, içerik konum istekleri için diğer sitelerde her zaman yönetim noktalarını kullanabilir. Geçerli sitedeki yönetim noktaları, istemcilerin istediği içeriğe sahip olan dağıtım noktalarının bir listesini istemcilere verebilir.  

 Yalnızca Internet istemci yönetimi için yapılandırılan istemci bilgisayarlar ve Configuration Manager tarafından kaydedilen mobil cihazlar ve Mac bilgisayarlar için, bu istemciler yalnızca atanmış sitelerindeki yönetim noktalarıyla iletişim kurar. Bu istemciler, ikincil sitelerdeki veya diğer birincil sitelerdeki yönetim noktalarıyla asla iletişim kurmaz.  
