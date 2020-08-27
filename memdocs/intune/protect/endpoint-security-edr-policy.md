---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle Endpoint Detection ve yanıt ayarlarını yönetme | Microsoft Docs
description: Microsoft Uç Nokta Yöneticisi 'nde uç nokta güvenlik uç noktası algılama ve yanıt ilkesiyle yönettiğiniz cihazlar için ilkeleri yapılandırın ve dağıtın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: ff880b564562b3e6d67dc852f97ef7a9f5d6b814
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915050"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için uç nokta algılama ve yanıt ilkesi

Microsoft Defender Gelişmiş tehdit koruması 'nı (Microsoft Defender ATP) Intune ile tümleştirdiğinizde, EDR ayarlarını yönetmek ve cihazları Microsoft Defender ATP 'ye eklemek için uç nokta algılama ve yanıt (EDR) için uç nokta güvenlik ilkeleri kullanabilirsiniz.

Microsoft Defender ATP uç noktası algılama ve yanıtının özellikleri, gerçek zamanlı ve eyleme dönüştürülebilir gelişmiş saldırı algılamalarını sağlar. Güvenlik analistleri uyarıları etkin bir şekilde önceliklendirebilir, ihlalin tam kapsamına yönelik görünürlük elde edebilir ve tehditleri düzeltmek için yanıt işlemleri gerçekleştirebilir.

EDR ilkeleri, EDR ayarlarını yönetmek için platforma özel profiller içerir. Profiller, Microsoft Defender ATP için bir *ekleme paketini* otomatik olarak içerir. Ekleme paketleri, cihazların Microsoft Defender ATP ile çalışacak şekilde nasıl yapılandırıldığı. Bir cihaz ontahtalarından sonra, bu cihazdan tehdit verilerini kullanmaya başlayabilirsiniz.

EDR ilkeleri, Intune ile yönettiğiniz Azure Active Directory (Azure AD) cihaz gruplarına ve Windows Server 'lar dahil Configuration Manager ile yönettiğiniz şirket içi cihazların koleksiyonlarına dağıtılır. Farklı yönetim yolları için EDR ilkeleri farklı ekleme paketleri gerektirir. Bu nedenle, yönettiğiniz farklı cihaz türleri için ayrı bir EDR ilkesi oluşturacaksınız.

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin **uç nokta güvenlik** düğümünde, EDR için uç nokta güvenlik ilkelerini bulun. *Manage*

[Uç nokta algılama ve yanıt profillerinin ayarlarını](endpoint-security-edr-profile-settings.md)görüntüleyin.

## <a name="prerequisites-for-edr-policies"></a>EDR ilkeleri önkoşulları

**Genel**:

- **Microsoft Defender Gelişmiş tehdit koruması Için kiracı** – EDR ilkeleri oluşturabilmeniz Için MICROSOFT Defender ATP kiracınız Microsoft Endpoint Manager kiracınızla (Intune aboneliğiniz) tümleştirilemelidir. Bkz. Intune belgelerinde [Microsoft Defender ATP kullanma](advanced-threat-protection.md) .

**Configuration Manager istemcileri Için destek**:

- **Configuration Manager cihazlar için kiracı eklemeyi ayarlama** -EDR ilkesinin Configuration Manager tarafından yönetilen cihazlara dağıtılmasını desteklemek için *kiracı eklemeyi*yapılandırın. Bu, Intune 'dan Endpoint Security ilkelerini desteklemek için Configuration Manager cihaz koleksiyonlarının yapılandırılmasını içerir.

  Configuration Manager koleksiyonlarının Microsoft Endpoint Manager yönetim merkezine eşitlenmesi ve uç nokta güvenlik ilkeleriyle çalışmasını sağlamak dahil olmak üzere kiracı ekleme 'yi ayarlamak için bkz. [Endpoint Protection ilkelerini desteklemek için kiracı eklemeyi yapılandırma](../protect/tenant-attach-intune.md).

