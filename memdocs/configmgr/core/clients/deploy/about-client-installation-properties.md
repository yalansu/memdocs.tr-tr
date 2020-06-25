---
title: İstemci yükleme parametreleri ve özellikleri
titleSuffix: Configuration Manager
description: Configuration Manager istemcisini yüklemek için CCMSetup komut satırı parametreleri ve özellikleri hakkında bilgi edinin.
ms.date: 06/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4065f320ec27f53e50c64bc7ca0c97d3f6923853
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353284"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Configuration Manager içindeki istemci yükleme parametreleri ve özellikleri hakkında

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcisini yüklemek için CCMSetup.exe komutunu kullanın. Komut satırında istemci yükleme *parametreleri* sağlarsanız, yükleme davranışını değiştirirler. Komut satırında istemci yükleme *özellikleri* sağlarsanız, yüklü istemci aracısının ilk yapılandırmasını değiştirir.

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> CCMSetup.exe hakkında

CCMSetup.exe komutu istemciyi bir yönetim noktasından veya kaynak konumdan yüklemek için gerekli dosyaları indirir. Bu dosyalar şunları içerebilir:  

- İstemci yazılımını yükleyen client.msi Windows Installer paketi

- İstemci önkoşulları

- Configuration Manager istemcisi için güncelleştirmeler ve düzeltmeler

> [!NOTE]
> client.msi doğrudan yükleyemezsiniz.  

