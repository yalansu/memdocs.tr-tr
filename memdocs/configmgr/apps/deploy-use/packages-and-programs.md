---
title: Paketler ve programlar
titleSuffix: Configuration Manager
description: Configuration Manager olan eski paketleri ve programları kullanan dağıtımları destekler.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2c125212a13790e196d001f53411633d1e42d4f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710114"
---
# <a name="packages-and-programs-in-configuration-manager"></a>Configuration Manager paket ve programlar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, Configuration Manager 2007 ' de kullanılan paketleri ve programları desteklemeye devam eder. Aşağıdaki araçlardan veya betiklerin birini dağıtırken, paket ve programları kullanan bir dağıtım bir uygulamadan daha uygun olabilir:  

- Bir bilgisayara uygulama yüklememe yönetim araçları
- Sürekli olarak izlenmesi gerekmeyen "bir kerelik" betikler  
- Yinelenen bir zamanlamaya göre çalışan ve küresel değerlendirmeyi kullanmıyorum betikler

> [!TIP]  
> Configuration Manager konsolundaki [betikler](create-deploy-scripts.md) özelliğini kullanmayı göz önünde bulundurun. Betikler, paket ve programları kullanmak yerine, önceki senaryolardan bazılarına yönelik daha iyi bir çözüm olabilir.

Configuration Manager önceki bir sürümünden paket geçirdiğinizde, bunları Configuration Manager hiyerarşinizde dağıtabilirsiniz. Geçiş tamamlandığında, paketler **Yazılım Kitaplığı** çalışma alanındaki **Paketler** düğümünde görünür.

Bu paketleri, yazılım dağıtımını kullanarak yaptığınız gibi değiştirebilir ve dağıtabilirsiniz. **Tanımdan Paket Içeri aktarma Sihirbazı** eski paketleri içeri aktarmak için Configuration Manager ' de kalır. Configuration Manager 2007 ' den Configuration Manager hiyerarşisine geçiş yaptığınızda reklamlar dağıtıma dönüştürülür.  

> [!NOTE]  
> Paketleri ve programları Configuration Manager uygulamalarına dönüştürmek için Paket Dönüştürme Yöneticisi 'ni kullanın.  
>
> Sürüm 1806 ' den başlayarak, Paket Dönüştürme Yöneticisi Configuration Manager ile tümleşiktir. Daha fazla bilgi için bkz. [Paket Dönüştürme Yöneticisi](../pcm/package-conversion-manager.md).  

Paketler, Configuration Manager dağıtım noktası grupları ve izleme gibi bazı yeni özellikleri kullanabilir. Microsoft Application Virtualization (App-V) uygulamalarını Configuration Manager paket ve programlarla dağıtamazsınız. Sanal uygulamaları dağıtmak için bunları Configuration Manager uygulamalar olarak oluşturun. Daha fazla bilgi için bkz. [App-V sanal uygulamalarını dağıtma](../get-started/deploying-app-v-virtual-applications.md).  


## <a name="create-a-package-and-program"></a>Paket ve program oluşturma

### <a name="use-the-create-package-and-program-wizard"></a>Paket ve program oluşturma Sihirbazı 'nı kullanma

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **paketler** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **paket oluştur**' u seçin.  

3. **Paket ve program oluşturma Sihirbazı**' nın **paket** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Ad**: paket için en fazla 50 karakter uzunluğunda bir ad belirtin.  

    - **Açıklama**: Bu paket için en fazla 128 karakter içeren bir açıklama belirtin.  

    - **Üretici** (isteğe bağlı): Configuration Manager konsolunda paketi tanımlamanızı sağlayacak bir üretici adı belirtin. Bu ad, en çok 32 karakter uzunluğunda olabilir.

    - **Dil** (isteğe bağlı): paketin dil sürümünü en fazla 32 karakter olacak şekilde belirtin.  

    - **Sürüm** (isteğe bağlı): paket için en fazla 32 karakter içeren bir sürüm numarası belirtin.

    - **Bu paket kaynak dosyaları içerir**: Bu ayar, paketin istemci cihazlarda kaynak dosyalarının mevcut olmasını gerektirip gerektirmediğini belirtir. Varsayılan olarak, sihirbaz bu seçeneği etkinleştirmez ve Configuration Manager paket için dağıtım noktaları kullanmaz. Bu seçeneği belirlediğinizde, dağıtım noktalarına dağıtılacak paket içeriğini belirtin.  

    - **Kaynak klasörü**: paket kaynak dosyaları Içeriyorsa, **kaynak klasörünü ayarla** iletişim kutusunu açmak için, **Araştır** ' ı seçin ve ardından paketin kaynak dosyalarının konumunu belirtin.  

        > [!NOTE]  
        > Site sunucusunun bilgisayar hesabı, belirttiğiniz kaynak klasör için okuma erişimi haklarına sahip olmalıdır.  

    - Sürüm 1906 ' den başlayarak, bir istemcideki içeriği önceden önbelleğe almak istiyorsanız paketin **mimarisini** ve **dilini** belirtin. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../../osd/deploy-use/configure-precache-content.md).<!--4224642-->  

