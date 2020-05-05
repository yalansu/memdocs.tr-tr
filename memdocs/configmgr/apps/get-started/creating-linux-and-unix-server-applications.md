---
title: Linux ve UNIX sunucu uygulamaları oluşturma
titleSuffix: Configuration Manager
description: Linux ve UNIX cihazları için uygulama oluştururken ve dağıtırken dikkate almanız gereken önemli noktalar bölümüne bakın.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3f5d0cfb930e6d1b8cf4cd6dfb0eabfa38ddab16
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075804"
---
# <a name="create-linux-and-unix-server-applications-with-configuration-manager"></a>Configuration Manager ile Linux ve UNIX sunucu uygulamaları oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez. 
> 
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

Linux ve UNIX çalıştıran bilgisayarlar için uygulama oluştururken ve dağıtırken aşağıdaki noktaları dikkate alın.  

## <a name="general-considerations"></a>Dikkat edilmesi gereken temel noktalar  
 Linux ve UNIX için Configuration Manager istemcisi, **paketler ve programlar kullanan yazılım dağıtımlarını**destekler. Configuration Manager uygulamalarını Linux ve UNIX çalıştıran bilgisayarlara dağıtamazsınız.  

 Linux ve UNIX yazılım dağıtımının özellikleri şunlardır:  

-   Linux ve UNIX sunucuları için yazılım yüklemesi, aşağıdaki özellikleri de dahil:  

    -   Yeni yazılım dağıtımı  

    -   Zaten bir bilgisayarda olan programlar için yazılım güncelleştirmeleri  

    -   İşletim sistemi düzeltme ekleri  

-   Yerel Linux ve UNIX komutları ve Linux ve UNIX sunucularında bulunan betikler  

-   **Yalnızca belirtilen istemci platformlarında** program seçeneğini belirlediğinizde belirttiğiniz işletim sistemleriyle sınırlı olan dağıtımlar

-   Yazılımın ne zaman yüklenmediği denetlemek için bakım pencereleri

-   Dağıtımları izlemek için dağıtım durum iletileri  

-   İstemci, bir dağıtım noktasından yazılım indirirken ağ kullanımını kısıtlama seçeneği  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Linux ve UNIX bilgisayarlara dağıtma ve Windows cihazlarına dağıtma arasındaki farklar
Linux ve UNIX bilgisayarlara paket ve program dağıtma ile Windows cihazlarına paket ve program dağıtma arasındaki temel farklılıklar şunlardır:  

