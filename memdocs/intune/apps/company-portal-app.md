---
title: Intune Şirket Portalı uygulamaları, Şirket Portalı Web sitesini ve Intune uygulamasını özelleştirme
titleSuffix: Microsoft Intune
description: Intune Şirket Portalı uygulamalar, Şirket Portalı Web sitesi ve Intune uygulamasına şirkete özgü markalamayı nasıl uygulayabileceğinizi öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: esthermsft
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4c8ee2e25d14d6b39cea91255ed955eeb27174d
ms.sourcegitcommit: 5dc3545d7f76ce81598f6b1c9734b0ac0a3e9722
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83690696"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>Intune Şirket Portalı uygulamaları, Şirket Portalı Web sitesini ve Intune uygulamasını özelleştirme

Android üzerinde Şirket Portalı uygulamalar, Şirket Portalı Web sitesi ve Intune uygulaması, kullanıcıların şirket verilerine erişebileceği ve ortak görevleri yapabilecekleri bir uygulamadır. Ortak görev, cihaz kaydetme, uygulama yükleme ve bilgi bulma (BT departmanınızdan yardım gibi) içerebilir. Ayrıca, kullanıcıların şirket kaynaklarına güvenli bir şekilde erişmesini sağlar. Son Kullanıcı deneyimi, giriş, uygulamalar, uygulama ayrıntıları, cihazlar ve cihaz ayrıntıları gibi çeşitli farklı sayfalar sağlar. Şirket Portalı içindeki uygulamaları hızlıca bulmak için uygulamalar sayfasındaki uygulamaları filtreleyebilirsiniz.

## <a name="customizing-the-user-experience"></a>Kullanıcı deneyimini özelleştirme

