---
title: Siteler ve hiyerarşilerin temel ilkeleri
titleSuffix: Configuration Manager
description: Configuration Manager siteleri ve hiyerarşileri hakkında temel bilgileri alın.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722819"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>Configuration Manager için sitelerin ve hiyerarşilerin temelleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bir Configuration Manager dağıtımı Active Directory bir etki alanına yüklenmelidir. Bu dağıtımın temeli, bir siteler hiyerarşisi oluşturan bir veya daha fazla Configuration Manager sitesi içerir. Tek bir siteden birden çok siteli bir hiyerarşiye, yüklediğiniz sitelerin türü ve konumu, gerektiğinde dağıtımınızın ölçeğini büyütme (genişletme) ve yönetilen kullanıcı ve cihazlara ana hizmetler verme olanağı sunar.

## <a name="hierarchies-of-sites"></a>Siteler hiyerarşisi
Configuration Manager ilk kez yüklediğinizde, yüklediğiniz ilk Configuration Manager Site hiyerarşinizin kapsamını belirler. İlk Configuration Manager site, kuruluşunuzdaki cihazları ve kullanıcıları yöneteceğiniz temel bir temelidir. Bu ilk site bir merkezi yönetim sitesi ya da tek başına bir birincil site olmalıdır.  

 *Merkezi Yönetim sitesi* büyük ölçekli dağıtımlar için uygundur, merkezi bir yönetim noktası sağlar ve küresel bir ağ altyapısına dağıtılan cihazları destekleme esnekliği sağlar. Bir merkezi yönetim sitesi yükledikten sonra, alt site olarak bir veya daha fazla birincil site yüklemeniz gerekir. Bir merkezi yönetim sitesi, bir birincil sitenin işlevi olan cihazların yönetimini doğrudan desteklemediğinden bu yapılandırma gereklidir. Bir merkezi yönetim sitesi, birden çok alt birincil siteyi destekler. Alt birincil siteler, cihazları doğrudan yönetmek ve yönetilen cihazlarınız farklı coğrafi konumlardayken ağ bant genişliğini denetlemek için kullanılır.  

 *Tek başına birincil site* , daha küçük dağıtımlar için uygundur ve ek siteler yüklemek zorunda kalmadan cihazları yönetmek için kullanılabilir. Tek başına bir birincil site dağıtımınızın boyutunu sınırlayabilse de, yeni bir merkezi yönetim sitesi yükleyerek hiyerarşinizi daha sonraki bir zamanda genişletme senaryosunu destekler. Bu site genişletme senaryosunda bağımsız birincil siteniz bir alt birincil site haline gelir ve daha sonra yeni merkezi yönetim sitenizin altına ek alt birincil siteler yükleyebilirsiniz. Daha sonra ilk dağıtımınızı, kuruluşunuzun gelecekteki büyümesi için genişletebilirsiniz.  

> [!TIP]  
>  Bağımsız bir birincil site ve bir alt birincil site aslında aynı tür site: birincil bir sitedir. Adındaki farklılık, merkezi yönetim sitesi kullandığınızda da oluşturulan hiyerarşi ilişkisine dayalıdır. Bu hiyerarşi ilişkisi Ayrıca Configuration Manager işlevselliği genişleten bazı site sistemi rollerinin yüklenmesini de sınırlayabilir. Bu rol sınırlaması, bazı site sistemi rollerinin yalnızca hiyerarşinin üst katman sitesine, merkezi bir yönetim sitesine veya tek başına bir birincil siteye yüklenebileceğinden oluşur.  

 İlk sitenizi yükledikten sonra ek siteler yükleyebilirsiniz. İlk siteniz bir merkezi yönetim sitesi ise, bir veya daha fazla alt birincil site yükleyebilirsiniz. Birincil bir siteyi (tek başına veya alt birincil) yükledikten sonra bir veya daha fazla ikincil site yükleyebilirsiniz.  

 Bir *ikincil site* , yalnızca bir birincil sitenin bir alt sitesi olarak yüklenebilir. Bu site, birincil sitenin birincil siteye yavaş bir ağ bağlantısı olan konumlarda cihaz yönetim erimini genişletir. İkincil bir site birincil siteyi genişletse de birincil site tüm istemcileri yönetir. İkincil site, uzak konumdaki cihazlar için destek sağlar. İstemcilere gönderilen (dağıttığınız) ve istemcilerin siteye geri gönderdiği bilgilerin aktarımını sıkıştırarak ve sonra yönetim sağlar.  

 Aşağıdaki diyagramlarda bazı örnek site tasarımları görülmektedir.  

 ![Hiyerarşi örnekleri](media/Hierarchy_examples.png)  

 Daha fazla bilgi edinmek için aşağıdaki kaynaklara bakın:  

