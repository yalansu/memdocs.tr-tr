---
title: Linux ve UNIX bilgisayarlara istemci dağıtımını planlama
titleSuffix: Configuration Manager
description: Configuration Manager ' de Linux ve UNIX bilgisayarlara istemci dağıtımını planlayın.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713236"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Configuration Manager 'da Linux ve UNIX bilgisayarlara istemci dağıtımını planlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!Important]  
> Sürüm 1902 ' den başlayarak Configuration Manager Linux veya UNIX istemcilerini desteklemez. 
> 
> Linux sunucularının yönetilmesi için Microsoft Azure yönetimini göz önünde bulundurun. Azure çözümlerinde, Linux için uçtan uca düzeltme eki yönetimi de dahil olmak üzere çoğu durumda Configuration Manager işlevselliği aşılacağından kapsamlı Linux desteği vardır.

Configuration Manager istemcisini Linux veya UNIX çalıştıran bilgisayarlara yükleyebilirsiniz. Bu istemci, bir çalışma grubu bilgisayarı olarak çalışan sunucular için tasarlanmıştır ve istemci, oturum açmış kullanıcılarla etkileşimi desteklemez. İstemci yazılımını yükledikten ve istemci Configuration Manager sitesiyle iletişim kurduktan sonra, Configuration Manager konsolunu ve raporlarını kullanarak istemciyi yönetirsiniz.  

> [!NOTE]
>  Linux ve UNIX bilgisayarlar için Configuration Manager istemcisi aşağıdaki yönetim özelliklerini desteklemez:  
> 
> - Client push yüklemesi  
>   -   İşletim sistemi dağıtımı  
>   -   Uygulama dağıtımı; bunun yerine paket ve programları kullanarak yazılımı dağıtın.  
>   -   Yazılım envanteri  
>   -   Yazılım güncelleştirmeleri  
>   -   Uyumluluk ayarları  
>   -   Uzaktan denetim  
>   -   Güç yönetimi  
>   -   İstemci durumu istemci denetimi ve düzeltmesi  
>   -   Internet tabanlı istemci yönetimi  

 Desteklenen Linux ve UNIX dağıtımları ve Linux ve UNIX için istemciyi desteklemek için gereken donanım hakkında daha fazla bilgi için, [Configuration Manager Için önerilen donanım](../../../../core/plan-design/configs/recommended-hardware.md)bölümüne bakın.  

 Linux ve UNIX için Configuration Manager istemcisini dağıtmayı planlamada yardımcı olması için bu makaledeki bilgileri kullanın.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a>Linux ve UNIX sunucularına Istemci dağıtımı önkoşulları  
 Linux ve UNIX istemcisini başarıyla yüklemek için sahip olmanız gereken önkoşulları belirlemek için aşağıdaki bilgileri kullanın.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a>Configuration Manager dış bağımlılıklar:  
 Aşağıdaki tablolar, gerekli UNIX ve Linux işletim sistemlerini ve paket bağımlılıklarını açıklamaktadır.  

 **Red Hat Enterprise Linux Server sürüm 5.1 (Tikanga)**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|glibc|C Standart Kitaplıkları|2.5-12|  
|Openssl|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü|0.9.8b-8.3.el5|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server sürüm 6**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|glibc|C Standart Kitaplıkları|2.12-1.7|  
|Openssl|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü|1.0.0-4|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri|1.1.1-4|  

 **Red Hat Enterprise Linux Server sürüm 7**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|glibc|C Standart Kitaplıkları|2.17|  
|Openssl|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü|1.0.1|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri|1.1.1-4|  

 **Solaris 10 SPARC**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|Gerekli işletim sistemi düzeltme eki|PAM bellek sızıntısı|117463-05|  
