---
title: Microsoft Intune-Azure 'da Android kurumsal cihaz ayarları | Microsoft Docs
description: Android Enterprise veya Android for Work cihazlarında, kopyalama ve yapıştırma, bildirimleri gösterme, uygulama izinleri, veri paylaşımı, parola uzunluğu, oturum açma hatalarında oturum açmak, parolaları yeniden kullanmak ve iş kişilerinin Bluetooth paylaşımını etkinleştirmek dahil olmak üzere cihazdaki ayarları kısıtlayın. Tek bir uygulama veya birden çok uygulama çalıştırmak için cihazları adanmış bir cihaz bilgi noktası olarak yapılandırın.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal, priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f49ba4fffd84ffae3e5b47ad74088b65d599533
ms.sourcegitcommit: cb9b452f8e566fe026717b59c142b65f426e5033
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86491261"
---
# <a name="android-enterprise-device-settings-to-allow-or-restrict-features-using-intune"></a>Intune kullanarak özelliklere izin vermek veya erişimi kısıtlamak için Android kurumsal cihaz ayarları

Bu makale, Android kurumsal cihazlarda denetleyebilmeniz için farklı ayarları listeler ve tanımlar. Mobil cihaz yönetimi (MDM) çözümünüzün bir parçası olarak bu ayarları, özelliklere izin vermek veya devre dışı bırakmak, uygulamaları adanmış cihazlarda çalıştırmak, güvenliği denetlemek ve daha fazlasını yapmak için kullanın.

## <a name="before-you-begin"></a>Başlamadan önce

[Bir cihaz yapılandırma profili oluşturun](device-restrictions-configure.md).

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Tam olarak yönetilen, adanmış ve şirkete ait Iş profili

Bu ayarlar, Intune 'un Android kurumsal tam olarak yönetilen, adanmış ve şirkete ait iş profili aygıtları gibi tüm cihazı denetlediği Android kurumsal kayıt türleri için geçerlidir.

Bazı ayarlar tüm kayıt türleri tarafından desteklenmez. Hangi ayarların hangi kayıt türleri tarafından desteklendiğini görmek için Kullanıcı arabirimine bakın. Her ayar, hangi kayıt türlerinin bu ayarı kullanacağını gösteren bir başlık altındadır.

![Üst bilgiler ayarlanıyor.](./media/device-restrictions-android-for-work/setting-headers.png)

Bazı ayarlar yalnızca şirkete ait cihazlar için iş profili düzeyinde iş profili ile uygulanır. Bu ayarlar, tam olarak yönetilen ve adanmış cihazlar için cihaz genelinde hala geçerlidir. Bu ayarlar Kullanıcı arabirimindeki *(iş profili düzeyi)* tanımlayıcısı ile işaretlenir.

![Üst bilgiler ayarlanıyor.](./media/device-restrictions-android-for-work/work-profile-level.png)


### <a name="general"></a>Genel

- **Ekran yakalama**: **engelleme** , cihazdaki ekran görüntülerini veya ekran yakalamalarını engeller. Ayrıca güvenli bir video çıkışına sahip olmayan görüntü cihazlarında gösterilen içeriği engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların ekran içeriğini görüntü olarak yakalamasına izin verebilir.
- **Kamera**: **blok** cihazdaki kameraya erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kameraya erişime izin verebilir.

  Intune yalnızca cihaz kamerasına erişimi yönetir. Resimlere veya videolara erişimi yoktur.

- **Varsayılan izin ilkesi**: Bu ayar, çalışma zamanı izin istekleri için varsayılan izin ilkesini tanımlar. Seçenekleriniz
  - **Cihaz varsayılanı**: cihazın varsayılan ayarını kullanın.
  - **İstem**: kullanıcılardan izni onaylaması istenir.
  - **Otomatik olarak izin ver**: İzinler otomatik olarak verilir.
  - **Otomatik olarak reddet**: İzinler otomatik reddedilir.
- **Tarih ve saat değişiklikleri**: **Engelle** , kullanıcıların tarih ve saati el ile değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların cihazdaki tarih ve saat ayarlama yapmasına izin verebilir.
- **Birim değişiklikleri**: **Engelle** , kullanıcıların cihazın birimini değiştirmesini önler ve ana birimi de kapatır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazdaki birim ayarlarının kullanılmasına izin verebilir.
- **Fabrika Sıfırlaması**: **Block** , kullanıcıların cihaz ayarlarındaki fabrika sıfırlaması seçeneğini kullanmalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazda bu ayarı kullanmasına izin verebilir.
- **Güvenli önyükleme**: **Block** , kullanıcıların cihazı güvenli moda başlatmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazı güvenli modda yeniden önyüklemelerine izin verebilir.
- **Durum çubuğu**: **blok** , bildirimler ve hızlı ayarlar dahil olmak üzere durum çubuğuna erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların durum çubuğuna erişmesine izin verebilir.
- **Dolaşım veri Hizmetleri**: **blok** , hücresel ağ üzerinde veri dolaşımını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihaz hücresel ağ üzerindeyken veri dolaşımına izin verebilir.
- **Wi-Fi ayarı değişiklikleri**: **Engelle** , kullanıcıların cihaz sahibi tarafından oluşturulan Wi-Fi ayarlarını değiştirmesini engeller. Kullanıcılar kendi Wi-Fi yapılandırmalarının oluşturulmasını sağlayabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazdaki Wi-Fi ayarlarını değiştirmesine izin verebilir.
- **Wi-Fi erişim noktası yapılandırması**: **blok** kullanıcıların herhangi bir Wi-Fi yapılandırması oluşturmasını veya değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazdaki Wi-Fi ayarlarını değiştirmesine izin verebilir.
- **Bluetooth yapılandırması**: **blok** kullanıcıların cihazda Bluetooth 'u yapılandırmalarını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda Bluetooth kullanılmasına izin verebilir.
- **Internet paylaşımı ve etkin noktalara erişim**: **blok** , İnternet paylaşımını ve taşınabilir etkin noktalara erişimi engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, internet paylaşımı ve taşınabilir etkin noktalara erişime izin verebilir.
- **USB depolama**: cihazda USB depolamaya erişime **izin ver** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi USB depolamaya erişimi engelleyebilir.
- **USB dosya aktarımı**: **blok** dosyaların USB üzerinden aktarımını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi dosya aktarmaya izin verebilir.
- **Dış medya**: **blok** , cihazdaki herhangi bir dış medyanın kullanılmasını veya bağlanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi cihazda dış medyaya izin verebilir.
- NFC: **Block** **kullanan Kirme verileri**, uygulamalardan gelen verileri Kirmek için yakın alan iletişimi (NFC) teknolojisinin kullanılmasını önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, cihazlar arasında veri paylaşmak için NFC 'nin kullanılmasına izin verebilir.
- **Hata ayıklama özellikleri**: kullanıcıların cihazdaki hata ayıklama özelliklerini kullanmasına izin vermek Için **izin ver** ' i seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazdaki hata ayıklama özelliklerini kullanmalarını engelleyebilir.
- **Mikrofon ayarlaması**: **engelleme** , kullanıcıların mikrofonu kapatıp mikrofon birimini ayarlamasına engel olur. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazdaki mikrofonun hacmini kullanmasına ve ayarlamasına izin verebilir.
- **Fabrika Sıfırlaması koruma e-postaları**: **Google hesabı e-posta adreslerini**seçin. Temizlenmeden sonra cihazın kilidini açabilebilen cihaz yöneticilerinin e-posta adreslerini girin. E-posta adreslerini, gibi bir noktalı virgülle ayırdığınızdan emin olun `admin1@gmail.com;admin2@gmail.com` . E-posta girilmemişse, fabrika ayarlarına geri yüklendikten sonra herkes cihazın kilidini açabilir. Bu e-postalar yalnızca, Kurtarma menüsünü kullanarak Fabrika Sıfırlaması çalıştırma gibi kullanıcı olmayan bir fabrika sıfırlaması çalıştırıldığında geçerlidir.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Ağ çıkış taraması**: **etkinleştirme** , kullanıcıların ağ çıkış tarama özelliğini açmasına olanak sağlar. Cihaz önyüklendiğinde bir ağ bağlantısı yapılmazsa, çıkış taraması geçici olarak bir ağa bağlanmayı ve cihaz ilkesini yenilemeyi ister. Bu ilke uygulandıktan sonra geçici ağ unutulur ve cihaz önyüklemeye devam eder. Bu özellik aşağıdaki durumlarda cihazları bir ağa bağlar:
  - Son ilkede uygun bir ağ yok.
  - Cihaz, kilit görevi modunda bir uygulamada önyüklenir.
  - Kullanıcılar cihaz ayarlarına ulaşamıyor.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kullanıcıların cihazda ağ çıkış tarama özelliğini açmasını önleyebilir.

