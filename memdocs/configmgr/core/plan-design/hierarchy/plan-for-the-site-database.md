---
title: Site veritabanını planlayın
titleSuffix: Configuration Manager
description: Configuration Manager hiyerarşinizi planlarken site veritabanı ve site veritabanı sunucu rolünü göz önünde bulundurun.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 068511c5b3b0c15eb355c484b241a76d9dd512e2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700189"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>Configuration Manager için site veritabanını planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Site veritabanı sunucusu, Microsoft SQL Server desteklenen bir sürümünü çalıştıran bir bilgisayardır. SQL Server, Configuration Manager sitelere ilişkin bilgileri depolamak için kullanılır. Bir Configuration Manager hiyerarşisindeki her site, site veritabanı sunucusu rolü atanmış bir site veritabanı ve bir sunucu içerir.  

-   Merkezi yönetim siteleri ve birincil siteler için site sunucusuna SQL Server yükleyebilir veya SQL Server site sunucusu dışında bir bilgisayara yükleyebilirsiniz.  

-   İkincil siteler için tam SQL Server yüklemesi yerine SQL Server Express kullanabilirsiniz. Ancak, veritabanı sunucusunun ikincil site sunucusunda çalıştırılması gerekir.  

-  SQL kullanılabilirlik grubu kullanımı için veritabanı kurtarma modelinin tam olarak ayarlanması gerekir  

-  SQL olmayan kullanılabilirlik grubu kullanımı için veritabanı kurtarma modelinin basıt olarak ayarlanması gerekir  

SQL kurtarma modları hakkında daha fazla bilgi, [Kurtarma modellerinde (SQL Server)](/sql/relational-databases/backup-restore/recovery-models-sql-server)bulunabilir.

Aşağıdaki SQL Server yapılandırmaları site veritabanını barındırmak için kullanılabilir:  

-   Varsayılan SQL Server örneği  

-   SQL Server çalıştıran tek bilgisayarda adlandırılmış bir örnek  

-   SQL Server'ın kümelenmiş örneğinde adlandırılmış bir örnek  

-   SQL Server bir AlwaysOn kullanılabilirlik grubu (Configuration Manager sürüm 1602 ' den başlayarak)


Site veritabanını barındırmak için SQL Server, [Configuration Manager SQL Server sürümleri Için destek](../../../core/plan-design/configs/support-for-sql-server-versions.md)bölümünde açıklanan gereksinimlere uymalıdır.  



## <a name="remote-database-server-location-considerations"></a>Uzak veritabanı sunucu konumu konuları  

Uzak bir veritabanı sunucu bilgisayarı kullanıyorsanız, aradaki ağ bağlantısının yüksek kullanılabilirliğe sahip ve yüksek bant genişliğine sahip bir ağ bağlantısı olduğundan emin olun. Site sunucusu ve bazı site sistem rolleri, site veritabanını barındıran uzak sunucuyla sürekli iletişim kurmalıdır.

-   Veritabanı sunucusuyla iletişim için gereken bant genişliği miktarı, birçok farklı site ve istemci yapılandırmasının birleşimine bağlıdır. Bu nedenle, gereken gerçek bant genişliği yeterince tahmin edilemez.  

-   SMS Sağlayıcısı çalıştıran ve site veritabanına bağlanan her bilgisayar ağ bant genişliği gereksinimlerini artırır.  

-   SQL Server çalıştıran bilgisayar, site sunucusuyla ve SMS Sağlayıcısı çalıştıran tüm bilgisayarlarla iki yönlü güvene sahip bir etki alanında bulunmalıdır.  

-   Site veritabanı ile site sunucusu birlikte konumlandırıldığında site veritabanı sunucusu için kümelenmiş bir SQL Server kullanamazsınız.  


Genellikle, bir site sistemi sunucusu yalnızca tek bir Configuration Manager sitesinden site sistem rollerini destekler. Ancak, farklı Configuration Manager sitelerinden bir veritabanını barındırmak için SQL Server çalıştıran kümelenmiş veya kümelenmemiş sunucularda SQL Server farklı örneklerini kullanabilirsiniz. Farklı sitelerden veritabanlarını desteklemek için her bir SQL Server örneğini benzersiz iletişim bağlantı noktaları kullanacak şekilde yapılandırmanız gerekir.