---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724114"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a>Görüntüye yazılım güncelleştirmeleri uygulama

> [!Note]  
> Bu bölüm hem **Işletim sistemi görüntüleri** hem de **işletim sistemi yükseltme paketleri**için geçerlidir. Windows görüntü dosyasına (WıM) başvurmak için "görüntü" genel terimini kullanır. Bu nesnelerin her ikisinde de Windows yükleme dosyalarını içeren bir WıM vardır. Yazılım güncelleştirmeleri, her iki nesnede da bu dosyalar için geçerlidir. Bu işlemin davranışı her iki nesne arasında aynıdır.  

Her ay görüntüde geçerli olan yeni yazılım güncelleştirmeleri vardır. Yazılım güncelleştirmelerini uygulayabilmeniz için önce aşağıdaki önkoşullara sahip olmanız gerekir:

- Yazılım güncelleştirme altyapısı  
- Yazılım güncelleştirmeleri başarıyla eşitlendi  
- Yazılım güncelleştirmeleri site sunucusundaki içerik kitaplığına indirildi  

Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini dağıtma](../../../sum/deploy-use/deploy-software-updates.md).  

Geçerli yazılım güncelleştirmelerini belirli bir zamanlamaya göre bir görüntüye uygulayın. Bu işleme bazen *çevrimdışı bakım*denir. Bu zamanlamada, Configuration Manager seçili yazılım güncelleştirmelerini görüntüye uygular. Ayrıca, güncelleştirilmiş görüntüyü dağıtım noktalarına yeniden dağıtabilir.

> [!Important]  
> Sürüme göre görüntü için geçerli olan herhangi bir yazılım güncelleştirmesini seçebilirsiniz, ancak DıSM yalnızca belirli türdeki güncelleştirmeleri görüntüye uygulayabilir. **Offlineservicingmgr. log** dosyası şu girişi gösterir: `Not applying this update binary, it is not supported`.<!-- SCCMDocs issue 1324 -->

Site veritabanı, içeri aktarma sırasında uygulanan yazılım güncelleştirmeleri de dahil olmak üzere görüntüyle ilgili bilgileri depolar. İlk eklendikten sonra görüntüye uyguladığınız yazılım güncelleştirmeleri de site veritabanında depolanır. Yazılım güncelleştirmelerini uygulamak için sihirbazı başlattığınızda, sitenin henüz yansımaya uygulanmadığı ilgili yazılım güncelleştirmelerinin listesini alır. Configuration Manager, seçtiğiniz yazılım güncelleştirmelerini site sunucusundaki içerik kitaplığından kopyalar. Ardından, yazılım güncelleştirmelerini görüntüye uygular.  

### <a name="servicing-process"></a>Bakım işlemi

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **Işletim sistemi görüntüleri** ya da **işletim sistemi yükseltme paketleri**' ni seçin.  

2. Yazılım güncelleştirmelerinin uygulanacağı nesneyi seçin.  

3. Şeritte, Sihirbazı başlatmak için **güncelleştirmeleri zamanla** ' yı seçin.  

4. **Güncelleştirmeleri Seç** sayfasında, görüntüye uygulanacak yazılım güncelleştirmelerini seçin. Güncelleştirmelerin listesi sihirbazda gözükme biraz zaman alabilir. Meta verilerde dize aramak için **filtreyi** kullanın. **X86**, **x64**veya **Tümünü**filtrelemek için **sistem mimarisi** açılan listesini kullanın. Listedeki bir, çok veya tüm güncelleştirmeleri seçebilirsiniz. Güncelleştirmeler seçimini tamamladıktan **sonra ileri**' yi seçin.  

5. **Zamanlama Belirle** sayfasında aşağıdaki ayarları belirtin ve **İleri**'ye tıklayın.  

    1. **Zamanlama**: sitenin görüntüye yazılım güncelleştirmelerini uyguladığı zamanlamayı belirtin.  

    2. **Hatada devam et**: hata olduğunda bile görüntüye yazılım güncelleştirmeleri uygulamaya devam etmek için bu seçeneği belirleyin.  

    3. **Dağıtım noktalarını görüntüyle Güncelleştir**: site yazılım güncelleştirmelerini uyguladıktan sonra dağıtım noktalarında görüntüyü güncelleştirmek için bu seçeneği belirleyin.  

6. Güncelleştirme zamanlama Sihirbazı 'Nı doldurun.  

> [!NOTE]  
> Yük boyutunu en aza indirmek için, işletim sistemi yükseltme paketleri ve işletim sistemi görüntülerinin Bakımı eski sürümü kaldırır.  

### <a name="servicing-operations"></a>Bakım işlemleri

Configuration Manager konsolunda, **Işletim sistemi görüntüleri** veya **Işletim sistemi yükseltme paketleri** düğümünde, şu sütunları görünüme ekleyin:

- **Zamanlanan güncelleştirmeler tarihi**: Bu özellik, tanımladığınız bir sonraki zamanlamayı gösterir.  
- **Zamanlanan güncelleştirmeler durumu**: Bu özellik durumu gösterir. Örneğin, **başarılı** veya **işlemde**.  

Belirli bir görüntü nesnesi seçin ve ardından Ayrıntılar bölmesindeki **güncelleştirme durumu** sekmesine geçin. Bu sekme görüntüdeki güncelleştirmelerin listesini gösterir.

