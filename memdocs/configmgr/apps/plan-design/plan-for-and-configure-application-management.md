---
title: Uygulama yönetimini planlayın
titleSuffix: Configuration Manager
description: Configuration Manager uygulamaları dağıtmak için gerekli bağımlılıkları uygulayın ve yapılandırın.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709946"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Configuration Manager 'de uygulama yönetimini planlayın ve yapılandırın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager içinde uygulama dağıtmak üzere gerekli bağımlılıkları uygulamanıza yardımcı olması için bu makaledeki bilgileri kullanın.  



## <a name="dependencies-external-to-configuration-manager"></a>Bağımlılıklar dış Configuration Manager  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

Aşağıdaki site sistem rollerini çalıştıran sunucularda IIS gereklidir:

- Yönetim noktası  
- Dağıtım noktası  

Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

> [!Note]  
> Uygulama Kataloğu da IIS gerektirir. Ancak, Silverlight Kullanıcı deneyimi güncel dal sürümü 1806 itibariyle desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Mobil cihazlar için kod imzalı uygulamalarda sertifikalar

Uygulamaları mobil cihazlara dağıtmak üzere kodlayarak, sürüm 3 şablonu (**Windows Server 2008, Enterprise Edition**) kullanılarak oluşturulmuş bir sertifika kullanmayın. Bu sertifika şablonu, mobil cihazlar için Configuration Manager uygulamalarla uyumsuz bir sertifika oluşturur.

Mobil cihaz uygulamalarına yönelik kod imzalama uygulamalarında Active Directory Sertifika Hizmetleri kullanıyorsanız, sürüm 3 sertifika şablonu kullanmayın.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Kullanıcı cihaz benzeşimi için oturum açma olaylarını denetleme  

Otomatik olarak Kullanıcı aygıt benzeşimleri oluşturmak istiyorsanız, istemcileri oturum açma olaylarını denetleyecek şekilde yapılandırın.

Configuration Manager istemcisi, otomatik Kullanıcı aygıt benzeşimlerini belirlemekte, Windows Güvenlik olay günlüğünden **başarı** türündeki oturum açma olaylarını okur. Aşağıdaki iki denetim ilkesiyle bu olayları etkinleştirin:

- **Hesap oturumu açma olaylarını denetle**
- **Oturum açma olaylarını denetle**

Kullanıcılar ve aygıtlar arasında otomatik olarak ilişkiler oluşturmak için bu iki ayarın istemci bilgisayarlarında etkinleştirildiğinden emin olun. Bu ayarları yapılandırmak için Windows Grup İlkesi'ni kullanabilirsiniz.

