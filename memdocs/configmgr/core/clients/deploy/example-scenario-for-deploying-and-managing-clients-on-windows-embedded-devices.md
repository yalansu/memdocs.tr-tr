---
title: Örnek senaryo-Windows Embedded istemcileri dağıtma
titleSuffix: Configuration Manager
description: Windows Embedded cihazlarında Configuration Manager istemcilerini dağıtmak ve yönetmek için örnek bir senaryoya bakın.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713334"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>Windows Embedded cihazlarında Configuration Manager istemcilerini dağıtmaya ve yönetmeye yönelik örnek senaryo

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu senaryo, yazma Filtresi özellikli Windows Embedded cihazlarını Configuration Manager ile nasıl yönetebileceğinizi gösterir. katıştırılmış cihazlarınız yazma filtrelerini desteklemiyorsa, standart Configuration Manager istemcileri gibi davranır ve bu yordamlar uygulanmaz.  

Coho Vineyard &, bir ziyaretçi merkezi açıyor ve etkileşimli sunular çalıştırmak için Windows Embedded çalıştıran bilgi noktaları 'leri istiyor. Yeni ziyaretçi merkezinin binası BT departmanına yakın olmadığından, bilgi noktaları 'in uzaktan yönetilmesi gerekir. Sunuları çalıştıran yazılıma ek olarak, bu cihazların şirket güvenlik ilkelerine uyum sağlamak için güncel kötü amaçlı yazılımdan koruma yazılımı çalıştırması gerekir. Bilgi noktaları, ziyaretçi merkezi açıkken kapalı kalma süresi olmadan haftada 7 gün önce çalışmalıdır.  

 Coho, ağdaki cihazları yönetmek için Configuration Manager zaten çalışıyor. Configuration Manager, Endpoint Protection çalıştıracak ve yazılım güncelleştirmelerini ve uygulamaları yükleyecek şekilde yapılandırılmıştır. Ancak, BT ekibi daha önce Windows Embedded cihazları yönetmediği için Configuration Manager yöneticisi, Alım lobisindeki iki bilgi noktasını yönetmek üzere bir pilot çalıştırmıştır.   

 Yazma filtresi etkin olan bu Windows Embedded cihazlarını yönetmek için Configuration Manager yöneticisi, Configuration Manager istemcisini yüklemek, Endpoint Protection kullanarak istemciyi korumak ve etkileşimli sunu yazılımını yüklemek için aşağıdaki adımları gerçekleştirir.  

