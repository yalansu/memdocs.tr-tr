---
title: Cihaz koleksiyonlarına uygulama dağıtımı teknik başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager için uygulama dağıtımlarının cihaz koleksiyonlarına yönelik teknik başvuru sorunlarını giderme.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709764"
---
# <a name="application-deployment-for-device-collections"></a>Cihaz Koleksiyonları için uygulama dağıtımı

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir uygulama bir cihaz koleksiyonuna dağıtıldığında, dağıtım amacı ne olursa olsun, ilke koleksiyondaki tüm cihazlara hedeflenmiş olur. Bu makalede, istemcide ilke indirme ve dağıtım işlemleri açıklanmaktadır.

> [!TIP]
> İstemci günlüklerini gözden geçirmek için gereken tüm bilgiler, [başlamadan önce](app-deployment-technical-reference.md#before-you-begin) bölümünde başvurulan SQL sorgusu çalıştırılarak elde edilebilir.

## <a name="policy-download"></a>İlke Indirme

Uygulama dağıtımı ilkesi istemciye hedeflendikten sonra, istemci ilkeyi bir sonraki ilke yoklama döngüsüne indirir. İstemci ilkeyi indirdiğinde, dağıtım ilkesine ek olarak ilgili ilkeleri indirir. Bu ilgili ilkeler uygulama, dağıtım türü, genel koşullar vb. için ilkeyi içerir. İlke indirme etkinliği, uygulama veya atama benzersiz KIMLIĞI kullanılarak istemcideki **policyagent. log** dosyasında izlenebilir.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

İlkeler istemciye indirildikten sonra Zamanlayıcı bileşeni, dağıtım etkinleştirme ve zorlaması için zamanlamalar oluşturur.

## <a name="deployment-activation"></a>Dağıtım etkinleştirme

Dağıtım etkinleştirildiğinde uygulama değerlendirmesi başlatılır. Scheduler bileşeni, atamayı dağıtımda yapılandırılmış kullanılabilir zamanda etkinleştirmek için bir zamanlama oluşturur. Bu etkinlik, uygulama atama benzersiz KIMLIĞI kullanılarak istemcideki **Zamanlayıcı. log** dosyasında izlenebilir.

- **Gerekli** dağıtımlarda, etkinleştirme zamanlaması oluşturulur, ancak site sunucularında ve dağıtım noktalarında kaynak çekişmesini önlemek için iki saate kadar bir gecikme süresi vardır. Gecikme, uygulama tanımlı gereksinim kurallarına göre geçerliyse, değerlendirme sırasında uygulama içeriği indirilene engel olmaya yardımcı olur.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- **Kullanılabilir** dağıtımlar için, etkinleştirme zamanlaması dağıtımda yapılandırılan kullanılabilir zamanda tetiklenmeye oluşturulur.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Zamanlama süresi geldiğinde zamanlayıcı bileşeni, uygulama değerlendirmesi gerçekleştirmek için etkinleştirme iletisini DCM aracısına gönderir.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

DCM Aracısı etkinleştirme iletisini alır ve uygulamayı değerlendirmek için bir iş oluşturur.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Dağıtım zorlaması

Dağıtım zorlandığında uygulama yüklemesi başlatılır.

- **Gerekli** dağıtımlar için Zamanlayıcı, uygulamayı dağıtım son tarihinde zorlamak üzere ilke indirildikten sonra bir son tarih zamanlama oluşturur. Son Tarih zamanlaması varsayılan olarak rastgele değildir. Etkinleştirme için rastgele davranış ayarı, [son tarih rastgele](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization) seçme istemci ayarıyla denetlenebilir.

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    Son tarihte, Scheduler bileşeni son tarih iletisini DCM aracısına gönderir. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    DCM Aracısı son tarih iletisini alır ve uygulamayı zorlamak için bir iş oluşturur.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > Son tarihi geçmiş dağıtımlar için uygulama, değerlendirme, indirme ve yükleme eylemlerini gerçekleştiren aynı DCM Aracısı işi tarafından hemen etkinleştirilir ve uygulanır.

- **Kullanılabilir** dağıtımlar için, uygulama yüklemesi yazılım merkezinden Kullanıcı tarafından başlatıldığında zorlama gerçekleşmeden bu yana son tarih zamanlaması yoktur. Kullanıcı bir yükleme başlattığında uygulama değerlendirme, indirme ve yükleme işlemleri gerçekleştirmek için bir DCM Aracısı işi oluşturulur. Bu etkinlik, istemcideki **Dcmagent. log** dosyasında izlenebilir.

## <a name="next-steps"></a>Sonraki Adımlar

- [Uygulama dağıtımı istemci bileşenlerini anlama](client-components-technical-reference.md)
