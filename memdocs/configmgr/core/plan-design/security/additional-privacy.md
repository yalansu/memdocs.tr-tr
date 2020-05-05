---
title: Ek gizlilik bilgileri
titleSuffix: Configuration Manager
description: Microsoft 'un Configuration Manager verileri nasıl toplayıp kullandığını öğrenin.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6891a46050bb83e54fb34b97d9129fcb5873785
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718675"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Configuration Manager gizliliği hakkında ek bilgiler

*Uygulama hedefi: Configuration Manager (geçerli dal)*


## <a name="updates-and-servicing"></a>Güncelleştirmeler ve bakım

Configuration Manager, ortamınızı en son güncelleştirmeler ve özelliklerle güncel tutmaya yardımcı olan bir güncelleştirme modeli kullanır. Bu özellik, hizmet bağlantı noktası adlı bir site sistem rolü kullanır. Bu rolün yükleneceği sunucuyu seçin. 

Toplanan bilgiler ve bu bilgilerin nasıl kullanıldığı hakkında daha fazla bilgi için bkz. [kullanım verileri](#usage-data).



## <a name="usage-data"></a>Kullanım verileri

Configuration Manager, Microsoft 'un gelecekteki sürümlerin yükleme deneyimini, kalitesini ve güvenliğini geliştirmek için kullandığı, kendisi hakkında tanılama ve kullanım verileri toplar.
Tanılama ve kullanım verileri her bir Configuration Manager hiyerarşisi için etkinleştirilir. Her birincil sitede ve merkezi yönetim sitesinde haftalık olarak çalışan SQL Server sorgulardan oluşur. Hiyerarşi bir merkezi yönetim sitesi kullandığında, birincil sitelerden veriler daha sonra bu siteye çoğaltılır. Hiyerarşinizin en üst düzey sitesinde hizmet bağlantı noktası, Güncelleştirmeleri denetlerken bu bilgileri gönderir. Hizmet bağlantı noktası çevrimdışı moddaysa bilgiler hizmet bağlantı aracını kullanılarak aktarılır.

Configuration Manager yalnızca sitenin SQL Server veritabanından veri toplar ve doğrudan istemcilerden veya site sunucularından veri toplamaz.

Yöneticiler, Configuration Manager konsolunun **kullanım verileri** bölümüne giderek toplanan veri düzeyini değiştirebilir.

Kullanım verileri düzeyleri ve ayarları hakkında daha fazla bilgi için bkz. [Tanılama ve kullanım verileri](../diagnostics/diagnostics-and-usage-data.md).



## <a name="log-analytics-connector"></a>Log Analytics Bağlayıcısı

Log Analytics Bağlayıcısı, Koleksiyonlar gibi verileri Configuration Manager Azure bulut hizmeti 'ne eşitler. Yönetici özelliği yapılandırdığında Azure abonelik KIMLIĞI ve gizli anahtar Configuration Manager veritabanında depolanır. Hem Azure Active Directory istemci parolası hem de Azure çalışma alanı paylaşılan anahtarı şirket içi Configuration Manager veritabanında depolanır. Configuration Manager ile Azure arasındaki tüm iletişimler HTTPS kullanır. Microsoft 'a rastgele tanılama ve kullanım verileri dışında Koleksiyonlar hakkında ek bilgi sağlanmaz. 

Log Analytics toplanan bilgiler hakkında daha fazla bilgi için bkz. [Log Analytics veri güvenliği](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Varlık Yönetim Bilgileri

Varlık Yönetim Bilgileri, yöneticilerin yapılandırma standartları ile uyumluluk tanımlamasına, izlemesine ve BT yönetimine olanak sağlar. Fiziksel ve sanal uygulamaların dağıtımında ölçüm ve raporlama, kuruluşların yazılım lisanslama hakkında daha iyi kararlar almasına ve lisans sözleşmelerine uyum sağlamasına yardımcı olur. Configuration Manager istemcilerinden kullanım verilerini topladıktan sonra koleksiyonlar, sorgular ve raporlama dahil olmak üzere verileri görüntülemek için farklı özellikler kullanabilirsiniz.

Her eşitlemede, bilinen yazılımların bir kataloğu Microsoft 'tan indirilir. Kuruluşunuzda bulunan kategorilere ayrılmamış yazılım başlıkları hakkında Microsoft bilgilerini, yeniden aranmak ve kataloğa eklenmek üzere gönderilmesini seçebilirsiniz. Bu bilgileri karşıya yüklemeden önce bir iletişim kutusu karşıya yüklenecek verileri gösterir. Karşıya yüklenen veriler geri çekilemez. Varlık Yönetim Bilgileri, Microsoft 'a Kullanıcı ve bilgisayar ve lisans kullanımı hakkında bilgi göndermez.

Bir yazılım başlığı karşıya yüklendikten sonra, Microsoft araştırmacıları bu bilgiyi belirler, kategorilere atar ve bu özelliği kullanan diğer tüm müşteriler ve kataloğun diğer müşterileri için kullanılabilir hale getirir. Karşıya yüklenen tüm yazılım başlıkları herkese açık hale gelir. Uygulama ve kategorisi kataloğun bir parçası haline gelir ve ardından kataloğun diğer tüketicilerine indirilebilir. Varlık Yönetim Bilgileri veri toplamasını yapılandırmadan ve Microsoft'a bilgi gönderme kararı vermeden önce, kuruluşunuzun gizlilik gereksinimlerini dikkate alın.

Varlık Yönetim Bilgileri Configuration Manager varsayılan olarak etkinleştirilmemiştir. Kategorilere ayrılmamış başlıkları karşıya yüklemek hiçbir şekilde otomatik olarak gerçekleşmez ve sistem bu görevi otomatikleştirmek için tasarlanmamıştır. Her yazılım programının yüklenmesini elle seçmeniz ve onaylamanız gerekir.



## <a name="endpoint-protection"></a>Uç Nokta Koruma

Microsoft Bulut koruma hizmeti daha önce Microsoft Etkin Koruma Hizmeti veya HARITALAR olarak bilinirdi.

İlgili ürünler System Center Endpoint Protection ve Configuration Manager Endpoint Protection özelliğidir (System Center Endpoint Protection ve Windows 10 için Windows Defender 'ı yönetmek için). Bu özellik, Linux için System Center Endpoint Protection veya Mac için System Center Endpoint Protection için uygulanmıyor.

Microsoft Bulut koruma hizmeti kötü amaçlı yazılımdan koruma topluluğu, System Center Endpoint Protection kullanıcıları içeren, gönüllü dünya çapında bir çevrimiçi topluluk. Microsoft Bulut koruma hizmeti 'ne katılırsanız, System Center Endpoint Protection otomatik olarak Microsoft 'a bilgi gönderir. Microsoft bu bilgileri olası tehditleri araştırmak ve System Center Endpoint Protection verimliliğini artırmaya yardımcı olmak için kullanır. Bu topluluk, yeni kötü amaçlı yazılımların yayılmasını önlemeye yardımcı olur. Bir Microsoft Bulut koruma hizmeti raporu, Endpoint Protection istemcisinin kaldırabileceği kötü amaçlı yazılım veya istenmeyebilecek yazılım hakkındaki ayrıntıları içeriyorsa Microsoft Bulut koruma hizmeti, en son imzayı çözmek için indirir. Microsoft Bulut koruma hizmeti, "yanlış pozitif sonuçlar" da bulabilir ve bunları çözebilir. (Yanlış pozitif sonuçlar, başlangıçta kötü amaçlı yazılım olarak belirlenen bir şeyin olmaması değildir.) 

Microsoft Bulut koruma hizmeti raporları; dosya adları, şifreleme karması, satıcı, boyut ve tarih damgaları gibi olası kötü amaçlı yazılım dosyaları hakkında bilgiler içerir. Ayrıca, Microsoft Bulut koruma hizmeti dosyanın kaynağını göstermek için tam URL 'Ler toplayabilir. Bu URL 'Ler bazen, arama terimleri veya formlara girilen veriler gibi kişisel bilgiler içerebilir. Raporlar, istenmeyen yazılımlar hakkında Endpoint Protection size bildirimde bulunduğunda aldığınız eylemleri de içerebilir. Microsoft Bulut koruma hizmeti raporları, Microsoft 'un kötü amaçlı yazılım ve istenmeyebilecek yazılımları algılama ve kaldırma ve yeni kötü amaçlı yazılımı belirlemeyi deneme Endpoint Protection ölçmesine yardımcı olmak için bu bilgileri içerir.

Temel veya gelişmiş üyeliğiniz varsa, Microsoft Bulut koruma hizmetine katabilirsiniz. Temel üye raporlarında daha önce açıklanan bilgiler vardır. Gelişmiş üye raporları daha kapsamlıdır ve Endpoint Protection algıladığı yazılım hakkında, bu yazılımın konumu, dosya adları, yazılımın nasıl çalıştığı ve bilgisayarınızı nasıl etkilediği gibi ek ayrıntılar içerebilir. Microsoft Bulut koruma hizmeti 'ne katılan diğer Endpoint Protection kullanıcılar Microsoft araştırmacılarının yeni tehditleri daha hızlı bulmasına yardımcı olan bu raporlar ve raporlar. Daha sonra analiz ölçütlerine uyan programlar için kötü amaçlı yazılım tanımları oluşturulur ve güncelleştirilmiş tanımlar Microsoft Update aracılığıyla tüm kullanıcılar için kullanılabilir hale getirilir.

Bazı kötü amaçlı yazılım bulaşmalarını algılamaya ve gidermeye yardımcı olmak için, ürün düzenli olarak BILGISAYARıNıZıN güvenlik durumu hakkında Microsoft Bulut koruma hizmeti bilgileri gönderir. Bu bilgiler bilgisayarınızın güvenlik ayarları ve BILGISAYARıNıZ önyükleme sırasında yüklenen sürücüleri ve diğer yazılımları tanımlayan günlük dosyalarıyla ilgili bilgileri içerir.

BILGISAYARıNıZı benzersiz bir şekilde tanımlayan bir sayı de gönderilir. Ayrıca, Microsoft Bulut koruma hizmeti potansiyel kötü amaçlı yazılım dosyalarının bağlanacağı IP adreslerini toplayabilir.

Microsoft Bulut koruma hizmeti raporları, Microsoft yazılım ve hizmetlerini geliştirmek için kullanılır. Raporlar ayrıca istatistiksel veya diğer test ya da analitik amaçlar için ve tanımlar oluşturmak için de kullanılabilir. Yalnızca raporları kullanması gereken Microsoft çalışanları, yüklenicileri, iş ortakları ve satıcıları bunlara erişebilir.

Microsoft Bulut koruma hizmeti kasıtlı olarak kişisel bilgi toplamaz. Microsoft Bulut koruma hizmeti 'nin herhangi bir kişisel bilgi topladığı ölçüde, Microsoft bu bilgileri kimliğinizi belirlemek veya sizinle iletişim kurmak için kullanmaz.

Daha fazla bilgi için bkz. [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Site Hiyerarşisi – Bing Haritalar ile Coğrafi Görünüm

Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **site hiyerarşisi** düğümünü seçin ve **coğrafi görünüme**geçin. Bu görünüm, Microsoft Bing Haritalar 'ın Configuration Manager fiziksel sunucu topolojinizi görüntülemek için sağladığı haritaları kullanmanıza olanak sağlar. Bu özelliği etkinleştirmek için sağladığınız konum bilgileri, sunucunuzdaki Bing Haritalar Web hizmetine gönderilir.

Microsoft bu bilgileri Microsoft Bing Haritalar'ı ve diğer Microsoft siteleri ve hizmetlerini işletmek ve geliştirmek için kullanır. Daha fazla bilgi için bkz. [Microsoft gizlilik bildirimi](https://go.microsoft.com/fwlink/?LinkId=823548).

Site Hiyerarşisi'nden Coğrafi Görünüm'ü kullanmamayı seçebilirsiniz. Varsayılan hiyerarşi Diyagramı görünümü hiyerarşiyi görmenizi sağlar ve Bing Haritalar hizmetini kullanmaz.
