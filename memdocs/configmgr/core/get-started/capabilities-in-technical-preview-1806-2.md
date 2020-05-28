---
title: Technical Preview 1806,2
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview sürüm 1806,2 ' de bulunan yeni özellikler hakkında bilgi edinin.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b7643c73d2e9dad00e926bdc3db905016c45860a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905212"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Configuration Manager için Technical Preview 1806,2 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1806,2 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Technical Preview sitenize güncelleştirmek ve yeni özellikleri eklemek için yükleyebilirsiniz. 

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

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a>İstemciler otomatik olarak güncelleştirmez
<!--518760-->
Sürüm 1806,2 ' e güncelleştirirken site, site sunucusunda bekleyen bir yeniden başlatmaya neden olabilecek SQL Native Client de güncelleştirir. Bu gecikme, belirli dosyaların güncelleştirilmesine neden olur ve bu da otomatik istemci yükseltmesini etkiler.

#### <a name="workarounds"></a>Geçici Çözümler
Configuration Manager 1806,2 sürümüne *güncelleştirmeden önce* SQL Native Client el ile yükselterek bu sorundan kaçının. Daha fazla bilgi için, [SQL Server 2012 Native Client için en son bakım güncelleştirmesine](https://www.microsoft.com/download/details.aspx?id=50402)bakın.

Sitenizi zaten güncelleştirdiyseniz, otomatik istemci yükseltmesi ve istemci gönderimi çalışmaz. Birçok yeni özelliği tam olarak test etmek için istemcileri güncelleştirmeniz gerekir. Aşağıdaki işlemi kullanarak Technical Preview istemcilerinizi el ile güncelleştirin:  

1. İstemci kaynak dosyalarını site sunucusundaki Configuration Manager yükleme dizininin **Cmuclient** klasöründe bulun. Örneğin, `C:\Program Files\Configuration Manager\CMUClient`  

2. Tüm CMUClient klasörünü istemci cihazına kopyalayın. Örneğin, `C:\Temp\CMUClient`  

    Bu konum, istemcilerden erişilebilen bir ağ paylaşımından olabilir.  

3. Yükseltilmiş bir komut isteminden aşağıdaki komut satırını çalıştırın:`C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Technical Preview sürüm 1806,2 sitenize yeni bir istemci yüklüyorsanız, bu işlemi kullanın. 

> [!Important]  
> `/MP`Bu senaryoda komut satırı parametresini kullanmayın. Bu parametre, üzerinden önceliklidir `/source` ve CCMSetup 'ın istemci içeriğini yönetim noktasından veya dağıtım noktasından indirmesini sağlar.
> 
> SMSSITEKODU veya CCMLOGLEVEL gibi komut satırı özelliklerinin kullanımı, ancak var olan bir istemciyi yükseltirken gerekli olmaması gerekir. 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a>Sürüm 1806,2, yaklaşık Configuration Manager sürümünde 1806 sürümünü gösterir
<!--518148-->
Technical Preview sürüm 1806,2 ' e yükselttikten sonra, konsolunun sol üst köşesinden **ilgili Configuration Manager** penceresini açarsanız, **Sürüm 1806**' yi de gösterir. 

#### <a name="workaround"></a>Geçici çözüm
1806 ile 1806,2 arasındaki farkı öğrenmek için **site sürümü** özelliğini kullanın:

| Site sürümü  | Sürüm
|---------|---------|
| 5,0.**8672**. 1000 | 1806 |
| 5,0.**8685**. 1000 | 1806,2 |
 


</br>

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a>Aşamalı dağıtımlarda iyileştirmeler

Bu sürüm, [aşamalı dağıtımlar](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)için aşağıdaki geliştirmeleri içerir:
- [Aşamalı dağıtım durumu](#bkmk_pod-monitor)
- [Uygulamaların aşamalı dağıtımı](#bkmk_pod-app)
- [Aşamalı dağıtımlar sırasında aşamalı dağıtım](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a>Aşamalı dağıtım durumu
<!--1358577-->
Aşamalı dağıtımlar artık yerel bir izleme deneyimine sahiptir. **İzleme** çalışma alanındaki **dağıtımlar** düğümünden aşamalı bir dağıtım seçin ve ardından şeritte **aşamalı dağıtım durumu** ' nu tıklatın.

![İki aşamaların durumunu gösteren aşamalı dağıtım durumu panosu](media/1358577-phased-deployment-status.png)

Bu Pano, dağıtımdaki her aşama için aşağıdaki bilgileri gösterir:  

- **Toplam cihaz sayısı**: Bu aşamada kaç cihaz hedeflenmiştir.  

- **Durum**: Bu aşamanın geçerli durumu. Her aşama aşağıdaki durumlardan birinde olabilir:  

    - **Dağıtım oluşturuldu**: aşamalı dağıtım, bu aşama için, yazılımın koleksiyona bir dağıtımını oluşturdu. İstemciler bu yazılımla etkin bir şekilde hedeflenmiştir.  

    - **Bekliyor**: önceki aşama, bu aşamaya devam etmek için dağıtımın başarı ölçütlerine henüz ulaşmadı.  

    - **Askıya alındı**: yönetici dağıtımı askıya aldı.  

- **İlerleme**: istemcilerden renk kodlu dağıtım durumları. Örneğin: başarılı, devam ediyor, hata, gereksinimler karşılanmadı ve bilinmiyor. 


#### <a name="known-issue"></a>Bilinen sorun
Aşamalı dağıtım durumu panosu aynı aşama için birden çok satır gösterebilir.<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a>Uygulamaların aşamalı dağıtımı
<!--1358147-->
Uygulamalar için aşamalı dağıtımlar oluşturun. Aşamalı dağıtımlar, özelleştirilebilir ölçütlere ve gruplara göre düzenlenmiş, sıralı bir yazılım dağıtımını düzenlemenize olanak tanır.

Configuration Manager konsolunda, **yazılım kitaplığı**' na gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar**' ı seçin. Bir uygulama seçin ve ardından şeritte **aşamalı dağıtım oluştur** ' a tıklayın. 

Uygulama aşamalı dağıtımının davranışı, görev dizileri için ile aynıdır. Daha fazla bilgi için bkz. [bir görev dizisi için aşamalı dağıtımlar oluşturma](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

#### <a name="prerequisite"></a>Önkoşul
Aşamalı dağıtımı oluşturmadan önce uygulamanın içeriğini bir dağıtım noktasına dağıtın.<!--518293-->

#### <a name="known-issue"></a>Bilinen sorun
Bir uygulama için el ile aşamalar oluşturamazsınız. Sihirbaz, uygulama dağıtımları için otomatik olarak iki aşama oluşturur.


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a>Aşamalı dağıtımlar sırasında aşamalı dağıtım
<!--1358578-->
Aşamalı bir dağıtım sırasında, her bir aşamadaki dağıtım artık aşamalı olarak gerçekleşebilir. Bu davranış, dağıtım sorunları riskini azaltmaya yardımcı olur ve içeriğin istemcilere dağıtılması nedeniyle ağdaki yükü azaltır. Site, her bir aşamanın yapılandırmasına bağlı olarak yazılımı aşamalı olarak kullanılabilir hale getirir. Bir aşamadaki her istemcinin, yazılımın kullanılabilir hale getirilme zamanına göre son tarihi vardır. Kullanılabilir saat ve son tarih arasındaki zaman penceresi, bir aşamadaki tüm istemciler için aynıdır. 

Aşamalı dağıtım oluşturup bir aşamayı el ile yapılandırdığınızda, aşama Ekleme sihirbazının **aşama ayarları** sayfasında veya aşamalı dağıtım oluşturma Sihirbazı ' nın **Ayarlar** sayfasında, şu seçeneği yapılandırın: **kademeli olarak bu yazılımın bu süre içinde kullanılabilmesini sağlama (gün)**. Bu ayarın varsayılan değeri **0**' dır, bu nedenle varsayılan olarak dağıtım kısıtlanmıyor.

> [!Note]  
> Bu seçenek şu anda yalnızca Görev sıralarının aşamalı dağıtımları için kullanılabilir.  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a>Yeni Windows uygulama paketi biçimleri için destek
<!--1357427-->
Configuration Manager artık yeni Windows 10 uygulama paketi (. msix) ve uygulama paketi (. msixdemeti) biçimlerinin dağıtımını desteklemektedir. En son [Windows Insider Preview](https://insider.windows.com/) derlemeleri Şu anda bu yeni biçimleri desteklemektedir.

MALTıYA genel bakış için [maltıya daha yakından](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix)bakın.

Yeni bir MSIX uygulaması oluşturma hakkında bilgi için bkz. [Insider Build 17682 ' de sunulan Msix desteği](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Ön koşullar
- En az Windows Insider Preview derleme 17682 çalıştıran bir Windows 10 istemcisi
- MSIX biçimindeki bir Windows uygulama paketi

### <a name="try-it-out"></a>Deneyin!
Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda [bir uygulama oluşturun](../../apps/deploy-use/create-applications.md). 
2. **Windows uygulama paketi ( \* . appx, \* . appxdemeti, \* . msix, \* . msixdemeti)** olarak uygulama yükleme dosya **türünü** seçin.
3. En son Windows Insider Preview yapısını çalıştıran istemciye [uygulamayı dağıtın](../../apps/deploy-use/deploy-applications.md) .



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a>İstemci anında iletme güvenliğine iyileştirme
<!--1358204-->
Configuration Manager istemcisini yüklemek için [Client Push](../clients/deploy/plan/client-installation-methods.md#client-push-installation) yöntemini kullanırken, site sunucusu yüklemeyi başlatmak için istemciye bir uzak bağlantı oluşturur. Bu sürümden itibaren, site bağlantı kurulmadan önce NTLM 'ye geri dönüşe izin vermeyerek Kerberos karşılıklı kimlik doğrulaması gerektirebilir. Bu geliştirme, sunucu ve istemci arasındaki iletişimin güvenliğini sağlamaya yardımcı olur. 

Güvenlik ilkelerinize bağlı olarak, ortamınız daha eski NTLM kimlik doğrulaması üzerinden Kerberos 'u zaten tercih edebilir veya zorunlu kılabilir. Bu kimlik doğrulama protokollerinin güvenlik konuları hakkında daha fazla bilgi için bkz. [NTLM 'yi kısıtlamak Için Windows güvenlik ilkesi ayarı](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Önkoşul

Bu özelliği kullanmak için istemciler güvenilir bir Active Directory ormanında olmalıdır. Windows 'da Kerberos, karşılıklı kimlik doğrulaması için Active Directory bağımlıdır. 


### <a name="try-it-out"></a>Deneyin!

Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

Siteyi yükselttiğinizde, mevcut davranış devam ettirir. İstemci anında yükleme özelliklerini *açtığınızda* site, Kerberos denetimini otomatik olarak etkinleştirmesine izin vermez. Gerekirse, geri dönüş bağlantısının, daha az güvenli bir NTLM bağlantısı kullanmasına izin verebilirsiniz, bu da önerilmez. 

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler**' i seçin. Hedef siteyi seçin. Şeritte **Istemci yükleme ayarları** ' na tıklayın ve **istemci gönderme yüklemesi**' ni seçin.  

2. Site artık istemci gönderimi için Kerberos denetimini etkinleştirdi. Pencereyi kapatmak için **Tamam**’a tıklayın.  

3. Ortamınız için gerekliyse, Istemci anında yükleme Özellikler penceresi, **genel** sekmesinde **bağlantı geri dönüşü NTLM 'ye izin verme**seçeneğine bakın. Bu seçenek varsayılan olarak devre dışıdır. 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a>Proaktif Bakım için yönetim öngörüleri
<!--1352184,et al-->
Olası yapılandırma sorunlarını vurgulamak için bu sürümde ek yönetim öngörüleri sunulmaktadır. Yeni **proaktif bakım** grubunda aşağıdaki kuralları gözden geçirin:  

- **Kullanılmayan yapılandırma öğeleri**: yapılandırma temelinin parçası olmayan ve 30 günden eski olan yapılandırma öğeleri.  

- **Kullanılmayan önyükleme görüntüleri**: PXE önyüklemesi veya görev dizisi kullanımı için önyükleme görüntülerine başvurulmadı.  

- **Atanmış site sistemleri olmayan sınır grupları**: atanmış site sistemleri olmadan sınır grupları yalnızca site ataması için kullanılabilir.  

- **Üyesi olmayan sınır grupları**: sınır grupları, herhangi bir üyesi yoksa, site atama veya içerik arama için geçerli değildir.  

- **İstemcilere içerik hizmet veren dağıtım noktaları**: son 30 gün içinde istemcilere içerik sunulmayan dağıtım noktaları. Bu veriler, indirme geçmişinin istemcilerinden gelen raporları temel alır.  

- Süre **biten güncelleştirmeler bulundu**: süre dolmayan güncelleştirmeler dağıtım için geçerli değildir.   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a>Ortak yönetilen cihazlar için mobil uygulamalar iş yükünü geçirme
<!--1357892-->
Windows masaüstü uygulamalarını dağıtmak için Configuration Manager kullanmaya devam ederken mobil uygulamaları Microsoft Intune yönetin. Modern uygulamalar iş yükünü geçmek için ortak yönetim özellikleri sayfasına gidin. Kaydırıcı çubuğunu Configuration Manager 'den pilot 'a veya tümüne taşıyın. 

Bu iş yükünü geçirdikten sonra, Intune 'dan dağıtılan kullanılabilir uygulamalar Şirket Portalı kullanılabilir. Configuration Manager 'ten dağıttığınız uygulamalar yazılım merkezi 'nde kullanılabilir. 

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

- [Windows 10 cihazları için ortak yönetim](../../comanage/overview.md)  

- [Microsoft Intune uygulama yönetimi nedir?](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Eş indirmeleri için sınır grubu seçenekleri
<!--1356193-->
Artık sınır grupları ortamınızda içerik dağıtımı üzerinde daha fazla denetim sağlamak için ek ayarlar içerir. Bu sürüm aşağıdaki seçenekleri ekler:  

- **Bu sınır grubunda eş indirmelere Izin ver**: Bu ayar varsayılan olarak etkindir. Yönetim noktası, istemcilere eş kaynakları içeren içerik konumlarının bir listesini sağlar. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Bu seçeneği devre dışı bırakmayı göz önünde bulundurmanız gereken iki yaygın senaryo vardır:  

    - VPN gibi coğrafi olarak dağınık konumlardan sınır içeren bir sınır grubunuz varsa. VPN üzerinden bağlı olduklarından iki istemci aynı sınır grubunda olabilir, ancak içeriğin eş paylaşımı için uygun olmayan büyük ölçüde farklı konumlarda olabilir.  

    - Site ataması için herhangi bir dağıtım noktasına başvurmayan tek bir büyük sınır grubu kullanıyorsanız.  

- **Eş Indirmeleri sırasında yalnızca aynı alt ağdaki eşleri kullanın**: Bu ayar yukarıdaki birine bağımlıdır. Bu seçeneği etkinleştirirseniz, yönetim noktası yalnızca istemciyle aynı alt ağda bulunan içerik konumu listesi eş kaynaklarını içerir.

    Bu seçeneği etkinleştirmeye yönelik yaygın senaryolar:

    - İçerik dağıtımı için sınır grubu tasarımınız, diğer küçük sınır gruplarıyla örtüşen bir büyük sınır grubu içerir. Bu yeni ayar ile, yönetim noktasının istemcilerine sağladığı içerik kaynakları listesi yalnızca aynı alt ağdaki eş kaynakları içerir.

    - Tüm uzak Office konumları için tek bir büyük sınır grubunuz vardır. Bu seçeneği etkinleştirin ve istemciler, konumlar arasında içerik paylaşımı yapmak yerine yalnızca uzak ofis konumundaki alt ağ içindeki içeriği paylaşır.


### <a name="known-issue"></a>Bilinen sorun
Eş kaynak istemcisinde birden fazla IP adresi (IPv4, IPv6 veya her ikisi) varsa, Eş önbelleğe alma çalışmaz. Yeni seçenek, **eş Indirmeleri sırasında yalnızca aynı alt ağdaki eşleri kullanır**, eş kaynağında bırden fazla IP adresi varsa, hiçbir etkisi yoktur.<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a>Özel kataloglar için üçüncü taraf yazılım güncelleştirmeleri desteği
<!--1358714-->
Bu sürüm, [UserVoice geri bildirimlerinizin](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)bir sonucu olarak üçüncü taraf yazılım güncelleştirmeleri desteğiyle daha da yinelenir. [Technical Preview sürüm 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) , yazılım satıcılarından kayıtlı kataloglar olan *iş ortağı katalogları*için destek sağlamıştır. Sağladığınız kataloglar, Microsoft 'a kaydolmayan *özel kataloglar*olarak adlandırılır. Configuration Manager konsoluna özel kataloglar ekleyin.  


### <a name="prerequisites"></a>Ön koşullar 

- [Üçüncü taraf yazılım güncelleştirmelerini](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)ayarlayın. 1. Aşama: özelliği etkinleştirin ve ayarlayın.   

- Dijital olarak imzalanmış yazılım güncelleştirmelerini içeren, dijital olarak imzalanan özel bir katalog.  

- Yönetici aşağıdaki izinleri gerektirir:  

    - Site: oluşturma, değiştirme  


### <a name="try-it-out"></a>Deneyin!

Görevleri tamamlamayı deneyin. Daha sonra nasıl çalıştığını bize bildirmek için [geri bildirim](capabilities-in-technical-preview-1804.md#bkmk_feedback) gönderin.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **yazılım güncelleştirmeleri**' ni genişletin ve **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü seçin. Şeritte **özel Katalog Ekle** ' ye tıklayın.  

2. **Genel** sayfasında, aşağıdaki ayrıntıları belirtin:  

    - **İndirme URL 'si**: özel kataloğun GEÇERLI bir HTTPS adresi.  

    - **Yayımcı**: kataloğu yayımlayan kuruluşun adı.  

    - **Ad**: Configuration Manager konsolunda görüntülenecek kataloğun adı.  

    - **Açıklama**: kataloğun açıklaması.  

    - **Destek URL 'si** (isteğe bağlı): katalogla ilgili yardım almak için bir Web sitesinin GEÇERLI bir HTTPS adresi.  

    - **Destek kişisi** (isteğe bağlı): Katalog hakkında yardım almak için iletişim bilgileri.  

3. Sihirbazı tamamlayın. Sihirbaz yeni kataloğu abone olunamaz durumuna ekler.  

4. Mevcut **kataloğa abone ol** eylemini kullanarak özel kataloğa abone olun. Daha fazla bilgi için bkz. [2. Aşama: bir üçüncü taraf kataloğuna abone olma ve güncelleştirmeleri eşitleme](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Aynı indirme URL 'siyle Katalog ekleyemez ve Katalog özelliklerini düzenleyemezsiniz. Özel bir katalog için yanlış Özellikler belirtirseniz, yeniden eklemeden önce kataloğu silin.  


#### <a name="unsubscribe-from-a-catalog"></a>Katalogdan abonelik kaldırma
Bir kataloğun aboneliğini kaldırmak için, listeden istediğiniz kataloğu seçin ve Şeritteki **abonelik aboneliği kaldır** ' a tıklayın. Bir kataloğun aboneliğini kaldırırsanız, aşağıdaki eylemler ve davranışlar oluşur: 
- Site yeni güncelleştirmelerin eşitlenmesini durduruyor 
- Site, Katalog imzalama ve içerik güncelleştirme için ilişkili sertifikaları engeller. 
- Var olan güncelleştirmeler kaldırılmaz, ancak bunları yayımlayamayabilir veya dağıtamazsınız.

#### <a name="delete-a-custom-catalog"></a>Özel bir katalog silme
Özel katalogları konsolunun aynı düğümünden silin. *Abonelik kaldırma* durumunda özel bir katalog seçin ve **özel kataloğu Sil ' e**tıklayın. Zaten kataloğa abone olduysa, silmeden önce aboneliğinizi kaldırın. İş ortağı kataloglarını silemezsiniz. Özel bir kataloğun silinmesi, bu uygulamayı Katalog listesinden kaldırır. Bu eylem, yazılım güncelleştirme noktanma yayımladığınız yazılım güncelleştirmelerini etkilemez.


### <a name="known-issue"></a>Bilinen sorun
Özel kataloglarda silme eylemi gri renkte, bu nedenle özel katalogları konsolundan silemezsiniz. Bu soruna geçici bir çözüm olarak, site sunucusunda **WBEMTest** aracını kullanın. Ad veya indirme URL 'siyle silmek istediğiniz örnek için sorgu. Örneğin: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"` . Sorgu sonucu penceresinde, nesneyi seçin ve **Sil**' e tıklayın.<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a>Bulut yönetimi özelliklerine yönelik iyileştirmeler

Bu sürüm aşağıdaki geliştirmeleri içerir:  

- Aşağıdaki özellikler artık Azure ABD kamu bulutu 'nın kullanımını desteklemektedir:<!--511980-->  

    - Siteyi [Azure hizmetleri](../servers/deploy/configure/azure-services-wizard.md) aracılığıyla **bulut yönetimi** için ekleme  

    - Azure Resource Manager bir [bulut yönetimi ağ geçidi](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager) dağıtma  

    - [Azure Resource Manager ile bulut dağıtım noktası](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager) dağıtma  

- Müşteriler, şirket içi ağa bağlı Azure Active Directory katılmış cihazlarda Windows 10 sağlamak için Windows AutoPilot kullanıyor. Bu cihazlarda Configuration Manager istemcisini yüklemek veya yükseltmek için, artık **istemcilerin anonim olarak bağlanmasına Izin verecek**şekilde yapılandırılmış bir bulut dağıtım noktası veya şirket içi dağıtım noktası gerekmez. Bunun yerine, bulut etki alanına katılmış bir istemcinin şirket içi HTTP özellikli bir dağıtım noktasıyla iletişim kurmasına izin veren **http site sistemleri için Configuration Manager tarafından oluşturulan sertifikaları kullanmak**üzere site seçeneğini etkinleştirin. Daha fazla bilgi için bkz. [Gelişmiş güvenli istemci iletişimleri](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a>Yeni yazılım güncelleştirmeleri uyumluluk raporu
<!--1357775-->
Yazılım güncelleştirmeleri uyumluluğuna ilişkin raporları görüntülemek, genellikle sitesiyle en son iletişim kurmayan istemcilerden gelen verileri içerir. Yeni bir rapor, belirli bir yazılım güncelleştirme grubu için uyumluluk sonuçlarını "sağlıklı" istemcilere göre filtrelemenize olanak sağlar. Bu rapor, ortamınızdaki etkin istemcilerin daha gerçekçi uyumluluk durumunu gösterir. 
 
Raporu görüntülemek için, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin, **raporlar**' ı genişletin, **yazılım güncelleştirmeleri-bir uyumluluk**' i genişletin ve **Uyumluluk 9 ' un genel durum ve uyumluluk**' i seçin. **Güncelleştirme grubunu**, **koleksiyon adını**ve **istemci sistem** durumunu belirtin.

Rapor aşağıdaki bölümleri içerir:
- **Sağlıklı istemciler ve toplam istemci**sayısı: Bu çubuk grafik, belirtilen dönemde siteyle iletişim kurulan "sağlıklı" istemcileri, belirtilen koleksiyondaki toplam istemci sayısına göre karşılaştırır.
- **Uyumluluk genel bakış**: Bu pasta grafik, belirtilen koleksiyondaki etkin istemcilerde belirli yazılım güncelleştirme grubu için genel uyumluluk durumunu gösterir.
- **Önde gelen 5 makale kimliğiyle uyumlu değil**: Bu çubuk grafik, belirtilen koleksiyondaki etkin istemcilerde uyumsuz olmayan, belirtilen gruptaki ilk beş yazılım güncelleştirmesini görüntüler.
- Raporun en altında, belirtilen gruptaki yazılım güncelleştirmelerini listeleyen daha fazla ayrıntı içeren bir tablo bulunur.



## <a name="next-steps"></a>Sonraki adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).    
