---
title: Uygulama yükleme teknik başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager için uygulama yüklemeleri teknik başvurusu sorunlarını giderme.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709785"
---
# <a name="application-installation"></a>Uygulama yükleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Devam etmeden önce lütfen DCM ve CI Aracısı iş işlemesini anlamak için [uygulama dağıtım istemci bileşenlerini](client-components-technical-reference.md) gözden geçirin.

Dağıtım zorlandığında, uygulama yüklemesi DCM Aracısı ve CI Aracısı bileşenleri tarafından gerçekleştirilir. Zorlama süresi kullanılabilir ve gerekli dağıtımlar için farklılık gösterir. Atamanın ne zaman uygulanacağını anlamak için, [cihaz koleksiyonlarına uygulama dağıtımına](device-deployment-technical-reference.md) veya [Kullanıcı koleksiyonları makalelerine uygulama dağıtımına](user-deployment-technical-reference.md) bakın.

## <a name="enforcement-initiation"></a>Zorlama başlatma

Uygulama yüklemesi, **Stateenforcingcıs** aşamasında ISTEMCI üzerindeki CI Aracısı bileşeni tarafından başlatılır. Bu işlem, uygulamanın bir cihaz koleksiyonuna veya bir kullanıcı koleksiyonuna dağıtılmasından bağımsız olarak aynıdır.

- **Kullanılabilir** dağıtımlar için, Kullanıcı yazılım merkezinden uygulama yüklemesini başlattığında uygulama yüklenir.
- **Gerekli** dağıtımlar için uygulama dağıtım son tarihinde yüklenir. Ancak, Kullanıcı son tarihten önce yazılım merkezinden yüklemeyi başlatabilir.

CI Aracısı uygulama yüklemesini başlattığında, CI Görev Yöneticisi bileşeni tarafından işlenen bir görevi oluşturur. CI görev yöneticisi daha sonra yüklemeyi başlatır. Bu etkinlik, dağıtım türü benzersiz KIMLIĞI kullanılarak **Cıtaskmgr. log** dosyasında izlenebilir.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Uygulama zorlaması

Uygulama zorlaması başlatıldıktan sonra, istemci uygulamanın önceden yüklü olmadığından emin olmak için uygulama algılamayı yeniden gerçekleştirir. Uygulamanın yüklenmediğini belirledikten sonra uygulama yüklemesi başlatılır. Bu etkinlik, dağıtım türü benzersiz KIMLIĞI kullanılarak istemcideki **AppEnforce. log** dosyasında izlenebilir.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Yükleme doğrulaması

Uygulama yüklendikten sonra, uygulamanın yüklü olarak algılandığına emin olmak için uygulama algılama yöntemi tekrar kullanılır.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Son olarak, zorlama tamamlandıktan sonra, CI Aracısı görev tamamlanma bildirimini alır ve CI Aracısı işi sonraki aşamaya gider.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Sonraki Adımlar

[Uygulama dağıtımlarının sorunlarını giderme](../deploy-use/troubleshoot-application-deployment.md)
