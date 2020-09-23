---
title: Microsoft Intune-Azure için Microsoft tünel VPN çözümünü kullanma | Microsoft Docs
description: Linux üzerinde çalışan Intune için bir VPN sunucusu olan Microsoft tünel ağ geçidi hakkında bilgi edinin. Intune ile yönettiğiniz bulut tabanlı cihazlar, Microsoft tüneli ile şirket içi altyapınızla iletişime geçebilirler.
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
ms.openlocfilehash: b77b9aea2fae8173389d3e660744fbb32424a89b
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017749"
---
# <a name="microsoft-tunnel-for-microsoft-intune"></a>Microsoft Intune için Microsoft tüneli

Microsoft tüneli Microsoft Intune için bir VPN Gateway çözümüdür. Tünel, modern kimlik doğrulama ve koşullu erişim kullanan iOS/ıpados ve Android kurumsal cihazlarından şirket içi kaynaklara erişim sağlar. Bu makalede, kullanım önkoşulları ve mimarinin mimarisi dahil olmak üzere tünelin nasıl çalıştığı açıklanmaktadır.

*Microsoft tüneli genel önizlemede*.

Önkoşul yapılandırmalarınız varsa ve tüneli yüklemeye hazırsanız, bkz. [Microsoft tüneli yapılandırma](../protect/microsoft-tunnel-configure.md).

## <a name="overview-of-microsoft-tunnel"></a>Microsoft tüneli 'ne genel bakış

Microsoft Tunnel Gateway, Linux sunucusu üzerinde çalışan bir Docker kapsayıcısına yüklenir. Linux sunucusu, şirket içi ortamınızda veya şirket içinde veya bulutta çalışan bir sanal makinede bulunan fiziksel bir kutu olabilir. Tünel yüklendikten sonra, cihazlarınızı şirket ağınıza ve kaynaklarınıza yönelik bağlantılara tünel kullanacak şekilde yönlendirmek için iOS veya Android için Intune VPN profillerini kullanırsınız. Tünel bulutta barındırıldığı zaman, şirket içi ağınızı buluta genişletmek için Azure ExpressRoute gibi bir çözüm kullanmanız gerekir.

Microsoft Endpoint Manager Yönetim Merkezi aracılığıyla şunları yapabilirsiniz:

- Linux sunucularında çalıştıracağınız Microsoft tüneli yükleme betiğini indirin.
- IP adresleri, DNS sunucuları ve bağlantı noktaları gibi Microsoft Tunnel Gateway 'in yönlerini yapılandırın.
- VPN profillerini, tünelini kullanmaya yönlendirmek için cihazlara dağıtın.
- Microsoft tünel uygulamalarını cihazlarınıza dağıtın.

Microsoft tünel uygulaması, iOS/ıpados ve Android Kurumsal cihazları aracılığıyla:

- Tünele kimlik doğrulamak için Azure Active Directory (Azure AD) kullanın.
- , Koşullu erişim ilkelerinize göre değerlendirilir. Cihaz uyumlu değilse, VPN sunucunuza veya şirket içi ağınıza erişemez.

Bir tüneme bağlanmak için, cihazlar iOS/ıpados veya Android uygulama mağazalarından erişilebilen Microsoft Tunnel uygulamasını kullanır.

Microsoft tüneli desteklemek için birden çok Linux sunucusu yükleyebilir ve sunucuları *siteler*adlı mantıksal gruplar halinde birleştirebilirsiniz. Her sunucu tek bir siteye katılabilir. Bir siteyi yapılandırırken, cihazların tünele erişirken kullanması için bir bağlantı noktası tanımlamanız gerekir. Siteleri tanımladığınız ve siteye atayacağınız bir *sunucu yapılandırması* gerektirir. Sunucu yapılandırması, bu siteye eklediğiniz her sunucuya uygulanır ve ek sunucu yapılandırmalarını basitleştirir.

