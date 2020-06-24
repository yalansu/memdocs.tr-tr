---
title: CMG güvenliği ve gizliliği
titleSuffix: Configuration Manager
description: Bulut yönetimi ağ geçidiyle güvenlik ve gizlilik hakkındaki rehberlik ve öneriler hakkında bilgi edinin.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: 1dd64404905df1452e45beda8610932db237410d
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715297"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Bulut yönetimi ağ geçidi için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale Configuration Manager bulut yönetim ağ geçidi (CMG) için güvenlik ve gizlilik bilgilerini içerir. Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidini planlayın](plan-cloud-management-gateway.md).

## <a name="cmg-security-details"></a>CMG güvenlik ayrıntıları

CMG, CMG bağlantı noktalarından gelen bağlantıları kabul eder ve yönetir. Sertifikaları ve bağlantı kimliklerini kullanarak karşılıklı kimlik doğrulaması kullanır.

CMG aşağıdaki yöntemleri kullanarak istemci isteklerini kabul eder ve iletir:

- PKI tabanlı istemci kimlik doğrulama sertifikası veya Azure AD ile karşılıklı HTTPS kullanarak bağlantıların ön kimlik doğrulamasını yapın.

  - CMG sanal makine örneklerinde IIS, CMG 'ye yüklediğiniz Güvenilen Kök sertifikalara göre sertifika yolunu doğrular.

  - Sertifika iptali etkinleştirirseniz, sanal makine örneğindeki IIS de istemci sertifikası iptalini doğrular. Daha fazla bilgi için bkz. [sertifika iptal listesini yayımlama](#bkmk_crl).

- Sertifika güven listesi (CTL), istemci kimlik doğrulama sertifikasının kökünü denetler. Ayrıca, istemci için yönetim noktasıyla aynı doğrulamayı yapar. Daha fazla bilgi için bkz. [sitenin Sertifika güven listesindeki girdileri gözden geçirme](#bkmk_ctl).

- Herhangi bir CMG bağlantı noktasının isteği denetleyebilir olup olmadığını denetlemek için istemci isteklerini (URL 'Ler) doğrular ve filtreler.  

- Her yayımlama uç noktası için içerik uzunluğunu denetler.

- Aynı sitedeki CMG bağlantı noktalarının yükünü dengelemek için hepsini bir kez deneme davranışı kullanır.

CMG bağlantı noktası aşağıdaki yöntemleri kullanır:

- CMG 'nin tüm sanal makine örneklerine tutarlı bir HTTPS/TCP bağlantısı oluşturur. Bu bağlantıları her dakikada denetler ve korur.

- Sertifikaları kullanarak CMG ile karşılıklı kimlik doğrulama kullanır.

- İstemci isteklerini URL eşlemelerine göre iletir.

- Konsolunda hizmet sistem durumunu göstermek için bağlantı durumunu raporlar.

- Her beş dakikada bir uç nokta başına trafiği rapor edin.

### <a name="configuration-manager-client-facing-roles"></a>Configuration Manager istemciye yönelik roller

Yönetim noktası ve yazılım güncelleştirme noktası, istemci isteklerine hizmet vermek için IIS 'de ana bilgisayar uç noktaları. CMG tüm iç uç noktaları kullanıma sunmuyor. CMG 'de yayınlanan her uç noktanın bir URL eşlemesi vardır.

- Dış URL, istemcinin CMG ile iletişim kurmak için kullandığı bir URL 'dir.

- İç URL, istekleri iç sunucuya iletmek için kullanılan CMG bağlantı noktasıdır.

#### <a name="url-mapping-example"></a>URL eşleme örneği

Bir yönetim noktasında CMG trafiğini etkinleştirdiğinizde Configuration Manager her yönetim noktası sunucusu için bir iç URL eşlemeleri kümesi oluşturur. Örneğin: ccm_system, ccm_incoming ve sms_mp. Yönetim noktası ccm_system uç noktası için dış URL şöyle görünebilir:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
URL her yönetim noktası için benzersizdir. Configuration Manager istemcisi daha sonra CMG etkin yönetim noktası adını İnternet Yönetim noktası listesine koyar. Bu ad şöyle görünür:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
Site yayımlanan tüm dış URL 'Leri otomatik olarak CMG 'ye yükler. Bu davranış, CMG 'nin URL Filtresi yapmasına izin verir. Tüm URL eşlemeleri CMG bağlantı noktasına çoğaltılır. Daha sonra, istemci isteğinden dış URL 'ye göre iletişimi iç sunucularla iletir.

## <a name="security-guidance-for-cmg"></a>CMG için Güvenlik Kılavuzu

<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Sertifika iptal listesini yayımlama

Internet tabanlı istemcilerin erişmesi için PKI 'nın sertifika iptal listesini (CRL) yayımlayın. PKI kullanarak bir CMG dağıttığınızda, Ayarlar sekmesinde **istemci sertifikası Iptalini doğrulamak** için hizmeti yapılandırın. Bu ayar, hizmeti yayınlanmış bir sertifika iptal listesi (CRL) kullanacak şekilde yapılandırır. Daha fazla bilgi için bkz. [plan for PKI sertifikası iptali](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Bu CMG seçeneği, istemci kimlik doğrulama sertifikasını doğrular.

- İstemci Azure AD kimlik doğrulamasını kullanıyorsa, CRL bu şekilde değildir.

- PKI kullanıyorsanız ve CRL 'YI dışarıdan yayımladığınızda bu seçeneği etkinleştirin (önerilir).

- PKI kullanıyorsanız, CRL 'yi yayımlamayın, ardından bu seçeneği devre dışı bırakın.

- Bu seçeneği yanlış yapılandırırsanız, istemcilerden CMG 'ye ek trafiğe neden olabilir. Bu ek trafik Azure çıkış verilerini artırabilir ve bu da Azure maliyetlerinizi artırabilir.<!-- SCCMDocs#1434 -->

<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Sitenin Sertifika güven listesindeki girdileri gözden geçirme

<!--503739-->
Her Configuration Manager sitesi, güvenilen kök sertifika yetkililerinin, sertifika güven listesinin (CTL) bir listesini içerir. **Yönetim** çalışma alanına gidip **Site yapılandırması**' nı genişleterek ve **siteler**' i seçerek listeyi görüntüleyin ve değiştirin. Bir site seçin ve ardından şeritte **Özellikler** ' i seçin. **Iletişim güvenliği** sekmesine geçin ve ardından güvenilen kök sertifika yetkilileri altında **Ayarla** ' yı seçin.

> [!Note]
> Sürüm 1902 ve önceki sürümlerde bu sekmeye **Istemci bilgisayar iletişimi**adı verilir.<!-- SCCMDocs#1645 -->

PKI istemci kimlik doğrulamasını kullanan bir CMG ile bir site için daha kısıtlayıcı bir CTL kullanın. Aksi takdirde, yönetim noktasında zaten mevcut olan herhangi bir güvenilir kök tarafından verilen istemci kimlik doğrulama sertifikaları olan istemciler, istemci kaydı için otomatik olarak kabul edilir.

Bu alt küme, yöneticilere güvenlik üzerinde daha fazla denetim sağlar. CTL, sunucuyu yalnızca CTL 'deki sertifika yetkililerinden verilen istemci sertifikalarını kabul edecek şekilde kısıtlar. Örneğin, Windows, VeriSign ve Thawte gibi bir dizi iyi bilinen üçüncü taraf sertifika yetkilisi (CA) sertifikası ile birlikte gelir. Varsayılan olarak, IIS çalıştıran bilgisayar, bu iyi bilinen CA 'Lara zincirlenen sertifikalara güvenir. IIS 'yi bir CTL ile yapılandırmadan, bu CA 'lardan verilmiş bir istemci sertifikasına sahip herhangi bir bilgisayar geçerli bir Configuration Manager istemcisi olarak kabul edilir. IIS 'yi bu CA 'Ları içermeyen bir CTL ile yapılandırırsanız, sertifika bu CA 'Lara zincirleme olursa istemci bağlantıları reddedilir.

### <a name="enforce-tls-12"></a><a name="bkmk_tls"></a>TLS 1,2 'yi zorla

<!-- SCCMDocs-pr#4021 -->

Sürüm 1906 ' den başlayarak, **TLS 1,2**' yi zorlamak için CMG ayarını kullanın. Yalnızca Azure bulut hizmeti VM 'si için geçerlidir. Şirket içi Configuration Manager site sunucuları veya istemcileri için uygulanmaz. TLS 1,2 hakkında daha fazla bilgi için bkz. [tls 1,2 'yi etkinleştirme](../../../plan-design/security/enable-tls-1-2.md).

### <a name="use-token-based-authentication"></a>Belirteç tabanlı kimlik doğrulaması kullan

Sürüm 2002 ' den başlayarak,<!--5686290--> Configuration Manager, genellikle dahili ağa bağlanmayan, Azure AD 'ye katılmadan ve PKI tarafından verilen bir sertifika yüklemek için bir yönteme sahip olmayan Internet tabanlı cihazlara yönelik desteğini uzatır. Site, iç ağa kaydolma cihazları için belirteçleri otomatik olarak yayımlar. Internet tabanlı cihazlar için toplu kayıt belirteci oluşturabilirsiniz. Daha fazla bilgi için bkz. [CMG Için belirteç tabanlı kimlik doğrulaması](../../deploy/deploy-clients-cmg-token.md).<!-- SCCMDocs#2331 -->

## <a name="next-steps"></a>Sonraki adımlar

- [Bulut yönetimi ağ geçidi planlama](plan-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidini kurma](setup-cloud-management-gateway.md)
- [Bulut yönetimi ağ geçidi hakkında sık sorulan sorular](cloud-management-gateway-faq.md)
- [Bulut yönetimi ağ geçidine yönelik sertifikalar](certificates-for-cloud-management-gateway.md)
