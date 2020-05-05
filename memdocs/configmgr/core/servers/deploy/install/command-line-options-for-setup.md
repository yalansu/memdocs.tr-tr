---
title: Kurulum komut satırı seçenekleri
titleSuffix: Configuration Manager
description: Bir komut satırından Configuration Manager yüklemek için Otomasyon betikleri oluşturun.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718255"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Configuration Manager Kurulum için komut satırı seçenekleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Betikleri yapılandırmak veya komut satırından Configuration Manager yüklemek için aşağıdaki bilgileri kullanın.  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a>Kurulum için komut satırı seçenekleri

Kurulum 'u site sunucusunda `\BIN\X64` Configuration Manager yükleme yolunun dizininden çalıştırın.

### `/DEINSTALL`

Siteyi kaldırın. Site sunucusu bilgisayarından kurulum 'u çalıştırın.  

### `/DONTSTARTSITECOMP`

Bir site yükler, ancak Site Bileşen Yöneticisi hizmetinin başlamasını engeller. Site Bileşen Yöneticisi hizmeti başlatılana kadar site etkin değil. Site Bileşen Yöneticisi, SMS_Executive hizmetini yükleyip başlatmadan ve sitedeki ek işlemlerin sorumluluğundadır. Site yüklemesi tamamlandıktan sonra, Site Bileşen Yöneticisi hizmetini başlattığınızda, sitenin çalışması için gerekli olan SMS_Executive hizmetini ve ek süreçlerini yükler.  

### `/HIDDEN`

Kurulum sırasında Kullanıcı arabirimini gizleyin. Bu seçeneği yalnızca **/SCRIPT** seçeneğiyle birlikte kullanın. Katılımsız betik dosyasında gerekli tüm seçenekler sağlanmalıdır veya kurulum başarısız olur.  

### `/NOUSERINPUT`

Kurulum sırasında Kullanıcı girişini devre dışı bırakın, ancak Kurulum Sihirbazı 'nı görüntüler. Bu seçeneği yalnızca **/SCRIPT** seçeneğiyle birlikte kullanın. Katılımsız betik dosyasında gerekli tüm seçenekler sağlanmalıdır veya kurulum başarısız olur.  

### `/RESETSITE`

Site için veritabanını ve hizmet hesaplarını sıfırlayan bir site sıfırlaması çalıştırın.