Belirli bir görüntü nesnesi seçin ve şeritte **Özellikler** ' i seçin. **Yüklü güncelleştirmeler** sekmesi görüntüdeki güncelleştirmelerin listesini gösterir. **Bakım** sekmesi, geçerli bakım zamanlamasının ve uygulamak üzere zamanladığınız güncelleştirmelerin salt okunurdur.

Durum **Işlem sırasında**, şeritte **zamanlanan güncelleştirmeleri iptal et** ' i seçebilirsiniz. Bu eylem, etkin bakım işlemini iptal eder.

Bu işlemde sorun gidermek için, site sunucusundaki **Offlineservicingmgr. log** ve **DISM. log** dosyalarını görüntüleyin. Daha fazla bilgi için bkz. [günlük dosyaları](../../../core/plan-design/hierarchy/log-files.md).

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a>Çevrimdışı işletim sistemi görüntüsü bakımı için sürücüyü belirtin

<!--1358924-->

Sürüm 1810 ' den başlayarak, işletim sistemi görüntülerinin çevrimdışı bakımı sırasında Configuration Manager kullanacağı sürücüyü belirtin. Bu işlem, geçici dosyalarla büyük miktarda disk alanı kullanabilir. Bu seçenek, kullanılacak sürücüyü seçme esnekliği sağlar.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Şeritte, **site bileşenlerini Yapılandır** ' a tıklayın ve **işletim sistemi dağıtımı**' nı seçin.  

2. **Çevrimdışı hizmet** sekmesinde, **görüntülerin çevrimdışı Bakımı tarafından kullanılacak yerel bir sürücü**seçeneğini belirtin.  

Varsayılan olarak, bu ayar **otomatiktir**. Bu değerle Configuration Manager yüklendiği sürücüyü seçer.

Site sunucusunda mevcut olmayan bir sürücü seçerseniz, Configuration Manager otomatik ' i **seçtikten**sonra aynı şekilde davranır.

Çevrimdışı bakım sırasında, Configuration Manager geçici dosyaları klasöründe depolar `<drive>:\ConfigMgr_OfflineImageServicing`. Ayrıca, işletim sistemi görüntüsünü bu klasöre bağlar.

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a>İyileştirilmiş görüntü Bakımı

<!--3555951-->

Sürüm 1902 ' den başlayarak, bir işletim sistemi görüntüsüne yazılım güncelleştirmeleri uyguladığınızda, yenisiyle değiştirilen tüm güncelleştirmeleri kaldırarak çıktıyı iyileştirmek için yeni bir seçenek vardır. Çevrimdışı hizmet verme iyileştirmesi yalnızca tek bir dizine sahip görüntüler için geçerlidir.

Siteyi bir işletim sistemi görüntüsüne yazılım güncelleştirmeleri uygulamak üzere zamanladığınızda, Windows Dağıtım Görüntüsü Bakımı ve yönetimi (DıSM) komut satırı aracını kullanır. Bakım işlemi sırasında, bu değişiklik aşağıdaki iki ek adımı tanıtır:  

- DıSM 'YI, bağlı çevrimdışı görüntüde parametrelerle `/Cleanup-Image /StartComponentCleanup /ResetBase`birlikte çalıştırır. Bu komut başarısız olursa, geçerli bakım işlemi başarısız olur. Görüntüde hiçbir değişiklik yapmaz.  

- Configuration Manager görüntüye değişiklikleri kaydettikten ve dosyayı dosya sisteminden kaldırdıktan sonra, görüntüyü başka bir dosyaya dışarı aktarır. Bu adım DıSM parametresini `/Export-Image`kullanır. Gereksiz dosyaları görüntüden kaldırır, bu da boyutu azaltır.  

Microsoft çevrimdışı görüntülerinize düzenli olarak güncelleştirmeleri uygulamanızı önerir. Bir yansımaya her hizmet yaptığınızda bu seçeneği kullanmanız gerekmez. Bu işlemi her ay yaptığınızda, bu yeni seçenek size zaman içinde kullanarak en büyük avantaj sağlar. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini yüklemeye yönelik öneriler adım](../../understand/install-software-updates.md#recommendations).

Bu seçenek, servis verilen görüntünün genel boyutunu azaltmaya yardımcı olsa da işlemin tamamlanması daha uzun sürer. Uygun zamanlarda bakım zamanlamak için Sihirbazı kullanın. Ayrıca, site sunucusunda ek depolama alanı gerektirir. Siteyi alternatif bir konum kullanacak şekilde özelleştirebilirsiniz. Daha fazla bilgi için bkz. [çevrimdışı işletim sistemi görüntüsü bakımı için sürücüyü belirtme](#bkmk_servicing-drive).

#### <a name="process-to-optimize-image-servicing"></a>Görüntü bakımını iyileştirmek için işlem

1. [Hizmet sürecini](#servicing-process)başlatın.  

2. **Zamanlamayı belirle** sayfasında, **görüntü güncelleştirildikten sonra yenisiyle değiştirilen güncelleştirmeleri kaldırma**seçeneğini belirleyin. Bu seçenek otomatik olarak etkinleştirilmez. Görüntüde birden fazla dizin varsa, bu seçeneği kullanamazsınız.  

3. Görüntü Bakımı zamanlamak için Sihirbazı doldurun.  

**OfflineServicing. log**kullanarak işlemi doğrulayın ve izleyin.
