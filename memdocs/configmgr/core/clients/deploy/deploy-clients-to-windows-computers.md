---
title: İstemcileri Windows 'a dağıtma
titleSuffix: Configuration Manager
description: Configuration Manager istemcisini Windows bilgisayarlarına dağıtmayı öğrenin.
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2eea75f39430f1cc38ff994280425ca918eaa432
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694568"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Configuration Manager 'da Windows bilgisayarlarına istemci dağıtma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager istemcisinin Windows bilgisayarlarına nasıl dağıtılacağı hakkında ayrıntılı bilgi verilmektedir. İstemci dağıtımı için planlama ve hazırlama hakkında daha fazla bilgi için şu makalelere bakın:

- [İstemci yükleme yöntemleri](plan/client-installation-methods.md)  
- [Windows bilgisayarlara istemci dağıtmak için önkoşullar](prerequisites-for-deploying-clients-to-windows-computers.md)
- [Configuration Manager istemcileri için güvenlik ve Gizlilik](plan/security-and-privacy-for-clients.md)  
- [İstemci dağıtımı için en iyi yöntemler](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a> Client push yüklemesi

İstemci gönderimi kullanmanın üç ana yolu vardır:  

- Bir site için istemci gönderme yüklemesini yapılandırdığınızda, istemci yükleme, sitenin bulduğu bilgisayarlarda otomatik olarak çalışır. Bu sınırlar bir sınır grubu olarak yapılandırıldığında, bu yöntem sitenin yapılandırılan sınırlarına göre kapsamlandırılır.  

- Bir koleksiyon içindeki belirli bir koleksiyon veya kaynak için Istemci anında Yükleme Sihirbazı 'nı çalıştırarak istemci gönderme yüklemesini başlatın.  

- Sonucu [sorgulamak](../../servers/manage/introduction-to-queries.md) için kullanabileceğiniz Configuration Manager istemcisini yüklemek Için Istemci anında Yükleme Sihirbazı 'nı kullanın. Yükleme, yalnızca sorgu tarafından döndürülen öğelerden biri **sistem kaynak** sınıfının **RESOURCEID** özniteliği ise başarılı olur.

Site sunucusu istemci bilgisayarla iletişim kuramıyor veya kurulum işlemini başlatamazsanız, her saat için yüklemeyi otomatik olarak yeniden dener. Sunucu yedi güne kadar yeniden denemeye devam eder.  

İstemci yükleme işleminin izlenmesine yardımcı olmak için, istemcileri yüklemeden önce bir geri dönüş durum noktası yükleyebilirsiniz. Bir geri dönüş durum noktası yüklediğinizde, istemci anında yükleme yöntemiyle yüklendiklerinde istemcilere otomatik olarak atanır. İstemci yükleme ilerlemesini izlemek için, istemci dağıtım ve atama raporlarını görüntüleyin.

İstemci günlük dosyaları, sorun giderme hakkında daha ayrıntılı bilgi sağlar. Günlük dosyaları geri dönüş durum noktası gerektirmez. Örneğin, site sunucusundaki CCM. log dosyası, site sunucusu bilgisayara bağlanırken oluşan tüm sorunları kaydeder. İstemcideki CCMSetup. log dosyası yükleme işlemini kaydeder.  

> [!IMPORTANT]  
> İstemci gönderimi yalnızca tüm önkoşullar karşılanıyorsa başarılı olur. Daha fazla bilgi için bkz. [yükleme yöntemi bağımlılıkları](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies).

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Siteyi, bulunan bilgisayarlar için otomatik olarak istemci gönderimi kullanacak şekilde yapılandırın

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Site genelinde otomatik client push yüklemesini yapılandırmak istediğiniz siteyi seçin.  

3. Şeridin **giriş** sekmesinde, **Ayarlar** grubunda, **istemci yükleme ayarları**' nı seçin ve ardından **Client Push yüklemesi**' ni seçin.  

4. Istemci anında yükleme Özellikler penceresi **genel** sekmesinde, **otomatik site genelinde client push yüklemesini etkinleştir**' i seçin.

5. Sürüm 1806 ' den başlayarak, siteyi güncelleştirdiğinizde istemci gönderimi için bir Kerberos denetimi etkinleştirilmiştir. **NTLM 'ye geri dönüş Için Izin verme** seçeneği varsayılan olarak etkindir ve bu, önceki davranışla tutarlıdır. Site, Kerberos kullanarak istemcinin kimliğini doğrulayamıyorum, NTLM kullanarak bağlantıyı yeniden dener. İyileştirilmiş güvenlik için önerilen yapılandırma, NTLM geri dönüşü olmadan Kerberos gerektiren bu ayarı devre dışı bırakmesidir.<!--1358204-->  

    > [!NOTE]  
    > Configuration Manager istemcisini yüklemek için Client Push kullandığında, site sunucusu istemciye uzak bir bağlantı oluşturur. Sürüm 1806 ' den başlayarak, site bağlantı kurulmadan önce NTLM 'ye geri dönüşe izin vermeyerek Kerberos karşılıklı kimlik doğrulaması gerektirebilir. Bu geliştirme, sunucu ve istemci arasındaki iletişimin güvenliğini sağlamaya yardımcı olur.  
    >
    > Güvenlik ilkelerinize bağlı olarak, ortamınız eski NTLM kimlik doğrulaması üzerinden Kerberos 'u zaten tercih edebilir veya zorunlu kılabilir. Bu kimlik doğrulama protokollerinin güvenlik konuları hakkında daha fazla bilgi için, [NTLM 'yi kısıtlamak üzere Windows güvenlik ilkesi ayarı](/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations)hakkında bilgi edinin.  
    >
    > Bu özelliği kullanmak için istemciler güvenilir bir Active Directory ormanında olmalıdır. Windows 'da Kerberos, karşılıklı kimlik doğrulaması için Active Directory kullanır.  

