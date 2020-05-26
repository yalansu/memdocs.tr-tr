---
title: Intune Endpoint Security uç noktası algılama ve yanıt ayarları | Microsoft Docs
description: Uç nokta güvenlik uç noktası algılama ve yanıt ilkesi ayarları Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
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
ms.openlocfilehash: dd53ec47435ba9dc416d2b152719b393d1647f90
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824010"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Intune 'da Endpoint Security için uç nokta algılama ve yanıt ilkesi ayarları

Intune 'un Endpoint Security düğümündeki [Endpoint Detection ve yanıt ilkesi](../protect/endpoint-security-edr-policy.md) için profillerde yapılandırabileceğiniz ayarları görüntüleyin.

Desteklenen platformlar ve profiller:

- **Windows 10 ve üzeri**: Intune ile yönetilen cihazlara dağıttığınız ilke için bu platformu kullanın.
  - Profil: **Endpoint Detection ve yanıt (MDM)**

- **Windows 10 ve Windows Server**: Configuration Manager tarafından yönetilen cihazlara dağıttığınız ilke için bu platformu kullanın.
  - Profil: **Endpoint Detection ve yanıt (ConfigMgr) (Önizleme)**
  
  *Bu platform ve profil genel önizlemede*.

## <a name="endpoint-detection-and-response-mdm"></a>Uç nokta algılama ve yanıt (MDM)

**Uç nokta algılama ve yanıt**:

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

## <a name="endpoint-detection-and-response-configmgr-preview"></a>Uç nokta algılama ve yanıt (ConfigMgr) (Önizleme)

**Uç nokta algılama ve yanıt**:

- **Tüm dosyalar için örnek paylaşımı**  

  Microsoft Defender Gelişmiş tehdit koruması örnek paylaşımı yapılandırma parametresini döndürür veya ayarlar.  
  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**

- **Telemetri raporlama sıklığını hızlandırın**

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -Microsoft Defender Gelişmiş tehdit koruması telemetri raporlama sıklığını artırın.

## <a name="next-steps"></a>Sonraki adımlar

[EDR için uç nokta güvenlik ilkesi](../protect/endpoint-security-edr-policy.md)
