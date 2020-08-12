---
title: İşletim sistemi yükseltme görev sırasını oluşturma
titleSuffix: Configuration Manager
description: Windows 7 veya sonraki bir sürümü Windows 10 ' a otomatik olarak yükseltmek için bir görev dizisi kullanma
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 907c36b6f06bbf4fbbabb9ee1b2df6cadb0acb75
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125466"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Configuration Manager işletim sistemini yükseltmek için görev dizisi oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hedef bilgisayarda bir işletim sistemini otomatik olarak yükseltmek için Configuration Manager görev dizilerini kullanın. Bu yükseltme, Windows 7 veya sonraki bir sürümü Windows 10 ' dan veya Windows Server 2012 veya sonraki bir sürümünden Windows Server 2016 ' e olabilir. İşletim sistemi yükseltme paketine ve uygulamalar veya yazılım güncelleştirmeleri gibi yüklenecek diğer içeriklere başvuran bir görev dizisi oluşturun. İşletim sistemini yükseltmek için görev dizisi, [yükseltme pencerelerinin en son sürüm](upgrade-windows-to-the-latest-version.md) senaryosuna bir parçasıdır.  


## <a name="prerequisites"></a>Ön koşullar

Görev dizisini oluşturmadan önce, aşağıdaki gereksinimlerin yerinde olması gerekir:

### <a name="required"></a>Gerekli

- [Işletim sistemi yükseltme paketi](../get-started/manage-operating-system-upgrade-packages.md) Configuration Manager konsolunda kullanılabilir olmalıdır.  

- Windows Server 2016 ' e yükseltirken, Işletim sistemini Yükselt görev dizisi adımında, **çözümlenemeyen uyumluluk Iletilerini yoksay** ayarını seçin. Aksi takdirde yükseltme başarısız olur.  

### <a name="required-if-used"></a>Gerekli (kullanılıyorsa)  

- [Yazılım güncelleştirmelerinin](../../sum/get-started/synchronize-software-updates.md) Configuration Manager konsolunda eşitlenmesi gerekir.  

- [Uygulamalar](../../apps/deploy-use/create-applications.md) Configuration Manager konsoluna eklenmelidir.  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a>İşletim sistemini yükseltmek için görev dizisi oluşturma  

İstemcilerdeki IŞLETIM sistemini yükseltmek için bir görev dizisi oluşturun ve görev sırası oluşturma Sihirbazı ' nda bir **işletim sistemini yükseltme paketinden Yükselt** ' i seçin. Sihirbaz, işletim sistemini yükseltmek, yazılım güncelleştirmelerini uygulamak ve uygulamaları yüklemek için görev dizisi adımlarını ekler.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası oluştur**' u seçin.  

3. Görev sırası oluşturma Sihirbazı ' nın **Yeni görev sırası oluştur** sayfasında, bir **işletim sistemini yükseltme paketinden Yükselt**' i seçin ve ardından **İleri**' yi seçin.  

4. **Görev sırası bilgileri** sayfasında, aşağıdaki ayarları belirtin:  

    - **Görev dizisi adı**: Görev dizisini tanımlayan adı belirtin.  

    - **Açıklama**: isteğe bağlı olarak bir açıklama belirtin.  

5. **Windows Işletim sistemini yükseltme** sayfasında, aşağıdaki ayarları belirtin:  

    - **Paketi Yükselt**: işletim sistemi yükseltme kaynak dosyalarını içeren yükseltme paketini belirtin. **Özellikler** bölmesindeki bilgilere bakarak doğru yükseltme paketini seçtiğinizi doğrulayın. Daha fazla bilgi için bkz. [işletim sistemi yükseltme paketlerini yönetme](../get-started/manage-operating-system-upgrade-packages.md).  

    - **Sürüm dizini**: pakette birden çok işletim sistemi sürümü dizini varsa, istenen sürüm dizinini seçin. Varsayılan olarak, sihirbaz ilk dizini seçer.  

    - **Ürün anahtarı**: işletim sisteminin yüklenmesi için Windows ürün anahtarını belirtin. Kodlanmış toplu lisans anahtarlarını veya standart ürün anahtarlarını belirtin. Standart bir ürün anahtarı kullanırsanız, beş karakter grubunu her bir tire () ile ayırın `-` . Örneğin: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. Yükseltme bir toplu lisans sürümü için olduğunda, ürün anahtarı gerekli olmayabilir.  

        > [!Note]  
        > Bu ürün anahtarı birden çok etkinleştirme anahtarı (MAK) veya bir genel toplu lisanslama anahtarı (GVLK) olabilir. Bir GVLK, anahtar yönetimi hizmeti (KMS) istemci kurulum anahtarı olarak da adlandırılır. Daha fazla bilgi için bkz. [toplu etkinleştirme planı](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). KMS istemci kurulum anahtarlarının bir listesi için, bkz. Windows Server etkinleştirme kılavuzunun [ek a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) .

    - **Çözümlenemeyen uyumluluk Iletilerini yoksayın**: Windows Server 2016 ' e yükseltiyorsanız Bu ayarı seçin. Bu ayarı seçmezseniz, Windows Kurulumu kullanıcının bir Windows uygulama uyumluluğu iletişim kutusunda **Onayla** ' yı seçmesini beklediği için görev sırası tamamlanamamalıdır.  

