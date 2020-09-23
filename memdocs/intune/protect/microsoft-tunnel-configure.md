---
title: Azure Microsoft Intune için Microsoft tüneli VPN çözümünü yükleyip yapılandırın | Microsoft Docs
description: Linux üzerinde çalışan bir VPN sunucusu olan Microsoft tünel ağ geçidini yükleyip yapılandırın. Microsoft tünele, Intune ile yönettiğiniz bulut tabanlı cihazlar şirket içi altyapınızla iletişime geçebilirler.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c3ed686ff7d3489cb73a992d58aafd041f89df60
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017746"
---
# <a name="configure-microsoft-tunnel-for-intune"></a>Intune için Microsoft tüneli yapılandırma

Bu makale, Microsoft Intune için Microsoft tüneli VPN ağ geçidini yüklemenize yardımcı olabilir. Tünel yazılımını bir Linux sunucusuna yüklersiniz ve ardından Microsoft Endpoint Manager yönetim merkezini kullanarak tüneli altyapınızla kullanılacak şekilde yapılandırabilirsiniz. Ayrıca, Intune VPN profillerini, desteklenen cihazlara tünel yapılandırmasını dağıtmak üzere yapılandırır ve cihazları Microsoft tünel uygulaması ile sağlamalıdır.

*Microsoft tüneli genel önizlemede*.

Microsoft tünel ağ geçidini yüklemek için, şirket içinde veya bulutta çalışan Docker yüklü en az bir Linux sunucusuna ihtiyacınız vardır. Ortamınıza ve altyapınıza bağlı olarak, Azure ExpressRoute gibi ek yapılandırmalara ve yazılımlara gerek duyabilirsiniz.

Yükleme başlamadan önce, aşağıdaki görevleri tamamladığınızdan emin olun:

- [Microsoft tüneli için önkoşulları](../protect/microsoft-tunnel-configure.md)gözden geçirin ve yapılandırın.
- Ortamınızın tünelin kullanımını desteklemeye hazır olduğunu doğrulamak için Microsoft tüneli [Hazırlık Aracı](../protect/microsoft-tunnel-overview.md#run-the-readiness-tool) 'nı çalıştırın.

Ön koşullar hazırlandıktan sonra, tünelyi yüklemeye ve yapılandırmaya başlamak için bu makaleye geri dönün.

Microsoft tüneli 'ni yüklediğinizde, kiracınız için tanımladığınız tünel siteleri hakkında bilgi alır. Bu bilgiler, bu siteler için sunucu yapılandırmasını içerir. Bu nedenle, bir Linux sunucusuna Microsoft tüneli yüklemeden önce en az bir site ve bir sunucu yapılandırması yapılandırmanız gerekir.

## <a name="create-a-server-configuration"></a>Sunucu yapılandırması oluşturma

*Sunucu yapılandırması* kullanımı bir kez yapılandırma ayarlamanıza ve bu yapılandırmanın birden çok sunucu tarafından kullanılmasını sağlar. Yapılandırma IP adresi aralıklarını, DNS sunucularını ve bölünmüş tünel kurallarını içerir. Daha sonra, bu yapılandırmayı bu siteye katılan her sunucuya otomatik olarak uygulayan bir siteye bir sunucu yapılandırması atayacaksınız.

### <a name="to-create-a-server-configuration"></a>Sunucu yapılandırması oluşturmak için

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Kiracı Yönetimi**  >  **Microsoft tünel ağ geçidi**' nde oturum açın  >  *select the* **sunucu yapılandırma** *sekmesini*  >  **Yeni oluştur**' u seçin.

2. **Temel bilgiler** sekmesinde bir *ad* ve *Açıklama* girin *(isteğe bağlı)* ve **İleri**' yi seçin.

3. **Ayarlar** sekmesinde, aşağıdaki öğeleri yapılandırın:
   - **IP adres aralığı**: Bu aralıktaki IP adresleri, tünel ağ geçidine bağlandıklarında cihazlara kiralanır. Örneğin, *169.254.0.0/16*.
   - **DNS sunucuları**: Bu sunucular, bir DNS Isteği tünel ağ geçidine bağlı bir cihazdan geldiğinde kullanılır.
   - **DNS son eki arama** *(isteğe bağlı)*: Bu etki alanı, tünel ağ geçidine bağlandıklarında istemcilere varsayılan etki alanı olarak sağlanır.
   - **Bölünmüş tünel** *(isteğe bağlı)*: adresleri dahil etme veya dışlama. Dahil edilen adresler tünel ağ geçidine yönlendirilir. Dışlanan adresler tünel ağ geçidine yönlendirilmez. Örneğin, 255.255.0.0 * veya *192.168.0.0/16*için bir içerme kuralı yapılandırabilirsiniz.

     Bölünmüş tünel, hem içerme hem de dışlama kuralları arasında toplam 500 kuralı destekler. Örneğin, 300 içerme kurallarını yapılandırırsanız, yalnızca 200 dışlama kuralına sahip olabilirsiniz.

   - **Sunucu bağlantı noktası**: sunucunun bağlantılar için dinlediği bağlantı noktasını girin.

4. **Gözden geçir + oluştur** sekmesinde, yapılandırmayı gözden geçirin ve ardından, kaydetmek için **Oluştur** ' u seçin.

## <a name="create-a-site"></a>Site oluşturma

Siteleri, Microsoft tüneli barındıran sunucuların mantıksal gruplarıdır. Oluşturduğunuz her siteye bir sunucu yapılandırması atarsınız. Bu yapılandırma, siteye katılan her sunucuya uygulanır.

### <a name="to-create-a-site-configuration"></a>Bir site yapılandırması oluşturmak için

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Kiracı Yönetimi**  >  **Microsoft tünel ağ geçidi**' nde oturum açın  >  *select the* **siteler** *sekmesi*  >  **Oluştur**' u seçin.

2. **Site oluştur** bölmesinde, aşağıdaki özellikleri belirtin:

   - **Ad**: Bu site için bir ad girin.
   - **Açıklama** *(isteğe bağlı)*
   - **Genel IP adresi veya FQDN**: tünel kullanan cihazlar için bağlantı noktası olan genel bir IP adresı veya FQDN belirtin. Bu IP adresi tek bir sunucu veya bir yük dengeleme sunucusunun IP veya FQDN 'si olabilir. IP adresi genel olarak yönlendirilebilir olmalıdır ve FQDN ortak DNS 'de çözümlenebilmelidir.
   - **Sunucu yapılandırması**: Bu siteyle ilişkilendirilecek sunucu yapılandırmasını seçmek için açılan listesini kullanın.

3. Siteyi kaydetmek için **Oluştur** ' u seçin.

## <a name="install-microsoft-tunnel-gateway"></a>Microsoft Tunnel Gateway 'i yükler

Bir Linux sunucusuna Microsoft tünel ağ geçidi yüklemeden önce, kiracınızı en az bir [sunucu yapılandırmasıyla](#create-a-server-configuration)yapılandırın ve ardından bir [site](#create-a-site)oluşturun. Daha sonra, bu sunucuya tüneli yüklerken bir sunucunun katılacağı siteyi belirtirsiniz.

### <a name="use-the-script-to-install-microsoft-tunnel"></a>Microsoft tüneli 'ni yüklemek için betiği kullanın

1. Aşağıdaki yöntemlerden birini kullanarak Microsoft tüneli yükleme betiğini indirin:

   - Aracı doğrudan bir Web tarayıcısı kullanarak indirin.  https://aka.ms/microsofttunneldownload **Mstunnel-Setup**dosyasını indirmek için bölümüne gidin.

   - [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Kiracı Yönetimi**  >  **Microsoft tünel ağ geçidi**' nde oturum açın, **sunucular** sekmesini seçin, **Oluştur** ' u seçerek *sunucu oluştur* bölmesini açın ve ardından **betiği indir**' i seçin.

     ![Yükleme betiğini indirmek için ekran yakalama](./media/microsoft-tunnel-configure/download-installation-script.png)

   - Hazırlık aracını doğrudan almak için bir Linux komutu kullanın. Örneğin, tüneli yükleyeceğiniz sunucuda, bağlantıyı açmak için **wget** veya **kıvrık** kullanabilirsiniz https://aka.ms/microsofttunneldownload .

2. Sunucu yüklemeyi başlatmak için betiği aşağıdaki komut satırıyla **kök** olarak çalıştırın: `./mstunnel-setup`

   > [!TIP]  
   > Yükleme ve betiği durdurursanız, komut satırını yeniden çalıştırarak yeniden başlatabilirsiniz. Yükleme kaldığınız yerden devam ediyor.

   Betiği başlattığınızda, Docker 'dan kapsayıcı görüntülerini indirir ve sunucuda gerekli klasörleri ve dosyaları oluşturur.

   Kurulum sırasında betik birkaç yönetici görevini tamamlamanızı ister.

3. Komut dosyası tarafından istendiğinde, lisans sözleşmesini (EULA) kabul edin.

4. Ortamınızı desteklemek için aşağıdaki dosyalardaki değişkenleri gözden geçirin ve yapılandırın.

   - Ortam dosyası: **/etc/mstunnel/env.sh**. Bu değişkenler hakkında daha fazla bilgi için bkz. Microsoft tüneli başvurusu makalesindeki [ortam değişkenleri](../protect/microsoft-tunnel-reference.md#environment-variables) .

5. İstendiğinde, TLS sertifika dosyanızın tam zincirini Linux sunucusuna kopyalayın. Betik, Linux sunucusunda kullanılacak doğru konumu görüntüler.

   TLS sertifikası, tüneli kullanan cihazlar ve tünel ağ geçidi uç noktası arasındaki bağlantıyı korur. Sertifika, SAN ağ geçidi sunucusunun IP adresini veya FQDN 'sini SAN 'da içermelidir.

   Özel anahtar, TLS sertifikası için sertifika imzalama isteğini oluşturduğunuz makinede kullanılabilir olmaya devam edecektir. Bu dosya, bir **site. Key**adıyla birlikte verilmelidir.

   TLS sertifikasını ve özel anahtarı yükler. Dosya biçiminizdeki ile eşleşen aşağıdaki kılavuzu kullanın:

   - **PFX**:
     - Sertifika dosyası adı, **site. pfx**olmalıdır. Sertifika dosyasını **/etc/mstunnel/Private/site.pfx**'e kopyalayın.

   - **Pey**:
     - Tam zincir (kök, ara, son varlık), **site. CRT**adlı tek bir dosyada olmalıdır. DigiCert gibi bir genel sağlayıcı tarafından verilen bir sertifika kullanıyorsanız, tüm zinciri tek bir. pem dosyası olarak indirme seçeneğiniz vardır.

     - Sertifika dosyası adı **site. CRT*olmalıdır. Tam zincir sertifikasını **/etc/mstunnel/certs/site.CRT**'e kopyalayın. Örnek: `cp [full path to cert] /etc/mstunnel/certs/site.crt`

       Alternatif olarak, **/etc/mstunnel/certs/site.CRT**içinde tam zincir sertifikaya bir bağlantı oluşturun. Örnek: `ln -s [full path to cert] /etc/mstunnel/certs/site.crt`

     - Özel anahtar dosyasını **/etc/mstunnel/Private/site.Key**'e kopyalayın. Örnek: `cp [full path to key] /etc/mstunnel/private/site.key`

       Alternatif olarak, **/etc/mstunnel/Private/site.Key**' de özel anahtar dosyasına bir bağlantı oluşturun. Örneğin: `ln -s [full path to key file] /etc/mstunnel/private/site.key` Bu anahtar bir parolayla şifrelenmemelidir. Özel anahtar dosya adı, **site. Key**olmalıdır.

6. Kurulum sertifikayı yükledikten ve tünel ağ geçidi Hizmetleri oluşturduktan sonra, oturum açmanız ve Intune ile kimlik doğrulamanız istenir. Kullanıcı hesabının, Intune Yöneticisi veya genel yönetici rollerine atanmış olması gerekir. Kimlik doğrulamasını gerçekleştirmek için kullandığınız hesabın bir Intune lisansı olmalıdır veya yönetici hesaplarının lisanslamayı gerektiren gereksinimi kapatmanız gerekir. Bu hesabın kimlik bilgileri kaydedilmez ve yalnızca ilk oturum açma Azure Active Directory için kullanılır. Başarılı kimlik doğrulamasından sonra, Azure Uygulama kimlikleri/gizli anahtarları, tünel ağ geçidi ve Azure Active Directory arasında kimlik doğrulaması için kullanılır.

   > [!TIP]  
   > Yönetici lisanslarının gereksinimini devre dışı bırakmak için, Microsoft Endpoint Manager Yönetim Merkezi ' nde **kiracı yönetim**  >  **rolleri**  >  **yönetici lisansı** ' na gidin ve yönetici lisansını devre dışı bırakın.

   Bu kimlik doğrulaması, tünel ağ geçidini Microsoft Endpoint Manager ve Intune kiracınız ile kaydeder.

   1. Bir Web tarayıcısından. öğesine gidin https://Microsoft.com/devicelogin ve yükleme betiği tarafından belirtilen cihaz kodunu girip Intune yönetici kimlik bilgilerinizle oturum açın.

   2. Microsoft tünel ağ geçidi Intune 'a kaydolduktan sonra, betik, Intune 'dan siteleriniz ve sunucu Yapılandırmalarınızla ilgili bilgileri alır. Betik daha sonra bu sunucunun katılması istediğiniz tünel sitesinin GUID 'sini girmenizi ister. Betik size kullanılabilir sitelerinizin bir listesini sunar.

   3. Bir site seçtikten sonra, kurulum bu site için sunucu yapılandırmasını çeker ve Microsoft tüneli yüklemesini tamamlaması için yeni sunucunuza uygular.

7. Yükleme komut dosyası tamamlandıktan sonra, tünelin üst düzey durumunu görüntülemek için Microsoft Endpoint Manager Yönetim Merkezi ' nde **Microsoft tüneli ağ geçidi** sekmesine gidebilirsiniz. Ayrıca, sunucunun çevrimiçi olduğunu onaylamak için **sistem** durumu sekmesini de açabilirsiniz.

## <a name="deploy-the-microsoft-tunnel-app"></a>Microsoft tünel uygulamasını dağıtma

Microsoft tünelini kullanmak için cihazların Microsoft tünel uygulamasına erişmesi gerekir. Uygulamayı kullanıcılara atayarak cihazlara dağıtabilirsiniz. Aşağıdaki uygulamalar mevcuttur:

- Android için, **Microsoft tünel** uygulamasını **Google Play** deposundan indirin. Bkz. Microsoft Intune Android Mağazası uygulamaları ekleme.
- İOS/ıpados için, Apple **App Store**'Dan **Microsoft tünel** uygulamasını indirin. Bkz. Microsoft Intune iOS Mağazası uygulamaları ekleme.

Intune ile uygulama dağıtma hakkında daha fazla bilgi için bkz. Microsoft Intune uygulama ekleme.

## <a name="create-a-vpn-profile"></a>VPN profili oluşturma

Microsoft tüneli bir sunucuya yüklendikten ve cihazlar Microsoft tünel uygulamasını yüklediğinden, cihazları tünelyi kullanacak şekilde yönlendirmek için VPN profilleri dağıtabilirsiniz. Bunu yapmak için, Microsoft tüneli bağlantı türü ile VPN profilleri oluşturacaksınız.

### <a name="android"></a>Android

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **yapılandırma profilleri**  >  **profil oluşturma**' da oturum açın.

2. *Platform*Için **Android Enterprise**' ı seçin ve ardından *profil* ' den yalnızca *cihaz sahibi* veya *iş profili*için ' den **VPN** ' yi seçin ve ardından **Oluştur**' u seçin.

3. **Temel bilgiler** sekmesinde bir *ad* ve *Açıklama* girin *(isteğe bağlı)* ve **İleri**' yi seçin.

4. *Bağlantı türü* Için **Microsoft tüneli**' ni seçin ve ardından aşağıdaki ayrıntıları yapılandırın:
   - **Taban VPN**:  
     - *Bağlantı adı*için kullanıcılara görüntülenecek bir ad belirtin.
     - *Microsoft tünel sitesi*IÇIN bu VPN profilinin kullanacağı tünel sitesini seçin.
   - **Uygulama BAŞıNA VPN**:  
     - Uygulama başına VPN profilinde atanan uygulamalar, tünele uygulama trafiği gönderir.
     - Uygulama başına VPN 'i etkinleştirmek için **Ekle** ' yi seçin ve ardından Intune 'a aktardığınız uygulamalara gidin. Bunlar özel veya genel uygulamalar olabilir.
   - **Her zaman VPN**:  
     - *Her zaman açık VPN*için VPN istemcisini otomatik olarak bağlanıp VPN 'ye yeniden bağlanacak şekilde ayarlamak için *Etkinleştir* ' i seçin. Her zaman açık VPN bağlantıları bağlı kalır. Uygulama başına VPN etkinse, yalnızca seçtiğiniz uygulamalardan gelen trafik tünelden geçer.
   - **Proxy**:  
     - Ortamınız için proxy sunucusu ayrıntılarını yapılandırın.  

   VPN ayarları hakkında daha fazla bilgi için bkz. [VPN yapılandırmak Için Android kurumsal cihaz ayarları](../configuration/vpn-settings-android-enterprise.md)

5. **Atamalar** sekmesinde, bu profili alacak grupları yapılandırın.

6. **Gözden geçir + oluştur** sekmesinde, yapılandırmayı gözden geçirin ve ardından, kaydetmek için **Oluştur** ' u seçin.

### <a name="ios"></a>iOS

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **cihaz yapılandırması**  >  **profil oluşturma**' da oturum açın.

2. *Platform*için **IOS/ıpados**' ı seçin ve ardından *profil* için **VPN**' i seçin ve ardından **oluşturun**.

3. **Temel bilgiler** sekmesinde bir *ad* ve *Açıklama* girin *(isteğe bağlı)* ve **İleri**' yi seçin.

4. *Bağlantı türü* Için **Microsoft tüneli**' ni seçin ve ardından aşağıdaki öğeleri yapılandırın:
   - **Taban VPN**:  
     - *Bağlantı adı*için kullanıcılara görüntülenecek bir ad belirtin.
     - *Microsoft tünel sitesi*IÇIN bu VPN profilinin kullanacağı tünel sitesini seçin.  
   - **Uygulama BAŞıNA VPN**:  
     - Uygulama başına VPN 'i etkinleştirmek için **Etkinleştir**' i seçin. İOS uygulama başına VPN 'Ler için ek yapılandırma adımları gereklidir. Daha fazla bilgi için bkz. [iOS Için uygulama BAŞıNA VPN/ıpados](../configuration/vpn-setting-configure-per-app.md).
     - **Proxy**:  
       - Ortamınız için proxy sunucusu ayrıntılarını yapılandırın.  

## <a name="upgrade-microsoft-tunnel"></a>Microsoft tüneli 'ni yükselt

Microsoft tünele ilgili güncelleştirmeler olduğunda, yüklü Microsoft Tünellerinizin yükseltilmesi, sıralı bir yükseltmede Intune tarafından otomatik olarak yönetilir:

- Intune, bir sitedeki Microsoft tünel sunucularını aynı anda bir sunucuda yükseltir.

- Bir sunucunun başarılı bir şekilde yükseltilmesiyle, Intune sonraki sunucunun yükseltilmeye başlamadan önce kısa bir süre bekler.

- Bu işlem, bir sitedeki tüm sunucular yeni sürüme güncelleştirilene kadar devam eder.

## <a name="uninstall-the-microsoft-tunnel"></a>Microsoft tüneli 'ni kaldırma

Ürünü kaldırmak için Linux sunucusundan **./MST-cli Uninstall** 'ı kök olarak çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar

[Microsoft tüneli izleme](microsoft-tunnel-monitor.md)
