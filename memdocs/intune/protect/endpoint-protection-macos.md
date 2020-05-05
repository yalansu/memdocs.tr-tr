---
title: Microsoft Intune - Azure’da macOS cihazlara Endpoint Protection ekleme | Microsoft Docs
description: macOS cihazlarda, Mac Apple Store dahil olmak üzere uygulamaların nereye yükleneceğini belirlemek için ağ geçidi denetleyicisini kullanın. Microsoft Intune kullanarak belirli uygulamalara izin vermek, belirli uygulamaları engellemek, gizli mod kullanmak ve hatta bazı gelen bağlantı türlerini engellemek için bir güvenlik duvarı etkinleştirin veya yapılandırın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/29/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 337f7608b4c75a5a2ce2c85774d2090d549ae1fe
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587255"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Intune’da macOS Endpoint Protection ayarları  

Bu makalede, macOS çalıştıran cihazlar için yapılandırabileceğiniz Endpoint Protection ayarları gösterilmektedir. Bu ayarları, Intune 'da [Endpoint Protection](endpoint-protection-configure.md) Için bir MacOS cihaz yapılandırma profili kullanarak yapılandırırsınız.  

## <a name="before-you-begin"></a>Başlamadan önce

[MacOS uç nokta koruma profili oluşturun](endpoint-protection-configure.md).

## <a name="gatekeeper"></a>Ağ Geçidi Denetleyicisi  

- **Bu konumlardan indirilen uygulamalara izin ver**  
  Uygulamaların nereden indirildiğine bağlı olarak, bir cihazın başlatabileceği uygulamaları sınırlayın. Amaç, cihazları kötü amaçlı yazılımlara karşı korumak ve yalnızca güvendiğiniz kaynaklardan gelen uygulamalara izin vermaktır.  

  - **Yapılandırılmadı**  
  - **Mac App Store**  
  - **Mac App Store ve tanımlı geliştiriciler**  
  - **Her yer**  

  **Varsayılan**: yapılandırılmadı  

- **Kullanıcı, ağ geçidi denetleyicisini geçersiz kılabilir**  
  Kullanıcıların, Gatekeeper ayarını geçersiz kılmasını engeller ve kullanıcıların bir uygulama yüklemek için tıklamasını denetlemesini engeller. Etkinleştirildiğinde, kullanıcılar Control tuşuna tıklama ile herhangi bir uygulamayı yükleyebilir.  
 
  - **Yapılandırılmadı** -kullanıcılar, uygulamaları yüklemek için ' yi denetleyebilir.  
  - **Engelle** -kullanıcıların uygulamaları yüklemek için Control-Click kullanmasını engeller.  

  **Varsayılan**: yapılandırılmadı  

## <a name="firewall"></a>Güvenlik duvarı  

Bağlantı noktası yerine uygulama başına bağlantıları denetlemek için güvenlik duvarı kullanın. Uygulama başına ayarlar kullanmak, güvenlik duvarı korumasından faydalanmayı kolaylaştırır. Ayrıca istenmeyen uygulamaların, güvenilen uygulamalara açık olan ağ bağlantı noktalarının kontrolünü ele geçirmelerini önler.  

**Genel**
- **Güvenlik duvarı**  
  Gelen bağlantıların ortamınızda nasıl işleneceğini yapılandırmak için güvenlik duvarını etkinleştirin.  
  - **Yapılandırılmadı**  
  - **Etkinleştir**  

  **Varsayılan**: yapılandırılmadı  

- **Gelen bağlantılar**  
  DHCP, Bonjour ve IPSec gibi temel Internet Hizmetleri için gereken bağlantılar hariç tüm gelen bağlantıları engelleyin. Bu özellik ayrıca, Dosya Paylaşımı ve Ekran Paylaşımı gibi tüm paylaşım hizmetlerini engeller. Paylaşım cihazları kullanıyorsanız bu ayarı *Yapılandırılmadı* olarak bırakın.  
  - **Yapılandırılmadı**  
  - **Engelleyin**  

  **Varsayılan**: yapılandırılmadı  

**Belirli uygulamalar için gelen bağlantılara izin verin veya bunları engelleyin.**  

  - **İzin verilen uygulamalar**  
    Gelen bağlantıları almasına açıkça izin verilen uygulamaları seçin.  

  - **Engellenen uygulamalar**  
    Gelen bağlantıları engellemesi gereken uygulamaları seçin.  

  - **Gizli mod**  
    Bilgisayarın yoklama isteklerine yanıt vermesini engellemek için gizli modu etkinleştirin. Cihaz, yetkilendirilmiş uygulamalardan gelen istekleri yanıtlamaya devam eder. ICMP (ping) gibi beklenmedik istekler yoksayılır.  
    - **Yapılandırılmadı**  
    - **Etkinleştir**  

    **Varsayılan**: yapılandırılmadı  

