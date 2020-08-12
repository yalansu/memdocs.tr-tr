---
title: Yazılım güncelleştirmelerini otomatik dağıtma
titleSuffix: Configuration Manager
description: Otomatik dağıtım kuralları (ADR) kullanarak yazılım güncelleştirmelerini otomatik olarak dağıtın.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 1a64d49edca146c70a56b07cb304d1744b86a1bf
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127755"
---
#  <a name="automatically-deploy-software-updates"></a>Yazılım güncelleştirmelerini otomatik dağıtma  

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Mevcut bir yazılım güncelleştirme grubuna yeni güncelleştirmeler eklemek yerine bir otomatik dağıtım kuralı (ADR) kullanın. Genellikle, ADRs 'yi kullanarak aylık yazılım güncelleştirmeleri ("Düzeltme Eki Salı" güncelleştirmeleri) ve Endpoint Protection tanım güncelleştirmelerini yönetme olarak da bilinir. Sizin için uygun olan dağıtım yönteminin belirlenmesi için yardıma ihtiyacınız varsa bkz. [yazılım güncelleştirmelerini dağıtma](deploy-software-updates.md).


##  <a name="create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a>Otomatik dağıtım kuralı (ADR) oluşturma  
ADR kullanarak yazılım güncelleştirmelerini otomatik olarak onaylayın ve dağıtın. Kural, kural her çalıştığında yeni bir yazılım güncelleştirme grubuna yazılım güncelleştirmeleri ekleyebilir veya mevcut bir gruba yazılım güncelleştirmeleri ekleyebilir. Bir kural çalıştırıldığında ve var olan bir gruba yazılım güncelleştirmeleri eklediğinde, kural gruptaki tüm güncelleştirmeleri kaldırır. Daha sonra, tanımladığınız kriterleri karşılayan güncelleştirmeleri gruba ekler. 

> [!WARNING]  
>  ADR 'yi ilk kez oluşturmadan önce, sitenin yazılım güncelleştirmeleri eşitlemesini tamamlamış olduğunu doğrulayın. Ingilizce olmayan bir dille Configuration Manager çalıştırdığınızda bu adım önemlidir. Yazılım güncelleştirme sınıflandırmaları, ilk eşitlemeden önce Ingilizce olarak görüntülenir ve ardından yazılım güncelleştirme eşitlemesi tamamlandıktan sonra yerelleştirilmiş dillerde görüntülenir. Yazılım güncelleştirmelerini eşitlemeden önce oluşturduğunuz kurallar eşitleme sonrasında doğru çalışmayabilir çünkü metin dizesi eşleşmeyebilir.  


### <a name="process-to-create-an-adr"></a><a name="bkmk_adr-process"></a>ADR oluşturma işlemi  

1.  Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **yazılım güncelleştirmeleri**' ni genişletin ve **Otomatik dağıtım kuralları** düğümünü seçin.  

2.  Şeritte **Otomatik dağıtım kuralı oluştur**' a tıklayın.  

