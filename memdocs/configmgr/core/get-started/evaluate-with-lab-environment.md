---
title: Laboratuvar ortamında değerlendirme
titleSuffix: Configuration Manager
description: Kuruluşunuzda kullanılmak üzere Configuration Manager değerlendirmek için bir laboratuar ortamı oluşturun.
ms.date: 02/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db59ad55c52f8d937b23704af310dc8879fe8a6d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692885"
---
# <a name="evaluate-configuration-manager-by-building-your-own-lab-environment"></a>Kendi laboratuvar ortamınızı oluşturarak Configuration Manager değerlendirin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Kuruluşunuzda kullanılmak üzere Configuration Manager değerlendirmek için laboratuvar ortamı oluşturmayı öğrenin.  

 Configuration Manager, kullanıcılarınızı, cihazlarınızı ve yazılımınızı yönetmek için karmaşık ve güçlü bir araçtır. Tam dağıtımdan önce Configuration Manager kapsamlı bir şekilde değerlendirmek iyi bir fikirdir. böylece, uygulamalı alýþtýrmalar ile kavramsal bir şekilde yararlanabilirsiniz.  

 Bu kılavuz, öncelikle kurumsal ortamlarda Configuration Manager kullanımını değerlendiren Yöneticiler için tasarlanmıştır:  

-   Bir çözümün bilgisayarları, sunucuları ve mobil cihazları tam olarak yönetmesini isteyen yöneticiler  

-   Bulut tabanlı cihaz yönetiminin esnekliğine sahip şirket içi cihaz yönetimi güvenliği gerektiren yüksek güvenlikli sektörlerdeki yöneticiler  

-   Şirket içi sunucu mimarisinin ölçeğini yönetmek isteyen yöneticiler  

## <a name="what-this-lab-does"></a>Bu laboratuvarın amacı  
 Bu laboratuvar ortamını oluşturmanın asıl hedefi, Configuration Manager ile çalışmaya başlamak ve Configuration Manager kavramak için genel bilgi sağlamaktır. İki sunucu kullanarak geçerli Configuration Manager sürümünün ayrıntılı bir derlemesini adım adım inceleyeceğiz:  

-   Active Directory, etki alanı denetleyicisi ve DNS sunucusu barındıran bir bilgisayar  

-   Configuration Manager ve ilişkili tüm SQL Server bileşenlerini barındıran bir  

İstemci Makineler Hyper-V içine yüklenir. Laboratuvar ayrıca tek bir sunucu üzerinde tamamen sanallaştırılmış bir sistem olarak çalıştırılabilir.  

## <a name="what-this-lab-does-not-do"></a>Bu laboratuvar ne sağlamaz  
 Bu laboratuvar size tüm Configuration Manager senaryolarından geçmeyecektir. Etkin bir ortama hemen geçirilecek şekilde tasarlanmamıştır.  

 Bu laboratuvarı oluşturduğunuzda çalışabilecek işlevsel bir ortama sahip olacaksınız. Ancak bu ortam sistem performansı, sabit disk alanı yönetimi ve SQL Server depolama gibi faktörlerle iyileştirilmez.  

##  <a name="recommended-reading-before-you-build-the-lab"></a><a name="BKMK_EvalRec"></a> Laboratuvar oluşturmadan önce okumanız önerilir  
 [Configuration Manager belgelerinde](/sccm/)çok sayıda içerik mevcuttur. Laboratuvarı oluşturmaya başlamadan önce bu kitaplıktan aşağıdaki konuları okumanızı öneririz:  

-   [Configuration Manager giriş](../../core/understand/introduction.md)bölümünde Configuration Manager konsolu, Son Kullanıcı portalları ve örnek senaryolar hakkında temel kavramlar öğrenin.  

-   [Configuration Manager Özellikler ve](../../core/plan-design/changes/features-and-capabilities.md)özellikleri içindeki Configuration Manager birincil yönetim özellikleri hakkında bilgi edinin.  

-   [Configuration Manager Temelleri](../../core/understand/fundamentals.md)hakkında bilgi sahibi olmanız.  

-   [Configuration Manager için rol tabanlı yönetimin temelleri](../../core/understand/fundamentals-of-role-based-administration.md)ile güvenlik rollerinin önemini öğrenin.  

-   İçerik [yönetimi kavramlarıyla](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)ilgili içerik yönetimi hakkında bilgi edinin.  

-   [İstemcilerin Configuration Manager için site kaynaklarını ve hizmetleri nasıl bulduklarını anlamak için](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)dağıtımınızın tamamında günlük görevleri başarıyla desteklemeyi öğrenin.