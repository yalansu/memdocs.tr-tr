---
title: Ön izleme
titleSuffix: Configuration Manager
description: Ön tümleştirme önizlemesi için yönergeler
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3871b51c85d0474c4bea2da24fc5a2f31d02f59f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719739"
---
# <a name="uup-private-preview-instructions"></a>Özel Önizleme yönergeleri

> [!Note]  
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez.  

## <a name="introduction"></a>Giriş

Birleşik güncelleştirme platformu (UUP), tüketici ve kurumsal cihazların Iş için Windows Update güncelleştirmeleri almak için kullandığı paketleme ve yayımlama platformudur. Dağıtım için özel Önizleme programı, müşterilerin Windows hizmet verme ile raporlayabileceği sorunları çözmesine yardımcı olmak için, Microsoft 'un Configuration Manager içindeki güncelleştirme kullanımını doğrulamasına yardımcı olan müşterilere yöneliktir. Bu güncelleştirmeler şu anda genel kullanıma sunulmamaktadır.

UUP hakkında daha fazla bilgi için şu Windows blog gönderisine bakın: [Birleşik güncelleştirme platformumuz (uup) Için bir güncelleştirme](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## <a name="benefits"></a>Avantajlar

Windows 10 UUP özelliği ve toplu güncelleştirmeler, müşterilerin hizmet verme sorunlarını bugün bildirme hakkında birden çok sorunu çözmeye yardımcı olur.

### <a name="feature-updates"></a>Özellik güncelleştirmeleri

- Windows Update işlemi, bir özellik güncelleştirmesi ile Isteğe bağlı özellikleri (FOD) ve dil paketlerini korur.

- Doğrudan en son güvenlik uyumluluk düzeyine güncelleştirin. Bir özellik güncelleştirmesinden hemen sonra güvenlik güncelleştirmeleri yüklemeniz gerekmez. Microsoft, her ay en son birikimli güvenlik güncelleştirmesiyle yeni bir özellik güncelleştirmesi yayımlar. Her ay özellik güncelleştirme içeriğini indirmeniz veya dağıtmanız gerekmez. Yalnızca toplu güncelleştirme ile paylaşımları olan güvenlik güncelleştirmesini indirebilirsiniz.

### <a name="cumulative-updates"></a>Toplu güncelleştirmeler

- UıUP ile toplu güncelleştirmeler, aylık toplu güvenlik güncelleştirmeleri ile yığın güncelleştirmelerine (SSU) hizmet vermeye dahildir. Bu davranış, bu iki güncelleştirmeyi düzenleme ile ilgili sorunları çözer. Toplu güncelleştirmeleri yüklemek için bakım yığını güncelleştirmelerinin yerinde olduğundan emin olur. Bu ilişkileri yönetmeniz ve yönetmeniz gerekmez.

- Toplu güncelleştirmeler, FOD ve Language Pack içeriğini çevrimdışına dağıtmanıza olanak tanır. Bu davranış, kullanıcıların bunları isteğe bağlı olarak eklemesini sağlar. Kullanıcıların Internet 'ten indirilmesi gerekmez ve bu içeriği önceden hazırlama hakkında bilgi almanız gerekmez.

## <a name="set-up"></a>Ayarla

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. WSUS KIMLIĞINIZI Microsoft 'a gönderin

Özel önizlemeye katılmak için, WSUS KIMLIĞINIZI, ön baskı önizleme kişiyle paylaşabilirsiniz. Microsoft, WSUS ortamınızı, ön izleme programına onaylar. Bu KIMLIK olmadığında, Önizleme Genel olana kadar hiçbir güncelleştirme işlemi göremezsiniz.

WSUS KIMLIĞINIZI almak için aşağıdaki PowerShell betiğini çalıştırın:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

**Muurl** özelliği olmalıdır `https://sws.update.microsoft.com`. Bunu değiştirmek için aşağıdaki destek makalesindeki çözünürlüğe bakın: [WSUS eşitlemesi, SoapException ile başarısız olur](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### <a name="2-update-configuration-manager"></a>2. güncelleştirme Configuration Manager

Bu ön önizlemeyi desteklemek için Configuration Manager sitenizde aşağıdaki değişiklikleri yapın:

#### <a name="diagnostics-and-usage-data-level"></a>Tanılama ve kullanım veri düzeyi

Bu önizleme sırasında Configuration Manager tanılama ve veri kullanım düzeyini artırmayı göz önünde bulundurun. **Tam** düzey, Microsoft 'un bu yeni özellik ile ilgili sorunları daha iyi çözümlemesine ve gidermeye yardımcı olur. Daha fazla bilgi için bkz. [sürüm 1906 için tanılama kullanım verileri toplama düzeyleri](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md).

#### <a name="install-the-latest-update"></a>En son güncelleştirmeyi yükler

1. Siteyi aşağıdaki güncelleştirmelerden biriyle güncelleştirin:

    - [Güncelleştirme paketi](https://support.microsoft.com/help/4500571) ile sürüm 1902
    - [Sürüm 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    Daha fazla bilgi için bkz. [konsol içi güncelleştirmeleri yüklemeyi](../../core/servers/manage/install-in-console-updates.md).

2. İstemcileri güncelleştirin.  

    - Bu işlemi basitleştirmek için otomatik istemci yükseltmesini kullanmayı göz önünde bulundurun. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

    - İstemciye, *6 GB kullanılmayan içeriğin çevresinde gereksiz indirmeyi* engellemek için, güncelleştirmeleri hedeflediğiniz tüm istemcileri güncelleştirin.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. Windows istemcilerini desteklenen bir sürüme güncelleştirin

Güncelleştirme güncelleştirmelerinin başarılı bir şekilde yüklenmesi için aşağıdaki güncelleştirmelerden her ikisini de kurun:

1. Belirli bir en düşük toplu aylık uyumluluk düzeyi.

2. Microsoft Update kataloğundan, toplu ve güvenlikle ilgili özel olmayan bir güncelleştirme. Güncelleştirmeyi dağıtım için Configuration Manager içine aktarmak için bkz. [Microsoft Update kataloğundan güncelleştirmeleri Içeri aktarma](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Desteklenen Windows 10 sürümleri ve gerekli güncelleştirmeler

| Windows 10 sürümü | En düşük uyumluluk düzeyi | Ek katalog güncelleştirmesi |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, sürüm 1903** | RTM | 7 Kasım 2019, [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10, sürüm 1809** | Ağustos 2019, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7 Kasım 2019, [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, sürüm 1803** | Nisan 2019, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7 Kasım 2019, [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, sürüm 1709** | Nisan 2019, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7 Kasım 2019, [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - 7 Kasım 2019 ek Katalog güncelleştirmesini uygulamadan önce istemciye 12 Kasım 2019 güncelleştirme uygularsanız, UUP 'yi desteklemek için gereken Windows Update aracı değişikliklerinin üzerine yazılır. Bu senaryodaki istemcileri düzeltmek için, 12 Kasım 2019 güncelleştirme yüklendikten sonra ek Katalog güncelleştirmesini uygulayın.
> - İstemciye bir özellik güncelleştirmesi uygularsanız, yükseltme tamamlandıktan sonra ek Katalog güncelleştirmesini yeniden yüklemeniz gerekir.
> - Özellik güncelleştirmelerini test etmek daha kolay hale getirmek için güncelleştirmeleri Configuration Manager içine aktarın. Daha fazla bilgi için bkz. [Microsoft Update kataloğundan güncelleştirmeleri Içeri aktarma](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog). Özellik Güncelleştirmesi tamamlandıktan sonra, ek Katalog güncelleştirmesi **gerekli**olduğu gibi görünür ve bu da, en yüksek işletim düzeyi sürümüne otomatik dağıtıma olanak tanır.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. kullanılabilir olduğunda istemcilerin Delta içeriğini indirmesine izin ver

Güncelleştirme güncelleştirmelerinin doğru indirilmesi için, istemci ayarını **istemcilerin kullanılabilir olduğunda Delta içerik yüklemelerine Izin verecek**şekilde etkinleştirin. Bu ayar Configuration Manager, Windows Update aracısının (WUA) istemcilere indirmek için gerekli içeriği belirlemesine izin verir. Bu davranış, Configuration Manager istemcisinin, güncelleştirme ile ilişkili tüm içeriği indirdiği varsayılan değer yerine yapılır. Bu ayarı etkinleştirdiğinizde, WUA her bir güncelleştirme için gereken ek içeriği belirler. Örneğin, yalnızca gerekli FOD ve Language paketleri.

Bu ayarı etkinleştirdiğinizde, internet 'ten sunucu içeriği indirmelerini etkilemez. Yalnızca istemci indirmeleri için geçerlidir. İstemcilere dağıtım güncelleştirmelerini dağıtmadan önce, bu ayarı, UıUP için desteklenen sürümleri karşılayan istemcilere uygulayın. Önkoşul istemci güncelleştirmeleri WSUS ve Configuration Manager ile ilgili güncelleştirme uyumluluk sorunlarını düzeltir.

Bu istemci ayarı hakkında daha fazla bilgi için bkz. [istemci ayarları-yazılım güncelleştirmeleri](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)

### <a name="5-review-your-software-update-infrastructure"></a>5. yazılım güncelleştirme altyapınızı gözden geçirin

Güncelleştirme güncelleştirmelerini eşitlemeden önce otomatik dağıtım kurallarınızı (ADR) ve bakım planlarınızı gözden geçirin. Bu güncelleştirmelerin otomatik olarak dağıtılmasını istemiyorsanız, ADRs 'nizi filtreleyecek şekilde değiştirin. Daha fazla bilgi için bkz. [eşitlenmiş güncelleştirme güncelleştirmelerini bulma](#how-to-find-synced-uup-updates). Varsayılan olarak, mevcut bakım planları yalnızca kurulum dışı güncelleştirmeleri dağıtır. Bu davranışı değiştirmek için bakım planlarını değiştirebilirsiniz.

Uyumluluk raporlarınızı gözden geçirin ve gerektiğinde gözden geçirin. Örneğin, tüm ürünlerde uyumluluğu ölçseniz, artık hem ön ve olmayan toplu güncelleştirmeleri görürsünüz. Cihazlar her iki güncelleştirme türüne karşı uyumluluk rapor eder. Uyumluluk raporlarınızın bu değişikliği ele aldığınızdan emin olun.

## <a name="enable-uup-and-start-testing"></a>Başlangıç ve başlatma testini etkinleştir

### <a name="select-products-and-classifications-to-sync"></a>Eşitlenecek ürünleri ve sınıflandırmaları seçin

Güncelleştirme güncelleştirmeleri eşitlenmeye başlamaya hazırsanız ve Microsoft WSUS KIMLIĞINIZI onaylamışsa, yeni ürünleri etkinleştirin:

1. Yeni ürünleri doldurmak için [yazılım güncelleştirmelerini eşitler](../get-started/synchronize-software-updates.md) .  

2. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.

3. Bir merkezi yönetim sitesi (CAS) veya tek başına birincil site olan en üst düzey siteyi seçin.

4. Şeritte, **site bileşenlerini Yapılandır**' ı seçin ve **yazılım güncelleştirme noktası**' nı seçin.

5. **Ürünler** sekmesine geçin ve aşağıdaki ürünlerden birini veya daha fazlasını seçin: 

    - **Windows 10 ön Önizleme**
    - **Windows Server yedekleme önizlemesi**

6. **Sınıflandırmalar** sekmesine geçin ve aşağıdaki seçenekleri belirleyin:  

    - **Güvenlik güncelleştirmeleri**: toplu güncelleştirmeleri görmek için  
    - **Yükseltmeler**: Özellik güncelleştirmelerini görmek için  

7. Yeni güncelleştirme güncelleştirmelerini görmek için yazılım güncelleştirmelerini yeniden eşitler.

### <a name="how-to-find-synced-uup-updates"></a>Eşitlenmiş güncelleştirme güncelleştirmelerini bulma

Çalışma ortamınızdaki güncelleştirmeleri eşitlendikten sonra, test etmek için Configuration Manager konsolunda bulun. Önizleme güncelleştirmelerini bulmanın iki yolu vardır:

- Bu önizleme güncelleştirmeleri ayrı bir üründe bulunduğundan, bu güncelleştirmeleri bulmak için filtrelemek üzere ürünü kullanın. Bakım planının ürün filtresini kullanarak, ön veya olmayan özellik güncelleştirmelerini dağıtın.  

- **Yazılım kitaplığı**'Nın **tüm yazılım güncelleştirmeleri** ve **tüm Windows 10 güncelleştirmeleri** düğümlerinde, yeni bir isteğe bağlı sütun **etiketi**vardır. Bu özellik ADRs 'de bir filtre olarak da kullanılabilir. Güncelleştirme güncelleştirmeleri için bu alanda için `UUP`arama yapın. Güncelleştirme olmayan güncelleştirmeler için boştur.  

### <a name="updates-available-during-preview"></a>Önizleme sırasında güncelleştirmeler var

Microsoft tarafından yayınlanan tüm Windows 10 güncelleştirmeleri hakkında daha fazla bilgi için bkz. [Windows 10 sürüm bilgileri](https://docs.microsoft.com/windows/release-information/).

#### <a name="cumulative-updates-to-test"></a>Sınanacak toplu güncelleştirmeler

Birden çok yukarı etiketli güncelleştirme görüyorsanız, **eylül 2019** (2019-09) güncelleştirmesiyle veya sonraki bir sürümle başlayın. Örneğin:

- 2019-09 x64 tabanlı sistemler için Windows 10 sürüm 1809 toplu güncelleştirmesi (KB4512578)
- 2019-09 x64 tabanlı sistemler için Windows 10 sürüm 1803 toplu güncelleştirmesi (KB4516058)
- 2019-09 x64 tabanlı sistemler için Windows 10 sürüm 1709 toplu güncelleştirmesi (KB4516066)

#### <a name="feature-updates-to-test"></a>Sınanacak özellik güncelleştirmeleri

Birden çok yukarı etiketli güncelleştirme görüyorsanız, **eylül 2019** (2019-09B) güncelleştirmesi veya sonraki bir sürümle başlayın. Örneğin:

- Windows 10 için özellik güncelleştirmesi, sürüm 1809 x64 2019-09B
- Windows 10 için özellik güncelleştirmesi, sürüm 1803 x64 2019-09B

## <a name="scenarios-to-test"></a>Sınanacak senaryolar

### <a name="test-feature-updates"></a>Test özelliği güncelleştirmeleri

- Doğrudan seçtiğiniz güvenlik uyumluluk düzeyine güncelleyin  

- Güncelleştirmeden önce FODs ve dil paketlerini yükler. Güncelleştirmenin bu bileşenleri koruyabilmesi için emin olun.  

### <a name="test-cumulative-updates"></a>Toplu güncelleştirmeleri test et

Önizleme sırasında, birden çok arka arkaya güncelleştirme için, istemci türü güncelleştirmesini kullanarak istemcileri uyumlu tutun. Bu test, devam eden davranışı anlamanıza yardımcı olur.

### <a name="test-content"></a>Test içeriği

Her ana sürüm için ilk güncelleştirme (1809, 1803, 1709), mimari ve dil birleşimi büyük gibi görünür. Bu boyut hem dosya hem de disk alanı halinde olduğundan, daha önce kurulum dışı güncelleştirmelerle birlikte gördük ile karşılaştırılır. Bu ek içerik, öncelikle toplu güncelleştirmeler için tüm FOD ve dil paketlerine yöneliktir. Özellik güncelleştirmeleri için, bu ilk güncelleştirme için ek büyük içerikler vardır.

Gelecekteki toplu ve özellik güncelleştirmeleri için, sitenin indirdiği ve dağıttığı yeni içerik miktarı çok daha küçüktür. Güncelleştirme, tüm FOD ve dil paketi içeriğini güncelleştirmeler arasında akıllıca paylaşır. Bu paylaşılan içeriği yeniden indirmesi veya yeniden dağıtmanız gerekmez. Önizleme sırasında, Windows 10 sürüm 1709 ve 1803 ' de, bu aylık indirme işlemi, toplu güncelleştirmelerin, toplu güncelleştirme boyutuyla aynı şekilde olduğu gibidir. Windows 10 sürüm 1809 ve sonrasında, toplu güncelleştirmenin artımlı indirmesi her ay çok daha küçüktür.

*Express olmayan*bir 12 aylık dönemde indirilen ve dağıtılan toplam içeriğe baktığınızda, uup olmadan Windows 10 sürüm 1803, uup ile aynı sürüm 1809 ile aynı olmalıdır. Sürümün tüm kullanım ömrü boyunca indirilen ve dağıtılan toplam içerik, sürüm 1809 ' de UUP ' de küçüktür.

### <a name="supported-content-channels"></a>Desteklenen içerik kanalları

Önizleme için, tipik gerçek dünyada senaryolarınızı test edin. UıUP, aşağıdakiler dahil olmak üzere tüm içerik kanallarını destekler:

- Windows teslim Iyileştirme (DO)
  - Bunu kullanırken doğru yapılandırıldığından emin olun. Daha fazla bilgi için bkz. [Windows 10 güncelleştirme teslimini iyileştirme](optimize-windows-10-update-delivery.md).
- Configuration Manager eş önbelleği
- Windows BranchCache
- **Dağıtım paketi yok** seçeneğini kullanın ve istemciler Microsoft Update doğrudan indirin. Teslim iyileştirme ile bu seçeneği kullanın.
- Üçüncü taraf alternatif içerik sağlayıcıları

İçerik kanalları hakkında daha fazla bilgi için bkz. [Windows 10 güncelleştirme teslimini iyileştirme](optimize-windows-10-update-delivery.md).

<!-- TODO: Addlink to WSUS Perf documentation-->
