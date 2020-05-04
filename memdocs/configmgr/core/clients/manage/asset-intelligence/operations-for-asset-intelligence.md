---
title: Varlık Yönetim Bilgileri’ni kullanma
titleSuffix: Configuration Manager
description: Configuration Manager ortak Varlık Yönetim Bilgileri görevleri yapın.
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1e272e8e71ceaa15c712cb3a53d9db835747d327
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714174"
---
# <a name="how-to-use-asset-intelligence-in-configuration-manager"></a>Configuration Manager Varlık Yönetim Bilgileri kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu, Configuration Manager hiyerarşinizdeki tipik Varlık Yönetim Bilgileri görevlerini yönetmenize yardımcı olacak bilgiler içerir:  

##  <a name="view-asset-intelligence-information"></a><a name="BKMK_ViewInformation"></a> Varlık Yönetim Bilgilerini görüntüleme  
 Varlık Yönetim Bilgilerini **Varlık Yönetim Bilgileri** giriş sayfasında ve Varlık Yönetim Bilgileri raporlarında görüntüleyebilirsiniz.  

###  <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Varlık Yönetim Bilgileri giriş sayfası  
 **Varlık Yönetim Bilgileri** giriş sayfasında Varlık Yönetim Bilgileri kataloğu bilgileri için bir özet panosu gösterilir. Giriş sayfasında, katalog eşitleme ve envantere kaydedilen yazılımların durumu hakkındaki bilgileri görüntüleyebilirsiniz. **Varlık Yönetim Bilgileri** giriş sayfası aşağıdaki bölümlere ayrılmıştır:  

- **Katalog Eşitleme**: Varlık Yönetim Bilgilerinin etkin olup olmadığı, Varlık Yönetim Bilgileri eşitleme noktasının geçerli durumu, eşitleme zamanlaması, müşteri lisans beyanının içeri aktarılıp aktarılmadığı, durumun en son ne zaman güncelleştirildiği ve zamanlanan sonraki güncelleştirme ile Varlık Yönetim Bilgileri eşitleme noktası site sistemi yüklendikten sonra gerçekleşen değişikliklerin sayısı hakkında bilgiler sağlar.  

  > [!NOTE]  
  >  **Varlık Yönetim Bilgileri** giriş sayfasının Varlık Yönetim Bilgileri kataloğu eşitleme noktası bölümü, yalnızca bir Varlık Yönetim Bilgileri eşitleme noktası site sistemi rolü yüklendiyse görüntülenir.  

- **Envantere Kaydedilmiş Yazılım Durumu**: Microsoft tarafından tanımlanan, bir yönetici kullanıcı tarafından tanımlanan, çevrimiçi olarak tanımlanmayı bekleyen veya tanımlanmamış ve beklemede olmayan, envantere kaydedilmiş yazılımların, yazılım kategorilerinin ve yazılım ailelerin sayısını ve yüzdesini sağlar. Tablo biçiminde gösterilen bilgiler her biri için sayıyı gösterirken, grafikte görüntülenen bilgilerde her biri için yüzde gösterilir.  

  **Varlık Yönetim Bilgileri** giriş sayfasında Varlık Yönetim Bilgilerini görüntülemek için aşağıdaki yordamı kullanın.  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>Varlık Yönetim Bilgileri giriş sayfasında Varlık Yönetim Bilgilerini görüntülemek için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlık ve Uyumluluk** çalışma alanında **Varlık Yönetimi Bilgileri**’ne tıklayın. Varlık Yönetim Bilgileri raporları görüntülenir.  

