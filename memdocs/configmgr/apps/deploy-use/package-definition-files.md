---
title: Paket tanımı dosyaları
titleSuffix: Configuration Manager
description: Configuration Manager içinde paket ve program oluşturmak için paket tanım dosyalarını kullanma hakkında bilgi edinin
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710142"
---
# <a name="package-definition-files"></a>Paket tanımı dosyaları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Paket tanımı dosyaları, Configuration Manager [paketlerin ve programların](packages-and-programs.md) oluşturulmasını otomatik hale getirmenize yardımcı olan betiklerdir. Bunlar, paket kaynak dosyalarının konumu dışında, bir paket ve program oluşturmak için gereken Configuration Manager tüm bilgileri sağlar.

## <a name="about-the-package-definition-file-format"></a>Paket tanımı dosya biçimi hakkında

Her paket tanım dosyası. ini dosya biçimini kullanan bir ASCII veya UTF-8 metin dosyasıdır. Aşağıdaki bölümleri içerir:  

### <a name="pdf"></a>[PDF]

Bu bölüm, dosyayı bir paket tanımlama dosyası olarak tanımlar. Aşağıdaki bilgileri içerir:  

- **Sürüm**: dosyanın kullandığı paket tanım dosyası biçiminin sürümünü belirtin. Bu sürüm, yazıldığı Configuration Manager sürümüne karşılık gelir. Bu girdi gereklidir.  

### <a name="package-definition"></a>[Package Definition]

Paket ve programın özelliklerini belirtin. Aşağıdaki bilgileri sağlar:  

- **Name**: En çok 50 karakter uzunluğunda olacak şekilde, paketin adı.  

- **Sürüm** (isteğe bağlı): en fazla 32 karakter uzunluğunda olmak üzere paketin sürümü.  

- **Simge** (isteğe bağlı): Bu paket için kullanılacak simgeyi içeren dosya. Belirtilmişse, bu simge Configuration Manager konsolundaki varsayılan paket simgesinin yerini alır.

- **Publisher**: En çok 32 karakter uzunluğunda olacak şekilde, paketin yayımcısı.

- **Language**: En çok 32 karakter uzunluğunda olacak şekilde, paketin dil sürümü.

- **Açıklama** (isteğe bağlı): 127 karakter kadar paketle ilgili bir açıklama.

- **Containsnofbir**: Bu giriş, paketin herhangi bir kaynak dosyasına sahip olup olmadığını gösterir.  

- **Programlar**: Bu paket için tanımladığınız programlar. Her bir program adı, bu paket tanımlama dosyasındaki bir **[Program]** bölümüne karşılık gelir.  

    Örnek:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: En çok 50 karakter uzunluğunda olacak şekilde, paket durumunu içeren Yönetim Bilgisi Biçimi (MIF) dosyasının adı.  

- **Mifname**: en fazla 50 karakter uzunluğunda olan MIF eşleştirme paketinin adı.  

- **Mifversion**: en fazla 32 karakter uzunluğunda olan MIF eşleştirme paketinin sürüm numarasıdır.  

- **Mifpublisher**: en fazla 32 karakter uzunluğunda olan MIF eşleştirme paketinin yazılım yayımcısı.  

### <a name="program"></a>[Program]

**[Paket tanımı]** bölümündeki **Programlar** girişinde belirttiğiniz her program için bir [Program] bölümü ekleyin. Bu bölüm her programı tanımlar. Her program bölümü aşağıdaki bilgileri sağlar:  

- **Name**: En çok 50 karakter uzunluğunda olacak şekilde, programın adı. Bu girdi, bir paket içinde benzersiz olmalıdır.  

- **Simge** (isteğe bağlı): Bu program için kullanılacak simgeyi Içeren dosyayı belirtin. Bu simge, Configuration Manager konsolundaki varsayılan program simgesinin yerini alır. Ayrıca, programı bir koleksiyona dağıttığınızda istemci bu simgeyi görüntüler.

- **Açıklama** (isteğe bağlı): en fazla 127 karakter olan program hakkında bir açıklama.

- **CommandLine**: en çok 127 karakter uzunluğunda olacak şekilde, program için komut satırını belirtin. Komut, paket kaynak klasörüne görelidir.

- **Startın**: en çok 127 karakter uzunluğunda olacak şekilde, program için çalışma klasörünü belirtin. Bu giriş, istemci bilgisayardaki mutlak bir yol veya paket kaynak klasörüne göreli bir yol olabilir.

- **Çalıştır**: programın çalıştığı program modunu belirtin. **Minimized**, **Maximized** veya **Hidden** seçeneklerinden birini belirtebilirsiniz. Bu girişi eklemezseniz, program normal modda çalışır.  

- **AfterRunning**: Program başarıyla tamamlandıktan sonra gerçekleşen özel bir eylemi belirtin. **SMSRestart**, **ProgramRestart** veya **SMSLogoff** seçenekleri kullanılabilir. Bu girişi eklemezseniz, program özel bir eylem çalıştırmaz.  

- **EstimatedDiskSpace**: yazılım programının bilgisayarda çalışması için gereken disk alanı miktarını belirtin. Varsayılan değer **bilinmiyor**. Değeri sıfırdan büyük veya sıfıra eşit bir tamsayı olarak ayarlayabilirsiniz. Değer belirtirseniz, değer için birimleri de dahil edin.  

    Örnek:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**: programın istemci bilgisayarda çalıştırılmasını bekleyeceğiniz tahmini süreyi dakika olarak belirtin. Varsayılan değer **120**' dir. Değeri sıfırdan büyük veya **Bilinmeyen**bir tam sayı olarak ayarlayabilirsiniz.  

    Örnek:  

    `EstimatedRunTime=25`  

