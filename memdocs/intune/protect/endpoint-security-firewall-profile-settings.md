---
title: Intune Endpoint Security Güvenlik Duvarı ayarları | Microsoft Docs
description: Windows ve macOS için uç nokta güvenlik güvenlik duvarı ilke ayarları Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/21/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 9b6af399d0f3fbd721932b47e8f1bc388711ca58
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814721"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için güvenlik duvarı ilke ayarları

Bir [uç nokta güvenlik ilkesinin](../protect/endpoint-security-policy.md)parçası olarak, Intune 'un uç nokta güvenlik düğümündeki *güvenlik duvarı* için profiller ilkesi içinde yapılandırabileceğiniz ayarları görüntüleyin.

Desteklenen platformlar ve profiller:

- **macOS**:
  - Profil: **MacOS güvenlik duvarı**

- **Windows 10 ve üzeri**:
  - Profil: **Microsoft Defender güvenlik duvarı**

## <a name="macos-firewall-profile"></a>macOS güvenlik duvarı profili

### <a name="firewall"></a>Güvenlik Duvarı

Aşağıdaki ayarlar [macOS güvenlik duvarları Için Endpoint Security ilkesi](../protect/endpoint-security-firewall-policy.md) olarak yapılandırılır

- **Güvenlik duvarını etkinleştir**

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -güvenlik duvarını etkinleştirin.
  
  *Evet*olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz.  

  - **Tüm gelen bağlantıları engelleme**

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -DHCP, Bonjour ve IPSec gibi temel Internet Hizmetleri için gerekli olan bağlantılar hariç tüm gelen bağlantıları engelleyin. Bu, tüm paylaşım hizmetlerini engeller.

  - **Gizli modu etkinleştir**

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -bilgisayarın yoklama isteklerine yanıt vermesini engelleyin. Bilgisayar, yetkili uygulamalardan gelen istekleri yanıtlamaya devam eder.

  - **Güvenlik duvarı uygulamaları** Açılan listeyi genişletin ve ardından **Ekle** ' yi seçin ve ardından uygulama için gelen bağlantılara yönelik uygulamaları ve kuralları belirtin.
    - **Gelen bağlantılara izin ver**
      - Yapılandırılmamış
      - Blok
      - İzin Ver

    - **Paket kimliği** -kimliği, uygulamayı tanımlar. Örneğin: *com. Apple. app*

## <a name="microsoft-defender-firewall-profile"></a>Microsoft Defender güvenlik duvarı profili

### <a name="microsoft-defender-firewall"></a>Microsoft Defender güvenlik duvarı

Aşağıdaki ayarlar, [Windows 10 güvenlik duvarları Için Endpoint Security ilkesi](../protect/endpoint-security-firewall-policy.md)olarak yapılandırılır.

