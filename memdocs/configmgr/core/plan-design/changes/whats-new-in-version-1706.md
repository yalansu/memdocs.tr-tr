---
title: Yeni sürüm 1706
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1706 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a8a4ce1c3d54311db18decc85f57d3e03298d339
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904689"
---
# <a name="what39s-new-in-version-1706-of-configuration-manager"></a>Sürüm 1706 ' deki yenilikler&#39;Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli dalın Configuration Manager güncelleştirme 1706, daha önce yüklü olan ve 1606, 1610 veya 1702 sürümlerini çalıştıran sitelerde konsol içi bir güncelleştirme olarak sunulmaktadır.

> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanmanız gerekir.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:    
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Sitelere güncelleştirme yükleme](../../servers/manage/updates.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)  

Aşağıdaki bölümlerde, Configuration Manager sürüm 1706 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi sağlanmaktadır.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Site altyapısı

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Windows 10 ve Office 365 için hızlı yükleme dosyaları için istemci eş önbelleği desteği  
<!-- 1352486 -->
Bu sürümden itibaren, eş önbellek Windows 10 için içerik hızlı yükleme dosyalarının ve Office 365 güncelleştirme dosyalarının dağıtımını destekler. Bu değişikliği desteklemek için ek yapılandırma gerekmez.

### <a name="updates-for-the-data-warehouse"></a>Veri ambarı güncelleştirmeleri
<!-- 1277922 -->
Veri ambarı artık yayın öncesi bir özellik değildir. Ayrıca, SQL Server Always on kullanılabilirlik grupları ve yük devretme kümelerinde veritabanı desteğini de içerecek şekilde önkoşulları güncelleştirdik. Daha fazla bilgi için bkz. [veri ambarı hizmet noktası](../../servers/manage/data-warehouse.md).

