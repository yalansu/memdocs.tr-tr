---
title: Uzak bağlantı profilleri oluşturma
titleSuffix: Configuration Manager
description: Kullanıcılarınızın iş bilgisayarlarına uzaktan bağlanmasını sağlamak için Configuration Manager uzak bağlantı profillerini kullanın.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c9a06e1b7c14cda02a8029925785c2109ea4204b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712354"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Configuration Manager uzak bağlantı profilleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Kullanıcılarınızın iş bilgisayarlarına uzaktan bağlanmasına izin vermek için Configuration Manager uzak bağlantı profillerini kullanın. Bu profiller, hiyerarşinizdeki kullanıcılara Uzak Masaüstü Bağlantısı ayarları dağıtmanızı sağlar. Kullanıcılar, bir VPN bağlantısı üzerinden Uzak Masaüstü aracılığıyla birincil iş bilgisayarlarından herhangi birine erişebilir.  

> [!IMPORTANT]  
> Configuration Manager ile uzak bağlantı profili ayarlarını belirttiğinizde, istemci ayarları Windows yerel ilkesinde depolar. Bu ayarlar, başka bir uygulamayla yapılandırdığınız uzak masaüstü ayarlarını geçersiz kılabilir. Ayrıca, uzak masaüstü ayarlarını yapılandırmak için Windows grup ilkesi kullanıyorsanız, grup ilkesi belirtilen ayarlar Configuration Manager ayarları geçersiz kılar.

Configuration Manager, **uzak bilgisayar bağlantısı**olan istemcilerde bir güvenlik grubu oluşturur. Bir uzak bağlantı profili dağıttığınızda istemci, bilgisayarın birincil kullanıcılarını bu gruba ekler. Yerel bir yönetici, kullanıcıları bu gruba el ile ekleyebilir veya kaldırabilir, ancak bir sonraki profilin uyumluluğunu değerlendirirken üyeliği güncelleştirir Configuration Manager.

> [!IMPORTANT]  
> Bir Kullanıcı ve bir cihaz arasındaki Kullanıcı cihaz benzeşimi ilişkisi değişirse Configuration Manager, uzak bağlantı profilini ve Windows Güvenlik Duvarı ayarlarını, bilgisayara bağlantıları engelleyecek şekilde devre dışı bırakır.

## <a name="prerequisites"></a>Önkoşullar  

### <a name="external-dependencies"></a>Dış bağımlılıklar  

- Kullanıcıların Internet 'ten bağlanmasını etkinleştirmek istiyorsanız, bir Uzak Masaüstü Ağ Geçidi sunucusu yükleyip yapılandırın. Uzak Masaüstü Ağ Geçidi sunucusunun nasıl yükleneceği ve yapılandırılacağı hakkında daha fazla bilgi için, [her yerden uzak Masaüstü Hizmetleri erişim](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere)bölümüne bakın.

- İstemciler ana bilgisayar tabanlı güvenlik duvarı çalıştırıyorsa, mstsc. exe programının etkinleştirilmesi gerekir. Uzak bağlantı profilini yapılandırırken **Windows etki alanlarındaki ve özel ağlardaki bağlantılarda Windows Güvenlik Duvarı özel durumuna Izin ver**ayarını etkinleştirin. Bu ayar Configuration Manager Windows güvenlik duvarını otomatik olarak yapılandırmak için izin verir.

    > [!TIP]
    > Windows Güvenlik Duvarını yapılandıran Grup İlkesi ayarları Configuration Manager’da ayarladığınız yapılandırmayı geçersiz kılabilir. Windows Güvenlik Duvarı 'Nı yapılandırmak için grup ilkesi kullanıyorsanız, grup ilkesi ayarlarının mstsc. exe ' yi engellemediğinden emin olun.

    İstemciler ana bilgisayar tabanlı farklı bir güvenlik duvarını çalıştıralıyorsa, bu güvenlik duvarı bağımlılığını el ile yapılandırın.  

### <a name="configuration-manager-dependencies"></a>Configuration Manager bağımlılıkları  

