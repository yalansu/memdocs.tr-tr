---
title: Yeni sürüm 1702
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1702 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 5c125bc92c8949384486c7efc03cea122258092e
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993514"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>Sürüm 1702 ' deki yenilikler&#39;Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli dalın Configuration Manager güncelleştirme 1702, daha önce yüklü olan ve 1602, 1606 veya 1610 sürümlerini çalıştıran sitelerde konsol içi bir güncelleştirme olarak sunulmaktadır. Ayrıca, yeni bir dağıtım yüklerken kullanabileceğiniz bir temel sürüm olarak da kullanılabilir.

> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanmanız gerekir.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:    
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Sitelere güncelleştirme yükleme](../../servers/manage/updates.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)

Aşağıdaki bölümlerde, Configuration Manager sürüm 1702 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi sağlanmaktadır.  

## <a name="deprecated-features-and-operating-systems"></a>Kullanımdan kaldırılan özellikler ve işletim sistemleri
[Kaldırılan ve kullanımdan kaldırılan öğelerde](deprecated/removed-and-deprecated.md)uygulanmadan önce yapılan değişiklikler hakkında bilgi edinin.

Sürüm 1702 aşağıdaki ürünler için desteği bırakır:
- Site veritabanı sunucuları için **SQL Server 2008 R2**. Desteğin kullanımdan kaldırılması ilk olarak 10 Temmuz 2015 ' de [duyurulmuştur](deprecated/removed-and-deprecated-server.md#sql-server) . Sürüm 1702 ' den önceki bir Configuration Manager sürümünü kullandığınızda SQL Server bu sürümü desteklenmeye devam eder.
- Site sistem sunucuları ve çoğu site sistem rolü için **Windows Server 2008 R2**. Desteğin kullanımdan kaldırılması ilk olarak 10 Temmuz 2015 ' de [duyurulmuştur](deprecated/removed-and-deprecated-server.md#server-os) . Sürüm 1702 ' den önceki bir Configuration Manager sürümünü kullandığınızda Windows 'un bu sürümü desteklenmektedir.  
- Site sistem sunucuları ve çoğu site sistem rolü için **Windows Server 2008**. Desteğin kullanımdan kaldırılması ilk olarak 10 Temmuz 2015 ' de [duyurulmuştur](deprecated/removed-and-deprecated-server.md#server-os) .
- **WINDOWS XP Embedded**, istemci işletim sistemi olarak. Kullanımdan kaldırma ilk olarak 10 Temmuz 2015 ' de [duyuruldu](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems) . Sürüm 1702 ' den önceki bir Configuration Manager sürümünü kullandığınızda Windows 'un bu sürümü desteklenmektedir.




## <a name="site-infrastructure"></a>Site altyapısı

### <a name="improvements-for-in-console-search"></a>Konsol içi aramada iyileştirmeler
Configuration Manager konsolunda arama kullanma geliştirmeleri aşağıda verilmiştir:
- **Nesne yolu:**  
  Birçok nesne artık **nesne yolu**adlı bir sütunu destekliyor.  Bu sütunu arama ve görüntüleme sonuçlarınıza dahil ettiğinizde her nesnenin yolunu görüntüleyebilirsiniz. Örneğin, Uygulamalar düğümünde uygulamalar için bir arama çalıştırırsanız ve ayrıca alt düğümleri arıyorsanız, sonuçlar bölmesindeki *nesne yolu* sütunu döndürülen her nesnenin yolunu gösterir.   

- **Arama metninin korunması:**  
  Arama metin kutusuna metin girdiğinizde ve sonra bir alt düğüm ve geçerli düğüm arama arasında geçiş yaptığınızda yazdığınız metin artık devam eder ve yeniden girmeye gerek kalmadan yeni bir arama için kullanılabilir kalır.

- **Alt düğümleri arama kararının korunması:**  
  *Geçerli düğümü* veya *tüm alt düğümleri* aramak için belirlediğiniz seçenek, artık üzerinde çalıştığınız düğümü değiştirdiğinizde devam ediyor. Bu yeni davranış, konsolunda hareket ettiğiniz sürece bu kararı sürekli olarak sıfırlamanız gerekmediği anlamına gelir. Varsayılan olarak, konsolunu açtığınızda bu seçenek yalnızca geçerli düğümü arayacak şekilde yapılır.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Configuration Manager konsolundan geri bildirim gönderin

