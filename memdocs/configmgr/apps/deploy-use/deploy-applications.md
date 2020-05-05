---
title: Uygulamaları dağıtma
titleSuffix: Configuration Manager
description: Bir cihaza veya Kullanıcı koleksiyonuna uygulama dağıtımı oluşturma veya benzetimi yapma
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7bbf395a5de98459043609986e51647362e7a0b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075345"
---
# <a name="deploy-applications-with-configuration-manager"></a>Configuration Manager ile uygulama dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager bir cihaza veya Kullanıcı koleksiyonuna bir uygulama dağıtımı oluşturun veya benzetimini yapın. Bu dağıtım, yazılımın nasıl ve ne zaman yükleneceğine ilişkin Configuration Manager istemcisine yönergeler sağlar.

Bir uygulamayı dağıtabilmeniz için önce, uygulama için en az bir dağıtım türü oluşturun. Daha fazla bilgi için bkz. [uygulama oluşturma](create-applications.md).

Sürüm 1906 ' den başlayarak, bir kullanıcı veya cihaz koleksiyonuna tek bir dağıtım olarak gönderebilmeniz için bir uygulama grubu oluşturabilirsiniz. Daha fazla bilgi için bkz. [uygulama grupları oluşturma](create-app-groups.md).

Ayrıca, bir uygulama dağıtımının benzetimini de yapabilirsiniz. Bu benzetim, uygulamayı yüklemeden veya kaldırmadan bir dağıtımın uygulanabilirliğini sınar. Sanal dağıtım, bir dağıtım türü için algılama yöntemini, gereksinimleri ve bağımlılıkları değerlendirir ve sonuçları **izleme** çalışma alanının **dağıtımlar** düğümünde raporlar. Daha fazla bilgi için bkz. [uygulama dağıtımlarının benzetimini](simulate-application-deployments.md)yapma.

> [!Note]
> Yalnızca gerekli uygulamaların dağıtımını taklit edebilir, ancak paketleri veya yazılım güncelleştirmelerini kullanamazsınız.
>
> MDM 'ye kayıtlı cihazlar sanal dağıtımları, Kullanıcı deneyimini veya zamanlama ayarlarını desteklemez.



## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a>Uygulama dağıtma

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** ya da **uygulama grupları** düğümünü seçin.

2. Dağıtılacak listeden bir uygulama veya uygulama grubu seçin. Şeritte **Dağıt**' a tıklayın.  

