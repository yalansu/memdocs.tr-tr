---
title: Yazılım kullanım ölçümü ile uygulama kullanımını izleme
titleSuffix: Configuration Manager
description: Configuration Manager yazılım ölçümüne sunulan işlemler hakkında bilgi edinin.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710086"
---
# <a name="software-metering-in-configuration-manager"></a>Configuration Manager 'de yazılım kullanım ölçümü

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager yazılım kullanım ölçümünü kullanırken gerçekleştirebileceğiniz tüm işlemlerin bir başvurusunu içerir.

> [!IMPORTANT]
>  Yazılım kullanım ölçümü, dosya adı sonu **.exe**olan Windows PC masaüstü uygulamalarını izlemek için kullanılır. Yazılım kullanım ölçümü modern Windows uygulamalarını (örneğin, Windows 8 tarafından kullanılanlar) izlemez.

##  <a name="prerequisites-for-software-metering"></a>Yazılım kullanım ölçümü için önkoşullar
Yazılım kullanım ölçümünün dış bağımlılıkları yoktur, yalnızca ürün içinde bağımlılıkları vardır.

|Bağımlılık|Daha fazla bilgi|
|----------------|----------------------|
|Yazılım kullanım ölçümü için istemci ayarları.|Yazılım kullanım ölçümünü kullanmak için **İstemcilerde yazılım kullanım ölçümünü etkinleştir** istemci ayarı etkinleştirilmeli ve bilgisayarlara dağıtılmalıdır. Hiyerarşideki tüm bilgisayarlara yazılım kullanım ölçümü ayarlarını dağıtabilir veya bir bilgisayar grubuna özel ayarları dağıtabilirsiniz. Bu konudaki **yazılım kullanım ölçümünü yapılandırma** konusuna bakın.|
|Raporlama hizmetleri noktası.|Yazılım kullanım ölçümü raporlarını görüntüleyebilmek için bir raporlama hizmetleri noktasını yapılandırmanız gerekir. Daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).|

##  <a name="configure-software-metering"></a>Configure software metering
 Bu yordam, yazılım kullanım ölçümü için varsayılan istemci ayarlarını yapılandırır ve hiyerarşinizdeki tüm bilgisayarlara uygular. Bu ayarların yalnızca bazı bilgisayarlara uygulanmasını istiyorsanız özel bir cihaz istemcisi ayarı oluşturun ve bu ayarı, üzerinde yazılım kullanım ölçümünü kullanmak istediğiniz bilgisayarları içeren bir koleksiyona dağıtın. Özel cihaz ayarları oluşturma hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md).

1. Configuration Manager konsolunda, **Yönetim** > **istemci ayarları** > **varsayılan istemci ayarları**' na tıklayın.

2. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.

3. **Varsayılan Ayarlar** iletişim kutusunda **Yazılım Kullanım Ölçümü**’ne tıklayın.

4. **Cihaz Ayarları** listesinde aşağıdakileri yapılandırın:

   -   **İstemcilerde yazılım kullanım ölçümünü etkinleştir**: Yazılım kullanım ölçümünü etkinleştirmek için **True** öğesini seçin.

   -   **Verile toplamayı zamanla**: Yazılım kullanım ölçümünün istemci bilgisayarlardan ne sıklıkta toplandığını yapılandırın. Varsayılan değer olan **7 gün** ’ü kullanın veya özel bir zamanlama belirtmek için **Zamanlama** ’ya tıklayın.

