---
title: Genel koşullar oluşturma
titleSuffix: Configuration Manager
description: Bir uygulamanın istemci cihazlarına nasıl sağlandığını ve dağıtıldığını belirtmek için genel koşullar oluşturun.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ae27e50e5093d7443c35df33b1757caec6086627
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710289"
---
# <a name="how-to-create-global-conditions-in-configuration-manager"></a>Configuration Manager genel koşullar oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, genel koşullar, bir uygulamanın istemci cihazlarına nasıl sağlandığını ve dağıtıldığını belirtmek için kullanabileceğiniz iş veya teknik koşulları temsil eden kurallardır. Genel koşullara, Dağıtım Tür Oluşturma Sihirbazı'nın **Gereksinimler** sayfasından erişim sağlanır.  

> [!NOTE]  
>  Genel koşulları yalnızca oluşturuldukları siteden düzenleyebilirsiniz.  

 Configuration Manager genel koşullar oluşturmak için aşağıdaki yordamları kullanın.  

## <a name="provide-basic-information-about-the-global-condition"></a>Genel koşul hakkındaki temel bilgileri sağlama  
 Birkaç farklı genel koşul türü kullanılır. Farklı genel koşul türleriyle farklı seçenekler ilişkilidir. Belirli bir genel koşul türünü seçtiğinizde, Configuration Manager seçiminize uygulanan seçenekleri gösterir.  

1.  Configuration Manager konsolunda, **yazılım kitaplığı** > **uygulama yönetimi** > **genel koşullar**' ı seçin.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **genel koşul oluştur**' u seçin.  

4.  **Genel Koşul Oluştur** iletişim kutusunda, o genel koşul için bir ad ve isteğe bağlı bir açıklama sağlayın.  

5.  **Cihaz türü** aşağı açılan listesinde, genel koşulun bir **Windows** bilgisayar veya **Windows mobil** cihaz için olup olmadığını seçin.  

6.  **Koşul Türü** aşağı açılan listesinde aşağıdaki seçeneklerden birini seçin:  

    -   **Ayar** – Bu seçenek, istemci cihazlarında bir veya daha çok öğenin bulunup bulunmadığını kontrol eder. Örneğin, bir dosya, klasör veya kayıt defteri anahtarı değerinin bir istemci cihazında bulunup bulunmadığını kontrol edebilirsiniz.  

    -   **İfade** – Bu seçenek, koşulun istemci cihazlarda karşılanıp karşılanmadığı denetlemek için daha karmaşık kurallar ayarlamanıza olanak sağlar. Örneğin, bir bilgisayardaki fiziksel belleğin 2 GB ile 4 GB arasında olup olmadığını veya bir mobil cihazın dokunmatik ekran girişi kullanıp kullanmadığını kontrol edebilirsiniz.  

## <a name="set-up-rules-for-the-global-condition"></a>Genel koşul için kuralları ayarla  
 Genel koşul kurallarını tanımlama yordamı, bir ayarı veya bir ifadeyi yapılandırıp yapılandırmadığınıza bağlı olarak farklılık belirtir. Genel koşul için bir ayar veya bir ifade ayarlamak üzere buradaki ilgili yordamı kullanın.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Genel koşula yönelik bir ayar ayarlamak için  

1. **Koşul Türü** aşağı açılan listesinde **Ayar**'ı seçin.  

