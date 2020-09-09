---
title: Laboratuvarınızı kurma
titleSuffix: Configuration Manager
description: Configuration Manager benzetilen gerçek zamanlı etkinliklerle değerlendirmek için bir laboratuvar kurun.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 7623663e340d964593854883fa588484e239b4d0
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607866"
---
# <a name="set-up-a-configuration-manager-lab"></a>Configuration Manager Laboratuvarı ayarlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konudaki yönergelerin ardından, Configuration Manager benzetimli gerçek zamanlı etkinliklerle değerlendirmek için bir laboratuvar ayarlamanıza olanak sağlar.  

> [!NOTE]
> Microsoft, Configuration Manager değerlendirme sürümünü kullanarak bu laboratuvarın önceden yapılandırılmış bir sürümünü sunmaktadır. Daha fazla bilgi için bkz. [Windows ve Office dağıtımı ve Yönetim Laboratuvarı seti](/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab). 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> Temel bileşenler  
 Ortamınızı Configuration Manager için ayarlamak, Configuration Manager yüklenmesini desteklemek için bazı çekirdek bileşenleri gerektirir.    

-   **Laboratuvar ortamı, Configuration Manager yükleyeceğiniz Windows Server 2012 R2 'yi kullanır**.  

     [Değerlendirme merkezinden](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012)Windows Server 2012 R2 'nin değerlendirme sürümünü indirebilirsiniz.  

     Bu alýþtýrmalar boyunca başvurulan indirmelere daha kolay erişebilmek için Internet Explorer Artırılmış güvenlik yapılandırmasını değiştirmeyi veya devre dışı bırakmayı göz önünde bulundurun. Daha fazla bilgi için bkz. [Internet Explorer: Artırılmış Güvenlik Yapılandırması](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10)).  

-   **SQL Server 2012 SP2** kullanır.  

     SQL Server 2012 ' nin değerlendirme sürümünü [Microsoft Indirme merkezi](https://www.microsoft.com/download/details.aspx?id=43340)' nden indirebilirsiniz.  

     SQL Server, Configuration Manager ile kullanılması için karşılanması gereken [SQL Server desteklenen sürümlerini](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) içerir.  

    -   Configuration Manager, site veritabanını barındırmak için SQL Server 64 bitlik bir sürümünü gerektirir.  

    -   **SQL_Latin1_General_CP1_CI_AS** , **SQL Harmanlama** sınıfı olarak kullanılır.  

    -   **Windows kimlik doğrulaması**, [SQL kimlik doğrulaması](/sql/relational-databases/security/choose-an-authentication-mode)yerine tercih edilir.  

    -   Adanmış bir **SQL Server örneği** gereklidir.  

    -   SQL Server için **sistem adreslenebilir belleği** sınırlandırmayın.  

    -   **SQL Server hizmet hesabını** , düşük haklara sahip bir etki alanı kullanıcı hesabı kullanarak çalışacak şekilde yapılandırın.  

    -   **SQL Server Reporting Services**'ı yüklemelisiniz.  

    -   **Siteler arası iletişimler** varsayılan TCP 4022 bağlantı noktasındaki SQL Server Hizmet Aracısı'nı kullanır.  

    -   SQL Server veritabanı altyapısı ve Configuration Manager site sistemi rolleri arasındaki **site içi iletişimler** varsayılan bağlantı noktası TCP 1433 ' i kullanır.  

-   **Etki alanı denetleyicisi, Active Directory Domain Services yüklü Windows Server 2008 R2 'yi kullanır** . Etki alanı denetleyicisi aynı zamanda, DHCP ve DNS sunucuları için tam etki alanı adıyla kullanılmak üzere ana bilgisayar olarak çalışır.  

     Daha fazla bilgi için bkz. [Active Directory Domain Services genel bakış](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831484(v=ws.11)).  

