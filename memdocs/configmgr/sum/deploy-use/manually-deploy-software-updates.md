---
title: Yazılım güncelleştirmelerini el ile dağıtma
titleSuffix: Configuration Manager
description: Gerekli yazılım güncelleştirmeleriyle istemcilerinizi güncel duruma getirmek veya bant dışı güncelleştirmeleri dağıtmak için yazılım dağıtımlarını el ile oluşturun.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: b7d6640beb9353d5c613cf38e3f880e7fd76b393
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717093"
---
# <a name="manually-deploy-software-updates"></a>Yazılım güncelleştirmelerini el ile dağıtma  

*Uygulama hedefi: Configuration Manager (geçerli dal)*

El ile yapılan yazılım güncelleştirme dağıtımı, Configuration Manager konsolundan yazılım güncelleştirmelerini seçme ve dağıtım işlemini el ile başlatma işlemidir. Veya seçili yazılım güncelleştirmelerini bir güncelleştirme grubuna ekleyin ve ardından güncelleştirme grubunu el ile dağıtın. Gerekli yazılım güncelleştirmeleriyle istemcilerinizi güncel duruma getirmek için genellikle el ile dağıtımları kullanırsınız. Ardından, devam eden aylık yazılım güncelleştirme dağıtımlarını yönetmek için otomatik dağıtım kuralları (ADR) kullanabilirsiniz. Ayrıca bant dışı yazılım güncelleştirmelerini dağıtmak için bu el ile yöntemi kullanın. Sizin için uygun olan dağıtım yöntemi hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmelerini dağıtma](deploy-software-updates.md).



##  <a name="step-1-specify-search-criteria-for-software-updates"></a><a name="BKMK_1SearchCriteria"></a>1. Adım: yazılım güncelleştirmeleri için arama ölçütlerini belirtme  

Sitenizin eşitlendiği ürünlerin ve sınıflandırmaların birleşimlerine bağlı olarak, Configuration Manager konsolunda görüntülenen binlerce yazılım güncelleştirmesi vardır. Yazılım güncelleştirmelerini elle dağıtmaya yönelik iş akışındaki ilk adım, dağıtmak istediğiniz yazılım güncelleştirmesinin tanımlanmasıdır. Örneğin, bir **güvenlik** veya **kritik** sınıflandırmayla 50 ' den fazla istemci cihazından gereken tüm yazılım güncelleştirmelerini gösterin.  

> [!IMPORTANT]  
>  Tek bir yazılım güncelleştirme dağıtımında 1000 yazılım güncelleştirmesi sınırlaması vardır.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Yazılım güncelleştirmeleri için arama ölçütlerini belirtme işlemi  

1.  Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **yazılım güncelleştirmeleri**' ni genişletin ve **tüm yazılım güncelleştirmeleri**' ne tıklayın. Bu düğüm eşitlenmiş tüm yazılım güncelleştirmelerini görüntüler.  

    > [!NOTE]  
    >  **Tüm yazılım güncelleştirmeleri** düğümü, yalnızca son 30 gün Içinde yayınlanan **kritik** ve **güvenlik** sınıflandırmasına sahip yazılım güncelleştirmelerini görüntüler.  

2.  Arama bölmesinde, ihtiyacınız olan yazılım güncelleştirmelerini tanımlamak için filtreleyin. Aşağıdaki seçeneklerden birini veya her ikisini birden kullanın:  

    -   Arama metin kutusuna yazılım güncelleştirmelerini filtreleyen bir arama dizesi yazın. Örneğin, belirli bir yazılım güncelleştirmesi için makaleyi veya bülten KIMLIĞINI yazın. Ya da çeşitli yazılım güncelleştirmelerinin başlığında görüntülenen bir dize girin.  

    -   **Ölçüt Ekle**' ye tıklayın ve yazılım güncelleştirmelerini filtrelemek için kriterleri seçin. **Ekle**' ye tıklayın ve ardından ölçütlerin değerlerini belirtin.  

3.  Yazılım güncelleştirmelerini filtrelemek için **Ara**'yı tıklatın.  

    > [!TIP]  
    >  Sık kullanılan filtre ölçütlerini kaydedin. Şeritte, **geçerli aramayı kaydetme**seçeneğine tıklayın. **Kayıtlı aramalara**tıklayarak önceki aramaları alın.   



