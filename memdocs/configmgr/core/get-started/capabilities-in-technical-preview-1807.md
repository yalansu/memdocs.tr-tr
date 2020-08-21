---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview dalı sürüm 1807 ' de bulunan yeni özellikler hakkında bilgi edinin.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 8ead53c71e336001ac820a437fa67758c6375cbd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694381"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Configuration Manager Technical Preview sürüm 1807 ' deki yetenekler 

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1807 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Teknik Önizleme sitenize yeni özellikler eklemek ve güncelleştirmek için bu sürümü yükler. 

Bu güncelleştirmeyi yüklemeden önce [Teknik Önizleme](technical-preview.md) makalesini gözden geçirin. Bu makalede, Technical Preview kullanımı, sürümler arasında nasıl güncelleştirme yapılacağı ve geri bildirimde bulunmak için genel gereksinimler ve sınırlamalar tamamladığınızda tercihinize.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Bilinen sorunlar 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a> Office 365 yazılım güncelleştirmeleriyle ilgili sorunlar
<!--521365-->
Technical Preview şube sürümlerini 1806 ve 1806,2 kullanarak Office 365 güncelleştirmelerini yönetiyorsanız, istemciler üzerinde yüklenemeyebilir. 

#### <a name="workaround"></a>Geçici çözüm
- Office 365 için mevcut dağıtım paketlerini ve yazılım güncelleştirme gruplarını silin.  

- 31 Temmuz 2018 ' den başlayarak Office 365 yazılım güncelleştirmelerini eşitleyin ve yalnızca en son güncelleştirmeleri dağıtın.  



</br>

**Aşağıdaki bölümlerde bu sürümde denenecek yeni özellikler açıklanır:**  


## <a name="community-hub"></a><a name="bkmk_hub"></a> Topluluk Merkezi
<!--1357766-->

Topluluk Merkezi, yararlı Configuration Manager nesnelerini başkalarıyla paylaşmak için merkezi bir konumdur. Configuration Manager konsolundaki Yeni **topluluk** çalışma alanına bakın ve **hub** düğümünü seçin. Aşağıdaki Configuration Manager nesne türlerini indirmek için Topluluk Merkezi kullanın: 
- Betikler
- Yapılandırma öğeleri

![Configuration Manager konsolu, topluluk çalışma alanı, hub düğümü](media/1357766-hub.png)

Kullanılabilir bir öğe hakkında daha fazla ayrıntı görmek için hub 'da tıklatın. Ayrıntılar sayfasında, öğeyi almak için **İndir** ' e tıklayın. Hub 'dan bir öğe indirdiğinizde, bu, sitenize otomatik olarak eklenir. 

![Configuration Manager konsolu, topluluk çalışma alanı, hub düğümü, Ayrıntılar sayfası](media/1357766-hub-details.png)

**Topluluk** çalışma alanı aşağıdaki düğümleri de içerir:

- **Belgeler**: Configuration Manager [belge kitaplığını](/sccm/) görüntüler  

- **Geri bildirim**: Configuration Manager [UserVoice sitesini](https://configurationmanager.uservoice.com/) görüntüler  


### <a name="prerequisites"></a>Ön koşullar

- İstemci IŞLETIM sisteminde Configuration Manager konsolunu kullanın.  

    - Alternatif olarak, ancak önerilmemiştir: bir sunucu IŞLETIM sisteminde [Internet Explorer: Artırılmış Güvenlik Yapılandırması](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10))'nı devre dışı bırakın.

- Konsola sahip olan bilgisayar için internet erişimi ve aşağıdaki sitelerle bağlantı gerekir:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Bilinen sorun

Hub 'a katkıda bulunan öğeler şu anda bu sürümde kullanılamıyor. 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a> Çevrimdışı işletim sistemi görüntüsü bakımı için sürücüyü belirtin  
<!--1358924-->

[UserVoice geri bildirimlerinizi](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive)temel alarak, artık Configuration Manager işletim sistemi görüntülerinin çevrimdışı bakımı sırasında kullanılan sürücüyü belirtin. Bu işlem geçici dosyalarla büyük miktarda disk alanı tüketebilir, bu nedenle kullanılacak sürücüyü seçme esnekliği sağlar. 


### <a name="try-it-out"></a>Deneyin!

