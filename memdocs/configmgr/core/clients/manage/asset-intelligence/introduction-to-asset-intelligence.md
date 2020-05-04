---
title: Varlık yönetim bilgileri tanıtımı
titleSuffix: Configuration Manager
description: Kuruluşunuzun tamamında yazılım lisansı kullanımını envantere almak ve yönetmek için Configuration Manager varlık yönetim bilgilerini kullanın.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714188"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Configuration Manager varlık yönetim bilgilerine giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Varlık yönetim bilgileri kataloğunu kullanarak kuruluşunuz genelinde yazılım lisansı kullanımını envanterini ve yönetin. Varlık yönetim bilgileri, Configuration Manager topladığı bilgilerin kapsamını geliştirmek için donanım envanteri sınıfları ekler. Bu bilgiler, ortamınızda kullanılan donanım ve yazılım başlıklarını içerir. 60 ' den fazla rapor, bu bilgileri kullanımı kolay bir biçimde sunar. Bu raporların çoğu, daha belirli raporlara bağlanır. Genel bilgiler için sorgu yapın ve daha ayrıntılı bilgi için ayrıntıya gidin. 

Varlık yönetim bilgileri kataloğuna özel bilgi ekleyin. Örneğin, özel yazılım kategorileri, yazılım aileleri, yazılım etiketleri ve donanım gereksinimleri. Varlık yönetim bilgileri kataloğunu kullanılabilir en güncel bilgilerle dinamik olarak güncelleştirmek için Microsoft Bulut bağlayın. 

Kurumsal yazılım lisansı kullanımınızı mutabık hale getirmek için varlık yönetim bilgilerini kullanın. Yazılım lisansı bilgilerini Configuration Manager site veritabanına aktararak yazılımın hangi yazılımda kullanıldığını görüntüleyin.  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a>Varlık yönetim bilgileri kataloğu  

Varlık yönetim bilgileri Kataloğu, site veritabanında depolanan bir veritabanı tabloları kümesidir. Bu tablolar, 300.000 üzerinde yazılım başlığı ve sürümü için kategori ve tanımlama bilgilerini içerir. Ayrıca, belirli yazılım başlıkları için donanım gereksinimlerinin yönetilmesine de yardımcı olur.  

Varlık yönetim bilgileri, Microsoft ve Microsoft dışı yazılımların her ikisi de kullanılmakta olan yazılım başlıkları için yazılım lisans bilgileri sağlar. Yazılım başlıkları için önceden tanımlanmış bir donanım gereksinimleri kümesi varlık yönetim bilgileri kataloğunda mevcuttur ve özel gereksinimleri karşılamak için Kullanıcı tanımlı yeni donanım gereksinimi bilgileri oluşturabilirsiniz. Varlık yönetim bilgileri kataloğundaki bilgileri de özelleştirebilir ve kategori için Microsoft bulutuna yazılım başlığı bilgilerini yükleyebilirsiniz.  

Yeni yayımlanmış yazılımları içeren varlık yönetim bilgileri Kataloğu güncelleştirmeleri toplu Katalog güncelleştirmeleri gerçekleştirmek için düzenli aralıklarla indirilebilir. Varlık yönetim bilgileri eşitleme noktası kullanılarak da dinamik olarak güncelleştirilir.  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Yazılım kategorileri  

Varlık yönetim bilgileri yazılım kategorileri, envantere kaydedilmiş yazılım başlıklarını ve daha belirli yazılım ailelerinin üst düzey gruplamalarını büyük ölçüde kategorilere ayırmak için kullanılır. Örneğin, bir yazılım kategorisi enerji şirketleri olabilir ve bu yazılım kategorisindeki bir yazılım ailesi petrol ve gaz veya hidroelektrik olabilir. Varlık yönetim bilgileri kataloğunda çok sayıda yazılım kategorisi önceden tanımlanmıştır. Envantere kaydedilmiş yazılımları ayrıca tanımlamak için Kullanıcı tanımlı kategoriler de oluşturabilirsiniz. Önceden tanımlanmış tüm yazılım kategorilerinin doğrulama durumu her zaman **onaylanır**. Varlık yönetim bilgileri kataloğuna eklenen özel yazılım kategorisi bilgileri **Kullanıcı tanımlı**' dır. 

