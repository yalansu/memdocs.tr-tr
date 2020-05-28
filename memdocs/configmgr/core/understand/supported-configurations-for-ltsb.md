---
title: 'LTSB için desteklenen konfigürasyonlar '
titleSuffix: Configuration Manager
description: System Center Configuration Manager uzun vadeli bakım dalında çalışan işletim sistemlerini ve bağımlı ürünleri anlayın.
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7de7d562131f97ac21d1c394b176d3b7f4ce7747
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906446"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager uzun vadeli bakım dalı için desteklenen konfigürasyonlar

*Uygulama hedefi: System Center Configuration Manager (uzun süreli bakım dalı)*

Configuration Manager uzun süreli bakım dalı (LTSB) tarafından desteklenen işletim sistemlerini ve ürün bağımlılıklarını anlamak için bu konudaki bilgileri kullanın.
Bu veya LTSB 'e özgü konularda aksi belirtilmedikçe, 1606 sürümü Güncel Dalı için uygulanan aynı yapılandırma ve sınırlamalar LTSB için de geçerlidir.  Çakışmalar oluştuğunda, kullanmakta olduğunuz sürüm için geçerli olan bilgileri kullanın. Genellikle, LTSB, Güncel Dalı kıyasla daha sınırlıdır.

## <a name="general-statement-of-support"></a>Genel destek beyanı
Aşağıdaki ürünler ve teknolojiler bu Configuration Manager Dalı tarafından desteklenir. Ancak, bu içeriğe dahil edilmesi, ürünün bireysel destek yaşam döngüsünün ötesinde herhangi bir ürün veya sürüm için bir destek uzantısı göstermez. Destek yaşam döngüsünün ötesinde ürünlerin Configuration Manager kullanımı desteklenmez. Daha fazla bilgi için [Microsoft desteği yaşam döngüsü](https://support.microsoft.com/lifecycle) Web sitesini ziyaret edin ve Microsoft desteği yaşam döngüsü ilkesi SSS makalesini okuyun.

Ayrıca, aşağıdaki konularda listelenmeyen ürünler ve ürün sürümleri [Enterprise Mobility + Security blogda](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity)duyurulmamışsa desteklenmez.

**Gelecekteki destek Için sınırlamalar:** LTSB, gelecekteki sunucu ve istemci işletim sistemleri ve ürün bağımlılıkları için sınırlı destek içerir. LTSB 'nin platformlar listesi, yayın ömrü için düzeltildi:

**Pencerelerin**
- Yalnızca Windows için kalite ve güvenlik güncelleştirmeleri desteklenir.
- Geçerli dallar (CB), geçerli iş dalları (CBB) veya Windows 10 ' un LTSB için destek eklenmez.
- Windows Server 'ın yeni ana sürümleri için destek yoktur.

**SQL Server:**
- SQL Server için yalnızca kalite ve güvenlik güncelleştirmeleri veya hizmet paketleri gibi küçük yükseltmeler desteklenir.
- SQL Server 'ın yeni ana sürümleri için destek yoktur.  

## <a name="site-systems-and-servers"></a>Site sistemleri ve sunucuları
LTSB, site sistemleri olarak aşağıdaki Windows bilgisayarı işletim sistemlerinin kullanımını destekler.  Her işletim sistemi, [site sistemi sunucuları Için desteklenen işletim sistemlerindeki](../plan-design/configs/supported-operating-systems-for-site-system-servers.md)aynı gereksinimlere ve sınırlamalara sahiptir.  Örneğin, Windows 2012 R2 'nin sunucu çekirdeği yüklemesi x64 sürümü olmalıdır, yalnızca bir dağıtım noktasını barındırmak için desteklenir ve PXE veya çok noktaya yayını desteklemez.

**Desteklenen işletim sistemleri:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows Server 2012 Server Core yüklemesi
- Windows Server 2012 R2 sunucu çekirdeği yüklemesi

## <a name="client-management"></a>İstemci yönetimi
Aşağıdaki bölümlerde, LTSB ile yönetebileceğiniz istemci işletim sistemleri tanımlanacaktır. LTSB, desteklenen istemciler olarak yeni işletim sistemlerinin eklenmesini desteklemez.

### <a name="windows-computers"></a>Windows bilgisayarları
Aşağıdaki Windows bilgisayar işletim sistemlerini Configuration Manager dahil Configuration Manager istemci yazılımıyla yönetmek için LTSB 'yi kullanabilirsiniz. Daha fazla bilgi için bkz. [Windows bilgisayarlarına istemci dağıtma](../clients/deploy/deploy-clients-to-windows-computers.md).

**Desteklenen işletim sistemleri:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Note 1)
- Windows Server 2012 (x64): Standard, Datacenter (Note 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows Server 2012 R2 (x64) sunucu çekirdeği yüklemesi (2. nota)
- Windows Server 2012 (x64) sunucu çekirdeği yüklemesi (Note 2)

**(Note 1)** Veri merkezi sürümleri desteklenir ancak Configuration Manager için sertifikalı değildir.  
**(Note 2)** İstemci gönderme yüklemesini desteklemek için, bu işletim sistemi sürümünü çalıştıran bilgisayarın dosya ve Depolama Hizmetleri sunucu rolü için dosya sunucusu rol hizmetini çalıştırması gerekir. Windows özelliklerini bir sunucu çekirdeği bilgisayara yükleme hakkında daha fazla bilgi için bkz. sunucu [rollerini ve özellikleri sunucu çekirdeği sunucusuna yükleme](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574158(v=ws.11)).

### <a name="windows-embedded"></a>Windows Embedded
İstemci yazılımını cihaza yükleyerek, LTSB 'yi kullanarak aşağıdaki Windows Embedded cihazlarını yönetebilirsiniz.  Daha fazla bilgi için bkz. [Windows Embedded cihazlarına istemci dağıtımını planlama](../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).

**Gereksinimler ve sınırlamalar:**  

-   Tüm istemci özellikleri, yazma filtreleri etkinleştirilmemiş olan desteklenen Windows Embedded sistemlerinde desteklenir.  

-   Aşağıdakilerden birini kullanan istemciler, güç yönetimi dışındaki tüm özellikler için desteklenir:  

    -   Gelişmiş yazma filtreleri (EWF)    

    -   RAM dosya tabanlı yazma filtreleri (FBWF)    

    -   Birleşik yazma filtreleri (UWF)  

-   Uygulama Kataloğu, herhangi bir Windows Embedded cihazında desteklenmez.  

-   Windows XP tabanlı Windows Embedded cihazlarında algılanan kötü amaçlı yazılımları izleyebilmeniz için önce, Microsoft Windows WMI betik paketini katıştırılmış cihaza yüklemelisiniz. Bu paketi yüklemek için Windows Embedded hedef Tasarımcısı 'nı kullanın. *Wbemdisp. DLL* ve *Wbemdisp. *Algılanan kötü amaçlı yazılımın raporlandığından emin olmak için, TLB dosyaları var olmalı ve katıştırılmış cihazdaki%windir%\System32\WBEM klasörüne kaydedilmelidir.  

**Desteklenen işletim sistemleri:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8,1 sektör (x86, x64)    
-   Windows Ince PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded standart 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Windows CE cihazlarını, Configuration Manager dahil olan Configuration Manager mobil cihaz eski istemcisiyle yönetebilirsiniz.  

**Gereksinimler ve sınırlamalar:**  

-   Mobil aygıt istemcisi, istemciyi yüklemek için 0,78 MB depolama alanı gerektirir. Bir mobil cihaz, oturum açmak için 256 KB 'a kadar ek depolama alanı gerektirebilir.    

-   Bu mobil cihazların özellikleri platforma ve istemci türüne göre farklılık gösterir. Mobil cihaz eski istemcisi için Configuration Manager desteklediği yönetim işlevleri hakkında daha fazla bilgi için, bkz. [Configuration Manager için bir cihaz yönetimi çözümü seçme](../plan-design/choose-a-device-management-solution.md).  

**Desteklenen işletim sistemleri:**  

-   Windows CE 7,0 (ARM ve x86 işlemciler)  

**Desteklenen diller:**  
-   Çince (Basitleştirilmiş ve geleneksel)    
-   İngilizce (ABD)    
-   Fransızca (Fransa)    
-   Almanca    
-   İtalyanca    
-   Japonca  
-   Korece  
-   Portekizce (Brezilya)  
-   Rusça  
-   İspanyolca (İspanya)  

### <a name="mac-computers"></a>Mac bilgisayarlar  
 Mac için Configuration Manager istemcisiyle Mac OS X bilgisayarları yönetmek için LTSB 'yi kullanabilirsiniz.

Mac istemcisi yükleme paketi Configuration Manager medyası ile birlikte sağlanmaz. Bunu, [Microsoft Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=47719)'Nden "ek işletim sistemleri için istemciler" indirmenin bir parçası olarak indirebilirsiniz.  

Mac işletim sistemleri için destek, bu bölümde listelenenler ile sınırlıdır. Destek, Güncel Dalı için Mac istemci yükleme paketlerine gelecek bir güncelleştirme tarafından desteklenen ek işletim sistemleri içermez.

Daha fazla bilgi için bkz. [Mac 'e istemci dağıtma](../clients/deploy/deploy-clients-to-macs.md).

**Desteklenen sürümler:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Linux ve UNIX sunucuları
Linux ve UNIX için Configuration Manager istemcisiyle Linux ve UNIX sunucularını yönetmek için LTSB 'yi kullanabilirsiniz.

Linux ve UNIX istemci yükleme paketleri Configuration Manager medyayla birlikte sağlanmaz. Bunları, [Microsoft Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=47719)'Nden "ek işletim sistemleri için istemciler" indirmesi bir parçası olarak indirebilirsiniz. İstemci indirmesi, istemci yükleme paketlerine ek olarak istemcinin her bilgisayara yüklenmesini yöneten install betiğini içerir.

Linux ve UNIX işletim sistemleri için destek, bu bölümde listelenenler ile sınırlıdır. Destek, Güncel Dalı için Linux ve UNIX istemci paketlerine gelecekteki bir güncelleştirme tarafından desteklenen ek işletim sistemleri içermez.

**Gereksinimler ve sınırlamalar:**  

-   Linux ve UNIX için istemcisine yönelik işletim sistemi dosya bağımlılıklarını gözden geçirmek için bkz. [Linux ve UNIX sunucularına Istemci dağıtımı önkoşulları](../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  
-   Linux veya UNIX çalıştıran bilgisayarlarda desteklenen yönetim özelliklerine genel bakış için bkz. [UNIX ve Linux sunuculara istemci dağıtma](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  
-   Linux ve UNIX 'in desteklenen sürümleri için, listelenen sürüm tüm sonraki ikincil sürümleri içerir. Örneğin, CentOS Sürüm 6 ' nın desteklediği durumlar için bu, CentOS 6 ' nın sonraki tüm alt sürümlerini de içerir (CentOS 6,3 gibi). Benzer şekilde, destek, SUSE Linux Enterprise Server 11 SP1 gibi hizmet paketlerini kullanan bir işletim sistemi için listelendiğinde, destek bu işletim sistemi sürümü için sonraki hizmet paketlerini de içerir.
-   İstemci yükleme paketleri ve Universal Agent hakkında daha fazla bilgi için bkz. [ISTEMCILERI UNIX ve Linux sunucularına dağıtma](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).


**Desteklenen sürümler:**   
Aşağıdaki sürümler belirtilen. tar dosyası kullanılarak desteklenir.  
### <a name="aix"></a>AIX  

|Sürüm|Dosya|  
|-|-|  
|Sürüm 5,3 (güç)|CCM-Aix53ppc. &lt; Build \> . tar|  
|Sürüm 6,1 (güç)|CCM-Aix61ppc. &lt; Build \> . tar|  
|Sürüm 7,1 (güç)|CCM-Aix71ppc. &lt; Build \> . tar|  

### <a name="centos"></a>CentOS  

|Sürüm|Dosya|  
|-|-|  
|Sürüm 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="debian"></a>Debian  

|Sürüm|Dosya|    
|-|-|  
|Sürüm 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 6x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 7 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 7 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 8 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 8 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="hp-ux"></a>HP-UX  

|Sürüm|Dosya|  
|-|-|  
|Sürüm 11iv2 ıA64|CCM-HpuxB. 11.23 i64. &lt; Build \> . tar|  
|Sürüm 11iv2 PA-RıSC|CCM-HpuxB. 11.23 PA. &lt; Build \> . tar|  
|Sürüm 11iv3 ıA64|CCM-HpuxB. 11.31 i64. &lt; Build \> . tar|  
|Sürüm 11iv3 PA-RıSC|CCM-HpuxB. 11.31 PA. &lt; Build \> . tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Sürüm|Dosya|    
|-|-|  
|Sürüm 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Sürüm|Dosya|  
|-|-|  
|Sürüm 4 x86|CCM-RHEL4x86. &lt; Build \> . tar|  
|Sürüm 4 x64|CCM-RHEL4x64. &lt; Build \> . tar|  
|Sürüm 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="solaris"></a>Solaris  

|Sürüm|Dosya|   
|-|-|  
|Sürüm 9 SPARC|CCM-Sol9sparc. &lt; Build \> . tar|  
|Sürüm 10 x86|CCM-Sol10x86. &lt; Build \> . tar|  
|Sürüm 10 SPARC|CCM-Sol10sparc. &lt; Build \> . tar|  
|Sürüm 11 x86|CCM-Sol11x86. &lt; Build \> . tar|  
|Sürüm 11 SPARC|CCM-Sol11sparc. &lt; Build \> . tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Sürüm|Dosya|  
|-|-|  
|Sürüm 9 x86|CCM-SLES9x86. &lt; Build \> . tar|  
|Sürüm 10 SP1 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 10 SP1 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 11 SP1 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 11 SP1 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 12 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="ubuntu"></a>Ubuntu  

|Sürüm|Dosya|    
|-|-|  
|Sürüm 10,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 10,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 12,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 12,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Sürüm 14,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Sürüm 14,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="exchange-server-connector"></a>Exchange Server bağlayıcısı
 LTSB, istemci yazılımı yüklemeden Exchange Server örneğinize bağlanan cihazların sınırlı yönetimini destekler. Daha fazla bilgi için bkz. [Configuration Manager ve Exchange ile mobil cihazları yönetme](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

 **Gereksinimler ve sınırlamalar:**  

-   Configuration Manager, mobil cihazlar için sınırlı yönetim sunar. Exchange Server veya Exchange Online çalıştıran bir sunucuya bağlanan Exchange Active Sync (EAS) özellikli cihazlarda Exchange Server bağlayıcısını kullandığınızda sınırlı yönetim kullanılabilir.  

-   Exchange Server bağlayıcısının yönettiği mobil cihazlar için Configuration Manager desteklediği yönetim işlevleri hakkında daha fazla bilgi için, bkz. [Configuration Manager için bir cihaz yönetimi çözümü seçme](../plan-design/choose-a-device-management-solution.md).  

**Desteklenen Exchange Server sürümleri:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> LTSB, Exchange Online (Office 365) gibi bir çevrimiçi hizmetle bağlanan cihazların yönetimini desteklemez.


## <a name="configuration-manager-console"></a>Configuration Manager konsolu
LTSB, Configuration Manager konsolunu çalıştırmak için aşağıdaki işletim sistemlerini destekler. Konsolunu barındıran her bilgisayarda, en az .NET Framework 4,6 gerektiren Windows 10 hariç en düşük .NET Framework sürümü 4.5.2 olmalıdır.

**Desteklenen işletim sistemleri:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Site veritabanı ve Raporlama noktası için desteklenen SQL Server sürümleri
LTSB, site veritabanını ve raporlama noktasını barındırmak için SQL Server aşağıdaki sürümlerini destekler. Desteklenen her sürüm için, Güncel Dalı için [SQL Server sürümleri Için destek](../plan-design/configs/support-for-sql-server-versions.md) içinde görüntülenen aynı yapılandırma gereksinimleri ve sınırlamaları LTSB için geçerlidir.  Buna bir SQL Server kümesinin veya SQL Server AlwaysOn kullanılabilirlik grubunun kullanımı dahildir.  

**Desteklenen sürümler:**

- SQL Server 2016: Standart, kurumsal
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Active Directory etki alanları için destek
Tüm LTSB site sistemleri desteklenen bir Windows Active Directory etki alanının üyesi olmalıdır. Active Directory etki alanlarına yönelik destek, [Active Directory etki alanları Için destek](../plan-design/configs/support-for-active-directory-domains.md)bölümünde görünenlerle aynı gereksinimlere ve sınırlamalara sahiptir, ancak aşağıdaki etki alanı işlev düzeyleriyle sınırlıdır:

**Desteklenen düzeyler:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Uzun süreli bakım dalı için uygulanan ek destek konuları
Aşağıdaki Güncel Dalı konulardaki bilgiler LTSB için geçerlidir:
- [Boyut ve ölçek sayıları](../plan-design/configs/size-and-scale-numbers.md)
- [Site ve site sistemi önkoşulları](../plan-design/configs/site-and-site-system-prerequisites.md)
- [Yüksek kullanılabilirlik seçenekleri](../servers/deploy/configure/high-availability-options.md)
- [Önerilen donanım](../plan-design/configs/recommended-hardware.md)
- [Windows özellikleri ve ağları için destek](../plan-design/configs/support-for-windows-features-and-networks.md)
- [Sanallaştırma ortamları desteği](../plan-design/configs/support-for-virtualization-environments.md)
