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
ms.openlocfilehash: 793f5992927a2ba1f93876ad1931300f0aed7550
ms.sourcegitcommit: 54a771f1a632aef5d6bf8c71ce1e2c7823513b52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2020
ms.locfileid: "90003457"
---
# <a name="add-assign-and-monitor-a-win32-app-in-microsoft-intune"></a>Microsoft Intune bir Win32 uygulaması ekleyin, atayın ve izleyin

[Microsoft Win32 içerik hazırlama aracı](https://go.microsoft.com/fwlink/?linkid=2065730)'Nı kullanarak [Intune 'a karşıya yüklenecek bir Win32 uygulamasını hazırladıktan](apps-win32-prepare.md) sonra, uygulamayı Intune 'a ekleyebilirsiniz. Karşıya yüklenecek Win32 uygulamasını hazırlama hakkında daha fazla bilgi edinmek için bkz. [Win32 uygulama içeriğini karşıya yükleme Için hazırlama](apps-win32-prepare.md).

## <a name="prerequisites"></a>Önkoşullar

Win32 uygulama yönetimini kullanmak için aşağıdaki ölçütleri karşıladığınızdan emin olun:

- Windows 10 sürüm 1607 veya üzeri (Enterprise, Pro ve eğitim sürümleri)
- Windows 10 istemcisi: 
  - Cihazların Azure AD 'ye katılması ve otomatik kaydı yapılmalıdır. Intune yönetim uzantısı, Azure AD 'ye katılmış, karma etki alanına katılmış, Grup İlkesi kayıtlı cihazlar desteklenir. 
  > [!NOTE]
  > Grup İlkesi kayıtlı senaryosu için Son Kullanıcı, Windows 10 cihazını birleştirmek için yerel kullanıcı hesabını kullanır. Kullanıcının AAD Kullanıcı hesabını kullanarak cihazda oturum açması ve Intune 'a kaydedilmesi gerekir. Intune yönetim uzantısı, bir PowerShell betiği veya bir Win32 uygulaması kullanıcı veya cihaza hedeflenirse, bu cihaza Intune yönetim uzantısını yükler.
- Windows uygulama boyutu uygulama başına 8 GB 'A göre belirlenir.

Standart bir iş kolu (LOB) uygulaması gibi, Microsoft Intune için bir Win32 uygulaması da ekleyebilirsiniz. Bu gibi uygulamalar normalde şirket içinde veya üçüncü taraflarca yazılır. 

## <a name="process-flow-to-add-a-win32-app-to-intune"></a>Intune 'a bir Win32 uygulaması eklemek için işlem akışı

<img alt="Process flow to add a Win32 app to Intune" src="./media/apps-win32-app-management/add-win32-app.svg" width="500">

## <a name="add-a-win32-app-to-intune"></a>Intune 'a bir Win32 uygulaması ekleme

Aşağıdaki adımlar Windows uygulamasını Intune'a eklemenize yardımcı olacak yönergeler sağlar.

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
2. **Uygulamalar**  >  **tüm uygulamalar**  >  **Ekle**' yi seçin.
3. **Uygulama türünü seçin** bölmesinde, **diğer** uygulama türleri altında **Windows uygulaması (Win32)** öğesini seçin.

    > [!IMPORTANT]
    > Microsoft Win32 Içerik hazırlığı aracının en son sürümünü kullandığınızdan emin olun. En son sürümü kullanmıyorsanız, uygulamanın Microsoft Win32 Içerik hazırlığı aracının daha eski bir sürümü kullanılarak paketlenmediğini belirten bir uyarı görürsünüz. 

4. **Seç**’e tıklayın. **Uygulama ekleme** adımları görüntülenir.

## <a name="step-1-app-information"></a>1. Adım: uygulama bilgileri

### <a name="select-the-app-package-file"></a>Uygulama paketi dosyasını seçin

1. **Uygulama Ekle** bölmesinde **uygulama paketi dosyası seç**' e tıklayın. 
2. **Uygulama paket dosyası** bölmesinde gözat düğmesini seçin. Daha sonra *.intunewin* uzantılı bir Windows yükleme dosyası seçin.
   Uygulama ayrıntıları görüntülenir.
3. İşiniz bittiğinde, **uygulama paketi dosyası** bölmesinde **Tamam** ' ı seçin.

### <a name="set-app-information"></a>Uygulama bilgilerini ayarla

1. **Uygulama bilgileri** sayfasında uygulamanızın ayrıntılarını ekleyin. Seçtiğiniz uygulamaya bağlı olarak bu bölmedeki değerlerden bazıları otomatik olarak doldurulabilir.
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
    - **Logo**: Uygulamayla ilişkilendirilen bir simgeyi karşıya yükleyin. Bu simge, kullanıcılar Şirket Portalı’na göz atarken uygulamayla birlikte görüntülenir.
2. **İleri** ' ye tıklayarak **Program** sayfasını görüntüleyin.

## <a name="step-2-program"></a>2. Adım: program

1. **Program** sayfasında, uygulama için uygulama yükleme ve kaldırma komutlarını yapılandırın:
    - **Yükleme komutu**: uygulamayı yüklemek için yükleme komut satırını tamamen ekleyin. 

        Örneğin, uygulama dosyanızın adı **MyApp123** ise şunu ekleyin: <br>
        `msiexec /p "MyApp123.msp"`<p>
        Ve uygulama ise, `ApplicationName.exe` komut uygulamanın adı ve ardından paket tarafından desteklenen komut bağımsız değişkenleri (anahtarlar) gelir. <br>
        Örneğin:<br>
        `ApplicationName.exe /quiet`<br>
        Yukarıdaki komutta `ApplicationName.exe` paket, `/quiet` komut bağımsız değişkenini destekler.<p> 
        Uygulama paketi tarafından desteklenen belirli bağımsız değişkenler için uygulama satıcınıza başvurun.

        > [!IMPORTANT]
        > Yöneticiler, komut araçlarını kullandıklarında dikkatli olmalıdır. Yükleme ve kaldırma komutu alanı kullanılarak beklenmeyen veya zararlı komutlar geçirilebilir.

    - **Kaldır komutu**: uygulamayı uygulamanın GUID 'ine göre kaldırmak için kaldırma komut satırını tamamen ekleyin. 

        Örneğin:<br>
        `msiexec /x "{12345A67-89B0-1234-5678-000001000000}"`

    - **Davranışı yükler**: Install davranışını **sistem** veya **Kullanıcı**olarak ayarlayın.

        > [!NOTE]
        > Bir Win32 uygulamasını **Kullanıcı** veya **Sistem** bağlamında yüklenecek şekilde yapılandırabilirsiniz. **Kullanıcı** bağlamı yalnızca belirli bir kullanıcıyı ifade eder. **Sistem** bağlamı bir Windows 10 cihazın tüm kullanıcılarını ifade eder.
        >
        > Son kullanıcıların Win32 uygulamalarını yüklemek için cihazda oturum açmış olmaları gerekmez.
        > 
        > Win32 uygulaması yükleme ve kaldırma, uygulama kullanıcı bağlamında yüklenmek üzere ayarlandığında ve cihazdaki son kullanıcının yönetici ayrıcalıklarına sahip olması durumunda yönetici ayrıcalıkları altında (varsayılan olarak) yürütülür.
    
    - **Cihaz yeniden başlatma davranışı**: aşağıdaki seçeneklerden birini belirleyin:
        - **Dönüş kodlarına dayalı davranışı belirleme**: cihazı dönüş kodlarına göre yeniden başlatmak için bu seçeneği belirleyin.
        - **Belirli bir eylem yok**: MSI tabanlı uygulamaların uygulama yüklemesi sırasında cihaz yeniden başlatmalarının görüntülenmesini sağlamak için bu seçeneği belirleyin.
        - **Uygulama yükleme bir cihazın yeniden başlatılmasını zorlayabilir**: uygulama yüklemesinin yeniden başlatmalar olmadan tamamlanmasına izin vermek için bu seçeneği belirleyin.
        - **Intune zorunlu bir cihaz yeniden başlatmaya zorlayacaktır**: başarılı bir uygulama yüklemesinden sonra cihazı her zaman yeniden başlatmak için bu seçeneği belirleyin.

    - **Yükleme sonrası davranışı belirtmek için dönüş kodlarını belirtin**: uygulama yükleme yeniden deneme davranışını veya yükleme sonrası davranışını belirtmek için kullanılan dönüş kodlarını ekleyin. Dönüş kodu girdileri varsayılan olarak uygulama oluşturma işlemi sırasında eklenir. Bununla birlikte, başka dönüş kodları ekleyebilir veya mevcut dönüş kodlarını değiştirebilirsiniz.
        1. **Kod türü** sütununda, **kod türünü** aşağıdakilerden birine ayarlayın:
            - **Failed** : bir uygulama yükleme hatasını gösteren dönüş değeri.
            - **Donanımdan önyükleme** – Donanımdan önyükleme dönüş kodu, istemcide önyükleme yapılmadan sonraki Win32 uygulamalarının yüklenmesine izin vermez. 
            - **Yazılımdan önyükleme** – Yazılımdan önyükleme dönüş kodu, istemci önyüklemesine gerek kalmadan sonraki Win32 uygulamasının yüklenmesine izin verir. Geçerli uygulamanın yüklemesini tamamlamak için önyükleme gereklidir.
            - **Yeniden deneme** – Yeniden deneme dönüş koduyla aracı uygulamayı yüklemeyi üç kez dener. Her denemeden sonra 5 dakika bekler. 
            - **Başarılı** – Uygulamanın başarıyla yüklendiğini belirten dönüş kodu.
        2. Gerekirse, ek dönüş kodları eklemek için **Ekle** ' ye tıklayın veya varolan dönüş kodlarını değiştirin.
2. **İleri** ' ye tıklayarak **gereksinimler** sayfasını görüntüleyin.        

## <a name="step-3-requirements"></a>3. Adım: gereksinimler

1. **Gereksinimler** sayfasında, uygulama yüklenmeden önce cihazların karşılaması gereken gereksinimleri belirtin:
    - **İşletim sistemi mimarisi**: Uygulamayı yüklemek için gereken mimarileri seçin.
    - **Minimum işletim sistemi**: Uygulamayı yüklemek için gereken minimum işletim sistemini seçin.
    - **Gerekli disk alanı (MB)**: İsteğe bağlı olarak, uygulamayı yüklemek için sistem sürücüsünde gereken boş disk alanını ekleyin.
    - **Gerekli fiziksel bellek (MB)**: İsteğe bağlı olarak, uygulamayı yüklemek için gereken fiziksel belleği (RAM) ekleyin.
    - **Gereken en düşük mantıksal işlemci sayısı**: İsteğe bağlı olarak, uygulamayı yüklemek için gereken en düşük mantıksal işlemci sayısını ekleyin.
    - **Gereken en düşük CPU hızı (MHz)**: İsteğe bağlı olarak, uygulamayı yüklemek için gereken en düşük CPU hızını ekleyin.
    - **Ek gereksinim kurallarını yapılandırın**: 
        1. **Gereksinim kuralı ekle** bölmesini göstermek ve ek gereksinim kurallarını yapılandırmak için **Ekle** ' ye tıklayın. Gereksinimin nasıl doğrulanacağını belirlemek için kullanacağınız kural türünü seçmek için **gereksinim türünü** seçin. Gereksinim kuralları dosya sistemi bilgilerini, kayıt defteri değerlerini veya PowerShell komut dosyalarını temel alabilir. 
            - **Dosya**: **Gereksinim türü**olarak **Dosya** ' yı seçtiğinizde, gereksinim kuralı bir dosya veya klasör, tarih, sürüm veya boyut algılamamalıdır. 
                - **Yol** – Algılanacak dosya veya klasörün bulunduğu klasörün tam yolu.
                - **Dosya veya klasör** - Algılanacak dosya veya klasör.
                - **Özellik** : uygulamanın varlığını doğrulamak için kullanılan kural türünü seçin.
                - **64 bit istemciler üzerinde bir 32 bit uygulamayla ilişkilendirildi** - Tüm yol ortam değişkenlerini 64 bit istemciler üzerinde 32 bit bağlamında genişletmek için **Evet**'i seçin. Tüm yol değişkenlerini 64 bit istemciler üzerinde 64 bit bağlamında genişletmek için **Hayır**'ı (varsayılan) seçin. 32 bit istemciler her zaman 32 bit bağlamını kullanır.
            - **Kayıt defteri**: **Gereksinim türü**olarak **kayıt defteri** ' ni seçtiğinizde, gereksinim kuralı değer, dize, tamsayı veya sürüme göre bir kayıt defteri ayarı tespit etmelidir.
                - **Anahtar yolu** – Algılanacak değerin bulunduğu kayıt defteri girdisinin tam yolu.
                - **Değer adı** - Algılanacak kayıt defteri değerinin adı. Bu değer boşsa algılama anahtarda gerçekleştirilir. Algılama yöntemi dosya veya klasör varlığından farklı bir yöntemse, algılama değeri olarak anahtarın (varsayılan) değeri kullanılır.
                - **Kayıt defteri anahtarı gereksinimi** – gereksinim kuralının nasıl doğrulanacağını belirlemek için kullanılan kayıt defteri anahtarı karşılaştırma türünü seçin.
                - **64 bit istemciler üzerinde bir 32 bit uygulamayla ilişkilendirildi** - 64 bit istemcilerde 32 bit kayıt defterinde arama yapmak için **Evet**'i seçin. 64 bit istemcilerde 64 bit kayıt defterinde arama yapmak için **Hayır**'ı (varsayılan) seçin. 32 bit istemcilerde her zaman 32 bit kayıt defterinde arama yapılır.
            - **Komut dosyası**: Intune konsolunda kullanabileceğiniz dosya, kayıt defteri veya başka bir yöntemi temel alan bir gereksinim kuralı oluştur, **Gereksinim türü**olarak **komut dosyasını** seçin.
                - **Betik dosyası** – PowerShell betiği tabanlı gereksinim kuralı için, var olan kod 0 Ise, stdout 'ı daha ayrıntılı olarak algılayacağız. Örneğin, STDOUT değerini 1 değeri olan bir tamsayı olarak tespit edebilirsiniz.
                - **Komut dosyasını 64 bit istemcilerde 32 bitlik işlem olarak çalıştır** -betiği, 64 bit istemcilerde bir 32 bit işlemde çalıştırmak için **Evet** ' i seçin. Komut dosyasını 64 bit istemcilerde 64 bitlik bir işlemde çalıştırmak için **Hayır** (varsayılan) seçeneğini belirleyin. 32 bitlik istemciler betiği 32 bit bir işlemde çalıştırır.
                - **Bu betiği oturum açmış oturum açma kimlik bilgilerini kullanarak Çalıştır**: komut dosyasını oturum açan cihaz kimlik bilgilerini * * kullanarak çalıştırmak için **Evet** ' i seçin.
                - **Betik imzası denetimini zorla** - Betiğin güvenilen bir yayımcı tarafından imzalandığını doğrulamak için **Evet**'i seçin. Bu doğrulama betiğin hiçbir uyarı veya istem gösterilmeden çalıştırılmasına olanak tanır. Betik engellenmeden çalıştırılır. Betiği imza doğrulaması yapılmadan son kullanıcının onayıyla çalıştırmak için **Hayır**'ı (varsayılan) seçin.
                - **Çıkış verisi türünü seçin**: bir gereksinim kuralı eşleşmesi belirlenirken kullanılan veri türünü seçin.
        2. Gereksinim kurallarını ayarlamayı tamamladığınızda **Tamam**' ı seçin.
2. **İleri** ' ye tıklayarak **algılama kuralları** sayfasını görüntüleyin.   

## <a name="step-4-detection-rules"></a>4. Adım: algılama kuralları

1. **Algılama kuralları** sayfasında, uygulamanın varlığını algılamak için kuralları yapılandırın:
    
    **Kurallar biçimi**: uygulama varlığının nasıl algılanacağını seçin. Algılama kurallarını el ile yapılandırmayı seçebileceğiniz gibi uygulamanın varlığını algılamak için özel bir betik de kullanabilirsiniz. En az bir algılama kuralı seçmelisiniz. 

    > [!NOTE]
    > **Algılama kuralları** bölmesinde birden fazla kural eklemeyi seçebilirsiniz. Uygulamanı algılanması için **tüm** kuralların koşullarına uyulmalıdır.
    >
    > Intune, uygulamanın cihazda mevcut olmadığını algılarsa, uygulamayı 24 saat sonra yeniden sunar. Bu, yalnızca gerekli amaca yönelik uygulamalar için oluşur.

    - **Algılama kurallarını el ile yapılandırın** - Şu kural türlerinden birini seçebilirsiniz:
        1. **MSI** – MSI sürüm denetimine dayanarak doğrulayın. Bu seçenek tek bir kez eklenebilir. Bu kural türünü seçtiğinizde iki ayarınız olur:
            - **MSI ürün kodu** – Uygulama için geçerli bir MSI ürün kodu ekleyin.
            - **MSI ürün sürümü denetimi** – MSI ürün koduna ek olarak MSI ürün sürümünü doğrulamak için **Evet**'i seçin.
        2. **Dosya** – Dosya veya klasör algılama, tarih, sürüm veya boyut temelinde doğrulayın.
            - **Yol** – Algılanacak dosya veya klasörün bulunduğu klasörün tam yolu.
            - **Dosya veya klasör** - Algılanacak dosya veya klasör.
            - **Algılama yöntemi** – Uygulamanın varlığını doğrulamak için kullanılan algılama yönteminin türünü seçin.
            - **64 bit istemciler üzerinde bir 32 bit uygulamayla ilişkilendirildi** - Tüm yol ortam değişkenlerini 64 bit istemciler üzerinde 32 bit bağlamında genişletmek için **Evet**'i seçin. Tüm yol değişkenlerini 64 bit istemciler üzerinde 64 bit bağlamında genişletmek için **Hayır**'ı (varsayılan) seçin. 32 bit istemciler her zaman 32 bit bağlamını kullanır.
            
            **Dosya tabanlı algılama örnekleri**
            1. Dosyanın varlığını denetleyin.
         
                ![Algılama kuralı bölmesi - dosya varlığı ekran görüntüsü](./media/apps-win32-app-management/apps-win32-app-03.png)
        
            2. Klasör varlığını denetleyin.
         
                ![Algılama kuralı bölmesi - klasör varlığı ekran görüntüsü](./media/apps-win32-app-management/apps-win32-app-04.png)
        
        3. **Kayıt defteri** – Değer, dize, tamsayı veya sürüm temelinde doğrulayın.
            - **Anahtar yolu** – Algılanacak değerin bulunduğu kayıt defteri girdisinin tam yolu. Geçerli bir sözdizimi HKEY_LOCAL_MACHINE \Software\WinRAR veya HKLM\Software\WinRAR.
            - **Değer adı** - Algılanacak kayıt defteri değerinin adı. Bu değer boşsa algılama anahtarda gerçekleştirilir. Algılama yöntemi dosya veya klasör varlığından farklı bir yöntemse, algılama değeri olarak anahtarın (varsayılan) değeri kullanılır.
            - **Algılama yöntemi** – Uygulamanın varlığını doğrulamak için kullanılan algılama yönteminin türünü seçin.
            - **64 bit istemciler üzerinde bir 32 bit uygulamayla ilişkilendirildi** - 64 bit istemcilerde 32 bit kayıt defterinde arama yapmak için **Evet**'i seçin. 64 bit istemcilerde 64 bit kayıt defterinde arama yapmak için **Hayır**'ı (varsayılan) seçin. 32 bit istemcilerde her zaman 32 bit kayıt defterinde arama yapılır.
            
            **Kayıt defteri temelinde algılama örnekleri**
            1. Kayıt defteri anahtarının varlığını denetleyin.
            
                ![Algılama kuralı bölmesi - kayıt defteri anahtarı var ekran görüntüsü](./media/apps-win32-app-management/apps-win32-app-05.png)    
            
            2. Kayıt defteri değerinin var olup olmadığını denetleyin.
        
                ![Algılama kuralı bölmesi - kayıt defteri değeri varlığı ekran görüntüsü](./media/apps-win32-app-management/apps-win32-app-06.png)    
        
            3. Kayıt defteri değer dizesinin eşitliğini denetleyin.
        
                ![Algılama kuralı bölmesi - kayıt defteri değer dizesi eşittir ekran görüntüsü](./media/apps-win32-app-management/apps-win32-app-07.png)    
     
    - **Özel algılama betiği kullan** – Bu uygulamayı algılamak için kullanılacak PowerShell betiğini belirtin. 
    
       1. **Betik dosyası** – İstemcide uygulamanın varlığını algılayacak PowerShell betiğini seçin. Betik hem 0 değerinde çıkış kodu döndürdüğünde hem de STDOUT'a bir dize değeri yazdığında uygulama algılanır.

       2. **Komut dosyasını 64 bit istemcilerde 32 bitlik işlem olarak çalıştır** -betiği, 64 bit istemcilerde bir 32 bit işlemde çalıştırmak için **Evet** ' i seçin. Komut dosyasını 64 bit istemcilerde 64 bitlik bir işlemde çalıştırmak için **Hayır** (varsayılan) seçeneğini belirleyin. 32 bitlik istemciler betiği 32 bit bir işlemde çalıştırır.

       3. **Betik imzası denetimini zorla** - Betiğin güvenilen bir yayımcı tarafından imzalandığını doğrulamak için **Evet**'i seçin. Bu doğrulama betiğin hiçbir uyarı veya istem gösterilmeden çalıştırılmasına olanak tanır. Betik engellenmeden çalıştırılır. Betiği imza doğrulaması yapılmadan son kullanıcının onayıyla çalıştırmak için **Hayır**'ı (varsayılan) seçin.
    
            Intune Aracısı, komut dosyasının sonuçlarını denetler. Betik tarafından standart çıkış (STDOUT) akışına, standart hata (STDERR) akışına ve çıkış koduna yazılan değerleri okur. Betikten sıfırdan farklı bir değerle çıkılırsa, betik başarısız olur ve uygulama algılama durumu Yüklü Değil olur. Çıkış kodu sıfırsa ve STDOUT veri içeriyorsa, uygulama algılama durumu Yüklü'dür. 

            > [!NOTE]
            > Microsoft, betiğinizi UTF-8 olarak kodlamayı önerir. Betikten 0 değeriyle çıkılırsa, betiğin yürütülmesi başarılı olmuştur. İkinci çıkış kanalı uygulamanın algılandığını gösterir - STDOUT verileri uygulamanın istemcide bulunduğunu gösterir. STDOUT akışından belirli bir dize beklemeyiz.

2. Kurallarınızı ekledikten sonra, **Bağımlılıklar** sayfasını göstermek için **İleri** ' yi seçin.

## <a name="step-5-dependencies"></a>5. Adım: bağımlılıklar

Uygulama bağımlılıkları, Win32 uygulamanızın yüklenebilmesi için yüklenmesi gereken uygulamalardır. Diğer uygulamaların bağımlılık olarak yüklenmesini zorunlu kılabilirsiniz. Özellikle, cihazın Win32 uygulamasını yüklemeden önce bağımlı uygulamaları yüklemesi gerekir. Dahil edilen bağımlılıkların bağımlılıklarını ve uygulamanın kendisini içeren en fazla 100 bağımlılığı vardır. Win32 uygulaması bağımlılıklarını yalnızca Win32 uygulamanız eklendikten ve Intune 'a yüklendikten sonra ekleyebilirsiniz. Win32 uygulamanız eklendikten sonra, Win32 uygulamanızın bölmesinde **Bağımlılıklar** seçeneğini görürsünüz. 

Herhangi bir Win32 uygulaması bağımlılığının de bir Win32 uygulaması olması gerekir. Tek MSI LOB uygulamaları veya Mağaza uygulamaları gibi diğer uygulama türlerine bağlı olarak desteklenmez.

Uygulama bağımlılığı eklerken, uygulama adı ve yayımcı temelinde arama yapabilirsiniz. Ek olarak, eklenen bağımlılıklarınızı uygulama adı ve yayımcıya göre sıralayabilirsiniz. Daha önce eklenen uygulama bağımlılıkları, eklenen uygulama bağımlılığı listesinde seçilemez. 

Her bağımlı uygulamanın otomatik olarak yüklenip yüklenmeyeceğini seçebilirsiniz. Varsayılan olarak, **otomatik olarak install** seçeneği her bağımlılık için **Evet** olarak ayarlanır. Bağımlı uygulama kullanıcı veya cihaza hedeflenmese bile, bağımlı uygulamayı otomatik olarak yükleyerek Intune, Win32 uygulamanızı yüklemeden önce bağımlılığı karşılamak üzere uygulamayı cihaza yükler. Bir bağımlılık özyinelemeli alt bağımlılıklara sahip olabileceğini ve ana bağımlılığı yüklemeden önce her bir alt bağımlılığın yükleneceğini unutmayın. Ayrıca, bağımlılıkların yüklenmesi belirli bir bağımlılık düzeyinde bir yükleme sırasına uymuyor.

### <a name="select-the-dependencies"></a>Bağımlılıkları seçin

**Bağımlılıklar** sayfasında, Win32 uygulamanızın yüklenebilmesi için yüklenmesi gereken uygulamaları seçin:
1. **Bağımlılık Ekle** bölmesini göstermek için **Ekle** ' ye tıklayın.
3. Bağımlı uygulamaları ekledikten sonra **Seç**' e tıklayın.
4. **Otomatik olarak install** sütununun altında **Evet** veya **Hayır** ' ı seçerek bağımlı uygulamanın otomatik olarak yüklenip yüklenmeyeceğini seçin.
5. **İleri** ' ye tıklayarak **kapsam etiketleri** sayfasını görüntüleyin.

### <a name="understand-additional-dependency-details"></a>Ek bağımlılık ayrıntılarını anlayın

Son Kullanıcı, bağımlı uygulamaların Win32 uygulama yükleme işleminin bir parçası olarak indirilmekte olduğunu ve yüklendiğini belirten Windows bildirim bildirimleri ' ni görür. Ayrıca, bağımlı bir uygulama yüklü olmadığında, son kullanıcı genellikle aşağıdaki bildirimlerden birini görür:
- 1 veya daha fazla bağımlı uygulama yüklenemedi
- 1 veya daha fazla bağımlı uygulama gereksinimi karşılanmadı
- 1 veya daha fazla bağımlı uygulama, cihaz yeniden başlatma bekliyor

**Otomatik olarak** bir bağımlılık yüklememeyi seçerseniz, Win32 uygulama yüklemesi denenmez. Ayrıca, uygulama raporlama bağımlılığın işaretli olduğunu gösterir `failed` ve ayrıca bir hata nedeni sağlar. Win 32 uygulama [yükleme ayrıntılarında](troubleshoot-app-install.md#win32-app-installation-troubleshooting)belirtilen bir hataya (veya uyarıya) tıklayarak bağımlılık yükleme hatasını görüntüleyebilirsiniz.

Her bağımlılık, Intune Win32 uygulaması yeniden deneme mantığına uyar (5 dakika bekledikten sonra 3 kez yüklemeyi deneyin) ve küresel yeniden değerlendirme zamanlaması. Ayrıca, bağımlılıklar yalnızca cihaza Win32 uygulamasını yükleme sırasında uygulanabilir. Bağımlılıklar bir Win32 uygulamasını kaldırmak için geçerli değildir. Bir bağımlılığı silmek için, bağımlılık listesi satırının sonunda bulunan bağımlı uygulamanın solundaki üç noktaya (üç nokta) tıklamalısınız. 

## <a name="step-6-select-scope-tags-optional"></a>6. Adım: kapsam etiketlerini seçin (isteğe bağlı)
Intune 'da istemci uygulama bilgilerini kimlerin görebileceğini anlamak için kapsam etiketlerini kullanabilirsiniz. Kapsam etiketleri hakkında tam Ayrıntılar için bkz. [Dağıtılmış BT için rol tabanlı erişim denetimi ve kapsam etiketleri kullanma](../fundamentals/scope-tags.md).

1. İsteğe bağlı olarak uygulamanın kapsam etiketlerini eklemek için **kapsam etiketlerini Seç** ' e tıklayın. 
2. **Atamalar** sayfasını göstermek için **İleri** ' ye tıklayın.

## <a name="step-7-assignments"></a>7. Adım: atamalar

**Kayıtlı cihazlar Için** **gerekli**olan, kullanılabilir olan cihazları seçebilir veya uygulama için Grup atamalarını **kaldırabilirsiniz** . Daha fazla bilgi için bkz. [kullanıcıları ve cihazları düzenlemek için grup ekleme](../fundamentals/groups-add.md) ve [Microsoft Intune olan gruplara uygulama atama](apps-deploy.md).

1. Belirli bir uygulama için atama türü seçin:
    - **Gerekli**: Uygulama, seçili gruplardaki cihazlara yüklenir.
    - **Kayıtlı cihazlar için bulunur**: Kullanıcılar, Şirket Portalı uygulamasından veya Şirket Portalı web sitesinden uygulamayı yükler.
    - **Kaldırma**: Uygulama, seçilen gruplardaki cihazlardan kaldırılır.
2. **Grup Ekle** ' ye tıklayın ve bu uygulamayı kullanacak grupları atayın.
3. **Grupları seçin** bölmesinde, kullanıcılara veya cihazlara göre ata ' yı seçin.
4. Gruplarınızı seçtikten sonra, **Son Kullanıcı bildirimleri**, **kullanılabilirliği**ve **yükleme son tarihini**de ayarlayabilirsiniz. Daha fazla bilgi için bkz. [Win32 uygulama kullanılabilirliğini ve bildirimlerini ayarlama](apps-win32-app-management.md#set-win32-app-availability-and-notifications).
5. Herhangi bir kullanıcı grubunu bu uygulama atamasından etkilenmeden dışlamak istiyorsanız, **mod** sütununun altına **dahil** ' ı seçin. **Atama düzenleme** bölmesi görüntülenir. **Modunun** **dışlandığından** **dahil** edilmesini sağlayabilirsiniz. **Atama düzenleme** bölmesini kapatmak için **Tamam** ' ı tıklatın.
6. **Uygulama ayarları** bölümünde, uygulamanın **teslim iyileştirme önceliğini** seçin. Bu ayar, uygulama içeriğinin nasıl indirileceğini saptacaktır. Uygulama içeriğini atamaya göre arka plan modunda veya ön plan modunda indirmeyi tercih edebilirsiniz. 
7. Uygulamalar için atamaları ayarlamayı tamamladıktan sonra, **gözden geçir + oluştur** sayfasını göstermek için **İleri** ' ye tıklayın.

## <a name="step-8-review-and-create"></a>8. Adım: Inceleme ve oluşturma

1. Uygulama için girdiğiniz değerleri ve ayarları gözden geçirin. Uygulama bilgilerini doğru yapılandırdığınızdan emin olun.
2. İşiniz bittiğinde, uygulamayı Intune 'a eklemek için **Oluştur** ' a tıklayın.

    İş kolu uygulaması için **genel bakış** dikey penceresi görüntülenir.

Bu noktada, Intune 'a bir Win32 uygulaması ekleme adımlarını tamamladınız. Uygulama atama ve izleme hakkında bilgi için bkz. [Microsoft Intune ile uygulamaları gruplara atama](apps-deploy.md) ve [Microsoft Intune ile uygulama bilgilerini ve atamalarını izleme](apps-monitor.md).

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune ile uygulama bilgilerini ve atamalarını izleme](apps-monitor.md)
- [Win32 uygulamasında sorun giderme](apps-win32-troubleshoot.md)