Yazılım kategorilerinin nasıl yönetileceği hakkında daha fazla bilgi için bkz. [varlık yönetim bilgilerini yapılandırma](configuring-asset-intelligence.md).  

> [!NOTE]  
> Varlık yönetim bilgileri kataloğunda depolanan önceden tanımlanmış yazılım kategorisi bilgileri salt okunurdur. Değiştiremez veya silemezsiniz. Yönetici kullanıcılar kullanıcı tanımlı yazılım kategorilerini ekleyebilir, değiştirebilir veya silebilir.  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a>Yazılım aileleri  

Varlık yönetim bilgileri yazılım aileleri, yazılım kategorileri içinde envantere kaydedilmiş yazılım başlıklarını tanımlamak için kullanılır. Varlık yönetim bilgileri kataloğunda çok sayıda yazılım ailesi önceden tanımlanmıştır. Envantere kaydedilmiş yazılımları ayrıca tanımlamak için Kullanıcı tanımlı kategoriler de oluşturabilirsiniz. Önceden tanımlanmış tüm yazılım aileleri için doğrulama durumu her zaman **onaylanır**. Varlık yönetim bilgileri kataloğuna eklenen özel yazılım ailesi bilgileri **Kullanıcı tanımlı**' dır. 

Yazılım ailelerini yönetme hakkında daha fazla bilgi için bkz. [varlık yönetim bilgilerini yapılandırma](configuring-asset-intelligence.md).  

> [!NOTE]  
> Önceden tanımlanmış yazılım ailesi bilgileri salt okunurdur ve değiştirilemez. Yönetici kullanıcılar kullanıcı tanımlı yazılım ailelerini ekleyebilir, değiştirebilir veya silebilir.  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a> Yazılım etiketleri  

Varlık yönetim bilgileri özel yazılım etiketleri, yazılım başlıklarını gruplamak ve varlık yönetim bilgileri raporlarında görüntülemek için filtreler oluşturmanızı sağlar. Ortak bir özniteliği paylaşan Kullanıcı tanımlı yazılım başlığı grupları oluşturmak için yazılım etiketlerini kullanın. Örneğin, paylaşılan yazılım adlı bir yazılım etiketi oluşturabilir, bunu envantere kaydedilmiş paylaşılan yazılım başlıklarıyla ilişkilendirebilir ve bu etikete sahip tüm yazılım başlıklarını göstermek için bir rapor çalıştırabilirsiniz. Önceden tanımlanmış etiket yok. Yazılım etiketleri için doğrulama durumu her zaman **Kullanıcı Tanımlı**’dır. 

Yazılım etiketlerinin nasıl yönetileceği hakkında daha fazla bilgi için bkz. [varlık yönetim bilgilerini yapılandırma](configuring-asset-intelligence.md).  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a>Donanım gereksinimleri  

Bilgisayarların yazılım dağıtımları için hedeflenmeden önce yazılım başlıkları için donanım gereksinimlerini karşıladığını doğrulamak üzere donanım gereksinimleri bilgilerini kullanın. **Varlık yönetim bilgileri** düğümünün altındaki **donanım gereksinimleri** düğümündeki **varlıklar ve uyum** çalışma alanında bulunan yazılım başlıkları için donanım gereksinimlerini yönetin. 

Varlık yönetim bilgileri kataloğunda birçok donanım gereksinimi önceden tanımlanmıştır. Özel gereksinimleri karşılamak için Kullanıcı tanımlı yeni donanım gereksinimi bilgileri oluşturun. Önceden tanımlanmış tüm donanım gereksinimleri için doğrulama durumu her zaman **onaylanır**. Varlık yönetim bilgileri kataloğuna eklenen Kullanıcı tanımlı donanım gereksinimleri bilgileri **Kullanıcı tanımlı**' dır. 