- **Sistem güncelleştirmesi**: cihazın uçak güncelleştirmelerini nasıl işlediğini tanımlamak için bir seçenek belirleyin. Seçenekleriniz
  - **Cihaz Varsayılanı**: Cihazın varsayılan ayarını kullanın.
  - **Otomatik**: Güncelleştirmeler, kullanıcı etkileşimi olmadan otomatik olarak yüklenir. Bu ilkeyi seçmek, bekleyen tüm güncelleştirmeleri hemen yükler.
  - **Erteleme**: Güncelleştirmeler 30 gün boyunca ertelenir. 30 günün sonunda Android, kullanıcılardan güncelleştirmeyi yüklemesini ister. Cihaz üreticilerin veya taşıyıcıların önemli güvenli güncelleştirmelerinin ertelenmesini engellemek (muaf tutmak) mümkündür. Muaf tutulan güncelleştirme, cihazdaki kullanıcılara bir sistem bildirimi gösterir.
  - **Bakım penceresi**: Güncelleştirmeleri Intune'da ayarladığınız bir günlük bakım penceresi içinde otomatik olarak yükler. Yükleme 30 gün boyunca günlük olarak çalışır ve yeterli alan veya pil düzeyi yoksa başarısız olabilir. Android, 30 gün sonra kullanıcılardan yüklenmesini ister. Bu pencere ayrıca Oynatma uygulamalarının güncelleştirmelerini yüklemek için de kullanılır. Tek uygulamayla ayrılmış cihaz ön plan uygulamaları güncelleştirilemeyebilir, kiosks gibi adanmış cihazlar için bu seçeneği kullanın.

- **Bildirim pencereleri**: **devre dışı**olarak ayarlandığında, Tolar, gelen çağrılar, giden çağrılar, sistem uyarıları ve sistem hataları gibi pencere bildirimleri cihazda gösterilmez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bildirimleri gösterebilir.
- **İlk kullanım Ipuçlarını atla**: **Etkinleştir** , öğreticilerde adım adım geçen uygulamalardan veya uygulamanın başladığı bir ipuçlarına ilişkin önerileri gizler veya atlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, uygulama başlatıldığında işletim sistemi bu önerileri gösterebilir.

### <a name="system-security"></a>Sistem güvenliği

- **Uygulamalarda tehdit taraması**: **gerektir** (varsayılan), uygulamaları yüklenmeden önce ve sonra taraması için Google Play koruma sağlar. Tehdit algılarsa, uygulamayı cihazdan kaldırmak için kullanıcıları uyarabilir. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi uygulamaları taramak için Google Play koruyamayabilir veya çalıştırmayabilir.

### <a name="device-experience"></a>Cihaz deneyimi

Adanmış cihazlarınızda bilgi noktası stili bir deneyim yapılandırmak veya tam olarak yönetilen cihazlarınızda giriş ekranı deneyimlerini özelleştirmek için bu ayarları kullanın. Cihazları tek bir uygulamayı çalıştıracak veya birçok uygulama çalıştıracak şekilde yapılandırabilirsiniz. Cihaz bilgi noktası moduyla ayarlandığında, yalnızca eklediğiniz uygulamalar kullanılabilir.

**Kayıt profili türü**: cihazlarınızda Microsoft başlatıcısı 'Nı veya Microsoft tarafından yönetilen giriş ekranını yapılandırmaya başlamak için bir kayıt profili türü seçin. Seçenekleriniz şunlardır:

- **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, kullanıcılar cihazın varsayılan giriş ekranı deneyimini görebilirler.
- **Adanmış cihaz**: adanmış cihazlarınızda bilgi noktası stili bir deneyim yapılandırın. Bu ayarları yapılandırmadan önce, cihazlarda istediğiniz uygulamaları [eklediğinizden](../apps/apps-add-android-for-work.md) ve [atamadığınızdan](../apps/apps-deploy.md) emin olun.

  - **Bilgi noktası modu**: cihazın bir uygulama çalıştırmasını veya birden çok uygulamayı çalıştırmasını seçin. Seçenekleriniz şunlardır:

    - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Tek uygulama**: kullanıcılar cihazdaki tek bir uygulamaya yalnızca erişebilir. Cihaz başlatıldığında yalnızca belirli bir uygulama başlatılır. Kullanıcılar yeni uygulamalar açamaz veya çalışan uygulamayı değiştiremez.

      - **Bilgi noktası modu için kullanılacak bir uygulama seçin**: listeden yönetilen Google Play uygulamasını seçin.

      > [!IMPORTANT]
      > Tek uygulama bilgi noktası modu kullanılırken, çevirici/telefon uygulamaları düzgün çalışmayabilir.
  
    - **Çoklu uygulama**: kullanıcılar cihazdaki sınırlı bir uygulama kümesine erişebilir. Cihaz başlatıldığında yalnızca eklediğiniz uygulamalar başlatılır. Ayrıca, kullanıcıların açabilme bazı Web bağlantıları ekleyebilirsiniz. İlke uygulandığında, kullanıcılar giriş ekranında izin verilen uygulamalar için simgeler görür.

      > [!IMPORTANT]
      > Çok uygulamayla ayrılmış cihazlarda, Google Play [yönetilen giriş ekranı uygulamasının](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) şu **olması gerekir**:
      >   - [Intune 'A eklendi](../apps/apps-add-android-for-work.md)
      >   - Adanmış cihazlarınız için oluşturulan [cihaz grubuna atandı](../apps/apps-deploy.md)
      >
      > **Yönetilen giriş ekranı** uygulamasının yapılandırma profilinde olması gerekmez, ancak uygulama olarak eklenmesi gerekir. **Yönetilen giriş ekranı** uygulaması eklendiğinde, yapılandırma profiline eklediğiniz diğer uygulamalar **yönetilen giriş ekranı** uygulamasında simgeler olarak gösterilir.
      >
      > Birden çok uygulama bilgi noktası modu kullanılırken, çevirici/telefon uygulamaları düzgün çalışmayabilir.
      >
      > Yönetilen giriş ekranı hakkında daha fazla bilgi için bkz. [özel cihazlarda Microsoft yönetilen giriş ekranını çok uygulama bilgi noktası modunda ayarlama](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

      - **Ekle**: listeden uygulamalarınızı seçin.

        **Yönetilen giriş ekranı** uygulaması listede yoksa [Google Play ekleyin](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). Uygulamayı adanmış cihazlarınız için oluşturulan cihaz grubuna [atadığınızdan](../apps/apps-deploy.md) emin olun.

        Ayrıca, kuruluşunuz tarafından oluşturulan diğer [Android uygulamalarını](../apps/apps-add-android-for-work.md) ve [Web uygulamalarını](../apps/web-app.md) cihaza ekleyebilirsiniz. [Uygulamayı adanmış cihazlarınız için oluşturulan cihaz grubuna atadığınızdan](../apps/apps-deploy.md)emin olun.

      - **Klasör simgesi**: yönetilen giriş ekranında gösterilen klasör simgesinin rengini ve şeklini seçin. Seçenekleriniz şunlardır:
        - Yapılandırılmamış 
        - Koyu tema dikdörtgeni
        - Koyu tema çemberi
        - Açık tema dikdörtgeni
        - Açık tema çemberi
      - **Uygulama ve klasör simge boyutu**: yönetilen giriş ekranında gösterilen klasör simgesinin boyutunu seçin. Seçenekleriniz şunlardır:
        - Yapılandırılmamış 
        - Çok küçük
        - Küçük
        - Ortalama
        - Büyük
        - Çok büyük

          Ekran boyutuna bağlı olarak, gerçek simge boyutu farklı olabilir.

      - **Ekran yönü**: yönetilen giriş ekranının cihazlarda gösterildiği yönü seçin. Seçenekleriniz şunlardır:
        - Yapılandırılmamış
        - Dikey
        - Yatay
        - Oto döndür
      - **Uygulama bildirimi rozetleri**: **Etkinleştir** , uygulama simgelerindeki yeni ve okunmamış bildirimlerin sayısını gösterir. **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
      - **Sanal giriş düğmesi**: kullanıcıların uygulamalar arasında geçiş yapabilmesi Için kullanıcıları yönetilen giriş ekranına döndüren bir yazılım tuşu düğmesi. Seçenekleriniz şunlardır:
        - **Yapılandırılmadı** (varsayılan): Giriş düğmesi gösterilmez. Kullanıcıların, uygulamalar arasında geçiş yapmak için geri düğmesini kullanmaları gerekir.
        - **Yukarı çek**: bir giriş düğmesi, bir kullanıcının cihazda ne zaman yüzümü gösterdiğini gösterir.
        - **Kayan**: cihazda kalıcı, kayan bir giriş düğmesi gösterir.

      - **Bilgi noktası modundan çıkma**: **Etkinleştir** ayarı, yöneticilerin cihazı güncelleştirmek için bilgi noktası modunu geçici olarak duraklatmasını sağlar. Bu özelliği kullanmak için yönetici:
  
        1. **Çıkış bilgi noktası** düğmesi gösterilene kadar geri düğmesini seçmeye devam eder. 
        2. **Bilgi noktası çıkış** düğmesini seçer ve **bilgi noktası modu kod** PIN 'ini girer.
        3. İşiniz bittiğinde, **yönetilen giriş ekranı** uygulamasını seçin. Bu adım, cihazı çok uygulama bilgi noktası moduna yeniden kilitler.

        **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi yöneticilerin bilgi noktası modunu duraklatmasını önleyebilir. Yönetici geri düğmesini seçip, **bilgi noktası çıkışı** düğmesini seçerse bir ileti geçiş kodunun gerekli olduğunu belirtir.

      - **Bilgi noktası modu kodunu bırak**: 4-6 basamaklı sayısal bir PIN girin. Yönetici bilgi noktası modunu geçici olarak duraklatmak için bu PIN 'ı kullanır.

      - **Özel URL arka planı ayarla**: adanmış cihazda arka plan ekranını özelleştirmek IÇIN bir URL girin. Örneğin, `http://contoso.com/backgroundimage.jpg` girin.

        > [!NOTE]
        > Çoğu durumda, en az aşağıdaki boyutlardaki görüntülerle başlamasını öneririz:
        >
        > - Telefon: 1080x1920 px
        > - Tablet: 1920x1080 px
        >
        > En iyi deneyim ve ayrıntılı Ayrıntılar için, görüntüleme belirtimlerine cihaz başına görüntü varlıkları oluşturulması önerilir.
        >
        > Modern görüntüler, daha yüksek piksel yoğunluklarını ve eşdeğer 2K/4K tanım görüntülerini görüntüleyebilir.

      - **Ayarlar menüsü kısayolu**: **devre dışı bırak** ayarı, yönetilen giriş ekranında yönetilen ayarlar kısayolunu gizler. Kullanıcılar, ayarlara erişmek için yine de aşağı doğru çekerek bulunabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, yönetilen ayarlar kısayolu cihazlarda gösterilir. Kullanıcılar ayrıca bu ayarlara erişmek için aşağı doğru da çekerek bulunabilir.

      - **Hata ayıklama menüsüne hızlı erişim**: Bu ayar, kullanıcıların hata ayıklama menüsüne nasıl erişdiğini denetler. Seçenekleriniz şunlardır:

        - **Etkinleştir**: kullanıcılar hata ayıklama menüsüne daha kolay erişebilir. Özellikle, bir daha aşağı çekerek veya yönetilen ayarlar kısayolunu kullanabilirler. Her zaman olduğu gibi, geri düğmesini 15 kez seçerken devam edebilirler.
        - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, hata ayıklama menüsüne kolay erişim kapalıdır. Kullanıcılar hata ayıklama menüsünü açmak için 15 kez geri düğmesini seçmelidir.

        Hata ayıklama menüsünü kullanarak, kullanıcılar şunları yapabilir:

        - Yönetilen giriş ekranı günlüklerine bakın ve karşıya yükleyin
        - Google 'ın Android cihaz Ilkesi Yöneticisi uygulamasını açın
        - [Microsoft Intune uygulamasını](https://play.google.com/store/apps/details?id=com.microsoft.intune) açın
        - Bilgi noktası modundan çık

      - **Wi-Fi yapılandırması**: **Etkinleştir** ayarı, yönetilen giriş ekranında Wi-Fi denetimini gösterir ve kullanıcıların cihazı farklı WiFi ağlarına bağlanmasına izin verir. Bu özelliği etkinleştirmek Ayrıca cihaz konumunu da etkinleştirir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, yönetilen giriş ekranında Wi-Fi denetimini göstermeyebilir. Kullanıcıların, yönetilen giriş ekranını kullanırken Wi-Fi ağlarına bağlanmasını engeller.

        - **Wi-Fi izin verilenler listesi**: hizmet kümesi tanımlayıcısı (SSID) olarak da bilinen geçerli bir kablosuz ağ adları listesi oluşturun. Yönetilen giriş ekranı kullanıcıları yalnızca girdiğiniz SSID 'ler ile bağlanabilir.

          Boş bırakılırsa, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, tüm kullanılabilir Wi-Fi ağlarına izin verilir.

          Geçerli SSID 'ler listesini içeren bir. csv dosyasını **Içeri aktarın** .

          Geçerli listenizi bir. csv dosyasına **dışarı aktarın** .

        - **SSID**: Ayrıca, yönetilen giriş ekranı kullanıcılarının bağlanabileceği Wi-Fi ağ ADLARıNı (SSID) da girebilirsiniz. Geçerli SSID 'leri girdiğinizden emin olun.

      - **Bluetooth yapılandırması**: **Etkinleştir** ayarı, yönetilen giriş ekranında Bluetooth denetimini gösterir ve kullanıcıların cihazları Bluetooth üzerinden eşleştirmesine olanak tanır. Bu özelliği etkinleştirmek Ayrıca cihaz konumunu da etkinleştirir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi yönetilen giriş ekranında Bluetooth denetimini göstermeyebilir. Yönetilen giriş ekranını kullanırken kullanıcıların Bluetooth ve eşleme cihazlarını yapılandırmalarını engeller.

      - **El feneri erişimi**: **Enable** , yönetilen giriş ekranında el feneri denetimini gösterir ve kullanıcıların el feneri 'i açmasına veya kapamesine olanak tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, yönetilen giriş ekranında el feneri denetimini göstermeyebilir. Yönetilen giriş ekranını kullanırken kullanıcıların el feneri kullanmasını engeller.

      - **Media Volume Control**: **Enable** ayarı, yönetilen giriş ekranında medya birimi denetimini gösterir ve kullanıcıların bir kaydırıcı kullanarak cihazın medya birimini ayarlamasına olanak tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, yönetilen giriş ekranında medya birimi denetimini göstermeyebilir. Kullanıcıların, donanım düğmeleri onu desteklemediği sürece, yönetilen giriş ekranını kullanırken cihazın medya hacmini değiştirmesini engeller.

      - **Cihaz bilgilerine hızlı erişim**: **Etkinleştir** ayarı, kullanıcıların seri numarası, oluşturma ve model numarası ve SDK düzeyi gibi yönetilen giriş ekranında cihaz bilgilerini görmesini sağlar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, cihaz bilgileri gösterilmeyebilir.

      - **Ekran koruyucu modu**: **Etkinleştir** , cihaz kilitlendiğinde veya zaman aşımına uğrarsa yönetilen giriş ekranında bir ekran koruyucu gösterir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, yönetilen giriş ekranında bir ekran koruyucu gösterme gösterebilir.

        Etkinleştirildiğinde, şunları da yapılandırın:

        - **Özel ekran koruyucu görüntüsünü ayarla**: özel bir PNG, jpg, JPEG, GIF, BMP, WEBP veya ııMAGE URL 'sini girin. Bir URL girmezseniz, varsayılan bir görüntü varsa cihazın varsayılan görüntüsü kullanılır.

          Örneğin şunu girin: 

          - `http://www.contoso.com/image.jpg`
          - `www.contoso.com/image.bmp`
          - `https://www.contoso.com/image.webp`

          > [!TIP]
          > Bit eşlemde açılabilir herhangi bir dosya kaynağı URL 'SI desteklenir.

        - **Cihazın ekranı kapatmadan önce ekran koruyucuyu gösterdiği saniye sayısı**: cihazın ekran koruyucuyu ne kadar süreyle gösterdüğüne seçin. 0-9999999 saniye arasında bir değer girin. Varsayılan değer `0` saniyedir. Boş bırakıldığında veya sıfır () olarak ayarlandığında `0` , Kullanıcı cihazla etkileşime gelinceye kadar ekran koruyucusu etkin olur.
        - **Ekran koruyucuyu göstermeden önce cihazın etkin olmadığı saniye sayısı**: ekran koruyucuyu göstermeden önce cihazın ne kadar süreyle boşta kalacağını seçin. 1-9999999 saniye arasında bir değer girin. Varsayılan değer `30` saniyedir. Sıfırdan büyük bir sayı girmeniz gerekir ( `0` ).
        - **Ekran koruyucuyu başlatmadan önce medyayı Algıla**: cihazda ses veya video yürütülıyorsa, **Etkinleştir** (varsayılan) ekran koruyucuyu göstermez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, ses veya video oynatılsa bile ekran koruyucuyu gösterebilir.

- **Tam olarak yönetilen**: tam olarak yönetilen cihazlarda Microsoft Başlatıcı uygulamasını yapılandırır.

  - **Microsoft başlatıcısı 'nı varsayılan Başlatıcı yap**: **Enable** Microsoft başlatıcısı 'nı ana ekranda varsayılan başlatıcı olarak ayarlar. Başlatıcısı varsayılan olarak yaparsanız, kullanıcılar başka bir başlatıcı kullanamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, Microsoft Başlatıcısı varsayılan başlatıcı olarak zorunlu değildir.
  - **Özel duvar kağıdını yapılandırma**: **Etkinleştir** seçeneği, kendi görüntünüzü ana ekran duvar kağıdı olarak uygulamanıza olanak sağlar ve kullanıcıların görüntüyü değiştirip değiştireseçebilmelidir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak cihaz geçerli duvar kağıdını korur.
    - **Duvar kağıdı resminin URL 'Sini girin**: duvar KAĞıDı resminizin URL 'sini girin. Bu görüntüde cihaz giriş ekranında gösterilir. Örneğin, `http://www.contoso.com/image.jpg` girin. 
    - **Kullanıcının duvar kağıdını değiştirmesine Izin ver**: **Etkinleştir** ayarı, kullanıcıların duvar kağıdı görüntüsünü değiştirmesine izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, kullanıcıların duvar kağıdını değiştirmesi engellenir.
  - **Başlatıcı akışını etkinleştir**: **Etkinleştir** , takvimleri, belgeleri ve en son etkinlikleri gösteren Başlatıcı akışını etkinleştirir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Bu akış varsayılan olarak gösterilmez.
    - **Kullanıcının akışı etkinleştirmesine/devre dışı bırakmasına Izin ver**: **Etkinleştir** , kullanıcıların Başlatıcı akışını etkinleştirmesine veya devre dışı bırakmasına olanak sağlar **Etkinleştir** ayarı yalnızca profil atandığında bu ayarı zorlar. Gelecekteki tüm profil atamaları bu ayarı zorlamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, kullanıcıların Başlatıcı akış ayarlarını değiştirmesi engellenir.
  - **Takma varlığı**: yerleştirme kullanıcılara uygulamalarına ve araçlarına hızlı erişim sağlar. Seçenekleriniz şunlardır:
    - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Göster**: yerleştirme cihazlarda görüntülenir.
    - **Gizle**: Dock gizlenir. Kullanıcıların Dock 'a erişmesi için çekme yapmanız gerekir.
    - **Devre dışı**: yuva cihazlarda gösterilmez ve kullanıcıların bunu göstermesini engellemiş olur.

  - **Kullanıcının yuva varlığını değiştirmesine Izin ver**: **Etkinleştir** ayarı, kullanıcıların yerleştirmeyi göstermesini veya gizlemesini sağlar. **Etkinleştir** ayarı yalnızca profil atandığında bu ayarı zorlar. Gelecekteki tüm profil atamaları bu ayarı zorlamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, kullanıcıların cihaz yuva yapılandırmasını değiştirmesine izin verilmez.

  - **Arama çubuğu değiştirme**: arama çubuğunun nereye yerleştirileceğini seçin. Seçenekleriniz şunlardır:
    - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
    - **Üst**: arama çubuğu, cihazların en üstünde gösterilir.
    - **Alt**: arama çubuğu cihazların en altında gösterilir.
    - **Gizle**: arama çubuğu gizli.

<!-- MandiA (7.16.2020) The following settings may be in a future release. Per PM, we can leave it in GitHub, not live. Remove comment tags if/when it releases.
  - **Allow user to change search bar placement**: **Enable** allows users to change the location of the search bar. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the location.
End of comment -->

### <a name="password"></a>Parola

- **Kilit ekranını devre dışı bırak**: kullanıcıların cihazda keyguard kilit ekranı özelliğini kullanmalarını engellemek Için **devre dışı bırak** ' ı seçin. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların Keyguard özelliklerini kullanmasına izin verebilir.
- **Devre dışı kilit ekranı özellikleri**: cihazda keyguard etkinleştirildiğinde, hangi özelliklerin devre dışı bırakılacağını seçin. Örneğin, **güvenli kamera** işaretlendiğinde kamera özelliği cihazda devre dışı bırakılır. Denetlenmeyen tüm özellikler cihazda etkinleştirilir.

  Bu özellikler, cihaz kilitlendiğinde kullanıcılar tarafından kullanılabilir. Kullanıcılar işaretli özellikleri göremez veya erişemez.

- **Gerekli parola türü**: gerekli parola karmaşıklığı düzeyini ve biyometrik cihazların kullanılıp kullanılamayacağını girin. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı**
  - **Parola gerekli, kısıtlama yok**
  - **Zayıf biyometrik**: [güçlü ve zayıf Biyometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (Android 'in Web sitesini açar)
  - **Sayısal**: parola yalnızca sayı olmalıdır, örneğin `123456789` . Şunları da girin:
    - **Minimum parola uzunluğu**: parolanın, 4 ile 16 karakter arasında olması gereken minimum uzunluğu girin.
  - **Sayısal karmaşık**: "1111" veya "1234" gibi yinelenen veya ardışık numaralara izin verilmez. Şunları da girin:
    - **Minimum parola uzunluğu**: parolanın, 4 ile 16 karakter arasında olması gereken minimum uzunluğu girin.
  - **Alfabetik**: alfabedeki harfler gereklidir. Rakamlar ve simgeler zorunlu tutulmaz. Şunları da girin:
    - **Minimum parola uzunluğu**: parolanın, 4 ile 16 karakter arasında olması gereken minimum uzunluğu girin.
  - **Alfasayısal**: büyük harfler, küçük harfler ve sayısal karakterler içerir. Şunları da girin:
    - **Minimum parola uzunluğu**: parolanın, 4 ile 16 karakter arasında olması gereken minimum uzunluğu girin.
  - **Simgelerle alfasayısal**: büyük harfler, küçük harfler, sayısal karakterler, noktalama işaretleri ve semboller içerir. Şunları da girin:

    - **Minimum parola uzunluğu**: parolanın, 4 ile 16 karakter arasında olması gereken minimum uzunluğu girin.
    - **Gerekli karakter sayısı**: parolanın, 0 ile 16 karakter arasında olması gereken karakter sayısını girin.
    - **Gereken küçük harfli karakter sayısı**: parolanın, 0 ile 16 karakter arasında olması gereken küçük harfli karakter sayısını girin.
    - **Gerekli olan büyük harfli karakter sayısı**: parolanın, 0 ile 16 karakter arasında olması gereken büyük harfli karakter sayısını girin.
    - **Gerekli harf olmayan karakter sayısı**: parolanın, 0 ile 16 karakter arasında olması gereken harf olmayan karakter sayısını (alfabedeki harfler dışında bir şey) girin.
    - **Gerekli sayısal karakter sayısı**: `1` `2` `3` parolanın 0 ile 16 karakter arasında olması gereken sayısal karakter (,, vb.) sayısını girin.
    - **Gerekli simge karakter sayısı**: `&` `#` `%` parolanın 0 ile 16 karakter arasında olması gereken simge karakterlerinin (,, vb.) sayısını girin.

- **Parolanın süresi dolana kadar geçen gün sayısı**: 1-365 adresinden cihaz parolasının değiştirilmesi gereken gün sayısını girin. Örneğin, `90` 90 gün sonra parolanın süresini dolacak şekilde girin. Parola geçerlilik süresi dolduğunda kullanıcıların yeni bir parola oluşturması istenir. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Kullanıcının bir parolayı yeniden kullanabilmesi için gereken parola sayısı**: Bu ayarı, kullanıcıların önceden kullanılan parolaları oluşturmasını kısıtlamak için kullanın. 1-24 adresinden, daha önce kullanılmış olan parolaların sayısını girin. Örneğin, `5` kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: cihaz temizlenmeden önce izin verilen hatalı parola sayısını 4-11 adresinden girin. `0`(sıfır) cihaz temizleme işlevini devre dışı bırakabilir. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.

  > [!NOTE]
  > Tam olarak yönetilen, adanmış ve şirkete ait iş profili cihazlarının bir parola ayarlaması istenmez. Ayarlar zorunlu kılınır ve parolayı el ile ayarlamanız gerekir. Gereksinimlerinizi karşılayan parolayı ayarlayıp, bunu uygulayan ilke başarısız olarak rapor eder.

### <a name="power-settings"></a>Güç ayarları

- **Kilit süresi ekranı**: bir kullanıcının cihaz kilitlenmeden önce ayarlayabilen en uzun süreyi girin. Örneğin, bu ayarı olarak ayarlarsanız `10 minutes` , kullanıcılar süreyi 15 saniye ila 10 dakikaya ayarlayabilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Cihaz prize takılıyken ekran açık**: Cihaz prize takılıyken hangi güç kaynaklarının ekranın açık kalmasına neden olacağını seçin.

### <a name="users-and-accounts"></a>Kullanıcılar ve hesaplar

- **Yeni Kullanıcı Ekle**: **Engelle** , kullanıcıların yeni kullanıcı eklemesini engeller. Her Kullanıcı, cihazda özel giriş ekranları, hesaplar, uygulamalar ve ayarlar için bir kişisel alana sahiptir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihaza başka kullanıcılar eklemesine izin verebilir.
- **Kullanıcı kaldırma**: **Block** kullanıcıların kullanıcıları kaldırmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazdan diğer kullanıcıları kaldırmasına izin verebilir.
- **Hesap değişiklikleri** (yalnızca adanmış cihazlar): **blok** kullanıcıların hesapları değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların cihazdaki kullanıcı hesaplarını güncelleştirmesine izin verebilir.

  > [!NOTE]
  > Bu ayar, tam olarak yönetilen, adanmış ve şirkete ait iş profili cihazlarında kabul edilemez. Bu ayarı yapılandırırsanız, ayar yok sayılır ve herhangi bir etkisi yoktur.

- **Kullanıcı kimlik bilgilerini yapılandırabilir**: **blok** kullanıcıların cihazlara atanan sertifikaları yapılandırmalarını, hatta bir kullanıcı hesabı ile ilişkilendirilmemiş cihazları değiştirmesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi, kullanıcıların anahtar deposunda bunlara erişirken kimlik bilgilerini yapılandırmasını veya değiştirmesini mümkün hale getirir.
- **Kişisel Google hesapları**: **Block** , kullanıcıların kişisel Google hesabını cihaza eklemesini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların kişisel Google hesabını eklemesine izin verebilir.

### <a name="applications"></a>Uygulamalar

- **Bilinmeyen kaynaklardan yüklemeye Izin ver**: **izin ver** , kullanıcıların **Bilinmeyen kaynakları**kullanmasına izin verir. Bu ayar, uygulamaların Google Play Store dışındaki kaynaklar da dahil olmak üzere bilinmeyen kaynaklardan yüklenmesine izin verir. Kullanıcıların cihazdaki uygulamaları Google Play Store dışındaki yollarla dışarıdan yüklemesine olanak tanır. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların **Bilinmeyen kaynakları**açmasını önleyebilir.
- **Google Play Store 'daki tüm uygulamalara erişime Izin ver**: **izin ver**olarak ayarlandığında, kullanıcılar Google Play deposundaki tüm uygulamalara erişim sağlar. [Istemci uygulamalarında](../apps/apps-add-android-for-work.md)yönetici blokları olan uygulamalara erişim almaz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi şunları içerebilir:
  
  - Kullanıcıları yalnızca yöneticinin Google Play deposunda veya [Istemci uygulamalarında](../apps/apps-add-android-for-work.md)gerekli olan uygulamalarda kullanılabilir hale getiren uygulamalara erişmelerini zorunlu kılın. 
  - Google Play deposu dışındaki kullanıcılar tarafından yüklendiği algılanan tüm uygulamaları otomatik olarak kaldırın.

  Dışarıdan yüklemeyi etkinleştirmek istiyorsanız, **Bilinmeyen kaynaklardan yüklemeyi Izin ver** ' i ayarlayın ve **Google Play Mağaza ayarlarındaki tüm uygulamalara** **izin ver**' e erişime izin verin.

- **Uygulama otomatik güncelleştirmeleri**: cihazlar uygulama güncelleştirmelerini günlük olarak denetler. Otomatik güncelleştirmelerin ne zaman yükleneceğini seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı**: Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Kullanıcı tercihi**: işletim sistemi bu seçenek için varsayılan olarak değişebilir. Kullanıcılar, yönetilen Google Play uygulamasında tercihlerini ayarlayabilir.
  - **Hiçbir**koşulda: güncelleştirmeler hiçbir şekilde yüklenmez. Bu seçenek önerilmez.
  - **Yalnızca Wi-Fi**: Güncelleştirmeler yalnızca cihaz bir Wi-Fi ağına bağlıyken yüklenir.
  - **Her zaman**: güncelleştirmeler kullanılabilir olduğunda yüklenir.

### <a name="connectivity"></a>Bağlantı

- **Her zaman-on VPN**: **Enable** VPN ISTEMCISINI otomatik olarak bağlanıp VPN 'ye yeniden bağlanacak şekilde ayarlar. Her zaman açık VPN bağlantıları bağlı kalır. Ya da kullanıcılar cihazlarını kilitlediğimde, cihaz yeniden başlatıldığında veya kablosuz ağ değişikliklerinden hemen bağlanabilirsiniz.

  Her zaman açık VPN'yi tüm VPN istemcilerinde devre dışı bırakmak için **Yapılandırılmadı**'yı seçin.

  > [!IMPORTANT]
  > Tek bir cihaza yalnızca bir adet her zaman açık VPN ilkesi dağıttığınızdan emin olun. Birden çok her sürekli VPN ilkesinin tek bir cihaza dağıtımı desteklenmez.

- **VPN istemcisi**: Her Zaman Açık'ı destekleyen bir VPN istemcisini seçin. Seçenekleriniz şunlardır:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Özel
    - **Paket kimliği**: Google Play mağazasına uygulamanın paket kimliğini girin. Örneğin Play mağazasındaki uygulamanın URL'si `https://play.google.com/store/details?id=com.contosovpn.android.prod` ise, paket kimliği `com.contosovpn.android.prod` olur.

  > [!IMPORTANT]
  > - Seçtiğiniz VPN istemcisinin cihaza yüklenmesi ve cihazın uygulama başına VPN iş profillerini desteklemesi gerekir. Aksi takdirde bir hata oluşur. 
  > - VPN istemci uygulamasını yine de **Yönetilen Google Play Mağazası**'nda onaylamanız, uygulamayı Intune ile eşitlemeniz ve cihaza dağıtmanız gerekir. Bu yapıldıktan sonra uygulama kullanıcının iş profiline yüklenir.
  > - VPN istemcisini yine de bir [VPN profiliyle](vpn-settings-android-enterprise.md)veya bir [uygulama yapılandırma profilinde](../apps/app-configuration-policies-use-android.md)yapılandırmanız gerekir.
  > - Android 3.0.4 için F5 Access ile uygulama başına VPN kullanılırken bilinen sorunlar olabilir. Daha fazla bilgi için bkz. [F5's sürüm notları Android 3.0.4 Için F5 Access](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Kilitleme modu**: **Etkinleştir** ayarı, tüm ağ trafiğini VPN tünelini kullanacak şekilde zorlar. VPN'e bir bağlantı oluşturulmazsa, cihazın ağ erişimi olmaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi trafiğin VPN tüneli üzerinden veya mobil ağ aracılığıyla akışa eklenmesine izin verebilir.

- **Önerilen genel proxy**: **Enable** cihazlara genel bir proxy ekler. Etkinleştirildiğinde, HTTP ve HTTPS trafiği, cihazdaki bazı uygulamalar dahil olmak üzere girdiğiniz proxy 'yi kullanır. Bu proxy yalnızca bir önerimiz. Bazı uygulamalar proxy kullanmaz. **Yapılandırılmadı** (varsayılan) önerilen küresel ara sunucu eklemez.

  Bu özellik hakkında daha fazla bilgi için bkz. [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (bir Android sitesi açar).

  Etkinleştirildiğinde, proxy **türünü** de girin. Seçenekleriniz şunlardır:

  - **Doğrudan**: aşağıdakiler dahil olmak üzere proxy sunucu ayrıntılarını el ile girin:
    - **Ana bilgisayar**: proxy sunucunuzun ana bilgisayar adını veya IP adresini girin. Örneğin `proxy.contoso.com` veya `127.0.0.1` girin.
    - **Bağlantı noktası numarası**: proxy sunucusu tarafından kullanılan TCP bağlantı noktası numarasını girin. Örneğin, `8080` girin.
    - **Dışlanan konaklar**: proxy 'yi kullanmayan konak ADLARıNıN veya IP adreslerinin bir listesini girin. Bu liste, boşluk olmadan bir yıldız işareti ( `*` ) joker karakteri ve noktalı virgül () ile ayrılmış birden çok ana bilgisayar içerebilir `;` . Örneğin, `127.0.0.1;web.contoso.com;*.microsoft.com` girin.

  - **Proxy otomatik yapılandırma**: bir proxy otomatik yapılandırma betiğine **Pac URL 'sini** girin. Örneğin, `https://proxy.contoso.com/proxy.pac` girin.

    PAC dosyaları hakkında daha fazla bilgi için bkz. [proxy otomatik yapılandırma (PAC) dosyası](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (Microsoft dışı bir site açar).

  Bu özellik hakkında daha fazla bilgi için bkz. [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (bir Android sitesi açar).

## <a name="work-profile-only"></a>Yalnızca iş profili

Bu ayarlar, Intune 'un yalnızca bir kişisel veya kendi cihazındaki (BYOD) Android kurumsal Iş profili kaydı gibi Iş profilini denetlediği Android kurumsal kayıt türleri için geçerlidir.

### <a name="work-profile-settings"></a>İş profili ayarları

- **İş ve kişisel profiller arasında kopyalama ve yapıştırma**: **blok** , iş ve kişisel uygulamalar arasında kopyalama ve yapıştırmayı önler. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, kullanıcıların kişisel profildeki uygulamalarla Kopyala ve yapıştır işlemlerini kullanarak veri paylaşmasına izin verebilir.
- **İş ve kişisel profiller arasında veri paylaşımı**: iş profilindeki uygulamaların kişisel profildeki uygulamalarla paylaşıp paylaşabilmesini seçin. Örneğin, uygulamalar içinde paylaşım eylemlerini (paylaşım gibi) denetleyebilirsiniz **...** seçeneği gibi uygulamalardaki paylaşma eylemlerini denetler. Bu ayar, kopyala/yapıştır pano davranışında geçerli değildir. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı**: cihazın varsayılan paylaşım davranışı, Android sürümüne bağlı olarak farklılık gösterir:
    - Android 6,0 ve üzeri sürümlerde çalışan cihazlarda, iş profilinden kişisel profile paylaşım engellenir. Kişisel profilden iş profiline paylaşıma izin verilir.
    - Android 5,0 ve üzeri sürümleri çalıştıran cihazlarda, iş profili ve kişisel profil arasında paylaşım her iki yönde de engellenir.
  - **İş profilindeki uygulamalar kişisel profilden gelen paylaşım isteklerini işleyebilir**: Kişisel profilden iş profiline paylaşıma izin veren yerleşik Android özelliğini etkinleştirir. Etkinleştirildiğinde, kişisel profildeki bir uygulamadan gelen bir paylaşım isteği, iş profilindeki uygulamalarla paylaşım kullanabilir. Bu ayar, 6.0 öncesi sürümleri çalıştıran Android cihazlarının varsayılan davranışıdır.
  - **Paylaşımda kısıtlama yok**: iş profili sınırları genelinde her iki yönde paylaşımı mümkün değildir. Bu ayarı seçtiğinizde, iş profilinizdeki uygulamalar kişisel profildeki rozetsiz uygulamalar ile veri paylaşabilir. Bu ayar iş profilindeki yönetilen uygulamaların cihazın yönetilmeyen kısmındaki uygulamalarla paylaşmasına izin verir. Bu nedenle bu ayarı dikkatli kullanın.

- **Cihaz kilitliyken iş profili bildirimleri**: **Engelle** , Kilitli cihazlarda gösterilmeleri, gelen çağrılar, giden çağrılar, sistem uyarıları ve sistem hataları dahil olmak üzere pencere bildirimlerini engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bildirimleri gösterebilir.
- **Varsayılan uygulama izinleri**: İş profilindeki tüm uygulamalar için varsayılan izin ilkesini ayarlar. Android 6 ' dan itibaren, kullanıcılardan uygulama başlatıldığında uygulamalar için gereken belirli izinleri vermesi istenir. Bu ilke ayarı, kullanıcıdan iş profilindeki tüm uygulamalar için izin istenip istenmeyeceğini belirlemenize olanak tanır. Örneğin, iş profiline konum erişimi gerektiren bir uygulama atarsınız. Normalde bu uygulama, kullanıcılardan uygulamaya konum erişimini onaylaması veya reddetmesini ister. Bu ilkeyi, istem olmadan otomatik olarak izin vermek, bir istem olmadan izinleri otomatik olarak reddetmek veya kullanıcıların karar vermesine izin vermek için kullanın. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı**
  - **İstem**
  - **Otomatik izin ver**
  - **Otomatik Reddet**

  Tek tek uygulamalara (**istemci uygulamaları**  >  **uygulama yapılandırma ilkeleri**) izin vermek için bir uygulama yapılandırma ilkesi de kullanabilirsiniz.

- **Hesap ekleme ve kaldırma**: **engelleme** , kullanıcıların iş profilinde hesapları el ile eklemesini veya kaldırmasını engeller. Örneğin, Gmail uygulamasını bir Android iş profiline dağıttığınızda, kullanıcıların bu iş profilinde hesap eklemesini veya kaldırmasını engelleyebilirsiniz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak işletim sistemi, iş profilinde hesap eklemeye izin verebilir.  

  > [!NOTE]
  > Google hesapları bir iş profiline eklenemez.

- **Bluetooth aracılığıyla kişi paylaşımı**: **etkinleştirme** , Bluetooth ile eşleştirilmiş bir otomobil dahil olmak üzere başka bir cihazdan iş profili kişilerine paylaşım ve erişim olanağı sağlar. Bu ayarı etkinleştirmek, bazı Bluetooth cihazlarının ilk bağlantı sırasında iş kişilerini önbelleğe almasına izin verebilir. İlk eşleme/eşitleme sonrasına bunu devre dışı bırakmak ise Bluetooth cihazından iş kişilerini kaldırmayabilir.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iş kişilerini paylaşmayabilir.

  Bu ayarın geçerli olduğu sürümler:

  - Android OS v 6.0 ve daha yenisini çalıştıran Android iş profili cihazları

- **Ekran yakalama**: **blok** , iş profilindeki cihazdaki ekran görüntülerini veya ekran yakalamalarını engeller. Ayrıca güvenli bir video çıkışına sahip olmayan görüntü cihazlarında gösterilen içeriği engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi ekran görüntülerini almaya izin verebilir.

- **Kişisel profilde iş kişisi arayan kimliğini görüntüle**: **blok** , kişisel profilde iş iletişim arayan numarasını göstermez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi iş iletişim çağıranı ayrıntılarını gösterebilir.

  Bu ayarın geçerli olduğu sürümler:

  - Android OS v 6.0 ve daha yeni sürümler

- **Kişisel profilden iş kişileri ara**: **Engelle** , kullanıcıların kişisel profildeki uygulamalarda iş kişilerini aramasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kişisel profilde iş kişileri aramasına izin verebilir.

- **Kamera**: **Engelle** , iş profilindeki cihazdaki kameraya erişimi engeller. Kişisel taraftaki kamera, bu ayardan etkilenmez. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kameraya erişime izin verebilir.

- **İş profili uygulamalarından Pencere öğelerinin oluşturulmasına Izin ver**: **Etkinleştir** ayarı, kullanıcıların, ana ekranda uygulamalar tarafından açığa çıkarılan pencere öğelerini almasına izin verir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi bu özelliği devre dışı bırakabilir.

  Örneğin, Outlook kullanıcılarınızın iş profillerine yüklendi. **Etkin**olarak ayarlandığında, kullanıcılar gündem pencere öğesini cihaz giriş ekranına yerleştirebilir.

- **Iş profili parolası gerektir**: **gerektir** , yalnızca iş profilindeki uygulamalar için geçerli olan bir geçiş kodu ilkesini zorlar. Varsayılan olarak, kullanıcılar ayrı olarak tanımlanan iki PIN 'i kullanabilir. Ya da, kullanıcılar PIN 'leri iki PIN 'in daha güçlü bir şekilde birleştirebilir. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parola girmeden iş uygulamalarını kullanmasına izin verebilir.

  Bu ayarın geçerli olduğu sürümler:

  - İş profili etkin olan Android 7,0 ve üzeri

- **Minimum parola uzunluğu**: parolanın, 4 ile 16 karakter arasında olması gereken minimum uzunluğu girin.
- **İş profili kilitlenmeden önce geçen işlem yapılmayan dakika sayısı**: ekran otomatik olarak kilitlenmeden önce cihazların boşta olması gereken sürenin uzunluğunu girin. Kullanıcıların, erişimi yeniden kazanmak için kimlik bilgilerini girmesi gerekir. Örneğin, `5` 5 dakika boşta kaldıktan sonra cihazı kilitlemek için yazın. Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Cihazlarda, kullanıcılar profilde yapılandırılan süreden daha büyük bir zaman değeri ayarlayamamakta. Kullanıcılar, daha düşük bir saat değeri ayarlayabilir. Örneğin, profil dakikalar olarak ayarlandıysa `15` , kullanıcılar değeri 5 dakikaya ayarlayabilirler. Kullanıcılar değeri 30 dakika olarak ayarlayamıyorum.

- **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: cihaz temizlenmeden önce izin verilen hatalı parola sayısını 4-11 adresinden girin. `0`(sıfır) cihaz temizleme işlevini devre dışı bırakabilir. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Parola kullanım süresi (gün)**: kullanıcı parolalarının değiştirilmesi gereken gün sayısını girin ( **1** - **365**arasında).
- **Gerekli parola türü**: gerekli parola karmaşıklığı düzeyini ve biyometrik cihazların kullanılıp kullanılamayacağını girin. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı**
  - **Düşük güvenlik Biyometri**: [güçlü ve zayıf Biyometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (Android 'in Web sitesini açar)
  - **Gerekli**
  - **En az sayısal**: gibi sayısal karakterler içerir `123456789` .
  - **Sayısal karmaşık**: veya gibi yinelenen veya ardışık numaralara `1111` `1234` izin verilmez.
  - En **az alfabetik**: alfabede harfler içerir. Rakamlar ve simgeler zorunlu tutulmaz.
  - En **az alfasayısal**: büyük harfler, küçük harfler ve sayısal karakterler içerir.
  - **Semboller ile en az alfasayısal**: büyük harfler, küçük harfler, sayısal karakterler, noktalama işaretleri ve semboller içerir.

- **Önceki parolaların yeniden kullanılmasını engelle**: kullanıcıların daha önce kullanılan parolaları oluşturmasını kısıtlamak için bu ayarı kullanın. 1-24 adresinden, daha önce kullanılmış olan parolaların sayısını girin. Örneğin, `5` kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Parmak iziyle kilit açma**: **engelleme** , kullanıcıların cihazın kilidini açmak için cihaz parmak izi tarayıcısını kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parmak izi kullanarak cihazın kilidini açmalarını sağlayabilir.
- **Akıllı kilit ve diğer güven aracıları**: **blok** akıllı kilit veya diğer güven aracılarının uyumlu cihazlarda kilit ekranı ayarlarını değiştirmesini engeller. Cihazlar güvenilir bir konumdayken, güven aracısı olarak da bilinen bu özellik, cihaz kilit ekranı parolasını devre dışı bırakmanıza veya atlamanıza izin verir. Örneğin, cihazlar belirli bir Bluetooth cihazına bağlıyken veya cihazlar bir NFC etiketine yakın olduğunda iş profili parolasını atlayın. Bu ayarı, kullanıcıların Akıllı Kilit'i yapılandırmasını önlemek için kullanın.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

### <a name="password"></a>Parola

Bu parola ayarları, bir iş profili kullanan cihazlardaki kişisel profiller için geçerlidir.

- **Minimum parola uzunluğu**: parolanın, 4 ile 16 karakter arasında olması gereken minimum uzunluğu girin.
- Ekran **kilitlenmeden önce geçen işlem yapılmayan dakika sayısı**: ekran otomatik olarak kilitlenmeden önce cihazların boşta olması gereken sürenin uzunluğunu girin. Kullanıcıların, erişimi yeniden kazanmak için kimlik bilgilerini girmesi gerekir. Örneğin, `5` 5 dakika boşta kaldıktan sonra cihazı kilitlemek için yazın. Değer boş olduğunda veya **Yapılandırılmadı**olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Cihazlarda, kullanıcılar profilde yapılandırılan süreden daha büyük bir zaman değeri ayarlayamamakta. Kullanıcılar, daha düşük bir saat değeri ayarlayabilir. Örneğin, profil dakikalar olarak ayarlandıysa `15` , kullanıcılar değeri 5 dakikaya ayarlayabilirler. Kullanıcılar değeri 30 dakika olarak ayarlayamıyorum.

- **Cihaz silinmeden önceki oturum açma hatalarının sayısı**: cihaz temizlenmeden önce izin verilen hatalı parola sayısını 4-11 adresinden girin. `0`(sıfır) cihaz temizleme işlevini devre dışı bırakabilir. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Parola kullanım süresi (gün)**: cihaz parolasının, 1-365 adresinden değiştirilinceye kadar gün sayısını girin. Örneğin, `90` 90 gün sonra parolanın süresini dolacak şekilde girin. Parola geçerlilik süresi dolduğunda kullanıcıların yeni bir parola oluşturması istenir. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Gerekli parola türü**: gerekli parola karmaşıklığı düzeyini ve biyometrik cihazların kullanılıp kullanılamayacağını girin. Seçenekleriniz şunlardır:
  - **Cihaz varsayılanı**
  - **Düşük güvenlik Biyometri**: [güçlü ve zayıf Biyometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (Android 'in Web sitesini açar)
  - **Gerekli**
  - **En az sayısal**: gibi sayısal karakterler içerir `123456789` .
  - **Sayısal karmaşık**: veya gibi yinelenen veya ardışık numaralara `1111` `1234` izin verilmez.
  - En **az alfabetik**: alfabede harfler içerir. Rakamlar ve simgeler zorunlu tutulmaz.
  - En **az alfasayısal**: büyük harfler, küçük harfler ve sayısal karakterler içerir.
  - **Semboller ile en az alfasayısal**: büyük harfler, küçük harfler, sayısal karakterler, noktalama işaretleri ve semboller içerir.

- **Önceki parolaların yeniden kullanılmasını engelle**: kullanıcıların daha önce kullanılan parolaları oluşturmasını kısıtlamak için bu ayarı kullanın. 1-24 adresinden, daha önce kullanılmış olan parolaların sayısını girin. Örneğin, `5` kullanıcıların geçerli parolasına veya önceki dört parolalarından birine yeni bir parola ayarlayamaması için girin. Değer boş olduğunda, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Parmak iziyle kilit açma**: **engelleme** , kullanıcıların cihazın kilidini açmak için cihaz parmak izi tarayıcısını kullanmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kullanıcıların bir parmak izi kullanarak cihazın kilidini açmalarını sağlayabilir.
- **Akıllı kilit ve diğer güven aracıları**: **blok** akıllı kilit veya diğer güven aracılarının uyumlu cihazlarda kilit ekranı ayarlarını değiştirmesini engeller. Cihazlar güvenilir bir konumdayken, güven aracısı olarak da bilinen bu özellik, cihaz kilit ekranı parolasını devre dışı bırakmanıza veya atlamanıza izin verir. Örneğin, cihazlar belirli bir Bluetooth cihazına bağlıyken veya cihazlar bir NFC etiketine yakın olduğunda iş profili parolasını atlayın. Bu ayarı, kullanıcıların Akıllı Kilit'i yapılandırmasını önlemek için kullanın.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

### <a name="system-security"></a>Sistem güvenliği

- **Uygulamalarda tehdit taraması**: **gerekli** , Iş ve kişisel profillerde **uygulamaları doğrula** ayarının etkinleştirilmesini zorunlu kılar. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

  Bu ayarın geçerli olduğu sürümler:

  - Android 8 (Oreo) ve üzeri

- **Kişisel profilde bilinmeyen kaynaklardan uygulama yüklemelerini engelleyin**: tasarım, Android kurumsal iş profili cihazları Play Store dışındaki kaynaklardan uygulama yükleyemez. Bu ayar, yöneticilerin bilinmeyen kaynaklardan uygulama yüklemelerinin daha fazla denetimine erişmesini sağlar. **Block** , kişisel profildeki Google Play Store dışındaki kaynaklardan uygulama yüklemelerinin yapılmasını engeller. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi kişisel profilde bilinmeyen kaynaklardan uygulama yüklemelerine izin verebilir. Doğası gereği, iş profili cihazlarının çift profil olması amaçlanmıştır:

  - MDM kullanılarak yönetilen bir iş profili.
  - MDM yönetiminden yalıtılmış bir kişisel profil.

### <a name="connectivity"></a>Bağlantı

- **Her zaman-on VPN**: **Enable** VPN ISTEMCISINI otomatik olarak bağlanıp VPN 'ye yeniden bağlanacak şekilde ayarlar. Her zaman açık VPN bağlantıları bağlı kalır. Ya da kullanıcılar cihazlarını kilitlediğimde, cihaz yeniden başlatıldığında veya kablosuz ağ değişikliklerinden hemen bağlanabilirsiniz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi tüm VPN istemcileri için Always on VPN 'i devre dışı bırakabilir.

  > [!IMPORTANT]
  > Bir cihaza yalnızca bir tane Her Zaman Açık VPN ilkesi dağıttığınızdan emin olun. Bir cihaza birden çok Her Zaman Açık VPN ilkesi dağıtma desteklenmez.

- **VPN istemcisi**: Her Zaman Açık'ı destekleyen bir VPN istemcisini seçin. Seçenekleriniz şunlardır:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Özel
    - **Paket kimliği**: Google Play mağazasına uygulamanın paket kimliğini girin. Örneğin Play mağazasındaki uygulamanın URL'si `https://play.google.com/store/details?id=com.contosovpn.android.prod` ise, paket kimliği `com.contosovpn.android.prod` olur.

  > [!IMPORTANT]
  > - Seçtiğiniz VPN istemcisinin cihaza yüklenmesi ve cihazın uygulama başına VPN iş profillerini desteklemesi gerekir. Aksi takdirde bir hata oluşur.
  > - VPN istemci uygulamasını yine de **Yönetilen Google Play Mağazası**'nda onaylamanız, uygulamayı Intune ile eşitlemeniz ve cihaza dağıtmanız gerekir. Bu yapıldıktan sonra uygulama kullanıcının iş profiline yüklenir.
  > - Android 3.0.4 için F5 Access ile uygulama başına VPN kullanılırken bilinen sorunlar olabilir. Daha fazla bilgi için bkz. [Android Için F5 erişimi Için F5's sürüm notları 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android) .

- **Kilitleme modu**: **Etkinleştir** ayarı, tüm ağ trafiğini VPN tünelini kullanacak şekilde zorlar. VPN'e bir bağlantı oluşturulmazsa, cihazın ağ erişimi olmaz.

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez. Varsayılan olarak, işletim sistemi trafiğin VPN tüneli üzerinden veya mobil ağ aracılığıyla akışa eklenmesine izin verebilir.

## <a name="next-steps"></a>Sonraki adımlar

[Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).

Ayrıca, [Android](device-restrictions-android.md#kiosk) ve [Windows 10](kiosk-settings.md) cihazları için adanmış cihaz bilgi noktası profilleri oluşturabilirsiniz.

[Microsoft Intune 'de Android kurumsal cihazlarını yapılandırın ve sorunlarını giderin](https://support.microsoft.com/help/4476974).
