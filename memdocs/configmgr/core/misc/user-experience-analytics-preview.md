---
title: Endpoint Analytics önizlemesi
titleSuffix: Configuration Manager
description: Endpoint Analytics önizlemesi için yönergeler.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: e7dbb53833c29aae442eec4ca3c8402b99cde237
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693229"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a>Endpoint Analytics önizlemesi

> [!Note]  
> Bu bilgiler, ticari olarak yayınlanmadan önce önemli ölçüde değiştirilebilen bir önizleme özelliğiyle ilgilidir. Burada verilen bilgilerle ilgili olarak Microsoft açık veya zımni hiçbir garanti vermez. 
>
> Endpoint Analytics 'teki değişiklikler hakkında daha fazla bilgi için bkz. [Endpoint Analytics 'teki](whats-new-endpoint-analytics.md)yenilikler. 

## <a name="endpoint-analytics-overview"></a>Endpoint Analytics genel bakış

Son kullanıcıların uzun önyükleme süreleri veya diğer kesintiler üzerinde karşılaşmaları çok seyrek değildir. Bu kesintiler bir birleşimi olabilir:

- Eski donanım
- Son Kullanıcı deneyimi için en iyi duruma getirilmeyen yazılım yapılandırması
- Yapılandırma değişikliklerinden ve güncelleştirmelerden kaynaklanan sorunlar

Bu sorunlar ve diğer son kullanıcı deneyimi sorunları, son kullanıcı deneyimine çok fazla görünürlük içermediğinden devam etmez. Genellikle, bu sorunların tek görünürlüğü, genellikle en iyi duruma getirilmesi gerekenler hakkında net bilgiler sağlamayan, yavaş maliyetli bir destek kanalından gelir. Bu sorunların maliyetini yalnızca BT desteklemez. Sorunlarla ilgilenirken harcadıkları zaman bilgisi çalışanları da maliyetlidir. Kullanıcı üretkenliğini azaltan performans, güvenilirlik ve destek sorunları, kuruluşun en alt hattına da büyük bir etkiye sahip olabilir.

Kullanıcı üretkenliğini geliştirmek ve Kullanıcı deneyimine yönelik Öngörüler sunarak BT destek maliyetlerini azaltmak için **Endpoint Analytics** amaçlar. İçgörüler, BT 'nin son kullanıcı deneyimini öngörülü destekle en uygun hale getirmesine ve yapılandırma değişikliklerinin Kullanıcı etkisini değerlendirerek Kullanıcı deneyimine yönelik gerilemeleri algılamasına olanak tanır.

Bu ilk sürüm, üç şeylere odaklanır:

- [**Önerilen yazılım**](#bkmk_uea_rs): en iyi kullanıcı deneyimini sağlamaya yönelik öneriler
- [**Proaktif düzeltme betiği**](#bkmk_uea_prs): son kullanıcılar sorunları fark etmeden önce yaygın destek sorunlarını giderin
- [**Başlangıç performansı**](#bkmk_uea_bp): kullanıcıların uzun süre önyükleme ve oturum açma gecikmeleri olmadan hızla verimliliğine hızlı bir şekilde yararlanmanıza yardımcı olun

Bu sürüm yalnızca başlangıcıdır. İlk sürümden sonra, diğer başlıca kullanıcı deneyimleri için hızlı bir şekilde yeni Öngörüler ekleyeceğiz. Endpoint Analytics 'teki değişiklikler hakkında daha fazla bilgi için bkz. [Endpoint Analytics 'teki](whats-new-endpoint-analytics.md)yenilikler.

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a>Başlarken

Endpoint Analytics 'i kullanmaya başlamak için önkoşulları doğrulayıp veri toplamaya başlayın. 

### <a name="technical-prerequisites"></a>Teknik Önkoşullar

Bu önizleme için Configuration Manager veya Microsoft Intune aracılığıyla cihazları kaydedebilirsiniz. 

Cihazları Intune ile kaydetmek için bu önizleme şunları gerektirir:
- Windows 10 çalıştıran Intune kayıtlı cihazlar
- Başlangıç performansı öngörüleri yalnızca, Windows 10 Enterprise (Home ve Pro sürümleri) sürümü 1903 veya üzeri sürümleri çalıştıran cihazlarda kullanılabilir ve cihazların Azure AD 'ye katılmış veya hibrit Azure AD 'ye katılmış olması gerekir. Çalışma alanına katılmış makineler Şu anda desteklenmiyor.
- Cihazlardan Microsoft genel bulutuna ağ bağlantısı. Daha fazla bilgi için bkz. [uç noktalar](#bkmk_uea_endpoints).
- [Intune Hizmet Yöneticisi rolü](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) , [veri toplamaya başlamak](#bkmk_uea_start)için gereklidir.
   - **Başlat**' a tıklayarak, müşteri verilerinizin Microsoft Intune kiracınızı sağladığınızda seçtiğiniz konumun dışında depolanabileceğini kabul etmiş ve kabul etmiş olursunuz.
   - Verileri toplamak için **Başlat** 'a tıkladıktan sonra, diğer salt okunurdur roller verileri görüntüleyebilir.

Configuration Manager aracılığıyla cihazları kaydetmek için bu önizleme şunları gerektirir:
- Configuration Manager sürüm 2002 veya daha yenisi
- 2002 veya daha yeni bir sürüme yükseltilen istemciler
- [Microsoft Endpoint Manager kiracı iliştirme](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) Kuzey Amerika bir Azure kiracı konumuyla etkinleştirildi (yakında diğer bölgelere genişletireceğiz)

Cihazların Intune veya Configuration Manager aracılığıyla kaydedilip edilmeyeceğini, [**proaktif düzeltme komut dosyası oluşturma**](#bkmk_uea_prs) aşağıdaki gereksinimlere sahiptir:
- Cihazların Azure AD 'ye katılmış veya hibrit Azure AD 'ye katılmış olması ve aşağıdaki koşullardan birini karşılaması gerekir:
- Intune tarafından yönetilen bir Windows 10 Enterprise, Professional veya eğitim cihazı
- Intune 'a işaret eden [istemci uygulamaları iş yükü](../../comanage/workloads.md#client-apps) ile Windows 10 Enterprise, sürüm 1607 veya üstünü çalıştıran [ortak yönetilen](../../comanage/overview.md) bir cihaz.
- Windows 10 Enterprise, sürüm 1903 veya üstünü çalıştıran, [istemci uygulamaları iş yükünün](../../comanage/workloads.md#client-apps) Configuration Manager işaret ettiği [ortak yönetilen](../../comanage/overview.md) bir cihaz.

### <a name="licensing-prerequisites"></a>Lisanslama önkoşulları

Endpoint Analytics aşağıdaki planlara dahildir: 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) veya üzeri
- [Microsoft 365 Kurumsal E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) veya üzeri.

Proaktif düzeltmeler Ayrıca, yönetilen cihazlar için aşağıdaki lisanslardan birini gerektirir:
- Windows 10 Enterprise E3 veya E5 (Microsoft 365 F3, E3 veya E5 'e dahildir)
- Windows 10 eğitim a3 veya a5 (Microsoft 365 a3 veya a5 'e dahildir)
- Windows sanal masaüstü erişimi E3 veya E5

### <a name="permissions"></a>İzinler

#### <a name="endpoint-analytics-permissions"></a>Endpoint Analytics izinleri

Endpoint Analytics için aşağıdaki izinler kullanılır:
- **Cihaz yapılandırması** kategorisi altında **okuyun** .
- **Kuruluş** kategorisinin altında **okuyun** . <!--temporary for pp-->
- **Endpoint Analytics** kategorisi altındaki kullanıcının rolüne uygun izinler.

Salt okunurdur bir Kullanıcı yalnızca **cihaz yapılandırmalarının** ve **Endpoint Analytics** kategorilerinin altında **okuma** iznine sahip olmalıdır. Bir Intune yöneticisinin tipik olarak tüm izinleri olması gerekir.

#### <a name="proactive-remediations-permissions"></a>Proaktif düzeltme izinleri

Öngörülü düzeltmeler için, kullanıcının **cihaz yapılandırması** kategorisi altında rollerine uygun izinlere ihtiyacı vardır.  Kullanıcı yalnızca proaktif düzeltmeler kullanıyorsa, **Endpoint Analytics** kategorisindeki izinler gerekli değildir.


## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a>Veri toplamaya başla

1. Şuraya gidin: `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. **Başlat**'a tıklayın. Bu, tüm uygun cihazlardan önyükleme performansı verilerini toplamak üzere otomatik olarak bir yapılandırma profili atar. [Atanan cihazları](#bkmk_uea_profile) daha sonra değiştirebilirsiniz. Başlangıç performansı verilerinin, yeniden başlatıldıktan sonra Intune kayıtlı cihazlarınızdan doldurulması 24 saate kadar sürebilir.
   - Yaygın sorunlar hakkında daha fazla bilgi için bkz. [Başlangıç performansı cihaz kaydı sorunlarını giderme](#bkmk_uea_enrollment_tshooter).

## <a name="overview-page"></a>Genel Bakış sayfası

Verileriniz hazırlandıktan sonra **genel bakış** sayfasında daha ayrıntılı olarak açıklanan bazı bilgiler görürsünüz:

- **Kullanıcı deneyimi puanı** , **Önerilen yazılım** ve **Başlangıç performansı puanlarının**50/50 ağırlıklı ortalamasıdır. Zaman içinde alt puanların kümesini genişleteceğiz.

- Bir taban çizgisi ayarlayarak, geçerli puanınızı diğer puanlara karşılaştırabilirsiniz.
  - [Taban çizgisi](#bkmk_uea_baselines) bölümünde açıklandığı gibi, *ticari ortanca* için yerleşik bir taban çizgisi vardır. Bu, tipik bir kurumsal ile nasıl karşılaştırılacağını görmenizi sağlar. İlerleme durumunu izleyebilir veya zaman içinde gerilemeleri görüntüleyebilmeniz için geçerli ölçümlerinize göre yeni taban çizgileri oluşturabilirsiniz.
   - Temel işaretçiler, genel puan ve alt puanlarınız için gösterilir. Puanlardan herhangi biri, seçili taban çizgisinden yapılandırılabilir eşikten daha fazla olursa, puan kırmızı olarak görüntülenir ve en üst düzey puan dikkat edilmesi gereken şekilde işaretlenir.
  - **Yetersiz veri** durumu, anlamlı bir puan sağlamak üzere rapor veren yeterli cihaz olmadığı anlamına gelir. Şu anda en az beş cihaz gereklidir.

- **Filtreler** , bir cihaz veya Kullanıcı alt kümesinde puanınızı görüntülemenize imkan tanır. Ancak, filtre işlevselliği bu önizlemede etkin değildir.

- **Öngörüler ve öneriler** puanınızı geliştirmek için öncelikli bir listesidir. **En iyi yöntemlere** veya **Önerilen yazılıma**gittiğinizde bu liste alt düğümün bağlamına filtrelenir.

[![Endpoint Analytics genel bakış sayfası](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a>Önerilen yazılım

> [!Important]  
> Endpoint Analytics, Endpoint Analytics 'e kaydedilip kaydedilmediğine bakılmaksızın tüm Intune yönetilen cihazlarınızın **yazılım benimseme** Puanını hesaplar.

Belirli yazılımlar, düşük düzeyli sistem durumu ölçümlerinden bağımsız olarak son kullanıcı deneyimini geliştirmek için bilinmektedir. Örneğin, Windows 10, Windows 7 ' den çok daha yüksek bir Net Promoter Puanı elde etti. **Yazılım benimseme** puanı, önerilen çeşitli yazılımları dağıtan cihazların yüzdesinin ağırlıklı ortalamasını temsil eden 0 ile 100 arasında bir sayıdır. Kullanıcılar bunlarla daha sık etkileşimde bulunduğundan, geçerli ağırlık, Windows için diğer ölçümler için daha yüksektir. Ölçümler aşağıda açıklanmıştır: 

[![Endpoint Analytics önerilen yazılım sayfası](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a> Windows 10

Windows 10, Windows 'un eski sürümlerinden daha iyi bir kullanıcı deneyimi sağlar. Daha fazla bilgi için bkz. [TEI teknik incelemesi](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf) .

Bu ölçüm Windows 10 ' da cihazların yüzdesini ve Windows 'un eski bir sürümünü ölçer.

Windows 'un eski sürümlerinden cihazları taşımak için önerilen düzeltme eylemi, [Masaüstü Analizi](../../desktop-analytics/overview.md)'ni kullanarak bir dağıtım planı oluşturmaktır.

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a>Autopilot

Microsoft Autopilot, çalışan cihazın fabrika veya sıfırlamaya doğru bir şekilde sağlanması için, ilk olarak Windows 10 bilgisayarlar için yerel deneyimden daha basit bir sağlama deneyimi sağlar.

Bu ölçüm, Autopilot için kayıtlı Windows 10 cihazlarının yüzdesini ölçer.

Önerilen Düzeltme eylemi, [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot)kullanarak var olan cihazları Autopilot 'ye kaydetmedir.

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a>Azure Active Directory

Azure Active Directory (Azure AD), kullanıcılara uygulamalar ve hizmetler için cihaz genelinde çoklu oturum açma, Windows Hello oturum açma, self servis BitLocker kurtarma ve kurumsal veri dolaşımı gibi çeşitli verimlilik avantajları sağlar.

Bu ölçüm, Azure AD 'ye kayıtlı cihazların yüzdesini ölçer.

Microsoft-Intune yönetilen cihazlarınız zaten Azure AD 'ye kayıtlı. Configuration Manager tarafından yönetilen cihazlar için önerilen düzeltme eylemi, [Azure AD 'ye kaydolmaları](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) veya [onları birlikte yönetmektedir](../../comanage/overview.md). Ortak yönetim cihazları, bulut yönetimi puanınızı da geliştirir.

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a>Bulut yönetimi

Microsoft Intune, kullanıcılara Kurumsal ağdan uzakta olduklarında bile kurumsal kaynaklara erişimi etkinleştirme dahil olmak üzere çeşitli verimlilik avantajları sağlar ve grup ilkesi gereksinimini ve performans ek yükünü ortadan kaldırır, daha iyi bir son kullanıcı deneyimi elde edilir. Bu ölçüm Microsoft Intune kayıtlı bilgisayarların yüzdesini ölçer. [Microsoft 'un çalışanlarınız için bunu nasıl etkinleştirçalıştığını](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune)görün.

Intune 'A henüz kaydolmamış Configuration Manager tarafından yönetilen cihazlar için önerilen düzeltme eylemi, [bunları ortak olarak yönetmektedir](../../comanage/overview.md).

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a>Ticari ortanca yok

**Ticari ortanca** 'in yerleşik taban çizgisi Şu anda yukarıdaki bölümlerde listelenen alt puanların ölçümlerine sahip değildir.

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a>Başlangıç performansı

> [!NOTE]
> Tüm cihazlarınızdan başlangıç performansı verilerini görmüyorsanız lütfen bkz. [Başlangıç performansı cihaz kaydında sorun giderme](#bkmk_uea_enrollment_tshooter).

Başlangıç performansı puanı, kullanıcıların uzun önyükleme ve oturum açma gecikmeleri olmadan hızla verimliliğine hızlı bir şekilde yararlanmasının sağlanmasına yardımcı olur. **Başlangıç puanı** 0 ile 100 arasında bir sayıdır. Bu puan, aşağıdaki gibi hesaplanan **önyükleme puanı** ve **oturum açma** puanının ağırlıklı ortalamasıdır:

- **Önyükleme puanı**: oturum açma süresinin, oturum açma süresini temel alır. Güncelleştirme aşaması hariç olmak üzere her bir cihazdan son önyükleme zamanına bakıyoruz ve sonra 0 (düşük) ile 100 (olağanüstü) arasında puan veriyoruz. Bu puanlar, genel bir kiracı önyükleme puanı sağlamak için ortalaması alınır.
- **Oturum açma puanı**: Kullanıcı yanıt veren bir masaüstüne erişebilene kadar kimlik bilgilerinin girildiği zamana bağlı olarak (Masaüstü tarafından IŞLENDIĞINDE ve CPU kullanımı en az 2 saniyede %50 altına düşmüş olabilir). Her bir cihaza yönelik son oturum açma zamanına bakar, ilk oturum açma işlemleri veya bir özellik güncelleştirmesinden hemen sonra oturum açma işlemleri hariç olur ve sonra 0 (düşük) ile 100 (olağanüstü) arasında puan elde ederiz. Bu puanlar, genel bir kiracı önyükleme puanı sağlamak için ortalaması alınır.

[![Endpoint Analytics başlangıç performansı sayfası](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>Insights

**Başlangıç performansı** sayfası, aşağıdaki bölümlerde açıklanan **öngörülerin ve önerilerin**öncelikli bir listesini de sağlar:

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a>Sabit disk sürücüleri

Başlangıç performansı, önyükleme sürücüsünün sabit disk olduğu cihaz sayısıyla ilgili bir öngörü sağlar. Sabit disk sürücüleri genellikle katı hal sürücülerinden en çok dört kat önyükleme zamanına neden olacaktır. Ayrıca, katı hal sürücülerine geçerek elde ettiğiniz performansı başlatmak için beklenen gelişimi de bildiririz.

Sabit disk sürücülerine sahip cihazların listesini görmek için öğesine tıklayın. Önerilen eylem, bu cihazları katı hal sürücülerine yükseltmesidir.

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a>grup ilkesi

Başlangıç performansı, grup ilkesi nedeniyle önyükleme ve oturum açma süreleri olan cihazların sayısı hakkında bir öngörü sağlar. Öğesine tıkladığınızda cihazlar görünümüne gidersiniz. Görünüm grup ilkesi zamana göre sıralanır, böylece daha fazla sorun giderme için etkilenen cihazları görebilirsiniz.

Belirli bir cihaza tıkladığınızda, önyükleme ve oturum açma geçmişini görebilirsiniz. Geçmiş, sorunun bir gerileme olup olmadığını ve ne zaman meydana gelebilir olduğunu belirlemenize yardımcı olur.

Grup Ilkeleri performansını iyileştirme hakkında birçok makale olmakla kalmaz, bunun yerine bulut yönetimine geçiş yapabilirsiniz. Bulut yönetimi ' ne geçiş yapmak, [Intune güvenlik temellerini](https://docs.microsoft.com/intune/protect/security-baselines) ve yakında Yayınlanan ilke Analizi aracını kullanmanıza olanak sağlar.

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a>Yavaş önyükleme ve oturum açma süreleri

Başlangıç performansı, yavaş önyükleme veya oturum açma süreleriyle cihaz sayısı hakkında bir öngörü sağlar. "0" önyükleme puanı veya oturum açma puanı yavaş olduğu anlamına gelir. Öğesine tıkladığınızda cihazlar görünümüne gidersiniz. Cihazlar, temel önyükleme zamanına veya temel oturum açma zamanına göre sıralanır, böylece daha fazla sorun giderme için etkilenen cihazları görebilirsiniz.

Belirli bir cihaza tıkladığınızda, önyükleme ve oturum açma geçmişini görebilirsiniz. Geçmiş, sorunun bir gerileme olup olmadığını ve ne zaman meydana gelebilir olduğunu belirlemenize yardımcı olur.

### <a name="reporting-tabs"></a>Raporlama sekmeleri

**Başlangıç performansı** sayfasında, içgörüler için aşağıdakiler dahil olmak üzere destek sağlayan raporlama sekmeleri bulunur:
1. **Model performansı**. Bu sekme, cihaz modeline göre önyükleme ve oturum açma performansını görmenizi sağlar. Bu, performans sorunlarının belirli modellere yalıtılmış olup olmadığını belirlemenize yardımcı olabilir.
1. **Cihaz performansı**. Bu sekme, tüm cihazlarınız için önyükleme ve oturum açma ölçümleri sağlar. Sorun gidermeye yardımcı olmak üzere hangi cihazların en kötü puanları olduğunu görmek için belirli bir ölçüye göre (örneğin, GP oturum açma zamanı) sıralama yapabilirsiniz. Ayrıca, bir cihazı adına göre de arayabilirsiniz. Bir cihaza tıkladığınızda, ön yükleme ve oturum açma geçmişini görebilirsiniz. Bu, son bir gerileme olup olmadığını belirlemenize yardımcı olabilir
1. **Başlangıç işlemi**. Bu sekme (görünür durumdaysa), bu özelliği geliştirdiğimiz sürece yalnızca sizin için bu özelliği geliştirdik. Bu özellik, hangi işlemlerin "yanıt veren masaüstü süresi" aşamasının hangi işlemlerde etkilendiğini gösterecektir. Bu, masaüstü işlendikten sonra CPU 'YU %50 oranında tutuyor.

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a>Proaktif düzeltmeler

Proaktif düzeltmeler, bir kullanıcının cihazında sorun olduğunu fark etmeden önce yaygın destek sorunlarını tespit edebilir ve giderebilecekleri komut dosyası paketlerdir. Bu düzeltmelere destek çağrılarının azaltılmasına yardımcı olabilir. Kendi betik paketinizi oluşturabilir veya yazdığımız ve destek biletlerini azaltmak için ortamımızda kullandığınız komut dosyası paketlerinden birini dağıtabilirsiniz.

Her betik paketi bir algılama betiği, bir düzeltme betiği ve meta veriler içerir. Intune aracılığıyla, bu betik paketlerini dağıtabilir ve bunların verimliliğine ilişkin raporları görebileceksiniz. Yeni betik paketlerini etkin bir şekilde geliştirdik ve bunları kullanarak deneyimlerinizi öğreniyoruz. Betik paketleri hakkında herhangi bir geri bildirimde bulunabilseniz, Endpoint Analytics önizleme kişinizin iletişim kurun.

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a>Algılama ve düzeltme betiklerini alma

1. [PowerShell betikleri](#bkmk_uea_ps_scripts) bölümünde Bu makalenin altındaki betikleri kopyalayın.
    - Adları ile `det` başlayan betik dosyaları algılama betikleridir. Düzeltme betikleri ile `rem`başlar.
    - Betiklerin açıklaması için bkz. [betik açıklamaları](#bkmk_uea_scripts).
1. Her betiği, belirtilen adı kullanarak kaydedin. Ad aynı zamanda her bir betiğin üst kısmındaki açıklamalardır.
    - Farklı bir betik adı kullanabilirsiniz, ancak [betik açıklamaları](#bkmk_uea_scripts) bölümünde listelenen adla eşleşmez.


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a>Betikleri dağıtma ve izleme
**Microsoft Intune yönetim uzantısı** hizmeti, Intune 'dan betikleri alır ve bunları çalıştırır. Betikler her 24 saatte bir yeniden çalıştırılır. Betikleri dağıtmak ve izlemek için aşağıdaki yönergeleri izleyin:

1. Konsolundaki **proaktif** düzeltmeler düğümüne gidin.
1. Bir betik paketi oluşturmak için **betik paketi oluştur** düğmesine tıklayın.
     [![Endpoint Analytics proaktif düzeltmeler sayfası. Oluştur bağlantısını seçin.](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. **Temel bilgiler** adımında, betik paketine bir **ad** ve isteğe bağlı olarak bir **Açıklama**verin. **Yayımcı** alanı düzenlenebilir, ancak varsayılan olarak kiracı adınızı alabilir. **Sürüm** düzenlenemiyor. 
1. **Ayarlar** adımında, indirdiğiniz betiklerdeki metni **algılama betiği** ve **Düzeltme betiği** alanlarına kopyalayın. 
   - Aynı pakette olması için karşılık gelen algılama ve düzeltme betiğinin olması gerekir. Örneğin, `Detect_stale_Group_Policies.ps1` algılama betiği `Remediate_stale_GroupPolicies.ps1` düzeltme betiğine karşılık gelir.
       [![Endpoint Analytics proaktif düzeltmeleri betik ayarları sayfası.](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. **Ayarlar** sayfasındaki seçenekleri önerilen yapılandırmalara göre son yapın:
   - **Bu betiği, oturum açma kimlik bilgilerini kullanarak çalıştırın**: Bu, betiğe bağımlıdır. Daha fazla bilgi için bkz. [betik açıklamaları](#bkmk_uea_scripts).
   - **Betik Imzasını zorla denetimi**: Hayır
   - **Betiği 64-bit PowerShell 'de Çalıştır**: Hayır
1. **İleri** ' ye tıklayın ve ihtiyacınız olan tüm **kapsam etiketlerini** atayın.
1. **Atamalar** adımında, komut dosyası paketini dağıtmak istediğiniz cihaz gruplarını seçin.
1. Dağıtımınız için **İnceleme ve oluşturma** adımını doldurun.
1. **Raporlama** > **Endpoint Analytics-proaktif**düzeltmeler altında, algılama ve düzeltme durumunuz için bir genel bakış görebilirsiniz.
       [![Endpoint Analytics proaktif düzeltmelere ilişkin rapor, genel bakış sayfası.](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. Dağıtımınızdaki her bir cihaz için durum ayrıntılarını almak üzere **cihaz durumu** ' na tıklayın.
       [![Endpoint Analytics proaktif düzeltmelere cihaz durumu.](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a>Uç nokta Analizi ayarları

Ayarlar sayfasından **genel** veya **temel**seçeneğini belirleyebilirsiniz. Bu ayarların her biri aşağıda açıklanmıştır:

### <a name="general"></a><a name="bkmk_uea_gen"></a>Genel

**Ayarlar** 'daki **genel** sayfası, Intune başlangıç performansı veri koleksiyonunun etkinleştirilip etkinleştirilmediğini görmenizi sağlar. Kullanıcı deneyimi analizlerini etkinleştirmek için **Başlat** ' a tıkladığınızda varsayılan olarak tüm cihazlarınız için otomatik olarak etkinleştirilir. Önyükleme ve oturum açma kayıtlarının toplandığı cihaz kümesini değiştirmek için Intune veri toplama ilkesi düğümüne gidebilirsiniz.


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a>Intune veri toplama ilkesi

Bu ayarı bir cihaz alt kümesine atamak için aşağıdaki bilgileri içeren [bir profil oluşturun](/intune/configuration/device-profile-create#create-the-profile) : 

  - **Ad**: profil için **Intune veri toplama ilkesi** gibi açıklayıcı bir ad girin
   
  - **Açıklama**: profil için bir açıklama girin. Bu ayar isteğe bağlıdır ancak önerilir.
    
  - **Platform**: **Windows 10 ve üzeri**’ni seçin
   
  - **Profil türü**: **Windows sistem durumu izleme** ' yi seçin
   
  - **Ayarları**yapılandırın:
   
       - **Sistem durumu izleme**: Windows 10 cihazlarından olay bilgilerini toplamak için **Etkinleştir** ' i seçin
    
    - **Kapsam**: **önyükleme performansını** seçin 

  - Profili belirli bir ölçüte uyan bir gruptaki belirli BT gruplarına veya cihazlara filtrelemek için [kapsam etiketleri](/intune/configuration/device-profile-create#scope-tags) ve [uygulanabilirlik kurallarını](/intune/configuration/device-profile-create#applicability-rules) kullanın.

> [!NOTE]
> Configuration Manager veri bağlayıcısını yapılandırma yönergeleri için yer tutucu vardır. Ancak bu işlev, bu ilk özel önizlemede uygulanmadı.

  [![Endpoint Analytics genel ayarları sayfası](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a>Taban çizgisi yönetimi

Bir taban çizgisi ayarlayarak, geçerli puanlarınızı ve alt puanlarını diğer kullanıcılarla karşılaştırabilirsiniz.

1. **Ticari ortanca**için yerleşik bir taban çizgisi vardır. Bu, puanlarınızı tipik bir kuruluşa göre karşılaştırmanızı sağlar.
1. İlerleme durumunu izlemek veya zaman içindeki gerilemeleri görüntülemek için geçerli ölçümlerinize göre yeni taban çizgileri oluşturabilirsiniz. **Yeni oluştur** düğmesine tıklayın ve yeni temele bir ad verin. Tarihi içeren bir ad öneririz, bu nedenle raporlar sayfalarında açılan listeden seçim yapmak daha kolay olur.
1. Kiracı başına 100 taban çizgisi sınırı vardır. Artık gerekli olmayan eski taban çizgilerini silebilirsiniz.
1. Geçerli ölçümleriniz kırmızı olarak işaretlenir ve raporlardaki geçerli taban çizgisinin altına düştiklerinde gerileme olarak gösterilir. Ölçümlerin gün ila güne kadar dalgalanmasına yönelik kusursuz bir normal olduğundan, varsayılan olarak %10 ' a bir regresyon eşiği ayarlayabilirsiniz. Bu eşikle, ölçümler yalnızca %10 ' dan fazla bir şekilde gerilediklerinde gerileme olarak işaretlenir.

   [![Endpoint Analytics taban çizgisi ayarları sayfası](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a>Sorunu

Aşağıdaki bölümler, karşılaşabileceğiniz sorunları gidermeye yardımcı olmak için kullanılabilir.

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a>Başlangıç performansı cihaz kaydı sorunlarını giderme

Genel Bakış sayfasında, verilerin beklendiğini gösteren bir başlık ile birlikte bir başlangıç performansı puanı gösterilirse veya başlangıç performansının cihaz performansı sekmesi beklediğinizden daha az cihaz gösteriyorsa, sorunu gidermek için gerçekleştirebileceğiniz bazı adımlar vardır.

İlk olarak, başlangıç performansı veri toplamaya yönelik kısıtlamaların hızlı bir özeti aşağıda verilmiştir:
1. Cihazların Windows 10 sürüm 1903 veya üzeri olması gerekir.
2. Cihazların Azure AD 'ye katılmış olması gerekir. Şu anda çalışma alanına katılmış cihazları desteklemiyoruz, ancak bu işlevselliği Windows 'a eklemenin etkin bir şekilde araştırılmaktadır.
3. Cihazlar Windows 10 Enterprise Edition olmalıdır. Windows 10 Home ve Professional Şu anda desteklenmemektedir, ancak bu işlevselliği Windows 'a eklemenin etkin bir şekilde araştırılmaktadır.

Bu sorunların yakında çıkacak Configuration Manager bağlayıcısından gelen verilere uygulanmadığını unutmayın; sürüm, sürüm veya dizin yapılandırmasından bağımsız olarak, herhangi bir Configuration Manager istemci BILGISAYARDAN veri toplayabilecektir.

İkincisi, sorun giderme için hızlı bir denetim listesi aşağıda verilmiştir:
1. Performans verilerini istediğiniz tüm cihazlara hedeflenmiş Windows sistem durumu Izleme profiline sahip olduğunuzdan emin olun. Bu profil için uç nokta Analizi ayar sayfasından bir bağlantı bulabilir veya diğer Intune profilinde olduğu gibi bu profile gidebilirsiniz. Beklenen cihaz kümesine atandığından emin olmak için atama sekmesine bakın. 
1. Veri toplama için hangi cihazların başarıyla yapılandırıldığını göz atalım. Ayrıca, bu bilgileri profillere Genel Bakış sayfasında de görebilirsiniz.  
   - Müşterilerin, etkilenen cihazların hata kodunu göstereceği profil atama hatalarını görebileceği bilinen bir sorun vardır `-2016281112 (Remediation failed)`. Bu sorunu etkin bir şekilde araştırıyoruz.
1. Veri toplama etkinleştirildikten sonra veri toplama için başarıyla yapılandırılmış cihazların yeniden başlatılması gerekir ve cihazın cihaz performansı sekmesinde gösterilmesi için 24 saate kadar beklemeniz gerekir.
1. Cihazınız veri toplama için başarılı bir şekilde yapılandırıldıysa, daha sonra yeniden başlatılırsa ve 24 saat sonra hala görmüyorsanız, cihazın koleksiyon uç noktalarımıza ulaşamamakta olması olabilir. Şirketiniz bir ara sunucu kullanıyorsa ve uç noktaların proxy 'de etkinleştirilmemiş olması durumunda bu sorun oluşabilir. Daha fazla bilgi için bkz. [sorun giderme uç noktaları](#bkmk_uea_endpoints).


### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a>Noktalarının

Cihazları Endpoint Analytics 'e kaydetmek için, gerekli işlevsel verileri Microsoft 'a göndermelidir. Ortamınız bir ara sunucu kullanıyorsa, proxy 'yi yapılandırmaya yardımcı olması için bu bilgileri kullanın.

İşlevsel veri paylaşımını etkinleştirmek için Proxy sunucunuzu aşağıdaki uç noktalara izin verecek şekilde yapılandırın:

> [!Important]  
> Gizlilik ve veri bütünlüğü için Windows, gerekli işlevsel veri paylaşımı uç noktalarıyla iletişim kurarken bir Microsoft SSL sertifikası (sertifika sabitleme) olup olmadığını denetler. SSL yakalamasyonu ve incelemesi mümkün değildir. Endpoint Analytics 'i kullanmak için bu uç noktaları SSL incelemeden hariç tutun.<!-- BUG 4647542 -->

| Uç Nokta  | İşlev  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | [Gerekli işlevsel verileri](#bkmk_uea_datacollection) Intune veri toplama uç noktasına göndermek için kullanılır. |
| `https://graph.windows.net` | Hiyerarşinizi Endpoint Analytics 'e iliştirirken ayarları otomatik olarak almak için kullanılır (Configuration Manager sunucu rolünde). Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Endpoint Analytics ile cihaz toplamayı ve cihazlarını eşitleme için kullanılır (yalnızca Configuration Manager sunucu rolünde). Daha fazla bilgi için bkz. [bir site sistemi sunucusu için proxy yapılandırma](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |


### <a name="proxy-server-authentication"></a>Proxy sunucusu kimlik doğrulaması

Kuruluşunuz internet erişimi için proxy sunucu kimlik doğrulamasını kullanıyorsa, kimlik doğrulama nedeniyle verileri engellemediğinden emin olun. Proxy 'niz cihazların bu verileri göndermesini izin vermezse, masaüstü Analizi 'nde gösterilmez.

#### <a name="bypass-recommended"></a>Atla (önerilir)

Proxy sunucularınızı, veri paylaşımı uç noktalarına giden trafik için proxy kimlik doğrulaması gerektirecek şekilde yapılandırın. Bu seçenek en kapsamlı çözümdür. Tüm Windows 10 sürümleri için geçerlidir.  

#### <a name="user-proxy-authentication"></a>Kullanıcı proxy kimlik doğrulaması

Cihazları, oturum açmış kullanıcının proxy kimlik doğrulaması bağlamını kullanacak şekilde yapılandırın. Bu yöntem aşağıdaki konfigürasyonları gerektirir:

- Cihazların desteklenen bir Windows sürümü için geçerli kalite güncelleştirmesi var

- Windows ayarları 'nın Internet & ağ **Ara sunucu ayarları** 'nda Kullanıcı düzeyi proxy 'Yi (Winınet proxy) yapılandırın. Eski Internet seçenekleri denetim masasını da kullanabilirsiniz.

- Kullanıcıların, veri paylaşım uç noktalarına erişmek için proxy iznine sahip olduğundan emin olun. Bu seçenek, cihazların proxy izinlerine sahip konsol kullanıcılarına sahip olmasını gerektirir, bu nedenle bu yöntemi gözetimsiz cihazlarla kullanamazsınız.

> [!IMPORTANT]
> Kullanıcı proxy kimlik doğrulama yaklaşımı, Microsoft Defender Gelişmiş tehdit koruması kullanımıyla uyumlu değildir. Bu davranış, bu kimlik doğrulamanın **Disableenterpriseauthproxy** kayıt defteri anahtarını olarak `0`ayarlanmış olması, Microsoft Defender ATP 'nin olarak `1`ayarlanmasını gerektirmesidir. Daha fazla bilgi için bkz. [Microsoft Defender ATP 'de makine proxy ve internet bağlantısı ayarlarını yapılandırma](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

#### <a name="device-proxy-authentication"></a>Cihaz proxy kimlik doğrulaması

Bu yaklaşım aşağıdaki senaryoları destekler:

- Kullanıcının oturum açtığı veya cihazın kullanıcılarının internet erişimi olmayan, gözetimsiz cihazlar

- Windows tümleşik kimlik doğrulaması kullanmayan kimliği doğrulanmış proxy 'ler

- Microsoft Defender Gelişmiş tehdit koruması 'nı da kullanıyorsanız

Bu yaklaşım en karmaşıktır çünkü aşağıdaki yapılandırmalarda gereklidir:

- Cihazların yerel sistem bağlamında WinHTTP aracılığıyla proxy sunucusuna ulaşabildiğinizden emin olun. Bu davranışı yapılandırmak için aşağıdaki seçeneklerden birini kullanın:

  - Komut satırı`netsh winhttp set proxy`

  - Web proxy otomatik bulma (WPAD) protokolü

  - Saydam proxy

  - Aşağıdaki Grup İlkesi ayarını kullanarak cihaz genelinde Winınet proxy yapılandırın: **makine başına proxy ayarları yap (Kullanıcı başına değil)** (proxysettingsperuser = `1`)

  - Yönlendirilmiş bağlantı veya ağ adresi çevirisi (NAT) kullanan

- Active Directory ' deki bilgisayar hesaplarının veri uç noktalarına erişmesine izin vermek için proxy sunucuları yapılandırın. Bu yapılandırma, proxy sunucularının Windows tümleşik kimlik doğrulamasını desteklemesini gerektirir.  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a>Sık sorulan sorular

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>Betikler neden 1 kodla çıkıyor?

Betiklerin, düzeltme olması gerektiğini Intune 'a bildirmek için 1 koduyla çıkış yapılır. Bu durumda, algılama betiğinin 1 ile çıkış yapılması, düzeltmenin gerekli olduğu doğru anlamına gelir. Yalnızca CM 'de çalışan pek çok betik paketi uyumlu gösterebilir, ancak 1 kodu ile çıkabilir. Bu betikler için, 1 kodu ile çıkış bir şey değildir ancak cihazın doğru şekilde düzeltme yaptığını doğrulamak isteyebilirsiniz.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>Eski Grup Ilkeleri güncelleştirmesi betiği neden 0x87D00321 hatasıyla geri döndürüyor?

0x87D00321 bir betik yürütme zaman aşımı hatasıdır. Bu hata genellikle uzaktan bağlanan makinelerde oluşur. Potansiyel bir risk azaltma yalnızca iç ağ bağlantısı olan dinamik bir makine koleksiyonuna dağıtılması olabilir.

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a>Betik açıklamaları

Bu tabloda betik adları, açıklamalar, algılamalar, düzeltmeler ve yapılandırılabilir öğeler gösterilmektedir. Adları ile `Detect` başlayan betik dosyaları algılama betikleridir. Düzeltme betikleri ile `Remediate`başlar. Bu betikler, bu makaledeki sonraki bölümden kopyalanabilir.

|Betik adı|Açıklama|
|---|---|
|**Eski grup Ilkelerini Güncelleştir** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Son grup ilkesi yenilemenin ne zaman `7 days` önce daha büyük olup olmadığını algılar.  </br>Algılama betiğinin değerini `$numDays` değiştirerek 7 günlük eşiğini özelleştirin. </br></br>Ve çalıştıran `gpupdate /target:computer /force``gpupdate /target:user /force`  </br> </br>, Sertifikalar ve yapılandırmalara grup ilkesi aracılığıyla teslim edildiğinde ağ bağlantısıyla ilgili destek çağrılarını azaltmaya yardımcı olabilir. </br> </br> **Oturum açma kimlik bilgilerini kullanarak betiği çalıştırın**: Evet|
|**Office Tıkla-Çalıştır hizmetini yeniden Başlat** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| Tıkla-Çalıştır hizmetinin otomatik olarak başlayacak şekilde ayarlandığını ve hizmetin durdurulup durdurulduğunu algılar. </br> </br> Hizmeti otomatik olarak başlayacak ve durdurulmuş ise hizmeti başlatmaya ayarlayarak düzeltme yapın. </br></br> , Tıkla-Çalıştır hizmeti durdurulduğu için Win32 Microsoft 365 uygulamalarının Çalıştırılmayabileceği sorunları gidermeye yardımcı olur. </br> </br> **Oturum açma kimlik bilgilerini kullanarak betiği çalıştırın**: Hayır|
|**Ağ sertifikalarını denetle** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Makinenin veya kullanıcının süresi dolduğundan veya süresi dolmak üzere olan bir CA tarafından verilen sertifikaları algılar. </br> Algılama betiğinin değerini `$strMatch` değiştirerek CA 'yı belirtin. Süresi dolmak `$expiringDays` üzere olan sertifikaları bulmak için 0 veya süre sonu yakın olan sertifikaların bulunacağı başka bir gün sayısını belirtin.  </br></br>Kullanıcıya bir bildirim göndererek düzeltme yaparak düzeltme. </br> İleti başlığı `$Title` ve `$msgText` kullanıcıların görmesini istediğiniz metni içeren ve değerlerini belirtin. </br> </br> Kullanıcılara, yenilenmesi gerekebilecek, son kullanma izni veren sertifikaları bildirir. </br> </br> **Oturum açma kimlik bilgilerini kullanarak betiği çalıştırın**: Hayır|
|**Eski sertifikaları temizle** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Geçerli kullanıcının kişisel deposunda bir CA tarafından verilen süre aşımına uğradı sertifikaları algılar. </br> Algılama betiğinin değerini `$certCN` değiştirerek CA 'yı belirtin. </br> </br> Geçerli kullanıcının kişisel mağazasından bir CA tarafından verilen süre dolan sertifikaları silerek düzeltme. </br> Düzeltme `$certCN` betikindeki değerini değiştirerek CA 'yı belirtin. </br> </br> Geçerli kullanıcının kişisel mağazasından bir CA tarafından verilen süre dolma sertifikalarını bulur ve siler. </br> </br> **Oturum açma kimlik bilgilerini kullanarak betiği çalıştırın**: Evet|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a>PowerShell betikleri

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a>Endpoint Analytics veri gizliliği

### <a name="data-flow"></a>Veri akışı

Aşağıdaki çizimde, veri hizmetlerimiz, geçici depolama ve kiracınız aracılığıyla her bir cihazdan, gereken işlevsel verilerin nasıl akabileceği gösterilmektedir. Veriler, Windows Tanılama verilerine güvenmeksizin mevcut kurumsal işlem hatlarımızla akar.

[![Kullanıcı deneyimi veri akışı diyagramı](media/dataflow.png)](media/dataflow.png#lightbox)

1. Kayıtlı cihazlar için **Intune veri toplama** ilkesini yapılandırın. Bu ilke varsayılan olarak, Endpoint Analytics 'i **başlattığınızda** "tüm cihazlar" a atanır. Ancak, herhangi bir zamanda atamayı istediğiniz zaman bir cihaz alt kümesiyle [değiştirebilir](#bkmk_uea_set) veya hiç cihaz kullanamazsınız.

2. Cihazlar gerekli işlevsel verileri gönderiyor.

    - Atanmış ilkeye sahip Intune cihazları için, veriler Intune yönetim uzantısından gönderilir. Daha fazla bilgi için bkz. [gereksinimler](#bkmk_uea_prereq).
    - Configuration Manager yönetilen cihazlarda, veriler ConfigMgr Bağlayıcısı aracılığıyla Microsoft uç nokta yönetimine de akabilir. ConfigMgr Bağlayıcısı buluta eklenmiş. Yalnızca bir Intune kiracısına bağlantı gerektirir, ortak yönetimi açık hale gelir.

> [!Note]  
> Bir cihazın başlangıç Puanını hesaplamak için gereken veriler önyükleme zamanında oluşturulur. Güç ayarlarına ve kullanıcı davranışına bağlı olarak, bir cihaz, yönetici konsolunda başlangıç Puanını göstermek için ilkeyi doğru bir şekilde atadıktan sonra hafta sürebilir.  

3. Microsoft uç nokta yönetimi hizmeti her bir cihaz için verileri işler ve MS Graph API 'Lerini kullanarak yönetim konsolundaki tek tek cihazlar ve kuruluş toplamaları için sonuçları yayımlar.

Ortalama gecikme süresi yaklaşık 12 saat ve günlük işleme yapmak için gereken süre ile biter. Veri akışının diğer tüm bölümleri neredeyse gerçek zamanlı.

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>Veri toplama

Şu anda, Endpoint Analytics 'in temel işlevselliği, [tanımlanan](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data) ve [sözde](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data) olmayan kategorilerle ilgili olan önyükleme performansı kayıtlarıyla ilişkili bilgileri toplar. Zaman içinde ek işlevler eklediğimiz için, toplanan veriler gerektiği şekilde değişir. Şu anda toplanan ana veri noktaları:

#### <a name="identified-data"></a>Tanımlanan veriler

- Donanım envanteri bilgileri
  - **şunları yapın:** Cihaz üreticisi
  - **model:** Cihaz modeli
  - **Deviceclass:** Cihaz sınıflandırması. Örneğin, Masaüstü, sunucu veya mobil.
  - **Ülke:** Cihaz bölgesi ayarı
- Uygulama envanteri, örneğin
  - **ad:** Pencerelerin
  - **ver:** Geçerli işletim sisteminin sürümü.
  
#### <a name="pseudonymized-data"></a>Takma ad kullanılan veriler

- Bir kullanıcı ve/veya cihaza bağlı tanılama, performans ve kullanım verileri
  - **LogonId**
  - **BootID:** Sistem önyükleme KIMLIĞI
  - **Coreboottimeınmilliseconds:** Çekirdek önyükleme zamanı
  - **Totalboottimeınmilliseconds:** Toplam önyükleme süresi
  - **Updatetimeınmilliseconds:** İşletim sistemi güncelleştirmelerinin tamamlanacağı süre
  - **gpLogonDurationInMilliseconds**: grup ilkelerinin işlemesi için zaman
  - **desktopShownDurationInMilliseconds:** Masaüstü (Explorer. exe) yüklenecek zaman
  - **desktopUsableDurationInMilliseconds:** Masaüstü (Explorer. exe) için zaman kullanılabilir
  - **Topsüreçler:** Ön yükleme sırasında, CPU kullanım istatistikleri ve uygulama ayrıntıları (ad, Yayımcı, sürüm) ile önyükleme sırasında yüklenen işlemlerin listesi. Örneğin, *{\"ProcessName\":\"Svchost\",\"CPUusage\": 43,\"processfullpath\":\"C:\\\\Windows\\\\system32\\\\Svchost. exe\",\"ProductName\":\"Microsoft&reg; Windows&reg; işletim sistemi\",\"Publisher\":\"Microsoft Corporation\",\"ProductVersion\":\"10.0.18362.1\"}*
- Bir cihaz veya kullanıcıya bağlı olmayan cihaz verileri (bu veriler bir cihaz veya kullanıcıya bağlıysa Intune bunlara tanımlanan verilere olduğu gibi davranır)
  - **Kimliği:** Windows Update tarafından kullanılan benzersiz cihaz KIMLIĞI
  - **YerelKimliği:** Cihaz için yerel olarak tanımlanan benzersiz KIMLIK. Bu, insan tarafından okunabilen cihaz adı değildir. Büyük olasılıkla Hklm\software\microsoft\sqmclient\machineıdyolunda depolanan değere eşittir.
  - **aaddeviceıd:** Azure Active Directory cihaz KIMLIĞI
  - **OrgID:** Microsoft O365 kiracısı temsil eden benzersiz GUID
  
> [!Important]  
> Veri işleme ilklerimiz [Microsoft Intune Gizlilik bildiriminde](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)açıklanmaktadır. Yalnızca sizin imzaladığınız hizmetleri sağlamak için müşteri verilerinizi kullanıyoruz. Ekleme işlemi sırasında açıklandığı gibi, ana öğeleri güncel tutmak için tüm kayıtlı kuruluşların puanlarını Anonimleştir ve topladık.


### <a name="resources"></a>Kaynaklar

İlgili gizlilik yönleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Microsoft Intune Gizlilik bildirimi](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 ve gizlilik uyumluluğu](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Lisans hüküm ve belgeler](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Microsoft Azure veri merkezlerinde güvenlik ve Gizlilik](https://azure.microsoft.com/global-infrastructure/)  
- [Güvenilir bulutta güven](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Güven Merkezi](https://www.microsoft.com/trustcenter)  