-   [Configuration Manager'a Giriş](../../core/understand/introduction.md)  

-   [Configuration Manager için bir site hiyerarşisi tasarlama](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Configuration Manager sitelerini yükler](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>Site sistemi sunucuları ve site sistemi rolleri  
 Her bir Configuration Manager sitesi, yönetim işlemlerini destekleyen *site sistem rollerini* yüklüyor. Aşağıdaki roller, bir sitesini yüklediğinizde varsayılan olarak yüklenir:

-   Site sunucusu rolü, siteyi yüklediğiniz bilgisayara atanır.

-   Site veritabanı sunucusu rolü, site veritabanını barındıran SQL Server atanır.

Diğer site sistem rolleri isteğe bağlıdır ve yalnızca bir site sistem rolünde etkin olan işlevleri kullanmak istediğinizde kullanılır. Site sistem rolü barındıran bir bilgisayara site sistem sunucusu denir.  

 Daha küçük bir Configuration Manager dağıtımı için, ilk olarak tüm site sistem rollerinizi doğrudan site sunucusu bilgisayarında çalıştırabilirsiniz. Daha sonra, yönetilen ortamınız ve gereksinimleriniz büyüdükçe, sitenin daha fazla cihaza hizmet sağlama verimliliğini artırmak için ek site sistem rollerini barındırmak üzere ek site sistemi sunucuları yükleyebilirsiniz.  

 Farklı site sistemi rolleri hakkında daha fazla bilgi için, bkz. site sistem [sunucuları ve site sistem Configuration Manager rolleri Için plan](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)'da [site sistemi rolleri](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) .

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Site bilgilerini Active Directory Etki Alanı Hizmetleri'nde yayımlama  
 Configuration Manager yönetimini basitleştirmek için, Active Directory şemasını Configuration Manager tarafından kullanılan ayrıntıları destekleyecek şekilde genişletebilir ve ardından sitelerin anahtar bilgilerini Active Directory Domain Services (AD DS) yayımlamasını sağlayabilirsiniz. Daha sonra yönetmek istediğiniz bilgisayarlar, AD DS güvenilir kaynağından siteyle ilgili bilgileri güvenli bir şekilde alabilir. İstemcilerin alabileceği bilgiler kullanılabilen siteleri, site sistem sunucularını ve bu site sistem sunucularının sağladığı hizmetleri tanımlar.  

 *Active Directory şemasının genişletilmesi* her orman için yalnızca bir kez gerçekleştirilir ve Configuration Manager yüklemeden önce veya sonra yapılabilir.   Şemayı genişlettiğinizde, her etki alanında sistem yönetimi adlı yeni bir Active Directory kapsayıcısı oluşturmanız gerekir. Kapsayıcı, istemcilerin bulması için veri yayımlayacak bir Configuration Manager sitesi içerir. Daha fazla bilgi için bkz. [site yayımlama için Active Directory hazırlama](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 *Site verilerini yayımlama* , Configuration Manager hiyerarşinizin güvenliğini artırır ve yönetim yükünü azaltır, ancak temel Configuration Manager işlevselliği için gerekli değildir.  
