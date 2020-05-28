---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager için Technical Preview sürüm 1802 ' de bulunan özellikler hakkında bilgi edinin.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 94208da3eda33cba69f04bbbf42edd08b585c1c4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428185"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Configuration Manager için Technical Preview 1802 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1802 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz. 

Technical Preview 'un bu sürümünü yüklemeden önce [Configuration Manager Için Teknik önizlemeyi](technical-preview.md) gözden geçirin. Bu makalede, Technical Preview kullanımı, sürümler arasında nasıl güncelleştirme yapılacağı ve geri bildirimde bulunmak için genel gereksinimler ve sınırlamalar tamamladığınızda tercihinize.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Bu Technical Preview 'da bilinen sorunlar
- **Pasif modda bir site sunucunuz varsa yeni bir önizleme sürümüne güncelleştirme başarısız olur**. [Pasif modda bir birincil site sunucunuz](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)varsa, bu yeni önizleme sürümüne güncelleştirmeden önce Pasif mod site sunucusunu kaldırmanız gerekir. Siteniz güncelleştirmeyi tamamladıktan sonra Pasif mod site sunucusunu yeniden yükleyebilirsiniz.

  Pasif mod site sunucusunu kaldırmak için:
  1. Configuration Manager konsolunda **Yönetim**  >  **genel bakış**  >  **Site yapılandırması**  >  **sunucuları ve site sistem rolleri**' ne gidin ve Pasif mod site sunucusunu seçin.
  2. **Site sistemi rolleri** bölmesinde, **site sunucusu** rolüne sağ tıklayın ve ardından **rolü kaldır**' ı seçin.
  3. Pasif mod site sunucusuna sağ tıklayın ve ardından **Sil**' i seçin.
  4. Site sunucusu kaldırıldıktan sonra, etkin birincil site sunucusunda hizmeti **CONFIGURATION_MANAGER_UPDATE**yeniden başlatın.
  <!--sms 489412-->


</br>

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Ortak yönetim kullanarak Intune 'a iş yükünü Endpoint Protection geçiş    
<!-- 1357365 -->
Bu sürümde, artık ortak yönetimi etkinleştirdikten sonra Configuration Manager Endpoint Protection iş yükünü Intune 'a geçiş yapabilirsiniz. Endpoint Protection iş yükünü dengelemek için ortak yönetim özellikleri sayfasına gidin ve kaydırıcı çubuğu Configuration Manager ' dan **pilot** ' a veya **tümüne**taşıyın. Ayrıntılar için bkz. [Windows 10 cihazlar Için ortak yönetim](../../comanage/overview.md).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Windows Dağıtım Iyileştirmesini Configuration Manager sınır grupları kullanacak şekilde yapılandırma
<!-- 1324696 -->
Şirket ağınızda ve Uzak ofislerde içerik dağıtımını tanımlamak ve düzenlemek için Configuration Manager sınır gruplarını kullanırsınız. [Windows teslim iyileştirme](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) , Windows 10 cihazları arasında içerik paylaşmak için bulut tabanlı ve eşler arası bir teknolojidir. Bu sürümden başlayarak, eşler arasında içerik paylaşırken sınır gruplarınızı kullanmak için teslim Iyileştirmesini yapılandırın. Yeni bir istemci ayarı, sınır grubu tanımlayıcısını istemcideki teslim Iyileştirme grubu tanımlayıcısı olarak uygular. İstemci, teslim Iyileştirme bulut hizmeti ile iletişim kurduğunda, istenen içeriğe sahip eşleri bulmak için bu tanımlayıcıyı kullanır. 

### <a name="prerequisites"></a>Ön koşullar
- Teslim Iyileştirme yalnızca Windows 10 istemcilerinde kullanılabilir

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

1. Configuration Manager konsolu, **Yönetim** çalışma alanı, **istemci ayarları** düğümünde özel bir istemci cihaz ayarları ilkesi oluşturun.
2. Yeni **teslim iyileştirme** grubunu seçin.
3. **Teslim Iyileştirme grubu kimliği için Configuration Manager sınır gruplarını kullan**ayarını etkinleştirin.

Daha fazla bilgi için [teslim iyileştirme seçeneklerinde](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization) **Grup** teslim modu seçeneğine bakın.



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi aracılığıyla Windows 10 yerinde yükseltme görev dizisi
<!-- 1357149 -->

Windows 10 [yerinde yükseltme görev sırası](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) artık, [bulut yönetimi ağ geçidi](../clients/manage/cmg/plan-cloud-management-gateway.md)aracılığıyla yönetilen internet tabanlı istemcilere dağıtımı desteklemektedir. Bu özellik, uzak kullanıcıların şirket ağına bağlanmasına gerek kalmadan Windows 10 ' a daha kolay yükseltme yapmasına olanak sağlar. 

Yerinde yükseltme görev sırası tarafından başvurulan tüm içeriklerin bir [bulut dağıtım noktasına](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)dağıtıldığından emin olun. Aksi halde cihazlar görev sırasını çalıştıramıyor.

