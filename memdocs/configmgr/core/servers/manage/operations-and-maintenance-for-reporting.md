---
title: Raporlamaya yönelik işlemler ve bakım
titleSuffix: Configuration Manager
description: Configuration Manager ' de raporların ve rapor aboneliklerinin yönetilmesine ilişkin ayrıntıları öğrenin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 5e154f2859a7541ac8f67b8588da7dfb8877c940
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713719"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Configuration Manager raporlama için işlemler ve bakım

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Altyapı Configuration Manager raporlama için olduktan sonra, raporları ve rapor aboneliklerini yönetmek için genellikle yaptığınız birkaç işlem vardır.

> [!NOTE]
> Bu makale SQL Server Reporting Services Reports 'a odaklanır. Sürüm 2002 ' den başlayarak raporlamayı Power BI Rapor Sunucusu ile tümleştirebilirsiniz. Daha fazla bilgi için bkz. [Power BI rapor sunucusu tümleştirme](powerbi-report-server.md).

## <a name="run-a-report-from-reporting-services"></a>Raporlama hizmetlerinden rapor çalıştırma

Configuration Manager raporlarını SQL Server Reporting Services depolar. Rapor, verileri Configuration Manager site veritabanından alır. Configuration Manager konsolundaki raporlara veya bir Web tarayıcısı aracılığıyla Rapor Yöneticisi kullanarak erişebilirsiniz. Raporları, Raporlama Hizmetleri noktasına erişebilen herhangi bir bilgisayarda bir Web tarayıcısından açın ve Kullanıcı, raporları görüntülemek için yeterli haklara sahip olabilir. Raporları çalıştırmak için **site** izni ve belirli nesneler Için **Raporu Çalıştır** iznine yönelik **okuma** haklarına sahip olmanız gerekir.