##  <a name="step-2-create-a-software-update-group-that-contains-the-software-updates"></a><a name="BKMK_2UpdateGroup"></a>2. Adım: yazılım güncelleştirmelerini içeren bir yazılım güncelleştirme grubu oluşturma   

Yazılım güncelleştirme grupları, dağıtım hazırlığı için yazılım güncelleştirmelerini düzenlemenize olanak tanır. Yazılım güncelleştirmelerini yeni bir yazılım güncelleştirme grubuna el ile eklemek için aşağıdaki yordamı kullanın.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Yazılım güncelleştirmelerini yeni bir yazılım güncelleştirme grubuna el ile ekleme işlemi  

1.  Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin ve **yazılım güncelleştirmeleri**' ni seçin. İstediğiniz yazılım güncelleştirmelerini seçin.  

2.  Şeritte **yazılım güncelleştirme grubu oluştur** ' a tıklayın.  

3.  Yazılım güncelleştirme grubunun adını belirtin ve isteğe bağlı olarak bir açıklama belirtin. Yazılım güncelleştirme grubunda hangi tür güncelleştirmelerin olduğunu belirlemek için yeterli bilgi sağlayan bir ad ve açıklama kullanın. **Oluştur**' a tıklayın.  

4.  **Yazılım güncelleştirme grupları** düğümünü seçin ve yeni yazılım güncelleştirme grubunu seçin. Gruptaki güncelleştirmelerin listesini görüntülemek için şeritte **üyeleri göster** ' e tıklayın.  



##  <a name="step-3-download-the-content-for-the-software-update-group"></a><a name="BKMK_3DownloadContent"></a>3. Adım: yazılım güncelleştirme grubu içeriğini Indirin  

Yazılım güncelleştirmelerini dağıtmadan önce yazılım güncelleştirme grubundaki yazılım güncelleştirmelerinin içeriğini indirin. Bu adım, yazılım güncelleştirmelerini dağıtmadan önce içeriğin dağıtım noktalarında kullanılabilir olduğunu doğrulamanızı sağlar. Ayrıca içerik dağıtımı ile ilgili beklenmeyen sorunları önlemenize yardımcı olur. Bu adımı atlarsanız, dağıtım işleminin bir parçası olarak site içeriği indirir ve dağıtım noktalarına dağıtır. Yazılım güncelleştirme grubundaki yazılım güncelleştirme içeriğini indirmek için aşağıdaki yordamı kullanın.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Yazılım güncelleştirme grubu için içerik indirme işlemi
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>İçerik durumunu izlemek için işlem
1. Yazılım güncelleştirmelerinin içerik durumunu izlemek için Configuration Manager konsolundaki **izleme** çalışma alanına gidin. **Dağıtım durumu**' nu genişletin ve **İçerik durumu** düğümünü seçin.  

2. Daha önce yazılım güncelleştirme gurubunda yazılım güncelleştirmelerini yüklemek için tanımladığınız yazılım güncelleştirme paketini seçin.  

3. Şeritte **durumu görüntüle** ' ye tıklayın.  



##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_4DeployUpdateGroup"></a>4. Adım: yazılım güncelleştirme grubunu dağıtma  

Dağıtmak istediğiniz güncelleştirmeleri belirledikten ve bunları bir yazılım güncelleştirme grubuna ekledikten sonra, yazılım güncelleştirme grubunu el ile dağıtın.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Yazılım güncelleştirmelerini bir yazılım güncelleştirme grubuna el ile dağıtmak için işlem  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **yazılım güncelleştirmeleri**' ni genişletin ve **yazılım güncelleştirme grupları** düğümünü seçin.  

2. Dağıtmak istediğiniz yazılım güncelleştirme grubunu seçin. Şeritte **Dağıt** ' a tıklayın.   