###  <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a>Varlık Yönetim Bilgileri raporları  
 Varlık Yönetim Bilgileri tarafından toplanan bilgileri görüntüleyen 60’tan fazla Varlık Yönetim Bilgileri raporu vardır. Bu raporların çoğu, genel bilgiler için sorgulayabileceğiniz ve daha ayrıntılı bilgiler için detaya gidebileceğiniz daha özel raporlara bağlanır. Varlık Yönetim Bilgileri raporları, **izleme** çalışma alanında, **raporlama** düğümü altındaki Configuration Manager konsolunda bulunur. Raporlar donanım, lisans yönetimi ve yazılım hakkında bilgi sağlar. Configuration Manager raporları hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Varlık Yönetim Bilgileri raporlarında görüntülenen yüklü yazılım başlığı miktarları ve lisans bilgilerinin doğruluğu, kurumsal ortamlara yüklenen yazılım başlıkları için yazılım lisansı bilgilerinin envantere kaydedilmesiyle ilgili karmaşık bağımlılıklar ve sınırlamalar nedeniyle ortamla gerçekte yüklü olan yazılım başlığı veya kullanımda olan lisans sayısından farklı olabilir. Satın alınan yazılım lisansı uyumluluğunu belirlemek için Varlık Yönetim Bilgileri raporları tek kaynak olarak kullanılmamalıdır.  

 Varlık Yönetim Bilgileri raporlarını kullanarak Varlık Yönetim Bilgilerini görüntülemek için aşağıdaki yordamı kullanın.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>Varlık Yönetim Bilgileri raporlarını kullanarak Varlık Yönetim Bilgilerini görüntülemek için  

1.  Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2.  **İzleme** çalışma alanında **Raporlama**'yı genişletin, **Raporlar**'ı genişletin ve **Varlık Yönetim Bilgileri**’ne tıklayın. Varlık Yönetim Bilgileri raporları görüntülenir.  

    > [!WARNING]  
    >  **Raporlar** düğümü altında hiç rapor klasörü yoksa, raporlamayı yapılandırdığınızı doğrulayın. Daha fazla bilgi için bkz. [raporlamayı yapılandırma](../../../../core/servers/manage/configuring-reporting.md).  

3.  Çalıştırmak istediğiniz Varlık Yönetim Bilgileri raporunu seçin ve daha sonra **Giriş** sekmesinin **Rapor Grubu** grubunda **Çalıştır**'a tıklayın.  

##  <a name="synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_SynchronizeTheCatalog"></a>Varlık Yönetim Bilgileri kataloğunu eşitler  
 En yeni yazılım başlığı kategorilerini almak için Varlık Yönetim Bilgileri kataloğunu System Center Online ile eşitleyebilirsiniz. System Center Online ile elle katalog eşitlemesi istediğinizde, System Center Online ile eşitleme işleminin tamamlanması 15 dakika veya daha uzun sürebilir. Configuration Manager, **varlık yönetim bilgileri** giriş sayfasındaki **son başarılı güncelleştirme** ayarını eşitlemenin başarıyla bittiği saat ile güncelleştirir.  

