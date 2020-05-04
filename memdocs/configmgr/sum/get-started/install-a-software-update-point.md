---
title: Yazılım güncelleştirme noktası yükleyip yapılandırma
titleSuffix: Configuration Manager
description: Birincil siteler, yazılım güncelleştirmeleri uyumluluk değerlendirmesi ve istemcilere yazılım güncelleştirmeleri dağıtmak için merkezi yönetim sitesinde bir yazılım güncelleştirme noktası gerektirir.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 0cddb8df51624a562597da17ea310db0a26081f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715476"
---
# <a name="install-and-configure-a-software-update-point"></a>Yazılım güncelleştirme noktası yükleyip yapılandırma  

*Uygulama hedefi: Configuration Manager (geçerli dal)*


> [!IMPORTANT]  
>  Yazılım güncelleştirme noktası site sistemi rolünü (SUP) yüklemeden önce, sunucunun gerekli bağımlılıkları karşıladığını ve sitedeki yazılım güncelleştirme noktası altyapısını belirlediğini doğrulamanız gerekir. Yazılım güncelleştirmelerinin nasıl planlanacağı ve yazılım güncelleştirme noktası altyapınızı belirleme hakkında daha fazla bilgi için bkz. [plan for Software Updates](../plan-design/plan-for-software-updates.md).  

 Yazılım güncelleştirme noktası, yazılım güncelleştirmeleri uyumluluk değerlendirmesini etkinleştirmek ve istemcilere yazılım güncelleştirmeleri dağıtmak için merkezi yönetim sitesinde ve birincil sitelerde gereklidir. Yazılım güncelleştirme noktası ikincil sitelerde isteğe bağlıdır. WSUS yüklü olan sunucuda yazılım güncelleştirme noktası site sistemi rolü oluşturulmalıdır. Yazılım güncelleştirme noktası WSUS hizmetleriyle etkileşerek yazılım güncelleştirme ayarlarını yapılandırır ve yazılım güncelleştirme meta verilerinin eşitlenmesini ister. Configuration Manager hiyerarşiniz olduğunda, yazılım güncelleştirme noktasını önce merkezi yönetim sitesine, sonra alt birincil sitelere ve daha sonra isteğe bağlı olarak ikincil sitelere yükleyip yapılandırın. Merkezi yönetim siteniz değil tek başına birincil siteniz varsa yazılım güncelleştirme noktasını önce birincil siteye, sonra da isteğe bağlı olarak ikincil sitelere yükleyin ve yapılandırın. Bazı ayarlar yalnızca yazılım güncelleştirme noktasını üst düzey sitede yapılandırdığınız zaman kullanılabilir. Yazılım güncelleştirme noktasını yüklediğiniz yere bağlı olarak değerlendirmeniz gereken farklı seçenekler vardır.  

> [!IMPORTANT]  
>  Siteye birden fazla yazılım güncelleştirme noktası yükleyebilirsiniz. Yüklediğiniz ilk yazılım güncelleştirme noktası, Microsoft Update'ten veya yukarı akış eşitleme kaynağından gelen güncelleştirmeleri eşitleyen bir eşitleme kaynağı olarak yapılandırılır. Sitedeki diğer yazılım güncelleştirme noktaları ilk yazılım güncelleştirme noktasının çoğaltmaları olarak yapılandırılır. Bu nedenle, bazı ayarlar ilk yazılım güncelleştirme noktasını yükleyip yapılandırdıktan sonra kullanılamaz.  

