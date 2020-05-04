---
title: Hizmet bağlantı aracı
titleSuffix: Configuration Manager
description: Kullanım bilgilerini el ile karşıya yüklemek için Configuration Manager bulut hizmetine bağlanmanızı sağlayan bu araç hakkında bilgi edinin.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e535653e0f31e186a6bdbde8da77750f2afdfdb0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710821"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Configuration Manager için hizmet bağlantısı aracını kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hizmet bağlantı noktanız çevrimdışı modda olduğunda veya Configuration Manager site sistem sunucularınız Internet 'e bağlı olmadığında **hizmet bağlantı aracını** kullanın. Araç, Configuration Manager en son güncelleştirmeleriyle sitenizi güncel tutmaya yardımcı olabilir.  

Çalıştırıldığında, araç, hiyerarşinizin kullanım bilgilerini karşıya yüklemek ve güncelleştirmeleri indirmek için Configuration Manager bulut hizmetine el ile bağlanır. Kullanım verilerinin karşıya yüklenmesi, bulut hizmetinin dağıtımınız için doğru güncelleştirmeleri sağlaması için gereklidir.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Hizmet bağlantı aracını kullanma önkoşulları
Önkoşullar ve bilinen sorunlar aşağıda verilmiştir.

**Kaynakları**

- Yüklü bir hizmet bağlantı noktanız var ve **Çevrimdışı, isteğe bağlı bağlantı**olarak ayarlanmış.  

- Aracın bir komut isteminden çalıştırılması gerekir.  

