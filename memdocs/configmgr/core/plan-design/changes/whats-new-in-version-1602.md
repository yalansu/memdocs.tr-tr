---
title: Sürüm 1602 ' de yeni
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1602 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 334397cfa52c90694823107c2144bfbbcbd509ac
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993633"
---
# <a name="what39s-new-in-version-1602-of-configuration-manager"></a>Sürüm 1602 ' deki yenilikler&#39;Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Configuration Manager için 1602 güncelleştirmesi yalnızca, 1511 sürümünü çalıştıran daha önce yüklenen sitelerde konsol içi bir güncelleştirme olarak sunulmaktadır. Sürüm 1511, yeni Configuration Manager siteleri yüklemek için kullandığınız ilk temel sürümdür.  


> [!TIP]  
> Aşağıdakiler hakkında daha fazla bilgi edinin:  
>   
> - [Yeni siteler yükleme](../../servers/deploy/install/prepare-to-install-sites.md) (1511 gibi bir temel sürüm kullanarak)  
> - [Güncelleştirmeleri sitelere yükleme](../../servers/manage/updates.md) (güncelleştirme 1602 gibi)  

 Aşağıdaki bölümlerde, Configuration Manager sürüm 1602 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi sağlanmaktadır.  

## <a name="site-infrastructure"></a>Site altyapısı  

###  <a name="in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a> Windows Server 2008 R2 çalıştıran site sunucularının işletim sistemini yerinde yükseltme  
 Sürüm 1602 veya sonraki sürümleri çalıştıran Configuration Manager siteleri, site sunucuları işletim sisteminin Windows Server 2008 R2 'den Windows Server 2012 R2 'ye yerinde yükseltmesini destekler.  

> [!WARNING]  
>  Windows Server 2012 R2’ye yükseltmeden önce sunucudan WSUS 3.2’yi kaldırmalısınız .  
>   
>  Bu kritik adım hakkında daha fazla bilgi için, [Windows Server Update Services genel bakış](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality)konusunun "yeni ve değiştirilmiş işlevsellik" bölümüne bakın.  

 Bir sunucuyu yükseltmek için, Windows Server 2012 R2 yükseltme yordamlarını kullanın. Yükseltmeden sonra bir Configuration Manager site sunucusu geri yüklemesi çalıştırmanız gerekmez. Yükseltme yordamları için bkz. Windows Server belgelerindeki [Windows Server 2012 R2 için Yükseltme Seçenekleri](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)).  