Donanım gereksinimlerinin nasıl yönetileceği hakkında daha fazla bilgi için bkz. [varlık yönetim bilgilerini yapılandırma](configuring-asset-intelligence.md).  

> [!NOTE]  
> Configuration Manager konsolunda görüntülenen donanım gereksinimleri varlık yönetim bilgileri kataloğundan alınır. İstemcilerden envantere kaydedilmiş yazılım başlığı bilgilerini temel almayan değildir. 
> 
> Donanım gereksinimi bilgileri Microsoft ile eşitleme işleminin bir parçası olarak güncellenmez. 
> 
> İlişkili donanım gereksinimleri olmayan envantere kaydedilmiş yazılımlar için Kullanıcı tanımlı donanım gereksinimleri oluşturabilirsiniz.  

Varsayılan olarak, listelenen her donanım gereksinimi için aşağıdaki bilgiler görüntülenir:  

- **Yazılım başlığı**: donanım gereksinimiyle ilişkili yazılım başlığı  

- **MINIMUM CPU (MHz)**: yazılım başlığı için gereken en düşük işlemci hızı megahertz (MHz)  

- **En az RAM (KB)**: yazılım başlığı için gereken en düşük RAM (KB)  

- **En az disk alanı (KB)**: yazılım başlığı için gereken minimum boş sabit disk alanı (KB)  

- **En az disk boyutu (KB)**: yazılım başlığı için gereken minimum sabit disk boyutu (KB)  

- **Doğrulama durumu**: donanım gereksinimi için doğrulama durumu  

Varlık yönetim bilgileri kataloğunda depolanan önceden tanımlanmış donanım gereksinimleri salt okunurdur ve silinemez. Yönetici kullanıcılar varlık yönetim bilgileri kataloğunda depolanmayan yazılım başlıkları için Kullanıcı tanımlı donanım gereksinimlerini ekleyebilir, değiştirebilir veya silebilir.  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a> Envantere kaydedilmiş yazılım başlıkları  

Configuration Manager konsolundaki envantere kaydedilmiş yazılım başlığı bilgilerini görüntülemek için **varlıklar ve uyum** çalışma alanına gidin, **varlık yönetim bilgileri** düğümünü genişletin ve **Envantere kaydedilen yazılım** düğümünü seçin. Donanım envanteri Aracısı, varlık yönetim bilgileri kataloğunda depolanan yazılım başlıklarını temel alarak Configuration Manager istemcilerinden alınan envantere kaydedilmiş yazılım bilgilerini toplar.  

> [!Note]  
> Donanım envanteri Aracısı, etkinleştirdiğiniz varlık yönetim bilgileri donanım envanteri raporlama sınıflarını temel alarak envanteri toplar. Raporlama sınıflarının nasıl etkinleştirileceği hakkında daha fazla bilgi için bkz. [varlık yönetim bilgilerini yapılandırma](configuring-asset-intelligence.md).  

Varsayılan olarak, envantere kaydedilen her yazılım başlığı için aşağıdaki bilgiler görüntülenir:  

- **Ad**: Envantere kaydedilen yazılım başlığının adı  

- **Satıcı**: Envantere kaydedilen yazılım başlığını geliştiren satıcının adı  

- **Sürüm**: Envantere kaydedilen yazılım başlığının ürün sürümü  

- **Kategori**: Envantere kaydedilen yazılım başlığına Şu anda atanmış olan yazılım kategorisi  

- **Aile**: Envantere kaydedilen yazılım başlığına Şu anda atanmış olan yazılım ailesi  

- **Etiket** [**1**, **2**ve **3**]: yazılım başlığıyla ilişkili özel etiketler. Envantere kaydedilmiş yazılım başlıklarıyla ilişkili en fazla üç özel etiket olabilir.  

