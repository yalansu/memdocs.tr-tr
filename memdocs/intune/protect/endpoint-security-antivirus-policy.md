---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle virüsten koruma ayarlarını yönetme | Microsoft Docs
description: Microsoft Endpoint Manager 'daki Endpoint Security Antivirus ilkesiyle yönettiğiniz cihazlar için ilkeleri yapılandırma ve dağıtma ve raporları kullanma.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: db1ad3250d04f79abd000a23f9f2064862b1dbd7
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915101"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için virüsten koruma ilkesi

Intune Endpoint Security virüsten koruma ilkeleri, güvenlik yöneticilerinin yönetilen cihazlar için ayrı virüsten koruma ayarları grubunu yönetmeye odaklanmasına yardımcı olabilir. Virüsten koruma ilkesini kullanmak için, Intune 'U Microsoft Defender Gelişmiş tehdit koruması (Microsoft Defender ATP) ile bir mobil tehdit savunması çözümü olarak tümleştirin.

Virüsten koruma ilkesi çeşitli profiller içerir. Her profil, yalnızca macOS, Windows 10 için Microsoft Defender ATP Antivirus veya Windows 10 cihazlarında Windows Güvenlik uygulamasındaki kullanıcı deneyimi için uygun olan ayarları içerir.

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin uç nokta güvenlik düğümünde, **Yönetim** altındaki virüsten koruma ilkelerini bulacaksınız.

Virüsten koruma ilkeleri, *uç nokta koruma* veya cihaz [yapılandırma](../configuration/device-profile-create.md) ilkesi için *cihaz kısıtlama* profillerinde bulunan ayarların aynısını içerir ve [cihaz uyumluluk](../protect/device-compliance-get-started.md) ilkesindeki ayarlara benzer. Ancak, bu ilke türleri, virüsten koruma ile ilgili olmayan ek ayar kategorilerini içerir. Ek ayarlar, virüsten koruma yapılandırma görevini karmaşıklaştırabilir. Ayrıca, macOS için virüsten koruma ilkesinde bulunan ayarlar diğer ilke türleri aracılığıyla kullanılamaz. MacOS virüsten koruma profili, dosyaları kullanarak ayarları yapılandırma ihtiyacını değiştirir `.plist` .

## <a name="prerequisites-for-antivirus-policy"></a>Virüsten koruma ilkesi önkoşulları

**Genel**:

- **macOS**
  - Tüm desteklenen macOS sürümleri
  - Intune 'un bir cihazdaki virüsten koruma ayarlarını yönetmesi için, bu cihaza Microsoft Defender ATP 'nin yüklü olması gerekir. Bakýn. [MacOS Için Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (MICROSOFT Defender ATP belgeleri)

- **Windows 10 ve üzeri**
  - Ek önkoşul gerekmez.

**Configuration Manager istemcileri Için destek** (*Önizleme*)

*Bu senaryo önizleme aşamasındadır ve geçerli Configuration Manager dalı sürümü 2006 veya sonraki bir sürümünü kullanmanızı gerektirir*.
<!--*This scenario is in preview and requires use of Configuration Manager Technical Preview version 2007 or later*.-->

- **Configuration Manager cihazlar için kiracı eklemeyi ayarlama** -virüsten koruma ilkesinin Configuration Manager tarafından yönetilen cihazlara dağıtılmasını desteklemek için *kiracı eklemeyi*yapılandırın. Kiracı ekleme 'nin kurulumunu, Intune 'dan Endpoint Security ilkelerini desteklemek için Configuration Manager cihaz koleksiyonlarının yapılandırılmasını içerir.

  Kiracı iliştirme 'yi ayarlamak için bkz. [Endpoint Protection ilkelerini desteklemek için kiracı eklemeyi yapılandırma](../protect/tenant-attach-intune.md).

## <a name="antivirus-profiles"></a>Virüsten koruma profilleri

### <a name="devices-managed-by-intune"></a>Intune tarafından yönetilen cihazlar

Intune ile yönettiğiniz cihazlar için aşağıdaki profiller desteklenir:

**macOS**:

- Platform: **MacOS**

  - Profil: **Virüsten koruma** -MacOS Için [Virüsten koruma ilkesi ayarlarını](../protect/antivirus-microsoft-defender-settings-macos.md) yönetin.

    [Mac Için Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)'yi kullandığınızda, dosyaları kullanarak bu ayarları yapılandırmak yerine, yönetilen MacOS cihazlarınıza Intune aracılığıyla bir virüsten koruma ayarları yapılandırabilir ve dağıtabilirsiniz `.plist` .

**Windows 10**:

- Platform: **Windows 10 profilleri**

  - Profil: **Microsoft Defender virüsten koruma** -Windows 10 Için [Virüsten koruma ilkesi ayarlarını](../protect/antivirus-microsoft-defender-settings-windows.md) yönetin.

    Defender virüsten koruma, Microsoft Defender Gelişmiş tehdit koruması 'nın (Microsoft Defender ATP) yeni nesil koruma bileşenidir. Yeni nesil koruma, kurumsal kuruluşunuzdaki cihazları korumak için makine öğrenimi ve bulut altyapısı gibi teknolojiler sunar.

    *Microsoft Defender virüsten koruma* profili, cihaz yapılandırma Ilkesinin *cihaz kısıtlama profilinde* bulunan virüsten koruma ayarlarının ayrı bir örneğidir.
  
    Bir *cihaz kısıtlama profilindeki*virüsten koruma ayarlarından farklı olarak, bu ayarları ortak yönetilen cihazlarla kullanabilirsiniz. Bu ayarları kullanmak için, Endpoint Protection için [ortak yönetim iş yükü kaydırıcısının](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) Intune olarak ayarlanması gerekir.

  - Profil: **Microsoft Defender virüsten koruma dışlamaları** -yalnızca [Virüsten koruma dışlamaları](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions)için ilke ayarlarını yönetin.
  
    Bu ilkeyle, virüsten koruma dışlamalarını tanımlayan aşağıdaki Microsoft Defender virüsten koruma yapılandırma hizmeti sağlayıcılarının (CSP 'Ler) ayarlarını yönetebilirsiniz:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    Virüsten koruma için bu CSP 'Ler Ayrıca, özel durumlar için aynı ayarları içeren *Microsoft Defender virüsten koruma* ilkesi tarafından da yönetilir. Her iki ilke türünden (*Virüsten koruma* ve *Virüsten koruma hariç*) ayarlar [ilke birleştirmeye](#policy-merge-for-settings)tabidir ve ilgili cihazlar ve kullanıcılar için bir süper Dışlamalar kümesi oluşturur.

  - Profil: **Windows Güvenlik deneyimi**-son kullanıcıların Microsoft Defender Güvenlik Merkezi 'nde görüntüleyebilecekleri [Windows güvenlik uygulaması ayarlarını](../protect/antivirus-security-experience-windows-settings.md) ve aldıkları bildirimleri yönetin.

    Windows güvenlik uygulaması, makinenin sistem durumu ve güvenliği hakkında bildirimler sağlamak için bir dizi Windows güvenlik özelliği tarafından kullanılır. Güvenlik uygulamaları bildirimleri arasında güvenlik duvarları, virüsten koruma ürünleri, Windows Defender SmartScreen ve diğerleri bulunur.

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Configuration Manager tarafından yönetilen cihazlar *(önizlemede)*

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](includes/configmgr-antivirus-profiles.md)]

## <a name="policy-merge-for-settings"></a>Ayarlar için ilke birleştirme

Bazı virüsten koruma ilkesi ayarları *ilke birleştirmeyi*destekler. İlke birleştirme, aynı cihazlara birden çok ilke uygulanacaksa ve aynı ayarı yapılandırırken çakışmaların önlenmesine yardımcı olur. Intune, ilke birleştirmenin desteklediği ayarları, her kullanıcı veya cihaz için geçerli tüm ilkelerden alındığı şekilde değerlendirir. Bu ayarlar daha sonra tek bir ilke üst kümesi ile birleştirilir.

Örneğin, farklı virüsten koruma dosya yolu dışlamalarını tanımlayan üç ayrı virüsten koruma ilkesi oluşturursunuz. Sonuç olarak, üç ilke de aynı kullanıcıya atanır. Microsoft Defender dosya yolu dışlama CSP, ilke birleştirmeyi desteklediğinden, Intune, Kullanıcı için geçerli tüm ilkelerden dosya dışlamalarını değerlendirir ve birleştirir. Dışlamalar bir üst küme 'e eklenir ve tek dışlamaları listesi kullanıcıların cihazına gönderilir.

Bir ayar için ilke birleştirme desteklenmediğinde, bir çakışma meydana gelebilir. Çakışmalar, Kullanıcı veya cihazın ayar için herhangi bir ilke almamasını sağlayabilir. Örneğin, ilke birleştirme, eşleşen cihaz kimliklerinin (*Preventınstaldmatchingdevicıdıd*) yüklenmesini önlemek için CSP 'yi desteklemez. Bu CSP için yapılandırma birleştirmez ve ayrı olarak işlenir.

Ayrı olarak işlendiğinde, ilke çakışmaları aşağıdaki şekilde çözümlenir:

1. En güvenli ilke geçerlidir.
2. İki ilke eşit derecede güvenliyse, son değiştirilen ilke uygulanır.
3. Son değiştirilen ilke çakışmayı çözümleyemezse cihaza hiçbir ilke teslim edilemiyor.

### <a name="settings-and-csps-that-support-policy-merge"></a>İlke birleştirmeyi destekleyen ayarlar ve CSP 'Ler

Aşağıdaki ayarlar ilke birleştirmeyi destekler:

[Microsoft Defender virüsten koruma ilkeleri](../protect/antivirus-microsoft-defender-settings-windows.md)

- **Defender dışlama Için işlem** -CSP: [Defender/excludedprocesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **Taramaların ve gerçek zamanlı korumanın dışında tutulacak dosya uzantıları** -CSP: [Defender/ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Defender dosyaları ve hariç tutulacak klasörler** -CSP: [Defender/excludedpaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## <a name="antivirus-policy-reports"></a>Virüsten koruma ilkesi raporları

Virüsten koruma ilkesi raporları, uç nokta güvenliği virüsten koruma ilkeleriniz ve cihaz durumunuz hakkındaki durum ayrıntılarını görüntüler. Bu raporlar, Microsoft Endpoint Manager Yönetim Merkezi 'nin uç nokta güvenlik düğümünde bulunabilir.

Raporları görüntülemek için, [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nde uç nokta güvenliği ' ne gidin ve **Virüsten koruma**' yı seçin. Virüsten koruma seçildiğinde Özet sayfası açılır. Ek sayfalar olarak ek rapor ve durum görünümleri mevcuttur.

### <a name="summary"></a>Özet

**Özet** sayfasında, [yeni ilkeler oluşturabilir](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) ve daha önce oluşturulmuş ilkelerin bir listesini görüntüleyebilirsiniz. Liste, ilkenin içerdiği profille ilgili üst düzey ayrıntıları (Ilke türü) ve ilke atanmışsa içerir.

![Virüsten koruma ilkesinin Özet sayfası](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

Listeden bir ilke seçtiğinizde, bu ilke örneğinin *genel bakış* sayfası açılır ve daha fazla bilgi görüntülenir. Bu görünümden bir kutucuk seçildikten sonra, Intune varsa, bu profilin ek ayrıntılarını görüntüler.

![Virüsten koruma ilkesinin genel bakış sayfası](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Windows 10 sağlıksız uç noktalar

**Windows 10 sağlıksız uç noktalar** SAYFASıNDA, MDM Ile yönetilen Windows 10 cihazlarınızın virüsten koruma durumu hakkında bilgi görüntüleyebilirsiniz. Bu bilgiler, *tehdit Aracısı durumu*olarak cihazda çalışan Windows Defender virüsten koruma 'dan döndürülür.

Bu görünümde yalnızca algılanan sorunları olan cihazlar görüntülenir. Bu görünüm, temiz olarak tanımlanan cihazların ayrıntılarını görüntülemez.

![Virüsten koruma ilkesinin sağlıksız uç noktaları sayfası](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Sonraki adımlar

[Uç nokta güvenlik ilkelerini yapılandırma](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)