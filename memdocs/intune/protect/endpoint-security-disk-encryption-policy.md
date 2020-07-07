---
title: Microsoft Intune | uç nokta güvenlik ilkeleriyle disk şifrelemeyi yönetme | Microsoft Docs
description: Microsoft Endpoint Manager 'daki Endpoint Security disk şifreleme ilkesiyle yönettiğiniz cihazlar için ilkeleri yapılandırın ve dağıtın.
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
ms.openlocfilehash: 3e01e54eb6e74c8139c266d677a6406554119273
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.contentlocale: tr-TR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972088"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Intune 'da uç nokta güvenliği için disk şifreleme ilkesi

Endpoint Security disk şifreleme profilleri, yalnızca bir cihaz yerleşik Şifreleme yöntemiyle ilgili olan, Filekasası veya BitLocker gibi ayarları odaklamaktadır. Bu odak, güvenlik yöneticilerinin, ilişkisiz ayarların bulunduğu bir konakta gezinmek gerekmeden disk şifreleme ayarlarını yönetmesini kolaylaştırır.

Cihaz yapılandırması için *Endpoint Protection* profillerini kullanarak aynı cihaz ayarlarını yapılandırabilmeniz durumunda, cihaz yapılandırma profilleri ek ayar kategorileri içerir. Bu ek ayarlar disk şifrelemesi ile ilgisiz değildir ve yalnızca disk şifrelemesini yapılandırma görevini karmaşıklaştırabilir.

[Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)'Nin **uç nokta güvenlik** düğümünde *Yönet* altında disk şifrelemesi için uç nokta güvenlik ilkelerini bulun.

## <a name="prerequisites-for-disk-encryption-policy"></a>Disk şifreleme ilkesi önkoşulları

- **MacOS** -macos 10,13 veya üzeri
- **Windows** -Windows 10 veya üzeri

## <a name="disk-encryption-profiles"></a>Disk şifreleme profilleri

**MacOS profilleri**:

- **Filekasası** -dosya Kasası, MacOS cihazları Için yerleşik tam disk şifrelemesi sağlar.

  MacOS için [Dosya Kasası ayarlarını](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) yönetin.

  Bir dosya Kasası profili oluşturmak için bkz. [macOS Için Filekasadisk şifrelemeyi kullanma](../protect/encrypt-devices-filevault.md).

**Windows 10 profilleri**:

- **BitLocker** -BitLocker Sürücü Şifrelemesi, işletim sistemiyle tümleştirilen ve kaybolan, çalınan veya uygun olmayan bilgisayarlardan gelen veri hırsızlığı veya etkilenme tehditlerini ele alan bir veri koruma özelliğidir

  Windows 10 için [BitLocker ayarlarını](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) yönetin.

  BitLocker profili oluşturmak için bkz. [Windows 10 Için BitLocker disk şifrelemesi kullanma](../protect/encrypt-devices.md).

## <a name="manage-device-encryption"></a>Cihaz şifrelemesini yönetme

Bir cihaz diskini şifrelemek üzere ilke dağıttıktan sonra, şifrelemeyi yönetme hakkında bilgi için aşağıdaki makalelere bakın:

- [seçin,](../protect/encrypt-devices.md#manage-bitlocker)
- [Dosya kasasını yönetme](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Cihaz şifrelemesini izleme](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Sonraki adımlar

- [Bir dosya Kasası profili oluşturmak için](../protect/encrypt-devices-filevault.md#create-endpoint-security-policy-for-filevault)
- [BitLocker profili oluşturmak için](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
