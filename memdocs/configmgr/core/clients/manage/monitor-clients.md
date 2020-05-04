---
title: İstemcileri izleme
titleSuffix: Configuration Manager
description: Configuration Manager 'da istemcilerin nasıl izleneceği hakkında ayrıntılı yönergeler alın
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1f31ac96f29fc302e601b8da071b1486f4e7df90
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715350"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Configuration Manager istemcileri izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcisini sitenizdeki Windows cihazlarına yükledikten sonra, Configuration Manager konsolundaki sistem durumlarını ve etkinliklerini izleyin.  


## <a name="about-client-status"></a><a name="bkmk_about"></a> İstemci durumu hakkında

Configuration Manager, istemci durumu olarak aşağıdaki bilgi türlerini sağlar:  

- **İstemci çevrimiçi durumu**: site, atanan yönetim noktasına bağlıysa bir cihazı **çevrimiçi** olarak kabul eder. İstemcinin çevrimiçi olduğunu göstermek için, yönetim noktasına ping benzeri iletiler gönderir. Yönetim noktası beş dakika içinde bir ileti almazsa, site istemciyi **çevrimdışı**olarak değerlendirir.  

- **İstemci etkinliği**: site, son yedi gün içinde Configuration Manager ile iletişim kurmışsa, istemciyi **etkin** olarak değerlendirir. Site, yedi gün içinde aşağıdaki işlemleri yapmamışsa, istemciyi **devre dışı** olarak kabul eder:  

    - İlke güncelleştirmesi istendi  
    - Sinyal iletisi gönderildi  
    - Gönderilen donanım envanteri  

