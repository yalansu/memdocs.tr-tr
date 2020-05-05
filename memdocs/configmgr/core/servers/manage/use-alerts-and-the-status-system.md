---
title: Uyarılar ve durum sistemi
titleSuffix: Configuration Manager
description: Uyarıları yapılandırın ve Configuration Manager dağıtımınızın durumu hakkında bilgi sahibi kalmak için durum sistemini kullanın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c066a61380e09961192bcbe7192e2e945341c97c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720719"
---
# <a name="use-alerts-and-the-status-system-for-configuration-manager"></a>Configuration Manager için uyarıları ve durum sistemini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Uyarıları yapılandırın ve Configuration Manager dağıtımınızın durumu hakkında bilgi sahibi kalmak için yerleşik durum sistemini kullanın.  


##  <a name="status-system"></a><a name="bkmk_Status"></a>Durum sistemi  
 Tüm ana site bileşenleri, site ve hiyerarşi işlemleri ile ilgili geri bildirim sağlayan durum iletileri oluşturur.    Bu bilgiler sayesinde farklı site işlemlerinin sistem durumundan haberdar olabilirsiniz. İlgilenmeniz gereken diğer sorunların erken fark edilmesini sağlamanın yanı sıra, uyarı sistemini bilinen sorunları yoksayacak şekilde ayarlayabilirsiniz.  

 Varsayılan olarak Configuration Manager durum sistemi, çoğu ortam için uygun olan ayarları kullanarak yapılandırma olmadan çalışır. Bununla birlikte, aşağıdakileri yapılandırabilirsiniz:  

-   **Durum Özetleyiciler:** Aşağıdaki dört özetleyici için bir durum göstergesi değişikliği oluşturan her bir sitedeki durum iletilerinin sıklığını denetlemek için durum özetleyicilerini değiştirebilirsiniz:  

    -   Uygulama Dağıtımı Özetleyici  

    -   Uygulama İstatistikleri Özetleyici  

    -   Bileşen Durum Özetleyicisi  

    -   Site Sistem Durumu Özetleyici  

-   **Durum Filtresi Kuralları:** Yeni durum filtresi kuralları oluşturabilir, kuralların önceliklerini değiştirebilir, kuralları devre dışı bırakabilir ya da etkinleştirebilir ve her sitedeki kullanılmayan kuralları silebilirsiniz.  

    > [!NOTE]  
    >  Durum filtresi kuralları dış komutları çalıştırmak üzere ortam değişkenleri kullanmayı desteklemez.  

-   **Durum bildirimi:** Durum iletilerinin Configuration Manager durum sistemine nasıl bildirildiğini değiştirmek için hem sunucu hem de istemci bileşeni raporlamasını yapılandırabilir ve durum iletilerinin nereye gönderileceğini belirtebilirsiniz.  

    > [!WARNING]  
    >  Varsayılan raporlama ayarları çoğu ortam için uygun olduğundan, bunları değiştirirken dikkatli olun. Tüm durum ayrıntılarını bildirmeyi seçerek durum raporlama düzeyini artırdığınızda, işlenecek durum iletilerinin miktarını artırabilir ve bu da Configuration Manager sitesindeki işlem yükünü artırır. Durum bildirim düzeyini azaltırsanız, durum özetleyicilerinin yararlılığını da azaltabilirsiniz.  

Durum sistemi her site için ayrı yapılandırma bulundurur, bu nedenle her site için durum sistemini ayrı olarak değiştirmeniz gerekir.  

###  <a name="procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> Durum sistemini yapılandırma yordamları  

##### <a name="to-configure-status-summarizers"></a>Durum özetleyicilerini yapılandırmak için  

1.  Configuration Manager konsolunda **Yönetim** > **Site yapılandırması** >**siteler**' e gidin ve ardından durum sistemini yapılandırmak istediğiniz siteyi seçin.  

2.  **Giriş** sekmesinde, **Ayarlar** grubunda, **Durum Özeti Hazırlayıcıları**'nı tıklatın.  

