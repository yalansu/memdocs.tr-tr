---
title: Intune Istemci uygulamalarından isteğe bağlı Tanılama verileri
titleSuffix: Microsoft Intune
description: Intune Istemci uygulamalarının topladığımız isteğe bağlı Tanılama verileri hakkında bilgi edinin.
keywords: Gizlilik, kişisel veriler
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5d78438301e8469189d0c70a2cf52b58938e277
ms.sourcegitcommit: 37dc6b78de8bb904b83a9d571f3c9f414b54f321
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90864501"
---
# <a name="optional-diagnostic-data-from-intune-client-apps"></a>Intune Istemci uygulamalarından isteğe bağlı Tanılama verileri

Intune, çeşitli Intune istemci uygulamaları aracılığıyla kullanıcıların sorunları algılamak, tanılamak ve onarmak için çeşitli isteğe bağlı veriler toplar. Intune istemci uygulamaları şunları içerir:
- iOS/ıpados Şirket Portalı
- macOS Şirket Portalı
- Windows Şirket Portalı
- Android Şirket Portalı
- Android Intune uygulaması
- MacOS sepet
- Windows sepet
- Android mobil uygulama yönetimi (MAM)

İstemcilerden toplanan isteğe bağlı veriler, Intune hizmetlerinin başarıyla çalıştırılması için gerekli değildir. Toplanan veriler yardımcı olur:
- ABD ürün geliştirmeleri yapın.
- Sorunları algılamanıza, tanımamıza ve gidermenize yardımcı olacak gelişmiş bilgiler sağlar.

## <a name="data-collected"></a>Toplanan veriler

Intune istemci uygulamaları tarafından toplanan isteğe bağlı Tanılama verileri aşağıdaki alanlara sahip olabilir:

- Microsoft tarafından oluşturulan kullanıcı bilgileri
    - Azure AD Kullanıcı KIMLIĞI
    - Cihaz Kimliği
    - Bağıntı Kimliği
    - Uygulama oturumu GUID 'SI
    - SDK Kullanıcı KIMLIĞI
- Yönetici ve hesap bilgileri
    - Kiracı Kimliği
    - Azure AD kiracı kimliği
- Donanım ve yazılım bilgileri
    - Cihaz işletim sistemi sürümü
    - Cihaz modeli
    - Cihaz yap
    - Uygulama Kimliği
    - Kullanıcı dili
    - Kullanıcı saat dilimi
- Hizmet olayları ve hata bilgileri
    - Kayıt olayı
    - Hata olayı
        - Ağ hatası
        - Çalışma zamanı hatası
        - Görev zamanlama hatası
        - Kayıt hatası
        - Azure AD kimlik doğrulama hatası
    - Kilitlenme raporu
    - Onay durumu
    - Uyumluluk durumu
    - İlke durumu
- Şirket Portalı olaylar
    - Şirket Portalı hatası
    - Şirket Portalı sayfası eylemi
    - Şirket Portalı sayfa görünümü
    - Şirket Portalı sürümü
- Performans ölçümü
    - Süre
    - Yanıt süresi
 
## <a name="data-not-collected"></a>Toplanan veriler
Veriler, şunun gibi müşteri bilgilerini içermez:
- Cihaz adı.
- Telefon numarası.
- Kullanıcının dosya veya fotoğrafının içeriği.

## <a name="turn-off-data-collection"></a>Veri toplamayı kapama
Kullanıcılar, Ayarlar uygulamasından bireysel cihazları için [kullanım verilerini toplamayı](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android) kapatabilir.


## <a name="next-steps"></a>Sonraki adımlar

[Intune 'da veri toplama hakkında daha fazla bilgi edinin.](privacy-data-collect.md)



