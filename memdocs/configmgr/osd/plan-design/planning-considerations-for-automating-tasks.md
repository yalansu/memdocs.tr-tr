---
title: Otomatikleştirme görevleri için plan
titleSuffix: Configuration Manager
description: Configuration Manager Görevleri otomatikleştirmek için görev dizileri oluşturmadan önce plan yapın.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0348cc245efdfd5e4d1e0bad25a457ea3b1ca609
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723568"
---
# <a name="plan-for-automating-tasks-in-configuration-manager"></a>Configuration Manager görevleri otomatikleştirmeye yönelik plan

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ortamınızdaki görevleri otomatikleştirmek için görev dizileri oluşturabilirsiniz. Bu görevler, işletim sistemini bir veya daha fazla hedef bilgisayara dağıtmak için bir referans bilgisayarda bir işletim sistemini yakalamaya göre değişir. Görev dizisinin eylemleri, dizinin tek tek adımlarında tanımlanır. Görev dizisi çalıştırıldığında, her adımın eylemlerini yerel sistem bağlamındaki komut satırı düzeyinde çalıştırır. Bu davranış, görev dizisinin Kullanıcı müdahalesi olmadan tamamen otomatik olarak çalıştığı anlamına gelir.

## <a name="task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a>Görev dizisi adımları ve eylemleri  

Adımlar, bir görev dizisinin temel bileşenleridir. Aşağıdakiler gibi komutları içerebilir:

- Başvuru bilgisayarının işletim sistemini yapılandırma ve yakalama
- Hedef bilgisayara Windows, donanım sürücüleri, Configuration Manager istemcisi ve yazılım yüklemesi

Adımın eylemleri, bir görev dizisi adımının komutlarını tanımlar. İki tür eylem vardır:  

- Komut satırı dizesi kullanarak tanımladığınız bir eylem, *özel eylem* olarak adlandırılır  
- Configuration Manager tarafından önceden tanımlanan bir eylem, *yerleşik eylem*olarak adlandırılır.  

Bir görev dizisi, özel ve yerleşik eylemlerin herhangi bir birleşimini gerçekleştirebilir.  

Görev dizisi adımları, adımın nasıl davranacağını denetleyen koşulları da içerebilir. Bu davranışlar, görev dizisini durdurmayı veya bir hata oluşursa görev dizisine devam etmek içerir. Bir koşul türü, bir görev dizisi değişkenidir. Örneğin, önceki adımın koşulunu test etmek için **Smstslastactionekcode** değişkenini kullanın. Tek bir adıma veya bir adım grubuna koşul ekleyin.  

Görev dizisi adımları sırayla işler. Bu dizi, adımın eylemini ve adımdaki koşulları içerir. Configuration Manager, bir görev dizisi adımını işlemeye başladığında, önceki eylem tamamlanana kadar sonraki adımı başlatmaz.

Şu durumlarda bir görev dizisi tamamlanmış olarak kabul edilir:

- Tüm adımları tamamlanmıştır  
- Başarısız bir adım, tüm adımları tamamlanmadan önce görev dizisinin çalışmasını durdurmak Configuration Manager neden olur.  

Örneğin, bir görev dizisinin adımı, bir dağıtım noktasında başvurulan bir görüntüyü veya paketi bulamıyorsa, görev sırası bozuk bir başvuru içerir. Configuration Manager, başarısız olan adımın bir hata oluştuğunda devam etmek için bir koşula sahip olmadığı durumlar dışında, bu noktada görev dizisini çalıştırmayı durduruyor.  

> [!IMPORTANT]  
> Varsayılan olarak, bir adım veya eylem başarısız olduğunda bir görev dizisi başarısız olur. Görev dizisinin bir adım başarısız olsa da devam etmesini istiyorsanız, görev dizisini düzenleyin, **Seçenekler** sekmesine geçin ve ardından **hatada devam et**' i seçin.  

Bir görev dizisine eklenebilecek adımlar hakkında daha fazla bilgi için bkz. [görev dizisi adımları](../understand/task-sequence-steps.md).  

## <a name="task-sequence-groups"></a><a name="BKMK_TSGroups"></a>Görev dizisi grupları  

