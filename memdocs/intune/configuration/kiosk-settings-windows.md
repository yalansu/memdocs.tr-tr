---
title: Microsoft Intune'da Windows 10 için bilgi noktası ayarları - Azure | Microsoft Docs
description: Windows 10 (ve sonraki) cihazlarınızı tek uygulama ve çoklu uygulama kiisleri olarak yapılandırın, Başlat menüsünü özelleştirin, uygulamalar ekleyin, görev çubuğunu görüntüleyin ve Microsoft Intune bir Web tarayıcısını yapılandırın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a4595be1e29910f71d48e82db456e3676bd69c3
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815434"
---
# <a name="windows-10-and-later-device-settings-to-run-as-a-kiosk-in-intune"></a>Intune 'da bilgi noktası olarak çalıştırılacak Windows 10 ve üzeri cihaz ayarları

Windows 10 ve üzeri cihazlarda, bu cihazları tek uygulama bilgi noktası modunda veya çok uygulama bilgi noktası modunda çalışacak şekilde yapılandırabilirsiniz.

Bu makalede, Windows 10 ve üzeri cihazlarda denetleyebilmeniz için farklı ayarlar listelenmektedir ve açıklanmaktadır. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak, Windows 10 ve üzeri cihazlarınızı bilgi noktası modunda çalışacak şekilde yapılandırmak için bu ayarları kullanın.

Bir Intune Yöneticisi olarak bu ayarları oluşturabilir ve cihazlarınıza atayabilirsiniz.

Intune 'da Windows bilgi noktası özelliği hakkında daha fazla bilgi edinmek için bkz. [bilgi noktası ayarlarını yapılandırma](kiosk-settings.md).

## <a name="before-you-begin"></a>Başlamadan önce

