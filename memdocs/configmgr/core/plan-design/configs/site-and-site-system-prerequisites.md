---
title: Site önkoşulları
titleSuffix: Configuration Manager
description: Bir Windows bilgisayarını Configuration Manager site sistem sunucusu olarak yapılandırmayı öğrenin.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce3420a6e229b5987616c5c0c1c41d50cdc499c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700359"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Configuration Manager için site ve site sistemi önkoşulları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Windows tabanlı bilgisayarlar, kullanımları Configuration Manager site sistemi sunucuları olarak desteklemek için belirli yapılandırmaların kullanılmasını gerektirir.

Yazılım güncelleştirme noktası için Windows Server Update Services (WSUS) gibi bazı ürünlerde, ek önkoşulları ve kullanım sınırlamalarını belirlemek için ürün belgelerine başvurmanız gerekir. Yalnızca Configuration Manager ile kullanım için doğrudan uygulanan konfigürasyonlar buraya dahildir.

.NET Framework hakkında daha fazla bilgi için bkz. [yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> Genel gereksinimler ve sınırlamalar

Tüm site sistemi sunucuları için aşağıdaki gereksinimler geçerlidir:

- Her site sistem sunucusu, 64 bitlik bir işletim sistemi kullanmalıdır. Tek istisna, bazı 32 bit işletim sistemlerine yükleyebileceğiniz dağıtım noktası site sistemi rolüdür.  

- Site sistemleri herhangi bir işletim sisteminin Sunucu Çekirdeği yüklemelerinde desteklenmez. Bir özel durum, dağıtım noktası site sistem rolü için sunucu çekirdeği yüklemelerinin desteklenme noktasıdır. Daha fazla bilgi için bkz. [Configuration Manager site sistemi sunucuları Için desteklenen işletim sistemleri](supported-operating-systems-for-site-system-servers.md).  

- Bir site sistemi sunucusu yüklendikten sonra değiştirmek desteklenmez:  

    - Site sistemi bilgisayarının bulunduğu etki alanının etki alanı adı ( **etki alanı yeniden adlandırma**da denir).  

    - Bilgisayarın etki alanı üyeliği.  

    - Bilgisayarın adı.  

    Bu öğelerden herhangi birini değiştirmeniz gerekiyorsa, önce bilgisayardan site sistem rolünü kaldırın. Ardından, değişiklik tamamlandıktan sonra rolü yeniden yükleyin. Site sunucusunu etkileyen değişiklikler için önce siteyi kaldırın. Ardından, değişiklik tamamlandıktan sonra siteyi yeniden yükleyin.  

- Site sistem rolleri bir Windows Server kümesinin örneğinde desteklenmez. Tek istisna site veritabanı sunucusudur. Daha fazla bilgi için bkz. [Configuration Manager site veritabanı için SQL Server kümesi kullanma](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).  

    Sürüm 1810 ' den başlayarak, Configuration Manager Kurulum işlemi artık site sunucusu rolünün yük devretme kümelemesi için Windows rolü olan bir bilgisayara yüklenmesini engeller. SQL Always on bu rolü gerektirir, bu nedenle daha önce site sunucusundaki site veritabanını birlikte bulunduramıyorsunuz. Bu değişiklik ile, SQL Always on ve site sunucusu ' nu pasif modda kullanarak daha az sunucu ile yüksek oranda kullanılabilir bir site oluşturabilirsiniz. Daha fazla bilgi için bkz. [yüksek kullanılabilirlik seçenekleri](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->  

- Herhangi bir Configuration Manager hizmeti için başlangıç türü veya "farklı oturum açma" ayarlarını değiştirmek desteklenmez. Bunu yaparsanız, önemli hizmetlerin düzgün çalışmasını engelleyebilirsiniz.  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Windows Server 2012 ve üzeri işletim sistemleri için Önkoşullar  

Windows Server 2012 ve üzeri sürümlerde site sistem sunucularına ve rollerine yönelik belirli Önkoşullar için bu makalenin ana bölümlerine bakın:

- [Merkezi Yönetim sitesi ve birincil site sunucuları](#bkmk_2012sspreq)
- [İkincil site sunucusu](#bkmk_2012secpreq)
- [Veritabanı sunucusu](#bkmk_2012dbpreq)
- [SMS sağlayıcı sunucusu](#bkmk_2012smsprovpreq)
- [Uygulama Kataloğu web sitesi noktası](#bkmk_2012acwspreq)
- [Uygulama Kataloğu web hizmet noktası](#bkmk_2012ACwsitepreq)
- [Varlık Yönetim Bilgileri eşitleme noktası](#bkmk_2012AIpreq)
- [Sertifika kayıt noktası](#bkmk_2012crppreq)
- [Dağıtım noktası](#bkmk_2012dppreq)
- [Uç Nokta Koruma noktası](#bkmk_2012EPPpreq)
- [Kayıt noktası](#bkmk_2012Enrollpreq)
- [Kayıt proxy noktası](#bkmk_2012EnrollProxpreq)
- [Geri dönüş durumu noktası](#bkmk_2012FSPpreq)
- [Yönetim noktası](#bkmk_2012MPpreq)
- [Raporlama Hizmetleri noktası](#bkmk_2012RSpoint)
- [Hizmet bağlantı noktası](#bkmk_SCPpreq)
- [Yazılım güncelleştirme noktası](#bkmk_2012SUPpreq)
- [Durum geçiş noktası](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a> Merkezi Yönetim sitesi ve birincil site sunucuları

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework 3.5

- Uzaktan Değişiklikleri Sıkıştırma  

- Site sunucusu dışında bir sunucuda yazılım güncelleştirme noktası kullandığınızda, site sunucusuna WSUS Yönetim Konsolu 'Nu yükleyebilirsiniz.

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- Bir merkezi yönetim sitesini veya birincil siteyi yüklemeden veya yükseltmeden önce, yüklediğiniz veya yükselttiğiniz Configuration Manager sürümünün gerektirdiği Windows değerlendirme ve dağıtım seti 'nin (ADK) sürümünü yükleyebilirsiniz. Daha fazla bilgi için bkz. [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Bu gereksinim hakkında daha fazla bilgi için bkz. [işletim sistemi dağıtımı Için altyapı gereksinimleri](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="visual-c-redistributable"></a>Yeniden dağıtılabilir Visual C++  

- Configuration Manager, Microsoft Visual C++ 2013 yeniden dağıtılabilir paketini bir site sunucusu yükleyen her bilgisayara yüklüyor.  

- Merkezi yönetim siteleri ve birincil siteler, uygulanabilir yeniden dağıtılabilir dosyanın hem x86 hem de x64 sürümlerini gerektirir.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a> İkincil site sunucusu

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework 3.5

- Uzaktan Değişiklikleri Sıkıştırma  

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Yeniden dağıtılabilir Visual C++

- Configuration Manager, Microsoft Visual C++ 2013 yeniden dağıtılabilir paketini bir site sunucusu yükleyen her bilgisayara yüklüyor.  

- İkincil siteler yalnızca x64 sürümünü gerektirir.  

### <a name="default-site-system-roles"></a>Varsayılan site sistemi rolleri  

- Varsayılan olarak, ikincil bir site bir **Yönetim noktası** ve bir **dağıtım noktası**yüklenir.  

- İkincil site sunucusunun bu site sistem rolleri için önkoşulları karşıladığından emin olun.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a> Veritabanı sunucusu  

### <a name="remote-registry-service"></a>Uzak Kayıt Defteri hizmeti  

- Configuration Manager sitesinin yüklenmesi sırasında, site veritabanını barındıran bilgisayarda **Uzak kayıt defteri** hizmetini etkinleştirin.  

### <a name="sql-server"></a>SQL Server  

- Bir merkezi yönetim sitesini veya birincil siteyi yüklemeden önce, site veritabanını barındırmak için SQL Server desteklenen bir sürümünü yükleyebilirsiniz. Daha fazla bilgi için bkz. [desteklenen SQL Server sürümleri](support-for-sql-server-versions.md).  

- İkincil bir site yüklemeden önce desteklenen bir SQL Server sürümünü yükleyebilirsiniz.  

- İkincil site yüklemesinin bir parçası olarak SQL Server Express Configuration Manager yüklemeyi tercih ederseniz, bilgisayarın SQL Server Express çalıştırma gereksinimlerini karşıladığından emin olun.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> SMS sağlayıcı sunucusu  

### <a name="windows-adk"></a>Windows ADK

- SMS sağlayıcısı 'nın bir örneğini yüklediğiniz bilgisayar, yüklemekte olduğunuz veya yükselttiğiniz Configuration Manager sürümünün gerektirdiği Windows ADK 'nin gerekli sürümüne sahip olmalıdır. Daha fazla bilgi için bkz. [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Bu gereksinim hakkında daha fazla bilgi için bkz. [işletim sistemi dağıtımı Için altyapı gereksinimleri](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- [Yönetim hizmetini](../../../develop/adminservice/overview.md)KULLANıYORSANıZ, SMS sağlayıcısı rolünü barındıran sunucu için .NET 4,5 veya üzeri bir sürüm gerekir  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager sürüm 1810, .NET 4.5.2 veya üstünü gerektirir.

- Web sunucusu (IIS): her sağlayıcı [Yönetim hizmetini](../../../develop/adminservice/overview.md)yüklemeye çalışır. Bu hizmetin, bir sertifikayı HTTPS bağlantı noktası 443 ' e bağlamak için IIS 'e bağımlılığı vardır. Configuration Manager, bu sertifika yapılandırmasını denetlemek için IIS API 'Lerini kullanır. Siteyi [GELIŞMIŞ http](../hierarchy/enhanced-http.md)için yapılandırırsanız Configuration Manager, site tarafından oluşturulan sertifikayı bağlamak Için IIS API 'lerini kullanır. Sürüm 2002 ' den başlayarak, site otomatik olarak otomatik olarak imzalanan sertifikayı kullanır.

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> Uygulama Kataloğu web sitesi noktası  

> [!Important]  
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makaleleri inceleyin:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS yapılandırması  

- Ortak HTTP özellikleri:  

    - Varsayılan Belge  

    - Statik İçerik  

- Uygulama geliştirme:  

    - ASP.NET 3,5 (ve otomatik olarak belirlenen seçenekler)  

    - ASP.NET 4,5 (ve otomatik olarak belirlenen seçenekler)  

    - .NET Genişletilebilirliği 3.5  

    - .NET Extensibility 4.5  

- Güven  

    - Windows Kimlik Doğrulaması  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> Uygulama Kataloğu Web hizmet noktası  

> [!Important]  
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makaleleri inceleyin:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework 3.5

- ASP.NET 4,5:  

    - HTTP Etkinleştirmesi (ve otomatik olarak belirlenen seçenekler)  

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS yapılandırması

- Ortak HTTP özellikleri:  

    - Varsayılan Belge  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  

- Uygulama geliştirme:  

    - ASP.NET 3,5 (ve otomatik olarak belirlenen seçenekler)  

    - .NET Genişletilebilirliği 3.5  

    - ASP.NET 4,5 (ve otomatik olarak belirlenen seçenekler)  

    - .NET Extensibility 4.5  

### <a name="computer-memory"></a>Bilgisayar belleği  

- Bu site sistemi rolünü barındıran bilgisayarda, site sistem rolünün istekleri işlemesini sağlamak için bilgisayarın kullanılabilir belleğinin en az %5 ' i olmalıdır.  

- Bu site sistem rolü aynı gereksinime sahip başka bir site sistem rolüyle birlikte kullanıldığında, bilgisayar için bu bellek gereksinimi artmaz, ancak en az %5 oranında kalır.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> Varlık Yönetim Bilgileri eşitleme noktası  

### <a name="net-framework"></a>.NET Framework

.NET Framework sürüm 4,5 veya sonraki bir sürümü için desteklenen bir sürümünü yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> Sertifika kayıt noktası  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework

    - HTTP Etkinleştirmesi  

### <a name="net-framework"></a>.NET Framework

.NET Framework sürüm 4,5 veya sonraki bir sürümü için desteklenen bir sürümünü yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS yapılandırması

- Uygulama geliştirme:  

    - ASP.NET 3,5 (ve otomatik olarak belirlenen seçenekler)  

    - ASP.NET 4,5 (ve otomatik olarak belirlenen seçenekler)  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  

    - IIS 6 WMI Uyumluluğu  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a> Dağıtım noktası  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- Uzaktan Değişiklikleri Sıkıştırma  

#### <a name="iis-configuration"></a>IIS yapılandırması

- Uygulama geliştirme:  

    - ISAPI Uzantıları  

- Güven  

    - Windows Kimlik Doğrulaması  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  

    - IIS 6 WMI Uyumluluğu  

### <a name="powershell"></a>PowerShell  

- Windows Server 2012 veya sonraki sürümlerde, dağıtım noktasını yüklemeden önce PowerShell 3,0 veya 4,0 gereklidir.  

### <a name="visual-c-redistributable"></a>Yeniden dağıtılabilir Visual C++

- Configuration Manager, Microsoft Visual C++ 2013 yeniden dağıtılabilir paketini bir dağıtım noktası barındıran her bilgisayara yüklenir.  

- Yüklenen sürüm, bilgisayarın platformuna (x86 veya x64) bağlıdır.  

### <a name="microsoft-azure"></a>Microsoft Azure  

- Dağıtım noktasını barındırmak için Microsoft Azure içinde bir bulut hizmeti kullanabilirsiniz.  

### <a name="to-support-pxe-or-multicast"></a>PXE veya çok noktaya yayını desteklemek için  

- Windows dağıtım hizmeti olmadan bir dağıtım noktasında PXE Yanıtlayıcıyı etkinleştirin.  

- Windows Dağıtım Hizmetleri (WDS) Windows Server rolünü yükleyip yapılandırın.  

    > [!NOTE]  
    > WDS, Windows Server 2012 veya üstünü çalıştıran bir sunucuda PXE veya çok noktaya yayını destekleyecek şekilde bir dağıtım noktası yapılandırdığınızda otomatik olarak yüklenir ve yapılandırır.  

- Çok noktaya yayın özellikli bir dağıtım noktası için SQL Server Native Client yüklendiğinden ve güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Daha fazla bilgi için bkz. [dağıtım noktalarını yükleyip yapılandırma](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Dağıtım noktası içerik aktarırken, Windows içinde yerleşik **arka plan Akıllı Aktarım Hizmeti** (BITS) kullanarak aktarır. İstemci bu sunucuya bilgi yüklemediğinden dağıtım noktası rolü isteğe bağlı BITS IIS sunucu uzantısı özelliğinin yüklenmesini gerektirmez.  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection noktası  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri  

- .NET Framework 3.5

- Windows Defender özellikleri (Windows Server 2016 veya üzeri)  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> Kayıt noktası  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework 3.5

    - HTTP Etkinleştirmesi (ve otomatik olarak belirlenen seçenekler)  

    - ASP.NET 4.5  

    - Windows Communication Foundation (WCF) Hizmetleri<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

> [!Note]
> Bu site sistemi rolü yüklendiğinde, Configuration Manager .NET Framework 4.5.2 otomatik olarak yüklenir. Bu yükleme, sunucuyu yeniden başlatma bekleme durumuna yerleştirebilir. .NET Framework için bir yeniden başlatma beklendiğinde, .NET uygulamaları sunucu yeniden başlatılana ve yükleme bitene kadar başarısız olabilir.  

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS yapılandırması

- Ortak HTTP özellikleri:  

    - Varsayılan Belge  

- Uygulama geliştirme:  

    - ASP.NET 3,5 (ve otomatik olarak belirlenen seçenekler)  

    - .NET Genişletilebilirliği 3.5  

    - ASP.NET 4,5 (ve otomatik olarak belirlenen seçenekler)  

    - .NET Extensibility 4.5  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  

### <a name="computer-memory"></a>Bilgisayar belleği

- Bu site sistemi rolünü barındıran bilgisayarda, site sistem rolünün istekleri işlemesini sağlamak için bilgisayarın kullanılabilir belleğinin en az %5 ' i olmalıdır.  

- Bu site sistem rolü aynı gereksinime sahip başka bir site sistem rolüyle birlikte kullanıldığında, bilgisayar için bu bellek gereksinimi artmaz, ancak en az %5 oranında kalır.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> Kayıt proxy noktası  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

> [!Note]
> Bu site sistemi rolü yüklendiğinde, Configuration Manager .NET Framework 4.5.2 otomatik olarak yüklenir. Bu yükleme, sunucuyu yeniden başlatma bekleme durumuna yerleştirebilir. .NET Framework için bir yeniden başlatma beklendiğinde, .NET uygulamaları sunucu yeniden başlatılana ve yükleme bitene kadar başarısız olabilir.  

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS yapılandırması

- Ortak HTTP özellikleri:  

    - Varsayılan Belge  

    - Statik İçerik  

- Uygulama geliştirme:  

    - ASP.NET 3,5 (ve otomatik olarak belirlenen seçenekler)  

    - ASP.NET 4,5 (ve otomatik olarak belirlenen seçenekler)  

    - .NET Genişletilebilirliği 3.5  

    - .NET Extensibility 4.5  

- Güven  

    - Windows Kimlik Doğrulaması  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  

### <a name="computer-memory"></a>Bilgisayar belleği

- Bu site sistemi rolünü barındıran bilgisayarda, site sistem rolünün istekleri işlemesini sağlamak için bilgisayarın kullanılabilir belleğinin en az %5 ' i olmalıdır.  

- Bu site sistem rolü aynı gereksinime sahip başka bir site sistem rolüyle birlikte kullanıldığında, bilgisayar için bu bellek gereksinimi artmaz, ancak en az %5 oranında kalır.  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> Geri dönüş durum noktası

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- BITS Sunucu Uzantıları (ve otomatik olarak belirlenen seçenekler) ya da arka plan Akıllı Aktarım Hizmetleri (BITS) (ve otomatik olarak belirlenen seçenekler)

#### <a name="iis-configuration"></a>IIS yapılandırması

Varsayılan IIS yapılandırması aşağıdaki eklemelerle gereklidir:  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a> Yönetim noktası  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- BITS Sunucu Uzantıları (ve otomatik olarak belirlenen seçenekler) ya da arka plan Akıllı Aktarım Hizmetleri (BITS) (ve otomatik olarak belirlenen seçenekler)  

### <a name="net-framework"></a>.NET Framework

.NET Framework sürüm 4,5 veya sonraki bir sürümü için desteklenen bir sürümünü yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS yapılandırması

- Uygulama geliştirme:  

    - ISAPI Uzantıları  

- Güven  

    - Windows Kimlik Doğrulaması  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  

    - IIS 6 WMI Uyumluluğu  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Raporlama Hizmetleri noktası  

### <a name="net-framework"></a>.NET Framework

.NET Framework sürüm 4,5 veya sonraki bir sürümü için desteklenen bir sürümünü yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- Raporlama noktasını yüklemeden önce SQL Server Reporting Services desteklemek için en az bir SQL Server örneğini yükleyip yapılandırın.  

- SQL Server Reporting Services için kullandığınız örnek, site veritabanı için kullandığınız örnekle aynı olabilir.  

- Ayrıca, kullandığınız örnek, diğer System Center ürünleri SQL Server örneğini paylaşma kısıtlamalarına sahip olmadığı sürece diğer System Center ürünleriyle paylaşılabilir.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a> Hizmet bağlantı noktası  

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

> [!Note]
> Bu site sistemi rolü yüklendiğinde, Configuration Manager .NET Framework 4.5.2 otomatik olarak yüklenir. Bu yükleme, sunucuyu yeniden başlatma bekleme durumuna yerleştirebilir. .NET Framework için bir yeniden başlatma beklendiğinde, .NET uygulamaları sunucu yeniden başlatılana ve yükleme bitene kadar başarısız olabilir.  

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Yeniden dağıtılabilir Visual C++

- Configuration Manager, Microsoft Visual C++ 2013 yeniden dağıtılabilir paketini bir dağıtım noktası barındıran her bilgisayara yüklenir.  

- Site sistemi rolü için x64 sürümü gerekir.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a> Yazılım güncelleştirme noktası  

### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework 3.5

Varsayılan IIS yapılandırması gereklidir.

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- Yazılım güncelleştirme noktası yüklemeden önce Windows Server rolü Windows Server Update Services 'ı bir bilgisayara yükler.  

- Daha fazla bilgi için bkz. [plan for Software Updates](../../../sum/plan-design/plan-for-software-updates.md).  

> [!NOTE]  
> Site sunucusu dışında bir sunucuda yazılım güncelleştirme noktası kullandığınızda, WSUS Yönetim konsolunu site sunucusuna yüklemelisiniz.

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> Durum geçiş noktası

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Windows Server rolleri ve özellikleri

- .NET Framework 3.5

    - HTTP Etkinleştirmesi (ve otomatik olarak belirlenen seçenekler)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

3,5 .NET Framework için Windows özelliğini etkinleştirin.

Ayrıca, 4,5 veya sonraki bir sürümü .NET Framework desteklenen bir sürümünü de yükler. Sürüm 1906 ' den başlayarak Configuration Manager .NET Framework 4,8 ' i destekler.

> [!Note]
> Bu site sistemi rolü yüklendiğinde, Configuration Manager .NET Framework 4.5.2 otomatik olarak yüklenir. Bu yükleme, sunucuyu yeniden başlatma bekleme durumuna yerleştirebilir. .NET Framework için bir yeniden başlatma beklendiğinde, .NET uygulamaları sunucu yeniden başlatılana ve yükleme bitene kadar başarısız olabilir.  

.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [.NET Framework sürümleri ve bağımlılıklar](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Yaşam döngüsü SSS-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS yapılandırması

- Ortak HTTP özellikleri:  

    - Varsayılan Belge  

- Uygulama geliştirme:  

    - ASP.NET 3,5 (ve otomatik olarak belirlenen seçenekler)  

    - .NET Genişletilebilirliği 3.5  

    - ASP.NET 4,5 (ve otomatik olarak belirlenen seçenekler)  

    - .NET Extensibility 4.5  

- IIS 6 Yönetim uyumluluğu:  

    - IIS 6 Metatabanı Uyumluluğu  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Yeni bir site yüklediğinizde Configuration Manager otomatik olarak yeniden dağıtılabilir bir bileşen olarak SQL Server Native Client yükler. Site yüklendikten sonra Configuration Manager SQL Server Native Client yükseltmez. Bu bileşenin güncel olduğundan emin olun. Daha fazla bilgi için bkz. [önkoşul denetimleri-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).