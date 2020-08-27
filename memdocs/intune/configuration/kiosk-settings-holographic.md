---
title: Microsoft Intune-Azure 'da Windows holographic for Business için bilgi noktası ayarları | Microsoft Docs
description: Windows holographic for Business cihazlarınızı tek uygulama ve çok kullanıcılı kiler olarak yapılandırın, Başlat menüsünü özelleştirin, uygulamalar ekleyin, görev çubuğunu görüntüleyin ve Microsoft Intune bir Web tarayıcısı yapılandırın.
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
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8127281069ce4209adfc2aec82a93f5a60669307
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911872"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Intune 'da bilgi noktası olarak çalışacak Windows holographic for Business cihaz ayarları

Windows Holographic for Business cihazlarında, bu cihazları tekli uygulama bilgi noktası modunda veya çoklu uygulama bilgi noktası modunda çalıştırılacak şekilde yapılandırabilirsiniz. Bazı özellikler, Windows Holographic for Business’ta desteklenmez.

Bu makalede, Windows holographic for Business cihazlarında denetleyebilmeniz için farklı ayarlar listelenmektedir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, Windows holographic for Business cihazlarınızı bilgi noktası modunda çalışacak şekilde yapılandırmak için bu ayarları kullanın.

Bir Intune Yöneticisi olarak bu ayarları oluşturabilir ve cihazlarınıza atayabilirsiniz.

Intune 'da Windows bilgi noktası özelliği hakkında daha fazla bilgi edinmek için bkz. [bilgi noktası ayarlarını yapılandırma](kiosk-settings.md).

## <a name="before-you-begin"></a>Başlamadan önce

