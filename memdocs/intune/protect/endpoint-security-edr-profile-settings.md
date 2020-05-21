---
title: Intune Endpoint Security uç noktası algılama ve yanıt ayarları | Microsoft Docs
description: Uç nokta güvenlik uç noktası algılama ve yanıt ilkesi ayarları Microsoft Intune
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
ms.reviewer: mattsha
ms.openlocfilehash: dd41cfc0d08771c461e6f681ed18791535202bef
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431316"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Intune 'da Endpoint Security için uç nokta algılama ve yanıt ilkesi ayarları

Endpoint [Security ilkesinin](../protect/endpoint-security-policy.md)bir parçası olarak, Intune 'un uç nokta güvenlik düğümündeki *Endpoint Detection ve yanıt* ilkesi için profillerde yapılandırabileceğiniz ayarları görüntüleyin.

Desteklenen platformlar ve profiller:

- **Windows 10 ve üzeri**:
  - Profil: **Endpoint Detection ve yanıt**

## <a name="endpoint-detection-and-response-profile"></a>Uç nokta algılama ve yanıt profili

### <a name="endpoint-detection-and-response"></a>Uç nokta algılama ve yanıt

- **Microsoft Defender ATP istemci yapılandırma paketi türü**

  Microsoft Defender ATP istemcisini eklemek için kullanılacak imzalı bir yapılandırma paketini karşıya yükleyin.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Blob ekleme**  
  - **Blob çıkarma blobu**  

  *BLOB 'U ekleme*' ye ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:

  - **Gelişmiş tehdit koruması ekleme blobu**  
    Dosya belirttiğinizde *ekleme dosyası seç* bölmesini açmak için **ekleme dosyası seç** ' e tıklayın `.onboarding` .

  *Çıkarma blobu*olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:
  
  - **Gelişmiş tehdit koruması çıkarma blobu**  
     Dosya belirttiğiniz yerde dosya *Seç* bölmesini açmak Için dosya **Seç** ' e tıklayın `.offboarding` .

- **Tüm dosyalar için örnek paylaşımı**  

  Microsoft Defender Gelişmiş tehdit koruması örnek paylaşımı yapılandırma parametresini döndürür veya ayarlar.  
  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**

- **Telemetri raporlama sıklığını hızlandırın**

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -Microsoft Defender Gelişmiş tehdit koruması telemetri raporlama sıklığını artırın.

## <a name="next-steps"></a>Sonraki adımlar

[EDR için uç nokta güvenlik ilkesi](../protect/endpoint-security-edr-policy.md)
