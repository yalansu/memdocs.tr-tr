---
title: Bulma yöntemleri
titleSuffix: Configuration Manager
description: Ağınızdaki, Active Directory veya Azure Active Directory cihazları bulmak için kullanılabilen bulma yöntemleri hakkında bilgi edinin.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: af35d5a941d5fd9bde2f87c8fb700b9d85e10b00
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078660"
---
# <a name="about-discovery-methods-for-configuration-manager"></a>Configuration Manager için bulma yöntemleri hakkında

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager bulma yöntemleri, ağınızdaki farklı cihazları, Active Directory veya Azure Active Directory (Azure AD) kullanıcıları aracılığıyla bulabilirsiniz. Bir bulma yöntemini etkin bir şekilde kullanmak için, kullanılabilir yapılandırma ve sınırlamalarını anlamanız gerekir.  



##  <a name="active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a>Active Directory orman keşfi  
 **Yapılandırılabilir:** Yes  

 **Varsayılan olarak etkindir:** Eşleşen  

 Bu yöntemi çalıştırmak için kullanabileceğiniz **hesaplar** :  

-   **Active Directory orman bulma hesabı** (Kullanıcı tanımlı)  

-   Site sunucusunun **bilgisayar hesabı**  

Diğer Active Directory bulma yöntemlerinin aksine, Active Directory orman keşfi yönetebileceğiniz kaynakları bulamaz. Bunun yerine, bu yöntem Active Directory yapılandırılan ağ konumlarını bulur. Bu konumları, hiyerarşiniz genelinde kullanılmak üzere sınırlara dönüştürebilir.  

Bu yöntem çalıştığında, yerel Active Directory ormanı, güvenilen her ormanı ve Configuration Manager konsolunun **Active Directory ormanları** düğümünde yapılandırdığınız her bir ek ormanı arar.  

Active Directory orman bulmayı şu şekilde kullan:  

-   Active Directory Siteleri ve alt ağları bulup bu ağ konumlarına göre Configuration Manager sınırları oluşturun.  

-   Bir Active Directory sitesine atanan üst ağları belirler. Her bir üst ağı bir IP adresi aralığı sınırına dönüştürür.  

-   Bu ormana yayımlama etkinleştirildiğinde bir ormanda Active Directory Domain Services (AD DS) yayımlayın. Belirtilen Active Directory orman hesabının o ormana yönelik izinleri olmalıdır.  

Configuration Manager konsolunda Active Directory orman bulmayı yönetebilirsiniz. **Yönetim** çalışma alanına gidin ve **Hiyerarşi Yapılandırması**' nı genişletin.   

-   **Bulma yöntemleri**: Active Directory orman bulmayı, hiyerarşinizin en üst düzey sitesinde çalışacak şekilde etkinleştirin. Bulmayı çalıştırmak için basit bir zamanlama da belirtebilirsiniz. IP alt ağlarından ve bulduğu siteleri Active Directory otomatik olarak sınırlar oluşturacak şekilde yapılandırın. Active Directory orman keşfi bir alt birincil sitede veya ikincil sitede çalıştırılamaz.  

-   **Active Directory ormanları**: keşfedilecek ek ormanları yapılandırın, her bir Active Directory ormanı hesabını belirtin ve her bir ormanda yayımlamayı yapılandırın. Bulma işlemini izleyin. IP alt ağları ve Active Directory siteleri Configuration Manager sınırları ve sınır gruplarının üyeleri olarak ekleyin.  

Hiyerarşinizdeki her site için Active Directory ormanları yayımlamayı yapılandırmak için Configuration Manager konsolunuzu hiyerarşinizin en üst düzey sitesine bağlayın. Bir Active Directory sitesinin **Özellikler** Iletişim kutusundaki **Yayımlama** sekmesi yalnızca geçerli siteyi ve onun alt sitelerini gösterebilir. Bir orman için yayımlama etkinleştirildiğinde ve ormanın şeması Configuration Manager için genişletilmişse, bu Active Directory ormanında yayımlamak üzere etkinleştirilen her bir site için aşağıdaki bilgiler yayımlanır:  

-    **SMS-site-&lt;site kodu>**

-   **SMS-MP-&lt;site kodu>-&lt;site sistemi sunucu adı>**  

-   **SMS-SLP-&lt;site kodu>-&lt;site sistemi sunucu adı>**  

-   **SMS-&lt;site kodu>-&lt;Active Directory site adı veya alt ağ>**  

> [!NOTE]  
>  İkincil siteler, Active Directory'e yayımlamak için daima ikincil site sunucusu bilgisayar hesabını kullanır. İkincil sitelerin Active Directory yayımlamasını istiyorsanız, ikincil site sunucusu bilgisayar hesabının Active Directory yayımlamak için izinlere sahip olduğundan emin olun. İkincil site güvenilmeyen bir ormana veri yayımlayamaz.  

> [!CAUTION]  
>  Bir siteyi Active Directory ormanında yayımlama seçeneğini kaldırdığınızda, kullanılabilir site sistemi rolleri dahil olmak üzere bu site için daha önce yayımlanmış tüm bilgiler Active Directory kaldırılır.  

Active Directory orman bulma işlemleri aşağıdaki günlüklere kaydedilir:  

-   Yayımlama ile ilgili eylemler dışındaki tüm eylemler, site sunucusundaki ** &lt;InstallationPath> \logs** klasöründeki **ADForestDisc. log** dosyasına kaydedilir.  

-   Active Directory orman keşfi yayımlama eylemleri, site sunucusundaki ** &lt;> ınstalman** **. log** ve **Sitecomp. log** dosyalarına kaydedilir.  