6. Configuration Manager istemci yazılımını göndermek zorunda olduğu sistem türlerini seçin. İstemcisini etki alanı denetleyicilerine yüklemek isteyip istemediğinizi seçin.  

7. **Hesaplar** sekmesinde, hedef bilgisayara bağlanırken kullanılacak Configuration Manager için bir veya daha fazla hesap belirtin. **Oluştur** simgesini seçin, **Kullanıcı adını** ve **parolayı** girin (38 karakterden fazla değil), parolayı onaylayın ve ardından **Tamam**' ı seçin. En az bir Client Push yükleme hesabı belirtin. Bu hesabın, istemciyi yüklemek için hedef bilgisayarda yerel yönetici haklarına sahip olması gerekir. İstemci anında yükleme hesabı belirtmezseniz, Configuration Manager site sistemi bilgisayar hesabını kullanmayı dener. Site sistem bilgisayar hesabı kullanılırken etki alanları arası istemci gönderimi başarısız olur.  

    > [!NOTE]  
    > Bir ikincil siteden Client Push kullanmak için, ikincil sitede istemci gönderimi Başlatan hesabı belirtin.  
    >
    > İstemci anında yükleme hesabı hakkında daha fazla bilgi için, sonraki yordama bakın, [Istemci anında Yükleme Sihirbazı 'Nı kullanın](#use-the-client-push-installation-wizard).  

8. **Yükleme özellikleri** sekmesinde gerekli yükleme özelliklerini belirtin.

    Configuration Manager için Active Directory şemasını genişlettiyseniz, site belirtilen [istemci yükleme özelliklerini](about-client-installation-properties.md) Active Directory Domain Services yayınlar. CCMSetup, yükleme özellikleri olmadan çalıştırıldığında, bu özellikleri Active Directory okur.  

    > [!NOTE]  
    > İstemci gönderme yüklemesini ikincil bir sitede etkinleştirirseniz **Smssitekodu** özelliğini üst birincil sitesinin Configuration Manager site kodu olarak ayarlayın. Configuration Manager için Active Directory şemasını genişlettiyseniz, doğru site atamasını otomatik olarak bulmak için bu özelliği **Otomatik**olarak ayarlayın.

### <a name="use-the-client-push-installation-wizard"></a>Client Push Yükleme Sihirbazı 'nı kullanma

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Site genelinde otomatik client push yüklemesini yapılandırmak istediğiniz siteyi seçin.  

3. Şeridin **giriş** sekmesinde, **Ayarlar** grubunda, **istemci yükleme ayarları**' nı seçin ve ardından **Client Push yüklemesi**' ni seçin.  

4. **Yükleme özellikleri** sekmesinde gerekli yükleme özelliklerini belirtin.  

    Configuration Manager için Active Directory şemasını genişlettiyseniz, site belirtilen [istemci yükleme özelliklerini](about-client-installation-properties.md) Active Directory Domain Services yayınlar. CCMSetup, yükleme özellikleri olmadan çalıştırıldığında, bu özellikleri Active Directory okur.

5. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin.  

6. **Cihazlar** düğümünde bir veya daha fazla bilgisayar seçin. Veya **Cihaz Koleksiyonları** düğümünde bir bilgisayar koleksiyonu seçin.  

7. Şeridin **giriş** sekmesinde, şu seçeneklerden birini seçin:  

    - İstemciyi bir veya daha fazla cihaza göndermek için, **cihaz** grubunda, **istemci yükleme**' yi seçin.  

    - İstemciyi bir cihaz koleksiyonuna göndermek için, **koleksiyon** grubunda **istemci yükleme**' yi seçin.  

8. Configuration Manager Istemci yüklemesi Sihirbazı ' nın **başlamadan önce** sayfasında, bilgileri gözden geçirin ve ardından **İleri**' yi seçin.  

9. **Yükleme seçenekleri** sayfasında uygun seçenekleri belirleyin.  

10. Yükleme ayarlarını gözden geçirin ve Sihirbazı doldurun.  

> [!NOTE]  
> Site istemci gönderimi için yapılandırılmamış olsa bile istemcileri yüklemek için bu sihirbazı kullanın.  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> Yazılım güncelleştirmesi tabanlı yükleme  

Yazılım güncelleştirme tabanlı istemci yüklemesi, istemciyi yazılım güncelleştirmesi olarak bir yazılım güncelleştirme noktasına yayımlar. İlk kez yükleme veya yükseltme için bu yöntemi kullanın.  

Configuration Manager istemcisi bir bilgisayarda yüklüyse, bilgisayar siteden istemci ilkesi alır. Bu ilke, yazılım güncelleştirmelerinin alınacağı yazılım güncelleştirme noktası sunucu adını ve bağlantı noktasını içerir.

> [!IMPORTANT]  
> Yazılım güncelleştirme tabanlı yükleme için, istemci yüklemesi ve yazılım güncelleştirmeleri için aynı Windows Server Update Services (WSUS) sunucusunu kullanın. Bu sunucunun, bir birincil sitedeki etkin yazılım günceleştirme noktası olması gerekir. Daha fazla bilgi için bkz. [yazılım güncelleştirme noktası yüklemesi](../../../sum/get-started/install-a-software-update-point.md).

Configuration Manager istemcisi bir bilgisayarda yüklü değilse, grup ilkesi nesnesini yapılandırın ve atayın. Grup ilkesi, yazılım güncelleştirme noktasının sunucu adını belirtir.  

Yazılım güncelleştirme tabanlı bir istemci yüklemesine komut satırı özellikleri ekleyemezsiniz. Configuration Manager için Active Directory şemasını genişlettiyseniz, istemci yükleme, yükleme özellikleri için Active Directory Domain Services otomatik olarak sorgular.  

Active Directory şemasını genişletmemiş değilseniz, istemci yükleme ayarlarını sağlamak için grup ilkesi kullanın. Bu ayarlar, herhangi bir yazılım güncelleştirmesi tabanlı istemci yüklemesine otomatik olarak uygulanır. Daha fazla bilgi için [istemci yükleme özelliklerini sağlama konusundaki](#BKMK_Provision) bölümüne ve [istemcileri bir siteye atamaya](assign-clients-to-a-site.md)yönelik makaleye bakın.  

Configuration Manager istemcisi olmayan bilgisayarları yazılım güncelleştirme noktasını kullanacak şekilde yapılandırmak için aşağıdaki yordamları kullanın. Ayrıca, istemci yazılımını yazılım güncelleştirme noktasına yayımlamak için bir yordam de vardır.  

> [!TIP]  
> Bilgisayarlar önceki bir yazılım yüklemesinin ardından bekleyen bir yeniden başlatma durumundaysa, yazılım güncelleştirmesi tabanlı bir istemci yüklemesi bilgisayarın yeniden başlatılmasına neden olabilir.  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Yazılım güncelleştirme noktasını belirtmek için bir grup ilkesi nesnesi yapılandırma  

1. Yeni veya var olan bir grup ilkesi nesnesini açmak için **Grup İlkesi Yönetim Konsolu** kullanın.  

2. **Bilgisayar yapılandırması**, **Yönetim Şablonları**ve **Windows bileşenleri**' ni genişletin ve **Windows Update**' ı seçin.  

3. **Intranet Microsoft güncelleştirme hizmeti konumunu belirtin**ayarının özelliklerini açın ve ardından **etkin**' i seçin.  

4. **Güncelleştirmeleri algılamak için intranet güncelleştirme hizmetini ayarlama**: yazılım güncelleştirme noktası sunucusunun adını ve bağlantı noktasını belirtin.  

    - Configuration Manager site sistemini bir tam etki alanı adı (FQDN) kullanmak üzere yapılandırdıysanız, bu biçimi kullanın.  

    - Configuration Manager site sistemi FQDN kullanmak üzere yapılandırılmamışsa, kısa bir ad biçimi kullanın.

    > [!TIP]  
    > Bağlantı noktası numarasını öğrenmek için bkz. [WSUS tarafından kullanılan bağlantı noktası ayarlarını belirleme](../../../sum/plan-design/plan-for-software-updates.md).

    FQDN biçimindeki örnek: `http://server1.contoso.com:8530`  

5. **İntranet istatistikleri sunucusunu ayarlama**: Bu ayar genellikle aynı sunucu adıyla yapılandırılır.

6. Grup ilkesi nesnesini, istemcisini yüklemek ve yazılım güncelleştirmeleri almak istediğiniz bilgisayarlara atayın.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Configuration Manager istemcisini yazılım güncelleştirme noktasına yayımlama  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Yazılım güncelleştirmesi tabanlı istemci yüklemesini yapılandırmak istediğiniz siteyi seçin.  

3. Şeridin **giriş** sekmesinde, **Ayarlar** grubunda, **istemci yükleme ayarları**' nı seçin ve ardından **yazılım güncelleştirmesi tabanlı istemci yüklemesi**' ni seçin.  

4. **Yazılım güncelleştirmesi tabanlı istemci yüklemesini etkinleştir**' i seçin.  

5. Sitenin istemci sürümü, yazılım güncelleştirme noktasındaki sürümden daha yeni ise, **Istemci paketi algılanan sonraki sürümü** iletişim kutusu açılır. En son sürümü yayımlamak için **Evet** ' i seçin.  

    > [!NOTE]  
    > İstemci yazılımını henüz yazılım güncelleştirme noktasına yayımlamadıysanız, bu iletişim kutusu boştur.

Configuration Manager istemcisi için yazılım güncelleştirmesi, yeni bir sürüm olduğunda otomatik olarak güncellenmez. Siteyi güncelleştirdiğinizde, istemciyi güncelleştirmek için bu yordamı tekrarlayın.  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a> grup ilkesi yükleme

Configuration Manager istemcisini yayınlamak veya atamak için Active Directory Domain Services grup ilkesi kullanın. İstemci, bilgisayar başladığında yüklenir. Grup ilkesi kullandığınızda, istemci Denetim Masası 'ndaki **Program Ekle veya Kaldır** ' da görünür. Kullanıcı onu oradan yükleyebilir.  

Grup ilkesi tabanlı yüklemeler için CCMSetup.msi Windows Installer paketini kullanın. Bu dosya, `<ConfigMgr installation directory>\bin\i386` site sunucusundaki klasöründe bulunur. Yükleme davranışını değiştirmek için bu dosyaya özellikler ekleyemezsiniz.  

> [!IMPORTANT]  
> İstemci yükleme dosyalarına erişmek için yönetici izinlerinizin olması gerekir.  

- Configuration Manager için Active Directory şemasını genişlettiyseniz ve **site özellikleri** Iletişim kutusunun **Yayımlama** sekmesinde etki alanını seçtiyseniz, istemci bilgisayarlar yükleme özellikleri için otomatik olarak Active Directory Domain Services arar. Daha fazla bilgi için bkz. [Active Directory Domain Services yayımlanan istemci yükleme özellikleri hakkında](about-client-installation-properties-published-to-active-directory-domain-services.md).  

- Active Directory şemasını genişletmemiş olmanız durumunda, yükleme özelliklerini bilgisayarların Windows kayıt defterine depolama hakkında bilgi için [istemci yükleme özelliklerini sağlama](#BKMK_Provision) konusunun bölümüne bakın. İstemci, yüklediğinde bu yükleme özelliklerini kullanır.  

Daha fazla bilgi için bkz. [Grup İlkesi kullanarak yazılımı uzaktan yüklemek için](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a> El ile yükleme

CCMSetup.exe kullanarak istemci yazılımını bilgisayarlara el ile yükleyebilirsiniz. Bu programı ve destekleyici dosyalarını site sunucusundaki Configuration Manager yükleme klasöründe bulunan Istemci klasöründe bulabilirsiniz. Site bu klasörü ağda paylaşır:  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>` birincil site sunucusu adıdır. `<site code>` , istemcinin atandığı birincil site kodudur. İstemci üzerindeki komut satırından CCMSetup.exe çalıştırmak için, bu ağ konumuna bağlanın ve ardından komutunu çalıştırın.  

> [!IMPORTANT]  
> İstemci yükleme dosyalarına erişmek için yönetici izinlerinizin olması gerekir.  

CCMSetup.exe, tüm gerekli önkoşulları istemci bilgisayara kopyalar ve istemciyi yüklemek için Windows Installer paketini (Client.msi) çağırır. Client.msi doğrudan çalıştıramazsınız.  

İstemci yüklemesinin davranışını değiştirmek için hem CCMSetup.exe hem de Client.msi için komut satırı seçeneklerini belirtin. Client.msi özellikleri belirttıklamadan önce ile başlayan CCMSetup parametrelerini belirttiğinizden emin olun `/` . Örnek:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

Bu örnekte istemci aşağıdaki seçeneklerle yüklenir:  

|Seçenek|Açıklama|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Bu CCMSetup parametresi, gerekli istemci yükleme dosyalarını indirmek için SMSMP01 yönetim noktasını belirtir.|  
|`/logon`|Bu CCMSetup parametresi, bilgisayarda var olan bir Configuration Manager istemcisi bulunursa yüklemenin durması gerektiğini belirtir.|  
|`SMSSITECODE=AUTO`|Bu Client.msi özelliği, istemcisinin Active Directory Domain Services kullanarak kullanmak üzere Configuration Manager site kodunu bulmaya çalışacağını belirtir.|  
|`FSP=SMSFP01`|Bu Client.msi özelliği, istemci bilgisayardan gönderilen durum iletilerini almak için SMSFP01 adlı geri dönüş durum noktasının kullanıldığını belirtir.|  

Daha fazla bilgi için bkz. [istemci yükleme parametreleri ve özellikleri hakkında](about-client-installation-properties.md).  

> [!TIP]  
> Configuration Manager istemcisini Azure Active Directory (Azure AD) kimliğini kullanarak modern bir Windows 10 cihazına yüklemek için, bkz. [kimlik doğrulaması Için Azure ad kullanarak Configuration Manager Windows 10 Istemcileri yüklemek ve atamak](deploy-clients-cmg-azure.md). Bu yordam, bir intranet veya internet üzerindeki istemciler içindir.  

### <a name="manual-installation-examples"></a>El ile yükleme örnekleri

Bu örnekler, intranette Active Directory katılmış istemciler içindir. Bunlar aşağıdaki değerleri kullanır:  

- **Mpserver**: yönetim noktasını barındıran sunucu
- **FSPSERVER**: geri dönüş durum noktasını barındıran sunucu  
- **ABC**: site kodu  
- **contoso.com**: etki alanı adı  

Tüm site sistemi sunucularını bir intranet FQDN 'siyle yapılandırdığınızı ve site bilgilerini Active Directory yayımladığınızı varsayalım.  

İstemci bilgisayarda aşağıdaki adımlarla başlayın:  

1. Yerel yönetici olarak oturum açın.  
2. Z sürücüsünü ile eşleyin `\\MPSERVER\SMS_ABC\Client` .  
3. Komut istemi 'ni Z sürücüsüne geçirin.  

Ardından aşağıdaki komutlardan birini çalıştırın:  

#### <a name="manual-example-1"></a>El ile örnek 1  

`CCMSetup.exe`  

Bu komut, istemciyi ek parametre veya özellik olmadan yüklenir. İstemci, Active Directory Domain Services yayımlanan istemci yükleme özellikleriyle otomatik olarak yapılandırılır, bu ayarlar dahil:  

- Site Kodu: Bu ayar, istemcinin ağ konumunun, istemci ataması için yapılandırdığınız bir sınır grubuna dahil edilmesini gerektirir.  
- Yönetim noktası.
- Geri dönüş durum noktası.
- Yalnızca HTTPS kullanarak iletişim kurun.  

Daha fazla bilgi için bkz. [Active Directory Domain Services yayımlanan istemci yükleme özellikleri hakkında](about-client-installation-properties-published-to-active-directory-domain-services.md).  

#### <a name="manual-example-2"></a>El ile örnek 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Bu komut Active Directory Domain Services tarafından sağlanan otomatik yapılandırmayı geçersiz kılar. İstemcinin ağ konumunu, istemci ataması için yapılandırılmış bir sınır grubuna eklemeniz gerekmez. Bunun yerine, yükleme bu ayarları belirtir:

- Site kodu
- Intranet yönetim noktası
- Internet tabanlı yönetim noktası
- Internet 'ten gelen bağlantıları kabul eden geri dönüş durumu noktası
- En uzun geçerlilik süresine sahip bir istemci ortak anahtar altyapısı (PKI) sertifikası (varsa) kullanın

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a> Oturum açma betiği yüklemesi

Configuration Manager, Configuration Manager istemci yazılımını yüklemek için oturum açma komut dosyalarının kullanılmasını destekler. İstemci yüklemesini tetiklemek için bir oturum açma komut dosyasında CCMSetup.exe program dosyasını kullanın.  

Oturum açma komut dosyası yüklemesi, el ile istemci yüklemeyle aynı yöntemleri kullanır. `/logon`CCMSsetup.exe için yükleme parametresini belirtin. İstemcinin herhangi bir sürümü bilgisayarda zaten varsa, bu parametre istemcinin yüklenmesini engeller. Bu davranış, oturum açma komut dosyası her çalıştığında istemcinin yeniden yüklenmesini önler.  

Parametresini kullanarak bir yükleme kaynağı belirtmezseniz `/Source` ve parametresi tarafından yüklemenin alınacağı hiçbir yönetim noktası belirtilmemişse `/MP` , CCMSetup.exe yönetim noktasını Active Directory Domain Services arayarak konumlandırır. Bu davranış yalnızca Configuration Manager şemasını genişlettiyseniz ve siteyi Active Directory Domain Services yayımladıysanız oluşur. Alternatif olarak, istemci, yönetim noktasını bulmak için DNS veya WINS kullanabilir.  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a> Paket ve program yükleme

Seçili cihazlar için istemci yazılımını yükselten bir paket ve program oluşturmak ve dağıtmak için Configuration Manager kullanın. Configuration Manager, paket özelliklerini genellikle kullanılan değerlerle dolduran bir paket tanımı dosyası sağlar. Ek komut satırı parametreleri ve özellikleri belirterek istemci yüklemesinin davranışını özelleştirin.  

> [!NOTE]  
> Configuration Manager 2007 istemcilerini bu yöntemi kullanarak yükseltemezsiniz. Bunun yerine istemcinin en son sürümünü içeren bir paketi otomatik olarak oluşturup dağıtan otomatik istemci yükseltme kullanın. Daha fazla bilgi için bkz. [Istemcileri yükseltme](../manage/upgrade/upgrade-clients.md).  
>
> Configuration Manager istemcisinin eski sürümlerinden geçiş hakkında daha fazla bilgi için bkz. [istemci geçiş stratejisi planlama](../../migration/planning-a-client-migration-strategy.md).  

### <a name="create-a-package-and-program-for-the-client-software"></a>İstemci yazılımı için bir paket ve program oluşturma  

İstemci yazılımını yükseltmek için Configuration Manager istemci bilgisayarlara dağıtabileceğiniz bir Configuration Manager paketi ve program oluşturmak için aşağıdaki yordamı kullanın.  

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **paketler** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **Tanımdan Paket Oluştur**' u seçin.  

3. Sihirbazın **paket tanımı** sayfasında, **Yayımcı** listesinden **Microsoft** ' u seçin ve **paket tanımı** listesinden **istemci yükseltme Configuration Manager** ' yi seçin.  

4. **Kaynak dosyaları** sayfasında **her zaman bir kaynak klasörden dosyaları al**' ı seçin.  

5. **Kaynak klasör** sayfasında, **ağ yolu (UNC adı)** öğesini seçin. Ardından, istemci yükleme dosyalarını içeren sunucunun ve paylaşımın ağ yolunu girin.  

    > [!NOTE]  
    > Configuration Manager dağıtımının çalıştırıldığı bilgisayarın, belirtilen ağ klasörüne erişimi olmalıdır. Aksi halde, istemci yüklemesi başarısız olur.  

    İstemci yükleme özelliklerinden herhangi birini değiştirmek için, **Configuration Manager Aracısı sessiz yükseltme özellikleri** program Iletişim kutusunun **genel** sekmesindeki CCMSetup.exe komut satırını değiştirin. Varsayılan yükleme özellikleri şunlardır `/noservice SMSSITECODE=AUTO` .  

6. Paketi, istemci yükseltme paketini barındırmak istediğiniz dağıtım noktalarının tümüne dağıtın. Ardından paketi, yükseltmek istediğiniz istemcileri içeren cihaz koleksiyonlarına dağıtın.  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a> Intune MDM ile yönetilen Windows cihazları

Configuration Manager istemcisini Microsoft Intune kayıtlı cihazlara dağıtın.

Bu yordam, bir intranete bağlı geleneksel bir istemci içindir. Geleneksel istemci kimlik doğrulama yöntemlerini kullanır. Cihazın istemciyi yükledikten sonra yönetilen bir durumda kaldığından emin olmak için, intranette ve Configuration Manager bir site sınırının içinde olması gerekir.  

Configuration Manager istemcisini Azure AD kimlik kullanarak modern bir Windows 10 cihazına yüklemek için, bkz. [kimlik doğrulaması Için Azure ad kullanarak Configuration Manager Windows 10 Istemcileri yüklemek ve atamak](deploy-clients-cmg-azure.md).

Configuration Manager istemcisini yükledikten sonra, cihazların Intune kaydını kaldırmayın. Configuration Manager istemci ve MDM kaydını aynı anda kullanabilirler. Daha fazla bilgi için bkz. [ortak yönetime genel bakış](../../../comanage/overview.md).  

> [!Note]
> Intune tarafından yönetilen bir cihaza Configuration Manager istemcisini yüklemek için diğer istemci yükleme yöntemlerini kullanabilirsiniz. Örneğin, Intune tarafından yönetilen bir cihaz intranette ve Active Directory etki alanına katılırsa, Configuration Manager istemcisini yüklemek için Grup İlkesi 'ni kullanabilirsiniz.<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>Intune kullanarak Configuration Manager istemcisini yüklemesi

1. Intune 'da, Configuration Manager istemci yükleme dosyasını içeren [bir Windows iş kolu uygulaması ekleyin](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows) **CCMSetup.msi**. Bu dosyayı `\bin\i386` site sunucusundaki Configuration Manager yükleme dizini klasöründe bulabilirsiniz.  

2. Intune Yazılım Yayımcısı, komut satırı parametrelerini girin. Örneğin, bu komutu intranette geleneksel bir istemciyle birlikte kullanın:  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > Azure AD kimlik doğrulaması kullanılarak modern bir Windows 10 istemcisiyle birlikte kullanılacak bir komut örneği için bkz. [İnternet tabanlı cihazları ortak yönetim için hazırlama](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).  

3. [Uygulamayı](../../../../intune/apps/apps-deploy.md) kayıtlı Windows bilgisayarları grubuna atayın.  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a> İşletim sistemi görüntüsü yükleme

Configuration Manager istemcisini, işletim sistemi görüntüsü oluşturmak için kullandığınız başvuru bilgisayarına önceden yükleyin.

> [!IMPORTANT]  
> Bir işletim sistemi görüntüsünü dağıtmak için Configuration Manager görev dizisini kullandığınızda, [ConfigMgr Istemcisini hazırla](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture) adımı, Configuration Manager istemcisini tamamen kaldırır.  

### <a name="prepare-the-client-computer-for-imaging"></a>İstemci bilgisayarı görüntü oluşturmaya hazırlama  

1. Configuration Manager istemci yazılımını referans bilgisayara el ile yükleyebilirsiniz. Daha fazla bilgi için bkz. [Configuration Manager istemcilerini El Ile nasıl yüklenir](#BKMK_Manual).  

    > [!IMPORTANT]  
    > CCMSetup.exe komut satırı özelliklerinde istemci için Configuration Manager bir site kodu belirtmeyin.  

2. Bir komut isteminde, `net stop ccmexec` başvuru BILGISAYARıNDA SMS aracı ana bilgisayar hizmeti 'ni (CcmExec.exe) durdurmak için yazın.  

3. SMSCFG.INI dosyasını referans bilgisayardaki Windows klasöründen silin.  

4. Referans bilgisayardaki yerel bilgisayar deposunda depolanan tüm sertifikaları kaldırın. Örneğin, PKI sertifikaları kullanıyorsanız, bilgisayarı görüntüetmeden önce **bilgisayar** ve **Kullanıcı**için **Kişisel** deposundaki sertifikaları kaldırın.  

5. İstemciler, başvuru bilgisayarının hiyerarşisinden farklı bir Configuration Manager hiyerarşisine yüklenirse, güvenilen kök anahtarı başvuru bilgisayarından kaldırın.  

    > [!NOTE]  
    > İstemciler bir yönetim noktasını bulmak için Active Directory Domain Services sorgulayamaz, güvenilen yönetim noktalarını belirlemek için güvenilen kök anahtarı kullanırlar. Tüm görüntü, istemcileri ana bilgisayarla aynı hiyerarşide dağıtırsanız, güvenilen kök anahtarı yerinde bırakın.
    >
    > İstemcileri farklı hiyerarşilerde dağıtırsanız, güvenilen kök anahtarı kaldırın. Ayrıca, bu istemcilere yeni güvenilen kök anahtarı sağlayın. Daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

6. Referans bilgisayarın bir görüntüsünü yakalamak için görüntüleme yazılımınızı kullanın.  

7. Görüntüyü hedef bilgisayarlara dağıtın.  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Çalışma grubu bilgisayarları

Configuration Manager, çalışma gruplarındaki bilgisayarlar için istemci yüklemeyi destekler. İstemcisini [Configuration Manager istemcilerini el ile yüklemek için](#BKMK_Manual)belirtilen yöntemi kullanarak, istemciyi çalışma grubu bilgisayarlarına yükleyebilirsiniz.  

### <a name="prerequisites"></a>Ön koşullar  

- İstemcisini her çalışma grubu bilgisayarına el ile yükleyebilirsiniz. Yükleme sırasında etkileşimli kullanıcı yerel yönetici haklarına sahip olmalıdır.  

- Configuration Manager site sunucusu etki alanındaki kaynaklara erişmek için, site için ağ erişim hesabını yapılandırın. Bu hesabı yazılım dağıtımı site bileşeninde belirtin. Daha fazla bilgi için bkz. [site bileşenleri](../../servers/deploy/configure/site-components.md).  

### <a name="limitations"></a>Sınırlamalar  

- Çalışma grubu istemcileri Active Directory Domain Services yönetim noktalarını bulamaz. Bunun yerine, DNS, WINS veya başka bir yönetim noktası kullanırlar.  

- Küresel dolaşım desteklenmez. Çalışma grubu istemcileri site bilgilerini Active Directory Domain Services sorgulayamaz.  

- Active Directory bulma yöntemleri, çalışma gruplarındaki bilgisayarları bulamaz.  

- Çalışma grubu bilgisayarlarının kullanıcılarına yazılım dağıtamazsınız.  

- İstemciyi çalışma grubu bilgisayarlarına yüklemek için istemci gönderme yükleme yöntemini kullanamazsınız.  

- Çalışma grubu istemcileri kimlik doğrulaması için Kerberos 'u kullanamaz ve el ile onay gerektirebilir.  

- Bir çalışma grubu istemcisini dağıtım noktası olarak yapılandıramazsınız. Configuration Manager, dağıtım noktası bilgisayarlarının bir etki alanına üye olmasını gerektirir.  

### <a name="install-the-client-on-workgroup-computers"></a>İstemciyi çalışma grubu bilgisayarlarına yükler  

Önkoşulları denetleyin ve sonra [Configuration Manager istemcilerini el ile yüklemek için](#BKMK_Manual)bölümündeki yönergeleri izleyin.  

#### <a name="workgroup-example-1"></a>Çalışma grubu örneği 1

Bu örnek aşağıdaki eylemleri yapar:

- İntranet istemci yönetimine yönelik istemciyi yükleme
- Site kodunu belirtir
- Bir yönetim noktasını bulmak için DNS sonekini belirtir  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>Çalışma grubu örneği 2

Bu örnek, istemcinin sınır grubunda yapılandırılmış bir ağ konumunda olmasını gerektirir. Bu gereksinim karşılanmazsa, otomatik site ataması çalışmaz. Komutu, Server FSPSERVER üzerinde bir geri dönüş durum noktası içerir. Bu özellik, istemci dağıtımını izlemeye ve tüm istemci iletişim sorunlarını belirlemenize yardımcı olur.

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> Internet tabanlı istemci yönetimi  

> [!NOTE]  
> Bu bölüm, [bulut yönetimi ağ geçidi](../manage/cmg/plan-cloud-management-gateway.md)kullanan istemciler için geçerlidir. Internet tabanlı istemcileri bir bulut yönetimi ağ geçidi kullanarak yüklemek için bkz. [Azure AD 'yi kullanarak kimlik doğrulaması için Configuration Manager Windows 10 Istemcileri yüklemek ve atamak](deploy-clients-cmg-azure.md).  

Configuration Manager sitesi bazen intranette ve bazen de internet 'te olan istemciler için [İnternet tabanlı istemci yönetimini](../manage/plan-internet-based-client-management.md) desteklediğinde, istemcileri intranete yüklerken iki seçeneğiniz vardır:  

- İstemcisini yüklerken Client.msi özelliğini `CCMHOSTNAME=<internet FQDN of the internet-based management point>` , el ile yükleme veya Client Push kullanarak ekleyin. Bu yöntemi kullandığınızda, istemcisini doğrudan siteye atayın. Otomatik site atamasını kullanamazsınız. Bu yapılandırma yönteminin bir örneğini sağlayan [el ile Configuration Manager Istemcileri nasıl yüklenir](#BKMK_Manual) bölümüne bakın.  

- İntranet istemci yönetimine yönelik istemciyi yükler ve ardından istemciye Internet tabanlı bir istemci yönetim noktası atayın. Denetim Masası 'ndaki **Configuration Manager** sayfasındaki istemci özelliklerini kullanarak veya bir komut dosyası kullanarak yönetim noktasını değiştirin. Bu yöntemi kullanırken otomatik istemci atamasını kullanabilirsiniz. Daha fazla bilgi için [istemci yüklemesinden sonra istemcileri internet tabanlı istemci yönetimi için yapılandırma](#BKMK_ConfigureIBCM_MP) bölümüne bakın.  

İnternet üzerindeki istemcileri yüklemek için aşağıdaki desteklenen yöntemlerden birini seçin:  

- Bu istemcilerin intranete bir VPN ile geçici olarak bağlanması için bir mekanizma sağlar. Ardından, uygun istemci yükleme yöntemini kullanarak istemcisini yükleme.  

- Configuration Manager bağımsız bir yükleme yöntemi kullanın. Örneğin, istemci yükleme kaynak dosyalarını çıkarılabilir medyaya paketleyin ve medyayı kullanıcılara gönderin. İstemci yükleme kaynak dosyaları `<installation path>\Client` Configuration Manager site sunucusundaki klasöründe bulunur. Medyada, istemci klasörü üzerine el ile kopyalamak için bir komut dosyası ekleyin. Bu klasörden CCMSetup.exe ve tüm uygun CCMSetup komut satırı özelliklerini kullanarak istemciyi kurun.  

> [!NOTE]  
> Configuration Manager, bir istemciyi doğrudan Internet tabanlı yönetim noktasından veya internet tabanlı yazılım güncelleştirme noktasından yüklemeyi desteklemez.

İnternet üzerinden yönetilen istemcilerin internet tabanlı site sistemleriyle iletişim kurması gerekir. İstemciyi yüklemeden önce bu istemcilerin ortak anahtar altyapısı (PKI) sertifikalarına da sahip olduğundan emin olun. Bu sertifikaları Configuration Manager bağımsız olarak yükler. Daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>CCMSetup komut satırı özelliklerini belirterek internet 'e istemci yükleme  

1. [Configuration Manager istemcilerini el ile yüklemek için](#BKMK_Manual)bölümündeki yönergeleri izleyin. Her zaman aşağıdaki seçenekleri ekleyin:  

    - CCMSetup komut satırı parametresi `/source:<local path of the copied Client folder>`  

    - CCMSetup komut satırı parametresi `/UsePKICert`  

    - Client.msi özelliği `CCMHOSTNAME=<FQDN of internet-based management point>`  

    - Client.msi özelliği `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - Client.msi özelliği `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > Sitede birden fazla internet tabanlı yönetim noktası varsa, bu özellik için ne belirttiğinize bağımsız değildir `CCMHOSTNAME` . Configuration Manager istemcisi belirtilen internet tabanlı yönetim noktasına bağlandığı zaman, istemciye sitedeki kullanılabilir internet tabanlı yönetim noktalarının listesini gönderir. İstemci listeden rastgele bir tane seçer.

2. İstemcinin sertifika iptal listesini (CRL) denetlemesini istemiyorsanız CCMSetup komut satırı parametresini belirtin `/NoCRLCheck` .  

3. Internet tabanlı bir geri dönüş durum noktası kullanıyorsanız, Client.msi özelliğini belirtin `FSP=<internet FQDN of the internet-based fallback status point>` .  

4. İstemcisini yalnızca İnternet istemci yönetimi için yüklüyorsanız Client.msi özelliğini belirtin `CCMALWAYSINF=1` .  

5. Ek CCMSetup komut satırı parametreleri belirtmeniz gerekip gerekmediğini belirleyin. Örneğin, istemcinin birden fazla geçerli PKI sertifikası varsa, bir sertifika seçim ölçütü belirtmeniz gerekebilir. Kullanılabilir özelliklerin bir listesi için bkz. [istemci yükleme parametreleri ve özellikleri hakkında](about-client-installation-properties.md).  

#### <a name="internet-based-example"></a>Internet tabanlı örnek

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

Bu örnek, istemcisini aşağıdaki davranışlarla birlikte yüklenir:

- D sürücüsündeki bir klasörden kaynak dosyalarını kullanın.
- İstemci PKI sertifikası kullanın.
- En uzun geçerlilik süresine sahip sertifikayı seçin.
- Yalnızca Internet istemci yönetimi.
- İstemciyi, Sunucu1 adlı internet tabanlı yönetim noktasını kullanmak üzere atayın.
- Contoso.com etki alanına Internet tabanlı geri dönüş durum noktasını atayın.
- İstemciyi ABC sitesine atayın.  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> İstemci yüklemesinden sonra istemcileri internet tabanlı istemci yönetimine göre yapılandırmak için  

İstemcisini yükledikten sonra Internet tabanlı yönetim noktasını atamak için aşağıdaki yordamlardan birini kullanın. İlki el ile yapılandırma gerektirir ve birkaç istemciye uygundur. İkincisi birçok istemciyi yapılandırmak için daha uygundur.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Configuration Manager denetim masasından istemci yüklemesinden sonra istemcileri internet tabanlı istemci yönetimi için yapılandırma  

1. İstemcide **Configuration Manager** denetim masasını açın.  

2. **Internet sekmesinde Internet** tabanlı yönetim noktasının tam etki alanı adını (FQDN) **Internet FQDN 'si**olarak girin.  

    > [!NOTE]  
    > **Internet** sekmesi yalnızca istemcinin BIR istemci PKI sertifikası olduğunda kullanılabilir.  

3. İstemci, bir proxy sunucusu kullanarak İnternet 'e eriştiğinde, proxy sunucu ayarlarını girin.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Bir komut dosyası kullanarak istemci yüklemesinden sonra istemcileri internet tabanlı istemci yönetimi için yapılandırma  

##### <a name="powershell"></a>PowerShell

1. PowerShell ıSE veya Visual Studio Code gibi bir PowerShell satır içi düzenleyiciyi açın. Not Defteri gibi bir metin Düzenleyicisi de kullanabilirsiniz.

2. Aşağıdaki kod satırlarını kopyalayıp düzenleyiciye ekleyin. `'mp.contoso.com'`Internet tabanlı yönetim noktanağınızın Internet FQDN 'siyle değiştirin.

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > Son satır yalnızca yeni internet yönetim noktası değerini doğrulamak için geçerlidir.
    >
    > Belirtilen bir internet tabanlı yönetim noktasını silmek için, tırnak işaretlerinin içindeki sunucu FQDN değerini kaldırın. Satır olur `$newInternetBasedManagementPointFQDN = ''` .

3. Dosyayı bir. ps1 uzantısıyla kaydedin.  

4. Betiği istemci bilgisayarlarda yükseltilmiş haklarla çalıştırın. Aşağıdaki yöntemlerden birini kullanın:  

    - Bir paket ve program kullanarak dosyayı mevcut Configuration Manager istemcilerine dağıtın.  

    - Dosya Gezgini 'nde betik dosyasına çift tıklayarak dosyayı mevcut Configuration Manager istemcilerinde yerel olarak çalıştırın.  

Değişikliklerin etkili olması için istemciyi yeniden başlatmanız gerekebilir.  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a> İstemci yükleme özelliklerini sağlama

Grup İlkesi ve yazılım güncelleştirmesi tabanlı istemci yüklemeleri için istemci yükleme özelliklerini sağlayın. Configuration Manager istemci yükleme özelliklerine sahip bilgisayarları sağlamak için Windows grup ilkesi kullanın. Bu özellikler bilgisayarın kayıt defterinde saklanır. İstemci, yüklediğinde onları okur. Bu yordam normalde gerekli değildir, ancak aşağıdaki gibi bazı istemci yükleme senaryoları için gerekli olabilir:  

- Grup İlkesi ayarlarını veya yazılım güncelleştirme tabanlı istemci yükleme yöntemlerini kullanıyorsunuz. Configuration Manager için Active Directory şemasını genişletmemiş olabilirsiniz.  

- Belirli bilgisayarlardaki istemci yükleme özelliklerini geçersiz kılmak istiyorsunuz.  

> [!NOTE]  
> CCMSetup.exe komut satırında herhangi bir yükleme özelliği sağlanmışsa, bilgisayarlarda sağlanan yükleme özellikleri kullanılmaz.

Configuration Manager yükleme medyasında adlı bir grup ilkesi yönetim şablonu `ConfigMgrInstallation.adm` sağlanır. İstemci bilgisayarlarını yükleme özellikleriyle sağlamak için bu şablonu kullanın.

> [!TIP]
> Varsayılan olarak `ConfigMgrInstallation.adm` 255 karakterden daha büyük dizeleri desteklemez. Bu yapılandırma, CCMCERTıSERS gibi uzun değerlerle birden fazla parametre veya parametre eklenmesini etkileyebilir.<!-- SCCMDocs#1648 -->
>
> Bu soruna geçici bir çözüm için:
>
> 1. `ConfigMgrInstallation.adm`Not defteri 'nde düzenleyin.
> 2. Özelliği için `VALUENAME SetupParameters` `MAXLEN` değeri daha büyük bir tam sayı olarak değiştirin. Örneğin, `MAXLEN 511`.

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Bir Grup İlkesi nesnesi kullanarak istemci yükleme özelliklerini yapılandırma ve atama  

1. Windows Grup İlkesi Nesne Düzenleyicisi gibi bir düzenleyiciyi kullanarak ConfigMgrInstallation. adm yönetim şablonunu yeni veya var olan bir Grup İlkesi nesnesine (GPO) aktarın. Bu dosyayı `TOOLS\ConfigMgrADMTemplates` Configuration Manager yükleme medyasında klasöründe bulabilirsiniz.  

2. İçeri aktarılan **İstemci Dağıtım Ayarlarını Yapılandır** ayarının özelliklerini açın.  

3. **Etkin**'i seçin.  

4. **CCMSetup** kutusunda, gerekli CCMSetup komut satırı özelliklerini girin. Tüm CCMSetup komut satırı özelliklerinin listesi ve kullanımları örnekleri için bkz. [istemci yükleme parametreleri ve özellikleri hakkında](about-client-installation-properties.md).  

5. Configuration Manager istemci yükleme özellikleriyle sağlamak istediğiniz bilgisayarlara GPO atayın.