- [Windows 10 bilgi noktası cihaz yapılandırma profili oluşturun](kiosk-settings.md#create-the-profile).

  Bir Windows 10 bilgi noktası cihaz yapılandırma profili oluşturduğunuzda, bu makalede listelenenlerden daha fazla ayar vardır. Bu makaledeki ayarlar Windows holographic for Business cihazlarında desteklenir.

- Bu bilgi noktası profili, [Microsoft Edge bilgi noktası ayarları](device-restrictions-windows-holographic.md#microsoft-edge-browser)kullanılarak oluşturduğunuz cihaz kısıtlamaları profiliyle doğrudan ilgilidir. Özetlemek gerekirse:

  1. Bu bilgi noktası profilini, cihazı bilgi noktası modunda çalıştırmak için oluşturun.
  2. [Cihaz kısıtlamaları profilini](device-restrictions-windows-holographic.md#microsoft-edge-browser)oluşturun ve Microsoft Edge 'de izin verilen belirli özellikleri ve ayarları yapılandırın.

> [!IMPORTANT]
> Bu bilgi noktası profilini [Microsoft Edge profilinizle](device-restrictions-windows-holographic.md#microsoft-edge-browser)aynı cihazlara atadığınızdan emin olun.

## <a name="single-app-full-screen-kiosk"></a>Tek uygulama, tam ekran bilgi noktası

Cihazda yalnızca bir uygulama çalıştırır. Kullanıcı oturum açtığında belirli bir uygulama başlar. Bu mod ayrıca kullanıcının yeni uygulamalar açmasını veya çalışan uygulamayı değiştirmesini önler.

- **Kullanıcı oturum açma türü**: uygulamayı çalıştıran hesap türünü seçin. Seçenekleriniz şunlardır:

  - **Otomatik oturum açma (Windows 10 sürüm 1803 ve üzeri)**: Windows holographic for Business 'te desteklenmez.
  - **Yerel kullanıcı hesabı**: Cihaz için yerel kullanıcı hesabını girin. Ya da bilgi noktası uygulamasıyla ilişkili bir Microsoft hesabı (MSA) hesabı girin. Girdiğiniz hesap, bilgi noktasında oturum açar.

    Herkese açık ortamlardaki bilgi noktaları için en az ayrıcalığa sahip bir kullanıcı türü kullanılmalıdır.

- **Uygulama türü**: **Mağaza uygulaması Ekle**' yi seçin.

  - **Bilgi noktası modunda çalıştırılacak uygulama**: listeden bir uygulama seçin.

    Listede hiç uygulama yok mu? [İstemci Uygulamaları](../apps/apps-add.md)’ndaki adımları kullanarak birkaç uygulama ekleyin.

## <a name="multi-app-kiosk"></a>Çoklu uygulama bilgi noktası

Bu modda uygulamalar Başlat menüsünde sağlanır. Bu uygulamalar, yalnızca kullanıcıların açabildiği uygulamalardır. Bir uygulamanın başka bir uygulamaya bağımlılığı varsa, her ikisi de izin verilen uygulamalar listesine eklenmelidir.

- **S modundaki cihazlarda Windows 10 ' u hedefleyin**: **Hayır**' ı seçin. S modu, Windows holographic for Business üzerinde desteklenmez.

- **Kullanıcı oturum açma türü**: Eklediğiniz uygulamaları kullanabilecek bir veya birden çok kullanıcı hesabı belirtin. Seçenekleriniz şunlardır:

  - **Otomatik oturum açma (Windows 10 sürüm 1803 ve üzeri)**: Windows holographic for Business 'te desteklenmez.
  - **Yerel kullanıcı hesapları**: Cihaz için yerel kullanıcı hesabını **ekleyin**. Girdiğiniz hesap, bilgi noktasında oturum açar.
  - **Azure Active Directory kullanıcı veya grubu (Windows 10, sürüm 1803 ve sonrası)**: Cihazda oturum açmak için kullanıcı kimlik bilgilerini gerektirir. Listeden Azure Active Directory kullanıcılarını veya gruplarını seçmek için **Ekle**’yi seçin. Birden çok kullanıcı ve grup seçebilirsiniz. Değişikliklerinizi kaydetmek için **Seçin**’e tıklayın.
  - **HoloLens ziyaretçisi**: Ziyaretçi hesabı, [paylaşılan PC modu kavramlarında](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts) anlatıldığı gibi, kullanıcı kimlik bilgileri veya kimlik doğrulaması gerektirmeyen bir konuk hesabıdır.

- **Tarayıcı ve uygulamalar**: bilgi noktası cihazında çalıştırılacak uygulamaları ekleyin. Birden fazla uygulama ekleyebileceğinizi unutmayın.

  - **Browsers (Tarayıcılar)**
    - **Microsoft Edge Ekle**: Microsoft Edge uygulama kılavuzuna eklenir ve tüm uygulamalar bu bilgi noktasında çalıştırılabilir. Microsoft Edge bilgi noktası modu türünü seçin:

      - **Normal mod (Microsoft Edge 'in tam sürümü)**: tüm göz atma özellikleriyle Microsoft Edge 'in tam bir sürümünü çalıştırır. Kullanıcı verileri ve durumu oturumlar arasında kaydedilir.
      - **Genel göz atma (InPrivate)**: tam ekran modunda çalışan bilgi noktaları için özel bir deneyim ile Microsoft Edge InPrivate 'ın çok bölgeli bir sürümünü çalıştırır.

      Bu seçenekler hakkında daha fazla bilgi için bkz. [Microsoft Edge bilgi noktası modunu dağıtma](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Bu ayar cihazda Microsoft Edge tarayıcısını sunar. Microsoft Edge 'e özgü ayarları yapılandırmak için bir cihaz kısıtlamaları profili oluşturun (**cihazlar**  >  **yapılandırma profilleri**  >  **Create profile**  >  **Windows 10** for platform > **cihaz kısıtlamaları**  >  **Microsoft Edge Browser**). [Microsoft Edge tarayıcısı](device-restrictions-windows-holographic.md#microsoft-edge-browser) , kullanılabilir holographic for Business ayarlarını listeler ve açıklar.

    - **Bilgi noktası tarayıcısı ekleme**: Windows holographic for Business 'ta desteklenmez.

  - **Uygulamalar**
    - **Mağaza uygulaması ekleme**: LOB uygulamaları [dahil olmak üzere](../apps/apps-add.md)Intune 'a eklediğiniz veya Intune 'a dağıttığınız mevcut bir uygulamayı seçin. Listelenen uygulamalarınız yoksa Intune, [Intune 'a eklediğiniz](../apps/store-apps-windows.md)birçok [uygulama türünü](../apps/apps-add.md) destekler.
    - **Win32 uygulaması ekle**: Windows Holographic for Business’ta desteklenmez.
    - **AUMID’e göre ekle**: Notepad veya Hesap Makinesi gibi gelen kutusu Windows uygulamalarını eklemek için bu seçeneği kullanın. Aşağıdaki özellikleri girin:

      - **Uygulama adı**: Gereklidir. Uygulama için bir ad girin.
      - **Uygulama kullanıcı modeli kimliği (AUMID)**: Gereklidir. Windows uygulamasının uygulama kullanıcı modeli kimliğini (AUMID) girin. Bu kimliği almak için bkz. [Yüklü bir uygulamanın Uygulama Kullanıcı Modeli Kimliğini bulma](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **Oto başlatması**: isteğe bağlı. Uygulamalarınızı ve tarayıcınızı ekledikten sonra, Kullanıcı oturum açtığında otomatik olarak açılacak bir uygulama veya tarayıcı seçin. Yalnızca tek bir uygulama veya tarayıcı, oto başlatılabilir.
    - **Kutucuk boyutu**: Gereklidir. Uygulamalarınızı ekledikten sonra küçük, orta, geniş veya büyük bir uygulama kutucuğu boyutu seçin.

- **Alternatif başlangıç düzenini kullan**: uygulamaların sırası dahil olmak üzere uygulamaların başlangıç menüsünde nasıl göründüğünü açıklayan bir XML dosyası girmek için **Evet** ' i seçin. Başlangıç menünüzü daha fazla özelleştirmeniz gerekiyorsa bu seçeneği kullanın. [Başlangıç düzenini özelleştirme ve dışarı aktarma](/hololens/hololens-kiosk#start-layout-for-hololens), Windows Holographic for Business cihazları için rehberlik sağlar ve belirli bir XML dosyası içerir.

- **Windows Görev Çubuğu**: Windows Holographic for Business’ta desteklenmez.
- **Indirmeler klasörüne erişime Izin ver**: Windows holographic for Business üzerinde desteklenmez.
- **Uygulama yeniden başlatmaları Için bakım penceresini belirtin**: Windows holographic for Business 'ta desteklenmez.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

[Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience)ve [Windows 10 ve üzeri](kiosk-settings-windows.md) cihazlar için bilgi noktası profilleri de oluşturabilirsiniz.