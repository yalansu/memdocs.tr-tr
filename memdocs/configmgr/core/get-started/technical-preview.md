---
title: Teknik Önizleme sürümleri
titleSuffix: Configuration Manager
description: Configuration Manager ' de yeni işlevsellik ve özellikleri test etmek için teknik önizleme dalı hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76d1edf8598e1abd71b6fd1db7faffa1750110d4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129129"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager için teknik önizleme

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makale, Configuration Manager aylık Technical Preview dalı hakkında ayrıntılı bilgi sağlar. Technical Preview, Microsoft 'un üzerinde çalıştığı yeni işlevselliği tanıtır. Henüz geçerli Configuration Manager dalına dahil olmayan yeni özellikler sunar. Bu özellikler, son olarak geçerli dalın bir güncelleştirmesine dahil edilebilir. Özellikleri sonlandırmadan önce, bunları denemenizi ve geri bildirimde bulunmamızı istiyoruz.

Bu sürüm teknik bir önizleme olduğundan, Ayrıntılar ve işlevler değişebilir.

Bu bilgiler Configuration Manager Technical Preview dalının tüm sürümleri için geçerlidir. Bu makalede, her yeni özellik, ilk görüntülenen Technical Preview sürümü ile birlikte listelenir. Örneğin, 2020 () için sürüm **2001** () `01` `20` . Her bir önizleme sürümü için ayrılmış makalelerin ayrı ayrı özelliklerini ayrıntılarıyla ayırın.

Configuration Manager *geçerli dalındaki* yenilikler hakkında daha fazla bilgi için bkz. [Configuration Manager artımlı sürümlerindeki](../plan-design/changes/whats-new-incremental-versions.md)yenilikler.

