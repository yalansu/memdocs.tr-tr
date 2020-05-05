---
title: Site kaynaklarını bulma
titleSuffix: Configuration Manager
description: Configuration Manager istemcilerinin site kaynaklarını bulmak için hizmet konumunu nasıl ve ne zaman kullandığını öğrenin.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a72ff9947f6ca31ce2158c5c763602b34948a15c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075668"
---
# <a name="learn-how-clients-find-site-resources-and-services-for-configuration-manager"></a>İstemcilerin Configuration Manager için site kaynaklarını ve hizmetleri nasıl bulkullandığını öğrenin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager istemcileri, iletişim kurabileceği ve istemcilerin kullanıma yönlendirildiği Site sistemi sunucularını bulmak için *hizmet konumu* adlı bir işlem kullanır. İstemcilerin site kaynaklarını bulmak için hizmet konumunu nasıl ve ne zaman kullandığını anlamak, sitelerinizi istemci görevlerini başarıyla destekleyecek şekilde yapılandırmanıza yardımcı olabilir. Bu yapılandırma, sitenin Active Directory Domain Services (AD DS) ve DNS gibi etki alanı ve ağ yapılandırmalarına karşı etkileşimini gerektirebilir. Ya da daha karmaşık alternatifleri yapılandırmanızı gerektirebilir.  

Hizmet sağlayan site sistemi rollerinin örnekleri şunlardır:

- İstemciler için çekirdek site sistemi sunucusu.
- Yönetim noktası.
- Dağıtım noktaları ve yazılım güncelleştirme noktaları gibi istemcinin iletişim kurabildiği ek site sistemi sunucuları.  



##  <a name="fundamentals-of-service-location"></a><a name="bkmk_fund"></a>Hizmet konumu temelleri  
 İstemci, iletişim kurabildiği bir yönetim noktası bulmak için hizmet konumunu kullanırken geçerli ağ konumunu, iletişim protokol tercihini ve atanan siteyi değerlendirir.  

**İstemci bir yönetim noktasıyla iletişim kurar:**  
- Site için diğer yönetim noktalarıyla ilgili bilgileri indirin, böylece gelecekteki hizmet konumu döngüleri için bilinen yönetim noktalarının bir listesini ( *MP listesi*olarak bilinir) oluşturabilir.  
- Envanter ve durum gibi yapılandırma ayrıntılarını karşıya yükleyin.  
- İstemci üzerindeki konfigürasyonları ayarlayan bir ilke indirin ve bu yazılımın istemcisini veya yüklemesi gereken yazılım ve diğer ilgili görevleri bilgilendirebilirler.  
- İstemcinin kullanmak üzere yapılandırıldığı hizmetler sağlayan ek site sistem rolleriyle ilgili bilgi isteyin. Örnek olarak, istemcinin yükleyebileceği yazılımın dağıtım noktaları veya güncelleştirmelerin alınacağı bir yazılım güncelleştirme noktası bulunur.  

**Configuration Manager istemcisi bir hizmet konumu isteği yapar:**  
- Her 25 saatte bir sürekli işlem.  
- İstemci, ağ yapılandırması veya konumunda bir değişiklik algıladığında.  
- Bilgisayardaki **Ccmexec. exe** hizmeti (çekirdek istemci hizmeti) başladığında.  
- İstemci, gerekli bir hizmeti sağlayan bir site sistem rolünü bulmalıdır.  

**Bir istemci, site sistem rollerini barındıran sunucuları bulmaya**çalıştığında, istemci protokolünü (http veya https) destekleyen bir site sistem rolünü bulmak için hizmet konumunu kullanır. Varsayılan olarak, istemciler tarafından kullanılabilen en güvenli yöntemi kullanır. Aşağıdaki topluluklara bir göz atın:  

- HTTPS kullanmak için, bir genel anahtar altyapısına (PKI) sahip olmanız ve PKI sertifikalarını istemcilere ve sunuculara yüklemeniz gerekir. Sertifikaların nasıl kullanılacağı hakkında bilgi için bkz. [Configuration Manager Için PKI sertifikası gereksinimleri](../../../core/plan-design/network/pki-certificate-requirements.md).  

