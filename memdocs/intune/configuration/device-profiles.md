---
title: Microsoft Intune'daki cihaz özellikleri ve ayarları - Azure | Microsoft Docs
description: Farklı Microsoft Intune cihaz profillerine genel bakış. Microsoft Endpoint Manager Yönetim merkezinde özellikler, kısıtlamalar, e-posta, WiFi, VPN, eğitim, sertifika, yükseltme Windows 10, BitLocker ve Microsoft Defender, Windows Information Protection, Yönetim Şablonları ve özel cihaz yapılandırma ayarlarını hakkında bilgi alın. Şirketinizdeki verileri ve cihazları yönetmek ve korumak için bu profilleri kullanın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5bf114edf17fa1f8959b5f26b83c771b711b83f5
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093180"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Microsoft Intune'daki cihaz profillerini kullanarak cihazlarınıza özellik ve ayar uygulama

Microsoft Intune, kuruluşunuzdaki farklı cihazlarda etkinleştirebileceğiniz veya devre dışı bırakabileceğiniz ayarları ve özellikleri içerir. Bu ayarlar ve özellikler "yapılandırma profillerine" eklenir. Farklı cihazlar ve iOS/ıpados, Android Cihaz Yöneticisi, Android Enterprise ve Windows dahil farklı platformlar için profiller oluşturabilirsiniz. Ardından Intune'u kullanarak bu profilleri cihazlara "atayabilirsiniz".

Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu yapılandırma profillerini kullanarak farklı görevler gerçekleştirebilirsiniz. Bazı profil örnekleri şunlardır:

- Windows 10 cihazlarda Internet Explorer'daki ActiveX denetimlerini engelleyen bir profil şablonu kullanabilirsiniz.
- İOS/ıpados ve macOS cihazlarında, kullanıcıların kuruluşunuzda AirPrint yazıcıları kullanmasına izin verin.
- Cihazların Bluetooth özelliğine erişim verebilir veya engelleyebilirsiniz.
- Kurumsal ağınıza farklı cihaz erişimi veren bir WiFi veya VPN profili oluşturabilirsiniz.
- Yazılım güncelleştirmelerini ve yükleme zamanlarını yönetebilirsiniz.
- Bir Android cihazını bir veya birden çok uygulamayı çalıştıran ayrılmış bilgi noktası cihazı olarak çalıştırabilirsiniz.

Bu makalede oluşturabileceğiniz profil türlerine genel bir bakış sağlanmaktadır. Cihazlardaki bazı özelliklere izin vermek veya bunları engellemek için bu profilleri kullanabilirsiniz.

## <a name="administrative-templates"></a>Yönetim şablonları

[Yönetim Şablonları](administrative-templates-windows.md) , Internet Explorer, Microsoft Edge, OneDrive, Uzak Masaüstü, Word, Excel ve diğer Office programları için yapılandırabileceğiniz yüzlerce ayarı içerir.

Yöneticiler, bu şablonlar sayesinde grup ilkelerine benzeyen ancak tamamen bulut tabanlı olan basitleştirilmiş bir görünüme sahip olur.

Bu özellik şunları destekler:

- Windows 10 ve üzeri

## <a name="certificates"></a>Sertifikalar

[Sertifikalar](../protect/certificates-configure.md), cihazlara atanan güvenilir, SCEP ve PKCS sertifikalarını yapılandırır. Bu sertifikalar WiFi, VPN ve e-posta profilleri için kimlik doğrulaması sağlar.

Bu özellik şunları destekler:

- Android cihaz yöneticisi
- Android Kurumsal
- iOS/iPadOS
- Mac OS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 ve üzeri

## <a name="custom-profile"></a>Özel profil

[Özel ayarlar](custom-settings-configure.md), yöneticilerin Intune'da yerleşik olarak sağlanmayan cihaz ayarlarını atamasına olanak tanır. Android cihazlarda, OMA-URI değerleri girebilirsiniz. İOS/ıpados cihazlarında, Apple Configurator 'da oluşturduğunuz bir yapılandırma dosyasını içeri aktarabilirsiniz.

Bu özellik şunları destekler:

- Android cihaz yöneticisi
- Android Kurumsal
- iOS/iPadOS
- Mac OS
- Windows Phone 8.1