Doğrudan geliştirme ekibine geri bildirim göndermek için konsol içi geri bildirim seçeneklerini kullanabilirsiniz.

**Geri bildirim** seçeneğini bulabilirsiniz:
- Şeritte, her bir düğümün Giriş sekmesinin en solundaki.  
  ![Şeridi](./media/feedback-home.png)

- Konsolda herhangi bir nesneye sağ tıkladığınızda.   
   ![Righ-tıklama seçeneği](./media/feedback-option.png)   

  **Geri bildirim** seçme, tarayıcınızı [Configuration Manager UserVoice geri bildirim Web sitesinde](https://configurationmanager.uservoice.com/forums/300492-ideas)açar.


###  <a name="changes-for-updates-and-servicing"></a>Güncelleştirmeler ve bakım için değişiklikler
Güncelleştirmeler ve bakım için değişiklikler aşağıda verilmiştir:

- **Düğüm konumu**   
  Sürüm 1702 yüklendikten sonra, **güncelleştirmeler ve bakım** düğümü **Yönetim**altında en üst düzey bir düğüm olarak görünür. Artık **Cloud Services**aşağıdaki alt düğüm değildir.

- **Yeni güncelleştirme durumları**  
  Konsolunda kullanılabilir güncelleştirmeleri görüntülediğinizde, iki yeni durum vardır:  
  - **Yüklenmek üzere kullanılabilir** -bu, indirilmiş ve yüklenmeye hazır bir güncelleştirmedir.
  - **Indirmeye hazır**  -Bu güncelleştirme mevcut, ancak indirilmedi. Bu güncelleştirmeyi indirmeyi seçebilirsiniz, ancak bu güncelleştirmenin yerini daha yeni bir güncelleştirme almıştır.


- **Daha basit güncelleştirme seçimleri**  
  Altyapınızda iki veya daha fazla güncelleştirme için bir sonraki sefer, yalnızca en son güncelleştirme indirilir. Örneğin, geçerli site sürümünüz mevcut en son sürümden iki veya daha eski ise, yalnızca en son güncelleştirme sürümü otomatik olarak indirilir.  

  En güncel sürüm olmadıkları zaman bile, diğer kullanılabilir güncelleştirmeleri indirip yüklemeyi tercih edebilirsiniz. Daha eski bir güncelleştirmeyi indirdiğinizde, güncelleştirmenin yeni bir güncelleştirme ile değiştirildiğini belirten bir uyarı alırsınız. *İndirileceği*bir güncelleştirmeyi indirmek için, konsolda güncelleştirmeyi seçin ve ardından **İndir**' e tıklayın.

- **Eski güncelleştirmeler için geliştirilmiş Temizleme**   
  Site sunucunuzdaki ' EasySetupPayload ' klasöründen gereksiz İndirmeleri silen bir otomatik temizleme işlevi ekledik. Bu sürüm 1702 ile sunulmuş olduğundan, bir güncelleştirme paketi veya gelecekteki güncelleştirme sürümü gibi sonraki bir güncelleştirme yüklendikten sonra temizlik çalışmaya başlar.  


### <a name="data-warehouse-service-point"></a>Veri ambarı hizmet noktası
Configuration Manager dağıtımınız için uzun süreli geçmiş verileri depolamak ve raporlamak için veri ambarı hizmet noktasını kullanın.

Veri ambarı, değişiklik izleme zaman damgalarına sahip 2 TB 'a kadar veriyi destekler. Veri depolama, Configuration Manager site veritabanından veri ambarı veritabanına otomatik eşitlemeler tarafından gerçekleştirilir. Bu bilgilere daha sonra Raporlama Hizmetleri noktanınızdan erişilebilir.

Daha fazla bilgi için bkz. [veri ambarı hizmet noktası](../../servers/manage/data-warehouse.md).


### <a name="peer-cache-improvements"></a>Eş önbellek geliştirmeleri
Sürüm 1702 ' den başlayarak, eş önbellek kaynak bilgisayarı aşağıdaki koşullardan herhangi birini karşılıyorsa eş önbellek kaynak bilgisayar bir içerik isteğini reddeder:  
-  Düşük pil modunda.
-  CPU yükü, içerik istenen zamanda %80 ' ü aşıyor.
-  Disk g/ç, 10 ' u aşan bir *Avgdiskqueuelength* öğesine sahiptir.
-  Bilgisayar için kullanılabilir başka bağlantı yok.   
Daha fazla bilgi için bkz. [Configuration Manager istemcileri Için eş önbellek](../hierarchy/client-peer-cache.md)içindeki **eş önbellek kaynağına sınırlı erişim** .   

Ayrıca, raporlama noktanlarınıza üç yeni rapor eklenir. Bu raporları, hangi sınır grubu, bilgisayar ve içerik dahil olmak üzere, reddedilen içerik istekleri hakkında daha fazla ayrıntıyı anlamak için kullanabilirsiniz. Bkz. eş önbellek konusunda [izleme](../hierarchy/client-peer-cache.md#monitoring) .

### <a name="content-library-cleanup-tool"></a>İçerik kitaplığı temizleme aracı
İçerik artık bir uygulamayla ilişkilendirilmediği zaman, içeriği dağıtım noktalarından kaldırmak için [içerik kitaplığı Temizleme aracını](../hierarchy/content-library-cleanup-tool.md) kullanın.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Azure Kamu bulutu ile OMS bağlayıcısını kullanma
Microsoft Azure Kamu buluttaki OMS Log Analytics bağlanmak için OMS bağlayıcısını kullanabilirsiniz. Bu, bağlayıcının kamu bulutuyla çalışabilmesi için OMS bağlayıcısını yüklemeden önce bir yapılandırma dosyasını değiştirmenizi gerektirir. Daha fazla bilgi için bkz. [Azure Kamu Bulutu Ile OMS bağlayıcısını kullanma](/azure/azure-monitor/platform/collect-sccm).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Yazılım güncelleştirme noktaları sınır gruplarına eklenir
Sürüm 1702 ' den başlayarak, istemciler yeni bir yazılım güncelleştirme noktası bulmak için sınır grupları kullanır ve geçerli biri artık erişilebilir değilse yeni bir yazılım güncelleştirme noktası bulur. Bir istemcinin bulabileceği sunucuları denetlemek için, farklı sınır gruplarına bireysel yazılım güncelleştirme noktaları ekleyebilirsiniz. Daha fazla bilgi için, [sınır gruplarını yapılandırma](../../servers/deploy/configure/boundary-groups.md) konusundaki [yazılım güncelleştirme noktaları](../../servers/deploy/configure/boundary-groups.md#bkmk_sup) konusuna bakın.


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Uyumluluk ayarları

### <a name="new-compliance-settings-for-ios"></a>İOS için yeni uyumluluk ayarları

İOS cihazları için Microsoft Intune ile kullanılabilir olanlarla eşleşecek pek çok yeni ayar ekledik.


## <a name="application-management"></a>Uygulama Yönetimi

### <a name="improved-support-for-windows-store-for-business-apps"></a>Iş için Windows Mağazası uygulamaları için geliştirilmiş destek

Artık, Configuration Manager istemcisini kullanarak yönettiğiniz Windows 10 bilgisayarlarına Iş için Windows Mağazası 'ndan çevrimiçi lisanslanmış uygulamalar dağıtabilirsiniz.
Daha fazla bilgi için bkz. [iş Için Windows Mağazası 'ndan uygulamaları yönetme](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Bir uygulamayı yüklemeden önce yürütülebilir dosyaları çalıştırmaya yönelik denetim

Dağıtım türünün **Özellikler** iletişim kutusunda, **yükleme davranışı** sekmesinde artık, çalışıyorsa dağıtım türünün yüklenmesini engelleyebilen daha fazla yürütülebilir dosyadan birini belirtebilirsiniz. Dağıtım türünün yüklenebilmesi için kullanıcının çalışan yürütülebilir dosyayı kapatması (veya gerekli amacına sahip dağıtımlar için otomatik olarak kapatılabilir) gerekir.

Uygulama **kullanılabilir**olarak dağıtılmışsa ve Son Kullanıcı uygulamayı yüklemeye çalışırsa, yüklemeye devam edebilmek için önce belirttiğiniz çalışan yürütülebilir dosyaları kapatmaları istenir.

Uygulama **gerekli**olarak dağıtılmışsa ve **dağıtım türü özellikleri iletişim kutusunun yükleme davranışı sekmesinde belirttiğiniz çalışan tüm yürütülebilir dosyaları otomatik olarak kapat** seçeneği işaretliyse, uygulama yükleme son tarihine ulaşıldığında belirttiğiniz yürütülebilir dosyaların otomatik olarak kapatıldığını bildiren bir iletişim kutusu görür.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Karma MDM için uygulama yönetimi geliştirmeleri

- [Toplu satın alınan iOS uygulamalarını cihaz koleksiyonlarına dağıtma](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Eğitim için iOS toplu satın alma programı desteği](#support-for-ios-volume-purchase-program-for-education)
- [Birden çok toplu satın alma programı belirteci için destek](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>İşletim sistemi dağıtımı

### <a name="expire-stand-alone-media"></a>Tek başına medyanın süre sonu
Tek başına medya oluşturduğunuzda, medyada isteğe bağlı başlangıç ve sona erme tarihlerini ayarlamaya yönelik yeni seçenekler vardır. Bu ayarlar varsayılan olarak devre dışıdır. Tarihler, tek başına medya çalıştırılmadan önce bilgisayardaki sistem saatine göre karşılaştırılır. Sistem saati, sona erme zamanından başlangıç zamanından veya ondan daha eski olduğunda, tek başına medya başlatılmaz. Bu seçenekler, New-CMStandaloneMedia PowerShell cmdlet 'i kullanılarak da kullanılabilir. Ayrıntılar için bkz. [tek başına medya oluşturma](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="package-id-displayed-in-task-sequence-steps"></a>Görev sırası adımlarında görünen paket KIMLIĞI
Bir pakete, sürücü paketine, işletim sistemi görüntüsüne, önyükleme görüntüsüne veya işletim sistemi yükseltme paketine başvuran herhangi bir görev dizisi adımı artık başvurulan nesnenin paket KIMLIĞINI görüntüler. Bir görev dizisi adımı bir uygulamaya başvurduğunda, nesne KIMLIĞI görüntülenir.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Tek başına medyada ek içerik desteği
Artık tek başına medyada ek içerik desteklenmektedir. Medyada hazırlanmak üzere ek paketler, sürücü paketleri ve uygulamalar, görev dizisinde başvurulan diğer içerikle birlikte seçebilirsiniz. Daha önce, yalnızca görev dizisinde başvurulan içerikler tek başına medyada hazırlanmıştı. Ayrıntılar için bkz. [tek başına medya oluşturma](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="hardware-inventory-collects-uefi-information"></a>Donanım envanteri, UEFı bilgilerini toplar
Bir bilgisayarın UEFı modunda başlatılıp başlatılmayacağını belirlemenize yardımcı olmak için yeni bir donanım envanteri sınıfı (**SMS_Firmware**) ve özelliği (**UEFI**) kullanılabilir. Bir bilgisayar UEFı modunda başlatıldığında, **UEFI** özelliği **true**olarak ayarlanır. Bu, varsayılan olarak donanım envanterinde etkinleştirilmiştir. Donanım envanteri hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Yüksek etkili görev dizileri için yazılım merkezi uyarı iletileri geliştirmeleri
Bu sürüm, yüksek etki dağıtım görev dizileri için Software Center uyarı iletilerine yönelik aşağıdaki geliştirmeleri içerir:

- Görev dizisinin özelliklerinde, artık, işletim sistemi olmayan görev dizileri dahil olmak üzere, yüksek riskli dağıtım olarak herhangi bir görev dizisini yapılandırabilirsiniz. Belirli koşullara uyan herhangi bir görev dizisi otomatik olarak yüksek etki olarak tanımlanır. Ayrıntılar için bkz. [yüksek riskli dağıtımları yönetme](../../servers/manage/settings-to-manage-high-risk-deployments.md).
- Görev dizisinin özelliklerinde, varsayılan bildirim iletisini kullanmayı veya yüksek etkili dağıtımlar için kendi özel bildirim iletinizi oluşturmayı seçebilirsiniz.
- Görev dizisinin özelliklerinde, bir yeniden başlatma gerekiyor, görev dizisinin indirme boyutu ve tahmini çalışma süresi dahil olmak üzere yazılım merkezi özelliklerini yapılandırabilirsiniz.
- Yerinde yükseltmeler için varsayılan yüksek etki dağıtım iletisi artık uygulamalarınızın, verilerinizin ve ayarlarınızın otomatik olarak geçirildiğini belirtir. Daha önce, herhangi bir işletim sistemi yüklemesi için varsayılan ileti, tüm uygulamaların, verilerin ve ayarların yerinde yükseltme için doğru olmayan kayıp olduğunu gösterdi.

Ayrıntılar için bkz. [yüksek etki görevi sırası ayarlarını yapılandırma](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Bir görev dizisi başarısız olduğunda önceki sayfaya dön
Artık bir görev dizisini çalıştırdığınızda ve bir hata olduğunda önceki sayfaya geri dönebilirsiniz. Bu sürümden önce, bir hata oluştuğunda görev sırasını yeniden başlatmanız gerekiyordu. Örneğin, **önceki** düğmeyi aşağıdaki senaryolarda kullanabilirsiniz:

- Bir bilgisayar Windows PE 'de başlatıldığında, görev dizisi önyükleme iletişim kutusu görev dizisi kullanılabilir olmadan önce görüntülenebilir. Bu senaryoda Ileri ' ye tıkladığınızda, görev dizisinin son sayfası, kullanılabilir görev dizileri olmadığını belirten bir iletiyle birlikte görüntülenir. Şimdi, kullanılabilir görev dizileri için yeniden aramak üzere **geri** ' ye tıklayabilirsiniz. Görev dizisi kullanılabilir olana kadar bu işlemi yineleyebilirsiniz.
- Bir görev dizisini çalıştırdığınızda, ancak bağımlı içerik paketleri dağıtım noktalarında henüz yoksa, görev sırası başarısız olur. Artık eksik içeriği dağıtabilir (henüz dağıtılmamışsa) veya içeriğin dağıtım noktalarında kullanılabilir olmasını bekleyebilir ve ardından görev dizisinin içerik için tekrar aramasını sağlamak üzere **önceki** ' ye tıklayın.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Kullanılabilir dağıtımlar ve görev dizileri için ön önbelleğe alma içeriği
Sürüm 1702 ' den başlayarak, Görev sıralarının kullanılabilir dağıtımları için ön önbellek içeriğini kullanmayı seçebilirsiniz. Ön önbellek içeriği, istemcinin yalnızca dağıtım aldığı anda ilgili içeriği indirmesine izin verme seçeneğini sunar. Bu nedenle, Kullanıcı yazılım merkezi 'nde **yükleme** ' ye tıkladığında içerik hazırlayın ve içerik yerel sabit sürücüde olduğundan yükleme işlemi hızlı bir şekilde başlatılır. Ayrıntılar için bkz. [ön önbellek Içeriğini yapılandırma](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Yerinde yükseltme sırasında BIOS 'tan UEFı 'ye dönüştürme
Windows 10 Creators Update, işlemi UEFı etkin donanımlar için sabit diski yeniden bölümlemek ve dönüştürme aracını Windows 10 yerinde yükseltme işlemine tümleştiren bir basit dönüştürme aracı sunuyor. Bu aracı işletim sistemi yükseltme görev diziniz ve bellenimi BIOS 'tan UEFı 'ye dönüştüren OEM aracı ile birleştirdiğinizde, Windows 10 Creators Update 'e yerinde yükseltme sırasında bilgisayarlarınızı BIOS 'tan UEFı 'e dönüştürebilirsiniz. Ayrıntılar için bkz. [BIOS 'TAN UEFI dönüştürmeyi yönetmeye yönelik görev dizisi adımları](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Uygulamaları yüklemek görev dizisi adımındaki geliştirmeler
Bu sürüm aşağıdaki geliştirmeleri getirdi:
- **Uygulamaları yüklemek** görev sırası adımında 99 'e yükleyebileceğiniz en fazla uygulama sayısını arttırın. Önceki en büyük sayı 9 uygulamaiydi.
- Görev sırası düzenleyicisinde **uygulamaları yüklemek** görev dizisi adımına uygulamalar eklediğinizde, şimdi **yüklenecek uygulamayı seçin** bölmesinde birden çok uygulama seçebilirsiniz.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Sürücüleri otomatik olarak Uygula görev dizisi geliştirmeleri
Yeni görev dizisi değişkenleri, HTTP Katalog istekleri yaparken sürücüyü otomatik olarak Uygula görev dizisi adımında zaman aşımı değerini yapılandırmak için kullanılabilir. Aşağıdaki değişkenler ve varsayılan değerler (saniye cinsinden) kullanılabilir:
- SMSTSDriverRequestResolveTimeOut  
  Varsayılan: 60
- SMSTSDriverRequestConnectTimeOut  
  Varsayılan: 60
- SMSTSDriverRequestSendTimeOut  
  Varsayılan: 60
- SMSTSDriverRequestReceiveTimeOut  
  Varsayılan: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Derleme sürümü tarafından izlenen Windows 10 ADK
Windows 10 önyükleme görüntülerini özelleştirirken daha desteklenen bir deneyim sağlamak için Windows 10 ADK artık derleme sürümü tarafından izlenir. Örneğin, site Windows 10, sürüm 1607 için Windows ADK kullanıyorsa, yalnızca sürüm 10.0.14393 olan önyükleme görüntüleri konsolunda özelleştirilebilir. WinPE sürümlerini özelleştirme hakkında daha fazla bilgi için bkz. [önyükleme görüntülerini özelleştirme](../../../osd/get-started/customize-boot-images.md).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Varsayılan önyükleme görüntüsü kaynak yolu artık değiştirilemez
Varsayılan önyükleme görüntüleri Configuration Manager tarafından yönetilir ve varsayılan önyükleme görüntüsü kaynak yolu artık Configuration Manager konsolunda veya Configuration Manager SDK kullanılarak değiştirilemez. Özel önyükleme görüntüleri için özel bir kaynak yolu yapılandırmaya devam edebilirsiniz.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Varsayılan önyükleme görüntüleri, Configuration Manager yeni bir sürüme yükseltildikten sonra yeniden oluşturulur
Bu sürümden itibaren, Windows ADK sürümünü yükselttiğinizde ve sonra Configuration Manager en son sürümünü yüklemek için güncelleştirmeler ve bakım kullandığınızda Configuration Manager varsayılan önyükleme görüntülerini yeniden oluşturur. Bu, güncelleştirilmiş Windows ADK 'den yeni Window PE sürümünü, Configuration Manager istemcisinin yeni sürümünü, sürücüleri, özelleştirmeleri vb. içerir. Özel önyükleme görüntüleri değiştirilmez. Ayrıntılar için bkz. [önyükleme görüntülerini yönetme](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault).

## <a name="software-updates"></a>Yazılım güncelleştirmeleri

### <a name="deploy-microsoft-365-apps-to-clients"></a>Microsoft 365 uygulamalarını istemcilere dağıtma
Sürüm 1702 ' den başlayarak, Office 365 Istemci yönetimi panosundan, yükleme ayarlarını yapılandırmanıza, Office Içerik teslim ağlarından (CDNs) dosya yüklemenize ve dosyaları Configuration Manager bir uygulama olarak dağıtmanıza olanak sağlayan Office 365 yükleyicisini başlatabilirsiniz. Ayrıntılar için bkz. [Microsoft 365 Apps güncelleştirmelerini yönetme](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_deploy).

> [!IMPORTANT]
> Configuration Manager Office 365 uygulama Sihirbazı 'Nı kullanarak oluşturduğunuz ve dağıttığınız Microsoft 365 uygulaması, **office 365 Istemci yeniden** yazılım güncelleştirmeleri istemci Aracısı ayarının yönetimini etkinleştirene kadar Configuration Manager tarafından otomatik olarak yönetilmez. Ayrıntılar için bkz. [istemci ayarları hakkında](../../clients/deploy/about-client-settings.md).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Windows 10 güncelleştirmeleri için Hızlı yükleme dosyalarını yönetme
Sürüm 1702 ' den başlayarak, Configuration Manager Windows 10 güncelleştirmeleri için hızlı yükleme dosyalarını destekler. Windows 10 ' un desteklenen bir sürümünü kullanırken, yalnızca geçerli ayın Windows 10 toplu güncelleştirmesi ve önceki ayın güncelleştirmesi arasındaki değişiklikleri indirmek için Configuration Manager ayarlarını kullanabilirsiniz. Hızlı yükleme dosyaları olmadan, tüm Windows 10 toplu güncelleştirmesini (önceki aydan tüm güncelleştirmeler dahil) her ay indirir Configuration Manager. Hızlı yükleme dosyalarının kullanılması, istemcilerde daha küçük indirmeler ve daha hızlı yükleme süreleri sağlar. Ayrıntılar için bkz. [Windows 10 güncelleştirmeleri için hızlı yükleme dosyalarını yönetme](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Mobil aygıt yönetimi

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Karma MDM için oluşturma sihirbazları 'nda Android ve iOS sürümleri artık hedeflenebilir

Karma mobil cihaz yönetimi (MDM) için sürüm 1702 ' den başlayarak, Intune tarafından yönetilen cihazlar için yeni ilkeler ve profiller oluştururken artık belirli Android ve iOS sürümlerini hedeflemenizin gerekli değildir. Bunun yerine, aşağıdaki cihaz türlerinden birini seçersiniz:

- Android
- Samsung KNOX Standard 4,0 ve üzeri
- iPhone
- iPad

Bu değişiklik aşağıdaki öğeleri oluşturmaya yönelik sihirbazları etkiler:

- Yapılandırma öğeleri
- Uyumluluk ilkeleri
- Sertifika profilleri
- E-posta profilleri
- VPN profilleri
- Wi-Fi profilleri

Bu değişiklik sayesinde, Karma dağıtımlar yeni bir Configuration Manager yayın veya uzantıya gerek duymadan yeni Android ve iOS sürümleri için daha hızlı destek sağlayabilir. Tek başına Intune 'da yeni bir sürüm desteklendikten sonra, kullanıcılar mobil cihazlarını bu sürüme yükseltebilecektir.

Önceki Configuration Manager sürümlerinden yükseltirken oluşan sorunları engellemek için, mobil işletim sistemi sürümleri bu öğelerin Özellikler sayfalarında hala kullanılabilir. Hala belirli bir sürümü hedefliyorsanız, yeni öğeyi oluşturabilir ve ardından yeni oluşturulan öğenin Özellikler sayfasında hedeflenen sürümü belirtebilirsiniz. 

> [!NOTE]
> Özellikler sayfalarında bulunan son mobil işletim sistemi sürümü, bu sürüm ve tüm sonraki sürümler için geçerlidir. Özellikler sayfaları, işletim sistemlerini Android 7 ve iOS 10 ' dan daha sonra hedeflemek için aşağıdaki seçenekleri sağlar: 
> - **Android 7 ve üzeri**
> - **Tüm iOS 10 ve üzeri iPhone veya iPod Touch cihazları**
> - **Tüm iOS 10 ve üzeri iPad cihazları**

### <a name="android-for-work-support"></a>Android for Work desteği
1702 ile başlayarak, Microsoft Intune ile karma mobil cihaz yönetimi artık Android for Work cihaz kaydını ve yönetimini desteklemektedir.

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Toplu satın alınan iOS uygulamalarını cihaz koleksiyonlarına dağıtma

Artık, lisanslanan uygulamaları cihazlara ve kullanıcılara dağıtabilirsiniz. Cihaz lisansını desteklemeye yönelik uygulamalara bağlı olarak, dağıtım sırasında aşağıdaki gibi uygun bir lisans talep edilir:

| Configuration Manager sürümü | Uygulama, cihaz lisansını destekliyor mu? | Dağıtım koleksiyonu türü | Talep edilen lisans |
| ----------------------------- | ------------------------------ | -------------------------- | --------------- |
|1702 öncesi|Evet|Kullanıcı|Kullanıcı Lisansı|
|1702 öncesi|Hayır|Kullanıcı|Kullanıcı Lisansı|
|1702 öncesi|Evet|Cihaz|Kullanıcı Lisansı|
|1702 öncesi|Hayır|Cihaz|Kullanıcı Lisansı|
|1702 ve üzeri|Evet|Kullanıcı|Kullanıcı Lisansı|
|1702 ve üzeri|Hayır|Kullanıcı|Kullanıcı Lisansı|
|1702 ve üzeri|Evet|Cihaz|Cihaz lisansı|
|1702 ve üzeri|Hayır|Cihaz|Kullanıcı Lisansı|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Eğitim için iOS toplu satın alma programı desteği

Artık, eğitim için iOS toplu satın alma programından satın aldığınız uygulamaları da dağıtabilir ve izleyebilirsiniz.

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Birden çok toplu satın alma programı belirteci için destek

Artık birden çok Apple Volume Purchase program belirtecini Configuration Manager ile ilişkilendirebilirsiniz.

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Iş için Windows Mağazası 'nda iş kolu uygulamaları için destek

Artık Iş için Windows Mağazası 'ndan özel iş kolu uygulamalarını eşitleyebilirsiniz.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Koşullu erişim cihaz uyumluluk ilkesi geliştirmeleri

Kullanıcılar uyumlu olmayan uygulamalar listesinin parçası olan uygulamaları kullanırken koşullu erişimi destekleyen kurumsal kaynaklara erişimi engellemenize yardımcı olacak yeni bir cihaz uyumluluk ilkesi kuralı kullanılabilir. Uyumlu olmayan uygulamalar listesi, **yüklenemeyen**yeni uyumlu kural uygulamaları eklenirken yönetici tarafından tanımlanabilir. Bu kural, bir uygulamayı uyumlu olmayan listesine eklerken yöneticinin **uygulama adını**, **uygulama kimliğini**ve **uygulama yayımcısını** (isteğe bağlı) girmesini gerektirir. Bu ayar yalnızca iOS ve Android cihazlar için geçerlidir.

Ayrıca, kuruluşların güvenli olmayan uygulamalar aracılığıyla veri sızıntısını azaltmasına ve belirli uygulamalarda aşırı veri tüketimini engellemesine yardımcı olur.


### <a name="new-mobile-threat-defense-monitoring-tools"></a>Yeni Mobile Threat Defense izleme araçları

Sürüm 1702 ' den başlayarak, mobil tehdit savunma hizmeti sağlayıcınızda uyumluluk durumunu izlemenin yeni yolları vardır.


## <a name="protect-devices"></a>Cihazları koruma

### <a name="detect-outdated-antimalware-client-versions"></a>Güncel olmayan kötü amaçlı yazılımdan koruma istemci sürümlerini Algıla
Sürüm 1702 ' den başlayarak, Endpoint Protection istemcilerinin güncel olmamasını sağlamak için bir uyarı yapılandırabilirsiniz. Daha fazla bilgi için bkz. [güncel olmayan kötü amaçlı yazılım istemcisi Için uyarı](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client).

### <a name="device-health-attestation-updates"></a>Cihaz sistem durumu kanıtlama güncelleştirmeleri
Şirket içi istemciler için cihaz sistem durumu kanıtlama hizmeti artık yönetim noktasından yapılandırılıp yönetilebilecek. Daha fazla bilgi için bkz. [sistem durumu kanıtlama](../../servers/manage/health-attestation.md).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Iş için Windows Hello sertifika profilleri

Sertifika profillerini Iş için Windows Hello anahtar kapsayıcısında depolamayı planlıyorsanız ve sertifika profilinde akıllı kart oturum açma EKU 'SU kullanılıyorsa, sertifikanın doğru bir şekilde doğrulanmasını sağlamak için anahtar kaydı için izinleri yapılandırmanız gerekir.
Daha fazla bilgi için bkz. [iş Için Windows Hello ayarları](../../../protect/deploy-use/windows-hello-for-business-settings.md).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Son kullanıcılar için yeni Iş için Windows Hello bildirimi
Yeni bir Windows 10 bildirimi, son kullanıcılara Iş için Windows Hello kurulumunu tamamlamaya yönelik ek eylemler gerçekleştirmeleri gerektiğini bildirir (örneğin, bir PIN ayarlama).