6. **Güncelleştirmeleri dahil et** sayfasında, gerekli, tümü veya yazılım güncelleştirmelerinin yüklenip yüklenmeyeceğini belirtin. Sonra **İleri**’yi seçin. Yazılım güncelleştirmelerini yüklemeyi belirtirseniz Configuration Manager, yalnızca hedef bilgisayarın üye olduğu koleksiyonlara hedeflenmiş güncelleştirmeleri yükler.  

7. **Uygulamaları yüklemek** sayfasında, hedef bilgisayara yüklenecek uygulamaları belirtin ve ardından **İleri**' yi seçin. Birden fazla uygulama seçerseniz, belirli bir uygulamanın yüklenmesi başarısız olursa görev dizisinin devam edip etmediğini de belirtin.  

8. Sihirbazı tamamlayın.  

> [!Important]  
> Görev dizisi bir cihazda çalıştırıldığında, Configuration Manager istemci, çeşitli senaryolarda görev sırası davranışını denetlemek için birkaç komut dosyası oluşturur. Görev dizisi tamamlandığında, istemci, bilgisayar yeniden başlatılana kadar bu betikleri kaldırmaz. Bu komut dosyaları gizli bilgiler içermez.  

Windows 10 yerinde yükseltme için varsayılan görev sırası şablonu, yükseltme işleminden önce ve sonra eklemek için önerilen eylemleri içeren ek gruplar içerir. Bu eylemler, cihazları Windows 10 ' a başarıyla yükselten birçok müşteri arasında ortaktır. Daha fazla bilgi için bkz. [yükseltmeye hazırlanmak için](#recommended-task-sequence-steps-to-prepare-for-upgrade) önerilen görev dizisi adımları ve [işleme sonrası](#recommended-task-sequence-steps-for-post-processing).

Sürüm 1806 ' den başlayarak, bu görev dizisi şablonu yükseltme işleminin başarısız olması durumunda eklemek için önerilen eylemleri içeren bir grup da içerir. Bu eylemler, sorun gidermeyi kolaylaştırır. Daha fazla bilgi için bkz. [hata üzerinde önerilen görev dizisi adımları](#recommended-task-sequence-steps-on-failure).<!--1358500-->  


## <a name="configure-pre-cache-content"></a>Önbellek içeriğini yapılandırma

<!--1021244-->
Kullanılabilir görev dizileri dağıtımları için ön önbellek özelliği, istemcilerin görev dizisini yüklemeden önce ilgili işletim sistemi yükseltme paketi içeriğini indirmesini sağlar.  

Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](configure-precache-content.md).


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Yükseltmeye hazırlanmak için önerilen görev dizisi adımları

Windows 10 yerinde yükseltme için varsayılan görev sırası şablonu, yükseltme işleminden önce eklemek üzere önerilen eylemleri olan ek grupları içerir. **Yükseltme hazırlığı** grubundaki bu eylemler, cihazları Windows 10 ' a başarıyla yükselten birçok müşteri arasında ortaktır. Zaten bu eylemlere sahip olmayan mevcut bir görev diziniz varsa, bunları **yükseltme Için hazırla** grubuna el ile görev dizize ekleyin.  

### <a name="battery-checks"></a>Pil denetimleri

