---
title: Intune ilkelerini kiracı ekli Configuration Manager cihazları ile kullanma | Microsoft Docs
description: Configuration Manager cihazların kiracı iliştirme 'sini Microsoft Endpoint Manager yönetim merkezine yapılandırarak, bu cihazlara Microsoft Intune desteklenen ilkeleri dağıtabilirsiniz.
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
ms.openlocfilehash: 5c3d5bd14efddc74e1898f374bbaac2aa962ebf7
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193674"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>Intune 'dan Endpoint Security ilkelerini desteklemek için kiracı eklemeyi yapılandırma

Configuration Manager kiracı iliştirme senaryosunu kullandığınızda, Intune 'dan uç nokta güvenlik ilkelerini, Configuration Manager yönettiğiniz cihazlara dağıtabilirsiniz. Bu senaryoyu kullanmak için, öncelikle Configuration Manager için kiracı eklemeyi yapılandırmanız ve cihaz koleksiyonlarını Intune ile kullanılmak üzere Configuration Manager için etkinleştirmeniz gerekir. Koleksiyonlar kullanım için etkinleştirildikten sonra, ilkeleri oluşturmak ve dağıtmak için Microsoft Endpoint Manager yönetim merkezini kullanırsınız.

Aşağıdaki ilke türleri, kiracının eklendiği Configuration Manager cihazlar tarafından desteklenir:

- Uç nokta güvenliği virüsten koruma ilkesi
- Uç nokta güvenlik uç noktası algılama ad yanıt ilkesi

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>Kiracı iliştirme için Intune ilkesi kullanma gereksinimleri

