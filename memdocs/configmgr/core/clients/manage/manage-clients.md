---
title: İstemcileri yönetme
titleSuffix: Configuration Manager
description: Configuration Manager istemcileri yönetmeyi öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b9111e3be82424425561e0a664fee955d73ee63
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270829"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Configuration Manager istemcileri yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcisi bir cihaza yüklediğinde ve bir siteye başarıyla atandığında, cihazı **cihazlar** düğümündeki **varlıklar ve uyum** çalışma alanında ve **Cihaz Koleksiyonları** düğümündeki bir veya daha fazla koleksiyonda görürsünüz. Cihazı veya koleksiyonu seçin ve sonra yönetim işlemlerini çalıştırın. Ancak, istemciyi yönetmenin başka yolları da vardır. Bu, konsolundaki diğer çalışma alanlarını veya konsolun dışındaki görevleri içerebilir.  

> [!NOTE]  
> Configuration Manager istemcisini yüklerseniz, ancak henüz bir siteye başarıyla atanmamışsa, konsolunda görünmeyebilir. İstemci bir siteye eklendikten sonra, koleksiyon üyeliğini güncelleştirin ve ardından konsol görünümünü yenileyin.  
>
> Configuration Manager istemcisi yüklenmediği zaman da cihaz konsolda görüntülenebilir. Bu davranış, site bir cihazı tespit eder ancak istemci yüklenip atanmamışsa oluşur.
>
> [Exchange Server Bağlayıcısı](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) veya [Şirket içi MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) ile yönetilen mobil cihazlar Configuration Manager istemcisini yüklemez.  
>
> Bir cihazı konsolundan yönetmek için, istemcinin yüklenip yüklenmediğini öğrenmek için **cihazlar** düğümündeki **istemci** sütununu kullanın.  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a>İstemcileri **cihazlar** düğümünden yönetme  

Cihaz türüne bağlı olarak, bu seçeneklerden bazısı kullanılamayabilir.  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin.  

2. Bir veya daha fazla cihaz seçin ve ardından şeritten bu istemci yönetim görevlerinden birini seçin. Ayrıca, cihaza sağ tıklayabilirsiniz.)  

### <a name="import-user-device-affinity"></a>Kullanıcı cihaz benzeşimini içeri aktar

Kullanıcılara etkin bir şekilde yazılım dağıtabilmeniz için kullanıcılar ve cihazlar arasındaki ilişkilendirmeleri yapılandırın.  