## <a name="delivery-optimization"></a>Teslim iyileştirme

[Teslim iyileştirme](delivery-optimization-windows.md), yazılım güncelleştirmelerini teslim etmek için daha iyi bir deneyim sunar. Bu ayarlar **yazılım güncelleştirmeleri**  >  **Windows 10 güncelleştirme halkası** ayarlarını değiştiriyor.

Bu ayarları kullanarak yazılım güncelleştirmelerinin kuruluşunuzdaki ayarlara nasıl indirileceğini denetleyebilirsiniz. Örneğin kullanıcıların kendi güncelleştirmelerini yapmalarına izin verebilir veya teslim iyileştirme bulut hizmetlerini bir cihaz profilinde kullanarak güncelleştirmeleri almalarını sağlayabilirsiniz.

Bu özellik şunları destekler:

- Windows 10 ve üzeri

## <a name="derived-credential"></a>Türetilmiş kimlik bilgileri

[Türetilmiş kimlik bilgileri](../protect/derived-credentials.md) , kimlik doğrulama, imzalama ve şifreleme için akıllı kartlardaki sertifikalardır. Intune 'da, uygulamalar, e-posta profilleri, VPN, S/MIME ve Wi-Fi ' d e bağlanmak için bu kimlik bilgileriyle birlikte profiller oluşturabilirsiniz.

Bu özellik şunları destekler:

- Android Kurumsal
- iOS/iPadOS

## <a name="device-features"></a>Cihaz özellikleri

[Cihaz özellikleri](device-features-configure.md) , IOS/ıpados ve MacOS cihazlarındaki AirPrint, Notifications ve Lock Screen iletileri gibi özellikleri denetler.

Bu özellik şunları destekler:

- iOS/iPadOS
- Mac OS

## <a name="device-firmware-configuration-interface"></a>Cihaz üretici yazılımı yapılandırma arabirimi

[Cihaz üretici yazılımı yapılandırma arabirimi](device-firmware-configuration-interface-windows.md) (dfcı), yöneticilerin ıNTUNE kullanarak UEFı (BIOS) ayarlarını etkinleştirmesine veya devre dışı bırakmasına olanak sağlar. Bu ayarları, genellikle kötü amaçlı saldırılara karşı daha dayanıklı olan bellenim düzeyinde güvenliği geliştirmek için kullanın.

Bu özellik şunları destekler:

- Desteklenen bellenim üzerinde Windows 10 1809 ve üzeri

## <a name="device-restrictions"></a>Cihaz kısıtlamaları

[Cihaz kısıtlamaları](device-restrictions-configure.md) cihazlarda güvenlik, donanım, veri paylaşımı ve daha fazla ayarı denetler. Örneğin, iOS/ıpados cihaz kullanıcılarının cihaz kamerasını kullanmasını engelleyen bir cihaz kısıtlama profili oluşturun. 

Bu özellik şunları destekler:

- Android cihaz yöneticisi
- Android Kurumsal
- iOS/iPadOS
- Mac OS
- Windows 10 ve üzeri
- Windows 10 Team

## <a name="domain-join"></a>Etki alanına katılım

[Etki alanına ekleme](domain-join-configure.md) , şirket içi Active Directory etki alanı bilgilerini yapılandırır. Bu bilgiler, Windows Autopilot ve Intune kullanılarak sağlandığında karma Azure AD 'ye katılmış cihazlara dağıtılır. Bu profil, cihazlara hangi etki alanı ve OU 'ya katılacağını söyler.

Bu özellik şunları destekler:

- Windows 10 ve üzeri

## <a name="edition-upgrade-and-mode-switch"></a>Sürüm yükseltme ve mod değiştirme

[Windows 10 sürüm yükseltmeleri](edition-upgrade-configure-windows-10.md), Windows 10'un bazı sürümlerini çalıştıran cihazları otomatik olarak yeni bir sürüme yükseltmenizi sağlar.

Bu özellik şunları destekler:

- Windows 10 ve üzeri

## <a name="education"></a>Eğitim

