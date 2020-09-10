---
title: Microsoft Intune’da uygulama yönetimi nedir?
titleSuffix: ''
description: Microsoft Intune tarafından sağlanan platforma göre istemci uygulaması yönetim özellikleri hakkında bilgi edinin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/03/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7061fbba1171615b265abd895c9c1d30c64d8bfe
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643594"
---
# <a name="what-is-microsoft-intune-app-management"></a>Microsoft Intune uygulama yönetimi nedir?

BT yöneticisi olarak Microsoft Intune'u şirketinizin iş gücünün kullandığı istemci uygulamaları yönetmek için kullanabilirsiniz. Bu işlev, cihazları yönetmeye ve verileri korumaya ek niteliğindedir. Yöneticinin önceliklerinden biri, son kullanıcıların işlerini yapabilmeleri için gereken uygulamalara erişimleri olduğundan emin olmaktır. Bu amaca ulaşmak zor olabilir çünkü:
- Çok çeşitli cihaz platformları ve uygulama türleri vardır.
- Hem şirket cihazlarındaki hem de kullanıcıların kişisel cihazlarındaki uygulamaları yönetmeniz gerekebilir.
- Ağınızın ve verilerinizi güvenli kaldığından emin olmanız gerekir.

Buna ek olarak, Intune’a kaydolmamış cihazlarda uygulamaları atamak ve yönetmek isteyebilirsiniz.

## <a name="mobile-application-management-mam-basics"></a>Mobil uygulama yönetimi (MAM) temelleri

[Intune mobil uygulama yönetimi](app-lifecycle.md), kullanıcılarınız için mobil uygulamaları yayımlama, gönderme, yapılandırma, güvenlik altına alma, izleme ve güncelleştirme gibi eylemler gerçekleştirmenize olanak tanıyan Intune yönetim özellikleri paketini ifade eder.

