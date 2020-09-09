---
title: Uygulama oluşturma
titleSuffix: Configuration Manager
description: Yazılım yüklemeye yönelik dağıtım türleri, algılama yöntemleri ve gereksinimlere sahip uygulamalar oluşturun.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3e16e605bde9224d641647ed8ad5ae58a9bfcf1e
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606522"
---
# <a name="create-applications-in-configuration-manager"></a>Configuration Manager uygulamalar oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir Configuration Manager uygulaması uygulamayla ilgili meta verileri tanımlar. Bir uygulamanın bir veya daha fazla dağıtım türü vardır. Bu dağıtım türleri, cihazlarda yazılım yüklemek için gereken yükleme dosyalarını ve bilgileri içerir. Dağıtım türü Ayrıca, algılama yöntemleri ve gereksinimleri gibi kurallara sahiptir. Bu kurallar, istemcinin yazılımın ne zaman ve nasıl yükleneceğini belirtir.  

Aşağıdaki yöntemleri kullanarak uygulamalar oluşturun:  

- Uygulama yükleme dosyalarını okuyarak otomatik olarak bir uygulama ve dağıtım türleri oluşturun:  
  - [Uygulama oluşturma](#bkmk_create) ve uygulama bilgilerini [otomatik olarak algılama](#bkmk_auto-app)
  - Dağıtım türü [oluşturma](#bkmk_create-dt) ve dağıtım türü bilgilerini [otomatik olarak tanımla](#bkmk_auto-dt)

- El ile bir uygulama oluşturun ve ardından dağıtım türlerini daha sonra ekleyin:  
  - Uygulama [oluşturma](#bkmk_create) ve uygulama bilgilerini [el ile belirtme](#bkmk_manual-app)
  - Dağıtım türü [oluşturma](#bkmk_create-dt) ve dağıtım türü bilgilerini [el ile belirtme](#bkmk_manual-dt)

- Bir dosyadan [uygulama Içeri aktarma](#bkmk_import)  

Bu makale, bir dağıtım türünü yapılandırmak için aşağıdaki bilgileri de içerir:  

- [İçerik](#bkmk_dt-content)
- [Görev sırası](#bkmk_dt-ts)
- [Algılama yöntemi](#bkmk_dt-detect)
- [Kullanıcı deneyimi](#bkmk_dt-ux)
- [Gereksinimler](#bkmk_dt-require)
- [Dönüş kodları](#bkmk_dt-return)
- [Bağımlılıklar](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a> Uygulama oluşturma  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **uygulama oluştur**' u seçin.  

Ardından, uygulama bilgilerini otomatik olarak algıla veya el ile belirt:  

- Tek bir dağıtım türü ile temel bir uygulama oluşturmak için uygulama bilgilerini [otomatik olarak algıla](#bkmk_auto-app) . Örneğin, bağımlılığı veya gereksinimleri olmayan bir Windows Installer dosyası. Bu yordamı kullanarak bir uygulama oluşturduktan sonra, gerektiğinde düzenleyin. Dağıtım türleri ekleyebilir veya değiştirebilir ve algılama yöntemleri, bağımlılıkları veya gereksinimleri ekleyebilirsiniz.  

- Daha karmaşık uygulamalar oluşturmak için uygulama bilgilerini [el ile belirtin](#bkmk_manual-app) . Birden fazla dağıtım türü, bağımlılık, algılama yöntemi veya gereksinimi tanımlayın.  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a> Uygulama bilgilerini otomatik olarak algıla  

1. Uygulama oluşturma Sihirbazı ' nın **genel** sayfasında **Bu uygulamayla Ilgili bilgileri otomatik olarak yükleme dosyalarından algıla**' yı seçin.  

2. **Tür** açılan listesinde, uygulama bilgilerini algılamak için kullanmak istediğiniz uygulama yükleme dosya türünü seçin. Kullanılabilir yükleme türleri hakkında daha fazla bilgi için bkz. [Configuration Manager tarafından desteklenen dağıtım türleri](create-applications.md#bkmk_deploy-types).  

3. **Konum** kutusunda, uygulama bilgilerini algılamak için kullanmak istediğiniz uygulama yükleme dosyasını belirtin. Bu konum bir ağ yolu ( `\\server\share\filename` ) veya bir depolama bağlantısı. Ağ yoluna ve uygulama içeriği içeren tüm alt klasörlere erişiminizin olması gerekir.  

    > [!IMPORTANT]  
    > Uygulama türü olarak **Windows Installer ( \* . msi dosyası)** seçeneğini belirlediğinizde, site belirtilen klasördeki tüm dosyaları içeri aktarır. Daha sonra bu dosyaları dağıtım noktalarına gönderir. Belirtilen klasörün yalnızca uygulamayı yüklemek için gerekli dosyaları içerdiğinden emin olun. Microsoft Test Configuration Manager uygulama paketindeki en fazla 20.000 dosyayı destekler. Uygulamanızda daha fazla dosya varsa, daha az dosya içeren birden çok uygulama oluşturmayı göz önünde bulundurun.  

4. Uygulama oluşturma Sihirbazı 'nın **bilgileri Içeri aktar** sayfasında, bilgileri gözden geçirin ve ardından **İleri**' yi seçin. Gerekirse, geri dönüp hataları onarmak için **önceki** ' ni seçin.  

5. Uygulama oluşturma Sihirbazı ' nın **genel bilgiler** sayfasında, aşağıdaki bilgileri belirtin:  

    > [!NOTE]  
    > Configuration Manager bu bilgileri uygulama yükleme dosyalarından otomatik olarak algılarsa, zaten doldurulmuştur. Buna ek olarak, görüntülenen seçenekler oluşturduğunuz uygulama türüne bağlı olarak farklı olabilir.  

    - Uygulama hakkında uygulama **adı**, **yönetici yorumları**, **Yayımcı**ve **yazılım sürümü**gibi genel bilgiler. Configuration Manager konsolunda uygulamayı bulmanıza yardımcı olmak için, **Isteğe bağlı bir başvuru**belirtin veya **Yönetim kategorilerini**seçin.  

    - **Yükleme programı**: yükleme programını ve uygulama dağıtım türünü yüklemek için gereken tüm gerekli özellikleri belirtin.  

        > [!TIP]  
        > Yükleme programı görüntülenmezse, **Araştır** ' ı seçin ve yükleme programı konumuna gidin.  

    - **Yükleme davranışı**: Configuration Manager Bu dağıtım türünü nasıl yüklediği hakkında üç seçenekten birini belirleyin. Bu seçenekler hakkında daha fazla bilgi için bkz. [Kullanıcı deneyimi](#bkmk_dt-ux).  

    - **OTOMATIK VPN bağlantısı kullan (yapılandırıldıysa)**: kullanıcının uygulamayı başlattığı CIHAZA bir VPN profili dağıttıysanız, uygulama başladığında VPN bağlantısını bağlayın. Bu seçenek yalnızca Windows 8.1 ve Windows Phone 8,1 içindir. Windows Phone 8,1 cihazlarda, cihaza birden fazla VPN profili dağıtırsanız, otomatik VPN bağlantıları desteklenmez. Daha fazla bilgi için bkz. [VPN profilleri](../../protect/deploy-use/vpn-profiles.md).  

    - **Cihazdaki tüm kullanıcılar için bu uygulamayı sağla**<!--1358310-->: Cihazdaki tüm kullanıcılar için Windows uygulama paketi ile bir uygulama sağlayın. Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../get-started/creating-windows-applications.md#bkmk_provision).  

       > [!Tip]  
       > Mevcut bir uygulamayı değiştiriyorsanız, bu ayar Windows uygulama paketi dağıtım türü özelliklerinin **Kullanıcı deneyimi** sekmesindedir.  

6. **İleri**' yi seçin, **Özet** sayfasında uygulama bilgilerini gözden geçirin ve ardından uygulama oluşturma Sihirbazı ' nı kapatın.  

Yeni uygulama artık Configuration Manager konsolunun **uygulamalar** düğümünde görüntülenir. Bir uygulama oluşturmayı tamamladınız.

Daha fazla dağıtım türü eklemek veya diğer ayarları yapılandırmak için bkz. [uygulama için dağıtım türleri oluşturma](#bkmk_create-dt).  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a> Uygulama bilgilerini el ile belirt  

1. Uygulama Oluştur sihirbazının **genel** sayfasında **uygulama bilgilerini el ile belirt**' i seçin ve ardından **İleri**' yi seçin.  

2. Uygulamayla ilgili **genel bilgileri** belirtin:  

    - Uygulama **adı** gereklidir ve 256 karakterden kısa olmalıdır.  

    - **Yönetici yorumları**, **yayımcısı**ve **yazılım sürümü** , uygulamayı daha ayrıntılı olarak açıklamaya yönelik ek meta verilerlerdir.  

    - Configuration Manager konsolunda uygulamayı bulmanıza yardımcı olmak için, **Isteğe bağlı bir başvuru**belirtin veya **Yönetim kategorilerini**seçin.  

    - **Yayımlanma tarihi**  

    - Bu uygulamadan sorumlu olan kullanıcıları veya grupları, **sahipler** ve **destek kişileri**' ni seçin. Varsayılan olarak, bu değerler Kullanıcı adınız olarak ayarlanır.  

3. Uygulama oluşturma Sihirbazı ' nın **Yazılım Merkezi** sayfasında, aşağıdaki bilgileri belirtin:  

    > [!Note]  
    > Sürüm 1902 ve önceki sürümlerde Bu sayfa **Uygulama Kataloğu**olarak adlandırılmıştır.

    - **Seçilen dil**: açılan listede, ayarlamak istediğiniz uygulamanın dil sürümünü seçin. Bu uygulama için daha fazla dil ayarlamak üzere **Ekle/Kaldır** ' ı seçin.  

    - **Yerelleştirilmiş uygulama adı**: seçili dilde uygulama adını belirtin.  

        > [!IMPORTANT]  
        > Ayarladığınız her dil sürümü için yerelleştirilmiş bir uygulama adı gereklidir.  

    - **Kullanıcı kategorileri**: seçili dilde uygulama kategorilerini belirtmek için **Düzenle** ' yi seçin. Software Center kullanıcıları, uygulamaları filtrelemeye ve sıralamaya yardımcı olması için bu kategorileri kullanır.  

        > [!Note]  
        > Sürüm 1902 ve önceki sürümlerde, Kullanıcı kategorileri yalnızca kullanıcı koleksiyonlarına kullanılabilir dağıtımlar için geçerlidir. Bir uygulama bir bilgisayar koleksiyonuna dağıtılırsa, Kullanıcı kategorileri yok sayılır.
        >
        > Sürüm 1906 ' den başlayarak, cihaz hedefli uygulama dağıtımları için Kullanıcı kategorileri yazılım merkezi 'nde filtreler olarak gösterilir. Bu dağıtımlar kullanılabilir veya gerekli olabilir.
        >
        > <!-- 4726793 -->Bir kategorinin yeniden adlandırılması veya silinmesi, bu kategorideki uygulamalara otomatik olarak uygulanmaz. Bu değişiklikler, uygulamanın bir sonraki düzeltmesine uygulanır. Yeniden adlandırmak veya silmek üzere bu sorunu geçici olarak çözmek için:
        >
        > - İlk olarak, kendisine başvuran tüm uygulamalarda kategorinin onay kutusunu temizleyin. Ardından, uygulamayı düzelten bu değişikliği uygulayın.
        >     - Yeniden adlandırma eylemi yerine, daha sonra yeni ada sahip yeni bir kategori oluşturun ve yeni kategoriyi ilgili uygulamalara ekleyin.
        >     - Uygulamaları düzelttiğinizde, kategoriyi silebilirsiniz.

    - **Kullanıcı belgeleri**: yazılım merkezi kullanıcılarının bu uygulama hakkında daha fazla bilgi alabileceğiniz bir dosyanın konumunu belirtin. Bu konum bir Web sitesi adresidir veya bir ağ yolu ve dosya adıdır. Kullanıcıların bu konuma erişimi olduğundan emin olun.  

    - **Bağlantı metni**: Kullanıcı belgeleri belirtildiğinde "ek bilgiler" yerine görüntülenen metni belirtin.  

    - **Gizlilik URL 'si**: uygulama için gizlilik bildirimine bir Web sitesi adresi belirtin.  

    - **Yerelleştirilmiş açıklama**: seçili dilde bu uygulama için bir açıklama girin.  

    - **Anahtar sözcükler**: seçili dildeki anahtar sözcüklerin bir listesini girin. Bu anahtar sözcükler yazılım merkezi kullanıcılarının uygulamayı aramasına yardımcı olur.  

    - **Simge**: Bu uygulama için bir simge seçmek üzere **Araştır** ' ı seçin. Bir simge belirtmezseniz, Configuration Manager varsayılan bir simge kullanır. Simgelerin piksel boyutları 512x512 ' ye kadar olabilir.  

4. Uygulama oluşturma Sihirbazı 'nın **dağıtım türleri** sayfasında **Ekle** ' yi seçerek yeni bir dağıtım türü oluşturun. Daha fazla bilgi için bkz. [uygulama için dağıtım türleri oluşturma](#bkmk_create-dt).  

5. **İleri**' yi seçin, **Özet** sayfasında uygulama bilgilerini gözden geçirin ve ardından uygulama oluşturma Sihirbazı ' nı kapatın.  

Yeni uygulama artık Configuration Manager konsolunun **uygulamalar** düğümünde görüntülenir.  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a> Uygulama için dağıtım türleri oluşturma  

[Uygulama bilgilerini otomatik olarak algılayın](#bkmk_auto-app), bu bölümdeki adımlardan bazılarını bitiremeyebilirsiniz.  

> [!Note]  
> Mevcut bir dağıtım türünün özelliklerini görüntülediğinizde, aşağıdaki bölümler dağıtım türü Özellikler penceresinin sekmelerine karşılık gelir:  
>
> - [İçerik](#bkmk_dt-content)
> - [Görev sırası](#bkmk_dt-ts)
> - [Algılama yöntemi](#bkmk_dt-detect)
> - [Kullanıcı deneyimi](#bkmk_dt-ux)
> - [Gereksinimler](#bkmk_dt-require)
> - [Dönüş kodları](#bkmk_dt-return)
> - [Bağımlılıklar](#bkmk_dt-depend)
>  
> Dağıtım türünün özelliklerindeki **davranış** denetimi sekmesi hakkında daha fazla bilgi için bkz. [çalıştırılabilir dosyaları çalıştırmaya yönelik denetim](deploy-applications.md#bkmk_exe-check).  

### <a name="start-the-create-deployment-type-wizard"></a>Dağıtım türü oluşturma Sihirbazı 'nı başlatma  

Dağıtım türü oluşturma Sihirbazı 'nı başlatmak için üç yol vardır:

- **Uygulamalar düğümünde**: Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin. Bir uygulama seçin ve ardından şeritte **dağıtım türü oluştur** ' u seçin.  

- Uygulama **oluştururken**: uygulama [bilgilerini el ile belirttiğinizde](#bkmk_manual-app) , uygulama oluşturma Sihirbazı 'Nda dağıtım türleri sayfasında **Ekle** ' yi seçin.  

- **Uygulama özelliklerinden**: **uygulamalar** düğümünde mevcut bir uygulamayı seçin ve **Özellikler**' i seçin. **Dağıtım türleri** sekmesine geçin ve **Ekle**' yi seçin.

Ardından, dağıtım türü bilgilerini [otomatik olarak tanımlamak](#bkmk_auto-dt) veya [el ile belirtmek](#bkmk_manual-dt) için aşağıdaki yordamlardan birini kullanın.  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a> Dağıtım türü bilgilerini otomatik olarak tanımla  

1. Dağıtım türü oluşturma Sihirbazı ' nın **genel** sayfasında:  

    1. Dağıtım türü bilgilerini algılamak için uygulama yükleme dosya **türünü** seçin.  

    2. **Bu dağıtım türü ile ilgili bilgileri yükleme dosyalarından otomatik olarak tanımla**' yı seçin.  

    3. **Konum** kutusunda, dağıtım türü bilgilerini algılamak için kullanmak istediğiniz uygulama yükleme dosyasını belirtin. Bu konum bir ağ yolu ( `\\server\share\filename` ) veya bir depolama bağlantısı. Ağ yoluna ve uygulama içeriği içeren tüm alt klasörlere erişiminizin olması gerekir.  

2. Dağıtım türü oluşturma Sihirbazı 'nın **bilgileri Içeri aktar** sayfasında, bilgileri gözden geçirin ve ardından **İleri**' yi seçin. Gerekirse, geri dönüp hataları onarmak için **önceki** ' ni seçin.  

3. Dağıtım türü oluşturma Sihirbazı ' nın **genel bilgiler** sayfasında, aşağıdaki bilgileri belirtin:  

    > [!NOTE]  
    > Uygulama yükleme dosyalarından okunmuşsa, bazı dağıtım türü bilgileri önceden mevcut olabilir. Ayrıca, görüntülenen seçenekler, oluşturmakta olduğunuz dağıtım türüne bağlı olarak farklılık gösterebilir.  

    - Dağıtım türüyle ilgili **genel bilgiler** :  
        - **Ad** gereklidir  

        - Daha ayrıntılı açıklama için **yönetici yorumları**  

        - Kullanılabilir **Diller**  

    - **Yükleme programı**: yükleme programını ve dağıtım türünü yüklemek için gerek duyduğunuz özellikleri belirtin.  

    - **Yükleme davranışı**: Configuration Manager Bu dağıtım türünü nasıl yüklediği hakkında üç seçenekten birini belirleyin. Bu seçenekler hakkında daha fazla bilgi için bkz. [Kullanıcı deneyimi](#bkmk_dt-ux).  

    - **OTOMATIK VPN bağlantısı kullan (yapılandırıldıysa)**: kullanıcının uygulamayı başlattığı CIHAZA bir VPN profili dağıttıysanız, uygulama başladığında VPN bağlantısını bağlayın. Bu seçenek yalnızca Windows 8.1 ve Windows Phone 8,1 içindir. Windows Phone 8,1 cihazlarda, cihaza birden fazla VPN profili dağıtırsanız, otomatik VPN bağlantıları desteklenmez. Daha fazla bilgi için bkz. [VPN profilleri](../../protect/deploy-use/vpn-profiles.md).  

4. **İleri**' yi seçin ve ardından [dağıtım türü içerik seçeneklerine](#bkmk_dt-content)devam edin.  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a> Dağıtım türü bilgilerini el ile belirt  

1. Dağıtım türü Oluştur sihirbazının **genel** sayfasında, **tür** açılan listesinde, bu dağıtım türü için uygulama yükleme dosya türünü seçin.

2. **Dağıtım türü bilgilerini el ile belirt**' i seçin ve ardından **İleri**' yi seçin.

3. Dağıtım türü oluşturma Sihirbazı ' nın **genel bilgiler** sayfasında, dağıtım türü Için bir **ad** belirtin. İsteğe bağlı olarak **yönetici açıklamalarını**belirtin, bu dağıtım türü için **dilleri** seçin ve ardından **İleri**' yi seçin.  

4. [Dağıtım türü içerik seçeneklerine](#bkmk_dt-content)devam edin.  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a> Dağıtım türü **içerik** seçenekleri  

**İçerik** sayfasında, aşağıdaki bilgileri belirtin:  

> [!Note]  
> Mevcut bir dağıtım türünün özelliklerini görüntülediğinizde, bu seçeneklerden bazıları **içerik** sekmesinde ve bazı **Programlar** sekmesinde görünür.  

- **İçerik konumu**: Bu dağıtım türü için içeriğin konumunu belirtin veya dağıtım türü içerik klasörünü seçmek için **Araştır** ' ı seçin.  

    > [!IMPORTANT]  
    > Site sunucusu bilgisayarının sistem hesabı, belirtilen içerik konumu için izinlere sahip olmalıdır.  

  - **İçeriği istemci önbelleğinde Sürdür**: Configuration Manager istemcisi, dağıtım türü içeriğini önbellekte süresiz olarak tutar. Uygulama zaten yüklü olsa bile, istemci içerik üzerinde devam ediyor. Bu seçenek Windows Installer tabanlı yazılımlar gibi bazı dağıtımlarda faydalıdır. Windows Installer, güncelleştirmelerin uygulanması için kaynak içeriğin yerel bir kopyasına ihtiyaç duyuyor. Bu seçenek, kullanılabilir önbellek alanını azaltır. Bu seçeneği belirlerseniz, önbellekte yeterli kullanılabilir alan yoksa büyük bir dağıtımın sonraki bir noktada başarısız olmasına neden olabilir.  

- **Yükleme programı**: yükleme programının adını ve gerekli yükleme parametrelerini belirtin.  

  - **Yükleme başlangıç**: isteğe bağlı olarak, dağıtım türü için yükleme programını içeren klasörü belirtin. Bu klasör, istemci üzerinde mutlak bir yol veya yükleme dosyalarını içeren dağıtım noktası klasörünün yolu olabilir.  

- **Programı kaldır**: isteğe bağlı olarak, kaldırma programının adını ve gerekli parametreleri belirtin.  

  - **Kaldırma başlangıç**süresi: isteğe bağlı olarak, dağıtım türü için kaldırma programına sahip klasörü belirtin. Bu klasör, istemci üzerinde mutlak bir yol olabilir. Ayrıca, paketin bulunduğu klasörün dağıtım noktasında göreli bir yol olabilir.  

- **Programı onarma**: Windows Installer ve betik yükleyici dağıtım türleri için, isteğe bağlı olarak onarım programının adını ve gerekli parametreleri belirtin.<!--1357866-->  

  - **Onarma başlangıcı**: isteğe bağlı olarak, dağıtım türü için onarım programına sahip klasörü belirtin. Bu klasör, istemci üzerinde mutlak bir yol olabilir. Ayrıca, paketin bulunduğu klasörün dağıtım noktasında göreli bir yol olabilir.  

- **Yükleme ve kaldırma programını 64 bit istemcilerde 32 bit işlem olarak çalıştırın**: dağıtım türü için yükleme programını çalıştırmak için Windows tabanlı bilgisayarlarda 32 bit dosya ve kayıt defteri konumlarını kullanın.  

#### <a name="deployment-type-properties-content-options"></a>Dağıtım türü özellikleri **içerik** seçenekleri

Bir dağıtım türünün özelliklerini görüntülediğinizde, aşağıdaki seçenekler yalnızca **içerik** sekmesinde görünür:

- **İçerik ayarlarını kaldırma**:  

  - **Yükleme Içeriğiyle aynı**: yükleme ve kaldırma içeriği aynıysa, bu seçeneği seçin. Bu seçenek varsayılandır.  

  - **Kaldırma Içeriği yok**: uygulamanızda kaldırma için içerik gerekmiyorsa, bu seçeneği seçin.  

  - **Yükleme Içeriğinden farklı**: kaldırma içeriği yükleme içeriğinden farklıysa, bu seçeneği seçin.  

    - **İçerik konumunu kaldır**: uygulamayı kaldırmak için kullanılan içeriğin ağ yolunu belirtin.  

- **İstemcilerin varsayılan site sınırı grubundan dağıtım noktalarını kullanmasına Izin ver**: istemcilerin, geçerli veya komşu sınır gruplarındaki bir dağıtım noktasından kullanılabilir olmadığında, yazılımın yazılım tarafından indirilip, site varsayılan sınır grubundaki bir dağıtım noktasından İndirilme ve yükleme gerekip gerekmediğini belirtin.  

- **Dağıtım seçenekleri**: istemcilerin bir komşudan veya varsayılan site sınır gruplarından bir dağıtım noktası kullandıklarında uygulamayı İndirmeleri gerekip gerekmediğini belirtin.  

- **İstemcilerin aynı alt ağdaki diğer istemcilerle içerik paylaşmasına izin ver**: İçerik yüklemeleri için BranchCache kullanımının etkinleştirilip etkinleştirilmeyeceğini belirtin. Daha fazla bilgi için bkz. [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). BranchCache her zaman istemcilerde etkindir. Dağıtım noktası destekliyorsa, istemciler BranchCache kullandığından, bu ayar 1802 sürümünde kaldırılmıştır.  

### <a name="deployment-type-task-sequence-options"></a><a name="bkmk_dt-ts"></a> Dağıtım türü **görev dizisi** seçenekleri

<!--3555953-->

Sürüm 2002 ' den başlayarak görev sırası dağıtım türü hakkında daha fazla bilgi için bkz. [görev dizisi dağıtım türü](../get-started/creating-windows-applications.md#bkmk_tsdt).

**Görev sırası** sayfasında, aşağıdaki bilgileri belirtin:

- **Görev sırasını yükleme**: Bu uygulama için yükleme işlemini çalıştıran bir görev sırası seçin.

- **Görev sırasını kaldır** (isteğe bağlı): Bu uygulamayı kaldıran bir görev sırası seçin.

> [!TIP]  
> Görev diziniz listede görünmezse, herhangi bir işletim sistemi dağıtımı veya işletim sistemi yükseltme adımı içermediğinden emin olun. Ayrıca, yüksek etkili bir görev dizisi olarak işaretlenmemiş olduğunu doğrulayın. Daha fazla bilgi için, [görev dizisi dağıtım türü](../get-started/creating-windows-applications.md#bkmk_tsdt)için önkoşulları gözden geçirin.

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a> Dağıtım türü **algılama yöntemi** seçenekleri

Bu yordam, dağıtım türünün varlığını gösteren bir algılama yöntemi ayarlar. Diğer bir deyişle, Windows cihazının uygulamanın zaten yüklü olup olmadığı. Bir algılama yöntemi oluşturmak için aşağıdaki iki yöntemden birini kullanın:

- [Bu dağıtım türünün varolup olmadığını algılamak için kurallar yapılandırın](#bkmk_detect-rule)
- [Bu dağıtım türünün varolup olmadığını algılamak için özel bir komut dosyası kullan](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a> Bu dağıtım türünün varolup olmadığını algılamak için kurallar yapılandırın

1. **Algılama yöntemi** sayfasında, **Bu dağıtım türünün varlığını algılamak için kuralları yapılandırma** seçeneği varsayılan olarak seçilidir. **Yan tümce Ekle**' yi seçin.  

2. **Algılama kuralı** iletişim kutusunda, dağıtım türünün varlığını algılamak Için bir **ayar türü** seçin:  

    - **Dosya sistemi**: belirtilen bir dosyanın veya klasörün cihazda mevcut olup olmadığını algıla. Bu algılama, uygulamanın yüklü olduğunu gösterir. Aşağıdaki ek ayrıntıları belirtin:  

        - **Yazın**: bir dosya veya klasör olup olmadığını seçin.  

        - **Yol** (gerekli): dosya veya klasörü içeren cihazdaki yerel yolu girin veya tarayın. Örneğin, `C:\Program Files`. Paylaşılan ağ yolunu belirtemezsiniz. **Araştır**' ı seçerseniz yerel dosya sistemine gözatıp veya bir temsilci istemci ile bağlantı kurmak için bağlanın.  

        - **Dosya veya klasör adı** (gerekli): yukarıdaki yolda tespit edilecek belirli dosya veya klasör adını belirtin. İstemci cihazda bu dosyayı veya klasörü algılarsa, uygulamayı cihazda yüklü olarak kabul eder.  

        - **Bu dosya veya klasör 64 bit sistemlerde 32 bitlik bir uygulamayla ilişkili**: istemci, belirtilen dosya veya klasör için ilk olarak 32-bit dosya konumlarını denetler. Dosya veya klasör bulunmazsa istemci, 64 bit konumları arar.  

    - **Kayıt defteri**: belirtilen bir kayıt defteri anahtarı veya kayıt defteri değerinin bir istemci cihazında mevcut olup olmadığını algıla. Bu algılama, uygulamanın yüklü olduğunu gösterir. Aşağıdaki ek ayrıntıları belirtin:  

        - **Hive** (gerekli): açılan listeden bir kayıt defteri kovanı seçin. Örneğin, `HKEY_LOCAL_MACHINE`.  

        - **Anahtar** (gerekli): Yukarıdaki Hive içinde arama yapmak için kayıt defteri anahtarını belirtin. Örneğin, `SOFTWARE\Microsoft\Office`.  

        - **Değer** (isteğe bağlı): Yukarıdaki anahtarda algılamak için belirli bir değer girin. İstemcinin (varsayılan) değerini algılamasını istiyorsanız, **algılama için (varsayılan) kayıt defteri anahtarı değerini kullanın**. Bir değer girdiğinizde veya bu seçeneği etkinleştirdiğinizde, bir **veri türü**seçmeniz gerekir.  

        - **Bu kayıt defteri anahtarı 64 bit sistemlerde 32 bitlik bir uygulamayla ilişkilidir**: belirtilen kayıt defteri anahtarı için önce 32 bit kayıt defteri konumlarını denetlemek üzere bu seçeneği belirleyin. Kayıt defteri anahtarı bulunmazsa, istemci 64-bit konumları arar.  

    - **Windows Installer**: belirtilen bir Windows Installer dosyasının istemci cihazda mevcut olup olmadığını algıla. Bu algılama, uygulamanın yüklü olduğunu gösterir. İstemcide algılanacak MSI **ürün kodunu** belirtin. **Araştır**' ı seçerseniz, ürün kodunun okunacağı MSI dosyasını seçin.

3. Algılama kuralı penceresinin en altında, öğenin var olup olmayacağını veya bir kuralı karşılayıp karşılamadığını belirtin. Örneğin, bir dosyayla karşılaşırsanız, varsayılan olarak aşağıdaki seçenek seçilidir: **dosya sistemi ayarı, bu uygulamanın varlığını göstermek için hedef sistemde**bulunmalıdır. Dosya veya klasör özelliklerine göre algılama için bir kural oluşturmak üzere diğer seçeneği belirleyin. Bu özellikler değiştirme tarihi, Oluşturulma tarihi, sürümü veya boyutu içerir. Bu kural ölçütleri her ayar türü için farklıdır.  

4. **Algılama kuralı** iletişim kutusunu kapatmak için **Tamam ' ı** seçin.  

Dağıtım türü için birden fazla algılama yöntemi oluşturduğunuzda, daha karmaşık mantık oluşturmak için yan tümceleri gruplandırabilirsiniz.  

#### <a name="group-detection-clauses-optional"></a>Grup algılama yan tümceleri *(isteğe bağlı)*

1. Dağıtım türü üzerinde üç veya daha fazla algılama yöntemi yan tümcesi oluşturun.  

2. İki veya daha fazla ardışık yan tümce seçin ve ardından **Grup**' u seçin. Grubun nerede başlatıldığını ve bittiğini gösteren ilişkili sütunlara parantez eklendiğini görürsünüz.  

    Örnek:

    | Bağlayıcı  |  ( | Yan Tümce           |  )  |
    |------------|----|------------------|-----|
    |            |    | MSI ürün kodu |     |
    | Veya         | (  | FILE1. Text var|     |
    | And        |    | file2.txt var | )   |

3. Grubu kaldırmak için gruplanmış yan tümceleri seçin ve ardından **Grubu Çöz**' ü seçin.  

Bir algılama yöntemi olarak özel bir betik kullanma ile ilgili sonraki bölüme *geçin* . Veya dağıtım türü için [Kullanıcı deneyimi](#bkmk_dt-ux) seçeneklerine *atlayın* .

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a> Dağıtım türünün varlığını denetlemek için özel bir betik kullanın  

1. **Algılama yöntemi** sayfasında, **Bu dağıtım türü kutusunun varolup olmadığını algılamak için özel bir komut dosyası kullan** ' ı seçin. Ardından **Düzenle**’yi seçin.  

2. **Betik Düzenleyicisi** iletişim kutusunda, dağıtım türünü algılamak Için bir **betik türü** seçin: PowerShell, VBScript veya JScript.  

    > [!Note]  
    > Bir Windows PowerShell betiği, uygulama algılama yöntemi olarak çalıştırıldığında, Configuration Manager istemcisi PowerShell 'i `-NoProfile` parametresiyle çağırır. Bu seçenek PowerShell 'i profil olmadan başlatır. PowerShell profili, PowerShell başladığında çalışan bir betiktir. <!--3607762-->  

3. **Betik içeriği** kutusunda, kullanmak istediğiniz betiği girin veya var olan bir betiğin içeriğini yapıştırın. Var olan kaydedilmiş bir betiğe gitmek için **Aç** ' ı seçin. Komut dosyası içeriği alanındaki metni kaldırmak için **Temizle** ' yi seçin. Gerekirse, **64 bit istemcilerde betiği 32 bit işlem olarak çalıştırma**seçeneğini etkinleştirin.  

    > [!NOTE]  
    > Bir betik için en büyük boyut 32 KB 'tır.  

4. Betiği kaydetmek ve **betik Düzenleyicisi** iletişim kutusunu kapatmak için **Tamam** ' ı seçin. Dağıtım türü oluşturma Sihirbazı 'na geri döndüğünüzde, betik **türü** ve **betik uzunluğu** alanları, betiğiyle ilgili ayrıntılarla birlikte günceldir.

#### <a name="about-custom-script-detection-methods"></a>Özel Betik algılama yöntemleri hakkında  

Configuration Manager, komut dosyasının sonuçlarını denetler. Betik tarafından standart çıkış (STDOUT) akışına, standart hata (STDERR) akışına ve çıkış koduna yazılan değerleri okur. Betik sıfır olmayan bir değerle çıkış yaptığında, betik başarısız olur ve uygulama algılama durumu *bilinmez*. Çıkış kodu sıfırsa ve STDOUT veri içeriyorsa, uygulama algılama durumu *yüklenir*.

> [!TIP]
> Bir algılama betiği yazarken, sıfır çıkış kodu döndürmeniz ancak çıkış döndürmezseniz (STDOUT 'da veriler), uygulama yüklü olarak algılanmaz. Daha fazla bilgi için aşağıdaki örneklere bakın.

Bir komut dosyasının çıktısından bir uygulamanın yüklenip yüklenmediğini denetlemek için aşağıdaki tabloları kullanın:  

##### <a name="zero-exit-code"></a>Sıfır çıkış kodu

|STDOUT|STDERR|Betik sonucu|Uygulama algılama durumu|
|---------|---------|---------|---------|
|Olmamalıdır|Olmamalıdır|Başarılı|Yüklü değil|
|Olmamalıdır|Boş değil|Hata|Bilinmiyor|
|Boş değil|Olmamalıdır|Başarılı|Yüklendi|
|Boş değil|Boş değil|Başarılı|Yüklendi|

##### <a name="non-zero-exit-code"></a>Sıfır olmayan çıkış kodu

|STDOUT|STDERR|Betik sonucu|Uygulama algılama durumu|
|---------|---------|---------|---------|
|Olmamalıdır|Olmamalıdır|Hata|Bilinmiyor|
|Olmamalıdır|Boş değil|Hata|Bilinmiyor|
|Boş değil|Olmamalıdır|Hata|Bilinmiyor|
|Boş değil|Boş değil|Hata|Bilinmiyor|

##### <a name="examples"></a>Örnekler

Kendi uygulama algılama komut dosyalarınızı yazmak için aşağıdaki PowerShell/VBScript örneklerini kullanın:  

**Örnek 1**: betik, sıfır olmayan bir çıkış kodu döndürür. Bu kod, betiğin başarıyla çalıştırılacağını gösterir. Bu durumda, uygulama algılama durumu bilinmez.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Örnek 2**: komut dosyası sıfır çıkış kodu döndürüyor, ancak stderr değeri boş değil. Bu sonuç, betiğin başarıyla çalıştırılacağını gösterir. Bu durumda, uygulama algılama durumu bilinmez.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Örnek 3**: betik, sıfır çıkış kodu döndürür; bu, başarıyla çalıştığını gösterir. Ancak, STDOUT değeri, uygulamanın yüklenmediğini gösteren boş olur.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Örnek 4**: komut dosyası sıfır çıkış kodu döndürür; bu, başarıyla çalıştığını gösterir. STDOUT değeri, uygulamanın yüklü olduğunu gösteren boş değildir.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Örnek 5**: betik, sıfır çıkış kodu döndürür; bu, başarıyla çalıştığını gösterir. STDOUT ve STDERR değerleri, uygulamanın yüklü olduğunu gösteren boş değildir.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a> Dağıtım türü **Kullanıcı deneyimi** seçenekleri

Bu ayarlar, istemcinin cihaza uygulamayı nasıl yüklediğini ve kullanıcının ne göreceğini belirtir.  

**Kullanıcı Deneyimi** sayfasında aşağıdaki bilgileri belirtin:  

- **Yükleme davranışı**: açılan listede, aşağıdaki seçeneklerden birini belirleyin:  

  - **Kullanıcı Için yükleme**: istemci yalnızca uygulamayı dağıttığınız Kullanıcı için uygulamayı yükler.  

  - **Sistem Için yükleme**: istemci uygulamayı yalnızca bir kez yükler. Bu, tüm kullanıcılar tarafından kullanılabilir.  

  - **Kaynak cihaz ise sistem Için yükleme; Aksi takdirde, Kullanıcı için yükleme**: uygulamayı bir cihaza dağıtırsanız, istemci onu tüm kullanıcılar için yükler. Uygulamayı bir kullanıcıya dağıtırsanız istemci yalnızca bu kullanıcı için yüklenir.  

- **Oturum açma gereksinimi**: aşağıdaki seçeneklerden birini belirleyin:  

  - **Yalnızca bir kullanıcı oturum açtığında**  

  - **Kullanıcının oturum açmış olup olmadığı**  

  - **Yalnızca hiçbir Kullanıcı oturum açmadığında**  

    > [!NOTE]  
    > Bu seçenek **, yalnızca bir Kullanıcı oturum açtığında**varsayılan olarak kullanılır. **Yükleme davranışı** açılır listesinde **Kullanıcı için yükleme** ' yi seçerseniz, bu seçeneği değiştiremezsiniz.  

- **Yükleme programı görünürlüğü**: dağıtım türünün istemci cihazlarda çalıştığı modu belirtin. Aşağıdaki seçeneklerden birini belirtin:  

  - **Ekranı kaplamış**: dağıtım türü, istemci cihazlarda ekranı kaplamış olarak çalışır. Kullanıcılar tüm yükleme etkinliklerini görür.  

  - **Normal**: dağıtım türü, sistem ve program varsayılanlarına bağlı olarak normal modda çalışır. Bu varsayılan moddur.  

  - **Simge durumuna küçültülmüş**: dağıtım türü istemci cihazlarda simge durumuna küçültülmüş olarak çalıştırılır. Kullanıcılar, bildirim alanında veya görev çubuğunda yükleme etkinliğini görebilir.  

  - **Gizli**: dağıtım türü istemci cihazlarda gizli olarak çalıştırılır. Kullanıcılar yükleme etkinliği görmez.  

- **Kullanıcıların program yüklemesini görüntülemesine ve etkileşime girmesine Izin ver**: yükleme seçeneklerini ayarlamak için bir kullanıcının dağıtım türü yüklemesiyle etkileşime giremeyeceğini belirtin.  

    **Yükleme davranışı** açılır listesinde **Kullanıcı için yükleme** seçeneğini belirlediyseniz, bu seçenek varsayılan olarak etkindir.  

    > [!IMPORTANT]  
    > **Sistem Için yüklemeyi** seçin davranışını seçtiğinizde, bu ayar isteğe bağlıdır. Bu değişiklik, birincil olarak son kullanıcının bir görev sırası sırasında yüklemeyle etkileşime geçmesini sağlar. Örneğin, son kullanıcıya çeşitli seçenekler için istemde bulunan bir kurulum işlemini çalıştırmak için. Bazı uygulama yükleyicilerinin Kullanıcı istemlerinin susuyor olması veya yükleme işleminin yalnızca Kullanıcı tarafından bilinen belirli yapılandırma değerlerinin olması gerekebilir. <!--1356976-->  
    >  
    > Sistem bağlamına yükleme ve kullanıcıların yüklemeyle etkileşime girmesine izin verme güvenli bir yapılandırma değildir. Daha fazla bilgi için bkz. [uygulama yönetimi için güvenlik ve gizlilik](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact).  

- **İzin verilen en fazla çalışma süresi (dakika)**: dağıtım türünün istemci bilgisayarda çalıştırılmasını beklemeniz için geçmesi gereken en uzun süreyi dakika cinsinden belirtin. Bu ayarı sıfırdan büyük bir tam sayı olarak belirtin. Varsayılan değer 120 dakikadır (iki saat).  

    Aşağıdaki eylemler için bu değeri kullanın:  

  - Dağıtım türünden sonuçları izlemek için.  

  - İstemci cihazlarında bakım pencerelerini tanımlarken bir dağıtım türünün yüklü olup olmadığını denetlemek için. Bir bakım penceresi olduğunda, dağıtım türü yalnızca bakım penceresinde **Izin verilen en fazla çalışma süresi** ayarına uyum sağlamak için yeterli zaman varsa başlar.  

    > [!IMPORTANT]  
    > **İzin verilen en fazla çalışma süresinin** zamanlanan bakım penceresinden daha uzun olması durumunda bir çakışma meydana gelebilir. Kullanıcı en fazla çalışma süresini kullanılabilir bakım penceresi uzunluğundan daha büyük bir süreye ayarlarsa, o dağıtım türü çalıştırılmaz.  

- **Tahmini yükleme süresi (dakika)**: dağıtım türünün tahmini yükleme süresini belirtin. Kullanıcılar, yazılım merkezi 'nde bu saati görür.  

#### <a name="deployment-type-properties-user-experience-options"></a>Dağıtım türü özellikleri **Kullanıcı deneyimi** seçenekleri

Bir dağıtım türünün özelliklerini görüntülediğinizde, aşağıdaki seçenekler yalnızca **Kullanıcı deneyimi** sekmesinde görünür:

Belirli yükleme sonrası davranışı zorunlu tutun. Aşağıdaki seçeneklerden birini belirtin:  

- **Dönüş kodlarına dayalı davranışı belirle**: [dönüş kodları](#bkmk_dt-return) sekmesinde yapılandırılan kodlara göre tanıtıcı yeniden başlatmalar. Software Center ekranları için **yeniden başlatma**gerekebilir. Yüklemesi sırasında bir Kullanıcı oturum açmışsa, bu kullanıcılara *dağıtımın* Kullanıcı deneyimi yapılandırmasına bağlı olarak sorulur.  

- **Belirli bir eylem yok**: yüklemeden sonra yeniden başlatma gerekmez. Yazılım Merkezi, yeniden başlatma gerekmediğini bildirir.  

- **Yazılım yükleme programı bir cihazın yeniden başlatılmasını zorlayabilir**: Configuration Manager yeniden başlatma işlemini denetlemez veya başlatamıyor, ancak gerçek yükleme bunu uyarı vermeden yapamayabilir. Yükleyici bir yeniden başlatma başlattığı zaman yükleme başarısızlığını Configuration Manager engellemek için bu ayarı kullanın. Software Center ekranları için **yeniden başlatma**gerekebilir.  

- **Configuration Manager istemci zorunlu bir cihaz yeniden başlatmaya zorlayacaktır**: Configuration Manager başarılı olduktan sonra cihaz yeniden başlatılmasını zorlar. Yazılım Merkezi bir yeniden başlatmanın gerekli olduğunu bildiriyor. Yüklemesi sırasında bir Kullanıcı oturum açmışsa, bu kullanıcılara *dağıtımın* Kullanıcı deneyimi yapılandırmasına bağlı olarak sorulur.  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a> Dağıtım türü **gereksinimleri**

Configuration Manager, dağıtım türünü yüklemeden önce cihazlarda bu gereksinimleri doğrular. Bu uygulamayı alan cihazları veya kullanıcıları daha ayrıntılı hale getirmek ve denetlemek için gereksinimleri kullanın. Örneğin, uygulamayı bir kullanıcı koleksiyonuna dağıtırsanız, uygulamanın donanım gereksinimlerini burada belirtin.

1. **Gereksinimler** sayfasında, **Ekle** ' yi seçerek **Gereksinim Oluştur** iletişim kutusunu açın.  

2. **Kategori** açılan listesinden, bu gereksinimin bir **cihaz** veya **Kullanıcı**için olup olmadığını seçin.  

    Önceden oluşturulmuş genel koşulu kullanmak için **özel** ' i seçin. **Özel**' i seçtiğinizde, yeni bir genel koşul oluşturmak için **Oluştur** ' u da seçebilirsiniz. Genel koşullar hakkında daha fazla bilgi için bkz. [genel koşullar oluşturma](create-global-conditions.md).  

    > [!IMPORTANT]  
    > Uygulamayı bir cihaz koleksiyonuna dağıtırsanız, istemci kategori **kullanıcısı** ve **birincil cihaz**koşulunun herhangi bir gereksinimini yoksayar.  

3. **Koşul** açılan listesinden, kullanıcının veya cihazın yükleme gereksinimlerini karşılayıp karşılamadığını değerlendirmek için koşulu seçin. Bu listenin içeriği, seçilen kategoriye göre değişir.  

4. **İşleç** açılan listesinden kullanılacak işleci seçin. Bu işleç, seçilen koşulu belirtilen değerle karşılaştırır. Kullanıcı veya cihazın yükleme gereksinimini karşılayıp karşılamadığını değerlendirir. Kullanılabilir operatörler, seçilen koşula bağlı olarak farklılık gösterir. `One Of`İşleci kullanılırken, Values alanı her satır için bir giriş girmeniz gerektiğini doğrulamaya sahiptir.

    > [!Note]  
    > Kullanılabilir gereksinimler, dağıtım türünün kullandığı cihaz türüne bağlı olarak farklılık gösterir.  

5. **Değer** kutusunda, karşılaştırma için kullanılacak değerleri belirtin. Bu değerler, seçilen koşul ve işleçle birlikte, kullanıcının veya cihazın yükleme gereksinimlerini karşılayıp karşılamadığını değerlendirin. Kullanılabilir değerler, seçilen koşula ve seçilen işlece bağlı olarak değişir.  

6. Gereksinimi kaydetmek ve **Gereksinim Oluştur** iletişim kutusunu kapatmak için **Tamam** ' ı seçin.  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a> Dağıtım türü **bağımlılıkları**  

Bağımlılıklar, istemcinin bu dağıtım türünü yüklemeden önce yüklenmesi gereken başka bir uygulamadan bir veya daha fazla dağıtım türünü tanımlar.

> [!IMPORTANT]  
> Bazı durumlarda, dağıtım türü bağımlılıkları olan bir dağıtım türüne bağımlıdır. Zincirde desteklenen en fazla bağımlılık sayısı beştir.  

1. **Bağımlılıklar** sayfasında **Ekle**' yi seçin.  

2. Bağımlılık Ekle penceresinde, **bağımlılık grubu adını**girin. Bu ad, bu uygulama bağımlılıkları grubuna başvurur.  

3. Bağımlılık Ekle penceresinde **Ekle**' yi seçin.  

4. **Gerekli uygulamayı belirtin** penceresinde, bir bağımlılık olarak kullanmak için kullanılabilir bir uygulama ve dağıtım türlerinden en az birini seçin.  

    > [!TIP]  
    > Seçili uygulamanın veya dağıtım türünün özelliklerini görüntülemek için **görüntüle** ' yi seçin.  

5. **Gerekli uygulamayı belirt** penceresini kapatmak için **Tamam ' ı** seçin.  

6. İstemcinin bağımlı uygulamayı otomatik olarak yüklemesini istiyorsanız, bağımlılığın yanındaki **otomatik yüklemeyi** seçin.  

    > [!NOTE]  
    > İstemcinin otomatik olarak yüklemesi için bağımlı bir uygulama dağıtmanız gerekmez.  

7. Birden fazla bağımlılık eklerseniz, **önceliği artır** ve **önceliği azalt** düğmelerini kullanın. Bu eylemler, istemcinin her bağımlılığı değerlendiren sırayı değiştirir.  

8. **Bağımlılık Ekle** penceresini kapatmak için **Tamam ' ı** seçin.  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a> Dağıtım türü **dönüş kodları**

> [!Note]  
> Bu sayfa, dağıtım türü oluşturma Sihirbazı 'nda değil. Bu yalnızca var olan bir dağıtım türünün özelliklerindeki bir sekmedir.  

Dağıtım türü tamamlandıktan sonra davranışları denetlemek için dönüş kodları belirtin. Örneğin, bir yeniden başlatmanın gerekli olduğu sinyalini yükleme tamamlanmıştır.

1. Dağıtım türü Özellikler penceresinin **dönüş kodları** sekmesinde **Ekle**' yi seçin.  

2. Dönüş kodu Ekle penceresinde, bu dağıtım türünden bekleeceğiniz **dönüş kodu değerini** belirtin. Bu değer, ve arasında herhangi bir pozitif veya negatif bir tamsayıdır `-2147483648` `2147483647` .  

3. Açılan listeden bir **kod türü** seçin. Bu ayar Configuration Manager, belirtilen dönüş kodunu bu dağıtım türünden nasıl yorumlayacağını tanımlar. Kullanılabilir türler, dağıtım türü teknolojisine göre farklılık gösterir.  

    - **Başarılı (yeniden başlatma yok)**: dağıtım türü başarıyla yüklendi ve yeniden başlatma gerekli değildir.  

    - **Hata (yeniden başlatma yok)**: dağıtım türü yüklenemedi.  

    - **Sabit yeniden başlatma**: dağıtım türü başarıyla yüklendi, ancak cihazın yeniden başlatılmasını gerektiriyor. Cihaz yeniden başlatılana kadar başka hiçbir şey yüklenemez.  

    - **Geçici yeniden başlatma**: dağıtım türü başarıyla yüklendi, ancak cihazın yeniden başlatılmasını ister. Diğer yüklemeler cihaz yeniden başlatılmadan önce gerçekleşebilir.  

    - **Hızlı yeniden deneme**: cihazda başka bir yükleme zaten devam ediyor. İstemci her iki saatte bir yeniden dener ve toplam 10 kez yeniden denenir.  

4. İsteğe bağlı olarak, bu dönüş kodu için bir **ad** ve **Açıklama** girin.

5. Dönüş kodu Ekle penceresini kapatmak için **Tamam ' ı** seçin.  

#### <a name="example-non-zero-success"></a>Örnek: sıfır olmayan başarılı

Başarılı bir şekilde yüklediğinde çıkış kodu döndüren bir uygulama dağıtuyoruz `1` . Varsayılan olarak, Configuration Manager sıfır olmayan geri dönüş kodunu hata olarak algılar. Dönüş kodu değerini belirtin `1` ve başarı kod türünü seçin **(yeniden başlatma yok)**. Şimdi Configuration Manager Bu dağıtım türü için bir başarı olarak döndürülen kodu yorumlar.

#### <a name="default-return-codes"></a>Varsayılan dönüş kodları

Bazı dağıtım türleri oluşturduğunuzda Configuration Manager, bu teknolojide ortak olan aşağıdaki dönüş kodlarını otomatik olarak ekler:  

##### <a name="windows-installer-msi-file"></a>Windows Installer ( \* . msi dosyası)

|Değer    |Kod türü|
|---------|---------|
|0        |Başarılı (yeniden başlatma yok)|
|1707     |Başarılı (yeniden başlatma yok)|
|3010     |Geçici yeniden başlatma|
|1641     |Sabit yeniden başlatma|
|1618     |Hızlı yeniden deneme|

##### <a name="script-installer"></a>Betik Yükleyici

|Değer    |Kod türü|
|---------|---------|
|0        |Başarılı (yeniden başlatma yok)|
|1641     |Sabit yeniden başlatma|
|3010     |Geçici yeniden başlatma|
|1618     |Hızlı yeniden deneme|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Windows uygulama paketi ( \* . appx, \* . appxdemeti, \* . msix, \* . msixdemeti)

|Değer    |Kod türü|
|---------|---------|
|15605    |Hızlı yeniden deneme|
|15618    |Hızlı yeniden deneme|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a> App-V dağıtım türleri için ek seçenekler  

Sanal uygulamalar (App-V) için dağıtım türleri için benzersiz olan ek seçenekleri yapılandırın.  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a> App-V dağıtım türü **içerik** seçenekleri  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.  

2. App-V dağıtım türüne sahip bir uygulama seçin ve **Özellikler**' i seçin.  

3. Uygulama özellikleri ' nde **dağıtım türleri** sekmesine geçin. App-V dağıtım türünü seçin ve **Düzenle**' yi seçin.  

4. Dağıtım türü özelliklerinde **içerik** sekmesine geçin. Aşağıdaki seçenekleri gerekli şekilde yapılandırın:  

    - **İçeriği istemci önbelleğinde Sürdür**: Configuration Manager istemci, bu dağıtım türü için içeriği önbellekten silmez.  

    - **Başlamadan önce App-v önbelleğine Içerik yükle**: uygulama başlamadan önce, Configuration Manager istemci App-v önbelleğine bu dağıtım türü için tüm içeriği yükler. İstemci önbellekteki içeriği sabitleyemez. Gerektiğinde içeriği siler.  

5. Dağıtım türü özelliklerini kapatmak için **Tamam ' ı** seçin. Ardından, uygulama özelliklerini kapatmak için **Tamam** ' ı seçin.  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a> App-V dağıtım türü **Yayımlama** seçenekleri

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.  

2. App-V dağıtım türüne sahip bir uygulama seçin ve **Özellikler**' i seçin.  

3. Uygulama özellikleri ' nde **dağıtım türleri** sekmesine geçin. App-V dağıtım türünü seçin ve **Düzenle**' yi seçin.  

4. Dağıtım türü özelliklerinde **Yayımlama** sekmesine geçin. Sanal uygulamadaki yayımlamak istediğiniz öğeleri seçin.  

5. Dağıtım türü özelliklerini kapatmak için **Tamam ' ı** seçin. Ardından, uygulama özelliklerini kapatmak için **Tamam** ' ı seçin.  

## <a name="import-an-application"></a><a name="bkmk_import"></a> Bir uygulamayı içeri aktarma  

Bir uygulamayı Configuration Manager aktarmak için aşağıdaki yordamı kullanın:

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar** düğümünü seçin.  

2. Şeritte, **giriş** sekmesinde ve **Oluştur** grubunda, **uygulamayı içeri aktar**' ı seçin.  

3. Uygulama alma Sihirbazı ' nın **genel** sayfasında, alınacak **dosyanın** ağ yolunu belirtin. Örneğin, `\\server\share\file.zip`. Bu dosya, dışarıya aktarılmış bir Configuration Manager uygulamasının geçerli bir sıkıştırılmış arşividir (ZIP biçimidir).  

4. **Dosya içeriği** sayfasında, bu uygulama mevcut bir uygulamanın yinelemesi olduğunda gerçekleştirilecek eylemi seçin. Yeni bir uygulama oluşturun veya yinelemeyi yoksayın ve var olan uygulamaya yeni bir düzeltme ekleyin.  

5. **Özet** sayfasında, eylemleri gözden geçirin ve Sihirbazı sona erdirin.  

Yeni uygulama **Uygulamalar** düğümünde görüntülenir.  

> [!TIP]  
> Windows PowerShell cmdlet **Import-Cmapp,** Bu yordamla aynı işleve sahiptir. Daha fazla bilgi için bkz. [Import-Cmappte](/powershell/module/configurationmanager/import-cmapplication).  

Bir uygulamayı dışarı aktarma hakkında daha fazla bilgi için bkz. [uygulamalar Için yönetim görevleri](management-tasks-applications.md).

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a> Desteklenen Dağıtım türleri  

Configuration Manager, uygulamalar için aşağıdaki dağıtım türlerini destekler:

| Dağıtım türü adı | Açıklama |
|--------------------------|----------------------|  
| **Windows Installer ( \* . msi dosyası)** | Bir Windows Installer dosyası. |  
| **Windows uygulama paketi ( \* . appx, \* . appxdemeti, \* . msix, \* . msixdemeti)** | Bir Windows uygulama paketi dosyası (. appx), bir Windows uygulama paketi paketi (. appxdemeti), bir Windows 10 uygulama paketi (. maltı) veya Windows 10 uygulama paketi (. msixdemeti).<!--1357427--> |  
| **Windows uygulama paketi (Windows Mağazası'nda)** | Windows Mağazası 'nda uygulamanın bağlantısını belirtin veya uygulamayı seçmek için mağazaya göz atabilirsiniz.<sup>[1. nota](#bkmk_note1)</sup> |  
| **Betik Yükleyici** | İçerik yüklemek veya bir eylem yapmak için Windows istemcilerinde çalışan bir betik veya program belirtin. setup.exe yükleyicileri veya betik sarmalayıcıları için bu dağıtım türünü kullanın. |  
| **Microsoft Application Virtualization 4** | Bir Microsoft App-V v4 bildirimi. |  
| **Microsoft Application Virtualization 5** | Bir Microsoft App-V v5 paket dosyası. |  
| **Windows Phone uygulama paketi ( \* . xap dosyası)** | Windows Phone uygulama paketi dosyası. |  
| **Windows Phone uygulama paketi (Windows Phone Mağazası'nda)** | Windows Mağazası 'nda uygulamanın bağlantısını belirtin. |  
| **Mac OS X** | Configuration Manager istemcisini çalıştıran macOS bilgisayarları için. **CMAppUtil** aracıyla bir. cmmac dosyası oluşturun. |  
| **Web uygulaması** | Bir Web uygulamasının bağlantısını belirtin. Bu dağıtım türü, kullanıcının cihazında Web uygulamasına bir kısayol yüklüyor. |  
| **MDM ( \* . msi) üzerinden Windows Installer** | Windows 10 cihazlarına Windows Installer tabanlı uygulamalar oluşturun ve dağıtın. Daha fazla bilgi için bkz. [MDM 'ye kayıtlı Windows 10 cihazlarına Windows Installer uygulamaları dağıtma](../get-started/creating-windows-applications.md#bkmk_mdm-msi). |
| **Görev dizisi** | Sürüm 2002 ' den başlayarak, görev dizilerini kullanarak karmaşık uygulamaları yükleme veya kaldırma. Daha fazla bilgi için bkz. [görev dizisi dağıtım türü](../get-started/creating-windows-applications.md#bkmk_tsdt). <!--3555953--> |

> [!NOTE]
> Configuration Manager konsolu diğer dağıtım türlerini görüntüleyebilir, ancak artık desteklenmesiz platformlar içindir. Daha fazla bilgi için bkz. [karma 'e ne oldu?](../../mdm/understand/what-happened-to-hybrid.md).

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a> Note 1: Windows uygulama paketi (Windows Mağazası 'nda)

Uygulamayı Windows Mağazası 'na bir bağlantı olarak dağıtmak için, Grup İlkesi 'ni **Mağaza uygulamasını**Kapat ' ı yapılandırın. Bu ilkeyi **devre dışı** veya **yapılandırılmamış**olarak ayarlayın. Bu ayarı etkinleştirirseniz istemciler, uygulamaları indirmek ve yüklemek üzere Windows Mağazası 'na bağlanamaz.

Windows istemcileri, diğer dağıtım türlerinden önce bir mağazaya bağlantı kullanan dağıtım türlerini her zaman değerlendirir. Ardından istemci, dağıtım türlerini önceliğe göre değerlendirir.

> [!TIP]
> Bazı mağaza bağlantıları uygulama oluşturma sihirbazında şu hataya neden olabilir: "geçersiz uygulama bağlantısı". Örneğin, bazı mağaza *öne çıkan uygulamalar* bu hataya neden olabilir. Sihirbazın **genel** sayfasında **İleri ' yi** hala seçebilirsiniz. Configuration Manager uygulamayı başarıyla oluşturur ve başarıyla dağıtabilirsiniz.<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>Sonraki adımlar

Configuration Manager bir uygulama oluşturduktan sonra, bir sonraki adım [uygulamayı dağıtmaktır](deploy-applications.md).

Sürüm 1906 ' den başlayarak, bir kullanıcı veya cihaz koleksiyonuna tek bir dağıtım olarak gönderebilmeniz için bir uygulama grubu oluşturun. Daha fazla bilgi için bkz. [uygulama grupları oluşturma](create-app-groups.md).

Farklı işletim sistemi platformlarında uygulama oluşturma hakkında daha fazla bilgi için aşağıdaki makalelere bakın:  

- [Windows uygulamaları oluşturma](../get-started/creating-windows-applications.md)
- [Mac uygulamaları oluşturma](../get-started/creating-mac-computer-applications.md)
- [Linux ve UNIX sunucu uygulamaları oluşturma](../get-started/creating-linux-and-unix-server-applications.md)
- [Windows Embedded uygulamaları oluşturma](../get-started/creating-windows-embedded-applications.md)