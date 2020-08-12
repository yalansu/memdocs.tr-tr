---
title: Desteklenen istemciler ve cihazlar
titleSuffix: Configuration Manager
description: Hangi işletim sistemi sürümlerinin istemciler ve cihazlar için Configuration Manager destekleyeceğinizi öğrenin.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 497a43fe6647f1dc2787f16a76f45ddd26d24796
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128857"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Configuration Manager için istemciler ve cihazlar için desteklenen işletim sistemi sürümleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Windows ve macOS bilgisayarlarına istemci yazılımı yüklemeyi destekler.  

## <a name="general-requirements-and-limitations"></a>Genel gereksinimler ve sınırlamalar

Tüm istemciler için aşağıdaki gereksinimleri ve sınırlamaları gözden geçirin:

- Herhangi bir Configuration Manager hizmeti için başlangıç türü veya **oturum açma** ayarlarını değiştirme desteklenmez. Bu değişiklik, önemli hizmetlerin düzgün çalışmasını engelleyebilir.

## <a name="windows-computers"></a>Windows bilgisayarları  

Aşağıdaki Windows işletim sistemi sürümlerini yönetmek için Configuration Manager bulunan istemcisini kullanın. Daha fazla bilgi için bkz. [Windows bilgisayarlarına istemci dağıtma](../../clients/deploy/deploy-clients-to-windows-computers.md).  

### <a name="supported-client-os-versions"></a>Desteklenen istemci işletim sistemi sürümleri

- **Windows 10**  

    Daha ayrıntılı bilgi için bkz. [Windows 10 Için destek](support-for-windows-10.md).  

- **Windows 8.1** (x86, x64): Professional, Enterprise

#### <a name="windows-virtual-desktop"></a>Windows Sanal Masaüstü

<!--3556025-->
[Windows sanal masaüstü](https://docs.microsoft.com/azure/virtual-desktop/) , Microsoft Azure üzerinde çalışan bir masaüstü ve uygulama sanallaştırma hizmetidir. Sürüm 1906 ' den başlayarak, Azure 'da Windows çalıştıran bu sanal cihazları yönetmek için Configuration Manager kullanın.

Terminal sunucusuna benzer şekilde, bu sanal cihazlardan bazıları çoklu eşzamanlı etkin kullanıcı oturumlarına izin verir. İstemci performansına yardımcı olmak için Configuration Manager artık bu çoklu kullanıcı oturumlarına izin veren her cihazda kullanıcı ilkelerini devre dışı bırakır. Kullanıcı ilkelerini etkinleştirseniz bile, istemci, Windows 10 Enterprise çoklu oturum ve Terminal Server 'lar dahil bu cihazlarda varsayılan olarak devre dışı bırakır.

İstemci, yeni bir yükleme sırasında bu cihaz türünü algıladığında yalnızca kullanıcı ilkesini devre dışı bırakır. Bu sürüme güncelleştirmeniz gereken mevcut bir istemci için, önceki davranış devam ettirir. Mevcut bir cihazda, cihazın birden çok kullanıcı oturumuna izin verdiğini algıladığında bile Kullanıcı ilkesi ayarını yapılandırır.

Bu senaryoda Kullanıcı ilkesine ihtiyacınız varsa ve olası performans etkisini kabul ediyorsanız, kullanıcı ilkesini etkinleştirmek için aşağıdaki yöntemlerden birini kullanın:

- Sürüm 1910 ve sonrasında [istemci ayarları](../../clients/deploy/configure-client-settings.md)' nı kullanın. **Istemci ilkesi** grubunda, aşağıdaki ayarı yapılandırın: **birden çok Kullanıcı oturumu Için kullanıcı ilkesini etkinleştirin**.<!-- 4737447 -->

- Sürüm 1906 ' de, [SMS_PolicyAgentConfig sunucusu WMI sınıfıyla](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md)Configuration Manager SDK 'sını kullanın. Yeni `PolicyEnableUserPolicyOnTS` özelliğini olarak ayarlayın `true` .

> [!Note]  
> Windows 10 Enterprise çoklu oturum çalıştıran bir istemciyle birlikte ortak yönetimi kullanamazsınız. <!-- SCCMDocs-pr#3950 -->

Sürüm 2006 ' den başlayarak, **Windows 10 Enterprise çoklu oturum** platformu, gereksinim kuralları veya uygulanabilirlik listeleri olan nesnelerde desteklenen işletim sistemi sürümleri listesinde bulunur.<!--6527576-->

> [!NOTE]
> En üst düzey **Windows 10** platformunu daha önce seçtiyseniz, bu eylem tüm alt platformları otomatik olarak seçti. Bu yeni platform otomatik olarak seçilmedi. **Windows 10 Enterprise çoklu oturum**eklemek istiyorsanız, listeden el ile seçin.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Sanallaştırma ortamları desteği](support-for-virtualization-environments.md)
- [Bir sanal masaüstü altyapısında (VDı) Configuration Manager istemcilerini yönetme](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)