- **İstemci denetimi**: Configuration Manager istemcisinin cihazda çalıştırdığı dönemsel değerlendirmenin durumu. Değerlendirme cihazı denetler ve bulduğu bazı sorunları düzeltebilir. Daha fazla bilgi için bkz. [istemci durum denetimleri](#BKMK_ClientHealth).  

     Windows 7 çalıştıran cihazlarda, istemci denetimi zamanlanmış bir görev olarak çalışır. Sonraki işletim sistemi sürümlerinde, istemci denetimi Windows bakım penceresi sırasında otomatik olarak çalışır.  

     Düzeltmeyi belirli cihazlarda (örneğin, iş açısından kritik bir sunucu) çalışmayacak şekilde yapılandırabilirsiniz. Değerlendirmek istediğiniz ek öğeler varsa, ek konfigürasyonları izlemek için Configuration Manager uyumluluk ayarları ' nı kullanın. Uyumluluk ayarları hakkında daha fazla bilgi için bkz. [plan, uyumluluk ayarlarını planlayın ve yapılandırın](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

- **Kullanımdan**çıkarıldı: site, silinmek üzere cihaz kaydını işaretledi. Aynı cihaza yönelik yeni bir kayıt, bir hiyerarşideki aynı veya farklı bir birincil siteye atandığında, bu davranış meydana gelebilir. Site, **eski bulma verilerini sil**site bakım görevini bir sonraki sefer çalıştırdığında bu cihazları siler.<!-- SCCMDocs issue #1418 -->  

- **Kullanımdan kalktı**: site aynı donanım kimliğine sahip yeni bir cihaz kaydı buldu, bu nedenle eski kaydı eski olarak işaretliyor. Raporlar aynı cihazın eski kayıtlarını birden çok kez sayamıyor. Hala eski cihazlara ilke hedefleyebilirsiniz. Site, 90 gün sonra etkin olmayan bir kayıt için sinyal almadığında, artık kullanılmayan cihaz, **eski Istemci bulma verilerini sil**site bakım görevini çalıştırdığında kaldırılır.


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a>Tek tek istemcileri izleme

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin. **Cihazlar** düğümünü seçin ya da **Cihaz Koleksiyonları**altında bir koleksiyon seçin.  

    Her satırın başındaki simgeler cihazın çevrimiçi durumunu gösterir:  

    |||  
    |-|-|  
    |![istemciler için çevrimiçi durum simgesi](../../../core/clients/manage/media/online-status-icon.png)|Cihaz çevrimiçi|  
    |![istemciler için çevrimdışı durum simgesi](../../../core/clients/manage/media/offline-status-icon.png)|Cihaz çevrimdışı|  
    |![istemciler için bilinmeyen durum simgesi](../../../core/clients/manage/media/unknown-status-icon.png)|Çevrimiçi durum bilinmiyor|  
    |![istemci yüklü değil](../../../core/clients/manage/media/client-not-installed.png)|İstemci cihazda yüklü değil|  

2. Daha ayrıntılı çevrimiçi durumu için, istemci çevrimiçi durum bilgilerini cihaz görünümüne ekleyin. Sütun başlığına sağ tıklayın ve eklemek istediğiniz çevrimiçi durum alanlarını seçin:

    - **Cihaz çevrimiçi durumu**: istemcinin şu anda çevrimiçi veya çevrimdışı olduğunu gösterir. (Bu durum, simgeler tarafından verilen bilgiler ile aynıdır.)  

    - **Son çevrimiçi saat**: istemci çevrimiçi durumunun çevrimiçi olarak değiştiğini gösterir  

    - **Son çevrimdışı zamanı** durumun ne zaman çevrimdışı olarak değiştirildiğini gösterir  

3. Ayrıntı bölmesinde daha fazla durum görmek için liste bölmesinde tek bir istemciyi seçin. Bu bilgiler istemci etkinliği ve istemci denetimi durumunu içerir.  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a>İstemci sistem durumu panosu

<!--3599209-->
Ortamınızın güvenliğini sağlamaya yardımcı olmak için yazılım güncelleştirmelerini ve diğer uygulamaları dağıtırsınız, ancak bu dağıtımlar yalnızca sağlıklı istemcilere ulaşın. Sağlıksız Configuration Manager istemcileri genel uyumluluğu olumsuz etkiler. İstemci durumunun belirlenmesi, paydaya bağlı olarak, kaç tane toplam cihazın yönetim kapsamınızda olması gerektiği konusunda zor olabilir mi? Örneğin, Active Directory tüm sistemleri keşfetseniz, bu kayıtlardan bazıları kullanımdan kaldırılan makineler için olsa bile, bu işlem paydayı arttırır.

Sürüm 1902 ' den başlayarak, ortamınızdaki Configuration Manager istemcilerinin sistem durumu hakkında bilgi içeren bir panoyu görüntüleyin. İstemci sistem durumunu, senaryo sistem durumunu ve sık karşılaşılan hataları görüntüleyin. İşletim sistemi ve istemci sürümlerine göre olası sorunları görmek için görünümü birkaç özniteliğe göre filtreleyin.

Configuration Manager konsolunda **izleme** çalışma alanına gidin. **İstemci durumu**' nu genişletin ve **istemci sistem durumu panosu** düğümünü seçin.

![İstemci sistem durumu panosu ekran görüntüsü](media/3599209-client-health-dashboard.png)

> [!Tip]  
> Ccmeval üzerinde hiçbir değişiklik yoktur.  

Varsayılan olarak, istemci sistem durumu panosu, son üç gün içinde etkin istemcileri ve istemcileri gösterir. Bu nedenle, bu panoda istemci sistem durumu geçmiş diğer kaynaklarından farklı sayılar görebilirsiniz. Örneğin, **Istemci durumu**altındaki diğer düğümler veya istemci durumu kategorisindeki raporlar.

### <a name="filters"></a>FilTReleri

Panonun üst kısmında, panoda görüntülenecek verileri ayarlamaya yönelik bir filtre kümesi vardır.

- **Koleksiyon**: varsayılan olarak, Pano **Tüm sistemler** koleksiyonundaki cihazları görüntüler. Görünümü, belirli bir koleksiyondaki cihazların bir alt kümesiyle kapsamını belirlemek için listeden bir cihaz koleksiyonu seçin.  

- **Çevrimiçi/çevrimdışı**: pano yalnızca çevrimiçi istemcileri görüntüler. Bu durum, istemcinin durumunu beş dakikada bir güncelleştiren istemci bildirim kanalından gelir. Daha fazla bilgi için bkz. [istemci durumu hakkında](monitor-clients.md#bkmk_about).  

- **Etkin \# günler**: varsayılan olarak, pano son üç günde etkin olan istemcileri görüntüler.  

- **Yalnızca hata**: görünümü yalnızca bir istemci sistem durumu hatası bildiren cihazlara kapsam.  

    > [!Tip]  
    > Bu filtreyi, istemci sürümü ve işletim sistemi sürümü kutucukları ile birlikte kullanın. Daha fazla bilgi için bkz. [Sürüm kutucukları](#version-tiles).

### <a name="client-health-percentage"></a>İstemci sistem durumu yüzdesi

Bu kutucuk, hiyerarşinizdeki genel istemci sistem durumunu gösterir.

Sağlıklı bir Configuration Manager istemcisi aşağıdaki özelliklere sahiptir:

- Çevrimiçi  
- Etkin bir şekilde veri gönderiyor  
- Tüm istemci sistem durumu değerlendirme denetimlerini geçirir  

Daha fazla bilgi için bkz. [istemci durumu hakkında](monitor-clients.md#bkmk_about).

Sağlıklı bir istemci, siteyle başarıyla iletişim kurar. İstemci ayarlarındaki tanımlı zamanlamalara göre tüm verileri raporlar.

Bir cihaz listesi görünümüne gitmek için bu grafiğin bir kesimini seçin.

### <a name="version-tiles"></a>Sürüm kutucukları

İstemci sistem durumunu Configuration Manager istemci sürümüne ve işletim sistemi sürümüne göre gösteren iki kutucuk vardır. Bu Kutucuklar, filtrelerinde **yalnızca hata**gibi değişiklikler yaptığınızda faydalıdır. Belirli bir sürümde herhangi bir sorunun tutarlı olup olmadığını vurgulamaya yardımcı olabilirler. Yükseltme kararları almanıza yardımcı olması için bu bilgileri kullanın.

Bir cihaz listesi görünümüne gitmek için bu grafiklerin segmentini seçin.

### <a name="scenario-health"></a>Senaryo durumu

Bu çubuk grafiğinde aşağıdaki temel senaryolar için genel sistem durumu gösterilmektedir:

- İstemci ilkesi
- Sinyal keşfi
- Donanım envanteri
- Yazılım envanteri
- Durum iletileri

Grafikteki belirli senaryolara odaklanarak odağı ayarlamak için seçicileri kullanın.

Aşağıdaki iki çubuk her zaman gösterilir:

- **Birleşik (tümü)**: tüm senaryoların BIRLEŞIMI (ve)  
- **Birleşik (any)**: senaryolardan en az bırı (veya)

> [!Tip]  
> Senaryo durumu, istemci ayarları yapılandırmanızda ölçülemez. Bu değerler, cihaz başına ilke sonuç kümesine bağlı olarak değişebilir. Senaryo sistem durumu için değerlendirme sürelerini ayarlamak için aşağıdaki adımları kullanın:
>
> - Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **istemci durumu** düğümünü seçin.  
> - Şeritte **Istemci durumu ayarları**' nı seçin.  
>
> Varsayılan olarak, bir istemci, senaryoya özgü verileri **7 gün**içinde göndermezse Configuration Manager, bu senaryo için sağlıksız olduğunu varsayar.

### <a name="top-10-client-health-failures"></a>İlk 10 istemci sistem durumu başarısızlığı

Bu grafik, ortamınızdaki en yaygın sorunları listeler. Bu hatalar Windows veya Configuration Manager gelir.

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> Tüm istemcilerin durumunu izleme

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **istemci durumu** düğümünü seçin. İstemci etkinliğinin ve site genelindeki istemci denetimlerinin genel istatistiklerini gözden geçirin. Farklı bir koleksiyon seçerek bilgilerin kapsamını değiştirin.  

2. Bildirilen istatistiklerle ilgili ayrıntıya gitmek için, bildirilen bilgilerin adını seçin. Örneğin, **İstemci denetimini geçen etkin istemciler veya sonuç yok**. Ardından ayrı istemcilerle ilgili bilgileri gözden geçirin.  

3. Configuration Manager sitenizdeki istemci etkinliğini gösteren grafikleri görmek için **Istemci etkinliği** ' ni seçin.  

4. Configuration Manager sitenizdeki istemci denetimlerinin durumunu gösteren grafikleri görmek için **Istemci denetimi** ' ni seçin.  

    İstemci denetimi sonuçları veya istemci etkinliği belirtilen yüzdenin altına düştüğünde size bildirimde bulunan uyarıları yapılandırın. Site, belirli bir istemci yüzdesinde düzeltme başarısız olduğunda da sizi uyarır. Daha fazla bilgi için bkz. [istemci durumunu yapılandırma](../deploy/configure-client-status.md).  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a>İstemci sistem durumu denetimleri

İstemci denetimi aşağıdaki denetimleri ve düzeltmeleri çalıştırır:  

|İstemci Denetimi|Düzeltme işlemi|Daha fazla bilgi|  
|------------------|------------------------|----------------------|  
|İstemci denetiminin yakın zamanda çalıştırıldığını doğrula|İstemci denetimini çalıştır|İstem denetiminin son üç günde en az bir kez gerçekleştirilip gerçekleştirilmediğini denetler.|  
|İstemci önkoşullarının yüklü olduğunu doğrulama|İstemci önkoşullarını yükleme|İstemci önkoşullarının yüklü olup olmadığını denetler. Önkoşulları keşfetmek için istemci yükleme klasöründeki ccmsetup.xml dosyasını okur.|  
|WMI deposu bütünlük sınaması|Configuration Manager istemcisini yeniden yükleme|Configuration Manager istemci girdilerinin WMI 'de mevcut olduğunu denetler.|  
|İstemci hizmetinin çalıştığını doğrulama|İstemci (SMS Aracı Ana Makinesi) hizmetini başlatma|Ek bilgi yok|  
|WMI Olay Havuzu Sınaması.|İstemci hizmetini yeniden başlatma|Configuration Manager ilgili WMI olay havuzunun kayıp olup olmadığını denetleyin|  
|Windows Yönetim Araçları (WMI) hizmetinin var olduğunu doğrulama|Düzeltme yok|Ek bilgi yok|  
|İstemcinin düzgün yüklendiğini doğrulama|İstemciyi yeniden yükleme|Ek bilgi yok|  
|Kötü amaçlı yazılım önleme hizmetinin başlatma türünün otomatik olduğunu doğrulama|Hizmet başlatma türünü otomatik olarak sıfırla|Ek bilgi yok|  
|Kötü amaçlı yazılım önleme hizmetinin çalıştığını doğrulama|Kötü amaçlı yazılım önleme hizmetini başlatma|Ek bilgi yok|  
|Windows Update hizmetinin başlatma türünün otomatik veya manuel olduğunu doğrulama|Hizmet başlatma türünü otomatik olarak sıfırla|Ek bilgi yok|  
|İstemci hizmetinin (SMS Aracı Ana Makinesi) başlatma türünün otomatik olduğunu doğrulama|Hizmet başlatma türünü otomatik olarak sıfırla|Ek bilgi yok|  
|Windows Yönetim Araçları (WMI) hizmetinin çalıştığını doğrulayın.|Windows Yönetim Araçları hizmetini başlatma|Ek bilgi yok|  
|Microsoft SQL CE veritabanının durumunu doğrulama|Configuration Manager istemcisini yeniden yükleme|Ek bilgi yok|  
|Microsoft Policy Platform WMI Bütünlük Sınaması|Microsoft Policy Platform'u onarma|Ek bilgi yok|  
|Microsoft Policy Platform Hizmeti'nin bulunduğunu doğruma|Microsoft Policy Platform'u onarma|Ek bilgi yok|  
|Microsoft Policy Platform hizmeti başlatma türünün manuel olduğunu doğrulama|Hizmet başlatma türünü manuel olarak sıfırlama|Ek bilgi yok|  
|Arka Plan Akıllı Aktarım Hizmetinin var olduğunu doğrulama|Düzeltme yok|Ek bilgi yok|  
|Arka Plan Akıllı Aktarım Hizmeti Hizmetinin başlatma türünün otomatik veya manuel olduğunu doğrulama|Hizmet başlatma türünü otomatik olarak sıfırla|Ek bilgi yok|  
|Ağ İnceleme Hizmeti başlatma türünün manuel olduğunu doğrulama|Yüklüyse hizmet başlatma türünü manuel olarak sıfırlama|Ek bilgi yok|  
|Windows Yönetim Araçları (WMI) hizmeti başlatma türünün otomatik olduğunu doğrulama|Hizmet başlatma türünü otomatik olarak sıfırla|Ek bilgi yok|  
|Windows 8 cihazlarındaki Windows Update hizmeti başlangıç türünün otomatik veya manuel olduğunu doğrulama|Hizmet başlatma türünü manuel olarak sıfırlama|Ek bilgi yok|  
|İstemci (SMS Aracı Ana Makinesi) hizmetinin var olduğunu doğrulayın.|Düzeltme yok|Ek bilgi yok|  
|Configuration Manager Uzaktan Denetim hizmetinin başlatma türünün otomatik veya manuel olduğunu doğrulama|Hizmet başlatma türünü otomatik olarak sıfırla|Ek bilgi yok|  
|Configuration Manager Uzaktan Denetim hizmetinin çalıştığını doğrulama|Uzaktan denetim hizmetini başlatma|Ek bilgi yok|  
|Uyandırma proxy hizmetinin (ConfigMgr Uyandırma Proxy) çalıştığını doğrulama|ConfigMgr Uyandırma Proxy hizmetini başlatma|Bu istemci denetimi, desteklenen istemci işletim sistemlerinde **Güç Yönetimi**: **Uyandırma proxy'sini etkinleştir** istemci ayarı **Evet** ise gerçekleştirilir.|  
|Uyandırma proxy hizmetinin (ConfigMgr Uyandırma Proxy) başlatma türünün otomatik olduğunu doğrulama|ConfigMgr Uyandırma Proxy hizmet başlatma türünü otomatik olarak sıfırlama|Bu istemci denetimi, desteklenen istemci işletim sistemlerinde **Güç Yönetimi**: **Uyandırma proxy'sini etkinleştir** istemci ayarı **Evet** ise gerçekleştirilir.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>İstemci dağıtım günlük dosyaları

İstemci dağıtımı ve yönetim işlemleri tarafından kullanılan günlük dosyaları hakkında daha fazla bilgi için bkz. [günlük dosyaları](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