Daha fazla bilgi için bkz. [site sıfırlaması çalıştırma](../../manage/modify-your-infrastructure.md#bkmk_reset).  

### `/TESTDBUPGRADE`

Veritabanının yükseltileceğiyle emin olmak için site veritabanının bir yedeklemesi üzerinde bir test çalıştırın.

> [!IMPORTANT]  
> Bu komut satırı seçeneğini üretim sitesi veritabanınızda çalıştırmayın. Bu komut satırı seçeneğini üretim sitesi veritabanınızda çalıştırmak, site veritabanını yükseltir ve sitenizi çalışamaz duruma getirebilir.

#### <a name="usage"></a>Kullanım

Site veritabanı için örnek adını ve veritabanı adını sağlayın. Yalnızca veritabanı adını belirtirseniz, kurulum varsayılan örnek adını kullanır.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Bir sitenin katılımsız yükseltmesini çalıştırın. Tireler (`-`) dahil olmak üzere ürün anahtarını belirtin. Ayrıca, daha önce indirilen kurulum önkoşul dosyalarının yolunu belirtin.  

Kurulum önkoşul dosyaları hakkında daha fazla bilgi için bkz. [Kurulum Yükleyici](setup-downloader.md).  

#### <a name="usage"></a>Kullanım

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Katılımsız yükleme çalıştırın. Bu seçenekle bir Kurulum başlatma dosyası kullanın. Kurulumu katılımsız çalıştırma hakkında daha fazla bilgi için bkz. [komut satırını kullanarak siteleri yükleme](use-a-command-line-to-install-sites.md).  

#### <a name="usage"></a>Kullanım

`/SCRIPT <setup script path>`

### `/SDKINST`

Belirtilen bilgisayara SMS sağlayıcısı 'nı yükler. SMS sağlayıcı bilgisayarı için tam etki alanı adını (FQDN) belirtin. SMS sağlayıcısı hakkında daha fazla bilgi için bkz. [plan for SMS Provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="usage"></a>Kullanım

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Belirtilen bilgisayarda SMS sağlayıcısı 'nı kaldırın. SMS sağlayıcı bilgisayarı için FQDN 'yi belirtin.  

#### <a name="usage"></a>Kullanım

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

Daha önce yüklenmiş bir sitede yüklü olan dilleri yönetin. Dil ayarlarını içeren dil betiği dosyasının konumunu belirtin. Daha fazla bilgi için bkz. [dilleri yönetmek Için komut satırı seçenekleri](#bkmk_Lang) bölümü.  

#### <a name="usage"></a>Kullanım

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a>Dilleri yönetmek için komut satırı seçenekleri

### <a name="identification"></a>Kimlik

- **Anahtar Adı:** Eylem  

    - **Gerekli:** Evet  

    - **Değerler:** `ManageLanguages`  

    - **Ayrıntılar:** Bir sitede sunucu, istemci ve mobil istemci dil desteğini yönetir.  

### <a name="options"></a>Seçenekler

- **Anahtar adı:** AddServerLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Configuration Manager konsolu, raporlar ve Configuration Manager nesneleri için kullanılabilecek sunucu dillerini belirtir. İngilizce varsayılan olarak kullanılabilir.  

- **Anahtar adı:** AddClientLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** İstemci bilgisayarlar için kullanılabilecek dilleri belirtir. İngilizce varsayılan olarak kullanılabilir.  

- **Anahtar adı:** DeleteServerLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Kaldırılacak dilleri belirtir ve Configuration Manager konsolu, raporlar ve Configuration Manager nesneleri için artık kullanılabilir olmayacaktır. İngilizce varsayılan olarak kullanılabilir, kaldırılamaz.  

- **Anahtar adı:** DeleteClientLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Kaldırılacak dilleri belirtir ve artık istemci bilgisayarlar için kullanılabilir olmayacaktır. İngilizce varsayılan olarak kullanılabilir, kaldırılamaz.  

- **Anahtar adı:** MobileDeviceLanguage  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Mobil aygıt istemci dillerinin yüklenip yüklenmediğini belirtir.  

- **Anahtar Adı:** PrerequisiteComp  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= İndir  

        - `1`= Zaten indirildi  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının daha önce indirilip indirilmediğini belirtir. Örneğin, bir değeri kullanırsanız `0`, kurulum dosyaları indirir.  

- **Anahtar Adı:** PrerequisitePath  

    - **Gerekli:** Evet  

    - **Değerler:** <*Önkoşul dosyalarının kurulum yolu*>  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının yolunu belirtir. **ÖnkoşullarBu** değerine bağlı olarak, kurulum bu yolu indirilen dosyaları depolamak veya daha önce indirilen dosyaları bulmak için kullanır.  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a>Katılımsız kurulum komut dosyası anahtarları

Katılımsız kurulum için komut dosyanızı oluşturmanıza yardımcı olması için aşağıdaki bölümleri kullanın. Listeler şunları gösterir:

- Kullanılabilir kurulum komut dosyası anahtarları ve bunlara karşılık gelen değerler
- Gerekirse
- Hangi tür yükleme için kullanıldıkları
- Anahtarın kısa bir açıklaması

### <a name="unattended-install-for-a-central-administration-site-cas"></a>Merkezi Yönetim sitesi (CA 'LAR) için katılımsız kurulum

Katılımsız bir Kurulum betik dosyası kullanarak bir CA yüklemek için aşağıdaki ayrıntıları kullanın.  

#### <a name="identification"></a>Kimlik

- **Anahtar Adı:** Eylem  

    - **Gerekli:** Evet  

    - **Değerler:** `InstallCAS`  

    - **Ayrıntılar:** Bir CA kurar.  

- **Anahtar adı:** CDLatest  

    - **Gerekli:** Evet, yalnızca CD 'den medya kullanılırken. En son klasör.

    - **Değerler:**

        - `1`= CD 'den medya kullanıyorsunuz. Sürümü

        - 1 dışında bir değer = CD 'yi kullanmıyoruz. En son medya

    - **Ayrıntılar:** Birincil bir siteyi veya CA 'yı yüklediğinizde veya kurtardığınızda ve kurulum 'u CD 'den çalıştırırsanız. En son klasör, bu anahtarı ve değeri içerir. Bu değer, kurulum 'u CD 'den medya kullandığınızı bildirir. Sürümü.

#### <a name="options"></a>Seçenekler

- **Anahtar Adı:** ProductID  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= tireleri olan geçerli bir ürün anahtarı

        - `Eval`= Configuration Manager değerlendirme sürümünü yükler

    - **Ayrıntılar:** Tireler dahil Configuration Manager yüklemesi ürün anahtarını belirtir.

- **Anahtar Adı:** SiteCode  

    - **Gerekli:** Evet  

    - **Değerler:** <*site kodu*>, örneğin,`ABC`

    - **Ayrıntılar:** Hiyerarşinizde siteyi benzersiz şekilde tanımlayan üç alfasayısal karakter belirtir.  

- **Anahtar adı:** Site adı  

    - **Gerekli:** Evet  

    - **Değerler:** <*site adı*>  

    - **Ayrıntılar:** Bu site için adı belirtir.  

- **Anahtar Adı:** SMSInstallDir  

    - **Gerekli:** Evet  

    - **Değerler:** <*Configuration Manager yükleme yolu*>  

    - **Ayrıntılar:** Configuration Manager program dosyaları için yükleme klasörünü belirtir.  

- **Anahtar Adı:** SDKServer  

    - **Gerekli:** Evet  

    - **Değerler:** <*SMS sağlayıcısı FQDN 'si*>  

    - **Ayrıntılar:** SMS Sağlayıcısı’nı barındıracak sunucunun FQDN'sini belirtir. İlk yüklemeden sonra site için ek SMS Sağlayıcılarını yapılandırabilirsiniz.  

- **Anahtar Adı:** PrerequisiteComp  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= İndir  

        - `1`= Zaten indirildi  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının daha önce indirilip indirilmediğini belirtir. Örneğin, bir değeri kullanırsanız `0`, kurulum dosyaları indirir.  

- **Anahtar Adı:** PrerequisitePath  

    - **Gerekli:** Evet  

    - **Değerler:** <*Önkoşul dosyalarının kurulum yolu*>  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının yolunu belirtir. **ÖnkoşullarBu** değerine bağlı olarak, kurulum bu yolu indirilen dosyaları depolamak veya daha önce indirilen dosyaları bulmak için kullanır.  

- **Anahtar adı:** AdminConsole  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Configuration Manager konsolunun yüklenip yüklenmeyeceğini belirtir.  

- **Anahtar Adı:** JoinCEIP  

    > [!Note]  
    > Configuration Manager sürüm 1802 ' den başlayarak CEIP özelliği üründen kaldırılır.

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Katılımayın  

        - `1`= Birleştir  

    - **Ayrıntılar:** Müşteri Deneyimini Geliştirme Programı (CEIP) öğesine katılıp katılmayacağını belirtir.  

- **Anahtar adı:** AddServerLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Configuration Manager konsolu, raporlar ve Configuration Manager nesneleri için kullanılabilecek sunucu dillerini belirtir. İngilizce varsayılan olarak kullanılabilir.  

- **Anahtar adı:** AddClientLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** İstemci bilgisayarlar için kullanılabilecek dilleri belirtir. İngilizce varsayılan olarak kullanılabilir.  

- **Anahtar adı:** DeleteServerLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Bir siteyi yükledikten sonra değiştirir. Kaldırılacak dilleri belirtir ve Configuration Manager konsolu, raporlar ve Configuration Manager nesneleri için artık kullanılabilir olmayacaktır. İngilizce varsayılan olarak kullanılabilir, kaldırılamaz.  

- **Anahtar adı:** DeleteClientLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Bir siteyi yükledikten sonra değiştirir. Kaldırılacak dilleri belirtir ve artık istemci bilgisayarlar için kullanılabilir olmayacaktır. İngilizce varsayılan olarak kullanılabilir, kaldırılamaz.  

- **Anahtar adı:** MobileDeviceLanguage  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Mobil aygıt istemci dillerinin yüklenip yüklenmediğini belirtir.  

#### <a name="sqlconfigoptions"></a>SQLYapılandırmaSeçenekleri

- **Anahtar adı:** SQLServerName  

    - **Gerekli:** Evet  

    - **Değerler:** <*SQL Server adı*>  

    - **Ayrıntılar:** Site veritabanını barındırmak için SQL Server çalıştıran sunucunun veya kümelenmiş örneğin adını belirtir.  

- **Anahtar adı:** DatabaseName  

    - **Gerekli:** Evet  

    - **Değerler:** <*site veritabanı adı*> veya <*örneği adı*>\\<*site veritabanı adı*>  

    - **Ayrıntılar:** Kurulum, CAS veritabanını yüklediğinde oluşturulacak SQL Server veritabanının veya kullanılacak SQL Server veritabanının adını belirtir.  

        > [!IMPORTANT]  
        > Varsayılan örneği kullanmıyorsanız, örnek adını ve site veritabanı adını belirtin.  

- **Anahtar adı:** SQLSSBPort  

    - **Gerekli:** Hayır  

    - **Değerler:** <*SSB bağlantı noktası numarası*>  

    - **Ayrıntılar:** SQL Server tarafından kullanılan SQL Server Hizmet Aracısı (SSB) bağlantı noktasını belirtir. SSB, varsayılan olarak 4022 numaralı TCP bağlantı noktasını kullanır, ancak farklı bir bağlantı noktası kullanabilirsiniz.  

- **Anahtar adı:** SQLDataFilePath  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Database. mdb dosyasının yolu*>  

    - **Ayrıntılar:** Database. mdb dosyasını oluşturmak için başka bir konum belirtir.  

- **Anahtar adı:** SQLLogFilePath  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Database. ldf dosyasının yolu*>  

    - **Ayrıntılar:** Database. ldf dosyasını oluşturmak için başka bir konum belirtir.  

#### <a name="cloudconnectoroptions"></a>Cloudconnectoroçen

- **Anahtar adı:** CloudConnector  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Bu sitede bir hizmet bağlantı noktası yüklenip yüklenmeyeceğini belirtir. Hizmet bağlantı noktasını yalnızca bir hiyerarşinin üst katman sitesine yükleyebildiğinden, bir alt birincil site için bu değeri olarak `1` ayarlayın.  

- **Anahtar adı:** CloudConnectorServer  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*hizmet bağlantı noktası sunucu FQDN 'si*>  

    - **Ayrıntılar:** Hizmet bağlantı noktası site sistemi rolünü barındıracak sunucunun FQDN 'sini belirtir.  

- **Anahtar adı:** UseProxy  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Hizmet bağlantı noktasının bir ara sunucu kullanıp kullanmadığını belirtir.  

- **Anahtar adı:** ProxyName  

    - **Gerekli:** **UseProxy** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*proxy sunucusu FQDN 'si*>  

    - **Ayrıntılar:** Hizmet bağlantı noktasının kullandığı proxy sunucusunun FQDN 'sini belirtir.  

- **Anahtar adı:** ProxyPort  

    - **Gerekli:** **UseProxy** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*bağlantı noktası numarası*>  

    - **Ayrıntılar:** Proxy bağlantı noktası için kullanılacak bağlantı noktası numarasını belirtir.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Anahtar adı:** Saactıve

    - **Gerekli:** Hayır

    - **Değerler:**

        - `0`= Yazılım güvencesi yok

        - `1`= Yazılım Güvencesi etkin

    - **Ayrıntılar:** Etkin yazılım güvencesi olup olmadığını belirtin. Daha fazla bilgi için bkz. [ürün ve lisanslama hakkında SSS](../../../understand/product-and-licensing-faq.md).

- **Anahtar adı:** CurrentBranch

    - **Gerekli:** Hayır

    - **Değerler:**

        - `0`= LTSB 'yi yükler

        - `1`= Geçerli dalı yükler

    - **Ayrıntılar:** Configuration Manager geçerli dal veya uzun süreli bakım dalı (LTSB) kullanıp kullanmayacağınızı belirtin. Daha fazla bilgi için, [hangi Configuration Manager dalını kullanmalıyım?](../../../understand/which-branch-should-i-use.md)bölümüne bakın.

### <a name="unattended-install-for-a-primary-site"></a>Birincil site için katılımsız kurulum

Katılımsız bir Kurulum betik dosyası kullanarak bir birincil site yüklemek için aşağıdaki ayrıntıları kullanın.  

#### <a name="identification"></a>Kimlik

- **Anahtar Adı:** Eylem  

    - **Gerekli:** Evet  

    - **Değerler:** `InstallPrimarySite`  

    - **Ayrıntılar:** Birincil siteyi kurar.  

- **Anahtar adı:** CDLatest  

    - **Gerekli:** Evet, yalnızca CD 'den medya kullanılırken. En son klasör.

    - **Değerler:**

        - `1`= CD 'den medya kullanıyorsunuz. Sürümü

        - 1 dışında bir değer = CD 'yi kullanmıyoruz. En son medya

    - **Ayrıntılar:** Birincil bir siteyi veya CA 'yı yüklediğinizde veya kurtardığınızda ve kurulum 'u CD 'den çalıştırırsanız. En son klasör, bu anahtarı ve değeri içerir. Bu değer, kurulum 'u CD 'den medya kullandığınızı bildirir. Sürümü.

#### <a name="options"></a>Seçenekler

- **Anahtar Adı:** ProductID  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= tireleri olan geçerli bir ürün anahtarı

        - `Eval`= Configuration Manager değerlendirme sürümünü yükler

    - **Ayrıntılar:** Tireler dahil Configuration Manager yüklemesi ürün anahtarını belirtir.

- **Anahtar Adı:** SiteCode  

    - **Gerekli:** Evet  

    - **Değerler:** <*site kodu*>  

    - **Ayrıntılar:** Hiyerarşinizde siteyi benzersiz şekilde tanımlayan üç alfasayısal karakter belirtir.  

- **Anahtar adı:** SiteName  

    - **Gerekli:** Evet  

    - **Değerler:** <*site adı*>  

    - **Ayrıntılar:** Bu site için adı belirtir.  

- **Anahtar Adı:** SMSInstallDir  

    - **Gerekli:** Evet  

    - **Değerler:** <*Configuration Manager yükleme yolu*>

    - **Ayrıntılar:** Configuration Manager program dosyaları için yükleme klasörünü belirtir.  

- **Anahtar Adı:** SDKServer  

    - **Gerekli:** Evet  

    - **Değerler:** <*SMS sağlayıcısı FQDN 'si*>  

    - **Ayrıntılar:** SMS Sağlayıcısı’nı barındıracak sunucunun FQDN'sini belirtir. İlk yüklemeden sonra site için ek SMS Sağlayıcılarını yapılandırabilirsiniz.  

- **Anahtar Adı:** PrerequisiteComp  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= İndir  

        - `1`= Zaten indirildi  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının daha önce indirilip indirilmediğini belirtir. Örneğin, bir değeri kullanırsanız `0`, kurulum dosyaları indirir.  

- **Anahtar Adı:** PrerequisitePath  

    - **Gerekli:** Evet  

    - **Değerler:** <*Önkoşul dosyalarının kurulum yolu*>  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının yolunu belirtir. **ÖnkoşullarBu** değerine bağlı olarak, kurulum bu yolu indirilen dosyaları depolamak veya daha önce indirilen dosyaları bulmak için kullanır.  

- **Anahtar adı:** AdminConsole  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Configuration Manager konsolunun yüklenip yüklenmeyeceğini belirtir.  

- **Anahtar Adı:** JoinCEIP  

    > [!Note]  
    > Configuration Manager sürüm 1802 ' den başlayarak CEIP özelliği üründen kaldırılır.

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Katılımayın  

        - `1`= Birleştir  

    - **Ayrıntılar:** CEIP 'e katılıp katılmayacağını belirtir.  

- **Anahtar adı:** Yönetim noktası  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Yönetim noktası site sunucusu FQDN 'si*>  

    - **Ayrıntılar:** Yönetim noktası site sistem rolünü barındıracak sunucunun FQDN 'sini belirtir.  

- **Anahtar adı:** ManagementPointProtocol  

    - **Gerekli:** Hayır  

    - **Değerler:** `HTTPS` veya`HTTP`  

    - **Ayrıntılar:** Yönetim noktası için kullanılacak protokolü belirtir.  

- **Anahtar adı:** DistributionPoint  

    - **Gerekli:** Hayır  

    - **Değerler:** <*dağıtım noktası site sunucusu FQDN 'si*>  

    - **Ayrıntılar:** Dağıtım noktası site sistem rolünü barındıracak sunucunun FQDN 'sini belirtir.  

- **Anahtar adı:** DistributionPointProtocol  

    - **Gerekli:** Hayır  

    - **Değerler:** `HTTPS` veya`HTTP`  

    - **Ayrıntılar:** Dağıtım noktası için kullanılacak protokolü belirtir.  

- **Anahtar adı:** RoleCommunicationProtocol  

    - **Gerekli:** Evet  

    - **Değerler:** `EnforceHTTPS` veya`HTTPorHTTPS`  

    - **Ayrıntılar:** Tüm site sistemlerinin istemcilerden yalnızca HTTPS iletişimini kabul edecek şekilde mi yapılandırılacağını yoksa her site sistem rolü için iletişim yöntemini mi yapılandırılacağını belirtir. ' I seçtiğinizde `EnforceHTTPS`, istemcilerin istemci kimlik doğrulaması için geçerli bir ortak anahtar ALTYAPıSı (PKI) sertifikasına sahip olması gerekir.  

- **Anahtar adı:** Clientsusepkıcertificate  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Kullanma  

        - `1`= Kullan  

    - **Ayrıntılar:** İstemcilerin, site sistem rolleriyle iletişim kurmak için bir istemci PKI sertifikası kullanıp kullanmayacağını belirtir.  

- **Anahtar adı:** AddServerLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Configuration Manager konsolu, raporlar ve Configuration Manager nesneleri için kullanılabilecek sunucu dillerini belirtir. İngilizce varsayılan olarak kullanılabilir.  

- **Anahtar adı:** AddClientLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** İstemci bilgisayarlar için kullanılabilecek dilleri belirtir. İngilizce varsayılan olarak kullanılabilir.  

- **Anahtar adı:** DeleteServerLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Bir siteyi yükledikten sonra değiştirir. Kaldırılacak dilleri belirtir ve Configuration Manager konsolu, raporlar ve Configuration Manager nesneleri için artık kullanılabilir olmayacaktır. İngilizce varsayılan olarak kullanılabilir, kaldırılamaz.  

- **Anahtar adı:** DeleteClientLanguages  

    - **Gerekli:** Hayır  

    - **Değerler:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN,, ıTA, KOR, NLD, PLK, PTB, PTG, SVE, TRK veya ZHH  

    - **Ayrıntılar:** Bir siteyi yükledikten sonra değiştirir. Kaldırılacak dilleri belirtir ve artık istemci bilgisayarlar için kullanılabilir olmayacaktır. İngilizce varsayılan olarak kullanılabilir, kaldırılamaz.  

- **Anahtar adı:** MobileDeviceLanguage  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Mobil aygıt istemci dillerinin yüklenip yüklenmediğini belirtir.  

#### <a name="sqlconfigoptions"></a>SQLYapılandırmaSeçenekleri

- **Anahtar adı:** SQLServerName  

    - **Gerekli:** Evet  

    - **Değerler:** <*SQL Server adı*>  

    - **Ayrıntılar:** Site veritabanını barındırmak için SQL Server çalıştıran sunucunun veya kümelenmiş örneğin adını belirtir.  

- **Anahtar adı:** DatabaseName  

    - **Gerekli:** Evet  

    - **Değerler:** <*site veritabanı adı*> veya <*örneği adı*>\\<*site veritabanı adı*>  

    - **Ayrıntılar:** Oluşturulacak SQL Server veritabanının adını veya birincil site veritabanı yüklenirken kullanılacak SQL Server veritabanını belirtir.  

        > [!IMPORTANT]  
        > Varsayılan örneği kullanmıyorsanız, örnek adını ve site veritabanı adını belirtin.  

- **Anahtar adı:** SQLSSBPort  

    - **Gerekli:** Hayır  

    - **Değerler:** <*SSB bağlantı noktası numarası*>  

    - **Ayrıntılar:** SQL Server kullandığı SSB bağlantı noktasını belirtir. SSB, varsayılan olarak 4022 numaralı TCP bağlantı noktasını kullanır, ancak farklı bir bağlantı noktası kullanabilirsiniz.  

- **Anahtar adı:** SQLDataFilePath  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Database. mdb dosyasının yolu*>  

    - **Ayrıntılar:** Database. mdb dosyasını oluşturmak için başka bir konum belirtir.  

- **Anahtar adı:** SQLLogFilePath  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Database. ldf dosyasının yolu*>  

    - **Ayrıntılar:** Database. ldf dosyasını oluşturmak için başka bir konum belirtir.  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **Anahtar Adı:** CCARSiteServer  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Merkezi Yönetim sitesi FQDN 'si*>  

    - **Ayrıntılar:** Birincil bir sitenin Configuration Manager hiyerarşisine katıldığında bu CA 'ya ilişi belirtir. Kurulum sırasında CA 'ları belirtin.  

- **Anahtar adı:** CASRetryInterval  

    - **Gerekli:** Hayır  

    - **Değerler:** <*dakika cinsinden Aralık*>  

    - **Ayrıntılar:** Bağlantı başarısız olduktan sonra CA 'lara bağlanmayı denemek için dakika cinsinden yeniden deneme aralığını belirtir. Örneğin, CA bağlantısı başarısız olursa, birincil site **CASRetryInterval** değeri için belirttiğiniz dakika sayısını bekler ve ardından bağlantıyı yeniden durdurur.  

- **Anahtar adı:** WaitForCASTimeout  

    - **Gerekli:** Hayır  

    - **Değerler:** <*dakika cinsinden 0 ila 100 arasında zaman aşımı*>  

    - **Ayrıntılar:** Birincil sitenin CAS 'e bağlanması için dakika cinsinden en uzun zaman aşımı değerini belirtir. Örneğin, birincil site bir CA 'ya bağlanamazsa, **WaitForCASTimeout** süresine ulaşılana kadar, birincil site **CASRetryInterval** değerine göre CAS bağlantısını yeniden dener. Öğesinden öğesinden `0` bir değer belirtebilirsiniz `100`.  

#### <a name="cloudconnectoroptions"></a>Cloudconnectoroçen

- **Anahtar adı:** CloudConnector  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Bu sitede bir hizmet bağlantı noktası yüklenip yüklenmeyeceğini belirtir. Hizmet bağlantı noktasını yalnızca bir hiyerarşinin üst katman sitesine yükleyebildiğinden, bir alt birincil site için bu değeri olarak `0` ayarlayın.  

- **Anahtar adı:** CloudConnectorServer  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*hizmet bağlantı noktası sunucu FQDN 'si*\>  

    - **Ayrıntılar:** Hizmet bağlantı noktası site sistemi rolünü barındıracak sunucunun FQDN 'sini belirtir.  

- **Anahtar adı:** UseProxy  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Hizmet bağlantı noktasının bir ara sunucu kullanıp kullanmadığını belirtir.  

- **Anahtar adı:** ProxyName  

    - **Gerekli:** **UseProxy** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*proxy sunucusu FQDN 'si*>  

    - **Ayrıntılar:** Hizmet bağlantı noktasının kullandığı proxy sunucusunun FQDN 'sini belirtir.  

- **Anahtar adı:** ProxyPort  

    - **Gerekli:** **UseProxy** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*bağlantı noktası numarası*>  

    - **Ayrıntılar:** Proxy bağlantı noktası için kullanılacak bağlantı noktası numarasını belirtir.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Anahtar adı:** Saactıve

    - **Gerekli:** Hayır

    - **Değerler:**

        - `0`= Yazılım güvencesi yok

        - `1`= Yazılım Güvencesi etkin

    - **Ayrıntılar:** Etkin yazılım güvencesi olup olmadığını belirtin. Daha fazla bilgi için bkz. [ürün ve lisanslama hakkında SSS](../../../understand/product-and-licensing-faq.md).

- **Anahtar adı:** CurrentBranch

    - **Gerekli:** Hayır

    - **Değerler:**

        - `0`= LTSB 'yi yükler

        - `1`= Geçerli dalı yükler

    - **Ayrıntılar:** Configuration Manager geçerli dal veya uzun süreli bakım dalı (LTSB) kullanıp kullanmayacağınızı belirtin. Daha fazla bilgi için, [hangi Configuration Manager dalını kullanmalıyım?](../../../understand/which-branch-should-i-use.md)bölümüne bakın.

### <a name="unattended-recovery-for-a-cas"></a>CA 'LAR için katılımsız kurtarma

Bir CA 'yı Katılımsız Kurulum betik dosyası kullanarak kurtarmak için aşağıdaki ayrıntıları kullanın.  

#### <a name="identification"></a>Kimlik

- **Anahtar Adı:** Eylem  

    - **Gerekli:** Evet  

    - **Değerler:** `RecoverCCAR`  

    - **Ayrıntılar:** CA 'ları kurtarır.  

- **Anahtar adı:** CDLatest  

    - **Gerekli:** Evet, yalnızca CD 'den medya kullanılırken. En son klasör.

    - **Değerler:**

        - `1`= CD 'den medya kullanıyorsunuz. Sürümü

        - 1 dışında bir değer = CD 'yi kullanmıyoruz. En son medya

    - **Ayrıntılar:** Birincil bir siteyi veya CA 'yı yüklediğinizde veya kurtardığınızda ve kurulum 'u CD 'den çalıştırırsanız. En son klasör, bu anahtarı ve değeri içerir. Bu değer, kurulum 'u CD 'den medya kullandığınızı bildirir. Sürümü.

#### <a name="recoveryoptions"></a>KurtarmaSeçenekleri

- **Anahtar adı:** ServerRecoveryOptions  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `1`= Site sunucusunu kurtar ve SQL Server

        - `2`= Yalnızca site sunucusunu kurtar

        - `4`= Yalnızca SQL Server kurtar  

    - **Ayrıntılar:** Kurulumun site sunucusunu, SQL Server veya her ikisini de kurtarıp kurtarmayacağını belirtir. Aşağıdaki seçenekler, belirtilen değere göre de gereklidir:  

        - **1** veya **2**: siteyi bir site yedeklemesini kullanarak kurtarmak Için, **SiteServerBackupLocation**için bir değer belirtin. Bir değer belirtmezseniz, kurulum siteyi bir yedekleme kümesinden geri yüklemeden yeniden yükler.  

        - **4**: site veritabanını yedeklemeden geri yüklemek Için olan **DatabaseRecoveryOptions** anahtarı Için **10** değerini yapılandırdığınızda **BackupLocation** anahtarı gereklidir.  

- **Anahtar Adı:** DatabaseRecoveryOptions  

    - **Gerekli:** **ServerRecoveryOptions** ayarı **1** veya **4**değerine sahip olduğunda bu anahtar gereklidir.  

    - **Değerler:**

        - `10`= Site veritabanını yedekten geri yükleyin.  

        - `20`= Başka bir yöntemle el ile kurtarılan bir site veritabanı kullanın.  

        - `40`= Site için yeni bir veritabanı oluşturun. Kullanılabilir site veritabanı yedeklemesi olmadığında bu seçeneği kullanın. Site, diğer sitelerden çoğaltma aracılığıyla genel ve site verilerini kurtarır.  

        - `80`= Veritabanı kurtarmayı atlayın.  

    - **Ayrıntılar:** Kurulumun SQL Server site veritabanını nasıl kurtaracağını belirtir.  

- **Anahtar Adı:** ReferenceSite  

    - **Gerekli:** Bu anahtar, **DatabaseRecoveryOptions** ayarında **40**değeri olduğunda gereklidir.  

    - **Değerler:** <*başvuru site FQDN 'si*>  

    - **Ayrıntılar:** Veritabanı yedeklemesi değişiklik izleme saklama süresinden eskiyse veya siteyi bir yedek olmadan kurtardığınızda, CA 'ların genel verileri kurtarmak için kullandığı referans birincil sitesini belirtin.  

        Bir başvuru sitesi belirtmezseniz ve yedekleme değişiklik izleme tutma süresinden eskiyse, tüm birincil siteler CA 'lardan geri yüklenen verilerle yeniden başlatılır.  

        Bir başvuru sitesi belirtmezseniz ve yedekleme değişiklik izleme tutma süresi içinde olduğunda, yalnızca yedeklemeden sonra yapılan değişiklikler birincil sitelerden çoğaltılır. Farklı birincil sitelerden çakışan değişiklikler olduğunda, CA 'LAR aldığı ilk olanı kullanır.  

- **Anahtar adı:** SiteServerBackupLocation  

    - **Gerekli:** Hayır  

    - **Değerler:** <*site sunucusu yedekleme kümesinin yolu*>  

    - **Ayrıntılar:** Site sunucusu yedekleme kümesinin yolunu belirtir. **ServerRecoveryOptions** ayarı **1** veya **2**değerine sahip olduğunda bu anahtar isteğe bağlıdır. Bir site yedeklemesini kullanarak siteyi kurtarmak için **SiteServerBackupLocation** anahtarı için bir değer belirleyin. Bir değer belirtmezseniz, kurulum siteyi bir yedekleme kümesinden geri yüklemeden yeniden yükler.  

- **Anahtar adı:** BackupLocation  

    - **Gerekli:** **ServerRecoveryOptions** anahtarı için **1** veya **4** değerini yapılandırdığınızda ve **DatabaseRecoveryOptions** anahtarı için **10** değerini yapılandırdığınızda bu anahtar gereklidir.  

    - **Değerler:** <*site veritabanı yedekleme kümesinin yolu*>  

    - **Ayrıntılar:** Site veritabanı yedekleme kümesinin yolunu belirtir.  

#### <a name="options"></a>Seçenekler

- **Anahtar Adı:** ProductID  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= tireleri olan geçerli bir ürün anahtarı

        - `Eval`= Configuration Manager değerlendirme sürümünü yükler

    - **Ayrıntılar:** Tireler dahil Configuration Manager yüklemesi ürün anahtarını belirtir.

- **Anahtar Adı:** SiteCode  

    - **Gerekli:** Evet  

    - **Değerler:** <*site kodu*>  

    - **Ayrıntılar:** Hiyerarşinizde siteyi benzersiz şekilde tanımlayan üç alfasayısal karakter belirtir. Hatanın hatadan önce kullandığı site kodunu belirtin.

- **Anahtar adı:** SiteName  

    - **Gerekli:** Hayır  

    - **Değerler:** <*site adı*>  

    - **Ayrıntılar:** Bu site için adı belirtir.  

- **Anahtar Adı:** SMSInstallDir  

    - **Gerekli:** Evet  

    - **Değerler:** <*Configuration Manager yükleme yolu*>  

    - **Ayrıntılar:** Configuration Manager program dosyaları için yükleme klasörünü belirtir.  

- **Anahtar Adı:** SDKServer  

    - **Gerekli:** Evet  

    - **Değerler:** <*SMS sağlayıcısı FQDN 'si*>  

    - **Ayrıntılar:** SMS sağlayıcısını barındıran sunucunun FQDN 'sini belirtir. Hatadan önce SMS sağlayıcısını barındıran sunucuyu belirtin.  

        İlk yüklemeden sonra site için ek SMS Sağlayıcılarını yapılandırabilirsiniz. SMS sağlayıcısı hakkında daha fazla bilgi için bkz. [plan for SMS Provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Anahtar Adı:** PrerequisiteComp  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= İndir  

        - `1`= Zaten indirildi  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının daha önce indirilip indirilmediğini belirtir. Örneğin, **0**değerini kullanırsanız, kurulum dosyaları indirir.  

- **Anahtar Adı:** PrerequisitePath  

    - **Gerekli:** Evet  

    - **Değerler:** <*Önkoşul dosyalarının kurulum yolu*>  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının yolunu belirtir. **ÖnkoşullarBu** değerine bağlı olarak, kurulum bu yolu indirilen dosyaları depolamak veya daha önce indirilen dosyaları bulmak için kullanır.  

- **Anahtar adı:** AdminConsole  

    - **Gerekli:** **ServerRecoveryOptions** ayarının **4**değerine sahip olduğu durumlar dışında bu anahtar gerekir.  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Configuration Manager konsolunun yüklenip yüklenmeyeceğini belirtir.  

- **Anahtar Adı:** JoinCEIP  

    > [!Note]  
    > Configuration Manager sürüm 1802 ' den başlayarak CEIP özelliği üründen kaldırılır.

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Katılımayın  

        - `1`= Birleştir  

    - **Ayrıntılar:** CEIP 'e katılıp katılmayacağını belirtir.  

#### <a name="sqlconfigoptions"></a>SQLYapılandırmaSeçenekleri

- **Anahtar adı:** SQLServerName  

    - **Gerekli:** Evet  

    - **Değerler:** <*SQL Server adı*>  

    - **Ayrıntılar:** SQL Server çalıştıran ve site veritabanını barındıran bir sunucunun veya kümelenmiş örneğin adını belirtir. Hatadan önce site veritabanını barındıran aynı sunucuyu belirtin.  

- **Anahtar adı:** DatabaseName  

    - **Gerekli:** Evet  

    - **Değerler:** <*site veritabanı adı*> veya <*örneği adı*>\\<*site veritabanı adı*>  

    - **Ayrıntılar:** Oluşturulacak SQL Server veritabanının adını veya CAS veritabanını yüklerken kullanılacak SQL Server veritabanını belirtir. Hata öncesi kullanılan aynı veritabanı adını belirtin.  

        > [!IMPORTANT]  
        > Varsayılan örneği kullanmıyorsanız, örnek adını ve site veritabanı adını belirtin.  

- **Anahtar adı:** SQLSSBPort  

    - **Gerekli:** Evet  

    - **Değerler:** <*SSB bağlantı noktası numarası*>  

    - **Ayrıntılar:** SQL Server kullandığı SSB bağlantı noktasını belirtir. Varsayılan olarak SSB, 4022 numaralı TCP bağlantı noktasını kullanır. Hatadan önce kullanılan SSB bağlantı noktasını belirtin.  

- **Anahtar adı:** SQLDataFilePath  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Database. mdb dosyasının yolu*>  

    - **Ayrıntılar:** Database. mdb dosyasını oluşturmak için başka bir konum belirtir.  

- **Anahtar adı:** SQLLogFilePath  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Database. ldf dosyasının yolu*>  

    - **Ayrıntılar:** Database. ldf dosyasını oluşturmak için başka bir konum belirtir.  

#### <a name="cloudconnectoroptions"></a>Cloudconnectoroçen

- **Anahtar adı:** CloudConnector  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Bu sitede bir hizmet bağlantı noktası yüklenip yüklenmeyeceğini belirtir. Hizmet bağlantı noktasını yalnızca bir hiyerarşinin üst katman sitesine yükleyebildiğinden, bu değer bir alt birincil site için **0** olmalıdır.  

- **Anahtar adı:** CloudConnectorServer  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*hizmet bağlantı noktası sunucu FQDN 'si*>  

    - **Ayrıntılar:** Hizmet bağlantı noktası site sistemi rolünü barındıracak sunucunun FQDN 'sini belirtir.  

- **Anahtar adı:** UseProxy  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Hizmet bağlantı noktasının bir ara sunucu kullanıp kullanmadığını belirtir.  

- **Anahtar adı:** ProxyName  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*proxy sunucusu FQDN 'si*>  

    - **Ayrıntılar:** Hizmet bağlantı noktasının kullandığı proxy sunucusunun FQDN 'sini belirtir.  

- **Anahtar adı:** ProxyPort  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*bağlantı noktası numarası*>  

    - **Ayrıntılar:** Proxy bağlantı noktası için kullanılacak bağlantı noktası numarasını belirtir.  

### <a name="unattended-recovery-for-a-primary-site"></a>Birincil site için katılımsız kurtarma

Bir birincil siteyi katılımsız bir Kurulum betik dosyası kullanarak kurtarmak için aşağıdaki ayrıntıları kullanın.  

#### <a name="identification"></a>Kimlik

- **Anahtar Adı:** Eylem  

    - **Gerekli:** Evet  

    - **Değerler:** `RecoverPrimarySite`  

    - **Ayrıntılar:** Birincil bir siteyi kurtarır.  

- **Anahtar adı:** CDLatest  

    - **Gerekli:** Evet, yalnızca CD 'den medya kullanılırken. En son klasör.

    - **Değerler:**

        - `1`= CD 'den medya kullanıyorsunuz. Sürümü

        - 1 dışında bir değer = CD 'yi kullanmıyoruz. En son medya

    - **Ayrıntılar:** Birincil bir siteyi veya CA 'yı yüklediğinizde veya kurtardığınızda ve kurulum 'u CD 'den çalıştırırsanız. En son klasör, bu anahtarı ve değeri içerir. Bu değer, kurulum 'u CD 'den medya kullandığınızı bildirir. Sürümü.

#### <a name="recoveryoptions"></a>KurtarmaSeçenekleri

- **Anahtar adı:** ServerRecoveryOptions  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `1`= Site sunucusunu kurtar ve SQL Server

        - `2`= Yalnızca site sunucusunu kurtar

        - `4`= Yalnızca SQL Server kurtar  

    - **Ayrıntılar:** Kurulumun site sunucusunu, SQL Server veya her ikisini de kurtarıp kurtarmayacağını belirtir. Aşağıdaki seçenekler, belirtilen değere göre de gereklidir:  

        - **1** veya **2**: siteyi bir site yedeklemesini kullanarak kurtarmak Için, **SiteServerBackupLocation**için bir değer belirtin. Bir değer belirtmezseniz, kurulum siteyi bir yedekleme kümesinden geri yüklemeden yeniden yükler.  

        - **4**: site veritabanını yedeklemeden geri yüklemek Için olan **DatabaseRecoveryOptions** anahtarı Için **10** değerini yapılandırdığınızda **BackupLocation** anahtarı gereklidir.  

- **Anahtar Adı:** DatabaseRecoveryOptions  

    - **Gerekli:** **ServerRecoveryOptions** ayarı **1** veya **4**değerine sahip olduğunda bu anahtar gereklidir.  

    - **Değerler:**

        - `10`= Site veritabanını yedekten geri yükleyin.  

        - `20`= Başka bir yöntemle el ile kurtarılan bir site veritabanı kullanın.  

        - `40`= Site için yeni bir veritabanı oluşturun. Kullanılabilir site veritabanı yedeklemesi olmadığında bu seçeneği kullanın. Site, diğer sitelerden çoğaltma aracılığıyla genel ve site verilerini kurtarır.  

        - `80`= Veritabanı kurtarmayı atlayın.  

    - **Ayrıntılar:** Kurulumun SQL Server site veritabanını nasıl kurtaracağını belirtir.  

- **Anahtar adı:** SiteServerBackupLocation  

    - **Gerekli:** Hayır  

    - **Değerler:** <*site sunucusu yedekleme kümesinin yolu*>  

    - **Ayrıntılar:** Site sunucusu yedekleme kümesinin yolunu belirtir. **ServerRecoveryOptions** ayarı **1** veya **2**değerine sahip olduğunda bu anahtar isteğe bağlıdır. Bir site yedeklemesini kullanarak siteyi kurtarmak için **SiteServerBackupLocation** anahtarı için bir değer belirleyin. Bir değer belirtmezseniz, kurulum siteyi bir yedekleme kümesinden geri yüklemeden yeniden yükler.  

- **Anahtar adı:** BackupLocation  

    - **Gerekli:** **ServerRecoveryOptions** anahtarı için **1** veya **4** değerini yapılandırdığınızda ve **DatabaseRecoveryOptions** anahtarı için **10** değerini yapılandırdığınızda bu anahtar gereklidir.  

    - **Değerler:** <*site veritabanı yedekleme kümesinin yolu*>  

    - **Ayrıntılar:** Site veritabanı yedekleme kümesinin yolunu belirtir.  

#### <a name="options"></a>Seçenekler

- **Anahtar Adı:** ProductID  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= tireleri olan geçerli bir ürün anahtarı

        - `Eval`= Configuration Manager değerlendirme sürümünü yükler

    - **Ayrıntılar:** Tireler dahil Configuration Manager yüklemesi ürün anahtarını belirtir.

- **Anahtar Adı:** SiteCode  

    - **Gerekli:** Evet  

    - **Değerler:** <*site kodu*>  

    - **Ayrıntılar:** Hiyerarşinizde siteyi benzersiz şekilde tanımlayan üç alfasayısal karakter belirtir. Hatanın hatadan önce kullandığı site kodunu belirtin.

- **Anahtar adı:** SiteName  

    - **Gerekli:** Hayır  

    - **Değerler:** <*site adı*>  

    - **Ayrıntılar:** Bu site için adı belirtir.  

- **Anahtar Adı:** SMSInstallDir  

    - **Gerekli:** Evet  

    - **Değerler:** <*Configuration Manager yükleme yolu*>  

    - **Ayrıntılar:** Configuration Manager program dosyaları için yükleme klasörünü belirtir.  

- **Anahtar Adı:** SDKServer  

    - **Gerekli:** Evet  

    - **Değerler:** <*SMS sağlayıcısı FQDN 'si*>  

    - **Ayrıntılar:** SMS sağlayıcısını barındıran sunucunun FQDN 'sini belirtir. Hatadan önce SMS sağlayıcısını barındıran sunucuyu belirtin. İlk yüklemeden sonra site için ek SMS Sağlayıcılarını yapılandırabilirsiniz. SMS sağlayıcısı hakkında daha fazla bilgi için bkz. [plan for SMS Provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Anahtar Adı:** PrerequisiteComp  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= İndir  

        - `1`= Zaten indirildi  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının daha önce indirilip indirilmediğini belirtir. Örneğin, **0**değerini kullanırsanız, kurulum dosyaları indirir.  

- **Anahtar Adı:** PrerequisitePath  

    - **Gerekli:** Evet  

    - **Değerler:** <*Önkoşul dosyalarının kurulum yolu*>  

    - **Ayrıntılar:** Kurulum önkoşul dosyalarının yolunu belirtir. **ÖnkoşullarBu** değerine bağlı olarak, kurulum bu yolu indirilen dosyaları depolamak veya daha önce indirilen dosyaları bulmak için kullanır.  

- **Anahtar adı:** AdminConsole  

    - **Gerekli:** **ServerRecoveryOptions** ayarının **4**değerine sahip olduğu durumlar dışında bu anahtar gerekir.  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Configuration Manager konsolunun yüklenip yüklenmeyeceğini belirtir.  

- **Anahtar Adı:** JoinCEIP  

    > [!Note]  
    > Configuration Manager sürüm 1802 ' den başlayarak CEIP özelliği üründen kaldırılır.

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Katılımayın  

        - `1`= Birleştir  

    - **Ayrıntılar:** CEIP 'e katılıp katılmayacağını belirtir.  

#### <a name="sqlconfigoptions"></a>SQLYapılandırmaSeçenekleri

- **Anahtar adı:** SQLServerName  

    - **Gerekli:** Evet  

    - **Değerler:** <*SQL Server adı*>  

    - **Ayrıntılar:** Site veritabanını barındırmak için SQL Server çalıştıran sunucunun veya kümelenmiş örneğin adını belirtir. Hatadan önce site veritabanını barındıran aynı sunucuyu belirtin.  

- **Anahtar adı:** DatabaseName  

    - **Gerekli:** Evet  

    - **Değerler:** <*site veritabanı adı*> veya <*örneği adı*>\\<*site veritabanı adı*>

    - **Ayrıntılar:** Oluşturulacak SQL Server veritabanının adını veya CAS veritabanını yüklerken kullanılacak SQL Server veritabanını belirtir. Hata öncesi kullanılan aynı veritabanı adını belirtin.  

        > [!IMPORTANT]  
        > Varsayılan örneği kullanmıyorsanız, örnek adını ve site veritabanı adını belirtin.  

- **Anahtar adı:** SQLSSBPort  

    - **Gerekli:** Evet  

    - **Değerler:** <*SSB bağlantı noktası numarası*>  

    - **Ayrıntılar:** SQL Server kullandığı SSB bağlantı noktasını belirtir. Varsayılan olarak SSB, 4022 numaralı TCP bağlantı noktasını kullanır. Hatadan önce kullanılan SSB bağlantı noktasını belirtin.  

- **Anahtar adı:** SQLDataFilePath  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Database. mdb dosyasının yolu*>  

    - **Ayrıntılar:** Database. mdb dosyasını oluşturmak için başka bir konum belirtir.  

- **Anahtar adı:** SQLLogFilePath  

    - **Gerekli:** Hayır  

    - **Değerler:** <*Database. ldf dosyasının yolu*>  

    - **Ayrıntılar:** Database. ldf dosyasını oluşturmak için başka bir konum belirtir.  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **Anahtar Adı:** CCARSiteServer  

    - **Gerekli:** Ayrıntılara bakın.  

    - **Değerler:** <*CA 'lar için site kodu*>  

    - **Ayrıntılar:** Birincil sitenin Configuration Manager hiyerarşisine katıldığında bağlanacağı CA 'ları belirtir. Birincil site, hatadan önce bir CA 'ya eklenmişse, bu ayar gereklidir. Hatadan önce CAS için kullanılan site kodunu belirtin.  

- **Anahtar adı:** CASRetryInterval  

    - **Gerekli:** Hayır  

    - **Değerler:** <*dakika cinsinden Aralık*>  

    - **Ayrıntılar:** Bağlantı başarısız olduktan sonra CA 'lara bağlanmayı denemek için dakika cinsinden yeniden deneme aralığını belirtir. Örneğin, CA bağlantısı başarısız olursa, birincil site **CASRetryInterval** değeri için belirttiğiniz dakika sayısını bekler ve ardından bağlantıyı yeniden dener.  

- **Anahtar adı:** WaitForCASTimeout  

    - **Gerekli:** Hayır  

    - **Değerler:** <*dakika cinsinden zaman aşımı*>  

    - **Ayrıntılar:** Birincil sitenin CAS 'e bağlanması için dakika cinsinden en uzun zaman aşımı değerini belirtir. Örneğin, birincil site bir CA 'ya bağlanamazsa, **WaitForCASTimeout** süresine ulaşılana kadar, birincil site **CASRetryInterval** değerine göre CAS bağlantısını yeniden dener. `0` İçin `100`bir değeri belirtebilirsiniz.  

#### <a name="cloudconnectoroptions"></a>Cloudconnectoroçen

- **Anahtar adı:** CloudConnector  

    - **Gerekli:** Evet  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Bu sitede bir hizmet bağlantı noktası yüklenip yüklenmeyeceğini belirtir. Hizmet bağlantı noktasını yalnızca bir hiyerarşinin üst katman sitesine yükleyebildiğinden, bu değer bir alt birincil site `0` için olmalıdır.  

- **Anahtar adı:** CloudConnectorServer  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*hizmet bağlantı noktası sunucu FQDN 'si*>  

    - **Ayrıntılar:** Hizmet bağlantı noktası site sistemi rolünü barındıracak sunucunun FQDN 'sini belirtir.  

- **Anahtar adı:** UseProxy  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:**

        - `0`= Yüklemeyin  

        - `1`= Install  

    - **Ayrıntılar:** Hizmet bağlantı noktasının bir ara sunucu kullanıp kullanmadığını belirtir.  

- **Anahtar adı:** ProxyName  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*proxy sunucusu FQDN 'si*>  

    - **Ayrıntılar:** Hizmet bağlantı noktasının kullandığı proxy sunucusunun FQDN 'sini belirtir.  

- **Anahtar adı:** ProxyPort  

    - **Gerekli:** **Cloudconnector** eşittir 1 olduğunda gereklidir  

    - **Değerler:** <*bağlantı noktası numarası*>  

    - **Ayrıntılar:** Proxy bağlantı noktası için kullanılacak bağlantı noktası numarasını belirtir.  