- Bir kullanıcının iş bilgisayarına bağlanabilmesi için o bilgisayarın, kullanıcının birincil cihazı olması gerekir. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi Ile bağlama](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

- Uzak bağlantı profillerini yönetmek için, Kullanıcı hesabınızın Configuration Manager özel izinleri olması gerekir. **Uyumluluk Ayarları Yöneticisi** yerleşik rolü, bu profilleri yönetmek için gereken izinleri içerir. Daha fazla bilgi için bkz. [rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="security-and-privacy-considerations"></a>Güvenlik ve gizlilik konuları

### <a name="security-considerations"></a>Güvenlik konuları  

- Kullanıcıların birincil cihazlarını tanımlamalarına izin vermek yerine kullanıcı aygıtı benzeşimini elle belirtin. Kullanım tabanlı yapılandırmayı etkinleştirmeyin.

  - Uzak bağlantı profilini dağıtabilmeniz için önce **iş bilgisayarının tüm birincil kullanıcılarının uzaktan bağlanmasına Izin ver**seçeneğini etkinleştirmeniz gerekir. Bu yapılandırmayla, Kullanıcı cihaz benzeşimini her zaman el ile belirtmeniz gerekir. Configuration Manager toplanan bilgileri kullanıcılardan veya cihazdan yetkili olacak şekilde değerlendirin. Bir profil dağıtırsanız ve güvenilen bir yönetici kullanıcı, Kullanıcı aygıtı benzeşimini belirtmiyorsa yetkisiz kullanıcılar yükseltilmiş ayrıcalıklar alabilir ve bilgisayarlara uzaktan bağlanabilirler.

  - Configuration Manager, hızlı ancak güvensiz bir iletişim kanalı olan durum iletileri aracılığıyla kullanım tabanlı bilgileri toplar. Bu tehdidi azaltmaya yardımcı olmak için istemci bilgisayarlar ile yönetim noktası arasında Sunucu İleti Bloğu (SMB) imzası veya İnternet Protokolü güvenliği (IPsec) kullanın.

- Site sunucusu bilgisayarda yerel yönetici haklarını kısıtlayın. Site sunucusundaki yerel bir yönetici, otomatik olarak Configuration Manager ve bakımını yaptığı **uzak bilgisayar Connect** güvenlik grubuna üye ekleyebilir. Üyeler Uzak Masaüstü izinleri aldığından, bu eylem ayrıcalık yükselmesine neden olabilir.

### <a name="privacy-considerations"></a>Gizlilik konuları  

Bir Kullanıcı bir iş bilgisayarına uzaktan bağlanıyorsa, bir. wsrdp dosyası indirir. Bu dosya, cihaz adını ve Uzak Masaüstü Ağ Geçidi sunucu adını içerir. Bu değerler, uzak masaüstü oturumunun oluşturulması için gereklidir. .wsrdp dosyası indirilir ve kendiliğinden yerel olarak kaydedilir. Kullanıcının Uzak Masaüstü oturumunu bir sonraki çalıştırmasında bu dosyanın üzerine yazılır.  

## <a name="create-a-profile"></a>Profil oluşturma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin ve **uzak bağlantı profilleri**' ni seçin.  

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **uzak bağlantı profili oluştur**' u seçin.  

1. **Uzaktan bağlantı profili oluşturma Sihirbazı**' nın **genel** sayfasında, profil için bir ad ve isteğe bağlı bir açıklama belirtin. Her iki değerin de en fazla 256 karakter sınırı vardır.  

1. **Profil ayarları** sayfasında, aşağıdaki ayarları belirtin:  

    - **Uzak Masaüstü Ağ Geçidi sunucusunun tam adı ve bağlantı noktası (isteğe bağlı)**: bağlantılarda kullanılacak uzak Masaüstü Ağ Geçidi sunucusunun adını belirtin. Bu değer aşağıdaki gereksinimlere sahiptir:

        - Sunucu adı 256 karakterden uzun olamaz.
        - Büyük harf, küçük harf ve sayısal karakterler içerebilir.
        - Bölümler arasında nokta (`.`) ve bağlantı noktasından önce iki nokta (`:`) dışında, tek özel karakterler Dash (`–`) ve alt çizgi (`_`).
        - Configuration Manager, bu değer için uluslararası bir etki alanı adının kullanımını desteklemez.

    - **Yalnızca ağ düzeyinde kimlik doğrulama Ile uzak masaüstü çalıştıran bilgisayarlardan bağlantıya Izin ver**: varsayılan olarak etkin, bu ayar bağlantı için ek bir güvenlik düzeyi ekler. Daha fazla bilgi için bkz. [Uzak Masaüstü erişimi verme](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication).

    - Aşağıdaki bağlantı ayarlarını etkinleştirin:

        - **İş bilgisayarlarına uzaktan bağlantıya izin ver**

        - **İş bilgisayarının tüm birincil kullanıcılarının uzaktan bağlanmasına izin ver**

        - **Windows etki alanlarındaki ve özel ağlardaki bağlantılarda Windows Güvenlik Duvarı özel durumuna izin ver**

        > [!IMPORTANT]  
        > Devam edebilmeniz için tüm üç ayar aynı olmalıdır.

        Yalnızca uzak bağlantıları kapatmak için bir profil dağıtırken bu ayarları devre dışı bırakın.

1. Sihirbazı tamamlayın.

Yeni profil, **varlıklar ve uyum** çalışma alanındaki **uzak bağlantı profilleri** düğümünde görüntülenir.  

## <a name="deploy"></a>Dağıtma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin, **Uyumluluk ayarları**' nı genişletin ve **uzak bağlantı profilleri**' ni seçin.

1. **Uzaktan bağlantı profilleri** listesinde, dağıtmak istediğiniz profili seçin. Şeridin **giriş** sekmesinde, **dağıtım** grubunda, **Dağıt**' ı seçin.  

1. **Uzak bağlantı profili dağıt** penceresinde, aşağıdaki bilgileri belirtin:

    - **Koleksiyon**: profili dağıtmak istediğiniz cihaz koleksiyonunu seçmek için gidin.

    - **Desteklendiğinde uyumsuz kuralları düzelt**: bir cihazda uyumsuz olduklarında profil ayarlarını otomatik olarak düzeltmek için bu ayarı etkinleştirin. Profil, mevcut olmadığında uyumsuz olabilir.

    - **Bakım süresi dışında düzeltmeye Izin ver**: profili dağıttığınız koleksiyon için bir bakım penceresi yapılandırırsanız, bakım penceresi dışında düzeltmek Configuration Manager izin vermek için bu seçeneği etkinleştirin. Daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).

    - **Uyarı oluştur**: bir uyumluluk uyarısını yapılandırmak için bu seçeneği etkinleştirin.

    - **Bu yapılandırma temeline ait uyumluluk değerlendirme zamanlamasını belirtin**: istemcinin profili değerlendiren basit veya özel bir zamanlama belirtin.

1. Pencereyi kapatmak ve dağıtımı oluşturmak için **Tamam ' ı** seçin.

### <a name="client-evaluation"></a>İstemci değerlendirmesi

Kullanıcı oturum açtığında, istemci profili değerlendirir.

Bir cihaz, uzak bağlantı profilini dağıttığınız bir koleksiyonu bırakırsa Configuration Manager cihazdaki ayarları devre dışı bırakır. Ancak, bu işlemin düzgün bir şekilde gerçekleşmesi için en az bir yapılandırma öğesi veya sitenizdeki bir yapılandırma öğesini içeren bir yapılandırma temel çizgisi dağıtmış olmanız gerekir.

### <a name="conflict-resolution"></a>Çakışma çözümleme

Aynı cihaza çakışan ayarlarla birden fazla uzak bağlantı profili dağıtmayın. Örneğin, aynı koleksiyona farklı ayarlarla iki profil dağıtırsınız. **Desteklendiğinde uyumsuz kuralları**düzeltmek için yalnızca bir profil dağıtımı yapılandırırsınız. Bu dağıtım, diğer profildeki ayarları geçersiz kılabilir. Configuration Manager, bu tür uzak bağlantı profili dağıtımını desteklemez.

## <a name="monitor"></a>İzleme

Configuration Manager konsolunda, **izleme** çalışma alanına gidin ve **dağıtımlar**' ı seçin. **Dağıtımlar** listesinde, uzaktan bağlantı profili dağıtımını seçin.

Uzaktan bağlantı profili dağıtımının uyumluluğu hakkında özet bilgileri anasayfada gözden geçirebilirsiniz. Daha ayrıntılı bilgi görüntülemek için profil dağıtımını seçin. Ardından, şeridin **giriş** sekmesinde, **dağıtım** grubunda, **durumu görüntüle**' yi seçin. Bu eylem, **dağıtım durumu** sayfasını açar.  

**Dağıtım Durumu** sayfası aşağıdaki sekmeleri içerir:  

- **Uyumlu**: uzak bağlantı profilinin uyumluluğunu, etkilenen varlıkların sayısına bağlı olarak görüntüler.

    > [!IMPORTANT]  
    > İstemci, geçerli değilse uzak bağlantı profilini değerlendirmez. Ancak yine de uyumlu raporlar.

- **Hata**: seçilen uzak bağlantı profili dağıtımı için tüm hataların bir listesini, etkilenen varlıkların sayısına bağlı olarak görüntüler.

- **Uyumlu değil**: uzak bağlantı profilindeki tüm uyumsuz kuralların listesini etkilenen varlıkların sayısına göre görüntüler.

- **Bilinmiyor**: seçilen uzak bağlantı profili dağıtımı için uyumluluk bildirmeyen tüm cihazların listesini, cihazların geçerli istemci durumuyla birlikte görüntüler.

Herhangi bir sekmede, **varlıklar ve uyum** çalışma alanındaki **Kullanıcılar** düğümü altında geçici bir alt düğüm oluşturmak için bir kural açın. Bu alt düğüm seçili sekmenin uyumluluk durumuna sahip tüm cihazları içerir.

**Varlık ayrıntıları** bölmesi, bu profil için seçili uyumluluk durumuna sahip olan cihazları görüntüler. Ek bilgileri göstermek için listeden bir cihaz açın.

## <a name="reports"></a>Raporlar

Configuration Manager, uzak bağlantı profilleri hakkındaki bilgileri izlemek için kullanabileceğiniz yerleşik raporlar içerir. Bu raporlar **Uyumluluk ve Ayarlar Yönetimi**rapor kategorisindedir.  

> [!IMPORTANT]  
> Uyumluluk ayarları raporlarında`%` **Cihaz filtresi** ve **Kullanıcı filtresi** parametrelerini kullanırken joker karakteri () kullanın.  

Configuration Manager raporlamayı yapılandırma hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).  
