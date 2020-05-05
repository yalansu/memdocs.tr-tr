---
title: İçerik kitaplığı
titleSuffix: Configuration Manager
description: Dağıtılan içeriğin genel boyutunu azaltmak için Configuration Manager tarafından kullanılan içerik kitaplığı hakkında bilgi edinin.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 253de522937e48fa1f3939c7303faf7e43e4e047
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720901"
---
# <a name="the-content-library-in-configuration-manager"></a>Configuration Manager içerik kitaplığı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İçerik kitaplığı, Configuration Manager içeriğin tek örnekli bir deposudur. Site, dağıttığınız içeriğin birleştirilmiş gövdesinin genel boyutunu azaltmak için onu kullanır. İçerik kitaplığı, yazılım dağıtımları için tüm içerik dosyalarını depolar, örneğin: yazılım güncelleştirmeleri, uygulamalar ve işletim sistemi dağıtımları.  

- Site, her site sunucusunda ve her dağıtım noktasında içerik kitaplığının bir kopyasını otomatik olarak oluşturur ve saklar.  

- Configuration Manager, site sunucusuna içerik dosyaları eklemeden veya dosyaları dağıtım noktalarına kopyalamayacak şekilde, her bir içerik dosyasının zaten içerik kitaplığında olup olmadığını doğrular.  

- İçerik dosyası kullanılabiliyorsa Configuration Manager dosyayı kopyalamaz. Bunun yerine, var olan içerik dosyasını uygulama veya paketle ilişkilendirir.  

Dağıtım noktası sunucularında, aşağıdaki seçenekleri yapılandırın:

- İçerik kitaplığını oluşturmak istediğiniz bir veya daha fazla disk sürücüsü.  

- Kullandığınız her sürücü için bir öncelik.  

Configuration Manager, bu sürücü, belirttiğiniz en az miktarda boş alan içerene kadar içerik dosyalarını sürücüye en yüksek önceliğe sahip olacak şekilde kopyalar.  

- Sürücü ayarlarını, dağıtım noktası yüklemesi sırasında yapılandırırsınız.  

- Yükleme bittikten sonra dağıtım noktası özelliklerindeki sürücü ayarlarını yapılandıramazsınız.  