### <a name="accessibility-improvements"></a>Erişilebilirlik geliştirmeleri
<!-- 1253000 -->
Configuration Manager konsolu için erişilebilirlik 'e ek geliştirmeler ekledik. Ayrıntılar için bkz. [erişilebilirlik özellikleri](../../understand/accessibility-features.md).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>SQL Server Always on kullanılabilirlik gruplarında iyileştirmeler
<!-- 1352094 -->
Bu sürümle birlikte, artık Configuration Manager kullandığınız SQL Server Always on kullanılabilirlik gruplarında zaman uyumsuz tamamlama çoğaltmaları kullanabilirsiniz. Bu, site dışı (uzak) yedeklemeler olarak kullanmak üzere kullanılabilirlik gruplarınıza ek çoğaltmalar ekleyebileceğiniz ve sonra bunları bir olağanüstü durum kurtarma senaryosunda kullanabileceğiniz anlamına gelir.  
- Configuration Manager, zaman uyumlu çoğaltmanızı kurtarmak için zaman uyumsuz tamamlama çoğaltmasını kullanmayı destekler. Bunun nasıl yapılacağını öğrenmek için yedekleme ve kurtarma konusundaki [site veritabanı kurtarma seçenekleri](../../servers/manage/recover-sites.md#site-database-recovery-options) bölümüne bakın.
- Bu sürüm, site veritabanınız olarak zaman uyumsuz tamamlama çoğaltmasını kullanmak için yük devretmeyi desteklemez.
Daha fazla bilgi için bkz. [Always on kullanılabilirlik grupları 'nı kullanmaya hazırlanma](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="update-reset-tool"></a>Sıfırlama aracını güncelleştirme
<!-- 1324589 -->
Sürüm 1706 ' den başlayarak Configuration Manager birincil siteler ve merkezi yönetim siteleri, Configuration Manager güncelleştirme sıfırlama aracı **Cmupdatereset. exe**' yi içerir. Konsol içi güncelleştirmelerin indirme veya çoğaltma sorunları olduğunda sorunları gidermek için bu aracı, destek aşamasında kalan geçerli dalın herhangi bir sürümüyle birlikte kullanın. Daha fazla bilgi için bkz. [güncelleştirme sıfırlama aracı](../../servers/manage/update-reset-tool.md).

### <a name="high-dpi-console-support"></a>Yüksek DPı konsol desteği  
<!-- 1353476 -->
Bu sürümle birlikte, Configuration Manager konsolunun, yüksek DPı cihazlarda (yüzey defteri gibi) görüntülendiğinde, Kullanıcı arabiriminin farklı kısımlarını ölçeklendirdiği ve gösterdiği sorunlar düzeltilmelidir.

### <a name="improved-boundary-groups-for-software-update-points"></a>Yazılım güncelleştirme noktaları için iyileştirilmiş sınır grupları
<!-- 1324591 -->
Bu sürüm, yazılım güncelleştirme noktalarının sınır gruplarıyla nasıl çalıştığı hakkında iyileştirmeler içerir. Aşağıda yeni geri dönüş davranışı özetlenmektedir:
- Yazılım güncelleştirme noktaları için geri dönüş artık komşu sınır gruplarına geri dönüş için yapılandırılabilir bir zaman kullanır.
- Geri dönüş yapılandırmasından bağımsız olarak, bir istemci 120 dakika boyunca kullanılan son yazılım güncelleştirme noktasına ulaşmaya çalışır. Bu sunucuya 120 dakika boyunca ulaşamadıktan sonra istemci, kullanılabilir yazılım güncelleştirme noktası havuzunu denetleyerek yeni bir tane bulabilir.
- İki saat boyunca özgün sunucusuna ulaşamadıktan sonra istemci, yeni bir yazılım güncelleştirme noktasıyla iletişim kurmaya yönelik daha kısa bir döngüye geçer. Bu, bir istemcinin yeni bir sunucuyla bağlantı kuramamasıdır, bir sonraki sunucuyu kullanılabilir sunucu havuzundan hızlıca seçer ve bununla iletişim kurmayı dener.

Daha fazla bilgi için, Güncel Dalı için sınır grupları konusundaki [yazılım güncelleştirme noktaları](../../servers/deploy/configure/boundary-groups.md#software-update-points) bölümüne bakın.

### <a name="azure-ad-integration-with-configuration-manager"></a>Configuration Manager ile Azure AD tümleştirmesi
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
Bu sürümle Configuration Manager ve Azure Active Directory (Azure AD) tümleştirmesini geliştirdik.  Bu geliştirmeler, Configuration Manager ile kullandığınız Azure hizmetlerini nasıl yapılandıracağınızı ve Azure AD 'de kimlik doğrulaması yapan istemcileri ve kullanıcıları yönetmenize yardımcı olur.

Geliştirilmiş tümleştirme şunları mümkün kılar:  
- Azure Hizmetleri Sihirbazı – Bu sihirbaz, Configuration Manager ile kullandığınız aşağıdaki Azure hizmetlerini ayarlamak için bireysel iş akışlarının yerini alan ortak bir yapılandırma deneyimi sağlar.
  - **Bulut yönetimi** İstemcilerin kimlik doğrulamasını Azure Active Directory (Azure AD) kullanarak etkinleştirin. Ayrıca, Azure AD Kullanıcı bulmayı da yapılandırabilirsiniz.
  - **Log Analytics Bağlayıcısı** Azure Log Analytics bağlanın ve koleksiyon verilerini eşitleyin.
  - **Yükseltme hazırlığı** Yükseltme Hazırlığı bağlanın ve istemci yükseltme-uyumluluk verilerini görüntüleyin.
  - **İş Için Windows Mağazası** Iş için Windows Mağazası 'nın çevrimiçi deposuna bağlanın ve kuruluşunuz için Configuration Manager ile dağıtabileceğiniz uygulamalar alın.


  Bu işlem, Azure ile yeni bir Configuration Manager bileşeni veya hizmeti her yaptığınızda girdiğiniz abonelik ve yapılandırma ayrıntılarını sağlamak için bir [Azure Server Web uygulaması](/azure/app-service/app-service-authentication-overview) kullanılarak yapılır. Daha fazla bilgi için bkz. [Azure Hizmetleri Sihirbazı](../../servers/deploy/configure/azure-services-wizard.md).

- Configuration Manager sitelerinize erişmek için Internet 'teki istemcilerin kimliğini doğrulamak üzere Azure AD 'yi kullanın. Azure AD, istemci kimlik doğrulama sertifikalarını yapılandırma ve kullanma gereksinimininin yerini almaktadır. Bu, bulut yönetimi ağ geçidi site sistem rolünü gerektirir. Daha fazla bilgi için bkz. [kimlik doğrulaması Için Azure ad kullanarak İnternet 'ten Configuration Manager Istemcileri yükleyip atama](../../clients/deploy/deploy-clients-cmg-azure.md).

- Configuration Manager istemcisini Internet üzerinde bulunan bilgisayarlara yükleyip yönetin. Bu, bulut yönetimi ağ geçidi site sistem rolünün kullanılmasını gerektirir. Daha fazla bilgi için bkz. [kimlik doğrulaması Için Azure ad kullanarak İnternet 'ten Configuration Manager Istemcileri yükleyip atama](../../clients/deploy/deploy-clients-cmg-azure.md).

- Azure AD Kullanıcı keşfini yapılandırın.  Bu yeni bulma yöntemini yapılandırmak için Azure Hizmetleri Sihirbazı 'Nı kullanın. Bu yeni yöntem, Azure AD 'yi Kullanıcı verilerini sorgular ve daha sonra geleneksel bulma verilerini birlikte kullanabilirsiniz.  Hem tam hem de Delta eşitlemesi desteklenir.  Daha fazla bilgi için bkz. [Azure AD Kullanıcı keşfi](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="peer-cache-improvements"></a>Eş önbellek geliştirmeleri
<!-- 1252345 -->
Eş önbellek artık eşlerden gelen indirme isteklerinin kimliğini doğrulamak için ağ erişim hesabını kullanmaz. Hesap istemciler için gerekli olmaya devam ettiği zaman buna bir desteklenmediği uyarısıyla vardır. Bu, WinPE 'de önyükleme yapan istemciler için bir gereksinim ve sonra da bir eş önbellek kaynağından içeriğe erişme gereksinimi ortadan saklanır. Daha fazla bilgi için bkz. [eş önbellek gereksinimleri ve konuları](../hierarchy/client-peer-cache.md#requirements).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Uyumluluk ayarları

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Configuration Manager istemcisiyle yönetilmeyen Windows 10 cihazları için yeni yapılandırma ayarları
<!-- 1354715 -->
Bu sürümde, Intune 'a kaydedilmiş veya şirket içinde Configuration Manager tarafından yönetilen Windows 10 cihazları için yeni yapılandırma öğesi ayarları ekledik. Ayarlar şunlardır:

- **Parola**
  - Cihaz şifreleme
- **Cihaz**
  - Bölge ayarlarının değiştirilmesi (yalnızca masaüstü)
  - Güç ve uyku ayarlarının değiştirilmesi
  - Dil ayarları değişikliği
  - Sistem saati değişikliği
  - Cihaz adı değişikliği
- **Depo**
  - Mağazadan uygulamaları otomatik güncelleştir
  - Yalnızca özel mağazayı kullan
  - Mağaza kaynaklı uygulama başlatma
- **Microsoft Edge**
  - About: Flags sayfasına erişimi engelle
  - SmartScreen istemi geçersiz kılma
  - Dosyalar için SmartScreen istemi geçersiz kılma
  - WebRTC localhost IP adresi
  - Varsayılan arama altyapısı
  - OpenSearch XML URL 'SI
  - Homepages (yalnızca masaüstü)

Tüm Windows 10 ayarlarının ayrıntıları için, bkz. [Configuration Manager istemcisi olmadan yönetilen Windows 8.1 ve Windows 10 cihazları için yapılandırma öğeleri oluşturma](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-device-compliance-policy-rules"></a>Yeni cihaz uyumluluk ilkesi kuralları

* **Gerekli parola türü**. Kullanıcının alfasayısal parola mı yoksa sayısal parola mı oluşturması gerektiğini belirtin. Alfasayısal parolalar için parolanın sahip olması gereken karakter kümesi sayısı alt sınırını da belirtirsiniz. Dört karakter kümesi şunlardır: küçük harf, büyük harfler, semboller ve sayılar.

  **Şu platformlarda desteklenir:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
  <br></br>
* **CIHAZDA USB hata ayıklamayı engelleyin**. Bu ayarları, Android for Work cihazlarında USB hata ayıklama zaten devre dışı bırakıldığı için yapılandırmanız gerekmez.

  **Şu platformlarda desteklenir:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Bilinmeyen kaynaklardan gelen uygulamaları engelleyin**. Cihazların bilinmeyen kaynaklardan uygulama yüklenmesini engellemesini gerektir. Android for Work cihazları her zaman bilinmeyen kaynaklardan yüklemeyi kısıtlayabileceğinden bu ayarı yapılandırmanız gerekmez.

  **Şu platformlarda desteklenir:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Uygulamalarda tehdit taraması gerektir**. Bu ayar, cihazda uygulamaları doğrula özelliğinin etkinleştirildiğini belirtir.

  **Şu platformlarda desteklenir:**
  * Android 4,2 ila 4,4
  * Samsung KNOX Standard 4.0+


## <a name="application-management"></a>Uygulama Yönetimi

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Configuration Manager konsolundan PowerShell betikleri çalıştırma
<!-- 1236459 -->

Configuration Manager, paketleri ve programları kullanarak istemci cihazlarına komut dosyaları dağıtabilirsiniz. Bu sürümde, aşağıdaki eylemleri gerçekleştirmenizi sağlayan yeni işlevler ekledik:

- PowerShell betiklerini Configuration Manager içeri aktar
- Configuration Manager konsolundan betikleri düzenleme (yalnızca imzasız betikler için)
- Güvenliği artırmak için betikleri onaylanmış veya reddedildi olarak işaretle
- Windows istemci bilgisayarlarının ve şirket içi yönetilen Windows bilgisayarlarının koleksiyonlarında betikleri çalıştırın. Betikleri dağıtmazsınız, bunun yerine istemci cihazlarda neredeyse gerçek zamanlı olarak çalıştırılır.
- Configuration Manager konsolundaki komut dosyası tarafından döndürülen sonuçları inceleyin.

Daha fazla bilgi için, bkz. [Configuration Manager konsolundan PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Yeni mobil uygulama yönetimi ilke ayarları    
<!--1324760-->
Bu sürümden itibaren, üç yeni mobil uygulama yönetimi (MAM) ilkesi ayarı kullanabilirsiniz:

- **Ekran yakalamayı engelle (yalnızca Android cihazlar):** Bu uygulama kullanılırken cihazın ekran yakalama yeteneklerinin engellendiğini belirtir.


## <a name="operating-system-deployment"></a>İşletim sistemi dağıtımı

### <a name="hardware-inventory-collects-secure-boot-information"></a>Donanım envanteri güvenli önyükleme bilgilerini toplar
Donanım envanteri artık istemcilerde güvenli önyüklemenin etkin olup olmadığı hakkında bilgi toplar. Bu bilgiler **SMS_Firmware** sınıfında depolanır (sürüm 1702 ' de kullanıma sunulmuştur) ve varsayılan olarak donanım envanterinde etkinleştirilir. Donanım envanteri hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="collapsible-task-sequence-groups"></a>Daraltılabilir görev dizisi grupları
Bu sürüm, görev dizisi gruplarını genişletme ve daraltma özelliğini tanıtır. Tek tek grupları genişletebilir veya daraltabilir veya aynı anda tüm grupları genişletebilir veya daraltabilirsiniz.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Önyükleme görüntülerini geçerli Windows PE sürümü ile yeniden yükle
Seçilen bir önyükleme görüntüsünde **güncelleştirme dağıtım noktalarını** çalıştırdığınızda, artık Windows PE 'nin en son sürümünü (Windows ADK yükleme dizininden) önyükleme görüntüsüne yeniden yüklemeyi tercih edebilirsiniz. Daha fazla bilgi için bkz. [dağıtım noktalarını Önyükleme görüntüsüyle güncelleştirme](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Yazılım güncelleştirmeleri

### <a name="improvements-to-express-update-download-time"></a>Hızlı güncelleştirme indirme süresi geliştirmeleri
Bu sürümde, Hızlı güncelleştirmeler için indirme süresini önemli ölçüde geliştirdik. Daha fazla bilgi için bkz. [Windows 10 güncelleştirmeleri Için hızlı yükleme dosyalarını yönetme](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

### <a name="manage-microsoft-surface-driver-updates"></a>Microsoft Surface sürücü güncelleştirmelerini yönetme
<!-- 1098490 -->
Artık, Microsoft Surface sürücü güncelleştirmelerini yönetmek için Configuration Manager kullanabilirsiniz.    


#### <a name="prerequisites"></a>Ön koşullar
- Tüm yazılım güncelleştirme noktalarında Windows Server 2016 çalışmalıdır.    
- Bu, kullanılabilir olması için açmanız gereken bir ön sürüm özelliğidir. Daha fazla bilgi için bkz. [Güncelleştirmelerden yayın öncesi sürüm özelliklerini kullanma](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Surface sürücü güncelleştirmelerini yönetmek için

1. Microsoft Surface sürücüleri için eşitlemeyi etkinleştirin. Surface sürücülerini etkinleştirmek için sınıflandırmaların [ve ürünlerin yapılandırma](../../../sum/get-started/configure-classifications-and-products.md) bölümündeki yordamı kullanın ve **sınıflandırmalar** sekmesinde **Microsoft Surface sürücülerini ve bellenim güncelleştirmelerini dahil et** onay kutusunu seçin.
2. [Microsoft Surface sürücülerini eşitler](../../../sum/get-started/synchronize-software-updates.md).
3. [Eşitlenmiş Microsoft Surface sürücüleri dağıtma](../../../sum/deploy-use/deploy-software-updates.md)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Iş erteleme ilkeleri için Windows Update yapılandırma
<!-- 1290890 -->
Artık Windows 10 için Windows 10 özellik güncelleştirmeleri veya kalite güncelleştirmeleri için erteleme ilkelerini, doğrudan Windows Update Iş tarafından yönetilen Windows 10 cihazları için yapılandırabilirsiniz. **Yazılım kitaplığı**Windows 10 bakımı altındaki **iş için yeni Windows Update ilke** düğümünde erteleme ilkelerini yönetebilirsiniz  >  **Windows 10 Servicing**.

Ayrıntılar için bkz. [Windows 10 ' da iş için Windows Update tümleştirme](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Office 365 güncelleştirmeleri için geliştirilmiş Kullanıcı bildirimleri
Bir istemci Office 365 güncelleştirmesi yüklediğinde Office Tıkla-Çalıştır Kullanıcı deneyiminden yararlanmak için geliştirmeler yapılmıştır. Bu, açılır ve uygulama içi bildirimleri ve geri sayım deneyimini içerir. Daha fazla bilgi için bkz. [yeniden başlatma davranışı ve Office 365 güncelleştirmeleri için istemci bildirimleri](../../../sum/deploy-use/manage-office-365-proplus-updates.md#restart-behavior-and-client-notifications-for-office-365-updates)

## <a name="reporting"></a>Raporlama

### <a name="use-windows-analytics-with-configuration-manager"></a>Windows Analytics 'i Configuration Manager kullanma
<!-- 1318608 -->
Windows Analytics, ortamınızın geçerli durumuna ilişkin Öngörüler ayarlamanıza olanak tanıyan bir dizi çözümdür. Ortamınızdaki cihazlar Windows telemetri verilerini rapor ediyor. Verilere Azure portal aracılığıyla erişilebilir. Yükseltme Hazırlığı durumunda veriler, Configuration Manager konsolunun İzleme düğümünde doğrudan kullanılabilir.


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Mobil aygıt yönetimi

### <a name="updates-to-android-for-work-sharing-configuration"></a>Android for Work paylaşım yapılandırması güncelleştirmeleri
<!-- 1338403 -->
Bu sürümde, **Iş profili** ayar grubundaki **iş ve kişisel profil arasında veri paylaşımına izin ver** ayarı güncelleştirildi. Ayrıca, iş ve kişisel profiller arasında kopyalama-yapıştırmayı engellemek için özel bir ayar ekledik.


### <a name="android-and-ios-enrollment-restrictions"></a>Android ve iOS kayıt kısıtlamaları
<!-- 1290826 -->
Bu sürümde, artık kullanıcıların kişisel Android veya iOS cihazlarını kaydedemeyecek olduğunu belirtebilirsiniz. Yeni cihaz kısıtlama ayarları, Android cihaz kaydını önceden tanımlanmış cihazlarla sınırlamanıza izin verir. İOS cihazlarında, Apple 'ın Aygıt Kayıt Programı, Apple Configurator veya Intune cihaz kayıt yöneticisi hesabı ile kaydolmuş olanlar hariç tüm cihazların kaydını engelleyebilirsiniz.

## <a name="protect-devices"></a>Cihazları koruma

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Bir Device Guard ilkesindeki belirli dosya ve klasörler için güven Ekle
<!--1324676-->
Bu sürümde, Device Guard ilke yönetimine daha fazla özellik ekledik.

Artık isteğe bağlı olarak, bir Device Guard ilkesindeki klasörler için belirli dosyalar için güven ekleyebilirsiniz. Bu şunları yapmanızı sağlar:

- Yönetilen yükleyici davranışları ile ilgili sorunları aşmak
- Configuration Manager ile dağıtılabilecek iş kolu uygulamalarına güvenin
- Bir işletim sistemi dağıtım görüntüsüne dahil olan uygulamalara güven

Daha ayrıntılı bilgi için bkz. [Configuration Manager Ile cihaz koruyucu yönetimi](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