- Aracın çalıştığı her bilgisayarda (hizmet bağlantı noktası bilgisayarı ve İnternet’e bağlı olan bilgisayar) x64 bit işletim sistemi ve aşağıdakilerin yüklü olması gerekir:  

  - **Visual C++ Yeniden Dağıtılabilir** x86 ve x64 dosyaları.   Varsayılan olarak, Configuration Manager, hizmet bağlantı noktasını barındıran bilgisayara x64 sürümünü yüklenir.  

    Visual C++ dosyalarının bir kopyasını indirmek için, Microsoft İndirme Merkezi’ndeki [Visual Studio 2013 için Visual C++ Yeniden Dağıtılabilir Paketleri](https://www.microsoft.com/download/details.aspx?id=40784) sayfasını ziyaret edin.  

  - .NET Framework 4.5.2 veya üzeri.  

- Aracı çalıştırmak için kullandığınız hesabın şunlara sahip olması gerekir:
  - Hizmet bağlantı noktasını barındıran (aracın çalıştığı) bilgisayarda**yerel yönetici** izinleri.
  - Site veritabanına**Okuma** izinleri.  



- Hizmet bağlantı noktası bilgisayarı ile İnternet bağlantısı olan bilgisayar arasında dosya aktarmak için, dosya ve güncelleştirmeleri depolamaya yetecek boş alana sahip bir USB sürücüye veya başka bir yönteme ihtiyacınız vardır. (Bu senaryoda, site ve yönetilen bilgisayarlarınızın doğrudan İnternet bağlantısı olmadığı varsayılır.)  



## <a name="use-the-service-connection-tool"></a>Hizmet bağlantısı aracını kullanma  

 Hizmet bağlantı aracını (**serviceconnectiontool. exe**), Configuration Manager yükleme medyasında **%Path%\smssetup\tools\serviceconnectiontool** klasöründe bulabilirsiniz. Her zaman kullandığınız Configuration Manager sürümüyle eşleşen hizmet bağlantı aracını kullanın.


 Bu yordamda, komut satırı örnekleri aşağıdaki dosya adlarını ve klasör konumlarını kullanmaktadır (bu yollar ile dosya adlarını kullanmanız gerekmez ve bunlar yerine ortamınız ve tercihlerinizle eşleşen alternatifler kullanabilirsiniz):  

- Sunucular arasında aktarılmak üzere verilerin depolandığı USB Çubuğu’nun yolu: **D:\USB\\**  

- Sitenizden dışarı aktarılan verileri içeren.cab dosyasının adı: **UsageData.cab**  

- Sunucular arasında aktarılmak üzere indirilen Configuration Manager güncelleştirmelerinin depolanacağı boş klasörün adı: **UpdatePacks**  

Hizmet bağlantı noktasını barındıran bilgisayarda:  

- Yönetici ayrıcalıklarıyla bir komut istemi açın ve ardından dizin değiştirerek **serviceconnectiontool.exe**aracını içeren konuma gidin.  

  Varsayılan olarak, bu aracı **%Path%\smssetup\tools\serviceconnectiontool** klasöründe Configuration Manager yükleme medyasında bulabilirsiniz. Hizmet bağlantı aracının çalışması için bu klasördeki tüm dosyaların aynı klasörde olması gerekir.  

Aşağıdaki komutu çalıştırdığınızda, araç, kullanım bilgileri içeren bir .cab dosyası hazırlar ve dosyayı belirttiğiniz konuma kopyalar. Bu .cab dosyasındaki veriler, sitenizin toplamak üzere yapılandırıldığı tanılama kullanım verileri düzeyini temel alır. ( [Configuration Manager Için tanılama ve kullanım verilerine](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)bakın).  .cab dosyasını oluşturmak için aşağıdaki komutu çalıştırın:  

- **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

Ayrıca, ServiceConnectionTool klasörünü tüm içindekilerle birlikte USB sürücüsüne kopyalamanız veya 3. ve 4. adımlar için kullanacağınız bilgisayardan bu klasöre erişebilmeniz gerekir.  

### <a name="overview"></a>Genel Bakış
#### <a name="there-are-three-primary-steps-to-using-the-service-connection-tool"></a>Hizmet bağlantı aracının kullanılmasına yönelik başlıca üç adım vardır  

1.  **Hazırlama**: Bu adım, hizmet bağlantı noktasını barındıran bilgisayarda çalışır. Araç çalıştırıldığında, kullanım verilerinizi bir. cab dosyasına koyar ve bir USB sürücüde (veya belirttiğiniz alternatif aktarım konumunda) depolar.  

2.  **Bağlan**: Bu adım için, aracı Internet 'e bağlanan uzak bir bilgisayarda çalıştırarak kullanım verilerinizi karşıya yükleyebilir ve sonra güncelleştirmeleri indirebilirsiniz.  

3.  **Içeri aktarma**: Bu adım, hizmet bağlantı noktasını barındıran bilgisayarda çalışır. Çalıştırdığınızda araç, indirdiğiniz güncelleştirmeleri içeri aktarır ve bu güncelleştirmeleri Configuration Manager konsolundan görüntüleyip yükleyebilmeniz için sitenize ekler.  

Sürüm 1606’dan başlayarak, Microsoft’a bağlandığınızda bir kerede birden çok .cab dosyasını karşıya yükleyebilir (her biri farklı hiyerarşiden), proxy sunucunu ve proxy sunucusu için kullanıcıyı belirtebilirsiniz.   

#### <a name="to-upload-multiple-cab-files"></a>Birden çok. cab dosyasını karşıya yüklemek için
- Ayrı hiyerarşilerden dışarı aktardığınız her .cab dosyasını aynı klasöre yerleştirin. Her dosyanın adı benzersiz olmalıdır; gerekirse bunları kendiniz yeniden adlandırabilirsiniz.
- Ardından, verileri Microsoft’a yükleme komutunu çalıştırdığınızda .cab dosyalarını içeren klasörü belirtirsiniz. (Güncelleştirme 1606’dan önce, bir kerede tek bir hiyerarşiden verileri karşıya yükleyebiliyordunuz ve araç, klasörde .cab dosyasının adını belirtmenizi istiyordu.)
- Daha sonra, hiyerarşinin hizmet bağlantı noktasında içeri aktarma görevini çalıştırdığınızda, araç otomatik olarak yalnızca o hiyerarşinin verilerini içeri aktarır.  

#### <a name="to-specify-a-proxy-server"></a>Proxy sunucusu belirtmek için
Proxy sunucusunu belirtmek için aşağıdaki isteğe bağlı parametreleri kullanabilirsiniz. (Bu konunun Komut satırı parametreleri bölümünde bu parametreleri kullanma hakkında daha fazla bilgi bulabilirsiniz):
- **-proxyserveruri [FQDN_of_proxy_server]**  Bu bağlantı için kullanılacak proxy sunucusunu belirtmek için bu parametreyi kullanın.
- **-proxyusername [kullanıcıadı]**  Proxy sunucusu için kullanıcı belirtmeniz gerektiğinde bu parametreyi kullanın.

#### <a name="specify-the-type-of-updates-to-download"></a>İndirilecek güncelleştirmelerin türünü belirtin
Sürüm 1706 ' den başlayarak, araçların varsayılan indirme davranışı değişmiştir ve araç, indirdiklerinizi hangi dosyaları kontrol etmek için seçenekleri destekler.
- Varsayılan olarak, araç yalnızca sitenizin sürümü için geçerli olan en son güncelleştirmeleri indirir. Düzeltmeleri indirmez.

Bu davranışı değiştirmek için, hangi dosyaların indirileceğini değiştirmek üzere aşağıdaki parametrelerden birini kullanın. 

> [!NOTE]
> Sitenizin sürümü, araç çalıştırıldığında karşıya yüklenen. cab dosyasındaki verilerden belirlenir.
>
> . Cab dosyasının içindeki *Siteversion*. txt dosyasını arayarak sürümü doğrulayabilirsiniz.

- **-downloadall**  Bu seçenek, sitenizin sürümünden bağımsız olarak, güncelleştirmeler ve düzeltmeler de dahil olmak üzere her şeyi indirir.
- **-downloadhotfix**  Bu seçenek, sitenizin sürümünden bağımsız olarak tüm düzeltmeleri indirir.
- **-downloadsiteversion**  Bu seçenek, sitenizin sürümünden daha yüksek bir sürüme sahip olan güncelleştirmeleri ve düzeltmeleri indirir.

*-Downloadsiteversion*kullanan örnek komut satırı:
- **serviceconnectiontool. exe-Connect *-downloadsiteversion* -usagedatasrc d:\usb-updatepackdest D:\USB\UpdatePacks**




### <a name="to-use-the-service-connection-tool"></a>Hizmet bağlantı aracını kullanmak için  

1. Hizmet bağlantı noktasını barındıran bilgisayarda:  

   - Yönetici ayrıcalıklarıyla bir komut istemi açın ve ardından dizin değiştirerek **serviceconnectiontool.exe**aracını içeren konuma gidin.   

2. Aracın, kullanım bilgileri içeren bir .cab dosyası hazırlamasını ve dosyayı belirttiğiniz konuma kopyalamasını sağlamak için aşağıdaki komutu çalıştırın:  

   - **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

   Birden çok hiyerarşiden .cab dosyalarını bir kerede karşıya yükleyecekseniz, klasördeki her .cab dosyasının adı benzersiz olmalıdır. Dosyaları klasöre eklerken el ile yeniden adlandırabilirsiniz.

   Configuration Manager bulut hizmetine yüklenmek üzere toplanan kullanım bilgilerini görüntülemek istiyorsanız, aşağıdaki komutu çalıştırarak aynı verileri .csv dosyası olarak dışarı aktarın (bu dosyayı Excel gibi bir uygulamada görüntüleyebilirsiniz):  

   - **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3. Hazırlama adımı tamamlandıktan sonra, USB sürücüsünü İnternet erişimi olan bir bilgisayara taşıyın (veya dışarı aktarılan verileri farklı bir şekilde aktarın).  

4. İnternet erişimi olan bilgisayarda, yönetici ayrıcalıklarıyla bir komut istemi açın ve ardından dizin değiştirerek  **serviceconnectiontool.exe** aracını ve bu klasördeki diğer dosyaların kopyasını içeren konuma gidin.  

5. Configuration Manager için kullanım bilgilerini karşıya yükleme ve güncelleştirmeleri indirme işlemine başlamak için aşağıdaki komutu çalıştırın:  

   - **serviceconnectiontool. exe-Connect-usagedatasrc D:\USB-updatepackdest D:\USB\UpdatePacks**

   Bu komut satırıyla ilgili diğer örnekler için, bu konunun devamındaki [Komut satırı seçenekleri](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) bölümüne bakın.

   > [!NOTE]  
   >  Configuration Manager bulut hizmetine bağlanmak için komut satırını çalıştırdığınızda, aşağıdakine benzer bir hata oluşabilir:  
   >   
   > - İşlenmemiş Özel Durum: System.UnauthorizedAccessException:  
   >   
   >      'C:\  
   >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' yoluna erişim reddedildi.  
   >   
   > Bu hata güvenli bir şekilde yok sayılabilir ve hata penceresini kapatarak devam edebilirsiniz.  

6. Configuration Manager güncelleştirmelerini indirme işlemi tamamlandıktan sonra, USB sürücüsünü hizmet bağlantı noktasını barındıran bilgisayara taşıyın (veya dışarı aktarılan verileri farklı bir şekilde aktarın).  

7. Hizmet bağlantı noktasını barındıran bilgisayarda, yönetici ayrıcalıklarıyla bir komut istemi açın, dizin değiştirerek **serviceconnectiontool.exe**aracını içeren konuma gidin ve ardından şu komutu çalıştırın:  

   - **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8. İçeri aktarma işlemi tamamlandıktan sonra komut istemini kapatabilirsiniz. (Yalnızca geçerli hiyerarşi için güncelleştirmeler içeri aktarılır).  

9. Configuration Manager konsolunu açın ve **Yönetim** > **güncelleştirmeleri ve bakım '** a gidin. İçeri aktarılan güncelleştirmeler artık yüklenebilir. (Sürüm 1702 ' den önce, güncelleştirmeler ve bakım, **Yönetim** > **Cloud Services**altındadır.)

   Güncelleştirmeleri yükleme hakkında daha fazla bilgi için bkz. [Configuration Manager için konsol içi güncelleştirmeleri yükleme](../../../core/servers/manage/install-in-console-updates.md).  