Görevleri tamamlamayı deneyin. Daha sonra bu özelliği kullanarak düşüncelerinizi [geri](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin. Şeritte, **site bileşenlerini Yapılandır** ' a tıklayın ve **yazılım güncelleştirme noktası**' nı seçin.  

2. **Çevrimdışı bakım** sekmesine geçin ve **görüntülerin çevrimdışı Bakımı tarafından kullanılacak yerel bir sürücü**için seçeneği belirtin.  

Varsayılan olarak, bu ayar **otomatiktir**. Bu değerle Configuration Manager yüklendiği sürücüyü seçer. 

Çevrimdışı bakım sırasında, Configuration Manager geçici dosyaları klasöründe depolar `<drive>:\ConfigMgr_OfflineImageServicing` . Ayrıca, işletim sistemi görüntülerini bu klasöre bağlar. 

**Offlineservicingmgr. log** günlük dosyasını gözden geçirin. 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a> Intune 'dan ortak yönetilen cihaz eşitleme etkinliği
<!--1358565-->

Configuration Manager konsolunda, ortak yönetilen bir cihazın Microsoft Intune birlikte etkin olup olmadığını gösterir. Bu durum, [Intune veri ambarından](/intune/reports-nav-create-intune-reports)alınan verileri temel alır. Configuration Manager konsolundaki **Istemci durumu** panosu, **Intune kullanan etkin olmayan istemcileri**gösterir. Bu yeni kategori, Configuration Manager ile etkin olmayan, ancak önceki haftada Intune hizmeti ile eşitlenen, ortak yönetilen cihazlar içindir.


### <a name="try-it-out"></a>Deneyin!

Görevleri tamamlamayı deneyin. Daha sonra bu özelliği kullanarak düşüncelerinizi [geri](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

Sitenizi ortak yönetim için zaten ayarladıysanız: 

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **ortak yönetim** düğümünü seçin. Şeritteki **Özellikler** ' e tıklayın.  

2. **Raporlama** sekmesine geçin. **oturum aç** ' a tıklayın ve kimlik doğrulaması yapın. Ardından, Intune veri ambarı için okuma izinlerini etkinleştirmek üzere **Güncelleştir** ' e tıklayın.  

3. Site Intune ile eşitlendikten sonra **izleme** çalışma alanına gidin ve **istemci durumu** düğümünü seçin. **Genel Istemci durumu** bölümünde, **Intune kullanarak etkin olmayan istemciler**için satıra bakın.  

Ortak yönetimi etkinleştirme hakkında daha fazla bilgi için bkz. [Windows 10 cihazlar Için ortak yönetim](../../comanage/overview.md).



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a> Uygulamaları onarma
<!--1357866-->

[UserVoice geri bildirimlerinizi](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application)temel alarak, Windows Installer ve betik yükleyicisi dağıtım türleri için bir onarım komut satırı belirtin. 


### <a name="try-it-out"></a>Deneyin!

Görevleri tamamlamayı deneyin. Daha sonra bu özelliği kullanarak düşüncelerinizi [geri](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda, bir Windows Installer veya betik yükleyici dağıtım türünün özelliklerini açın.  

2. **Programlar** sekmesine geçin. **programı Onar** komutunu belirtin.  

3. Uygulamayı dağıtın. Dağıtımın **dağıtım ayarları** sekmesinde, **son kullanıcıların bu uygulamayı onarmayı denemesine izin verme**seçeneğini etkinleştirin.  


### <a name="known-issue"></a>Bilinen sorun

Yazılım Merkezi 'nde kullanıcıların uygulamayı **onarması** için yeni düğme bu sürümde görünmez değildir.  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a> Uygulama isteklerini e-postayla onaylama
<!--1321550-->

Uygulama onay istekleri için e-posta bildirimlerini yapılandırın. Bir Kullanıcı bir uygulama istediğinde, bir e-posta alırsınız. Configuration Manager konsolu gerekmeden isteği onaylamak veya reddetmek için e-postadaki bağlantılar ' a tıklayın.


### <a name="prerequisites"></a>Ön koşullar

#### <a name="to-send-email-notifications"></a>E-posta bildirimleri göndermek için
- [İsteğe bağlı özelliği](../servers/manage/install-in-console-updates.md#bkmk_options) **cihaz başına Kullanıcı için uygulama isteklerini Onayla**' yı etkinleştirin.  

- [Uyarılar için e-posta bildirimini](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts)yapılandırın.  

#### <a name="to-approve-or-deny-requests-from-email"></a>E-postadaki istekleri onaylamak veya reddetmek için
Bu önkoşulları yapılandırmazsanız site, isteği onaylama veya reddetme bağlantısı olmadan uygulama istekleri için e-posta bildirimi gönderir.  

- Site özelliklerinde, **Bu sitedeki tüm sağlayıcı rolleri IÇIN REST uç noktasını etkinleştirin ve bulut yönetimi ağ geçidi trafiğine Configuration Manager izin verin**. Daha fazla bilgi için bkz. [OData uç noktası veri erişimi](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access).  

    - REST uç noktasını etkinleştirdikten sonra SMS_EXEC hizmetini yeniden başlatın

- [Bulut yönetimi ağ geçidi](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- Siteyi **bulut yönetimi** için [Azure hizmetlerine](../servers/deploy/configure/azure-services-wizard.md) ekleme  

    - [Azure AD Kullanıcı bulmayı](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) etkinleştir  

    - Azure AD 'de bu yerel uygulama için aşağıdaki ayarları el ile yapılandırın:  

        - **Yeniden yönlendirme URI 'si**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth` . Bulut yönetimi ağ geçidi (CMG) hizmetinin tam etki alanı adını (FQDN) kullanın, örneğin, GraniteFalls.Contoso.com.   

        - **Manifest**: **oauth2AllowImplicitFlow** değerini true olarak ayarlayın: `"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Deneyin!

Görevleri tamamlamayı deneyin. Daha sonra bu özelliği kullanarak düşüncelerinizi [geri](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda, bir uygulamayı bir kullanıcı koleksiyonuna kullanılabilir olarak dağıtın. **Dağıtım ayarları** sayfasında, onay için etkinleştirin. Ardından, bildirim almak için *tek* bir e-posta adresi girin.  

     > [!Note]  
     > Azure AD kuruluşunuzda e-postayı alan herkes isteği onaylayabilir. İşlem yapmak istemediğiniz müddetçe e-postayı başkalarına iletmeyin.  

2. Bir kullanıcı olarak, uygulamayı Yazılım Merkezi 'nde isteyin.  

3. Aşağıdaki örneğe benzer bir e-posta bildirimi alırsınız:  

![Uygulama onayı için örnek e-posta bildirimi](media/1321550-email.png)

> [!Note]  
> Onaylama veya reddetme bağlantısı, tek seferlik kullanım içindir. Örneğin, bildirimleri almak için bir grup diğer adı yapılandırırsınız. Meg, isteği onaylar. Şimdi deneme yanılması isteği reddedemez.  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a> Betik çıktısına iyileştirme
<!--1236459-->

Artık ham veya yapılandırılmış JSON biçiminde ayrıntılı betik çıktısını görüntüleyebilirsiniz. Bu biçimlendirme, çıktının okunmasını ve çözümlenmesini kolaylaştırır. Betik geçerli bir JSON biçimli metin döndürürse, ayrıntılı çıktıyı **JSON çıktısı** veya **Ham çıktı**olarak görüntüleyin. Aksi takdirde tek seçenek **betik çıktıdır**. 

#### <a name="example-script-output-is-valid-json"></a>Örnek: betik çıkışı geçerli bir JSON
Komutundaki `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Örnek: betik çıkışı geçerli bir JSON değil
Komutundaki `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Deneyin!

Görevleri tamamlamayı deneyin. Daha sonra bu özelliği kullanarak düşüncelerinizi [geri](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Cihaz Koleksiyonları** düğümünü seçin. Bir koleksiyona sağ tıklayın ve **Betiği Çalıştır**' ı seçin. Betikleri oluşturma ve çalıştırma hakkında daha fazla bilgi için, bkz. [Configuration Manager konsolundan PowerShell betikleri oluşturma ve çalıştırma](../../apps/deploy-use/create-deploy-scripts.md).  

2. Hedef koleksiyonda bir betiği çalıştırın.  

3. Betiği Çalıştır sihirbazının **betik durumu izleme** sayfasında, alt kısımdaki **Özet** sekmesini seçin. En üstteki iki açılan listeyi **betik çıkışı** ve **veri tablosu**ile değiştirin. Ardından, **ayrıntılı çıkış** iletişim kutusunu açmak için sonuçlar satırına çift tıklayın.  

4. Betiği Çalıştır sihirbazının **betik durumu izleme** sayfasında, alt kısımdaki **ayrıntıları Çalıştır** sekmesini seçin. Bu cihaz için ayrıntılı çıkış iletişim kutusunu açmak için bir sonuç satırına çift tıklayın.  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a> Üçüncü taraf yazılım güncelleştirmelerine yönelik geliştirme
<!--1358714-->

Artık özel katalogların özelliklerini değiştirebilirsiniz.

Daha fazla bilgi için bkz. [özel kataloglar Için üçüncü taraf yazılım güncelleştirmeleri desteği](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate).



## <a name="next-steps"></a>Sonraki adımlar

Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Technical Preview](technical-preview.md).    

Configuration Manager farklı dalları hakkında daha fazla bilgi için bkz. [hangi Configuration Manager dalını kullanmalıyım?](../understand/which-branch-should-i-use.md)