Cihazları tüneli kullanmak üzere yönlendirmek için, Microsoft tüneli için bir VPN ilkesi oluşturup dağıtabilirsiniz. Bu ilke, bağlantı türü için Microsoft tüneli kullanan bir cihaz yapılandırması VPN profilidir.

Tünel için VPN profillerinin özellikleri şunlardır:

- Son kullanıcılarınızın göreceği VPN bağlantısı için kolay bir ad.
- VPN istemcisinin bağlandığı site.
- VPN profilinin hangi uygulamalara kullanıldığını ve her zaman açık olup olmadığını tanımlayan uygulama başına VPN yapılandırması. Her zaman açık olduğunda VPN otomatik olarak bağlanır ve yalnızca tanımladığınız uygulamalar için kullanılır. Hiçbir uygulama tanımlanmamışsa, her zaman açık bağlantı cihazdan tüm ağ trafiği için tünel erişimi sağlar.
- Kullanıcı VPN 'yi başlattığında ve *Connect*' i seçtiğinde Tünelle el ile bağlantı.
- Proxy desteği (iOS/ıpados, Android 10 +)

Sunucu yapılandırmalarına şunlar dahildir:

- IP adres aralığı: bir Microsoft tünelini bağlayan cihazlara atanan IP adresleri.
- DNS sunucuları: DNS sunucusu cihazların sunucuya bağlandıklarında kullanması gerekir.
- DNS son eki arama.
- Ayırma ve dışlama rotalarında paylaşılan en fazla 500 kurala kadar ayrılmış tünel kuralları. Örneğin, 300 ekleme kuralları oluşturursanız, en fazla 200 dışlama kuralı kullanabilirsiniz.
- Port: Microsoft tüneli ağ geçidinin dinlediği bağlantı noktası.

Site yapılandırması şunları içerir:

- Tüneli kullanan cihazlar için bağlantı noktası olan genel bir IP adresi veya FQDN. Bu adres, tek bir sunucu veya bir yük dengeleme sunucusunun IP veya FQDN 'si için olabilir.
- Sitedeki her sunucuya uygulanan sunucu yapılandırması.

Linux sunucusuna tünel yazılımını yüklerken bir siteye sunucu atarsınız. Yükleme, Yönetim Merkezi içinden indirebileceğiniz bir betiği kullanır. Betiği başlattıktan sonra, sunucunun katılabileceği siteyi belirtmeyi de içeren, ortamınız için işlemini yapılandırmanız istenir.

Microsoft tünelini kullanmak için cihazların Microsoft tünel uygulamasını yüklemeleri gerekir. Uygulamayı iOS/ıpados veya Android uygulama mağazalarından alır ve kullanıcılara dağıtırsınız.

## <a name="configure-prerequisites-for-microsoft-tunnel"></a>Microsoft tüneli için önkoşulları yapılandırma

Aşağıdaki bölümlerde, tünel yazılımını ve ağınızı barındıran Linux sunucusu için Önkoşullar ayrıntılı olarak verilmiştir.  

> [!NOTE]
> Microsoft tüneli, Azure Kamu bulut ortamlarında desteklenmez.

### <a name="linux-server"></a>Linux sunucusu

Linux tabanlı bir sanal makine veya Microsoft Tunnel Gateway 'in yükleneceği bir fiziksel sunucu ayarlayın.

- **Linux dağıtımı** -aşağıdakiler desteklenir:

  - CentOS 7.4 + (CentOS 8 + desteklenmez)
  - Red Hat (RHEL) 7.4 + (RHEL 8 + desteklenmez)
  - Ubuntu 18.04
  - Ubuntu 20.04

