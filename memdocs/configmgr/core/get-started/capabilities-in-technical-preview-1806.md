---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview sürüm 1806 ' de bulunan yeni özellikler hakkında bilgi edinin.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 44fcea129b6f45c292bcdd6b83004131ce2d4e96
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694432"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Configuration Manager için Technical Preview 1806 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1806 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Technical Preview sitenize güncelleştirmek ve yeni özellikleri eklemek için yükleyebilirsiniz. 

Bu güncelleştirmeyi yüklemeden önce [Teknik Önizleme](technical-preview.md) makalesini gözden geçirin. Bu makalede, Technical Preview kullanımı, sürümler arasında nasıl güncelleştirme yapılacağı ve geri bildirimde bulunmak için genel gereksinimler ve sınırlamalar tamamladığınızda tercihinize.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Bu Technical Preview 'da bilinen sorunlar

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a> Site, uzak içerik kitaplığıyla yükseltme yapamıyor
<!--514642-->
Site, **cmupdate. log**dosyasında aşağıdaki hatalarla yükseltme yapamıyor:  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Bu sorun, içerik kitaplığı uzak bir konumda olduğunda bu yayında oluşur.

#### <a name="workaround"></a>Geçici çözüm
İçerik kitaplığını site sunucusuna yerel bir sürücüye taşıyın. Daha fazla bilgi için bkz. [site sunucusu için uzak içerik kitaplığı yapılandırma](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server). 



</br>

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a> Üçüncü taraf yazılım güncelleştirmeleri
<!--1352101-->
Bu sürüm, [UserVoice geri bildirimlerinizin](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)bir sonucu olarak üçüncü taraf yazılım güncelleştirmeleri desteğiyle daha da yinelenir. Artık bazı yaygın senaryolar için System Center Updates Publisher (SCUP) kullanımını gerektirsiz olursunuz. Configuration Manager konsolundaki Yeni **üçüncü taraf yazılım güncelleştirme katalogları** düğümü, üçüncü taraf kataloglara abone olmanıza, güncelleştirmelerini yazılım güncelleştirme noktanya yayımlamanıza ve sonra istemcilere dağıtmanıza olanak tanır. 

Aşağıdaki üçüncü taraf yazılım güncelleştirme katalogları bu sürümde sunulmaktadır:

 | Publisher | Katalog adı |
 |--------|---------------------|
 | HP | HP Istemci güncelleştirmeleri Kataloğu |

SCUP, diğer katalogları ve senaryoları desteklemeye devam etmektedir. Configuration Manager konsolunun üçüncü taraf yazılım güncelleştirme katalogları düğümündeki katalogların listesi dinamiktir ve ek kataloglar kullanılabilir ve desteklenir olarak güncelleştirilir.