Bilgisayarın pil veya kablolu güç kullanıp kullanmadığını denetlemek için bu gruba adımlar ekleyin. Bu eylem, bu denetimi gerçekleştirmek için özel bir betik veya yardımcı program gerektirir.

#### <a name="battery-check-example"></a>Pil denetimi örneği

WbemTest kullanın ve `root\cimv2` ad alanına bağlanın. Ardından aşağıdaki sorguyu çalıştırın:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

Herhangi bir sonuç döndürürse cihaz pille çalışır. Aksi halde cihaz kablolu güce bağlanır.  

### <a name="networkwired-connection-checks"></a>Ağ/kablolu bağlantı denetimleri

Bilgisayarın bir ağa bağlı olup olmadığını denetlemek için bu gruba adımlar ekleyin ve kablosuz bağlantı kullanıp kullanmadığını denetleyin. Bu eylem, bu denetimi gerçekleştirmek için özel bir betik veya yardımcı program gerektirir.

#### <a name="network-check-example"></a>Ağ denetimi örneği

WbemTest kullanın ve `root\cimv2` ad alanına bağlanın. Ardından aşağıdaki sorguyu çalıştırın:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

Herhangi bir sonuç döndürürse cihaz Wi-Fi üzerinde çalışır. Aksi takdirde, cihaz kablolu ağ bağlantısına bağlanır.

### <a name="remove-incompatible-applications"></a>Uyumsuz uygulamaları kaldırma

Windows 10 ' un bu sürümüyle uyumlu olmayan uygulamaları kaldırmak için bu gruba adımlar ekleyin. Bir uygulamayı kaldırma yöntemi farklılık gösterir.  

Uygulama Windows Installer kullanıyorsa, uygulamanın Windows Installer dağıtım türü özelliklerindeki **Programlar** sekmesinden **Program kaldır** komut satırını kopyalayın. Ardından, program Kaldır komut satırı ile bu gruba bir **komut satırı Çalıştır** adımı ekleyin. Örnek:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>Uyumsuz sürücüleri kaldır

Windows 10 ' un bu sürümü ile uyumlu olmayan sürücüleri kaldırmak için bu gruba adımlar ekleyin.  

### <a name="removesuspend-third-party-security"></a>Üçüncü taraf güvenliği kaldırma/askıya alma

Virüsten koruma gibi üçüncü taraf güvenlik programlarını kaldırmak veya askıya almak için bu gruba adımlar ekleyin.  

Üçüncü taraf bir disk şifreleme programı kullanıyorsanız, `/ReflectDrivers` [komut satırı seçeneğiyle](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers)Windows kurulumu için şifreleme sürücüsünü belirtin. Bu gruptaki görev dizisine bir [görev dizisi değişkeni ayarlama](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) adımı ekleyin. Görev sırası değişkenini **Osdsetupadditionalupgradeoptions**olarak ayarlayın. Değerini, `/ReflectDrivers` sürücü yoluyla olarak ayarlayın. Bu [görev dizisi değişkeni](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) , görev sırası tarafından kullanılan Windows kurulumu komut satırını ekler. Bu işlemle ilgili ek yönergeler için yazılım satıcınıza başvurun.  

### <a name="download-package-content-task-sequence-step"></a>Paket Içeriğini indir görev dizisi adımı  

Aşağıdaki senaryolarda **Işletim sistemini yükseltme** adımından önce [paket içeriğini indir](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) adımını kullanın:  

- Hem x86 hem de x64 platformları için tek bir yükseltme görev dizisi kullanırsınız. **Yükseltme Için hazırlama** grubuna Iki **paket içeriğini indirme** adımı ekleyin. İstemci mimarisini algılamak için her adımın koşullarını belirleyin. Bu durum, adımın yalnızca uygun işletim sistemi yükseltme paketini indirmesine neden olur. Her bir **Paket İçeriğini İndirme** adımını aynı değişkeni kullanacak şekilde yapılandırın ve değişkeni **İşletim Sistemini Yükseltme** adımındaki medya yolu için kullanın.  

