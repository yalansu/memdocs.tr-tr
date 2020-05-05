---
title: Technical Preview 1701 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1701 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: f100d28b3fd4ce0d310ddb2f0b4e777c72f72881
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076212"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Configuration Manager için Technical Preview 1701 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*



Bu makalede, sürüm 1701 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Yazılım güncelleştirme noktaları için sınır grupları geliştirmeleri
Bu önizlemeden başlayarak, artık istemcileri yazılım güncelleştirme noktalarıyla ilişkilendirmek için sınır grupları kullanıyorsunuz. Bu, ek site sistem rollerini yönetmek üzere sınır grupları değişikliklerini genişletmek için çalışmaya devam etmenin bir parçasıdır.  Sınır grupları için değişiklikler ilk olarak Technical Preview 1609 ' de ve sürüm 1610 ' de Güncel Dalı sunulmuştur.  

Bu önizleme ile, bir istemcinin hangi dağıtım noktası tarafından kullanılabileceğini yönetme gibi, bir istemcinin kullanabileceği yazılım güncelleştirme noktalarını yönetmek için yeni sınır grubu davranışını kullanın:  

- Sınır gruplarını, bir yazılım güncelleştirme noktasını barındıran bir veya daha fazla sunucuyu ilişkilendirmek üzere yapılandırırsınız.
- Yeni bir yazılım güncelleştirme noktası arayan istemciler, geçerli sınır grubuyla ilişkilendirilmiş bir tane kullanmaya çalışacaktır.
- İstemci geçerli yazılım güncelleştirme noktasına ulaşamazsa ve geçerli sınır grubundan birini bulamazsa, istemci, kullanabileceği yazılım güncelleştirme noktalarının kullanılabilir havuzunu genişletmek için geri dönüş davranışını kullanır.    

Sınır grupları hakkında daha fazla bilgi için, Güncel Dalı içerikte [sınır grupları](../servers/deploy/configure/boundary-groups.md) konusuna bakın.

Ancak, bu önizleme ile yazılım güncelleştirme noktaları için sınır grupları yalnızca kısmen uygulanmıştır. Yazılım güncelleştirme noktaları ekleyebilir ve yazılım güncelleştirme noktaları içeren komşu sınır gruplarını yapılandırabilirsiniz, ancak yazılım güncelleştirme noktaları için geri dönüş süresi henüz desteklenmemektedir ve istemciler, geri dönüşü başlatmadan önce iki saat bekler.

Aşağıda, bu Technical Preview ile yazılım güncelleştirme noktalarına yönelik davranış açıklanmaktadır:  

- **Yeni istemciler, yazılım güncelleştirme noktalarını seçmek için sınır grupları kullanır** . 1701 sürümünü yükledikten sonra yüklediğiniz istemci, istemcinin sınır grubuyla ilişkili olanlardan bir yazılım güncelleştirme noktası seçer.

  Bu, istemcilerin bir yazılım güncelleştirme noktasını istemciler ormanından paylaşanlar listesinden rastgele seçenler için önceki davranışı değiştirir.   

- **Daha önce yüklenen istemciler yeni bir yazılım güncelleştirme noktasını, yeni bir tane bulmaya geri dönüşene kadar kullanmaya devam eder.**
  Daha önce yüklenmiş olan ve zaten bir yazılım güncelleştirme noktası olan istemciler, geri yüklenene kadar bu yazılım güncelleştirme noktasını kullanmaya devam eder. Bu, istemcinin geçerli sınır grubuyla ilişkilendirilmemiş yazılım güncelleştirme noktalarını içerir. Bunlar, güncel sınır grubundan bir yazılım güncelleştirme noktasını bulmayı ve kullanmayı hemen denemez.

  Zaten bir yazılım güncelleştirme noktası olan bir istemci, bu yeni sınır grubu davranışını yalnızca istemci geçerli yazılım güncelleştirme noktasına ulaşamazsa ve geri dönüşü başlattığında kullanmaya başlar.
  Yeni davranışa geçiş yaparken bu gecikme bilerek yapılır. Bunun nedeni, yazılım güncelleştirme noktası değişikliğinin, istemci verileri yeni yazılım güncelleştirme noktasıyla eşitlediği için ağ bant genişliğinin büyük bir kullanımına neden olabilir. Geçişin gecikmesi, tüm istemcileriniz aynı anda yeni yazılım güncelleştirme noktalarına geçiş yapmak zorunda kalmamak için ağınızı doygunluğu önlemeye yardımcı olabilir.

