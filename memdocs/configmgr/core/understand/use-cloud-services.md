---
title: Bulut hizmetlerini kullanma
titleSuffix: Configuration Manager
description: Şirket içi altyapınızı tamamlamak için Configuration Manager bulut kaynakları sağlayın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5ea198f944cf44909e54e123889a3f0f29b1db5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699118"
---
# <a name="use-cloud-services-with-configuration-manager"></a>Bulut hizmetlerini Configuration Manager ile birlikte kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager bulut tabanlı birçok seçeneği destekler. Bunlar şirket içi altyapınızı tamamlayabilir ve aşağıdaki gibi iş sorunlarını çözmenize yardımcı olabilir:  

-   KCG 'yi yönetme (mobil cihaz yönetimi için Intune 'U kullanarak).  

-   Şirket güvenlik duvarınızın dışında (bulut tabanlı dağıtım noktalarını kullanarak), intranet üzerindeki yalıtılmış istemcilere veya kaynaklara içerik kaynakları sağlama.  

-   Fiziksel donanım kullanılamadığında altyapının ölçeğini genişletme veya gereksinimlerinizi desteklemek için mantıksal olarak yerleştirilme (Microsoft Azure sanal makineler kullanarak).  

Bulut kaynaklarının sağlanması Configuration Manager dağıtmadan önce yapmanız gereken bir şey olmasa da, bir hiyerarşi tasarım planında çok uzakta ilermeden önce bu seçenekleri anlamanız yararlı olabilir. Bulut kaynaklarının kullanımı, şirket içi altyapının iş sorunlarını çözirken para ve zaman tasarruf edebilir.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Configuration Manager ile kullanabileceğiniz bulut tabanlı kaynaklar  
 Her seçenek farklı gereksinimlere sahip olduğundan, benzersiz önkoşulları, sınırlamaları ve kullanıma bağlı olası ek giderleri anlamak için her birini daha derinlemesine araştırmanız önerilir.  

-   Bulut tabanlı dağıtım noktaları hakkında bilgi için bkz. [bulut tabanlı dağıtım noktalarını Install](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).

-   Azure hakkında daha fazla bilgi için bkz. [Azure nedir?](https://azure.microsoft.com/overview/what-is-azure/)

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Azure sanal makineleri (bulut tabanlı altyapı için)  
 Configuration Manager, Azure 'daki sanal makinelerde çalışan bilgisayarların, fiziksel kurumsal ağınızda şirket içinde çalıştığı şekilde kullanılmasını destekler. Azure sanal makinelerini aşağıdaki senaryolarda kullanabilirsiniz:  

-   **Senaryo 1:** Configuration Manager bir sanal makinede çalıştırabilir ve diğer sanal makinelerde yüklü istemcileri yönetmek için kullanabilirsiniz.  

-   **Senaryo 2:** Configuration Manager bir sanal makinede çalıştırabilir ve Azure 'da çalıştırmayan istemcileri yönetmek için kullanabilirsiniz.  

-   **Senaryo 3:** Fiziksel şirket ağınızda diğer rolleri çalıştırırken (iletişimler için uygun ağ bağlantısı ile), sanal makinelerde farklı Configuration Manager site sistem rolleri çalıştırabilirsiniz.  

Fiziksel kurumsal ağınıza Configuration Manager yüklemek için uygulanan ağ, işletim sistemi ve donanım gereksinimleri için aynı gereksinimler, Azure 'daki Configuration Manager yüklemesi için de geçerlidir.  

Azure sanal makinelerini kullanmak için bir Azure aboneliği gereklidir. Kullandığınız sanal makine sayısına, bunların yapılandırmasına ve bulut tabanlı kaynakların kullanımına göre ücretlendirilirsiniz.  

Ayrıca, Azure sanal makinelerinde çalışan Configuration Manager siteleri ve istemcileri, şirket içi yüklemelerle aynı lisans gereksinimlerine tabidir.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Azure Hizmetleri (bulut tabanlı dağıtım noktaları için)  
 Bulut tabanlı bir dağıtım noktası olarak adlandırılan Configuration Manager dağıtım noktasını barındırmak için bir Azure hizmeti kullanabilirsiniz. Şirket içi dağıtım noktaları ve Azure sanal makinelerinde dağıtılan dağıtım noktaları [ile birlikte Configuration Manager ile bulut tabanlı bir dağıtım noktası kullanabilirsiniz](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) .  

 Bu, üzerinde site sistem rolü dağıttığınız bir Azure sanal makinesini kullanmaktan farklıdır. Bulut tabanlı dağıtım noktaları:  

-   Bir sanal makinede değil, Azure 'da hizmet olarak çalıştırın.  

-   İstemcilerden gelen içerik isteklerini karşılamak için otomatik olarak ölçeklendirin.  

-   Internet ve intranet 'teki istemcileri destekler.  

Dağıtım noktalarını barındırmak için Azure 'un kullanılması için Azure aboneliği gereklidir. Ücretlere veya hizmetten aktarılan veri miktarına göre ücretlendirilirsiniz.  

### <a name="additional-configuration-manager-capabilities"></a>Ek Configuration Manager özellikleri  
 Bazı Configuration Manager özellikleri bulut tabanlı hizmetlere bağlanarak şöyle olabilir:  

-   Windows Server Update Services (WSUS).  

-   Configuration Manager güncelleştirmelerini indirmek için Configuration Manager hizmeti bulutu.  

Bu ek yetenekler için bir Azure aboneliğinizin olması gerekmez. Bulutta belirli bağlantılar, sertifikalar veya hizmetler ayarlamanıza gerek yoktur. Bunun yerine, sizin için Configuration Manager tarafından otomatik olarak yönetilir. Tüm yapmanız gereken, ilgili site sistemlerinin ve cihazların Internet tabanlı URL 'Lere erişebildiğinden emin olmanızı sağlar.  

##  <a name="security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a> Bulut tabanlı hizmetler için güvenlik  
 Configuration Manager Azure 'da içeriğinizi sağlamak ve bu içeriklerinize erişmek ve kullandığınız hizmetleri yönetmek için sertifikaları kullanır. Configuration Manager, Azure 'da depoladığınız verileri şifreler, ancak Azure 'un sağladıkları dışında ek güvenlik veya veri denetimleri sunmaz.  

 Daha fazla bilgi için, bulut tabanlı farklı kaynak senaryolarının ayrıntılarına bakın. Ayrıca bkz. [Azure Güvenlik 'e giriş](/azure/security/fundamentals/overview).