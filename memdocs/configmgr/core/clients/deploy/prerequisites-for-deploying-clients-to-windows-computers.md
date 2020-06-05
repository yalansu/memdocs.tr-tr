---
title: Windows istemci dağıtımı önkoşulları
titleSuffix: Configuration Manager
description: Configuration Manager istemcisini Windows bilgisayarlarına dağıtmaya yönelik önkoşullar hakkında bilgi edinin.
ms.date: 06/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2aa375d0521e6088904ebe9a1f10af83f4bc261f
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428565"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Configuration Manager 'da Windows bilgisayarlarına istemci dağıtmak için Önkoşullar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Ortamınızdaki Configuration Manager istemcilerinin dağıtımı, ürün içinde aşağıdaki dış bağımlılıklara ve bağımlılıklara sahiptir. Ayrıca, her istemci dağıtım yönteminin, istemci yüklemelerinin başarılı olması için karşılanması gereken kendi bağımlılıkları vardır.  

Configuration Manager istemcisi için en düşük donanım ve işletim sistemi gereksinimleri hakkında daha fazla bilgi için bkz. [desteklenen konfigürasyonlar](../../plan-design/configs/supported-configurations.md).  

> [!NOTE]  
> Bu makalede gösterilen yazılım sürüm numaraları yalnızca gerekli minimum sürüm numaralarıdır.  

## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a>Windows istemcileri için Önkoşullar  

Windows cihazlarına Configuration Manager istemcisini yüklerken önkoşulları öğrenmek için aşağıdaki bilgileri kullanın.  

### <a name="dependencies-external-to-configuration-manager"></a>Bağımlılıklar dış Configuration Manager

Bu bileşenlerin birçoğu, Windows 'un varsayılan olarak izin veren hizmetler veya özelliklerdir. Configuration Manager istemcilerinde bu bileşenleri devre dışı bırakın.

|Bileşen|Description|
|---|---|
|Windows Installer|Uygulamalar ve yazılım güncelleştirmeleri için Windows Installer dosyalarının kullanımını desteklemek için gereklidir.|
|Microsoft Arka Plan Akıllı Aktarım Hizmeti (BITS)|İstemci bilgisayar ile Configuration Manager site sistemleri arasında kısıtlanan veri aktarımına izin vermek için gereklidir.|
|Microsoft Görev Zamanlayıcısı|Configuration Manager istemcisinin sistem durumunu düzenli olarak değerlendirmek gibi istemci işlemleri için gereklidir.|
|Microsoft Uzaktan Değişiklikleri Sıkıştırma (RDC)|Ağ üzerinden veri iletimini en uygun hale getirmek için gereklidir.|
|SHA-2 kod imzalama desteği|Sürüm 1906 ' den başlayarak, istemciler SHA-2 kod imzalama algoritması için destek gerektirir. Daha fazla bilgi için bkz. [SHA-2 kod imzalama desteği](#bkmk_sha2).|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a>SHA-2 kod imzalama desteği

<!--SCCMDocs-pr#3404-->
SHA-1 algoritmasındaki zayıf noktalar nedeniyle ve sektör standartlarına uyum sağlamak için, Microsoft artık yalnızca daha güvenli SHA-2 algoritmasını kullanarak Configuration Manager ikililerini imzalar. Eski Windows işletim sistemi sürümleri, SHA-2 kod imzalama desteği için bir güncelleştirme gerektirir. Daha fazla bilgi için bkz. [Windows ve WSUS için 2019 SHA-2 kod imzalama desteği gereksinimi](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus).

Bu işletim sistemi sürümlerini güncelleştirmemeniz durumunda Configuration Manager Client 1906 sürümünü yükleyemezsiniz. Bu davranış, yeni bir istemci yüklemesi ya da önceki bir sürümden güncelleştirilmesi için geçerlidir.

Güncelleştirilmemiş bir Windows sürümünde veya yukarıda listelenen sürümlerden daha eski olan bir istemciyi yönetmeniz gerekiyorsa, Configuration Manager genişletilmiş birlikte çalışabilirlik istemci (EIC) sürüm 1902 ' i kullanın. Daha fazla bilgi için bkz. [genişletilmiş birlikte çalışabilirlik istemcisi](../../understand/interoperability-client.md).

