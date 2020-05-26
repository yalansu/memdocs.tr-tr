---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle Endpoint Detection ve yanıt ayarlarını yönetme | Microsoft Docs
description: Microsoft Uç Nokta Yöneticisi 'nde uç nokta güvenlik uç noktası algılama ve yanıt ilkesiyle yönettiğiniz cihazlar için ilkeleri yapılandırın ve dağıtın.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
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
ms.openlocfilehash: 063d7fbbd5572e1ff2399efc161d319c6c9c5c1b
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824138"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için uç nokta algılama ve yanıt ilkesi

Microsoft Defender Gelişmiş tehdit koruması 'nı (Defender ATP) Intune ile tümleştirdiğinizde, EDR ayarlarını yönetmek ve cihazları Defender ATP 'ye eklemek için uç nokta algılama ve yanıt (EDR) için uç nokta güvenlik ilkeleri kullanabilirsiniz.

Defender ATP uç nokta algılama ve yanıtının özellikleri, gerçek zamanlı ve eyleme dönüştürülebilir gelişmiş saldırı algılamalarını sağlar. Güvenlik analistleri uyarıları etkin bir şekilde önceliklendirebilir, ihlalin tam kapsamına yönelik görünürlük elde edebilir ve tehditleri düzeltmek için yanıt işlemleri gerçekleştirebilir.

EDR ilkeleri, EDR ayarlarını yönetmek için platforma özel profiller içerir. Profiller, Defender ATP için bir *ekleme paketi* otomatik olarak içerir. Ekleme paketleri, cihazların Defender ATP ile çalışacak şekilde nasıl yapılandırıldığı. Bir cihaz ontahtalarından sonra, bu cihazdan tehdit verilerini kullanmaya başlayabilirsiniz.

EDR ilkeleri, Intune ile yönettiğiniz Azure Active Directory (Azure AD) cihaz gruplarına ve Windows Server 'lar dahil Configuration Manager ile yönettiğiniz şirket içi cihazların koleksiyonlarına dağıtılır. Farklı yönetim yolları için EDR ilkeleri farklı ekleme paketleri gerektirir. Bu nedenle, yönettiğiniz farklı cihaz türleri için ayrı bir EDR ilkesi oluşturacaksınız.

> [!TIP]
> Configuration Manager ile yönettiğiniz cihazlar için destek *genel önizlemededir*.

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin **uç nokta güvenlik** düğümünde, EDR için uç nokta güvenlik ilkelerini bulun. *Manage*

[Uç nokta algılama ve yanıt profillerinin ayarlarını](../protect/endpoint-security-edr-profile-settings.md)görüntüleyin.

## <a name="prerequisites-for-edr-policies"></a>EDR ilkeleri önkoşulları

**Genel**:

- **Microsoft Defender Gelişmiş tehdit koruması Için kiracı** -EDR ilkeleri oluşturabilmeniz IÇIN Defender ATP kiracınız Microsoft Endpoint Manager kiracınızla (Intune aboneliğiniz) tümleştirilemelidir. Bkz. Intune belgelerinde [Microsoft Defender ATP kullanma](../protect/advanced-threat-protection.md) .

**Configuration Manager cihazları desteklemek için**:

Configuration Manager cihazlarla EDR ilkelerini kullanmayı desteklemek için, Configuration Manager ortamınız aşağıdaki ek yapılandırmalara gerek duyar. [Yapılandırma kılavuzu](#set-up-configuration-manager-to-support-edr-policy) Bu makalede verilmiştir:

- **Sürüm 2002 veya üzeri ile Configuration Manager** : sitenizin Configuration Manager 2002 veya üzeri bir sürümü çalıştırması gerekir.

- **Configuration Manager güncelleştirmesini yüklemek** -Microsoft Endpoint Manager Yönetim merkezinde oluşturduğunuz EDR ilkesini kullanmak için Configuration Manager 2002 ' de desteği etkinleştirmek üzere, aşağıdaki güncelleştirmeyi Configuration Manager konsolundan yükleyebilirsiniz:
  - **Configuration Manager 2002 düzeltme (KB4563473)**

- **Kiracı eklemeyi yapılandırma** -kiracı iliştirme, Configuration Manager cihaz koleksiyonlarını Microsoft Endpoint Manager yönetim merkezine eşitlemenize olanak tanır. Daha sonra bu koleksiyonlara EDR ilkeleri dağıtmak için yönetim merkezini kullanabilirsiniz.

  Kiracı iliştirme genellikle ortak yönetim ile yapılandırılır, ancak kiracı eklemeyi kendi kendine yapılandırabilirsiniz.

- **Configuration Manager koleksiyonlarını eşitler** – kiracı eklemeyi yapılandırırken, Microsoft Endpoint Manager Yönetim Merkezi ile eşitlenmek üzere Configuration Manager cihaz koleksiyonlarını seçebilirsiniz. Ayrıca, eşitlediğiniz cihaz koleksiyonlarını değiştirmek için daha sonra geri dönebilirsiniz. Configuration Manager cihazlar için EDR ilkesi, yalnızca eşitlediğiniz koleksiyonlara atanabilir.

  Eşitlenmek üzere koleksiyonlar seçildikten sonra, bunları Microsoft Defender ATP ile kullanım için etkinleştirmeniz gerekir.

- **Azure AD izinleri** -kiracı iliştirme kurulumunu tamamlamaya ve Microsoft Endpoint Manager Yönetim Merkezi ile eşitleyeceğiniz Configuration Manager koleksiyonları yapılandırmaya yönelik Izinler, Azure aboneliğiniz Için genel yönetici izinlerine sahip bir hesap gerekir.

## <a name="edr-profiles"></a>EDR profilleri

Aşağıdaki platformlar ve profiller için yapılandırabileceğiniz [ayarları görüntüleyin](../protect/endpoint-security-edr-profile-settings.md) .

**Intune** – Intune ile yönettiğiniz cihazlar için aşağıdakiler desteklenir:

- Platform: **Windows 10 ve üzeri** -Intune, ILKEYI Azure AD gruplarınızdaki cihazlara dağıtır.
- Profil: **Endpoint Detection ve yanıt (MDM)**

**Configuration Manager** *(önizlemede)* : Configuration Manager ile yönettiğiniz cihazlarda aşağıdakiler desteklenir:

- Platform: **Windows 10 ve Windows Server** -Configuration Manager ilkeyi Configuration Manager Koleksiyonlarınızdaki cihazlara dağıtır.
- Profil: **Endpoint Detection ve yanıt (ConfigMgr) (Önizleme)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>EDR ilkesini desteklemek için Configuration Manager ayarlama

Configuration Manager cihazlara EDR ilkeleri dağıtabilmeniz için önce aşağıdaki bölümlerde açıklanan yapılandırma ayrıntılarını doldurun.

Bu yapılandırma Configuration Manager konsolunda ve Configuration Manager dağıtımınız içinde yapılır. Configuration Manager hakkında bilgi sahibi değilseniz, bu görevleri tamamlamaya yönelik bir Configuration Manager Yöneticisi ile çalışmayı planlayın.  

Aşağıdaki bölümler gerekli görevleri kapsar:

1. [Configuration Manager için güncelleştirmeyi yükler](#task-1-install-the-update-for-configuration-manager)
2. [Kiracı eklemeyi etkinleştirme](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Eşitlenmek üzere koleksiyonları seçin](#task-3-select-collections-to-synchronize)
4. [Microsoft Defender ATP için koleksiyonları etkinleştir](#task-4-enable-collections-for-microsoft-defender-atp)

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

Ortak yönetim önceden etkinleştirildiyse, kiracı iliştirme zaten ayarlanmıştır ve [görev 3](#task-3-select-collections-to-synchronize)' e atlayabilirsiniz.

Kiracı iliştirme ile, Microsoft Endpoint Manager Yönetim Merkezi ile eşitlenmek üzere Configuration Manager dağıtımınıza ait cihaz koleksiyonlarını belirtirsiniz. Koleksiyonlar eşitlendikten sonra, bu cihazlarla ilgili bilgileri görüntülemek ve bir Intune 'dan EDR ilkesi dağıtmak için yönetim merkezini kullanın.  

Kiracı iliştirme senaryosu hakkında daha fazla bilgi için bkz. Configuration Manager içerikte [kiracı eklemeyi etkinleştirme](../../configmgr/tenant-attach/device-sync-actions.md) .

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Ortak yönetim etkin olmadığında kiracı eklemeyi etkinleştir

> [!TIP]
> Kiracı eklemeyi etkinleştirmek için Configuration Manager konsolundaki **ortak yönetim Yapılandırma Sihirbazı** 'nı kullanın, ancak ortak yönetimi etkinleştirmeniz gerekmez.

Ortak yönetimi etkinleştirmeyi planlıyorsanız, ortak yönetimi, önkoşulları ve devam etmeden önce iş yüklerini yönetme hakkında bilgi sahibi olun. Configuration Manager belgelerinde [ortak yönetim nedir?](../../configmgr/comanage/overview.md) konusuna bakın.

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.
2. Şeritte, Sihirbazı açmak için **ortak yönetimi yapılandırma** ' ya tıklayın.
3. **Kiracı ekleme** sayfasında, ortamınız için **AzurePublicCloud** ' yi seçin. Azure Kamu Bulutu desteklenmez.
   1. **Oturum Aç**’a tıklayın. Oturum açmak için *genel yönetici* hesabınızı kullanın.

   2. **Kiracı ekleme** sayfasında **Microsoft Endpoint Manager yönetim merkezine yükle** seçeneğinin seçili olduğundan emin olun.

   3. **Ortak yönetim için otomatik istemci kaydını etkinleştir**onay kutusundan Kaldır.

      Bu seçenek belirlendiğinde, sihirbaz ortak yönetim kurulumunu tamamlamaya yönelik ek sayfalar sunar. Daha fazla bilgi için bkz. Configuration Manager içerikte [ortak yönetimi etkinleştirme](../../configmgr/comanage/how-to-enable.md) .

     ![Kiracı eklemeyi Yapılandır](./media/endpoint-security-edr-policy/tenant-onboarding.png)

4. **AAD uygulaması oluştur** bildirimini kabul etmek için **İleri** ' ye ve ardından **Evet** ' e tıklayın. Bu eylem, bir hizmet sorumlusu sağlar ve koleksiyonların Microsoft Endpoint Manager yönetim merkezine eşitlenmesini kolaylaştırmak için bir Azure AD uygulama kaydı oluşturur.

5. **Karşıya yüklemeyi Yapılandır** sayfasında, hangi koleksiyonları eşitlemek istediğinizi yapılandırın. Yapılandırmanızı bir veya birkaç cihaz koleksiyonlarıyla sınırlayabilir veya **Microsoft uç nokta tarafından yönetilen tüm Cihazlarım**için önerilen cihaz yükleme ayarını kullanabilirsiniz Configuration Manager.

6. Seçiminizi gözden geçirmek için **Özet** ' e tıklayın ve ardından **İleri**' ye tıklayın.

7. Sihirbaz tamamlandığında **Kapat**' a tıklayın.

   Kiracı iliştirme artık yapılandırılmıştır ve seçilen koleksiyonlar Microsoft Endpoint Manager yönetim merkezine eşitlenir.

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>Ortak yönetimi kullanırken kiracı eklemeyi etkinleştirin

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.

2. Ortak yönetim ayarlarınıza sağ tıklayıp **Özellikler**' i seçin.

3. **Karşıya yüklemeyi Yapılandır** sekmesinde, **Microsoft Endpoint Manager yönetim merkezine yükle**' yi seçin. **Uygula**’ya tıklayın.
   - Cihaz yükleme için varsayılan ayar, **Microsoft uç nokta Configuration Manager tarafından yönetilen tüm cihazlardır**. Yapılandırmanızı bir veya birkaç cihaz koleksiyonu ile sınırlandırmayı da tercih edebilirsiniz.

     ![Ortak yönetim özellikleri sekmesini görüntüleme](./media/endpoint-security-edr-policy/configure-upload.png)

4. İstendiğinde *genel yönetici* hesabınızla oturum açın.

5. **AAD uygulaması oluştur** bildirimini kabul etmek için **Evet** ' e tıklayın. Bu eylem, bir hizmet sorumlusu sağlar ve eşitlemeyi kolaylaştırmak için bir Azure AD uygulama kaydı oluşturur.

6. Değişiklik yapmayı tamamladıktan sonra ortak yönetim özelliklerinden çıkmak için **Tamam** ' ı tıklatın.

   Kiracı iliştirme artık yapılandırılmıştır ve seçilen koleksiyonlar Microsoft Endpoint Manager yönetim merkezine eşitlenir.

### <a name="task-3-select-collections-to-synchronize"></a>3. görev: eşitlenmek üzere koleksiyonları seçme

Kiracı iliştirme yapılandırıldığında eşitlenecek koleksiyonları seçebilirsiniz. Zaten koleksiyonları eşitleyemiyorsanız veya hangilerinin eşitlemesini yeniden yapılandırmanız gerekiyorsa, Configuration Manager konsolundaki ortak yönetim özelliklerini düzenleyebilirsiniz.

#### <a name="select-collections"></a>Koleksiyon Seç

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.

2. Ortak yönetim ayarlarınıza sağ tıklayıp **Özellikler**' i seçin.

3. **Karşıya yüklemeyi Yapılandır** sekmesinde, **Microsoft Endpoint Manager yönetim merkezine yükle**' yi seçin. **Uygula**’ya tıklayın.

   Cihaz yükleme için varsayılan ayar, **Microsoft uç nokta Configuration Manager tarafından yönetilen tüm cihazlardır**. Yapılandırmanızı bir veya birkaç cihaz koleksiyonu ile sınırlandırmayı da tercih edebilirsiniz.

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>Görev 4: Microsoft Defender ATP için koleksiyonları etkinleştirme

Koleksiyonları Microsoft Endpoint Manager yönetim merkezine eşitlenecek şekilde yapılandırdıktan sonra, bu koleksiyonların ekleme ve Microsoft Defender ATP ilkelerine uygun olması için yine de etkinleştirilmesi gerekir.  Bunu yapmak için Configuration Manager konsolundaki her bir koleksiyonun özelliklerini düzenlersiniz.

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Gelişmiş tehdit koruması ile kullanım için koleksiyonları etkinleştirme

1. Üst düzey sitenize bağlı bir Configuration Manager konsolundan, Microsoft Endpoint Manager Yönetim Merkezi 'ne eşitlediğiniz bir cihaz koleksiyonuna sağ tıklayıp **Özellikler**' i seçin.

2. **Bulut eşitleme** sekmesinde, **Bu koleksiyonun Intune 'DA Microsoft Defender ATP ilkeleri atamasını sağlamak Için kullanılabilir hale getirme**seçeneğini etkinleştirin.

   - Configuration Manager hiyerarşiniz kiracı ekli değilse bu seçeneği seçemezsiniz.
  
   ![Bulut eşitlemesini yapılandırma](./media/endpoint-security-edr-policy/cloud-sync.png)

3. Yapılandırmayı kaydetmek için **Tamam ' ı** seçin.

   Bu koleksiyondaki cihazlar artık Microsoft Defender ATP ilkesini alabilir.

## <a name="create-and-deploy-edr-policies"></a>EDR ilkeleri oluşturma ve dağıtma

Microsoft Defender ATP aboneliğiniz Intune ile tümleşikse, EDR ilkeleri oluşturabilir ve dağıtabilirsiniz. Oluşturabileceğiniz iki farklı EDR ilkesi türü vardır. MDM aracılığıyla Intune ile yönettiğiniz cihazlar için bir ilke türü. İkinci tür Configuration Manager ile yönettiğiniz cihazlar içindir.

İlke için platformu seçtiğinizde yeni bir EDR ilkesi oluştururken oluşturduğunuz ilke türünü seçersiniz.

İlkeyi Configuration Manager tarafından yönetilen cihazlara dağıtabilmeniz için önce, Microsoft Endpoint Manager Yönetim Merkezi ' nden [EDR ilkesini destekleyecek Configuration Manager ayarlayın](#set-up-configuration-manager-to-support-edr-policy) .

### <a name="create-edr-policies"></a>EDR ilkeleri oluşturma

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.

2. **Uç nokta güvenlik**  >  **uç noktası algılama ve yanıt**  >  **oluşturma ilkesi**seçin.

3. İlkenizin için platformu ve profili seçin. Aşağıdaki bilgiler, seçeneklerinizi tanımlar:

   - Intune-Intune, ilkeyi Azure AD gruplarınızdaki cihazlara dağıtır. İlkeyi oluştururken şunları seçin:
     - Platform: **Windows 10 ve üzeri**
     - Profil: **Endpoint Detection ve yanıt (MDM)**

   - Configuration Manager-Configuration Manager ilkeyi Configuration Manager Koleksiyonlarınızdaki cihazlara dağıtır. İlkeyi oluştururken şunları seçin:
     - Platform: **Windows 10 ve Windows Server**
     - Profil: **Endpoint Detection ve yanıt (ConfigMgr) (Önizleme)**

4. **Oluştur**’u seçin.

5. **Temel bilgiler** sayfasında, profil için bir ad ve açıklama girin ve ardından **İleri**' yi seçin.

6. **Yapılandırma ayarları** sayfasında, bu profille yönetmek istediğiniz ayarları yapılandırın. Ekleme paketi otomatik olarak eklenir ve yapılandırabileceğiniz bir şey değildir.

   Ayarları yapılandırmayı tamamladıktan **sonra ileri**' yi seçin.

7. *Bu adım yalnızca **Endpoint Detection ve yanıt (MDM)** profili için geçerlidir*:  

   **Kapsam etiketleri sayfasında,** kapsam etiketlerini profile atamak için kapsam etiketlerini **Seç** ' *i seçin.*
  
   Devam etmek için **İleri**’yi seçin.

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

- **Windows 10 ve Windows Server** platformunu (Configuration Manager) hedefleyen ilkeler için, ilkeye yönelik uyumluluğa bir genel bakış görürsünüz, ancak ek ayrıntıları görüntülemek için ayrıntıya gidebilirsiniz. Yönetim Merkezi, ilkenin Configuration Manager cihazlara dağıtımını yöneten Configuration Manager 'dan sınırlı durum ayrıntılarını aldığından görünüm sınırlıdır.

Hem platformlar hem de profiller için yapılandırabileceğiniz [ayarları görüntüleyin](../protect/endpoint-security-edr-profile-settings.md) .

## <a name="next-steps"></a>Sonraki adımlar

- [Uç nokta güvenlik ilkelerini yapılandırma](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
- Microsoft Defender ATP belgelerindeki [uç nokta algılama ve yanıt](https://docs.microsoft.com/windows/security/-threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) hakkında daha fazla bilgi edinin.