|SUNWlibC|Sun Atölye Derleyicileri Paket libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Matematik ve Microtasking Kitaplıkları (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Matematik ve Microtasking Kitaplıkları (Kök) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Çekirdek Solaris Kitaplıkları (Kök) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Çekirdek Solaris Kitaplıkları (Kök) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|OpenSSL|SUNopenssl-librararies (Usr)<br /><br /> Sun, Solaris 10 SPARC için OpenSSL kitaplıkları sağlar. Bunlar işletim sistemi ile paketlenmiştir.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri<br /><br /> SUNWcsr, Çekirdek Solaris (Kök) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|Gerekli işletim sistemi düzeltme eki|PAM bellek sızıntısı|117464-04|  
|SUNWlibC|Sun Atölye Derleyicileri Paket libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Matematik ve Microtasking Kitaplıkları (Kök) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Çekirdek Solaris, (Paylaşılan Kitaplıklar) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Çekirdek Solaris Kitaplıkları (Kök) (i386)|11.10.0, REV=2005.01.21.16.34|  
|OpenSSL|SUNWopenssl-libraries; OpenSSL Libraries (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri<br /><br /> SUNWcsr Çekirdek Solaris, (Kök) (i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Atölye Derleyicileri Paket libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Matematik ve Küçük Görevli İşlem Kitaplığı (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Çekirdek Solaris Kitaplıkları (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Çekirdek Solaris, (Paylaşılan Kitaplıklar)|11.11, REV=2009.11.11|  
|SUNWcsr|Çekirdek Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Atölye Derleyicileri Paket libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Matematik ve Küçük Görevli İşlem Kitaplığı (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Çekirdek Solaris Kitaplıkları (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Çekirdek Solaris, (Paylaşılan Kitaplıklar)|11.11, REV=2009.11.11|  
|SUNWcsr|Çekirdek Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|glibc-2.4-31.30|C Standart paylaşılan kitaplığı|2.4-31.30|  
|OpenSSL|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü|0.9.8a-18.15|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|C Standart paylaşılan kitaplığı|2.9-13.2|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri|pam-1.0.2-20.1|  

 **Evrensel Linux (Debian paketi) Debian, Ubuntu Server**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|libc6|C Standart paylaşılan kitaplığı|2.3.6|  
|OpenSSL|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü|0.9.8 veya 1.0|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri|0.79-3|  

 **Universal Linux (RPM paketi) CentOS, Oracle Linux**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|glibc|C Standart paylaşılan kitaplığı|2.5-12|  
|OpenSSL|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü|0.9.8 veya 1.0|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|İşletim sistemi sürümü|İşletim sisteminin sürümü|AıX 6,1: herhangi bir teknoloji düzeyi ve hizmet paketi|  
|xlC.rte|XL C/C++ Çalışma Zamanı|9.0.0.5|  
|OpenSSL/openssl.base|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|İşletim sistemi sürümü|İşletim sisteminin sürümü|AıX 7,1: herhangi bir teknoloji düzeyi ve hizmet paketi|  
|xlC.rte|XL C/C++ Çalışma Zamanı||  
|OpenSSL/openssl.base|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü||  


 **HP-UX 11i v3 IA64**  

|Gerekli paket|Açıklama|En düşük sürüm|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Belirli IA geliştirme kitaplıkları|B.11.31|  
|SysMgmtMin|En Küçük Yazılım Dağıtım Araçları|B.11.31.0709|  
|SysMgmtMin.openssl|OpenSSL Kitaplıkları; Güvenli Ağ İletişim Protokolü|A.00.09.08d.002|  
|PAM|Eklenebilir Kimlik Doğrulaması Modülleri|HP-UX'te, PAM çekirdek işletim sistemi bileşenlerinin parçasıdır. Başka bir bağımlılık yoktur.|  

 **Configuration Manager Bağımlılıklar:** Aşağıdaki tabloda, Linux ve UNIX istemcilerini destekleyen site sistemi rolleri listelenmektedir. Bu site sistemi rolleri hakkında daha fazla bilgi için bkz. [Configuration Manager istemcileri için site sistemi rollerini belirleme](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Configuration Manager site sistemi|Daha fazla bilgi|  
|---------------------------------------|----------------------|  
|Yönetim noktası|Linux ve UNIX için Configuration Manager istemcisi yüklemek üzere bir yönetim noktası gerekli olmasa da, istemci bilgisayarlar ve Configuration Manager sunucuları arasında bilgi aktarmak için bir yönetim noktanız olmalıdır. Bir yönetim noktası olmadan istemci bilgisayarları yönetemezsiniz.|  
|Dağıtım noktası|Dağıtım noktası, Linux ve UNIX için Configuration Manager istemcisi yüklemek için gerekli değildir. Ancak Linux ve UNIX sunucularına yazılım dağıtımı yaparsanız, site sistemi rolü gereklidir.<br /><br /> Linux ve UNIX için Configuration Manager istemcisi SMB kullanan iletişimleri desteklemediğinden, istemciyle birlikte kullandığınız dağıtım noktalarının HTTP veya HTTPS iletişimini desteklemesi gerekir.|  
|Geri dönüş durumu noktası|Linux ve UNIX için Configuration Manager istemcisi yüklemek için geri dönüş durum noktası gerekli değildir. Ancak geri dönüş durum noktası, Configuration Manager sitesindeki bilgisayarların bir yönetim noktasıyla iletişim kuramadıklarında durum iletileri göndermesini sağlar. İstemci aynı zamanda bu bilgisayarların yükleme durumunu geri dönüş durum noktasına gönderebilir.|  

 **Güvenlik duvarı gereksinimleri**: güvenlik duvarlarının istemci istek bağlantı noktaları olarak belirttiğiniz bağlantı noktaları genelinde iletişimleri engellemediğinden emin olun. Linux ve UNIX istemcisi yönetim noktalarıyla, dağıtım noktalarıyla ve geri dönüş durum noktalarıyla doğrudan iletişim kurar.  

 İstemci iletişimi ve istek bağlantı noktaları hakkında daha fazla bilgi için bkz. [Linux ve UNIX İçin İstemciyi Yönetim Noktalarını Bulacak Biçimde Yapılandırma](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a>Linux ve UNIX sunucuları için orman güvenleri arasındaki Iletişimi planlama  
 Configuration Manager ile yönettiğiniz Linux ve UNIX sunucuları, çalışma grubu istemcileri olarak çalışır ve bir çalışma grubunda bulunan Windows tabanlı istemciler olarak benzer yapılandırmalara gerek duyar. Çalışma gruplarındaki bilgisayarlardan gelen iletişimler hakkında daha fazla bilgi için bkz. [Active Directory ormanları arasındaki iletişimler](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a>Linux ve UNIX için istemci tarafından hizmet konumu  
 İstemcilere hizmet sunan bir site sistemi sunucusunun konumunu bulma görevi, hizmet konumlandırma olarak adlandırılır. Windows tabanlı bir istemciden farklı olarak, Linux ve UNIX istemcisi hizmet konumu için Active Directory kullanmaz. Ayrıca, Linux ve UNIX için Configuration Manager istemcisi bir yönetim noktasının etki alanı son ekini belirten bir istemci özelliğini desteklemez. Bunun yerine istemci, istemci yazılımını yüklerken atadığınız bilinen bir yönetim noktasından istemcilere hizmet sağlayan ek site sistemi sunucuları hakkında bilgi edinir.  

 Daha fazla bilgi için bkz. [hizmet konumu ve istemcilerin atanan yönetim noktalarını belirleme şekli](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a>Linux ve UNIX sunucuları için güvenlik ve sertifika planlaması  
 Configuration Manager siteleriyle güvenli ve kimliği doğrulanmış iletişimler için, Linux ve UNIX için Configuration Manager istemcisi, Windows için Configuration Manager istemcisiyle aynı iletişim modelini kullanır.  

 Linux ve UNIX istemcisini yüklediğinizde, istemciye, Configuration Manager sitelerle iletişim kurmak için HTTPS kullanmasını sağlayan bir PKI sertifikası atayabilirsiniz. Bir PKI sertifikası atamadıysanız, istemci otomatik olarak imzalanan bir sertifika oluşturur ve yalnızca HTTP ile iletişim kurar.  

 Yüklendiklerinde bir PKI sertifikası verilen istemciler, yönetim noktalarıyla iletişim kurmak için HTTPS kullanır. İstemci, HTTPS’yi destekleyen bir yönetim noktası bulamazsa, sağlanan PKI sertifikasıyla HTTP kullanmaya geri döner.  

 Bir Linux veya UNIX istemcisi bir PKI sertifikası kullandığında, bunları onaylamanız gerekmez. İstemci otomatik olarak imzalanan bir sertifika kullandığında, Configuration Manager konsolundaki istemci onayı için hiyerarşi ayarlarını gözden geçirin. İstemci onay yöntemi **Tüm bilgisayarları otomatik olarak onayla (önerilmez)** değilse, istemciyi el ile onaylamanız gerekir.  

 İstemcinin el ile nasıl onaylanacağı hakkında daha fazla bilgi için bkz. [Cihazlar düğümünden Istemcileri yönetme](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 Configuration Manager sertifikaların nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../../plan-design/network/pki-certificate-requirements.md).  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a>Linux ve UNIX sunucuları tarafından kullanılan sertifikalar hakkında  
 Linux ve UNIX için Configuration Manager istemcisi, Windows tabanlı istemciler gibi otomatik olarak imzalanan bir sertifika veya bir X. 509.440 PKI sertifikası kullanır. Linux ve UNIX istemcilerini yönetirken Configuration Manager site sistemleri için PKI gereksinimlerinde değişiklik yapılmaz.  

 Configuration Manager site sistemleriyle iletişim kuran Linux ve UNIX istemcileri için kullandığınız sertifikaların ortak anahtar sertifika standardı (PKCS # 12) biçiminde olması ve PKI sertifikasını belirttiğinizde bunu istemciye belirleyebilmeniz için parolanın bilinmesi gerekir.  

 Linux ve UNIX için Configuration Manager istemcisi tek bir PKI sertifikasını destekler ve birden fazla sertifikayı desteklemez. Bu nedenle, bir Configuration Manager sitesi için yapılandırdığınız sertifika seçim kriterleri uygulanmaz.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a>Linux ve UNIX sunucuları için sertifikaları yapılandırma  
 Linux ve UNIX sunucuları için bir Configuration Manager istemcisini HTTPS iletişimleri kullanacak şekilde yapılandırmak için, istemcisini istemcisini yüklerken bir PKI sertifikası kullanacak şekilde yapılandırmanız gerekir. İstemci yazılımını yüklemeden önce bir sertifika sağlayamazsınız.  

 PKI sertifikası kullanan bir istemciyi yüklediğinizde, PKI sertifikasını içeren PKCS # 12 dosyasının konumunu ve adını belirtmek `-UsePKICert` için komut satırı parametresini kullanın. Ayrıca, sertifika parolasını belirtmek için komut satırı parametresini `-certpw` kullanmanız gerekir.  

 Belirtmezseniz `-UsePKICert`, istemci otomatik olarak imzalanan bir sertifika oluşturur ve yalnızca http kullanarak site sistemi sunucularıyla iletişim kurmaya çalışır.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a>SHA-256 desteklemeyen sürümler  
 Configuration Manager için istemci olarak desteklenen aşağıdaki Linux ve UNIX işletim sistemleri, SHA-256 ' y i desteklemeyen OpenSSL sürümleriyle yayımlanmıştır:  

-   Solaris sürüm 10 (SPARC/x86)  


 Bu işletim sistemlerini Configuration Manager ile yönetmek için, Linux ve UNIX için Configuration Manager istemcisini, istemciyi SHA-256 doğrulamasını atlayacak şekilde yönlendiren bir komut satırı anahtarıyla yüklemelisiniz. Bu işletim sistemi sürümlerinde çalışan Configuration Manager istemcileri, SHA-256 ' y i destekleyen istemcilerden daha az güvenli bir modda çalışır. Bu daha az güvenli çalışma modu şu davranışa sahiptir:  

-   İstemciler, bir yönetim noktasından istedikleri ilkeyle ilişkili site sunucusu imzasını doğrulamaz.  

-   İstemciler, bir dağıtım noktasından indirdikleri paketlerin karmasını doğrulamaz.  

> [!IMPORTANT]  
>  Seçeneği `ignoreSHA256validation` , LINUX ve UNIX bilgisayarlar için istemcisini daha az güvenli bir modda çalıştırmanızı sağlar. Bu özellik, SHA-256 desteği bulunmayan daha eski platformlar için kullanıma yöneliktir. Bu, güvenlik ayarlarını geçersiz kıldığından Microsoft tarafından önerilmez, ancak güvenli ve güvenilir bir veri merkezi ortamında kullanılması desteklenir.  

 Linux ve UNIX için Configuration Manager istemcisi yüklediğinde, yükleme betiği işletim sistemi sürümünü denetler. Varsayılan olarak, işletim sistemi sürümü, SHA-256 ' y i destekleyen bir OpenSSL sürümü olmadan yayımlanmışsa, Configuration Manager istemcisinin yüklenmesi başarısız olur.  

 SHA-256 ' y i destekleyen bir OpenSSL sürümüyle birlikte yayınlanmadığınız Linux ve UNIX işletim sistemlerine Configuration Manager istemcisini yüklemek için, Install komut satırı anahtarını `ignoreSHA256validation`kullanmanız gerekir. Bu komut satırı seçeneğini geçerli bir Linux veya UNIX işletim sisteminde kullandığınızda, Configuration Manager istemcisi SHA-256 doğrulamasını atlar ve yüklemeden sonra istemci, site sistemlerine gönderdiği verileri HTTP kullanarak imzalamak için SHA-256 kullanmaz. Linux ve UNIX istemcilerini sertifika kullanacak şekilde yapılandırma hakkında bilgi için bkz. [Linux ve UNIX sunucuları Için güvenlik ve sertifika planlaması](#BKMK_SecurityforLnU). SHA-256 gerektirme hakkında daha fazla bilgi için bkz. [imzalamayı ve şifrelemeyi yapılandırma](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  Komut satırı seçeneği `ignoreSHA256validation` , SHA-256 ' y i destekleyen OpenSSL sürümleriyle kullanıma sunulan LINUX ve UNIX sürümlerini çalıştıran bilgisayarlarda yok sayılır.  
