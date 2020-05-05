---
title: Yeni sürüm 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Configuration Manager sürüm 1710 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 15735b015796d2cccfa9b0a24afc8f6eb0573df1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073628"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Sürüm 1710 ' deki yenilikler&#39;Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli dalın Configuration Manager güncelleştirme 1710, daha önce yüklü olan ve 1610, 1702 veya 1706 sürümlerini çalıştıran sitelerde konsol içi bir güncelleştirme olarak sunulmaktadır.

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

Bu sürüm için aşağıdaki ek güncelleştirmeler de kullanılabilir:
- [Geçerli Configuration Manager dalı için güncelleştirme paketi, sürüm 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Geçerli Configuration Manager dalı için güncelleştirme paketi 2, sürüm 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanmanız gerekir.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:    
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Sitelere güncelleştirme yükleme](../../servers/manage/updates.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)

Aşağıdaki bölümlerde, Configuration Manager sürüm 1710 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi sağlanmaktadır.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Site altyapısı

### <a name="updates-for-peer-cache-----sms500850---"></a>Eş önbellek güncelleştirmeleri  <!-- sms500850 -->
Bu sürümden itibaren, eş önbellek artık yayın öncesi bir özellik değildir.  Bu sürümle eş önbellek için başka bir değişiklik yapılmaz. Daha fazla bilgi için bkz. [Configuration Manager istemcileri Için eş önbellek](../hierarchy/client-peer-cache.md).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Azure Kamu Bulutu için bulut dağıtım noktası desteği   <!-- sms491428 -->
Artık Azure Kamu bulutundaki [bulut tabanlı dağıtım noktalarını](../hierarchy/use-a-cloud-based-distribution-point.md) kullanabilirsiniz.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Stok varsayılan birim düzeltmesi <!-- sms503697 -->
Cihazlar artık gigabayt (GB), terabaytlık (TB) ve daha büyük ölçeklerdeki boyutlarda sabit sürücüler içerdiği için, bu sürüm birçok görünümde kullanılan varsayılan birimi (SMS_Units) megabayt (MB) ile GB olarak değiştirir. Örneğin, v_gs_LogicalDisk. FreeSpace değeri artık GB birimleri bildiriyor.


<!-- ## Migration  -->


## <a name="client-management"></a>İstemci yönetimi

### <a name="co-management-for-windows-10-devices"></a>Windows 10 cihazları için ortak yönetim    
<!-- 1350871 -->
Önceki Windows 10 güncelleştirmelerinde, bir Windows 10 cihazını şirket içi Active Directory (AD) ve bulut tabanlı Azure AD 'ye aynı anda (Hibrit Azure AD) ekleyebilirsiniz. Configuration Manager sürüm 1710 ' den başlayarak, ortak yönetim bu iyileştirmelerden yararlanır ve hem Configuration Manager hem de Intune 'u kullanarak Windows 10, sürüm 1709 (Ayrıca, Fall Creators Update olarak da bilinir) cihazlarını eşzamanlı olarak yönetmenizi sağlar. Geleneksel ve modern yönetime köprü sağlayan ve bir aşamalı yaklaşım kullanarak geçişi yapmak için size yol veren bir çözümdür. Ayrıntılar için bkz. [Windows 10 cihazlar Için ortak yönetim](../../../comanage/overview.md).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Configuration Manager konsolundan bilgisayarları yeniden başlatma  <!-- 1356283 -->
Bu sürümden itibaren, yeniden başlatma gerektiren istemci cihazlarını belirlemek için Configuration Manager konsolunu kullanabilir ve sonra yeniden başlatmak için bir istemci bildirim eylemi kullanabilirsiniz.