3.  **Durum Özeti Hazırlayıcıları** iletişim kutusunda, yapılandırmak istediğiniz durum özetleyicilerini seçin ve **Düzenle** 'yi tıklatarak bu özetleyicinin özelliklerini açın. Uygulama Dağıtımı veya Uygulama İstatistikleri özetleyicisini düzenliyorsanız adım 5 ile devam edin. Bileşen Durumu’nu düzenliyorsanız Adım 6’ya atlayın. Site Sistem Durumu özetleyicisini düzenliyorsanız Adım 7’ye atlayın.  

4.  Uygulama Dağıtımı Özetleyici ya da Uygulama İstatistikleri Özetleyici'nin özellik sayfasını açtıktan sonra aşağıdaki adımları kullanın:  

    1.  Özetleyiciler özellikler sayfasının **Genel** sekmesinde, özetleme aralıklarını yapılandırın ve **Tamam** 'ı tıklatarak özellikler sayfasını kapatın.  

    2.  **Durum Özeti Hazırlayıcıları** iletişim kutusunu kapatmak için **Tamam** 'ı tıklatın ve bu yordamı tamamlayın.  

5.  Bileşen Durumu Özetleyici'nin özellikler sayfasını açtıktan sonra aşağıdaki adımları kullanın:  

    1.  Hazırlayıcıları ' özellikler sayfasının **genel** sekmesinde, çoğaltma ve eşik süresi değerlerini yapılandırın.  

    2.  **Eşikler** sekmesinde, yapılandırmak istediğiniz **İleti türü** 'nü seçin, **Eşikler** listesindeki bir bileşenin adını tıklatın.  

    3.  **Durum Eşiği Özellikleri** iletişim kutusunda, uyarı ve kritik eşik değerlerini düzenleyip **Tamam**'ı tıklatın.  

    4.  Bitirdiğinizde 6.b ve 6.c adımlarını gerektiği şekilde yineleyin ve özetleyici özelliklerini kapatmak için **Tamam** 'ı tıklatın.  

    5.  **Durum Özeti Hazırlayıcıları** iletişim kutusunu kapatmak için **Tamam** 'ı tıklatın ve bu yordamı tamamlayın.  

6.  Site Sistem Durumu Özetleyici'nin özellikler sayfasını açtıktan sonra aşağıdaki adımları kullanın:  

    1.  Hazırlayıcıları ' özellikler sayfasının **genel** sekmesinde, çoğaltma ve zamanlama değerlerini yapılandırın.  

    2.  **Eşikler** sekmesinde, kritik ve uyarı durumu görüntüleme için varsayılan eşikleri yapılandırmak için **Varsayılan eşikler** 'in değerlerini belirtin.  

    3.  Belirli **Depolama nesneleri**değerlerini düzenlemek için, **Özel eşikler** listesinden nesneyi seçin ve depolama nesnelerinin uyarı ve kritik eşiklerini yapılandırmak için **Özellikler** düğmesini tıklatın. Depolama nesneleri özelliklerini kapatmak için **Tamam** 'ı tıklatın.  

    4.  Yeni bir depolama nesnesi oluşturmak için, **Nesne Oluştur** düğmesini tıklatın ve depolama nesnelerinin değerlerini belirtin. Nesnelerin özelliklerini kapatmak için **Tamam** 'ı tıklatın.  

    5.  Bir depolama nesnesini silmek için, nesneyi seçip **Sil** düğmesini tıklatın.  

    6.  7. b ile 7. e arasındaki adımları yineleyin gerektiğinde. Bitirdiğinizde, özetleyicinin özelliklerini kapatmak için **Tamam** 'ı tıklatın.  

    7.  **Durum Özeti Hazırlayıcıları** iletişim kutusunu kapatmak için **Tamam** 'ı tıklatın ve bu yordamı tamamlayın.  

##### <a name="to-create-a-status-filter-rule"></a>Durum filtre kuralı oluşturmak için  

1.  Configuration Manager konsolunda **Yönetim** > **Site yapılandırması** >**siteler**' e gidin ve ardından durum sistemini yapılandırmak istediğiniz siteyi seçin.  

2.  **Giriş** sekmesinde, **Ayarlar** grubunda, **Durum Filtre Kuralları**'nı tıklatın. **Durum Filtre Kuralları** iletişim kutusu açılır.  

