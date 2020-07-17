---
title: Güncelleştirmeler ve bakım
titleSuffix: Configuration Manager
description: Güncelleştirmeler ve bakım adlı, önerilen güncelleştirmeleri bulmayı ve yüklemeyi kolaylaştıran konsol içi hizmet yöntemi hakkında bilgi edinin.
ms.date: 06/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5eb1a5ef844a8dbf94cbde9d2c99986ce0634260
ms.sourcegitcommit: 034226b5a60de49a75c7b54e856814f81c03a112
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86422795"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Configuration Manager için güncelleştirmeler ve bakım

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager **, güncelleştirmeler ve bakım**adlı konsol içi bir hizmet yöntemi kullanır. Bu konsol içi yöntemi, Configuration Manager altyapınız için önerilen güncelleştirmeleri bulmayı ve yüklemeyi kolaylaştırır. Konsol içi hizmet verme, düzeltmeler gibi bant dışı güncelleştirmeler tarafından kullanıma alınmıştır. Bant dışı güncelleştirmeler, ortamlarına özgü olabilecek sorunları çözmesi gereken müşterilere yöneliktir.  

> [!TIP]  
> *Yükseltme*, güncelleştirme ve *güncelleştirme*terimleri, Configuration Manager üç ayrı kavramı *tanımlamakta kullanılır.* Her bir terimin nasıl kullanıldığı hakkında daha fazla bilgi için bkz. [Upgrade, Update ve Install hakkında](../../understand/upgrade-update-install.md).  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Temel ve güncelleştirme sürümleri  

Yeni bir hiyerarşiye yeni bir site yüklerken en güncel temel sürümü kullanın.

- Ayrıca, System Center 2012 Configuration Manager yükseltmek için bir temel sürümü kullanın.  

- Güncel dala Configuration Manager yükseltme yaptıktan sonra, geçerli kalmak için temel sürümlerini kullanmayın. Bunun yerine, yalnızca en yeni sürüme güncelleştirmek için [konsol içi güncelleştirmeleri](install-in-console-updates.md) kullanın.  

- Düzenli olarak, ek temel sürümler yayımlanır. Yeni bir hiyerarşi yüklemek için en son temel sürümü kullandığınızda, güncel olmayan veya desteklenmeyen bir Configuration Manager sürümünü yüklemeden sonra altyapınızı güncel hale getirmek için altyapınızın ek bir yükseltmesini kullanmaktan kaçının.  

Temel sürüm yüklendikten sonra, ek Configuration Manager sürümleri konsol içi güncelleştirmeler olarak kullanılabilir. Konsol içi güncelleştirmeler, altyapınızı en güncel Configuration Manager sürümüne güncelleştirir.  

- En üst düzey sitenizin sürümünü güncelleştirmek için konsol içi güncelleştirmeleri yüklersiniz.  

- Merkezi yönetim sitesinde yüklediğiniz güncelleştirmeler alt birincil sitelerde otomatik olarak yüklenir. Birincil sitede bir bakım penceresi kullanarak bu zamanlamayı denetleyin.  

- İkincil siteleri konsolunun içinden yeni bir güncelleştirme sürümüne el ile güncelleştirin.  

