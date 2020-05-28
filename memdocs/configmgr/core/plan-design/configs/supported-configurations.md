---
title: Desteklenen yapılandırmalar
titleSuffix: Configuration Manager
description: İşlevsel Configuration Manager dağıtımı planlayabilmeniz, dağıtmanız ve koruyabilmeniz için anahtar yapılandırma ve gereksinimleri belirler.
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66770ea14c3ae53bad8e6df61b54c7c5e2d2aaa0
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904568"
---
# <a name="supported-configurations-for-configuration-manager"></a>Configuration Manager için desteklenen yapılandırmalar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Şirket içi bir çözüm olarak, Configuration Manager sunucularınızın, istemcilerinizin, ağ yapılandırmalarından ve Microsoft Intune, SQL Server ve Azure gibi ek ürünlerden yararlanmasına olanak sağlar.

Bu ve aşağıdaki konularda yer alan bilgiler temel yapılandırma, gereksinimler ve sınırlamaları tanımlamanızı sağlamak için önemlidir. böylece işlevsel Configuration Manager dağıtımı planlayabilir, dağıtabilir ve koruyabilirsiniz.  Bu bilgiler Configuration Manager siteleri, hiyerarşileri ve yönetilen cihazlar için altyapıya özgüdür.

Bir Configuration Manager özelliği veya özelliği daha belirli yapılandırmalar gerektirdiğinde, bu bilgiler özelliğe özgü belgelere dahil edilir ve daha genel yapılandırma ayrıntılarına ek olarak sunulur.  

 Aşağıdaki konularda açıklanan ürün ve teknolojiler Configuration Manager tarafından desteklenir. Ancak, bu içeriğe dahil edilmesi, ürünün bireysel destek yaşam döngüsünün ötesinde herhangi bir ürünün destek uzantısını göstermez. Destek yaşam döngüsünün ötesinde ürünlerin, [genişletilmiş güvenlik güncelleştirmeleri (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) programı kapsamında yer alan ürünler dahil olmak üzere Configuration Manager ile kullanılması desteklenmez. Microsoft Destek Yaşam Döngüleri hakkında daha fazla bilgi için [Microsoft Destek Yaşam Döngüleri](https://support.microsoft.com/lifecycle) web sitesini ziyaret edin. Configuration Manager 'de genişletilmiş güvenlik güncelleştirmeleri hakkında daha fazla bilgi için, bkz. [istemciler ve cihazlar Için desteklenen işletim sistemi sürümleri Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

> [!NOTE]  
>  Microsoft destek yaşam döngüsü ilkesi hakkında daha fazla bilgi için, [Microsoft desteği yaşam döngüsü ILKESI SSS](https://support.microsoft.com/lifecycle)adresindeki Microsoft desteği yaşam döngüsü destek ilkesi SSS Web sitesine gidin.  

 Ayrıca, aşağıdaki konularda listelenmeyen ürünler ve ürün sürümleri, [Enterprise Mobility and Security bloglarında](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity)duyurulmadığı müddetçe Configuration Manager desteklenmez.  Her zaman, bu blogdaki içerik bu belge gövdesinde bir güncelleştirmeden önce gelir.


-  [Boyut ve ölçek sayıları](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Configuration Manager için farklı hiyerarşi tasarımlarında kaç site, site sistem rolü ve istemci ya da cihaz için desteklendiği hakkında bilgi edinin.

-  [Site ve site sistemi önkoşulları](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Farklı site türlerini ve site sistem rollerini desteklemek için Windows Server 'da gerekli olan yapılandırma hakkında bilgi edinin.

-  [Site sistem sunucuları için desteklenen işletim sistemleri](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Site sunucusu veya site sistem sunucusu olarak kullanabileceğiniz işletim sistemleri hakkında bilgi edinin.

-  [İstemciler ve cihazlar için desteklenen işletim sistemleri](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Windows, Windows Embedded, Linux ve UNIX, Mac ve mobil cihazlar dahil olmak üzere Configuration Manager hangi işletim sistemlerini yönetebileceğinizi öğrenin.

-  [Konsol için desteklenen işletim sistemleri](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Dağıtımınızı yönetmek için bir erişim noktası sağlamak üzere Configuration Manager konsolunu barındırabilen işletim sistemleri hakkında bilgi edinin.  

-  [SQL Server sürümleri desteği](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Hangi SQL Server sürümlerinin site veritabanını ve raporlama veritabanını barındırabileceği ve gereken yapılandırma ve isteğe bağlı yapılandırmaların yanı sıra kullanabileceğiniz hakkında bilgi edinin.

-  [Yüksek kullanılabilirlik seçenekleri](../../servers/deploy/configure/high-availability-options.md)  
Ortamınızı tasarlarken uygulayabileceğiniz seçenekler hakkında bilgi edinmek için, Configuration Manager dağıtımınız için yüksek düzeyde kullanılabilir bir hizmetin sağlanmasına yardımcı olun.

-  [Önerilen donanım](../../../core/plan-design/configs/recommended-hardware.md)  
Configuration Manager sitelerinizi ve anahtar hizmetlerinizi barındırmak için doğru donanım ve yapılandırmaların tanımlanmasına yardımcı olabilecek yönergeler hakkında bilgi edinin.

-  [Active Directory etki alanları için destek](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Configuration Manager gerektirdiği ve desteklediği desteklenen Active Directory etki alanı yapılandırması hakkında bilgi edinin.

-  [Windows özellikleri ve ağları için destek](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Desteklenen Windows teknolojileri (BranchCache ve yinelenen verileri kaldırma gibi) ve Configuration Manager kullanımı için sınırlamalar hakkında bilgi edinin.

-  [Sanallaştırma ortamları desteği](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Desteklenen sanal makine teknolojilerinin nasıl kullanılacağı hakkında daha fazla bilgi edinin.
