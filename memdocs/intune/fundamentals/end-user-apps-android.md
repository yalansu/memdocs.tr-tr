---
title: Android kullanıcılarınız uygulamalarını nasıl alır
description: Android uygulamalarını son kullanıcılara sağlama yöntemleri
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f33d1684-b1b5-44f7-9aac-c6d5186a5d7c
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c0c913d3bc1467096090ac4e80d1d9d5f578a1b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182319"
---
# <a name="how-your-android-users-get-their-apps"></a>Android kullanıcılarınız uygulamalarını nasıl alır  

Bu makale, Android cihaz yöneticinizin son kullanıcılarının Microsoft Intune aracılığıyla dağıttığınız uygulamaları nasıl ve nereden alabileceğini anlamanıza yardımcı olur. Bilgiler cihaz türüne göre değişebilir (yerel Android cihazlar veya Samsung Knox Standard cihazlar).

## <a name="native-non-samsung-knox-standard-android-devices"></a>Yerel (Samsung Knox Standard harici) Android cihazlar   

| Uygulama türü | İş kolu (LOB) uygulamaları | Play Store uygulamaları  |
| ------------- |-------------| -----|
| Kullanılabilir uygulamalar      | Kullanıcılar Şirket Portalı’nda **yükle**’ye dokunur. Bir bildirim görüntülenir ve kullanıcılar buna dokunarak yüklemeyi başlatır. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır. | Kullanıcılar Şirket Portalı uygulamaya dokunur ve Play Store bir uygulama sayfasına alınmıştır. Bu, yüklemeyi başlattıkları yerdir.|
| Gerekli uygulamalar      | Kullanıcılara, bir uygulama yüklemeleri gerektiğini belirten bir bildirim gösterilir. Kullanıcılar yüklemeyi başlatmak için bildirime dokunur. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır.    | Kullanıcılara, bir uygulama yüklemeleri gerektiğini belirten bir bildirim gösterilir. Kullanıcılar bildirime dokunur ve Play Store bir uygulama sayfasına alınır. Bu, yüklemeyi başlattıkları yerdir. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır. |

Son kullanıcılarınızın [LOB uygulamalarını](../apps/lob-apps-android.md)yüklemek için bilinmeyen kaynaklardan yükleme yapmasına izin vermeniz gerekir. Bu ayar, Android sürümüne bağlı olarak normalde iki farklı yerde bulunur:

* Android 7.1.2 ve Lower: **Ayarlar** > **güvenlik** > **Bilinmeyen kaynaklar**
* Android 8,0 ve üzeri: **Ayarlar** > **uygulamalar & bildirimler** > **özel uygulama erişimi** > **Bu kaynaktan izin verilen** **Şirket portalı** > **bilinmeyen uygulamaları yükler** > 

Bu durumda Şirket Portalı uygulaması, son kullanıcıya bilgi verip onu doğrudan uygun ayara yönlendirecektir. 

## <a name="samsung-knox-standard-android-devices"></a>Samsung Knox Standard Android cihazlar

| Uygulama türü | İş kolu (LOB) uygulamaları | Play Store uygulamaları  |
| ------------- |-------------| -----|
| Kullanılabilir uygulamalar      | Kullanıcılar Şirket Portalı’nda **yükle**’ye dokunur. Uygulama, başka kullanıcı müdahalesi olmadan yüklenir. | Kullanıcılar Şirket Portalı uygulamaya dokunur ve Play Store bir uygulama sayfasına alınır. Bu, yüklemeyi başlattıkları yerdir.|
| Gerekli uygulamalar      | Uygulama, hiçbir kullanıcı müdahalesi olmadan yüklenir.    | Kullanıcılara, bir uygulama yüklemeleri gerektiğini belirten bir bildirim gösterilir. Kullanıcılar bildirime dokunur ve Play Store bir uygulama sayfasına alınır. Bu, yüklemeyi başlattıkları yerdir. Yükleme başarılı olduktan sonra, bildirim görüntüden kaldırılır. |

Uygulamalar, aşağıda açıklandığı gibi yönetilebilir veya yönetilmeyebilir. Uygulamaları yönetilen uygulama yapma işlemi, tüm Android cihaz türlerinde aynıdır.

* Yönetilen uygulamalar: Bu uygulamalar ilkeler aracılığıyla yönetilir. Intune tarafından "sarmalanmış" veya Intune uygulama SDK 'Sı ile oluşturulmuştur. Bu uygulamalar Intune tarafından yönetilebilir ve uygulama ilkeleri uygulanabilir.

* Yönetilmeyen uygulamalar: Bu uygulamalar ilkeler aracılığıyla yönetilmez. Intune tarafından sarmalanmamış veya Intune uygulama SDK 'Sı dahil değildir. Uygulama ilkeleri bu uygulamalara uygulanamaz.

## <a name="zebra-devices-with-zebra-mobility-extensions"></a>Zeköşeli Mobility uzantılarına sahip zeköşeli cihazlar

Intune, Cihaz Yöneticisi tarafından yönetilen Zeköşeli cihazlara uygulamaları sessizce yüklemek için Zeköşeli Mobility uzantıları (MX) araç takımını kullanır. Bu özellik, Zeköşeli cihazlarda Kullanıcı müdahalesi olmadan uygulama dağıtmanıza ve güncelleştirmenize olanak tanır. Cihazınızdaki MX sürümü 4,2 veya daha eski bir sürümse, uygulamalar sessizce yüklenmez. Daha fazla bilgi için bkz. Zeköşeli Web sitesinde [tam MX özelliği matrisi](http://techdocs.zebra.com/mx/compatibility/) .

Zeköşeli cihazlara dağıtılan LOB uygulamalarının, cihazdaki ortak bir konumdan yüklenmesi gerekir. . Apk uygulama paketine, cihazdaki ortak depolamaya da erişimi olan diğer uygulama ve hizmetlerle erişilebilir. Genellikle bu erişim, uygulamanın indirilmesi tamamlanırken ve yükleme başlangıcında küçük bir pencere olur. Bu pencere bir zamanlama saldırısına izin verebilir. Örneğin, bu pencere sırasında bir. APK paketi değiştirilebilir. Intune,. apk 'nin Genel depolamada harcadığı süreyi en aza indirir ve imzasız uygulamaların yüklenmesine izin vermez. Güvenlik riskini en aza indirmenize yardımcı olmak için karşıya yüklediğiniz. apk dosyalarının hassas bilgiler içermediğinden emin olun.

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft Intune’la uygulamaları ekleme](../apps/apps-add.md)

[İOS/ıpados kullanıcılarınızın uygulamalarını nasıl alır](end-user-apps-ios.md)

[Windows kullanıcılarınız uygulamalarını nasıl alır](end-user-apps-windows.md)
