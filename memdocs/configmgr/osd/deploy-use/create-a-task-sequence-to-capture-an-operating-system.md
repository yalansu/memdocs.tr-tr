---
title: İşletim sistemini yakalamak için görev dizisi oluşturma
titleSuffix: Configuration Manager
description: Derleme ve yakalama görev dizisi, işletim sistemi ile birlikte belirli sürücü ve yazılım güncelleştirmelerini içerebilen bir başvuru bilgisayarı oluşturur.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 349ae2b8d574904d25f6f23bfb1707bb11df8af0
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125517"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>İşletim sistemini yakalamak için görev dizisi oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir işletim sistemini Configuration Manager bir bilgisayara dağıtmak için görev dizisi kullandığınızda, bilgisayar görev dizisinde belirttiğiniz işletim sistemi görüntüsünü yüklenir. İşletim sistemi görüntüsünü belirli sürücüleri, uygulamaları ve yazılım güncelleştirmelerini içerecek şekilde özelleştirebilirsiniz. Önce bir referans bilgisayar oluşturmak için derleme ve yakalama görev dizisini kullanın. Ardından bu Referans bilgisayarından işletim sistemi görüntüsünü yakalayın. Yakalamaya hazır bir başvuru bilgisayarınız zaten varsa, işletim sistemini yakalamak için özel bir görev dizisi oluşturun.

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a>Oluşturma ve yakalama görev dizisi hakkında

Oluşturma ve yakalama görev sırası:

- Referans bilgisayarı bölümler ve biçimlendirir
- İşletim sistemini yükleme
- Configuration Manager istemcisini yükleme
- Uygulamaları yükleme
- Yazılım güncelleştirmelerini uygular
- İşletim sistemini başvuru bilgisayarından yakalar

Uygulamalar gibi görev dizisiyle ilişkili paketler, oluşturma ve yakalama görev dizisini dağıtmadan önce dağıtım noktalarında kullanılabilir olmalıdır.

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a>Gereklilik

Bir işletim sistemini yüklemek için bir görev dizisi oluşturmadan önce, aşağıdaki bileşenlerin yerinde olduğundan emin olun:  

### <a name="required"></a>Gerekli

- [Önyükleme görüntüsü](../get-started/manage-boot-images.md)