- **Geri dönüş süresi Için yapılandırma:** İstemcilerin yeni bir yazılım güncelleştirme noktası aramak için geri dönüş başlatması için yapılandırma bu Technical Preview 'da desteklenmez. Bu, **geri dönüş süreleri (dakika cinsinden)** için yapılandırma ve farklı sınır grubu ilişkileri Için yapılandırabileceğiniz **hiçbir zaman geri dönüş**içerir.

  Bunun yerine, istemciler, bir istemcinin geçerli yazılım güncelleştirme noktasına geri dönüş başlatılmadan önce iki saat boyunca bağlanmaya çalıştığı, kullanabileceği yeni bir yazılım güncelleştirme noktasını bulmak için geçerli davranışlarını korur.

  Bir istemci geri dönüş kullanır, bir kullanılabilir yazılım güncelleştirme noktası havuzu oluşturmak için geri dönüş için sınır grubu yapılandırmasını kullanır. Bu havuz, istemcilerin *geçerli sınır grubundaki*tüm yazılım güncelleştirme noktalarını, *komşu sınır gruplarını*ve istemcilerin *site varsayılan sınır grubunu*içerir.

- **Varsayılan site sınır grubunu yapılandırın:**  
  *Varsayılan site sınır grubu&lt;sitekoduna>* yazılım güncelleştirme noktası eklemeyi göz önünde bulundurun. Bu, başka bir sınır grubunun üyesi olmayan istemcilerin yazılım güncelleştirme noktası bulmak için geri dönüşmesini sağlar.


Sınır grupları için yazılım güncelleştirme noktalarını yönetmek için, [güncel dalı belgelerindeki yordamları](../servers/deploy/configure/boundary-group-procedures.md)kullanın, ancak yapılandırabileceğiniz geri dönüş sürelerinin henüz yazılım güncelleştirme noktaları için kullanılmadığını unutmayın.


## <a name="hardware-inventory-collects-uefi-information"></a>Donanım envanteri, UEFı bilgilerini toplar
Bir bilgisayarın UEFı modunda başlatılıp başlatılmayacağını belirlemenize yardımcı olmak için yeni bir donanım envanteri sınıfı (**SMS_Firmware**) ve özelliği (**UEFI**) kullanılabilir. Bir bilgisayar UEFı modunda başlatıldığında, **UEFI** özelliği **true**olarak ayarlanır. Bu, varsayılan olarak donanım envanterinde etkinleştirilmiştir. Donanım envanteri hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="improvements-to-operating-system-deployment"></a>İşletim sistemi dağıtımı geliştirmeleri
İşletim sistemi dağıtımı için, çoğu kullanıcı sesli geri bildiriminizin sonucu olan aşağıdaki geliştirmeleri yaptık.
- [**Uygulamaları yüklemeyi uygulamalar görev dizisi adımı için daha fazla uygulama desteği**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): **uygulamaları yüklemek** görev sırası adımında 99 'e yükleyebileceğiniz en fazla uygulama sayısını artırdık. Önceki en büyük sayı 9 uygulamaiydi.
- [**Uygulamayı yüklemek görev sırası adımında birden çok uygulama seçin**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): uygulama ekleme görev dizisi adımına uygulamalar eklediğinizde, uygulamayı yüklemek **için uygulamayı seçin** bölmesinde birden çok uygulama seçebilirsiniz.
- [**Tek başına medyanın süresi doluyor**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): tek başına medya oluşturduğunuzda, medyada isteğe bağlı başlangıç ve sona erme tarihlerini ayarlamak için yeni seçenekler vardır. Bu ayarlar varsayılan olarak devre dışıdır. Tarihler, tek başına medya çalıştırılmadan önce bilgisayardaki sistem saatine göre karşılaştırılır. Sistem saati, sona erme zamanından başlangıç zamanından veya ondan daha eski olduğunda, tek başına medya başlatılmaz. Bu seçenekler, New-CMStandaloneMedia PowerShell cmdlet 'i kullanılarak da kullanılabilir.
- [**Tek başına medyada ek Içerik desteği**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): artık tek başına medyada ek içerik desteklenir. Medyada hazırlanmak üzere ek paketler, sürücü paketleri ve uygulamalar, görev dizisinde başvurulan diğer içerikle birlikte seçebilirsiniz. Daha önce, yalnızca görev dizisinde başvurulan içerikler tek başına medyada hazırlanmıştı.
- [**Sürücüyü otomatik olarak Uygula görev dizisi adımı Için yapılandırılabilir zaman aşımı**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): yeni görev dizisi değişkenleri artık, http Katalog Istekleri yaparken sürücüyü otomatik olarak Uygula görev dizisi adımında zaman aşımı değerini yapılandırmak için kullanılabilir. Aşağıdaki değişkenler ve varsayılan değerler (saniye cinsinden) kullanılabilir:
   - SMSTSDriverRequestResolveTimeOut varsayılan: 60
   - SMSTSDriverRequestConnectTimeOut varsayılan: 60
   - SMSTSDriverRequestSendTimeOut varsayılan: 60
   - SMSTSDriverRequestReceiveTimeOut varsayılan: 480