### <a name="prerequisites"></a>Ön koşullar
- HTTPS etkin bir yazılım güncelleştirme noktasıyla yazılım güncelleştirmeleri yönetimini ayarlayın. Daha fazla bilgi için bkz. [yazılım güncelleştirme yönetimi Için hazırlanma](../../sum/get-started/prepare-for-software-updates-management.md).  
  - Bu sürümdeki bu özellik için yazılım güncelleştirme noktası site sunucusunda olmalıdır. <!--515810--> 

    > [!Tip]  
    > Yazılım güncelleştirme noktası, imzalama sertifikalarını işlemek için kullanılan WSUS API 'Leri için bir gereksinim olduğundan, HTTPS gerektirir. İstemcilerin da HTTPS etkin olması gerekmez. WSUS üzerinde HTTPS 'yi etkinleştirme hakkında daha fazla bilgi için, yardım için aşağıdaki makalelere bakın:  
    > - [WSUS’u Güvenli Yuva Katmanı Protokolü ile güvenli hale getirme](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 
    > - [WSUS desteği blog gönderisi](/archive/blogs/sus/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names)

- Yazılım güncelleştirme noktası, sunucusundaki WSUSContent klasöründe, üçüncü taraf yazılım güncelleştirmeleri için kaynak ikili içeriğini depolamak için yeterli disk alanı. Gerekli depolama alanı, satıcıya, güncelleştirme türlerine ve dağıtım için yayımladığınız belirli güncelleştirmelere göre farklılık gösterir. Sunucusundaki WSUSContent klasörünü daha fazla boş alana sahip başka bir sürücüye taşımanız gerekiyorsa, WSUS destek ekibi Web günlüğü gönderisine [WSUS 'nin güncelleştirmeleri yerel olarak depoladığı konumu nasıl değiştirileceği](/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally)konusuna bakın.  

- İstemci ayarını etkinleştirin ve dağıtın **yazılım güncelleştirmeleri** grubundaki [üçüncü taraf yazılım güncelleştirmelerini etkinleştirin](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) .  

- Site sunucusu, HTTPS bağlantı noktası 443 üzerinden download.microsoft.com için internet erişimi gerektirir. Üçüncü taraf yazılım güncelleştirme eşitleme hizmeti şu anda site sunucusunda çalışır. Bu hizmet, mevcut üçüncü taraf katalogların listesini güncelleştirir, abone olduğunuzda katalogları indirir ve yayımlandığında güncelleştirmeleri indirir. Gerekirse, site sunucusu bilgisayarının site sistem rolü özelliklerindeki **proxy** sekmesinde Internet proxy ayarlarını yapılandırın.  


### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>1. Aşama: özelliği etkinleştirme ve ayarlama
Özelliğini etkinleştirmek ve kullanmak üzere ayarlamak için *hiyerarşi başına bir kez* aşağıdaki adımları gerçekleştirin:  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Hiyerarşide en üst düzey siteyi seçin. Şeritte, **site bileşenlerini Yapılandır**' a tıklayın ve **yazılım güncelleştirme noktası**' nı seçin.  

3. **Üçüncü taraf güncelleştirmeleri** sekmesine geçin. **üçüncü taraf yazılım güncelleştirmelerini etkinleştirme**seçeneğini belirleyin. Sertifika seçenekleri hakkında daha fazla bilgi için bkz. [üçüncü taraf yazılım güncelleştirme desteğini etkinleştirme geliştirmeleri](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Bu sertifikayı yönetmek için Configuration Manager varsayılan seçeneğini kullanırsanız, **Yönetim** çalışma alanındaki **güvenlik** altındaki **Sertifikalar** düğümünde **üçüncü taraf WSUS imzalama** türünde yeni bir sertifika oluşturulur.  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>2. Aşama: bir üçüncü taraf kataloğuna abone olma ve güncelleştirmeleri eşitleme
Abone olmak istediğiniz her bir *üçüncü taraf kataloğu* için aşağıdaki adımları gerçekleştirin:  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Yazılım güncelleştirmeleri** ' ni genişletin ve **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü seçin.  

2. Abone olmak için kataloğu seçin ve Şeritteki **kataloğa abone ol** ' a tıklayın.   

3. Katalog sertifikasını gözden geçirin ve onaylayın.  

   > [!Note]  
   > Üçüncü taraf bir yazılım güncelleştirme kataloğuna abone olduğunuzda, sihirbazda gözden geçirmeniz ve onaylamanız gereken sertifika sitesine eklenir. Bu sertifika, **üçüncü taraf yazılım güncelleştirmeleri Kataloğu**türüdür. **Yönetim** çalışma alanındaki **güvenlik** altındaki **Sertifikalar** düğümünden yönetebilirsiniz.  

4. Sihirbazı tamamlayın.  

   > [!Tip]  
   > İlk abonelikle sonra katalog hemen indirilmeye başlamalıdır. Daha sonra bu sürümde her 24 saatte bir yeniden eşitleniyor. Kataloğun otomatik olarak indirilmesini beklemek istemiyorsanız Şeritteki **Şimdi Eşitle** ' ye tıklayın.  
   > 
   > Katalog indirildikten sonra, ürün meta verilerinin yazılım güncelleştirme noktasıyla eşitlenmesi gerekir. Bu süreç hakkında daha fazla bilgi ve el ile başlatma hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmelerini Synchronize](../../sum/get-started/synchronize-software-updates.md). Bu noktada, üçüncü taraf güncelleştirmelerini **tüm güncelleştirmeler** düğümünde görebilirsiniz. 

5. Ardından, abone olduğunuz üçüncü taraf kataloğu için yazılım güncelleştirme noktası **ürünlerini** yapılandırın. Daha fazla bilgi için bkz. [eşitlenmek için sınıflandırmaları ve ürünleri yapılandırma](../../sum/get-started/configure-classifications-and-products.md). Ürün ölçütleri değiştirildikten sonra, yazılım güncelleştirme eşitlemesi yeniden gerçekleşmelidir.

İstemcilerden uyumluluk sonuçlarını görebilmeniz için önce güncelleştirmeleri taramaları ve değerlendirmesi gerekir. Bu döngüyü, **yazılım güncelleştirmeleri tarama çevrimi** eylemini çalıştırarak bir istemcideki Configuration Manager denetim masasından el ile tetikleyebilirsiniz. İşlem hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri tanıtımı](../../sum/understand/software-updates-introduction.md).


#### <a name="phase-3-deploy-third-party-software-updates"></a>3. Aşama: üçüncü taraf yazılım güncelleştirmelerini dağıtma
İstemcilere dağıtmak istediğiniz *tüm üçüncü taraf yazılım güncelleştirmeleri* için aşağıdaki adımları gerçekleştirin:  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Yazılım güncelleştirmeleri** ' ni genişletin ve **tüm yazılım güncelleştirmeleri** düğümünü seçin.  

   > [!Tip]  
   > Güncelleştirme listesini filtrelemek için **Ölçüt Ekle** ' ye tıklayın. Örneğin, Adobe **Systems, Inc.** için **satıcı** ekleyerek Adobe 'ın tüm güncelleştirmelerini görüntüleyin.  

2. İstemciler için gereken güncelleştirmeleri seçin. **Üçüncü taraf yazılım güncelleştirme Içeriğini Yayımla** ' ya tıklayın ve SMS_ISVUPDATES_SYNCAGENT. log dosyasındaki ilerlemeyi gözden geçirin. Bu eylem, güncelleştirme ikili dosyalarını satıcıdan indirir ve yazılım güncelleştirme noktasındaki sunucusundaki WSUSContent klasöründe depolar. Ayrıca, güncelleştirme durumunu meta verilerden ve yalnızca içerikle ve dağıtılabilir olarak değiştirir.  

   > [!Note]  
   > Üçüncü taraf yazılım güncelleştirme içeriğini yayımladığınızda, içeriği imzalamak için kullanılan tüm sertifikalar siteye eklenir. Bu sertifikalar, **üçüncü taraf yazılım güncelleştirme içerikleri**türündedir. Bunları, **Yönetim** çalışma alanındaki **güvenlik** altındaki **Sertifikalar** düğümünden yönetebilirsiniz.  

3. Mevcut yazılım güncelleştirme yönetimi işlemini kullanarak güncelleştirmeleri dağıtın. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini dağıtma](../../sum/deploy-use/deploy-software-updates.md). Yazılım güncelleştirmelerini dağıtma Sihirbazı 'nın **konum indir** sayfasında, **yazılım güncelleştirmelerini Internet 'ten indirmek**için varsayılan seçeneği belirleyin. Bu senaryoda içerik, dağıtım paketinin içeriğini indirmek için kullanılan yazılım güncelleştirme noktasına zaten yayımlandı.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Üçüncü taraf yazılım güncelleştirmelerinin ilerlemesini izleme
Üçüncü taraf yazılım güncelleştirmelerinin eşitlenmesi, site sunucusundaki SMS_ISVUPDATES_SYNCAGENT bileşeni tarafından gerçekleştirilir. Bu bileşenden durum iletilerini görüntüleyebilir veya SMS_ISVUPDATES_SYNCAGENT. log dosyasında daha ayrıntılı durumu görebilirsiniz. Bu günlük, site yükleme dizininin **Günlükler** alt klasöründeki site sunucusudur. Varsayılan olarak bu yol olur `C:\Program Files\Microsoft Configuration Manager\Logs` . Genel yazılım güncelleştirme yönetimi sürecini izleme hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmelerini izleme](../../sum/deploy-use/monitor-software-updates.md).


