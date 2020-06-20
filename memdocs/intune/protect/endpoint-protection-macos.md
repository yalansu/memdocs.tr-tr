---
title: MacOS cihazlarında Endpoint Protection 'ı Microsoft Intune ile yapılandırma | Microsoft Docs
description: MacOS cihazlarını yapılandırmak için Intune 'U kullanarak belirli uygulamalara izin vermek veya bu uygulamaları engellemek veya gizli modu kullanmak için, uygulamaların yüklendiği yeri belirleme ve Filekasası disk şifrelemesi kullanma hakkında daha fazla ağ geçidi kullanmak için yerleşik güvenlik duvarını kullanın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107502"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Intune’da macOS Endpoint Protection ayarları

Bu makalede, macOS çalıştıran cihazlar için yapılandırabileceğiniz Endpoint Protection ayarları gösterilmektedir. Bu ayarları, Intune 'da [Endpoint Protection](endpoint-protection-configure.md) Için bir MacOS cihaz yapılandırma profili kullanarak yapılandırırsınız.

## <a name="before-you-begin"></a>Başlamadan önce

[MacOS uç nokta koruma profili oluşturun](endpoint-protection-configure.md).

## <a name="firewall"></a>Güvenlik Duvarı

Bağlantı noktası yerine uygulama başına bağlantıları denetlemek için güvenlik duvarı kullanın. Uygulama başına ayarlar kullanmak, güvenlik duvarı korumasından faydalanmayı kolaylaştırır. Ayrıca istenmeyen uygulamaların, güvenilen uygulamalara açık olan ağ bağlantı noktalarının kontrolünü ele geçirmelerini önler.

- **Güvenlik duvarını etkinleştir**

  MacOS 'ta güvenlik duvarının kullanımını açın ve sonra gelen bağlantıların ortamınızda nasıl işleneceğini yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**

- **Tüm gelen bağlantıları engelleme**

  DHCP, Bonjour ve IPSec gibi temel Internet Hizmetleri için gereken bağlantılar hariç tüm gelen bağlantıları engelleyin. Bu özellik ayrıca, Dosya Paylaşımı ve Ekran Paylaşımı gibi tüm paylaşım hizmetlerini engeller. Paylaşım cihazları kullanıyorsanız bu ayarı *Yapılandırılmadı* olarak bırakın.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**

  *Yapılandırılmış* *tüm gelen bağlantıları engelle* seçeneğini belirlediğinizde, hangi uygulamaların gelen bağlantıları alabileceğini veya alabileceğini yapılandırabilirsiniz.

  **İzin verilen uygulamalar**: gelen bağlantıları almasına izin verilen uygulamaların bir listesini yapılandırın.

  - **Paket kimliğine göre uygulama ekleme**: UYGULAMANıN [paket kimliğini](../configuration/bundle-ids-built-in-ios-apps.md) girin. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur.
  - **Mağaza uygulaması ekleme**: daha önce Intune 'a eklemiş olduğunuz bir mağaza uygulaması seçin. Daha fazla bilgi için bkz. [Microsoft Intune’a uygulama ekleme](../apps/apps-add.md).

  **Engellenen uygulamalar**: gelen bağlantıları engellenen uygulamaların listesini yapılandırın.

  - **Paket kimliğine göre uygulama ekleme**: UYGULAMANıN [paket kimliğini](../configuration/bundle-ids-built-in-ios-apps.md) girin. Apple 'ın Web sitesinde [yerleşik bir Apple Apps](https://support.apple.com/HT208094)listesi bulunur.
  - **Mağaza uygulaması ekleme**: daha önce Intune 'a eklemiş olduğunuz bir mağaza uygulaması seçin. Daha fazla bilgi için bkz. [Microsoft Intune’a uygulama ekleme](../apps/apps-add.md).

- **Gizli modu etkinleştir**

  Bilgisayarın yoklama isteklerine yanıt vermesini engellemek için gizli modu etkinleştirin. Cihaz, yetkilendirilmiş uygulamalardan gelen istekleri yanıtlamaya devam eder. ICMP (ping) gibi beklenmedik istekler yoksayılır.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**

## <a name="gatekeeper"></a>Ağ Geçidi Denetleyicisi

- **Bu konumlardan indirilen uygulamalara izin ver**

  Uygulamaların nereden indirildiğine bağlı olarak, bir cihazın başlatabileceği uygulamaları sınırlayın. Amaç, cihazları kötü amaçlı yazılımlara karşı korumak ve yalnızca güvendiğiniz kaynaklardan gelen uygulamalara izin vermaktır.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Mac App Store**
  - **Mac App Store ve tanımlı geliştiriciler**
  - **Her yer**

- **Kullanıcının ağ geçidi denetleyicisini geçersiz kılmasına izin verme**

  Kullanıcıların, Gatekeeper ayarını geçersiz kılmasını engeller ve kullanıcıların bir uygulama yüklemek için tıklamasını denetlemesini engeller. Etkinleştirildiğinde, kullanıcılar Control tuşuna tıklama ile herhangi bir uygulamayı yükleyebilir.

  - **Yapılandırılmadı** (*varsayılan*)-kullanıcılar, uygulamaları yüklemek için ' i denetleyebilir.
  - **Evet** -kullanıcıların uygulamayı yüklemek için Control-Click kullanmasını engeller.