- **SupportedClients**: Bu programın üzerinde çalıştığı işlemcileri ve işletim sistemlerini belirtin. Platformları virgülle ayırın. Bu girişi eklemezseniz, istemci bu program için desteklenen platformları denetlemez.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: **SupportedClients** girdisinde belirtilen işletim sistemlerinin sürüm numaraları için başlangıç-bitiş aralığını belirtin.  

    Örnek:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (isteğe bağlı): en fazla 127 karakter uzunluğunda istemci bilgisayarlar için diğer bilgileri veya gereksinimleri belirtin.

- **Canrunne zaman**: programın istemci bilgisayarda çalışması için gereken Kullanıcı durumunu belirtin. **UserLoggedOn**, **NoUserLoggedOn** veya **AnyUserStatus** değerleri kullanılabilir. **UserLoggedOn** varsayılan değerdir.  

- **UserInputRequired**: programın kullanıcıyla etkileşime ihtiyacı olup olmadığını belirtin. Kullanılabilir değerler **True** veya **False**’tur. Varsayılan değer **true**'dur. **Canrunıf** , **UserLoggedOn**olarak ayarlanmazsa, bu girdi **false** olarak ayarlanır.  

- **Adminettsrequired**: programın çalıştırmak için bilgisayarda yönetici kimlik bilgilerinin gerekli olup olmadığını belirtin. Kullanılabilir değerler **True** veya **False**’tur. Varsayılan değer **false**'dur. **Canrunıf** , **UserLoggedOn**olarak ayarlanmazsa, bu girdi **true** olarak ayarlanır.  

- **UseInstallAccount**: programın istemci bilgisayarlarda çalıştırıldığında istemci yazılımı yükleme hesabını kullanıp kullanmayacağını belirtin. Varsayılan olarak bu değer **False**’tur. Ayrıca **CanRunWhen** değeri **UserLoggedOn** olarak ayarlanmışsa da bu değer **False**’tur.  

- **DriveLetterConnection**: Programın dağıtım noktasındaki paket dosyalarına bir sürücü harfi bağlantısı gerektirip gerektirmediğini belirtin. **True** veya **False** olarak belirtebilirsiniz. Varsayılan değer **false**şeklindedir, bu da programın bir evrensel adlandırma KURALı (UNC) bağlantısı kullanmasına olanak sağlar. Bu değer **true**olarak ayarlandığında, istemci Z: ile başlayıp sonraki kullanılabilir sürücü harfini kullanır ve geriye devam edin.  

- **Ydrive** belirtir (isteğe bağlı): Programın dağıtım noktasındaki paket dosyalarına bağlanması için gereken bir sürücü harfi belirtin. Bu ayar, dağıtım noktalarına istemci bağlantıları için belirtilen sürücü harfinin kullanımını zorlar.

- **ReconnectDriveAtLogon**: Kullanıcı oturum açtığında bilgisayarın dağıtım noktasına yeniden bağlanıp bağlanmayacağını belirtin. Kullanılabilir değerler **True** veya **False**’tur. Varsayılan değer **false**'dur.  

- **DependentProgram**: Bu pakette, geçerli programdan önce çalıştırılması gereken bir program belirtin. Bu girdi biçimini `DependentProgram=<ProgramName>`kullanır. burada `<ProgramName>` , paket tanım dosyasındaki bu programın **ad** girişi olur. Bağımlı program yoksa, bu girdiyi boş bırakın.  

    Örnekler:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Atama**: programın kullanıcılara nasıl atandığını belirtin. Bu değer şu olabilir:

    - **FirstUser**: yalnızca istemcide oturum açan ilk Kullanıcı programı çalıştırır
    - **Herkes kullanıcısı**: oturum açan her kullanıcı programı çalıştırır

    **Canrunne zaman** **UserLoggedOn**olarak ayarlanmazsa, bu girdi **FirstUser**olarak ayarlanır.  

- **Devre dışı**: Bu programı istemcilere dağıtacağınızı belirtin. Kullanılabilir değerler **True** veya **False**’tur. Varsayılan değer **false**'dur.  


## <a name="use-a-package-definition-file"></a>Paket tanımı dosyası kullan  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **paketler** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **Tanımdan Paket Oluştur**' u seçin.  

3. **Tanımdan Paket Oluştur Sihirbazı**' nın **paket tanımı** sayfasında, var olan bir paket tanımı dosyasını seçin. Yeni bir paket tanımı dosyası açmak için, **Araştır**' ı seçin. Yeni bir paket tanımı dosyası belirttikten sonra **paket tanımı** listesinden seçin.

4. **Kaynak dosyaları** sayfasında paket ve program için gereken tüm kaynak dosyaları hakkındaki bilgileri belirtin.  

5. Paket kaynak dosyaları gerektiriyorsa, **kaynak klasör** sayfasında, sitenin kaynak dosyaları nereden geçirebileceği konumu belirtin.  

6. Sihirbazı tamamlayın.  


## <a name="see-also"></a>Ayrıca bkz.

[Paketler ve programlar](packages-and-programs.md)
