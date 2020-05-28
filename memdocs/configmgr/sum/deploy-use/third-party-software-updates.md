---
title: Üçüncü taraf güncelleştirmelerini etkinleştir
titleSuffix: Configuration Manager
description: Configuration Manager üçüncü taraf güncelleştirmelerini etkinleştir
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5461f888bfa2b749061eef4000f0d7c5f756b84
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906740"
---
# <a name="enable-third-party-updates"></a>Üçüncü taraf güncelleştirmelerini etkinleştirme 

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sürüm 1806 ' den başlayarak, Configuration Manager konsolundaki **üçüncü taraf yazılım güncelleştirme katalogları** düğümü, üçüncü taraf kataloglara abone olmanızı, güncelleştirmelerini yazılım güncelleştirme noktanya (SUP) yayımlamanıza ve ardından bunları istemcilere dağıtmanıza olanak tanır.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> Configuration Manager Bu özelliği varsayılan olarak etkinleştirmez. Kullanmadan önce, **istemcilerde üçüncü taraf güncelleştirme desteğini etkinleştirmek**için isteğe bağlı özelliği etkinleştirin. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="prerequisites"></a>Ön koşullar 
- Üçüncü taraf yazılım güncelleştirmeleri için kaynak ikili içeriğini depolamak üzere en üst düzey yazılım güncelleştirme noktasının sunucusundaki WSUSContent klasöründe yeterli disk alanı.
    - Gerekli depolama alanı, satıcıya, güncelleştirme türlerine ve dağıtım için yayımladığınız belirli güncelleştirmelere göre farklılık gösterir.
    - Sunucusundaki WSUSContent klasörünü daha fazla boş alana sahip başka bir sürücüye taşımanız gerekiyorsa, [WSUS tarafından güncelleştirmelerin yerel olarak nasıl değiştirileceği](https://docs.microsoft.com/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally) blog gönderisine bakın.
- Üçüncü taraf yazılım güncelleştirme eşitleme hizmeti için internet erişimi gerekir.
    - İş ortağı katalogları listesi için HTTPS bağlantı noktası 443 üzerinden download.microsoft.com gerekir. 
    -  Üçüncü taraf kataloglara Internet erişimi ve içerik dosyalarını güncelleştirme. 443 dışındaki ek bağlantı noktaları gerekebilir.
    - Üçüncü taraf güncelleştirmeleri, SUP ile aynı proxy ayarlarını kullanır.


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Üst düzey site sunucusundan SUP uzakta olduğunda ek gereksinimler 

1. Uzakta olduğunda, SSL 'nin SUP üzerinde etkinleştirilmesi gerekir. Bu, bir iç sertifika yetkilisinden veya bir genel sağlayıcı aracılığıyla oluşturulan bir sunucu kimlik doğrulama sertifikası gerektirir.
    - [WSUS üzerinde SSL 'yi yapılandırma](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - WSUS üzerinde SSL yapılandırdığınızda, bazı Web Hizmetleri ve sanal dizinlerin her zaman HTTP ve HTTPS değil olduğunu not edin. 
        - Configuration Manager, WSUS içerik dizininden yazılım güncelleştirme paketleri için üçüncü taraf içeriği HTTP üzerinden indirir.   
    - [SUP üzerinde SSL yapılandırma](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Yazılım güncelleştirme noktası bileşen özelliklerindeki **sertifikayı Configuration Manager** , üçüncü taraf güncelleştirmeleri WSUS imza sertifikası yapılandırması ' na ayarlandığında, otomatik olarak imzalanan WSUS imza sertifikası oluşturulmasına izin vermek için aşağıdaki yapılandırmalar gereklidir: 
   - SUP sunucusunda uzak kayıt defteri etkinleştirilmelidir.
   -  **WSUS sunucusu bağlantı hesabı** , SUP/WSUS sunucusunda uzak kayıt defteri izinlerine sahip olmalıdır. 


3. Configuration Manager site sunucusunda aşağıdaki kayıt defteri anahtarını oluşturun: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, bir değeri olan **Enableselfsignedcertificates** adlı yenı bir DWORD oluşturun `1` . 

4. Otomatik olarak imzalanan WSUS imzalama sertifikasını, uzak SUP sunucusundaki Güvenilen Yayımcılar ve güvenilen kök depolarına yüklemeyi etkinleştirmek için:
   - **WSUS sunucusu bağlantı hesabı** , SUP sunucusunda uzaktan yönetim izinlerine sahip olmalıdır.

     Bu öğe mümkün değilse, sertifikayı yerel bilgisayarın WSUS deposundan güvenilen yayımcı ve güvenilen kök depolarına dışarı aktarın. 

> [!NOTE] 
>**WSUS sunucusu bağlantı hesabı** , SUP 'Nin site sistemi rolü özelliklerindeki **proxy ve hesap ayarları** sekmesi görüntülenirken belirlenebilir. Bir hesap belirtilmemişse, site sunucusunun bilgisayar hesabı kullanılır.

## <a name="enable-third-party-updates-on-the-sup"></a>SUP üzerinde üçüncü taraf güncelleştirmeleri etkinleştirin
Bu seçeneği etkinleştirirseniz, Configuration Manager konsolundaki üçüncü taraf güncelleştirme kataloglarına abone olabilirsiniz. Daha sonra bu güncelleştirmeleri WSUS 'de yayımlayabilir ve istemcilere dağıtabilirsiniz. Özelliği etkinleştirmek ve kullanmak üzere ayarlamak için aşağıdaki adımlar hiyerarşi başına bir kez çalıştırılmalıdır. Üst düzey SUP 'nin WSUS sunucusunu değiştirirseniz, adımların yeniden çalıştırılması gerekebilir. 

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.
2. Hiyerarşide en üst düzey siteyi seçin. Şeritte, **site bileşenlerini Yapılandır**' a tıklayın ve **yazılım güncelleştirme noktası**' nı seçin.
3. **Üçüncü taraf güncelleştirmeleri** sekmesine geçin. **üçüncü taraf yazılım güncelleştirmelerini etkinleştir**seçeneğini belirleyin.

    ![Üçüncü taraf güncelleştirmeleri SUP özellikleri ekran görüntüsü](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>WSUS imza sertifikasını yapılandırma
Otomatik olarak imzalanan bir sertifika kullanarak üçüncü taraf WSUS imzalama sertifikasını otomatik olarak yönetmesini mi yoksa sertifikayı el ile yapılandırmanız mı gerektiğini Configuration Manager belirlemeniz gerekir. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>WSUS imza sertifikasını otomatik olarak yönetme
PKI sertifikalarını kullanma gerekliliği yoksa, üçüncü taraf güncelleştirmeler için imza sertifikalarını otomatik olarak yönetmeyi tercih edebilirsiniz. WSUS sertifika yönetimi, eşitleme döngüsünün bir parçası olarak yapılır ve oturum açar `wsyncmgr.log` . 

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.
2. Hiyerarşide en üst düzey siteyi seçin. Şeritte, **site bileşenlerini Yapılandır**' a tıklayın ve **yazılım güncelleştirme noktası**' nı seçin.
3. **Üçüncü taraf güncelleştirmeleri** sekmesine geçin. **sertifikayı yönetmek Configuration Manager**seçeneği belirleyin. 
4. **Yönetim** çalışma alanındaki **güvenlik** altındaki **SERTIFIKALAR** düğümünde, **üçüncü taraf WSUS imzalama** türünde yeni bir sertifika oluşturulur.  

### <a name="manually-manage-the-wsus-signing-certificate"></a>WSUS imza sertifikasını el ile yönetme
Sertifikayı bir PKI sertifikası kullanma gereksinimi gibi el ile yapılandırmanız gerekirse, bunu yapmak için [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) ya da başka bir aracı kullanmanız gerekir.  

1. İmzalama sertifikasını [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server)kullanarak yapılandırın.
2. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.
3. Hiyerarşide en üst düzey siteyi seçin. Şeritte, **site bileşenlerini Yapılandır**' a tıklayın ve **yazılım güncelleştirme noktası**' nı seçin.
4. **Üçüncü taraf güncelleştirmeleri** sekmesine geçin. **sertifikayı el Ile yönetme**seçeneğini belirleyin.


## <a name="enable-third-party-updates-on-the-clients"></a>İstemcilerde üçüncü taraf güncelleştirmelerini etkinleştirme
İstemci ayarlarındaki istemcilerde üçüncü taraf güncelleştirmelerini etkinleştirin. Bu ayar, [Intranet Microsoft güncelleştirme hizmeti konumu için imzalı güncelleştirmelere Izin ver](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location)için Windows Update aracı ilkesini ayarlar. Bu istemci ayarı, WSUS imzalama sertifikasını istemcideki güvenilen yayımcı deposuna da yüklenir. Sertifika yönetimi günlüğü, istemcilerde ' de görülür `updatesdeployment.log` .  Üçüncü taraf güncelleştirmeler için kullanmak istediğiniz her özel istemci ayarı için bu adımları çalıştırın. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) makalesi.

1. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **istemci ayarları** düğümünü seçin.
2. Mevcut bir özel istemci ayarı seçin veya yeni bir tane oluşturun. 
3. Sol taraftaki **yazılım güncelleştirmeleri** sekmesini seçin. Bu sekmeye sahipseniz, **yazılım güncelleştirmeleri** kutusunun etkinleştirildiğinden emin olun.
4. **Üçüncü taraf yazılım güncelleştirmelerini** **Evet**olarak ayarlayın. 


## <a name="add-a-custom-catalog"></a>Özel katalog ekleme
*Iş ortağı katalogları* , bilgileri Microsoft 'a zaten kayıtlı olan yazılım satıcısı kataloglarıdır. İş ortağı katalogları ile herhangi bir ek bilgi belirtmeniz gerekmeden bunlara abone olabilirsiniz. Eklediğiniz kataloglara *özel kataloglar*denir. Configuration Manager için bir üçüncü taraf güncelleştirme satıcısından özel bir katalog ekleyebilirsiniz. Özel kataloglar HTTPS kullanmalıdır ve güncelleştirmelerin dijital olarak imzalanması gerekir. 

1. **Yazılım güncelleştirmeleri kitaplığı** çalışma alanına gidin, **yazılım güncelleştirmeleri**' ni genişletin ve **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü seçin. 
   
     ![Üçüncü taraf güncelleştirmeler düğümü ekran görüntüsü](media/third-party-updates-node.PNG)
2. Şeritte **özel Katalog Ekle** ' ye tıklayın. 

     ![Üçüncü taraf güncelleştirmeleri özel Katalog ekleme](media/third-party-updates-custom-catalog.png)
1. **Genel** sayfasında, aşağıdaki öğeleri belirtin: 
    - **İndirme URL 'si**: özel kataloğun GEÇERLI bir HTTPS adresi.
    - **Yayımcı**: kataloğu yayımlayan kuruluşun adı. 
    - **Ad**: Configuration Manager konsolunda görüntülenecek kataloğun adı. 
    - **Açıklama**: kataloğun açıklaması. 
    - **Destek URL 'si** (isteğe bağlı): katalogla ilgili yardım almak için bir Web sitesinin GEÇERLI bir HTTPS adresi. 
    - **Destek kişisi** (isteğe bağlı): Katalog hakkında yardım almak için iletişim bilgileri. 
2. Katalog özetini gözden geçirmek ve **üçüncü taraf yazılım güncelleştirmeleri özel katalog Sihirbazı 'nı**tamamlamaya devam etmek için **İleri** ' ye tıklayın.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Üçüncü taraf kataloğa abone olma ve güncelleştirmeleri eşitleme
Configuration Manager konsolundaki bir üçüncü taraf kataloğuna abone olduğunuzda, katalogdaki her güncelleştirme için meta veriler, SUPs 'niz için WSUS sunucularıyla eşitlenir. Meta verilerin eşitlenmesi, istemcilerin güncelleştirmelerden herhangi birinin uygulanabilir olup olmadığını belirlemesine izin verir. Abone olmak istediğiniz her bir üçüncü taraf kataloğu için aşağıdaki adımları gerçekleştirin:  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Yazılım güncelleştirmeleri** ' ni genişletin ve **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü seçin.  
2. Abone olmak için kataloğu seçin ve Şeritteki **kataloğa abone ol** ' a tıklayın. 
    ![Üçüncü taraf güncelleştirmeleri özel Katalog ekleme](media/third-party-updates-subscribe.png)
3. Katalog sertifikasını gözden geçirin ve onaylayın.  
   > [!NOTE]
   > 
   > Üçüncü taraf bir yazılım güncelleştirme kataloğuna abone olduğunuzda, sihirbazda gözden geçirmeniz ve onaylamanız gereken sertifika sitesine eklenir. Bu sertifika, **üçüncü taraf yazılım güncelleştirmeleri Kataloğu**türüdür. **Yönetim** çalışma alanındaki **güvenlik** altındaki **Sertifikalar** düğümünden yönetebilirsiniz.  
4. Sihirbazı tamamlayın. İlk abonelikle sonra katalog birkaç dakika içinde indirilmek üzere başlamalıdır. 
    - Katalog her 7 günde bir otomatik olarak eşitlenir.
    - Eşitlemeye zorlamak için şeritte **Şimdi Eşitle** ' ye tıklayın.
5. Katalog indirildikten sonra, ürün meta verilerinin WSUS veritabanından Configuration Manager veritabanına eşitlenmesi gerekir. Ürün bilgilerini eşitlemek için [yazılım güncelleştirmeleri eşitlemesini el ile başlatın](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) .
6. Ürün bilgileri eşitlendikten sonra, [istenen ürünü Configuration Manager EŞITLENECEK SUP 'Yi yapılandırın](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) .  
7. Yeni ürünün güncelleştirmelerini Configuration Manager Ile eşitlemek için [yazılım güncelleştirmeleri eşitlemesini el ile başlatın](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) .  
8. Eşitleme tamamlandığında, üçüncü taraf güncelleştirmelerini **tüm güncelleştirmeler** düğümünde görebilirsiniz. Bu güncelleştirmeler, yayımlamayı seçinceye kadar **yalnızca meta veri** güncelleştirmeleri olarak yayımlanır. 
     - Mavi oklu simge, yalnızca meta veri yazılım güncelleştirmesini ifade eder. ![Yalnızca meta veriler yazılım güncelleştirme simgesi](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Üçüncü taraf yazılım güncelleştirmelerini yayımlama ve dağıtma 
Üçüncü taraf güncelleştirmeleri **tüm güncelleştirmeler** düğümünden olduktan sonra, hangi güncelleştirmelerin dağıtım için yayımlanacak olduğunu seçebilirsiniz. Bir güncelleştirme yayımladığınızda, ikili dosyalar satıcıdan indirilir ve en üst düzey SUP üzerinde sunucusundaki WSUSContent dizinine yerleştirilir. 

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Yazılım güncelleştirmeleri** ' ni genişletin ve **tüm yazılım güncelleştirmeleri** düğümünü seçin.
2. Güncelleştirme listesini filtrelemek için **Ölçüt Ekle** ' ye tıklayın. Örneğin, **HP**için **satıcı** ekleyin. HP 'deki tüm güncelleştirmeleri görüntülemek için.  
3. Kuruluşunuz için gereken güncelleştirmeleri seçin. **Üçüncü taraf yazılım güncelleştirme Içeriğini Yayımla**' ya tıklayın.
    - Bu eylem, güncelleştirme ikili dosyalarını satıcıdan indirir ve en üst düzey yazılım güncelleştirme noktasındaki sunucusundaki WSUSContent klasöründe depolar. 
4. Yayımlanan güncelleştirmelerin durumunu yalnızca içeriğe sahip dağıtılabilir güncelleştirmelere değiştirmek için [yazılım güncelleştirmeleri eşitlemesini el ile başlatın](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) . 
    >[!NOTE]
    >Üçüncü taraf yazılım güncelleştirme içeriğini yayımladığınızda, içeriği imzalamak için kullanılan tüm sertifikalar siteye eklenir. Bu sertifikalar, **üçüncü taraf yazılım güncelleştirme içerikleri**türündedir. Bunları, **Yönetim** çalışma alanındaki **güvenlik** altındaki **Sertifikalar** düğümünden yönetebilirsiniz.  

5. SMS_ISVUPDATES_SYNCAGENT. log dosyasındaki ilerlemeyi gözden geçirin. Günlük, site sistem günlükleri klasöründeki en üst düzey yazılım güncelleştirme noktasında bulunur.
6. Güncelleştirmeleri, [yazılım güncelleştirmelerini dağıtma](../deploy-use/deploy-software-updates.md) işlemini kullanarak dağıtın. 
7. **Yazılım güncelleştirmelerini dağıtma Sihirbazı**'Nın **konum indir** sayfasında, **yazılım güncelleştirmelerini Internet 'ten indirmek**için varsayılan seçeneği belirleyin. Bu senaryoda içerik, dağıtım paketinin içeriğini indirmek için kullanılan yazılım güncelleştirme noktasına zaten yayımlandı.
8. Uyumluluk sonuçlarını görebilmeniz için istemcilerin bir tarama çalıştırması ve güncelleştirmeleri değerlendirmesi gerekir.  Bu döngüyü, **yazılım güncelleştirmeleri tarama çevrimi** eylemini çalıştırarak bir istemcideki Configuration Manager denetim masasından el ile tetikleyebilirsiniz.


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a>1910 ' den başlayarak üçüncü taraf güncelleştirme geliştirmeleri
<!--4469002-->
Artık üçüncü taraf güncelleştirme kataloglarının eşitlenmesi üzerinde daha ayrıntılı denetimleriniz vardır. Configuration Manager sürüm 1910 ' den başlayarak, her bir kataloğun eşitleme zamanlamasını bağımsız olarak yapılandırabilirsiniz. Kategorilere ayrılmış güncelleştirmeler içeren kataloglar kullanılırken, tüm kataloğun eşitlenmesini önlemek için eşitlemeyi yalnızca belirli güncelleştirme kategorilerini içerecek şekilde yapılandırabilirsiniz. Kategorilere ayrılmış kataloglar sayesinde, bir kategori dağıtacağınız zaman, bunu otomatik olarak indirip WSUS 'e yayımlayabilecek şekilde yapılandırabilirsiniz.

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>Yeni bir katalog aboneliğindeki bir kataloğun zamanlamasını ayarlama

1. **Yazılım kitaplığı** çalışma alanına gidin, **yazılım güncelleştirmeleri**' ni genişletin ve ardından **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü seçin.
1. Abone olmak için kataloğu seçin ve Şeritteki **kataloğa abone ol** ' a tıklayın.
1. Varsayılan eşitleme zamanlamasını geçersiz kılmak istiyorsanız **zamanlama** sayfasında seçeneklerinizi belirleyin:
   - **Basit zamanlama**: saat, gün veya ay aralığını seçin.
   - **Özel zamanlama**: karmaşık bir zamanlama ayarlayın.

### <a name="update-the-schedule-per-catalog"></a>Zamanlamayı Katalog başına güncelleştirme

1. **Yazılım kitaplığı** çalışma alanına gidin, **yazılım güncelleştirmeleri**' ni genişletin ve ardından **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü seçin.
1. Kataloğa sağ tıklayıp **Özellikler**' i seçin.
1. Zamanlama sekmesinde seçeneklerinizi belirleyin: 
   - **Basit zamanlama**: saat, gün veya ay aralığını seçin.
   - **Özel zamanlama**: karmaşık bir zamanlama ayarlayın.

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>Üçüncü taraf v3 kataloğuna yeni abonelik

> [!IMPORTANT]
> Bu seçenek yalnızca güncelleştirme kategorilerini destekleyen v3 üçüncü taraf güncelleştirme katalogları için kullanılabilir. Bu seçenekler, Yeni v3 biçiminde yayımlanmamış kataloglar için devre dışı bırakılmıştır.


1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Yazılım güncelleştirmeleri** ' ni genişletin ve **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü seçin.
1. Abone olmak için kataloğu seçin ve Şeritteki **kataloğa abone ol** ' a tıklayın.
1. **Kategorileri seçin** sayfasında seçeneklerinizi belirleyin:

   - **Tüm güncelleştirme kategorilerini eşitler** (varsayılan)
       - Üçüncü taraf güncelleştirme kataloğundaki tüm güncelleştirmeleri Configuration Manager olarak eşitler.
   -  **Eşitleme için kategorileri seçin**
       - Configuration Manager hangi kategorilerin ve alt kategorilerin eşitleneceğini seçin.

      ![Configuration Manager eşitlenmek üzere kategorileri Güncelleştir ' i seçin](./media/4469002-select-categories-for-sync.png)
1. Katalog için **güncelleştirme Içeriğini hazırlamak** istiyorsanız seçin. İçeriği aşamalandırdığınızda, seçili kategorilerdeki tüm güncelleştirmeler otomatik olarak en üst düzey yazılım güncelleştirme noktanya indirilir, bu da dağıtım öncesinde zaten indirildiklerinden emin olmanız gerekmez. Daha fazla bant genişliği ve depolama gereksinimini ortadan kaldırmak için, içeriği yalnızca sizin dağıtmanız gereken güncelleştirmeler için otomatik olarak aşamalandırmalısınız.

   - **İçerik aşamalamayın, yalnızca tarama için eşitlenir (önerilir)**
     - Üçüncü taraf katalogdaki güncelleştirmeler için herhangi bir içerik indirmeyin
   - **Seçili kategorilerin içeriğini otomatik olarak hazırlama**
     - İçeriği otomatik olarak indirecek güncelleştirme kategorilerini seçin.
     - Seçili kategorilerdeki güncelleştirmelerin içeriği en üst düzey yazılım güncelleştirme noktasının WSUS içerik dizinine indirilir.
      ![İçerik hazırlamak için kategorileri Güncelleştir ' i seçin](./media/4469002-stage-content.png)
1. Katalog eşitleme için **zamanlamanızı** ayarlayın ve Sihirbazı doldurun.

 

### <a name="edit-an-existing-subscription"></a>Mevcut bir aboneliği Düzenle

> [!IMPORTANT]
> Bu seçenek yalnızca güncelleştirme kategorilerini destekleyen v3 üçüncü taraf güncelleştirme katalogları için kullanılabilir. Bu seçenekler, Yeni v3 biçiminde yayımlanmamış kataloglar için devre dışı bırakılmıştır.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Yazılım güncelleştirmeleri** ' ni genişletin ve **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü seçin.
1. Kataloğa sağ tıklayıp **Özellikler**' i seçin.
1. **Kategorileri Seç** sekmesinde seçeneklerinizi belirleyin.
   - **Tüm güncelleştirme kategorilerini eşitler** (varsayılan)
       - Üçüncü taraf güncelleştirme kataloğundaki tüm güncelleştirmeleri Configuration Manager olarak eşitler.
   -  **Eşitleme için kategorileri seçin**
       - Configuration Manager hangi kategorilerin ve alt kategorilerin eşitleneceğini seçin.
1. **Aşama güncelleştirme içeriği** sekmesi için seçeneklerinizi belirleyin.
   - **İçerik aşamalamayın, yalnızca tarama için eşitlenir (önerilir)**
     - Üçüncü taraf katalogdaki güncelleştirmeler için herhangi bir içerik indirmeyin
   - **Seçili kategorilerin içeriğini otomatik olarak hazırlama**
     - İçeriği otomatik olarak indirecek güncelleştirme kategorilerini seçin.
     - Seçili kategorilerdeki güncelleştirmelerin içeriği en üst düzey yazılım güncelleştirme noktasının WSUS içerik dizinine indirilir. 

## <a name="monitoring-progress-of-third-party-software-updates"></a>Üçüncü taraf yazılım güncelleştirmelerinin ilerlemesini izleme 

Üçüncü taraf yazılım güncelleştirmelerinin eşitlenmesi, en üst düzey varsayılan yazılım güncelleştirme noktasındaki SMS_ISVUPDATES_SYNCAGENT bileşeni tarafından işlenir. Bu bileşenden durum iletilerini görüntüleyebilir veya SMS_ISVUPDATES_SYNCAGENT. log dosyasında daha ayrıntılı durumu görebilirsiniz. Bu günlük, site sistem günlükleri klasöründeki en üst düzey yazılım güncelleştirme noktasıdır. Varsayılan olarak, bu yol C:\Program Files\Microsoft Configuration Manager\Logs. konumundadır. Genel yazılım güncelleştirme yönetimi sürecini izleme hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmelerini izleme](../deploy-use/monitor-software-updates.md) 

## <a name="known-issues"></a>Bilinen sorunlar

- Konsolun çalıştığı makine, güncelleştirmeleri WSUS 'den indirmek ve güncelleştirmeler paketine eklemek için kullanılır. WSUS imzalama sertifikası konsol makinesinde güvenilir olmalıdır. Aksi takdirde, üçüncü taraf güncelleştirmelerin indirilmesi sırasında imza denetiminde sorunlar yaşayabilirsiniz. 
- Üçüncü taraf yazılım güncelleştirme eşitleme hizmeti, yalnızca farklı bir uygulama, araç veya bir komut dosyası tarafından WSUS 'a eklenen güncelleştirmeler (örneğin, SCUP) için içerik yayımlayamaz. **Üçüncü taraf yazılım güncelleştirme Içeriğini Yayımla** eylemi Bu güncelleştirmelerde başarısız olur. Bu özelliğin henüz desteklemediği üçüncü taraf güncelleştirmeleri dağıtmanız gerekiyorsa, bu güncelleştirmeleri dağıtmak için mevcut işleminizi tam olarak kullanın.  
-  Configuration Manager, Katalog cab dosyası biçimi için yeni bir sürüme sahiptir. Yeni sürüm, satıcının ikili dosyalarının sertifikalarını içerir. Bu sertifikalar, kataloğa onayladıktan ve güvendikten sonra **Yönetim** çalışma alanındaki **güvenlik** altındaki **Sertifikalar** düğümüne eklenir.  
     - İndirme URL 'SI https olduğu ve güncelleştirmeler imzalandığı sürece eski Katalog cab dosyası sürümünü kullanmaya devam edebilirsiniz. İkili dosyalar için sertifikalar cab dosyasında olmadığından ve zaten onaylanmış olduğundan içerik yayımlanamaz. **Sertifika düğümündeki sertifikayı** bularak, onun engellemesini kaldırarak ve güncelleştirmeyi yeniden yayımlayarak bu soruna geçici bir çözüm bulabilirsiniz. Farklı sertifikalarla imzalanmış birden çok güncelleştirme yayımlıyorsanız, kullanılan her bir sertifikanın engellemesini kaldırmanız gerekir.
     - Daha fazla bilgi için aşağıdaki durum iletisi tablosunda 11523 ve 11524 durum iletileri bölümüne bakın.
-  Üst düzey yazılım güncelleştirme noktasındaki üçüncü taraf yazılım güncelleştirme eşitleme hizmeti internet erişimi için bir proxy sunucu gerektirdiğinde, dijital imza denetimleri başarısız olabilir. Bu sorunu azaltmak için, site sisteminde WinHTTP proxy ayarlarını yapılandırın. Daha fazla bilgi için bkz. [WinHTTP Için Netsh komutları](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731131(v=ws.10)).
- İçerik depolaması için bir CMG kullanırken, kullanılabilir [istemci ayarı](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) etkinleştirildiğinde **Delta içeriğini indir** , üçüncü taraf güncelleştirmeler için içerik istemcilere indirmez. <!--6598587-->

## <a name="status-messages"></a>Durum iletileri

| Ileti       | Severity           | Açıklama | Olası nedeni| Olası çözüm
| ------------- |-------------| -----|----|----|
| 11516     | Hata |İçerik imzasız olduğundan "güncelleştirme KIMLIĞI" güncelleştirmesi için içerik yayımlanamadı.  Yalnızca geçerli imzalara sahip içerikler yayımlanabilir.  |Configuration Manager, imzasız güncelleştirmelerin yayımlanmasına izin vermez.| Güncelleştirmeyi alternatif bir şekilde yayımlayın. </br></br>Satıcıdan imzalı bir güncelleştirme olup olmadığını görün.|
| 11523  | Uyarı |  "X" kataloğunda içerik imzalama sertifikaları yoktur, içerik imzalama sertifikaları eklenip onaylanana kadar bu katalogdan güncelleştirme içeriğini yayımlama girişimleri başarısız olabilir. | Bu ileti, cab dosya biçiminin eski bir sürümünü kullanan bir kataloğu içeri aktardığınızda oluşabilir.|İçerik imzalama sertifikalarını içeren güncelleştirilmiş bir katalog almak için Katalog sağlayıcısına başvurun. </br> </br> İkili dosyalar için sertifikalar cab dosyasına dahil edilmez, bu nedenle içerik yayımlayamayacak. **Sertifika düğümündeki sertifikayı** bularak, onun engellemesini kaldırarak ve güncelleştirmeyi yeniden yayımlayarak bu soruna geçici bir çözüm bulabilirsiniz. Farklı sertifikalarla imzalanmış birden çok güncelleştirme yayımlıyorsanız, kullanılan her bir sertifikanın engellemesini kaldırmanız gerekir.|
| 11524| Hata  | Eksik güncelleştirme meta verileri nedeniyle "ID" güncelleştirmesi yayımlanamadı. | Güncelleştirme, Configuration Manager dışında WSUS ile eşitlenmiş olabilir.| Güncelleştirmeyi, içeriğini yayımlamayı denemeden önce Configuration Manager ile eşitler.  </br> </br>Güncelleştirmeyi **yalnızca meta veriler**olarak yayımlamak için bir dış araç kullanılmışsa, güncelleştirme içeriğini yayımlamak için aynı aracı kullanın.|



## <a name="working-with-third-party-updates-video"></a>Üçüncü taraf güncelleştirmelerle çalışma videosu
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Sonraki adım
> [!div class="nextstepaction"]
> [Yazılım güncelleştirmelerini dağıtma](./deploy-software-updates.md)