- [İşletim sistemi görüntüsü](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>Gerekli (kullanılıyorsa)

- Başvuru bilgisayarında donanımı desteklemek için gerekli Windows sürücülerini içeren [sürücü paketleri](../get-started/manage-drivers.md) . Sürücüleri yönetmeye yönelik görev dizisi adımları hakkında daha fazla bilgi için bkz. [Use task sequences to install device drivers](../get-started/manage-drivers.md#BKMK_TSDrivers).

- [Yazılım güncelleştirmeleri](../../sum/get-started/synchronize-software-updates.md)

- [Uygulamalar](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> Oluşturma ve yakalama görev dizisi oluşturma

Bir başvuru bilgisayarı oluşturmak ve işletim sistemini yakalamak için bir görev dizisi kullanmak üzere aşağıdaki yordamı kullanın.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

1. Şerit **giriş** sekmesinde, **Oluştur** grubunda, görev sırası oluşturma Sihirbazı 'Nı başlatmak için **görev sırası oluştur** ' u seçin.  

1. **Yeni Görev Sırası Oluştur** sayfasında **Başvuru işletim sistemi yansıması oluştur ve yakala**öğesini seçin.  

1. **Görev sırası bilgileri** sayfasında, aşağıdaki ayarları belirtin:  

    - **Görev dizisi adı**: Görev dizisini tanımlayan adı belirtin.  

    - **Açıklama**: görev dizisi için isteğe bağlı bir açıklama belirtin. Örneğin, görev dizisinin oluşturduğu işletim sistemini tanıtın.

    - **Önyükleme görüntüsü**: Bu görev dizisiyle kullanılacak önyükleme görüntüsünü belirtin.  

        > [!IMPORTANT]  
        > Önyükleme görüntüsü, hedef bilgisayarın donanım mimarisiyle uyumlu olmalıdır.  

1. Windows 'u **yükler** sayfasında, aşağıdaki ayarları belirtin:  

    - **Görüntü paketi**: işletim sistemini yüklemek için gerekli dosyaları içeren işletim sistemi görüntü paketini belirtin.  

    - **Görüntü dizini**: görüntüde yüklenecek işletim sisteminin dizinini belirtin. İşletim sistemi görüntüsü birden çok sürüm içeriyorsa yüklemek istediğiniz sürümü seçin.  

    - **Ürün anahtarı**: gerekirse, Windows işletim sisteminin yüklemesi için ürün anahtarını belirtin. Kodlanmış toplu lisans anahtarlarını ve standart ürün anahtarlarını belirtebilirsiniz. Kodsuz bir ürün anahtarı kullanırsanız, beş karakterlik her bir grubu tireyle ( `-` ) ayırın. Örnek: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Sunucu Lisanslama modu**: gerekirse, sunucu lisansının **bilgisayar** **başına, sunucu başına**olduğunu veya hiçbir lisansın belirtilolmadığını belirtin. Sunucu lisansı **Sunucu başına**ise maksimum sunucu bağlantısı sayısını da belirtin.  

    - Dağıtılan işletim sistemi için yönetici hesabının nasıl yapılandırılacağını belirtin:  

        - **Yerel yönetici parolasını rastgele oluştur ve tüm desteklenen platformlarda hesabı devre dışı bırak**: yerel yönetici hesabı için rastgele bir parola oluşturun. Windows ayarlandığında hesabı devre dışı bırakın.

        - **Hesabı etkinleştirin ve yerel yönetici parolasını belirtin**: Bu işletim sistemini dağıttığınız tüm bilgisayarlarda yerel yönetici hesabı için aynı parolayı kullanın.

1. **Ağı Yapılandır** sayfasında, aşağıdaki ayarları belirtin:

    - **Çalışma grubuna katıl**: işletim sistemi dağıtıldığında hedef bilgisayarın bir çalışma grubuna eklenip eklenmeyeceğini belirtin.  

    - **Etki alanına katılarak**: işletim sistemi dağıtıldığında hedef bilgisayarın bir etki alanına eklenip eklenmeyeceğini belirtin. **Etki Alanı**'nda etki alanının adını belirtin.  

        > [!IMPORTANT]  
        > Yerel ormandaki etki alanlarını bulmak için tarama yapabilirsiniz. Uzak orman için etki alanı adını belirtin.

        Kuruluş birimini (OU) de belirtebilirsiniz. Bu ayar isteğe bağlıdır ve henüz yoksa bilgisayar hesabının oluşturulacağı OU 'nun LDAP X. 500 ayırt edici adını belirtir.  

    - **Hesap**: Belirtilen etki alanına katılmak üzere izinlere sahip olan hesap için kullanıcı adını ve parolayı belirtin. Örneğin: `domain\user` veya `%variable%` .  

        > [!IMPORTANT]  
        > Dağıtım sırasında etki alanı ayarlarını ya da çalışma grubu ayarlarını geçirmeyi planlıyorsanız, uygun etki alanı kimlik bilgilerini buraya girdiğinizden emin olun.  

1. **Configuration Manager yüklemeyi** , Configuration Manager istemci paketini belirtin. Bu paket, Configuration Manager istemcisini yüklemek için kaynak dosyaları içerir. Ayrıca, istemciyi yüklemek için gereken ek özellikleri de belirtin.  

    Daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../core/clients/deploy/about-client-installation-properties.md).

1. **Güncelleştirmeleri dahil et** sayfasında, gerekli yazılım güncelleştirmelerinin, tüm yazılım güncelleştirmelerinin mi yükleneceğini, yoksa yazılım güncelleştirmelerinin mi yükleneceğini belirtin. Yazılım güncelleştirmelerini yüklemeyi belirtirseniz Configuration Manager, yalnızca hedef bilgisayarın üyesi olduğu koleksiyonları hedefleyen yazılım güncelleştirmelerini yükler.  

1. **Uygulamaları yüklemek** sayfasında, hedef bilgisayara yüklenecek uygulamaları belirtin. Birden çok uygulamayı belirlerseniz, belirli bir uygulamanın yüklemesinin başarısız olmasına karşı, görev dizisinin devam etmesini de belirtebilirsiniz.  

    > [!NOTE]
    > Sihirbazın yanında **Sistem Hazırlama** sayfası görüntülenir, ancak artık kullanılmamaktadır. Devam etmek için **İleri** seçeneğini belirleyin.

1. **Görüntü özellikleri** sayfasında işletim sistemi görüntüsü için aşağıdaki ayarları belirtin:

    - **Oluşturan**: işletim sistemi görüntüsünü oluşturan kullanıcının adını belirtin.  

    - **Sürüm**: işletim sistemi görüntüsüyle ilişkili sürüm numaranızı belirtin. Site bu değeri ayrı olarak depoladığından, bu özniteliğin işletim sistemi sürümü olması gerekmez.

    - **Açıklama**: işletim sistemi görüntüsünün açıklamasını belirtin.  

1. **Görüntü yakala** sayfasında, aşağıdaki ayarları belirtin:

    - **Yol**: Configuration Manager çıkış görüntü dosyasını (. wim) depolayacağı bir paylaşılan ağ klasörü belirtin. Bu dosya, bu sihirbazda belirttiğiniz ayarlara bağlı olarak işletim sistemi görüntüsünü içerir. Var olan bir klasörü belirtirseniz. WıM dosyası, üzerine yazılır.  

    - **Hesap**: Görüntünün depolandığı ağ paylaşımı için izinlere sahip Windows hesabını belirtin.  

1. Sihirbazı tamamlayın.  

Görev dizisine ek adımlar eklemek için, seçin ve **Düzenle**' yi seçin. Bir görev dizisinin nasıl düzenleneceği hakkında daha fazla bilgi için bkz. [görev dizisi düzenleyicisini kullanma](../understand/task-sequence-editor.md).  

Görev dizisini aşağıdaki yollardan biriyle dağıtın başvuru bilgisayarına dağıtın:  

- Referans bilgisayar zaten bir Configuration Manager istemcidir, derleme ve yakalama görev dizisini referans bilgisayarı içeren bir koleksiyona dağıtın. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).

- Referans bilgisayar bir Configuration Manager istemcisi değilse veya görev dizisini başvuru bilgisayarında elle çalıştırmak istiyorsanız, önyüklenebilir medya oluşturmak için **görev sırası medyası oluşturma Sihirbazı 'nı** kullanın. Daha fazla bilgi için bkz. [önyüklenebilir medya oluşturma](create-bootable-media.md).  

Görüntüyü yakaladıktan sonra, diğer bilgisayarlara dağıtabilirsiniz. Yakalanan işletim sistemi görüntüsünün nasıl dağıtılacağı hakkında daha fazla bilgi için bkz. bir [işletim sistemi yüklemek için görev dizisi oluşturma](create-a-task-sequence-to-install-an-operating-system.md).  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a>Var olan bir başvuru bilgisayarından yakala

Yakalamaya hazırsanız bir referans Bilgisayarınız zaten varsa, yalnızca başvuru bilgisayarından işletim sistemini yakalayan bir görev dizisi oluşturun. Bir başvuru bilgisayarından bir veya daha fazla görüntü yakalamak ve bunları belirtilen ağ paylaşımındaki bir görüntü dosyasına (. wim) depolamak için **Işletim sistemi görüntüsünü yakala** görev dizisi adımını kullanın. Windows PE 'de başvuru bilgisayarını Önyükleme görüntüsüyle başlatın. Görev dizisi, başvuru bilgisayarındaki her sabit sürücüyü. wim dosyası içinde ayrı bir görüntü olarak yakalar. Başvurulan bilgisayarda birden çok sürücü varsa, elde edilen. wim dosyası her birim için ayrı bir görüntü içerir. Yalnızca NTFS veya FAT32 olarak biçimlendirilen birimleri yakalar. Diğer biçimlere veya USB birimlerine sahip birimleri atlar.  

Var olan bir başvuru bilgisayarından işletim sistemi görüntüsü yakalamak için aşağıdaki yordamı kullanın:

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası oluştur**' u seçin. Bu eylem görev sırası oluşturma Sihirbazı 'Nı başlatır.  

1. **Yeni Görev Sırası Oluştur** sayfasında **Yeni bir özel görev sırası oluştur**öğesini seçin.  

1. **Görev sırası bilgileri** sayfasında, görev sırası için bir ad belirtin. İsteğe bağlı olarak, görev dizisi için bir açıklama ekleyin.  

1. Görev dizisi için bir önyükleme görüntüsü belirtin. Configuration Manager, başvuru bilgisayarını Windows PE ile başlatmak için bu önyükleme görüntüsünü kullanır. Daha fazla bilgi için bkz. [önyükleme görüntülerini yönetme](../get-started/manage-boot-images.md).  

1. Sihirbazı tamamlayın.  

1. **Görev dizileri** düğümünde yeni görev sırasını seçin. Ardından, şeridin **giriş** sekmesinde, **görev dizisi** grubunda **Düzenle**' yi seçin. Bu eylem, görev sırası düzenleyicisini açar.  

1. Configuration Manager istemcisi başvuru bilgisayarında yüklüyse:

    **Ekle** menüsüne gidin, **görüntüler**' i seçin ve ardından [ConfigMgr istemcisini yakalama için hazırla](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)' yı seçin. Bu adım başvuru bilgisayarındaki Configuration Manager istemcisini genelleştirir.

    > [!Note]  
    > Görev sırası Configuration Manager istemcisinin kaldırılmasını desteklemez.

1. **Ekle** menüsüne gidin, **görüntüler**' i seçin ve Windows 'u [yakalama için hazırla](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture)' yı seçin. Bu adım Sysprep 'i çalıştırır ve ardından bilgisayarı görev sırası için belirtilen Windows PE önyükleme görüntüsü ile yeniden başlatır. Bu eylemin başarıyla tamamlanabilmesi için referans bilgisayarı bir etki alanına katın.

1. **Ekle** menüsüne gidin, **görüntüler**' i seçin ve [işletim sistemi görüntüsünü yakala](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)' yı seçin. Bu adım, başvuru bilgisayarındaki sabit sürücüleri yakalamak için yalnızca Windows PE 'den çalışır. Aşağıdaki ayarları yapılandırın:

    - **Ad** ve **Açıklama**: İsteğe bağlı olarak, görev dizisi adımının adını değiştirebilir ve bir açıklama belirtebilirsiniz.  

    - **Hedef**: output .WIM dosyasının depolandığı bir paylaşılan ağ klasörü belirtin. Bu dosya, bu Sihirbazı kullanarak belirttiğiniz ayarlara dayanan işletim sistemi görüntüsünü içerir. Var olan bir klasörü belirtirseniz. WıM dosyası, üzerine yazılır.  

    - **Açıklama**, **Sürüm**ve **oluşturan**: isteğe bağlı olarak, yakalanacak görüntüyle ilgili ayrıntıları sağlayın.  

    - **İşletim sistemi görüntü hesabını yakala**: Belirttiğiniz ağ paylaşımı için izinlere sahip Windows hesabını belirtin. Bu Windows hesabının adını belirtmek için **Ayarla** ' yı seçin.  

Değişikliklerinizi kaydetmek için **Tamam** ' ı seçin ve görev sırası düzenleyicisini kapatın.  

Görev dizisini aşağıdaki yollardan biriyle dağıtın başvuru bilgisayarına dağıtın:  

- Referans bilgisayar zaten bir Configuration Manager istemcidir, yakalama görev sırasını referans bilgisayarı içeren bir koleksiyona dağıtın. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).

