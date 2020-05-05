---
title: Görev dizisi ortamı için başlatma öncesi komutları
titleSuffix: Configuration Manager
description: Başlatma öncesi komutu için kullanmak üzere bir betik oluşturun, başlatma öncesi komutuyla ilişkili içeriği dağıtın ve medyada başlatma öncesi komutunu yapılandırın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9dd921d58e6ef777017af3e2eb24dbf4bd611fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717464"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>Configuration Manager 'de görev sırası medyası için başlatma öncesi komutları

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Önyükleme medyası, tek başına medya ve önceden hazırlanmış medya ile kullanmak üzere Configuration Manager ' de bir başlatma öncesi komutu oluşturabilirsiniz. Başlatma öncesi komutu, görev sırası seçilmeden önce çalışan ve Windows PE'de kullanıcıyla etkileşim kurabilen bir betik veya yürütülebilir bir dosyadır. Başlatma öncesi komutu kullanıcıdan bilgi isteyebilir ve görev sırası ortamına kaydedebilir veya bilgi için bir görev sırası değişkenini sorgulayabilir. Hedef bilgisayar önyükleme yaptığında, ilke, yönetim noktasından indirilmeden önce komut satırı çalıştırılır. Başlatma öncesi komutu için kullanmak üzere bir betik oluşturmak, başlatma öncesi komutuyla ilişkilendirilmiş içeriği dağıtmak ve medyada başlatma öncesi komutunu yapılandırmak için aşağıdaki yordamları kullanın.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Başlatma Öncesi Komutu için kullanmak üzere betik oluşturma  
 Görev dizisi değişkenleri, görev dizisi çalışırken Microsoft.SMS.TSEnvironment COM nesnesi kullanılarak okunabilir ve yazılabilir. Aşağıdaki örnekte, geçerli günlük konumunu almak üzere _SMSTSLogPath görev sırası değişkenini sorgulayan bir Visual Basic betik dosyası görülmektedir. Komut dosyası ayrıca özel bir değişken ayarlar.  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Betik Dosyası için Paket Oluşturma ve İçeriği Dağıtma  
 Başlatma öncesi komutu için betik veya yürütülebilir dosya oluşturduktan sonra, betik veya yürütülebilir dosyalarını barındıracak bir paket kaynağı oluşturmanız, dosyalar için bir paket oluşturmanız (program gerekmez) ve içeriği bir dağıtım noktasına dağıtmanız gerekir.  

 Paket oluşturma hakkında daha fazla bilgi için bkz. [paket ve programlar](../../apps/deploy-use/packages-and-programs.md).  

 İçerik dağıtma hakkında daha fazla bilgi için bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Medyadaki Başlatma Öncesi Komutunu Yapılandırma  
 Tek başına medya, önyüklenebilir medya veya önceden hazırlanmış medya için Görev Sırası Medyası Oluşturma Sihirbazı'nda bir başlatma öncesi komutu yapılandırabilirsiniz. Medya türleri hakkında daha fazla bilgi için bkz. [görev dizisi medyası oluşturma](../deploy-use/create-task-sequence-media.md). Medyada bir başlatma öncesi komutu oluşturmak için aşağıdaki yordamı kullanın.  

#### <a name="to-create-a-prestart-command-in-media"></a>Medyada bir başlatma öncesi komutu oluşturmak için  

1.  Configuration Manager konsolunda **Yazılım Kitaplığı**'nı tıklatın.  

2.  **Yazılım kitaplığı** çalışma alanında **işletim sistemleri**' ni genişletin ve **görev dizileri**' ne tıklayın.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, Görev Sırası Medyası Oluşturma Sihirbazı'nı başlatmak için **Görev Sırası Medyası Oluştur** 'u tıklatın.  

4.  **Medya Türü Seçin** sayfasında, **Tek başına medya**, **Önyüklenebilir medya**veya **Önhazırlığı yapılan medya**'yı seçin ve **İleri**'ye tıklayın.  

5.  Sihirbazın **Özelleştirme** sayfasına gidin. Sihirbazdaki diğer sayfaları yapılandırma hakkında daha fazla bilgi için bkz. [görev dizisi medyası oluşturma](../deploy-use/create-task-sequence-media.md).  

6.  **Özelleştirme** sayfasında, aşağıdaki bilgileri belirtin ve **İleri**'ye tıklayın.  

    -   **Başlatma öncesi komutunu etkinleştir**'i seçin.  

    -   **Komut satırı** metin kutusuna, başlatma öncesi komutu için oluşturduğunuz betiği veya yürütülebilir dosyayı girin.  

        > [!IMPORTANT]  
        >  Başlatma öncesi komutunu belirtmek için **cmd\> /c <başlatma öncesi komutunu** kullanın. Örneğin, başlatma öncesi komutunuzun betiği için TSScript.vbs adını kullandıysanız, komut satırı için **cmd /C TSScript.vbs** girersiniz. Buradaki **cmd /C** yeni bir Windows komut yorumlayıcı penceresi açar ve başlatma öncesi komut betiğini veya yürütülebilir dosyasını bulmak üzere Path ortam değişkenini kullanır. Ayrıca başlatma öncesi komutunun tam yolunu da belirtebilirsiniz, ancak sürücü harfi farklı sürücü yapılandırmalarına sahip bilgisayarlarda farklı olabilir.  

    -   **Başlatma öncesi komut için dosyaları ekle**'yi seçin.  

    -   Başlatma öncesi komutu dosyalarıyla ilişkili paketi seçmek için **Ayarla** 'yı seçin.  

    -   Başlatma öncesi komutunun içeriğini barındıran dağıtım noktasını seçmek için **Gözat** 'a tıklayın.  

7.  Sihirbazı tamamlayın.  
