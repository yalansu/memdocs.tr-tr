---
title: Technical Preview 1609 ' deki yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1609 ' de teknik önizlemede bulunan özellikler hakkında bilgi edinin.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05ed0daf56275b2e0ed46b2f9dd93fd66eb360be
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995543"
---
# <a name="capabilities-in-technical-preview-1609-for-configuration-manager"></a>Configuration Manager için Technical Preview 1609 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*



Bu makalede, sürüm 1609 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Configuration Manager Technical Preview sitenize yeni yetenekler eklemek ve güncelleştirmek için yükleyebilirsiniz.      Technical Preview 'un bu sürümünü yüklemeden önce, teknik önizleme kullanımıyla ilgili genel gereksinimleri ve sınırlamaları öğrenmek, sürümler arasında güncelleştirme yapmak ve teknik Önizlemedeki özelliklerle ilgili geri bildirim sağlamak için tanıtım konusunu gözden geçirin [Configuration Manager](../../core/get-started/technical-preview.md).    

**Bu teknik önizlemede bilinen sorunlar:**  
*  Configuration Manager 1609 Technical Preview sürümüne güncelleştirdiğinizde, dağıttığınız herhangi bir sürüm yükseltme ilkesi silinir. Bu ilkeleri kullanmaya devam etmek için bunları yeniden oluşturup dağıtmanız gerekir.


**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  

## <a name="improvements-to-endpoint-protection"></a>Endpoint Protection geliştirmeleri
Kötü amaçlı yazılımdan koruma ilkesi ayarlarını Endpoint Protection geliştirme-artık Endpoint Protection bulut koruma hizmeti 'nin şüpheli dosyaları engelleyebileceği düzeyi belirtebilirsiniz. Yeni bir ayar, yöneticilerin karşılaştığı çok sayıda kötü amaçlı yazılımı temel alarak "riskli" bilgisayarları belirtmesini sağlar.

## <a name="increased-number-of-enrolled-devices"></a>Daha fazla kayıtlı cihaz sayısı
Yöneticiler artık kullanıcıların Intune ile karma mobil cihaz yönetiminde 15 ' e kadar cihaz kaydetmelerini sağlayabilir. Sınır, Kullanıcı başına 5 cihazlıydı.

## <a name="additional-apple-dep-settings"></a>Ek Apple DEP ayarları

Yöneticiler artık iOS ve Mac cihazları için DEP profilinde aşağıdaki Apple Aygıt Kayıt Programı (DEP) ayarlarını yapılandırabilir:
- **Touch ID**
- **Zoom**
- **Siri**

Etkinleştirilirse, Apple 'ın Kurulum Yardımcısı bu hizmeti cihaz etkinleştirme sırasında ister.

## <a name="integration-with-upgrade-analytics"></a>Upgrade Analytics ile tümleştirme

Upgrade Analytics, daha kolay ve daha sorunsuz yükseltmeler sağlamak için cihaz hazırlığını değerlendirmenizi ve Windows 10 ile uyumluluğunu incelemenize olanak sağlar. Upgrade Analytics Configuration Manager ile tümleştirmeyle, Configuration Manager yönetim konsolundaki yükseltme uyumluluğu verilerine erişebilir ve sonra cihaz listesinden, yükseltme veya düzeltme için hedef cihazları kullanabilirsiniz.


## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Windows 10 VPN karma profilleri için yerel bağlantı türleri

Intune ile Configuration Manager kullanırken, artık Configuration Manager konsolundaki OMA-URI kullanmadan Microsoft otomatik, Ikev2, PPTP ve L2TP bağlantı türleriyle Windows 10 VPN profilleri oluşturabilirsiniz.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Iş için Windows Mağazası 'nda Configuration Manager ile tümleştirme geliştirmeleri

Bu sürümde, bu yeni özelliklerle [iş Için Windows Mağazası tümleştirmesini](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) güncelleştirdik:

**Güncelleştirme:** Geçerli Technical Preview sürümünde anında eşitleme özelliği işlevsel değildir.

- Daha önce Iş için Windows Mağazası 'ndan ücretsiz uygulamalar dağıtabilirsiniz. Artık Configuration Manager, ücretli çevrimiçi lisanslanmış uygulamalar (yalnızca Intune 'A kayıtlı cihazlar için) dağıtılmasını da desteklemektedir.
- Artık Iş için Windows Mağazası ve Configuration Manager arasında anında eşitleme başlatabilirsiniz.
- Artık Azure Active Directory aldığınız istemci gizli anahtarını değiştirebilirsiniz

### <a name="try-it-out"></a>Deneyin!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Ücretli bir çevrimiçi lisanslı uygulamayı satın alıp eşitleyin

1. Iş için Windows Mağazası 'ndan ücretli bir çevrimiçi lisanslı uygulama satın alın.
2. Configuration Manager konsolunun **Yönetim** çalışma alanında, **Cloud Services**güncelleştirmeler ' e tıklayın  >  **ve**  >  **iş için Windows Mağazası**' na bakım yapın.
3. **Giriş** sekmesinde, **Eşitle** grubunda, **Şimdi Eşitle**' ye tıklayın.
4. Daha sonra, satın aldığınız uygulama, **uygulama yönetimi** çalışma alanının **Mağaza uygulamaları için lisans bilgileri** düğümünde görünür.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Eşitlenmiş uygulama verilerinden bir Configuration Manager uygulaması oluşturma ve dağıtma

