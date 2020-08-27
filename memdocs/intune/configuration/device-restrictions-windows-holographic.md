---
title: Windows holographic Business cihaz ayarları-Microsoft Intune-Azure | Microsoft Docs
description: Windows holographic for Business için Microsoft Intune cihaz kısıtlama ayarlarını okuyun ve yapılandırın. Kayıt kaldırma, coğrafi konum, parolalar, App Store 'dan uygulama yüklemesi, tanımlama bilgileri ve açılır pencereler, Microsoft Defender, arama, bulut ve depolama, Bluetooth bağlantısı, sistem saati ve kullanım verileri.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2cd769b8e3ca4497c095210ea266d225354db24c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912840"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune kullanarak özelliklere izin vermek veya erişimi kısıtlamak için Windows holographic for Business cihaz ayarları

Bu makalede, Microsoft HoloLens gibi Windows holographic for Business cihazlarında denetleyebilmeniz için farklı ayarlar listelenmektedir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu ayarları, özelliklere izin vermek veya devre dışı bırakmak, güvenliği denetlemek ve daha fazlasını yapmak için kullanın.

Bir Intune Yöneticisi olarak bu ayarları oluşturabilir ve cihazlarınıza atayabilirsiniz.

## <a name="before-you-begin"></a>Başlamadan önce