-   Hyper-V, bu alıştırmalarda uygulanan yönetim adımlarının beklendiği gibi çalıştığını doğrulamak için **birkaç sanal makineyle kullanılır** . Windows 10 yüklü olan en az üç sanal makine önerilir.  

     Daha fazla bilgi için bkz. [Hyper-V ' e genel bakış](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).  

-   **yönetici izinleri** gereklidir.  

    -   Configuration Manager, Windows Server ortamında yerel izinlere sahip bir yönetici gerektirir  

    -   Active Directory, şemayı değiştirme izinlerine sahip bir yönetici gerektirir  

    -   Sanal makineler, makinelerin kendisinde yerel izinler gerektirir  

Bu laboratuvar için gerekli olmasa da, Configuration Manager uygulama gereksinimleri hakkında daha fazla bilgi için [Desteklenen yapılandırmaların Configuration Manager](../../core/plan-design/configs/supported-configurations.md) gözden geçirebilirsiniz. Burada başvurulmadan başka yazılım sürümleri için belgelere bakın.  

Bu bileşenlerin tümünü yükledikten sonra, Windows ortamınızı Configuration Manager için yapılandırmak üzere yapmanız gereken ek adımlar vardır:  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> Active Directory içeriğini laboratuvar için hazırlama  
 Bu laboratuvar için bir güvenlik grubu oluşturup gruba bir etki alanı kullanıcısı eklersiniz.  

-   Güvenlik grubu: **Evaluation**  

    -   Grup kapsamı: **Universal**  

    -   Grup türü: **güvenlik**  

-   Etki alanı kullanıcısı: **ConfigUser**  

     Normal şartlar altında ortamınızdaki tüm kullanıcılara evrensel erişim vermezsiniz. Bunu, bu kullanıcı için laboratuvarınızı çevrimiçi hale getirme işlemini kolaylaştırmak üzere yaparsınız.  

Configuration Manager istemcilerinin site kaynaklarını bulmak için Active Directory Domain Services sorgulamasını sağlamak için gereken sonraki adımlar, sonraki yordamlarda listelenir.  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> Sistem Yönetimi kapsayıcısını oluşturma  
 Configuration Manager, şema genişletildiğinde Active Directory Domain Services gerekli sistem yönetimi kapsayıcısını otomatik olarak oluşturmaz. Bu nedenle bunu, laboratuvarınız için kendiniz oluşturursunuz. Bu adım, [ADSI düzenleme yüklemenizi](/previous-versions/windows/it-pro/windows-server-2003/cc773354(v=ws.10))gerektirir.

 Active Directory Etki Alanı Hizmetleri'nde **Sistem** Kapsayıcısı’nda **Tüm Bağımlı Nesneleri Oluştur** iznine sahip bir hesapla oturum açmalısınız.  

#### <a name="to-create-the-system-management-container"></a>Sistem Yönetimi kapsayıcısını oluşturmak için:  

1.  **ADSI Düzenleyicisi**'ni çalıştırın ve site sunucusunun bulunduğu etki alanına bağlanın.  

2.  **Etki alanı &lt; bilgisayar tam etki alanı adını \> **genişletin, **<ayırt edici \> ad**' ı genişletin, **CN = System**' **e**sağ tıklayın ve ardından **nesne**' ye tıklayın.  

3.  **Nesne Oluştur** iletişim kutusunda, **Kapsayıcı**'yı seçin ve ardından **İleri**'ye tıklayın.  

4.  **Değer** kutusuna **System Management**yazdıktan sonra **İleri**'ye tıklayın.  

5.  Yordamı tamamlamak için **Son** 'a tıklayın.  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> Sistem Yönetimi kapsayıcısı için güvenlik izinleri ayarlama  
 Site sunucusunun bilgisayar hesabına, site bilgilerini kapsayıcıda yayımlamak için gereken izinleri verin. Bu görev için de ADSI Düzenleyicisi kullanırsınız.  

> [!IMPORTANT]  
>  Sonraki yordama başlamadan önce site sunucusunun etki alanına bağlı olduğunuzdan emin olun.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Sistem Yönetimi kapsayıcısı için güvenlik izinleri ayarlamak için:  

1.  Konsol bölmesinde, **site sunucusunun etki alanını**genişletin, **DC = &lt; sunucu ayırt edici adı \> **' nı genişletin ve sonra **CN = System**' i genişletin. **CN=System Management**'a sağ tıkladıktan sonra **Özellikler**'e tıklayın.  

2.  **CN=System Management Properties** iletişim kutusunda, **Güvenlik** sekmesine tıkladıktan sonra **Ekle** 'ye tıklayarak site sunucusu bilgisayar hesabını ekleyin. Hesaba **Tam Denetim** izinleri verin.  

3.  **Gelişmiş**' e tıklayın, site sunucusunun bilgisayar hesabını seçin ve ardından **Düzenle**' ye tıklayın.  

4.  **Uygula** listesinde, **Bu nesne ve tüm alt nesneler**'i seçin.  

5.  **Tamam** 'a tıklayarak **ADSI Düzenleyicisi** konsolunu kapatın ve yordamı tamamlayın.  

     Daha fazla bilgi için bkz [. Configuration Manager için Active Directory Şemayı genişletme](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> extadsch.exe kullanarak Active Directory şemasını genişletme  
 Bu laboratuvar için Active Directory şemasını genişletecaksınız çünkü bu, tüm Configuration Manager özellikleri ve işlevleri en az yönetim yüküyle kullanmanıza olanak sağlar. Active Directory şemasının genişletilmesi, her orman için bir kez yapılan orman çapında bir yapılandırmadır. Şemanın genişletilmesi, temel Active Directory yapılandırmanızdaki sınıf ve öznitelik kümelerini kalıcı olarak değiştirir. Bu eylem geri alınamaz. Şemayı genişletmek Configuration Manager, Laboratuvar ortamınızda en verimli şekilde çalışmasını sağlayan bileşenlere erişmesini sağlar.  

> [!IMPORTANT]  
>  Şema yöneticisi etki alanı denetleyicisinde **Şema Yöneticileri** güvenlik grubunun üyesi olan bir hesapla oturum açmalısınız. Alternatif kimlik bilgilerini kullanma girişimi başarısız olur.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>extadsch.exe kullanarak Active Directory şemasını genişletmek için:  

1.  Şema yöneticisi etki alanı denetleyicisinin sistem durumunun bir yedeğini oluşturun. Ana etki alanı denetleyicisini yedekleme hakkında daha fazla bilgi için bkz. [Windows Server yedekleme](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770757(v=ws.11))  

2.  Yükleme medyasında **\SMSSETUP\BIN\X64** konumuna gidin.  

3.  **extadsch.exe**'i çalıştırın.  

4.  Sistem sürücüsünün kök klasöründe bulunan **extadsch.log** dosyasını inceleyerek şema genişletmenin başarılı olup olmadığını doğrulayın.  

     Daha fazla bilgi için bkz. [Configuration Manager için Active Directory şemasını genişletme](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> Diğer gerekli görevler  
 Yüklemeden önce şu görevleri de tamamlamanız gerekir.  

 **Tüm yüklemeleri depolamak için klasör oluşturma**  

 Bu alıştırmada yükleme ortamı bileşenleri için birden fazla indirme gerekir. Yükleme yordamlarına başlamadan önce laboratuvarınızı kullanımdan çıkarana dek bu dosyaları taşımanızı gerektirmeyecek bir konum belirleyin. Bu indirmeleri depolamanız için ayrı alt klasörleri bulunan tek bir klasör öneririz.  

 **.NET yükleme ve Windows Communication Foundation’ı etkinleştirme**  

 İki .NET Framework sürümü yüklemeniz gerekir: Önce .NET 3.5.1 ve sonra .NET 4.5.2+. Ayrıca Windows Communication Foundation’ı etkinleştirmeniz gerekir. WCF; dağıtılmış bilgi işlem, kapsamlı birlikte çalışılabilirlik ve hizmet yönlendirmesi için doğrudan desteğe yönelik yönetilebilir bir yaklaşım sunmak üzere tasarlanmıştır ve hizmet odaklı bir programlama modeli aracılığıyla bağlı uygulamaların geliştirilmesini kolaylaştırır. Daha fazla bilgi için bkz. [Windows Communication Foundation nedir?](/previous-versions/dotnet/netframework-3.5/ms731082(v=vs.90)).

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>.NET yüklemek ve Windows Communication Foundation’ı etkinleştirmek için:  

1.  **Server Manager**’ni açın ve **Yönet**’e gidin. Rol ve **Özellik Ekleme Sihirbazı** ' nı açmak için **rol ve Özellik Ekle** ' ye tıklayın.  

2.  **Başlamadan Önce** bölmesindeki bilgileri gözden geçirip **İleri**’ye tıklayın.  

3.  **Rol tabanlı veya özellik tabanlı yükleme**’yi seçip **İleri**’ye tıklayın.  

4.  **Sunucu Havuzu**’ndan sunucunuzu seçip **İleri**’ye tıklayın.  

5.  **Sunucu Rolleri** bölmesini gözden geçirip **İleri**’ye tıklayın.  

6.  Listeden seçerek aşağıdaki **Özellikleri** ekleyin:  

    -   **.NET Framework 3.5 Özellikleri**  

        -   **.NET Framework 3.5 (.NET 2.0 ve 3.0 içerir)**  

    -   **.NET Framework 4.5 Özellikleri**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **WCF Hizmetleri**  

            -   **HTTP Etkinleştirmesi**  

            -   **TCP Bağlantı Noktası Paylaşma**  

7.  **Web Sunucusu Rolü (IIS)** ve **Rol Hizmetleri** ekranını gözden geçirip **İleri**’ye tıklayın.  

8.  **Onay** ekranını gözden geçirip **İleri**’ye tıklayın.  

9. **Yükle** ’ye tıklayın ve **Sunucu Yöneticisi** ’nin **Bildirimler**bölmesinden yüklemenin düzgün bir şekilde tamamlanıp tamamlanmadığını doğrulayın.  

10. .NET’in temel yüklemesi tamamlandıktan sonra .NET Framework 4.5.2’nin web yükleyicisini edinmek için [Microsoft Yükleme Merkezi](https://www.microsoft.com/download/details.aspx?id=42643) ’ne gidin. **İndir** düğmesine tıklayıp yükleyiciyi **Çalıştırın** . Bu işlem, gerekli bileşenleri seçtiğiniz dilde otomatik olarak algılayıp yükler.  

**BITS, IIS ve RDC’yi etkinleştirme**  

Bir istemci ve sunucu arasında dosyaları zaman uyumsuz olarak aktarması gereken uygulamalar için [Arka Plan Akıllı Aktarım Hizmeti (BITS)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282296(v=ws.11)) kullanılır. BITS, ön ve arka plandaki aktarım akışını ölçerek diğer ağ uygulamalarının yanıt hızlarını korur. Ayrıca bir aktarım oturumu kesintiye uğrarsa dosya aktarımına otomatik olarak devam eder.  

Bu site sunucusu yönetim noktası olarak da kullanılacağından bu laboratuvar için BITS’i yüklersiniz.  

Internet Information Services (IIS), web’deki herhangi bir şeyi barındırmak için kullanılabilen esnek, ölçeklenebilir bir web sunucusudur. Birçok site sistemi rolü için Configuration Manager tarafından kullanılır. IIS hakkında daha fazla bilgi için [site sistemi sunucuları Için Web sitelerini](../../core/plan-design/network/websites-for-site-system-servers.md)gözden geçirin.  

[Uzaktan Değişiklikleri Sıkıştırma (RDC)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754372(v=ws.11)) , uygulamaların, belirli bir dosya kümesinde herhangi bir değişiklik yapılıp yapılmadığını tespit etmek üzere kullanabileceği bir API kümesidir. RDC, uygulamanın dosyanın yalnızca değişmiş bölümlerini çoğaltmasını sağlayarak ağ trafiğini en düşük düzeyde tutar.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>BITS, IIS ve RDC site sunucusu rollerini etkinleştirmek için:  

1.  Site sunucunuzdan **Server Manager**’ni açın. **Yönet**'e gidin. **Rol ve Özellik Ekleme Sihirbazı** ’nı açmak için **Rol ve Özellik Ekle**’ye tıklayın.  

2.  **Başlamadan Önce** bölmesindeki bilgileri gözden geçirip **İleri**’ye tıklayın.  

3.  **Rol tabanlı veya özellik tabanlı yükleme**’yi seçip **İleri**’ye tıklayın.  

4.  **Sunucu Havuzu**’ndan sunucunuzu seçip **İleri**’ye tıklayın.  

5.  Listeden seçerek aşağıdaki **Sunucu Rollerini** ekleyin:  

    -   **Web Sunucusu (IIS)**  

        -   **Ortak HTTP Özellikleri**  

            -   **Varsayılan Belge**  

            -   **Dizin Tarama**  

            -   **HTTP Hataları**  

            -   **Statik İçerik**  

            -   **HTTP Yeniden Yönlendirme**  

        -   **Sistem Durumu ve Tanılama**  

            -   **HTTP Günlüğe Kaydetme**  

            -   **Günlük Araçları**  

            -   **İstek İzleyicisi**  

            -   **İzleme**  

    -   **Performans**  

        -   **Statik İçerik Sıkıştırması**  

        -   **Dinamik İçerik Sıkıştırması**  

    -   **Güvenlik**  

        -   **İstek Filtreleme**  

        -   **Temel kimlik doğrulaması**  

        -   **İstemci Sertifikası Eşleme Kimlik Doğrulaması**  

        -   **IP ve Etki Alanı Kısıtlamaları**  

        -   **URL Yetkilendirmesi**  

        -   **Windows Kimlik Doğrulaması**  

    -   **Uygulama geliştirme**  

        -   **.NET Genişletilebilirliği 3.5**  

        -   **.NET Extensibility 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **ISAPI Uzantıları**  

        -   **ISAPI filtreleri**  

        -   **Sunucu Tarafına Şunlar Dahildir**  

    -   **FTP Sunucusu**  

        -   **FTP Hizmeti**  

    -   **Yönetim Araçları**  

        -   **IIS Yönetim Konsolu**  

        -   **IIS 6 Yönetimi Uyumluluğu**  

            -   **IIS 6 Metatabanı Uyumluluğu**  

            -   **IIS 6 Yönetim Konsolu**  

            -   **IIS 6 Komut Dosyası Araçları**  

            -   **IIS 6 WMI Uyumluluğu**  

        -   **IIS 6 Yönetim Komut Dosyaları ve Araçları**  

        -   **Yönetim Hizmeti**  

6.  Listeden seçerek aşağıdaki **Özellikleri** ekleyin:  

    -   **Arka Plan Akıllı Aktarım Hizmeti (BITS)**  

          -   **IIS Sunucusu Uzantısı**  

    -   **Uzak Sunucu Yönetim Araçları**  

          -   **Özellik Yönetimi Araçları**  

          -   **BITS Sunucu Uzantıları Araçları**  

7.  **Yükle** ’ye tıklayın ve **Sunucu Yöneticisi** ’nin **Bildirimler**bölmesinden yüklemenin düzgün bir şekilde tamamlanıp tamamlanmadığını doğrulayın.  

Varsayılan olarak IIS, çeşitli dosya uzantısı türlerine ve konumlarına HTTP veya HTTPS iletişimi tarafından erişilmesini engeller. Bu dosyaların istemci sistemlerine dağıtılmasına izin vermek için dağıtım noktanızda IIS için istek filtrelemeyi yapılandırmanız gerekir. Daha fazla bilgi için bkz. [dağıtım noktaları Için IIS Istek filtreleme](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Dağıtım noktalarında IIS filtrelemesini yapılandırmak için:  

1.  **IIS Manager** ’ni açın ve kenar çubuğunda sunucunuzun adını seçin. Bu işlem sizi **Giriş** ekranına götürür.  

2.  **Giriş** ekranının altında **Özellikler Görünümü** ’nün seçili olması gerekir. **IIS** ’ye gelip **İstek Filtreleme**’yi açın.  

3.  **Eylemler** bölmesinde **Dosya Adı Uzantısına İzin Ver...** öğesine tıklayın.  

4.  İletişim kutusuna **.msi** yazıp **Tamam**’a tıklayın.  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Configuration Manager’ı yükleme  
İstemcileri doğrudan yönetmek için bir [birincil sitenin ne zaman kullanılacağını belirleme](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) oluşturacaksınız. Bu, laboratuvar ortamınızın olası cihazların [site sistem ölçeğinde](../plan-design/configs/size-and-scale-numbers.md) yönetimini desteklemesini sağlar.  
Bu işlem sırasında, değerlendirme cihazlarınızı ileriye doğru yönetmek için kullanılacak Configuration Manager konsolunu da yükleyeceksiniz.  

Yüklemeye başlamadan önce tüm ayarların doğru bir şekilde etkinleştirildiklerini doğrulamak üzere Windows Server 2012 kullanarak sunucuda  [Prerequisite Checker](../servers/deploy/install/prerequisite-checker.md) programını başlatın.  

#### <a name="to-download-and-install-configuration-manager"></a>Configuration Manager’ı indirmek ve yüklemek için:  

1.  Configuration Manager en yeni değerlendirme sürümünü indirmek için [System Center değerlendirmeleri](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) sayfasına gidin.  

2.  Sıkıştırılmış indirme ortamını önceden tanımlanmış konumunuzda açın.  

3.  [Configuration Manager Kurulum Sihirbazı 'nı kullanarak site yükleme](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md)' de listelenen yükleme yordamını izleyin. Bu yordamda şunları girersiniz:  

    |Site yükleme yordamında adım|Seçim|  
    |-----------------------------------------|---------------|  
    |4. Adım: **Ürün Anahtarı** sayfası|**Değerlendirme**’yi seçin.|  
    |7. Adım:  **Önkoşul İndirmeleri**|**Gerekli dosyaları indir** ’i seçip önceden tanımladığınız konumu belirtin.|  
    |10. Adım: **Site ve Yükleme Ayarları**|-   **Site kodu:LAB**<br />-   **Site adı:Evaluation**<br />-   **Yükleme klasörü:** Önceden tanımladığınız konumu belirtin.|  
    |11. Adım: **Birincil Site Yüklemesi**|**Birincil siteyi tek başına site olarak yükle**seçeneğini belirleyip **İleri**’ye tıklayın.|  
    |12. Adım: **Veritabanı Yüklemesi**|-   **SQL Server adı (FQDN):** Buraya FQDN değerinizi girin.<br />-   **Örnek adı:** Önceden yüklediğiniz varsayılan SQL örneğini kullanacağınız için bu değeri boş bırakın.<br />-   **Hizmet Aracısı Bağlantı Noktası:** Varsayılan 4022 bağlantı noktasını değiştirmeyin.|  
    |13. Adım: **Veritabanı Yüklemesi**|Bu ayarları varsayılan olarak bırakın.|  
    |14. Adım: **SMS sağlayıcısı**|Bu ayarları varsayılan olarak bırakın.|  
    |15. Adım: **İstemci İletişim Ayarları**|**Tüm site sistemi rolleri istemcilerden yalnızca HTTPS bağlantısı kabul eder** ’in seçili olmadığını doğrulayın|  
    |16. Adım: **Site Sistemi Rolleri**|FQDN değerinizi girip **Tüm site sistemi rolleri istemcilerden yalnızca HTTPS bağlantısı kabul eder** ’in hala seçili olmadığından emin olun.|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a> Configuration Manager sitesi için yayımlamayı etkinleştirme  
Her bir Configuration Manager sitesi, kendi siteye özgü bilgilerini Active Directory şeması içindeki etki alanı bölümü içinde sistem yönetimi kapsayıcısına yayımlar. Bu trafiği işlemek için Active Directory ve Configuration Manager arasındaki iletişim için çift yönlü kanallar açılmalıdır. Active Directory ve ağ altyapınızın belirli bileşenlerini belirlemek için ayrıca Orman Saptama’yı da etkinleştirmeniz gerekir.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Active Directory ormanlarını yayın yapmak için yapılandırmak amacıyla:  

1.  Configuration Manager konsolunun sol alt köşesinde **Yönetim**' e tıklayın.  

2.  **Yönetim** çalışma alanında, **Hiyerarşi Yapılandırması**'nı genişletip **Saptama Yöntemleri**'ne tıklayın.  

3.  **Active Directory Orman Saptama** ’yı seçip **Özellikler**’e tıklayın.  

4.  **Özellikler** iletişim kutusunda **Active Directory Orman Saptama**’yı seçin. Etkin olduğunda **Saptandıklarında Active Directory site sınırlarını otomatik olarak oluştur**seçeneğini belirleyin. **Tam saptamayı mümkün olan en yakın zamanda çalıştırmak ister misiniz?** **Evet**'e tıklayın.  

5.  Ekranın üstündeki **Saptama Yöntemi** grubunda **Orman Saptamayı Şimdi Çalıştır**’a tıklayıp kenar çubuğunda **Active Directory Ormanları** ’na gelin. Saptanan ormanlar listesinde Active Directory ormanınızın görüntülenmesi gerekir.  

6.  Ekranın üstündeki **Genel** sekmesine gelin.  

7.  **Yönetim** çalışma alanında, **Hiyerarşi Yapılandırması**'nı genişletip **Active Directory Ormanları**'na tıklayın.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Configuration Manager sitesinin site bilgilerini Active Directory ormanınızda yayımlamasını sağlamak için:  

1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2.  Henüz saptanmamış yeni bir orman yapılandırırsınız.  

3.  **Yönetim** çalışma alanında, **Active Directory Ormanları**'na tıklayın.  

4.  Site özelliklerinin **Yayımlama** sekmesinde bağlı ormanınızı seçip **Tamam** ’a yapılandırmanızı kaydedin.