Bir görev dizisi içinde birden çok adımı gruplandırabilirsiniz. Bir görev dizisi grubu, bir ad, isteğe bağlı bir açıklama ve isteğe bağlı koşullardan oluşur. Görev sırası, Grup koşullarını bir sonraki adımla devam etmeden önce birim olarak değerlendirir. Grupları birbirlerine iç içe veya bir dizi adımı ve alt grupları içerir. Gruplar, ortak bir durumu paylaşan birden çok adımı birleştirmek için faydalıdır.  

Görev dizisi gruplarına bir ad atayın. Benzersiz olması gerekmez. Görev dizisi grubu için isteğe bağlı bir açıklama sağlamanız gerekir.  

> [!IMPORTANT]  
> Varsayılan olarak, içindeki herhangi bir adım veya katıştırılmış grup başarısız olduğunda bir görev dizisi grubu başarısız olur. Görev dizisinin bir adım veya katıştırılmış grup başarısız olduğunda devam etmesini istiyorsanız, adımla veya grupta **hata durumunda devam et** seçeneğini ayarlayın.  

Aşağıdaki tabloda, adımları gruplandırdığınızda **hata durumunda devam et** seçeneğinin nasıl çalıştığı gösterilmektedir.  

Bu örnekte, her biri üç görev dizisi adımı içeren iki görev dizisi grubu vardır.  

|Görev dizisi grubu veya adımı|Hatada devam et ayarı|  
|---------------------------------|-------------------------------|  
|**Görev dizisi grubu 1**|**Hatada devam et** seçili.|  
|Görev dizisi adımı 1|**Hatada devam et** seçili.|  
|Görev dizisi adımı 2|Ayarlanmadı.|  
|Görev sırası adımı 3|Ayarlanmadı.|  
|**Görev dizisi grubu 2**|Ayarlanmadı.|  
|Görev dizisi adımı 4|Ayarlanmadı.|  
|Görev dizisi adımı 5|Ayarlanmadı.|  
|Görev sırası adımı 6|Ayarlanmadı.|  

- Görev dizisi adımı 1 başarısız olursa, görev dizisi adım 2 görev dizisi ile devam eder.  

- Görev dizisi 2. adım başarısız olursa, görev dizisi adım 3 görev dizisi çalıştırmaz. Görev dizisi grubu 1 **hata durumunda devam**edecek şekilde yapılandırıldığından, görev dizisi, görev dizisi grubu 2 ' ye devam eder. Sonraki adım 4 görev dizisini çalıştırır.  

- Görev dizisi adımı 4 başarısız olursa, başka bir adım çalıştırılmaz. **Hata durumunda devam et** ayarı görev dizisi grubu 2 için yapılandırılmadığından, görev sırası başarısız olur.  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Bir görev dizisine alt görev dizileri ekleme

<!--1261338-->

Başka bir görev dizisi çalıştıran yeni bir görev dizisi adımı ekleyin. Bu adım, görev dizileri arasında bir üst-alt ilişkisi oluşturur. Bu adımın kullanılması, yeniden kullanabileceğiniz daha modüler görev dizileri oluşturmanıza olanak sağlar.  