- [**Paket kimliği artık görev sırası adımlarında görüntülenir**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): bir pakete, sürücü paketine, işletim sistemi görüntüsüne, önyükleme görüntüsüne veya işletim sistemi yükseltme paketine başvuran herhangi bir görev dizisi adımı artık başvurulan NESNENIN paket kimliğini görüntüler. Bir görev dizisi adımı bir uygulamaya başvurduğunda, nesne KIMLIĞI görüntülenir.
- **Windows 10 ADK derleme sürümü tarafından izleniyor**: Windows 10 önyükleme görüntülerini özelleştirirken daha desteklenen bir deneyim sağlamak için WINDOWS 10 ADK artık derleme sürümü tarafından izlenir. Örneğin, site Windows 10, sürüm 1607 için Windows ADK kullanıyorsa, yalnızca sürüm 10.0.14393 olan önyükleme görüntüleri konsolunda özelleştirilebilir. WinPE sürümlerini özelleştirme hakkında daha fazla bilgi için bkz. [önyükleme görüntülerini özelleştirme](../../osd/get-started/customize-boot-images.md).
- **Varsayılan önyükleme görüntüsü kaynak yolu artık değiştirilemez**: varsayılan önyükleme görüntüleri Configuration Manager tarafından yönetilir ve varsayılan önyükleme görüntüsü kaynak yolu artık Configuration Manager konsolunda veya Configuration Manager SDK kullanılarak değiştirilemez. Özel önyükleme görüntüleri için özel bir kaynak yolu yapılandırmaya devam edebilirsiniz.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Bulut tabanlı dağıtım noktalarında yazılım güncelleştirmeleri barındırma
Bu önizleme sürümünden itibaren, bir yazılım güncelleştirme paketini barındırmak için bulut tabanlı bir dağıtım noktası kullanabilirsiniz. Ancak, istemcileri doğrudan Microsoft Update yazılım güncelleştirmelerini indirecek şekilde yapılandırabileceğiniz için, bir yazılım güncelleştirme paketini bulut tabanlı bir dağıtım noktasına dağıtmanın ek maliyetlerini göz önünde bulundurun.

Bulut tabanlı dağıtım noktalarını kullanma hakkında daha fazla bilgi için bkz. Configuration Manager Güncel Dalı için içerikte [bulut tabanlı dağıtım noktası kullanma](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) .

## <a name="validate-device-health-attestation-data-via-management-points"></a>Yönetim noktaları aracılığıyla cihaz durumu kanıtlama verilerini doğrulama

Bu önizleme sürümünden itibaren, bulut veya şirket içi sistem durumu kanıtlama hizmeti için sistem durumu kanıtlama raporlama verilerini doğrulamak üzere yönetim noktalarını yapılandırabilirsiniz. **Yönetim noktası bileşen özellikleri** iletişim kutusundaki yeni bir **Gelişmiş Seçenekler** sekmesi **Şirket içi cihaz sistem durumu kanıtlama hizmeti URL 'Sini** **eklemenize**, **düzenlemenize**veya **kaldırmanıza** olanak tanır. Ayrıca, istemci aracısının **Şirket Içi sistem durumu kanıtlama hizmeti 'Ni kullanması**Için **özel cihaz ayarları** belirtebilirsiniz.  Bu ayar için **Evet** ayarı, bulut tabanlı hizmet yerine şirket içi yönetim noktasına raporlamayı etkinleştirir.

### <a name="try-it-out"></a>Deneyin

