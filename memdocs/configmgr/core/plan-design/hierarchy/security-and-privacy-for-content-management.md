---
title: İçerik yönetimi güvenliği ve gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager 'de içerik yönetimi için güvenliği ve gizliliği iyileştirin.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720859"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Configuration Manager 'de içerik yönetimi için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale Configuration Manager ' deki içerik yönetimi için güvenlik ve gizlilik bilgilerini içerir. 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> İçerik yönetimi için önerilen güvenlik uygulamaları  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>İntranet dağıtım noktaları için HTTPS veya HTTP 'nin avantajları ve dezavantajları
İntranetteki dağıtım noktaları için HTTPS ve HTTP kullanmanın olumlu ve olumsuz yönlerini göz önünde bulundurun. Çoğu senaryoda, yetkilendirme için HTTP ve paket erişim hesapları kullanmak, şifreleme ile HTTPS kullanmaktan daha fazla güvenlik sağlar, ancak yetkilendirme olmadan. Bununla birlikte, içeriğinizde aktarım sırasında şifrelemek istediğiniz gizli veriler varsa HTTPS kullanın.  

-   **Dağıtım noktası IÇIN https kullandığınızda**Configuration Manager, içeriğe erişim yetkisi vermek için paket erişim hesapları kullanmaz, ancak içerik ağ üzerinden aktarıldığında şifrelenir.  

-   **Bir dağıtım noktası IÇIN http kullandığınızda**, yetkilendirme için paket erişim hesaplarını kullanabilirsiniz, ancak içerik ağ üzerinden aktarıldığında şifrelenmez.  

Sürüm 1806 ' den başlayarak, site için **GELIŞMIŞ http** 'yi etkinleştirmeyi düşünün. Bu özellik, istemcilerin bir HTTP dağıtım noktasıyla güvenli iletişim kurmak için Azure Active Directory kimlik doğrulaması kullanmasına izin verir. Daha fazla bilgi için bkz. [GELIŞMIŞ http](enhanced-http.md).

#### <a name="protect-the-client-authentication-certificate-file"></a>İstemci kimlik doğrulama sertifikası dosyasını koruma
Dağıtım noktası için otomatik olarak imzalanan bir sertifika yerine PKI istemci kimlik doğrulama sertifikası kullanıyorsanız, sertifika dosyasını (.pfx) güçlü bir parola ile koruyun. Dosyayı ağda depolarsanız, dosyayı Configuration Manager içine aktardığınızda ağ kanalını güvenli hale getirin.

Dağıtım noktasının yönetim noktalarıyla iletişim kurmak için kullandığı istemci kimlik doğrulaması sertifikasını içeri aktarmak için parola istediğinizde bu yapılandırma, sertifikayı saldırgandan korumaya yardımcı olur. Bir saldırganın sertifika dosyası üzerinde değişiklik yapmasını engellemek için ağ konumu ile site sunucusu arasında sunucu Ileti bloğu (SMB) imzası veya IPSec kullanın.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Dağıtım noktası rolünü site sunucusundan kaldır
Configuration Manager Kurulum, varsayılan olarak site sunucusuna bir dağıtım noktası yüklüyor. İstemcilerin site sunucusuyla doğrudan iletişim kurması gerekmez. Saldırı yüzeyini azaltmak için, dağıtım noktası rolünü diğer site sistemlerine atayın ve site sunucusundan kaldırın.  

