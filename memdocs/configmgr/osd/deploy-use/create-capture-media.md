---
title: Yakalama ortamı oluşturma
titleSuffix: Configuration Manager
description: Bir başvuru bilgisayarından işletim sistemi görüntüsü yakalamak için Configuration Manager yakalama medyasını kullanın.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbbec355356a74d61f263fe2b16d44c0cd15ba80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711150"
---
# <a name="create-capture-media"></a>Yakalama ortamı oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager medya yakala, bir referans bilgisayarından işletim sistemi görüntüsü yakalamanızı sağlar. Yakalama medyası, başvuru bilgisayarını Başlatan önyükleme görüntüsünü ve işletim sistemi görüntüsünü yakalayan görev dizisini içerir. [İşletim sistemini yakalamak için bir görev dizisi oluşturmak](create-a-task-sequence-to-capture-an-operating-system.md)üzere senaryo için yakalama medyasını kullanın.  


## <a name="prerequisites"></a>Önkoşullar

Görev sırası medyası oluşturma Sihirbazı 'Nı kullanarak yakalama medyası oluşturmadan önce, tüm bu koşulların karşılandığından emin olun.

### <a name="boot-image"></a>Önyükleme görüntüsü

İşletim sistemini dağıtmak için görev dizisinde kullandığınız önyükleme görüntüsü hakkında aşağıdaki noktaları göz önünde bulundurun:

- Önyükleme görüntüsünün mimarisi hedef bilgisayarın mimarisine uygun olmalıdır. Örneğin, bir x64 hedef bilgisayar, x86 veya x64 önyükleme görüntüsünü başlatabilir ve çalıştırabilir. Ancak, bir x86 hedef bilgisayar yalnızca x86 önyükleme görüntüsünü başlatabilir ve çalıştırabilir.
- Önyükleme görüntüsünün, hedef bilgisayarı sağlamak için gereken ağ ve depolama sürücülerini içerdiğinden emin olun.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Görev dizisiyle ilişkili tüm içeriği dağıtma

Görev dizisinin gerektirdiği tüm içeriği en az bir dağıtım noktasına dağıtın. Bu içerik önyükleme görüntüsünü, işletim sistemi görüntüsünü ve diğer ilişkili dosyaları içerir. Sihirbaz, yakalama medyası oluşturduğunda dağıtım noktasından içeriği toplar.

Kullanıcı hesabınızın, bu dağıtım noktasındaki içerik kitaplığı için en azından **okuma** erişimi hakları olması gerekir. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Çıkarılabilir USB sürücüyü hazırlama

Çıkarılabilir bir USB sürücü kullanıyorsanız, bu sürücüyü görev sırası medyası oluşturma Sihirbazı 'nı çalıştırdığınız bilgisayara bağlayın. USB sürücünün Windows tarafından bir kaldırma aygıtı olarak algılanabilmesi gerekir. Sihirbaz medya oluştururken doğrudan USB sürücüye yazar.

### <a name="create-an-output-folder"></a>Bir çıkış klasörü oluşturun

Bir CD veya DVD seti için medya oluşturmak üzere görev sırası medyası oluşturma Sihirbazı 'Nı çalıştırmadan önce, oluşturduğu çıktı dosyaları için bir klasör oluşturun. CD veya DVD seti için oluşturduğu medya bir olarak yazılmıştır. ISO dosyasını doğrudan klasörde.


## <a name="process"></a>İşleme

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası medyası oluştur**' u seçin. Bu eylem, görev sırası medyası oluşturma Sihirbazı 'Nı başlatır.  

3. **Medya türü seçin** sayfasında, **yakalama medyası**' nı seçin.  

