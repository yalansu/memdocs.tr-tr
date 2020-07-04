---
title: Hizmet bağlantı aracı
titleSuffix: Configuration Manager
description: Kullanım bilgilerini el ile karşıya yüklemek için Configuration Manager bulut hizmetine bağlanmanızı sağlayan bu araç hakkında bilgi edinin.
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 48aa08f3318aaa4629691bfb30b60580cd3e25f0
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946853"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Configuration Manager için hizmet bağlantısı aracını kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hizmet bağlantı noktanız çevrimdışı modda olduğunda **hizmet bağlantı aracını** kullanın. Ayrıca, Configuration Manager site sistem sunucularınız internet 'e bağlı olmadığında da kullanabilirsiniz. Araç, Configuration Manager en son güncelleştirmeleriyle sitenizi güncel tutmanıza yardımcı olabilir.

Aracı çalıştırdığınızda, Configuration Manager bulut hizmetine bağlanır, hiyerarşiniz için kullanım bilgilerini karşıya yükler ve güncelleştirmeleri indirir. Kullanım verilerinin karşıya yüklenmesi, bulut hizmetinin ortamınız için doğru güncelleştirmeleri sağlamasını sağlamak için gereklidir.

## <a name="prerequisites"></a>Önkoşullar

- Sitenin bir hizmet bağlantı noktası vardır ve bunu **çevrimdışı, isteğe bağlı bir bağlantı**için yapılandırırsınız.

- Aracı bir komut isteminden yönetici olarak çalıştırın. Kullanıcı arabirimi yok.