- **Sayı**: yazılım başlığına envantere kaydedilmiş Configuration Manager istemci sayısı  

- **Durum**: Envantere kaydedilen yazılım başlığının doğrulama durumu  

> [!NOTE]  
> Envantere kaydedilen yazılım için kategori bilgilerini yalnızca hiyerarşinizdeki en üst düzey sitede değiştirebilirsiniz. Bu bilgiler ürün adı, satıcı, yazılım kategorisi ve yazılım ailesini içerir. Önceden tanımlanmış yazılım kategorisi bilgilerini değiştirdikten sonra, yazılım değişiklikleri için doğrulama durumu **Doğrulanmış** ’tan **Kullanıcı Tanımlı**’ya değişir.  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a>Varlık yönetim bilgileri eşitleme noktası  

Varlık yönetim bilgileri eşitleme noktası Configuration Manager bir site sistemi rolüdür. Dinamik Katalog bilgileri güncelleştirmelerini yönetmek için 443 numaralı TCP bağlantı noktasında Microsoft bulutuna bağlanmak üzere kullanılır. Bu site rolünü yalnızca hiyerarşinin en üst düzey sitesine yükler. En üst düzey siteye bağlı bir Configuration Manager konsolu kullanarak tüm varlık yönetim bilgileri Kataloğu özelleştirmesini yapılandırın. 

Üst düzey sitede tüm güncelleştirmeleri yapılandırırken, Katalog bilgileri hiyerarşideki diğer sitelere çoğaltılır. Site rolü, Microsoft ile isteğe bağlı katalog eşitleme isteğinde bulunan veya otomatik katalog eşitlemesini zamanlamanıza olanak sağlar. Varlık yönetim bilgileri eşitleme noktası, yeni katalog bilgilerini indirmeye ek olarak özel yazılım başlığı bilgilerini kategorilere ayırmak üzere Microsoft 'a yükleyebilir. Microsoft, karşıya yüklenen tüm yazılım başlıklarını genel bilgi olarak değerlendirir. Özel yazılım başlıklarınızın gizli veya özel bilgiler içerdiğinden emin olun.  

Kategorilere ayrılmamış bir yazılım başlığı gönderdikten sonra, Microsoft, aynı yazılım başlığı için müşterilerden en az dört sınıflandırma isteği bulunana kadar bunu gözden geçirmez. Sonra, Microsoft araştırmacıları, yazılım başlığı kategori bilgilerini, çevrimiçi hizmeti kullanan tüm müşteriler için kullanılabilir hale getirir, kategorilere atar ve belirler. En çok kategorilere ayırma isteğini temsil eden yazılım başlıkları, kategorilere ayrılmak için en yüksek önceliğe sahiptir. Özel yazılım ve iş kolu uygulamalarının bir kategori alması çok düşüktür. Bu yazılım başlıklarını kategorilere ayırmak için Microsoft 'a göndermeyin.  

Microsoft bulutuna bağlanmak için varlık yönetim bilgileri eşitleme noktası gereklidir. Rolü nasıl yükleyeceğiniz hakkında bilgi için bkz. [varlık yönetim bilgilerini yapılandırma](configuring-asset-intelligence.md).  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a>Varlık yönetim bilgileri giriş sayfası  

**Varlıklar ve uyum** çalışma alanındaki **Varlık Yönetim Bilgileri** düğümü, Configuration Manager varlık yönetim bilgileri için giriş sayfasıdır. Bu giriş sayfasında varlık yönetim bilgileri Kataloğu bilgileri için bir Özet pano görünümü görüntülenir.  

> [!NOTE]  
> **Varlık yönetim bilgileri** giriş sayfası görüntülenirken otomatik olarak güncelleştirmez.  

**Varlık yönetim bilgileri** giriş sayfası aşağıdaki bölümleri içerir:  