3.  Otomatik dağıtım kuralı oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdaki ayarları yapılandırın:  

    -   **Ad:** ADR’nin adını belirtin. Ad benzersiz olmalıdır, kuralın amacını açıklamaya yardımcı olur ve Configuration Manager sitesinde başkalarından ayırt edilebilir.  

    -   **Açıklama:** ADR için bir açıklama belirtin. Açıklama, Dağıtım kuralına ve kuralın diğerlerinden ayırt edilmesine yardımcı olan diğer ilgili bilgilere genel bir bakış sağlamalıdır. Açıklama alanı isteğe bağlıdır, 256 karakter limiti vardır ve varsayılan olarak boş değere sahiptir.  

    -   **Şablon**: daha önce kaydedilen ADR yapılandırmalarının uygulanıp uygulanmayacağını belirtmek için bir dağıtım şablonu seçin. Ek ADRs oluştururken kullanabileceğiniz birden çok ortak güncelleştirme dağıtım özelliği içeren bir dağıtım şablonu yapılandırın. Bu şablonlar, benzer dağıtımlar arasında tutarlılık sağlamaya yönelik zaman kazandırır ve yardım sağlar. Aşağıdaki yerleşik yazılım güncelleştirme dağıtım şablonlarından birini seçin:  

         - **Patch Tuesday** şablonu, yazılım güncelleştirmelerini aylık bir döngüde dağıtırken kullanacağınız genel ayarları sağlar.  

         - **Office 365 Istemci güncelleştirmeleri** şablonu, Microsoft 365 Apps istemcilerine yönelik güncelleştirmeleri dağıtırken kullanılacak genel ayarları sağlar.
             > [!Note]
             > 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. ADRs 'niz "title" özelliğini kullanıyorsa, 9 Haziran 2020 ' den itibaren düzenlemeniz gerekir. `Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)`yeni başlığa bir örnektir. Başlık değişikliği için ADRs 'nizi değiştirme hakkında daha fazla bilgi için bkz. [Microsoft 365 uygulamaları için kanalları güncelleştirme](manage-office-365-proplus-updates.md#bkmk_channel). Ad değişikliği hakkında daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](https://docs.microsoft.com/deployoffice/name-change).

         - **SCEP ve Windows Defender virüsten koruma güncelleştirmeleri** şablonu, Endpoint Protection tanım güncelleştirmelerini dağıtırken kullanılacak genel ayarları sağlar.  

    -   **Koleksiyon**: Dağıtım için kullanılacak hedef koleksiyonu belirtir. Koleksiyon üyeleri, dağıtımda tanımlanan yazılım güncelleştirmelerini alır.  

    -   Yazılım güncelleştirmelerini yeni veya mevcut bir yazılım güncelleştirme grubuna eklemek arasında seçim yapın. Çoğu durumda, ADR çalıştırıldığında yeni bir yazılım güncelleştirme grubu oluşturmayı seçin. Kural daha agresif bir zamanlamaya göre çalışıyorsa, var olan bir grubu kullanmayı tercih edebilirsiniz. Örneğin, kuralı tanım güncelleştirmeleri için günlük olarak çalıştırırsanız, yazılım güncelleştirmelerini mevcut bir yazılım güncelleştirme grubuna ekleyebilirsiniz.  

    -   **Bu kural çalıştırıldıktan sonra dağıtımı etkinleştir**: ADR çalıştırıldıktan sonra yazılım güncelleştirme dağıtımının etkinleştirilip etkinleştirilmeyeceğini belirtin. Bu ayar için aşağıdaki seçenekleri göz önünde bulundurun:  

        -   Dağıtımı etkinleştirdiğinizde, kuralın tanımlı ölçütlerine uyan güncelleştirmeler bir yazılım güncelleştirme grubuna eklenir. Yazılım güncelleştirme içeriği gerektiğinde indirilir. İçerik belirtilen dağıtım noktalarına kopyalanır ve güncelleştirmeler hedef koleksiyondaki istemcilere dağıtılır.  

        -   Dağıtımı etkinleştirmezseniz, kuralın tanımlı ölçütlerine uyan güncelleştirmeler bir yazılım güncelleştirme grubuna eklenir. Yazılım güncelleştirme dağıtım içeriği, gerektiğinde indirilir ve belirtilen dağıtım noktalarına dağıtılır. Site, güncelleştirmelerin istemcilere dağıtılmasını engellemek için yazılım güncelleştirme grubunda devre dışı bir dağıtım oluşturur. Bu seçenek, güncelleştirmeleri dağıtmaya hazırlanma, ölçütleri karşılayan güncelleştirmelerin yeterli olduğunu doğrulama ve sonra dağıtımı etkinleştirme için zaman sağlar.  

