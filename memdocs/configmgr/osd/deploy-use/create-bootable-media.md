---
title: Önyüklenebilir ortam oluşturma
titleSuffix: Configuration Manager
description: Windows 'un yeni bir sürümünü yüklemek veya bir bilgisayarı değiştirmek için Configuration Manager 'da önyüklenebilir medya kullanın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e18c5e9e029900e10cebfb8e7bcdee29fd928ba
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125415"
---
# <a name="create-bootable-media"></a>Önyüklenebilir ortam oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager 'da önyüklenebilir medya, önyükleme görüntüsünü, isteğe bağlı başlatma öncesi komutlarını ve ilişkili dosyaları ve Configuration Manager dosyaları içerir. Aşağıdaki işletim sistemi dağıtım senaryoları için önyüklenebilir medya kullanın:

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)

- [Mevcut bir bilgisayarı değiştirme ve ayarları aktarma](replace-an-existing-computer-and-transfer-settings.md)

## <a name="usage"></a>Kullanım

Önyüklenebilir medyaya önyükleme yaptığınızda aşağıdaki süreç gerçekleşir:

1. Hedef bilgisayar başlar

1. Ağa bağlanır

1. Siteden aşağıdaki içeriği alır:

    - Belirtilen görev sırası

    - İşletim sistemi görüntüsü

    - Diğer tüm gerekli içerikler

Görev sırası medyada olmadığından, medyayı yeniden oluşturmak zorunda kalmadan görev dizisini veya içeriği değiştirebilirsiniz.

Önyüklenebilir medyadaki paketler şifrelenmez. Paket içeriklerinin yetkisiz kullanıcılardan güvenli olduğundan emin olmak için, uygun güvenlik önlemleri alın. Örneğin, medyaya bir parola ekleyin.

Sürüm 2006 ' den başlayarak önyüklenebilir medya, bulut tabanlı içeriği indirebilir. Cihazın hala yönetim noktasına bir intranet bağlantısı olması gerekir. İçerik özellikli bir bulut yönetimi ağ geçidi (CMG) veya bulut dağıtım noktasından içerik alabilir.<!--6209223--> Daha fazla bilgi için bkz. [bulut tabanlı Içerik desteği](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

## <a name="prerequisites"></a>Ön koşullar

Görev sırası medyası oluşturma Sihirbazı 'Nı kullanarak önyüklenebilir medya oluşturmadan önce, tüm bu koşulların karşılandığından emin olun.

### <a name="boot-image"></a>Önyükleme görüntüsü

İşletim sistemini dağıtmak için görev dizisinde kullandığınız önyükleme görüntüsü hakkında aşağıdaki noktaları göz önünde bulundurun:

- Önyükleme görüntüsünün mimarisi hedef bilgisayarın mimarisine uygun olmalıdır. Örneğin, bir x64 hedef bilgisayar, x86 veya x64 önyükleme görüntüsünü başlatabilir ve çalıştırabilir. Ancak, bir x86 hedef bilgisayar yalnızca x86 önyükleme görüntüsünü başlatabilir ve çalıştırabilir.
- Önyükleme görüntüsünün, hedef bilgisayarı sağlamak için gereken ağ ve depolama sürücülerini içerdiğinden emin olun.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>İşletim sistemini dağıtmak için görev dizisi oluşturma

