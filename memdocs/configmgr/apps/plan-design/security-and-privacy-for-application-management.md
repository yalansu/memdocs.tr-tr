---
title: Uygulamalar için güvenlik ve Gizlilik
titleSuffix: Configuration Manager
description: Configuration Manager uygulamalar yönetirken güvenlik ve gizlilik için rehberlik ve öneriler.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e3ceb036180d002956eb0f62348ad317dfce6e7e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695146"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Configuration Manager 'de uygulama yönetimi için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

## <a name="security-guidance-for-application-management"></a>Uygulama yönetimi için Güvenlik Kılavuzu  

### <a name="use-the-software-center-without-the-application-catalog"></a>Uygulama Kataloğu olmadan yazılım merkezini kullanma

<!--1358309-->

Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Bu yapılandırma, kullanıcılara uygulama sunmak için gereken sunucu altyapısını azaltmanıza yardımcı olur.

Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Sunucu altyapısını düşürmek saldırı yüzeyini de azaltır.

Internet tabanlı istemciler için tutarlı ve güvenli bir uygulama deneyimi sunmak üzere Azure Active Directory ve bulut yönetimi ağ geçidini kullanın.

Daha fazla bilgi için bkz. [Software Center 'ı yapılandırma](plan-for-software-center.md#bkmk_userex).

### <a name="use-https-with-the-application-catalog"></a>Uygulama Kataloğu ile HTTPS kullanma

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Uygulama Kataloğu web sitesi noktasını ve Uygulama Kataloğu Web hizmeti noktasını HTTPS bağlantılarını kabul edecek şekilde yapılandırın. Bu yapılandırmayla, sunucunun kimlik doğrulaması kullanıcılara verilir. Aktarılan veriler izinsiz ve görüntüleme işleminden korunur.

Kullanıcıları yalnızca güvenilen Web sitelerine bağlanmak üzere eğiterek sosyal mühendislik saldırılarını önlemeye yardımcı olun. Kullanıcıları kötü amaçlı Web sitelerinin tehlikeleri konusunda eğitin.

HTTPS kullanmıyorsanız, marka yapılandırma seçeneklerini kullanmayın. Bu ayarlar, kimlik kanıtı olarak uygulama kataloğu 'nda kuruluşunuzun adını gösterir.  


### <a name="use-role-separation"></a>Rol ayrımı kullan

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Uygulama Kataloğu web sitesi noktasını ve Uygulama Kataloğu Web hizmet noktasını ayrı sunuculara yükler. Web sitesi noktası tehlikedeyse, Web hizmeti noktasından ayrıdır. Bu tasarım, Configuration Manager istemcilerini ve altyapısını korumanıza yardımcı olur. Bu yapılandırma, Web sitesi noktası Internet 'ten istemci bağlantılarını kabul ediyorsa özellikle önemlidir. Sunucuyu saldırılara karşı daha savunmasız hale getirir.  

### <a name="close-browser-windows"></a>Tarayıcı pencerelerini kapat

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Kullanıcıları, uygulama kataloğu 'nu kullanmayı bitirdiklerinde tarayıcı penceresini kapatacak şekilde eğitin. Kullanıcılar, uygulama kataloğu için kullandıkları tarayıcı penceresinde bir dış Web sitesine gözatlarsa, tarayıcı intranetteki güvenilen siteler için uygun olan güvenlik ayarlarını kullanmaya devam eder.  

### <a name="centrally-specify-user-device-affinity"></a>Kullanıcı cihaz benzeşimini merkezi olarak belirtme

Kullanıcıların birincil cihazlarını tanımlamasına izin vermek yerine Kullanıcı aygıtı benzeşimini el ile belirtin. Kullanım tabanlı yapılandırmayı etkinleştirmeyin.

Kullanıcılardan veya cihazdan toplanan bilgileri yetkili olacak şekilde değerlendirin. Güvenilir bir yöneticinin belirtmediği Kullanıcı cihaz benzeşimini kullanarak yazılım dağıtırsanız, yazılım, bu yazılımı alma yetkisi olmayan bilgisayarlara ve kullanıcılara yüklenebilir.  

### <a name="dont-run-deployments-from-distribution-points"></a>Dağıtım noktalarından dağıtımları çalıştırma

Dağıtımları daima dağıtım noktalarından çalışmak yerine dağıtım noktalarından içerik indirecek şekilde yapılandırın. Dağıtımları bir dağıtım noktasından içerik indirip yerel olarak çalışacak şekilde yapılandırdığınızda, Configuration Manager istemci, içeriği indirdikten sonra paket karmasını doğrular. Karma, ilkedeki karmayla eşleşmiyorsa, istemci paketi atar.

Dağıtımı doğrudan bir dağıtım noktasından çalışacak şekilde yapılandırırsanız, Configuration Manager istemcisi paket karmasını doğrulamaz. Bu davranış, Configuration Manager istemcisinin ile oynanmış yazılımları yükleyebileceği anlamına gelir.

Dağıtımları doğrudan dağıtım noktalarından çalıştırmanız gerekiyorsa, dağıtım noktalarındaki paketlerde en az NTFS izinlerini kullanın. Ayrıca, istemci ve dağıtım noktaları arasında ve dağıtım noktaları ile site sunucusu arasındaki kanalı korumak için Internet Protokolü güvenliği (IPSec) kullanın.

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a> Kullanıcıların yükseltilmiş işlemlerle etkileşime girmesine izin verme
  
Ayarları **yönetici haklarıyla çalıştırma** veya **sistem için yüklemeyi**etkinleştirirseniz, kullanıcıların bu uygulamalarla etkileşime girmesine izin verin. Bir uygulamayı yapılandırdığınızda, **kullanıcıların program yüklemesini görüntülemesine ve etkileşime girmesine Izin ver**seçeneğini belirleyebilirsiniz. Bu ayar, kullanıcıların kullanıcı arabirimindeki gerekli istemlere yanıt vermesini sağlar. Uygulamayı **yönetici haklarıyla çalışacak**şekilde yapılandırırsanız veya **sistem için**sürüm 1802 ' den başlayarak, programı çalıştıran bilgisayardaki bir saldırgan, istemci bilgisayardaki ayrıcalıkların iletmek için Kullanıcı arabirimini kullanabilir.

Kurulum için Windows Installer kullanan programları ve yönetim kimlik bilgileri gerektiren yazılım dağıtımları için Kullanıcı başına yükseltilmiş ayrıcalıkları kullanın. Kurulumun, yönetici kimlik bilgilerine sahip olmayan bir kullanıcı bağlamında çalıştırılması gerekir. Windows Installer Kullanıcı başına yükseltilmiş ayrıcalıklar, bu gereksinime sahip uygulamaları dağıtmak için en güvenli yolu sağlar.

### <a name="restrict-whether-users-can-install-software-interactively"></a>Kullanıcıların yazılımları etkileşimli olarak yükleyip yükleyemeyeceklerini kısıtlama

**Bilgisayar Aracısı** grubundaki **izinleri yükler** istemci ayarını yapılandırın. Bu ayar, yazılım merkezi 'nde yazılım yükleyebilen Kullanıcı türlerini kısıtlar.

Örneğin, **İzinleri yükle** 'yi **Yalnızca yöneticiler**olarak ayarlayarak özel bir istemci ayarı oluşturun. Bu istemci ayarını bir sunucu koleksiyonuna uygulayın. Bu yapılandırma, yönetim izinlerine sahip olmayan kullanıcıların bu sunuculara yazılım yüklemesini engeller.  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Mobil cihazlar söz konusu olduğunda, yalnızca imzalı uygulamaları dağıtın

Mobil cihaz uygulamalarını yalnızca, mobil cihazın güvendiği bir sertifika yetkilisi (CA) tarafından kod İmzalandıklarında dağıtın.

Örnek:

- Bir satıcıdan gelen ve VeriSign gibi iyi bilinen bir CA tarafından imzalanan bir uygulama.  

- İç sertifika yetkilinizi kullanarak Configuration Manager bağımsız olarak oturum açmanızı sağlayan dahili bir uygulamadır.  

- Uygulama türünü oluştururken ve imza sertifikası kullandığınızda Configuration Manager kullanarak imzalamanız gereken dahili bir uygulamadır.

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Mobil cihaz uygulama imzalama sertifikası konumunun güvenliğini sağlama

Mobil cihaz uygulamalarını, Configuration Manager **Uygulama Oluştur sihirbazını** kullanarak imzalayıp imza sertifikası dosyasının konumunu güvenli hale getirin ve iletişim kanalının güvenliğini sağlayın. Ayrıcalıkların yükseltilmesinin ve ortadaki adam saldırılarına karşı korunmaya yardımcı olmak için, imza sertifikası dosyasını güvenli bir klasörde saklayın.

Aşağıdaki bilgisayarlar arasında IPSec kullanın:

- Configuration Manager konsolunu çalıştıran bilgisayar
- Sertifika imzalama dosyasını depolayan bilgisayar
- Uygulama kaynak dosyalarını depolayan bilgisayar

Alternatif olarak, uygulama **oluşturma Sihirbazı 'nı**çalıştırmadan önce uygulamayı Configuration Manager bağımsız olarak imzalayın.

### <a name="implement-access-controls"></a>Erişim denetimleri uygulama

Başvuru bilgisayarlarını korumak için erişim denetimleri uygulayın. Bir dağıtım türündeki algılama yöntemini bir başvuru bilgisayarına giderek yapılandırdığınızda, bilgisayarın güvenliğinin aşılmadığı durumda olduğundan emin olun.

### <a name="restrict-and-monitor-administrative-users"></a>Yönetici kullanıcılarını kısıtlama ve izleme

Aşağıdaki uygulama yönetimi rol tabanlı güvenlik rollerine verdiğiniz yönetim kullanıcılarını kısıtlayın ve izleyin:

- **Uygulama Yöneticisi**
- **Uygulama Yazarı**
- **Uygulama Dağıtım Yöneticisi**

Rol tabanlı yönetimi yapılandırırken bile, uygulamaları oluşturup dağıtan yönetim kullanıcıları sizin fark ettiğinizden çok daha fazla izne sahip olabilir. Örneğin, bir uygulamayı oluşturan veya değiştiren yönetici kullanıcılar, kendi güvenlik kapsamlarında olmayan bağımlı uygulamaları seçebilir.

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Aynı güven düzeyine sahip sanal ortamlarda App-V uygulamalarını yapılandırma

Microsoft Application Virtualization (App-V) sanal ortamlarını yapılandırırken, sanal ortamda aynı güven düzeyine sahip olan uygulamalar ' ı seçin. App-V sanal ortamındaki uygulamalar kaynakları paylaşabileceğinden, pano gibi, sanal ortamı seçili uygulamaların aynı güven düzeyine sahip olacak şekilde yapılandırın.

Daha fazla bilgi için bkz. [App-V sanal ortamları oluşturma](../deploy-use/create-app-v-virtual-environments.md).

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>MacOS uygulamalarının güvenilir bir kaynaktan geldiğinden emin olun

MacOS cihazları için uygulama dağıtırsanız, kaynak dosyaların güvenilir bir kaynaktan geldiğinden emin olun. CMAppUtil aracı kaynak paketin imzasını doğrulamaz. Paketin güvendiğiniz bir kaynaktan geldiğinden emin olun. CMAppUtil Aracı, dosyaların değiştirilip değiştirilmediğini algılayamaz.

### <a name="secure-the-cmmac-file-for-macos-apps"></a>MacOS uygulamaları için cmmac dosyasının güvenliğini sağlama

MacOS bilgisayarları için uygulamalar dağıtırsanız, **. cmmac** dosyasının konumunun güvenliğini sağlayın. CMAppUtil aracı bu dosyayı oluşturur ve sonra Configuration Manager içeri aktarırsınız. Bu dosya imzalı değil veya doğrulanmadı.

Bu dosyayı Configuration Manager 'e aktardığınızda iletişim kanalının güvenliğini sağlayın. Bu dosya üzerinde değişiklik yapılmasını önlemeye yardımcı olmak için güvenli bir klasörde saklayın. Aşağıdaki bilgisayarlar arasında IPSec kullanın:

- Configuration Manager konsolunu çalıştıran bilgisayar  
- **. Cmmac** dosyasını depolayan bilgisayar  

### <a name="use-https-for-web-applications"></a>Web uygulamaları için HTTPS Kullan

Bir Web uygulaması dağıtım türü yapılandırırsanız, bağlantıyı güvenli hale getirmek için HTTPS kullanın. Bir Web uygulamasını HTTPS bağlantısı yerine HTTP bağlantısı kullanarak dağıtırsanız, cihaz standart dışı bir sunucuya yeniden yönlendirilebilir. Cihaz ve sunucu arasında aktarılan veriler ile oynanmış olabilir.


## <a name="security-issues-for-application-management"></a>Uygulama yönetimiyle ilgili güvenlik sorunları  

- Düşük haklara sahip olan kullanıcılar, istemci bilgisayarındaki istemci önbelleğinden dosya kopyalayabilirler.  

     Kullanıcılar istemci önbelleğini okuyabilir, ancak yazamaz. Okuma izinleri olan bir kullanıcı, uygulama yükleme dosyalarını bir bilgisayardan başka bir bilgisayara kopyalayabilir.  

- Düşük haklara sahip kullanıcılar, istemci bilgisayarında yazılım dağıtımı geçmişini kaydeden dosyaları değiştirebilir.  

     Uygulama geçmişi bilgileri korunmadığından, bir Kullanıcı, bir uygulamanın yüklenip yüklenmediğini rapor eden dosyaları değiştirebilir.  

- App-V paketleri imzalanmadı.  

     Configuration Manager ' deki App-V paketleri imzalamayı desteklemez. Dijital imzalar içeriğin güvenilir bir kaynaktan olduğunu ve aktarım sırasında değiştirilmediğini doğrular. Bu güvenlik sorunu için risk azaltma yoktur. İçeriği güvenilir bir kaynaktan ve güvenli bir konumdan indirmek için en iyi güvenlik uygulamasını izleyin.  

- Yayımlanan App-V uygulamaları bilgisayardaki tüm kullanıcılar tarafından yüklenebilir.  

     Bir App-V uygulaması bir bilgisayarda yayımlandığında, o bilgisayarda oturum açan tüm kullanıcılar uygulamayı yükleyebilir. Yayımlandıktan sonra uygulamayı yükleyebilen kullanıcıları kısıtlayamazsınız.  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a> Microsoft Silverlight 5 sertifikaları ve uygulama kataloğu için gerekli yükseltilmiş güven modu  

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Configuration Manager istemcileri sürüm 1710 ve önceki sürümleri, kullanıcıların uygulama kataloğu 'ndan yazılım yükleyebilmesi için yükseltilmiş güven modunda çalıştırılması gereken Microsoft Silverlight 5 gerektirir. Varsayılan olarak, Silverlight uygulamaları, uygulamaların kullanıcı verilerine erişmesini engelleyen kısmi güven modunda çalışır. Zaten yüklenmemişse Configuration Manager, Microsoft Silverlight 5 ' i istemcilere otomatik olarak yüklenir. Varsayılan olarak, Configuration Manager bilgisayar Aracısı, **Silverlight uygulamalarının yükseltilmiş güven modu istemci ayarında çalışmasına Izin ver** ' i **Evet**olarak ayarlar. Bu ayar, imzalı ve güvenilen Silverlight uygulamalarının yükseltilmiş güven modunu istemesine olanak tanır.  

Uygulama Kataloğu web sitesi noktası site sistemi rolünü yüklediğinizde, istemci, her bir Configuration Manager istemci bilgisayarındaki güvenilen yayımcılar bilgisayar sertifikası deposuna bir Microsoft imza sertifikası da yükler. Bu sertifika tarafından imzalanan Silverlight uygulamaları, kullanıcıların uygulama kataloğu 'ndan yazılım yüklemesi için gereken yükseltilmiş güven modunda çalışır. Configuration Manager, bu imza sertifikasını otomatik olarak yönetir. Hizmet devamlılığını artırmak için, bu Microsoft imza sertifikasını el ile silmeyin veya taşımayın.  

> [!WARNING]  
> Etkinleştirildiğinde, **Silverlight uygulamalarının yükseltilmiş güven modunda çalışmasına Izin ver** istemci ayarı, bilgisayar deposunda veya kullanıcı deposunda bulunan Güvenilen Yayımcılar sertifika deposundaki sertifikalar tarafından Imzalanan tüm Silverlight uygulamalarının yükseltilmiş güven modunda çalışmasına izin verir. İstemci ayarı, Configuration Manager uygulama kataloğu veya bilgisayar deposundaki güvenilen yayımcılar sertifika deposu için özel olarak yükseltilmiş güven modunu etkinleştiremez. Kötü amaçlı yazılım Güvenilen Yayımcılar deposuna bir standart dışı sertifika eklerse, kendi Silverlight uygulamasını kullanan kötü amaçlı yazılım artık yükseltilmiş güven modunda da çalışabilir.  

**Silverlight uygulamalarının yükseltilmiş güven modunda çalışmasına Izin ver** ayarını **Hayır**olarak ayarlarsanız, istemciler Microsoft imzalama sertifikasını kaldırmaz.  

Silverlight 'taki güvenilen uygulamalar hakkında daha fazla bilgi için bkz. [Güvenilen uygulamalar](/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\)).  


## <a name="privacy-information-for-application-management"></a> Uygulama yönetimi için gizlilik bilgileri  

Uygulama yönetimi, hiyerarşideki herhangi bir istemcide herhangi bir uygulamayı, programı veya betiği çalıştırmanızı sağlar. Configuration Manager çalıştırdığınız uygulama, program veya komut dosyası ya da iletdikleri bilgi türü üzerinde denetim yoktur. Uygulama dağıtım işlemi sırasında, Configuration Manager istemci ve sunucular arasındaki cihaz ve oturum açma hesaplarını tanımlayan bilgileri iletebilir.  

Configuration Manager, yazılım dağıtım işlemiyle ilgili durum bilgilerini tutar. İstemci HTTPS kullanarak iletişim kurmadığı takdirde, yazılım dağıtımı durum bilgileri aktarım sırasında şifrelenmez. Durum bilgileri veritabanında şifreli biçimde depolanmaz.  

Uygulamaları uzaktan, etkileşimli olarak veya sessizce yüklemek için Configuration Manager uygulama yüklemesinin kullanımı, bu yazılımın yazılım lisans koşullarına tabi olabilir. Bu Kullanım Configuration Manager yazılım lisans koşullarından ayrıdır. Configuration Manager kullanarak yazılım dağıtmadan önce yazılım lisans koşulları 'nı her zaman gözden geçirin ve kabul edin.  

Configuration Manager, Microsoft tarafından gelecek sürümleri geliştirmek üzere kullanılan uygulamalar hakkında tanılama ve kullanım verileri toplar. Daha fazla bilgi için bkz. [Tanılama ve kullanım verileri](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

Uygulama dağıtımı varsayılan olarak gerçekleşmez ve birkaç yapılandırma adımı gerektirir.  

Aşağıdaki özellikler verimli yazılım dağıtımına yardımcı olur:

- **Kullanıcı cihaz benzeşimi** , bir kullanıcıyı cihazlara eşler. Configuration Manager yöneticisi bir kullanıcıya yazılım dağıtır. İstemci yazılımı, kullanıcının en sık kullandığı bir veya daha fazla bilgisayara otomatik olarak yüklenir.  

- **Yazılım Merkezi** , Configuration Manager istemcisini yüklediğinizde bir cihaza otomatik olarak yüklenir. Kullanıcılar ayarları değiştirir, yazılım merkezi 'nden yazılım için tarama ve yüklemeyi yükler.  

- **Uygulama Kataloğu** , kullanıcıların yazılım yüklemesine izin veren bir Web sitesidir.  

    > [!Important]  
    > Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a> Kullanıcı cihaz benzeşimi gizlilik bilgileri

- Configuration Manager istemcilerle yönetim noktası site sistemleri arasında bilgi aktarabilir. Bilgiler bilgisayar ve oturum açma hesabı ile oturum açma hesaplarının özetlenen kullanımını tanımlayabilir.  

- Yönetim noktası istemcilerin HTTPS kullanarak iletişim kurmasını gerektirecek şekilde yapılandırılmadığı müddetçe, istemci ve sunucu arasında aktarılan bilgiler şifrelenmez.  

- Bir kullanıcıyı bir cihazla eşlemek için kullanılan bilgisayar ve oturum açma hesabı kullanım bilgileri, istemci bilgisayarlarda depolanır, yönetim noktalarına gönderilir ve sonra Configuration Manager veritabanında depolanır. Eski bilgiler veritabanından varsayılan olarak 90 gün sonra silinir. Silme davranışı, **Eski Kullanıcı Aygıtı Benzeşimi Verilerini Sil** site bakım görevi ayarlanarak yapılandırılabilir.  

- Configuration Manager, Kullanıcı cihaz benzeşimi ile ilgili durum bilgilerini tutar. İstemciler, HTTPS kullanarak yönetim noktalarıyla iletişim kuracak şekilde yapılandırılmadığı müddetçe, iletim sırasında durum bilgileri şifrelenmez. Durum bilgileri veritabanında şifreli biçimde depolanmaz.  

- Kullanıcı ve cihaz benzeşimi oluşturmak için kullanılan bilgisayar ve oturum açma kullanım bilgileri her zaman etkindir. Kullanıcılar ve yönetici kullanıcılar, Kullanıcı aygıt benzeşimi bilgilerini sağlayabilir.  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a> Yazılım Merkezi gizlilik bilgileri

- Software Center, Configuration Manager yöneticisinin kullanıcıların çalıştırması için herhangi bir uygulama veya program veya betiği yayımlamasına olanak sağlar. Configuration Manager katalogda yayınlanan program veya komut dosyası türleri veya iletilerdeki bilgi türü üzerinde denetim yoktur.  

- Configuration Manager istemciler ve yönetim noktası arasında bilgi aktarabilir. Bilgiler bilgisayar ve oturum açma hesaplarını tanımlayabilir. Yönetim noktasını istemcilerin HTTPS kullanarak bağlanmasını gerektirecek şekilde yapılandırmadığınız müddetçe, istemci ve sunucular arasında aktarılan bilgiler şifrelenmez.  

- Uygulama onay isteğiyle ilgili bilgiler Configuration Manager veritabanında depolanır. İptal edilen veya reddedilen istekler ve karşılık gelen istek geçmişi girdileri 30 gün sonra varsayılan olarak silinir. Silme davranışı, **Eski Uygulama İsteği Verilerini Sil** site bakım görevi ayarlanarak yapılandırılabilir. Onaylanan ve bekleyen durumundaki uygulama onay istekleri hiçbir şekilde silinmez.  

- Yazılım Merkezi, Configuration Manager istemcisini bir cihaza yüklediğinizde otomatik olarak yüklenir.  

### <a name="application-catalog-privacy-information"></a>Uygulama Kataloğu gizlilik bilgileri

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- Uygulama Kataloğu varsayılan olarak yüklü değildir. Bu yükleme birkaç yapılandırma adımını gerektirir.  

- Uygulama Kataloğu, Configuration Manager yöneticisinin kullanıcıların çalıştırması için herhangi bir uygulama veya program veya betiği yayımlamasına olanak sağlar. Configuration Manager katalogda yayınlanan program veya komut dosyası türleri veya iletilerdeki bilgi türü üzerinde denetim yoktur.  

- Configuration Manager istemcilerle Uygulama Kataloğu site sistem rolleri arasında bilgi aktarabilir. Bilgiler bilgisayar ve oturum açma hesaplarını tanımlayabilir. İstemci ve sunucular arasında aktarılan bilgiler, bu site sistem rolleri istemcilerin HTTPS kullanarak bağlanmasını gerektirecek şekilde yapılandırılmadığı takdirde şifrelenmez.