---
title: İşletim sistemi görüntülerini yönetme
titleSuffix: Configuration Manager
description: Windows resim (WıM) dosyalarında depolanan işletim sistemi görüntülerini yönetme yöntemlerini öğrenin.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 190a203494cecfd28c198197f3a582adff745265
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724121"
---
# <a name="manage-os-images-with-configuration-manager"></a>Configuration Manager ile işletim sistemi görüntülerini yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager işletim sistemi görüntüleri Windows görüntü (WıM) dosya biçiminde depolanır. Bu görüntüler, bir bilgisayara yeni bir işletim sistemi yüklemek ve yapılandırmak için kullanılan başvuru dosya ve klasörlerinin sıkıştırılmış bir koleksiyonudur. Birçok işletim sistemi dağıtım senaryosu bir işletim sistemi görüntüsü gerektirir.


## <a name="os-image-types"></a>İşletim sistemi görüntü türleri

[Varsayılan bir işletim sistemi görüntüsünü](#default-image)kullanabilir veya yapılandırdığınız bir [başvuru bilgisayarından](#bkmk_capture) işletim sistemi görüntüsünü oluşturabilirsiniz. Referans bilgisayarı oluştururken işletim sistemi dosyalarını, sürücüleri, destek dosyalarını, yazılım güncelleştirmelerini, araçları ve uygulamaları işletim sistemine eklersiniz. Daha sonra görüntü dosyasını oluşturmak için bunu yakalarsınız.

### <a name="default-image"></a>Varsayılan görüntü

Windows yükleme dosyaları varsayılan işletim sistemi görüntüsünü içerir. Bu görüntü, standart bir sürücü kümesi içeren temel bir işletim sistemi görüntüsüdür. Varsayılan işletim sistemi görüntüsünü kullandığınızda, görev dizisi adımlarını kullanarak uygulamaları yükler ve işletim sistemi bir cihaza yükledikten sonra diğer yapılandırma işlemleri yapın. Windows kaynak dosyalarında varsayılan işletim sistemi görüntüsünü bulun: `\Sources\install.wim`.  

#### <a name="default-image-advantages"></a>Varsayılan görüntü avantajları

- Görüntü boyutu yakalanan görüntüden daha küçüktür.  

- Görev dizisi adımlarıyla uygulama ve yapılandırmaların yüklenmesi daha dinamik bir görevdir. Örneğin, cihaz yeniden görüntüsüne gerek kalmadan, görev dizisinde yüklenen yapılandırma ve uygulamaları değiştirin.  

#### <a name="default-image-disadvantages"></a>Varsayılan görüntü dezavantajları

- İşletim sistemi yüklemesi daha uzun sürebilir. Uygulama yüklemesi ve diğer yapılandırma işlemleri, işletim sistemi yüklemesi tamamlandıktan sonra oluşur.  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a>Referans bilgisayarından yakalanan görüntü

Özelleştirilmiş bir işletim sistemi görüntüsü oluşturmak için, istenen IŞLETIM sistemiyle bir başvuru bilgisayarı oluşturun. Ardından uygulamaları yükleyip ayarları yapılandırın. WıM dosyasını oluşturmak için başvuru bilgisayarından işletim sistemi görüntüsünü yakalayın. Referans bilgisayarı el ile oluşturun veya derleme adımlarının bazılarını veya tümünü otomatikleştirmek için bir görev dizisi kullanın. Daha fazla bilgi için bkz. [OS görüntülerini özelleştirme](customize-operating-system-images.md).  

#### <a name="captured-image-advantages"></a>Yakalanan görüntü avantajları

- Yükleme varsayılan görüntünün kullanılmasından daha hızlı olabilir. Örneğin, uygulamalar yakalanan işletim sistemi görüntüsüyle önceden yüklenebilir. Daha sonra görev dizisi adımlarını kullanarak bu uygulamaları daha sonra yüklemeniz gerekmez.  

#### <a name="captured-image-disadvantages"></a>Yakalanan görüntü dezavantajları

- Görüntü boyutu, varsayılan görüntüden daha büyük olabilir.  

- Uygulamalar ve araçlar için güncelleştirmeler gerektiğinde yeni bir görüntü oluşturmanız gerekir.  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a>Bir işletim sistemi görüntüsü ekleme  

Bir işletim sistemi görüntüsü kullanabilmeniz için, Configuration Manager sitenize ekleyin.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **işletim sistemi görüntüleri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **işletim sistemi görüntüsü Ekle**' yi seçin. Bu eylem, Işletim sistemi görüntüsü ekleme Sihirbazı 'Nı başlatır.  

3. **Veri kaynağı** sayfasında, aşağıdaki bilgileri belirtin:

    - İşletim sistemi görüntü dosyasının ağ **yolu** . Örneğin, `\\server\share\path\image.wim`.

    - **BELIRTILEN WIM dosyasından belirli bir görüntü dizinini ayıklayın** ve ardından listeden bir görüntü dizini seçin.<!--3719699--> Sürüm 1902 ' den başlayarak, bu seçenek dosyadaki tüm görüntü dizinleri yerine otomatik olarak tek bir dizin aktarır. Bu seçeneğin kullanılması, daha küçük bir görüntü dosyası ve daha hızlı çevrimdışı bakım ile sonuçlanır. Ayrıca, yazılım güncelleştirmelerini uyguladıktan sonra küçük bir görüntü dosyası için [görüntü bakımını iyileştirme](#bkmk_resetbase)işlemini destekler.  

        > [!Note]  
        > Configuration Manager kaynak görüntü dosyasını değiştirmez. Aynı kaynak dizinde yeni bir görüntü dosyası oluşturur.
        >
        > Bu ayıklama işlemi, örneğin 60 GB üzerinde çok büyük görüntü dosyaları için başarısız olabilir. DıSM hatası, Configuration Manager `Not enough storage is available to process this command.` kullanımı, Smsprov. log ve DISM. log dosyasında yer alan komut satırdır. Aynı komutu el ile çalıştırın ve ardından görüntüyü içeri aktarın.<!-- SCCMDocs-pr issue 3502 -->  

    - Sürüm 1906 ' den başlayarak, bir istemcideki içeriği önceden önbelleğe almak istiyorsanız görüntünün **mimarisini** ve **dilini** belirtin. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../deploy-use/configure-precache-content.md).<!--4224642-->  

4. **Genel** sayfasında, aşağıdaki bilgileri belirtin. Bu bilgiler, birden fazla işletim sistemi görüntüsü olduğunda tanımlama amaçları için yararlıdır.  

    - **Ad**: görüntü için benzersiz bir ad. Varsayılan olarak, ad WıM dosya adından gelir.  

    - **Sürüm**: isteğe bağlı bir sürüm tanımlayıcısı. Bu özelliğin görüntünün işletim sistemi sürümü olması gerekmez. Bu, genellikle kuruluşunuzun paketinin sürümüdür.  

    - **Açıklama**: isteğe bağlı kısa bir açıklama.  

5. Sihirbazı tamamlayın.  

Bu konsol Sihirbazı 'nın PowerShell cmdlet 'inin eşdeğeri için, bkz. [New-CMOperatingSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps).

Sonra, işletim sistemi görüntüsünü dağıtım noktalarına dağıtın.  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a>İçeriği dağıtım noktalarına dağıtma  

İşletim sistemi görüntülerini, diğer içerikle aynı şekilde dağıtım noktalarına dağıtın. Görev dizisini dağıtmadan önce, işletim sistemi görüntüsünü en az bir dağıtım noktasına dağıtın. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a>İşletim sistemi görüntüsünü çok noktaya yayın dağıtımları için hazırlama  

Birden fazla bilgisayarın aynı anda bir işletim sistemi görüntüsünü indirmesini sağlamak için çok noktaya yayın dağıtımlarını kullanın. Görüntü, her istemci dağıtım noktasından ayrı bir bağlantı üzerinden bir görüntünün kopyasını indirmek yerine dağıtım noktası tarafından istemcilere çok noktaya yayın yapılır. [Windows 'u ağ üzerinden dağıtmak için çok noktaya yayın kullanmak](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)üzere işletim sistemi dağıtım yöntemini seçtiğinizde, işletim sistemi görüntüsünü çok noktaya yayını destekleyecek şekilde yapılandırın. Sonra görüntüyü çok noktaya yayın özellikli bir dağıtım noktasına dağıtın.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **işletim sistemi görüntüleri** düğümünü seçin.  

2. Çok noktaya yayın özellikli bir dağıtım noktasına dağıtmak istediğiniz işletim sistemi görüntüsünü seçin.  

3. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

4. **Dağıtım ayarları** sekmesine geçin ve aşağıdaki seçenekleri yapılandırın:  

    - **Bu paketin çok noktaya yayın üzerinden aktarılmasına Izin ver (yalnızca WinPE)**: çok noktaya yayın kullanarak işletim sistemi görüntülerini eşzamanlı olarak dağıtmak üzere Configuration Manager için bu seçeneği belirleyin.  

    - **Çok noktaya yayın paketlerini şifreleme**: sitenin dağıtım noktasına gönderilmeden önce görüntünün şifrelenip şifrelenmeyeceğini belirtin. Görüntü hassas bilgiler içeriyorsa, bu seçeneği kullanın. Görüntü şifrelenmemişse, içeriği ağda şifresiz metin halinde görünür. Ardından, yetkisiz bir Kullanıcı görüntü içeriğini ele geçirebilir ve görüntüleyebilir.  

    - **Bu paketi yalnızca çok noktaya yayın üzerinden aktar**: Dağıtım noktasının görüntüyü yalnızca çok noktaya yayın oturumu sırasında dağıtmasını isteyip istemediğinizi belirtin.  

         **Bu paketi yalnızca çok noktaya yayın üzerinden aktar**' ı seçerseniz, **çalışan görev dizisi için gerektiğinde Içeriği yerel olarak indirmek**için görev sırası dağıtım seçeneğini de belirtmeniz gerekir. Daha fazla bilgi için, bkz. [Deploy a task sequence](../deploy-use/deploy-a-task-sequence.md).  

5. Ayarları kaydetmek ve görüntü özelliklerini kapatmak için **Tamam** ' ı seçin.  