|Yapılandırma|Ayrıntılar|  
|-------------------|-------------|  
|Yalnızca bilgisayarlara yönelik olan konfigürasyonları kullanın ve kullanıcılara yönelik olan konfigürasyonları kullanmayın.|Linux ve UNIX için Configuration Manager istemcisi, kullanıcılara yönelik olan konfigürasyonları desteklemez.|  
|Programları dağıtım noktasından yazılım indirmek için yapılandırın ve programları yerel istemci önbelleğinden çalıştırın.|Linux ve UNIX için Configuration Manager istemcisi, yazılımın dağıtım noktasından çalıştırılmasını desteklemez. Bunun yerine, yazılımı istemciye indirmek için yapılandırmanız ve sonra yüklenmesi gerekir.<br /><br /> Varsayılan olarak, Linux ve UNIX için istemcisi yazılım yükledikten sonra, o yazılım istemcinin önbelleğinden silinir. Ancak, **istemci önbelleğinde Içeriği devam** ettir ile yapılandırılan paketler, istemciden silinmez ve yazılım yüklendikten sonra istemcinin önbelleğinde kalır.<br /><br /> Linux ve UNIX için istemcisi istemci önbelleğinin yapılandırmasını desteklemez ve istemci önbelleğinin en büyük boyutu yalnızca istemci bilgisayardaki boş disk alanı ile sınırlıdır.|  
|Ağ Erişim Hesabı'nı dağıtım noktası erişimi için yapılandırın|Linux ve UNIX bilgisayarlar, çalışma grubu bilgisayarları olmak üzere tasarlanmıştır. Configuration Manager site sunucusu etki alanındaki dağıtım noktasından paketlere erişmek için, site için ağ erişim hesabı 'nı yapılandırmanız gerekir. Bu hesabı, bir yazılım dağıtım bileşeni özelliği olarak belirtmeniz ve yazılımı dağıtmadan önce hesabı yapılandırmanız gerekir.<br /><br /> Her sitede birden çok Ağ Erişim Hesabı yapılandırabilirsiniz. Linux ve UNIX için istemci, yapılandırdığınız bu hesapların her birini bir Ağ Erişim Hesabı olarak kullanabilir.<br /><br /> Daha fazla bilgi için bkz. [Configuration Manager Için site bileşenleri](../../core/servers/deploy/configure/site-components.md).|  

 Paketler ve programları, yalnızca Linux veya UNIX istemcileri içeren koleksiyonlara dağıtabilir veya onları, **Tüm Sistemler Koleksiyonu**gibi, istemci türlerinin bir karışımını içeren koleksiyonlara dağıtabilirsiniz. Ancak, Linux olmayan ve UNIX olmayan istemciler yazılımı veya rapor hatasını yüklemez.  

 Linux ve UNIX için Configuration Manager istemcisi bir dağıtım aldığında ve çalıştırdığında, durum mesajları oluşturur. Bu durum iletilerini Configuration Manager konsolunda görüntüleyebilir veya dağıtım durumunu izlemek üzere raporlar kullanarak görüntüleyebilirsiniz.  

 Paket ve programları kullanma hakkında daha fazla bilgi için bkz. [paket ve programlar](../../apps/deploy-use/packages-and-programs.md).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Linux ve UNIX sunucuları için paket, program ve dağıtımları yapılandırma  
 Configuration Manager konsolundaki kullanılabilir varsayılan seçenekleri kullanarak paketler ve programlar oluşturabilir ve dağıtabilirsiniz. İstemci herhangi bir benzersiz yapılandırma gerektirmez.  

 Paketleri ve programları ve dağıtımları yapılandırmak için aşağıdaki bölümlerdeki bilgileri kullanın.  

### <a name="packages-and-programs"></a>Paketler ve programlar  
 Bir Linux veya UNIX sunucusu için bir paket ve program oluşturmak için, Configuration Manager konsolundan **paket ve program oluşturma Sihirbazı** ' nı kullanın. Linux ve UNIX için istemci, çoğu paket ve program ayarını destekler. Ancak, çeşitli ayarlar desteklenmez. Bir paket ve program oluşturduğunuzda veya yapılandırdığınızda, aşağıdaki noktaları göz önünde bulundurun:  

-   Hedef bilgisayarların desteklediği dosya türlerini dahil edin.  

-   Hedef bilgisayarda kullanım için uygun olan komut satırlarını tanımlayın.  

-   Kullanıcılarla etkileşime geçen ayarların desteklenmediğini aklınızda bulundurun.  

Aşağıdaki tabloda, desteklenmeyen paketler ve programlar için özellikler listelenmektedir:  

