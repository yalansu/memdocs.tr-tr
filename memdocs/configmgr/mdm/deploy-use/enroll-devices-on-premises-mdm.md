---
title: Cihazları şirket içi MDM için kaydetme
titleSuffix: Configuration Manager
description: Configuration Manager ' de şirket içi mobil cihaz yönetimi (MDM) için cihaz kaydetme yöntemleri hakkında bilgi edinin.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720677"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager Şirket içi MDM için cihazları kaydetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager Şirket içi mobil cihaz yönetimi (MDM) ile cihazları yönetmek için önce bunları kaydetmeniz gerekir. Configuration Manager, yönetim görevleri için cihazlarla iletişim kurabilir. Configuration Manager cihazları kaydetmek için iki yöntem sunar:

- **Kullanıcı kaydı**: kullanıcılar, kendi cihazındaki kayıt işlemini başlatır. Kullanıcı kaydının başarılı olması için, güvenilir kök sertifikayı cihaza yükledikten sonra istemci ayarları ' nda kullanıcıyı kayıt için sağlayın. Bir cihazı kaydetmek için kullanıcının kimlik bilgilerini girmesi yeterlidir.

    Daha fazla bilgi için bkz. [Kullanıcılar cihazları nasıl kaydeder](user-enroll-devices-on-premises-mdm.md).

- **Toplu kayıt**: Cihazın kullanıcısı kayıt başlatmaz. Configuration Manager ' de bir toplu kayıt paketi oluşturabilirsiniz. Cihazda açtığınızda, paket cihazı kaydetmek için gereken bilgileri sağlar.

    Daha fazla bilgi için bkz. [cihazları toplu kaydetme](bulk-enroll-devices-on-premises-mdm.md).

Şirket içi MDM 'de cihaz kaydı için Configuration Manager desteklediği işletim sistemi sürümleri hakkında daha fazla bilgi için bkz. [desteklenen konfigürasyonlar](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).
