---
title: Sertifika profillerine giriş
titleSuffix: Configuration Manager
description: Configuration Manager 'deki Sertifika profillerinin Active Directory Sertifika hizmetleriyle nasıl çalıştığını öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 35269e7c727031a9cd66072985f3d9ec362978cf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722308"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Configuration Manager 'da sertifika profillerine giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sertifika profilleri Active Directory Sertifika Hizmetleri ve ağ cihazı kayıt hizmeti (NDES) rolüyle çalışır. Kullanıcıların kuruluş kaynaklarına kolayca erişebilmeleri için yönetilen cihazlar için kimlik doğrulama sertifikaları oluşturun ve dağıtın. Örneğin, kullanıcıların VPN ve kablosuz bağlantılara bağlanması için gerekli sertifikaları sağlamak üzere sertifika profilleri oluşturabilir ve dağıtabilirsiniz.

Sertifika profilleri, Wi-Fi ağları ve VPN sunucuları gibi kuruluş kaynaklarına erişmek için Kullanıcı cihazlarını otomatik olarak yapılandırabilir. Kullanıcılar, sertifikaları el ile yüklemeden veya bant dışı bir işlem kullanmadan bu kaynaklara erişebilir. Ortak anahtar altyapınız (PKI) tarafından desteklenen daha güvenli ayarlar kullanabileceğinizden sertifika profilleri, kaynakların güvenliğini sağlamaya yardımcı olur. Örneğin, yönetilen cihazlarda gerekli sertifikaları dağıttığınız için tüm Wi-Fi ve VPN bağlantıları için sunucu kimlik doğrulaması gerektir.

Sertifika profilleri aşağıdaki yönetim yeteneklerini sağlar:  

- Farklı işletim sistemi türlerini ve sürümlerini çalıştıran cihazlar için bir sertifika yetkilisinden (CA) sertifika kaydı ve yenileme. Bu sertifikalar daha sonra Wi-Fi ve VPN bağlantıları için kullanılabilir.  

- Güvenilen kök CA sertifikalarının ve ara CA sertifikalarının dağıtımı. Bu sertifikalar, sunucu kimlik doğrulaması gerektiğinde VPN ve Wi-Fi bağlantıları için cihazlarda bir güven zinciri yapılandırır.  

- Yüklü sertifikaları izleme ve sertifikalar hakkında rapor gönderme.  

**Örnek 1**: tüm çalışanların birden fazla ofis konumunda Wi-Fi etkin noktalarına bağlanması gerekir. Kolay Kullanıcı bağlantısını etkinleştirmek için önce Wi-Fi ' a bağlanmak için gereken sertifikaları dağıtın. Ardından, sertifikaya başvuran Wi-Fi profillerini dağıtın.  

**Örnek 2**: BIR PKI 'sı vardır. Sertifika dağıtmaya yönelik daha esnek ve güvenli bir yönteme geçmek istiyorsunuz. Kullanıcıların güvenliği tehlikeye atmadan şirket kaynaklarına kendi kişisel cihazlarından erişmesi gerekir. Sertifika profillerini, belirli cihaz platformu için desteklenen ayarlar ve protokollerle yapılandırın. Cihazlar daha sonra otomatik olarak bu sertifikaları internet 'e yönelik bir kayıt sunucusundan isteyebilir. Daha sonra, cihazın kuruluş kaynaklarına erişebilmesi için VPN profillerini bu sertifikaları kullanacak şekilde yapılandırın.  

## <a name="types"></a>Türler

Üç tür sertifika profili vardır:  

- **GÜVENILEN CA sertifikası**: güvenilen BIR kök CA veya ara CA sertifikası dağıtın. Bu sertifikalar, cihazın bir sunucu kimliğini doğrulaması gerektiğinde bir güven zinciri oluşturur.  