|Paket ve program özelliği|Davranış|Daha fazla bilgi|  
|----------------------------------|--------------|----------------------|  
|Paket paylaşım ayarları:<br /><br /> -Tüm seçenekler|Bir hata oluşturulur ve yazılım yüklemesi başarısız olur|İstemci bu yapılandırmayı desteklemiyor. Bunun yerine, istemcinin, yazılımı HTTP veya HTTPS kullanarak indirmesi ve ardından komut satırını bunun yerel önbelleğinden çalıştırması gerekir.|  
|Paket güncelleştirme ayarları:<br /><br /> -Kullanıcıların dağıtım noktalarından bağlantısını kesme|Ayarlar yok sayılır|İstemci bu yapılandırmayı desteklemiyor.|  
|İşletim sistemi dağıtım ayarları:<br /><br /> -Tüm seçenekler|Ayarlar yok sayılır|İstemci bu yapılandırmayı desteklemiyor.|  
|Raporlama:<br /><br /> -Durum MIF eşleme için paket özelliklerini kullanın<br /><br /> -Bu alanları durum MIF eşlemesi için kullanın|Ayarlar yok sayılır|İstemci, durum MIF dosyalarının kullanılmasını desteklememektedir.|  
|Şunu **Çalıştır**:<br /><br /> -Tüm seçenekler|Ayarlar yok sayılır|İstemci daima kullanıcı arabirimi olmayan paketler çalıştırıyor.<br /><br /> İstemci Çalıştırma için tüm yapılandırma ayarlarını yok sayıyor.|  
|Çalıştırma sonrasında:<br /><br />-Configuration Manager bilgisayarı yeniden başlatır<br /><br /> -Program denetimleri yeniden başlatılır<br /><br /> -Configuration Manager Kullanıcı oturumunu kapatır|Bir hata oluşturulur ve yazılım yüklemesi başarısız olur|Sistem yeniden başlatma ayarı ve kullanıcıya özel ayarlar desteklenmez.<br /><br /> **Eylem gerekli değil** ayarı dışındaki herhangi bir ayar kullanımda olduğunda, istemci bir hata oluşturur ve yazılım yüklemesini bir eylem yapılmadan devam ettirir.|  
|Program çalışabilir:<br /><br /> -Yalnızca bir Kullanıcı oturum açmışsa|Bir hata oluşturulur ve yazılım yüklemesi başarısız olur|Kullanıcıya özel ayarlar desteklenmez.<br /><br /> Bu seçenek yapılandırıldığında, istemci bir hata oluşturur ve yazılımı yükleyemez.<br /><br /> Diğer seçenekler yok sayılır ve yazılım yüklemesi devam eder.|  
|Çalıştırma modu:<br /><br /> -Kullanıcının haklarıyla Çalıştır|Ayarlar yok sayılır|Kullanıcıya özel ayarlar desteklenmez.<br /><br /> Ancak istemci, yönetici haklarıyla çalışan yapılandırmayı destekler.<br /><br /> **Yönetici haklarıyla Çalıştır**belirttiğinizde Configuration Manager istemcisi kök kimlik bilgilerini kullanır.<br /><br /> Bu ayar bir hata veya günlük girişi oluşturmaz. Bunun yerine, istemci **programın** = önkoşul yapılandırması için bir hata oluşturduğunda yazılım yüklemesi başarısız olur ve**yalnızca bir Kullanıcı oturum açtığınızda**çalıştırılabilir.|  
|Kullanıcıların program yüklemesini görüntülemesine ve etkileşime girmesine izin ver|Ayarlar yok sayılır|Kullanıcıya özel ayarlar desteklenmez.<br /><br /> Bu yapılandırma yok sayılır ve yazılım yüklemesi devam eder.|  
|Sürücü modu:<br /><br /> -Tüm seçenekler|Ayarlar yok sayılır|İçerik istemciye her zaman indirilip yerel olarak çalıştırıldığı için bu ayar desteklenmez.|  
|Önce başka bir program çalıştır|Bir hata oluşturulur ve yazılım yüklemesi başarısız olur|Yinelemeli program yüklemesi desteklenmez.<br /><br /> Bir program, önce başka bir programı çalıştıracak şekilde yapılandırıldığında, yazılım yüklemesi başarısız olur ve diğer program yüklemesi başlatılmaz.|  
|Bu program bir bilgisayara atandığında:<br /><br /> -Oturum açan her kullanıcı için bir kez çalıştır|Ayarlar yok sayılır|Kullanıcıya özel ayarlar desteklenmez.<br /><br /> Ancak, istemci, bilgisayar için bir kez çalıştırılan yapılandırmayı destekler.<br /><br /> Bu ayar bir hata veya günlük girişi oluşturmaz çünkü programın önkoşul yapılandırması için zaten**bir Kullanıcı oturum açtığında** **çalıştırılabilir** = .|  
|Program bildirimlerini gösterme|Ayarlar yok sayılır|İstemci bir kullanıcı arabirimi uygulamaz.<br /><br /> Bu yapılandırma seçildiğinde, yok sayılır ve yazılım yüklemesi devam eder.|  
|Bu programı dağıtıldığı bilgisayarlarda devre dışı bırak|Ayarlar yok sayılır|Bu ayar desteklenmez ve yazılımın yüklenmesini etkilemez.|  
|Bu programın dağıtılmadan paket yükleme görev sırasından yüklenmesine izin ver||İstemci görev dizilerini desteklemez.<br /><br /> Bu ayar desteklenmez ve yazılımın yüklenmesini etkilemez.|  
|Windows Installer:<br /><br /> -Tüm seçenekler|Ayarlar yok sayılır|İstemci Windows Installer dosyalarını veya ayarlarını desteklemez.|  
|OpsMgr Bakım Modu:<br /><br /> -Tüm seçenekler|Ayarlar yok sayılır|İstemci bu yapılandırmayı desteklemiyor.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Linux veya UNIX sunucusuna yazılım dağıtma
 Bir Linux veya UNIX sunucusuna bir paket ve program kullanarak yazılım dağıtmak için, Configuration Manager konsolundan **Yazılım Dağıtma Sihirbazı** ' nı kullanabilirsiniz. Çoğu dağıtım ayarı, Linux ve UNIX için istemcisi tarafından desteklenir. Ancak çeşitli ayarlar desteklenmez. Yazılım dağıttığınızda, aşağıdaki noktaları göz önünde bulundurun:  

