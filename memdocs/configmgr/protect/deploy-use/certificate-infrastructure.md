---
title: Sertifika altyapısını yapılandırma
titleSuffix: Configuration Manager
description: Configuration Manager 'da sertifika kaydını yapılandırmayı öğrenin.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 656cc80c929eb7e829dd06b642a83cb174d3b0c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697254"
---
# <a name="configure-certificate-infrastructure"></a>Sertifika altyapısını yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager 'de sertifika altyapısını yapılandırmayı öğrenin. Başlamadan önce, [sertifika profilleri önkoşulları](../../protect/plan-design/prerequisites-for-certificate-profiles.md)bölümünde listelenen önkoşulları denetleyin.  

Altyapınızı SCEP veya PFX sertifikaları için yapılandırmak üzere bu adımları kullanın.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>1. adım-ağ cihazı kayıt hizmeti 'ni ve bağımlılıklarını (yalnızca SCEP sertifikaları için) yükleyip yapılandırın

 Active Directory Sertifika Hizmetleri (AD CS) için Ağ Cihazı Kayıt Hizmetini yüklemeniz ve yapılandırmanız, sertifika şablonlarındaki güvenlik izinlerini değiştirmeniz, bir ortak anahtar altyapısı (PKI) istemci kimlik doğrulama sertifikası dağıtmanız ve İnternet Bilgi Hizmetleri (IIS) varsayılan URL boyut limitini artırmak için kayıt defterini düzenlemeniz gerekir. Gerekirse, yayımlama sertifika yetkilisini (CA), özel bir geçerlilik süresine izin verecek şekilde yapılandırmanız da gerekir.  

> [!IMPORTANT]  
>  Configuration Manager, ağ cihazı kayıt hizmeti ile çalışacak şekilde yapılandırmadan önce, ağ aygıtı kayıt hizmeti yükleme ve yapılandırmasını doğrulayın. Bu bağımlılıklar doğru çalışmıyorsa, Configuration Manager kullanarak sertifika kaydında sorun giderme konusunda zorluk yapmış olursunuz.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Ağ Aygıtı Kayıt Hizmeti ve bağımlılıklarını yüklemek ve yapılandırmak için  

1. Windows Server 2012 R2 çalıştıran bir sunucuda, Active Directory Sertifika Hizmetleri sunucu rolü için Ağ Aygıtı Kayıt Hizmeti rol hizmetini yükleyin ve yapılandırın. Daha fazla bilgi için bkz. [ağ cihazı kayıt hizmeti Kılavuzu](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).

