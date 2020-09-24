---
title: Intune Istemci uygulamalarından isteğe bağlı Tanılama verileri
titleSuffix: Microsoft Intune
description: Intune Istemci uygulamalarının topladığımız isteğe bağlı Tanılama verileri hakkında bilgi edinin.
keywords: Gizlilik, kişisel veriler
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/15/2020
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
ms.openlocfilehash: e4d8833860b5c16375e5a68ea0174d81357df819
ms.sourcegitcommit: bcfacddbee1faa3826eea89697018450dfa9d264
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91134858"
---
# <a name="optional-diagnostic-data-from-intune-client-apps"></a>Intune Istemci uygulamalarından isteğe bağlı Tanılama verileri

Intune, çeşitli Intune istemci uygulamaları aracılığıyla kullanıcıların sorunları algılamak, tanılamak ve onarmak için çeşitli isteğe bağlı veriler toplar.  Bu isteğe bağlı Tanılama verileri, bir sorun haline gelmeden önce, kuruluşunuzdaki sorunları önceden tespit etmek için yardım toplamaktadır. Intune istemci uygulamaları şunları içerir:
- iOS/ıpados Şirket Portalı
- macOS Şirket Portalı
- Windows Şirket Portalı
- Android Şirket Portalı
- Android Intune uygulaması
- MacOS için Yönetim Aracısı Microsoft Intune
- Microsoft Intune Yönetimi uzantısı
- Android mobil uygulama yönetimi (MAM)

İstemcilerden toplanan isteğe bağlı veriler, Intune hizmetlerinin başarıyla çalıştırılması için gerekli değildir. Toplanan veriler yardımcı olur:
- Sorunları proaktif olarak algılamamızı, tanılamanıza ve gidermenize yardımcı olacak gelişmiş bilgiler sağlar.
- Ürün ve hizmet iyileştirmeleri yapar.


## <a name="data-collected"></a>Toplanan veriler

Intune istemci uygulamaları tarafından toplanan isteğe bağlı Tanılama verileri aşağıdaki alanlara sahip olabilir:

- Microsoft tarafından oluşturulan kullanıcı bilgileri
    - Azure AD Kullanıcı KIMLIĞI
    - Cihaz Kimliği
    - Bağıntı Kimliği
    - Uygulama oturum KIMLIĞI
    - Kullanıcı oturum KIMLIĞI
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
Veriler, aşağıdakiler gibi herhangi bir müşteri bilgisini içermez:
- Cihaz adı.
- Telefon numarası.
- Kullanıcının dosya veya fotoğrafının içeriği.


## <a name="turn-off-data-collection"></a>Veri toplamayı kapama
Kullanıcıların bu isteğe bağlı verileri paylaşması için ilginç nedenler olduğunu düşündük. Microsoft 'un kurumsal uygulamalar ve hizmetler için herhangi bir Microsoft 365 uygulamasının kullanımı sırasında topladığı tüm isteğe bağlı Tanılama verileri, ISO/ıEC 19944:2017 (Section 8.3.3) standardında tanımlanan şekilde belirlenir. Kullanıcılar, bireysel cihazları için [kullanım verileri toplamayı kapatabilir](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android) .


## <a name="next-steps"></a>Sonraki adımlar
[Intune 'da veri toplama hakkında daha fazla bilgi edinin.](privacy-data-collect.md)



