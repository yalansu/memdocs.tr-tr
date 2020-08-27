---
title: Microsoft Intune - Azure’da Windows 10 cihaz kısıtlama ayarları | Microsoft Docs
description: Windows 10 ve üzeri cihazlarda cihaz kısıtlamaları oluşturmaya yönelik tüm ayarların ve bunların açıklamalarının listesini görüntüleyin. Bu ayarları, ekran görüntülerini, parola gereksinimlerini, bilgi noktası ayarlarını, depodaki uygulamaları, Microsoft Edge tarayıcısı, Microsoft Defender, buluta erişimi, Başlangıç menüsünü ve Microsoft Intune daha fazlasını denetlemek için bir yapılandırma profilinde kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38465f709cf07da97e26c36a9fabba232aca9ba2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912891"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune kullanarak özelliklere izin vermek veya erişimi kısıtlamak için Windows 10 (ve üzeri) cihaz ayarları

Bu makalede, Windows 10 ve daha yeni cihazlarda denetleyebilmeniz için kullanabileceğiniz tüm farklı ayarlar listelenmiştir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu ayarları, özelliklere izin vermek veya devre dışı bırakmak, parola kuralları ayarlamak, kilit ekranını özelleştirmek, Microsoft Defender 'ı kullanmak ve daha fazlasını yapmak için kullanın.

Bu ayarlar, Intune 'da bir cihaz yapılandırma profiline eklenir ve ardından Windows 10 cihazlarınıza atanır veya dağıtılır.

> [!Note]
> Tüm Windows sürümlerinde tüm seçenekler kullanılamaz. Desteklenen sürümleri görmek için, [CSP](/windows/client-management/mdm/policy-configuration-service-provider) 'lere başvurun (başka bir Microsoft Web sitesi açar).
>  
> Bir Windows 10 cihaz kısıtlama profilinde, yapılandırılabilir ayarların çoğu cihaz grupları kullanılarak cihaz düzeyinde dağıtılır. Kullanıcı gruplarına dağıtılan ilkeler hedeflenen kullanıcılara uygulanır ve Intune lisansına sahip kullanıcılar için geçerlidir ve bu cihazda oturum açın.

## <a name="before-you-begin"></a>Başlamadan önce