- Referans bilgisayar bir Configuration Manager istemcisi değilse veya görev dizisini başvuru bilgisayarında el ile çalıştırmak istiyorsanız, yakalama medyası oluşturmak için **görev sırası medyası oluşturma Sihirbazı 'nı** kullanın. Daha fazla bilgi için bkz. [yakalama medyası oluşturma](create-capture-media.md).  

Görüntüyü yakaladıktan sonra, diğer bilgisayarlara dağıtabilirsiniz. Yakalanan işletim sistemi görüntüsünün nasıl dağıtılacağı hakkında daha fazla bilgi için bkz. bir [işletim sistemi yüklemek için görev dizisi oluşturma](create-a-task-sequence-to-install-an-operating-system.md).

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a>Örnek görev dizisi

Bir işletim sistemi görüntüsü oluşturup yakalayan bir görev dizisi oluştururken kılavuz olarak aşağıdaki tabloyu kullanın. Tablo, görev dizisi adımlarınız için genel sıralama ve bu adımları mantıksal gruplar halinde nasıl düzenleyip yapılandıracağınıza karar vermenize yardımcı olur. Oluşturduğunuz görev dizisi bu örnekten farklı olabilir. Daha fazla veya daha az adım ve grup içerebilir.

> [!NOTE]  
> Bu tür bir görev dizisi oluşturmak için her zaman Görev Dizisi Oluşturma Sihirbazı’nı kullanın.
>
> Sihirbaz, aynı adımları el ile eklediğinizde daha az farklı adlarla görev dizisine adımlar ekler.

