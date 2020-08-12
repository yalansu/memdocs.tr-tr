---
title: Görev dizilerini yönetme
titleSuffix: Configuration Manager
description: Görevlerinizi yönetmek ve ortamınızdaki görevleri otomatikleştirmek için görev dizilerini oluşturun, düzenleyin, dağıtın, içeri aktarın ve dışarı aktarın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 609f5d010018fa23dd4a533b2f1079f07d8c2283
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125074"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Görevleri otomatikleştirmek için görev dizilerini yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ortamınızdaki adımları otomatikleştirmek için görev dizilerini kullanın. Bu adımlar bir işletim sistemi görüntüsünü bir hedef bilgisayara dağıtabilir, bir dizi IŞLETIM sistemi yükleme dosyasından bir IŞLETIM sistemi görüntüsü oluşturup yakalayabilir ve Kullanıcı durumu bilgilerini yakalayıp geri yükleyebilir. Görev dizileri Configuration Manager konsolunda bulunur. **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin. Oluşturduğunuz alt klasörler dahil olmak üzere **görev dizileri** düğümü Configuration Manager hiyerarşisi boyunca çoğaltılır. Planlama bilgileri için bkz. [görevleri otomatikleştirme Için planlama değerlendirmeleri](../plan-design/planning-considerations-for-automating-tasks.md).  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a>Oluşturma

Görev Sırası Oluşturma Sihirbazı'nı kullanarak görev sıraları oluşturun. Bu sihirbaz aşağıdaki görev sırası türlerini oluşturabilir:  

- [İşletim sistemini yüklemek Için görev dizisi](create-a-task-sequence-to-install-an-operating-system.md): işletim sistemini yüklemek için gereken adımları oluşturun. Ayrıca, Kullanıcı verilerini geçirme, yazılım güncelleştirmelerini dahil etme ve uygulama yüklemeye yönelik seçenekleri de içerir.

- [Bir işletim sistemini yükseltmek Için görev dizisi](create-a-task-sequence-to-upgrade-an-operating-system.md): BIR işletim sistemini yükseltme adımlarını oluşturun. Ayrıca, yazılım güncelleştirmelerini dahil etme ve uygulamaları yüklemeye yönelik seçenekleri de içerir.

- [İşletim sistemini yakalamak Için görev dizisi](create-a-task-sequence-to-capture-an-operating-system.md): bir başvuru bilgisayarından işletim sistemi oluşturma ve yakalama adımlarını oluşturun. Görüntü yakalanmadan önce başvuru bilgisayarına yazılım güncelleştirmelerini dahil edebilir ve uygulamaları yükleyebilirsiniz.

- [Kullanıcı durumunu yakalamak ve geri yüklemek Için görev dizisi](create-a-task-sequence-to-capture-and-restore-user-state.md): Kullanıcı durumu verilerini yakalamak ve geri yüklemek için var olan bir görev dizisine adımlar ekleyin.

- [Özel görev sırası](create-a-custom-task-sequence.md): Bu tür, görev dizisine herhangi bir adım eklemez. Bu görev dizisini oluşturduktan sonra düzenleyin ve adımlar ekleyin.

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a>Düzenle  

Bir görev dizisini, adımlar ekleyerek veya kaldırarak, grup ekleyerek veya kaldırarak ya da adımların sırasını değiştirerek değiştirebilirsiniz. Daha fazla bilgi için bkz. [görev dizisi düzenleyicisini kullanma](../understand/task-sequence-editor.md).

## <a name="reduce-the-size-of-task-sequence-policy"></a><a name="bkmk_policysize"></a>Görev sırası ilkesi boyutunu azaltma

<!--6982275-->
Görev dizisi ilkesinin boyutu 32 MB 'yi aşarsa, istemci büyük ilkeyi işleyemez. İstemci daha sonra görev dizisi dağıtımını çalıştıramazsa.

Görev dizisinin site veritabanında depolanan boyutu küçüktür, ancak hala çok büyük olduğunda sorunlara neden olabilir. İstemci, tüm görev sırası ilkesini işlediğinde, genişletilmiş boyut 32 MB üzerinde sorunlara neden olabilir.