1. Configuration Manager Yöneticisi (yönetici), Windows Embedded cihazlarının yazma filtrelerini nasıl kullandığını ve Configuration Manager otomatik olarak devre dışı bırakıp daha sonra yeniden etkinleştirerek bir yazılım yüklemesini kalıcı hale getirerek bu şekilde nasıl daha kolay hale getirebileceği okur.  

    Daha fazla bilgi için bkz. [Windows Embedded cihazlarına istemci dağıtımını planlama](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2. Yönetici Configuration Manager istemcisini yüklemeden önce, yönetici Windows Embedded cihazlar için yeni bir sorgu tabanlı cihaz koleksiyonu oluşturur. Şirket bilgisayarlarını tanımlamak için standart adlandırma biçimlerini kullandığından, yönetici Windows Embedded cihazlarını bilgisayar adının ilk altı harfiyle benzersiz şekilde tanımlayabilir: **WEMDVC**. Yönetici bu koleksiyonu oluşturmak için şu WQL sorgusunu kullanır: **SMS_R_System SMS_R_System. NetbiosName ' in "WEMDVC%" gibi SMS_R_System. NetbiosName öğesini seçin**  

    Bu koleksiyon, yöneticinin Windows Embedded cihazlarını diğer cihazlardan farklı yapılandırma seçenekleriyle yönetmesine olanak tanır. Yönetici, yeniden başlatmaları denetlemek, istemci ayarlarıyla Endpoint Protection dağıtmak ve etkileşimli sunu uygulamasını dağıtmak için bu koleksiyonu kullanacaktır.  

    Bkz. [koleksiyonları oluşturma](../../../core/clients/manage/collections/create-collections.md).  

3. Yönetici, sunu uygulamasını yüklemek için gerekebilecek yeniden başlatmalarının ve ziyaretçi merkezi için açma saatlerinde hiçbir yükseltme gerçekleşmediğinden emin olmak üzere bir bakım penceresi için koleksiyonu yapılandırır. Açık saatler pazartesiden cumaya 09:00 ile 18:00 arası olacaktır. Yönetici, bakım penceresini her gün için yapılandırır, 18:30 ile 06:00 arasında.  

4. Daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5. Yönetici daha sonra aşağıdaki ayarlarda **Evet** ' i seçerek Endpoint Protection istemcisini yüklemek için özel bir cihaz istemcisi ayarı yapılandırır ve sonra bu özel Istemci ayarını Windows Embedded cihaz koleksiyonuna dağıtır:  

   - **İstemci bilgisayarlarda Endpoint Protection istemcisini yükle**  

   - **Yazma filtresi olan Windows Embedded cihazları için Endpoint Protection istemci yüklemesini yürüt (yeniden başlatma gerekir)**  

   - **Bakım penceresi dışında Endpoint Protection istemci yükleme ve yeniden başlatma işlemlerine izin ver**  

     Configuration Manager istemcisi yüklendiğinde, bu ayarlar Endpoint Protection istemcisini yükler ve işletim sisteminde yalnızca bir katmana yazılmak yerine, yüklemenin bir parçası olarak kalıcı olmasını sağlar. Şirket güvenlik ilkeleri, kötü amaçlı yazılımdan koruma yazılımının her zaman yüklenmesini ve yöneticinin, yeniden başlatmaları durumunda kısa bir süre boyunca yük korumasız olma riskini de çalıştırmak istememesini gerektirir.  

   > [!NOTE]  
   >  Uç Nokta Koruma istemcisini yüklemek için gereken yeniden başlatmalar bir defalıktır ve bu, cihazların kurulumu sırasında ve ziyaretçi merkezi çalışmaya başlamadan önce olur. Uygulamaların veya yazılım tanımı güncelleştirmelerinin düzenli dağıtımının aksine, Endpoint Protection istemci aynı cihaza bir sonraki yüklenilişinde, şirket bir sonraki Configuration Manager sürümüne yükseltiyordan kaynaklanıyor olur.  

    Daha fazla bilgi için bkz. [Endpoint Protection yapılandırma](../../../protect/deploy-use/endpoint-protection-configure.md).  

6. İstemcinin yapılandırma ayarları artık yerinde olduğunda, yönetici Configuration Manager istemcilerini yüklemeye hazırlar. Yöneticinin istemcileri yükleyebilmesi için Windows Embedded cihazlarında yazma filtresini elle devre dışı bırakmaları gerekir. Yönetici, bilgi noktaları ile ilgili OEM belgelerini okur ve yazma filtrelerini devre dışı bırakmak için yönergelerini izler.  

    Yönetici, şirket standart adlandırma biçimini kullanacak şekilde cihazı yeniden adlandırır ve sonra CCMSetup 'ı istemci kaynak dosyalarını tutan eşlenmiş bir sürücüden aşağıdaki komutla çalıştırarak istemciyi el ile kurar: **CCMSetup. exe/MP: mpserver. cohovıneyardandwınlik. com SMSSITEKODU = CO1**  

    Bu komut, istemciyi yükler, **mpserver.cohovineyardandwinery.com**intranet FQDN'sine sahip yönetim noktasına atar ve **CO1**adlı birincil siteye atar.  

    Yönetici, istemcilerin yüklenmesi ve durumlarını siteye geri gönderilmesi sırasında her zaman bir süre sürer. Bu nedenle, yönetici istemcilerin başarıyla yüklendiğini, siteye atamasını ve Windows Embedded cihazlar için oluşturdukları koleksiyonda istemci olarak göründüğünü onaylamadan önce bekler.  

    Ek bir onay olarak, yönetici cihazlarda Denetim Masası 'ndaki Configuration Manager özelliklerini denetler ve bunları site tarafından yönetilen standart Windows bilgisayarlarıyla karşılaştırır. Örneğin, **Bileşenler** sekmesinde, **Donanım Envanteri Aracısı****Etkin**görünür ve **Eylemler** sekmesinde kullanılabilen 11 eylem olup bunların arasında **Uygulama Dağıtımı Değerlendirme Döngüsü** ve **Keşif Verisi Toplama Döngüsü**de vardır.  

    İstemcilerin başarıyla yüklendiğinden, atandığından ve yönetim noktasından istemci ilkesini aldığından emin olmak için yönetici, OEM 'deki yönergeleri izleyerek yazma filtrelerini el ile mümkün bir şekilde sunar.  

    Daha fazla bilgi için bkz.  

   -   [İstemcileri Windows bilgisayarlara dağıtma](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [İstemcileri bir siteye atama](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Configuration Manager istemcisi Windows Embedded cihazlarında yüklü olduğuna göre, yönetici bunları standart Windows istemcilerini yönettikleri şekilde yönetebilecekleri şekilde onaylar. Örneğin, Configuration Manager konsolundan, yönetici uzaktan denetimi kullanarak onları uzaktan yönetebilir, onlara yönelik istemci ilkesi başlatabilir ve istemci özelliklerini ve donanım envanterini görüntüleyebilir.  

    Bu cihazlar bir Active Directory etki alanına katıldığından, yöneticinin onları güvenilen istemci olarak elle onaylaması gerekmez ve Configuration Manager konsolundan onaylandıklarını doğrular.  

    Daha fazla bilgi için bkz. [istemcileri yönetme](../../../core/clients/manage/manage-clients.md).  

8. Etkileşimli sunu yazılımını yüklemek için yönetici, **Yazılım Dağıtma Sihirbazı 'nı** çalıştırır ve gerekli bir uygulamayı yapılandırır. Sihirbazın **Kullanıcı deneyimi** sayfasında, **Windows Embedded cihazlar Için filtre işleme yaz** bölümünde, **değişiklikleri son tarihte veya bakım penceresinde Yürüt (yeniden başlatma gerektirir)** seçeneğini seçen varsayılan seçeneği kabul ederler.  

    Yönetici, yeniden başlatmadan sonra uygulamanın devam ettiğinden emin olmak için yazma filtreleri için bu varsayılan seçeneği korur. böylece, her zaman kiosks kullanan ziyaretçilerin kullanımına açıktır. Günlük bakım penceresi, yüklemeyle ve olası güncelleştirmelerle ilgili yeniden başlatmaların gerçekleşebileceği güvenli bir süre sağlar.  

    Yönetici, uygulamayı Windows Embedded cihazlar koleksiyonuna dağıtır.  

    Daha fazla bilgi için bkz. [Configuration Manager ile uygulama dağıtma](../../../apps/deploy-use/deploy-applications.md).  

9. Yönetici, Endpoint Protection tanım güncelleştirmelerini yapılandırmak için yazılım güncelleştirmelerini kullanır ve otomatik dağıtım kuralı oluşturma Sihirbazı 'Nı çalıştırır. Bu ayarlar, Sihirbazı Endpoint Protection için uygun ayarlarla önceden doldurmak için **tanım güncelleştirmeleri** şablonunu seçer.  

     Bu ayarlar, sihirbazın **Kullanıcı Deneyimi** sayfasında şunları içerir:  

   - **Son tarih davranışı**: **Yazılım Yükleme** onay kutusu seçilmez.  

   - **Windows Embedded cihazlar için filtre işleme yaz**: **Değişiklikleri son tarihte veya bakım penceresinde yürüt (yeniden başlatma gerektirir)** onay kutusu seçilmez.  

     Yönetici bu varsayılan ayarları korur. Bu yapılandırmada bu iki seçenek bir arada, Uç Nokta Koruma ile ilgili tüm yazılım güncelleştirme tanımlarının gün içinde katmana yüklenmesini sağlar ve bakım penceresi sırasında yüklenmeyi ve yürütülmeyi beklemez. Bu, bilgisayarların güncel kötü amaçlı yazılımlardan koruma yazılımı çalıştırılmasına yönelik şirket güvenlik ilkesine en uygun olan yapılandırmadır.  

     > [!NOTE]  
     >  Uygulamalara yönelik yazılım yüklemelerinin tersine, Uç Nokta Koruma ile ilgili yazılım güncelleştirme tanımları çok sık, hatta günde birkaç kez olabilir. Çoğunlukla bunlar küçük dosyalardır. Güvenlikle ilgili bu tür dağıtımlarda, bakım penceresini beklemek yerine her zaman katmana yükleme yapmak çoğu kez yararlı olabilir. Cihaz yeniden başlatılırsa Configuration Manager istemcisi yazılım tanımı güncelleştirmelerini hızla yeniden yükler çünkü bu eylem bir değerlendirme denetimi başlatır ve sonraki zamanlanmış değerlendirmeye kadar beklemelidir.  

     Yönetici, otomatik dağıtım kuralı için Windows Embedded cihazlar koleksiyonunu seçer.  

     Daha fazla bilgi için bkz.  
               3. Adım: Istemci bilgisayarlara tanım güncelleştirmelerini Iletmek için Configuration Manager yazılım güncelleştirmelerini yapılandırma [Endpoint Protection yapılandırma](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. Yönetici, tüm değişiklikleri düzenli aralıklarla işleme yapan bir bakım görevi yapılandırmaya karar verir. Bu görev, yazılım güncelleştirme tanımlarının dağıtımını desteklemek, biriken ve cihaz her yeniden başlatıldığında yeniden yüklenmesi gereken güncelleştirmelerin sayısını azaltmak amaçlıdır. Yönetici deneyiminde bu, kötü amaçlı yazılımdan koruma programlarının daha verimli çalışmasına yardımcı olur.  

    > [!NOTE]  
    >  Katıştırılmış cihazlar değişiklikleri yürütmeyi destekleyen başka bir yönetim görevi çalıştırdığında bu yazılım güncelleştirme tanımları görüntüye otomatik olarak uygulanacaktır. Örneğin, etkileşimli sunu yazılımının yeni bir sürümünü yüklemek yazılım güncelleştirme tanımlarına yönelik değişiklikleri de uygulayacaktır. Veya her ay bakım penceresi sırasında yüklenen standart yazılım güncelleştirmelerini yüklemek de yazılım güncelleştirme tanımlarına yönelik değişiklikleri uygulayacaktır. Ne var ki standart yazılım güncelleştirmelerinin çalıştırılmadığı ve etkileşimli sunu yazılımının çok sık güncelleştirilme olasılığının bulunmadığı bu senaryoda, yazılım tanımı güncelleştirmeleri otomatik olarak görüntüye uygulanana kadar aylar geçebilir.  

     Yönetici önce, adı dışında bir ayarı olmayan özel bir görev sırası oluşturur. Görev sırası oluşturma Sihirbazı 'Nı çalıştırır:  

    1. **Yeni görev dizisi oluştur** sayfasında, yönetici **Yeni bir özel görev dizisi oluştur**' u seçer ve ardından **İleri**' ye tıklar.  

    2. **Görev dizisi bilgileri** sayfasında, yönetici, görev sırası adı için **katıştırılmış cihazlarda değişiklikleri yürütmek üzere bakım görevi** girer ve sonra **İleri**' ye tıklar.  

    3. **Özet** sayfasında, yönetici **İleri**' yi seçer ve sihirbazı tamamlar.  

       Yönetici daha sonra bu özel görev dizisini Windows Embedded cihazlar koleksiyonuna dağıtır ve zamanlamayı her ay çalışacak şekilde yapılandırır. Dağıtım ayarlarının parçası olarak değişikliklerin yeniden başlatmadan sonra kalıcı olması için değişiklikleri **son tarihte veya bakım penceresinde Yürüt (yeniden başlatma gerektirir)** onay kutusunu seçer. Bu dağıtımı yapılandırmak için yönetici, az önce oluşturduğu özel görev dizisini seçer ve sonra **giriş** sekmesinde, **dağıtım** grubunda, **Dağıt** ' a tıklayarak yazılım dağıtma sihirbazını başlatır:  

    4. **Genel** sayfasında, yönetici Windows Embedded cihazlar koleksiyonunu seçer ve ardından **İleri**' ye tıklar.  

    5. **Dağıtım ayarları** sayfasında, yönetici **gerekli** **amacını** seçip **İleri**' ye tıklar.  

    6. **Zamanlama** sayfasında, yönetici, bakım penceresi sırasında haftalık bir zamanlama belirtmek için **Yeni** ' ye tıklar ve sonra **İleri**' ye tıklar.  

    7. Yönetici, başka bir değişiklik yapmadan sihirbazı tamamlar.  

       Daha fazla bilgi için bkz.  
                 [Görevleri otomatikleştirmek için görev dizilerini yönetin](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Bilgi noktaları 'in otomatik olarak çalışması için yönetici, cihazları aşağıdaki ayarlarla yapılandırmak üzere bir betik Yazar:  

    - Parolası olmayan bir konuk hesabı kullanarak otomatik olarak oturum aç.  

    - Etkileşimli sunu yazılımını başlangıçta otomatik olarak çalıştır.  

      Yönetici, bu betiği Windows Embedded cihazlar koleksiyonuna dağıtmak için paketleri ve programları kullanır. Yönetici Yazılım Dağıtma Sihirbazı 'nı çalıştırdığında, yeniden başlatmadan sonra değişiklikleri kalıcı hale getirmek için **değişiklikleri son tarihte veya bakım penceresinde Yürüt (yeniden başlatma gerektirir)** onay kutusunu yeniden seçin.  

      Daha fazla bilgi için bkz. [paketler ve programlar](../../../apps/deploy-use/packages-and-programs.md).  

12. Aşağıdaki sabah, yönetici Windows Embedded cihazları denetler. Bunlar aşağıdakileri doğrulamalar:  

    - Konuk hesabı kullanılarak bilgi noktası otomatik olarak oturum açıyor.  

    - Etkileşimli sunu yazılımı çalışıyor.  

    - Uç Nokta Koruma istemcisi yüklü ve en yeni yazılım güncelleştirme tanımlarına sahip.  

    - Bakım penceresi sırasında cihaz yeniden başlatıldı.  

      Daha fazla bilgi için bkz.  

    - [Endpoint Protection nasıl izlenir](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Configuration Manager ile uygulamaları izleme](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. Yönetici, bilgi noktalarını izler ve bunların yöneticilerine başarılı bir şekilde yönetilmesini bildirir. Sonuç olarak, ziyaretçi merkezi için 20 bilgi noktası sipariş edilir.  

     El ile devre dışı bırakma ve sonra Yazma filtrelerini etkinleştirmeye yönelik Configuration Manager istemcisinin el ile yüklenmesini önlemek için, yöneticinin sıranın, Configuration Manager istemcisinin yükleme ve site atamasını zaten içeren özelleştirilmiş bir görüntü içermesi gerekir. Ayrıca, cihazlar şirket adlandırma biçimine göre adlandırılır.  

     Bilgi noktaları ziyaretçi merkezinin açılmasından bir hafta önce teslim edilir. Bu süre içinde bilgi noktaları ağa bağlanır, bunlarla ilgili tüm cihaz yönetimi otomatiktir ve bir yerel yönetici gerekmez. Yönetici, bilgi noktaları 'nın gerektiği şekilde çalıştığını onaylar:  

    -   Bilgi noktalarındaki istemciler site atamasını tamamlıyor ve Active Directory Etki Alanı Hizmetlerinden güvenilen kök anahtarı indiriyor.  

    -   Bilgi noktalarındaki istemciler Windows Embedded cihazlar koleksiyonuna otomatik olarak ekleniyor ve bakım penceresi ile yapılandırılıyor.  

    -   Uç Nokta Koruma istemcisi yüklüdür ve kötü amaçlı yazılımlardan korumaya yönelik en yeni yazılım güncelleştirme tanımlarına sahip.  

    -   Etkileşimli sunu yazılımı yüklü ve ziyaretçilere hazır olarak otomatik çalışıyor.  

14. Bu ilk kurulumdan sonra, güncelleştirmeler için gerekebilecek tüm yeniden başlatmalar yalnızca ziyaretçi merkezi kapalıyken gerçekleşir.  
