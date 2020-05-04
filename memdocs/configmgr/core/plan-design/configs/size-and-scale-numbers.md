---
title: Boyut ve ölçek
titleSuffix: Configuration Manager
description: Ortamınızdaki cihazları desteklemek için ihtiyacınız olan site sistemi rollerinin ve sitelerinin sayısını belirleme.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0861bb73769beb6c7595b896afc8d0e156eef94d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709645"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Configuration Manager için boyut ve ölçek numaraları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Her Configuration Manager dağıtımında en fazla sayıda site, site sistem rolü ve destekleyebileceği cihaz vardır. Bu sayılar, hiyerarşi yapısına, hangi tür ve kullandığınız sitelere ve dağıttığınız site sistem rollerine bağlı olarak farklılık gösterir. Bu makaledeki bilgiler, yönetmek istediğiniz cihazları desteklemek için ihtiyacınız olan site sistemi rollerinin ve sitelerinin sayısını belirlemenize yardımcı olabilir.

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Önerilen donanım](recommended-hardware.md)
- [Site sistem sunucuları için desteklenen işletim sistemleri](supported-operating-systems-for-site-system-servers.md)  
- [İstemciler ve cihazlar için desteklenen işletim sistemleri](supported-operating-systems-for-clients-and-devices.md)
- [Site ve site sistemi önkoşulları](site-and-site-system-prerequisites.md)

Bu destek numaraları Configuration Manager için önerilen donanımın kullanımına dayanır. Bunlar, tüm kullanılabilir Configuration Manager özellikleri için varsayılan ayarları da temel alır. Önerilen donanımı kullanmazsanız veya daha Agresif özel ayarlar kullandığınızda, site sistemlerinin performansı düşebilir. Site sistemleri, belirtilen destek düzeylerini karşılayamayabilir. (Daha fazla agresif istemci ayarlarına bir örnek, her yedi günde bir kez varsayılan olarak donanım veya yazılım envanterinden daha sık çalışır.)

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a>Site türleri  

### <a name="central-administration-site"></a>Merkezi yönetim sitesi  

- Bir merkezi yönetim sitesi en fazla 25 alt birincil siteyi destekler.  

### <a name="primary-site"></a>Birincil site  

- Her birincil site en fazla 250 ikincil siteyi destekler.  