- Aracı, hizmet bağlantı noktasından ve internet 'e bağlanabilecek bir bilgisayardan çalıştırırsınız. Bu bilgisayarların her birinin x64 bit işletim sistemi olması ve aşağıdaki bileşenlere sahip olması gerekir:

  - **Visual C++ Yeniden Dağıtılabilir** x86 ve x64 dosyaları. Varsayılan olarak, Configuration Manager, hizmet bağlantı noktasını barındıran bilgisayara x64 sürümünü yüklenir. Bu bileşeni indirmek için, bkz. [Visual Studio 2013 Için yeniden dağıtılabilir paketler Visual C++](https://www.microsoft.com/download/details.aspx?id=40784).

  - **.NET Framework 4.5.2** veya üzeri

- Aracı çalıştırmak için kullandığınız hesap şu izinlere ihtiyaç duyuyor:

  - Hizmet bağlantı noktasını barındıran bilgisayarda **yerel yönetici**

  - Site veritabanı için **okuma** izinleri

- Internet erişimi ve hizmet bağlantı noktası olan bilgisayar arasında dosyaları aktarmak için bir yönteme ihtiyacınız vardır. Örneğin, dosyaları ve güncelleştirmeleri depolamak için yeterli boş alana sahip bir USB sürücü.

## <a name="overview"></a>Genel Bakış

1. **Hazırla**: Aracı hizmet bağlantı noktasında çalıştırın. Kullanım verilerinizi, belirttiğiniz konumdaki bir. cab dosyasına yerleştirir. Veri dosyasını Internet bağlantısı olan bilgisayara kopyalayın.

2. **Bağlan**: bilgisayarda bir internet bağlantısı olan aracı çalıştırın. Kullanım verilerinizi karşıya yükler ve ardından Configuration Manager güncelleştirmeleri indirir. İndirilen güncelleştirmeleri hizmet bağlantı noktasına kopyalayın.

    Tek seferde birden çok veri dosyasını, her biri farklı bir hiyerarşiden karşıya yükleyebilirsiniz. Proxy sunucusu için bir ara sunucu ve Kullanıcı da belirtebilirsiniz.

3. **Içeri aktar**: Aracı hizmet bağlantı noktasında çalıştırın. Güncelleştirmeleri içeri aktarır ve sitenize ekler. Daha sonra [Bu güncelleştirmeleri](install-in-console-updates.md) Configuration Manager konsolunda görüntüleyebilir ve yükleyebilirsiniz.

### <a name="upload-multiple-data-files"></a>Birden çok veri dosyasını karşıya yükleme

- Ayrı Hiyerarşilerden tüm aktarılmış veri dosyalarını aynı klasöre yerleştirin. Her dosyaya benzersiz bir ad verin. Gerekirse, bunları el ile yeniden adlandırabilirsiniz.

- Microsoft 'a veri yüklemek için aracı çalıştırdığınızda, veri dosyalarını içeren klasörü belirtirsiniz.

- Verileri içeri aktarmak için aracı çalıştırdığınızda, araç yalnızca söz konusu hiyerarşinin verilerini içeri aktarır.

### <a name="specify-a-proxy-server"></a>Proxy sunucusu belirtin

Internet bağlantısı olan bilgisayar bir ara sunucu gerektiriyorsa, araç temel bir proxy yapılandırmasını destekler. **-Proxyserveruri** ve **-ProxyUserName**isteğe bağlı parametrelerini kullanın. Daha fazla bilgi için bkz. [komut satırı parametreleri](#bkmk_cmd).

### <a name="specify-the-type-of-updates-to-download"></a>İndirilecek güncelleştirmelerin türünü belirtin

Araç, hangi dosyaları indirdiklerinizi denetlemek için seçenekleri destekler. Varsayılan olarak, araç yalnızca sitenizin sürümü için geçerli olan en son güncelleştirmeleri indirir. Düzeltmeleri indirmez.

Bu davranışı değiştirmek için, indirdiği dosyaları değiştirmek üzere aşağıdaki parametrelerden birini kullanın:

- **-downloadall**: sitenizin sürümü ne olursa olsun, güncelleştirmeler ve düzeltmeler de dahil olmak üzere tüm güncelleştirmeleri indirin.
- **-downloadhotfix**: sitenizin sürümüne her şeyi olan tüm düzeltmeleri indirin.
- **-downloadsiteversion**: güncelleştirmeleri ve düzeltmeleri sitenizin sürümünden daha sonraki bir sürümle indirir.

    > [!IMPORTANT]
    > Configuration Manager sürüm 2002 ' deki bilinen bir sorundan dolayı varsayılan davranış beklendiği gibi çalışmaz. Sürüm 2002 için gerekli güncelleştirmeleri indirmek üzere **-downloadsiteversion** parametresini kullanın.<!-- 7594517 -->

Daha fazla bilgi için bkz. [komut satırı parametreleri](#bkmk_cmd).

> [!TIP]
> Araç, sitenizin veri dosyasından sürümünü belirler. Sürümü doğrulamak için, site sürümüyle adlı metin dosyası için. cab dosyasına bakın.

## <a name="use-the-tool"></a>Aracı kullanma  

Hizmet bağlantı aracı, aşağıdaki yolda Configuration Manager yükleme medyasında bulunur: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe` . Her zaman kullandığınız Configuration Manager sürümüyle eşleşen hizmet bağlantı aracını kullanın. Hizmet bağlantı aracının çalışması için bu dosyaların tümünün aynı klasörde olması gerekir.

**Serviceconnectiontool** klasörünü tüm içeriğiyle birlikte internet bağlantısı olan bilgisayara kopyalayın.

Bu yordamda, komut satırı örnekleri aşağıdaki dosya adlarını ve klasör konumlarını kullanır. Bu yolları ve dosya adlarını kullanmanız gerekmez. Ortamınız ve tercihlerinizle eşleşen alternatifleri kullanabilirsiniz.

- Hizmet bağlantı noktasındaki Configuration Manager yükleme medyası kaynak dosyalarının yolu:`C:\Source`

- Bilgisayarlar arasında aktarılacak verileri depoladığınız USB sürücüsünün yolu:`D:\USB\`

- Siteden dışarı verdiğiniz veri dosyasının adı:`UsageData.cab`

- Aracın Configuration Manager için indirilen güncelleştirmeleri depoladığı boş klasörün adı:`UpdatePacks`

### <a name="prepare"></a>Hazırlama

1. Hizmet bağlantı noktasını barındıran bilgisayarda yönetici olarak bir komut istemi açın ve dizini araç konumuyla değiştirin. Örneğin:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Veri dosyasını hazırlamak için aşağıdaki komutu çalıştırın:

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > Aynı anda birden fazla hiyerarşiden veri dosyası yükleyeceksiniz, her veri dosyasına benzersiz bir ad verin. Gerekirse dosyaları daha sonra yeniden adlandırabilirsiniz.

    Dosyadaki veriler, site için yapılandırdığınız tanılama ve kullanım verileri düzeyini temel alır. Daha fazla bilgi için bkz. [Tanılama ve kullanım verilerine genel bakış](../../plan-design/diagnostics/diagnostics-and-usage-data.md). İçeriğini görüntülemek için, bir CSV dosyasına verileri dışarı aktarmak için aracını kullanabilirsiniz. Daha fazla bilgi için bkz. [-dışarı aktarma](#-export).

1. Araç kullanım verilerini dışarı aktarmayı tamamladıktan sonra, veri dosyasını internet erişimi olan bir bilgisayara kopyalayın.

### <a name="connect"></a>Bağlan

1. İnternet erişimi olan bilgisayarda, yönetici olarak bir komut istemi açın ve dizini araç konumuyla değiştirin. Bu konum, **Serviceconnectiontool** klasörünün tamamının bir kopyasıdır. Örneğin:

    `cd D:\USB\ServiceConnectionTool\`

1. Veri dosyasını karşıya yüklemek ve Configuration Manager güncelleştirmelerini indirmek için aşağıdaki komutu çalıştırın:

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    Daha fazla örnek için bkz. [komut satırı parametreleri](#bkmk_cmd).

    > [!NOTE]  
    > Bu komut satırını çalıştırdığınızda, aşağıdaki hatayı görebilirsiniz:
    >
    > **İşlenmeyen özel durum: System. UnauthorizedAccessException: ' C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql ' yoluna erişim reddedildi.**
    >
    > Bu hatayı güvenle yoksayabilirsiniz. Devam etmek için hata penceresini kapatın.

1. Araç güncelleştirmeleri indirmeyi tamamladıktan sonra, bunları hizmet bağlantı noktasına kopyalayın.

### <a name="import"></a>İçeri Aktar

1. Hizmet bağlantı noktasını barındıran bilgisayarda yönetici olarak bir komut istemi açın ve dizini araç konumuyla değiştirin. Örneğin:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Güncelleştirmeleri içeri aktarmak için aşağıdaki komutu çalıştırın:

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. İçeri aktarma işlemi tamamlandıktan sonra komut istemi ' ni kapatın. Yalnızca ilgili hiyerarşinin güncelleştirmelerini içeri aktarır.

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **güncelleştirmeler ve bakım** düğümünü seçin. İçeri aktarılan güncelleştirmeler artık yüklenebilir. Daha fazla bilgi için bkz. [konsol içi güncelleştirmeleri yüklemeyi](install-in-console-updates.md).

## <a name="log-files"></a>Günlük dosyaları

- **Serviceconnectiontool. log**: hizmet bağlantı aracını her çalıştırdığınızda, bu günlük dosyasına yazar. Günlük dosyasının yolu, araç ile her zaman aynı konumdur. Bu günlük dosyası, kullandığınız parametrelere göre araç kullanımı hakkında basit ayrıntılar sağlar. Aracı her çalıştırdığınızda, araç var olan herhangi bir günlük dosyasının yerini alır.

- **ConfigMgrSetup. log**: [bağlantı](#connect) aşamasında, araç sistem sürücüsünün kökündeki bu günlük dosyasına yazar. Bu günlük dosyası daha ayrıntılı bilgi sağlar. Örneğin, aracın indirdiği dosyalar ve karma denetimleri başarılı olursa.

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a>Komut satırı parametreleri

Bu bölüm, hizmet bağlantı aracı için tüm kullanılabilir parametrelerin alfabetik sırasını alfabetik olarak listeler.

### <a name="-connect"></a>-Bağlan

İnternet erişimi olan bilgisayardaki [bağlanma](#connect) aşamasında kullanın. Veri dosyasını karşıya yüklemek ve güncelleştirmeleri indirmek için Configuration Manager bulut hizmetine bağlanır.

Aşağıdaki parametreleri gerektirir:

- **-usagedatasrc**: karşıya yüklenecek veri dosyasının konumu
- **-updatepackdest**: indirilen güncelleştirmeler için bir yol

Aşağıdaki isteğe bağlı parametreleri de kullanabilirsiniz:

- **-proxyserveruri**: proxy sunucusunun FQDN 'si
- **-ProxyUserName**: proxy sunucu için bir Kullanıcı adı
- **-downloadall**: sitenizin sürümü ne olursa olsun, güncelleştirmeler ve düzeltmeler de dahil olmak üzere her şeyi indirin.
- **-downloadhotfix**: sitenizin sürümünü her ne olursa olsun tüm düzeltmeleri indirin.
- **-downloadsiteversion**: sitenizin sürümünden daha sonraki bir sürüme sahip güncelleştirmeleri ve düzeltmeleri indirin.

#### <a name="example-of-connect-without-a-proxy-server"></a>Proxy sunucusu olmadan bağlanma örneği

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>Proxy sunucusu ile bağlanma örneği

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>Yalnızca site sürümü uygulanabilir güncelleştirmeleri indirmek için Bağlan örneği

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-dest

Dışarı aktarılacak CSV dosyasının yolunu ve dosya adını belirtmek için **-Export** parametresine sahip gerekli bir parametre. Daha fazla bilgi için bkz. [-dışarı aktarma](#-export).

### <a name="-downloadall"></a>-downloadall

Sitenizin sürümü ne olursa olsun, güncelleştirmeler ve düzeltmeler de dahil olmak üzere her şeyi indirmek için **-Connect** parametresine sahip isteğe bağlı bir parametre. Daha fazla bilgi için bkz. [-Connect](#connect).

### <a name="-downloadhotfix"></a>-downloadhotfix

Sitenizin sürümü ne olursa olsun, yalnızca tüm düzeltmeleri indirmek için **-Connect** parametresine sahip isteğe bağlı bir parametre. Daha fazla bilgi için bkz. [-Connect](#-connect).

### <a name="-downloadsiteversion"></a>-downloadsiteversion

Yalnızca sitenizin sürümünden daha sonraki bir sürüme sahip güncelleştirmeleri ve düzeltmeleri indirmek için **-Connect** parametresine sahip isteğe bağlı bir parametre. Daha fazla bilgi için bkz. [-Connect](#-connect).

### <a name="-export"></a>-dışarı aktarma

Kullanım verilerini bir CSV dosyasına aktarmak için [hazırlama](#prepare) aşamasında kullanın. Hizmet bağlantı noktasında yönetici olarak çalıştırın. Bu eylem, Microsoft 'a yüklemeden önce kullanım verilerinin içeriğini incelemenizi sağlar. CSV dosyasının konumunu belirtmek için **-dest** parametresini gerektirir.

#### <a name="example-of-export"></a>Dışarı aktarma örneği

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>-İçeri Aktar

Güncelleştirmeleri siteye aktarmak için hizmet bağlantı noktasındaki [Içeri aktarma](#import) aşamasında öğesini kullanın. İndirilen güncelleştirmelerin konumunu belirtmek için **-updatepacksrc** parametresini gerektirir.

#### <a name="example-of-import"></a>İçeri aktarma örneği

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>-hazırlama

Siteden kullanım verilerini dışarı aktarmak için hizmet bağlantı noktasındaki [hazırlama](#prepare) aşamasında ' ı kullanın. Bu, **-usagedatadest** parametresinin, dışarıya aktarılmış veri dosyasının konumunu belirtmesini gerektirir.

#### <a name="example-of-prepare"></a>Hazırlama örneği

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>-proxyserveruri

Ara sunucunuzun FQDN 'sini belirtmek için **-Connect** parametresine sahip isteğe bağlı bir parametre. Daha fazla bilgi için bkz. [-Connect](#-connect).

### <a name="-proxyusername"></a>-ProxyUserName

Proxy sunucunuz ile kimlik doğrulaması yapılacak Kullanıcı adını belirtmek için **-Connect** parametresine sahip isteğe bağlı bir parametre. Daha fazla bilgi için bkz. [-Connect](#-connect).

### <a name="-updatepackdest"></a>-updatepackdest

İndirilen güncelleştirmeler için bir yol belirtmek üzere **-Connect** parametresine sahip gerekli bir parametre. Daha fazla bilgi için bkz. [-Connect](#-connect).

### <a name="-updatepacksrc"></a>-updatepacksrc

İndirilen güncelleştirmelerin yolunu belirtmek için **-import** parametresine sahip gerekli bir parametre. Daha fazla bilgi için bkz. [-içeri aktarma](#-import).

### <a name="-usagedatadest"></a>-usagedatadest

İçe aktarılmış veri dosyasının yolunu ve dosya adını belirtmek için **-Prepare** parametresine sahip gerekli bir parametre. Daha fazla bilgi için bkz. [-hazırlama](#-prepare).

## <a name="next-steps"></a>Sonraki adımlar

[Konsol güncelleştirmelerini yükleyin](install-in-console-updates.md)

[Tanılama ve kullanım verilerini görüntüleme](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
