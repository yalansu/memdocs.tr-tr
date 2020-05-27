---
title: Intune ve Azure cihaz sınırı kısıtlamaları arasında anlayın
titleSuffix: ''
description: Intune 'un cihaz sınırı kısıtlamaları ve Azure AD 'nin sınırlandırma kısıtlamaları arasındaki farkları anlayın.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8610b619a4ac05f37b893060b3b3a2bcb1dae528
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864863"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Intune ve Azure AD 'nin cihaz sınır kısıtlamalarını anlayın

Cihaz sınırı kısıtlamaları iki şekilde yapılandırılabilir:
- Intune kaydı
- Azure Active Directory (AD) birleştirilmiş veya Azure AD kayıtlı

Bu makalede, bu limitlerin yapılandırmanıza göre ne zaman uygulandığı açıklanır.

## <a name="intune-device-limit-restrictions"></a>Intune cihaz sınırı kısıtlamaları

Intune cihaz sınırı kısıtlamaları, bir kullanıcının denetleyebileceği maksimum cihaz sayısını ayarlar (en fazla ayar 15 ' tir). Bu **cihaz sınırını**ayarlamak için [Microsoft Endpoint Manager Yönetim Merkezi](https://go.microsoft.com/fwlink/?linkid=2109431)  >  **cihazlar**  >  **Kayıt kısıtlamaları**' na gidin. Daha fazla bilgi için bkz. [cihaz sınır kısıtlaması oluşturma](enrollment-restrictions-set.md#create-a-device-limit-restriction)

## <a name="azure-device-limit-restriction"></a>Azure cihaz sınırı kısıtlaması

Azure cihaz sınırı kısıtlamaları, Azure AD 'nin birleşen fazla cihaz sayısını veya Azure AD kayıtlarını ayarlar. **Kullanıcı başına en fazla cihaz sayısını**ayarlamak için Azure Portal > **Azure Active Directory**  >  **cihazlara**gidin. Daha fazla bilgi için bkz. [cihaz ayarlarını yapılandırma](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal)

## <a name="settings-applied-based-on-user-affinity"></a>Kullanıcı benzeşimi temelinde uygulanan ayarlar

Hem Intune hem de Azure cihaz sınırı kısıtlaması varsa, aşağıdaki tabloda Kullanıcı benzeşim ayarınız temelinde nelerin uygulandığı gösterilmektedir.

| Cihaz platformu | Kullanıcı benzeşimi | Azure geçerlidir | Intune geçerlidir |
| ----- | ----- | ----- | ----- | ----- |
| Android kurumsal iş profili | Yes | Yes | Yes|
| Android kurumsal adanmış cihaz | Hayır | Hayır | Hayır |
| Android kurumsal tam yönetilen | Yes | Yes | Yes |
| Android cihaz yöneticisi | Yes | Yes | Yes |
| Android Cihaz Yöneticisi DEM | Hayır | | Hayır | 
| iOS/macOS BYOD | Yes | Yes | Yes |
| iOS/macOS otomatik cihaz kaydı (ADE) | Yes | Yes | Yes |
| iOS/macOS ADE | No | Yes | No |
| Windows BYOD | Yes | Yes | Yes |
| Yalnızca Windows MD | | Yes | Yes |
| Windows Azure AD 'ye katılmış| Yes | Yes | No |
| Windows Autopilot | Yes | Yes | No |
| Windows hibrit Azure AD 'ye katılmış | Hayır | Hayır | Yes |
| Windows ortak yönetimi | No | Yes | No |
| Windows DEM | No | Yes | No |
| Windows Toplu kaydı | No | Yes | No |


## <a name="android-and-ios-devices"></a>Android ve iOS cihazları

### <a name="ios-or-android-devices-example-1"></a>iOS veya Android cihazları örnek 1

- Azure **Kullanıcı başına en fazla cihaz sayısı** ayarı 3 olarak ayarlanır.
- Intune **cihaz sınırı** ayarı 5 olarak ayarlanır.
 
**Sonuç:** En yüksek sayı Kullanıcı başına. Örneğin, üç Intune cihazı kaydederseniz, cihazların kayıt sayısını sınırlayan ayarlar nedeniyle dördüncü cihazın Azure kaydı başarısız olur.

### <a name="ios-or-android-devices-example-2"></a>iOS veya Android cihazları örnek 2

- Azure **Kullanıcı başına en fazla cihaz sayısı** ayarı 20 olarak ayarlanır.
- Intune **cihaz sınırı** ayarı 2 olarak ayarlanır.

**Sonuç:** İki cihazı başarıyla kaydedebilir ve kaydedebilirsiniz. Intune kaydı, diğer tüm cihazlar için engellenir. Kullanıcı benzeşimi olmadan ADE, bir kullanıcıyla ilişkilendirilmese de Azure cihaz kayıt sınırları tarafından kısıtlanır.

## <a name="windows-devices"></a>Windows cihazları

Intune cihaz sınırı kısıtlamaları aşağıdaki Windows kayıt türleri için uygulanmaz:
- Ortak yönetilen kayıtlar
- Grup İlkesi nesnesi (GPO) kayıtları
- Azure AD 'ye katılmış kayıtlar
- Toplu Azure AD 'ye katılmış kayıtlar
- Autopilot kayıtları
- Cihaz kayıt yöneticisi kayıtları

Paylaşılan cihaz senaryolarında kabul edildiği için, bu kayıt türleri için cihaz sınırı kısıtlamalarını zorunlu kılamaz. Azure Active Directory'de bu kayıt türleri için sabit sınır belirleyebilirsiniz.

Azure 'daki cihaz sınırı kısıtlaması için, **Kullanıcı başına en fazla cihaz sayısı** ayarı, Azure AD 'ye katılmış veya Azure AD 'ye kayıtlı cihazlar için geçerlidir. Bu ayar, karma Azure AD 'ye katılmış cihazlar için geçerlidir.

### <a name="windows-10-example-1"></a>Windows 10 örnek 1

- Azure **Kullanıcı başına en fazla cihaz sayısı** ayarı 5 olarak ayarlanır.
- Intune **cihaz sınırı** ayarı 3 olarak ayarlanır.
- Cihazlar karma Azure AD 'ye katılmış ve otomatik olarak kaydedilmiş (GPO yapılandırılmış).

**Sonuç:** Kayıt GPO aracılığıyla gönderildiği için, Azure cihaz kayıt sınırı uygulanmaz.  Intune cihaz sınırı kısıtlaması de uygulanmaz.

### <a name="windows-10-example-2"></a>Windows 10 örnek 2

- Azure **Kullanıcı başına en fazla cihaz sayısı** ayarı 5 olarak ayarlanır.
- Intune **cihaz sınırı** ayarı 2 olarak ayarlanır.
- Cihazlar yerel etki alanına katılmış ve **Ayarlar**  >  **iş veya okul**  >  **Connect**erişimi kullanılarak kaydedilir.

**Sonuç:** Engellenmeleri için yalnızca iki cihaz kaydedebilirsiniz. En fazla beş cihaz kaydedebilirsiniz.


## <a name="next-steps"></a>Sonraki adımlar

- [Azure 'da bir cihaz sınırı kısıtlaması oluşturun.](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Azure 'da cihaz ayarlarını yapılandırın.](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [Kayıt ve etki alanına katılmış hakkında daha fazla bilgi edinin.](https://docs.microsoft.com/azure/active-directory/devices/overview#getting-devices-in-azure-ad)
