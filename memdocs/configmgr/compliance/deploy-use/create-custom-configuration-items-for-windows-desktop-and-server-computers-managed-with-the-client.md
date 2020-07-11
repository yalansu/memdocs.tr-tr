---
title: Özel yapılandırma öğeleri oluşturma
titleSuffix: Configuration Manager
description: Windows masaüstleri ve sunucuları için özel bir yapılandırma öğesi olan Windows bilgisayarları ve sunucuları ayarlarını yönetme
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 24637862326b029f974843c18ccba835ee5501ba
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240431"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Configuration Manager istemcisiyle yönetilen Windows Masaüstü ve sunucu bilgisayarları için özel yapılandırma öğeleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Configuration Manager istemcisi tarafından yönetilen Windows bilgisayarları ve sunucularının ayarlarını yönetmek için Configuration Manager **özel Windows masaüstleri ve sunucuları** yapılandırma öğesini kullanın.  



## <a name="start-the-wizard"></a>Sihirbazı Başlat

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin ve **yapılandırma öğeleri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **yapılandırma öğesi oluştur**' u seçin.  

3. **Yapılandırma Öğesi Oluştur Sihirbazı** ’nın **Genel**sayfasında, yapılandırma öğesi için bir ad ve isteğe bağlı bir açıklama belirtin.  

4. **Oluşturmak istediğiniz yapılandırma öğesi türünü belirtin** bölümünün altında, **Windows Masaüstleri ve Sunucuları (özel)** seçeneğini belirleyin.  

    > [!TIP]  
    > Bir uygulamanın varlığını denetleyen algılama yöntemi ayarları sağlamak istiyorsanız **Bu yapılandırma dosyası uygulama ayarları içerir** seçeneğini belirleyin.  

5. Configuration Manager konsolundaki yapılandırma öğelerini aramanıza ve filtrelemenize yardımcı olması için kategoriler oluşturup atamak üzere **Kategoriler** ' i seçin.  



## <a name="detection-methods"></a>Algılama yöntemleri  

Yapılandırma öğesi için algılama yöntemi bilgileri sağlamak için bu yordamı kullanın.  

> [!NOTE]  
> Bu bilgiler yalnızca sihirbazın **genel** sayfasındaki **Bu yapılandırma öğesi uygulama ayarlarını içeriyorsa** geçerlidir.  

Configuration Manager bir algılama yöntemi, bir uygulamanın bir bilgisayarda yüklü olup olmadığını algılamak için kullanılan kuralları içerir. Bu algılama, istemcinin yapılandırma öğesi için uyumluluğunu değerlendirir önce oluşur. Bir uygulamanın yüklü olup olmadığını algılamak için uygulamanın Windows Installer dosyasının varlığını algılayabilir, özel bir betik kullanabilir veya uygulamanın yüklenip yüklenmediğine bakılmaksızın yapılandırma öğesinin uyumluluğunu değerlendirmek için **Her zaman uygulamanın yüklü olduğunu varsay** seçeneğini belirleyebilirsiniz.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Windows Installer dosyasını kullanarak bir uygulama yüklemesini algılamak için  

1. **Yapılandırma öğesi oluşturma Sihirbazı**' nın **algılama yöntemleri** sayfasında, **Windows Installer algılamayı kullanma**seçeneğini belirleyin.  

2. **Aç**' ı seçin, algılamak istediğiniz Windows Installer (. msi) dosyasına gidin ve **Aç**' ı seçin.  

3. **Sürüm** alanı, Windows Installer dosyasının sürüm numarasıyla otomatik olarak doldurulur. Görünen değer yanlışsa, buraya yeni bir sürüm numarası girin.  

4. Bilgisayardaki her kullanıcı profilini algılamak istiyorsanız, **Bu uygulama bir veya daha fazla kullanıcı için yüklendi**' ı seçin.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Belirli bir uygulama ve dağıtım türünü algılamak için  

1. **Yapılandırma öğesi oluşturma Sihirbazı**' nın **algılama yöntemleri** sayfasında, **belirli bir uygulama ve dağıtım türünü algılamayı**seçin. **Seç**’i seçin.   

2. **Uygulamayı Belirtin** iletişim kutusunda, algılamak istediğiniz uygulamayı ve ilişkili bir dağıtım türünü seçin.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Özel bir betik kullanarak uygulama yüklemesini algılamak için  