[Eğitim ayarları - Windows 10](education-settings-configure.md), [Windows Sınav Zamanı uygulamasının](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) seçeneklerini yapılandırır. Bu seçenekleri yapılandırdığınızda, sınav tamamlanana kadar cihazda başka uygulama çalıştırılamaz.

[Eğitim ayarları-iOS/ıpados](../fundamentals/education-settings-configure-ios-shared.md) , ders içindeki öğrenci cihazlarını öğrenmeye ve denetlemeye kılavuzluk etmek için IOS/ıpados derslik uygulamasını kullanır. iPad cihazlarını, çok sayıda öğrencinin aynı cihazı paylaşmasını sağlamak için yapılandırabilirsiniz.

## <a name="email"></a>E-posta

[E-posta ayarları](email-settings-configure.md), cihazlarda Exchange ActiveSync e-posta ayarları oluşturur, atar ve izler. E-posta profilleri tutarlılık konusunda yardımcı olur, destek çağrılarını azaltır ve son kullanıcıların, herhangi bir kurulum yapmalarına gerek kalmadan kendi cihazlarından şirket e-postasına erişmelerini sağlar. 

Bu özellik şunları destekler:

- Android cihaz yöneticisi
- Android Kurumsal
- iOS/iPadOS
- Windows Phone 8.1
- Windows 10 ve üzeri

## <a name="endpoint-protection"></a>Endpoint protection

[Endpoint Protection](../protect/endpoint-protection-configure.md) , BitLocker ve Windows 10 cihazları Için Microsoft Defender ayarlarını yapılandırır. Ve, macOS cihazlarındaki güvenlik duvarını, ağ geçidini ve diğer kaynakları yapılandırın.

