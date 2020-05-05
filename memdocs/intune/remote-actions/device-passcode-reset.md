---
title: Microsoft Intune - Azure ile cihaz geçiş kodlarını sıfırlama | Microsoft Docs
description: Intune ile yönettiğiniz veya izlediğiniz cihazlarda Geçiş kodunu kaldır eylemini kullanarak geçiş kodunu kaldırın veya sıfırlayın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 47181d19-4049-4c7a-a8de-422206c4027e
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef7a076c0a41e84e0028da6655569401f334772c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078983"
---
# <a name="reset-or-remove-a-device-passcode-in-intune"></a>Intune’da bir cihazın geçiş kodunu sıfırlama veya kaldırma

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Bu belgede, Android Enterprise 'ta (eski adıyla Android for Work veya AfW) cihaz düzeyinde geçiş kodu sıfırlama ve iş profili geçiş kodu sıfırlama açıklanmaktadır. Her biri için gereksinimler farklılık gösterebileceğinden, bu ayrımı dikkate almak önemlidir. Cihaz düzeyinde bir geçiş kodu sıfırlaması geçiş kodunu cihazın tamamı için sıfırlar. Bir iş profili geçiş kodu sıfırlama, geçiş kodunu yalnızca Android kurumsal cihazlarındaki kullanıcının iş profili için sıfırlar.

## <a name="supported-platforms-for-device-level-passcode-reset"></a>Cihaz düzeyinde geçiş kodu sıfırlama için desteklenen platformlar

| Platform | Destekleniyor mu? |
| ---- | ---- |
| Sürüm 6.x veya öncesindeki Android cihazları | Yes |
| Cihaz sahibi olarak kaydedilmiş Android Kurumsal cihazları | Yes |
| iOS/ıpados cihazları | Yes |
| Kullanıcı kaydıyla kaydedilen iOS/ıpados cihazları | Hayır |
| İş profiliyle kaydedilmiş Android cihazları | Hayır |
| Sürüm 7.0 veya üzeri Android cihazlar | Hayır |
| Mac OS | Hayır |
| Windows | Hayır |

Android cihazlarda, bu, cihaz düzeyi geçiş kodu sıfırlamasının yalnızca 6. x veya önceki sürümleri çalıştıran cihazlarda ya da bilgi noktası modunda çalışan Android kurumsal cihazlarda desteklenir. Bunun nedeni, Google 'ın bir Android 7 cihazının geçiş kodunu/parolasını bir cihaz yöneticisi tarafından verilen uygulama içinden sıfırlama desteğinin kaldırılmasına ve tüm MDM satıcılarına uygulanmasından kaynaklanır.

## <a name="supported-platforms-for-android-enterprise-work-profile-passcode-reset"></a>Android kurumsal iş profili geçiş kodu sıfırlaması için desteklenen platformlar

| Platform | Destekleniyor mu? |
| ---- | ---- |
| Bir iş profili ile kaydedilmiş ve sürüm 8.0 ve sonrasını çalıştıran Android kurumsal cihazlar | Yes |
| Bir iş profili ile kaydedilmiş ve sürüm 7.x ve öncesini çalıştıran Android kurumsal cihazlar | Hayır |
| Sürüm 7.x ve öncesini çalıştıran Android cihazlar | Hayır |

Yeni bir iş profili geçiş kodu oluşturmak için Geçiş Kodunu Sıfırla eylemini kullanın. Bu eylem, bir geçiş kodu sıfırlaması ister ve yalnızca iş profili için yeni, geçici bir geçiş kodu oluşturur. 

## <a name="reset-a-passcode"></a>Geçiş kodu sıfırlama


1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431) şu rollerden herhangi biriyle oturum açın: Azure Active Directory genel yönetici, Azure Active Directory Intune Hizmet Yöneticisi, yardım masası Işleci veya rol yöneticisi.
2. **Cihazlar**’ı ve ardından **Tüm Cihazlar**’ı seçin.
3. Yönettiğiniz cihazların listesinden bir cihaz seçin ve **geçiş kodunu Sıfırla**' yı seçin.

## <a name="reset-android-work-profile-and-device-owner-passcodes"></a>Android iş profilini ve cihaz sahibi geçiş kodlarını Sıfırla

İş profili ile kaydolmuş desteklenen Android Kurumsal cihazları, yeni bir yönetilen profil kilidi açma parolası veya son kullanıcı için bir yönetilen profil sınaması alır.

Sürüm 8. x veya üzeri çalıştıran Android kurumsal iş profili cihazlarında, son kullanıcılar kayıt tamamlandıktan hemen sonra sıfırlama geçiş kodunu etkinleştirmek için bildirim alırlar. Bir iş profili parolası gerekli ve ayarlıysa bildirim görüntülenir. Geçiş kodu girildikten sonra bildirim kapatılır.

Sürüm 8. x veya sonrasını çalıştıran Android kurumsal cihaz sahibi veya iş profili cihazlarında, sıfırlama geçiş kodu konsolundan seçildikten sonra, MEM Intune yöneticisine geçici bir geçiş kodu sunulur. Geçici geçiş kodu cihaza girilmelidir. Cihazın geçici geçiş kodu konsolda 7 gün boyunca görüntülenir.


## <a name="remove-iosipados-passcodes"></a>İOS/ıpados geçiş kodlarını kaldır

Geçiş yapmak yerine, geçiş kodlarını iOS/ıpados cihazlarından kaldırılır. Ayarlı bir geçiş kodu uyumluluk ilkesi varsa, cihaz kullanıcıdan Ayarlar'da yeni bir geçiş kodu ayarlamasını ister.

## <a name="next-steps"></a>Sonraki adımlar

Az önce gerçekleştirdiğiniz eylemin durumunu görmek için **Cihazlar**’da, **Cihaz eylemleri**’ni seçin.