3.  **Oluştur**' a tıklayın.  

4.  **Durum Filtre Kuralı Oluşturma Sihirbazı**'nda, **Genel** sayfasında, yeni durum filtre kuralı için bir ad ve kural için ileti eşleştirme ölçütü belirtin ve **İleri**'yi tıklatın.  

5.  **Eylemler** sayfasında, filtre kuralıyla eşleşen bir durum iletisi olduğunda gerçekleştirilecek eylemleri belirtin ve **İleri**'yi tuıklatın.  

6.  **Özet** sayfasında, yeni kuralın ayrıntılarını gözden geçirin ve sihirbazı tamamlayın.  

    > [!NOTE]  
    >  Configuration Manager yalnızca yeni durum filtre kuralının bir adı olmasını gerektirir. Kural oluşturulur, ancak durumu iletilerini işlemek için herhangi bir ölçüt belirtmezseniz, durum filtre kuralının etkisi olmaz. Bu davranış her kural için durum filtre ölçütlerini yapılandırmadan önce kurallar oluşturmanıza ve düzenlemenize olanak sağlar.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Durum filtre kuralını değiştirmek veya silmek için  

1.  Configuration Manager konsolunda **Yönetim** > **Site yapılandırması** >**siteler**' e gidin ve ardından durum sistemini yapılandırmak istediğiniz siteyi seçin.  

2.  **Giriş** sekmesinde, **Ayarlar** grubunda, **Durum Filtre Kuralları**'nı tıklatın.  

3.  **Durum Filtre Kuralları** iletişim kutusunda, değiştirmek istediğiniz kuralı seçin ve aşağıdaki eylemlerden birini gerçekleştirin:  

    -   Durum filtre kuralının işlem sırasını değiştirmek için **Önceliği Arttır** veya **Önceliği Azalt** 'ı tıklatın. Sonra başka bir eylem seçin veya bu görevi tamamlamak üzere bu yordamın 8. adımına geçin.  

    -   Kuralın durumunu değiştirmek için **Devre Dışı Bırak** veya **Etkinleştir** 'i tıklatın. Kuralın durumunu değiştirdikten sonra başka bir eylem seçin veya bu görevi tamamlamak üzere bu yordamın 8. adımına geçin.  

    -   Durum filtre kuralını bu siteden silmek isterseniz **Sil** 'i tıklatın ve eylemi doğrulamak için **Evet** 'i tıklatın. Bir kuralı sildikten sonra başka bir eylem seçin veya bu görevi tamamlamak üzere bu yordamın 8. adımına geçin.  

    -   Durum iletisi kuralının ölçütlerini değiştirmek isterseniz **Düzenle** 'yi tıklatın ve bu yordamın 5. adımından devam edin.  

4.  Durum filtre kuralı özellikler iletişim kutusunun **Genel** sekmesinde, kuralı ve ileti eşleşme ölçütlerini değiştirin.  

5.  **Eylemler** sekmesinde, filtre kuralıyla eşleşen bir durum iletisi olduğunda gerçekleştirilecek eylemleri değiştirin ve İleri'yi tıklatın.  

6.  Değişiklikleri kaydetmek için **Tamam**’a tıklayın.  

7.  **Durum Filtre Kuralları** iletişim kutusunu kapatmak için **Tamam** 'ı tıklatın.  

##### <a name="to-configure-status-reporting"></a>Durum bildirimini yapılandırmak için  

1.  Configuration Manager konsolunda **Yönetim** > **Site yapılandırması** > **siteler**' e gidin ve ardından durum sistemini yapılandırmak istediğiniz siteyi seçin.  

2.  **Ayarlar** grubunun **Giriş** sekmesinde, **Site Bileşenlerini Yapılandır**'ı tıklatıp ardından **Durum Bildirimi**'ni seçin.  

3.  **Durum Bildirim Bileşeni Özellikleri** iletişim kutusunda, raporlamak veya günlüğe kaydetmek istediğiniz sunucu ve istemci bileşeni durum iletilerini belirtin:  

    1.  Durum iletilerini Configuration Manager durum iletisi sistemine göndermek için **raporu** yapılandırın.  

    2.  Durum iletilerinin türünün ve önem derecesinin Windows olay günlüğüne yazılması için **Günlük** ' yapılandırın.  