### <a name="known-issues"></a>Bilinen sorunlar
- Üçüncü taraf yazılım güncelleştirme eşitleme hizmeti, **WSUS sunucusu bağlantı hesabı**kullanmak üzere yapılandırılmış yazılım güncelleştirme noktasını desteklemez. Bu hesap, yazılım güncelleştirme noktası özellikleri sayfasının **proxy ve hesap ayarları** sekmesinde yapılandırılmışsa, SMS_ISVUPDATES_SYNCAGENT. log dosyasında şu hatayı görürsünüz:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Bu hesap hakkında daha fazla bilgi için bkz. [yazılım güncelleştirme noktası bağlantı hesabı](../plan-design/hierarchy/accounts.md#software-update-point-connection-account).<!--515492-->  

- Bu yeni tümleşik üçüncü taraf yazılım güncelleştirme özelliği ile SCUP gibi diğer araçların kullanımını karıştırmayın. Üçüncü taraf yazılım güncelleştirme eşitleme hizmeti, yalnızca farklı bir uygulama, araç veya bir komut dosyası tarafından WSUS 'a eklenen güncelleştirmeler (örneğin, SCUP) için içerik yayımlayamaz. **Üçüncü taraf yazılım güncelleştirme Içeriğini Yayımla** eylemi Bu güncelleştirmelerde başarısız olur. Bu özelliğin henüz desteklemediği üçüncü taraf güncelleştirmeleri dağıtmanız gerekiyorsa, bu güncelleştirmeleri dağıtmak için mevcut işleminizi tam olarak kullanın.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Microsoft Edge için Windows Defender SmartScreen ayarlarını yapılandırma
<!--1353701-->
Bu sürüm, [Microsoft Edge tarayıcı uyumluluk ayarları Ilkesine](../../compliance/deploy-use/browser-profiles.md) [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) 'in üç ayarını ekler. İlke artık **SmartScreen ayarları** sayfasında aşağıdaki ek ayarları içerir:
- **SmartScreen 'e Izin ver**: Windows Defender SmartScreen 'e izin verilip verilmeyeceğini belirtir. Daha fazla bilgi için bkz. [Allowsmartscreen tarayıcı ilkesi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Kullanıcılar siteler Için SmartScreen istemlerini geçersiz kılabilir**: kullanıcıların olası kötü amaçlı Web siteleri hakkındaki Windows Defender SmartScreen Filtresi uyarılarını geçersiz kılıp kılamayacağını belirtir. Daha fazla bilgi için [PreventSmartScreenPromptOverride Browser ilkesine](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)bakın.
- **Kullanıcılar dosyalar Için SmartScreen istemlerini geçersiz kılabilir**: kullanıcıların, doğrulanmamış dosyaları Indirme hakkındaki Windows Defender SmartScreen Filtresi uyarılarını geçersiz kılıp kılamayacağını belirtir. Daha fazla bilgi için [PreventSmartScreenPromptOverrideForFiles Browser ilkesine](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)bakın.



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Ortak yönetilen bir cihaz için Microsoft Intune MDM ilkesini eşitleme
<!--1357377-->
Bu sürümden itibaren [ortak yönetim iş yükünü](../../comanage/how-to-switch-workloads.md)değiştirdiğinizde, ortak YÖNETILEN cihazlar MDM ilkesini Microsoft Intune otomatik olarak eşitler. Bu eşitleme Ayrıca, Configuration Manager konsolundaki Istemci bildirimlerinden **bilgisayar Ilkesini indir** eylemini başlattığınızda de gerçekleşir. Daha fazla bilgi için bkz. [istemci bildirimini kullanarak istemci ilkesi almayı başlatma](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Ortak yönetimi kullanarak Office 365 iş yükünü Intune 'a geçirme
<!--1357841-->
Artık, ortak yönetimi etkinleştirdikten sonra Configuration Manager Office 365 iş yükünü Microsoft Intune olarak geçiş yapabilirsiniz. Bu iş yükünü dengelemek için ortak yönetim özellikleri sayfasına gidin ve kaydırıcı çubuğunu Configuration Manager 'den pilot 'a veya tümüne taşıyın. Daha fazla bilgi için bkz. [Windows 10 cihazlar Için ortak yönetim](../../comanage/overview.md).

Ayrıca yeni bir genel koşul da vardır. Bu, **cihazda Intune tarafından yönetilen Office 365 uygulamalardır**. Bu koşul, varsayılan olarak yeni Office 365 uygulamalarına bir gereksinim olarak eklenir. Bu iş yükünü geçiş yaparken, ortak yönetilen istemciler uygulamadaki gereksinimi karşılamıyor, bu nedenle Configuration Manager aracılığıyla dağıtılan Office 365 ' i yüklemez.

### <a name="known-issue"></a>Bilinen sorun
- Bu iş yükü geçişi Şu anda yalnızca Office 365 dağıtımları için geçerlidir. Configuration Manager, Office 365 güncelleştirmelerini yönetmeye devam eder.<!--510876--> Olası bir geçici çözüm hakkında daha fazla bilgi için, Configuration Manager sürüm 1802 sürüm notunda [Office 365 istemci ayarını değiştirme uygulanmadığını](../servers/deploy/install/release-notes.md)inceleyin.



## <a name="package-conversion-manager"></a>Paket Dönüştürme Yöneticisi 
<!--1357861-->
Paket Dönüştürme Yöneticisi artık eski Configuration Manager 2007 paketlerini güncel dal uygulamalarına Configuration Manager dönüştürmenize olanak sağlayan tümleşik bir araçtır. Daha sonra bağımlılıklar, gereksinim kuralları ve Kullanıcı cihaz benzeşimi gibi uygulamaların özelliklerini kullanabilirsiniz.

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

> [!Important]  
> Daha önce Package Conversion Manager 'ın daha eski bir sürümünü yüklediyseniz, önce sitenizi yükseltmeden önce bu sürümü kaldırın. Yeni tümleşik sürüm yükleme gerektirmez, ancak var olan sürümlerle çakışabilir.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Uygulama yönetimi** ' ni genişletin ve **paketler**' i seçin.  
2. Bir paket seçin. Aşağıdaki üç seçenek, şeridin **paket dönüştürme** grubunda mevcuttur:  
     - **Paketi çözümle**: paketi çözümleyerek dönüştürme işlemini başlatın.
     - **Paketi Dönüştür**: bazı paketler, bu eylemle kolayca uygulamalara dönüştürülebilir.
     - **Düzeltme ve dönüştürme**: bazı paketler, uygulamalara dönüştürmeden önce sorunların düzeltilmesi gerekir.  


3. **İzleme** çalışma alanına gidin ve **paket dönüştürme durumu**' nu seçin. Bu yeni panoda, sitedeki paketlerin genel analiz ve dönüştürme durumu gösterilmektedir. Yeni bir arka plan görevi, analiz verilerini otomatik olarak özetler.  

   > [!Tip]  
   > Paket Dönüştürme Yöneticisi, paketlerin analizini zamanlamanıza gerek yoktur. Bu eylem artık tümleşik özetleme görevi tarafından işlenir.  

![Paket dönüştürme durumu panosunun ekran görüntüsü](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Yazılım güncelleştirmelerini içerik olmadan dağıtma
<!--1357933-->
Artık yazılım güncelleştirmelerini, yazılım güncelleştirme içeriğini indirilmeden ve dağıtım noktalarına dağıtmadan cihazlara dağıtabilirsiniz. Bu özellik son derece büyük güncelleştirme içeriğiyle ilgilenirken veya istemcilerin Microsoft Update bulut hizmetinden her zaman içerik almasını istediğinizde faydalıdır. Bu senaryodaki istemciler, gerekli içeriğe zaten sahip olan eşlerden içerik de indirebilir. Configuration Manager istemcisi içerik indirmeyi yönetmeye devam eder, bu nedenle Configuration Manager eş önbellek özelliğini veya teslim Iyileştirme gibi diğer teknolojileri kullanabilir. Bu özellik, Windows ve Office güncelleştirmeleri de dahil olmak üzere Configuration Manager yazılım güncelleştirme yönetimi tarafından desteklenen tüm güncelleştirme türlerini destekler. 

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Normal başına yazılım güncelleştirme dağıtımı başlatın. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini dağıtma](../../sum/deploy-use/deploy-software-updates.md).
2. Yazılım güncelleştirmelerini dağıtma Sihirbazı ' nda, **dağıtım paketi** sayfasında, **dağıtım paketi**için yeni seçeneğini belirleyin.

### <a name="known-issues"></a>Bilinen sorunlar
- Bu ayarla dağıtılan bir güncelleştirmenin simgesi, güncelleştirme geçersiz olduğu gibi kırmızı bir X ile yanlış görüntülenir. Daha fazla bilgi için bkz. [yazılım güncelleştirmeleri için kullanılan simgeler](../../sum/understand/software-updates-icons.md). <!--515556-->  
- Bu ayar yalnızca yazılım güncelleştirmelerini dağıtma Sihirbazı ile tümleşiktir. Bu, şu anda otomatik dağıtım kurallarıyla kullanılamıyor. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office Özelleştirme Aracı tümleştirmesiyle Office 365 yükleyicisi
<!--1358149-->
Office özelleştirme aracı artık Configuration Manager konsolundaki Office 365 yükleyicisiyle tümleşiktir. Office 365 için bir dağıtım oluştururken, artık en son Office yönetilebilirlik ayarlarını dinamik olarak yapılandırabilirsiniz. Office Özelleştirme Aracı, yeni Office 365 Derlemeleriyle aynı anda güncelleştirilir. Artık kullanılabilir oldukları anda Office 365 ' deki yeni yönetilebilirlik ayarlarından yararlanabilirsiniz. 

### <a name="prerequisites"></a>Ön koşullar
- Configuration Manager konsolunu çalıştıran bilgisayarda HTTPS bağlantı noktası 443 üzerinden internet erişimi gerekir. Office 365 Istemci Yükleme Sihirbazı, açmak için bir Windows standart Web tarayıcısı API 'SI kullanır https://config.office.com . Bir internet proxy 'si kullanılıyorsa, Kullanıcı bu URL 'ye erişebilmelidir.

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin ve **Office 365 istemci yönetimi** düğümünü seçin.
2. Office 365 Istemci Yükleme Sihirbazı 'nı başlatmak için panoda **office 365 yükleyicisi** kutucuğuna tıklayın. Daha fazla bilgi için bkz. [Office 365 uygulamalarını dağıtma](../../sum/deploy-use/manage-office-365-proplus-updates.md).
3. **Office ayarı** sayfasında, **Office Web sayfasına git ' e**tıklayın. Bu dağıtımın ayarlarını belirtmek için çevrimiçi Office Özelleştirme Aracı 'nı kullanın. 
4. Tamamlandığında sağ üst köşedeki **Gönder** ' e tıklayın. Office 365 Istemci Yükleme Sihirbazı 'Nı sona erdirin.



## <a name="improvements-to-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi geliştirmeleri
Bu sürüm, bulut yönetimi ağ geçidi (CMG) için aşağıdaki geliştirmeleri içerir:

### <a name="simplified-client-bootstrap-command-line"></a>Basitleştirilmiş istemci önyükleme komut satırı
<!--1358215-->
Configuration Manager istemcisini Internet 'e bir CMG aracılığıyla yüklerken, daha az komut satırı özelliği gereklidir. Bu senaryonun bir örneği hakkında daha fazla bilgi için, bkz. ortak yönetim için hazırlanırken [Configuration Manager Client 'ı yüklemek Için komut satırı](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) . 

Aşağıdaki komut satırı özellikleri tüm senaryolarda gereklidir:
- CCMHOSTNAME  
- SMSSITECODE  

PKI tabanlı istemci kimlik doğrulama sertifikaları yerine istemci kimlik doğrulaması için Azure AD kullanılırken aşağıdaki özellikler gereklidir:
- AADCLIENTAPPıD  
- AADRESOURCEURI  

İstemci intranete geri dolaşırsa aşağıdaki özellik gereklidir:
- SMSMP  

Aşağıdaki örnek, yukarıdaki tüm özellikleri içerir:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Daha fazla bilgi için bkz. [istemci yükleme özellikleri](../clients/deploy/about-client-installation-properties.md).

### <a name="download-content-from-a-cmg"></a>Bir CMG 'den içerik indirin
<!--1358651-->
Daha önce, bulut dağıtım noktası ve CMG 'yi ayrı roller olarak dağıtmanız gerekiyordu. Artık bu sürümde, bir CMG, istemcilere içerik de sunabilir. Bu işlevsellik, Azure VM 'lerinin gerekli sertifikalarını ve maliyetini azaltır. Bu özelliği etkinleştirmek için, **CMG 'nin bulut dağıtım noktası olarak çalışmasına Izin verme ve** CMG özelliklerinin **Ayarlar** sekmesinde Azure Storage 'dan içerik sunma için yeni seçeneği etkinleştirin. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Azure AD 'de güvenilen kök sertifika gerekli değildir
<!--503899-->
Bir CMG oluşturduğunuzda, artık ayarlar sayfasında [Güvenilen bir kök sertifika](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) sağlamanız gerekmez. İstemci kimlik doğrulaması için Azure Active Directory (Azure AD) kullanılırken bu sertifika gerekli değildir, ancak sihirbazda gerekli olması için kullanılır.

> [!Important]  
> PKI istemci kimlik doğrulama sertifikaları kullanıyorsanız, yine de CMG 'ye bir güvenilen kök sertifika eklemeniz gerekir.



## <a name="improvements-to-secure-client-communications"></a>Güvenli istemci iletişimlerinde iyileştirmeler
<!--1358278,1358279-->
Bu sürüm, ağ erişim hesabındaki ek bağımlılıklar kaldırılarak [Gelişmiş güvenli istemci iletişimlerinde](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) yineleme yapmaya devam eder. Yeni site seçeneğini **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanmak**üzere etkinleştirdiğinizde, aşağıdaki senaryolar bir dağıtım noktasından içerik indirmek için bir ağ erişim hesabı gerektirmez:  

- Önyükleme medyasından veya PXE 'den çalışan görev dizileri
- Yazılım merkezinden çalıştırılan görev dizileri  

Bu görev dizileri işletim sistemi dağıtımı veya özel olabilir. Ayrıca, çalışma grubu bilgisayarları için de desteklenir.



## <a name="software-center-infrastructure-improvements"></a>Software Center altyapı geliştirmeleri
<!--1358309-->
Uygulama Kataloğu rollerinin artık yazılım merkezi 'nde Kullanıcı tarafından kullanılabilen uygulamaları görüntülemesi gerekmez. Bu değişiklik, kullanıcılara uygulama sunmak için gereken sunucu altyapısını azaltmanıza yardımcı olur. Yazılım Merkezi artık, bu bilgileri almak için yönetim noktasına dayanır ve bu da daha büyük ortamların [sınır gruplarına](../servers/deploy/configure/boundary-groups.md#management-points)atayarak daha iyi ölçeklendirilmesine yardımcı olur.

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Tüm uygulama kataloğu rollerini siteden kaldırın. Bu roller, Uygulama Kataloğu Web hizmet noktası ve Uygulama Kataloğu web sitesi noktasını içerir.
2. Bir uygulamayı bir kullanıcı koleksiyonuna kullanılabilir olarak dağıtın.
3. Uygulamayı bulmak, istemek ve yüklemek için hedeflenen kullanıcı olarak yazılım merkezi 'ni kullanın.

### <a name="known-issue"></a>Bilinen sorun
- Bu özellikle Azure Active Directory katılmış bir istemci kullanıyorsanız, siteyi **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanacak**şekilde yapılandırmayın. Şu anda bu özellikle çakışıyor.<!--515846--> Bu ayar hakkında daha fazla bilgi için bkz. [Gelişmiş güvenli istemci iletişimleri](capabilities-in-technical-preview-1805.md#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Bir cihazdaki tüm kullanıcılar için Windows uygulama paketleri sağlama
<!--1358310-->
Artık cihazdaki tüm kullanıcılar için Windows uygulama paketi ile bir uygulama sağlayabilirsiniz. Bu senaryonun yaygın bir örneği, bir okuldaki öğrenciler tarafından kullanılan tüm cihazlara Minecseft: eğitim sürümü gibi Iş ve eğitim Microsoft Store bir uygulama sağlamadır. Daha önce Configuration Manager yalnızca Kullanıcı başına bu uygulamaları yüklemeyi destekler. Yeni bir cihazda oturum açtıktan sonra bir öğrenciye bir uygulamaya erişmeniz gerekir. Artık uygulama tüm kullanıcılar için cihaza sağlandığında, daha hızlı bir şekilde üretken olabilirler.

> [!Important]  
> Aynı Windows uygulama paketinin farklı sürümlerini yükleme, sağlama ve güncelleştirme konusunda dikkatli olun, bu durum beklenmedik sonuçlara neden olabilir. Bu davranış, uygulamayı sağlamak için Configuration Manager kullanılırken ve sonra kullanıcıların uygulamayı Microsoft Store güncelleştirmesine izin verirken meydana gelebilir. Daha fazla bilgi için bkz. [iş için Microsoft Store uygulamaları yönetirken](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)sonraki adım Kılavuzu.  

Configuration Manager, çevrimdışı lisanslı bir uygulamayı sağlarken, Windows 'un Microsoft Store otomatik olarak güncelleştirmesine izin vermez.  

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Yeni bir uygulama oluşturun. Bu uygulama, Iş ve eğitim için Microsoft Store eşitlediğiniz bir Windows uygulama paketinden veya çevrimdışı lisanslı bir uygulamadan olmalıdır.  

2. Uygulama oluşturma Sihirbazı 'nın **genel bilgiler** sayfasında **Bu uygulamayı cihazdaki tüm kullanıcılar için sağlama**seçeneğini etkinleştirin.  

   > [!Tip]  
   > Mevcut bir uygulamayı değiştiriyorsanız, bu ayar uygulama özelliklerinin **Kullanıcı deneyimi** sekmesindedir.  

3. Uygulamayı bir cihaz koleksiyonuna dağıtın.  

4. Farklı kullanıcı hesaplarıyla hedeflenen bir cihazda oturum açın ve uygulamayı başlatın.  

> [!Note]  
> Sağlanan bir uygulamayı kullanıcıların zaten oturum açmış olduğu cihazlardan kaldırmanız gerekiyorsa, iki adet kaldırma dağıtımı oluşturmanız gerekir. İlk kaldırma dağıtımını cihazları içeren bir cihaz koleksiyonuna hedefleyin. İkinci kaldırma dağıtımını, sağlanan uygulamayla cihazlarda zaten oturum açmış olan kullanıcıları içeren bir kullanıcı koleksiyonuna hedefleyin. Bir cihazda sağlanan uygulamayı kaldırırken, Windows bu uygulamayı da kullanıcılar için kaldırmıyor. 



## <a name="improvements-to-the-surface-dashboard"></a>Yüzey panosu geliştirmeleri
<!--1358654-->
Bu sürüm, [yüzey panosu](../clients/manage/surface-device-dashboard.md)için aşağıdaki geliştirmeleri içerir:
- Surface panosu artık grafik bölümleri seçiliyken ilgili cihazların bir listesini görüntüler.
   - **Surface cihazlarının yüzdesi** kutucuğuna tıkladığınızda Surface cihazlarının bir listesi açılır.
   - **En üstteki beş bellenim** sürümü kutucuğunda bir çubuğa tıkladığınızda, bu ilgili bellenim sürümüne sahip Surface cihazlarının bir listesi açılır.
- Bu cihaz listeleri yüzey panosundan görüntülenirken bir cihaza sağ tıklayıp ortak eylemler gerçekleştirebilirsiniz.



## <a name="hardware-inventory-default-unit-revision"></a>Donanım envanteri varsayılan birim düzeltmesi
<!--514442-->
[Configuration Manager sürüm 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure)' de, birçok raporlama görünümünde kullanılan varsayılan birim MEGABAYT (MB) ila GIGABAYT (GB) olarak değiştirildi. [Büyük tamsayı değerleri için donanım envanterinde iyileştirmeler](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)ve müşteri geri bildirimlerine bağlı olarak, bu varsayılan bırım artık MB 'dir.



## <a name="next-steps"></a>Sonraki adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).