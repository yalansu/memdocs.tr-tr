---
title: 'Önyükleme görüntülerini özelleştirme '
titleSuffix: Configuration Manager
description: Bir önyükleme görüntüsünü özelleştirmek için Configuration Manager veya Dağıtım Görüntüsü Bakımı ve yönetimi (DıSM) komut satırı aracını kullanmanın birkaç yolunu öğrenin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc679ec7e73e9d43902ad70e09fb2a01c95eed65
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906876"
---
# <a name="customize-boot-images-with-configuration-manager"></a>Configuration Manager ile önyükleme görüntülerini özelleştirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager her sürümü belirli bir Windows değerlendirme ve Dağıtım Seti (Windows ADK) sürümünü destekler. Windows ADK 'nin desteklenen sürümünden bir Windows PE sürümünü temel alırken Configuration Manager konsolundan önyükleme görüntülerini hizmet edebilir veya özelleştirebilirsiniz. Diğer önyükleme görüntüleri söz konusu olduğunda, Windows AIK ve Windows ADK'nin parçası olan Dağıtım Görüntüsü Bakımı ve Yönetimi (DISM) komut satırı aracı gibi başka bir yöntem kullanarak özelleştirmeniz gerekir  

 Aşağıdakiler, Windows ADK 'nin desteklenen sürümünü, Configuration Manager konsolundan özelleştirilebilecek önyükleme görüntüsünün temel aldığı Windows PE sürümünü ve DıSM kullanarak özelleştirebileceğiniz ve ardından görüntüyü Configuration Manager eklemek için temel alınan Windows PE sürümlerini sağlamaktadır.  

- **Windows ADK sürümü**  

   Windows 10 için Windows ADK  

- **Configuration Manager konsolundan özelleştirilebilen önyükleme görüntüleri için Windows PE sürümleri**  

   Windows PE 10  

- **Configuration Manager konsolundan özelleştirilemeyen önyükleme görüntüleri için desteklenen Windows PE sürümleri**  

   Windows PE 3.1<sup>1</sup> ve Windows PE 5  

   <sup>1</sup> yalnızca Windows PE 3,1 tabanlı Configuration Manager bir önyükleme görüntüsü ekleyebilirsiniz. Windows 7 için Windows AIK'yi (Windows PE 3 tabanlı) Windows 7 SP1 için Windows AIK Eki (Windows PE 3.1 tabanlı) ile yükseltmek için, Windows 7 SP1 için Windows AIK Eki'ni yükleyin. Windows 7 SP1 için Windows AIK Eki'ni [Microsoft İndirme Merkezi](https://www.microsoft.com/download/details.aspx?id=5188)'nden indirebilirsiniz.  

   Örneğin, Configuration Manager sahip olduğunuzda, Windows 10 için Windows ADK (Windows PE 10 tabanlı) önyükleme görüntülerini Configuration Manager konsolundan özelleştirebilirsiniz. Bununla birlikte, Windows PE 5 tabanlı önyükleme görüntüleri desteklendiğinden, bunları farklı bir bilgisayardan özelleştirmeniz ve DISM'nin Windows 8 için Windows ADK ile birlikte yüklenen sürümünü kullanmanız gerekir. Ardından, önyükleme görüntüsünü Configuration Manager konsoluna ekleyebilirsiniz.  

  Bu konudaki yordamlar, aşağıdaki Windows PE paketlerini kullanarak Configuration Manager için gereken isteğe bağlı bileşenlerin önyükleme görüntüsüne nasıl ekleneceğini gösterir:  

- **WinPE-WMI**: Windows Yönetim Araçları (WMI) desteği ekler.  

- **WinPE-Scripting**: Windows Komut Dosyası Sistemi (WSH) desteği ekler.  