### <a name="group-build-the-reference-machine"></a>Grup: başvuru makinesini oluşturun

Bu grup bir başvuru bilgisayarı oluşturmak için gerekli işlemleri içerir.

|Görev sırası adımı|Açıklama|  
|-------------------------------|---------------|  
|**Windows PE'de yeniden başlat**|Hedef bilgisayarı görev dizisine atanan önyükleme görüntüsüne yeniden başlatın. Bu adım, kullanıcıya yüklemenin devam edebilmesi için bilgisayarın yeniden başlatıldığını belirten bir ileti görüntüler.<br /><br />Bu adım salt okunurdur `_SMSTSInWinPE` görev dizisi değişkenini kullanır. İlişkili değer eşitse `false` , görev sırası adımı devam eder.|
|**Diski Bölümle 0 - BIOS**|Hedef bilgisayardaki sabit sürücüyü BIOS modunda bölümleyip biçimlendirin. Varsayılan disk numarası `0` .<br /><br />Bu adım birkaç salt okunurdur görev dizisi değişkenini kullanır. Örneğin, yalnızca Configuration Manager istemci önbelleği yoksa ve bilgisayar UEFı için yapılandırılmışsa çalışır.|
|**Diski Bölümle 0 - UEFI**|Hedef bilgisayardaki sabit sürücüyü UEFı modunda bölümleyip biçimlendirin. Varsayılan disk numarası `0` .<br /><br />Bu adım birkaç salt okunurdur görev dizisi değişkenini kullanır. Örneğin, yalnızca Configuration Manager istemci önbelleği yoksa çalışır ve yalnızca bilgisayar UEFı için yapılandırılmışsa çalışır.|
|**İşletim Sistemini Uygula**|Belirtilen işletim sistemi görüntüsünü hedef bilgisayara yükler. Bu adım öncelikle birimdeki Configuration Manager özgü denetim dosyalarından başka tüm dosyaları siler. Ardından, WıM dosyasında bulunan tüm birim görüntülerini hedef bilgisayarda karşılık gelen sıralı disk birimine uygular.|
|**Windows Ayarlarını Uygula**|Hedef bilgisayar için Windows ayarlarını yapılandırın.|
|**Ağ Ayarlarını Uygula**|Hedef bilgisayar için ağ veya çalışma grubu yapılandırma bilgilerini belirtin.|
|**Aygıt Sürücülerini Uygula**|Bu işletim sistemi dağıtımının bir parçası olarak sürücüleri eşleştirin ve yükler. Daha fazla bilgi için, bkz. [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).<br /><br />Bu adım salt okunurdur `_SMSTSMediaType` görev dizisi değişkenini kullanır. İlişkili değer eşit değilse `FullMedia` , bu adım çalıştırılmaz.|
|**Windows 'u ve Configuration Manager ayarlama**|Configuration Manager istemci yazılımını yükler. Configuration Manager, Configuration Manager istemci GUID 'sini yükleyip kaydeder. Gerekli **yükleme özelliklerini**ekleyin.|
|**Güncelleştirmeleri yükler**|Yazılım güncelleştirmelerinin hedef bilgisayara nasıl yükleneceğini belirtin. Hedef bilgisayar, bu adım çalıştırılıncaya kadar ilgili yazılım güncelleştirmeleri için değerlendirilmez. Bu noktada, değerlendirme diğer Configuration Manager yönetilen tüm istemcilere benzer. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini yükler](../understand/install-software-updates.md).<br /><br />Bu adım salt okunurdur `_SMSTSMediaType` görev dizisi değişkenini kullanır. İlişkili değer eşit değilse `FullMedia` , bu adım çalıştırılmaz.|
|**Uygulamaları yükler**|Referans bilgisayara yüklenecek uygulamaları belirtir.|