Daha fazla bilgi için bkz. [kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi Ile bağlama](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="import-computer-information"></a>Bilgisayar bilgilerini içeri aktar

Yeni bilgisayar bilgilerini Configuration Manager veritabanına aktarmak için **bilgisayar bilgilerini Içeri aktarma Sihirbazı 'nı** başlatın. Bir dosya kullanarak birden çok bilgisayarı içeri aktarabilir veya tek bir bilgisayar için bilgileri belirtebilirsiniz.

### <a name="add-selected-items"></a>Seçili öğeleri ekle

Aşağıdaki seçenekleri sağlar:

- **Seçili öğeleri mevcut cihaz koleksiyonuna Ekle**: **Koleksiyon Seç** iletişim kutusunu açar. Bu cihazı eklemek istediğiniz koleksiyonu seçin. Cihaz, **doğrudan** üyelik kuralı kullanılarak bu koleksiyona dahil edilir.  

- **Seçili öğeleri yeni cihaz koleksiyonuna Ekle**: yeni bir koleksiyon oluşturabileceğiniz **cihaz koleksiyonu oluşturma Sihirbazı** ' nı açar. Seçilen koleksiyon, **doğrudan** üyelik kuralı kullanılarak bu koleksiyona dahil edilir.  

Daha fazla bilgi için bkz. [koleksiyonlar oluşturma](collections/create-collections.md).

### <a name="install-client"></a>İstemci yüklemesi

**Istemci yüklemesi Sihirbazı**' nı açar. Bu sihirbaz, seçilen cihaza Configuration Manager istemcisini yüklemek veya yeniden yüklemek için Client Push yüklemesini kullanır.

> [!TIP]  
> Configuration Manager istemcisini yüklemenin birçok farklı yolu vardır. Istemci Gönderme Sihirbazı konsolundan uygun bir istemci yükleme yöntemi sunmakla birlikte, bu yöntemin birçok bağımlılığı vardır ve tüm ortamlar için uygun değildir. Bağımlılıklar hakkında daha fazla bilgi için bkz. [Windows bilgisayarlarına istemci dağıtmak Için Önkoşullar](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation). Diğer istemci yükleme yöntemleri hakkında daha fazla bilgi için bkz. [istemci yükleme yöntemleri](../deploy/plan/client-installation-methods.md).

Daha fazla bilgi için bkz. [Client Push kullanarak Configuration Manager istemcileri yükleme](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

### <a name="run-script"></a>Betik çalıştırma

Seçili cihazda bir PowerShell Betiği çalıştırmak için **Betiği Çalıştır** sihirbazını açar.

Daha fazla bilgi için bkz. [PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="install-application"></a>Uygulamayı yükler

Bir cihaza gerçek zamanlı bir uygulama yüklemek. Bu özellik, her uygulama için ayrı koleksiyonlar gereksinimini azaltmaya yardımcı olabilir.

Daha fazla bilgi için bkz. [cihaz için uygulama yüklemesi](../../../apps/deploy-use/install-app-for-device.md).

### <a name="reassign-site"></a>Siteyi yeniden ata

Yönetilen mobil cihazlar dahil olmak üzere bir veya daha fazla istemciyi hiyerarşideki başka bir birincil siteye yeniden atayın. İstemcileri ayrı ayrı yeniden atayabilir veya toplu olarak yeniden atamak için birden fazla seçim yapabilirsiniz.  

### <a name="client-settings---resultant-client-settings"></a>İstemci ayarları-sonuç istemci ayarları

Aynı cihaza birden çok istemci ayarı dağıttığınızda, ayarların önceliklendirmesi ve bileşimi karmaşıktır. Bu cihaza dağıtılan istemci ayarları sonuç kümesini görüntülemek için bu seçeneği kullanın.

Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../deploy/configure-client-settings.md).

### <a name="start"></a>Başlangıç

- Donanım ve yazılım envanteri bilgilerini bir Windows istemcisinden görmek için **Kaynak Gezgini** çalıştırın. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

  - [Donanım envanterini görüntülemek için Kaynak Gezgini’ni kullanma](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [Yazılım envanterini görüntülemek için Kaynak Gezgini’ni kullanma](inventory/use-resource-explorer-to-view-software-inventory.md)

- **Uzaktan denetim**, **Uzaktan Yardım**veya **Uzak Masaüstü istemcisi**'ni kullanarak cihazı uzaktan yönetin. Daha fazla bilgi için bkz. [bir Windows istemci bilgisayarını uzaktan yönetme](remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="approve"></a>Onaylama

İstemci, HTTP ve otomatik olarak imzalanan bir sertifika kullanarak site sistemleriyle iletişim kurduğunda, bu istemcileri güvenilen bilgisayar olarak tanımlamak için onaylamanız gerekir. Varsayılan olarak, site yapılandırması istemcileri aynı Active Directory ormanı, güvenilen ormanları ve bağlı Azure Active Directory (Azure AD) kiracılarından otomatik olarak onaylar<!-- MEMDocs#318 -->. Bu varsayılan davranış, her istemciyi el ile onaylamanız gerekmediği anlamına gelir. Güvendiğiniz çalışma grubu bilgisayarlarını ve güvendiğiniz diğer onaylanmamış bilgisayarları el ile onaylayın.

> [!IMPORTANT]  
> Bazı yönetim işlevleri onaylanmamış istemciler için çalışabilse de Configuration Manager için desteklenmeyen bir senaryodur.  

HTTPS kullanarak site sistemleriyle her zaman iletişim kuran istemcileri veya site sistemleriyle HTTP kullanarak iletişim kurduklarında bir PKI sertifikası kullanan istemcileri onaylamanız gerekmez. Bu istemciler, PKI sertifikalarını kullanarak güven kurar.

### <a name="block-or-unblock"></a>Engelleme veya engellemeyi kaldırma

Artık güvenmediğiniz bir istemciyi engelleyin. Engelleme, istemcinin ilke almasını önler ve site sistemlerinin istemciyle iletişim kurmasını engeller.  

> [!IMPORTANT]  
> Bir istemciyi engellemek yalnızca istemciden Configuration Manager site sistemlerine yönelik iletişimin yapılmasını engeller. Diğer cihazlarla iletişimi engellemez. İstemci, HTTPS yerine HTTP kullanarak site sistemleriyle iletişim kurduğunda bazı güvenlik sınırlamaları vardır.  

Engellenmiş bir istemcinin engellemesini da kaldırabilirsiniz.

Daha fazla bilgi için bkz. [istemcilerin engellenip engellenmeyeceğini belirleme](../deploy/plan/determine-whether-to-block-clients.md).

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>Gerekli PXE dağıtımlarını temizle

Bir Configuration Manager koleksiyonuna veya bir bilgisayara atanan son PXE dağıtımının durumunu temizleyerek gerekli bir PXE dağıtımını yeniden dağıtabilirsiniz. Bu eylem, o dağıtımın durumunu sıfırlar ve gereken en son dağıtımları yeniden yükler.

Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

### <a name="client-notification"></a>İstemci bildirimi

Daha fazla bilgi için bkz. [istemci bildirimleri](client-notification.md#client-notification).

### <a name="endpoint-protection"></a>Uç Nokta Koruma

Daha fazla bilgi için bkz. [istemci bildirimleri](client-notification.md#endpoint-protection).

### <a name="edit-primary-users"></a>Birincil kullanıcıları Düzenle

Bu cihazın kullanıcılarını son 90 gün içinde görüntüleyin veya bu cihazın birincil kullanıcılarını belirtin.

Daha fazla bilgi için bkz. [kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi Ile bağlama](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="wipe-a-mobile-device"></a>Mobil cihazı silme

Temizle komutunu destekleyen mobil cihazları silebilirsiniz. Bu eylem, kişisel ayarlar ve kişisel veriler de dahil olmak üzere mobil cihazdaki tüm verileri kalıcı olarak kaldırır. Genellikle, bu işlem mobil cihazı fabrika ayarlarına geri döndürür. Artık güvenilir olmadığında bir mobil cihazı temizleyin. Örneğin, cihaz kaybolur veya çalınırsa.  

> [!TIP]  
> Mobil cihazın uzaktan silme komutunu nasıl işlediği hakkında daha fazla bilgi için üretici belgelerine bakın.  

Mobil cihaz silme komutunu alıncaya kadar genellikle bir gecikme vardır:  

- Mobil cihaz Configuration Manager tarafından kaydedildiyse istemci, istemci ilkesini indirdiğinde komutu alır.

- Mobil cihaz Exchange Server Bağlayıcısı tarafından yönetiliyorsa, Exchange ile eşitlendiğinde komutunu alır.  

Cihazın silme komutunu ne zaman aldığını izlemek için **silme durumu** sütununu kullanın. Cihaz Configuration Manager için bir silme bildirimi gönderene kadar silme komutunu iptal edebilirsiniz.  

### <a name="retire-a-mobile-device"></a>Mobil cihazı devre dışı bırakma

**Devre dışı bırakma** seçeneği yalnızca ŞIRKET içi MDM tarafından kaydedilen mobil cihazlar tarafından desteklenir.  

Daha fazla bilgi için bkz. [uzaktan silme, uzaktan kilitleme veya parola sıfırlama ile verilerinizin korunmasına yardımcı olma](../../../mdm/deploy-use/wipe-lock-reset-devices.md).

### <a name="change-ownership"></a>Sahipliği Değiştir

Bir cihaz etki alanına katılmamışsa ve Configuration Manager istemcisi yüklü değilse, sahipliği **Şirket** veya **Kişisel**olarak değiştirmek için bu seçeneği kullanın.  

Bu değeri, dağıtımları denetlemek ve kullanıcıların cihazlarından ne kadar envanter toplandığını denetlemek için uygulama gereksinimlerinde kullanabilirsiniz.  

Herhangi bir sütun başlığına sağ tıklayıp seçerek **cihaz sahibi** sütununu görünüme eklemeniz gerekebilir.

### <a name="delete"></a>Sil

> [!WARNING]  
> Configuration Manager istemcisini kaldırmak veya bir koleksiyondan kaldırmak istiyorsanız istemciyi silmeyin.  

**Silme** eylemi, istemci kaydını Configuration Manager veritabanından el ile kaldırır. Yalnızca bir sorunu gidermek için bu eylemi kullanın. Nesneyi silerseniz ancak istemci hala yüklenip siteyle iletişim kurduğunda, sinyal keşfi istemci kaydını yeniden oluşturur. Configuration Manager konsolunda yeniden görünür, ancak istemci geçmişi ve önceki tüm ilişkilendirmeler kaybolur.  
> [!NOTE]  
> Configuration Manager tarafından kaydedilen bir mobil cihaz istemcisini sildiğinizde, bu eylem verilen PKI sertifikasını da iptal eder. Bu sertifika, IIS sertifika iptal listesini (CRL) denetmasa bile yönetim noktası tarafından reddedilir.
>
> Eski mobil cihaz istemcilerindeki sertifikalar bu istemciler silindiğinde iptal edilmez.

İstemciyi kaldırmak için bkz. [Configuration Manager Istemcisini kaldırma](#BKMK_UninstalClient).  

İstemciyi yeni bir birincil siteye atamak için bkz. [istemcileri bir siteye atama](../deploy/assign-clients-to-a-site.md).

İstemciyi koleksiyondan kaldırmak için koleksiyon özelliklerini yeniden yapılandırın. Daha fazla bilgi için bkz. [koleksiyonları yönetme](collections/manage-collections.md).

### <a name="refresh"></a>Yenile

Veritabanında en son verilerle konsol görünümünü yenileyin. Örneğin, bir cihaz bulma listesinden görüntülenirse, ancak yüklü olarak gösterilmez. İstemcisini yükledikten ve siteye atandığından emin olduktan sonra **Yenile**' yi seçin.

### <a name="properties"></a>Özellikler

İstemci için hedeflenen keşif verilerini ve dağıtımlarını görüntüleyin.

Ayrıca, Görev sıralarının cihaza bir işletim sistemi dağıtmak için kullandığı değişkenleri yapılandırabilirsiniz. Daha fazla bilgi için, [cihazlar ve koleksiyonlar için görev dizisi değişkenleri oluşturun](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a>İstemcileri **Cihaz Koleksiyonları** düğümünden yönetme

**Cihazlar** düğümündeki cihazlar için kullanılabilen görevlerin birçoğu koleksiyonlar üzerinde de mevcuttur. Konsol, işlemi koleksiyondaki tüm uygun cihazlara otomatik olarak uygular. Tüm bir koleksiyon üzerinde bu eylem, ek ağ paketleri oluşturur ve site sunucusundaki CPU kullanımını artırır.  

Koleksiyon düzeyindeki görevleri çalıştırmadan önce aşağıdaki soruları göz önünde bulundurun. Başlatıldıktan sonra, konsolundan görevi durduramazsınız.

- Koleksiyonda kaç cihaz var?
- Cihazlar düşük bant genişliğine sahip ağ bağlantılarıyla mı bağlı?
- Bu görevin tüm cihazlarda ne kadar süre tamamlaması gerekir?

Daha fazla bilgi için bkz. [koleksiyonları yönetme](collections/manage-collections.md).


## <a name="restart-clients"></a>İstemcileri yeniden Başlat

Yeniden başlatma gerektiren istemcileri belirlemek için Configuration Manager konsolunu kullanın. Sonra yeniden başlatmak için bir istemci bildirimi eylemi kullanın.

> [!Tip]
> İstemcileri daha az çabayla güncel tutmak için otomatik istemci yükseltmesini etkinleştirin. Daha fazla bilgi için bkz. [otomatik istemci yükseltme hakkında](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

Yeniden başlatma bekleyen cihazları tanımlamak için Configuration Manager konsolundaki **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar** düğümünü seçin. Ardından, Ayrıntılar bölmesinde her bir cihazın durumunu **bekleyen yeniden başlatma**adlı yeni bir sütunda görüntüleyin. Her cihazda aşağıdaki değerlerden biri veya daha fazlası vardır:

- **Hayır**: bekleyen yeniden başlatma yok
- **Configuration Manager**: Bu değer, istemci yeniden başlatma Düzenleyicisi bileşeninden gelir (rebootcoordinator. log)
- **Dosya yeniden adlandırma**: Bu değer, Windows 'u bekleyen bir dosya yeniden adlandırma işlemini (Hklm\system\currentcontrolset\control\session Manager, PendingFileRenameOperations) ile gelir
- **Windows Update**: Bu değer, bir veya daha fazla güncelleştirme için bekleyen bir yeniden başlatmanın gerekli olduğunu bildiren Windows Update aracısından gelir (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **Özellik Ekle veya Kaldır**: Bu değer Windows Bileşen tabanlı hizmet verme işleminden gelir bir Windows özelliğinin eklenmesi veya kaldırılması için yeniden başlatma gerekiyor (HKLM\Software\Microsoft\Windows\CurrentVersion\Component tabanlı Servicing\Reboot bekleniyor)

### <a name="create-the-client-notification-to-restart-a-device"></a>Bir cihazı yeniden başlatmak için istemci bildirimini oluşturma

1. Konsolunun **Cihaz Koleksiyonları** düğümünde bir koleksiyon içinde yeniden başlatmak istediğiniz cihazı seçin.
2. Şeritte **Istemci bildirimi**' ni seçin ve ardından **Yeniden Başlat**' ı seçin. Yeniden başlatma hakkında bir bilgi penceresi açılır. Yeniden başlatma isteğini onaylamak için **Tamam ' ı** seçin.

Bildirim bir istemci tarafından alındığında, kullanıcıyı yeniden başlatma hakkında bilgilendirmek için bir **Yazılım Merkezi** bildirim penceresi açılır. Yeniden başlatma işlemi varsayılan olarak 90 dakika sonra gerçekleşir. [İstemci ayarlarını](../deploy/configure-client-settings.md)yapılandırarak yeniden başlatma süresini değiştirebilirsiniz. Yeniden başlatma davranışı ayarları, varsayılan ayarların [bilgisayar yeniden başlatma](../deploy/about-client-settings.md#computer-restart) sekmesinde bulunur.


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a>İstemci önbelleğini yapılandırma

İstemci önbelleği, istemcileri uygulamaları ve programları yüklerken geçici dosyaları depolar. Yazılım güncelleştirmeleri de istemci önbelleğini kullanır, ancak boyut ayarından bağımsız olarak her zaman önbelleğe indirmeyi dener. İstemciyi el ile yüklediğinizde, istemci anında yükleme kullandığınızda veya yüklemeden sonra boyut ve konum gibi önbellek ayarlarını yapılandırın.

Önbellek klasörünün boyutunu Configuration Manager konsolundaki istemci ayarlarını kullanarak belirtebilirsiniz. Daha fazla bilgi için bkz. [istemci önbellek ayarları](../deploy/about-client-settings.md#client-cache-settings).

Configuration Manager istemci önbelleğinin varsayılan konumu `%windir%\ccmcache` ve varsayılan disk alanı 5120 MB 'tır.  

> [!IMPORTANT]  
> İstemci önbelleği için kullanılan klasörü şifrelemeyin. Configuration Manager şifrelenmiş bir klasöre içerik indiremez.  

### <a name="about-the-client-cache"></a>İstemci önbelleği hakkında  

Configuration Manager istemcisi dağıtımı aldıktan hemen sonra gerekli yazılım içeriğini indirir, ancak dağıtımın zamanlandığı zamana kadar çalıştırmayı bekler. Zamanlanan zamanda Configuration Manager istemci, içeriğin önbellekte kullanılabilir olup olmadığını kontrol eder. İçerik önbellekte ise ve doğru sürümteyse, istemci önbelleğe alınmış içeriği kullanır. İçeriğin gerekli sürümü değiştiğinde veya istemci başka bir pakete yer açmak üzere içeriği silerse, istemci içeriği yeniden önbelleğe indirir.  

İstemci, önbelleğin boyutundan daha büyük bir program veya uygulamanın içeriğini indirmeye çalışırsa, yetersiz önbellek boyutu nedeniyle dağıtım başarısız olur. İstemci yetersiz önbellek boyutu için 10050 durum iletisini oluşturur. Önbellek boyutunu daha sonra artırırsanız, sonuç şu şekilde olur:  

- Gerekli bir program için: istemci içeriği indirmeyi otomatik olarak yeniden dener. Paketi ve programı istemciye yeniden dağıtın.  
- Gerekli bir uygulama için: istemci, istemci ilkesini indirdiğinde içeriği indirmeyi otomatik olarak yeniden dener.  

İstemci önbelleğin boyutundan küçük olan bir paketi indirmeye çalışırsa, ancak önbellek doluysa, tüm *gerekli* dağıtımlar şu kadar yeniden denemeye devam tutar:

- Önbellek alanı kullanılabilir
- İndirme zaman aşımına uğrar
- Yeniden deneme sayısı sınırına ulaştı

Daha sonra önbellek boyutunu artırırsanız, istemci, sonraki yeniden deneme aralığı sırasında paketi indirmeyi yeniden dener. İstemci, 18 kez denenene kadar her dört saatte bir içeriği indirmeyi dener.  

Önbelleğe alınan içerik otomatik olarak silinmez. İstemci bu içeriği kullandıktan sonra en az bir gün önbellekte kalır. İstemci önbelleğinde içeriği kalıcı hale getirme seçeneğiyle paket özelliklerini yapılandırırsanız, istemci onu otomatik olarak silmez. Önbellek alanı son 24 saat içinde indirilen paketler tarafından kullanılıyorsa ve istemcinin yeni paketler indirmesi gerekiyorsa, önbellek boyutunu artırın veya kalıcı önbellek içeriğini silme seçeneğini belirleyin.  

İstemci önbelleğini manuel istemci yüklemesi sırasında veya istemci yüklendikten sonra yapılandırmak için aşağıdaki yordamları kullanın.  

### <a name="configure-the-cache-during-manual-client-installation"></a>El ile istemci yüklemesi sırasında önbelleği yapılandırma  

Yükleme kaynak konumundan CCMSetup.exe komutunu çalıştırın ve gereken aşağıdaki özellikleri boşlukla ayırarak belirtin:  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > SMSCACHESIZE yerine Configuration Manager konsolundaki **Istemci ayarları** ' nda bulunan önbellek boyutu ayarlarını kullanın. Daha fazla bilgi için bkz. [istemci önbellek ayarları](../deploy/about-client-settings.md#client-cache-settings).

CCMSetup. exe için bu komut satırı özelliklerinin nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../deploy/about-client-installation-properties.md).

### <a name="configure-the-cache-during-client-push-installation"></a>İstemci gönderme yüklemesi sırasında önbelleği yapılandırma  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Uygun siteyi seçin. Şeridin **giriş** sekmesinde, **Ayarlar** grubunda, **istemci yükleme ayarları**' nı seçin ve **istemci gönderme yüklemesi**' ni seçin. **Yükleme özellikleri** sekmesine geçin.  

3. Boşluklarla ayırarak aşağıdaki özellikleri belirtin:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > SMSCACHESIZE yerine Configuration Manager konsolundaki **Istemci ayarları** ' nda bulunan önbellek boyutu ayarlarını kullanın. Daha fazla bilgi için bkz. [istemci önbellek ayarları](../deploy/about-client-settings.md#client-cache-settings).

     CCMSetup. exe için bu komut satırı özelliklerinin nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../deploy/about-client-installation-properties.md).  

### <a name="configure-the-cache-on-the-client-computer"></a>İstemci bilgisayarda önbelleği yapılandırma  

1. İstemci bilgisayarda **Configuration Manager** denetim masasını açın.  

2. **Önbellek** sekmesine geçin. boşluk ve konum özelliklerini ayarlayın. Varsayılan konum `%windir%\ccmcache` .  

3. Önbellek klasöründeki dosyaları silmek için **dosyaları sil**' i seçin.  

### <a name="configure-client-cache-size-in-client-settings"></a>İstemci ayarları 'nda istemci önbellek boyutunu Yapılandır

İstemciyi yeniden yüklemek zorunda kalmadan istemci önbelleğinin boyutunu ayarlayın. Configuration Manager konsolundaki **Istemci ayarları** ' nda bulunan önbellek boyutu ayarlarını kullanın. Daha fazla bilgi için bkz. [istemci önbellek ayarları](../deploy/about-client-settings.md#client-cache-settings).


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a>İstemciyi kaldırma

Configuration Manager istemci yazılımını bir bilgisayardan, **CCMSetup. exe** ' yi **/Uninstall** özelliğiyle kullanarak kaldırabilirsiniz. Komut isteminden tek bir bilgisayarda CCMSetup. exe ' yi çalıştırın veya bir bilgisayar koleksiyonu için istemciyi kaldırmak üzere bir paket dağıtın.  

> [!NOTE]  
> Configuration Manager istemcisini bir mobil cihazdan kaldıramazsınız. Configuration Manager istemcisini bir mobil cihazdan kaldırmanız gerekiyorsa, mobil cihazdaki tüm verileri silen cihazı silmelisiniz.  

1. Yönetici olarak bir Windows komut istemi açın. Klasörü CCMSetup. exe ' nin bulunduğu konum olarak değiştirin, örneğin:`cd %windir%\ccmsetup`

2. Şu komutu çalıştırın:`CCMSetup.exe /uninstall`

> [!TIP]  
> Kaldırma işlemi, ekranda sonuç görüntülemez. İstemcinin başarıyla yüklemesini doğrulamak için şu günlük dosyasına bakın:`%windir%\ccmsetup\logs\CCMSetup.log`  
>
> Kaldırma işleminin başka bir şey yapmadan önce tamamlanmasını beklemeniz gerekiyorsa, `Wait-Process CCMSetup` PowerShell 'de çalıştırın. Bu komut, CCMSetup işlemi tamamlanana kadar bir betiği duraklatabilir.


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a>Çakışan kayıtları yönetme

Configuration Manager, tekrarlanmış olabilecek istemcileri belirlemeyi denemek ve çakışan kayıtlarla ilgili olarak sizi uyarmak için donanım tanımlayıcısını kullanır. Örneğin, bir bilgisayarı yeniden yüklerseniz, donanım tanımlayıcısı aynı olur ancak Configuration Manager tarafından kullanılan GUID değişebilir.  

Configuration Manager, bilgisayar hesabının Windows kimlik doğrulamasını veya güvenilen bir kaynaktan bir PKI sertifikasını kullanarak çakışmaları otomatik olarak çözer. Configuration Manager yinelenen donanım tanımlayıcılarının çakışmasını çözümleyemezse, bir hiyerarşi ayarı davranışı belirler.

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>Çakışan kayıtları yönetmek için hiyerarşi ayarını değiştirin  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.

1. Şeritte **Hiyerarşi ayarları**' nı seçin.

1. **Istemci onayı ve çakışan kayıtlar** sekmesine geçin ve aşağıdaki seçeneklerden birini belirleyin:

    - **Çakışan kayıtları otomatik olarak çözümle**
    - **Çakışan kayıtları el ile Çözümle**

### <a name="manually-resolve-conflicting-records"></a>Çakışan kayıtları el ile Çözümle  

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **sistem durumu**' nu genişletin ve **Çakışan Kayıtlar** düğümünü seçin.  

1. Bir veya daha fazla çakışan kaydı seçin ve **Çakışan kayıt**' ı seçin.  

1. Aşağıdaki seçeneklerden birini belirtin:  

    - **Birleştir**: yeni algılanan kaydı mevcut istemci kaydıyla birleştirin.  

    - **Yeni**: çakışan istemci kaydı için yeni bir kayıt oluşturun.  

    - **Engelle**: çakışan istemci kaydı için yeni bir kayıt oluşturun, ancak engellenmiş olarak işaretleyin.  


## <a name="manage-duplicate-hardware-identifiers"></a>Yinelenen donanım tanımlayıcılarını yönetme

PXE önyüklemesi ve istemci kaydı için Configuration Manager yok sayan donanım tanımlayıcılarının bir listesini sağlayabilirsiniz. Bu liste, iki genel sorunun ele sağlanmasına yardımcı olur:

1. Birçok yeni cihaz, yerleşik bir Ethernet bağlantı noktası içermez. Teknisyenler, işletim sistemi dağıtımı amaçlarıyla kablolu bağlantı kurmak için bir USB-Ethernet bağdaştırıcısı kullanır. Bu bağdaştırıcılar genellikle maliyet ve genel kullanılabilirlik nedeniyle paylaşılır. Site, cihazı tanımlamak için bu bağdaştırıcının MAC adresini kullanır. Bu nedenle, bağdaştırıcıyı yeniden kullanmak her dağıtım arasında ek yönetici eylemleri olmadan sorunlu olur. Bu senaryodaki bağdaştırıcıyı yeniden kullanmak için MAC adresini dışlayın.

2. SMBıOS özniteliği benzersiz olmalıdır, ancak bazı özel donanım cihazlarında yinelenen tanımlayıcılar vardır. Bu yinelenen tanımlayıcıyı dışlayın ve her bir cihazın benzersiz MAC adresine güvenin.

Yok sayılacak Configuration Manager donanım tanımlayıcıları eklemek için aşağıdaki işlemi kullanın:

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.

2. Şeridin **giriş** sekmesinde, **siteler** grubunda, **Hiyerarşi ayarları**' nı seçin.

3. **Istemci onayı ve çakışan kayıtlar** sekmesine geçin. Yeni donanım tanımlayıcıları eklemek için **yinelenen donanım tanımlayıcıları** bölümünde **Ekle** ' yi seçin.

> [!TIP]
> Sürüm 1910 ' den başlayarak, yinelenen donanım tanımlayıcılarının yönetimini otomatikleştirmek için aşağıdaki PowerShell cmdlet 'lerini kullanın:<!-- 4852819 -->
>
> - New-Cmduplicatehardwareıdguid
> - Remove-Cmduplicatehardwareıdguid
> - New-Cmduplicatehardwareıdmacaddress
> - Remove-Cmduplicatehardwareıdmacaddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a>İlke almayı Başlat

Configuration Manager istemcisi istemci ilkesini istemci ayarı olarak yapılandırdığınız bir zamanlamaya göre indirir. Ayrıca, istemciden isteğe bağlı ilke alma işlemi başlatabilirsiniz. Örneğin, sorun giderme veya test durumları için.  

- [İstemci bildirimi](#bkmk_policy-notify)
- [İstemci Denetim Masası](#bkmk_policy-manual)
- [Destek Merkezi](#bkmk_policy-support)
- [Betik](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a>İstemci bildirimi ile istemci ilkesi almayı Başlat  

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **cihazlar**' ı seçin.  

1. İlkeyi indirmek istediğiniz cihazı seçin. Şeridin **giriş** sekmesinde, **cihaz** grubunda, **İstemci bildirimi**' ni seçin ve ardından **bilgisayar ilkesini indir**' i seçin.  

    > [!NOTE]  
    > Ayrıca, bir koleksiyondaki tüm cihazlar için ilke alımı başlatmak üzere istemci bildirimini de kullanabilirsiniz.  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a>Configuration Manager istemci denetim masasından istemci ilkesi almayı başlatma

1. Bilgisayardaki **Configuration Manager** denetim masasını açın.  

2. **Eylemler** sekmesine geçin. bilgisayar ilkesini başlatmak Için **makine Ilkesi alımı & değerlendirme döngüsünü** seçin ve **Şimdi Çalıştır**' ı seçin.  

3. İstemi onaylamak için **Tamam ' ı** seçin.  

4. Diğer eylemler için önceki adımları tekrarlayın. Örneğin, Kullanıcı Ilkesi alımı Kullanıcı istemci ayarları için **değerlendirme döngüsünü &** .  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a>Destek Merkezi ile istemci ilkesi almayı başlatma

İstemci ilkesi istemek ve görüntülemek için destek merkezini kullanın. Daha fazla bilgi için bkz. [Destek Merkezi başvurusu](../../support/support-center-ui-reference.md#bkmk_support-policy).

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a>Betiği ile istemci ilkesi almayı Başlat  

1. Not defteri veya Windows PowerShell ISE gibi bir betik düzenleyicisini açın.  

2. Aşağıdaki örnek PowerShell kodunu kopyalayın ve ekleyin<!-- SCCMDocs#1591 --> dosyasına:  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > Zamanlama kimlikleri hakkında daha fazla bilgi için bkz. [Ileti kimlikleri](../../support/send-schedule-tool.md#bkmk_sendschedule-guids).

3. Dosyayı bir. ps1 uzantısıyla kaydedin.  

4. Betiği istemcide çalıştırın.