## <a name="edr-profiles"></a>EDR profilleri

Aşağıdaki platformlar ve profiller için yapılandırabileceğiniz [ayarları görüntüleyin](endpoint-security-edr-profile-settings.md) .

**Intune** – Intune ile yönettiğiniz cihazlar için aşağıdakiler desteklenir:

- Platform: **Windows 10 ve üzeri** -Intune, ILKEYI Azure AD gruplarınızdaki cihazlara dağıtır.
- Profil: **Endpoint Detection ve yanıt (MDM)**

**Configuration Manager** , Configuration Manager yönettiğiniz cihazlarda aşağıdakiler desteklenir:

- Platform: **Windows 10 ve Windows Server (ConfigMgr)** -Configuration Manager ilkeyi Configuration Manager Koleksiyonlarınızdaki cihazlara dağıtır.
- Profil: **Endpoint Detection ve yanıt (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>EDR ilkesini desteklemek için Configuration Manager ayarlama

Configuration Manager cihazlara EDR ilkeleri dağıtabilmeniz için önce aşağıdaki bölümlerde açıklanan yapılandırma ayrıntılarını doldurun.

Bu yapılandırma Configuration Manager konsolunda ve Configuration Manager dağıtımınız içinde yapılır. Configuration Manager hakkında bilgi sahibi değilseniz, bu görevleri tamamlamaya yönelik bir Configuration Manager Yöneticisi ile çalışmayı planlayın.  

Aşağıdaki bölümler gerekli görevleri kapsar:

1. [Configuration Manager için güncelleştirmeyi yükler](#task-1-install-the-update-for-configuration-manager)
2. [Kiracı eklemeyi etkinleştirme](#task-2-configure-tenant-attach-and-synchronize-collections)  

> [!TIP]
> Microsoft Defender ATP 'yi Configuration Manager kullanma hakkında daha fazla bilgi için Configuration Manager içeriğinde aşağıdaki makalelere bakın:
>
> - [Microsoft Endpoint Manager Yönetim Merkezi aracılığıyla Microsoft Defender ATP 'ye Configuration Manager istemcileri ekleme](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Uç Nokta Yöneticisi kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Görev 1: Configuration Manager için güncelleştirmeyi yükler

Configuration Manager sürüm 2002, Microsoft Endpoint Manager yönetim merkezinden dağıttığınız uç nokta algılama ve yanıt ilkeleriyle kullanımı desteklemek için bir güncelleştirme gerektirir.

**Güncelleştirme ayrıntıları**:

- **Configuration Manager 2002 düzeltme (KB4563473)**

Bu güncelleştirmeyi, Configuration Manager 2002 için *konsol içi bir güncelleştirme* olarak bulacaksınız.

Bu güncelleştirmeyi yüklemek için Configuration Manager belgelerine [konsol içi güncelleştirmeleri yüklemeyin](../../configmgr/core/servers/manage/install-in-console-updates.md) bölümündeki yönergeleri izleyin.

Güncelleştirmeyi yükledikten sonra, ortamınızı Microsoft Endpoint Manager Yönetim Merkezi ' nden EDR ilkesini destekleyecek şekilde yapılandırmaya devam etmek için buraya dönün.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Görev 2: kiracı eklemeyi ve koleksiyonları eşitlemeyi yapılandırma

Kiracı iliştirme ile, Microsoft Endpoint Manager Yönetim Merkezi ile eşitlenmek üzere Configuration Manager dağıtımınıza ait cihaz koleksiyonlarını belirtirsiniz. Koleksiyonlar eşitlendikten sonra, bu cihazlarla ilgili bilgileri görüntülemek ve bir Intune 'dan EDR ilkesi dağıtmak için yönetim merkezini kullanın.  

Kiracı iliştirme senaryosu hakkında daha fazla bilgi için bkz. Configuration Manager içerikte [kiracı eklemeyi etkinleştirme](../../configmgr/tenant-attach/device-sync-actions.md) .

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Ortak yönetim etkin olmadığında kiracı eklemeyi etkinleştir

> [!TIP]
> Kiracı eklemeyi etkinleştirmek için Configuration Manager konsolundaki **ortak yönetim Yapılandırma Sihirbazı** 'nı kullanın, ancak ortak yönetimi etkinleştirmeniz gerekmez.

Ortak yönetimi etkinleştirmeyi planlıyorsanız, ortak yönetimi, önkoşulları ve devam etmeden önce iş yüklerini yönetme hakkında bilgi sahibi olun. Configuration Manager belgelerinde [ortak yönetim nedir?](../../configmgr/comanage/overview.md) konusuna bakın.

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.
2. Şeritte, Sihirbazı açmak için **ortak yönetimi yapılandırma** ' ya tıklayın.
3. **Kiracı ekleme** sayfasında, ortamınız için **AzurePublicCloud** ' yi seçin. Azure Kamu Bulutu desteklenmez.
   1. **Oturum aç**' a tıklayın. Oturum açmak için *genel yönetici* hesabınızı kullanın.

Intune ile yönettiğiniz cihazlar için aşağıdakiler desteklenir:

- Platform: **Windows 10 ve üzeri** -Intune, ILKEYI Azure AD gruplarınızdaki cihazlara dağıtır.
  - Profil: **Endpoint Detection ve yanıt (MDM)**

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Configuration Manager tarafından yönetilen cihazlar *(önizlemede)*

Aşağıdaki, *kiracı iliştirme* senaryosu aracılığıyla Configuration Manager yönettiğiniz cihazlarda desteklenir:

- Platform: **Windows 10 ve Windows Server (ConfigMgr)** -Configuration Manager ilkeyi Configuration Manager Koleksiyonlarınızdaki cihazlara dağıtır.
  - Profil: **Endpoint Detection ve yanıt (ConfigMgr) (Önizleme)**

## <a name="create-and-deploy-edr-policies"></a>EDR ilkeleri oluşturma ve dağıtma

Microsoft Defender ATP aboneliğinizi Intune ile tümleştirdiğinizde, EDR ilkeleri oluşturabilir ve dağıtabilirsiniz. Oluşturabileceğiniz iki farklı EDR ilkesi türü vardır. MDM aracılığıyla Intune ile yönettiğiniz cihazlar için bir ilke türü. İkinci tür Configuration Manager ile yönettiğiniz cihazlar içindir.

İlke için bir platform seçerek yeni bir EDR ilkesi yapılandırılırken oluşturulacak ilke türünü seçersiniz.

İlkeyi Configuration Manager tarafından yönetilen cihazlara dağıtabilmeniz için önce, Microsoft Endpoint Manager Yönetim Merkezi ' nden EDR ilkesini destekleyecek Configuration Manager ayarlayın. Bkz. [Endpoint Protection ilkelerini desteklemek için kiracı eklemeyi yapılandırma](../protect/tenant-attach-intune.md).


### <a name="create-edr-policies"></a>EDR ilkeleri oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Uç nokta güvenlik**  >  **uç noktası algılama ve yanıt**  >  **oluşturma ilkesi**seçin.

3. İlkenizin için platformu ve profili seçin. Aşağıdaki bilgiler, seçeneklerinizi tanımlar:

   - Intune-Intune, ilkeyi Azure AD gruplarınızdaki cihazlara dağıtır. İlkeyi oluştururken şunları seçin:
     - Platform: **Windows 10 ve üzeri**
     - Profil: **Endpoint Detection ve yanıt (MDM)**

   - Configuration Manager-Configuration Manager ilkeyi Configuration Manager Koleksiyonlarınızdaki cihazlara dağıtır. İlkeyi oluştururken şunları seçin:
     - Platform: **Windows 10 ve Windows Server (ConfigMgr)**
     - Profil: **Endpoint Detection ve yanıt (ConfigMgr)**

4. **Oluştur**’u seçin.

5. **Temel bilgiler** sayfasında, profil için bir ad ve açıklama girin ve ardından **İleri**' yi seçin.

6. **Yapılandırma ayarları** sayfasında, bu profille yönetmek istediğiniz ayarları yapılandırın. Ekleme paketi otomatik olarak eklenir ve yapılandırabileceğiniz bir şey değildir.

   Ayarları yapılandırmayı tamamladıktan **sonra ileri**' yi seçin.

7. *Bu adım yalnızca **Endpoint Detection ve yanıt (MDM)** profili için geçerlidir*:  

   **Kapsam etiketleri sayfasında,** kapsam etiketlerini profile atamak için kapsam etiketlerini **Seç** ' *i seçin.*
  
   Devam etmek için **İleri** seçeneğini belirleyin.

8. **Atamalar** sayfasında, bu ilkeyi alacak grupları veya koleksiyonları seçin. Seçim, seçtiğiniz platforma ve profile bağlıdır:

   - Intune için Azure AD 'den grupları seçersiniz.
   - Configuration Manager için, Microsoft Endpoint Manager Yönetim Merkezi ile eşitlenen ve Microsoft Defender ATP ilkesi için etkinleştirilen Configuration Manager koleksiyonları seçersiniz.

   Şu anda grup veya koleksiyonlar atamamalı ve daha sonra bir atama eklemek için ilkeyi düzenleyeseçemezsiniz.

   Devam etmeye hazırsanız **İleri**' yi seçin.

9. **Gözden geçir + oluştur** sayfasında, Işiniz bittiğinde **Oluştur**' u seçin.

   Oluşturduğunuz profilin ilke türünü seçtiğinizde yeni profil listede görüntülenir.

## <a name="edr-policy-reports"></a>EDR ilke raporları

Microsoft Endpoint Manager Yönetim merkezinde dağıttığınız EDR ilkeleriyle ilgili ayrıntıları görüntüleyebilirsiniz. Ayrıntıları görüntülemek için **uç nokta güvenlik**  >  **uç noktası dağıtımı ve yanıt**' a gidin ve uyumluluk ayrıntılarını görüntülemek istediğiniz ilkeyi seçin:

- **Windows 10 ve üzeri** platformu (Intune) hedefleyen ilkeler için, ilkeye uyumluluğa bir genel bakış görürsünüz. Ayrıca, ilkeyi alan cihazların listesini görüntülemek için grafiği ve daha fazla ayrıntı için ayrı cihazlarda detaya gitmeyi seçebilirsiniz.

  **ATP algılayıcısı olan cihazlar** için grafik, yalnızca **Windows 10 ve üzeri** PROFIL kullanılarak Microsoft Defender ATP 'ye başarıyla eklenen cihazları görüntüler. Bu grafikteki cihazlarınızın tam gösterimine sahip olduğunuzdan emin olmak için, ekleme profilini tüm cihazlarınıza dağıtın. Grup ilkesi veya PowerShell gibi dış yollarla, Microsoft Defender 'a eklenen cihazlar **ATP algılayıcısı olmadan cihaz**olarak sayılır.

- **Windows 10 ve Windows Server (ConfigMgr)** platformunu (Configuration Manager) hedefleyen ilkeler için, ilkeye uyumluluğa ilişkin bir genel bakış görürsünüz, ancak ek ayrıntıları görüntülemek için ayrıntıya gidebilirsiniz. Yönetim Merkezi, ilkenin Configuration Manager cihazlara dağıtımını yöneten Configuration Manager 'dan sınırlı durum ayrıntılarını aldığından görünüm sınırlıdır.

Hem platformlar hem de profiller için yapılandırabileceğiniz [ayarları görüntüleyin](endpoint-security-edr-profile-settings.md) .

## <a name="next-steps"></a>Sonraki adımlar

- [Uç nokta güvenlik ilkelerini yapılandırma](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Microsoft Defender ATP belgelerindeki [uç nokta algılama ve yanıt](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) hakkında daha fazla bilgi edinin.