4.  **Dağıtım ayarları** sayfasında, aşağıdaki ayarları yapılandırın:  

    -   **Gerekli dağıtımlarda istemcileri uyandırmak IÇIN lan 'Da uyandırma 'Yı kullan**: son tarihte LAN'da Uyandırma etkinleştirilip etkinleştirilmeyeceğini belirtir. LAN'da Uyandırma dağıtımda bir veya daha fazla yazılım güncelleştirmesi gerektiren bilgisayarlara Uyandırma paketleri gönderir. Site, yüklemenin başlatılması için, yükleme son tarihinde uyku modunda olan tüm bilgisayarları uyandırır. Dağıtımda yazılım güncelleştirmesi gerektirmeyen uyku modundaki istemciler başlatılmaz. Varsayılan olarak bu ayar etkin değildir. Bu seçeneği kullanmadan önce LAN'da Uyandırma için bilgisayarları ve ağları yapılandırın. Daha fazla bilgi için bkz. [nasıl yapılandırılır LAN'da Uyandırma](../../core/clients/deploy/configure-wake-on-lan.md).  

    -   **Ayrıntı düzeyi**: istemciler tarafından raporlanan güncelleştirme zorlama durumu iletileri için ayrıntı düzeyini belirtin.  

        > [!IMPORTANT]  
        >  Tanım güncelleştirmelerini dağıtırken, istemcinin yalnızca bir tanım güncelleştirmesi başarısız olduğunda bir durum iletisi rapor vermesi için ayrıntı düzeyini **yalnızca hata** olarak ayarlayın. Aksi halde, istemci, site sunucusu performansını etkileyebilecek çok sayıda durum iletisi bildirir.  
        
        > [!NOTE]  
        > **Hata yalnızca** ayrıntı düzeyi, bekleyen yeniden başlatmaları izlemek için gereken zorlama durum iletilerini göndermez.

    -   **Lisans koşulları ayarı**: Yazılım güncelleştirmelerinin otomatik olarak ilgili lisans koşullarıyla dağıtılıp dağıtılmayacağını belirtin. Bazı yazılım güncelleştirmeleri lisans koşulları içerir. Yazılım güncelleştirmelerini otomatik olarak dağıttığınızda, lisans koşulları görüntülenmez ve lisans koşullarını kabul etme seçeneği yoktur. İlişkili bir lisans teriminden bağımsız olarak tüm yazılım güncelleştirmelerini otomatik olarak dağıtmayı veya yalnızca ilişkili lisans koşullarına sahip olmayan güncelleştirmeleri dağıtmayı seçin.  

         - Yazılım güncelleştirmesi lisans koşullarını gözden geçirmek için, yazılım **kitaplığı** çalışma alanının **tüm yazılım güncelleştirmeleri** düğümünde yazılım güncelleştirmesini seçin. Şeritte **lisansı gözden geçir**' e tıklayın.    

         - İlişkili lisans koşullarına sahip yazılım güncelleştirmelerini bulmak için, **Lisans koşulları** sütununu **tüm yazılım güncelleştirmeleri** düğümündeki sonuçlar bölmesine ekleyin. Lisans koşullarına sahip yazılım güncelleştirmelerine göre sıralanacak sütunun başlığına tıklayın.  

5.  **Yazılım güncelleştirmeleri** SAYFASıNDA, ADR 'nin aldığı ve yazılım güncelleştirme grubuna eklediği yazılım güncelleştirmeleri için kriterleri yapılandırın.  

     - ADR’deki yazılım güncelleştirme limiti 1000 yazılım güncelleştirmesidir.  

     - Gerekirse, otomatik dağıtım kurallarında yazılım güncelleştirmeleri için içerik boyutunu filtreleyin. Daha fazla bilgi için, bkz. [Configuration Manager ve Basitleştirilmiş Windows Bakımı alt düzey işletim sistemleri](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056).  

     - Sürüm 1910 ' den başlayarak, otomatik dağıtım kurallarınız için bir güncelleştirme filtresi olarak **dağıtılan** ' ı kullanabilirsiniz. Bu filtre, pilot veya test koleksiyonlarınız için dağıtılması gerekebilecek yeni güncelleştirmeleri tanımlamanızı sağlar. Yazılım güncelleştirme filtresi, eski güncelleştirmelerin yeniden dağıtılmasını önlemeye de yardımcı olabilir. 
         - Bir filtre olarak **dağıtılan** kullanırken, güncelleştirmeyi bir pilot veya test koleksiyonu gibi başka bir koleksiyona zaten dağıtmış olabilirsiniz. <!--4852033-->
     - Sürüm 1806 ' den başlayarak, **mimari** için bir özellik filtresi artık kullanılabilir. Daha az ortak olan Itanium ve ARM64 gibi mimarileri hariç tutmak için bu filtreyi kullanın. 64 bit (x64) sistemlerde çalışan 32-bit (x86) uygulamaları ve bileşenleri olduğunu unutmayın. X86 gerekmediği sürece, x64 ' u seçtiğinizde de etkinleştirin.<!--1322266-->  

    > [!NOTE]  
    > **Windows 10, sürüm 1903 ve üzeri,** **Windows 10** ürününün önceki sürümleri gibi bir parçası olmak yerine kendi ürünü olarak Microsoft Update eklenmiştir. Bu değişiklik, istemcilerinizin bu güncelleştirmeleri görmesini sağlamak için birkaç el ile adım uygulamanızı sağlar. Configuration Manager sürüm 1906 ' de yeni ürün için gerçekleştirmeniz gereken el ile adım sayısını azaltmaya yardımcı oluyoruz. Daha fazla bilgi için bkz. [Windows 10 sürümleri için ürünleri yapılandırma](../get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later) <!--4682946-->


