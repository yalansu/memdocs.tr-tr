---
title: Windows 10 Team için Microsoft Intune cihaz kısıtlamaları
titleSuffix: ''
description: Windows 10 Team çalıştıran cihazlar için sağlanan cihaz kısıtlamaları hakkında bilgi edinin.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31457667612617bb573ddfb145ed26f70de33159
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79332270"
---
# <a name="microsoft-intune-windows-10-team-device-restriction-settings"></a>Microsoft Intune Windows 10 Team cihaz kısıtlama ayarları

Bu makalede, Windows 10 Team çalıştıran cihazlar için yapılandırabileceğiniz Microsoft Intune cihaz kısıtlama ayarları gösterilir.

## <a name="apps-and-experience"></a>Uygulamalar ve deneyim

- **Birisi odadayken uyku modundan çıkar** - Algılayıcı, odada birisini algıladığında cihazın otomatik olarak uyanmasına izin verir.
- **Hoş Geldiniz ekranında gösterilen toplantı bilgileri** - Hoş Geldiniz ekranının Toplantılar kutucuğunda gösterilecek bilgileri seçmek için bu seçeneği etkinleştirin. Şunları yapabilirsiniz:
  - **Yalnızca düzenleyeni ve saati göster**
  - **Düzenleyiciyi, saati ve konuyu göster (özel toplantılar için konu gizlidir)**
- **Hoş Geldiniz ekranı arka plan görüntüsü URL’si** - Windows 10 Team cihazlarının **Hoş Geldiniz** ekranında, belirttiğiniz URL’den özel bir arka plan görüntülemek için bu ayarı etkinleştirin.<br>Görüntü PNG biçiminde olmalıdır ve URL **https://** ile başlamalıdır.

## <a name="azure-operational-insights"></a>Azure operasyonel içgörüler

- **Azure Operasyonel İçgörüler** - Microsoft Operations Manager’ın bir parçası olan Azure Operasyonel İçgörüler Windows 10 Team cihazlarından günlük dosyası verilerini toplar, depolar ve analiz eder.
Azure Operasyonel İçgörüler'e bağlanmak için bir **Çalışma Alanı Kimliği** ve bir **Çalışma Alanı Anahtarı** belirtmeniz gerekir.

## <a name="maintenance"></a>Bakım

- **Güncelleştirmeler için bakım penceresi** - Cihazda güncelleştirme gerçekleştirilebildiği zaman pencereyi yapılandırır. Pencerenin **Başlangıç saati** ve **Saat cinsinden süresi**’ni (1-5 saat) yapılandırabilirsiniz.

## <a name="wireless-projection"></a>Kablosuz yansıtma

- **Kablosuz projeksiyon için PIN** - Cihazın kablosuz projeksiyon özelliklerini kullanabilmek için PIN girmenin gerekli olup olmadığını belirtir.
- **Miracast kablosuz projeksiyon** - Windows 10 Team cihazlarının projeksiyon için Miracast özellikli cihazları kullanmasına izin vermek istiyorsanız bu seçeneği etkinleştirin.
- **Miracast kablosuz yansıtma kanalı** - Bağlantı kurmak için kullanılan Miracast kanalını seçin.

## <a name="next-steps"></a>Sonraki adımlar

Profili kaydetmek ve kullanıcılara ve cihazlara atamak için [cihaz kısıtlama ayarlarını yapılandırma](device-restrictions-configure.md) bölümündeki bilgileri kullanın.