Kullanıcı cihaz benzeşimi hakkında daha fazla bilgi için bkz. [Kullanıcı cihaz benzeşimi ile kullanıcıları ve cihazları bağlama](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  



## <a name="configuration-manager-dependencies"></a>Configuration Manager bağımlılıkları


### <a name="management-point"></a>Yönetim noktası

İstemciler, içerik bulmak için istemci ilkesini indirmek üzere bir yönetim noktasıyla iletişim kurun.

Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır.

Sürüm 1902 ve önceki sürümlerde istemciler, uygulama kataloğuna bağlanmak için yönetim noktasını kullanır. İstemciler bir yönetim noktasına erişeiyorlarsa uygulama kataloğunu kullanamaz.

> [!Note]  
> Sürüm 1806 ' den başlayarak, Kullanıcı tarafından kullanılabilen uygulamaları yazılım merkezi 'nde göstermek için uygulama kataloğu rollerinin artık gerekli değildir. Daha fazla bilgi için bkz. [Software Center 'ı yapılandırma](plan-for-software-center.md#bkmk_userex).<!--1358309-->  
>
> Sürüm 1906 ' den başlayarak yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
  

### <a name="distribution-point"></a>Dağıtım noktası

İstemcilere uygulama dağıtabilmeniz için önce hiyerarşide en az bir dağıtım noktasına ihtiyacınız vardır. Varsayılan olarak site sunucusu, standart bir yükleme sırasında etkinleştirilen bir dağıtım noktası site rolüne sahiptir. Dağıtım noktalarının sayısı ve konumu, ortamınızın özel gereksinimlerine göre farklılık gösterir.

Dağıtım noktalarının nasıl yükleneceği ve içeriğin nasıl yönetileceği hakkında daha fazla bilgi için bkz. [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="reporting-services-point"></a>Raporlama hizmetleri noktası

Raporları uygulama yönetimi için Configuration Manager ' de kullanmak için, önce bir raporlama hizmetleri noktası yükleyip yapılandırın.

Daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="client-settings"></a>İstemci ayarları

Birçok istemci ayarı, istemcinin uygulamaları nasıl yüklediğini ve cihazdaki kullanıcı deneyimini denetler. Bu istemci ayarları aşağıdaki grupları içerir:

- Bilgisayar Aracısı  
- Bilgisayar yeniden başlatma  
- Yazılım Merkezi  
- Yazılım dağıtımı  
- Kullanıcı ve cihaz benzeşimi  

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [İstemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md)  
- [İstemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Uygulama yönetimi için güvenlik izinleri

- **Uygulama yazarı** güvenlik rolü, uygulamaları oluşturmak, değiştirmek ve devre dışı bırakmak için gerekli izinleri içerir.  

- **Uygulama dağıtım Yöneticisi** güvenlik rolü, uygulamaları dağıtmak için gerekli izinleri içerir.  

- **Uygulama Yöneticisi** güvenlik rolü, **uygulama yazarı** ve **uygulama dağıtım Yöneticisi** güvenlik rollerinin tüm izinlerine sahiptir.  

Daha fazla bilgi için bkz. [rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>Sanal uygulamaları çalıştırmak için App-V 4.6 SP1 veya daha üst sürüm istemci

Configuration Manager ' de sanal uygulamalar oluşturmak için cihazlara App-V 4,6 SP1 veya sonraki bir sürümü yüklemelisiniz.

Sanal uygulamaları dağıtmadan önce, App-V istemcisini [Microsoft desteği makalesi 2645225](https://support.microsoft.com/help/2645225)' de açıklanan düzeltmeyle de güncelleştirin.  


### <a name="application-catalog"></a>Uygulama Kataloğu

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Uygulama Kataloğu Web hizmet noktası

Uygulama Kataloğu Web hizmet noktası, yazılım kitaplığınızdaki kullanılabilir yazılımlar hakkında kullanıcılara erişen uygulama Kataloğu Web sitesine bilgi sağlayan bir site sistem rolüdür.

Bu site sistemi rolünü yapılandırma hakkında daha fazla bilgi için, bkz. [Uygulama Kataloğu yükleyip yapılandırma](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Uygulama Kataloğu web sitesi noktası

Uygulama Kataloğu web sitesi noktası, kullanıcılara kullanılabilir yazılımların listesini sağlayan bir site sistem rolüdür.

Bu site sistemi rolünü yapılandırma hakkında daha fazla bilgi için, bkz. [Uygulama Kataloğu yükleyip yapılandırma](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Uygulama Kataloğu için bulunan Kullanıcı hesapları

Configuration Manager, kullanıcıların uygulama kataloğu 'ndan uygulamaları görüntüleyip isteyebilmesi için öncelikle Kullanıcı hesaplarını bulmalıdır. Daha fazla bilgi için bkz. [bulmayı çalıştırma](../../core/servers/deploy/configure/run-discovery.md).  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Yazılım merkezini yapılandırma  

Yazılım Merkezi 'ni yapılandırma ve markalama hakkında daha fazla bilgi için bkz. [plan for Software Center](plan-for-software-center.md).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a>Uygulama kataloğunu kaldırma

<!-- SCCMDocs-pr issue 3051 -->

Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [kaldırılan ve kullanım dışı Özellikler](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Aşağıdaki listede değişiklikler özetlenmektedir:

- Sürüm 1806 ' den başlayarak, Uygulama Kataloğu web sitesi noktası için **Silverlight Kullanıcı deneyimi** artık desteklenmemektedir.<!--1358309--> Uygulama Kataloğu Web hizmet noktası rolü artık *gerekli*değildir, ancak yine de *desteklenir*.

- Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz.

- Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  

Yazılım Merkezi ve yönetim noktası ile ilgili bu yinelemeli geliştirmeler, altyapınızı basitleştirecek ve Kullanıcı tarafından kullanılabilen dağıtımlar için uygulama kataloğu gereksinimini ortadan kaldıracak. Yazılım Merkezi, uygulama kataloğu olmadan tüm uygulama dağıtımlarını teslim edebilir. Ayrıca, TLS 1,2 'yi etkinleştirir ve Uygulama Kataloğu ile HTTP kullanırsanız, kullanıcılar kullanıcı hedefli, kullanılabilir dağıtımları göremez. Bu geliştirmelerden yararlanmak için Configuration Manager sürüm 1906 veya sonraki bir sürüme güncelleştirin.

1. Tüm istemcileri 1806 veya sonraki bir sürüme güncelleştirin. Sürüm 1906 önerilir.  

1. Uygulama Kataloğu web sitesi rolünün özellikleri yerine yazılım merkezi için marka belirleyin. Daha fazla bilgi için bkz. [Software Center istemci ayarları](../../core/clients/deploy/about-client-settings.md#software-center).  

1. Varsayılan ve tüm özel istemci ayarlarını gözden geçirin. **Bilgisayar Aracısı** grubunda, **Varsayılan Uygulama Kataloğu web sitesi noktasının** olduğundan emin olun `(none)`.  

    Sürüm 1902 ve önceki sürümlerde, istemci yalnızca hiyerarşide Uygulama Kataloğu rolü olmadığında yönetim noktasını kullanmaya geçer. Aksi takdirde, istemciler hiyerarşideki Uygulama Kataloğu örneklerinden birini kullanmaya devam eder. Bu davranış ayrı birincil siteler arasında geçerlidir.  

1. **Uygulama Kataloğu web sitesi** ve **Uygulama Kataloğu Web hizmeti** site sistem rollerini tüm birincil sitelerden kaldırın.

Uygulama Kataloğu rollerini kaldırdıktan sonra, yazılım merkezi kullanıcı hedefli, kullanılabilir dağıtımlar için yönetim noktasını kullanmaya başlar. Sürüm 1902 ve önceki sürümlerde bu değişikliğin gerçekleşmesi 65 dakikaya kadar sürebilir. Belirli bir istemcide bu davranışı doğrulamak için, `SCClient_<username>.log`öğesini gözden geçirin ve aşağıdaki satıra benzer bir giriş bulun:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a>Uygulama Kataloğu 'nu yükleyip yapılandırma  

> [!Important]  
> Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer. Daha fazla bilgi için bkz. [uygulama kataloğunu kaldırma](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>1. Adım: HTTPS için Web sunucusu sertifikası

HTTPS bağlantıları kullanıyorsanız, Uygulama Kataloğu web sitesi noktası ve Uygulama Kataloğu Web hizmet noktası için site sistem sunucularına bir Web sunucusu sertifikası dağıtın.

İstemcilerin uygulama kataloğunu Internet 'ten kullanmasını istiyorsanız, en az bir yönetim noktasına bir Web sunucusu sertifikası dağıtın. Internet 'ten istemci bağlantıları için yapılandırın.

Sertifika gereksinimleri hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-2-client-authentication-certificate-for-https"></a>2. Adım: HTTPS için Istemci kimlik doğrulama sertifikası

Yönetim noktalarına bağlantılar için bir istemci PKI sertifikası kullanıyorsanız, istemci bilgisayarlara bir istemci kimlik doğrulama sertifikası dağıtın. İstemciler Uygulama Kataloğu 'na bağlanmak için bir istemci PKI sertifikası kullanmasa da, uygulama kataloğu 'nu kullanabilmek için önce bir yönetim noktasına bağlanmaları gerekir.

Aşağıdaki senaryolarda istemci bilgisayarlara bir istemci kimlik doğrulama sertifikası dağıtın:

- İntranetteki tüm yönetim noktaları yalnızca HTTPS istemci bağlantılarını kabul eder.
- İstemciler, Internet 'ten Uygulama Kataloğu 'na bağlanır.

Sertifika gereksinimleri hakkında daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>3. Adım: Uygulama Kataloğu rollerini yükleyip yapılandırma

Uygulama Kataloğu Web hizmet noktasını ve Uygulama Kataloğu web sitesi rollerini aynı siteye yükler. Bunları aynı sunucuya veya aynı Active Directory ormana yüklemek zorunda değilsiniz. Ancak, Uygulama Kataloğu Web hizmet noktasının site veritabanıyla aynı ormanda olması gerekir.

Sunucu yerleşimi hakkında daha fazla bilgi için bkz. [plan sistem sunucuları ve site sistem rolleri Için plan](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

> [!NOTE]  
> Uygulama kataloğunu birincil bir siteye yükler. Bunu ikincil bir siteye veya merkezi yönetim sitesine yükleyemezsiniz.  

Uygulama kataloğunu yeni bir site sistemi sunucusuna veya sitedeki mevcut bir sunucuya yükler. Genel yordam hakkında daha fazla bilgi için bkz. [site sistemi rollerini yüklemeyi](../../core/servers/deploy/configure/install-site-system-roles.md). Bir site sistemi rolü eklemek veya bir site sistemi sunucusu oluşturmak için sihirbazda, listeden aşağıdaki rolleri seçin:  

- **Uygulama Kataloğu Web hizmet noktası**  
- **Uygulama Kataloğu web sitesi noktası**  

> [!TIP]  
> İstemci bilgisayarların uygulama kataloğunu Internet üzerinden kullanmasını istiyorsanız, Internet tam etki alanı adını (FQDN) belirtin.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Bu site sistemi rollerinin yüklenmesini doğrula  

- Durum iletileri: **SMS_PORTALWEB_CONTROL_MANAGER** ve **SMS_AWEBSVC_CONTROL_MANAGER**bileşenlerini kullanın.  

    Örneğin, **SMS_PORTALWEB_CONTROL_MANAGER** IÇIN durum kimliği **1015** , Uygulama Kataloğu web sitesi noktasını başarıyla yükleSite Bileşen Yöneticisi doğrular.  

- Günlük dosyaları: **SMSAWEBSVCSetup.log** ve **SMSPORTALWEBSetup.log** dosyalarını arayın.  

    Daha fazla bilgi için **awebsvcMSI. log** ve **Portlwebmsi. log** günlük dosyalarını arayın.  


### <a name="step-4-configure-client-settings"></a>4. Adım: istemci ayarlarını yapılandırma

Tüm kullanıcıların aynı ayarlara sahip olmasını istiyorsanız, varsayılan istemci ayarlarını yapılandırın. Tersi durumda, belirli koleksiyonlar için özel istemci ayarları yapılandırın.

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [İstemci ayarları hakkında](../../core/clients/deploy/about-client-settings.md)  
    - Bilgisayar Aracısı  
    - Bilgisayar yeniden başlatma  
    - Yazılım Merkezi  
    - Yazılım dağıtımı  
    - Kullanıcı ve cihaz benzeşimi  
- [İstemci ayarlarını yapılandırma](../../core/clients/deploy/configure-client-settings.md)  

Configuration Manager istemcisi, bir sonraki istemci ilkesini indirdiğinde cihazları bu ayarlarla yapılandırır. Tek bir istemci için ilke almayı tetiklemek için bkz. [istemcileri yönetme](../../core/clients/manage/manage-clients.md).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>5. Adım: uygulama kataloğunun çalışır durumda olduğunu doğrulama

Uygulama kataloğunun çalışır durumda olduğunu doğrulamak için aşağıdaki yordamları kullanın.

> [!NOTE]  
> Uygulama Kataloğu Kullanıcı deneyimi için Microsoft Silverlight gereklidir. Uygulama kataloğunu doğrudan bir tarayıcıdan kullanıyorsanız, önce bilgisayarda Microsoft Silverlight 'ın yüklü olduğunu doğrulayın.  

> [!TIP]  
> Eksik Önkoşullar, uygulama kataloğunun yüklemeden sonra yanlış çalışması için en yaygın nedenlerden arasındadır. Uygulama Kataloğu site sistem rolleri için rol önkoşullarını onaylayın. Daha fazla bilgi için bkz. [Site ve site sistem önkoşulları](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

Bir tarayıcıda, Uygulama Kataloğu web sitesinin adresini girin. Web sayfasının üç sekmeye ( **Uygulama Kataloğu**, **uygulama Isteklerim**ve **Cihazlarım**) görüntülendiğini onaylayın.  

Aşağıdaki listeden uygulama kataloğu için uygun adresi kullanın; burada `<server>` bilgisayar adı, intranet FQDN 'si veya Internet FQDN 'sidir:  

- HTTPS istemci bağlantıları ve varsayılan site sistemi rol ayarları:`https://<server>/CMApplicationCatalog`  

- HTTP istemci bağlantıları ve varsayılan site sistemi rol ayarları:`http://<server>/CMApplicationCatalog`  

- HTTPS istemci bağlantıları ve özel site sistemi rol ayarları:`https://<server>:<port>/<web application name>`  

- HTTP istemci bağlantıları ve özel site sistemi rol ayarları:`http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Cihazda bir etki alanı yönetici hesabıyla oturum açtıysanız Configuration Manager istemci bildirim iletilerini görüntülemez. Örneğin, yeni yazılımın kullanılabildiğini belirten iletiler.  
