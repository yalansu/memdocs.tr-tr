---
title: Microsoft Intune için Win32 uygulamaları ekleme ve atama
titleSuffix: ''
description: Microsoft Intune ile Win32 uygulamaları eklemeyi, atamayı ve yönetmeyi öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5266f354ea5806743813d1aeb4c456890fa46b19
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083956"
---
# <a name="add-assign-and-monitor-a-win32-app-in-microsoft-intune"></a>Microsoft Intune bir Win32 uygulaması ekleyin, atayın ve izleyin

[Microsoft Win32 içerik hazırlama aracı](https://go.microsoft.com/fwlink/?linkid=2065730)'Nı kullanarak [Intune 'A yüklenecek bir Win32 uygulaması hazırladıktan](apps-win32-prepare.md) sonra, uygulamayı Intune 'a ekleyebilirsiniz. Karşıya yüklenecek Win32 uygulamasını hazırlama hakkında daha fazla bilgi edinmek için bkz. [Win32 uygulama içeriğini karşıya yükleme Için hazırlama](apps-win32-prepare.md).

## <a name="prerequisites"></a>Önkoşullar

Win32 uygulama yönetimini kullanmak için aşağıdaki ölçütleri karşıladığınızdan emin olun:

- Windows 10 sürüm 1607 veya üstünü (Enterprise, Pro ve eğitim sürümleri) kullanın.
- Cihazların Azure Active Directory (Azure AD) ve otomatik olarak kaydedilmiş olması gerekir. Intune yönetim uzantısı, Azure AD 'ye katılmış, karma etki alanına katılmış ve Grup İlkesi kayıtlı olan cihazları destekler. 
  > [!NOTE]
  > Kullanıcı, Grup İlkesi kaydı senaryosunda, Azure AD 'de Windows 10 cihazını birleştirmek için yerel kullanıcı hesabını kullanır. Kullanıcı, Azure AD Kullanıcı hesabını kullanarak cihazda oturum açması ve Intune 'a kaydolmalıdır. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza hedeflenirse, bu cihaza Intune yönetim uzantısını yükler.
- Windows uygulama boyutu uygulama başına 8 GB 'A göre belirlenir.

Standart bir iş kolu (LOB) uygulaması gibi, Microsoft Intune için bir Win32 uygulaması da ekleyebilirsiniz. Bu tür bir uygulama genellikle şirket içinde veya üçüncü bir taraflarca yazılmıştır. 

## <a name="process-flow-to-add-a-win32-app-to-intune"></a>Intune 'a bir Win32 uygulaması eklemek için işlem akışı

<img alt="Flow chart of the process to add a Win32 app to Intune." src="./media/apps-win32-app-management/add-win32-app.svg" width="500">

## <a name="add-a-win32-app-to-intune"></a>Intune 'a bir Win32 uygulaması ekleme

Aşağıdaki adımlar, Intune 'a bir Windows uygulaması eklemenize yardımcı olur:

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar**  >  **tüm uygulamalar**  >  **Ekle**' yi seçin.
3. **Uygulama türünü seçin** bölmesinde, **diğer** uygulama türleri altında **Windows uygulaması (Win32)** öğesini seçin.

    > [!IMPORTANT]
    > Microsoft Win32 Içerik hazırlığı aracının en son sürümünü kullandığınızdan emin olun. En son sürümü kullanmıyorsanız, uygulamanın aracın eski bir sürümü kullanılarak paketlendiğini bildiren bir uyarı görürsünüz. 

4. **Seç**’e tıklayın. **Uygulama ekleme** adımları görüntülenir.

## <a name="step-1-app-information"></a>1. Adım: uygulama bilgileri

### <a name="select-the-app-package-file"></a>Uygulama paketi dosyasını seçin

1. **Uygulama Ekle** bölmesinde **uygulama paketi dosyası seç**' e tıklayın. 
2. **Uygulama paketi dosyası** bölmesinde, tarayıcı düğmesini seçin. Daha sonra *.intunewin* uzantılı bir Windows yükleme dosyası seçin.
   Uygulama ayrıntıları görüntülenir.
3. İşiniz bittiğinde, **uygulama paketi dosyası** bölmesinde **Tamam** ' ı seçin.

### <a name="set-app-information"></a>Uygulama bilgilerini ayarla

**Uygulama bilgileri** sayfasında uygulamanızın ayrıntılarını ekleyin. Seçtiğiniz uygulamaya bağlı olarak, bu sayfadaki bazı değerler otomatik olarak doldurulabilir.

- **Ad**: Uygulamanın Şirket Portalı’nda görünen adını girin. Kullandığınız tüm uygulama adlarının benzersiz olduğundan emin olun. Aynı uygulama adı iki kez kullanılmışsa uygulamalardan yalnızca biri Şirket Portalı’nda kullanıcılara görüntülenir.
- **Açıklama**: Uygulama açıklamasını girin. Açıklama, Şirket Portalı’nda görünür.
- **Yayımcı**: Uygulama yayımcısının adını girin.
- **Kategori**: Yerleşik uygulama kategorilerinden birini veya kendi oluşturduğunuz bir kategoriyi seçin. Kategoriler, kullanıcıların Şirket Portalı’na göz atarken uygulamayı daha kolay bulabilmesini sağlar.
- **Bunu şirket portalı öne çıkan uygulama olarak göster**: kullanıcılar uygulamalara gözatarken, uygulamayı şirket portalının ana sayfasında göze çarpacak şekilde görüntüleyin.
- **Bilgi URL’si**: İsteğe bağlı olarak, bu uygulama hakkında bilgi içeren bir web sitesinin URL’sini girin. URL Şirket Portalı’nda görünür.
- **Gizlilik URL’si**: İsteğe bağlı olarak, bu uygulamayla ilgili gizlilik bilgilerini içeren bir web sitesinin URL’sini girin. URL Şirket Portalı’nda görünür.
- **Geliştirici**: İsteğe bağlı olarak, uygulama geliştiricisinin adını girin.
- **Sahip**: İsteğe bağlı olarak uygulama sahibinin adını girin. Örneğin **İK departmanı**.
- **Notlar**: Bu uygulamayla ilişkilendirmek istediğiniz notları girin.
- **Logo**: uygulamayla ilişkili bir simgeyi karşıya yükleyin. Bu simge, kullanıcılar Şirket Portalı’na göz atarken uygulamayla birlikte görüntülenir.

**Program** sayfasını göstermek için **İleri ' yi** seçin.

## <a name="step-2-program"></a>2. Adım: program

**Program** sayfasında, uygulama için uygulama yükleme ve kaldırma komutlarını yapılandırın:

- **Yükleme komutu**: uygulamayı yüklemek için yükleme komut satırını tamamen ekleyin. 

    Örneğin, uygulamanızın dosya adı **MyApp123**ise, aşağıdakileri ekleyin:

    `msiexec /p "MyApp123.msp"`
    
    Uygulama ise `ApplicationName.exe` , komut uygulamanın adı ve ardından paketin desteklediği komut bağımsız değişkenleri (anahtarlar) gelir. Örnek:

    `ApplicationName.exe /quiet`
    
    Önceki komutta, `ApplicationName.exe` paket `/quiet` komut bağımsız değişkenini destekler. 
    
    Uygulama paketinin desteklediği belirli bağımsız değişkenler için uygulama satıcınıza başvurun.

    > [!IMPORTANT]
    > Yöneticiler, komut araçlarını kullandıklarında dikkatli olmalıdır. Beklenmeyen veya zararlı komutlar **Install komutu** ve **Uninstall komut** alanları aracılığıyla geçirilebilir.

- **Kaldır komutu**: uygulamanın GUID 'ine göre uygulamayı kaldırmak için komut satırının tamamını ekleyin. 

    Örnek:
    
    `msiexec /x "{12345A67-89B0-1234-5678-000001000000}"`

- **Davranışı yükler**: Install davranışını **sistem** veya **Kullanıcı**olarak ayarlayın.

    > [!NOTE]
    > Bir Win32 uygulamasını **Kullanıcı** veya **Sistem** bağlamında yüklenecek şekilde yapılandırabilirsiniz. **Kullanıcı** bağlamı yalnızca belirli bir kullanıcıyı ifade eder. **Sistem** bağlamı bir Windows 10 cihazın tüm kullanıcılarını ifade eder.
    >
    > Win32 uygulamalarını yüklemek için kullanıcıların cihazda oturum açması gerekmez.
    > 
    > Uygulama kullanıcı bağlamında yüklenmek üzere ayarlandığında ve cihazdaki kullanıcının yönetici ayrıcalıklarına sahip olması durumunda, Win32 uygulama yüklemesi ve kaldırma işlemi yönetici ayrıcalığında (varsayılan olarak) gerçekleşir.
    
- **Cihaz yeniden başlatma davranışı**: aşağıdaki seçeneklerden birini belirleyin:
    - **Dönüş kodlarına dayalı davranışı belirleme**: cihazı dönüş kodlarına göre yeniden başlatmak için bu seçeneği belirleyin.
    - **Belirli bir eylem yok**: MSI tabanlı uygulamaların uygulama yüklemesi sırasında cihaz yeniden başlatmalarının görüntülenmesini sağlamak için bu seçeneği belirleyin.
    - **Uygulama yüklemesi bir cihazın yeniden başlatılmasını zorlayabilir**: uygulama yüklemesinin yeniden başlatmalar olmadan tamamlanmasına izin vermek için bu seçeneği belirleyin.
    - **Intune zorunlu bir cihaz yeniden başlatmaya zorlayacaktır**: başarılı bir uygulama yüklemesinden sonra cihazı her zaman yeniden başlatmak için bu seçeneği belirleyin.

- **Yükleme sonrası davranışı göstermek için dönüş kodlarını belirtin**: uygulama yükleme yeniden deneme davranışını veya yükleme sonrası davranışını belirtmek için kullanılan dönüş kodlarını ekleyin. Dönüş kodu girdileri varsayılan olarak uygulama oluşturma işlemi sırasında eklenir. Ancak, daha fazla dönüş kodu ekleyebilir veya varolan dönüş kodlarını değiştirebilirsiniz.
    1. **Kod türü** sütununda, **kod türünü** aşağıdakilerden birine ayarlayın:
        - **Başarısız**: bir uygulama yükleme hatasını gösteren dönüş değeri.
        - **Sabit yeniden başlatma**: sabit yeniden başlatma dönüş kodu, sonraki Win32 uygulamasının önyükleme yapılmadan istemciye yüklenmesine izin vermez. 
        - **Geçici yeniden başlatma**: geçici yeniden başlatma dönüş kodu, bir sonraki Win32 uygulamasının istemci yeniden başlatmaya gerek kalmadan yüklenmesine izin verir. Geçerli uygulamanın yüklemesini tamamlamak için önyükleme gereklidir.
        - **Yeniden deneme**: yeniden deneme dönüş kodu Aracısı, uygulamayı üç kez yüklemeyi deneyecek. Her girişimde beş dakika bekleyecektir. 
        - **Başarılı**: uygulamanın başarıyla yüklendiğini gösteren dönüş değeri.
    2. Gerekirse, daha fazla dönüş kodu eklemek için **Ekle** ' yi seçin veya mevcut dönüş kodlarını değiştirin.

**Gereksinimler** sayfasını göstermek için **İleri ' yi** seçin.    

## <a name="step-3-requirements"></a>3. Adım: gereksinimler

**Gereksinimler** sayfasında, uygulama yüklenmeden önce cihazların karşılaması gereken gereksinimleri belirtin:

- **İşletim sistemi mimarisi**: uygulamayı yüklemek için gereken mimarileri seçin.
- **Minimum işletim sistemi**: Uygulamayı yüklemek için gereken minimum işletim sistemini seçin.
- **Gerekli disk alanı (MB)**: İsteğe bağlı olarak, uygulamayı yüklemek için sistem sürücüsünde gereken boş disk alanını ekleyin.
- **Gerekli fiziksel bellek (MB)**: İsteğe bağlı olarak, uygulamayı yüklemek için gereken fiziksel belleği (RAM) ekleyin.
- **Gereken en düşük mantıksal işlemci sayısı**: İsteğe bağlı olarak, uygulamayı yüklemek için gereken en düşük mantıksal işlemci sayısını ekleyin.
- **Gereken en düşük CPU hızı (MHz)**: İsteğe bağlı olarak, uygulamayı yüklemek için gereken en düşük CPU hızını ekleyin.
- **Ek gereksinim kurallarını yapılandırın**: 
    1. **Gereksinim kuralı ekle** bölmesini göstermek ve daha fazla gereksinim kuralı yapılandırmak için **Ekle** ' yi seçin. Gereksinimin nasıl doğrulanacağını belirlemek için kullanacağınız kural türünü seçmek için **Gereksinim türü** değerini seçin. Gereksinim kuralları dosya sistemi bilgilerini, kayıt defteri değerlerini veya PowerShell komut dosyalarını temel alabilir. 
        - **Dosya**: **Gereksinim türü** değeri olarak **Dosya** ' yı seçtiğinizde, gereksinim kuralı bir dosya veya klasör, tarih, sürüm veya boyut algılamamalıdır. 
            - **Yol**: algılanacak dosyayı veya klasörü içeren klasörün tam yolu.
            - **Dosya veya klasör**: algılanacak dosya veya klasör.
            - **Özellik**: uygulamanın varlığını doğrulamak için kullanılan kural türünü seçin.
            - **64 bit istemcilerde 32 bitlik bir uygulamayla ilişkili**: 64 bit istemcilerde 32-bit bağlamındaki herhangi bir yol ortam değişkenini genişletmek için **Evet** ' i seçin. Tüm yol değişkenlerini 64 bit istemciler üzerinde 64 bit bağlamında genişletmek için **Hayır**'ı (varsayılan) seçin. 32 bit istemciler her zaman 32 bit bağlamını kullanır.
        - **Kayıt defteri**: **Gereksinim türü** değeri olarak **kayıt defteri** ' ni seçtiğinizde, gereksinim kuralı değer, dize, tamsayı veya sürüme göre bir kayıt defteri ayarı tespit etmelidir.
            - **Anahtar yolu**: algılanacak değeri içeren kayıt defteri girdisinin tam yolu.
            - **Değer adı**: algılanacak kayıt defteri değerinin adı. Bu değer boşsa algılama anahtarda gerçekleştirilir. Algılama yöntemi dosya veya klasör varlığından farklı bir yöntemse, algılama değeri olarak anahtarın (varsayılan) değeri kullanılır.
            - **Kayıt defteri anahtarı gereksinimi**: gereksinim kuralının nasıl doğrulanacağını belirlemek için kullanılan kayıt defteri anahtarı karşılaştırma türünü seçin.
            - **64 bit istemcilerde 32 bitlik bir uygulamayla ilişkili**: 64-bit istemcilerde 32 bit kayıt defterinde aramak için **Evet** ' i seçin. 64 bit istemcilerde 64 bit kayıt defterinde arama yapmak için **Hayır** (varsayılan) seçeneğini belirleyin. 32 bit istemcilerde her zaman 32 bit kayıt defterinde arama yapılır.
        - **Betik**: Intune konsolunda kullanabileceğiniz dosya, kayıt defteri veya başka bir yöntemi temel alan bir gereksinim kuralı oluşturamıyoruz, **Gereksinim türü** olarak **komut dosyasını** seçin.
            - **Betik dosyası**: bir PowerShell betik gereksinimini temel alan bir kural için, mevcut kod 0 ise standart ÇıKTıYı (STDOUT) daha ayrıntılı olarak algılayacağız. Örneğin, STDOUT değerini 1 değeri olan bir tamsayı olarak tespit edebilirsiniz.
            - **Komut dosyasını 64 bit istemcilerde 32 bitlik işlem olarak çalıştır**: betiği, 64 bit istemcilerde bir 32 bit işlemde çalıştırmak için **Evet** ' i seçin. Komut dosyasını 64 bit istemcilerde 64 bitlik bir işlemde çalıştırmak için **Hayır** (varsayılan) seçeneğini belirleyin. 32 bitlik istemciler betiği 32 bit bir işlemde çalıştırır.
            - **Bu betiği oturum açmış olan kimlik bilgilerini kullanarak Çalıştır**: oturum açmış cihaz kimlik bilgilerini kullanarak betiği çalıştırmak için **Evet** ' i seçin.
            - **Betik Imzasını zorla denetimi**: güvenilen bir yayımcının betiği imzaladığını doğrulamak için **Evet** ' i seçin; Bu, komut dosyasının hiçbir uyarı veya istem görüntülenmeden çalışmasına izin verir. Betik engellenmeden çalıştırılır. Komut dosyasını imza doğrulaması olmadan Kullanıcı onayıyla çalıştırmak için **Hayır** (varsayılan) seçeneğini belirleyin.
            - **Çıkış verisi türünü seçin**: bir gereksinim kuralı eşleşmesini belirlemek için kullanılan veri türünü seçin.
    2. Gereksinim kurallarını ayarlamayı tamamladığınızda **Tamam**' ı seçin.

**Algılama kuralları** sayfasını göstermek için **İleri ' yi** seçin. 

## <a name="step-4-detection-rules"></a>4. Adım: algılama kuralları

**Algılama kuralları** sayfasında, uygulamanın varlığını algılamak için kuralları yapılandırın:
    
- **Kurallar biçimi**: uygulama varlığının nasıl algılanacağını seçin. Algılama kurallarını el ile yapılandırmayı seçebileceğiniz gibi uygulamanın varlığını algılamak için özel bir betik de kullanabilirsiniz. En az bir algılama kuralı seçmelisiniz. 

  > [!NOTE]
  > **Algılama kuralları** bölmesinde, birden çok kural eklemeyi seçebilirsiniz. Uygulamanı algılanması için *tüm* kuralların koşullarına uyulmalıdır.
  >
  > Intune, uygulamanın cihazda mevcut olmadığını algılarsa, uygulamayı 24 saat sonra yeniden sunar. Bu, yalnızca gerekli amaca yönelik uygulamalar için gerçekleşir.

- **Algılama kurallarını el ile yapılandır**: aşağıdaki kural türlerinden birini seçebilirsiniz:
    - **MSI**: MSI sürüm denetimini temel alarak doğrulayın. Bu seçenek yalnızca bir kez eklenebilir. Bu kural türünü seçtiğinizde iki ayarınız olur:
        - **MSI ürün kodu**: uygulama için GEÇERLI bir MSI ürün kodu ekleyin.
        - **MSI ürün sürümü denetimi**: MSI ürün kodunun yanı sıra MSI ürün sürümünü doğrulamak için **Evet** ' i seçin.
    - **Dosya**: dosya veya klasör algılamayı, tarihi, sürümü veya boyutu temel alarak doğrulayın.
        - **Yol**: algılanacak dosyayı veya klasörü içeren klasörün tam yolunu girin.
        - **Dosya veya klasör**: algılanacak dosyayı veya klasörü girin.
        - **Algılama yöntemi**: uygulamanın varlığını doğrulamak için kullanılan algılama yöntemi türünü seçin.
        - **64 bit istemcilerde 32 bitlik bir uygulamayla ilişkili**: 64 bit istemcilerde 32-bit bağlamındaki herhangi bir yol ortam değişkenini genişletmek için **Evet** ' i seçin. Tüm yol değişkenlerini 64 bit istemciler üzerinde 64 bit bağlamında genişletmek için **Hayır**'ı (varsayılan) seçin. 32 bit istemciler her zaman 32 bit bağlamını kullanır.
            
        **Dosya tabanlı algılama örnekleri**

        Dosyanın varlığını denetleyin.
         
        ![Algılama kuralı bölmesinin ekran görüntüsü-dosya varlığı.](./media/apps-win32-app-management/apps-win32-app-03.png)
        
        Klasör varlığını denetleyin.
        
        ![Algılama kuralı bölmesinin ekran görüntüsü-klasör var.](./media/apps-win32-app-management/apps-win32-app-04.png)
        
    - **Kayıt defteri**: değer, dize, tamsayı veya sürüme göre doğrulayın.
        - **Anahtar yolu**: algılanacak değeri içeren kayıt defteri girdisinin tam yolu. Geçerli bir sözdizimi HKEY_LOCAL_MACHINE \Software\WinRAR veya HKLM\Software\WinRAR.
        - **Değer adı**: algılanacak kayıt defteri değerinin adı. Bu değer boşsa algılama anahtarda gerçekleştirilir. Algılama yöntemi dosya veya klasör varlığından farklı bir yöntemse, algılama değeri olarak anahtarın (varsayılan) değeri kullanılır.
        - **Algılama yöntemi**: uygulamanın varlığını doğrulamak için kullanılan algılama yöntemi türünü seçin.
        - **64 bit istemcilerde 32 bitlik bir uygulamayla ilişkili**: 64-bit istemcilerde 32 bit kayıt defterinde aramak için **Evet** ' i seçin. 64 bit istemcilerde 64 bit kayıt defterinde arama yapmak için **Hayır** (varsayılan) seçeneğini belirleyin. 32 bit istemcilerde her zaman 32 bit kayıt defterinde arama yapılır.
            
        **Kayıt defteri temelinde algılama örnekleri**
        
        Kayıt defteri anahtarının var olup olmadığını denetleyin.
            
        ![Algılama kuralı bölmesinin ekran görüntüsü-kayıt defteri anahtarı var.](./media/apps-win32-app-management/apps-win32-app-05.png)    
            
        Kayıt defteri değerinin var olup olmadığını denetleyin.
        
        ![Algılama kuralı bölmesinin ekran görüntüsü-kayıt defteri değeri var.](./media/apps-win32-app-management/apps-win32-app-06.png)    
        
        Kayıt defteri değer dizesinin eşitliğini denetleyin.
        
        ![Algılama kuralı bölmesinin ekran görüntüsü-kayıt defteri değer dizesi eşittir.](./media/apps-win32-app-management/apps-win32-app-07.png)    
     
- **Özel bir algılama betiği kullan**: Bu uygulamayı algılamak Için kullanılacak PowerShell betiğini belirtin. 
    
   - **Betik dosyası**: istemcide uygulamanın varlığını algılayan bir PowerShell betiği seçin. Betik her ikisi de **0** değer çıkış kodu DÖNDÜRDÜĞÜNDE ve STDOUT 'a bir dize değeri yazdığında uygulama algılanır.

   - **Komut dosyasını 64 bit istemcilerde 32 bitlik işlem olarak çalıştır**: betiği, 64 bit istemcilerde bir 32 bit işlemde çalıştırmak için **Evet** ' i seçin. Komut dosyasını 64 bit istemcilerde 64 bitlik bir işlemde çalıştırmak için **Hayır** (varsayılan) seçeneğini belirleyin. 32 bitlik istemciler betiği 32 bit bir işlemde çalıştırır.

   - **Betik Imzasını zorla denetimi**: güvenilen bir yayımcının betiği imzaladığını doğrulamak için **Evet** ' i seçin; Bu, komut dosyasının hiçbir uyarı veya istem görüntülenmeden çalışmasına izin verir. Betik engellenmeden çalıştırılır. Komut dosyasını imza doğrulaması olmadan Kullanıcı onayıyla çalıştırmak için **Hayır** (varsayılan) seçeneğini belirleyin.
    
   Intune Aracısı, komut dosyasının sonuçlarını denetler. Betik tarafından yazılan değerleri STDOUT akışına, standart hata (STDERR) akışına ve çıkış koduna okur. Betikten sıfırdan farklı bir değerle çıkılırsa, betik başarısız olur ve uygulama algılama durumu Yüklü Değil olur. Çıkış kodu sıfırsa ve STDOUT veri içeriyorsa, uygulama algılama durumu yüklenir. 

   > [!NOTE]
   > Betiğinizi UTF-8 olarak kodlanmasını öneririz. Komut dosyası **0**değeri ile çıkıldığında, betik yürütme başarılı oldu. İkinci çıkış kanalı, uygulamanın algılandığını gösterir. STDOUT verileri, uygulamanın istemcide bulunduğunu gösterir. STDOUT 'dan belirli bir dizeyi aramaz.

Kurallarınızı ekledikten sonra **Bağımlılıklar** sayfasını göstermek için **İleri** ' yi seçin.

## <a name="step-5-dependencies"></a>5. Adım: bağımlılıklar

Uygulama bağımlılıkları, Win32 uygulamanızın yüklenebilmesi için yüklenmesi gereken uygulamalardır. Diğer uygulamaların bağımlılık olarak yüklenmesini zorunlu kılabilirsiniz. 

Özellikle, cihazın Win32 uygulamasını yüklemeden önce bağımlı uygulamaları yüklemesi gerekir. Dahil edilen bağımlılıkların bağımlılıklarını ve uygulamanın kendisini içeren en fazla 100 bağımlılığı vardır. 

Win32 uygulaması bağımlılıklarını yalnızca Win32 uygulamanız eklendikten ve Intune 'a yüklendikten sonra ekleyebilirsiniz. Win32 uygulamanız eklendikten sonra, Win32 uygulamanızın bölmesinde **Bağımlılıklar** seçeneğini görürsünüz. 

Herhangi bir Win32 uygulaması bağımlılığının de bir Win32 uygulaması olması gerekir. Tek MSI LOB uygulamaları veya Microsoft Store uygulamaları gibi diğer uygulama türlerine bağlı olarak desteklenmez.

Uygulama bağımlılığı eklerken, uygulama adı ve yayımcı temelinde arama yapabilirsiniz. Ek olarak, eklenen bağımlılıklarınızı uygulama adı ve yayımcıya göre sıralayabilirsiniz. Daha önce eklenen uygulama bağımlılıkları, eklenen uygulama bağımlılıkları listesinde seçilemez. 

Her bağımlı uygulamanın otomatik olarak yüklenip yüklenmeyeceğini seçebilirsiniz. Varsayılan olarak, **otomatik olarak install** seçeneği her bağımlılık için **Evet** olarak ayarlanır. Bağımlı uygulama kullanıcı veya cihaza hedeflenmese bile, bağımlı uygulamayı otomatik olarak yükleyerek Intune, Win32 uygulamanızı yüklemeden önce bağımlılığı karşılamak üzere uygulamayı cihaza yükler. 

Bir bağımlılığın özyinelemeli alt bağımlılıklara sahip olabileceğini ve ana bağımlılık yüklenmeden önce her bir alt bağımlılığın yükleneceğini aklınızda olması önemlidir. Bunlara ek olarak, bağımlılıklar yüklemesi, bir bağımlılık düzeyinde belirli bir sırayı takip etmez.

### <a name="select-the-dependencies"></a>Bağımlılıkları seçin

**Bağımlılıklar** sayfasında, Win32 uygulamanızın yüklenebilmesi için yüklenmesi gereken uygulamaları seçin:
1. **Ekle** ' yi seçerek **bağımlılık Ekle** bölmesini görüntüleyin.
3. Bağımlı uygulamaları ekleyin ve ardından **Seç**' e tıklayın.
4. **Otomatik olarak install** sütununun altında **Evet** veya **Hayır** ' ı seçerek bağımlı uygulamaların otomatik olarak yüklenip yüklenmeyeceğini seçin.

Bağımlılıkları seçtikten sonra, **İleri** ' yi seçerek **kapsam etiketleri** sayfasını görüntüleyin.

### <a name="understand-additional-dependency-details"></a>Ek bağımlılık ayrıntılarını anlayın

Kullanıcı, bağımlı uygulamaların, Win32 uygulama yükleme işleminin bir parçası olarak indirilmekte olduğunu ve yüklendiğini belirten Windows bildirimleri ' ni görür. Ayrıca, bağımlı bir uygulama yüklü olmadığında, Kullanıcı genellikle aşağıdaki bildirimlerden birini görür:
- Bir veya daha fazla bağımlı uygulama yüklenemedi.
- Bir veya daha fazla bağımlı uygulama gereksinimi karşılanmadı.
- Bir veya daha fazla bağımlı uygulama, cihazın yeniden başlatılmasını bekliyor.

**Otomatik yükleme** sütununa bir bağımlılık koyulamıyor seçeneğini belirlerseniz, Win32 uygulama yüklemesi denenmez. Ayrıca, uygulama raporlama bağımlılığın işaretli olduğunu gösterir `failed` ve bir hata nedeni sağlar. Win32 uygulaması [yükleme ayrıntılarında](troubleshoot-app-install.md#win32-app-installation-troubleshooting)sağlanmış bir hata (veya uyarı) seçerek bağımlılık yükleme hatasını görüntüleyebilirsiniz.

Her bağımlılık, Intune Win32 uygulaması yeniden deneme mantığına uyar (beş dakika bekledikten sonra üç kez yüklemeyi deneyin) ve küresel yeniden değerlendirme zamanlaması. Ayrıca, bağımlılıklar yalnızca cihaza Win32 uygulamasını yükleme sırasında uygulanabilir. Bağımlılıklar bir Win32 uygulamasını kaldırmak için geçerli değildir. Bir bağımlılığı silmek için, bağımlılık listesi satırının sonunda bulunan bağımlı uygulamanın sol tarafındaki üç nokta (üç nokta) simgesini seçmeniz gerekir. 

## <a name="step-6-select-scope-tags-optional"></a>6. Adım: kapsam etiketlerini seçin (isteğe bağlı)
Intune 'da istemci uygulama bilgilerini kimlerin görebileceğini anlamak için kapsam etiketlerini kullanabilirsiniz. Kapsam etiketleri hakkında tam Ayrıntılar için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md).

İsteğe bağlı olarak uygulamanın kapsam etiketlerini eklemek için **kapsam etiketlerini Seç** ' e tıklayın. Sonra **atamalar** sayfasını göstermek için **İleri** ' yi seçin.

## <a name="step-7-assignments"></a>7. Adım: atamalar

**Kayıtlı cihazlar Için** **gerekli**olan, kullanılabilir olan cihazları seçebilir veya uygulama için Grup atamalarını **kaldırabilirsiniz** . Daha fazla bilgi için bkz. [kullanıcıları ve cihazları düzenlemek için grup ekleme](../fundamentals/groups-add.md) ve [Microsoft Intune olan gruplara uygulama atama](apps-deploy.md).

1. Belirli bir uygulama için atama türü seçin:
    - **Gerekli**: Uygulama, seçili gruplardaki cihazlara yüklenir.
    - **Kayıtlı cihazlar Için kullanılabilir**: kullanıcılar uygulamayı şirket portalı uygulamasından veya şirket portalı Web sitesinden yükler.
    - **Kaldırma**: Uygulama, seçilen gruplardaki cihazlardan kaldırılır.
2. **Grup Ekle** ' yi seçin ve bu uygulamayı kullanacak grupları atayın.
3. **Grupları seçin** bölmesinde, kullanıcılara veya cihazlara göre atanacak grupları seçin.
4. Gruplarınızı seçtikten sonra, **Son Kullanıcı bildirimleri**, **kullanılabilirliği**ve **yükleme son tarihini**de ayarlayabilirsiniz. Daha fazla bilgi için bkz. [Win32 uygulama kullanılabilirliğini ve bildirimlerini ayarlama](apps-win32-app-management.md#set-win32-app-availability-and-notifications).
5. Bu uygulama atamasının Kullanıcı gruplarını etkilemesini istemiyorsanız, **mod** sütununun altına **dahil** ' ı seçin. **Atama düzenleme** bölmesinde, **mod** değerini **dahil edildi** iken **hariç**olarak değiştirin. **Atama düzenleme** bölmesini kapatmak için **Tamam ' ı** seçin.
6. **Uygulama ayarları** bölümünde, uygulama için **teslim iyileştirme önceliği** değerini seçin. Bu ayar, uygulama içeriğinin nasıl indirileceğini saptacaktır. Uygulama içeriğini atamaya göre arka plan modunda veya ön plan modunda indirmeyi tercih edebilirsiniz. 

Uygulamalar için atamaları ayarlamayı bitirdikten sonra, **gözden geçir + oluştur** sayfasını göstermek için **İleri** ' yi seçin.

## <a name="step-8-review-and-create"></a>8. Adım: Inceleme ve oluşturma

1. Uygulama için girdiğiniz değerleri ve ayarları gözden geçirin. Uygulama bilgilerini doğru yapılandırdığınızdan emin olun.
2. Uygulamayı Intune 'a eklemek için **Oluştur** ' u seçin.

    LOB uygulaması için **genel bakış** bölmesi görüntülenir.

Bu noktada, Intune 'a bir Win32 uygulaması ekleme adımlarını tamamladınız. Uygulama atama ve izleme hakkında bilgi için bkz. [Microsoft Intune ile uygulamaları gruplara atama](apps-deploy.md) ve [Microsoft Intune ile uygulama bilgilerini ve atamalarını izleme](apps-monitor.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune ile uygulama bilgilerini ve atamalarını izleme](apps-monitor.md)
- [Win32 uygulamasında sorun giderme](apps-win32-troubleshoot.md)
