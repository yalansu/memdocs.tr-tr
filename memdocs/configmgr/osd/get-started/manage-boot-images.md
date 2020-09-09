---
title: Önyükleme görüntülerini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager, bir işletim sistemi dağıtımı sırasında kullandığınız Windows PE önyükleme görüntülerini yönetmeyi öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ddcf0c9ff4a9af1e74a745d8bda326804365206
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606314"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Configuration Manager ile önyükleme görüntülerini yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager bir önyükleme görüntüsü, işletim sistemi dağıtımı sırasında kullanılan bir [WINDOWS PE](/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) görüntüsüdür. Önyükleme görüntüleri, WinPE 'de bir bilgisayarı başlatmak için kullanılır. Bu en düşük işletim sistemi sınırlı bileşen ve hizmet içerir. Configuration Manager, WinPE 'yi kullanarak hedef bilgisayarı Windows yüklemesine hazırlar.

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a> Varsayılan önyükleme görüntüleri

Configuration Manager iki varsayılan önyükleme görüntüsü sağlar: biri x86 platformlarını ve diğeri de x64 platformlarını destekler. Bu görüntüler, site sunucusunda aşağıdaki paylaşımdaki *x64* veya *I386* klasörlerinde depolanır: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\` . Varsayılan önyükleme görüntüleri, aldığınız eyleme göre güncelleştirilir veya yeniden oluşturulur.

Varsayılan önyükleme görüntüleri için açıklanan eylemlerden herhangi biri için aşağıdaki davranışları göz önünde bulundurun:

- Kaynak sürücü nesneleri geçerli olmalıdır. Bu nesneler sürücü kaynak dosyalarını içerir. Nesneler geçerli değilse, site sürücüleri önyükleme görüntülerine eklemez.  

- Aynı Windows PE sürümünü kullansalar bile, varsayılan önyükleme görüntülerini temel almayan önyükleme yansımaları değiştirilmez.  

- Değiştirilen önyükleme görüntülerini dağıtım noktalarına yeniden dağıtın.  

- Değiştirilen önyükleme görüntülerini kullanan medyayı yeniden oluşturun.  

- Özelleştirilmiş/varsayılan önyükleme görüntülerinizin otomatik olarak güncelleştirilmesini istemiyorsanız, bunları varsayılan konumda saklamayın.  

> [!NOTE]
> Configuration Manager günlük Aracı (**CMTrace**), **yazılım kitaplığındaki**tüm önyükleme görüntülerine eklenir. Windows PE 'de çalışırken komut isteminden yazarak aracı başlatın `cmtrace` .
>
> CMTrace, Windows PE 'de günlük dosyaları için varsayılan görüntüleyiciye sahiptir.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Configuration Manager en son sürümünü yüklemek için güncelleştirmeler ve bakım kullanın

Windows değerlendirme ve Dağıtım Seti (ADK) sürümünü yükselttiğinizde ve sonra Configuration Manager en son sürümünü yüklemek için güncelleştirmeler ve bakım kullandığınızda, site varsayılan önyükleme görüntülerini yeniden oluşturur. Bu güncelleştirme, güncelleştirilmiş Windows ADK 'den yeni WinPE sürümünü, Configuration Manager istemcisinin yeni sürümünü, sürücülerini ve özelleştirmeleri içerir. Site özel önyükleme görüntülerini değiştirmez.

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Configuration Manager 2012 ' den güncel dala yükseltme

2012 Configuration Manager geçerli dala yükselttiğinizde, site varsayılan önyükleme görüntülerini yeniden oluşturur. Bu güncelleştirme, güncelleştirilmiş Windows ADK 'den yeni WinPE sürümünü ve Configuration Manager istemcisinin yeni sürümünü içerir. Tüm önyükleme görüntüsü özelleştirmeleri değişmeden kalır. Site özel önyükleme görüntülerini değiştirmez.

### <a name="update-distribution-points-with-the-boot-image"></a>Dağıtım noktalarını Önyükleme görüntüsüyle güncelleştirme

Konsolundaki **önyükleme görüntüleri** düğümünden **dağıtım noktalarını güncelleştir** eylemini kullandığınızda, site hedef önyükleme görüntüsünü istemci bileşenleriyle, sürücülerle ve özelleştirmeleriyle güncelleştirir.

Windows ADK yükleme dizininden önyükleme görüntüsünü en son WinPE sürümüyle yeniden yükleyebilirsiniz. Dağıtım noktalarını Güncelleştirme Sihirbazı 'nın **genel** sayfası aşağıdaki bilgileri sağlar:

- Site sunucusunda yüklü olan geçerli Windows ADK sürümü
- Geçerli üretim istemcisi sürümü
- Önyükleme görüntüsündeki WinPE 'nin Windows ADK sürümü
- Önyükleme görüntüsündeki Configuration Manager istemcisinin sürümü

Önyükleme görüntüsündeki sürümler güncel değilse, **Bu önyükleme görüntüsünü WINDOWS ADK 'den geçerli WINDOWS PE sürümü Ile yeniden yükleme**seçeneğini kullanın.

> [!Important]  
> Bu eylem hem varsayılan hem de özel önyükleme görüntüleri için kullanılabilir. Bu işlem sırasında önyükleme görüntüsünü yeniden yükleme sırasında, site Configuration Manager dışında yapılan el ile özelleştirmeleri korumaz. Bu özelleştirmeler üçüncü taraf uzantılarını içerir. Bu seçenek, en son WinPE sürümünü ve en son istemci sürümünü kullanarak önyükleme görüntüsünü yeniden oluşturur. Yalnızca önyükleme görüntüsünün özelliklerinde belirttiğiniz konfigürasyonlar yeniden uygulanır. <!--SCCMDocs issue #1283-->

**Önyükleme görüntüleri** düğümü (**istemci sürümü**) için de yeni bir sütun içerir. Her Önyükleme görüntüsündeki Configuration Manager istemci sürümünü hızlıca görüntülemek için bu sütunu kullanın.

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a> Önyükleme görüntüsünü özelleştirme  

Bir önyükleme görüntüsü Windows ADK 'nin desteklenen sürümünden WinPE sürümünü temel alırken, konsoldan [bir önyükleme görüntüsünü](#BKMK_ModifyBootImages) özelleştirebilir veya değiştirebilirsiniz. Bir siteyi yükselttiğinizde ve Windows ADK 'nin yeni bir sürümünü yüklediğinizde, Özel önyükleme görüntüleri Windows ADK 'nin yeni sürümüyle güncellenmez. Bu durumda, Configuration Manager konsolundaki önyükleme görüntülerini özelleştiremezsiniz. Ancak, yükseltmeden önceki gibi çalışmaya devam ederler.  

Bir önyükleme görüntüsü, bir sitede yüklü olan farklı bir Windows ADK sürümünü temel alarak önyükleme görüntülerini özelleştirmeniz gerekir. Dağıtım Görüntüsü Bakımı ve yönetimi (DıSM) komut satırı aracını kullanma gibi bu önyükleme görüntülerini özelleştirmek için başka bir yöntem kullanın. DıSM, Windows ADK 'nin bir parçasıdır. Daha fazla bilgi için bkz. [önyükleme görüntülerini özelleştirme](customize-boot-images.md).  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a> Önyükleme görüntüsü ekleme  

Site yüklemesi sırasında Configuration Manager, bir WinPE sürümünü temel alan önyükleme görüntülerini Windows ADK 'nin desteklenen sürümünden otomatik olarak ekler. Configuration Manager sürümüne bağlı olarak, farklı bir WinPE sürümünü temel alan önyükleme görüntülerini Windows ADK 'nin desteklenen sürümünden ekleyebilirsiniz. Desteklenmeyen bir WinPE sürümünü içeren bir önyükleme görüntüsü eklemeye çalıştığınızda bir hata oluşur. Aşağıdaki liste, şu anda desteklenen Windows ADK ve WinPE sürümleridir:

- Windows ADK sürümü: Windows 10 için Windows ADK

- Configuration Manager konsolundan özelleştirilebilen önyükleme görüntüleri için Windows PE sürümleri: Windows PE 10

- Configuration Manager konsolundan *özelleştirilemeyen* önyükleme görüntüleri Için desteklenen Windows PE sürümleri

  - Windows PE 3,1<sup>[Note 1](#bkmk_note1)</sup>

  - Windows PE 5

Örneğin, Windows 10 için Windows ADK 'den Windows PE 10 tabanlı önyükleme görüntülerini özelleştirmek için Configuration Manager konsolunu kullanın. Windows PE 5 tabanlı bir önyükleme görüntüsü için, Windows 8 için Windows ADK 'den DıSM sürümünü kullanarak farklı bir bilgisayardan özelleştirin. Ardından, Özel önyükleme görüntüsünü Configuration Manager konsoluna ekleyin. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Önyükleme görüntülerini özelleştirme](customize-boot-images.md)
- [Windows 10 ADK desteği](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [DıSM desteklenen platformlar](/windows-hardware/manufacture/desktop/dism-supported-platforms)

<a name="bkmk_note1"></a>

> [!NOTE]
> **Note 1: Windows PE 3,1 için destek**
>
> Yalnızca Windows PE *3,1 sürümüne*göre Configuration Manager bir önyükleme görüntüsü ekleyin. Windows 7 için Windows AIK 'yi (Windows PE 3,0 tabanlı) Windows 7 SP1 için Windows AIK eki (Windows PE 3,1 tabanlı) ile yükseltin. Windows 7 SP1 için Windows AIK eki 'ni [Microsoft Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=5188)' nden indirin.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **önyükleme görüntüleri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **önyükleme görüntüsü Ekle**' yi seçin. Bu eylem önyükleme görüntüsü ekleme Sihirbazı 'Nı başlatır.  

3. **Veri kaynağı** sayfasında, aşağıdaki seçenekleri belirtin:  

    - **Yol** kutusunda, önyükleme görüntüsü WIM dosyasının yolunu belirtin. Belirtilen yol UNC biçiminde geçerli bir ağ yolu olmalıdır. Örnek: `\\ServerName\ShareName\BootImageName.wim`

    - **Önyükleme Görüntüsü** açılan listesinden önyükleme görüntüsünü seçin. WıM dosyası birden çok önyükleme görüntüsü içeriyorsa uygun görüntüyü seçin.  

4. **Genel** sayfasında, aşağıdaki seçenekleri belirtin:  

    - **Ad** kutusunda önyükleme görüntüsü için benzersiz adı belirtin.  

    - **Sürüm** kutusunda önyükleme görüntüsü için sürüm numarasını belirtin.  

    - **Açıklama** kutusunda, önyükleme görüntüsünü nasıl kullanacağınızı gösteren kısa bir açıklama belirtin.  

5. Sihirbazı tamamlayın.  

Önyükleme görüntüsü artık **önyükleme görüntüsü** düğümünde listelenir. Bir işletim sistemini dağıtmak için önyükleme görüntüsünü kullanmadan önce, önyükleme görüntüsünü dağıtım noktalarına dağıtın.

> [!Tip]  
> Konsolunun **önyükleme görüntüsü** düğümünde **Boyut (KB)** sütunu her önyükleme görüntüsünün açılmış boyutunu görüntüler. Site, ağ üzerinden bir önyükleme görüntüsü gönderdiğinde, sıkıştırılmış bir kopya gönderir. Bu kopya genellikle **Boyut (KB)** sütununda listelenen boyuttan daha küçüktür.  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a> Önyükleme görüntülerini dağıtma  

Önyükleme görüntüleri dağıtım noktalarına, diğer içerikleri dağıttığınız şekilde dağıtılır. Bir işletim sistemini dağıtmadan veya medya oluşturmadan önce, önyükleme görüntüsünü en az bir dağıtım noktasına dağıtın.

Önyükleme görüntüsünü dağıtma hakkında daha fazla bilgi için bkz. [Içerik dağıtma](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

İşletim sistemini dağıtmak üzere PXE kullanmak için önyükleme görüntüsünü dağıtmadan önce aşağıdaki noktaları göz önünde bulundurun:  

- Dağıtım noktasını PXE isteklerini kabul edecek şekilde yapılandırın.  
- Hem x86 hem de x64 PXE özellikli bir önyükleme görüntüsünü en az bir PXE 'yi destekleyen dağıtım noktasına dağıtın.  
- Configuration Manager, önyükleme görüntülerini PXE 'yi destekleyen dağıtım noktasındaki **RemoteInstall** klasörüne dağıtır.  
  
İşletim sistemlerini dağıtmak için PXE kullanma hakkında daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a> Önyükleme görüntüsünü değiştirme  

Görüntüye aygıt sürücüleri ekleyin veya kaldırın ya da önyükleme görüntüsünün özelliklerini düzenleyin. Eklediğiniz veya kaldırdığınız Sürücüler ağ veya depolama sürücülerini içerebilir. Önyükleme görüntülerini değiştirirken aşağıdakileri göz önünde bulundurun:  

- Önyükleme görüntüsüne sürücü eklemeden önce, cihazı cihaz sürücüsü kataloğunda içeri aktarıp etkinleştirin.  

- Bir önyükleme görüntüsünü değiştirdiğinizde önyükleme görüntüsü, önyükleme görüntüsünün başvurduğu ilişkili paketlerden hiçbirini değiştirmez.  

- Bir önyükleme görüntüsünde değişiklikler yaptıktan sonra, önyükleme görüntüsünü zaten sahip olduğu dağıtım noktalarında **güncelleştirin** . Bu işlem, önyükleme görüntüsünün en güncel sürümünü istemciler için kullanılabilir hale getirir. Daha fazla bilgi için bkz. [dağıttığınız Içeriği yönetme](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="modify-the-properties-of-a-boot-image"></a>Önyükleme görüntüsünün özelliklerini değiştirme  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **önyükleme görüntüleri** düğümünü seçin.  

2. Düzenlemek istediğiniz önyükleme görüntüsünü seçin.  

3. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

4. Önyükleme görüntüsünün davranışını değiştirmek için aşağıdaki ayarlardan birini düzenleyin:  

#### <a name="images"></a>Görüntüler

**Görüntüler** sekmesinde, önyükleme görüntüsünün özelliklerini bir dış araç kullanarak değiştirirseniz, **yeniden yükle**' yi seçin.  

#### <a name="drivers"></a>Sürücüler

**Sürücüler** sekmesinde, WinPE 'nin önyüklemesi Için gereken Windows cihaz sürücülerini ekleyin. Cihaz sürücülerini eklerken aşağıdaki noktaları göz önünde bulundurun:  

- Önyükleme görüntüsüne eklediğiniz sürücülerin önyükleme görüntüsünün mimarisiyle eşleştiğinden emin olun.  

- Yalnızca önyükleme görüntüsünün mimarisine yönelik sürücüleri göstermek için **önyükleme görüntüsünün mimarisiyle eşleşmeyen sürücüleri gizle**' yi seçin. Sürücünün mimarisi, üreticiden gelen INF dosyasında bildirilen mimariye dayanır.  

- WinPE zaten yerleşik birçok sürücü ile birlikte gelir. Yalnızca WinPE 'ye dahil olmayan ağ ve depolama sürücülerini ekleyin.  

- WinPE 'deki diğer sürücüler için gereksinimler olmadıkça, önyükleme görüntüsüne yalnızca ağ ve depolama sürücülerini ekleyin.  

- Yalnızca depolama ve ağ sürücülerini göstermek için **depolama veya ağ sınıfında olmayan sürücüleri gizle (önyükleme görüntüleri için)** öğesini seçin. Bu seçenek, genellikle video veya modem sürücüleri gibi önyükleme görüntüleri için gerekli olmayan diğer sürücüleri de gizler.  

- Geçerli dijital imzaya sahip olmayan sürücüleri gizlemek için **dijital olarak imzalanmamış sürücüleri gizle**' yi seçin.  

> [!NOTE]  
> Cihaz sürücülerini önyükleme görüntüsüne eklemeden önce sürücü kataloğuna aktarın. Cihaz sürücülerini içeri aktarma hakkında daha fazla bilgi için bkz. [sürücüleri yönetme](manage-drivers.md).  

#### <a name="customization"></a>Özelleştirme

**Özelleştirme** sekmesinde, aşağıdaki ayarlardan birini seçin:  

- Görev dizisi çalıştırılmadan önce çalıştırılacak komutu belirtmek için **başlatma öncesi komutlarını etkinleştir** seçeneğini belirleyin. Bu seçeneği etkinleştirdiğinizde, çalıştırılacak komut satırını ve komut için gereken destek dosyalarını da belirtin.  

    > [!WARNING]  
    > `cmd /c`Komut satırının başlangıcına ekleyin. Belirtmezseniz `cmd /c` , komut çalıştıktan sonra kapanmaz. Dağıtım, komutun bitmesini beklemeye devam eder ve yapılandırılmış diğer komut veya eylemleri başlatmayacaktır.  

    > [!TIP]  
    > Görev sırası medya oluşturma sırasında, sihirbaz paket KIMLIĞINI ve başlatma öncesi komut satırını **CreateTsMedia. log** dosyasına yazar. Bu bilgiler, herhangi bir görev dizisi değişkeni için değer içerir. Bu günlük Configuration Manager konsolunu çalıştıran bilgisayarda bulunur. Görev dizisi değişkenlerinin değerlerini doğrulamak için bu günlük dosyasını gözden geçirin.  

- Varsayılan WinPE arka planını mı yoksa özel arka planı mı kullanmak istediğinizi belirtmek için **Windows PE Arka Planı** ayarlarını yapın.  

- WinPE tarafından kullanılan geçici depolama (RAM sürücüsü) olan **WINDOWS PE karalama alanını (MB)** yapılandırın. Örneğin, bir uygulama WinPE içinden çalıştırıldığında ve geçici dosyalar yazması gerektiğinde, WinPE sabit disk varmış gibi onu taklit ederek o dosyaları bellekteki boş alana yönlendirir. Varsayılan olarak, bu miktar 1 GB 'den fazla RAM 'e sahip cihazlarda 512 MB 'tır, aksi takdirde varsayılan değer 32 MB 'tır.  

- Önyükleme görüntüsü dağıtılırken **F8** tuşunu kullanarak bir komut istemi açmak için **Komut desteğini etkinleştir (yalnızca test)** öğesini seçin. Bu seçenek, dağıtımınızı test ederken sorun gidermeye yarar. Bu ayarın bir üretim dağıtımında kullanılması, güvenlik sorunları nedeniyle önerilmez.  

- **WinPE 'de varsayılan klavye düzeni ayarla**: <!--4910348-->Sürüm 1910 ' den başlayarak, önyükleme görüntüsü için varsayılan klavye yerleşimini yapılandırın. En-US dışında bir dil seçerseniz Configuration Manager, kullanılabilir giriş yerel ayarları 'nda hala en-US ' i içerir. Cihazda, ilk klavye düzeni seçili yerel ayar olur, ancak gerekirse Kullanıcı cihazı en-US ' a değiştirebilir.

> [!Tip]
> Bu ayarları bir betikten yapılandırmak için [set-Cmbootımage](/powershell/module/configurationmanager/set-cmbootimage) PowerShell cmdlet 'ini kullanın.

#### <a name="optional-components"></a>İsteğe bağlı bileşenler

**Isteğe bağlı bileşenler** sekmesinde, Configuration Manager ile kullanılmak üzere Windows PE 'ye eklenen bileşenleri belirtin. Kullanılabilir isteğe bağlı bileşenler hakkında daha fazla bilgi için bkz. [WinPE: Paket ekleme (İsteğe Bağlı Bileşenler Başvurusu)](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Aşağıdaki bileşenler Configuration Manager için gereklidir ve her zaman önyükleme görüntülerine eklenir:

- Betik oluşturma (WinPE-Scripting)
- Başlangıç (WinPE-SecureStartup)
- Ağ (WinPE-WDS-Tools)
- Betik oluşturma (WinPE-WMI)

**Bileşenler** listesi, bu önyükleme görüntüsüne eklenen ek öğeleri gösterir. Daha fazla bileşen eklemek için altın yıldız işaretini seçin. Bir bileşeni kaldırmak için listeden seçin ve ardından kırmızı X ' i seçin.

Müşteriler tarafından yaygın olarak kullanılan bileşenler şunlardır:

- Microsoft .NET (WinPE-NetFX): Bu bileşen PowerShell için bir önkoşuldur. Bu, daha büyük isteğe bağlı bileşenlerden biridir.  
- Windows PowerShell (WinPE-PowerShell): Bu bileşen .NET gerektirir ve sınırlı PowerShell desteği ekler. Görev dizinizin WinPE aşamasında özel PowerShell betikleri çalıştırırsanız, bu bileşeni ekleyin. Diğer PowerShell cmdlet 'leri için gerekli olabilecek başka bileşenler de vardır.
- HTML (WinPE-HTA): görev dizinizin WinPE aşamasında özel HTML uygulamaları çalıştırırsanız, bu bileşeni ekleyin.

Dil ekleme hakkında daha fazla bilgi için bkz. [birden çok dil yapılandırma](#BKMK_BootImageLanguage).

#### <a name="data-source"></a>Veri Kaynağı

**Veri Kaynağı** sekmesinde, aşağıdaki ayarlardan birini güncelleştirin:  

- Önyükleme görüntüsünün kaynak dosyasını değiştirmek için, **görüntü yolu** ve **görüntü dizini**' ni ayarlayın.  

- Sitenin önyükleme görüntüsünü ne zaman güncelleştirdiği hakkında bir zamanlama oluşturmak için bir **zamanlamaya göre dağıtım noktalarını güncelleştir**' i seçin.  

- Bu paketin içeriğinin diğer içeriklere yer açmak için istemci önbelleğinde yaşlanmak istemiyorsanız, **içeriği istemci önbelleğinde Sürdür**' ü seçin.  

- Sitenin, dağıtım noktasındaki önyükleme görüntüsü paketini güncelleştirdiğinde yalnızca değiştirilen dosyaları dağıttığını belirtmek için **ikili değişiklik çoğaltmasını etkinleştir** (BDR) seçeneğini belirleyin. Bu ayar, siteler arasındaki ağ trafiğini en aza indirir. BDR, özellikle önyükleme görüntüsü paketi büyükse ve değişiklikler nispeten küçük olduğunda yararlıdır.  

- Önyükleme görüntüsünü PXE 'yi destekleyen bir dağıtımda kullanırsanız, **Bu önyükleme GÖRÜNTÜSÜNÜ PXE 'yi destekleyen dağıtım noktasından dağıt**' ı seçin. Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

#### <a name="data-access"></a>Veri Erişimi

**Veri erişimi** sekmesinde, paket paylaşma ayarlarını yapılandırabilirsiniz. Ortamınızda gerekiyorsa, **Bu paketteki içeriği dağıtım noktalarındaki bir paket paylaşımıyla kopyalama**seçeneğini ayarlayın. Daha sonra **paket paylaşımında özel bir ad kullanmak** ve özel **paylaşımın adını**belirtmek için ek seçeneğe sahip olursunuz. Bu seçeneği etkinleştirdiğinizde dağıtım noktalarında ek disk alanı gerekir. Bu önyükleme görüntüsünü alan tüm dağıtım noktaları için geçerlidir.

#### <a name="distribution-settings"></a>Dağıtım ayarları

**Dağıtım Ayarları** sekmesinde, aşağıdaki ayarlardan birini seçin:  

- **Dağıtım önceliği** listesinde, öncelik düzeyini belirtin. Configuration Manager, site birden çok paketi aynı dağıtım noktasına dağıttığı zaman bu öncelik listesini kullanır.  

- Tercih edilen dağıtım noktalarına isteğe bağlı içerik dağıtımını etkinleştirmek istiyorsanız, **isteğe bağlı dağıtım Için etkinleştir**' i seçin. Bu ayarı etkinleştirdiğinizde, bir istemci paketin içeriğini isterse ve içerik herhangi bir dağıtım noktasında kullanılabilir değilse, yönetim noktası içeriği dağıtır. Daha fazla bilgi için bkz. [isteğe bağlı içerik dağıtımı](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

- Sitenin önyükleme görüntüsünü önceden hazırlanan içerik için etkinleştirilen dağıtım noktalarına nasıl dağıtacağınızı belirtmek için **önceden hazırlanan dağıtım noktası ayarlarını**ayarlayın. Önceden hazırlanan içerik hakkında daha fazla bilgi için bkz. [İçeriği önceden hazırlama](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

#### <a name="content-locations"></a>İçerik konumları

**Içerik konumları** sekmesinde, dağıtım noktasını veya dağıtım noktası grubunu seçin ve aşağıdaki eylemleri kullanın:  

- **Doğrula**: Seçili dağıtım noktasındaki veya dağıtım noktası grubundaki önyükleme görüntüsü paketinin bütünlüğünü denetleyin.  

- Yeniden **Dağıt**: önyükleme görüntüsünü seçilen dağıtım noktasına veya dağıtım noktası grubuna yeniden dağıtın.  

- **Kaldır**: önyükleme görüntüsünü Seçili dağıtım noktasından veya dağıtım noktası grubundan silin.  

#### <a name="security"></a>Güvenlik

**Güvenlik** sekmesinde, bu nesne için izinleri olan yönetici kullanıcıları görüntüleyin.

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a> PXE için önyükleme görüntüsü yapılandırma  

PXE tabanlı bir dağıtım için önyükleme görüntüsü kullanabilmeniz için, önyükleme görüntüsünü PXE 'yi destekleyen bir dağıtım noktasından dağıtılacak şekilde yapılandırın.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **önyükleme görüntüleri** düğümünü seçin.  

2. Düzenlemek istediğiniz önyükleme görüntüsünü seçin.  

3. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

4. **Veri Kaynağı** sekmesinde **Bu önyükleme görüntüsünü PXE'yi destekleyen dağıtım noktasından dağıt** öğesini seçin. Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a> Birden çok dil yapılandırma

> [!TIP]
> Sürüm 1910 ' den başlayarak, varsayılan klavye düzeni bir önyükleme görüntüsünün özelliklerinde yapılandırılır. Daha fazla bilgi için bkz. [Özelleştirme](#customization).<!--4910348-->

Önyükleme görüntüleri dilden bağımsızdır. Bu işlevsellik, WinPE 'de görev dizisi metnini birden fazla dilde göstermek için bir önyükleme görüntüsü kullanmanızı sağlar. Önyükleme görüntüsü **Isteğe bağlı bileşenler** sekmesinden uygun dil desteğini ekleyin. Ardından, görüntülenecek dili göstermek için uygun görev sırası değişkenini ayarlayın. Dağıtılan işletim sisteminin dili, WinPE 'deki dilden bağımsızdır. WinPE 'nin kullanıcıya gösterdiği dil şu şekilde belirlenir:  

- Bir kullanıcı görev sırasını var olan bir IŞLETIM sisteminden çalıştırdığında, Configuration Manager otomatik olarak Kullanıcı için yapılandırılan dili kullanır. Bir zorunlu dağıtım son tarihinin sonucu olarak görev dizisi otomatik olarak çalıştırıldığında, Configuration Manager işletim sisteminin dilini kullanır.  

- PXE veya medya kullanan işletim sistemi dağıtımları için, **SMSTSLanguageFolder** DEĞIŞKENINDE dil kimliği değerini bir başlatma öncesi komutun parçası olarak ayarlayın. Bilgisayar WinPE'ye önyükleme yaptığında iletiler, değişkende belirttiğiniz dilde görüntülenir.  Belirtilen klasördeki dil kaynak dosyasına erişirken bir hata oluşursa veya değişkeni ayarlamazsanız, WinPE iletileri varsayılan dilde görüntüler.  

    > [!NOTE]  
    > Medyayı parolayla koruduğunuzda, kullanıcıdan parola isteyen metin her zaman WinPE dilinde görüntülenir.  

PXE veya medya tarafından başlatılan işletim sistemi dağıtımları için WinPE dilini ayarlamak için aşağıdaki yordamı kullanın.  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>PXE veya medya tarafından başlatılan işletim sistemi dağıtımı için Windows PE dilini ayarlama  

1. Önyükleme görüntüsünü güncelleştirmeden önce ilgili görev dizisi kaynak dosyasının (tsres.dll) site sunucusundaki ilgili dil klasöründe bulunduğunu doğrulayın. Örneğin, Ingilizce kaynak dosyası şu konumdadır: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Başlatma öncesi komutunuz kapsamında, **SMSTSLanguageFolder** ortam değişkenini ılgılı dil kimliğine ayarlayın. Dil KIMLIĞI, onaltılı biçimde değil, Decimal kullanılarak belirtilmelidir. Örneğin, dil KIMLIĞINI Ingilizce olarak ayarlamak için, klasör adının 00000409 onaltılık değerini değil **1033**ondalık değerini belirtin.