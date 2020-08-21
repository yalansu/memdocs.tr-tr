---
title: Cihaz yönetim çözümü seçme
titleSuffix: Configuration Manager
description: Microsoft 'un bilgisayarları, sunucuları ve cihazları yönetmek için sunduğu çözümler hakkında bilgi edinin.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877345e64045530193a4cdd735cdd399235b90c7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700274"
---
# <a name="choose-a-device-management-solution"></a>Cihaz yönetim çözümü seçme

Microsoft, bilgisayarları, sunucuları ve cihazları yönetmek için farklı çözümler sunar. Bu çözümler şirket içi, bulut tabanlı veya her ikisinin bir birleşimi ile kullanılabilir. Kuruluşunuzun iş gereksinimleri için doğru çözümü seçin. Yönetmeniz gereken cihaz platformları ve ihtiyacınız olan yönetim işlevleri için kararınızı temel edin.

## <a name="overview"></a>Genel Bakış

Farklı senaryolarda sizin için en iyi şekilde çalışgerekebilecek birkaç Microsoft çözümü vardır. Yalnızca bir tane seçmeniz gerekmez.

- Küçük bir kuruluş için, Windows Yönetim Merkezi gibi bir araç harika bir şekilde olabilir.
- BT kuruluşlarının yaklaşık %75 ' ü, cihazlarını yönetmek için Configuration Manager kullanır.
- Microsoft Azure, bulutta veya şirket içinde, birincil olarak sunucu yönetimini hedefleyen Azure Stack çeşitli çözümler sağlar.
- Microsoft Intune, istemcilerin bulut yönetimini sağlar.
- Configuration Manager ve Intune 'U ortak yönetim ile birleştirebilirsiniz.

Bu yönetim teknolojilerini karşılaştırmanıza yardımcı olması için aşağıdaki tabloyu kullanın:

|  | Yalnızca bulut | Buluta bağlı | Şirket içi | Bağlantı kesildi |
|---------|---------|---------|---------|---------|
| **Hyper-V konağı** | Geçerli değil | -Azure Stack<br/> -Windows Yönetim Merkezi<br/> -Virtual Machine Manager | -Azure Stack<br/> -Windows Yönetim Merkezi<br/> -Virtual Machine Manager | -Azure Stack<br/> -Windows Yönetim Merkezi<br/> -Virtual Machine Manager |
| **Windows Server** | -Azure yönetimi<br/> -Configuration Manager | -Azure yönetimi<br/> -Configuration Manager | -Azure yönetimi<br/> -Configuration Manager | Configuration Manager |
| **Linux sunucusu** | Azure yönetimi | Azure yönetimi | Azure yönetimi |  |
| **Windows 10** | -Intune<br/> -Configuration Manager | -Intune<br/> -Configuration Manager | -Intune<br/> -Configuration Manager | Configuration Manager |
| **Windows 7 veya 8,1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows Sanal Masaüstü** | Configuration Manager | Geçerli değil | Geçerli değil | Geçerli değil |

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Azure Stack nedir?](/azure-stack/operator/azure-stack-overview)
- [Windows Yönetim Merkezi nedir?](/windows-server/manage/windows-admin-center/understand/what-is)
- [Virtual Machine Manager nedir?](/system-center/vmm/overview)
- [Azure yönetim ürünleri](/azure/)
- [Windows Sanal Masaüstü nedir?](/azure/virtual-desktop/overview)

Configuration Manager ve Intune çözümleri hakkında daha fazla bilgi için sonraki bölüme geçin.

## <a name="client-management"></a>İstemci yönetimi

Bu bölümde, aşağıdaki dört istemci yönetimi çözümü karşılaştırılır:

- [Configuration Manager istemcisi](#bkmk_sccm)
- [Configuration Manager ile şirket içi mobil cihaz yönetimi (MDM)](#bkmk_opmdm)
- [Microsoft Intune ile ortak yönetim](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

Bu çözümleri kendileriyle veya birbirleriyle birlikte kullanabilirsiniz. Örneğin, kuruluşunuzdaki bilgisayarları ve sunucuları yönetmek için istemci tabanlı yönetim yaklaşımını kullanın ve ayrıca internet tabanlı dizüstü bilgisayarları yönetmek için ortak yönetimi kullanın. Bu şekilde yaklaşımları birleştirerek, tüm cihaz yönetimi ihtiyaçlarınızı ele alabilirsiniz.  

Aşağıdaki etkenlere göre yönetim çözümlerini karşılaştıran iki tablo da vardır:

- [Desteklenen platformlarla karşılaştırın](#bkmk_comp1)
- [Yönetim işlevselliğine göre karşılaştırın](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> Configuration Manager istemcisi  

Bu seçenek, cihazlarda Configuration Manager istemcisinin yüklenmesini gerektirir. Ortamınızdaki bilgisayarları, sunucuları ve diğer cihazları yönetmeye yönelik en fazla özelliği sağlar.

Daha fazla bilgi için bkz. [istemci yükleme yöntemleri](../clients/deploy/plan/client-installation-methods.md).  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Şirket içi MDM  

Bu seçenek, Windows 10 ' da yerleşik olarak bulunan cihaz yönetimi özelliklerini kullanır. İstemci tabanlı yönetim olarak tam özellikli olmadığı sürece, şirket içi MDM, yönetime daha hafif bir dokunma yaklaşımı sağlar. Cihazları yönetmek için şirket içi Configuration Manager kaynaklarını kullanır.  

Daha fazla bilgi için bkz. [Şirket içi altyapıyla mobil cihazları yönetme](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a> Microsoft Intune ile ortak yönetim

Ortak yönetim, mevcut Configuration Manager dağıtımınızı Microsoft 365 buluta eklemenin birincil yöntemlerinden biridir. Hem Configuration Manager hem de Microsoft Intune kullanarak Windows 10 cihazlarını eşzamanlı olarak yönetmenizi sağlar. Ortak yönetim, yeni işlevler ekleyerek mevcut yatırımlarınızı bulutta Configuration Manager.

Daha fazla bilgi için bkz. [ortak yönetim nedir?](../../comanage/overview.md).  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Microsoft Exchange  

Bu seçenek, birden çok Exchange sunucusunu Configuration Manager 'e bağlamak için Exchange Server bağlayıcısını kullanır. Exchange ActiveSync 'e bağlanabilecek cihazların yönetimini merkezileştirir. Exchange mobil cihaz yönetimi özelliklerini Configuration Manager konsolundan yapılandırabilirsiniz. Örnek özellikler, uzak cihaz temizleme ve birden çok Exchange sunucusu için ayarlar denetimini içerir.

Daha fazla bilgi için bkz. [Configuration Manager ve Exchange ile mobil cihazları yönetme](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> Çözümleri desteklenen platformlar ile karşılaştırın  

|Platform|Configuration Manager istemcisi|Şirket içi MDM|Exchange ile Configuration Manager| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Evet| Evet |
|iOS| | |Evet| Evet |
|Mac OS X|Evet| |Evet| Evet |
|Windows 10|Evet|Evet|Evet| Evet |
|Windows 10 Mobile| |Evet|Evet| Evet |
|Windows (önceki sürümler)|Evet| |Evet|  |
|Windows Server|Evet| |Evet|  |
|Windows Embedded|Evet| | |  |

Desteklenen platformların tüm listesi için aşağıdaki makalelere bakın:

- [Configuration Manager için istemciler ve cihazlar için desteklenen işletim sistemleri](configs/supported-operating-systems-for-clients-and-devices.md)
- [Intune tarafından desteklenen konfigürasyonlar](/intune/supported-devices-browsers)

Microsoft, Android, iOS ve Windows 10 mobil cihazlarını yönetmek için Intune 'un kullanılmasını önerir. Daha fazla bilgi için bkz. [Microsoft Intune nedir?](/intune/what-is-intune).

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a> Yönetim işlevselliğine göre çözümleri karşılaştırın  

|Yönetim işlevi|Configuration Manager istemcisi|Şirket içi MDM|Exchange ile Configuration Manager|  
|--------|----------------------------|---------------|-----------------------------------|  
|Sertifika tabanlı karşılıklı kimlik doğrulaması|Evet|Evet| |
|İstemci yüklemesi|Evet| | |
|Internet üzerinden destek|Evet| | |
|Bulma|Evet| |Evet|
|Donanım envanteri|Evet|Evet|Evet|
|Yazılım envanteri|Evet| |Evet|
|Ayarlar|Evet|Evet|Evet|
|Yazılım dağıtımı|Evet|Evet| |
|Yazılım güncelleştirme yönetimi|Evet| | |
|İşletim sistemi dağıtımı|Evet| | |
|Configuration Manager engelle|Evet|Evet| |
|Exchange Server 'dan karantina ve engelleme (ve Configuration Manager)| | |Evet|
|Uzaktan temizleme| |Evet|Evet|