2. **Ayar türü** aşağı açılan listesinde gereksinimlerin kontrol edileceği koşul olarak kullanılacak öğeyi seçin. Aşağıdaki ayar türleri ve konfigürasyonlar kullanılabilir.  

   - **Active Directory sorgusu**  

     -   **LDAP öneki** - İstemci biglisayarlarındaki uygunluğu değerlendirmek için Active Directory Etki Alanı Hizmetleri'ne geçerli bir LDAP öneki belirleyin. **LDAP://** veya **GC://** kullanabilirsiniz.  

     -   **Ayırt edici ad (DN)** -istemci bilgisayarlarda uygunluk açısından değerlendirilecek Active Directory Domain Services nesnesinin ayırt edici adını belirtin.  

     -   **Arama süzgeci** - İstemci bilgisayarlarındaki uygunluğu değerlendirmek için Active Directory Etki Alanı Hizmetleri sorgusundan gelen sonuçları daraltmak için isteğe bağlı bir LDAP süzgeci belirleyin.  

     -   **Arama kapsamı** - Active Directory Etki Alanı Hizmetlerinde arama kapsamını belirleyin:  

         -   **Temel** -yalnızca belirtilen nesneyi sorgular.  

         -   **Tek düzey** -bu seçenek Configuration Manager bu sürümünde kullanılmaz.  

         -   **Alt ağaç** -belirtilen nesneyi ve dizin içindeki tam alt ağacını sorgular.  

     -   **Özellik** - İstemci bilgisayarlarındaki uygunluğu değerlendirmekte kullanılacak Active Directory Etki Alanı Hizmetlerinin özelliğini belirleyin.  

     -   **Sorgu** - **LDAP ön eki**, **ayırt edici ad (DN)**, belirtilmişse **arama filtresi** ve **özellik**içindeki girişlerden oluşturulan LDAP sorgusunu gösterir. Bu sorgu, istemci bilgisayarlarındaki uygunluğu değerlendirmekte kullanılacaktır.  

   - **Derleme**  

     -   **Derleme adı** - Arama yapılacak derleme nesnesinin adını belirler. Ad aynı türdeki diğer hiçbir derleme nesnesiyle aynı olamaz ve ad genel derleme önbelleğinde kayıtlı olmalıdır. Derleme adı en fazla 256 karakter olabilir.  

     > [!NOTE]  
     >  Bir derleme, uygulamalar arasında paylaştırılabilen bir kod parçasıdır. Derlemeler. dll veya. exe dosya adı uzantısına sahip olabilir. Genel Derleme Önbelleği, istemci bilgisayarlarında bulunan, tüm paylaşılan derlemelerin saklandığı, *%systemroot%\assembly* adlı bir klasördür.  

   - **Dosya sistemi**  

     - **Tür** – aşağı açılan listeden, bir **Dosya** veya **klasör**için arama yapmak isteyip istemediğinizi seçin.  

     - **Yol** - Belirlenen dosya veya klasörün istemci bilgisayarlardaki yolunu belirleyin. Sistem ortam değişkenlerini ve *%USERPROFILE%* ortam değişkenini yolda belirleyebilirsiniz.  

       > [!NOTE]  
       >  *%USERPROFILE%* ortam değişkenini **Yol** veya **Dosya ya da klasör adı** alanlarında kullanırsanız, istemci bilgisayardaki tüm kulalnıcı profillerinde arama yapılır. Bu durum, dosya veya klasörün birden çok örneğinin bulunmasıyla sonuçlanabilir.  

     - **Dosya veya klasör adı** - Arama yapılacak dosya veya klasör nesnesinin adını belirleyin. Sistem ortam değişkenlerini ve *%USERPROFILE%* ortam değişkenini dosya veya klasör adında belirleyebilirsiniz. * Ve? öğesini de kullanabilirsiniz. dosya adında joker karakterler.  

       > [!NOTE]  
       >  Bir dosya veya klasör adı belirler ve joker karakterleri kullanırsanız, bu durum yüksek sayıda sonuç ortaya çıkmasına neden olabilir. Bu durum Configuration Manager sonuçları bildirilse de istemci bilgisayarda yüksek kaynak kullanımına ve yüksek ağ trafiğine neden olabilir.  

     - **Alt klasörleri dahil et** – Ayrıca belirtilen yolun altındaki tüm alt klasörlerde arama yapmak istiyorsanız bu seçeneği etkinleştirin.  

     - **Bu dosya veya klasör 64 bitlik bir uygulamayla ilişkilendirildi** -Windows 'un 64 bit sürümünü çalıştıran Configuration Manager istemcilerinde, 64 bit sistem dosyası konumunun (*% windir%* \system32), 32-bit sistem dosyası konumuna (*%* windir% \Syswow64) ek olarak arama yapılıp yapılmayacağını seçin.  

       > [!NOTE]  
       >  Aynı 64-bit bilgisayarda 64-bit ve 32-bit sistem dosyası konumlarının her ikisinde de aynı dosya veya klasör varsa, genel koşul tarafından birden çok dosya bulunacaktır.  

       **Dosya sistemi** ayar türü **Yol** alanındaki ağ paylaşımına giden UNC yolunu belirtme özelliğini desteklemez.  

   - **IIS metatabanı**  

     -   **Metataban yolu** - IIS Metatabanı'na giden geçerli bir yol belirleyin.  

     -   **Özellik Kimliği** - IIS Metatabanı ayarının sayısal özelliğini belirleyin.  

   - **Kayıt defteri anahtarı**  

     -   **Hive** : aşağı açılan listeden, içinde arama yapmak istediğiniz kayıt defteri kovanını seçin.  

     -   **Anahtar** - Arama yapmak istediğini kayıt defteri anahtarı adını belirleyin. Kullanılan format *anahtar\alt anahtar*şeklinde olmalıdır.  

     -   **Bu kayıt defteri anahtarı bir 64-bit uygulamayla ilişkili** - Windows'ın 64-bit sürümünü çalıştıran istemcilerde 32-bit kayıt defteri anahtarlarının yanı sıra 64-bit kayıt defteri anahtarlarında da arama yapılıp yapılmayacağını belirler.  

         > [!NOTE]  
         >  Aynı 64-bit bilgisayarda 64-bit ve 32-bit kayıt defteri konumlarının her ikisinde de aynı kayıt defteri anahtarı varsa, genel koşul tarafından her iki kayıt defteri anahtarı da bulunacaktır.  

   - **Kayıt defteri değeri**  

     -   **Kovan** - Aşağı açılan liesteden içinde arama yapmak istediğiniz kayıt defteri kovanını seçin.  

     -   **Anahtar** - Arama yapmak istediğini kayıt defteri anahtarı adını belirleyin. Kullanılan format *anahtar\alt anahtar*şeklinde olmalıdır.  

     -   **Değer** – Belirtilen kayıt defteri anahtarı içinde bulunması gereken değeri belirleyin.  

     -   **Bu kayıt defteri anahtarı bir 64-bit uygulamayla ilişkili** - Windows'ın 64-bit sürümünü çalıştıran istemcilerde 32-bit kayıt defteri anahtarlarının yanı sıra 64-bit kayıt defteri anahtarlarında da arama yapılıp yapılmayacağını belirler.  

         > [!NOTE]  
         >  Aynı 64-bit bilgisayarda 64-bit ve 32-bit kayıt defteri konumlarının her ikisinde de aynı kayıt defteri anahtarı varsa, genel koşul tarafından her iki kayıt defteri anahtarı da bulunacaktır.  

   - **Komut Dosyası**  

     -   **Keşif betiği** – kullanılacak betiği girmek veya bu betiğe gitmek için **Ekle** ' yi seçin. Windows PowerShell, VBScript veya JScript betiklerini kullanabilirsiniz.  

     -   **Komut dosyalarını oturum açmış kullanıcı kimlik bilgilerini kullanarak Çalıştır** – bu seçeneği etkinleştirirseniz, komut dosyası, oturum açan kullanıcının kimlik bilgilerini kullanarak istemci bilgisayarlarda çalışır.  

         > [!NOTE]  
         >  Komut dosyası tarafından döndürülen değer, genel koşula uygunluğun değerlendirmesinde kullanılacaktır. Örneğin, VBScript kullandığınızda, genel koşula sonuç değişken değerini döndürmek için **WScript. Echo Result** komutunu kullanabilirsiniz.  
         >   
         >  Betiğiniz birden fazla değer döndürürse bu değerler tek bir satırda olmalı ve noktalı virgülle ayrılmalıdır. Her değer ayrı bir satırdaysa değerlendirme başarısız olur.  

   - **SQL sorgusu**  

     -   **SQL Sunucusu örneği** – SQL sorgusunun varsayılan örnek, tüm örnekler veya belirlenen veritabanı örnek adından hangisinin üzerinde çalıştırılacağını seçin.  

         > [!NOTE]  
         >  Örnek adı, SQL Sunucusu yerel örneğine karşılık gelmelidir. Kümelenmiş bir SQL sunucusu örneğine başvuru yapmak için, bir komut dosyası ayarı kullanmalısınız.  

     -   **Veritabanı** - SQL sorgusunun çalıştırılacağı Microsoft SQL Sunucusu veritabanının adını belirleyin.  

     -   **Sütun** - Genel koşulun uygunluğunu değerlendirmek amacıyla kullanılacak, Transact-SQL ifadesinin döndürdüğü sütun adını belirleyin.  

     -   **Transact-SQL ifadesi** – Genel koşul için kullanılacak tam SQL sorgusunu belirleyin. Ayrıca, var olan bir SQL sorgusunu açmak için **Aç** ' ı da seçebilirsiniz.  

   - **WQL sorgusu**  

     -   **Ad Alanı** - İstemci bilgisayarlarında uygunluk açısından değerlendirilecek bir WQL sorgusu oluşturmakta kullanılacak WMI ad alanını belirleyin. Varsayılan değer, Root\cimv2'dir.  

     -   **Sınıf** - İstemci bilgisayarlarında uygunluk açısından değerlendirilecek bir WQL sorgusu oluşturmakta kullanılacak WMI sınıfını belirler.  

     -   **Özellik** - İstemci bilgisayarlarında uygunluk açısından değerlendirilecek bir WQL sorgusu oluşturmakta kullanılacak WMI özelliğini belirler.  

     -   **WQL sorgusu WHERE yan tümcesi** - **WQL sorgusu WHERE yan tümcesi** öğesini, istemci bilgisayarlarda belirlenen ad alanı, sınıf ve özelliğe uygulanacak WHERE yan tümcesini belirlemek için kullanabilirsiniz.  

   - **XPath sorgusu**  

     -   **Yol** - İstemci bilgisayarlardaki uyumluluğu değerlendirmek üzere kullanılacak XML dosyasının yolunu belirtin. Configuration Manager, tüm Windows sistem ortamı değişkenlerinin ve yol adında *% USERPROFILE%* Kullanıcı değişkeninin kullanımını destekler.  

     -   **XML dosya adı** -istemci bilgisayarlarındaki uyumluluğu değerlendirmek IÇIN kullanılacak XML sorgusunu içeren dosya adını belirtin.  

     -   **Alt klasörleri dahil et** - Belirlenen yolın altındaki tüm alt klasörlerde arama yapmak istiyorsanız, bu seçeneği etkinleştirir.  

     -   **Bu dosya, 64 bitlik bir uygulamayla ilişkili** -Windows 'un 64 bit sürümünü çalıştıran Configuration Manager istemcilerinde, 64 bit sistem dosyası konumunun (*% windir%* \system32) Ayrıca, 32-bit sistem dosyası konumuna (*%* windir% \Syswow64) ek olarak arama yapılıp yapılmayacağını seçin.  

     -   **XPath sorgusu** - İstemci bilgisayarlarda uygunluğu değerlendirmekte kullanıacak geçerli bir tam XML yol dili (XPath) belirleyin.  

     -   **Ad Alanları** - XPath sorgusu sırasında kullanılacak ad alanlarını ve önekleri belirlemek için **XML Ad Alanları** iletişim kutusunu açar.  