> [!Tip]  
> [Otomatik istemci güncelleştirmesini](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)kullanmıyorsanız ve istemcileri başka bir mekanizmaya güncelleştirirseniz, CCMSetup sürümünü güncelleştirdiğinizden emin olun. CCMSetup 'ın daha eski bir sürümü sürüm 1906 istemci ikili dosyalarında yeni SHA-2 kod imzalama sertifikasını düzgün şekilde doğrulayamayabilir. Örneğin, CCMSetup. exe dosyasını bir dosya paylaşımında kopyalarsanız veya CCMSetup. msi ' yi grup ilkesiyle birlikte kullanabilirsiniz.<!-- 4963362 -->
>
> Aşağıdaki istemci güncelleştirme mekanizmaları etkilenmemelidir:
>
> - Client push yüklemesi: siteden istemci paketini kullanır
> - Yazılım güncelleştirmesi tabanlı yükleme: site güncelleştirmesi WSUS 'ye ikinci olarak
> - Intune MDM ile yönetilen Windows cihazları: Bu mekanizma için desteklenen sürüm, zaten SHA-2 kod imzalamayı destekliyor, ancak en son CCMSetup. msi kullanılması hala önemlidir

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a>Configuration Manager dış bağımlılıklar ve yükleme sırasında otomatik olarak indirilir  

Configuration Manager istemcisinde dış bağımlılıklar vardır. Bu bağımlılıklar, istemci bilgisayardaki işletim sistemi sürümüne ve yüklü yazılıma bağlıdır.  

İstemci bu bağımlılıkları yüklemeyi tamamlaması gerekiyorsa, otomatik olarak yüklenir.