- Paketi, içerik konumu için yapılandırılan bir sınır grubuyla ilişkilendirilmiş en az bir dağıtım noktasına sağlayın.  

- Bu dağıtımı alan Linux ve UNIX için istemci, ağ konumundan bu dağıtım noktasına erişebilmelidir.  

- Linux ve UNIX için istemci, paketi dağıtım noktasından indirir ve programı yerel bilgisayarda çalıştırır.  

- Linux ve UNIX için istemcisi, Paylaşılan klasörlerden paket indiremez. HTTP veya HTTPS destekleyen IIS özellikli dağıtım noktalarından paketleri indirir.  

  Aşağıdaki tabloda, desteklenmeyen dağıtımlar için özellikler listelenmektedir:  

|Dağıtım özelliği|Davranış|Daha fazla bilgi|  
|-------------------------|--------------|----------------------|  
|Dağıtım ayarları - amaç:<br /><br /> -Kullanılabilir<br /><br /> -Gerekli|Ayarlar yok sayılır|Kullanıcıya özel ayarlar desteklenmez.<br /><br /> Ancak istemci, zamanlanmış yükleme süresini zorlayan, ancak bu zamanlanan zamandan önce el ile yüklemeyi desteklemeyen **gerekli**ayarı destekler.|  
|Uyanma paketleri gönderme|Ayarlar yok sayılır|İstemci bu yapılandırmayı desteklemiyor.|  
|Atama zamanlaması:<br /><br /> -oturum aç<br /><br /> -Oturumu Kapat|Bir hata oluşturulur ve yazılım yüklemesi başarısız olur|Kullanıcıya özel ayarlar desteklenmez.<br /><br /> Ancak, istemci **Olabildiğince çabuk**ayarını destekler.|  
|Bildirim ayarları:<br /><br /> -Kullanıcıların programı atamalardan bağımsız olarak çalıştırmasına izin ver|Ayarlar yok sayılır|İstemci bir kullanıcı arabirimi uygulamaz.|  
|Zamanlanan atama süresine ulaşıldığında, bakım penceresinin dışında aşağıdaki etkinliğin gerçekleştirilmesine izin ver:<br /><br /> -Sistem yeniden başlatma (yükleme işlemini gerçekleştirmek için gerekliyse)|Bir hata oluşturulur|İstemci sistemin yeniden başlatılmasını desteklemez.|  
|Hızlı (LAN) ağlar için dağıtım seçeneği:<br /><br /> -Programı dağıtım noktasından Çalıştır|Bir hata oluşturulur ve yazılım yüklemesi başarısız olur|İstemci dağıtım noktasından yazılım çalıştıramıyor, bunun yerine çalıştırılmadan önce programı indirmesi gerekir.|  
|Yavaş veya güvenilir olmayan bir ağ sınırı veya içerik için bir geri dönüş kaynak konumu için dağıtım seçeneği:<br /><br /> -İstemcilerin aynı alt ağdaki diğer istemcilerle içerik paylaşmasına izin ver|Ayarlar yok sayılır|İstemci, eşler arasında içerik paylaşımını desteklemez.|  

 İçerik konumu hakkında daha fazla bilgi için bkz. [Configuration Manager içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Dağıtım oluşturma hakkında daha fazla bilgi için bkz. [uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a> Dağıtım noktalarından yazılım indirme işlemleri için ağ bant genişliğini yönetme  
 Linux ve UNIX istemcisi, bir dağıtım noktasından yazılım indirirken ağ bant genişliği denetimlerini destekler.  

 İstemci, Configuration Manager istemci ayarları olarak yapılandırdığınız arka plan Akıllı Aktarım (BITS) ayarlarını kullanır, ancak BITS uygulamaz. Bunun yerine, ağ bant genişlinin kullanımını kısıtlamak için, istemci yazılım indirmesi için HTTP isteği öbek boyutunu ve öbekler arası gecikmeyi denetler.  

 Bir istemciyi, ağ bant genişliği denetimleri kullanmak üzere yapılandırmak için, istemci ayarları **Arka Plan Akıllı Aktarım** için yapılandırılır ve ardından ayarlar istemci bilgisayarına uygulanır. Bant genişliği denetimleri kullanmak için, istemcinin, aşağıdaki ayarlarla, **Evet**olarak yapılandırıldığında **arka plan Akıllı Aktarım** için istemci ayarları alması gerekir:  

- **BITS arka plan aktarımları için maksimum ağ bant genişliğini sınırlayın**  

  İstemci, Arka Plan Akıllı Aktarım için aşağıdaki yapılandırmaları destekler:  

  -   **Daraltma penceresi başlangıç zamanı**  

  -   **Daraltma penceresi bitiş zamanı**  

  -   **Daraltma penceresinde en çok aktarım hızı (Kbps)**  

  -   **Daraltma penceresi dışındaki en fazla aktarım hızı (Kbps)**  

Arka Plan Akıllı Aktarım için aşağıdaki yapılandırma desteklenmez ve Linux ve UNIX için istemci tarafından yok sayılır.  

- **Daraltma penceresi dışında BITS indirmelerine izin ver**  

  Yazılımın bir dağıtım noktasından istemciye indirilmesi kesintiye uğrarsa, Linux ve UNIX için istemci indirme işlemini sürdürmez. Bunun yerine, tüm yazılım paketinin indirilmesini yeniden başlatır.  

##  <a name="configure-operations-for-software-deployments"></a>Yazılım dağıtımları için işlemleri yapılandırma  
 Windows istemcisine benzer şekilde, Linux ve UNIX için Configuration Manager istemcisi, yeni ilkeyi yokladığında ve denetlediğinde yeni yazılım dağıtımlarını bulur. İstemcinin yeni ilke denetimi yaptığı sıklık, istemci ayarlarına bağlıdır. Bakım pencerelerini, yazılım dağıtımlarının ne zaman gerçekleşeceğini denetlemek üzere yapılandırabilirsiniz.  

 Linux ve UNIS sunucularına yazılım dağıtımlarını, paket özellikleri, program özellikleri ve dağıtım özelliklerini kullanarak yapılandırabilirsiniz.  

 İstemci bir dağıtım için ilke aldığında, bir durum mesajı gönderir. Ayrıca, yazılım yüklemesini başlattığında ve yükleme tamamlandığında veya başarısız olduğunda durum iletileri gönderir.  

 Yazılım dağıtımları için programlar, Linux ve UNIX için Configuration Manager istemcisinin birlikte çalıştığı kök kimlik bilgileriyle çalışır. Program komutunun çıkış kodu, başarı veya başarısızlığı belirlemek için kullanılır. 0 (sıfır) çıkış kodu, başarı olarak kabul edilir. Ek olarak, **stdout** (standart çıktı akışı) ve **stderr** (standart hata akışı), günlük düzeyi BİLGİ veya İZ olarak ayarlandığında günlük dosyasına kopyalanır.  

> [!TIP]  
>  Dağıtmak istediğiniz yazılım, Linux veya UNIX sunucusunun erişebileceği bir Ağ Dosya Sistemi (NFS) paylaşımında bulunuyorsa, paketi indirmek için bir dağıtım noktası kullanmanız gerekmez. Bunun yerine, paketi oluşturduğunuzda, **Bu paket, kaynak dosyaları içerir**onay kutusunu seçmeyin. Ardından, programı yapılandırdığınızda, NFS bağlama noktasındaki pakete doğrudan erişmek için uygun komut satırını belirtin.  
