---
title: Konsolu yükler
titleSuffix: Configuration Manager
description: Bir merkezi yönetim sitesine veya birincil siteye bağlanmak için Configuration Manager konsolunu yükler.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718241"
---
# <a name="install-the-configuration-manager-console"></a>Configuration Manager konsolunu yüklerken

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yöneticiler, Configuration Manager ortamını yönetmek için Configuration Manager konsolunu kullanır. Her bir Configuration Manager konsolu bir merkezi yönetim sitesine (CAS) veya bir birincil siteye bağlanabilir. Configuration Manager konsolunu ikincil bir siteye bağlanamazsınız.

Configuration Manager konsolu, her zaman CA 'LAR veya birincil bir site için site sunucusuna yüklenir. Konsolu site sunucusu yüklemesinden ayrı olarak yüklemek için tek başına yükleyiciyi çalıştırın.  



## <a name="prerequisites"></a>Önkoşullar

- Konsolun hedef bilgisayarda yerel **yönetici** haklarınız vardır.  

- Configuration Manager konsolu yükleme dosyalarının konumu için **okuma** izinleriniz vardır.  



## <a name="source-paths"></a>Kaynak yolları

Hangi kaynak yolunun kullanılacağını belirleyin:  

- Site sunucusundaki ConsoleSetup klasörü:`<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Bir site sunucusu yüklediğinizde, konsol yükleme dosyalarını ve site için desteklenen dil paketlerini **Tools\consolesetup** alt klasörüne kopyalar. İsteğe bağlı olarak, yüklemeyi başlatmak için **ConsoleSetup** klasörünü alternatif bir konuma kopyalayabilirsiniz. Siteyi güncelleştirdiğinizde, her zaman kendi yerel sürümünü güncel tutar.  

- Yükleme medyası Configuration Manager:`<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Configuration Manager konsolunun yükleme medyasından yüklenmesi daima Ingilizce sürümü yüklenir. Bu davranış, site sunucusu farklı dilleri desteklediğinden veya hedef bilgisayarın işletim sisteminin farklı bir dile ayarlanmış olması durumunda bile gerçekleşir.  

Mümkün olduğunda, konsol yükleyicisini kaynak medya yerine **ConsoleSetup** klasöründen başlatın.

> [!Important]  
> Konsolu **CD 'yi kullanarak yüklemeyin. En son** kaynak dosyaları. Bu, desteklenmeyen bir senaryodur ve konsol yüklemesinde sorun oluşmasına neden olabilir. Daha fazla bilgi için [CD 'ye bakın. En son klasör](../../manage/the-cd.latest-folder.md#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Konsolunu başka bilgisayarlara yüklemek için bir paket oluşturursanız, paketin aşağıdaki dosyaları içerdiğinden emin olun:<!--3612513-->

- ConsoleSetup. exe
- AdminConsole.msi
- ConfigMgr. AC_Extension. i386. cab (sürüm 1902 ' den başlayarak)
- ConfigMgr. AC_Extension. AMD64. cab (sürüm 1902 ' den başlayarak)



## <a name="use-the-setup-wizard"></a>Kurulum Sihirbazı’nı kullanma  

1. Kaynak yoluna gidin ve **ConsoleSetup. exe**dosyasını açın.  

    > [!IMPORTANT]  
    > Konsolu her zaman **ConsoleSetup. exe**' yi kullanarak yükleme. AdminConsole. msi ' yi çalıştırarak Configuration Manager konsolunu yükleyebilseniz de, bu yöntem önkoşulları veya bağımlılık denetimlerini çalıştırmaz. Yükleme doğru yüklenmeyebilir.  

2. Sihirbazda, **İleri**' yi seçin.  

3. **Site sunucusu** sayfasında, Configuration Manager konsolunun bağlandığı site sunucusunun tam etki alanı adını (FQDN) girin.  

4. **Yükleme klasörü** sayfasında, Configuration Manager konsolunun yükleme klasörünü girin. Klasör yolu, sondaki boşlukları veya Unicode karakterlerini içeremez.  

5. **Müşteri deneyimini geliştirme programı** sayfasında, MÜŞTERI DENEYIMINI GELIŞTIRME programı (CEIP) katılıp katılmayacağını seçin.  

    > [!Note]  
    > Configuration Manager sürüm 1802 ' den başlayarak CEIP özelliği üründen kaldırılır.

6. **Yüklemeye hazırlanma** sayfasında, **yükler**' i seçin.  



## <a name="install-from-a-command-prompt"></a>Komut isteminden yüklemesi  

> [!TIP]  
> Configuration Manager konsolunu bir komut isteminden yüklemek daima Ingilizce sürümü yüklenir. Bu davranış, hedef bilgisayarın işletim sistemi farklı bir dile ayarlanmış olsa bile oluşur. Configuration Manager konsolunu Ingilizce dışındaki bir dilde yüklemek için [Kurulum Sihirbazı 'nı kullanın](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>ConsoleSetup. exe komut satırı seçenekleri

#### <a name="q"></a>/q

Configuration Manager konsolunu katılımsız olarak kurar. Bu seçeneği kullandığınızda **Enablesqm**, **Targetı**ve **defaultsiteservername** seçenekleri gereklidir.

#### <a name="uninstall"></a>/uninstall

Configuration Manager konsolunu kaldırır. Bu seçeneği ilk olarak **/q** seçeneğiyle kullandığınızda belirtin.

#### <a name="langpackdir"></a>LangPackDir

Dil dosyalarını içeren klasörün yolunu belirtir. Dil dosyalarını indirmek için **Kurulum Yükleyici** 'yi kullanabilirsiniz. Bu seçeneği kullanmazsanız, Kurulum geçerli klasörde dil klasörünü arar. Dil klasörü bulunamazsa, kurulum yalnızca Ingilizce yüklemeye devam eder. Daha fazla bilgi için bkz. [Kurulum Yükleyici](setup-downloader.md).

#### <a name="targetdir"></a>Dır

Configuration Manager konsolunun yükleneceği yükleme klasörünü belirtir. Bu seçenek, **/q** seçeneğini kullandığınızda gereklidir.

#### <a name="enablesqm"></a>EnableSQM

Müşteri Deneyimini Geliştirme Programı (CEIP) öğesine katılıp katılmayacağını belirtir. CEIP 'e katılması için **1** değerini ve programa katılmayan **0** değerini kullanın. Bu seçenek, **/q** seçeneğini kullandığınızda gereklidir.

> [!Important]  
> Configuration Manager sürüm 1802 ' den başlayarak CEIP özelliği üründen kaldırılır. Parametresinin kullanılması yüklemenin başarısız olmasına neden olur.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Konsolun açıldığı zaman bağlanacağı site sunucusunun FQDN 'sini belirtir. Bu seçenek, **/q** seçeneğini kullandığınızda gereklidir.


### <a name="examples"></a>Örnekler

> [!Important]  
> Sürüm 1802 ve üzeri için **Enablesqm** parametresini eklemeyin

#### <a name="silent-install"></a>Sessiz yükleme

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Dil paketleriyle sessiz yüklemesi

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Sessiz kaldırma

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Ayrıca bkz.

Yönetici, Kullanıcı hesaplarına atanan izinlere göre konsolundaki nesneleri görür. Daha fazla bilgi için bkz. [rol tabanlı yönetimin temelleri](../../../understand/fundamentals-of-role-based-administration.md).

Configuration Manager konsoluna gidilme temelleri hakkında daha fazla bilgi için, bkz. [konsolunu kullanma](../../manage/admin-console.md).