- Uygun bir sürücü paketini dinamik olarak indirmek için, her bir sürücü paketine uygun donanım türünü algılamaya yönelik koşulları içeren iki adet **Paket İçeriğini İndirme** adımı kullanın. Her bir **paket Içeriğini indirme** adımını aynı değişkeni kullanacak şekilde yapılandırın. Ardından, **Işletim sistemini yükseltme** adımının sürücüler bölümündeki **hazırlanmış içerik** değeri için bu değişkeni kullanın.  

    > [!NOTE]  
    > Configuration Manager Bu değişken adına sayısal bir sonek ekler. Örneğin, `%mycontent%` özel bir değişken olarak belirtirseniz, istemci başvurulan tüm içeriği bu konumda depolar. **Işletim sistemini yükseltme**gibi sonraki bir adımda değişkenine başvurduğunuzda, değişkeni sayısal bir sonek ile kullanın. Bu örnekte, `%mycontent01%` veya `%mycontent02%` numarası, **paket içeriğini indir** adımının bu belirli içeriği listeleyen sıraya karşılık gelir.  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>İşlem sonrası için önerilen görev sırası adımları

Görev dizisini oluşturduktan sonra, görev dizisinin **Işlem sonrası** grubuna ek adımlar ekleyin.  

> [!NOTE]  
> Bu görev sırası doğrusal değil. Adımlarda görev dizisinin sonuçlarını etkileyebilecek koşullar vardır. Bu davranış, istemci bilgisayarı başarıyla yükseltmelerine veya istemci bilgisayarı özgün işletim sistemine geri alma işlemi yapılıp yapılmayacağını bağlıdır.  

Windows 10 yerinde yükseltme için varsayılan görev sırası şablonu, yükseltme işleminden sonra eklemek için önerilen eylemleri olan ek grupları içerir. **Son işlem** grubundaki bu eylemler, cihazları Windows 10 ' a başarıyla yükselten birçok müşteri arasında ortaktır. Bu eylemlere zaten sahip olmayan mevcut bir görev diziniz varsa, bunları el ile, **Işlem sonrası** grubundaki görev dizize ekleyin.  

### <a name="apply-setup-based-drivers"></a>Kurulum tabanlı sürücüleri uygulama

Paketten kurulum tabanlı sürücüler (. exe) yüklemek için bu gruba adımlar ekleyin.  

### <a name="installenable-third-party-security"></a>Üçüncü taraf güvenliğini yükler/etkinleştir

Virüsten koruma gibi üçüncü taraf güvenlik programlarını yüklemek veya etkinleştirmek için bu gruba adımlar ekleyin.  

### <a name="set-windows-default-apps-and-associations"></a>Windows varsayılan uygulamalarını ve ilişkilendirmelerini ayarla

Windows varsayılan uygulamalarını ve dosya ilişkilendirmelerini ayarlamak için bu gruba adımlar ekleyin.

