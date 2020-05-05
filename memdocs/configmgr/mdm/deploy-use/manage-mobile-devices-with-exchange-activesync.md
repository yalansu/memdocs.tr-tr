---
title: Exchange ile cihaz yönetimi
titleSuffix: Configuration Manager
description: Configuration Manager 'de Exchange Server Bağlayıcısı ile mobil cihazları yönetin.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721930"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Exchange ve Configuration Manager cihaz yönetimi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Exchange Server 'a ActiveSync protokolü aracılığıyla bağlandığınız mobil cihazlarınız varsa, bu cihazları yönetmek için Configuration Manager içindeki Exchange Server bağlayıcısını kullanabilirsiniz. Bağlayıcı, şirket içi Exchange Server veya Exchange Online ile birlikte kullanılabilir. Exchange mobil cihaz yönetimi özelliklerini yapılandırmak için Configuration Manager konsolunu kullanın. Örneğin, birden çok Exchange sunucusu için uzak cihaz temizleme ve ayarlar denetimi.

![Exchange Server bağlayıcısının Configuration Manager ile mantıksal diyagramı](media/configmgr-with-exchange.png)  

Mobil cihazları bu bağlayıcıyla yönetirken, Configuration Manager istemcisini yüklemez veya cihazları MDM aracılığıyla kaydetmez. Exchange Server 'ın yönetim işlevleri bu diğer seçeneklerle karşılaştırıldığında sınırlandırılır. Örneğin, bu cihazları yapılandırmak için yazılım yükleyemez veya yapılandırma öğelerini kullanamazsınız. Daha fazla bilgi için bkz. [Configuration Manager için bir cihaz yönetimi çözümü seçme](../../core/plan-design/choose-a-device-management-solution.md).  

## <a name="policies"></a>İlkeler

Bağlayıcısını kullandığınızda Configuration Manager mobil cihazlarda ayarları yapılandırır. Cihazlar varsayılan Exchange ActiveSync posta kutusu ilkelerini kullanmaz. Aşağıdaki gruplarda kullanmak istediğiniz ayarları tanımlayın:

- **Genel**
- **Parola**
- **E-posta yönetimi**
- **Güvenlik**
- **Uygulama**

Örneğin, **parola** grubunda, aşağıdaki ayarları yapılandırabilirsiniz:

- Mobil cihazların parola gerektirip
- En az parola uzunluğu
- Parola karmaşıklığı
- Parola kurtarmaya izin verilip verilmeyeceğini belirtir

Grupta en az bir ayarı yapılandırdığınızda, Configuration Manager mobil cihazlar grubundaki tüm ayarları yönetir. Grupta herhangi bir ayarı yapılandırmazsanız Exchange, mobil cihazlar için bu ayarları yönetmeye devam eder. Exchange Server 'da yapılandırdığınız ve kullanıcılara atadığınız tüm Exchange ActiveSync posta kutusu ilkeleri hala uygulanır.

## <a name="access-rules-and-remote-actions"></a>Erişim kuralları ve uzak eylemler

Exchange Server bağlayıcısını Exchange erişim kurallarını yönetecek şekilde de yapılandırabilirsiniz. Bu erişim kuralları, mobil cihazların izin verme, engelleme veya karantinaya alma ' yı içerir. Configuration Manager konsolunu kullanarak mobil cihazları uzaktan silebilirsiniz ve kullanıcılar, uygulama kataloğu 'nu kullanarak mobil cihazlarını uzaktan temizleyebilir.

Bir kullanıcının mobil cihazı, yönettiğiniz zaman uygulama kataloğunda otomatik olarak görünür ve Exchange Server şirket içi olduğunda. Exchange Online kullandığınızda mobil cihazın uygulama kataloğunda görünmesi için, Kullanıcı cihaz benzeşimini el ile yapılandırın. Daha fazla bilgi için bkz. [kullanıcıları ve cihazları Kullanıcı cihaz benzeşimi Ile bağlama](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

> [!TIP]  
> Bir mobil cihaz başka bir kullanıcıya aktarıldığında, yeni sahibi cihazda Exchange hesabını yapılandırmadan önce mobil cihazı Configuration Manager konsolundan silin.

## <a name="prerequisites"></a>Önkoşullar

> [!IMPORTANT]  
> Bu bağlayıcıyı yüklemeden önce Configuration Manager Exchange sürümünüzü desteklediğinden emin olun. Daha fazla bilgi için bkz. [desteklenen konfigürasyonlar-Exchange Server Bağlayıcısı](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS).  

### <a name="permissions-to-configure-the-connector"></a>Bağlayıcıyı yapılandırma izinleri

Configuration Manager 'de Exchange Server bağlayıcısını yapılandırmak için aşağıdaki güvenlik izinlerine sahip olmanız gerekir:

- Exchange Server bağlayıcısını eklemek, değiştirmek ve silmek için: **Site** nesnesi için **Değiştirme** izni.  

- Mobil cihaz ayarlarını yapılandırmak için: **Site** nesnesi için **ModifyConnectorPolicy** izni.  

Örneğin, **tam yönetici** yerleşik rolü bu gerekli izinleri içerir.  

### <a name="permissions-to-manage-mobile-devices"></a>Mobil cihazları yönetme izinleri

Mobil cihazları yönetmek için aşağıdaki güvenlik izinlerine sahip olmanız gerekir:  

- Mobil cihazı silmek için: **Koleksiyon** nesnesi için **Kaynağı silme** .  

- Bir silme komutunu iptal etmek için: **Koleksiyon** nesnesi için **Kaynağı değiştirme** .  

- Mobil cihazlara izin vermek ve onları engellemek istiyorsanız: **Koleksiyon** nesnesi için **Kaynağı değiştirme** .  

Örneğin, **Operations Administrator** yerleşik rolü bu gerekli izinleri içerir.

Daha fazla bilgi için bkz. [rol tabanlı yönetimi yapılandırma](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Exchange bağlayıcısını yükleyip yapılandırma](install-configure-exchange-connector.md)
