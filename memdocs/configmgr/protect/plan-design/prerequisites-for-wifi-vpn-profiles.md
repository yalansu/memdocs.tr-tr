---
title: Wi-Fi ve VPN profili önkoşulları
titleSuffix: Configuration Manager
description: Configuration Manager ' de Wi-Fi profillerini ve VPN profillerini yönetme önkoşulları hakkında bilgi edinin
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722133"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager 'de Wi-Fi ve VPN profilleri için Önkoşullar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager 'daki Wi-Fi ve VPN profillerinin yalnızca ürün içinde bağımlılıkları vardır.

Sertifika profilleri, Wi-Fi profilleri ve VPN profilleri gibi şirket kaynaklarına erişim ayarlarını yönetmek için aşağıdaki güvenlik izinlerine sahip olmanız gerekir:  

- Wi-Fi ve profiller için uyarıları ve raporları görüntülemek ve yönetmek için: **Uyarılar** nesnesi için **Oluştur**, **Sil**, **Değiştir**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .  

- Sertifika profilleri oluşturup yönetmek için: **sertifika profili** nesnesi Için **Ilke yaz**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .  

- Wi-Fi, sertifika ve VPN profili dağıtımlarını yönetmek için: **koleksiyon** nesnesi Için **yapılandırma Ilkeleri dağıt**, **İstemci Durumu Uyarısını Değiştir**, **Oku**ve **kaynağı oku** .  

- Tüm yapılandırma ilkelerini yönetmek için: **yapılandırma ilkesi** nesnesi için **Oluştur**, **Sil**, **Değiştir**, **Oku**ve **güvenlik kapsamını ayarla** .  

- Wi-Fi ve VPN profilleriyle ilgili sorguları çalıştırmak için: **sorgu** nesnesi için **Oku** izni.  

- Configuration Manager konsolundaki Wi-Fi ve VPN profilleri bilgilerini görüntülemek için: **site** nesnesi için **Oku** izni.  

- Wi-Fi ve VPN profillerinin durum iletilerini görüntülemek için: **durum iletileri** nesnesi için **Oku** izni.  

- Güvenilen CA sertifika profili oluşturup değiştirmek için: **GÜVENILIR CA sertifika profili** nesnesi Için **Ilke yaz**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .  

- VPN profilleri oluşturup yönetmek için: **VPN profili** nesnesi Için **Ilke yaz**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .  

- Wi-Fi profilleri oluşturup yönetmek için: **Wi-Fi profili** nesnesi Için **Ilke yaz**, **Raporu Değiştir**, **Oku**ve **Raporu Çalıştır** .  

**Şirket kaynağı Erişim Yöneticisi** yerleşik güvenlik rolü, Configuration Manager Wi-Fi profillerini yönetmek için gereken bu izinleri içerir. Daha fazla bilgi için bkz. [güvenliği yapılandırma](../../core/plan-design/security/configure-security.md).
