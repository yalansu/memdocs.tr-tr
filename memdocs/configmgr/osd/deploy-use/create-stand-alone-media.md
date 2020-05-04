---
title: Tek başına medya oluşturma
titleSuffix: Configuration Manager
description: İşletim sistemini ağ bağlantısı olmadan bir bilgisayara dağıtmak için tek başına medya kullanın.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e477d08ed97fe46bbe51b62a0ed024d437c2626
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711010"
---
# <a name="create-stand-alone-media"></a>Tek başına medya oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager tek başına medya, işletim sistemini ağ bağlantısı olmadan bir bilgisayara dağıtmak için gereken her şeyi içerir.

Aşağıdaki işletim sistemi dağıtım senaryolarında tek başına medya kullanın:  

- [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Yeni bir bilgisayara yeni bir Windows sürümünü yükleme (tam)](install-new-windows-version-new-computer-bare-metal.md)  

- [Windows’u en yeni sürüme yükseltme](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>Kullanım

Tek başına medya, işletim sistemini ve diğer tüm gerekli içeriği yüklemeye yönelik adımları otomatikleştiren görev dizisini içerir. Bu içerik önyükleme görüntüsünü, işletim sistemi görüntüsünü ve cihaz sürücülerini içerir. Tek başına medya işletim sistemini dağıtmak için her şeyi depoladığından, diğer medya türleri için gerekenden daha fazla disk alanı gerektirir.

Bir merkezi yönetim sitesinde tek başına medya oluşturduğunuzda, istemci, atanan site kodunu Active Directory alır. Alt sitelerde oluşturulan tek başına medya, bu sitenin site kodunu istemciye otomatik olarak atar.  


## <a name="prerequisites"></a>Önkoşullar

Görev sırası medyası oluşturma Sihirbazı 'Nı kullanarak tek başına medya oluşturmadan önce, tüm bu koşulların karşılandığından emin olun.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>İşletim sistemini dağıtmak için görev dizisi oluşturma

Tek başına medyanın bir parçası olarak işletim sistemini dağıtmak için görev dizisini belirtin. Daha fazla bilgi için bkz. bir [işletim sistemi yüklemek için görev dizisi oluşturma](create-a-task-sequence-to-install-an-operating-system.md).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Tek başına medya için desteklenmeyen eylemler

Tek başına medya için aşağıdaki eylemler desteklenmez:

- Görev dizisindeki [sürücüleri otomatik olarak Uygula](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) adımı. Tek başına medya, sürücü kataloğundan cihaz sürücülerinin otomatik uygulamasını desteklemez. Windows Kurulumu belirli bir sürücü kümesini kullanılabilir hale getirmek için [sürücü paketini Uygula](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) adımını kullanın.  

- Görev dizisindeki [paket Içeriğini indir](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) adımı. Yönetim noktası bilgileri tek başına medyada mevcut değildir, bu nedenle adım içerik konumlarını numaralandırmaya çalışırken başarısız olur.  

- Yazılım güncelleştirmelerinin yüklenmesi.  

- İşletim sistemini dağıtmaya başlamadan önce yazılım yükleme.  

- İşletim sistemi dışındaki dağıtımlar için özel görev dizileri.  

- Kullanıcı cihaz benzeşimini desteklemek için kullanıcılar ile hedef bilgisayarın ilişkilendirilmesi.  

- Dinamik paket, [paketleri yükleme](../understand/task-sequence-steps.md#BKMK_InstallPackage) adımı aracılığıyla yüklenir.  

- Dinamik uygulama, [uygulama yükleme](../understand/task-sequence-steps.md#BKMK_InstallApplication) adımı aracılığıyla yüklenir.

- **Windows 'u ve ConfigMgr 'Yi Kur** görev dizisi adımında **kullanılabilir olduğunda ön üretim istemci paketini kullan** ayarı. Bu ayar hakkında daha fazla bilgi için bkz. [Windows ve ConfigMgr kurulumu](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> Görev diziniz [paketi Kur](../understand/task-sequence-steps.md#BKMK_InstallPackage) adımını içeriyorsa ve tek başına medyayı merkezi yönetim sitesinde oluşturursanız bir hata oluşabilir. Merkezi Yönetim sitesi gerekli istemci yapılandırma ilkelerine sahip değildir. Bu ilkeler, görev sırası çalıştırıldığında yazılım dağıtım Aracısı 'nı etkinleştirmek için gereklidir. **CreateTsMedia. log** dosyasında aşağıdaki hata görünebilir:  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> **Paketi yüklemeyi** içeren tek başına medya için, tek başına medyayı yazılım dağıtım Aracısı etkinleştirilmiş bir birincil sitede oluşturun.
>
> Alternatif olarak, özel [komut satırı Çalıştır](../understand/task-sequence-steps.md#BKMK_RunCommandLine) adımını kullanın. [Windows 'u ve ConfigMgr 'Yi Kur](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) adımından sonra ve Ilk **paket yükleme** adımından önce ekleyin. **Komut satırını Çalıştır** adımı, Ilk paketi Kur adımından önce yazılım dağıtım aracısını etkinleştirmek IÇIN aşağıdaki WMIC komutunu çalıştırır:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Görev dizisiyle ilişkili tüm içeriği dağıtma

Görev dizisinin gerektirdiği tüm içeriği en az bir dağıtım noktasına dağıtın. Bu içerik önyükleme görüntüsünü, işletim sistemi görüntüsünü ve diğer ilişkili dosyaları içerir. Sihirbaz, medyayı oluşturduğunda dağıtım noktasından içeriği toplar.

Kullanıcı hesabınızın, bu dağıtım noktasındaki içerik kitaplığı için en azından **okuma** erişimi hakları olması gerekir. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Çıkarılabilir USB sürücüyü hazırlama

Çıkarılabilir bir USB sürücü kullanıyorsanız, bu sürücüyü görev sırası medyası oluşturma Sihirbazı 'nı çalıştırdığınız bilgisayara bağlayın. USB sürücünün Windows tarafından bir kaldırma aygıtı olarak algılanabilmesi gerekir. Sihirbaz medya oluştururken doğrudan USB sürücüye yazar.

Tek başına medya FAT32 dosya sistemini kullanır. İçeriği, boyutu 4 GB 'ın üzerinde olan bir dosyayı içeren çıkarılabilir USB sürücüsünde tek başına medya oluşturamazsınız.

### <a name="create-an-output-folder"></a>Bir çıkış klasörü oluşturun

Bir CD veya DVD seti için medya oluşturmak üzere görev sırası medyası oluşturma Sihirbazı 'Nı çalıştırmadan önce, oluşturduğu çıktı dosyaları için bir klasör oluşturun. CD veya DVD seti için oluşturduğu medya bir olarak yazılmıştır. ISO dosyasını doğrudan klasörde.


## <a name="process"></a>İşleme

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası medyası oluştur**' u seçin. Bu eylem, görev sırası medyası oluşturma Sihirbazı 'Nı başlatır.  

3. **Medya türü seçin** sayfasında, aşağıdaki seçenekleri belirtin:  

    - **Tek başına medya**' yı seçin.  

    - İsteğe bağlı olarak, yalnızca IŞLETIM sisteminin kullanıcı girişi gerektirmeden dağıtılmasını istiyorsanız **Katılımsız işletim sistemi dağıtımına Izin ver**' i seçin.  

        > [!IMPORTANT]  
        > Bu seçeneği belirlediğinizde, kullanıcıya ağ yapılandırma bilgileri veya isteğe bağlı görev dizileri sorulmaz. Medyayı parola koruması için yapılandırırsanız, kullanıcıdan bir parola istenir.  

4. **Medya türü** sayfasında, medyanın **çıkarılabilir bir USB sürücüsü** mi yoksa bir **CD/DVD seti**mi olduğunu belirtin. Ardından, aşağıdaki seçenekleri yapılandırın:  

    > [!IMPORTANT]  
    > Medya bir FAT32 dosya sistemi kullanır. İçeriği, boyutu 4 GB 'ın üzerinde olan bir dosyayı içeren USB sürücüsünde medya oluşturamazsınız.  

    - **ÇıKARıLABILIR USB sürücü**' yi seçerseniz, içeriği depolamak istediğiniz sürücüyü seçin.  

        - **ÇıKARıLABILIR USB sürücüsünü (FAT32) biçimlendirin ve önyüklenebilir yapın**: varsayılan olarak, USB sürücüsünü hazırlamasına Configuration Manager. Daha yeni UEFı cihazlarının çoğu önyüklenebilir FAT32 bölümü gerektirir. Ancak, bu biçim dosyaların boyutunu ve sürücünün genel kapasitesini de sınırlar. Çıkarılabilir sürücüyü zaten biçimlendirdikten ve yapılandırdıysanız, bu seçeneği devre dışı bırakın.

    - **CD/DVD seti**' ni seçerseniz, medyanın kapasitesini (**medya boyutu**) ve çıkış dosyasının adını ve yolunu (**medya dosyası**) belirtin. Sihirbaz çıkış dosyalarını bu konuma yazar. Örneğin, `\\servername\folder\outputfile.iso`  

        Medyanın kapasitesi tüm içeriği depolayamayacak kadar küçükse, birden çok dosya oluşturur. Daha sonra içeriği birden fazla CD veya DVD 'de depolamanız gerekir. Birden çok medya dosyası gerektirdiğinde Configuration Manager, oluşturduğu her çıkış dosyasının adına bir sıra numarası ekler.  

        Bir uygulamayı işletim sistemi ile birlikte dağıtırsanız ve uygulama tek bir medyaya sığmayacak Configuration Manager, uygulamayı birden çok medyaya depolar. Tek başına medya çalıştırıldığında, Configuration Manager kullanıcıdan uygulamanın depolandığı sonraki medyayı ister.  

        > [!IMPORTANT]  
        > Varolan bir .iso görüntüsünü seçerseniz, Görev Sırası Medyası Sihirbazı sonraki sayfaya geçtiğinizde hemen bu görüntüyü sürücüden veya paylaşımdan siler. Daha sonra sihirbazı iptal etseniz bile mevcut görüntü silinir.  

    - **Hazırlama klasörü**<!--1359388-->: Medya oluşturma işlemi çok sayıda geçici sürücü alanı gerektirebilir. Varsayılan olarak, bu konum şu yola benzer: `%UserProfile%\AppData\Local\Temp`. Sürüm 1902 ' den başlayarak, bu geçici dosyaları nerede depolayabileceğiniz konusunda daha fazla esneklik sağlamak için bu değeri başka bir sürücü ve yol olarak değiştirin.  

    - **Medya etiketi**<!--1359388-->: Sürüm 1902 ' den başlayarak, görev dizisi medyasına bir etiket ekleyin. Bu etiket, medyayı oluşturduktan sonra daha iyi tanımanıza yardımcı olur. Varsayılan değer: `Configuration Manager`. Bu metin alanı aşağıdaki konumlarda görünür:  

        - Bir ISO dosyası bağlarsanız, Windows bu etiketi bağlı sürücünün adı olarak görüntüler.  

        - USB sürücüsünü biçimlendirirseniz, etiketin adı olarak ilk 11 karakteri kullanır  

        - Configuration Manager, medyanın köküne adlı `MediaLabel.txt` bir metin dosyası yazar. Varsayılan olarak, dosya tek satırlık bir metin içerir: `label=Configuration Manager`. Medya için etiketi özelleştirirseniz, bu satır varsayılan değer yerine özel etiketinizi kullanır.  

    - **Medyaya Autorun. inf dosyasını dahil et**<!-- 4090666 -->: Sürüm 1906 ' den başlayarak Configuration Manager, varsayılan olarak Autorun. inf dosyası eklemez. Bu dosya genellikle kötü amaçlı yazılımdan koruma ürünleri tarafından engelleniyor. Windows 'un Otomatik Çalıştır özelliği hakkında daha fazla bilgi için bkz. [Autorun-Enabled CD-ROM uygulaması oluşturma](https://docs.microsoft.com/windows/desktop/shell/autoplay). Senaryonuz için hala gerekliyse, dosyayı eklemek için bu seçeneği belirleyin.  

5. **Güvenlik** sayfasında, aşağıdaki seçenekleri belirtin:

    - **Medyayı parolayla koru**: medyanın yetkisiz erişimlerden korunmasına yardımcı olmak için güçlü bir parola girin. Bir parola belirttiğinizde, kullanıcının medyayı kullanabilmesi için bu parolayı sağlaması gerekir.  

        > [!IMPORTANT]  
        > En iyi güvenlik uygulaması olarak, medyayı korumaya yardımcı olmak için her zaman bir parola atayın.  
        >
        > Tek başına medyada, yalnızca görev dizisi adımlarını ve değişkenlerini şifreler. Medyanın kalan içeriğini şifrelemez. Görev dizisi betiklerine herhangi bir hassas bilgi eklemeyin. Tüm hassas bilgileri, görev dizisi değişkenlerini kullanarak depolayın ve uygulayın.  

    - **Bu tek başına medyanın geçerli olması için tarih aralığı seçin**: medyada isteğe bağlı başlangıç ve sona erme tarihlerini ayarlayın. Bu ayar varsayılan olarak devre dışıdır. Tarihler, tek başına medya çalıştırılmadan önce bilgisayardaki sistem saatine göre karşılaştırılır. Sistem saati, sona erme zamanından önceki bir zamandan veya ondan sonra olduğunda, tek başına medya başlatılmaz. Bu seçenekler, [New-CMStandaloneMedia](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps) PowerShell cmdlet 'i kullanılarak da kullanılabilir.  

6. **Tek BAŞıNA CD/DVD** sayfasında, işletim sistemini dağıtan görev sırasını seçin. Yalnızca bir Önyükleme görüntüsüyle ilişkili olan görev dizilerini seçebilirsiniz. Görev sırası tarafından başvurulan içerik listesini doğrulayın.  

    - **İlişkili uygulama bağımlılıklarını Algıla ve bu medyaya Ekle**: Ayrıca, uygulama bağımlılıkları için medyaya içerik ekleyin.  

        > [!TIP]  
        > Beklenen uygulama bağımlılıklarını görmüyorsanız Listeyi yenilemek için bu seçeneği kaldırın ve yeniden seçin.  

7. **Uygulama Seç** sayfasında, medya dosyasının bir parçası olarak dahil edilecek ek uygulama içeriğini belirtin.  

8. **Paket Seç** sayfasında, medya dosyasının bir parçası olarak dahil edilecek ek paket içeriğini belirtin.  

9. **Sürücü paketini Seç** sayfasında, medya dosyasının bir parçası olarak dahil edilecek ek sürücü paketi içeriğini belirtin.  

10. **Dağıtım noktaları** sayfasında, gerekli içeriği içeren dağıtım noktalarını belirtin.  

    Configuration Manager yalnızca içeriği olan dağıtım noktalarını görüntüler. Devam etmeden önce görev dizisiyle ilişkili tüm içeriği en az bir dağıtım noktasına dağıtın. İçeriği dağıttıktan sonra dağıtım noktası listesini yenileyin. Bu sayfada zaten seçtiğiniz dağıtım noktalarını kaldırın, önceki sayfaya gidin ve **dağıtım noktaları** sayfasına dönün. Alternatif olarak, Sihirbazı yeniden başlatın. Daha fazla bilgi için bkz. [bir görev dizisi tarafından başvurulan Içeriği dağıtma](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) ve [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

11. **Özelleştirme** sayfasında, aşağıdaki seçenekleri belirtin:  

    - Görev dizisinin kullandığı tüm değişkenleri ekleyin.  

    - **Başlatma öncesi komutunu etkinleştir**: görev dizisi çalışmadan önce çalıştırmak istediğiniz başlatma öncesi komutlarını belirtin. Başlatma öncesi komutlar, görev dizisi çalıştırılmadan önce Windows PE 'de kullanıcıyla etkileşime girebilen bir betik veya yürütülebilir dosyadır. Daha fazla bilgi için bkz. [görev dizisi medyası Için başlatma öncesi komutları](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Medya oluşturma sırasında, görev sırası değişkenlerinin değeri de dahil olmak üzere paket KIMLIĞINI ve başlatma öncesi komut satırını, Configuration Manager konsolunu çalıştıran bilgisayardaki **CreateTsMedia. log** dosyasına yazar. Görev dizisi değişkenlerinin değerini doğrulamak için bu günlük dosyasını inceleyebilirsiniz.  

        Başlatma öncesi komutu herhangi bir içerik gerektiriyorsa, **başlatma öncesi komutu için dosya ekleme**seçeneğini belirleyin.  

12. Sihirbazı tamamlayın.  

Tek başına medya dosyaları (. ISO), hedef klasörde oluşturulur. **CD/DVD seti**' ni seçtiyseniz çıktı dosyalarını bir CD veya DVD kümesine kopyalayın.


## <a name="next-steps"></a>Sonraki adımlar

[Windows’u ağ kullanmadan dağıtmak için tek başına ortam kullanma](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