- **Linux sunucusunu Boyutlandır**: beklenen kullanımı karşılamak için aşağıdaki kılavuzu kullanın:

  |Cihaz sayısı | CPU sayısı | Bellek (GB) | Sunucu sayısı | # Siteler | Disk alanı GB |
  |----------|--------|-----------|-----------|---------|---------------|
  | 1.000    | 4      | 4         | 1         | 1       | 30            |
  | 2.000    | 4      | 4         | 1         | 1       | 30            |
  | 5.000    | 8      | 8         | 2         | 1       | 30            |
  | 10,000   | 8      | 8         | 3         | 1       | 30            |
  | 20.000   | 8      | 8         | 4         | 1       | 30            |
  | 40,000   | 8      | 8         | 8         | 1       | 30            |

  Destek, doğrusal ölçeği ölçeklendirir. Her Microsoft tüneli en fazla 64.000 eşzamanlı bağlantıyı destekleirken, tek tek cihazlar birden çok bağlantı açabilir.

- **CPU**: 64-bit AMD/Intel işlemcisi.

- **Docker 'ı yükler**: Docker sürüm 19,03 CE veya üstünü yükler.

  Microsoft tüneli, kapsayıcılar için destek sağlamak üzere Linux sunucusunda Docker gerektirir. Kapsayıcılar tutarlı bir yürütme ortamı, sistem durumu izleme ve proaktif düzeltme ve temiz bir yükseltme deneyimi sağlar.

  Docker 'ı yükleme ve yapılandırma hakkında daha fazla bilgi için bkz.:

  - [CentOS 'a Docker altyapısını yükler]( https://docs.docker.com/engine/install/centos/)
  - [Red Hat Enterprise Linux 7 ' de Docker kullanma](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.0_release_notes/sect-red_hat_enterprise_linux-7.0_release_notes-linux_containers_with_docker_format-using_docker)
  - [Ubuntu 'da Docker altyapısını kurma](https://docs.docker.com/engine/install/ubuntu/)

- **Aktarım Katmanı Güvenliği (TLS) sertifikası**: Linux sunucusu, cihazlar ve tünel ağ geçidi sunucusu arasındaki bağlantıyı güvenli hale getirmek için GÜVENILEN bir TLS sertifikası gerektirir. Tünel ağ geçidinin yüklenmesi sırasında, tam güvenilir sertifika zinciri dahil olmak üzere TLS sertifikasını sunucuya ekleyeceksiniz.

  - Tünel ağ geçidi uç noktasının güvenliğini sağlamak için kullanılan TLS sertifikası, SAN 'da tünel ağ geçidi sunucusunun IP adresini veya FQDN 'sini içermelidir.

  - TLS sertifikası iki yıldan daha uzun bir süre sonu tarihine sahip olamaz. Tarih iki yıldan uzunsa iOS cihazlarında kabul edilmez.

  - Joker karakter kullanımı, sınırlı desteğe sahiptir. Örneğin, ** \* . contoso.com** desteklenir. **cont \* . com** desteklenmez.

  - Tünel ağ geçidi sunucusunun yüklenmesi sırasında, tüm güvenilen sertifika zincirini Linux sunucunuza kopyalamanız gerekir. Yükleme betiği, sertifika dosyalarını kopyaladığınız konumu sağlar ve bunu yapmanızı ister.

  - Genel olarak güvenilen olmayan bir TLS sertifikası kullanıyorsanız, bir Intune *güvenilir sertifika* profili kullanarak tüm güven zincirinin cihazlara gönderim yapmanız gerekir.

  - TLS sertifikası **ped** veya **PFX** biçiminde olabilir.

### <a name="network"></a>Ağ

Performansı artırmak için Linux sunucusu başına iki ağ arabirim denetleyicisi (NIC) kullanmanızı öneririz, ancak iki kullanımı isteğe bağlıdır.

- **NIC 1** -bu NIC yönetilen cihazlarınızdan gelen trafiği işler ve genel IP adresine sahip ortak bir ağda olmalıdır.Bu IP adresi, *site yapılandırmasında*yapılandırdığınız adresidir. Bu adres tek bir sunucuyu veya yük dengeleyiciyi temsil edebilir.

- **NIC 2** -bu NIC, şirket içi kaynaklarınız için trafiği işler ve ağ kesimlemesi olmadan özel iç ağınızda olmalıdır.

Linux 'u bir bulutta VM olarak çalıştırırsanız, sunucunun şirket içi ağınıza erişebildiğinden emin olmanız gerekir. Örneğin, VM 'niz Azure 'da çalışıyorsa, [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 'u veya erişim sağlamak için benzer bir ad kullanabilirsiniz. Sunucuyu şirket içi bir VM 'de çalıştırırsanız ExpressRoute gerekli değildir.

Yük dengeleyici eklemeyi seçerseniz, yapılandırma ayrıntıları için satıcınızın belgelerine başvurun. Intune ve Microsoft tünele ilgili ağ trafiğini ve güvenlik duvarı bağlantı noktalarını dikkate alın.

### <a name="firewall"></a>Güvenlik Duvarı

Varsayılan olarak, Microsoft tüneli ve sunucusu aşağıdaki bağlantı noktalarını kullanır:

**Gelen bağlantı noktaları**:

- TCP 443 – Microsoft tüneli için gereklidir.
- UDP 443 – Microsoft tüneli için gereklidir.
- TCP 22 – Isteğe bağlı. Linux sunucusuna SSH/SCP için kullanılır.

**Giden bağlantı noktaları**:

- TCP 443 – Intune hizmetlerine erişmek için gereklidir. Docker 'ın görüntüleri çekmek için gereklidir.
- TCP – 80 – Intune hizmetlerine erişmek için gereklidir.

Tünel için bir sunucu yapılandırması oluşturduğunuzda, varsayılan 443 olan farklı bir bağlantı noktası belirtebilirsiniz. Farklı bir bağlantı noktası belirtirseniz, yapılandırmanızı desteklemek için güvenlik duvarlarını yapılandırmayı unutmayın.

**Ek gereksinimler**:

- Tünel, yukarıda belirtildiği gibi, TCP 22 bağlantı noktası eklenmesiyle aynı gereksinimleri [Microsoft Intune Için ağ uç noktaları](../fundamentals/intune-endpoints.md)ile paylaşır.

- Güvenlik duvarı kurallarını,  [Microsoft Container Registry (MCR) Istemci güvenlik duvarı kuralları yapılandırmasında](https://github.com/microsoft/containerregistry/blob/master/client-firewall-rules.md)ayrıntılı olarak açıklanan yapılandırmaları destekleyecek şekilde yapılandırın.

### <a name="proxy"></a>Ara sunucu

Microsoft tünele bir ara sunucu kullanabilirsiniz. Aşağıdaki noktalar, Linux sunucusunu ve ortamınızı başarılı olarak yapılandırmanıza yardımcı olabilir:

- İç ara sunucu kullanıyorsanız, Linux konağını, ortam değişkenlerini kullanarak Proxy sunucunuzu kullanacak şekilde yapılandırmanız gerekebilir. Değişkenleri kullanmak için, Linux sunucusundaki **/etc/ortam** dosyasını düzenleyin ve aşağıdaki satırları ekleyin:

  `http_proxy=[address]`  
  `https_proxy=[address]`

- Kimliği doğrulanmış proxy 'ler desteklenmez.

- Ara sunucu kesme ve İnceleme gerçekleştiremez. Bunun nedeni, Linux sunucusunun Intune 'a bağlanırken TLS karşılıklı kimlik doğrulaması kullanmadır.

- Görüntü çekmek için, Docker 'ı proxy 'yi kullanacak şekilde yapılandırın. Bunu yapmak için, Linux sunucusundaki **/etc/systemd/System/Docker.exe** dosyasını düzenleyin ve aşağıdaki satırları ekleyin:

  ```
  [Service]
  Environment="HTTP_PROXY=http://your.proxy:8080/"
  Environment="HTTPS_PROXY=http://your.proxy:8080/"
  Environment="NO_PROXY=127.0.0.1,localhost
  ```

  > [!NOTE]  
  > Microsoft tüneli Azure AD Uygulaması Proxy veya benzer proxy çözümlerini desteklemez.

### <a name="platforms"></a>Platformlar

Yalnızca Intune 'a kayıtlı cihazlar Microsoft tüneli ile desteklenir. Aşağıdaki cihaz platformları desteklenir:

- Android Enterprise (tam olarak yönetilen, şirkete ait Iş profili, Iş profili)
- iOS/iPadOS

Aşağıdaki işlev tüm platformlar tarafından desteklenir:

- Kullanıcı adı ve parola ya da sertifikalar kullanarak tünele Azure Active Directory (Azure AD) kimlik doğrulaması.
- Uygulama başına destek.
- Kullanıcının VPN 'yi başlattığında ve *Bağlan*' ı seçtiği bir tünel uygulaması aracılığıyla el ile tam cihaz tüneli.
- Bölünmüş tünel. Ancak, VPN profiliniz *uygulama BAŞıNA VPN*kullanıyorsa, iOS bölünmüş tünel kuralları üzerinde yok sayılır.

Bir ara sunucu desteği aşağıdaki platformlarla sınırlıdır:

- Android 10 ve üzeri
- iOS/iPadOS

## <a name="run-the-readiness-tool"></a>Hazırlık aracını çalıştırma

Bir sunucu yüklemesine başlamadan önce, **MST hazırlığı** aracını indirmeniz ve çalıştırmanız önerilir. Araç, Linux sunucunuzda çalışan ve aşağıdaki eylemleri yapan bir betiktir:

- Ağ yapılandırmanızın Microsoft tünelinin gerekli Microsoft uç noktalarına erişmesine izin verdiğini onaylar.  
- Microsoft tüneli 'ni yüklemek için kullanacağınız Azure Active Directory (Azure AD) hesabının, kaydı tamamlamaya yönelik gerekli rollere sahip olduğunu doğrular. 

MST hazırlığı Aracı, **JQ**'nin bir Command-Lie JSON işlemcisi olan bir bağımlılığı vardır. Hazırlık aracını çalıştırmadan önce **JQ** 'nin yüklü olduğundan emin olun. **JQ**'nin nasıl alınacağı ve yükleneceği hakkında daha fazla bilgi için, kullandığınız Linux sürümüne yönelik belgelere bakın.

Hazırlık aracını kullanmak için:

1. Aşağıdaki yöntemlerden birini kullanarak Hazırlık aracını alın:
   - Aracı doğrudan bir Web tarayıcısı kullanarak indirin.  https://aka.ms/microsofttunnelready **MST hazırlığı**adlı bir dosyayı indirmek için bölümüne gidin.
   - [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **Kiracı Yönetimi**  >  **Microsoft tünel ağ geçidi**' nde oturum açın, **sunucular** sekmesini seçin, **Oluştur** ' u seçerek *sunucu oluştur* bölmesini açın ve ardından **hazırlık hazırlığı aracını**seçin.  
   - Hazırlık aracını doğrudan almak için bir Linux komutu kullanın. Örneğin, bağlantıyı açmak için **wget** veya **kıvrı** kullanabilirsiniz https://aka.ms/microsofttunnelready .

   Bu betiği, yüklemeyi planladığınız sunucuyla aynı ağ üzerinde bulunan herhangi bir Linux sunucusundan çalıştırabilir, ağ yöneticilerinin bunu çalıştırmasına ve ağ sorunlarını bağımsız olarak gidermenize izin verebilirsiniz.

2. Ağ yapılandırmanızı doğrulamak için betiği **kök** olarak çalıştırın ve aşağıdaki komut satırını kullanın: `./mst-readiness network`

   Betik aşağıdaki eylemleri, her ikisi için de başarı veya hata raporlarını çalıştırır:
   - Tünelin kullanacağı her bir Microsoft uç noktasına bağlanmaya çalışır.
   - Güvenlik duvarınızdaki gerekli bağlantı noktalarının açık olup olmadığını denetler.

3. Microsoft tüneli 'ni yüklemek için kullanacağınız hesabın, kaydı tamamlamaya yönelik gerekli roller ve izinlere sahip olduğunu doğrulamak için, komut dosyasını aşağıdaki komut satırıyla çalıştırın: `./mst-readiness account`

   Betik, Azure AD 'de ve Intune 'da kimlik doğrulaması yapmak için kullandığınız bir Web tarayıcısı ile farklı bir makine kullanmanızı ister. Araç başarı veya hata bildirir.

Bu araç hakkında daha fazla bilgi için bkz. Microsoft tüneli için başvuru makalesinde [MST-CLI başvurusu](../protect/microsoft-tunnel-reference.md#mst-cli-command-line-tool-for-microsoft-tunnel-gateway) .

## <a name="use-conditional-access-with-the-microsoft-tunnel"></a>Microsoft tüneli ile koşullu erişim kullanma

Intune ile koşullu erişim kullandığınızda, cihaz erişimini Microsoft tünel ağ geçidine bağlamak için ilkeler oluşturabilirsiniz.

### <a name="provision-your-tenant"></a>Kiracınızı sağlayın

Tünel için koşullu erişim ilkelerini yapılandırmadan önce, kiracınızı koşullu erişim için Microsoft tünelini destekleyecek şekilde etkinleştirmeniz gerekir. Kiracınızı etkinleştirmek için kiracınızı değiştiren bir PowerShell betiği çalıştırarak, daha sonra koşullu erişim ilkesinin bir parçası olarak seçebileceğiniz bir bulut uygulaması olarak **Microsoft tünel ağ geçidini** ekleyebilirsiniz.  Bu işlem, Azure Active Directory PowerShell modülünün kullanılmasını gerektirir.

1. **Azuread PowerShell modülünü** [indirip yükleyin](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0&preserve-view=true) .

2. **mst-CA-provisioning.ps1** adlı PowerShell betiğini **aka.MS/MST-CA-provisioning**adresinden indirin.

3. Azure rolü izinleri olan kimlik bilgilerini [ **uygulama yöneticisine**eşdeğer](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#application-administrator-permissions)olarak kullanarak kiracınızı sağlamak için ortamınızdaki herhangi bir konumdan betiği çalıştırın. Betik, aşağıdaki ayrıntılarla bir hizmet ilkesi oluşturarak kiracınızı değiştirir:

   - Uygulama KIMLIĞI: 3678c9e9-9681-447A-974d-d19f668fcd88
   - Ad: Microsoft tünel ağ geçidi

   Koşullu erişim ilkelerini yapılandırırken tünel bulutu uygulamasını seçebilmeniz için bu hizmet ilkesinin eklenmesi gereklidir. Ayrıca, kiracınıza hizmet ilkesi bilgilerini eklemek için Graf kullanılması mümkündür.  
4. Betik tamamlandıktan sonra, normal işleminizi kullanarak koşullu erişim ilkeleri oluşturabilirsiniz.

Koşullu erişim ilkeleri oluşturmak için bkz. [cihaz tabanlı koşullu erişim Ilkesi oluşturma](../protect/create-conditional-access-intune.md).

### <a name="create-conditional-access-policy-to-limit-access-to-microsoft-tunnel"></a>Microsoft tünele erişimi sınırlandırmak için koşullu erişim ilkesi oluşturma

Koşullu erişim ilkesini Kullanıcı erişimini sınırlamak üzere yapılandırmayı seçerseniz, kiracınızı Microsoft tünel ağ geçidi bulutu uygulamasını destekleyecek şekilde hazırladıktan sonra, ancak tünel ağ geçidini yüklemeden önce Bu ilkeyi yapılandırmanızı öneririz.

1. [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **uç nokta güvenlik**  >  **koşullu erişim**  >  **Yeni ilke**' de oturum açın.
2. Bu kural için bir ad belirtin.
3. Kullanıcı ve grup erişimini yapılandırmak için *atamalar*altında **Kullanıcılar ve gruplar**' ı seçin.
   1. **Include**  >  **Tüm kullanıcıları**içer ' i seçin.  
   2. Sonra, **hariç tut** ' u seçin ve *erişim vermek*istediğiniz grupları yapılandırın ve ardından Kullanıcı ve grup yapılandırmasını kaydedin.
4. *Erişim denetimleri*altında, **izin ver**' i seçin, **erişimi engelle**' yi seçin ve ardından yapılandırmayı kaydedin.  
5. **İlkeyi etkinleştir**’i **Açık** duruma getirin.
6. **Oluştur**’u seçin.

## <a name="architecture"></a>Mimari

Microsoft tünel ağ geçidi, Linux sunucularında çalışan Docker kapsayıcılarında çalışır.  

![Microsoft Tunnel Gateway mimarisinin çizimi](./media/microsoft-tunnel-overview/tunnel-architecture.png)
  
**Bileşenler**:  
- **A** – Microsoft Intune.
- **B**-Azure ACTIVE DIRECTORY (ad).
- **C** – Docker ile Linux sunucusu.
  - **CI** -Microsoft tünel ağ geçidi.
  - **Cii** – Yönetim Aracısı.
  - **Cııı** – kimlik doğrulama eklentisi – Azure AD ile kimlik doğrulaması yapan yetkilendirme eklentisi.
- **D** – genel kullanıma açık IP veya Microsoft TÜNELININ FQDN 'si. Bu, bir yük dengeleyiciyi temsil edebilir.
- **E** – mobil cihaz YÖNETIMI (MDM) kayıtlı cihaz.
- **F** – güvenlik duvarı
- **G** – Iç proxy sunucusu (isteğe bağlı).
- **H** – kurumsal ağ.
- **I** – genel internet.

**Eylemler**:  
- **1** -Intune Yöneticisi *sunucu yapılandırma* ve *sitelerini*yapılandırır, sunucu konfigürasyonları sitelerle ilişkilendirilir.
- **2** -Intune Yöneticisi Microsoft tünel ağ geçidini yüklüyor ve kimlik doğrulama eklentisi, Microsoft tünel ağ geçidinin KIMLIĞINI Azure AD ile doğrular. Microsoft tünel ağ geçidi sunucusu bir siteye atandı.
- **3** -Yönetim Aracısı, sunucu yapılandırma ilkelerinizi almak ve Intune 'a telemetri günlükleri göndermek için Intune ile iletişim kurar.  
- **4** -Intune YÖNETICISI, VPN profilleri ve tünel uygulamasını cihazlara oluşturur ve dağıtır.  
- **5** -CIHAZ Azure AD kimlik doğrulaması yapar. Koşullu erişim ilkeleri değerlendirilir.  
- **6** -bölünmüş tünele:  
  - **6a** -bazı trafik doğrudan genel İnternet 'e gider.  
  - **6B** -bazı trafik, tünel için herkese açık IP adresine gider.  
- **7** -tünel, trafiği iç ara sunucunuza (isteğe bağlı) ve şirket ağınıza yönlendirir.

**Ek ayrıntılar**:

- Koşullu erişim, VPN istemcisinde ve bulut uygulaması *Microsoft tüneli ağ geçidine*göre yapılır. Uyumlu olmayan cihazlar Azure AD 'den bir erişim belirteci almaz ve VPN sunucusuna erişemez. Microsoft tünele koşullu erişim kullanma hakkında daha fazla bilgi için bkz. [Microsoft tüneli Ile koşullu erişim kullanma](#use-conditional-access-with-the-microsoft-tunnel).

- Yönetim Aracısı Azure uygulama KIMLIĞI/gizli anahtarları kullanılarak Azure AD 'de yetkilendirilir.

- Tünel ağ geçidi sunucusu, kurumsal ağa bağlanan VPN istemcilerine adresler sağlamak için NAT kullanır.
  
## <a name="next-steps"></a>Sonraki adımlar

[Microsoft tüneli 'ni yükleyip yapılandırma](microsoft-tunnel-configure.md)