Daha fazla bilgi için bkz. [görev dizisini çalıştırma](../understand/task-sequence-steps.md#child-task-sequence).

> [!Note]  
> Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="task-sequence-variables"></a><a name="BKMK_TSVariables"></a>Görev dizisi değişkenleri  

Görev dizisi değişkenleri bir ad ve değer çiftleri kümesidir. Bunlar, Configuration Manager istemcisinde bilgisayar, işletim sistemi ve Kullanıcı durumu yapılandırma görevleri için yapılandırma ve işletim sistemi dağıtım ayarları sağlar. Görev dizisi değişkenleri, bir görev dizisindeki adımları yapılandırmak ve özelleştirmek için bir mekanizma sağlar.  

Bir görev dizisini çalıştırdığınızda, görev dizisi ayarlarının çoğunu ortam değişkenleri olarak depolar. Yerleşik görev dizisi değişkenlerinin değerlerine erişebilir veya bunları değiştirebilirsiniz. Ayrıca, bir görev dizisinin hedef bilgisayarda çalışma biçimini özelleştirmek için yeni görev dizisi değişkenleri oluşturabilirsiniz.  

Aşağıdaki işlemleri yapmak için görev dizisi değişkenlerini kullanın:  

- Bir görev dizisi eylemi için ayarları yapılandırma  

- Bir görev dizisi adımı için komut satırı bağımsız değişkenleri sağlama  

- Bir görev dizisi adımının veya grubunun çalışıp çalışmadığını belirleyen bir koşulu değerlendirin  

- Bir görev dizisinde kullanılan özel betikler için değer sağlama  

Örneğin, bir **etki alanına veya çalışma grubuna katıl** görev dizisi adımını içeren bir görev diziniz vardır. Görev sırasını, koleksiyonun üyeliğinin etki alanı üyeliğiyle belirlendiği farklı koleksiyonlara dağıtın. Her bir koleksiyonun etki alanı adı için koleksiyon başına görev dizisi değişkenini belirtin. Ardından, görev dizisinde uygun etki alanı adını sağlamak için bu görev dizisi değişkenini kullanın.  

Daha fazla bilgi için bkz. [görev dizisi değişkenlerini kullanma](../understand/using-task-sequence-variables.md).

## <a name="create-a-task-sequence"></a><a name="BKMK_TSCreate"></a>Görev sırası oluşturma  

Görev Sırası Oluşturma Sihirbazı'nı kullanarak görev sıraları oluşturun. Sihirbaz, birçok farklı görev gerçekleştirebilen belirli görevleri veya özel görev dizilerini gerçekleştiren yerleşik görev dizileri oluşturabilir. Sihirbaz, aşağıdaki görev dizisi türlerini oluşturmanızı sağlar:

- Hedef bilgisayara var olan bir işletim sistemi görüntüsü yükler  

- Başvuru bilgisayarının işletim sistemi görüntüsünü oluşturma ve yakalama  

- Hedef bilgisayardaki bir işletim sistemi yükseltme paketinden Windows 10 ' a yükseltme

- Özelleştirilmiş bir görevi veya özelleştirilmiş işletim sistemi dağıtımını yapan özel bir görev dizisi oluşturma  

Daha fazla bilgi için bkz. [görev dizileri oluşturma](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

## <a name="edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> Bir görev dizisini düzenleme  

Görev dizisi **düzenleyicisini**kullanarak görev sırasını düzenleyin. Düzenleyici, görev dizisine aşağıdaki değişiklikleri yapabilir:  

- Görev dizisinde adım ekleme veya kaldırma  

- Görev dizisinin adımlarının sırasını değiştirme  

- Adım grupları ekleme veya kaldırma  

- Bir hata oluştuğunda görev dizisinin devam edip etmediğini belirtin  

- Bir görev dizisinin adımları ve gruplarına koşullar ekleme  

> [!IMPORTANT]  
> Görev dizisinin, düzenleme sonucu olarak bir nesneye ilişkilendirilmemiş başvuruları varsa, düzenleyici, kapatmadan önce başvuruyu çözmenizi gerektirir. Olası eylemler şunlardır:  
>
> - Başvuruyu düzeltin
> - Başvurulmayan nesneyi görev dizisinden Sil  
> - Bozuk başvuru düzeltilene veya kaldırılana kadar, başarısız görev dizisi adımını geçici olarak devre dışı bırakın  

Görev dizilerini düzenleme hakkında daha fazla bilgi için bkz. [görev dizisi düzenleyicisini kullanma](../understand/task-sequence-editor.md).  

## <a name="deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a>Görev sırası dağıtma  

Bir görev dizisini, herhangi bir Configuration Manager koleksiyonundaki hedef bilgisayarlara dağıtın. Bilinmeyen bilgisayarlara işletim sistemi dağıtmak için yerleşik **Tüm Bilinmeyen bilgisayarlar** koleksiyonunu kullanın. Bir görev dizisini Kullanıcı koleksiyonlarına dağıtamazsınız.  

> [!IMPORTANT]  
> Uygun olmayan koleksiyonlara işletim sistemlerini yükleyen görev dizilerini dağıtmayın. Görev sırasını dağıttığınız koleksiyonun yalnızca işletim sistemini yüklemek istediğiniz bilgisayarları içerdiğinden emin olun. İstenmeyen işletim sistemi dağıtımlarını önlemeye yardımcı olmak için, yüksek riskli dağıtımlar için ayarları yapılandırın. Daha fazla bilgi için bkz. [yüksek riskli dağıtımları yönetme ayarları](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Görev dizisini alan her bir hedef bilgisayar, dağıtımda belirtilen ayarlara göre görev dizisini çalıştırır. Görev sıralarının kendisi ilişkili dosya veya programları içermez. Görev sırası başvurularını içeren tüm dosyalar hedef bilgisayarda zaten var olmalıdır veya istemcilerin erişebileceği bir dağıtım noktasında depolanır.

> [!NOTE]  
> Görev sırası, program veya paket hedef bilgisayarda zaten yüklü olsa bile, programlar tarafından başvurulan paketleri yüklenir.
>
> Görev dizisi bir uygulama yüklerse, uygulama yalnızca uygulama için gereksinim kuralları karşılanıyorsa ve uygulama için belirtilen algılama yöntemine bağlı olarak zaten yüklü değilse yüklenir.  

Configuration Manager istemcisi, istemci ilkesini indirdiğinde bir görev dizisi dağıtımı çalıştırır. Sonraki yoklama döngüsüne kadar beklemek yerine bu eylemi tetiklemek için, bkz. [Configuration Manager istemcisi için ilke alımı başlatma](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

Bir yazma filtresiyle etkinleştirilen Windows Embedded cihazlarına görev dizilerini dağıttığınızda, dağıtım sırasında cihazdaki Yazma filtresinin devre dışı bırakılıp başlatılmayacağını belirtebilir ve dağıtımdan sonra cihazı yeniden başlatın. Yazma filtresi devre dışı bırakılmazsa, görev dizisi geçici bir katmana dağıtılır ve cihaz yeniden başlatıldığında kullanılabilir olmaz.  

> [!NOTE]  
> Windows Embedded cihazına bir görev sırası dağıttığınızda, cihazın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun. Bu, Yazma filtresinin ne zaman devre dışı ve etkin olduğunu ve cihaz yeniden başlatıldığında yönetmenizi sağlar.  
>
> İstemciler, bir bakım penceresinin dışında görev dizileri indirdiyse, görev dizisi iki kez indirilir. Bu senaryoda, istemci görev dizisini indirir, yazma filtresini devre dışı bırakır, bilgisayarı yeniden başlatır ve ardından görev dizisini yeniden indirir. Bu davranış, görev dizisinin ilk olarak geçici bir katmana İndirilme nedeni ve cihaz yeniden başlatıldığında temizlenir.  

Görev sıralarının nasıl dağıtılacağı hakkında daha fazla bilgi için, bkz. [bir görev dizisi dağıtma](../deploy-use/deploy-a-task-sequence.md).  

## <a name="export-and-import"></a><a name="BKMK_TSExportImport"></a>Dışarı ve içeri aktarma

Configuration Manager, görev dizilerini dışarı ve içeri aktarmanıza olanak tanır. Bir görev dizisini dışarı aktardığınızda, görev dizisinin başvurduğu nesneleri ekleyebilirsiniz.

Daha fazla bilgi için bkz. [görev dizilerini dışarı ve içeri aktarma](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

## <a name="run-a-task-sequence"></a><a name="BKMK_TSRun"></a> Görev dizisi çalıştırma  

Görev dizileri her zaman yerel sistem hesabı kullanılarak çalıştırılır. Görev dizisi çalıştırıldığında, Configuration Manager istemci, görev dizisinin adımlarını başlamadan önce, başvurulan tüm paketleri kontrol eder. Başvurulan bir paketi doğrulayamıyor veya indiremez, görev sırası ilişkili görev dizisi adımı için bir hata döndürür.  

> [!Note]  
> Görev sırası adımı **Çalıştırma komut satırı** , bir komutu farklı bir hesap olarak çalıştırma olanağı sağlar.  

İndirmek ve çalıştırmak üzere bir görev dizisi dağıtımı yapılandırırsanız, Configuration Manager istemcisi tüm bağımlı içeriği önbelleğine indirir. İstemci önbellek boyutu çok küçükse veya içerik bulunamazsa, görev dizisi başarısız olur. İstemci bir durum iletisi oluşturur.

Ayrıca, istemcinin içeriği yalnızca gerekli olduğunda indirmelerini de belirtebilirsiniz. Bu eylemi yapmak için görev sırası dağıtımında **görev dizisini çalıştırarak içeriği gerektiğinde yerel olarak indir** ' i seçin. Başka bir seçenek de **programı dağıtım noktasından çalıştırdır**. Bu seçenekle istemci, dosyaları önce önbelleğe indirmeden doğrudan dağıtım noktasından yüklenir.

Görev sırası dağıtımını **kullanılabilir**olarak yapılandırdığınızda, istemci görev sırası için bağımlı içeriği bulamıyorsa, hemen bir hata gönderir. **Gerekli** bir dağıtım için Configuration Manager istemcisi bu durumda bekler. İçerik henüz istemcinin erişebileceği bir içerik konumuna çoğaltılmazsa, son tarihe kadar içeriği indirmeyi yeniden dener.  

Bir görev dizisi başarıyla tamamlandığında veya başarısız olduğunda, Configuration Manager bu durumu istemci geçmişine kaydeder.

Bir görev dizisi bir bilgisayar üzerinde başlatıldıktan sonra, bunu iptal edemezsiniz veya durduramazsınız.  

> [!IMPORTANT]  
> Bir görev dizisi adımı bilgisayarın yeniden başlatılmasını gerektiriyorsa, istemci, biçimlendirilen bir disk bölümüne önyüklenebilmelidir. Aksi takdirde, görev dizisinde belirttiğiniz herhangi bir hata işleme ne olursa olsun, görev sırası başarısız olur.  

Bir görev dizisinin bağımlı bir nesnesi daha yeni bir sürüme güncelleştirildiği zaman, pakete başvuran herhangi bir görev dizisi otomatik olarak güncelleştirilir. Kaç güncelleştirme dağıttığınıza bakılmaksızın en yeni sürüme başvurur.  

## <a name="use-maintenance-windows"></a><a name="BKMK_TSMaintenanceWindow"></a>Bakım pencerelerini kullanma

Cihaz koleksiyonu için bir bakım penceresi tanımlayarak görev dizisinin ne zaman çalıştırılabilirler belirtebilirsiniz. Bakım pencerelerini başlangıç tarihi, başlangıç ve bitiş saati ve yinelenme düzeniyle yapılandırırsınız. Bakım penceresi için zamanlamayı ayarladığınızda bakım penceresinin yalnızca görev dizileri için geçerli olduğunu belirtebilirsiniz. Daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
> Bir görev dizisini çalıştıracak şekilde bir bakım penceresini yapılandırırsanız, görev dizisi çalıştırıldığında bakım penceresi kapatılsa bile çalışmaya devam eder.  

Bir cihazda birden fazla bakım penceresi uygulanmışsa, istemci **tüm dağıtımlar** bakım penceresini yok sayabilir. Sürüm 1810 ' den başlayarak, bu davranışı denetlemek için aşağıdaki istemci ayarını kullanın: **"yazılım güncelleştirmesi" bakım penceresi kullanılabilir olduğunda "tüm dağıtımlar" bakım penceresinde yazılım güncelleştirmelerinin yüklenmesini etkinleştirin**. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint)<!-- SCCMDocs-pr #4596 -->


## <a name="task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a>Görev dizileri ve ağ erişim hesabı  

> [!Important]  
> Bazı işletim sistemi dağıtım senaryoları ağ erişim hesabı kullanılmasını gerektirmez. Daha fazla bilgi için bkz. [GELIŞMIŞ http](#enhanced-http).

Görev dizileri yalnızca yerel sistem hesabı bağlamında çalıştırılsa da, aşağıdaki durumlarda [ağ erişim hesabı](../../core/plan-design/hierarchy/accounts.md#network-access-account) 'nı yapılandırmanız gerekebilir:  

- Görev sırası, dağıtım noktalarında Configuration Manager içeriğe erişmeyi denediğinde. Ağ erişim hesabını doğru şekilde yapılandırın veya görev sırası başarısız olur.

- Bir işletim sistemi dağıtımı başlatmak için önyükleme görüntüsü kullandığınızda. Bu durumda Configuration Manager, tam bir işletim sistemi olmayan Windows PE ortamını kullanır. Windows PE ortamı, herhangi bir etki alanının üyesi olmayan otomatik olarak oluşturulmuş rastgele bir ad kullanır. Ağ erişim hesabını doğru şekilde yapılandırmazsanız bilgisayar, görev sırası için gerekli içeriğe erişemez.  

> [!NOTE]  
> Ağ erişim hesabı, programları çalıştırmak, uygulamaları yüklemek, güncelleştirmeleri yüklemek veya görev dizilerini çalıştırmak için güvenlik bağlamı olarak hiçbir şekilde kullanılmaz. Ağ erişim hesabı yalnızca ağdaki ilişkili kaynaklara erişmek için kullanılır.  

Ağ erişim hesabı hakkında daha fazla bilgi için bkz. [ağ erişim hesabı](../../core/plan-design/hierarchy/accounts.md#network-access-account).  

### <a name="enhanced-http"></a>Gelişmiş HTTP
<!--1358278-->

**GELIŞMIŞ http**'yi etkinleştirdiğinizde aşağıdaki senaryolar bir dağıtım noktasından içerik indirmek için bir ağ erişim hesabı gerektirmez:

- Önyükleme medyasından veya PXE 'den çalışan görev dizileri  
- Yazılım merkezinden çalıştırılan görev dizileri  

Bu görev dizileri işletim sistemi dağıtımı veya özel olabilir. Çalışma grubu bilgisayarları için de desteklenir.

Daha fazla bilgi için bkz. [GELIŞMIŞ http](../../core/plan-design/hierarchy/enhanced-http.md).  

> [!Note]  
> Aşağıdaki işletim sistemi dağıtım senaryolarında yine de bir ağ erişim hesabı kullanılması gerekir:
>  
> - Görev sırası [dağıtım seçeneği](../deploy-use/deploy-a-task-sequence.md), **çalışan görev sırası için gerektiğinde doğrudan bir dağıtım noktasından içeriğe erişin**
> - [Durum depolama iste](../understand/task-sequence-steps.md#BKMK_RequestStateStore) adım seçeneği, **bilgisayar hesabı bir durum deposuna bağlanamazsa, ağ erişim hesabını kullanın.**
> - Güvenilmeyen bir etki alanı veya Active Directory ormanlar arasında bağlantı kurulurken
> - [İşletim sistemi görüntüsünü Uygula](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) adımı seçeneği, **içeriğe doğrudan dağıtım noktasından erişin**
> - **Önce başka bir programı çalıştırmak** için görev sırası [Gelişmiş ayarı](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced)
> - [Noktalı](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)  

## <a name="create-media"></a><a name="BKMK_TSCreateMedia"></a>Medya oluşturma

Görev dizilerini ve bunlarla ilgili dosyaları ve bağımlılıkları çeşitli medya türlerine yazabilirsiniz. Configuration Manager, yakalama, tek başına ve önyüklenebilir medya için bir DVD veya USB flash sürücü gibi çıkarılabilir medyayı destekler. Önceden hazırlanan medya bir Windows görüntü (WıM) dosyası kullanır.  

Medya oluştururken, erişimi denetlemek için bir parola belirtin. Daha sonra, görev dizisini çalıştırmak için bir kişinin hedef bilgisayarda parolayı girmesi gerekir.  

Medyadan bir görev dizisi çalıştırdığınızda, medyanın belirtilen işlemci mimarisi tanınmaz. Belirtilen mimari hedef bilgisayarla eşleşmiyorsa, görev sırası hala çalışmaya çalışır. Medya mimarisi hedef bilgisayarın mimarisiyle eşleşmiyorsa, görev sırası başarısız olur.  

Daha fazla bilgi için bkz. [görev dizisi medyası oluşturma](../deploy-use/create-task-sequence-media.md).  

### <a name="media-types"></a>Medya türleri

Configuration Manager aşağıdaki medya türlerini destekler:  

#### <a name="capture-media"></a>Medyayı yakala

Bu medya, Configuration Manager altyapısının dışında yapılandırdığınız ve oluşturduğunuz bir işletim sistemi görüntüsünü yakalar. Yakalama medyası, bir görev dizisinden önce çalıştırılabilen özel programları içerebilir. Özel program masaüstüyle etkileşim kurabilir, kullanıcıdan girdi değerlerini isteyebilir veya görev dizisi tarafından kullanılacak değişkenler oluşturabilir.  

Daha fazla bilgi için bkz. [yakalama medyası oluşturma](../deploy-use/create-capture-media.md).  

#### <a name="stand-alone-media"></a>Tek başına medya

Tek başına medya, görev dizisini ve görev dizisinin çalıştırılması için gereken ilişkilendirilmiş tüm nesneleri içerir. Tek başına medya görev dizileri, Configuration Manager sınırlı olduğunda veya ağ bağlantısı olmadığında çalıştırılabilir. Tek başına medyayı aşağıdaki yollarla çalıştırın:  

- Hedef bilgisayar önyüklenmiyorsa, görev dizisiyle ilişkili Windows PE görüntüsü tek başına medyadan kullanılır ve görev sırası başlar.  

- Tek başına medyayı el ile başlatın. Bir Kullanıcı bilgisayarda oturum açmışsa, medyadan görev sırasını başlatabilir.  

> [!IMPORTANT]  
> Tek başına medya görev dizisinin adımları ağdan herhangi bir veri alınmadan çalıştırılabilir olmalıdır. Aksi takdirde, verileri almaya çalışan görev dizisi adımı başarısız olur. Örneğin, dağıtım noktasının bir paketi almasını gerektiren bir görev dizisi adımı başarısız olur. Tek başına medya gerekli paketi içeriyorsa, görev sırası adımı başarılı olur.  

Daha fazla bilgi için bkz. [tek başına medya oluşturma](../deploy-use/create-stand-alone-media.md).  

#### <a name="bootable-media"></a>Önyüklenebilir medya

Önyüklenebilir medya, Configuration Manager altyapısına bağlanabilmesi için bir hedef bilgisayarı başlatmak için gerekli dosyaları içerir. Daha sonra, hangi görev sıralarının koleksiyon üyeliğine göre çalıştırılacağını belirler. Bu medya, görev dizisini veya bağımlı nesneleri içermez. Bunun yerine istemci, içeriği ağ üzerinden indirir. Bu yöntem, hedef bilgisayarda herhangi bir işletim sistemi olmadığında yeni bilgisayarlar veya çıplak dağıtımlar için yararlıdır.  

Daha fazla bilgi için bkz. [önyüklenebilir medya oluşturma](../deploy-use/create-bootable-media.md).  

#### <a name="prestaged-media"></a>Önhazırlığı yapılan medya

Önceden hazırlanan medya, bir işletim sistemi görüntüsünü sağlanmayan bir hedef bilgisayara dağıtır. Önceden hazırlanan medya bir Windows görüntü (WıM) dosyası olarak depolanır. Bu dosya, üretici tarafından veya bir kuruluş hazırlama merkezinde çıplak bir bilgisayara yüklenebilir. Önceden hazırlanmış medyanın bir avantajı, bu konumların Configuration Manager ortamınıza bir bağlantı gerektirmeme bir avantajdır.  

Daha fazla bilgi için bkz. [önceden hazırlanmış medya oluşturma](../deploy-use/create-prestaged-media.md).  

## <a name="next-steps"></a>Sonraki adımlar

- [İşletim sistemi dağıtımı için güvenlik ve gizlilik](security-and-privacy-for-operating-system-deployment.md)

- [İşletim sistemi dağıtımları için site sistemi rollerini hazırlama](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