- **WinPE-WDS-Tools**: Windows Dağıtım Hizmetleri araçlarını yükler.  

  Ekleyebileceğiniz başka Windows PE paketleri de bulunur. Önyükleme görüntüsüne ekleyebileceğiniz isteğe bağlı bileşenler hakkında daha fazla bilgi için bkz. [WinPE: paket ekleme (Isteğe bağlı bileşenler başvurusu)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

> [!NOTE]
>Eklediğiniz araçları içeren özelleştirilmiş bir önyükleme görüntüsünden WinPE ile açılış yaptığınızda, WinPE’den bir komut satırı açabilir ve çalıştırmak için aracın dosya adını yazabilirsiniz. Bu araçların konumu otomatik olarak yol değişkenine eklenir. Komut istemi yalnızca önyükleme görüntüsü özelliklerindeki **Özelleştirme** sekmesinde **komut desteğini etkinleştir (yalnızca test)** ayarı seçiliyse eklenebilir.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Windows PE 5 kullanan önyükleme görüntüsünü özelleştirme  
 Windows PE 5 kullanan bir önyükleme görüntüsünü özelleştirmek için, Windows ADK yüklemeniz ve DISM komut satırı aracını kullanarak önyükleme görüntüsünü bağlamanız, isteğe bağlı bileşenleri ve sürücüleri eklemeniz ve değişiklikleri önyükleme görüntüsüne kaydetmeniz gerekir. Önyükleme görüntüsünü özelleştirmek için aşağıdaki yordamı izleyin.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Windows PE 5 kullanan bir önyükleme görüntüsünü özelleştirmek için  

1. Windows ADK 'yi, Windows AIK veya Windows ADK 'nin başka bir sürümüne sahip olmayan ve yüklü Configuration Manager bileşeni olmayan bir bilgisayara yükler.  

2. [Microsoft İndirme Merkezi](https://www.microsoft.com/download/details.aspx?id=39982)'nden Windows 8.1 için Windows ADK’yi indirin.  

3. Önyükleme görüntüsünü (wimpe. wim) Windows ADK yükleme klasöründen (örneğin, <*yükleme yolu*> \Windows Kits \\ < *sürümü*> \Assessment and Deployment Kit\Windows önyükleme ortamı \\ < *x86 veya AMD64* > \\ < *locale*>), önyükleme görüntüsünü özelleştireceğiniz bilgisayardaki bir hedef klasöre kopyalayın. Bu yordamda hedef klasör adı olarak C:\WinPEWAIK kullanılmıştır.  

4. Önyükleme görüntüsünü yerel bir Windows PE klasörüne bağlamak için DISM’yi kullanın. Örneğin, aşağıdaki komut satırını yazın:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Burada C:\WinPEWAIK önyükleme görüntüsünü içeren klasör ve C:\WinPEMount ise bağlanan klasördür.  

   > [!NOTE]
   >  Daha fazla bilgi için bkz. [DISM (Dağıtım Görüntüsü Bakımı ve yönetimi) başvurusu](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

5. Önyükleme görüntüsünü bağladıktan sonra, isteğe bağlı bileşenleri önyükleme görüntüsüne eklemek için DISM'yi kullanın. Windows PE 5'de 64 bit isteğe bağlı bileşenler <*Yükleme yolu*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs konumunda bulunur.  

   > [!NOTE]
   >  Bu yordam isteğe bağlı bileşenler için şu konumu kullanır: C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs. Sizin kullandığınız yol, kullandığınız sürüme ve Windows ADK için belirlediğiniz yükleme seçeneklerine bağlı olarak farklı olabilir.  

    İsteğe bağlı bileşenleri yüklemek için aşağıdakileri yazın:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<yerel ayar\>* **\WinPE-SecureStartup_** *<yerel ayar\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<yerel ayar\>* **\WinPE-WMI_** *<yerel ayar\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<yerel ayar\>* **\WinPE-Scripting** *<yerel ayar\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<yerel ayar\>* **\WinPE-WDS-Tools_** *<yerel ayar\>* **.cab"**  

    C:\WinPEMount değeri bağlı klasördür ve yerel ayar da bileşenlerin yerel ayarıdır. Örneğin, **en-us** yereli için şunu yazarsınız:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

   > [!TIP]
   >  Önyükleme görüntüsüne ekleyebileceğiniz isteğe bağlı bileşenler hakkında daha fazla bilgi için, bkz. [WINDOWS PE Isteğe bağlı bileşenler başvurusu](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

6. Gerektiğinde önyükleme görüntüsüne belirli sürücüleri eklemek için DISM'yi kullanın. Önyükleme görüntüsüne sürücü eklemek için aşağıdakileri yazın:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *sürücü .inf dosyasının yolu* **>**  

    Burada C:\WinPEMount takma klasörüdür.  

7. Önyükleme görüntüsü dosyasının bağlantısını kesmek ve değişiklikleri uygulamak için aşağıdakileri yazın.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Burada C:\WinPEMount takma klasörüdür.  

8. Güncelleştirilmiş önyükleme görüntüsünü, görev dizilerinizde kullanılmak üzere kullanılabilir hale getirmek için Configuration Manager ekleyin. Güncelleştirilen önyükleme görüntüsünü içeri aktarmak için aşağıdaki adımları kullanın:  

   1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

   2. **Yazılım Kitaplığı** çalışma alanında **İşletim Sistemleri**'ni genişletin ve **Önyükleme Görüntüleri**'ne tıklayın.  

   3. Önyükleme Görüntüsü Ekleme Sihirbazı'nı başlatmak için **Oluştur** grubunun **Giriş** sekmesinde **Önyükleme Görüntüsü Ekle**'yi tıklatın.  

   4. **Veri Kaynağı** sayfasında aşağıdaki seçenekleri belirtin ve **İleri**'ye tıklayın.  

      - **Yol** kutusunda, güncelleştirilen önyükleme görüntüsü dosyasının yolunu belirtin. Belirtilen yol UNC biçiminde geçerli bir ağ yolu olmalıdır. Örneğin: **\\\\<** <em>sunucuadı</em> **>\\<** <em>winpewaık paylaşım</em> **> \Winpe.exe**.  

      - **Önyükleme Görüntüsü** açılan listesinden önyükleme görüntüsünü seçin. WIM dosyası birden çok önyükleme görüntüsü içeriyorsa her görüntü listelenir.  

   5. **Genel** sayfasında aşağıdaki seçenekleri belirtin ve **İleri**'yi tıklatın.  

      -   **Ad** kutusunda önyükleme görüntüsü için benzersiz adı belirtin.  

      -   **Sürüm** kutusunda önyükleme görüntüsü için sürüm numarasını belirtin.  

      -   **Açıklama** kutusunda önyükleme görüntüsünün nasıl kullanılacağı ile ilgili kısa bir açıklama belirtin.  

   6. Sihirbazı tamamlayın.  

9. Windows PE'de hata ayıklamak ve sorun gidermek için önyükleme görüntüsünde bir komut kabuğunu etkinleştirebilirsiniz. Komut kabuğunu etkinleştirmek için aşağıdaki adımları kullanın.  

   1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

   2. **Yazılım Kitaplığı** çalışma alanında **İşletim Sistemleri**'ni genişletin ve **Önyükleme Görüntüleri**'ne tıklayın.  

   3. Listede yeni önyükleme görüntüsünü bulun ve görüntünün paket kimliğini tanımlayın. Paket kimliğini önyükleme görüntüsünün **Görüntü Kimliği** sütununda bulabilirsiniz.  

   4. Bir komut isteminden, **wbemtest** yazarak Windows Yönetim Araçları Sınayıcısı'nı açın.  

   5. Ad alanında **\\\\<** <em>SMS sağlayıcısı bilgisayar</em> **> \root\sms\ Site_<** <em>sitekodu</em> yazın **>** ve sonra **Bağlan**' a tıklayın. **Namespace**  

   6. **Örnek Aç**’a tıklayın, **sms_bootimagepackage.packageID="<packageID\>"** yazın ve **Tamam**’a tıklayın. packageID için, 3. adımda tanımladığınız değeri girin.  

   7. **Nesne Yenile**'yi tıklatın ve sonra **Özellikler** bölmesinde **EnableLabShell**'i tıklatın.  

   8. **Özelliği Düzenle**'ye tıklayın, değeri **TRUE** olarak değiştirin ve **Özelliği Kaydet**'e tıklayın.  

   9. **Nesneyi Kaydet**'e tıklayın ve sonra Windows Yönetim Araçları Sınayıcısı'ndan çıkın.  

10. Önyükleme görüntüsünü bir görev dizisinde kullanabilmeniz için önce, önyükleme görüntüsünü dağıtım noktalarına, dağıtım noktası gruplarına veya dağıtım noktası gruplarıyla ilişkilendirilmiş koleksiyonlara dağıtmanız gerekir. Önyükleme görüntüsünü dağıtmak için aşağıdaki adımları izleyin.  

    1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

    2.  **Yazılım Kitaplığı** çalışma alanında **İşletim Sistemleri**'ni genişletin ve **Önyükleme Görüntüleri**'ne tıklayın.  

    3.  Adım 3'te tanımlanan önyükleme görüntüsüne tıklayın.  

    4.  **Giriş** sekmesinde, **Dağıtım** grubunda, **Dağıtım Noktalarını Güncelleştir**'i tıklatın.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Windows PE 3.1 kullanan önyükleme görüntüsünü özelleştirme  
 WinPE 3.1 kullanan bir önyükleme görüntüsünü özelleştirmek için, Windows AIK yüklemeniz, Windows 7 SP1 için Windows AIK ekini yüklemeniz ve DISM komut satırı aracını kullanarak önyükleme görüntüsünü bağlamanız, isteğe bağlı bileşenleri ve sürücüleri eklemeniz ve değişiklikleri önyükleme görüntüsüne kaydetmeniz gerekir. Önyükleme görüntüsünü özelleştirmek için aşağıdaki yordamı izleyin.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Windows PE 3.1 kullanan bir önyükleme görüntüsünü özelleştirmek için  

1. Windows AIK 'yi, Windows AIK veya Windows ADK 'nin başka bir sürümüne sahip olmayan ve yüklü Configuration Manager bileşeni olmayan bir bilgisayara yükler. Windows AIK'yi [Microsoft Yükleme Merkezi](https://www.microsoft.com/download/details.aspx?id=5753)'nden indirin.  

2. 1. Adım’daki bilgisayara Windows 7 SP1 için Windows AIK Eki’ni yükleyin. Windows 7 SP1 için Windows AIK Eki'ni [Microsoft İndirme Merkezi](https://www.microsoft.com/download/details.aspx?id=5188)'nden indirin.  

3. Önyükleme görüntüsünü (wimpe.wim) Windows AIK yükleme klasöründen (örneğin, <*YüklemeYolu*>\Windows AIK\Tools\PETools\amd64\\), önyükleme görüntüsünü özelleştireceğiniz bilgisayardaki bir klasöre kopyalayın. Bu yordamda klasör adı olarak C:\WinPEWAIK kullanılmıştır.  

4. Önyükleme görüntüsünü yerel bir Windows PE klasörüne bağlamak için DISM’yi kullanın. Örneğin, aşağıdaki komut satırını yazın:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Burada C:\WinPEWAIK önyükleme görüntüsünü içeren klasör ve C:\WinPEMount ise bağlanan klasördür.  

   > [!NOTE]
   > Daha fazla bilgi için bkz. [DISM (Dağıtım Görüntüsü Bakımı ve yönetimi) başvurusu](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

5. Önyükleme görüntüsünü bağladıktan sonra, isteğe bağlı bileşenleri önyükleme görüntüsüne eklemek için DISM'yi kullanın. Windows PE 3.1'de, örneğin, isteğe bağlı bileşenler <*YüklemeYolu*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\ konumunda bulunur.  

   > [!NOTE]
   >  Bu yordam isteğe bağlı bileşenler için şu konumu kullanır: C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs. Sizin kullandığınız yol, kullandığınız sürüme ve Windows AIK için belirlediğiniz yükleme seçeneklerine bağlı olarak farklı olabilir.  

    İsteğe bağlı bileşenleri yüklemek için aşağıdakileri yazın:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<yerel ayar\>* **\winpe-wmi_** *<yerel ayar\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<yerel ayar\>* **\winpe-scripting_** *<yerel ayar\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<yerel ayar\>* **\winpe-wds-tools_** *<yerel ayar\>* **.cab"**  

    C:\WinPEMount değeri bağlı klasördür ve yerel ayar da bileşenlerin yerel ayarıdır. Örneğin, **en-us** yereli için şunu yazarsınız:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

   > [!TIP]
   >  Önyükleme görüntüsüne ekleyebileceğiniz farklı paketler hakkında daha fazla bilgi için bkz. bir [WINDOWS PE görüntüsüne paket ekleme](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd799312(v=ws.10)).

6. Gerektiğinde önyükleme görüntüsüne belirli sürücüleri eklemek için DISM'yi kullanın. Gerekirse önyükleme görüntüsüne sürücü eklemek için aşağıdakileri yazın:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *sürücü .inf dosyasının yolu* **>**  

    Burada C:\WinPEMount takma klasörüdür.  

7. Önyükleme görüntüsü dosyasının bağlantısını kesmek ve değişiklikleri uygulamak için aşağıdakileri yazın.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Burada C:\WinPEMount takma klasörüdür.  

8. Güncelleştirilmiş önyükleme görüntüsünü, görev dizilerinizde kullanılmak üzere kullanılabilir hale getirmek için Configuration Manager ekleyin. Güncelleştirilen önyükleme görüntüsünü içeri aktarmak için aşağıdaki adımları kullanın:  

   1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

   2. **Yazılım Kitaplığı** çalışma alanında **İşletim Sistemleri**'ni genişletin ve **Önyükleme Görüntüleri**'ne tıklayın.  

   3. Önyükleme Görüntüsü Ekleme Sihirbazı'nı başlatmak için **Oluştur** grubunun **Giriş** sekmesinde **Önyükleme Görüntüsü Ekle**'yi tıklatın.  

   4. **Veri Kaynağı** sayfasında aşağıdaki seçenekleri belirtin ve **İleri**'ye tıklayın.  

      - **Yol** kutusunda, güncelleştirilen önyükleme görüntüsü dosyasının yolunu belirtin. Belirtilen yol UNC biçiminde geçerli bir ağ yolu olmalıdır. Örneğin: **\\\\<** <em>sunucuadı</em> **>\\<** <em>winpewaık paylaşım</em> **> \Winpe.exe**.  

      - **Önyükleme Görüntüsü** açılan listesinden önyükleme görüntüsünü seçin. WIM dosyası birden çok önyükleme görüntüsü içeriyorsa her görüntü listelenir.  

   5. **Genel** sayfasında aşağıdaki seçenekleri belirtin ve **İleri**'yi tıklatın.  

      -   **Ad** kutusunda önyükleme görüntüsü için benzersiz adı belirtin.  

      -   **Sürüm** kutusunda önyükleme görüntüsü için sürüm numarasını belirtin.  

      -   **Açıklama** kutusunda önyükleme görüntüsünün nasıl kullanılacağı ile ilgili kısa bir açıklama belirtin.  

   6. Sihirbazı tamamlayın.  

9. Windows PE'de hata ayıklamak ve sorun gidermek için önyükleme görüntüsünde bir komut kabuğunu etkinleştirebilirsiniz. Komut kabuğunu etkinleştirmek için aşağıdaki adımları kullanın.  

   1. Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

   2. **Yazılım Kitaplığı** çalışma alanında **İşletim Sistemleri**'ni genişletin ve **Önyükleme Görüntüleri**'ne tıklayın.  

   3. Listede yeni önyükleme görüntüsünü bulun ve görüntünün paket kimliğini tanımlayın. Paket kimliğini önyükleme görüntüsünün **Görüntü Kimliği** sütununda bulabilirsiniz.  

   4. Bir komut isteminden, **wbemtest** yazarak Windows Yönetim Araçları Sınayıcısı'nı açın.  

   5. Ad alanında **\\\\<** <em>SMS sağlayıcısı bilgisayar</em> **> \root\sms\ Site_<** <em>sitekodu</em> yazın **>** ve sonra **Bağlan**' a tıklayın. **Namespace**  

   6. **Örnek Aç**’a tıklayın, **sms_bootimagepackage.packageID="<packageID\>"** yazın ve **Tamam**’a tıklayın. packageID için, 3. adımda tanımladığınız değeri girin.  

   7. **Nesne Yenile**'yi tıklatın ve sonra **Özellikler** bölmesinde **EnableLabShell**'i tıklatın.  

   8. **Özelliği Düzenle**'ye tıklayın, değeri **TRUE** olarak değiştirin ve **Özelliği Kaydet**'e tıklayın.  

   9. **Nesneyi Kaydet**'e tıklayın ve sonra Windows Yönetim Araçları Sınayıcısı'ndan çıkın.  

10. Önyükleme görüntüsünü bir görev dizisinde kullanabilmeniz için önce, önyükleme görüntüsünü dağıtım noktalarına, dağıtım noktası gruplarına veya dağıtım noktası gruplarıyla ilişkilendirilmiş koleksiyonlara dağıtmanız gerekir. Önyükleme görüntüsünü dağıtmak için aşağıdaki adımları izleyin.  

    1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

    2.  **Yazılım Kitaplığı** çalışma alanında **İşletim Sistemleri**'ni genişletin ve **Önyükleme Görüntüleri**'ne tıklayın.  

    3.  Adım 3'te tanımlanan önyükleme görüntüsüne tıklayın.  

    4.  **Giriş** sekmesinde, **Dağıtım** grubunda, **Dağıtım Noktalarını Güncelleştir**'i tıklatın.  
