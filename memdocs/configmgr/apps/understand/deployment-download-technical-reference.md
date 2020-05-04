---
title: Uygulama indirme teknik başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager için uygulama indirme teknik başvurusu sorunlarını giderme.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709813"
---
# <a name="application-download-in-configuration-manager"></a>Configuration Manager 'de uygulama Indirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Devam etmeden önce lütfen DCM ve CI Aracısı iş işlemesini anlamak için [uygulama dağıtım istemci bileşenlerini](client-components-technical-reference.md) gözden geçirin.

## <a name="download-initiation"></a>Yüklemeyi başlatma

Uygulama içeriği indirme, **Statedownloadingcontents** aşamasında ISTEMCI üzerindeki CI Aracısı bileşeni tarafından başlatılır. Bu işlem, uygulamanın bir cihaz koleksiyonuna veya bir kullanıcı koleksiyonuna dağıtılmasından bağımsız olarak aynıdır.

- **Kullanılabilir** dağıtımlar için, Kullanıcı yazılım merkezinden uygulama yüklemesini başlattığında uygulama içeriği indirilir.
- **Gerekli** dağıtımlarda, atama etkinleştirildiğinde uygulama içeriği indirilir ve uygulama değerlendirmeden sonra uygulanabilir. Atamanın etkin olduğunu anlamak için, [cihaz koleksiyonlarına uygulama dağıtımına](device-deployment-technical-reference.md) veya [Kullanıcı koleksiyonları makalelerine uygulama dağıtımına](user-deployment-technical-reference.md) bakın.

CI Aracısı içerik indirmeyi başlattığında, CI Görev Yöneticisi bileşeni tarafından işlenen bir görevi oluşturur. CI görev yöneticisi daha sonra içerik indirmeyi başlatır. Bu etkinlik, dağıtım türü benzersiz KIMLIĞI kullanılarak **Cıtaskmgr. log** dosyasında izlenebilir.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Dağıtım noktası konumu

Tüm indirme görevleri, istemci önbelleğinin yönetiminden sorumlu olan Içerik erişim bileşeni tarafından işlenir. İndirme görevi oluşturulduktan sonra Içerik erişim bileşeni, içeriğin istemci önbelleğinde zaten kullanılabilir olup olmadığını denetler. İçerik kullanılamıyorsa, içeriğin alınbildiği dağıtım noktalarının listesini almak için bir konum isteği oluşturur. Bu etkinlik, Içerik benzersiz KIMLIĞI kullanılarak, istemci üzerindeki **CAS. log** ve **LocationServices. log** dosyasında izlenebilir.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Konum Hizmetleri bileşeni konum isteklerini işlese de, doğrudan yönetim noktasından konum isteğinde yoktur. Yönetim noktasına yapılan tüm istekler genellikle **CcmMessaging. log**DOSYASıNA kaydeden CCM mesajlaşma bileşeni aracılığıyla gider.

Yanıt yanıtı XML, istemcinin sınır grubunu temel alan dağıtım noktalarının listesini içerir. Bu liste, [Içerik kaynağı önceliğine](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority)göre istemcide WMI 'da ayrıştırılır ve kalıcı hale getirilir. Bu etkinlik, Içerik benzersiz KIMLIĞI kullanılarak ve için `Persisted location`arama yaparak **ContentTransferManager. log**' da görülebilir. 

Yanıt XML konumu herhangi bir dağıtım noktası içermiyorsa, **ContentTransferManager. log** görüntülenir `Received empty location update` ve istemci, uygulamayı indirirken %0 ' da takılı kalabilir. Bu yanıt, genellikle sınır grubu yapılandırma sorunları nedeniyle ortaya çıkabilir. Daha fazla bilgi için bkz. [indirme sorunları](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## <a name="content-download"></a>İçerik Indirme

Dağıtım noktası konumları alındıktan sonra, Içerik erişim bileşeni bir Içerik aktarma işi oluşturur. Bu etkinlik, Içerik benzersiz KIMLIĞI kullanılarak **CAS. log** dosyasında izlenebilir.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

İçerik aktarma Yöneticisi daha sonra içerik indirmeyi yapmak için bir Veri Aktarımı hizmeti işi oluşturur. Bu etkinlik, Içerik benzersiz KIMLIĞI kullanılarak istemcide **ContentTransferManager. log** dosyasında izlenebilir.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Bu günlük girdisi, sırasıyla **ContentTransferManager. log** ve **DataTransferService. log** ' da içerik aktarımının ILERLEMESINI izlemek için KULLANıLABILECEK CTI ve DTS iş kimliği ' ni belirlemek için kullanılabilir.

Veri Aktarımı hizmet, bir Arka Plan Akıllı Aktarım Hizmeti (BITS) işi oluşturarak ve indirmenin tamamlanmasını beklerken uygulama içeriğini indirmeyi gerçekleştirir. Bu etkinlik, **Contenttransferservice. log**' dan edinilen DTS iş kimliği kullanılarak Istemcideki **DataTransferService. log** dosyasında izlenebilir.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

İndirme işlemi tamamlandıktan sonra, Içerik erişim bileşenine bildirilir. İçerik erişim bileşeni daha sonra indirilen içeriği doğrular ve bu da içeriğin indirme sırasında değiştirilmediğinden emin olun. Bu etkinlik, Içerik benzersiz KIMLIĞI kullanılarak **CAS. log** dosyasında izlenebilir.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Son olarak, içerik doğrulandıktan sonra, CI Aracısı görev tamamlanma bildirimini alır ve CI Aracısı işi sonraki aşamaya gider.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Sonraki Adımlar

- [Uygulama yükleme](deployment-install-technical-reference.md)