Intune uç nokta güvenlik ilkelerini Configuration Manager cihazlarla kullanmayı desteklemek için Configuration Manager ortamınız aşağıdaki konfigürasyonları gerektirir. [Yapılandırma kılavuzu](#set-up-configuration-manager-to-support-intune-policies) Bu makalede verilmiştir:

### <a name="general-requirements-for-tenant-attach"></a>Kiracı iliştirme için genel gereksinimler

- **Kiracı eklemeyi yapılandırma** - *kiracı iliştirme* senaryosu Ile Configuration Manager cihaz koleksiyonlarını Microsoft Endpoint Manager yönetim merkezine eşitler. Daha sonra bu koleksiyonlara desteklenen ilkeleri dağıtmak için yönetim merkezini kullanabilirsiniz.

  Kiracı iliştirme genellikle ortak yönetim ile yapılandırılır, ancak kiracı eklemeyi kendi kendine yapılandırabilirsiniz.

- **Configuration Manager koleksiyonlarını eşitler** – kiracı eklemeyi yapılandırırken, Microsoft Endpoint Manager Yönetim Merkezi ile eşitlenmek üzere Configuration Manager cihaz koleksiyonlarını seçebilirsiniz. Ayrıca, eşitlediğiniz cihaz koleksiyonlarını değiştirmek için daha sonra geri dönebilirsiniz. Configuration Manager cihazlar için desteklenen ilkeler yalnızca eşitlediğiniz koleksiyonlara atanabilir.

  Eşitlenmesi gereken koleksiyonları seçtikten sonra, bunları Intune 'dan Endpoint Security ilkeleriyle kullanmak üzere etkinleştirmelisiniz.

- **Azure AD izinleri** -kiracı iliştirme kurulumunu tamamlamaya yönelik olarak, Azure aboneliğiniz Için genel yönetici izinlerine sahip bir hesap gerekir.

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Intune Endpoint Security ilkeleri için özel gereksinimler

- **Virüsten koruma ilkesi** (*Önizleme*):

  - **Configuration Manager** -aşağıdaki ortamlar desteklenir:

    - **Configuration Manager geçerli dal sürümü 2006 veya üzeri** -bu güncel dal sürümüyle Intune virüsten koruma ilkeleri için destek eklendi.
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - Microsoft **Defender Gelişmiş tehdit koruması Için kiracı** – MICROSOFT Defender ATP kiracınız Microsoft Endpoint Manager kiracınızla (Intune aboneliğiniz) tümleştirilemelidir.  Bkz. Intune belgelerinde [Microsoft Defender ATP kullanma](advanced-threat-protection.md) .

- **Uç nokta algılama ve yanıt ilkesi**:

  - **Configuration Manager** -aşağıdaki ortamlar desteklenir:

    - **Configuration Manager Technical preview 2003 veya sonraki sürümler** -Intune Endpoint Detection ve yanıt ilkeleri için destek, technical preview Sürüm 2003 ile eklenmiştir.

    - **Geçerli dal sürümü 2002 veya üzeri Configuration Manager** -sürüm 2002 ile Configuration Manager kullanıyorsanız, konsol içi güncelleştirme **Configuration Manager 2002 düzeltmesini (KB4563473)** yüklemelisiniz. Bu güncelleştirme, uç nokta güvenlik ilkelerini kullanmak için Configuration Manager 2002 ' de desteği sunar.

  - Microsoft **Defender Gelişmiş tehdit koruması Için kiracı** – MICROSOFT Defender ATP kiracınız Microsoft Endpoint Manager kiracınızla (Intune aboneliğiniz) tümleştirilemelidir.  Bkz. Intune belgelerinde [Microsoft Defender ATP kullanma](advanced-threat-protection.md) .

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>Intune ilkelerini desteklemek için Configuration Manager ayarlama

Intune ilkelerini Configuration Manager cihazlara dağıtmadan önce, aşağıdaki bölümlerde ayrıntılı olarak açıklanan konfigürasyonları doldurun. Bu yapılandırma, Microsoft Defender ATP ile Configuration Manager cihazlarınızı birlikte bulundurur ve Intune ilkeleriyle çalışmasını sağlar.

Aşağıdaki görevler Configuration Manager konsolunda tamamlanır. Configuration Manager hakkında bilgi sahibi değilseniz, bu görevleri gerçekleştirmek için bir Configuration Manager Yöneticisi ile çalışın.

1. [Configuration Manager için güncelleştirmeyi yükler](#task-1-install-the-update-for-configuration-manager)
2. [Kiracı eklemeyi etkinleştirme](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Eşitlenmek üzere koleksiyonları seçin](#task-3-select-collections-to-synchronize)
4. [Koleksiyonları Intune ilkelerini destekleyecek şekilde etkinleştirme](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> Microsoft Defender ATP 'yi Configuration Manager kullanma hakkında daha fazla bilgi için Configuration Manager içeriğinde aşağıdaki makalelere bakın:
>
> - [Microsoft Endpoint Manager Yönetim Merkezi aracılığıyla Microsoft Defender ATP 'ye Configuration Manager istemcileri ekleme](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Uç Nokta Yöneticisi kiracı iliştirme: cihaz eşitleme ve cihaz eylemleri](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Görev 1: Configuration Manager için güncelleştirmeyi yükler

Geçerli Configuration Manager dalı sürümü 2002 kullanıyorsanız, Microsoft Endpoint Manager yönetim merkezinden dağıttığınız uç nokta güvenlik ilkelerine yönelik destek ekleyen aşağıdaki konsol içi güncelleştirmeyi yükleyebilirsiniz.

**Güncelleştirme ayrıntıları**:

- **Configuration Manager 2002 düzeltme (KB4563473)**

Bu güncelleştirmeyi yüklemek için Configuration Manager belgelerine [konsol içi güncelleştirmeleri yüklemeyin](../../configmgr/core/servers/manage/install-in-console-updates.md) bölümündeki yönergeleri izleyin.

Güncelleştirmeyi yükledikten sonra, ortamınızı Microsoft Endpoint Manager yönetim merkezinden Endpoint Security ilkelerini destekleyecek şekilde yapılandırmaya devam etmek için buraya dönün.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Görev 2: kiracı eklemeyi ve koleksiyonları eşitlemeyi yapılandırma

Kiracı iliştirme ile, Microsoft Endpoint Manager Yönetim Merkezi ile eşitlenmek üzere Configuration Manager dağıtımınıza ait cihaz koleksiyonlarını belirtirsiniz. Koleksiyonlar eşitlendikten sonra, bu cihazlarla ilgili bilgileri görüntülemek ve Intune 'dan uç nokta güvenlik ilkesi dağıtmak için yönetim merkezini kullanın.

Kiracı iliştirme senaryosu hakkında daha fazla bilgi için bkz. Configuration Manager içerikte [kiracı eklemeyi etkinleştirme](../../configmgr/tenant-attach/device-sync-actions.md) .

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Ortak yönetim etkin olmadığında kiracı eklemeyi etkinleştir

> [!TIP]
> Kiracı eklemeyi etkinleştirmek için Configuration Manager konsolundaki **ortak yönetim Yapılandırma Sihirbazı** 'nı kullanın, ancak ortak yönetimi etkinleştirmeniz gerekmez.
>
> Ortak yönetimi etkinleştirmeyi planlıyorsanız, ortak yönetimi, önkoşulları ve devam etmeden önce iş yüklerini yönetme hakkında bilgi sahibi olun. Configuration Manager belgelerinde [ortak yönetim nedir?](../../configmgr/comanage/overview.md) konusuna bakın.

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.
2. Şeritte, Sihirbazı açmak için **ortak yönetimi yapılandırma** ' ya tıklayın.
3. **Kiracı ekleme** sayfasında, ortamınız için **AzurePublicCloud** ' yi seçin. Azure Kamu Bulutu desteklenmez.
   1. **Oturum aç**' a tıklayın. Oturum açmak için *genel yönetici* hesabınızı kullanın.

   2. **Kiracı ekleme** sayfasında **Microsoft Endpoint Manager yönetim merkezine yükle** seçeneğinin seçili olduğundan emin olun.

   3. **Ortak yönetim için otomatik istemci kaydını etkinleştir**onay kutusundan Kaldır.

      Bu seçenek belirlendiğinde, sihirbaz ortak yönetim kurulumunu tamamlamaya yönelik ek sayfalar sunar. Daha fazla bilgi için bkz. Configuration Manager içerikte [ortak yönetimi etkinleştirme](../../configmgr/comanage/how-to-enable.md) .

     ![Kiracı eklemeyi Yapılandır](./media/tenant-attach-intune/tenant-onboarding.png)

4. **AAD uygulaması oluştur** bildirimini kabul etmek için **İleri** ' ye ve ardından **Evet** ' e tıklayın. Bu eylem, bir hizmet sorumlusu sağlar ve koleksiyonların Microsoft Endpoint Manager yönetim merkezine eşitlenmesini kolaylaştırmak için bir Azure AD uygulama kaydı oluşturur.

5. **Karşıya yüklemeyi Yapılandır** sayfasında, hangi koleksiyonları eşitlemek istediğinizi yapılandırın. Yapılandırmanızı bir veya birkaç cihaz koleksiyonlarıyla sınırlayabilir veya **Microsoft uç nokta tarafından yönetilen tüm Cihazlarım**için önerilen cihaz yükleme ayarını kullanabilirsiniz Configuration Manager.

   > [!TIP]
   > Artık koleksiyonları seçme işlemini atlayabilirsiniz ve daha sonra Microsoft Endpoint Manager Yönetim Merkezi ile hangi koleksiyonların eşitleneceğini yapılandırmak için aşağıdaki görev 3 ' teki bilgileri kullanabilirsiniz.

6. Seçiminizi gözden geçirmek için **Özet** ' e tıklayın ve ardından **İleri**' ye tıklayın.

7. Sihirbaz tamamlandığında **Kapat**' a tıklayın.

   Kiracı iliştirme artık yapılandırılmıştır ve seçilen koleksiyonlar Microsoft Endpoint Manager yönetim merkezine eşitlenir.

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>Zaten ortak yönetimi kullanırken kiracı eklemeyi etkinleştirin

1. Configuration Manager yönetim konsolunda, **Yönetim**  >  **genel bakış**  >  **Cloud Services**  >  **ortak yönetim**' e gidin.

2. Ortak yönetim ayarlarınıza sağ tıklayıp **Özellikler**' i seçin.

3. **Karşıya yüklemeyi Yapılandır** sekmesinde, **Microsoft Endpoint Manager yönetim merkezine yükle**' yi seçin. **Uygula**’ya tıklayın.

   Cihaz yükleme için varsayılan ayar, **Microsoft uç nokta Configuration Manager tarafından yönetilen tüm cihazlardır**. Yapılandırmanızı bir veya birkaç cihaz koleksiyonu ile sınırlandırmayı da tercih edebilirsiniz.

   ![Ortak yönetim özellikleri sekmesini görüntüleme](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > Artık koleksiyonları seçme işlemini atlayabilirsiniz ve daha sonra Microsoft Endpoint Manager Yönetim Merkezi ile hangi koleksiyonların eşitleneceğini yapılandırmak için aşağıdaki görev 3 ' teki bilgileri kullanabilirsiniz.

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

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>Görev 4: uç nokta güvenlik ilkeleri için koleksiyonları etkinleştirme

Koleksiyonları Microsoft Endpoint Manager yönetim merkezine eşitlenecek şekilde yapılandırdıktan sonra, bu koleksiyonları uç nokta güvenlik ilkeleriyle çalışacak şekilde etkinleştirin. Cihaz koleksiyonlarının Endpoint Security ilkeleriyle Intune 'a çalışmasını etkinleştirdiğinizde, bu koleksiyonlardaki cihazları Microsoft Defender ATP ile birlikte çalışmak üzere yapılandırıyorsunuz demektir.

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>Koleksiyonları Endpoint Security ilkeleriyle kullanmak üzere etkinleştirme

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>Sonraki adımlar

- *Virüsten koruma* ve *uç nokta algılama ve yanıt*için [uç nokta güvenlik ilkelerini yapılandırın](endpoint-security-policy.md#create-an-endpoint-security-policy) .

- Microsoft Defender ATP belgelerindeki [uç nokta algılama ve yanıt](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) hakkında daha fazla bilgi edinin.