- **Katalog eşitleme**: varlık yönetim bilgilerinin etkin olup olmadığı ve varlık yönetim bilgileri eşitleme noktasının geçerli durumu hakkında bilgiler.  

    > [!NOTE]  
    > Giriş sayfası yalnızca bir varlık yönetim bilgileri eşitleme noktası yüklediğinizde bu bölümü görüntüler.  

    Bu bölüm ayrıca aşağıdaki bilgileri sağlar:  

    - Eşitleme zamanlaması  

    - Bir müşteri lisans beyanı içeri aktardıysanız   

    - Son durum güncelleştirmesi  

    - Zamanlanan bir sonraki güncelleştirmenin saati  

    - Varlık yönetim bilgileri eşitleme noktasını yükledikten sonraki değişiklik sayısı   

- **Envantere kaydedilmiş yazılım durumu**: Microsoft tarafından tanımlanan, bir yönetici tarafından tanımlanan, çevrimiçi olarak tanımlanmayı bekleyen veya tanımlanmamış ve beklemede olmayan, envantere kaydedilmiş yazılımların, yazılım kategorilerinin ve yazılım ailelerinin sayısı ve yüzdesi. Tablo biçiminde gösterilen bilgiler her biri için sayıyı gösterirken, grafikte görüntülenen bilgilerde her biri için yüzde gösterilir.  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a>Varlık yönetim bilgileri raporları  

Varlık yönetim bilgileri raporları Configuration Manager konsolunda, **izleme** çalışma alanında, **Raporlama** düğümü altındaki **varlık yönetim bilgileri** klasöründe bulunur. Raporlar donanım, lisans yönetimi ve yazılım hakkında bilgi sağlar. Configuration Manager raporları hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
> Varlık yönetim bilgileri raporlarında görüntülenen yüklü yazılım başlığı miktarının ve lisans bilgilerinin doğruluğu, yüklü olan yazılım başlığı veya ortamda kullanılan lisans sayısından farklı olabilir. Bu farklılığın nedeni, kurumsal ortamlarda yüklenen yazılım başlıkları için yazılım lisansı bilgilerinin envanterinin oluşturulmasıyla ilgili karmaşık bağımlılıkların ve sınırlamaların olmasıdır. Satın alınan yazılım lisansı uyumluluğunu belirlemek için varlık yönetim bilgileri raporlarını tek kaynak olarak kullanmayın.  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a>Donanım raporları  

Varlık yönetim bilgileri donanım raporları kuruluştaki donanım varlıkları hakkında bilgiler sağlar. Hız, bellek ve çevre birimi cihazları gibi donanım envanteri bilgilerini kullanarak, varlık yönetim bilgileri donanım raporları, USB cihazlar, yükseltilmesi gereken donanım ve hatta belirli bir yazılım yükseltmesi için hazır olmayan bilgisayarlar hakkında bilgi sunabilir.  

> [!NOTE]  
> Varlık yönetim bilgileri donanım raporlarındaki bazı Kullanıcı verileri Windows Güvenliği olay günlüğü 'nden toplanır. Daha iyi rapor doğruluğu için, bir bilgisayarı yeni bir kullanıcıya atadığınızda bu günlüğü temizleyin.  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a>Lisans Yönetimi raporları  

Varlık yönetim bilgileri lisans yönetimi raporları, kullanılmakta olan lisanslar hakkında veriler sağlar. **Lisans defteri** raporu, yüklü Microsoft uygulamalarını bir Microsoft Lisans bildirimiyle (MLS) bir biçimde listeler. Bu biçim, kullanılan lisanslarla alınan lisansları eşleştirmek için kullanışlı bir yöntem sağlar. Diğer lisans yönetimi raporları, Windows etkinleştirme istatistikleri için anahtar yönetimi hizmeti 'ni (KMS) çalıştıran sunucular olarak davranan bilgisayarlar hakkında bilgi sağlar.  

> [!IMPORTANT]  
> Bazı varlık yönetim bilgileri lisans yönetimi raporları, toplu lisanslamayı yönetme yöntemi olan KMS işlevi hakkında bilgi sunar. KMS sunucusu uygulamadıysanız, bazı raporlar herhangi bir veri döndürmeyebilir.  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a>Yazılım raporları  