- **Yönetim noktasında şirket içi cihaz durumu kanıtlamasını etkinleştirme**<br>  Configuration Manager konsolunda, yönetim noktasına gidin ve **Yönetim noktası bileşen özellikleri** ' ni açın ve ardından **Gelişmiş Seçenekler** sekmesine tıklayın. **Ekle** ' ye tıklayın ve şirket içi URL 'yi (örneğin, https://10.10.10.10) şirket içi **cihaz durumu kanıtlama hizmeti URL 'leri**için) belirtin.
- **İstemci Aracısı için şirket içi yönetim noktası durumu kanıtlama raporlamasını etkinleştirin**<br>Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** ' nı seçin ve çift tıklayın veya yeni bir **özel cihaz ayarları**oluşturun. **Bilgisayar Aracısı** ' nı seçin ve şirket **Içi sistem durumu kanıtlama hizmetini kullan '** ı **Evet**olarak ayarlayın. **Cihaz sistem durumu kanıtlama hizmeti ile Iletişimi etkinleştir** seçeneği **Evet** olarak ayarlanırsa ve **Şirket Içi sistem durumu kanıtlama kullanımı** **Hayır**olarak ayarlanırsa, yönetim noktası bulut tabanlı cihaz sistem durumu kanıtlama hizmeti 'ni kullanır.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Microsoft Azure Kamu Bulutu için OMS bağlayıcısını kullanma
Bu Technical Preview ile, artık Microsoft Azure Kamu buluttaki bir OMS çalışma alanına bağlanmak için Microsoft Operations Management Suite (OMS) bağlayıcısını kullanabilirsiniz.  

Bunu yapmak için, bir yapılandırma dosyasını kamu bulutuna işaret etmek üzere değiştirirsiniz ve sonra OMS bağlayıcısını yüklersiniz.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Microsoft Azure Kamu Bulutu için OMS Bağlayıcısı ayarlama
1. Configuration Manager konsolunun yüklü olduğu herhangi bir bilgisayarda, kamu bulutunu işaret etmek için aşağıdaki yapılandırma dosyasını düzenleyin: *** &lt;cm yükleme yolu> \adminconsole\bin\microsoft.configurationmanagmenet.exe.config***

   **Düzeltmeler**

   *FairFaxArmResourceID* ayar adı için değeri "şuna eşit olacak şekilde değiştirin<https://management.usgovcloudapi.net/">

   - **Özgün:** &lt;Setting Name = "FairFaxArmResourceId" SerializeAs = "String" >   
     &lt;değer>&lt;/değer>   
     &lt;/Setting>

   - **Bilmesini**     
     &lt;ayar adı = "FairFaxArmResourceId" serializeAs = "String" > &lt;değer><https://management.usgovcloudapi.net/&lt;/value>>  
     &lt;/Setting>

   *FairFaxAuthorityResource* ayar adı için değeri "<https://login.microsoftonline.com/>" değerine eşit olacak şekilde değiştirin

   - **Özgün:** &lt;Setting Name = "FairFaxAuthorityResource" SerializeAs = "String" >   
     &lt;değer>&lt;/değer>

   - **Düzenlendi:** &lt;Setting Name = "FairFaxAuthorityResource" SerializeAs = "String" >   
     &lt;değer><https://login.microsoftonline.com/&lt;/value>>

2. Dosyayı İki değişiklikle kaydettikten sonra, Configuration Manager konsolunu aynı bilgisayarda yeniden başlatın ve ardından bu konsolu kullanarak OMS bağlayıcısını yükleyebilirsiniz. Bağlayıcıyı yüklemek için [Configuration Manager verileri Microsoft Operations Management Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)' deki bilgileri kullanın ve Microsoft Azure Kamu buluttaki **Operations Management Suite çalışma alanını** seçin.

3. OMS Bağlayıcısı yüklendikten sonra, siteye bağlanan herhangi bir konsolu kullandığınızda kamu bulutuna bağlantı sağlanır.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Karma MDM için oluşturma sihirbazları 'nda Android ve iOS sürümleri artık hedeflenebilir

Karma mobil cihaz yönetimi (MDM) için bu teknik önizlemede başlayarak, Intune tarafından yönetilen cihazlar için yeni ilkeler ve profiller oluştururken artık belirli Android ve iOS sürümlerini hedeflemenize gerek kalmaz. Bunun yerine, aşağıdaki cihaz türlerinden birini seçersiniz:

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
