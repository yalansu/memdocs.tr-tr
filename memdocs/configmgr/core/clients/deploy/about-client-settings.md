---
title: İstemci ayarları
titleSuffix: Configuration Manager
description: İstemci davranışlarını denetlemek için varsayılan ve özel ayarlar hakkında bilgi edinin
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1435c1ab6be8c80178566ae9d354084fddebb22a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771348"
---
# <a name="about-client-settings-in-configuration-manager"></a>Configuration Manager istemci ayarları hakkında

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager konsolundaki tüm istemci ayarlarını **Yönetim** çalışma alanındaki **istemci ayarları** düğümünden yönetin. Configuration Manager bir varsayılan ayarlar kümesiyle birlikte gelir. Varsayılan istemci ayarlarını değiştirdiğinizde, bu ayarlar hiyerarşideki tüm istemcilere uygulanır. Ayrıca, koleksiyonlara atadığınızda varsayılan istemci ayarlarını geçersiz kılan özel istemci ayarlarını da yapılandırabilirsiniz. Daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](configure-client-settings.md).

Aşağıdaki bölümlerde, ayarları ve seçenekleri daha ayrıntılı olarak açıklanır.  


## <a name="background-intelligent-transfer-service-bits"></a>Arka Plan Akıllı Aktarım Hizmeti (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>BITS arka plan aktarımları için maksimum ağ bant genişliğini sınırlayın

Bu seçenek **Evet**olduğunda, istemciler BITS bant genişliği azaltmayı kullanır. Bu gruptaki diğer ayarları yapılandırmak için bu ayarı etkinleştirmeniz gerekir.

### <a name="throttling-window-start-time"></a>Daraltma penceresi başlangıç zamanı

BITS daraltma penceresi için yerel başlangıç saatini belirtin.  

### <a name="throttling-window-end-time"></a>Daraltma penceresi bitiş zamanı

BITS daraltma penceresi için yerel bitiş saatini belirtin. Bitiş saati **daraltma penceresi başlangıç zamanına**eşitse, BITS daraltma her zaman etkindir.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Daraltma penceresinde en çok aktarım hızı (Kbps)

İstemcilerin pencere sırasında kullanabileceği en yüksek aktarım hızını belirtin.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Daraltma penceresi dışında BITS indirmelerine izin ver

İstemcilerin belirtilen pencerenin dışında ayrı BITS ayarları kullanmasına izin ver.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Daraltma penceresi dışındaki en fazla aktarım hızı (Kbps)

İstemcilerin BITS daraltma penceresi dışında kullanabileceği en yüksek aktarım hızını belirtin.  



## <a name="client-cache-settings"></a>İstemci önbellek ayarları

### <a name="configure-branchcache"></a>BranchCache yapılandırma

[Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
)için istemci bilgisayarı ayarlayın. İstemcide BranchCache önbelleğe almaya izin vermek için **BranchCache** **'i Evet**olarak ayarlayın.

- **BranchCache 'ı etkinleştir**: Istemci bilgisayarlarda BranchCache 'i etkinleştirir.

- **Maksimum BranchCache önbellek boyutu (disk yüzdesi)**: BranchCache 'in kullanmasına izin veren diskin yüzdesi.

> [!TIP]
> **BranchCache yapılandırma** 'yı **hayır**olarak ayarlarsanız Configuration Manager BranchCache ayarlarını yapılandırmaz.
>
> BranchCache 'i devre dışı bırakmak için, **BranchCache yapılandırma** 'yı **Evet**olarak ayarlayın ve **BranchCache** 'i **Hayır**olarak ayarlayın.<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>İstemci önbellek boyutunu Yapılandır

Windows bilgisayarlarda Configuration Manager istemci önbelleği, uygulamaları ve programları yüklemek için kullanılan geçici dosyaları depolar. Bu seçenek **Hayır**olarak ayarlanırsa, varsayılan boyut 5.120 MB 'tır.

**Evet**' i seçerseniz şunu belirtin:

- **En büyük önbellek boyutu (MB)**
- **En yüksek önbellek boyutu (disk yüzdesi)**: istemci önbellek boyutu MEGABAYT (MB) cinsinden en büyük boyuta veya diskin yüzdesine (hangisi daha küçükse) kadar genişler.

### <a name="enable-as-peer-cache-source"></a>Eş önbellek kaynağı olarak etkinleştir

> [!Note]  
> Sürüm 1902 ve önceki sürümlerde, bu ayar, **tam işletim sisteminde içeriğin paylaşılması için Configuration Manager Istemcisinin etkinleştirilmesi**olarak adlandırılmıştır. Ayarın davranışı değişmedi.

Configuration Manager istemcileri için [Eş Önbelleği](../../plan-design/hierarchy/client-peer-cache.md) etkinleştirilir. **Evet**' i seçin ve ardından istemcinin eş bilgisayarla iletişim kurduğu bağlantı noktasını belirtin.

- **İlk ağ yayını Için bağlantı noktası** (varsayılan UDP 8004): Configuration Manager Bu bağlantı noktasını Windows PE 'de veya tam Windows işletim sisteminde kullanır. Windows PE 'deki görev dizisi altyapısı, görev dizisini başlamadan önce içerik konumlarını almak için yayını gönderir.<!--SCCMDocs issue 910-->