4.  **Tamam**'a tıklayın.  

###  <a name="monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a>Configuration Manager durum sistemini izleme  
 Configuration Manager **sistem durumu** , hiyerarşinizdeki sitelerin ve site sunucusu işlemlerinin genel işlemlerine genel bir bakış sağlar. Site sistem sunucuları veya bileşenleri için işlem sorunlarını açığa çıkaryükleyebilir ve farklı Configuration Manager işlemlerine yönelik belirli ayrıntıları gözden geçirmek için sistem durumunu kullanabilirsiniz. Sistem durumunu, Configuration Manager konsolundaki **izleme** çalışma alanının **sistem durumu** düğümünden izleyebilirsiniz.  

 Çoğu Configuration Manager site sistemi rolü ve bileşeni durum iletileri oluşturur. Durum iletisi ayrıntıları her bileşenin işlem günlüğüne kaydedilir, ancak özetlenerek her bileşenin veya site sistemi durumunun genel dökümünde sunulduğu site veritabanına gönderilir. Bu durum iletisi dökümleri, normal işlemlere yönelik ayrıntılı bilgilerle birlikte uyarı ve hata ayrıntıları sağlar. Uyarı veya hataların tetiklenme eşiklerini yapılandırabilir ve döküm bilgilerinde sizinle ilgili olmayan bilinen sorunların yoksayılmasını sağlamak ve bu sırada araştırmak isteyebileceğiniz sunuculardaki veya bileşen işlemlerindeki gerçek sorunlara dikkat çekmek için sistemde hassas ayarlar yapabilirsiniz.  

 Sistem durumu, hiyerarşideki diğer sitelere genel veri değil site verileri olarak çoğaltılır. Bu, yalnızca Configuration Manager konsolunuzun bağlandığı sitenin ve o sitenin altındaki tüm alt sitelerin durumunu görebileceğiniz anlamına gelir. Bu nedenle, sistem durumunu görüntülerken Configuration Manager konsolunuzu hiyerarşinizin en üst düzey sitesine bağlamayı göz önünde bulundurun.  

 Farklı sistem durumu görünümlerini ve her birinin ne zaman kullanılacağını belirlemek için aşağıdaki tabloyu kullanın.  

|Node|Daha fazla bilgi|  
|----------|----------------------|  
|Site Durumu|Her site sistemi sunucusunun sistem durumunu incelemek üzere her site sistemi durumunun dökümünü görüntülemek için bu düğümü kullanın. Site sistem durumu, her site için **Site Sistem Durumu Özetleyicisi**'nde yapılandırılan eşiklerce belirlenir.<br /><br /> **Configuration Manager Service Manager**'ı kullanarak her site sisteminin durum iletilerini görüntüleyebilir, durum iletileri için eşikler ayarlayabilir ve site sistemlerindeki bileşenlerin çalışmasını yönetebilirsiniz.|  
|Bileşen Durumu|Bileşenin işletimsel durumunu gözden geçirmek için her bir Configuration Manager bileşenin durumunun bir toplamasını görüntülemek için bu düğümü kullanın. Bileşen durumu, her site için **Site Sistem Durumu Özetleyicisi**'nde yapılandırılan eşiklerce belirlenir.<br /><br /> **Configuration Manager Service Manager**'ı kullanarak her bileşenin durum iletilerini görüntüleyebilir, durum iletileri için eşikler ayarlayabilir ve bileşenlerin çalışmasını yönetebilirsiniz.|  
|Çakışan Kayıtlar|Çakışan kayıtları olabilen istemcilerle ilgili durum iletilerini görüntülemek için bu düğümü kullanın.<br /><br /> Configuration Manager, tekrarlanmış olabilecek istemcileri belirlemeyi denemek ve çakışan kayıtlarla ilgili olarak sizi uyarmak için donanım KIMLIĞINI kullanır. Örneğin, bir bilgisayarı yeniden yüklemeniz gerekiyorsa, donanım KIMLIĞI aynı olacaktır, ancak Configuration Manager kullanılan GUID de değişebilir.|  
|Durum İletisi Sorguları|Belirli olaylarla ilgili durum iletilerini ve bunların ayrıntılarını sorgulamak için bu düğümü kullanın. Belirli olaylarla ilgili durum iletilerini bulmak için durum iletisi sorgularını kullanabilirsiniz.<br /><br /> Belirli bir bileşen, işlem veya Configuration Manager nesnenin ne zaman değiştirildiğini ve bu değişikliği yapmak için kullanılan hesabı belirlemek için çoğunlukla durum iletisi sorgularını kullanabilirsiniz. Örneğin, belirli bir koleksiyonun ne zaman oluşturulduğunu ve o koleksiyonu oluşturmak için kullanılan kullanıcı hesabını belirlemek için **Oluşturulan, Değiştirilen ve Silinen Koleksiyonlar** yerleşik sorgusunu çalıştırabilirsiniz.|  