### <a name="group-capture-the-reference-machine"></a>Grup: başvuru makinesini yakala

Bu grup bir başvuru bilgisayarını hazırlamak ve yakalamak için gerekli adımları içerir.

|Görev sırası adımı|Açıklama|  
|-------------------------------|---------------|  
|**Configuration Manager Istemcisini hazırla**|Başvuru bilgisayarında Configuration Manager istemcisini genelleştirin.|
|**İşletim sistemini hazırla**|Windows 'un genelleştirçalışacağı Sysprep 'ı çalıştırır. Ardından, bilgisayarı görev sırası için belirtilen Windows PE önyükleme görüntüsüne yeniden başlatır.|
|**Başvuru Makinesini Yakala**|Görüntüyü belirtilen ağ paylaşımında ve olarak yakalar. WıM dosyası.|

> [!IMPORTANT]
> Referans bilgisayardan bir görüntü yakaladıktan sonra, Referans bilgisayarından başka bir işletim sistemi görüntüsü yakalamayın. Kayıt defteri girdileri ilk yapılandırma sırasında oluşturulur. İşletim sistemi görüntüsünü her yakaladığınızda yeni bir referans bilgisayarı oluşturun. Sonraki işletim sistemi görüntülerini oluşturmak için aynı referans bilgisayarını kullanmayı planlıyorsanız, önce Configuration Manager istemcisini kaldırın ve yeniden yükleyin.

## <a name="next-steps"></a>Sonraki adımlar

[Kurumsal işletim sistemlerini dağıtma yöntemleri](methods-to-deploy-enterprise-operating-systems.md)