> [!Note]  
> Mevcut bir dağıtımın özelliklerini görüntülediğinizde, aşağıdaki bölümler dağıtım özellikleri penceresinin sekmelerine karşılık gelir:  
>
> - [Genel](#bkmk_deploy-general)
> - [İçerik](#bkmk_deploy-content)
> - [Dağıtım ayarları](#bkmk_deploy-settings)
> - [Zamanlama](#bkmk_deploy-sched)
> - [Kullanıcı deneyimi](#bkmk_deploy-ux)
> - [Uyarılar](#bkmk_deploy-alerts)


### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a>Dağıtım **genel** bilgileri

Yazılım Dağıtma Sihirbazı 'nın **genel** sayfasında aşağıdaki bilgileri belirtin:  

- **Yazılım**: Bu değer dağıtılacak uygulamayı görüntüler. Farklı bir uygulama seçmek için, **Araştır** ' a tıklayın.  

- **Koleksiyon**: uygulamayı dağıtmak istediğiniz koleksiyonu seçmek Için, **Araştır** ' a tıklayın.  

- **Bu koleksiyonla ilişkili varsayılan dağıtım noktası gruplarını kullan**: uygulama içeriğini koleksiyonun varsayılan dağıtım noktası grubunda depolayın. Seçili koleksiyonu bir dağıtım noktası grubuyla ilişkilendirmediyseniz, bu seçenek gri renkte olur.  

- **Bağımlılıklar için Içeriği otomatik olarak dağıt**: uygulamadaki dağıtım türlerinden herhangi birinin bağımlılıkları varsa, site Ayrıca dağıtım noktalarına bağımlı uygulama içeriği gönderir.  

    >[!Note]  
    > Birincil uygulamayı dağıttıktan sonra bağımlı uygulamayı güncelleştirirseniz, site bağımlılık için hiçbir yeni içeriği otomatik olarak dağıtmaz.  

- **Yorumlar (isteğe bağlı)**: isteğe bağlı olarak, bu dağıtım için bir açıklama girin.  


### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a>Dağıtım **içeriği** seçenekleri

**İçerik** sayfasında, bu uygulamanın içeriğini bir dağıtım noktasına veya bir dağıtım noktası grubuna dağıtmak için **Ekle** ' ye tıklayın.

Genel sayfasında **Bu koleksiyonla ilişkili varsayılan dağıtım noktalarını kullan** seçeneğini seçtiyseniz, bu seçenek otomatik olarak doldurulur. Yalnızca **Uygulama Yöneticisi** güvenlik rolünün bir üyesi tarafından değiştirilebilir.

Uygulama içeriği zaten dağıtılmışsa, burada görünürler.


### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a>**Dağıtım ayarları**

**Dağıtım ayarları** sayfasında, aşağıdaki bilgileri belirtin:  

- **Eylem**: açılan listeden, bu dağıtımın uygulamayı **yükleme** veya **kaldırma** seçeneklerinden birini belirleyin.  

    > [!NOTE]  
    > Aynı cihazda aynı uygulamayı **kaldırmak** için bir uygulamayı ve başka bir dağıtımı **yüklemek** üzere bir dağıtım oluşturursanız, **yükleme** dağıtımı önceliklidir.  

    Oluşturulduktan sonra bir dağıtımın eylemini değiştiremezsiniz.  

- **Amaç**: Açılan listede aşağıdaki seçeneklerden birini belirleyin:  

  - **Kullanılabilir**: Kullanıcı, uygulamayı Yazılım Merkezi 'nde görür. Bu, isteğe bağlı olarak yükleyebilir.  

  - **Gerekli**: istemci, ayarladığınız zamanlamaya göre uygulamayı otomatik olarak kurar. Uygulama gizli değilse, Kullanıcı dağıtım durumunu izleyebilir. Ayrıca, son tarihten önce uygulamayı yüklemek için yazılım merkezi 'ni de kullanabilirler.  

    > [!NOTE]  
    > Dağıtım eylemini **Kaldır**olarak ayarladığınızda, dağıtım amacı otomatik olarak **gerekli**olarak ayarlanır. Bu davranışı değiştiremezsiniz.  

- **Son kullanıcıların bu uygulamayı onarmayı denesin**: sürüm 1810 ' den başlayarak, uygulamayı bir onarım komut satırı ile oluşturduysanız, bu seçeneği etkinleştirin. Kullanıcılar, uygulamayı **onarmak** Için yazılım merkezi 'nde bir seçenek görür.<!--1357866-->  

- **Kullanıcının birincil cihazına yazılım ön dağıtımını**yapın: dağıtım bir kullanıcıya ise, uygulamayı kullanıcının birincil cihazına dağıtmak için bu seçeneği belirleyin. Bu ayar, dağıtım çalıştırılmadan önce kullanıcının oturum açmasını gerektirmez. Kullanıcının yüklemeyle etkileşim kurması gerekiyorsa, bu seçeneği seçmeyin. Bu seçenek yalnızca dağıtım **gerekli**olduğunda kullanılabilir.  

- **Uyandırma paketleri gönder**: dağıtım **gerekliyse**, istemci dağıtımı çalıştırmadan önce bilgisayarlara bir uyandırma paketi gönderir Configuration Manager. Bu paket, yükleme son tarihinde bilgisayarları uyandırır. Bu seçeneği kullanmadan önce, bilgisayarlar ve ağların LAN'da Uyandırma için yapılandırılması gerekir. Daha fazla bilgi için bkz. [istemcileri uyandırmayı planlayın](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

- **Tarifeli bir Internet bağlantısı kullanan istemcilerin, yükleme son tarihinden sonra içerik Indirmelerine Izin ver, bu da ek ücret doğurmayabilir**: Bu seçenek yalnızca **gerekli**amacı olan dağıtımlar için kullanılabilir.  

- **Bu uygulamanın yenisiyle değiştirilen tüm sürümlerini otomatik olarak yükselt**: istemci, yerine geçen uygulamayla uygulamanın yenisiyle değiştirilen sürümlerini yükseltir.

    > [!Note]  
    > Bu seçenek, yönetici onayına bakılmaksızın işe yarar. Bir yönetici, yenisiyle değiştirilen sürümü zaten onayladıysa, aynı zamanda yerine geçen sürümü de onaylaması gerekmez. Onay, yükseltme yerine yalnızca yeni istekler için geçerlidir.<!--515824-->  
    >
    > **Kullanılabilir** yüklemenin amacı için bu seçeneği etkinleştirebilir veya devre dışı bırakabilirsiniz. <!--1351266-->


#### <a name="approval-settings"></a><a name="bkmk_approval"></a>Onay ayarları

Uygulama onay davranışı, önerilen isteğe bağlı özelliği etkinleştirdiğinize ve **cihaz başına Kullanıcı için uygulama Isteklerini onayladığınıza**bağlıdır.

- **Bir yönetici cihazdaki bu uygulama için bir isteği onaylamalıdır**: isteğe bağlı özelliği etkinleştirirseniz, kullanıcı istenen cihaza yüklemeden önce, yönetici, uygulama için tüm Kullanıcı isteklerini onaylar. Yönetici isteği onayladığında, Kullanıcı yalnızca bu cihaza uygulamayı kurabilir. Kullanıcı başka bir cihaza uygulamayı yüklemek için başka bir istek göndermesi gerekir. Bu seçenek, dağıtım amacı **gerekli**olduğunda ya da uygulamayı bir cihaz koleksiyonuna dağıttığınızda gri olur.

- **Kullanıcıların bu uygulamayı istemesi durumunda yönetici onayı iste**: isteğe bağlı özelliği etkinleştirmezseniz, yönetici, Kullanıcı tarafından yüklenmeden önce uygulamaya yönelik kullanıcı isteklerini onaylar. Bu seçenek, dağıtım amacı **gerekli**olduğunda ya da uygulamayı bir cihaz koleksiyonuna dağıttığınızda gri olur.  

Daha fazla bilgi için bkz. [uygulamaları onaylama](app-approval.md).


#### <a name="deployment-properties-deployment-settings"></a>Dağıtım özellikleri **dağıtım ayarları**

Dağıtım türü teknolojisi tarafından destekleniyorsa, bir dağıtımın özelliklerini görüntülediğinizde, **dağıtım ayarları** sekmesinde aşağıdaki seçenek görünür:

**Dağıtım türü özellikleri iletişim kutusunun Kurulum davranışı sekmesinde belirttiğiniz çalışan tüm yürütülebilir dosyaları otomatik olarak kapatın**. Daha fazla bilgi için bkz. [bir uygulamayı yüklemeden önce yürütülebilir dosyaları çalıştırmaya yönelik denetim](#bkmk_exe-check).



### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a>Dağıtım **zamanlama** ayarları

**Zamanlama** sayfasında, bu uygulamanın ne zaman dağıtıldığını veya istemci cihazları için kullanılabilir olduğunu ayarlayın.

Varsayılan olarak, Configuration Manager dağıtım ilkesini istemciler için hemen kullanılabilir hale getirir. Dağıtım oluşturmak, ancak daha sonra bir tarihe kadar istemciler için kullanılabilir hale getirmek istiyorsanız, **uygulamayı kullanılabilir olacak şekilde zamanlama**seçeneğini yapılandırın. Ardından, UTC 'ye veya istemcinin yerel saatine bağlı olup olmadığına bakılmaksızın tarih ve saati seçin.

Dağıtım **gerekliyse**, **yükleme son tarihini**de belirtin. Varsayılan olarak bu son tarih mümkün olan en kısa zamandır.

Örneğin, yeni bir iş kolu uygulaması dağıtmanız gerekir. Tüm kullanıcıların bu uygulamayı belirli bir zamana göre yüklemesi gerekir, ancak bu kullanıcılara erken kabul etme seçeneğini vermek istersiniz. Ayrıca, sitenin içeriği tüm dağıtım noktalarına dağıttığınızdan emin olmanız gerekir. Uygulamayı Bugünden beş gün içinde kullanılabilir olacak şekilde zamanlayın. Bu zamanlama, içeriği dağıtmanız ve durumunu onaylamanız için zaman kazandırır. Sonra, yükleme son tarihini bugünden itibaren bir ay olarak ayarlarsınız. Kullanıcılar, beş gün içinde kullanılabilir olduğunda uygulamayı Yazılım Merkezi 'nde görür. Hiçbir şey yoksa, istemci otomatik olarak uygulamayı yükleme son tarihinde kurar.

Dağıttığınız uygulama başka bir uygulamanın yerini alıyorsa, kullanıcılar yeni uygulamayı alırken yükleme son tarihini ayarlayın. **Yükleme son tarihini** , kullanıcıları yenisiyle değiştirilen uygulamayla yükseltmek için ayarlayın.


#### <a name="delay-enforcement-with-a-grace-period"></a>Yetkisiz kullanım süresi ile uygulamayı geciktir

Kullanıcılara, gerekli uygulamaları ayarladığınız süre *sonundan* daha fazla zaman vermek isteyebilirsiniz. Bu davranış genellikle bir bilgisayar uzun bir süre kapalıyken gereklidir ve birçok uygulama yüklemesi gerekir. Örneğin, bir Kullanıcı tatilden döndüğünde, istemci vadesi geçmiş dağıtımları yüklerken uzun süre beklemelidir. Bu sorunu çözmeye yardımcı olmak için bir zorlama yetkisiz kullanım süresi tanımlayın.

- İlk olarak, bu yetkisiz kullanım süresini, istemci ayarlarındaki **dağıtım son tarihi (saat) sonra zorlama için özellik yetkisiz kullanım** süresiyle yapılandırın. Daha fazla bilgi için [Bilgisayar Aracısı](../../core/clients/deploy/about-client-settings.md#computer-agent) grubuna bakın. **1** ila **120** saat arasında bir değer belirtin.  

- Gerekli bir uygulama dağıtımının **zamanlama** sayfasında, **Bu dağıtımın uygulanmasını, istemci ayarlarında tanımlanan yetkisiz kullanım süresine kadar olan kullanıcı tercihlerine göre geciktir**seçeneğini etkinleştirin. Zorlama yetkisiz kullanım süresi, bu seçenek etkinleştirilmiş ve istemci ayarını dağıttığınız cihazlara hedeflenmiş tüm dağıtımlar için geçerlidir.

Son tarihten sonra istemci, uygulamayı kullanıcının yapılandırdığı, bu yetkisiz kullanım süresine kadar olan ilk iş dışı pencereye yükleme. Ancak kullanıcı hala yazılım merkezini açabilir ve uygulamayı dilediğiniz zaman yükleyebilir. Yetkisiz kullanım süresi dolduktan sonra, zorlama süresi dolan dağıtımlar için normal davranışa geri döner.

![Yetkisiz kullanım süresi zaman çizelgesinin diyagramı](media/grace-period.svg)

<!-- SCCMDocs issue #1599 -->

> [!Note]  
> Çoğu zaman, bu özellik, Kullanıcı ofis dışı durumdayken cihazın gücü kapatıldığında senaryoya yöneliktir. Teknik olarak, yetkisiz kullanım süresi, istemci, dağıtım son tarihinden sonra ilke aldığında başlar. Configuration Manager istemci hizmetini (CcmExec) durdurup bir süre sonra dağıtım son tarihinden sonra yeniden başlatırsanız aynı davranış oluşur.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a>Dağıtım **Kullanıcı deneyimi** ayarları

**Kullanıcı deneyimi** sayfasında, kullanıcıların uygulama yüklemesiyle nasıl etkileşim kurabileceğine ilişkin bilgileri belirtin.

- **Kullanıcı bildirimleri**: Yazılım Merkezi 'nde yapılandırılan kullanılabilir zamanda bildirimin görüntülenip görüntülenmeyeceğini belirtin. Bu ayar ayrıca kullanıcılara istemci bilgisayarlarda bildirim yapılıp yapılmayacağını da denetler. Kullanılabilir dağıtımlar için, **Yazılım Merkezi 'nde ve tüm bildirimlerde gizleme**seçeneğini seçemezsiniz.  

    - **Yazılım değişiklikleri gerektiğinde kullanıcıya bildirim yerine bir iletişim kutusu penceresi gösterin**<!--3555947-->: Sürüm 1902 ' den başlayarak, Kullanıcı deneyimini daha zorbir şekilde değiştirmek için bu seçeneği belirleyin. Yalnızca gerekli dağıtımlar için geçerlidir. Daha fazla bilgi için bkz. [plan for Software Center](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Yazılım yükleme** ve **sistem yeniden başlatma**: Bu ayarları yalnızca gerekli dağıtımlar için yapılandırın. Dağıtım, son tarihe kadar tanımlanmış bakım pencerelerinin dışında kaldığında davranışları belirler. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  

- **Windows Embedded cihazlar için filtre Işleme yaz**: Bu ayar, yazma filtresiyle etkinleştirilen Windows Embedded cihazlarındaki yükleme davranışını denetler. Yükleme son tarihinde veya bakım penceresi sırasında değişiklikleri Yürüt seçeneğini belirleyin. Bu seçeneği belirlediğinizde, yeniden başlatma gerekir ve değişiklikler cihazda kalır. Aksi takdirde, uygulama geçici bir katmana yüklenir ve daha sonra kaydedilir.  

    - Windows Embedded cihazına bir yazılım güncelleştirmesi dağıttığınızda, cihazın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun. Bakım pencereleri ve Windows Embedded cihazları hakkında daha fazla bilgi için bkz. [Windows Embedded uygulamaları oluşturma](../get-started/creating-windows-embedded-applications.md).  


### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a>Dağıtım **uyarıları**

**Uyarılar** sayfasında, bu dağıtım için Configuration Manager uyarıları nasıl üretir yapılandırın. System Center Operations Manager kullanıyorsanız, uyarılarını da yapılandırın. Gerekli dağıtımlar için yalnızca bazı uyarıları yapılandırabilirsiniz. 


## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a>Aşamalı dağıtım oluşturma

<!--1358147-->
Sürüm 1806 ' den başlayarak, bir uygulama için aşamalı bir dağıtım oluşturun. Aşamalı dağıtımlar, özelleştirilebilir ölçütlere ve gruplara göre düzenlenmiş, sıralı bir yazılım dağıtımını düzenlemenize olanak tanır. Örneğin, uygulamayı bir pilot koleksiyonuna dağıtın ve ardından başarı ölçütlerine göre otomatik olarak piyasaya devam edin.

Daha fazla bilgi için aşağıdaki makalelere bakın:  

- [Aşamalı dağıtım oluşturma](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Aşamalı dağıtım izleme ve yönetme](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a>Bir dağıtımı silme

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** ya da **uygulama grupları** düğümünü seçin.  

2. Silmek istediğiniz dağıtımı içeren uygulamayı veya uygulama grubunu seçin.  

3. Ayrıntılar bölmesinin **dağıtımlar** sekmesine geçin ve dağıtımı seçin.  

4. Şeritte, **dağıtım** sekmesinde ve **dağıtım** grubunda, **Sil**' e tıklayın.  

Bir uygulama dağıtımını sildiğinizde, uygulamanın zaten yüklemiş olduğu uygulamanın tüm örnekleri kaldırılmaz. Bu uygulamaları kaldırmak için **uygulamayı kaldırmak üzere bilgisayarlara dağıtın.** Bir uygulama dağıtımını siler veya dağıtım yaptığınız koleksiyondan bir kaynağı kaldırırsanız uygulama artık yazılım merkezi 'nde görünmez.



## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a>Gerekli dağıtımlar için Kullanıcı bildirimleri

Kullanıcılar gerekli yazılımları alır ve **erteleme ve bana anımsat** ayarını seçtiğinizde, aşağıdaki seçeneklerden birini seçebilirler:  

- **Daha sonra**: bildirimlerin istemci ayarlarında yapılandırılan bildirim ayarlarına göre zamanlandığını belirtir.  

- **Sabit zaman**: bildirimin seçili zamandan sonra yeniden görüntülenmek üzere zamanlandığını belirtir. Örneğin, 30 dakika ' yı seçerseniz, bildirim 30 dakika içinde yeniden görüntülenir.  

![Varsayılan istemci ayarlarındaki bilgisayar Aracısı grubu](media/ComputerAgentSettings.png)

En uzun süre erteleme süresi her zaman dağıtım zaman çizelgesinde istemci ayarlarında yapılandırılan bildirim değerlerine göre belirlenir. Örneğin:  

- **Dağıtım son tarihini 24 saatten büyük bir süre sonra,** **Bilgisayar Aracısı** sayfasında her saat için 10 saat için hatırlat.  

- İstemci, dağıtım son tarihinden önce 24 saatten fazla bildirim iletişim kutusunu görüntüler.  

- İletişim kutusu, erteleme seçeneklerini 10 saatten fazla olacak şekilde gösterir.  

- Dağıtım son tarihi yaklaşırsa, iletişim kutusunda daha az seçenek gösterilir. Bu seçenekler, dağıtım zaman çizelgesinin her bileşeni için ilgili istemci ayarlarıyla tutarlıdır.  

Bir işletim sistemini dağıtan görev dizisi gibi yüksek riskli bir dağıtım için Kullanıcı bildirim deneyimi daha zorlayıcıdır. Geçici bir görev çubuğu bildirimi yerine, kritik yazılım bakımının gerekli olduğu her bildirileceği sırada aşağıdakine benzer bir iletişim kutusu görüntülenir:

![Gerekli yazılım iletişim kutusu size kritik yazılım bakımı bildirir](media/client-toast-notification.png)



## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a>Yürütülebilir dosyaları çalıştırmaya yönelik denetim

İstemci üzerinde belirli yürütülebilir dosyaların çalışıp çalışmadığını denetlemek için bir dağıtım yapılandırın. Uygulamanın yüklenmesini kesintiye uğratan süreçler denetlemek için bu seçeneği kullanın. Bu yürütülebilir dosyalardan biri çalıştırıyorsa, istemci, dağıtım türünün yüklenmesini engeller. İstemcinin dağıtım türünü yükleyebilmesi için önce çalışan yürütülebilir dosyayı kapatması gerekir. Gerekli amacı olan dağıtımlar için, istemci çalışan yürütülebilir dosyayı otomatik olarak kapatabilir.

1. Dağıtım türü için **Özellikler** iletişim kutusunu açın.  

2. **Yüklemeyi davranışı** sekmesine geçin ve **Ekle**' ye tıklayın.  

3. **Yürütülebilir dosya Ekle** iletişim kutusunda, hedef yürütülebilir dosyanın adını girin. İsteğe bağlı olarak, uygulamayı listede tanımanıza yardımcı olması için kolay bir ad girin.  

4. **Tamam**' a tıklayın ve ardından dağıtım türü Özellikler penceresini kapatmak için **Tamam** ' a tıklayın.  

5. Uygulamayı dağıttığınızda, **dağıtım türü özellikleri iletişim kutusunun Kurulum davranışı sekmesinde belirtilen çalışan yürütülebilir dosyaları otomatik olarak kapat**seçeneğini belirleyin. Bu seçenek, dağıtım özelliklerinin **dağıtım ayarları** sekmesinde bulunur.  

> [!Note]
> Yürütülebilir dosyaların çalıştırılmasını denetlemek üzere bir uygulama yapılandırırsanız ve [uygulamayı yüklemeyi uygulama](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) görev sırası adımına eklerseniz, görev sırası bunu yükleyemez. Bu görev dizisi adımını hata durumunda devam etmek için yapılandırmazsanız, tüm görev sırası başarısız olur.

### <a name="client-behaviors-and-user-notifications"></a>İstemci davranışları ve Kullanıcı bildirimleri

İstemciler dağıtımı aldıktan sonra, aşağıdaki davranış geçerlidir:  

- Uygulamayı **kullanılabilir**olarak dağıttıysanız ve bir Kullanıcı yüklemeyi denediğinde, istemci, yüklemeye devam etmeden önce kullanıcıdan belirtilen çalışan yürütülebilir dosyaları kapatmasını ister.  

- Uygulamayı **gerekli**olarak dağıttıysanız ve **dağıtım türü özellikleri iletişim kutusunun Kurulum davranışı sekmesinde belirttiğiniz çalışan tüm yürütülebilir dosyaları otomatik olarak kapatmak**için belirtilmişse, istemci bir bildirim görüntüler. Uygulama yükleme son tarihine ulaşıldığında belirtilen yürütülebilir dosyaların otomatik olarak kapatıldığını kullanıcıya bildirir.  

    - Bu iletişim kutularını istemci ayarlarının **Bilgisayar Aracısı** grubunda zamanlayın. Daha fazla bilgi için bkz. [Bilgisayar Aracısı](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    - Kullanıcının bu iletileri görmesini istemiyorsanız, **Yazılım Merkezi 'Nde gizleme seçeneğini ve** dağıtım özelliklerinin **Kullanıcı deneyimi** sekmesindeki tüm bildirimler ' i seçin. Daha fazla bilgi için bkz. [dağıtım Kullanıcı deneyimi ayarları](#bkmk_deploy-ux).  

- Uygulamayı **gerekli**olarak dağıttıysanız ve **dağıtım türü özellikleri iletişim kutusunun yükleme davranışı sekmesinde belirttiğiniz çalışan tüm yürütülebilir dosyaları otomatik olarak kapatmak**için belirtmediyseniz, belirtilen uygulamalardan biri veya birkaçı çalışıyorsa uygulamanın yüklenmesi başarısız olur.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Azure AD 'ye katılmış cihazlarda Kullanıcı tarafından kullanılabilen uygulamaları dağıtma

<!-- 1322613 -->
Uygulamaları kullanıcılara kullanılabilir olarak dağıtırsanız, Azure Active Directory (Azure AD) cihazlarda yazılım merkezi aracılığıyla bunlara göz atabilir ve bunları yükleyebilir.  

### <a name="prerequisites"></a>Önkoşullar

- Yönetim noktasında HTTPS 'yi etkinleştir  

- Siteyi **bulut yönetimi** IÇIN [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) ile tümleştirme  

    - [Azure AD Kullanıcı bulmayı](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc) yapılandırma  

- Bir uygulamayı Azure AD 'den bir kullanıcı koleksiyonuna kullanılabilir olarak dağıtma  

- Herhangi bir uygulama içeriğini bir [bulut dağıtım noktasına](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) dağıtma  

- İstemci ayarını etkinleştir [Bilgisayar Aracısı](../../core/clients/deploy/about-client-settings.md#computer-agent) grubunda **yeni yazılım merkezi 'ni kullan**  

- İstemci işletim sistemi Windows 10 ve Azure AD 'ye katılmış olmalıdır. Tamamen bulut etki alanına katılmış ya da karma Azure AD 'ye katılmış olarak.  

- Internet tabanlı istemcileri desteklemek için:  

    - [Bulut yönetimi ağ geçidi](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)  

    - İstemci ayarını etkinleştir: [Istemci ilkesi](../../core/clients/deploy/about-client-settings.md#client-policy) grubundaki **Internet istemcilerinden gelen Kullanıcı ilkesi isteklerini etkinleştir**  

- İntranetteki istemcileri desteklemek için:  

    - Bulut dağıtım noktasını istemciler tarafından kullanılan bir sınır grubuna ekleyin  

    - İstemciler, HTTPS özellikli yönetim noktasının tam etki alanı adını (FQDN) çözmelidir  



## <a name="next-steps"></a>Sonraki adımlar

- [Uygulamaları izleme](monitor-applications-from-the-console.md)
- [Uygulama dağıtımları sorunlarını giderme](troubleshoot-application-deployment.md)
- [Uygulamalar için yönetim görevleri](management-tasks-applications.md)
- [Yazılım Merkezi kullanıcı kılavuzu](../../core/understand/software-center.md)