> [!IMPORTANT]  
>  Yazılım güncelleştirme noktası site sistemi rolünün, tek başına WSUS sunucusu olarak yapılandırılmış ve kullanılan bir sunucuya yüklenmesi veya WSUS istemcilerini doğrudan yönetmek için bir yazılım güncelleştirme noktası kullanılması desteklenmez. Mevcut WSUS sunucuları yalnızca etkin yazılım güncelleştirme noktası için yukarı akış eşitleme kaynakları olarak desteklenir. Bkz. [yukarı akış veri kaynağı konumundan Synchronize](#BKMK_wsussync)

 Yazılım güncelleştirme noktası site sistemi rolünü mevcut bir site sistemi sunucusuna ekleyebilir veya yenisini oluşturabilirsiniz. Site sistemi **sunucusu oluşturma Sihirbazı** ' nın veya **site sistemi rolleri ekleme Sihirbazı**' nın **sistem rolü seçimi** sayfasında, site sistemi rolünü yeni veya mevcut bir site sunucusuna mı yoksa **yazılım güncelleştirme noktası**' nı seçin ve ardından sihirbazda yazılım güncelleştirme noktası ayarlarını yapılandırın. Ayarları, kullandığınız Configuration Manager sürümüne göre farklılık gösteren bir sürümdür. Site sistemi rollerinin nasıl yükleneceği hakkında daha fazla bilgi için bkz. [site sistemi rollerini yüklemek](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Sitedeki yazılım güncelleştirme noktası ayarları hakkında bilgi için aşağıdaki bölümleri kullanın.  

## <a name="proxy-server-settings"></a>Proxy sunucusu ayarları  
 Ara sunucu ayarlarını, kullandığınız Configuration Manager sürümüne bağlı olarak **site sistemi sunucusu oluşturma Sihirbazı** ' nın veya **site sistemi rolleri ekleme Sihirbazı** ' nın farklı sayfalarında yapılandırabilirsiniz.  

-   Ara sunucuyu yapılandırdıktan sonra ara sunucunun yazılım güncelleştirmeleri için ne zaman kullanılacağını belirtmeniz gerekir. Aşağıdaki ayarları yapılandırın:  

    -   Ara sunucu ayarlarını sihirbazın **Proxy** sayfasında veya Site Sistemi Özellikleri’nin **Proxy** sekmesinde yapılandırın. Ara sunucu ayarları site sistemine özeldir, yani tüm site sistem rolleri belirttiğiniz ara sunucu ayarlarını kullanır.  

    -   Configuration Manager, yazılım güncelleştirmelerini eşitlediğinde ve otomatik dağıtım kuralı kullanarak içerik indirdiğinde ara sunucunun kullanılıp kullanılmayacağını belirtin. Yazılım güncelleştirme noktası ara sunucusu ayarlarını sihirbazın **Proxy ve Hesap Ayarları** sayfasında veya Yazılım Güncelleştirme Noktası Özellikleri’nin **Proxy ve Hesap Ayarları** sekmesinde yapılandırın.  

        > [!NOTE]  
        >  **Otomatik dağıtım kuralları kullanarak içerik indirirken proxy sunucu kullan** ayarı kullanılabilir ancak ikincil sitedeki bir yazılım güncelleştirme noktası için kullanılmaz. Yalnızca merkezi yönetim sitesindeki ve birincil sitedeki yazılım güncelleştirme noktası Microsoft Update sayfasından içerik indirir.  

> [!IMPORTANT]  
>  Varsayılan seçenek olarak, İnternet’e bağlanmak ve otomatik dağıtım kuralları çalıştırıldığında yazılım güncelleştirmelerini indirmek için üzerinde otomatik dağıtım kuralı oluşturulmuş olan sunucunun **Yerel Sistem** hesabı kullanılır. Bu hesabın İnternet erişimi olmadığında yazılım güncelleştirmeleri indirilemez ve ruleengine.log dosyasına şu giriş kaydedilir: **Güncelleştirme İnternet’ten yüklenemedi. Hata = 12007**. Yerel Sistem hesabının İnternet erişimi olmadığında ara sunucuya bağlanmak için kimlik bilgilerini yapılandırın.  


## <a name="wsus-settings"></a>WSUS ayarları  
 Kullandığınız Configuration Manager sürümüne ve bazı durumlarda yalnızca yazılım güncelleştirme noktası bileşen özellikleri olarak da bilinen yazılım güncelleştirme noktası özelliklerine bağlı olarak, WSUS ayarlarını **site sistemi sunucusu oluşturma Sihirbazı** ' nın veya **site sistemi rolleri ekleme Sihirbazı** ' nın farklı sayfalarında yapılandırmanız gerekir. WSUS ayarlarını yapılandırmak için aşağıdaki bölümlerdeki bilgileri kullanın.  

### <a name="wsus-port-settings"></a><a name="BKMK_wsusport"></a>WSUS bağlantı noktası ayarları  
 WSUS bağlantı noktası ayarlarını, sihirbazın Yazılım Güncelleştirme Noktası sayfasında veya yazılım güncelleştirme noktasının özelliklerinde yapılandırmanız gerekir. WSUS tarafından kullanılan bağlantı noktası ayarlarını belirlemek için aşağıdaki yordamları kullanın.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>IIS’de kullanılan bağlantı noktası ayarlarını belirlemek için  

 1.  WSUS sunucusunda, Internet Information Services (IIS) Yöneticisi'ni açın.  

 2.  **Siteler**'i genişletin, WSUS sunucusuyla ilgili Web sitesini sağ tıklatıp **Bağlamaları Düzenle**'yi tıklatın. Site Bağlamaları iletişim kutusunda, HTTP ve HTTPS bağlantı noktası değerleri **Bağlantı Noktası** sütununda görüntülenir.


### <a name="configure-ssl-communications-to-wsus"></a>WSUS'a SSL iletişimini yapılandırma  
 SSL iletişimini sihirbazın **Genel** sayfasında veya yazılım güncelleştirme noktasının özelliklerindeki **Genel** sekmesinde yapılandırabilirsiniz.  

 SSL kullanma hakkında daha fazla bilgi için bkz. [WSUS’i SSL kullanacak şekilde yapılandırmaya karar verme](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### <a name="wsus-server-connection-account"></a>WSUS Sunucusu Bağlantı Hesabı  
 Site sunucusunun, yazılım güncelleştirme noktasında çalışan WSUS'a bağlanırken kullanacağı hesabı yapılandırabilirsiniz. Bu hesabı yapılandırmadığınızda Configuration Manager, site sunucusunun WSUS 'a bağlanması için bilgisayar hesabını kullanır. WSUS Sunucusu Bağlantı Hesabını sihirbazın **Proxy ve Hesap Ayarları** sayfasında veya Yazılım Güncelleştirme Noktası Özellikleri’nin **Proxy ve Hesap Ayarları** sekmesinde yapılandırın.  Kullandığınız Configuration Manager sürümüne bağlı olarak, hesabı sihirbazın farklı yerlerinde yapılandırabilirsiniz.  

 Configuration Manager hesapları hakkında daha fazla bilgi için bkz. [kullanılan hesaplar](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Eşitleme kaynağı  
 Yazılım güncelleştirme eşitlemesi için yukarı akış eşitleme kaynağını, sihirbazın **eşitleme kaynağı** sayfasında veya yazılım güncelleştirme noktası bileşen özellikleri 'Ndeki **eşitleme ayarları** sekmesinde yapılandırabilirsiniz. Eşitleme kaynağınız için seçenekleriniz, siteye bağlı olarak farklılık gösterir.  

 Bir sitede yazılım güncelleştirme noktasını yapılandırırken kullanılabilecek seçenekler için aşağıdaki tabloyu kullanın.  

|Site|Kullanılabilir eşitleme kaynağı seçenekleri|  
|----------|----------------------------------------------|  
|-   Merkezi yönetim sitesi<br />-   Tekil birincil site|-   Microsoft Update web sitesinden eşitleme<br />-   Bir yukarı akış veri kaynağı konumundan eşitleme<br />-   Microsoft Update veya yukarı akış veri kaynağından eşitlemeyin|  
|-   Bir sitedeki ek yazılım güncelleştirme noktaları<br />-   Alt birincil site<br />-   İkincil site|-   Bir yukarı akış veri kaynağı konumundan eşitleme|  

 Aşağıdaki listede eşitleme kaynağı olarak kullanabileceğiniz her bir seçenek hakkında daha fazla bilgi sağlanmaktadır:  

-   **Microsoft Update’den Eşitleme**: Microsoft Update’den yazılım güncelleştirmeleri meta verilerini eşitlemek için bu ayarı kullanın. Merkezi yönetim sitesinin İnternet erişimi bulunmalıdır; aksi takdirde eşitleme başarısız olur. Bu ayar yalnızca yazılım güncelleştirme noktasını üst düzey sitede yapılandırdığınızda kullanılabilir.  

    > [!NOTE]  
    >  Yazılım güncelleştirme noktası ile İnternet arasında bir güvenlik duvarı olduğunda güvenlik duvarının WSUS Web sitesi için kullanılan HTTP ve HTTPS bağlantı noktalarını kabul etmek üzere yapılandırılması gerekebilir. Güvenlik duvarındaki erişimi, sınırlı etki alanlarına da kısıtlayabilirsiniz. Yazılım güncelleştirmelerini destekleyen bir güvenlik duvarı için nasıl planlama yapılacağı hakkında daha fazla bilgi için bkz. [Güvenlik duvarlarını yapılandırma](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **Bir yukarı akış veri kaynağı konumundan eşitleme: yukarı akış eşitleme kaynağından yazılım güncelleştirmeleri meta verilerini eşitlemek için bu ayarı kullanın. <a name="BKMK_wsussync"> </a>** Alt birincil siteler ve ikincil siteler, bu ayar için ana site URL'sini kullanmak üzere otomatik olarak yapılandırılır. Var olan bir WSUS sunucusundan yazılım güncelleştirmelerini eşitleme seçeneğiniz bulunmaktadır. Örneğin `https://WSUSServer:8531`, WSUS sunucusuna bağlanmak için kullanılan bağlantı noktası olan 8531 gıbı bir URL belirtin.  

-   **Microsoft Update veya yukarı akış veri kaynağından eşitlemeyin**: Üst düzeydeki yazılım güncelleştirme noktasının İnternet bağlantısı kesildiğinde yazılım güncelleştirmelerini el ile eşitlemek için bu ayarı kullanın. Daha fazla bilgi için bkz. [Yazılım güncelleştirmelerini bağlantısı kesilen yazılım güncelleştirme noktasında eşitleme](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  Yazılım güncelleştirme noktası ile İnternet arasında bir güvenlik duvarı olduğunda güvenlik duvarının WSUS Web sitesi için kullanılan HTTP ve HTTPS bağlantı noktalarını kabul etmek üzere yapılandırılması gerekebilir. Güvenlik duvarındaki erişimi, sınırlı etki alanlarına da kısıtlayabilirsiniz. Yazılım güncelleştirmelerini destekleyen bir güvenlik duvarı için nasıl planlama yapılacağı hakkında daha fazla bilgi için bkz. [Güvenlik duvarlarını yapılandırma](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Ayrıca, sihirbazın **eşitleme kaynağı** sayfasında veya yazılım güncelleştirme noktası bileşen özellikleri ' nde **EŞITLEME ayarları** sekmesinde WSUS raporlama olaylarının oluşturulup oluşturulmayacağını de yapılandırabilirsiniz. Configuration Manager bu olayları kullanmaz; Bu nedenle, normalde **WSUS raporlama olaylarını oluşturma**varsayılan ayarını seçersiniz.  

## <a name="synchronization-schedule"></a>Eşitleme zamanlaması  
 Eşitleme zamanlamasını, sihirbazın **Eşitleme Zamanlaması** sayfasında veya Yazılım Güncelleştirme Noktası Bileşen Özellikleri’nde yapılandırın. Bu ayar yalnızca yazılım güncelleştirme noktasında üst düzey sitede yapılandırılır.  

 Zamanlamayı etkinleştirirseniz, yinelenen basit veya özel bir eşitleme zamanlaması yapılandırabilirsiniz. Basit bir zamanlama yapılandırdığınızda, başlangıç saati, zamanlamayı oluştururken Configuration Manager konsolunu çalıştıran bilgisayar için yerel saate dayanır. Bir özel zamanlama için başlangıç saatini yapılandırdığınızda, bu, Configuration Manager konsolunu çalıştıran bilgisayar için yerel saate dayanır.  

> [!TIP]  
>  Yazılım güncelleştirmeleri eşitlemesini, ortamınız için uygun bir zaman çerçevesi kullanarak çalışacak şekilde zamanlayın. Tipik bir senaryo, yazılım güncelleştirmeleri eşitleme zamanlamasını, normalde Patch Tuesday olarak adlandırılan her ayın ikinci Salı günü yayınlanan Microsoft düzenli güvenlik güncelleştirmesinden kısa süre sonra çalışmak üzere ayarlamaktır. Başka bir tipik senaryo, yazılım güncelleştirmeleri eşitlemesini, Uç Nokta Koruma tanımı ve motor güncelleştirmelerini göndermek için yazılım güncelleştirmeleri kullandığınızda her gün çalışacak şekilde ayarlamaktır.  

> [!NOTE]  
>  Yazılım güncelleştirmeleri eşitlemesini bir zamanlamayla yapılmasını etkinleştirmemeyi seçtiğinizde, yazılım güncelleştirmelerini, Yazılım Kitaplığı çalışma alanında **Yazılım Güncelleştirme Grupları** veya **Tüm Yazılım Güncelleştirmeleri** düğümünden el ile eşitleyebilirsiniz. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini Synchronize](synchronize-software-updates.md).  

## <a name="supersedence-rules"></a>Yerine geçme kuralları  
 Yerine geçme ayarlarını, sihirbazın **Yerine Geçme Kuralları** sayfasında veya Yazılım Güncelleştirme Noktası Bileşen Özellikleri’ndeki **Yerine Geçme Kuralları** sekmesinde yapılandırın. Yerine geçme kurallarını yalnızca üst düzey sitede yapılandırabilirsiniz. Configuration Manager sürüm 1810 ' den başlayarak, özellik **güncelleştirmeleri** için değiştirme kuralları davranışını **Özellik dışı güncelleştirmelerden**ayrı olarak belirtebilirsiniz. <!--3098809, 2977644-->

 Bu sayfada, değiştirilen yazılım güncelleştirmelerinin derhal süresinin geçeceğini belirtebilirsiniz, böylelikle yeni dağıtımlara dahil edilmeleri önlenir ve var olan dağıtımlar, değiştirilen yazılım güncelleştirmelerinin bir veya daha fazla süresi geçmiş yazılım güncelleştirmesi içerdiği belirtilecek şekilde işaretlenir. Ya da önceki yazılım güncelleştirmelerinin süresi dolmadan önce beklenecek bir süre belirtebilirsiniz ve bu da onları dağıtmaya devam etmenize olanak tanır. Daha fazla bilgi için, bkz. [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  Sihirbazın **Yerine Geçme Kuralları** sayfası yalnızca sitede ilk yazılım güncelleştirme noktasını yapılandırdığınızda kullanılabilir. Bu sayfa, ek yazılım güncelleştirme noktaları yüklediğinizde görüntülenmez.  

## <a name="classifications"></a>Sınıflandırmalar  
 Sınıflandırma ayarlarını, sihirbazın **sınıflandırmalar** sayfasında veya yazılım güncelleştirme noktası bileşen özellikleri 'ndeki **sınıflandırmalar** sekmesinde yapılandırın. Yazılım güncelleştirme sınıflandırmaları hakkında daha fazla bilgi için bkz. [Güncelleştirme sınıflandırmaları](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  Sihirbazın **Sınıflandırmalar** sayfası, yalnızca sitede ilk yazılım güncelleştirme noktasını yapılandırdığınızda kullanılabilir. Bu sayfa, ek yazılım güncelleştirme noktaları yüklediğinizde görüntülenmez.  

> [!TIP]  
>  Yazılım güncelleştirme noktasını üst düzey sitede ilk kez yüklediğinizde, tüm yazılım güncelleştirme sınıflandırmalarını temizleyin. İlk yazılım güncelleştirmeleri eşitlemesi sonrasında, sınıflandırmaları, güncelleştirilmiş bir listeden yapılandırın ve ardından eşitlemeyi yeniden başlatın. Bu ayar yalnızca yazılım güncelleştirme noktasında üst düzey sitede yapılandırılır.  

## <a name="products"></a>Ürünler  
 Ürün ayarlarını, sihirbazın **Ürünler** sayfasında veya yazılım güncelleştirme noktası bileşen özellikleri 'ndeki **Ürünler** sekmesinde yapılandırın.  

> [!NOTE]  
>  Sihirbazın **Ürünler** sayfası, yalnızca sitede ilk yazılım güncelleştirme noktasını yapılandırdığınızda kullanılabilir. Bu sayfa, ek yazılım güncelleştirme noktaları yüklediğinizde görüntülenmez.  

> [!TIP]  
>  Yazılım güncelleştirme noktasını üst düzey sitede ilk kez yüklediğinizde, tüm ürünleri temizleyin. İlk yazılım güncelleştirmeleri eşitlemesi sonrasında, ürünleri, güncelleştirilmiş bir listeden yapılandırın ve ardından eşitlemeyi yeniden başlatın. Bu ayar yalnızca yazılım güncelleştirme noktasında üst düzey sitede yapılandırılır.  

## <a name="languages"></a>Diller  
 Dil ayarlarını, sihirbazın **Diller** sayfasında veya yazılım güncelleştirme noktası bileşen özellikleri 'ndeki **Diller** sekmesinde yapılandırın. Yazılım güncelleştirme dosyalarını ve özet ayrıntılarını eşitlemek istediğiniz dilleri belirtin. **Yazılım güncelleştirme dosyası** ayarı, Configuration Manager hiyerarşisindeki her bir yazılım güncelleştirme noktasında yapılandırılır. **Özet Ayrıntıları** ayarları, yalnızca üst düzey yazılım güncelleştirme noktasında yapılandırılır. Daha fazla bilgi için bkz. [Diller](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  Sihirbazın **Diller** sayfası, yalnızca merkezi yönetim sitesinde ilk yazılım güncelleştirme noktasını yüklediğinizde kullanılabilir. Alt sitelerdeki Yazılım Güncelleştirme Dosyası dillerini, Yazılım Güncelleştirme Noktası Bileşen Özellikleri’nde **Diller** sekmesinde yapılandırabilirsiniz.  

## <a name="third-party-updates"></a>Üçüncü taraf güncelleştirmeleri
Configuration Manager sürüm 1802 ' den başlayarak Configuration Manager istemcileri için üçüncü taraf güncelleştirmelerini etkinleştirebilirsiniz. SUP bileşen özelliklerinde üçüncü taraf yazılım güncelleştirmelerini etkinleştirdiğinizde, SUP, WSUS tarafından üçüncü taraf güncelleştirmeleri için kullanılan imzalama sertifikasını indirir. Bu seçenek, yazılım güncelleştirme noktasının yüklenmesi sırasında kullanılamaz ve SUP yüklendikten sonra yapılandırılmalıdır. Üçüncü taraf güncelleştirmeleri için istemci ayarlarını etkinleştirmek üzere bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) makalesi.

## <a name="next-steps"></a>Sonraki adımlar
Yazılım güncelleştirme noktasını, Configuration Manager hiyerarşinizdeki en üst siteden başlayarak yüklediniz. Yazılım güncelleştirme noktasını alt sitelere yüklemek için bu makaledeki yordamları tekrarlayın.

Yazılım güncelleştirme noktalarınızı yükledikten sonra, [yazılım güncelleştirmelerini Synchronize](synchronize-software-updates.md)' a gidin.