#### <a name="secure-content-at-the-package-access-level"></a>Paket erişim düzeyinde içerik güvenliğini sağlama
Dağıtım noktası paylaşma, tüm kullanıcılara okuma erişimi sağlar. İçeriğe erişebilen kullanıcıları sınırlandırmak amacıyla, dağıtım noktası HTTP için yapılandırıldığında paket erişim hesaplarını kullanın. Bu yapılandırma, paket erişim hesaplarını desteklemeyen bulut dağıtım noktaları için uygulanmaz. Daha fazla bilgi için bkz. [paket erişim hesapları](accounts.md#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Dağıtım noktası rolünde IIS 'yi yapılandırma
Dağıtım noktası site sistem rolü eklediğinizde Configuration Manager IIS 'yi yüklerse, dağıtım noktası yüklemesi tamamlandığında HTTP yeniden yönlendirme veya IIS Yönetim betikleri ve araçları 'nı kaldırın. Dağıtım noktası, HTTP yönlendirmesi veya IIS Yönetim betikleri ve araçları gerektirmez. Saldırı yüzeyini azaltmak için, Web sunucusu rolü için bu rol hizmetlerini kaldırın.  Dağıtım noktaları için Web sunucusu rolü rol hizmetleri hakkında daha fazla bilgi için bkz. [site ve site sistemi önkoşulları](../configs/site-and-site-system-prerequisites.md).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Paketi oluşturduğunuzda paket erişim izinlerini ayarlama
Paket dosyalarındaki erişim hesaplarında yapılan değişiklikler yalnızca paketi yeniden dağıttığınızda etkin hale geldiği için, paketi ilk oluşturduğunuzda paket erişim izinlerini dikkatli bir şekilde ayarlayın. Bu yapılandırma, paket büyük olduğunda veya çok sayıda dağıtım noktasına dağıtıldığında ve içerik dağıtımı için ağ bant genişliği kapasitesinin sınırlı olduğu durumlarda önemlidir.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Önceden hazırlanan içerik içeren medyayı korumak için erişim denetimleri uygulama
Önceden hazırlanan içerik sıkıştırılır, ancak şifrelenmez. Bir saldırgan cihazlara indirilen dosyaları okuyabilir ve değiştirebilir. Configuration Manager istemcileri ile değiştirilen içeriği reddeder, ancak yine de indirirler.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Önceden hazırlanan içeriği ExtractContent ile içeri aktarma
Yalnızca ExtractContent. exe komut satırı aracını kullanarak önceden hazırlanan içeriği içeri aktarın. Ayrıcalıkların izinsiz ve yükselmesine engel olmak için yalnızca Configuration Manager ile birlikte gelen yetkili komut satırı aracını kullanın.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Site sunucusu ve paket kaynak konumu arasındaki iletişim kanalının güvenliğini sağlama
Uygulamalar ve paketler oluşturduğunuzda, site sunucusu ve paket kaynak konumu arasında IPSec veya SMB imzası kullanın. Bu yapılandırma, bir saldırganın kaynak dosyaları izinsiz değişikliklere engel olmaya yardımcı olur.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Özel Web sitesi için varsayılan sanal dizinleri dağıtım noktası rolüyle kaldır
Site yapılandırma seçeneğini, bir dağıtım noktası rolü yüklendikten sonra varsayılan Web sitesi yerine özel bir Web sitesi kullanmak üzere değiştirirseniz varsayılan sanal dizinleri kaldırın. Varsayılan Web sitesinden özel bir Web sitesine geçtiğinizde, eski sanal dizinleri kaldırmaz Configuration Manager. Configuration Manager ilk olarak varsayılan Web sitesi altında oluşturulan aşağıdaki sanal dizinleri kaldırın:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Bulut dağıtım noktaları için, Azure abonelik ayrıntılarınızı ve sertifikalarınızı koruyun
Bulut dağıtım noktalarını kullandığınızda, aşağıdaki yüksek değerli öğeleri koruyun:
- Azure aboneliğiniz için Kullanıcı adı ve parola
- Azure Yönetim sertifikası 
- Bulut dağıtım noktası hizmet sertifikası

Sertifikaları güvenli bir şekilde depolayın. Bulut dağıtım noktasını yapılandırırken ağ üzerinden bunlara gözattığınızda, site sistem sunucusu ve kaynak konumu arasında IPSec veya SMB imzalama kullanın.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Hizmet sürekliliği için, bulut dağıtım noktası sertifikalarının bitiş tarihini izleyin
Bulut dağıtım noktası için içeri aktarılan sertifikaların kullanım süreleri sona ermek üzereyken Configuration Manager sizi uyarır. Bitiş tarihlerini Configuration Manager bağımsız olarak izleyin. Son Tarih tarihinden önce yeni sertifikaları yenilediğinizden ve içeri aktardığınızdan emin olun. Bu eylem, bir dış, ortak sağlayıcıdan bir sunucu kimlik doğrulama sertifikası elde ediyorsanız önemlidir, çünkü yenilenen bir sertifikayı almak için ek zaman gerekebilir.  

 Sertifikanın süresi dolarsa Cloud Services Yöneticisi **9425**durum iletisini oluşturur. CloudMgr. log dosyası, **süresi dolma**TARIHI de UTC olarak günlüğe kaydedilir.  



## <a name="security-considerations-for-content-management"></a>İçerik yönetimi için güvenlik değerlendirmeleri  

İçerik yönetimi için planlama yaparken aşağıdaki noktaları göz önünde bulundurun:  

-   İstemciler indirilene kadar içeriği doğrulamaz.  

     Configuration Manager istemcileri içerikte karma değeri yalnızca istemci önbelleğine indirildikten sonra doğrular. Bir saldırgan, indirilecek dosyaların listesini veya içeriğin kendisini içeren bir dosyayı kurcaıyorsa, yükleme işlemi, yalnızca istemcinin geçersiz karma ile karşılaştığında içeriği atması için önemli ölçüde ağ bant genişliği oluşturabilir.  

-   Bulut dağıtım noktalarını kullandığınızda içeriğe erişim otomatik olarak kurumla kısıtlıdır. Bunu seçili kullanıcı veya gruplarla daha fazla kısıtlayamazsınız.  

-   Bulut dağıtım noktalarını kullandığınızda, istemcilerin kimliği yönetim noktası tarafından doğrulanır ve ardından bulut dağıtım noktalarına erişmek için bir Configuration Manager belirteci kullanılır. Belirteç sekiz saat için geçerlidir. Bu davranış, istemci artık güvenilir olmadığı için bir istemciyi engellediğinizde bu belirtecin geçerlilik süresi sona erene kadar bir bulut dağıtım noktasından içerik indirmeye devam edebilir. Bu noktada, istemci engellendiğinden yönetim noktası istemci için başka bir belirteç vermez.  

     Engellenen bir istemcinin bu sekiz saatlik pencere içinde içerik indirmesinden kaçınmak için bulut hizmetini durdurun. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **bulut dağıtım noktaları** düğümünü seçin.  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> İçerik yönetimi için gizlilik bilgileri  

 Configuration Manager, bir yönetici kullanıcı bu eylemi yapmak üzere seçim yapabilse de, içerik dosyalarındaki hiçbir Kullanıcı verisi içermez.  



## <a name="see-also"></a>Ayrıca bkz.

- [İçerik yönetimi için temel kavramlar](fundamental-concepts-for-content-management.md)  

- [Uygulama yönetimi için güvenlik ve Gizlilik](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [Yazılım güncelleştirmeleri için güvenlik ve gizlilik](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [İşletim sistemi dağıtımı için güvenlik ve gizlilik](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
