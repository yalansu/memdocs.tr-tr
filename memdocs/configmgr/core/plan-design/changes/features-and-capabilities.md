---
title: Özellikler ve yetenekler
titleSuffix: Configuration Manager
description: Configuration Manager 'ın birincil yönetim özellikleri hakkında bilgi edinin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 74b150b5a2157104b6a380489202fd309224a3bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129044"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Configuration Manager özellikleri ve yetenekleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makalede Configuration Manager birincil yönetim özellikleri özetlenmektedir. Her özelliğin kendi önkoşulları vardır ve bunların nasıl kullanılacağı Configuration Manager hiyerarşinizin tasarımını ve uygulamasını etkileyebilir. Örneğin, hiyerarşinizdeki cihazlara yazılım güncelleştirmeleri dağıtmak istiyorsanız, yazılım güncelleştirme noktası site sistem rolüne sahip olmanız gerekir.  

Ortamınızda bu yönetim yeteneklerini desteklemek üzere Configuration Manager nasıl planlanacağı ve yükleneceği hakkında daha fazla bilgi için bkz. [Configuration Manager için hazırlanma](../get-ready.md).  

## <a name="co-management"></a>Ortak yönetim

Ortak yönetim, mevcut Configuration Manager dağıtımınızı Microsoft 365 buluta eklemenin birincil yöntemlerinden biridir. Hem Configuration Manager hem de Microsoft Intune kullanarak Windows 10 cihazlarını eşzamanlı olarak yönetmenizi sağlar. Ortak yönetim, koşullu erişim gibi yeni işlevler ekleyerek mevcut yatırımlarınızı bulutta Configuration Manager. Daha fazla bilgi için bkz. [ortak yönetim](../../../comanage/overview.md)nedir?

## <a name="desktop-analytics"></a>Desktop Analytics

Masaüstü analizi, Configuration Manager ile tümleşen bulut tabanlı bir hizmettir. Hizmet, Windows istemcilerinizin güncelleştirme hazırlığı hakkında daha bilinçli kararlar almanıza yardımcı olmak için Öngörüler ve zeka sağlar. Microsoft bulut hizmetlerine bağlı milyonlarca cihazdan toplanan verilerle kuruluşunuzdaki verileri birleştirir. Daha fazla bilgi için bkz. [Masaüstü Analizi](../../../desktop-analytics/overview.md)nedir?

## <a name="cloud-attached-management"></a>Buluta bağlı yönetim