3. Gereksinimleri kontrol etmekte kullanılmadan önce koşul tarfından verilerin döndürüleceği formatı **Veri türü** aşağı açılan listesinde seçin.  

   > [!NOTE]  
   >  **Veri türü** aşağı açılan listesi tüm ayar türleri için gösterilmez.  

4. **Ayar türü** aşağı açılan listesinin altında bu ayarla ilgili daha fazla ayrıntı ayarlayın. Ayarlayabileceğiniz öğeler, seçmiş olduğunuz ayar türüne bağlı olarak değişir.  

5. Kuralı kaydetmek ve **genel koşul oluştur** iletişim kutusunu kapatmak için **Tamam** ' ı seçin.  

### <a name="set-up-an-expression-for-the-global-condition"></a>Genel koşul için bir ifade ayarlayın  

1.  **Koşul Türü** aşağı açılan listesinde **İfade**'yi seçin.  

2.  **Yan tümce Ekle iletişim kutusunu** açmak Için **yan tümce Ekle** ' yi seçin.  

3.  **Kategori seç** aşağı açılan listesinden bu ifadenin bir cihaz için veya bir kullanıcı olup olmadığını seçin. Farklı şekilde, daha önce yapılandırılmış bir genel koşulu kullanmak için **Özel** 'i seçin.  

