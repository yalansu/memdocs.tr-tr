---
title: Mac istemcilerinin bakımını yapma
titleSuffix: Configuration Manager
description: Configuration Manager Mac istemcileri için bakım görevleri.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 520315c4bb740f23a9534e532f75c3bd3ee66a2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710653"
---
# <a name="maintain-mac-clients"></a>Mac istemcilerinin bakımını yapma
*Uygulama hedefi: Configuration Manager (geçerli dal)*

Mac istemcilerini kaldırmaya ve sertifikalarını yenilemeye yönelik yordamlar aşağıda verilmiştir.

##  <a name="uninstalling-the-mac-client"></a>Uninstalling the Mac client  

1.  Bir Mac bilgisayarda, bir Terminal penceresi açın ve **macclient. dmg**' yi içeren klasöre gidin.  

2.  Araçlar klasörüne gidin ve aşağıdaki komut satırını girin:  

     `./CMUninstall -c`

    > [!NOTE]  
    >  **-C** özelliği istemcisini kaldırma işlemini istemci kilitlenme günlüklerini ve günlük dosyalarını da kaldıracak şekilde yönlendirir. Daha sonra istemciyi yeniden yüklerseniz karışıklık oluşmasını önlemek için bunu yapmanızı öneririz.  

3.  Gerekirse, Configuration Manager tarafından kullanılan istemci kimlik doğrulama sertifikasını el ile kaldırın veya iptal edin. CMUnistall bu sertifikayı kaldırmaz veya iptal etmez.  

##  <a name="renewing-the-mac-client-certificate"></a>Mac İstemci Sertifikasını Yenileme  
 Mac istemci sertifikasını yenilemek için aşağıdaki yöntemlerden birini kullanın:  

