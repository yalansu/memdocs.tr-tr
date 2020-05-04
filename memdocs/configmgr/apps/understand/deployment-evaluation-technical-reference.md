---
title: Uygulama değerlendirmesi teknik başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager için uygulama değerlendirmesi teknik başvurusu sorunlarını giderme.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709799"
---
# <a name="application-deployment-evaluation"></a>Uygulama dağıtımı değerlendirmesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Devam etmeden önce lütfen DCM ve CI Aracısı iş işlemesini anlamak için [uygulama dağıtım istemci bileşenlerini](client-components-technical-reference.md) gözden geçirin.

Uygulama değerlendirmesi, dağıtım etkinleştirildiğinde DCM Aracısı ve CI Aracısı bileşenleri tarafından gerçekleştirilir. Atamanın etkin olduğunu anlamak için, [cihaz koleksiyonlarına uygulama dağıtımına](device-deployment-technical-reference.md) veya [Kullanıcı koleksiyonları makalelerine uygulama dağıtımına](user-deployment-technical-reference.md) bakın.

## <a name="application-detection-and-evaluation"></a>Uygulama algılama ve değerlendirme

Uygulama değerlendirmesi bir CI Aracısı işinin **InvokingSdmMethod** aşamasında gerçekleştirilir. Bu aşama, istemcinin cihaza uygulamanın yüklenip yüklenmediğini saptamak için tanımlanan algılama yöntemini değerlendirdiği yerdir. Bu etkinlik, dağıtım türü benzersiz KIMLIĞI veya dağıtım türü adı kullanılarak **AppDiscovery. log** dosyasında izlenebilir.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> Yukarıdaki örnek, MSI ürün kodunun cihaza yüklenip yüklenmediğini denetleyerek, algılamanın yapıldığı bir MSI uygulaması için algılamayı gösterir. Alternatif algılama yöntemlerini kullanan uygulamalar için, uygulamanın yüklenip yüklenmediğini denetlemek için uygun algılama yöntemi kullanılır.

Ardından istemci, dağıtım amacını temel alarak uygulamanın istenen durumunu değerlendirir. Bu adım Ayrıca uygulamanın uygulama için kullanılması gereken bağımlılıklara veya yerine geçme kurallarına sahip olup olmadığını algılamaya de yöneliktir. Bu etkinlik uygulama ve dağıtım türü benzersiz KIMLIĞI kullanılarak **Appsınteval. log** dosyasında izlenebilir.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

Yukarıdaki günlük girişinde **geçerli durum** uygulamanın cihazda yüklü olup olmadığını gösterir. **Uygulanabilirlik** , uygulamanın tanımlı gereksinim kurallarına göre geçerli olup olmadığını gösterir. **ResolvedState** , dağıtım amacını temel alarak uygulamanın istenen durumunu gösterir.

> [!TIP]
> Uygulama durumunu, uygulanabilirlik durumunu ve gereksinim ihlallerini görüntülemek için [dağıtım Izleme aracını](../../core/support/deployment-monitoring-tool.md) kullanın.

## <a name="next-steps"></a>Sonraki Adımlar

- [Uygulama Indirme](deployment-download-technical-reference.md)
