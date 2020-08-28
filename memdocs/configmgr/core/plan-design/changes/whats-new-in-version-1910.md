---
title: Sürüm 1910’daki yenilikler
titleSuffix: Configuration Manager
description: Geçerli dalın Configuration Manager sürüm 1910 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c99716070bf32ae27a7bd8b7a114d8b920814e2
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993480"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Geçerli dalın Configuration Manager sürüm 1910 ' deki yenilikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme 1910, konsol içi bir güncelleştirme olarak sunulmaktadır. Sürüm 1806 veya üstünü çalıştıran sitelerde bu güncelleştirmeyi uygulayın. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Bu makalede Configuration Manager, sürüm 1910 ' deki değişiklikler ve yeni özellikler özetlenmektedir.

Bu güncelleştirmeyi yüklemek için her zaman en son denetim listesini gözden geçirin. Daha fazla bilgi için bkz. [güncelleştirme 1910 yükleme denetim listesi](../../servers/manage/checklist-for-installing-update-1910.md). Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist)de gözden geçirin.

Yeni Configuration Manager özelliklerinden tam olarak yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme de güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

> [!TIP]
> Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a> Microsoft uç noktası Configuration Manager

<!--4960084-->

Configuration Manager artık Microsoft Endpoint Manager 'ın bir parçasıdır.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, Configuration Manager ve Intune 'U Basitleştirilmiş lisanslama ile birlikte sunar. Microsoft bulutun gücünden kendi hızınızda yararlanırken, mevcut Configuration Manager yatırımlarınızı kullanmaya devam edin.

Aşağıdaki Microsoft yönetim çözümleri artık Microsoft Endpoint Manager markasının bir parçasıdır:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../../desktop-analytics/overview.md)
- [Otomatik Pilot](/intune/enrollment/enrollment-autopilot)
- [Cihaz yönetimi yönetici konsolundaki](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760) diğer özellikler

Daha fazla bilgi için, Microsoft Kurumsal Başkan Yardımcısı Microsoft 365 atacan Anderson 'tan aşağıdaki gönderilere bakın:

- [Duyuru blog gönderisi](https://aka.ms/cmannounce)
- [Vizyon kağıdı](https://aka.ms/MEMVisionPaper)
- [Duyuru Özeti videosu](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Microsoft Uç Nokta Yöneticisi ile Configuration Manager hangi şeyler değişir?

Sürüm 1910 ' de, ad değişikliğinden ayrılan Configuration Manager hala aynı işlevleri görür. Bazı ad değişiklikleri aşağıdaki bileşenlerin kullanımını etkileyebilir:

- **Configuration Manager konsolu**: **Microsoft Endpoint Manager** klasöründeki Windows Başlat menüsünün altındaki konsola ve **Uzaktan denetim görüntüleyicisine** kısayollar bulun.

- **Yazılım Merkezi**: **Microsoft Endpoint Manager** klasöründe Windows Başlat menüsünün altında yazılım merkezi kısayolunu bulun.

![Microsoft Uç Nokta Yöneticisi başlangıç menüsü simgeleri](media/microsoft-endpoint-manager-start-menu.png)

Bu yeni konumları dahil etmek için tuttuğunuz tüm dahili belgeleri güncelleştirdiğinizden emin olun.

> [!TIP]
> Windows 10 ' da, Başlat menüsünü açtığınızda, simgeyi bulmak için adı yazın. Örneğin `Configuration Manager` veya `Software Center` girin.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site altyapısı

### <a name="reclaim-sedo-lock"></a>SEDO kilidini geri kazan

<!--4786915-->

[Geçerli dal sürüm 1906](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)' den başlayarak, bir görev dizisinde kilidi temizleyebilirsiniz. Artık Configuration Manager konsolundaki herhangi bir nesne üzerindeki kilidi temizleyebilirsiniz.

Daha fazla bilgi için, bkz. [Configuration Manager konsolunu kullanma](../../servers/manage/admin-console.md#bkmk_sedo).

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Şirket içi siteyi genişletme ve Microsoft Azure için geçirme
<!--3556022-->

Bu yeni araç, Configuration Manager için programlı olarak Azure sanal makineleri (VM 'Ler) oluşturmanıza yardımcı olur. Bu, pasif site sunucusu, yönetim noktaları ve dağıtım noktaları gibi varsayılan ayarlar site rolleriyle yüklenebilir. Yeni rolleri doğruladıktan sonra, yüksek kullanılabilirlik için bunları ek site sistemleri olarak kullanın. Ayrıca şirket içi site sistem rolünü kaldırabilir ve yalnızca Azure VM rolünü tutabilirsiniz.

Daha fazla bilgi için bkz. [Şirket içi siteleri Microsoft Azure Için genişletme ve geçirme](../../support/azure-migration-tool.md).

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Masaüstü Analizi

Masaüstü Analizi bulut hizmetindeki aylık değişiklikler hakkında daha fazla bilgi için bkz. [Masaüstü](../../../desktop-analytics/whats-new.md)analizine ilişkin yenilikler.

## <a name="real-time-management"></a><a name="bkmk_real"></a> Gerçek zamanlı yönetim

### <a name="optimizations-to-the-cmpivot-engine"></a>CMPivot altyapısına iyileştirmeler
<!--3197353-->
CMPivot altyapısına bazı önemli iyileştirmeler ekledik. Artık, daha fazla işlemi ConfigMgr istemcisine gönderebilirsiniz. İyileştirmeler, CMPivot sorguları çalıştırmak için gereken ağ ve sunucu CPU yükünü büyük ölçüde azaltır. Bu iyileştirmelere göre, artık gigabayt 'tan fazla istemci verisi gerçek zamanlı olarak bulunabilir. 

Daha fazla bilgi için bkz. [CMPivot altyapısına iyileştirmeler](../../servers/manage/cmpivot-changes.md#bkmk_optimization).

### <a name="additional-cmpivot-entities-and-enhancements"></a>Ek CMPivot varlıkları ve geliştirmeleri
<!--5410930-->
Sorun giderme ve avlamaya yardımcı olmak için çeşitli yeni CMPivot varlıkları ve varlık geliştirmeleri ekledik. Sorgulamak için aşağıdaki varlıkları ekledik:

- Windows olay günlükleri ([WinEvent](../../servers/manage/cmpivot-changes.md#bkmk_WinEvent))
- Dosya içeriği ([FileContent](../../servers/manage/cmpivot-changes.md#bkmk_File))
- Süreçler tarafından yüklenen dll 'Ler ([ProcessModule](../../servers/manage/cmpivot-changes.md#bkmk_ProcessModule))
- Azure Active Directory bilgileri ([Aadstatus](../../servers/manage/cmpivot-changes.md#bkmk_AadStatus))
- Uç nokta koruma durumu ([Epstatus](../../servers/manage/cmpivot-changes.md#bkmk_EPStatus))

Bu sürüm ayrıca CMPivot için çeşitli [diğer geliştirmeler](../../servers/manage/cmpivot-changes.md#bkmk_Other) de içerir. Daha fazla bilgi için bkz. [sürüm 1910 ' den başlayarak CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1910).

## <a name="content-management"></a><a name="bkmk_content"></a> İçerik yönetimi

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Intune Win32 uygulamaları için Microsoft bağlı önbellek desteği

<!--5032900-->

Configuration Manager dağıtım noktalarınız üzerinde Microsoft bağlı önbelleğini etkinleştirdiğinizde, bu kişiler artık Microsoft Intune Win32 uygulamalarını ortak yönetilen istemcilere sunabilir.

Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği Configuration Manager](../hierarchy/microsoft-connected-cache.md#bkmk_intune).

> [!NOTE]
> Geçerli dal sürümü 1906, Windows Server 'da yüklü olan ve hala geliştirmede bulunan bir uygulama olan [ağ üzerinde dağıtım iyileştirmesi](../hierarchy/microsoft-connected-cache.md)dahil Configuration Manager. Geçerli dal sürüm 1910 ' den başlayarak, bu özellik artık Microsoft bağlı önbelleği olarak adlandırılmaktadır.
>
> Bağlı önbelleği bir Configuration Manager dağıtım noktasına yüklediğinizde, teslim Iyileştirme hizmeti trafiğini yerel kaynaklara yükler. Bağlı önbellek, içeriği bayt aralığı düzeyinde verimli bir şekilde önbelleğe alarak bu davranışı yapar.

## <a name="client-management"></a><a name="bkmk_client"></a> İstemci yönetimi

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Uyumluluk ilkesi değerlendirmesinin bir parçası olarak özel yapılandırma temellerini dahil et
<!--3608345-->

Artık Uyumluluk ilkesi değerlendirme kuralı olarak özel yapılandırma temellerinin değerlendirmesini ekleyebilirsiniz. Bir yapılandırma temeli oluşturduğunuzda veya düzenlediğinizde, artık **Bu temeli uyumluluk ilkesi değerlendirmesi kapsamında değerlendir** seçeneğini kullanabilirsiniz. Bir uyumluluk ilkesi kuralı eklediğinizde veya düzenlediğinizde, **Uyumluluk ilkesi değerlendirmesi ' nde yapılandırılmış taban çizgileri ekle**adlı bir koşulunuz vardır.

Ortak yönetilen cihazlar için ve Intune 'u, genel uyumluluk durumunun bir parçası olarak Configuration Manager uyumluluk değerlendirmesi sonuçları alacak şekilde yapılandırdığınızda, bu bilgiler Azure Active Directory gönderilir. Daha sonra, Microsoft 365 kaynaklarınıza koşullu erişim için kullanabilirsiniz.

Daha fazla bilgi için bkz. [Uyumluluk ilkesi değerlendirmesinin bir parçası olarak özel yapılandırma temelleri ekleme](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Windows 10 Enterprise çoklu oturum için kullanıcı ilkesini etkinleştir

<!--4737447-->

Configuration Manager geçerli dal sürümü 1906 [Windows sanal masaüstü](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)için destek sunmuştur. Bu Microsoft Azure ortamı, bazıları birden çok eşzamanlı etkin kullanıcı oturumuna izin veren çeşitli işletim sistemi sürümlerini destekler. Örneğin, Windows 10 Enterprise çoklu oturum, bu işletim sistemi sürümlerinden biridir.

Bu çoklu oturum cihazlarındaki Kullanıcı ilkesine ihtiyacınız varsa ve olası performans etkisini kabul ediyorsanız, artık kullanıcı ilkesini etkinleştirmek için bir istemci ayarı yapılandırabilirsiniz. **Istemci ilkesi** grubunda, **birden çok Kullanıcı oturumu Için kullanıcı ilkesini etkinleştir** ayarını yapılandırın.

Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../clients/deploy/configure-client-settings.md).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a> Uygulama yönetimi

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Microsoft Edge sürüm 77 ve üzerini dağıtma
<!--4561024-->
Tüm yeni Microsoft Edge iş için hazırlayın. Artık kullanıcılarınıza Microsoft Edge, sürüm 77 ve üzeri dağıtım yapabilirsiniz. Yöneticiler, dağıtım için Microsoft Edge istemcisinin bir sürümüyle birlikte Beta, dev veya kararlı kanal seçebilir.

Daha fazla bilgi için bkz. [Microsoft Edge, sürüm 77 ve üstünü dağıtma](../../../apps/deploy-use/deploy-edge.md).

### <a name="improvements-to-application-groups"></a>Uygulama gruplarında iyileştirmeler

<!--4760058-->

Geçerli dal sürüm 1906 ' den başlayarak, bir cihaz koleksiyonuna tek bir dağıtım olarak gönderilmek üzere bir uygulama grubu oluşturabilirsiniz. Bu sürüm, bu özelliğin üzerine geliştirilmiştir:

- Kullanıcılar, yazılım merkezi 'nde uygulama grubu için **Kaldır** ' ı seçebilir.
- Bir uygulama grubunu bir **Kullanıcı koleksiyonuna**dağıtabilirsiniz.

Daha fazla genel bilgi için bkz. [uygulama grupları oluşturma](../../../apps/deploy-use/create-app-groups.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> İşletim sistemi dağıtımı

### <a name="improvements-to-the-task-sequence-editor"></a>Görev sırası Düzenleyicisi geliştirmeleri

 Görev sırası Düzenleyicisi aşağıdaki geliştirmeleri içerir:

- **Görev sırası düzenleyicisine ara:**<!--4621085--> Birçok grup ve adım içeren büyük bir görev diziniz varsa, belirli adımları bulmak zor olabilir. Artık görev sırası düzenleyicisinde arama yapabilirsiniz. Bu eylem görev dizisindeki adımları daha hızlı bulmanızı sağlar.
- **Görev sırası koşullarını Kopyala ve Yapıştır:**<!--4621098--> Bir görev dizisi adımından diğerine koşulları yeniden kullanmak istiyorsanız, artık görev sırası düzenleyicisinde koşulları kopyalayabilir ve yapıştırabilirsiniz.

Daha fazla bilgi için, [görev dizisi düzenleyicisini kullanma](../../../osd/understand/task-sequence-editor.md)hakkında yeni makaleye bakın.

### <a name="task-sequence-performance-improvements-power-plans"></a>Görev sırası performans iyileştirmeleri: güç planları

<!--3555926-->

Artık yüksek performanslı güç planıyla bir görev dizisi çalıştırabilirsiniz. Bu seçenek, görev dizisinin genel hızını geliştirir. Windows 'u, daha yüksek güç tüketimi masrafına en yüksek performans sunan yerleşik yüksek performanslı güç planını kullanacak şekilde yapılandırır.

Daha fazla bilgi için bkz. [güç planlarına yönelik performans iyileştirmeleri](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf).

### <a name="task-sequence-download-on-demand-over-the-internet"></a>İnternet üzerinden isteğe bağlı görev sırası indirme

<!--3601238-->

Görev sırasını, bulut yönetimi ağ geçidi (CMG) aracılığıyla bir Windows 10 yerinde yükseltme dağıtmak için kullanabilirsiniz. Ancak, görev dizisini başlatmadan önce dağıtımın tüm içeriği yerel olarak indirmesini gerektirir.

Bu sürümden itibaren, görev sırası altyapısı, içerik etkinleştirilmiş bir CMG veya bulut dağıtım noktasından isteğe bağlı paket indirebilir. Bu değişiklik, Internet tabanlı cihazlara Windows 10 yerinde yükseltme dağıtımlarınızla ek esneklik sağlar.

Daha fazla bilgi için bkz. [CMG aracılığıyla Windows 10 yerinde yükseltme dağıtımı](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-os-deployment"></a>İşletim sistemi dağıtımına yönelik iyileştirmeler

Bu sürüm, işletim sistemi dağıtımına yönelik aşağıdaki geliştirmeleri içerir.

#### <a name="boot-image-keyboard-layout"></a>Önyükleme görüntüsü klavye düzeni

<!--4910348-->

Önyükleme görüntüsü için varsayılan klavye düzeni yapılandırın. Bir önyükleme görüntüsünün **Özelleştirme** sekmesinde, yeni **WinPE 'de varsayılan klavye düzeni ayarla** seçeneğini kullanın. En-US dışında bir dil seçerseniz Configuration Manager, kullanılabilir giriş yerel ayarları 'nda hala en-US ' i içerir. Cihazda, ilk klavye düzeni seçili yerel ayar olur, ancak gerekirse Kullanıcı cihazı en-US ' a değiştirebilir.

Daha fazla bilgi için bkz. [önyükleme görüntülerini yönetme](../../../osd/get-started/manage-boot-images.md#customization).

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Bir işletim sistemi yükseltme paketinin tek bir dizinini içeri aktarma

<!--4931110-->

Bir işletim sistemi yükseltme paketini içeri aktardığınızda, **Seçilen yükseltme paketinin Install. wim dosyasındaki belirli bir görüntü dizinini Ayıkla** seçeneğini kullanabilirsiniz. Bu davranış, işletim sistemi, işletim sistemi yükseltme paketindeki var olan Install. wim dosyasını geçersiz yazmasının dışında, [Işletim sistemi görüntüleriyle](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages)aynı şekilde benzerdir. Görüntü dizinini geçici bir konuma ayıklar ve sonra özgün kaynak dizinine taşıýr.

Daha fazla bilgi için bkz. [işletim sistemi yükseltme paketlerini yönetme](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs).

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>Bir görev dizisi sırasında bir değişkene komut satırı çalıştırma adımının sonuçlarını çıkış

<!--user story 4977616/bug 4798352-->

**Komut satırını Çalıştır** adımı artık **görev dizisi değişken** seçeneğine bir çıkış içeriyor. Bu seçeneği etkinleştirdiğinizde, görev sırası komuttan çıktıyı belirttiğiniz özel bir görev sırası değişkenine kaydeder.

Daha fazla bilgi için bkz. [komut satırını çalıştırma](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine).

#### <a name="improvements-to-task-sequence-debugger"></a>Görev dizisi hata ayıklayıcısındaki geliştirmeler

Bu sürüm, görev sırası hata ayıklayıcısında aşağıdaki geliştirmeleri içerir:

- Görev dizisi bir hata döndürdüğünde hata ayıklayıcıyı otomatik olarak başlatmak için **Tsdebughatayeni** görev dizisi değişkenini kullanın.<!-- 5012536 -->
- Hata ayıklayıcıda bir kesme noktası oluşturursanız ve ardından görev sırası bilgisayarı yeniden başlatırsanız, hata ayıklayıcı yeniden başlattıktan sonra kesme noktalarını tutar.<!-- 5012509 -->

Daha fazla bilgi için bkz. [görev dizisi hata ayıklayıcısı](../../../osd/deploy-use/debug-task-sequence.md) ve [görev dizisi değişkenleri-tsdebughata.](../../../osd/understand/task-sequence-variables.md#TSDebugOnError)

#### <a name="improved-language-support-in-task-sequence"></a>Görev dizisinde geliştirilmiş dil desteği

<!--5411057, 5138936-->

Bu sürüm, işletim sistemi dağıtımı sırasında dil yapılandırması üzerinde denetim ekler. Bu dil ayarlarını zaten uyguluyorsanız, bu değişiklik işletim sistemi dağıtımı görev dizinizi basitleştirmenize yardımcı olabilir. Dil veya ayrı betikler başına birden çok adım kullanmak yerine, yerleşik **Windows ayarlarını uygula** adımının bu dile yönelik bir koşulla birlikte tek bir örneğini kullanın.

Aşağıdaki yeni ayarları yapılandırmak için **Windows ayarlarını uygula** görev dizisi adımını kullanın:

- Giriş yerel ayarı (varsayılan klavye düzeni)
- Sistem yerel ayarı
- Kullanıcı arabirimi dili
- Kullanıcı arabirimi dili geri dönüş
- Kullanıcı yerel ayarı

Daha fazla bilgi için, bkz. [Apply Windows Settings](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Windows 10 yerinde yükseltme için yeni değişken

<!--4680263-->

Windows kurulumu tamamlandığında, yüksek performanslı cihazlarda Windows 10 yerinde yükseltme görev dizisi ile zamanlama sorunlarını gidermek için, şimdi **Setupcompletepause**adlı yeni bir görev dizisi değişkeni ayarlayabilirsiniz. Bu değişkene saniye cinsinden bir değer atadığınızda, Windows kurulum işlemi, görev dizisini çalıştırmadan önce bu süreyi geciktirir. Bu zaman aşımı Configuration Manager istemcisinin başlatılması için ek zaman sağlar.

Daha fazla bilgi için bkz. [görev dizisi değişkenleri-SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> Yazılım güncelleştirmeleri

### <a name="additional-options-for-third-party-update-catalogs"></a>Üçüncü taraf güncelleştirme katalogları için ek seçenekler
<!--4469002-->
Artık üçüncü taraf güncelleştirme kataloglarının eşitlenmesi üzerinde daha ayrıntılı denetimleriniz vardır. Configuration Manager sürüm 1910 ' den başlayarak, her bir kataloğun eşitleme zamanlamasını bağımsız olarak yapılandırabilirsiniz. Kategorilere ayrılmış güncelleştirmeler içeren katalogları kullandığınızda, tüm kataloğun eşitlenmesini önlemek için eşitlemeyi yalnızca belirli güncelleştirme kategorilerini içerecek şekilde yapılandırabilirsiniz. Kategorilere ayrılmış kataloglar sayesinde bir kategori dağıtacağınız zaman, Windows Server Update Services 'ı (WSUS) otomatik olarak indirip yayımlanacak şekilde yapılandırabilirsiniz.

Daha fazla bilgi için bkz. [üçüncü taraf güncelleştirmelerini etkinleştirme](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910).

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Tüm Windows güncelleştirmeleri için teslim Iyileştirmesi kullan
<!--4699118-->
Daha önce, yalnızca hızlı güncelleştirmeler için teslim Iyileştirmesini kullanabilirsiniz. Configuration Manager sürüm 1910 ile, Windows 10 sürüm 1709 veya üstünü çalıştıran istemciler için tüm Windows Update içeriğinin dağıtımı için teslim Iyileştirmesini kullanmak mümkündür.

Daha fazla bilgi için bkz.
- [Windows 10 güncelleştirme teslimini en iyi duruma getirme](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [Yazılım güncelleştirmeleri için istemci ayarları](../../clients/deploy/about-client-settings.md#software-updates)
- [Teslim Iyileştirme için istemci ayarları](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>ADRs için ek yazılım güncelleştirme filtresi
<!--4852033-->
Artık otomatik dağıtım kurallarınız (ADRs) için bir güncelleştirme filtresi olarak **Dağıtılmış** ' yi kullanabilirsiniz. Bu filtre, pilot veya test koleksiyonlarınız için dağıtılması gerekebilecek yeni güncelleştirmelerin tanımlanmasına yardımcı olur.

Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

## <a name="office-management"></a><a name="bkmk_o365"></a> Office yönetimi


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Office 365 ProPlus pilot ve sistem durumu panosu
<!--4488272, 4488301-->

Office 365 ProPlus pilot ve sistem durumu panosu, Office 365 ProPlus ' i planlayıp, pilot ve dağıtmanıza yardımcı olur. Pano, dağıtım planlarınızı etkileyebilecek olası sorunları belirlemenize yardımcı olmak üzere Office 365 ProPlus ile cihazlarda sistem durumu öngörüleri sağlar. Office 365 ProPlus pilot ve sistem durumu panosu, eklenti envanterini temel alan pilot cihazlar için bir öneri sunar.

Daha fazla bilgi için bkz. [Office 365 ProPlus pilot ve sistem durumu panosu](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot).

## <a name="protection"></a><a name="bkmk_protect"></a> Korunmasına

### <a name="bitlocker-management"></a>BitLocker yönetimi

<!--3601034-->

Configuration Manager artık BitLocker Sürücü Şifrelemesi için aşağıdaki yönetim özelliklerini sağlamaktadır:

- BitLocker istemcisini yönetilen Windows cihazlarına dağıtın.
- Cihaz şifreleme ilkelerini yönetin.
- Uyumluluk raporları oluşturun.
- Anahtar kurtarma için bir yönetim ve izleme Web sitesi kullanın.
- Bir Kullanıcı self servis portalına erişin.

Daha fazla bilgi için bkz. [plan for BitLocker Management](../../../protect/plan-design/bitlocker-management.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager konsolu

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Konsol bağlantıları aracılığıyla etkin konsolları ve ileti yöneticilerini görüntüleme
<!--4923997-->
**Konsol bağlantılarında**aşağıdaki iyileştirmeleri yaptık:

- Diğer Configuration Manager yöneticilerini Microsoft ekipleri aracılığıyla iletme özelliği.
- **Son konsol sinyal** sütunu **son bağlı saat** sütununu değiştirdi.
  - Ön planda bulunan açık bir konsol, şu anda hangi konsol bağlantılarının etkin olduğunu belirlemenize yardımcı olmak için 10 dakikada bir sinyal gönderir.

Daha fazla bilgi için bkz. [son bağlantılı konsolları](../../servers/manage/admin-console.md#bkmk_viewconnected) ve [ileti yöneticilerini](../../servers/manage/admin-console.md#bkmk_message)görüntüleme.

### <a name="client-diagnostics-actions"></a>İstemci tanılama eylemleri

<!--4433455-->

Configuration Manager konsolunda **Istemci tanılama** için yeni cihaz eylemleri vardır:

- **Ayrıntılı günlüğü etkinleştir:** CCM bileşeni için genel günlük düzeyini *verbose*olarak değiştirin ve hata ayıklama günlüğünü etkinleştirin.
- **Ayrıntılı günlüğe kaydetmeyi devre dışı bırak:** Genel günlük düzeyini *varsayılana*değiştirin ve hata ayıklama günlüğünü devre dışı bırakın.

Daha fazla bilgi için bkz. [istemci tanılama](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="improvements-to-console-search"></a>Konsol aramasında iyileştirmeler
<!--4640570-->

Bu sürüm Configuration Manager konsolunda arama yapmak için aşağıdaki geliştirmeleri içerir:

- Artık **sürücü paketleri** ve **sorgular** düğümlerinde **tüm alt klasörler** arama seçeneğini kullanabilirsiniz.<!--2841181,5424892-->
- Bir arama 1.000 'den fazla sonuç döndürdüğünde daha fazla sonuç görüntülemek için bildirim çubuğunda **Tamam** ' ı seçin.<!--4640570-->

## <a name="other-updates"></a>Diğer güncelleştirmeler

Configuration Manager için Windows PowerShell cmdlet 'lerinde yapılan değişiklikler hakkında daha fazla bilgi için bkz. [PowerShell sürüm 1910 sürüm notları](/powershell/sccm/1910-release-notes?view=sccm-ps).

Yönetim hizmeti REST API değişiklikler hakkında daha fazla bilgi için bkz. [Yönetim hizmeti sürüm notları](../../../develop/adminservice/release-notes.md#bkmk_1910).

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 1910](https://support.microsoft.com/help/4535776).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
Aşağıdaki güncelleştirme paketi (4537079) konsolunda 18 Şubat 2020 tarihinden itibaren kullanılabilir: [Microsoft uç noktası Için güncelleştirme paketi, geçerli dal, sürüm 1910 Configuration Manager](https://support.microsoft.com/help/4537079).



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Sonraki adımlar

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
20 Aralık 2019 itibariyle, sürüm 1910 tüm müşterilerin yüklemesi için genel kullanıma sunulmuştur.

Bu sürümü yüklemeye hazırsanız, [güncelleştirme 1910 ' i yüklemek için](../../servers/manage/checklist-for-installing-update-1910.md) [Configuration Manager güncelleştirmeleri](../../servers/manage/updates.md) ve denetim listesini yükleme bölümüne bakın.

> [!TIP]
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanın.
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:
>
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md) 
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines) 

Bilinen önemli sorunlar için bkz. [sürüm notları](../../servers/deploy/install/release-notes.md).

Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist)de gözden geçirin.