-   [Sertifika Yenileme Sihirbazı](#renew-certificate-wizard)  

-   [Sertifikayı el ile Yenile](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Sertifika Yenileme Sihirbazı  

1. Sertifikayı Yenile sihirbazının ne zaman açıldığını kontrol eden ccmclient. plist dosyasında *dizeler* olarak aşağıdaki değerleri yapılandırın:  

   - **RenewalPeriod1** -kullanıcıların sertifikayı yenileyebileceği ilk yenileme süresini saniye cinsinden belirtir. Varsayılan değer 3.888.000 saniyedir (45 gün). Süre varsayılan değere döndürülerek 300 'den küçük bir değer yapılandırmayın. 

   - **RenewalPeriod2** -kullanıcıların sertifikayı yenileyebileceği ikinci yenileme süresini saniye cinsinden belirtir. Varsayılan değer 259.200 saniyedir (3 gün). Bu değer yapılandırılırsa ve 300 saniyeye eşitse ve **RenewalPeriod1**değerinden büyük veya buna eşitse, değer kullanılacaktır. **RenewalPeriod1** 3 günden büyükse, **RenewalPeriod2**için 3 günlük değer kullanılır.  **RenewalPeriod1** 3 günden küçükse, **RenewalPeriod2** , **RenewalPeriod1**ile aynı değere ayarlanır.  

   - **RenewalReminderInterval1** -ilk yenileme döneminde Sertifikayı Yenile sihirbazının kullanıcılara gösterileceği sıklığı saniye cinsinden belirtir. Varsayılan değer 86.400 saniyedir (1 gün). **RenewalReminderInterval1** değeri 300 saniyeden büyükse ve **RenewalPeriod1**için yapılandırılan değerden azsa yapılandırılan değer kullanılır. Aksi takdirde 1 günlük varsayılan değer kullanılır.  

   - **RenewalReminderInterval2 büyükse** -ikinci yenileme döneminde Sertifikayı Yenile sihirbazının kullanıcılara gösterileceği sıklığı saniye cinsinden belirtir. Varsayılan değer 28.800 saniyedir (8 saat). **RenewalReminderInterval2** değeri 300 saniyeden büyükse, **RenewalReminderInterval1** değerine eşit veya daha küçükse ve **RenewalPeriod2**değerine eşit veya daha küçükse yapılandırılan değer kullanılır. Aksi takdirde 8 saatlik değer kullanılır.  

     **Örnek:** Değerler varsayılan olarak bırakıldığında, sertifikanın süresi dolmadan 45 gün önce, sihirbaz her 24 saatte bir açılır.  Sertifikanın süresi dolmadan 3 gün önce, sihirbaz her 8 saatte bir açılır.  

     **Örnek:** Birinci yenileme süresini 20 güne ayarlamak için aşağıdaki komut satırını veya bir betik kullanın.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. Sertifikayı Yenile Sihirbazı açıldığında, **Kullanıcı adı** ve **sunucu adı** alanları genellikle önceden doldurulmuş olur ve Kullanıcı sertifikayı yenilemek için yalnızca bir parola girebilir.  

   > [!NOTE]  
   >  Sihirbaz açılmazsa veya sihirbazı yanlışlıkla kapatırsanız **Configuration Manager** tercih sayfasından **Yenile** öğesini tıklatarak sihirbazı açın.  

###  <a name="renew-certificate-manually"></a>Sertifikayı el ile Yenile  
 Mac istemci sertifikasının geçerlilik süresi, genellikle 1 yıldır. Configuration Manager, kayıt sırasında istek yaptığı Kullanıcı sertifikasını otomatik olarak yenilemez, bu nedenle sertifikayı el ile yenilemek için aşağıdaki yordamı kullanmanız gerekir.  

> [!IMPORTANT]  
>  Sertifikanın süresi dolarsa Mac istemcisini kaldırmanız, yeniden yüklemeniz ve ardından yeniden kaydetmeniz gerekir.  

 Bu yordam aynı Mac bilgisayar için yeni bir sertifika istemek üzere gerekli olan SMSID'yi kaldırır. İstemci SMSıD 'sini kaldırdığınızda ve değiştirdiğinizde, istemciyi Configuration Manager konsolundan sildikten sonra envanter gibi depolanmış tüm istemci geçmişi silinir.  

1.  Kullanıcı sertifikalarını yenilemesi gereken Mac bilgisayarlar için bir cihaz koleksiyonu oluşturun ve doldurun.  

    > [!WARNING]  
    >  Configuration Manager, Mac bilgisayarlar için kaydettiği sertifikanın geçerlilik süresini izlemez. Bu koleksiyona eklenecek Mac bilgisayarları tanımlamak için bunu Configuration Manager bağımsız olarak izlemeniz gerekir.  

2.  **Varlıklar ve Uyum** çalışma alanında **Yapılandırma Öğesi Oluştur Sihirbazı**'nı başlatın.  

3.  **Genel** sayfasında aşağıdaki bilgileri belirtin:  

    -   **Ad:Mac için SMSID'yi Kaldırma**  

    -   **Tür:Mac OS X**  

4.  **Desteklenen platformlar** sayfasında, tüm Mac OS X sürümlerinin seçildiğinden emin olun.  

5.  **Ayarlar** sayfasında, **Yeni** ' yi seçin ve ardından **ayar oluştur** iletişim kutusunda aşağıdaki bilgileri belirtin:  

    -   **Ad:Mac için SMSID'yi Kaldırma**  

    -   **Ayar türü:Betik**  

    -   **Veri türü:Dize**  

6.  **Bulma komut dosyası**Için **ayar oluştur** iletişim kutusunda, yapılandırılmış bir SMSID ile Mac bilgisayarlarını bulan bir komut dosyasını belirtmek için **komut dosyası Ekle** ' yi seçin.  

7.  **Bulma Komut Dosyasını Düzenle** iletişim kutusunda, aşağıdaki Kabuk Betiği'ni girin:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  **Bulma betiğini Düzenle** iletişim kutusunu kapatmak için **Tamam ' ı** seçin.  

9. **Ayar oluştur** iletişim kutusunda, **Düzeltme betiği (isteğe bağlı)** için, Mac bilgisayarlarında bulunduğunda SMSID 'yi kaldıran bir komut dosyasını belirtmek için **komut dosyası Ekle** ' yi seçin.  

10. **Düzeltme Komut Dosyası Oluştur** iletişim kutusunda, aşağıdaki Kabuk Betiği'ni girin:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. **Düzeltme betiği oluştur** iletişim kutusunu kapatmak için **Tamam ' ı** seçin.  

12. Sihirbazın **Uyumluluk Kuralları** sayfasında, **Yeni**'yi tıklatın ve daha sonra **Ayar Oluştur** iletişim kutusunda aşağıdaki bilgileri belirtin:  

    -   **Ad:Mac için SMSID'yi Kaldırma**  

    -   **Seçilen ayar:** **Araştır** ' ı seçin ve daha önce belirlediğiniz bulma betiğini seçin.  

    -   **Aşağıdaki değerler** alanında, **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**girin.  

    -   **Bu ayar uyumsuz olduğunda belirtilen düzeltme komut dosyasını çalıştır**seçeneğini etkinleştirin.  

13. Yapılandırma Öğesi Oluştur Sihirbazı'nı Tamamlayın  

14. Yeni oluşturduğunuz yapılandırma öğesini içeren bir yapılandırma temeli oluşturun ve bunu adım 1 ' de oluşturduğunuz cihaz koleksiyonuna dağıtın.  

     Yapılandırma temellerini oluşturma ve dağıtma hakkında daha fazla bilgi için bkz. [yapılandırma temelleri oluşturma](../../../compliance/deploy-use/create-configuration-baselines.md) ve [yapılandırma temellerini dağıtma](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. SMSID'si kaldırılmış Mac bilgisayarlarda aşağıdaki komutu çalıştırarak yeni bir sertifika yükleyin:  

    ``` Shell
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Sorulduğunda süper kullanıcı hesabı parolasını belirterek komutu çalıştırın ve ardından Active Directory kullanıcı hesabı parolasını girin.  

16. Kayıtlı sertifikayı Configuration Manager sınırlandırmak için Mac bilgisayarda bir Terminal penceresi açın ve aşağıdaki değişiklikleri yapın:  

    a.  Komutu girin`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`

    b.  **Anahtarlık erişimi** iletişim kutusunda, **anahtarlıklar** bölümünde **sistem**' i seçin ve sonra **Kategori** bölümünde **anahtarlar**' ı seçin.  

    c.  İstemci sertifikalarını görüntülemek için anahtarları genişletin. Yeni yüklediğiniz özel anahtarı içeren sertifikayı tanımladığınızda, anahtarı çift tıklatın.  

    d.  **Access Control** sekmesinde, **erişime Izin vermeden önce Onayla**' yı seçin.  

    e.  **/Library/Application Support desteği/Microsoft/CCM**'ye gidin, **ccmclient**' ı seçin ve ardından **Ekle**' yi seçin.  

    f.  **Değişiklikleri Kaydet** ' i seçin ve **Anahtarlık erişimi** iletişim kutusunu kapatın.  

17. Mac bilgisayarı yeniden başlatın.  