|Bileşen|Description|
|---|---|
|Microsoft Core XML Services (MSXML) sürüm 6.20.5002 veya üzeri ( `msxml6.msi` )|Windows'ta XML belgelerinin işlenmesini desteklemek için gereklidir.|
|Microsoft Visual C++ 2013 yeniden dağıtılabilir sürüm 12.0.40660.0 ( `vcredist_x*.exe` )|İstemci işlemlerini desteklemek için gereklidir. Bu güncelleştirmeyi istemci bilgisayarlara yüklediğinizde, yüklemenin tamamlanabilmesi için yeniden başlatma gerekebilir.|<!-- SCCMDocs#1526 -->
|Windows görüntüleme API 'Leri 'ları 6.0.6001.18000 veya üzeri ( `wimgapi.msi` )|Configuration Manager Windows görüntü (. wim) dosyalarını yönetmesine izin vermek için gereklidir.|
|Microsoft Policy Platform 1.2.3514.0 veya üzeri ( `MicrosoftPolicyPlatformSetup.msi` )|İstemcilerin uygunluk ayarlarını değerlendirmelerini sağlamak için gereklidir.|  
|Microsoft .NET Framework sürüm 4.5.2 veya üzeri ( `NDP452-KB2901907-x86-x64-AllOS-ENU.exe` )|İstemci işlemlerini desteklemek için gereklidir. Microsoft .NET Framework sürüm 4,5 veya sonraki bir sürümü yüklü değilse, istemci bilgisayara otomatik olarak yüklenir. Daha fazla bilgi için bkz. [Microsoft .NET Framework sürüm 4.5.2 hakkında ek ayrıntılar](#dotNet).|  
|Microsoft SQL Server Compact 4,0 SP1 bileşenleri|İstemci işlemleriyle ilgili bilgileri saklamak için gereklidir.|  

> [!Important]
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makaleleri inceleyin:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> Hala Uygulama Kataloğu web sitesi kullanıcı deneyimini kullanıyorsanız, istemci Microsoft Silverlight 5.1.41212.0 gerektirir. İstemci Silverlight 'ı otomatik olarak yüklemez. Uygulama kataloğunun birincil işlevselliği artık yazılım merkezi 'ne eklenmiştir.<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a>Microsoft .NET Framework sürüm 4.5.2 hakkında ek ayrıntılar  

> [!NOTE]  
> .NET 4,0, 4,5 ve 4.5.1 artık desteklenmemektedir. Daha fazla bilgi için bkz. [Microsoft .NET Framework destek yaşam döngüsü ILKESI SSS](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Microsoft .NET Framework sürüm 4.5.2, yüklemenin tamamlanabilmesi için yeniden başlatma gerektirebilir. Kullanıcı, sistem tepsisinde **yeniden başlatma gerekli** bildirimini görür. Aşağıdaki yaygın senaryolar istemci bilgisayarların yeniden başlatılmasını gerektirir:  

- Bilgisayarda çalışan .NET uygulamaları ya da hizmetleri.  

- .NET yüklemesi için gereken bir veya daha fazla yazılım güncelleştirmesi eksik.  

- Bilgisayarda daha önce yüklenen .NET Framework yazılım güncelleştirmelerinden dolayı yeniden başlatma bekleniyor.  

.NET Framework 4.5.2 yüklendikten sonra ek güncelleştirmeler gerekebilir. Bu sonraki güncelleştirmeler, ek bilgisayar yeniden başlatmaları gerektirebilir.  

### <a name="configuration-manager-dependencies"></a>Configuration Manager bağımlılıkları  

Daha fazla bilgi için bkz. [istemciler için site sistemi rollerini belirleme](plan/determine-the-site-system-roles-for-clients.md).  

|Bileşen|Description|  
|---|---|  
|Yönetim noktası|Configuration Manager istemcisini dağıtmak için bir yönetim noktası gerekmez. İstemciler, site ile bilgi aktarmak için bir yönetim noktası gerektirir. Bir yönetim noktası olmadan istemci bilgisayarları yönetemezsiniz.|  
|Dağıtım noktası|Dağıtım noktası isteğe bağlıdır, ancak istemci dağıtımı ve yönetimi için önerilen site sistem rolüdür. Tüm dağıtım noktaları, istemci kaynak dosyalarını barındırır. İstemciler, istemci dağıtımı veya güncelleştirmesi sırasında kaynak dosyaların indirileceği en yakın dağıtım noktasını bulur. Sitenin bir dağıtım noktası yoksa, bilgisayarlar istemci kaynak dosyalarını yönetim noktasından indirir.|  
|Geri dönüş durumu noktası|Geri dönüş durum noktası isteğe bağlıdır, ancak istemci dağıtımı için önerilen site sistem rolüdür. Geri dönüş durum noktası istemci dağıtımını izler ve Configuration Manager sitesindeki bilgisayarların bir yönetim noktasıyla iletişim kuramadıklarında durum iletileri göndermesini sağlar.|  
|Raporlama hizmetleri noktası|Raporlama Hizmetleri noktası isteğe bağlıdır, ancak önerilen site sistem rolüdür. İstemci dağıtımı ve yönetimiyle ilgili raporları görüntüler. Daha fazla bilgi için bkz. [raporlamaya giriş](../../servers/manage/introduction-to-reporting.md).|  

### <a name="installation-method-dependencies"></a>Yükleme yöntemi bağımlılıkları  

Aşağıdaki önkoşullar, çeşitli istemci yükleme yöntemlerine özgüdür.  

#### <a name="client-push-installation"></a>Client push yüklemesi  

- Site, istemciyi yüklemek için bilgisayarlara bağlanmak üzere istemci anında yükleme hesapları kullanır. Istemci gönderme yüklemesi özelliklerinin **hesaplar** sekmesinde bu hesapları belirtin. Hesap, hedef bilgisayarda yerel Yöneticiler grubunun bir üyesi olmalıdır.  

    İstemci anında yükleme hesabı belirtmezseniz, site sunucusu bilgisayar hesabını kullanır.  

- Sitenin, istemcisini yüklemekte olduğunuz bilgisayarı bulması gerekir. En az bir Configuration Manager bulma yöntemi gerekir.  

- Bilgisayarda ADMIN$ paylaşımı vardır.  

- Configuration Manager istemcisini, bulunan kaynaklara otomatik olarak göndermek için, istemci anında yükleme özellikleri ' nde **istemci gönderme yüklemesini atanmış kaynaklara etkinleştirme** seçeneğini belirleyin.  

- Kaynak dosyaları indirmek için istemci bilgisayarın bir dağıtım noktası veya bir yönetim noktasıyla iletişim kurması gerekir.  

- Kerberos karşılıklı kimlik doğrulaması gerektiğinde, istemcilerin güvenilir bir Active Directory ormanında olması gerekir. Windows 'da Kerberos, karşılıklı kimlik doğrulaması için Active Directory bağımlıdır.<!--1358204-->  

Client Push kullanmak için aşağıdaki güvenlik izinlerine sahip olmanız gerekir:  

- İstemci anında yükleme hesabını yapılandırmak için: **site** nesnesi için **değiştirme** ve **okuma** izni.  

- İstemcisini koleksiyonlara, cihazlara ve sorgulara yüklemek üzere Client Push kullanmak için: **koleksiyon** nesnesi Için **kaynak değiştirme** ve **okuma** izni.  

**Altyapı Yöneticisi** varsayılan güvenlik rolü, istemci gönderme yüklemelerini yönetmek için gerekli izinleri içerir.  

#### <a name="software-update-point-based-installation"></a>Yazılım güncelleştirme noktası tabanlı yükleme  

- Active Directory şemasını genişletmemiş veya başka bir ormandan istemci yüklüyorsanız, CCMSetup. exe için yükleme parametreleri sağlamak üzere Grup İlkesi 'ni kullanın. Daha fazla bilgi için bkz. [istemci yükleme özelliklerini sağlama](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Configuration Manager istemcisini yazılım güncelleştirme noktasına yayımlayın.  

- Kaynak dosyaları indirmek için istemci bilgisayarın bir dağıtım noktası veya bir yönetim noktasıyla iletişim kurması gerekir.  

Configuration Manager yazılım güncelleştirmelerini yönetmek için gereken güvenlik izinleri için bkz. [yazılım güncelleştirmeleri Için Önkoşullar](../../../sum/plan-design/prerequisites-for-software-updates.md).  

#### <a name="group-policy-based-installation"></a>Grup İlkesi tabanlı yükleme  

- Active Directory şemasını genişletmemiş veya başka bir ormandan istemci yüklüyorsanız, CCMSetup. exe için yükleme parametreleri sağlamak üzere Grup İlkesi 'ni kullanın. Daha fazla bilgi için bkz. [istemci yükleme özelliklerini sağlama](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Kaynak dosyaları indirmek için istemci bilgisayarın bir dağıtım noktası veya bir yönetim noktasıyla iletişim kurması gerekir.  

#### <a name="logon-script-based-installation"></a>Oturum açma betiği tabanlı yükleme  

Kaynak dosyaları indirmek için istemci bilgisayarın bir dağıtım noktası veya bir yönetim noktasıyla iletişim kurması gerekir. CCMSetup. exe ' yi aşağıdaki komut satırı parametresiyle belirtmediğiniz durumlar için:`ccmsetup /source`  

#### <a name="manual-installation"></a>El ile yükleme  

Kaynak dosyaları indirmek için istemci bilgisayarın bir dağıtım noktası veya bir yönetim noktasıyla iletişim kurması gerekir. CCMSetup. exe ' yi aşağıdaki komut satırı parametresiyle belirtmediğiniz durumlar için:`ccmsetup /source`  

#### <a name="microsoft-intune-mdm-installation"></a>MDM yüklemesini Microsoft Intune

- Microsoft Intune Abonelik ve uygun lisanslar gerektirir.  

- İnternet tabanlı olmasa bile cihazın İnternet erişimine sahip olmasını gerektirir.  

- Kullanım örneğine bağlı olarak, aşağıdaki teknolojilerden birini veya her ikisini de isteyebilirsiniz:  

    - Azure Active Directory  

    - Bulut yönetimi ağ geçidi  

#### <a name="workgroup-computer-installation"></a>Çalışma grubu bilgisayar yükleme  

Configuration Manager site sunucusunun etki alanındaki kaynaklara erişmek için, site için bir ağ erişim hesabı yapılandırın.  

Ağ erişim hesabının nasıl yapılandırılacağı hakkında daha fazla bilgi için bkz. [içerik yönetimi Için temel kavramlar](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Yazılım dağıtım tabanlı yükleme (salt yükseltmeler için)  

- Active Directory şemasını genişletmemiş veya başka bir ormandan istemci yüklüyorsanız, CCMSetup. exe için yükleme parametreleri sağlamak üzere Grup İlkesi 'ni kullanın. Daha fazla bilgi için bkz. [istemci yükleme özelliklerini sağlama](deploy-clients-to-windows-computers.md#BKMK_Provision).

- Kaynak dosyaları indirmek için istemci bilgisayarın bir dağıtım noktası veya bir yönetim noktasıyla iletişim kurması gerekir.  

Uygulama yönetimi 'ni kullanarak Configuration Manager istemcisini yükseltmek için gereken güvenlik izinleri için, bkz. [uygulama yönetimi Için güvenlik ve gizlilik](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

#### <a name="automatic-client-upgrades"></a>Otomatik istemci yükseltmeleri  

Otomatik istemci yükseltmelerini yapılandırabilmek için **Tam Yönetici** güvenlik rolünün bir üyesi olmanız gerekir.  

### <a name="firewall-requirements"></a>Güvenlik duvarı gereksinimleri  

Site sistemi sunucuları ile Configuration Manager istemcisini yüklemek istediğiniz bilgisayarlar arasında bir güvenlik duvarı varsa, bkz. [istemciler Için Windows Güvenlik Duvarı ve bağlantı noktası ayarları](windows-firewall-and-port-settings-for-clients.md).  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a>Mobil aygıt istemcileri için Önkoşullar  

Mobil cihazlara Configuration Manager istemcisini yükleyip kaydettiğinizde, önkoşulları öğrenmek için bu bilgileri kullanın.  

### <a name="dependencies-external-to-configuration-manager"></a>Bağımlılıklar dış Configuration Manager

- Mobil aygıtlarda gereken sertifikaları dağıtmak ve yönetmek için sertifika şablonlarına sahip bir Microsoft kuruluş sertifika verme yetkilisi (CA).  

    Sertifika verme yetkilisi, kayıt işlemi sırasında mobil aygıtlardan gelen sertifika isteklerini otomatik olarak onaylamalıdır.  

    Sertifika gereksinimleri hakkında daha fazla bilgi için bkz. [sertifika profilleri Için güvenlik ve gizlilik](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

- Mobil aygıtlarına kaydedebilecekleri kullanıcıları içeren bir güvenlik grubu.  

    Bu güvenlik grubu, mobil aygıt kaydı sırasında kullanılan sertifika şablonunu yapılandırmakta kullanılır.  

- İsteğe bağlı ancak önerilen: **ConfigMgrEnroll**ADLı bir DNS diğer adı (CNAME kaydı). Bu diğer adı, kayıt proxy noktası sunucu adı için yapılandırın.  

    Bu DNS diğer adı, kayıt hizmeti için otomatik bulmayı desteklemek için gereklidir. Bu DNS kaydını yapılandırmazsanız kullanıcıların, kayıt işleminin bir parçası olarak kayıt proxy noktasının adını el ile belirtmesi gerekir.  

- Kayıt noktasını ve kayıt proxy noktası site sistem rollerini çalıştıran bilgisayarlar için site sistemi rolü bağımlılıkları.  

    Daha fazla bilgi için bkz. [site sistemi sunucuları Için desteklenen işletim sistemleri](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Configuration Manager bağımlılıkları

Daha fazla bilgi için bkz. [istemciler için site sistemi rollerini belirleme](plan/determine-the-site-system-roles-for-clients.md).  

- HTTPS istemci bağlantıları için yapılandırılan ve mobil cihazlar için etkinleştirilen yönetim noktası  

    Mobil cihazlara Configuration Manager istemcisini yüklemek için her zaman bir yönetim noktası gereklidir. Yönetim noktasının HTTPS Yapılandırma gereksinimlerine ek olarak, bir İnternet FQDN 'SI ile yapılandırılması ve internet 'ten gelen istemci bağlantılarını kabul etmesi gerekir.  

- Kayıt noktası ve kayıt proxy noktası  

    Bir kayıt proxy noktası, mobil aygıtlardan gelen kayıt isteklerini yönetir, kayıt noktası ise kayıt işlemini tamamlar. Kayıt noktası site sunucusuyla aynı Active Directory ormanında olmalıdır ancak kayıt proxy noktası başka bir ormanda bulunabilir.  

- Mobil aygıt kaydı için istemci ayarları  

    Mobil aygıtları kaydetmek ve en az bir kayıt profilini yapılandırmak için kullanıcılara izin vermek amacıyla istemci ayarlarını yapılandırın.  

- Raporlama hizmetleri noktası  

    Raporlama hizmetleri noktası isteğe bağlıdır ancak mobil aygıt kaydı ve istemci yönetimiyle ilgili raporları görüntüleyebilen, önerilen site sistem rolüdür.  

    Daha fazla bilgi için bkz. [raporlamaya giriş](../../servers/manage/introduction-to-reporting.md).  

- Mobil aygıtlara yönelik kaydı yapılandırmak için, aşağıdaki güvenlik izinlerine sahip olmalısınız:  

    - Kayıt site sistemi rollerini eklemek, değiştirmek ve silmek istiyorsanız: **Site** nesnesi için **Değiştirme** izni.  

    - Kayıt amacıyla istemci ayarlarını yapılandırmak istiyorsanız: Varsayılan istemci ayarları, **Site** nesnesi için **Değiştirme** iznini gerektirirken özel istemci ayarları, **İstemci aracısı** izinlerini gerektirir.  

    **Tam yönetici** varsayılan güvenlik rolü, kayıt site sistem rollerini yapılandırmak için gereken izinleri içerir.  

- Kayıtlı mobil aygıtları yönetmek için, aşağıdaki güvenlik izinlerine sahip olmalısınız:  

    - Mobil cihazı silmek veya devre dışı bırakmak istiyorsanız: **Koleksiyon** nesnesi için **Kaynağı silme**.  

    - Bir silme veya devre dışı bırakma komutunu iptal etmek istiyorsanız: **Koleksiyon** nesnesi için **Kaynağı silme**.  

    - Mobil cihazlara izin vermek ve onları engellemek istiyorsanız: **Koleksiyon** nesnesi için **Kaynağı değiştirme** .  

    - Bir mobil cihazda geçiş kodunu uzaktan kilitlemek veya sıfırlamak istiyorsanız: **Koleksiyon** nesnesi için kaynağı **Değiştirme**.  

    **Operations Administrator** varsayılan güvenlik rolü, mobil cihazları yönetmek için gereken izinleri içerir.  

    Güvenlik izinlerini yapılandırma hakkında daha fazla bilgi için bkz. [rol tabanlı yönetimin temelleri](../../understand/fundamentals-of-role-based-administration.md) ve [rol tabanlı yönetimi yapılandırma](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Güvenlik duvarı gereksinimleri

Yönlendiriciler ve güvenlik duvarları gibi ilgili ağ aygıtları ve varsa Windows Güvenlik Duvarı, mobil aygıt kaydıyla ilişkili trafiğe izin vermelidir:  

- Mobil cihazlar ile kaydolma proxy noktası arasında: HTTPS (varsayılan olarak, TCP 443)  

- Kaydolma proxy noktası ile kaydolma noktası arasında: HTTPS (varsayılan olarak, TCP 443)  

Proxy Web sunucusu kullanıyorsanız, SSL tünellemesi için yapılandırılması gerekir. Mobil aygıtlar için SSL köprüleme desteklenmez.  
