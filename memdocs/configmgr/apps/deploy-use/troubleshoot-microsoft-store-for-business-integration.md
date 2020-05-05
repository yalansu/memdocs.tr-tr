---
title: MSfB tümleştirmesinin sorunlarını giderme
titleSuffix: Configuration Manager
description: Iş ve eğitim tümleştirmesinde Microsoft Store en yaygın sorunların giderilmesine yönelik öneriler ve çözümler sağlar.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149106"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Configuration Manager ile Iş ve eğitim tümleştirmesi Microsoft Store sorunlarını giderin

Bu makalede, Configuration Manager Iş ve eğitim (MSfB) tümleştirmesi için Microsoft Store sahip olabilecek bazı başlıca sorunlar için temel sorun giderme ipuçları ve düzeltmeler sağlanmaktadır.

Configuration Manager ile Iş ve eğitim için Microsoft Store kullanma hakkında daha fazla bilgi için bkz. [Configuration Manager Ile iş ve eğitim için Microsoft Store uygulamaları yönetme](manage-apps-from-the-windows-store-for-business.md).

## <a name="monitor"></a>İzleme

### <a name="component-status"></a>Bileşen durumu

Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **sistem durumu**' nu genişletin ve **Bileşen durumu** düğümünü seçin. Aşağıdaki bileşenlerin durumunu izleyin:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Eşitleme durumu

Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **iş için Microsoft Store** düğümünü seçin. **Son eşitleme durumu** sütununu kontrol edin.

### <a name="view-synchronized-apps"></a>Eşitlenmiş uygulamaları görüntüleme

Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **Mağaza uygulamaları için lisans bilgileri** düğümünü seçin.


## <a name="log-files"></a>Günlük dosyaları

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker. log

Bu günlük dosyası, `\Logs` Configuration Manager yükleme dizininde bulunan hizmet bağlantı noktasında bulunur. Bulut hizmetiyle iletişim hakkındaki bilgileri kaydeder. Bu bilgiler meta veriler, simgeler, paketler ve lisans dosyası alımı içerir.