- Internet Information Services (IIS) kullanan ve istemcilerinden gelen iletişimi destekleyen bir site sistem rolü dağıttığınızda, istemcilerin site sistemine HTTP veya HTTPS kullanarak bağlandığını belirtmeniz gerekir. HTTP kullanırsanız imzalama ve şifreleme seçeneklerini de göz önünde bulundurmanız gerekir. Daha fazla bilgi için, [güvenlik planında](../../../core/plan-design/security/plan-for-security.md) [Imzalama ve şifrelemeyi planlama](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) konusuna bakın.  

##  <a name="service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a>Hizmet konumu ve istemcilerin atanan yönetim noktalarını belirleme şekli  
Bir istemci birincil siteye ilk atandığında, bu site için varsayılan bir yönetim noktası seçer. Birincil siteler birden çok yönetim noktasını destekler ve her bir istemci, varsayılan Yönetim noktası olarak bir yönetim noktasını bağımsız olarak tanımlar. Bu varsayılan Yönetim noktası daha sonra istemcinin atanan yönetim noktası olur. (İstemci yükleme komutlarını, yüklü olduğunda bir istemci için atanan yönetim noktasını ayarlamak için de kullanabilirsiniz.)  

İstemci, istemcinin geçerli ağ konumuna ve sınır grubu yapılandırmalarına bağlı olarak iletişim kuracak bir yönetim noktası seçer. Atanmış bir yönetim noktasına sahip olsa da, bu, istemcinin kullandığı yönetim noktası olmayabilir.  

> [!NOTE]  
> İstemci, diğer iletişimler proxy veya yerel yönetim noktasına gönderilse bile, kayıt iletileri ve belirli ilke iletileri için atanan yönetim noktasını kullanır.

Tercih edilen yönetim noktalarını kullanabilirsiniz. Tercih edilen yönetim noktaları, istemcinin atanmış sitesinden, istemcinin site sistem sunucularını bulmak için kullandığı bir sınır grubuyla ilişkilendirilmiş yönetim noktalarıdır. Site sistemi sunucusu olarak bir sınır grubuyla tercih edilen bir yönetim noktasının ilişkilendirmesi, dağıtım noktalarının veya durum geçiş noktalarının bir sınır grubuyla ilişkilendirilmesiyle benzerdir. Bir istemci atanan sitesinden bir yönetim noktası kullanırken hiyerarşi için tercih edilen yönetim noktalarını etkinleştirirseniz, atanan sitesinden diğer yönetim noktalarını kullanmadan önce tercih edilen bir yönetim noktasını kullanmayı dener.  

