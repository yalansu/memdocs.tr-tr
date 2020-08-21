---
title: Hibrit MDM’ye ne oldu?
titleSuffix: Configuration Manager
description: Configuration Manager ' de karma mobil cihaz yönetimi (MDM) kullanımdan kaldırılması hakkında bilgi edinin
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95ac4160895394eb075589ed18a317923f317b45
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695401"
---
# <a name="what-happened-to-hybrid-mdm"></a>Hibrit MDM’ye ne oldu?

*Uygulama hedefi: Configuration Manager (geçerli dal)*

> [!WARNING]
> Microsoft, 1 Eylül 2019 itibariyle hibrit MDM hizmeti sunumunu kullanımdan kaldırdı. Kalan tüm karma MDM cihazları ilke, uygulama veya güvenlik güncelleştirmeleri almaz.

## <a name="remove-hybrid-mdm"></a>Karma MDM 'yi kaldır

Configuration Manager sitenizde bir Microsoft Intune aboneliği varsa, bunu kaldırmanız gerekir.

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin. **Cloud Services**öğesini genişletin ve **Microsoft Intune Abonelik** düğümünü seçin. Mevcut Intune aboneliğinizi silin.

1. **Microsoft Intune aboneliğini kaldırma sihirbazında**, **Configuration Manager Microsoft Intune aboneliğini kaldırma**seçeneğini belirleyin ve ardından **İleri**' ye tıklayın.

1. Sihirbazı tamamlayın.

## <a name="deprecation-announcement"></a>Kullanımdan kaldırma duyurusu

Özgün kullanımdan kaldırma duyurusu aşağıdaki notta verilmiştir:

> [!NOTE]  
> 14 Ağustos 2018 itibariyle, karma mobil cihaz yönetimi [kullanım dışı bir özelliktir](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). 1902 Intune hizmet sürümünden itibaren, 2019 Şubat sonunda, yeni müşteriler yeni bir karma bağlantı oluşturamaz.
> <!--Intune feature 2683117-->  
> Intune, yılda bir süre önce kullanıma sunulduğundan bu yana, yüzlerce yeni müşteri tarafından istenen ve pazara önde gelen hizmet özelliği ekledi. Artık karma mobil cihaz yönetimi (MDM) ile sunulduğundan çok daha fazla özellik sunmaktadır. Azure 'da Intune, kurumsal taşınabilirlik gereksinimleriniz için daha tümleşik ve kolaylaştırılmış bir yönetim deneyimi sağlar.
>
> Sonuç olarak, çoğu müşteri karma MDM üzerinden Azure 'da Intune 'u seçer. Karma MDM kullanan müşterilerin sayısı, daha fazla müşteri buluta geçtiğinde azalmaya devam eder. Bu nedenle, 1 Eylül 2019 ' de Microsoft hibrit MDM hizmet teklifini devre dışı bırakacaktır.
>
> Bu değişiklik, şirket içi Configuration Manager veya [Windows 10 cihazları için ortak yönetimi](../../comanage/overview.md)etkilemez. Karma MDM kullanıp kullanmayacağınızı bilmiyorsanız, Configuration Manager konsolunun **Yönetim** çalışma alanına gidin, **Cloud Services**' i genişletin ve **Microsoft Intune abonelikler**' i seçin. Ayarlanmış bir Microsoft Intune aboneliğiniz varsa, kiracınız karma MDM için yapılandırılır.
>
> **Bu değişiklik beni nasıl etkileyecek?**
>
> - Microsoft, hibrit MDM kullanımınızı bir sonraki yılda destekleyecek. Özellik, önemli hata düzeltmeleri almaya devam edecektir. Microsoft, iOS 12 ' de kayıt gibi yeni işletim sistemi sürümlerindeki mevcut işlevleri destekleyecektir. Karma MDM için yeni özellik olmayacaktır.  
>
> - Hibrit MDM teklifi 'nin sonundan önce Azure 'da Intune 'a geçiş yaparsanız, Son Kullanıcı etkisi olmamalıdır.  
>
> - 1 Eylül 2019 ' de kalan tüm karma MDM cihazları artık ilke, uygulama veya güvenlik güncelleştirmeleri almaz.  
>
> - Lisanslama aynı kalır. Azure lisanslarında Intune, karma MDM 'ye dahildir.  
>
> - Configuration Manager ' deki şirket içi MDM özelliği kullanım dışı bırakılmıştır. Configuration Manager sürüm 1810 ' den başlayarak, şirket içi MDM 'yi Intune bağlantısı olmadan kullanabilirsiniz. Daha fazla bilgi için bkz. [yeni şirket ıçı MDM dağıtımları Için bir Intune bağlantısı artık gerekli](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm)değildir.
>
> - Configuration Manager Şirket içi koşullu erişim özelliği karma MDM ile de kullanım dışıdır. Configuration Manager istemcisiyle yönetilen cihazlarda koşullu erişim kullanıyorsanız, geçirmeden önce bunların korunduğundan emin olun.
>     1. Azure 'da koşullu erişim ilkeleri ayarlama
>     2. Intune portalında uyumluluk ilkelerini ayarlama
>     3. Karma geçişi tamamlama ve MDM yetkilisini Intune olarak ayarlama
>     4. Ortak yönetimi etkinleştirme
>     5. Uyumluluk ilkeleri ortak yönetim iş yükünü Intune 'a taşıma
>
>     Daha fazla bilgi için bkz. [ortak yönetim Ile koşullu erişim](../../comanage/quickstart-conditional-access.md).
>
> **Bu değişikliğe hazırlanmak için ne yapmam gerek?**
>
> - ConfigMgr konsolundan Azure 'a geçiş için geçişinizi planlamaya başlayın. Microsoft IT dahil pek çok müşteri bu işlemden geçmiş. Daha fazla bilgi için bu [Microsoft örnek olay incelemesi](https://aka.ms/Intune_MSFT)bölümüne bakın.  
>
> - Yardım için kayıt iş ortağınıza veya FastTrack 'e başvurun. [Microsoft 365 Için FastTrack](https://aka.ms/hybrid_fasttrack) , Azure 'DA karma MDM 'den Intune 'a geçişinize yardımcı olabilir.
>
> Daha fazla bilgi için bkz. [Intune destek blog gönderisi](https://aka.ms/hybrid_notification).

## <a name="next-steps"></a>Sonraki adımlar

MDM cihazlarını yönetmeye yönelik desteklenen özellikler hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Microsoft Intune nedir?](/intune/what-is-intune)
- [Şirket içi MDM nedir?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Exchange ile cihaz yönetimi](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)