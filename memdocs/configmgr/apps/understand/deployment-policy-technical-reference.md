---
title: Uygulama dağıtım ilkesi teknik başvurusu
titleSuffix: Configuration Manager
description: Configuration Manager için uygulama dağıtım ilkelerine ilişkin teknik başvuru sorunlarını giderme.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709792"
---
# <a name="application-deployment-policy"></a>Uygulama dağıtım Ilkesi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

## <a name="policy-creation"></a>İlke oluşturma

Bir uygulamayı dağıtırken, bir uygulamanın bir koleksiyona atanmasını temsil eden [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) sınıfının bir örneği oluşturulur. Bu etkinlik **Smsprov. log**dosyasında izlenebilir.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

Configuration Manager veritabanında, bu bilgiler `CI_CIAssignments` `AssignmentType` 2. bir uygulama dağıtımını temsil eden tabloda depolanır. Atama oluşturulduğunda, SMS veritabanı Izleyicisi bileşeni tabloda bir değişiklik algıladığında, nesne çoğaltma Yöneticisi 'nin CI ataması (CIA) ilkesini işlemesini bildirir. Nesne çoğaltma Yöneticisi bileşeni daha sonra veritabanında bulunan `Policy` tabloda depolanan uygulama ataması için ilkeyi oluşturur ve ilke kimliği, UYGULAMANıN benzersiz kimliğini temel alır. Bu etkinlik, atama benzersiz KIMLIĞINE başvurarak **Objreplmgr. log** dosyasında izlenebilir ve bu, [başlamadan önce](app-deployment-technical-reference.md#before-you-begin) bölümünde başvurulan SQL sorgusundan elde edilebilir.

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

Uygulama atamasının ilkesi, aşağıda gösterilene benzer bir SQL sorgusu kullanılarak veritabanında görülebilir.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>İlke hedefleme

İlke oluşturulduktan sonra, Ilke sağlayıcısı bileşeni bu ilkeyi uygulama dağıtımı tarafından hedeflenen koleksiyondaki kaynaklara atar. İlke hedefleme bilgileri veritabanındaki `ResPolicyMap` tabloda depolanır. Bu etkinliği **policypv. log**dosyasında izlemek için yukarıdaki sorgu tarafından döndürülen ıBIR deklarasyon kullanabilirsiniz. Ancak, günlüğe kaydedilen bir Ise Deklarasyonu, aynı anda birden çok ilke işlenirse yukarıdaki sorgu tarafından döndürülen Ise DEKLARASYONUNU her zaman eşleşmeyebilir.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap`tablo, Kullanıcı koleksiyonlarına **kullanılabilir** olarak dağıtılan uygulamalar için herhangi bir hedefleme bilgisi içermiyor. Software Center bu uygulamaların listesini yönetim noktasından sorgular ve bu uygulamalar için ilke hedefleme bilgileri, bir kullanıcı yazılım merkezinden bir uygulama istediğinde dinamik olarak oluşturulur.

## <a name="next-steps"></a>Sonraki Adımlar

- [Cihaz koleksiyonlarına uygulama dağıtımı](device-deployment-technical-reference.md)
- [Kullanıcı koleksiyonlarına uygulama dağıtımı](user-deployment-technical-reference.md)