Varlık yönetim bilgileri yazılım raporları, kuruluştaki bilgisayarlarda yüklü yazılım aileleri, Kategoriler ve belirli yazılım başlıkları hakkında bilgiler sağlar. Yazılım raporları, tarayıcı yardımcısı nesneleri ve otomatik olarak başlayan yazılımlar gibi bilgileri sunar. Bu raporlar, reklam yazılımlarını, casus yazılımları ve diğer kötü amaçlı yazılımları belirlemek için kullanılabilir. Ayrıca, yazılım alımı ve desteğini kolaylaştırmaya yardımcı olmak üzere yazılım artıklığını belirlemek için de kullanabilirsiniz.  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a>Yazılım tanımlama etiketi raporları  

Varlık yönetim bilgileri yazılım tanımlama etiketi raporları, ISO/ıEC 19770-2 ile uyumlu bir yazılım tanımlama etiketi içeren yazılımlar hakkında bilgiler sağlar. Yazılım tanımlama etiketleri, yüklü yazılımları tanımlamak için kullanılan yetkili bilgileri sağlar. **SMS_SoftwareTag** donanım envanteri raporlama sınıfını etkinleştirdiğinizde, Configuration Manager yazılım tanımlama etiketleriyle yazılım hakkında bilgi toplar. 

Aşağıdaki raporlar yazılımlar hakkında bilgi sağlar:  

- **Yazılım 14A-yazılım kimliği etiketi etkinleştirilmiş yazılımları arama**: yazılım kimliği etiketi etkin yüklü yazılım sayısı  

- **Yazılım 14B-Belirli bir yazılım kimliği etiketi etkinleştirilmiş yazılımların yüklü olduğu bilgisayarlar**: belirli bir yazılım kimliği etiketi etkin yüklü yazılıma sahip bilgisayarlar  

- **Yazılım 14C-belirli bir bilgisayarda yüklü yazılım kimliği etiketi etkin yazılım**: belirli bir bilgisayarda belirli bir yazılım kimliği etiketi etkinleştirilmiş olan tüm yüklü yazılımlar  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a>Raporlama sınırlamaları  

Varlık yönetim bilgileri raporları, yüklü yazılım başlıkları ve kullanılmakta olan yazılım lisansları hakkında büyük miktarlarda bilgi sağlayabilir. Bu bilgileri, alınan yazılım lisansı uyumluluğunu belirlemek için tek kaynak olarak kullanmayın.  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Örnek bağımlılıklar  
Varlık yönetim bilgileri raporlarında yüklü yazılım başlıkları ve lisans bilgileri için görüntülenen miktarın doğruluğu, şu anda kullanılan gerçek miktarlardan farklı olabilir. Bu farklılığın nedeni, kurumsal ortamlarda kullanılan yazılım başlıkları için yazılım lisansı bilgilerinin envanterinin oluşturulmasıyla ilgili karmaşık bağımlılıkların olmasıdır. Aşağıdaki örnekler, varlık yönetim bilgileri raporlarının doğruluğunu etkileyebilecek varlık yönetim bilgileri 'ni kullanarak kuruluştaki yüklü yazılımlar hakkında bilgi sahibi olan bağımlılıkları göstermektedir:  