> [!NOTE]  
>  Daha önceden yordamlar kullanılarak bir Varlık Yönetim Bilgileri eşitleme noktası site sistemi rolünün yüklenmesi gerekir. Varlık Yönetim Bilgileri eşitleme noktası yükleme hakkında daha fazla bilgi için bkz. [varlık yönetim bilgileri yapılandırma](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Varlık Yönetim Bilgileri kataloğuna yönelik bir eşitleme zamanlaması oluşturmak için aşağıdaki yordamı kullanın.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>Varlık Yönetim Bilgileri kataloğuna yönelik bir eşitleme zamanlaması oluşturmak için  

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2. **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne tıklayın.  

3. **Giriş** sekmesinde, **Oluştur** grubunda, **Eşitle**’ye tıklayın ve ardından **Eşitleme Zamanla**’ya tıklayın.  

4. **Varlık Yönetim Bilgileri Eşitleme Noktası Zamanlama** iletişim kutusunda, **Bir zamanlamaya göre eşitlemeyi etkinleştir**’i seçin ve ardından basit veya özel bir zamanlama yapılandırın.  

5. Değişiklikleri kaydetmek için **Tamam**’a tıklayın.  

   > [!NOTE]  
   >  Sonraki zamanlanmış eşitleme dahil, eşitleme zamanlaması hakkında daha fazla bilgi için hiyerarşideki en üst düzey sitenin **Varlıklar ve Uyumluluk** çalışma alanındaki **Varlık Yönetim Bilgileri** düğümüne bakın.  

   Varlık Yönetim Bilgileri kataloğunu elle eşitlemek için aşağıdaki yordamı kullanın.  

> [!WARNING]  
>  System Center Online, 12 saatlik bir dönemde yalnızca bir elle eşitleme isteği kabul eder.  

###  <a name="to-manually-synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_ManuallySynchronizeCatalog"></a> Varlık Yönetim Bilgileri kataloğunu elle eşitlemek için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne tıklayın.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **Eşitle**’ye tıklayın, **Varlık Yönetim Bilgileri Kataloğunu Eşitle**’ye tıklayın ve ardından **Tamam**’a tıklayın.  

##  <a name="customize-the-asset-intelligence-catalog"></a><a name="BKMK_CustomizeCatalog"></a> Varlık Yönetim Bilgileri kataloğunu özelleştirme  
 System Center Online’dan alınan Varlık Yönetim Bilgileri kataloğu kategori bilgileri site veritabanında salt okunur izinlerle depolanır ve değiştirilemez veya silinemez. Ancak, özel yazılım kategorileri, yazılım aileleri, yazılım etiketleri ve donanım gereksinimleri katalog bilgilerini oluşturabilir, düzenleyebilir ve silebilirsiniz. Daha sonra mevcut veya kullanıcı tanımlı yazılım başlığı bilgileri için System Center Online tarafından sağlanan bilgiler yerine özel kategori verilerini kullanabilirsiniz. Kategori bilgilerini değiştirdiğinizde veya bilgi eklediğinizde, katalog bilgileri kullanıcı tanımlı olarak kabul edilir. Kullanıcı tanımlı kategori bilgileri doğrulanmış katalog bilgilerinden farklı veritabanı tablolarında depolanır.  

###  <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Yazılım kategorileri  
 Varlık Yönetim Bilgileri yazılım kategorileri, envantere kaydedilmiş yazılım başlıklarını geniş kategorilere ayırmak için ve ayrıca daha belirli yazılım ailelerinin üst düzey gruplandırması olarak da kullanılır. Örneğin, bir yazılım kategorisi enerji şirketleri olabilir ve bu yazılım kategorisindeki bir yazılım ailesi petrol ve gaz veya hidroelektrik olabilir. Varlık Yönetim Bilgileri kataloğunda çok sayıda yazılım kategorisi önceden tanımlanmıştır. Envantere kaydedilmiş yazılımları daha ayrıntılı bir şekilde tanımlamak için ek kullanıcı tanımlı kategoriler de oluşturulabilir. Önceden tanımlanmış tüm yazılım kategorileri için doğrulama durumu her zaman **Doğrulanmış**’tır. Varlık Yönetim Bilgileri kataloğuna eklenen özel yazılım kategorisi bilgileriyse **Kullanıcı Tanımlı**’dır.  

 Kullanıcı tanımlı bir yazılım kategorisi oluşturmak için aşağıdaki yordamı kullanın.  

##### <a name="to-create-a-user-defined-software-category"></a>Kullanıcı tanımlı bir yazılım kategorisi oluşturmak için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne ve ardından **Katalog**’a tıklayın.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **Yazılım Kategorisi Oluştur**'a tıklayın.  

4.  **Genel** sayfasında, yeni yazılım kategorisi için bir ad ve isteğe bağlı olarak bir açıklama girin.  

    > [!NOTE]  
    >  Tüm yeni özel yazılım kategorileri için doğrulama durumu her zaman **Kullanıcı Tanımlı**olarak ayarlanmıştır.  

     **İleri**’ye tıklayın.  

5.  **Özet** sayfasında, ayarları gözden geçirin ve **İleri**'ye tıklayın.  

6.  **Tamamlanma** sayfasında, sihirbazı tamamlamak için **Kapat** 'a tıklayın.  

###  <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a>Yazılım aileleri  
 Varlık Yönetim Bilgileri yazılım aileleri, yazılım kategorileri içinde envantere kaydedilmiş yazılım başlıklarını daha ayrıntılı bir şekilde tanımlamak için kullanılır. Örneğin, bir yazılım kategorisi enerji şirketleri olabilir ve bu yazılım kategorisindeki bir yazılım ailesi petrol ve gaz veya hidroelektrik olabilir. Varlık Yönetim Bilgileri kataloğunda çok sayıda yazılım ailesi önceden tanımlanmıştır. Envantere kaydedilmiş yazılımları tanımlamak için ek kullanıcı tanımlı aileler de oluşturulabilir. Önceden tanımlanmış tüm yazılım aileleri için doğrulama durumu her zaman **Doğrulanmış**’tır. Varlık Yönetim Bilgileri kataloğuna eklenen özel yazılım ailesi bilgileriyse **Kullanıcı Tanımlı**’dır.  

 Kullanıcı tanımlı bir yazılım ailesi oluşturmak için aşağıdaki yordamı kullanın.  

##### <a name="to-create-a-user-defined-software-family"></a>Kullanıcı tanımlı bir yazılım ailesi oluşturmak için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne ve ardından **Katalog**’a tıklayın.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **Yazılım Ailesi Oluştur**'a tıklayın.  

4.  **Genel** sayfasında, yeni yazılım ailesi için bir ad ve isteğe bağlı olarak bir açıklama girin.  

    > [!NOTE]  
    >  Tüm yeni özel yazılım aileleri için doğrulama durumu her zaman **Kullanıcı Tanımlı**olarak ayarlanmıştır.  

5.  **Özet** sayfasında, ayarları gözden geçirin ve **İleri**'ye tıklayın.  

6.  **Tamamlanma** sayfasında, sihirbazı tamamlamak için **Kapat** 'a tıklayın.  

###  <a name="software-labels"></a><a name="BKMK_SoftwareLabels"></a> Yazılım etiketleri  
 Varlık Yönetim Bilgileri özel yazılım etiketleri, yazılım başlıklarını gruplamak ve Varlık Yönetim Bilgileri raporlarını kullanarak görüntülemek için kullanabileceğiniz filtreler oluşturmanızı sağlar. Örneğin, paylaşılan yazılım adlı bir yazılım etiketi oluşturup birkaç uygulamayla ilişkilendirebilir ve ardından paylaşılan yazılım yazılım etiketine sahip tüm başlıkları görüntüleyen bir rapor çalıştırabilirsiniz. Varlık Yönetim Bilgileri kataloğuna eklediğiniz tüm özel yazılım etiketleri için doğrulama durumu **Kullanıcı Tanımlı** ’dır.  

 Kullanıcı tanımlı bir özel etiket oluşturmak için aşağıdaki yordamı kullanın.  

##### <a name="to-create-a-user-defined-software-label"></a>Kullanıcı tanımlı bir yazılım etiketi oluşturmak için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne ve ardından **Katalog**’a tıklayın.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **Yazılım Etiketi Oluştur**'a tıklayın.  

4.  **Genel** sayfasında, yeni yazılım ailesi için bir ad ve isteğe bağlı olarak bir açıklama girin.  

    > [!NOTE]  
    >  Tüm yeni özel yazılım etiketleri için doğrulama durumu her zaman **Kullanıcı Tanımlı**olarak ayarlanmıştır.  

5.  **Özet** sayfasında, ayarları gözden geçirin ve **İleri**'ye tıklayın.  

6.  **Tamamlanma** sayfasında, sihirbazı tamamlamak için **Kapat** 'a tıklayın.  

###  <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a>Donanım gereksinimleri  
 Donanım gereksinimleri bilgileri, bilgisayarların yazılım dağıtımları için hedeflenmeden önce yazılım başlıkları için donanım gereksinimlerini karşıladığını doğrulamanıza yardımcı olabilir. Varlık Yönetim Bilgileri kataloğunda birçok donanım gereksinimi önceden tanımlanmıştır. Özel gereksinimlerinizi karşılamak için yeni kullanıcı tanımlı donanım gereksinimi bilgileri de oluşturabilirsiniz. Önceden tanımlanmış tüm donanım gereksinimleri için doğrulama durumu her zaman **Doğrulanmış**’tır. Varlık Yönetim Bilgileri kataloğuna eklenen kullanıcı tanımlı donanım gereksinimleri bilgileriyse **Kullanıcı Tanımlı**’dır.  

> [!IMPORTANT]  
>  Configuration Manager konsolunda görüntülenen donanım gereksinimleri yerel bilgisayardaki Varlık Yönetim Bilgileri kataloğundan alınır ve System Center 2012 Configuration Manager istemcilerinden alınan envantere kaydedilmiş yazılım başlığı bilgilerini temel alır. Donanım gereksinimleri bilgileri System Center Online ile eşitleme işleminin bir parçası olarak güncelleştirilmez. İlişkili donanım gereksinimleri olmayan envantere kaydedilmiş yazılımlar için kullanıcı tanımlı donanım gereksinimleri oluşturabilirsiniz.  

 Kullanıcı tanımlı bir donanım gereksinimi oluşturmak için aşağıdaki yordamı kullanın.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>Kullanıcı tanımlı donanım gereksinimleri oluşturmak için  

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2. **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne ve ardından **Donanım Gereksinimleri**’ne tıklayın.  

3. **Giriş** sekmesinde, **Oluştur** grubunda, **Donanım Gereksinimi Oluştur**'a tıklayın.  

4. **Genel** sayfasında aşağıdaki bilgileri belirtin:  

   1. **Yazılım başlığı**: Donanım gereksinimleriyle ilişkili yazılım başlığını belirtir. Yazılım başlığı Varlık Yönetim Bilgileri kataloğunda zaten var olamaz.  

   2. **Doğrulama durumu**: Donanım gereksinimleri için doğrulama durumunu **Kullanıcı Tanımlı** olarak listeler. Bu ayar değiştirilemez.  

   3. **Minimum CPU (MHz)**: Yazılım başlığı için gereken en düşük işlemci hızını megahertz (MHz) cinsinden belirtir.  

   4. **Minimum RAM (KB)**: Yazılım başlığı için gereken en düşük RAM’i kilobayt (KB) cinsinden belirtir.  

   5. **Minimum Disk Alanı (KB)**: Yazılım başlığı için gereken minimum boş disk alanını KB cinsinden belirtir.  

   6. **Minimum Disk Boyutu (KB)**: Yazılım başlığı için gereken minimum sabit disk boyutunu KB cinsinden belirtir.  

      **İleri**’ye tıklayın.  

5. **Özet** sayfasında, ayarları gözden geçirin ve **İleri**'ye tıklayın.  

6. **Tamamlanma** sayfasında, sihirbazı tamamlamak için **Kapat** 'a tıklayın.  

###  <a name="modify-categorization-information-for-inventoried-software"></a><a name="BKMK_ModifyCategorization"></a>Envantere kaydedilen yazılım için kategori bilgilerini değiştirme  
 Varlık Yönetim Bilgileri kataloğunda önceden tanımlanmış yazılımlar ürün adı, satıcı, yazılım kategorisi ve yazılım ailesi gibi belirli kategori bilgileri ile yapılandırılır. Önceden tanımlanan kategori bilgileri gereksinimlerinizi karşılamadığında, yazılım başlığı için özelliklerdeki bilgileri değiştirebilirsiniz. Önceden tanımlanmış yazılım kategorisi bilgileri değiştirildiğinde, yazılım değişiklikleri için doğrulama durumu **Doğrulanmış** ’tan **Kullanıcı Tanımlı**’ya değişir.  

> [!IMPORTANT]  
>  Kategori bilgileri yalnızca üst düzey sitede değiştirilebilir.  

 Envantere kaydedilen yazılım için kategori bilgilerini değiştirmek üzere aşağıdaki yordamı kullanın.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>Yazılım başlıkları kategorilerini değiştirmek için  

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2. **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne ve ardından **Envantere Kaydedilen Yazılımlar**’a tıklayın.  

3. Kategorilerini değiştirmek istediğiniz bir veya birden çok yazılım başlığını seçin.  

4. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**'e tıklayın.  

5. **Genel** sekmesinde, aşağıdaki kategorilere ayırma bilgilerini değiştirebilirsiniz:  

   -   **Ürün Adı**: Envantere kaydedilen yazılım başlığının adını belirtir.  

   -   **Satıcı**: Envantere kaydedilen yazılım başlığını geliştiren satıcı adını belirtir.  

   -   **Kategori**: Envantere kaydedilen yazılım başlığına şu anda atanmış olan yazılım kategorisini belirtir.  

   -   **Aile**: Envantere kaydedilen yazılım başlığına şu anda atanmış olan yazılım ailesini belirtir.  

6. Değişiklikleri kaydetmek için **Tamam**’a tıklayın.  

   Yazılımı özgün kategori bilgilerine döndürmek için aşağıdaki yordamı kullanın.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Yazılım için kategori bilgilerini özgün ayarlara döndürme  
 Configuration Manager, System Center Online 'dan alınan kategori bilgilerini veritabanında depolar. Bilgiler silinemez. Bilgiler değiştirildikten sonra, kategori bilgilerini System Center Online kategorilerine döndürebilirsiniz. Varlık Yönetim Bilgileri kataloğunda olmayan envantere kaydedilen yazılımlar, özgün ayarlarına döndürülebilir.  

 Yazılım kategori bilgilerini özgün ayarlarına döndürmek için aşağıdaki yordamı kullanın.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>Kategori bilgilerini özgün ayarlara döndürmek için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne ve ardından **Envantere Kaydedilen Yazılımlar**’a tıklayın.  

3.  Özgün ayarlarına döndürmek istediğiniz bir veya birden çok yazılım başlığını seçin. Yalnızca **Kullanıcı Tanımlı** durumuna sahip yazılımlar geri döndürülebilir.  

    > [!TIP]  
    >  Doğrulama durumuna göre sıralamak için **Durum** sütununa tıklayın. Sıralama, tüm yazılımları doğrulama durumlarına göre görüntülemenizi ve birden çok öğeyi özgün ayarlarına döndürmek üzere hızlı bir şekilde seçmenizi sağlar.  

4.  **Giriş** sekmesinde, **Ürün** grubunda **Döndür**'e tıklayın.  

5.  Yazılımı özgün kategori bilgilerine döndürmek için **Evet** ’e tıklayın.  

6.  Varlık Yönetim Bilgileri kataloğunda olan yazılımlar için kategori bilgilerini geri döndürdüğünüzde, doğrulama durumu **Kullanıcı Tanımlı** ’dan **Doğrulanmış**’a değiştirilir. Katalogda olmayan yazılımları geri döndürdüğünüzde, doğrulama durumu **Kullanıcı Tanımlı** ’dan **Kategorilere Ayrılmamış**’a değiştirilir.  

##  <a name="request-a-catalog-update-for-uncategorized-software-titles"></a><a name="BKMK_RequestCatalogUpdate"></a>Kategorilere ayrılmamış yazılım başlıkları için Katalog güncelleştirmesi isteme  
 Kategorilere ayrılmamış yazılım başlığı bilgileri, araştırma ve kategorilere ayırma için System Center Online’a gönderilebilir. Kategorilere ayrılmamış bir yazılım başlığı gönderildikten sonra, aynı yazılım başlığı için müşterilerden en az 4 kategorilere ayırma isteği alınırsa, araştırmacılar yazılım başlığını tanımlar, kategorilere ayırır ve kategori bilgilerini, System Center Online hizmetini kullanan tüm müşterilerin kullanımına sunar. Microsoft, en yüksek önceliği en çok kategorilere ayırma isteğine sahip olan yazılım başlıklarına verir. Özel yazılım ve iş kolu uygulamalarının kategorilere ayrılma olasılığı düşüktür ve en iyi uygulama olarak, bu yazılım başlıklarını kategorilere ayrılmak üzere Microsoft'a göndermemelisiniz.  

 Yazılım başlığı bilgileri kategorilere ayrılmak üzere System Center Online’a gönderildiğinde, aşağıdaki koşullar geçerli olur:  

-   Yalnızca temel yazılım başlığı bilgileri System Center Online’a aktarılır ve kategorilere ayrılacak yazılım başlığı bilgileri gönderilmeden önce gözden geçirilebilir.  

-   Yazılım lisans bilgileri hiçbir zaman iletilmez.  

-   Karşıya yüklenen tüm yazılım başlıkları System Center Online kataloğunun parçası olarak genel kullanıma açık hale gelir ve diğer müşteriler tarafından indirilebilir.  

-   Yazılım başlığı kaynağı System Center Online kataloğunda depolanmaz. Ancak, gizli ve özel bilgileri içeren uygulama başlıkları kategorilere ayrılmak için System Center Online’a gönderilmemelidir.  

> [!NOTE]  
>  Varlık Yönetim Bilgileri gizlilik bilgileri hakkında daha fazla bilgi için bkz. [varlık yönetim bilgileri Için güvenlik ve gizlilik](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 System Center Online’dan Varlık Yönetim Bilgileri kataloğu yazılım başlığı kategori isteğinde bulunmak için aşağıdaki yordamı kullanın.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>Kategorilere ayrılmamış yazılım başlıklarına yönelik katalog güncelleştirmesi istemek için  

1.  Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2.  **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne ve ardından **Envantere Kaydedilen Yazılımlar**’a tıklayın.  

3.  Kategorilere ayrılmak üzere System Center Online’a gönderilecek bir veya daha fazla ürün adı seçin. Yalnızca kategorilere ayrılmamış envantere kaydedilen yazılım başlıkları kategorilere ayırma için System Center Online’a gönderilebilir. Envantere kaydedilen bir yazılım başlığı bir yönetici tarafından kategorilere ayrılarak kullanıcı tanımlı duruma geçmişse, kategorilere ayrılmak üzere System Center Online’a gönderilmeden önce envantere kaydedilen yazılım başlığına sağ tıklayıp **Döndür** ’e tıklayarak yazılım başlığını **Kategorilere ayrılmadı** durumuna döndürmeniz gerekir.  

    > [!NOTE]  
    >  Configuration Manager, tek seferde kategorilere ayırmak için en fazla 2000 yazılım başlığını işleyebilir. 2000 ' den fazla yazılım başlığı seçerseniz, yalnızca ilk 2000 yazılım başlıkları işlenir. Kategori için kalan yazılım başlıklarını 2000 ' den az olan toplu işlerle seçmeniz gerekir.  

    > [!TIP]  
    >  Doğrulama durumuna göre sıralamak için **Durum** sütununa tıklayın. Bu, kategorilere ayrılmamış ürün adlarını görmenizi ve birden çok öğeyi kategorilere ayrılmak üzere hızlı bir şekilde seçebilmenizi sağlar.  

4.  **Giriş** sekmesinde, **Ürün** grubunda **Katalog Güncelleştirmesi İste**'ye tıklayın.  

5.  System Center Online kategori gönderimi gizlilik iletisini inceleyin. System Center Online’a gönderilecek bilgileri görüntülemek için **Ayrıntılar** ’a tıklayın.  

6.  **Bu iletiyi okudum ve anladım**’ı seçin ve ardından seçili yazılım başlıklarının kategorilere ayrılmak üzere gönderilmesine izin vermek üzere **Tamam** ’a tıklayın.  

7.  Kategorilere ayrılmak üzere System Center Online’a gönderilen envantere kaydedilmiş yazılım ürün adlarının durumunun **Kategorilere Ayrılmamış** ’tan **Bekleniyor**’a değiştiğini doğrulayın.  

    > [!NOTE]  
    >  Kategorilere ayrılmak üzere System Center Online’a gönderilen yazılımlar, merkezi yönetim sitesinde **Bekleniyor** doğrulama durumuna sahiptir, ancak alt birincil sitelerde **Kategorilere Ayrılmamış** doğrulama durumuyla gösterilmeye devam eder.  

##  <a name="resolve-software-details-conflicts"></a><a name="BKMK_ResolveSoftwareDetails"></a>Yazılım ayrıntıları çakışmalarını çözme  
 System Center Online’dan mevcut yazılım ayrıntıları bilgileriyle çakışan yeni güncelleştirilmiş yazılım kategorisi ayrıntıları alındığında, çakışmayı nasıl gidereceğinizi seçebilirsiniz. Geçerli bir çakışma bulunan yazılımlar **Güncelleştirilebilir**doğrulama durumuna sahiptir. Bir yazılım ayrıntıları çakışması giderildikten sonra, belirttiğiniz ayara uygun yazılım kategorisi bilgileri Varlık Yönetim Bilgileri kataloğunda tutulur. Çakışma çözüldükten sonra System Center Online değeri değiştirilmediği sürece, aynı yazılım kategorisi değeri için yazılım ayrıntıları çakışması yeniden oluşmaz.  

 Bir yazılım ayrıntıları çakışmasını gidermek için aşağıdaki yordamı kullanın.  

#### <a name="to-resolve-a-software-details-conflict"></a>Bir yazılım ayrıntıları çakışmasını gidermek için  

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

2. **Varlıklar ve Uyum** çalışma alanında **Varlık Yönetim Bilgileri**’ne ve ardından **Envantere Kaydedilen Yazılımlar**’a tıklayın.  

3. **Güncelleştirilebilir** durumuna sahip yazılım başlıklarının **Durum** sütununu gözden geçirin.  

4. Çakışmayı gidermeniz gereken yazılım başlığını seçin ve ardından **Giriş** sekmesinde, **Ürün** grubunda **Çakışmayı Gider**’e tıklayın.  

5. Aşağıdaki bilgileri gözden geçirin:  

   -   **Yerel değer**: Varlık Yönetim Bilgileri kataloğunda daha yeni System Center Online yazılım kategorisi ayrıntılarıyla çakışan mevcut yazılım kategorisi bilgilerini belirtir.  

   -   **İndirilen değer**: Çakışan Varlık Yönetim Bilgileri kataloğu yazılım kategorisi bilgileri için yeni System Center Online yazılım kategorisi bilgilerini belirtir.  

6. Yazılım ayrıntıları çakışmasını gidermek için aşağıdaki ayarlardan birini seçin:  

   - **Yerel olarak düzenlenen katalogdaki bilgi değerini değiştirme**: Mevcut Varlık Yönetim Bilgileri kataloğu yazılım kategorisi bilgilerini koruyarak yazılım ayrıntıları çakışmasını giderir. Bu ayarı seçtiğinizde, yazılım başlığı durumu **Güncelleştirilebilir** ’den **Kullanıcı Tanımlı**olarak değiştirilir.  

   - **Yerel olarak düzenlenmiş katalog bilgileri değerini indirilen System Center Online değeriyle değiştir**: Mevcut Varlık Yönetim Bilgileri kataloğu yazılım kategorisi bilgilerini System Center Online’dan alınan yeni bilgilerle değiştirerek yazılım ayrıntıları çakışmasını giderir. Bu ayarı seçtiğinizde, yazılım başlığı durumu **Güncelleştirilebilir** ’den **Doğrulandı**olarak değiştirilir.  

     Çakışma çözümünü kaydetmek için **Tamam** ’a tıklayın.  
