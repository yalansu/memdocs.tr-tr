---
title: İstemciyi Mac 'e dağıtmaya hazırlanma
titleSuffix: Configuration Manager
description: Configuration Manager istemcisini Mac 'e dağıtmadan önce yapılandırma görevleri.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2b5bcbce659601e10f44f06af94eb939767a389a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906633"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Mac 'e istemci yazılımı dağıtmaya hazırlanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

[Configuration Manager Istemcisini Mac bilgisayarlara dağıtmaya](deploy-clients-to-macs.md)hazırsınız olduğunuzdan emin olmak için aşağıdaki adımları izleyin.



## <a name="mac-prerequisites"></a>Mac önkoşulları

Mac istemcisi yükleme paketi Configuration Manager medyayla birlikte sağlanmaz. **Ek işletim sistemleri Için Istemcileri** [Microsoft İndirme Merkezi](https://www.microsoft.com/download/details.aspx?id=47719)' nden indirin.  

Desteklenen sürümlerin listesi için bkz. [istemciler ve cihazlar Için desteklenen işletim sistemleri](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).



## <a name="certificate-requirements"></a>Sertifika gereksinimleri

Mac bilgisayarlar için istemci yükleme ve yönetimi ortak anahtar altyapısı (PKI) sertifikaları gerektirir. PKI sertifikaları, karşılıklı kimlik doğrulaması ve şifrelenmiş veri aktarımları kullanarak Mac bilgisayarlar ile Configuration Manager sitesi arasındaki iletişimin güvenliğini güvence altına alın. Configuration Manager, bir kullanıcı istemci sertifikası isteyebilir ve yükleyebilir. Bir kuruluş sertifika yetkilisi ile Sertifika Hizmetleri, Configuration Manager kayıt noktası ve kayıt proxy noktası kullanır. Ayrıca, Configuration Manager bağımsız olarak bir bilgisayar sertifikası isteyebilir ve yükleyebilirsiniz. Bu sertifikanın Configuration Manager sertifika gereksinimlerini karşılaması gerekir.  

Configuration Manager Mac istemcileri her zaman sertifika iptalini denetler. Bu işlevi devre dışı bırakamıyorum.  

Mac istemcileri sertifika iptal listesini (CRL) bulamıyorsa, Configuration Manager site sistemlerine bağlanamaz. Özellikle, farklı bir ormandaki Mac istemcileri için veren sertifika yetkilisine, CRL tasarımınızı denetleyin. Mac istemcilerinin bir CRL bulup indirebiliyorsa emin olun.  

Configuration Manager istemcisini bir Mac bilgisayara yüklemeden önce istemci sertifikasını nasıl yükleyeceğinize karar verin:  

-   [CMEnroll aracını](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll)kullanarak Configuration Manager kaydını kullanın. Kayıt işlemi otomatik sertifika yenilemeyi desteklemiyor. Mac bilgisayarlarını sertifikanın süresi dolmadan önce yeniden kaydedin.  

-   [Configuration Manager bağımsız bir sertifika isteği ve yükleme yöntemi kullanın](deploy-clients-to-macs.md#bkmk_external).  

Mac istemci sertifikası gereksinimleri hakkında daha fazla bilgi için bkz. [Configuration Manager Için PKI sertifikası gereksinimleri](../../plan-design/network/pki-certificate-requirements.md).  

Mac istemcileri, bunları yöneten Configuration Manager sitesine otomatik olarak atanır. Mac istemcileri, iletişim intranet ile sınırlandırıldığı halde bile yalnızca Internet istemcileri olarak yüklenir. Bu yapılandırma, kendilerine atanan sitelerindeki İnternet etkin yönetim noktaları ve dağıtım noktalarıyla iletişim kurdukları anlamına gelir. Mac bilgisayarlar, kendilerine atanan siteleri dışındaki site sistemleriyle iletişim kurmaz.  

> [!IMPORTANT]  
>  MacOS için Configuration Manager istemcisi, [veritabanı çoğaltması](../../servers/deploy/configure/database-replicas-for-management-points.md)kullanmak üzere yapılandırılmış bir yönetim noktasına bağlanmak için kullanılamaz.  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Site sistemi sunucularına bir Web sunucusu sertifikası dağıtın  

Bu site sistemleri yoksa, bu site sistem rollerine sahip bilgisayarlara bir Web sunucusu sertifikası dağıtın:  

-   Yönetim noktası  

-   Dağıtım noktası  

-   Kayıt noktası  

-   Kayıt proxy noktası  

Web sunucusu sertifikası, site sistem özelliklerinde belirtilen Internet FQDN 'sini içermelidir. Mac bilgisayarlarını desteklemek için sunucunun internet 'ten erişilebilir olması gerekmez. Internet tabanlı istemci yönetimine ihtiyaç duymuyorsanız Internet FQDN 'si için intranet FQDN değerini belirtebilirsiniz.  

Yönetim noktası, dağıtım noktası ve kayıt proxy noktası için Web sunucusu sertifikasında site sisteminin Internet FQDN 'SI değerini belirtin.

Örnek bir dağıtım hakkında daha fazla bilgi için bkz. [IIS çalıştıran site sistemleri için Web sunucusu sertifikasını dağıtma](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Site sistem sunucularına bir istemci kimlik doğrulama sertifikası dağıtma  

Bu site sistemleri yoksa, bu site sistem rollerini barındıran bilgisayarlara bir istemci kimlik doğrulama sertifikası dağıtın:  

-   Yönetim noktası  

-   Dağıtım noktası  

Yönetim noktaları için istemci sertifikası oluşturan ve yükleyen örnek bir dağıtım için bkz. [Windows bilgisayarları için istemci sertifikasını dağıtma](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

Dağıtım noktaları için istemci sertifikası oluşturan ve yükleyen örnek bir dağıtım için bkz. [dağıtım noktaları için istemci sertifikasını dağıtma](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  İstemciyi macOS Sierra çalıştıran cihazlara dağıtmak için, yönetim noktası sertifikasının konu adı doğru şekilde yapılandırılmalıdır. Örneğin, yönetim noktası sunucusunun FQDN 'sini kullanın.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Mac için istemci sertifikası şablonunu hazırlama  

Sertifika şablonu, Mac bilgisayara sertifikayı kaydeden Kullanıcı hesabı için **okuma** ve **kaydetme** izinlerine sahip olmalıdır.  

Daha fazla bilgi için bkz. [Mac bilgisayarlar için istemci sertifikasını dağıtma](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Yönetim noktasını ve dağıtım noktasını yapılandırma  

Aşağıdaki seçenekler için yönetim noktalarını yapılandırın:  

-   HTTPS  

-   İnternet 'ten istemci bağlantılarına izin ver. Bu yapılandırma değeri Mac bilgisayarların yönetilmesi için gereklidir. Ancak, site sistem sunucularının Internet 'ten erişilebilir olması anlamına gelmez.  

-   Mobil aygıtların ve Mac bilgisayarların bu yönetim noktasını kullanmasına izin ver  

Mac istemcisini yüklemek için dağıtım noktaları gerekli değildir. İstemcisini yükledikten sonra bu bilgisayarlara yazılım dağıtmak istiyorsanız, dağıtım noktalarını Internet 'ten istemci bağlantılarına izin verecek şekilde yapılandırın.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Yönetim noktalarını ve dağıtım noktalarını, Mac 'ler destekleyecek şekilde yapılandırmak için  

Bu yordama başlamadan önce yönetim noktasını ve dağıtım noktasını bir Internet FQDN 'SI ile yapılandırdığınızdan emin olun. Bu sunucular Internet tabanlı istemci yönetimini desteklemiyorsa, intranet FQDN 'sini Internet FQDN değeri olarak belirtin.

Site sistemi rolleri bir birincil sitede olmalıdır.  

1.  Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **sunucular ve site sistemi rolleri** düğümünü seçin. Ardından, doğru site sistem rollerine sahip sunucuyu seçin.  

2.  Ayrıntılar bölmesinde, **Yönetim noktası** rolünü seçin ve Şeritteki **Özellikler** ' i seçin. **Yönetim noktası özellikleri** penceresinde, şu seçenekleri yapılandırın:  

    1.  **Https**seçin.  

    2.  **Yalnızca Internet istemci bağlantılarına Izin ver** veya **intranet ve Internet Istemci bağlantılarına izin ver ' i**seçin. Bu seçenekler için bir Internet veya intranet FQDN gerekir.  

    3.  **Mobil cihazların ve Mac bilgisayarların bu yönetim noktasını kullanmasına Izin ver '** i seçin.  

    4. Bu yapılandırmayı kaydetmek için **Tamam**’ı seçin.  

3.  Sunucu ve site sistemi rolleri düğümünün Ayrıntılar bölmesinde **dağıtım noktası** rolünü seçin ve Şeritteki **Özellikler** ' i seçin. **Dağıtım noktası özellikleri** penceresinde, şu seçenekleri yapılandırın:  

    -   **Https**seçin.  

    -   **Yalnızca Internet istemci bağlantılarına Izin ver** veya **intranet ve Internet Istemci bağlantılarına izin ver ' i**seçin. Bu seçenekler için bir Internet veya intranet FQDN gerekir.  

    -   **Sertifikayı Içeri aktar**' ı seçin, dışarı aktarılan istemci dağıtım noktası sertifika dosyasına gidin ve parolayı belirtin.  

4.  Mac bilgisayarları yöneten birincil sitelerdeki tüm yönetim noktaları ve dağıtım noktaları için bu yordamı tekrarlayın.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Kayıt proxy noktasını ve kayıt noktasını yapılandırma  

Her iki rolü de aynı siteye yükler. Bunları aynı site sistem sunucusuna veya aynı Active Directory ormanına yüklemek zorunda değilsiniz.  

Site sistemi rolü yerleşimi ve konuları hakkında daha fazla bilgi için bkz. [site sistemi rolleri](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles).  

Mac bilgisayarlarını desteklemek için site sistemi rolleri eklemek için bkz. [site sistemi rollerini yüklemek](../../servers/deploy/configure/install-site-system-roles.md).

**Sistem rolü seçimi** sayfasında, kullanılabilir roller listesinden **kaydolma proxy noktası** ve **kayıt noktası** ' nı seçin.  



## <a name="install-the-reporting-services-point"></a>Raporlama Hizmetleri noktasını yükler  

Daha fazla bilgi için bkz. [Reporting Services noktasını Install](../../servers/manage/configuring-reporting.md).  



## <a name="next-steps"></a>Sonraki adımlar

[Configuration Manager istemcisini Mac bilgisayarlara dağıtma](deploy-clients-to-macs.md)  