### <a name="supported-server-os-versions"></a>Desteklenen sunucu işletim sistemi sürümleri

- **Windows Server 2019**: Standard, Datacenter <sup> [Note 1](#bkmk_note1)</sup>  
    (Configuration Manager sürüm 1806 ' den itibaren.)

- **Windows Server 2016**: Standard, Datacenter <sup> [Note 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: çalışma grubu, standart  

- **Windows Server 2012 R2** (x64): Standard, Datacenter <sup> [Note 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Datacenter <sup> [Note 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Sunucu Çekirdeği

Aşağıdaki sürümler özellikle işletim sisteminin Sunucu Çekirdeği yüklemesine başvurur. <sup>[3. nota](#bkmk_note3)</sup>  

Windows Server yarı yıllık kanal sürümleri, Windows Server, sürüm 1809 gibi sunucu çekirdeği yüklemelerdir. Configuration Manager istemci olarak, ilişkili Windows 10 yarı yıllık kanal sürümü ile aynı şekilde desteklenirler. Daha fazla bilgi için bkz. [Windows 10 Için destek](support-for-windows-10.md).

- **Windows Server 2019** (x64) <sup> [Note 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup> [Note 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup> [Note 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup> [Note 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a>1. nota

Configuration Manager testleri ve Windows Server Datacenter sürümlerini destekler, ancak Windows Server için resmi sertifikalı değildir. Configuration Manager Düzeltme desteği Windows Server Datacenter Edition 'a özgü sorunlar için sunulmamaktadır. Windows Server sertifika programı hakkında daha fazla bilgi için bkz. [Windows Server Kataloğu](https://www.windowsservercatalog.com/).

#### <a name="note-2"></a><a name="bkmk_note2"></a>2. nota

[Client Push yüklemesini](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)desteklemek için dosya ve Depolama Hizmetleri sunucu rolünün dosya sunucusu hizmetini ekleyin. Sunucu Çekirdeği üzerine Windows özellikleri yükleme hakkında daha fazla bilgi için bkz. [Windows PowerShell cmdlet 'lerini kullanarak rolleri, rol hizmetlerini ve özellikleri yükleme](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets).  

#### <a name="note-3"></a><a name="bkmk_note3"></a>3. nota

Yeni Yazılım Merkezi uygulaması herhangi bir Windows Server Core sürümünde desteklenmez.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Windows Embedded bilgisayarlar  

Cihaza Configuration Manager istemcisini yükleyerek Windows Embedded cihazlarını yönetin. Daha fazla bilgi için bkz. [Windows Embedded cihazlarına istemci dağıtımını planlama](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

### <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar

- Tüm istemci özellikleri, yazma filtreleri etkinleştirilmemiş Windows Embedded sistemlerinde desteklenir.  

- Aşağıdakilerden birini kullanan istemciler, güç yönetimi dışındaki tüm özellikler için desteklenir:  

  - Gelişmiş yazma filtreleri (EWF)

  - RAM dosya tabanlı yazma filtreleri (FBWF)

  - Birleşik yazma filtreleri (UWF)  

- Uygulama Kataloğu, herhangi bir Windows Embedded aygıtı için desteklenmez.  

### <a name="supported-os-versions"></a>Desteklenen işletim sistemi sürümleri  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Bu sürüm, uzun süreli bakım kanalını (LTSC) içerir. Daha fazla bilgi için bkz. [Windows 10 IoT Enterprise 'A genel bakış](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8,1 sektör** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Ince PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 SP1** (x86, x64)

## <a name="windows-ce-computers"></a>Windows CE bilgisayarlar

Configuration Manager bulunan Configuration Manager mobil cihaz eski istemcisiyle Windows CE cihazları yönetin.  

### <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar

- Mobil cihaz istemcisi, yükleme için 0,78 MB depolama alanı gerektirir. Oturum açma, 256 KB 'a kadar ek depolama alanı gerektirebilir.

- Bu mobil cihazların özellikleri platforma ve istemci türüne göre farklılık gösterir. Hangi yönetim işlevlerinin desteklendiği hakkında bilgi için bkz. [cihaz yönetimi çözümü seçme](../choose-a-device-management-solution.md).  

### <a name="supported-os-versions"></a>Desteklenen işletim sistemi sürümleri

- Windows CE 7,0 (ARM ve x86 işlemciler)  

    > [!IMPORTANT]
    > Configuration Manager sürüm 2006, istemci olarak Windows CE 7,0 desteğini bırakır. [Sürüm 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated)ile kullanımdan kaldırma duyurulmuştur.

#### <a name="supported-languages-include"></a>Desteklenen diller şunlardır

- Çince (Basitleştirilmiş ve geleneksel)

- İngilizce (ABD)

- Fransızca (Fransa)

- Almanca

- İtalyanca

- Japonca  

- Korece  

- Portekizce (Brezilya)  

- Rusça  

- İspanyolca (İspanya)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Genişletilmiş güvenlik güncelleştirmeleri ve Configuration Manager

[Genişletilmiş güvenlik güncelleştirmeleri (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) programı, destek sonunun ötesinde belirli eski Microsoft ürünlerini çalıştırması gereken müşteriler için son çare bir seçenektir. Örneğin, Windows 7. Ürünün genişletilmiş destek tarihine kadar olan en fazla üç yıl sonra kritik ve/veya önemli güvenlik güncelleştirmelerini ( [Microsoft Güvenlik Yanıt Merkezi (MSRC)](https://www.microsoft.com/msrc)tarafından tanımlandığı şekilde) içerir.

Destek yaşam döngüsünün ötesinde ürünlerin Configuration Manager kullanımı desteklenmez. Bu, ESU programının kapsamında kapsanan tüm ürünleri içerir. ESU programı altında yayınlanan güvenlik güncelleştirmeleri Windows Server Update Services (WSUS) hizmetine yayımlanacak. Bu güncelleştirmeler Configuration Manager konsolunda görünür. ESU programının kapsamında yer alan ürünler Configuration Manager ile kullanım için artık desteklenirken, [Configuration Manager geçerli dalın en son yayınlanan sürümü](../../servers/manage/updates.md#version-details) program altında Yayınlanan Windows güvenlik güncelleştirmelerini dağıtmak ve yüklemek için kullanılabilir. Windows 7 çalıştıran cihazlara Windows 10 dağıtmak için en son yayınlanan sürüm de kullanılabilir.

Windows yazılım güncelleştirme yönetimi veya işletim sistemi dağıtımıyla ilgili olmayan istemci yönetimi özellikleri artık ESU programının kapsamında yer alan işletim sistemlerinde sınanmayacak ve çalışmaya devam edeceğini garanti etmeyiz. İstemci yönetimi desteğini almak için en kısa sürede işletim sistemlerinin güncel bir sürümüne yükseltilmesi veya geçirilmesi önerilir.

## <a name="mac-computers"></a>Mac bilgisayarlar  

MacOS için Configuration Manager istemcisiyle Apple Mac bilgisayarlarını yönetin.  

MacOS istemci yükleme paketi Configuration Manager medyayla birlikte sağlanmaz. Microsoft Download Center 'dan indirin, [Microsoft uç nokta Configuration Manager-macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850).  

Daha fazla bilgi için bkz. [Mac 'e istemci dağıtma](../../clients/deploy/deploy-clients-to-macs.md).  

### <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar

- Kök dışında bir hesap altındaki bilgisayarlara macOS için Configuration Manager istemcisini yüklemek veya çalıştırmak desteklenmez. Bunun yapılması, önemli hizmetlerin düzgün çalışmasını engelleyebilir.  

### <a name="supported-versions"></a>Desteklenen sürümler

- **MacOS Catalina (10,15)** (Configuration Manager site sürümü 1910 veya üzeri ve MacOS sürüm 5.0.8742.1000 veya üzeri için istemci Configuration Manager gerekir)

- **macOS Mojave (10,14)**

- **macOS High Sierra (10,13)**

## <a name="linux-and-unix-servers"></a>Linux ve UNIX sunucuları  

> [!Important]  
> Configuration Manager sürüm 1902, Linux ve UNIX için istemci olarak desteği bırakır. [Sürüm 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support)ile kullanımdan kaldırma duyurulmuştur. Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

Linux ve UNIX istemci yükleme paketleri Configuration Manager medyayla birlikte sağlanmaz. **Ek Işletim sistemleri Için Istemcileri** [Microsoft İndirme Merkezi](https://www.microsoft.com/download/details.aspx?id=47719)' nden indirin. İstemci indirmesi, istemci yükleme paketlerine ek olarak, her bilgisayarda istemcinin yüklenmesini yöneten betiği de içerir.  

### <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar

- Linux ve UNIX istemcisi için işletim sistemi dosya bağımlılıklarını gözden geçirmek için bkz. [Linux ve UNIX sunucularına istemci dağıtımı önkoşulları](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

- Linux veya UNIX için desteklenen yönetim özelliklerine genel bakış için bkz. [UNIX ve Linux sunuculara istemci dağıtma](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

- Linux ve UNIX 'in desteklenen sürümleri için, listelenen sürüm tüm sonraki ikincil sürümleri içerir. Örneğin, CentOS Sürüm 6, CentOS 6,3 ' i içerir. Benzer şekilde, hizmet paketlerini kullanan bir işletim sistemi (örneğin, SUSE Linux Enterprise Server 11 SP1) için destek, bu işletim sistemi sürümü için sonraki hizmet paketlerini içerir.  

- İstemci yükleme paketleri ve Universal Agent hakkında daha fazla bilgi için bkz. [ISTEMCILERI UNIX ve Linux sunucularına dağıtma](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

### <a name="supported-versions"></a>Desteklenen sürümler

Aşağıdaki sürümler belirtilen. tar dosyası kullanılarak desteklenir.  

#### <a name="aix"></a>AIX  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 6,1 (güç)|CCM-Aix61ppc. &lt; Build \> . tar|  
|Sürüm 7,1 (güç)|CCM-Aix71ppc. &lt; Build \> . tar|  

#### <a name="centos"></a>CentOS  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="debian"></a>Debian  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 7 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 7 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 8 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 8 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="hp-ux"></a>HP-UX  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 11iv3 ıA64|CCM-HpuxB. 11.31 i64. &lt; Build \> . tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="solaris"></a>Solaris  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 10 x86|CCM-Sol10x86. &lt; Build \> . tar|  
|Sürüm 10 SPARC|CCM-Sol10sparc. &lt; Build \> . tar|  
|Sürüm 11 x86|CCM-Sol11x86. &lt; Build \> . tar|  
|Sürüm 11 SPARC|CCM-Sol11sparc. &lt; Build \> . tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 10 SP1 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 10 SP1 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 11 SP1 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 11 SP1 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 12 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Sürüm|IK dosyası|  
|-|-|  
|Sürüm 10,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 10,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 12,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 12,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 14,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 14,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 16,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 16,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a>Şirket içi MDM

Configuration Manager, şirket içi mobil cihazları istemci yazılımı yüklemeden yönetmek için yerleşik yeteneklere sahiptir. Daha fazla bilgi için bkz. [Şirket içi altyapıyla mobil cihazları yönetme](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="supported-operating-systems"></a>Desteklenen işletim sistemleri

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Bu sürüm, uzun süreli bakım kanalını (LTSC) içerir. Daha fazla bilgi için bkz. [Windows 10 IoT Enterprise 'A genel bakış](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Surface Hub için Windows 10 ekibi**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!IMPORTANT]
    > Configuration Manager sürüm 2006, Windows 10 Mobile ve Windows 10 Mobile Enterprise 'ın istemci olarak desteğini bırakır. [Sürüm 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated)ile kullanımdan kaldırma duyurulmuştur.

## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a>Exchange Server Bağlayıcısı  

Configuration Manager, Configuration Manager istemcisini yüklemeden Exchange Server 'a bağlanan cihazların sınırlı yönetimini destekler. Daha fazla bilgi için bkz. [Configuration Manager ve Exchange ile mobil cihazları yönetme](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="supported-versions-of-exchange-server"></a>Desteklenen Exchange Server sürümleri

- **Exchange Online (Office 365)**: Bu sürüm, Iş üretkenliği çevrimiçi standart paketini içerir  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange server 2010 SP1** veya **Exchange Server 2010 SP2**