## <a name="log-files"></a><a name="bkmk_cmd"></a>Günlük dosyaları

**ServiceConnectionTool. log**

Hizmet bağlantı aracını her çalıştırdığınızda, **Serviceconnectiontool. log**adlı araçla aynı konumda bir günlük dosyası oluşturulur.  Bu günlük dosyası, hangi komutların kullanıldığına bağlı olarak aracın yürütülmesi hakkında basit ayrıntılar sağlar.  Aracı her çalıştırdığınızda var olan bir günlük dosyası değişir.

**ConfigMgrSetup. log**

Güncelleştirmeleri bağlamak ve indirmek için araç kullanırken, **ConfigMgrSetup. log**adlı sistem sürücüsünün kökünde bir günlük dosyası oluşturulur.  Bu günlük dosyası, hangi dosyaların indirileceği, ayıklandığı ve karma denetimlerin başarılı olup olmadığı gibi daha ayrıntılı bilgiler sağlar.

## <a name="command-line-options"></a><a name="bkmk_cmd"></a> Komut satırı seçenekleri  
Hizmet bağlantı noktası aracına yönelik yardım bilgilerini görüntülemek için, aracı içeren klasöre ait komut satırını açın ve şu komutu çalıştırın:  **serviceconnectiontool.exe**.  