- Birincil site başına ikincil sitelerin sayısı, sürekli olarak bağlanan ve güvenilir geniş alan ağı (WAN) bağlantılarına dayanır. 500 ' den az istemcisi olan konumlar için, ikincil bir site yerine bir dağıtım noktası düşünün.  

  Birincil bir sitenin destekleyebileceği Istemci ve cihaz sayısı hakkında daha fazla bilgi için bkz. [siteler ve Hiyerarşiler Için istemci numaraları](#bkmk_clientnumbers).  

### <a name="secondary-site"></a>İkincil site  

- İkincil siteler alt siteleri desteklemez.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Site sistemi rolleri

### <a name="application-catalog-web-service-point"></a>Uygulama Kataloğu Web hizmet noktası  

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- Birincil sitelerde Uygulama Kataloğu Web hizmeti noktasının birden fazla örneğini yükleyebilirsiniz.  

### <a name="application-catalog-website-point"></a>Uygulama Kataloğu web sitesi noktası  

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- Birincil sitelerde Uygulama Kataloğu web sitesi noktasının birden fazla örneğini yükleyebilirsiniz.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a>Bulut yönetimi ağ geçidi

- Birincil sitelerde veya merkezi yönetim sitesinde bulut yönetimi ağ geçidinin (CMG) birden çok örneğini yükleyebilirsiniz.  

    > [!Tip]  
    > Hiyerarşide, merkezi yönetim sitesinde CMG 'yi oluşturun.  

  - Bir CMG, Azure bulut hizmetindeki 16 ' dan fazla sanal makine (VM) örneğini destekler.  

  - Her CMG VM örneği, 6.000 eşzamanlı istemci bağlantısını destekler. Desteklenen sayıda istemciden daha fazla istemci olması nedeniyle CMG yüksek yük altında olduğunda, hala istekleri işler, ancak gecikme olabilir.  

Daha fazla bilgi için bkz. CMG [performansı ve ölçeği](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale)

### <a name="cloud-management-gateway-connection-point"></a>Bulut yönetimi ağ geçidi bağlantı noktası

- Birincil sitelerde CMG bağlantı noktasının birden fazla örneğini yükleyebilirsiniz.  

- Bir CMG bağlantı noktası, en fazla dört VM örneğiyle CMG 'yi destekleyebilir. CMG 'nin dörtten fazla VM örneği varsa yük dengeleme için ikinci bir CMG bağlantı noktası ekleyin. 16 VM örneğiyle CMG, dört CMG bağlantı noktasıyla bağlanmalıdır.

Daha fazla bilgi için bkz. CMG [performansı ve ölçeği](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale)

> [!NOTE]
> CMG bağlantı noktası için donanım gereksinimlerini değerlendirirken, [uzak site sistemi sunucuları Için önerilen donanım](recommended-hardware.md#bkmk_RemoteSiteSystem)bölümüne bakın.<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Dağıtım noktası  

- Site başına dağıtım noktaları:  

  - Her birincil ve ikincil site en fazla 250 dağıtım noktasını destekler.  

  - Her birincil ve ikincil site, çekme dağıtım noktası olarak yapılandırılmış en fazla 2000 ek dağıtım noktasını destekler. **Örneğin**, tek bir birincil site, bu dağıtım noktalarının 2000, çekme dağıtım noktası olarak yapılandırıldığında 2250 dağıtım noktasını destekler.  

  - Her dağıtım noktası 4.000 istemciden fazla bağlantıyı destekler.  

  - İstek temelli dağıtım noktası, kaynak dağıtım noktasından içerik eriştiğinde istemci gibi davranır.  

- Her birincil site toplam 5.000 dağıtım noktasını destekler. Bu toplam, birincil sitedeki tüm dağıtım noktalarını ve birincil sitenin alt ikincil sitelerine ait olan tüm dağıtım noktalarını içerir.  

- Her dağıtım noktası toplam 10.000 paketi ve uygulamayı destekler.  

> [!WARNING]  
> Bir dağıtım noktasının destekleyebileceği gerçek istemci sayısı, ağın hızına ve sunucunun donanım yapılandırmasına bağlıdır.  
>
> Tek bir kaynak dağıtım noktasının destekleyebileceği çekme dağıtım noktası sayısı, ağın hızına ve kaynak dağıtım noktasının donanım yapılandırmasına bağlıdır. Ancak bu sayı, dağıttığınız içerik miktarından da etkilenir. Bu efekt, bir dağıtım sırasında genellikle içeriğe farklı zamanlarda erişen istemcilerin aksine, tüm çekme dağıtım noktalarının içeriği aynı anda istemesi nedeniyle oluşur. Çekme dağıtım noktaları, yalnızca kendileri için geçerli olan içeriği değil, tüm kullanılabilir içeriği talep edebilir. Kaynak dağıtım noktasına yüksek bir işlem yükü yerleştirdiğinizde, içeriği hedef dağıtım noktalarına dağıtırken beklenmedik gecikmeler olabilir.  

### <a name="fallback-status-point"></a>Geri dönüş durumu noktası  

- Her geri dönüş durum noktası, en fazla 100.000 istemciyi destekleyebilir.  

### <a name="management-point"></a>Yönetim noktası  

- Her birincil site en fazla 15 yönetim noktasını destekler.  

    > [!TIP]  
    > Yönetim noktalarını, birincil site sunucusu veya site veritabanı sunucusundan yavaş bir bağlantıda bulunan sunuculara yüklemeyin.  

- Her ikincil site, ikincil site sunucusuna yüklenmesi gereken tek bir yönetim noktasını destekler.  

Bir yönetim noktasının destekleyebileceği istemci ve cihaz sayısı hakkında daha fazla bilgi için [Yönetim noktaları](#bkmk_mp) bölümüne bakın.  

### <a name="software-update-point"></a>Yazılım güncelleştirme noktası  

Aşağıdaki önerileri temel olarak kullanın. Bu taban çizgisi, kuruluşunuza uygun yazılım güncelleştirmeleri kapasite planlaması bilgilerini belirlemenize yardımcı olur. Gerçek kapasite gereksinimleri, aşağıdaki kriterlere bağlı olarak, bu makalede listelenen önerilerden farklı olabilir:

- Belirli ağ ortamınız
- Yazılım güncelleştirme noktası site sistemini barındırmak için kullandığınız donanım
- Yönetilen istemci sayısı
- Sunucuda yüklü olan diğer site sistem rolleri  

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Yazılım güncelleştirme noktası için kapasite planlaması  

Desteklenen istemci sayısı, yazılım güncelleştirme noktasında çalıştırılan Windows Server Update Services (WSUS) sürümüne bağlıdır. Ayrıca, yazılım güncelleştirme noktası site sistem rolünün başka bir site sistem rolüyle birlikte var olup olmamasına bağlıdır:  

- Yazılım güncelleştirme noktası, WSUS yazılım güncelleştirme noktası sunucusunda çalıştırıldığında 25.000 adede kadar istemciyi destekleyebilir ve yazılım güncelleştirme noktası, başka bir site sistem rolüyle birlikte bulunur.  

- Yazılım güncelleştirme noktası, bir uzak sunucu WSUS gereksinimlerini karşıladığında, WSUS Configuration Manager ile kullanıldığında ve aşağıdaki ayarları yapılandırdığınızda 150.000 adede kadar istemciyi destekleyebilir:

  IIS uygulama havuzları:

  - WsusPool Kuyruk Uzunluğu’nu 2000’e çıkarın
  - WsusPool özel bellek sınırını x4 kez artırın veya 0 (sınırsız) olarak ayarlayın. Örneğin, varsayılan sınır 1.843.200 KB ise, bunu 7.372.800 ' e yükseltin. Daha fazla bilgi için bu [Configuration Manager Destek ekibi blog gönderisine](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/)bakın.  

    Yazılım güncelleştirme noktası için donanım gereksinimleri hakkında daha fazla bilgi için bkz. [site sistemleri Için önerilen donanım](recommended-hardware.md#bkmk_ScaleSieSystems).  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a>Yazılım güncelleştirmeleri nesneleri için kapasite planlaması  

Yazılım güncelleştirme nesnelerini planlamak için aşağıdaki kapasite bilgilerini kullanın:  

- **Bir dağıtımda 1000 yazılım güncelleştirmesi sınırı** -her yazılım güncelleştirme dağıtımı için yazılım güncelleştirme sayısını 1000 olarak sınırlandırın. Bir otomatik dağıtım kuralı (ADR) oluşturduğunuzda, yazılım güncelleştirme sayısını sınırlayan ölçütleri belirtin. Belirtilen ölçüt 1000 ' den fazla yazılım güncelleştirmesi döndürdüğünde ADR başarısız olur. Configuration Manager konsolundaki **Otomatik dağıtım kuralları** düğümünden ADR 'nin durumunu denetleyin. Yazılım güncelleştirmelerini el ile dağıttığınızda, dağıtılacak 1000 ' den fazla güncelleştirme seçmeyin.  

  Ayrıca, bir yapılandırma temelindeki yazılım güncelleştirme sayısını 1000 olarak sınırlandırın. Daha fazla bilgi için bkz. [yapılandırma temelleri oluşturma](../../../compliance/deploy-use/create-configuration-baselines.md).

- **Otomatik dağıtım kuralları için 580 güvenlik kapsamının limiti** -<!--ado 4962928-->
Otomatik dağıtım kurallarında (ADRs) güvenlik kapsamlarının sayısını 580 ' den az olacak şekilde sınırlayın. ADR oluşturduğunuzda, erişimi olan güvenlik kapsamları otomatik olarak eklenir. 580 'den fazla güvenlik kapsamı ayarlandıysa, ADR çalıştırılamaz ve RuleEngine. log dosyasına bir hata kaydedilir.

### <a name="sms-provider"></a>site veritabanı

<!-- SCCMDocs#1958 -->

Her SMS sağlayıcısı örneği, birden çok istekten eş zamanlı bağlantıları destekler. Bu bağlantılardaki tek sınırlamalar, Windows için kullanılabilen sunucu bağlantısı sayısı ve bağlantı isteklerine hizmet vermek için sunucudaki kullanılabilir kaynaklardır.

Daha fazla bilgi için bkz. [plan for SMS Provider](../hierarchy/plan-for-the-sms-provider.md).

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a>Siteler ve Hiyerarşiler için istemci numaraları

Bir sitede veya hiyerarşide kaç tane istemci ve hangi tür istemci destekleyeceğini öğrenmek için aşağıdaki bilgileri kullanın.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a>Merkezi Yönetim sitesi olan hiyerarşi

Bir merkezi yönetim sitesi, aşağıdaki üç grup için listelenen cihaz sayısını içeren toplam cihaz sayısını destekler:  

- 700.000 Windows masaüstü bilgisayarları. Ayrıca bkz. [Katıştırılmış cihazlar](#embedded)için destek.

- Mac ve Windows CE 7,0 çalıştıran 25.000 cihazları  

- Şirket içi mobil cihaz yönetimi (MDM) kullanarak yönettiğiniz 100.000 cihaz

Örneğin, bir hiyerarşide 700.000 masaüstü bilgisayar, 25.000 ' e kadar Mac ve Windows CE 7,0 cihazlara ve şirket içi MDM tarafından yönetilen en fazla 100.000 cihaza destek sağlayabilirsiniz. Bu hiyerarşi, toplam 825.000 cihazı destekler.

> [!IMPORTANT]  
> Merkezi yönetim sitesinin SQL Server Standart bir sürümünü kullandığı hiyerarşide hiyerarşi, en fazla 50.000 masaüstü ve cihazı destekler. 50.000 ' den fazla masaüstü ve cihazı desteklemek için SQL Server Enterprise sürümünü kullanmanız gerekir. Bu gereksinim yalnızca bir merkezi yönetim sitesi için geçerlidir. Tek başına birincil site veya bir alt birincil site için uygulanmaz. Birincil site için kullandığınız SQL Server sürümü, belirtilen sayıda istemciyi destekleyecek kapasitesini sınırlandırmaz.

Bağımsız bir birincil sitede kullanımda olan SQL Server sürümü, belirtilen sayıda istemciyi desteklemek için o sitenin kapasitesini sınırlandırmaz.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a>Alt birincil site

Bir merkezi yönetim sitesi içeren bir hiyerarşideki her alt birincil site, aşağıdaki sayıda istemciyi destekler:  

- 150.000, destek hiyerarşisi için desteklenen sayıyı aşmadığı sürece belirli bir grup veya türle sınırlı olmayan toplam istemci ve cihaz. Ayrıca bkz. [Katıştırılmış cihazlar](#embedded)için destek.

Örneğin, bir birincil site 25.000 Mac ve Windows CE 7,0 cihazlarını destekler. Bu sayı, bir hiyerarşinin limiti olur. Bu birincil site daha sonra, ek 125.000 masaüstü bilgisayarları destekleyebilir. Alt birincil site için desteklenen toplam cihaz sayısı, 150.000 olan en yüksek limit sayısıdır.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a>Tek başına birincil site

Tek başına birincil site aşağıdaki sayıda cihazı destekler:  

- Toplam 175.000 istemci ve cihaz, aşmamak için:  

  - 150.000 masaüstü bilgisayar (Windows, Linux ve UNIX çalıştıran bilgisayarlar). Ayrıca bkz. [Katıştırılmış cihazlar](#embedded)için destek.

  - Mac ve Windows CE 7,0 çalıştıran 25.000 cihazları

  - Şirket içi MDM kullanarak yönettiğiniz 50.000 cihaz  

Örneğin, 150.000 masaüstü bilgisayarları ve 10.000 Mac 'i destekleyen bağımsız bir birincil site yalnızca şirket içi MDM tarafından yönetilen ek 15.000 mobil cihazları destekleyebilir.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a>Birincil siteler ve Windows Embedded cihazları

Birincil siteler dosya tabanlı yazma filtreleri (FBWF) etkin Windows Embedded cihazlarını destekler. Katıştırılmış cihazlarda yazma filtreleri etkin olmadığında, birincil site, bu site için izin verilen sayıda cihaza kadar eklenmiş olan cihazları destekleyebilir. Katıştırılmış cihazlarda FBWF veya Birleşik yazma filtreleri (UWF) etkin olduğunda, birincil site en fazla 10.000 Windows Embedded cihazını destekleyebilir. Bu cihazların [Windows Embedded cihazlarına istemci dağıtımını planlama](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)bölümünde bulunan önemli notta listelenen özel durumlarla yapılandırılması gerekir. Birincil bir site yalnızca EWF 'nin etkinleştirildiği ve özel durumlar için yapılandırılmayan 3.000 Windows katıştırılmış cihazlarını destekler.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a>İkincil siteler

İkincil siteler aşağıdaki sayıda cihazı destekler:  

- 15.000 masaüstü bilgisayar (Windows, Linux ve UNIX çalıştıran bilgisayarlar)  

### <a name="management-points"></a><a name="bkmk_mp"></a>Yönetim noktaları

Her yönetim noktası aşağıdaki sayıda cihazı destekleyebilir:  

- Toplam 25.000 istemci ve cihaz, aşmamak için:  

  - 25.000 masaüstü bilgisayar (Windows, Linux ve UNIX çalıştıran bilgisayarlar)  

  - Aşağıdakilerden biri (her ikisi değil):  

    - Şirket içi MDM kullanılarak yönetilen 10.000 cihaz  

    - Mac ve Windows CE 7,0 istemcileri çalıştıran 10.000 cihaz