Bir yükseltme görev dizisi dağıttığınızda, aşağıdaki ayarları kullanın:
- Dağıtımın Kullanıcı deneyimi sekmesinde **Internet 'te istemci için görev dizisinin çalışmasına Izin verin**.
- Dağıtımın dağıtım noktaları sekmesinde, **görev sırasını başlatmadan önce tüm içeriği yerel olarak indirin**. **Çalışan görev dizisi için gerektiğinde içeriği yerel olarak indir** gibi diğer seçenekler bu senaryoda çalışmaz. Görev sırası altyapısı şu anda bir bulut dağıtım noktasından içerik alamıyor. Configuration Manager istemci, görev dizisini başlatmadan önce bulut dağıtım noktasındaki içeriği indirmelidir.
- (*Isteğe bağlı*) Dağıtımın Genel sekmesinde **Bu görev dizisinin Içeriğini önceden indirin**. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 yerinde yükseltme görev dizisinde iyileştirmeler
<!-- 1357425 -->
Windows 10 yerinde yükseltme için varsayılan görev sırası şablonu, yükseltme işleminden önce ve sonra eklemek için önerilen eylemleri içeren ek gruplar içerir. Bu eylemler, cihazları Windows 10 ' a başarıyla yükselten birçok müşteri arasında ortaktır. 

### <a name="new-groups-under-prepare-for-upgrade"></a>**Yükseltmeye hazırlanma** altındaki yeni gruplar
- **Pil denetimleri**: bilgisayarın pil veya kablolu güç kullanıp kullanmadığını denetlemek için bu gruba adımlar ekleyin. Bu eylem, bu denetimi gerçekleştirmek için özel bir betik veya yardımcı program gerektirir.
- **Ağ/kablolu bağlantı denetimleri**: bilgisayarın bir ağa bağlı olup olmadığını denetlemek için bu gruba adımlar ekleyin ve kablosuz bağlantı kullanmıyor. Bu eylem, bu denetimi gerçekleştirmek için özel bir betik veya yardımcı program gerektirir.
- **Uyumsuz uygulamaları kaldır**: Windows 10 ' un bu sürümüyle uyumlu olmayan uygulamaları kaldırmak için bu gruba adımlar ekleyin. Bir uygulamayı kaldırma yöntemi farklılık gösterir. Uygulama Windows Installer kullanıyorsa, uygulamanın Windows Installer dağıtım türü özelliklerindeki **Programlar** sekmesinden **Program kaldır** komut satırını kopyalayın. Ardından, program Kaldır komut satırı ile bu gruba bir **komut satırı Çalıştır** adımı ekleyin. Örneğin: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Uyumsuz sürücüleri kaldır**: Windows 10 ' un bu sürümü ile uyumlu olmayan sürücüleri kaldırmak için bu gruba adımlar ekleyin.
- **Üçüncü taraf güvenliği kaldır/askıya al**: virüsten koruma gibi üçüncü taraf güvenlik programlarını kaldırmak veya askıya almak için bu gruba adımlar ekleyin.
   - Üçüncü taraf bir disk şifreleme programı kullanıyorsanız, **/Yansıtıctdrivers** [komut satırı seçeneğiyle](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)Windows kurulumu için şifreleme sürücüsünü belirtin. Bu gruptaki görev dizisine bir [görev dizisi değişkeni ayarlama](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) adımı ekleyin. Görev sırası değişkenini **Osdsetupadditionalupgradeoptions**olarak ayarlayın. Değeri, sürücünün yoluyla **/Yansıtıctdriver** olarak ayarlayın. Bu [görev dizisi eylem değişkeni](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) , görev sırası tarafından kullanılan Windows kurulumu komut satırını ekler. Bu işlemle ilgili ek yönergeler için yazılım satıcınıza başvurun.

