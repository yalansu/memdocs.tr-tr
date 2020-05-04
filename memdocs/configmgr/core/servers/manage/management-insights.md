---
title: Yönetim içgörüleri
titleSuffix: Configuration Manager
description: Configuration Manager konsolunda bulunan yönetim öngörüleri işlevselliği hakkında bilgi edinin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9aae1da48deabd0cc339cd25055827caf07354b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713740"
---
# <a name="management-insights-in-configuration-manager"></a>Configuration Manager 'de Yönetim öngörüleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager yönetim öngörüleri ortamınızın geçerli durumu hakkında bilgi sağlar. Bilgiler, site veritabanındaki verilerin analizini temel alır. Öngörüler, ortamınızı daha iyi anlamanıza ve öngörülere göre işlem yapmanıza yardımcı olur. <!--1353967-->

## <a name="review-management-insights"></a>Yönetim öngörülerini gözden geçirin

Kuralları görüntülemek için hesabınızın **site** nesnesi üzerinde **okuma** izni olması gerekir.

1. Configuration Manager konsolunu açın.  

2. **Yönetim** çalışma alanına gidin, **Yönetim Öngörüler**' i genişletin ve **tüm Öngörüler**' i seçin.  

    > [!Note]  
    > **Management Insights** düğümünü seçtiğinizde, [Yönetim öngörüleri panosunu](#bkmk_insights)gösterir.  

3. Gözden geçirmek istediğiniz yönetim öngörüleri grubu adını açın. Şeritte **öngörüleri göster** ' i seçin.  

Gözden geçirmek için aşağıdaki dört sekme kullanılabilir:

- **Tüm kurallar**: seçili yönetim Insight grubu için kuralların tüm listesini verir.  

- **Tamam**: herhangi bir eylemde bulunmanız gereken kuralları listeler.  

- **Devam ediyor**: bazı Önkoşullar, ancak tümünün tamamlanmalarındaki kuralları gösterir.  

- **Eylem gerekiyor**: eylemlerin alınması gereken kurallar listelenmiştir. Eylem gereken belirli öğeleri almak için **diğer ayrıntılar** ' ı seçin.  

**Önkoşullar** bölmesi, kuralı çalıştırmak için gerekli olan öğeleri listeler.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Cloud Services grubu için tüm kurallar ve Önkoşullar

![Yönetim öngörüleri-bulut hizmetleri grubu için tüm kurallar ve Önkoşullar](./media/Management-insights-all-cloud-rules.png)

Kural ayrıntılarını görmek için bir kural seçin ve **daha sonra Ayrıntılar** ' ı seçin.

## <a name="operations"></a>İşlemler

Yönetim öngörüleri kuralları, bir haftalık zamanlamaya göre uygulanabilirliğini yeniden değerlendirin. Bir kuralı isteğe bağlı olarak yeniden değerlendirmek için kurala sağ tıklayın ve **yeniden değerlendir**' i seçin.

Yönetim öngörüleri kuralları için günlük dosyası, site sunucusunda **SMS_DataEngine. log** dosyasıdır.

<!--1357930-->
Bazı kurallar, işlem yapmanızı sağlar. Bir kural seçin, **daha fazla ayrıntı**' yı seçin ve varsa **eylem al**' ı seçin.

Kurala bağlı olarak, bu eylem aşağıdaki davranışlardan birine sahiptir:  

- Konsolda daha fazla işlem gerçekleştirebileceğiniz düğüme otomatik olarak gidin. Örneğin, yönetim öngörüleri bir istemci ayarının değiştirilmesini önerse, işlem gerçekleşmesi Istemci ayarları düğümüne gider. Ardından, varsayılan veya özel bir istemci ayarları nesnesini değiştirerek daha fazla işlem gerçekleştirin.  

- Sorgu temelinde filtrelenmiş görünüme gidin. Örneğin, boş koleksiyonlar kuralında işlem gerçekleştirmek koleksiyonlar listesinde yalnızca bu koleksiyonları gösterir. Daha sonra bir koleksiyonu silme veya üyelik kurallarını değiştirme gibi işlemleri gerçekleştirin.  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a>Yönetim öngörüleri panosu

<!--1357979-->

**Yönetim öngörüleri** düğümü bir grafik panosu içerir. Bu Pano, kural durumlarına genel bir bakış gösterir, bu da ilerlemenizi göstermenizi kolaylaştırır.

Görünümü iyileştirmek için panonun üst kısmında aşağıdaki filtreleri kullanın:

- Tamamlandı olarak göster
- İsteğe Bağlı
- Önerilen
- Kritik

Pano aşağıdaki kutucukları içerir:  

- **Management Insights dizini**: yönetim öngörüleri kurallarında genel ilerleme durumunu izler. Dizin ağırlıklı bir ortalamadır. Kritik kurallar en çok değer taşır. Bu dizin, isteğe bağlı kurallara en az ağırlığı verir.  

- **Yönetim öngörüleri grupları**: her bir gruptaki kuralların yüzdesini gösterir ve filtreleri uygular. Bu gruptaki belirli kurallara gitmek için bir grup seçin.  

- **Yönetim öngörüleri önceliği**: filtrelerin öncelik sırasına göre yüzde sayısını gösterir.  

- **Tüm Öngörüler**: öncelik ve durum dahil olmak üzere Öngörüler tablosu. Kullanılabilir sütunlardan herhangi birinde dizeleri eşleştirmek için tablonun en üstündeki **filtre** alanını kullanın. Pano, tabloyu aşağıdaki sırada sıralar:

  - Durum: eylem gerekli, tamamlandı, bilinmiyor  
  - Öncelik: kritik, önerilen, Isteğe bağlı  
  - Son değiştirme: en üstteki eski tarihler  

![Yönetim öngörüleri panosunun ekran görüntüsü](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Gruplar ve kurallar

Kurallar aşağıdaki yönetim Insight grupları halinde düzenlenmiştir:

- [Uygulamalar](#applications)
- [Bulut Hizmetleri](#cloud-services)
- [Koleksiyonlar](#collections)
- [Configuration Manager değerlendirmesi](#configuration-manager-assessment)
- [Proaktif Bakım](#proactive-maintenance)
- [Güvenlik](#security)
- [Basitleştirilmiş yönetim](#simplified-management)
- [Yazılım Merkezi](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>Uygulamalar

Uygulama yönetilikleriniz için Öngörüler.

- **Dağıtımsız uygulamalar**: ortamınızda etkin dağıtımlar bulunmayan uygulamaları listeler. Bu kural, konsolunda görünen uygulamaların listesini basitleştirmek için kullanılmayan uygulamaları bulmanıza ve silmeye yardımcı olur. Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../../apps/deploy-use/deploy-applications.md).  

### <a name="cloud-services"></a>Bulut hizmetleri

, Cihazlarınızın modern yönetimini etkinleştiren birçok bulut hizmeti ile tümleştirmenize yardımcı olur.

- **Ortak yönetim hazırlığını değerlendirin**: ortak yönetimi etkinleştirmek için hangi adımların gerekli olduğunu anlamanıza yardımcı olur. Bu kuralın önkoşulları vardır. Daha fazla bilgi için bkz. [ortak yönetime genel bakış](../../../comanage/overview.md).  

- **Azure AD 'ye yüklenmemiş cihazlar**: sürüm 2002 ' den başlayarak, site https için düzgün şekilde yapılandırılmadığından, bu kural Azure AD 'ye yüklenmemiş cihazları listeler.<!--6268489--> [GELIŞMIŞ http](../../plan-design/hierarchy/enhanced-http.md)'yi yapılandırın veya https için en az bir yönetim noktası etkinleştirin. Siteyi HTTPS iletişimi için zaten yapılandırdıysanız, bu kural görünmez.

- **Azure hizmetlerini Configuration Manager ile kullanım Için yapılandırma**: Bu kural, ISTEMCILERIN Azure AD 'yi kullanarak sitede kimlik doğrulamasını sağlayan Azure ad 'ye Configuration Manager eklemenize yardımcı olur. Daha fazla bilgi için bkz. [Azure hizmetlerini yapılandırma](../deploy/configure/azure-services-wizard.md).  

- **Cihazların hibrit Azure Active Directory katılmasını sağlama**: Azure AD 'ye katılmış cihazlar, cihazların kuruluşun güvenlik ve uyumluluk standartlarını karşıladığından emin olmakla birlikte kullanıcıların etki alanı kimlik bilgileriyle oturum açmalarına olanak tanır. Daha fazla bilgi için bkz. [Azure AD karma kimlik tasarımı konuları](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Uygun https yapılandırmasına sahip olmayan siteler**: sürüm 2002 ' den başlayarak, bu kural hiyerarşinizdeki https için düzgün şekilde yapılandırılmamış siteleri listeler. Bu yapılandırma, sitenin [koleksiyon üyeliği sonuçlarının Azure Active Directory (Azure AD) grupları eşitlemesini](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)engeller. Azure AD eşitleme 'nin tüm cihazları karşıya yüklememesine neden olabilir. Bu istemcilerin yönetimi düzgün çalışmayabilir.<!--6268489--> [GELIŞMIŞ http](../../plan-design/hierarchy/enhanced-http.md)'yi yapılandırın veya https için en az bir yönetim noktası etkinleştirin. Siteyi HTTPS iletişimi için zaten yapılandırdıysanız, bu kural görünmez.

- **İstemcileri en son Windows 10 sürümüne güncelleştirin**: Windows 10, sürüm 1709 veya üzeri, kullanıcılarınızın bilgi işlem deneyimini geliştirir ve modernleştirir. Daha fazla bilgi için bkz. [Windows 'u hizmet olarak benimseme hakkındaki önemli makaleler](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).  

### <a name="collections"></a>Koleksiyonlar

Koleksiyonları temizleyip yeniden yapılandırarak yönetimi basitleştirmeye yardımcı olan Öngörüler.

- **Boş Koleksiyonlar**: ortamınızda üyesi olmayan koleksiyonlar listelenir. Daha fazla bilgi için bkz. [koleksiyonları yönetme](../../clients/manage/collections/manage-collections.md).  

Sürüm 1902 ' den başlayarak, koleksiyonları yönetmeye yönelik önerilerle yeni kurallar vardır.<!--3555752--> Yönetimi basitleştirmek ve performansı artırmak için bu öngörüleri kullanın:

- **Sorgu kuralları olmayan koleksiyonlar ve doğrudan üye yok**: hiyerarşinizdeki koleksiyonların listesini basitleştirmek için bu koleksiyonları silin.  

- **Aynı yeniden değerlendirme başlangıç saatine sahip koleksiyonlar**: Bu koleksiyonlar, diğer koleksiyonlarla aynı yeniden değerlendirme zamanına sahiptir. Yeniden değerlendirme süresini, çakışmayan bir şekilde değiştirin.  

- **Sorgu süresi iki saniye üzerinde olan koleksiyonlar**: Bu koleksiyonun sorgu kurallarını gözden geçirin. Koleksiyonu değiştirmeyi veya silmeyi düşünün.

- Aşağıdaki kurallar, sitede gereksiz yüke neden olabilecek konfigürasyonları içerir. Bu koleksiyonları gözden geçirin, sonra silin ya da kural değerlendirmesini devre dışı bırakın:  

  - **Sorgu kuralları ve artımlı güncelleştirmeler etkin olmayan Koleksiyonlar**  

  - **Sorgu kuralları olmayan ve zamanlanan veya artımlı değerlendirme için etkinleştirilen Koleksiyonlar**  

  - **Sorgu kuralları olmayan koleksiyonlar ve tam değerlendirme zamanlaması seçildi**  

### <a name="configuration-manager-assessment"></a>Configuration Manager değerlendirmesi

<!--3607758-->

Sürüm 2002 ' den başlayarak bu grup Microsoft Premier alan mühendisinin bir sürümüdür. Bu kurallar, Microsoft Premier 'in [hizmet hub 'ında](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments)sağladığı pek çok daha fazla denetim örneğidir.

- **Active Directory güvenlik grubu keşfi çok sık çalışacak şekilde yapılandırılmıştır**: genellikle Active Directory güvenlik grubu bulmayı her üç saatte bir daha sık gerçekleşecek şekilde yapılandırmanız gerekmez. Daha sık bir yapılandırmanın Active Directory, ağ ve Configuration Manager üzerinde olumsuz bir performans etkisi olabilir. Tam eşitleme zamanlaması kullanmak yerine artımlı eşitlemeyi etkinleştirin. Daha fazla bilgi için [Active Directory grubu bulma](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)bölümüne bakın.

- **Active Directory sistem keşfi çok sık çalışacak şekilde yapılandırılmıştır**: genellikle Active Directory sistem bulmayı her üç saatte bir daha sık gerçekleşecek şekilde yapılandırmanız gerekmez. Daha sık bir yapılandırmanın Active Directory, ağ ve Configuration Manager üzerinde olumsuz bir performans etkisi olabilir. Tam eşitleme zamanlaması kullanmak yerine artımlı eşitlemeyi etkinleştirin. Daha fazla bilgi için bkz. [sistem keşfi Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).

- **Active Directory Kullanıcı keşfi çok sık çalışacak şekilde yapılandırılmıştır**: genellikle Active Directory Kullanıcı bulmayı her üç saatte bir daha sık gerçekleşecek şekilde yapılandırmanız gerekmez. Daha sık bir yapılandırmanın Active Directory, ağ ve Configuration Manager üzerinde olumsuz bir performans etkisi olabilir. Tam eşitleme zamanlaması kullanmak yerine artımlı eşitlemeyi etkinleştirin. Daha fazla bilgi için bkz. [Kullanıcı keşfi Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

- **Tüm sistemler veya tüm kullanıcılar ile sınırlı koleksiyonlar**: **tüm sistemleri** veya tüm **Kullanıcı** koleksiyonlarını sınırlandırma koleksiyonu olarak kullanan tüm koleksiyonları gözden geçirin. Configuration Manager, bu varsayılan koleksiyonların üyeliğini Active Directory bulma yöntemlerindeki verilerle güncelleştirir. Bu veriler Configuration Manager istemcileri için geçerli bilgiler olmayabilir.

- **Sinyal keşfi devre dışı**: sinyal bulma, Configuration Manager istemcisini cihazlara yüklemenizi gerektirir. Bu, istemcilerin başlayacağı tek bulma yöntemidir. Site sunucularında diğer tüm yöntemler oluşur. Sinyal keşfi, istemci etkinlik durumunun güncel tutulması için gereklidir. Site veritabanından kaynak kayıtlarını yanlışlıkla yaşmadığından emin olur. Daha fazla bilgi için bkz. [sinyal keşfi](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).

- **Artımlı güncelleştirmeler için etkinleştirilen uzun süre çalışan koleksiyon sorguları**: en son artımlı yenileme zamanına sahip koleksiyonlar, 30 saniyeden yüksek olan koleksiyonlar site sunucusu ve veritabanı kaynaklarını kullanır ve bu da genel Configuration Manager performansını etkileyebilir. Daha fazla bilgi için bkz. [koleksiyonlar Için en iyi uygulamalar](../../clients/manage/collections/best-practices-for-collections.md).

- **Dağıtım noktalarındaki uygulama ve paket sayısını azaltın**: Microsoft, bir dağıtım noktasındaki toplam 10.000 paketi ve uygulamayı resmi olarak destekler. Bu toplamın aşıldığı işlem sorunlarına yol açabilir. Daha fazla bilgi için bkz. [boyut ve ölçek numaraları-dağıtım noktası](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).

- **İkincil site yükleme sorunları**: bazı ikincil sitelerin yükleme durumu **bekliyor** veya **başarısız oldu**. Bu durumlar, yüklemeyi başlattığınız ancak başarıyla tamamlamadığınız anlamına gelir. İkincil site yüklemesi bitene kadar istemciler, birincil siteyle düzgün iletişim kuramayabilir. **İzleme** çalışma alanını denetleyin ve yüklemeyi yeniden deneyin. Daha fazla bilgi için bkz. [başarısız bir güncelleştirme yüklemesini yeniden deneme](install-in-console-updates.md#bkmk_retry).

- **Tüm siteleri aynı sürüme Güncelleştir**: aynı Configuration Manager sürümünü bir hiyerarşide kullanın. Bu yapılandırma, tüm sitelerin aynı işlevselliği sağlamasına olanak sağlar. Aynı hiyerarşideki farklı sürümlerin siteleri birlikte çalışabilirlik senaryolarını ortaya çıkarabilir. Configuration Manager sonraki sürümleri yeni özellikler içerir ve bilinen sorunları çözer. Daha fazla bilgi için bkz. [farklı sürümler arasında birlikte çalışabilirlik](../../plan-design/hierarchy/interoperability-between-different-versions.md).

Bu kurallar hakkında daha fazla bilgi için bkz. [Configuration Manager Management Insights Için düzeltme adımları](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Zaten Microsoft 'un birleştirilmiş veya Microsoft Premier müşterisiyseniz, isteğe bağlı ek değerlendirmeler için [Hizmetler hub 'ında](https://serviceshub.microsoft.com/assessments/) oturum açın.
>
> Microsoft hizmetleri hakkında daha fazla bilgi için bkz. [destek çözümleri](https://www.microsoft.com/enterprise/services/support).

### <a name="proactive-maintenance"></a>Proaktif Bakım

<!--1352184-->
Bu gruptaki kurallar, Configuration Manager nesnelerinin önüne geçmemek için olası yapılandırma sorunlarını vurgular.

- **Atanmış site sistemleri olmayan sınır grupları**: atanmış site sistemleri olmadan sınır grupları yalnızca site ataması için kullanılabilir. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../deploy/configure/boundary-groups.md).  

- **Üyesi olmayan sınır grupları**: sınır grupları, herhangi bir üyesi yoksa, site atama veya içerik arama için geçerli değildir. Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../deploy/configure/boundary-groups.md).  

- **İstemcilere içerik hizmet veren dağıtım noktaları**: son 30 gün içinde istemcilere içerik sunulmayan dağıtım noktaları. Bu veriler, indirme geçmişinin istemcilerinden gelen raporları temel alır. Daha fazla bilgi için bkz. [dağıtım noktalarını yükleyip yapılandırma](../deploy/configure/install-and-configure-distribution-points.md).  

- **WSUS temizlemeyi etkinleştir**: yazılım güncelleştirme noktası BILEŞENININ özelliklerinde WSUS temizliği çalıştırma seçeneğini etkinleştirdiğini doğrular. Bu seçenek WSUS performansını artırmaya yardımcı olur. Daha fazla bilgi için bkz. [yazılım güncelleştirme Bakımı](../../../sum/deploy-use/software-updates-maintenance.md).  

- **Kullanılmayan önyükleme görüntüleri**: PXE önyüklemesi veya görev dizisi kullanımı için önyükleme görüntülerine başvurulmadı. Daha fazla bilgi için bkz. [önyükleme görüntülerini yönetme](../../../osd/get-started/manage-boot-images.md).  

- **Kullanılmayan yapılandırma öğeleri**: yapılandırma temelinin parçası olmayan ve 30 günden eski olan yapılandırma öğeleri. Daha fazla bilgi için bkz. [yapılandırma temelleri oluşturma](../../../compliance/deploy-use/create-configuration-baselines.md).  

- **Eş önbellek kaynaklarını Configuration Manager istemcisinin en son sürümüne yükseltin**: eş önbellek kaynağı olarak hizmet veren ve 1806 olan bir istemci sürümünden yükseltilmemiş istemcileri tanımla. 1806 öncesi istemciler, sürüm 1806 veya üzerini çalıştıran istemciler için eş önbellek kaynağı olarak kullanılamaz. İstemci listesini görüntüleyen bir cihaz görünümü açmak için **Işlem yap** ' ı seçin.<!--1358008-->  

### <a name="security"></a>Güvenlik

Altyapınızın ve cihazlarınızın güvenliğini iyileştirmeye yönelik Öngörüler.

- **NTLM geri dönüşü etkin**:<!--4572953--> Sürüm 1906 ' den başlayarak, bu kural site için daha az güvenli NTLM kimlik doğrulama geri dönüş yöntemi etkinleştirilip etkinleştirilmediğini algılar. Configuration Manager istemcisini yüklemek için Client Push yöntemini kullanırken, site Kerberos karşılıklı kimlik doğrulaması gerektirebilir. Bu geliştirme, sunucu ve istemci arasındaki iletişimin güvenliğini sağlamaya yardımcı olur. Daha fazla bilgi için bkz. [Client Push ile istemcileri yükleme](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

- **Desteklenmeyen kötü amaçlı yazılımdan koruma istemci sürümleri**: istemcilerin %10 ' dan fazlası desteklenmeyen System Center Endpoint Protection sürümlerini çalıştırıyor. Daha fazla bilgi için bkz. [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="simplified-management"></a>Basitleştirilmiş yönetim

Ortamınızın günlük yönetimini basitleştirmeye yardımcı olan Öngörüler.

- **Siteyi Configuration Manager güncelleştirmeleri Için Microsoft bulutuna bağlama**: Bu kural, Configuration Manager hizmet bağlantı noktanağınızın son yedi gün içinde Microsoft bulutuna bağlı olmasını sağlar. Bu bağlantı, düzenli güncelleştirmeler için içerik indirmek içindir. DMPDownloader. log ve HMAN. log ' u inceleyin. Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).

- **CB olmayan Istemci sürümleri**: sürümleri geçerli dal (CB) derlemesi olmayan tüm istemcileri listeler. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../../clients/manage/upgrade/upgrade-clients.md).  

- **İstemcileri desteklenen bir Windows 10 sürümüne güncelleştirme**: sürüm 1902 ' den başlayarak, bu kural artık desteklenmeyen bir Windows 10 sürümünü çalıştıran istemcilerde raporlar. Hizmet sonuna yakın bir Windows 10 sürümü olan istemcileri de içerir (üç ay).<!--3897268-->  

### <a name="software-center"></a>Yazılım Merkezi

Yazılım merkezini yönetmek için Öngörüler.

- **Kullanıcıları Uygulama Kataloğu yerine Software Center 'A doğrudan yönlendirin**: kullanıcıların son 14 gün içinde Uygulama Kataloğu 'ndan yüklenmiş veya istenen uygulamaları yükleyip yüklemediğine bakın. Uygulama Kataloğu 'nun başlıca işlevselliği artık yazılım merkezi 'ne eklenmiştir. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [kullanımdan kaldırılan özellikler](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).  

- **Yazılım Merkezi 'nin yeni sürümünü kullan**: Yazılım Merkezi 'nin önceki sürümü artık desteklenmemektedir. İstemci ayarını, **Bilgisayar Aracısı** grubunda **yeni yazılım merkezi kullan** ' ı etkinleştirerek yeni yazılım merkezini kullanmak için istemcileri ayarlayın. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../clients/deploy/about-client-settings.md#use-new-software-center).  

### <a name="software-updates"></a>Yazılım Güncelleştirmeleri

- **İstemci ayarları istemcilerin Delta içeriğini indirmesine izin vermek üzere yapılandırılmamış**: ortamınızda eşitlenen bazı yazılım güncelleştirmeleri Delta içeriğini içerir. İstemci ayarını etkinleştirin, **istemcilerin kullanılabilir olduğunda Delta içeriğini Indirmesine Izin verin**. Bu ayarı etkinleştirmezseniz, bu güncelleştirmeleri dağıttığınızda istemci gereksiz yere daha fazla içerik indirirler. Daha fazla bilgi için bkz. [istemci ayarları-yazılım güncelleştirmeleri](../../clients/deploy/about-client-settings.md#software-updates).

- **Yazılım güncelleştirmeleri ürün kategorisi ' Windows 10, sürüm 1903 ve üzeri ' etkinleştir**: Windows 10, sürüm 1903 ve üzeri için yeni bir yazılım güncelleştirmeleri ürün kategorisi vardır. Windows 10 güncelleştirmelerini eşitlerseniz ve Windows 10, sürüm 1903 veya üzeri bir istemciye sahipseniz, yazılım güncelleştirme noktası bileşen özellikleri ' nde **Windows 10, sürüm 1903 ve sonraki** ürün kategorisini seçin. Daha fazla bilgi için bkz.[eşitlenmek için sınıflandırmaları ve ürünleri yapılandırma](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="windows-10"></a>Windows 10

Windows 10 dağıtımı ve bakımı ile ilgili Öngörüler. Windows 10 Management Insight grubu yalnızca, Windows 7, Windows 8 veya Windows 8.1 çalıştıran istemcilerin yarısında kullanılabilir.

- **Windows tanılama verilerini ve TICARI kimlik anahtarını yapılandırın**: Masaüstü analizinden veri kullanmak Için, ticari kimlik anahtarı ile cihazları yapılandırın ve Tanılama verileri toplamayı etkinleştirin. Windows 10 cihazlarını **Gelişmiş (sınırlı)** düzeyde veya daha yüksek bir düzeye ayarlayın. Daha fazla bilgi için bkz. [Masaüstü analizi için veri paylaşımını etkinleştirme](../../../desktop-analytics/enable-data-sharing.md).

#### <a name="windows-10-management-insights-rules"></a>Windows 10 Yönetim öngörüleri kuralları

![Management Insights-Windows 10 için kurallar](./media/Windows-10-insights-group.png)