Günlük düzeyini değiştirmek için `LoggingLevel` değeri `0` `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` kayıt defteri anahtarında olarak değiştirin. Daha fazla bilgi için bkz. [günlük seçeneklerini yapılandırma](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION. log

Bu günlük dosyası, `\Logs` Configuration Manager yükleme dizininde bulunan hizmet bağlantı noktasında bulunur. WSfBSyncWorker hizmeti başlatılmamışsa veya art arda başlayıp durdurulduğunda, bu günlük dosyasındaki girişleri gözden geçirin.

> [!NOTE]
> Bu günlük dosyası diğer özelliklerle paylaşılır.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker. log

Bu günlük dosyası, hiyerarşideki en üst düzey site için site sunucusunda bulunur. Configuration Manager yükleme dizininde `\Logs` yer alabilir. Aşağıdaki işlemlerle ilgili bilgileri kaydeder:

- BusinessAppProcessWorker bileşeni tarafından eşitlenen meta veri bilgilerini veritabanına ekleyin
- Dosyaları işleme`\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER. log

Bu günlük dosyası, hiyerarşideki en üst düzey site için site sunucusunda bulunur. Configuration Manager yükleme dizininde `\Logs` yer alabilir. BusinessAppProcessWorker hizmeti başlatılmamışsa veya art arda başlayıp durdurulduğunda, bu günlük dosyasındaki girişleri gözden geçirin.



## <a name="last-sync-failed"></a>Son eşitleme başarısız oldu

Son eşitleme durumu *başarısız*olduğunda, belirtiyi belirlemek için aşağıdaki [günlük dosyalarını](#log-files) inceleyerek başlayın:

- WSfbSyncWorker. log
- SMS_CLOUDCONNECTION. log

Daha sonra genel sorunlar için aşağıdaki bölümlerden birine bakın:

- [Yetkilendirme hatası](#bkmk_fail-symptom1)
- [Gizli anahtar geçersiz](#bkmk_fail-symptom2)
- [Uygulama belirteci alınırken hata oluştu](#bkmk_fail-symptom3)
- [İçerik konumu yok veya yanlış izinler](#bkmk_fail-symptom4)
- [Http isteği ' GET ' metodu çağrılırken hata oluştu](#bkmk_fail-symptom5)
- [Arabelleğe daha fazla bayt yazılamaz](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a>Yetkilendirme hatası

#### <a name="cause"></a>Nedeni

Bu sorun, yapılandırılan Azure Active Directory (Azure AD) uygulamasının bu kiracıya yönelik Iş ve eğitim Microsoft Store yönetme izinleri yoksa oluşabilir.

#### <a name="workaround"></a>Geçici çözüm

1. Microsoft Store Iş veya eğitim portalında yönetici olarak oturum açın.
1. **Ayarlar**' a gidin ve **Yönetim Araçları**' nı seçin.
1. Uygulama listede yoksa, **Yönetim Aracı Ekle**' yi seçin. Ardından ada göre arama yapın ve Configuration Manager aynı ClientID ile ilişkili Azure AD uygulamasını seçin.
1. Durum **etkin**' i göstermezse, **eylem** bölümünde **Etkinleştir** ' i seçin.
1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **iş için Microsoft Store** düğümünü seçin. Mağaza ile eşitleyin veya bir sonraki eşitleme aralığının gerçekleşmesini bekleyin.

> [!Tip]
> Configuration Manager içindeki ClientID 'yi bulmak için:
>
> 1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Azure Active Directory tenmi** düğümünü seçin.
> 1. Iş ve eğitim tümleştirmesi için Microsoft Store kullandığınız kiracıyı seçin.
> 1. Sonuçlar bölmesinde, eşleşen uygulamayı bulun ve **ISTEMCI kimliği** sütununa bakın.

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a>Gizli anahtar geçersiz

#### <a name="cause"></a>Nedeni

Bu sorun, Iş ve eğitim yapılandırması için Microsoft Store Azure AD uygulamasında gizli anahtarın süresi dolmuşsa oluşabilir.

#### <a name="resolution"></a>Çözüm

Azure AD uygulaması için gizli anahtarı yenileyin. Daha fazla bilgi için bkz. [gizli anahtarı yenileme](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a>Uygulama belirteci alınırken hata oluştu

#### <a name="cause"></a>Nedeni

Bu sorun, bağlantılı uygulama artık Azure AD 'de yoksa oluşabilir.

#### <a name="resolution"></a>Çözüm

Iş ve eğitim için Microsoft Store bağlantısını silin ve yeniden oluşturun.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **iş için Microsoft Store** düğümünü seçin.
1. Mevcut bağlantıyı seçin.
1. Şeritte **Sil** ' i seçin.

Sonra bağlantıyı yeniden oluşturun. Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Azure hizmetlerini yapılandırma](../../core/servers/deploy/configure/azure-services-wizard.md)
- [Iş ve eğitim eşitlemesi için Microsoft Store ayarlama](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a>İçerik konumu yok veya yanlış izinler

#### <a name="cause"></a>Nedeni

Iş ve eğitim bağlantısı için Microsoft Store ayarlarken, eşitlenen içeriği depolamak için bir ağ paylaşımının olduğunu belirtirsiniz. Bu sorun, bu paylaşımın bulunmaması veya yanlış izinlere sahip olmaması durumunda ortaya çıkabilir. Hizmet bağlantı noktasının bilgisayar hesabı, bu dizinin sahibi ve tüm alt dizinler olmalıdır.<!-- memdocs#146 --> Aksi takdirde, aşağıdaki hatayla benzer bir hata görürsünüz:

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

Yapılandırdığınız konumu görmek için:

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **iş için Microsoft Store** düğümünü seçin.

1. Hesabı seçin ve **özelliklerini**açın.

1. **Yapılandırma** sekmesine geçin. **Konum** ayarı, Iş ve eğitim için Microsoft Store indirilen uygulama içeriğinin depolandığı ağ yolunu gösterir.

#### <a name="workaround"></a>Geçici çözüm

1. Henüz yoksa, paylaşma oluşturun.

1. Klasördeki NTFS izinlerini ve ağ paylaşımındaki izinleri denetleyin. Hizmet bağlantı noktasının bilgisayar hesabına **okuma** ve **yazma** izinleri verin.

Konumu yeniden yapılandırmak istiyorsanız yeni içerik konumuyla bağlantıyı silin ve yeniden oluşturun.

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a>Http isteği ' GET ' metodu çağrılırken hata oluştu

#### <a name="cause"></a>Nedeni

Bu sorun, mağazadan uygulamaların eşitlenmesi içerik URL 'sinin süre dolduğunda uzun sürmesi durumunda ortaya çıkabilir.

#### <a name="workaround"></a>Geçici çözüm

Eşitleme işlemini yeniden deneyin

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **iş için Microsoft Store** düğümünü seçin.
1. Bağlantıyı seçin. Şeritte, **iş için Microsoft Store Eşitle**' yi seçin.

Her seferinde daha fazla devam etmelidir. Aşağıdaki faktörlere bağlı olarak birkaç yeniden deneme alabilir:

- Çevrimdışı uygulama sayısı
- Paketlerin boyutu
- Ağ hızı

Her girişimle, hatayı daha az kez görmeniz gerekir. Hata sayısı azalmazsa, başka bir sorun var.

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a>Arabelleğe daha fazla bayt yazılamaz

#### <a name="cause"></a>Nedeni

Bu sorun, uygulamanın paketi 500 MB 'tan büyükse oluşabilir. Configuration Manager, yalnızca 500 MB 'tan küçük paketlere sahip çevrimdışı uygulamaların otomatik eşitlemesini destekler.

#### <a name="workaround"></a>Geçici çözüm

Bu uygulamaları otomatik olarak eşitleyemezsiniz, ancak içeriği indirebilir ve uygulamayı el ile oluşturabilirsiniz:

1. **Wsfbsynworker. log**dosyasında aşağıdaki satırdan başarısız olan uygulama kimliğini alın:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Microsoft Store Iş veya eğitim portalında yönetici olarak oturum açın. Bu uygulamanın sayfasını bulun.

    > [!Tip]
    > Sayfanın URL 'SI şuna benzerdir:`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Henüz seçili değilse **çevrimdışı**' ı seçin. Ardından **Yönet**' i seçin.

    1. Tüm desteklenen platformlar için uygulama içerik paylaşımınızda ayrı bir klasör oluşturun.

    1. Paketi paket klasörüne indirin.

    1. Kodlanmış lisans dosyasını Paket klasörüne bir `.bin` dosya olarak indirin.

    1. Tüm gerekli çerçeveleri Paket klasörüne indirin.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.

1. Uygulama bilgilerini el ile belirterek [bir uygulama oluşturun](create-applications.md).

    1. Daha önce indirdiğiniz desteklenen her platform için bir dağıtım türü oluşturun.

    1. Yazın: **Windows uygulama paketi (\*. appx, \*. appxpaket)**

    1. Gerekli bir bağımlılık paketini değil, gerçek uygulama paketi için appx/appxdemeti belirtin.

Son **Içeri aktarma bilgileri** sayfasında aşağıdaki ayrıntıları onaylayın:

- **Lisans dosyası:** `.bin` Dosyayı belirtir. Bu lisans dosyası, çevrimdışı uygulamalar için gereklidir.
- **Windows uygulama bağımlılıkları:** Bu paket için tüm gerekli bağımlılıkların indirildiğini doğrulayın.


## <a name="sync-doesnt-run"></a>Eşitleme çalıştırılmadı

Bu bölümde aşağıdaki eşitleme sorunları ele alınmaktadır:

- Eşitleme işlemini el ile başlatırsanız, ancak çalışmaz
- Site her gün otomatik olarak eşitlenmez

Belirtiyi belirlemek için aşağıdaki [günlük dosyalarını](#log-files) inceleyerek başlayın:

- BusinessAppProcessWorker. log
- SMS_BUSINESS_APP_PROCESS_MANAGER. log
- WsfbSyncWorker. log
- SMS_CLOUDCONNECTION. log

Daha sonra genel sorunlar için aşağıdaki bölümlerden birine bakın:

- [El ile eşitleme başlamıyor](#bkmk_sync-symptom1)
- [SMS_BUSINESS_APP_PROCESS_MANAGER. log dosyasında otomatik günlük eşitleme çalışmıyor ve "# çalışan kapatılıyor" hatası](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a>El ile eşitleme başlamıyor

#### <a name="cause"></a>Nedeni

Bu sorun, önceki eşitlemeden 10 dakikadan daha az bir eşitleme başlatırsanız oluşabilir. Her 10 dakikada bir daha sık eşitleme yapamazsınız.

#### <a name="resolution"></a>Çözüm

Başka bir eşitleme başlatmadan önce en az 10 dakika bekleyin.

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a>SMS_BUSINESS_APP_PROCESS_MANAGER. log dosyasında otomatik günlük eşitleme çalışmıyor ve "# çalışan kapatılıyor" hatası

#### <a name="cause"></a>Nedeni

Bu sorun, SMS_BUSINESS_APP_PROCESS_MANAGER bileşen WsfbSyncWorker iş parçacığını durdurduktan sonra ortaya çıkabilir. Hata ya da `2` `4` çalışanları belirtebilir.

#### <a name="workaround"></a>Geçici çözüm

**SMS_EXECUTIVE** hizmetini yeniden başlatın.

Bu ana hizmeti yeniden başlatamadıysanız, her iki bileşeni de MSfB çalışanları ile durdurun ve her ikisini de başlatın:

1. Hizmet bağlantı noktasını çalıştıran sunucuda Windows kayıt defteri 'ni açın

1. Şuraya gidin: `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. Istenen Işlemi **Durdur**olarak ayarlayın.

    1. Geçerli durumu doğrulamak için Yenile = **durduruldu**.

1. Şuraya gidin: `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. Istenen Işlemi **Durdur**olarak ayarlayın.

    1. Geçerli durumu doğrulamak için Yenile = **durduruldu**.

1. **SMS_CLOUDCONNECTION**, Istenen işlemi **Başlangıç**olarak ayarlayın.

1. **SMS_BUSINESS_APP_PROCESS_MANAGER**, Istenen işlemi **Başlangıç**olarak ayarlayın.


## <a name="language-related-issues"></a>Dille ilgili sorunlar

Bu bölüm aşağıdaki yaygın sorunları içerir:

- [Dil seçimi değişiklikleri uygulanmadı](#bkmk_lang-symptom1)
- [Tüm lisans bilgileri için seçili dillerin hepsi yok](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a>Dil seçimi değişiklikleri uygulanmadı

#### <a name="cause"></a>Nedeni

Bu sorun, dil seçimi önbelleğe alınmışsa ve özellik değerleri değiştirildikten sonra temizlenmemişse ortaya çıkabilir.

#### <a name="workaround"></a>Geçici çözüm

Bu sorunu çözmek için **SMS_Executive** hizmetini yeniden başlatın.

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a>Tüm lisans bilgileri için seçili dillerin hepsi yok

#### <a name="cause"></a>Nedeni

Bu sorun, Iş ve eğitim uygulamasının lisans bilgileri için Microsoft Store belirtilen dile ait yerelleştirilmiş verileri içermiyorsa ortaya çıkabilir.

#### <a name="workaround"></a>Geçici çözüm

Oluşturulan uygulamalar için eksik dilleri el ile ekleyin.


## <a name="offline-applications"></a>Çevrimdışı uygulamalar

Bu bölüm aşağıdaki yaygın sorunları içerir:

- [İçerik doğrulanamadığından çevrimdışı uygulama oluşturulamadı](#bkmk_off-symptom1)
- [Çevrimdışı lisans bilgileriyle oluşturulan uygulama yüklenemedi](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a>İçerik doğrulanamadığından çevrimdışı uygulama oluşturulamadı

#### <a name="cause"></a>Nedeni

Bu sorun, çevrimdışı uygulamanın eşitlenen içeriği bozuksa veya değiştirilirse ortaya çıkabilir.

#### <a name="workaround"></a>Geçici çözüm

Yeni bir eşitleme başlatın. Eşitleme tamamlandığında, yanlış içerik dosyalarını doğrulayıp indirmeli.

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a>Çevrimdışı lisans bilgileriyle oluşturulan uygulama yüklenemedi

#### <a name="cause"></a>Nedeni

Bu sorun, uygulamayı Windows 10 ' un 1511 sürümünden önceki bir sürümünü çalıştıran bir istemciye dağıtırsanız ortaya çıkabilir. Iş ve eğitim için Microsoft Store çevrimdışı lisanslı uygulamalar yalnızca Windows 10 sürüm 1511 ve üzeri sürümlerde desteklenir.

#### <a name="resolution"></a>Çözüm

Windows 10 ' un en son sürümünü yükler.


## <a name="next-steps"></a>Sonraki adımlar

Ek Yardım bulmak için bkz. [Configuration Manager kullanmak için yardım bulma](../../core/understand/find-help.md).