### <a name="new-groups-under-post-processing"></a>**Işlem sonrası** yeni gruplar
- **Kurulum tabanlı sürücüleri Uygula**: paketten kurulum tabanlı sürücüler (. exe) yüklemek için bu gruba adımlar ekleyin.
- **Üçüncü taraf güvenliği yüklemek/etkinleştirmek**: virüsten koruma gibi üçüncü taraf güvenlik programlarını yüklemek veya etkinleştirmek için bu gruba adımlar ekleyin. 
- **Windows varsayılan uygulamalarını ve Ilişkilendirmelerini ayarla**: Windows varsayılan uygulamalarını ve dosya ilişkilendirmelerini ayarlamak için bu gruba adımlar ekleyin. Önce istediğiniz uygulama ilişkilendirmelerinizi içeren bir başvuru bilgisayarı hazırlayın. Ardından dışarı aktarmak için aşağıdaki komut satırını çalıştırın: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>XML dosyasını bir pakete ekleyin. Sonra bu grupta bir [komut satırı Çalıştır](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) adımı ekleyin. XML dosyasını içeren paketi belirtin ve ardından aşağıdaki komut satırını belirtin: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Daha fazla bilgi için bkz. [Varsayılan uygulama Ilişkilendirmelerini dışarı veya içeri](https://docs.microsoft.com/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)aktarma.
- **Özelleştirmeleri ve kişiselleştirmeyi uygulama**: program gruplarını düzenleme gibi Başlat menüsü özelleştirmeleri uygulamak için bu gruba adımlar ekleyin. Daha fazla bilgi için bkz. [Başlangıç ekranını özelleştirme](https://docs.microsoft.com/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Ek öneriler
- Windows [10 yükseltme hatalarını çözmek](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)için Windows belgelerini gözden geçirin. Bu makale, yükseltme işlemiyle ilgili ayrıntılı bilgileri de içerir.
- **Hazır olma durumunu denetle** adımında **minimum boş DISK alanı (MB) sağlayın**. Değeri 32 bit işletim sistemi yükseltme paketi için en az **16384** (16 GB) veya 64-bit için **20480** (20 GB) olarak ayarlayın. 
- İlkeyi indirmeyi yeniden denemek için **SMSTSDownloadRetryCount** [yerleşik görev dizisi değişkenini](../../osd/understand/task-sequence-variables.md) kullanın. Şu anda varsayılan olarak istemci iki kez yeniden denenir; Bu değişken iki (2) olarak ayarlanır. İstemcileriniz kablolu bir kurumsal ağ bağlantısında değilse, istemcinin ilkeyi almasına yardımcı olur. Bu değişkenin kullanılması, olumsuz bir yan etkiye neden olmaz, bu, ilke indirilemez gecikmez.<!-- 501016 --> Ayrıca, varsayılan 15 saniyeden **SMSTSDownloadRetryDelay** değişkenini de artırın.
- Satır içi uyumluluk değerlendirmesi gerçekleştirin. 
   - **Yükseltme Için hazırlama** grubunun başlarında Ikinci bir **yükseltme işletim sistemi** adımı ekleyin. *Yükseltme değerlendirmesini*adlandırın. Aynı yükseltme paketini belirtin ve ardından **yükseltmeyi başlatmadan Windows Kurulumu uyumluluk taraması gerçekleştirme**seçeneğini etkinleştirin. Seçenekler sekmesinde **hata durumunda devam et '** i etkinleştirin. 
   - Bu *yükseltme değerlendirmesi* adımını hemen takip eden bir **komut satırını Çalıştır** adımı ekleyin. Aşağıdaki komut satırını belirtin:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>**Seçenekler** sekmesinde, aşağıdaki koşulu ekleyin: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Bu dönüş kodu, hiçbir sorun olmadan başarılı bir uyumluluk taraması olan MOSETUP_E_COMPAT_SCANONLY (0xC1900210) değerinin ondalık eşdeğeridir. *Yükseltme değerlendirmesi* adımı başarılı olursa ve bu kodu döndürürse, bu adım atlanır. Aksi takdirde, değerlendirme adımı başka bir dönüş kodu döndürürse, bu adım görev sırasını Windows Kurulumu uyumluluk taramasından döndürülen kodla başarısız olur.
   - Daha fazla bilgi için bkz. [işletim sistemini yükseltme](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).
- Bu görev sırası sırasında cihazı BIOS 'tan UEFı 'ye değiştirmek istiyorsanız, [yerinde yükseltme SıRASıNDA BIOS 'TAN UEFI 'ye dönüştürme](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)bölümüne bakın.

Daha fazla öneriniz veya önerileriniz varsa, şeridin **giriş** sekmesinden **geri bildirim** gönderin.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>PXE 'yi destekleyen dağıtım noktalarında iyileştirmeler
<!-- 1357580 -->
İlk olarak Technical Preview sürüm 1706 ' de sunulan [yenı PXE işlevselliğinin](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6) davranışını netleştirmek Için, **destek IPv6** seçeneğini yeniden adlandırdık. Dağıtım noktası özelliklerinin **PXE** sekmesinde, **Windows Dağıtım HIZMETI olmadan bir PXE yanıtlayıcısını etkinleştir**' i işaretleyin. 

Bu seçenek, dağıtım noktasında Windows Dağıtım Hizmetleri (WDS) gerektirmeyen bir PXE yanıtlayıcıu sunar. Bu yeni seçeneği, zaten PXE özellikli olan bir dağıtım noktasında etkinleştirirseniz, Configuration Manager WDS hizmetini askıya alır. Bu yeni seçeneği devre dışı bırakırsanız ancak **istemciler IÇIN PXE desteğini hala etkinleştirirseniz**, DAĞıTıM noktası WDS 'yi yeniden etkinleştirir.

WDS gerekli olmadığından, PXE 'yi destekleyen dağıtım noktası Windows Server Core dahil bir istemci veya sunucu işletim sistemi olabilir. Bu yeni PXE Yanıtlayıcı hizmeti IPv6 'yı desteklemeye devam eder ve ayrıca uzak ofislerdeki PXE 'yi destekleyen dağıtım noktalarının esnekliğini geliştirir.

> [!NOTE]
> Bu hizmet, Technical Preview sürüm 1712 ' deki [istemci tabanlı PXE Yanıtlayıcı hizmeti](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) ile aynı temel teknolojiyi kullanır. Bu özellik dağıtım noktası rolünün ek yükünü gerektirmez.

### <a name="multicast"></a>Noktalı
Dağıtım noktası özelliklerinin **çok noktaya** yayın sekmesinde çok noktaya yayını etkinleştirmek ve yapılandırmak için, DAĞıTıM noktasının WDS kullanması gerekir. 
- **İstemciler IÇIN PXE desteğini etkinleştirir** ve çok **noktaya yayının birden çok istemciye eşzamanlı olarak veri göndermesini**Isterseniz, **WINDOWS dağıtım hizmeti olmadan bir PXE yanıtlayıcıu etkinleştiremezsiniz**.
- **İstemciler IÇIN PXE desteğini etkinleştirir** ve **Windows Dağıtım HIZMETI olmadan bir PXE Yanıtlayıcı 'yı etkinleştirirseniz**, çok **noktaya yayının birden çok Istemciye eşzamanlı olarak veri göndermesini olanaklı hale** yükleyemezsiniz



## <a name="deployment-templates-for-task-sequences"></a>Görev dizileri için dağıtım şablonları
<!-- 1357391 -->
Görev dizileri için Dağıtım Sihirbazı artık bir dağıtım şablonu oluşturabilir. Dağıtım şablonu, dağıtım oluşturmak için var olan veya yeni bir görev dizisine kaydedilip uygulanabilir. 

### <a name="try-it-out"></a>Deneyin!  
Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin. 

 **Yeni bir görev dizisi dağıtımı için dağıtım şablonu oluşturma** <br/> 
1. **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.
2. Bir görev dizisine sağ tıklayıp **Dağıt**' ı seçin. 
3. **Genel** sekmesinde artık **dağıtım şablonu**' nu seçme seçeneği vardır. 
4. Görev dizisinin dağıtım ayarlarını seçerek **Yazılım Dağıtma Sihirbazı** ile devam edin. 
5. **Yazılım Dağıtma Sihirbazı**'nın **Özet** sekmesine ulaştığınızda, **şablon olarak kaydet**' e tıklayın.
6. Şablona bir ad verin ve şablonda kaydedilecek ayarları seçin. 
7. **Kaydet**’e tıklayın. Şablon artık **dağıtım şablonu seç** seçeneğinde kullanılabilir.



## <a name="product-lifecycle-dashboard"></a>Ürün yaşam döngüsü panosu
<!--1319632-->
Yeni [ürün yaşam döngüsü panosu](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md) , Configuration Manager ile yönetilen cihazlarda yüklü Microsoft ürünleri Için Microsoft ürün yaşam döngüsü ilkesinin durumunu gösterir. Pano, ortamınızda Microsoft ürünleriyle ilgili bilgiler sağlar, desteklenebilirlik State ve bitiş tarihlerini destekler. Bu panoyu, her ürün için desteğin kullanılabilirliğini anlamak için kullanabilirsiniz. 

Yaşam döngüsü panosuna erişmek için Configuration Manager konsolunda **varlıklar ve uyum**  > **varlık yönetim bilgileri**  > **ürün yaşam döngüsü** ' ne gidin



## <a name="improvements-to-reporting"></a>Raporlama geliştirmeleri
<!--1357653-->
[Geri bildirimlerinizin](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) bir sonucu olarak, **belirli bir koleksiyon Için Windows 10 Bakımı ayrıntılarını**yeni bir rapor ekledik. Bu rapor, Windows 10 cihazlarının kaynak KIMLIĞI, NetBIOS adı, IŞLETIM sistemi adı, işletim sistemi sürüm adı, derleme, işletim sistemi dalı ve bakım durumunu gösterir. Rapora erişmek için, **Monitoring**  > **Reporting**  > **Reports**  > belirli bir koleksiyon için izleme raporlama raporları**işletim sistemleri**  > **Windows 10 bakım ayrıntıları**' na gidin.



## <a name="improvements-to-software-center"></a>Yazılım Merkezi geliştirmeleri
<!--1357592-->
[Geri bildirimlerinizin](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) bir sonucu olarak, yüklü uygulamalar artık yazılım merkezi 'nde gizlenebilir. Zaten yüklü olan uygulamalar, bu seçenek etkinleştirildiğinde, uygulamalar sekmesinde artık gösterilmez. 

### <a name="try-it-out"></a>Deneyin!
Yazılım Merkezi istemci ayarlarındaki **Yazılım Merkezi 'Nde yüklü uygulamaları Gizle** ayarını etkinleştirin. Son Kullanıcı bir uygulama yüklediğinde yazılım merkezi 'nin davranışını gözlemleyin.



## <a name="improvements-to-run-scripts"></a>Betikleri çalıştırma geliştirmeleri
<!--1236459-->
[Betikleri Çalıştır](../../apps/deploy-use/create-deploy-scripts.md) ÖZELLIĞI artık JSON biçimlendirmesini kullanarak betik çıkışı döndürüyor. Bu biçim sürekli olarak okunabilir bir betik çıkışı döndürür. Çalıştırılmayan betikler, döndürülen çıktıyı alamaz. 



## <a name="boundary-group-fallback-for-management-points"></a>Yönetim noktaları için sınır grubu geri dönüşü
<!-- 1324594 -->
Bu sürümden itibaren, [sınır grupları](../servers/deploy/configure/boundary-groups.md)arasındaki yönetim noktaları için geri dönüş ilişkilerini yapılandırabilirsiniz. Bu davranış, istemcilerin kullandığı yönetim noktaları için daha fazla denetim sağlar. Sınır grubu özelliklerinin **ilişkiler** sekmesinde, yönetim noktası için yeni bir sütun vardır. Yeni bir geri dönüş sınır grubu eklediğinizde, yönetim noktası için geri dönüş süresi şu anda her zaman sıfırdır (0). Bu davranış, sitenin varsayılan sınır grubundaki **varsayılan davranış** için aynıdır.

Daha önce, güvenli bir ağda korumalı bir yönetim noktanız olduğunda yaygın bir sorun oluşur. Ana şirket ağındaki istemciler, bir güvenlik duvarı genelinde iletişim kuramasa bile, bu korumalı yönetim noktasını içeren ilkeyi alır. Bu sorunu gidermek için, istemcilerin yalnızca iletişim kurabileceği yönetim noktalarına geri eklendiğinden emin olmak için **hiçbir şekilde geri dönüş** seçeneğini kullanın.

Siteyi bu sürüme yükseltirken, Configuration Manager İnternet 'e yönelik olmayan tüm yönetim noktalarını site varsayılan sınır grubuna ekler. Bu yükseltme davranışı, eski istemci sürümlerinin yönetim noktalarıyla iletişim kurmaya devam etmesini sağlar. Bu özellikten tam anlamıyla yararlanabilmek için, yönetim noktalarınızı istenen sınır gruplarına taşıyın.

Yönetim noktası sınır grubu geri dönüşü, istemci yüklemesi sırasında davranışı değiştirmez (CCMSetup). Komut satırı/MP parametresini kullanarak ilk yönetim noktasını belirtmezse, yeni istemci kullanılabilir yönetim noktalarının tam listesini alır. İlk önyükleme işlemi için istemci, erişebileceği ilk yönetim noktasını kullanır. İstemci sitesiyle kaydolduğunda, bu yeni davranışla birlikte yönetim noktası listesini doğru şekilde sıralanmış olarak alır. 

### <a name="prerequisites"></a>Ön koşullar
- [Tercih edilen yönetim noktalarını](../servers/deploy/configure/boundary-groups.md#bkmk_preferred)etkinleştirin. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması** ' nı genişletin ve **siteler**' i seçin. Şeritte **Hiyerarşi ayarları** ' na tıklayın. **Genel** sekmesinde, **istemcileri sınır gruplarında belirtilen yönetim noktalarını kullanmayı tercih eder**. 

### <a name="known-issues"></a>Bilinen sorunlar
- İşletim sistemi dağıtım işlemlerinde sınır grupları farkında değildir.

### <a name="troubleshooting"></a>Sorun giderme
Yeni girişler **LocationServices. log**dosyasında görünür. **Yerleşim** özniteliği aşağıdaki durumlardan birini tanımlar:
- 0: bilinmiyor
- 1: belirtilen yönetim noktası, geri dönüş için yalnızca site varsayılan sınır grubunda bulunur
- 2: belirtilen yönetim noktası uzak veya komşu sınır grubunda. Yönetim noktası hem komşu hem de site varsayılan sınır gruplarında olduğunda, konum 2 ' dir.
- 3: belirtilen yönetim noktası yerel veya geçerli sınır grubunda. Yönetim noktası, bir komşu veya site varsayılan sınır grubu ile birlikte geçerli sınır grubunda olduğunda, konum 3 ' dir. Hiyerarşi Ayarları ' nda tercih edilen yönetim noktaları ayarını etkinleştirmezseniz, yönetim noktasının hangi sınır grubuna bakılmaksızın konum her zaman 3 olur.

İstemciler önce yerel yönetim noktalarını (konum 3), uzak ikinci (konum 2), ardından geri dönüş (konum 1) kullanır. 

Bir istemci on dakika içinde beş hata aldığında ve geçerli sınır grubundaki bir yönetim noktasıyla iletişim kuramazsa, bir komşunuzun veya sitenin varsayılan sınır grubundaki bir yönetim noktasıyla iletişim kurmayı dener. Geçerli sınır grubundaki yönetim noktası daha sonra yeniden çevrimiçi duruma gelirse, istemci sonraki yenileme döngüsündeki yerel yönetim noktasına geri döner. Yenileme çevrimi 24 saattir veya Configuration Manager Aracı hizmeti yeniden başlatılır.



## <a name="improved-support-for-cng-certificates"></a>CNG sertifikaları için geliştirilmiş destek
<!-- 1357314 -->
Configuration Manager (geçerli dal) sürüm 1710, [şifreleme: yeni nesil (CNG) sertifikaları](../plan-design/network/cng-certificates-overview.md)destekler. Sürüm 1710, çeşitli senaryolarda istemci sertifikalarına yönelik desteği kısıtlar. 

Bu Technical Preview sürümünden itibaren, aşağıdaki HTTPS etkin sunucu rolleri için CNG sertifikalarını kullanın:
- Yönetim noktası
- Dağıtım noktası
- Yazılım güncelleştirme noktası

[Desteklenmeyen senaryoların](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios) listesi aynı kalır.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Azure Resource Manager için bulut yönetimi ağ geçidi desteği
<!-- 1324735 -->
[Bulut yönetimi ağ geçidinin](../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) bir örneğini oluştururken, sihirbaz artık **Azure Resource Manager dağıtımı**oluşturma seçeneği sağlar. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) , tüm çözüm kaynaklarının, [kaynak grubu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)olarak adlandırılan tek bir varlık olarak yönetilmesine yönelik modern bir platformdur. Azure Resource Manager ile CMG 'yi dağıttığınızda, site kimlik doğrulaması yapmak ve gerekli bulut kaynaklarını oluşturmak için Azure Active Directory (Azure AD) kullanır. Bu modernlanmış dağıtım, klasik Azure Yönetim sertifikası gerektirmez.  

CMG Sihirbazı yine de Azure Yönetim sertifikası kullanan **Klasik hizmet dağıtımı** için seçenek sağlar. Kaynakların dağıtımını ve yönetimini basitleştirmek için, tüm yeni CMG örnekleri için Azure Resource Manager dağıtım modelini kullanmanızı öneririz. Mümkünse, var olan CMG örneklerini Kaynak Yöneticisi aracılığıyla yeniden dağıtın.

Configuration Manager var olan klasik CMG örneklerini Azure Resource Manager dağıtım modeline geçirmez. Azure Resource Manager dağıtımlarını kullanarak yeni CMG örnekleri oluşturun ve ardından klasik CMG örneklerini kaldırın. 

> [!IMPORTANT]
> Bu özellik, Azure bulut hizmeti sağlayıcıları (CSP) için desteği etkinleştirmez. Azure Resource Manager ile CMG dağıtımı, CSP 'nin desteklemediği klasik bulut hizmetini kullanmaya devam eder. Daha fazla bilgi için bkz. [Azure CSP 'de kullanılabilir Azure hizmetleri](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Ön koşullar
- [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md)ile tümleştirme. Azure AD Kullanıcı keşfi gerekli değildir.
- Azure Yönetim sertifikası dışında, [bulut yönetimi ağ geçidi için aynı gereksinimler](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements).

### <a name="try-it-out"></a>Deneyin!  
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

1. Configuration Manager konsolunda, **Yönetim** çalışma alanında, **Cloud Services**' i genişletin ve **bulut yönetimi ağ geçidi**' yı seçin. Şeritte **bulut yönetimi ağ geçidi oluştur** ' a tıklayın. 
2. **Genel** sayfasında, **Azure Resource Manager dağıtımı**' nı seçin. Azure abonelik yönetici hesabıyla kimlik doğrulamak için **oturum aç** ' a tıklayın. Sihirbaz, geri kalan alanları tümleştirme önkoşulu sırasında depolanan Azure AD abonelik bilgilerini otomatik olarak doldurur. Birden çok aboneliğiniz varsa, kullanılacak istediğiniz aboneliği seçin. **İleri**’ye tıklayın.  
3. **Ayarlar** sayfasında, sunucu PKI sertifika dosyasını her zamanki gibi sağlayın. Bu sertifika, Azure 'da CMG hizmet adını tanımlar. **Bölgeyi**seçin ve ardından **Yeni oluştur** veya **mevcut olanı kullan**' ı seçerek bir kaynak grubu seçeneğini belirleyin. Yeni kaynak grubu adını girin veya açılan listeden var olan bir kaynak grubunu seçin. 
4. Sihirbazı tamamlayın.

> [!NOTE] 
> Seçili Azure AD Server uygulaması için, Azure abonelik **katılımcısı** iznini atar. 

Hizmet bağlantı noktasındaki **CloudMgr. log** ile hizmet dağıtımı ilerlemesini izleyin.



## <a name="approve-application-requests-for-users-per-device"></a>Cihaz başına Kullanıcı için uygulama isteklerini Onayla
<!-- 1357015 -->
Bu sürümden itibaren, Kullanıcı onay gerektiren bir uygulama istediğinde, belirli cihaz adı artık isteğin bir parçasıdır. Yönetici isteği onayladığında, Kullanıcı yalnızca bu cihaza uygulamayı kurabilir. Kullanıcı başka bir cihaza uygulamayı yüklemek için başka bir istek göndermesi gerekir. 

> [!NOTE]
> Bu özellik isteğe bağlıdır. Bu yayına güncelleştirme yaparken, bu özelliği güncelleştirme sihirbazında etkinleştirin. Alternatif olarak, daha sonra konsolundaki özelliği etkinleştirin. Daha fazla bilgi için, bkz. [Enable optional features from updates](../servers/manage/install-in-console-updates.md#bkmk_options).

### <a name="prerequisites"></a>Ön koşullar
- Configuration Manager istemcisini en son sürüme yükseltme
- İstemci ayarını etkinleştir [Bilgisayar Aracısı](../clients/deploy/about-client-settings.md#computer-agent) grubunda **yeni yazılım merkezi 'ni kullan**

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

1. Bir uygulamayı bir kullanıcı koleksiyonuna kullanılabilir olarak dağıtın.
2. **Dağıtım ayarları** sayfasında, seçeneği etkinleştirin: **bir yöneticinin cihazdaki bu uygulama için bir isteği onaylaması gerekir**.
3. Hedeflenen kullanıcı olarak, uygulama için bir istek göndermek üzere yazılım merkezi 'ni kullanın. 
4. Configuration Manager konsolunun **yazılım kitaplığı** çalışma alanında **uygulama yönetimi** altında **onay isteklerini** görüntüleyin. Artık her istek için listede bir **cihaz** sütunu var. İstek üzerinde eylem gerçekleştirdiğinizde, uygulama Isteği iletişim kutusu ayrıca kullanıcının isteği gönderdiği cihaz adını da içerir.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Azure AD 'ye katılmış cihazlarda Kullanıcı tarafından kullanılabilen uygulamalara gözatıp yüklemek için yazılım merkezi 'ni kullanma
<!-- 1322613 -->
Uygulamaları kullanıcılara kullanılabilir olarak dağıtırsanız, artık Azure Active Directory (Azure AD) cihazlarındaki Yazılım Merkezi aracılığıyla bunlara göz atabilir ve bunları yükleyebilirler.  

### <a name="prerequisites"></a>Ön koşullar
- Yönetim noktasında HTTPS 'yi etkinleştir
- Siteyi [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md) ile tümleştirme
- Bir uygulamayı bir kullanıcı koleksiyonuna kullanılabilir olarak dağıtma
- Herhangi bir uygulama içeriğini bir [bulut dağıtım noktasına](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) dağıtma
- İstemci ayarını etkinleştir [Bilgisayar Aracısı](../clients/deploy/about-client-settings.md#computer-agent) grubunda **yeni yazılım merkezi 'ni kullan**
- İstemci şu şekilde olmalıdır: 
   - Windows 10
   - Bulut etki alanına katılmış olarak da bilinen Azure AD 'ye katılmış
- Internet tabanlı istemcileri desteklemek için:
    - [Bulut yönetimi ağ geçidi](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - İstemci ayarını etkinleştir: [Istemci ilkesi](../clients/deploy/about-client-settings.md#client-policy) grubundaki **Internet istemcilerinden gelen Kullanıcı ilkesi isteklerini etkinleştir**
- Şirket ağındaki istemcileri desteklemek için:
    - Bulut dağıtım noktasını istemciler tarafından kullanılan bir sınır grubuna ekleyin
    - İstemciler, HTTPS özellikli yönetim noktasının tam etki alanı adını (FQDN) çözümleyebilmelidir



## <a name="report-on-windows-autopilot-device-information"></a>Windows AutoPilot cihaz bilgileri hakkında rapor
<!-- 1351442 -->
Windows AutoPilot, yeni Windows 10 cihazlarını modern bir şekilde ekleme ve yapılandırma çözümüdür. Daha fazla bilgi için bkz. [Windows Autopilot 'e genel bakış](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Windows AutoPilot ile var olan cihazları kaydetmenin bir yöntemi, cihaz bilgilerini Iş ve eğitim için Microsoft Store karşıya yüklemedir. Bu bilgilere cihaz seri numarası, Windows ürün tanımlayıcısı ve bir donanım tanımlayıcısı dahildir. Bu cihaz bilgilerini toplamak ve raporlamak için Configuration Manager kullanın. 

### <a name="prerequisites"></a>Ön koşullar
- Bu cihaz bilgileri yalnızca Windows 10, sürüm 1703 ve üzeri istemciler için geçerlidir

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

1. Configuration Manager konsolunda, **izleme** çalışma alanında, **Raporlama** düğümünü genişletin, **raporlar**' ı genişletin ve **donanım-genel** düğümünü seçin.
2. Yeni rapor, **Windows Autopilot cihaz bilgilerini** çalıştırın ve sonuçları görüntüleyin. 
3. Rapor görüntüleyicisinde **dışarı aktar** simgesine tıklayın ve **CSV (virgülle sınırlandırılmış)** seçeneğini belirleyin.
4. Dosyayı kaydettikten sonra Iş ve eğitim için Microsoft Store verileri karşıya yükleyin. Daha fazla bilgi için bkz. [iş ve eğitim için Microsoft Store cihaz ekleme](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Windows Defender Exploit Guard için Configuration Manager Ilkelerine yönelik iyileştirmeler
<!-- 1356220 -->
[Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)Için Configuration Manager saldırı yüzeyi azaltma ve denetimli klasör erişim bileşenleri için ek ilke ayarları eklenmiştir.

**Denetimli klasör erişimi için yeni ayarlar**<br/>
Denetlenen klasör erişimini yapılandırırken iki ek seçenek vardır: **yalnızca disk kesimlerini engelle** ve **yalnızca disk kesimlerini denetle**. Bu iki ayar, denetlenen klasör erişiminin yalnızca önyükleme kesimleri için etkinleştirilmesini sağlar ve belirli klasörlerin veya varsayılan korumalı klasörlerin korumasını etkinleştirmez. 

**Saldırı yüzeyi azaltma için yeni ayarlar**
- Fidye yazılımı ile gelişmiş koruma kullanın.
- Windows yerel güvenlik yetkilisi alt sisteminden kimlik bilgisi çalınmasını engelleyin. 
- Bir yaygınlık, yaş veya güvenilenler listesi kriterine uymadıkları sürece yürütülebilir dosyaları engeller. 
- USB’den çalışan güvenilmeyen ve imzasız işlemleri engeller.



## <a name="microsoft-edge-browser-policies"></a>Microsoft Edge tarayıcı ilkeleri
<!-- 1357310 -->
Windows 10 istemcilerinde [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) Web tarayıcısını kullanan müşteriler için artık birkaç Microsoft Edge ayarını yapılandırmak üzere bir Configuration Manager uyumluluk ayarları ilkesi oluşturabilirsiniz. Bu ilke şu anda aşağıdaki ayarları içerir:
- **Microsoft Edge tarayıcısını varsayılan olarak ayarla**: Web tarayıcısı için Windows 10 varsayılan uygulama ayarını Microsoft Edge olarak yapılandırır
- **Adres çubuğu açılır öğesine Izin ver**: Windows 10, sürüm 1703 veya üstünü gerektirir. Daha fazla bilgi için bkz. [Allowaddressbardropı tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Microsoft tarayıcıları arasında sık kullanılanlara eşitlemeye Izin ver**: Windows 10, sürüm 1703 veya üstünü gerektirir. Daha fazla bilgi için bkz. [Syncfavoritesbetweenıeandmicrosoftedge Browser ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Çıkışta tarama verilerini temizlemeye Izin ver**: Windows 10, sürüm 1703 veya üstünü gerektirir. Daha fazla bilgi için bkz. [Clearbrowsingdataonexit Browser ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Üst bilgileri Izlememe Izin ver**: daha fazla bilgi için bkz. [allowdonottrack tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Otomatik doldurmaya Izin ver**: daha fazla bilgi için bkz. [allowotomatik doldurma tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Tanımlama bilgilerine Izin ver**: daha fazla bilgi için bkz. [AllowCookies tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Açılır pencere engelleyiciye Izin ver**: daha fazla bilgi için bkz. [allowpopup Browser Policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Adres çubuğunda arama önerilerine Izin ver**: daha fazla bilgi için bkz. [Allowsearchmülationsınaddressbar tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Internet Explorer 'a intranet trafiği gönderilmesine Izin ver**: daha fazla bilgi için bkz. [SendIntranetTraffictoInternetExplorer Browser Policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Parola Yöneticisi 'Ne Izin ver**: daha fazla bilgi için bkz. [allowpasswordmanager tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Geliştirici Araçları Izin ver**: daha fazla bilgi için bkz. [AllowDeveloperTools Browser Policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Uzantılara Izin ver**: daha fazla bilgi için bkz. [AllowExtensions tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Ön koşullar
- Azure Active Directory katılmış Windows 10 istemcisi. 

### <a name="known-issues"></a>Bilinen sorunlar
- Şirket içi etki alanına katılmış cihazlar bu ilkeyi bu sürümde uygulayamaz. Bu sorun, karma etki alanına katılmış cihazlar için de geçerlidir.

### <a name="try-it-out"></a>Deneyin!  
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

**İlkeyi oluşturma**
1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Uyumluluk ayarları** ' nı genişletin ve yeni **Microsoft Edge tarayıcı profilleri** düğümünü seçin. **Microsoft Edge tarayıcı Ilkesi oluşturmak**için şerit seçeneğine tıklayın.
2. İlke için bir **ad** belirtin, isteğe bağlı olarak bir **Açıklama**girin ve **İleri**' ye tıklayın.
3. **Ayarlar** sayfasında, bu ilkeye dahil edilecek ayarlar için **yapılandırılan** değeri değiştirin ve **İleri**' ye tıklayın.
4. **Desteklenen platformlar** sayfasında, bu ilkenin uygulanacağı işletim sistemi sürümlerini ve mimarilerini seçin ve **İleri**' ye tıklayın. 
5. Sihirbazı tamamlayın.

**İlkeyi dağıtma**
1. İlkenizi seçin ve **dağıtmak**için şerit seçeneğine tıklayın.
2. İlkenin dağıtılacağı Kullanıcı veya cihaz koleksiyonunu seçmek için, **Araştır** ' a tıklayın. 
3. Gereken ek seçenekleri seçin. İlke uyumlu olmadığında uyarılar oluşturun. İstemcinin bu ilkeyle cihazın uyumluluğunu değerlendiren zamanlamayı ayarlayın.
4. Dağıtımı oluşturmak için **Tamam** ' ı tıklatın.

Tüm uyumluluk ayarları ilkeleri gibi, istemci belirttiğiniz zamanlamaya göre ayarları düzeltir. Configuration Manager konsolundaki [Cihaz uyumluluğunu izleyin ve rapor](../../compliance/deploy-use/monitor-compliance-settings.md) edin.



## <a name="report-for-default-browser-counts"></a>Varsayılan tarayıcı sayıları için rapor
<!-- 1357830 -->
Artık Windows varsayılan olarak belirli bir Web tarayıcısına sahip istemcilerin sayısını gösteren yeni bir rapor var. 

### <a name="known-issues"></a>Bilinen sorunlar
- Raporu ilk kez açtığınızda, yalnızca Browserprogıd değil sayısını gösterir. Bu sorunu geçici olarak çözmek için, raporun sorgusunu aşağıdaki sözdizimine göre düzenleyin:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Deneyin!  
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.
1. **Configuration Manager** konsolunda, **izleme** çalışma alanında, **Raporlama**' yı genişletin, **raporlar**' ı genişletin, **Yazılım-şirketler ve ürünler**' i seçin.
2. **Varsayılan tarayıcı sayısı** raporunu çalıştırın.

Ortak Browserprogıds için aşağıdaki başvuruyu kullanın:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE. HTTP**: Microsoft Internet Explorer
- **Bermehtml**: Google Chrome
- İşletim **hakkı: Opera**yazılımı
- **Firefoxurl-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Windows 10 ARM64 cihazları için destek
<!-- 1353704 -->
Bu sürümden itibaren Configuration Manager istemcisi Windows 10 ARM64 cihazlarında desteklenir. Mevcut istemci yönetimi özellikleri bu yeni cihazlarla çalışmalıdır. Örneğin, donanım ve yazılım envanteri, yazılım güncelleştirmeleri ve uygulama yönetimi. İşletim sistemi dağıtımı şu anda desteklenmiyor. 

## <a name="changes-to-phased-deployments"></a>Aşamalı dağıtımlarda yapılan değişiklikler
<!-- 1357405 -->
Aşamalı dağıtımlar, birden çok koleksiyonda yazılım Eşgüdümlü, sıralı bir şekilde piyasaya dağıtımını otomatik hale getirir. Bu Technical Preview sürümünde, yönetim konsolundaki görev dizileri için aşamalı dağıtım Sihirbazı tamamlanabilir ve dağıtımlar oluşturulur. Ancak ikinci aşama, ilk aşamanın başarı ölçütlerine göre otomatik olarak başlamaz. İkinci aşama bir SQL ifadesiyle el ile başlatılabilir.   

### <a name="try-it-out"></a>Deneyin!  
  Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.
 
**Görev dizisi için aşamalı dağıtım oluşturma** </br>
1. **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.
2. Var olan bir görev dizisine sağ tıklayın ve **aşamalı dağıtım oluştur**' u seçin. 
3. **Genel** sekmesinde, aşamalı dağıtıma bir ad, açıklama (isteğe bağlı) verin ve **otomatik olarak varsayılan iki aşamalı dağıtım oluştur**' u seçin. 
4. **Ilk koleksiyonu** ve **ikinci koleksiyon** alanlarını doldurun. **İleri**’yi seçin.
5. **Ayarlar** sekmesinde, zamanlama ayarlarının her biri için bir seçenek belirleyin ve tamamlandığında **İleri ' yi** seçin. 
6. **Aşamalar** sekmesinde, gerekirse aşamaların birini düzenleyin ve ardından **İleri**' ye tıklayın.
7. **Özet** sekmesinde seçimlerinizi onaylayın ve devam etmek için **İleri** ' ye tıklayın.
8. İlk aşama için başarı ölçütlerine ulaşıldığında, bir SQL ifadesiyle ikinci aşamayı başlatmak için yönergeleri izleyin.
 
**Bir SQL ifadesiyle ikinci aşamayı Başlat**
1. Aşağıdaki SQL sorgusuyla oluşturduğunuz dağıtım için Phaseddeploymentıd 'yi tanımla:<br/> `Select * from PhasedDeployment`
2. Üretim aşamasını başlatmak için aşağıdaki ifadeyi çalıştırın:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Sonraki adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).    