Önyüklenebilir medyanın bir parçası olarak işletim sistemini dağıtmak için görev dizisini belirtin. Daha fazla bilgi için bkz. bir [işletim sistemi yüklemek için görev dizisi oluşturma](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Görev dizisiyle ilişkili tüm içeriği dağıtma

Görev dizisinin gerektirdiği tüm içeriği en az bir dağıtım noktasına dağıtın. Bu içerik önyükleme görüntüsünü ve diğer ilişkili başlatma öncesi dosyalarını içerir. Sihirbaz önyüklenebilir medyayı oluşturduğunda dağıtım noktasından içeriği toplar.

Kullanıcı hesabınızın, bu dağıtım noktasındaki içerik kitaplığı için en azından **okuma** erişimi hakları olması gerekir. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Çıkarılabilir USB sürücüyü hazırlama

Çıkarılabilir bir USB sürücü kullanıyorsanız, bu sürücüyü görev sırası medyası oluşturma Sihirbazı 'nı çalıştırdığınız bilgisayara bağlayın. USB sürücünün Windows tarafından bir kaldırma aygıtı olarak algılanabilmesi gerekir. Sihirbaz medya oluştururken doğrudan USB sürücüye yazar.

### <a name="create-an-output-folder"></a>Bir çıkış klasörü oluşturun

Bir CD veya DVD seti için medya oluşturmak üzere görev sırası medyası oluşturma Sihirbazı 'Nı çalıştırmadan önce, oluşturduğu çıktı dosyaları için bir klasör oluşturun. CD veya DVD seti için oluşturduğu medya bir olarak yazılmıştır. ISO dosyasını doğrudan klasörde.

## <a name="process"></a>İşlem

> [!NOTE]
> PKI ortamları için birincil sitede kök sertifika yetkilisini (CA) belirttikten sonra, birincil sitede önyüklenebilir medyayı seçtiğinizden emin olun. Merkezi Yönetim sitesi (CAS), önyüklenebilir medyayı düzgün şekilde oluşturmak için kök CA bilgilerine sahip değildir.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin.

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası medyası oluştur**' u seçin. Bu eylem, görev sırası medyası oluşturma Sihirbazı 'Nı başlatır.

1. **Medya türü seçin** sayfasında, aşağıdaki seçenekleri belirtin:

    - **Önyüklenebilir medya**'yı seçin.

    - İsteğe bağlı olarak, yalnızca IŞLETIM sisteminin kullanıcı girişi gerektirmeden dağıtılmasını istiyorsanız **Katılımsız işletim sistemi dağıtımına Izin ver**' i seçin.

        > [!IMPORTANT]
        > Bu seçeneği belirlediğinizde, kullanıcıya ağ yapılandırma bilgileri veya isteğe bağlı görev dizileri sorulmaz. Medyayı parola koruması için yapılandırırsanız, kullanıcıdan bir parola istenir.

1. **Medya yönetimi** sayfasında, aşağıdaki seçeneklerden birini belirtin:

    - **Dinamik medya**: bir yönetim noktasının, medyayı site sınırlarındaki istemci konumuna bağlı olarak başka bir yönetim noktasına yönlendirmesine izin verin.

    - **Site tabanlı medya**: medya yalnızca belirtilen yönetim noktasıyla iletişim kurar.

1. **Medya türü** sayfasında, medyanın **çıkarılabilir bir USB sürücüsü** mi yoksa bir **CD/DVD seti**mi olduğunu belirtin. Ardından, aşağıdaki seçenekleri yapılandırın:

    > [!IMPORTANT]
    > Medya bir FAT32 dosya sistemi kullanır. İçeriği, boyutu 4 GB 'ın üzerinde olan bir dosyayı içeren USB sürücüsünde medya oluşturamazsınız.

    - **ÇıKARıLABILIR USB sürücü**' yi seçerseniz, içeriği depolamak istediğiniz sürücüyü seçin.

        - **ÇıKARıLABILIR USB sürücüsünü (FAT32) biçimlendirin ve önyüklenebilir yapın**: varsayılan olarak, USB sürücüsünü hazırlamasına Configuration Manager. Daha yeni UEFı cihazlarının çoğu önyüklenebilir FAT32 bölümü gerektirir. Ancak, bu biçim dosyaların boyutunu ve sürücünün genel kapasitesini de sınırlar. Çıkarılabilir sürücüyü zaten biçimlendirdikten ve yapılandırdıysanız, bu seçeneği devre dışı bırakın.

    - **CD/DVD seti**' ni seçerseniz, medyanın kapasitesini (**medya boyutu**) ve çıkış dosyasının adını ve yolunu (**medya dosyası**) belirtin. Sihirbaz çıkış dosyalarını bu konuma yazar. Örnek: `\\servername\folder\outputfile.iso`

        Medyanın kapasitesi tüm içeriği depolayamayacak kadar küçükse, birden çok dosya oluşturur. Daha sonra içeriği birden fazla CD veya DVD 'de depolamanız gerekir. Birden çok medya dosyası gerektirdiğinde Configuration Manager, oluşturduğu her çıkış dosyasının adına bir sıra numarası ekler.

        > [!IMPORTANT]
        > Varolan bir .iso görüntüsünü seçerseniz, Görev Sırası Medyası Sihirbazı sonraki sayfaya geçtiğinizde hemen bu görüntüyü sürücüden veya paylaşımdan siler. Daha sonra sihirbazı iptal etseniz bile mevcut görüntü silinir.

    - **Hazırlama klasörü**<!--1359388-->: Medya oluşturma işlemi çok daha geçici sürücü alanı gerektirebilir. Varsayılan olarak, bu konum şu yola benzer: `%UserProfile%\AppData\Local\Temp` . Bu geçici dosyaları nerede depolayabileceğiniz konusunda daha fazla esneklik sağlamak için bu değeri başka bir sürücü ve yol olarak değiştirebilirsiniz.

    - **Medya etiketi**<!--1359388-->: Görev sırası medyasına bir etiket ekleyin. Bu etiket, medyayı oluşturduktan sonra daha iyi tanımanıza yardımcı olur. Varsayılan değer: `Configuration Manager`. Bu metin alanı aşağıdaki konumlarda görünür:

        - Bir ISO dosyası bağlarsanız, Windows bu etiketi bağlı sürücünün adı olarak görüntüler.

        - USB sürücüsünü biçimlendirirseniz, etiket adı olarak etiketin ilk 11 karakterini kullanır.

        - Configuration Manager, medyanın köküne adlı bir metin dosyası yazar `MediaLabel.txt` . Varsayılan olarak, dosya tek satırlık bir metin içerir: `label=Configuration Manager` . Medya için etiketi özelleştirirseniz, bu satır varsayılan değer yerine özel etiketinizi kullanır.

    - **Medyaya Autorun. inf dosyasını dahil et**<!-- 4090666 -->: Sürüm 1906 ' den başlayarak Configuration Manager, varsayılan olarak Autorun. inf dosyası eklemez. Bu dosya genellikle kötü amaçlı yazılımdan koruma ürünleri tarafından engelleniyor. Windows 'un Otomatik Çalıştır özelliği hakkında daha fazla bilgi için bkz. [Autorun-Enabled CD-ROM uygulaması oluşturma](https://docs.microsoft.com/windows/desktop/shell/autoplay). Senaryonuz için hala gerekliyse, dosyayı eklemek için bu seçeneği belirleyin.

1. **Güvenlik** sayfasında, aşağıdaki seçenekleri belirtin:

    - **Bilinmeyen bilgisayar desteğini etkinleştir**: medyanın, Configuration Manager tarafından yönetilmeyen bir bilgisayara işletim sistemi dağıtmasına izin verin. Configuration Manager veritabanında bu bilgisayarların kaydı yoktur. Daha fazla bilgi için bkz. [bilinmeyen bilgisayar dağıtımları Için hazırlanma](../get-started/prepare-for-unknown-computer-deployments.md).

    - **Medyayı parolayla koru**: medyanın yetkisiz erişimlerden korunmasına yardımcı olmak için güçlü bir parola girin. Parola belirtirseniz kullanıcının önyüklenebilir medyayı kullanabilmesi için o parolayı girmesi gerekir.

        > [!IMPORTANT]
        > En iyi güvenlik uygulaması olarak, önyüklenebilir medyayı korumaya yardımcı olmak için her zaman parola atayın.

    - HTTP iletişimleri için, **otomatik olarak imzalanan medya sertifikası oluştur**' u seçin. Ardından, sertifika için başlangıç ve sona erme tarihi belirtin.

        > [!NOTE]
        > Bu seçeneği belirlerseniz, bu sihirbazın **önyükleme görüntüsü** sayfasında HERHANGI bir HTTPS yönetim noktası seçemezsiniz.

    - HTTPS iletişimleri için, **PKI sertifikasını Içeri aktar**' ı seçin. Ardından İçeri aktarılacak sertifikayı ve parolasını belirtin.

        Önyükleme görüntülerinin kullandığı bu istemci sertifikası hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../core/plan-design/network/pki-certificate-requirements.md).

    - **Kullanıcı cihaz benzeşimi**: Configuration Manager Kullanıcı merkezli yönetimi desteklemek için, medyanın kullanıcıları hedef bilgisayarla nasıl ilişkilendirmesini istediğinizi belirtin. İşletim sistemi dağıtımının Kullanıcı cihaz benzeşimini nasıl desteklediği hakkında daha fazla bilgi için bkz. [kullanıcıları bir hedef bilgisayarla ilişkilendirme](../get-started/associate-users-with-a-destination-computer.md).

        - **Kullanıcı cihaz benzeşimine otomatik onay Ile Izin ver**: medya kullanıcıları hedef bilgisayarla otomatik olarak ilişkilendirir. Bu işlev, işletim sistemini dağıtan görev sırasının eylemlerine bağlıdır. Bu senaryoda görev sırası, işletim sistemini hedef bilgisayara dağıtırken belirtilen kullanıcılar ve hedef bilgisayar arasında bir ilişki oluşturur.

        - **Kullanıcı cihaz benzeşimi bekleyen yönetici onayına Izin ver**: medya, onay verildikten sonra kullanıcıları hedef bilgisayarla ilişkilendirir. Bu işlev, işletim sistemini dağıtan görev dizisinin kapsamını temel alır. Bu senaryoda, görev sırası belirtilen kullanıcılar ve hedef bilgisayar arasında bir ilişki oluşturur. Daha sonra, işletim sistemini dağıtmadan önce yönetici kullanıcıdan onay bekler.

        - **Kullanıcı cihaz benzeşimine izin verme**: medya, kullanıcıları hedef bilgisayarla ilişkilendirmez. Bu senaryoda, görev sırası, işletim sistemini dağıtırken kullanıcıları hedef bilgisayarla ilişkilendirmez.

1. **Önyükleme görüntüsü** sayfasında, aşağıdaki seçenekleri belirtin:

    > [!IMPORTANT]
    > Dağıttığınız önyükleme görüntüsünün mimarisi hedef bilgisayarın mimarisine uygun olmalıdır. Örneğin, bir x64 hedef bilgisayar, x86 veya x64 önyükleme görüntüsünü başlatabilir ve çalıştırabilir. Ancak, bir x86 hedef bilgisayar yalnızca x86 önyükleme görüntüsünü başlatabilir ve çalıştırabilir.

    - **Önyükleme görüntüsü**: hedef bilgisayarı başlatmak için önyükleme görüntüsünü seçin.

    - **Dağıtım noktası**: önyükleme görüntüsüne sahip olan dağıtım noktasını seçin. Sihirbaz önyükleme görüntüsünü dağıtım noktasından alır ve medyaya yazar.

        > [!NOTE]
        > Kullanıcı hesabınız, dağıtım noktasındaki içerik kitaplığı için en azından **okuma** izinlerine sahip olmalıdır.

    - **Yönetim noktası**: yalnızca *Site tabanlı medya*için birincil siteden bir yönetim noktası seçin.

    - **İlişkili yönetim noktaları**: yalnızca *dinamik medya*için, kullanılacak birincil site yönetim noktalarını ve ilk iletişim için öncelik sırasını seçin.

        > [!NOTE]
        > Bu sihirbazın **güvenlik** SAYFASıNDA bir PKI sertifikası belirttiğinizde, Bu sayfa yalnızca https etkin yönetim noktalarını görüntüler.

1. **Özelleştirme** sayfasında, aşağıdaki seçenekleri belirtin:

    - Görev dizisinin kullandığı tüm değişkenleri ekleyin.

    - **Başlatma öncesi komutunu etkinleştir**: görev dizisi çalışmadan önce çalıştırmak istediğiniz başlatma öncesi komutlarını belirtin. Başlatma öncesi komutlar, görev dizisi çalıştırılmadan önce Windows PE 'de kullanıcıyla etkileşime girebilen bir betik veya yürütülebilir dosyadır. Daha fazla bilgi için bkz. [görev dizisi medyası Için başlatma öncesi komutları](../understand/prestart-commands-for-task-sequence-media.md).

        > [!TIP]
        > Medya oluşturma sırasında, görev sırası değişkenlerinin değeri de dahil olmak üzere paket KIMLIĞINI ve başlatma öncesi komut satırını, Configuration Manager konsolunu çalıştıran bilgisayardaki **CreateTsMedia. log** dosyasına yazar. Görev dizisi değişkenlerinin değerini doğrulamak için bu günlük dosyasını inceleyebilirsiniz.

        Başlatma öncesi komutu herhangi bir içerik gerektiriyorsa, **başlatma öncesi komutu için dosya ekleme**seçeneğini belirleyin.

1. Sihirbazı tamamlayın.

## <a name="alternate-method"></a>Alternatif Yöntem

Sürücü, Configuration Manager konsolunu çalıştıran bilgisayara bağlı olmadığında, çıkarılabilir bir USB sürücüde önyüklenebilir medya oluşturabilirsiniz.

1. [Görev dizisi önyükleme medyasını oluşturun](#process). **Medya türü** sayfasında **CD/DVD kümesi**' ni seçin. Sihirbaz, çıktı dosyalarını belirttiğiniz konuma yazar. Örneğin: `\\servername\folder\outputfile.iso`.  

1. Çıkarılabilir USB sürücüyü hazırlayın. Sürücü biçimlendirilmelidir, boş ve önyüklenebilir olmalıdır.

1. Share konumundan ISO bağlama yapın ve dosyaları ISO 'dan USB sürücüsüne aktarın.

## <a name="next-steps"></a>Sonraki adımlar

[Windows’u ağ üzerinden dağıtmak için önyüklenebilir ortam kullanma](use-bootable-media-to-deploy-windows-over-the-network.md)  
