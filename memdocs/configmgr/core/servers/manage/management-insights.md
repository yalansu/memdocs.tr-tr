---
title: Yönetim içgörüleri
titleSuffix: Configuration Manager
description: Configuration Manager konsolunda bulunan yönetim öngörüleri işlevselliği hakkında bilgi edinin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: de3c75982e19e6183260a2a5f99f65b9c785d27f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700523"
---
# <a name="management-insights-in-configuration-manager"></a>Configuration Manager 'de Yönetim öngörüleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager yönetim öngörüleri ortamınızın geçerli durumu hakkında bilgi sağlar. Bilgiler, site veritabanındaki verilerin analizini temel alır. Öngörüler, ortamınızı daha iyi anlamanıza ve öngörülere göre işlem yapmanıza yardımcı olur. <!--1353967-->

## <a name="review-management-insights"></a>Yönetim öngörülerini gözden geçirin

Öngörüleri görüntülemek için hesabınızın **site** nesnesi üzerinde **okuma** izni olması gerekir.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Yönetim Öngörüler**' i genişletin ve **tüm Öngörüler**' i seçin.

    > [!NOTE]
    > **Management Insights** düğümünü seçtiğinizde, [Yönetim öngörüleri panosunu](#bkmk_insights)gösterir.

1. Gözden geçirmek istediğiniz yönetim öngörüleri grubu adını açın.

1. Şeritte **öngörüleri göster**' i seçin.

Gözden geçirmek için aşağıdaki dört sekme kullanılabilir:

- **Tüm kurallar**: seçili grup için öngörülerin tüm listesini verir.

- **Tamam**: herhangi bir eylemde bulunmanız gereken öngörüleri listeler.

- **Devam ediyor**: bazı Önkoşullar, ancak tümünün tamamlanmamalarından oluşan öngörüleri gösterir.

- **Eylem gerekiyor**: Bu sekme, işlem gerçekleştirmeniz gereken öngörüleri listeler. Eylem gereken belirli öğeleri göstermek için **diğer ayrıntılar** ' ı seçin.

**Önkoşullar** bölmesi, seçilen öngörüleri çalıştırmak için gerekli olan tüm öğeleri listeler.

Örneğin, aşağıdaki ekran görüntüsünde **Cloud Services** grubu Için **tüm kurallar** sekmesine bir örnek gösterilmektedir:

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="Yönetim öngörüleri: Cloud Services grup için tüm kurallar ve Önkoşullar":::

Ayrıntıları görmek için bir öngörü seçin ve **daha sonra diğer ayrıntılar**' ı seçin.

## <a name="operations"></a>İşlemler

Site, bir haftalık zamanlamaya göre yönetim öngörülerinin uygulanabilirliğini yeniden değerlendirin. Bir öngörüyü el ile yeniden hesaplamak için, öngörüye sağ tıklayın ve **yeniden değerlendir**' i seçin.

Management Insights günlük dosyası, site sunucusunda **SMS_DataEngine. log** ' dır.

<!--1357930-->
Bazı Öngörüler, işlem yapmanızı sağlar. Bir öngörü seçin, **daha fazla ayrıntı**seçin ve varsa **eylem al**' ı seçin. Öngörülere bağlı olarak, bu eylem aşağıdaki davranışlardan birine sahiptir:

- Konsolda daha fazla işlem gerçekleştirebileceğiniz düğüme otomatik olarak gidin. Örneğin, yönetim öngörüleri bir istemci ayarının değiştirilmesini önerse, işlem gerçekleşmesi **Istemci ayarları** düğümüne gider. Ardından, varsayılan veya özel bir istemci ayarları nesnesini değiştirerek daha fazla işlem gerçekleştirin.

- Sorgu temelinde filtrelenmiş görünüme gidin. Örneğin, boş koleksiyonlar üzerinde işlem yapmak, koleksiyonlar listesinde yalnızca bu koleksiyonları gösterir. Daha sonra bir koleksiyonu silme veya üyelik kurallarını değiştirme gibi işlemleri gerçekleştirin.

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Yönetim öngörüleri panosu

<!--1357979-->

Grafik panosunu göstermek için **Yönetim öngörüleri** düğümünü seçin. Bu Pano, öngörülere genel bir bakış sunar ve bu da ilerlemenizi göstermenizi kolaylaştırır.

Görünümü iyileştirmek için panonun üst kısmında aşağıdaki filtreleri kullanın:

- Tamamlandı olarak göster
- İsteğe Bağlı
- Önerilen
- Kritik

Pano aşağıdaki kutucukları içerir:  

- **Management Insights dizini**: yönetim öngörülerinin genel ilerlemesini izler. Dizin ağırlıklı bir ortalamadır. Önemli içgörüler en çok önem taşır. Bu dizin, isteğe bağlı öngörülere en az ağırlığı verir.

- **Yönetim öngörüleri grupları**: her bir grupta bulunan öngörülerin yüzdesini gösterir. Bu gruptaki belirli öngörülere gitmek için bir grup seçin.

- **Yönetim öngörüleri önceliği**: filtrelerin öncelikli olarak, filtreleri gerçekleştirerek öngörülerin yüzdesini gösterir.

- **En iyi 10 ilgili öngörü kuralları**: öncelik ve durum dahil olmak üzere Öngörüler tablosu. Kullanılabilir sütunlardan herhangi birinde dizeleri eşleştirmek için tablonun en üstündeki **filtre** alanını kullanın. Pano, tabloyu aşağıdaki sırada sıralar:

  - Durum: eylem gerekli, tamamlandı, bilinmiyor  
  - Öncelik: kritik, önerilen, Isteğe bağlı  
  - Son değiştirme: en üstteki eski tarihler  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="Yönetim öngörüleri panosunun ekran görüntüsü" lightbox="media/1357979-management-insights-dashboard.png":::

## <a name="groups-and-insights"></a>Gruplar ve Öngörüler

Öngörüler aşağıdaki yönetim Insight grupları halinde düzenlenmiştir:

- [Uygulamalar](#applications)
- [Bulut Hizmetleri](#cloud-services)
- [Koleksiyonlar](#collections)
- [Configuration Manager değerlendirmesi](#configuration-manager-assessment)
- [Uzak çalışanlar için iyileştirin](#optimize-for-remote-workers)
- [Proaktif Bakım](#proactive-maintenance)
- [Güvenlik](#security)
- [Basitleştirilmiş yönetim](#simplified-management)
- [Yazılım Merkezi](#software-center)
- [Yazılım güncelleştirmeleri](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> Siteniz aşağıdaki grupların ve öngörülerin tümünü gösteremeyebilir. Daha önce siteyi öneri için yapılandırdıysanız bazı Öngörüler görünmez.

### <a name="applications"></a>Uygulamalar

Uygulama yönetilikleriniz için Öngörüler.

- **Dağıtımları veya başvuruları olmayan uygulamalar**: ortamınızda etkin dağıtımlar veya başvurular bulunmayan uygulamaları listeler. Başvurular arasında bağımlılıklar, görev dizileri ve sanal ortamlar bulunur. Bu öngörü, konsolunda görünen uygulamaların listesini basitleştirmek için kullanılmayan uygulamaları bulmanıza ve silmeye yardımcı olur. Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../../apps/deploy-use/deploy-applications.md).<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### <a name="cloud-services"></a>Bulut hizmetleri

, Cihazlarınızın modern yönetimini etkinleştiren birçok bulut hizmeti ile tümleştirmenize yardımcı olur.

- **Ortak yönetim hazırlığını değerlendirin**: ortak yönetimi etkinleştirmek için hangi adımların gerekli olduğunu anlamanıza yardımcı olur. Bu öngörüde Önkoşullar vardır. Daha fazla bilgi için bkz. [ortak yönetime genel bakış](../../../comanage/overview.md).<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- **Azure AD 'ye yüklenmemiş cihazlar**: sürüm 2002 ' den başlayarak, bu Öngörüler, https için yapılandırmadığınız için sitenin Azure Active Directory (Azure AD) karşıya yüklenmediği cihazları listeler.<!--6268489--> [GELIŞMIŞ http](../../plan-design/hierarchy/enhanced-http.md)'yi yapılandırın veya https için en az bir yönetim noktası etkinleştirin. Siteyi HTTPS iletişimi için zaten yapılandırdıysanız, bu öngörü görünmez.<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- **Bulut yönetimi ağ geçidini etkinleştir**: bulut yönetimi ağ geçidi (CMG), Configuration Manager istemcilerini Internet üzerinden yönetmek için basit bir yol sağlar. CMG 'yi Microsoft Azure bir bulut hizmeti olarak dağıtarak, internet üzerinde dolaşan istemcilere içerik yönetmeye ve hizmet vermeye devam edebilirsiniz. CMG ile, internet 'e açık ek şirket içi altyapıya gerek kalmaz. Daha fazla bilgi için [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md)konusuna bakın.<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **Cihazların karma Azure Active Directory katılmasını sağlama**: Azure AD 'ye katılmış cihazlar, kullanıcıların kendi etki alanı kimlik bilgileriyle oturum açmalarına olanak tanır ve cihazların kuruluşun güvenlik ve uyumluluk standartlarını karşıladığından emin olmanızı sağlar. Daha fazla bilgi için bkz. [Azure AD karma kimlik tasarımı konuları](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview).<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- **Uygun https yapılandırmasına sahip olmayan siteler**: sürüm 2002 ' den başlayarak, bu Öngörüler hiyerarşinizdeki https için düzgün şekilde yapılandırılmamış siteleri listeler. Bu yapılandırma, sitenin [koleksiyon üyeliği sonuçlarını Azure AD gruplarına eşitlemesini](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)engeller. Azure AD eşitleme 'nin tüm cihazları karşıya yüklememesine neden olabilir. Bu istemcilerin yönetimi düzgün çalışmayabilir.<!--6268489--> [GELIŞMIŞ http](../../plan-design/hierarchy/enhanced-http.md)'yi yapılandırın veya https için en az bir yönetim noktası etkinleştirin. Siteyi HTTPS iletişimi için zaten yapılandırdıysanız, bu öngörü görünmez.<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **İstemcileri en son Windows 10 sürümüne güncelleştirin**: Windows 10, sürüm 1709 veya üzeri, kullanıcılarınızın bilgi işlem deneyimini geliştirir ve modernleştirir. Daha fazla bilgi için bkz. [Windows 'u hizmet olarak benimseme hakkındaki önemli makaleler](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### <a name="collections"></a>Koleksiyonlar

Koleksiyonları temizleyip yeniden yapılandırarak yönetimi basitleştirmeye yardımcı olan Öngörüler.

- **Boş Koleksiyonlar**: ortamınızda üyesi olmayan koleksiyonlar listelenir. Daha fazla bilgi için bkz. [koleksiyonları yönetme](../../clients/manage/collections/manage-collections.md).<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **Sorgu kuralları olmayan koleksiyonlar ve doğrudan üye yok**: hiyerarşinizdeki koleksiyonların listesini basitleştirmek için bu koleksiyonları silin.<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **Aynı yeniden değerlendirme başlangıç saatine sahip koleksiyonlar**: Bu koleksiyonlar, diğer koleksiyonlarla aynı yeniden değerlendirme zamanına sahiptir. Yeniden değerlendirme süresini, çakışmayan bir şekilde değiştirin.<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- **Sorgu süresi 5 dakikadan fazla olan koleksiyonlar**: Bu koleksiyonun sorgu kurallarını gözden geçirin. Koleksiyonu değiştirmeyi veya silmeyi düşünün.<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- Aşağıdaki içgörüler, sitede gereksiz yüke neden olabilecek konfigürasyonları içerir. Bu koleksiyonları gözden geçirin, sonra silin ya da koleksiyon kuralı değerlendirmesini devre dışı bırakın:

  - **Sorgu kuralları ve artımlı güncelleştirmeler etkin olmayan Koleksiyonlar**<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - **Sorgu kuralları olmayan ve herhangi bir zamanlama için etkin olan Koleksiyonlar**<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **Sorgu kuralları olmayan koleksiyonlar ve tam değerlendirme zamanlaması seçildi**<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

### <a name="configuration-manager-assessment"></a>Configuration Manager değerlendirmesi

<!--3607758-->

Sürüm 2002 ' den başlayarak bu grup Microsoft Premier alan mühendisinin bir sürümüdür. Bu Öngörüler, Microsoft Premier 'in [hizmet hub 'ında](/services-hub/health/getting_started_with_on_demand_assessments)sağladığı pek çok daha fazla denetim örneğidir.

- **Active Directory güvenlik grubu keşfi çok sık çalışacak şekilde yapılandırılmıştır**: genellikle Active Directory güvenlik grubu bulmayı her üç saatte bir daha sık gerçekleşecek şekilde yapılandırmanız gerekmez. Daha sık bir yapılandırmanın Active Directory, ağ ve Configuration Manager üzerinde olumsuz bir performans etkisi olabilir. Tam eşitleme zamanlaması kullanmak yerine artımlı eşitlemeyi etkinleştirin. Daha fazla bilgi için [Active Directory grubu bulma](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)bölümüne bakın.<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **Active Directory sistem keşfi çok sık çalışacak şekilde yapılandırılmıştır**: genellikle Active Directory sistem bulmayı her üç saatte bir daha sık gerçekleşecek şekilde yapılandırmanız gerekmez. Daha sık bir yapılandırmanın Active Directory, ağ ve Configuration Manager üzerinde olumsuz bir performans etkisi olabilir. Tam eşitleme zamanlaması kullanmak yerine artımlı eşitlemeyi etkinleştirin. Daha fazla bilgi için bkz. [sistem keşfi Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **Active Directory Kullanıcı keşfi çok sık çalışacak şekilde yapılandırılmıştır**: genellikle Active Directory Kullanıcı bulmayı her üç saatte bir daha sık gerçekleşecek şekilde yapılandırmanız gerekmez. Daha sık bir yapılandırmanın Active Directory, ağ ve Configuration Manager üzerinde olumsuz bir performans etkisi olabilir. Tam eşitleme zamanlaması kullanmak yerine artımlı eşitlemeyi etkinleştirin. Daha fazla bilgi için bkz. [Kullanıcı keşfi Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **Tüm sistemler veya tüm kullanıcılar ile sınırlı koleksiyonlar**: **tüm sistemleri** veya tüm **Kullanıcı** koleksiyonlarını sınırlandırma koleksiyonu olarak kullanan tüm koleksiyonları gözden geçirin. Configuration Manager, bu varsayılan koleksiyonların üyeliğini Active Directory bulma yöntemlerindeki verilerle güncelleştirir. Bu veriler Configuration Manager istemcileri için geçerli bilgiler olmayabilir.<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **Sinyal keşfi devre dışı**: sinyal bulma, Configuration Manager istemcisini cihazlara yüklemenizi gerektirir. Bu, istemcilerin başlayacağı tek bulma yöntemidir. Site sunucularında diğer tüm yöntemler oluşur. Sinyal keşfi, istemci etkinlik durumunun güncel tutulması için gereklidir. Site veritabanından kaynak kayıtlarını yanlışlıkla yaşmadığından emin olur. Daha fazla bilgi için bkz. [sinyal keşfi](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- **Artımlı güncelleştirmeler için etkinleştirilen uzun süre çalışan koleksiyon sorguları**: en son artımlı yenileme zamanına sahip koleksiyonlar, 30 saniyeden yüksek olan koleksiyonlar site sunucusu ve veritabanı kaynaklarını kullanır ve bu da genel Configuration Manager performansını etkileyebilir. Daha fazla bilgi için bkz. [koleksiyonlar Için en iyi uygulamalar](../../clients/manage/collections/best-practices-for-collections.md).<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **Dağıtım noktalarındaki uygulama ve paket sayısını azaltın**: Microsoft, bir dağıtım noktasındaki toplam 10.000 paketi ve uygulamayı resmi olarak destekler. Bu toplamın aşıldığı işlem sorunlarına yol açabilir. Daha fazla bilgi için bkz. [boyut ve ölçek numaraları-dağıtım noktası](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- **İkincil site yükleme sorunları**: bazı ikincil sitelerin yükleme durumu **bekliyor** veya **başarısız oldu**. Bu durumlar, yüklemeyi başlattığınız ancak başarıyla tamamlamadığınız anlamına gelir. İkincil site yüklemesi bitene kadar istemciler, birincil siteyle düzgün iletişim kuramayabilir. **İzleme** çalışma alanını denetleyin ve yüklemeyi yeniden deneyin. Daha fazla bilgi için bkz. [başarısız bir güncelleştirme yüklemesini yeniden deneme](install-in-console-updates.md#bkmk_retry).<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **Tüm siteleri aynı sürüme Güncelleştir**: aynı Configuration Manager sürümünü bir hiyerarşide kullanın. Bu yapılandırma, tüm sitelerin aynı işlevselliği sağlamasına olanak sağlar. Aynı hiyerarşideki farklı sürümlerin siteleri birlikte çalışabilirlik senaryolarını ortaya çıkarabilir. Configuration Manager sonraki sürümleri yeni özellikler içerir ve bilinen sorunları çözer. Daha fazla bilgi için bkz. [farklı sürümler arasında birlikte çalışabilirlik](../../plan-design/hierarchy/interoperability-between-different-versions.md).<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

Bu Öngörüler hakkında daha fazla bilgi için bkz. [Configuration Manager Management Insights Için düzeltme adımları](/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Zaten Microsoft 'un birleştirilmiş veya Microsoft Premier müşterisiyseniz, isteğe bağlı ek değerlendirmeler için [Hizmetler hub 'ında](https://serviceshub.microsoft.com/assessments/) oturum açın.
>
> Microsoft hizmetleri hakkında daha fazla bilgi için bkz. [destek çözümleri](https://www.microsoft.com/enterprise/services/support).

### <a name="operating-system-deployment"></a>İşletim sistemi dağıtımı

<!--6982275-->

Sürüm 2006 ' den başlayarak, aşağıdaki yönetim öngörüleri Görev sıralarının ilke boyutunu yönetmenize yardımcı olur. Görev dizisi ilkesinin boyutu 32 MB 'yi aşarsa, istemci büyük ilkeyi işleyemez. İstemci daha sonra görev dizisi dağıtımını çalıştıramazsa.

- **Büyük görev dizileri maksimum ilke boyutunu aşmaya katkıda bulunabilir**: Bu görev dizilerini dağıtırsanız, istemciler büyük ilke nesnelerini işleyemeyebilir. Olası ilke işleme sorunlarını engellemek için görev dizisi ilkesinin boyutunu küçültün.<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- **Görev dizileri Için toplam ilke boyutu ilke sınırını aşıyor**: çok büyük olduğundan istemciler bu görev sıralarının ilkesini işleyemez. Dağıtımın istemcilerde çalışmasına izin vermek için görev dizisi ilkesinin boyutunu küçültün.<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

Daha fazla bilgi için bkz. [görev sırası ilkesi boyutunu azaltma](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize).

Sürüm 2006 ' de, aşağıdaki Öngörüler **proaktif bakım** grubundan bu gruba taşındı:

- **Kullanılmayan önyükleme görüntüleri**: PXE önyüklemesi veya görev dizisi kullanımı için önyükleme görüntülerine başvurulmadı. Daha fazla bilgi için bkz. [önyükleme görüntülerini yönetme](../../../osd/get-started/manage-boot-images.md).<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### <a name="optimize-for-remote-workers"></a>Uzak çalışanlar için iyileştirin

<!--6982226-->

Sürüm 2006 ' den başlayarak, aşağıdaki Öngörüler uzak çalışanlar için daha iyi deneyimler oluşturmanıza ve altyapınızın yükünü azaltmaya yardımcı olur:

- **VPN bağlantılı istemcileri bulut tabanlı içerik kaynaklarını tercih etmek üzere yapılandırın**: VPN 'deki trafiği azaltmak için, sınır grubu seçeneğini **Şirket içi kaynaklar üzerinde bulut tabanlı kaynakları tercih**etmek üzere etkinleştirin. Bu seçenek, istemcilerin VPN genelindeki dağıtım noktaları yerine internet 'ten içerik indirmesini sağlar. Daha fazla bilgi için bkz. [sınır grubu seçenekleri](../deploy/configure/boundary-groups.md#bkmk_bgoptions4).<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- **VPN sınır gruplarını tanımlayın**: VPN sınırı oluşturun ve bunu bir sınır grubuyla ilişkilendirin. VPN 'e özgü site sistemlerini grupla ilişkilendirin ve ortamınız için ayarları yapılandırın. Bu öngörü, en az bir VPN sınırı olan en az bir sınır grubu olup olmadığını denetler. Bu öngörüdeki özelliklerden, **sınır grupları** düğümüne gitmek Için **eylemleri gözden geçir** ' i seçin. Daha fazla bilgi için bkz. [VPN sınır türü](../deploy/configure/boundaries.md#vpn).<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- **VPN bağlantılı istemciler için eşler arası içerik paylaşımını devre dışı bırak**: uzak istemcilere avantaj gerektirmeyen gereksiz eşler arası trafiği engellemek için, **Bu sınır grubunda eş indirmelere izin**vermek için sınır grubu seçeneğini devre dışı bırakın. Daha fazla bilgi için bkz. [sınır grubu seçenekleri](../deploy/configure/boundary-groups.md#bkmk_bgoptions1).<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### <a name="proactive-maintenance"></a>Proaktif Bakım

<!--1352184-->
Bu gruptaki Öngörüler Configuration Manager nesnelerinin önüne geçmemek için olası yapılandırma sorunlarını vurgular.

- **Atanmış site sistemleri olmayan sınır grupları**: atanmış site sistemleri olmadan sınır grupları yalnızca site ataması için kullanılabilir. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../deploy/configure/boundary-groups.md).<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **Üyesi olmayan sınır grupları**: sınır grupları, herhangi bir üyesi yoksa, site atama veya içerik arama için geçerli değildir. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../deploy/configure/boundary-groups.md).<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **İstemcilere içerik hizmet veren dağıtım noktaları**: son 30 gün içinde istemcilere içerik sunulmayan dağıtım noktaları. Bu veriler, indirme geçmişinin istemcilerinden gelen raporları temel alır. Daha fazla bilgi için bkz. [dağıtım noktalarını yükleyip yapılandırma](../deploy/configure/install-and-configure-distribution-points.md).<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **WSUS temizlemeyi etkinleştir**: yazılım güncelleştirme noktası BILEŞENININ özelliklerinde WSUS temizliği çalıştırma seçeneğini etkinleştirdiğini doğrular. Bu seçenek WSUS performansını artırmaya yardımcı olur. Daha fazla bilgi için bkz. [yazılım güncelleştirme Bakımı](../../../sum/deploy-use/software-updates-maintenance.md).<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **Kullanılmayan yapılandırma öğeleri**: yapılandırma temelinin parçası olmayan ve 30 günden eski olan yapılandırma öğeleri. Daha fazla bilgi için bkz. [yapılandırma temelleri oluşturma](../../../compliance/deploy-use/create-configuration-baselines.md).<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **Eş önbellek kaynaklarını Configuration Manager istemcisinin en son sürümüne yükseltin**:<!--1358008--> Eş önbellek kaynağı olarak hizmet veren ancak 1806 olmayan bir istemci sürümünden yükseltilmemiş istemcileri belirler. 1806 öncesi istemciler, sürüm 1806 veya üzerini çalıştıran istemciler için eş önbellek kaynağı olarak kullanılamaz. İstemci listesini görüntüleyen bir cihaz görünümü açmak için **Işlem yap** ' ı seçin.<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> Sürüm 2006 ' de **kullanılmayan önyükleme görüntülerinin** öngörüleri yeni [işletim sistemi dağıtım](#operating-system-deployment) grubuna taşınır.

### <a name="security"></a>Güvenlik

Altyapınızın ve cihazlarınızın güvenliğini iyileştirmeye yönelik Öngörüler.

- **NTLM geri dönüşü etkin**:<!--4572953--> Sürüm 1906 ' den başlayarak, bu öngörü site için daha az güvenli NTLM kimlik doğrulama geri dönüş yöntemi etkinleştirilip etkinleştirilmediğini algılar. Configuration Manager istemcisini yüklemek için Client Push yöntemini kullanırken, site Kerberos karşılıklı kimlik doğrulaması gerektirebilir. Bu geliştirme, sunucu ve istemci arasındaki iletişimin güvenliğini sağlamaya yardımcı olur. Daha fazla bilgi için bkz. [Client Push ile istemcileri yükleme](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **Desteklenmeyen kötü amaçlı yazılımdan koruma istemci sürümleri**: istemcilerin %10 ' dan fazlası desteklenmeyen System Center Endpoint Protection sürümlerini çalıştırıyor. Daha fazla bilgi için bkz. [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

### <a name="simplified-management"></a>Basitleştirilmiş yönetim

Ortamınızın günlük yönetimini basitleştirmeye yardımcı olan Öngörüler.

- **Configuration Manager güncelleştirmeleri için siteyi Microsoft bulutuna bağlama**: bu öngörü, Configuration Manager hizmet bağlantı noktanağınızın son yedi gün içinde Microsoft bulutuna bağlı olduğundan emin olmanızı sağlar. Bu bağlantı, düzenli güncelleştirmeler için içerik indirmek içindir. DMPDownloader. log ve HMAN. log ' u inceleyin. Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **CB olmayan Istemci sürümleri**: sürümleri geçerli dal (CB) derlemesi olmayan tüm istemcileri listeler. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../../clients/manage/upgrade/upgrade-clients.md).<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **İstemcileri desteklenen bir Windows 10 sürümüne güncelleştirin**:<!--3897268--> Bu öngörü, artık desteklenmeyen bir Windows 10 sürümünü çalıştıran istemcilerle ilgili raporlar. Hizmet sonuna yakın bir Windows 10 sürümü olan istemcileri de içerir (üç ay).<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### <a name="software-center"></a>Yazılım Merkezi

Yazılım merkezini yönetmek için Öngörüler.

- **Kullanıcıları Uygulama Kataloğu yerine Software Center 'A doğrudan yönlendirin**: kullanıcıların son 14 gün içinde Uygulama Kataloğu 'ndan yüklenmiş veya istenen uygulamaları yükleyip yüklemediğine bakın. Uygulama Kataloğu 'nun başlıca işlevselliği artık yazılım merkezi 'ne eklenmiştir. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [kullanımdan kaldırılan özellikler](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **Yazılım Merkezi 'nin yeni sürümünü kullan**: Yazılım Merkezi 'nin önceki sürümü artık desteklenmemektedir. İstemci ayarını, **Bilgisayar Aracısı** grubunda **yeni yazılım merkezi kullan** ' ı etkinleştirerek yeni yazılım merkezini kullanmak için istemcileri ayarlayın. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../clients/deploy/about-client-settings.md#use-new-software-center).<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### <a name="software-updates"></a>Yazılım güncelleştirmeleri

- **İstemci ayarları istemcilerin Delta içeriğini indirmesine izin vermek üzere yapılandırılmamış**: ortamınızda eşitlenen bazı yazılım güncelleştirmeleri Delta içeriğini içerir. İstemci ayarını etkinleştirin, **istemcilerin kullanılabilir olduğunda Delta içeriğini Indirmesine Izin verin**. Bu ayarı etkinleştirmezseniz, bu güncelleştirmeleri dağıttığınızda istemci gereksiz yere daha fazla içerik indirirler. Daha fazla bilgi için bkz. [istemci ayarları-yazılım güncelleştirmeleri](../../clients/deploy/about-client-settings.md#software-updates).<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **Yazılım güncelleştirmeleri ürün kategorisi ' Windows 10, sürüm 1903 ve üzeri ' etkinleştir**: Windows 10, sürüm 1903 ve üzeri için yeni bir yazılım güncelleştirmeleri ürün kategorisi vardır. Windows 10 güncelleştirmelerini eşitlerseniz ve Windows 10, sürüm 1903 veya üzeri istemcilere sahipseniz, yazılım güncelleştirme noktası bileşen özellikleri ' nde **Windows 10, sürüm 1903 ve sonraki** ürün kategorisini seçin. Daha fazla bilgi için bkz.[eşitlenmek için sınıflandırmaları ve ürünleri yapılandırma](../../../sum/get-started/configure-classifications-and-products.md).<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

### <a name="windows-10"></a>Windows 10

Windows 10 dağıtımı ve bakımı ile ilgili Öngörüler. Windows 10 Management Insight grubu yalnızca, Windows 7, Windows 8 veya Windows 8.1 çalıştıran istemcilerin yarısında kullanılabilir.

- **Windows tanılama verilerini ve TICARI kimlik anahtarını yapılandırın**: Masaüstü analizinden veri kullanmak Için, ticari kimlik anahtarı ile cihazları yapılandırın ve Tanılama verileri toplamayı etkinleştirin. Windows 10 cihazlarını **Gelişmiş (sınırlı)** düzeyde veya daha yüksek bir düzeye ayarlayın. Daha fazla bilgi için bkz. [Masaüstü analizi için veri paylaşımını etkinleştirme](../../../desktop-analytics/enable-data-sharing.md).<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->