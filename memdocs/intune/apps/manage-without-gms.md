---
title: Intune 'u Google Mobile Services olmayan ortamlarda kullanma
titleSuffix: Microsoft Intune
description: Intune 'u Google Mobile Services olmayan ortamlarda nasıl kullanacağınızı öğrenin.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7955afb2aef88e3787546843cc477bce22369a4d
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.contentlocale: tr-TR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022390"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Intune 'u Google Mobile Services olmayan ortamlarda kullanma

Microsoft Intune, Android cihazlarını yönetirken Microsoft Intune şirket portalı ile iletişim kurmak için Google Mobile Services (GMS) kullanır. Bazı durumlarda, cihazların geçici veya kalıcı olarak GMS erişimi olmayabilir. Örneğin, bir cihaz GMS olmadan sevk edebilir veya cihaz, GMS 'nin kullanılamadığı kapalı bir ağa bağlanıyor olabilir. Bu belgede, Android cihazlarını GMS olmadan yönetmek için Intune 'u yüklerken ve kullanırken karşılaşabileceğiniz farklar ve sınırlamalar özetlenmektedir.

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>Intune Şirket Portalı uygulamasını Google Play Store erişimi olmadan yüklemesi 

### <a name="for-users-outside-of-peoples-republic-of-china"></a>Çin Halk Cumhuriyeti dışındaki kullanıcılar için

Google Play kullanılamıyorsa, Android cihazlar [Android için Microsoft Intune şirket portalı](https://www.microsoft.com/en-us/download/details.aspx?id=49140) indirebilir ve uygulamayı dışarıdan yükleyebilir. Uygulama bu şekilde yüklendiğinde güncelleştirmeleri veya düzeltmeleri otomatik olarak almaz. Uygulamayı düzenli olarak güncelleştirdiğinizden ve düzeltme ekinin el ile düzeltmeniz gerekir. 

### <a name="for-users-in-peoples-republic-of-china"></a>Çin Halk Cumhuriyeti kullanıcıları için

Google Play Store şu anda Çin Halk Cumhuriyeti 'nde kullanılamadığından, Android cihazlarının uygulamaları Çince uygulama marketlerinden alması gerekir. Daha fazla bilgi için, bkz. [Çin halk cumhuriyeti Şirket Portalı uygulamasını](../user-help/install-company-portal-android-china.md)öğrenin.

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>GMS kullanılamadığında Intune Cihaz Yöneticisi yönetiminin sınırlamaları 

### <a name="unavailable-intune-features"></a>Kullanılamayan Intune özellikleri

Bazı Intune özellikleri, Google Play deposu veya Google Play hizmetleri gibi GMS bileşenlerini kullanır. Bu bileşenler GMS olmadan ortamlarda kullanılamadığından, Intune yönetici konsolundaki aşağıdaki özellikler kullanılamayabilir.  

| Senaryo  | Özellikler  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cihaz uyumluluğu ilkeleri  | Android Cihaz Yöneticisi için uyumluluk ilkeleri oluştururken veya düzenlenirken, **Google Play koruma** altında listelenen tüm seçenekler kullanılamaz.  |
| Uygulama koruma ilkeleri (koşullu başlatma)  | **Uygulamalar üzerinde tehdit taraması gerektir ve uygulamalarda tehdit taraması iste** **cihaz koşulları** koşullu başlatma için kullanılamaz.  |
| İstemci uygulamaları  | **Android** türündeki uygulamalar kullanılamıyor. Uygulamaları dağıtmak ve yönetmek için **Iş kolu uygulamasını** kullanın.  |
| Mobile Threat Defense  | Çözümünüzün Intune ile tümleştirildiğini, ilgilendiğiniz bölgede kullanılabilir olup olmadığını ve GMS 'ye dayanmasını anlamak için MTD satıcınız ile birlikte çalışın.  |

### <a name="some-tasks-may-be-delayed"></a>Bazı görevler gecikebilir 

GMS 'nin kullanılabildiği ortamlarda, Intune görevlerin bitmesini hızlandırmak için anında iletme bildirimlerini kullanır. Örneğin, cihazı uzaktan temizlemeyi denerseniz bildirimler genellikle cihaza Saniyeler içinde alınır. GMS 'nin kullanılamadığı koşullarda, anında iletme bildirimleri de kullanılamayabilir. Bu nedenle, Intune 'un görevleri tamamlaması için bir sonraki cihaz iade etme süresi beklemesi gerekir.  

Kaydedilen Android cihazları, her 8 saatte bir Intune 'a rapor sağlar. Örneğin, bir cihaz 1 PM 'de Intune 'a bildirirse ve uzak görevler 1:05 PM 'de verildiğinde, Intune, görevleri tamamladıktan sonra cihaz 9 ' da cihazla iletişim kuracaktır. 

Aşağıdaki görevlerin tamamlanabilmesi için en fazla 8 saat gerekebilir: 

**Intune Konsolu**:
- Tam temizleme
- Seçmeli temizleme
- Yeni veya güncelleştirilmiş uygulamaların dağıtımı
- Uzaktan kilitleme
- Geçiş kodu sıfırlama

**Android için Intune şirket portalı uygulaması**:
- Uzak cihaz kaldırma
- Cihaz sıfırlama
- Kullanılabilir iş kolu uygulamalarının yüklenmesi

**Intune şirket portalı Web sitesi**:
- Cihaz kaldırma (yerel ve uzak)
- Cihaz sıfırlama
- Cihaz geçiş kodu sıfırlama

Cihaz son zamanlarda kaydedildiyse, uyumluluk, uyumsuzluk ve yapılandırma iadede daha sık çalışır. Cihaz iadeleri hakkında daha fazla bilgi için, bkz. [Microsoft Intune cihaz ilkeleri ve profillerle Ilgili yaygın sorular, sorunlar ve çözümler](../configuration/device-profile-troubleshoot.md). 

## <a name="next-steps"></a>Sonraki adımlar

- [Microsoft Intune ile uygulamaları gruplara atama](../apps/apps-deploy.md)
