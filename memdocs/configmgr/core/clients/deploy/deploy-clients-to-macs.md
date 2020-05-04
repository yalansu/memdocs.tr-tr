---
title: Mac istemcilerini dağıtma
titleSuffix: Configuration Manager
description: Configuration Manager ' de Mac bilgisayarlara istemci dağıtmayı öğrenin.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713446"
---
# <a name="how-to-deploy-clients-to-macs"></a>Mac bilgisayarlara istemci dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Mac bilgisayarlarda Configuration Manager istemcisinin nasıl dağıtılacağı ve bakımını yapılacağı açıklanır. İstemcileri Mac bilgisayarlara dağıtmadan önce yapılandırmanız gerekenler hakkında bilgi edinmek için bkz. Mac ['e istemci yazılımı dağıtmaya hazırlanma](prepare-to-deploy-mac-clients.md).

Mac bilgisayarlar için yeni bir istemci yüklediğinizde, Configuration Manager konsolundaki yeni istemci bilgilerini yansıtmak için Configuration Manager güncelleştirmelerini de yüklemelisiniz.

Bu yordamlarda, istemci sertifikalarını yüklemek için iki seçeneğiniz vardır. Mac ['e istemci yazılımı dağıtmaya hazırlanma](prepare-to-deploy-mac-clients.md#certificate-requirements)bölümünde Mac için istemci sertifikaları hakkında daha fazla bilgi edinin.  

- [CMEnroll aracını](#bkmk_enroll)kullanarak Configuration Manager kaydını kullanın. Kayıt işlemi otomatik sertifika yenilemeyi desteklemiyor. Yüklenen sertifikanın süresi dolmadan önce Mac bilgisayarını yeniden kaydedin.    

- [Configuration Manager bağımsız bir sertifika isteği ve yükleme yöntemi kullanın](#bkmk_external).  

> [!IMPORTANT]  
> İstemciyi macOS Sierra çalıştıran cihazlara dağıtmak için, yönetim noktası sertifikasının **konu adını** doğru şekilde yapılandırın. Örneğin, yönetim noktası sunucusunun FQDN 'sini kullanın.



## <a name="configure-client-settings"></a>İstemci ayarlarını yapılandırma  

Mac bilgisayarlar için kaydı yapılandırmak üzere [varsayılan istemci ayarlarını](about-client-settings.md) kullanın. Özel istemci ayarlarını kullanamazsınız. Sertifikayı istemek ve yüklemek için, Mac için Configuration Manager istemcisi varsayılan istemci ayarlarını gerektirir.  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Istemci ayarları** düğümünü seçin ve **varsayılan istemci ayarları**' nı seçin.  

2. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

3. **Kayıt** bölümünü seçin ve ardından aşağıdaki ayarları yapılandırın:  

    1. **Kullanıcıların mobil cihazları ve Mac bilgisayarları kaydetmesine Izin ver**: **Evet**  

    2. **Kayıt profili:** **Profili ayarla**' yı seçin.  

4. **Mobil cihaz kayıt profili** Iletişim kutusunda **Oluştur**' u seçin.  

5. **Kayıt profili oluştur** iletişim kutusunda, bu kayıt profili için bir ad girin. Ardından **Yönetim sitesi kodunu**yapılandırın. Bu Mac bilgisayarlarının yönetim noktalarını içeren Configuration Manager birincil sitesini seçin.  

    > [!NOTE]  
    >  Siteyi seçemiyorum için sitede en az bir yönetim noktasını mobil cihazları destekleyecek şekilde yapılandırmadığınızdan emin olun.  

6. **Ekle**' yi seçin.  

7. **Mobil cihazlar Için sertifika yetkilisi Ekle** penceresinde, Mac bilgisayarlara sertifika veren sertifika yetkilisi sunucusunu seçin.  

8. **Kayıt profili oluştur** iletişim kutusunda, daha önce oluşturduğunuz Mac bilgisayar sertifikası şablonunu seçin.  

9. **Tamam** ' ı seçerek **kayıt profili** Iletişim kutusunu ve ardından **varsayılan istemci ayarları** iletişim kutusunu kapatın.  

    > [!TIP]  
    > İstemci ilkesi aralığını değiştirmek istiyorsanız **istemci** ilkesi istemci ayar grubundaki **istemci ilkesi yoklama aralığı** ' nı kullanın.  

Cihazların istemci ilkesini bir sonraki indirilişinde Configuration Manager, tüm kullanıcılar için bu ayarları uygular. Tek bir istemci için ilke almayı başlatmak için bkz. [Configuration Manager istemcisi için ilke almayı başlatma](../manage/manage-clients.md#BKMK_PolicyRetrieval).  

Kayıt istemci ayarlarına ek olarak aşağıdaki istemci aygıt ayarlarını yapılandırdığınızdan emin olun:  

- **Donanım envanteri**: Mac ve Windows istemci bilgisayarlarından donanım envanteri toplamak istiyorsanız bu özelliği etkinleştirin ve yapılandırın. Daha fazla bilgi için bkz. [donanım envanterini genişletme](../manage/inventory/extend-hardware-inventory.md).  

- **Uyumluluk ayarları**: Mac ve Windows istemci bilgisayarlarındaki ayarları değerlendirmek ve düzeltmek istiyorsanız bu özelliği etkinleştirin ve yapılandırın. Daha fazla bilgi için bkz. [Uyumluluk ayarlarını planlayın ve yapılandırın](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](configure-client-settings.md).  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a>MacOS istemcisini indirin

1. MacOS istemci dosyası paketini indirin, [Microsoft uç noktası Configuration Manager-macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850). **ConfigmgrMacClient. msi** dosyasını Windows çalıştıran bir bilgisayara kaydedin. Bu dosya Configuration Manager yükleme medyasında yok.  

2. Yükleyiciyi Windows bilgisayarda çalıştırın. **Macclient. dmg**Mac istemci paketini yerel diskteki bir klasöre ayıklayın. Varsayılan yol `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`.  

3. **Macclient. dmg** dosyasını Mac bilgisayarındaki bir klasöre kopyalayın.  

4. Mac bilgisayarda, dosyaları yerel diskteki bir klasöre ayıklamak için **macclient. dmg** komutunu çalıştırın.  

5. Klasöründe, aşağıdaki dosyaları içerdiğinden emin olun: 

    - **CCMSetup**: **CMClient. pkg** kullanarak Mac bilgisayarlarınıza Configuration Manager istemcisini yükleme  

    - **CMDiagnostics**: Mac bilgisayarlarınızda Configuration Manager istemcisiyle ilgili tanılama bilgilerini toplar  

    - **CMUninstall**: istemciyi Mac bilgisayarlarınızdan kaldırır  

    - **CMAppUtil**: Apple uygulama paketlerini Configuration Manager uygulaması olarak dağıtabileceğiniz bir biçime dönüştürür  

    - **CMEnroll**: Configuration Manager istemcisini yükleyebilmek Için bir Mac bilgisayara istemci sertifikası ister ve yükler  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a>Mac istemcisini kaydetme  

Tek tek istemcileri [Mac bilgisayar kaydetme Sihirbazı](#enroll-the-client-with-the-mac-computer-enrollment-wizard)ile kaydedin.

Birçok istemci için kaydı otomatik hale getirmek amacıyla [CMEnroll aracını](#client-and-certificate-automation-with-cmenroll)kullanın.   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>İstemciyi Mac bilgisayar kaydetme Sihirbazı 'na kaydetme  

1. İstemcisini yükledikten sonra, bilgisayar kayıt Sihirbazı açılır. Sihirbazı el ile başlatmak için **Configuration Manager** tercih sayfasından **Kaydet** ' i seçin.  

2. Sihirbazın ikinci sayfasında, aşağıdaki bilgileri sağlayın:  

   - **Kullanıcı adı**: Kullanıcı adı aşağıdaki biçimlerde olabilir:  

     - `domain\name`. Örneğin, `contoso\mnorth`  

     - `user@domain`. Örneğin, `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  **Kullanıcı adı** alanını doldurmak için bir e-posta adresi kullandığınızda, Configuration Manager **sunucu adı** alanını otomatik olarak doldurur. Kayıt proxy noktası sunucusunun varsayılan adını ve e-posta adresinin etki alanı adını kullanır. Bu adlar, kayıt proxy noktası sunucusunun adı ile eşleşmiyorsa kayıt sırasında **sunucu adını** düzeltir.  

       Kullanıcı adı ve karşılık gelen parola, Mac istemci sertifikası şablonunda **okuma** ve **kaydetme** izinlerine sahip bir Active Directory kullanıcı hesabıyla eşleşmelidir.  

   - **Sunucu adı**: kayıt proxy noktası sunucusunun adı.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>CMEnroll ile istemci ve sertifika Otomasyonu  

Bu yordamı, istemci yükleme otomasyonu ve CMEnroll aracı ile istemci sertifikaları isteme ve kaydetme amacıyla kullanın. Aracı çalıştırmak için bir Active Directory Kullanıcı hesabınızın olması gerekir.

1. Mac bilgisayarda, **macclient. dmg** dosyasının içeriğini ayıkladığınız klasöre gidin.  

2. Aşağıdaki komutu girin:`sudo ./ccmsetup`  

3. **Yükleme tamamlandı** iletisini görene kadar bekleyin. Yükleyici şimdi yeniden başlatmanız gerektiğini belirten bir ileti görüntülüyor olsa da, yeniden başlatmayın ve sonraki adıma geçin.  

4. Mac bilgisayardaki **Araçlar** klasöründen aşağıdaki komutu yazın:`sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    İstemci yüklendikten sonra Mac Bilgisayar Kaydetme sihirbazı açılarak Mac bilgisayarı kaydetmenize yardımcı olur. Daha fazla bilgi için bkz. [Mac bilgisayar kaydetme Sihirbazı 'nı kullanarak Istemciyi kaydetme](#bkmk_enroll).  

     Örnek: kayıt proxy noktası sunucusu **Server02.contoso.com**olarak adlandırılmışsa ve Mac istemci sertifikası şablonu için **contoso\mkuzey** izinleri verirseniz, aşağıdaki komutu yazın:`sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Kullanıcı adı aşağıdaki karakterlerden herhangi birini içeriyorsa, kayıt başarısız olur: `<>"+=,`. Bu karakterleri içermeyen bir Kullanıcı adı ile bant dışı bir sertifika kullanın.  
    >  
    > Daha sorunsuz bir kullanıcı deneyimi için yükleme adımlarını izleyin. Kullanıcıların yalnızca Kullanıcı adını ve parolasını sağlaması gerekir.  

5. Active Directory Kullanıcı hesabının parolasını yazın. Bu komutu girdiğinizde, iki parola istenir. İlk parola, süper kullanıcı hesabının komutu çalıştırması içindir. İkinci uyarı ise Active Directory kullanıcı hesabı içindir. Uyarılar aynı görünür, bu yüzden parolaları doğru sırayla belirttiğinizden emin olun.  

6. **Başarıyla kaydedildi** iletisini görene kadar bekleyin.  

7. Kayıtlı sertifikayı Configuration Manager sınırlandırmak için Mac bilgisayarda bir Terminal penceresi açın ve aşağıdaki değişiklikleri yapın:  

    1. Komutu girin`sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. **Anahtarlık erişimi** penceresinde, **anahtar zincirleri** bölümünde **sistem**' i seçin. Sonra **Kategori** bölümünde **anahtarlar**' ı seçin.  

    3. İstemci sertifikalarını görüntülemek için anahtarları genişletin. Yüklediğiniz bir özel anahtara sahip sertifikayı bulun ve anahtarı açın.  

    4. **Access Control** sekmesinde, **erişime Izin vermeden önce Onayla**' yı seçin.  

    5. **/Library/Application Support desteği/Microsoft/CCM**'ye gidin, **ccmclient**' ı seçin ve ardından **Ekle**' yi seçin.  

    6. **Değişiklikleri Kaydet** ' i seçin ve **Anahtarlık erişimi** iletişim kutusunu kapatın.  

8. Mac bilgisayarı yeniden başlatın.  

İstemci yüklemesinin başarılı olduğunu doğrulamak için, Mac bilgisayardaki **Sistem Tercihleri** ' nde **Configuration Manager** öğesini açın. Ayrıca, Configuration Manager konsolundaki **Tüm sistemler** koleksiyonunu güncelleştirin ve görüntüleyin. Mac bilgisayarın bu koleksiyonda yönetilen istemci olarak göründüğünü onaylayın.  

> [!TIP]  
> Mac istemcisinde sorun gidermeye yardımcı olmak için Mac istemci paketine dahil edilen **CMDiagnostics** aracını kullanın. Aşağıdaki tanılama bilgilerini toplamak için kullanın:  
>   
> - Çalışan işlemlerin bir listesi  
> - Mac OS X işletim sistemi sürümü  
> - **CCM\*. Crash** ve **sistem tercihi. kilitlenme**dahil Configuration Manager istemcisiyle ilgili kilitlenme raporları Mac OS X.  
> - Configuration Manager istemci yüklemesi tarafından oluşturulan ürün reçetesi (BOM) dosyası ve özellik listesi (. plist) dosyası.  
> - **/Library/Application Support destek/Microsoft/CCM/Logs**klasörünün içeriği.  
>   
> CmDiagnostics tarafından toplanan bilgiler bilgisayarın masaüstüne kaydedilen ve adı verilen bir zip dosyasına eklenir`cmdiag-<hostname>-<datetime>.zip`



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a>Configuration Manager harici sertifikaları yönetme

Configuration Manager bağımsız olarak bir sertifika isteği ve yükleme yöntemi kullanabilirsiniz. Aynı genel işlemi kullanın, ancak aşağıdaki ek adımları ekleyin: 

- Configuration Manager istemcisini yüklediğinizde, **MP** ve **SubjectName** komut satırı seçeneklerini kullanın. Şu komutu girin: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. Sertifika konu adı büyük/küçük harfe duyarlıdır, bu nedenle tam olarak sertifika ayrıntılarında göründüğü şekilde yazın.  

     Örnek: yönetim noktasının İnternet FQDN 'si **server03.contoso.com**' dir. Mac istemci sertifikası, sertifika konusunun ortak adı olarak **MAC12.contoso.com** FQDN 'sine sahiptir. Aşağıdaki komutu kullanın:`sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Aynı konu değerini içeren birden fazla sertifikanız varsa, Configuration Manager istemcisi için kullanılacak sertifika seri numarasını belirtin. Şu komutu kullanın: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Örneğin, `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Mac istemci sertifikasını yenileme  

Bu yordam SMSıD 'yi kaldırır. Mac için Configuration Manager istemcisi yeni veya yenilenen bir sertifikayı kullanmak için yeni bir KIMLIK gerektirir.  

> [!IMPORTANT]  
> İstemci SMSıD 'sini değiştirdikten sonra, Configuration Manager konsolundaki eski kaynağı sildiğinizde, depolanan istemci geçmişini de silersiniz. Örneğin, bu istemci için donanım envanteri geçmişi.  


1. Bilgisayar sertifikalarını yenilemesi gereken Mac bilgisayarlar için bir cihaz koleksiyonu oluşturun ve doldurun.  

2. **Varlıklar ve Uyum** çalışma alanında **Yapılandırma Öğesi Oluştur Sihirbazı**'nı başlatın.  

3. Sihirbazın **Genel** sayfasında aşağıdaki bilgileri belirtin:  

    - **Ad**: **Mac için SMSID 'yi kaldırma**  

    - **Tür**: **Mac OS X**  

4. **Desteklenen platformlar** sayfasında, tüm Mac OS X sürümlerini seçin.  

5. **Ayarlar** sayfasında **Yeni**’yi seçin. **Ayar oluştur** penceresinde, aşağıdaki bilgileri belirtin:  

    - **Ad**: **Mac için SMSID 'yi kaldırma**  

    - **Ayar türü**: **betik**  

    - **Veri türü**: **dize**  

6. **Ayar oluştur** penceresinde, **Bulma betiği**için **komut dosyası Ekle**' yi seçin. Bu eylem, SMSıD ile yapılandırılmış Mac bilgisayarlarının keşfedilmesine yönelik bir komut dosyası belirtir.  

7. **Bulma betiğini Düzenle** penceresinde, aşağıdaki kabuk betiğini girin:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. **Bulma betiğini Düzenle** penceresini kapatmak için **Tamam ' ı** seçin.  

9. **Ayar oluştur** penceresinde, **Düzeltme betiği (isteğe bağlı)** için **komut dosyası Ekle**' yi seçin. Bu eylem, Mac bilgisayarlarında bulunduğunda SMSıD 'yi kaldırmak için bir komut dosyası belirtir.  

10. **Düzeltme betiği oluştur** penceresinde, aşağıdaki kabuk betiğini girin:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. **Düzeltme betiği oluştur** penceresini kapatmak için **Tamam ' ı** seçin.  

12. **Uyumluluk kuralları** sayfasında, **Yeni**' yi seçin. Sonra **kural oluştur** penceresinde, aşağıdaki bilgileri belirtin:  

    - **Ad**: **Mac için SMSID 'yi kaldırma**  

    - **Seçilen ayar**: **Araştır** ' ı seçin ve daha önce belirlediğiniz bulma betiğini seçin.  

    - **Aşağıdaki değerler** alanında: **(com. Microsoft. CCMCLIENT, SMSID) etki alanı/varsayılan çifti yok**.  

    - **Bu ayar uyumsuz olduğunda belirtilen düzeltme betiğini çalıştırma**seçeneğini etkinleştirin.  

13. Sihirbazı tamamlayın.  

14. Bu yapılandırma öğesini içeren bir yapılandırma temeli oluşturun. Ana temeli hedef koleksiyona dağıtın.  

     Daha fazla bilgi için bkz. [yapılandırma temelleri oluşturma](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. SMSıD 'nin kaldırıldığı Mac bilgisayarlarına yeni bir sertifika yükledikten sonra, istemciyi yeni sertifikayı kullanacak şekilde yapılandırmak için aşağıdaki komutu çalıştırın:  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Ayrıca bkz.

[Mac bilgisayarlara istemci dağıtmaya hazırlanma](prepare-to-deploy-mac-clients.md)

[Mac istemcilerinin bakımını yapma](../manage/maintain-mac-clients.md)