Ücretli mağaza uygulamasından bir Configuration Manager uygulaması oluşturma ve dağıtma yordamı, ücretsiz bir uygulamadan uygulama oluşturma ile aynıdır. [Configuration Manager Ile iş Için Windows Mağazası 'ndan uygulamaları yönetme](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)bölümündeki bir **Iş için windows Mağazası uygulamasından Configuration Manager uygulaması oluşturma ve dağıtma** bölümüne bakın.


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Azure Active Directory istemci gizli anahtarını değiştirme

1. Configuration Manager konsolunun **Yönetim** çalışma alanında, **Cloud Services**güncelleştirmeler ' e tıklayın  >  **ve**  >  **iş için Windows Mağazası**' na bakım yapın.
2. Iş için Windows Mağazası hesabınızı seçin ve ardından **Özellikler**' e tıklayın.
3. **İş Için Windows Mağazası hesap özellikleri** iletişim kutusunda, **istemci gizli anahtarı** alanına yeni bir anahtar girin ve ardından **Doğrula**' ya tıklayın. Doğrulandıktan sonra **Uygula**' ya tıklayın ve iletişim kutusunu kapatın.


## <a name="new-compliance-settings-for-configuration-items"></a>Yapılandırma öğeleri için yeni uyumluluk ayarları

Çeşitli cihaz platformları için yapılandırma öğelerinde kullanabileceğiniz pek çok yeni ayar ekledik.
Bunlar, bir tek başına yapılandırmada Microsoft Intune daha önce var olan ve Intune 'U Configuration Manager ile kullandığınızda kullanılabilir olan ayarlardır.
Bu ayarlardan herhangi biriyle ilgili yardıma ihtiyacınız varsa, [Microsoft Intune ilkeleriyle cihazlarınızda ayarları ve özellikleri yönetin](../../../intune/configuration/device-profiles.md) ' i açın ve istediğiniz platformun ayarlar alt konusunu seçin.


### <a name="new-settings-for-android-devices"></a>Android cihazları için yeni ayarlar

#### <a name="password-settings"></a>Parola ayarları

- **Parola geçmişini anımsa**
- **Parmak izi ile kilit açmaya izin ver**

#### <a name="security-settings"></a>Güvenlik ayarları

- **Depolama kartlarında şifreleme iste**
- **Ekran yakalamaya izin ver**
- **Tanılama verilerinin gönderimine izin ver**

#### <a name="browser-settings"></a>Tarayıcı ayarları

- **Web tarayıcısına izin ver**
- **Otomatik doldurmaya izin ver**
- **Açılır pencere engelleyicisine izin ver**
- **Tanımlama bilgilerine izin ver**
- **Etkin betik yazmaya izin ver**

#### <a name="app-settings"></a>Uygulama ayarları

- **Google Play mağazasına izin ver**

#### <a name="device-capability-settings"></a>Cihaz özelliği ayarları

- **Çıkarılabilir depolama birimine izin ver**
- **Wi-Fi İnternet paylaşımına izin ver**
- **Coğrafi konuma izin ver**
- **NFC'ye izin ver**
- **Bluetooth'a izin ver**
- **Ses dolaşımına izin ver**
- **Veri dolaşımına izin ver**
- **SMS/MMS iletilerine izin ver**
- **Sesli yardıma izin ver**
- **Sesli aramaya izin ver**
- **Kopyalama ve yapıştırmaya izin ver**


### <a name="new-settings-for-ios-devices"></a>İOS cihazları için yeni ayarlar

#### <a name="password-settings"></a>Parola ayarları

- **Parolada gerekli karmaşık karakter sayısı**
- **Basit parolalara izin ver**
- **Parola gerekmeden önce etkin olmama süresi (dakika)**
- **Parola geçmişini anımsa**

### <a name="new-settings-for-mac-os-x-devices"></a>Mac OS X cihazları için yeni ayarlar

#### <a name="password-settings"></a>Parola ayarları

- **Parolada gerekli karmaşık karakter sayısı**
- **Basit parolalara izin ver**
- **Parola geçmişini anımsa**
- **Ekran koruyucu etkinleştirilmeden önce işlem yapılmadan geçen süre**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Windows 10 Masaüstü ve mobil cihazlar için yeni ayarlar

#### <a name="password-settings"></a>Parola ayarları

- **Minimum karakter kümesi sayısı**
- **Parola geçmişini anımsa**
- **Cihaz boş bir durumdan döndürüldüğünde parola iste**

#### <a name="security-settings"></a>Güvenlik ayarları

- **Cihazda şifrelemeyi gerektir**
- **Elle kayıt kaldırmaya izin ver**

#### <a name="device-capability-settings"></a>Cihaz özelliği ayarları

- **Hücresel veri üzerinden VPN'ye izin ver**
- **Hücresel veri üzerinden VPN dolaşımına izin ver**
- **Telefon sıfırlamaya izin ver**
- **USB bağlantısına izin ver**
- **Cortana’ya izin ver**
- **İşlem merkezi bildirimlerine izin ver**

### <a name="new-settings-for-windows-10-team-devices"></a>Windows 10 Team cihazları için yeni ayarlar

#### <a name="device-settings"></a>Cihaz ayarları

- **Azure Operasyonel İçgörüler'i etkinleştir**
- **Miracast kablosuz projektörü etkinleştir**
- **Karşılama ekranında görüntülenen toplantı bilgilerini seçin**
- **Kilit ekranı arka plan görüntüsü URL'si**


### <a name="new-settings-for-windows-81-devices"></a>Windows 8.1 cihazları için yeni ayarlar

#### <a name="applicability-settings"></a>Uygulanabilirlik ayarları

- **Tüm yapılandırmaları Windows 10'a uygula**

#### <a name="password-settings"></a>Parola ayarları

- **Gerekli parola türü**
- **Minimum karakter kümesi sayısı**
- **Minimum parola uzunluğu**
- **Cihaz silinmeden önce izin verilen yinelenen oturum açma hatası sayısı**
- **Ekran kapanmadan önce işlem yapılmadan geçen dakika sayısı**
- **Parola geçerlilik süresi (gün)**
- **Parola geçmişini anımsa**
- **Önceki parolaların yeniden kullanılmasını engelleme**
- **Resimli parolaya veya PIN’e izin ver**

#### <a name="browser-settings"></a>Tarayıcı ayarları

- **İntranet ağının otomatik algılanmasına izin ver**


### <a name="new-settings-for-windows-phone-81-devices"></a>Windows Phone 8,1 cihazları için yeni ayarlar

#### <a name="applicability-settings"></a>Uygulanabilirlik ayarları

- **Tüm yapılandırmaları Windows 10'a uygula**

#### <a name="password-settings"></a>Parola ayarları

- **Minimum karakter kümesi sayısı**
- **Basit parolalara izin ver**
- **Parola geçmişini anımsa**

#### <a name="device-capability-settings"></a>Cihaz özelliği ayarları

- **Ücretsiz Wi-Fi etkin noktalarına otomatik olarak bağlanmaya izin ver**


## <a name="improvements-for-boundary-groups"></a>Sınır grupları geliştirmeleri
Bu önizleme, sınır gruplarında önemli değişiklikleri ve bunların dağıtım noktalarıyla nasıl çalıştığını açıklar. Bu değişiklikler, içerik altyapısının tasarımını kolaylaştırmaya yardımcı olur. bu sayede, istemcilerin ek dağıtım noktalarını içerik kaynak konumları olarak aramak için nasıl ve ne zaman geri dönüş konusunda daha fazla denetim sağlarsınız. Bu, hem şirket içi hem de bulut tabanlı dağıtım noktaları içerir.

Bu geliştirmeler, bugün (dağıtım noktalarını hızlı veya yavaş olacak şekilde yapılandırma gibi) bildiğiniz kavramların ve davranışların yerini alır ve bunları kurmak ve sürdürmek daha kolay olan yeni bir modelle değiştirir. Bu değişiklikler Ayrıca, sınır gruplarıyla ilişkilendirdiğiniz diğer site sistem rollerini iyileştirecek sonraki değişiklikler için de aynı şekilde çalışır.  

Güncelleştirme, 1609 sürümüne yükseltme sırasında geçerli sınır grubu yapılandırmalarınızı yeni modele uyacak şekilde dönüştürerek, bu değişiklikler içerik dağıtım yapılandırmalarınızı rahatsız etmez (bkz. [var olan sınır gruplarını yeni modele güncelleştirme](capabilities-in-technical-preview-1609.md#bkmk_update)).

Aşağıdaki bölümlerde, bu önizleme ile tanıtılan değişiklikler, yeni modelin nasıl çalıştığı ve zaten sınır grupları yapılandırılmış olan bir siteyi yükseltirken neler tahmin edebileceğiniz açıklanır.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Sınır grupları ve içerik konumları için Kullanıcı arabirimi ve davranıştaki değişiklikler
Sınır gruplarında yapılan önemli değişiklikler ve istemcilerin içerik bulma yöntemleri aşağıda verilmiştir. Bu değişikliklerin ve kavramların birçoğu birlikte çalışır.
- **Hızlı veya yavaş yapılandırma işlemleri kaldırılır:** Artık tek tek dağıtım noktalarını hızlı veya yavaş olacak şekilde yapılandıramazsınız.  Bunun yerine, bir sınır grubuyla ilişkilendirilmiş her site sistemi aynı şekilde değerlendirilir. Bu değişiklik nedeniyle, sınır grubu özelliklerinin **Başvurular** sekmesi artık hızlı veya yavaş yapılandırmayı desteklememektedir.
- **Her sitede yeni varsayılan sınır grubu:**  Her birincil sitenin ***varsayılan-site-sınır grubu \<sitecode> ***adlı yeni bir varsayılan sınır grubu vardır.  İstemci, bir sınır grubuna atanan bir ağ konumunda olmadığında, bu istemci, atanmış sitesinden varsayılan grupla ilişkili site sistemlerini kullanır. Bu sınır grubunu, geri dönüş içerik konumu kavramının yerini alarak kullanmayı planlayın.    
  -  **' İçerik için geri dönüş kaynak konumlarına Izin ver '** kaldırıldı: artık geri dönüş için kullanılacak bir dağıtım noktasını açıkça yapılandırmayın ve bunu ayarlama seçenekleri kullanıcı arabiriminden kaldırılır.

  Ayrıca, istemcilerin uygulama için dağıtım türündeki **içerik için bir geri dönüş kaynak konumu kullanmasına Izin ver** ayarının sonucu değişmiştir. Dağıtım türündeki bu ayar artık istemcinin varsayılan site sınır grubunu içerik kaynağı konumu olarak kullanmasına olanak sağlar.

  -  **Sınır grupları ilişkileri:** Her sınır grubu, bir veya daha fazla ek sınır grubuna bağlanabilir. Bu bağlantılar, **ilişkiler**adlı yeni sınır grubu özellikleri sekmesinde yapılandırılan ilişkileri oluşturur:
  -   Bir istemcinin doğrudan ilişkilendirildiği her sınır grubuna **geçerli** bir sınır grubu denir.  
  -   İstemcinin *geçerli* sınır grubu ve başka bir gruba **komşu** sınır grubu olarak adlandırılan bir ilişki nedeniyle istemci bir sınır grubu tarafından kullanılabilir.
  -  Bu, bir *komşu* sınır grubu olarak kullanılabilecek sınır grupları eklediğiniz **ilişkiler** sekmesindedir. Ayrıca, *geçerli* gruptaki bir dağıtım noktasından içerik bulamamaları başarısız olan bir istemcinin, bu *komşu* sınır gruplarından içerik konumlarında arama yapmaya başlayabileceğini belirleyen bir süre yapılandırabilirsiniz.

      Bir sınır grubu yapılandırması eklediğinizde veya değiştirirken, yapılandırdığınız geçerli gruptan bu belirli sınır grubuna geri dönüşü engelleme seçeneğine sahip olursunuz.

  Yeni yapılandırmayı kullanmak için, bir sınır grubundan diğerine açık ilişkiler (bağlantılar) tanımlarsınız ve bu ilişkili gruptaki tüm dağıtım noktalarını dakikalar içinde aynı zamana göre yapılandırırsınız. Yapılandırdığınız zaman, *geçerli* sınır grubundan içerik kaynağı bulamadığında bir istemcinin, bu komşu sınır grubundan içerik kaynaklarını aramaya başlayabileceğini belirler.

  Açıkça yapılandırdığınız sınır gruplarının yanı sıra, her sınır grubu, varsayılan site sınır grubuna yönelik örtülü bir bağlantıya sahiptir. Bu bağlantı, varsayılan site sınır grubu, istemcilerin bu sınır grubuyla ilişkili dağıtım noktalarını içerik kaynak konumları olarak kullanmasına izin veren bir komşu sınır grubu haline geldiği zaman 120 dakika sonra etkin hale gelir.

  Bu davranış, daha önce içeriğe geri dönüş olarak adlandırılan nelerin yerini alır.  Varsayılan site sınır grubunu *geçerli* bir grupla doğrudan ilişkilendirerek ve belirli bir saati dakikalar içinde ayarlayarak veya kullanımını engellemek için tamamen geri dönüşü engelleyerek 120 dakikalık bu varsayılan davranışı geçersiz kılabilirsiniz.


- **İstemciler her dağıtım noktasından 2 dakikaya kadar içerik almaya çalışır:** İstemci bir içerik kaynak konumunu aradığında, daha sonra başka bir dağıtım noktası denemeden önce her bir dağıtım noktasına 2 dakika boyunca erişmeyi dener. Bu, istemcilerin bir dağıtım noktasına 2 saate kadar bağlanmaya çalıştığı önceki sürümlerden yapılan bir değişikdir.

  - Bir istemcinin kullanmaya çalıştığı ilk dağıtım noktası, istemcinin *geçerli* sınır grubundaki (veya gruplardaki) kullanılabilir dağıtım noktaları havuzundan rastgele seçilir.

  - İki dakika sonra istemci içerik bulmadığından, yeni bir dağıtım noktasına geçer ve bu sunucudan içerik almaya çalışır. Bu işlem, istemci içeriği bulana veya havuzundaki son sunucuya ulaşana kadar her iki dakikada bir yinelenir.

  - Bir istemci, bir *komşu* sınır grubuna geri dönüş dönemine ulaşılmadan önce *geçerli* havuzundan geçerli bir içerik kaynağı konumu bulamazsa, istemci o *komşu* grubundaki dağıtım noktalarını geçerli listesinin sonuna ekler ve ardından her iki sınır grubundan dağıtım noktalarını içeren genişletilmiş kaynak konumları grubunu arar.

      > [!TIP]  
      > Geçerli sınır grubundan varsayılan site sınır grubuna açık bir bağlantı oluşturduğunuzda ve bir komşu sınır grubuna bir bağlantı için geri dönüş zamanından daha az bir geri dönüş süresi tanımladığınızda, istemciler, komşu grubunu eklemeden önce varsayılan site sınırı grubundan kaynak konumları aramaya başlar.

  - İstemci, havuzdaki son sunucudan içerik alabilmek için işlemi yeniden başlatır.


### <a name="how-the-new-model-works"></a>Yeni modelin nasıl çalıştığı
Sınır gruplarını yapılandırırken, sınırları (ağ konumları) ve dağıtım noktaları gibi site sistem rollerini sınır grubuna ilişkilendirirsiniz. Bu, istemcilerin ağdaki istemcilerin yakınında yer alan dağıtım noktaları gibi site sistem sunucularına bağlantı sağlanmasına yardımcı olur.   
- Aynı sınırı birden fazla sınır grubuna atayabilirsiniz
- Dağıtım noktaları gibi site sistem sunucuları, birden fazla sınır grubu ile ilişkilendirilebilir ve bunları daha geniş bir ağ konumu aralığı için kullanılabilir hale getirebilirsiniz
- Bir dağıtım noktası bir sınır grubuyla ilişkilendirilmediği takdirde, istemciler bu dağıtım noktasını içerik kaynağı konumu olarak kullanamaz.

Bu Technical Preview sürümünden itibaren, içerik kaynak konumları için geri dönüş davranışını yapılandırmak üzere sınır grubu ilişkileri tanımlarsınız. Bu yeni davranış, sınır grubu özelliklerinin yeni **ilişkiler** sekmesinde yapılandırılır ve site sistemlerinin yavaş veya hızlı bir şekilde yapılandırılmasını ve bir sınır grubunun içerik için geri dönüş kaynak konumuna izin verecek şekilde yapılandırılmasını değiştirir.

Ilişkiler sekmesinde, diğer sınır gruplarını ekleyerek bu gruplarla bir ilişki yapılandırabilirsiniz. Her ilişki **geçerli** sınır grubundan, **komşu**olarak adlandırılan sınır grubuna tek yönlü bir bağlantıdır. Oluşturduğunuz her bağlantı için, dağıtım noktalarını dakikalar içinde bir geri dönüş süresi ile yapılandırabilirsiniz. Bu süre, *geçerli sınır grubundaki istemcilerin geçerli sınır grubundan* geçerli bir içerik kaynak konumu bulamadıklarında, *komşu* sınır grubundaki istemcilerin dağıtım noktalarını ne kadar süreyle kullanmaya başlayabilecekleri hakkında bilgi almak için kullanılır.

İstemci içerik bulamadığında ve komşu sınır gruplarından konumları aramaya başladığında, bu istemci için kullanılabilir dağıtım noktaları havuzunu denetimli bir şekilde arttırır.  

- Sınır grubu birden fazla Ilişkiye sahip olabilir. Bu, farklı komşulara geri dönüş yapılandırmanıza olanak tanır.
- İstemciler yalnızca geçerli sınır grubunun doğrudan komşusu olan bir sınır grubuna geri dönüş yapılır.
- Bir istemci birden fazla sınır grubunun üyesi olduğunda, geçerli sınır grubu, tüm istemci sınır gruplarının birleşimi olarak tanımlanır.  Bu istemci daha sonra bu orijinal sınır gruplarının herhangi birinin bir komşusuyla geri dönüş yapabilir.

Tanımladığınız bağlantılara ek olarak, oluşturduğunuz sınır grupları ve her site için otomatik olarak oluşturulan varsayılan sınır grubu arasında otomatik olarak oluşturulan bir örtülü bağlantı vardır. Bu otomatik bağlantı:
- , Hiyerarşinizdeki herhangi bir sınır grubuyla ilişkili bir sınır üzerinde olmayan istemciler tarafından kullanılır geçerli içerik kaynak konumlarını tanımlamak için varsayılan sınır grubunu atanan sitesinden otomatik olarak kullanın.   
-  , Geçerli sınır grubundan 120 dakika sonra kullanılan siteler varsayılan sınır grubuna varsayılan bir geri dönüş seçeneğidir.

**Yeni modeli kullanma örneği:** Sınırları veya site sistemi sunucularını paylaşmayan üç sınır grubu oluşturursunuz:
- Grup BG_A dağıtım noktaları DP_A1 ve grupla ilişkili DP_A2
- Grup BG_B dağıtım noktaları DP_B1 ve grupla ilişkili DP_B2
- Grup BG_C dağıtım noktaları DP_C1 ve grupla ilişkili DP_C2

İstemcilerinizin ağ konumlarını sınır olarak yalnızca BG_A sınır grubuna eklersiniz ve ardından o sınır grubundaki ilişkileri diğer iki sınır grubuna yapılandırırsınız:
- 10 dakika sonra kullanılacak ilk *komşu* grubu (BG_B) için dağıtım noktalarını yapılandırırsınız. Bu grup DP_B1 ve DP_B2 dağıtım noktalarını içerir. Her ikisi de ilk gruplar sınır konumlarına bağlıdır.
- İkinci *komşu* grubunu (BG_C) 20 dakika sonra kullanılacak şekilde yapılandırırsınız. Bu grup DP_C1 ve DP_C2 dağıtım noktalarını içerir. Her ikisi de diğer iki sınır grubundan bir WAN üzerinden yapılır.
- Ayrıca, site sunucusunda bulunan ek bir dağıtım noktasını siteler varsayılan site sınır grubuna eklersiniz. Bu, en az tercih ettiğiniz içerik kaynağı konumudur, ancak tüm sınır gruplarınız için merkezi olarak bulunur.

  Sınır grupları ve geri dönüş süreleri örneği:

  ![BG_Fallack](media/BG_Fallback.png)


Bu yapılandırmayla:
- İstemci, *geçerli* sınır grubundaki (BG_A) dağıtım noktalarından içerik aramaya başlar ve her bir dağıtım noktasını, sınır grubundaki bir sonraki dağıtım noktasına geçmeden önce iki dakika boyunca arayın. Geçerli içerik kaynak konumlarının istemci havuzu DP_A1 ve DP_A2 içerir.
- İstemci, 10 dakika aramadan sonra *geçerli* sınır grubundan içerik bulamazsa, dağıtım noktalarını BG_B sınır grubundan aramaya ekler. Ardından, artık hem BG_A hem de BG_B sınır gruplarından gelen birleştirilmiş dağıtım noktaları havuzundaki bir dağıtım noktasından içerik aramaya devam eder. İstemci, havuzdan sonraki dağıtım noktasına geçmeden önce her dağıtım noktasıyla iki dakika boyunca iletişim kurmaya devam eder. Geçerli içerik kaynak konumlarının istemci havuzu DP_A1, DP_A2, DP_B1 ve DP_B2 içerir.
- Ek 10 dakika sonra (20 dakikalık toplam), istemci hala içeriğe sahip bir dağıtım noktası bulmadığından, mevcut dağıtım noktası havuzunu ikinci *komşu* grubundan, sınır grubu BG_C dahil etmek üzere genişletir. İstemci artık arama yapmak için 6 dağıtım noktasına sahiptir (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 ve DP_C2) ve içerik bulunana kadar her iki dakikada bir yeni dağıtım noktasına değiştirmeye devam eder.
- İstemci toplam 120 dakikadan sonra içerik bulmadığından, devam eden aramasının bir parçası olarak *varsayılan site sınır grubunu* dahil etmek için geri döner. Artık dağıtım noktaları havuzu, üç yapılandırılmış sınır grubundan ve site sunucusu bilgisayarında bulunan son dağıtım noktasından tüm dağıtım noktalarını içerir.  İstemci daha sonra içerik aramaya devam eder ve içerik bulunana kadar her iki dakikada bir dağıtım noktasını değiştirir.

Farklı komşu grupları, belirli dağıtım noktalarının bir içerik kaynağı konumu olarak ne zaman eklendiğini kontrol ettiğiniz ve ne zaman veya ne zaman, istemci diğer bir konumdan kullanılamayan içerik için bir güvenlik ağı olarak varsayılan site sınır grubuna geri dönüş kullanır.


### <a name="update-existing-boundary-groups-to-the-new-model"></a><a name="bkmk_update"></a>Mevcut sınır gruplarını yeni modele Güncelleştir
Sürüm 1609 ' i yüklediğinizde ve sitenizi güncelleştirdiğinizde, aşağıdaki konfigürasyonlar otomatik olarak yapılır. Bunlar, yeni sınır grupları ve ilişkiler yapılandırılana kadar geçerli geri dönüş davranışının kullanılabilir kalmasını sağlamak için tasarlanmıştır.  
- Bir sitedeki korumasız dağıtım noktaları, bu sitenin *varsayılan site sınır grubu \<sitecode> * sınır grubuna eklenir.
- Bir kopya, yavaş bağlantıyla yapılandırılmış bir site sunucusu içeren her bir mevcut sınır grubundan oluşur. Yeni grubun adı *** \<original boundary group name> -yavaş-tmp***:  
  -   Hızlı bağlantısı olan site sistemleri orijinal sınır grubunda bırakılır.
  -   Sınır grubunun kopyasına yavaş bağlantısı olan site sistemlerinin bir kopyası eklenir. Yavaş olarak yapılandırılan özgün site sistemleri geriye dönük uyumluluk için özgün sınır grubunda kalır, ancak bu sınır grubundan kullanılmaz.
  -   Bu sınır grubu kopyasında kendisiyle ilişkili sınırlar yok. Ancak, özgün grup ve geri dönüş süresi sıfır olan yeni sınır grubu kopyası arasında bir geri dönüş bağlantısı oluşturulur.

  Aşağıdaki tabloda, özgün dağıtım ayarlarını ve dağıtım noktası yapılandırmalarının birleşimini beklemeniz için kullanabileceğiniz yeni geri dönüş davranışı tanımlanmaktadır:

Yavaş ağda "program çalıştırma" için özgün dağıtım yapılandırması  |"İstemcinin içerik için bir geri dönüş kaynak konumu kullanmasına Izin ver" için özgün dağıtım noktası yapılandırması  |Yeni geri dönüş davranışı  
---------|---------|---------
Seçili     |  Seçili    |  **Geri dönüş yok** -yalnızca geçerli sınır grubundaki dağıtım noktalarını kullan       
Seçili     |  Seçilmedi|  **Geri dönüş yok** -yalnızca geçerli sınır grubundaki dağıtım noktalarını kullan       
Seçilmedi |  Seçilmedi|  **Komşuyla geri dönüş** -geçerli sınır grubundaki dağıtım noktalarını kullanın ve ardından komşu sınır grubundan dağıtım noktalarını ekleyin. Varsayılan site sınır grubuna yönelik açık bir bağlantı yapılandırılmadığı takdirde, istemciler bu gruba geri dönüşmeyecektir.    
Seçilmedi | Seçili |   **Normal geri dönüş** -geçerli sınır grubundaki dağıtım noktalarını, ardından komşu ve site varsayılan sınır gruplarını kullanın

 Diğer tüm dağıtım yapılandırmalarının **normal geri dönüşte**sonuçlanır.  



## <a name="office-365-client-management-dashboard"></a>Office 365 Istemci yönetimi panosu  
Configuration Manager 1609 Technical Preview, yeni bir pano sunar. Panoyu görüntülemek için Configuration Manager konsolunda **yazılım kitaplığı**  >  **'na genel bakış**  >  **Office 365 istemci yönetimi**' ne gidin.
>[!NOTE]
>Configuration Manager konsolundaki **Yenilikler çalışma alanında, yeni Pano** **Office 365 bakım panosu**yanlış biçimde adlandırılmaktadır.

Panoda aşağıdakiler için grafikler görüntülenir:

- Office 365 istemcilerinin sayısı
- Office 365 istemci sürümleri
- Office 365 istemci dilleri
- Office 365 istemci kanalları     
Daha fazla bilgi için bkz. [Microsoft 365 uygulamalar için güncelleştirme kanallarına genel bakış](https://docs.microsoft.com/deployoffice/overview-update-channels).
- Kullanılabilir ürünler kümesinde Office 365 Istemcisinin seçtiği otomatik dağıtım kuralları.

Panoda aşağıdaki eylemleri gerçekleştirebilirsiniz:
- Panonun üst kısmında, belirli bir koleksiyonun üyelerine Pano verilerini filtrelemek için **koleksiyon** açılan ayarını kullanın.
- Office 365 Istemci yükleme Microsoft 365 sihirbazını başlatmak için panonun sağ üst kısmında **office 365 yükleyicisi** ' ne tıklayın. Ayrıntılar için bkz. [uygulamaları Istemcilere dağıtma Microsoft 365](#deploy-microsoft-365-apps-to-clients).
- Yeni bir otomatik dağıtım kuralı (ADR) oluşturmak için panonun sağ orta tarafındaki **ADR oluştur** ' a tıklayın. Microsoft 365 uygulamalar için bir ADR oluşturmak için, ürünü seçerken **Office 365 istemcisi** ' ni seçin. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](../../sum/deploy-use/automatically-deploy-software-updates.md).
- Panonun sağ alt tarafında, istemci Aracısı Ayarları ' nı açmak için **Istemci Aracısı ayarları oluştur** ' a tıklayın. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../clients/deploy/about-client-settings.md).



Kurumsal güncelleştirmelere yönelik Microsoft 365 uygulamalar hakkında daha fazla bilgi için, bkz. [Configuration Manager ile Microsoft 365 Apps güncelleştirmelerini yönetme](../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="deploy-microsoft-365-apps-to-clients"></a>Microsoft 365 uygulamalarını istemcilere dağıtma
Bu sürümde, Office 365 Istemci yönetimi panosundan, Microsoft 365 yükleme ayarlarını yapılandırmanıza, Office Içerik teslim ağlarından (CDNs) dosya yüklemenize ve dosyaları Configuration Manager bir uygulama olarak dağıtmanıza olanak sağlayan Office 365 yükleyicisini başlatabilirsiniz.

### <a name="limitations-of-microsoft-365-deployment"></a>Microsoft 365 dağıtımının sınırlamaları
- Office 365 uygulama yüklemesi Sihirbazı 'nda mevcut istemci ayarlarını (XML) içeri aktarmaya çalıştığınızda sorunlarla karşılaşabilirsiniz. İstemci ayarlarını bir sorun olmadan el ile yapılandırabilirsiniz.

#### <a name="to-deploy-microsoft-365-apps-to-clients"></a>İstemcilere Microsoft 365 uygulamaları dağıtmak için
1. Configuration Manager konsolunda, **yazılım kitaplığı**  >  **genel bakış**  >  **Office 365 istemci yönetimi**' ne gidin.
2. Sağ üst bölmedeki **Office 365 yükleyicisi** ' ne tıklayın. Office 365 Istemci Yükleme Sihirbazı açılır.
3. **Uygulama ayarları** sayfasında, uygulama için bir ad ve açıklama sağlayın, dosyalar için karşıdan yükleme konumunu girin ve ardından **İleri**' ye tıklayın. Konumun &#92;&#92;*server*&#92;*paylaşımında*belirtilmesi gerektiğini unutmayın.
4. **Istemci ayarlarını Içeri aktar** sayfasında, Microsoft 365 istemci ayarlarını var olan bir XML yapılandırma dosyasından içeri aktarıp aktarmayacağını seçin veya ayarları el Ile belirtip **İleri**' ye tıklayın.
Varolan bir yapılandırma dosyanız varsa, dosyanın konumunu girin ve 7. adıma atlayın. Konumun &#92;&#92;*server*&#92;*Share*&#92;*filename*biçiminde belirtilmesi gerektiğini unutmayın. 'Sini.

    > [!IMPORTANT]
    >Bu Technical Preview 'da mevcut istemci ayarlarını (XML) içeri aktarmaya çalıştığınızda sorunlarla karşılaşabilirsiniz.

5. **Istemci ürünleri** sayfasında, kullandığınız Microsoft 365 paketini seçin, dahil etmek istediğiniz uygulamaları seçin, dahil edilecek diğer Office ürünlerini seçin ve ardından **İleri**' ye tıklayın.
6. **Istemci ayarları** sayfasında, dahil edilecek ayarları seçin ve ardından **İleri**' ye tıklayın.
7. **Dağıtım** sayfasında, uygulamayı dağıtıp dağıtmeyeceğinizi seçin ve ardından **İleri**' ye tıklayın.
Paketi sihirbazda dağıtmamalıdır seçeneğini belirlerseniz adım 9 ' a atlayın.
8. Sihirbaz sayfalarının geri kalanını tipik bir uygulama dağıtımında yaptığınız gibi yapılandırın. Daha fazla bilgi için bkz. [uygulama oluşturma ve dağıtma](../../apps/get-started/create-and-deploy-an-application.md).
9. Sihirbazı tamamlayın.
10. Uygulamayı, **yazılım kitaplığı**  >  **'na genel bakış**  >  **uygulama yönetimi**  >  **uygulamalarından**Configuration Manager içindeki diğer uygulamalarla aynı şekilde dağıtabilir veya düzenleyebilirsiniz.

>[!NOTE]
>Microsoft 365 uygulamaları dağıttıktan sonra, uygulamaları sürdürmek için otomatik dağıtım kuralları oluşturabilirsiniz. Microsoft 365 uygulamalar için ADR oluşturmak için, **ADR oluştur**' a tıklayın ve ürünü seçerken **Office 365 istemcisi** ' ni seçin. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini otomatik olarak dağıtma](../../sum/deploy-use/automatically-deploy-software-updates.md).

## <a name="improvements-for-bios-to-uefi-conversion"></a><a name="BKMK_UEFIConversion"></a>BIOS 'TAN UEFı 'ye dönüştürmeye yönelik iyileştirmeler
Artık, bilgisayarı yeniden Başlat adımının UEFı 'ye geçiş için sabit sürücüdeki bir FAT32 bölümünü hazırlayabilmesi için TSUEFIDrive adlı yeni bir değişkenle bir işletim sistemi dağıtımı görev dizisini özelleştirebilirsiniz. Aşağıdaki yordam, BIOS 'TAN UEFı 'ye dönüştürme için sabit sürücüyü hazırlamak üzere görev dizisi adımlarını nasıl oluşturabileceğiniz hakkında bir örnek sağlar.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>UEFı 'ye dönüştürme için FAT32 bölümünü hazırlamak için:
Bir işletim sistemini yüklemek için var olan bir görev dizisinde, BIOS 'TAN UEFı dönüştürmesi yapmak için gereken adımları içeren yeni bir grup ekleyeceksiniz.

1. Dosya ve ayarları yakalama adımlarında ve işletim sistemini yüklemek için olan adımlardan önce yeni bir görev dizisi grubu oluşturun. Örneğin, **BIOS-UEFI**adlı **yakalama dosyaları ve ayarlar** grubundan sonra bir grup oluşturun.
2. Yeni grubun **Seçenekler** sekmesinde, **_SMSTSBootUEFI** **true** **değerine eşit olmayan** bir koşul olarak yeni bir görev dizisi değişkeni ekleyin. Bu, bir bilgisayar zaten UEFı modunda olduğunda gruptaki adımların çalıştırılmasını önler.
![BIOS 'TAN UEFı grubuna](media/BIOS-to-UEFI-group.png)
3. Yeni Grup altında **Bilgisayarı yeniden Başlat** görev sırası adımını ekleyin. **Yeniden başlatma işleminden sonra ne çalıştırılacağını belirtin**bölümünde, BILGISAYARı Windows PE 'de başlatmak için **Bu görev dizisine atanan önyükleme görüntüsünü** seçin.  
4. **Seçenekler** sekmesinde, **_SMSTSInWinPE eşitse**bir koşul olarak bir görev dizisi değişkeni ekleyin. Bu, bilgisayar zaten Windows PE 'de ise bu adımın çalışmasını önler.

    ![Bilgisayarı yeniden Başlat adımı](media/Restart-in-Windows-PE.png)
5. Yazılım yazılımını BIOS 'tan UEFı 'ye dönüştürecek OEM aracını başlatmak için bir adım ekleyin. Bu, tipik olarak bir komut satırı Çalıştır görev dizisi adımını bir komut satırı ile **ÇALıŞTıRARAK** OEM aracını başlatır.
5. Sabit sürücüyü bölümlemek ve biçimlendirmek için disk Biçimlendir ve bölümle disk görev dizisi adımını ekleyin. Adımda şunları yapın:
    1. İşletim sistemi yüklenmeden önce UEFı 'ye dönüştürülecek FAT32 bölümünü oluşturun. **Disk türü**için **GPT** 'yi seçin.
    ![Diski Biçimlendir ve bölümle adımı](media/Format-and-partition-disk.png)
    2. FAT32 bölümünün özelliklerine gidin. **Değişken** alanına **Tsuefidrive** girin. Görev dizisi bu değişkeni algıladığında, bilgisayar yeniden başlatılmadan önce UEFı geçişi için hazırlanacaktır.
    ![Bölüm Özellikleri](media/Partition-properties.png)
    3. Görev dizisi altyapısının durumunu kaydetmek ve günlük dosyalarını depolamak için kullandığı bir NTFS bölümü oluşturun.
6. **Bilgisayarı yeniden Başlat** görev dizisi adımını ekleyin. **Yeniden başlatma işleminden sonra ne çalıştırılacağını belirtin**bölümünde, BILGISAYARı Windows PE 'de başlatmak için **Bu görev dizisine atanan önyükleme görüntüsünü** seçin.  




## <a name="intune-compliance-charts"></a>Intune uyumluluk grafikleri
Bu sürümde, Configuration Manager konsolundaki **izleme çalışma alanı** altındaki yeni grafikleri kullanarak cihazların genel uyumluluğuna ve en önemli nedenlere ilişkin hızlı bir bakış edinebilirsiniz.

#### <a name="to-view-the-intune-compliance-charts"></a>Intune uyumluluk grafiklerini görüntülemek için
1. Configuration Manager konsolunda, **izleme**  >  **genel bakış**  >  **Uyumluluk ayarları**' na gidin.
2. **Genel cihaz uyumluluk** grafiği görüntülenir.
3. **Genel cihaz uyumluluğu** ve **en iyi uyumsuzluk nedenleri** grafiklerini görüntülemek için **uyumluluk ilkeleri** düğümüne tıklayın.

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>TP 1609 ' de Intune uyumluluk grafiklerinin sınırlamaları
- **Genel cihaz uyumluluk** grafiğinin detaya gitme işlemi şu anda bir hata oluşturuyor.
- **En üst uyumsuzluk nedenleri** grafiğinde ilke adı, bireysel uyumsuzluk nedenlerini listeler. Ayrıntıya gitmek ve bu ilke için uyumlu olmayan cihazları görmek için ilkeye tıklayabilirsiniz.

### <a name="try-it-out"></a>Deneyin
Aşağıdaki bölümleri sırasıyla doldurun:

#### <a name="check-overall-compliance-chart"></a>Genel uyumluluk grafiğini denetle
1. Configuration Manager iki iOS uyumluluk ilkesine ekleyin. Bir ilke, cihazlar için bir ayarlar kümesine sahip olmalıdır (örneğin, PIN uzunluğunu 6 olarak ayarlayın). Diğer ilke başka bir ayar kümesine sahip olmalıdır (örneğin, PIN karmaşıklığı). İlke ayarları çakışmamalı veya çakışmamalıdır.
2. İki ilkeyi bir kullanıcı kümesine dağıtın.
3. Intune 'a aynı kullanıcı hesabını kullanarak iki iOS cihazı ve önceki adımda ilkeleri alan bir hesabı kaydedin. Cihazların uyumluluk ilkesinin ölçütlerine uyması gerekmez.
4. Configuration Manager, **genel cihaz uyumluluk** grafiğini kontrol edin. Her iki cihaz de uyumlu değil olarak raporlanmalıdır.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>En yüksek uyumsuzluk nedenleri grafiğini denetle
5. **En üst uyumsuzluk nedenleri** grafiğini kontrol edin. Bu grafik uyumsuzluk için en iyi 5 nedeni listeler, ancak yalnızca iki uyumluluk ayarı ilke genelinde ayarlandığında yalnızca ilk 2 uyumsuzluk nedeni görüntülenir.
6. Grafikteki bölümlerden birine tıklayın. Her iki cihaz de **varlıklar ve uyumluluk**  >  **genel bakış**  >  **cihazı**altında filtrelenmiş görünümde görünmelidir.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Cihazları uyumlu hale getirme ve grafikleri denetleme
7. Cihazlardan birini ilkelerden biriyle uyumlu hale getirin. **Genel cihaz uyumluluk** grafiğini yeniden kontrol edin. Grafik, uyumlu bir cihaz ve uyumlu olmayan bir cihaz görüntülemelidir.
8. Diğer cihazı aynı ilkeyle uyumlu hale getirin. Bu, tek bir cihazı, ilkelerin yalnızca biri ile uyumlu olacak şekilde ve tek bir cihazla uyumlu hale getirir.
9. **En üst uyumsuzluk nedenleri** grafiğini kontrol edin. Yalnızca listelenen bir uyumsuzluk nedeni olmalıdır.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Ayrıca Bkz.
[Configuration Manager için teknik önizleme](../../core/get-started/technical-preview.md)