- **Durum bilgisi olan Dosya Aktarım Protokolü (FTP)**  
  CSP: [Mdmstore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Yapılandırılmadı** (*varsayılan*)
  - **Izin ver** -güvenlik duvarı, ikincil bağlantılara izin vermek için durum bilgisi olan Dosya Aktarım Protokolü (FTP) filtrelemesi gerçekleştirir. 
  - **Devre dışı** -durum BILGISI olan FTP devre dışı.

- **Bir güvenlik ilişkisinin silinmeden önce boşta kalabileceği saniye sayısı**  
  CSP: [Mdmstore/Global/Saıdsaati](https://go.microsoft.com/fwlink/?linkid=872539)

  Ağ trafiğinden sonra güvenlik ilişkilerinin ne kadar süreyle tutulacağını öğrenmek için, 300 ile 3600 arasındaki süreyi saniye cinsinden belirtin.
  
  Herhangi bir değer belirtmezseniz, sistem 300 saniye boyunca boşta kaldıktan sonra bir güvenlik ilişkilendirmesini siler.
  
- **Önceden paylaşılan anahtar kodlaması**  
  CSP: [Mdmstore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  *UTF-8*gerekmiyorsa, önceden PAYLAŞıLMıŞ anahtarlar UTF-8 kullanılarak kodlanır. Bundan sonra cihaz kullanıcıları başka bir kodlama yöntemi seçebilirler.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Hiçbiri**
  - **UTF8**

- **Güvenlik Duvarı IP 'si için muafiyet yok**  
  - **Yapılandırılmadı** (*varsayılan*)-yapılandırılmadığında, tek tek yapılandırabileceğiniz aşağıdaki IP sn muafiyet ayarlarına erişebilirsiniz.
  - **Evet** -tüm GÜVENLIK duvarı IP sn muafiyetlerini devre dışı bırakın. Aşağıdaki ayarlar yapılandırmak için kullanılamaz.

  - **Güvenlik Duvarı IP sn muafiyetleri komşu bulmaya izin ver**  
    CSP: [Mdmstore/Global/ıpsecmuaf muafiyet](https://go.microsoft.com/fwlink/?linkid=872547)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -güvenlik duvarı IPSec muafiyetleri komşu bulmayı sağlar.

  - **Güvenlik Duvarı IP sn muafiyetleri ıCMP 'ye izin ver**  
    CSP: [Mdmstore/Global/ıpsecmuaf muafiyet](https://go.microsoft.com/fwlink/?linkid=872547)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -güvenlik duvarı IPSec MUAFIYETLERI ICMP 'ye izin verir.

  - **Güvenlik Duvarı IP sn muafiyetleri yönlendirici bulmaya izin ver**  
    CSP: [Mdmstore/Global/ıpsecmuaf muafiyet](https://go.microsoft.com/fwlink/?linkid=872547)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -güvenlik duvarı IPSec muafiyetleri yönlendirici bulmaya izin verir.

  - **Güvenlik Duvarı IP sn muafiyetleri DHCP 'ye izin ver**  
    CSP: [Mdmstore/Global/ıpsecmuaf muafiyet](https://go.microsoft.com/fwlink/?linkid=872547)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -GÜVENLIK duvarı IP sn MUAFIYETLERI DHCP 'ye izin ver

- **Sertifika iptal listesi (CRL) doğrulaması**  
  CSP: [Mdmstore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Sertifika iptal listesi (CRL) doğrulamanın nasıl uygulanacağını belirtin.
  - **Yapılandırılmadı** (*varsayılan*)-CRL doğrulamasını devre dışı bırakmak için varsayılan istemci varsayılanını kullanın.
  - **Hiçbiri**
  - **Girişimde**
  - **Gerektirme**

- **Anahtar modüllerinin yalnızca desteklemediği kimlik doğrulama paketlerini yoksaymasını gerektir**  
  CSP: [Mdmstore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Yapılandırılmadı** (*varsayılan*)
  - **Devre dışı**
  - **Etkin** anahtar modülleri desteklenmeyen kimlik doğrulama paketlerini yoksayar.

- **Paket Kuyruklama**  
  CSP: [Mdmstore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  IPSec tüneli ağ geçidi senaryosunda şifrelenmiş alma ve şifresiz metin iletme için alma tarafında yazılım ölçeklendirmesinin nasıl etkinleştirileceğini belirtin. Bu, paket sırasının korunmasını sağlar.
  - **Yapılandırılmadı** (*varsayılan*)-paket Kuyruklama, varsayılan olarak devre dışı olan istemci varsayılana döndürülür.
  - **Devre dışı**
  - **Gelen kuyruk**
  - **Giden kuyruk**
  - **Her Ikisini de kuyruğa al**

- **Etki alanı ağları için Microsoft Defender güvenlik duvarını açma**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Yapılandırılmadı** (*varsayılan*)-istemci, güvenlik duvarını etkinleştirecek olan varsayılan değerini döndürür.
  - **Evet** - **etki alanının** ağ türü Için Microsoft Defender güvenlik duvarı açılıp zorlanır. Ayrıca, bu ağ için ek ayarlara erişim elde edersiniz.
  - **Hayır** -güvenlik duvarını devre dışı bırakın.

  Bu ağ için ek ayarlar, *Evet*olarak ayarlandığında:

  - **Gizli modu engelle**  
    CSP: [Disablestealthmode](https://go.microsoft.com/fwlink/?linkid=872559)

    Varsayılan olarak, cihazlar üzerinde gizli mod etkinleştirilmiştir. Kötü amaçlı kullanıcıların ağ cihazları ve çalıştırdığı hizmetlerle ilgili bilgileri bulmasını önlemeye yardımcı olur. Gizli modu devre dışı bırakmak, cihazların saldırıya açık olmasını sağlayabilir.
    - **Yapılandırılmadı** *(varsayılan)*
    - **Evet**
    - **Hayır**

  - **Korumalı modu etkinleştir**  
    CSP: [korumalı](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Yapılandırılmadı** *(varsayılan)* -korumalı modu devre dışı bırakmak için varsayılan istemci varsayılanını kullanın.
    - **Evet** -makine, ağ üzerinden yalıtan, *korumalı moda*konur. Tüm trafik engellenir.
    - **Hayır**

  - **Çok noktaya yayın yayınlarına tek noktaya yayın yanıtlarını engelleyin**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, tek noktaya yayın yanıtlarına izin veren istemci varsayılan değerini döndürür.
    - **Evet** -çok noktaya yayın yayınlarına tek noktaya yayın yanıtları engellenir.
    - , **Tek noktaya** yayın yanıtlarına izin vermek olan istemci varsayılanını zorunlu kılmaz.

  - **Gelen bildirimleri devre dışı bırak**  
    CSP [Disableınboundnotifications](https://go.microsoft.com/fwlink/?linkid=872563)
    - **Yapılandırılmadı** *(varsayılan)* -ayar, kullanıcı bildirimine izin veren istemci varsayılan değerini döndürür.
    - **Evet** -bir uygulama bir gelen kural tarafından engellendiğinde Kullanıcı bildirimi bastırılır.
    - **No** Kullanıcı bildirimlerine izin verilmez.

  - **Giden bağlantıları engelle**  

    *Bu ayar Windows sürüm 1809 ve üzeri için geçerlidir*.
    CSP: [Defaultoutboundavction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    Bu kural, kural listesinin en sonunda değerlendirilir.
    - **Yapılandırılmadı** *(varsayılan)* -ayar, bağlantılara izin vermek olan istemci varsayılan değerini döndürür.
    - **Evet** -giden bir kuralla eşleşmeyen tüm giden bağlantılar engellenir.
    - **Hayır** -giden bir kuralla eşleşmeyen tüm bağlantılara izin verilir.

  - **Gelen bağlantıları engelle**  
    CSP: [Defaulınboundadction](https://go.microsoft.com/fwlink/?linkid=872564)

    Bu kural, kural listesinin en sonunda değerlendirilir.
    - **Yapılandırılmadı** *(varsayılan)* -ayar, bağlantıları engelleyecek olan istemci varsayılan değerini döndürür.
    - **Evet** -bir gelen kuralla eşleşmeyen tüm gelen bağlantılar engellenir.
    - **Hayır** -bir gelen kuralla eşleşmeyen tüm bağlantılara izin verilir.

  - **Yetkili uygulama güvenlik duvarı kurallarını yoksay**  
    CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki yetkili uygulama güvenlik duvarı kuralları yok sayılır.
    - **No** Yetkili uygulama güvenlik duvarı kuralları kabul edilemez.

  - **Genel bağlantı noktası güvenlik duvarı kurallarını yoksay**  
    CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki genel bağlantı noktası güvenlik duvarı kuralları yok sayılır.
    - **Hayır** -genel bağlantı noktası güvenlik duvarı kuralları kabul edilir.

  - **Tüm yerel güvenlik duvarı kurallarını yoksay**  
    CSP: [ıpsecmuaf muafiyet](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki tüm güvenlik duvarı kuralları yok sayılır.
    - **Hayır** -yerel depodaki güvenlik duvarı kuralları kabul edilir.

  - **Bağlantı güvenlik kurallarını yoksay** CSP: [Allowlocalıpsecpolicymerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki IPSec güvenlik duvarı kuralları yok sayılır.
    - **No** Yerel depoda IPSec güvenlik duvarı kuralları kabul edilemez.

- **Özel ağlar için Microsoft Defender güvenlik duvarını Aç**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Yapılandırılmadı** (*varsayılan*)-istemci, güvenlik duvarını etkinleştirecek olan varsayılan değerini döndürür.
  - **Evet** - **özel** ağ türü Için Microsoft Defender güvenlik duvarı açıktır ve zorlanır. Ayrıca, bu ağ için ek ayarlara erişim elde edersiniz.
  - **Hayır** -güvenlik duvarını devre dışı bırakın.

  Bu ağ için ek ayarlar, *Evet*olarak ayarlandığında:

  - **Gizli modu engelle**  
    CSP: [Disablestealthmode](https://go.microsoft.com/fwlink/?linkid=872559)

    Varsayılan olarak, cihazlar üzerinde gizli mod etkinleştirilmiştir. Kötü amaçlı kullanıcıların ağ cihazları ve çalıştırdığı hizmetlerle ilgili bilgileri bulmasını önlemeye yardımcı olur. Gizli modu devre dışı bırakmak, cihazların saldırıya açık olmasını sağlayabilir.
    - **Yapılandırılmadı** *(varsayılan)*
    - **Evet**
    - **Hayır**

  - **Korumalı modu etkinleştir**  
    CSP: [korumalı](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Yapılandırılmadı** *(varsayılan)* -korumalı modu devre dışı bırakmak için varsayılan istemci varsayılanını kullanın.
    - **Evet** -makine, ağ üzerinden yalıtan, *korumalı moda*konur. Tüm trafik engellenir.
    - **Hayır**

  - **Çok noktaya yayın yayınlarına tek noktaya yayın yanıtlarını engelleyin**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, tek noktaya yayın yanıtlarına izin veren istemci varsayılan değerini döndürür.
    - **Evet** -çok noktaya yayın yayınlarına tek noktaya yayın yanıtları engellenir.
    - , **Tek noktaya** yayın yanıtlarına izin vermek olan istemci varsayılanını zorunlu kılmaz.

  - **Gelen bildirimleri devre dışı bırak**  
    CSP [Disableınboundnotifications](https://go.microsoft.com/fwlink/?linkid=872563)
    - **Yapılandırılmadı** *(varsayılan)* -ayar, kullanıcı bildirimine izin veren istemci varsayılan değerini döndürür.
    - **Evet** -bir uygulama bir gelen kural tarafından engellendiğinde Kullanıcı bildirimi bastırılır.
    - **No** Kullanıcı bildirimlerine izin verilmez.

  - **Giden bağlantıları engelle**  

    *Bu ayar Windows sürüm 1809 ve üzeri için geçerlidir*.
    CSP: [Defaultoutboundavction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    Bu kural, kural listesinin en sonunda değerlendirilir.
    - **Yapılandırılmadı** *(varsayılan)* -ayar, bağlantılara izin vermek olan istemci varsayılan değerini döndürür.
    - **Evet** -giden bir kuralla eşleşmeyen tüm giden bağlantılar engellenir.
    - **Hayır** -giden bir kuralla eşleşmeyen tüm bağlantılara izin verilir.

  - **Gelen bağlantıları engelle**  
    CSP: [Defaulınboundadction](https://go.microsoft.com/fwlink/?linkid=872564)

    Bu kural, kural listesinin en sonunda değerlendirilir.
    - **Yapılandırılmadı** *(varsayılan)* -ayar, bağlantıları engelleyecek olan istemci varsayılan değerini döndürür.
    - **Evet** -bir gelen kuralla eşleşmeyen tüm gelen bağlantılar engellenir.
    - **Hayır** -bir gelen kuralla eşleşmeyen tüm bağlantılara izin verilir.

  - **Yetkili uygulama güvenlik duvarı kurallarını yoksay**  
    CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki yetkili uygulama güvenlik duvarı kuralları yok sayılır.
    - **No** Yetkili uygulama güvenlik duvarı kuralları kabul edilemez.

  - **Genel bağlantı noktası güvenlik duvarı kurallarını yoksay**  
    CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki genel bağlantı noktası güvenlik duvarı kuralları yok sayılır.
    - **Hayır** -genel bağlantı noktası güvenlik duvarı kuralları kabul edilir.

  - **Tüm yerel güvenlik duvarı kurallarını yoksay**  
    CSP: [ıpsecmuaf muafiyet](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki tüm güvenlik duvarı kuralları yok sayılır.
    - **Hayır** -yerel depodaki güvenlik duvarı kuralları kabul edilir.

  - **Bağlantı güvenlik kurallarını yoksay** CSP: [Allowlocalıpsecpolicymerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki IPSec güvenlik duvarı kuralları yok sayılır.
    - **No** Yerel depoda IPSec güvenlik duvarı kuralları kabul edilemez.

- **Ortak ağlar için Microsoft Defender güvenlik duvarını açma**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Yapılandırılmadı** (*varsayılan*)-istemci, güvenlik duvarını etkinleştirecek olan varsayılan değerini döndürür.
  - **Evet** - **genel** ağ türü Için Microsoft Defender güvenlik duvarı açıktır ve zorlanır. Ayrıca, bu ağ için ek ayarlara erişim elde edersiniz.
  - **Hayır** -güvenlik duvarını devre dışı bırakın.

  Bu ağ için ek ayarlar, *Evet*olarak ayarlandığında:

  - **Gizli modu engelle**  
    CSP: [Disablestealthmode](https://go.microsoft.com/fwlink/?linkid=872559)

    Varsayılan olarak, cihazlar üzerinde gizli mod etkinleştirilmiştir. Kötü amaçlı kullanıcıların ağ cihazları ve çalıştırdığı hizmetlerle ilgili bilgileri bulmasını önlemeye yardımcı olur. Gizli modu devre dışı bırakmak, cihazların saldırıya açık olmasını sağlayabilir.
    - **Yapılandırılmadı** *(varsayılan)*
    - **Evet**
    - **Hayır**

  - **Korumalı modu etkinleştir**  
    CSP: [korumalı](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Yapılandırılmadı** *(varsayılan)* -korumalı modu devre dışı bırakmak için varsayılan istemci varsayılanını kullanın.
    - **Evet** -makine, ağ üzerinden yalıtan, *korumalı moda*konur. Tüm trafik engellenir.
    - **Hayır**

  - **Çok noktaya yayın yayınlarına tek noktaya yayın yanıtlarını engelleyin**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, tek noktaya yayın yanıtlarına izin veren istemci varsayılan değerini döndürür.
    - **Evet** -çok noktaya yayın yayınlarına tek noktaya yayın yanıtları engellenir.
    - , **Tek noktaya** yayın yanıtlarına izin vermek olan istemci varsayılanını zorunlu kılmaz.

  - **Gelen bildirimleri devre dışı bırak**  
    CSP [Disableınboundnotifications](https://go.microsoft.com/fwlink/?linkid=872563)
    - **Yapılandırılmadı** *(varsayılan)* -ayar, kullanıcı bildirimine izin veren istemci varsayılan değerini döndürür.
    - **Evet** -bir uygulama bir gelen kural tarafından engellendiğinde Kullanıcı bildirimi bastırılır.
    - **No** Kullanıcı bildirimlerine izin verilmez.

  - **Giden bağlantıları engelle**  

    *Bu ayar Windows sürüm 1809 ve üzeri için geçerlidir*.
    CSP: [Defaultoutboundavction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    Bu kural, kural listesinin en sonunda değerlendirilir.
    - **Yapılandırılmadı** *(varsayılan)* -ayar, bağlantılara izin vermek olan istemci varsayılan değerini döndürür.
    - **Evet** -giden bir kuralla eşleşmeyen tüm giden bağlantılar engellenir.
    - **Hayır** -giden bir kuralla eşleşmeyen tüm bağlantılara izin verilir.

  - **Gelen bağlantıları engelle**  
    CSP: [Defaulınboundadction](https://go.microsoft.com/fwlink/?linkid=872564)

    Bu kural, kural listesinin en sonunda değerlendirilir.
    - **Yapılandırılmadı** *(varsayılan)* -ayar, bağlantıları engelleyecek olan istemci varsayılan değerini döndürür.
    - **Evet** -bir gelen kuralla eşleşmeyen tüm gelen bağlantılar engellenir.
    - **Hayır** -bir gelen kuralla eşleşmeyen tüm bağlantılara izin verilir.

  - **Yetkili uygulama güvenlik duvarı kurallarını yoksay**  
    CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki yetkili uygulama güvenlik duvarı kuralları yok sayılır.
    - **No** Yetkili uygulama güvenlik duvarı kuralları kabul edilemez.

  - **Genel bağlantı noktası güvenlik duvarı kurallarını yoksay**  
    CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki genel bağlantı noktası güvenlik duvarı kuralları yok sayılır.
    - **Hayır** -genel bağlantı noktası güvenlik duvarı kuralları kabul edilir.

  - **Tüm yerel güvenlik duvarı kurallarını yoksay**  
    CSP: [ıpsecmuaf muafiyet](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki tüm güvenlik duvarı kuralları yok sayılır.
    - **Hayır** -yerel depodaki güvenlik duvarı kuralları kabul edilir.

  - **Bağlantı güvenlik kurallarını yoksay** CSP: [Allowlocalıpsecpolicymerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Yapılandırılmadı** *(varsayılan)* -ayar, yerel kuralları kabul etmek için olan istemci varsayılan değerini döndürür.
    - **Evet** -yerel depodaki IPSec güvenlik duvarı kuralları yok sayılır.
    - **No** Yerel depoda IPSec güvenlik duvarı kuralları kabul edilemez.

### <a name="microsoft-defender-firewall-rules"></a>Microsoft Defender güvenlik duvarı kuralları

*Bu profil önizlemededir*.

Aşağıdaki ayarlar, [Windows 10 güvenlik duvarları Için Endpoint Security ilkesi](../protect/endpoint-security-firewall-policy.md)olarak yapılandırılır.

#### <a name="windows-firewall-rule"></a>Windows güvenlik duvarı kuralı

- **Ad**  
  Kuralınız için bir kolay ad belirtin. Bu ad, bu adı belirlemenize yardımcı olacak kurallar listesinde görünür.

- **Açıklama**  
  Kural için bir açıklama sağlayın.

- **Yön**  
  - **Yapılandırılmadı** (*varsayılan*)-Bu kural varsayılan olarak giden trafiğe göre yapılır.
  - **Out** -bu kural giden trafik için geçerlidir.
  - Bu kural **,** gelen trafik için geçerlidir.

- **Eylem**  
  - **Yapılandırılmadı** (*varsayılan*)-kural, trafiğe izin verecek şekilde varsayılan olur.
  - **Engellenmiş** -trafik yapılandırdığınız *yönde* engellenir.
  - **Izin verilen** trafik, yapılandırdığınız *yönde* izin verilir.

- **Ağ türü**  
  Kuralın ait olduğu ağ türünü belirtin. Aşağıdakilerden birini veya birkaçını seçebilirsiniz. Bir seçenek seçmezseniz, kural tüm ağ türlerine uygulanır.
  - **Etki alanı**
  - **Özelleştirme**
  - **Geneldir**
  - **Yapılandırılmadı**

- **Paket ailesi adı**  
  [Get-AppxPackage](/previous-versions//hh856044(v=technet.10))

  Paket aile adları, PowerShell 'den Get-AppxPackage komutu çalıştırılarak alınabilir.

- **Dosya yolu**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](/windows/client-management/mdm/firewall-csp#filepath)

  Bir uygulamanın dosya yolunu belirtmek için, istemci cihazında uygulamalar konumunu girin. Örneğin: `C:\Windows\System\Notepad.exe` veya `%WINDIR%\Notepad.exe`

- **Hizmet adı**  
  [FirewallRules/FirewallRuleName/App/ServiceName](/windows/client-management/mdm/firewall-csp#servicename)

  Bir uygulama değil, trafik gönderirken veya alırken bir Windows hizmeti kısa adı kullanın. Hizmet kısa adları, `Get-Service` PowerShell 'den komut çalıştırılarak alınır.

- **Protokol**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](/windows/client-management/mdm/firewall-csp#protocol)

  Bu bağlantı noktası kuralı için protokolü belirtin.
  - *TCP (6)* ve *UDP (17)* gibi aktarım katmanı protokolleri, bağlantı noktalarını veya bağlantı noktası aralıklarını belirtmenize olanak tanır.
  - Özel protokoller için IP protokolünü temsil eden *0* ile *255* arasında bir sayı girin.
  - Hiçbir şey belirtilmediğinde kural varsayılan olarak **herhangi bir**olur.

- **Arabirim türleri**  
  Kuralın ait olduğu arabirim türlerini belirtin. Aşağıdakilerden birini veya birkaçını seçebilirsiniz. Bir seçenek seçmezseniz, kural tüm arabirim türlerine uygulanır:
  - **Uzaktan erişim**
  - **Kablosuz**
  - **Yerel alan ağı**
  - **Yapılandırılmadı**

- **Yetkili kullanıcılar**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Bu kural için yetkili yerel kullanıcıların bir listesini belirtin. Bu ilkedeki *hizmet adı* bir Windows hizmeti olarak ayarlandıysa yetkili kullanıcıların listesi belirtilemez. Yetkili Kullanıcı belirtilmemişse, varsayılan olarak *tüm kullanıcılar*' dır.

- **Herhangi bir yerel adres**  
  **Yapılandırılmadı** (*varsayılan*)-destekedilecek bir adres aralığını yapılandırmak Için aşağıdaki ayarı ve *Yerel adres aralıklarını*kullanın.
  - **Evet** -herhangi bir yerel adresi destekler ve bir adres aralığı yapılandırmayın.

- **Yerel adres aralıkları**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Bu kural için yerel adres aralıklarını yönetin. Seçenekleriniz şunlardır:
  - Kuralın kapsadığı yerel adreslerin virgülle ayrılmış bir listesi olarak bir veya daha fazla adres **ekleyin** .
  - Yerel adres aralıkları olarak kullanılacak adreslerin listesini içeren bir. csv dosyasını **Içeri aktarın** .
  - Geçerli yerel adres aralıkları listenizi bir. csv dosyası olarak **dışarı aktarın** .

  Geçerli girişler (belirteçler) aşağıdaki seçenekleri içerir:
  - **Bir yıldız işareti** ( \* ) herhangi bir yerel adresi belirtir. Varsa, yıldız işareti dahil edilen tek belirteç olmalıdır.
  - **Alt ağ-alt** ağ maskesini veya ağ öneki gösterimini kullanarak alt ağları belirtin. Bir alt ağ maskesi veya ağ öneki belirtilmemişse, alt ağ maskesi varsayılan olarak 255.255.255.255 olur.
  - **Geçerli bir IPv6 adresi**
  - **IPv4 adres aralığı** -IPv4 aralıkları, boşluk dahil olmayan *Başlangıç adresi-bitiş adresi* biçiminde olmalıdır; burada başlangıç adresi bitiş adresinden daha küçüktür.
  - **IPv6 adres aralığı** -IPv6 aralıkları, boşluk dahil olmayan *Başlangıç adresi-bitiş adresi* biçiminde olmalıdır; burada başlangıç adresi bitiş adresinden daha küçüktür.

  Hiçbir değer belirtilmediğinde, bu ayar varsayılan olarak *herhangi bir adresi*kullanır.

- **Herhangi bir uzak adres**  
  **Yapılandırılmadı** (*varsayılan*)-destekedilecek bir adres aralığını yapılandırmak Için aşağıdaki ayarı, *uzak adres aralıklarını** kullanın.
  - **Evet** -herhangi bir uzak adresi destekler ve bir adres aralığı yapılandırmayın.

- **Uzak adres aralıkları**  
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Bu kural için uzak adres aralıklarını yönetin. Seçenekleriniz şunlardır:
  - Kuralın kapsadığı uzak adreslerin virgülle ayrılmış bir listesi olarak bir veya daha fazla adres **ekleyin** .
  - Uzak adres aralıkları olarak kullanılacak adreslerin listesini içeren bir. csv dosyasını **Içeri aktarın** .
  - Geçerli uzak adres aralıkları listenizi bir. csv dosyası olarak **dışarı aktarın** .

  Geçerli girişler (belirteçler) aşağıdakileri içerir ve büyük/küçük harfe duyarlı değildir:
  - **Bir yıldız işareti** (), \* herhangi bir uzak adresi belirtir. Varsa, yıldız işareti dahil edilen tek belirteç olmalıdır.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** -Windows 1809 veya üstünü çalıştıran cihazlarda desteklenir.
  - **Rmtıntranet** -Windows 1809 veya üstünü çalıştıran cihazlarda desteklenir.
  - **Ply2Renders** -Windows 1809 veya üstünü çalıştıran cihazlarda desteklenir.
  - **LocalSubnet** -yerel alt ağdaki herhangi bir yerel adresi belirtir.
  - **Alt ağ-alt** ağ maskesini veya ağ öneki gösterimini kullanarak alt ağları belirtin. Bir alt ağ maskesi veya ağ öneki belirtilmemişse, alt ağ maskesi varsayılan olarak 255.255.255.255 olur.
  - **Geçerli bir IPv6 adresi**
  - **IPv4 adres aralığı** -IPv4 aralıkları, boşluk dahil olmayan *Başlangıç adresi-bitiş adresi* biçiminde olmalıdır; burada başlangıç adresi bitiş adresinden daha küçüktür.
  - **IPv6 adres aralığı** -IPv6 aralıkları, boşluk dahil olmayan *Başlangıç adresi-bitiş adresi* biçiminde olmalıdır; burada başlangıç adresi bitiş adresinden daha küçüktür.

  Hiçbir değer belirtilmediğinde, bu ayar varsayılan olarak *herhangi bir adresi*kullanır.

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>Sonraki adımlar

[Güvenlik duvarları için uç nokta güvenlik ilkesi](../protect/endpoint-security-firewall-policy.md)