- **İstemci donanım envanteri bağımlılıkları**: varlık yönetim bilgileri yüklü yazılım raporları, varlık yönetim bilgileri raporlamasını etkinleştirmek için donanım envanterini genişleterek Configuration Manager istemcilerinden toplanan verileri temel alır. Donanım envanteri raporlamaya bu bağımlılık nedeniyle, varlık yönetim bilgileri raporları yalnızca gerekli varlık yönetim bilgileri WMI raporlama sınıfları etkin olan donanım envanteri süreçlerini başarıyla tamamlayacak istemcilerden verileri yansıtır. Configuration Manager istemcileri, yönetici kullanıcı tarafından tanımlanan bir zamanlamaya göre donanım envanteri işlemleri gerçekleştirdiğinden, veri raporlamada varlık yönetim bilgileri raporlarının doğruluğunu etkileyen bir gecikme meydana gelebilir. 

    Örneğin, istemci başarılı bir donanım envanteri döngüsünü tamamlandıktan sonra envantere kaydedilmiş lisanslı bir yazılım başlığı kaldırılabilir. Varlık yönetim bilgileri raporları, istemci bir sonraki zamanlanmış donanım envanteri raporlama döngüsüne kadar yazılım başlığını yüklendi olarak görüntüler.  

- **Yazılım paketleme bağımlılıkları**: varlık yönetim bilgileri raporları, standart Configuration Manager istemci donanım envanteri süreçlerini kullanarak toplanan yüklü yazılım başlığı verilerini temel alır. Bazı yazılım başlığı verileri doğru toplanmayabilir. Yanlış varlık yönetim bilgileri raporlamaya neden olabilecek örnekler:  

    - Standart yükleme işlemleriyle uyumlu olmayan yazılım yüklemeleri  

    - Yüklemeden önce değiştirilen yazılım yüklemeleri   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Yasal sınırlamalar  
Varlık yönetim bilgileri raporlarında görünen bilgiler birçok sınırlamalara tabidir. Bunlar içinde görünen bilgiler yasal, muhasebe veya diğer profesyonel önerileri temsil etmez. Varlık yönetim bilgileri raporları tarafından sunulan bilgiler yalnızca bilgi amaçlıdır. Yazılım Lisansı kullanım uyumluluğunu belirlemek için tek bilgi kaynağı olarak kullanmayın.  

Aşağıdaki sınırlamalar, raporların doğruluğunu etkileyebilecek varlık yönetim bilgileri kullanmanın örnekleridir:  

- **Microsoft lisans kullanım miktarı sınırlamaları**:  

    - Satın alınan Microsoft yazılım lisansı miktarı, yöneticilerin tedarik ettiği bilgileri temel alır. Doğru yazılım lisansı sayısının sağlandığından emin olmak için bunu yakından gözden geçirin.  

    - Bildirilen Microsoft yazılım lisansı sayısı, yalnızca toplu lisanslama programları aracılığıyla edinilen Microsoft yazılım lisansları hakkında bilgiler içerir. Perakende, OEM veya diğer yazılım lisansı satış kanalları aracılığıyla edinilen yazılım lisansları için bilgileri yansıtmaz.  

    - Son 45 gün içinde alınan yazılım lisansları, yazılım satıcılarının raporlama gereksinimleri ve zamanlamaları nedeniyle, raporlanan Microsoft yazılım lisansı miktarına eklenmemiş olabilir.  

    - Şirket birleşmeleri veya satın almalarıyla gerçekleşen yazılım lisansı aktarımları Microsoft yazılım lisansı miktarlarında yansıtılmayabilir.  

    - Bir Microsoft Toplu Lisanslama (MVLS) anlaşmasındaki standart olmayan hüküm ve koşullar, raporlanan yazılım lisansı sayısını etkileyebilir. Microsoft temsilcisiyle daha fazla gözden geçirilmesi gerekebilir.  

- **Yüklü yazılım başlığı miktar sınırlamaları**: Configuration Manager istemcilerin, varlık yönetim bilgileri raporlarının yüklü yazılım başlıklarının miktarını doğru şekilde raporlamaları için donanım envanteri raporlama döngülerini başarıyla tamamlaması gerekir. Başarılı bir donanım envanteri raporlama döngüsünden sonra lisanslı bir yazılım başlığının yüklenmesi veya kaldırılması arasında bir gecikme olabilir. Bu eylem, istemci bir sonraki zamanlanmış donanım envanterini raporladığı için varlık yönetim bilgileri raporları ' na yansıtılmayabilir.  

