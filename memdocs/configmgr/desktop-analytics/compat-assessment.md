---
title: Uyumluluk değerlendirmesi
titleSuffix: Configuration Manager
description: Masaüstü Analizi 'nde Windows Uygulamaları ve sürücüleri için uyumluluk değerlendirmesi hakkında bilgi edinin.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7b2bff4f8365693c86540c9b0578307340f13a49
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268904"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Masaüstü Analizi 'nde uyumluluk değerlendirmesi

Önceki çözümlerdeki yükseltme değerlendirmeleri geneldir, örneğin: Ilgilenilmesi gereken veya düzeltilmesi gereken. Sorunları veya yükseltme öngörülerini kullanarak uygulamaların veya sürücülerin önceliklerini belirleme konusunda hiçbir görsel gösterge sağlamaz. Masaüstü analizi, bu özelliğin yerini **Uyumluluk riskidir**. Masaüstü analizi, yalnızca yükseltme öncesi senaryonun dağıtım görünümündeki uygulamalar için değerlendirmeyi gösterir. Microsoft, geçerli bir dağıtım planına dahil olan makinelerime dayanarak uygulamaları kategorilere ayırır.

Masaüstü Analizi aşağıdaki uyumluluk değerlendirmesi kategorilerini kullanır:

- **Düşük**: hizmet, bir Windows yükseltmesi için bu uygulamayı riske almak üzere hiçbir sinyal bulamadı. Hedef işletim sistemi üzerinde olduğu gibi çalışıyor olma olasılığı yüksektir.

- **Orta**: analiz, uygulamanın Engelli işlevlere sahip olabileceğini gösterir, ancak düzeltme olasıdır.

- **Yüksek**: uygulama, yükseltme sırasında veya sonrasında başarısız olarak neredeyse belli olur. Düzeltilmesi gerekebilir.

- **Bilinmiyor**: uygulama değerlendirilmedi. *MS bilinen sorunlar* veya *Windows için hazırlanma*gibi başka Öngörüler bulunmamaktadır.

Dağıtım planındaki uygulama veya sürücü varlıkları listesinde, **uyumluluk riski** sütunundaki her bir varlık için bu değeri görürsünüz.

## <a name="app-risk-assessment"></a>Uygulama risk değerlendirmesi

![Uygulama risk değerlendirmesi kaynakları diyagramı](media/app-risk-assessment-sources.png)

Masaüstü analizinin uygulamalar için değerlendirme derecelendirmesi oluşturmak üzere kullandığı birkaç kaynak vardır:

- [Microsoft 'un bilinen sorunları](#microsoft-known-issues)
- [Windows için hazırlanıyor](#ready-for-windows)
- [Gelişmiş Öngörüler](#advanced-insights)

Uygulama üzerinde her bir kaynağın değerlendirmesini, masaüstü Analizi ' nde bulabilirsiniz. Bir dağıtım planındaki uygulama varlıkları listesinde, tek bir uygulamayı seçerek Özellikler açılan penceresini açın. Genel bir öneri ve değerlendirme düzeyi görürsünüz. **Uyumluluk riski faktörleri** bölümünde, bu değerlendirmelerin ayrıntıları gösterilmektedir.

> [!TIP]
> Uygulama ayrıntıları bölmesinde uyumluluk değerlendirmesi gösterilmezse, bunun nedeni **uygulama sürümleri ayrıntıları** ayarının kapalı olması olabilir. Varsayılan olarak kapalıdır ve tüm uygulama sürümlerini aynı ad ve yayımcı ile birleştirir. Hizmet, her sürüm için uyumluluk risk değerlendirmesi de yapar. Belirli bir uygulama sürümünün uyumluluk risk değerlendirmesini görmek için **uygulama sürümleri ayrıntılarını** etkinleştirin. Daha fazla bilgi için bkz. [varlıkları planlayın](about-deployment-plans.md#plan-assets).

## <a name="microsoft-known-issues"></a>Microsoft 'un bilinen sorunları

Masaüstü analizi, bilinen sorunlar için Microsoft uygulama uyumluluğu veritabanına bakar. Bu veritabanını, Microsoft 'un veya diğer yayımcıların genel kullanıma açık uygulamalarına yönelik mevcut uyumluluk bloklarını tespit etmek için kullanır. Bu denetim yalnızca seçtiğiniz dağıtım planına yönelik hedef işletim sistemi için geçerlidir.

Uygulama özellikleri bölmesinde, şu sorunları **MS bilinen sorunlar**olarak görürsünüz:

### <a name="asset-is-removed-during-upgrade"></a>Varlık yükseltme sırasında kaldırılır

Windows, bir uygulama veya sürücü ile ilgili uyumluluk sorunları algıladı. Varlık yeni işletim sistemi sürümüne geçirilmez. Yükseltmenin devam etmesi için herhangi bir eylem gerekmez. Uygulamanın veya sürücünün uyumlu bir sürümünü yeni işletim sistemi sürümüne yükler.

<!-- 3594545 -->
Windows, bu varlıkları kısmen veya tamamen kaldırabilir:

- Tam kaldırma: Windows kurulumu, yükseltme sırasında uygulamayı veya sürücüyü cihazdan tamamen kaldırır.
- Kısmi kaldırma: Windows kurulumu, uygulamayı veya sürücüyü cihazdan kısmen kaldırır. Windows yükseltildikten sonra el ile kaldırmanız gerekir.

Her iki durumda da, Windows 'u yükselttikten sonra, Kullanıcı uygulamayı veya sürücüyle ilişkili donanımı kullanamaz.

Bu öneriyi masaüstü Analizi portalında görmek için:

1. Bir dağıtım planında **pilot hazırlama**' yı seçin.
1. **Uygulamalar** sekmesini seçin.
1. Bir uygulama seçin ve ardından yan bölmedeki uyumluluk risk faktörlerini ve önerilerini görüntüleyin.

[![Masaüstü Analizi portalındaki varlık önerisi ekran görüntüsü](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>Yükseltme engelleniyor

Windows engelleme sorunları algıladı ve yükseltme sırasında uygulamayı kaldıramıyor. Yeni işletim sistemi sürümünde çalışmayabilir. Yükseltmeden önce uygulamayı kaldırın. Yeni işletim sistemi sürümüne yeniden yükleyin ve test edin.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Yükseltme engelleniyor, ancak yükseltmeden sonra yeniden yüklenebilir

Uygulama yeni işletim sistemi sürümü ile uyumludur, ancak geçirilmez. Windows 'ı yükseltmeden önce uygulamayı kaldırın. Yeni işletim sistemi sürümüne yeniden yükleyin.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Yükseltme engelleniyor, uygulamayı en yeni sürüme Güncelleştir

Uygulamanın mevcut sürümü yeni işletim sistemi sürümü ile uyumlu değil ve geçirilmez. Uygulamanın uyumlu bir sürümü kullanılabilir. Yükseltmeden önce uygulamayı güncelleştirin.

### <a name="disk-encryption-blocking-upgrade"></a>Disk şifrelemesini engelleme yükseltmesi

Uygulamanın şifreleme özellikleri yükseltmeyi engeller. Windows 'yi yükseltmeden önce şifreleme özelliğini devre dışı bırakın ve yükseltmeden sonra etkinleştirin.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Yeni işletim sistemi ile çalışmaz, ancak yükseltmeyi engellemez

Uygulama, yeni işletim sistemi sürümü ile uyumlu değildir, ancak yükseltmeyi engellemez. Yükseltmenin devam etmesi için herhangi bir eylem gerekmez. Uygulamanın uyumlu bir sürümünü yeni işletim sistemi sürümüne yükler.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Yeni işletim sistemi ile çalışmaz ve yükseltme engellenir

Uygulama, yeni işletim sistemi sürümü ile uyumlu değil ve yükseltmeyi engelleyecek. Yükseltmeden önce uygulamayı kaldırın. Uygulamanın uyumlu bir sürümü kullanılabilir olabilir.

### <a name="evaluate-application-on-new-os"></a>Uygulamayı yeni işletim sisteminde değerlendir

Windows, uygulamayı taşıyacaktır, ancak uygulamanın yeni işletim sistemi sürümünde performansını etkileyebilecek sorunlar algıladı. Yükseltmenin devam etmesi için herhangi bir eylem gerekmez. Uygulamayı yeni işletim sistemi sürümünde test edin.

### <a name="may-block-upgrade-test-application"></a>Yükseltmeyi engelleyebilir, uygulamayı test edebilir

Windows, yükseltmeye engel olabilecek, ancak daha fazla araştırma gerektiren sorunlar tespit etti. Yükseltme sırasında uygulamanın davranışını test edin. Yükseltmeyi engelliyorsa, ' yi yükseltmeden önce kaldırın. Sonra yeniden yükleyin ve yeni işletim sistemi sürümünü test edin.

### <a name="multiple"></a>Birden çok

Birden çok sorun uygulamayı etkiler. Windows tarafından algılanan sorunlar hakkındaki ayrıntıları görmek için **sorgu** ' yı seçin.

### <a name="reinstall-application-after-upgrading"></a>Yükseltmeden sonra uygulamayı yeniden yükle

Uygulama, yeni işletim sistemi sürümü ile uyumludur, ancak Windows 'u yükselttikten sonra yeniden yüklemeniz gerekir. Yükseltme işlemi, uygulamayı kaldırır. Yükseltmenin devam etmesi için herhangi bir eylem gerekmez. Uygulamayı yeni işletim sistemi sürümüne yeniden yükleyin.

### <a name="safeguards"></a>Düzeyde

<!-- 5746559 -->

Windows Uyumluluk verileri bazı uygulamaları ve sürücüleri bir *güvenlik önlemi*ile sınıflandırarak Windows 10 güncelleştirmesinin başarısız olmasına veya geri alınmasına neden olabilir. Windows da yükseltebilir, ancak uygulamayı veya sürücüyü kaldırır. Masaüstü Analizi artık bu korumaları önceden belirlemenize yardımcı olabilir. böylece, güncelleştirmeyi dağıtmadan önce varlığı düzeltebilirsiniz.

1. Masaüstü Analizi portalında bir dağıtım planı seçin.

1. Menüden **varlıkları planla** ' yı seçin ve **uygulamalar** sekmesine geçin.

1. Sözcüğü içeren değerleri olan öğeleri göstermek için ad sütununu filtreleyin `Safeguard` . Daha fazla bilgi görmek için sonucu seçin.

    > [!NOTE]
    > Bu giriş, cihazlarınızda yüklü olan gerçek bir uygulama değildir. Bu, ortamınızdaki uygulamaları veya sürücüleri korumaya yönelik uyumluluk etiketiyle tanımanıza yardımcı olan bir yer tutucudur.

1. Öneri bölümünde *daha fazla bilgi edinmek*için bağlantıyı seçin. Bu bağlantı, koruma etiketi ile Windows Web sitesini geçerli uygulama veya sürücü listesiyle açar.

1. Geçerli yayımlanmış listeyi ortamınızdaki varlıkların listesiyle karşılaştırın. Uyumlu bir sürüme güncelleştirerek sorunlu olabilecek uygulamaları veya sürücüleri düzeltin.

[![Masaüstü analizinden koruma uygulamasının ekran görüntüsü](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="ready-for-windows"></a>Windows için hazırlanıyor

Benimseme durumu, Microsoft ile veri paylaşan ticari cihazlardan gelen bilgileri temel alır. Durum, yazılım satıcılarından destek deyimleriyle tümleşiktir.

Masaüstü analizi, ticari cihazlarda bulunan bir varlığın her sürümü için benimseme durumu sağlar. Bu durum, tüketici cihazlarından veya veri paylaşmeyen cihazlardan veri içermez. Durum, tüm Windows 10 cihazlarında benimseme oranını temsil edemeyebilir.

Olası kategoriler şunlardır:

- **Son derece benimseme**: en az 100.000 ticari Windows 10 cihaz bu uygulamayı yükledi.

- **Benimseme**: en az 10.000 ticari Windows 10 cihaz bu uygulamayı yükledi.

- **Yetersiz veri**: çok az sayıda ticari Windows 10 cihaz, Microsoft 'un benimsemesi için bu uygulamayla ilgili bilgileri paylaşıyor.

- **Geliştiriciye başvurun**: uygulamanın bu sürümünde uyumluluk sorunları olabilir. Microsoft daha fazla bilgi edinmek için yazılım sağlayıcısına başvurmayı önerir.

- **Bilinmiyor**: Bu uygulamanın bu sürümü için kullanılabilir bilgi yok. Bilgiler, uygulamanın diğer sürümleri için kullanılabilir olabilir.

### <a name="support-statement"></a>Support bildirisi

Yazılım sağlayıcısı Windows 10 ' da bu uygulamanın bir veya daha fazla sürümünü destekliyorsa, bu bildiriyi uygulama özellikleri bölmesinde görürsünüz. Uyumluluk risk faktörleri bölümünde, **destek bildirimine**bakın.

## <a name="advanced-insights"></a>Gelişmiş Öngörüler

Ayrıca, masaüstü Analizi aşağıdaki ek öngörüleri kullanarak sorunları tespit edebilir:

### <a name="adopted-version-available"></a>Benimsenen sürümü kullanılabilir

Bu uygulamanın, diğer müşteriler tarafından çok fazla benimseyen başka bir sürümü vardır. Bu sinyal, Windows ekosistemindeki benimseme verilerini kullanır. Geçerli sürümünüzle herhangi bir yükseltme engelleyicileri varsa, bunun yerine alternatif sürümü dağıtmaya dikkat edin. Alternatif uygulama benimsenen sürümlerini bulmak için, bkz. "üretimi hazırlama" bölümünde uygulama durumu.

### <a name="driver-dependency"></a>Sürücü bağımlılığı

Uygulama bir sürücüye bağımlıdır. Masaüstü analizi, herhangi bir gerileme bulması için pilot teste yönelik uygulamayı önerir. Herhangi bir sorununuz varsa, Windows 10 ile uyumlu bir sürüm istemek için Yayımcıya başvurun.

### <a name="additional-insights"></a>Ek Öngörüler

<!-- 4021225 -->
Configuration Manager sitesini ve istemcileri 1906 sürümüne güncelleştirdiğinizde, istemciler tanılama veri düzeyi gelişmiş sınırlı olarak ayarlandığında bu ek öngörüleri de raporlar.

> [!Important]  
> Yeni Configuration Manager özelliklerinden tam olarak yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme de güncelleştirin. Bu senaryo, istemci sürümü de en son olana kadar işlevsel değildir.

#### <a name="16-bit-apps"></a>16 bit uygulamalar

Tüm 16 bit bileşenleri uygulamalardan kaldırın ve 32-bit veya 64 bit eşdeğerleriyle değiştirin. Daha fazla bilgi için bkz. [Windows Vista ve Windows Server 2008 Geliştirici hikayesi: uygulama uyumluluğu tanımlama kitabı](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\)).

Diğer seçenek, Windows 10 desteği için NT Sanal DOS makinesi 'ni (NTVDM) etkinleştirmektir.

#### <a name="requires-admin-privileges"></a>Yönetici ayrıcalıkları gerektirir

Uygulama, kullanıcının cihaza yönetici erişimine sahip olmasını gerektirir. Bu uygulamalar için yönetici izinleri gerektiren bir uygulama bildirimi kullanın. Daha fazla bilgi için bkz. [uygulama bildirimi oluşturma ve ekleme](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

Masaüstü analizi, herhangi bir gerileme bulması için pilot teste yönelik uygulamayı önerir.

#### <a name="java-dependency"></a>Java bağımlılığı

Birçok Java uygulaması ayrı olarak yüklenen Java Runtime Environment (JRE) kullanır. Eski JRE sürümleri Windows 10 ' da çalışmaya devam edeken, Oracle yalnızca en son JRE sürümlerini destekler. Daha eski bir desteklenmeyen JRE kullanmanın güvenlik açıkları olabilir. Uygulamanızın en son JRE sürümlerinde çalışıp çalışmadığınızı denetleyin.

#### <a name="not-dpi-aware"></a>DPı olmayan duyarlı

Uygulama, Windows 10 ' da Gelişmiş ekran çözünürlükleriyle ilgili sorunları gösterebilir. Yüksek DPı çözünürlükleriyle ilgili sorunlardan kaçınmak için bir uygulama bildirimi kullanın. Daha fazla bilgi için bkz. [uygulama bildirimleri](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Masaüstü analizi, herhangi bir gerileme bulması için pilot teste yönelik uygulamayı önerir.

#### <a name="silverlight-framework"></a>Silverlight çerçevesi

Microsoft, tarayıcı olmayan tabanlı uygulamaların Silverlight kullanmaz. Silverlight 5 için destek bitiş tarihi 2021 Ekim 'e yöneliktir.

En güncel web tarayıcıları Silverlight 'ı desteklemez.

| Tarayıcı | Destek |
|---------|---------|
| Google Chrome | Destek sonu: Eylül 2015 |
| Firefox | Destek sonu: Mart 2017 |
| Microsoft Edge | Eklenti yok |

Masaüstü analizi, herhangi bir gerileme bulması için pilot teste yönelik uygulamayı önerir.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

.NET Framework sürüm 1,0, Windows 10 ' da desteklenmez. Sürüm 1,1, Windows 10 ' da uyumlu değildir. Uygulama üçüncü taraf bir yayıncıya ait ise, Windows 10 ile uyumlu bir sürüm istemek için satıcıya başvurun. Aksi takdirde, .NET 'in desteklenen bir sürümünü kullanmak için uygulamayı yeniden geliştirin.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

.NET 2,0 ve 3,5 çerçeveleri Windows 10 ' da desteklenir. Windows özelliğini etkinleştirmeniz gerekebilir. Daha fazla bilgi için bkz. [Windows 10 ' da .NET Framework 3,5](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>UI erişimi

Kullanıcı Arabirimi erişimi olan uygulamalar, masaüstünde daha yüksek ayrıcalıklı pencereler için girişi yönlendirmek üzere Kullanıcı arabirimi denetim düzeylerini atlayabilir. Bu ayarı yalnızca kullanıcı arabirimi yardımcı teknoloji uygulamaları için kullanın.

Uygulamanızda erişilebilirlik özelliklerini kullanmıyorsanız, uygulama bildiriminde UI erişim bayrağını yanlış olarak ayarlayın. Daha fazla bilgi için bkz. [uygulama bildirimi oluşturma ve ekleme](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

Masaüstü analizi, herhangi bir gerileme bulması için pilot teste yönelik uygulamayı önerir.

## <a name="driver-risk-assessment"></a>Sürücü risk değerlendirmesi

Masaüstü Analizi Ayrıca, işletim sistemi sürümüne geçiş olmayacak tüm sürücülere uygunluk olarak da listeler ve gruplar.

Değerlendirme, masaüstü Analizi 'nde sürücü üzerinde bulunabilir. Bir dağıtım planındaki sürücü varlıkları listesinde, Özellikler açılan penceresini açmak için tek bir sürücü seçin. Genel bir öneri ve değerlendirme düzeyi görürsünüz. **Uyumluluk riski faktörleri** bölümünde, bu değerlendirmelerin ayrıntıları gösterilmektedir.

| Sürücü kullanılabilirliği | Eylem gerekli mi? | Anlamı | Rehber |
|---------------------|------------------|---------------|----------|
| Yerleşik olarak kullanılabilir | Hayır, yalnızca tanıma için | Uygulamanın veya sürücünün yüklü olan sürümü yeni işletim sistemi sürümüne geçirilmez. Yeni işletim sistemi sürümü ile uyumlu bir sürüm yüklü. | Yükseltmenin devam etmesi için herhangi bir eylem gerekmez. |
| Windows Update içeri aktar | Yes | Bir sürücünün Şu anda yüklü olan sürümü yeni işletim sistemi sürümüne geçirilmez. Windows Update ile uyumlu bir sürüm kullanılabilir. | Bilgisayar Windows Update güncelleştirmeleri otomatik olarak alırsa, herhangi bir eylem gerekmez. Aksi takdirde, Windows 'u yükselttikten sonra Windows Update yeni bir sürücü alın. |
| Kullanıma hazır ve Windows Update | Yes | Bir sürücünün Şu anda yüklü olan sürümü yeni işletim sistemi sürümüne geçirilmez. Yükseltme sırasında yeni bir sürücü yüklense de Windows Update yeni bir sürüm kullanılabilir. | Bilgisayar Windows Update güncelleştirmeleri otomatik olarak alırsa, herhangi bir eylem gerekmez. Aksi takdirde, Windows 'u yükselttikten sonra Windows Update yeni bir sürücü alın. |
| Satıcıyla denetle | Yes | Sürücü yeni işletim sistemi sürümüne geçirilmez ve Masaüstü Analizi uyumlu bir sürümü bulamıyor. | Bir çözüm için sürücüyü üreten bağımsız donanım satıcısı (IHV) veya cihazı sağlayan özgün ekipman üreticisi (OEM) ile görüşün. |

## <a name="see-also"></a>Ayrıca bkz.

Windows 10 için FastTrack Center avantajı, **Masaüstü uygulaması güvence altına**erişim sağlar. Bu avantaj, Windows 10 ve kurumsal uyumluluk için Microsoft 365 uygulamalarla ilgili sorunları gidermek üzere tasarlanan yeni bir hizmettir. Daha fazla bilgi için bkz. [Masaüstü uygulamaları güvence](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