4. **Paket ve program oluşturma Sihirbazı**' nın **program türü** sayfasında, oluşturulacak programın türünü seçin ve ardından **İleri**' yi seçin. [Bilgisayar](#create-a-standard-program) veya [cihaz](#create-a-device-program)için bir program oluşturabilir ya da bu adımı atlayabilir ve daha sonra bir program oluşturabilirsiniz.  

    > [!TIP]  
    > Mevcut bir pakete yönelik yeni bir program oluşturmak için önce paketi seçin. Ardından, **giriş** sekmesinde, **paket** grubunda program oluştur ' **u seçerek** **program oluşturma Sihirbazı**' nı açın.  

#### <a name="create-a-standard-program"></a>Standart program oluşturma

1. **Paket ve program oluşturma Sihirbazı**' nın **program türü** sayfasında, **standart program**' ı seçin ve ardından **İleri**' yi seçin.  

2. **Standart program** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Ad**: Program için en çok 50 karakter uzunluğunda bir ad belirtin.  

        > [!NOTE]  
        > Program adı, paket içinde benzersiz olmalıdır. Bir program oluşturduktan sonra adını değiştiremezsiniz.  

    - **Komut satırı**: Bu programı başlatmak için kullanılacak komut satırını girin veya dosya konumuna gitmek için **Araştır** ' ı seçin.  

        Bir dosya adı için uzantı belirtmezseniz, Configuration Manager. com,. exe ve. bat dosyalarını olası uzantılar olarak kullanmaya çalışır.  

        İstemci programı çalıştırdığında, Configuration Manager dosyayı aşağıdaki konumlarda arar:

        - Paket içinde
        - Yerel Windows klasörü
        - Yerel *% Path%*

        Dosyayı bulamazsa, program başarısız olur.  

    - **Başlangıç klasörü** (isteğe bağlı): 127 karaktere kadar programın çalıştırıldığı klasörü belirtin. Bu klasör, istemci üzerinde mutlak bir yol olabilir. Ayrıca, paketi içeren dağıtım noktası klasörüyle ilişkili bir yol da olabilir.

    - **Çalıştır**: programın istemci bilgisayarlarda çalışacağı modu belirtin. Aşağıdaki seçeneklerden birini belirtin:  

        - **Normal**: program, sistem ve program varsayılanlarına bağlı olarak normal modda çalışır. Bu varsayılan moddur.  

        - **Küçültülmüş**: program, istemci cihazlarda simge durumuna küçültülmüş olarak çalıştırılır. Kullanıcılar yükleme etkinliğini bildirim alanında veya görev çubuğunda görebilir.  

        - **Ekranı kaplamış**: program, istemci cihazlarda ekranı kaplamış olarak çalışır. Kullanıcılar tüm yükleme etkinliklerini görür.  

        - **Gizli**: program, istemci cihazlarda gizli olarak çalıştırılır. Kullanıcılar herhangi bir yükleme etkinliği görmez.  

    - **Program çalışabilir**: programın yalnızca bir Kullanıcı oturum açmış olduğunda, yalnızca Kullanıcı oturumu açık olduğunda mı yoksa bir kullanıcının istemci bilgisayarda oturum açmış olmasına bakılmaksızın mi çalışacağını belirtin.  

    - **Çalıştırma modu**: programın, yönetim izinleriyle mi yoksa o anda oturum açmış kullanıcının izinleriyle mi çalışacağını belirtin.  

    - **Kullanıcıların program yüklemesini görüntülemesine ve etkileşime girmesine Izin ver**: varsa bu ayarı, kullanıcıların program yüklemesiyle etkileşime girmesine izin verilip verilmeyeceğini belirtmek için kullanın. Bu seçenek yalnızca aşağıdaki koşullar karşılandığında kullanılabilir:

        - **Program** , **yalnızca hiçbir Kullanıcı oturum açmadığında** veya **Kullanıcı oturum açmış olsun ya da** Açmadığınızda ayar çalıştırılabilir
        - **Çalıştırma modu** ayarı, **Yönetim haklarıyla çalıştırılır**  

    - **Sürücü modu**: Bu programın ağ üzerinde nasıl çalıştığı hakkında bilgi belirtin. Aşağıdaki seçeneklerden birini belirleyin:  

        - **UNC adıyla çalışır**: programın bir evrensel adlandırma KURALı (UNC) adıyla çalışacağını belirtin. Bu varsayılan ayardır.  

        - **Sürücü harfi gerektirir**: programın konumunu tam olarak nitelemek için bir sürücü harfi gerektirdiğini belirtin. Bu ayar için Configuration Manager, istemcideki kullanılabilir herhangi bir sürücü harfini kullanabilir.  

        - **Belirli bir sürücü harfi gerektirir**: programın konumunu tam olarak nitelemek için belirttiğiniz belirli bir sürücü harfi gerektirdiğini belirtin. Örneğin, **Z:**. İstemci zaten belirtilen sürücü harfini kullanıyorsa, program çalıştırılmaz.  

    - **Oturum açıldığında dağıtım noktasına yeniden bağlan**: Kullanıcı oturum açtığında istemcinin dağıtım noktasına bağlanıp bağlanmadığını belirtin. Varsayılan olarak, sihirbaz bu seçeneği etkinleştirmez.

3. **Paket ve program oluşturma Sihirbazı '** nın **gereksinimler** sayfasında, aşağıdaki bilgileri belirtin:  

    - **Önce başka bir program çalıştır**: Bu paket ve program çalıştırılmadan önce çalışan bir paket ve program tanımla.  

    - **Platform gereksinimleri**: **Bu program herhangi bir platformda çalışabilir '** i seçin veya **Bu program yalnızca belirtilen platformlarda çalışabilir**. Ardından, istemcilerin bu paketi ve programı yüklemek için sahip olması gereken işletim sistemi sürümlerini seçin.  

    - **Tahmini disk alanı**: Programın bilgisayarda çalışması için gereken disk alanı miktarını belirtin. Varsayılan ayar **bilinmiyor**. Gerekirse, sıfırdan büyük veya sıfıra eşit bir tamsayı belirtin. Değer ayarlarsanız, değer için birim ' i de seçin.  

    - **İzin verilen en fazla çalışma süresi (dakika)**: programın istemci bilgisayarda çalıştırılmasını bekleen uzun süreyi belirtin. Varsayılan değer **120** dakikadır. Yalnızca sıfırdan büyük tamsayılar kullanın.  

        > [!IMPORTANT]  
        > Bu programı dağıttığınız koleksiyonda bakım pencerelerini kullanıyorsanız, **izin verilen en fazla çalışma süresi** zamanlanan bakım penceresinden daha uzunsa bir çakışma meydana gelebilir. Maksimum çalışma süresini **bilinmiyor**olarak ayarlarsanız, program bakım penceresi sırasında çalışmaya başlar. Ardından bakım penceresi kapatıldıktan sonra gerekirse çalışmaya devam eder. En fazla çalışma süresini kullanılabilir bakım penceresi uzunluğundan daha büyük olan belirli bir döneme ayarlarsanız, istemci programı çalıştırmaz.  

        Bu değeri **bilinmiyor**olarak ayarlarsanız Configuration Manager izin verilen en fazla çalışma süresini 12 saat (720 dakika) olarak ayarlar.  

        > [!NOTE]  
        > Program en uzun çalışma süresini aşarsa, aşağıdaki koşullar karşılandığında Configuration Manager bunu sonlandırır:
        >
        > - **Yönetici haklarıyla çalıştırma** seçeneğini etkinleştirirsiniz
        > - **Kullanıcıların program yüklemesini görüntülemesine ve etkileşime girmesine Izin verme** seçeneğini etkinleştirmeyin  

#### <a name="create-a-device-program"></a>Cihaz programı oluşturma  

1. **Paket ve program oluşturma Sihirbazı**' nın **program türü** sayfasında **cihaz için program**' ı seçin ve ardından **İleri**' yi seçin.  

2. **Cihaz Için program** sayfasında, aşağıdaki ayarları belirtin:  

    - **Ad**: program için en fazla 50 karakter uzunluğunda bir ad belirtin.  

        > [!NOTE]  
        > Program adı, paket içinde benzersiz olmalıdır. Bir program oluşturduktan sonra adını değiştiremezsiniz.  

    - **Açıklama** (isteğe bağlı): Bu cihaz programı için en fazla 127 karakter içeren bir açıklama belirtin.  

    - **İndirme klasörü**: cihazdaki, paket kaynak dosyalarını depolayabileceği klasörün adını belirtin. Varsayılan değer: `\Temp\`.  

    - **Komut satırı**: Bu programı başlatmak için kullanılacak komut satırını girin. Dosya konumuna gitmek için, **Araştır**' ı seçin.  

    - **İndirme klasöründe komut satırını Çalıştır**: programı indirme klasöründen çalıştırmak için bu seçeneği belirleyin.  

    - **Komut satırını bu klasörden Çalıştır**: programın çalıştırılacağı farklı bir klasör belirtmek için bu seçeneği belirleyin.  

3. **Gereksinimler** sayfasında, aşağıdaki ayarları belirtin:  

    - **Tahmini disk alanı**: yazılım için gerekli olan disk alanı miktarını belirtin. İstemci, programı yüklemeden önce mobil cihaz kullanıcılarına bu değeri görüntüler.  

    - **Programı indir**: mobil cihazın bu programı ne zaman indirebileceğiniz hakkında bilgi belirtin. **Hemen**, **Yalnızca hızlı bir ağ üzerinden** veya **Yalnızca cihaz yerleşik olduğunda** seçeneklerinden birini belirtebilirsiniz.  

    - **Ek gereksinimler**: Bu program için tüm ek gereksinimleri belirtin. Kullanıcılar yazılımı yüklemeden önce bu gereksinimleri görür. Örneğin, kullanıcılara programı çalıştırmadan önce diğer tüm uygulamaları kapatmaları gerektiğini bildirebilirsiniz.  

## <a name="deploy-packages-and-programs"></a>Paket ve program dağıtma  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **paketler** düğümünü seçin.  

2. Dağıtmak istediğiniz paketi seçin. Şeridin **giriş** sekmesinde, **dağıtım** grubunda, **Dağıt**' ı seçin.  

3. **Yazılım Dağıtma Sihirbazı**'nın **genel** sayfasında, dağıtmak istediğiniz paket ve programın adını belirtin. Paketi ve programı dağıtmak istediğiniz koleksiyonu ve tüm isteğe bağlı açıklamaları seçin.  

    Paket içeriğini koleksiyonun varsayılan dağıtım noktası grubunda depolamak için **Bu koleksiyonla ilişkili varsayılan dağıtım noktası gruplarını kullan**seçeneğini belirleyin. Bu koleksiyonu bir dağıtım noktası grubuyla ilişkilendirmediyseniz, bu seçenek kullanılamaz.  

4. **İçerik** sayfasında **Ekle**' yi seçin. Bu paket ve program için içeriği dağıtmak istediğiniz dağıtım noktalarını veya dağıtım noktası gruplarını seçin.  

5. **Dağıtım ayarları** sayfasında, aşağıdaki ayarları yapılandırın:  

    - **Amaç**: aşağıdaki seçeneklerden birini belirleyin:

        - **Kullanılabilir**: Kullanıcı, yayımlanan paketi ve programı yazılım merkezi 'nde görür ve isteğe bağlı olarak yükleyebilir.  

        - **Gerekli**: paket ve program, yapılandırılmış zamanlamaya göre otomatik olarak dağıtılır. Yazılım Merkezi 'nde, dağıtım durumunu izleyebilir ve son tarihten önce yükleyebilirsiniz.  

        > [!NOTE]
        > Cihazda birden çok kullanıcı oturum açmışsa, paket ve görev sırası dağıtımları yazılım merkezi 'nde görünmeyebilir.

    - **Uyandırma paketleri gönder**: dağıtım amacını **gerekli** olarak ayarlarsanız ve bu seçeneği belirlerseniz, site önce yükleme son tarihinde bilgisayarlara bir uyandırma paketi gönderir. Bu seçeneği kullanabilmeniz için LAN'da Uyandırma bilgisayarları yapılandırın. Daha fazla bilgi için bkz. [LAN 'Da uyandırma yapılandırma](../../core/clients/deploy/configure-wake-on-lan.md).  

    - **Tarifeli bir Internet bağlantısı kullanan istemcilerin, yükleme son tarihinden sonra içerik indirmelerine izin ver, bu da ek ücret doğurmayabilir**  

    > [!NOTE]  
    > Bir paket ve program dağıttığınızda, **kullanıcının birincil cihazına yazılım ön dağıtımı** seçeneği kullanılamaz.  

6. **Zamanlama** sayfasında bu paketin ve programın istemci cihazlara ne zaman dağıtılacağını yapılandırın.  

    Bu sayfadaki seçenekler, dağıtım eyleminin **kullanılabilir** veya **gerekli**olarak ayarlanmış olmasına bağlı olarak değişir.  

    **Gerekli** dağıtımlar için programın yeniden çalıştırma davranışını **yeniden çalıştırma davranışı** açılan menüsünden yapılandırın. Aşağıdaki seçeneklerden birini seçin:  

    | Yeniden çalıştırma davranışı | Açıklama |
    |----------------|-------------|
    | **Dağıtılan programı asla yeniden çalıştırma** | İstemci programı yeniden çalıştırmaz. Program başlangıçta başarısız olsa veya program dosyaları değiştirilse bile bu davranış oluşur. |
    | **Programı her zaman yeniden çalıştır** | Dağıtım zamanlandığında istemci her zaman programı yeniden çalıştırır. Program zaten başarıyla çalıştırılmış olsa bile bu davranış oluşur. Programı güncelleştirdiğinizde yinelenen dağıtımlar yararlı olur. |
    | **Önceki deneme başarısız olursa yeniden çalıştır** | Dağıtım zamanlandığında istemci, yalnızca önceki çalıştırma denemesinde başarısız olduysa programı yeniden çalıştırır. |
    | **Önceki deneme başarılı olursa yeniden çalıştır** | İstemci, yalnızca daha önce istemcide başarıyla çalıştırıldıysa programı yeniden çalıştırır. Bu davranış, programın düzenli olarak güncelleştirilmesi sırasında yinelenen dağıtımlarla faydalıdır ve her güncelleştirme, önceki güncelleştirmenin başarıyla yüklenmesini gerektirir. |

7. **Kullanıcı Deneyimi** sayfasında aşağıdaki bilgileri belirtin:  

    - **Kullanıcıların programı atamalardan bağımsız olarak çalıştırmasına Izin ver**: kullanıcılar bu yazılımı, zamanlanmış yükleme zamanından bağımsız olarak yazılım merkezi 'nden yükleyebilir.  

    - **Yazılım yükleme**: Yazılımın yapılandırılmış herhangi bir bakım penceresinin dışında yüklenmesine olanak sağlar.  

    - **Sistem yeniden başlatma (yüklemeyi gerçekleştirmek için gerekliyse)**: yazılım yüklemesi için bir cihazın yeniden başlatılması gerekiyorsa, bu eylemin yapılandırılmış bakım pencerelerinin dışında çalışmasına izin verin.  

    - **Katıştırılmış cihazlar**: Yazma filtresi etkin Windows Embedded cihazlarına paket ve programlar dağıtırken, paket ve programları geçici katmana yüklemeyi ve değişiklikleri daha sonra gerçekleştirmeyi belirtebilirsiniz. Alternatif olarak, değişiklikleri yükleme son tarihinde veya bakım penceresi sırasında işleyin. Yükleme son tarihinde veya bakım penceresi sırasında değişiklikler yaptığınızda, yeniden başlatma gerekir ve değişiklikler cihazda kalır.  

        > [!NOTE]  
        > Windows Embedded cihazına bir paket veya program dağıttığınızda, cihazın yapılandırılmış bakım penceresine sahip bir koleksiyonun üyesi olduğundan emin olun. Windows Embedded cihazlarına paket ve program dağıtırken bakım pencerelerinin nasıl kullanıldığı hakkında daha fazla bilgi için bkz. [Windows Embedded uygulamaları oluşturma](../get-started/creating-windows-embedded-applications.md).  

8. **Dağıtım Noktaları** sayfasında aşağıdaki bilgileri belirtin:  

    - **Dağıtım seçenekleri**: bir istemcinin geçerli sınır grubunda bir dağıtım noktası kullandığında bu eylemi belirtin. Ayrıca, bir komşu sınır grubundaki veya varsayılan site sınır grubundaki bir dağıtım noktasını kullandığında istemci için eylemi seçin.

        > [!IMPORTANT]  
        > Dağıtım seçeneğini **programı dağıtım noktasından Çalıştır**olarak yapılandırırsanız, paket özelliklerinin **veri erişimi** sekmesinde **Bu paketteki içeriği dağıtım noktalarında bir paket paylaşımıyla kopyalama** seçeneğini etkinleştirdiğinizden emin olun. Aksi takdirde paket, dağıtım noktalarından çalıştırılamaz.  

    - **İstemcilerin varsayılan site sınır grubundaki dağıtım noktalarını kullanmasına Izin ver**: Bu içerik geçerli veya komşu sınır gruplarındaki herhangi bir dağıtım noktasından kullanılamadığında, site varsayılan sınır grubundaki dağıtım noktalarını denemeye izin vermek için bu seçeneği etkinleştirin.

9. Sihirbazı tamamlayın.  

Dağıtımı seçtiğinizde, **izleme** çalışma alanının **dağıtımlar** düğümünde ve paket dağıtımı sekmesinin Ayrıntılar bölmesinde dağıtımı görüntüleyin. Daha fazla bilgi için bkz. [paketleri ve programları izleme](#monitor-packages-and-programs).  


## <a name="monitor-packages-and-programs"></a>Paketleri ve programları izleme

Paket ve program dağıtımlarını izlemek için, uygulamaları [izleme](monitor-applications-from-the-console.md)bölümünde ayrıntılı olarak uygulamaları izlemek için kullandığınız yordamları kullanın.  

Paketler ve programlar, paketlerin ve programların dağıtım durumuyla ilgili bilgileri izlemenize olanak tanıyan çeşitli yerleşik raporlar da içerir. Bu raporlar, **Yazılım Dağıtımı – Paketler ve Programlar** ve **Yazılım Dağıtımı – Paket ve Program Dağıtımı Durumu** rapor kategorisindedir.  

Configuration Manager raporlamayı yapılandırma hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).  


## <a name="manage-packages-and-programs"></a>Paketleri ve programları yönetme

**Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin ve **paketler** düğümünü seçin. Yönetmek istediğiniz paketi seçin ve ardından bir yönetim görevi seçin.  

### <a name="create-prestage-content-file"></a>Önceden Hazırlanan İçerik Dosyası Oluşturma

Paket içeriğini içeren bir dosya oluşturmak için **önceden hazırlanan Içerik dosyası oluşturma Sihirbazı**' nı açar. Paketi uzak bir dağıtım noktasına el ile içeri aktarmak için bu dosyayı kullanın. Bu eylem, site sunucusu ve dağıtım noktası arasında düşük ağ bant genişliğiniz olduğunda faydalıdır.

### <a name="create-program"></a>Program Oluştur

Bu paket için yeni bir program oluşturmak üzere **program oluşturma Sihirbazı**' nı açar.

### <a name="export"></a>Dışarı Aktarma

Seçilen paketi ve içeriğini bir dosyaya aktarmak için **paket dışarı aktarma Sihirbazı**' nı açar. Dosyayı başka bir hiyerarşiye aktarmak için bu dosyayı kullanın.

Paket ve programları içeri aktarma hakkında daha fazla bilgi için bkz. [paket ve program oluşturma](#create-a-package-and-program).

### <a name="deploy"></a>Dağıtma

Seçilen paket ve programı bir koleksiyona dağıtmak için **Yazılım Dağıtma Sihirbazı**' nı açar. Daha fazla bilgi için bkz. [paketleri ve programları dağıtma](#deploy-packages-and-programs).

### <a name="distribute-content"></a>İçeriği dağıt

Bir paket ve program içeriğini seçili dağıtım noktalarına veya dağıtım noktası gruplarına göndermek için **Içerik Dağıtma Sihirbazı**' nı açar.

### <a name="update-distribution-points"></a>Dağıtım noktalarını güncelleştir

Dağıtım noktalarını, seçilen paket ve programa ait en son içeriklerle güncelleştirir.


## <a name="see-also"></a>Ayrıca bkz.

- [Betikler](create-deploy-scripts.md)

- [Paket Dönüştürme Yöneticisi](../pcm/package-conversion-manager.md)

- [Paket tanımı dosyaları](package-definition-files.md)
