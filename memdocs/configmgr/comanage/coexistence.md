---
title: Üçüncü taraf MDM birlikte kullanımı
titleSuffix: Configuration Manager
description: Configuration Manager ile üçüncü taraf MDM hizmetini kullanma hakkında bilgi edinin
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f22ba6f29e0c85e19ab66d1b052085db5303cc2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710828"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Configuration Manager ile üçüncü taraf MDM birlikte bulunma

Windows 10 cihazlarını aynı anda hem Configuration Manager hem de Microsoft Intune ile yönettiğinizde, bu işlevselliğe [ortak yönetim](overview.md)denir. Configuration Manager olan cihazları yönetirken ve bir üçüncü taraf MDM hizmetine kaydettiğinizde, bu işlevselliğe birlikte *bulunma*denir. İkisi arasında düzgün şekilde yönetilemeyeceği tek bir cihaz için iki yönetim yetkilisinin olması zor olabilir. Ortak yönetim sayesinde, Configuration Manager ve Intune, çakışma olmadığından emin olmak için [iş yüklerini](workloads.md) dengeleyin. Bu etkileşim, üçüncü taraf hizmetlerde mevcut olmadığından, birlikte bulunma yönetim özellikleri ile ilgili sınırlamalar vardır.

Configuration Manager istemcisi, Windows 10 sürüm 1709 veya üstünü çalıştıran bir cihazda bir üçüncü taraf MDM hizmeti ile birlikte çalışabilir ve Azure Active Directory birleştirilir. Cihaz aşağıdaki türlerden biri olabilir:

- [Azure AD-yalnızca birleştirilmiş](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) . (Bu tür bazen "bulut etki alanına katılmış" olarak adlandırılır)  

- Cihazın şirket içi Active Directory katıldığı ve Azure Active Directory kaydedildiği [karma etki alanına katılmış](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).  

> [!Note]  
> [Kişisel cihazları](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device)desteklemez.  

Configuration Manager istemcisi bir üçüncü taraf MDM hizmetinin de cihazı yönetiyor algıladığında, Configuration Manager içindeki belirli iş yüklerini otomatik olarak devre dışı bırakır. Bu davranış MDM hizmetinin bu işlevleri almasına izin verir. Ayrıca, istemci üzerinde, cihazı ve Kullanıcı deneyimini olumsuz yönde etkileyebilecek çakışan ayarları da engeller. Configuration Manager içindeki aşağıdaki iş yükleri bu durumda devre dışı bırakılır:

- VPN, Wi-Fi, e-posta ve sertifika ayarları için kaynak erişim ilkeleri
- Eski paketler dahil olmak üzere uygulama yönetimi
- Yazılım güncelleştirme tarama ve yükleme
- Endpoint Protection, Windows Defender 'ın kötü amaçlı yazılımdan koruma özellikleri paketi
- Koşullu erişim için uyumluluk ilkesi
- Cihaz yapılandırması
- Office Tıkla-Çalıştır yönetimi

Configuration Manager istemcisi, aşağıdaki salt okuma işlemlerine devam ederek üçüncü taraf yönetim yetkilisi ile çakışmayı önler:

- Donanım ve yazılım envanteri
- Varlık Yönetim Bilgileri
- Yazılım kullanım ölçümü
- Güç yönetimi raporlaması

Configuration Manager ve Intune ile ortak yönetimin avantajları hakkında daha fazla bilgi için bkz. [ortak yönetim avantajları](overview.md#benefits).
