---
title: Bulma yöntemlerini seçme
titleSuffix: Configuration Manager
description: Hangi yöntemlerin kullanılacağı ve hangi sitelerde çalıştırılacağı hakkında dikkat edilecek konuları gözden geçirin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f08ab44a11b48b4446a372c4f6065ea0d7c63e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718353"
---
# <a name="select-discovery-methods-to-use-for-configuration-manager"></a>Configuration Manager için kullanılacak bulma yöntemlerini seçin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için bulmayı başarılı ve verimli bir şekilde kullanmak için hangi yöntemlerin kullanılacağını ve hangi sitelerde çalıştırılacağını göz önünde bulundurmanız gerekir.  

 Bulma işlemi büyük miktarda ağ trafiği üretebildiğinden ve sonuç bulma verileri kayıtları (DDR 'ler) işlem sırasında önemli CPU kaynakları kullanabileceğinden, yalnızca hedeflerinizi karşılamak için gerekli olan bulma yöntemlerini kullanın. Yalnızca bir veya iki bulma yöntemi kullanarak başlayabilir ve daha sonra ortamınızda bulma düzeyini genişletmek için daha sonra denetimli bir şekilde ek yöntemler etkinleştirebilirsiniz. Bu konudaki bilgiler bilinçli kararlar almanıza yardımcı olabilir.  

 Farklı bulma yöntemleri hakkında daha fazla bilgi için bkz. [Configuration Manager bulma yöntemleri hakkında](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Farklı şeyleri keşfetme yöntemlerini seçin  
 Potansiyel Configuration Manager istemci bilgisayarlarını veya Kullanıcı kaynaklarını bulmak için uygun bulma yöntemlerini etkinleştirmeniz gerekir. Farklı kaynakları bulmak ve bu kaynaklarla ilgili ek bilgileri bulmak için farklı bulma yöntemleri birleşimleri kullanabilirsiniz. Kullandığınız bulma yöntemleri, bulunan ve bulma işleminde hangi Configuration Manager hizmetleri ve aracılarının kullanıldığını belirleyen kaynak türlerini ve hangilerinin kullanılacağını tespit ediyor. Ayrıca, keşfedebilmeniz gereken kaynaklarla ilgili bilgi türünü de tespit ederler.  

### <a name="discover-computers"></a>Bilgisayarları bul   
Bilgisayarları bulmak istediğinizde **Active Directory sistem bulma** veya **ağ bulma**'yı kullanabilirsiniz.  

 Örneğin, Client Push yüklemesini kullanmadan önce Configuration Manager istemcisini yükleyebilen kaynakları bulmak istiyorsanız Active Directory sistem bulma işlemini çalıştırabilirsiniz. Bu yöntemi kullanarak, yalnızca kaynağı bulamayacak gibi temel bilgileri de Active Directory Domain Services ile ilgili genişletilmiş bilgiler de bulabilirsiniz. Bu bilgiler, istemci ayarları veya içerik dağıtımı ataması için kullanılacak karmaşık sorgular ve Koleksiyonlar oluşturmak için yararlı olabilir.

Alternatif olarak, ağ bulmayı çalıştırabilir ve kaynakların işletim sistemini bulmak için seçeneklerini kullanabilirsiniz (daha sonra Client Push yüklemesini kullanmak için gereklidir). Ağ bulma, ağ topolojiniz hakkında diğer keşif yöntemleriyle elde edemeyebilirsiniz hakkında bilgiler sağlar. Ancak, bu yöntem Active Directory ortamınız hakkında herhangi bir bilgi sağlamaz.

 Ayrıca **sinyal bulma**adlı bir yöntem de vardır. İstemci gönderme yüklemesi dışındaki yöntemlerle yüklediğiniz istemcilerin bulunmasını zorlamak için yalnızca sinyal keşfi kullanmak mümkündür. Ancak, diğer bulma yöntemlerinin aksine, sinyal keşfi etkin bir Configuration Manager istemcisine sahip olmayan bilgisayarları bulamaz. Bu, kaydın temeli yerine var olan bir veritabanı kaydını sürdürmek için tasarlanan sınırlı bir bilgi kümesi döndürür. Sinyal keşfi tarafından gönderilen bilgiler karmaşık sorgular veya Koleksiyonlar oluşturmak için yeterli olmayabilir.  

 Belirtilen grubun üyeliğini bulmak için **Active Directory Grup keşfi** kullanıyorsanız, sınırlı sistem veya bilgisayar bilgilerini bulabilirsiniz. Bu, bilgisayarların tam keşfinin yerini almaz, ancak temel bilgileri sağlayabilir. Bu bilgi, istemci gönderme yüklemesi için yetersiz.  

### <a name="discover-users"></a>Kullanıcıları bul   
Kullanıcılar hakkında bilgi bulmak istediğinizde **Active Directory Kullanıcı keşfi**' ni kullanın. Active Directory sistem bulmaya benzer şekilde, bu yöntem kullanıcıları Active Directory bulur. Genişletilmiş Active Directory bilgilerine ek olarak temel bilgileri içerir. Bu bilgileri, bilgisayarlara benzer karmaşık sorgular ve Koleksiyonlar oluşturmak için kullanabilirsiniz.  

### <a name="discover-group-information"></a>Grup bilgilerini bul   
Gruplar ve grup üyelikleri hakkında bilgi bulmak istediğinizde **Active Directory Grup keşfi**kullanın. Bu bulma yöntemi güvenlik grupları için kaynak kayıtları oluşturur.  

 Bu yöntemi, bu grubun üyelerini tanımlamak üzere belirli bir Active Directory grubunu aramak için kullanabilirsiniz. Bu yöntemi, gruplar için bir Active Directory konumu aramak ve Active Directory Etki Alanı Hizmetleri'nde o konumun her bir alt kapsayıcısını özyinelemeli olarak aramak için de kullanabilirsiniz.  

 Bu bulma yöntemi dağıtım gruplarının üyeliğini de arayabilir. Bu, hem kullanıcıların hem de bilgisayarların grup ilişkilerini tanımlayabilir.  

 Bir grup bulduğunuzda, üyeleri hakkında sınırlı bilgileri de bulabilirsiniz. Bu, Active Directory sistemi veya Kullanıcı bulma yöntemlerinin yerini almaz. Karmaşık sorgular ve Koleksiyonlar oluşturmak için genellikle yeterli değildir veya istemci gönderme yüklemesinin temeli olarak görev yapar.  

### <a name="discover-infrastructure"></a>Altyapıyı bul   
Ağ altyapısını bulmak için kullanabileceğiniz iki yöntem vardır, **Active Directory orman bulma** ve **ağ bulma**.  

 Active Directory orman bulma kullanarak alt ağlar ve Active Directory site yapılandırması hakkında bilgi için Active Directory ormanında arama yapın. Bu konfigürasyonlar daha sonra, sınır konumları olarak Configuration Manager otomatik olarak girilebilir.  

 Ağ topolojinizi bulmak istediğinizde ağ bulma 'yı kullanın. Diğer bulma yöntemleri Active Directory Domain Services ile ilgili bilgiler döndürirken ve bir istemcinin geçerli ağ konumunu belirleyebilecekleri için, ağınızın alt ağlarına ve yönlendirici topolojisine göre altyapı bilgileri sağlamalardır.  

##  <a name="discovery-data-is-shared-among-sites"></a><a name="bkmk_shared"></a>Bulma verileri siteler arasında paylaşılıyor  
 Configuration Manager bir veritabanına bulgu verileri ekledikten sonra, hiyerarşideki tüm siteler arasında hızlı bir şekilde paylaşılır. Hiyerarşinizdeki birden çok sitede aynı bilgileri bulmanın bir avantajı olmadığından, tek bir sitede çalıştırmak için kullandığınız her bulma yönteminin tek bir örneğini ayarlamayı düşünün. Farklı sitelerde tek bir yöntemin birden çok örneğini çalıştırmak yerine bunu yapmak iyi bir fikirdir.  

 Ancak bazı ortamlarda, her biri ayrı bir yapılandırma ve zamanlamaya sahip birden fazla sitede çalışacak aynı bulma yöntemini atamak yararlı olabilir. Örneğin, ağ bulmayı kullanırken, WAN genelindeki tüm ağ konumlarını bulmayı denemek yerine, her siteyi yerel ağını bulmak için yönlendirmek isteyebilirsiniz.

Aynı bulma yöntemlerinin birden fazla örneğini farklı sitelerde çalışacak şekilde yapılandırırsanız, her sitenin yapılandırmasını dikkatle planlayın. İki veya daha fazla sitenin, ağınızdan veya Active Directory aynı kaynakları bulmasını önlemek isteyebilirsiniz. Bu, ek ağ bant genişliği kullanabilir ve yinelenen DDR 'ler oluşturabilir.

Aşağıdaki tabloda farklı bulma yöntemlerini ayarlayabileceğiniz siteler tanımlanmaktadır.  

|Bulma yöntemi|Desteklenen konumlar|  
|----------------------|-------------------------|  
|Active Directory Orman Saptama|Merkezi yönetim sitesi<br /><br /> Birincil site|  
|Active Directory Grup Saptama|Birincil site|  
|Active Directory Sistem Saptama|Birincil site|  
|Active Directory Kullanıcı Saptama|Birincil site|  
|Sinyal bulma<sup>1</sup>|Birincil site|  
|Ağ Bulma|Birincil site<br /><br /> İkincil site|  

 <sup>1</sup> ikincil siteler, sinyal bulmayı yapılandıramıyor, ancak bir ISTEMCIDEN sinyal DDR 'sini alabilir.  

 İkincil siteler ağ bulmayı çalıştırır veya sinyal keşfi DDR 'leri aldıktan sonra DDR 'yi dosya tabanlı çoğaltma ile üst birincil sitelerine aktarır. Bunun nedeni yalnızca birincil sitelerin ve merkezi yönetim sitelerinin DDR 'leri işleyebileceğinden kaynaklanır. DDR 'lerin nasıl işlendiği hakkında daha fazla bilgi için bkz. [bulma verileri kayıtları hakkında](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Farklı bulma yöntemlerine ilişkin hususlar  
 Her site sunucusu ve ağ ortamı farklı olduğundan, ilk konfigürasyonların keşif için sınırlandırmanız iyi bir fikirdir. Daha sonra, her site sunucusunu, oluşturulan bulgu verilerini işleyebilme yeteneği için yakından izleyin.  

Sistemler, kullanıcılar veya gruplar için **Active Directory** bulma yöntemi kullandığınızda:  

-   Etki alanı denetleyicilerinize hızlı bir ağ bağlantısı olan bir sitede bulma işlemini çalıştırın.  

-   Bulmanın en son bilgilere erişebildiğinden emin olmak için Active Directory çoğaltma topolojisini göz önünde bulundurun.  

-   Bulma yapılandırmasının kapsamını değerlendirin ve bulmayı yalnızca keşfettiğiniz Active Directory konumları ve gruplarıyla sınırlayın.  

**Ağ bulma**kullanıyorsanız:  

-   Ağ topograflarınızı tanımlamak için sınırlı bir başlangıç yapılandırması kullanın.  

-   Ağ topograflarınızı tanımladıktan sonra, ağ bulmayı daha fazla tam bulmak istediğiniz ağ alanlarına merkezi olan belirli sitelerde çalışacak şekilde ayarlayın.  

**Sinyal keşfi** belirli bir sitede çalıştırılmadığından, bulmayı nerede çalıştıracağınızı genel planlamaya göz önünde bulundurmayın.  

##  <a name="best-practices-for-discovery"></a><a name="bkmk_best"></a>Bulma için en iyi uygulamalar  
Bulma ile ilgili en iyi sonuçlar için şunları öneririz:

- **Active Directory Grup bulmayı çalıştırmadan önce sistem bulmayı ve Active Directory Kullanıcı bulmayı Active Directory çalıştırın.**  

  Active Directory Grup keşfi, daha önce keşfedilmemiş bir kullanıcıyı veya bilgisayarı bir grubun üyesi olarak belirlediğinde, Kullanıcı veya bilgisayar için temel ayrıntıları bulmaya çalışır. Active Directory Grup keşfi bu tür bir bulma için iyileştirilmediğinden, bu işlem yavaş çalışmasına neden olabilir. Ayrıca, Active Directory Grup keşfi yalnızca bulduğu kullanıcılar ve bilgisayarlarla ilgili temel ayrıntıları tanımlar ve tüm Kullanıcı veya bilgisayar bulma kaydı oluşturmaz. Active Directory sistem bulmayı ve Active Directory Kullanıcı bulmayı çalıştırdığınızda, her nesne türü için ek Active Directory öznitelikleri kullanılabilir. Sonuç olarak, Active Directory Grup keşfi daha verimli bir şekilde çalışır.  

- **Active Directory grubu bulmayı ayarlarken, yalnızca Configuration Manager kullandığınız grupları belirtin.**  

  Active Directory Grup keşfi tarafından kaynakların kullanımını denetlemeye yardımcı olmak için, yalnızca Configuration Manager birlikte kullandığınız grupları belirtin. Bunun nedeni, Active Directory grubu bulmanın kullanıcılar, bilgisayarlar ve iç içe gruplar için bulduğu her grubu yinelemeli olarak arayacağı bir işlemdir. Her iç içe bir grubun araması Active Directory Grup bulma kapsamını genişletebilir ve performansı düşürebilir. Ayrıca, Active Directory Grup keşfi için Delta Keşfi ayarladığınızda, bulma yöntemi her grubu değişiklik için izler. Bu, yöntemin gereksiz grupları aramasını gerektiğinde performansı azaltır.  

- **Tam keşif ve daha sık değişim bulma süreci arasında daha uzun bir zaman aralığı ile bulma yöntemleri ayarlayın.**  

  Delta Keşfi tam bir keşif döngüsünden daha az kaynak kullandığından ve Active Directory yeni veya değiştirilmiş kaynakları belirleyebildiğinden, tam keşif döngülerinin sıklığını haftalık (veya daha az) çalışacak şekilde azaltabilirsiniz. Active Directory sistem bulma, Active Directory Kullanıcı bulma ve Active Directory Grup bulma için Delta Keşfi, Active Directory nesnelerinin neredeyse tüm değişikliklerini tanımlar ve kaynakların doğru bulma verilerini koruyabilir.  

- **Active Directory bulma yöntemlerini, Active Directory etki alanı denetleyicinize en yakın ağ konumuna sahip olan bir birincil sitede çalıştırın.**  

  Active Directory bulmanın performansını artırmak için, bulma işlemini etki alanı denetleyicilerinize hızlı bir ağ bağlantısı olan bir birincil sitede çalıştırmak iyi bir fikirdir. Aynı Active Directory bulma yöntemini birden çok sitede çalıştırırsanız, çakışma yaşamamak için her bulma yöntemini ayarlayın. Configuration Manager geçmiş sürümlerinden farklı olarak, bulma verileri siteler arasında paylaşılır. Bu nedenle, aynı bilgileri birden çok sitede keşfetmek gerekli değildir. Daha fazla bilgi için bkz. [bulma verileri siteler arasında paylaşılır](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Bulma verilerinden otomatik olarak sınırlar oluşturmayı planlarken yalnızca bir sitede Active Directory orman keşfi çalıştırın.**  

  Bir hiyerarşide birden fazla sitede Active Directory orman keşfi çalıştırırsanız, yalnızca tek bir sitede sınırları otomatik olarak oluşturmak için seçeneklerin etkinleştirilmesi iyi bir fikirdir. Bunun nedeni, Active Directory orman bulma her sitede çalışırken ve sınırlar oluşturduğunda Configuration Manager bu sınırları tek bir sınır nesnesi halinde birleştiremez. Birden çok sitede sınırları otomatik olarak oluşturmak için Active Directory orman bulmayı yapılandırdığınızda, sonuç, Configuration Manager konsolundaki yinelenen sınır nesneleri olabilir.  
