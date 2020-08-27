---
title: Intune için Microsoft Defender virüsten koruma için macOS virüsten koruma ilkesi ayarları | Microsoft Docs
description: MacOS için Microsoft Defender virüsten koruma profilindeki ayarların listesini görüntüleyin. Bu profil, Microsoft Intune gelen macOS için uç nokta güvenlik virüsten koruma ilkesinin bir parçasıdır.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: a75fe5bac4bb99b30e21ec842dcbbe3be83e9e5b
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909457"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Microsoft Intune 'de Mac için Microsoft Defender ATP ayarları

Microsoft Intune ' de Mac için Microsoft Defender ATP için yapılandırabileceğiniz *Virüsten koruma* profili ayarlarını görüntüleyin. Bu ayarlar hakkında daha fazla bilgi için Windows belgelerindeki [Mac Için Microsoft Defender Gelişmiş tehdit koruması](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) bölümüne bakın.

Intune 'da [Endpoint Security ilkelerini](../protect/endpoint-security-policy.md) kullanma hakkında bilgi edinin.

**Microsoft Defender ATP**

- **Gerçek zamanlı koruma**  
  MacOS cihazlarında Defender 'ın gerçek zamanlı Izleme işlevini kullanmasını gerektir. Gerçek zamanlı izleme, kötü amaçlı yazılımın bilgisayarınıza yüklenmesini veya cihazınızı çalıştırmayı engeller. Bu ayarı, otomatik olarak yeniden kapanmadan önce kısa bir süre için kapatabilirsiniz.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir
  - **Etkin** -gerçek zamanlı izlemenin kullanımını zorunlu tutun. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Devre dışı** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Buluta teslim edilen koruma**  
  Varsayılan olarak, Defender bulduğu sorunlar hakkında Microsoft 'a bilgi gönderir. Microsoft, sizi ve diğer müşterileri etkileyen sorunlar hakkında daha fazla bilgi edinmek için bu bilgileri çözümleyerek geliştirilmiş çözümler sunar. Koruma, *Otomatik örnek gönderimi* üzerinde ayarlandığında en iyi şekilde çalışacaktır.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Etkin** -buluta teslim edilen koruma açıktır. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Devre dışı** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Otomatik örnek gönderimi**  
  Cihaz kullanıcılarını ve kuruluşunuzu olası tehditlere karşı korumaya yardımcı olmak için Microsoft 'a örnek dosyalar gönderir.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Etkin** -buluta teslim edilen koruma açıktır.  Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Devre dışı** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Tanılama verileri toplama**

  Tanılama ve kullanım verilerinin Microsoft ile nasıl paylaşılacağını yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Gerekli**
  - **İsteğe bağlı**

- **Taramadan dışlanan klasörler**  
  **Ekle** ' yi seçin ve ardından tarama sırasında yoksayılacak klasörleri belirtin.

- **Taramadan dışlanan dosyalar**  
  **Ekle** ' yi seçin ve ardından tarama sırasında yoksayılacak dosyaları belirtin.

- **Taramadan dışlanan dosya türleri**  
  **Ekle** ' yi seçin ve ardından tarama sırasında yoksayılacak dosya uzantılarını belirtin.

- **Taramadan dışlanan süreçler**  
  **Ekle** ' yi seçin ve ardından tarama sırasında yoksayılacak süreçler belirtin.