---
title: Windows hizmetini hizmet olarak yönetme
titleSuffix: Configuration Manager
description: Windows 10 istemcileri destek sonuna yakın olduğunda, hizmet olarak Windows (WaaS Configuration Manager) durumunu görüntüleyin, dağıtım halkalarını biçimlendirmek üzere bakım planları oluşturun ve Uyarıları görüntüleyin.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710842"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>Configuration Manager kullanarak Windows hizmeti olarak yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, ortamınızdaki hizmet olarak Windows (WaaS) durumunu görüntüleyebilirsiniz. Dağıtım halkalarını biçimlendirmek üzere bakım planları oluşturun ve yeni derlemeler yayınlandığında Windows 10 sistemlerinin güncel tutulduğundan emin olun. Ayrıca, Windows 10 istemcileri yarı yıllık kanal derlemesi için destek sonuna yaklaştığında uyarıları görüntüleyebilirsiniz.

Windows 10 bakım seçenekleri hakkında daha fazla bilgi için bkz. [hizmet olarak Windows 'A genel bakış](/windows/deployment/update/waas-overview#servicing-channels).

Windows hizmetini bir hizmet olarak yönetmek için aşağıdaki bölümleri kullanın.

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a>Kaynakları

Windows 10 Bakımı panosundaki verileri görmek için aşağıdaki işlemleri yapmanız gerekir:

- Windows 10 bilgisayarları, yazılım güncelleştirme yönetimi için Windows Server Update Services (WSUS) ile Configuration Manager yazılım güncelleştirmeleri kullanmalıdır. Bilgisayarlar, yazılım güncelleştirme yönetimi için Iş için Windows Update (veya Windows Insider 'lar) kullandıklarında, bilgisayar Windows 10 bakım planlarında değerlendirilmez. Daha fazla bilgi için bkz. [Windows 10’da Windows Update for Business ile Tümleştirme](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).

- Desteklenen bir WSUS sürümü kullanın:
  - WSUS 10.0.14393 (Windows Server 2016 ' de rol)
  - WSUS 10.0.17763 (Windows Server 2019 ' de rol) (Configuration Manager 1810 veya üzeri) gerektirir)
  - WSUS 6,2 ve 6,3 (Windows Server 2012 ve Windows Server 2012 R2 'deki rol)
    - [Kb 3095113 ve kb 3159706 (veya eşdeğer bir güncelleştirme)](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012) WSUS 6,2 ve 6,3 üzerine yüklenmelidir.

- Sinyal Saptama’yı etkinleştirin. Windows 10 bakımı panosunda gösterilen veriler bulma kullanılarak tespit edilir. Sinyal saptama hakkında daha fazla bilgi için bkz. [Sinyal Saptamayı Yapılandırma](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).

    Aşağıdaki Windows 10 kanal ve derleme bilgileri aşağıdaki özniteliklerde bulunur ve depolanır:  

    - **Işletim sistemi hazırlık dalı**: işletim sistemi kanalını belirtir. Örneğin, **0** = yarı yıllık kanal hedefli (güncelleştirmeleri erteleyin), **1** = yarı yıllık kanal (güncelleştirmeleri ertele), **2** = uzun vadeli bakım kanalı (ltsc)

    - **Işletim sistemi derlemesi**: işletim sistemi derlemesini belirtir. Örneğin, **10.0.10240** (RTM) veya **10.0.10586** (sürüm 1511)

- Windows 10 Bakımı panosundaki verileri görmek için hizmet bağlantı noktası yüklenmeli ve **çevrimiçi, kalıcı bağlantı** modu için yapılandırılmış olmalıdır. Çevrimdışı moddayken, Configuration Manager bakım güncelleştirmeleri yapana kadar Panoda veri güncelleştirmelerini görmezsiniz. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../../core/servers/deploy/configure/about-the-service-connection-point.md).

- Configuration Manager konsolunu çalıştıran bilgisayarda Internet Explorer 9 veya üzeri bir sürümü yüklü olmalıdır.

- Yazılım güncelleştirmeleri yapılandırılmalı ve eşitlenmelidir. Configuration Manager konsolunda herhangi bir Windows 10 özellik yükseltmesinin kullanılabilir olması için **yükseltmeler** sınıflandırmasını seçin ve yazılım güncelleştirmelerini eşitler. Daha fazla bilgi için bkz. [yazılım güncelleştirme yönetimi Için hazırlanma](../../sum/get-started/prepare-for-software-updates-management.md).

- Configuration Manager sürüm 1902 ' den başlayarak, ortamınız için uygun olduğundan emin olmak için **özellik güncelleştirmeleri için iş parçacığı önceliği belirtin** [istemci ayarını](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) doğrulayın.

- Configuration Manager sürüm 1906 ' den başlayarak, ortamınız için uygun olduğundan emin olmak için **özellik güncelleştirmeleri Için dinamik güncelleştirmeyi etkinleştir** [istemci ayarını](../../core/clients/deploy/about-client-settings.md#bkmk_du) doğrulayın. <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a>Windows 10 Bakımı panosu

Windows 10 bakımı panosu ortamınızdaki Windows 10 bilgisayarlar, etkin bakım planları, uyumluluk bilgileri ve benzeri bilgiler verir. Windows 10 bakımı panosundaki veriler Hizmet Bağlantı Noktasının yüklü olup olmadığına bağlıdır. Pano aşağıdaki kutucuklara sahiptir:

- **Windows 10 kullanım kutucuğu**: Windows 10 ' un ortak Derlemeleriyle bir döküm sağlar. Windows Insiders derlemeleri, siteniz için henüz bilinen derlemeler ve **diğer** tüm yapılar olarak listelenir. Hizmet bağlantı noktası, Windows derlemeleri hakkında bilgilendiren meta verileri indirir ve ardından bu veriler bulma verileriyle karşılaştırılır.

- **Windows 10 halkaları kutucuğu**: Kanal ve hazırlık durumuna göre Windows 10 ' un dökümünü sağlar. LTSC segmenti tüm LTSC sürümlerini içerir. İlk kutucuk belirli sürümlerin ölçeğini keser, örneğin, Windows 10 LTSC 2015.

- **Hizmet planı kutucuğu oluştur**: bir bakım planı oluşturmanın hızlı bir yolunu sağlar. Ad, koleksiyon (yalnızca boyuta göre ilk 10 koleksiyonu, en küçüğü), dağıtım paketini (yalnızca en son değiştiren en son 10 paketi gösterir) ve hazırlık durumunu belirtirsiniz. Varsayılan değerler diğer ayarlar için kullanılır. Tüm hizmet planı ayarlarını yapılandırabileceğiniz bakım planı oluşturma sihirbazını başlatmak için **Gelişmiş ayarlar** ' a tıklayın.

- **Süresi doldu kutucuğu**: Bir Windows 10 derlemesinde kullanım ömrü geçmiş cihazların yüzdesini görüntüler. Configuration Manager, hizmet bağlantı noktasının indirdiği meta verilerden alınan yüzdeyi belirler ve bulma verileriyle karşılaştırır. Kullanım ömrü geçmiş bir derleme, güvenlik güncelleştirmelerini içeren aylık toplu güncelleştirmeleri artık almıyor. Bu kategorideki bilgisayarlar sonraki derleme sürüme yükseltilmelidir. Configuration Manager bir sonraki tam sayıya yuvarlar. Örneğin, 10.000 bilgisayarınız varsa ve yalnızca bir süre dolmuşsa, kutucuk %1 ' i görüntüler.

- **Yakında Sona Erecek kutucuğu**: **Süresi doldu** kutucuğuna benzer şekilde, bir derlemede süresi yakında (yaklaşık dört ay içinde) sona erecek bilgisayarların yüzdesini gösterir. Configuration Manager bir sonraki tam sayıya yuvarlar.

- **Uyarılar kutucuğu**: Etkin uyarıları gösterir.

- **Hizmet planı İzleme kutucuğu**: oluşturduğunuz bakım planlarını ve her biri için uyumluluk grafiğini görüntüleyin. Bu kutucuk, bakım planı dağıtımlarının geçerli durumuna hızlı bir genel bakış sağlar. Önceki bir dağıtım halkası uyumluluk beklentilerinizi karşılıyorsa, daha sonraki bir bakım planını (dağıtım halkası) seçebilir ve bakım planı kurallarının otomatik olarak başlatılmasını beklemek yerine **Şimdi Dağıt** ’a tıklayabilirsiniz.

- **Windows 10 derlemeleri kutucuğu**: Display, şu anda yayınlanmış olan Windows 10 yapılarına genel bakış sağlayan ve derlemelerin farklı durumlara ne zaman geçeceğiyle ilgili genel bir fikir veren bir sabit görüntü zaman çizgisi. [Ürün yaşam döngüsü panosunda](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md)daha ayrıntılı bilgi sunulduğundan bu kutucuk Configuration Manager sürüm 1902 ' den itibaren kaldırılmıştır. <!--3446861-->

> [!IMPORTANT]
> Windows 10 bakımı panosunda gösterilen bilgiler (örneğin, Windows 10 sürümleri için destek yaşam döngüsü) size kolaylık sağlamak için verilir ve yalnızca şirketinizin içinde kullanıma yöneliktir. Güncelleştirme uyumluluğunu onaylamak için bu bilgilere güvenmemelisiniz. Size verilen bilgilerin doğruluğunu kontrol edin.

## <a name="drill-through-required-updates"></a>Gerekli güncelleştirmeler arasında detaya gitme
<!--4224414-->
*(Sürüm 1906 ' de tanıtılmıştır)*

Hangi cihazların belirli bir Windows 10 Özellik Güncelleştirmesi gerektirdiğini görmek için uyumluluk istatistikleri detayına gidebilirsiniz. Cihaz listesini görüntülemek için, cihazların ait olduğu güncelleştirmeleri ve koleksiyonları görüntülemek için izninizin olması gerekir. Cihaz listesinin detayına gitmek için:

1.  > **Tüm Windows 10 güncelleştirmelerine**bakım sağlamak için **yazılım kitaplığı** > **Windows 10**' a gidin.
1. En az bir cihaz için gerekli olan herhangi bir güncelleştirmeyi seçin.
1. **Özet** sekmesine bakın ve **İstatistikler**altında Pasta grafiğini bulun.
1. Cihaz listesinin detayına gitmek için pasta grafiğinin yanındaki **gereken köprüyü görüntüle** ' yi seçin.
1. Bu eylem sizi, güncelleştirme gerektiren cihazları görebileceğiniz **cihazlarda** geçici bir düğüme götürür. Ayrıca, bir düğüm için, listeden yeni koleksiyon oluşturma gibi işlemler gerçekleştirebilirsiniz.

## <a name="servicing-plan-workflow"></a>Bakım planı iş akışı

Configuration Manager içindeki Windows 10 bakım planları, yazılım güncelleştirmeleri için otomatik dağıtım kurallarına çok benzer. Configuration Manager değerlendiren aşağıdaki ölçütlere sahip bir bakım planı oluşturursunuz:

- **Yükseltmeler sınıflandırması**: Yalnızca **Yükseltmeler** sınıflandırmasındaki güncelleştirmeler değerlendirilir.

- **Hazırlık durumu**: Bakım planında tanımlanan hazırlık durumu, yükseltmenin hazırlık durumu ile karşılaştırılır. Hizmet bağlantı noktası güncelleştirmeleri denetlediğinde yükseltmenin meta verileri alınır.

- **Zaman erteleme**: Bakım planında **Microsoft yeni bir yükseltme yayımladıktan sonra ortamınıza dağıtmak için kaç gün beklemek istersiniz** için belirttiğiniz gün sayısı. Geçerli tarih, Yayın tarihi ve yapılandırılan gün sayısından sonra ise, dağıtıma bir yükseltme dahil edilip edilmeyeceğini değerlendirir Configuration Manager.

  Bir yükseltme ölçütleri karşıladığında bakım planı yükseltmeyi dağıtım paketine ekler, paketi dağıtım noktalarına dağıtır ve bakım planında yapılandırdığınız ayarlara göre yükseltmeyi koleksiyona dağıtır. Dağıtımları Windows 10 Bakım Panosundaki Bakım Planı İzleme bölümünden izleyebilirsiniz. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini izleme](../../sum/deploy-use/monitor-software-updates.md).

> [!NOTE]
> **Windows 10, sürüm 1903 ve üzeri,** **Windows 10** ürününün önceki sürümleri gibi bir parçası olmak yerine kendi ürünü olarak Microsoft Update eklenmiştir. Bu değişiklik, istemcilerinizin bu güncelleştirmeleri görmesini sağlamak için birkaç el ile adım uygulamanızı sağlar. Configuration Manager sürüm 1906 ' de yeni ürün için gerçekleştirmeniz gereken el ile adım sayısını azaltmaya yardımcı oluyoruz. Daha fazla bilgi için bkz. [Windows 10 sürümleri için ürünleri yapılandırma](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later).<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Windows 10 bakım planı

Windows 10 yarı yıllık kanalını dağıtırken, ortamınızda istediğiniz dağıtım halkalarını tanımlamak için bir veya daha fazla bakım planı oluşturabilir ve ardından bunları Windows 10 bakım panosunda izleyebilirsiniz. Bakım planları yalnızca **Yükseltmeler** yazılım güncelleştirmeleri sınırlandırmasını kullanır; Windows 10 için toplu güncelleştirmeleri kullanmaz. Bu güncelleştirmeler için yine de yazılım güncelleştirmeleri iş akışını kullanarak dağıtmanız gerekir. Bir bakım planıyla son kullanıcı deneyimi, bakım planında yapılandırdığınız ayarlar dahil olmak üzere yazılım güncelleştirmelerinde olduğu gibidir.  

> [!NOTE]
> Her bir Windows 10 derlemesi için yükseltme dağıtmak üzere bir görev dizisi kullanabilirsiniz, ancak bu işlem daha fazla el ile iş gerektirir. Güncelleştirilmiş kaynak dosyalarını işletim sistemi yükseltme paketi olarak içe aktarmanız ve ardından görev dizisini oluşturup uygun bilgisayar kümesine dağıtmanız gerekir. Ancak, bir görev dizisi dağıtım öncesi ve dağıtım sonrası eylemleri gibi özelleştirilmiş ek seçenekler sağlar.

Windows 10 bakım panosundan temel bir bakım planı oluşturabilirsiniz. Ad, koleksiyon (yalnızca boyuta göre ilk 10 koleksiyonu görüntüler), dağıtım paketi (yalnızca en son değiştirilen ilk 10 paketi gösterir) ve hazırlık durumu ' nu belirttikten sonra, Configuration Manager diğer ayarlar için varsayılan değerlerle bakım planını oluşturur. Ayrıca, tüm ayarları yapılandırmak için Bakım Planı Oluşturma sihirbazını başlatabilirsiniz. Bakım Planı Oluşturma sihirbazını kullanarak bir bakım planı oluşturmak için aşağıdaki yordamı kullanın.  

> [!NOTE]  
> Yüksek riskli dağıtımlar için davranışı yönetebilirsiniz. Yüksek riskli dağıtım otomatik olarak yüklenen ve istenmeyen sonuçlara neden olabilecek bir dağıtımıdır. Örneğin, amacı **Gerekli** olup bir Windows 10 dağıtan bir görev dizisi, yüksek riskli dağıtım olarak kabul edilir. Daha fazla bilgi için bkz. [yüksek riskli dağıtımları yönetme ayarları](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

### <a name="to-create-a-windows-10-servicing-plan"></a>Windows 10 bakım planı oluşturmak için

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.

1. Yazılım Kitaplığı çalışma alanında **Windows 10 Bakımı**’nı genişletin ve ardından **Bakım Planları**’na tıklayın.

1. **Giriş** sekmesinin **Oluştur** grubunda **Bakım Planı Oluştur**'a tıklayın. Bakım Planı Oluşturma Sihirbazı açılır.

1. **Genel** sayfasında, aşağıdaki ayarları yapılandırın:

    - **Ad**: Bakım planının adını belirtin. Ad benzersiz olmalıdır, kuralın hedefini açıklamaya yardımcı olur ve Configuration Manager sitesinde başkalarından ayırt edilebilir.

    - **Açıklama**: Bakım planı için bir açıklama belirtin. Açıklama, bakım planına genel bir bakış ve Configuration Manager sitedeki diğer kullanıcılarla planı belirlemek ve ayırt etmeye yardımcı olan diğer ilgili bilgileri sağlamalıdır. Açıklama alanı isteğe bağlıdır, 256 karakter limiti vardır ve varsayılan olarak boş değere sahiptir.

1. Bakım planı sayfasında, **hedef koleksiyonu**belirtin. Koleksiyonun üyeleri bakım planında tanımlanan yazılım Windows 10 yükseltmelerini alır.

    - Bakım planı gibi yüksek riskli bir dağıtım dağıttığınızda, **Koleksiyon Seç** penceresinde yalnızca sitenin özelliklerinde yapılandırılmış dağıtım doğrulama ayarlarını karşılayan özel koleksiyonlar görüntülenir.

    - Yüksek riskli dağıtımlar her zaman özel koleksiyonlar, oluşturduğunuz koleksiyonlar ve yerleşik **Bilinmeyen Bilgisayarlar** koleksiyonu ile sınırlıdır. Yüksek riskli dağıtım oluşturduğunuzda, **Tüm sistemler**gibi yerleşik bir koleksiyon seçemezsiniz. Yapılandırılan en büyük boyuttan daha az istemci içeren tüm özel koleksiyonları görmek için **sitenin en düşük boyut yapılandırmasından daha büyük bir üye sayısına sahip koleksiyonları Gizle** seçeneğinin işaretini kaldırın. Daha fazla bilgi için bkz. [yüksek riskli dağıtımları yönetme ayarları](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

    - Dağıtım doğrulama ayarları, koleksiyonu geçerli üyeliğine bağlıdır. Bakım planını dağıttıktan sonra, yüksek riskli dağıtım ayarları için koleksiyon üyeliği yeniden değerlendirilmez.

      - Örneğin, **varsayılan boyutu** 100 olarak, **en büyük boyutu** 1000 olarak ayarlayadığınızı varsayalım. Yüksek riskli bir dağıtım oluşturduğunuzda **Koleksiyon Seç** penceresinde yalnızca 100 ' den az istemci içeren koleksiyonlar görüntülenir. **Üye sayısı sitenin en düşük boyut yapılandırmasından daha büyük olan koleksiyonları Gizle** ayarını temizlerseniz, pencerede 1000 ' den az istemci içeren koleksiyonlar gösterilir.  
      Site rolü içeren bir koleksiyon seçtiğinizde, aşağıdaki ölçütler geçerlidir:
        - Koleksiyon bir site sistem sunucusu içeriyorsa ve dağıtım doğrulama ayarlarında site sistem sunucularıyla koleksiyonları engelleyecek şekilde yapılandırırsanız bir hata oluşur ve devam edebilirsiniz.
        - Bir koleksiyon site sistem sunucusu içeriyorsa ve dağıtım doğrulama ayarlarında site sistem sunucularına sahip koleksiyonların varsayılan boyut değerini aşması veya koleksiyonun bir sunucu içermesi durumunda sizi uyaracak şekilde yapılandırırsanız, Yazılım Dağıtma Sihirbazı yüksek risk uyarısı gösterir. Yüksek riskli dağıtım oluşturmayı kabul etmeniz gerekir ve bir durum mesajı oluşturulur.

1. Dağıtım Halkası sayfasında aşağıdaki ayarları yapılandırın:

   - **Bu bakım planının uygulanacağı Windows hazır olma durumunu belirtin**: aşağıdaki seçeneklerden birini belirleyin:

      - **Yarı yıllık kanal (hedefli)**: Bu bakım modelinde, Microsoft tarafından yayımlandığında özellik güncelleştirmeleri kullanılabilir.

      - **Yarı yıllık kanal**: Bu bakım kanalı genellikle geniş dağıtım için kullanılır. Yarı yıllık kanaldaki Windows 10 istemcileri, daha sonra yalnızca daha sonraki bir zamanda hedeflenen kanalda bulunan bu cihazlarla aynı Windows 10 derlemesini alır.

        Kanallarda bakım yapma hakkında daha fazla bilgi için bkz. [bakım kanalları](/windows/deployment/update/waas-overview#servicing-channels).

   - **Microsoft yeni bir yükseltme yayımladıktan sonra, ortamınızda dağıtım yapmadan önce kaç gün beklemek**istiyorsunuz: geçerli tarih, yayın tarihinden sonra, bu ayar için yapılandırdığınız gün sayısından sonra Configuration Manager, dağıtıma bir yükseltme dahil edilip edilmeyeceğini değerlendirir.

1. Yükseltmeler sayfasında, hizmet planına eklenen yükseltmeleri filtrelemek için arama ölçütlerini yapılandırın. Yalnızca belirtilen ölçütlere uyan yükseltmeler ilişkili dağıtıma eklenir. Aşağıdaki özellik filtreleri kullanılabilir: <!--3098809, 3113836, 3204570 -->

   - **Mimari** (sürüm 1810 ' den başlayarak)
   - **Dil**
   - **Ürün kategorisi** (sürüm 1810 ' den başlayarak)
   - **Gerekli**
      > [!IMPORTANT]
      > Arama ölçütlerinizin bir parçası olarak, **gerekli** alanı **>= 1**değeriyle ayarlamanızı öneririz. Bu ölçütleri kullanmak, hizmet planına yalnızca geçerli güncelleştirmelerin eklenmesini sağlar.
   - **Yenisiyle değiştirildi** (sürüm 1810 ' den başlayarak)
   - **Başlık**

    Belirtilen ölçütleri karşılayan yükseltmeleri görüntülemek için **Önizleme** ’ye tıklayın.

1. Dağıtım Zamanlaması sayfasında, aşağıdaki ayarları yapılandırın:

   - **Değerlendirmeyi zamanla**: CONFIGURATION Manager, UTC 'yi veya Configuration Manager konsolunu çalıştıran bilgisayarın yerel saatini kullanarak, kullanılabilir saat ve yükleme son tarih zamanlarını belirleyip değerlendirmeyeceğini belirtin.

       > [!NOTE]
       > **Yazılım kullanılabilir saati** veya **yükleme son tarihi**için yerel zamanı ve ardından mümkün olan en **kısa sürede** ' yi seçtiğinizde, güncelleştirmelerin ne zaman kullanılabilir olduğunu veya bir istemcide ne zaman yüklendiğini değerlendirmek için Configuration Manager konsolunu çalıştıran bilgisayardaki geçerli zaman kullanılır. İstemci farklı bir zaman dilimindeyse bu eylemler, istemcinin saati değerlendirme saatine ulaştığında gerçekleşir.

   - **Yazılım uygunluk saati**: Yazılım güncelleştirmelerinin istemciler için ne zaman kullanılabilir olduğunu belirtmek için aşağıdaki ayarlardan birini seçin:

        - **Mümkün olan en kısa sürede**: Dağıtımdaki yazılım güncelleştirmelerinin istemci bilgisayarlar için hemen kullanılabilir olması için bu ayarı seçin. Dağıtımı bu ayar seçili olarak oluşturduğunuzda, Configuration Manager istemci ilkesini güncelleştirir. Ardından, bir sonraki istemci ilkesi yoklama döngüsünün, istemcileri dağıtımın farkında olur ve yükleme için mevcut güncelleştirmeleri elde edebilir.

        - **Belirli bir zamanda**: Dağıtımdaki yazılım güncelleştirmelerinin istemci bilgisayarlar için belirli bir tarih ve saatte kullanılabilir olması için bu ayarı seçin. Bu ayar etkinken dağıtımı oluşturduğunuzda Configuration Manager istemci ilkesini güncelleştirir. Ardından, sonraki istemci ilkesi yoklama döngüsünde istemciler dağıtımdan haberdar edilir. Ancak, Dağıtımdaki yazılım güncelleştirmeleri, yapılandırılan tarih ve saate kadar, yükleme için kullanılamaz.

   - **Yükleme son tarihi**: Dağıtımdaki yazılım güncelleştirmeleri için yükleme son tarihini belirtmek üzere aşağıdaki ayarlardan birini seçin:

        - **Mümkün olan en kısa sürede**: Dağıtımdaki yazılım güncelleştirmelerinin mümkün olan en kısa sürede otomatik olarak yüklenmesi için bu ayarı seçin.

        - **Belirli bir zamanda**: Dağıtımdaki yazılım güncelleştirmelerini belirli bir tarih ve saatte otomatik olarak yüklemek için bu ayarı seçin. Configuration Manager, yapılandırılmış **belirli zaman** aralığını **Yazılım kullanılabilir zamanına**ekleyerek yazılım güncelleştirmelerinin yükleneceği son tarihi belirler.

           > [!NOTE]
           > Gerçek yükleme son tarih zamanı, görüntülenen son tarih saati artı 2 saate kadar rasgele bir zaman miktarıdır. Bunun yapılması, dağıtımda aynı anda güncelleştirmeleri yükleyen hedef koleksiyondaki tüm istemci bilgisayarların olası etkisini azaltır.
           >
           > **Bilgisayar Aracısı** istemci ayarını, gerekli güncelleştirmeler için yükleme rastgele gecikmesini devre dışı bırakmak için **Rastgele son tarih seçimini devre dışı bırak** olarak yapılandırabilirsiniz. Daha fazla bilgi edinmek için bkz. [Bilgisayar Aracısı](../../core/clients/deploy/about-client-settings.md#computer-agent).

        - **Bu dağıtımın uygulanmasını, istemci üzerinde tanımlanan yetkisiz kullanım süresine kadar kullanıcı tercihlerine göre geciktir**: [ **dağıtım son tarihi (saat) istemci ayarından sonra zorlama için yetkisiz kullanım süresini** ](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours)dikkate almak üzere bu seçeneği belirleyin.

1. Kullanıcı Deneyimi sayfasında, aşağıdaki ayarları yapılandırın:  

    - **Kullanıcı bildirimleri**: İstemci bilgisayarda yapılandırılmış **Yazılım uygunluk saati** 'nde Yazılım Merkezinde güncelleştirme bildirimlerinin görüntülenip görüntülenmeyeceğini ve istemci bilgisayarlarda kullanıcı bildirimlerinin görüntülenip görüntülenmeyeceğini belirtin.

    - **Son tarih davranışı**: Güncelleştirme dağıtımı için son tarihe gelindiğinde gerçekleşecek davranışı belirtin. Dağıtımda güncelleştirmelerin yüklenip yüklenmeyeceğini belirtin. Ayrıca, güncelleştirme yüklemesi sonrasında, yapılandırılmış bakım penceresini dikkate almaksızın sistemin yeniden başlatılıp başlatılmayacağını belirtin. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  

    - **Cihaz yeniden başlatma davranışı**: Güncelleştirmeler yüklendikten sonra ve yüklemeyi tamamlamak için sistemin yeniden başlaması gerektiğinde, sunucularda ve iş istasyonlarında sistemin yeniden başlatılmasının engellenip engellenmeyeceğini belirtin.

    - **Windows Embedded cihazlar için filtre işleme yaz**: Yazma filtresi etkinleştirilmiş Windows Embedded cihazlara güncelleştirmeleri dağıtırken, güncelleştirmeyi geçici katmana yüklemeyi ve değişiklikleri daha sonra yapmayı veya değişiklikleri yükleme son tarihinde veya bakım penceresi sırasında yapmayı belirtebilirsiniz. Yükleme son tarihinde veya bakım penceresi sırasında değişiklik yaparsanız, yeniden başlatma gerekir ve değişiklikler aygıtta kalır.
        - Windows Embedded cihazına bir güncelleştirme dağıttığınızda, aygıtın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun.

    - **Yazılım güncelleştirmeleri dağıtımı yeniden başlatma sırasında yeniden değerlendirme davranışı**: yeniden başlattıktan sonra başka bir güncelleştirme dağıtımı değerlendirme döngüsünü zorlamak için, **Bu dağıtımdaki herhangi bir güncelleştirme sistemin yeniden başlatılmasını gerektiriyorsa, yeniden başlatmadan sonra güncelleştirmeleri dağıtım değerlendirme döngüsünü Çalıştır**seçeneğini belirleyin.

1. Dağıtım paketi sayfasında, mevcut bir dağıtım paketi seçin, dağıtım paketi yok veya aşağıdaki ayarları yapılandırarak yeni bir dağıtım paketi oluşturun:

    1. **Ad**: Dağıtım paketinin adını belirtin. Bu ad benzersiz olmalıdır ve paket içeriğini açıklar. 50 karakterle sınırlıdır.

    1. **Açıklama**: Dağıtım paketiyle ilgili bilgi sağlayan bir açıklama belirtin. Açıklama 127 karakterle sınırlıdır.

    1. **Paket kaynağı**: Yazılım güncelleştirmesi kaynak dosyalarının konumunu belirtir. Kaynak konumu için bir ağ yolu yazın, örneğin ** \\\Server\\PaylaşımAdı\\yol**veya ağ konumunu bulmak için **göz at** ' a tıklayın. Sonraki sayfaya geçmeden önce dağıtım paketi kaynak dosyaları için paylaşılan klasör oluşturun.
        - Belirttiğiniz dağıtım paketi kaynak konumu başka bir yazılım dağıtım paketi tarafından kullanılamaz.
        - SMS Sağlayıcısı bilgisayar hesabı ve yazılım güncelleştirmelerini indirmek için sihirbazı çalıştıran kullanıcı, indirme konumunda **Yazma** NTFS izinlerine sahip olmalıdır. Yazılım güncelleştirme kaynak dosyalarıyla saldırganların izinsiz değiştirilme riskini azaltmak için indirme konumuna erişimi dikkatle kısıtlamalısınız.
        - Dağıtım paketini Configuration Manager oluşturulduktan sonra dağıtım paketi özelliklerinde paket kaynak konumunu değiştirebilirsiniz. Ancak bunu yaparsanız, öncelikle özgün paket kaynağındaki içeriği yeni paket kaynak konumuna kopyalamanız gerekir.

    1. **Gönderme önceliği**: Dağıtım paketi için gönderme önceliğini belirtin. Configuration Manager, paketi dağıtım noktalarına gönderdiğinde dağıtım paketi için gönderme önceliğini kullanır. Dağıtım paketleri öncelik sırasıyla gönderilir: yüksek, orta veya düşük. Benzer önceliklere sahip paketler oluşturulma sıralarına göre gönderilir. Biriktirme listesi yoksa, paket önceliğe bakılmaksızın hemen işlenir.

    1. **İkili değişiklik çoğaltmasını etkinleştir**: ikili değişiklik çoğaltmasını kullanmak istiyorsanız bu seçeneği etkinleştirin.

1. Dağıtım noktaları sayfasında, güncelleştirme dosyalarını barındıran dağıtım noktalarını veya dağıtım noktası gruplarını belirtin. Dağıtım noktaları hakkında daha fazla bilgi için bkz. [dağıtım noktası yapılandırma](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).

    > [!NOTE]
    > Bu sayfa sadece yeni yazılım güncelleştirme dağıtım paketi oluşturduğunuzda kullanılabilir.  

1. Yükleme Konumu sayfasında güncelleştirme dosyalarının internetten mi yoksa yerel ağınızdan mı yükleneceğini belirtin. Aşağıdaki ayarları yapılandırın:

    - **Yazılım güncelleştirmelerini İnternet’ten indir**: Güncelleştirmeleri İnternet’te belirtilen konumdan yüklemek için bu ayarı seçin. Bu ayar, varsayılan olarak etkinleştirilmiştir.

    - **Yazılım güncelleştirmelerini yerel ağdaki bir konumdan indir**: Güncelleştirmeleri yerel bir dizinden veya paylaşılan ağ klasöründen indirmek için bu ayarı kullanın. Bu ayar, Sihirbazı çalıştıran bilgisayarın Internet erişimi olmadığında yararlıdır. İnternet erişimi olan herhangi bir bilgisayar güncelleştirmeleri indirebilir ve bunları sihirbazı çalıştıran bilgisayarda erişilebilen yerel ağdaki bir konumda saklar.

1. Dil Seçimi sayfasında seçilen güncelleştirmelerin yükleneceği dili seçin. Güncelleştirmeler yalnızca seçili dillerde kullanılabilir olmaları durumunda indirilir. Dile özgü olmayan güncelleştirmeler daima indirilir. Varsayılan olarak, sihirbaz, yazılım güncelleştirme noktası özelliklerinde yapılandırdığınız dilleri seçer. Sonraki sayfaya geçmeden önce en az bir dil seçilmelidir. Yalnızca bir güncelleştirme tarafından desteklenmeyen dilleri seçtiğinizde, güncelleştirme için indirme başarısız olur.

1. Özet sayfasında ayarları gözden geçirin ve **İleri** 'ye tıklayarak bakım planını oluşturun.  

Sihirbazı tamamladıktan sonra bakım planı çalışacaktır. Belirtilen kriterleri karşılayan güncelleştirmeleri yazılım güncelleştirme grubuna ekler, güncelleştirmeleri site sunucusundaki içerik kitaplığına yükler, güncelleştirmeleri yapılandırılan dağıtım noktalarına dağıtır ve ardından yazılım güncelleştirme grubunu hedef koleksiyondaki istemcilere dağıtır.

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a>Bakım planını değiştirme

Windows 10 bakım panosundan temel bir bakım planı oluşturduktan sonra veya var olan bir bakım planının ayarlarını değiştirmeniz gerekiyorsa, bakım planının özelliklerine gidebilirsiniz.

> [!NOTE]
> Bakım planı oluştururken sihirbazda kullanılamayan bakım planına yönelik özelliklerde ayarları yapılandırabilirsiniz. Sihirbaz, aşağıdakiler için ayarlar için varsayılan ayarları kullanır: indirme ayarları, dağıtım ayarları ve uyarılar.  

Bir bakım planının özelliklerini değiştirmek için aşağıdaki yordamı kullanın. 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Bakım planının özelliklerini değiştirmek için

1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.

1. Yazılım Kitaplığı çalışma alanında **Windows 10 Bakımı**' nı genişletin, **bakım planları**' na tıklayın ve ardından değiştirmek istediğiniz bakım planını seçin.

1. **Giriş** sekmesinde **Özellikler** ’e tıklayarak seçili bakım planının özelliklerini açın.

    Aşağıdaki ayarlar, sihirbazda yapılandırılmayan bakım planı özelliklerinde mevcuttur:

    **Dağıtım ayarları**: dağıtım ayarları sekmesinde, aşağıdaki ayarları yapılandırın:

    - **Gerekli dağıtımlarda istemcileri uyandırmak için LAN'da Uyandırma'yı kullan**: Son tarihte, dağıtımdaki bir veya daha fazla yazılım güncelleştirmesini gerektiren bilgisayarlara uyandırma paketleri göndermek üzere LAN'da Uyandırma özelliğinin etkinleştirilip etkinleştirilmeyeceğini belirtin. Yükleme son tarihinde uyku modunda olan tüm bilgisayarlar, yazılım güncelleştirme yüklemesinin başlatabilmesi için başlatılabilmesi uyandırılır. Dağıtımda yazılım güncelleştirmesi gerektirmeyen uyku modundaki istemciler başlatılmaz. Varsayılan olarak bu ayar etkin değildir.

        > [!WARNING]
        > Bu seçeneği kullanabilmeniz için, bilgisayarlar ve ağlar Ağ Üzerinde Etkin için yapılandırılmalıdır.

    - **Ayrıntı düzeyi**: İstemci bilgisayarlar tarafından bildirilen durum iletileri için ayrıntı düzeyini belirtin.

    **Ayarları indir**: indirme ayarları sekmesinde aşağıdaki ayarları yapılandırın:

    - İstemci yavaş bir ağa bağlıyken veya bir geri dönüş içerik konumu kullanırken, istemcinin yazılım güncelleştirmelerini indirip indirmeyeceğini ve yükleyip yüklemediği belirtin.

    - Yazılım güncelleştirmelerinin içeriği tercih edilen bir dağıtım noktasında mevcut olmadığında istemcinin geri dönüş dağıtım noktasından yazılım güncelleştirmelerini indirip indirmeyeceğini ve yüklemesini belirtin.

    - **İstemcilerin aynı alt ağdaki diğer istemcilerle içerik paylaşmasına izin ver**: İçerik yüklemeleri için BranchCache kullanımının etkinleştirilip etkinleştirilmeyeceğini belirtin. BranchCache hakkında daha fazla bilgi için bkz. [içerik yönetimi Için temel kavramlar](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

    - Dağıtım noktalarında yazılım güncelleştirmeleri yoksa, istemcilerin Microsoft Update yazılım güncelleştirmelerini indirip indirmeyeceğini belirtin.
        > [!IMPORTANT]
        > Windows 10 bakım güncelleştirmeleri için bu ayarı kullanmayın. Configuration Manager (en azından sürüm 1610), Microsoft Update Windows 10 bakım güncelleştirmelerini indiremez.

    - Tarifeli internet bağlantısı kullanılırken istemcilerin yükleme son tarihinden sonra yükleme yapmasına izin verip vermeyeceğinizi belirtin. Tarifeli Internet bağlantısında olduğunuzda, Internet sağlayıcıları bazen gönderdiğiniz ve aldığınız veri miktarına göre ücret uygular.

    **Uyarılar**: uyarılar sekmesinde, bu dağıtım için Configuration Manager ve System Center Operations Manager uyarı oluşturma şeklini yapılandırın.
    - Son yazılım güncelleştirme uyarılarını **Yazılım Kitaplığı** çalışma alanındaki **Yazılım Güncelleştirmeleri** düğümünde gözden geçirebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz. [hizmet olarak Configuration Manager Temelleri ve hizmet olarak Windows](../../core/understand/configuration-manager-and-windows-as-service.md).