1. **Yapılandırma öğesi oluşturma Sihirbazı**' nın **algılama yöntemleri** sayfasında, **Bu uygulamayı algılamak Için özel bir komut dosyası kullanma**seçeneğini belirleyin.  

2. Listede betiğin dilini seçin. Aşağıdaki biçimlerden birini seçin:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > Sürüm 1810 ' den başlayarak, bir Windows PowerShell betiği bir algılama yöntemi olarak çalıştırıldığında, Configuration Manager istemci PowerShell 'i `-NoProfile` parametresiyle çağırır. Bu seçenek PowerShell 'i profil olmadan başlatır. PowerShell profili, PowerShell başladığında çalışan bir betiktir. <!--3607762-->  

3. **Aç**' ı seçin, kullanmak istediğiniz betiğe gidin ve **Aç**' ı seçin.  



## <a name="specify-supported-platforms"></a>Desteklenen platformları belirtme  

**Yapılandırma öğesi oluşturma Sihirbazı**' nın **Desteklenen platformlar** sayfasında, yapılandırma öğesinin uyumluluk Için değerlendirileceğini istediğiniz Windows sürümlerini seçin veya **Tümünü Seç**' i seçin.

**Windows sürümünü el ile de belirtebilirsiniz**. **Ekle** ' yi seçin ve Windows yapı numarasının her bölümünü belirtin.

> [!NOTE]
> Windows Server 2016 belirtirken, seçimi `All Windows Server 2016 and higher 64-bit)` Windows server 2019 de içerir. Yalnızca Windows Server 2016 ' i belirtmek için, **Windows sürümünü el Ile belirtmek**için seçeneğini kullanın. <!--5866480-->



##  <a name="configure-settings"></a>Ayarları yapılandırma  

Yapılandırma öğesindeki ayarları yapılandırmak için bu yordamı kullanın.  

Ayarlar, istemci cihazlarındaki uyumluluğu değerlendirmek için kullanılan iş koşullarını veya teknik koşulları temsil eder. Yeni bir ayar yapılandırabilir veya referans bilgisayarındaki mevcut bir ayara gidebilirsiniz.  

1. **Yapılandırma öğesi oluşturma Sihirbazı**' nın **Ayarlar** sayfasında **Yeni**' yi seçin.  

