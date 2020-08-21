---
title: OSD altyapı gereksinimleri
titleSuffix: Configuration Manager
description: Configuration Manager içinde işletim sistemi dağıtımı için dış ve ürün bağımlılıklarını ve gereksinimleri öğrenin
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9bb07bd2b82a9411bc527d04a9a64a0bb6e12f8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697679"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Configuration Manager işletim sistemi dağıtımı için altyapı gereksinimleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager işletim sistemi dağıtımının dış bağımlılıkları ve ürün içinde bağımlılıkları vardır. Altyapıyı işletim sistemi dağıtımına hazırlanmanıza yardımcı olması için bu makaleyi kullanın.  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a> Configuration Manager dış bağımlılıklar  

Bu bölümde, Configuration Manager ' de işletim sistemlerini dağıtmak için gereken harici araçlar, yükleme setleri ve işletim SISTEMI sürümleri hakkında bilgi verilmektedir.  

### <a name="windows-adk-for-windows-10"></a>Windows 10 için Windows ADK  

Windows değerlendirme ve Dağıtım Seti (ADK), Windows 'un yapılandırmasını ve dağıtımını destekleyen bir araç ve belge kümesidir. Configuration Manager, Windows 'u yükleme, görüntü yakalama ve Kullanıcı profillerini ve verilerini geçirme gibi eylemleri otomatikleştirmek için Windows ADK 'yi kullanır.  

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