|Komut satırı seçenekleri|Ayrıntılar|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [drive:][path][filename.cab]**|Bu komut, geçerli kullanım verilerini bir .cab dosyasında depolar.<br /><br /> Bu komutu, hizmet bağlantı noktasını barındıran sunucuda **yerel yönetici** olarak çalıştırın.<br /><br /> Örnek:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [sürücü:][yol] -updatepackdest [sürücü:][yol] -proxyserveruri [proxy sunucusu FQDN’si] -proxyusername [kullanıcıadı]** <br /> <br /> Configuration Manager’ın 1606’dan önceki bir sürümünü kullanıyorsanız, .cab dosyasının adını belirtmeniz gerekir ve proxy sunucusu seçeneklerini kullanamazsınız.  Desteklenen komutu parametreleri: <br /> **-connect -usagedatasrc [sürücü:][yol][dosyaadı] -updatepackdest [sürücü:][yol]** |Bu komut, belirtilen konumdan kullanım verileri .cab dosyalarını karşıya yüklemek ve sağlanan güncelleştirme paketleriyle konsol içeriğini indirmek için Configuration Manager bulut hizmetine bağlanır. Proxy sunucularına yönelik seçenekler isteğe bağlıdır.<br /><br /> Bu komutu, İnternet’e bağlanabilen bilgisayarda **yerel yönetici** olarak çalıştırın.<br /><br /> Proxy sunucusu olmadan bağlanma örneği: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Proxy sunucusu kullanırken bağlanma örneği: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> 1606’dan önceki bir sürümü kullanıyorsanız, .cab dosyası için dosya adını belirtmeniz gerekir ve proxy sunucusu belirtemezsiniz. Aşağıdaki örnek komut satırını kullanın: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [drive:][path]**|Bu komut, daha önce Configuration Manager konsolunuza indirdiğiniz güncelleştirme paketlerini ve konsol içeriğini içeri aktarır.<br /><br /> Bu komutu, hizmet bağlantı noktasını barındıran sunucuda **yerel yönetici** olarak çalıştırın.<br /><br /> Örnek:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [drive:][path][filename.csv]**|Bu komut, kullanım verilerini daha sonra görüntüleyebileceğiniz bir .csv dosyasına dışarı aktarır.<br /><br /> Bu komutu, hizmet bağlantı noktasını barındıran sunucuda **yerel yönetici** olarak çalıştırın.<br /><br /> Örnek: **-export -dest D:\USB\usagedata.csv**|  