CCMSetup.exe, yüklemeyi özelleştirmek için komut satırı *parametreleri* sağlar. Parametrelere bir eğik çizgi () eklenir `/` ve kural, küçük harfe göre yapılır. Bir parametresinin değerini, `:` hemen ardından değeri olan bir iki nokta üst üste () kullanmak için belirtirsiniz. Daha fazla bilgi için bkz. [CCMSetup.exe komut satırı parametreleri](#ccmsetupexe-command-line-parameters).

Ayrıca, client.msi davranışını değiştirmek için CCMSetup.exe komut satırına *Özellikler* sağlayabilirsiniz. Kurala göre özellikler büyük bir durumdur. Bir özellik için değeri `=` , hemen ardından değer gelen eşittir işareti () kullanarak belirtirsiniz. Daha fazla bilgi için bkz. [Client.msi özellikleri](#clientMsiProps).

> [!IMPORTANT]  
> client.msi özelliklerini belirttıklamadan önce CCMSetup parametrelerini belirtin.  

CCMSetup.exe ve destekleyici dosyalar, site sunucusunda Configuration Manager yükleme klasörünün **istemci** klasöründe bulunur. Configuration Manager, bu klasörü site paylaşımı altındaki ağa paylaşır. Örneğin, `\\SiteServer\SMS_ABC\Client`.

Komut satırında, CCMSetup.exe komutu aşağıdaki biçimi kullanır:  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

Örneğin:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

Bu örnek aşağıdaki işlemleri yapar:  

- İstemci yükleme dosyalarını indirmek için dağıtım noktalarının bir listesini istemek üzere SMSMP01 adlı yönetim noktasını belirtir.  

- İstemcinin bir sürümü bilgisayarda zaten varsa yüklemenin durması gerektiğini belirtir.  

- client.msi dosyasına istemciyi site kodu S01'e ataması yönergesi verir.  

- client.msi dosyasına, SMSFP01 adlı geri dönüş durum noktasını kullanma yönergesi verir.  

> [!TIP]  
> Bir parametre değeri boşluk içeriyorsa, tırnak işaretleri ile çevreleyin.  

Configuration Manager için Active Directory şemasını genişletirseniz, site Active Directory Domain Services çok sayıda istemci yükleme özelliği yayımlar. Configuration Manager istemcisi bu özellikleri otomatik olarak okur. Daha fazla bilgi için bkz. [Active Directory Domain Services yayımlanan istemci yükleme özellikleri hakkında](about-client-installation-properties-published-to-active-directory-domain-services.md)  

## <a name="ccmsetupexe-command-line-parameters"></a>Komut satırı parametrelerini CCMSetup.exe

### <a name=""></a><a name="bkmk_help"></a> /?

ccmsetup.exe için kullanılabilir komut satırı parametrelerini gösterir.  

Örnek: `ccmsetup.exe /?`

### <a name="source"></a>/Source

Dosya yükleme konumunu belirtir. Yerel veya UNC yolunu kullanın. Cihaz, sunucu ileti bloğu (SMB) protokolünü kullanarak dosyaları indirir. **/Source**kullanmak için, istemci yüklemesine yönelik Windows Kullanıcı hesabının konum üzerinde **okuma** izinleri olması gerekir.

CCMSetup 'ın içeriği nasıl indirdiği hakkında daha fazla bilgi için bkz. [sınır grupları-istemci yüklemesi](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup). Ayrıca, bu makalede hem **/MP** hem de **/Source** parametreleri kullanırsanız CCMSetup davranışının ayrıntıları da yer almaktadır.

> [!TIP]  
> Alternatif indirme konumlarını belirtmek için, komut satırında **/Source** parametresini birden çok kez kullanabilirsiniz.  

Örnek: `ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/MP

Bilgisayarların bağlanacağı bir kaynak yönetim noktası belirtir. Bilgisayarlar, yükleme dosyaları için en yakın dağıtım noktasını bulmak üzere bu yönetim noktasını kullanır. Dağıtım noktası yoksa veya bilgisayarlar dosyaları dağıtım noktalarından dört saatten sonra indiremez, dosyaları belirtilen yönetim noktasından indirirler.  

CCMSetup 'ın içeriği nasıl indirdiği hakkında daha fazla bilgi için bkz. [sınır grupları-istemci yüklemesi](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup). Ayrıca, bu makalede hem **/MP** hem de **/Source** parametreleri kullanırsanız CCMSetup davranışının ayrıntıları da yer almaktadır.

> [!IMPORTANT]  
> Bu parametre, bilgisayarların bir indirme kaynağını bulması için bir başlangıç yönetim noktası belirtir ve herhangi bir sitede herhangi bir yönetim noktası olabilir. İstemciyi belirtilen yönetim noktasına *atamaz* .

Bilgisayarlar, istemci bağlantıları için site sistem rolü yapılandırmasına bağlı olarak dosyaları bir HTTP veya HTTPS bağlantısı üzerinden indirir. Bu indirme, yapılandırırsanız BITS daraltma da kullanabilir. Yalnızca HTTPS istemci bağlantıları için tüm dağıtım noktalarını ve yönetim noktalarını yapılandırırsanız, istemci bilgisayarın geçerli bir istemci sertifikasına sahip olduğunu doğrulayın.  

Birden fazla yönetim noktası belirtmek için **/MP** komut satırı parametresini kullanabilirsiniz. Bilgisayar ilk sunucuya bağlanamıyorsa, belirtilen listede bir sonraki işlemi dener. Birden çok yönetim noktası belirttiğinizde, değerleri noktalı virgülle ayırın.

İstemci HTTPS kullanarak bir yönetim noktasına bağlanırsa, bilgisayar adı olmayan FQDN 'yi belirtin. Değer, yönetim noktası PKI sertifikasının **Konu** veya **Konu diğer adı**ile aynı olmalıdır. Configuration Manager, intranetteki bağlantılar için sertifikadaki bir bilgisayar adını kullanmayı desteklese de, FQDN kullanılması önerilir.

Bilgisayar adına sahip bir örnek:`ccmsetup.exe /mp:SMSMP01`  

FQDN ile örnek:`ccmsetup.exe /mp:smsmp01.contoso.com`  

Bu parametre Ayrıca bir bulut yönetimi ağ geçidinin (CMG) URL 'sini de belirtebilir. İstemciyi Internet tabanlı bir cihaza yüklemek için bu URL 'YI kullanın. Bu parametrenin değerini almak için aşağıdaki adımları kullanın:

- CMG oluşturma. Daha fazla bilgi için bkz. [CMG 'Yi ayarlama](../manage/cmg/setup-cloud-management-gateway.md).
- Etkin bir istemcide, yönetici olarak bir Windows PowerShell komut istemi açın.
- Şu komutu çalıştırın:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- `https://` **/MP** parametresiyle kullanılacak ön eki ekleyin.

Bulut yönetimi ağ geçidi URL 'sini kullandığınız zaman için örnek:`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> **/MP** parametresi için bir bulut yönetimi ağ geçidinin URL 'sini belirtirken, ile başlaması gerekir `https://` .

### <a name="regtoken"></a>/regtoken

<!--5686290-->

Sürüm 2002 ' den başlayarak, toplu kayıt belirteci sağlamak için bu parametreyi kullanın. Internet tabanlı bir cihaz, bu belirteci bir bulut yönetimi ağ geçidi (CMG) üzerinden kayıt işleminde kullanır. Daha fazla bilgi için bkz. [CMG Için belirteç tabanlı kimlik doğrulaması](deploy-clients-cmg-token.md).

Bu parametreyi kullandığınızda, aşağıdaki parametreleri ve özellikleri de ekleyin:

- [**/MP**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSITECODE**](#smssitecode)
- [**SMSMP**](#smsmp)

Aşağıdaki örnek komut satırı, gerekli diğer kurulum parametrelerini ve özelliklerini içerir:

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

CCMSetup.exe yükleme dosyalarını indirilemezse, yeniden deneme aralığını dakika olarak belirtmek için bu parametreyi kullanın. CCMSetup, [**/DownloadTimeout**](#downloadtimeout) parametresinde belirtilen sınıra ulaşana kadar yeniden denemeye devam eder.

Örnek: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Bu parametre, CCMSetup 'ın varsayılan olarak yaptığı bir hizmet olarak çalışmasını önler. CCMSetup bir hizmet olarak çalıştığında, bilgisayarın yerel sistem hesabı bağlamında çalışır. Bu hesap, yükleme için gereken ağ kaynaklarına erişmek için yeterli haklara sahip olmayabilir. **/Noservice**ile CCMSetup.exe, yüklemeyi başlatmak için kullandığınız kullanıcı hesabının bağlamında çalışır.

Örnek: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

CCMSetup 'ın yerel sistem hesabını kullanan bir hizmet olarak çalışması gerektiğini belirtir.  

> [!TIP]
> **/Service** parametresiyle CCMSetup.exe çalıştırmak için bir komut dosyası kullanıyorsanız, hizmet başladıktan sonra CCMSetup.exe çıkar. Yükleme ayrıntılarını betiğe doğru şekilde bildiremeyebilir.

Örnek: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Configuration Manager istemcisini kaldırmak için bu parametreyi kullanın. Daha fazla bilgi için bkz. [Istemciyi kaldırma](../manage/manage-clients.md#BKMK_UninstalClient).

Örnek: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

İstemcinin herhangi bir sürümü zaten yüklüyse, bu parametre istemci yüklemesinin durması gerektiğini belirtir.  

Örnek: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

Yüklemeyi tamamlaması gerekirse bilgisayarı yeniden başlamaya zorlamak için bu parametreyi kullanın. Bu parametreyi belirtmezseniz, yeniden başlatma gerektiğinde CCMSetup çıkar. Sonraki el ile yeniden başlatma sonrasında devam eder.

Örnek: `CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSÖnceliği

Cihaz, istemci yükleme dosyalarını bir HTTP bağlantısı üzerinden indirdiğinde, İndirme önceliğini belirtmek için bu parametreyi kullanın. Aşağıdaki olası değerlerden birini belirtin:

- `FOREGROUND`

- `HIGH`

- `NORMAL`varsayılanını

- `LOW`

Örnek: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/indirmezamanaşımı

CCMSetup istemci yükleme dosyalarını indiremediğinde, bu parametre en fazla zaman aşımını dakika olarak belirtir. Bu zaman aşımından sonra, CCMSetup yükleme dosyalarını indirmeye çalışmayı durduruyor. Varsayılan değer **1440** dakikadır (bir gün).

Yeniden deneme girişimleri arasındaki aralığı belirtmek için [**/retry**](#retry) parametresini kullanın.

Örnek: `ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

İstemcinin bir PKI istemci kimlik doğrulama sertifikası kullanması için bu parametreyi belirtin. Bu parametreyi eklemezseniz veya istemci geçerli bir sertifika bulamazsa, otomatik olarak imzalanan bir sertifika ile HTTP bağlantısı kullanır.

Örnek: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> Bazı senaryolarda bu parametreyi belirtmeniz gerekmez, ancak yine de bir istemci sertifikası kullanın. Örneğin, istemci gönderme ve yazılım güncelleştirme tabanlı istemci yüklemesi. Bir istemciyi el ile yüklerken ve HTTPS etkin bir yönetim noktasıyla **/MP** parametresini kullandığınızda bu parametreyi kullanın.
>
> Ayrıca, bir istemciyi yalnızca internet iletişimi için yüklediğinizde bu parametreyi de belirtin. **CCMALWAYSINF = 1** özelliğini Internet tabanlı yönetim noktası (**CCMHOSTNAME**) ve site kodu (**smssitekodu**) özellikleriyle birlikte kullanın. Internet tabanlı istemci yönetimi hakkında daha fazla bilgi için bkz. [İnternet 'ten veya güvenilmeyen bir ormandan istemci iletişimleri Için değerlendirmeler](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

### <a name="nocrlcheck"></a>/NoCRLCheck

Bir istemcinin, bir PKI sertifikasıyla HTTPS üzerinden iletişim kurduğunda sertifika iptal listesini (CRL) denetmaması gerektiğini belirtir. Bu parametreyi belirtmezseniz, istemci HTTPS bağlantısı kurmadan önce CRL 'YI denetler. İstemci CRL denetimi hakkında daha fazla bilgi için bkz., [PKI sertifikası iptali Için planlama](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Örnek: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

Bu parametre, istemci yükleme özelliklerini listeleyen bir metin dosyasını belirtir.

- CCMSetup bir hizmet olarak çalışıyorsa, bu dosyayı CCMSetup sistem klasörüne yerleştirin: `%Windir%\Ccmsetup` .

- [**/Noservice**](#noservice) parametresini belirtirseniz, bu dosyayı CCMSetup.exe aynı klasöre yerleştirin.

Örnek: `CCMSetup.exe /config:"configuration file name.txt"`

Doğru dosya biçimini sağlamak için, site sunucusundaki Configuration Manager yükleme dizinindeki klasöründe **mobileclienttemplate. tcf** dosyasını kullanın `\bin\<platform>` . Bu dosya, bölümler ve bunların nasıl kullanılacağı hakkında açıklamalar içerir. `[Client Install]`Aşağıdaki metinden sonra, bölümünde istemci yükleme özelliklerini belirtin: `Install=INSTALL=ALL` .

Örnek `[Client Install]` bölüm girdisi:`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/önkoşuluatla

Bu parametre CCMSetup.exe belirtilen önkoşulu yüklememediğini belirtir. Birden çok değer girebilirsiniz. Her bir değeri ayırmak için noktalı virgül karakterini ( `;` ) kullanın.

Örnekler:

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

İstemci önkoşulları hakkında daha fazla bilgi için bkz. [Windows istemci önkoşulları](prerequisites-for-deploying-clients-to-windows-computers.md).

### <a name="forceinstall"></a>/forceinstall

CCMSetup.exe var olan tüm istemcileri kaldırmasını ve yeni bir istemci yüklemesini belirtin.  

### <a name="excludefeatures"></a>/ExcludeFeatures

Bu parametre CCMSetup.exe belirtilen özelliği yüklememediğini belirtir.

Örnek: `CCMSetup.exe /ExcludeFeatures:ClientUI` Istemciye yazılım merkezi yüklenmez.  

> [!NOTE]  
> `ClientUI`, **/Excludefeatem** parametresinin desteklediği tek değerdir.

### <a name="alwaysexcludeupgrade"></a>/AlwaysExcludeUpgrade

Bu parametre, [**otomatik istemci yükseltmesini**](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)etkinleştirdiğinizde bir istemcinin otomatik olarak yükseltilmesi gerekip gerekmediğini belirtir.

Desteklenen değerler:

- `TRUE`: İstemci otomatik olarak yükseltilmez
- `FALSE`: İstemci otomatik olarak yükseltir (varsayılan)

Örneğin:  

`CCMSetup.exe /AlwaysExcludeUpgrade:TRUE`

Daha fazla bilgi için bkz. [genişletilmiş birlikte çalışabilirlik istemcisi](../../understand/interoperability-client.md).

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a>CCMSetup.exe dönüş kodları

CCMSetup.exe komutu aşağıdaki dönüş kodlarını sağlar. Sorunu gidermek için, `%WinDir%\ccmsetup\ccmsetup.log` bağlam için istemciyi ve dönüş kodları hakkında ek ayrıntıları gözden geçirin.

|Dönüş kodu|Anlamı|  
|-----------|-------|  
|0|Başarılı|  
|6|Hata|  
|7|Yeniden başlatma gerekiyor|  
|8|Kurulum zaten çalışıyor|  
|9|Önkoşul değerlendirme hatası|  
|10|Kurulum bildirim karma doğrulama hatası|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a>Ccmsetup.msi özellikleri

Aşağıdaki özellikler ccmsetup.msi yükleme davranışını değiştirebilir.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

Bu CCMSetup 'ı kullanın. ek komut satırı parametreleri ve özellikleri CCMSetup 'a geçirmek için *MSI* özelliği. *exe*. Diğer parametreleri ve özellikleri tırnak işaretleri () içine ekleyin `"` . Configuration Manager istemcisini [ıNTUNE MDM yükleme yöntemiyle önyüklediğinizde](plan/client-installation-methods.md#microsoft-intune-mdm-installation)bu özelliği kullanın.

Örnek: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune komut satırını 1024 karakterle sınırlandırır.

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a>Client.msi özellikleri

Aşağıdaki özellikler, ccmsetup.exe yüklenen client.msi yükleme davranışını değiştirebilir. [Client Push yükleme yöntemini](plan/client-installation-methods.md#client-push-installation)kullanırsanız, bu özellikleri Configuration Manager konsolundaki **Client Push Yükleme özelliklerinin** **istemci** sekmesinde belirtin.

### <a name="aadclientappid"></a>AADCLIENTAPPıD

Azure Active Directory (Azure AD) istemci uygulaması tanımlayıcısını belirtir. Bulut yönetimi için [Azure hizmetlerini yapılandırırken](../../servers/deploy/configure/azure-services-wizard.md) istemci uygulamasını oluşturabilir veya içeri aktarabilirsiniz. Azure Yöneticisi, Azure portal bu özelliğin değerini alabilir. Daha fazla bilgi için bkz. [uygulama kimliği Al](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). **Aadclientappıd** özelliği için, bu uygulama kimliği **Yerel** uygulama türü içindir.

Örnek: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Azure AD Server uygulama tanımlayıcısını belirtir. Bulut yönetimi için [Azure hizmetlerini yapılandırırken](../../servers/deploy/configure/azure-services-wizard.md) sunucu uygulamasını oluşturabilir veya içeri aktarabilirsiniz. Sunucu uygulamasını oluştururken, sunucu uygulaması oluştur penceresinde bu özellik, **uygulama kimliği URI 'sidir**.

Azure Yöneticisi, Azure portal bu özelliğin değerini alabilir. **Azure Active Directory**, **uygulama kayıtları**altında sunucu uygulamasını bulun. **Web uygulaması/API**uygulama türü ' ne bakın. Uygulamayı açın, **Ayarlar**' ı seçin ve ardından **Özellikler**' i seçin. Bu **Aadresourceuri** istemci yükleme özelliği IÇIN **uygulama kimliği URI 'si** değerini kullanın.

Örnek: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTıD

Azure AD kiracı tanımlayıcısını belirtir. [Azure hizmetlerini](../../servers/deploy/configure/azure-services-wizard.md) bulut yönetimi için yapılandırırken bu kiracının bağlantılarını Configuration Manager. Bu özelliğin değerini almak için aşağıdaki adımları kullanın:

- Aynı Azure AD kiracısına katılmış bir Windows 10 cihazında, bir komut istemi açın.
- Şu komutu çalıştırın:`dsregcmd.exe /status`
- Cihaz durumu bölümünde **Tenantıd** değerini bulun. Örneğin, `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Azure Yöneticisi Azure portal bu değeri de alabilir. Daha fazla bilgi için bkz. [KIRACı kimliği Al](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).

Örnek: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

İstemci ayarlarına ve ilkelerine erişim verilecek bir veya daha fazla Windows kullanıcı hesabını veya grubunu belirtir. İstemci bilgisayarda yerel yönetici kimlik bilgileriniz olmadığında bu özellik faydalıdır. Noktalı virgüllerle () ayrılan hesapların bir listesini belirtin `;` .

Örnek: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Gerekirse, istemci yüklemesinden sonra bilgisayarın sessizce yeniden başlatılmasına izin verin.

> [!IMPORTANT]  
> Bu özelliği kullandığınızda, bilgisayar uyarı vermeden yeniden başlatılır. Bu davranış, bir Kullanıcı Windows 'da oturum açmış olsa bile oluşur.

Örnek: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

İstemcisinin her zaman internet tabanlı olduğunu ve intranete hiçbir zaman bağlanmayacağını belirtmek için bu özellik değerini olarak ayarlayın `1` . İstemcinin bağlantı türü **İnternet**görüntüler.  

İnternet tabanlı yönetim noktasının FQDN 'sini belirtmek için bu özelliği [**CCMHOSTNAME**](#ccmhostname) ile birlikte kullanın. Ayrıca, CCMSetup parametresi [**/UsePKICert**](#usepkicert) ve site kodu ([**smssitekodu**](#smssitecode)) ile birlikte kullanın.

Internet tabanlı istemci yönetimi hakkında daha fazla bilgi için bkz. [İnternet 'ten veya güvenilmeyen bir ormandan istemci iletişimleri Için değerlendirmeler](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).

Örnek: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

Sertifika verenler listesini belirtmek için bu özelliği kullanın. Bu liste, Configuration Manager sitesinin güvendiği güvenilen kök sertifika yetkilileri (CA) için sertifika bilgilerini içerir.  

Bu değer, kök CA sertifikasındaki konu öznitelikleri için büyük/küçük harfe duyarlı bir eşleşmedir. Öznitelikleri virgül ( `,` ) veya noktalı virgül () ile ayırın `;` . Bir ayırıcı çubuk () kullanarak birden fazla kök CA sertifikası belirtin `|` .

Örnek: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> Site için **MobileClient. tcf** dosyasındaki **certificateverenler** özniteliğinin değerini kullanın. Bu dosya, `\bin\<platform>` site sunucusundaki Configuration Manager yükleme dizininin alt klasörüdür.

Sertifika verenler listesi ve istemcilerin sertifika seçimi işlemi sırasında bunu nasıl kullanacağı hakkında daha fazla bilgi için bkz., [PKI istemci sertifikası seçimini planlama](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).

### <a name="ccmcertsel"></a>CCMCERTSEL

İstemcide HTTPS iletişimi için birden fazla sertifika varsa, bu özellik, geçerli bir istemci kimlik doğrulama sertifikası seçme ölçütlerini belirtir.

Sertifika konu adı veya konu diğer adını aramak için aşağıdaki anahtar sözcükleri kullanın:

- **Konu**: tam eşleşme bulma
- **SubjectStr**: kısmi eşleşme bulma

Örnekler:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: `computer1.contoso.com` Konu adı veya konu alternatif adı içindeki bilgisayar adıyla tam olarak eşleşen bir sertifika arayın.

- `CCMCERTSEL="SubjectStr:contoso.com"`: `contoso.com` Konu adı veya konu diğer adı içinde içeren bir sertifika arayın.

Konu adı veya konu diğer adı içinde nesne tanımlayıcısı (OID) veya ayırt edici ad özniteliklerini aramak için **SubjectAttr** anahtar sözcüğünü kullanın.

Örnekler:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: Bir nesne tanımlayıcısı ve adı olarak ifade edilen kuruluş birimi özelliğini arayın `Computers` .

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: Bir ayırt edici ad olarak ifade edilen ve adlı kuruluş birimi özniteliği için arama yapın `Computers` .

> [!IMPORTANT]
> Konu adını kullanırsanız, **Subject** anahtar sözcüğü büyük/küçük harfe duyarlıdır ve **SubjectStr** anahtar sözcüğü büyük/küçük harfe duyarsızdır.
>
> Konu alternatif adını kullanırsanız, hem **Konu** hem de **SubjectStr** anahtar sözcükleri büyük/küçük harfe duyarlıdır.

Sertifika seçimi için kullanabileceğiniz özniteliklerin tüm listesi için bkz. [PKI sertifika seçim ölçütleri Için desteklenen öznitelik değerleri](#BKMK_attributevalues).

Aramayla birden fazla sertifika eşleşiyorsa ve [**Ccmfirstcert**](#ccmfirstcert) ' ı ayarlarsanız, `1` istemci yükleyicisi en uzun geçerlilik süresine sahip sertifikayı seçer.

### <a name="ccmcertstore"></a>CCMCERTSTORE

İstemci yükleyicisi, bilgisayar için varsayılan **Kişisel** sertifika deposunda geçerli bir sertifika bulamazsa, alternatif bir sertifika deposu adı belirtmek için bu özelliği kullanın.

Örnek: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

Bu özellik, istemci yüklenirken hata ayıklama günlüğüne yazmayı mümkün yapar. Bu özellik, istemcinin sorun giderme için düşük düzey bilgileri kaydetmesine neden olur. Bu özelliği üretim sitelerinde kullanmaktan kaçının. Aşırı günlük kaydı gerçekleşebilir, bu durum günlük dosyalarındaki ilgili bilgileri bulmayı zorlaştırır. [**Ccmenablelogging**](#ccmenablelogging)'i de etkinleştirin.

Desteklenen değerler:

- `0`: Hata ayıklama günlüğünü kapat (varsayılan)
- `1`: Hata ayıklama günlüğünü aç

Örnek: `CCMSetup.exe CCMDEBUGLOGGING=1`  

Daha fazla bilgi için bkz. [günlük dosyaları hakkında](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Configuration Manager varsayılan olarak günlüğe kaydetmeyi mümkün.

Desteklenen değerler:

- `TRUE`: Günlüğü aç (varsayılan)
- `FALSE`: Günlüğü kapat

Örnek: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

Daha fazla bilgi için bkz. [günlük dosyaları hakkında](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

İstemci sistem durumu değerlendirme aracının (ccmeval.exe) çalışma süresi (dakika). Öğesinden öğesinden bir tamsayı değeri `1` belirtin `1440` . Varsayılan olarak, ccmeval günde bir kez çalışır (1440 dakika).

Örnek: `CCMSetup.exe CCMEVALINTERVAL=1440`

İstemci sistem durumu değerlendirmesi hakkında daha fazla bilgi için bkz. [Istemcileri izleme](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmevalhour"></a>CCMEVALHOUR

İstemci sistem durumu değerlendirme aracının (ccmeval.exe) çalıştırıldığı günün saati. `0`(Gece yarısı) ile `23` (11:00 PM) arasında bir tamsayı değeri belirtin. Varsayılan olarak, ccmeval gece yarısı çalışır.

İstemci sistem durumu değerlendirmesi hakkında daha fazla bilgi için bkz. [Istemcileri izleme](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

Bu özelliği olarak ayarlarsanız `1` , istemci en uzun geçerlilik süresine sahıp PKI sertifikasını seçer.

Örnek: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

İstemci internet üzerinden yönetiliyorsa, bu özellik Internet tabanlı yönetim noktasının FQDN 'sini belirtir.  

**Smssitekodu = Auto**yükleme özelliğiyle bu seçeneği belirtmeyin. Internet tabanlı istemcileri doğrudan Internet tabanlı bir siteye atayın.

Örnek: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Bu özellik, bir bulut yönetimi ağ geçidinin (CMG) adresini belirtebilir. Bu özelliğin değerini almak için aşağıdaki adımları kullanın:

- CMG oluşturma. Daha fazla bilgi için bkz. [CMG 'Yi ayarlama](../manage/cmg/setup-cloud-management-gateway.md).
- Etkin bir istemcide, yönetici olarak bir Windows PowerShell komut istemi açın.
- Şu komutu çalıştırın:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Döndürülen değeri **CCMHOSTNAME** özelliği ile olduğu gibi kullanın.

Örneğin, `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> **CCMHOSTNAME** özelliği için bir CMG adresi belirttiğinizde, gibi bir ön ek eklemeyin `https://` . Bu öneki yalnızca bir CMG 'nin **/MP** URL 'siyle kullanın.

### <a name="ccmhttpport"></a>CCMHTTPPORT

HTTP üzerinden site sistem sunucularıyla iletişim kurarken kullanılacak istemci bağlantı noktasını belirtir. Varsayılan olarak, bu değer `80` .

Örnek: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

HTTPS üzerinden site sistem sunucularıyla iletişim kurarken kullanılacak istemci bağlantı noktasını belirtir. Varsayılan olarak, bu değer `443` .

Örnek: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

Configuration Manager istemci dosyalarını yükleyecek klasörü ayarlamak için bu özelliği kullanın. Varsayılan olarak, kullanır `%WinDir%\CCM` .

> [!TIP]
> İstemci dosyalarını yüklediğiniz yere bakılmaksızın, **ccmcore.dll** dosyayı her zaman `%WinDir%\System32` klasörüne yükler. 64 bitlik bir IŞLETIM sisteminde, klasöre bir ccmcore.dll kopyası yüklenir `%WinDir%\SysWOW64` . Bu dosya, Configuration Manager SDK 'dan istemci API 'Lerinin 32 bit sürümünü kullanan 32 bitlik uygulamaları destekler.

Örnek: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Configuration Manager günlük dosyalarına yazılacak ayrıntı düzeyini belirtmek için bu özelliği kullanın.

Desteklenen değerler:

- `0`: Verbose
- `1`: Varsayılan
- `2`: Uyarılar ve hatalar
- `3`: Yalnızca hatalar

Örnek: `CCMSetup.exe CCMLOGLEVEL=0`

Daha fazla bilgi için bkz. [günlük dosyaları hakkında](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Bir Configuration Manager günlük dosyası en büyük boyuta ulaştığında, istemci onu bir yedekleme olarak yeniden adlandırır ve yeni bir günlük dosyası oluşturur. Bu özellik, günlük dosyasının kaç tane önceki sürümünün tutulacağını belirtir. Varsayılan değer: `1`. Değerini olarak ayarlarsanız `0` , istemci herhangi bir günlük dosyası geçmişini tutar.

Örnek: `CCMSetup.exe CCMLOGMAXHISTORY=5`

Daha fazla bilgi için bkz. [günlük dosyaları hakkında](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Bu özellik, en fazla günlük dosyası boyutunu bayt cinsinden belirtir. Bir günlük belirtilen boyuta büyüdükçe, istemci onu bir geçmiş dosyası olarak yeniden adlandırır ve yeni bir tane oluşturur. Varsayılan boyut 250.000 bayttır ve en küçük boyut 10.000 bayttır.

Örnek: `CCMSetup.exe CCMLOGMAXSIZE=300000` (300.000 bayt)

### <a name="disablesiteopt"></a>DISABLESITEOPT

`TRUE`Yöneticilerin Configuration Manager Denetim Masası 'ndaki atanmış siteyi değiştirmesini engellemek için bu özelliği olarak ayarlayın.

Örnek: **CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

TRUE olarak ayarlanırsa, bu özellik yönetici kullanıcıların **Configuration Manager** Denetim Masası 'ndaki istemci önbellek klasörü ayarlarını değiştirmesini devre dışı bırakır.  

Örnek: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

İstemcilerin DNS 'de yayımladığınız yönetim noktalarını bulması için bir DNS etki alanı belirtin. İstemci bir yönetim noktası bulduktan sonra, istemciye hiyerarşideki diğer yönetim noktalarını bildirir. Bu davranış, istemcinin DNS 'den bulduğu yönetim noktasının hiyerarşide herhangi biri olabileceği anlamına gelir.

> [!NOTE]
> İstemci yayımlanmış bir yönetim noktasıyla aynı etki alanında ise bu özelliği belirtmeniz gerekmez. Bu durumda, istemcinin etki alanı yönetim noktaları için DNS aramak üzere otomatik olarak kullanılır.

Configuration Manager istemcileri için hizmet konumu olarak DNS yayımlama hakkında daha fazla bilgi için bkz. [hizmet konumu ve istemcilerin atanan yönetim noktalarını belirleme şekli](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).

> [!NOTE]  
> Varsayılan olarak, Configuration Manager DNS yayımlamasını etkinleştirmez.

Örnek: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Configuration Manager istemcileri tarafından gönderilen durum iletilerini alan ve işleyen geri dönüş durum noktasını belirtin.

Daha fazla bilgi için, bkz. [geri dönüş durum noktası](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)gerekip gerekmediğini belirleme.

Örnek: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

Bu özelliği olarak ayarlarsanız `TRUE` , istemci yükleyicisi Microsoft Application Virtualization (App-V) için gereken en düşük sürümü denetlemez.

> [!IMPORTANT]  
> Configuration Manager istemcisini App-V yüklemeden yüklerseniz, [sanal uygulamaları dağıtamazsınız](../../../apps/get-started/deploying-app-v-virtual-applications.md).

Örnek: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

Bu özelliği etkinleştirdiğinizde, istemci durumu raporlar, ancak bulduğu sorunları düzeltmez.

Örnek: `CCMSetup.exe NOTIFYONLY=TRUE`

Daha fazla bilgi için bkz. [istemci durumunu yapılandırma](configure-client-status.md).

### <a name="provisionts"></a>PROVISIONTS

<!--5526972-->

Sürüm 2002 ' den başlayarak, bu özelliği kullanarak, bir istemcide siteye başarıyla kaydolduktan sonra bir görev sırası başlatın.

Örneğin, Windows Autopilot ile yeni bir Windows 10 cihaz sağlacaksınız, Microsoft Intune için otomatik olarak kaydedin ve sonra ortak yönetim için Configuration Manager istemcisini yükleyebilirsiniz. Bu yeni seçeneği belirtirseniz, yeni sağlanan istemci daha sonra bir görev dizisi çalıştırır. Bu işlem, uygulamaları ve yazılım güncelleştirmelerini yüklemek veya ayarları yapılandırmak için ek esneklik sağlar.

Aşağıdaki işlemi kullanın:

1. Uygulamaları yüklemek, yazılım güncelleştirmelerini yüklemek ve ayarları yapılandırmak için [işletim sistemi olmayan dağıtım görev dizisi oluşturun](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md) .

1. [Bu görev dizisini](../../../osd/deploy-use/deploy-a-task-sequence.md) yeni yerleşik koleksiyona, **tüm sağlama cihazlarına**dağıtın. Örneğin, görev dizisi dağıtım KIMLIĞINI aklınızda yapın `PRI20001` .

1. [Configuration Manager istemcisini](deploy-clients-to-windows-computers.md#BKMK_Manual) bir cihaza yükleyip şu özelliği ekleyin: `PROVISIONTS=PRI20001` . Bu özelliğin değerini görev sırası dağıtım KIMLIĞI olarak ayarlayın.

    - İstemciyi ortak yönetim kaydı sırasında Intune 'dan yüklüyorsanız bkz. [İnternet tabanlı cihazları ortak yönetim için hazırlama](../../../comanage/how-to-prepare-Win10.md).

      > [!NOTE]
      > Bu yöntem ek önkoşullara sahip olabilir. Örneğin, siteyi Azure Active Directory kaydetme veya içerik etkinleştirilmiş bir bulut yönetimi ağ geçidi oluşturma.

İstemci yüklenip siteye doğru şekilde kaydolduktan sonra, başvurulan görev dizisini başlatır. İstemci kaydı başarısız olursa, görev dizisi başlatılmaz.

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

İstemcide yanlış Configuration Manager güvenilen kök anahtarı varsa, yeni güvenilen kök anahtarı almak için güvenilir bir yönetim noktasıyla bağlantı kuramıyor. Eski güvenilen kök anahtarı kaldırmak için bu özelliği kullanın. Bu durum, bir istemciyi bir site hiyerarşisinden diğerine taşıdığınızda ortaya çıkabilir. Bu özellik HTTP ve HTTPS istemci iletişimini kullanan istemciler için geçerlidir. Daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Örnek: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SıTEREASSIGN

[Smssitekodu = Auto](#smssitecode)ile kullanıldığında istemci yükseltmeleri için otomatik site yeniden atamaya izin vermez.

Örnek: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

İstemci bilgisayarda istemci önbellek klasörünün konumunu belirtir. Varsayılan olarak, önbellek konumu olur `%WinDir%\ccmcache` .

Örnek: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

İstemci önbellek klasörü konumunu denetlemek için [**SMSCACHEFLAGS**](#smscacheflags) özelliğiyle birlikte bu özelliği kullanın. Örneğin, istemci önbellek klasörünü kullanılabilir en büyük istemci disk sürücüsüne yüklemek için:`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

İstemci önbellek klasörü için diğer yükleme ayrıntılarını belirtmek için bu özelliği kullanın. **SMSCACHEFLAGS** özelliklerini tek tek veya noktalı virgülle () ayırarak birlikte kullanabilirsiniz `;` .

Bu özelliği eklemezseniz:

- İstemci, [**smscachedir**](#smscachedir) özelliğine göre önbellek klasörünü yüklüyor
- Klasör sıkıştırılmadı
- İstemci, önbelleğin MB cinsinden boyut sınırı olarak [**SMSCachesize**](#smscachesize) özelliğini kullanır

Var olan bir istemciyi yükselttiğinizde, istemci yükleyicisi bu özelliği yoksayar.

#### <a name="values-for-the-smscacheflags-property"></a>SMSCACHEFLAGS özelliği için değerler

- **Percentdiskspace**: önbellek boyutunu *Toplam* disk alanının yüzdesi olarak ayarlayın. Bu özelliği belirtirseniz, [**SMSCachesize**](#smscachesize) öğesini de bir yüzde değerine ayarlayın.

- **Yüztfreediskspace**: önbellek boyutunu *boş* disk alanının yüzdesi olarak ayarlayın. Bu özelliği belirtirseniz, [**SMSCachesize**](#smscachesize) değerini yüzde değeri olarak da ayarlayın. Örneğin, diskte 10 MB boş yer vardır ve bunu belirtirsiniz `SMSCACHESIZE=50` . İstemci yükleyicisi önbellek boyutunu 5 MB olarak ayarlar. Bu özelliği **Percentdiskspace** özelliğiyle kullanamazsınız.

- **Maxdrive**: önbelleği, kullanılabilir en büyük diske yükler. [**Smscachedir**](#smscachedir) özelliği ile bir yol belirtirseniz, istemci yükleyicisi bu değeri yoksayar.

- **Maxdrivespace**: önbelleği en fazla boş alana sahip disk sürücüsüne yükler. [**Smscachedir**](#smscachedir) özelliği ile bir yol belirtirseniz, istemci yükleyicisi bu değeri yoksayar.

- **NTFSONLY**: önbelleği yalnızca bir NTFS biçimli disk sürücüsüne yükler. [**Smscachedir**](#smscachedir) özelliği ile bir yol belirtirseniz, istemci yükleyicisi bu değeri yoksayar.

- **Sıkıştır**: önbelleği sıkıştırılmış bir biçimde depolayın.

- **Failifnospace**: önbelleği yüklemek için yeterli alan yoksa Configuration Manager istemcisini kaldırın.

Örnek: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> İstemci ayarları, istemci önbelleği klasör boyutunu belirtmek için kullanılabilir. Eklenen söz konusu istemci ayarları, istemci önbelleğinin boyutunu belirtmek üzere client.msi özelliği olarak SMSCACHESIZE kullanımının yerini alır. Daha fazla bilgi için bkz. [Önbellek boyutu için istemci ayarları](about-client-settings.md#client-cache-settings).  

Var olan bir istemciyi yükselttiğinizde, istemci yükleyicisi bu ayarı yoksayar. İstemci, yazılım güncelleştirmelerini indirdiğinde önbellek boyutunu da yoksayar.

Örnek: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> Bir istemciyi yeniden yüklerseniz, daha önce olduğu gibi, önbellek boyutunu daha küçük olacak şekilde ayarlamak için **SMSCachesize** veya **SMSCACHEFLAGS** kullanamazsınız. Önceki boyut en küçük değerdir.

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

İstemci yükleyicisinin yapılandırma ayarlarını denetlediği konumu ve sırayı belirtmek için bu özelliği kullanın. Her biri belirli bir yapılandırma kaynağını tanımlayan bir veya daha fazla karakter dizesidir:

- `R`: Kayıt defterindeki yapılandırma ayarlarını kontrol edin.

  Daha fazla bilgi için bkz. [istemci yükleme özellikleri sağlama](deploy-clients-to-windows-computers.md#BKMK_Provision).

- `P`: Komut satırındaki yükleme özelliklerinde yapılandırma ayarlarını kontrol edin.

- `M`: Eski bir istemciyi yükselttiğinizde mevcut ayarları kontrol edin.

- `U`: Yüklü istemciyi daha yeni bir sürüme yükseltin ve atanan site kodunu kullanın.

Varsayılan olarak, istemci yükleyicisi kullanır `PU` . Önce yükleme özelliklerini ( `P` ) ve ardından var olan ayarları ( `U` ) denetler.  

Örnek: `CCMSetup.exe SMSCONFIGSOURCE=RP`

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

İstemcinin Windows İnternet Ad Hizmeti'ni (WINS) kullanarak HTTP bağlantılarını kabul eden bir yönetim noktası bulup bulmayacağını belirtir. İstemciler, Active Directory Domain Services veya DNS 'de bir yönetim noktası bulamadıklarında bu yöntemi kullanır.

Bu özellik, istemcinin ad çözümlemesi için WINS kullanıp kullanmadığını etkilemez.

Bu özellik için iki farklı mod yapılandırabilirsiniz:

- **Nowins**: Bu değer, bu özellik için en güvenli ayardır. İstemcilerin WINS 'de bir yönetim noktası bulmasını engeller. Bu ayarı kullandığınızda, istemcilerin intranette yönetim noktası bulmak için alternatif bir yöntemi olması gerekir. Örneğin, Active Directory Domain Services veya DNS yayımı.

- **WINSSECURE** (varsayılan): Bu modda, HTTP iletişimi kullanan bir istemci, yönetim noktası bulmak için WINS kullanabilir. Ancak, yönetim noktasına başarıyla bağlanmadan önce istemcide güvenilen kök anahtarının kopyası olması gerekir. Daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Örnek: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Configuration Manager istemcisinin kullanması için bir başlangıç yönetim noktası belirtir.  

> [!IMPORTANT]  
> Yönetim noktası yalnızca HTTPS üzerinden istemci bağlantılarını kabul ediyorsa, yönetim noktası adını ile önek yapın `https://` .

Örnekler:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

İstemci Active Directory Domain Services Configuration Manager güvenilen kök anahtarı alamazsanız, anahtarı belirtmek için bu özelliği kullanın. Bu özellik HTTP ve HTTPS iletişimi kullanan istemciler için geçerlidir. Daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Örnek: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> Site sunucusundaki MobileClient. tcf dosyasından sitenin güvenilen kök anahtarı için değeri alın. Daha fazla bilgi için bkz. [bir dosya kullanarak güvenilir kök anahtarla bir Istemciyi önceden sağlama](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file).

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

Configuration Manager güvenilen kök anahtarını yeniden yüklemek için bu özelliği kullanın. Bu, güvenilen kök anahtarı içeren bir dosyanın tam yolunu ve adını belirtir. Bu özellik HTTP ve HTTPS istemci iletişimini kullanan istemciler için geçerlidir. Daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Örnek: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

Site sunucusunda, dışarıya aktarılmış otomatik olarak imzalanan sertifikanın tam yolunu ve adını belirtir. Site sunucusu bu sertifikayı **SMS** sertifika deposunda depolar. Konu adı **site sunucusu** ve kolay adı **site sunucusu imzalama sertifikası**olur.

Örnek: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

Bu özellik, istemciyi atadığınız bir Configuration Manager sitesini belirtir. Bu değer üç karakterli bir site kodu veya kelime olabilir `AUTO` . `AUTO`Bu özelliği belirtirseniz veya belirtmezseniz, istemci, Active Directory Domain Services veya belirtilen bir yönetim noktasından site atamasını saptamaya çalışır. `AUTO`İstemci yükseltmelerini etkinleştirmek için, Ayrıca, [Sıtereassign = true](#sitereassign)olarak ayarlayın.

> [!NOTE]  
> Ayrıca, [**CCMHOSTNAME**](#ccmhostname) özelliğine sahip bir internet tabanlı yönetim noktası belirtirseniz, `AUTO` **smssitekodu**ile kullanmayın. Site kodunu belirterek istemciyi doğrudan sitesine atayın.

Örnek: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a>Sertifika seçim ölçütleri için öznitelik değerleri

Configuration Manager, PKI sertifika seçim ölçütleri için aşağıdaki öznitelik değerlerini destekler:

|OID özniteliği|Ayırt Edici Ad özniteliği|Öznitelik tanımı|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|Etki alanı bileşeni|  
|1.2.840.113549.1.9.1|E veya E-posta|E-posta adresi|  
|2.5.4.3|CN|Ortak ad|  
|2.5.4.4|SN|Konu adı|  
|2.5.4.5|SERIALNUMBER|Seri numarası|  
|2.5.4.6|C|Ülke kodu|  
|2.5.4.7|L|Konum|  
|2.5.4.8|S veya ST|Eyalet veya bölge adı|  
|2.5.4.9|STREET|Açık adres|  
|2.5.4.10|O|Kuruluş adı|  
|2.5.4.11|OU|Kurum birimi|  
|2.5.4.12|T veya Title|Başlık|  
|2.5.4.42|G veya GN veya GivenName|Ad|  
|2.5.4.43|I veya Initials|Baş harfler|  
|2.5.29.17|(değer yok)|Konu Diğer Adı|  