[Windows 10 cihaz kısıtlama profili oluşturun](device-restrictions-configure.md#create-the-profile).

## <a name="app-store"></a>App Store

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [ApplicationManagement ILKESI CSP](/windows/client-management/mdm/policy-csp-applicationmanagement)'sini kullanır.

- **App Store (yalnızca mobil)**: **Block** , kullanıcıların mobil cihazlarda App Store 'a erişmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların uygulama mağazası 'na erişmesine izin verebilir.
- **Store 'dan uygulamaları otomatik güncelleştir**: **blok** , güncelleştirmelerin Microsoft Store otomatik olarak yüklenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Microsoft Store yüklenen uygulamaların otomatik olarak güncelleştirilmesini sağlayabilir.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Güvenilen uygulama yüklemesi**: Microsoft Store olmayan uygulamalar yüklenebiliyorsa, dışarıdan yükleme olarak da bilinen ' yi seçin. Dışarıdan yükleme, Microsoft Store tarafından sertifikasız bir uygulamayı yüklüyor ve çalıştırmıyor. Örneğin, yalnızca şirket içi bir uygulama. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Engelle**: dışarıdan yüklemeyi engeller. Microsoft Store olmayan uygulamalar yüklenemez.
  - **Izin ver**: dışarıdan yüklemeyi sağlar. Microsoft Store olmayan uygulamalar yüklenebilir.

- **Geliştirici kilidi açma**: dışarıdan yüklenen uygulamaların kullanıcılar tarafından değiştirilmesine izin verme gibi Windows Geliştirici ayarlarına izin verin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Engelle**: Geliştirici modunu ve dışarıdan yükleme uygulamalarını engeller.
  - **Izin ver**: geliştirici modu ve dışarıdan yükleme uygulamalarına izin verir.

  [Cihazınızı geliştirme Için etkinleştirme](/windows/uwp/get-started/enable-your-device-for-development) bu özellik hakkında daha fazla bilgi içerir.
  
  [ApplicationManagement/AllowAllTrustedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Paylaşılan kullanıcı uygulaması verileri**: aynı cihazdaki farklı kullanıcılar arasında ve bu uygulamanın diğer örnekleriyle uygulama verilerini paylaşmaya **izin ver** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, diğer kullanıcılar ve aynı uygulamanın diğer örnekleri ile veri paylaşmayı önleyebilir.

  [ApplicationManagement/AllowSharedUserAppData CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Yalnızca özel mağazayı kullan**: **izin ver** , bir perakende kataloğu dahil olmak üzere yalnızca uygulamaların özel bir mağazadan indirilmesine ve ortak depodan İndirilme yapmasına izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi uygulamaların özel bir mağazadan ve genel bir mağazadan indirilmesine izin verebilir.

  [ApplicationManagement/RequirePrivateStoreOnly CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Mağaza kaynaklı uygulama başlatma**: **blok** cihazda önceden yüklenmiş olan veya Microsoft Store indirilen tüm uygulamaları devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu uygulamaların açılmasını sağlayabilir.

  [ApplicationManagement/DisableStoreOriginatedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **Uygulama verilerini sistem birimine yükler**: **blok** , uygulamaların cihaz sistem biriminde veri depolamasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, IŞLETIM sistemi uygulamaların sistem diski biriminde veri depolamasına izin verebilir.

  [ApplicationManagement/Kısıttappdatatosystemvolume CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Uygulamaları sistem sürücüsüne yükleme**: **blok** , uygulamaların cihazdaki sistem sürücüsüne yüklenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, IŞLETIM sistemi uygulamaların sistem sürücüsüne yüklenmesine izin verebilir.

  [ApplicationManagement/Kısıttapptosystemvolume CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **Game DVR (yalnızca masaüstü)**: **blok** , Windows oyun kaydı ve yayını devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi oyunları kaydetmeye ve yayınlamasını sağlayabilir.

  [ApplicationManagement/AllowGameDVR CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Yalnızca mağazadan uygulamalar**: Bu ayar, kullanıcılar Microsoft Store dışındaki yerlerden uygulama yüklerken Kullanıcı deneyimini belirler. Bu, USB aygıtlarından, ağ paylaşımlarından veya internet dışı diğer kaynaklardan içerik yüklenmesini engellemez. Bu korumaların beklenen şekilde çalıştığından emin olmak için güvenilir bir tarayıcı kullanın.

  Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların diğer ilke ayarlarında tanımlı uygulamalar dahil olmak üzere Microsoft Store dışındaki yerlerden uygulama yüklemelerine izin verebilir.  
  - **Her yerde**: uygulama önerilerini devre dışı bırakır ve kullanıcıların herhangi bir konumdan uygulama yüklemesine izin verir.  
  - **Yalnızca depola**: amaç, kötü amaçlı içeriğin internet 'ten yürütülebilir içerik indirirken Kullanıcı cihazlarınızı etkilemesini önlemektir. Kullanıcılar Internet 'ten uygulama yüklemeye çalıştıklarında, yükleme engellenir. Kullanıcılar Microsoft Store uygulamaları indirdikleri öneren bir ileti görür.
  - **Öneriler**: Microsoft Store bulunan Web 'den bir uygulama yüklerken, kullanıcılar onu mağazadan indirdikleri öneren bir ileti görür.  
  - **Depoyu tercih et**: Microsoft Store dışındaki yerlerden uygulama yüklediklerinde kullanıcıları uyarır.

  [SmartScreen/Enableappınstallcontrol CSP](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **Yüklemeler üzerinde Kullanıcı denetimi**: **blok** kullanıcıların, dosyaları yüklemek için Dizin girme gibi sistem yöneticileri için genellikle ayrılmış yükleme seçeneklerini değiştirmelerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Windows Installer, varsayılan olarak kullanıcıların bu yükleme seçeneklerini değiştirmelerini engelleyebilir ve Windows Installer güvenlik özelliklerinden bazıları atlanır.

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Yükseltilmiş ayrıcalıklarla uygulamalar yükleme**: **blok** , sistem üzerinde herhangi bir program yüklerken yükseltilmiş izinleri kullanmak Windows Installer. Bu ayrıcalıklar tüm programlara genişletilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, sistem, bir sistem yöneticisinin dağıtamayacağı veya sunamayacağı programları yüklediğinde geçerli kullanıcının izinlerini uygulayabilir.

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Başlangıç uygulamaları**: Kullanıcı cihazda oturum açtıktan sonra açılacak uygulamaların listesini girin. Windows uygulamalarının paket aile adları (PFN) için noktalı virgülle ayrılmış bir liste kullandığınızdan emin olun. Bu ilkenin çalışması için, Windows uygulamalarındaki bildirimin bir başlangıç görevi kullanması gerekir.

  [ApplicationManagement/LaunchAppAfterLogOn CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>Hücresel ve Bağlantı

Bu ayarlar, desteklenen Windows sürümlerini de listelenecek olan [bağlantı ilkesini](/windows/client-management/mdm/policy-csp-connectivity) ve [Wi-Fi ilkesi](/windows/client-management/mdm/policy-csp-wifi) CSP 'leri kullanır.

- **Hücresel veri kanalı**: kullanıcıların bir hücresel ağa bağlıyken Web 'e göz atma gibi verileri kullanıp kullanmadığı seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. kullanıcılar devre dışı bırakabilirsiniz.
  - **Engelle**: hücresel veri kanalına izin verme. Kullanıcılar açamaz.
  - **Izin ver (düzenlenemez)**: hücresel veri kanalına izin verir. Kullanıcılar bu uygulamayı kapatamaz.

- **Veri dolaşımı**: **blok** , cihazda hücresel veri dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, verilere erişirken ağlar arasında dolaşıma izin verilebilir.
- **Hücresel ağ üzerinden VPN**: **blok** cihazın BIR hücresel ağa bağlıyken VPN bağlantılarına erişmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, hücresel dahil olmak üzere VPN 'nin herhangi bir bağlantıyı kullanmasına izin verebilir.
- **Hücresel ağ üzerinden VPN dolaşımı**: **blok** cihazın bir hücresel ağda dolaşımda VPN bağlantılarına erişmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi dolaşım sırasında VPN bağlantılarına izin verebilir.
- **Bağlı cihazlar hizmeti**: **blok** bağlı cihazlar platformu (CDP) bileşenini devre dışı bırakır. CDP, uzak uygulama başlatma, uzak mesajlaşma, uzak uygulama oturumları ve diğer cihazlar arası deneyimleri desteklemek için diğer cihazlara (Bluetooth/LAN veya bulut aracılığıyla) bulma ve bağlantı sağlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bağlı cihazlar hizmetine izin verebilir, bu da diğer Bluetooth cihazlarına keşif ve bağlantı sağlar.
- **NFC**: **Block** , yakın alan iletişimleri (NFC) yeteneklerini engelliyor. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazda NFC özelliklerini etkinleştirmesine ve yapılandırmasına izin verebilir.
- **Wi-Fi**: **Block** , kullanıcıların cihazdaki Wi-Fi bağlantılarını kullanmasını ve etkinleştirmelerini, yapılandırmalarını ve kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Wi-Fi bağlantılarına izin verebilir.
- **Wi-Fi etkin noktalarına otomatik olarak bağlan**: **blok** cihazların Wi-Fi etkin noktalarına otomatik olarak bağlanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazların ücretsiz Wi-Fi etkin noktalarına otomatik olarak bağlanmasına izin verebilir ve bağlantı için tüm hüküm ve koşulları otomatik olarak kabul edebilir.
- **El Ile Wi-Fi yapılandırması**: **blok** cihazların, MDM sunucusu yüklü ağlarının dışında Wi-Fi ' a bağlanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların kendi Wi-Fi bağlantısı ağ SSID 'lerini eklemesine ve yapılandırmasına izin verebilir.
- **Wi-Fi tarama aralığı**: cihazların ne sıklıkta Wi-Fi ağlarını tarayacağını girin. 1 (en sık) ile 500 (en az sık) arasında bir değer girin. Varsayılan değer `0` (sıfır).

### <a name="bluetooth"></a>Bluetooth

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [Bluetooth ILKESI CSP](/windows/client-management/mdm/policy-csp-bluetooth)'sini kullanır.

- **Bluetooth**: **blok** kullanıcıların Bluetooth 'u etkinleştirmelerini engeller. **Yapılandırılmamış** (varsayılan) cihazda Bluetooth 'a izin verir.
- **Bluetooth bulunabilirliği**: **blok** cihazın diğer Bluetooth özellikli cihazlar tarafından keşfedilmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kulaklık gibi diğer Bluetooth özellikli cihazların cihazı bulmasına izin verebilir.

  [Bluetooth/AllowDiscoverableMode CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Bluetooth önceden eşleme**: **blok** , belirli Bluetooth cihazlarının bir konak cihazla otomatik olarak eşleşmesini önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi konak cihazla otomatik eşleştirmeye izin verebilir.

  [Bluetooth/Allowpreeşleştirmeye yönelik CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **Bluetooth reklamcılık**: **blok** cihazın Bluetooth tanıtımları göndermesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazın Bluetooth tanıtımları göndermesini sağlayabilir.

  [Bluetooth/AllowAdvertising CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **Bluetooth proxde bağlantılar**: **blok** bir cihaz kullanıcısının Swift çiftini ve diğer yakınlık tabanlı senaryoları kullanmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazın Bluetooth tanıtımları göndermesini sağlayabilir.

  [Bluetooth/AllowPromptedProximalConnections CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Bluetooth izin verilen hizmetler**: Izin verilen Bluetooth hizmetleri ve profillerinin bir listesini gibi onaltılık dizeler olarak **ekleyin** `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}` .

  [Servicesallowedlist kullanım kılavuzu](/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) , hizmet listesi hakkında daha fazla bilgi içerir.

  [Bluetooth/ServicesAllowedList CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## <a name="cloud-and-storage"></a>Bulut ve Depolama

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [hesaplar ILKESI CSP](/windows/client-management/mdm/policy-csp-accounts)'sini kullanır.

> [!IMPORTANT]
> Bu Microsoft hesabı ayarlarını engellemek veya devre dışı bırakmak, kullanıcıların Azure AD 'de oturum açmasını gerektiren kayıt senaryolarını etkileyebilir. Örneğin, [Autopilot beyaz eldiven](/windows/deployment/windows-autopilot/white-glove)kullanıyorsunuz. Genellikle, kullanıcılara bir Azure AD oturum açma penceresi gösterilir. Bu ayarlar **Engelle** veya **devre dışı bırak**olarak ayarlandığında Azure AD oturum açma seçeneği görüntülenmeyebilir. Bunun yerine, kullanıcıların EULA 'yı kabul etmesi ve yerel bir hesap oluşturması istenir ve bu da istediğiniz şey olmayabilir.

- **Microsoft hesabı**: **Block** , kullanıcıların bir Microsoft hesabı cihazla ilişkilendirilmesini engeller. **Blok** Ayrıca, kayıt işlemini tamamlaması için kullanıcılara güvenen bazı kayıt senaryolarını etkileyebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Microsoft hesabı eklemeye ve kullanmaya izin verebilir.
- **Microsoft hesabı dışı**: **blok** , kullanıcıların kullanıcı arabirimini kullanarak Microsoft olmayan hesaplar eklemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir Microsoft hesabı ile ilişkilendirilmemiş e-posta hesapları eklemesine izin verebilir.
- **Microsoft hesabı Için ayarların eşitlenmesi**: **blok** , bir Microsoft hesabı ilişkili cihaz ve uygulama ayarlarının cihazlar arasında eşitlenmesine engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu eşitlemeye izin verebilir.
- **Microsoft hesabı oturum açma Yardımcısı**: Bu işletim sistemi hizmeti, kullanıcıların Microsoft hesabı oturum açmasına olanak tanır. Varsayılan olarak, işletim sistemi kullanıcıların **Microsoft hesabı oturum açma Yardımcısı** (wlidsvc) hizmetini başlatıp durdurmasına izin verebilir.
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların **Microsoft hesabı oturum açma Yardımcısı** (wlidsvc) hizmetini başlatıp durdurmasına izin verebilir.
  - **Devre dışı**: Microsoft oturum açma Yardımcısı hizmetini (wlidsvc) devre dışı olarak ayarlar ve kullanıcıların bunu el ile başlatmasını önler.

      **Devre dışı bırak ayarı** , kullanıcıların kaydı tamamlaması için kullandığı bazı kayıt senaryolarına de etkisi olabilir. Örneğin, [Autopilot beyaz eldiven](/windows/deployment/windows-autopilot/white-glove)kullanıyorsunuz. Genellikle, kullanıcılara bir Azure AD oturum açma penceresi gösterilir. **Devre dışı**olarak AYARLANDıĞıNDA Azure AD oturum açma seçeneği görüntülenmeyebilir. Bunun yerine, kullanıcıların EULA 'yı kabul etmesi ve yerel bir hesap oluşturması istenir ve bu da istediğiniz şey olmayabilir.

## <a name="cloud-printer"></a>Bulut Yazıcı

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [Enterprisecloudprint ILKESI CSP](/windows/client-management/mdm/policy-csp-enterprisecloudprint)'sini kullanır.

- **Yazıcı bulma URL 'si**: bulut yazıcılarını bulmak için URL 'yi girin. Örneğin, `https://cloudprinterdiscovery.contoso.com` girin.
- **Yazıcı erişim yetkilisi URL 'si**: OAuth belirteçlerini almak için kimlik doğrulama uç noktası URL 'sini girin. Örneğin, `https://azuretenant.contoso.com/adfs` girin.
- **Azure yerel istemci uygulama GUID 'si**: OAuthAuthority 'den OAuth belirteçleri almaya izin verilen bir ISTEMCI uygulamasının GUID 'sini girin. Örneğin, `E1CF1107-FF90-4228-93BF-26052DD2C714` girin.
- **Yazdırma hizmeti kaynak URI 'si**: Azure Portal yapılandırılmış yazdırma hizmeti için OAUTH Kaynak URI 'sini girin. Örneğin, `http://MicrosoftEnterpriseCloudPrint/CloudPrint` girin.
- **Sorgulanacak en fazla yazıcı**: sorgulanmasını istediğiniz en fazla yazıcı sayısını girin. Varsayılan değer: `20`.
- **Yazıcı bulma hizmeti kaynak URI 'si**: Azure Portal için yapılandırılmış yazıcı bulma hizmeti OAUTH Kaynak URI 'sini girin. Örneğin, `http://MopriaDiscoveryService/CloudPrint` girin.

> [!TIP]
> Bir [Windows Server hibrit bulutu](/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview)oluşturduktan sonra, bu ayarları yapılandırabilir ve ardından Windows cihazlarınıza dağıtabilirsiniz.

## <a name="control-panel-and-settings"></a>Denetim Masası ve Ayarlar

- **Settings App**: **Block** , kullanıcıların Windows ayarları uygulamasına erişmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazda Ayarlar uygulamasını açmasına izin verebilir.
  - **System**: **Block** , ayarlar uygulamasının sistem alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Güç ve uyku ayarlarının değiştirilmesi** (yalnızca masaüstü): **Block** , kullanıcıların cihazdaki güç ve uyku ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan), kullanıcıların güç ve uyku ayarlarını değiştirmesine izin verir.
  - **Cihazlar**: **blok** cihazdaki ayarlar uygulamasının cihazlar alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Ağ Internet**: **Block** , cihazdaki ayarlar uygulamasının ağ & Internet alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Kişiselleştirme**: **blok** cihazdaki ayarlar uygulamasının kişiselleştirme alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Uygulamalar**: **blok** cihazdaki ayarlar uygulamasının uygulamalar alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Hesaplar**: **blok** cihazdaki ayarlar uygulamasının hesaplar alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Zaman ve dil**: **blok** cihazdaki ayarlar uygulamasının zaman & dil alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Sistem saati değişikliği**: **Block** , kullanıcıların cihazdaki tarih ve saat ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Kullanıcılar bu ayarları değiştirebilir.
    - **Bölge ayarlarının değiştirilmesi** (yalnızca masaüstü): **Block** , kullanıcıların cihazdaki bölge ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Kullanıcılar bu ayarları değiştirebilir.
    - **Dil ayarlarının değiştirilmesi (yalnızca masaüstü)**: **Block** , kullanıcıların cihazdaki dil ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Kullanıcılar bu ayarları değiştirebilir.

      [Ayarlar ilkesi CSP 'si](/windows/client-management/mdm/policy-csp-settings)

  - **Oyun**: **Block** , cihazdaki ayarlar uygulamasının oyun alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Erişim kolaylığı**: **blok** cihazdaki ayarlar uygulamasının erişim kolaylığı alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Gizlilik**: **blok** cihazdaki ayarlar uygulamasının gizlilik alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Update ve Security**: **Block** , cihazdaki ayarlar uygulamasının Update & Security alanına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="display"></a>Göster

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [görüntüleme ILKESI CSP](/windows/client-management/mdm/policy-csp-display)'sini kullanır.

GDI DPı ölçeklendirme, DPı kullanmayan uygulamaların, monitör DPı 'si ile uyumlu olmasını sağlar.

- **Uygulamalar IÇIN GDI ölçeklendirmeyi aç**: GDI DPI ölçeklendirme özelliğinin açık olmasını istediğiniz eski uygulamaları **ekleyin** . Örneğin `filename.exe` veya `%ProgramFiles%\Path\Filename.exe` girin.

  Listedeki tüm eski uygulamalar için GDI DPı ölçeklendirme açıktır.

- **Uygulamalar IÇIN GDI ölçeklendirmeyi**kapat: GDI DPI ölçeklendirme özelliğinin kapalı olmasını istediğiniz eski uygulamaları **ekleyin** . Örneğin `filename.exe` veya `%ProgramFiles%\Path\Filename.exe` girin.

  Listedeki tüm eski uygulamalar için GDI DPı ölçeklendirme kapalıdır.

Ayrıca, uygulama listesiyle bir. csv dosyasını **Içeri aktarabilirsiniz** .

## <a name="general"></a>Genel

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [deneyim ILKESI CSP](/windows/client-management/mdm/policy-csp-experience)'sini kullanır. 

- **Ekran yakalama** (yalnızca mobil): **blok** kullanıcıların cihazda ekran görüntüleri almasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Kopyala ve Yapıştır (yalnızca mobil)**: **Engelle** , kullanıcıların cihazdaki uygulamalar arasında Kopyala ve Yapıştır kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **El ile kayıt kaldırma**: **blok** , kullanıcıların cihazdaki çalışma alanı denetim masasını kullanarak çalışma alanı hesabını silmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Bu ilke ayarı, bilgisayar Azure AD 'ye katılırsa ve otomatik kayıt etkinse uygulanmaz.

- **El ile kök sertifika yüklemesi** (yalnızca mobil): **blok** kullanıcıların kök sertifikaları ve ara Cap sertifikalarını el ile yüklemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Kamera**: **blok** kullanıcıların cihazda kamera kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz kamerasına erişime izin verebilir.

  Intune yalnızca cihaz kamerasına erişimi yönetir. Resimlere veya videolara erişimi yoktur.

  [Kamera CSP 'si](/windows/client-management/mdm/policy-csp-camera)

- **OneDrive dosya eşitleme**: **Block** , kullanıcıların dosyaları OneDrive 'a cihazdan eşitlemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [System/DisableOneDriveFileSync CSP](/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **Çıkarılabilir depolama**: **Block** , kullanıcıların cihazla SD kartlar gibi harici depolama cihazlarını kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Coğrafi konum**: **blok** kullanıcıların cihazdaki konum hizmetlerini açmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Sistem/AllowLocation CSP](/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **İnternet paylaşımı**: **engelleme** cihazda İnternet bağlantısı paylaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Telefon sıfırlaması**: **engelleme** , kullanıcıların cihazda fabrika sıfırlaması gerçekleştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **USB bağlantısı**: **blok** , cihazdaki bir USB bağlantısı aracılığıyla dış depolama cihazlarına erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. USB ücretlendirme bu ayardan etkilenmez.

  [Bağlantı/AllowUSBConnection CSP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **Hırsızlık önleme modu** (yalnızca mobil): **Block** , kullanıcıların cihazda antihırsızlık modu tercihini seçmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Cortana**: **blok** , cihazda Cortana sesli yardımcısını devre dışı bırakır. Cortana devre dışı bırakıldığında, kullanıcılar hala cihazdaki öğeleri bulmak için arama yapabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Cortana 'Ya izin verebilir.

  [Deneyim/AllowCortana CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

- **Ses kaydı** (yalnızca mobil): **Block** , kullanıcıların cihazda Ses Kaydedicisi 'ni kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, uygulamalar için ses kaydına izin verebilir.
- **Cihaz adı değişikliği** (yalnızca mobil): **Block** , kullanıcıların cihazın adını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Sağlama paketleri ekleme**: **blok** , cihaza sağlama paketlerini yükleyen çalışma zamanı yapılandırma aracısını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Sağlama paketlerini kaldır**: **blok** , kaynak sağlama paketlerini cihazdan kaldıran çalışma zamanı yapılandırma aracısını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Cihaz bulma**: **blok** cihazın diğer cihazlar tarafından bulunmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Deneyim/AllowDeviceDiscovery](/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **Görev değiştirici** (yalnızca mobil): **blok** cihazda görev değiştirmeyi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **SIM kart hatası iletişim kutusu** (yalnızca mobil): bir SIM kart algılanmazsa cihazda hata Iletilerinin gösterilmesini **engelleyin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi hata iletilerini gösterebilir.
- **Mürekkep çalışma alanı**: kullanıcının mürekkep çalışma alanına erişip erişene olduğunu ve nasıl erişebileceğini seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi mürekkep çalışma alanını açabilir ve kullanıcıların bunu kilit ekranı üzerinde kullanmasına izin verilir.
  - **Kilit ekranında devre dışı**: mürekkep çalışma alanı etkindir ve özellik açıktır. Ancak kullanıcılar bu kilit ekranının üzerine erişemez.
  - **Devre dışı**: mürekkep çalışma alanına erişim devre dışı bırakıldı. Özellik kapalı.

  [WindowsInkWorkspace ilkesi CSP 'si](/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Autopilot Reset**: yönetici haklarına sahip olan kullanıcıların, cihaz kilidi ekranında **CTRL + Win + R** kullanarak tüm Kullanıcı verilerini ve ayarlarını silebilmesi için **izin ver** ' i seçin. Cihaz otomatik olarak yeniden yapılandırılır ve yönetime yeniden kaydedilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği önleyebilir.
- Cihazların **Cihaz kurulumu sırasında ağa bağlanmasını gerektir**: Windows kurulumu sırasında ağ sayfasını geçmeden önce cihazın bir ağa bağlanması için **gerektir** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, bir ağa bağlı olmasalar bile, kullanıcıların ağ sayfasını geçmemesine izin verebilir.

  Bu ayar, cihazın bir sonraki temizlenmeden veya sıfırlanışında etkili olur. Diğer Intune yapılandırmaları gibi, yapılandırma ayarlarını almak için cihazın Intune tarafından kaydedilmiş ve yönetilen olması gerekir. Ancak, kaydedildikten ve ilkeleri aldıktan sonra, bir sonraki Windows kurulumu sırasında cihazın sıfırlanması ayarı uygular.

  [TenantLockdown CSP](/windows/client-management/mdm/tenantlockdown-csp)

- **Doğrudan bellek erişimi**: **blok** , Kullanıcı Windows 'a oturum açana kadar tüm etkin takılabilir PCI aşağı akış bağlantı noktaları için doğrudan bellek erişimini (DMA) engeller. **Etkin** (varsayılan) bir Kullanıcı oturum açmamış olsa bile DMA erişimine izin verir.

  [DataProtection/AllowDirectMemoryAccess CSP](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **Görev Yöneticisi 'nden Işlemleri Sonlandır**: Bu ayar, yönetici olmayanların Görev Yöneticisi 'nin görevleri sonlandırıp kullanıp kullanamayacağını belirler. **Blok** , standart kullanıcıların (yönetici olmayanlar), Görev Yöneticisi 'ni kullanarak cihazdaki bir işlem veya görevi sonlandırmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi standart kullanıcıların, Görev Yöneticisi 'Ni kullanarak bir işlem veya görevi sonlandırarak izin verebilir.

  [TaskManager/AllowEndTask CSP](/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## <a name="locked-screen-experience"></a>Kilit ekranı deneyimi

- **İşlem merkezi bildirimleri (yalnızca mobil)**: **blok** , cihaz kilitleme ekranında işlem merkezi bildirimlerinin gösterilmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların hangi uygulamaların kilit ekranında bildirim gösterileceğini seçmesine izin verebilir.

  [AboveLock/AllowActionCenterNotifications CSP](/windows/client-management/mdm/policy-configuration-service-provider#AboveLock_AllowActionCenterNotifications)

- **Kilitli ekran resmi URL 'si (yalnızca masaüstü)**: Windows kilit ekranı duvar kağıdı olarak kullanılan jpg, JPEG veya PNG biçiminde bir resmin URL 'sini girin. Örneğin, `https://contoso.com/image.png` girin. Bu ayar görüntüyü kilitler ve daha sonra değiştirilemez.

  [Kişiselleştirme/Lockscreenımageurl CSP](/windows/client-management/mdm/personalization-csp)

- **Kullanıcı tarafından yapılandırılabilir ekran zaman aşımı (yalnızca mobil)**: **izin ver** kullanıcıların ekran zaman aşımını yapılandırmasına izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu seçeneği kullanıcılara sunmayabilir.

  [DeviceLock/AllowScreenTimeoutWhileLockedUserConfig CSP](/windows/client-management/mdm/policy-configuration-service-provider#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Kilitli ekranda Cortana** (yalnızca masaüstü): **blok** kullanıcıların, cihaz kilit ekranı üzerinde olduğunda Cortana ile etkileşime almasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Cortana ile etkileşime izin verebilir.

  [AboveLock/AllowCortanaAboveLock CSP](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Kilitli ekranda bildirim bildirimleri**: **blok** bildirimlerin cihaz kilitleme ekranında gösterilmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu bildirimlere izin verebilir.

  [AboveLock/Allowtoine CSP](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **Ekran zaman aşımı (yalnızca mobil)**: ekran kilitlemeden ekrana kadar geçen süreyi (saniye cinsinden) ayarlayın. Desteklenen değerler 11-1800 ' dir. Örneğin, `300` Bu zaman aşımını 5 dakikaya ayarlamak için girin.

  [DeviceLock/ScreenTimeoutWhileLocked CSP](/windows/client-management/mdm/policy-configuration-service-provider#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Mesajlaşma

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [mesajlaşma ILKESI CSP](/windows/client-management/mdm/policy-csp-messaging)'sini kullanır.

- **İleti eşitleme (yalnızca mobil)**: **blok** metin iletilerinin yedeklenmesini ve geri yüklenmesini devre dışı bırakır ve Windows cihazları arasında ileti eşitlemeye engel olmaz. Devre dışı bırakma, bilgilerin kuruluşun denetimi dışındaki sunucularda depolanmasını önlemeye yardımcı olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarları değiştirmesine ve iletilerini eşitlemesine izin verebilir.
- **MMS (yalnızca mobil)**: **blok** , cihazda MMS gönderme ve alma işlevini devre dışı bırakır. Kuruluşlar için bu ilkeyi, denetim veya yönetim gereksiniminin parçası olarak cihazlarda MMS 'yi devre dışı bırakmak için kullanın. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi MMS gönderme ve alma izni verebilir.
- **RCS (yalnızca mobil)**: **blok** , cihaza zengin iletişim hizmetleri (RCS) gönderme ve alma işlevini devre dışı bırakır. Kuruluşlar için bu ilkeyi, denetim veya yönetim gereksiniminin parçası olarak cihazlarda RCS 'yi devre dışı bırakmak için kullanın. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi RCS 'nin gönderme ve alma izni verebilir.

## <a name="microsoft-edge-browser"></a>Microsoft Edge Tarayıcısı

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [tarayıcı ILKESI CSP](/windows/client-management/mdm/policy-csp-browser)'sini kullanır.

> [!NOTE]
> Tarayıcı ilkesi CSP, Microsoft Edge sürüm 45 ve önceki sürümleri için geçerlidir. Microsoft Edge Enterprise sürüm 77 ve üzeri için bkz. [Microsoft Edge ilke ayarlarını Microsoft Intune Ile yapılandırma](/DeployEdge/configure-edge-with-intune).

### <a name="use-microsoft-edge-kiosk-mode"></a>Microsoft Edge bilgi noktası modunu kullan

Kullanılabilir ayarlar, seçtiğiniz seçeneğe göre değişir. Seçenekleriniz şunlardır:

- **Hayır** (varsayılan): Microsoft Edge bilgi noktası modunda çalışmıyor. Tüm Microsoft Edge ayarları, değişiklik ve yapılandırma için kullanılabilir.
- **Dijital/Etkileşimli imza (tek uygulama bilgi noktası)**: yalnızca Windows 10 tek uygulama kiosks ' de kullanılmak üzere dijital/Etkileşimli imza için geçerli olan Microsoft Edge ayarlarını filtreler. Bir URL tam ekran açmak için bu ayarı seçin ve yalnızca bu Web sitesindeki içeriği gösterin. [Dijital Işaretleri ayarla](/windows/configuration/setup-digital-signage) özelliği, bu özellik hakkında daha fazla bilgi sağlar.
- **InPrivate genel göz atma (tek uygulama bilgi noktası)**: Windows 10 tek uygulama kiosları 'nda kullanılmak üzere InPrivate genel göz atma modu için geçerli olan Microsoft Edge ayarlarını filtreler. Microsoft Edge 'in çok sekmeli bir sürümünü çalıştırır.
- **Normal mod (çok uygulama bilgi noktası)**: normal Microsoft Edge bilgi noktası modu için geçerli olan Microsoft Edge ayarlarını filtreler. Tüm göz atma özellikleriyle Microsoft Edge 'in tam bir sürümünü çalıştırır.
- **Genel göz atma (çok uygulama bilgi noktası)**: bir Windows 10 çok uygulama bilgi noktasında genel göz atma için geçerli olan Microsoft Edge ayarlarını filtreler.  Microsoft Edge InPrivate 'ın çok bölgeli bir sürümünü çalıştırır.

> [!TIP]
> Bu seçeneklerin ne yaptığı hakkında daha fazla bilgi için bkz. [Microsoft Edge bilgi noktası modu yapılandırma türleri](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

Bu cihaz kısıtlamaları profili, [Windows bilgi noktası ayarları](kiosk-settings-windows.md)kullanılarak oluşturduğunuz bilgi noktası profiliyle doğrudan ilgilidir. Özetlemek gerekirse:

1. Cihazı bilgi noktası modunda çalıştırmak için [Windows bilgi noktası ayarları](kiosk-settings-windows.md) profilini oluşturun. Uygulama olarak Microsoft Edge ' i seçin ve bilgi noktası profilinde Microsoft Edge bilgi noktası modunu ayarlayın.
2. Bu makalede açıklanan cihaz kısıtlamaları profilini oluşturun ve Microsoft Edge 'de izin verilen belirli özellikleri ve ayarları yapılandırın. Bilgi noktası profilinizde ([Windows bilgi noktası ayarları](kiosk-settings-windows.md)) seçili olan Microsoft Edge bilgi noktası modu türünü seçtiğinizden emin olun. 

    [Desteklenen bilgi noktası modu ayarları](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) harika bir kaynaktır.

> [!IMPORTANT] 
> Bu Microsoft Edge profilini, bilgi noktası profilinizle aynı cihazlara ([Windows bilgi noktası ayarları](kiosk-settings-windows.md)) atadığınızdan emin olun.

[ConfigureKioskMode CSP](/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>Deneyim başlangıcı

- **Microsoft Edge 'i Ile Başlat**: Microsoft Edge başladığında hangi sayfaların açılacağını seçin. Seçenekleriniz şunlardır:
  - **Özel başlangıç sayfaları**: gibi başlangıç sayfalarını girin `http://www.contoso.com` . Microsoft Edge, girdiğiniz başlangıç sayfalarını yükler.
  - **Yeni sekme sayfası**: **Yeni sekme URL 'Si** ayarında Microsoft Edge yükleme her şey girilir.
  - **Son oturum sayfası**: Microsoft Edge son oturum sayfasını yükler.
  - **Yerel uygulama ayarlarındaki sayfaları Başlat**: Microsoft Edge, işletim sistemi tarafından tanımlanan varsayılan başlangıç sayfası ile başlar.

- **Kullanıcının başlangıç sayfalarını değiştirmesine Izin ver**: **Evet** (varsayılan), kullanıcıların başlangıç sayfalarını değiştirmesine izin verir. Yöneticiler, `EdgeHomepageUrls` Varsayılan olarak Microsoft Edge 'i açtığınızda kullanıcıların göreceği başlangıç sayfalarını girmek için kullanabilir. **Hayır** , kullanıcıların başlangıç sayfalarını değiştirmesini engeller.
- **Yeni sekme sayfasında Web Içeriğine Izin ver**: **Evet** (varsayılan) olarak ayarlandığında, Microsoft Edge **Yeni sekme URL 'si** ayarında girilen URL 'yi açar. **Yeni sekme URL 'si** ayarı boşsa, Microsoft Edge, Microsoft Edge ayarlarında listelenen yeni sekme sayfasını açar. Kullanıcılar bunu değiştirebilir. **Hayır**olarak ayarlandığında, Microsoft Edge boş bir sayfayla yeni bir sekme açar. Kullanıcılar bu değişikliği değiştiremezler.
- **Yeni sekme URL 'si**: yeni sekme sayfasında açılacak URL 'yi girin. Örneğin `https://www.bing.com` veya `https://www.contoso.com` girin.

- **Giriş düğmesi**: Giriş düğmesi seçildiğinde ne olacağını seçin. Seçenekleriniz şunlardır:
  - **Başlangıç sayfaları**: **Microsoft Edge** 'i ayarla ayarında seçtiğiniz seçeneği açar
  - **Yeni sekme sayfası**: **Yeni sekme URL 'si** ayarında girdiğiniz URL 'yi açar.
  - **Giriş düğmesi URL 'si**: açılacak URL 'yi girin. Örneğin `https://www.bing.com` veya `https://www.contoso.com` girin.
  - **Giriş düğmesini Gizle**: giriş düğmesini gizler
- **Kullanıcıların giriş düğmesini değiştirmesine Izin ver**: **Evet** seçeneği, kullanıcıların giriş düğmesini değiştirmesine izin verir. Kullanıcı değişiklikleri tüm yönetici ayarlarını giriş düğmesine geçersiz kılar. **Hayır** (varsayılan), kullanıcıların giriş düğmesini yöneticinin nasıl yapılandırmasıyla değiştirmesini engeller.
- **Ilk çalıştırma deneyimini göster sayfası (yalnızca mobil)**: **Evet** (varsayılan) Microsoft Edge 'de ilk kullanıma giriş sayfasını gösterir. **Hayır** , Microsoft Edge 'i ilk kez çalıştırdığınızda giriş sayfasının gösterilmesini engeller. Bu özellik, bu sayfayı engellemek için sıfır emisyonlarını yapılandırmasına kayıtlı kuruluşlar gibi kuruluşlara izin verir.
- **Ilk çalıştırma DENEYIMI URL listesi konumu** (yalnızca Windows 10 Mobile): ilk çalıştırma sayfa URL 'SINI içeren XML dosyasına işaret eden URL 'yi girin. Örneğin, `https://www.contoso.com/sites.xml` girin.

- **Boşta kalma zamanından sonra tarayıcıyı yenile**: 0-1440 dakika içinde tarayıcı yenilenene kadar boşta kalma dakikalarının sayısını girin. Varsayılan değer `5` dakikadır. `0`(Sıfır) olarak ayarlandığında tarayıcı, boşta kaldıktan sonra yenilenmez.

  Bu ayar yalnızca [InPrivate genel göz atma (tek uygulama bilgi noktası)](#use-microsoft-edge-kiosk-mode)içinde çalıştırılırken kullanılabilir.

- **Açılır pencerelere Izin ver** (yalnızca masaüstü): **Evet** (varsayılan) Web tarayıcısında açılır pencerelere izin verir. **Hayır** , tarayıcıda açılır pencereleri engeller.
- **Internet Explorer 'a intranet trafiği gönder** (yalnızca masaüstü): **Evet** seçeneği, kullanıcıların Intranet web sitelerini Microsoft Edge yerine Internet Explorer 'da açmasına olanak sağlar. Bu ayar geriye dönük uyumluluk içindir. **Hayır** (varsayılan), kullanıcıların Microsoft Edge kullanmasına izin verir.
- **Kuruluş modu Site listesi konumu** (yalnızca masaüstü): Kurumsal modda açık bir Web siteleri LISTESINI içeren XML dosyasına işaret eden URL 'yi girin. Kullanıcılar bu listeyi değiştiremez. Örneğin, `https://www.contoso.com/sites.xml` girin.
- **Internet Explorer 'da siteler açılırken ileti**: Microsoft Edge 'i bir site Internet Explorer 11 ' de açılmadan önce bildirim gösterecek şekilde yapılandırmak için bu ayarı kullanın. Seçenekleriniz şunlardır:
  - **İleti gösterme**: işletim sistemi varsayılan davranışı kullanılır, bu durum bir ileti göstermez.
  - **Sitenin Internet Explorer 11 ' de açıldığını belirten Iletiyi göster**: IE 'de siteleri açarken iletiyi göster. IE 'de açık siteler. 
  - **Microsoft Edge 'de siteleri açma seçeneği içeren Iletiyi göster**: siteleri Microsoft Edge 'de açarken iletiyi göster. Bu ileti, kullanıcıların IE yerine Microsoft Edge 'i seçebilmeleri için **Microsoft Edge bağlantısını kullanmaya devam** eder.

  > [!IMPORTANT]
  > Bu ayar, **Kurumsal mod site listesi konumu** ayarını, **Intranet trafiğini Internet Explorer 'a gönder** ayarını veya her iki ayarı da kullanmanızı gerektirir.

- **Microsoft uyumluluk listesine Izin ver**: **Evet** (varsayılan) bir Microsoft Uyumluluk Listesi kullanılmasına izin verir. **Hayır** , Microsoft Edge 'de Microsoft Uyumluluk Listesi 'ni engeller. Microsoft 'un bu listesi, Microsoft Edge 'in bilinen uyumluluk sorunlarına sahip siteleri düzgün şekilde görüntülemesine yardımcı olur.
- **Başlangıç sayfalarını ve yeni sekme sayfasını Önyükle**: **Evet** (varsayılan), bu sayfaları önceden yüklemek için olabilecek işletim sistemi varsayılan davranışını kullanır. Önceden yükleme, Microsoft Edge 'i başlatma ve yeni sekmeler yükleme süresini en aza indirir. **Hayır** , Microsoft Edge 'in başlangıç sayfalarını ve yeni sekme sayfasını önyüklenmesini engeller.
- **Başlangıç sayfaları ve yeni sekme sayfası ön başlatması**: **Evet** (varsayılan), bu sayfaları önceden başlatmak olabilecek işletim sistemi varsayılan davranışını kullanır. Önceden başlatma, Microsoft Edge performansına yardımcı olur ve Microsoft Edge 'i başlatmak için gereken süreyi en aza indirir. **Hayır** , Microsoft Edge 'in başlangıç sayfalarını ve yeni sekme sayfasını başlatmasını önler.

### <a name="favorites-and-search"></a>Sık Kullanılanlar ve arama

- **Sık Kullanılanlar çubuğunu göster**: herhangi bir Microsoft Edge sayfasında Sık Kullanılanlar çubuğunda ne olacağını seçin. Seçenekleriniz şunlardır:
  - **Başlangıç ve yeni sekme sayfalarında**: Microsoft Edge başladığında ve tüm sekme sayfalarında Sık Kullanılanlar çubuğunu gösterir. Kullanıcılar bu ayarı değiştirebilir.
  - **Tüm sayfalarda**: tüm sayfalarda Sık Kullanılanlar çubuğunu gösterir. Kullanıcılar bu ayarı değiştiremezler.
  - **Gizli**: tüm sayfalarda Sık Kullanılanlar çubuğunu gizler. Kullanıcılar bu ayarı değiştiremezler.
- **Sık kullanılanlara değişikliklere Izin ver**: **Evet** (varsayılan), kullanıcıların listeyi değiştirmesine izin veren işletim sistemi varsayılanını kullanır. **Hayır** , kullanıcıların sık kullanılanlar listesini eklemesini, içeri aktarmayı, sıralamasını veya düzenlemesini engeller.
  - **Sık Kullanılanlar listesi**: Sık Kullanılanlar dosyasına URL 'lerin bir listesini ekleyin. Örneğin, `http://contoso.com/favorites.html` ekleyin.
- **Microsoft tarayıcıları arasında sık kullanılanları Eşitle** (yalnızca masaüstü): **Evet** , Windows 'un Internet Explorer ve Microsoft Edge arasında sık kullanılanları eşitlemesine zorlar. Sık Kullanılanlar için eklemeler, silmeler, değişiklikler ve düzen değişiklikleri, tarayıcılar arasında paylaşılır.  **Hayır** (varsayılan) işletim sistemi varsayılanını kullanır, bu da kullanıcılara tarayıcılar arasında sık kullanılanları eşitleme seçeneği verebilir.
- **Varsayılan arama motoru**: cihazda varsayılan arama altyapısını seçin. Kullanıcılar, bu değeri dilediğiniz zaman değiştirebilir. Seçenekleriniz şunlardır:
  - İstemci Microsoft Edge ayarları 'nda arama altyapısı
  - Bing
  - Google
  - Yahoo
  - Özel değer: **OpenSearch XML URL 'Si**içinde, kısa adı ve arama altyapısının URL 'sini IÇEREN BIR https URL 'sini en düşük düzeyde girin. Örneğin, `https://www.contoso.com/opensearch.xml` girin.
- **Arama önerilerini göster**: **Evet** (varsayılan) arama motorunuzun, adres çubuğuna arama ifadeleri yazarken site önermesine izin verir. **Hayır** bu özelliği engeller.
- **Arama altyapısında değişikliklere Izin ver**: **Evet** (varsayılan), kullanıcıların yeni arama motorları eklemesine veya Microsoft Edge 'de varsayılan arama altyapısını değiştirmesine izin verir. Kullanıcıların arama altyapısını özelleştirmesini engellemek için **Hayır** ' ı seçin.

  Bu ayar yalnızca [normal modda (çok uygulama bilgi noktası)](#use-microsoft-edge-kiosk-mode)çalışırken kullanılabilir.

### <a name="privacy-and-security"></a>Gizlilik ve güvenlik

- **InPrivate gözatmaya Izin ver**: **Evet** (varsayılan), Microsoft Edge 'de InPrivate gözatmaya izin verir. Tüm InPrivate sekmeleri kapatıldıktan sonra Microsoft Edge, tarama verilerini cihazdan siler. **Hayır** , kullanıcıların InPrivate Gözatma oturumlarını açmasını önler.
- **Gözatma geçmişini kaydet**: **Evet** (varsayılan) gözatma geçmişinin Microsoft Edge 'de kaydedilmesine izin verin. **Hayır** , gözatma geçmişinin kaydedilmesini engeller.
- **Çıkışta tarama verilerini temizle** (yalnızca masaüstü): **Evet** , kullanıcılar Microsoft Edge 'den çıkarken geçmişi temizler ve verilere göz atar. **Hayır** (varsayılan) işletim sistemi varsayılanını kullanır, bu da tarama verilerini önbelleğe alabilir.
- **Tarayıcı ayarlarını kullanıcının cihazları arasında Eşitle**: tarayıcı ayarlarını cihazlar arasında nasıl eşitlemek istediğinizi seçin. Seçenekleriniz şunlardır:
  - **Izin ver**: kullanıcıların cihazları arasında Microsoft Edge tarayıcı ayarlarının eşitlenmesine izin ver
  - **Kullanıcı geçersiz kılmayı engelle ve Etkinleştir**: Microsoft Edge tarayıcı ayarlarının kullanıcı cihazları arasında eşitlenmesini engelleyin. Kullanıcılar bu ayarı geçersiz kılabilir.
  - **Engelle**: Kullanıcı cihazları arasında Microsoft Edge tarayıcı ayarı eşitlemesini engelleyin. Kullanıcılar bu ayarı geçersiz kılamaz.

"Kullanıcı geçersiz kılmayı engelle" seçildiğinde, kullanıcı yönetici atamasını geçersiz kılabilir.

- **Parola Yöneticisi 'Ne Izin ver**: **Evet** (varsayılan), Microsoft Edge 'In otomatik olarak parola yöneticisini kullanmasına izin verir. Bu, kullanıcıların cihazdaki parolaları kaydetmesine ve yönetmesine olanak tanır. **Hayır** , Microsoft Edge 'In parola Yöneticisi 'ni kullanmasını engeller.
- **Tanımlama bilgileri**: Web tarayıcısında tanımlama bilgilerinin nasıl işlendiğini seçin. Seçenekleriniz şunlardır:
  - **Izin ver**: tanımlama bilgileri cihazda depolanıyor.
  - **Tüm tanımlama bilgilerini engelle**: tanımlama bilgileri cihazda depolanmaz.
  - **Yalnızca üçüncü taraf tanımlama bilgilerini engelle**: üçüncü taraf veya iş ortağı tanımlama bilgileri cihazda depolanmaz.
- **Formlarda otomatik doldurmaya Izin ver**: **Evet** (varsayılan), kullanıcıların tarayıcıdaki otomatik tamamlama ayarlarını değiştirmesine ve form alanlarını otomatik olarak doldurmasına izin verir. **Hayır** özelliği, Microsoft Edge 'de otomatik doldurma özelliğini devre dışı bırakır.
- **Do-Not-Track üst bilgileri gönder**: **Evet** , izleme bilgisi isteyen web sitelerine Do-Not-Track üst bilgilerini gönderir (önerilir). **Hayır** (varsayılan), Web sitelerinin kullanıcıyı izlemesine izin veren üst bilgileri göndermez. Kullanıcılar bu ayarı yapılandırabilir.
- **WebRTC localhost IP adresini göster**: **Evet** (varsayılan), bu protokol kullanılarak telefon ARAMALARı yapıldığında kullanıcıların localhost IP adresinin gösterilmesini sağlar. **Hayır** , KULLANıCıLARıN localhost IP adresinin gösterilmesini engeller. 
- **Canlı kutucuk veri toplamaya Izin ver**: **Evet** (varsayılan), Microsoft Edge 'In Başlat menüsüne sabitlenmiş canlı kutucuktan bilgi toplamasına izin verir. **Hayır** , kullanıcılara sınırlı bir deneyim sağlayabilen bu bilgilerin toplanmasını engeller.
- **Kullanıcı sertifika hatalarını geçersiz kılabilir**: **Evet** (varsayılan), kullanıcıların Güvenli Yuva Katmanı/Aktarım katmanı GÜVENLIĞI (SSL/TLS) hataları olan Web sitelerine erişmesine izin verir. **Hayır** (Artırılmış güvenlik için önerilir), kullanıcıların Web sitelerine SSL veya TLS hatalarıyla erişmesini önler.

### <a name="additional"></a>Ek

- **Microsoft Edge tarayıcısına Izin ver** (yalnızca mobil): **Evet** (varsayılan) mobil cihazda Microsoft Edge Web tarayıcısının kullanılmasına izin verir. **Hayır** , cihazlarda Microsoft Edge kullanımını engeller. **Hayır**' ı seçerseniz, diğer tek ayarlar yalnızca masaüstü için geçerlidir.
- **Adres çubuğu açılır listesine Izin ver**: **Evet** (varsayılan), Microsoft Edge 'in adres çubuğu açılır listesini öneriler listesiyle göstermesini sağlar. **Hayır** , Microsoft Edge 'in, yazarken açılan listede öneriler listesi göstermesini engeller. **Hayır**olarak ayarlandığında, şunları yapabilirsiniz:
  - Microsoft Edge ve Microsoft Hizmetleri arasındaki ağ bant genişliğini en aza indirmeye yardımcı olun.
  - Microsoft Edge > ayarlarını **Yazarken arama ve site önerilerini göster ' i** devre dışı bırakın.
- **Tam ekran moduna Izin ver**: **Evet** (varsayılan), Microsoft Edge 'in yalnızca Web Içeriğini gösteren ve Microsoft Edge Kullanıcı arabirimini gizleyen tam ekran modunu kullanmasına izin verir. **Hayır** , Microsoft Edge 'de tam ekran modunu engeller.
- **Bayrak hakkında Izin ver sayfası**: **Evet** (varsayılan), sayfanın erişimine izin verebilecek işletim sistemi varsayılanını kullanır `about:flags` . `about:flags`Sayfa, kullanıcıların geliştirici ayarlarını değiştirmesine ve deneysel özellikleri etkinleştirmesine olanak sağlar. **Hayır** `about:flags` , kullanıcıların Microsoft Edge 'de sayfaya erişmesini önler.
- **Geliştirici araçlarına Izin ver**: **Evet** (varsayılan), kullanıcıların varsayılan olarak Web sayfalarını derlemek ve hatalarını ayıklamak için F12 geliştirici araçlarını kullanmasına izin verir. **Hayır** , kullanıcıların F12 geliştirici araçlarını kullanmasını engeller.
- **JavaScript 'e Izin ver**: **Evet** (varsayılan) JavaScript gibi betiklerin Microsoft Edge tarayıcısında çalışmasına izin verir. **Hayır** , tarayıcıda Java betikleri çalıştırılmasını önler.
- **Kullanıcı Uzantıları yükleyebilir**: **Evet** (varsayılan), kullanıcıların cihazlara Microsoft Edge uzantıları yüklemesine izin verir. **Hayır** , yüklemeyi engeller.
- **Geliştirici uzantılarının dışarıdan yüklenmesine Izin ver**: **Evet** (varsayılan), dışarıdan yükleme izni olabilen işletim sistemi varsayılanını kullanır. Dışarıdan yükleme, doğrulanmamış uzantıları yükleyip çalıştırır. **Hayır** özelliği, **yükleme uzantıları** özelliğini kullanarak Microsoft Edge dışarıdan dışarıdan yüklemeye engel olur. PowerShell gibi diğer yollarla dışarıdan yükleme uzantılarının engellemez.
- **Gerekli uzantılar**: Microsoft Edge 'de kullanıcılar tarafından hangi uzantıların devre dışı bırakılamıyoruz ' i seçin. Paket aile adlarını girin ve **Ekle**' yi seçin. [Uygulama BAŞıNA VPN için bir paket aile adı (PFN) bulma](/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) bazı kılavuzluk sağlar.

  Ayrıca paket aile adlarını içeren bir CSV dosyasını **Içeri aktarabilirsiniz** . Ya da, girdiğiniz paket aile adlarını **dışarı aktarın** .

## <a name="network-proxy"></a>Ağ proxy’si

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [Networkproxy ILKESI CSP](/windows/client-management/mdm/networkproxy-csp)'sini kullanır.

- **Proxy ayarlarını otomatik olarak algıla**: **blok** cihazların bir proxy otomatik yapılandırma (PAC) betiğini otomatik olarak algılamasını devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği etkinleştirebilir ve cihazlar bir PAC betiğinin yolunu bulmaya çalışır.
- **Proxy betiği kullan**: proxy sunucusunu YAPıLANDıRMAK için Pac betiğinizin yolunu girmeye **izin ver** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bir PAC betiğine URL girmenize izin vermiyor olmayabilir.
  - **Kurulum komut dosyası adresi URL 'si**: proxy sunucusunu yapılandırmak için kullanmak istediğiniz Pac BETIĞININ URL 'sini girin.
- **El ile proxy sunucusu kullan**: bir proxy sunucusunun adını veya IP ADRESINI ve TCP bağlantı noktası numarasını el ile girmek Için **izin ver** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bir proxy sunucusunun ayrıntılarını el ile girmenize izin vermiyor.
  - **Adres**: proxy sunucusunun adını veya IP adresini girin.
  - **Bağlantı noktası numarası**: proxy sunucunuzun bağlantı noktası numarasını girin.
  - **Proxy özel durumları**: proxy sunucusunu kullanmamalıdır gereken URL 'leri girin. `;`Her öğeyi ayırmak için noktalı virgül () kullanın.
  - **Yerel adres için proxy sunucusunu atla**: **izin ver** , yerel intranet adresleri için proxy sunucusunu kullanmaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi intranetinizdeki yerel adresler için bir proxy sunucu kullanabilir.

## <a name="password"></a>Parola

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [DeviceLock ILKESI CSP](/windows/client-management/mdm/policy-csp-devicelock)'sini kullanır.

- **Parola**: kullanıcıların cihaza erişmek için bir parola **girmesini zorunlu kılar** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, bir parola olmadan cihazlara erişime izin verebilir. Yalnızca yerel hesaplar için geçerlidir. Etki alanı hesabı parolaları Active Directory (AD) ve Azure AD tarafından yapılandırılmış olarak kalır.

  [DeviceLock/DevicePasswordEnabled CSP 'si](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - **Gerekli parola türü**: parola türünü seçin. Seçenekleriniz şunlardır:
    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi parolanın rakam ve harf içermesi için izin verebilir.
    - **Alfasayısal**: parola sayıların ve harflerin karışımı olmalıdır.
    - **Sayısal**: parola yalnızca sayı olmalıdır.

    [DeviceLock/alfanümerik ıdevicepasswordrequired CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - **Minimum parola uzunluğu**: 4-16 adresinden gereken en az karakter sayısını girin. Örneğin, `6` parola uzunluğunun en az altı karakter gerektirmek için girin. Varsayılan olarak, işletim sistemi olarak ayarlayabilir `4` .
  
    [DeviceLock/MinDevicePasswordLength CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > Windows masaüstünde parola gereksinimi değiştirildiğinde, cihazlar boşta durumundan etkin 'e geçtiğinde, kullanıcılar bir sonraki oturum açışlarında etkilenir. Gereksinimi karşılayan parolalara sahip olan kullanıcılar parolalarını değiştirmelerini de istenir.

  - **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: Cihaz silinmeden önce izin verilen yanlış parola sayısını 11 ' e kadar girin. Girdiğiniz geçerli sayı sürüme bağlıdır. [DeviceLock/MaxDevicePasswordFailedAttempts CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) desteklenen değerleri listeler. `0` (sıfır) cihaz temizleme işlevini devre dışı bırakabilir.

    Bu ayarın Ayrıca sürüme bağlı olarak farklı etkileri vardır. Bu ayar hakkında ayrıntılı bilgi için bkz. [DeviceLock/MaxDevicePasswordFailedAttempts CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts).

  - **Ekran kilitlenmeden önce geçen işlem yapılmayan dakika sayısı**: ekran kilitlenmeden önce cihazın boşta kalması gereken sürenin uzunluğunu girin. Örneğin, `5` 5 dakika çalıştıktan sonra cihazları kilitlemek için yazın. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, `0` zaman aşımı olmayan (sıfır) olarak ayarlayabilir.

    [DeviceLock/MaxInactivityTimeDeviceLock CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **Parola kullanım süresi (gün)**: cihaz parolasının değiştirilme tarihi olan 1-365 ' dan gün cinsinden süre uzunluğunu girin. Örneğin, `90` 90 gün sonra parolanın süresini dolacak şekilde girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, `0` süresi dolmayan (sıfır) olarak ayarlayabilir.

    [DeviceLock/Devicepasswordexpiasyon CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **Önceki parolaların yeniden kullanılmasını engelle**: daha önce kullanılan ve 1-24 'den kullanılamayan parolaların sayısını girin. Örneğin, `5` kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.

    [DeviceLock/DevicePasswordHistory CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **Cihaz boşta durumundan çıktığında parola iste** (Mobile ve holographic): **gerektir** , kullanıcılardan, boşta kaldıktan sonra cihazın kilidini açmak için bir parola girmesini zorlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi boşta kaldıktan sonra PIN veya parola gerektirmeyebilir.

    [DeviceLock/AllowIdleReturnWithoutPassword CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **Basit parolalar**: **blok** , kullanıcıların veya gibi basit parolalar oluşturmasını engeller `1234` `1111` . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların basit parolalar oluşturmasına izin verebilir. Bu ayar, resim parolalarını kullanmayı da engeller.

    [DeviceLock/AllowSimpleDevicePassword CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **Asıfatı: bloğu sırasında otomatik şifreleme**, cihazlar ilk kullanım için hazırlandıktan sonra ve CIHAZLAR Azure AD 'ye katıldığında otomatik BitLocker cihaz şifrelemesini engeller. **Block** **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi şifrelemeyi etkinleştirebilir.

  [BitLocker cihaz şifrelemesi](/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption)hakkında daha fazla bilgi.

  [Güvenlik/koruyucu Tautomaticdeviceencryptionforazureadjoineddevices CSP](/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **Federal bilgi Işleme standardı (FIPS) ilkesi**: **izin ver** , şifreleme, karma ve imzalama için ABD devlet standardı olan Federal BILGI işleme standardı (FIPS) ilkesini kullanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi FIPS 'ye izin vermiyor.

  [Şifreleme/AllowFipsAlgorithmPolicy CSP](/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Windows Hello cihaz kimlik doğrulaması**: kullanıcıların bir Windows 10 bilgisayarında oturum açmak için telefon, uygunluk bandı veya IoT cihazı gibi bir Windows Hello yardımcı cihazı kullanmasına **izin verin** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, Windows Hello yardımcı cihazlarının kimlik doğrulamasından geçmasını önleyebilir.

  [Authentication/AllowSecondaryAuthenticationDevice CSP](/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Tercih edilen Azure AD kiracı etki alanı**: Azure AD kuruluşunuzda mevcut bir etki alanı adı girin. Bu etki alanındaki kullanıcılar oturum açtığında, etki alanı adını yazmak zorunda kalmaz. Örneğin, `contoso.com` girin. `contoso.com`Etki alanındaki kullanıcılar, yerine gibi kullanıcı adlarını kullanarak oturum açabilir `abby` `abby@contoso.com` .

  [Authentication/PreferredAadTenantDomainName CSP](/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>Uygulama başına gizlilik özel durumları

"Varsayılan gizlilik" bölümünde tanımladıklarınızdan farklı bir gizlilik davranışına sahip olması gereken uygulamaları **ekleyin** .

- **Paket adı**: uygulama paketi aile adı.
- **Uygulama adı**: uygulamanın adı.

### <a name="exceptions"></a>Özel durumlar

- **Hesap bilgileri**: Bu uygulamanın kullanıcı adına, resmine ve diğer kişi bilgilerine erişip erişemeyeceğini tanımlayın.
- **Arka plan uygulamaları**: Bu uygulamanın arka planda çalıştırılıp çalıştırılamayacağını tanımlayın.
- **Takvim**: Bu uygulamanın takvime erişip erişemeyeceğini tanımlayın.
- **Arama geçmişi**: Bu uygulamanın çağrı geçmişime erişip erişemeyeceğini tanımlayın.
- **Kamera**: Bu uygulamanın kameraya erişip erişemeyeceğini tanımlayın.
- **Kişiler**: Bu uygulamanın kişilere erişip erişemeyeceğini tanımlayın.
- **E-posta**: Bu uygulamanın e-postaya erişip erişemeyeceğini tanımlayın.
- **Konum**: Bu uygulamanın konum bilgilerine erişip erişemeyeceğini tanımlayın.
- **Mesajlaşma**: Bu uygulamanın metın veya MMS iletilerini okuyup okuyamayacağını veya gönderemeyeceğini tanımlayın.
- **Mikrofon**: Bu uygulamanın mikrofonu kullanıp kullanamayacağını tanımlayın.
- **Hareket**: Bu uygulamanın cihaz hareket bilgilerine erişip erişemeyeceğini tanımlayın.
- **Bildirimler**: Bu uygulamanın bildirimlere erişip erişemeyeceğini tanımlayın.
- **Telefon**: Bu uygulamanın telefona erişip erişemeyeceğini tanımlayın.
- **Radyolar**: bazı uygulamalar, veri göndermek ve almak ve Bu radyoların açık veya kapalı olması için cihazınızda radyoları (örneğin Bluetooth) kullanır. Bu uygulamanın bu radyoları denetleyip denetleyemeyeceğini tanımlayın.
- **Görevler**: Bu uygulamanın görevlerinize erişip erişemeyeceğini tanımlayın.
- **Güvenilen cihazlar**: Bu uygulamanın Güvenilen cihazları kullanıp kullanseçemediğini seçin. Güvenilen cihazlar, zaten bağlı olduğunuz donanımdır veya cihazla birlikte gelen donanımlardır. Örneğin, güvenilir cihazlar olarak televizyonlar, projektörler vb. kullanın.
- **Geri bildirim ve tanılama**: Bu uygulamanın tanılama bilgilerine erişip erişemeyeceğini tanımlayın.
- **Cihazlarla Eşitle**: Bu uygulamanın, cihazla açıkça eşleşmeyen kablosuz cihazlarla otomatik olarak bilgi paylaşıp eşitleyip eşitleyebileceğini seçin.

## <a name="personalization"></a>Kişiselleştirme

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [Kişiselleştirme ILKESI CSP](/windows/client-management/mdm/personalization-csp)'sini kullanır.

- **Masaüstü arka plan resmi URL 'si (yalnızca masaüstü)**: Windows masaüstü duvar kağıdı olarak kullanmak istediğiniz. jpg,. jpeg veya. png biçimindeki bir resmin URL 'sini girin. Kullanıcılar bu resmi değiştiremez. Örneğin, `https://contoso.com/logo.png` girin.

  Boş bırakılırsa, Intune bu ayarı değiştirmez veya güncelleştirmez.

## <a name="printer"></a>Yazıcı

- **Yazıcılar**: ağ ana bilgisayar ADLARıNı (DNS adı) kullanarak yazıcı ekleyin. İşletim sistemi, cihazdaki her yazıcı için eşleşen yazıcı sürücülerini arar ve kurar. Bir değer girmezseniz, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Eğitim/YazıcıAdı CSP](/windows/client-management/mdm/policy-csp-education#education-printernames)

- **Varsayılan yazıcı**: varsayılan yazıcı olarak kullanılacak yüklü bir yazıcının ağ ana bilgisayar adını (DNS adı) girin. Bir değer girmezseniz, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Eğitim/Defaultyazıcı_adı CSP](/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **Yeni yazıcı ekleme**: **Engelle** , kullanıcıların yeni yazıcı eklemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi yeni yazıcı eklemeye izin verebilir.

  [Eğitim/önleyici Taddingnewprinters CSP](/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## <a name="privacy"></a>Gizlilik

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [Gizlilik ILKESI CSP](/windows/client-management/mdm/policy-csp-privacy)'sini kullanır.

- **Gizlilik deneyimi**: **blok** , kullanıcılar oturum açtığında ve yeni ve yükseltilen kullanıcılar için açıldığında gizlilik deneyiminin açılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Gizlilik/DisablePrivacyExperience](/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **Giriş kişiselleştirme**: **blok** , dikte Için ses kullanımını ve Cortana ile Microsoft bulut tabanlı konuşma tanımayı kullanan diğer uygulamalarla konuşmasını önler. Devre dışıdır ve kullanıcılar, ayarları kullanarak çevrimiçi konuşma tanımayı etkinleştiremez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların seçebilmesine izin verebilir. Bu hizmetlere izin verirseniz Microsoft, hizmeti geliştirmek için sesli veri toplayabilir.

  [Gizlilik/Allowınputkişiselleştirmesi CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **Eşleştirme ve gizlilik Kullanıcı onay Istemlerini otomatik olarak kabul**et: **izin ver** ' i seçin. bu nedenle Windows, uygulamaları çalıştırırken eşleştirmeyi ve gizlilik izin iletilerini otomatik olarak kabul edebilir **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi otomatik kabulü engelleyebilir.

  [Gizlilik/AllowAutoAcceptPairingAndPrivacyConsentPrompts CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **Kullanıcı etkinliklerini Yayımla**: **blok** , uygulamaların ve işletim sisteminin kullanıcı etkinliklerini yayımlamasını önler. Aynı zamanda, Etkinlik akışında paylaşılan deneyimleri ve son kullanılan kaynakların bulunmasını da engeller. Kullanıcı etkinlikleri bir uygulamadaki veya işletim sistemindeki bir kullanıcının görevlerinin durumunu izler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi uygulamaların kullanıcı etkinliklerini yayımlayabilmesi için bu özelliği etkinleştirebilir.

  [Gizlilik/PublishUserActivities CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **Yalnızca yerel etkinlikler**: **blok** , paylaşılan deneyimleri ve yalnızca yerel etkinliğe bağlı olarak görev değiştiricisinde son kullanılan kaynakların bulunmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

Cihazdaki tüm uygulamaların erişebileceği bilgileri yapılandırabilirsiniz. Ayrıca, **uygulama başına gizlilik özel durumlarını**kullanarak uygulama temelinde özel durumlar tanımlayın.

### <a name="exceptions"></a>Özel durumlar

- **Hesap bilgileri**: Bu uygulamanın kullanıcı adına, resmine ve diğer kişi bilgilerine erişip erişemeyeceğini tanımlayın.
- **Arka plan uygulamaları**: Bu uygulamanın arka planda çalıştırılıp çalıştırılamayacağını tanımlayın.
- **Takvim**: Bu uygulamanın takvime erişip erişemeyeceğini tanımlayın.
- **Arama geçmişi**: Bu uygulamanın çağrı geçmişime erişip erişemeyeceğini tanımlayın.
- **Kamera**: Bu uygulamanın kameraya erişip erişemeyeceğini tanımlayın.
- **Kişiler**: Bu uygulamanın kişilere erişip erişemeyeceğini tanımlayın.
- **E-posta**: Bu uygulamanın e-postaya erişip erişemeyeceğini tanımlayın.
- **Konum**: Bu uygulamanın konum bilgilerine erişip erişemeyeceğini tanımlayın.
- **Mesajlaşma**: Bu uygulamanın metın veya MMS iletilerini okuyup okuyamayacağını veya gönderemeyeceğini tanımlayın.
- **Mikrofon**: Bu uygulamanın mikrofonu kullanıp kullanamayacağını tanımlayın.
- **Hareket**: Bu uygulamanın cihaz hareket bilgilerine erişip erişemeyeceğini tanımlayın.
- **Bildirimler**: Bu uygulamanın bildirimlere erişip erişemeyeceğini tanımlayın.
- **Telefon**: Bu uygulamanın telefona erişip erişemeyeceğini tanımlayın.
- **Radyolar**: bazı uygulamalar, veri göndermek ve almak ve Bu radyoların açık veya kapalı olması için cihazınızda radyoları (örneğin Bluetooth) kullanır. Bu uygulamanın bu radyoları denetleyip denetleyemeyeceğini tanımlayın.
- **Görevler**: Bu uygulamanın görevlerinize erişip erişemeyeceğini tanımlayın.
- **Güvenilen cihazlar**: Bu uygulamanın Güvenilen cihazları kullanıp kullanseçemediğini seçin. Güvenilen cihazlar, zaten bağlı olduğunuz donanımdır veya cihazla birlikte gelen donanımlardır. Örneğin, güvenilir cihazlar olarak televizyonlar, projektörler vb. kullanın.
- **Geri bildirim ve tanılama**: Bu uygulamanın tanılama bilgilerine erişip erişe, bu uygulamayı seçin.
- **Cihazlarla eşitle** - Bu uygulamanın bu PC, tablet veya telefonla açıkça eşleştirilmemiş kablosuz cihazlarla otomatik olarak bilgi paylaşma ve eşitleme işlemleri yapıp yapamayacağını tanımlayın.

## <a name="projection"></a>Projeksiyon

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [kablolu Lessdisplay Ilke CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay)'sini kullanır.

- **Kablosuz Görüntü alıcılarından Kullanıcı girişi**: **engelleme** , kablosuz görüntü alıcılarından Kullanıcı girişini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kablosuz bir ekran 'nin kaynak cihaza klavye, fare, kalem ve dokunmatik giriş göndermesini sağlayabilir.

  [Kablosuzekran/AllowUserInputFromWirelessDisplayReceiver CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **Bu bilgisayara yansıtma**: **blok** , diğer cihazların yansıtma için cihaz bulmasını önler ve diğer cihazlara yansıtımasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazların bulunabilir olmasını sağlayabilir ve kilit ekranının üzerinde cihaza proje verebilir.

  [Kablolu Lessdisplay/AllowProjectionFromPC CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **Eşleştirme IÇIN PIN gerektir**: bir projeksiyon cihazına bağlanırken her zaman PIN istemlerini **iste** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, cihazı eşleştirmek için bir PIN gerektirmeyebilir.

  [Kablolu Lessdisplay/Requirepınforıdentifier CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## <a name="reporting-and-telemetry"></a>Raporlama ve telemetri

- **Kullanım verilerini paylaşma**: gönderilen tanılama verilerinin düzeyini seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar gönderilen düzeyi seçer. Varsayılan olarak, işletim sistemi herhangi bir veri paylaşmayabilir.
  - **Güvenlik**: bağlı kullanıcı deneyimi ve telemetri bileşen ayarları, kötü amaçlı yazılım kaldırma aracı ve Microsoft Defender hakkındaki veriler de dahil olmak üzere Windows 'un daha güvenli kalmasına yardımcı olmak için gereken bilgiler
  - **Temel**: kalite ile ilgili veriler, uygulama uyumluluğu, uygulama kullanımı verileri ve güvenlik düzeyinden alınan veriler de dahil olmak üzere temel cihaz bilgileri
  - **Gelişmiş**: Windows, Windows Server, System Center ve uygulamaların nasıl kullanıldığı, nasıl gerçekleştirdikleri, gelişmiş güvenilirlik verileri ve hem temel hem de güvenlik seviyelerine ait veriler dahil olmak üzere ek Öngörüler
  - **Full**: sorunları belirlemek ve gidermek için gereken tüm veriler ve güvenlik, temel ve Gelişmiş düzeydeki veriler.

  [System/Allowtelemetri CSP 'si](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **Microsoft Edge tarama verilerini Microsoft 365 Analytics 'e gönder**: Bu özelliği kullanmak için, **kullanım verilerini paylaşma** ayarlarını **Gelişmiş** veya **tam**olarak ayarlayın. Bu özellik, Microsoft Edge 'in yapılandırılmış ticari KIMLIĞI olan kurumsal cihazlarda Microsoft 365 Analytics 'e gönderdiği verileri denetler. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi hiçbir göz atma geçmişi verisi toplamayabilir veya gönderemeyebilir.
  - **Yalnızca intranet verilerini Gönder**: yöneticinin intranet veri geçmişini göndermesini sağlar.
  - **Yalnızca internet verilerini Gönder**: yöneticinin Internet veri geçmişini göndermesini sağlar.
  - **Intranet ve internet verileri gönderme**: yöneticinin intranet ve Internet veri geçmişini göndermesini sağlar.

  [Tarayıcı/ConfigureTelemetryForMicrosoft365Analytics CSP](/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Telemetri proxy sunucusu**: bağlı kullanıcı deneyimlerini ve telemetri isteklerini iletmek için bir proxy sunucusunun tam etki alanı adını (FQDN) veya IP adresini (bir GÜVENLI yuva KATMANı (SSL) bağlantısı kullanarak girin. Bu ayarın biçimi *sunucu*:*bağlantı noktası* olur. Adlandırılmış ara sunucu başarısız olursa veya bir ara sunucu girilmemişse, bağlı kullanıcı deneyimleri ve telemetri verileri gönderilmez. Yerel cihazda kalır.

  Bir değer girmezseniz, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, bağlı kullanıcı deneyimlerini ve telemetri verilerini varsayılan ara sunucu yapılandırmasını kullanarak Microsoft 'a gönderebilir.

  Örnek biçimler:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [System/TelemetryProxy CSP](/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

## <a name="search"></a>Arayın

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [arama ILKESI CSP](/windows/client-management/mdm/policy-csp-search)'sini kullanır.

- **Güvenli Arama (yalnızca mobil)**: Cortana 'nın, arama sonuçlarında yetişkinlere yönelik içeriği nasıl filtreleyeceğini denetleyin. Seçenekleriniz şunlardır:
  - **Kullanıcı tanımlı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kendi ayarlarını seçer.
  - **Katı**: yetişkin içerikli en yüksek filtreleme
  - **Orta**: yetişkinlere yönelik içeriğe göre orta filtreleme. Geçerli arama sonuçları filtrelenmez.
- **Aramada Web sonuçlarını görüntüle**: **Block** , kullanıcıların Internet 'Te arama yapmak için Windows Search kullanmasını engeller ve arama sırasında Web sonuçları gösterilmez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Web 'de arama yapmasına izin verebilir ve sonuçlar cihazda gösterilir.
- **Aksanlar**: **blok** aksanların Windows Search 'te gösterilmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi aksan işareti gösterebilir.

  [Search/Allowusingaksanlar CSP](/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **Otomatik dil algılama**: **blok** , içerik veya özellikleri dizinlerken Windows Search 'un dili otomatik olarak algılamasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.

  [Search/Alwaysuseoto Langdetection CSP](/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **Arama konumu**: **Block** , Windows Search 'un konumu kullanmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.

  [Search/AllowSearchToUseLocation CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **Dizin Oluşturucu geri**alma: **blok** arama Dizin Oluşturucu geri alma özelliğini devre dışı bırakır. Dizin oluşturma, sistem etkinliği yüksek olsa bile tam hızda devam eder. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, IŞLETIM sistemi, sistem etkinliği yüksek olduğunda dizin oluşturma etkinliğini kısıtlamak için geri alma mantığını kullanabilir.

  [Arama/DisableBackoff CSP](/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **Çıkarılabilir sürücü dizini oluşturma**: **blok** , Çıkarılabilir sürücülerdeki konumların kitaplıklara eklenmesini ve dizin oluşturulmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.

  [Search/Disableremovabledrivedizin oluşturma CSP](/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **Yetersiz disk alanı dizin oluşturma**: **Etkinleştir** ayarı, disk alanı azaldığında bile otomatik dizin oluşturmaya izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi sabit disk alanı 600 MB veya daha az olduğunda otomatik dizin oluşturmayı kapatabilir. Kuruluşunuzdaki cihazlarda sabit disk alanı sınırlıysa, **Yapılandırılmadı**olarak ayarlayın.

  [Search/Preventındexinglowdiskspacemb CSP](/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **Uzaktan sorgular**: **Etkinleştir** , cihazın dizininin uzak sorgularına izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazın dizinini uzaktan sorgulamasını engelleyebilir.

  [Search/PreventRemoteQueries CSP](/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## <a name="start"></a>Başlangıç

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [Başlangıç ILKESI CSP](/windows/client-management/mdm/policy-csp-start)'sini kullanır.  

- **Başlangıç menüsü düzeni**: özelleştirmeleri IÇEREN bir XML dosyasını karşıya yükleyin, bu da uygulamaların listelendiği sıralama ve daha fazlasını içerir. XML dosyası varsayılan başlangıç yerleşimini geçersiz kılar. Kullanıcılar girdiğiniz başlangıç menüsü yerleşimini değiştiremezler.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Başlat/StartLayout CSP 'si](/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **Web sitelerini Başlangıç menüsünde kutucuklara sabitle**: Microsoft Edge 'den resimleri içeri aktarma. Bu görüntüler masaüstü cihazlar için Windows Başlat menüsünde bağlantılar olarak gösterilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Başlangıç/ımportedgevarlıklarının CSP 'si](/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **Görev çubuğundan uygulamaları kaldırma**: **blok** kullanıcıların görev çubuğundan uygulama bağlantısını kaldırmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların görev çubuğundan uygulama kaydetmesine izin verebilir.

  [Start/Nopinningtogörev çubuğu CSP 'si](/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **Hızlı Kullanıcı geçişi**: **blok** , oturum açmadan aynı anda oturum açan kullanıcılar arasında geçiş yapılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Kullanıcı kutucuğunda **Kullanıcı Değiştir** ' i gösterebilir.

  [Start/HideSwitchAccount CSP](/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **En çok kullanılan uygulamalar**: **blok** , en çok kullanılan uygulamaların başlangıç menüsünde gösterilmesini gizler. Bu ayrıca Ayarlar uygulamasında aynı ada sahip iki durumlu ayarı da devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi en sık kullanılan uygulamaları gösterebilir.

  [Start/Hierteleme Entlyusedapps CSP](/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **Son eklenen uygulamalar**: **blok** , son eklenen uygulamaları başlangıç menüsünde gizler. Bu ayrıca Ayarlar uygulamasında aynı ada sahip iki durumlu ayarı da devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi başlangıç menüsünde en son eklenen uygulamaları gösterebilir.

  [Start/HideRecentlyAddedApps CSP](/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **Başlangıç ekranı modu**: başlangıç ekranının boyutunu seçin. Seçenekleriniz şunlardır:
  - **Kullanıcı tanımlı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar boyutu ayarlayabilir.
  - **Tam ekran**: başlangıç boyutunu tam ekran olarak zorlar.
  - **Tam ekran: tam**ekran olmayan bir başlangıç boyutu zorla.

  [Start/ForceStartSize CSP](/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **Atlama listelerinde son açılan öğeler**: **blok** , son atlama listelerinin başlangıç menüsünde ve görev çubuğunda gösterilmesinin gizlenmesini engeller. Bu ayrıca Ayarlar uygulamasında aynı ada sahip iki durumlu ayarı da devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi atlama listelerinde son açılan öğeleri gösterebilir.

  [Start/HideRecentJumplists CSP](/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **Uygulama listesi**: tüm uygulamalar listelerinin nasıl gösterileceğini seçin. Seçenekleriniz şunlardır:
  - **Kullanıcı tanımlı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar uygulama listesinin nasıl gösterileceğini seçer.
  - **Daralt**: tüm uygulamalar listesini gizler.
  - **Ayarlar uygulamasını daraltma ve devre dışı bırakma**: tüm uygulamalar listesini gizler ve Ayarlar uygulamasındaki **Başlangıç menüsünde uygulama listesini göster** ' i devre dışı bırakır.
  - **Ayarları uygulamayı kaldırır ve devre dışı bırakır**: tüm uygulamalar listesini gizler, tüm uygulamalar düğmesini kaldırır ve Ayarlar uygulamasındaki **Başlangıç menüsünde uygulama listesini göster** ' i devre dışı bırakır.

  [Start/HideAppList CSP](/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **Güç düğmesi**: **blok** , başlangıç menüsündeki güç düğmesini gizler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi güç düğmesini gösterebilir.

  [Start/HidePowerButton CSP](/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **Kullanıcı kutucuğu**: **engelleme** , başlangıç menüsündeki Kullanıcı kutucuğunu gizler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Kullanıcı kutucuğunu gösterebilir. Aşağıdaki ayarları yapılandırın:
  - **Lock**: **Block** , başlangıç menüsündeki Kullanıcı kutucuğunda **kilit** seçeneğini gizler.  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi **kilit** seçeneğini gösterebilir.
  - **Oturumu**kapat: **Engelle** , başlangıç menüsündeki Kullanıcı kutucuğunda **oturumu** Kapat seçeneğini gizler. **Yapılandırılmadı** (varsayılan) **oturumu** Kapat seçeneğini gösterir.

  [Start/Hideuserkutucuk CSP 'si](/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **Kapat**: **Engelle** , Başlat menüsündeki güç düğmesinde **Güncelleştir ve Kapat** ve **Kapat** seçeneklerini gizler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Start/Hidekapatması CSP](/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **Sleep**: **blok** , başlangıç menüsündeki güç düğmesinde **uyku** seçeneğini gizler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Başlat/HideSleep CSP](/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **Hazırda Beklet**: **Engelle** , başlangıç menüsündeki güç düğmesinde **Hazırda Beklet** seçeneğini gizler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Başlat/Hidehazırda beklet CSP](/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **Hesap değiştir**: **Engelle** , başlangıç menüsündeki Kullanıcı kutucuğunda **anahtar hesabını** gizler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Start/HideSwitchAccount CSP](/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Yeniden başlatma seçenekleri**:  **Engelle** , Başlat menüsündeki güç düğmesinde **güncelleştirme ve yeniden başlatma** ve **yeniden başlatma** seçeneklerini gizler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Start/HideRestart CSP](/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **Başlangıç 'Ta belgeler**: Windows Başlat menüsünde Belgeler klasörünü gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/AllowPinnedFolderDocuments CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **Başlangıç 'Ta indirmeler**: Windows Başlat menüsünde indirmeler klasörünü gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/AllowPinnedFolderDownloads CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **Başlangıç 'Ta dosya Gezgini**: Windows Başlat menüsünde Dosya Gezgini 'ni gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/AllowPinnedFolderFileExplorer CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **Başlangıç 'Ta ev grubu**: Windows Başlangıç menüsünde ev grubu kısayolunu gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/Allowpinnedfolderev grubu CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **Başlangıç 'Ta müzik**: Windows Başlat menüsünde müzik klasörünü gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/AllowPinnedFolderMusic CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **Başlangıç 'Ta ağ**: Windows başlat menüsünü ağa gelen gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/AllowPinnedFolderNetwork CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **Başlangıç klasörü**: Windows Başlat menüsünde Kişisel klasörünü gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/Allowpinnedfolderpersonfolder CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **Başlangıç 'Ta resimler**: Windows Başlat menüsünde resimlerin klasörünü gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/Allowpinnedfolderresimlerim CSP 'si](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **Başlangıç ayarları**: Windows Başlat menüsünde ayarlar kısayolunu gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/AllowPinnedFolderSettings CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **Başlamadan videolar**: Windows Başlat menüsünde videoların klasörünü gizleyin veya gösterin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar kısayolu göstermeyi veya gizlemeyi seçer.
  - **Gizle**: kısayol gizlenir ve Ayarlar uygulamasında ayar devre dışıdır.
  - **Göster**: kısayol gösterilir ve Ayarlar uygulamasında ayar devre dışıdır.

  [Start/Allowpinnedfoldervideolarım CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **Microsoft Edge Için SmartScreen**: **gerektir** , Microsoft Defender SmartScreen 'i etkinleştirir ve kullanıcıların bunu kapatmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi SmartScreen 'i açıp kullanıcıların açıp kapatmasına izin verebilir.

  Microsoft Edge, kullanıcıların olası kimlik avı dolandırıcılarından ve kötü amaçlı yazılımlardan korunması için Microsoft Defender SmartScreen (açık) kullanır.

  [Tarayıcı/AllowSmartScreen CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Kötü amaçlı site erişimi**: **blok** kullanıcıların Microsoft Defender SmartScreen Filtresi uyarılarını yok saymalarını engeller ve siteye gitmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların uyarıları yoksaymasına ve siteye devam etmesine izin verebilir.

  [Tarayıcı/PreventSmartScreenPromptOverride CSP](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Doğrulanmamış dosya indirme**: **engelleme** , kullanıcıların Microsoft Defender SmartScreen Filtresi uyarılarını yok saymalarını engeller ve doğrulanmamış dosyaları indirmelerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların uyarıları yoksaymasına ve doğrulanmamış dosyaları indirmeye devam etmesine izin verebilir.

  [Tarayıcı/PreventSmartScreenPromptOverrideForFiles CSP](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Windows Spot

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [deneyim ILKESI CSP](/windows/client-management/mdm/policy-csp-experience)'sini kullanır.

- **Windows spot**: **blok** kilit ekranında Windows spot 'u, Windows ipuçlarını, Microsoft tüketici özelliklerini ve diğer ilgili özellikleri kapatır. Amacınız, cihazlardan gelen ağ trafiğini en aza indirmektir, **Evet**' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Windows spot özelliklerine izin verebilir ve kullanıcılar tarafından denetlenebilir.

  [Deneyim/AllowWindowsSpotlight CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  **Yapılandırılmadı**olarak ayarlandığında, aşağıdaki ayarları da izin verebilir veya engelleyebilirsiniz:

  - **Kilit ekranında Windows spot**: **blok** Windows spot 'un cihaz kilitleme ekranında bilgi göstermesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kilit ekranında Windows spot bilgilerini gösterebilir.

    [Deneyim/ConfigureWindowsSpotlightOnLockScreen CSP](/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Windows spot 'Ta üçüncü taraf önerileri**: blok Windows spot 'un Microsoft tarafından yayımlanmamış içerik önermasını **önleyemez** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iş ortaklarından uygulama ve içerik önerilerine izin verebilir ve başlangıç menüsünde önerilen uygulamaları ve Windows ipuçlarını gösterebilir.

    [Deneyim/AllowThirdPartySuggestionsInWindowsSpotlight CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **Tüketici özellikleri**: **engelleme** , başlangıç önerileri, üyelik bildirimleri, kutudan çıkarma deneyimi uygulama yüklemesi ve yeniden yönlendirme kutucukları gibi tüketicilere yönelik deneyimler kapatır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

    [Deneyim/AllowWindowsConsumerFeatures CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Windows ipuçları**: **blok** açılır pencere ipuçlarını devre dışı bırakır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Windows Ipuçlarının gösterilmesini sağlayabilir.

    [Deneyim/AllowWindowsTips CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **İşlem merkezi 'Nde Windows spot**: **blok** , Windows spot bildirimlerinin işlem merkezinde gösterilmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların Windows 'da daha üretken olmalarını sağlamak için uygulama veya özellik öneren Işlem merkezinde bildirimleri gösterebilir.

    [Deneyim/AllowWindowsSpotlightOnActionCenter CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Windows spot kişiselleştirme**: **blok** , Windows 'un kullanıcılara özelleştirilmiş deneyimler sağlaması için tanılama verilerini kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Microsoft 'un Kullanıcı ihtiyaçlarına göre Windows 'u uyarlamak için özelleştirilmiş öneriler, ipuçları ve teklifler sağlamak üzere tanılama verilerini kullanmasına izin verebilir.

    [Deneyim/AllowTailoredExperiencesWithDiagnosticData CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Windows hoş geldiniz deneyimi**: **blok** Windows spot Windows hoş geldiniz deneyimi özelliğini kapatır. Windows Karşılama deneyimi, Windows 'da ve uygulamalarında güncelleştirmeler ve değişiklikler olduğunda gösterilmez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Kullanıcı bilgilerini yeni veya güncelleştirilmiş özelliklerle gösteren Windows Karşılama deneyimine izin verebilir.

    [Deneyim/AllowWindowsSpotlightWindowsWelcomeExperience CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender virüsten koruma

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [Defender Ilke CSP](/windows/client-management/mdm/policy-csp-defender)'sini kullanır.

- **Gerçek zamanlı izleme**: **Etkinleştir** kötü amaçlı yazılım, casus yazılım ve diğer istenmeyen yazılım için gerçek zamanlı taramayı etkinleştirir. Kullanıcılar bu uygulamayı kapatamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği etkinleştirir ve kullanıcıların değiştirmesini sağlar.

  Bu ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowRealtimeMonitoring CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Davranış izleme**: **etkinleştirme** davranış izlemeyi etkinleştirir ve cihazlarda bilinen şüpheli etkinlik desenlerini denetler. Kullanıcılar davranış izlemeyi kapatamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi davranış Izlemeyi açabilir ve kullanıcıların bunu değiştirmesine izin verebilir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowBehaviorMonitoring CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Ağ İnceleme sistemi (NIS)**: NIS, cihazları ağ tabanlı saldırılara karşı korumaya yardımcı olur. Kötü amaçlı trafiği algılamaya ve engellemeye yardımcı olmak için Microsoft Endpoint Protection Center’dan bilinen açıkların imzalarını kullanır.

  - **Etkinleştir**: ağ korumasını ve ağ engellemeyi etkinleştirir. Kullanıcılar bu uygulamayı kapatamaz. Etkinleştirildiğinde, kullanıcıların bilinen güvenlik açıklarına bağlanması engellenir.

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi NIS 'yi etkinleştirir ve kullanıcıların bunu değiştirmesine izin verir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/EnableNetworkProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Tüm Indirmeleri Tara**: **Etkinleştir** ayarı bu ayarı açar ve Defender, Internet 'ten indirilen tüm dosyaları tarar. Kullanıcılar bu ayarı kapatamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu ayarı açabilir ve kullanıcıların bunu değiştirmesine izin verebilir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/Allowwioavprotection CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Microsoft Web tarayıcılarında yüklenen dosyaları tara**: **Etkinleştir** , Defender 'ın Internet Explorer 'da kullanılan betikleri taramasını sağlar. Kullanıcılar bu ayarı kapatamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu ayarı açabilir ve kullanıcıların bunu değiştirmesine izin verebilir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowScriptScanning CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Defender 'A Son Kullanıcı erişimi**: **blok** , Microsoft Defender Kullanıcı arabirimini kullanıcılardan gizler. Tüm Microsoft Defender bildirimleri de bastırılır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, Microsoft Defender Kullanıcı arabirimine Kullanıcı erişimine izin verebilir ve kullanıcıların bunu değiştirmesine izin verebilir.

  Ayarı engeller ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  Bu ayar değiştirildiğinde, cihaz bir dahaki sefer yeniden başlatıldığında devreye girer.

  [Defender/AllowUserUIAccess CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Güvenlik Zekası güncelleştirme aralığı (saat)**: Defender 'ın, 0-24 adresinden yeni güvenlik zekasını denetlediği aralığı girin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. İşletim sistemi varsayılanı, güncelleştirmeleri her 8 saatte bir denetleyebilir.
  - **Denetleme**: Defender yeni güvenlik zekası güncelleştirmelerini denetlemez.
  - **1-24**: `1` saatte bir denetim yapın, her iki saatte bir denetim yapın, `2` `24` her gün kontrol eder.
  
  [Defender/Signatureupdateınterval CSP](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Dosya ve program etkinliğini izle**: Defender 'ın cihazlarda dosya ve program etkinliğini izlemesine izin verir. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. İşletim sistemi varsayılanı tüm dosyaları izleyebilir.
  - **İzleme devre dışı**
  - **Tüm dosyaları izle**
  - **Yalnızca gelen dosyaları izle**
  - **Yalnızca giden dosyaları izle**

  [Defender/RealTimeScanDirection CSP 'si](/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Karantinaya alınan kötü amaçlı yazılımı silmeden önce geçen gün**: daha önce etkilenen cihazları el ile kontrol edebilmeniz için, girdiğiniz gün sayısı için çözümlenmiş kötü amaçlı yazılımı izlemeye devam edin 

  Bu ayarı yapılandırmazsanız veya gün olarak ayarlarsanız `0` , kötü amaçlı yazılım Karantina klasöründe kalır ve otomatik olarak kaldırılmaz. Olarak ayarlandığında `90` , karantina öğeleri sistemde 90 gün süreyle depolanır ve sonra kaldırılır.

  [Defender/DaysToRetainCleanedMalware CSP](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Tarama sırasında CPU kullanım sınırı**: taramaların kullanmasına ızın verilen CPU miktarını `0` yüzde ile sınırlayın `100` . Varsayılan olarak, işletim sistemi bunu %50 olarak ayarlayabilir.
- **Arşiv dosyalarını Tara**: **Enable** , zip veya CAB dosyaları gibi arşiv dosyalarını taramak için Defender 'ı etkinleştirir. Kullanıcılar bu ayarı kapatamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu taramayı açabilir ve kullanıcıların bunu değiştirmesine izin verebilir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowArchiveScanning CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Gelen posta Iletilerini Tara**: **Enable** , Defender 'ın cihazlara geldikçe e-posta iletilerini taramasını sağlar. Etkinleştirildiğinde, altyapı posta gövdesini ve eklerini çözümlemek için posta kutusu ve posta dosyalarını ayrıştırır. . PST (Outlook),. dbx,. mbx, MIME (Outlook Express) ve BinHex (Mac) biçimlerini tarayabilirsiniz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu taramayı kapatır ve kullanıcıların bunu değiştirmesine izin verir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowEmailScanning CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Tam tarama sırasında çıkarılabilir sürücüleri Tara**: **Etkinleştir** ayarı, tam tarama sırasında Defender çıkarılabilir sürücü taramalarını etkinleştirir. Kullanıcılar bu ayarı kapatamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Defender 'ın USB sürücüleri gibi çıkarılabilir sürücüleri taramasına ve kullanıcıların bu ayarı değiştirmesine izin verebilir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Bir hızlı tarama sırasında, çıkarılabilir sürücüler yine de taranabilecek.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowFullScanRemovableDriveScanning CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Tam tarama sırasında eşlenmiş ağ sürücülerine Tara**: **Etkinleştir** , Defender tarafından eşlenen ağ sürücülerindeki dosyaları tarar. Sürücüdeki dosyalar salt okunurdur, Defender bu bilgisayarlarda bulunan herhangi bir kötü amaçlı yazılımı kaldıramıyor. Kullanıcılar bu ayarı kapatamaz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği etkinleştirir ve kullanıcıların değiştirmesini sağlar.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır. 

  Hızlı tarama sırasında, eşlenmiş ağ sürücüleri yine de taranamaz.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowFullScanOnMappedNetworkDrives CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Ağ klasörlerinden açılan dosyaları tara**: **Enable** Defender, bir UNC yolundan erişilen dosyalar gibi ağ klasörlerinden veya paylaşılan ağ sürücülerinden açılan dosyaları tarar. Kullanıcılar bu ayarı kapatamaz. Sürücüdeki dosyalar salt okunurdur, Defender bu bilgisayarlarda bulunan herhangi bir kötü amaçlı yazılımı kaldıramıyor.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Ağ klasörlerinden açılan dosyaları tarar ve kullanıcıların bunu değiştirmesine izin verir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowScanningNetworkFiles CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Bulut koruması**: **etkinleştirme** , yönettiğiniz cihazlardan gelen kötü amaçlı yazılım etkinlikleri hakkında bilgi almak için Microsoft etkin koruma hizmeti açar. Kullanıcılar bu ayarı değiştiremezler. 

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Microsoft Etkin Koruma Hizmeti bilgi almasına izin verir ve kullanıcıların bu ayarı değiştirmesine izin verir.

  Ayarı etkinleştirir ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce yapılandırılmış durumda bırakır.

  Intune bu özelliği devre dışı bırakır. Devre dışı bırakmak için özel bir URI kullanın.

  [Defender/AllowCloudProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Örnek gönderimi yapmadan önce kullanıcılara sor**: daha fazla analiz gerektirebilecek kötü amaçlı olabilecek dosyaların otomatik olarak Microsoft 'a gönderilip gönderilmeyeceğini denetler. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. İşletim sistemi varsayılanı, güvenli örnekleri otomatik olarak gönderebilir.
  - **Her zaman sor**
  - **Kişisel verileri göndermeden önce sor**
  - **Hiçbir şekilde veri gönderme**
  - **Tüm verileri sorulmadan gönder**: veriler otomatik olarak gönderilir.

  [Defender/Submitsamplesonay CSP 'si](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Günlük hızlı tarama gerçekleştirme süresi**: günlük hızlı tarama çalıştırmak için saati seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu taramayı 2 ' de çalıştırabilir.

  Daha fazla özelleştirme istiyorsanız, ayar **yapmak için sistem taraması türünü** yapılandırın.

  [Defender/ScheduleQuickScanTime CSP](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Gerçekleştirilecek sistem taraması türü**: tarama düzeyini ve taramanın çalıştırılacağı günü ve saati içeren bir sistem taraması zamanlayın. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar, gerektiğinde taramaları el ile çalıştırabilir veya cihazlarına ister.
  - **Devre dışı bırak**: cihazlarda sistem taramasını devre dışı bırakır. Cihazları tarayan bir iş ortağı virüsten koruma çözümü kullanıyorsanız bu seçeneği belirleyin.
  - **Hızlı tarama**: kayıt defteri anahtarları ve bilinen Windows başlangıç klasörleri gibi kötü amaçlı yazılımın kaydedildiği yaygın konumlara bakar.
    - **Zamanlanan gün**: taramanın çalıştırılacağı günü seçin.
    - **Zamanlanan saat**: taramanın çalıştırılacağı saati seçin.
  - **Tam tarama**: kötü amaçlı yazılımın kaydedildiği yaygın konumlara bakar ve cihazdaki her dosyayı ve klasörü tarar.
    - **Zamanlanan gün**: taramanın çalıştırılacağı günü seçin.
    - **Zamanlanan saat**: taramanın çalıştırılacağı saati seçin.

  > [!TIP]
  > Bu ayar **günlük hızlı tarama ayarı gerçekleştirme zamanına** göre çakışabilir. Bazı öneriler:  
  >
  > - Günlük hızlı tarama ve haftalık tam tarama zamanlamak istiyorsanız:
  >   1. **Günlük hızlı tarama ayarı gerçekleştirme saatini** yapılandırın.
  >   2. Tam tarama yapmak için **gerçekleştirilecek sistem taraması türünü** yapılandırın.
  > 
  > - Her gün yalnızca bir hızlı tarama (tam tarama yok) istiyorsanız, her iki ayarı kullanın: **günlük hızlı tarama** veya **gerçekleştirilecek sistem taraması türü**. Örneğin, 6 ' da her Salı günde bir hızlı tarama çalıştırmak için, ayar **yapmak için sistem taraması türünü** yapılandırın.
  > 
  > - **Hızlı tarama**olarak ayarlanacak **sistem taraması türü** ile **günlük hızlı tarama ayarı gerçekleştirmek için geçen süreyi** yapılandırmayın. Bu ayarlar çakışabilir ve bir tarama çalışmayabilir.

  [Defender/ScanParameter CSP](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [Defender/ScheduleScanDay CSP](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [Defender/ScheduleScanTime CSP](/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- İstenmeyebilecek **uygulamaları Algıla**: Bu özellik, istenmeyebilecek UYGULAMALARı (pua), ağınıza indirme ve yükleme konusunda tanımlar ve engeller. Bu uygulamalar virüsler, kötü amaçlı yazılım veya diğer tehdit türleri olarak kabul edilmez. Ancak, performans veya kullanımını etkileyebilecek uç noktalar üzerinde eylemler çalıştırabilir. Windows PUAs algıladığında koruma düzeyini seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, Microsoft Defender bu özelliği devre dışı bırakabilir.
  - **Kapalı**: Pua koruması kapalı.
  - **Etkinleştir**: Microsoft Defender PUAs 'i algılar ve algılanan öğeler engellenir. Bu öğeler, diğer tehditlerle birlikte geçmiş olarak gösterilir.
  - **Denetim**: Microsoft Defender PUAs 'i algılar, ancak hiçbir işlem gerçekleşmez. Microsoft Defender 'ın işlem yapması için gereken uygulamalarla ilgili bilgileri gözden geçirebilirsiniz. Örneğin, Olay Görüntüleyicisi Microsoft Defender tarafından oluşturulan olayları arayın.

  İstenmeyebilecek uygulamalar hakkında daha fazla bilgi için bkz. istenmeyebilecek [uygulamaları algılama ve engelleme](/windows/security/threat-protection/microsoft-defender-antivirus/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus).

  [Defender/PUAProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Örnek gönderme onayı**: Şu anda bu ayarın etkisi yoktur. Bu ayarı kullanmayın. Gelecekteki bir sürümde kaldırılabilir.

- **Erişim koruması**: **blok** , erişilen veya indirilen dosyaların taranmasını engeller. Kullanıcılar açamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği etkinleştirebilir ve kullanıcıların bunu değiştirmesine izin verir.

  Ayarı engelleyemez ve sonra **Yapılandırılmadı**olarak değiştirirseniz, Intune ayarı daha önce işletim sistemi tarafından yapılandırılan durumunda bırakır.

  Intune bu özelliği kullanmaz. Etkinleştirmek için özel bir URI kullanın.

  [Defender/AllowOnAccessProtection CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Algılanan kötü amaçlı yazılım tehditleri eylemleri**: Defender 'ın algıladığı her tehdit düzeyi için hangi eylemleri istediğini belirlemek için **Etkinleştir** ' i seçin: düşük, orta, yüksek ve önemli. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Microsoft Defender 'ın en iyi seçeneği seçmesini sağlayabilir.

  **Etkinleştir**olarak ayarlandığında, eylemi seçin:
  
  - **Temizlenemedi**
  - **Karantina**
  - **Kaldır**
  - **İzin Ver**
  - **Kullanıcı tanımlı**
  - **Block**

  Eyleminiz mümkün değilse, Microsoft Defender tehdit 'nin düzeltildiğinden emin olmak için en iyi seçeneği seçer.

  [Defender/ThreatSeverityDefaultAction CSP](/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender virüsten koruma dışlamaları

Dışlama listelerini değiştirerek, belirli dosyaları Microsoft Defender virüsten koruma taramalarından dışlayabilirsiniz. **Genellikle, dışlamaları uygulamanız gerekmez**. Microsoft Defender virüsten koruma, şirket yönetimi, veritabanı yönetimi ve diğer kurumsal senaryolar ve durumlar gibi bilinen işletim sistemi davranışlarına ve tipik yönetim dosyalarına dayalı olarak çeşitli otomatik dışlamaları içerir.

> [!WARNING]
> **Dışlamaları tanımlama, Microsoft Defender virüsten koruma tarafından sunulan korumayı düşürür**. Dışlamaları uygulamayla ilişkili riskleri her zaman değerlendirin. Yalnızca kötü amaçlı olmayan bildiğiniz dosyaları hariç tutun.

- **Taramaların ve gerçek zamanlı korumanın dışında tutulacak dosya ve klasörler**: dışlamalar listesine **C:\path** veya **% ProgramFiles% \Path\filename.exe** gibi bir veya daha fazla dosya ve klasör ekler. Bu dosya ve klasörler gerçek zamanlı veya zamanlanmış hiçbir taramaya katılmaz.
- **Taramaların ve gerçek zamanlı korumanın dışında tutulacak dosya uzantıları**: dışlamalar listesine **jpg** veya **txt** gibi bir veya daha fazla dosya uzantısı ekleyin. Bu uzantılara sahip tüm dosyalar gerçek zamanlı veya zamanlanmış taramalara dahil değildir.
- **Taramaların ve gerçek zamanlı korumanın dışında tutulacak süreçler**: dışlamalar listesine **. exe**, **. com**veya **. scr** türünde bir veya daha fazla işlem ekleyin. Bu süreçler gerçek zamanlı veya zamanlanmış taramalara dahil değildir.

## <a name="power-settings"></a>Güç ayarları

Bu ayarlar, desteklenen Windows sürümlerini de listeleyen [Güç ILKESI CSP](/windows/client-management/mdm/policy-csp-power)'sini kullanır.

### <a name="battery"></a>Pil

- **Enerji tasarrufunu açmak Için pil düzeyi**: cihaz pil gücünü kullanırken, 0-100 adresinden enerji tasarrufu 'nı açmak için pil ücreti düzeyini girin. Pil ücreti düzeyini gösteren bir yüzde değeri girin. Örneğin, olarak ayarlandığında `80` , pil %80 ücret veya daha az kullanılabilir olduğunda enerji tasarrufu ' nı etkinleştirir.

  Bir değer girmezseniz, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bunu %70 olarak ayarlayabilir.

  [Güç/enerji Gysaverbatteryıthresholdonpili CSP](/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Kapağı kapatma (yalnızca mobil)**: cihaz pil gücünü kullanırken, kapak kapatıldığında ne olacağını seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarı denetlemesine izin verebilir.
  - **Eylem yok**: cihaz açık kalır ve pil gücünü kullanmaya devam eder.
  - **Uyku**: Cihaz uyku moduna geçer ve az miktarda pil ücreti kullanır. Bilgisayar hala açık ve açık uygulamalar ve dosyalar rasgele erişimli bellek (RAM) içinde depolanır.
  - **Hazırda Beklet**: cihaz hazırda bekleme moduna girer. Açık uygulamalar ve dosyalar sabit diskte depolanır ve cihaz kapanır.
  - **Kapat**: Cihaz kapanıyor. Açık uygulamalar ve dosyalar kaydedilmeden kapalıdır.

  [Power/Selectlidcloseactiononpili CSP](/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Güç düğmesi**: cihaz pil gücünü kullanırken, güç düğmesi seçildiğinde ne olacağını seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarı denetlemesine izin verebilir.
  - **Eylem yok**: cihaz açık kalır ve pil gücünü kullanmaya devam eder.
  - **Uyku**: Cihaz uyku moduna geçer ve az miktarda pil ücreti kullanır. Bilgisayar hala açık ve açık uygulamalar ve dosyalar rasgele erişimli bellek (RAM) içinde depolanır.
  - **Hazırda Beklet**: cihaz hazırda bekleme moduna girer. Açık uygulamalar ve dosyalar sabit diskte depolanır ve cihaz kapanır.
  - **Kapat**: Cihaz kapanıyor. Açık uygulamalar ve dosyalar kaydedilmeden kapalıdır.

  [Power/Selectpowerbuttonactiononpili CSP](/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Uyku düğmesi**: cihaz pil gücünü kullanırken, uyku düğmesi seçildiğinde ne olacağını seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarı denetlemesine izin verebilir.
  - **Eylem yok**: cihaz açık kalır ve pil gücünü kullanmaya devam eder.
  - **Uyku**: Cihaz uyku moduna geçer ve az miktarda pil ücreti kullanır. Bilgisayar hala açık ve açık uygulamalar ve dosyalar rasgele erişimli bellek (RAM) içinde depolanır.
  - **Hazırda Beklet**: cihaz hazırda bekleme moduna girer. Açık uygulamalar ve dosyalar sabit diskte depolanır ve cihaz kapanır.
  - **Kapat**: Cihaz kapanıyor. Açık uygulamalar ve dosyalar kaydedilmeden kapalıdır.

  [Power/Selecttur Epbuttonactiononpili CSP](/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Karma uyku**: cihaz pil gücünü kullanırken karma uyku moduna izin vermeyi veya devre dışı bırakmayı seçin.

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarı denetlemesine izin verebilir.
  - **Etkinleştir**: cihazlar karma uyku moduna geçebilir. Açık uygulamalar ve dosyalar, rastgele erişim belleği (RAM) ve sabit disk üzerinde depolanır. Bu, az miktarda pil ücreti kullanır.
  - **Devre dışı bırak**: cihazların karma uyku moduna geçmesini önler.

  [Power/Turnoffhybridstaeponpili CSP](/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>Pluggedın

- **Enerji tasarrufunu açmak Için pil düzeyi**: cihaz prize takılıyken, 0-100 adresinden enerji tasarrufu 'nı açmak için pil ücreti düzeyini girin. Pil ücreti düzeyini gösteren bir yüzde değeri girin. Örneğin, olarak ayarlandığında `80` , pil %80 ücret veya daha az kullanılabilir olduğunda enerji tasarrufu ' nı etkinleştirir.

  Bir değer girmezseniz, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bunu %70 olarak ayarlayabilir.

  [Güç/enerji Gysaverbatteryıthresholdpluggedın CSP](/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Kapağı kapatma (yalnızca mobil)**: cihaz prize takılıyken, kapak kapatıldığında ne olacağını seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Eylem yok**: cihaz açık kalır.
  - **Uyku**: Cihaz uyku moduna girer. Bilgisayar hala açık ve açık uygulamalar ve dosyalar rasgele erişimli bellek (RAM) içinde depolanır.
  - **Hazırda Beklet**: cihaz hazırda bekleme moduna girer. Açık uygulamalar ve dosyalar sabit diskte depolanır ve cihaz kapanır.
  - **Kapat**: Cihaz kapanıyor. Açık uygulamalar ve dosyalar kaydedilmeden kapalıdır.
  
    [Power/Selectlidcloseactionpluggedın CSP](/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Güç düğmesi**: cihaz prize takılıyken, güç düğmesi seçildiğinde ne olacağını seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Eylem yok**: cihaz açık kalır.
  - **Uyku**: Cihaz uyku moduna girer. Bilgisayar hala açık ve açık uygulamalar ve dosyalar rasgele erişimli bellek (RAM) içinde depolanır.
  - **Hazırda Beklet**: cihaz hazırda bekleme moduna girer. Açık uygulamalar ve dosyalar sabit diskte depolanır ve cihaz kapanır.
  - **Kapat**: Cihaz kapanıyor. Açık uygulamalar ve dosyalar kaydedilmeden kapalıdır.

  [Power/Selectpowerbuttonactionpluggedın CSP](/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Uyku düğmesi**: cihaz prize takılıyken, uyku düğmesi seçildiğinde ne olacağını seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Eylem yok**: cihaz açık kalır.
  - **Uyku**: Cihaz uyku moduna girer. Bilgisayar hala açık ve açık uygulamalar ve dosyalar rasgele erişimli bellek (RAM) içinde depolanır.
  - **Hazırda Beklet**: cihaz hazırda bekleme moduna girer. Açık uygulamalar ve dosyalar sabit diskte depolanır ve cihaz kapanır.
  - **Kapat**: Cihaz kapanıyor. Açık uygulamalar ve dosyalar kaydedilmeden kapalıdır.

  [Power/Selecttur Epbuttonactionpluggedın CSP](/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Karma uyku**: cihaz prize takılıyken karma uyku moduna izin vermeyi veya devre dışı bırakmayı seçin.

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarı denetlemesine izin verebilir.
  - **Etkinleştir**: cihazlar karma uyku moduna geçebilir. Açık uygulamalar ve dosyalar, rastgele erişim belleği (RAM) ve sabit disk üzerinde depolanır.
  - **Devre dışı bırak**: cihazların karma uyku moduna geçmesini önler.

  [Power/Turnoffhybridstaeppluggedın CSP](/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Sonraki adımlar

Her bir ayara dair ek teknik ayrıntılar ve hangi Windows sürümlerinin desteklendiği hakkında bilgi için bkz. [Windows 10 İlke CSP Başvurusu](/windows/client-management/mdm/policy-configuration-service-provider)

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).