Microsoft Intune ile Microsoft Defender Gelişmiş tehdit koruması (WDADTP) eklemek için bkz. [mobil cihaz yönetimi (MDM) araçlarını kullanarak uç noktaları yapılandırma](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

Bu özellik şunları destekler:

- Mac OS
- Windows 10 ve üzeri

## <a name="esim-cellular---public-preview"></a>eSIM hücresel - Genel önizleme

[eSIM hücresel profilleri](esim-device-configuration.md), yöneticilere İnternet ve veri erişimi için yönetilen cihazlarınızda mobil İnternet tarifelerini yapılandırma olanağı sağlar. Mobil operatörünüzden etkinleştirme kodlarını aldıktan sonra bu etkinleştirme kodlarını içeri aktarmak ve ardından eSIM uyumlu cihazlarınıza atamak için Intune’u kullanabilirsiniz.

Bu özellik şunları destekler:

- Windows 10 Fall Creators Update ve üzeri

## <a name="extensions"></a>Uzantılar

[MacOS sistem uzantıları ve çekirdek uzantıları](kernel-extensions-overview-macos.md) , yöneticilerin işletim sisteminin yerel yeteneklerini genişleten özellikler veya programlar eklemesine olanak tanır. Bu ayarları, belirli bir geliştirici veya iş ortağındaki tüm uzantılara güvenmek veya belirli uzantılara izin vermek üzere yapılandırın.

Bu özellik şunları destekler:

- Mac OS

## <a name="identity-protection"></a>Kimlik koruması

[Kimlik koruması](../protect/identity-protection-configure.md), Windows 10 ve Windows 10 Mobile cihazlarda İş İçin Windows Hello deneyimini denetler. İş İçin Windows Hello’yu kullanıcı ve cihazlar için kullanılabilir kılmak ve cihaz PIN’i ve hareketlerini belirtmek için bu ayarları yapılandırın.  

Bu özellik şunları destekler:  

- Windows 10 ve üzeri
- Windows 10 Holographic for Business  

## <a name="kiosk"></a>Bilgi noktası

[Bilgi noktası ayarları](kiosk-settings.md) profili, cihazı tek uygulama veya birden çok uygulama çalıştıracak şekilde yapılandırır. Ayrıca bilgi noktanızda başlat menüsü ve web tarayıcısı gibi diğer özellikleri de özelleştirebilirsiniz.

Bu özellik şunları destekler:

- Windows 10 ve üzeri

Bilgi noktası ayarları, [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience)ve [iOS/ıpados](device-restrictions-ios.md#kiosk)için cihaz kısıtlamaları olarak da kullanılabilir.

## <a name="mx-profile-zebra"></a>MX profili (Zeköşeli)

[Mobility uzantıları (MX)](android-zebra-mx-overview.md) , yerleşik Intune ayarları ' nı genişleterek zeköşeli cihazlara özgü daha fazla ayar özelleştirin veya ekleyin. Zeköşeli cihazlar genellikle fabrika katlarında ve perakende ortamlarda kullanılır. Yüzlerce veya binlerce Zeköşeli cihaza sahipseniz bu cihazları yapılandırmak ve yönetmek için Intune 'u kullanabilirsiniz.

Bu özellik şunları destekler:

- Android cihaz yöneticisi

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

[Microsoft Defender Gelişmiş tehdit koruması (ATP)](../protect/advanced-threat-protection.md) , cihazları izlemek ve korumak için Intune ile tümleşir. Risk düzeylerini ayarlar ve cihazların bu düzeyi aşması durumunda ne olacağını belirleyin. Koşullu erişimle birleştirildiğinde, kuruluşunuzdaki kötü amaçlı etkinlikleri önlemeye yardımcı olabilirsiniz.

Bu özellik şunları destekler:

- Windows 10 ve üzeri

## <a name="oemconfig"></a>OEMConfig

Android kurumsal cihazlarda, [Oemconfig](android-oem-configuration-overview.md) , OEM 'lerin (özgün donanım üreticileri) ve EMMS 'nin (Enterprise Mobility Management), OEM 'e özgü özellikleri standartlaştırılmış bir şekilde oluşturup desteklememesini sağlayan bir standarttır. OEMConfig ile bir OEM, OEM'e özgü yönetim özelliklerini tanımlayan bir şema oluşturur ve bunu Google Play'e yüklenen bir uygulamaya ekler. Intune, uygulamadaki şemayı okur ve Intune yöneticilerinin şemadaki ayarları yapılandırmasına izin verir.

Bu özellik şunları destekler:

- Android Kurumsal (OEMConfig)

## <a name="powershell-scripts"></a>PowerShell komut dosyaları

[PowerShell betikleri](../apps/intune-management-extension.md) Intune 'da PowerShell betiklerinizi karşıya yüklemek Için Intune yönetim uzantısını kullanır ve ardından bu betikleri cihazlarınızda çalıştırır. Ayrıca, uzantıyı kullanmak için gerekenleri, Intune 'a nasıl ekleneceğini ve diğer önemli bilgileri görün.

Bu özellik şunları destekler:

- Windows 10 ve üzeri
- Windows 10 Holographic for Business

## <a name="preference-file"></a>Tercih dosyası

MacOS cihazlarındaki [tercih dosyaları](preference-file-settings-macos.md) , uygulamalar hakkında bilgi içerir. Örneğin, Web tarayıcısı ayarlarını denetlemek, uygulamaları özelleştirmek ve daha fazlasını yapmak için tercih dosyalarını kullanabilirsiniz.

Bu özellik şunları destekler:

- Mac OS

## <a name="shared-multi-user-device"></a>Paylaşılan çok kullanıcılı cihaz

[Windows 10](shared-user-device-settings-windows.md) ve [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md), paylaşılan cihazlar veya paylaşılan bilgisayarlar olarak da bilinen ve birden fazla kişinin kullandığı cihazları yönetmek için kullanabileceğiniz ayarlar sunar. Cihazda oturum açan kullanıcıların uykuya geçme seçeneklerini değiştirme veya cihaza dosya kaydetme konusunda yetki sahibi olup olmayacağını belirleyebilirsiniz. Bir diğer örnekte de yer kazanmak için Windows HoloLens cihazlardaki etkin olmayan kimlik bilgilerini silen bir profil oluşturabilirsiniz.

Bu paylaşılan çok kullanıcılı cihaz ayarları, yöneticilere cihazın bazı özelliklerini denetleme ve bu paylaşılan cihazları Intune kullanarak yönetme imkanı tanır.

Bu özellik şunları destekler:

- Windows 10 ve üzeri
- Windows 10 Holographic for Business

## <a name="update-policies"></a>Güncelleştirme ilkeleri

IOS/ıpados [güncelleştirme ilkeleri](../protect/software-updates-ios.md) , IOS/ıpados cihazlarınıza yazılım güncelleştirmelerini yüklemek için IOS/ıpados ilkeleri oluşturmayı ve atamayı gösterir. Ayrıca yükleme durumunu da gözden geçirebilirsiniz.

Windows cihazlardaki güncelleştirme ilkeleri hakkında bilgi için bkz. [Teslim iyileştirme](delivery-optimization-windows.md). 

Bu özellik şunları destekler:

- iOS/iPadOS

## <a name="vpn"></a>VPN

[VPN ayarları](vpn-settings-configure.md), kuruluşunuzdaki kullanıcılara ve cihazlara VPN profilleri atar, böylece ağa kolayca ve güvenli bir şekilde bağlanabilirler. 

Sanal özel ağlar (VPN’ler), kullanıcılara şirket ağınıza güvenli uzaktan erişim vermenize olanak tanır. Cihazlar VPN sunucunuzla bağlantı başlatmak için VPN bağlantısı profilini kullanır. 

Bu özellik şunları destekler: 

- Android cihaz yöneticisi
- Android Kurumsal
- iOS/iPadOS
- Mac OS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 ve üzeri

## <a name="wi-fi"></a>Wi-Fi

[Wi-Fi ayarları](wi-fi-settings-configure.md), kullanıcılar ve cihazlar için kablosuz ağ ayarları atar. Bir Wi-Fi profili atadığınızda, kullanıcılar kurumsal Wi-Fi ağınıza, ağı kendileri yapılandırmak zorunda kalmadan erişim elde eder. 

Bu özellik şunları destekler:

- Android cihaz yöneticisi
- Android Kurumsal
- iOS/iPadOS
- Mac OS
- Windows 8.1 (yalnızca içeri aktarma)
- Windows 10 ve üzeri

## <a name="wired-networks"></a>Kablolu ağlar

[Kablolu ağlar](wired-networks-configure.md) , MacOS masaüstü bilgisayarları için 802.1 x kablolu bağlantıları oluşturmanıza ve yönetmenize olanak sağlar. Profilinizde, ağ arabirimini seçersiniz, kabul edilen EAP türlerini seçersiniz ve PKCS ve SCEP sertifikaları dahil sunucu güven ayarlarını girersiniz.

Profili atadığınızda macOS masaüstü kullanıcıları, kendisini yapılandırmak zorunda kalmadan şirket kablolu ağınıza erişim sağlar.

Bu özellik şunları destekler:

- Mac OS

## <a name="zebra-mobility-extensions-mx"></a>Zebra Mobility Uzantıları (MX)

[Zebra Mobility Uzantıları (MX)](android-zebra-mx-overview.md), yöneticilerin Zebra cihazları Intune'dan kullanmasını ve yönetmesini sağlar. Ayarlarınızla StageNow profilleri oluşturabilir ve ardından Intune'u kullanarak bu profilleri Zebra cihazlarınıza atayabilir ve dağıtabilirsiniz. [StageNow günlükleri ve yaygın sorunlar](android-zebra-mx-logs-troubleshoot.md) sayfasında profillerle ilgili sorun giderme adımlarını ve StageNow kullanırken karşılaşabileceğiniz potansiyel sorunları inceleyebilirsiniz.

Bu özellik şunları destekler:

- Android Cihaz Yöneticisi (Mobility uzantıları)

## <a name="manage-and-troubleshoot"></a>Yönetme ve sorun giderme

[Profillerinizi yöneterek](device-profile-monitor.md) cihazların ve atanan profillerin durumunu denetleyin. Ayrıca, çakışma yaratan ayarları ve bu ayarları içeren profilleri görerek çakışmaların çözümlenmesine yardımcı olun. [Sık karşılaşılan sorunlar ve çözümleri](device-profile-troubleshoot.md) sayfası, yöneticilere profiller üzerinde çalışma konusunda yardımcı olur. Profil sildiğinizde gerçekleşen işlemleri, cihazlara bildirim gönderilmesine neden olan işlemleri ve daha fazlasını anlatmaktadır.

## <a name="next-steps"></a>Sonraki adımlar

Platformunuzu seçin ve kullanmaya başlayın.