4.  **Bir koşul seç** aşağı açılan listesinde, kural gereksinimlerini kullanıcının veya cihazın karşılayıp karşılamadığını değerlendirmek için kullanılacak koşulu seçin. Bu listenin içeriği, seçilen kategoriye göre değişir.  

5.  **İşleç seç** aşağı açılan listesinden, seçilen koşulu, kural gereksinimlerini kullanıcının veya cihazın mı karşılayıp karşılamadığını değerlendirmek için belirlenen değerle karşılaştırmak üzere kullanılacak işleci seçin. Kullanılabilir operatörler, seçilen koşula göre değişir.  

6.  **Değer** alanında, kural gereksinimlerini kullanıcını veya cihazın karşılayıp karşılamadığını değerlendirmek için seçilen koşul ve işleçle birlikte kullanılacak değerleri belirleyin. Kullanılabilir değerler, seçilen koşula ve seçilen operatöre göre değişir.  

7.  İfadeyi kaydetmek ve **yan tümce Ekle** iletişim kutusunu kapatmak için **Tamam** ' ı seçin.  

8.  Genel koşula yan tümceler eklemeyi bitirdiğinizde, genel koşul **Oluştur** iletişim kutusunu kapatmak ve genel koşulu kaydetmek için **Tamam** ' ı seçin.  