2. Ağ Cihazı Kayıt Hizmetinin kullandığı sertifika şablonları için güvenlik izinlerini denetleyin ve gerekirse değiştirin:  

   -   Configuration Manager konsolunu çalıştıran hesap için: **okuma** izni.  

        Bu izin, Sertifika Profili Oluşturma Sihirbazı'nı çalıştırdığınız zaman, bir SCEP ayarları profili oluşturduğunuzda kullanmak istediğiniz sertifika şablonunu seçmek üzere göz atabilmeniz adına gereklidir. Bir sertifika şablonu seçilmesi, sihirbazda bazı ayarların otomatik olarak doldurulacağı anlamına gelir, böylelikle yapılandıracağınız kısım daha azdır ve Ağ Cihazı Kayıt Hizmetinin kullandığı sertifika şablonlarıyla uyumlu olmayan ayarlar seçilmesine dair daha az risk vardır.  

   -   Ağ Cihazı Kayıt Hizmeti uygulama havuzunun kullandığı SCEP Hizmeti hesabı için: **Okuma** ve **Kayıt** izinleri.  

        Bu gereksinim Configuration Manager özgü değildir ancak ağ cihazı kayıt hizmeti 'nin yapılandırılmasına bir parçasıdır. Daha fazla bilgi için bkz. [ağ cihazı kayıt hizmeti Kılavuzu](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).  

   > [!TIP]  
   >  Ağ Aygıtı Kayıt Hizmetinin hangi sertifika şablonlarını kullandığını belirlemek için, Ağ Aygıtı Kayıt Hizmetini çalıştıran sunucuda şu kayıt defteri anahtarını görüntüleyin: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Bunlar, çoğu ortam için uygun olacak varsayılan güvenlik izinleridir. Ancak, alternatif bir güvenlik yapılandırması kullanabilirsiniz. Daha fazla bilgi için bkz. [sertifika profilleri için sertifika şablonu Izinlerini planlama](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3. Bu sunucuya, istemci kimlik doğrulamasını destekleyen bir PKI sertifikası dağıtın. Bilgisayarınızda yüklü, kullanabileceğiniz uygun bir sertifikanız bulunabilir veya özel olarak bu amaç için bir sertifika dağıtmanız gerekebilir (veya bunu tercih edebilirsiniz). Bu sertifika için gereksinimler hakkında daha fazla bilgi için, [Configuration Manager Için PKI sertifika gereksinimleri](../../core/plan-design/network/pki-certificate-requirements.md) konusunun **sunucular için PKI sertifikaları** bölümünde bulunan Configuration Manager İlkesi modülünü çalıştıran sunucuların ayrıntılarına bakın.  

   > [!TIP]
   >  Bu sertifikayı dağıtmaya yönelik yardıma ihtiyacınız varsa, sertifika gereksinimleri tek bir özel durumla aynı olduğundan [dağıtım noktaları Için Istemci sertifikasını dağıtma](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)yönergelerini kullanabilirsiniz:  
   > 
   > - Sertifika şablonu için özelliklerin **Talep İşleme** sekmesinde **Özel anahtarın dışarı aktarılmasına izin ver** onay kutusunu seçmeyin.  
   > 
   >   Yerel bilgisayar deposuna gözatacağından ve Configuration Manager Ilkesi modülünü yapılandırırken seçebileceksiniz, bu sertifikayı özel anahtarla dışarı aktarmanız gerekmez.  

4. İstemci kimlik doğrulama sertifikasının zincirine bağlı olduğu kök sertifikayı bulun. Ardından, bu kök CA sertifikasını bir sertifika (.cer) dosyasına aktarın. Bu dosyayı, sertifika kayıt noktası için site sistem sunucusunu daha sonra yüklediğinizde ve yapılandırdığınızda güvenli bir şekilde erişebileceğiniz, güvenli bir konuma kaydedin.  

5. Aynı sunucuda, kayıt defteri düzenleyicisini kullanıp HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters içinde aşağıdaki kayıt defteri anahtarı DWORD değerlerini ayarlayarak IIS varsayılan URL boyutunun sınırını artırın:  

   - **MaxFieldLength** anahtarını **65534** olarak ayarlayın.  

   - **MaxRequestBytes** anahtarını **16777216** olarak ayarlayın.  

     Daha fazla bilgi için bkz. Microsoft Desteği makalesi [820129: Windows için kayıt defteri ayarları Http.sys](https://support.microsoft.com/help/820129).

6. Aynı sunucuda, İnternet Bilgi Hizmetleri (IIS) Yöneticisinde, /certsrv/mscep uygulaması için istek filtresi ayarlarını değiştirin ve ardından sunucuyu yeniden başlatın. **İstek Filtresi Ayarlarını Düzenle** iletişim kutusunda, **İstek Sınırları** ayarlarının aşağıdaki gibi olması gerekir:  

   - **İzin verilen maksimum içerik uzunluğu (Bayt)**: **30000000**  

   - **Maksimum URL uzunluğu (Bayt)**: **65534**  

   - **Maksimum sorgu dizesi (Bayt)**: **65534**  

     Bu ayarlar ve nasıl yapılandırılacağı hakkında daha fazla bilgi için bkz. [IIS Istek sınırları](/iis/configuration/system.webServer/security/requestFiltering/requestLimits/).

7. Kullandığınız sertifika şablonundan daha düşük geçerlilik süresine sahip olan bir sertifika talep edebilmek istiyorsanız: Kuruluş sertifika yetkilisi için bu yapılandırma varsayılan olarak devre dışıdır. Bir kuruluş sertifika yetkilisinde bu seçeneği etkinleştirmek için, Certutil komut satırı aracını kullanın ve ardından aşağıdaki komutları kullanarak sertifika hizmetini durdurun ve yeniden başlatın:  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Daha fazla bilgi için bkz. [Sertifika Hizmetleri araçları ve ayarları](/previous-versions/windows/it-pro/windows-server-2003/cc780742\(v=ws.10\)).

8. Aşağıdaki bağlantıyı örnek olarak kullanıp ağ cihazı kayıt hizmetinin çalıştığını doğrulayın: `https://server.contoso.com/certsrv/mscep/mscep.dll` . Yerleşik Ağ Cihazı Kayıt Hizmeti web sayfasını görmeniz gerekir. Bu web sayfası, hizmetin ne olduğunu açıklar ve ağ aygıtlarının sertifika isteklerini göndermek için URL'yi kullandığını açıklar.  

   Artık Ağ Cihazı Kayıt Hizmeti ve bağımlılıkları yapılandırıldığından, sertifika kayıt noktasını yüklemeye ve yapılandırmaya hazırsınız demektir.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>2. adım-sertifika kayıt noktasını yükleyip yapılandırın.

Configuration Manager hiyerarşisinde en az bir sertifika kayıt noktası yüklemeli ve yapılandırmanız gerekir ve bu site sistem rolünü merkezi yönetim sitesine veya bir birincil siteye yükleyebilirsiniz.  

> [!IMPORTANT]  
>  Sertifika kayıt noktasını yüklemeden önce, sertifika kayıt noktası için işletim sistemi gereksinimleri ve Bağımlılıklar için [desteklenen Configuration Manager için yapılandırma](../../core/plan-design/configs/supported-configurations.md) konusunun **site sistem gereksinimleri** bölümüne bakın.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Sertifika kayıt noktasını yüklemek ve yapılandırmak için  

1. Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

2. **Yönetim** çalışma alanında, **Site Yapılandırması** öğesini genişletin, **Sunucu ve Site Sistem Rolleri** öğesine tıklayın ve ardından sertifika kayıt noktası için kullanmak istediğiniz sunucuyu seçin.  

3. **Sunucu** grubunun **Giriş** sekmesinde, **Site Sistemi Rolleri Ekle**'yi tıklatın.  

4. **Genel** sayfasında, site sisteminin genel ayarlarını belirleyin ve **İleri**'yi tıklatın.  

5. **Proxy** sayfasında, **İleri**'ye tıklayın. Sertifika kayıt noktası, İnternet proxy ayarları kullanmaz.  

6. **Sistem Rolü Seçim** sayfasında, kullanılabilir roller listesinden **Sertifika kayıt noktası**'nı seçin ve ardından **İleri**'ye tıklayın. 

7. **Sertifika kayıt modu** sayfasında, bu sertifika kayıt noktasının **SCEP sertifika isteklerini IŞLEMESINI**mi yoksa **PFX Sertifika isteklerini işlemesini**mi istediğinizi seçin. Sertifika kayıt noktası her iki isteği de işleyemez, ancak her iki sertifika türüyle de çalışıyorsanız birden çok sertifika kayıt noktası oluşturabilirsiniz.

   PFX sertifikalarını işleme alıyorsa, Microsoft veya Entrust olarak bir sertifika yetkilisi seçmeniz gerekir.

8. **Sertifika kayıt noktası ayarları** sayfası, sertifika türüne göre değişir:
   - **SCEP sertifika Isteklerini işle**' yi seçtiyseniz, aşağıdakileri yapılandırın:
     -   Sertifika kayıt noktası için **Web sitesi adı**, **HTTPS bağlantı noktası numarası**ve **sanal uygulama adı** . Bu alanlar varsayılan değerlerle otomatik olarak doldurulur. 
     -   **Ağ cihazı kayıt hizmeti ve kök CA sertifikası Için URL** - **Ekle**' ye tıklayın, ardından **URL ve kök CA sertifikası Ekle** iletişim kutusunda aşağıdakileri belirtin:
         - **Ağ Cihazı Kayıt Hizmeti için URL**: URL'yi şu biçimde belirtin: https://*<server_FQDN>*/certsrv/mscep/mscep.dll. Örneğin, ağ aygıtı kayıt hizmeti 'ni çalıştıran sunucunuzun FQDN 'SI server1.contoso.com ise, yazın `https://server1.contoso.com/certsrv/mscep/mscep.dll` .
         - **Kök CA Sertifikası**: **1. Adım: Ağ Cihazı Kayıt Hizmeti’ni ve bağımlılıkları yükleme ve yapılandırma** aşamasında oluşturduğunuz ve kaydettiğiniz (.cer) dosyasını bulun ve seçin. Bu kök CA sertifikası, sertifika kayıt noktasının Configuration Manager Ilke modülünün kullanacağı istemci kimlik doğrulama sertifikasını doğrulamasına olanak tanır.  

   - **PFX Sertifika Isteklerini işle**' yi seçtiyseniz, seçili sertifika yetkilisi için bağlantı ayrıntılarını ve kimlik bilgilerini yapılandırırsınız.

     - Microsoft 'u sertifika yetkilisi olarak kullanmak için, **Ekle** ' ye tıklayın **ve ardından sertifika yetkilisi ve hesabı ekle** iletişim kutusunda aşağıdakileri belirtin:
         - **Sertifika yetkilisi sunucu adı** -sertifika yetkilisi sunucunuzun adını girin.
         - **Sertifika yetkilisi hesabı** -sertifika yetkilisinde şablonlara Kaydolma izinleri olan hesabı seçmek veya oluşturmak için **Ayarla** ' ya tıklayın.
         - **Sertifika kayıt noktası bağlantı hesabı** -sertifika kayıt noktasını Configuration Manager veritabanına bağlayan hesabı seçin veya oluşturun. Bu şekilde, sertifika kayıt noktasını barındıran bilgisayarın yerel bilgisayar hesabını kullanabilirsiniz.
         - **Active Directory Sertifika Yayımlama hesabı** -bir hesap seçin veya Active Directory Kullanıcı nesnelerine sertifika yayımlamak için kullanılacak yeni bir hesap oluşturun.

         - **Ağ aygıtı kaydı ve kök CA sertifikası** iletişim kutusunda, aşağıdakileri belirtin ve ardından **Tamam**' a tıklayın:  

     - Sertifika yetkilisi olarak Entrust 'ı kullanmak için şunu belirtin:

       - **MDM Web hizmeti URL 'si**
       - URL için Kullanıcı adı ve parola kimlik bilgileri.

         Entrust Web hizmeti URL 'sini tanımlamak için MDM API kullandığınızda, aşağıdaki örnekte gösterildiği gibi API 'nin en az sürüm 9 ' u kullandığınızdan emin olun:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         API 'nin önceki sürümleri, Entrust 'ı desteklemez.

9. **İleri** 'yi tıklatın ve sihirbazı tamamlayın.  

10. Birkaç dakika yüklemenin tamamlanmasını bekleyin ve ardından aşağıdaki yöntemlerin birini kullanarak sertifika kayıt noktasının başarılı bir şekilde yüklendiğini doğrulayın:  

    -   **İzleme** çalışma alanında, **Sistem Durumu**'nu genişletin, **Bileşen Durumu**'na tıklayın ve **SMS_CERTIFICATE_REGISTRATION_POINT** bileşeninden durum mesajlarına bakın.  

    -   Site sistem sunucusunda *<ConfigMgr Yükleme Yolu\>* \Logs\crpsetup.log dosyasını ve *<ConfigMgr Yükleme Yolu\>* \Logs\crpmsi.log dosyasını kullanın. Başarılı bir yükleme, 0 çıkış kodu getirir.  

    -   Bir tarayıcı kullanarak, sertifika kayıt noktasının URL 'sine bağlanabildiğinizi doğrulayın. Örneğin, `https://server1.contoso.com/CMCertificateRegistration`. Uygulama için, bir HTTP 404 tanımlı bir **Sunucu Hatası** sayfası görmeniz gerekir.  

11. Birincil site sunucu bilgisayarında aşağıdaki klasörde, sertifika kayıt noktasının otomatik olarak oluşturduğu kök CA için dışa aktarılan sertifika dosyasını bulun: *<ConfigMgr Yükleme Yolu\>* \inboxes\certmgr.box. Bu dosyayı, daha sonra Configuration Manager Ilke modülünü ağ cihazı kayıt hizmeti 'ni çalıştıran sunucuya yüklediğinizde güvenli bir şekilde erişebileceğiniz güvenli bir konuma kaydedin.  

    > [!TIP]  
    >  Bu sertifika bu klasörde hemen kullanılabilir değildir. Configuration Manager önce bir zaman beklemeniz gerekebilir (örneğin, yarım saat), dosyayı bu konuma kopyalarken.  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>3. adım-Configuration Manager Ilkesi modülünü (yalnızca SCEP sertifikaları için) yükler.

Configuration Manager Ilkesi modülünü, **Adım 2: sertifika kayıt noktasını** , sertifika kayıt noktası özelliklerinde **ağ cihazı kayıt hizmeti için URL** olarak yükleyip yapılandırmak zorundasınız.  

##### <a name="to-install-the-policy-module"></a>İlke Modülünü yüklemek için  

1. Ağ aygıtı kayıt hizmeti 'ni çalıştıran sunucuda, bir etki alanı yöneticisi olarak oturum açın ve aşağıdaki dosyaları Configuration Manager yükleme ortamındaki <Configmgrınstalservıce Media \> \smssetup\polıcymodule\x64 klasöründen klasöründen geçici bir klasöre kopyalayın:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Ek olarak, yükleme medyasında bir LanguacePack klasörünüz varsa, bu klasörü ve içindekileri kopyalayın.  

2. Geçici klasörden, Configuration Manager Ilke modülü Kurulum Sihirbazı 'nı başlatmak için PolicyModuleSetup.exe ' yi çalıştırın.  

3. Sihirbazın ilk sayfasında, **İleri**'ye tıklayın, lisans koşullarını kabul edin ve ardından **İleri**'ye tıklayın.  

4. **Kurulum Klasörü** sayfasında, ilke modülü için varsayılan kurulum klasörünü kabul edin veya alternatif bir klasör belirtin ve ardından **İleri**'ye tıklayın.  

5. **Sertifika Kayıt Noktası** sayfasında, sertifika kayıt noktası için özelliklerde belirtilen sanal uygulama adını ve site sistem sunucusunun FQDN'sini kullanarak sertifika kayıt noktasının URL'sini belirtin. Varsayılan sanal uygulama adı CMCertificateRegistration'dır. Örneğin, site sistem sunucusunun bir server1.contoso.com FQDN 'SI varsa ve varsayılan sanal uygulama adını kullandıysanız, öğesini belirtin `https://server1.contoso.com/CMCertificateRegistration` .

6. **443** varsayılan bağlantı noktasını kabul edin veya sertifika kayıt noktasının kullandığı alternatif bağlantı noktası numarasını belirtin ve ardından **İleri**'ye tıklayın.  

7. **İlke Modülü için İstemci Sertifikası** sayfasında, **1. Adım: Ağ Cihazı Kayıt Hizmeti’ni ve bağımlılıkları yükleme ve yapılandırma** aşamasında dağıttığınız istemci kimlik doğrulama sertifikasını bulun ve belirtin, sonra **İleri**’ye tıklayın.  

8. **Sertifika Kayıt Noktası Sertifikası** sayfasında, **2. Adım: Sertifika kayıt noktasını yükleme ve yapılandırma** aşamasının sonunda bulduğunuz ve kaydettiğiniz kök CA’nın dışa aktarılan sertifika dosyasını seçmek üzere **Gözat**'a tıklayın.  

   > [!NOTE]  
   >  Bu sertifika dosyasını daha önce kaydetmediyseniz, site sunucu bilgisayarında <ConfigMgr Yükleme Yolu\>\inboxes\certmgr.box yolunda bulunur.  

9. **İleri** 'yi tıklatın ve sihirbazı tamamlayın.  

   Configuration Manager Ilkesi modülünü kaldırmak istiyorsanız Denetim Masası 'ndaki **Programlar ve Özellikler** ' i kullanın. 

 
Yapılandırma adımlarını tamamladığınıza göre, sertifika profilleri oluşturup dağıtarak kullanıcılara ve cihazlara sertifika dağıtmaya hazırsınız demektir. Sertifika profillerinin nasıl oluşturulacağı hakkında daha fazla bilgi için bkz. [sertifika profilleri oluşturma](../../protect/deploy-use/create-certificate-profiles.md).