Son Kullanıcı deneyimini özelleştirerek, son kullanıcılarınız için tanıdık ve yararlı bir deneyim sağlamaya yardımcı olursunuz. Bunu yapmak için, [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' ne gidin ve **Kiracı Yönetimi**  >  **özelleştirmesi**' ni seçin; burada varsayılan ilkeyi düzenleyebilir veya en fazla 10 grup hedefli ilke oluşturabilirsiniz. Bu ayarlar, Android 'de Şirket Portalı uygulamalar, Şirket Portalı Web sitesi ve Intune uygulaması için de geçerlidir.

## <a name="branding"></a>Markalama

Aşağıdaki tabloda son kullanıcı deneyimi için marka özelleştirme ayrıntıları verilmiştir:

| Alan adı | Daha fazla bilgi |
|---|---|---|
| **Kuruluş adı** | Bu ad, son kullanıcı deneyiminde mesajlaşma boyunca görüntülenir. Üst **bilgide göster** ayarı kullanılarak, üstbilgilere görüntülenecek şekilde ayarlanabilir. Maksimum Uzunluk 40 karakterdir. |
| **Renk** | Beş standart renkten seçmek için **Standart** ' ı seçin. Onaltılık kod değerine göre belirli bir rengi seçmek için **özel** ' i seçin. |
| **Tema rengi** | Son Kullanıcı deneyimine göre göstermek için tema rengini ayarlayın. Metin rengini otomatik olarak siyah veya beyaz olarak ayarlayacağız, bu sayede seçtiğiniz tema renginizdeki en üstünde görünür. |
| **Üst bilgide göster** | Son Kullanıcı deneyimlerinde bulunan üstbilginin **kuruluş logosu ve adı**, **yalnızca kuruluş logosu**veya **yalnızca kuruluş adını**görüntülemesi gerekip gerekmediğini seçin. Aşağıdaki önizleme kutuları, adı değil yalnızca logoları gösterir.  |
| **Tema rengi arka planı için logoyu karşıya yükle** | Seçtiğiniz Tema renginiz üzerinde göstermek istediğiniz logoyu karşıya yükleyin. En iyi görünüm için saydam bir arka plana sahip bir logo yükleyin. Bunun, ayarın altındaki Önizleme kutusunda nasıl görüneceğini görebilirsiniz.<p>Maksimum görüntü boyutu: 400 x 400 piksel<br>En büyük dosya boyutu: 750KB<br>Dosya türü: PNG, JPG veya JPEG |
| **Beyaz veya hafif arka plan için logoyu karşıya yükle** | Beyaz veya hafif renkli arka planların üzerine göstermek istediğiniz logoyu karşıya yükleyin. En iyi görünüm için saydam bir arka plana sahip bir logo yükleyin. Bunun, ayarın altındaki Önizleme kutusunda beyaz bir arka plana nasıl görüneceğini görebilirsiniz.<p>Maksimum görüntü boyutu: 400 x 400 piksel<br>En büyük dosya boyutu: 750 KB<br>Dosya türü: PNG, JPG veya JPEG |
| **Marka görüntüsünü karşıya yükle** | Kuruluşunuzun markasını yansıtan bir görüntü yükleyin.<p><ul><li>Önerilen Görüntü genişliği: 1125 piksel 'den büyük (en az 650 piksel olması gerekir)</li><li>En büyük görüntü boyutu: 1,3 MB</li><li>Dosya türü: PNG, JPG veya JPEG</li><li>Şu konumlarda görüntülenir:</li><ul><li>iOS/ıpados Şirket Portalı: kullanıcının profil sayfasında arka plan resmi.</li><li>Şirket Portalı Web sitesi: kullanıcının profil sayfasında arka plan resmi.</li><li>Android Intune uygulaması: çekmecede, kullanıcının profil sayfasında bir arka plan görüntüsü olarak.</li></ul></ul> |

> [!NOTE]
> Bir Kullanıcı Şirket Portalı bir iOS/ıpados uygulaması yüklerken bir istem alır. Bu durum, iOS/ıpados uygulamasının bir toplu satın alma programı (VPP) ile bağlantılı veya iş kolu (LOB) uygulamasına bağlı olan App Store 'a bağlanması durumunda meydana gelir. İstem, kullanıcıların eylemi kabul etmesine veya uygulamanın yönetimine izin veriyor. İstem şirketinizin adını gösterir veya şirketinizin adı kullanılamadığında **Şirket portalı** görüntülenir.

### <a name="brand-image-best-practices"></a>Marka resmi en iyi uygulamaları

Doğru marka resmi, kuruluşunuzun markasının sağlam bir şekilde bir fikir sunarak kullanıcının güvenini geliştirebilir. Görüntü konumları için görüntüyü alma, seçme ve iyileştirmeyle ilgili düşünmek isteyebileceğiniz bazı ipuçları aşağıda verilmiştir.

- Pazarlama veya sanat departmanınıza ulaşın. Bu departmanların elinde zaten onaylanmış birkaç marka imajı olabilir. Departmanlar ayrıca görüntüleri ihtiyaca göre iyileştirme konusunda size yardım edebilir.
- Yatay ve dikey kompozisyonları değerlendirin. İmajın odak noktasını çevreleyen arka planın yeterli olmasına dikkat edin. İmaj cihaz boyutuna, hizalamasına ve platformuna göre farklı şekillerde kırpılabilir.
- Sıradan, hazır bir imaj seçmekten kaçının. Görüntü, kuruluşunuzun markasını ve kullanıcılara tanıdık olduğunu yansıtmalıdır. Bir tane yoksa, bir tane kullanmaktan, kullanıcılarınız için bir anlamı olmayan bir genel kullanım kullanmaktan daha iyidir.
- Gereksiz meta verileri kaldırın. İmaj dosyası; kamera profili, coğrafi konum, başlık, açıklama gibi meta veriler içerebilir. Kaliteyi korumak ve dosya boyutu sınırını aşmamak için bir görüntü iyileştirme aracını kullanarak bu bilgileri kaldırın.

### <a name="brand-image-examples"></a>Marka imajı örnekleri

Aşağıdaki görüntüde bir iPhone 'daki marka görüntüsüne bir örnek gösterilmektedir:

<img alt="Screenshot of example iPhone branding image" src="./media/company-portal-app/company-portal-app-01.png" width="250">

Aşağıda, Android için Intune uygulamasındaki marka görüntüsünün bir örneği gösterilmektedir:

<img alt="Screenshot of example #1 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-02.png" width="250">

<img alt="Screenshot of example #2 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-03.png" width="250">

## <a name="support-information"></a>Destek bilgileri

Çalışanların sorularla iletişime geçebilmesi için kuruluşunuzun destek bilgilerini girin. Bu destek bilgileri, destek, **yardım & destek**ve son kullanıcı deneyimi genelinde Yardım **masası** **sayfaları üzerinde görüntülenir**.

| Alan adı | Maksimum uzunluk | Daha fazla bilgi |
|------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kişi adı | 40 | Bu ad, kullanıcıların destek ekibiyle iletişime geçebilecekleri kişidir. |
| Telefon numarası | 20 | Bu sayı, kullanıcıların destek için çağrı yapmasına olanak sağlar. |
| E-posta adresi | 40 | Bu e-posta adresi, kullanıcıların destek için e-posta gönderebilecekleri yerdir. `alias@domainname.com` biçiminde geçerli bir e-posta adresi girmeniz gerekir. |
| Web sitesinin adı | 40 | Bu, destek web sitesinin URL 'SI için bazı konumlarda görüntülenen kolay addır. Bir destek web sitesi URL 'SI belirtirseniz ve kolay bir ad yoksa, URL 'nin kendisi Son Kullanıcı deneyimlerinde görüntülenir.  |
| Web sitesi URL'si | 150 | Kullanıcıların kullanması gereken destek web sitesi. URL biçiminde olmalıdır `https://www.contoso.com` .  |
| Ek bilgiler | 120 | Kullanıcılara daha fazla destekle ilgili tüm iletileri ekleyin. |

## <a name="configuration"></a>Yapılandırma

Şirket Portalı deneyimini, özellikle kayıt, gizlilik, bildirimler, uygulama kaynakları ve self servis eylemleri için yapılandırabilirsiniz.

### <a name="enrollment"></a>Kayıt

Aşağıdaki tabloda kayda özgü yapılandırma ayrıntıları verilmiştir:

| Alan adı | Maksimum uzunluk | Daha fazla bilgi |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cihaz kaydı | Yok | Kullanıcıların mobil cihaz yönetimine kaydolmasını ve nasıl sorulup sorulmayacağını belirtin. Daha fazla bilgi için bkz. [cihaz kayıt ayarı seçenekleri](../apps/company-portal-app.md#device-enrollment-setting-options). |

#### <a name="device-enrollment-setting-options"></a>Cihaz kayıt ayarı seçenekleri

> [!NOTE]
> Cihaz kayıt ayarı için destek, son kullanıcıların bu Şirket Portalı sürümlerine sahip olmasını gerektirir:
> - İOS/ıpados üzerinde Şirket Portalı: sürüm 4,4 veya üzeri
> - Android üzerinde Şirket Portalı: sürüm 5.0.4715.0 veya üzeri 

|    Cihaz kayıt seçenekleri    |    Açıklama    |    Denetim listesi istemleri    |    Bildirim    |    Cihaz ayrıntıları durumu    |    Uygulama ayrıntıları durumu (kayıt gerektiren bir uygulama)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    Kullanılabilir, istemlerle    |    Tüm olası konumlara kaydolmak için istemlerle ilgili varsayılan deneyim.    |    Yes    |    Yes    |    Yes    |    Yes    |
|    Kullanılabilir, istem yok    |    Kullanıcı, geçerli cihazlarından veya kayıt gerektiren uygulamalardan cihaz ayrıntıları ' nda durum aracılığıyla kaydedebilir.    |    Hayır    |    Hayır    |    Yes    |    Yes    |
|    Kullanılamaz    |    Kullanıcıların kaydolmasına yol yoktur.    |    Hayır    |    Hayır    |    Hayır    |    Hayır<sup>(1)</sup>    |

<sup>(1)</sup> **bilinen sorun:** uygulamaları yüklemek için kayıt gerektirecek şekilde ayarlarsanız ve ayrıca cihaz kaydını "kullanılamaz" olarak ayarlarsanız, Android 'deki Şirket portalı uygulaması, kullanıcıların kaydolmasına kılavuzluk eder. Bu, kısa süre içinde kaldırılacak.

### <a name="privacy"></a>Gizlilik

Aşağıdaki tabloda gizlilik 'e özgü yapılandırma ayrıntıları verilmiştir:

| Alan adı | Maksimum uzunluk | Daha fazla bilgi |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Gizlilik bildirimi URL'si | 79 | Kullanıcılar gizlilik bağlantılarına tıkladığı zaman görüntülenecek şekilde kuruluşunuzun gizlilik bildirimini ayarlayın. `https://www.contoso.com` biçiminde geçerli bir URL girmeniz gerekir. |
| İOS/ıpados için Şirket Portalı gizlilik iletisi | 520 | Kuruluşunuzun yönetilen iOS/ıpados cihazlarında göremediği öğeleri listelemek için **Varsayılanı** değiştirmeyin veya **özel** bir ileti ayarlayın. Marku kullanarak madde işaretleri, kalın, italik ve bağlantılar ekleyebilirsiniz. Kullanıcılar ayrıca kuruluşunuzun görebileceği ve yapabileceğinize ilişkin bir liste görür, ancak bu liste Intune tarafından otomatik olarak oluşturulur ve özelleştirilemez. |

### <a name="device-ownership-notification"></a>Cihaz sahipliği bildirimi

Aşağıdaki tabloda bildirime özgü yapılandırma ayrıntıları verilmiştir:

| Alan adı | Maksimum uzunluk | Daha fazla bilgi |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cihaz sahiplik türü kişisel 'den şirkete (yalnızca Android ve iOS/ıpados) değiştirildiğinde kullanıcılara anında iletme bildirimi gönderin | Yok | Hem Android hem de iOS Şirket Portalı kullanıcılarınıza cihaz sahiplik türü kişisel ' e değiştirildiğinde, anında iletme bildirimi gönderin. Varsayılan olarak, bu anında iletme bildirimi off olarak ayarlanır. Cihaz sahipliği kurumsal sahiplik olarak ayarlandığında, Intune cihaza daha fazla erişim sahibi olur. Bu, tam uygulama envanteri, Filekasası anahtar döndürme, telefon numarası alma ve birkaç uzak eylem seçme işlemlerini içerir. Daha fazla bilgi için bkz. [cihaz sahipliğini değiştirme](../enrollment/corporate-identifiers-add.md#change-device-ownership).  |

### <a name="app-sources"></a>Uygulama kaynakları

Şirket Portalı, hangi ek uygulama kaynaklarının gösterildiğini seçebilirsiniz. Aşağıdaki tabloda, uygulama kaynağına özgü yapılandırma ayrıntıları verilmiştir:

| Alan adı | Maksimum uzunluk | Daha fazla bilgi |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Azure AD kurumsal uygulamaları | Yok | Her son kullanıcı için Şirket Portalı **Azure AD kurumsal uygulamalarını** görüntülemek üzere **Gizle** veya **göster** ' i seçin. Daha fazla bilgi için bkz. [Uygulama kaynağı ayarı seçenekleri](../apps/company-portal-app.md#app-source-setting-options). |
| Office Online Uygulamaları | Yok | Her son kullanıcı için Şirket Portalı **Office Online uygulamalarını** görüntülemek üzere **Gizle** veya **göster** ' i seçin. Daha fazla bilgi için bkz. [Uygulama kaynağı ayarı seçenekleri](../apps/company-portal-app.md#app-source-setting-options). |

#### <a name="app-source-setting-options"></a>Uygulama kaynağı ayarı seçenekleri

> [!NOTE]
> Şirket Portalı Web sitesi, ilk olarak diğer Microsoft hizmetlerinden uygulamaların görüntülenmesini destekler.

Her son kullanıcı için Şirket Portalı **Azure AD kurumsal uygulamalarını** ve **Office Online uygulamalarını** gizleyebilir veya gösterebilirsiniz. **Göster** , Şirket portalı, kullanıcıya atanan seçili Microsoft hizmetinden tüm uygulama kataloğunun görüntülenmesine neden olur. **Azure AD kurumsal uygulamaları** [Azure Portal](https://portal.azure.com)aracılığıyla kaydedilir ve atanır. **Office Online Uygulamaları** , [M365 Yönetim merkezinde](https://admin.microsoft.com)bulunan lisanslama denetimleri kullanılarak atanır. Bu yapılandırma ayarını bulmak için [Microsoft Uç Nokta Yöneticisi Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)' nde **Kiracı Yönetimi**  >  **özelleştirmesi** ' nı seçin. Varsayılan olarak, her bir ek uygulama kaynağı **gizleyecek**şekilde ayarlanır. 

### <a name="customizing-user-self-service-actions-for-the-company-portal"></a>Şirket Portalı için Kullanıcı self servis eylemlerini özelleştirme

Şirket Portalı uygulamasında ve Web sitesinde son kullanıcılara gösterilen kullanılabilir self servis cihaz eylemlerini özelleştirebilirsiniz. İstenmeyen cihaz eylemlerini önlemeye yardımcı olmak için **Kiracı Yönetimi**özelleştirmesi ' nı seçerek Şirket portalı uygulamasının ayarlarını yapılandırabilirsiniz  >  **Customization**. 

Aşağıdaki eylemler kullanılabilir:
- Kurumsal Windows cihazlarında **Kaldır** düğmesini gizleyin.
- Kurumsal Windows cihazlarında **sıfırlama** düğmesini gizleyin.
- Kurumsal iOS/ıpados cihazlarında **Kaldır** düğmesini gizleyin.
- Kurumsal iOS/ıpados cihazlarında **sıfırlama** düğmesini gizleyin.

> [!NOTE]
> Bu eylemler, Şirket Portalı uygulaması ve Web sitesindeki cihaz eylemlerini kısıtlamak ve herhangi bir cihaz kısıtlama ilkesi uygulamamayı yapmak için kullanılabilir. Kullanıcıların, ayarlardan fabrika sıfırlaması veya MDM kaldırma gerçekleştirmesini kısıtlamak için, cihaz kısıtlama ilkelerini yapılandırmanız gerekir. 

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>İOS/ıpados cihazları için türetilmiş kimlik bilgilerini Şirket Portalı

Intune, kişisel kimlik doğrulama (PıV) ve ortak erişim kartı (CAC) ile birlikte gelen kimlik bilgilerini, DıŞA geçmiş kimlik bilgisi sağlayıcıları, Entrust Datacard ve ıntercede ile iş ortaklığı için destekler. Son kullanıcılar, Şirket Portalı uygulamasındaki kimliklerini doğrulamak için iOS/ıpados cihazının kayıt sonrası ek adımlara geçer. Türetilmiş kimlik bilgileri, önce kiracınız için bir kimlik bilgisi sağlayıcısı ayarlayıp, ardından kullanıcılara veya cihazlara türetilmiş kimlik bilgilerini kullanan bir profili hedefleyerek kullanıcılara etkinleştirilir.

> [!NOTE]
> Kullanıcı, Intune aracılığıyla belirttiğiniz bağlantıya bağlı olarak türetilmiş kimlik bilgileri hakkındaki yönergeleri görür.

İOS/ıpados cihazlarının türetilmiş kimlik bilgileri hakkında daha fazla bilgi için bkz. [Microsoft Intune türetilmiş kimlik bilgilerini kullanma](../protect/derived-credentials.md).

## <a name="dark-mode-for-iosipados-company-portal"></a>İOS/ıpados Şirket Portalı için koyu mod

İOS/ıpados Şirket Portalı için koyu mod kullanılabilir. Kullanıcılar uygulamaları indirebilir, cihazlarını yönetebilir ve cihaz ayarlarına bağlı olarak tercih ettikleri renk düzeninde BT desteği alabilir. İOS/ıpados Şirket Portalı, son kullanıcının cihaz ayarlarını koyu veya hafif modda otomatik olarak eşleştirecektir.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Windows Şirket Portalı klavye kısayolları

Son kullanıcılar, Windows Şirket Portalı’nda klavye kısayollarını (hızlandırıcılar) kullanarak gezinti, uygulama ve cihaz eylemlerini tetikleyebilirler.

Windows Şirket Portalı uygulamasında aşağıdaki kısayollar kullanılabilir.

| Alan | Açıklama | Klavye kısayolu |
|:------------------:|:--------------:|:-----------------:|
| Gezinti menüsü | Gezinti | Alt+M |
|  | Giriş Sayfası | Alt+H |
|  | Tüm uygulamalar | Alt+A |
|  | Yüklenen uygulamalar | Alt+I |
|  | Geri bildirim gönder | Alt+F |
|  | Profilim | Alt+U |
|  | Ayarlar | Alt+T |
| Giriş - Cihaz kutucuğu | Rename | F2 |
|  | Kaldır | Ctrl+D veya Delete |
|  | Erişimi denetleme | Ctrl+M veya F9 |
| Cihaz ayrıntıları | Rename | F2 |
|  | Kaldır | Ctrl+D veya Delete |
|  | Erişimi denetleme | Ctrl+M veya F9 |
| Uygulama ayrıntıları | Yükleme | Ctrl+I |
| Cihazlar | Kullanılabilir | Ctrl+D |

Son kullanıcılar, Windows Şirket Portalı uygulamasında kullanılabilen kısayolları da görebilir.

![Windows Şirket Portalı'nda kullanılabilen kısayolların ekran görüntüsü](./media/company-portal-app/company-portal-app-04.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Şirket Portalı Kullanıcı self servis cihaz eylemleri

Kullanıcılar, Android 'de Şirket Portalı uygulama, Şirket Portalı Web sitesi veya Intune uygulaması aracılığıyla yerel veya uzak cihazlarında eylemler gerçekleştirebilir. Bir kullanıcının gerçekleştirebileceği eylemler cihaz platformu ve yapılandırmasına göre farklılık gösterir. Her durumda, uzak cihaz eylemleri yalnızca cihazın birincil kullanıcısı tarafından gerçekleştirilebilir.  

Kullanılabilir self servis cihaz eylemleri şunları içerir:

- **Devre dışı bırak** – cihazı Intune yönetiminden kaldırır. Şirket portalı uygulamasında ve Web sitesinde bu, **Kaldır**olarak gösterilir.
- **Silme** – bu eylem bir cihaz sıfırlamayı başlatır. Şirket portalı Web sitesinde bu, **Sıfırla**veya IOS/ıpados Şirket portalı uygulamasında **Fabrika Sıfırlaması** olarak gösterilir.
- **Yeniden Adlandır** – bu eylem, kullanıcının şirket portalı görebileceği cihaz adını değiştirir. Yerel cihaz adını değiştirmez, yalnızca Şirket Portalı listelemez.
- **Eşitleme** – bu eylem, Intune hizmeti ile bir cihaz iade işlemini başlatır. Bu, Şirket Portalı **denetim durumunu** gösterir.
- **Uzaktan kilitleme** – bu, cihazın kilidini açmak için PIN gerektiren cihazı kilitler.
- **Geçiş kodunu Sıfırla** – bu eylem, cihaz geçiş kodunu sıfırlamak için kullanılır. İOS/ıpados cihazlarında geçiş kodu kaldırılır ve son kullanıcının ayarlar ' da yeni bir kod girmesi gerekecektir. Desteklenen Android cihazlarda Intune tarafından yeni bir geçiş kodu oluşturulur ve geçici olarak Şirket Portalı görüntülenir.
- **Anahtar kurtarma** – bu eylem, Şirket portalı Web sitesinden şifrelenmiş MacOS cihazları için kişisel kurtarma anahtarını kurtarmak üzere kullanılır. 

Kullanılabilir Kullanıcı self servis eylemlerini özelleştirmek için bkz. [Şirket portalı için Kullanıcı self servis eylemlerini özelleştirme](../apps/company-portal-app.md#customizing-user-self-service-actions-for-the-company-portal).

### <a name="self-service-actions"></a>Self Servis eylemleri

Bazı platformlar ve Konfigürasyonlar self servis cihaz eylemlerine izin vermez. Aşağıdaki tabloda self servis eylemleri hakkında daha ayrıntılı bilgi verilmektedir:

|  | Windows 10<sup>(3)</sup> | iOS/ıpados<sup>(3)</sup> | MacOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Devre Dışı Bırakma | Kullanılabilir<sup>(1)</sup> | Kullanılabilir | Kullanılabilir | Kullanılabilir<sup>(7)</sup> |
| Silme | Kullanılabilir | Kullanılabilir<sup>(5)</sup> | NA | Kullanılabilir<sup>(7)</sup> |
| Yeniden Adlandır<sup>(4)</sup> | Kullanılabilir | Kullanılabilir | Kullanılabilir | Kullanılabilir |
| Sync | Kullanılabilir | Kullanılabilir | Kullanılabilir | Kullanılabilir |
| Uzaktan Kilitleme | Yalnızca Windows Phone | Kullanılabilir | Kullanılabilir | Kullanılabilir |
| Geçiş kodunu Sıfırla | Yalnızca Windows Phone | Kullanılabilir<sup>(8)</sup> | NA | Kullanılabilir<sup>(6)</sup> |
| Anahtar Kurtarma | NA | NA | Kullanılabilir<sup>(2)</sup> | NA |

<sup>(1)</sup> **devre dışı BıRAKMA** , Azure AD 'ye katılmış Windows cihazlarında her zaman engellenir.<br>
<sup>(2)</sup> MacOS Için **anahtar kurtarma** yalnızca Web portalı aracılığıyla kullanılabilir.<br>
<sup>(3)</sup> bir cihaz kayıt yöneticisi kaydı kullanılıyorsa tüm uzak eylemler devre dışı bırakılır.<br>
<sup>(4)</sup> **yeniden adlandırma** yalnızca cihaz adını cihazda değil şirket portalı uygulamasında veya Web portalında değiştirir.<br>
<sup>(5)</sup> Kullanıcı kayıtlı IOS/ıpados cihazlarında **silme** işlemi kullanılamıyor.<br>
<sup>(6)</sup> bazı Android ve Android kurumsal yapılandırmalarında, **geçiş kodu sıfırlama** işlemi desteklenmez. Daha fazla bilgi için bkz. [Intune 'da cihaz geçiş kodunu sıfırlama veya kaldırma](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> **devre dışı bırakma** ve **Temizleme** , ANDROID kurumsal cihaz sahibi senaryolarında (Cope, Cobo, cosu) kullanılamaz.<br>
<sup>(8)</sup> Kullanıcı kayıtlı IOS/ıpados cihazlarında **geçiş kodunu sıfırlama** işlemi desteklenmez.

### <a name="app-logs"></a>Uygulama günlükleri

Azure Kamu kullanıyorsanız, bir sorunla ilgili yardım alma sürecini başlattığında bunu nasıl paylaşacağına karar vermesi için son kullanıcıya uygulama günlükleri sunulur. Ancak, Azure Kamu 'yu kullanmıyorsanız, Kullanıcı bir sorunla ilgili yardım almak için işlemi başlattığında Şirket Portalı uygulama günlüklerini doğrudan Microsoft 'a gönderir. Uygulama günlüklerini Microsoft'a göndermek sorunları gidermeyi ve çözmeyi kolaylaştıracaktır.

> [!NOTE]
> Microsoft ve Apple ilkesiyle tutarlı olan her nedenden dolayı hizmetimiz tarafından toplanan herhangi bir veriyi üçüncü taraflardan satmayacağız.

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Edge 'de yeni sekme sayfaları için kuruluşunuzun logosunu ve marka rengini yapılandırın](../apps/manage-microsoft-edge.md#configure-your-organizations-logo-and-brand-color-for-new-tab-pages-in-microsoft-edge)
- [Uygulamaları ekleme](apps-add.md)
