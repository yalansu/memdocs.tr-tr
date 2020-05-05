---
title: Güvenlik temel ilkeleri
titleSuffix: Configuration Manager
description: Configuration Manager güvenlik katmanları hakkında bilgi edinin.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722840"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Configuration Manager için güvenliğin temelleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede, Configuration Manager ortamının aşağıdaki temel güvenlik bileşenleri özetlenmektedir:
- [Güvenlik katmanları](#bkmk_layers)
- [Rol tabanlı yönetim](#bkmk_rba)
- [İstemci uç noktalarını güvenli hale getirme](#bkmk_endpoints)
- [Configuration Manager hesapları ve grupları](#bkmk_accounts)
- [Gizlilik](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a>Güvenlik katmanları

Configuration Manager güvenliği aşağıdaki katmanlardan oluşur: 
- [Windows işletim sistemi ve ağ güvenliği](#bkmk_layer-windows)
- [Ağ altyapısı: güvenlik duvarları, yetkisiz giriş algılama, ortak anahtar altyapısı (PKI)](#bkmk_layer-network)
- [Configuration Manager Güvenlik denetimleri](#bkmk_layer-cm)
- [SMS sağlayıcısı](#bkmk_layer-provider)
- [Site veritabanı izinleri](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a>Windows işletim sistemi ve ağ güvenliği
İlk katman Windows güvenlik özellikleri tarafından hem işletim sistemi hem de ağ için sağlanır. Bu katman aşağıdaki bileşenleri içerir:  

-   Configuration Manager bileşenleri arasında dosyaları aktarmak için dosya paylaşımı  

-   Dosyaları ve kayıt defteri anahtarlarını güvenli hale getirmek için Erişim Denetim Listeleri (ACL'ler)  

-   İletişimleri güvenli hale getirmeye yardımcı olmak için Internet Protokolü güvenliği (IPSec)  

-   Güvenlik ilkesini ayarlamak için grup ilkesi  

-   Dağıtılmış uygulamalar için Configuration Manager konsolu gibi dağıtılmış bileşen nesne modeli (DCOM) izinleri  

-   Güvenlik ilkelerini depolamak için Active Directory Etki Alanı Hizmetleri  

-   Configuration Manager, kurulum sırasında oluşturduğu bazı grupları içeren Windows hesap güvenliği  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a>Ağ altyapısı

Güvenlik duvarları ve izinsiz giriş algılama gibi ek güvenlik bileşenleri, tüm ortam için savunma sağlamaya yardımcı olur. Endüstri standardı ortak anahtar altyapısı (PKI) uygulamaları tarafından verilen sertifikalar kimlik doğrulama, imzalama ve şifreleme sağlamaya yardımcı olur.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a>Configuration Manager Güvenlik denetimleri

Windows Server ve ağ altyapısı tarafından sunulan güvenliğe ek olarak, Configuration Manager konsoluna ve kaynaklarına erişimi birkaç şekilde denetler. Varsayılan olarak, yalnızca yerel Yöneticiler, Configuration Manager konsolunun yüklediğiniz bilgisayarlarda gerektirdiği dosya ve kayıt defteri anahtarları için haklara sahip olur.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a>SMS sağlayıcısı

Sonraki güvenlik katmanı, Windows Yönetim Araçları, özellikle de SMS Sağlayıcısı üzerinden erişime dayanır. SMS sağlayıcısı, kullanıcıya site veritabanını bilgi için sorgulama erişimi veren bir Configuration Manager bileşenidir. Varsayılan olarak, sağlayıcıya erişim, yerel SMS Yöneticileri grubunun üyeleriyle sınırlıdır. Bu grup ilk olarak yalnızca Configuration Manager yükleyen kullanıcıyı içerir. Diğer hesaplara Ortak Bilgi Modeli (CIM) deposu ve SMS Sağlayıcısı için izin vermek üzere diğer hesapları SMS Yöneticileri grubuna ekleyin.  

Sürüm 1810 ' den başlayarak, yöneticilerin Configuration Manager sitelere erişmesi için en düşük kimlik doğrulama düzeyini belirtebilirsiniz. Bu özellik, yöneticilerin Windows 'da gerekli düzeyiyle oturum açmasını zorlar. <!--1357013-->  

Daha fazla bilgi için bkz. [plan for SMS Provider](../plan-design/hierarchy/plan-for-the-sms-provider.md).

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a>Site veritabanı izinleri

Son güvenlik katmanı, site veritabanındaki nesneler için izinlere dayanır. Varsayılan olarak, Configuration Manager yüklemek için kullandığınız yerel sistem hesabı ve Kullanıcı hesabı, site veritabanındaki tüm nesneleri yönetebilir. Rol tabanlı yönetim kullanarak Configuration Manager konsolundaki ek Yönetici kullanıcılara izinler verin ve kısıtlayın.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a>Rol tabanlı yönetim  

 Configuration Manager koleksiyonlar, dağıtımlar ve siteler gibi nesnelerin güvenli hale getirilmesine yardımcı olmak için rol tabanlı yönetimi kullanır. Bu yönetim modeli, tüm site ve site ayarları için hiyerarşi genelindeki güvenlik erişim ayarlarını merkezi olarak tanımlar ve yönetir. 

 Yönetici, yönetici kullanıcılara ve grup izinlerine *güvenlik rolleri* atar. İzinler, örneğin, istemci ayarları oluşturmak veya değiştirmek için farklı Configuration Manager nesne türlerine bağlanır. 

 *Güvenlik kapsamları* , Microsoft Office yükleyen bir uygulama gibi bir yönetici kullanıcının yönetmekle sorumlu olduğu nesnelerin belirli örneklerini gruplar. 

 Güvenlik rollerinin, güvenlik kapsamlarının ve koleksiyonların birleşimi, bir yönetici kullanıcının görüntüleyebileceği ve yönetebileceği nesneleri tanımlar. Configuration Manager tipik yönetim görevleri için bazı varsayılan güvenlik rollerini yüklüyor. Belirli iş gereksinimlerinizi desteklemek için kendi güvenlik rollerinizi oluşturun.  

 Daha fazla bilgi için bkz. [rol tabanlı yönetimi yapılandırma](../servers/deploy/configure/configure-role-based-administration.md).  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a>İstemci uç noktalarını güvenli hale getirme  

 Configuration Manager, otomatik olarak imzalanan veya PKI sertifikaları ya da Azure Active Directory (Azure AD) belirteçleri kullanarak site sistem rolleriyle istemci iletişimini korur. Bazı senaryolarda PKI sertifikalarının kullanılması gerekir. Örneğin, [İnternet tabanlı istemci yönetimi](../clients/manage/plan-internet-based-client-management.md)ve [mobil cihaz istemcileri](../../mdm/plan-design/plan-on-premises-mdm.md)için.  

 İstemcilerin HTTPS veya HTTP istemci iletişimi için bağlandığı site sistem rollerini yapılandırabilirsiniz. İstemci bilgisayarları her zaman, mevcut en güvenli yöntemi kullanarak iletişim kurar. İstemci bilgisayarlar yalnızca HTTP iletişimine izin veren site sistemleri rolleriniz varsa, daha az güvenli iletişim yöntemini kullanmaya geri döner.  

 Daha fazla bilgi için bkz. [güvenlik Için plan](../plan-design/security/plan-for-security.md).



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a>Configuration Manager hesapları ve grupları  

 Configuration Manager, çoğu site işlemi için yerel sistem hesabını kullanır. Bazı yönetim görevleri için ek hesap oluşturmanız ve bakım yapmanız gerekebilir. Configuration Manager, kurulum sırasında birkaç varsayılan grup ve SQL Server rolü oluşturur. Bilgisayar veya Kullanıcı hesaplarını varsayılan gruplara ve SQL Server rollere el ile eklemeniz gerekebilir.  

 Daha fazla bilgi için bkz. [Configuration Manager kullanılan hesaplar](../plan-design/hierarchy/accounts.md).  



## <a name="privacy"></a><a name="bkmk_privacy"></a>Gizliliğinin  

 Configuration Manager uygulamadan önce gizlilik gereksinimlerinizi göz önünde bulundurun. Kurumsal Yönetim ürünleri, çok sayıda istemciyi etkin bir şekilde yönetebildikleri için birçok avantaj sunmakla birlikte, bu yazılım kuruluşunuzdaki kullanıcıların gizliliğini etkileyebilir. Configuration Manager, verileri toplamak ve cihazları izlemek için birçok araç içerir. Bazı araçlar, kuruluşunuzda gizlilik sorunları oluşturabilir.  

 Örneğin, Configuration Manager istemcisini yüklediğinizde, varsayılan olarak birçok yönetim ayarı etkinleştirilir. Bu yapılandırma, istemci yazılımının Configuration Manager sitesine bilgi göndermesini sağlar. Site, istemci bilgilerini site veritabanında depolar. İstemci bilgileri doğrudan Microsoft 'a gönderilmez. Daha fazla bilgi için bkz. [Tanılama ve kullanım verileri](../plan-design/diagnostics/diagnostics-and-usage-data.md).



## <a name="see-also"></a>Ayrıca bkz.

- [Güvenliği planlama](../plan-design/security/plan-for-security.md)  

- [Configuration Manager istemcileri için güvenlik ve Gizlilik](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Güvenliği yapılandırma](../plan-design/security/configure-security.md)   

- [Uç noktalar arasında iletişim](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Şifreleme denetimleri teknik başvurusu](../plan-design/security/cryptographic-controls-technical-reference.md)  