- [BT Uzmanlarına yönelik Windows 10 için Windows ADK senaryoları](/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Windows 10 için Windows ADK’yi indirin](/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > ADK için hem Windows **10 Için WINDOWS ADK** hem de **Windows PE eklentisi**' ni indirdiğinizden emin olun.

- [Windows 10 için destek](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>Site sistemleri
Windows ADK, aşağıdaki site sistemi sunucuları için bir önkoşuldur:

- Hiyerarşideki en üst düzey sitenin site sunucusu  

- Hiyerarşideki her birincil sitenin site sunucusu  

- SMS sağlayıcısı 'nın her örneği  


> [!NOTE]  
> Configuration Manager sitesini yüklemeden önce, Windows ADK 'yi her site sunucusuna el ile yükleyebilirsiniz.  

#### <a name="windows-adk-features"></a>Windows ADK özellikleri
Windows ADK 'nin aşağıdaki özelliklerini yükler:  

-   Kullanıcı Durumu Taşıma Aracı (USMT)  

    > [!Note]  
    > USMT, SMS sağlayıcısında gerekli değildir.

-   Windows Dağıtım Araçları  

-   Windows Önyükleme Ortamı (Windows PE)  

    > [!Important]  
    > Windows 10 sürüm 1809 ' den itibaren, Windows PE ayrı bir yükleyicidir. Aksi takdirde işlevsel farklılık yoktur.<!--SCCMDocs-pr issue 2908-->  

Farklı Configuration Manager sürümleriyle kullanabileceğiniz Windows 10 ADK sürümlerinin bir listesi için, bkz. [Windows 10 Için destek](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).


### <a name="user-state-migration-tool-usmt"></a>Kullanıcı Durumu Taşıma Aracı (USMT)  

Configuration Manager, işletim sistemi dağıtımınızın parçası olarak Kullanıcı durumunu yakalamak ve geri yüklemek için USMT 10 kaynak dosyalarını içeren bir USMT paketini kullanır. Configuration Manager Kurulum, USMT paketini otomatik olarak oluşturur. USMT 10, Windows 7, Windows 8, Windows 8.1 ve Windows 10 ' dan Kullanıcı durumunu yakalar.  

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

- [USMT 10 için Genel Geçiş Senaryoları](/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Kullanıcı durumunu yönetme](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Windows PE, bir bilgisayarı başlatmak için kullanılan önyükleme yansımaları için kullanılır. Windows 'un yükleme öncesi ve dağıtımı sırasında kullanılan sınırlı hizmetlere sahip bir Windows sürümüdür. Aşağıdaki liste Configuration Manager için Windows ADK 'nin desteklenen sürümlerini içerir, güncel Dalı:  

#### <a name="windows-adk-version"></a>Windows ADK sürümü  
Windows 10 için Windows ADK. Daha fazla bilgi için bkz. [Windows 10 Için destek](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Configuration Manager konsolundan özelleştirilebilen önyükleme görüntüleri için Windows PE sürümleri  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Configuration Manager konsolundan özelleştirilemeyen önyükleme görüntüleri için desteklenen Windows PE sürümleri  
Windows PE 3.1<sup>1</sup> ve Windows PE 5  

<sup>1</sup> yalnızca Windows PE 3,1 temelinde Configuration Manager bir önyükleme görüntüsü ekleyebilirsiniz. Windows 7 için Windows AIK'yi (Windows PE 3 tabanlı) Windows 7 SP1 için Windows AIK Eki (Windows PE 3.1 tabanlı) ile yükseltmek için, Windows 7 SP1 için Windows AIK Eki'ni yükleyin. Windows 7 SP1 için Windows AIK eki 'ni [Microsoft Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=5188)' nden indirin.  

Örneğin, Configuration Manager sahip olduğunuzda, Windows 10 için Windows ADK (Windows PE 10 tabanlı) önyükleme görüntülerini Configuration Manager konsolundan özelleştirebilirsiniz. Bununla birlikte, Windows PE 5 tabanlı önyükleme görüntüleri desteklenirken, bunları farklı bir bilgisayardan özelleştirmeniz ve DıSM 'nin Windows 8 için Windows ADK ile birlikte yüklenen sürümünü kullanmanız gerekir. Ardından önyükleme görüntüsünü Configuration Manager konsoluna ekleyin. Önyükleme görüntüsünü özelleştirme (isteğe bağlı bileşenler ve Sürücüler ekleme), önyükleme görüntüsü için komut desteğini etkinleştirme, önyükleme görüntüsünü Configuration Manager konsoluna ekleme ve Önyükleme görüntüsüyle dağıtım noktalarını güncelleştirme adımları hakkında daha fazla bilgi için bkz. [önyükleme görüntülerini özelleştirme](../get-started/customize-boot-images.md). Önyükleme görüntüleri hakkında daha fazla bilgi için bkz. [Önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

Yazılım güncelleştirme noktası için WSUS gereklidir, bu, işletim sistemi dağıtımı sırasında yazılım güncelleştirmelerini yüklemek için gereklidir. Daha fazla bilgi için bkz. [Configure a Install a Software Update Point](../../sum/get-started/install-a-software-update-point.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Site sistem sunucularındaki Internet Information Services (IIS)  

Dağıtım noktası, durum geçiş noktası ve yönetim noktası için IIS gereklidir. Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


### <a name="windows-deployment-services-wds"></a>Windows Dağıtım Hizmetleri (WDS)  

Sürüm 1802 ve önceki sürümlerinde WDS, PXE dağıtımları için gereklidir. Sürüm 1806 ' den başlayarak, WDS olmadan bir dağıtım noktasında PXE 'yi etkinleştirebilirsiniz. Daha fazla bilgi için bu makaledeki [Windows Dağıtım Hizmetleri](#BKMK_WDS) bölümüne bakın. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Dinamik Ana Bilgisayar Yapılandırma Protokolü (DHCP)  

DHCP, PXE dağıtımları için gerekli olur. İşletim sistemlerini PXE kullanarak dağıtmak için aktif ana bilgisayarı olan çalışır durumda bir DHCP sunucunuzun olması gerekir. PXE dağıtımları hakkında daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Desteklenen işletim sistemleri ve sabit disk yapılandırmaları  

İşletim sistemlerini dağıtırken Configuration Manager tarafından desteklenen işletim sistemi sürümleri ve sabit disk yapılandırması hakkında daha fazla bilgi için bkz. [desteklenen işletim sistemleri](#BKMK_SupportedOS) ve [Desteklenen disk yapılandırması](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Windows cihaz sürücüleri  

İşletim sistemini hedef bilgisayara yüklediğinizde, Windows cihaz sürücüleri kullanılabilir. Ayrıca, Windows PE 'yi bir önyükleme görüntüsünde çalıştırdığınızda da kullanılır. Daha fazla bilgi için bkz. [sürücüleri yönetme](../get-started/manage-drivers.md).  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a> Configuration Manager Bağımlılıklar  

Bu bölüm Configuration Manager işletim sistemi dağıtımı önkoşulları hakkında bilgiler sağlar.  


### <a name="os-image"></a>İşletim sistemi görüntüsü  

Configuration Manager işletim sistemi görüntüleri Windows Imaging (WıM) dosya biçiminde depolanır. Bunlar, başvuru dosya ve klasörlerinin sıkıştırılmış bir koleksiyonunu temsil ederler. Bu görüntüler, bir bilgisayarda bir işletim sistemini başarılı bir şekilde yüklemek ve yapılandırmak için gereklidir. Daha fazla bilgi için bkz. [OS görüntülerini yönetme](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Sürücü kataloğu  

Bir cihaz sürücüsünü dağıtmak için cihaz sürücüsünü içeri aktarın, etkinleştirin ve Configuration Manager istemcisinin erişebileceği bir dağıtım noktasında kullanılabilir hale getirin. Sürücü kataloğu hakkında daha fazla bilgi için bkz. [sürücüleri yönetme](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Yönetim noktası  

Yönetim noktaları, istemcilerle Configuration Manager sitesi arasında bilgi aktarır. İstemci, işletim sistemi dağıtımını gerçekleştirmek üzere görev dizisini çalıştırmak için bir yönetim noktası kullanır. Görev dizileri hakkında daha fazla bilgi için bkz. [görevleri otomatikleştirme Için planlama değerlendirmeleri](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Dağıtım noktası  

Dağıtım noktaları çoğu dağıtımda, görüntü veya sürücü paketleri gibi bir işletim sistemini dağıtmak için kullanılan verileri depolamak için kullanılır. Görev dizileri genellikle işletim sistemini dağıtmak için bir dağıtım noktasından veri alır. Dağıtım noktalarının nasıl yükleneceği ve içeriğin nasıl yönetileceği hakkında daha fazla bilgi için bkz. [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="pxe-enabled-distribution-point"></a>PXE'yi destekleyen dağıtım noktası  

PXE tarafından başlatılan dağıtımları dağıtmak için, istemcilerden gelen PXE isteklerini kabul etmek üzere bir dağıtım noktası yapılandırın. Daha fazla bilgi için bkz. [dağıtım noktası yapılandırma](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Çok noktaya yayını destekleyen dağıtım noktası  

İşletim sistemi dağıtımlarınızı çok noktaya yayın kullanarak iyileştirmek için bir dağıtım noktasını çok noktaya yayını destekleyecek şekilde yapılandırın. Daha fazla bilgi için bkz. [dağıtım noktası yapılandırma](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Durum Geçiş noktası  

Yan yana ve yenileme dağıtımlarında Kullanıcı durumu verilerini yakalayıp geri yüklediğinizde, Kullanıcı durumu verilerini başka bir bilgisayarda depolamak için bir durum geçiş noktası yapılandırın.  

Durum geçiş noktasını yapılandırma hakkında daha fazla bilgi için bkz. [Durum geçiş noktası](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

Kullanıcı durumunu yakalama ve geri yükleme hakkında daha fazla bilgi için bkz. [Kullanıcı durumunu yönetme](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Raporlama hizmetleri noktası  

İşletim sistemi dağıtımları için Configuration Manager raporlarını kullanmak için bir Raporlama noktası yükleyip yapılandırın. Daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>İşletim sistemi dağıtımları için güvenlik izinleri  

**Işletim sistemi dağıtım Yöneticisi** güvenlik rolü, değiştiremiyoruz yerleşik bir roldür. Ancak bu rolü kopyalayabilir, değişikliler yapabilir ve sonra bu değişiklikleri yeni özel güvenlik rolü olarak kaydedebilirsiniz. Doğrudan işletim sistemi dağıtımları için uygulanan izinlerden bazıları şunlardır:  

- **Önyükleme Görüntü Paketi**: Oluşturma, Silme, Değiştirme, Klasör Değiştirme, Nesne Taşıma, Okuma, Güvenlik Kapsamını Ayarlama  

- **Cihaz Sürücüleri**: Oluşturma, Silme, Değiştirme, Klasör Değiştirme, Rapor Değiştirme, Nesne Taşıma, Okuma, Rapor Çalıştırma  

- **Sürücü Paketi**: Oluşturma, Silme, Değiştirme, Klasör Değiştirme, Nesne Taşıma, Okuma, Güvenlik Kapsamını Ayarlama  

- **İşletim Sistemi Görüntüsü**: Oluşturma, Silme, Değiştirme, Klasör Değiştirme, Nesne Taşıma, Okuma, Güvenlik Kapsamını Ayarlama  

- **Işletim sistemi yükseltme paketi**: oluşturma, silme, değiştirme, klasör değiştirme, nesne taşıma, okuma, güvenlik kapsamını ayarlama  

- **Görev Dizisi Paketi**: Oluşturma, Görev Dizisi Medyası Oluşturma, Silme, Değiştirme, Klasör Değiştirme, Rapor Değiştirme, Nesne Taşıma, Okuma, Rapor Çalıştırma, Güvenlik Kapsamını Ayarlama  

Daha fazla bilgi için bkz. [özel güvenlik rolleri oluşturma](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>İşletim sistemi dağıtımları için güvenlik kapsamları  

Yönetim kullanıcılarının işletim sistemi dağıtımlarında kullanılan işletim sistemi ve önyükleme görüntüleri, sürücü paketleri ve görev dizisi paketleri gibi güvenliği sağlanabilir nesnelere erişimini sağlamak için güvenlik kapsamlarını kullanın. Daha fazla bilgi için bkz. [Güvenlik kapsamları](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Windows Dağıtım Hizmetleri  

Sürüm 1802 ve önceki sürümlerinde Windows Dağıtım Hizmetleri (WDS), PXE veya çok noktaya yayını destekleyecek şekilde yapılandırdığınız dağıtım noktalarıyla aynı sunucuda yüklü olmalıdır. WDS, sunucu işletim sistemine dahildir. PXE dağıtımlarında, WDS hizmeti PXE önyüklemesini yapan hizmettir. Dağıtım noktası yüklenip PXE için etkinleştirildiğinde, Configuration Manager WDS 'ye WDS PXE önyükleme işlevlerini kullanan bir sağlayıcı yükler.  

Sürüm 1806 ' den başlayarak, WDS olmadan bir dağıtım noktasında PXE 'yi etkinleştirebilirsiniz. Daha fazla bilgi için bkz. [dağıtım noktalarını yükleyip yapılandırma](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)bölümünde **Windows DAĞıTıM hizmeti olmadan PXE yanıtlayıcısını etkinleştirme** seçeneği.


> [!NOTE]  
>  Sunucu yeniden başlatma gerektiriyorsa, WDS yüklemesi başarısız olabilir. 


### <a name="wds-requirements"></a>WDS gereksinimleri  

-   Sunucusundaki WDS yüklemesi, yöneticinin yerel Yöneticiler grubunun bir üyesi olmasını gerektirir.  

-   WDS sunucusu, bir Active Directory etki alanının üyesi veya bir Active Directory etki alanının etki alanı denetleyicisi olmalıdır. Tüm Windows etki alanı ve orman yapılandırmaları WDS'yi destekler.  

-   Sağlayıcı uzak bir sunucuda yüklüyse, WDS 'yi site sunucusuna ve uzak sağlayıcıya yükleme.  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> WDS ve DHCP'yi aynı sunucuda bulundurmayla ilgili önemli noktalar  

Dağıtım noktasını DHCP çalıştıran bir sunucuda birlikte barındırmak istiyorsanız, aşağıdaki yapılandırma sorunlarını göz önünde bulundurun:  

-   Etkin kapsamlı bir düzgün çalışan DHCP sunucunuzun olması gerekir. WDS, bir DHCP sunucusu gerektiren PXE 'yi kullanır.  

-   WDS çalıştırmak için bir DNS sunucusu gereklidir.  

-   WDS sunucusunda aşağıdaki UDP bağlantı noktaları açık olmalıdır:  

    -   Bağlantı Noktası 67 (DHCP)  

    -   Bağlantı Noktası 69 (TFTP)  

    -   Bağlantı Noktası 4011 (PXE)  

    > [!NOTE]  
    >  Sunucuda DHCP yetkilendirmesi gerekliyse, sunucuda DHCP istemci bağlantı noktası 68 ' nin açık olması gerekir.  

-   DHCP ve WDS, 67 numaralı bağlantı noktasını gerektirir. WDS ve DHCP 'yi birlikte barındırdıysanız, DHCP 'yi veya PXE için yapılandırılmış dağıtım noktasını ayrı bir sunucuya taşıyabilirsiniz. Ya da, farklı bir bağlantı noktasını dinlemek üzere WDS sunucusunu yapılandırmak için aşağıdaki yordamı kullanabilirsiniz.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>WDS sunucusunu farklı bir bağlantı noktasında dinlemek üzere yapılandırmak için  

1.  Aşağıdaki kayıt defteri anahtarını değiştirin:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  **UseDHCPPorts** kayıt defteri değerini **0**olarak ayarlayın.  

3.  Yeni yapılandırmanın etkili olması için sunucuda aşağıdaki komutu çalıştırın:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> Sürüm 1810 ve önceki sürümlerde, aynı zamanda bir DHCP sunucusu çalıştıran sunucularda WDS olmadan PXE Yanıtlayıcı 'yı kullanmak desteklenmez.
>
> Sürüm 1902 ' den başlayarak, bir dağıtım noktasında Windows dağıtım hizmeti olmadan bir PXE Yanıtlayıcı 'yı etkinleştirdiğinizde, artık DHCP hizmetiyle aynı sunucuda olabilir. Daha fazla bilgi için bkz. [PXE isteklerini kabul etmek için en az bir dağıtım noktasını yapılandırma](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a> Desteklenen işletim sistemleri  

[İstemciler ve cihazlar için desteklenen işletim sistemlerinde](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) desteklenen istemciler olarak listelenen tüm Windows işletim sistemleri işletim sistemi dağıtımı için desteklenir.  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a> Desteklenen disk yapılandırması  

Referans ve hedef bilgisayarlardaki Configuration Manager işletim sistemi dağıtımı için desteklenen sabit disk yapılandırması bileşimleri aşağıdaki tabloda gösterilmiştir:  

|Referans bilgisayar sabit disk yapılandırması|Hedef bilgisayar sabit disk yapılandırması|  
|------------------------------------------------|--------------------------------------------------|  
|Temel disk|Temel disk|  
|Bir dinamik diskteki basit birim|Bir dinamik diskteki basit birim|  

Configuration Manager, işletim sistemi görüntüsü yakalamayı yalnızca basit birimlerle yapılandırılmış bilgisayarlardan destekler. Aşağıdaki sabit disk yapılandırmalarına yönelik destek yoktur:  

-   Dağıtılmış birimler  

-   Şeritli birimler (RAID 0)  

-   Yansıtılmış birimler (RAID 1)  

-   Eşlik birimleri (RAID 5)  

Aşağıdaki tabloda, başvuru ve hedef bilgisayarlarda Configuration Manager işletim sistemi dağıtımında desteklenmeyen ek sabit disk yapılandırması gösterilmektedir.  

|Referans bilgisayar sabit disk yapılandırması|Hedef bilgisayar sabit disk yapılandırması|  
|------------------------------------------------|--------------------------------------------------|  
|Temel disk|Dinamik disk|  



## <a name="next-steps"></a>Sonraki adımlar

- [İşletim sistemi dağıtımları için site sistemi rollerini hazırlama](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [İşletim sistemi dağıtımına hazırlanma](../get-started/prepare-for-operating-system-deployment.md)