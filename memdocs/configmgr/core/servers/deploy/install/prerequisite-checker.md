---
title: Önkoşul denetleyicisi
titleSuffix: Configuration Manager
description: Bir siteyi veya site sistemi rolü yüklemesini engelleyebilen sorunları belirlemek ve onarmak için önkoşul denetleyicisi 'ni nasıl kullanacağınızı öğrenin.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ee871d99285bee3a4489d88bf0d203bf74cde3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718178"
---
# <a name="prerequisite-checker-for-configuration-manager"></a>Configuration Manager için önkoşul denetleyicisi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Bir Configuration Manager sitesini yüklemek veya yükseltmek için kurulum 'U çalıştırmadan önce veya yeni bir sunucuya site sistemi rolü yüklemeden önce, bu tek başına uygulamayı (**prereqchk. exe**), sunucu hazırlığını doğrulamak için kullanmak istediğiniz Configuration Manager sürümünden kullanabilirsiniz. Bir siteyi veya site sistemi rolü yüklemesini engelleyen sorunları belirlemek ve onarmak için önkoşul denetleyicisi 'ni kullanın.  

> [!NOTE]  
>  Önkoşul denetleyicisi her zaman Kurulumun bir parçası olarak çalışır.  

Varsayılan olarak, önkoşul denetleyicisi çalıştırıldığında:  

-   Çalıştığı sunucuyu doğrular.  
-   Yerel bilgisayar, var olan bir site sunucusu için taranır ve yalnızca site için geçerli olan denetimler çalıştırılır.  
-   Mevcut bir site algılanmazsa, tüm önkoşul kuralları çalıştırılır.  
-   Kurulum için gerekli olan yazılımların ve ayarların yüklü olduğunu doğrulamak için kuralları denetler. Gerekli yazılımın, önkoşul denetleyicisi tarafından doğrulanmamış ek yapılandırma veya yazılım güncelleştirmeleri gerektirmesi olasıdır.  
-   Bu, sonuçlarını bilgisayarın sistem sürücüsündeki **ConfigMgrPrereq. log** dosyasında günlüğe kaydeder. Günlük dosyası, uygulama arabiriminde görünmeyen ek bilgiler içerebilir.  

Önkoşul denetleyicisi 'Ni bir komut isteminde çalıştırdığınızda ve belirli komut satırı seçeneklerini belirttiğinizde:  

-   Önkoşul denetleyicisi, yalnızca komut satırında belirttiğiniz site sunucusu veya site sistemleriyle ilişkili denetimleri gerçekleştirir.  
-   Uzak bir bilgisayarı denetlemek için Kullanıcı hesabınızın uzak bilgisayarda yönetici haklarına sahip olması gerekir.  

Önkoşul denetleyicisi 'nin gerçekleştirdiği denetimler hakkında daha fazla bilgi için bkz. [Configuration Manager için önkoşul denetimleri listesi](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Önkoşul denetleyicisi dosyalarını başka bir bilgisayara Kopyala  

1.  Windows Gezgini 'nde, aşağıdaki konumlardan birine gidin:  

    -   **&lt;*Configuration Manager yükleme medyası*\>\smssetup\bin\x64**  
    -   **&lt;*Configuration Manager yükleme yolu*\>\Bin\X64**  

2.  Aşağıdaki dosyaları diğer bilgisayardaki hedef klasöre kopyalayın:  

    - prereqchk. exe
    - Prereqcore. dll
    - prereqchkres. dll
      - Bu dosya, install dilinin alt klasörüdür. Örneğin, Ingilizce `00000409` alt klasördeyse. <!--586808-->
    - basesql. dll
    - Basesvr. dll
    - baseutil. dll

##  <a name="run-prerequisite-checker-with-default-checks"></a>Önkoşul denetleyicisini varsayılan denetimler ile Çalıştır  

1.  Windows Gezgini 'nde, aşağıdaki konumlardan birine gidin:  

    -   **&lt;*Configuration Manager yükleme medyası*\>\smssetup\bin\x64**  
    -   **&lt;*Configuration Manager yükleme yolu*\>\Bin\X64**  