Sürüm 2006 ' den başlayarak, istemcilerde 32-MB görev sırası ilke boyutunu denetlemek için [Yönetim öngörülerini](../../core/servers/manage/management-insights.md#operating-system-deployment)kullanın.

Bir görev dizisi dağıtımının genel ilke boyutunu azaltmaya yardımcı olmak için aşağıdaki işlemleri gerçekleştirin:

- İşlevsel kesimleri alt görev dizileri halinde ayırın ve [görev dizisi Çalıştır](../understand/task-sequence-steps.md#child-task-sequence) adımını kullanın. Her görev dizisinin ilke boyutu üzerinde ayrı bir 32 MB sınırı vardır.

    > [!NOTE]
    > Bir görev dizisindeki adımların ve grupların toplam sayısını azaltmak, ilke boyutu üzerinde en az etkiye sahiptir. Her adım genellikle ilkede birkaç KB 'dir. Bir alt görev dizisine adım grupları taşımak daha etkili olur.

- Görev dizisiyle aynı koleksiyona yapılan dağıtımlardaki yazılım güncelleştirme sayısını azaltın.

- [PowerShell komut dosyası adımını Çalıştır](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) adımına bir betik girmek yerine, bir paket aracılığıyla başvuru yapın.

- Görev sırası ortamının çalıştığı zaman boyutu için 8 KB 'lik bir sınır vardır. Özel görev dizisi değişkenlerinin kullanımını gözden geçirin. Bu, ilke boyutuna da katkıda bulunabilir.

- Son çare olarak, karmaşık, dinamik bir görev dizisini farklı koleksiyonlara ayrı dağıtımlar ile ayrı görev sıralarına ayırın.

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a>Yazılım Merkezi özellikleri

Yazılım Merkezi 'nde görünen görev dizisinin ayrıntılarını yapılandırmak için aşağıdaki yordamı kullanın. Bu ayrıntılar yalnızca bilgi amaçlıdır.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.  

2. Düzenlenecek görev sırasını seçin ve **Özellikler**' i seçin.  

3. **Genel** sekmesinde, yazılım merkezi için aşağıdaki ayarlar kullanılabilir:  

    - **Yeniden başlatma gerekli**: kullanıcının yükleme sırasında yeniden başlatma gerekip gerekmediğini bilmesini sağlar.  

    - **İndirme boyutu (MB)**: görev sırası Için yazılım merkezi 'nde kaç megabayt görüntülendiğini belirtir.  

    - **Tahmini çalışma süresi (dakika)**: görev sırası Için yazılım merkezi 'nde görüntülenen tahmini çalışma süresini dakika cinsinden belirtir.  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a>Gelişmiş ayarlar

Configuration Manager istemcisinde görev dizisinin davranışını yapılandırmak için aşağıdaki yordamı kullanın.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.  

2. Düzenlenecek görev sırasını seçin ve **Özellikler**' i seçin.  

3. **Gelişmiş** sekmesinde, aşağıdaki ayarlar kullanılabilir:  

    - **Önce başka bir program çalıştır**: görev dizisi çalıştırılmadan önce başka bir pakette program çalıştırmak için bu seçeneği belirleyin. Varsayılan olarak bu onay kutusu işaretli değildir. İlk olarak çalıştırmak için belirttiğiniz programı ayrı ayrı dağıtmanız gerekmez.  

        > [!IMPORTANT]
        > Bu ayar yalnızca tam işletim sisteminde çalışan görev dizileri için geçerlidir. Görev dizisini PXE veya Önyükleme medyası kullanarak başlatırsanız Configuration Manager Bu ayarı yoksayar.  

        - **Paket**: Bu görev sırasından önce çalıştırılacak programı içeren pakete gidin.  

        - **Program**: Bu görev sırasından önce çalıştırılacak programı seçin.  

        > [!NOTE]  
        > Seçilen program bir istemcide çalışamazsa, görev sırası çalıştırılmaz. Seçilen program başarıyla çalışırsa, görev sırası aynı istemcide yeniden çalıştırılsa bile, yeniden çalışmaz.  

    - **Görev sırası bildirimlerini gösterme**: **yeni yazılımın kullanılabilir** bildirim bildirimini gizlemek için bu seçeneği belirleyin. Bildirim alanında yazılım merkezinden **yeni yazılım** simgesini hala görürsünüz. Varsayılan olarak, bu seçenek devre dışıdır.  

    - Bu **görev sırasını dağıtıldığı bilgisayarlarda devre dışı bırak**: Bu seçeneği belirlerseniz, Configuration Manager Bu görev dizisini içeren tüm dağıtımları geçici olarak devre dışı bırakır. Ayrıca görev dizisini, çalıştırılacak olan dağıtımlar listesinden kaldırır. Görev sırası, etkinleştirilinceye kadar çalışmaz. Varsayılan olarak, bu seçenek devre dışıdır.  

    - **İzin verilen en fazla çalışma süresi**: görev dizisinin hedef bilgisayarda çalıştırılmasını beklemeniz için geçmesi gereken en uzun süreyi dakika cinsinden belirtir. Sıfırdan büyük veya sıfıra eşit bir tamsayı kullanın. Varsayılan olarak, bu değer 120 dakikadır.  

        > [!IMPORTANT]  
        > Bu görev dizisini dağıttığınız koleksiyon için bakım pencereleri kullanıyorsanız, **izin verilen en fazla çalışma süresi** zamanlanan bakım penceresinden daha uzunsa bir çakışma meydana gelebilir. Maksimum çalışma süresini **0**olarak ayarlarsanız, görev sırası bakım penceresi sırasında başlar. Bakım penceresi kapatıldıktan sonra tamamlanana veya başarısız olana kadar çalışmaya devam eder. Sonuç olarak, en fazla çalışma süresi **0** olarak ayarlanan görev dizileri, bakım pencerelerinin sonundan daha fazla çalışmayabilir. En fazla çalışma süresini kullanılabilir bakım penceresi uzunluğunu aşan belirli bir döneme (sıfır olmayan) ayarlarsanız, bu görev dizisi çalıştırılmaz. Daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  

        Değeri **0**olarak ayarlarsanız Configuration Manager, izleme ilerleme durumunu izlemek için izin verilen en fazla çalışma süresini **12** saat (720 dakika) olarak değerlendirir. Ancak, geri sayım süresi bakım penceresi değerini aşmadığı sürece görev sırası başlar.  

        > [!NOTE]
        > Maksimum çalışma zamanına ulaştığında, kullanıcıların gerekli bir dağıtımla etkileşime girmesine izin vermezseniz, Configuration Manager görev dizisini sonlandırır. Görev sırasının kendisi durdurulmamışsa, Configuration Manager izin verilen en fazla çalışma zamanına ulaştıktan sonra görev dizisini izlemeyi durduruyor.

    - **Önyükleme görüntüsü kullan**: görev sırası çalıştırıldığında seçili önyükleme görüntüsünü kullanın. Farklı bir önyükleme görüntüsü seçmek için **Araştır** ' ı seçin. Görev sırası çalıştırıldığında seçili önyükleme görüntüsünün kullanımını devre dışı bırakmak için bu seçeneği temizleyin.  

    - **Bu görev dizisi herhangi bir platformda çalışabilir**: Bu seçeneği belirlerseniz, Configuration Manager görev sırası çalıştırıldığında hedef bilgisayarın Platform türünü denetlemez. Bu seçenek varsayılan olarak seçilidir.  

    - **Bu görev sırası yalnızca belirtilen istemci platformlarında çalışabilir**: Bu seçenek, bu görev dizisinin çalışacağı işlemcileri, işletim sistemi sürümlerini ve hizmet paketlerini belirtir. Bu seçeneği belirlediğinizde listeden en az bir platform seçin. Varsayılan olarak, hiçbir platform seçilmemiş. Configuration Manager, bir koleksiyondaki hangi hedef bilgisayarların dağıtılan görev sırasını alacağını değerlendirirken bu bilgileri kullanır.  

        > [!NOTE]  
        > Bir görev dizisini önyükleme medyasından veya PXE 'den çalıştırdığınızda Configuration Manager bu seçeneği yoksayar. Görev sırası, **Bu programın herhangi bir platformda çalışmasına** izin verecek şekilde çalışır.  

## <a name="high-impact-settings"></a>Yüksek etki ayarları

Bir görev dizisini yüksek etki olarak yapılandırın ve kullanıcıların görev dizisini çalıştırırken aldığı iletileri özelleştirin.

> [!WARNING]
> PXE dağıtımlarını kullanır ve ilk önyükleme aygıtı olarak ağ bağdaştırıcısı ile cihaz donanımını yapılandırırsanız, bu cihazlar Kullanıcı etkileşimi olmadan bir işletim sistemi dağıtımı görev sırasını otomatik olarak başlatabilir. Dağıtım doğrulaması bu yapılandırmayı yönetmez. Bu yapılandırma işlemi basitleştirecek ve kullanıcı etkileşimini azaltmasına karşın, yanlışlıkla yeniden görüntü için cihazı daha fazla riske koyar.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Bir görev dizisini yüksek etkili bir görev dizisi olarak ayarlama

Bir görev dizisini yüksek etki olarak ayarlamak için aşağıdaki yordamı kullanın.

> [!NOTE]  
> Belirli koşullara uyan herhangi bir görev dizisi otomatik olarak yüksek etki olarak tanımlanır. Daha fazla bilgi için bkz. [yüksek riskli dağıtımları yönetme](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.  

2. Düzenlenecek görev sırasını seçin ve **Özellikler**' i seçin.  

3. **Kullanıcı bildirimi** sekmesinde, **Bu bir üst etki görevi sırası**seçin.  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Yüksek riskli dağıtımlar için özel bildirim oluşturma

Yüksek etkili dağıtımlar için özel bir bildirim oluşturmak üzere aşağıdaki yordamı kullanın.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.  

2. Düzenlenecek görev sırasını seçin ve **Özellikler**' i seçin.  

3. **Kullanıcı bildirimi** sekmesinde **özel metin kullan**' ı seçin.  

    > [!NOTE]
    > Kullanıcı bildirim metnini yalnızca seçeneği belirlediğinizde ayarlayabilirsiniz; **Bu, yüksek etki bir görev sırasıdır**.  

4. Aşağıdaki ayarları yapılandırın:  

    > [!Note]  
    > Her metin kutusunda en fazla 255 karakter sınırı vardır.  

    - **Kullanıcı bildirimi başlık metni**: Software Center Kullanıcı bildiriminde görüntülenen mavi metni belirtir. Örneğin, varsayılan kullanıcı bildiriminde bu bölüm, "Bu bilgisayardaki işletim sistemini yükseltmek istediğinizi onaylayın."  

    - **Kullanıcı bildirim iletisi metni**: özel bildirimin gövdesini sağlayan üç metin kutusu vardır. Tüm metin kutuları, metin eklemenizi gerektirir.  

        - İlk metin kutusu: genellikle Kullanıcı yönergelerini içeren metnin ana gövdesini belirtir. Örneğin, varsayılan kullanıcı bildiriminde, bu bölümde "işletim sisteminin yükseltilmesi zaman alır ve bilgisayarınızın birkaç kez yeniden başlatılması istenebilir."  

        - İkinci metin kutusu: metnin ana gövdesinde kalın metni belirtir. Örneğin, varsayılan kullanıcı bildiriminde, bu bölümde "Bu yerinde yükseltme yeni işletim sistemini yüklüyor ve uygulamalarınızı, verilerinizi ve ayarlarınızı otomatik olarak geçirir" içerir.  

        - Üçüncü metin kutusu: kalın metin altında metnin son satırını belirtir. Örneğin, varsayılan kullanıcı bildiriminde, bu bölüm "başlamak için Install ' a tıklayın. Aksi takdirde Iptal ' e tıklayın. "  

#### <a name="example"></a>Örnek

Özelliklerde aşağıdaki özel bildirimi yapılandıracaksınız.

![Görev sırası özelliklerinin özelleştirilmiş Kullanıcı bildirimi sekmesi](../media/user-notification.png)

Son Kullanıcı yükleme yazılımını Software Center 'dan açtığında aşağıdaki bildirim iletisi görüntülenir.

![Yazılım Merkezi 'nden son kullanıcıya özelleştirilmiş görev sırası bildirimi](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a>Güç planlarına yönelik performans iyileştirmeleri

<!--3555926-->

Sürüm 1910 ' den başlayarak, artık yüksek performanslı güç planıyla bir görev dizisi çalıştırabilirsiniz. Bu seçenek, görev dizisinin genel hızını geliştirir. Windows 'u, daha yüksek güç tüketimi masrafına en yüksek performans sunan yerleşik yüksek performanslı güç planını kullanacak şekilde yapılandırır. Bu seçenek, yeni görev dizileri için varsayılan olarak açık olur.

Görev sırası başladığında Çoğu senaryoda şu anda etkin olan güç planı kayıt olur. Ardından etkin güç planını Windows varsayılan **yüksek performans** planına geçirir. Görev sırası bilgisayarı yeniden başlatirse, bu işlem yinelenir. Görev dizisinin sonunda, güç planını depolanan değere sıfırlar. Bu işlevsellik hem Windows hem de Windows PE 'de çalışmaktadır, ancak sanal makinelere hiçbir etkisi yoktur.

- Görev dizisi Windows PE 'de başlarsa, görev dizisi daha sonra yeniden kullanmak üzere şu anda etkin olan güç planını kaydetmez.

- Bilgisayarın (Temizleme ve yükleme) yeniden görüntüsünü oluşturan bir işletim sistemi dağıtımı görev dizisi eski işletim sisteminin güç planı ayarını korumaz. Görev dizisinin sonunda, varsayılan **dengeli** güç planını geri yükler.

> [!Important]
> Bu yeni Configuration Manager özelliğinden yararlanmak için, siteyi güncelleştirdikten sonra istemcileri en son sürüme güncelleştirin. Ayrıca, en son istemci bileşenlerini dahil etmek için önyükleme görüntülerini güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin.

1. Var olan bir görev sırası oluşturun veya seçin ve ardından **Özellikler**' i seçin.

1. **Performans** sekmesine geçin.

1. **Yüksek performanslı güç planı olarak çalıştır**seçeneğini etkinleştirin.

> [!Warning]
> Düşük performanslı donanımda bu ayarla dikkatli olun. Yoğun sistem işlemlerini uzun bir süre çalıştırmak, düşük uca donanımları zorlayabilir. Belirli rehberlik için donanım üreticinize danışın.

### <a name="known-issue"></a>Bilinen sorun

<!-- 5554928 -->

Genellikle, görev dizisi özelliklerindeki ayarları değiştirdiğinizde, mevcut tüm dağıtımları günceller. Görev sırası özelliklerindeki bu performans ayarını değiştirdiğinizde, görev dizisinin mevcut dağıtımlarını etkilemez. Yüksek performans için bu ayarı etkinleştirmek veya devre dışı bırakmak üzere yeni bir görev dizisi dağıtımı oluşturun.
<!-- MEMDocs#437, SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a>Başvurulan içeriği dağıtma  

İstemciler içeriğe başvuruda bulunan bir görev dizisini çalıştırmadan önce, bu içeriği dağıtım noktalarına dağıtın. Herhangi bir zamanda görev sırasını seçebilir ve içeriğini dağıtarak dağıtım için yeni referans paketleri listesi oluşturabilirsiniz. Görev dizisinde güncelleştirilmiş içerikle değişiklik yaparsanız, içeriği istemciler için kullanılabilir olmadan önce yeniden dağıtın. Görev sırası tarafından referans verilen içeriği dağıtmak için aşağıdaki prosedürü kullanın.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Başvurulan içeriği dağıtım noktalarına dağıtma işlemi  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

2. **Görev Sırası** listesinde, dağıtmak istediğiniz görev sırasını seçin.  

3. Şeridin **giriş** sekmesinde, **dağıtım** grubunda, **içeriği dağıt**' ı seçin. Bu eylem, Içerik Dağıtma Sihirbazı 'Nı başlatır.  

4. **Genel** sayfasında, dağıtım için doğru görev dizisinin seçildiğini doğrulayın.  

5. **İçerik** sayfasında, görev sırası tarafından başvurulan önyükleme görüntüsü gibi, dağıtılacak içeriği doğrulayın.  

6. **Içerik hedefi** sayfasında, görev sırası içeriklerini dağıtmak istediğiniz koleksiyonları, dağıtım noktasını veya dağıtım noktası grubunu belirtin.  

    > [!IMPORTANT]  
    > Seçtiğiniz görev sırası, belirli bir dağıtım noktasına zaten dağıtılmış içeriğe başvuruyorsa, sihirbaz bu dağıtım noktasını listeetmez.  

7. Sihirbazı tamamlayın.  

Ayrıca, görev dizisinde başvurulan içeriği önceden hazırlayabilirsiniz. Configuration Manager, seçtiğiniz içerik için dosyaları, ilişkili bağımlılıkları ve ilişkili meta verileri içeren sıkıştırılmış, önceden hazırlanmış bir içerik dosyası oluşturur. Daha sonra içeriği bir site sunucusunda, ikincil sitede veya dağıtım noktasında el ile içeri aktarırsınız. İçerik dosyalarının önceden hazırlanması hakkında daha fazla bilgi için bkz. [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a>Dağıtımı  

Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a>Dışarı ve içeri aktarma  

Görev dizilerini ilgili nesneleriyle veya bunlarla birlikte içeri ve dışarı aktarın. Başvurulan Bu içerik aşağıdaki nesneleri içerir:  

- İşletim sistemi görüntüleri  
- Önyükleme görüntüleri  
- İstemci yüklemesi paketi gibi paketler  
- Sürücü paketleri  
- Bağımlılıkları olan uygulamalar  

Görev dizilerini dışa ve içe aktarırken aşağıdaki noktaları göz önünde bulundurun:  

- Configuration Manager, görev dizisinde parolaları dışarı aktarmıyor. Parola içeren bir görev dizisini dışa ve içe aktarırsanız, herhangi bir parolayı yeniden girmek için içe aktarılan görev sırasını düzenleyin. Bir parola içerebilen aşağıdaki adımları gözden geçirin:  

  - [Etki Alanına veya Çalışma Grubuna Katıl](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [Ağ Klasörüne Bağlan](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [Komut satırını Çalıştır](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- **Dinamik değişkenleri ayarla** adımla bir görev dizisini dışarı aktardığınızda, Configuration Manager **gizli değer** ayarıyla yapılandırdığınız değişkenlerin değerlerini dışarı aktarmaz. Görev sırasını aldıktan sonra bu değişkenlerin değerlerini yeniden girin.  

- Birden çok birincil siteniz olduğunda, görev dizilerini merkezi yönetim sitesinde içeri aktarın.  

### <a name="process-to-export-task-sequences"></a>Görev dizilerini dışarı aktarma işlemi  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

2. **Görev Sırası** listesinde, dışa aktarmak istediğiniz görev sıralarını seçin. Birden fazla görev sırası seçerseniz, bunlar tek bir dışarı aktarma dosyasında saklanır.  

3. Şeridin **giriş** sekmesinde, **görev dizisi** grubunda, **dışarı aktar**' ı seçin. Bu eylem, görev sırasını dışarı aktarma Sihirbazı 'Nı başlatır.  

4. **Genel** sayfasında, aşağıdaki ayarları belirtin:  

    - **Dosya**: dışa aktarma dosyasının konumunu ve adını belirtin. Dosyanın adını doğrudan giriyorsanız, dosya adına .zip uzantısını eklemeyi unutmayın. Dışa aktarma dosyasına gözatıyorsanız, sihirbaz bu dosya adı uzantısını otomatik olarak ekler.  

    - Görev sırası bağımlılıklarını dışa aktarmak istemiyorsanız, **tüm görev sırası bağımlılıklarını dışarı aktarma**seçeneğinin seçimini kaldırın. Sihirbaz varsayılan olarak tüm ilgili nesneleri tarar ve bunları görev sırasıyla birlikte dışa aktarır. Bu bağımlılıklar, uygulamalar için herhangi bir içerir.  

    - İçeriği paket kaynağından dışa aktarma konumuna kopyalamak istemiyorsanız, **seçilen görev sıraları ve Bağımlılıklar için tüm Içeriği dışarı aktarma**seçeneğinin işaretini kaldırın. Bu seçeneği belirlerseniz, görev sırası alma Sihirbazı içeri aktarma yolunu yeni paket kaynağı konumu olarak kullanır.  

    - **Yönetici yorumları**: dışarı aktarılacak Görev sıralarının açıklamasını ekleyin.  

5. Sihirbazı tamamlayın.  

Sihirbaz, aşağıdaki çıkış dosyalarını oluşturur:  

- İçeriği dışarı aktarmazsanız: bir. zip dosyası.  

- İçeriği dışa aktarmak istemiyorsanız: bir .zip dosyası ve *dışa aktarma*_dosyaları, burada *dışa aktarma* aktarılan içeriği içeren .zip dosyasının adıdır.  

Bir görev dizisini dışarı aktardığınızda içerik dahil ederseniz,. zip dosyasını ve *dışarı aktarma*_files klasörünü kopyalamadığınızdan emin olun, aksi takdirde içeri aktarma başarısız olur.  

### <a name="process-to-import-task-sequences"></a>Görev dizilerini içeri aktarma işlemi  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırasını al**' ı seçin. Bu eylem, görev sırasını alma Sihirbazı 'Nı başlatır.  

3. Şeridin **genel** sayfasında, aktarılmış. zip dosyasını belirtin.  

4. **Dosya İçeriği** sayfasında, aldığınız her bir nesne için ihtiyacınız olan eylemi seçin. Bu sayfa, içeri aktarmak için Configuration Manager bulunan tüm nesneleri gösterir.  

    - Nesne hiçbir zaman alınmamışsa **Yeni Oluştur**'u seçin.  

    - Nesne daha önce alınmışsa aşağıdaki eylemlerden birini seçin:  

        - **Yineleneni yoksay** (varsayılan): Bu eylem nesneyi içe aktarmaz. Bunun yerine, sihirbaz var olan nesneyi görev sırasına bağlar.  

        - **Üzerine yaz**: Bu eylem, alınan nesneyi var olan nesnenin üzerine yazar. Uygulamalar için, var olan uygulamayı güncelleştirme veya yeni bir uygulama oluşturmak üzere bir düzeltme ekleyebilirsiniz.  

5. Sihirbazı tamamlayın.  

Görev sırasını aldıktan sonra, orijinal görev sırasında bulunan parolaları belirlemek için görev sırasını düzenleyin. Güvenlik nedenleriyle parolalar aktarılmaz.  

## <a name="return-to-previous-page-on-failure"></a>Hata durumunda önceki sayfaya geri dön

Bir görev dizisini çalıştırdığınızda ve bir hata olduğunda, görev sırası sihirbazının önceki sayfasına dönebilirsiniz. Configuration Manager önceki sürümlerinde, bir hata olduğunda görev sırasını yeniden başlatmanız gerekiyordu. Aşağıdaki senaryolarda **önceki** düğmeyi kullanın:

- Bir bilgisayar Windows PE 'de başlatıldığında, görev dizisi önyükleme iletişim kutusu görev dizisi kullanılabilir olmadan önce görüntülenebilir. Bu senaryoda Ileri ' yi seçtiğinizde, görev dizisinin son sayfası, kullanılabilir görev dizileri olmadığını belirten bir iletiyle birlikte görüntülenir. Şimdi, kullanılabilir görev dizileri için yeniden aramak üzere **önceki** ' yi seçebilirsiniz. Görev dizisi kullanılabilir olana kadar bu işlemi yineleyebilirsiniz.  

- Bir görev dizisini çalıştırdığınızda ancak dağıtım noktalarında bağımlı içerik paketleri yoksa, görev sırası başarısız olur. Eksik içerik henüz dağıtılmadıysa, şimdi dağıtın. Ya da içeriğin dağıtım noktalarında kullanılabilir olmasını bekleyin. Ardından, görev dizisinin içerik için tekrar aramasını sağlamak üzere **önceki** ' ni seçin.

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a>Koleksiyon ve cihaz değişkenleri

Bilgisayarlar ve koleksiyonlar için özel görev sırası değişkenlerini tanımlayabilirsiniz. Bir bilgisayar için tanımladığınız değişkenlere bilgisayar başına görev sırası değişkenleri denir. Bir koleksiyon için tanımlanan değişkenler koleksiyon başına görev sırası değişkenleri olarak bilinir. Daha fazla bilgi için bkz. [koleksiyon ve cihaz değişkenleri](../understand/using-task-sequence-variables.md#bkmk_set-coll-var).

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a>Ek eylemler  

Görev dizilerini, görev sırasını seçtiğinizde ek eylemleri kullanarak yönetebilirsiniz.  

### <a name="edit"></a>Düzenle

Daha fazla bilgi için bkz. [görev dizisi düzenleyicisini kullanma](../understand/task-sequence-editor.md#bkmk_edit).

### <a name="enable"></a>Etkinleştir

İstemcilerin çalıştırabilmeleri için görev dizisini etkinleştirilir. Etkinleştirildikten sonra bir görev sırasını yeniden dağıtmanız gerekmez.  

### <a name="disable"></a>Devre Dışı Bırak

Görev sırasını, bilgisayarlarda çalışabilmesi için devre dışı bırakır. Devre dışı bırakılmış bir görev sırasını dağıtabilirsiniz, ancak bilgisayar, etkinleştirilinceye kadar görev dizisini çalıştırmaz.  

### <a name="export"></a>Dışarı Aktarma

Daha fazla bilgi için bkz. [görev dizilerini dışarı ve içeri aktarma](#BKMK_ExportImport).

### <a name="copy"></a>Kopyala

Seçilen görev sırasının bir kopyasını oluşturur. Bu eylem, var olan bir görev dizisini temel alan yeni bir görev dizisi oluşturmak için kullanışlıdır.

Bir klasörde görev sırasının bir kopyasını oluşturduğunuzda, siz görev sırası düğümünü yenileyene kadar kopya bu klasörde listelenir. Yenilemenin ardından kopya kök klasörde görüntülenir.  

### <a name="refresh"></a>Yenile

Seçili görev dizisinin ayrıntılarını yeniler.

### <a name="delete"></a>Sil

Seçili görev sırasını siler.

### <a name="create-phased-deployment"></a>Aşamalı dağıtım oluştur

Daha fazla bilgi için bkz. [aşamalı dağıtımlar oluşturma](create-phased-deployment-for-task-sequence.md).

### <a name="deploy"></a>Dağıtma

Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).

### <a name="distribute-content"></a>İçeriği Dağıt

Başvurulan içeriği dağıtım noktalarına göndermek için Içerik Dağıtma Sihirbazı 'Nı başlatır.

### <a name="create-prestaged-content-file"></a>Önceden Hazırlanan İçerik Dosyası Oluştur

Görev sırası içeriğini önceden hazırlamak için Önceden Hazırlanan İçerik Dosyası Oluşturma Sihirbazı'nı başlatır. Önceden hazırlanan içerik dosyasının nasıl oluşturulacağı hakkında daha fazla bilgi için [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)'ya bakın.

### <a name="move"></a>Taşı

Seçili görev sırasını **görev dizileri** düğümündeki başka bir klasöre kaydırır.

### <a name="set-security-scopes"></a>Güvenlik kapsamlarını ayarla

Seçili görev sırası için güvenlik kapsamlarını seçin. Daha fazla bilgi için bkz. [Güvenlik kapsamları](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

### <a name="properties"></a>Özellikler

Daha fazla bilgi için bkz. [Yazılım Merkezi özelliklerini yapılandırma](#bkmk_prop-general) ve [Gelişmiş görev sırası ayarlarını yapılandırma](#bkmk_prop-advanced).

### <a name="view"></a>Görüntüle

<!--3633146-->
Sürüm 1902 ' den başlayarak, görev dizilerinde **görüntüleme** eylemi varsayılandır. Bu eylem, görev dizisinin adımlarını, düzenlenmek üzere kilitlemeden görmenizi sağlar. Daha fazla bilgi için bkz. [görev dizisi düzenleyicisini kullanma](../understand/task-sequence-editor.md#bkmk_view).

## <a name="see-also"></a>Ayrıca bkz.

- [Kurumsal işletim sistemlerini dağıtma senaryoları](scenarios-to-deploy-enterprise-operating-systems.md)

- [Görev dizisi düzenleyicisini kullanma](../understand/task-sequence-editor.md)

- [Görev dizisini dağıtma](deploy-a-task-sequence.md)

- [Görev dizisi adımları](../understand/task-sequence-steps.md)

- [Koleksiyon ve cihaz değişkenleri](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [Aşamalı dağıtımlar oluşturma](create-phased-deployment-for-task-sequence.md)