3. Yazılım güncelleştirmelerini dağıtma Sihirbazı 'nın **genel** sayfasında, aşağıdaki ayarları yapılandırın:  

   -   **Ad**: Dağıtımın adını belirtin. Dağıtım, amacını açıklayan benzersiz bir ada sahip olmalıdır ve sitedeki diğer dağıtımlardan farklılaştırır. Bu ad alanı 256 karakterlik bir sınıra sahiptir. Varsayılan olarak, Configuration Manager otomatik olarak dağıtım için aşağıdaki biçimde bir ad sağlar:`Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Açıklama**: Dağıtım için bir açıklama belirtin. Açıklama isteğe bağlıdır, ancak dağıtıma genel bir bakış sağlar. Sitedeki diğer kullanıcılarla ayırt edilmesine ve ayırt edilmesine yardımcı olan diğer ilgili bilgileri de ekleyin. Açıklama alanı 256 karakterlik bir sınıra sahiptir ve varsayılan olarak boş değere sahiptir.  

   -   **Yazılım güncelleştirmesi/yazılım güncelleştirme grubu**: görüntülenen yazılım güncelleştirme grubunun veya yazılım güncelleştirmesinin doğru olduğundan emin olun.  

   -   **Dağıtım Şablonu Seçin**: Önceden kaydedilmiş bir dağıtım şablonunun uygulanıp uygulanmayacağını belirtin. Ortak yazılım güncelleştirme dağıtım özelliklerini kaydetmek için bir dağıtım şablonu yapılandırın. Ardından, gelecekte yazılım güncelleştirmelerini dağıtırken şablonu uygulayın. Bu şablonlar, benzer dağıtımlar arasında tutarlılık sağlamaya yönelik zaman kazandırır ve yardım sağlar.  

   -   **Koleksiyon**: dağıtım için koleksiyon belirtin. Koleksiyondaki cihazlar bu Dağıtımdaki yazılım güncelleştirmelerini alır.  

4. **Dağıtım ayarları** sayfasında, aşağıdaki ayarları yapılandırın:  

   -   **Dağıtım türü**: Yazılım güncelleştirmesi dağıtımı için dağıtım türünü belirtin.  

       > [!IMPORTANT]  
       >  Yazılım güncelleştirme dağıtımını oluşturduktan sonra, dağıtım türünü değiştiremezsiniz.  

        - Zorunlu bir yazılım güncelleştirme dağıtımı oluşturmak için **gerekli** ' yi seçin. Yazılım güncelleştirmeleri, yapılandırdığınız yükleme son tarihinden önce istemcilere otomatik olarak yüklenir.  

        - İsteğe bağlı bir yazılım güncelleştirme dağıtımı oluşturmak için **kullanılabilir** ' i seçin. Bu dağıtım, kullanıcıların yazılım merkezi 'nden yüklemesi için kullanılabilir.  

       > [!NOTE]  
       >  Yazılım güncelleştirme grubunu **gerektiği**şekilde dağıttığınızda, istemciler içeriği arka planda indirir ve yapılandırılmışsa BITS ayarlarını kabul edin.  
       > 
       > **Kullanılabilir**olarak dağıtılan yazılım güncelleştirme grupları için, istemciler içeriği ön planda INDIRIR ve BITS ayarlarını yoksayar.  

   -   **Gerekli dağıtımlarda istemcileri uyandırmak IÇIN lan 'Da uyandırma 'Yı kullan**: son tarihte LAN'da Uyandırma etkinleştirilip etkinleştirilmeyeceğini belirtir. LAN'da Uyandırma dağıtımda bir veya daha fazla yazılım güncelleştirmesi gerektiren bilgisayarlara Uyandırma paketleri gönderir. Site, yüklemenin başlatılması için, yükleme son tarihinde uyku modunda olan tüm bilgisayarları uyandırır. Dağıtımda yazılım güncelleştirmesi gerektirmeyen uyku modundaki istemciler başlatılmaz. Varsayılan olarak bu ayar etkin değildir. Yalnızca **gerekli** dağıtımlar için kullanılabilir. Bu seçeneği kullanmadan önce LAN'da Uyandırma için bilgisayarları ve ağları yapılandırın. Daha fazla bilgi için bkz. [nasıl yapılandırılır LAN'da Uyandırma](../../core/clients/deploy/configure-wake-on-lan.md).  

   -   **Ayrıntı düzeyi**: istemcilerin siteye rapor veren durum iletileri için ayrıntı düzeyini belirtin.  

5. **Zamanlama** sayfasında, aşağıdaki ayarları yapılandırın:  

   -   **Değerlendirmeyi zamanla**: Configuration Manager, kullanılabilir saat ve yükleme son tarih zamanlarını değerlendiren süreyi belirtin. Eşgüdümlü Evrensel Saat (UTC) veya Configuration Manager konsolunu çalıştıran bilgisayarın yerel saatini kullanmayı seçin.  

       - Burada **istemci yerel saati** ' ni seçip **Yazılım kullanılabilir saati**için **mümkün olan en kısa sürede** ' yi seçtiğinizde, güncelleştirmelerin ne zaman kullanılabilir olduğunu değerlendirmek için Configuration Manager konsolunu çalıştıran bilgisayardaki geçerli saat kullanılır. Bu davranış, **yükleme son tarihi** ve güncelleştirmelerin bir istemciye yüklendiği zaman ile aynıdır. İstemci farklı bir saat dilimindeyse bu eylemler, istemcinin saati değerlendirme saatine ulaştığında gerçekleşir.  

   -   **Yazılım uygunluk saati**: Yazılım güncelleştirmelerinin istemciler için ne zaman kullanılabilir olduğunu belirtmek için aşağıdaki ayarlardan birini seçin:  

       -   **Mümkün olan en kısa sürede**: Dağıtımdaki yazılım güncelleştirmelerinin istemciler için mümkün olan en kısa sürede kullanılabilmesini sağlar. Dağıtımı bu ayar seçili olarak oluşturduğunuzda, Configuration Manager istemci ilkesini güncelleştirir. Bir sonraki istemci ilkesi yoklama döngüsünün, istemcileri dağıtımdan haberdar edilir ve yazılım güncelleştirmeleri yükleme için kullanılabilir hale gelir.  

       -   **Belirli bir süre**: dağıtıma dahil edilen yazılım güncelleştirmelerini belirli bir tarih ve saatte istemciler için kullanılabilir hale getirir. Bu ayar etkinken dağıtımı oluşturduğunuzda Configuration Manager istemci ilkesini güncelleştirir. Bir sonraki istemci ilkesi yoklama döngüsünden istemciler, dağıtımın farkında olur. Ancak, Dağıtımdaki yazılım güncelleştirmeleri, yapılandırılan tarih ve saate kadar, yükleme için kullanılamaz.  

   -   **Yükleme son tarihi**: Bu seçenekler yalnızca **gerekli** dağıtımlar için kullanılabilir. Dağıtımdaki yazılım güncelleştirmeleri için yükleme son tarihini belirtmek üzere aşağıdaki ayarlardan birini seçin  

       -   **Mümkün olan en kısa sürede**: Dağıtımdaki yazılım güncelleştirmelerinin mümkün olan en kısa sürede otomatik olarak yüklenmesi için bu ayarı seçin.  

       -   **Belirli bir zamanda**: Dağıtımdaki yazılım güncelleştirmelerini belirli bir tarih ve saatte otomatik olarak yüklemek için bu ayarı seçin.  

           - Gerçek yükleme son tarih saati, en fazla iki saate kadar rastgele bir süre ile görüntülenir. Rasgeleleştirme, koleksiyondaki istemcilerin aynı anda dağıtımdaki güncelleştirmeleri yükleyen potansiyel etkisini azaltır.   

           - Gerekli yazılım güncelleştirmeleri için yükleme rastgele gecikmesini devre dışı bırakmak için, istemci ayarını **Bilgisayar Aracısı** grubundaki **rastgele son tarih seçimini devre dışı bırakacak** şekilde yapılandırın. Daha fazla bilgi için bkz. [Bilgisayar Aracısı istemci ayarları](../../core/clients/deploy/about-client-settings.md#computer-agent).  

   -  **İstemci ayarlarında tanımlanan yetkisiz kullanım süresine kadar bu dağıtımın uygulanmasını kullanıcı tercihlerine göre geciktir**: kullanıcıların gerekli yazılım güncelleştirmelerini son tarihten sonra yüklemesi daha fazla zaman vermesi için bu ayarı etkinleştirin.  

       - Bu davranış, genellikle bir bilgisayar uzun süredir kapalıyken gereklidir ve birçok yazılım güncelleştirmesi ya da uygulama yüklemesi gerekir. Örneğin, bir Kullanıcı tatilden döndüğünde, istemci vadesi geçmiş dağıtımları yüklerken uzun süre beklemelidir.  

       - Bu yetkisiz kullanım süresini, istemci ayarlarındaki **dağıtım son tarihi (saat) sonra zorlama için özellik yetkisiz kullanım** süresiyle yapılandırın. Daha fazla bilgi için [Bilgisayar Aracısı](../../core/clients/deploy/about-client-settings.md#computer-agent) bölümüne bakın. Zorlama yetkisiz kullanım süresi, bu seçenek etkinleştirilmiş ve istemci ayarını dağıttığınız cihazlara hedeflenmiş tüm dağıtımlar için geçerlidir.  

       - Son tarihten sonra istemci, yazılım güncelleştirmelerini kullanıcı tarafından yapılandırılan ve bu yetkisiz kullanım süresine kadar olan ilk iş dışı pencereye yüklenir. Ancak, Kullanıcı hala yazılım merkezini açabilir ve yazılım güncelleştirmelerini dilediğiniz zaman yükleyebilir. Yetkisiz kullanım süresi dolduktan sonra, zorlama süresi dolan dağıtımlar için normal davranışa geri döner.  

6. **Kullanıcı deneyimi** sayfasında, aşağıdaki ayarları yapılandırın:  

   -   **Kullanıcı bildirimleri**: Yazılım Merkezi 'Nde yapılandırılan **yazılım kullanım zamanında**bildirimin görüntülenip görüntülenmeyeceğini belirtin. Bu ayar ayrıca kullanıcılara istemci bilgisayarlarda bildirim yapılıp yapılmayacağını da denetler. **Kullanılabilir** dağıtımlar Için, **Yazılım Merkezi 'nde ve tüm bildirimlerde gizleme**seçeneğini seçemezsiniz.  

   -   **Son tarih davranışı**: Bu ayar yalnızca **gerekli** dağıtımlar için yapılandırılabilir. Yazılım güncelleştirme dağıtımı, tüm tanımlı bakım pencerelerinin dışında son tarihe ulaştığında davranışları belirtin. Seçenekler, yazılım güncelleştirmelerinin yüklenip yüklenmeyeceğini ve yükleme sonrasında sistemin yeniden başlatılması yapılıp yapılmayacağını içerir. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md). 
  
       > [!Note]
       > Bu, yalnızca bakım penceresi istemci cihaz için yapılandırıldığında geçerlidir. Cihazda herhangi bir bakım penceresi tanımlanmazsa, yükleme ve yeniden başlatma güncelleştirmesi her zaman son tarihten sonra gerçekleşecektir.

   -   **Cihaz yeniden başlatma davranışı**: Bu ayar yalnızca **gerekli** dağıtımlar için yapılandırılabilir. Güncelleştirme yüklemesinin tamamlanabilmesi için yeniden başlatma gerekirse, sunucularda ve iş istasyonlarında sistemin yeniden başlatılmasının engellenip engellenmeyeceğini belirtin.  

       > [!WARNING]  
       >  Sistem yeniden başlatmaları gizleme sunucu ortamlarında veya hedef bilgisayarların varsayılan olarak yeniden başlatılmasını istemediğiniz durumlarda yararlı olabilir. Ancak bunu yapmak bilgisayarları güvenli olmayan bir durumda bırakabilir. Zorla yeniden başlatmaya izin verilmesi, yazılım güncelleştirme yüklemesinin anında tamamlanmasını sağlamaya yardımcı olur.  

   -   **Windows Embedded cihazlar için filtre Işleme yaz**: Bu ayar, yazma filtresiyle etkinleştirilen Windows Embedded cihazlarındaki yükleme davranışını denetler. Yükleme son tarihinde veya bakım penceresi sırasında değişiklikleri Yürüt seçeneğini belirleyin. Bu seçeneği belirlediğinizde, yeniden başlatma gerekir ve değişiklikler cihazda kalır. Aksi takdirde, güncelleştirme yüklenir, geçici katmana uygulanır ve daha sonra kaydedilir.  

       -  Windows Embedded cihazına bir yazılım güncelleştirmesi dağıttığınızda, cihazın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun.  

   - **Yazılım güncelleştirmeleri dağıtımı yeniden başlatma sırasında yeniden değerlendirme davranışı**: yazılım güncelleştirmeleri dağıtımlarını, bir istemci yazılım güncelleştirmelerini yükledikten ve yeniden başlatıldıktan hemen sonra bir yazılım güncelleştirmeleri uyumluluk taraması çalıştıracak şekilde yapılandırmak için bu ayarı seçin. Bu ayar, istemcinin, istemci yeniden başlatıldıktan sonra geçerli hale gelen ek güncelleştirmeleri denetlemesini sağlar ve aynı bakım penceresi sırasında bunları yüklenir.  

7. **Uyarılar** sayfasında, bu dağıtım için Configuration Manager uyarıları nasıl üretir yapılandırın. **Yazılım kitaplığı** çalışma alanının **yazılım güncelleştirmeleri** düğümündeki Configuration Manager 'deki son yazılım güncelleştirme uyarılarını gözden geçirin. System Center Operations Manager kullanıyorsanız, uyarılarını da yapılandırın. Yalnızca **gerekli** dağıtımlar için uyarıları yapılandırın.  

8. **Yükleme ayarları** sayfasında, aşağıdaki ayarları yapılandırın:  

    > [!NOTE]  
    >  İstemciler, dağıtımdaki yazılım güncelleştirmeleri için bir yönetim noktasından içerik konumunu ister. Yükleme davranışı, dağıtım noktasını, dağıtım paketini ve bu sayfadaki ayarları nasıl yapılandırdığınıza bağlıdır.  

    - İstemcilerin bir komşudan veya varsayılan site sınır gruplarından bir dağıtım noktası kullandıklarında güncelleştirmeleri indirip yüklemesi gerekip gerekmediğini belirtin.  

    - İstemcilerin, yazılım güncelleştirmeleri için içerik geçerli veya komşu sınır gruplarındaki bir dağıtım noktasından kullanılamadığında, güncelleştirmeleri site varsayılan sınır grubundaki bir dağıtım noktasından indirmesi ve yüklemesi gerekip gerekmediğini belirtin.  

    - **İstemcilerin aynı alt ağdaki diğer istemcilerle içerik paylaşmasına izin ver**: İçerik yüklemeleri için BranchCache kullanımının etkinleştirilip etkinleştirilmeyeceğini belirtin. Daha fazla bilgi için bkz. [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Sürüm 1802 ' den başlayarak, BranchCache her zaman istemcilerde etkindir. İstemciler, dağıtım noktası destekliyorsa BranchCache kullandığından, bu ayar kaldırılır.  

    - **Yazılım güncelleştirmeleri geçerli, komşu veya site sınır gruplarındaki dağıtım noktasında yoksa, Microsoft Updates 'ten içerik indirin**: dağıtım noktalarında güncelleştirmeler yoksa, intranet bağlantılı istemcilerin Microsoft Update yazılım güncelleştirmelerini indirmesini sağlamak için bu ayarı seçin. Internet tabanlı istemciler, her zaman yazılım güncelleştirme içerikleri için Microsoft Update 'ye gider.

    - Tarifeli İnternet bağlantıları kullandıklarında, yükleme son tarihinden sonra istemcilerin indirmelerine izin verilip verilmeyeceğini belirtin. Tarifeli bir bağlantıda olduğunuzda, Internet sağlayıcıları bazen gönderme ve alma yaptığınız veri miktarına göre ücretlendirilir.  

9. **Dağıtım paketi** sayfasında, aşağıdaki seçeneklerden birini seçin:  

    > [!Note]  
    > Daha önce [3. Adım: yazılım güncelleştirme grubu Içeriğini indirme](#BKMK_3DownloadContent)seçeneğini gerçekleştirdiyseniz, sihirbaz **dağıtım paketini**, **dağıtım noktalarını**ve **Dil seçimi** sayfalarını göstermez. Sihirbazın [Özet](#bkmk_summary) sayfasına atlayın.  
    > 
    >  Daha önce site sunucusundaki içerik kitaplığına indirilmiş olan yazılım güncelleştirmeleri tekrar yüklenmez. Bu davranış, yazılım güncelleştirmeleri için yeni bir dağıtım paketi oluşturduğunuz zaman bile geçerlidir. Tüm yazılım güncelleştirmeleri zaten indirildiyse sihirbaz [Özet](#bkmk_summary) sayfasına atlar.  

    - **Bir dağıtım paketi seçin**: Bu güncelleştirmeleri mevcut bir dağıtım paketine ekleyin.  

    - **Yeni dağıtım paketi oluştur**: Bu güncelleştirmeleri yeni bir dağıtım paketine ekleyin. Aşağıdaki ek ayarları yapılandırın:  

        -  **Ad**: Dağıtım paketinin adını belirtin. Paket içeriğini açıklayan benzersiz bir ad kullanın. 50 karakterle sınırlıdır.  

        -  **Açıklama**: Dağıtım paketiyle ilgili bilgi sağlayan bir açıklama belirtin. İsteğe bağlı Açıklama 127 karakterle sınırlıdır.  

        -  **Paket kaynağı**: Yazılım güncelleştirmesi kaynak dosyalarının konumunu belirtin. Kaynak konumu için bir ağ yolu yazın (örneğin `\\server\sharename\path`,) veya ağ konumunu bulmak için **Araştır** ' a tıklayın. Sonraki sayfaya geçmeden önce dağıtım paketi kaynak dosyaları için paylaşılan klasör oluşturun.  

            - Belirtilen konumu başka bir yazılım dağıtım paketinin kaynağı olarak kullanamazsınız.  

            - Dağıtım paketini Configuration Manager oluşturulduktan sonra dağıtım paketi özelliklerinde paket kaynak konumunu değiştirebilirsiniz. Bunu yaparsanız, öncelikle özgün paket kaynağındaki içeriği yeni paket kaynak konumuna kopyalayın.  

            -  SMS sağlayıcısının bilgisayar hesabı ve yazılım güncelleştirmelerini indirmek için Sihirbazı çalıştıran kullanıcı, indirme konumuna **yazma** izinlerine sahip olmalıdır. İndirme konumuna erişimi kısıtlayın. Bu kısıtlama, saldırganların yazılım güncelleştirme kaynak dosyalarıyla izinsiz değiştirilme riskini azaltır.  

        -  **Gönderme önceliği**: Dağıtım paketi için gönderme önceliğini belirtin. Configuration Manager, paketi dağıtım noktalarına gönderdiğinde bu önceliği kullanır. Dağıtım paketleri öncelik sırasıyla gönderilir: yüksek, orta veya düşük. Benzer önceliklere sahip paketler oluşturulma sıralarına göre gönderilir. Biriktirme listesi yoksa, paket önceliğe bakılmaksızın hemen işlenir.  

        - **İkili değişiklik çoğaltmasını etkinleştir**: siteler arasındaki ağ trafiğini en aza indirmek için bu ayarı etkinleştirin. İkili farklar çoğaltması (BDR), paket içeriğinin tamamını güncelleştirmek yerine yalnızca pakette değiştirilen içeriği güncelleştirir. Daha fazla bilgi için bkz. [ikili farklar çoğaltması](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Dağıtım paketi yok**: sürüm 1806 ' den başlayarak, yazılım güncelleştirmelerini, içeriği önce indirip dağıtım noktalarına dağıtmadan cihazlara dağıtın. Son derece büyük güncelleştirme içeriğiyle ilgilenirken bu ayar faydalıdır. Ayrıca, istemcilerin Microsoft Update bulut hizmetinden içerik almasını istediğiniz zaman da kullanabilirsiniz. Bu senaryodaki istemciler, gerekli içeriğe zaten sahip olan eşlerden içerik de indirebilir. Configuration Manager istemcisi içerik indirmeyi yönetmeye devam eder, bu nedenle Configuration Manager eş önbellek özelliğini veya teslim Iyileştirme gibi diğer teknolojileri kullanabilir. Bu özellik, Windows ve Office güncelleştirmeleri de dahil olmak üzere Configuration Manager yazılım güncelleştirme yönetimi tarafından desteklenen tüm güncelleştirme türlerini destekler.<!--1357933-->  

10. **Dağıtım noktaları** sayfasında, yazılım güncelleştirme dosyalarını barındıracak dağıtım noktalarını veya dağıtım noktası gruplarını belirtin. Dağıtım noktaları hakkında daha fazla bilgi için bkz. [Dağıtım noktası yapılandırmaları](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!Note]  
    > Daha önce [3. Adım: yazılım güncelleştirme grubu Içeriğini indirme](#BKMK_3DownloadContent)seçeneğini gerçekleştirdiyseniz, sihirbaz **dağıtım paketini**, **dağıtım noktalarını**ve **Dil seçimi** sayfalarını göstermez. Sihirbazın [Özet](#bkmk_summary) sayfasına atlayın.  

11. **Yükleme konumu** sayfasında, yazılım güncelleştirme dosyalarının internetten mi yoksa yerel ağınızdan mı yükleneceğini belirtin. Aşağıdaki ayarları yapılandırın:  

    -   **Yazılım güncelleştirmelerini İnternet 'Ten indir**: yazılım güncelleştirmelerini İnternet 'teki belirli bir konumdan indirmek için bu ayarı seçin. Bu ayar, varsayılan olarak etkinleştirilmiştir.  

    -   **Yazılım güncelleştirmelerini yerel ağdaki bir konumdan indir**: Yazılım güncelleştirmelerini yerel bir dizinden veya paylaşılan ağ klasöründen indirmek için bu ayarı kullanın. Bu ayar, Sihirbazı çalıştıran bilgisayarın İnternet erişimi olmadığında yararlıdır. İnternet erişimi olan herhangi bir bilgisayar, yazılım güncelleştirmelerini indirebilir indirebilir. Ardından, bunları, Sihirbazı çalıştıran bilgisayardan erişilebilen yerel ağda bir yerde saklayın.  

12. **Dil seçimi** sayfasında, sitenin seçili yazılım güncelleştirmelerini indirdiği dilleri seçin. Site yalnızca seçili dillerde kullanılabiliyorsa bu güncelleştirmeleri indirir. Dile özgü olmayan yazılım güncelleştirmeleri her zaman indirilir. Varsayılan olarak, sihirbaz, yazılım güncelleştirme noktası özelliklerinde yapılandırdığınız dilleri seçer. Sonraki sayfaya geçmeden önce en az bir dil seçilmelidir. Yalnızca bir yazılım güncelleştirmesinin desteklemediği dilleri seçtiğinizde, güncelleştirme için indirme başarısız olur.  

    > [!Note]  
    > Daha önce [3. Adım: yazılım güncelleştirme grubu Içeriğini indirme](#BKMK_3DownloadContent)seçeneğini gerçekleştirdiyseniz, sihirbaz **dağıtım paketini**, **dağıtım noktalarını**ve **Dil seçimi** sayfalarını göstermez. Sihirbazın [Özet](#bkmk_summary) sayfasına atlayın.  

13. <a name="bkmk_summary"></a>**Özet** sayfasında, ayarları gözden geçirin. Ayarları bir Dağıtım şablonuna kaydetmek için **şablon olarak kaydet**' e tıklayın. Bir ad girin ve şablona dahil etmek istediğiniz ayarları seçin, sonra **Kaydet**' e tıklayın. Yapılandırılmış bir ayarı değiştirmek için, ilgili sihirbaz sayfasını tıklatın ve ayarı değiştirin.  

    -  Şablon adı alfasayısal ASCII karakterlerinin yanı sıra `\` (ters eğik çizgi) veya `'` (tek tırnak işareti) içerebilir.  

14. **İleri** 'ye tıklayarak yazılım güncelleştirmesini dağıtın.  

    Sihirbazı tamamladıktan sonra Configuration Manager, yazılım güncelleştirmelerini site sunucusundaki içerik kitaplığına indirir. Daha sonra içeriği yapılandırılan dağıtım noktalarına dağıtır ve yazılım güncelleştirme grubunu hedef koleksiyondaki istemcilere dağıtır. Dağıtım işlemi hakkında daha fazla bilgi için bkz. [Yazılım güncelleştirmesi dağıtım işlemi](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Sonraki adımlar
[Yazılım güncelleştirmelerini izleme](monitor-software-updates.md)