5. **Varsayılan Ayarlar** iletişim kutusunu kapatmak için **Tamam** 'a tıklayın.

   İstemci bilgisayarlar, istemci ilkesini sonraki sefer indirdiklerinde bu ayarlarla yapılandırılır. Tek bir istemci için ilke almayı başlatmak için bkz. [Istemcileri yönetme](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a> Yazılım kullanım ölçümü kuralları oluşturma
 Configuration Manager siteniz için yeni bir yazılım kullanım ölçümü kuralı oluşturmak için yazılım kullanım ölçümü kuralı oluşturma Sihirbazı ' nı kullanın.

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **yazılım ölçümü**' ne tıklayın.

3.  **Giriş** sekmesindeki **Oluştur** grubunda **Yazılım Kullanım Ölçümü Kuralı Oluştur**'a tıklayın.

4.  Yazılım kullanım ölçümü kuralı oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdaki bilgileri belirtin:

    -   **Ad** - Yazılım kullanım ölçümü kuralının adı. Bu ad benzersiz ve açıklayıcı olmalıdır.

        > [!NOTE]
        >  Kurallarda yer alan dosya adı farklıysa yazılım kullanım ölçümü kuralları aynı adı paylaşabilir.

    -   **Dosya Adı** - Ölçmek istediğiniz program dosyasının adı. **Gözat** ’a tıklayarak **Aç** iletişim kutusunu görüntüleyebilir ve buradan kullanılacak bir program dosyası seçebilirsiniz.

        > [!NOTE]
        >  **Dosya adı** kutusuna yürütülebilir dosya adını yazarsanız, bu dosyanın var olup olmadığını veya gerekli üst bilgileri içerip içermediğini belirlemek için bir denetim yapılmaz. Mümkün olduğunda, **Gözat** ’a tıklayın ve ölçülecek yürütülebilir dosyayı seçin.
        >
        >  Dosya adında joker karakterlere izin verilmez.
        >
        >  **Özgün dosya adı** için bir değer belirtilirse bu kutu isteğe bağlıdır.

    -   **Özgün Dosya Adı** - Ölçmek istediğiniz yürütülebilir dosyanın adı. Bu ad, dosya adının kendisiyle değil, dosyanın üst bilgisindeki bilgilerle eşleşir; böylece, yürütülebilir dosyanın yeniden adlandırıldığı ancak dosyayı özgün adına göre ölçmek istediğiniz durumlarda yararlı olabilir.

        > [!NOTE]
        >  Özgün dosya adında joker karakterlere izin verilmez.
        >
        >  **Dosya Adı** için bir değer belirtilirse bu kutu isteğe bağlıdır.

    -   **Sürüm** - Ölçmek istediğiniz yürütülebilir dosyanın sürümü. Herhangi bir karakter dizesini veya joker karakterini (?) göstermek için joker karakterini (&#42;) kullanabilirsiniz (? ) tek bir karakteri temsil eder. Yürütülebilir dosyanın tüm sürümleri için ölçüm yapmak istiyorsanız, varsayılan değeri (&#42;) kullanın.

    -   **Dil** - Ölçülecek yürütülebilir dosyanın dili. Varsayılan dil, kullanmakta olduğunuz işletim sisteminin geçerli yerel ayarıdır. **Gözat** düğmesine tıklayarak ölçülecek bir yürütülebilir dosya seçerseniz, dil bilgisinin dosya üst bilgisinde mevcut olması durumunda bu kutu otomatik olarak doldurulur. Bir dosyanın tüm dil sürümlerini ölçmek için açılır listede **Tümü** öğesini seçin.

    -   **Açıklama** - Yazılım ölçüm kuralı için isteğe bağlı bir açıklama.

    -   **Bu yazılım kullanım ölçümü kuralını aşağıdaki istemcilere uygula** – yazılım kullanım ölçümü kuralını hiyerarşideki tüm istemcilere veya **Site** listesinde belirtilen siteye atanmış istemcilere uygulamayı seçin.

5.  Devam etmek için **İleri**'ye tıklayın.

6.  Ayarları gözden geçirip onaylayın ve ardından sihirbazı tamamlayarak yazılım kullanım ölçümü kuralını oluşturun. Yeni yazılım kullanım ölçümü kuralı **Varlıklar ve Uyumluluk** çalışma alanının **Yazılım Kullanım Ölçümü** düğümünde gösterilir.

##  <a name="configure-automatic-software-metering-rules"></a> Otomatik yazılım kullanım ölçümü kurallarını yapılandırma
 Configuration Manager ' de yazılım kullanım ölçümünü, site veritabanında tutulan son kullanım Envanter verilerinden devre dışı bırakılmış yazılım kullanım ölçümü kurallarını otomatik olarak oluşturacak şekilde yapılandırabilirsiniz. Bu envanter verilerini, yalnızca belirtilen bir bilgisayar yüzdesinde kullanılan uygulamalar için ölçüm kurallarının oluşturulmasını sağlayacak şekilde yapılandırabilirsiniz. Ayrıca, sitede izin verilen otomatik olarak oluşturulmuş yazılım kullanım ölçümü kurallarının üst sınırını belirtebilirsiniz.

> [!NOTE]
>  Varsayılan olarak, otomatik olarak oluşturulan yazılım kullanım ölçümü kuralları devre dışıdır. Bu kurallardan kullanım verilerini toplamaya başlamadan önce bunları etkinleştirmeniz gerekir.

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **yazılım ölçümü**' ne tıklayın ve ardından **giriş** sekmesinde, **Ayarlar** grubunda, **yazılım kullanım ölçümü özellikleri**' ne tıklayın.

3.  **Yazılım Kullanım Ölçümü Özellikleri** iletişim kutusunda aşağıdakileri yapılandırın:

    -   **Veri tutma (gün cinsinden)** - Yazılım kullanım ölçümü kuralları tarafından oluşturulan verilerin site veritabanında tutulduğu süreyi belirtir. Varsayılan değer **90** gündür.

    -   **En son envanter verilerinden devre dışı ölçüm kurallarını otomatik olarak oluştur**seçeneğini etkinleştirin.

    -   **Yazılım ölçüm kuralının otomatik olarak oluşturulmasına neden olacak, bir program kullanması gereken hiyerarşideki bilgisayar yüzdesini belirtin:** - Varsayılan değer yüzde **10** ’dur.

    -   **Kuralların otomatik olarak oluşturulmasının devre dışı bırakılmasına neden olacak, hiyerarşide aşılacak yazılım ölçüm kuralı sayısını belirtin:** - Varsayılan değer **100** kuraldır.

4.  **Tamam** ’a tıklayarak **Yazılım Kullanım Ölçümü Özellikleri** iletişim kutusunu kapatın.

##  <a name="manage-software-metering-rules"></a> Yazılım kullanım ölçümü kurallarını yönetme
 **Varlıklar ve Uyumluluk** çalışma alanında **Yazılım Kullanım Ölçümü**’nü seçin, yönetilecek yazılım kullanım ölçümü kuralını seçin ve ardından bir yönetim görevi seçin.

 Seçmeden önce bazı bilgiler gerektirebilen yönetim görevleri hakkında daha fazla bilgi için aşağıdaki tabloyu kullanın.

|Yönetim Görevi|Ayrıntılar|
|---------------------|-------------|
|**Etkinleştir**<br /><br /> **Devre Dışı Bırak**|Bir yazılım kullanım ölçümü kuralını etkinleştirir veya devre dışı bırakır. Bu ayar istemci ayarlarının **İstemci İlkesi** bölümündeki **İstemci ilkesi yoklama aralığı** ’na göre istemci bilgisayarlara indirilir (varsayılan olarak 60 dakikada bir).<br /><br /> Bkz. [istemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md) .|

##  <a name="monitor-software-metering"></a> Yazılım kullanım ölçümünü izleme
 Configuration Manager yazılım kullanım ölçümü, yazılım kullanım ölçümü işlemleriyle ilgili bilgileri izlemenize olanak tanıyan çeşitli yerleşik raporlar içerir. Bu raporlar **Yazılım Kullanım Ölçümü**rapor kategorisindedir.

 Configuration Manager raporlamayı yapılandırma hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).

 Ayrıca, yazılım kullanım ölçümü tarafından Configuration Manager veritabanında depolanan verileri temel alan sorgular ve koleksiyonlar oluşturabilirsiniz.

 Configuration Manager Koleksiyonlar hakkında daha fazla bilgi için bkz. [koleksiyonlara giriş](../../core/clients/manage/collections/introduction-to-collections.md).

 Configuration Manager sorguları hakkında daha fazla bilgi için bkz. [sorgulara giriş](../../core/servers/manage/introduction-to-queries.md).

##  <a name="security-and-privacy-for-software-metering"></a>Yazılım kullanım ölçümü için güvenlik ve gizlilik

### <a name="security-issues-for-software-metering"></a>Yazılım Kullanım Ölçümü için Güvenlik Sorunları
 Saldırgan, yazılım kullanım ölçümü istemci ayarı devre dışı olduğunda bile yönetim noktası tarafından kabul edilecek Configuration Manager için geçersiz yazılım kullanım ölçümü bilgileri gönderebilir. Bu, hiyerarşide çoğaltılan çok sayıda ölçüm kuralına yol açabilir ve ağ üzerinde hizmet reddine ve site sunucularının Configuration Manager.

 Bir saldırgan geçersiz yazılım kullanım ölçümü verileri oluşturabileceğinden, yazılım kullanım ölçümü bilgilerinin yetkili olduğunu düşünmeyin.

 Yazılım kullanım ölçümü varsayılan olarak bir istemci ayarı olarak etkindir.

###  <a name="privacy-information-for-software-metering"></a> Yazılım Kullanım Ölçümü için Gizlilik Bilgileri
 Yazılım kullanım ölçümü, istemci bilgisayarlardaki uygulama kullanımını izler. Yazılım kullanım ölçümü varsayılan olarak etkindir. Hangi uygulamaların ölçüleceğini yapılandırmanız gerekir. Ölçüm bilgileri Configuration Manager veritabanında depolanır. Bilgiler bir yönetim noktasına aktarım sırasında şifrelenir, ancak Configuration Manager veritabanında şifreli biçimde depolanmaz.

 Bu bilgiler **Eski Yazılım Kullanım Ölçümü Verilerini Sil** (beş günde bir) ve **Eski Yazılım Kullanım Ölçümü Özet Verilerini Sil** (270 günde bir) site bakım görevleri tarafından silinene kadar veritabanında tutulur. Silme aralığını yapılandırabilirsiniz. Ölçüm bilgileri Microsoft'a gönderilmez.

 Yazılım kullanım ölçümünü yapılandırmadan önce gizlilik gereksinimlerinizi dikkate alın.

## <a name="example-scenario-for-using-software-metering"></a>Yazılım kullanım ölçümü kullanma örnek senaryosu
 Bu bölümde, aşağıdaki iş gereksinimlerini çözmenize yardımcı olabilecek örnek bir yazılım kullanım ölçümü kuralı oluşturursunuz:

- Şirketinizde belirli bir uygulamanın kaç tane kopyası olduğunu belirleme

- Bir uygulamanın kullanılmayan tüm kopyalarını bulma

- Hangi kullanıcıların belirli bir uygulamayı düzenli olarak kullandığını belirleme

  Woodgrove Bank, standart ofis üretkenliği paketi olarak Microsoft Office 2010 dağıtmıştır. Ancak, eski bir uygulamayı desteklemek için bazı bilgisayarların Microsoft Office Word 2003 çalıştırmaya devam etmesi gerekmektedir. BT departmanı, eski uygulama artık kullanılmıyorsa bu Word 2003 kopyalarını kaldırarak destek ve lisanslama maliyetlerini azaltmak istemektedir. Yardım masası ayrıca hangi kullanıcıların eski uygulamayı kullandığını belirlemek istemektedir.

  Woodgrove Bank 'ın BT sistemleri Yöneticisi, bu iş hedeflerine ulaşmak için Configuration Manager ' de yazılım ölçümü kullanır. Yönetici aşağıdaki eylemleri gerçekleştirir:

- Yazılım kullanım ölçümü önkoşullarını denetler ve Raporlama Hizmetleri noktasının yüklü ve çalışır durumda olduğunu doğrular.
- Yazılım kullanım ölçümü için varsayılan istemci ayarlarını yapılandırır:<br>Yönetici yazılım kullanım ölçümünü sunar ve her yedi günde bir kez varsayılan veri toplama zamanlamasını kullanır.<br>Yönetici, **Bu dosya türlerini envantere**alarak yazılım envanteri istemci ayarını yapılandırarak. exe uzantısına sahip dosyaları envantere almak için yazılım envanterini yapılandırır.<br>Yönetici, eski uygulamayı izlemek için **Woodgrove. exe**adlı yeni bir yazılım kullanım ölçümü kuralı ekler.
- İstemci bilgisayarlar **Woodgrove. exe** yürütülebilir dosyası için kullanım verilerini bildirmeye başladıktan sonra yedi gün bekler.
- Yönetici, hangi bilgisayarlarda **Woodgrove. exe** uygulamasının yüklü olduğunu görmek için **ölçülen tüm yazılım programları Için** Configuration Manager raporu yüklemesini kullanır.
- Altı ay sonra, yönetici **ölçülen bir programın yüklendiği ancak belirtilen bir tarihten bu yana programı çalıştırmayan**, yazılım kullanım ölçümü kuralını ve geçmişte altı ay tarihini belirterek rapor bilgisayarlarını çalıştırır. Bu rapor, geçen altı ay içinde programı çalıştırmayan 120 bilgisayarı tanımlar.
- Yönetici, eski uygulamanın tanımlanan bilgisayarlarda gerekli olmadığını onaylamak için bazı başka denetimler yapar. Yönetici daha sonra eski uygulamayı ve Word 2003 kopyasını bu bilgisayarlardan kaldırır.<br>Yönetici, yardım masasına eski uygulamayı kullanmaya devam eden kullanıcıların listesini sağlamak için **belirli bir ölçümlenen yazılım programını çalıştıran kullanıcılar** raporunu çalıştırır.
- Yönetici, yazılım kullanım ölçümü raporlarını haftada bir denetlemeye devam eder ve gerekirse düzeltici eylem gerçekleştirir.

  Bu eylemin bir sonucu olarak, artık gerekli olmayan uygulamaların kaldırılması yoluyla BT destek ve lisanslama maliyetleri azaltılır. Ayrıca, yardım masası eski uygulamayı çalıştıran kullanıcılar için istediği listeye artık sahiptir.