Bkz. [istemcileri yönetme](../../clients/manage/manage-clients.md#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>Uygulama Yönetimi
### <a name="improvements-for-run-scripts------1236459---"></a>Çalıştırma betikleri geliştirmeleri   <!-- 1236459 -->
Bu sürüm, **komut dosyalarını çalıştır** özelliği için, yönetilen cihazlarda çalıştırmak üzere PowerShell betikleri dağıtmanıza imkan tanıyan birkaç geliştirme getirir. Bu özellik ilk olarak sürüm 1706 ' de sunulmuştur.

Geliştirmeler şunları içerir:
- Çalıştırma betikleri kullanabilecek kişileri denetlemeye yardımcı olması için güvenlik kapsamları kullanın
- Çalıştırdığınız betikleri gerçek zamanlı izleme
- Komut dosyası oluşturma Sihirbazı 'nda betik görüntüsüne yönelik parametreler, doğrulama desteği ve zorunlu veya isteğe bağlı olarak tanımlanır.

Çalıştırma betikleri kullanma hakkında daha fazla bilgi için bkz. [betik oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Yeni mobil uygulama yönetimi ilke ayarları
<!-- 1324760 -->
Mobil uygulama yönetimi ilkesi ayarlarına aşağıdaki ayarlar eklenmiştir:
- **Kişi eşitlemesini devre dışı bırak**: uygulamanın cihazdaki yerel Kişiler uygulamasına veri kaydetmesini önler.
- **Yazdırmayı devre dışı bırak**: uygulamanın iş veya okul verilerini yazdırmasını önler.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Yazılım Merkezi artık 250x250 ' dan büyük simgeleri bozar  
<!-- 1356194 -->

Bu sürümle birlikte, Yazılım Merkezi artık 250x250 ' dan büyük simgeleri bozmayacaktır. Yazılım Merkezi bu tür simgeler bulanık bir şekilde görünür. Artık 512x512 ' ye kadar piksel boyutlarına sahip bir simge ayarlayabilirsiniz ve bozulma olmadan görüntülenir.

Yazılım Merkezi 'nde uygulamanız için bir simge eklemek için bkz. [uygulama oluşturma](../../../apps/deploy-use/create-applications.md).

## <a name="operating-system-deployment"></a>İşletim sistemi dağıtımı
 > [!TIP]   
 > <!-- 1354281 -->
 > Windows 10, sürüm 1709 (Fall Creators Update olarak da bilinir) sürümü ile başlayarak, Windows Media birden çok sürüm içerir. Bir görev dizisini bir işletim sistemi yükseltme paketi veya işletim sistemi görüntüsü kullanacak şekilde yapılandırırken, [Configuration Manager tarafından kullanılmak üzere desteklenen bir sürüm](../configs/support-for-windows-10.md#windows-10-as-a-client)seçtiğinizden emin olun.

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Bir görev dizisine alt görev dizileri ekleme
<!-- 1261338 -->

Görev dizileri arasında bir üst/alt ilişki oluşturan başka bir görev dizisi çalıştıran yeni bir görev dizisi adımı ekleyebilirsiniz. Bu, yeniden kullanabileceğiniz daha modüler görev dizileri oluşturmanızı sağlar.  

Alt görev sırası hakkında daha fazla bilgi için bkz. [alt görev sırası](../../../osd/understand/task-sequence-steps.md#child-task-sequence).

## <a name="software-center-customization"></a>Yazılım Merkezi özelleştirmesi
<!-- 1351224 -->
Kurumsal marka öğeleri ekleyebilir ve yazılım merkezi 'ndeki sekmelerin görünürlüğünü belirtebilirsiniz. Yazılım merkezine özgü şirket adınızı ekleyebilir, bir yazılım merkezi yapılandırma renk teması ayarlayabilir, bir şirket logosu ayarlayabilir ve istemci cihazları için görünür sekmeleri ayarlayabilirsiniz.

Daha fazla bilgi için bkz. [uygulama yönetimini planlayın ve yapılandırın](../../../apps/plan-design/plan-for-and-configure-application-management.md).

## <a name="software-updates"></a>Yazılım güncelleştirmeleri

### <a name="surface-driver-updates-----1098490---"></a>Surface sürücü güncelleştirmeleri  <!-- 1098490 -->
Bu sürümden itibaren, Surface sürücü güncelleştirmelerini yönetmek artık yayın öncesi bir özellik değildir.  


## <a name="reporting"></a>Raporlama

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Windows 10 geliştirilmiş verilerini yalnızca Windows Analytics ile ilgili verileri gönderecek şekilde sınırlayın Cihaz Durumu
<!-- 1356148 -->

Artık Windows 10 tanılama veri toplama düzeyini **Gelişmiş (sınırlı)** olarak ayarlayabilirsiniz. Bu ayar, ortamınızdaki cihazlar hakkında, Windows 10 sürüm 1709 veya sonraki bir sürümü ile **Gelişmiş** düzeydeki tüm verileri raporlayan cihazlar hakkında eyleme dönüştürülebilir Öngörüler elde etmenizi sağlar.

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Mobil aygıt yönetimi

### <a name="actions-for-non-compliance"></a>Uyumsuzluk için eylemler 
<!--1321366 -->    
Artık, uyumsuz olan cihazlara uygulanan bir zaman sıralı eylem sırası yapılandırabilirsiniz. Örneğin, uyumlu olmayan cihazların kullanıcılarına e-posta yoluyla bildirimde bulunabilir veya bu cihazları uyumsuz olarak işaretleyebilirsiniz.

### <a name="windows-10-arm64-device-support"></a>Windows 10 ARM64 cihaz desteği
<!-- 1355000 -->

Karma mobil cihaz yönetimi (MDM) senaryoları, bu cihazlar kullanılabilir olduğunda Windows 10 çalıştıran ARM64 cihazlarında desteklenecektir.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Configuration Manager konsolunda geliştirilmiş VPN profili deneyimi 
<!-- 1318232 -->

Bu sürümle birlikte, VPN profili Sihirbazı ve Özellikler sayfalarını seçili platforma uygun ayarları görüntüleyecek şekilde güncelleştirdik:


- Her platformun kendi iş akışı vardır, yani yeni VPN profillerinin yalnızca platform tarafından desteklenen ayarı vardır.
- **Desteklenen platformlar** sayfası artık **genel** sayfasından sonra görüntülenir.  Artık özellik değerlerini ayarlamadan önce platformu seçersiniz.
- Platform **Android**, **Android for Work**veya **Windows Phone 8,1**olarak ayarlandığında, **Desteklenen platformlar** sayfası gerekli değildir ve gösterilmez.
- Configuration Manager istemci tabanlı iş akışı, karma mobil cihaz (MDM) istemci tabanlı Windows 10 iş akışlarıyla birleştirilmiştir. aynı ayarları destekler.
- Her platform iş akışı yalnızca ilgili iş akışına uygun olan ayarları içerir.  Örneğin, Android iş akışı Android için uygun ayarları içerir; iOS veya Windows 10 Mobile için uygun olan ayarlar artık Android iş akışında görünmez.
- Otomatik VPN sayfası artık kullanılmıyor ve kaldırıldı.

Bu değişiklikler yeni VPN profilleri için geçerlidir.  

Uyumluluk riskini en aza indirmek için mevcut VPN profilleri değiştirilmez.  Mevcut bir profili düzenlediğinizde, ayarlar profil oluşturulduğu sırada olduğu gibi görüntülenir.  

Daha fazla bilgi için bkz. [mobil cihazlarda VPN profilleri](../../../protect/deploy-use/vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Şifreleme için sınırlı destek: yeni nesil (CNG) sertifikaları <!-- 1356191 -->

Configuration Manager şifreleme: yeni nesil (CNG) sertifikaları için sınırlı destek içerir. Configuration Manager istemcileri, CNG Anahtar depolama sağlayıcısında (KSP) özel anahtarla PKI istemci kimlik doğrulama sertifikasını kullanabilir. KSP desteğiyle Configuration Manager istemcileri, PKI istemci kimlik doğrulama sertifikaları için TPM KSP gibi donanım tabanlı özel anahtarı destekler.

Daha fazla bilgi için bkz. [CNG sertifikalarına genel bakış](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Cihazları koruma

### <a name="create-and-deploy-exploit-guard-policies"></a>Exploit Guard ilkeleri oluşturma ve dağıtma
<!-- 1355468 -->

Windows Defender Exploit Guard 'ın saldırı yüzeyi azaltma, denetimli klasör erişimi, yararlanma koruması ve ağ koruması gibi dört bileşen bileşenini yöneten [ilkeler oluşturabilir ve dağıtabilirsiniz](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) .

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Windows Defender Application Guard ilkesi oluşturma ve dağıtma
<!-- 1351960 -->

Configuration Manager Endpoint Protection ['ı kullanarak Windows Defender Application Guard ilkeleri oluşturabilir ve dağıtabilirsiniz](../../../protect/deploy-use/create-deploy-application-guard-policy.md) .

### <a name="device-guard-policy-changes"></a>Device Guard ilke değişiklikleri
<!-- 1355092 -->
Device Guard ilkeleriyle ilgili olarak aşağıdaki üç değişiklik yapılmıştır:

- Device Guard ilkeleri Windows Defender uygulama denetimi ilkeleriyle yeniden adlandırıldı. Bu nedenle, örneğin, **Device Guard Ilke oluşturma Sihirbazı** artık **Windows Defender uygulama denetim ilkesi oluşturma Sihirbazı**olarak adlandırılmaktadır.
- Windows sürüm 1709 için Fall Creators Update 'i kullanan cihazlar, Windows Defender uygulama denetimi ilkelerini uygulamak için yeniden başlatma gerektirmez. Yeniden başlatma hala varsayılandır, ancak [yeniden başlatmalar devre dışı](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)bırakabilirsiniz.
- Cihazları, Intelligent Security Graph tarafından güvenilen [yazılımları otomatik olarak çalıştıracak şekilde ayarlayabilirsiniz](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) .





## <a name="next-steps"></a>Sonraki Adımlar
Bu sürümü yüklemeye hazırsanız, [Configuration Manager Için güncelleştirmeler](../../servers/manage/updates.md)bölümüne bakın.