2.  Önkoşul denetleyicisi 'ni başlatmak için **prereqchk. exe dosyasını** çalıştırın.   
    Önkoşul denetleyicisi var olan siteleri algılar ve bulunursa, yükseltme hazırlığı için denetimler gerçekleştirir. Hiçbir site bulunamazsa, tüm denetimler gerçekleştirilir. **Site türü** sütunu, kuralın ilişkilendirildiği site sunucusu veya site sistemi hakkında bilgi sağlar.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Önkoşul denetleyicisi 'Ni bir komut isteminden tüm varsayılan denetimler için Çalıştır  

1.  Bir komut Istemi penceresi açın ve dizinleri aşağıdaki konumlardan biriyle değiştirin:  

    -   **&lt;*Configuration Manager yükleme medyası*\>\smssetup\bin\x64**  
    -   **&lt;*Configuration Manager yükleme yolu*\>\Bin\X64**  

2.  Önkoşul denetleyicisi 'ni başlatmak için **prereqchk. exe/LOCAL** girin ve sunucuda tüm önkoşul denetimlerini çalıştırın.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Seçenekleri kullanmak için bir komut isteminden önkoşul denetleyicisi 'ni çalıştırın  

1. Bir komut Istemi penceresi açın ve dizinleri aşağıdaki konumlardan biriyle değiştirin:  

   -   **&lt;*Configuration Manager yükleme medyası*\>\smssetup\bin\x64**  
   -   **&lt;*Configuration Manager yükleme yolu*\>\Bin\X64**  