Bu keşif yöntemini yapılandırma hakkında daha fazla bilgi için bkz. [keşif yöntemlerini yapılandırma](configure-discovery-methods.md#BKMK_ConfigADForestDisc).  



##  <a name="active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a>Active Directory grubu bulma  
**Yapılandırılabilir:** Yes  

**Varsayılan olarak etkindir:** Eşleşen  

Bu yöntemi çalıştırmak için kullanabileceğiniz **hesaplar** :  

-   **Active Directory grubu bulma hesabı** (Kullanıcı tanımlı)  

-   Site sunucusunun **bilgisayar hesabı**  

> [!TIP]  
>  Bu bölümdeki bilgilere ek olarak, [Active Directory grubu, sistem ve Kullanıcı bulmanın ortak özellikleri](#bkmk_shared)bölümüne bakın.  

Şunları belirlemek için Active Directory Domain Services aramak için bu yöntemi kullanın:  

-   Yerel, genel ve Evrensel güvenlik grupları.  

-   Grupların üyeliği.  

-   Başka bir bulma yöntemi bu bilgisayarları ve kullanıcıları daha önce bulmadığından bile bir grubun üye bilgisayarları ve kullanıcılarıyla ilgili sınırlı bilgiler.  

Bu bulma yöntemi grupları ve grupların üyelerinin grup ilişkilerini tanımlamak için tasarlanmıştır. Varsayılan olarak yalnızca güvenlik grupları bulunur. Dağıtım gruplarının üyeliğini de bulmak istiyorsanız, **Active Directory grubu bulma özellikleri** Iletişim kutusundaki **seçenek** sekmesinde **dağıtım gruplarının üyeliğini bulma** seçeneğinin kutusunu denetlemeniz gerekir.  

Active Directory Grup keşfi Active Directory sistem keşfi veya Active Directory Kullanıcı keşfi kullanılarak belirlenebilmiş genişletilmiş Active Directory özniteliklerini desteklemez. Bu bulma yöntemi bilgisayar ve kullanıcı kaynaklarını bulmak için iyileştirilmediğinden, Active Directory sistem bulma ve Kullanıcı keşfi Active Directory çalıştırdıktan sonra bu bulma yöntemini çalıştırmayı göz önünde bulundurun. Bu öneri, bu yöntemin gruplar için tam bulgu verileri kaydı (DDR) oluşturması, ancak grupların üyesi olan bilgisayarlar ve kullanıcılar için yalnızca sınırlı DDR 'nin oluşturulmasıdır.  

Bu yöntemin bilgileri nasıl arayacağını denetleyen aşağıdaki bulma kapsamlarını yapılandırabilirsiniz:  

-   **Konum**: bir veya daha fazla Active Directory kapsayıcısı aramak istiyorsanız bir konum kullanın. Bu kapsam seçeneği, belirtilen Active Directory kapsayıcılarının özyinelemeli aramasını destekler. Bu işlem, belirttiğiniz kapsayıcının altındaki her bir alt kapsayıcıyı arar. Daha fazla alt kapsayıcı bulunana kadar devam eder.  

-   **Gruplar**: bir veya daha fazla belirli Active Directory grubunda arama yapmak istiyorsanız grupları kullanın. **Active Directory etki alanı** varsayılan etki alanı ve ormanı kullanacak şekilde yapılandırabilir veya aramayı tek bir etki alanı denetleyicisiyle sınırlayabilirsiniz. Ayrıca, aranacak bir veya daha fazla grup belirtebilirsiniz. En az bir grup belirtmezseniz, belirtilen **Active Directory etki alanı** konumunda bulunan tüm gruplar aranır.  

> [!CAUTION]  
>  Bir bulma kapsamı yapılandırdığınızda, yalnızca bulmanız gereken grupları seçin. Bu öneri, Active Directory grubu bulmanın keşif kapsamındaki her bir grubun her bir üyesini bulmaya çalışacağı. Büyük grupları bulmanın bant genişliği ve Active Directory kaynaklarının kapsamlı bir şekilde kullanılması gerekebilir.  

> [!NOTE]  
>  Genişletilmiş Active Directory özniteliklerine dayalı koleksiyonlar oluşturabilmeniz ve bilgisayarlar ve kullanıcılar için doğru keşif sonuçları sağlamak için, Active Directory sistem bulma veya Active Directory Kullanıcı bulma işlemlerini, bulmak istediğinize bağlı olarak çalıştırın.  

Active Directory Grup bulma eylemleri, site sunucusundaki ** &lt;InstallationPath\>\logs** klasöründeki **adsgdıs. log** dosyasına kaydedilir.  

Bu keşif yöntemini yapılandırma hakkında daha fazla bilgi için bkz. [keşif yöntemlerini yapılandırma](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a>Active Directory sistem bulma  
**Yapılandırılabilir:** Yes  

**Varsayılan olarak etkindir:** Eşleşen  

Bu yöntemi çalıştırmak için kullanabileceğiniz **hesaplar** :  

-   **Active Directory sistem bulma hesabı** (Kullanıcı tanımlı)  

-   Site sunucusunun **bilgisayar hesabı**  

> [!TIP]  
>  Bu bölümdeki bilgilere ek olarak, [Active Directory grubu, sistem ve Kullanıcı bulmanın ortak özellikleri](#bkmk_shared)bölümüne bakın.  

Koleksiyonlar ve sorgular oluşturmak için kullanılabilecek bilgisayar kaynakları için belirtilen Active Directory Domain Services konumlarında arama yapmak üzere bu bulma yöntemini kullanın. İstemci anında yükleme kullanarak, bulunan bir cihaza Configuration Manager istemcisini de yükleyebilirsiniz.  

Varsayılan olarak, bu yöntem, aşağıdaki öznitelikler de dahil olmak üzere bilgisayar hakkındaki temel bilgileri bulur:  

-   Bilgisayar adı  

-   İşletim sistemi ve sürümü  

-   Active Directory kapsayıcı adı  

-   IP adresi  

-   Active Directory sitesi  

-   Son oturum açma zaman damgası  

Bir bilgisayar için DDR 'yi başarılı bir şekilde oluşturmak için Active Directory sistem keşfi bilgisayar hesabını tanımlayabilmelidir ve bilgisayar adını bir IP adresine başarıyla çözümleyebilir.  

**Active Directory sistem bulma özellikleri** iletişim kutusunda, **Active Directory öznitelikleri** sekmesinde, bulduğu varsayılan nesne özniteliklerinin tam listesini görebilirsiniz. Ayrıca, ek (genişletilmiş) öznitelikleri keşfetmek için yöntemini de yapılandırabilirsiniz.  

Active Directory sistem bulma eylemleri, site sunucusundaki ** &lt;InstallationPath\>\logs** klasöründeki **adsysdsıs. log** dosyasına kaydedilir.  

Bu keşif yöntemini yapılandırma hakkında daha fazla bilgi için bkz. [keşif yöntemlerini yapılandırma](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a>Kullanıcı keşfi Active Directory  
**Yapılandırılabilir:** Yes  

**Varsayılan olarak etkindir:** Eşleşen  

Bu yöntemi çalıştırmak için kullanabileceğiniz **hesaplar** :  

-   **Kullanıcı keşfi hesabını Active Directory** (Kullanıcı tanımlı)  

-   Site sunucusunun **bilgisayar hesabı**  

> [!TIP]  
>  Bu bölümdeki bilgilere ek olarak, [Active Directory grubu, sistem ve Kullanıcı bulmanın ortak özellikleri](#bkmk_shared)bölümüne bakın.  

Kullanıcı hesaplarını ve ilişkili öznitelikleri tanımlamak üzere Active Directory Domain Services aramak için bu bulma yöntemini kullanın. Varsayılan olarak, bu yöntem, aşağıdaki öznitelikler de dahil olmak üzere Kullanıcı hesabı hakkındaki temel bilgileri bulur:  

-   Kullanıcı adı  

-   Benzersiz Kullanıcı adı (etki alanı adını içerir)  

-   Domain  

-   Active Directory kapsayıcı adları  

**Active Directory Kullanıcı keşfi özellikleri** iletişim kutusunda, **Active Directory öznitelikleri** sekmesinde, bulduğu nesne özniteliklerinin tam varsayılan listesini görüntüleyebilirsiniz. Ayrıca, ek (genişletilmiş) öznitelikleri keşfetmek için yöntemini de yapılandırabilirsiniz.

Active Directory Kullanıcı keşfi eylemleri, site sunucusundaki ** &lt;InstallationPath\>\logs** klasöründeki **adusrdsıs. log** dosyasına kaydedilir.  

Bu keşif yöntemini yapılandırma hakkında daha fazla bilgi için bkz. [keşif yöntemlerini yapılandırma](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



## <a name="azure-active-directory-user-discovery"></a><a name="azureaddisc"></a>Kullanıcı keşfi Azure Active Directory

Modern bir bulut kimliği olan kullanıcılar için Azure AD aboneliğinizi aramak üzere Azure Active Directory (Azure AD) Kullanıcı keşfi kullanın. Azure AD Kullanıcı keşfi aşağıdaki öznitelikleri bulabilir:

- Uzantının
- displayName
- posta
- mailNickname
- onPremisesSecurityIdentifier
- userPrincipalName
- AAD Tenantıd
- onPremisesDomainName
- onPremisesSamAccountName
- onPremisesDistinguishedName

Bu yöntem, Azure AD 'den kullanıcı özniteliklerinin tam ve değişim eşitlemesini destekler. Bu bilgiler daha sonra diğer keşif yöntemlerinden topladığınız bir arada bulunan bulma verileri için kullanılabilir.

Azure AD Kullanıcı keşfi için Eylemler, hiyerarşinin üst katman site sunucusundaki **SMS_AZUREAD_DISCOVERY_AGENT. log** dosyasına kaydedilir.

Azure AD Kullanıcı bulmayı yapılandırmak için bkz. [Azure hizmetlerini](azure-services-wizard.md) bulut yönetimi için yapılandırma. Bu keşif yöntemini yapılandırma hakkında daha fazla bilgi için bkz. [Azure AD Kullanıcı bulmayı yapılandırma](configure-discovery-methods.md#azureaadisc).

## <a name="azure-active-directory-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Kullanıcı grubu bulmayı Azure Active Directory
<!--3611956-->
*(Sürüm 1906 ' de [yayın öncesi özelliği](../../manage/pre-release-features.md) olarak sunulmuştur)*

Azure Active Directory 'de (Azure AD) bu grupların Kullanıcı gruplarını ve üyelerini bulabilirsiniz. Azure AD Kullanıcı grubu bulma aşağıdaki öznitelikleri bulabilir:

- Uzantının
- displayName
- mailNickname
- onPremisesSecurityIdentifier
- AAD Tenantıd

Azure AD Kullanıcı grubu bulma işlemleri, hiyerarşinin üst katman site sunucusundaki **SMS_AZUREAD_DISCOVERY_AGENT. log** dosyasına kaydedilir. Bu keşif yöntemini yapılandırma hakkında daha fazla bilgi için bkz. [Azure AD Kullanıcı grubu bulmayı yapılandırma](configure-discovery-methods.md#bkmk_azuregroupdisco).

##  <a name="heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a>Sinyal keşfi  
**Yapılandırılabilir:** Yes  

**Varsayılan olarak etkindir:** Yes  

Bu yöntemi çalıştırmak için kullanabileceğiniz **hesaplar** :  

-   Site sunucusunun **bilgisayar hesabı**  

Sinyal keşfi diğer Configuration Manager bulma yöntemlerinden farklıdır. Varsayılan olarak etkindir ve DDR oluşturmak için her bilgisayar istemcisinde (site sunucusu yerine) çalışır. Mobil aygıt istemcileri için bu DDR, mobil aygıt istemcisinin kullandığı yönetim noktası tarafından oluşturulur. Configuration Manager istemcilerinin veritabanı kaydını sürdürmenize yardımcı olmak için sinyal bulmayı devre dışı bırakın. Bu yöntem, veritabanı kaydının korunmasının yanı sıra bir bilgisayarın yeni kaynak kaydı olarak bulunmasını zorlayabilir. Ayrıca, veritabanından silinen bir bilgisayarın veritabanı kaydını yeniden oluşturabilir.  

Sinyal Saptama, hiyerarşideki tüm istemciler için yapılandırılmış bir zamanlamaya göre çalışır. Sinyal bulma için varsayılan zamanlama yedi güne ayarlanır. Sinyal bulma aralığını değiştirirseniz, **eski bulma verilerini sil**site bakım görevinden daha sık çalıştığından emin olun. Bu görev etkin olmayan istemci kayıtlarını site veritabanından siler. **Eski bulma verilerini sil** görevini yalnızca birincil siteler için yapılandırabilirsiniz. 

Ayrıca, belirli bir istemcide sinyal bulmayı el ile çağırabilirsiniz. Bir istemcinin Configuration Manager Denetim Masası ' nın **eylem** sekmesinde **bulma verileri toplama döngüsünü** çalıştırın.  

Sinyal keşfi çalıştırıldığında, istemcinin geçerli bilgilerine sahip bir DDR oluşturur. İstemci daha sonra bu küçük dosyayı (yaklaşık 1 KB boyutunda) bir yönetim noktasına kopyalar, böylece birincil bir site onu işleyebilir. Dosyada aşağıdaki bilgiler bulunur:  

-   Ağ konumu  

-   NetBIOS adı  

-   İstemci aracısının sürümü  

-   İşletimsel durum ayrıntıları  

Sinyal keşfi, istemci yükleme durumu hakkında ayrıntılı bilgi sağlayan tek bulgu yöntemidir. Bunu, sistem kaynak istemci özniteliğini güncelleştirmek için **Evet**değerine eşit bir değer ayarlamak için yapar.  

> [!NOTE]  
>  Sinyal keşfi devre dışı bırakılsa bile DDR 'ler, etkin mobil cihaz istemcileri için oluşturulur ve gönderilir. Bu davranış, **eski bulma verilerini silme** görevinin etkin mobil cihazları etkilememesini sağlar. **Eski bulma verilerini sil** görevi bir mobil cihazın veritabanı kaydını sildiğinde, cihaz sertifikasını da iptal eder. Bu eylem, mobil cihazın yönetim noktalarına bağlanmasını engeller.  

Sinyal bulma işlemleri aşağıdaki konumlarda günlüğe kaydedilir:  

-   Bilgisayar istemcileri için sinyal bulma eylemleri, *%Windir%\CCM\Logs* klasöründeki **InventoryAgent. log** dosyasında istemciye kaydedilir.  

-   Mobil cihaz istemcilerinde, sinyal bulma eylemleri, mobil aygıt istemcisinin kullandığı yönetim noktasının *% Program Files%\CCM\Logs* klasöründeki **DMPRP. log** dosyasına kaydedilir.  

Bu keşif yöntemini yapılandırma hakkında daha fazla bilgi için bkz. [keşif yöntemlerini yapılandırma](configure-discovery-methods.md#BKMK_ConfigHBDisc).  



##  <a name="network-discovery"></a><a name="bkmk_aboutNetwork"></a>Ağ bulma  
**Yapılandırılabilir:** Yes  

**Varsayılan olarak etkindir:** Eşleşen  

Bu yöntemi çalıştırmak için kullanabileceğiniz **hesaplar** :  

-   Site sunucusunun **bilgisayar hesabı**  

Ağınızın topolojisini bulma ve ağınızda bir IP adresi olan cihazları bulma için bu yöntemi kullanın. Ağ bulma, aşağıdaki varlıkları sorgulayarak ağınızı IP özellikli kaynaklar için arar: 
- DHCP 'nin Microsoft uygulamasını çalıştıran sunucular
- Ağ yönlendiricilerinde Adres Çözümleme Protokolü (ARP) önbellekleri
- SNMP etkin cihazlar
- Active Directory etki alanları  

Ağ bulmayı kullanabilmeniz için, çalıştırılacak bulma *düzeyini* belirtmeniz gerekir. Ağ kesimlerini veya cihazları sorgulamak için ağ bulmayı etkinleştiren bir veya daha fazla bulma mekanizması da yapılandırırsınız. Ayrıca, ağ üzerinde bulma eylemlerini denetlemeye yardımcı olan ayarları yapılandırabilirsiniz. Son olarak, ağ bulma işlemi çalıştırıldığında bir veya daha fazla zamanlama tanımlarsınız.  

Bu yöntemin bir kaynağı başarılı bir şekilde bulması için ağ bulma 'nın, kaynağın IP adresini ve alt ağ maskesini tanımlaması gerekir. Aşağıdaki yöntemler bir nesnenin alt ağ maskesini tanımlamak için kullanılır:  

-   **YÖNLENDIRICI ARP önbelleği:** Ağ bulma, alt ağ bilgilerini bulmak için bir yönlendiricinin ARP önbelleğini sorgular. Genellikle, bir yönlendirici ARP önbelleğindeki verilerin yaşam süresi daha kısadır. Bu nedenle, ağ bulma ARP önbelleğini sorguladığında ARP önbelleğinde artık istenen nesneyle ilgili bilgiler bulunmayabilir.  

-   **DHCP:** Ağ bulma, DHCP sunucusunun kira verdiği cihazları bulmak için belirttiğiniz her DHCP sunucusunu sorgular. Ağ bulma, yalnızca DHCP 'nin Microsoft uygulamasını çalıştıran DHCP sunucularını destekler.  

-   **SNMP cihazı:** Ağ bulma, bir SNMP cihazını doğrudan sorgulayabilir. Ağ bulma 'nın bir cihazı sorgulaması için cihazda yerel bir SNMP aracısının yüklü olması gerekir. Ayrıca, ağ bulmayı SNMP aracısının kullandığı topluluk adını kullanacak şekilde yapılandırın.  

Bulma, IP adreslenebilir bir nesneyi belirlediğinde ve nesnenin alt ağ maskesini belirleyebilmesine göre, bu nesne için bir DDR oluşturur. Farklı cihaz türleri ağa bağlandığından, ağ bulma Configuration Manager istemcisini desteklemeyen kaynakları bulur. Örneğin, keşfedilmiş ancak yönetilebilecek cihazlar, yazıcılar ve yönlendiriciler içerir.  

Ağ bulma, oluşturduğu bulma kaydının bir parçası olarak birkaç öznitelik döndürebilir. Bu öznitelikler arasında şunlar yer alır:  

-   NetBIOS adı  

-   IP adresleri  

-   Kaynak etki alanı  

-   Sistem rolleri  

-   SNMP topluluk adı  

-   MAC adresleri  

Ağ bulma etkinliği, bulmayı çalıştıran site sunucusundaki * &lt;InstallationPath\>\logs* içindeki **Netdisc. log** dosyasına kaydedilir.  

 Bu keşif yöntemini yapılandırma hakkında daha fazla bilgi için bkz. [keşif yöntemlerini yapılandırma](configure-discovery-methods.md#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Karmaşık ağlar ve düşük bant genişliğine sahip bağlantılar, ağ bulmanın yavaş çalışmasına ve önemli ölçüde ağ trafiği oluşturulmasına neden olabilir. En iyi uygulama olarak, ağ bulmayı yalnızca diğer bulma yöntemleri keşfettiğiniz kaynakları bulamadığında çalıştırın. Örneğin, çalışma grubu bilgisayarlarını bulmanız gerekiyorsa ağ bulmayı kullanın. Diğer bulma yöntemleri çalışma grubu bilgisayarlarını bulamaz.  

###  <a name="levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a>Ağ bulma düzeyleri  
Ağ bulmayı yapılandırırken, üç bulma düzeyinden birini belirtirsiniz:  

|Bulma düzeyi|Ayrıntılar|  
|------------------------|-------------|  
|Topoloji|Bu düzey, yönlendiricileri ve alt ağları bulur ancak nesneler için bir alt ağ maskesi tanımlamaz.|  
|Topoloji ve istemci|Topolojiye ek olarak, bu düzey bilgisayarlar gibi olası istemcileri ve Yazıcılar ve yönlendiriciler gibi kaynakları bulur. Bu bulma düzeyi, bulduğu nesnelerin alt ağ maskesini belirlemeyi dener.|  
|Topoloji, istemci ve istemci işletim sistemi|Topoloji ve potansiyel istemcilerin yanı sıra, bu düzey bilgisayar işletim sistemi adını ve sürümünü bulmaya çalışır. Bu düzey Windows tarayıcısı ve Windows ağ çağrılarını kullanır.|  

 Her artımlı düzeyiyle, ağ bulma etkinliği ve ağ bant genişliği kullanımını artırır. Ağ bulmanın tüm yönlerini etkinleştirmeden önce, oluşturulabilecek ağ trafiğini göz önünde bulundurun.  

 Örneğin, ağ bulmayı ilk kez kullandığınızda, ağ altyapınızı tanımlamak için yalnızca topoloji düzeyiyle başlayabilirsiniz. Ardından, nesneleri ve bunların cihaz işletim sistemlerini bulmak için ağ bulmayı yeniden yapılandırın. Ağ bulmayı sınırlayan ayarları belirli bir ağ kesimleri aralığıyla de yapılandırabilirsiniz. Böylece, gerek duyduğunuz ağ konumlarında ve gereksiz ağ trafiğinden kaçınabilirsiniz. Bu işlem, Edge yönlendiricilerinde veya ağınızın dışından nesneleri keşfetmenizi de sağlar.  

###  <a name="network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a>Ağ bulma seçenekleri  
Ağ bulmayı, IP adreslenebilir cihazları arayacak şekilde etkinleştirmek için, bu seçeneklerden birini veya daha fazlasını yapılandırın.  

> [!NOTE]  
>  Ağ bulma, bulmayı çalıştıran site sunucusunun bilgisayar hesabı bağlamında çalışır. Bilgisayar hesabının güvenilmeyen bir etki alanı için izinleri yoksa, etki alanı ve DHCP sunucusu yapılandırmalarının kaynakları bulamamasına neden olabilir.  

#### <a name="dhcp"></a>DHCP  

Ağ bulmanın sorgulamak istediğiniz her DHCP sunucusunu belirtin. (Ağ bulma yalnızca Microsoft 'un DHCP uygulamasını çalıştıran DHCP sunucularını destekler.)  

-   Ağ bulma, DHCP sunucusundaki veritabanına yönelik uzak yordam çağrılarını kullanarak bilgileri alır.  

-   Ağ bulma, her bir sunucuya kayıtlı cihazların listesi için hem 32-bit hem de 64 bit DHCP sunucusunu sorgulayabilir.  

-   Ağ bulma 'nın bir DHCP sunucusunu başarıyla sorgulaması için, bulmayı çalıştıran sunucunun bilgisayar hesabı, DHCP sunucusundaki DHCP kullanıcıları grubunun bir üyesi olmalıdır. Örneğin, aşağıdaki deyimlerden biri true olduğunda bu erişim düzeyi vardır:  

    -   Belirtilen DHCP sunucusu, bulmayı çalıştıran sunucunun DHCP sunucusudur.  

    -   Bulmayı ve DHCP sunucusunu çalıştıran bilgisayar aynı etki alanında yer alan bir bilgisayardır.  

    -   Bulmayı ve DHCP sunucusunu çalıştıran bilgisayar arasında çift yönlü bir güven bulunur.  

    -   Site sunucusu, DHCP kullanıcıları grubunun bir üyesidir.  

-   Ağ bulma bir DHCP sunucusunu Numaralandırdığınızda, her zaman statik IP adreslerini bulamaz. Ağ bulma, DHCP sunucusundaki dışlanan bir IP adresi aralığının parçası olan IP adreslerini bulamaz. Ayrıca, el ile atama için ayrılan IP adreslerini bulamaz.  

#### <a name="domains"></a>Etki Alanları  

Ağ bulmanın sorgulamasını istediğiniz her etki alanını belirtin.  

-   Bulmayı çalıştıran site sunucusunun bilgisayar hesabının, belirtilen her etki alanındaki etki alanı denetleyicilerini okuma izinleri olmalıdır.  

-   Yerel etki alanındaki bilgisayarları öğrenmek için bilgisayar tarayıcısı hizmetini en az bir bilgisayarda etkinleştirmeniz gerekir. Bu bilgisayar, ağ bulmayı çalıştıran site sunucusuyla aynı alt ağda olmalıdır.  

-   Ağ bulma, ağa gözatarken site sunucunuzdaki görüntüleyebildiği herhangi bir bilgisayarı bulabilir.  

-   Ağ bulma IP adresini alır. Ardından, bulduğu her cihaza ping göndermek için bir Internet Denetim Iletisi Protokolü (ıCMP) yankı isteği kullanır. **Ping** komutu, şu anda hangi bilgisayarların etkin olduğunu belirlemenize yardımcı olur.  

#### <a name="snmp-devices"></a>SNMP cihazları  

Ağ bulmanın sorgulamak istediğiniz her SNMP cihazını belirtin.  

-   Ağ bulma, bu sorguya yanıt veren SNMP cihazlarından ıpnettomediatable değerini alır. Bu değer, istemci bilgisayarlar veya yazıcılar, yönlendiriciler veya IP adreslenebilir diğer cihazlar gibi diğer kaynaklar olan IP adresi dizilerini döndürür.  

-   Bir cihazı sorgulamak için, cihazın IP adresini veya NetBIOS adını belirtmeniz gerekir.  

-   Ağ bulmayı cihazın topluluk adını kullanacak şekilde yapılandırın veya cihaz SNMP tabanlı sorguyu reddeder.  


###  <a name="limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a>Ağ bulmayı sınırlandırma  
Ağ bulma, ağınızın kenarına bir SNMP cihazını sorguladığında, bu, anlık ağınızın dışındaki alt ağlar ve SNMP cihazları hakkında bilgi tanımlayabilir. Bulmanın iletişim kurabildiği SNMP cihazlarını yapılandırarak ve Sorgulanacak ağ kesimlerini belirterek ağ bulmayı sınırlandırmak için aşağıdaki bilgileri kullanın.  

#### <a name="subnets"></a>Alt ağlar  

Ağ bulma tarafından SNMP ve DHCP seçeneklerini kullandığında, sorgulayan alt ağları yapılandırın. Bu iki seçenek yalnızca etkin alt ağları arar.  

Örneğin, bir DHCP isteği tüm ağınızdaki konumlardan cihaz döndürebilir. Yalnızca belirli bir alt ağdaki cihazları bulmak istiyorsanız, **ağ bulma özellikleri** Iletişim kutusundaki **alt ağlar** sekmesinde söz konusu alt ağı belirtin ve etkinleştirin. Alt ağları belirttiğinizde ve etkinleştirdiğinizde, gelecekteki DHCP ve SNMP bulma görevlerini bu alt ağlarla sınırlayabilirsiniz.  

> [!NOTE]  
>  Alt ağ yapılandırmalarında, **etki alanları** bulma seçeneğinin bulduğu nesneler sınırlandırmaz.  

#### <a name="snmp-community-names"></a>SNMP topluluk adları  

Ağ bulmayı, bir SNMP cihazını başarıyla sorgulamak üzere etkinleştirmek için, ağ bulmayı cihazın topluluk adıyla yapılandırın. Ağ bulma, SNMP cihazının topluluk adı kullanılarak yapılandırılmamışsa, cihaz sorguyu reddeder.  

#### <a name="maximum-hops"></a>En fazla atlama  

Maksimum yönlendirici atlama sayısını yapılandırdığınızda, ağ bulmanın SNMP kullanarak sorgulayayapabileceğini ağ kesimlerinin ve yönlendiricilerin sayısını sınırlandıracaksınız.  

Yapılandırdığınız atlama sayısı, ağ bulmanın sorgulayabileceği ek cihazların ve ağ kesimlerinin sayısını sınırlar.  

Örneğin, **0** (sıfır) yönlendirici atlamaları olan bir topoloji bulma, kaynak sunucunun bulunduğu alt ağı bulur. Bu alt ağdaki tüm yönlendiricileri içerir.  

Aşağıdaki diyagramda, yalnızca topoloji ağ bulma sorgusunun, sunucu 1 ' de çalıştırıldığında, 0 yönlendirici atlaması belirtildiğinde bulduğu durum gösterilmektedir: alt ağ D ve yönlendirici 1.  

 ![Sıfır yönlendirici atlayan bulma görüntüsü](media/Disc-0.gif)  

 Aşağıdaki diyagramda, bir topoloji ve istemci ağı bulma sorgusunun, sunucu 1 ' de 0 yönlendirici atlaması belirtilen şekilde ne zaman bulduğu gösterilmektedir: alt ağ D ve yönlendirici 1 ve alt ağ D üzerinde tüm olası istemciler.  

 ![Tek yönlendiriciyle atlayan bulma görüntüsü](media/Disc-1.gif)  

 Ek yönlendirici atlamalarının keşfedilen ağ kaynakları miktarını nasıl artıradığının daha iyi bir fikir edinmek için aşağıdaki ağı göz önünde bulundurun:  

 ![İki yönlendirici atmayla bulma görüntüsü](media/Disc-2.gif)  

 Tek yönlendiriciyle sunucu 1 ' den yalnızca topoloji ağ bulma işlemi çalıştırmak aşağıdaki varlıkları bulur:  

-   Yönlendirici 1 ve alt ağ 10.1.10.0 (sıfır atlamalarla bulundu)  

-   Alt ağlar 10.1.20.0 ve 10.1.30.0, alt ağ A ve yönlendirici 2 (ilk atlamada bulunur)  

> [!WARNING]  
>  Yönlendirici atlama sayısının her artışı, keşfedilebilir kaynak sayısını önemli ölçüde artırabilir ve ağ bulmanın kullandığı ağ bant genişliğini artırabilir.  



##  <a name="server-discovery"></a><a name="bkmk_aboutServer"></a>Sunucu bulma  
**Yapılandırılabilir:** Eşleşen  

Kullanıcı tarafından yapılandırılabilen bulma yöntemlerine ek olarak Configuration Manager, **sunucu bulma** (SMS_WINNT_SERVER_DISCOVERY_AGENT) adlı bir işlem kullanır. Bu bulma yöntemi, yönetim noktası olarak yapılandırılmış bir bilgisayar gibi site sistemleri olan bilgisayarlar için kaynak kayıtları oluşturur.  



##  <a name="common-features-of-active-directory-group-discovery-system-discovery-and-user-discovery"></a><a name="bkmk_shared"></a>Active Directory grubu bulmanın, sistem bulmanın ve Kullanıcı bulmanın ortak özellikleri  
Bu bölümde, aşağıdaki bulma yöntemlerinde ortak olan özellikler hakkında bilgi verilmektedir:  

-   Active Directory Grup Saptama  

-   Active Directory Sistem Saptama  

-   Active Directory Kullanıcı Saptama  

> [!NOTE]  
>  Bu bölümdeki bilgiler Active Directory orman keşfi için geçerlidir.  

Bu üç bulma yöntemi yapılandırma ve işleme benzerdir. Bunlar, Active Directory Domain Services depolanan kaynakların grup üyelikleri hakkında bilgisayarları, kullanıcıları ve bilgileri bulabilirler. Bulma işlemi bir bulma Aracısı tarafından yönetilir. Aracı, bulma 'nın çalışmak üzere yapılandırıldığı her sitede site sunucusunda çalışır. Bu bulma yöntemlerinin her birini, Yerel ormandaki veya uzak ormanlardaki konum örnekleri olarak bir veya daha fazla Active Directory konumu arayacak şekilde yapılandırabilirsiniz.  

Bulma, kaynaklar için güvenilmeyen bir ormanı aradığında, bulma aracısının başarılı olması için aşağıdakileri çözümleyebilmesi gerekir:  

-   Active Directory sistem bulma kullanarak bir bilgisayar kaynağını bulmak için, bulma aracısının kaynağın FQDN 'sini çözümleyebilmesi gerekir. FQDN 'yi çözümleyemezse kaynağı NetBIOS adına göre çözümlemeye çalışır.  

-   Active Directory Kullanıcı bulma veya Active Directory Grup bulma kullanarak bir kullanıcı veya grup kaynağı bulmak için, bulma aracısının Active Directory konumu için belirttiğiniz etki alanı denetleyicisi adının FQDN 'sini çözümleyebilmesi gerekir.  

Belirttiğiniz her konum için, konumun Active Directory alt kapsayıcılarının özyinelemeli bir aramasını etkinleştirmek gibi ayrı arama seçeneklerini yapılandırabilirsiniz. Ayrıca, bu konumu ararken kullanılacak benzersiz bir hesap da yapılandırabilirsiniz. Bu hesap, birden çok ormanda birden çok Active Directory konumu aramak için bir sitede bulma yöntemi Yapılandırma esnekliği sağlar. Tüm konumlar için izinleri olan tek bir hesap yapılandırmanız gerekmez.  

Bu üç bulma yönteminin her biri belirli bir sitede çalıştığında, bu sitedeki Configuration Manager site sunucusu, Active Directory kaynaklarını bulmak için belirtilen Active Directory ormanındaki en yakın etki alanı denetleyicisiyle iletişim kurar. Etki alanı ve orman desteklenen Active Directory modunda olabilir. Her bir konum örneğine atadığınız hesabın, belirtilen Active Directory konumlarında **okuma** erişim izni olması gerekir.

Bulgu nesneler için belirtilen konumları arar ve ardından bu nesneler hakkında bilgi toplamaya çalışır. Bir kaynakla ilgili yeterli bilgi tanımlanabilecek şekilde DDR oluşturulur. Gerekli bilgiler, kullanılmakta olan bulma yöntemine bağlı olarak farklılık gösterir.  

Yerel Active Directory sunucularının sorgulanmasının avantajlarından yararlanmak için aynı bulma yöntemini farklı Configuration Manager sitelerde çalışacak şekilde yapılandırırsanız, her siteyi benzersiz bir keşif seçenekleri kümesiyle yapılandırabilirsiniz. Bulma verileri hiyerarşideki her siteyle paylaşıldığından, her kaynağı tek bir kez etkin bir şekilde bulmak için bu yapılandırmaların arasındaki çakışmaktan kaçının.

Daha küçük ortamlar için, her bulma yöntemini hiyerarşinizdeki tek bir sitede çalıştırmayı göz önünde bulundurun. Bu yapılandırma, yönetim yükünü ve birden çok bulma eylemi için aynı kaynakları yeniden bulma potansiyelini azaltır. Bulmayı çalıştıran sitelerin sayısını en aza indirmeniz durumunda, bulmanın kullandığı genel ağ bant genişliğini azaltabilirsiniz. Ayrıca, oluşturulan ve site sunucularınız tarafından işlenmesi gereken toplam DDR sayısını da azaltabilirsiniz.  

Bulma yöntemi yapılandırmalarının birçoğu kendi kendine açıklayıcıdır. Yapılandırmadan önce ek bilgiler gerektirebilecek bulma seçenekleri hakkında daha fazla bilgi için aşağıdaki bölümleri kullanın.  

Aşağıdaki seçenekler birden çok Active Directory bulma yöntemi ile kullanılabilir:  

-   [Delta Keşfi](#bkmk_delta)  

-   [Eski bilgisayar kayıtlarını etki alanına oturum açmaya göre filtrele](#bkmk_stalelogon)  

-   [Eski kayıtları bilgisayar parolasına göre filtrele](#bkmk_stalepassword)  

-   [Özelleştirilmiş Active Directory özniteliklerini arama](#bkmk_customAD)  


###  <a name="delta-discovery"></a><a name="bkmk_delta"></a>Delta Keşfi  
Kullanılabilir:  

-   Active Directory Grup Saptama  

-   Active Directory Sistem Saptama  

-   Active Directory Kullanıcı Saptama  

Delta Keşfi bağımsız bir bulma yöntemi değil, geçerli bulma yöntemleri için kullanılabilir bir seçenek değil. Delta Keşfi, geçerli keşif yönteminin son tam keşif döngüsünden bu yana yapılan değişiklikler için belirli Active Directory özniteliklerini arar. Öznitelik değişiklikleri, kaynağın bulma kaydını güncelleştirmek için Configuration Manager veritabanına gönderilir.  

Varsayılan olarak, Delta Keşfi beş dakikalık bir döngüde çalışır. Bu zamanlama, tam bulma döngüsünün tipik zamanlamalarından çok daha sık görülen bir noktadır. Delta Keşfi tam bulgu döngüsünden daha az site sunucusu ve ağ kaynakları kullandığından, bu sık kullanılan bir işlem mümkündür. Delta Keşfi kullandığınızda, bu bulma yöntemi için tam keşif döngüsünün sıklığını azaltabilirsiniz.  

Delta bulmanın algıladığı en yaygın değişiklikler aşağıda verilmiştir:  

-   Active Directory eklenen yeni bilgisayarlar veya kullanıcılar  

-   Temel bilgisayar ve Kullanıcı bilgilerinde yapılan değişiklikler  

-   Bir gruba eklenen yeni bilgisayarlar veya kullanıcılar  

-   Bir gruptan kaldırılan bilgisayarlar veya kullanıcılar  

-   Sistem grubu nesnelerinde yapılan değişiklikler  

Delta Keşfi yeni kaynakları ve grup üyeliğinde değişiklikleri algılayabilse de, bir kaynağın Active Directory silindiği tespit edilemez. Delta Keşfi tarafından oluşturulan DDR 'ler, tam bir keşif döngüsüyle oluşturulan DDR 'ler benzer şekilde işlenir.  

Her bulgu yönteminin özelliklerindeki **yoklama zamanlaması** sekmesinde Delta Keşfi yapılandırırsınız.  


###  <a name="filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a>Eski bilgisayar kayıtlarını etki alanına oturum açmaya göre filtrele  
Kullanılabilir:  

-   Active Directory Grup Saptama  

-   Active Directory Sistem Saptama  

Bulma işlemini, bilgisayarları eski bir bilgisayar kaydıyla hariç bırakacak şekilde yapılandırabilirsiniz. Bu dışlama, bilgisayarın son etki alanı oturum açma bilgilerini temel alır. Bu seçenek etkinleştirildiğinde Active Directory sistem bulma, tanımladığı her bilgisayarı değerlendirir. Active Directory Grup keşfi, bulunan bir grubun üyesi olan her bilgisayarı değerlendirir.  

Bu seçeneği kullanmak için:  

-   Bilgisayarların **lastLogonTimestamp** özniteliği Active Directory Domain Services güncelleştirilecek şekilde yapılandırılması gerekir.  

-   Active Directory etki alanı işlev düzeyinin Windows Server 2003 veya üzeri olarak ayarlanması gerekir.  

Bu ayar için kullanmak istediğiniz son oturum açma zamanından sonra geçen süreyi yapılandırırken, etki alanı denetleyicileri arasında çoğaltma aralığını göz önünde bulundurun.  

Filtreleme, **Active Directory sistem bulma özellikleri** ve **Active Directory grubu bulma özellikleri** iletişim kutularında **seçenek** sekmesinde yapılandırılır. **Yalnızca belirli bir süre içinde bir etki alanında oturum açan bilgisayarları bulmayı**seçin.  

> [!WARNING]  
>  Bu filtreyi yapılandırıp **eski kayıtları bilgisayar parolasına göre filtreleyerek**, bulma işlemi her iki filtrenin ölçütlerine uyan bilgisayarları dışlar.  


###  <a name="filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a>Eski kayıtları bilgisayar parolasına göre filtrele  
Kullanılabilir:  

-   Active Directory Grup Saptama  

-   Active Directory Sistem Saptama  

Bulma işlemini, bilgisayarları eski bir bilgisayar kaydıyla hariç bırakacak şekilde yapılandırabilirsiniz. Bu dışlama, bilgisayar tarafından son bilgisayar hesabı parolasının güncelleştirilmesini temel alır. Bu seçenek etkinleştirildiğinde Active Directory sistem bulma, tanımladığı her bilgisayarı değerlendirir. Active Directory Grup keşfi, bulunan bir grubun üyesi olan her bilgisayarı değerlendirir.  

Bu seçeneği kullanmak için:  

-   Bilgisayarların, Active Directory Domain Services **pwdLastSet** özniteliğini güncelleştirmek için yapılandırılması gerekir.  

Bu seçeneği yapılandırırken, bu öznitelik için güncelleştirmeler aralığını göz önünde bulundurun. Ayrıca, etki alanı denetleyicileri arasındaki çoğaltma aralığını göz önünde bulundurun.  

Filtreleme, **Active Directory sistem bulma özellikleri** ve **Active Directory grubu bulma özellikleri** iletişim kutularında **seçenek** sekmesinde yapılandırılır. **Belirli bir süre Içinde yalnızca bilgisayar hesabı parolalarını güncelleştiren bilgisayarları bulmayı**seçin.  

> [!WARNING]  
>  Bu filtreyi yapılandırıp **etki alanı oturum açma ile eski kayıtları filtreleyerek**, bulma işlemi her iki filtrenin ölçütlerine uyan bilgisayarları dışlar.  


###  <a name="search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a>Özelleştirilmiş Active Directory özniteliklerini ara  
 Kullanılabilir:  

-   Active Directory Sistem Saptama  

-   Active Directory Kullanıcı Saptama  

Her bulma yöntemi, keşfedilebilir Active Directory özniteliklerin benzersiz bir listesini destekler.  

Özelleştirilmiş özniteliklerin listesini, **Active Directory sistem bulma özellikleri** ve **Active Directory Kullanıcı keşfi özellikleri** iletişim kutularındaki **Active Directory öznitelikleri** sekmesinde görüntüleyebilir ve yapılandırabilirsiniz.  