MAM, kuruluşunuzun verilerini bir uygulama içinde yönetmenizi ve korumanızı sağlar. **Kayıt olmadan mam** (mam-we) ile, hassas veriler içeren iş veya okul ile ilgili bir uygulama, **kendi cihazını getir** (KCG) senaryolarında kişisel cihazlar dahil olmak üzere neredeyse her [cihazda](app-management.md#app-management-capabilities-by-platform)yönetilebilir. Microsoft Office uygulamaları gibi birçok üretkenlik uygulaması Intune MAM tarafından yönetilebilir. Genel kullanıma sunulan [Microsoft Intune korunan uygulamaların](apps-supported-intune-apps.md) resmi listesine bakın.

Intune MAM iki yapılandırmayı destekler:

- **Intune MDM + MAM**: BT yöneticileri, yalnızca Intune mobil cihaz yönetiminde (MDM) kayıtlı cihazlarda MAM ve uygulama koruma ilkelerini kullanarak uygulamaları yönetebilir. MDM + MAM kullanarak uygulamaları yönetmek için, müşterilerin [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde Intune kullanması gerekir.
- **Cihaz kaydı olmadan MAM**: Cihaz kaydı olmadan MAM ya da diğer adıyla MAM-WE, BT yöneticilerinin Intune MDM’de kayıtlı olmayan cihazlarda MAM ve uygulama koruma ilkelerini kullanarak uygulamaları yönetmesine olanak sağlar. Bu, uygulamaların üçüncü taraf EMM sağlayıcılarında kayıtlı cihazlarda Intune tarafından yönetilebileceği anlamına gelir. Uygulamaları MAM-WE kullanarak yönetmek için, müşterilerin [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'nde Intune kullanması gerekir. Ayrıca uygulamalar, üçüncü taraf Enterprise Mobility Management (EMM) sağlayıcıları ile kaydedilmiş veya hiçbir MDM ile kaydedilmemiş cihazlarda uygulamalar Intune ile yönetilebilir. KCG ve Microsoft 'un EMS hakkında daha fazla bilgi için, [Microsoft Enterprise Mobility + Security (EMS) ile KCG 'yi etkinleştirmek Için teknoloji kararları](../fundamentals/byod-technology-decisions.md)bölümüne bakın.

## <a name="app-management-capabilities-by-platform"></a>Platforma göre uygulama yönetimi özellikleri

Intune, ihtiyacınız olan uygulamaları çalıştırmak istediğiniz cihazlara almanıza yardımcı olacak çeşitli özellikler sunar. Aşağıdaki tablo, uygulama yönetimi özelliklerinin bir özetini sağlar.

| Uygulama yönetimi özelliği | Android/Android Kurumsal | iOS/iPadOS | macOS | Windows 10 |
|-------------------------- | -------------------------- | ---------- | ----- | ---------- |
| Cihazlara ve kullanıcılara uygulamaları ekleme ve atama | Yes | Yes | Yes | Yes |
| Intune’a kayıtlı olmayan cihazlara uygulamaları atama | Yes | Yes | Hayır | Hayır |  |
| Uygulamaların başlangıç davranışını denetlemek için uygulama yapılandırma ilkelerini kullanma | Yes | Yes | Hayır | Hayır |
| Süresi dolan uygulamaları yenilemek için mobil uygulama sağlama ilkelerini kullanma | Hayır | Yes | Hayır | Hayır |
| Uygulama koruma ilkeleriyle uygulamalardaki şirket verilerini koruma | Yes | Yes | Hayır | Hayır <sup>1</sup> |
| Yüklü uygulamadan yalnızca şirket verilerini kaldırma (uygulama seçmeli silme) | Yes | Yes | Hayır | Yes |
| Uygulama atamalarını izleme | Yes | Yes | Yes | Yes |
| Uygulama mağazasından toplu satın alınan uygulamaları atama ve izleme | Hayır | Hayır | Hayır | Yes |
| Cihazlara uygulamaları zorunlu yükleme (gerekli) <sup>2</sup> | Yes | Yes | Yes | Yes |
| Şirket Portalı’ndan cihazlara isteğe bağlı yükleme (kullanılabilir yükleme) | Evet <sup>3</sup> | Yes | Yes | Yes |
| Web’deki bir uygulamanın kısayolunu yükleme (web bağlantısı) | Evet <sup>4</sup> | Yes | Yes | Yes |
| Şirket içi (iş kolu) uygulamaları | Yes | Yes | Yes | Yes |
| Mağazadan uygulamalar | Yes | Yes | Hayır | Yes |
| Uygulamaları güncelleştirme | Yes | Yes | Hayır | Yes |

<sup>1</sup> Windows 10 çalıştıran cihazlarda uygulamaları korumak için [Windows Bilgi Koruması](../protect/windows-information-protection-configure.md)’nu kullanmayı göz önüne alabilirsiniz.<br>
<sup>2</sup> Yalnızca Intune tarafından yönetilen cihazlar için geçerlidir.<br>
<sup>3</sup> Intune, Android Kurumsal cihazlarda Yönetilen Google Play mağazasında kullanılabilen uygulamaları destekler.<br>
<sup>4</sup> Intune, standart Android Kurumsal cihazlarda web bağlantısı biçiminde uygulama kısayolu yüklenmesi seçeneğini sunmaz. Ancak web bağlantısı desteği [çoklu uygulama için ayrılmış Android Kurumsal cihazlarında](../configuration/device-restrictions-android-for-work.md#device-experience) desteklenir. 


## <a name="get-started"></a>Kullanmaya başlayın

Uygulamalarla ilgili birçok bilgiyi **uygulamalar** iş yükünde bulabilirsiniz ve aşağıdakileri yaparak erişebilirsiniz:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Uygulamalar**' ı seçin.

    ![Uygulamalar iş yükü bölmesi](./media/app-management/apps-workload.png)

Uygulamalar iş yükü, genel uygulama bilgilerine ve işlevlerine erişim için bağlantılar sağlar. 

Uygulama iş yükü gezinti menüsünün en üst kısmında, yaygın olarak kullanılan uygulama ayrıntıları sağlanır:
- **Genel bakış**: kiracı adını, MDM yetkilisini, kiracı konumunu, hesap durumunu, uygulama yükleme durumunu ve uygulama koruma ilkesi durumunu görüntülemek için bu seçeneği belirleyin.
- **Tüm uygulamalar**: kullanılabilir tüm uygulamaların listesini göstermek için bu seçeneği belirleyin. Bu sayfadan başka uygulamalar ekleyebilirsiniz. Ayrıca, her bir uygulamanın durumunu ve her uygulamanın atanıp atanmadığını da görebilirsiniz. Daha fazla bilgi için bkz. [uygulama ekleme](apps-add.md) ve [uygulama atama](apps-deploy.md).
- **Uygulamaları izleme**
    - **Uygulama lisansları**: Uygulama mağazalarından toplu satın alınan uygulamaları görüntüleyin, atayın ve izleyin. Daha fazla bilgi için bkz. [iOS toplu satın alınan program (VPP) uygulamaları](vpp-apps-ios.md) ve [Microsoft Store iş toplu satın alınan uygulamalar için](windows-store-for-business.md).
    - **Bulunan uygulamalar**: Intune tarafından atanan veya bir cihaza yüklenen uygulamaları görüntüleyin. Daha fazla bilgi için bkz. [Intune bulunan uygulamalar](app-discovered-apps.md).
    - **Uygulama yüklemesi durumu**: oluşturduğunuz uygulama atamasının durumunu görüntüleyin. Daha fazla bilgi için bkz. [Microsoft Intune ile uygulama bilgilerini ve atamalarını izleme](apps-monitor.md#device-and-user-status-graphs).
    - **Uygulama koruma durumu**: Seçtiğiniz kullanıcı için uygulama koruma ilkesinin durumunu görüntüleyin.
- **Platforma göre**: kullanılabilir uygulamaları platforma göre görüntülemek için bu platformları seçin.
    - Windows
    - iOS
    - macOS
    - Android
- **İlke**:
    - **Uygulama koruma ilkeleri**: Ayarları uygulamayla ilişkilendirmek ve kullandığı şirket verilerini korumaya yardımcı olmak için bu seçeneği seçin. Örneğin, bir uygulamanın diğer uygulamalarla iletişim kurma özelliklerini kısıtlayabilir veya kullanıcının şirket uygulamasına erişmek için PIN girmesini isteyebilirsiniz. Daha fazla bilgi için bkz. [Uygulama koruma ilkeleri](app-protection-policies.md).
    - **Uygulama yapılandırma ilkeleri**: Kullanıcı bir uygulama çalıştırdığında gerekebilecek ayarları sağlamak için bu ayarı kullanın. Daha fazla bilgi için bkz. [uygulama yapılandırma ilkeleri](app-configuration-policies-use-ios.md), [iOS uygulama yapılandırma ilkeleri](app-configuration-policies-use-ios.md)ve [Android uygulama yapılandırma ilkeleri](app-configuration-policies-overview.md).
    - **iOS uygulama sağlama profilleri**: iOS uygulamaları, bir sağlama profili ve bir sertifika tarafından imzalanmış kod içerir. Sertifikanın süresi dolduğunda, uygulama artık çalıştırılamaz. Intune size süresi dolmak üzere olan uygulamaların bulunduğu cihazlara yeni sağlama profili ilkesini önceden atamak için araçlar verir. Daha fazla bilgi için bkz. [iOS uygulama sağlama profilleri](app-provisioning-profile-ios.md).
    - **S modu ek ilkeleri**: yönetilen S modundaki cihazlarınızda çalışacak ek uygulamalar yetkilendirmek için bu seçeneği belirleyin. Daha fazla bilgi için bkz. [S modu ek ilkeleri](apps-win32-s-mode.md).
    - **Office uygulamalarına yönelik ilkeler**: Microsoft 365 hizmetlerine bağlanan Office mobil uygulamaları için mobil uygulama yönetimi ilkeleri oluşturmak üzere bu seçeneği belirleyin. İOS için Outlook ve karma modern kimlik doğrulamasıyla etkinleştirilmiş Android için Intune uygulama koruma ilkeleri oluşturarak şirket içi Exchange posta kutularına erişimi de koruyabilirsiniz. Office uygulamalarına yönelik ilkeleri kullanmak için gereksinimleri karşılamanız gerekir. Gereksinimler hakkında daha fazla bilgi için bkz. [Office bulut ilkesi hizmetini kullanma gereksinimleri](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service). Uygulama koruma ilkeleri, şirket içi Exchange veya SharePoint hizmetlerine bağlanan diğer uygulamalar için desteklenmez. İlgili bilgiler için bkz. [Enterprise için Microsoft 365 uygulamaları Için Office bulut İlkesi Hizmeti 'Ne genel bakış](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service).
    - **İlke kümeleri**: Bu seçeneği, oluşturduğunuz uygulama, ilke ve diğer yönetim nesnelerinin atanabilir bir koleksiyonunu oluşturmak için seçin. Daha fazla bilgi için bkz. [ilke kümeleri](../fundamentals/policy-sets.md).
- **Diğer**:   
    - **Uygulama seçmeli silme**: Seçili bir kullanıcının cihazından yalnızca şirket verilerini kaldırmak için bu seçeneği kullanın. Daha fazla bilgi için bkz. [uygulama seçmeli silme](apps-selective-wipe.md).
    - **Uygulama kategorileri**: Uygulama kategorisi adlarını ekleyin, sabitleyin ve silin.
    - **E-kitaplar**: bazı uygulama depoları, şirketinizde kullanmak istediğiniz bir uygulama veya kitap için birden fazla lisans satın almanıza olanak sağlar. Daha fazla bilgi için bkz. [Toplu satın alınan uygulama ve kitapları Microsoft Intune ile yönetme](vpp-apps.md).
- **Yardım ve destek**: Sorun giderin, destek isteyin veya Intune durumunu görüntüleyin. Daha fazla bilgi için bkz. sorun [giderme](../fundamentals/help-desk-operators.md).

### <a name="try-the-interactive-guide"></a>Etkileşimli Kılavuzu deneyin
[Microsoft Uç Nokta Yöneticisi ile mobil ve masaüstü uygulamalarını yönetme ve koruma](https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager) Etkileşimli Kılavuzu, Intune 'a kayıtlı cihazların nasıl yönetileceğini, ilkelerle uyumluluğu zorunlu kılmak ve kuruluşunuzun verilerini korumak Için Microsoft Uç Nokta Yöneticisi Yönetim Merkezi 'nde size adım adım yol gösterir.</br></br>

<div align=”center”>
<iframe allowfullscreen width="95%" height="450" src="https://mslearn.cloudguides.com/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager" frameborder="0" scrolling="no"/></iframe>
</div>

## <a name="additional-information"></a>Ek bilgiler
Konsolun içindeki aşağıdaki öğeler uygulamayla ilgili işlevsellik sağlar:
- **İş İçin Microsoft Mağazası**: İş İçin Microsoft Mağazası’na tümleştirmeyi kurun. Bundan sonra, satın alınan uygulamaları Intune’a eşitleyebilir, bunları atayabilir ve lisans kullanımınızı izleyebilirsiniz. Daha fazla bilgi için, bkz. [iş toplu satın alınan uygulamalar için Microsoft Store](windows-store-for-business.md).
- **Windows Enterprise sertifikası**: Yönetilen Windows cihazlarınıza iş kolu uygulamalarını dağıtmak için kullanılan kod imzalama sertifikasını uygulayın veya durumunu görüntüleyin.
- **Windows Symantec sertifikası**: Symantec kod imzalama sertifikasını uygulayın veya durumunu görüntüleyin.
- **Windows dışarıdan yükleme anahtarları**: Uygulamayı Windows mağazasından yayımlamak ve indirmek yerine doğrudan cihazlara yüklemek için kullanılabilecek bir Windows dışarıdan yükleme anahtarı ekleyin. Daha fazla bilgi için bkz. [bir Windows uygulamasını dışarıdan yükleme](app-sideload-windows.md).
- **Apple VPP belirteçleri**: IOS/ıpados toplu satın alma programı (VPP) lisanslarınızı uygulayın ve görüntüleyin. Daha fazla bilgi için bkz. [iOS/ıpados toplu satın alınan uygulamalar](vpp-apps-ios.md).
- **Yönetilen Google Play**: yönetilen Google Play, Google 'ın kurumsal uygulama mağazası ve Android Enterprise uygulamalarının tek kaynağıdır. Daha fazla bilgi için bkz. [Intune Ile Android Enterprise cihazlarına yönetilen Google Play uygulamaları ekleme](apps-add-android-for-work.md).
- **Özelleştirme**: Şirket portalı, şirketinizin markasını sağlamak için özelleştirin. Daha fazla bilgi için bkz. [Şirket portalı Configuration](company-portal-app.md).

Uygulamalar hakkında daha fazla bilgi için bkz. [Microsoft Intune uygulama ekleme](../apps/apps-add.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune’a uygulama ekleme](apps-add.md)