###  <a name="sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a> AlwaysOn kullanılabilirlik grupları SQL Server  
 Birincil sitelerde site veritabanını barındırmak için SQL Server AlwaysOn kullanılabilirlik gruplarını ve merkezi yönetim sitesini bir yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümü olarak kullanın.  

 Ayrıntılar için bkz. [Configuration Manager için yüksek oranda kullanılabilir site veritabanı Için AlwaysOn SQL Server](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>İşletim sistemi dağıtımı  

### <a name="windows-10-servicing"></a>Windows 10 Bakımı  
 Windows 10 bakımı için aşağıdaki iyileştirmeler Configuration Manager sürüm 1602 ' ye eklenmiştir:  

-   **Dil**, **gerekli**ve **başlık**için filtrelemenize izin veren bakım planlarında yeni filtre seçenekleri mevcuttur. Yalnızca belirtilen ölçütleri karşılayan yükseltmeler ilişkili dağıtıma eklenecektir.  

-   Yazılım güncelleştirmeleri eşitlemesi için **yükseltmeler** sınıflandırmasını seçtiğinizde bir uyarı görüntülenir. Bu uyarı, yazılım güncelleştirmelerini başarıyla eşitleyebilmeniz ve Windows 10 hizmetinin düzgün çalışması için Windows Server Update Services (WSUS) 4,0 için [düzeltme 3095113](https://support.microsoft.com/kb/3095113) ' nin gerekli olduğunu bilmenizi sağlar. Uyarı iletisinden ilişkili Bilgi Bankası makalesine gidebilirsiniz.  

-   Kullanılabilir Windows 10 yükseltmeleri artık yalnızca Configuration Manager konsolunun **Windows 10 Bakımı**  \  **tüm Windows 10 güncelleştirmeleri** düğümünde görüntülenir. Bu güncelleştirmeler artık **yazılım güncelleştirmeleri**  \  konsolunun**tüm yazılım güncelleştirmeleri** düğümünde görüntülenmez.  

-   Bakım planı yüksek riskli dağıtım olarak kabul edilir ve **Koleksiyon Seç** penceresinde yalnızca sitenin özelliklerinde yapılandırılmış dağıtım doğrulama ayarlarını karşılayan özel koleksiyonlar görüntülenir. Daha fazla bilgi için bkz. [Configuration Manager için yüksek riskli dağıtımları yönetme ayarları](../../servers/manage/settings-to-manage-high-risk-deployments.md).  

-   Windows 10 yükseltme paketini Başlatan kullanıcılar artık işletim sistemlerini yükseltileceğiyle ilgili bir ileti alıyor.  

## <a name="application-management"></a>Uygulama yönetimi  

### <a name="ios-app-configuration-policies"></a>iOS uygulama yapılandırma ilkeleri  
 Kullanıcı bir iOS uygulaması çalıştırdığında gerekebilecek ayarları sağlamak için Configuration Manager uygulama yapılandırma ilkelerini kullanın. Örneğin, bir uygulama kullanıcının özel bir bağlantı noktası numarası, dil, güvenlik ayarları veya marka ayarları (örneğin, bir şirket logosu) belirtmesini gerektirebilir. Bu ayarlar yanlış girilirse, bu, yardım masanızın yükünü artırabilir ve ayrıca yeni uygulamaların benimsenmesini yavaşlatır.  

 Uygulama yapılandırma ilkeleri, bu ayarları uygulamayı çalıştırmadan önce bir ilkedeki kullanıcılara dağıtmanıza izin vererek bu sorunları ortadan kaldırmanıza yardımcı olabilir. Daha sonra ayarlar otomatik olarak sağlanır ve kullanıcının herhangi bir işlem yapması gerekmez.

### <a name="manage-volume-purchased-ios-apps"></a>Toplu satın alınan iOS uygulamalarını yönetme  
 Configuration Manager, Apple Volume Purchase program 'dan (VPP) toplu olarak satın aldığınız uygulamaları dağıtmanıza ve yönetmenize yardımcı olabilir. Configuration Manager, uygulama mağazasından lisans bilgilerini içeri aktarır ve kaç lisansın kullanıldığını izler.  


### <a name="automatic-creation-of-office-mobile-apps"></a>Office mobil uygulamalarının otomatik olarak oluşturulması  
 1511 sürümünden 1602 sürümüne güncelleştirdiğinizde Configuration Manager, Android ve iOS için aşağıdaki Microsoft Office mobil uygulamaları otomatik olarak oluşturur:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (yalnızca iOS)  

-   Microsoft Outlook  

Bu uygulamaları Configuration Manager konsolunun **uygulamalar** düğümünde bulabilirsiniz.  

 Uygulamaları dağıtma hakkında daha fazla bilgi için bkz. [Configuration Manager ile uygulama dağıtma](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Yazılım güncelleştirmeleri  

### <a name="manage-microsoft-365-client-updates"></a>Microsoft 365 istemci güncelleştirmelerini yönetme  
 Configuration Manager, yazılım güncelleştirme yönetimi iş akışını kullanarak Microsoft 365 istemci güncelleştirmelerini yönetme olanağına sahiptir. Daha fazla bilgi için bkz. [Configuration Manager Ile Office 365 uygulama güncelleştirmelerini yönetme](../../../sum/deploy-use/manage-office-365-proplus-updates.md).  

## <a name="compliance-settings"></a>Uyumluluk ayarları  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Windows 10 Team çalıştıran cihazlar için uyumluluk ayarları  
 **Windows 8.1 ve Windows 10** yapılandırma öğesine yeni ayarlar eklendi. Bu ayarlar, Surface Hub bir cihaz gibi Windows 10 Team çalıştıran cihazları denetlemenize yardımcı olur.  

 Ayrıntılar için bkz. [Configuration Manager istemcisi olmadan yönetilen Windows 8.1 ve Windows 10 cihazları için yapılandırma öğeleri oluşturma](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Android Samsung KNOX Standard cihazlar için bilgi noktası modu ayarları  
 Bilgi noktası modu bir cihazı yalnızca belirli özellikleri çalışacak şekilde kilitlemenize izin verir. Örneğin, cihazın yalnızca belirttiğiniz bir yönetilen uygulamayı çalıştırmasına izin verebilir veya cihazdaki ses düğmelerini devre dışı bırakabilirsiniz. Bu ayarlar, bir cihazın tanıtım modeli için veya yalnızca tek bir işlevi (satış noktası cihazı gibi) gerçekleştirmeye ayrılmış bir cihaz için kullanılabilir. Configuration Manager, artık Samsung KNOX Standard cihazlar için bilgi noktası modu ayarlarını belirtebilirsiniz.  


## <a name="conditional-access"></a>Koşullu erişim  

### <a name="conditional-access-for-pcs-managed-by-configuration-manager"></a>Configuration Manager tarafından yönetilen bilgisayarlar için koşullu erişim  
 Bu sürümden önceki bir BILGISAYARA koşullu erişim ayarlamak için, BILGISAYARıN Intune 'a kaydolması veya etki alanına katılmış bir BILGISAYAR olması gerekiyordu. 1602 güncelleştirmesiyle başlayarak, Configuration Manager tarafından yönetilen bilgisayarlar için koşullu erişim desteklenir. Configuration Manager tarafından yönetilen PC 'Ler için, Exchange Online ve SharePoint Online 'a erişimi yalnızca ayarladığınız uyumluluk ilkeleriyle uyumlu cihazlara kısıtlayabilirsiniz.  


### <a name="restricting-access-based-on-the-health-of-devices"></a>Cihazların sistem durumuna göre erişimi kısıtlama  
 Artık sistem durumu kanıtlama hizmeti tarafından bildirilen cihazların sistem durumuna bağlı olarak e-posta ve Microsoft 365 hizmetlerine erişimi kısıtlayabilirsiniz. Ayrıca, Intune tarafından yönetilen cihazlar cihaz sistem durumu raporlarına dahil edilir.  

 Configuration Manager konsolu, cihazların sistem durumlarına göre erişim izni verilip verilmeyeceğini belirtmenize izin veren yeni bir uyumluluk kuralı sunar. Sistem durumu kanıtlama hizmeti ve Intune 'da cihazların sistem durumunun nasıl bildirildiği hakkında ayrıntılar için bkz. [Configuration Manager Için durum kanıtlama](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Yeni uyumluluk ilkesi kuralları  
 Otomatik Güncelleştirmeler ve cihazların kilidini açmak için parola gerektirme gibi yeni uyumluluk ilkesi kuralları, daha iyi güvenlik gereksinimlerini desteklemek için eklenmiştir.


### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Kayıtlı ve uyumlu cihazların şirket içi Exchange 'e her zaman erişebildiğinizden emin olun  
 Aşağıdaki seçeneği belirlediğinizde, Intune 'a kayıtlı ve uyumluluk ilkeleriyle uyumlu olan cihazların şirket içi Exchange 'e erişmesine izin verilir: **varsayılan kural geçersiz kılma-Intune 'a kayıtlı ve uyumlu cihazların şirket Içi Exchange 'e erişmesine her zaman izin ver:**. Bu kural, şirket içi Exchange için **koşullu erişim Ilkesini Yapılandırma Sihirbazı** ' nın **Genel sayfasında** bulunur.

 Bu kural varsayılan kuralı geçersiz kılar. Bu, varsayılan kuralı karantina veya engelleme erişimi olarak ayarlamış olsanız bile kayıtlı ve uyumlu cihazların şirket içi Exchange 'e erişebileceği anlamına gelir. Kayıtlı ve uyumlu cihazların her zaman şirket içi Exchange aracılığıyla e-posta erişimine sahip olmasını istiyorsanız bu ayarı kullanın.   

 Ayrıntılı yönergeler için bkz. [e-posta erişimini yönetme](../../../mdm/understand/what-happened-to-hybrid.md).  

## <a name="client-management"></a>İstemci yönetimi  

### <a name="client-online-status"></a>İstemci çevrimiçi durumu  
 İstemciler için yeni bir durum, bir bilgisayarın çevrimiçi olup olmadığını izlemek için kullanılabilir. Bir bilgisayar, atanan yönetim noktasına bağlıysa çevrimiçi olarak kabul edilir. Bilgisayarın çevrimiçi olduğunu göstermek için, istemci, yönetim noktasına ping benzeri iletiler gönderir. Yönetim noktası 5 dakikadan sonra bir ileti almazsa, istemci çevrimdışı kabul edilir.  

 Ayrıntılar için bkz. [istemcileri izleme](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Yazılım Merkezi 'nden bılgısayar makinesi ve kullanıcı ilkesini yenileme  
 **Options**Yazılım merkezi 'nin **Sync Policy**  >  **bilgisayar bakım** sayfasına, bilgisayar Configuration Manager makine ve kullanıcı ilkesini yenilemeye neden olan yeni bir seçenek, eşitleme ilkesi eklenmiştir.  

### <a name="software-center-branding-changes"></a>Yazılım Merkezi marka değişiklikleri  
 Yazılım Merkezi 'nde görünen rengi, kuruluş adını ve simgeyi değiştirebilirsiniz. Bu ayarlar aşağıdaki kurallara göre uygulanır:  

- Uygulama Kataloğu web sitesi noktası site sunucusu rolü yüklü değilse, Yazılım Merkezi, **Yazılım Merkezi 'nde görüntülenen kuruluş adı**adlı **Bilgisayar Aracısı** istemci ayarında belirtilen kuruluş adını görüntüler.  

- Uygulama Kataloğu web sitesi noktası site sunucusu rolü yüklüyse, Yazılım Merkezi Uygulama Kataloğu web sitesi noktası site sunucusu rolünün özelliklerinde belirtilen kuruluş adını ve rengini görüntüler.  

- Microsoft Intune bir abonelik yapılandırılıp Configuration Manager ortamına bağlanırsa, Yazılım Merkezi, Intune Abonelik özelliklerinde belirtilen kuruluş adını, rengini ve Şirket logosunu görüntüler.  

### <a name="health-attestation"></a>Durum kanıtlama  
 Yöneticiler, Configuration Manager konsolunda Windows 10 Cihaz Durumu Kanıtlama’nın durumunu görebilir. Bu, Configuration Manager için kullanılabilir ve Microsoft Intune ile Configuration Manager. Cihaz durumu kanıtlama, yöneticinin istemci bilgisayarlarda aşağıdaki güvenilir BIOS, TPM ve önyükleme yazılım yapılandırmalarının etkin olduğundan emin olmasını sağlar:  

-   Erken başlatılan kötü amaçlı yazılımdan koruma  

-   BitLocker  

-   Güvenli Önyükleme  

-   Kod Bütünlüğü  

Ayrıntılar için bkz. [Configuration Manager Için durum kanıtlama](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Kötü amaçlı yazılımdan koruma ayarlarında iyileştirmeler Endpoint Protection  
 1602 Endpoint Protection Windows Defender için kötü amaçlı yazılımdan koruma ilkesine aşağıdaki yeni ayarları ekler:  

-   Gerçek zamanlı koruma: yüklemeden önce istenmeyebilecek uygulamaları indirme sırasında engelleyin.  

-   Tarama ayarları: tam tarama sırasında eşlenmiş ağ sürücülerine tarama yapın.  

-   Otomatik örnek dosya gönderimi ayarları:  

     Kötü amaçlı yazılımdan koruma altyapısı, daha fazla analiz için Microsoft 'a gönderilecek dosya örnekleri isteyebilir. Varsayılan olarak, bu tür örnekleri göndermeden önce her zaman sorar. Yöneticiler artık bu davranışı yapılandırmak için aşağıdaki ayarları yönetebilir:  

    -   Gelişmiş: Microsoft 'un algılanan belirli öğelerin kötü amaçlı olup olmadığını belirlemesine yardımcı olmak için otomatik örnek dosya gönderimini etkinleştirin.  

    -   Gelişmiş: kullanıcıların otomatik örnek dosya gönderimi ayarlarını değiştirmesine Izin verin.  

    Ayrıca, Endpoint Protection kötü amaçlı yazılımdan koruma ilkesinin "dışlama ayarları" bölümünde, var olan **dosyaları ve klasörleri çıkar** ayarı artık cihaz dışlamalarını sağlar.  

Ayrıntılar için bkz. [Endpoint Protection için kötü amaçlı yazılımdan koruma ilkeleri oluşturma ve dağıtma](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Mobil aygıt yönetimi  

### <a name="ios-activation-lock"></a>iOS Etkinleştirme Kilidi  
 Configuration Manager, iOS 7,1 ve üzeri cihazlar için iPhone 'Umu bul uygulamasının bir özelliği olan iOS Etkinleştirme Kilidi yönetmenize yardımcı olabilir. Bir cihazda iPhone’umu Bul uygulaması kullanıldığında Etkinleştirme Kilidi otomatik olarak etkinleştirilir. Bu özellik etkinleştirildikten sonra şunların yapılabilmesi için Apple kimliği ve parolasının girilmesi gerekir:  

-   İPhone 'Umu bul seçeneğini devre dışı bırakın.  

-   Cihazı silin.  

-   Cihazı yeniden etkinleştirin.  

Configuration Manager, iOS 7,1 ve üstünü çalıştıran hem denetimli hem de denetlenen cihazların Etkinleştirme Kilidi durumunu isteyebilir. Denetimli cihazlarda, Configuration Manager Etkinleştirme Kilidi atlama kodunu alabilir ve doğrudan cihaza gönderebilir.  

### <a name="monitor-terms-and-conditions-deployments"></a>Hüküm ve koşullar dağıtımlarını izleme  
 Hüküm ve koşullar dağıtımlarını Configuration Manager konsolunda izleyebilirsiniz.  

 Dağıtımlar listesinden hüküm ve koşullar dağıtımını seçin. Özet alanı aşağıdaki istatistikleri gösterir:  

-   **Uyumlu**: kullanıcılar hüküm ve koşulların en son sürümünü kabul etmiş.  

-   **Hata**  

-   **Uyumsuz**: kullanıcılar hüküm ve koşulların bir sürümünü kabul etmiş, ancak en son sürümü değil.  

-   **Bilinmiyor**: kullanıcılar, kayıtlı bir cihaz olmadan dahil olmak üzere hüküm ve koşulları hiç kabul etmedi.