2. **Ayar Oluştur** iletişim kutusunun **Genel** sekmesinde aşağıdaki bilgileri sağlayın:  

    - **Ad**: ayar için benzersiz bir ad girin. En fazla 256 karakter kullanabilirsiniz.  

    - **Açıklama**: ayar için bir açıklama girin. En fazla 256 karakter kullanabilirsiniz.  

    - **Ayar türü**: listede, bu ayar için kullanmak üzere aşağıdaki ayar türlerinden birini seçin ve yapılandırın:  
        - [Active Directory sorgusu](#bkmk_adquery)
        - [Bütünleştirilmiş Kod](#bkmk_assembly)
        - [Dosya sistemi](#bkmk_file)
        - [IIS metatabanı](#bkmk_iis)
        - [Kayıt defteri anahtarı](#bkmk_regkey)
        - [Kayıt defteri değeri](#bkmk_regval)
        - [Komut Dosyası](#bkmk_script)
        - [SQL sorgusu](#bkmk_sql)
        - [WQL sorgusu](#bkmk_wql)
        - [XPath sorgusu](#bkmk_xpath)

    - **Veri türü**: koşulun, ayarı değerlendirmek için kullanılmadan önce veriyi döndürdüğü biçimi seçin. **Veri türü** listesi tüm ayar türleri için gösterilmez.  

        > [!Tip]  
        > **Kayan nokta** veri türü, ondalık ayırıcıdan sonra yalnızca üç basamağı destekler.  

3. Bu ayar hakkındaki ek ayrıntıları **Ayar türü** listesi altında yapılandırın. Yapılandırabileceğiniz öğeler, seçmiş olduğunuz ayar türüne bağlı olarak değişiklik gösterir.  

4. Ayarı kaydetmek için **Tamam** ' ı seçin ve **ayar oluştur** iletişim kutusunu kapatın.  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a>Active Directory sorgu

- **LDAP ön eki**: istemci bilgisayarlarındaki uyumluluğu değerlendirmek için Active Directory Domain Services sorgusuna yönelik geçerli bir ön ek belirtin. Genel katalog arama yapmak için ya da kullanın `LDAP://` `GC://` .  

- **Ayırt edici ad (DN)**: istemci bilgisayarlarda uyumluluk için değerlendirilen Active Directory Domain Services nesnesinin ayırt edici adını belirtin.  

- **Arama filtresi**: istemci bilgisayarlarındaki uyumluluğu değerlendirmek için Active Directory Domain Services sorgusunun sonuçlarını daraltmak için isteğe bağlı bir LDAP filtresi belirtin. Sorgunun tüm sonuçlarını döndürmek için girin `(objectclass=*)` .  

- **Arama kapsamı**: Active Directory Domain Services arama kapsamını belirtin  

    - **Taban**: yalnızca belirtilen nesneyi sorgular  

    - **Tek düzey**: Bu seçenek bu Configuration Manager sürümünde kullanılmıyor  

    - **Alt ağaç**: belirtilen nesneyi ve dizindeki tüm alt ağacını sorgular  

- **Özellik**: istemci bilgisayarlarındaki uyumluluğu değerlendirmek için kullanılan Active Directory Domain Services nesnesinin özelliğini belirtin.  

    Örneğin, kullanıcının hatalı parola girme sayısını depolayan Active Directory özelliğini sorgulamak istiyorsanız, `badPwdCount` Bu alana girin.  

- **Sorgu**: **LDAP ön eki**, **ayırt edici ad (DN)**, **arama filtresi** (belirtilmişse) ve **özellik**içindeki girdilerden oluşturulan sorguyu görüntüler.  


### <a name="assembly"></a><a name="bkmk_assembly"></a>Derleme

Bir derleme, uygulamalar arasında paylaştırılabilen bir kod parçasıdır. Derlemeler .dll veya .exe dosya adı uzantısına sahip olabilirler. Genel derleme önbelleği, `%SystemRoot%\Assembly` istemci bilgisayarlarındaki klasördür. Bu önbellek, Windows 'un tüm paylaşılan derlemeleri depoladığı yerdir.  

- **Bütünleştirilmiş kod adı**: Aramak istediğiniz bütünleştirilmiş kod nesnesinin adını belirtir. Ad aynı türdeki diğer derleme nesneleriyle aynı olamaz. Önce genel derleme önbelleğine kaydedin. Bütünleştirilmiş kod adı en çok 256 karakter uzunluğunda olabilir.  


### <a name="file-system"></a><a name="bkmk_file"></a>Dosya sistemi

- **Tür**: listede, bir **Dosya** veya **klasör**için arama yapmak isteyip istemediğinizi seçin.  

- **Yol**: istemci bilgisayarlarda belirtilen dosya veya klasörün yolunu belirtin. Sistem ortam değişkenlerini ve `%USERPROFILE%` ortam değişkenini yolda belirtebilirsiniz.  

    > [!NOTE]  
    > `%USERPROFILE%`Ortam değişkenini **yol** veya **dosya ya da klasör adı** kutularında kullanırsanız, Configuration Manager istemcisi istemci bilgisayardaki tüm Kullanıcı profillerini arar. Bu davranış, dosya veya klasörün birden çok örneğini bulmaya neden olabilir.  
    >   
    > Uyumluluk ayarlarının belirtilen yola erişimi yoksa, bir bulma hatası oluşturulur. Ayrıca, aradığınız dosya o anda kullanımda olduğunda da bulma hatası oluşur.  

    > [!Tip]  
    > Ayarı başvuru bilgisayarındaki değerlerden yapılandırmak için **Araştır** ' ı seçin.   

- **Dosya veya klasör adı**: arama yapılacak dosya veya klasör nesnesinin adını belirtin. Sistem ortam değişkenlerini ve `%USERPROFILE%` ortam değişkenini dosya veya klasör adında belirtebilirsiniz. Joker karakterleri `*` ve dosya adını da kullanabilirsiniz `?` .  

    > [!NOTE]  
    > Bir dosya veya klasör adı belirtir ve joker karakterleri kullanırsanız, Bu bileşim yüksek sayıda sonuç üretebilir. Ayrıca, istemci bilgisayarda yüksek kaynak kullanımına ve sonuçları Configuration Manager bildirirken yüksek ağ trafiğine neden olabilir.  

- **Alt klasörleri dahil et**: aynı zamanda belirtilen yolun altındaki tüm alt klasörlerde arama yapın.  

- **Bu dosya veya klasör 64 bitlik bir uygulamayla ilişkili**: etkinleştirilirse, yalnızca 64 bit bilgisayarlarda 64 bit dosya konumları arayın `%ProgramFiles%` . Bu seçenek etkinleştirilmemişse, hem 64 bitlik konumlarda hem de 32 bit konumlarında arama yapın `%ProgramFiles(x86)%` .  

    > [!NOTE]  
    > Aynı 64 bit bilgisayarda 64 bit ve 32 bit sistem dosyası konumlarının her ikisinde de aynı dosya veya klasör varsa, genel koşul tarafından birden çok dosya bulunur.  

    **Dosya sistemi** ayar türü, **yol** kutusunda bir ağ paylaşımının UNC yolunu belirtmeyi desteklemez.  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a>IIS metatabanı

- **Metatabanı yolu**: Internet INFORMATION SERVICES (IIS) metatabanının geçerli bir yolunu belirtin. Örneğin, `/LM/W3SVC/`.  

- **ÖZELLIK kimliği**: IIS metatabanı ayarının sayısal özelliğini belirtin.  


### <a name="registry-key"></a><a name="bkmk_regkey"></a>Kayıt defteri anahtarı

- **Hive**: aramak istediğiniz kayıt defteri kovanını seçin

    > [!Tip]  
    > Ayarı başvuru bilgisayarındaki değerlerden yapılandırmak için **Araştır** ' ı seçin. Uzak bilgisayardaki bir kayıt defteri anahtarına gitmek için uzak bilgisayarda **Uzak kayıt defteri** hizmetini etkinleştirin.  

- **Anahtar**: aramak istediğiniz kayıt defteri anahtarı adını belirtin. `key\subkey` biçimini kullanın.  

- **Bu kayıt defteri anahtarı 64 bitlik bir uygulamayla ilişkili**: Windows 'un 64 bit sürümünü çalıştıran istemcilerde 32-bit kayıt defteri anahtarlarına ek olarak 64 bit kayıt defteri anahtarları ara.  

    > [!NOTE]  
    > Aynı 64 bit bilgisayarda 64 bit ve 32 bit kayıt defteri konumlarının her ikisinde de aynı kayıt defteri anahtarı varsa, genel koşul tarafından her iki kayıt defteri anahtarı da bulunur.  


### <a name="registry-value"></a><a name="bkmk_regval"></a>Kayıt defteri değeri

- **Hive**: aranacak kayıt defteri kovanını seçin.  

    > [!Tip]  
    > Ayarı başvuru bilgisayarındaki değerlerden yapılandırmak için **Araştır** ' ı seçin. Uzak bilgisayardaki bir kayıt defteri değerine gitmek için uzak bilgisayarda **Uzak kayıt defteri** hizmetini etkinleştirin. Uzak bilgisayara erişmek için yönetici izinlerine de ihtiyacınız vardır.  

- **Anahtar**: aranacak kayıt defteri anahtarı adını belirtin. `key\subkey` biçimini kullanın.  

- **Değer**: belirtilen kayıt defteri anahtarı içinde bulunması gereken değeri belirtin.  

- **Bu kayıt defteri anahtarı 64 bitlik bir uygulamayla ilişkili**: Windows 'un 64 bit sürümünü çalıştıran istemcilerde 32-bit kayıt defteri anahtarlarının yanı sıra 64 bit kayıt defteri anahtarlarında da arama yapın.  

    > [!NOTE]  
    > Aynı 64 bit bilgisayarda 64 bit ve 32 bit kayıt defteri konumlarının her ikisinde de aynı kayıt defteri anahtarı varsa, genel koşul tarafından her iki kayıt defteri anahtarı da bulunur.  


### <a name="script"></a><a name="bkmk_script"></a>SCRIPT

Betik tarafından döndürülen değer, genel koşula uyumluluğun değerlendirmesinde kullanılır. Örneğin, VBScript kullanırken genel koşula *Result* değişken değerini döndürmek için **WScript.Echo Result** komutunu kullanabilirsiniz.  

- **Bulma betiği**: **komut dosyası Ekle**' yi seçin ve bir betik girin veya dosyaya gidin. Bu betik, değeri bulmak için kullanılır. Windows PowerShell, VBScript veya Microsoft JScript betiklerini kullanabilirsiniz.  

- **Düzeltme betiği (isteğe bağlı)**: **komut dosyası Ekle**' yi seçin ve bir betik girin veya dosyaya gidin. Bu betik uyumlu olmayan ayar değerlerini düzeltmek için kullanılır. Windows PowerShell, VBScript veya Microsoft JScript betiklerini kullanabilirsiniz.  

- **Oturum açmış kullanıcı kimlik bilgilerini kullanarak betikleri çalıştırın**: Bu seçeneği etkinleştirirseniz, komut dosyası, oturum açmış kullanıcının kimlik bilgilerini kullanan istemci bilgisayarlarda çalışır.  

> [!Note]  
> Sürüm 1810 ' den başlayarak, Windows PowerShell 'i bulma veya düzeltme betiği olarak kullandığınızda Configuration Manager istemcisi PowerShell 'i `-NoProfile` parametresiyle çağırır. Bu seçenek PowerShell 'i profil olmadan başlatır. PowerShell profili, PowerShell başladığında çalışan bir betiktir. <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a>SQL sorgusu

- **SQL Server örneği**: SQL sorgusunun varsayılan örnek, tüm örnekler veya belirtilen veritabanı örneği adı üzerinde çalışmasını isteyip istemediğinizi seçin.  

    > [!NOTE]  
    > Örnek adı, SQL Sunucusu yerel örneğine karşılık gelmelidir. Kümelenmiş bir SQL sunucusu örneğine başvuru yapmak için, bir komut dosyası ayarı kullanmalısınız.  

- **Veritabanı**: SQL sorgusunu çalıştırmak istediğiniz Microsoft SQL Server veritabanının adını belirtin.  

- **Sütun**: genel koşulun uyumluluğunu değerlendirmek Için kullanılan Transact-SQL ifadesinin döndürdüğü sütun adını belirtin.  

- **Transact-SQL ekstresi**: genel koşul için kullanmak ISTEDIĞINIZ tam SQL sorgusunu belirtin. Mevcut bir SQL sorgusunu kullanmak için **Aç**' ı seçin.  

    > [!IMPORTANT]  
    > SQL sorgu ayarları, veritabanını değiştiren herhangi bir SQL komutunu desteklemez. Yalnızca veritabanındaki bilgileri okuyan SQL komutlarını kullanabilirsiniz.  


### <a name="wql-query"></a><a name="bkmk_wql"></a>WQL sorgusu

- **Ad alanı**: istemci bilgisayarlarda uyumluluk IÇIN değerlendirilen WMI ad alanını belirtin. Varsayılan değer: `root\cimv2`.  

- **Sınıf**: Yukarıdaki ad alanında hedef WMI sınıfını belirtin.  

- **Özellik**: Yukarıdaki SıNıFTA hedef WMI özelliğini belirtin.  

- **Wql sorgusu where yan tümcesi**: sonuçları azaltmak için uygun bir yan tümce belirtin. Örneğin, Win32_Service sınıfında yalnızca DHCP hizmetini sorgulamak için WHERE yan tümcesi olabilir `Name = 'DHCP' and StartMode = 'Auto'` .   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a>XPath sorgusu

- **Yol**: uyumluluğu değerlendirmek için kullanılan istemci bilgisayarlardaki. xml dosyasının yolunu belirtin. Configuration Manager, tüm Windows sistem ortam değişkenlerinin ve `%USERPROFILE%` yol adındaki Kullanıcı değişkeninin kullanımını destekler.  

- **XML dosyası adı**: YUKARıDAKI yolda XML sorgusunu içeren dosya adını belirtin.  

- **Alt klasörleri dahil et**: belirtilen yolun altındaki tüm alt klasörlerde arama yapmak için bu seçeneği etkinleştirin.  

- **Bu dosya 64 bitlik bir uygulamayla ilişkili**: `%Windir%\System32` `%Windir%\Syswow64` Windows 'un 64 bit sürümünü çalıştıran Configuration Manager istemcilerde 32 bit sistem dosyası konumuna ek olarak 64 bit sistem dosyası konumunu arayın.  

- **XPath sorgusu**: geçerli BIR tam XML yol dili (XPath) sorgusu belirtin.  

- **Ad alanları**: XPath sorgusu sırasında kullanılacak ad alanlarını ve önekleri belirler.  

Şifrelenmiş bir. xml dosyası bulmaya çalışırsanız, uyumluluk ayarları dosyayı bulur, ancak XPath sorgusu sonuç üretmez. Configuration Manager istemcisi bir hata oluşturmaz.  

XPath sorgusu geçerli değilse, bu ayar istemci bilgisayarlarında uyumsuz olarak değerlendirilir.  



##  <a name="configure-compliance-rules"></a>Uyumluluk kurallarını yapılandırma  

Uyumluluk kuralları, yapılandırma öğesinin uyumluluğunu tanımlayan koşulları belirtir. Bir ayar, uyumluluk bakımından değerlendirilmeden önce en az bir uyumluluk kuralına sahip olmalıdır. WMI, kayıt defteri ve betik ayarları uyumsuz olarak bulunan değerleri düzeltmenizi sağlar. Yeni kurallar oluşturabilir veya içindeki kuralları seçmek için herhangi bir yapılandırma öğesindeki mevcut ayarlara gidebilirsiniz.  


### <a name="to-create-a-compliance-rule"></a>Uyumluluk ilkesi oluşturmak için  

1. **Yapılandırma öğesi oluşturma Sihirbazı**' nın **Uyumluluk kuralları** sayfasında, **Yeni**' yi seçin.  

2. **Kural Oluştur** iletişim kutusunda, aşağıdaki bilgileri sağlayın:  

    - **Ad**: uyumluluk kuralı için bir ad girin.  

    - **Açıklama**: uyumluluk kuralı için bir açıklama girin.  

    - **Seçili ayar**: **Ayar seç** Iletişim kutusunu açmak için **Gözden** geçirme ' yi seçin. Kural tanımlamak istediğiniz ayarı seçin veya **yeni ayar**' ı seçin. İşiniz bittiğinde **Seç**' i seçin.  

        > [!Tip]  
        > Seçili olan ayar hakkındaki bilgileri görüntülemek için **Özellikler**' i seçin.  

    - **Kural türü**: kullanmak istediğiniz uyumluluk kuralının türünü seçin:  

        - **Değer**: yapılandırma öğesi tarafından döndürülen değeri belirttiğiniz değerle karşılaştıran bir kural oluşturun. Ek ayarlar hakkında daha fazla bilgi için bkz. [değer kuralları](#bkmk_value).  

        - **Varlıksal**: ayarı bir istemci cihazında var olup olmadığına veya bulunma sayısına bağlı olarak değerlendiren bir kural oluşturun. Ek ayarlar hakkında daha fazla bilgi için bkz. [varlıksal Rules](#bkmk_exist).  

3. **Kural oluştur** iletişim kutusunu kapatmak için **Tamam ' ı** seçin.  




### <a name="value-rules"></a><a name="bkmk_value"></a>Değer kuralları  

- **Özellik**: denetlenecek nesnenin özelliği, seçilen ayara bağlı olarak değişir. Kullanılabilir özellikler ayar türüne göre değişiklik gösterir. 

- **Ayar, aşağıdaki gibi uyumlu olmalıdır...**: kullanılabilir kurallar veya izinler ayar türüne göre değişiklik gösterir.

- **Desteklendiğinde uyumsuz kuralları düzelt**: uyumlu olmayan kuralları otomatik olarak düzeltmek için Configuration Manager için bu seçeneği belirleyin. Configuration Manager, bu eylemi aşağıdaki kural türleriyle destekler:  

    - **Kayıt defteri değeri**: uyumsuzsa, istemci kayıt defteri değerini ayarlar. Yoksa, istemci değeri oluşturur.  

    - **Betik**: istemci, ayarıyla belirttiğiniz düzeltme betiğini kullanır.  

    - **WQL sorgusu**  

    > [!IMPORTANT]  
    > Uyumsuz kuralları, yalnızca kural işleci **Eşittir** olarak ayarlandığında düzeltebilirsiniz.  

- **Bu ayar örneği bulunmazsa uyumsuzluğu bildir**: Bu ayar istemci bilgisayarlarda bulunmazsa, yapılandırma öğesi için uyumsuzluğu raporlamak üzere bu seçeneği etkinleştirin.  

- **Raporlar Için uyumsuzluk önem derecesi**: Bu uyumluluk kuralı başarısız olursa Configuration Manager raporlarında bildirilen önem derecesini belirtin. Aşağıdaki önem düzeyleri kullanılabilir:  
    - **Hiçbiri**  
    - **Bilgi**  
    - **Uyarı**  
    - **Kritik**  
    - **Kritik ve olayla**: Bu uyumluluk kuralında başarısız olan bilgisayarlar **kritik**hata önem derecesini raporlar. Bu önem düzeyi ayrıca uygulama olay günlüğünde bir Windows olayı olarak kaydedilir.  


### <a name="existential-rules"></a><a name="bkmk_exist"></a>Varlıksal kuralları 

> [!NOTE]  
> Gösterilen seçenekler, kural yapılandırmakta olduğunuz ayar türüne bağlı olarak değişiklik gösterebilir.  

- **Ayar istemci cihazlarda mevcut olmalıdır**  

- **Ayar istemci cihazlarda mevcut olmamalıdır**  

- **Ayarın tekrarlanma sayısı:**  

- **Raporlar Için uyumsuzluk önem derecesi**: Bu uyumluluk kuralı başarısız olursa Configuration Manager raporlarında bildirilen önem derecesini belirtin. Aşağıdaki önem düzeyleri kullanılabilir:  
    - **Hiçbiri**  
    - **Bilgi**  
    - **Uyarı**  
    - **Kritik**  
    - **Kritik ve olayla**: Bu uyumluluk kuralında başarısız olan bilgisayarlar **kritik**hata önem derecesini raporlar. Bu önem düzeyi ayrıca uygulama olay günlüğünde bir Windows olayı olarak kaydedilir.  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a>Yapılandırma öğesi değişikliklerini izle
<!--4261411-->
*(Sürüm 2002 ' de tanıtılmıştır)*

Configuration Manager sürüm 2002 ' den başlayarak, yapılandırma öğesi uyumluluk kurallarınızın **desteklenmesinden sonra düzeltme geçmişini izleyebilirsiniz** . Bu seçenek etkinleştirildiğinde, yapılandırma öğesi için istemcide gerçekleşen tüm düzeltme bir durum iletisi oluşturur. Geçmiş Configuration Manager veritabanında depolanır.

Ortak görünüm **v_CIRemediationHistory**kullanarak düzeltme geçmişini görüntülemek için özel raporlar oluşturun. `RemediationDate`Sütun, UTC olarak, istemcinin düzeltmeyi çalıştırdığı süredir. , `ResourceID` Cihazı tanımlar. **V_CIRemediationHistory** görünümü ile özel raporlar oluşturmak şunları yapmanıza yardımcı olur:

- Düzeltme betiklerinizde olası sorunları belirlemek
- Her değerlendirme döngüsünün sürekli olarak uyumsuz olduğu bir istemci gibi düzeltmelere yönelik eğilimleri bulun.

### <a name="enable-the-track-remediation-history-when-supported-option"></a>Desteklençalışırken düzeltme geçmişini Izle seçeneğini etkinleştirin

- Yeni yapılandırma öğeleri için, sihirbazın **Ayarlar** sayfasında yeni bir ayar oluşturduğunuzda **Uyumluluk kuralları** sekmesinde, **Desteklenne zaman düzeltme geçmişini izle** seçeneğini ekleyin.
- Mevcut yapılandırma öğeleri için yapılandırma öğesi **özelliklerindeki** **Uyumluluk kuralları** sekmesinde **Desteklenne zaman düzeltme geçmişini izle** seçeneğini ekleyin.
[![Sürüm 2002 ' de desteklenmekte olan düzeltme geçmişini izleme](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>Sonraki adımlar

[Yapılandırma taban çizgileri oluşturma](create-configuration-baselines.md)