Bulut yönetimi ağ geçidi, bulut tabanlı dağıtım noktaları ve Azure Active Directory gibi özellikleri kullanarak internet tabanlı istemcileri yönetin.

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [İnternetteki istemcileri yönetme](../../clients/manage/manage-clients-internet.md)
- [Azure AD planlaması](../security/plan-for-security.md#bkmk_planazuread)
- [Azure hizmetleri](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>Gerçek zamanlı yönetim

Çevrimiçi cihazları hemen sorgulamak için CMPivot kullanın, daha derin Öngörüler için verileri filtreleyin ve gruplandırın. Ayrıca, Windows PowerShell betiklerini yönetmek ve istemcilere dağıtmak için Configuration Manager konsolunu kullanın. Daha fazla bilgi için bkz. [CMPivot](../../servers/manage/cmpivot.md) ve [PowerShell betikleri oluşturma ve çalıştırma](../../../apps/deploy-use/create-deploy-scripts.md).

## <a name="application-management"></a>Uygulama yönetimi

Yönettiğiniz farklı cihazlarda uygulamalar oluşturmanıza, yönetmenize, dağıtmanıza ve izlemenize yardımcı olur. Configuration Manager konsolundan Microsoft 365 uygulamalarını dağıtın, güncelleştirin ve yönetin. Ayrıca, bulut tabanlı uygulamalar sunmak için Iş ve eğitimin Microsoft Store Configuration Manager tümleştirilir. Daha fazla bilgi için bkz. [uygulama yönetimine giriş](../../../apps/understand/introduction-to-application-management.md).

## <a name="os-deployment"></a>İşletim sistemi dağıtımı

Windows 10 ' un yerinde yükseltmesini dağıtın veya işletim sistemi görüntülerini yakalayın ve dağıtın. Görüntü dağıtımı PXE, çok noktaya yayın veya önyüklenebilir medya kullanabilir. Ayrıca, Windows AutoPilot kullanarak mevcut cihazların yeniden dağıtılmasına da yardımcı olabilir. Daha fazla bilgi için bkz. [OS dağıtımına giriş](../../../osd/understand/introduction-to-operating-system-deployment.md).  

## <a name="software-updates"></a>Yazılım güncelleştirmeleri

Kuruluştaki yazılım güncelleştirmelerini yönetin, dağıtın ve izleyin. Ağ kullanımını denetlemeye yardımcı olması için Windows teslim Iyileştirme ve diğer eş önbelleğe alma teknolojileriyle tümleştirin. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerine giriş](../../../sum/understand/software-updates-introduction.md).  

## <a name="company-resource-access"></a>Şirket kaynak erişimi

Kuruluşunuzdaki kullanıcılara uzak konumlardan veri ve uygulamalara erişim izni vermenizi sağlar. Bu özellik Wi-Fi, VPN, e-posta ve sertifika profilleri içerir. Daha fazla bilgi için bkz. [veri ve site altyapısını koruma](../../../protect/understand/protect-data-and-site-infrastructure.md).

## <a name="compliance-settings"></a>Uyumluluk ayarları

Kuruluştaki istemci cihazların yapılandırma uyumluluğunu değerlendirmenize, izlemenize ve düzeltmenize yardımcı olur. Ayrıca, yönettiğiniz cihazlarda bir dizi özelliği ve güvenlik ayarını yapılandırmak için uyumluluk ayarlarını kullanabilirsiniz. Daha fazla bilgi için bkz. [Cihaz uyumluluğunu doğrulayın](../../../compliance/understand/ensure-device-compliance.md).  

## <a name="endpoint-protection"></a>Uç Nokta Koruma

Kuruluşunuzdaki bilgisayarlar için güvenlik, kötü amaçlı yazılımdan koruma ve Windows Güvenlik Duvarı yönetimi sağlar. Bu alan, aşağıdaki Windows Defender paketi özellikleriyle yönetimi ve tümleştirmeyi içerir:

- Windows Defender Virüsten Koruma
- Microsoft Defender Gelişmiş Tehdit Koruması
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Windows Defender Uygulama Denetimi
- Windows Defender Güvenlik Duvarı

Daha fazla bilgi için bkz. [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

## <a name="inventory"></a>Envanter

Varlıkları tanımanıza ve izlemenize yardımcı olur.

### <a name="hardware-inventory"></a>Donanım envanteri

Kuruluşunuzdaki cihazların donanımıyla ilgili ayrıntılı bilgi toplar. Daha fazla bilgi için bkz. [Donanım envanterine giriş](../../clients/manage/inventory/introduction-to-hardware-inventory.md).  

### <a name="software-inventory"></a>Yazılım envanteri

Kuruluşunuzdaki istemci bilgisayarlarda depolanan dosyalarla ilgili bilgileri toplar ve raporlar. Daha fazla bilgi için bkz. [yazılım envanterine giriş](../../clients/manage/inventory/introduction-to-software-inventory.md).  

### <a name="asset-intelligence"></a>Varlık Yönetim Bilgileri

, Kuruluşunuzda envanter verilerini toplamak ve yazılım lisansı kullanımını izlemek için araçlar sağlar. Daha fazla bilgi için bkz. [varlık yönetim bilgileri giriş](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

## <a name="on-premises-mobile-device-management"></a>Şirket içi mobil cihaz yönetimi

Cihaz platformlarında yerleşik olarak bulunan yönetim işlevselliğiyle şirket içi Configuration Manager altyapısını kullanarak cihazları kaydeder ve yönetir. (Tipik yönetim, ayrı olarak yüklü bir Configuration Manager istemcisi kullanır.) Bu özellik şu anda Windows 10 Enterprise ve Windows 10 Mobile cihazlarının yönetilmesini desteklemektedir. Daha fazla bilgi için bkz. [Şirket içi altyapıyla mobil cihazları yönetme](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="power-management"></a>Güç yönetimi

Kuruluştaki istemci bilgisayarların güç tüketimini yönetin ve izleyin. Güç planlarını yapılandırın ve iş saatleri dışında bakım yapmak için LAN 'da uyandırma 'yı kullanın. Daha fazla bilgi için bkz. [güç yönetimine giriş](../../clients/manage/power/introduction-to-power-management.md).  

## <a name="remote-control"></a>Uzaktan denetim

İstemci bilgisayarlarını Configuration Manager konsolundan uzaktan yönetmek için araçlar sağlar. Daha fazla bilgi için bkz. [uzaktan denetime giriş](../../clients/manage/remote-control/introduction-to-remote-control.md).  

## <a name="reporting"></a>Raporlama

Configuration Manager konsolundan SQL Server Reporting Services gelişmiş raporlama yeteneklerini kullanın. Bu özellik yüzlerce varsayılan rapor sağlar. Daha fazla bilgi için bkz. [raporlamaya giriş](../../servers/manage/introduction-to-reporting.md).  

## <a name="software-metering"></a>Yazılım kullanım ölçümü

Configuration Manager istemcilerinden yazılım kullanım verilerini izleyin ve toplayın. Bu verileri, yazılımın yüklendikten sonra kullanılıp kullanılmayacağını anlamak için kullanabilirsiniz. Daha fazla bilgi için bkz. [yazılım kullanım ölçümü ile uygulama kullanımını izleme](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  
