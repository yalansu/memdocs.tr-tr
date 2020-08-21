---
title: Düzeltme yükleyicisi
titleSuffix: Configuration Manager
description: Configuration Manager için düzeltme yükleyicisi aracılığıyla güncelleştirmelerin ne zaman ve nasıl yükleneceğini öğrenin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c5cc09b7c2723a5dbdd1030cb0053ae75b1ff22
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699475"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-configuration-manager"></a>Configuration Manager güncelleştirmelerini yüklemek için düzeltme yükleyicisini kullanın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için bazı güncelleştirmeler, Microsoft bulut hizmetinde bulunmaz ve yalnızca bant dışından edinilir. Buna örnek olarak belirli bir soruna yönelik sınırlı bir düzeltme sürümü gösterilebilir.   
Microsoft 'tan aldığınız bir güncelleştirmeyi (veya düzeltmeyi) kurmanız gerektiğinde ve bu güncelleştirmenin dosya adı **. exe** ( **update.exe**değil) ile bitiyorsa, güncelleştirmeyi doğrudan Configuration Manager site sunucusuna yüklemek için bu düzeltme indirmesinde yer alan düzeltme yükleyicisini kullanırsınız.  

Düzeltme dosyasında **.update.exe** dosya uzantısı varsa, [düzeltmeleri Configuration Manager almak Için güncelleştirme kayıt aracı 'nı kullanma](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)bölümüne bakın.  

> [!NOTE]  
> Bu konu, Configuration Manager güncelleştiren düzeltmelerin nasıl yükleneceğine ilişkin genel yönergeler sağlar. Belirli bir güncelleştirme hakkındaki ayrıntılar için Microsoft Destek'te ilgili Bilgi Bankası (BB) makalesine başvurun.  

##  <a name="overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a> Configuration Manager düzeltmelere genel bakış  
Configuration Manager düzeltmeler, SQL Server gibi diğer Microsoft ürünleriyle benzerdir, tek bir düzeltme veya bir paket (bir düzeltme toplaması) içerir ve bir Microsoft Bilgi Bankası makalesinde açıklanır.  

Tek tek güncelleştirmeler, belirli bir Configuration Manager sürümü için tek bir odaklanmış güncelleştirme içerir.  
Güncelleştirme paketleri, belirli bir Configuration Manager sürümü için birden çok güncelleştirme içerir.  
Bir güncelleştirme bir pakete dahilse, bu paketten ayrı ayrı güncelleştirmeler yükleyemezsiniz.  

Güncelleştirmeleri ek bilgisayarlara yüklemek için dağıtımlar oluşturmayı planlıyorsanız, güncelleştirme paketini merkezi yönetim site sunucusuna veya birincil site sunucusuna yüklemeniz gerekir.  

Güncelleştirme paketini çalıştırdığınızda aşağıdakiler gerçekleşir:  

- Güncelleştirme paketindeki her bir geçerli bileşenin güncelleştirme dosyaları ayıklanır.  

- Güncelleştirmeler ile güncelleştirmelere yönelik dağıtım seçeneklerini yapılandırma işleminde size rehberlik eden bir sihirbaz başlatılır.  

- Bu sihirbazı tamamladığınızda, site sunucusu için geçerli paketteki güncelleştirmeler site sunucusuna yüklenir.  

Sihirbaz aynı zamanda güncelleştirmeleri ek bilgisayarlara yüklemekte kullanabileceğiniz dağıtımları da oluşturur. Güncelleştirmeleri, bir yazılım dağıtım paketi veya Microsoft System Center Updates Publisher 2011 gibi desteklenen bir dağıtım yöntemini kullanarak ek bilgisayarlara dağıtabilirsiniz.  

Sihirbaz çalıştığında, site sunucusunda Updates Publisher 2011 ile kullanmak üzere bir **.cab** dosyası oluşturur. İsteğe bağlı olarak, sihirbazı yazılım dağıtımı için bir veya daha fazla paket oluşturacak şekilde yapılandırabilirsiniz. Bu dağıtımları istemciler veya Configuration Manager konsolu gibi bileşenlere güncelleştirmeleri yüklemek için kullanabilirsiniz. Güncelleştirmeleri, Configuration Manager istemcisini çalıştırmayan bilgisayarlara da el ile yükleyebilirsiniz.  

Configuration Manager ' deki aşağıdaki üç grup güncelleştirilemeyebilir:  

- Şunları içeren Configuration Manager sunucu rolleri:  

  - Merkezi yönetim sitesi  

  - Birincil site  

  - İkincil site  

  - Uzak SMS Sağlayıcısı  

- Configuration Manager konsolu  

- Configuration Manager istemcisi  

> [!NOTE]  
> Site **sistem rolleri Için güncelleştirmeler** (site veritabanı ve bulut tabanlı dağıtım noktaları için güncelleştirmeler dahil), site Bileşen Yöneticisi tarafından site sunucuları ve Hizmetleri güncelleştirmesinin bir parçası olarak yüklenir.  
>   
> Ancak, güncelleştirme çekme dağıtım noktalarına, site Bileşen Yöneticisi yerine dağıtım Yöneticisi tarafından hizmet verilir.  

Configuration Manager her güncelleştirme paketi, güncelleştirmeyi Configuration Manager geçerli bileşenlerine yüklemek için gerekli dosyaları içeren kendi kendine ayıklanabilen. exe dosyasıdır (SFX). SFX dosyası genellikle aşağıdaki dosyaları içerebilir:  

|Dosya|Ayrıntılar|  
|----------|-------------|  
|&lt;Ürün sürümü \> -QFE-KB &lt; KB Makale No \> - &lt; Platform \> - &lt; Language \> . exe|Bu, güncelleştirme dosyasıdır. Bu dosyanın komut satırı Updatesetup.exe tarafından yönetilir.<br /><br /> Örnek:<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|Bu .msi sarmalayıcı, güncelleştirme paketinin yüklemesini yönetir.<br /><br /> Güncelleştirmeyi çalıştırdığınızda, Updatesetup.exe çalıştığı bilgisayarın görüntüleme dilini saptar. Güncelleştirme için kullanıcı arayüzü varsayılan olarak İngilizce'dir Ancak, görüntüleme dili desteklendiğinde, kullanıcı arayüzü bilgisayarın yerel dilini görüntüler.|  
|License_&lt;language\>.rtf|Uygun olduğunda her güncelleştirme desteklenen diller için bir veya daha çok lisans dosyası içerir.|  
|&lt;Ürün&güncelleştirme türü>- &lt; ürün sürümü \> - &lt; KB Makale No \> - &lt; Platform \> . msp|Güncelleştirme, Configuration Manager konsolu veya istemcileri için geçerli olduğunda, güncelleştirme paketi ayrı Windows Installer Patch (. msp) dosyalarını içerir.<br /><br /> Örnek:<br /><br /> **Configuration Manager konsol güncelleştirmesi:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **İstemci güncelleştirmesi:** ConfigMgr1511-client-KB1234567-i386. msp<br />ConfigMgr1511-client-KB1234567-x64. msp|  

Güncelleştirme paketi varsayılan olarak eylemlerinin günlüğünü site sunucusunda bir .log dosyasında tutar. Günlük dosyası, güncelleştirme paketiyle aynı ada sahiptir ve **%SystemRoot%/Temp** klasörüne yazılır.  

Güncelleştirme paketini çalıştırdığınızda, güncelleştirme paketiyle aynı ada sahip bir dosyayı bilgisayarda geçici bir klasörde genişletir ve ardından Updatesetup.exe uygulamasını çalıştırır. Updatesetup.exe Configuration Manager &lt; ürün sürümü \> &lt; KB numarası Sihirbazı için yazılım güncelleştirmesi başlatılır \> .  

Sihirbaz, güncelleştirmenin kapsamına uygun olarak, site sunucusundaki Configuration Manager yükleme klasörü altında bir dizi klasör oluşturur. Klasör yapısı şuna benzer:   
** \\ \\ &lt; Sunucu adı \> \ SMS_ &lt; site kodu \ \> Düzeltme \\ &lt; KB numarası \> \\ &lt; güncelleştirme türü \> \\ &lt; platformu \> **.  

Aşağıdaki tabloda klasör yapısındaki klasörler hakkındaki ayrıntılar verilmektedir:  

|Klasör adı|Daha fazla bilgi|  
|-----------------|----------------------|  
|&lt;Sunucu adı\>|Bu, güncelleştirme paketini çalıştırdığınız site sunucusuyla aynı ada sahiptir.|  
|SMS_ &lt; site kodu\>|Bu, Configuration Manager yükleme klasörünün paylaşma adıdır.|  
|&lt;KB Numarası\>|Bu, söz konusu güncelleştirme paketi için Bilgi Bankası makalesinin kimlik numarasıdır.|  
|&lt;Güncelleştirme türü\>|Bunlar Configuration Manager güncelleştirme türleridir. Sihirbaz, güncelleştirme paketinde bulunan her bir güncelleştirme tipi için ayrı bir klasör oluşturur. Klasör adı güncelleştirme tiplerini temsil eder. Bunlar aşağıdakileri içerir:<br /><br /> **Sunucu**: site sunucuları, site veritabanı SUNUCULARı ve SMS sağlayıcısını çalıştıran bilgisayarlar için güncelleştirmeleri içerir.<br /><br /> **İstemci**: Configuration Manager istemcisine yönelik güncelleştirmeleri içerir.<br /><br /> **AdminConsole**: Configuration Manager konsolundaki güncelleştirmeleri içerir<br /><br /> Yukarıdaki güncelleştirme türlerine ek olarak, sihirbaz **SCUP**adlı bir klasör oluşturur. Bu klasör bir güncelleştirme türünü temsil etmez ancak bunun yerine Updates Publisher’ın .cab dosyasını içerir.|  
|&lt;Platform\>|Bu, platforma özgü bir klasördür. İşlemci türüne özgü güncelleştirme dosyalarını içerir.  Bu klasörler şunları içerir:<br /><br />-x64<br /><br /> -I386|  

##  <a name="how-to-install-updates"></a><a name="bkmk_Install"></a> Güncelleştirmeleri yükleme  
Güncelleştirmeleri yüklemek için önce bir site sunucusuna güncelleştirme paketini yüklemeniz gerekir. Bir güncelleştirme paketini yüklerken, paket, söz konusu güncelleştirme için bir yükleme sihirbazı başlatır. Bu sihirbaz aşağıdaki görevleri gerçekleştirir:  

- Güncelleştirme dosyalarını ayıklar  

- Dağıtımları yapılandırmanıza yardımcı olur  

- Yerel bilgisayarın sunucu bileşenlerinde geçerli güncelleştirmeleri yükler  

Güncelleştirme paketini bir site sunucusuna yükledikten sonra, Configuration Manager için ek bileşenleri güncelleştirebilirsiniz. Aşağıdaki tabloda bu çeşitli bileşenler için güncelleştirme eylemleri açıklanmaktadır:  

|Bileşen|Yönergeler|  
|---------------|------------------|  
|Site sunucusu|Güncelleştirme paketini doğrudan o uzak site sunucusuna yüklemeyi seçmediğinizde güncelleştirmeleri uzak site sunucusuna dağıtın.|  
|Site veritabanı|Uzak site sunucuları için, güncelleştirme paketini doğrudan o uzak site sunucusuna yüklemiyorsanız, site veritabanına yönelik bir güncelleştirmeyi içeren güncelleştirmeleri sunucuya dağıtın.|  
|Configuration Manager konsolu|Configuration Manager konsolunun ilk yüklemesinden sonra, konsolu çalıştıran her bilgisayarda Configuration Manager konsolu için güncelleştirmeleri yükleyebilirsiniz. Konsolun ilk yüklemesi sırasında güncelleştirmeleri uygulamak için Configuration Manager konsolu yükleme dosyalarını değiştiremezsiniz.|  
|Uzak SMS Sağlayıcısı|Güncelleştirmeleri, güncelleştirme paketini yüklediğiniz site sunucusu dışında bir bilgisayarda çalışan her SMS Sağlayıcısı örneği için yükleyin.|  
|Configuration Manager istemcileri|Configuration Manager istemcisinin ilk yüklemesinden sonra, istemciyi çalıştıran her bilgisayara Configuration Manager istemcisi için güncelleştirmeleri yükleyebilirsiniz.|  

> [!NOTE]  
> Güncelleştirmeleri yalnızca Configuration Manager istemcisini çalıştıran bilgisayarlara dağıtabilirsiniz.  

Bir istemciyi, Configuration Manager konsolunu veya SMS sağlayıcısını yeniden yüklerseniz, bu bileşenlere yönelik güncelleştirmeleri de yeniden yüklemeniz gerekir.  

Configuration Manager her bir bileşenden güncelleştirmeleri yüklemek için aşağıdaki bölümlerde yer alan bilgileri kullanın.  

###  <a name="update-servers"></a><a name="bkmk_servers"></a> Güncelleştirme sunucuları  
Sunucular için güncelleştirmeler, **SMS sağlayıcısı**'nın bir örneğini çalıştıran **siteler**, **site veritabanı**ve bilgisayarlar için güncelleştirmeleri içerebilir:  

####  <a name="update-a-site"></a><a name="bkmk_site"></a> Bir siteyi güncelleştirme  
Bir Configuration Manager sitesini güncelleştirmek için, güncelleştirme paketini doğrudan site sunucusuna yükleyebilir veya güncelleştirme paketini farklı bir siteye yükledikten sonra güncelleştirmeleri bir site sunucusuna dağıtabilirsiniz.  

Bir site sunucusuna bir güncelleştirmeyi yüklediğinizde, güncelleştirme yükleme işlemi site sistem rollerinin güncelleştirilmesi gibi, güncelleştirmeyi uygulaması gereken ek eylemleri yönetir. Site veritabanı bu konuda istisnadır. Aşağıdaki bölümde site veritabanının nasıl güncelleştirileceği hakkındaki bilgiler yer alır.  

####  <a name="update-a-site-database"></a><a name="bkmk_database"></a> Site veritabanını güncelleştirme  
Site veritabanını güncelleştirmek için, yükleme işlemi site veritabanında **Update. SQL** adlı bir dosya çalıştırır. Site veritabanını otomatik olarak güncelleştirmek için güncelleştirme işlemini yapılandırabilir veya site veritabanını daha sonra el yordamıyla güncelleştirebilirsiniz.  

**Site veritabanını otomatik güncelleştirme**  

Güncelleştirme paketini bir site sunucusuna yüklediğinizde, sunucu güncelleştirmesi yüklendiğinde site veritabanını otomatik olarak güncelleştirmeyi tercih edebilirsiniz. Bu karar yalnızca güncelleştirme paketini yüklediğiniz site sunucusu için geçerlidir ve uzak site sunucularına güncelleştirmeleri yüklemek için oluşturulan dağıtımlar için geçerli değildir.  

> [!NOTE]  
> Site veritabanını otomatik olarak güncelleştirmeyi seçtiğinizde, işlem veritabanının site sunucusunda mı yoksa uzak bir bilgisayarda mı olduğuna bakılmaksızın bir veritabanını güncelleştirir.  

> [!IMPORTANT]  
> Site veritabanını güncelleştirmeden önce site veritabanının bir yedeğini oluşturun. Site veritabanındaki bir güncelleştirmeyi kaldıramazsınız. Configuration Manager için yedekleme oluşturma hakkında daha fazla bilgi için bkz. [Configuration Manager Için Yedekleme ve kurtarma](backup-and-recovery.md).  

**Site veritabanını el ile güncelleştirme**  

Site sunucusuna güncelleştirme paketini yüklediğinizde site veritabanını otomatik olarak güncelleştirmeme seçeneğini belirlerseniz, sunucu güncelleştirmesi güncelleştirme paketinin çalıştırıldığı site sunucusundaki veritabanını değiştirmez. Ancak, yazılım dağıtımı için oluşturulan paketi kullanan veya yüklediği dağıtımlar her zaman site veritabanını güncelleştirir.  

> [!WARNING]  
> Güncelleştirme hem site sunucusu hem de site veritabanı için güncelleştirmeler içerdiğinde, güncelleştirme hem site sunucusu hem de site veritabanı için tamamlanana kadar bu güncelleştirme işlevsel değildir. Güncelleştirme site veritabanına uygulanana kadar, site desteklenmeyen bir durumda.  

**Bir site veritabanını el ile güncelleştirmek için:**  

1.  Site sunucusunda SMS_SITE_COMPONENT_MANAGER hizmetini durdurun ve SMS_EXECUTIVE hizmetini durdurun.  

2.  Configuration Manager konsolunu kapatın.  

3.  Bu sitenin veritabanında **Update. SQL** adlı güncelleştirme betiğini çalıştırın. Bir SQL Server veritabanını güncelleştirmek üzere bir komut dosyasının nasıl çalıştırılacağı hakkında bilgi için, site veritabanı sunucunuz için kullandığınız SQL Server sürümüne yönelik belgelere bakın.  

4.  Önceki adımlarda durdurulan hizmetleri yeniden başlatın.  

5.  Güncelleştirme paketi yüklediğinde, **Update. SQL** dosyasını site sunucusunda şu konuma ayıklar: ** \\ \\ &lt; sunucu adı \> \ SMS_ &lt; site kodu \ \> Düzeltme \\ &lt; KB numarası \> \Update.exe. SQL**  

####  <a name="update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a> SMS sağlayıcısı 'nı çalıştıran bir bilgisayarı güncelleştirme  
SMS sağlayıcısına yönelik güncelleştirmeleri içeren bir güncelleştirme paketini yükledikten sonra, güncelleştirmeyi SMS sağlayıcısı 'nı çalıştıran her bilgisayara dağıtmanız gerekir. Bunun tek özel durumu, güncelleştirme paketini yüklediğiniz site sunucusuna daha önce yüklenen SMS Sağlayıcısı örneğidir. Site sunucusundaki SMS sağlayıcısının yerel örneği, güncelleştirme paketini yüklediğinizde güncelleştirilir.  

SMS Sağlayıcıyı bir bilgisayara kaldırıp yeniden yüklerseniz, SMS sağlayıcısı güncelleştirmesini o bilgisayara yeniden yüklemeniz gerekir.  

###  <a name="update-clients"></a><a name="BKMK_clients"></a> İstemcileri Güncelleştir  
Configuration Manager istemcisi için güncelleştirmeleri içeren bir güncelleştirme yüklediğinizde, istemcileri güncelleştirme yüklemesiyle otomatik olarak yükseltme veya istemcileri daha sonra el ile yükseltme seçeneği sunulur. Otomatik istemci yükseltme hakkında daha fazla bilgi için bkz. [Windows bilgisayarları için istemcileri yükseltme](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Güncelleştirmeleri Updates Publisher veya bir yazılım dağıtım paketi ile dağıtabilirsiniz veya güncelleştirmeyi her istemciye elle yüklemeyi tercih edebilirsiniz. Güncelleştirmeleri yüklemek için dağıtımları kullanma hakkında daha fazla bilgi için bu konudaki [Configuration Manager için güncelleştirmeleri dağıtma](#BKMK_Deploy) bölümüne bakın.  

> [!IMPORTANT]  
> İstemcileri için güncelleştirmeleri yüklediğinizde ve güncelleştirme paketi sunucular için güncelleştirmeleri içeriyorsa, sunucu güncelleştirmelerini istemcilerin atandığı birincil siteye de yüklediğinizden emin olun.  

İstemci güncelleştirmesini her bir Configuration Manager istemcisinde el ile yüklemek için, **Msiexec.exe** çalıştırmanız ve platforma özgü istemci güncelleştirmesi. msp dosyasına başvurmanız gerekir.  

Örneğin, bir istemci güncelleştirmesi için aşağıdaki komut satırını kullanabilirsiniz. Bu komut satırı istemci bilgisayarda MSIEXEC 'i çalıştırır ve güncelleştirme paketinin site sunucusunda ayıkladığı. msp dosyasına başvurur: **msiexec.exe/p \\ \\ &lt; sunucuadı \> \ SMS_ &lt; sitekodu \> \ düzeltme \\ &lt; KB numarası \> \ istemci \\ &lt; platformu \> \\ &lt; msp \> /l \* v &lt; logfile \> REINSTALLMODE = ünlü yeniden yükleme = tümü**  

###  <a name="update-configuration-manager-consoles"></a><a name="BKMK_console"></a> Configuration Manager konsolları güncelleştirme  
Configuration Manager konsolunu güncelleştirmek için, konsol yüklemesi tamamlandıktan sonra güncelleştirmeyi, konsolu çalıştıran bilgisayara yüklemeniz gerekir.  

> [!IMPORTANT]  
> Configuration Manager konsolu için güncelleştirmeleri yüklediğinizde ve güncelleştirme paketi sunucular için güncelleştirmeleri içeriyorsa, sunucu güncelleştirmelerini de Configuration Manager konsolu ile kullandığınız siteye yüklediğinizden emin olun.  

Güncelleştirmeniz gereken bilgisayar Configuration Manager istemcisini çalıştırıyorsa:  

- Güncelleştirmeyi yüklemek için bir dağıtım kullanabilirsiniz. Güncelleştirmeleri yüklemek için dağıtımları kullanma hakkında daha fazla bilgi için bu konudaki [Configuration Manager için güncelleştirmeleri dağıtma](#BKMK_Deploy) bölümüne bakın.  

- İstemci bilgisayarda doğrudan oturum açtıysanız, yüklemeyi etkileşimli olarak çalıştırabilirsiniz.  

- Güncelleştirmeleri tüm bilgisayarlara elle yükleyebilirsiniz. Configuration Manager konsolu güncelleştirmesini Configuration Manager konsolunu çalıştıran her bilgisayara el ile yüklemek için, Msiexec.exe çalıştırabilir ve Configuration Manager konsolu Update. msp dosyasına başvurabilirsiniz.  

Örneğin, bir Configuration Manager konsolunu güncelleştirmek için aşağıdaki komut satırını kullanabilirsiniz. Bu komut satırı bilgisayarda MSIEXEC 'i çalıştırır ve güncelleştirme paketinin site sunucusunda ayıkladığı. msp dosyasına başvurur: **msiexec.exe/p \\ \\ &lt; ServerName \> \ SMS_ &lt; sitekodu \> \ düzeltme \\ &lt; KB numarası \> \adminkonsol \\ &lt; platformu \> \\ &lt; msp \> /l \* v &lt; logfile \> REINSTALLMODE = ünlü yeniden yükleme = tümü**  

##  <a name="deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Configuration Manager için güncelleştirmeleri dağıtma  
Güncelleştirme paketini bir site sunucusuna yükledikten sonra, güncelleştirmeleri ek bilgisayarlara dağıtmak için aşağıdaki üç yöntemden birini kullanabilirsiniz.  

###  <a name="use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a> Güncelleştirmeleri yüklemek için Publisher 2011 güncelleştirmelerini kullanın  
Güncelleştirme paketini bir site sunucusuna yüklediğinizde, Yükleme Sihirbazı Updates Publisher için, güncelleştirmeleri ilgili bilgisayarlara dağıtmak için kullanabileceğiniz bir katalog dosyası oluşturur. **Bu güncelleştirmeyi dağıtmak için paket ve program kullan**seçeneğini belirlediğinizde bile sihirbaz her zaman bu kataloğu oluşturur.  

Updates Publisher için Katalog **SCUPCatalog.cab** adı verilir ve güncelleştirme paketinin çalıştırıldığı bilgisayardaki şu konumda bulunabilir: ** \\ \\ &lt; ServerName \> \ SMS_ &lt; sitekodu \> \düzeltme \\ &lt; KB numarası \>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
> SCUPCatalog.cab dosyası, güncelleştirme paketinin yüklü olduğu site sunucusuna özgü yollar kullanılarak oluşturulduğundan, diğer site sunucularında kullanılamaz.  

Sihirbaz tamamlandıktan sonra, kataloğu Updates Publisher 'a aktarabilir ve ardından güncelleştirmeleri dağıtmak için Configuration Manager yazılım güncelleştirmelerini kullanabilirsiniz. Updates Publisher hakkında daha fazla bilgi için bkz. [Updates publisher 2011](/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

SCUPCatalog.cab dosyasını güncelleştirme yayımcısına aktarmak ve güncelleştirmeleri yayımlamak için aşağıdaki yordamı kullanın.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Güncelleştirmeleri Updates Publisher 2011 ' e aktarmak için  

1.  Updates Publisher konsolunu başlatın ve **Içeri aktar**' a tıklayın.  

2.  Yazılım güncelleştirmelerini Içeri aktarma Sihirbazı ' nın **Içeri aktarma türü** sayfasında, **içeri aktarılacak kataloğun yolunu belirt**' i seçin ve ardından SCUPCatalog.cab dosyasını belirtin.  

3.  **İleri**' ye ve ardından yeniden **İleri** ' ye tıklayın.  

4.  **Güvenlik uyarısı-Katalog doğrulaması** Iletişim kutusunda **kabul et**' e tıklayın. Sihirbazı tamamladıktan sonra kapatın.  

5.  Updates Publisher konsolunda, dağıtmak istediğiniz güncelleştirmeyi seçin ve ardından **Yayımla**' ya tıklayın.  

6.  Yazılım güncelleştirmelerini Yayımlama Sihirbazı 'nın **Yayımlama seçenekleri** sayfasında, **tam içerik**' i seçin ve ardından **İleri**' ye tıklayın.  

7.  Güncelleştirmeleri yayımlamak için Sihirbazı doldurun.  

###  <a name="use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a> Güncelleştirmeleri yüklemek için yazılım dağıtımını kullanma  
Güncelleştirme paketini bir birincil sitenin veya merkezi yönetim sitesinin site sunucusuna yüklediğinizde, Yükleme Sihirbazı 'Nı yazılım dağıtımı için güncelleştirme paketleri oluşturacak şekilde yapılandırabilirsiniz. Daha sonra her bir paketi, güncelleştirmek istediğiniz bir bilgisayar koleksiyonuna dağıtabilirsiniz.  

Yazılım dağıtım paketi oluşturmak için sihirbazın **yazılım güncelleştirme dağıtımını yapılandırın** sayfasında, güncelleştirmek istediğiniz her bir güncelleştirme paketi türünün onay kutusunu seçin. Kullanılabilir türler arasında sunucular, Configuration Manager konsolları ve istemciler bulunabilir. Seçtiğiniz her güncelleştirme türü için ayrı bir paket oluşturulur.  

> [!NOTE]  
> Sunucular için paket, aşağıdaki bileşenler için güncelleştirmeleri içerir:  
>   
> - Site sunucusu  
> - site veritabanı  
> - Site veritabanı  

Daha sonra, sihirbazın **Yazılım Güncelleştirmesi Dağıtım Yöntemini Yapılandırın** sayfasında, **Yazılım dağıtımını kullanacağım**seçeneğini işaretleyin. Bu seçim, Sihirbazı yazılım dağıtım paketleri oluşturmaya yönlendirir.  

Sihirbaz tamamlandıktan sonra, oluşturduğu paketleri **yazılım kitaplığı** çalışma alanındaki **paketler** düğümünde Configuration Manager konsolunda görüntüleyebilirsiniz. Daha sonra, yazılım paketlerini Configuration Manager istemcilere dağıtmak için standart işleminizi kullanabilirsiniz. Bir paket bir istemcide çalıştığında, güncelleştirmeleri istemci bilgisayardaki Configuration Manager ilgili bileşenlere kurar.  

Paketlerin Configuration Manager istemcilere dağıtılması hakkında daha fazla bilgi için bkz. [paket ve programlar](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a> Configuration Manager güncelleştirmeleri dağıtmak için koleksiyonlar oluşturma  
Belirli güncelleştirmeleri geçerli istemcilere dağıtabilirsiniz. Aşağıdaki bilgiler Configuration Manager için farklı bileşenler için cihaz koleksiyonları oluşturmanıza yardımcı olabilir.  

|Configuration Manager bileşeni|Yönergeler|  
|----------------------------------------|------------------|  
|Merkezi yönetim sitesi sunucusu|Bir doğrudan üyelik sorgusu oluşturun ve merkezi yönetim site sunucusu bilgisayarını ekleyin.|  
|Tüm birincil site sunucuları|Bir doğrudan üyelik sorgusu oluşturun ve tüm birincil site sunucusu bilgisayarlarını ekleyin.|  
|Tüm ikincil site sunucuları|Bir doğrudan üyelik sorgusu oluşturun ve tüm ikincil site sunucusu bilgisayarlarını ekleyin.|  
|Tüm x86 istemciler|Aşağıdaki sorgu ölçütleriyle bir koleksiyon oluşturun:<br /><br /> **\*SMS_G_System_SYSTEM SMS_R_System iç birleşim SMS_G_System_SYSTEM arasından seçim yapın. RESOURCEID = SMS_R_System. RESOURCEID, SMS_G_System_SYSTEM.SystemType = "x86 tabanlı bılgısayar"**|  
|Tüm x64 istemciler|Aşağıdaki sorgu ölçütleriyle bir koleksiyon oluşturun:<br /><br /> **\*SMS_G_System_SYSTEM SMS_R_System iç birleşim SMS_G_System_SYSTEM arasından seçim yapın. RESOURCEID = SMS_R_System. RESOURCEID, SMS_G_System_SYSTEM.SystemType = "x64 tabanlı bılgısayar"**|  
|Configuration Manager konsolunu çalıştıran tüm bilgisayarlar|Bir doğrudan üyelik sorgusu oluşturun ve tüm bilgisayarları ekleyin.|  
|SMS Sağlayıcısının bir örneğini çalıştıran uzak bilgisayarlar|Bir doğrudan üyelik sorgusu oluşturun ve tüm bilgisayarları ekleyin.|  

> [!NOTE]  
> Bir site veritabanını güncelleştirmek için, güncelleştirmeyi o siteye ait site sunucusuna dağıtın.  

Koleksiyon oluşturma hakkında daha fazla bilgi için bkz. [koleksiyonları oluşturma](../../../core/clients/manage/collections/create-collections.md).