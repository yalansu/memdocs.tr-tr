---
title: İstemci güvenliği ve gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager istemcileri için güvenlik ve gizlilik hakkında bilgi edinin.
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84ef4e37ddf756f04101c9cdec0ec7a4ed91688d
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270846"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Configuration Manager istemcileri için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede Configuration Manager istemcileri için güvenlik ve gizlilik bilgileri açıklanmaktadır. Ayrıca [Exchange Server Bağlayıcısı](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)tarafından yönetilen mobil cihazlar için bilgiler içerir.  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a>İstemciler için en iyi güvenlik uygulamaları  

Configuration Manager site, Configuration Manager istemcisini çalıştıran cihazlardan gelen verileri kabul eder. Bu davranış, istemcilerin siteye saldırması riskini tanıtır. Örneğin, hatalı oluşturulmuş envanter gönderebilir veya site sistemlerini aşırı yüklemeyi deneyebilirler. Configuration Manager istemcisini yalnızca güvendiğiniz cihazlara dağıtın. Ayrıca, siteyi yanlış veya riskli aygıtlardan korumaya yardımcı olmak için aşağıdaki en iyi güvenlik uygulamalarını kullanın:  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>IIS çalıştıran site sistemleriyle istemci iletişimleri için ortak anahtar altyapısı (PKI) sertifikaları kullanın  

- Bir site özelliği olarak, **Site sistem ayarları**'nı **Yalnızca HTTPS** kullanacak şekilde yapılandırın.  

- `UsePKICert`CCMSetup özelliği ile istemcileri yükleme.  

- Bir sertifika iptal listesi (CRL) kullanın ve istemcilerin ve iletişim sunucularının buna daima erişebilmesini sağlayın.  

Mobil cihaz istemcileri ve bazı internet tabanlı istemciler bu sertifikaları gerektirir. Microsoft, intranetteki tüm istemci bağlantıları için bu sertifikaları önerir.  

PKI sertifika gereksinimleri ve Configuration Manager korunmasına yardımcı olmak için nasıl kullanıldıkları hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md).  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Güvenilir etki alanlarındaki istemci bilgisayarlarını otomatik olarak onaylama ve diğer bilgisayarları el ile kontrol edip onaylama  

PKI kimlik doğrulamasını kullandığınızda, onay Configuration Manager tarafından yönetilmek üzere güvendiğiniz bir bilgisayarı tanımlar. Hiyerarşi, istemci onayını yapılandırmak için aşağıdaki seçeneklere sahiptir:  

- El ile
- Güvenilir etki alanlarındaki bilgisayarlar için otomatik
- Tüm bilgisayarlar için otomatik  

En güvenli onay yöntemi, güvenilen etki alanlarının üyesi olan istemcileri otomatik olarak onaylamaktır. Bu seçenek, bağlı Azure Active Directory (Azure AD) kiracılarından bulut etki alanına katılmış istemcileri içerir.<!-- MEMDocs#318 --> Ardından diğer tüm bilgisayarları el ile kontrol edin ve onaylayın. Güvenilir olmayan bilgisayarların ağınıza erişmesini engellemek için başka erişim denetimleriniz yoksa, tüm istemcilerin otomatik olarak onaylanması önerilmez.  

