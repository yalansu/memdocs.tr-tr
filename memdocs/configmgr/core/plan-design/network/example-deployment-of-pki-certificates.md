---
title: Örnek PKI sertifikası dağıtımı
titleSuffix: Configuration Manager
description: Configuration Manager kullandığı PKI sertifikalarının nasıl oluşturulacağını ve dağıtılacağını öğrenmek için adım adım bir örneği izleyin.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7781c20ca542d19c562574c554a08c38493911f6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700087"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-configuration-manager-windows-server-2008-certification-authority"></a>Configuration Manager için PKI sertifikalarının adım adım örnek dağıtımı: Windows Server 2008 sertifika yetkilisi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Windows Server 2008 sertifika yetkilisi (CA) kullanan Bu adım adım örnek dağıtım, Configuration Manager kullandığı ortak anahtar altyapısı (PKI) sertifikalarının nasıl oluşturulduğunu ve dağıtılacağını gösteren yordamlar içerir. Bu yordamlar, bir kuruluş sertifika yetkilisi (CA) ve sertifika şablonlarını kullanır. Adımlar, kanıt kavramı olarak, salt bir test ağı için uygundur.  

Gerekli sertifikalara yönelik tek bir dağıtım yöntemi olmadığından, bir üretim ortamı için gerekli sertifikaları dağıtmak üzere gerekli yordamlar ve en iyi uygulamalar için belirli PKI dağıtım belgelerinize başvurun. Sertifika gereksinimleri hakkında daha fazla bilgi için bkz. [Configuration Manager Için PKI sertifikası gereksinimleri](pki-certificate-requirements.md).  

> [!TIP]
> Bu konudaki yönergeleri, test ağı gereksinimleri bölümünde belgelenmeyen işletim sistemleri için uyarlayabilirsiniz. Ancak, sertifika veren CA 'yı Windows Server 2012 üzerinde çalıştırıyorsanız, sertifika şablonu sürümü sizden istenmez. Bunun yerine, şablon özelliklerinin **Uyumluluk** sekmesinde bunu belirtin:  
>
> - **Sertifika Yetkilisi**: **Windows Server 2003**  
>   - **Sertifika alıcısı**: **Windows XP / Server 2003**  

## <a name="test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> Test ağı gereksinimleri

Adım adım talimatlar aşağıdaki gereksinimlere sahiptir:  

- Test ağı, Windows Server 2008 ile Active Directory Etki Alanı Hizmetleri’ni çalıştırır ve tek bir etki alanı, tek bir orman olarak yüklenmiştir.  

- Üzerinde Active Directory Sertifika Hizmetleri rolü yüklü olan Windows Server 2008 Enterprise Edition çalıştıran bir üye sunucunuz vardır ve bir kuruluş kök sertifika yetkilisi (CA) olarak ayarlanır.  

- Üzerinde Windows Server 2008 (Standard Edition veya Enterprise Edition, R2 veya üzeri) yüklü bir bilgisayarınız var, bu bilgisayar üye sunucu olarak belirlenmiş ve Internet Information Services (IIS) bu bilgisayarda yüklü. Bu bilgisayar, intranet üzerindeki istemci bağlantılarını desteklemek için bir intranet tam etki alanı adı (FQDN) ve internet üzerindeki Configuration Manager ve istemciler tarafından kaydedilen mobil cihazları desteklemeniz gerekiyorsa bir İnternet FQDN 'si ile yapılandırabileceğiniz Configuration Manager site sistem sunucusudur.  

- En son hizmet paketinin yüklü olduğu bir Windows Vista istemciniz var ve bu bilgisayar ASCII karakterlerinden oluşan ve etki alanına katılmış bir bilgisayar adıyla ayarlanmış. Bu bilgisayar bir Configuration Manager istemci bilgisayarı olacaktır.  

- Bir kök etki alanı yönetici hesabıyla veya kuruluş etki alanı yönetici hesabıyla oturum açabilir ve bu hesabı bu örnek dağıtımdaki tüm yordamlar için kullanabilirsiniz.  

## <a name="overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> Sertifikalara genel bakış

Aşağıdaki tablo, Configuration Manager için gerekebilecek PKI sertifikalarının türlerini listeler ve bunların nasıl kullanıldığını açıklar.  