6. **Değerlendirme zamanlaması** SAYFASıNDA, ADR 'nin bir zamanlamaya göre çalışmasına etkinleştirilip etkinleştirilmeyeceğini belirtin. Etkinleştirildiğinde, **Özelleştir** 'i tıklatarak tekrarlama zamanlamasını ayarlayın.  

    - Zamanlamanın başlangıç zamanı yapılandırması, Configuration Manager konsolunu çalıştıran bilgisayarın yerel zamanına bağlıdır.  

    - ADR değerlendirmesi günde üç kez kadar sık yapılabilir.  

    - Değerlendirme zamanlamasını, yazılım güncelleştirmeleri eşitleme zamanlamasını aşan bir sıklık ile hiçbir zaman ayarlama. Bu sayfada değerlendirme zamanlaması sıklığını belirlemenize yardımcı olması için yazılım güncelleştirme noktası eşitleme zamanlaması görüntülenir.  

    - ADR 'yi el ile çalıştırmak için, konsolunun **Otomatik dağıtım kuralı** düğümünde kuralı seçin ve ardından şeritte **Şimdi Çalıştır** ' a tıklayın.  

    - Sürüm 1802 ' den başlayarak, ADRs, bir temel gündeki sapmayı değerlendirmek için zamanlanabilir. Örneğin, Salı düzeltme eki, sizin için Çarşamba günü geliyorsa, ayın ikinci Salı günü için değerlendirme zamanlamasını bir güne ayarlayın.<!--1357133-->  
        - Bir sonraki aya devam eden bir uzaklığa sahip bir sapmayı bir uzaklığa göre hesaplamayı zamanlıyorsanız, site ayın son günü için değerlendirmeyi zamanlar.<!--506731-->  
        ![ADR özel değerlendirme zamanlaması taban günden uzaklığa göre](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  **Dağıtım zamanlaması** sayfasında, aşağıdaki ayarları yapılandırın:  

    -   **Değerlendirmeyi zamanla**: Configuration Manager, kullanılabilir saat ve yükleme son tarih zamanlarını değerlendiren süreyi belirtin. Eşgüdümlü Evrensel Saat (UTC) veya Configuration Manager konsolunu çalıştıran bilgisayarın yerel saatini kullanmayı seçin.  

          - Burada **istemci yerel saati** ' ni seçip **Yazılım kullanılabilir saati**için **mümkün olan en kısa sürede** ' yi seçtiğinizde, güncelleştirmelerin ne zaman kullanılabilir olduğunu değerlendirmek için Configuration Manager konsolunu çalıştıran bilgisayardaki geçerli saat kullanılır. Bu davranış, **yükleme son tarihi** ve güncelleştirmelerin bir istemciye yüklendiği zaman ile aynıdır. İstemci farklı bir saat dilimindeyse bu eylemler, istemcinin saati değerlendirme saatine ulaştığında gerçekleşir.  

    -   **Yazılım uygunluk saati**: Yazılım güncelleştirmelerinin istemciler için ne zaman kullanılabilir olduğunu belirtmek için aşağıdaki ayarlardan birini seçin:  

        -   **Mümkün olan en kısa sürede**: Dağıtımdaki yazılım güncelleştirmelerinin istemciler için mümkün olan en kısa sürede kullanılabilmesini sağlar. Dağıtımı bu ayar seçili olarak oluşturduğunuzda, Configuration Manager istemci ilkesini güncelleştirir. Bir sonraki istemci ilkesi yoklama döngüsünün, istemcileri dağıtımdan haberdar edilir ve yazılım güncelleştirmeleri yükleme için kullanılabilir hale gelir.  

        -   **Belirli bir süre**: dağıtıma dahil edilen yazılım güncelleştirmelerini belirli bir tarih ve saatte istemciler için kullanılabilir hale getirir. Bu ayar etkinken dağıtımı oluşturduğunuzda Configuration Manager istemci ilkesini güncelleştirir. Bir sonraki istemci ilkesi yoklama döngüsünden istemciler, dağıtımın farkında olur. Ancak, Dağıtımdaki yazılım güncelleştirmeleri, yapılandırılan tarih ve saate kadar, yükleme için kullanılamaz.  

    -   **Yükleme son tarihi**: Dağıtımdaki yazılım güncelleştirmeleri için yükleme son tarihini belirtmek üzere aşağıdaki ayarlardan birini seçin:  

        -   **Mümkün olan en kısa sürede**: Dağıtımdaki yazılım güncelleştirmelerinin mümkün olan en kısa sürede otomatik olarak yüklenmesi için bu ayarı seçin.  

        -   **Belirli bir zamanda**: Dağıtımdaki yazılım güncelleştirmelerini belirli bir tarih ve saatte otomatik olarak yüklemek için bu ayarı seçin. Configuration Manager, yapılandırılmış **belirli zaman** aralığını **Yazılım kullanılabilir zamanına**ekleyerek yazılım güncelleştirmelerinin yükleneceği son tarihi belirler.  

             - Gerçek yükleme son tarih saati, en fazla iki saate kadar rastgele bir süre ile görüntülenir. Rasgeleleştirme, koleksiyondaki istemcilerin aynı anda dağıtımdaki güncelleştirmeleri yükleyen potansiyel etkisini azaltır.  

             - Gerekli yazılım güncelleştirmeleri için yükleme rastgele gecikmesini devre dışı bırakmak için, istemci ayarını **Bilgisayar Aracısı** grubundaki **rastgele son tarih seçimini devre dışı bırakacak** şekilde yapılandırın. Daha fazla bilgi için bkz. [Bilgisayar Aracısı istemci ayarları](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    -  **İstemci ayarlarında tanımlanan yetkisiz kullanım süresine kadar bu dağıtımın uygulanmasını kullanıcı tercihlerine göre geciktir**: kullanıcıların gerekli yazılım güncelleştirmelerini son tarihten sonra yüklemesi daha fazla zaman vermesi için bu ayarı etkinleştirin.  

        - Bu davranış, genellikle bir bilgisayar uzun süredir kapalıyken gereklidir ve birçok yazılım güncelleştirmesi ya da uygulama yüklemesi gerekir. Örneğin, bir Kullanıcı tatilden döndüğünde, istemci vadesi geçmiş dağıtımları yüklerken uzun süre beklemelidir.  

        - Bu yetkisiz kullanım süresini, istemci ayarlarındaki **dağıtım son tarihi (saat) sonra zorlama için özellik yetkisiz kullanım** süresiyle yapılandırın. Daha fazla bilgi için [Bilgisayar Aracısı](../../core/clients/deploy/about-client-settings.md#computer-agent) bölümüne bakın. Zorlama yetkisiz kullanım süresi, bu seçenek etkinleştirilmiş ve istemci ayarını dağıttığınız cihazlara hedeflenmiş tüm dağıtımlar için geçerlidir.  

        - Son tarihten sonra istemci, yazılım güncelleştirmelerini kullanıcı tarafından yapılandırılan ve bu yetkisiz kullanım süresine kadar olan ilk iş dışı pencereye yüklenir. Ancak, Kullanıcı hala yazılım merkezini açabilir ve yazılım güncelleştirmelerini dilediğiniz zaman yükleyebilir. Yetkisiz kullanım süresi dolduktan sonra, zorlama süresi dolan dağıtımlar için normal davranışa geri döner.  

8. **Kullanıcı deneyimi** sayfasında, aşağıdaki ayarları yapılandırın:  

    -   **Kullanıcı bildirimleri**: Yazılım Merkezi 'Nde yapılandırılan **yazılım kullanım zamanında**bildirimin görüntülenip görüntülenmeyeceğini belirtin. Bu ayar ayrıca kullanıcılara istemcilerde bildirim yapılıp yapılmayacağını da denetler.  

    -   **Son tarih davranışı**: yazılım güncelleştirme dağıtımı, tüm tanımlı bakım pencerelerinin dışında son tarihe ulaştığında davranışları belirtin. Seçenekler, yazılım güncelleştirmelerinin yüklenip yüklenmeyeceğini ve yükleme sonrasında sistemin yeniden başlatılması yapılıp yapılmayacağını içerir. Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  
        
        > [!Note]
        > Bu, yalnızca bakım penceresi istemci cihaz için yapılandırıldığında geçerlidir. Cihazda herhangi bir bakım penceresi tanımlanmazsa, yükleme ve yeniden başlatma güncelleştirmesi her zaman son tarihten sonra gerçekleşecektir.

    -   **Cihaz yeniden başlatma davranışı**: güncelleştirme yüklemesini tamamlaması için yeniden başlatma gerekiyorsa, sunucularda ve iş istasyonlarında sistemin yeniden başlatılmasının engellenip engellenmeyeceğini belirtin.  

        > [!WARNING]  
        >  Sistem yeniden başlatmaları gizleme sunucu ortamlarında veya hedef bilgisayarların varsayılan olarak yeniden başlatılmasını istemediğiniz durumlarda yararlı olabilir. Ancak bunu yapmak bilgisayarları güvenli olmayan bir durumda bırakabilir. Zorla yeniden başlatmaya izin verilmesi, yazılım güncelleştirme yüklemesinin anında tamamlanmasını sağlamaya yardımcı olur.  

    -   **Windows Embedded cihazlar için filtre Işleme yaz**: Bu ayar, yazma filtresiyle etkinleştirilen Windows Embedded cihazlarındaki yükleme davranışını denetler. Yükleme son tarihinde veya bakım penceresi sırasında değişiklikleri Yürüt seçeneğini belirleyin. Bu seçeneği belirlediğinizde, yeniden başlatma gerekir ve değişiklikler cihazda kalır. Aksi takdirde, güncelleştirme yüklenir, geçici katmana uygulanır ve daha sonra kaydedilir.  

           -  Windows Embedded cihazına bir yazılım güncelleştirmesi dağıttığınızda, cihazın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun.  

    - **Yazılım güncelleştirmeleri dağıtımı yeniden başlatma sırasında yeniden değerlendirme davranışı**: yazılım güncelleştirmeleri dağıtımlarını, bir istemci yazılım güncelleştirmelerini yükledikten ve yeniden başlatıldıktan hemen sonra bir yazılım güncelleştirmeleri uyumluluk taraması çalıştıracak şekilde yapılandırmak için bu ayarı seçin. Bu ayar, istemcinin, istemci yeniden başlatıldıktan sonra geçerli hale gelen ek güncelleştirmeleri denetlemesini sağlar ve aynı bakım penceresi sırasında bunları yüklenir.  

9. **Uyarılar** sayfasında, bu dağıtım için Configuration Manager uyarıları nasıl üretir yapılandırın. **Yazılım kitaplığı** çalışma alanının **yazılım güncelleştirmeleri** düğümündeki Configuration Manager 'deki son yazılım güncelleştirme uyarılarını gözden geçirin. System Center Operations Manager kullanıyorsanız, uyarılarını da yapılandırın.  

10. **Yükleme ayarları** sayfasında, aşağıdaki ayarları yapılandırın:  

    - İstemcilerin bir komşudan veya varsayılan site sınır gruplarından bir dağıtım noktası kullandıklarında güncelleştirmeleri indirip yüklemesi gerekip gerekmediğini belirtin.  

    - İstemcilerin, yazılım güncelleştirmeleri için içerik geçerli veya komşu sınır gruplarındaki bir dağıtım noktasından kullanılamadığında, güncelleştirmeleri site varsayılan sınır grubundaki bir dağıtım noktasından indirmesi ve yüklemesi gerekip gerekmediğini belirtin.  

    - **İstemcilerin aynı alt ağdaki diğer istemcilerle içerik paylaşmasına izin ver**: İçerik yüklemeleri için BranchCache kullanımının etkinleştirilip etkinleştirilmeyeceğini belirtin. Daha fazla bilgi için bkz. [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Sürüm 1802 ' den başlayarak, BranchCache her zaman istemcilerde etkindir. İstemciler, dağıtım noktası destekliyorsa BranchCache kullandığından, bu ayar kaldırılır.  

    - **Yazılım güncelleştirmeleri geçerli, komşu veya site sınır gruplarındaki dağıtım noktasında yoksa, Microsoft Updates 'ten içerik indirin**: dağıtım noktalarında güncelleştirmeler yoksa, intranet bağlantılı istemcilerin Microsoft Update yazılım güncelleştirmelerini indirmesini sağlamak için bu ayarı seçin. Internet tabanlı istemciler, her zaman yazılım güncelleştirme içerikleri için Microsoft Update 'ye gider.  

    - Tarifeli İnternet bağlantıları kullandıklarında, yükleme son tarihinden sonra istemcilerin indirmelerine izin verilip verilmeyeceğini belirtin. Tarifeli bir bağlantıda olduğunuzda, Internet sağlayıcıları bazen gönderme ve alma yaptığınız veri miktarına göre ücretlendirilir.  

    > [!NOTE]  
    >  İstemciler, dağıtımdaki yazılım güncelleştirmeleri için bir yönetim noktasından içerik konumunu ister. Yükleme davranışı, dağıtım noktasını, dağıtım paketini ve bu sayfadaki ayarları nasıl yapılandırdığınıza bağlıdır.   

11. **Dağıtım paketi** sayfasında, aşağıdaki seçeneklerden birini seçin:  

    - **Bir dağıtım paketi seçin**: Bu güncelleştirmeleri mevcut bir dağıtım paketine ekleyin.  

    - **Yeni dağıtım paketi oluştur**: Bu güncelleştirmeleri yeni bir dağıtım paketine ekleyin. Aşağıdaki ek ayarları yapılandırın:  

        -  **Ad**: Dağıtım paketinin adını belirtin. Paket içeriğini açıklayan benzersiz bir ad kullanın. 50 karakterle sınırlıdır.  

        -  **Açıklama**: Dağıtım paketiyle ilgili bilgi sağlayan bir açıklama belirtin. İsteğe bağlı Açıklama 127 karakterle sınırlıdır.  

        -  **Paket kaynağı**: Yazılım güncelleştirmesi kaynak dosyalarının konumunu belirtir. Kaynak konumu için bir ağ yolu yazın (örneğin,) `\\server\sharename\path` veya ağ konumunu bulmak Için **Araştır** ' a tıklayın. Sonraki sayfaya geçmeden önce dağıtım paketi kaynak dosyaları için paylaşılan klasör oluşturun.  

            - Belirtilen konumu başka bir yazılım dağıtım paketinin kaynağı olarak kullanamazsınız.  

            - Dağıtım paketini Configuration Manager oluşturulduktan sonra dağıtım paketi özelliklerinde paket kaynak konumunu değiştirebilirsiniz. Bunu yaparsanız, öncelikle özgün paket kaynağındaki içeriği yeni paket kaynak konumuna kopyalayın.  

            -  SMS sağlayıcısının bilgisayar hesabı ve yazılım güncelleştirmelerini indirmek için Sihirbazı çalıştıran kullanıcı, indirme konumuna **yazma** izinlerine sahip olmalıdır. İndirme konumuna erişimi kısıtlayın. Bu kısıtlama, saldırganların yazılım güncelleştirme kaynak dosyalarıyla izinsiz değiştirilme riskini azaltır.  

        -  **Gönderme önceliği**: Dağıtım paketi için gönderme önceliğini belirtin. Configuration Manager, paketi dağıtım noktalarına gönderdiğinde bu önceliği kullanır. Dağıtım paketleri öncelik sırasıyla gönderilir: yüksek, orta veya düşük. Benzer önceliklere sahip paketler oluşturulma sıralarına göre gönderilir. Biriktirme listesi yoksa, paket önceliğe bakılmaksızın hemen işlenir.  

        - **İkili değişiklik çoğaltmasını etkinleştir**: dağıtım paketi için ikili değişiklik çoğaltmasını kullanmak için bu ayarı etkinleştirin. Daha fazla bilgi için bkz. [ikili farklar çoğaltması](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Dağıtım paketi yok**: sürüm 1806 ' den başlayarak, yazılım güncelleştirmelerini, içeriği önce indirip dağıtım noktalarına dağıtmadan cihazlara dağıtın. Son derece büyük güncelleştirme içeriğiyle ilgilenirken bu ayar faydalıdır. Ayrıca, istemcilerin Microsoft Update bulut hizmetinden içerik almasını istediğiniz zaman da kullanabilirsiniz. Bu senaryodaki istemciler, gerekli içeriğe zaten sahip olan eşlerden içerik de indirebilir. Configuration Manager istemcisi içerik indirmeyi yönetmeye devam eder, bu nedenle Configuration Manager eş önbellek özelliğini veya teslim Iyileştirme gibi diğer teknolojileri kullanabilir. Bu özellik, Windows ve Microsoft 365 Apps güncelleştirmeleri dahil Configuration Manager yazılım güncelleştirme yönetimi tarafından desteklenen tüm güncelleştirme türlerini destekler.<!--1357933-->  

        > [!Note]  
        > Bu seçeneği belirleyip ayarları uyguladığınızda, artık değiştirilemez. Diğer seçenekler gri renkte.<!--SCCMDocs-pr issue 3003-->  

12. **Dağıtım noktaları** sayfasında, yazılım güncelleştirme dosyalarını barındıracak dağıtım noktalarını veya dağıtım noktası gruplarını belirtin. Dağıtım noktaları hakkında daha fazla bilgi için bkz. [Dağıtım noktası yapılandırmaları](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Bu sayfa sadece yeni yazılım güncelleştirme dağıtım paketi oluşturduğunuzda kullanılabilir.  
  

13. **Yükleme konumu** sayfasında, yazılım güncelleştirme dosyalarının internetten mi yoksa yerel ağınızdan mı yükleneceğini belirtin. Aşağıdaki ayarları yapılandırın:  

    -   **Yazılım güncelleştirmelerini İnternet 'Ten indir**: yazılım güncelleştirmelerini İnternet 'teki belirli bir konumdan indirmek için bu ayarı seçin. Bu ayar varsayılan olarak etkindir.  

    -   **Yazılım güncelleştirmelerini yerel ağdaki bir konumdan indir**: Yazılım güncelleştirmelerini yerel bir dizinden veya paylaşılan ağ klasöründen indirmek için bu ayarı kullanın. Bu ayar, Sihirbazı çalıştıran bilgisayarın İnternet erişimi olmadığında yararlıdır. İnternet erişimi olan herhangi bir bilgisayar, yazılım güncelleştirmelerini indirebilir indirebilir. Ardından, bunları, Sihirbazı çalıştıran bilgisayardan erişilebilen yerel ağda bir yerde saklayın. System Center Updates Publisher veya üçüncü taraf düzeltme eki uygulama çözümü aracılığıyla yayınlanan içeriği indirirken başka bir senaryo olabilir. Üst düzey yazılım güncelleştirme noktasındaki WSUS içerik paylaşma, ' den indirilecek ağ konumu olarak girilebilir `\\server\WsusContent` . <!--memdocs-issue-211-->

14. **Dil seçimi** sayfasında, sitenin seçili yazılım güncelleştirmelerini indirdiği dilleri seçin. Site yalnızca seçili dillerde kullanılabiliyorsa bu güncelleştirmeleri indirir. Dile özgü olmayan yazılım güncelleştirmeleri her zaman indirilir. Varsayılan olarak, sihirbaz, yazılım güncelleştirme noktası özelliklerinde yapılandırdığınız dilleri seçer. Sonraki sayfaya geçmeden önce en az bir dil seçilmelidir. Yalnızca bir yazılım güncelleştirmesinin desteklemediği dilleri seçtiğinizde, güncelleştirme için indirme başarısız olur.  

15. **Özet** sayfasında, ayarları inceleyin. Ayarları bir Dağıtım şablonuna kaydetmek için **şablon olarak kaydet**' e tıklayın. Bir ad girin ve şablona dahil etmek istediğiniz ayarları seçin, sonra **Kaydet**' e tıklayın. Yapılandırılmış bir ayarı değiştirmek için, ilgili sihirbaz sayfasını tıklatın ve ayarı değiştirin.  

    -  Şablon adı alfasayısal ASCII karakterlerinin yanı sıra `\` (ters eğik çizgi) veya `'` (tek tırnak işareti) içerebilir.  

16. **İleri** 'ye tıklayarak ADR’yi oluşturun.  

Sihirbazı tamamladıktan sonra ADR çalışır. Belirtilen ölçütlere uyan yazılım güncelleştirmelerini bir yazılım güncelleştirme grubuna ekler. Ardından ADR, güncelleştirmeleri site sunucusundaki içerik kitaplığına indirir ve bunları yapılandırılmış dağıtım noktalarına dağıtır. ADR daha sonra yazılım güncelleştirme grubunu hedef koleksiyondaki istemcilere dağıtır.  



##  <a name="add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a>Var olan bir ADR 'ye yeni bir dağıtım ekleme  

ADR oluşturduktan sonra kurala başka dağıtımlar ekleyin. Bu eylem farklı koleksiyonlara farklı güncelleştirmeler dağıtma karmaşıklığını yönetmenize yardımcı olur. Her yeni dağıtım, tüm işlevlere ve dağıtım izleme deneyimine sahiptir.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Var olan bir ADR 'ye yeni bir dağıtım ekleme işlemi  

1.  Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **yazılım güncelleştirmeleri**' ni genişletin, **Otomatik dağıtım kuralları** düğümünü seçin ve ardından istediğiniz kuralı seçin.  

2.  Şeritte **dağıtım Ekle**' ye tıklayın.   

3.  Dağıtım Ekle sihirbazının **koleksiyon** sayfasında, kullanılabilir ayarları, otomatik dağıtım kuralı oluşturma Sihirbazı ' nın **genel** sayfasında benzer şekilde yapılandırın. Daha fazla bilgi için, [BIR ADR oluşturma işleminin](#bkmk_adr-process)önceki bölümüne bakın. Dağıtım Ekleme Sihirbazı 'nın geri kalanı, yukarıdaki ayrıntılı açıklamalarla de eşleşen aşağıdaki sayfaları içerir:  

     - Dağıtım ayarları
     - Dağıtım zamanlaması
     - Kullanıcı Deneyimi
     - Uyarılar
     - İndirme Ayarları  

Dağıtımlar ayrıca Windows PowerShell cmdlet 'leri kullanılarak programlı bir şekilde eklenebilir. Bu yöntemin kullanımıyla ilgili tam bir açıklama için, bkz. [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment) .

Dağıtım işlemi hakkında daha fazla bilgi için bkz. [Yazılım güncelleştirmesi dağıtım işlemi](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Sonraki adımlar
[Yazılım güncelleştirmelerini izleme](monitor-software-updates.md)
