---
title: Intune’da Android cihazları kaydetme
titleSuffix: Microsoft Intune
description: Intune’da Android cihazları kaydetmeyi öğrenin.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/23/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f276d98c-b077-452a-8835-41919d674db5
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b2a948b99abed1f2f7cb988016d047e5d1a86c11
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814996"
---
# <a name="enroll-android-devices"></a>Android cihazlarını kaydetme

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Bir Intune Yöneticisi olarak, Android cihazlarını aşağıdaki yollarla kaydedebilirsiniz:
- Android Enterprise (kullanıcılara en güncel ve güvenli özellikleri sağlayan bir kayıt seçenekleri kümesi sunar):
    - [**Android kurumsal iş profili**](android-work-profile-enroll.md): kişisel cihazlara kurumsal verilere erişim izni verildi. Yöneticiler iş hesaplarını, uygulamaları ve verileri yönetebilir. Cihazdaki kişisel veriler iş verilerinden ayrı tutulur ve yöneticiler kişisel ayarları veya verileri denetlemez. 
    - [**Android kurumsal adanmış**](android-kiosk-enroll.md): dijital imza, Bilet yazdırma veya stok yönetimi gibi şirkete ait, tek kullanım cihazları için. Yöneticiler bir cihazın kullanımını sınırlı sayıda uygulama ve web bağlantısına indirger. Ayrıca kullanıcılar başka uygulama ekleyemez veya farklı eylemler gerçekleştiremez.
    - [**Android kurumsal tam olarak yönetilen**](android-fully-managed-enroll.md): şirkete ait, tek kullanıcı cihazları için özel olarak çalışır ve kişisel kullanım için kullanılır. Yöneticiler cihazın tamamını yönetebilir ve ilke denetimlerini iş profilleri için kullanılamaz hale getirebilirsiniz.
    - [**Android kurumsal şirkete ait iş profili**](android-corporate-owned-work-profile-enroll.md): Kurumsal ve kişisel kullanım için tasarlanan şirkete ait, tek kullanıcı cihazları için.
- Samsung KNOX Standard cihazlar ve [Zeköşeli cihazlar](../configuration/android-zebra-mx-overview.md)dahil olmak üzere [**Android Cihaz Yöneticisi**](android-enroll-device-administrator.md). Android Enterprise 'ın kullanılabildiği alanlarda, Google, yeni Android sürümlerindeki yönetim desteğini azaltarak Cihaz Yöneticisi (DA) yönetimi kapalı teşvik. Ancak, Android Enterprise veya GMS 'nin kullanılamadığı durumlarda, Cihaz Yöneticisi 'ni kullanmak ve bu değişiklikleri öğrenmek isteyeceksiniz. Daha fazla bilgi için bkz. [ülkenizde Android kurumsal mi var](https://support.google.com/work/android/answer/6270910)?

## <a name="prerequisites"></a>Önkoşullar

Mobil cihazların yönetimine hazırlık olarak, **Microsoft Intune**’a mobil cihaz yönetimi (MDM) yetkilisi ayarlamanız gerekir. Yönergeler için bkz. [MDM yetkilisini ayarlama](../fundamentals/mdm-authority-set.md). Bu öğeyi yalnızca mobil cihaz yönetimi için Intune’u ilk defa kurduğunuzda ayarlayabilirsiniz.

Android Enterprise için, Android Enterprise 'ın ülkenizde veya bölgenizde kullanılabilir olduğundan emin olmak için Google 'daki aşağıdaki destek makalesine bakın: https://support.google.com/work/android/answer/6270910

Zeköşeli teknolojiler tarafından üretilen cihazlarda, belirli bir cihazın özelliklerine bağlı olarak Şirket Portalı ek izinler vermeniz gerekebilir. [Zeköşeli cihazlarda Mobility uzantılarında](../configuration/android-zebra-mx-overview.md) daha fazla ayrıntı vardır.

Samsung KNOX Standard cihazlarında [daha fazla önkoşul](android-samsung-knox-mobile-enroll.md)vardır.

## <a name="next-steps"></a>Sonraki adımlar

- [Android kurumsal iş profili kayıtlarını ayarlama](android-work-profile-enroll.md)
- [Android kurumsal adanmış cihaz kayıtlarını ayarlama](android-kiosk-enroll.md)
- [Android kurumsal tam olarak yönetilen kayıtları ayarlama](android-fully-managed-enroll.md)
- [Android Cihaz Yöneticisi kaydını ayarlama](android-enroll-device-administrator.md)