- [Windows 10 bilgi noktası cihaz yapılandırma profili](kiosk-settings.md#create-the-profile)oluşturun.

- Bu bilgi noktası profili, [Microsoft Edge bilgi noktası ayarları](device-restrictions-windows-10.md#microsoft-edge-browser)kullanılarak oluşturduğunuz cihaz kısıtlamaları profiliyle doğrudan ilgilidir. Özetlemek gerekirse:

  1. Bu bilgi noktası profilini, cihazı bilgi noktası modunda çalıştırmak için oluşturun.
  2. [Cihaz kısıtlamaları profilini](device-restrictions-windows-10.md#microsoft-edge-browser)oluşturun ve Microsoft Edge 'de izin verilen belirli özellikleri ve ayarları yapılandırın.

- Tüm dosyaların, betiklerin ve kısayolların yerel sistemde bulunduğundan emin olun. Diğer Windows gereksinimleri dahil daha fazla bilgi için bkz. [Özelleştirme ve dışa aktarma başlangıç düzeni](/windows/configuration/customize-and-export-start-layout).

> [!IMPORTANT]
> Bu bilgi noktası profilini [Microsoft Edge profilinizle](device-restrictions-windows-10.md#microsoft-edge-browser)aynı cihazlara atadığınızdan emin olun.

## <a name="single-app-full-screen-kiosk"></a>Tek uygulama, tam ekran bilgi noktası

Cihazda yalnızca bir uygulama çalıştırır.

- **Bilgi noktası modu seçin**: **tek uygulama, tam ekran bilgi noktası**seçin.

- **Kullanıcı oturum açma türü**: uygulamayı çalıştıran hesap türünü seçin. Seçenekleriniz şunlardır:

  - **Otomatik oturum açma (Windows 10 sürüm 1803 ve üzeri)**: bir Konuk hesabına benzer şekilde, kullanıcının oturum açmasını gerektirmeyen, genel kullanıma yönelik ortamlarda bilgi noktaları kullanın. Bu ayar, [AssignedAccess CSP](/windows/client-management/mdm/assignedaccess-csp) kullanır.
  - **Yerel kullanıcı hesabı**: Cihaz için yerel kullanıcı hesabını girin. Girdiğiniz hesap, bilgi noktasında oturum açar.

- **Uygulama türü**: uygulama türünü seçin. Seçenekleriniz şunlardır:

  - **Microsoft Edge tarayıcısı Ekle**: **Microsoft Edge tarayıcısı**' nı seçin ve **Microsoft Edge bilgi noktası modu türünü**seçin:

    - **Dijital/Etkileşimli imza**: bir URL tam ekran açar ve yalnızca o Web sitesindeki içeriği gösterir. [Dijital Işaretleri ayarla](/windows/configuration/setup-digital-signage) özelliği, bu özellik hakkında daha fazla bilgi sağlar.
    - **Genel göz atma (InPrivate)**: Microsoft Edge 'in sınırlı bir çok sekmeli sürümünü çalıştırır. Kullanıcılar herkese açık bir şekilde göz atabilir veya gözatma oturumlarını sonlandırabilir.

    Bu seçenekler hakkında daha fazla bilgi için bkz. [Microsoft Edge bilgi noktası modunu dağıtma](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

    > [!NOTE]
    > Bu ayar cihazda Microsoft Edge tarayıcısını sunar. Microsoft Edge 'e özgü ayarları yapılandırmak için bir cihaz kısıtlamaları profili oluşturun (**cihazlar**  >  **yapılandırma profilleri**  >  **Create profile**  >  **Windows 10** for platform > **cihaz kısıtlamaları**  >  **Microsoft Edge Browser**). [Microsoft Edge tarayıcısı](device-restrictions-windows-10.md#microsoft-edge-browser) , kullanılabilir ayarları listeler ve açıklar.

  - **Bilgi noktası tarayıcısı Ekle**: **bilgi noktası tarayıcı ayarları**' nı seçin. Bu ayarlar bilgi noktasındaki web tarayıcısı uygulamasını denetler. [Bilgi noktası tarayıcı uygulamasını](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP) mağazadan aldığınızdan emin olun, bunu bir [Istemci uygulaması](../apps/apps-add.md)olarak Intune 'a ekleyin. Ardından, uygulamayı bilgi noktası cihazlarına atayın.

    Aşağıdaki ayarları girin:

    - **Varsayılan giriş sayfası URL 'si**: bilgi noktası tarayıcısı açıldığında veya tarayıcı yeniden başlatıldığında gösterilen varsayılan URL 'yi girin. Örneğin `http://bing.com` veya `http://www.contoso.com` girin.

    - **Giriş düğmesi**: Bilgi noktası tarayıcısının giriş düğmesini **gösterin** veya **gizleyin**. Varsayılan olarak düğme gösterilmez.

    - **Gezinti düğmeleri**: İleri ve geri düğmelerini **gösterin** veya **gizleyin**. Varsayılan olarak gezinti düğmeleri gösterilmez.

    - **Oturumu sonlandır düğmesi**: Oturumu sonlandır düğmesini **gösterin** veya **gizleyin**. Gösterildiğinde, kullanıcı düğmeyi seçer ve uygulama oturumun sonlandırılmasını ister. Onaylandığında tarayıcı, tüm göz atma verilerini (çerezler, önbellek vb.) temizler ve daha sonra varsayılan URL’yi açar. Varsayılan olarak düğme gösterilmez.

    - **Boşta kalma zamanından sonra tarayıcıyı yenile**: bilgi noktası tarayıcısı yeni bir durumda yeniden başlatılana kadar, 1-1440 dakikadan itibaren boşta kalma süresi miktarını girin. Boşta kalma süresi, kullanıcının son etkileşimini bu yana geçen dakika sayısıdır. Varsayılan olarak değer boştur veya boşluktur ve bu, boşta kalma süresinin olmadığı anlamına gelir.

    - **İzin verilen web siteleri**: Belirli Web sitelerinin açılmasına izin vermek için bu ayarı kullanın. Diğer bir deyişle, cihazda web sitelerine erişimi kısıtlamak veya tamamen önlemek için bu özelliği kullanın. Örneğin `http://contoso.com` adresindeki tüm Web sitelerinin açılmasına izin verebilirsiniz. Varsayılan olarak tüm Web sitelerine izin verilir.

      Belirli web sitelerine izin vermek için izin verilecek web sitelerini ayrı satırlarda listeleyen bir dosyayı karşıya yükleyin. Bir dosya eklemezseniz tüm web sitelerine izin verilir. Varsayılan olarak, Intune Web sitesinin tüm alt etki alanlarına izin verir. Örneğin, `sharepoint.com` etki alanını girersiniz. Intune, ve gibi tüm alt etki alanlarına otomatik olarak izin verir `contoso.sharepoint.com` `my.sharepoint.com` . Yıldız işareti () gibi joker karakterler girmeyin `*` .

      Örnek dosyanız, aşağıdaki listeye benzer görünmelidir:

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > Microsoft bilgi noktası tarayıcısı kullanılarak otomatik oturum açma özelliği etkinleştirilmiş Windows 10 kiosks, Microsoft Store Iş için çevrimdışı bir lisans kullanmalıdır. Bu gereksinim, otomatik oturum açma 'nın Azure Active Directory (AD) kimlik bilgileri olmayan bir yerel kullanıcı hesabı kullanması nedeniyle oluşur. Bu nedenle, çevrimiçi lisanslar değerlendirilemiyor. Daha fazla bilgi için bkz. [çevrimdışı uygulamaları dağıtma](/microsoft-store/distribute-offline-apps).

  - **Mağaza uygulaması ekleme**: **Mağaza uygulaması Ekle**' yi seçin ve listeden bir uygulama seçin.

    Listede hiç uygulama yok mu? [İstemci Uygulamaları](../apps/apps-add.md)’ndaki adımları kullanarak birkaç uygulama ekleyin.

- **Uygulama yeniden başlatmaları Için bakım penceresini belirtin**: bazı uygulamalar, uygulama yüklemesinin tamamlanabilmesi için yeniden başlatma gerektirir veya güncelleştirmelerin yüklenmesi tamamlanır. **Gerektir** , bir bakım penceresi oluşturur. Uygulama yeniden başlatma gerektiriyorsa, bu pencere sırasında yeniden başlatılır.

  Şunları da girin:

  - **Bakım penceresi başlangıç zamanı**: yeniden başlatma gerektiren tüm uygulama güncelleştirmeleri için istemcileri denetlemeye başlamak üzere günün tarihini ve saatini seçin. Varsayılan başlangıç saati gece yarısı veya sıfır dakikadır. Boşsa, uygulamalar bir uygulama güncelleştirmesi yüklendikten sonra zamanlanmamış bir süre 3 gün sonra yeniden başlatılır.

  - **Bakım penceresi yinelemesi**: varsayılan olarak günlük. Uygulama güncelleştirmelerinin bakım pencerelerinin ne sıklıkta yapılacağını seçin. Zamanlanmamış uygulama yeniden başlatmalarının önüne geçmek için, öneri **her gün**olur.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [ApplicationManagement/Scheduleforcerestartforupdatearızaları CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="multi-app-kiosk"></a>Çoklu uygulama bilgi noktası

Bu modda uygulamalar Başlat menüsünde sağlanır. Bu uygulamalar, yalnızca kullanıcıların açabildiği uygulamalardır. Bir uygulamanın başka bir uygulamaya bağımlılığı varsa, her ikisi de izin verilen uygulamalar listesine eklenmelidir. Örneğin, Internet Explorer 64 bit, Internet Explorer 32 bit 'e bağımlıdır. bu nedenle hem "C:\Program Files\explorer\iexplore.exe" hem de "C:\Program Files (x86) \Internet Explorer\iexplore.exe" için izin vermelisiniz. 

- **Bilgi noktası modu seçin**: **çok uygulama bilgi noktası**' nı seçin.

- **Windows 10 ' un modundaki cihazları hedefleyin**:
  - **Evet**: bilgi noktası profilinde mağaza uygulamalarına ve aumıd uygulamalarına izin verir. Win32 uygulamalarını dışlar.
  - **Hayır**: bilgi noktası profilinde mağaza uygulamalarına, Win32 uygulamalarına ve aumıd uygulamalarına izin verir. Bu bilgi noktası profili S modundaki cihazlara dağıtılmadı.

- **Kullanıcı oturum açma türü**: uygulamalarınızı çalıştıran hesap türünü seçin. Seçenekleriniz şunlardır:

  - **Otomatik oturum açma (Windows 10 sürüm 1803 ve üzeri)**: bir Konuk hesabına benzer şekilde, kullanıcının oturum açmasını gerektirmeyen, genel kullanıma yönelik ortamlarda bilgi noktaları üzerinde kullanın. Bu ayar, [AssignedAccess CSP](/windows/client-management/mdm/assignedaccess-csp) kullanır.
  - **Yerel kullanıcı hesabı**: Cihaz için yerel kullanıcı hesabını **ekleyin**. Girdiğiniz hesap, bilgi noktasında oturum açar.
  - **Azure AD kullanıcısı veya grubu (Windows 10 sürüm 1803 ve üzeri)**: **Ekle**' yi SEÇIN ve listeden Azure AD kullanıcıları veya grupları ' nı seçin. Birden çok kullanıcı ve grup seçebilirsiniz. Değişikliklerinizi kaydetmek için **Seçin**’e tıklayın.
  - **HoloLens ziyaretçisi**: Ziyaretçi hesabı, [paylaşılan PC modu kavramlarında](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts) anlatıldığı gibi, kullanıcı kimlik bilgileri veya kimlik doğrulaması gerektirmeyen bir konuk hesabıdır.

- **Tarayıcı ve uygulamalar**: bilgi noktası cihazında çalıştırılacak uygulamaları ekleyin. Birden fazla uygulama ekleyebileceğinizi unutmayın.

  :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-add-applications-browser.png" alt-text="Microsoft Intune 'de çok uygulama bilgi noktası profiline tarayıcılar veya uygulamalar ekleyin.":::  

  - **Browsers (Tarayıcılar)**

    - **Microsoft Edge Ekle**: Microsoft Edge uygulama kılavuzuna eklenir ve tüm uygulamalar bu bilgi noktasında çalıştırılabilir. **Microsoft Edge bilgi noktası modu türünü**seçin:

      - **Normal mod (Microsoft Edge 'in tam sürümü)**: tüm göz atma özellikleriyle Microsoft Edge 'in tam bir sürümünü çalıştırır. Kullanıcı verileri ve durumu oturumlar arasında kaydedilir.
      - **Genel göz atma (InPrivate)**: tam ekran modunda çalışan bilgi noktaları için özel bir deneyim ile Microsoft Edge InPrivate 'ın çok bölgeli bir sürümünü çalıştırır.

      Bu seçenekler hakkında daha fazla bilgi için bkz. [Microsoft Edge bilgi noktası modunu dağıtma](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Bu ayar cihazda Microsoft Edge tarayıcısını sunar. Microsoft Edge 'e özgü ayarları yapılandırmak için bir cihaz kısıtlamaları profili**oluşturun (cihaz**  >  **yapılandırma profilleri**  >  platform için **Windows 10** > > **profil oluşturma** > **cihaz kısıtlamaları**  >   **Microsoft Edge tarayıcısı**). [Microsoft Edge tarayıcısı](device-restrictions-windows-10.md#microsoft-edge-browser) , kullanılabilir ayarları listeler ve açıklar.

    - **Bilgi noktası tarayıcısı Ekle**: Bu ayarlar, bilgi noktasında bir Web tarayıcısı uygulamasını denetler. Bilgi noktasına web tarayıcısı uygulamasını [İstemci Uygulamaları](../apps/apps-add.md)’nı kullanarak dağıttığınıza emin olun.

      Aşağıdaki ayarları girin:

      - **Varsayılan giriş sayfası URL 'si**: bilgi noktası tarayıcısı açıldığında veya tarayıcı yeniden başlatıldığında gösterilen varsayılan URL 'yi girin. Örneğin `http://bing.com` veya `http://www.contoso.com` girin.

      - **Giriş düğmesi**: Bilgi noktası tarayıcısının giriş düğmesini **gösterin** veya **gizleyin**. Varsayılan olarak düğme gösterilmez.

      - **Gezinti düğmeleri**: İleri ve geri düğmelerini **gösterin** veya **gizleyin**. Varsayılan olarak gezinti düğmeleri gösterilmez.

      - **Oturumu sonlandır düğmesi**: Oturumu sonlandır düğmesini **gösterin** veya **gizleyin**. Gösterildiğinde, kullanıcı düğmeyi seçer ve uygulama oturumun sonlandırılmasını ister. Onaylandığında tarayıcı, tüm göz atma verilerini (çerezler, önbellek vb.) temizler ve daha sonra varsayılan URL’yi açar. Varsayılan olarak düğme gösterilmez.

      - **Boşta kalma süresi geçince tarayıcıyı yenile**: Bilgi noktası tarayıcısı temiz bir durumda yeniden başlatılana kadar geçecek oturum başka kalma süresini (1-1440 dakika) girin. Boşta kalma süresi, kullanıcının son etkileşimini bu yana geçen dakika sayısıdır. Varsayılan olarak değer boştur veya boşluktur ve bu, boşta kalma süresinin olmadığı anlamına gelir.

      - **İzin verilen web siteleri**: Belirli Web sitelerinin açılmasına izin vermek için bu ayarı kullanın. Diğer bir deyişle, cihazda web sitelerine erişimi kısıtlamak veya tamamen önlemek için bu özelliği kullanın. Örneğin `contoso.com*` adresindeki tüm Web sitelerinin açılmasına izin verebilirsiniz. Varsayılan olarak tüm Web sitelerine izin verilir.

        Belirli Web sitelerine izin vermek için izin verilen Web siteleri listesini içeren bir .csv dosyasını karşıya yükleyin. Bir .csv dosyası eklemezseniz tüm Web sitelerine izin verilir.

      > [!NOTE]
      > Microsoft bilgi noktası tarayıcısı kullanılarak otomatik oturum açma özelliği etkinleştirilmiş Windows 10 kiosks, Microsoft Store Iş için çevrimdışı bir lisans kullanmalıdır. Bu gereksinim, otomatik oturum açma 'nın Azure Active Directory (AD) kimlik bilgileri olmayan bir yerel kullanıcı hesabı kullanması nedeniyle oluşur. Bu nedenle, çevrimiçi lisanslar değerlendirilemiyor. Daha fazla bilgi için bkz. [çevrimdışı uygulamaları dağıtma](/microsoft-store/distribute-offline-apps).

  - **Uygulamalar**

    - **Mağaza uygulaması ekle**: İş İçin Microsoft Store’dan bir uygulama ekleyin. Listede hiç uygulama yoksa uygulama edilebilir ve [bunları Intune’a ekleyebilirsiniz](../apps/store-apps-windows.md). Örneğin Bilgi Noktası Tarayıcısı, Excel, OneNote gibi pek çok uygulama ekleyebilirsiniz.

    - **Win32 uygulaması ekle**: Win32 uygulamaları, Visual Studio Code veya Google Chrome gibi geleneksel masaüstü uygulamalarıdır. Aşağıdaki özellikleri girin:

      - **Uygulama adı**: Gereklidir. Uygulama için bir ad girin.
      - **Uygulama yürütülebilir dosyasının yerel yolu**: gerekli. Yürütülebilir dosyanın yolunu girin, örneğin `C:\Program Files (x86)\Microsoft VS Code\Code.exe` veya `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`.
      - **Win32 uygulaması Için uygulama Kullanıcı MODELI kimliği (aumıd)**: Win32 uygulamasının uygulama kullanıcı modeli KIMLIĞINI (aumıd) girin. Bu ayar, masaüstündeki kutucuk başlangıç düzenini belirler. Bu KIMLIĞI almak için bkz. [Get-StartApps](/powershell/module/startlayout/get-startapps?view=win10-ps).

    - **AUMID’e göre ekle**: Notepad veya Hesap Makinesi gibi gelen kutusu Windows uygulamalarını eklemek için bu seçeneği kullanın. Aşağıdaki özellikleri girin:

      - **Uygulama adı**: Gereklidir. Uygulama için bir ad girin.
      - **Uygulama kullanıcı modeli kimliği (AUMID)**: Gereklidir. Windows uygulamasının uygulama kullanıcı modeli kimliğini (AUMID) girin. Bu kimliği almak için bkz. [Yüklü bir uygulamanın Uygulama Kullanıcı Modeli Kimliğini bulma](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **Oto başlatması**: isteğe bağlı. Uygulamalarınızı ve tarayıcınızı ekledikten sonra, Kullanıcı oturum açtığında otomatik olarak açılacak bir uygulama veya tarayıcı seçin. Yalnızca tek bir uygulama veya tarayıcı, oto başlatılabilir.
    - **Kutucuk boyutu**: Gereklidir. Uygulamalarınızı ekledikten sonra küçük, orta, geniş veya büyük bir uygulama kutucuğu boyutu seçin.

      :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-autolaunch-tiles.png" alt-text="Uygulamayı veya tarayıcıyı otomatik olarak başlatın ve Microsoft Intune bir çok uygulama bilgi noktası profilinde kutucuk boyutunu seçin.":::

  > [!TIP]
  > Tüm uygulamaları ekledikten sonra tıklayıp sürükleme yoluyla listedeki uygulamaların görüntülenme sırasını değiştirebilirsiniz.  

- **Alternatif başlangıç düzenini kullan**: uygulamaların sırası dahil olmak üzere uygulamaların başlangıç menüsünde nasıl göründüğünü açıklayan bir XML dosyası girmek için **Evet** ' i seçin. Başlangıç menünüzü daha fazla özelleştirmeniz gerekiyorsa bu seçeneği kullanın. [Özelleştirme ve dışa aktarma başlangıç düzeninde](/windows/configuration/customize-and-export-start-layout) bazı kılavuzluk ve örnek XML vardır.

- **Windows Görev Çubuğu**: Görev çubuğunu **Göstermeyi** veya **Gizlemeyi** seçin. Varsayılan olarak görev çubuğu gösterilmez. Wi-Fi simgesi gibi simgeler gösterilir, ancak ayarlar son kullanıcılar tarafından değiştirilemez.

- **Indirmeler klasörüne erişime Izin ver**: kullanıcıların Windows Gezgini 'nde indirmeler klasörüne erişmesine izin vermek için **Evet** ' i seçin. Varsayılan olarak, Indirmeler klasörüne erişim devre dışıdır. Bu özellik genellikle son kullanıcıların bir tarayıcıdan indirilen öğelere erişmesi için kullanılır.

- **Uygulama yeniden başlatmaları Için bakım penceresini belirtin**: bazı uygulamalar, uygulama yüklemesinin tamamlanabilmesi için yeniden başlatma gerektirir veya güncelleştirmelerin yüklenmesi tamamlanır. **Gerektir** , bir bakım penceresi oluşturur. Uygulamalar yeniden başlatma gerektiriyorsa, bu pencere sırasında yeniden başlatılır.

  Şunları da girin:

  - **Bakım penceresi başlangıç zamanı**: yeniden başlatma gerektiren tüm uygulama güncelleştirmeleri için istemcileri denetlemeye başlamak üzere günün tarihini ve saatini seçin. Varsayılan başlangıç saati gece yarısı veya sıfır dakikadır. Boşsa, uygulamalar bir uygulama güncelleştirmesi yüklendikten sonra zamanlanmamış bir süre 3 gün sonra yeniden başlatılır.

  - **Bakım penceresi yinelemesi**: varsayılan olarak günlük. Uygulama güncelleştirmelerinin bakım pencerelerinin ne sıklıkta yapılacağını seçin. Zamanlanmamış uygulama yeniden başlatmalarının önüne geçmek için, öneri **her gün**olur.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  [ApplicationManagement/Scheduleforcerestartforupdatearızaları CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="next-steps"></a>Sonraki adımlar

[Profili atayın](device-profile-assign.md)ve [durumunu izleyin](device-profile-monitor.md).

[Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience)ve [Windows holographic for Business](kiosk-settings-holographic.md) cihazları için bilgi noktası profilleri de oluşturabilirsiniz.

Ayrıca bkz. [tek uygulama bilgi noktası ayarlama](/windows/configuration/kiosk-single-app) veya Windows kılavuzunda [birden çok uygulama bilgi noktası](/windows/configuration/lock-down-windows-10-to-specific-apps) ayarlama.