[Windows 10 cihaz kısıtlamaları yapılandırma profili oluşturun](device-restrictions-configure.md#create-the-profile).

Bir Windows 10 cihaz kısıtlamaları yapılandırma profili oluşturduğunuzda, bu makalede listelenenden daha fazla ayar vardır. Bu makaledeki ayarlar Windows holographic for Business cihazlarında desteklenir.

## <a name="app-store"></a>App Store

- **Store 'dan uygulamaları otomatik güncelleştir**: **blok** , güncelleştirmelerin Microsoft Store otomatik olarak yüklenmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Microsoft Store yüklenen uygulamaların otomatik olarak güncelleştirilmesini sağlayabilir.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Güvenilen uygulama yüklemesi**: Microsoft Store olmayan uygulamalar yüklenebiliyorsa, dışarıdan yükleme olarak da bilinen ' yi seçin. Dışarıdan yükleme, Microsoft Store tarafından sertifikasız bir uygulamayı yüklüyor ve çalıştırmıyor. Örneğin, yalnızca şirket içi bir uygulama. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Engelle**: dışarıdan yüklemeyi engeller. Microsoft Store olmayan uygulamalar yüklenemez.
  - **Izin ver**: dışarıdan yüklemeyi sağlar. Microsoft Store olmayan uygulamalar yüklenebilir.

  [ApplicationManagement/AllowAllTrustedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Geliştirici kilidi açma**: dışarıdan yüklenen uygulamaların kullanıcılar tarafından değiştirilmesine izin verme gibi Windows Geliştirici ayarlarına izin verin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Engelle**: Geliştirici modunu ve dışarıdan yükleme uygulamalarını engeller.
  - **Izin ver**: geliştirici modu ve dışarıdan yükleme uygulamalarına izin verir.

  [ApplicationManagement/AllowDeveloperUnlock CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Hücresel ve Bağlantı

- **Bluetooth**: **blok** kullanıcıların Bluetooth 'u etkinleştirmelerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda Bluetooth 'a izin verebilir.

  [Bağlantı/AllowBluetooth CSP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Bluetooth bulunabilirliği**: **blok** cihazın diğer Bluetooth özellikli cihazlar tarafından keşfedilmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kulaklık gibi diğer Bluetooth özellikli cihazların cihazı bulmasına izin verebilir.

  [Bluetooth/AllowDiscoverableMode CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Bluetooth reklamcılık**: **blok** cihazın Bluetooth tanıtımları göndermesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazın Bluetooth tanıtımları göndermesini sağlayabilir.

  [Bluetooth/AllowAdvertising CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Bulut ve Depolama

- **Microsoft hesabı**: **Block** , kullanıcıların bir Microsoft hesabı cihazla ilişkilendirilmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Microsoft hesabı eklemeye ve kullanmaya izin verebilir.

  [Hesaplar/AllowMicrosoftAccountConnection CSP](/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Denetim Masası ve Ayarlar

- **Sistem saati değişikliği**: **Block** , kullanıcıların cihazdaki tarih ve saat ayarlarını değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bu ayarları değiştirmesine izin verebilir.

  [Ayarlar/AllowDateTime CSP](/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>Genel

- **El ile kayıt kaldırma**: **blok** , kullanıcıların cihazdaki çalışma alanı denetim masasını kullanarak çalışma alanı hesabını silmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Deneyim/Allowmanualmdmunkayıt CSP 'si](/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Coğrafi konum**: **blok** kullanıcıların cihazdaki konum hizmetlerini açmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [Deneyim/AllowFindMyDevice CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: **Block** , cihazda Cortana sesli yardımcısını devre dışı bırakır. Cortana devre dışı bırakıldığında, kullanıcılar hala cihazdaki öğeleri bulmak için arama yapabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi Cortana 'Ya izin verebilir.

  [Deneyim/AllowCortana CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Microsoft Edge Tarayıcısı

- **Deneyim başlangıcı**  >  **Açılır pencerelere Izin ver**: **Evet** (varsayılan) Web tarayıcısında açılır pencerelere izin verir. **Hayır** , tarayıcıda açılır pencereleri engeller.

  [Tarayıcı/Allowpopup CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Sık Kullanılanlar ve arama**  >  **Arama önerilerini göster**: **Evet** (varsayılan), adres çubuğuna arama ifadeleri yazarken arama motorunuzun siteleri önermesine izin verir. **Hayır** bu özelliği engeller.

  [Tarayıcı/Allowsearchmülationsınaddressbar CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Gizlilik ve güvenlik**  >  **Parola Yöneticisi 'Ne Izin ver**: **Evet** (varsayılan), Microsoft Edge 'In otomatik olarak parola yöneticisini kullanmasına izin verir. Bu, kullanıcıların cihazdaki parolaları kaydetmesine ve yönetmesine olanak tanır. **Hayır** , Microsoft Edge 'In parola Yöneticisi 'ni kullanmasını engeller.

  [Tarayıcı/AllowPasswordManager CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Gizlilik ve güvenlik**  >  **Tanımlama bilgileri**: Web tarayıcısında tanımlama bilgilerinin nasıl işlendiğini seçin. Seçenekleriniz şunlardır:
  - **Izin ver**: tanımlama bilgileri cihazda depolanıyor.
  - **Tüm tanımlama bilgilerini engelle**: tanımlama bilgileri cihazda depolanmaz.
  - **Yalnızca üçüncü taraf tanımlama bilgilerini engelle**: üçüncü taraf veya iş ortağı tanımlama bilgileri cihazda depolanmaz.

  [Tarayıcı/AllowCookies CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Gizlilik ve güvenlik**  >  **Do-Not-Track üst bilgileri gönder**: **Evet** , izleme bilgisi isteyen web sitelerine Do-Not-Track üst bilgilerini gönderir (önerilir). **Hayır** (varsayılan), Web sitelerinin kullanıcıyı izlemesine izin veren üst bilgileri göndermez. Kullanıcılar bu ayarı yapılandırabilir.

  [Tarayıcı/AllowDoNotTrack CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **Microsoft Edge Için SmartScreen**: **gerektir** , Microsoft Defender SmartScreen 'i etkinleştirir ve kullanıcıların bunu kapatmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi SmartScreen 'i açıp kullanıcıların açıp kapatmasına izin verebilir.

  [Tarayıcı/AllowSmartScreen CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>Parola

- **Parola**: kullanıcıların cihaza erişmek için bir parola **girmesini zorunlu kılar** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, bir parola olmadan cihazlara erişime izin verebilir. Yalnızca yerel hesaplar için geçerlidir. Etki alanı hesabı parolaları Active Directory (AD) ve Azure AD tarafından yapılandırılmış olarak kalır.

  [DeviceLock/DevicePasswordEnabled CSP 'si](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Cihaz boşta durumundan çıktığında parola gerektir**: ' ın, boşta kaldıktan sonra cihazın kilidini açmak için kullanıcılardan parola **girmesini zorunlu kılar** . **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi boşta kaldıktan sonra PIN veya parola gerektirmeyebilir.

  [DeviceLock/AllowIdleReturnWithoutPassword CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Raporlama ve Telemetri

- **Kullanım verilerini paylaşma**: gönderilen tanılama verilerinin düzeyini seçin. Seçenekleriniz şunlardır:

  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Hiçbir ayar zorunlu değildir. Kullanıcılar gönderilen düzeyi seçer. Varsayılan olarak, işletim sistemi herhangi bir veri paylaşmayabilir.
  - **Güvenlik**: bağlı kullanıcı deneyimi ve telemetri bileşen ayarları, kötü amaçlı yazılım kaldırma aracı ve Microsoft Defender hakkındaki veriler de dahil olmak üzere Windows 'un daha güvenli kalmasına yardımcı olmak için gereken bilgiler
  - **Temel**: kalite ile ilgili veriler, uygulama uyumluluğu, uygulama kullanımı verileri ve güvenlik düzeyinden alınan veriler de dahil olmak üzere temel cihaz bilgileri
  - **Gelişmiş**: Windows, Windows Server, System Center ve uygulamaların nasıl kullanıldığı, nasıl gerçekleştirdikleri, gelişmiş güvenilirlik verileri ve hem temel hem de güvenlik seviyelerine ait veriler dahil olmak üzere ek Öngörüler
  - **Full**: sorunları belirlemek ve gidermek için gereken tüm veriler ve güvenlik, temel ve Gelişmiş düzeydeki veriler.

  [System/Allowtelemetri CSP 'si](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>Arayın

- **Arama konumu**: **Block** , Windows Search 'un konumu kullanmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliğe izin verebilir.

  [Search/AllowSearchToUseLocation CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).