####  <a name="manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> Site durumunu ve bileşen durumunu yönetme  
 Site durumunu ve bileşen durumunu yönetmek için aşağıdaki bilgileri kullanın:  

-   Durum sistemine yönelik eşikler yapılandırmak için bkz. [Durum sistemini yapılandırma yordamları](#bkmk_configstatus).  

-   Configuration Manager bireysel bileşenleri yönetmek için **Configuration Manager Service Manager**kullanın.  

####  <a name="view-status-messages"></a><a name="bkmk_view"></a> Durum iletilerini görüntüleme  
 Her bir site sistemi sunucusuna veya bileşenine ait durum iletilerini görüntüleyebilirsiniz.  

 Configuration Manager konsolundaki durum iletilerini görüntülemek için belirli bir site sistemi sunucusunu veya bileşenini seçin ve ardından **Iletileri göster**' e tıklayın. İletileri görüntülerken belirli ileti türlerini veya belirli bir zamana ait iletileri görüntülemeyi seçebilir ve sonuçları durum iletisi ayrıntılarına göre filtreleyebilirsiniz.  

##  <a name="alerts"></a><a name="bkmk_Alerts"></a>Larınız  
 Configuration Manager uyarıları, belirli bir koşul oluştuğunda bazı işlemler tarafından oluşturulur.  

- Normalde, çözümlemeniz gereken bir hata oluştuğunda uyarılar oluşturulur.  

- Uyarılar, durumu izlemeye devam edebilmeniz için bir koşul oluştuğunda sizi uyarmak amacıyla da oluşturulabilir  

- Endpoint Protection ve istemci durumu gibi uyarıları kendiniz yapılandırırsınız, ancak diğer uyarılar otomatik olarak yapılandırılır  

- Uyarılara ait abonelikleri yapılandırarak bu uyarıların ayrıntıları e-postayla göndermesini sağlayabilir ve temel sorunlar hakkında daha fazla bilgi sahibi olabilirsiniz  

  Configuration Manager 'de uyarıların ve uyarı aboneliklerinin nasıl yapılandırılacağı hakkında bilgi edinmek için aşağıdaki tabloyu kullanın:  


|Eylem|Daha Fazla Bilgi|  
|------------|----------------------|  
|Bir koleksiyon için Endpoint Protection uyarılarını yapılandırma|Yapılandırma bölümünde **Configuration Manager Endpoint Protection uyarılarını yapılandırma** bölümüne bakın [Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)|  
|Koleksiyon için istemci durumu uyarılarını yapılandırma|Bkz. [istemci durumunu yapılandırma](../../../core/clients/deploy/configure-client-status.md).|  
|Configuration Manager uyarılarını yönetme|Bu konudaki [Management tasks for alerts](#BKMK_Manage) bölümüne bakın.|  
|Uyarılar için e-posta aboneliklerini yapılandırma|Bu konudaki [Uyarılar Için yönetim görevleri](#BKMK_Manage) bölümüne bakın.|  
|Uyarıları izleme|Bu konudaki [Uyarıları izleme](#BKMK_MonitorAlerts)|  

###  <a name="management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Genel uyarıları yönetmek için  

1. Configuration Manager konsolunda **izleme** > **uyarıları**' na gidin ve ardından bir yönetim görevi seçin.  

   Seçmeden önce bazı bilgiler gerektirebilen yönetim görevleri hakkında daha fazla bilgi için aşağıdaki tabloyu kullanın.  

|Yönetim görevi|Ayrıntılar|  
    |---------------------|-------------|  
    |**Yapılandır**|Seçili uyarının adını, önem derecesini ve eşiklerini değiştirebileceğiniz * &lt;uyarı adı*\>**özellikleri** iletişim kutusunu açar. Uyarının önem derecesini değiştirirseniz bu yapılandırma, uyarıların Configuration Manager konsolunda nasıl görüntülendiğini etkiler.|  
    |**Açıklamayı Düzenle**|Seçilen uyarılar için bir açıklama girin. Bu açıklamalar Configuration Manager konsolundaki uyarıyla birlikte görüntülenir.|  
    |**Ertele**|Belirtilen tarihe ulaşılana kadar uyarının izlenmesini askıya alır. Belirtilen tarihte, uyarı durumu güncelleştirilir.<br /><br /> Yalnızca etkin olması durumunda bir uyarıyı erteleyebilirsiniz.|  
    |**Abonelik oluşturma**|Seçilen uyarı için bir e-posta aboneliği oluşturabileceğiniz **Yeni Abonelik** iletişim kutusunu açar.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Koleksiyonun istemci durumu uyarılarını yapılandırmak için  

1.  Configuration Manager konsolunda, **varlıklar ve uyum** >   **Cihaz Koleksiyonları**' na tıklayın.  

2.  **Cihaz Koleksiyonları** listesinde, uyarıları yapılandırmak istediğiniz koleksiyonu seçin ve sonra **Giriş** sekmesinde, **Özellikler** grubunda **Özellikler**'i tıklatın.  

    > [!NOTE]  
    >  Kullanıcı koleksiyonları için uyarılar yapılandıramasınız.  

3.  \>**Properties** *Koleksiyon adı Özellikler iletişim kutusunun uyarılar sekmesinde Ekle &lt;*' ye tıklayın. **Alerts** **Add**  

    > [!NOTE]  
    >  **Uyarılar** sekmesi yalnızca, ilişkilendirilmiş olduğunuz güvenlik rolünün uyarılarla ilgili izinleri varsa görünür.  

4.  **Yeni Koleksiyon Uyarıları Ekle** iletişim kutusunda, istemci durumu eşikleri belirli bir değerin altında kaldığında oluşturulmasını istediğiniz uyarıları seçin ve **Tamam**'ı tıklatın.  

5.  **Uyarılar** sekmesinin **Koşullar** listesinde, her istemci durumu uyarısını seçip aşağıdaki bilgileri belirtin.  

    -   **Uyarı adı** -varsayılan adı kabul edin veya uyarı için yeni bir ad girin.  

    -   **Uyarı önem derecesi** -aşağı açılan listeden Configuration Manager konsolunda görüntülenecek uyarı düzeyini seçin.  

    -   **Uyarı oluştur** -uyarı için eşik yüzdesini belirtin.  

6.  \>**Properties** *Koleksiyon adı Özellikler iletişim kutusunu kapatmak için Tamam &lt;*' ı tıklatın. **OK**  

##### <a name="to-configure-email-notification-for-alerts"></a>Uyarıların e-posta bildirimini yapılandırmak için  

1.  Configuration Manager konsolunda **izleme** > **uyarıları** > **abonelikleri**' ne gidin.  

2.  **Oluştur** grubunun **Giriş** sekmesinde, **E-posta Bildirimini Yapılandır**'ı tıklatın.  

3.  **E-posta Bildirimi Bileşen Özellikleri** iletişim kutusunda aşağıdaki bilgileri belirtin:  

    -   **Uyarılar için e-posta bildirimini etkinleştir**: e-posta uyarıları göndermek üzere bir SMTP sunucusu kullanmak Configuration Manager etkinleştirmek için bu onay kutusunu işaretleyin.  

    -   **E-posta uyarıları gönderilecek SMTP sunucusunun FQDN’si veya IP Adresi**: Bu uyarılar için kullanmak istediğiniz e-posta sunucusuna ait SMTP bağlantı noktasının tam etki alanı adını (FQDN) veya IP adresini girin.  

    -   **SMTP sunucusu bağlantı hesabı**: e-posta sunucusuna bağlanmak için kullanılacak Configuration Manager kimlik doğrulama yöntemini belirtin.  

    -   **E-posta uyarıları için gönderen adresi**: Uyarı e-postalarının gönderildiği e-posta adresini belirtin.  

    -   **Test SMTP Sunucusu**: **E-posta uyarıları için gönderen adresi**alanında belirtilen e-posta adresine bir test e-postası gönderir.  

4.  Ayarları kaydetmek ve **E-posta Bildirimi Bileşen Özellikleri** iletişim kutusunu kapatmak için **Tamam** ’a tıklayın.  

##### <a name="to-subscribe-to-email-alerts"></a>E-posta uyarılarına abone olmak için  

1.  Configuration Manager konsolunda **izleme** > **uyarıları**' na gidin.  

2.  Bir uyarı seçtikten sonra, **Giriş** sekmesinde bulunan **Abonelik** grubunda, **Abonelik oluştur**seçeneğine tıklayın.  

3.  **Yeni Abonelik** iletişim kutusunda aşağıdaki bilgileri belirtin:  

    -   **Ad**: E-posta aboneliğini tanımlamak için bir ad girin. En fazla 255 karakter kullanabilirsiniz.  

    -   **E-posta adresi**: Uyarının gönderilmesini istediğiniz e-posta adresini girin. Birden fazla e-posta adresini noktalı virgülle ayırabilirsiniz.  

    -   **E-posta dili**: Listede, e-postanın dilini belirtin.  

4.  **Yeni Abonelik** iletişim kutusunu kapatmak ve e-posta aboneliğini oluşturmak için **Tamam** ’a tıklayın.  

    > [!NOTE]  
    >  **İzleme** çalışma alanında, **Uyarılar** düğümünü genişlettikten sonra **Abonelikler** düğümüne tıklayarak abonelikleri silebilir ve düzenleyebilirsiniz.  

###  <a name="monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a> Uyarıları izleme  
 Uyarıları **İzleme** çalışma alanının **Uyarılar** düğümünde görüntüleyebilirsiniz. Uyarılar şu uyarı durumlarından birine sahiptir:  

- **Asla tetiklenmez**: Uyarının koşulu karşılanmadı.  

- **Etkin**: Uyarının koşulu karşılandı.  

- **İptal edildi**: Etkin olan uyarının koşulu artık karşılanmıyor. Bu durum, uyarıya neden olan koşulun artık çözümlendiğini gösterir.  

- **Ertelendi**: bir yönetici kullanıcı, uyarının durumunu daha sonra değerlendirmek için Configuration Manager yapılandırmış.  

- **Devre dışı**: Uyarı, yönetici kullanıcı tarafından devre dışı bırakıldı. Bir uyarı bu durumdayken, uyarının durumu değişse bile uyarıyı güncelleştirmez Configuration Manager.  

  Configuration Manager bir uyarı oluşturduğunda aşağıdaki işlemlerden birini yapabilirsiniz:  

- Uyarıya neden olan durumu düzeltin, örneğin, uyarıyı oluşturan bir ağ sorununu veya yapılandırma sorununu giderin. Configuration Manager, sorunun artık mevcut olmadığını algıladığında, uyarı durumu **iptal**olarak değişir.  

- Uyarı bilinen bir sorunsa, uyarıyı belirli bir süre için erteleyebilirsiniz. Bu sırada, uyarıyı geçerli durumuna güncelleştirir Configuration Manager.  

   Uyarı etkinken onu erteleyebilirsiniz.  

- Diğer yönetici kullanıcıların uyarıdan haberdar olduğunuzu görebilmeleri için uyarının **Açıklama** 'sını düzenleyebilirsiniz. Örneğin, açıklamada koşulu nasıl çözümleyebileceğinizi tanımlayabilir, koşulun geçerli durumuyla ilgili bilgiler sağlayabilir veya uyarıyı neden ertelediğinizi açıklayabilirsiniz.  