## <a name="filevault"></a>FileVault

Apple Filekasası ayarları hakkında daha fazla bilgi için Apple geliştirici içerikleriyle ilgili [Fdefilekasasını](https://developer.apple.com/documentation/devicemanagement/fdefilevault) inceleyin.

> [!IMPORTANT]
> MacOS 10,15 itibariyle, Filekasası yapılandırması kullanıcı onaylı MDM kaydı gerektirir.

- **Dosya kasasını etkinleştir**  

  MacOS 10,13 ve üstünü çalıştıran cihazlarda Filekasasıyla XTS-AES 128 kullanarak tam disk şifrelemeyi *etkinleştirebilirsiniz* .

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**

  *Dosya kasasını etkinleştir* *Evet*olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:

  - **Kurtarma anahtarı türü**

    Cihazlar için *kişisel anahtar* kurtarma anahtarları oluşturulur. Kişisel anahtar için aşağıdaki ayarları yapılandırın.

  - **Emanet kişisel kurtarma anahtarının konum açıklaması**

    Kullanıcıya kişisel kurtarma anahtarını nasıl ve nereden alabilecekleri hakkında kısa bir ileti belirtin. Bu metin, bir parola unutursa kişisel kurtarma anahtarını girmeniz istendiğinde kullanıcının oturum açma ekranında gördüğü iletiye eklenir.

  - **Kişisel kurtarma anahtarı döndürme**

    Bir cihaz için kişisel kurtarma anahtarının ne sıklıkta döndürüleceğini belirtin. **Yapılandırılmadı**' dan varsayılan değeri veya **1** ile **12** ay arasında bir değer seçebilirsiniz.

  - **Kurtarma anahtarını gizle**

    Dosya Kasası 2 şifrelemesi sırasında bir cihaz kullanıcısının kişisel anahtarını gizlemeyi seçin.

    - **Yapılandırılmadı** (*varsayılan*) – kişisel anahtar, şifreleme sırasında cihaz kullanıcısı tarafından görülebilir.
    - **Evet** -kişisel anahtar, şifreleme sırasında cihaz kullanıcıdan gizlenir.

    Şifreleme sonrasında, cihaz kullanıcıları şifrelenmiş macOS cihazının kişisel kurtarma anahtarlarını aşağıdaki konumlardan görüntüleyebilir:
    - iOS/ıpados Şirket portalı uygulaması
    - Intune uygulaması
    - Şirket portalı Web sitesi
    - Android şirket portalı uygulaması

    Anahtarı görüntülemek için, uygulama veya Web sitesinden şifrelenmiş macOS cihazının cihaz ayrıntıları ' na gidin ve *Kurtarma anahtarı al*' ı seçin.

  - **Oturumu kapatmak için istemi devre dışı bırak**

    Kullanıcıdan oturum açtıklarında dosya kasasını etkinleştirdikleri isteyen kullanıcıya sorma işlemini engelleyin.  Devre dışı olarak ayarlandığında, oturum kapatma istemi devre dışı bırakılır ve bunun yerine kullanıcıya oturum açtıklarında sorulur.

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -oturum kapatma sırasında istemi devre dışı bırakın.

  - **Atlayakaç kez izin verilir**

    Kullanıcının oturum açması için dosya kasasından önce dosya kasasını etkinleştirmek üzere bir kullanıcının istekleri yoksaymasına izin sayısını belirleyin.

    - **Yapılandırılmadı** -bir sonraki oturum açma işlemine izin verilmesi için cihazda şifreleme gerekir.
    - **0** -Kullanıcı cihazda bir dahaki sefer oturum açtığında cihazların şifrelenmesini gerektir.
    - **1** ila **10** -bir kullanıcının cihazda şifrelemeyi gerektirmeden önce 1 ila 10 kez istemi yoksaymasına izin verin.
    - **Sınır yok, her zaman sor** -kullanıcıdan dosya kasasını etkinleştirmesi istenir, ancak şifreleme hiçbir zaman gerekli değildir.

    Bu ayar için varsayılan değer, *oturum kapatma sırasında devre dışı bırakma isteminin*yapılandırmasına bağlıdır. *Oturumu kapatma sırasında Istemi devre dışı bırak* ayarı **Yapılandırılmadı**olarak ayarlandığında, bu ayar varsayılan olarak **yapılandırılmaz**. *Oturumu kapatma sırasında devre dışı bırak* **Evet**olarak ayarlanırsa, bu ayar varsayılan olarak **1** ' dir ve **yapılandırılmamış** bir değer bir seçenek değildir.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](../configuration/device-profile-assign.md) ve [durumunu izleme](../configuration/device-profile-monitor.md).

Ayrıca, [Windows 10 ve daha yeni cihazlarda](endpoint-protection-windows-10.md)Endpoint Protection 'ı yapılandırabilirsiniz.
