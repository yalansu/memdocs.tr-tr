---
title: Güvenliği planlama
titleSuffix: Configuration Manager
description: Configuration Manager ' deki güvenlikle ilgili en iyi uygulamaları ve diğer bilgileri alın.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0cdb14d282cbfa93655d6678b12b5f0837a225aa
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699288"
---
# <a name="plan-for-security-in-configuration-manager"></a>Configuration Manager Güvenlik için plan yapın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager uygulamanıza güvenlik planlaması yaparken göz önünde bulundurmanız gereken kavramlar açıklanmaktadır. Aşağıdaki bölümleri içerir:  

- [Sertifikaları planlayın (otomatik imzalı ve PKI)](#BKMK_PlanningForCertificates)  
  - [Şifreleme: yeni nesil (CNG) sertifikaları](#bkmk_plan-cng)  
  - [Gelişmiş HTTP](#bkmk_plan-ehttp)  
  - [CMG ve CDP sertifikaları](#bkmk_plan-cmgcdp)  
  - [Site sunucusu imzalama sertifikası (otomatik imzalı)](#bkmk_plansitesign)  
  - [PKI sertifikası iptali](#BKMK_PlanningForCRLs)  
  - [PKI güvenilir kök sertifikaları ve sertifika verenler](#BKMK_PlanningForRootCAs)  
  - [PKI istemci sertifikası seçimi](#BKMK_PlanningForClientCertificateSelection)  
  - [PKI sertifikaları ve internet tabanlı istemci yönetimi için geçiş stratejisi](#BKMK_PlanningForPKITransition)  

- [Güvenilen kök anahtarı planlayın](#BKMK_PlanningForRTK)  

- [İmzalama ve şifrelemeyi planlayın](#BKMK_PlanningForSigningEncryption)  

- [Rol tabanlı yönetimi planlayın](#BKMK_PlanningForRBA)  

- [Azure Active Directory için plan yapın](#bkmk_planazuread)  

- [SMS sağlayıcısı kimlik doğrulamasını planlayın](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Sertifikaları planlayın (otomatik imzalı ve PKI)  

Configuration Manager, otomatik olarak imzalanan sertifikaların ve ortak anahtar altyapısı (PKI) sertifikalarının bir birleşimini kullanır.  

Mümkün olduğunda PKI sertifikalarını kullanın. Daha fazla bilgi için bkz. [PKI sertifikası gereksinimleri](../network/pki-certificate-requirements.md). Configuration Manager, mobil cihazlar için kayıt sırasında PKI sertifikaları istediğinde, Active Directory Domain Services ve bir kuruluş sertifika yetkilisini kullanmanız gerekir. Diğer tüm PKI sertifikaları için bunları Configuration Manager bağımsız olarak dağıtın ve yönetin. 

İstemci bilgisayarlar Internet tabanlı site sistemlerine bağlandıklarında PKI sertifikaları gereklidir. Bulut yönetimi ağ geçidi ve bulut dağıtım noktasıyla ilgili bazı senaryolar da PKI sertifikaları gerektirir. Daha fazla bilgi için bkz. [İnternet 'te Istemcileri yönetme](../../clients/manage/manage-clients-internet.md).

Bir PKI kullandığınızda, bir sitedeki site sistemleri arasındaki sunucudan sunucuya iletişimin güvenliğini sağlamaya yardımcı olmak için IPSec kullanabilirsiniz, siteler arasındaki diğer veri aktarımı için de kullanabilirsiniz. IPSec 'in uygulanması Configuration Manager bağımsızdır.  

PKI sertifikaları kullanılabilir olmadığında, otomatik olarak imzalanan sertifikalar oluşturur Configuration Manager. Configuration Manager içindeki bazı sertifikalar her zaman otomatik olarak imzalanır. Çoğu durumda Configuration Manager otomatik olarak imzalanan sertifikaları otomatik olarak yönetir ve ek işlem yapmanız gerekmez. Bir örnek, site sunucusu imzalama sertifikasıdır. Bu sertifika her zaman otomatik olarak imzalanır. İstemcilerin yönetim noktasından indirdikleri ilkelerin site sunucusundan gönderildiğinden ve kurcalanmadığından emin olur.  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a> Şifreleme: yeni nesil (CNG) sertifikaları  

Configuration Manager şifrelemeyi destekler: yeni nesil (CNG) sertifikaları. Configuration Manager istemcileri, CNG Anahtar depolama sağlayıcısında (KSP) özel anahtarla PKI istemci kimlik doğrulama sertifikasını kullanabilir. KSP desteğiyle Configuration Manager istemcileri, PKI istemci kimlik doğrulama sertifikaları için TPM KSP gibi donanım tabanlı özel anahtarı destekler. Daha fazla bilgi için bkz. [CNG sertifikalarına genel bakış](../network/cng-certificates-overview.md).


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a> Gelişmiş HTTP  

HTTPS iletişimini kullanmak tüm Configuration Manager iletişim yollarında önerilir, ancak PKI sertifikalarını yönetme yükü nedeniyle bazı müşteriler için zordur. Azure Active Directory (Azure AD) Tümleştirmesi 'nin tanıtımı, sertifika gereksinimlerinin tümünü değil, bazılarını azaltır. Sürüm 1806 ' den başlayarak, sitenin **GELIŞMIŞ http**kullanmasını sağlayabilirsiniz. Bu yapılandırma, otomatik olarak imzalanan sertifikaların ve Azure AD 'nin bir birleşimini kullanarak site sistemlerinde HTTPS 'yi destekler. PKI gerektirmez. Daha fazla bilgi için bkz. [GELIŞMIŞ http](../hierarchy/enhanced-http.md).  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a> CMG ve CDP sertifikaları

Bulut yönetimi ağ geçidi (CMG) ve bulut dağıtım noktası (CDP) aracılığıyla Internet 'teki istemcileri yönetmek için sertifikaların kullanılması gerekir. Sertifika sayısı ve türü, belirli senaryolarınıza bağlı olarak farklılık gösterir. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:
- [Bulut yönetimi ağ geçidi için sertifikalar](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [Bulut dağıtım noktası için sertifikalar](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a> Site sunucusu imzalama sertifikası (otomatik imzalı) için plan yapın  

İstemciler site sunucusu imzalama sertifikasının bir kopyasını Active Directory Domain Services 'den ve Client Push yüklemesinden güvenli bir şekilde alabilir. İstemcileri bu mekanizmalardan biri ile bu sertifikanın bir kopyasını alamazsanız, istemciyi yüklerken yükleyebilirsiniz. İstemcinin siteyle ilk iletişimi Internet tabanlı bir yönetim noktası ise bu işlem özellikle önemlidir. Bu sunucu güvenilmeyen bir ağa bağlı olduğundan saldırıya karşı daha savunmasız olur. Bu ek adım yapmazsanız, istemciler site sunucusu imzalama sertifikasının bir kopyasını yönetim noktasından otomatik olarak indirir.  

İstemciler, aşağıdaki senaryolarda site sunucusu sertifikasının bir kopyasını güvenli bir şekilde alamıyor:  

- İstemcisini Client Push kullanarak yüklememeniz ve:  

  - Configuration Manager için Active Directory şemasını genişletmemiş olabilirsiniz.  

  - İstemci sitesini Active Directory Domain Services için yayımlamadınız.  

  - İstemci, güvenilmeyen bir orman veya çalışma grubundan.  

- Internet tabanlı istemci yönetimini kullanıyorsunuz ve istemciyi Internet üzerinden yükleyeceksiniz.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>İstemcileri site sunucusu imzalama sertifikasının bir kopyasıyla yüklemek için  

1.  Birincil site sunucusunda site sunucusu imzalama sertifikasını bulun. Sertifika, Windows 'un **SMS** sertifika deposunda depolanır. Konu adı **site sunucusu** ve kolay adı, **site sunucusu imzalama sertifikası**olur.  

2.  Özel anahtar olmadan sertifikayı dışarı aktarın, dosyayı güvenli bir şekilde depolayın ve yalnızca güvenli bir kanaldan erişin.  

3.  Aşağıdaki client.msi özelliğini kullanarak istemciyi yükler: `SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> PKI sertifikası iptalini planlayın  

Configuration Manager ile PKI sertifikaları kullandığınızda, sertifika iptal listesinin (CRL) kullanımını planlayın. Cihazlar bağlanan bilgisayardaki sertifikayı doğrulamak için CRL 'YI kullanır. CRL, bir sertifika yetkilisi (CA) tarafından oluşturulan ve işaret eden bir dosyadır. CA 'nın verdiği ancak iptal edildiği sertifikaların listesini içerir. Bir sertifika yöneticisi sertifikaları iptal ettiğinizde, parmak izi CRL 'ye eklenir. Örneğin, verilen bir sertifikanın tehlikede olduğu bilinmektedir veya bu sertifikaya şüphe Duyulmuşsa.

> [!IMPORTANT]  
> CA 'nın konumu bir sertifika yetkilisi tarafından bir sertifikaya eklendiği için, Configuration Manager kullandığı herhangi bir PKI sertifikasını dağıtmadan önce CRL 'yi planladığınızdan emin olun.  

IIS her zaman istemci sertifikaları için CRL 'yi denetler ve Configuration Manager Bu yapılandırmayı değiştiremezsiniz. Varsayılan olarak, Configuration Manager istemcileri site sistemleri için her zaman CRL 'YI denetler. Bir site özelliği belirterek ve bir CCMSetup özelliği belirterek bu ayarı devre dışı bırakın.  

Sertifika iptal denetimini kullanan ancak CRL 'YI bulamamaları gereken bilgisayarlar, sertifika zincirindeki tüm sertifikalar iptal edildiğinde olduğu gibi davranır. Bu davranışın nedeni, sertifikaların sertifika iptal listesinde olup olmadığını doğrulayamazlar. Bu senaryoda, sertifika gerektirmeyen ve CRL denetimi içeren tüm bağlantılar başarısız olur. Http konumuna göz atarak CRL 'nizin erişilebilir olduğu doğrulanırken Configuration Manager istemcisinin yerel SISTEM olarak çalıştığını unutmayın. Bu nedenle, Kullanıcı bağlamı altında çalışan bir Web tarayıcısı ile CRL erişilebilirliğini test etmek başarılı olabilir, ancak iç Web filtreleme çözümü nedeniyle aynı CRL URL 'sine http bağlantısı kurmaya çalışırken bilgisayar hesabı engellenebilir. Bu durumda, herhangi bir Web filtreleme çözümlerinde CRL URL 'sinin beyaz listeye eklenmesi gerekebilir.

Her sertifika kullanıldığında CRL 'nin denetlenmesi, iptal edilen bir sertifikayı kullanmaya karşı daha fazla güvenlik sunar. İstemci üzerinde bir bağlantı gecikmesi ve ek işleme tanıtılsa da. Kuruluşunuz, internet üzerindeki istemciler veya güvenilmeyen bir ağ için bu ek güvenlik denetimini gerektirebilir.  

Configuration Manager istemcilerinin CRL 'YI denetlemesini gerekip gerekmediğine karar vermeden önce PKI yöneticilerinize başvurun. Ardından, aşağıdaki koşullardan her ikisi de doğru olduğunda bu seçeneği Configuration Manager etkin tutmayı göz önünde bulundurun:  

- PKI altyapınız bir CRL 'yi destekler ve bu, tüm Configuration Manager istemcilerinin bulabildiği yerde yayımlanır. Bu istemciler internet 'teki cihazları ve güvenilmeyen ormanlara dahil edebilir.  

- PKI sertifikası kullanmak üzere yapılandırılmış bir site sistemine yapılan her bağlantı için CRL 'YI denetleme gereksinimi aşağıdaki gereksinimden büyüktür:  
  - Daha hızlı bağlantılar  
  - İstemci üzerinde verimli işlem  
  - CRL bulunamıyorsa istemciler, sunuculara bağlanamayan risk  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> PKI güvenilir kök sertifikaları ve sertifika verenler listesini planlayın  

IIS site sistemleriniz HTTP üzerinden istemci kimlik doğrulaması için veya HTTPS üzerinden istemci kimlik doğrulaması ve şifreleme için PKI istemci sertifikaları kullanıyorsa, kök CA sertifikalarını site özelliği olarak içeri aktarmanız gerekebilir. İki senaryo şunlardır:  

- İşletim sistemlerini Configuration Manager kullanarak dağıtırsınız ve yönetim noktaları yalnızca HTTPS istemci bağlantılarını kabul eder.  

- Yönetim noktalarının güvendiği bir kök sertifikaya zincirsiz olmayan PKI istemci sertifikalarını kullanırsınız.  

  > [!NOTE]  
  > Yönetim noktaları için kullandığınız sunucu sertifikalarını veren aynı sertifika yetkilisi hiyerarşisinden istemci PKI sertifikalarını verdiğinizde, bu kök CA sertifikasını belirtmeniz gerekmez. Ancak, birden çok CA hiyerarşisi kullanıyorsanız ve bunların birbirlerine güvenip güvenmediğini bilmiyorsanız, istemcilerin CA hiyerarşisi için kök CA 'yı içeri aktarın.  

Configuration Manager için kök CA sertifikalarını içeri aktarmanız gerekiyorsa, bunları sertifika veren CA 'dan veya istemci bilgisayardan dışarı aktarın. Sertifikayı, aynı zamanda kök CA olan veren CA 'dan dışarı aktardıysanız, özel anahtarı dışarı aktardığınızdan emin olun. İzinsiz değişiklik yapılmasını engellemek için, dışarıya aktarılmış sertifika dosyasını güvenli bir konuma depolayın. Siteyi ayarlarken dosyaya erişmeniz gerekir. Dosyaya ağ üzerinden eriştiğinizde, iletişimin IPSec kullanarak değişikliklere karşı korunduğundan emin olun.  

İçeri aktardığınız herhangi bir kök CA sertifikası yenilendiğinde, yenilenen sertifikayı içeri aktarmanız gerekir.  

Bu içeri aktarılan kök sertifika YETKILISI sertifikaları ve her bir yönetim noktasının kök CA sertifikası Configuration Manager bilgisayarların aşağıdaki yollarla kullandığı sertifika verenler listesini oluşturur:  

- İstemciler yönetim noktalarına bağlandıklarında, yönetim noktası istemci sertifikasının sitenin sertifika verenler listesinde güvenilen bir kök sertifikaya zincirleme yaptığını doğrular. Aksi takdirde, sertifika reddedilir ve PKI bağlantısı başarısız olur.  

- İstemciler bir PKI sertifikası seçtiklerinde ve sertifika verenler listesine sahip olduğunda, sertifika verenler listesinde güvenilen bir kök sertifikaya zincirden bir sertifika seçer. Eşleşme yoksa, istemci bir PKI sertifikası seçmez. Daha fazla bilgi için bkz. [plan for PKI istemci sertifikası seçimi](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> PKI istemci sertifikası seçimini planlayın  

IIS site sistemleriniz HTTP üzerinden istemci kimlik doğrulaması için veya HTTPS üzerinden istemci kimlik doğrulaması ve şifreleme için PKI istemci sertifikaları kullanıyorsa, Windows istemcilerinin Configuration Manager için kullanılacak sertifikayı nasıl seçmesini planlayın.  

> [!NOTE]  
> Bazı cihazlar bir sertifika seçme yöntemini desteklemez. Bunun yerine, sertifika gereksinimlerini karşılayan ilk sertifikayı otomatik olarak seçer. Örneğin, Mac bilgisayarlar ve mobil cihazlardaki istemciler bir sertifika seçme yöntemini desteklemez.  

Çoğu durumda varsayılan yapılandırma ve davranış yeterlidir. Windows bilgisayarlarındaki Configuration Manager istemcisi bu ölçütleri kullanarak birden çok sertifikayı bu sırayla filtreler:  

1.  Sertifika verenler listesi: sertifika, yönetim noktası tarafından güvenilen bir kök CA 'ya zincirdir.  

2.  Sertifika, varsayılan **Kişisel**sertifika deposundadır.  

3.  Sertifika geçerlidir, iptal edilmemiştir ve süresi dolmamıştır. Geçerlilik denetimi, özel anahtarın erişilebilir olduğunu da doğrular.  

4.  Sertifikada istemci kimlik doğrulama özelliği bulunur.

5.  Sertifika konu adı, yerel bilgisayar adını bir alt dize olarak içerir.  

6.  Sertifika en uzun geçerlilik süresine sahiptir.  

Aşağıdaki mekanizmalardan yararlanarak istemcileri sertifika verenler listesini kullanacak şekilde yapılandırın:  

- Active Directory Domain Services için Configuration Manager site bilgileriyle yayımlayın.  

- İstemcileri Client Push kullanarak yükleme.  

- İstemciler, sitesine başarıyla atandıktan sonra yönetim noktasından indirir.  

- CCMCERTıSERS 'in CCMSetup client.msi özelliği olarak istemci yüklemesi sırasında belirtin.  

İlk yüklendiklerinde ve henüz siteye atanmadıysa, sertifika verenler listesine sahip olmayan istemciler bu denetimi atlayın. İstemciler sertifika verenler listesine sahip olduğunda ve sertifika verenler listesinde güvenilen bir kök sertifikaya zincirler bir PKI sertifikasına sahip olmadığında, sertifika seçimi başarısız olur. İstemciler diğer sertifika seçim ölçütlerine devam eder.  

Çoğu durumda Configuration Manager istemcisi benzersiz ve uygun bir PKI sertifikasını doğru şekilde tanımlar. Ancak, bu davranış durumda, istemci kimlik doğrulaması özelliğine dayalı olarak sertifikayı seçmek yerine iki alternatif seçim yöntemi ayarlayabilirsiniz:  

- İstemci sertifikası konu adı üzerinde kısmi dize eşleşmesi. Bu yöntem, büyük/küçük harfe duyarlı bir eşleşmedir. Konu alanındaki bir bilgisayarın tam etki alanı adını (FQDN) kullanıyor ve sertifika seçiminin, örneğin **contoso.com**gibi etki alanı sonekine dayanı olmasını istiyorsanız bu uygundur. Ancak bu seçim yöntemini, sertifikayı istemci sertifika deposundaki diğerlerinden ayıran, sertifika konu adındaki herhangi bir sıralı karakter dizesini belirlemek için kullanabilirsiniz.  

  > [!NOTE]
  > Konu alternatif adı (SAN) ile kısmi dize eşleşmesini bir site ayarı olarak kullanamazsınız. CCMSetup kullanarak SAN için kısmi dize eşleşmesi belirtebilseniz de, aşağıdaki senaryolarda site özellikleri ile üzerine yazılacaktır:  
  > 
  > - İstemciler Active Directory Domain Services yayımlanan site bilgilerini alır.  
  >   - İstemciler, istemci anında yükleme kullanılarak yüklendiğinde.  
  > 
  >   Yalnızca istemcileri el ile yüklediğinizde ve Active Directory Domain Services site bilgilerini almadıklarında SAN 'da kısmi dize eşleşmesi kullanın. Örneğin, bu koşullar yalnızca İnternet istemcileri için geçerlidir.  

- İstemci sertifikası konu adı öznitelik değerleri veya konu diğer adı (SAN) öznitelik değerleri ile eşleşme. Bu yöntem, büyük/küçük harfe duyarlı bir eşleşmedir. RFC 3280 ile uyumlu bir X500 ayırt edici adı veya eşdeğer nesne tanımlayıcıları (OID) kullanıyorsanız ve sertifika seçiminin öznitelik değerlerini temel alarak olmasını istiyorsanız bu uygundur. Sertifikayı benzersiz şekilde tanımlamak ve doğrulamak ve sertifikayı, sertifika deposundaki diğerlerinden ayırmak için, yalnızca size gerekli özellik ve değerlerini belirtebilirsiniz.  

Aşağıdaki tabloda, Configuration Manager istemci sertifikası seçim kriterleri için desteklenen öznitelik değerleri gösterilmektedir.  

|OID Özelliği|Ayırt edici ad özelliği|Öznitelik tanımı|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Etki alanı bileşeni|  
|1.2.840.113549.1.9.1|E veya E-posta|E-posta adresi|  
|2.5.4.3|CN|Ortak ad|  
|2.5.4.4|SN|Konu adı|  
|2.5.4.5|SERIALNUMBER|Seri numarası|  
|2.5.4.6|C|Ülke kodu|  
|2.5.4.7|L|Yerleşim yeri|  
|2.5.4.8|S veya ST|Eyalet veya bölge adı|  
|2.5.4.9|STREET|Açık adres|  
|2.5.4.10|O|Kuruluş adı|  
|2.5.4.11|OU|Kurum birimi|  
|2.5.4.12|T veya Title|Başlık|  
|2.5.4.42|G veya GN veya GivenName|Ad|  
|2.5.4.43|I veya Initials|Baş harfler|  
|2.5.29.17|(değer yok)|Konu Diğer Adı| 

  > [!NOTE]
  > Yukarıdaki diğer sertifika seçme yöntemlerinden birini yapılandırırsanız, sertifika konu adının yerel bilgisayar adını içermesi gerekmez.

Seçim kriterleri uygulandıktan sonra birden fazla uygun sertifika bulunuyorsa, en uzun geçerlilik süresine sahip sertifikayı seçmek için varsayılan yapılandırmayı geçersiz kılabilir ve bunun yerine hiçbir sertifika seçili olmadığını belirtebilirsiniz. Bu senaryoda, istemci bir PKI sertifikasıyla IIS site sistemleriyle iletişim kuramaz. İstemci, kendi atanan geri dönüş durum noktasına bir hata iletisi göndererek, sertifika Seçim kriterlerinizi değiştirebilmeniz veya iyileştirmek için sertifika seçim hatası hakkında sizi uyarır. İstemci davranışı ardından, başarısız bağlantının HTTPS veya HTTP üzerinden olmasına bağlıdır:  

- Başarısız bağlantı HTTPS üzerindense: istemci HTTP üzerinden bağlanmayı dener ve istemci otomatik olarak imzalanan sertifikasını kullanır.  

- Başarısız bağlantı HTTP üzerindense: istemci, otomatik olarak imzalanan istemci sertifikasını kullanarak HTTP üzerinden tekrar bağlanmayı dener.  

Benzersiz bir PKI istemci sertifikasını belirlemenize yardımcı olmak için, **bilgisayar** deposundaki **Kişisel** varsayılan dışında bir özel depo da belirtebilirsiniz. Ancak, bu depoyu Configuration Manager bağımsız olarak oluşturmanız gerekir. Bu özel depoya sertifika dağıtabilecek ve geçerlilik süresi dolmadan önce yenileyebilmelisiniz.  

Daha fazla bilgi için bkz. [ISTEMCI PKI sertifikaları için ayarları yapılandırma](configure-security.md#BKMK_ConfigureClientPKI).  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> PKI sertifikaları ve Internet tabanlı istemci yönetimi için bir geçiş stratejisi planlayın  

Configuration Manager ' deki esnek yapılandırma seçenekleri, istemci uç noktalarını güvenli hale getirmek için istemcileri ve siteyi PKI sertifikalarını kullanmak üzere giderek büyütmenizi sağlar. PKI sertifikaları daha iyi güvenlik sağlar ve internet istemcilerini yönetmenizi sağlar.  

Configuration Manager yapılandırma seçenekleri ve seçim sayısı nedeniyle, tüm istemciler HTTPS bağlantıları kullanacak şekilde bir siteyi geçişin tek yolu yoktur. Ancak, kılavuz olarak aşağıdaki adımları uygulayabilirsiniz:  

1. Configuration Manager sitesini yükleyip, site sistemleri HTTPS ve HTTP üzerinden istemci bağlantılarını kabul edecek şekilde yapılandırın.  

2. Site özelliklerindeki **Istemci bilgisayarı iletişimi** sekmesini, **site sistem ayarları** **http veya https**olacak şekilde yapılandırın ve **kullanılabilir olduğunda PKI istemci sertifikası (istemci kimlik doğrulama yeteneği) kullan**' ı seçin.  Daha fazla bilgi için bkz. [ISTEMCI PKI sertifikaları için ayarları yapılandırma](configure-security.md#BKMK_ConfigureClientPKI).  

    > [!Note]
    > Sürüm 1906 ' den başlayarak bu sekmeye **Iletişim güvenliği**denir.<!-- SCCMDocs#1645 -->  

3. İstemci sertifikaları için bir PKI sunumu deneyin. Örnek bir dağıtım için bkz. [Windows bilgisayarları için istemci sertifikasını dağıtma](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

4. İstemci anında yükleme yöntemini kullanarak istemcileri yükleyin. Daha fazla bilgi için bkz. [istemci gönderme kullanarak Configuration Manager istemcileri yükleme](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

5. Configuration Manager konsolundaki raporları ve bilgileri kullanarak istemci dağıtımı ve durumunu izleyin.  

6. **Varlıklar ve Uyum** çalışma alanında **Aygıtlar** düğümünde **İstemci Sertifikası** sütununu görüntüleyerek kaç istemcinin bir istemci PKI sertifikası kullandığını izleyin.  

    Ayrıca, Configuration Manager HTTPS hazırlık değerlendirme aracı 'nı (**cmHttpsReadiness.exe**) bilgisayarlara dağıtabilirsiniz. Ardından, Configuration Manager ile istemci PKI sertifikasını kaç bilgisayarın kullanabileceğinizi görüntülemek için raporları kullanın.  

   > [!NOTE]
   >  Configuration Manager istemcisini yüklediğinizde, klasöre **CMHttpsReadiness.exe** aracı yüklenir `%windir%\CCM` . Bu aracı çalıştırdığınızda aşağıdaki komut satırı seçenekleri kullanılabilir:  
   > 
   > - `/Store:<name>`: Bu seçenek **Ccmccertstore** client.msi özelliğiyle aynıdır  
   > - `/Issuers:<list>`: Bu seçenek **Ccmcertısers** client.msi özelliğiyle aynıdır    
   > - `/Criteria:<criteria>`: Bu seçenek **Ccmccertsel** client.msi özelliğiyle aynıdır    
   > - `/SelectFirstCert`: Bu seçenek **Ccmfirstcert** client.msi özelliğiyle aynıdır    
   > 
   >   Daha fazla bilgi için bkz. [istemci yükleme özellikleri hakkında](../../clients/deploy/about-client-installation-properties.md).  

7. Yeterli sayıda istemcinin HTTP üzerinden kimlik doğrulaması için istemci PKI sertifikalarını başarılı bir şekilde kullandığınızdan emin olduğunuzda, aşağıdaki adımları izleyin:  

   1.  Site için ek bir yönetim noktası çalıştıran bir üye sunucuya bir PKI Web sunucusu sertifikası dağıtın ve bu sertifikayı IIS 'de yapılandırın. Daha fazla bilgi için bkz. [IIS çalıştıran site sistemleri için Web sunucusu sertifikasını dağıtma](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

   2.  Bu sunucuya yönetim noktası rolünü yükleyin ve **HTTPS** için yönetim noktası özelliklerinde **İstemci bağlantıları**seçeneğini yapılandırın.  

8. İzleyin ve bir PKI sertifikası olan istemcilerin, HTTPS kullanarak yeni yönetim noktasını kullandığını doğrulayın. Doğrulamak için IIS günlük kaydı veya performans sayaçlarını kullanabilirsiniz.  

9. HTTPS istemci bağlantılarını kullanmak için diğer site sistem rollerini yeniden yapılandırın. İstemcileri Internet 'te yönetmek istiyorsanız, site sistemlerinde bir İnternet FQDN 'SI olduğundan emin olun. Bireysel yönetim noktalarını ve dağıtım noktalarını internetten istemci bağlantılarını kabul edecek şekilde yapılandırın.  

    > [!IMPORTANT]  
    > Site sistem rollerini Internet 'ten gelen bağlantıları kabul edecek şekilde ayarlamadan önce, internet tabanlı istemci yönetimi için planlama bilgilerini ve önkoşulları gözden geçirin. Daha fazla bilgi için bkz. [uç noktalar arasındaki iletişimler](../hierarchy/communications-between-endpoints.md).  

10. İstemciler ve IIS çalıştıran site sistemleri için PKI sertifikası dağıtımını genişletin. HTTPS istemci bağlantıları ve internet bağlantıları için gereken şekilde site sistem rollerini ayarlayın.  

11. En yüksek güvenlik için: tüm istemcilerin kimlik doğrulama ve şifreleme için bir istemci PKI sertifikası kullandığı konusunda emin olduğunuzda, site özelliklerini yalnızca HTTPS kullanmak üzere değiştirin.  

    Bu plan, ilk olarak yalnızca HTTP üzerinden kimlik doğrulaması için PKI sertifikaları ve HTTPS üzerinden kimlik doğrulaması ve şifreleme sağlar. Bu bir sertifikayı kademeli olarak tanıtmak için bu planı izlediğinizde, istemcilerin yönetilmeyen hale geldiği riski azaltabilirsiniz. Configuration Manager desteklediği en yüksek güvenlikten de yararlanabilirsiniz.  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Güvenilen kök anahtarı planlayın  

Configuration Manager güvenilir kök anahtarı, Configuration Manager istemcilerinin, site sistemlerinin kendi hiyerarşilerine ait olduğunu doğrulaması için bir mekanizma sağlar. Her site sunucusu, diğer sitelerle iletişim kurmak için bir site değişim anahtarı oluşturur. Hiyerarşideki üst düzey siteden site değişim anahtarına, güvenilir kök anahtar adı verilir.  

Configuration Manager içinde güvenilir kök anahtarın işlevi, ortak anahtar altyapısındaki bir kök sertifikaya benzer. Güvenilen kök anahtarın özel anahtarı tarafından imzalanan herhangi bir şeye hiyerarşide daha fazla güveniliyor. İstemciler, sitenin güvenilen kök anahtarının bir kopyasını **root\ccm\locationservices** WMI ad alanında depolar. 

Örneğin, site yönetim noktasına bir sertifika yayınlar ve bu, güvenilen kök anahtarın özel anahtarıyla imzalanır. Site, güvenilen kök anahtarının ortak anahtarını istemcilerle paylaşır. Sonra istemciler kendi hiyerarşilerindeki yönetim noktaları ve kendi hiyerarşisinde olmayan yönetim noktalarını birbirinden ayırt edebilir.   

İstemciler, iki mekanizma kullanarak güvenilir kök anahtarın genel kopyasını otomatik olarak alır:  

- Configuration Manager için Active Directory şemasını genişletir ve siteyi Active Directory Domain Services olarak yayımlayabilirsiniz. Daha sonra istemciler bu site bilgilerini bir genel katalog sunucusundan alır. Daha fazla bilgi için bkz. [site yayımlama için Active Directory hazırlama](../network/extend-the-active-directory-schema.md).  

- Client Push yükleme yöntemini kullanarak istemcileri yüklediğinizde. Daha fazla bilgi için bkz. [Client Push yüklemesi](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).  

İstemciler, bu mekanizmalardan birini kullanarak güvenilir kök anahtarı alamıyorsa, iletişim kurdukları ilk yönetim noktası tarafından sağlanmış olan güvenilen kök anahtara güvenirler. Bu senaryoda, bir istemci hatalı yönetim noktasından ilke alacak bir saldırganın yönetim noktasına yanlış yönlendirilebilir. Bu eylem, gelişmiş bir saldırgan gerektirir. Bu saldırı, istemci, geçerli bir yönetim noktasından güvenilir kök anahtarı almadan önce kısa bir süre ile sınırlıdır. Bir saldırganın istemcileri yanlış bir yönetim noktasına yönlendirmesine yönelik bu riski azaltmak için, istemcileri güvenilir kök anahtarı önceden sağlayın.  

Bir Configuration Manager istemcisi için güvenilir kök anahtarı önceden sağlamak ve doğrulamak için aşağıdaki yordamları kullanın:  

- [Bir dosya kullanarak güvenilir kök anahtarla bir istemciyi önceden sağlama](#bkmk_trk-provision-file)  

- [Bir dosya kullanmadan güvenilir kök anahtarla bir istemciyi önceden sağlama](#bkmk_trk-provision-nofile)  

- [Bir istemcide güvenilen kök anahtarı doğrulama](#bkmk_trk-verify)  

- [Güvenilen kök anahtarı kaldır veya Değiştir](#bkmk_trk-reset)  

  > [!NOTE]  
  > İstemciler Active Directory Domain Services veya Client Push 'tan güvenilen kök anahtarı alabilir, bunu önceden sağlamanız gerekmez. 
  > 
  > İstemciler yönetim noktalarına HTTPS iletişimi kullandıklarında, güvenilen kök anahtarı önceden sağlamanız gerekmez. Bunlar, PKI sertifikaları tarafından güven kurarlar.  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a> Bir dosya kullanarak güvenilir kök anahtarla bir istemciyi önceden sağlama  

1.  Site sunucusunda aşağıdaki dosyayı bir metin düzenleyicisinde açın: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  **SMSPublicRootKey =** girişini bulun. Anahtarı bu satırdan kopyalayın ve herhangi bir değişiklik yapmadan dosyayı kapatın.  

3.  Yeni bir metin dosyası oluşturun ve MobileClient. tcf dosyasından kopyaladığınız anahtar bilgilerini yapıştırın.  

4.  Dosyayı tüm bilgisayarların erişebileceği bir konuma kaydedin, ancak dosyanın üzerinde değişiklik yapılmasını güvenli hale getirebilirsiniz.  

5.  client.msi özellikleri kabul eden herhangi bir yükleme yöntemini kullanarak istemcisini yükler. Aşağıdaki özelliği belirtin: `SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > İstemci yüklemesi sırasında güvenilir kök anahtarı belirttiğinizde, site kodunu da belirtin. Aşağıdaki client.msi özelliğini kullanın: `SMSSITECODE=<site code>`   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a> Bir dosya kullanmadan güvenilir kök anahtarla bir istemciyi önceden sağlama  

1.  Site sunucusunda aşağıdaki dosyayı bir metin düzenleyicisinde açın: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  **SMSPublicRootKey =** girişini bulun. Anahtarı bu satırdan kopyalayın ve herhangi bir değişiklik yapmadan dosyayı kapatın.  

3.  client.msi özellikleri kabul eden herhangi bir yükleme yöntemini kullanarak istemcisini yükler. Aşağıdaki client.msi özelliğini belirtin: `SMSPublicRootKey=<key>` burada `<key>` , MobileClient. tcf dosyasından kopyaladığınız dizedir.  

    > [!IMPORTANT]  
    >  İstemci yüklemesi sırasında güvenilir kök anahtarı belirttiğinizde, site kodunu da belirtin. Aşağıdaki client.msi özelliğini kullanın: `SMSSITECODE=<site code>`   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a> Bir istemcide güvenilen kök anahtarı doğrulama  

1. Yönetici olarak bir Windows PowerShell konsolu açın.  

2. Şu komutu çalıştırın:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

Döndürülen dize, güvenilen kök anahtarıdır. Site sunucusundaki MobileClient. tcf dosyasındaki **SMSPublicRootKey** değeriyle eşleştiğinden emin olun.  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a> Güvenilen kök anahtarı kaldır veya Değiştir  

client.msi özelliğini kullanarak, güvenilen kök anahtarı bir istemciden kaldırın, **Resetkeyınformation = true**. 

Güvenilir kök anahtarı değiştirmek için, istemciyi yeni güvenilir kök anahtarla birlikte yeniden yükleyin. Örneğin, Client Push kullanın ya da **SMSPublicRootKey**client.msi özelliğini belirtin.  

Bu yükleme özellikleri hakkında daha fazla bilgi için bkz. [istemci yükleme parametreleri ve özellikleri hakkında](../../clients/deploy/about-client-installation-properties.md).



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> İmzalama ve şifrelemeyi planlayın  
 
Tüm istemci iletişimleri için PKI sertifikaları kullandığınızda, istemci veri iletişiminin güvenliğini sağlamaya yardımcı olmak için imzalama ve şifreleme planlaması yapmanız gerekmez. IIS çalıştıran site sistemlerini HTTP istemci bağlantılarına izin verecek şekilde ayarlarsanız, site için istemci iletişiminin güvenliğini sağlamaya nasıl yardımcı olacağına karar verin.  

İstemcilerin yönetim noktalarına gönderdikleri verilerin korunmasına yardımcı olmak için istemcilerin verileri imzalamasını zorunlu kılabilirsiniz. İmzalanmak üzere SHA-256 algoritmasına de ihtiyacınız olabilir. Bu yapılandırma daha güvenlidir, ancak tüm istemciler tarafından destek yoksa SHA-256 gerekmez. Birçok işletim sistemi bu algoritmayı yerel olarak destekler, ancak daha eski işletim sistemleri için bir güncelleştirme veya düzeltme gerekebilir. 

İmzalama, verilerin izinsiz korunmasına yardımcı olurken, şifreleme verilerin bilgilerin açığa çıkmasına karşı korunmasına yardımcı olur. İstemciler tarafından sitedeki yönetim noktalarına gönderilen envanter verileri ve durum iletileri için 3DES şifrelemeyi etkinleştirebilirsiniz. Bu seçeneği desteklemek üzere istemcilere herhangi bir güncelleştirme yüklemenize gerek yoktur. İstemciler ve yönetim noktaları şifreleme ve şifre çözme için ek CPU kullanımı gerektirir.  

İmzalama ve şifreleme ayarlarını yapılandırma hakkında daha fazla bilgi için bkz. [imzalama ve şifrelemeyi yapılandırma](configure-security.md#BKMK_ConfigureSigningEncryption).  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Rol tabanlı yönetimi planlayın  

Daha fazla bilgi için bkz. [rol tabanlı yönetimin temelleri](../../understand/fundamentals-of-role-based-administration.md).  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a> Azure Active Directory için plan yapın

Configuration Manager, site ve istemcilerin modern kimlik doğrulamasını kullanmasını sağlamak için Azure Active Directory (Azure AD) ile tümleşir. Sitenizi Azure AD ile ekleme aşağıdaki Configuration Manager senaryolarını destekler:

**İstemci**  

- [Bulut yönetimi ağ geçidi aracılığıyla Internet 'teki istemcileri yönetme](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [Bulut etki alanına katılmış cihazları yönetme](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Ortak yönetim](../../../comanage/overview.md)  

- [Kullanıcı tarafından kullanılabilen uygulamaları dağıtma](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)

- [Iş çevrimiçi uygulamaları için Microsoft Store](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- Altyapı gereksinimlerini azaltın. Örneğin, uygulama kataloğu yerine [yönetim noktasını kullanan yazılım merkezi](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)  

- [Microsoft 365 uygulamalarını kurumsal olarak yönetme](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Sunucu**  

- [Desktop Analytics](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm)  

- [Topluluk Merkezi](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Bulut dağıtım noktası](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [Kullanıcı keşfi](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Sitenizi Azure AD 'ye bağlama hakkında daha fazla bilgi için bkz. [Azure hizmetlerini yapılandırma](../../servers/deploy/configure/azure-services-wizard.md).


Azure AD hakkında daha fazla bilgi için bkz. [Azure Active Directory belgeleri](/azure/active-directory/).



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a> SMS sağlayıcısı kimlik doğrulamasını planlayın
<!--1357013--> 

Sürüm 1810 ' den başlayarak, yöneticilerin Configuration Manager sitelere erişmesi için en düşük kimlik doğrulama düzeyini belirtebilirsiniz. Bu özellik, yöneticilerin Windows 'da gerekli düzeyiyle oturum açmasını zorlar. SMS sağlayıcısına erişen tüm bileşenler için geçerlidir. Örneğin, Configuration Manager konsolu, SDK yöntemleri ve Windows PowerShell cmdlet 'leri. 

Bu yapılandırma, hiyerarşi genelinde bir ayardır. Bu ayarı değiştirmeden önce, tüm Configuration Manager yöneticilerinin Windows 'da gerekli kimlik doğrulama düzeyiyle oturum açmasını sağlayın. 

Aşağıdaki düzeyler mevcuttur:

- **Windows kimlik doğrulaması**: Active Directory etki alanı kimlik bilgileriyle kimlik doğrulaması gerektir.   

- **Sertifika kimlik doğrulaması**: GÜVENILEN bir PKI sertifika yetkilisi tarafından verilen geçerli bir sertifika ile kimlik doğrulaması gerektir.  

- **İş Için Windows Hello kimlik doğrulaması**: bir cihaza bağlı olan ve Biyometri veya PIN kullanan güçlü iki öğeli kimlik doğrulama ile kimlik doğrulaması gerektir.  

Daha fazla bilgi için bkz. [plan for SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). 



## <a name="see-also"></a>Ayrıca bkz.
- [Configuration Manager istemcileri için güvenlik ve Gizlilik](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Güvenliği yapılandırma](configure-security.md)  

- [Uç noktalar arasında iletişim](../hierarchy/communications-between-endpoints.md)  

- [Şifreleme denetimleri teknik başvurusu](cryptographic-controls-technical-reference.md)  

- [PKI sertifikası gereksinimleri](../network/pki-certificate-requirements.md)