1. İstenen uygulama ilişkilendirmelerinizi içeren bir başvuru bilgisayarı hazırlayın.
1. Dışarı aktarmak için aşağıdaki komut satırını çalıştırın:  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. XML dosyasını bir pakete ekleyin.
1. Bu grupta bir [komut satırı Çalıştır](../understand/task-sequence-steps.md#BKMK_RunCommandLine) adımı ekleyin. XML dosyasını içeren paketi belirtin ve ardından aşağıdaki komut satırını belirtin:  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

Daha fazla bilgi için bkz. [Varsayılan uygulama Ilişkilendirmelerini dışarı veya içeri](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)aktarma.

### <a name="apply-customizations-and-personalization"></a>Özelleştirmeleri ve kişiselleştirmeyi uygulama

Program gruplarını düzenleme gibi Başlat menüsü özelleştirmeleri uygulamak için bu gruba adımlar ekleyin. Daha fazla bilgi için bkz. [Başlangıç ekranını özelleştirme](/windows-hardware/manufacture/desktop/customize-the-start-screen).  


## <a name="optional-task-sequence-steps-for-rollback"></a>Geri alma için isteğe bağlı görev dizisi adımları  

Bilgisayar yeniden başlatıldıktan sonra yükseltme işleminde bir sorun olduğunda, Windows Kurulumu sistemi önceki IŞLETIM sistemine geri kaydeder. Görev sırası daha sonra **geri alma** grubundaki adımlarla devam eder. Görev dizisini oluşturduktan sonra, bu gruba gerektiği şekilde isteğe bağlı adımlar ekleyin. Örneğin, yükseltme hazırlığı grubundaki sistemde yapılan tüm değişiklikleri, uyumsuz yazılımları kaldırma gibi tersine çevirin.


## <a name="recommended-task-sequence-steps-on-failure"></a>Hata durumunda önerilen görev dizisi adımları

<!--1358500-->
Sürüm 1806 ' den başlayarak, Windows 10 yerinde yükseltme için varsayılan görev sırası şablonu, **hata durumunda eylemler çalıştırmak**için bir grup içerir. Bu grup, yükseltme işleminin başarısız olması durumunda eklemek için önerilen eylemleri içerir. Bu eylemler, sorun gidermeyi kolaylaştırır.

### <a name="collect-logs"></a>Günlük toplama

İstemciden günlükleri toplamak için bu gruba adımlar ekleyin.  

- Ortak bir uygulama, günlük dosyalarını bir ağ paylaşımında kopyalamadır. Bu bağlantıyı kurmak için, [ağ klasörüne Bağlan](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) adımını kullanın.  

- Kopyalama işlemini gerçekleştirmek için [komut satırı Çalıştır](../understand/task-sequence-steps.md#BKMK_RunCommandLine) veya [PowerShell Betiği Çalıştır](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) adımla özel bir betik veya yardımcı program kullanın.  

- Toplanacak dosyalar aşağıdaki günlükleri içerebilir:  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- Setupact. log ve diğer Windows Kurulumu günlükleri hakkında daha fazla bilgi için bkz. [Windows Kurulumu günlük dosyaları](https://docs.microsoft.com/windows/deployment/upgrade/log-files).  

- Configuration Manager istemci günlükleri hakkında daha fazla bilgi için bkz. [Configuration Manager istemci günlükleri](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs).  

- **_SMSTSLogPath** ve diğer yararlı değişkenler hakkında daha fazla bilgi için bkz. [görev dizisi değişkenleri](../understand/task-sequence-variables.md).  

### <a name="run-diagnostic-tools"></a>Tanılama araçlarını Çalıştır

Ek tanılama araçları çalıştırmak için bu gruba adımlar ekleyin. Hatadan sonra sistemden daha fazla bilgi toplamak için bu araçları otomatikleştirin.  

Bu tür bir araç Windows [Setupdiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag)'dir. Bir Windows 10 yükseltmesinin neden başarısız olduğuna ilişkin ayrıntıları almak için tek başına bir tanılama aracıdır.  

- Configuration Manager, araç için [bir paket oluşturun](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) .  

- Görev sıralarınızın bu grubuna [komut satırı Çalıştır](../understand/task-sequence-steps.md#BKMK_RunCommandLine) adımı ekleyin. Araca başvurmak için **paket** seçeneğini kullanın. Aşağıdaki dize örnek bir **komut satırı**örneğidir:  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`  

> [!TIP]
> En son işlevsellik ve bilinen sorunlara yönelik düzeltmeler için her zaman SetupDiag 'un en son sürümünü kullanın. Daha fazla bilgi için bkz. [Setupdiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag).

## <a name="additional-recommendations"></a>Ek öneriler

### <a name="windows-documentation"></a>Windows belgeleri

Windows [10 yükseltme hatalarını çözmek](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)için Windows belgelerini gözden geçirin. Bu makale, yükseltme işlemiyle ilgili ayrıntılı bilgileri de içerir.  

### <a name="check-minimum-disk-space"></a>En az disk alanını denetle

**Hazır olma durumunu denetle** adımında **minimum boş DISK alanı (MB) sağlayın**. Değeri 32 bit işletim sistemi yükseltme paketi için en az **16384** (16 GB) veya 64-bit için **20480** (20 GB) olarak ayarlayın.  

### <a name="retry-downloading-policy"></a>İlkeyi indirmeyi yeniden dene

İlkeyi indirmeyi yeniden denemek için **SMSTSDownloadRetryCount** [görev dizisi değişkenini](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) kullanın. Şu anda varsayılan olarak istemci iki kez yeniden denenir; Bu değişken iki (2) olarak ayarlanır. İstemcileriniz kablolu intranet ağ bağlantısı üzerinde değilse, istemcinin ilkeyi almasına yardımcı olur. Bu değişkenin kullanılması, olumsuz bir yan etkiye neden olmaz, bu, ilke indiremez gecikmeli bir hata değildir.<!--501016--> Ayrıca, varsayılan 15 saniyeden **SMSTSDownloadRetryDelay** değişkenini de artırın.  

### <a name="perform-an-inline-compatibility-assessment"></a>Satır içi uyumluluk değerlendirmesi gerçekleştirme

1. **Yükseltme Için hazırlama** grubunun başlarında Ikinci bir **yükseltme işletim sistemi** adımı ekleyin.  

    1. *Yükseltme değerlendirmesini*adlandırın.
    1. Aynı yükseltme paketini belirtin ve ardından **yükseltmeyi başlatmadan Windows Kurulumu uyumluluk taraması gerçekleştirme**seçeneğini etkinleştirin.
    1. Seçenekler sekmesinde **hata durumunda devam et '** i etkinleştirin.  

1. Bu *yükseltme değerlendirmesi* adımını hemen takip eden bir **komut satırını Çalıştır** adımı ekleyin. Aşağıdaki komut satırını belirtin:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

    Bu komut, komut isteminin belirtilen sıfır olmayan çıkış koduyla çıkmasına neden olur ve bu da görev dizisinin bir hata olduğunu varsayar.

1. **Seçenekler** sekmesinde, aşağıdaki koşulu ekleyin:

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

    Bu durum, görev dizisinin yalnızca bir başarı kodu olmaması durumunda bu **komut satırını Çalıştır** adımını çalıştırdığı anlamına gelir.

Dönüş kodu, `3247440400` hiçbir sorun olmadan başarılı bir uyumluluk taraması olan MOSETUP_E_COMPAT_SCANONLY (0xC1900210) değerinin ondalık eşdeğeridir. *Yükseltme değerlendirmesi* adımı başarılı olur ve dönerse `3247440400` , görev sırası bu **komut satırını Çalıştır** adımını atlar ve devam eder. Değerlendirme adımı başka bir dönüş kodu döndürürse, bu **komut satırı Çalıştır** adımı çalışır. Komut sıfır olmayan bir dönüş koduyla çıkış yaptığından, görev sırası da başarısız olur. Görev sırası günlüğü ve durum iletileri Windows Kurulumu uyumluluk taramasının dönüş kodunu içerir. **_SMSTSOSUpgradeActionReturnCode**hakkında daha fazla bilgi için bkz. [görev dizisi değişkenleri](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode).

Daha fazla bilgi için [işletim sistemini yükseltme](../understand/task-sequence-steps.md#BKMK_UpgradeOS) görev dizisi adımına bakın.

### <a name="convert-from-bios-to-uefi"></a>BIOS 'tan UEFı 'ye Dönüştür

Bu görev sırası sırasında cihazı BIOS 'tan UEFı 'ye değiştirmek istiyorsanız, [yerinde yükseltme SıRASıNDA BIOS 'TAN UEFI 'ye dönüştürme](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)bölümüne bakın.  

### <a name="manage-bitlocker"></a>seçin,

<!--SCCMDocs issue #494-->
BitLocker disk şifrelemesi kullanıyorsanız, varsayılan olarak Windows Kurulumu yükseltme sırasında otomatik olarak askıya alır. Windows 10 sürüm 1803 ' den başlayarak, Windows Kurulumu `/BitLocker` Bu davranışı denetlemek için komut satırı parametresini içerir. Güvenlik gereksinimleriniz, etkin disk şifrelemesini her zaman gerektirdiğinde, **yükseltme Için hazırla** grubunda **Osdsetupadditionalupgradeoptions** [görev dizisi değişkenini](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) kullanın `/BitLocker TryKeepActive` . Daha fazla bilgi için bkz. [Windows kurulumu komut satırı seçenekleri](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### <a name="remove-default-apps"></a>Varsayılan uygulamaları Kaldır

<!--SCCMDocs issue #526-->
Bazı müşteriler Windows 10 ' da varsayılan sağlanan uygulamaları kaldırır. Örneğin, Bing hava durumu uygulaması veya Microsoft Solitaire koleksiyonu. Bazı durumlarda, bu uygulamalar Windows 10 ' u güncelleştirdikten sonra döndürülür. Daha fazla bilgi için bkz. [Windows 10 ' dan kaldırılan uygulamaları tutma](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update).

**Yükseltme Için hazırla** grubundaki görev dizisine **komut satırı Çalıştır** adımı ekleyin. Aşağıdaki örneğe benzer bir komut satırı belirtin:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