|Sertifika Gereksinimi|Sertifika Açıklaması|  
|-----------------------------|-----------------------------|  
|IIS çalıştıran site sistemleri için Web sunucusu sertifikası|Bu sertifika, verileri şifrelemek ve sunucuların istemcilere yetki doğrulamasını yapmak için kullanılır. Internet Information Services (IIS) çalıştıran ve HTTPS kullanacak şekilde Configuration Manager ayarlanan site sistemleri sunucularındaki Configuration Manager dışarıdan yüklenmelidir.<br /><br /> Bu sertifikayı ayarlama ve kurma adımları için, bkz. bu konuda [IIS çalıştıran site sistemleri için Web sunucusu sertifikasını dağıtma](#BKMK_webserver2008_cm2012) .|  
|Bulut tabanlı dağıtım noktalarına bağlanmak için istemcilere yönelik hizmet sertifikası|Bu sertifikayı yapılandırma ve yüklemeye yönelik adımlar için, bkz. bu konuda [bulut tabanlı dağıtım noktaları için hizmet sertifikası dağıtma](#BKMK_clouddp2008_cm2012) .<br /><br /> **Önemli** : Bu sertifika Windows Azure yönetim sertifikası ile birlikte kullanılır. Yönetim sertifikası hakkında daha fazla bilgi için bkz. [Yönetim sertifikası oluşturma](/azure/cloud-services/cloud-services-certs-create#create-a-new-self-signed-certificate) ve [Windows Azure aboneliğine yönetim sertifikası ekleme](/azure/cloud-services/cloud-services-configure-ssl-certificate-portal#step-3-upload-a-certificate).|  
|Windows bilgisayarlar için istemci sertifikası|Bu sertifika, HTTPS kullanacak şekilde ayarlanan site sistemlerine Configuration Manager istemci bilgisayarlarının kimliğini doğrulamak için kullanılır. Aynı zamanda, HTTPS kullanmak üzere ayarlandıklarında işletimsel durumlarını izlemek amacıyla yönetim noktaları ve durum geçiş noktaları için de kullanılabilir. Bilgisayarların Configuration Manager dışarıdan yüklenmesi gerekir.<br /><br /> Bu sertifikayı ayarlama ve yüklemeye yönelik adımlar için bu konudaki [Windows bilgisayarları için istemci sertifikasını dağıtma](#BKMK_client2008_cm2012) bölümüne bakın.|  
|Dağıtım noktaları için istemci sertifikası|Bu sertifika iki amaca sahiptir:<br /><br /> Bu sertifika, dağıtım noktası durum iletileri göndermeden önce HTTPS etkin bir yönetim noktasına dağıtım noktasının kimliğini doğrulamak amacıyla kullanılır.<br /><br /> **İstemciler için PXE desteğini etkinleştir** dağıtım noktası seçeneği seçildiğinde, sertifika, işletim sisteminin dağıtımı sırasında bir HTTPS etkin yönetim noktasına bağlanabilmeleri için PXE önyüklemesi gerçekleştiren bilgisayarlara gönderilir.<br /><br /> Bu sertifikayı ayarlama ve kurma adımları için bu konudaki [dağıtım noktaları için istemci sertifikasını dağıtma](#BKMK_clientdistributionpoint2008_cm2012) bölümüne bakın.|  
|Mobil aygıtlar için kayıt sertifikası|Bu sertifika, HTTPS kullanacak şekilde ayarlanan site sistemlerine Configuration Manager mobil cihaz istemcilerinin kimliğini doğrulamak için kullanılır. Configuration Manager mobil cihaz kaydının bir parçası olarak yüklenmelidir ve yapılandırılmış sertifika şablonunu bir mobil aygıt istemci ayarı olarak seçersiniz.<br /><br /> Bu sertifikayı ayarlama adımları için bu konudaki [mobil cihazlar için kayıt sertifikasını dağıtma](#BKMK_mobiledevices2008_cm2012) bölümüne bakın.|  
|Mac bilgisayarlar için istemci sertifikası|Configuration Manager kaydını kullandığınızda ve yapılandırılmış sertifika şablonunu bir mobil aygıt istemci ayarı olarak seçtiğinizde, bu sertifikayı bir Mac bilgisayardan isteyebilir ve yükleyebilirsiniz.<br /><br /> Bu sertifikayı ayarlama adımları için bu konudaki [Mac bilgisayarlar için istemci sertifikasını dağıtma](#BKMK_MacClient_SP1) bölümüne bakın.|  

## <a name="deploy-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> IIS çalıştıran site sistemleri için Web sunucusu sertifikasını dağıtma

Sertifika dağıtımı aşağıdaki yordamlara sahiptir:  

- Sertifika yetkilisinde Web sunucusu sertifika şablonu oluşturma ve verme  

- Web sunucusu sertifikası isteme  

- IIS 'yi Web sunucusu sertifikasını kullanacak şekilde yapılandırma  

### <a name="create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> Sertifika yetkilisinde Web sunucusu sertifika şablonu oluşturma ve verme

Bu yordam Configuration Manager site sistemleri için bir sertifika şablonu oluşturur ve sertifika yetkilisine ekler.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Sertifika yetkilisinde Web sunucusu sertifika şablonu oluşturmak ve vermek için

1.  IIS 'yi çalıştıracak Configuration Manager site sistemlerini yüklemek için üye sunucuları içeren **CONFIGMGR IIS sunucuları** adlı bir güvenlik grubu oluşturun.  

2.  Sertifika **şablonları** konsolunu yüklemek Için Sertifika Hizmetleri 'nin yüklü olduğu üye sunucusunda, sertifika yetkilisi konsolunda, **sertifika şablonları** ' na sağ tıklayın ve **Yönet** ' i seçin.  

3.  Sonuçlar bölmesinde, **şablon görünen adı** sütununda **Web sunucusu** olan girdiye sağ tıklayın ve ardından **Yinelenen şablon**' u seçin.  

4.  **Yinelenen şablon** Iletişim kutusunda **Windows 2003 Server, Enterprise Edition** ' ın seçili olduğundan emin olun ve ardından **Tamam**' ı seçin.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition ' ı**seçmeyin.  

5.  **Yeni Şablon Özellikleri** iletişim kutusunda, **genel** sekmesinde, Configuration Manager site sistemlerinde kullanılacak web sertifikalarını oluşturmak Için **ConfigMgr Web sunucusu sertifikası**gibi bir şablon adı girin.  

6.  **Konu adı** sekmesini seçin ve **istekteki tedarikin** seçildiğinden emin olun.  

7.  **Güvenlik** sekmesini seçin ve ardından **etki alanı yöneticileri** ve **Enterprise Admins** güvenlik gruplarından **kaydetme** iznini kaldırın.  

8.  **Ekle**' yi seçin, metin kutusuna **ConfigMgr IIS sunucuları** girin ve ardından **Tamam**' ı seçin.  

9. Bu grup için **kaydetme** iznini seçin ve **okuma** izninin işaretini kaldırmayın.  

10. **Tamam**' ı seçin ve ardından **Sertifika Şablonları konsolunu**kapatın.  

11. Sertifika Yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın, **Yeni**' yi seçin ve ardından **verilecek sertifika şablonu**' nu seçin.  

12. **Sertifika şablonlarını etkinleştir** iletişim kutusunda, az önce oluşturduğunuz yeni **ConfigMgr Web sunucusu sertifikası**şablonunu seçtikten sonra **Tamam**' ı seçin.  

13. Daha fazla sertifika oluşturmanız ve bu sertifikaların verilgerekmiyorsa **sertifika yetkilisi**' ni kapatın.  

###  <a name="request-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> Web sunucusu sertifikası isteme  
 Bu yordam, site sistem sunucusu özelliklerinde ayarlanacak intranet ve İnternet FQDN değerlerini belirtmenizi sağlar ve ardından Web sunucusu sertifikasını IIS çalıştıran üye sunucuya kurar.  

##### <a name="to-request-the-web-server-certificate"></a>Web sunucusu sertifikası istemek için  

1.  Bilgisayarın, yapılandırdığınız **okuma** ve **kaydetme** izinlerini kullanarak oluşturduğunuz sertifika şablonuna ERIŞEBILDIĞINDEN emin olmak için IIS çalıştıran üye sunucuyu yeniden başlatın.  

2.  **Başlat**' ı seçin, **Çalıştır**' ı seçin ve ardından **mmc.exe yazın.** Boş konsolda **Dosya**' yı seçin ve **ek bileşen Ekle/Kaldır**' ı seçin.  

3.  **Ek bileşenler Ekle/Kaldır** Iletişim kutusunda **kullanılabilir ek bileşenler**listesinden **Sertifikalar** ' ı seçin ve ardından **Ekle**' yi seçin.  

4.  **Sertifika ek bileşeni** Iletişim kutusunda **bilgisayar hesabı**' nı seçin ve ardından **İleri**' yi seçin.  

5.  **Bilgisayar Seç** iletişim kutusunda, **Yerel bilgisayar: (bu konsolun üzerinde çalıştığı bilgisayar)** ' ın seçili olduğundan emin olun ve ardından **son**' u seçin.  

6.  **Ek bileşenler Ekle veya Kaldır** Iletişim kutusunda **Tamam**' ı seçin.  

7.  Konsolunda, **Sertifikalar (yerel bilgisayar)**' ı genişletin ve **Kişisel**' i seçin.  

8.  **Sertifikalar**' a sağ tıklayın, **Tüm görevler**' i seçin ve ardından **Yeni sertifika iste**' yi seçin.  

9. **Başlamadan önce** sayfasında **İleri**' yi seçin.  

10. **Sertifika kayıt Ilkesi Seç** sayfasını görürseniz **İleri**' yi seçin.  

11. Sertifika **iste** sayfasında, kullanılabilir sertifikalar listesinden **ConfigMgr Web sunucusu sertifikası** ' nı belirleyin ve **Bu sertifikaya kaydolmak için daha fazla bilgi gerekiyor ' u seçin. Ayarları yapılandırmak için buraya tıklayın**.  

12. **Sertifika özellikleri** iletişim kutusunda, **Konu** sekmesinde **Konu adı**' nda herhangi bir değişiklik yapmayın. Bu, **Konu adı** bölümünün **Değer** kutusunun boş kalacağı anlamına gelir. Bunun yerine, **Alternatif ad** bölümünde **tür** açılan listesini seçin ve **DNS**' yi seçin.  

13. **Değer** kutusunda, Configuration Manager site sistem ÖZELLIKLERINDE belirleyeceğiniz FQDN değerlerini belirtin ve ardından **Tamam** ' ı seçerek **sertifika özellikleri** iletişim kutusunu kapatın.  

     Örnekler:  

    - Site sistemi yalnızca intranetten gelen istemci bağlantılarını kabul edecektir ve site sistem sunucusunun intranet FQDN 'SI **server1.internal.contoso.com**ise, **server1.internal.contoso.com**yazın ve ardından **Ekle**' yi seçin.  

    - Site sistemi intranetten ve internet 'ten istemci bağlantılarını kabul edecektir ve site sistem sunucusunun intranet FQDN 'SI **server1.internal.contoso.com** ise ve site sistem sunucusunun İnternet fqdn 'si **Server.contoso.com**ise:  

        1.  **Server1.internal.contoso.com**girin ve ardından **Ekle**' yi seçin.  

        2.  **Server.contoso.com**girin ve ardından **Ekle**' yi seçin.  

        > [!NOTE]  
        >  Configuration Manager için FQDN 'leri dilediğiniz sırada belirtebilirsiniz. Ancak, sertifikayı kullanacak mobil aygıtlar ve proxy Web sunucuları gibi tüm cihazların bir sertifika konu alternatif adı (SAN) ve SAN 'da birden çok değer kullanmasını sağlayabilirsiniz. Aygıtlarda sertifikalarda SAN değerleri için sınırlı destek varsa, FQDN'lerin sırasını değiştirmek veya bunun yerine Konu değerini kullanmak isteyebilirsiniz.  

14. **Sertifika iste** sayfasında, kullanılabilir sertifikalar listesinden **ConfigMgr Web sunucusu sertifikası** ' nı seçin ve ardından **Kaydet**' i seçin.  

15. **Sertifikalar yükleme sonuçları** sayfasında, sertifika yüklenene kadar bekleyin ve ardından **son**' u seçin.  

16. **Sertifikalar (Yerel Bilgisayar)**'ı kapatın.  

###  <a name="configure-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> IIS 'yi Web sunucusu sertifikasını kullanacak şekilde yapılandırma  
 Bu yordam, yüklü sertifikayı IIS **Varsayılan Web Sitesi**'ne bağlar.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>IIS 'yi Web sunucusu sertifikasını kullanacak şekilde ayarlamak için  

1. IIS yüklü üye sunucusunda **Başlat**' ı seçin, **Programlar**' ı seçin, **Yönetimsel Araçlar**' ı seçin ve ardından **Internet Information Services (IIS) Yöneticisi**' ni seçin.  

2. **Siteler**' i genişletin, **varsayılan Web sitesi**' ne sağ tıklayın ve ardından **bağlamaları Düzenle**' yi seçin.  

3. **Https** girişini seçin ve ardından **Düzenle**' yi seçin.  

4. **Site Bağlamasını Düzenle** iletişim kutusunda, ConfigMgr Web sunucusu sertifikaları şablonunu kullanarak istediğiniz sertifikayı seçin ve ardından **Tamam**' ı seçin.  

   > [!NOTE]  
   >  Doğru sertifikanın hangisi olduğundan emin değilseniz, bir tane seçin ve ardından **görüntüle**' yi seçin. Bu, seçili sertifika ayrıntılarını Sertifikalar ek bileşenindeki sertifikalarla karşılaştırmanıza imkan tanır. Örneğin, Sertifikalar ek bileşeni sertifika istemek için kullanılan sertifika şablonunu gösterir. Daha sonra ConfigMgr Web sunucusu sertifikaları şablonunu kullanarak istenen sertifikanın sertifika parmak izini, **Site Bağlamasını Düzenle** iletişim kutusunda şu anda seçili olan sertifikanın sertifika parmak izine göre karşılaştırabilirsiniz.  

5. **Site Bağlamasını Düzenle** Iletişim kutusunda **Tamam** ' ı seçin ve ardından **Kapat**' ı seçin.  

6. **Internet Information Services (IIS) Yöneticisi 'ni**kapatın.  

   Üye sunucu artık Configuration Manager bir Web sunucusu sertifikası ile ayarlanır.  

> [!IMPORTANT]  
>  Bu bilgisayara Configuration Manager site sistem sunucusunu yüklediğinizde, site sistem özelliklerinde FQDN 'leri sertifikayı istediğinizde belirtdiklerinizle aynı şekilde belirttiğinizden emin olun.  

##  <a name="deploy-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> Bulut tabanlı dağıtım noktaları için hizmet sertifikası dağıtma  

Sertifika dağıtımı aşağıdaki yordamlara sahiptir:  

- [Sertifika yetkilisinde özel Web sunucusu sertifika şablonu oluşturma ve verme](#BKMK_clouddpcreating2008)  

- [Özel Web sunucusu sertifikası isteme](#BKMK_clouddprequesting2008)  

- [Bulut tabanlı dağıtım noktaları için özel Web sunucusu sertifikasını dışarı aktarma](#BKMK_clouddpexporting2008)  

###  <a name="create-and-issue-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> Sertifika yetkilisinde özel Web sunucusu sertifika şablonu oluşturma ve verme  
 Bu yordam, Web sunucusu sertifika şablonunu temel alan özel bir sertifika şablonu oluşturur. Sertifika, bulut tabanlı Configuration Manager dağıtım noktalarına yöneliktir ve özel anahtar dışarı aktarılabilir olmalıdır. Sertifika şablonu oluşturulduktan sonra sertifika yetkilisine eklenir.  

> [!NOTE]
>  Bu yordam, IIS çalıştıran site sistemleri için oluşturduğunuz Web sunucusu sertifika şablonundan farklı bir sertifika şablonu kullanır. Her iki sertifika da sunucu kimlik doğrulama özelliği gerektirse de, bulut tabanlı dağıtım noktalarına yönelik sertifika, konu adı için özel tanımlanmış bir değer girmenizi gerektirir ve özel anahtar aktarılmalıdır. En iyi güvenlik uygulaması olarak, bu yapılandırma gerekmediği sürece özel anahtarın verilebilmesi için sertifika şablonları ayarlamayın. Sertifikayı sertifika deposundan seçmek yerine bir dosya olarak içeri aktarmanız gerektiğinden bulut tabanlı dağıtım noktası bu yapılandırmayı gerektirir.  
> 
>  Bu sertifika için yeni bir sertifika şablonu oluşturduğunuzda, özel anahtarı verilebilecek bir sertifika isteyebilecek bilgisayarları kısıtlayabilirsiniz. Bir üretim ağında, bu sertifika için aşağıdaki değişiklikleri eklemeyi de düşünebilirsiniz:  
> 
> - Ek güvenlik için sertifikayı yüklemek üzere onay gerektir.  
>   - Sertifika geçerlilik süresini artırın. Sertifikayı, süresi dolmadan her seferinde dışarı ve içeri aktarmanız gerektiğinden, geçerlilik süresinin artırılması bu yordamı yinelemeniz gereken sıklığı azaltır. Ancak, bir saldırganın özel anahtarın şifresini çözmesini ve sertifikayı çalmasını daha fazla zaman sağladığından, geçerlilik süresinin bir artışı sertifikanın güvenliğini de düşürür.  
>   - Bu sertifikayı IIS ile kullandığınız standart Web sunucusu sertifikaları arasından tanımaya yardımcı olması için sertifikanın Konu Diğer Adında (SAN) özel bir değer kullanın.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Sertifika yetkilisinde özel Web sunucusu sertifika şablonu oluşturmak ve vermek için  

1.  Bulut tabanlı dağıtım noktalarını yönetecek Configuration Manager birincil site sunucularını yüklemek için üye sunucuları içeren **ConfigMgr Site sunucuları** adlı bir güvenlik grubu oluşturun.  

2.  Sertifika şablonları yönetim konsolunu yüklemek için Sertifika Yetkilisi konsolunu çalıştıran üye sunucusunda, **sertifika şablonları**' na sağ tıklayın ve **Yönet** ' i seçin.  

3.  Sonuçlar bölmesinde, **şablon görünen adı** sütununda **Web sunucusu** olan girdiye sağ tıklayın ve ardından **Yinelenen şablon**' u seçin.  

4.  **Yinelenen şablon** Iletişim kutusunda **Windows 2003 Server, Enterprise Edition** ' ın seçili olduğundan emin olun ve ardından **Tamam**' ı seçin.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition ' ı**seçmeyin.  

5.  **Yeni Şablon Özellikleri** iletişim kutusunda, **genel** sekmesinde, bulut tabanlı dağıtım noktalarına yönelik Web sunucusu sertifikasını oluşturmak Için **ConfigMgr bulut tabanlı dağıtım noktası sertifikası**gibi bir şablon adı girin.  

6.  **Istek işleme** sekmesini seçin ve ardından **özel anahtarın verilmesine izin ver**' i seçin.  

7.  **Güvenlik** sekmesini seçin ve ardından **Enterprise Admins** güvenlik grubundan **kaydetme** iznini kaldırın.  

8.  **Ekle**' yi seçin, metin kutusuna **ConfigMgr Site sunucuları** yazın ve ardından **Tamam**' ı seçin.  

9. Bu grup için **Kaydetme** iznini seçin ve **Okuma** izninin işaretini kaldırmayın.  

10. **Şifreleme** sekmesini seçin ve **Minimum anahtar boyutunun** **2048**olarak ayarlandığından emin olun.

11. **Tamam**' ı ve ardından **Sertifika Şablonları konsolunu**Kapat ' ı seçin.  

12. Sertifika Yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın, **Yeni**' yi seçin ve ardından **verilecek sertifika şablonu**' nu seçin.  

13. **Sertifika şablonlarını etkinleştir** iletişim kutusunda, az önce oluşturduğunuz yeni **ConfigMgr bulut tabanlı dağıtım noktası Sertifikası**şablonunu seçtikten sonra **Tamam**' ı seçin.  

14. Daha fazla sertifika oluşturmanız ve bu sertifikaya ihtiyacınız yoksa **sertifika yetkilisi**' ni kapatın.  

###  <a name="request-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> Özel Web sunucusu sertifikası isteme  
 Bu yordam, site sunucusunu çalıştıracak üye sunucuya özel Web sunucusu sertifikasını ister ve sonra kurar.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Özel Web sunucusu sertifikası istemek için  

1.  Bilgisayarın, yapılandırdığınız **okuma** ve **kaydetme** izinlerini kullanarak oluşturduğunuz sertifika şablonuna erişebildiğinden emin olmak için **ConfigMgr Site sunucuları** güvenlik grubunu oluşturduktan ve yapılandırdıktan sonra üye sunucuyu yeniden başlatın.  

2.  **Başlat**' ı seçin, **Çalıştır**' ı seçin ve ardından **mmc.exe girin.** Boş konsolda **Dosya**' yı seçin ve **ek bileşen Ekle/Kaldır**' ı seçin.  

3.  **Ek bileşenler Ekle/Kaldır** Iletişim kutusunda **kullanılabilir ek bileşenler**listesinden **Sertifikalar** ' ı seçin ve ardından **Ekle**' yi seçin.  

4.  **Sertifika ek bileşeni** Iletişim kutusunda **bilgisayar hesabı**' nı seçin ve ardından **İleri**' yi seçin.  

5.  **Bilgisayar Seç** iletişim kutusunda, **Yerel bilgisayar: (bu konsolun üzerinde çalıştığı bilgisayar)** ' ın seçili olduğundan emin olun ve ardından **son**' u seçin.  

6.  **Ek bileşenler Ekle veya Kaldır** Iletişim kutusunda **Tamam**' ı seçin.  

7.  Konsolunda, **Sertifikalar (yerel bilgisayar)**' ı genişletin ve **Kişisel**' i seçin.  

8.  **Sertifikalar**' a sağ tıklayın, **Tüm görevler**' i seçin ve ardından **Yeni sertifika iste**' yi seçin.  

9. **Başlamadan önce** sayfasında **İleri**' yi seçin.  

10. **Sertifika kayıt Ilkesi Seç** sayfasını görürseniz **İleri**' yi seçin.  

11. Sertifika **iste** sayfasında, kullanılabilir sertifikalar listesinden **ConfigMgr bulut tabanlı dağıtım noktası sertifikası** ' nı belirleyin ve **Bu sertifikaya kaydolmak için daha fazla bilgi gerekiyor. ayarları yapılandırmak için buraya tıklayın**.  

12. **Sertifika özellikleri** iletişim kutusunda, **Konu sekmesinde** **Konu adı**için, **tür**olarak **ortak ad** ' ı seçin.  

13. **Değer** kutusunda, FQDN biçimini kullanarak hizmet adı ve etki alanı adı seçiminizi belirtin. Örneğin: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Hizmet adını ad alanınız içinde benzersiz yapın. Bu hizmet adını Windows Azure'den otomatik olarak oluşturulan tanımlayıcı (GUID) ve IP adresi ile eşleştirmek için DNS kullanarak diğer adı (CNAME kaydı) oluşturursunuz.  

14. **Ekle**' yi seçin ve ardından **sertifika özellikleri** Iletişim kutusunu kapatmak için **Tamam** ' ı seçin.  

15. **Sertifika iste** sayfasında, kullanılabilir sertifikalar listesinden **ConfigMgr bulut tabanlı dağıtım noktası sertifikası** ' nı seçin ve ardından **Kaydet**' i seçin.  

16. **Sertifikalar yükleme sonuçları** sayfasında, sertifika yüklenene kadar bekleyin ve ardından **son**' u seçin.  

17. **Sertifikalar (Yerel Bilgisayar)**'ı kapatın.  

###  <a name="export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> Bulut tabanlı dağıtım noktaları için özel Web sunucusu sertifikasını dışarı aktarma  
 Bu yordam, bulut tabanlı dağıtım noktasını oluşturduğunuzda özel Web sunucusu sertifikasının içeri aktarılabilmesi için onu dosyaya aktarır.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Bulut tabanlı dağıtım noktalarına yönelik özel Web sunucusu sertifikasını dışarı aktarmak için  

1. **Sertifikalar (yerel bilgisayar)** konsolunda, yeni yüklediğiniz sertifikaya sağ tıklayın, **Tüm görevler**' i seçin ve ardından **dışarı aktar**' ı seçin.  

2. Sertifika dışarı aktarma sihirbazında **İleri**' yi seçin.  

3. **Özel anahtarı dışarı aktar** sayfasında **Evet, özel anahtarı dışarı aktar**' ı seçin ve ardından **İleri**' yi seçin.  

   > [!NOTE]  
   >  Bu seçenek kullanılamıyorsa, sertifika özel anahtarı dışarı aktarma seçeneği olmadan oluşturulmuştur. Bu senaryoda, sertifikayı gereken biçimde dışarı aktaramazsınız. Özel anahtarın verilebilmesi için sertifika şablonunu ayarlamanız ve ardından sertifikayı yeniden istemeniz gerekir.  

4. **Dışarı aktarma dosyası biçimi** sayfasında **Kişisel BILGI değişimi-PKCS #12 (. PFX)** seçeneği seçilidir.  

5. **Parola** sayfasında, verdiğiniz sertifikayı özel anahtarıyla korumak için güçlü bir parola belirtin ve ardından **İleri**' yi seçin.  

6. **Dışarı aktarılacak dosya** sayfasında, dışarı aktarmak istediğiniz dosyanın adını belirtin ve ardından **İleri**' yi seçin.  

7. Sihirbazı kapatmak için, **sertifika dışarı aktarma Sihirbazı** sayfasında **son** ' u seçin ve ardından onay iletişim kutusunda **Tamam** ' ı seçin.  

8. **Sertifikalar (Yerel Bilgisayar)**'ı kapatın.  

9. Dosyayı güvenli bir şekilde depolayın ve Configuration Manager konsolundan erişiminizin olduğundan emin olun.  

   Sertifika artık bulut tabanlı dağıtım noktasını oluşturduğunuzda içeri aktarılmaya hazırdır.  

##  <a name="deploy-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Windows bilgisayarları için istemci sertifikasını dağıtma  
 Sertifika dağıtımı aşağıdaki yordamlara sahiptir:  

- Sertifika yetkilisinde Iş Istasyonu kimlik doğrulama sertifika şablonu oluşturma ve verme  

- grup ilkesi kullanarak Iş Istasyonu kimlik doğrulama şablonunun otomatik kaydını yapılandırın  

- Iş Istasyonu kimlik doğrulama sertifikasını otomatik olarak kaydetme ve bilgisayarlara yüklenmesini doğrulama  

###  <a name="create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> Sertifika yetkilisinde Iş Istasyonu kimlik doğrulama sertifika şablonu oluşturma ve verme  
 Bu yordam Configuration Manager istemci bilgisayarları için bir sertifika şablonu oluşturur ve sertifika yetkilisine ekler.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Sertifika yetkilisinde İş İstasyonu Kimlik Doğrulama sertifika şablonu oluşturmak ve vermek için  

1.  Sertifika şablonları yönetim konsolunu yüklemek için Sertifika Yetkilisi konsolunu çalıştıran üye sunucusunda, **sertifika şablonları**' na sağ tıklayın ve **Yönet** ' i seçin.  

2.  Sonuçlar bölmesinde, **şablon görünen adı** sütununda **Iş istasyonu kimlik doğrulaması** olan girdiye sağ tıklayın ve ardından **Yinelenen şablon**' u seçin.  

3.  **Yinelenen şablon** Iletişim kutusunda **Windows 2003 Server, Enterprise Edition** ' ın seçili olduğundan emin olun ve ardından **Tamam**' ı seçin.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition ' ı**seçmeyin.  

4.  **Yeni Şablon Özellikleri** iletişim kutusunda, **genel** sekmesinde, Configuration Manager istemci bilgisayarlarında kullanılacak Istemci sertifikalarını oluşturmak için **ConfigMgr istemci sertifikası**gibi bir şablon adı girin.  

5.  **Güvenlik** sekmesini seçin, **etki alanı bilgisayarları** grubunu seçin ve ardından **Oku** ve **otomatik kayıt**ek izinlerini seçin. **Kaydetme**'yi silmeyin.  

6.  **Tamam**' ı ve ardından **Sertifika Şablonları konsolunu**Kapat ' ı seçin.  

7.  Sertifika Yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın, **Yeni**' yi seçin ve ardından **verilecek sertifika şablonu**' nu seçin.  

8.  **Sertifika şablonlarını etkinleştir** iletişim kutusunda, az önce oluşturduğunuz yeni **ConfigMgr İstemci Sertifikası**şablonunu seçtikten sonra **Tamam**' ı seçin.  

9. Daha fazla sertifika oluşturmanız ve bu sertifikaların verilgerekmiyorsa **sertifika yetkilisi**' ni kapatın.  

###  <a name="configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> grup ilkesi kullanarak Iş Istasyonu kimlik doğrulama şablonunun otomatik kaydını yapılandırın  
 Bu yordam, bilgisayarlardaki istemci sertifikasını otomatik olarak kaydetmek için grup ilkesi ayarlar.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>grup ilkesi kullanarak Iş Istasyonu kimlik doğrulama şablonunun otomatik kaydını ayarlamak için  

1.  Etki alanı denetleyicisinde, **Başlat**' ı seçin, **Yönetim Araçları**' nı seçin ve sonra **Grup İlkesi Yönetim**' i seçin.  

2.  Etki alanına gidin, etki alanına sağ tıklayın ve **Bu etki alanında GPO oluştur ve buraya bağla**' yı seçin.  

    > [!NOTE]  
    >  Bu adım, en iyi uygulama olarak Active Directory Etki Alanı Hizmetleri ile birlikte yüklenen Varsayılan Etki Alanı İlkesini düzenlemek yerine özel ayarlar için yeni bir Grup İlkesi oluşturmayı kullanır. Bu grup ilkesi etki alanı düzeyinde atadığınızda, bunu etki alanındaki tüm bilgisayarlara uygularsınız. Bir üretim ortamında, otomatik kaydı yalnızca seçilen bilgisayarlara kaydolur şekilde kısıtlayabilirsiniz. Grup ilkesi bir kuruluş birimi düzeyinde atayabilir veya etki alanı grup ilkesi bir güvenlik grubuyla filtreleyerek yalnızca gruptaki bilgisayarlara uygulanabilmesi gerekir. Otomatik kaydı kısıtladığınızda, yönetim noktası olarak ayarlanan sunucuyu eklemeyi unutmayın.  

3.  **Yenı GPO** iletişim kutusunda, yeni Grup İlkesi Için **otomatik kayıt sertifikaları**gibi bir ad girin ve ardından **Tamam**' ı seçin.  

4.  Sonuçlar bölmesinde, **bağlı Grup İlkesi nesneleri** sekmesinde, yeni Grup İlkesi sağ tıklatın ve ardından **Düzenle**' yi seçin.  

5.  **Grup İlkesi Yönetimi Düzenleyicisi**, **bilgisayar yapılandırması**altında **ilkeler** ' i genişletin ve ardından **Windows ayarları**  /  **güvenlik ayarları**  /  **ortak anahtar ilkeleri**' ne gidin.  

6.  **Sertifika Hizmetleri istemcisi-otomatik kayıt**adlı nesne türüne sağ tıklayın ve ardından **Özellikler**' i seçin.  

7.  **Yapılandırma modeli** açılan listesinden, **etkin**' i seçin, süre sonu **sertifikalarını Yenile, bekleyen sertifikaları güncelleştir, iptal edilen sertifikaları kaldır**' ı seçin, **sertifika şablonlarını kullanan sertifikaları güncelleştir**' i seçin ve ardından **Tamam**' ı seçin.  

8.  **Grup İlkesi Yönetimi**'ni kapatın.  

###  <a name="automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-computers"></a><a name="BKMK_client22008"></a> Iş Istasyonu kimlik doğrulama sertifikasını otomatik olarak kaydetme ve bilgisayarlara yüklenmesini doğrulama  
 Bu yordam, istemci sertifikasını bilgisayarlara yükler ve yüklemeyi doğrular.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Iş Istasyonu kimlik doğrulama sertifikasını otomatik olarak kaydetmek ve istemci bilgisayara yüklenmesini doğrulamak için  

1. İş istasyonu bilgisayarını yeniden başlatın ve oturum açmadan önce birkaç dakika bekleyin.  

   > [!NOTE]  
   >  Bilgisayarı yeniden başlatmak, otomatik sertifika kaydında başarılı olmayı sağlayan en güvenilir yöntemdir.  

2. Yönetici ayrıcalıklarına sahip bir hesapla oturum açın.  

3. Arama kutusuna **mmc.exe.** **yazın ve ENTER tuşuna basın**.  

4. Boş yönetim konsolunda **Dosya**' yı seçin ve **ek bileşen Ekle/Kaldır**' ı seçin.  

5. **Ek bileşenler Ekle/Kaldır** Iletişim kutusunda **kullanılabilir ek bileşenler**listesinden **Sertifikalar** ' ı seçin ve ardından **Ekle**' yi seçin.  

6. **Sertifika ek bileşeni** Iletişim kutusunda **bilgisayar hesabı**' nı seçin ve ardından **İleri**' yi seçin.  

7. **Bilgisayar Seç** iletişim kutusunda, **Yerel bilgisayar: (bu konsolun üzerinde çalıştığı bilgisayar)** ' ın seçili olduğundan emin olun ve ardından **son**' u seçin.  

8. **Ek bileşenler Ekle veya Kaldır** Iletişim kutusunda **Tamam**' ı seçin.  

9. Konsolunda, **Sertifikalar (yerel bilgisayar)**' ı genişletin, **Kişisel**' i genişletin ve ardından **Sertifikalar**' ı seçin.  

10. Sonuçlar bölmesinde, bir sertifikanın **Hedeflenen amaç** sütununda **istemci kimlik doğrulamasına** sahip olduğunu ve **ConfigMgr Istemci sertifikası** ' nın **sertifika şablonu** sütununda olduğunu doğrulayın.  

11. **Sertifikalar (Yerel Bilgisayar)**'ı kapatın.  

12. Yönetim noktası olarak ayarlanacak sunucunun da bir istemci sertifikası olduğunu doğrulamak için üye sunucu için 1 ile 11 arasındaki adımları yineleyin.  

    Bilgisayar artık Configuration Manager istemci sertifikası ile ayarlanır.  

##  <a name="deploy-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> Dağıtım noktaları için istemci sertifikasını dağıtma  

> [!NOTE]  
>  Sertifika gereksinimleri aynı olduğundan bu sertifika, PXE önyüklemesi kullanmayan medya görüntüleri için de kullanılabilir.  

 Sertifika dağıtımı aşağıdaki yordamlara sahiptir:  

- Sertifika yetkilisinde özel Iş Istasyonu kimlik doğrulama sertifika şablonu oluşturma ve verme  

- Özel Iş Istasyonu kimlik doğrulama sertifikası isteme  

- Dağıtım noktaları için istemci sertifikasını dışarı aktarma  

###  <a name="create-and-issue-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> Sertifika yetkilisinde özel Iş Istasyonu kimlik doğrulama sertifika şablonu oluşturma ve verme  
 Bu yordam, özel anahtarın verilebilmesi ve sertifika şablonunu sertifika yetkilisine eklemesi için Configuration Manager dağıtım noktaları için özel bir sertifika şablonu oluşturur.  

> [!NOTE]
>  Bu yordam, istemci bilgisayarlar için oluşturduğunuz sertifika şablonundan farklı bir sertifika şablonu kullanır. Her iki sertifika da istemci kimlik doğrulaması özelliği gerektirse de, dağıtım noktaları için sertifika özel anahtarın verilmesini gerektirir. En iyi güvenlik uygulaması olarak, bu yapılandırma gerekmediği sürece özel anahtarın verilebilmesi için sertifika şablonları ayarlamayın. Sertifikayı sertifika deposundan seçmek yerine bir dosya olarak içeri aktarmanız gerektiğinden dağıtım noktası bu yapılandırmayı gerektirir.  
> 
>  Bu sertifika için yeni bir sertifika şablonu oluşturduğunuzda, özel anahtarı verilebilecek bir sertifika isteyebilecek bilgisayarları kısıtlayabilirsiniz. Örnek dağıtımda, bu, IIS çalıştıran Configuration Manager site sistem sunucuları için daha önce oluşturduğunuz güvenlik grubu olacaktır. IIS site sistemi rollerini dağıtan bir üretim ağında, sertifikayı yalnızca bu site sistemi sunucuları ile sınırlandırabilmek için dağıtım noktalarını çalıştıran sunucular için yeni bir güvenlik grubu oluşturmayı dikkate alın. Bu sertifikaya aşağıdaki değişiklikleri eklemeyi de düşünebilirsiniz:  
> 
> - Ek güvenlik için sertifikayı yüklemek üzere onay gerektir.  
>   - Sertifika geçerlilik süresini artırın. Sertifikayı, süresi dolmadan her seferinde dışarı ve içeri aktarmanız gerektiğinden, geçerlilik süresinin artırılması bu yordamı yinelemeniz gereken sıklığı azaltır. Ancak, bir saldırganın özel anahtarın şifresini çözmesini ve sertifikayı çalmasını daha fazla zaman sağladığından, geçerlilik süresinin bir artışı sertifikanın güvenliğini de düşürür.  
>   - Bu sertifikayı standart istemci sertifikaları arasından tanımaya yardımcı olması için sertifikanın Konu alanında veya Konu Diğer Adı'nda (SAN) özel bir değer kullanın. Aynı sertifikayı birden çok dağıtım noktası için kullanacaksanız bu özellikle yararlı olabilir.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Sertifika yetkilisinde özel İş İstasyonu Kimlik Doğrulama sertifika şablonu oluşturmak ve vermek için  

1.  Sertifika şablonları yönetim konsolunu yüklemek için Sertifika Yetkilisi konsolunu çalıştıran üye sunucusunda, **sertifika şablonları**' na sağ tıklayın ve **Yönet** ' i seçin.  

2.  Sonuçlar bölmesinde, **şablon görünen adı** sütununda **Iş istasyonu kimlik doğrulaması** olan girdiye sağ tıklayın ve ardından **Yinelenen şablon**' u seçin.  

3.  **Yinelenen şablon** Iletişim kutusunda **Windows 2003 Server, Enterprise Edition** ' ın seçili olduğundan emin olun ve ardından **Tamam**' ı seçin.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition ' ı**seçmeyin.  

4.  **Yeni Şablon Özellikleri** iletişim kutusunda, **genel** sekmesinde, dağıtım noktalarına yönelik istemci kimlik doğrulama sertifikasını oluşturmak Için **ConfigMgr istemci dağıtım noktası sertifikası**gibi bir şablon adı girin.  

5.  **Istek işleme** sekmesini seçin ve ardından **özel anahtarın verilmesine izin ver**' i seçin.  

6.  **Güvenlik** sekmesini seçin ve ardından **Enterprise Admins** güvenlik grubundan **kaydetme** iznini kaldırın.  

7.  **Ekle**' yi seçin, metin kutusuna **ConfigMgr IIS sunucuları** girin ve ardından **Tamam**' ı seçin.  

8.  Bu grup için **Kaydetme** iznini seçin ve **Okuma** izninin işaretini kaldırmayın.  

9. **Tamam**' ı ve ardından **Sertifika Şablonları konsolunu**Kapat ' ı seçin.  

10. Sertifika Yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın, **Yeni**' yi seçin ve ardından **verilecek sertifika şablonu**' nu seçin.  

11. **Sertifika şablonlarını etkinleştir** iletişim kutusunda, az önce oluşturduğunuz yeni **ConfigMgr Istemci dağıtım noktası Sertifikası**şablonunu seçtikten sonra **Tamam**' ı seçin.  

12. Daha fazla sertifika oluşturmanız ve bu sertifikaya ihtiyacınız yoksa **sertifika yetkilisi**' ni kapatın.  

###  <a name="request-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> Özel Iş Istasyonu kimlik doğrulama sertifikası isteme  
 Bu yordam, IIS çalıştıran ve bir dağıtım noktası olarak ayarlanacak üye sunucusuna özel istemci sertifikasını ister ve sonra kurar.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Özel İş İstasyonu Kimlik Doğrulama sertifikası istemek için  

1.  **Başlat**' ı seçin, **Çalıştır**' ı seçin ve ardından **mmc.exe girin.** Boş konsolda **Dosya**' yı seçin ve **ek bileşen Ekle/Kaldır**' ı seçin.  

2.  **Ek bileşenler Ekle/Kaldır** Iletişim kutusunda **kullanılabilir ek bileşenler**listesinden **Sertifikalar** ' ı seçin ve ardından **Ekle**' yi seçin.  

3.  **Sertifika ek bileşeni** Iletişim kutusunda **bilgisayar hesabı**' nı seçin ve ardından **İleri**' yi seçin.  

4.  **Bilgisayar Seç** iletişim kutusunda, **Yerel bilgisayar: (bu konsolun üzerinde çalıştığı bilgisayar)** ' ın seçili olduğundan emin olun ve ardından **son**' u seçin.  

5.  **Ek bileşenler Ekle veya Kaldır** Iletişim kutusunda **Tamam**' ı seçin.  

6.  Konsolunda, **Sertifikalar (yerel bilgisayar)**' ı genişletin ve **Kişisel**' i seçin.  

7.  **Sertifikalar**' a sağ tıklayın, **Tüm görevler**' i seçin ve ardından **Yeni sertifika iste**' yi seçin.  

8.  **Başlamadan önce** sayfasında **İleri**' yi seçin.  

9. **Sertifika kayıt Ilkesi Seç** sayfasını görürseniz **İleri**' yi seçin.  

10. **Sertifika iste** sayfasında, kullanılabilir sertifikalar listesinden **ConfigMgr Istemci dağıtım noktası sertifikası** ' nı seçin ve ardından **Kaydet**' i seçin.  

11. **Sertifikalar yükleme sonuçları** sayfasında, sertifika yüklenene kadar bekleyin ve ardından **son**' u seçin.  

12. Sonuçlar bölmesinde, bir sertifikanın **Hedeflenen amaç** sütununda **istemci kimlik doğrulamasına** sahip olduğunu ve **ConfigMgr Istemci dağıtım noktası sertifikası ' nın** **sertifika şablonu** sütununda olduğunu doğrulayın.  

13. **Sertifikalar (Yerel Bilgisayar)**'ı kapatmayın.  

###  <a name="export-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> Dağıtım noktaları için istemci sertifikasını dışarı aktarma  
 Bu yordam, dağıtım noktası özelliklerine alınabilmesi için özel Iş Istasyonu kimlik doğrulama sertifikasını bir dosyaya aktarır.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Dağıtım noktaları için istemci sertifikasını vermek için  

1. **Sertifikalar (yerel bilgisayar)** konsolunda, yeni yüklediğiniz sertifikaya sağ tıklayın, **Tüm görevler**' i seçin ve ardından **dışarı aktar**' ı seçin.  

2. Sertifika dışarı aktarma sihirbazında **İleri**' yi seçin.  

3. **Özel anahtarı dışarı aktar** sayfasında **Evet, özel anahtarı dışarı aktar**' ı seçin ve ardından **İleri**' yi seçin.  

   > [!NOTE]  
   >  Bu seçenek kullanılamıyorsa, sertifika özel anahtarı dışarı aktarma seçeneği olmadan oluşturulmuştur. Bu senaryoda, sertifikayı gereken biçimde dışarı aktaramazsınız. Özel anahtarın verilebilmesi için sertifika şablonunu ayarlamanız ve ardından sertifikayı yeniden istemeniz gerekir.  

4. **Dışarı aktarma dosyası biçimi** sayfasında **Kişisel BILGI değişimi-PKCS #12 (. PFX)** seçeneği seçilidir.  

5. **Parola** sayfasında, verdiğiniz sertifikayı özel anahtarıyla korumak için güçlü bir parola belirtin ve ardından **İleri**' yi seçin.  

6. **Dışarı aktarılacak dosya** sayfasında, dışarı aktarmak istediğiniz dosyanın adını belirtin ve ardından **İleri**' yi seçin.  

7. Sihirbazı kapatmak için, **sertifika dışarı aktarma Sihirbazı** sayfasında **son** ' u seçin ve onay iletişim kutusunda **Tamam** ' ı seçin.  

8. **Sertifikalar (Yerel Bilgisayar)**'ı kapatın.  

9. Dosyayı güvenli bir şekilde depolayın ve Configuration Manager konsolundan erişiminizin olduğundan emin olun.  

   Sertifika artık dağıtım noktasını ayarlarken içeri aktarılmaya hazırdır.  

> [!TIP]  
>  PXE önyüklemesi kullanmayan bir işletim sistemi dağıtımı için medya görüntülerini ayarlarken aynı sertifika dosyasını kullanabilirsiniz ve görüntüyü yükleme görev dizisi, HTTPS istemci bağlantıları gerektiren bir yönetim noktasıyla iletişim kurmanız gerekir.  

##  <a name="deploy-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> Mobil cihazlar için kayıt sertifikasını dağıtma  
 Bu sertifika dağıtımı, sertifika yetkilisinde kayıt sertifikası şablonu oluşturmak ve vermek için tek bir yordama sahiptir.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Sertifika yetkilisinde kayıt sertifikası şablonu oluşturma ve verme  
 Bu yordam Configuration Manager mobil cihazlar için bir kayıt sertifikası şablonu oluşturur ve sertifika yetkilisine ekler.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Sertifika yetkilisinde kayıt sertifikası şablonu oluşturmak ve vermek için  

1. Mobil cihazları Configuration Manager kaydeden kullanıcılara sahip bir güvenlik grubu oluşturun.  

2. Sertifika şablonları yönetim konsolunu yüklemek için Sertifika Hizmetleri 'nin yüklü olduğu üye sunucusunda, sertifika yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın ve **Yönet** ' i seçin.  

3. Sonuçlar bölmesinde, **şablon görünen adı** sütununda **kimliği doğrulanmış oturum** olan girdiye sağ tıklayın ve ardından **Yinelenen şablon**' u seçin.  

4. **Yinelenen şablon** Iletişim kutusunda **Windows 2003 Server, Enterprise Edition** ' ın seçili olduğundan emin olun ve ardından **Tamam**' ı seçin.  

   > [!IMPORTANT]  
   >  **Windows 2008 Server, Enterprise Edition ' ı**seçmeyin.  

5. **Yeni Şablon Özellikleri** iletişim kutusunda, **genel** sekmesinde, Configuration Manager tarafından yönetilecek mobil cihazlara yönelik kayıt sertifikalarını oluşturmak Için **ConfigMgr mobil cihaz kayıt sertifikası**gibi bir şablon adı girin.  

6. **Konu adı** sekmesini seçin, **Bu Active Directory bilgilerden oluştur** ' un seçili olduğundan emin olun, **Konu adı biçimi**için **ortak ad** ' ı seçin ve ardından **Bu bilgileri alternatif konu adına DAHIL et**' den **Kullanıcı asıl adı 'nı (UPN)** temizleyin.  

7. **Güvenlik** sekmesini seçin, kaydedilecek mobil cihazları olan kullanıcıların bulunduğu güvenlik grubunu seçin ve ardından **kaydetme**ek iznini seçin. **Okuma**'yı silmeyin.  

8. **Tamam**' ı ve ardından **Sertifika Şablonları konsolunu**Kapat ' ı seçin.  

9. Sertifika Yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın, **Yeni**' yi seçin ve ardından **verilecek sertifika şablonu**' nu seçin.  

10. **Sertifika şablonlarını etkinleştir** iletişim kutusunda, az önce oluşturduğunuz yeni **ConfigMgr mobil cihaz kayıt Sertifikası**şablonunu seçtikten sonra **Tamam**' ı seçin.  

11. Daha fazla sertifika oluşturmanız ve bu sertifikaların verilgerekmiyorsa Sertifika Yetkilisi konsolunu kapatın.  

    Mobil cihaz kayıt sertifikası şablonu artık istemci ayarlarında bir mobil cihaz kayıt profili ayarlarken seçilmeye hazırdır.  

##  <a name="deploy-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Mac bilgisayarlar için istemci sertifikasını dağıtma  

Bu sertifika dağıtımı, sertifika yetkilisinde kayıt sertifikası şablonu oluşturmak ve vermek için tek bir yordama sahiptir.  

###  <a name="create-and-issue-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> Sertifika yetkilisinde bir Mac istemci sertifikası şablonu oluşturma ve verme  
 Bu yordam Configuration Manager Mac bilgisayarları için özel bir sertifika şablonu oluşturur ve sertifika şablonunu sertifika yetkilisine ekler.  

> [!NOTE]  
>  Bu yordam, Windows istemci bilgisayarları veya dağıtım noktaları için oluşturmuş olabileceğiniz sertifika şablonundan farklı bir sertifika şablonu kullanır.  
>   
>  Bu sertifika için yeni bir sertifika şablonu oluşturduğunuzda, sertifika isteğini yetkili kullanıcılara kısıtlayabilirsiniz.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Sertifika yetkilisinde Mac istemcisi sertifika şablonu oluşturmak ve vermek için  

1. Configuration Manager kullanarak Mac bilgisayara sertifikayı kaydedecek yönetici kullanıcılar için Kullanıcı hesapları içeren bir güvenlik grubu oluşturun.  

2. Sertifika şablonları yönetim konsolunu yüklemek için Sertifika Yetkilisi konsolunu çalıştıran üye sunucusunda, **sertifika şablonları**' na sağ tıklayın ve **Yönet** ' i seçin.  

3. Sonuçlar bölmesinde, **şablon görünen adı** sütununda **kimliği doğrulanmış oturum** ' yi görüntüleyen girişe sağ tıklayın ve **Yinelenen şablon**' u seçin.  

4. **Yinelenen şablon** Iletişim kutusunda **Windows 2003 Server, Enterprise Edition** ' ın seçili olduğundan emin olun ve ardından **Tamam**' ı seçin.  

   > [!IMPORTANT]  
   >  **Windows 2008 Server, Enterprise Edition ' ı**seçmeyin.  

5. **Yeni Şablon Özellikleri** iletişim kutusunda, **genel** sekmesinde, Mac Istemci sertifikasını oluşturmak Için **ConfigMgr Mac istemci sertifikası**gibi bir şablon adı girin.  

6. **Konu adı** sekmesini seçin, **Bu Active Directory bilgilerden oluştur** ' un seçili olduğundan emin olun, **Konu adı biçimi**için **ortak ad** ' ı seçin ve ardından **Bu bilgileri alternatif konu adına DAHIL et**' den **Kullanıcı asıl adı 'nı (UPN)** temizleyin.  

7. **Güvenlik** sekmesini seçin ve ardından **etki alanı yöneticileri** ve **Enterprise Admins** güvenlik gruplarından **kaydetme** iznini kaldırın.  

8. **Ekle**' yi seçin, birinci adımda oluşturduğunuz güvenlik grubunu belirtin ve ardından **Tamam**' ı seçin.  

9. Bu grup için **kaydetme** iznini seçin ve **okuma** izninin işaretini kaldırmayın.  

10. **Tamam**' ı ve ardından **Sertifika Şablonları konsolunu**Kapat ' ı seçin.  

11. Sertifika Yetkilisi konsolunda, **sertifika şablonları**' na sağ tıklayın, **Yeni**' yi seçin ve ardından **verilecek sertifika şablonu**' nu seçin.  

12. **Sertifika şablonlarını etkinleştir** iletişim kutusunda, az önce oluşturduğunuz yeni **ConfigMgr Mac istemci sertifikası**şablonunu seçtikten sonra **Tamam**' ı seçin.  

13. Daha fazla sertifika oluşturmanız ve bu sertifikaya ihtiyacınız yoksa **sertifika yetkilisi**' ni kapatın.  

    Kayıt için istemci ayarlarını ayarlarken Mac istemci sertifikası şablonu artık seçilmeye hazırdır.