- **Lisans mutabakat sınırlamaları**: yüklü yazılım başlığı miktarının alınan yazılım lisanslarının miktarına göre mutabakatı, yönetici tarafından belirtilen lisans miktarının ve yönetici tarafından ayarlanan zamanlamaya göre Configuration Manager istemci donanım envanterlerinden toplanan yüklü yazılım başlıklarının miktarı kullanılarak hesaplanır. Bu karşılaştırma, lisans konumlarının son Microsoft sonucunun sonucunu göstermez. Gerçek lisans konumu, belirli yazılım başlığı lisansı ve lisans koşulları tarafından belirtilen kullanım haklarına bağlıdır.  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a>Varlık yönetim bilgileri doğrulama durumları  

Varlık yönetim bilgileri doğrulama durumları, varlık yönetim bilgileri kataloğu bilgilerinin kaynak ve geçerli doğrulama durumunu temsil eder. Aşağıdaki tabloda olası varlık yönetim bilgileri doğrulama durumları ve bunlara neden olabilecek yönetici eylemleri gösterilmektedir.  

| Durum | Tanım | Yönetici eylemi | Açıklama |  
|---------------|--------------------|------------------------------|-----------------|  
|**Doğrulanmış**|Microsoft araştırmacıları Katalog öğesi tanımladı|Hiçbiri|En iyi durum|  
|**Kullanıcı Tanımlı**|Microsoft araştırmacıları Katalog öğesi tanımlamamıştı|Yerel katalog bilgilerini özelleştirme|Bu durum varlık yönetim bilgileri raporlarında görüntülenir|  
|**Bekleniyor**|Microsoft araştırmacıları Katalog öğesi tanımlamamıştı, ancak öğeyi kategori için Microsoft 'a gönderdiniz|Kategori istenmeden sonra başka eylem yok|Katalog öğesi, Microsoft araştırmacıları öğeyi kategorilere ayırana ve varlık yönetim bilgileri kataloğunuzu eşitlene kadar bu durumda kalır|  
|**Güncelleştirilebilir**|Kullanıcı tanımlı bir katalog öğesi, Katalog eşitlemesi sırasında Microsoft tarafından farklı şekilde kategorilere ayrılmıştır.|Yeni kategori bilgilerini veya önceki Kullanıcı tanımlı değeri kullanıp kullanmayacağınızı belirlemek için **çakışmayı çöz** eylemini kullanın. Çakışmaların nasıl çözümleneceği hakkında daha fazla bilgi için bkz. [varlık yönetim bilgileri Için işlemler](operations-for-asset-intelligence.md).|Kategori çakışmasını çözdükten sonra, daha sonra kategorilere ayırma güncelleştirmeleri öğe hakkında yeni bilgi oluşturmadığı sürece öğe yeniden çakışan olarak doğrulanmaz.|  
|**Kategorilere ayrılmamış**|Katalog öğesi Microsoft araştırmacıları tarafından tanımlı değil, öğe kategorilere ayırmak için Microsoft 'a gönderilmedi ve Yönetici Kullanıcı tanımlı bir kategori değeri atamadı.|Kategori isteyin veya yerel Katalog bilgilerinizi özelleştirin. Daha fazla bilgi için bkz. [varlık yönetim bilgileri Için işlemler](operations-for-asset-intelligence.md).|Hiçbiri|  

> [!NOTE]  
> Kategorilere ayırmak için Microsoft 'a gönderdiğiniz katalog öğeleri, bir merkezi yönetim sitesinde **bekleyen** doğrulama durumuna sahiptir, ancak alt birincil sitelerde **kategorilere ayrılmamış** doğrulama durumuyla gösterilmeye devam eder.  

Bir doğrulama durumunun bir durumdan diğerine geçeceğinin örnekleri için, bkz. [varlık yönetim bilgileri Için örnek doğrulama durumu geçişleri](example-validation-state-transitions-for-asset-intelligence.md).  
