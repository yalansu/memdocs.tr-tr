---
title: Wi-Fi ve VPN profili güvenliği ve gizliliği
titleSuffix: Configuration Manager
description: Configuration Manager 'de cihazların Wi-Fi ve VPN profillerini yönetmeye yönelik güvenlik önerileri hakkında bilgi edinin.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722070"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager 'de Wi-Fi ve VPN profilleri için güvenlik ve Gizlilik

*Uygulama hedefi: Configuration Manager (geçerli dal)*

## <a name="security-recommendations"></a>Güvenlik önerileri

Cihazlar için Wi-Fi ve VPN profillerini yönetirken aşağıdaki en iyi güvenlik yöntemlerini kullanın.

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>Wi-Fi ve VPN altyapınızın ve istemci işletim sistemlerinin destekleyebileceği en güvenli seçenekleri seçin

Wi-Fi ve VPN profilleri, cihazlarınızın zaten desteklediği Wi-Fi ve VPN ayarlarını merkezi olarak dağıtmak ve yönetmek için kullanışlı bir yöntem sağlar. Configuration Manager, Wi-Fi veya VPN işlevselliği eklemez. Cihazlarınız ve altyapınızın tüm güvenlik önerilerini belirleyip uygulayın.

## <a name="privacy-information"></a>Gizlilik bilgileri

Wi-Fi ve VPN profillerini, istemci cihazlarını Wi-Fi ve VPN sunucularına bağlanacak şekilde yapılandırmak için kullanabilirsiniz. Ardından bu cihazların profiller uygulandıktan sonra uyumlu olup olmadığını değerlendirmek için Configuration Manager kullanın. Yönetim noktası uyumluluk bilgisini site sunucusuna gönderir ve bu bilgi site veritabanında depolanır. Bilgiler, cihazlar yönetim noktasına gönderilirken şifrelenir, ancak site veritabanında şifreli biçimde depolanmaz. Veritabanı, site bakım görevi **Eski Yapılandırma Yönetimi Verilerini Sil** onu silene dek bilgileri saklar. Varsayılan silme aralığı 90 gündür, ancak bunu değiştirebilirsiniz. Uyumluluk bilgileri Microsoft 'a gönderilmez.

Varsayılan olarak, cihazlar Wi-Fi ve VPN profillerini değerlendirmez. Ayrıca, profilleri yapılandırmalı ve ardından kullanıcılara dağıtmanız gerekir.  

Wi-Fi veya VPN profillerini yapılandırmadan önce gizlilik gereksinimlerinizi göz önünde bulundurun.  