> [!Tip]
> Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın:`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a>Gereksinimler ve sınırlamalar

> [!IMPORTANT]
> Technical Preview yalnızca laboratuvar ortamında kullanılmak üzere lisanslanır. Microsoft Destek Hizmetleri sağlayamayabilir ve bazı özellikler teknik önizlemelerde kullanılamayabilir. Ayrıca, teknik önizleme yazılımı, ticari olarak sağlanmış yazılımlarla ilgili olarak azaltılan veya farklı güvenlik, gizlilik, erişilebilirlik, kullanılabilirlik ve güvenilirlik standartlarına sahip olabilir.

Çoğu ürün ön koşulu için [desteklenen yapılandırmalarda](../plan-design/configs/supported-configurations.md)bulunan bilgileri kullanın. Technical Preview dalı için aşağıdaki özel durumlar geçerlidir:

- Her bir yüklemesi, devre dışı olmadan önce 90 gün süreyle etkindir.

- Yalnızca İngilizce dili desteklenir.

- Yalnızca aşağıdaki kurulum komut satırı parametrelerini destekler:

  - `/silent`
  - `/testdbupgrade`

- Hizmet bağlantı noktası çevrimiçi moda yüklenir. Çevrimdışı modu desteklemez.

- Her bir Technical Preview sürümü için ayrı makaleler, uygun şekilde ek sınırlamalar ve gereksinimler içerir.

- Teknik Önizleme dalında aşağıdaki özellikler desteklenmez:

  - Bu önizleme dalına veya bu daldan [geçiş](../migration/migrate-data-between-hierarchies.md) yapın.

  - Bu önizleme dalına [yükseltin](../servers/deploy/install/upgrade-to-configuration-manager.md) .

  - CD. Latest klasöründen [Site Recovery](../servers/manage/recover-sites.md) .<!--507106-->

- Bu önizleme dalında güncel dala güncelleştirme desteği yoktur.

    > [!Note]
    > Bir önizleme sürümü için güncelleştirmeler kullanılabilir olduğunda, bu güncelleştirmeleri Configuration Manager konsolunun **güncelleştirmeler ve bakım** düğümünden bulup de yüklersiniz. Konsol içi yükseltme işleminin bir videosu için bkz. youtube.com üzerinde [Configuration Manager güncelleştirme paketleri yükleme](https://www.youtube.com/embed/KBd_EGFbUT8) .

- Yalnızca tek başına birincil siteyi destekler. Merkezi Yönetim sitesi, birden çok birincil site veya ikincil site desteği yoktur.

Configuration Manager Technical Preview dalı aşağıdaki ürünleri ve teknolojileri destekler:

- Aksi belirtilmediği sürece, Technical Preview dalı geçerli Dalla aynı SQL Server sürümlerini destekler. Daha fazla bilgi için bkz. [desteklenen SQL Server sürümleri](../plan-design/configs/support-for-sql-server-versions.md).

- Site, desteklenen herhangi bir [istemci işletim sistemi sürümünü](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)çalıştıran en fazla 10 istemciyi destekler.<!-- SCCMDocs#1656 -->

> [!Note]
> Bu ürünlerin bu içerik dahil edilmesi, destek yaşam döngüsünün ötesinde bir sürüm için destek uzantısı göstermez. Configuration Manager, destek yaşam döngüsünün ötesinde olan ürünleri desteklemez. Daha fazla bilgi için bkz. [Microsoft yaşam döngüsü ilkesi](https://support.microsoft.com/lifecycle).

## <a name="install-and-update"></a><a name="bkmk_install"></a>Yükleyip Güncelleştir

Laboratuvar kullanımı için Configuration Manager Technical Preview dalı, üretim kullanımı için Configuration Manager geçerli daldan farklıdır.

Önce Technical Preview dalının temel bir sürümünü yüklemeniz gerekir. Temel sürümü yükledikten sonra, en son önizleme sürümüyle yüklemenizi güncel hale getirmek için konsol içi güncelleştirmeleri kullanın. Teknik önizlemenin yeni sürümleri genellikle her ay kullanılabilir.

Microsoft, art arda üç sürüm kullanılabilir olana kadar her bir Technical Preview sürümünü destekler. Örneğin sürüm 1908 yayınlanmışsa, sürüm 1904 artık destede değildir. 1905, 1906 ve 1907 sürümleri desteğe kaldı. Bir taban çizgisi destek dışı kaldığında, desteklenen bir sürüme hemen güncelleştirmiş olduğunuz varsayılarak yeni bir Technical Preview sitesi yüklemek için yine de desteklenmektedir. Yeni bir temel sürüm kullanılabilir olana kadar eski taban çizgisi desteklenir. Taban çizgisinden sunulan en son sürüme güncelleştirin ve en son Technical Preview sürümünü yükleyinceye kadar güncelleştirme işlemini tekrarlayın.

> [!TIP]
> Teknik önizlemeye bir güncelleştirme yüklediğinizde, önizleme yüklemenizi bu yeni teknik önizleme sürümüne güncelleştireceksiniz. Teknik Önizleme yüklemesi hiçbir şekilde geçerli bir dal yüklemesine yükseltme seçeneği yoktur. Ayrıca, geçerli dal sürümünden güncelleştirmeleri hiçbir şekilde almaz.
>
> Yılda birkaç kez, aynı sürüm numarasına sahip Technical Preview dalı ve güncel dal sürümleri mevcuttur. Örneğin, Technical Preview sürüm 1910 ve geçerli bir dal sürümü 1910 vardır.

### <a name="active-baseline-versions"></a>Etkin temel sürümler

Sürümünden sonraki bir yıla kadar bir temel sürümü yükler. Yeni bir Technical Preview sitesi yüklediğinizde, en son temel sürümü kullanın. Aşağıdaki Configuration Manager Technical Preview dalı sürümleri, konsol içi güncelleştirmeler ve yeni temel sürümler olarak kullanılabilir:

- **Technical Preview sürüm 2007**

[Değerlendirme merkezinden](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)bir temel sürüm indirin.

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a>Geri bildirim sağlama

Technical Preview sürümündeki yeni özelliklerle ilgili geri bildirimlerinizi duymak isteriz. Daha fazla bilgi için bkz. [ürün geri bildirimi](../understand/find-help.md#product-feedback).

Görmek istediğiniz yeni özellikler hakkında fikirleriniz varsa bize bize izin verin! Yeni fikirler gönderebilir ve fikirlerinizi daha fazla oylayın: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a>En son sürümdeki özellikler

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2007.md) <!--ID-->

Aşağıdaki özellikler en son Configuration Manager Technical Preview sürümü ile sunulmaktadır:

### <a name="technical-preview-version-2008"></a>Technical Preview sürüm 2008

- [Koleksiyon sorgu önizlemesi](2020/technical-preview-2008.md#collection-query-preview) <!--7380401-->
- [Özellik güncelleştirmeleri için SetupDiag hatalarını çözümle](2020/technical-preview-2008.md#bkmk_setupdiag) <!--4385028-->
- [Senaryo durumunu izleme](2020/technical-preview-2008.md#bkmk_health) <!--7699463-->
- [Koleksiyon değerlendirme görünümü](2020/technical-preview-2008.md#bkmk_colleval) <!--6251274-->
- [Bkz. konsolundaki görev sırası boyutu](2020/technical-preview-2008.md#bkmk_tssize) <!--7645732-->
- [Eski toplanan tanılama dosyalarını Sil görevi](2020/technical-preview-2008.md#bkmk_logs) <!--6503308-->
- [Nesneleri geçerli klasöre aktar](2020/technical-preview-2008.md#bkmk_folder) <!--6601203-->

> [!NOTE]
> Technical Preview 'un önceki bir sürümünde kullanılabilen özellikler sonraki sürümlerde de kullanılabilir durumda kalır. Benzer şekilde, geçerli dala eklenen Configuration Manager özellikler, Technical Preview dalında kullanılabilir kalır.

## <a name="features-in-recent-technical-previews"></a>Son teknik önizlemelerde Özellikler

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Şu özellikler, geçerli dal sürümü 2006 ' den bu yana Configuration Manager Technical Preview dalının önceki sürümleriyle yayımlanmıştır:

> [!TIP]
> Yeni bir geçerli dal sürümü kullanılabilir olduğunda, bu sürümde kullanılabilen özellikler en son *Yenilikler* makalesinde listelenmiştir. Daha fazla bilgi için bkz. [artımlı sürümlerindeki](../plan-design/changes/whats-new-incremental-versions.md#supported-versions)yenilikler.

### <a name="technical-preview-version-2007"></a>Technical Preview sürüm 2007

- [Kiracı iliştirme: Microsoft Endpoint Manager Yönetim Merkezi 'nde donanım envanterini görüntüleme](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [İstemci veri kaynakları panosundaki geliştirmeler](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [Artık bazı konsol alanlarında kullanılan sabit genişlikli yazı tipi](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [Görev sırası ilke boyutunu Yönet](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [Yönetim merkezinde cihaz zaman çizelgesinde iyileştirmeler](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

## <a name="features-in-previous-technical-previews"></a>Önceki teknik önizlemelerde Özellikler

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Aşağıdaki özellikler Configuration Manager Technical Preview dalının önceki sürümleriyle yayımlanmıştır. Bu özellikler sonraki sürümlerde kullanılabilir kalır, ancak henüz geçerli dalda kullanılabilir değildir.

| Özellik        | Technical Preview sürümü |
|----------------|---------------------------|
| Ortak yönetilen cihazlarda Şirket Portalı uygulamasını kullanma <!--3601237--> | [Teknik Önizleme 2006](2020/technical-preview-2006.md#bkmk_portal) |
| CMG aracılığıyla kullanılabilir uygulamalarda iyileştirmeler <!--7033501--> | [Teknik Önizleme 2006](2020/technical-preview-2006.md#bkmk_availapp) |
| Kiracı Iliştirme: Microsoft Endpoint Manager Yönetim Merkezi 'ndeki Configuration Manager eylemlerine yönelik Iyileştirmeler <!--7518897--> | [Teknik Önizleme 2006](2020/technical-preview-2006.md#bkmk_apps) |
| Kiracı iliştirme: Yönetim merkezinde cihaz zaman çizelgesi <!--7141381--> | [Teknik Önizleme 2005](2020/technical-preview-2005.md#bkmk_timeline) |
| Kiracı iliştirme: yönetim merkezinden bir uygulama yükler <!--6024389--> | [Teknik Önizleme 2005](2020/technical-preview-2005.md#bkmk_apps) |
| Kiracı iliştirme: yönetim merkezinden CMPivot <!--6024392--> | [Teknik Önizleme 2005](2020/technical-preview-2005.md#bkmk_cmpivot) |
| Kiracı iliştirme: yönetim merkezinden betikleri çalıştırma <!--6234688--> | [Teknik Önizleme 2005](2020/technical-preview-2005.md#bkmk_scripts) |
| Bulut yönetimi ağ geçidi cmdlet 'leri geliştirmeleri <!--6978300--> | [Teknik Önizleme 2005](2020/technical-preview-2005.md#bkmk_pwshcmg) |
| Microsoft 'a kurulum ve yükseltme başarısızlıklarını bildir <!--5622909--> | [Teknik Önizleme 2005](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) |
| İçerik kitaplığı Temizleme aracında geliştirmeler <!--6887878--> | [Teknik Önizleme 2005](2020/technical-preview-2005.md#bkmk_content) |
| Keşif verilerini konsolundan kopyalama <!--6890051--> | [Teknik Önizleme 2004](2020/technical-preview-2004.md#bkmk_copydisco) |
| PowerShell sürüm 7 desteği <!--6023299--> | [Teknik Önizleme 2004](2020/technical-preview-2004.md#bkmk_pwsh7) |
| Yeni geri bildirim Sihirbazı <!--3180826--> | [Teknik Önizleme 2003](2020/technical-preview-2003.md#bkmk_feedback) |
| Microsoft 'a gönderilen geri bildirim sorgusu <!--6488450--> | [Teknik Önizleme 2003](2020/technical-preview-2003.md#bkmk_smile) |
| Geri bildirime dosya iliştirme <!--3556011--> | [Teknik Önizleme 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Çok noktaya yayın özellikli dağıtım noktalarında iyileştirmeler <!--3785535--> | [Teknik Önizleme 1908,2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Aşamalı dağıtım şablonları <!--4961086--> | [Teknik Önizleme 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Bulut yönetimi ağ geçidini kullanarak her yerde uzaktan denetim <!--4575930--> | [Teknik Önizleme 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Cloud Services maliyet tahmini <!--3555774--> | [Teknik Önizleme 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| İstemci tabanlı PXE Yanıtlayıcı hizmeti <!--3556018, fka 1357148--> | [Teknik Önizleme 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| IPv6 için PXE ağ önyükleme desteği <!--3601254, fka 1269793--> |[Teknik Önizleme 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Azure Active Directory kullanma <!--3607315, fka 1322145--> | [Teknik Önizleme 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Varlık Yönetim Bilgileri geliştirmeleri <!--3601024, fka 1307390--> | [Teknik Önizleme 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Ayrıca bkz.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Configuration Manager’ı laboratuvarda değerlendirme](evaluate-with-lab-environment.md)
- [Configuration Manager artımlı sürümlerindeki yenilikler](../plan-design/changes/whats-new-incremental-versions.md)
- [Configuration Manager'a Giriş](../understand/introduction.md)

> [!Tip]
> Etkinleştirme onayı gerektiren güncel dal özellikleri hakkında daha fazla bilgi için bkz. [yayın öncesi Özellikler](../servers/manage/pre-release-features.md).
>
> İlk olarak etkinleştirmeniz gereken geçerli dal özellikleri hakkında daha fazla bilgi için bkz. [güncelleştirmelerden isteğe bağlı özellikleri etkinleştirme](../servers/manage/install-in-console-updates.md#bkmk_options).
