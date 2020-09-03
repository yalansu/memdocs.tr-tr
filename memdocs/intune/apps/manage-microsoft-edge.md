---
title: Intune ile iOS ve Android için kenarı yönetme
titleSuffix: ''
description: Şirket web sitelerine her zaman karşı korumalar ile erişildiğinden emin olmak için iOS ve Android için Edge ile Intune uygulama koruma ve yapılandırma ilkelerini kullanın.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9391be828452cbda25dd6c4f4ed75cffa2ef687c
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423756"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>Microsoft Intune ile iOS ve Android için Edge kullanarak Web erişimini yönetme

İOS ve Android için Edge, kullanıcıların Web 'e gözatmasını ve çoklu kimliği desteklemesini sağlamak üzere tasarlanmıştır. Kullanıcılar, göz atmak için bir iş hesabı ve kişisel hesap ekleyebilir. İki kimlik arasında, diğer Microsoft mobil uygulamalarında sunulan gibi bir ayrım vardır.

İOS için Edge, iOS 12,0 ve üzeri sürümlerde desteklenir. Android için Edge, Android 5 ve üzeri sürümlerde desteklenir.

> [!NOTE]
> İOS ve Android için Edge, bu ayarlara erişemediği için iOS ve Android Edge, kullanıcıların cihazlarında yerel tarayıcı için ayarlandığı ayarları tüketmez.

Microsoft 365 verilerine yönelik zengin ve en geniş koruma özellikleri, koşullu erişim gibi Microsoft Intune ve Azure Active Directory Premium özellikleri içeren Enterprise Mobility + Security Suite 'e abone olduğunuzda kullanılabilir. En azından, mobil cihazlardan iOS ve Android için uçtan bağlantıya izin veren bir koşullu erişim ilkesi ve göz atma deneyiminin korunmasını sağlayan bir Intune uygulama koruma ilkesi dağıtmak isteyeceksiniz.

> [!NOTE]
> İOS cihazlarında yeni web klipleri (sabitlenmiş Web uygulamaları), korumalı bir tarayıcıda açılması gerektiğinde Intune Managed Browser yerine iOS ve Android için açılır. Daha eski iOS web klipleri için, Managed Browser yerine iOS ve Android için Edge 'de açıldıklarından emin olmak üzere bu web kliplerini yeniden hedeflemelidir.

## <a name="apply-conditional-access"></a>Koşullu erişim Uygula
Kuruluşlar, kullanıcıların yalnızca iOS ve Android için Edge kullanarak iş veya okul içeriğine erişebildiğinden emin olmak için Azure AD koşullu erişim ilkelerini kullanabilir. Bunu yapmak için tüm olası kullanıcıları hedefleyen bir koşullu erişim ilkesine ihtiyacınız olacaktır. Bu ilkeyi oluşturma hakkındaki ayrıntılar, [bulut uygulaması Için koşullu erişimle uygulama koruma Ilkesi iste](/azure/active-directory/conditional-access/app-protection-based-conditional-access)' de bulunabilir.

1. Senaryo 2: tarayıcı uygulamaları, iOS ve Android için kenara izin veren [Uygulama koruma ilkeleriyle onaylanan uygulamalar gerektirir](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies), ancak diğer mobil cihaz Web tarayıcılarının Office 365 uç noktalarına bağlanmasını engeller.

   >[!NOTE]
   > Bu ilke, mobil kullanıcıların iOS ve Android için Edge içinden tüm Microsoft 365 uç noktalarına erişebilmesini sağlar. Bu ilke ayrıca kullanıcıların Microsoft 365 uç noktalarına erişmek için InPrivate kullanmasını engeller.

Koşullu erişimle, [Azure AD uygulama ara sunucusu](/azure/active-directory/active-directory-application-proxy-get-started)aracılığıyla dış kullanıcılara kullanıma sunulacak şirket içi siteleri de hedefleyebilirsiniz.

## <a name="create-intune-app-protection-policies"></a>Intune uygulama koruma ilkeleri oluşturma

Uygulama koruma Ilkeleri (uygulama) hangi uygulamalara izin verileceğini ve kuruluşunuzun verileriyle alabilecekleri eylemleri tanımlar. UYGULAMADA kullanılabilen seçimler, kuruluşların korumayı özel gereksinimlerine uyarlamalarını sağlar. Bazıları için, bir bütün senaryoyu uygulamak için hangi ilke ayarlarının gerekli olduğu açık olmayabilir. Microsoft, kuruluşların mobil istemci uç noktası sağlamlaştırma için öncelik vermesini sağlamak üzere iOS ve Android mobil uygulama yönetimi için uygulama veri koruma çerçevesi için Taksonomi sunmuştur.

UYGULAMA veri koruma çerçevesi, her düzey bir önceki düzeyin üzerinde oluşturulmasıyla birlikte üç ayrı yapılandırma düzeyi halinde düzenlenmiştir:

- **Kurumsal temel veri koruması** (düzey 1), uygulamaların PIN ile korunmasını ve şifreli silme işlemleri gerçekleştirmesini sağlar. Android cihazlar için bu düzey, Android cihaz kanıtlamasını doğrular. Bu, Exchange Online posta kutusu ilkelerinde benzer veri koruma denetimi sağlayan ve bunu ve Kullanıcı popülasyonu uygulamayı sunan bir giriş düzeyi yapılandırmadır.
- **Kurumsal gelişmiş veri koruması** (düzey 2), uygulama veri sızıntısı önleme mekanizmalarını ve en düşük işletim sistemi gereksinimlerini tanıtır. Bu, iş veya okul verilerine erişen mobil kullanıcıların çoğu için geçerli olan yapılandırmadır.
- **Kurumsal yüksek veri koruma** (düzey 3) gelişmiş veri koruma mekanizmaları, gelişmiş PIN YAPıLANDıRMASı ve uygulama mobil tehdit savunması sağlar. Bu yapılandırma, yüksek riskli verilere erişen kullanıcılar için istenir.

