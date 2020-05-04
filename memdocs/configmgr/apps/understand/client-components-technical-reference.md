---
title: Uygulama dağıtımı istemci bileşenleri teknik başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager 'de uygulama dağıtımı sorunlarını gidermek için kullanılan istemci bileşenleri.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709806"
---
# <a name="understanding-application-deployment-client-components"></a>Uygulama dağıtımı Istemci bileşenlerini anlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Uygulama dağıtımı değerlendirmesi ve zorlama işlemleri, istemci üzerindeki DCM Aracısı ve CI Aracısı bileşenleri tarafından işlenir. Bu makalede tipik bir DCM ve CI Aracısı işinin nasıl çalıştığı açıklanmaktadır.

## <a name="dcm-agent"></a>DCM Aracısı

DCM Aracısı, uygulamaları içeren yapılandırma öğelerinin değerlendirilmesinden sorumlu olan üst düzey istemci bileşenidir. Bir dağıtım etkinleştirildiğinde veya zorlandığında, atama ilkesini okuyan ve gerçekleştirilmesi gereken eylemleri belirleyen bir DCM Aracısı işi oluşturulur. Bu etkinlik, uygulamanın benzersiz KIMLIĞI aranarak belirlenebilen DCM Aracısı Iş KIMLIĞI kullanılarak istemcideki **Dcmagent. log** dosyasında izlenebilir.

### <a name="device-deployments"></a>Cihaz dağıtımları

- **Gerekli** dağıtımlar Için DCMAgent. log ilgili eylemleri gösterir. Bu eylemler, dağıtım son tarihinin zaten geçmiş olmasına bağlı olarak farklılık gösterebilir.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- **Kullanılabilir** dağıtımlar Için DCMAgent. log dağıtımın `is not mandatory`olduğunu gösterir. Bu dağıtımlar için uygulama değerlendirmesi yapılır ancak Kullanıcı yüklemeyi başlatmadığı müddetçe zorlama atlanır.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Kullanıcı dağıtımları

- **Gerekli** dağıtımlar Için DCMAgent. log ilgili eylemleri gösterir. Bu eylemler, dağıtım son tarihinin zaten geçmiş olmasına bağlı olarak farklılık gösterebilir.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- **Kullanılabilir** dağıtımlar için, uygulama yüklemesi Kullanıcı tarafından başlatıldığında Kullanıcı tarafından değerlendirme ve zorlama Için DCM Aracısı işleri oluşturulur.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>CI Aracısı

CI Aracısı, yapılandırma öğelerinin değerlendirilmesi ve düzeltilmesinden sorumlu istemci bileşenidir. DCM Aracısı atama ilkesini okur ve istenen eylemleri gerçekleştirmek için CI Aracısı bileşeni için bir iş oluşturur. **Dcmagent. log** , Istemci üzerindeki **cıagent. log** dosyasında CI Aracısı etkinliğini Izlemek Için yararlı olan CI Aracısı iş kimliğini kaydeder.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Tipik bir CI Aracısı işi birden çok aşamadan geçer. Bu, CI Aracısı Iş KIMLIĞINDE **cıagent. log dosyasına** filtre uygulayarak tanımlanabilir ve için `TransitionState`öğesini aramıştır. Bir uygulama dağıtımı CI Aracısı işi için bazı temel aşamalar şunlardır:

- **Downloadingcıs**
  - Bu aşamada, uygulamayı değerlendirmek için gereken uygulama meta verileri indirilir. Meta veriler, algılama yöntemi, gereksinim kuralları, genel koşullar vb. içerir. Bu etkinlik, **CIDownloader. log** ve **DataTransferService. log**' da izlenebilir. **Kullanılabilir** dağıtımlar için bu işlem, uygulamanın ilk değerlendirmesi sırasında oluşur. Ancak **gerekli** dağıtımlar için bu işlem, ilke indirildikten hemen sonra gerçekleşir.

- **InvokingSdmMethod**
  - Bu aşamada uygulama algılama yöntemi, uygulamanın yüklenip yüklenmediğini denetlemek için kullanılır ve istenen durum belirlenir. Bu etkinlik **AppDiscovery. log** ve **Appsınteval. log**içinde izlenebilir. Bu aşama hakkında daha fazla bilgi için bkz. [uygulama değerlendirmesi](deployment-evaluation-technical-reference.md).

- **StateDownloadingContents**
  - Bu aşamada, uygulama içeriği gerekirse indirilir. Bu etkinlik **CAS. log**, **ContentTransferManager. log**, **LocationServices. log**ve **DataTransferService. log**içinde izlenebilir. Bu aşama hakkında daha fazla bilgi için bkz. [uygulama indirme](deployment-download-technical-reference.md).

- **Stateenforcingcıs**
  - Bu aşamada uygulama yüklemesi başlatılır. Bu etkinlik, **AppEnforce. log**' da izlenebilir. Bu aşama hakkında daha fazla bilgi için bkz. [uygulama yükleme](deployment-install-technical-reference.md).

- **StateEnforcementReporting**
  - Bu aşamada, uygulama yükleme durumu yönetim noktasına raporlama için kaydedilir. Bu etkinlik, **Statemessage. log**dosyasında izlenebilir.

CI Aracısı işi tüm aşamalardan geçer, ancak gerekmiyorsa, aşamayı atlar. Örnek olarak, **mevcut** dağıtımlar için, Kullanıcı uygulamayı Yazılım Merkezi 'nden yüklemeye girişiminden sonra, Downloadingcontents ve Stateenforcingcıs aşamaları atlanır. Ancak, **gerekli** dağıtımlarda, StateDownloadingContents aşaması, atama etkinleştirildiğinde uygulama içeriğini (gerekliyse) indirir, ancak son tarih gelecekte olduğunda Stateenforcingcıs aşaması atlanır. Bu davranış, CI Aracısı Iş KIMLIĞINDE filtreleyerek ve için `Skipping policy`arama yaparak cıaracısı. log dosyasında gözlemlenebilir.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Sonraki Adımlar

- [Uygulama değerlendirmesi](deployment-evaluation-technical-reference.md)
- [Uygulama Indirme](deployment-download-technical-reference.md)
- [Uygulama yükleme](deployment-install-technical-reference.md)
