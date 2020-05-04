---
title: Altyapıyı değiştirme
titleSuffix: Configuration Manager
description: Configuration Manager altyapınızı etkileyen değişiklikler yapın veya eylemler gerçekleştirin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713677"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Configuration Manager altyapınızı değiştirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir veya daha fazla site yükledikten sonra, yapılandırmaların değiştirilmesi veya altyapınızı etkileyen işlemler gerçekleştirmeniz gerekebilir.

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a>SMS Sağlayıcıyı yönetme

SMS sağlayıcısı, bir veya daha fazla Configuration Manager konsolu için yönetim iletişim noktası sağlar. Birden çok SMS sağlayıcısı yüklediğinizde, site ve hiyerarşinizi yönetmek için iletişim noktaları için artıklık sağlayabilirsiniz.

Her Configuration Manager sitesinde kurulum 'u yeniden çalıştırabilirsiniz:

- SMS sağlayıcısının başka bir örneğini ekleyin. SMS sağlayıcısının her ek örneği ayrı bir bilgisayarda olmalıdır.

- SMS sağlayıcısı 'nın bir örneğini kaldırın. Bir site için son SMS Sağlayıcıyı kaldırmak için, siteyi kaldırmanız gerekir.

Kurulumunu çalıştırdığınız site sunucusunun kök klasöründe **ConfigMgrSetup. log** ' i görüntüleyerek SMS sağlayıcının yüklenmesini veya kaldırılmasını izleyin.

Bir sitedeki SMS sağlayıcısını değiştirmeden önce, bkz. [plan for SMS Provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md).

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>Bir site için SMS sağlayıcı yapılandırmasını yönetme  

1. **Configuration Manager Kurulum 'u** `\BIN\X64\setup.exe` Configuration Manager site yükleme klasöründen çalıştırın.

1. **Başlarken** sayfasında, **Site bakımı yap veya bu siteyi sıfırla**' yı seçin.

1. **Site Bakımı** sayfasında **SMS sağlayıcısı yapılandırmasını değiştir**' i seçin.

1. **SMS Sağlayıcılarını Yönet** sayfasında, aşağıdaki seçeneklerden birini seçin:

    - **Yenı SMS sağlayıcısı ekle**: Şu anda BARıNDıRMAKTA olmayan SMS sağlayıcısını barındıracak bir BILGISAYAR için FQDN belirtin.

    - **BELIRTILEN SMS sağlayıcısını**kaldır: SMS sağlayıcısı 'nı kaldırmak istediğiniz bilgisayarın adını seçin.

    > [!TIP]  
    > SMS Sağlayıcıyı iki bilgisayar arasında taşımak için, önce bunu yeni bilgisayara yüklersiniz. Ardından özgün konumdan kaldırın. SMS sağlayıcısını bilgisayarlar arasında taşıma seçeneği yoktur.

Kurulum Sihirbazı bittikten sonra, SMS sağlayıcı yapılandırması tamamlanır. Site **özellikleri**' nde, **genel** sekmesinde, BIR site için bir SMS sağlayıcısı yüklü olan bilgisayarları doğrulayın.

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a>Configuration Manager konsolunu yönetme

Aşağıdaki görevler Configuration Manager konsolunu yönetmenize yardımcı olur:

- Configuration Manager konsolunda görüntülenen dili değiştirmek için, [Configuration Manager konsolu dilini yönetme](#BKMK_ManageConsoleLanguages) bölümüne bakın.

- Ek konsolları yüklemek için bkz. [ınstall Configuration Manager konsolları](../deploy/install/install-consoles.md).

- Site sunucusundan uzakta olan konsolları etkinleştirmek üzere DCOM izinlerini yapılandırmak için, [uzak Configuration Manager konsolları IÇIN DCOM Izinlerini yapılandırma](#BKMK_ConfigDCOMforRemoteConsole) bölümüne bakın.

- Kullanıcıların konsolunda neleri görebileceğini ve yapabileceklerini sınırlamak üzere yönetici izinlerini değiştirmek için, bkz. [yönetici kullanıcının yönetim kapsamını değiştirme](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser).

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a>Configuration Manager konsolu dilini yönetme

Site sunucusu yüklemesi sırasında, Configuration Manager konsolu yükleme dosyaları ve site için desteklenen dil paketleri, site sunucusundaki Configuration Manager yükleme yolunun `\Tools\ConsoleSetup` alt klasörüne kopyalanır.

- Site sunucusunda bu klasörden Configuration Manager konsolu yüklemesini başlattığınızda, Configuration Manager konsolu ve desteklenen dil paketi dosyalarını bilgisayara kopyalar.

- Bilgisayardaki geçerli dil ayarı için bir dil paketi kullanılabilir olduğunda, Configuration Manager konsolu bu dilde açılır.

- Configuration Manager konsolu için ilişkili dil paketi yoksa, konsolu Ingilizce (Birleşik Devletler) açılır.

Örneğin, Ingilizce, Almanca ve Fransızca 'yı destekleyen bir site sunucusundan Configuration Manager konsolunu yüklersiniz. Configuration Manager konsolunu, yapılandırılmış dil ayarı Fransızca olan bir bilgisayarda açarsanız, konsol Fransızca ' da açılır. Configuration Manager konsolunu yapılandırılmış dili Japonca olan bir bilgisayarda açarsanız, Japonca dil paketi kullanılamadığından konsol Ingilizce olarak açılır.  

Configuration Manager konsolunun her açılışında:

- TT bilgisayar için yapılandırılmış dil ayarlarını belirler
- Configuration Manager konsolu için ilişkili bir dil paketinin kullanılabilir olup olmadığını doğrular
- Konsolu uygun dil paketini kullanarak açar

Bilgisayardaki yapılandırılmış dil ayarlarından bağımsız olarak Configuration Manager konsolunu Ingilizce açmak istediğinizde, bilgisayardaki dil paketi dosyalarını kaldırın veya yeniden adlandırın.

Bilgisayardaki yapılandırılmış yerel ayarı ne olursa olsun Configuration Manager konsolunu Ingilizce olarak başlatmak için aşağıdaki yordamları kullanın.  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Bilgisayarlarda Configuration Manager konsolunun yalnızca Ingilizce sürümünü yükler  

1. Windows Gezgini 'nde, Configuration Manager yükleme `\Tools\ConsoleSetup\LanguagePack` yolunda öğesine gidin.

1. **.msp** ve **.mst** dosyalarını yeniden adlandırın. Örneğin, ** &lt;dosya adını\>değiştirebilirsiniz. MSP** 'den ** &lt;dosya adına\>. MSP. Disabled**.

1. Configuration Manager konsolunu bilgisayara yüklersiniz.

    > [!IMPORTANT]
    > Site sunucusu için yeni sunucu dilleri yapılandırıldığında,. msp ve. MST dosyaları **LanguagePack** klasörüne yeniden kopyalanır ve yeni Configuration Manager konsollarını yalnızca İngilizce yüklemek için bu yordamı yinelemeniz gerekir.  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Mevcut bir Configuration Manager konsolu yüklemesinde bir konsol dilini geçici olarak devre dışı bırakma

1. Configuration Manager konsolunu çalıştıran bilgisayarda, Configuration Manager konsolunu kapatın.

1. Windows Gezgini 'nde, Configuration Manager konsol &lt;bilgisayarında *consoleınstallationpath*> \Bin\ ' e gidin.  

1. Uygun dil klasörünü, bilgisayarda yapılandırılmış dil için yeniden adlandırın. Örneğin, bilgisayar için dil ayarları Almanca olarak belirlenmişse **de** klasörünü **de.disabled** olarak yeniden adlandırabilirsiniz.  

1. Configuration Manager konsolunu bilgisayar için yapılandırılmış dilde açmak için, klasörü orijinal adıyla yeniden adlandırın. Örneğin **de.disabled** klasörünü **de** olarak yeniden adlandırın.  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a>Uzak konsollar için DCOM izinlerini yapılandırma

Configuration Manager konsolunu çalıştıran kullanıcı hesabı, SMS sağlayıcı kullanarak site veritabanına erişim izni gerektirir. Ancak, uzak bir Configuration Manager konsolunu kullanan bir yönetici kullanıcı, üzerinde **Uzaktan etkinleştirme** DCOM izinleri gerektirir:

- Site sunucusu bilgisayar

- SMS sağlayıcısı 'nın bir örneğini barındıran her bilgisayar

**SMS yöneticileri** adlı güvenlik grubu BIR bilgisayardaki SMS Sağlayıcısına erişim verir ve gerekli DCOM izinlerini vermek için de kullanılabilir. SMS sağlayıcı bir üye sunucuda çalıştırıldığında bu grup bilgisayarda yereldir. SMS sağlayıcı bir etki alanı denetleyicisinde çalıştırıldığında, bu bir etki alanı yerel grubudur.

> [!IMPORTANT]
> Configuration Manager konsolu SMS sağlayıcısına bağlanmak için WMI kullanır ve WMI, dahili olarak DCOM kullanır. Configuration Manager konsolu SMS sağlayıcı bilgisayarından başka bir bilgisayarda çalışıyorsa, SMS sağlayıcı bilgisayarında bir DCOM sunucusunu etkinleştirmek için izinler gerekir. Varsayılan olarak, uzaktan etkinleştirme yalnızca yerleşik Yöneticiler grubunun üyelerine verilir.
>
> SMS yöneticileri grubuna uzaktan etkinleştirme izni bulunmasına izin verirseniz, bu grubun bir üyesi SMS sağlayıcı bilgisayarında DCOM saldırıları deneyebilir. Bu yapılandırma aynı zamanda bilgisayarın saldırı yüzeyini de arttırır. Bu tehdidi azaltmak için, SMS Yöneticileri grubunun üyeliğini dikkatli yönetin.

Yönetim kullanıcıları için uzaktan Configuration Manager konsol erişimi sağlamak üzere her bir merkezi yönetim sitesini (CAS), birincil site sunucusunu ve SMS sağlayıcısının yüklendiği her bilgisayarı yapılandırmak için aşağıdaki yordamı kullanın.

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Uzaktan Configuration Manager konsol bağlantıları için DCOM izinlerini yapılandırma

1. Hedef bilgisayarda yönetici olarak, **Bileşen Hizmetleri**'ni açmak `Dcomcnfg.exe` için öğesini çalıştırın.

1. **Bileşen Hizmetleri**' ni genişletin, **bilgisayarlar**' ı genişletin ve **ardından Bilgisayarım ' ı seçin.** **Eylem** menüsünde **Özellikler**' i seçin.

1. Bilgisayarım **Özellikler** penceresinde **com güvenliği** sekmesine geçin. **Başlatma ve etkinleştirme izinleri** bölümünde **sınırları Düzenle**' yi seçin.

1. **Başlatma ve etkinleştirme izinleri** penceresinde **Ekle**' yi seçin.

1. **Kullanıcıları, bilgisayarları, hizmet hesaplarını veya grupları seç** penceresinde, **Seçilecek nesne adlarını girin** alanına yazın `SMS Admins`ve ardından **Tamam**' ı seçin.

   > [!TIP]
   > SMS yöneticileri grubunu bulmak için **Bu konumdan**ayarını değiştirmeniz gerekebilir: SMS sağlayıcı bir üye sunucuda çalıştırıldığında bu grup bilgisayarda yereldir ve SMS sağlayıcı bir etki alanı denetleyicisinde çalıştırıldığında bir etki alanı yerel grubudur.

1. **SMS yöneticileri Için izinler** bölümünde, uzaktan etkinleştirmeye izin vermek Için, **Uzaktan etkinleştirme** satırına **izin ver** sütununu seçin.

1. Değişiklikleri kaydetmek ve tüm pencereleri kapatmak için **Tamam** ' ı seçin.

Bilgisayarınız artık SMS yöneticileri grubunun üyelerine uzaktan Configuration Manager konsolunun erişimine izin verecek şekilde yapılandırılmıştır.

Uzaktan Configuration Manager konsollarını destekleyen her SMS sağlayıcısı bilgisayarında bu yordamı yineleyin.

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a>Site veritabanı yapılandırmasını değiştirme

Bir siteyi yükledikten sonra site veritabanı ve site veritabanı sunucusunun yapılandırmasını değiştirebilirsiniz. Değişiklik yapmak için bir CAS sunucusunda veya birincil site sunucusunda Configuration Manager kurulumunu çalıştırın. Site veritabanını aynı bilgisayardaki yeni bir SQL Server örneğine veya SQL Server’ın desteklenen bir sürümünü çalıştıran farklı bir bilgisayara taşıyabilirsiniz. Bu değişiklikler, ikincil sitelerdeki veritabanı yapılandırması için desteklenmez.

Destek sınırları hakkında daha fazla bilgi için bkz. [Configuration Manager ortamında elle yapılan veritabanı değişikliklerine yönelik destek ilkesi](https://support.microsoft.com/kb/3106512).  

> [!NOTE]
> Bir sitenin veritabanı yapılandırmasını değiştirdiğinizde, Configuration Manager yeniden başlatır veya site sunucusuna ve veritabanıyla iletişim kuran uzak site sistem sunucularına Configuration Manager hizmetleri yeniden yükler.

### <a name="modify-the-database-configuration"></a>Veritabanı yapılandırmasını değiştirme

Site sunucusunda Configuration Manager kurulumunu çalıştırın ve **Site bakımı yap veya bu siteyi sıfırla**seçeneğini belirleyin. Sonra **SQL Server yapılandırmayı Değiştir** seçeneğini belirleyin. Aşağıdaki site veritabanı yapılandırmalarını değiştirebilirsiniz:

- Veritabanını barındıran Windows tabanlı sunucu.

- SQL Server veritabanını barındıran bir sunucuda kullanımda olan SQL Server örneği.

- Veritabanı adı.

- Configuration Manager tarafından kullanılan bağlantı noktası SQL Server.

- Configuration Manager tarafından kullanılan bağlantı noktası SQL Server Hizmet Aracısı.

### <a name="move-the-site-database"></a>Site veritabanını taşıma

Site veritabanını taşırsanız, aşağıdaki konfigürasyonları da gözden geçirin:

- Site veritabanını yeni bir bilgisayara taşıdığınızda, site sunucusunun bilgisayar hesabını SQL Server çalıştıran bilgisayardaki local **Administrators** grubuna ekleyin. Site veritabanı için bir SQL Server kümesi kullanıyorsanız, bilgisayar hesabını her bir Windows Server küme düğümü bilgisayarının yerel **Yöneticiler** grubuna ekleyin.

- Veritabanını SQL Server yeni bir örneğe veya yeni bir SQL Server bilgisayara taşıdığınızda, ortak dil çalışma zamanı (CLR) tümleştirmesini etkinleştirin. Site veritabanını barındıran SQL Server örneğine bağlanmak için **SQL Server Management Studio** kullanın. Ardından aşağıdaki saklı yordamı bir sorgu olarak çalıştırın:`sp_configure 'clr enabled',1; reconfigure`

- Yeni SQL Server yedekleme konumuna erişimi olduğundan emin olun. Site veritabanı yedeklemenizi depolamak için bir UNC kullandığınızda, veritabanını yeni bir sunucuya taşıdıktan sonra, yeni SQL Server bilgisayar hesabının UNC konumuna **yazma** izinlerine sahip olduğundan emin olun. Bu yapılandırma, SQL Server bir AlwaysOn kullanılabilirlik grubuna veya bir SQL Server kümesine ne zaman geçilebileceğinizi içerir.

> [!IMPORTANT]
> Yönetim noktaları için bir veya daha fazla veritabanı yinelemesi içeren bir veritabanını taşımadan önce, önce veritabanı çoğaltmalarını kaldırın. Veritabanı taşımayı tamamladıktan sonra veritabanı yinelemelerini yeniden yapılandırabilirsiniz. Daha fazla bilgi için bkz. [Yönetim noktaları Için veritabanı çoğaltmaları](../deploy/configure/database-replicas-for-management-points.md).

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a>Site veritabanı sunucusu için SPN 'YI yönetme

Site veritabanı için SQL Services çalıştıran hesabı seçebilirsiniz:

- Hizmetler bilgisayar sistem hesabıyla çalıştırıldığında, hizmet asıl adını (SPN) sizin için otomatik olarak kaydeder.

- Hizmetler bir etki alanı yerel kullanıcı hesabıyla çalıştığında SPN 'yi el ile kaydedin. SPN, SQL istemcilerinin ve diğer site sistemlerinin Kerberos ile kimlik doğrulamasına olanak tanır. Kerberos kimlik doğrulaması olmadan veritabanıyla iletişim başarısız olabilir.

SPN 'Ler ve Kerberos bağlantıları hakkında daha fazla bilgi için bkz. [Kerberos bağlantıları için hizmet asıl adını kaydetme](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections).

**Setspn** aracını kullanarak site veritabanı sunucusunun SQL Server hizmet hesabı IÇIN bir SPN kaydedin. Setspn 'yi, SQL Server aynı etki alanındaki bir bilgisayarda etki alanı yöneticisi olarak çalıştırın.

Aşağıdaki yordamlar SQL Server hizmet hesabı için SPN 'nin nasıl yönetileceği örneklerdir. Setspn hakkında daha fazla bilgi için bkz. [Setspn Overview](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\)).

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>SQL Server hizmet hesabı için el ile bir etki alanı kullanıcı SPN 'si oluşturun

1. Yönetici olarak bir komut istemi açın.

1. SPN 'YI hem NetBIOS adı hem de FQDN için oluşturmak üzere geçerli bir komut girin:

    > [!IMPORTANT]
    > Kümelenmiş bir SQL Server için SPN oluşturduğunuzda, SQL Server bilgisayar adı olarak SQL Server kümesinin sanal adını belirtin.

    - NetBIOS adı:`setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        Örneğin, `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - TAM`setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        Örneğin, `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > Bir SQL Server adlandırılmış örnek için SPN kaydetme komutu, varsayılan bir örnek için SPN kaydettiğinizde kullandığınız ile aynıdır. Tek istisna, bağlantı noktası numarasının, adlandırılmış örneğin kullandığı bağlantı noktasıyla aynı olması gerekir.

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>Etki alanı kullanıcı SPN 'nin doğru şekilde kaydedildiğini doğrulama

1. Yönetici olarak bir komut istemi açın.

1. Aşağıdaki komutu girin:`setspn -L <domain\SQL service account>`

    Örneğin, `setspn -L contoso\sqlservice`

1. Kayıtlı **servicePrincipalName**öğesini gözden geçirin. SQL Server için geçerli bir SPN oluşturdunuz emin olun.

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>SQL Server hizmet hesabını yerel sistemden etki alanı kullanıcı hesabına değiştirme

1. SQL Server hizmet hesabı olarak kullanmak istediğiniz bir etki alanı veya yerel sistem kullanıcı hesabı oluşturun ya da seçin.

1. **SQL Server Configuration Manager**’ı açın.

1. **SQL Server Hizmetleri**' ni seçin ve ardından **SQL Server&lt;örnek adı\>**' nı açın.

1. **Oturum açma** sekmesine geçin. **Bu hesabı**seçin ve ardından 1. adımdaki etki alanı kullanıcı hesabı için Kullanıcı adını ve parolayı girin.

1. Hizmet hesabı değişikliğini onaylayın ve SQL Server hizmetini yeniden başlatın.

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a>Site sıfırlaması Çalıştır

Bir CA veya birincil sitede bir site sıfırlaması çalıştırıldığında, site:

- Varsayılan Configuration Manager dosya ve kayıt defteri izinlerini yeniden uygular

- Tüm site bileşenlerini ve tüm site sistemi rollerini yeniden yükler

İkincil siteler Site sıfırlamayı desteklemez.

Bir siteyi el ile sıfırlayabilirsiniz. Ayrıca, site yapılandırmasını değiştirdikten sonra otomatik olarak da çalıştırılabilir. Örneğin:

- Configuration Manager bileşenleri tarafından kullanılan hesaplarda değişiklik yaptıysanız el ile site sıfırlamayı düşünün. Bu eylem, site bileşenlerinin yeni hesap ayrıntılarını kullanmak üzere güncellediğinizden emin olmanızı sağlar.

- Bir sitedeki istemci veya sunucu dillerini değiştirirseniz Configuration Manager otomatik olarak bir site sıfırlaması çalıştırır. Site, yeni dillerin kullanılması için bir sıfırlama gerektirir.

> [!NOTE]
> Site sıfırlaması Configuration Manager olmayan nesneler için erişim izinlerini sıfırlayamaz.

### <a name="what-happens-during-a-site-reset"></a>Site sıfırlaması sırasında ne olur?

Site sıfırlaması çalışırken:

1. Kurulum, **SMS_EXECUTIVE** hizmetinin **SMS_SITE_COMPONENT_MANAGER** hizmetini ve iş parçacığı bileşenlerini durdurup yeniden başlatır.

1. Kurulum, site sistem paylaşma klasörünü ve yerel bilgisayarda ve uzak site sistem bilgisayarlarında bulunan **SMS Executive** bileşenini kaldırır ve yeniden oluşturur.

1. Kurulum, **SMS_EXECUTIVE** ve **SMS_SQL_MONITOR** hizmetlerini yükleyecek **SMS_SITE_COMPONENT_MANAGER** hizmetini yeniden başlatır.

Site sıfırlaması aşağıdaki nesneleri geri yükler:

- **SMS** veya **NAL** kayıt defteri anahtarları ve bu anahtarların altındaki tüm varsayılan alt anahtarlar.

- Configuration Manager dosya dizini ağacı ve bu dosya dizin ağacındaki tüm varsayılan dosyalar veya alt dizinler.

### <a name="prerequisites-for-site-reset"></a>Site sıfırlaması için Önkoşullar

Bir siteyi sıfırlamak için kullandığınız hesabın aşağıdaki izinlere sahip olması gerekir:

- CA 'ları sıfırlamak için:

  - CAS sunucusunda yerel **yönetici**

  - **Tam yönetici** rol tabanlı yönetim güvenlik rolüne denk olan ayrıcalıklar

- Birincil bir siteyi sıfırlamak için:

  - Birincil site sunucusunda yerel **yönetici**

  - **Tam yönetici** rol tabanlı yönetim güvenlik rolüne denk olan ayrıcalıklar
  
  - Birincil site CAS içeren bir hiyerarşide ise, bu hesabın CAS sunucusunda da yerel **yönetici** olması gerekir.

### <a name="limitations-for-a-site-reset"></a>Site sıfırlaması için sınırlamalar

Hiyerarşi, [istemci yükseltmelerini bir ön üretim koleksiyonunda test](../../clients/manage/upgrade/test-client-upgrades.md)etmeyi destekleyecek şekilde yapılandırıldıysa, sitelerdeki sunucu veya istemci dil paketlerini değiştirmek için bir site sıfırlaması kullanamazsınız.

### <a name="run-a-site-reset"></a>Site sıfırlaması gerçekleştirme

1. Aşağıdaki yöntemlerden birini kullanarak site sunucusunda Configuration Manager kurulumunu başlatın:

    - **Başlat** menüsünde **Configuration Manager Kurulum**' u seçin.

    - Configuration Manager *yükleme medyası*dizininde öğesini açın `\SMSSETUP\BIN\X64\setup.exe`. Bu sürümün site sürümüyle aynı olduğundan emin olun.

    - Configuration Manager *yüklendiği*dizinde açın `\BIN\X64\setup.exe`.

1. **Başlarken** sayfasında, **Site bakımı yap veya bu siteyi sıfırla**' yı seçin.

1. **Site Bakımı** sayfasında, **yapılandırma değişikliği olmadan siteyi sıfırla**' yı seçin.

1. Site sıfırlamasına başlamak için **Evet** ' i seçin.

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a>Bir sitedeki dil paketlerini yönetme

Bir site yüklendikten sonra, kullanımda olan sunucu ve istemci dil paketlerini değiştirebilirsiniz.

### <a name="server-language-packs"></a>Sunucu dil paketleri

*Uygulama hedefi: Configuration Manager konsol yüklemeleri, geçerli site sistem rollerinin yeni yüklemeleri*

Sunucu dil paketlerini bir sitede güncelleştirdikten sonra, Configuration Manager konsollarına dil paketleri için destek ekleyebilirsiniz.

Bir Configuration Manager konsoluna bir sunucu dil paketi desteği eklemek için, kullanmak istediğiniz dil paketini içeren bir site sunucusundaki **ConsoleSetup** klasöründen Configuration Manager konsolunu yükleme. Configuration Manager Konsolu zaten yüklüyse, yeni yüklemenin desteklenen dil paketlerinin güncel listesini belirlemesini sağlamak için önce bu sürümü kaldırmanız gerekir.

### <a name="client-language-packs"></a>İstemci dil paketleri

İstemci dil paketlerinde yapılan değişiklikler istemci yükleme kaynak dosyalarını güncelleştirir. Yeni istemci yüklemeleri ve yükseltmeleri güncelleştirilmiş istemci dilleri listesi için destek ekler.

Bir sitedeki istemci dil paketlerini güncelleştirdikten sonra, dil paketlerini kullanacak olan her bir istemciyi istemci dil paketlerini içeren kaynak dosyalarını kullanarak yükleyebilirsiniz.

Configuration Manager desteklediği istemci ve sunucu dilleri hakkında daha fazla bilgi için bkz. [dil paketleri](../deploy/install/language-packs.md).

### <a name="modify-the-supported-language-packs-at-a-site"></a>Bir sitede desteklenen dil paketlerini değiştirme

1. Aşağıdaki yöntemlerden birini kullanarak site sunucusunda Configuration Manager kurulumunu başlatın:

    - **Başlat** menüsünde **Configuration Manager Kurulum**' u seçin.

    - Configuration Manager *yükleme medyası*dizininde öğesini açın `\SMSSETUP\BIN\X64\setup.exe`. Bu sürümün site sürümüyle aynı olduğundan emin olun.

    - Configuration Manager *yüklendiği*dizinde açın `\BIN\X64\setup.exe`.

1. **Başlarken** sayfasında, **Site bakımı yap veya bu siteyi sıfırla**' yı seçin.

1. **Site Bakımı** sayfasında, **dil yapılandırmasını değiştir**' i seçin.

1. **Önkoşul İndirmeleri** sayfasında, aşağıdaki seçeneklerden birini seçin:

    - **Gerekli dosyaları indir**: dil paketlerine güncelleştirme al.

    - **Daha önce indirilen dosyaları kullan**: siteye eklemek istediğiniz dil paketlerini içeren daha önce indirilen dosyaları kullanın.

1. **Sunucu dili seçimi** sayfasında, bu sitenin desteklediği sunucu dillerini seçin.

1. **Istemci dili seçimi** sayfasında, bu sitenin desteklediği istemci dillerini seçin.

1. Sitedeki dil desteğini değiştirmek için Sihirbazı doldurun.

    > [!NOTE]
    > Configuration Manager, sitedeki tüm site sistem rollerini de yeniden yükler bir site sıfırlaması başlatır.

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a>Veritabanı sunucusu uyarı eşiğini değiştirme

Varsayılan olarak, bir site veritabanı sunucusundaki boş disk alanı azaldığında Configuration Manager uyarı oluşturur:

- 10 GB veya daha az boş disk alanı olduğunda uyarı oluştur
- 5 GB veya daha az boş disk alanı olduğunda kritik uyarı oluştur

Bu değerleri değiştirebilir veya her bir site için uyarıları devre dışı bırakabilirsiniz:

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.

1. Yapılandırmak istediğiniz siteyi seçin. Şeritte **Özellikler**' i seçin.

1. **Uyarı** sekmesine geçin ve ardından ayarları düzenleyin.

## <a name="uninstall-sites-and-hierarchies"></a>Siteleri ve hiyerarşileri kaldırma

Bir Configuration Manager site sistem rolünü, sitesini veya hiyerarşisini kaldırmanız gerekebilir. Daha fazla bilgi için bkz. [rolleri, siteleri ve hiyerarşileri kaldırma](../deploy/install/uninstall-sites-and-hierarchies.md).

Sürüm 2002 ' den başlayarak, CA 'ları bir hiyerarşiden da kaldırabilir, ancak birincil siteyi tutabilirsiniz. Daha fazla bilgi için bkz. [CA 'Ları kaldırma](../deploy/install/remove-central-administration-site.md).