4. **Medya türü** sayfasında, medyanın **çıkarılabilir bir USB sürücüsü** mi yoksa bir **CD/DVD seti**mi olduğunu belirtin. Ardından, aşağıdaki seçenekleri yapılandırın:  

    > [!IMPORTANT]  
    > Medya bir FAT32 dosya sistemi kullanır. İçeriği, boyutu 4 GB 'ın üzerinde olan bir dosyayı içeren USB sürücüsünde medya oluşturamazsınız.  

    - **ÇıKARıLABILIR USB sürücü**' yi seçerseniz, içeriği depolamak istediğiniz sürücüyü seçin.  

        - **ÇıKARıLABILIR USB sürücüsünü (FAT32) biçimlendirin ve önyüklenebilir yapın**: varsayılan olarak, USB sürücüsünü hazırlamasına Configuration Manager. Daha yeni UEFı cihazlarının çoğu önyüklenebilir FAT32 bölümü gerektirir. Ancak, bu biçim dosyaların boyutunu ve sürücünün genel kapasitesini de sınırlar. Çıkarılabilir sürücüyü zaten biçimlendirdikten ve yapılandırdıysanız, bu seçeneği devre dışı bırakın.

    - **CD/DVD seti**' ni seçerseniz, medyanın kapasitesini (**medya boyutu**) ve çıkış dosyasının adını ve yolunu (**medya dosyası**) belirtin. Sihirbaz çıkış dosyalarını bu konuma yazar. Örneğin, `\\servername\folder\outputfile.iso`  

        Medyanın kapasitesi tüm içeriği depolayamayacak kadar küçükse, birden çok dosya oluşturur. Daha sonra içeriği birden fazla CD veya DVD 'de depolamanız gerekir. Birden çok medya dosyası gerektirdiğinde Configuration Manager, oluşturduğu her çıkış dosyasının adına bir sıra numarası ekler.  

        > [!IMPORTANT]  
        > Varolan bir .iso görüntüsünü seçerseniz, Görev Sırası Medyası Sihirbazı sonraki sayfaya geçtiğinizde hemen bu görüntüyü sürücüden veya paylaşımdan siler. Daha sonra sihirbazı iptal etseniz bile mevcut görüntü silinir.  

    - **Hazırlama klasörü**<!--1359388-->: Medya oluşturma işlemi çok sayıda geçici sürücü alanı gerektirebilir. Varsayılan olarak, bu konum şu yola benzer: `%UserProfile%\AppData\Local\Temp`. Sürüm 1902 ' den başlayarak, bu geçici dosyaları nerede depolayabileceğiniz konusunda daha fazla esneklik sağlamak için bu değeri başka bir sürücü ve yol olarak değiştirin.  

    - **Medya etiketi**<!--1359388-->: Sürüm 1902 ' den başlayarak, görev dizisi medyasına bir etiket ekleyin. Bu etiket, medyayı oluşturduktan sonra daha iyi tanımanıza yardımcı olur. Varsayılan değer: `Configuration Manager`. Bu metin alanı aşağıdaki konumlarda görünür:  

        - Bir ISO dosyası bağlarsanız, Windows bu etiketi bağlı sürücünün adı olarak görüntüler.  

        - USB sürücüsünü biçimlendirirseniz, etiketin adı olarak ilk 11 karakteri kullanır  

        - Configuration Manager, medyanın köküne adlı `MediaLabel.txt` bir metin dosyası yazar. Varsayılan olarak, dosya tek satırlık bir metin içerir: `label=Configuration Manager`. Medya için etiketi özelleştirirseniz, bu satır varsayılan değer yerine özel etiketinizi kullanır.  

    - **Medyaya Autorun. inf dosyasını dahil et**<!-- 4090666 -->: Sürüm 1906 ' den başlayarak Configuration Manager, varsayılan olarak Autorun. inf dosyası eklemez. Bu dosya genellikle kötü amaçlı yazılımdan koruma ürünleri tarafından engelleniyor. Windows 'un Otomatik Çalıştır özelliği hakkında daha fazla bilgi için bkz. [Autorun-Enabled CD-ROM uygulaması oluşturma](https://docs.microsoft.com/windows/desktop/shell/autoplay). Senaryonuz için hala gerekliyse, dosyayı eklemek için bu seçeneği belirleyin.  

5. **Önyükleme görüntüsü** sayfasında, aşağıdaki seçenekleri belirtin:  

    > [!IMPORTANT]  
    > Dağıttığınız önyükleme görüntüsünün mimarisi hedef bilgisayarın mimarisine uygun olmalıdır. Örneğin, bir x64 hedef bilgisayar, x86 veya x64 önyükleme görüntüsünü başlatabilir ve çalıştırabilir. Ancak, bir x86 hedef bilgisayar yalnızca x86 önyükleme görüntüsünü başlatabilir ve çalıştırabilir.  

    - **Önyükleme görüntüsü**: hedef bilgisayarı başlatmak için önyükleme görüntüsünü seçin.  

    - **Dağıtım noktası**: önyükleme görüntüsüne sahip olan dağıtım noktasını seçin. Sihirbaz önyükleme görüntüsünü dağıtım noktasından alır ve medyaya yazar.  

        > [!NOTE]  
        > Kullanıcı hesabınız, dağıtım noktasındaki içerik kitaplığı için en azından **okuma** izinlerine sahip olmalıdır.  

6. Sihirbazı tamamlayın.  


## <a name="next-steps"></a>Sonraki adımlar

[İşletim sistemini yakalamak için görev dizisi oluşturma](create-a-task-sequence-to-capture-an-operating-system.md)