Güncelleştirme yüklediğinizde güncelleştirme, site sunucusundaki bu sürüm için yükleme dosyalarını CD adlı bir klasörde depolar **. En son**. Bu dosyalar hakkında daha fazla bilgi için [CD 'ye bakın. En son klasör](the-cd.latest-folder.md).  

- CD 'deki dosyaları kullanın. Site Recovery sırasında en son klasör. Ayrıca, hiyerarşiniz artık temel bir sürümü çalıştırmadıysa ek siteleri yüklemek için bu dosyaları kullanın.  

- CD 'den yükleme dosyalarını kullanamazsınız. Yeni bir hiyerarşinin ilk sitesini yüklemek veya bir siteyi System Center 2012 Configuration Manager yükseltmek için en son.  

### <a name="version-details"></a>Sürüm ayrıntıları

Bazı Configuration Manager güncelleştirmeleri hem mevcut altyapıya ait konsol içi güncelleştirme sürümü hem de yeni bir temel sürüm olarak sunulur.  

#### <a name="supported-versions"></a>Desteklenen sürümler

Aşağıdaki desteklenen Configuration Manager sürümleri temel, bir güncelleştirme veya her ikisi olarak sunulmaktadır:  

| Sürüm | Kullanılabilirlik tarihi | [Destek bitiş tarihi](current-branch-versions-supported.md) | Taban çizgisi | Konsol içi güncelleştirme |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | 1 Nisan 2020 | 1 Ekim 2021 | Evet<sup>[1](#bkmk_note1)</sup> | Evet |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 29 Kasım 2019 | 29 Mayıs 2021 | Hayır | Evet |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 26 Temmuz 2019 | 26 Ocak 2021 | Hayır | Evet |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 27 Mart 2019 | 27 Eylül 2020 | Evet | Yes |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 27 Kasım 2018 | 1 Aralık 2020 | Hayır | Evet |

**Kullanılabilirlik tarihi** , [erken güncelleştirme halkasının](checklist-for-installing-update-2002.md#early-update-ring) Yayınlanma tarihidir. Güncelleştirme genel kullanıma alındıktan sonra toplu lisans hizmet merkezi 'nde temel medya kullanılabilir olacaktır.

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**1. nota:**</sup> Temel medya, [Toplu Lisans Hizmet Merkezi](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) üzerinde aşağıdaki sürümlerin bir parçası olarak kullanılabilir:
>
> - Microsoft uç nokta ConfigMgr (geçerli dal)
> - System Center veri merkezi
> - System Center Standart  
>
> Örneğin VLSC 'de için arama yapın `Microsoft Endpoint Configmgr (current branch)` . Dosya listesindeki temel medyayı bulun ve bu sürüm için indirin.  

#### <a name="historical-versions"></a>Geçmiş sürümler

Aşağıdaki tabloda, güncel dalın Configuration Manager geçmiş sürümleri listelenmekte.

| Sürüm | Kullanılabilirlik tarihi | Destek bitiş tarihi | Taban çizgisi | Konsol içi güncelleştirme |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 31 Temmuz 2018 | 31 Ocak 2020 | Hayır | Evet |
| **1802** <br /> (5.00.8634) | 22 Mart 2018 | 22 Eylül 2019 | Evet | Yes |
| **1710** <br /> (5.00.8577) | 20 Kasım 2017 | 20 Mayıs 2019 | Hayır | Evet |
| **1706** <br /> (5.00.8540) | 31 Temmuz 2017 | 31 Temmuz 2018 | Hayır | Evet |
| **1702** <br /> (5.00.8498) | 27 Mart 2017 | 27 Mart 2018 | Yes | Yes |
| **1610** <br /> (5.00.8458) | 18 Kasım 2016 | 18 Kasım 2017 | Hayır | Evet |
| **1606** <br /> (5.00.8412.1000) | 22 Temmuz 2016 | 22 Temmuz 2017 | Hayır | Evet |
| **KB3186654 ile 1606** <br />5.00.8412.1307) | 12 Ekim 2016 | 12 Ekim 2017 | Evet | Hayır |
| **1602** <br /> (5.00.8355) | 11 Mart 2016 | 11 Mart 2017 | Hayır | Evet |
| **1511** <br /> (5.00.8325) | 8 Aralık 2015 | 8 Aralık 2016 | Evet | Hayır |  

#### <a name="how-to-check-the-version"></a>Sürümü denetleme

Configuration Manager sitenizin sürümünü denetlemek için konsolun sol üst köşesindeki **Configuration Manager hakkında** bölümüne gidin. Bu iletişim kutusu, site ve konsol sürümlerini görüntüler.  

> [!Note]  
> Konsol sürümü, site sürümünden biraz farklıdır. Konsolun ikincil sürümü Configuration Manager yayın sürümüne karşılık gelir. Örneğin, Configuration Manager sürüm 1802 ' de ilk site sürümü 5.0.8634.1000 ve ilk konsol sürümü 5 ' tir. **1802**. 1082,1700. Derleme (1082) ve düzeltme (1700) numaraları gelecekteki düzeltmelerle birlikte değişebilir.

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Konsol içi güncelleştirmeler ve bakım  

Configuration Manager geçerli dalı için üretime hazır bir yükleme kullandığınızda, çoğu güncelleştirme, **güncelleştirmeler ve bakım** kanalı kullanılarak kullanılabilir. Bu yöntem, geçerli altyapı sürümünüz ve yapılandırmanız için geçerli olan güncelleştirmeleri tanımlar, indirir ve kullanıma sunar. Yalnızca Microsoft 'un tüm müşterilerine önerdiği güncelleştirmeleri içerir.

Bu güncelleştirmeler şunlardır:  

- Sürüm 1906, 1910 veya 2002 gibi yeni sürümler.

- Güncel sürümünüz için yeni özellikler içeren güncelleştirmeler.

- Configuration Manager sürümünüze yönelik düzeltmeler ve tüm müşterilerin yüklenmesi gerekir.

    > [!Note]  
    > Sürüm 1902 ' den başlayarak, konsol içi düzeltmelerde yenisiyle değiştirme ilişkileri vardır. Daha fazla bilgi için bkz. [konsol içi düzeltmelere yönelik değiştirme](#bkmk_supersede).

Konsol içi güncelleştirmeler daha iyi kararlılık sunarak sık karşılaşılan sorunları giderir. Hizmet paketleri, toplu güncelleştirmeler, tüm müşteriler için geçerli olan düzeltmeler ve Microsoft Intune Uzantısı gibi önceki ürün sürümleri için görülen güncelleştirme türlerini değiştirir.

Konsol içi güncelleştirmeler aşağıdaki sistemlerin bir veya daha fazlasına uygulanabilir:  

- Birincil ve merkezi yönetim sitesi sunucuları  

- Site sistemi rolleri ve site sistemi sunucuları  

- SMS Sağlayıcısı örnekleri  

- Configuration Manager konsolları  

- Configuration Manager istemcileri  

Configuration Manager, yeni güncelleştirmeleri sizin için bulur. Aşağıdaki davranışları belirterek Configuration Manager hizmet bağlantı noktanızı Microsoft bulut hizmeti ile eşitler:  

- Hizmet bağlantı noktanız çevrimiçi modda olduğunda, siteniz her gün Microsoft ile eşitlenir. Altyapınız için uygulanan yeni güncelleştirmeleri otomatik olarak belirler. Güncelleştirmeleri ve yeniden dağıtılabilir dosyaları indirmek için, hizmet bağlantı noktası site sistem rolünü barındıran bilgisayar şu internet konumlarına erişmek için **sistem** bağlamını kullanır: go.microsoft.com ve download.Microsoft.com. Hizmet bağlantı noktası tarafından kullanılan ek konumlar hakkında daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../deploy/configure/about-the-service-connection-point.md#bkmk_urls).  

- Hizmet bağlantı noktanız çevrimdışı modda olduğunda, Microsoft bulutuyla el ile eşitleme yapmak için hizmet bağlantı aracını kullanın. Daha fazla bilgi için bkz. [hizmet bağlantı aracını kullanma](use-the-service-connection-tool.md).  

- Konsol içi güncelleştirmeler sayesinde güncelleştirmeleri, hizmet paketlerini ve yeni özellikleri ayrı ayrı bulmanıza ve yüklemenize gerek kalmaz.  

- Yalnızca seçtiğiniz konsol içi güncelleştirmeleri yükler. Bazı güncelleştirmeleri yüklerken etkinleştirmek ve kullanmak için tek tek özellikleri seçebilirsiniz. Daha fazla bilgi için, bkz. [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

Konsol içi bir güncelleştirme yüklediğinizde aşağıdaki işlem gerçekleşir:  

- Otomatik olarak bir önkoşul denetimi çalıştırılır. Yüklemeyi başlatmadan önce bu denetimi el ile de çalıştırabilirsiniz.  

- Ortamınızdaki en üst düzey siteye yüklenir. Bu site, varsa merkezi yönetim sitesidir. Hiyerarşide güncelleştirme, birincil sitelere otomatik olarak yüklenir. [Site sunucuları Için hizmet pencerelerini](service-windows.md)kullanarak her bir birincil site sunucusunun güncelleştirmesine izin verildiğinde denetim.  

- Bir site sunucusu güncelleştirildikten sonra, etkilenen tüm site sistem rolleri otomatik olarak güncelleştirilir. Bu roller SMS sağlayıcısının örneklerini içerir. Site güncelleştirmeyi yükledikten sonra, Configuration Manager konsolları konsol kullanıcısına konsolu güncelleştirmesini de ister.  

- Bir güncelleştirme Configuration Manager istemcisini içeriyorsa, güncelleştirmeyi ön üretim aşamasında test etme veya tüm istemcilere hemen uygulama seçenekleri sunulur.  

- Birincil site güncelleştirildikten sonra ikincil siteler otomatik olarak güncelleştirmez. Bunun yerine, ikincil site güncelleştirmesini el ile başlatmanız gerekir.  

> [!NOTE]  
> Configuration Manager geçerli dal, uzun süreli bakım dalı ve Technical Preview dalı farklı sürümlerdir. Bir dal için uygulanan güncelleştirmeler, diğer dallar için konsol içi güncelleştirmeler olarak kullanılamaz. Kullanılabilir dallar hakkında daha fazla bilgi için, [hangi Configuration Manager dalını kullanmalıyım?](../../understand/which-branch-should-i-use.md)bölümüne bakın.

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a>Konsol içi düzeltmelerde yerine geçme

<!-- 3229613 -->
Sürüm 1902 ' den başlayarak, konsol içi düzeltmelerde yenisiyle değiştirme ilişkileri vardır. Microsoft yeni bir Configuration Manager düzeltmesi yayımladığında, konsol bu yeni düzeltmenin yerini aldığı düzeltmeleri göstermez. Bu yeni davranış, hangi düzeltmelerin yükleneceğini daha iyi bir şekilde belirlemenizi sağlar.

### <a name="supersedence-example"></a>Yenisiyle değiştirme örneği

Kullanılabilecek üç düzeltme vardır: düzeltme-A, düzeltme-B ve düzeltme-C. Düzeltme-B düzeltmesinin yerini almıştır ve düzeltme-B 'nin yerini düzeltme-C almıştır.

|Düzeltme-A|Düzeltme-B|Düzeltme-C|Konsol içi görünüm|
|--------|--------|--------|---------------|
|Yüklü değil|Yüklü değil|Yüklü değil|Üç düzeltmeyi de göster|
|Yüklendi|Yüklendi|Yüklü değil|Düzeltme-B yüklü olarak gösteriliyor<br/>Düzeltme-C, yüklenmeye hazırlanma olarak gösteriliyor|
|Yüklü değil|Yüklü değil|Yüklendi|Düzeltme-C yüklü olarak gösteriliyor|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Bant dışı düzeltmeler  

Bazı düzeltmeler, belirli sorunları gidermek için sınırlı kullanılabilirliğe sahip bir sürümdür. Diğer düzeltmeler tüm müşteriler için geçerlidir, ancak konsol içi yöntemi kullanılarak yüklenemez. Bu düzeltmeler bant dışı sunulur ve Microsoft bulut hizmetiyle bulunmaz.  

Genellikle, Configuration Manager dağıtımıyla ilgili bir sorunu gidermeye veya gidermeye çalışırken, Microsoft Müşteri Destek Hizmetleri, Microsoft Destek Bilgi Bankası makalesi veya [Configuration Manager ekip blogundan](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog)bant dışı düzeltmeler hakkında bilgi edinebilirsiniz.

Aşağıdaki iki yöntemden birini kullanarak bu düzeltmeleri el ile yükleyebilirsiniz:  

### <a name="update-registration-tool"></a>Güncelleştirme kayıt aracı

Bu araç, düzeltmeyi Configuration Manager konsoluna el ile içeri aktarır. Ardından, otomatik olarak bulunan konsol içi güncelleştirmelere yaptığınız gibi güncelleştirmeyi yükleyebilirsiniz.  

Bu yöntem, aşağıdaki dosya adı yapısını kullanan düzeltmeler için kullanılır:  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

Daha fazla bilgi için bkz. [düzeltmeleri içeri aktarmak için güncelleştirme kayıt aracını kullanma](use-the-update-registration-tool-to-import-hotfixes.md).  

### <a name="hotfix-installer"></a>Düzeltme yükleyicisi

Konsol içi yöntemi kullanılarak yüklenebilen bir düzeltmeyi el ile yüklemek için bu aracı kullanın.  

Bu yöntem, aşağıdaki dosya adı yapısını kullanan düzeltmeler için kullanılır:  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Daha fazla bilgi için bkz. [güncelleştirmeleri yüklemek için düzeltme yükleyicisini kullanma](use-the-hotfix-installer-to-install-updates.md).  

## <a name="next-steps"></a>Sonraki adımlar

Aşağıdaki makaleler Configuration Manager için farklı güncelleştirme türlerini bulmayı ve yüklemeyi anlamanıza yardımcı olabilir:  

- [Konsol güncelleştirmelerini yükleyin](install-in-console-updates.md)  

- [Hizmet bağlantısı aracını kullanma](use-the-service-connection-tool.md)  

- [Düzeltmeleri içeri aktarmak için güncelleştirme kayıt aracı 'nı kullanma](use-the-update-registration-tool-to-import-hotfixes.md)  

- [Güncelleştirmeleri yüklemek için düzeltme yükleyicisini kullanma](use-the-hotfix-installer-to-install-updates.md)  

Technical Preview dalı hakkında daha fazla bilgi için bkz. [Technical Preview](../../get-started/technical-preview.md).
