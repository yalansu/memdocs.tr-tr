---
title: Microsoft Intune kullanarak Windows 10 cihazlarına Office 365 uygulamaları ekleme
titleSuffix: ''
description: Windows 10 cihazlarına Office 365 uygulamalarını yüklemek için Microsoft Intune nasıl kullanabileceğinizi öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3292671a-5f5a-429e-90f7-b20019787d22
ms.reviewer: craigma
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84e77a894e207d5dfb2ffe9247ef449050d46036
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80324940"
---
# <a name="add-office-365-apps-to-windows-10-devices-with-microsoft-intune"></a>Microsoft Intune ile Windows 10 cihazlarına Office 365 uygulamaları ekleme

Uygulamaları atama, izleme, yapılandırma veya korumadan önce bunları Intune’a eklemelisiniz. Kullanılabilir [uygulama türlerinden](apps-add.md#app-types-in-microsoft-intune) biri, Windows 10 cihazları için Office 365 uygulamalarıdır. Intune 'da bu uygulama türünü seçerek, Windows 10 çalıştıran yönettiğiniz cihazlara Office 365 uygulamaları atayabilir ve yükleyebilirsiniz. Ayrıca, lisanslarınız varsa Microsoft Project Online masaüstü istemcisi ve Microsoft Visio Online Plan 2 için de uygulamalar atayabilir ve yükleyebilirsiniz. Kullanılabilir Office 365 uygulamaları, Azure 'daki Intune konsolundaki uygulamalar listesinde tek bir girdi olarak görüntülenir.

> [!NOTE]
> Microsoft Intune aracılığıyla dağıtılan Office 365 ProPlus uygulamalarını etkinleştirmek için Office 365 ProPlus lisansları kullanmanız gerekir. Office 365 Business Edition Intune tarafından desteklenir, ancak XML verilerini kullanarak Office 365 Business Edition uygulama paketini yapılandırmanız gerekir. Daha fazla bilgi için bkz. [XML verilerini kullanarak App Suite 'ı yapılandırma](apps-add-office365.md#step-2---option-2-configure-app-suite-using-xml-data).

## <a name="before-you-start"></a>Başlamadan önce

> [!IMPORTANT]
> Son kullanıcının cihazında .msi Office uygulamaları varsa, bu uygulamaları güvenle kaldırmak için **MSI'yi kaldır** özelliğini kullanmalısınız. Aksi takdirde, Intune tarafından teslim edilen Office 365 uygulamaları yüklenemez.

- Bu uygulamaları dağıtacağınız cihazların Windows 10 Creators Update veya üzerini çalıştırıyor olması gerekir.
- Intune, yalnızca Office 365 paketinden Office uygulamaları eklemeyi destekler.
- Intune uygulama paketini yüklerken herhangi bir Office uygulaması açıksa yükleme başarısız olabilir ve kullanıcılar kaydedilmeyen dosyalardaki veriler kaybedebilir.
- Bu yükleme yöntemi Windows Home, Windows Team, Windows holographic veya Windows holographic for Business cihazlarında desteklenmez.
- Intune, daha önce Intune ile Office 365 uygulamalarını dağıttığınız bir cihaza Microsoft Mağazası’ndan Office 365 masaüstü uygulamalarının (Office Centennial uygulamaları olarak bilinir) yüklenmesini desteklemez. Bu yapılandırmayı yüklerseniz veri kaybına veya bozulmasına neden olabilir.
- Birden fazla gerekli veya kullanılabilir uygulama ataması aynı anda çalışmaz. Bir uygulama ataması, kendinden önce yüklenmiş diğer uygulama atamalarının üzerine yazar. Örneğin ilk Office uygulamaları kümesi Word’ü barındırıyor ve sonraki barındırmıyorsa, Word kaldırılır. Bu koşul Visio ve Project uygulamaları için geçerli değildir.
- Birden çok Office 365 dağıtımı şu anda desteklenmiyor. Cihaza yalnızca bir dağıtım gönderilir
- **Office sürümü** - Office’in hangi sürümünü (32 bit veya 64 bit) atamak istediğinizi seçin. 32 bit sürümünü hem 32 bit hem de 64 bit cihazlara yükleyebilirsiniz ancak 64 bit sürümünü yalnızca 64 bit cihazlara yükleyebilirsiniz.
- **Son kullanıcı cihazlarından MSI’yi kaldırma** - Son kullanıcı cihazlarında önceden var olan Office .MSI uygulamalarını kaldırmak isteyip istemediğinizi belirtin. Önceden var olan varsa yükleme başarılı olmayacaktır. Son Kullanıcı cihazlarındaki MSI uygulamaları. Kaldırılacak uygulamalar, **Uygulama Paketini Yapılandır** altında yükleme için seçilen uygulamalarla sınırlı değildir çünkü tüm Office (MSI) uygulamalarını son kullanıcı cihazından kaldıracaktır. Daha fazla bilgi için bkz. [Office 365 ProPlus’a yükseltirken mevcut Office MSI sürümlerini kaldırma](https://docs.microsoft.com/deployoffice/upgrade-from-msi-version). Intune son kullanıcı makinenize Office’i yeniden yüklediğinde, son kullanıcılar önceki .MSI Office yüklemeleri ile aldıkları aynı dil paketini otomatik olarak alır.

## <a name="select-the-office-365-suite-app-type"></a>Office 365 Suite uygulama türünü seçin

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Tüm uygulamalar** ** >  > ** **Ekle**' yi seçin.
3. **Uygulama türü seç** bölmesinin **Office 365 Suite** bölümünde **Windows 10** ' u seçin.
4. **Seçin**’e tıklayın. **Add Office 365 Suite** adımları görüntülenir.


## <a name="step-1---app-suite-information"></a>1\. adım-uygulama paketi bilgileri

Bu adımda, uygulama paketi hakkında bilgi sağlarsınız. Bu bilgiler, Intune’da uygulama paketini bulmanıza yardımcı olur ve kullanıcıların Şirket Portalı’nda paketi bulması kolaylaşır.

1. **Uygulama paketi bilgileri** sayfasında, varsayılan değerleri onaylama veya değiştirme yapabilirsiniz:
    - **Paket Adı**: Uygulama paketinin Şirket Portalı’nda görüntülenen adını girin. Kullandığınız tüm paket adlarının benzersiz olduğundan emin olun. Aynı uygulama paketi adı iki kez kullanılmışsa uygulamalardan yalnızca biri şirket portalında kullanıcılara görüntülenir.
    - **Paket Açıklaması**: Uygulama paketi için bir açıklama girin. Örneğin dahil etmek üzere seçtiğiniz uygulamaları listeleyebilirsiniz.
    - **Yayımcı**: Yayımcı olarak Microsoft gösterilir.
    - **Kategori**: İsteğe bağlı olarak, yerleşik uygulama kategorilerinden veya kendi oluşturduğunuz kategorilerden birini ya da birkaçını seçin. Bu ayar, kullanıcıların şirket portalına göz atarken uygulama paketlerini daha kolay bulabilmesini sağlar.
    - **Bunu şirket portalı öne çıkan uygulama olarak göster**: kullanıcılar uygulamalara gözatarken, uygulama paketini Şirket portalının ana sayfasında göze çarpacak şekilde görüntülemek için bu seçeneği belirleyin.
    - **Bilgi URL’si**: İsteğe bağlı olarak, bu uygulama hakkında bilgi içeren bir web sitesinin URL’sini girin. URL, şirket portalında kullanıcılara görüntülenir.
    - **Gizlilik URL’si**: İsteğe bağlı olarak, bu uygulamayla ilgili gizlilik bilgilerini içeren bir web sitesinin URL’sini girin. URL, şirket portalında kullanıcılara görüntülenir.
    - **Geliştirici**: Geliştirici olarak Microsoft gösterilir.
    - **Sahip**: Sahip olarak Microsoft gösterilir.
    - **Notlar**: Bu uygulamayla ilişkilendirmek istediğiniz notları girin.
    - **Logo**: Kullanıcılar şirket portalına göz attığında uygulamayla birlikte Office 365 logosu görüntülenir.
2. **İleri** ' ye tıklayarak **uygulama paketini Yapılandır** sayfasını görüntüleyin.

## <a name="step-2---option-1-configure-app-suite-using-the-configuration-designer"></a>2\. adım-(**1. seçenek**) yapılandırma tasarımcısını kullanarak uygulama paketini yapılandırma 

**Yapılandırma ayarları biçimi**seçerek uygulama ayarını yapılandırmak için bir yöntem seçebilirsiniz. Biçim seçeneklerini ayarlama şunları içerir:
- Yapılandırma Tasarımcısı
- XML verilerini girme

**Yapılandırma Tasarımcısı** ' nı seçtiğinizde, **Uygulama Ekle** bölmesi üç ek ayar alanı sunacak şekilde değişir:
- Uygulama paketini Yapılandır
- Uygulama paketi bilgileri
- Özellikler

<img alt="Add Office 365 - Configuration designer" src="./media/apps-add-office365/apps-add-office365-02.png" width="700">

1. **Yapılandırma uygulama paketi** sayfasında **yapılandırma Tasarımcısı**' nı seçin.
   - **Office uygulamaları seçin**: açılan listeden uygulamalar ' ı seçerek cihazlara atamak Istediğiniz standart Office uygulamalarını seçin.
   - **Diğer Office uygulamalarını (lisans gerekir) seçin**: cihazlara atamak istediğiniz ve açılır listedeki uygulamaları seçerek lisanslarınızın olduğu diğer Office uygulamalarını seçin. Bu uygulamalar Microsoft Project Online masaüstü istemcisi ve Microsoft Visio Online Plan 2 gibi lisanslı uygulamaları içerir.
   - **Mimari**: Office ProPlus 'ın **32-bit** veya **64 bit** sürümünü atamak isteyip istemediğinizi seçin. 32 bit sürümünü hem 32 bit hem de 64 bit cihazlara yükleyebilirsiniz ancak 64 bit sürümünü yalnızca 64 bit cihazlara yükleyebilirsiniz.
    - **Güncelleştirme Kanalı**: Office’in cihazlarda nasıl güncelleştirileceğini seçin. Çeşitli güncelleştirme kanalları hakkında bilgi için bkz. [Office 365 ProPlus güncelleştirme kanallarına genel bakış](https://docs.microsoft.com/DeployOffice/overview-of-update-channels-for-office-365-proplus). Aşağıdakilerden birini seçin:
        - **Aylık**
        - **Aylık (Hedeflenen)**
        - **Yarı Yıllık**
        - **Yarı Yıllık (Hedeflenen)**

        Bir kanalı seçtikten sonra şunları seçebilirsiniz:
        - **Diğer sürümleri kaldır**: diğer OFFICE (MSI) sürümlerini Kullanıcı cihazlarından kaldırmak için **Evet** ' i seçin. Önceden var olan Office 'i kaldırmak istediğinizde bu seçeneği belirleyin. Son Kullanıcı cihazlarından MSI uygulamaları. Önceden var olan varsa yükleme başarılı olmayacaktır. Son Kullanıcı cihazlarındaki MSI uygulamaları. Kaldırılacak uygulamalar, **Uygulama Paketini Yapılandır** altında yükleme için seçilen uygulamalarla sınırlı değildir çünkü tüm Office (MSI) uygulamalarını son kullanıcı cihazından kaldıracaktır. Daha fazla bilgi için bkz. [Office 365 ProPlus’a yükseltirken mevcut Office MSI sürümlerini kaldırma](https://docs.microsoft.com/deployoffice/upgrade-from-msi-version). Intune son kullanıcı makinenize Office’i yeniden yüklediğinde, son kullanıcılar önceki .MSI Office yüklemeleri ile aldıkları aynı dil paketini otomatik olarak alır. 
        - **Yüklenecek sürüm**: yüklenmesi gereken Office sürümünü seçin.
        - **Belirli sürüm**: Yukarıdaki ayarda **yüklenecek sürüm** olarak **özel** ' i seçtiyseniz, Son Kullanıcı cihazlarındaki seçili kanal için belirli bir Office sürümünü yüklemeyi seçebilirsiniz. 
            
            Kullanılabilir sürümler zaman içerisinde değişir. Bu neden yeni bir dağıtım oluştururken kullanılabilir sürümler daha yeni olabilir ve bazı eski sürümleri bulamayabilirsiniz. Mevcut dağıtımlar eski sürümü dağıtmaya devam eder ancak her kanaldaki sürüm listesi sürekli olarak güncelleştirilir.
            
            Sabitlenmiş sürümlerini güncelleştiren (veya diğer özelliklerini güncelleştiren) ve kullanılabilir olarak dağıtılan cihazlar için raporlama durumu, iade etme işlemi gerçekleşene kadar cihaz önceki sürümü yüklerse Yüklendi olarak görünür. Cihaz iade etme işlemi gerçekleştiğinde ise durum geçici olarak Bilinmiyor olur ancak kullanıcıya gösterilmez. Kullanıcı, kullanılabilir yeni sürümü yüklemeye başladığında durumu Yüklendi olarak görür.
            
            Daha fazla bilgi için bkz. [Office 365 ProPlus güncelleştirme kanallarına genel bakış](https://docs.microsoft.com/DeployOffice/overview-of-update-channels-for-office-365-proplus).
    - **Paylaşımlı bilgisayar etkinleştirme kullanın**: Birden çok kullanıcı tek bir bilgisayarı kullanıyorsa bu seçeneği belirtin. Daha fazla bilgi için bkz. [Office 365 için paylaşılan bilgisayar etkinleştirmeye genel bakış](https://docs.microsoft.com/DeployOffice/overview-of-shared-computer-activation-for-office-365-proplus).
    - **Uygulama son kullanıcı lisans sözleşmesini otomatik kabul edin**: Son kullanıcıların lisans sözleşmesini kabul etmesinin gerekli olmasını istemiyorsanız bunu seçin. Ardından Intune, sözleşmeyi otomatik olarak kabul eder.
    - **Diller**: Office, son kullanıcının bilgisayarına Windows ile yüklenmiş olan tüm dillerde otomatik olarak yüklenir. Uygulama paketiyle birlikte ilave diller yüklemek istiyorsanız bunu seçin. <p></p>
        Intune üzerinden yönetilen Office 365 Pro Plus uygulamaları için ek diller dağıtabilirsiniz. Kullanılabilir diller listesi, dil paketinin **Tür** bilgisini içerir (çekirdek, kısmı ve yazım denetleme). Azure portal **Microsoft Intune** > **uygulamalar** > **tüm uygulamalar** ' a > **Ekle**' yi seçin. **Uygulama Ekle** bölmesinin **uygulama türü** listesinde, **Office 365 paketi**altında **Windows 10** ' u seçin. **Uygulama paketi ayarları** bölmesinde **Diller** ' i seçin. Ek bilgi için bkz: [Office 365 ProPlus'ta dil dağıtmaya genel bakış](https://docs.microsoft.com/deployoffice/overview-of-deploying-languages-in-office-365-proplus).
2. **İleri** ' ye tıklayarak **kapsam etiketleri** sayfasını görüntüleyin.

## <a name="step-2---option-2-configure-app-suite-using-xml-data"></a>2\. adım-(**2. seçenek**) App SUITE 'i XML verilerini kullanarak yapılandırma 

**Uygulama paketini Yapılandır** sayfasındaki biçim açılan kutusu **ayarı** altında **XML verisi gir** seçeneğini belirlediyseniz, Office uygulama paketini özel bir yapılandırma dosyası kullanarak yapılandırabilirsiniz.

![Office 365 yapılandırma Tasarımcısı ekleme](./media/apps-add-office365/apps-add-office365-01.png)

1. Yapılandırma XML 'niz eklendi.

    > [!NOTE]
    > Ürün KIMLIĞI Iş (`O365BusinessRetail`) ya da ProPlus (`O365ProPlusRetail`) olabilir. Ancak, yalnızca XML verilerini kullanarak Office 365 Business Edition 'ın uygulama paketini yapılandırabilirsiniz. 

2. **İleri** ' ye tıklayarak **kapsam etiketleri** sayfasını görüntüleyin.

XML verileri girme hakkında daha fazla bilgi için bkz. [Office dağıtım aracı Için yapılandırma seçenekleri](https://docs.microsoft.com/DeployOffice/configuration-options-for-the-office-2016-deployment-tool).

## <a name="step-3---select-scope-tags-optional"></a>3\. adım-kapsam etiketlerini seçin (isteğe bağlı)
Intune 'da istemci uygulama bilgilerini kimlerin görebileceğini anlamak için kapsam etiketlerini kullanabilirsiniz. Kapsam etiketleri hakkında tam Ayrıntılar için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md).

1. **Kapsam etiketlerini Seç** ' e tıklayarak uygulama paketi için isteğe bağlı olarak kapsam etiketleri ekleyin.
2. **Atamalar** sayfasını göstermek için **İleri** ' ye tıklayın.

## <a name="step-4---assignments"></a>4\. adım-atamalar

1. **Gerekli**, **Kayıtlı cihazlar için kullanılabilir**veya uygulama paketi için Grup atamalarını **Kaldır** ' ı seçin. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları düzenlemek için grup ekleme](../fundamentals/groups-add.md) ve [Microsoft Intune olan gruplara uygulama atama](apps-deploy.md).
2. **İleri** ' ye tıklayarak **gözden geçir + oluştur** sayfasını görüntüleyin.

## <a name="step-5---review--create"></a>5\. adım-Inceleme ve oluşturma

1. Uygulama paketi için girdiğiniz değerleri ve ayarları gözden geçirin.
2. İşiniz bittiğinde, uygulamayı Intune 'a eklemek için **Oluştur** ' a tıklayın.

    Oluşturduğunuz Office 365 Windows 10 uygulama paketinin **genel bakış** dikey penceresi görüntülenir.

## <a name="deployment-details"></a>Dağıtım ayrıntıları

Intune 'dan dağıtım ilkesi, [Office yapılandırma hizmeti sağlayıcısı (CSP)](https://docs.microsoft.com/windows/client-management/mdm/office-csp)aracılığıyla hedef makinelere atandıktan sonra, son cihaz yükleme paketini otomatik olarak *officecdn.Microsoft.com* konumundan indirir. *Program dosyaları* dizininde görüntülenen iki dizin görürsünüz:

![Program Files dizinindeki Office yükleme paketleri](./media/apps-add-office365/office-folder.png)

*Microsoft Office* dizininde, yükleme dosyalarının depolandığı yeni bir klasör oluşturulur:

![Microsoft Office Directory altında yeni oluşturulan klasör](./media/apps-add-office365/created-folder.png)

*Microsoft Office 15* dizini altında, Office Tıkla-Çalıştır yükleme Başlatıcısı dosyaları depolanır. Atama türü gerekliyse yükleme otomatik olarak başlatılır:

![Yükleme Başlatıcısı dosyalarını çalıştırmak için tıklayın](./media/apps-add-office365/clicktorun-files.png)

O365 paketinin atanması gerekli olarak yapılandırılmışsa yükleme sessiz modda olur. Yükleme başarılı olduktan sonra indirilen yükleme dosyaları silinir. Atama **kullanılabilir**olarak yapılandırılmışsa, son kullanıcıların yüklemeyi el ile tetikleyebilmesi için Office uygulamaları şirket portalı uygulamasında görüntülenir.

## <a name="troubleshooting"></a>Sorun giderme
Intune, Office [365 CDN](https://docs.microsoft.com/office365/enterprise/content-delivery-networks)'yi kullanarak Office 365 ProPlus 'ı istemci bilgisayarlarınıza indirip dağıtmak Için [Office dağıtım aracı](https://docs.microsoft.com/DeployOffice/overview-of-the-office-2016-deployment-tool) 'nı kullanır. Ağ yapılandırmanızın, istemcilerin, gereksiz gecikme süresine ulaşmaktan kaçınmak için merkezi proxy 'ler aracılığıyla CDN trafiğini yönlendirmek yerine doğrudan CDN 'ye erişmesine izin verdiğinden emin olmak için, [Office 365 uç noktalarını yönetme](https://docs.microsoft.com/office365/enterprise/managing-office-365-endpoints) bölümünde özetlenen en iyi yöntemlere başvurun.

Yükleme veya çalışma zamanı sorunlarıyla karşılaşırsanız, hedeflenen bir cihazda [Office 365 için Microsoft desteği ve Kurtarma Yardımcısı](https://diagnostics.office.com) 'nı çalıştırın.

### <a name="additional-troubleshooting-details"></a>Ek sorun giderme ayrıntıları

O365 uygulamalarını bir cihaza yükleyemezseniz, sorunun Intune ile ilgili olup olmadığını ve işletim sistemi/ofis ile ilgili olduğunu tanımlamalısınız. *Microsoft Office* iki klasörü ve cihazın *Program dosyaları* dizininde görünen *Microsoft Office 15* ' i görürseniz, Intune 'un dağıtımı başarıyla başlattığını doğrulayabilirsiniz. *Program dosyaları*altında görüntülenen iki klasörü göremiyorsanız, aşağıdaki durumları onaylamanız gerekir:

- Cihaz Microsoft Intune 'ye düzgün şekilde kaydedilir. 
- Cihazda etkin bir ağ bağlantısı var. Cihaz uçak modundaysa, kapalıysa veya hizmeti olmayan bir konumdaysa, ağ bağlantısı kurulana kadar ilke uygulanmaz.
- Hem Intune hem de Office 365 ağ gereksinimleri karşılanır ve ilgili IP aralıkları aşağıdaki makalelere göre erişilebilir:

  - [Intune ağ yapılandırma gereksinimleri ve bant genişliği](https://docs.microsoft.com/intune/network-bandwidth-use)
  - [Office 365 URL 'Leri ve IP adresi aralıkları](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges)

- Doğru gruplara O365 uygulama paketi atanmıştır. 

Ayrıca, *C:\Program Files\Microsoft Office\Updates\Download*dizininin boyutunu izleyin. Intune bulutlarından indirilen yükleme paketi bu konumda depolanır. Boyut artmaz veya yalnızca çok yavaş artışlar durumunda ağ bağlantısının ve bant genişliğinin iki kez denetlenmesi önerilir.

Hem Intune hem de ağ altyapısının beklendiği gibi çalıştığını sonuçladıktan sonra, sorunu bir işletim sistemi perspektifinden daha fazla analiz etmeniz gerekir. Aşağıdaki koşulları göz önünde bulundurun:

- Hedef cihaz Windows 10 Creators Update veya üzeri sürümlerde çalışmalıdır.
- Intune uygulamaları dağıttığında mevcut Office uygulamaları açılmaz.
- Office 'in mevcut MSI sürümleri cihazdan düzgün şekilde kaldırıldı. Intune, Office MSI ile uyumlu olmayan Office Tıkla-Çalıştır 'ı kullanır. Bu davranış, bu belgede daha da bahsediliyor:<br>
  [Aynı bilgisayarda Tıkla-Çalıştır ve Windows Installer ile yüklenen Office desteklenmez](https://support.office.com/article/office-installed-with-click-to-run-and-windows-installer-on-same-computer-isn-t-supported-30775ef4-fa77-4f47-98fb-c5826a6926cd)
- Oturum açma kullanıcısının cihaza uygulama yüklemesi için izni olmalıdır.
- Windows Olay Görüntüleyicisi günlük **Windows günlükleri** -> **uygulamalarına**dayalı bir sorun olmadığını onaylayın.
- Yükleme sırasında Office yükleme ayrıntılı günlüklerini yakalayın. Bunu yapmak için şu adımları izleyin:<br>
    1. Hedef makinelerde Office yüklemesi için ayrıntılı günlük kaydını etkinleştirin. Bunu yapmak için, kayıt defterini değiştirmek için aşağıdaki komutu çalıştırın:<br>
        `reg add HKLM\SOFTWARE\Microsoft\ClickToRun\OverRide /v LogLevel /t REG_DWORD /d 3`<br>
    2. Office 365 paketini hedef cihazlara yeniden dağıtın.<br>
    3. Yaklaşık 15 ila 20 dakika bekleyin ve **% Temp%** klasörüne ve **%windir%\Temp** klasörüne gidin, **değiştirme tarihine**göre sıralayın, yeniden oluşturma zamanına göre değiştirilen *{Machine Name}-{timestamp}. log* dosyalarını seçin.<br>
    4. Ayrıntılı günlüğü devre dışı bırakmak için aşağıdaki komutu çalıştırın:<br>
        `reg delete HKLM\SOFTWARE\Microsoft\ClickToRun\OverRide /v LogLevel /f`<br>
        Ayrıntılı Günlükler, yükleme işlemi hakkında daha ayrıntılı bilgi sağlayabilir.

## <a name="errors-during-installation-of-the-app-suite"></a>Uygulama paketinin yüklenmesi sırasında karşılaşılan hatalar

Ayrıntılı yükleme günlüklerinin nasıl görüntüleneceği hakkında bilgi için bkz. [Office 365 ProPlus ULS günlüğünü etkinleştirme](/office/troubleshoot/diagnostic-logs/how-to-enable-office-365-proplus-uls-logging) .

Karşınıza çıkabilecek yaygın hata kodları ve anlamları, aşağıdaki tablolarda listelenmiştir.

### <a name="status-for-office-csp"></a>Office CSP durumu

| Durum | Aşama | Açıklama |
|--------------------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1460 (ERROR_TIMEOUT) | İndir | Office Dağıtım Aracı’nı indirme başarısız |
| 13 (ERROR_INVALID_DATA) | - | İndirilen Office Dağıtım Aracı’nın imzası doğrulanamıyor |
| CertVerifyCertificateChainPolicy hata kodu | - | İndirilen Office Dağıtım Aracı için sertifika denetimi başarısız |
| 997 | Süren İş | Yükleniyor |
| 0 | Yükleme sonrası | Yükleme başarılı |
| 1603 (ERROR_INSTALL_FAILURE) | - | Şu gibi önkoşul denetimi başarısız oldu: SxS (2016 MSI yüklendiğinde yüklenmeye çalışıldı) sürüm hatalı Matchoınstler |
| 0x8000ffff (E_UNEXPECTED) | - | Makinede Tıkla-Çalıştır Office yokken kaldırılmaya çalışıldı |
| 17002 | - | Senaryoyu tamamlama başarısız (yükleme). Olası nedenler: yükleme işlemi kullanıcı tarafından iptal edildi yükleme sırasında başka bir ınstaldisk alanı tarafından iptal edildi bilinmeyen dil KIMLIĞI |
| 17004 | - | Bilinmeyen SKU’lar |


### <a name="office-deployment-tool-error-codes"></a>Office Dağıtım Aracı hata kodları

| Senaryo | Dönüş kodu | Kullanıcı Arabirimi | Not |
|------------------------------------------------------------------------------------------------------------------|---------------------------------------|----------------------------------------------------|------------------------------------|
| Etkin bir Tıkla-Çalıştır yükleme yokken kaldırma çabası | -2147418113, 0x8000ffff veya 2147549183 | Hata kodu: 30088-1008Hata kodu: 30125-1011 (404) | Office Dağıtım Aracı |
| MSI sürümü yüklü olduğunda yükleyin | 1603 | - | Office Dağıtım Aracı |
| Yükleme, kullanıcı veya başka bir yükleme tarafından iptal edildi | 17002 | - | Tıkla-Çalıştır |
| 32 bit yüklü olan bir cihaza 64 bit yüklemeyi deneyin. | 1603 | - | Office Dağıtım Aracı dönüş kodu |
| Bilinmeyen bir SKU yüklemeyi deneyin (yalnızca geçerli SKU’lardan geçmemiz gerektiğinden, Office CSP için yasal bir kullanım durumu değildir) | 17004 | - | Tıkla-Çalıştır |
| Yetersiz alan | 17002 | - | Tıkla-Çalıştır |
| Tıkla-Çalıştır istemcisi başlatılamadı (beklenmeyen) | 17000 | - | Tıkla-Çalıştır |
| Tıkla-Çalıştır istemcisi, senaryoyu kuyruğa alamadı (beklenmeyen) | 17001 | - | Tıkla-Çalıştır |

## <a name="next-steps"></a>Sonraki adımlar

- Uygulama paketini ek gruplara atamak için bkz. [uygulamaları gruplara atama](/mem/intune/apps/apps-deploy).