Bir raporu çalıştırdığınızda, rapor başlığını, açıklamasını ve kategorisini yerel işletim sisteminin dilinde görüntüler. Daha fazla bilgi için bkz. [raporlar Için diller](configuring-reporting.md#-languages-for-reports).

> [!NOTE]  
> Rapor Yöneticisi, Web tabanlı bir rapor erişim ve yönetim aracıdır. Bunu, HTTPS bağlantısı üzerinden tek bir rapor sunucusu örneğini yönetmek için kullanabilirsiniz. İşletimsel görevler için Rapor Yöneticisi kullanın: raporları görüntüleyin, rapor özelliklerini değiştirin ve ilişkili rapor aboneliklerini yönetin. Bu makalede, Rapor Yöneticisi rapor görüntüleme ve rapor özelliklerini değiştirme adımları sağlanmaktadır. Rapor Yöneticisi diğer seçenekler hakkında daha fazla bilgi için bkz. [Rapor Yöneticisi nedir?](https://docs.microsoft.com/sql/reporting-services/report-manager-ssrs-native-mode)

Bir Configuration Manager raporu çalıştırmak için aşağıdaki yordamları kullanın.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Configuration Manager konsolunda bir rapor çalıştırma

1. Configuration Manager konsolunda **izleme** çalışma alanına gidin. **Raporlama**' yı genişletin ve **raporlar**' ı seçin. Bu düğüm, kullanılabilir raporları listeler.

    > [!TIP]
    > Bu düğüm hiçbir rapor listemezse, Raporlama Hizmetleri noktasının yüklü ve yapılandırılmış olduğunu doğrulayın. Daha fazla bilgi için bkz. [raporlamayı yapılandırma](configuring-reporting.md).

1. Çalıştırmak istediğiniz raporu seçin. Şeridin **giriş** sekmesinde, **rapor grubu** bölümünde, raporu açmak için **Çalıştır** ' ı seçin.

1. Gerekli parametreler varsa, bunları belirtin ve sonra **raporu görüntüle**' yi seçin.

### <a name="run-a-report-in-a-web-browser"></a>Bir raporu Web tarayıcısında çalıştırma

1. Web tarayıcınızda Rapor Yöneticisi URL 'sine gidin, örneğin, `https://Server1/Reports`. Reporting Services Configuration Manager **Rapor Yöneticisi URL 'si** sayfasında bu adresi bulun.

1. Rapor Yöneticisi, Configuration Manager için rapor klasörünü (örneğin, **ConfigMgr_CAS**) seçin.

    > [!TIP]
    > Rapor Yöneticisi rapor listemezse, Raporlama Hizmetleri noktasının yüklü ve yapılandırılmış olduğunu doğrulayın. Daha fazla bilgi için bkz. [raporlamayı yapılandırma](configuring-reporting.md).

1. Çalıştırmak istediğiniz rapor için rapor kategorisini seçin ve ardından belirli raporu seçin. Rapor Rapor Yöneticisi açılır.

1. Gerekli parametreler varsa, bunları belirtin ve sonra **raporu görüntüle**' yi seçin.

## <a name="modify-the-properties-of-a-report"></a>Bir raporun özelliklerini değiştirme

Rapor özellikleri rapor adı ve açıklamasını içerir. Configuration Manager konsolunun bir raporun özelliklerini görüntüleyebilirsiniz.

Özellikleri değiştirmek için Rapor Yöneticisi kullanın:

1. Web tarayıcınızda Rapor Yöneticisi URL 'sine gidin, örneğin, `https://Server1/Reports`.

1. Rapor Yöneticisi, Configuration Manager için rapor klasörünü (örneğin, **ConfigMgr_CAS**) seçin.

1. Rapor kategorisini seçin ve ardından belirli raporu seçin. Rapor Rapor Yöneticisi açılır.

1. **Özellikler** sekmesini seçin. rapor adını ve açıklamasını değiştirin ve ardından **Uygula**' yı seçin.

Rapor Yöneticisi rapor özelliklerini rapor sunucusuna kaydeder. Configuration Manager konsolu raporun güncelleştirilmiş rapor özelliklerini gösterir.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a>Rapor düzenleme

Mevcut bir Configuration Manager rapor, istediğiniz bilgileri almadığında, Rapor Oluşturucusu ' de düzenleyin. Ayrıca, raporun düzen veya tasarımını değiştirmek için Rapor Oluşturucusu de kullanabilirsiniz. Varsayılan bir raporu doğrudan düzenleyebileceğiniz sırada klonlamak en iyisidir. Düzenlemek için raporu açın ve **farklı kaydet**' i seçin.

Bir raporu düzenlemek için, rapordaki belirli nesneler üzerinde **site değiştirme** Iznine ve **rapor değiştirme** izinlerine sahip olmanız gerekir.

> [!IMPORTANT]
> Site güncelleştirmeleri yerleşik raporları korur. Bir standart raporu değiştirirseniz, site güncelleştirildiğinde, raporu alt çizgi öneki (`_`) ile yeniden adlandırır. Bu davranış, site güncelleştirmesinin standart rapor tarafından değiştirilen raporun üzerine yazılmayacağı şekilde emin olur.
>
> Önceden tanımlanmış raporları değiştirirseniz, bir site güncelleştirmesini yüklemeden önce özel raporlarınızı yedekleyin. Güncelleştirmeden sonra raporu Raporlama Hizmetleri 'ne geri yükleyin. Önceden tanımlanmış bir raporda önemli değişiklikler yaparsanız bunun yerine yeni bir rapor oluşturun. Bir siteyi yükseltmeden önce oluşturduğunuz yeni raporların üzerine yazılmaz.

Bir Configuration Manager raporunun özelliklerini düzenlemek için aşağıdaki yordamı kullanın.

1. Configuration Manager konsolunda **izleme** çalışma alanına gidin. **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin.

1. Değiştirmek istediğiniz raporu seçin. Şeridin **giriş** sekmesinde, **rapor grubu** bölümünde, **Düzenle**' yi seçin. Kimlik bilgilerini girmenizi isteyebilir. Rapor Oluşturucusu bilgisayarda yüklü değilse, Configuration Manager yüklemenizi ister. Raporları değiştirmek ve oluşturmak için Rapor Oluşturucusu gereklidir.

1. Rapor Oluşturucusu, uygun rapor ayarlarını değiştirin. Raporu rapor sunucusuna kaydetmek için **Kaydet** ' i seçin.

## <a name="create-reports"></a>Rapor oluşturma

Oluşturabileceğiniz iki tür rapor vardır:

- **Model tabanlı bir rapor** , raporunuza dahil etmek istediğiniz öğeleri etkileşimli bir şekilde seçmenizi sağlar. Özel rapor modelleri oluşturma hakkında daha fazla bilgi için bkz. [SQL Server Reporting Services Configuration Manager için özel rapor modelleri oluşturma](creating-custom-report-models-in-sql-server-reporting-services.md).

- **SQL tabanlı bir rapor** , BIR rapor SQL bildirisini temel alan verileri almanızı sağlar.

> [!IMPORTANT]
> Yeni bir rapor oluşturmak için hesabınızın **site değiştirme** izni olması gerekir. Yalnızca **rapor değiştirme** izinlerine sahip olduğunuz klasörlerde bir rapor oluşturabilirsiniz.

### <a name="create-a-model-based-report"></a>Model tabanlı rapor oluşturma

Model tabanlı bir Configuration Manager raporu oluşturmak için aşağıdaki yordamı kullanın.

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** bölümünde **rapor oluştur**' u seçin. Bu eylem **rapor oluşturma Sihirbazı 'nı**açar.

1. **Bilgi** sayfasında, aşağıdaki ayarları yapılandırın:

    - **Tür**: **model tabanlı rapor**seçin.

    - **Ad**: rapor için bir ad belirtin.

    - **Açıklama**: rapor için bir açıklama belirtin.

    - **Sunucu**: Bu raporu oluşturduğunuz rapor sunucusunun adını görüntüler.

    - **Yol**: raporun kaydedileceği klasörü belirtmek için **Araştır** ' ı seçin.

1. **Model seçimi** sayfasında, bu raporu oluşturmak için listeden kullanılabilir bir modeli seçin. **Önizleme** bölümünde, bu rapor modelinde kullanılabilen SQL Server görünümleri ve varlıkları görüntülenir.

1. Rapor oluşturma Sihirbazı 'Nı doldurun.

1. Rapor ayarlarını yapılandırmak için Rapor Oluşturucusu açın. Daha fazla bilgi için bkz. [Configuration Manager raporunu düzenleme](#bkmk_edit).

1. Rapor Oluşturucusu, rapor düzeni oluşturun, kullanılabilir SQL Server görünümlerindeki verileri seçin ve rapora parametreler ekleyin.

1. Raporunuzu çalıştırmak için **Çalıştır** ' ı seçin. Raporun, beklediğinizi bilgileri sağladığını doğrulayın. Gerekirse, raporu daha fazla değiştirmek için **Tasarım** ' ı seçin.

1. Raporu rapor sunucusuna kaydetmek için **Kaydet** ' i seçin.

### <a name="create-a-sql-based-report"></a>SQL tabanlı rapor oluşturma

Özel rapor için bir SQL bildirimi oluşturduğunuzda SQL Server tablolarına doğrudan başvurmayın. Site veritabanından desteklenen raporlama SQL Server görünümlerine her zaman başvurun. Bu görünümlerde ile `v_`başlayan adlar vardır. Daha fazla bilgi için bkz. [Configuration Manager SQL Server görünümlerini kullanarak özel raporlar oluşturma](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

Ayrıca, site veritabanından ortak saklı yordamlara de başvurabilirsiniz. Bu saklı yordamların ile `sp_`başlayan adları vardır.

SQL tabanlı bir Configuration Manager raporu oluşturmak için aşağıdaki yordamı kullanın.

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** bölümünde **rapor oluştur**' u seçin. Bu eylem **rapor oluşturma Sihirbazı 'nı**açar.

1. **Bilgi** sayfasında, aşağıdaki ayarları yapılandırın:

    - **Yazın**: **SQL tabanlı rapor**' u seçin.

    - **Ad**: rapor için bir ad belirtin.

    - **Açıklama**: rapor için bir açıklama belirtin.

    - **Sunucu**: Bu raporu oluşturduğunuz rapor sunucusunun adını görüntüler.

    - **Yol**: raporun kaydedileceği klasörü belirtmek için **Araştır** ' ı seçin.

1. Rapor oluşturma Sihirbazı 'Nı doldurun.

1. Rapor ayarlarını yapılandırmak için Rapor Oluşturucusu açın. Daha fazla bilgi için bkz. [Configuration Manager raporunu düzenleme](#bkmk_edit).

1. Rapor Oluşturucusu ' de, rapor için SQL ifadesini belirtin. Ayrıca, kullanılabilir görünümlerde sütunları kullanarak SQL ifadesini de oluşturabilirsiniz. Gerekirse, rapora parametreler ekleyin.

1. Raporunuzu çalıştırmak için **Çalıştır** ' ı seçin. Raporun, beklediğinizi bilgileri sağladığını doğrulayın. Gerekirse, raporu daha fazla değiştirmek için **Tasarım** ' ı seçin.

1. Raporu rapor sunucusuna kaydetmek için **Kaydet** ' i seçin.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a>Rapor aboneliklerini yönetme

SQL Server Reporting Services ' de rapor abonelikleri, belirtilen raporların e-posta veya zamanlanan aralıklarda bir dosya paylaşımında otomatik olarak teslimini yapılandırmanızı sağlar. Rapor aboneliklerini yapılandırmak için, Configuration Manager **abonelik oluşturma Sihirbazı 'nı** kullanın.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Bir dosya paylaşımında rapor teslim etmek için bir rapor aboneliği oluşturma

Bir dosya paylaşımında rapor teslim etmek üzere bir rapor aboneliği oluşturduğunuzda, Raporlama Hizmetleri raporu belirtilen biçimde, belirttiğiniz dosya paylaşımında kopyalar. Tek seferde yalnızca bir rapor için abone olabilir ve teslim isteyebilirsiniz.

Bir dosya paylaşımının kullanıldığı bir abonelik oluşturduğunuzda, hedef olarak var olan bir paylaşılan klasör belirtin. Rapor sunucusu, klasörü veya ağ payını oluşturmaz. Bir abonelikte hedef klasörü belirttiğinizde, bir UNC yolu kullanın ve klasör yolunda sonunda ters eğik çizgi (`\`) eklemeyin. Aşağıdaki örnek, hedef klasör için geçerli bir UNC yoludur: `\\server\reportfiles\operations\2001`.

> [!NOTE]
> Aboneliği oluştururken, bir Kullanıcı adı ve parola belirtirsiniz. Bu hesabın hedef klasöre **yazma** izinleri olan bu paylaşıma erişmesi gerekir.

Raporlama Hizmetleri, raporları farklı dosya biçimlerinde işleyebilir. Örneğin, MHTML veya Excel. Aboneliği oluştururken biçimi seçersiniz. Desteklenen bir işleme biçimini seçebilirsiniz, ancak bazı biçimler bir dosyaya işlerken diğerlerinden daha iyi çalışır.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Bir dosya paylaşımıyla ilgili rapor aboneliklerine yönelik sınırlamalar

Aşağıdaki liste, rapor aboneliklerinin bir dosya paylaşımında sınırlamalarını içerir:

- Rapor sunucusu üzerinde ana bilgisayar ve yönettiğiniz raporların aksine, Raporlama Hizmetleri raporları paylaşılan bir klasöre statik dosyalar olarak gönderir.

- Raporun etkileşimli özellikleri, dosya olarak depolanan raporlar için çalışmaz. Rapor, herhangi bir etkileşimli özelliği statik öğe olarak temsil eder.

- Rapor grafikler içeriyorsa, varsayılan sunumu kullanır.

- Rapor, başka bir rapora bağlantı alıyorsa, bağlantıyı statik metin olarak işler.

Teslim edilen bir rapordaki etkileşimli özellikleri korumak istiyorsanız, e-posta teslimi kullanın. Daha fazla bilgi için bkz. [e-posta ile rapor teslim etmek için rapor aboneliği oluşturma](#bkmk_subscription-email).

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Dosya paylaşımının rapor aboneliğini oluşturma işlemi

Bir dosya paylaşımında rapor teslim etmek üzere bir rapor aboneliği oluşturmak için aşağıdaki yordamı kullanın.  

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin.

1. Bir rapor klasörü seçin ve ardından abone olmak istediğiniz raporu seçin. Şeridin **giriş** sekmesinde, **rapor grubu** bölümünde, **abonelik oluştur**' u seçin. Bu eylem **abonelik oluşturma Sihirbazı**' nı açar.

1. **Abonelik teslimi** sayfasında, aşağıdaki ayarları yapılandırın:  

    - **Raporu teslim eden**: **Windows dosya paylaşma**' yı seçin.

    - **Dosya adı**: rapor için dosya adını belirtin. Varsayılan olarak, rapor dosyası bir dosya adı uzantısı içermez. Bir dosya adı uzantısını otomatik olarak biçime göre eklemek için **oluşturulduğunda dosya uzantısı Ekle** ' yi seçin.

    - **Yol**: Bu raporu göndermek istediğiniz var olan bir klasöre YÖNELIK bir UNC yolu belirtin. Örneğin, `\\server\reportfiles\operations`.

    - **Işleme biçimi**: rapor dosyası için aşağıdaki biçimlerden birini seçin:

      - **Rapor verileri olan XML dosyası**
      - **CSV (virgülle ayrılmış)**
      - **TIFF dosyası**
      - **Acrobat (PDF) dosyası**
      - **HTML 4,0**
        > [!NOTE]
        > Raporunuzda görüntüler varsa, HTML 4,0 biçimi bunları içermez.
      - **MHTML (Web arşivi)**
      - **RPL Oluşturucusu** (rapor sayfası düzeni)
      - **Excel**
      - **Word**

    - **Kullanıcı adı**: belirtilen **yol**için *yazma* izinlerine sahip bir Windows Kullanıcı hesabı belirtin.

    - **Parola**: Yukarıdaki Windows Kullanıcı hesabının parolasını belirtin.

    - **Üzerine yazma seçeneği**: hedef klasörde aynı ada sahip bir dosya varken davranışı yapılandırmak için aşağıdaki seçeneklerden birini belirleyin:

      - **Varolan bir dosyanın üzerine daha yeni bir sürüm yazın**
      - **Varolan bir dosyanın üzerine yazma**
      - **Daha yeni sürümler eklendikçe dosya adlarını artır**: Bu seçenek, önceki sürümlerden ayırt edilebilmesi için yeni raporun dosya adına bir sayı ekler.

    - **Açıklama**: isteğe bağlı olarak, bu rapor aboneliğiyle ilgili ek bilgileri belirtin.

1. **Abonelik zamanlaması** sayfasında, rapor aboneliği için aşağıdaki teslim zamanlaması seçeneklerinden birini seçin:

    - **Paylaşılan zamanlama kullan**: paylaşılan bir zamanlama, diğer rapor abonelikleri tarafından kullanılabilen önceden tanımlanmış bir zamanlamadır. Bu seçeneği belirlediğinizde, paylaşılan bir zamanlama da seçin. Paylaşılan zamanlama yoksa, yeni bir zamanlama oluşturma seçeneğini belirleyin.

    - **Yeni zamanlama oluştur**: Bu raporun çalışacağı zamanlamayı yapılandırın. Zamanlama, bu aboneliğin aralığını, başlangıç saatini ve tarihini ve bitiş tarihini içerir. Varsayılan olarak, yeni bir abonelik geçerli tarih ve saatte başlayarak her saat çalışacak yeni bir zamanlama oluşturur.

1. **Abonelik parametreleri** sayfasında, bu raporun katılımsız çalışması için gerekli tüm parametreleri belirtin. Raporda parametre yoksa, sihirbaz bu sayfayı görüntülemez.

1. Sihirbazı tamamlayın.

1. Configuration Manager rapor aboneliğini başarıyla oluşturduğunu doğrulayın. Rapor aboneliklerini görüntülemek ve değiştirmek için **abonelikler** düğümünü seçin.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a>Raporu e-postayla teslim etmek için rapor aboneliği oluşturma

Raporu e-postayla teslim etmek için bir rapor aboneliği oluşturduğunuzda, Raporlama Hizmetleri yapılandırdığınız alıcılara bir e-posta gönderir. E-posta, raporu ek olarak içerir. Rapor sunucusu e-posta adreslerini doğrulamaz veya bir e-posta sunucusundan alamaz. Raporları kuruluşunuzun içindeki veya dışındaki geçerli bir e-posta hesabına e-posta ile gönderebilirsiniz.

> [!NOTE]
> **E-posta** aboneliği seçeneğini etkinleştirmek Için, Raporlama Hizmetleri 'ndeki e-posta ayarlarını yapılandırmanız gerekir. Daha fazla bilgi için bkz. [Reporting Services 'Da e-posta teslimi](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services).

Aşağıdaki e-posta teslim seçeneklerinden birini veya her ikisini seçebilirsiniz:

- Oluşturulan raporun bağlantısını içeren bir bildirim gönderin.

- Eklenmiş veya iliştirilmiş bir rapor gönderin. İşleme biçimi ve tarayıcı, raporu katıştırıp katışmadığını veya iliştirir belirtir.

  - Tarayıcınız HTML 4,0 ve MHTML 'yi destekliyorsa ve **MHTML (Web arşivi)** biçimini seçerseniz, e-posta raporu iletiye gömer.
  - Diğer tüm biçimler raporları ekler olarak sunar.
  - Raporlama Hizmetleri, raporu göndermeden önce ekin veya iletinin boyutunu denetlemez. Ek veya ileti, posta sunucunuz tarafından izin verilen üst sınırı aşarsa rapor teslim değildir.

E-posta kullanarak rapor teslim etmek üzere bir rapor aboneliği oluşturmak için aşağıdaki yordamı kullanın.  

1. Configuration Manager konsolunda, **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin.

1. Bir rapor klasörü seçin ve ardından abone olmak istediğiniz raporu seçin. Şeridin **giriş** sekmesinde, **rapor grubu** bölümünde, **abonelik oluştur**' u seçin. Bu eylem **abonelik oluşturma Sihirbazı**' nı açar.

1. **Abonelik teslimi** sayfasında, aşağıdaki ayarları yapılandırın:  

    - **Raporu teslim eden**: **e-posta**seçin.

    - **Kime**: alıcı olarak geçerli bir e-posta adresi belirtin.

        > [!NOTE]
        > Birden çok alıcı girmek için her e-posta adresini noktalı virgülle (`;`) ayırın.

    - **Bilgi**: isteğe bağlı olarak, bu raporun bir kopyasını almak için bir e-posta adresi belirtin.

    - **Gizli**: isteğe bağlı olarak, bu raporun gizli bir kopyasını almak için bir e-posta adresi belirtin.

    - **Yanıtla**: yanıt adresini belirtin. Alıcı, e-posta iletisine yanıt verdiğinde, yanıt bu adrese gider.

    - **Konu**: abonelik e-posta iletisi için bir konu satırı belirtin.

    - **Öncelik**: Bu e-posta iletisi için öncelik bayrağını seçin: **düşük**, **normal**veya **yüksek**. Microsoft Exchange bu bayrağı, e-posta iletisinin önemini göstermek için kullanır.

    - **Açıklama**: abonelik e-posta iletisinin gövdesi için metin belirtin.

    - **Açıklama**: isteğe bağlı olarak, bu rapor aboneliğiyle ilgili ek bilgileri belirtin.

    - **Bağlantıyı Ekle**: e-posta iletisinin gövdesine bu raporun URL 'sini ekleyin.

    - **Raporu Ekle**: e-posta iletisine ekleyin. Eklenecek rapor biçimini belirtmek için **Işleme biçimi** seçeneğini kullanın.

    - **Işleme biçimi**: ekli rapor dosyası için aşağıdaki biçimlerden birini seçin:

      - **Rapor verileri olan XML dosyası**
      - **CSV (virgülle ayrılmış)**
      - **TIFF dosyası**
      - **Acrobat (PDF) dosyası**
      - **MHTML (Web arşivi)**
      - **Excel**
      - **Word**

1. **Abonelik zamanlaması** sayfasında, rapor aboneliği için aşağıdaki teslim zamanlaması seçeneklerinden birini seçin:

    - **Paylaşılan zamanlama kullan**: paylaşılan bir zamanlama, diğer rapor abonelikleri tarafından kullanılabilen önceden tanımlanmış bir zamanlamadır. Bu seçeneği belirlediğinizde, paylaşılan bir zamanlama da seçin. Paylaşılan zamanlama yoksa, yeni bir zamanlama oluşturma seçeneğini belirleyin.

    - **Yeni zamanlama oluştur**: Bu raporun çalışacağı zamanlamayı yapılandırın. Zamanlama, bu aboneliğin aralığını, başlangıç saatini ve tarihini ve bitiş tarihini içerir. Varsayılan olarak, yeni bir abonelik geçerli tarih ve saatte başlayarak her saat çalışacak yeni bir zamanlama oluşturur.

1. **Abonelik parametreleri** sayfasında, bu raporun katılımsız çalışması için gerekli tüm parametreleri belirtin. Raporda parametre yoksa, sihirbaz bu sayfayı görüntülemez.

1. Sihirbazı tamamlayın.

1. Configuration Manager rapor aboneliğini başarıyla oluşturduğunu doğrulayın. Rapor aboneliklerini görüntülemek ve değiştirmek için **abonelikler** düğümünü seçin.