Dağıtım noktası için sürücü ayarlarının nasıl yapılandırılacağı hakkında daha fazla bilgi için bkz. [içeriği ve içerik altyapısını yönetme](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

> [!IMPORTANT]
> Yükleme sonrasında içerik kitaplığını bir dağıtım noktasındaki farklı bir konuma taşımak için Configuration Manager araçlarında **Içerik kitaplığı aktarma** aracını kullanın. Daha fazla bilgi için bkz. [Içerik kitaplığı aktarım aracı](../../support/content-library-transfer.md).  


## <a name="about-the-content-library-on-the-central-administration-site"></a>Merkezi yönetim sitesindeki içerik kitaplığı hakkında

Configuration Manager, varsayılan olarak, site yüklenirken merkezi yönetim sitesinde bir içerik kitaplığı oluşturur. İçerik kitaplığı, en fazla boş disk alanına sahip site sunucusunun sürücüsüne yerleştirilir. Merkezi yönetim sitesine bir dağıtım noktası yükleyemiyoruz, sürücülerin içerik kitaplığı tarafından kullanılması için önceliklendirmez. Diğer site sunucularındaki ve dağıtım noktalarındaki içerik kitaplığına benzer şekilde, içerik kitaplığını içeren sürücüde kullanılabilir disk alanı tükendiği zaman, içerik kitaplığı otomatik olarak bir sonraki kullanılabilir sürücüye yayılır.  

Configuration Manager, aşağıdaki senaryolarda merkezi yönetim sitesindeki içerik kitaplığını kullanır:  

- Merkezi yönetim sitesinde içerik oluşturursunuz  

- Başka bir Configuration Manager sitesinden içerik geçirin ve merkezi yönetim sitesini bu içeriği yöneten site olarak atarsınız  

> [!NOTE]  
> Birincil bir sitede içerik oluşturup, farklı bir birincil siteye veya bir ikincil siteye dağıttığınızda, merkezi yönetim sitesi bu içeriği Merkezi yönetim sitesindeki Zamanlayıcı gelen kutusuna geçici olarak depolar, ancak bu içeriği içerik kitaplığına eklemez.  

Merkezi yönetim sitesindeki içerik kitaplığını yönetmek için aşağıdaki seçenekleri kullanın:  

- İçerik kitaplığının belirli bir sürücüye yüklenmesini engellemek için **no_sms_on_drive. SMS**adlı boş bir dosya oluşturun. İçerik kitaplığı oluşturulmadan önce bu dosyayı sürücünün köküne kopyalayın.  

- İçerik kitaplığı oluşturulduktan sonra, içerik kitaplığının konumunu yönetmek için Configuration Manager araçlarından **Içerik kitaplığı aktarma** aracını kullanın. Daha fazla bilgi için bkz. [Içerik kitaplığı aktarım aracı](../../support/content-library-transfer.md).  

> [!Note]  
> Bulut dağıtım noktaları, tek örnekli depolama kullanmaz. Site, Azure 'a göndermeden önce paketleri şifreler ve her pakette benzersiz bir şifrelenmiş anahtar vardır. İki dosya özdeş olsa da şifrelenmiş sürümler aynı olmayacaktır.  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a>Site sunucusu için uzak içerik kitaplığı yapılandırma

<!--1357525-->
Sürüm 1806 ' den başlayarak, [site sunucusu yüksek kullanılabilirliği](../../servers/deploy/configure/site-server-high-availability.md) yapılandırmak veya merkezi yönetim veya birincil site sunucularınızda sabit disk alanı boşaltmak için, içerik kitaplığını başka bir depolama konumuna yeniden yerleştir. İçerik kitaplığını site sunucusundaki başka bir sürücüye, ayrı bir sunucuya veya bir depolama alanı ağında (SAN) hataya dayanıklı disklere taşıyın. Yüksek oranda kullanılabilir olduğundan bir SAN önerilir ve değişen içerik gereksinimlerinizi karşılamak için zaman içinde büyüyerek veya küçüldüğü esnek depolama sağlar. Daha fazla bilgi için bkz. [yüksek kullanılabilirlik seçenekleri](../../servers/deploy/configure/site-server-high-availability.md).

Uzak içerik kitaplığı, [site sunucusu yüksek kullanılabilirliği](../../servers/deploy/configure/site-server-high-availability.md)için bir önkoşuldur.

> [!Note]  
> Bu eylem yalnızca site sunucusundaki içerik kitaplığını hareket ettirir. Dağıtım noktalarındaki içerik kitaplığının konumunu etkilemez. 

> [!Tip]  
> Ayrıca, içerik kitaplığı dışındaki paket kaynak içeriğini yönetmeyi planlayın. Configuration Manager içindeki her yazılım nesnesinin bir ağ paylaşımında bir paket kaynağı vardır. Tüm kaynakları tek bir paylaşıma merkezileştirmeyi düşünün, ancak bu konumun gereksiz ve yüksek oranda kullanılabilir olduğundan emin olun.
>
> İçerik kitaplığını paket kaynaklarınızla aynı depolama birimine taşırsanız, bu birimi yinelenen verileri kaldırma için işaretleyemezsiniz. İçerik kitaplığı yinelenen verileri kaldırma 'yı desteklese de, paket kaynakları birimi tarafından desteklenmez. Daha fazla bilgi için bkz. [yinelenen verileri kaldırma](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>Önkoşullar  

- Site sunucusu bilgisayar hesabının, içerik kitaplığını taşıdığınız ağ yolu için **tam denetim** izinlerine sahip olması gerekir. Bu izin hem paylaşma hem de dosya sistemi için geçerlidir. Uzak sistemde yüklü bileşen yok.

- Site sunucusunun dağıtım noktası rolü olamaz. Dağıtım noktası ayrıca içerik kitaplığını kullanır ve bu rol, uzak bir içerik kitaplığını desteklemez. İçerik kitaplığını taşıdıktan sonra, dağıtım noktası rolünü site sunucusuna ekleyemezsiniz.  

> [!Important]  
> Birden çok site arasında paylaşılan ağ konumunu yeniden kullanmayın. Örneğin, hem bir merkezi yönetim sitesi hem de bir alt birincil site için aynı yolu kullanmayın. Bu yapılandırmanın içerik kitaplığını bozma olasılığı vardır ve yeniden oluşturmanız gerekir.<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>İçerik kitaplığını yönetme işlemi

1. Bir ağ paylaşımında içerik kitaplığı hedefi olarak bir klasör oluşturun. Örneğin, `\\server\share\folder`.  

    > [!Warning]  
    > Mevcut bir klasörü içerikle yeniden kullanmayın. Örneğin, paket kaynaklarınızla aynı klasörü kullanmayın. İçerik kitaplığını kopyalamadan önce, Configuration Manager var olan içeriği belirttiğiniz konumdan kaldırır.  

2. Configuration Manager konsolunda **Yönetim** çalışma alanına geçin. **Site yapılandırması**' nı genişletin, **siteler** düğümünü seçin ve siteyi seçin. Ayrıntılar bölmesinin alt kısmındaki **Özet** sekmesinde, **içerik kitaplığı**için yeni bir sütuna dikkat edin.  

3. Şeritte **Içerik kitaplığını Yönet** ' i seçin.  

4. Içerik kitaplığını Yönet penceresinde, **geçerli konum** alanı yerel sürücü ve yolu gösterir. **Yeni konum**için geçerli bir ağ yolu girin. Bu yol, sitenin içerik kitaplığını taşıdıkları konumdur. Paylaşımda zaten var olan bir klasör adı içermesi gerekir, örneğin, `\\server\share\folder`. **Tamam**’ı seçin.  

5. Ayrıntılar bölmesinin Özet sekmesindeki Içerik kitaplığı sütunundaki **durum** değerini aklınızda edin. Sitenin, içerik kitaplığını taşırken ilerlemesini göstermek için güncelleştirir.  

   - **Devam**ederken, **taşıma ilerlemesi (%)** değeri tamamlanma yüzdesini gösterir.  

        > [!Note]  
        > Büyük bir içerik kitaplığınız varsa, konsolunda bir süre boyunca ilerleme `0%` durumunu görebilirsiniz. Örneğin, 1 TB kitaplığı ile, başlamadan önce 10 GB kopyalaması gerekir `1%`. Kopyalanan dosya ve bayt sayısını gösteren **Distmgr. log**dosyasını gözden geçirin. Sürüm 1810 ' den başlayarak, günlük dosyasında kalan tahmini süre de gösterilir.

   - Bir hata durumu varsa, durum hatayı görüntüler. Genel hatalar **erişim engellendi** veya **disk dolu**' i içerir.  

   - Tamamlandığında, **tamamlanmış**' i görüntüler.  

     Ayrıntılar için **Distmgr. log dosyasına** bakın. Daha fazla bilgi için bkz. [site sunucusu ve site sistemi sunucu günlükleri](log-files.md#BKMK_SiteSiteServerLog).  

Bu işlemle ilgili daha fazla bilgi için bkz. [akış çizelgesi-içerik kitaplığını yönetme](manage-content-library-flowchart.md).

Site aslında içerik kitaplığı dosyalarını uzak konuma *kopyalar* . Bu işlem, site sunucusundaki özgün konumdaki içerik kitaplığı dosyalarını silmez. Alan boşaltmak için, bir yöneticinin bu özgün dosyaları el ile silmesi gerekir.

Özgün içerik kitaplığı iki sürücüye yayılmışsa, yeni hedefte tek bir klasöre birleştirilir.

Sürüm 1810 ' den başlayarak, kopyalama işlemi sırasında, **despooler** ve **distribution Manager** bileşenleri yeni paketleri işlemez. Bu eylem, taşırken içeriğin kitaplığa eklenmediğinden emin olmanızı sağlar. Ne olursa olsun, bu değişikliği sistem bakımı sırasında zamanlayın.

İçerik kitaplığını site sunucusuna geri taşımanız gerekiyorsa, bu işlemi tekrarlayın, ancak **Yeni konum**için yerel bir sürücü ve yol girin. Sürücüde zaten var olan bir klasör adı içermesi gerekir, örneğin, `D:\SCCMContentLib`. Özgün içerik hala mevcut olduğunda, işlem yapılandırmayı hızla site sunucusuna yerel konuma taşımakta.

> [!Tip]  
> İçeriği site sunucusundaki başka bir sürücüye taşımak için, **Içerik kitaplığı aktarma** aracını kullanın. Daha fazla bilgi için bkz. [Içerik kitaplığı aktarım aracı](../../support/content-library-transfer.md).  


## <a name="inside-the-content-library"></a>İçerik Kitaplığı içinde

> [!Warning]  
> Aşağıdaki bölüm yalnızca bilgilendirme amacıyla verilmiştir. İçerik kitaplığındaki herhangi bir dosyayı veya klasörü değiştirmeyin, eklemeyin veya kaldırmayın. Bunun yapılması paketleri, içerikleri veya içerik kitaplığını bir bütün olarak bozabilir. Eksik, bozuk veya geçersiz verilerden şüphelenirseniz, bu tür sorunları algılamak için Configuration Manager konsolundaki doğrulama özelliğini kullanın. Ardından sorunları düzeltmek için etkilenen içeriği yeniden dağıtın.

Varsayılan olarak, içerik kitaplığı **Sccmcontentlib**adlı bir klasördeki bir sürücünün kökünde depolanır. Bu klasör varsayılan olarak **Sccmcontentlib $** olarak paylaşılır. Klasör ve paylaşımın yanlışlıkla hasar oluşmasını engellemek için sınırlı izinleri vardır. Tüm değişiklikler Configuration Manager konsolundan yapılmalıdır. Bu klasörün içinde aşağıdaki nesneler vardır:  

- Paket kitaplığı (**PkgLib** klasörü): dağıtım noktasında hangi paketlerin mevcut olduğu hakkında bilgi.  

- Veri kitaplığı (**Veriıb** klasörü): paketlerin orijinal yapısıyla ilgili bilgiler.  

- Dosya kitaplığı (**Filelib** klasörü): paketteki orijinal dosyalar. Bu klasör genellikle depolamanın toplu birimini kullanır.  

![Configuration Manager içerik kitaplığına diyagrama genel bakış](media/content-library-overview.png)

> [!Tip]  
> İçerik kitaplığının içeriğine gitmek için Configuration Manager araçlarından **Içerik kitaplığı gezgin** aracını kullanın. İçeriği değiştirmek için bu aracı kullanamazsınız. Bunun yanı sıra doğrulama ve yeniden dağıtım olanağı da sağlar. Daha fazla bilgi için bkz. [Içerik kitaplığı Gezgini](../../support/content-library-explorer.md).  

### <a name="package-library"></a>Paket kitaplığı

Paket kitaplığı klasörü, **PkgLib**, dağıtım noktasına dağıtılan her bir paket için bir dosya içerir. Dosya adı paket KIMLIĞIDIR, örneğin, `ABC00001.INI`. Bu dosyada, `[Packages]` bölümünde, paketin parçası olan içerik kimliklerinin yanı sıra sürüm gibi diğer bilgiler yer alan bir listesidir. Örneğin, **ABC00001** sürüm **1**' deki eski bir pakettir. Bu dosyadaki içerik KIMLIĞI `ABC00001.1`.

### <a name="data-library"></a>Veri kitaplığı

Veri kitaplığı klasörü, oturum **bağlantısı**, her paketteki içerik için bir dosya ve bir klasör içerir. Örneğin, bu dosya ve klasör sırasıyla ve `ABC00001.1.INI` `ABC00001.1`olarak adlandırılır. Dosya, doğrulama bilgilerini içerir. Klasör, özgün paketten klasör yapısını yeniden oluşturur.

Veri kitaplığındaki dosyalar, paketteki orijinal dosyanın adı ile birlikte ıNı dosyaları ile değiştirilmiştir. Örneğin, `MyFile.exe.INI`. Bu dosyalar, özgün dosya hakkında boyut, değiştirilme saati ve karma gibi bilgileri içerir. Dosya kitaplığındaki orijinal dosyayı bulmak için Karmadaki ilk dört karakteri kullanın. Örneğin, dosyam. exe. INI içindeki karma **DEF98765**ve ilk dört karakter **DEF9**' dir.

### <a name="file-library"></a>Dosya kitaplığı

İçerik kitaplığı birden çok sürücüye yayılmışsa, paket dosyaları bu sürücülerden herhangi birine **Filelib**dosya kitaplığı klasöründe olabilir.

Veri kitaplığında bulunan Karmadaki ilk dört karakteri kullanarak belirli bir dosyayı bulun. Dosya kitaplığı klasörünün içinde, her biri dört karakterli bir ada sahip birçok klasör vardır. Karmadan ilk dört karakterle eşleşen klasörü bulun. Bu klasörü bulduktan sonra, bir veya daha fazla üç dosya kümesi içerir. Bu dosyalar aynı adı paylaşır, ancak biri ıNı uzantısına sahiptir, biri bir uzantıya sahiptir ve birinin dosya uzantısı yoktur. Özgün dosya, adı veri kitaplığındaki karmaya eşit olan uzantısı olmayan bir uzantıdır.

Örneğin, **DEF9** klasörü, `DEF98765.INI` `DEF98765.SIG`ve `DEF98765`içerir. `DEF98765`özgün `MyFile.exe`. INı dosyası, aynı dosyayı paylaşan "kullanıcılar" veya içerik kimliklerinin bir listesini içerir. Bu içeriklerin tümü de kaldırılmadığı takdirde site bir dosyayı kaldırmaz.

### <a name="drive-spanning"></a>Sürücü yayma

İçerik kitaplığı birden çok sürücüye yayılmış olabilir. Dağıtım noktasını oluştururken bu sürücüleri seçersiniz. Varsayılan olarak, içerik kitaplığını yayıldığınızda sürücüleri otomatik olarak seçer Configuration Manager.

Sürücüleri seçerken, birincil ve ikincil bir sürücü seçin. Site tüm meta verileri birincil sürücüde depolar. Yalnızca dosya kitaplığını ikincil sürücüye yaymıştır. İkincil sürücüler için klasörün paylaşma adı, sürücü harfini içerir. Örneğin, D: ve E: içerik kitaplığı için ikincil sürücülerise, paylaşma adları **Sccmcontentlibd $** ve **sccmcontentliin $** olur.

**Otomatik** seçeneğini belirlediyseniz Configuration Manager en fazla kullanılabilir boş alana sahip sürücüyü birincil sürücüsüyle seçer. Bu sürücüdeki tüm meta verileri depolar. Site yalnızca dosya kitaplığını ikincil sürücülere yaymıştır.

Yapılandırma sırasında bir yedek alan miktarı belirtirsiniz. Configuration Manager en iyi kullanılabilir diskte yalnızca bu yedek alan miktarı boş bırakılır. Her yeni sürücü kullanım için seçildiğinde, en fazla kullanılabilir boş alana sahip olan sürücü seçilir.

Bir dağıtım noktasının belirli bir küme hariç tüm sürücüleri kullanması gerektiğini belirtemezsiniz. Adlı `NO_SMS_ON_DRIVE.SMS`sürücünün kökünde boş bir dosya oluşturarak bu davranışı önleyin. Bu dosyayı, kullanım için sürücüyü seçmeden Configuration Manager önce yerleştirin. Configuration Manager bu dosyayı sürücünün kökünde algılarsa, içerik kitaplığı sürücüsünü kullanmaz.


## <a name="troubleshooting"></a>Sorun giderme

Aşağıdaki ipuçları, içerik kitaplığıyla ilgili sorunları gidermenize yardımcı olabilir:  

- Hatalara yönelik işaretçiler için site sunucusundaki günlükleri (**Distmgr. log** ve **PkgXferMgr. log**) ve dağıtım noktasını (**Smsdpprov. log**) gözden geçirin.  

- [Içerik kitaplığı gezgin](../../support/content-library-explorer.md) aracını kullanın.  

- Virüsten koruma yazılımı gibi diğer işlemlere yönelik dosya kilitlerini denetleyin. Tüm sürücülerdeki içerik kitaplığını otomatik virüsten koruma taramalarının yanı sıra her sürücüdeki geçici hazırlama dizinini **SMS_DP $**, hariç tutun.  

- Karma uyuşmazlıkları olup olmadığını görmek için Configuration Manager konsolundan paketi doğrulayın.  

- Son seçenek olarak, içeriği yeniden dağıtır. Bu eylem çoğu sorunu çözmelidir.  