Her yapılandırma düzeyi ve korunması gereken en düşük uygulamalar için belirli önerilere bakmak için, [Uygulama koruma ilkelerini kullanarak Data Protection Framework 'ü](app-protection-framework.md)inceleyin.

Cihazın birleştirilmiş bir uç nokta yönetimi (UEM) çözümüne kaydolmasından bağımsız olarak, [Uygulama koruma ilkeleri oluşturma ve atama](app-protection-policies.md)bölümündeki adımları kullanarak hem iOS hem de Android Uygulamaları Için bir Intune uygulama koruma ilkesi oluşturulması gerekir. En azından bu ilkelerin aşağıdaki koşullara uyması gerekir:

1. Bu kişiler, Edge, Outlook, OneDrive, Office veya takımlar gibi tüm mobil uygulamaları Microsoft 365, böylece kullanıcıların herhangi bir Microsoft uygulamasındaki iş veya okul verilerine güvenli bir şekilde erişebilmesini ve bunları işleyebilmesini sağlar.

2. Bunlar tüm kullanıcılara atanır. Bu, iOS veya Android için Edge kullanıp kullanmadıklarından bağımsız olarak tüm kullanıcıların korunmasını sağlar.

3. Gereksinimlerinizi karşılayan çerçeve düzeyini saptayın. Çoğu kuruluş, veri koruma ve erişim gereksinimleri denetimlerine izin veren şekilde **Kurumsal gelişmiş veri koruması** 'nda (düzey 2) tanımlanan ayarları uygulamalıdır.

Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Android uygulama koruma ilkesi ayarları](app-protection-policy-settings-android.md) ve [iOS uygulama koruma ilkesi ayarları](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Intune uygulama koruma ilkelerini Intune 'a kayıtlı olmayan Android cihazlarda uygulamalara uygulamak için, kullanıcının da Intune Şirket Portalı yüklemesi gerekir. Daha fazla bilgi için bkz. [Android uygulamanız uygulama koruma ilkeleriyle yönetildiğinde beklemeniz gerekenler](../fundamentals/end-user-mam-apps-android.md).

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>İlkeyle korunan tarayıcılarda Azure AD 'ye bağlı Web Apps 'te çoklu oturum açma

İOS ve Android için Edge, Azure AD 'ye bağlı olan tüm Web uygulamalarına (SaaS ve şirket içi) çoklu oturum açma (SSO) özelliğinden yararlanabilir. SSO, kullanıcıların kimlik bilgilerini yeniden girmeye gerek kalmadan iOS ve Android için Azure AD bağlantılı Web uygulamalarına erişmesine olanak sağlar.

SSO, cihazınızın iOS cihazları için Microsoft Authenticator uygulaması veya Android üzerindeki Intune Şirket Portalı kaydedilmesini gerektirir. Kullanıcılar bunlardan herhangi birine sahip olduklarında, ilke korumalı bir tarayıcıda Azure AD 'ye bağlı bir Web uygulamasına gittiklerinde cihazlarını kaydetmeleri istenir (Bu yalnızca cihazlarınızın henüz kaydedilmediği durumlarda geçerlidir). Cihaz, kullanıcının Intune tarafından yönetilen hesabına kaydedildikten sonra, bu hesabın Azure AD 'ye bağlı Web uygulamaları için etkin SSO 'SU vardır.

> [!NOTE]
> Cihaz kaydı, Azure AD hizmeti ile basit bir iade etme işlemidir. Tam cihaz kaydı gerektirmez ve bu cihaza cihazda ek ayrıcalıklar vermez.

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>Gözatma deneyimini yönetmek için uygulama yapılandırması 'nı kullanın

İOS ve Android için Edge, Microsoft Endpoint Manager, yöneticilerin uygulamanın davranışını özelleştirmesini sağlamak gibi Birleşik uç nokta yönetimine izin veren uygulama ayarlarını destekler.

Uygulama yapılandırması, kayıtlı cihazlarda mobil cihaz yönetimi (MDM) işletim sistemi kanalı aracılığıyla (iOS için[yönetilen uygulama yapılandırma](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) kanalı veya Android için [kuruluş kanalında android](https://developer.android.com/work/managed-configurations) ) veya Intune uygulama koruması ilkesi (uygulama) kanalı aracılığıyla teslim edilebilir. İOS ve Android için Edge aşağıdaki yapılandırma senaryolarını destekler:

- Yalnızca iş veya okul hesaplarına izin ver
- Genel uygulama yapılandırma ayarları
- Veri koruma ayarları

> [!IMPORTANT]
> Android 'de cihaz kaydı gerektiren yapılandırma senaryolarında cihazların Android Enterprise 'a kayıtlı olması ve Android için Edge 'in yönetilen Google Play deposu aracılığıyla dağıtılması gerekir. Daha fazla bilgi için bkz. [Android kurumsal iş profili cihazlarının kaydını ayarlama](../enrollment/android-work-profile-enroll.md) ve [yönetilen Android Kurumsal cihazları için uygulama yapılandırma ilkeleri ekleme](app-configuration-policies-use-android.md).

Her yapılandırma senaryosunda belirli gereksinimler vurgulanmıştır. Örneğin, yapılandırma senaryosunun cihaz kaydı gerektirip gerektirmediğini ve bu nedenle herhangi bir UıEM sağlayıcısıyla çalışıp çalışmadığını veya Intune Uygulama Koruması Ilke gerektirip gerektirmediğini belirtir.

> [!NOTE]
> Microsoft Endpoint Manager ile, MDM işletim sistemi kanalı üzerinden sunulan uygulama yapılandırması, **yönetilen cihazlar** uygulama yapılandırma IlkesI (ACP) olarak adlandırılır; Uygulama koruma Ilkesi kanalı üzerinden sunulan uygulama yapılandırması, **yönetilen uygulamalar** uygulama yapılandırma ilkesi olarak adlandırılır.

## <a name="only-allow-work-or-school-accounts"></a>Yalnızca iş veya okul hesaplarına izin ver

En büyük ve yüksek oranda düzenlenen müşterilerinin veri güvenliği ve uyumluluk ilkeleri, Microsoft 365 değerine göre önemli bir değerdir. Bazı şirketlerin kurumsal ortamlarında tüm iletişim bilgilerini yakalama gereksinimi vardır ve ayrıca cihazların yalnızca kurumsal iletişimler için kullanıldığından emin olun. Bu gereksinimleri desteklemek için iOS ve Android 'de Android 'e yönelik uç, uygulama içinde yalnızca tek bir şirket hesabının sağlanmasını sağlayacak şekilde yapılandırılabilir.

Aşağıdaki kuruluş izin verilen hesaplar modu ayarını yapılandırma hakkında daha fazla bilgi edinebilirsiniz:

- [Android ayarı](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS ayarı](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Bu yapılandırma senaryosu yalnızca kayıtlı cihazlarla birlikte kullanılabilir. Ancak, herhangi bir UıEM sağlayıcısı desteklenir. Microsoft Endpoint Manager kullanmıyorsanız, bu yapılandırma anahtarlarının nasıl dağıtılacağı konusunda UEM belgelerinize danışmanız gerekir.

## <a name="general-app-configuration-scenarios"></a>Genel uygulama yapılandırma senaryoları

İOS ve Android için Edge, yöneticilere birçok uygulama içi ayar için varsayılan yapılandırmayı özelleştirme olanağı sunar. Bu özellik şu anda yalnızca iOS ve Android için Edge 'de, uygulamada oturum açan iş veya okul hesabına uygulanan bir Intune Uygulama Koruması Ilkesi olduğunda ve ilke ayarları yönetilen uygulamalar uygulama yapılandırma Ilkesi aracılığıyla teslim edildiğinde sunulur.

> [!IMPORTANT]
> Android Edge, yönetilen Google Play kullanılabilen Kmıum ayarlarını desteklemez.

Edge, yapılandırma için aşağıdaki ayarları destekler:

- Yeni sekme sayfası deneyimleri
- Yer işareti deneyimleri
- Uygulama davranışı deneyimleri
- Bilgi noktası modu deneyimleri

Bu ayarlar, cihaz kayıt durumundan bağımsız olarak uygulamaya dağıtılabilir.

### <a name="new-tab-page-experiences"></a>Yeni sekme sayfası deneyimleri

İOS ve Android için Edge, kuruluşların yeni sekme sayfası deneyimini ayarlamak için çeşitli seçenekler sunar.

#### <a name="organization-logo-and-brand-color"></a>Kuruluş logosu ve marka rengi

Bu ayarlar, iOS ve Android Edge için yeni sekme sayfasını, sayfanın arka planı olarak kuruluşunuzun logosu ve marka rengini görüntüleyecek şekilde özelleştirmenize olanak tanır.

Kuruluşunuzun logosunu ve rengini karşıya yüklemek için, önce aşağıdaki adımları uygulayın:
1. [Microsoft Endpoint Manager](https://endpoint.microsoft.com)'da **Kiracı Yönetimi**  ->  **özelleştirmesi**  ->  **Şirket kimliği markasına**gidin.
2. Markanızı ayarlamak için **üst bilgide göster ' in**yanındaki "kuruluş logosu" seçeneğini belirleyin. Saydam arka plan logoları önerilir.
3. Markdosyanın arka plan rengini ayarlamak için bir **Tema rengi**seçin. İOS ve Android için Edge, yeni sekme sayfasında rengin daha açık bir gölgeyi uygular ve bu da sayfanın yüksek okunabilirlik olmasını sağlar.

Ardından, iOS ve Android için kuruluşunuzun markasını bir kenara çekmek üzere aşağıdaki anahtar/değer çiftlerini kullanın:

|    Anahtar    |    Değer    |
|--------------------------------------------------------------------|------------|
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. BrandLogo    |    **doğru** , kuruluşun marka logosunu gösterir<br>**false** (varsayılan), bir logo sunmaz    |
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. BrandColor    |    **doğru** , kuruluşun marka rengini gösterir<br>**false** (varsayılan) bir renk göstermeyecektir    |

#### <a name="homepage-shortcut"></a>Giriş sayfası kısayolu

Bu ayar, iOS ve Android için Edge için bir giriş sayfası kısayolu yapılandırmanıza olanak tanır. Yapılandırdığınız giriş sayfası kısayolu, Kullanıcı iOS ve Android için kenarda yeni bir sekme açtığında arama çubuğunun altında ilk simge olarak görünür. Kullanıcı, yönetilen bağlamlarına bu kısayolu düzenleyemez veya silemez. Ana sayfa kısayolu, kuruluşunuzun adını ayırt etmek için görüntüler. 

|    Anahtar    |    Değer    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Geçerli bir URL belirtin. Hatalı URL’ler güvenlik önlemi olarak engellenir.<br>Örnek: `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>Birden çok üst site kısayolu

Benzer şekilde, bir giriş sayfası kısayolunu yapılandırmak için, iOS ve Android için Edge 'de yeni sekme sayfalarında birden çok üst site kısayolunu yapılandırabilirsiniz. Kullanıcı yönetilen bağlamdaki bu kısayolları düzenleyemez veya silemez. Note: bir giriş sayfası kısayolu da dahil olmak üzere toplam 8 kısayol yapılandırabilirsiniz. Bir giriş sayfası kısayolu yapılandırdıysanız, yapılandırılan ilk üst siteyi geçersiz kılar. 

|    Anahtar    |    Değer    |
|-------------------------------------------------------------------|-------------|
|    com. Microsoft. Intune. mam. managedbrowser. managedTopSites   |    Değer URL 'Leri kümesi belirtin. Her üst site kısayolu bir başlık ve URL 'den oluşur. Başlığı ve URL 'YI `|` karakterle ayırın.<br>Örnek: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>Sektör Haberleri

İOS ve Android için Edge içindeki yeni sekme sayfası deneyimini, kuruluşunuzla ilgili sektör haberlerini görüntüleyecek şekilde yapılandırabilirsiniz. Bu özelliği etkinleştirdiğinizde, iOS ve Android için uç, kuruluşunuzun etki alanı adını kullanarak kuruluşunuz, kuruluşunuzun sektör ve rakipler hakkında Web 'den haberleri toplayabilir, böylece kullanıcılarınız iOS ve Android için Edge içindeki Merkezi yeni sekme sayfalarından tüm ilgili dış haberleri bulabilir. Sektör Haberleri varsayılan olarak kapalıdır. 

|    Anahtar    |    Değer    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. NewTabPage. IndustryNews    |    **doğru** , yeni sekme sayfasında sektör haberlerini gösterir<br>**false** (varsayılan) yeni sekme sayfasından sektör haberlerini gizler    |

### <a name="bookmark-experiences"></a>Yer işareti deneyimleri

İOS ve Android için Edge, etkin yer işaretlerini yönetmek için çeşitli seçenekler sunar.

#### <a name="managed-bookmarks"></a>Yönetilen yer işaretleri

Erişim kolaylığı için, kullanıcılarınızın iOS ve Android için Edge kullanırken kullanılabilir olmasını istediğiniz yer imlerini yapılandırabilirsiniz.

- Yer işaretleri yalnızca iş veya okul hesabında görüntülenir ve kişisel hesaplara gösterilmez.
- Yer işaretleri kullanıcılar tarafından silinemez veya değiştirilemez.
- Yer işaretleri listenin en üstünde görünür. Kullanıcıların oluşturmakta olduğu tüm yer işaretleri bu yer işaretlerinin altında görünür.
- Uygulama proxy 'Si yeniden yönlendirmeyi etkinleştirdiyseniz, iç veya dış URL 'lerini kullanarak uygulama proxy 'Si Web uygulamaları ekleyebilirsiniz.
- **Http://** veya **https://** ile tüm URL 'leri listeye girerken ön ek olduğunuzdan emin olun.
- Yer işaretleri, Azure Active Directory tanımlı kuruluşun adından sonra adlı bir klasörde oluşturulur.

|    Anahtar    |    Değer    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    Bu yapılandırmanın değeri, yer işaretlerinin bir listesidir. Her yer işareti, yer işareti başlığından ve yer işareti URL 'sinden oluşur. Başlığı ve URL 'YI `|` karakterle ayırın.<br> Örnek: `Microsoft Bing|https://www.bing.com`<p>Birden çok yer işaretini yapılandırmak için, her çifti çift karakterle ayırın `||` .<br>Örneğin:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>Uygulamalarım yer işareti

Varsayılan olarak, kullanıcılar iOS ve Android için Edge içinde kuruluş klasörü içinde yapılandırılmış uygulamalarım yer işaretine sahiptir.

|    Anahtar    |    Değer    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. Uygulamaps    |    **true** (varsayılan) IOS ve Android yer Işaretlerine yönelik Edge Içindeki uygulamalarımı gösterir<br>**false** , IOS ve Android için Edge Içindeki uygulamalarımı gizler    |

### <a name="app-behavior-experiences"></a>Uygulama davranışı deneyimleri

İOS ve Android için Edge, kuruluşların uygulamanın davranışını yönetmek için çeşitli seçenekler sunar.

#### <a name="default-protocol-handler"></a>Varsayılan protokol işleyicisi

Varsayılan olarak, iOS ve Android için uç, Kullanıcı URL 'de Protokolü belirtmezse HTTPS protokol işleyicisini kullanır. Genellikle bu, en iyi uygulama olarak kabul edilir ancak devre dışı bırakılabilir.

|    Anahtar    |    Değer    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. defaultHTTPS     |     **true** (varsayılan) varsayılan protokol işleyicisi https 'dir<br>**yanlış** varsayılan protokol işleyicisi http 'dir     |

#### <a name="disable-data-sharing-for-personalization"></a>Kişiselleştirme için veri paylaşımını devre dışı bırak

Varsayılan olarak, iOS ve Android için, kullanıcıların, gözatma deneyimlerini kişiselleştirmek için kullanım verilerini toplama ve gözatma geçmişini paylaşma istemleri istenir. Kuruluşlar bu veri paylaşımını, bu istem son kullanıcılara gösterilmesini önleyecek şekilde devre dışı bırakabilir.

|    Anahtar    |    Değer    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com. Microsoft. Intune. mam. managedbrowser. disableShareUsageData    |     **true** , bu istemi son kullanıcılara görüntülemesini devre dışı bırakır<br>**yanlış** (varsayılan) kullanıcılardan kullanım verilerini paylaşması istenir    |
|     com. Microsoft. Intune. mam. managedbrowser. disableShareBrowsingHistory    |     **true** , bu istemi son kullanıcılara görüntülemesini devre dışı bırakır<br>**yanlış** (varsayılan) kullanıcıların gözatma geçmişini paylaşması istenir     |

#### <a name="disable-specific-features"></a>Belirli özellikleri devre dışı bırak

İOS ve Android için Edge, kuruluşların varsayılan olarak etkinleştirilen bazı özellikleri devre dışı bırakmasına olanak sağlar. Bu özellikleri devre dışı bırakmak için aşağıdaki ayarı yapılandırın:

|    Anahtar    |    Değer    |
|-----------------------|-----------------------|
|    com. Microsoft. Intune. mam. managedbrowser. disabledFeatures    |    **parola** , son kullanıcının parolalarını kaydetmenizi sağlayan istemleri devre dışı bırakır<br>**InPrivate** , InPrivate taramayı devre dışı bırakır<p>Birden çok özelliği devre dışı bırakmak için değerleri ile ayırın `|` . Örneğin, `inprivate|password` hem InPrivate hem de parola depolamayı devre dışı bırakır.     |

> [!NOTE]
> Android Edge, parola Yöneticisi 'nin devre dışı bırakılmasını desteklemez.

#### <a name="disable-extensions"></a>Uzantıları devre dışı bırak

Kullanıcıların herhangi bir uygulama uzantısını yüklemesini engellemek için Android 'in Edge içindeki uzantı çerçevesini devre dışı bırakabilirsiniz. Bunu yapmak için aşağıdaki ayarı yapılandırın:

|    Anahtar    |    Değer    |
|-----------|-------------|
|    com. Microsoft. Intune. mam. managedbrowser. disableExtensionFramework    |    **true** , uzantı çerçevesini devre dışı bırakır<br>**false** (varsayılan) uzantı çerçevesini etkinleştirilir    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Android cihazlarda bilgi noktası modu deneyimleri

Android Edge, aşağıdaki ayarlara sahip bir bilgi noktası uygulaması olarak etkinleştirilebilir:

|    Anahtar    |    Değer    |
|-----------|-------------|
|    com. Microsoft. Intune. mam. managedbrowser. Enablekıoskmode    |    **true** , Android için uç bilgi noktası modunu sunar<br>**false** (varsayılan) bilgi noktası modunu devre dışı bırakır    |
|    com. Microsoft. Intune. mam. managedbrowser. Showaddressbarınkioskmode    |    **doğru** , adres çubuğunu bilgi noktası modunda gösterir<br> **yanlış** (varsayılan) bilgi noktası modu etkinleştirildiğinde adres çubuğunu gizler    |
|    com. Microsoft. Intune. mam. managedbrowser. Showbot, Arınkioskmode    |    **true** , bilgi noktası modunda alt eylem çubuğunu gösterir<br> **yanlış** (varsayılan) bilgi noktası modu etkinleştirildiğinde alt çubuğu gizler    |

## <a name="data-protection-app-configuration-scenarios"></a>Veri koruma uygulaması yapılandırma senaryoları

Uygulama Microsoft Uç Nokta Yöneticisi tarafından, uygulamada oturum açan iş veya okul hesabına uygulanan bir Intune Uygulama Koruması Ilkesiyle yönetilen ve ilke ayarları yönetilen uygulamalar uygulama yapılandırma Ilkesi aracılığıyla teslim edildiğinde, iOS ve Android için uygulama yapılandırma ilkelerini, aşağıdaki veri koruma ayarları için destekler:

- Hesap eşitlemesini yönetme
- Kısıtlanmış Web sitelerini yönetme
- Ara sunucu yapılandırmasını yönetme
- NTLM çoklu oturum açma sitelerini yönetme

Bu ayarlar, cihaz kayıt durumundan bağımsız olarak uygulamaya dağıtılabilir.

### <a name="manage-account-synchronization"></a>Hesap eşitlemesini yönetme

Varsayılan olarak, Microsoft Edge eşitleme, kullanıcıların kendi oturum açan cihazlarındaki gözatma verilerine erişmesini sağlar. Eşitleme tarafından desteklenen veriler şunları içerir:

- Sık Kullanılanlar
- Parolalar
- Adresler ve daha fazlası (otomatik doldurma formu girişi)

Eşitleme işlevselliği Kullanıcı izni aracılığıyla etkinleştirilir ve kullanıcılar, yukarıda listelenen her veri türü için eşitlemeyi açıp kapatabilir. Daha fazla bilgi için bkz. [Microsoft Edge Sync](/DeployEdge/microsoft-edge-enterprise-sync).

Kuruluşların iOS ve Android 'de Edge eşitlemesini devre dışı bırakma yeteneği vardır. 

|Anahtar  |Değer  |
|---------|---------|
|com. Microsoft. Intune. mam. managedbrowser. account. syncDisabled     |**true** (varsayılan) kenar eşitlemesine izin verir<br>**false** , kenar eşitlemesini devre dışı bırakır          |

### <a name="manage-restricted-web-sites"></a>Kısıtlanmış Web sitelerini yönetme

Kuruluşlar, kullanıcıların iOS ve Android için Edge 'deki iş veya okul hesabı bağlamı dahilinde erişebileceği siteleri tanımlayabilir. Bir izin verilenler listesi kullanırsanız, kullanıcılarınız yalnızca açıkça listelenen sitelere erişebilir. Engellenen bir liste kullanıyorsanız, kullanıcılar açıkça Engellenenler hariç tüm sitelere erişebilirler. Yalnızca izin verilen veya engellenen bir liste oluşturmanız gerekir, her ikisini birden değil. Her ikisini de ayarlarsanız yalnızca izin verilenler listesi kabul edilir.

Kuruluş Ayrıca, bir Kullanıcı kısıtlı bir Web sitesine gitmeye çalıştığında ne olacağını tanımlar. Varsayılan olarak, geçişlere izin verilir. Kuruluş buna izin veriyorsa, kısıtlı web siteleri kişisel hesap bağlamında, Azure AD hesabının InPrivate bağlamında açılabilir veya sitenin tamamen engellenip engellenmeyeceğini belirtir. Desteklenen çeşitli senaryolar hakkında daha fazla bilgi için bkz. [Microsoft Edge Mobile 'Da kısıtlı web sitesi geçişleri](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333). Geçiş deneyimlerine izin vererek, kuruluşun kullanıcıları korumalı kalır ve şirket kaynaklarını güvende tutun.

> [!NOTE]
> İOS ve Android için Edge, sitelere yalnızca doğrudan erişildiğinde erişimi engelleyebilir. Kullanıcılar, siteye erişmek için ara hizmetler (örneğin bir çeviri hizmeti) kullandıklarında erişimi engellemez.

İOS ve Android için Edge için izin verilen veya engellenen bir site listesini yapılandırmak için aşağıdaki anahtar/değer çiftlerini kullanın. 

|Anahtar  |Değer  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |Bir anahtara karşılık gelen değer bir URL listesidir. Tek bir değer olarak izin vermek istediğiniz tüm URL 'Leri bir kanal karakteriyle ayırarak girersiniz `|` .<p>**Örnekler:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |Bir anahtara karşılık gelen değer bir URL listesidir. Engellemek istediğiniz tüm URL 'Leri tek bir değer olarak, bir kanal karakteriyle ayırarak girersiniz `|` .<br>**Örnekler:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com. Microsoft. Intune. mam. managedbrowser. Allowgeçişli Tiononblock     |**true** (varsayılan), IOS ve Android Edge 'in kısıtlanmış siteleri geçmesine izin verir. Kişisel hesaplar devre dışı bırakılmadıkça, kullanıcılardan kısıtlı siteyi açmak veya kişisel hesap eklemek için kişisel bağlamına geçmesi istenir. Com. Microsoft. Intune. mam. managedbrowser. Openınprivateifengellenme true olarak ayarlanırsa, kullanıcılar kısıtlanmış siteyi InPrivate bağlamda açma yeteneğine sahiptir.<p>**false** , IOS ve Android 'in kullanıcıları geçişini önler. Kullanıcılara erişmeye çalıştıkları sitenin engellendiğini bildiren bir ileti gösterilir.         |
|com. Microsoft. Intune. mam. managedbrowser. Openınprivateifengellenme     |**doğru** , Azure AD hesabının InPrivate bağlamında kısıtlı sitelerin açılmasına izin verir. Azure AD hesabı, iOS ve Android için Edge 'de yapılandırılmış tek hesap ise, kısıtlanmış site, InPrivate bağlamda otomatik olarak açılır. Kullanıcının yapılandırılmış bir kişisel hesabı varsa, kullanıcıdan InPrivate açma veya kişisel hesaba geçiş arasında seçim yapması istenir.<p> **false** (varsayılan), kısıtlı sitenin kullanıcının kişisel hesabında açılmasını gerektirir. Kişisel hesaplar devre dışıysa, site engellenir.<p>Bu ayarın etkili olabilmesi için com. Microsoft. Intune. mam. managedbrowser. Allowgeçişli Tiononblock değeri true olarak ayarlanmalıdır.          |
|com. Microsoft. Intune. mam. managedbrowser. durationOfOpenInPrivateSnackBar     | Kullanıcıların Snack Bar bildirimini (), InPrivate mod ile açıldı bağlantısını göreceği saniye sayısını girin. Kuruluşunuz bu içerik için InPrivate modunun kullanılmasını gerektiriyor. " Varsayılan olarak, Snack çubuğu bildirimi 7 saniye boyunca gösterilir.

Tanımlı izin verilenler listesi veya engellenenler listesi ayarlarından bağımsız olarak aşağıdaki sitelere her zaman izin verilir:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>İzin verilen ve engellenen site listesi için URL biçimleri 

İzin verilen/Engellenen siteler listelerinizi oluşturmak için çeşitli URL biçimleri kullanabilirsiniz. Bu izin verilen desenler aşağıdaki tabloda ayrıntılı olarak verilmiştir.

- **Http://** veya **https://** ile tüm URL 'leri listeye girerken ön ek olduğunuzdan emin olun.
- \*Aşağıdaki izin verilen desenler listesindeki kurallara göre joker karakter simgesini () kullanabilirsiniz.
- Bir joker karakter yalnızca bir bölümden (örn.) veya ana bilgisayar adının (örn.) ya da eğik `news-contoso.com` `host.contoso.com` çizgi () ile ayrıldığınızda yolun tamamının bir bölümüyle eşleşir `www.contoso.com/images` .
- Adreste bağlantı noktası numaraları belirtebilirsiniz. Bir bağlantı noktası numarası belirtmezseniz, kullanılan değerler şöyle olacaktır:
  - http için bağlantı noktası 80
  - https için bağlantı noktası 443
- Bağlantı noktası numarası için joker karakter kullanılması **desteklenmez.** Örneğin `http://www.contoso.com:*` ve `http://www.contoso.com:*/` desteklenmez. 

    |    URL    |    Ayrıntılar    |    Eşleşmeler    |    Eşleşmez    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Tek bir sayfayla eşleşir    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Tek bir sayfayla eşleşir    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*`   |    `www.contoso.com` ile başlayan tüm URL’lerle eşleşir    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Altındaki tüm alt etki alanlarını eşleştirir `contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`<br>`news-contoso.com`
    |    `http://*contoso.com/*`    |    Şununla biten tüm alt etki alanlarını eşleştirir `contoso.com/`    |    `news-contoso.com`<br>`news-contoso.com.com/daily`    |    `news-contoso.host.com`<br>`news.contoso.com`    |
    `http://www.contoso.com/images`    |    Tek bir klasörle eşleşir    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Bir bağlantı noktası numarası kullanarak tek bir sayfayla eşleşir    |    `www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Güvenli tek bir sayfayla eşleşir    |    `www.contoso.com`    |    `www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Tek bir klasör ve tüm alt klasörleriyle eşleşir    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Aşağıda, belirtemeyeceğiniz bazı girişlerin örnekleri verilmiştir:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP adresleri
  - `https://*`
  - `http://*`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>Ara sunucu yapılandırmasını yönetme

Kullanıcılara mobil cihazlarındaki intranet sitelerine erişim sağlamak için iOS ve Android için Edge ve [Azure AD uygulama ara sunucusu](/azure/active-directory/active-directory-application-proxy-get-started) birlikte kullanabilirsiniz. Örneğin: 

- Kullanıcı, Intune tarafından korunan Outlook mobil uygulamasını kullanıyor. Ardından, bir e-postada intranet sitesinin bağlantısına tıklamıştır ve iOS ve Android için Edge, bu intranet sitesinin kullanıcı tarafından uygulama proxy 'Si aracılığıyla sunulduğunu algılar. Kullanıcı, intranet sitesine ulaşmadan önce geçerli bir Multi-Factor Authentication ve koşullu erişim ile kimlik doğrulamak için uygulama proxy 'Si üzerinden otomatik olarak yönlendirilir. Kullanıcı artık mobil cihazlarında bile iç sitelere erişebiliyor ve Outlook 'taki bağlantı beklendiği gibi çalışıyor.
- Kullanıcı iOS veya Android cihazında iOS ve Android için Edge 'i açar. İOS ve Android için Edge Intune ile korunuyorsa ve uygulama proxy 'Si etkinse, Kullanıcı, kullanıldıkları iç URL 'YI kullanarak bir intranet sitesine gidebilir. İOS ve Android için Edge, bu intranet sitesinin kullanıcıya uygulama proxy 'Si aracılığıyla sunulduğunu algılar. Kullanıcı, intranet sitesine ulaşmadan önce kimlik doğrulaması yapmak için uygulama proxy 'Si üzerinden otomatik olarak yönlendirilir. 

Başlamadan önce:

- Azure AD Uygulama Ara Sunucusu aracılığıyla iç uygulamalarınızı ayarlayın.
  - Uygulama Proxy’sini yapılandırmak ve uygulama yayımlamak için bkz. [kurulum belgeleri](/azure/active-directory/manage-apps/application-proxy).
- İOS ve Android uygulamasının kenarına atanmış bir [Intune uygulama koruma ilkesi](app-protection-policy.md) olmalıdır.
- Microsoft uygulamalarının, **Microsoft Edge**olarak ayarlanan diğer uygulamalar veri aktarımı ayarı **ile Web içeriği aktarımını kısıtla** bir uygulama koruma ilkesine sahip olması gerekir.

> [!NOTE]
> Güncelleştirilmiş uygulama proxy 'Si yeniden yönlendirme verilerinin, iOS ve Android için Edge 'de etkili olması 24 saate kadar sürebilir.

Uygulama proxy 'Sini etkinleştirmek için aşağıdaki anahtar/değer çiftine sahip iOS için hedef Edge:

|    Anahtar    |    Değer    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **doğru** , Azure AD uygulaması proxy yeniden yönlendirme senaryolarına izin verebilir<br>**false** (varsayılan) Azure AD uygulaması proxy senaryolarına engel olur    |

> [!NOTE]
> Android Edge bu anahtarı tüketmez. Bunun yerine Android Edge, oturum açmış Azure AD hesabında uygulanan bir uygulama koruma Ilkesi olduğu sürece Azure AD Uygulama Ara Sunucusu yapılandırmasını otomatik olarak kullanır.

Şirket içi Web uygulamalarına sorunsuz (ve korumalı) erişimin yanı sıra iOS ve Android ve Azure AD Uygulama Ara Sunucusu için Edge kullanma hakkında daha fazla bilgi için, bkz. [daha iyi: Intune ve Azure Active Directory ekibi, Kullanıcı erişimini geliştirmek için](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). Bu blog gönderisi Intune Managed Browser başvurur, ancak içerik iOS ve Android için de geçerlidir.

### <a name="manage-ntlm-single-sign-on-sites"></a>NTLM çoklu oturum açma sitelerini yönetme

Kuruluşlar, kullanıcıların intranet Web sitelerine erişmek için NTLM ile kimlik doğrulaması yapmasını gerektirebilir. Varsayılan olarak, NTLM kimlik bilgisi önbelleğe alma devre dışı olduğunda, kullanıcılardan NTLM kimlik doğrulaması gerektiren bir Web sitesine her erişirken kimlik bilgilerini girmesi istenir. 

Kuruluşlar, belirli Web siteleri için NTLM kimlik bilgisi önbelleğe almayı etkinleştirebilir. Bu siteler için, Kullanıcı kimlik bilgilerini girdikten ve başarıyla kimlik doğrulamasından geçtikten sonra, kimlik bilgileri 30 gün varsayılan olarak önbelleğe alınır.


|Anahtar  |Değer  |
|---------|---------|
|com. Microsoft. Intune. mam. managedbrowser. NTLMSSOURLs     |Bir anahtara karşılık gelen değer bir URL listesidir. Tek bir değer olarak izin vermek istediğiniz tüm URL 'Leri bir kanal karakteriyle ayırarak girersiniz `|` .<p>**Örnekler:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>Desteklenen URL biçimlerinin türleri hakkında daha fazla bilgi için bkz. [izin verilen ve engellenen site listesi Için URL biçimleri](#url-formats-for-allowed-and-blocked-site-list).         |
|com. Microsoft. Intune. mam. managedbrowser. durationOfNTLMSSO     |Kimlik bilgilerini önbelleğe alma saati sayısı, varsayılan değer 720 saattir         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Microsoft Uç Nokta Yöneticisi ile uygulama yapılandırma senaryolarını dağıtma

Mobil uygulama yönetimi sağlayıcınız olarak Microsoft Endpoint Manager kullanıyorsanız, aşağıdaki adımlar yönetilen uygulamalar uygulama yapılandırma ilkesi oluşturmanızı sağlar. Yapılandırma oluşturulduktan sonra, ayarlarını Kullanıcı gruplarına atayabilirsiniz.

1. [Microsoft Uç Nokta Yöneticisi](https://endpoint.microsoft.com)' nde oturum açın.

2. **Uygulamalar** ' ı seçin ve ardından **uygulama yapılandırma ilkeleri**' ni seçin.

3. **Uygulama yapılandırma ilkeleri** dikey penceresinde **Ekle** ' yi seçin ve **yönetilen uygulamalar**' ı seçin.

4. **Temel bilgiler** bölümünde, uygulama yapılandırma ayarları Için bir **ad**ve isteğe bağlı bir **Açıklama** girin.

5. **Ortak**uygulamalar için **ortak uygulamaları seç**' i seçin ve ardından **hedeflenen uygulamalar** dikey penceresinde iOS ve Android Platform uygulamalarını seçerek **iOS ve Android için Edge** ' i seçin. Seçilen ortak uygulamaları kaydetmek için **Seç** ' e tıklayın.

6. Uygulama yapılandırma ilkesinin temel ayarlarını gerçekleştirmek için **İleri** ' ye tıklayın.

7. **Ayarlar** bölümünde, **sınır yapılandırması ayarlarını**genişletin.

8. Veri koruma ayarlarını yönetmek istiyorsanız, istenen ayarları uygun şekilde yapılandırın:

    - **Uygulama proxy 'si yeniden yönlendirmesi**için kullanılabilir seçenekler arasından seçim yapın: **Etkinleştir**, **devre dışı bırak** (varsayılan).

    - **Giriş sayfası kısayol URL 'si**için, *http://* veya *https://* önekini içeren geçerli bir URL belirtin. Hatalı URL’ler güvenlik önlemi olarak engellenir.

    - **Yönetilen yer işaretleri**için, başlık ve *http://* veya *https://* önekini içeren geçerli bir URL belirtin.

    - **Izin verilen URL 'ler**için GEÇERLI bir URL belirtin (yalnızca bu URL 'lere izin verilir; başka sitelere erişilemez). Desteklenen URL biçimlerinin türleri hakkında daha fazla bilgi için bkz. [izin verilen ve engellenen site listesi Için URL biçimleri](#url-formats-for-allowed-and-blocked-site-list).

    - **Engellenen URL 'ler**için GEÇERLI bir URL belirtin (yalnızca bu URL 'ler engellenir). Desteklenen URL biçimlerinin türleri hakkında daha fazla bilgi için bkz. [izin verilen ve engellenen site listesi Için URL biçimleri](#url-formats-for-allowed-and-blocked-site-list).

    - **Kısıtlı siteleri kişisel Içeriğe yeniden yönlendirme**için, kullanılabilir seçenekler arasından seçim yapın: **Etkinleştir** (varsayılan), **devre dışı bırak**.

    > [!NOTE]
    > İlkede Izin verilen URL 'Ler ve engellenen URL 'Ler tanımlandığında, yalnızca izin verilenler listesi kabul edilir.

9. Yukarıdaki ilkede gösterilmeyen ek uygulama yapılandırma ayarları yapmak istiyorsanız, **genel yapılandırma ayarları** düğümünü genişletin ve anahtar değer çiftlerine uygun şekilde girin.

10. Ayarları yapılandırmayı bitirdiğinizde **İleri**' yi seçin.

11. **Atamalar** bölümünde, **dahil edilecek grupları seçin**öğesini seçin. Uygulama yapılandırma ilkesini atamak istediğiniz Azure AD grubunu seçin ve ardından **Seç**' i seçin.

12. Atamalarla işiniz bittiğinde **İleri**' yi seçin.

13. **Uygulama yapılandırma Ilkesi Incelemesi oluştur +** dikey penceresinde, yapılandırılan ayarları gözden geçirin ve **Oluştur**' u seçin.

Yeni oluşturulan yapılandırma ilkesi, **uygulama yapılandırma** dikey penceresinde görüntülenir.

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>İOS ve Android için Edge kullanarak yönetilen uygulama günlüklerine erişin

İOS ve Android için Edge ve Android cihazlarda yüklü olan kullanıcılar, Microsoft tarafından yayımlanan tüm uygulamaların yönetim durumunu görüntüleyebilir. Aşağıdaki adımları kullanarak, yönetilen iOS veya Android uygulamalarında sorun gidermeye yönelik Günlükler gönderebilirler:

1. Cihazınızda iOS ve Android için açık uç.
2. Adres kutusuna `about:intunehelp` yazın.
3. İOS ve Android için Edge, sorun giderme modunu başlatır.

Uygulama günlüklerinde saklanan ayarların bir listesi için bkz. [istemci uygulama koruma günlüklerini gözden geçirme](app-protection-policy-settings-log.md).

Android cihazlarda günlükleri görüntüleme hakkında bilgi için bkz. [e-posta ile GÜNLÜKLERI BT yöneticinize gönderme](../user-help/send-logs-to-your-it-admin-by-email-android.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Uygulama koruma ilkeleri nelerdir?](app-protection-policy.md) 
- [Microsoft Intune için uygulama yapılandırma ilkeleri](app-configuration-policies-overview.md)