Yönetim noktası benzeşimini yapılandırmak için TechNet.com üzerindeki [Yönetim noktası benzeşimi](https://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx) bloguna ait bilgileri de kullanabilirsiniz. Yönetim noktası benzeşimi, atanmış yönetim noktalarının varsayılan davranışını geçersiz kılar ve istemcinin bir veya daha fazla belirli yönetim noktası kullanmasına izin verir.  

İstemcinin bir yönetim noktasıyla iletişim kurabilmesi her seferinde, Windows Yönetim Araçları (WMI) ' de yerel olarak depoladığı MP listesini denetler. İstemci, yüklendiğinde bir başlangıç MP listesi oluşturur. İstemci daha sonra listeyi hiyerarşideki her bir yönetim noktasıyla ilgili ayrıntılarla düzenli olarak güncelleştirir.  

İstemci MP listesinde geçerli bir yönetim noktası bulamazsa, kullanabileceği bir yönetim noktası bulana kadar aşağıdaki hizmet konumu kaynaklarını sırayla arar:  

1.  Yönetim noktası  
2.  AD DS  
3.  DNS  
4.  WINS  

Bir istemci bir yönetim noktasını başarıyla bulduktan ve iletişim kurduğunda, hiyerarşide kullanılabilen yönetim noktalarının geçerli listesini indirir ve yerel MP listesini güncelleştirir. Bu, etki alanı ile birleşik olan ve olmayan istemciler için eşit oranda geçerlidir.  

Örneğin, internet üzerindeki bir Configuration Manager istemcisi Internet tabanlı bir yönetim noktasına bağlanırsa, yönetim noktası istemciye sitedeki kullanılabilir internet tabanlı yönetim noktalarının bir listesini gönderir. Benzer şekilde, etki alanı ile birleşik olan veya çalışma gruplarında bulunan istemciler de kullanabilecekleri yönetim noktalarının listesini alır.  

İnternet için yapılandırılmayan bir istemci, yalnızca İnternet 'e yönelik yönetim noktaları sağlanmaz. İnternet için yapılandırılan çalışma grubu istemcileri, yalnızca İnternet 'e yönelik yönetim noktalarıyla iletişim kurar.  

##  <a name="the-mp-list"></a><a name="BKMK_MPList"></a>MP listesi  
MP listesi, istemcinin daha önce tanımladığı yönetim noktalarının öncelikli listesi olduğundan, istemci için tercih edilen hizmet konumu kaynağıdır. Bu liste, istemci listeyi güncelleştirdiğinde her bir kullanıcı tarafından kendi ağ konumlarına göre sıralanır ve ardından istemci WMI'sinde yerel olarak depolanır.  

### <a name="building-the-initial-mp-list"></a>Başlangıç MP listesini oluşturma  
İstemci yüklemesi sırasında, istemcinin başlangıç MP listesini oluşturmak için aşağıdaki kurallar kullanılır:  

- Başlangıç listesi, istemci yüklemesi sırasında belirtilen yönetim noktalarını içerir ( **SMSMP**= veya **/MP** seçeneğini kullandığınızda).  
- İstemci, yayımlanan Yönetim noktaları için AD DS sorgular. AD DS tanımlanması için, yönetim noktasının istemcinin atanan sitesinden olması ve istemci ile aynı ürün sürümüne sahip olması gerekir.  
- İstemci yüklemesi sırasında bir yönetim noktası belirtilmemişse ve Active Directory şeması genişletilmemişse, istemci yayımlanan Yönetim noktaları için DNS ve WINS 'yi denetler.  
- İstemci başlangıç listesini oluşturduğunda, hiyerarşideki bazı yönetim noktaları hakkındaki bilgiler bilinmiyor olabilir.  

### <a name="organizing-the-mp-list"></a>MP listesini düzenleme  
İstemciler, aşağıdaki sınıflandırmaları kullanarak yönetim noktaları listelerini düzenler:  

- **Proxy**: ikincil sitede bir yönetim noktası.  
- **Yerel**: istemci, site sınırları tarafından tanımlanan geçerli ağ konumu ile ilişkili olan herhangi bir yönetim noktası. Sınırlar hakkında aşağıdaki bilgilere göz önünde edin:
  - Bir istemci birden fazla sınır grubuna ait olduğunda, yerel yönetim noktalarının listesi, istemcinin geçerli ağ konumunun da içinde bulunduğu tüm sınırların birleşimi tarafından belirlenir.  
  - Yerel yönetim noktaları, istemci, sınır gruplarına hizmet veren yönetim noktaları olan başka bir siteyle ilişkili bir ağ konumunda olmadığı takdirde, genellikle istemcinin atanan yönetim noktalarının bir alt kümesidir.   


- **Atandı**: istemcinin atanmış sitesi için bir site sistemi olan herhangi bir yönetim noktası.  

Tercih edilen yönetim noktalarını kullanabilirsiniz. Bir sitede bir sınır grubuyla ilişkilendirilmemiş veya istemcinin geçerli ağ konumuyla ilişkili bir sınır grubunda olmayan yönetim noktaları, tercih edilen olarak kabul edilmez. İstemci, kullanılabilir bir tercih edilen yönetim noktasını tanımlayamayacak şekilde kullanılacaktır.  

### <a name="selecting-a-management-point-to-use"></a>Kullanılacak yönetim noktası seçme  
Tipik iletişimler için, istemci, istemcinin ağ konumuna bağlı olarak sınıflandırmalardan bir yönetim noktası kullanmayı dener:  

1.  Ara sunucu  
2.  Yerel  
3.  Atandı  

Ancak istemci, diğer iletişimler proxy veya yerel yönetim noktasına gönderilse bile, kayıt iletileri ve belirli ilke iletileri için atanan yönetim noktasını kullanır.  

Her bir sınıflandırma içinde (proxy, yerel veya atanan), istemci, aşağıdaki sırayla Tercihler temelinde bir yönetim noktası kullanmayı dener:  

1.  Güvenilir veya yerel bir ormanda olan HTTPS özelliği (istemci HTTPS iletişimi için yapılandırıldığında)  
2.  Güvenilir veya yerel bir ormanda olmayan HTTPS özelliği (istemci HTTPS iletişimi için yapılandırıldığında)  
3.  Güvenilen veya yerel bir ormanda HTTP özelliği  
4.  Güvenilir veya yerel bir ormanda olmayan HTTP özelliği  

Tercihler tarafından sıralanan yönetim noktaları kümesinden istemci, listedeki ilk yönetim noktasını kullanmayı dener. Bu yönetim noktaları listesi rastgele ve sıralanamıyor. Listenin sırası, istemci MP listesini her güncelleştirilişinde değişebilir.  

İstemci ilk yönetim noktasıyla iletişim kuramazsa, listesinde birbirini izleyen her yönetim noktasını dener. Tercih edilmeyen yönetim noktalarını denemeden önce sınıflandırmadaki her bir tercih edilen yönetim noktasını dener. Bir istemci sınıflandırmadaki hiçbir yönetim noktasıyla iletişim kuramadıysanız bir sonraki sınıflandırmadan tercih edilen bir yönetim noktasıyla iletişim kurmayı dener ve daha sonra kullanmak üzere bir yönetim noktası bulana kadar bu şekilde devam eder.  

Bir istemci bir yönetim noktasıyla iletişim kurduktan sonra, şu kadar aynı yönetim noktasını kullanmaya devam eder:  

- 25 saat geçti.  
- İstemci, 10 dakikalık bir süre içinde beş deneme için yönetim noktasıyla iletişim kuramadı.

İstemci daha sonra kullanılacak yeni bir yönetim noktasını rastgele seçer.  

##  <a name="active-directory"></a><a name="bkmk_ad"></a>Active Directory  
Etki alanı ile birleşik istemciler hizmet konumu için AD DS kullanabilir. Bu, sitelerin [verileri Active Directory'ye yayımlamasını](https://technet.microsoft.com/library/hh696543.aspx)gerektirir.  

İstemci, aşağıdaki koşulların tümü doğru olduğunda hizmet konumu için AD DS kullanabilir:  

- Active Directory [şeması genişletildi](https://technet.microsoft.com/library/mt345589.aspx) veya System Center 2012 Configuration Manager için genişletildi.  
- [Active Directory ormanı yayımlama için yapılandırılmıştır](https://technet.microsoft.com/library/hh696542.aspx)ve Configuration Manager siteleri yayımlamak üzere yapılandırılır.  
- İstemci bilgisayarı, bir Active Directory etki alanının üyesi olduğunda ve bir genel katalog sunucusuna erişebildiğinde.  

İstemci, AD DS hizmet konumu için kullanmak üzere bir yönetim noktası bulamazsa DNS kullanmaya çalışır.  

##  <a name="dns"></a><a name="bkmk_dns"></a>BKZ  
İntranetteki istemciler hizmet konumu için DNS kullanabilir. Bu, hiyerarşideki sitelerden en az birinin DNS'teki yönetim noktaları hakkında bilgi yayımlamasını gerektirir.  

Aşağıdaki koşullardan herhangi biri doğruysa, hizmet konumu için DNS kullanabilirsiniz:
- AD DS şeması Configuration Manager desteklemek için genişletilmedi.
- İntranetteki istemciler, Configuration Manager yayımlama için etkinleştirilmemiş bir ormanda yer alır.  
- Çalışma grubu bilgisayarlarında istemcileriniz var ve bu istemciler yalnızca İnternet istemci yönetimi için yapılandırılmamış. (İnternet için yapılandırılmış bir çalışma grubu istemcisi, yalnızca İnternet 'e yönelik yönetim noktalarıyla iletişim kurar ve hizmet konumu için DNS kullanmaz.)  
- [İstemcileri yönetim noktalarından DNS bulmak için yapılandırabilirsiniz](https://technet.microsoft.com/library/gg682055).  

Bir site, aşağıdaki durumlarda yönetim noktaları için hizmet konumu kayıtlarını DNS'te yayımlar:  

- Yayımlama yalnızca intranetten gelen istemci bağlantılarını kabul eden yönetim noktaları için uygulanabilir olduğunda.  
- Yayımlama, yönetim noktası bilgisayarının DNS bölgesine bir hizmet konumu kaynak kaydı (SRV RR) eklediğinde. DNS'te söz konusu bilgisayara karşılık gelen bir konak girişi olmalıdır.  

Varsayılan olarak, etki alanına katılmış istemciler yönetim noktası kayıtları için DNS 'i istemcinin yerel etki alanından arar. DNS 'de yayımlanan yönetim noktası bilgilerine sahip bir etki alanı için etki alanı soneki belirten bir istemci özelliğini yapılandırabilirsiniz.  

DNS soneki istemci özelliğinin nasıl yapılandırılacağı hakkında daha fazla bilgi için bkz. [DNS yayımlaması kullanarak istemci bilgisayarları yönetim noktalarını bulmak için yapılandırma](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

İstemci, hizmet konumu için DNS 'den kullanılacak bir yönetim noktası bulamazsa, WINS kullanmaya çalışır.  

### <a name="publish-management-points-to-dns"></a>Yönetim noktalarını DNS'ye yayımlama  
Yönetim noktalarını DNS'ye yayımlamak için, aşağıdaki iki koşulun doğru olması gerekir:  

- DNS sunucularınızın en az 8.1.2 sürümlü bir BIND kullanarak hizmet konumu kaynak kayıtlarını desteklemesi.  
- Configuration Manager içindeki yönetim noktaları için belirtilen intranet FQDN 'Lerinin, DNS 'de konak girişleri (örneğin, A kayıtları) vardır.  

> [!IMPORTANT]  
> Configuration Manager DNS yayımlaması ayrık ad alanını desteklemez. Ayrık bir ad alanınız varsa, yönetim noktalarını DNS 'ye el ile yayımlayabilirsiniz veya bu bölümde belgelenen diğer hizmet konumu yöntemlerinden birini kullanabilirsiniz.  

**DNS sunucularınız otomatik güncelleştirmeleri destekledikleri zaman**, intranet üzerindeki YÖNETIM noktalarını DNS 'ye otomatik olarak yayımlamak üzere Configuration Manager yapılandırabilir veya bu kayıtları DNS 'ye el ile yayımlayabilirsiniz. Yönetim noktaları DNS'ye yayımlandığında, intranet FQDN'leri ve bağlantı noktası numaraları, hizmet konumu (SRV) kaydına yayımlanır. DNS yayımlamayı, sitenin yönetim noktası bileşen özelliklerindeki bir sitede yapılandırırsınız. Daha fazla bilgi için bkz. [Configuration Manager Için site bileşenleri](../../../core/servers/deploy/configure/site-components.md).  

**DNS bölgeniz dinamik güncelleştirmeler için "yalnızca güvenli" olarak ayarlandığında**, yalnızca DNS 'de yayımlanacak ilk yönetim noktası, varsayılan izinlerle bu işlemi başarıyla yapabilir.

Yalnızca bir yönetim noktası DNS kaydını başarıyla yayımlayıp değiştirebiliyorsanız ve yönetim noktası sunucusu sağlıklı ise, istemcileri bu yönetim noktasından tam MP listesini alabilir ve ardından tercih edilen yönetim noktalarını bulabilir.


**DNS sunucularınız otomatik güncelleştirmeleri desteklemiyor ancak hizmet konumu kayıtlarını destekliyorsa**, yönetim noktalarını DNS'ye manuel olarak yayımlayabilirsiniz. Bunu gerçekleştirmek için, hizmet konumu kaynak kaydını (SRV RR) DNS'ye el ile belirtmeniz gerekir.  

Configuration Manager, hizmet konumu kayıtları için RFC 2782 ' ü destekler. Bu kayıtlar şu biçimdedir: *_Service. _Proto. Name TTL sınıfı SRV öncelik ağırlığı bağlantı noktası hedefi*  

Configuration Manager bir yönetim noktası yayımlamak için, aşağıdaki değerleri belirtin:  

- **_Service**: **_mssms_mp**_&lt;sitekodu\>girin; &lt;burada\> sitekodu yönetim noktasının site kodudur.  
- **._Proto**: **._tcp**belirtin.  
- **.Name**: Yönetim noktasının DNS son ekini girin, örneğin **contoso.com**.  
- **TTL**: Dört saat anlamına gelen **14400**girin.  
- **Sınıf**: **IN** belirtin (RFC 1035 ile uyumlu şekilde).  
- **Öncelik**: Configuration Manager bu alanı kullanmaz.
- **Ağırlık**: Configuration Manager bu alanı kullanmaz.  
- **Bağlantı Noktası**: Yönetim noktasının kullandığı bağlantı noktası numarasını girin, örneğin HTTP için **80** ve HTTPS için **443** .  

  > [!NOTE]  
  >  SRV kayıt bağlantı noktası, yönetim noktasının kullandığı iletişim bağlantı noktasıyla eşleşmelidir. Bu, varsayılan olarak HTTP iletişimi için **80** , HTTPS iletişimi için **443** ' dir.  

- **Hedef**: Yönetim noktası site rolüyle yapılandırılan site sistem için intranet FQDN'sini girin.  

Windows Server DNS'i kullanırsanız, intranet yönetim noktaları için bu DNS kaydını girmek üzere aşağıdaki yordamı kullanabilirsiniz. DNS için farklı bir uygulama kullanırsanız, bu bölümde bulunan, alan değerleri hakkındaki bilgileri kullanın ve bu yordamı uyarlamak için o DNS belgesine danışın.  

##### <a name="to-configure-automatic-publishing"></a>Otomatik yayımlamayı yapılandırmak için:  

1.  Configuration Manager konsolunda, **Yönetim** > **Site yapılandırması** > **siteler**' i genişletin.  

2.  Sitenizi seçin ve ardından **site bileşenlerini Yapılandır**' ı seçin.  

3.  **Yönetim noktası**seçin.  

4.  Yayımlamak istediğiniz yönetim noktalarını seçin. (Bu seçim, AD DS ve DNS 'de yayımlama için geçerlidir.)  

5.  DNS 'de yayımlamak için kutuyu işaretleyin. Bu kutu:  

    - DNS 'de hangi yönetim noktalarının yayımlanacağını seçmenizi sağlar.  

    - AD DS yayımlamayı yapılandırmaz.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Windows Server'da DNS'ye yönetim noktalarını el ile yayımlamak için  

1.  Configuration Manager konsolunda, site sistemlerinin intranet FQDN 'lerini belirtin.  

2.  DNS yönetim konsolunda, yönetim noktası bilgisayarı için DNS bölgesini seçin.  

3.  Site sisteminin intranet FQDN'si için bir konak kaydının (A veya AAAA) bulunduğunu doğrulayın. Bu kayıt yoksa, onu oluşturun.  

4.  **Yeni diğer kayıtlar** seçeneğini kullanarak, **kaynak kaydı türü** iletişim kutusunda **hizmet konumu (SRV)** öğesini seçin, **kayıt oluştur**' u seçin, aşağıdaki bilgileri girin ve **bitti**' yi seçin:  

    - **Etki Alanı**: Gerekirse, yönetim noktasının DNS sonekini girin, örneğin **contoso.com**.  
    - **Hizmet**: **_mssms_mp**_&lt;sitekodu\>yazın; &lt;burada\> sitekodu yönetim noktasının site kodudur.  
    - **Protokol**: **_tcp**yazın.  
    - **Öncelik**: Configuration Manager bu alanı kullanmaz.  
    - **Ağırlık**: Configuration Manager bu alanı kullanmaz.  
    - **Bağlantı Noktası**: Yönetim noktasının kullandığı bağlantı noktası numarasını girin, örneğin HTTP için **80** ve HTTPS için **443** .  

      > [!NOTE]  
      > SRV kayıt bağlantı noktası, yönetim noktasının kullandığı iletişim bağlantı noktasıyla eşleşmelidir. Bu, varsayılan olarak HTTP iletişimi için **80** , HTTPS iletişimi için **443** ' dir.  

    - **Bu hizmeti sunan konak**: yönetim noktası site rolüyle yapılandırılan site sistemi için BELIRTILEN intranet FQDN 'sini girin.  

Bu adımları, DNS'ye yayımlamak istediğiniz, intranetteki her bir yönetim noktası için tekrarlayın.  

##  <a name="wins"></a><a name="bkmk_wins"></a>DÜR  
Diğer hizmet konumu mekanizmaları başarısız olduğunda, istemciler WINS'i denetleyerek bir ilk yönetim noktası bulabilir.  

Varsayılan olarak, birincil site, sitede HTTP için yapılandırılan ilk yönetim noktasını ve HTTPS için yapılandırılan ilk yönetim noktasını WINS 'te yayımlar.  

İstemcilerin WINS'de bir HTTP yönetim noktası bulmasını istemiyorsanız, istemcileri CCMSetup.exe Client.msi özelliği **SMSDIRECTORYLOOKUP=NOWINS**ile yapılandırın.  
