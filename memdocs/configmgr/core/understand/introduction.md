---
title: Configuration Manager nedir?
titleSuffix: Configuration Manager
description: Microsoft uç nokta Configuration Manager temellerini öğrenin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99e02c190e02a5e017fe2c3f41682ad1624b6051
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699356"
---
# <a name="what-is-configuration-manager"></a>Configuration Manager nedir?

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Sürüm 1910 ' den başlayarak Configuration Manager artık Microsoft Endpoint Manager 'ın bir parçasıdır.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Uç Nokta Yöneticisi, tüm cihazlarınızı yönetmek için tümleşik bir çözümdür. Microsoft, karmaşık bir geçiş olmadan ve Basitleştirilmiş lisanslama ile Configuration Manager ve Intune 'u birlikte sunar. Mevcut Configuration Manager yatırımlarınızdan yararlanmaya devam edin, Microsoft bulutun gücünden kendi hızınızda yararlanın.

Aşağıdaki Microsoft yönetim çözümleri artık **Microsoft Endpoint Manager** markasının bir parçasıdır:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Otomatik Pilot](/intune/enrollment/enrollment-autopilot)
- [Cihaz yönetimi yönetici konsolundaki](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760) diğer özellikler

Daha fazla bilgi için bkz. [Microsoft uç nokta CONFIGURATION Manager SSS](microsoft-endpoint-manager-faq.md).

## <a name="introduction"></a>Giriş

Aşağıdaki sistem yönetimi etkinliklerine yardımcı olması için Configuration Manager kullanın:

- El ile gerçekleştirilen görevleri azaltarak ve yüksek değerli projelere odaklanmanızı sağlayarak BT üretkenliğini ve verimliliği artırın.  
- Donanım ve yazılım yatırımlarını en üst düzeye çıkarın.  
- Doğru zamanda doğru yazılımı sağlayarak kullanıcı üretkenliğini güçlendirin.  

Configuration Manager şunları etkinleştirerek daha etkili BT hizmetleri sunmanıza yardımcı olur:

- Uygulamaların, yazılım güncelleştirmelerinin ve işletim sistemlerinin güvenli ve ölçeklenebilir dağıtımı.
- Yönetilen cihazlarda gerçek zamanlı eylemler.
- Şirket içi ve internet tabanlı cihazlar için bulut destekli analiz ve yönetim.
- Uyumluluk ayarları yönetimi.  
- Sunucuların, masaüstü bilgisayarların ve dizüstü bilgisayarların kapsamlı yönetimi.

Configuration Manager birçok Microsoft teknolojisinden ve çözümünden daha iyi bir şekilde genişletilir. Örneğin, Configuration Manager ile tümleşir:  

- Çok çeşitli mobil cihaz platformlarını ortak yönetmek için Microsoft Intune
- Yönetim hizmetlerinizi genişletmek için Cloud Services 'ı barındırmak Microsoft Azure
- Yazılım güncelleştirmelerini yönetmek için Windows Server Update Services (WSUS)
- Sertifika Hizmetleri
- Exchange Server ve Exchange Online
- Grup İlkesi
- DNS
- Windows otomatik dağıtım seti (Windows ADK) ve Kullanıcı Durumu Taşıma Aracı (USMT)
- Windows Dağıtım Hizmetleri (WDS)
- Uzak Masaüstü ve Uzaktan Yardım

Configuration Manager de şunları kullanır:  

- Güvenlik, hizmet konumu, yapılandırma ve yönetmek istediğiniz kullanıcı ve cihazları öğrenmek için Active Directory Domain Services ve Azure Active Directory.  
- Dağıtılmış değişiklik yönetim veritabanı olarak Microsoft SQL Server ve yönetim etkinliklerini izlemek ve izlemek için raporlar oluşturmak üzere SQL Server Reporting Services (SSRS) ile tümleşir.  
- Yönetim işlevselliğini genişleten ve Internet Information Services (IIS) Web hizmetlerini kullanan site sistemi rolleri.
- Dağıtım Iyileştirmesi, Windows düşük ekstra gecikmeli arka plan taşıma (LEDBAT), Arka Plan Akıllı Aktarım Hizmeti (BITS), BranchCache ve diğer eş önbelleğe alma teknolojileri, ağlarınızdaki ve cihazlar arasındaki içeriği yönetmeye yardımcı olur.

Bir üretim ortamındaki Configuration Manager başarılı olmak için yönetim özelliklerini kapsamlı bir şekilde planlayın ve test edin. Configuration Manager, kuruluşunuzdaki her bilgisayarı etkilemek için güçlü bir yönetim uygulamasıdır. Configuration Manager Configuration Manager, iş gereksinimlerinizi dikkatli bir planlama ve göz önünde bulundurarak dağıtıp yönettiğinizde, yönetim yükünüzü ve toplam sahip olma maliyetinizi azaltabilir.  

## <a name="user-interfaces"></a>Kullanıcı arabirimleri

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> Configuration Manager konsolu

Configuration Manager yükledikten sonra, siteleri ve istemcileri yapılandırmak ve yönetim görevlerini çalıştırmak ve izlemek için Configuration Manager konsolunu kullanın. Bu konsol ana yönetim noktasıdır ve birden fazla siteyi yönetmenize olanak sağlar.  

Configuration Manager konsolunu ek bilgisayarlara yükleyebilir ve Configuration Manager rol tabanlı yönetimi kullanarak erişimi kısıtlayabilir ve yönetici kullanıcıların konsolunda görebileceklerini sınırlayabilirsiniz.  

Daha fazla bilgi için bkz. [Configuration Manager konsolunu kullanma](../servers/manage/admin-console.md).

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a> Yazılım Merkezi

**Yazılım Merkezi** , Configuration Manager Istemcisini bir Windows cihazına yüklediğinizde yüklenen bir uygulamadır. Kullanıcılar, dağıttığınız yazılımı istemek ve yüklemek için yazılım merkezi 'ni kullanır. Software Center, kullanıcıların aşağıdaki işlemleri yapmanızı sağlar:  

- Uygulamaları, yazılım güncelleştirmelerini ve yeni işletim sistemi sürümlerini inceleyin ve bunları yükler
- Yazılım isteği geçmişini görüntüle
- Kuruluşunuzun ilkelerine karşı cihaz uyumluluğunu görüntüleme

Ayrıca, ek iş gereksinimlerini karşılamak için yazılım merkezi 'nde özel sekmeler de gösterebilirsiniz.

Daha fazla bilgi için bkz. [Yazılım Merkezi Kullanıcı Kılavuzu](software-center.md).

## <a name="next-steps"></a>Sonraki adımlar

Configuration Manager yüklemeden önce temel kavramları ve koşulları öğrenmeye çalışın:

- System Center 2012 Configuration Manager hakkında bilgi sahibiyseniz, bkz. [System center 2012 ' den nelerin değiştirilme Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- Configuration Manager yüksek düzeyde teknik bir genel bakış için bkz. [Configuration Manager Temelleri](fundamentals.md).

Temel kavramlara alışdığınızda, Configuration Manager başarıyla dağıtmanıza ve kullanmanıza yardımcı olması için bu belge kitaplığını kullanın. Aşağıdaki makalelerle başlayın:

- [Configuration Manager özellikleri ve yetenekleri](../plan-design/changes/features-and-capabilities.md)  
- [Cihaz yönetim çözümü seçme](../plan-design/choose-a-device-management-solution.md)  
- [Kendi laboratuvar ortamınızı oluşturarak Configuration Manager değerlendirin](../get-started/set-up-your-lab.md)
- [Configuration Manager kullanmaya yönelik yardım bulun](find-help.md)