Bilgisayarların el ile nasıl onaylanacağı hakkında daha fazla bilgi için bkz. [Cihazlar düğümünden Istemcileri yönetme](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>İstemcilerin Configuration Manager hiyerarşisine erişmesini engellemek için engellemeye güvenmeyin  

Engellenen istemciler Configuration Manager altyapısı tarafından reddedilir. İstemciler engellenirse, ilke indirmek, envanter verileri yüklemek veya durum iletilerini göndermek için site sistemleriyle iletişim kuramaz.

Engelleme aşağıdaki senaryolar için tasarlanmıştır:

- İstemcilere bir işletim sistemi dağıttığınızda kayıp veya güvenliği aşılmış önyükleme medyasını engellemek için
- Tüm site sistemleri HTTPS istemci bağlantılarını kabul ettiğinde

Site sistemleri HTTP istemci bağlantılarını kabul ettiğinde Configuration Manager hiyerarşisini güvenilmeyen bilgisayarlardan korumak için engellemeye güvenmeyin. Bu senaryoda engellenen bir istemci, otomatik olarak imzalanan yeni bir sertifika ve donanım KIMLIĞIYLE siteye yeniden katılabilir.

Sertifika iptali, riskli olabilecek sertifikalara karşı birincil savunma hattınızdır. Bir sertifika iptal listesi (CRL) yalnızca desteklenen bir ortak anahtar altyapısında (PKI) kullanılabilir. Configuration Manager istemcilerin engellenmesi, hiyerarşinizi korumak için ikinci bir savunma hattı sunar.  

Daha fazla bilgi için bkz. [istemcilerin engellenip engellenmeyeceğini belirleme](determine-whether-to-block-clients.md).  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Ortamınız için pratik olan en güvenli istemci yükleme yöntemlerini kullanın  

- Etki alanı bilgisayarları için, Grup İlkesi istemci yüklemesi ve yazılım güncelleştirme tabanlı istemci yükleme yöntemleri, istemci anında yüklemeden daha güvenlidir.  

- Erişim denetimleri ve değişiklik denetimleri uygularsanız, görüntüleme ve el ile yükleme yöntemlerini kullanın.  

- Sürüm 1806 veya sonraki sürümlerde, istemci anında yükleme ile Kerberos karşılıklı kimlik doğrulaması kullanın.  

İstemci yükleme yöntemlerinin tümünde, sahip olduğu birçok bağımlılık nedeniyle istemci gönderme yüklemesi en az güvenlidir. Bu bağımlılıklar yerel yönetim izinleri, admin $ Share ve güvenlik duvarı özel durumlarını içerir. Bu bağımlılıkların sayısı ve türü, saldırı yüzeyinizi artırır.  

Sürüm 1806 ' den başlayarak, istemci gönderimi kullanılırken site, bağlantı kurulmadan önce NTLM 'ye geri dönüşe izin vermeyerek Kerberos karşılıklı kimlik doğrulaması gerektirebilir. Bu geliştirme, sunucu ve istemci arasındaki iletişimin güvenliğini sağlamaya yardımcı olur. Daha fazla bilgi için bkz. [Client Push ile istemcileri yükleme](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!--1358204-->  

Farklı istemci yükleme yöntemleri hakkında daha fazla bilgi için bkz. [istemci yükleme yöntemleri](client-installation-methods.md).  

Mümkün olan yerlerde, Configuration Manager için en az güvenlik izinleri gerektiren bir istemci yükleme yöntemi seçin. Güvenlik rollerine atanmış yönetici kullanıcıları, istemci dağıtımı dışındaki amaçlarla kullanılabilecek izinlerle kısıtlayın. Örneğin, otomatik istemci yükseltmesini yapılandırmak, yönetici kullanıcıya tüm güvenlik izinlerini veren **tam yönetici** güvenlik rolünü gerektirir.  

Her istemci yükleme yöntemi için gereken bağımlılıklar ve güvenlik izinleri hakkında daha fazla bilgi için, [bilgisayar istemcilerine yönelik önkoşulların](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers)"yükleme yöntemi bağımlılıkları" bölümüne bakın.  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>İstemci anında yükleme kullanmanız gerekiyorsa, İstemci Anında Yükleme Hesabını güvenli hale getirmek için ek adımlar uygulayın  

Bu hesap, Configuration Manager istemcisini yükleyen her bilgisayarda yerel **Yöneticiler** grubunun bir üyesi olmalıdır. Istemci anında yükleme hesabını hiçbir şekilde **etki alanı yöneticileri** grubuna eklemeyin. Bunun yerine, genel bir grup oluşturun ve ardından bu genel grubu istemcilerinizdeki yerel **Yöneticiler** grubuna ekleyin. Istemci anında yükleme hesabını yerel **Yöneticiler** grubuna eklemek üzere bir kısıtlı grup ayarı eklemek için bir Grup İlkesi nesnesi oluşturun.  

Ek güvenlik için, her biri sınırlı sayıda bilgisayara yönetim erişimi olan birden çok Istemci anında yükleme hesabı oluşturun. Bir hesap tehlikeye girerse, yalnızca bu hesabın erişimi olan istemci bilgisayarlarının güvenliği aşılmış olur.  

### <a name="remove-certificates-before-imaging-clients"></a>Görüntüleme istemcilerinden önce sertifikaları kaldırma  

İstemcileri, işletim sistemi görüntülerini kullanarak dağıttığınızda, görüntüyü yakalamadan önce her zaman sertifikaları kaldırın. Bu sertifikalar, istemci kimlik doğrulaması ve otomatik olarak imzalanan sertifikalar için PKI sertifikaları içerir. Bu sertifikaları kaldırmazsanız, istemciler birbirini taklit edebilir. Her istemci için verileri doğrularsınız.  

Daha fazla bilgi için bkz. bir [işletim sistemini yakalamak için görev dizisi oluşturma](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Configuration Manager bilgisayar istemcilerinin bu sertifikaların yetkili bir kopyasını aldığından emin olun  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>Configuration Manager güvenilen kök anahtar sertifikası  

Aşağıdaki deyimlerden her ikisi de doğru olduğunda, istemciler geçerli yönetim noktalarının kimliğini doğrulamak için Configuration Manager güvenilen kök anahtarı kullanır:  

- Configuration Manager için Active Directory şemasını genişletmemiş olabilirsiniz
- İstemciler yönetim noktalarıyla iletişim kurduğunda PKI sertifikaları kullanmaz  

Bu senaryoda, istemcilerin, güvenilen kök anahtarı kullanmadıkça, yönetim noktasının hiyerarşi için güvenilir olduğunu doğrulama yolu yoktur. Güvenilir kök anahtar olmadan, becerikli bir saldırgan, istemcileri yanlış bir yönetim noktasına yönlendirebilir.  

İstemciler, genel katalogdan veya PKI sertifikalarını kullanarak Configuration Manager güvenilen kök anahtarını indiremiyorsa, istemcileri güvenilen kök anahtarla önceden sağlayın. Bu eylem, bir standart dışı yönetim noktasına yönlendirilmezler olmasını sağlar. Daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="the-site-server-signing-certificate"></a>Site sunucusu imzalama sertifikası  

İstemciler, site sunucusunun bir yönetim noktasından indirilen ilkeyi imzaladığı doğrulamak için bu sertifikayı kullanır. Bu sertifika, site sunucusu tarafından otomatik imzalanır ve Active Directory Etki Alanı Hizmetlerine yayımlanır.  

İstemciler site sunucusu imzalama sertifikasını genel katalogdan indiremez, varsayılan olarak yönetim noktasından indirirler. Yönetim noktası internet gibi güvenilmeyen bir ağa sunulduktan sonra, istemcilere site sunucusu imzalama sertifikasını el ile yükleyebilirsiniz. Bu eylem, güvenliği aşılmış bir yönetim noktasından değiştirilen istemci ilkelerini indirememesini sağlar.  

Site sunucusu imzalama sertifikasını el ile yüklemek için CCMSetup client.msi’nin **SMSSIGNCERT** özelliğini kullanın. Daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../about-client-installation-properties.md).  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>İstemci güvenilen kök anahtarı, iletişim kurduğu ilk yönetim noktasından indirirse otomatik site ataması kullanmayın  

Yeni bir istemcinin, yanlış bir yönetim noktasından güvenilir kök anahtarı indirme riskini önlemek için, otomatik site atamasını yalnızca aşağıdaki senaryolarda kullanın:  

- İstemci, Active Directory Domain Services yayımlanan Configuration Manager site bilgilerine erişebilir.  

- İstemciye güvenilir kök anahtarı önceden sağladığınızda.  

- İstemci ve yönetim noktası arasında güven sağlamak için bir kuruluş sertifika yetkilisinden PKI sertifikaları kullandığınızda.  

Güvenilen kök anahtar hakkında daha fazla bilgi için bkz. [güvenilir kök anahtar Için planlama](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>İstemci bilgisayarlarını CCMSetup Client.msi seçeneği SMSDIRECTORYLOOKUP=NoWINS ile yükleyin  

İstemcilerin, siteleri ve yönetim noktalarını bulmak için en güvenli hizmet konumu yöntemi, Active Directory Etki Alanı Hizmetleri'ni kullanmaktır. Bazen bazı ortamlar için bu yöntem mümkün değildir. Örneğin, Configuration Manager için Active Directory şemayı genişletemiyorum veya istemciler güvenilmeyen bir ormanda veya bir çalışma grubunda olduğundan. Bu yöntem mümkün değilse, alternatif bir hizmet konumu yöntemi olarak DNS yayımlama kullanın. Bu yöntemlerin her ikisi de başarısız olursa ve yönetim noktası HTTPS istemci bağlantıları için yapılandırılmadığında istemciler WINS kullanmaya geri dönebilir.  

WINS 'e yayımlama, diğer yayımlama yöntemlerinden daha az güvenlidir. İstemci bilgisayarlarını **Smsdirectorylookup = NoWINS**belirterek WINS kullanmaya geri dönememek üzere yapılandırın. Hizmet konumu için WINS kullanmanız gerekiyorsa, **Smsdirectorylookup = WıNSSECURE**komutunu kullanın. Bu varsayılan ayardır. Yönetim noktasının otomatik olarak imzalanan sertifikasını doğrulamak için Configuration Manager güvenilen kök anahtarını kullanır.  

> [!NOTE]  
> **Smsdirectorylookup = WıNSSECURE** için istemcisini YAPıLANDıRDıĞıNıZDA ve WINS 'den bir yönetim noktası bulduğunda, ISTEMCI, wmı 'de Configuration Manager güvenilen kök anahtarı kopyasını denetler.  
>
> Yönetim noktası sertifikasındaki imza, istemcinin güvenilir kök anahtar kopyasıyla eşleşiyorsa, sertifika onaylanır. Sertifika doğrulandıktan sonra istemci, WINS kullanarak bulduğu yönetim noktasıyla iletişim kurar.  
>
> Yönetim noktası sertifikasındaki imza, istemcinin güvenilir kök anahtarı kopyasıyla eşleşmezse, sertifika geçerli değildir. Bu senaryoda, istemci WINS kullanarak bulduğu yönetim noktasıyla iletişim kurmaz.  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Bakım pencerelerinin, kritik yazılım güncelleştirmelerini dağıtmaya yetecek büyüklükte olmalarını sağlayın  

Cihaz Koleksiyonları için bakım pencereleri, Configuration Manager bu cihazlara yazılım yükleyebileceği zamanları kısıtlar. Bakım penceresini çok küçük olacak şekilde yapılandırırsanız, istemci kritik yazılım güncelleştirmelerini yükleyemeyebilir. Bu davranış, istemciyi yazılım güncelleştirmesinin azaltır herhangi bir saldırıya karşı savunmasız bırakır.  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Yazma filtreleriyle Windows Embedded cihazlarında saldırı yüzeyini azaltmak için ek güvenlik önlemleri alın  

Windows Embedded cihazlarında yazma filtrelerini etkinleştirdiğinizde, herhangi bir yazılım yüklemesi veya değişikliği yalnızca katmana yapılır. Cihaz yeniden başlatıldıktan sonra bu değişiklikler kalıcı olmaz. Yazma filtrelerini devre dışı bırakmak için Configuration Manager kullanırsanız, bu süre boyunca katıştırılmış cihaz tüm birimlerde değişikliklere açıktır. Bu birimler paylaşılan klasörleri içerir.  

Configuration Manager, bilgisayarı bu süre boyunca yalnızca yerel yöneticilerin oturum açmasını sağlayacak şekilde kilitler. Mümkün olduğunda, bilgisayarın korunmasına yardımcı olmak için ek güvenlik önlemleri alın. Örneğin, güvenlik duvarında ek kısıtlamaları etkinleştirin.  

Değişiklikleri sürdürmek için bakım pencerelerini kullanırsanız, bu pencereleri dikkatle planlayın. Yazma filtrelerinin devre dışı bırakıldığı süreyi en aza indirir, ancak yazılım yüklemelerinin ve yeniden başlatmalarının tamamlanmasına izin vermek için yeterince uzun hale getirin.  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Yazılım güncelleştirmesi tabanlı istemci yüklemesiyle en son istemci sürümünü kullan

Yazılım güncelleştirmesi tabanlı istemci yüklemesi kullanırsanız ve siteye istemcinin daha sonraki bir sürümünü yüklerseniz, yayımlanan yazılım güncelleştirmesini güncelleştirin. Ardından istemciler, yazılım güncelleştirme noktasından en son sürümü alır.  

Siteyi güncelleştirdiğinizde, yazılım güncelleştirme noktasına yayımlanan istemci dağıtımı yazılım güncelleştirmesi otomatik olarak güncellenmez. Configuration Manager istemcisini yazılım güncelleştirme noktasına yeniden yayımlayın ve sürüm numarasını güncelleştirin.  

Daha fazla bilgi için bkz. [yazılım güncelleştirmesi tabanlı yükleme kullanarak Configuration Manager istemcileri yükleme](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Yalnızca güvenilen ve kısıtlı erişimli cihazlarda BitLocker PIN girişini askıya al  

Yalnızca güvendiğiniz ve sınırlı fiziksel erişimi olan bilgisayarlar için **her zaman** **yeniden başlatma sırasında BitLocker PIN girişini askıya** almak için istemci ayarını yapılandırın.

Bu istemci ayarını **her zaman**olarak ayarlarsanız Configuration Manager yazılım yüklemesini tamamlayabilir. Bu davranış, kritik yazılım güncelleştirmelerini yüklemeye ve Hizmetleri sürdürmenize yardımcı olur. Bir saldırgan yeniden başlatma işlemini ele alıyorsa, bilgisayar denetimini ele geçirebilir. Bu ayarı yalnızca bilgisayara güveniyorsanız ve bilgisayara fiziksel erişim kısıtlı olduğunda kullanın. Örneğin, bu ayar bir veri merkezindeki sunucular için uygun olabilir.  

Bu istemci ayarı hakkında daha fazla bilgi için bkz. [istemci ayarları hakkında](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart).  

### <a name="dont-bypass-powershell-execution-policy"></a>PowerShell yürütme ilkesini atlama

**PowerShell yürütme ilkesi** için Configuration Manager Istemci ayarını **atlamak**üzere yapılandırırsanız, Windows imzasız PowerShell betiklerinin çalışmasına izin verir. Bu davranış, kötü amaçlı yazılımların istemci bilgisayarlarda çalışmasına izin verebilir. Kuruluşunuz bu seçeneği gerektirdiğinde, özel bir istemci ayarı kullanın. Bunu yalnızca imzasız PowerShell betiklerini çalıştırması gereken istemci bilgisayarlara atayın.  

Bu istemci ayarı hakkında daha fazla bilgi için bkz. [istemci ayarları hakkında](../about-client-settings.md#powershell-execution-policy).  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a>Mobil cihazlar için en iyi güvenlik uygulamaları  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Kayıt proxy noktasını bir çevre ağına ve intranet 'teki kayıt noktasına yükler  

Configuration Manager ile kaydolmasını istediğiniz Internet tabanlı mobil cihazlarda, kayıt proxy noktasını bir çevre ağına ve intranet 'teki kayıt noktasına yükleyebilirsiniz. Bu rol ayrımı, kayıt noktasını saldırıdan korumaya yardımcı olur. Bir saldırgan kayıt noktasını kullanıyorsa, kimlik doğrulaması için sertifikalar edinebilir. Ayrıca, mobil cihazlarını kaydeden kullanıcıların kimlik bilgilerini de çalabilir.  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Mobil cihazların yetkisiz erişime karşı korunmasına yardımcı olmak için parola ayarlarını yapılandırın  

*Configuration Manager tarafından kaydedilen mobil cihazlar için*: PIN olarak parola karmaşıklığını yapılandırmak için bir mobil cihaz yapılandırma öğesi kullanın. En azından varsayılan parola uzunluğunu belirtin.  

*Configuration Manager istemcisi yüklü olmayan, ancak Exchange Server Bağlayıcısı tarafından yönetilen mobil cihazlar için*: Exchange Server Bağlayıcısı Için **parola ayarlarını** , parola karmaşıklığı PIN olacak şekilde yapılandırın. En azından varsayılan parola uzunluğunu belirtin.  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Yalnızca güvendiğiniz şirketler tarafından imzalanan uygulamaların çalışmasına izin verin  

Uygulamaların yalnızca güvendiğiniz şirketler tarafından İmzalandıklarında çalışmasına izin vererek envanter bilgilerinin ve durum bilgilerinin değiştirilmesini önlemeye yardımcı olun. Cihazların imzasız dosyaları yüklemesine izin verme.  

*Configuration Manager tarafından kaydedilen mobil cihazlar için*: **imzasız uygulamalar** güvenlik ayarını **yasaklanmış**olarak yapılandırmak için bir mobil cihaz yapılandırma öğesi kullanın. **İmzasız dosya yüklemelerini** güvenilen bir kaynak olacak şekilde yapılandırın.  

*Configuration Manager istemcisi yüklü olmayan, ancak Exchange Server Bağlayıcısı tarafından yönetilen mobil cihazlar için*: Exchange Server Bağlayıcısı Için **uygulama ayarlarını** **imzasız dosya yükleme** ve **imzasız uygulamalara** **izin verilmeyen**şekilde yapılandırın.  

### <a name="lock-mobile-devices-when-not-in-use"></a>Kullanımda olmadığında mobil cihazları kilitle  

Kullanılmayan mobil cihazı kilitleyerek ayrıcalık saldırılarının yükseltilmesini önlemeye yardımcı olun.

*Configuration Manager tarafından kaydedilen mobil cihazlar için*: mobil cihazın **kilitlenmesinden önce dakika olarak boşta kalma süresi**ayarını yapılandırmak için bir mobil cihaz yapılandırma öğesi kullanın.  

*Configuration Manager istemcisi yüklü olmayan, ancak Exchange Server Bağlayıcısı tarafından yönetilen mobil cihazlar için*: Exchange Server Bağlayıcısı Için **parola ayarlarını** , **mobil cihazın kilitlenmesinden önce dakika olarak boşta kalma süresini**ayarlamak üzere yapılandırın.  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Mobil cihazlarını kaydedebilen kullanıcıları kısıtlama  

Mobil cihazlarını kaydedebilen kullanıcıları kısıtlayarak ayrıcalıkların yükselmesini önlemeye yardımcı olun. Yalnızca izin verilen kullanıcıların mobil aygıtlarını kaydetmesine izin vermek için varsayılan istemci ayarları yerine özel bir istemci ayarı kullanın.  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Mobil cihazlar için Kullanıcı cihaz benzeşimi Kılavuzu  

Configuration Manager veya Microsoft Intune tarafından kaydedilmiş mobil cihazlara sahip kullanıcılara uygulamaları dağıtmayın aşağıdaki senaryolarda:  

- Mobil cihaz birden fazla kişi tarafından kullanılıyor.  

- Cihaz, bir kullanıcı adına yönetici tarafından kaydedilir.  

- Cihaz devre dışı bırakılıp yeniden kaydedilmeden başka bir kişiye aktarılır.  

Cihaz kaydı, bir Kullanıcı cihaz benzeşimi ilişkisi oluşturur. Bu ilişki, kaydı gerçekleştiren kullanıcıyı mobil cihaza eşler. Mobil aygıtı başka bir Kullanıcı kullanıyorsa, özgün kullanıcıya dağıtılan uygulamaları çalıştırabilir ve bu da ayrıcalıkların yükselmesine yol açabilir. Benzer şekilde, bir yönetici bir kullanıcı için mobil cihazı kaydederse, kullanıcıya dağıtılan uygulamalar mobil cihaza yüklenmez. Bunun yerine, yöneticiye dağıtılan uygulamalar yüklü olabilir.  

Windows bilgisayarlar için Kullanıcı aygıt benzeşiminin aksine, Microsoft Intune tarafından kaydedilen mobil cihazlar için Kullanıcı aygıt benzeşimi bilgilerini el ile tanımlayamazsınız.  

Intune tarafından kaydedilen bir mobil cihazın sahipliğini aktarırsanız, önce mobil cihazı Intune 'dan devre dışı bırakın. Bu eylem, Kullanıcı aygıtı benzeşim ilişkisini kaldırır. Ardından geçerli kullanıcıdan cihazı tekrar kaydetmesini isteyin.  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Kullanıcıların Microsoft Intune için kendi mobil cihazlarını kaydetdiğinin emin olun  

Kayıt sırasında bir kullanıcı aygıtı benzeşim ilişkisi oluşturulur. Bu eylem, kaydı gerçekleştiren kullanıcıyı mobil cihaza eşler. Bir yönetici bir kullanıcı için mobil cihazı kaydederse, kullanıcıya dağıtılan uygulamalar mobil cihaza yüklenmez. Bunun yerine, yöneticiye dağıtılan uygulamalar yüklü olabilir.  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Configuration Manager site sunucusu ve Exchange sunucusu arasındaki bağlantıyı koruyun

Exchange Server şirket içi ise, IPSec kullanın. Barındırılan Exchange, SSL kullanarak bağlantı güvenliğini otomatik olarak sağlar.  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Bağlayıcı için en az ayrıcalık ilkesini kullanın  

Exchange Server bağlayıcısının gerektirdiği en küçük cmdlet 'lerin listesi için bkz. [Configuration Manager ve Exchange ile mobil cihazları yönetme](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a>Mac için en iyi güvenlik uygulamaları  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>İstemci kaynak dosyalarını depolayın ve güvenli bir konumdan erişin  

İstemciyi Mac bilgisayarına yüklemeden veya kaydetmeden önce, Configuration Manager Bu istemci kaynak dosyalarının ile oynanmış olup olmadığını doğrulamaz. Bu dosyaları güvenilir bir kaynaktan indirin. Güvenli bir şekilde depolayın ve bunlara erişin.  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Sertifikanın geçerlilik süresini izleyin ve izleyin  

İş sürekliliğini sağlamak üzere, Mac bilgisayarlar için kullandığınız sertifikaların geçerlilik süresini izleyin. Configuration Manager, bu sertifikanın otomatik yenilenmesini desteklemez veya sertifikanın sona ermek üzereyken sizi uyarır. Tipik bir geçerlilik süresi bir yıldır.  

Sertifikanın nasıl yenileneceği hakkında daha fazla bilgi için bkz. [Mac istemci sertifikasını el Ile yenileme](../deploy-clients-to-macs.md#renew-the-mac-client-certificate).  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Güvenilen kök sertifikayı yalnızca SSL için yapılandırma  

Ayrıcalıkların yükselmesine karşı korunmaya yardımcı olmak için, güvenilen kök sertifika yetkilisinin sertifikasını yalnızca SSL protokolü için güvenilecek şekilde yapılandırın.

Mac bilgisayarları kaydettiğinizde, Configuration Manager istemcisini yönetmek için bir kullanıcı sertifikası otomatik olarak yüklenir. Bu Kullanıcı sertifikası, güven zincirindeki güvenilen kök sertifikalarını içerir. Bu kök sertifikanın güvenini yalnızca SSL protokolüyle kısıtlamak için aşağıdaki yordamı kullanın:  

1. Mac bilgisayarda bir terminal penceresi açın.  

2. Aşağıdaki komutu girin:`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. **Anahtarlık erişimi** iletişim kutusunda, **anahtarlıklar** bölümünde **sistem**' e tıklayın. Sonra **Kategori** bölümünde **Sertifikalar**' a tıklayın.  

4. Mac istemci sertifikası için kök CA sertifikasını bulun ve çift tıklatın.  

5. Kök CA sertifikası iletişim kutusunda **Güven** bölümünü genişletin ve ardından aşağıdaki değişiklikleri yapın:  

    1. **Bu sertifikayı kullanırken**: **her zaman güven** ayarını **sistem varsayılanlarını kullanacak**şekilde değiştirin.  

    2. **Güvenli Yuva Katmanı (SSL)**: **her zaman güven**için **belirtilen değeri** değiştirin.  

6. İletişim kutusunu kapatın. İstendiğinde, yöneticinin parolasını girip **Ayarları Güncelleştir**' e tıklayın.  

Bu yordamı tamamladıktan sonra kök sertifikaya yalnızca SSL protokolünü doğrulamak için güvenilir. Artık bu kök sertifikayla güvenilmeyen diğer protokoller güvenli posta (S/MIME), Genişletilebilir kimlik doğrulaması (EAP) veya kod imzalama içerir.  

> [!NOTE]  
> İstemci sertifikasını Configuration Manager bağımsız olarak yüklediyseniz de bu yordamı kullanın.


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a>Configuration Manager istemcileri için güvenlik sorunları  

Aşağıdaki güvenlik sorunlarının çözümü yoktur:  

### <a name="status-messages-arent-authenticated"></a>Durum iletilerinin kimliği doğrulanmadı

Durum iletileri üzerinde bir kimlik doğrulaması gerçekleştirilmez. Bir yönetim noktası HTTP istemci bağlantılarını kabul ettiğinde yönetim noktasına herhangi bir aygıt durum iletisi gönderebilir. Yönetim noktası yalnızca HTTPS istemci bağlantılarını kabul ediyorsa, bir cihazın geçerli bir istemci kimlik doğrulama sertifikası olması gerekir, ancak aynı zamanda herhangi bir durum iletisi gönderebilir. Yönetim noktası bir istemciden alınan geçersiz durum iletilerini atar.  

Bu güvenlik açığına karşı birkaç olası saldırı vardır:

- Saldırgan, durum iletisi sorgularına dayalı bir koleksiyonda üyelik kazanmak için sahte bir durum iletisi gönderebilir.
- Herhangi bir istemci, yönetim noktasını durum iletileriyle doldurarak yönetim noktasına karşı bir hizmet reddi başlatabilir.
- Durum iletileri durum iletisi filtreleme kurallarında eylemleri tetikliyorsa, durum iletisi filtreleme kuralını bir saldırgan tetikleyebilir.
- Saldırgan, raporlama bilgilerini yanlış bir şekilde işleyecek durum iletisi gönderebilir.  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>İlkeler hedeflenmeyen kullanıcılara yönlendirilebilir  

Saldırganlar bir istemciye yöneltilmiş bir ilkeyi tamamen farklı bir istemciye uygulamak üzere birçok yöntem kullanabilir. Örneğin, güvenilen bir istemcideki bir saldırgan, bilgisayarın ait olmaması gereken bir koleksiyona eklenmesi için yanlış envanter veya bulma bilgileri gönderebilir. Bu istemci daha sonra bu koleksiyona yönelik tüm dağıtımları alır.

Saldırganların ilkeyi doğrudan değiştirmesini önlemeye yardımcı olmak için denetimler vardır. Ancak saldırganlar, bir işletim sistemini yeniden biçimlendiren ve yeniden dağıtan ve farklı bir bilgisayara gönderen mevcut bir ilkeyi alabilir. Bu yeniden yönlendirilen ilke bir hizmet reddi oluşturabilir. Bu tür saldırılar, Configuration Manager altyapısı için kesin bir zamanlama ve kapsamlı bilgi gerektirir.  

### <a name="client-logs-allow-user-access"></a>İstemci günlükleri kullanıcı erişimine izin veriyor  

Tüm istemci günlük dosyaları, **Kullanıcılar** grubuna *okuma* erişimi ve *yazma* erişimi olan özel **etkileşimli** Kullanıcı için izin verir. Ayrıntılı günlüğe yazmayı etkinleştirirseniz, saldırganlar uyum veya sistem güvenlik açıkları hakkındaki bilgileri aramak için günlük dosyalarını okuyabilir. İstemcinin bir kullanıcının bağlamına yüklediği yazılımlar gibi işlemlerin, düşük haklara sahip bir kullanıcı hesabıyla günlüklere yazması gerekir. Bu davranış, bir saldırganın düşük haklara sahip bir hesapla günlüklere da yazabilmesi anlamına gelir.  

En ciddi risk, bir saldırganın günlük dosyalarındaki bilgileri kaldıra,. Yönetici, denetim ve yetkisiz giriş algılama için bu bilgilere ihtiyaç duyuyor.  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Mobil cihaz kaydı için tasarlanan bir sertifika almak için bir bilgisayar kullanılabilir  

Configuration Manager bir kayıt isteğini işlediğinde, isteğin bir bilgisayar yerine bir mobil cihazdan geldiğini doğrulayamaz. İstek bir bilgisayardan ise, daha sonra Configuration Manager kaydına izin veren bir PKI sertifikası yükleyebilir.

Bu senaryoda ayrıcalık yükselmesine engel olmak için, yalnızca güvenilen kullanıcıların mobil cihazlarını kaydetmesine izin verin. Sitedeki cihaz kaydı etkinliklerini dikkatle izleyin.  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Engellenen istemci, yönetim noktasına ileti gönderebilmeye devam edebilir

Artık güvenmediğiniz bir istemciyi engellediğinizde, ancak istemci bildirimi için bir ağ bağlantısı kurmadıysa Configuration Manager oturumun bağlantısını kesmez. Engellenen istemci, ağ bağlantısı kesilene kadar yönetim noktasına paket göndermeye devam edebilir. Bu paketler yalnızca küçük, etkin tutma paketleridir. Bu istemci, engeli kaldırılana kadar Configuration Manager tarafından yönetilemez.  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>Otomatik istemci yükseltmesi yönetim noktasını doğrulamaz

Otomatik istemci yükseltmesi kullandığınızda istemci, istemci kaynak dosyalarını indirmek için bir yönetim noktasına yönlendirilebilir. Bu senaryoda istemci, yönetim noktasını güvenilir bir kaynak olarak doğrulamaz.  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Kullanıcılar Mac bilgisayarları ilk kez kaydettiğinde, DNS yanıltma riskine karşı risk altındasınız  

Mac bilgisayarı kayıt sırasında kayıt proxy noktasına bağlanırsa, Mac bilgisayarının zaten güvenilen kök CA sertifikasına sahip olması düşüktür. Bu noktada, Mac bilgisayar sunucuya güvenmez ve kullanıcıdan devam etmesini ister. Standart dışı bir DNS sunucusu, kayıt proxy noktasının tam etki alanı adını (FQDN) çözümlerse, güvenilir olmayan bir kaynaktan sertifika yüklemek için Mac bilgisayarı bir standart dışı kayıt proxy noktasına yönlendirebilir. Bu riski azaltmaya yardımcı olmak üzere en iyi uygulamaları izleyerek ortamınızda DNS yanıltmayı önleyin.  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Mac kaydı sertifika isteklerini sınırlamaz  

Kullanıcılar Mac bilgisayarlarını yeniden kaydettirerek her seferinde yeni bir istemci sertifikası isteyebilirler. Configuration Manager birden fazla isteği denetlemez veya tek bir bilgisayardan istenen sertifika sayısını sınırlamaz. Standart dışı bir Kullanıcı, komut satırı kayıt isteğini tekrardan çalışan bir komut dosyası çalıştırabilir. Bu saldırı, ağda veya sertifika verme yetkilisinde (CA) bir hizmet reddine neden olabilir. Bu riski azaltmaya yardımcı olmak için sertifika verme yetkilisini bu tür şüpheli davranışlara karşı dikkatlice izleyin. Configuration Manager hiyerarşisinden, bu davranış düzenlerini gösteren herhangi bir bilgisayarda hemen engelleyin.  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Silme onayı, cihazın başarıyla silindiğini doğrulamıyor  

Bir mobil cihaz için silme eylemi başlattığınızda ve silme işlemini Configuration Manager, doğrulama işlemi, iletiyi başarıyla *gönderdiği* Configuration Manager. *Cihazın istek* üzerinde işlem yapıldığını doğrulamaz.

Exchange Server Bağlayıcısı tarafından yönetilen mobil cihazlar için silme onayı, komutun aygıt tarafından değil, Exchange tarafından alındığını doğrular.  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Windows Embedded cihazlarında değişiklikleri yürütmek için bu seçenekleri kullanırsanız, hesaplar beklenenden daha önce kilitlenmiş olabilir  

Windows Embedded cihazı Windows 7 ' den önceki bir işletim sistemi sürümünü çalıştırıyorsa ve yazma filtreleri Configuration Manager tarafından devre dışı bırakıldığı sırada bir Kullanıcı oturum açmayı denerse, Windows, hesap kilitlenmeden önce yalnızca, yapılandırılan hatalı girişim sayısının yarısını kullanmasına izin verir.

Örneğin, **Hesap kilitleme eşiği** için etki alanı ilkesini altı girişimle yapılandırırsınız. Bir Kullanıcı parolalarını üç kez yanlış yazdığında, hesap kilitlenir. Bu davranış etkin bir şekilde hizmet reddi oluşturur. Kullanıcıların bu senaryodaki katıştırılmış cihazlarda oturum açması gerekiyorsa, daha düşük bir kilitleme eşiğine yönelik potansiyel olarak dikkat edin.  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a>Configuration Manager istemcileri için gizlilik bilgileri  

Configuration Manager istemcisini dağıttığınızda, Configuration Manager özellikler için istemci ayarlarını etkinleştirirsiniz. Özellikleri yapılandırmak için kullandığınız ayarlar Configuration Manager hiyerarşisindeki tüm istemcilere uygulanabilir. Bu davranış, doğrudan dahili ağa bağlanıp bağlanmadığı, uzak bir oturumla bağlanmış veya internet 'e bağlı olmalarıyla aynıdır.  

İstemci bilgileri, SQL sunucunuzdaki Configuration Manager veritabanında depolanır ve Microsoft 'a gönderilmez. Bilgiler, site bakım görevleri tarafından silinene kadar veritabanında tutulur ve her 90 günde bir **eski bulma verilerini silin** . Silme aralığını yapılandırabilirsiniz. 

Bazı özetlenen veya toplu tanılama ve kullanım verileri Microsoft 'a gönderilir. Daha fazla bilgi için bkz. [Tanılama ve kullanım verileri](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Configuration Manager istemcisini yapılandırmadan önce gizlilik gereksinimlerinizi göz önünde bulundurun.  

Microsoft 'un veri toplama ve kullanımı hakkında daha fazla bilgi için [Microsoft gizlilik bildirimi](https://privacy.microsoft.com/privacystatement)' ne erişebilirsiniz.

### <a name="client-status"></a>İstemci durumu  

Configuration Manager, istemcilerin etkinliğini izler. Configuration Manager istemcisini düzenli olarak değerlendirir ve istemci ve bağımlılıklarındaki sorunları düzeltebilir. İstemci durumu varsayılan olarak etkindir. İstemci etkinlik denetimleri için sunucu tarafı ölçümleri kullanır. İstemci durumu kendi kendine denetimler, düzeltme ve istemci durum bilgilerini siteye göndermek için istemci tarafı eylemlerini kullanır. İstemci kendi denetimlerini yapılandırdığınız bir zamanlamaya göre çalıştırır. İstemci, denetimlerin sonuçlarını Configuration Manager sitesine gönderir. Bu bilgiler aktarım sırasında şifrelenir.  

İstemci durum bilgileri, SQL sunucunuzdaki Configuration Manager veritabanında depolanır ve Microsoft 'a gönderilmez. Bilgiler site veritabanında şifreli biçimde depolanmaz. Bu bilgiler, **aşağıdaki gün sayısı istemci durumu ayarı için istemci durum geçmişini sakla** için yapılandırılan değere göre silinene kadar veritabanında tutulur. Bu ayar için varsayılan değer her 31 günde birdir.  

İstemci durum denetimi ile Configuration Manager istemcisini yüklemeden önce gizlilik gereksinimlerinizi göz önünde bulundurun.  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a>Exchange Server Bağlayıcısı ile yönetilen mobil cihazlar için gizlilik bilgileri  

Exchange Server Bağlayıcısı, ActiveSync protokolünü kullanarak şirket içi veya barındırılan bir Exchange sunucusuna bağlanan cihazları bulur ve yönetir. Exchange Server Bağlayıcısı tarafından bulunan kayıtlar, SQL sunucunuzdaki Configuration Manager veritabanında depolanır. Bilgiler Exchange Server 'dan toplanır. Mobil cihazların Exchange Server 'a gönderdiklerinin dışında ek bilgiler içermez.  

Mobil cihaz bilgileri Microsoft 'a gönderilmez. Mobil cihaz bilgileri, SQL sunucunuzdaki Configuration Manager veritabanında depolanır. Bilgiler, site bakım görevi tarafından silinene kadar, **eski bulma verilerini** her 90 günde bir silinene kadar veritabanında tutulur. Silme aralığını yapılandırırsınız.  

Exchange Server bağlayıcısını yüklemeden ve yapılandırmadan önce gizlilik gereksinimlerinizi gözden geçirin.  

Microsoft 'un veri toplama ve kullanımı hakkında daha fazla bilgi için [Microsoft gizlilik bildirimi](https://privacy.microsoft.com/privacystatement)' ne erişebilirsiniz.