- **Eşten içerik indirmesi Için bağlantı noktası** (varsayılan TCP 8003): Configuration Manager, Windows güvenlik duvarı kurallarını bu trafiğe izin verecek şekilde otomatik olarak yapılandırır. Farklı bir güvenlik duvarı kullanıyorsanız, bu trafiğe izin vermek için kuralları el ile yapılandırmanız gerekir.  

    Daha fazla bilgi için bkz. [bağlantılar için kullanılan bağlantı noktaları](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>Önbelleğe alınan içeriğin kaldırılabilmesi için gereken en kısa süre (dakika)

<!--4485509-->
Sürüm 1906 ' den başlayarak, önbelleğe alınmış içeriği tutmak için Configuration Manager istemcisinin en düşük süresini belirtin. Bu istemci ayarı, daha fazla alana ihtiyaç duyulmanız durumunda Configuration Manager aracısının önbellekten içerik kaldırabilmesi için bekleyeceği en az süreyi tanımlar.

Bu değer varsayılan olarak 1.440 dakikadır (24 saat).
Bu ayar için en yüksek değer 10.080 dakikadır (1 hafta).

Bu ayar, farklı türde cihazlarda istemci önbelleği üzerinde daha fazla denetim sağlar. Küçük sabit sürücüleri olan istemcilerdeki değeri azaltabilir ve başka bir dağıtım çalıştırılmadan önce var olan içerikleri tutmanız gerekmez.


## <a name="client-policy"></a>İstemci ilkesi  

### <a name="client-policy-polling-interval-minutes"></a>İstemci ilkesi yoklama zaman aralığı (dakika)

Aşağıdaki Configuration Manager istemcilerinin istemci ilkesini ne sıklıkta indirmelerini belirtir:

- Windows bilgisayarlar (örneğin masaüstü bilgisayarlar, sunucular, dizüstü bilgisayarlar)  
- Configuration Manager olan mobil cihazlar  
- Mac bilgisayarlar  
- Linux veya UNIX ile çalışan bilgisayarlar  

Bu değer varsayılan olarak 60 dakikadır. Bu değerin azaltılması, istemcilerin siteyi daha sık yoklamasına neden olur. Çok sayıda istemci sayesinde, bu davranışın site performansı üzerinde olumsuz bir etkisi olabilir. [Boyut ve ölçek Kılavuzu](../../plan-design/configs/size-and-scale-numbers.md) , varsayılan değere göre belirlenir. Bu değerin artırılması, istemcilerin siteyi daha az sıklıkta yoklamasına neden olur. Yeni dağıtımlar da dahil olmak üzere istemci ilkelerine yapılan tüm değişiklikler istemcilerin indirmesi ve işlemesi için daha uzun sürer.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>İstemcilerde kullanıcı ilkesini etkinleştir

Bu seçeneği **Evet**olarak belirlediğinizde ve [Kullanıcı keşfi](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)kullandığınızda istemciler, oturum açmış kullanıcıya hedeflenen uygulamaları ve programları alırlar.  

Bu ayar **Hayır**ise, kullanıcılar kullanıcılara dağıttığınız gerekli uygulamaları almaz. Kullanıcılar, kullanıcı ilkelerinde başka yönetim görevleri de almaz.  

Bu ayar kullanıcılar için, bilgisayarları intranet veya internet üzerinde olduğunda geçerlidir. Ayrıca Internet 'te kullanıcı ilkelerini etkinleştirmek istiyorsanız, bu, **Evet** olmalıdır.  

> [!Note]  
> Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Yeni Uygulama Kataloğu rolleri yükleyemezsiniz.
>
> Uygulama kataloğunu kullanmaya devam ediyorsanız, site sunucusundan kullanıcılar için kullanılabilir yazılım listesini alır. Bu nedenle, kullanıcıların uygulama kataloğu 'ndan uygulamaları görüp istemesi için bu ayarın **Evet** olması gerekmez. Bu ayar **Hayır**ise, kullanıcılar uygulama kataloğunda göreceği uygulamaları yükleyemez.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>İnternet istemcilerinden gelen Kullanıcı ilkesi isteklerini etkinleştir

Kullanıcıların Internet tabanlı bilgisayarlarda kullanıcı ilkesini alabilmesi için bu seçeneği **Evet** olarak ayarlayın. Aşağıdaki gereksinimler de geçerlidir:  

- İstemci ve site, [İnternet tabanlı istemci yönetimi](../manage/plan-internet-based-client-management.md) veya bir [bulut yönetimi ağ geçidi](../manage/cmg/plan-cloud-management-gateway.md)için yapılandırılır.  

- **İstemcilerde Kullanıcı Ilkesini etkinleştir** ayarı **Evet**'tir.  

- Internet tabanlı yönetim noktası, Windows kimlik doğrulaması (Kerberos veya NTLM) kullanarak kullanıcının kimliğini başarılı bir şekilde doğrular. Daha fazla bilgi için bkz. [İnternet 'ten istemci iletişimleri Için değerlendirmeler](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

- Bulut yönetimi ağ geçidi, Azure Active Directory kullanarak kullanıcının kimliğini başarılı bir şekilde doğrular. Daha fazla bilgi için bkz. [Azure AD 'ye katılmış cihazlarda Kullanıcı tarafından kullanılabilen uygulamaları dağıtma](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).  

Bu seçeneği **Hayır**olarak ayarlarsanız veya önceki gereksinimlerin hiçbiri karşılanmazsa, internet üzerindeki bir bilgisayar yalnızca bilgisayar ilkeleri alır. Bu senaryoda, kullanıcılar hala Internet tabanlı bir uygulama kataloğu 'ndan uygulamaları görebilir, isteyebilir ve yükleyebilir. Bu ayar **Hayır**ise, ancak **Istemcilerde kullanıcı ilkesini etkinleştir** **Evet**ise, kullanıcılar bilgisayar intranete bağlanana kadar kullanıcı ilkeleri almaz.  

> [!NOTE]  
> Internet tabanlı istemci yönetimi için, kullanıcılardan gelen uygulama onay istekleri kullanıcı ilkeleri veya Kullanıcı kimlik doğrulaması gerektirmez. Bulut yönetimi ağ geçidi, uygulama onay isteklerini desteklemez.  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>Birden çok Kullanıcı oturumu için kullanıcı ilkesini etkinleştir

<!--4737447-->

*Sürüm 1910 için geçerlidir*

Bu ayar varsayılan olarak devre dışıdır. Kullanıcı ilkelerini etkinleştirseniz bile, sürüm 1906 ' den başlayarak istemci, Çoklu eşzamanlı etkin kullanıcı oturumlarına izin veren herhangi bir cihazda varsayılan olarak devre dışı bırakır. Örneğin, [Windows sanal masaüstü](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)'nde Terminal sunucuları veya Windows 10 Enterprise çoklu oturum.

İstemci, yeni bir yükleme sırasında bu cihaz türünü algıladığında yalnızca kullanıcı ilkesini devre dışı bırakır. Sürüm 1906 veya sonraki bir sürüme güncelleştirmeniz gereken bu türden mevcut bir istemci için önceki davranış devam ettirir. Mevcut bir cihazda, cihazın birden çok kullanıcı oturumuna izin verdiğini algıladığında bile Kullanıcı ilkesi ayarını yapılandırır.

Bu senaryoda Kullanıcı ilkesine ihtiyacınız varsa ve olası performans etkisini kabul ediyorsanız, bu istemci ayarını etkinleştirin.


## <a name="cloud-services"></a>Bulut hizmetleri

### <a name="allow-access-to-cloud-distribution-point"></a>Bulut dağıtım noktasına erişime izin ver

İstemcilerin bir bulut dağıtım noktasından içerik alması için bu seçeneği **Evet** olarak ayarlayın. Bu ayar, cihazın İnternet tabanlı olmasını gerektirmez.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Azure Active Directory ile yeni Windows 10 etki alanına katılmış cihazları otomatik olarak kaydet

Karma birleştirmeyi desteklemek için Azure Active Directory yapılandırdığınızda, Configuration Manager Bu işlevsellik için Windows 10 cihazlarını yapılandırır. Daha fazla bilgi için bkz. [karma Azure Active Directory katılmış cihazları yapılandırma](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>İstemcilerin bulut yönetimi ağ geçidi kullanmasını sağlama

Varsayılan olarak, tüm Internet dolaşımı istemcileri kullanılabilir [bulut yönetimi ağ geçidini](../manage/cmg/plan-cloud-management-gateway.md)kullanır. Bu **ayarın, bir** pilot proje veya maliyet tasarrufu gibi, hizmetin kapsam kullanımına yönelik olarak ne zaman yapılandırılacağını bir örnektir.



## <a name="compliance-settings"></a>Uyumluluk ayarları  

### <a name="enable-compliance-evaluation-on-clients"></a>İstemcilerde uyumluluk değerlendirmesini etkinleştirme

Bu gruptaki diğer ayarları yapılandırmak için bu seçeneği **Evet** olarak ayarlayın.

### <a name="schedule-compliance-evaluation"></a>Uyum değerlendirmesi zamanlama

Yapılandırma temeli dağıtımları için Varsayılan zamanlamayı oluşturmak için **zamanla** ' yı seçin. Bu değer, **yapılandırma temeli dağıt** iletişim kutusundaki her bir taban çizgisi için yapılandırılabilir.  

### <a name="enable-user-data-and-profiles"></a>Kullanıcı Verilerini ve Profillerini Etkinleştir

[Kullanıcı verileri ve profilleri](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) yapılandırma öğelerini dağıtmak istiyorsanız **Evet** ' i seçin.



## <a name="computer-agent"></a>Bilgisayar Aracısı  

### <a name="user-notifications-for-required-deployments"></a>Gerekli dağıtımlar için Kullanıcı bildirimleri

Aşağıdaki üç ayar hakkında daha fazla bilgi için bkz. [Gerekli dağıtımlar Için Kullanıcı bildirimleri](../../../apps/deploy-use/deploy-applications.md#bkmk_notify):

- **Dağıtım son tarihi, 24 saatten fazla, kullanıcıyı şu aralıklarla uyar (saat)**
- **Dağıtım son tarihi, 24 saatten az, kullanıcıyı şu aralıklarla uyar (saat)**
- **Dağıtım son tarihi 1 saatten az, kullanıcıyı şu aralıklarla uyar (dakika)**

### <a name="default-application-catalog-website-point"></a>Varsayılan Uygulama Kataloğu web sitesi noktası

> [!Important]  
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Configuration Manager, bu ayarı kullanıcıları Yazılım Merkezi 'nden Uygulama Kataloğu 'na bağlamak için kullanır. Uygulama Kataloğu web sitesi noktasını barındıran bir sunucu belirtmek için **Web sitesini ayarla** ' yı seçin. NetBIOS adını veya FQDN 'sini girin, otomatik algılamayı belirtin veya özelleştirilmiş dağıtımlar için bir URL belirtin. Çoğu durumda, otomatik algılama en iyi seçimdir.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Varsayılan Uygulama Kataloğu web sitesini Internet Explorer güvenilen siteler bölgesine ekleme

> [!Important]  
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  
>
> Daha fazla bilgi için aşağıdaki makalelere bakın:
>
> - [Yazılım merkezini yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Kaldırılan ve kullanım dışı bırakılan özellikler](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Bu seçenek **Evet**ise, istemci otomatik olarak geçerli varsayılan uygulama Kataloğu web sitesi URL 'Sini Internet Explorer güvenilen siteler bölgesine ekler.  

Bu ayar, korumalı mod için Internet Explorer ayarının etkin olmamasını sağlar. Korumalı mod etkinleştirilirse, Configuration Manager istemci uygulama kataloğu 'ndan uygulamaları yükleyemeyebilir. Varsayılan olarak, güvenilen siteler bölgesi, uygulama kataloğu için Windows kimlik doğrulaması gerektiren Kullanıcı oturum açma 'yı da destekler.  

Bu seçeneği **Hayır**olarak bırakırsanız Configuration Manager istemcileri Uygulama Kataloğu 'ndan uygulamaları yükleyemeyebilir. Alternatif bir yöntem, istemcilerin kullandığı uygulama kataloğu URL 'SI için başka bir bölgedeki bu Internet Explorer ayarlarını yapılandırmaktır.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Silverlight uygulamalarının yükseltilmiş güven modunda çalışmasına izin ver

> [!Important]  
> İstemci Silverlight 'ı otomatik olarak yüklemez.
>
> Sürüm 1806 ' den başlayarak, Uygulama Kataloğu web sitesi noktası için **Silverlight Kullanıcı deneyimi** artık desteklenmemektedir. Kullanıcıların yeni yazılım merkezini kullanması gerekir. Daha fazla bilgi için bkz. [Software Center 'ı yapılandırma](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).  

Kullanıcıların uygulama kataloğunu kullanabilmesi için bu ayar **Evet** olmalıdır.  

Bu ayarı değiştirirseniz, kullanıcılar tarayıcılarına bir dahaki sefer yüklendiğinde ya da o anda açılan tarayıcı penceresini yenileirken geçerli olur.  

Bu ayar hakkında daha fazla bilgi için bkz. [Microsoft Silverlight 5 sertifikaları ve uygulama kataloğu için gerekli yükseltilmiş güven modu](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Yazılım Merkezi'nde görünen organizasyon adı

Kullanıcıların Yazılım Merkezi'nde gördüğü adı yazın. Bu markalama bilgileri, kullanıcıların bu uygulamayı güvenilir bir kaynak olarak belirlemesine yardımcı olur. Bu ayarın önceliği hakkında daha fazla bilgi için bkz. [marka yazılım merkezi](../../../apps/plan-design/plan-for-software-center.md#branding-software-center).  

### <a name="use-new-software-center"></a>Yeni Yazılım Merkezini kullanma

Varsayılan ayar **Evet**' tir.

Bu seçeneği **Evet**olarak belirlediğinizde, tüm Istemci bilgisayarlar yazılım merkezini kullanır. Yazılım Merkezi, kullanıcılara veya cihazlara dağıttığınız yazılım, yazılım güncelleştirmeleri ve görev dizilerini gösterir.

### <a name="enable-communication-with-health-attestation-service"></a>Durum kanıtlama hizmeti ile iletişimi etkinleştir

Windows 10 cihazlarının [sistem durumu kanıtlama](../../servers/manage/health-attestation.md)kullanmasını sağlamak için bu seçeneği **Evet** olarak ayarlayın. Bu ayarı etkinleştirdiğinizde, yapılandırma için aşağıdaki ayar de kullanılabilir.

### <a name="use-on-premises-health-attestation-service"></a>Şirket içi sistem durumu kanıtlama hizmetini kullan

Cihazların şirket içi hizmeti kullanabilmesi için bu seçeneği **Evet** olarak ayarlayın. Cihazların Microsoft bulut tabanlı hizmeti kullanabilmesi için **Hayır** olarak ayarlayın.  

### <a name="install-permissions"></a>İzinleri yükle

Kullanıcıların yazılımları, yazılım güncelleştirmelerini ve görev dizilerini nasıl yükleyebilirim yapılandırın:  

- **Tüm kullanıcılar**: Konuk dışında herhangi bir izne sahip kullanıcılar.  

- **Yalnızca Yöneticiler**: kullanıcılar yerel Yöneticiler grubunun bir üyesi olmalıdır.  

- **Yalnızca Yöneticiler ve birincil kullanıcılar**: kullanıcılar yerel Yöneticiler grubunun bir üyesi veya bilgisayarın birincil kullanıcısı olmalıdır.  

- **Kullanıcı yok**: bir istemci bilgisayarda oturum açmış hiçbir Kullanıcı yazılım, yazılım güncelleştirmeleri ve görev dizilerini yükleyebilir. Bilgisayar için gerekli dağıtımlar her zaman son tarihte yüklenir. Kullanıcılar yazılım merkezi 'nden yazılım yükleyemez.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Yeniden başlatma sırasında BitLocker PIN girişini askıya al

Bilgisayarlar BitLocker PIN girişi gerektiriyorsa, bu seçenek bir yazılım yüklemesinden sonra bilgisayar yeniden başlatıldığında PIN girme gereksinimini atlar.  

- **Her zaman**: Configuration Manager, bir yeniden başlatma gerektiren yazılım yükledikten ve bilgisayarın yeniden başlatılmasını başlatduktan sonra, BitLocker 'ı geçici olarak askıya alır. Bu ayar yalnızca Configuration Manager tarafından başlatılan bir bilgisayar yeniden başlatması için geçerlidir. Bu ayar, kullanıcı bilgisayarı yeniden başlattığında BitLocker PIN 'ini girme gereksinimini askıya almaz. BitLocker PIN girişi gereksinimi Windows başlangıcından sonra devam eder.

- **Hiçbir**şekilde: Configuration Manager, yeniden başlatma gerektiren yazılımları yükledikten sonra BitLocker 'ı askıya almaz. Bu senaryoda, Kullanıcı standart başlangıç işlemini tamamlayıp Windows 'u yüklemek üzere PIN girene kadar yazılım yüklemesi tamamlanamaz.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>Ek yazılım, uygulamaların dağıtımını ve yazılım güncelleştirmelerini yönetir

Bu seçeneği yalnızca aşağıdaki koşullardan biri geçerliyse etkinleştirin:  

- Bu ayarın etkinleştirilmesini gerektiren bir satıcı çözümü kullanıyorsanız.  

- İstemci aracı bildirimlerini ve uygulamaların ve yazılım güncelleştirmelerinin yüklenmesini yönetmek için Configuration Manager yazılım geliştirme seti 'ni (SDK) kullanırsınız.  

> [!WARNING]  
> - Bu koşulların hiçbiri geçerli olmadığında bu seçeneği belirlerseniz, istemci yazılım güncelleştirmelerini ve gerekli uygulamaları yüklemez. Bu ayar, kullanıcıların uygulamalar, paketler ve görev dizileri dahil olmak üzere yazılım merkezi 'nden kullanılabilir yazılımları yüklemesini engellemez.  
> -  Bu ayarı etkinleştirdiğinizde, istemcilerde yeni yazılım veya gerekli yazılım için bildirim bildirimleri gerçekleşmez. <!--6347668-->

### <a name="powershell-execution-policy"></a>PowerShell yürütme ilkesi

Configuration Manager istemcilerinin Windows PowerShell betiklerini nasıl çalıştırabilirim yapılandırın. Bu komut dosyalarını uyumluluk ayarları için yapılandırma öğelerinde algılama amacıyla kullanabilirsiniz. Ayrıca, betikleri bir dağıtımda standart bir komut dosyası olarak da gönderebilirsiniz.  

- **Atla**: Configuration Manager istemcisi, imzasız betikler çalıştırmak için Istemci bilgisayardaki Windows PowerShell yapılandırmasını atlar.  

- **Kısıtlanmış**: Configuration Manager istemcisi istemci bilgisayardaki geçerli PowerShell yapılandırmasını kullanır. Bu yapılandırma, imzasız betiklerin çalıştırılıp çalıştırılamayacağını belirler.  

- **Tümü imzalı**: Configuration Manager istemcisi yalnızca güvenilir bir yayımcı tarafından imzalanmışsa betikleri çalıştırır. Bu kısıtlama, istemci bilgisayardaki geçerli PowerShell yapılandırmasından bağımsız olarak uygulanır.  

Bu seçenek en az Windows PowerShell sürüm 2,0 gerektirir. Varsayılan değer **Tümü imzalanır**.  

> [!TIP]  
> İmzasız betikler Bu istemci ayarı nedeniyle çalıştırılmamışsa, Configuration Manager Bu hatayı aşağıdaki yollarla bildirir:  
>
> - Konsolundaki **izleme** çalışma alanında, dağıtım durumu hata kimliği **0X87d00327**görüntülenir. Ayrıca, açıklama **komut dosyasının imzalanmadığını**gösterir.  
> - Raporlar hata türü **bulma hatasını**görüntüler. Sonra raporlar **0X87d00327** hata kodunu ve açıklama **betiği Imzalı değil**veya **0x87d00320** hata kodu ve **betik ana bilgisayarının henüz yüklenmemiş**olduğunu gösterir. Örnek rapor: bir **varlık için yapılandırma temelindeki yapılandırma öğelerinin hatalarının ayrıntıları**.  
> - **Dcmwmiprovider. log** dosyası, ileti **betiği imzalanmadı Iletisini görüntülüyor (hata: 87D00327; Kaynak: CCM)**.  

### <a name="show-notifications-for-new-deployments"></a>Yeni dağıtımlar için bildirimleri göster

Bir haftadan daha az kullanılabilir olan dağıtımlar için bir bildirim göstermek üzere **Evet** ' i seçin. Bu ileti, istemci aracısının her başlayışında görüntülenir.

### <a name="disable-deadline-randomization"></a>Rastgele son tarih seçimini devre dışı bırak

Dağıtım son tarihinden sonra, bu ayar istemcinin gerekli yazılım güncelleştirmelerinin yüklenmesi için iki saate kadar etkinleştirme gecikmesi kullanıp kullanmadığını belirler. Varsayılan olarak etkinleştirme gecikmesi devre dışıdır.  

Sanal Masaüstü Altyapısı (VDı) senaryolarında bu gecikme, birden çok sanal makineyle bir konak makineye yönelik CPU işleme ve veri aktarımını dağıtmaya yardımcı olur. VDı kullanmıyor olsanız bile, aynı güncelleştirmeleri aynı anda yükleyen birçok istemcinin olması, site sunucusundaki CPU kullanımını olumsuz yönde artırabilir. Bu davranış ayrıca dağıtım noktalarını yavaşlatabilir ve kullanılabilir ağ bant genişliğini önemli ölçüde azaltır.  

İstemcilerin gerekli yazılım güncelleştirmelerini gecikmeli olmadan dağıtım son tarihinde yüklemesi gerekiyorsa, bu ayarı **Evet**olarak yapılandırın.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Dağıtım son tarihinden sonra zorlama için yetkisiz kullanım süresi (saat)

Kullanıcılardan gerekli uygulama veya yazılım güncelleştirme dağıtımlarını son tarihin ötesinde daha fazla zaman vermek istiyorsanız, bu seçeneği **Evet**olarak ayarlayın. Bu yetkisiz kullanım süresi, bir bilgisayarın uzun süre kapalı olması için, kullanıcının birçok uygulama veya güncelleştirme dağıtımı yüklemesi gerekir. Örneğin, bu ayar Kullanıcı tatilden döndürüldüğünde ve istemci vadesi geçmiş uygulama dağıtımlarını yüklerken uzun süre beklemek zorunda olduğunda yararlıdır.

Yetkisiz kullanım süresini 1-120 saat olarak ayarlayın. Bu ayarı, **kullanıcı tercihlerine göre bu dağıtımın uygulanması için**dağıtım özelliği ile birlikte kullanın. Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period).


## <a name="computer-restart"></a>Bilgisayar yeniden başlatma

Aşağıdaki ayarlar, bilgisayara uygulanan en kısa bakım penceresinden daha kısa sürede olmalıdır:

- **Kullanıcıya, Kullanıcı oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki aralığı belirten geçici bir bildirim göster (dakika)**
- **Kullanıcı oturumu kapatmadan veya bilgisayar yeniden başlatılmadan önceki geri sayım aralığını gösteren, kullanıcının kapatamayacağı bir iletişim kutusu görüntüler (dakika)**


Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../manage/collections/use-maintenance-windows.md).

- **Bilgisayar yeniden başlatma geri sayım bildirimleri (dakika) için erteleme süresini belirtin** (sürüm 1906 ' den başlayarak)<!--3976435-->
  - Varsayılan değer 240 dakikadır.
  - Erteleme süresi değeri, geçici bildirim değerinden daha az olmalıdır ve kullanıcının kapatamıyorum bildirimin değeri eksi değer olmalıdır.
  - Daha fazla bilgi için bkz. [cihaz yeniden başlatma bildirimleri](device-restart-notifications.md).

**Bir dağıtım yeniden başlatma gerektirdiğinde, bildirim yerine kullanıcıya bir iletişim kutusu penceresi gösterin**<!--3555947-->: Sürüm 1902 ' den başlayarak, bu ayarı **Evet** olarak yapılandırmak, Kullanıcı deneyimini daha zorbir şekilde değiştirir. Bu ayar tüm uygulamaların, Görev sıralarının ve yazılım güncelleştirmelerinin tüm dağıtımları için geçerlidir. Daha fazla bilgi için bkz. [plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> Configuration Manager 1902 ' de, bazı durumlarda iletişim kutusu bildirim bildirimlerini değiştirmez. Bu sorunu çözmek için [Configuration Manager sürüm 1902 için güncelleştirme paketini](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)yükledikten sonra. <!--4404715-->


## <a name="delivery-optimization"></a>Teslim Iyileştirme 

<!-- 1324696 -->
Şirket ağınızda ve Uzak ofislerde içerik dağıtımını tanımlamak ve düzenlemek için Configuration Manager sınır gruplarını kullanırsınız. [Windows teslim iyileştirme](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) , Windows 10 cihazları arasında içerik paylaşmak için bulut tabanlı ve eşler arası bir teknolojidir. Dağıtım Iyileştirmesini, içerik eşleri arasında paylaşırken sınır gruplarınızı kullanacak şekilde yapılandırın.

> [!Note]
> - Teslim Iyileştirme yalnızca Windows 10 istemcilerinde kullanılabilir.
> - Teslim Iyileştirme bulut hizmetine Internet erişimi, eşler arası işlevselliğini kullanmak için bir gereksinimdir. Gerekli Internet uç noktaları hakkında daha fazla bilgi için bkz. [dağıtım iyileştirmesi hakkında sık sorulan sorular](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).
> - İçerik depolaması için bir CMG kullanırken, kullanılabilir [istemci ayarı](#allow-clients-to-download-delta-content-when-available) etkinleştirildiğinde **Delta içeriğini indir** , üçüncü taraf güncelleştirmeler için içerik istemcilere indirmez. <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Teslim Iyileştirme grubu KIMLIĞI için Configuration Manager sınır grupları kullanma

Sınır grubu tanımlayıcısını istemcideki teslim Iyileştirme grubu tanımlayıcısı olarak uygulamak için **Evet** ' i seçin. İstemci, teslim Iyileştirme bulut hizmeti ile iletişim kurduğunda, istenen içeriğe sahip eşleri bulmak için bu tanımlayıcıyı kullanır.

> [!Note]
> Microsoft, istemcinin bu ayarı Grup ilkesi yerine yerel ilke aracılığıyla yapılandırmasına izin vermesini önerir. Bu, sınır grubu tanımlayıcısının istemcide teslim Iyileştirme grubu tanımlayıcısı olarak ayarlanalmasına izin verir. Daha fazla bilgi için bkz. [teslim iyileştirmesi](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>Configuration Manager tarafından yönetilen cihazları, içerik indirme için Microsoft bağlı önbellek sunucularını kullanacak şekilde etkinleştirin

<!--3555764-->
İstemcilerin Microsoft bağlı önbellek sunucusu olarak etkinleştirdiğiniz şirket içi dağıtım noktasından içerik indirmesine izin vermek için **Evet** ' i seçin. Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği Configuration Manager](../../plan-design/hierarchy/microsoft-connected-cache.md).


## <a name="endpoint-protection"></a>Uç Nokta Koruma

> [!Tip]
> Aşağıdaki bilgilere ek olarak, Endpoint Protection istemci ayarlarını kullanma hakkındaki ayrıntıları [örnek senaryoda bulabilirsiniz: bilgisayarları kötü amaçlı yazılımlardan korumak için Endpoint Protection kullanma](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>İstemci bilgisayarlarda Endpoint Protection istemcisini yönetme

Hiyerarşinizdeki bilgisayarlarda var olan Endpoint Protection ve Windows Defender istemcilerini yönetmek istiyorsanız **Evet** ' i seçin.  

Endpoint Protection istemcisini zaten yüklediyseniz ve Configuration Manager ile yönetmek istiyorsanız bu seçeneği belirleyin. Bu ayrı yükleme, Configuration Manager bir uygulama veya paket ve program kullanan bir komut dosyası işleme içerir. Windows 10 cihazlarında Endpoint Protection aracısının yüklü olması gerekmez. Ancak, bu cihazların **istemci bilgisayarlarda Endpoint Protection Istemcisinin yönetilmesi** hala gerekir. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>İstemci bilgisayarlarda Endpoint Protection istemcisini yükle

İstemcisini zaten çalıştırmayan istemci bilgisayarlarda Endpoint Protection istemcisini yüklemek ve etkinleştirmek için **Evet** ' i seçin. Windows 10 istemcilerinin Endpoint Protection aracısının yüklü olması gerekmez.  

> [!NOTE]  
> Endpoint Protection istemcisi zaten yüklüyse, **Hayır** seçimi Endpoint Protection istemcisini kaldırmaz. Endpoint Protection istemcisini kaldırmak için **istemci bilgisayarlarda Endpoint Protection Istemcisini Yönet** Istemci ayarını **Hayır**olarak ayarlayın. Ardından, Endpoint Protection istemcisini kaldırmak için bir paket ve program dağıtın.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Bakım pencerelerinin dışında Endpoint Protection istemci yüklemesine ve yeniden başlatılmasına izin verin. Bakım pencereleri, istemci yüklemesi için en az 30 dakika uzunluğunda olmalıdır

Bakım pencereleri ile tipik yükleme davranışlarını geçersiz kılmak için bu seçeneği **Evet** olarak ayarlayın. Bu ayar, güvenlik amaçları doğrultusunda sistem bakımının önceliği için iş gereksinimlerini karşılar.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Yazma filtresi olan Windows Embedded cihazları için Endpoint Protection istemci yüklemesini yürüt (yeniden başlatma gerektirir)

Windows Embedded cihazında yazma filtresini devre dışı bırakmak için **Evet** ' i seçin ve cihazı yeniden başlatın. Bu eylem, yükleme işlemini cihaza kaydeder.  

**Hayır**' ı seçerseniz, istemci, cihaz yeniden başlatıldığında temizleyen geçici bir katmana yüklenir. Bu senaryoda Endpoint Protection istemci, başka bir yükleme cihaza değişiklikler yapana kadar tam olarak yüklenmez. Bu yapılandırma varsayılandır.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Endpoint Protection istemcisi yüklendikten sonra gereken bilgisayar yeniden başlatmalarının bastır

Endpoint Protection istemcisi yüklendikten sonra bilgisayarın yeniden başlatılmasını engellemek için **Evet** ' i seçin.  

> [!IMPORTANT]  
> Endpoint Protection istemcisi bir bilgisayarın yeniden başlatılmasını gerektiriyorsa ve bu ayar **Hayır**ise, bilgisayar yapılandırılmış bakım pencerelerinden bağımsız olarak yeniden başlatılır.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Endpoint Protection yüklemesini tamamlaması için gereken yeniden başlatmayı kullanıcının erteleyebilmesi için izin verilen süre (saat)

Endpoint Protection istemcisi yüklendikten sonra bir yeniden başlatma gerekiyorsa, bu ayar kullanıcıların gerekli yeniden başlatmayı erteleyene saat sayısını belirtir. Bu ayar, **Endpoint Protection istemcisi yüklendikten sonra gereken bilgisayar yeniden başlatmalarının** ayarlanmasını **gerektirir.**  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>İstemci bilgisayarlardaki ilk tanım güncelleştirmesi için alternatif kaynakları (Microsoft Windows Update, Microsoft Windows Server Update Services veya UNC paylaşımları gibi) devre dışı bırak

Configuration Manager istemci bilgisayarlara yalnızca ilk tanım güncelleştirmesini yüklemesini istiyorsanız **Evet** ' i seçin. Bu ayar, gereksiz ağ bağlantılarını önlemek ve tanım güncelleştirmesinin ilk yüklemesi sırasında ağ bant genişliğini azaltmak için faydalı olabilir.  



## <a name="enrollment"></a>Kayıt

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Mobil cihaz eski istemcileri için yoklama aralığı

Eski mobil cihazların ilke için yoklama süresini dakika veya saat olarak belirlemek için **aralığı ayarla** ' yı seçin. Bu cihazlar Windows CE, Mac OS X ve UNIX ya da Linux gibi platformları içerir.

### <a name="polling-interval-for-modern-devices-minutes"></a>Modern cihazlar için yoklama aralığı (dakika)

Modern cihazların ilkeyi yoklayacağını belirten dakika sayısını girin. Bu ayar, şirket içi mobil cihaz yönetimi ile yönetilen Windows 10 cihazlarına yöneliktir.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Kullanıcıların mobil cihazları ve Mac bilgisayarları kaydetmesine izin ver

Eski cihazların Kullanıcı tabanlı kaydını etkinleştirmek için, bu seçeneği **Evet**olarak ayarlayın ve ardından aşağıdaki ayarı yapılandırın:

- **Kayıt profili**: bir kayıt profili oluşturmak veya seçmek Için **profili ayarla** ' yı seçin. Daha fazla bilgi için bkz. [kayıt için istemci ayarlarını yapılandırma](deploy-clients-to-macs.md#configure-client-settings).

### <a name="allow-users-to-enroll-modern-devices"></a>Kullanıcıların modern cihazları kaydetmesine izin ver

Modern cihazların Kullanıcı tabanlı kaydını etkinleştirmek için, bu seçeneği **Evet**olarak ayarlayın ve ardından aşağıdaki ayarı yapılandırın:

- **Modern cihaz kayıt profili**: bir kayıt profili oluşturmak veya seçmek Için **profili ayarla** ' yı seçin. Daha fazla bilgi için bkz. [kullanıcıların modern cihazları kaydetmesine izin veren bir kayıt profili oluşturma](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf).



## <a name="hardware-inventory"></a>Donanım envanteri  

### <a name="enable-hardware-inventory-on-clients"></a>İstemcilerde donanım envanterini etkinleştir

Varsayılan olarak, bu ayar **Evet**' tir. Daha fazla bilgi için bkz. [Donanım envanterine giriş](../manage/inventory/introduction-to-hardware-inventory.md).

### <a name="hardware-inventory-schedule"></a>Donanım envanteri zamanlaması

İstemcilerin donanım envanteri döngüsünü çalıştırma sıklığını ayarlamak için **zamanla** ' yı seçin. Varsayılan olarak, bu geçiş her yedi günde bir gerçekleşir.

### <a name="maximum-random-delay-minutes"></a>En yüksek rastgele gecikme (dakika)

Configuration Manager istemcisinin, belirlenen zamanlamadan donanım envanteri döngüsünü rastgele rasgele hale geçmesi için en fazla dakika sayısını belirtin. Tüm istemcilerde bu rastgele seçim, site sunucusundaki envanter işleme yükünü dengelemeye yardımcı olur. 0 ile 480 dakika arasında bir değer belirtebilirsiniz. Varsayılan olarak, bu değer 240 dakikaya ayarlanır (4 saat).

### <a name="maximum-custom-mif-file-size-kb"></a>En büyük özel MIF dosyası boyutu (KB)

İstemcinin bir donanım envanteri çevrimi sırasında topladığı her bir özel yönetim bilgisi biçimi (MIF) dosyası için izin verilen en büyük boyutu kilobayt (KB) cinsinden belirtin. Configuration Manager donanım envanteri Aracısı, bu boyutu aşan özel MIF dosyalarını işlemez. 1 KB ile 5.120 KB arasında bir boyut belirtebilirsiniz. Varsayılan olarak bu değer 250 KB'ye ayarlanır. Bu ayar normal donanım envanteri veri dosyasının boyutunu etkilemez.  

> [!NOTE]  
> Bu ayar yalnızca varsayılan istemci ayarlarında kullanılabilir.  

### <a name="hardware-inventory-classes"></a>Donanım envanteri sınıfları

Sms_def. mof dosyasını el ile düzenlemeden istemcilerden topladığınız donanım bilgilerini genişletmek için **sınıfları ayarla** ' yı seçin. Daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../manage/inventory/configure-hardware-inventory.md).  

### <a name="collect-mif-files"></a>MIF dosyalarını topla

Donanım envanteri sırasında Configuration Manager istemcilerinden MIF dosyalarının toplanmasını isteyip istemediğinizi belirtmek için bu ayarı kullanın.  

Bir MIF dosyasının donanım envanteri tarafından toplanması için istemci bilgisayarda doğru konumda olması gerekir. Varsayılan olarak, dosyalar aşağıdaki yollarda bulunur:  

- **IDMIF dosyaları** , Windows\system32\ccm\ınventory\ıdmıf klasöründe olmalıdır.

- **NOIDMIF dosyaları** , Windows\system32\ccm\ınventory\noıdmıf klasöründe olmalıdır.

> [!NOTE]  
> Bu ayar yalnızca varsayılan istemci ayarlarında kullanılabilir.



## <a name="metered-internet-connections"></a>Tarifeli İnternet bağlantıları  

Windows 8 ve üzeri bilgisayarların Configuration Manager ile iletişim kurmak için Tarifeli İnternet bağlantıları kullanma biçimini yönetin. İnternet sağlayıcıları bazen tarifeli bir İnternet bağlantısında olduğunuzda, gönderilen ve aldığınız veri miktarına göre ücretlendirilir.  

> [!NOTE]  
> Yapılandırılmış istemci ayarı aşağıdaki senaryolarda uygulanmaz:  
>
> - Bilgisayar bir gezici veri bağlantısı üzerinde ise Configuration Manager istemci, verilerin Configuration Manager sitelere aktarılmasını gerektiren herhangi bir görev gerçekleştirmez.  
> - Windows ağ bağlantısı özellikleri tarifeli olmayan olarak yapılandırılırsa, Configuration Manager istemci bağlantı tarifeli olmayan şekilde davranır ve bu nedenle verileri siteye aktarır.  

### <a name="client-communication-on-metered-internet-connections"></a>Tarifeli İnternet bağlantılarında istemci iletişimi

Bu ayar için aşağıdaki seçeneklerden birini belirleyin:  

- **Izin ver**: istemci cihazı gezici bir veri bağlantısı kullanmadığı takdirde Tarifeli İnternet bağlantısı üzerinden tüm istemci iletişimlerine izin verilir.  

- **Limit**: Tarifeli İnternet bağlantısı üzerinden yalnızca aşağıdaki istemci iletişimlerine izin verilir:  

    - İstemci ilkesi alma  

    - Siteye gönderilecek istemci durumu iletileri  

    - Yazılım Merkezi 'nden yazılım yükleme istekleri  

    - Gerekli dağıtımlar (yükleme son tarihine ulaşıldığında)  

    > [!IMPORTANT]  
    > İstemci, tarifeli internet bağlantısı ayarlarından bağımsız olarak yazılım merkezinden yazılım yüklemelerine her zaman izin verir.  

    İstemci Tarifeli İnternet bağlantısı için veri aktarım sınırına ulaşırsa, istemci artık Configuration Manager sitelerle iletişim kurmayı dener.  

- **Engelle**: Configuration Manager istemci tarifeli bir internet bağlantısı olduğunda Configuration Manager sitelerle iletişim kurmayı denemez. Bu seçenek varsayılandır.  



## <a name="power-management"></a>Güç yönetimi  

### <a name="allow-power-management-of-devices"></a>Cihazların güç yönetimine izin ver

İstemcilerde güç yönetimini etkinleştirmek için bu seçeneği **Evet** olarak ayarlayın. Daha fazla bilgi için bkz. [güç yönetimine giriş](../manage/power/introduction-to-power-management.md).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Kullanıcıların aygıtlarını güç yönetimi dışında bırakmasına izin ver

Yazılım Merkezi kullanıcılarının bilgisayarlarını yapılandırılmış tüm güç yönetimi ayarlarından dışlamasına izin vermek için **Evet** ' i seçin.  

### <a name="allow-network-wake-up"></a>Ağ Uyandırma için izin ver

1810 'ye eklendi. **Enable**olarak ayarlandığında, ağ bağdaştırıcısının cihazı uyandırmasına izin vermek için ağ bağdaştırıcısında güç ayarlarını yapılandırır. **Devre dışı**olarak ayarlandığında, ağ bağdaştırıcısındaki güç ayarları ağ bağdaştırıcısının cihazı uyandırmasına izin vermiyor olarak yapılandırılır.

### <a name="enable-wake-up-proxy"></a>Uyandırma proxy'sini etkinleştir

Tek noktaya yayın paketleri için yapılandırıldığında sitenin LAN'da Uyandırma ayarını tamamlamak için **Evet** ' i belirtin.  

Uyandırma proxy 'si hakkında daha fazla bilgi için bkz. [istemcileri nasıl uyandırmayı planlayın](plan/plan-wake-up-clients.md).  

> [!WARNING]  
> Bir üretim ağında, ilk olarak nasıl çalıştığını ve bir test ortamında değerlendirmeyi bilmeden uyandırma proxy 'sini etkinleştirmeyin.  

Ardından, gerektiğinde aşağıdaki ek ayarları yapılandırın:

- **Uyandırma proxy 'si bağlantı noktası numarası (UDP)**: istemcilerin uyuyan bilgisayarlara Uyandırma paketleri göndermek için kullandığı bağlantı noktası numarası. Varsayılan 25536 bağlantı noktasını koruyun veya numarayı seçtiğiniz bir değerle değiştirin.  

- **LAN'da Uyandırma bağlantı noktası numarası (UDP)**: site **özelliklerinin** **bağlantı noktaları** sekmesinde LAN'da Uyandırma (UDP) bağlantı noktası numarasını değiştirmediğiniz müddetçe varsayılan 9 değerini koruyun.  

    > [!IMPORTANT]  
    > Bu numara, site **Özellikleri**'ndeki numara ile aynı olmalıdır. Bu numarayı tek bir yerde değiştirirseniz, diğer yerde otomatik olarak güncellenmez.  

- **Uyandırma proxy 'si Için Windows Defender güvenlik duvarı özel durumu**: Configuration Manager Istemcisi, Windows Defender güvenlik duvarı 'nı çalıştıran cihazlarda uyandırma proxy bağlantı noktası numarasını otomatik olarak yapılandırır. İstenen Güvenlik Duvarı profillerini belirtmek için **Yapılandır** ' ı seçin.  

    İstemcileri farklı bir güvenlik duvarı çalıştırıyorsanız, **uyandırma proxy 'si bağlantı noktası numarasına (UDP)** izin vermek için el ile yapılandırın.  

- **DirectAccess veya başka bir araya giren ağ cihazları için gerekliyse IPv6 ön ekleri. Birden çok girdi belirtmek için virgül kullanın**: ağınızda çalışacak uyandırma proxy 'si için gereken IPv6 öneklerini girin.



## <a name="remote-tools"></a>Uzak Araçlar  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>İstemcilerde uzaktan denetimi etkinleştir ve güvenlik duvarı özel durum profilleri

Configuration Manager uzaktan denetim özelliğini etkinleştirmek için **Yapılandır** ' ı seçin. İsteğe bağlı olarak, uzaktan denetimin istemci bilgisayarlarda çalışmasına izin vermek için güvenlik duvarı ayarlarını yapılandırın.  

Varsayılan seçenek olarak uzaktan denetim devre dışıdır.  

> [!IMPORTANT]  
> Güvenlik Duvarı ayarlarını yapılandırmazsanız, uzaktan denetim düzgün çalışmayabilir.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Kullanıcılar, Yazılım Merkezi'nde ilkeleri veya bildirim ayarlarını değiştirebilirler

Kullanıcıların uzaktan denetim seçeneklerini Yazılım Merkezi içinden değiştirip değiştiremeyeceğini seçin.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Beklenmeyen bilgisayarın Uzak Denetimi'ne izin ver

Yöneticinin oturumu kapalı veya kilitlenmiş bir istemci bilgisayara erişmek için uzaktan denetimi kullanıp kullanamayacağını seçin. Bu ayar devre dışı bırakıldığında yalnızca oturum açmış ve kilidi açılmış bir bilgisayar uzaktan denetlenebilir.  

### <a name="prompt-user-for-remote-control-permission"></a>Kullanıcıya Uzak Denetim izni sor

İstemci bilgisayarın uzaktan denetim oturumuna izin vermeden önce kullanıcının iznini soran bir ileti gösterilip gösterilmeyeceğini seçin.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Kullanıcıdan paylaşılan panodan içerik aktarma izni iste

Bir uzaktan denetim oturumunda paylaşılan panodan içerik aktarmadan önce, kullanıcılarınıza dosya aktarımlarını kabul etme veya reddetme fırsatı verin. Kullanıcıların oturum başına yalnızca bir kez izin vermesi gerekir. Görüntüleyici kendisine dosyayı aktarma izni verebilir.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Yerel Yöneticiler grubuna Uzak Denetim iznini ver

Uzaktan Denetim bağlantısını başlatan sunucuda yerel yöneticilerin istemci bilgisayarlara uzaktan denetim oturumları kurup kuramayacağını seçin.  

### <a name="access-level-allowed"></a>İzin verilen erişim düzeyi

İzin verilecek uzaktan denetim erişiminin düzeyini belirtin. Aşağıdaki ayarlardan birini seçin:  

- **Erişim Yok**
- **Yalnızca görüntüleme**
- **Tam denetim**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Uzaktan denetim ve Uzaktan Yardım 'ın izin verilen görüntüleyicileri

İstemci bilgisayarlara uzaktan denetim oturumları kurabilen Windows kullanıcılarının adlarını belirtmek için **Izleyicileri ayarla** ' yı seçin.  

### <a name="show-session-notification-icon-on-taskbar"></a>Görev çubuğunda oturum bildirimi simgesini göster

Etkin bir uzaktan denetim oturumu göstermek üzere istemcinin Windows görev çubuğunda bir simge göstermek için bu ayarı **Evet** olarak yapılandırın.  

### <a name="show-session-connection-bar"></a>Oturum bağlantı çubuğunu göster

Etkin bir uzaktan denetim oturumu göstermek için istemcilerde yüksek görünürlük oturum bağlantı çubuğunu göstermek üzere bu seçeneği **Evet** olarak ayarlayın.  

### <a name="play-a-sound-on-client"></a>İstemcide ses çıkart

Bir istemci bilgisayarda bir uzaktan denetim oturumunun etkin olduğunu göstermek için bu seçeneği ses kullanmak üzere ayarlayın. Aşağıdaki seçeneklerden birini belirtin:

- **Ses yok**
- **Oturum başlangıcı ve sonu** (varsayılan)
- **Oturum sırasında defalarca**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>İstenmeyen Uzak Yardım ayarlarını yönet

İstenmeyen uzaktan yardım oturumlarını Configuration Manager izin vermek için bu ayarı **Evet** olarak yapılandırın.  

İstenmeyen uzaktan yardım oturumunda, istemci bilgisayardaki kullanıcı oturumu başlatmak için yardım istemedi.  

### <a name="manage-solicited-remote-assistance-settings"></a>İstenen Uzak Yardım ayarlarını yönet

Bu seçeneği, istenen uzaktan yardım oturumlarını Configuration Manager yönetmeye izin vermek için **Evet** olarak ayarlayın.  

İstenen Uzaktan Yardım oturumunda, istemci bilgisayardaki kullanıcı uzaktan yardım için yöneticiye bir istek gönderdi.  

### <a name="level-of-access-for-remote-assistance"></a>Uzak Yardım için erişim düzeyi

Configuration Manager konsolunda başlatılan uzaktan yardım oturumlarına atanacak erişim düzeyini seçin. Aşağıdaki seçeneklerden birini belirtin:

- **Hiçbiri** (varsayılan)
- **Uzaktan görüntüleme**
- **Tam denetim**

> [!NOTE]  
> Uzaktan Yardım oturumunun gerçekleşmesi için istemci bilgisayardaki kullanıcının her zaman izin vermesi gerekir.  

### <a name="manage-remote-desktop-settings"></a>Uzak Masaüstü ayarlarını yönet

Bilgisayarlarda Uzak Masaüstü oturumlarını yönetmek Configuration Manager sağlamak için bu seçeneği **Evet** olarak ayarlayın.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>İzin verilen kullanıcıların Uzak Masaüstü bağlantısını kullanarak bağlanmasına izin ver

İzin verilen Görüntüleyici listesinde belirtilen kullanıcıları istemcilerdeki uzak masaüstü yerel kullanıcı grubuna eklemek için bu seçeneği **Evet** olarak ayarlayın.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Windows Vista işletim sistemini veya daha ileri işletim sistemini çalıştıran bilgisayarlarda ağ düzeyi kimlik doğrulamayı gerektir

İstemci bilgisayarlara Uzak Masaüstü bağlantıları kurmak için ağ düzeyinde kimlik doğrulaması (NLA) kullanmak üzere bu seçeneği **Evet** olarak ayarlayın. NLA, bir Uzak Masaüstü bağlantısı kurmadan önce Kullanıcı kimlik doğrulamasını tamamlayacağından, başlangıçta daha az uzak bilgisayar kaynağı gerektirir. NLA kullanılması daha güvenli bir yapılandırmadır. NLA, bilgisayarın kötü amaçlı kullanıcılardan veya yazılımlardan korunmasına yardımcı olur ve hizmet reddi saldırılarına karşı riski azaltır.  



## <a name="software-center"></a>Yazılım Merkezi

### <a name="select-these-new-settings-to-specify-company-information"></a>Şirket bilgilerini belirtmek için bu yeni ayarları seçin

Bu seçeneği **Evet**olarak ayarlayın ve ardından kuruluşunuz Için marka yazılım merkezi için aşağıdaki ayarları belirtin:

- **Şirket adı**: kullanıcıların yazılım merkezi 'nde göreceği kuruluş adını girin.  

- **Yazılım Merkezi Için renk şeması**: Software Center tarafından kullanılan birincil rengi tanımlamak Için **renk seç** ' e tıklayın.  

- **Yazılım Merkezi için bir logo seçin**: Yazılım Merkezi 'nde görünecek bir görüntü seçmek Için, **Araştır** ' a tıklayın. Logo, 400 x 100 piksellik bir JPEG, PNG veya BMP olmalı ve en fazla 750 KB boyutunda olmalıdır. Logo dosya adı boşluk içermemelidir.  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a>Yazılım merkezindeki onaylanmamış uygulamaları gizle

Bu seçeneği etkinleştirdiğinizde, onay gerektiren Kullanıcı tarafından kullanılabilir uygulamalar yazılım merkezi 'nde gizlenir.<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a>Yüklü uygulamaları yazılım merkezi 'nde gizle

Bu seçeneği etkinleştirdiğinizde, zaten yüklü olan uygulamalar artık Uygulamalar sekmesinde gösterilmez. Configuration Manager 1802 ' ye yüklediğinizde veya yükselttiğinizde Bu seçenek varsayılan olarak ayarlanır. Yüklenen uygulamalar, yükleme durumu sekmesi altında hala gözden geçirilmek üzere kullanılabilir. <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a>Yazılım Merkezi 'nde Uygulama Kataloğu bağlantısını gizle

Yazılım Merkezi 'nde Uygulama Kataloğu web sitesi bağlantısının görünürlüğünü belirtin. Bu seçenek ayarlandığında, kullanıcılar yazılım merkezi 'nin yükleme durumu düğümünde Uygulama Kataloğu web sitesi bağlantısını görmez. <!--1358214-->

> [!Important]  
> Uygulama kataloğunun Silverlight Kullanıcı deneyimi, güncel dal sürümü 1806 ' den itibaren desteklenmez. Sürüm 1906 ' den başlayarak, güncelleştirilmiş istemciler Kullanıcı tarafından kullanılabilen uygulama dağıtımları için yönetim noktasını otomatik olarak kullanır. Ayrıca yeni uygulama kataloğu rolleri yükleyemezsiniz. Sürüm 1910 ile uygulama kataloğu rolleri için destek sona erer.  

### <a name="software-center-tab-visibility"></a>Yazılım Merkezi sekme görünürlüğü

#### <a name="starting-in-version-1906"></a>1906 sürümünden başlayarak
<!--4063773-->

Yazılım Merkezi 'nde hangi sekmelerin görünür olacağını seçin. Sekmeyi **görünür sekmelere**taşımak için **Ekle** düğmesini kullanın. **Gizli sekmeler** listesine taşımak için **Kaldır** düğmesini kullanın. **Yukarı taşı** veya **aşağı taşı** düğmelerini kullanarak sekmeleri sıralayın. 

Kullanılabilir sekmeler:
- **Uygulamalar**
- **Güncelleştirmeler**
- **İşletim Sistemleri**
- **Yükleme durumu**
- **Cihaz Uyumluluğu**
- **Seçenekler**
- **Sekme Ekle** düğmesine tıklayarak 5 ' e kadar özel sekme ekleyin.
  - Özel sekme için **sekme adı** ve **içerik URL 'si** belirtin.
  - Özel bir sekmeyi kaldırmak için **Sil sekmesine** tıklayın.  

  >[!Important]  
  > - Bazı Web sitesi özellikleri, yazılım merkezi 'nde özel bir sekme olarak kullanılırken çalışmayabilir. Bunu istemcilere dağıtılmadan önce sonuçları test ettiğinizden emin olun. <!--519659-->
  > - Özel bir sekme eklediğinizde yalnızca güvenilen veya intranet Web sitesi adresleri belirtin.<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>Sürüm 1902 ve öncesi

Aşağıdaki sekmeleri yazılım merkezi 'nde görünür yapmak için bu gruptaki ek ayarları **Evet** olarak yapılandırın:

- **Uygulamalar**
- **Güncelleştirmeler**
- **İşletim Sistemleri**
- **Yükleme durumu**
- **Cihaz Uyumluluğu**
- **Seçenekler**
- **Yazılım Merkezi için özel bir sekme belirtin** <!--1358132-->
    - **Sekme adı**
    - **İçerik URL 'SI**

    >[!Important]  
    > Bazı Web sitesi özellikleri, yazılım merkezi 'nde özel bir sekme olarak kullanılırken çalışmayabilir. Bunu istemcilere dağıtılmadan önce sonuçları test ettiğinizden emin olun. <!--519659-->
    >
    > Özel bir sekme eklediğinizde yalnızca güvenilen veya intranet Web sitesi adresleri belirtin.<!--SCCMDocs issue 1575-->

Örneğin, kuruluşunuz uyumluluk ilkelerini kullanmıyorsa ve yazılım merkezi 'nde cihaz uyumluluğu sekmesini gizlemek istiyorsanız, **Cihaz uyumluluğunu etkinleştir sekmesini** **Hayır**olarak ayarlayın.

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a>Yazılım Merkezi 'nde varsayılan görünümleri yapılandırma
<!--3612112-->
*(Sürüm 1902 ' de tanıtılmıştır)*

- **Varsayılan uygulama filtresini** **Tüm** ya da yalnızca **gerekli** uygulamalar olarak yapılandırın.  

  - Software Center her zaman varsayılan ayarınızı kullanır. Kullanıcılar bu filtreyi değiştirebilir, ancak yazılım merkezi 'nin tercih etmesi devam etmez.  

- **Varsayılan uygulama görünümünü** **kutucuk görünümü** veya **liste görünümü**olarak ayarlayın. 

  - Bir Kullanıcı bu yapılandırmayı değiştirirse, yazılım merkezi kullanıcının gelecekte tercih ettiği tercihi sürdürür. 


## <a name="software-deployment"></a>Yazılım dağıtımı  

### <a name="schedule-re-evaluation-for-deployments"></a>Dağıtımlar için yeniden değerlendirmeyi zamanla

Configuration Manager, tüm dağıtımlar için gereksinim kurallarını yeniden değerlendirmeye yönelik bir zamanlama yapılandırın. Varsayılan değer her yedi günde bir olur.  

> [!IMPORTANT]  
> Bu ayar, yerel istemciye ağ veya site sunucusuna ait olduğundan daha fazla bilgi sağlar. Daha Agresif yeniden değerleme zamanlaması, ağınızın ve istemci bilgisayarlarınızın performansını olumsuz yönde etkiler. Microsoft varsayılan değerden daha düşük bir değer ayarlanmasını önermez. Bu değeri değiştirirseniz, performansı yakından izleyin.  

Bu eylemi bir istemciden şu şekilde başlatın: **Configuration Manager** Denetim Masası 'Nda, **Eylemler** sekmesinden **uygulama dağıtımı değerlendirme döngüsünü**seçin.  



## <a name="software-inventory"></a>Yazılım envanteri  

### <a name="enable-software-inventory-on-clients"></a>İstemcilerde yazılım envanterini etkinleştir

Bu seçenek varsayılan olarak **Evet** ' e ayarlanır. Daha fazla bilgi için bkz. [yazılım envanterine giriş](../manage/inventory/introduction-to-software-inventory.md).

### <a name="schedule-software-inventory-and-file-collection"></a>Yazılım envanterini ve dosya toplamayı zamanla

İstemcilerin yazılım envanterini ve dosya toplama döngülerini çalıştırma sıklığını ayarlamak için **zamanla** ' yı seçin. Varsayılan olarak, bu geçiş her yedi günde bir gerçekleşir.

### <a name="inventory-reporting-detail"></a>Envanter raporlama ayrıntısı

Envantere kaydedilecek aşağıdaki dosya bilgisi düzeylerinden birini belirtin:

- **Yalnızca dosya**
- **Yalnızca ürün**
- **Tüm ayrıntılar** (varsayılan)

### <a name="inventory-these-file-types"></a>Bu dosya türlerini envantere kaydet

Envantere kaydedilecek dosya türlerini belirtmek istiyorsanız, **türleri ayarla**' yı seçin ve ardından aşağıdaki seçenekleri yapılandırın:  

> [!NOTE]  
> Bir bilgisayara birden çok özel istemci ayarı uygulanmışsa, her bir ayarın döndürdüğü sayım birleştirilir.  

- Stoğa yeni bir dosya türü eklemek için **Yeni** ' yi seçin. Sonra **envantere kaydedilmiş dosya özellikleri** iletişim kutusunda aşağıdaki bilgileri belirtin:  

    - **Ad**: envantere eklemek istediğiniz dosya için bir ad girin. Herhangi bir metin dizesini`*`temsil etmek için bir yıldız işareti () joker karakteri ve herhangi bir tek`?`karakteri temsil eden bir soru işareti () kullanın. Örneğin,. doc uzantılı tüm dosyaları envantere eklemek istiyorsanız, dosya adını `*.doc`belirtin.  

    - **Konum**: **Ayarla** ' yı seçerek **yol özellikleri** iletişim kutusunu açın. Yazılım envanterini, belirtilen dosya için tüm istemci sabit disklerini arayacak, belirtilen bir yolu arayacak ( `C:\Folder`Örneğin,) veya belirtilen değişkeni (örneğin, `%windir%`) arayacak şekilde yapılandırın. Ayrıca, belirtilen yolun altındaki tüm alt klasörleri arayabilirsiniz.  

    - **Şifrelenmiş ve sıkıştırılmış dosyaları dışarıda bırak**: Bu seçeneği belirlediğinizde, sıkıştırılan veya şifrelenen tüm dosyalar envantere aktarılmaz.  

    - **Windows klasöründeki dosyaları dışarıda bırak**: Bu seçeneği belirlediğinizde, Windows klasöründeki ve onun alt klasörlerindeki tüm dosyalar envantere aktarılmaz.  

    **Envantere kaydedilmiş dosya özellikleri** iletişim kutusunu kapatmak için **Tamam ' ı** seçin. Envantere eklemek istediğiniz tüm dosyaları ekleyin ve ardından **Tamam** ' ı seçerek **istemci ayarını Yapılandır** iletişim kutusunu kapatın.  

### <a name="collect-files"></a>Dosyaları topla

İstemci bilgisayarlardan dosya toplamak istiyorsanız **dosyaları ayarla**' yı seçin ve ardından aşağıdaki ayarları yapılandırın:  

> [!NOTE]  
> Bir bilgisayara birden çok özel istemci ayarı uygulanmışsa, her bir ayarın döndürdüğü sayım birleştirilir.  

- **Istemci ayarını Yapılandır** iletişim kutusunda, toplanacak bir dosya eklemek için **Yeni** ' yi seçin.  

- **Toplanan Dosya Özellikleri** iletişim kutusunda, şu bilgileri sağlayın:  

    - **Ad**: toplamak istediğiniz dosya için bir ad sağlayın. Herhangi bir metin dizesini`*`temsil etmek için bir yıldız işareti () joker karakteri ve herhangi bir tek`?`karakteri temsil eden bir soru işareti () kullanın.  

    - **Konum**: **Ayarla** ' yı seçerek **yol özellikleri** iletişim kutusunu açın. Yazılım envanterini, toplamak istediğiniz dosya için tüm istemci sabit disklerini aramak, belirtilen bir yolu aramak (örneğin, `C:\Folder`) veya belirtilen değişkeni (örneğin, `%windir%`) aramak üzere yapılandırın. Ayrıca, belirtilen yolun altındaki tüm alt klasörleri arayabilirsiniz.  

    - **Şifrelenmiş ve sıkıştırılmış dosyaları dışarıda bırak**: Bu seçeneği belirlediğinizde, sıkıştırılan veya şifrelenen dosyalar toplanmaz.  

    - **Dosyaların toplam boyutu (KB) değerini aştığında dosya toplamayı Durdur (KB)**: istemcinin belirtilen dosyaları toplamayı durdurduğu dosya boyutunu KILOBAYT (KB) cinsinden belirtin.  

    > [!NOTE]  
    > Site sunucusu toplanan dosyaların en son değişen beş sürümünü toplar ve bunları `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` dizinde depolar. Son yazılım envanteri döngüsünden bu yana bir dosya değiştirilmediyse, dosya yeniden toplanmaz.  
    >
    > Yazılım envanteri 20 MB 'tan büyük dosyalar toplanmaz.  
    >
    > **Istemci ayarını Yapılandır** iletişim kutusundaki **toplanan tüm dosyalar için en büyük boyut (KB)** değeri, toplanan tüm dosyaların en büyük boyutunu gösterir. Bu boyuta ulaşıldığında dosya toplama işlemi duraklar. Toplanmış olan tüm dosyalar tutulur ve site sunucusuna gönderilir.  

    > [!IMPORTANT]
    > Yazılım envanterini birçok büyük dosyayı toplayacak şekilde yapılandırırsanız bu yapılandırma, ağınızın ve site sunucunuzun performansını olumsuz yönde etkileyebilir.  

    Toplanan dosyaları görüntüleme hakkında daha fazla bilgi için bkz. [Kaynak Gezgini kullanarak yazılım envanterini görüntüleme](../manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    **Toplanan dosya özellikleri** iletişim kutusunu kapatmak için **Tamam ' ı** seçin. Toplamak istediğiniz tüm dosyaları ekleyin ve ardından **Tamam** ' ı seçerek **istemci ayarını Yapılandır** iletişim kutusunu kapatın.  

### <a name="set-names"></a>Adları Ayarla

Yazılım envanteri Aracısı, dosya üst bilgisi bilgisinden üretici ve ürün adlarını alır. Bu adlar her zaman dosya üst bilgisi bilgilerinde standartlaştırılmış değildir. Kaynak Gezgini ' de yazılım envanterini görüntülediğinizde, aynı üretici veya ürün adının farklı sürümleri görünebilir. Bu görünen adları standartlaştırmak için **adları ayarla**' yı seçin ve ardından aşağıdaki ayarları yapılandırın:  

- **Ad türü**: yazılım envanteri hem üretici hem de ürünlerle ilgili bilgiler toplar. **Üretici** veya **ürün**için görünen adları yapılandırmak isteyip istemediğinizi seçin.  

- **Görünen ad**: **envantere alınan adlar** listesindeki adların yerine kullanmak istediğiniz görünen adı belirtin. Yeni bir görünen ad belirtmek için **Yeni**' yi seçin.  

- **Envantere kaydedilen adlar**: envantere kaydedilmiş bir ad eklemek için **Yeni**' yi seçin. Bu ad, yazılım envanterinde **görünen ad** listesinde seçilen ad ile değiştirilmiştir. Değiştirilecek birden çok ad ekleyebilirsiniz.  



## <a name="software-metering"></a>Yazılım Kullanım Ölçümü

### <a name="enable-software-metering-on-clients"></a>İstemcilerde yazılım kullanım ölçümünü etkinleştir

Bu ayar varsayılan olarak **Evet** olarak ayarlanır. Daha fazla bilgi için bkz. [yazılım kullanım ölçümü](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering).

### <a name="schedule-data-collection"></a>Veri toplamayı zamanla

İstemcilerin yazılım kullanım ölçümü döngüsünü çalıştırma sıklığını ayarlamak için **zamanla** ' yı seçin. Varsayılan olarak, bu geçiş her yedi günde bir gerçekleşir.



## <a name="software-updates"></a>Yazılım güncelleştirmeleri  

### <a name="enable-software-updates-on-clients"></a>İstemcilerde yazılım güncelleştirmelerini etkinleştir

Configuration Manager istemcilerde yazılım güncelleştirmelerini etkinleştirmek için bu ayarı kullanın. Bu ayarı devre dışı bıraktığınızda, Configuration Manager var olan dağıtım ilkelerini istemcilerden kaldırır. Bu ayarı yeniden etkinleştirirseniz istemci geçerli dağıtım ilkesini indirir.  

> [!IMPORTANT]  
> Bu ayarı devre dışı bıraktığınızda, yazılım güncelleştirmelerine dayalı uyumluluk ilkeleri artık çalışmaz.  

### <a name="software-update-scan-schedule"></a>Yazılım güncelleştirmesi tarama zamanlaması

İstemcinin bir uyumluluk değerlendirmesi taramasını ne sıklıkta başlattığını belirtmek için **zamanlama** ' yı seçin. Bu tarama, istemcideki yazılım güncelleştirmelerinin durumunu belirler (örneğin, gerekli veya yüklü). Uyumluluk değerlendirmesi hakkında daha fazla bilgi için bkz. [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

Varsayılan olarak, bu tarama her yedi günde bir başlatmak için basit bir zamanlama kullanır. Özel bir zamanlama oluşturabilirsiniz. Tam bir başlangıç günü ve saati belirtebilir, Evrensel Eşgüdümlü saat (UTC) veya yerel saati kullanabilir ve haftanın belirli bir günü için yineleme aralığını yapılandırabilirsiniz.  

> [!NOTE]  
> Bir günden daha az bir Aralık belirtirseniz Configuration Manager otomatik olarak bir gün olur.  

> [!WARNING]  
> İstemci bilgisayarlarındaki gerçek başlangıç saati, başlangıç zamanı ve en fazla iki saate kadar rastgele bir zaman miktarıdır. Bu rastgele seçim, istemci bilgisayarlarının taramayı başlatmasını ve aynı anda etkin yazılım güncelleştirme noktasına bağlanmasını engeller.  

### <a name="schedule-deployment-re-evaluation"></a>Dağıtım yeniden değerlendirmesini zamanla

Yazılım güncelleştirmeleri istemci aracısının, Configuration Manager istemci bilgisayarlarındaki yükleme durumu için yazılım güncelleştirmelerini yeniden değerlendirme sıklığını yapılandırmak için **zamanla** ' yı seçin. Daha önce yüklenmiş yazılım güncelleştirmeleri artık istemcilerde yer kalmadığında ancak hala gerekliyse, istemci yazılım güncelleştirmelerini yeniden yükler.

Bu zamanlamayı, yazılım güncelleştirme uyumluluğu için şirket ilkesine göre ve kullanıcıların yazılım güncelleştirmelerini kaldırıp kaldıramayacağı şekilde ayarlayın. Her dağıtım yeniden değerlendirme çevrimi, ağ ve istemci bilgisayar işlemcisi etkinliğine neden olur. Varsayılan olarak, bu ayar, her yedi günde bir dağıtım yeniden değerlendirme taraması başlatmak için basit bir zamanlama kullanır.  

> [!NOTE]  
> Bir günden daha az bir Aralık belirtirseniz Configuration Manager otomatik olarak bir gün olur.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Yazılım güncelleştirme dağıtım son tarihine ulaşıldığında, belirli bir süre içinde süresi dolacak tüm diğer yazılım güncelleştirme dağıtımlarını yükler

Belirli bir süre içinde gerçekleşen son tarihleri olan gerekli dağıtımlardan tüm yazılım güncelleştirmelerini yüklemek için bu seçeneği **Evet** olarak ayarlayın. Gerekli bir yazılım güncelleştirme dağıtımı bir son tarihe ulaştığında, istemci Dağıtımdaki yazılım güncelleştirmeleri için yükleme işlemini başlatır. Bu ayar, belirtilen süre içinde son tarih olan diğer gerekli dağıtımlardan yazılım güncelleştirmelerinin yüklenip yüklenmeyeceğini belirler.  

Gerekli yazılım güncelleştirmeleri için yüklemeyi hızlandırmak üzere bu ayarı kullanın. Bu ayar ayrıca, istemci güvenliğini artırmak, kullanıcıya yönelik bildirimleri azaltmak ve istemci yeniden başlatmaları azaltmak için de potansiyel olarak bulunur. Varsayılan seçenek olarak bu ayar **Hayır**olarak ayarlanmıştır.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Süre sonu geçmemiş bekleyen dağıtımların yükleneceği zaman aralığı

Önceki ayarın süresini belirtmek için bu ayarı kullanın. 1 ile 23 saat arasında bir değer girebilir ve 1 ile 365 gün arasında bir değer girebilirsiniz. Bu ayar varsayılan olarak yedi gün için yapılandırılmıştır.  

### <a name="allow-clients-to-download-delta-content-when-available"></a>İstemcilerin kullanılabilir olduğunda Delta içeriğini indirmesine izin ver

*(Sürüm 1902 ' de tanıtılmıştır)*

İstemcilerin Delta içerik dosyalarını kullanmasına izin vermek için bu seçeneği **Evet** olarak ayarlayın. Bu ayar cihazdaki Windows Update aracısına izin verir ve bunu seçmeli olarak indirin. 

- Bu istemci ayarını etkinleştirmeden önce, dağıtım Iyileştirmesinin ortamınız için uygun şekilde yapılandırıldığından emin olun. Daha fazla bilgi için bkz. [Windows teslim iyileştirme](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) ve [teslim iyileştirme istemci ayarı](#delivery-optimization).
 - Bu istemci ayarı **, Istemcilerde hızlı yükleme dosyalarının yüklenmesini etkinleştir ' in**yerini alır. İstemcilerin hızlı yükleme dosyalarını kullanmasına izin vermek için bu seçeneği **Evet** olarak ayarlayın. Daha fazla bilgi için bkz. [Windows 10 güncelleştirmeleri Için hızlı yükleme dosyalarını yönetme](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).
 - Configuration Manager sürüm 1910 ' den başlayarak, bu seçenek ayarlandığında Delta indirme yalnızca hızlı yükleme dosyaları değil, tüm Windows Update yükleme dosyaları için kullanılır.
    - İçerik depolaması için bir CMG kullanırken, kullanılabilir istemci ayarı etkinleştirildiğinde **Delta Içeriğini indir** , üçüncü taraf güncelleştirmeler için içerik istemcilere indirmez. <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>İstemcilerin Delta içeriği isteklerini almak için kullandığı bağlantı noktası

*(Sürüm 1902 ' de tanıtılmıştır)*

Bu ayar, Delta içeriğini indirmek üzere HTTP dinleyicisi için yerel bağlantı noktasını yapılandırır. Bu, varsayılan olarak 8005 olarak ayarlanmıştır. Bu bağlantı noktasını istemci güvenlik duvarında açmanız gerekmez. 

> [!NOTE]
>Bu istemci ayarı, **hızlı yükleme dosyaları için içerik indirmek için kullanılan bağlantı noktasını**değiştirir.


### <a name="enable-management-of-the-office-365-client-agent"></a>Office 365 Istemci aracısının yönetimini etkinleştirme

Bu seçeneği **Evet**olarak belirlediğinizde, Office 365 yükleme ayarlarının yapılandırılmasını sağlar. Ayrıca Office Içerik teslim ağlarından (CDNs) dosya indirmeyi ve dosyaları Configuration Manager bir uygulama olarak dağıtmanızı da mümkün kılar. Daha fazla bilgi için bkz. [Office 365 ProPlus 'ı yönetme](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a>"Yazılım güncelleştirmesi" bakım penceresi kullanılabilir olduğunda "tüm dağıtımlar" bakım penceresinde yazılım güncelleştirmelerinin yüklenmesini etkinleştir

Sürüm 1810 ' den başlayarak, bu seçeneği **Evet** olarak belirlediğinizde ve istemcide en az bir "yazılım güncelleştirmesi" bakım penceresi tanımlanmışsa, yazılım güncelleştirmeleri "tüm dağıtımlar" bakım penceresi sırasında yüklenir.

Varsayılan seçenek olarak bu ayar **Hayır**olarak ayarlanmıştır. Bu değer, daha önce olduğu gibi aynı davranışı kullanır: her iki tür de varsa, pencereyi yoksayar. <!--2839307-->

> [!NOTE]
> Bu ayar ayrıca, **görev dizileri**için geçerli olacak şekilde yapılandırdığınız bakım pencereleri için de geçerlidir.<!-- SCCMDocs-pr #4596 -->
>
> İstemcide yalnızca bir **dağıtımlar** penceresi varsa, bu pencerede yazılım güncelleştirmelerini veya görev dizilerini yine de yüklenir.

#### <a name="maintenance-window-example"></a>Bakım penceresi örneği

Örneğin, aşağıdaki bakım pencerelerini yapılandırırsınız:

- **Tüm dağıtım**: 02:00-04:00
- **Yazılım güncelleştirmeleri**: 04:00-06:00

Varsayılan olarak, istemci yazılım güncelleştirmelerini yalnızca ikinci bakım penceresi sırasında kurar. Bu senaryodaki tüm dağıtımlar için bakım penceresini yoksayar. Bu ayarı **Evet**olarak değiştirdiğinizde istemci, 02:00-06:00 arasında yazılım güncelleştirmelerini yüklüyor.


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a>Özellik güncelleştirmeleri için iş parçacığı önceliği belirtin

<!--3734525-->
Configuration Manager sürüm 1902 ' den başlayarak, Windows 10 sürüm 1709 veya üzeri istemcilerin [Windows 10 Bakımı](../../../osd/deploy-use/manage-windows-as-a-service.md)aracılığıyla bir özellik güncelleştirmesi yükleme önceliğini ayarlayabilirsiniz. Bu ayarın Windows 10 yerinde yükseltme görev dizileri üzerinde hiçbir etkisi yoktur.

Bu istemci ayarı aşağıdaki seçenekleri sağlar:

- **Yapılandırılmadı**: Configuration Manager ayarı değiştirmez. Yöneticiler kendi setupconfig. ini dosyasını önceden hazırlamalarını sağlayabilir. Bu varsayılan değerdir.

- **Normal**: Windows kurulumu daha hızlı bir şekilde daha fazla sistem kaynağı ve güncelleştirme kullanır. Daha fazla işlemci zamanı kullanır, bu nedenle toplam yükleme süresi daha kısadır, ancak kullanıcının kesintisi daha uzundur.  

    - `/Priority Normal` [Windows kurulumu komut satırı seçeneğiyle](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)cihazdaki setupconfig. ini dosyasını yapılandırır.

- **Düşük**: cihaz, arka planda indirildiğinde ve güncelleştirmelerde çalışmaya devam edebilirsiniz. Toplam yükleme süresi daha uzundur, ancak kullanıcının kesintisi daha kısadır. Bu seçeneği kullanırken bir zaman aşımını önlemek için en fazla çalışma süresini artırmanız gerekebilir.  

    - `/Priority` [Windows kurulumu komut satırı seçeneğini](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) setupconfig. ini dosyasından kaldırır.


### <a name="enable-third-party-software-updates"></a>Üçüncü taraf yazılım güncelleştirmelerini etkinleştir

Bu seçeneği **Evet**olarak belirlediğinizde, **bir intranet Microsoft güncelleştirme hizmeti konumu Için Imzalı güncelleştirmelere izin ver** ilkesini ayarlar ve Imzalama sertifikasını istemcideki güvenilen yayımcı deposuna kurar.

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>Özellik güncelleştirmeleri için dinamik güncelleştirmeyi etkinleştir
<!--4062619-->
Configuration Manager sürüm 1906 ' den başlayarak, [Windows 10 Için dinamik güncelleştirme](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)'yi yapılandırabilirsiniz. Dinamik güncelleştirme, istemciyi Internet 'ten bu güncelleştirmeleri indirmek üzere yönlendirerek Windows kurulumu sırasında dil paketlerini, istek üzerine, sürücüleri ve toplu güncelleştirmeleri yükler. Bu ayar **Evet** veya **Hayır**olarak ayarlandığında, özellik güncelleştirme yüklemesi sırasında kullanılan [setupconfig](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) dosyasını değiştirir Configuration Manager.

- **Yapılandırılmadı** -varsayılan değer. Setupconfig dosyasında değişiklik yapılmadı.
  - Dinamik güncelleştirme, Windows 10 ' un tüm desteklenen sürümlerinde varsayılan olarak etkinleştirilmiştir.
    - Windows 10 sürümleri 1803 ve öncesi için dinamik güncelleştirme, cihazın WSUS sunucusunu onaylanan dinamik güncelleştirmeler için denetler. Configuration Manager ortamlarında dinamik güncelleştirmeler, WSUS sunucusunda hiçbir şekilde doğrudan onaylanmamış ve bu sayede bu cihazların yüklemesi yüklenmez.
    - Dinamik güncelleştirme, Windows 10 sürüm 1809 ' den başlayarak Microsoft Update 'den dinamik güncelleştirmeleri almak için cihazın İnternet bağlantısını kullanır. Bu dinamik güncelleştirmeler WSUS kullanımı için yayımlanmaz.
- **Evet** -dinamik güncelleştirmeyi etkinleştirilir.
- **Hayır** -dinamik güncelleştirmeyi devre dışı bırakır.


## <a name="state-messaging"></a>Durum mesajlaşma

### <a name="state-message-reporting-cycle-minutes"></a>Durum iletisi raporlama çevrimi (dakika)

İstemcilerin durum iletilerini ne sıklıkta raporacağını belirtir. Bu ayar varsayılan olarak 15 dakikadır.



## <a name="user-and-device-affinity"></a>Kullanıcı ve cihaz benzeşimi  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Kullanıcı cihaz benzeşimi kullanım eşiği (dakika)

Configuration Manager bir Kullanıcı cihaz benzeşimi eşlemesi oluşturmadan önce geçecek dakika sayısını belirtin. Varsayılan olarak, bu değer 2880 dakikadır (iki gün).

### <a name="user-device-affinity-usage-threshold-days"></a>Kullanıcı cihaz benzeşimi kullanım eşiği (gün)

İstemcinin, kullanım tabanlı cihaz benzeşimi eşiğini ölçtüğünden itibaren geçen gün sayısını belirtin. Varsayılan olarak, bu değer 30 gündür.

> [!NOTE]  
> Örneğin, **Kullanıcı cihaz benzeşimi kullanım eşiğini (dakika)** **60** dakika olarak ve **Kullanıcı cihaz benzeşimi kullanım eşiği (gün)** **5** gün olarak belirtirsiniz. Daha sonra Kullanıcı, cihazla otomatik benzeşim oluşturmak için cihazı 5 gün süresince 60 dakika boyunca kullanmalıdır.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Kullanıcı cihaz benzeşimlerini kullanım verilerinden otomatik olarak yapılandır

Configuration Manager topladığı kullanım bilgilerine göre otomatik Kullanıcı cihaz benzeşimi oluşturmak için **Evet** ' i seçin.  

### <a name="allow-user-to-define-their-primary-devices"></a>Kullanıcıların kendi birincil cihazlarını tanımlamalarına izin ver
<!--3485366-->
Bu ayar **Evet**olduğunda, kullanıcılar yazılım merkezi 'nde kendi birincil cihazlarını tanımlayabilir. Daha fazla bilgi için bkz. [Yazılım Merkezi Kullanıcı Kılavuzu](../../understand/software-center.md#work-information).

## <a name="windows-analytics"></a>Windows Analizi

> [!Important]  
> Windows Analytics hizmeti 31 Ocak 2020 itibariyle kullanımdan kaldırıldı. Daha fazla bilgi için bkz. [KB 4521815: Windows Analytics emekli on 31 ocak 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Masaüstü analizi, Windows Analytics 'in gelişmidir. Daha fazla bilgi için bkz. [Masaüstü analizi nedir?](../../../desktop-analytics/overview.md)