2. Aşağıdaki komut satırı seçeneklerinden bir veya daha fazlasını ekleme ile **prereqchk. exe** girin.  

   Örneğin, bir birincil siteyi denetlemek için aşağıdakileri kullanabilirsiniz:  

      **prereqchk. exe [/NOUı]/PRı/SQL &lt;fqdn 'si SQL Server\> /SDK &lt;FQDN of SMS Provider\> [/JOIN &lt;yönetim sitesinin\> &lt;\> &lt;\>FQDN 'si**  

   **Merkezi Yönetim sitesi sunucusu:**  

   -   **/NOUı**  

        Gerekli değildir. Önkoşul denetleyicisi 'Ni Kullanıcı arabirimini görüntülemeden başlatır. Komut satırında herhangi bir seçenekten önce bu seçeneği belirtmeniz gerekir.  

   -   **/CAS**  

        Gereklidir. Yerel bilgisayarın merkezi yönetim sitesi için gereksinimleri karşıladığını doğrular.  

   -   **SQL Server/SQL &lt; *FQDN 'si*>**  

        Gereklidir. Tam etki alanı adını (FQDN) kullanarak, belirtilen bilgisayarın Configuration Manager site veritabanını barındırmak için SQL Server gereksinimlerini karşıladığını doğrular.  

   -   **&lt; *SMS sağlayıcısının/SDK FQDN 'si*>**  

        Gereklidir. Belirtilen bilgisayarın SMS sağlayıcısı için gereksinimleri karşıladığını doğrular.  

   -   **/Ssbport**  

        Gerekli değildir. SQL Server Hizmet Aracısı (SSB) bağlantı noktasında iletişime izin vermek için bir güvenlik duvarı istisnasının geçerli olduğunu doğrular. Varsayılan SSB bağlantı noktası 4022 ' dir.  

   -   **InstallDir &lt; *Configuration Manager yükleme yolu*>**  

        Gerekli değildir. Site yüklemesi için gereksinimlerde bulunan en düşük disk alanını doğrular.  

   **Birincil site sunucusu:**  

   -   **/NOUı**  

       Gerekli değildir. Önkoşul denetleyicisi 'Ni Kullanıcı arabirimini görüntülemeden başlatır. Komut satırında herhangi bir seçenekten önce bu seçeneği belirtmeniz gerekir.  

   -   **/PRı**  

        Gereklidir. Yerel bilgisayarın birincil site için koşulları karşıladığını doğrular.  

   -   **SQL Server/SQL &lt; *FQDN 'si*>**  

        Gereklidir. Belirtilen bilgisayarın, Configuration Manager site veritabanını barındırmak için SQL Server gereksinimlerini karşıladığını doğrular.  

   -   **&lt; *SMS sağlayıcısının/SDK FQDN 'si*>**  

        Gereklidir. Belirtilen bilgisayarın SMS sağlayıcısı için gereksinimleri karşıladığını doğrular.  

   -   **/Merkez &lt; *yönetim sitesinin FQDN* 'sine Birleştir>**  

        Gerekli değildir. Yerel bilgisayarın, merkezi yönetim site sunucusuna bağlanmak için gereken koşulları karşıladığını doğrular.  

   -   **&lt; *Yönetim noktasının/MP FQDN 'si*>**  

        Gerekli değildir. Belirtilen bilgisayarın yönetim noktası site sistem rolü gereksinimlerini karşıladığını doğrular. Bu seçenek yalnızca **/PRI** seçeneğini kullandığınızda desteklenir.  

   -   **&lt; *Dağıtım noktasının/DP FQDN 'si*>**  

        Gerekli değildir. Belirtilen bilgisayarın dağıtım noktası site sistem rolü gereksinimlerini karşıladığını doğrular. Bu seçenek yalnızca **/PRI** seçeneğini kullandığınızda desteklenir.  

   -   **/Ssbport**  

        Gerekli değildir. SSB bağlantı noktasında iletişime izin vermek için bir güvenlik duvarı istisnasının geçerli olduğunu doğrular. Varsayılan SSB bağlantı noktası 4022 ' dir.  

   -   **InstallDir &lt; *Configuration Manager yükleme yolu*>**  

        Gerekli değildir. Site yüklemesi için gereksinimlerde bulunan en düşük disk alanını doğrular.  

   **İkincil site sunucusu:**  

   -   **/NOUı**  

        Gerekli değildir. Önkoşul denetleyicisi 'Ni Kullanıcı arabirimini görüntülemeden başlatır. Komut satırında herhangi bir seçenekten önce bu seçeneği belirtmeniz gerekir.  

   -   **/ &lt;Sn *ikincil site sunucusunun FQDN 'si*>**  

        Gereklidir. Belirtilen bilgisayarın ikincil site için koşulları karşıladığını doğrular.  

   -   **/INSTALLSQLEXPRESS**  

        Gerekli değildir. SQL Server Express belirtilen bilgisayara yüklenebildiğini doğrular.  

   -   **/Ssbport**  

        Gerekli değildir. SSB bağlantı noktası için iletişime izin vermek üzere bir güvenlik duvarı istisnasının geçerli olduğunu doğrular. Varsayılan SSB bağlantı noktası 4022 ' dir.  

   -   **/Sqlport**  

        Gerekli değildir. SQL Server hizmet bağlantı noktası için iletişime izin vermek üzere bir güvenlik duvarı istisnasının geçerli olduğunu ve bağlantı noktasının başka bir SQL Server adlandırılmış örneği tarafından kullanımda olmadığını doğrular. Varsayılan bağlantı noktası 1433'tür.  

   -   **InstallDir &lt; *Configuration Manager yükleme yolu*>**  

        Gerekli değildir. Site yüklemesi için gereksinimlerde bulunan en düşük disk alanını doğrular.  

   -   **/SourceDir**  

        Gerekli değildir. İkincil sitenin bilgisayar hesabının, kurulum için kaynak dosyalarını barındıran klasöre erişebildiğini doğrular.  

   **Configuration Manager konsolu:**  

   -   **/Adminui**  

        Gereklidir. Yerel bilgisayarın Configuration Manager yükleme gereksinimlerini karşıladığını doğrular.  

3. Önkoşul Denetleyicisi Kullanıcı arabiriminde, önkoşul denetleyicisi, **Önkoşul sonucu** bölümünde bulunan sorunların bir listesini oluşturur.  

   -   Sorunu çözme hakkında ayrıntılı bilgi için listedeki bir öğeye tıklayın.  
   -   Site sunucusunu, site sistemini veya Configuration Manager konsolunu yüklemeden önce, listede **hata** durumunda olan tüm öğeleri çözmeniz gerekir.  
   -   Önkoşul denetleyicisi sonuçlarını gözden geçirmek için sistem sürücüsünün kökündeki **ConfigMgrPrereq. log** dosyasını da açabilirsiniz. Günlük dosyası, önkoşul denetleyicisi kullanıcı arabiriminde görüntülenmeyen ek bilgiler içerebilir.  