## <a name="filevault"></a>FileVault  
Apple Filekasası ayarları hakkında daha fazla bilgi için Apple geliştirici içerikleriyle ilgili [Fdefilekasasını](https://developer.apple.com/documentation/devicemanagement/fdefilevault) inceleyin. 

> [!IMPORTANT]  
> MacOS 10,15 itibariyle, Filekasası yapılandırması kullanıcı onaylı MDM kaydı gerektirir. 

- **FileVault**  
  MacOS 10,13 ve üstünü çalıştıran cihazlarda Filekasasıyla XTS-AES 128 kullanarak tam disk şifrelemeyi *etkinleştirebilirsiniz* .  
  - **Yapılandırılmadı**  
  - **Etkinleştir**  

  **Varsayılan**: yapılandırılmadı  

  - **Kurtarma anahtarı türü**  
    Cihazlar için *kişisel anahtar* kurtarma anahtarları oluşturulur. Kişisel anahtar için aşağıdaki ayarları yapılandırın.  

    - **Kişisel kurtarma anahtarının konumu** -kullanıcıya kişisel kurtarma anahtarını nasıl ve nereden alabilecekleri hakkında kısa bir ileti belirtin. Bu metin, bir parola unutursa kişisel kurtarma anahtarını girmeniz istendiğinde kullanıcının oturum açma ekranında gördüğü iletiye eklenir.  

    - **Kişisel kurtarma anahtarı döndürme** -bir cihaz için kişisel kurtarma anahtarının ne sıklıkta döndürüleceğini belirtin. **Yapılandırılmadı**' dan varsayılan değeri veya **1** ile **12** ay arasında bir değer seçebilirsiniz.  

  - **Oturumu kapatmak için istemi devre dışı bırak**  
    Kullanıcıdan oturum açtıklarında dosya kasasını etkinleştirdikleri isteyen kullanıcıya sorma işlemini engelleyin.  Devre dışı olarak ayarlandığında, oturum kapatma istemi devre dışı bırakılır ve bunun yerine kullanıcıya oturum açtıklarında sorulur.  
    - **Yapılandırılmadı**  
    - **Devre dışı bırak** -oturum kapatma sırasında istemi devre dışı bırak.

    **Varsayılan**: yapılandırılmadı  

  - **Atlayakaç kez izin verilir**  
  Kullanıcının oturum açması için dosya kasasından önce dosya kasasını etkinleştirmek üzere bir kullanıcının istekleri yoksaymasına izin sayısını belirleyin. 

    > [!IMPORTANT]
    >
    > Hiçbir limit değeri olmayan bilinen bir sorun vardır **, her zaman sor**. Kullanıcının oturum açtıklarında şifrelemeyi atlamasına olanak tanımak yerine, bu ayar bir sonraki oturum açma sırasında cihaz şifrelemesi gerektirir. Bu sorunun geç Haziran 'da düzeltilmesi ve MC210922 içinde bildirilmesi beklenmektedir.
    >
    > Bu ayar düzeltildiğinde, bir Kullanıcı cihazda bir dahaki sefer oturum açtığında cihazların şifrelenmesini gerektiren yeni bir sıfır (**0**) seçeneği olacaktır. Buna ek olarak, Intune bu çözümü dahil etmek için güncelleştirmeler yaparken, sınırsız olarak ayarlanan herhangi bir ilke, **her zaman sor** , şifreleme gerektirmesinin geçerli davranışını tutan yeni **0**değerini kullanacak şekilde güncelleştirilir.
    >
    > Bu sorun giderildikten sonra, bu ayarı **hiçbir sınır** ayarlamak için yeniden yapılandırarak şifreleme gerektirmeyi atlama özelliğini kullanabilirsiniz, ayarın başlangıçta beklendiği gibi çalışacağını ve kullanıcıların cihazı şifrelemeyi atlamasına izin vermesini sağlayabilirsiniz.
    >
    > Kayıtlı MacOS cihazları varsa, [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açtığınızda daha fazla bilgi görüntüleyebilirsiniz, **Kiracı Yönetimi** > **kiracı durumu**' na gidin, **hizmet durumu ve ileti merkezi**' ni seçip ileti kimliği **MC210922**' ni arayın.

    <br> 

    - **Yapılandırılmadı** -bir sonraki oturum açma işlemine izin verilmesi için cihazda şifreleme gerekir.  
    - **1** ila **10** -bir kullanıcının cihazda şifrelemeyi gerektirmeden önce 1 ila 10 kez istemi yoksaymasına izin verin.  
    - **Sınır yok, her zaman sor** -kullanıcıdan dosya kasasını etkinleştirmesi istenir, ancak şifreleme hiçbir zaman gerekli değildir.  
 
    **Varsayılan**: *değişir* - *oturumu kapatma sırasında devre dışı bırakma istemi* **Yapılandırılmadı**olarak ayarlandığında, bu ayar varsayılan olarak **yapılandırılmaz**. *Oturumu kapatma sırasında Disable* seçeneğini devre **dışı**bırak olarak ayarlarsanız, bu ayar varsayılan olarak **1** ' dir ve **yapılandırılmamış** bir değer bir seçenek değildir.

Intune ile Filekasası hakkında daha fazla bilgi için bkz. [filekasası kurtarma anahtarları](encryption-monitor.md#filevault-recovery-keys).

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](../configuration/device-profile-assign.md) ve [durumunu izleme](../configuration/device-profile-monitor.md).

Ayrıca, [Windows 10 ve daha yeni cihazlarda](endpoint-protection-windows-10.md)Endpoint Protection 'ı yapılandırabilirsiniz.
