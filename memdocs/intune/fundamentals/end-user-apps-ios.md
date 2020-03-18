---
title: İOS/ıpados kullanıcılarınızın uygulamalarını nasıl alır
description: İOS/ıpados uygulamalarını son kullanıcılar için kullanılabilir hale getirme yöntemleri
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326866"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>İOS/ıpados kullanıcılarınızın uygulamalarını nasıl alır

Microsoft Intune aracılığıyla dağıttığınız uygulamaları son kullanıcılarınızın nasıl ve nereden alacağını anlamak için bu bilgileri kullanın.

**Gerekli uygulamalar**--Platforma bağlı olarak yönetici tarafından gerekli kılınan ve en düşük kullanıcı katılımıyla cihaza yüklenen uygulamalar.

**Kullanılabilir uygulamalar**--Şirket Portalı uygulama listesinde sağlanan ve kullanıcıların isteğe bağlı olarak yüklemeyi seçebileceği uygulamalar.

**Yönetilen uygulamalar**--İlkeler aracılığıyla yönetilebilen ve Intune tarafından “sarmalanmış” veya Intune Uygulama Yazılım Geliştirme Seti (SDK) ile oluşturulmuş uygulamalardır. Bu uygulamalar Intune tarafından yönetilebilir ve bunlara uygulama koruma ilkeleri uygulanabilir.

**Yönetilmeyen uygulamalar**--kullanıcıların Intune uygulama SDK 'sı ile tümleştirilen IOS/ıpados App Store 'dan indirebileceği uygulamalar. Intune, bu uygulamaların dağıtım, yönetim veya seçmeli silme üzerinde herhangi bir denetime sahip değildir.  

Kayıtlı kullanıcılar, Şirket Portalı uygulamasının Uygulamalar ekranında aşağıdaki kutucuklara dokunarak uygulamalarını alabilir:

- **Tüm Uygulamalar**, [Şirket Portalı web sitesinin](https://portal.manage.microsoft.com) TÜMÜ sekmesindeki tüm uygulamaların listesine yönlendirir.

- **Öne Çıkan Uygulamalar**, kullanıcıları Şirket Portalı web sitesinin ÖNE ÇIKAN sekmesine götürür.

- **Kategoriler**, Şirket Portalı web sitesinin KATEGORİLER sekmesine yönlendirir.

![iOS Şirket Portalı uygulaması ekranı](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

Uygulama ekleme hakkında bilgi için bkz. [Microsoft Intune’a uygulama ekleme](../apps/apps-add.md).

## <a name="app-management-takeover"></a>Uygulama yönetimi
Bir uygulama son kullanıcının cihazında zaten yüklüyse iOS/ıpados cihazı, uygulamanın kuruluşunuza göre yönetimine izin veren bir uyarı gösterir. Son Kullanıcı, uygulama yapılandırmalarının yönetilen bir cihaza uygulanmadan önce kuruluşun yönetim geçirmesine izin vermelidir. Kullanıcı uyarıyı iptal ederse, cihaz yönetildiği ve uygulamanın atandığı sürece uyarı düzenli aralıklarla görüntülenir.  


![Uygulama yönetimi değişiklik uyarısının görüntüsü, Iptal ve yönetim seçeneklerini gösterir.](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>Ayrıca bkz.  

[Android kullanıcılarınız uygulamalarını nasıl alır](end-user-apps-android.md)

[Windows kullanıcılarınız uygulamalarını nasıl alır](end-user-apps-windows.md)