- **Basit sertifika kayıt Protokolü (SCEP)**: SCEP protokolünü kullanarak bir cihaz veya Kullanıcı için sertifika isteyin. Bu tür, Windows Server 2012 R2 veya üstünü çalıştıran bir sunucuda ağ cihazı kayıt hizmeti (NDES) rolünü gerektirir.

    **Basit sertifika kayıt Protokolü (SCEP)** sertifika profili oluşturmak için önce BIR **Güvenilen CA sertifika** profili oluşturun.

- **Kişisel bilgi değişimi (. pfx)**: bir cihaz veya Kullanıcı için bir. pfx (PKCS #12 olarak da bilinir) sertifikası isteyin.<!--1321368--> PFX Sertifika profilleri oluşturmak için iki yöntem vardır:

  - Mevcut sertifikalardan [kimlik bilgilerini Içeri aktarma](../../mdm/deploy-use/import-pfx-certificate-profiles.md)
  - İstekleri işlemek için [bir sertifika yetkilisi tanımlama](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

  > [!Note]  
  > Configuration Manager varsayılan olarak bu isteğe bağlı özelliği etkinleştirmez. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

  **Kişisel bilgi değişimi (. pfx)** sertifikaları için Microsoft veya Entrust sertifika yetkilileri olarak kullanabilirsiniz.

## <a name="requirements"></a>Gereksinimler

SCEP kullanan sertifika profillerini dağıtmak için, sertifika kayıt noktasını bir site sistemi sunucusuna yükler. Ayrıca, Windows Server 2012 R2 veya üstünü çalıştıran bir sunucuda NDES için Configuration Manager Ilke modülünü bir ilke modülü de yükler. Bu sunucu Active Directory Sertifika Hizmetleri rolü gerektirir. Ayrıca, sertifikaları gerektiren cihazların erişebileceği çalışan bir NDES de gerektirir. Cihazlarınızın internet 'ten sertifikalara kaydolması gerekiyorsa, NDES sunucunuza internet 'ten erişilebilir olması gerekir. Örneğin, internet 'ten NDES sunucusuna giden trafiği güvenle etkinleştirmek için [Azure uygulama proxy 'si](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)kullanabilirsiniz.

PFX sertifikaları bir sertifika kayıt noktası da gerektirir. Ayrıca sertifika için sertifika yetkilisini (CA) ve ilgili erişim kimlik bilgilerini belirtin. Sertifika yetkilisi olarak Microsoft veya Entrust belirtebilirsiniz.  

NDES 'nin sertifikaları dağıtabilmesi için bir ilke Configuration Manager modülünü nasıl desteklediği hakkında daha fazla bilgi için, bkz. [ağ cihazı kayıt hizmeti Ile Ilke modülü kullanma](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\)).

Gereksinimlere bağlı olarak, Configuration Manager çeşitli cihaz türlerindeki ve işletim sistemlerindeki farklı sertifika depolarına sertifika dağıtılmasını destekler. Şu cihazlar ve işletim sistemleri desteklenir:  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> Windows Phone 8,1 ve Windows 10 Mobile 'ı yönetmek için şirket içi MDM Configuration Manager kullanın. Daha fazla bilgi için bkz. [Şirket ıçı MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Configuration Manager için tipik bir senaryo, Wi-Fi ve VPN sunucuları için kimlik doğrulaması yapmak üzere güvenilen kök CA sertifikaları yüklemektir. Tipik bağlantılar aşağıdaki protokolleri kullanır:

- Kimlik doğrulama protokolleri: EAP-TLS, EAP-TTLS ve PEAP
- VPN tünel protokolleri: Ikev2, L2TP/IPSec ve Cisco IPSec

Cihazın bir SCEP sertifika profili kullanarak sertifikaları isteyebilmesi için önce bir kuruluş kök CA sertifikası yüklü olmalıdır.  

Farklı ortamlar veya bağlantı gereksinimleri için özelleştirilmiş sertifikalar istemek üzere bir SCEP sertifika profilinde ayarları belirtebilirsiniz. **Sertifika profili oluşturma Sihirbazı** , kayıt parametreleri için iki sayfa içerir. Birincisi, **SCEP Kaydı**, kayıt isteği ve sertifikanın nereye yükleneceği ile ilgili ayarları içerir. İkinci sayfa olan **Sertifika Özellikleri**, istenen sertifikanın kendisini açıklar.  

## <a name="deploy"></a>Dağıtma

Bir SCEP sertifika profili dağıttığınızda Configuration Manager istemci ilkeyi işler. Daha sonra yönetim noktasından bir SCEP sınama parolası ister. Cihaz bir ortak/özel anahtar çifti oluşturur ve bir sertifika imzalama isteği (CSR) oluşturur. Bu istek NDES sunucusuna gönderilir. NDES sunucusu, isteği NDES ilke modülü aracılığıyla sertifika kayıt noktası site sistemine iletir. Sertifika kayıt noktası isteği doğrular, SCEP sınama parolasını denetler ve isteğin ile oynanmadığını doğrular. Ardından, isteği onaylar veya reddeder. Onaylanırsa, NDES sunucusu imzalama isteğini imzalama için bağlı sertifika yetkilisine (CA) gönderir. CA isteği imzalar ve sertifikayı istenen cihaza döndürür.

Sertifika profillerini Kullanıcı veya cihaz koleksiyonlarına dağıtın. Her sertifika için hedef depoyu belirtebilirsiniz. Uygulanabilirlik kuralları, cihazın sertifikayı yükleyip yükleyemeyeceğini belirtir.

Bir sertifika profilini bir kullanıcı koleksiyonuna dağıttığınızda, [Kullanıcı cihaz benzeşimi](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) , kullanıcıların cihazlarının sertifikaları yükleyeceğini belirler. Bir sertifika profilini bir kullanıcı sertifikasıyla bir cihaz koleksiyonuna dağıttığınızda, varsayılan olarak kullanıcıların birincil cihazlarının her biri sertifikaları yükler. Sertifikayı kullanıcıların cihazlarına yüklemek için **sertifika profili oluşturma Sihirbazı**'Nın **SCEP Kaydı** sayfasında bu davranışı değiştirin. Cihazlar bir çalışma grubundaysa, Configuration Manager Kullanıcı sertifikaları dağıtmaz.  

## <a name="monitor"></a>İzleme

Uyumluluk sonuçlarını veya raporları görüntüleyerek, sertifika profili dağıtımlarını izleyebilirsiniz. Daha fazla bilgi için bkz. [sertifika profillerini izleme](monitor-certificate-profiles.md).

## <a name="automatic-revocation"></a>Otomatik iptal

Configuration Manager, aşağıdaki durumlarda sertifika profilleri kullanılarak dağıtılan Kullanıcı ve bilgisayar sertifikalarını otomatik olarak iptal eder:  

- Cihaz Configuration Manager yönetiminden kullanımdan kaldırıldı.  

- Cihaz Configuration Manager hiyerarşisinden engellendi.  

Sertifikaları iptal etmek için site sunucusu, sertifikayı veren sertifika yetkilisine bir iptal komutu gönderir. İptal işleminin sebebi **İşlemin Sona Ermesi**'dir.

> [!NOTE]
> Bir sertifikayı düzgün bir şekilde iptal etmek için hiyerarşideki en üst düzey sitenin bilgisayar hesabı, CA 'da **sertifika verme ve yönetme** iznine sahip olmalıdır.
>
> Gelişmiş güvenlik için CA 'daki CA yöneticilerini de kısıtlayabilirsiniz. Ardından, bu hesaba yalnızca sitedeki SCEP profilleri için kullandığınız belirli sertifika şablonunda izin verin.

## <a name="next-steps"></a>Sonraki adımlar

- [Sertifika profilleri oluşturma](create-certificate-profiles.md)

- [Sertifika altyapısını yapılandırma](certificate-infrastructure.md)
