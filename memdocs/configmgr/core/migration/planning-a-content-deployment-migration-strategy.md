---
title: İçeriği geçir
titleSuffix: Configuration Manager
description: Configuration Manager geçerli bir dal hedefi hiyerarşisine veri geçirirken içeriği yönetmek için dağıtım noktalarını kullanın.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: afb39af5087daaca3b2bb6eb15f33d81d959beec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719690"
---
# <a name="plan-a-content-deployment-migration-strategy-in-configuration-manager"></a>Configuration Manager bir içerik dağıtımı geçiş stratejisi planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Verileri Configuration Manager geçerli dal hedefi hiyerarşisine etkin bir şekilde geçirdiğinizde, kaynak ve hedef Hiyerarşilerdeki istemciler Configuration Manager, kaynak hiyerarşisinde dağıttığınız içeriğe erişimi de koruyabilir. Kaynak hiyerarşisinden dağıtım noktalarını hedef hiyerarşide dağıtım noktaları olacak şekilde yükseltmek veya yeniden atamak için geçiş de kullanabilirsiniz. Dağıtım noktalarını paylaşarak yükselttiğinizde veya yeniden atadığınızda, geçişini yaptığınız istemciler için içeriği hedef hiyerarşideki yeni sunuculara yeniden dağıtmaktan kaçınmanıza bu strateji yardımcı olabilir.  

İçeriği hedef hiyerarşide yeniden oluşturup dağıtabilmenize karşın, bu içeriği yönetmek için aşağıdaki seçenekleri de kullanabilirsiniz:  

-   Kaynak hiyerarşideki dağıtım noktalarını hedef hiyerarşideki istemcilerle paylaşma.  

-   Kaynak hiyerarşisindeki tek başına Configuration Manager 2007 dağıtım noktasını veya Configuration Manager 2007 ikincil sitesini, hedef hiyerarşide dağıtım noktaları olacak şekilde yükseltin.  

-   Dağıtım noktalarını bir Configuration Manager kaynak hiyerarşisinden hedef hiyerarşisindeki bir siteye yeniden atayın.  

##  <a name="share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> Dağıtım noktalarını kaynak ve hedef hiyerarşiler arasında paylaştırma  
Geçiş sırasında, kaynak hiyerarşideki dağıtım noktalarını hedef hiyerarşiyle paylaşabilirsiniz. Kaynak hiyerarşiden geçirdiğiniz içeriği yeniden oluşturmak zorunda kalmadan hedef hiyerarşideki istemcilerin kullanımına anında sunmak ve sonra bu içeriği hedef hiyerarşideki yeni dağıtım noktalarına dağıtmak için paylaşılan dağıtım noktalarını kullanabilirsiniz. Hedef hiyerarşideki istemciler paylaştırdığınız dağıtım noktalarına dağıtılan içeriği istediğinde, paylaşılan dağıtım noktaları istemcilere geçerli içerik konumları olarak sunulabilir.  

 Kaynak hiyerarşisinden geçiş etkin olmaya çalışırken hedef hiyerarşideki istemciler için geçerli bir içerik konumu olmanın yanı sıra, dağıtım noktasını hedef hiyerarşiye yükseltmek veya yeniden atamak mümkündür. Configuration Manager 2007 paylaşılan dağıtım noktasını yükseltebilir ve System Center 2012 Configuration Manager paylaşılan dağıtım noktalarını yeniden atayabilirsiniz. Paylaşılan bir dağıtım noktasını yükselttiğinizde veya yeniden atadığınızda, o dağıtım noktası kaynak hiyerarşiden kaldırılır ve hedef hiyerarşide bir dağıtım noktasına dönüşür. Paylaşılan dağıtım noktasını yükselttikten veya yeniden atadıktan ve kaynak hiyerarşiden geçiş tamamlandıktan sonra, o dağıtım noktasını hedef hiyerarşide kullanmaya devam edebilirsiniz. Paylaşılan bir dağıtım noktasını yükseltme hakkında daha fazla bilgi için bkz. [Configuration Manager 2007 paylaşılan dağıtım noktasını yükseltmeyi planlayın](#Planning_to_Upgrade_DPs). Paylaşılan dağıtım noktasını yeniden atama hakkında daha fazla bilgi için, bkz. [Configuration Manager dağıtım noktalarını yeniden atamayı planlayın](#BKMK_ReassignDistPoint).  

 Kaynak hiyerarşinizdeki herhangi bir kaynak sitenin dağıtım noktalarını paylaşmayı seçebilirsiniz. Bir kaynak sitenin dağıtım noktalarını paylaştığınızda, alt ikincil siteler ilgili birincil sitedeki her bir uygun dağıtım noktasında ve birincil sitelerde paylaşılır. Paylaşılan bir dağıtım noktası olmasını sağlamak için, dağıtım noktasını barındıran site sistem sunucusunun tam etki alanı adı (FQDN) ile ayarlanması gerekir. NetBIOS adı ile ayarlanan tüm dağıtım noktaları göz ardı edilir.  

> [!TIP]  
>  Configuration Manager 2007, site sistemi sunucuları için bir FQDN ayarlamanıza gerek yoktur.  

Paylaşılan dağıtım noktalarını planlamanıza yardımcı olması için aşağıdaki bilgileri kullanın:  

-   Paylaştığınız dağıtım noktaları paylaşılan dağıtım noktalarına yönelik önkoşulları karşılamalıdır. Bu Önkoşullar hakkında daha fazla bilgi için, [geçiş önkoşulları](../../core/migration/prerequisites-for-migration.md)' nda [geçiş için gereken yapılandırmalara](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) bakın.  

-   Dağıtım noktası paylaşma işlemi, bir kaynak sitedeki ve onun tüm doğrudan alt ikincil sitelerindeki uygun olan tüm dağıtım noktalarını paylaşan site genelinde bir ayardır. Dağıtım noktası paylaşımını etkinleştirdiğinizde dağıtım noktalarını tek tek seçemezsiniz.  

-   Hedef hiyerarşideki istemciler, kaynak hiyerarşiden paylaşılan dağıtım noktalarına dağıtılan paketlerle ilgili içerik konum bilgilerini alabilir. Configuration Manager 2007 kaynak hiyerarşisinden dağıtım noktaları için, bu dal dağıtım noktaları, sunucu paylaşımlarında dağıtım noktaları ve standart dağıtım noktaları içerir.  

    > [!WARNING]  
    >  Kaynak hiyerarşisini değiştirdiğinizde, özgün kaynak hiyerarşisinden paylaşılan dağıtım noktaları artık kullanılamaz ve hedef hiyerarşideki istemcilere içerik konumu olarak sunulamaz. Geçiş işlemini özgün kaynak hiyerarşisini kullanacak şekilde yeniden yapılandırırsanız, önceden paylaşılmış dağıtım noktaları geçerli içerik konumu sunucuları olarak geri yüklenir.  

-   Paylaşılan dağıtım noktasında barındırılan bir paketi geçirdiğinizde, paket sürümü kaynak ve hedef hiyerarşilerde aynı kalmalıdır. Paket sürümü kaynak ve hedef hiyerarşide aynı olmadığında, hedef hiyerarşideki istemciler o içeriği paylaşılan dağıtım noktasından alamazlar. Bu nedenle, kaynak hiyerarşideki bir paketi güncelleştiriyorsanız hedef hiyerarşideki istemcilerin paylaşılan dağıtım noktasından o içeriği alabilmeleri için paketi yeniden geçirmeniz gerekir.  

    > [!NOTE]  
    >  Paylaşılan bir dağıtım noktasında barındırılan bir paketin ayrıntılarını görüntülediğinizde, kaynak sitenin **paylaşılan dağıtım noktaları** sekmesinde **barındırılan geçirilmiş paketler** olarak görüntülenen paket sayısı, sonraki veri toplama çevrimi tamamlanana kadar güncellenmez.  

-   Paylaşılan dağıtım noktalarını ve özelliklerini, hedef hiyerarşiye bağlanan Configuration Manager konsolundaki **Yönetim** çalışma alanının **kaynak hiyerarşisi** düğümünde görüntüleyebilirsiniz.  

-   Microsoft Application Virtualization (App-V) paketlerini barındırmak için Configuration Manager 2007 kaynak hiyerarşisinden paylaşılan dağıtım noktasını kullanamazsınız. App-V paketlerinin hedef hiyerarşideki istemciler tarafından kullanılmak üzere geçirilmesi ve dönüştürülmesi gerekir. Ancak, bir hedef hiyerarşideki istemciler için App-V paketlerini barındırmak üzere System Center 2012 Configuration Manager paylaşılan dağıtım noktasını kullanabilir veya geçerli dal kaynak hiyerarşisinden Configuration Manager.  

-   Configuration Manager 2007 kaynak hiyerarşisinden korunan bir dağıtım noktasını paylaştığınızda, hedef hiyerarşi o dağıtım noktasının korunan ağ konumlarını içeren bir sınır grubu oluşturur. Bu sınır grubunu hedef hiyerarşide değiştiremezsiniz. Ancak, Configuration Manager 2007 kaynak hiyerarşisinde dağıtım noktası için korumalı sınır bilgilerini değiştirirseniz, bu değişiklik, bir sonraki veri toplama döngüsünden sonra hedef hiyerarşiye yansıtılır.  

    > [!NOTE]  
    >  System Center 2012 Configuration Manager ve Configuration Manager geçerli dal siteleri, korunan dağıtım noktaları yerine tercih edilen dağıtım noktaları kavramını kullanır. Bu koşul yalnızca Configuration Manager 2007 kaynak sitelerinden paylaşılan dağıtım noktaları için geçerlidir.  

Dağıtım noktalarını bir kaynak sitesinden paylaşmadan önce, uygun dağıtım noktaları Configuration Manager konsolunda görünmez. Dağıtım noktalarını paylaştıktan sonra, yalnızca başarıyla paylaşılan dağıtım noktaları listelenir.  

Dağıtım noktalarını paylaştıktan sonra, kaynak hiyerarşide paylaşılan tüm dağıtım noktalarının yapılandırmasını değiştirebilirsiniz. Dağıtım noktasının yapılandırmasında yaptığınız değişiklikler bir sonraki veri toplama döngüsünden sonra hedef hiyerarşiye yansıtılır. Paylaşıma uygun hale getirmek için güncelleştirdiğiniz dağıtım noktaları otomatik olarak paylaşılırken artık uygun olmayanlar dağıtım noktası paylaşımını durdurur. Örneğin, intranet FQDN 'SI ile ayarlanmamış ve başlangıçta hedef hiyerarşiyle paylaşılmayan bir dağıtım noktanız olabilir. Bu dağıtım noktası için FQDN ayarladıktan sonra, bir sonraki veri toplama çevrimi bu yapılandırmayı tanımlar ve dağıtım noktası daha sonra hedef hiyerarşiyle paylaşılır.  

##  <a name="plan-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a>Configuration Manager 2007 paylaşılan dağıtım noktasını yükseltmeyi planlayın  
Configuration Manager 2007 kaynak hiyerarşisinden geçiş yaptığınızda, paylaşılan bir dağıtım noktasını yükselterek güncel bir dal dağıtım noktası Configuration Manager yapabilirsiniz. Dağıtım noktalarını birincil sitelerde ve ikincil sitelerde yükseltebilirsiniz. Yükseltme işlemi, dağıtım noktasını Configuration Manager 2007 hiyerarşisinden kaldırır ve hedef hiyerarşide bir site sistemi sunucusu yapar. Bu işlem Ayrıca dağıtım noktasındaki mevcut içeriği dağıtım noktası bilgisayarında yeni bir konuma kopyalar. Yükseltme işlemi daha sonra hedef hiyerarşide içerik dağıtımında kullanılmak üzere tek örnekli depo oluşturmak için bu içeriğin kopyasında değişiklik yapar. Bu nedenle, bir dağıtım noktasını yükselttiğinizde, Configuration Manager 2007 dağıtım noktasında barındırılan geçirilmiş içeriği yeniden dağıtmanız gerekmez.  

Configuration Manager, içeriği tek örnek deposuna dönüştürdükten sonra, Configuration Manager disk alanını boşaltmak için dağıtım noktası bilgisayarındaki özgün kaynak içeriğini siler. Configuration Manager özgün kaynak içeriği konumunu kullanmaz.  

Paylaşabileceğiniz tüm Configuration Manager 2007 dağıtım noktaları geçerli dala Configuration Manager yükseltmeye uygun değildir. Configuration Manager 2007 dağıtım noktasının yükseltmeye uygun olması için yükseltme koşullarını karşılaması gerekir. Bu koşullar, dağıtım noktasının yüklendiği site sistemi sunucusunu ve yüklü Configuration Manager 2007 dağıtım noktasının türünü içerir. Örneğin, birincil sitedeki site sunucusu bilgisayara yüklenmiş hiçbir tür dağıtım noktası yükseltilemez, ancak ikincil bir sitedeki site sunucusu bilgisayara yüklenmiş standart bir dağıtım noktasını yükseltebilirsiniz.  

> [!NOTE]  
>  Yalnızca hedef hiyerarşideki dağıtım noktaları için desteklenen bir işletim sistemi sürümünü çalıştıran bir bilgisayarda bulunan Configuration Manager 2007 paylaşılan dağıtım noktalarını yükseltebilirsiniz. Örneğin, Windows Vista çalıştıran bir bilgisayarda bir Configuration Manager 2007 dağıtım noktasını paylaşabilseniz de, işletim sistemi bir dağıtım noktası olarak kullanılmak üzere Configuration Manager geçerli dalı tarafından desteklenmediğinden, bu paylaşılan dağıtım noktasını yükseltemezsiniz.  

Aşağıdaki tabloda, yükselteceğiniz her bir Configuration Manager 2007 dağıtım noktası türü için desteklenen konumlar listelenmektedir.  

|Dağıtım noktası türü|Site sunucusu dışındaki site sistemi bilgisayarında olan dağıtım noktası|Site sunucusu dışında olan ve diğer site sistemi rollerini barındıran bir site sistemi bilgisayarındaki dağıtım noktası|İkincil site sunucusundaki dağıtım noktası|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Standart dağıtım noktası|Yes|Hayır|Yes|  
|Sunucu paylaşımlarındaki dağıtım noktası<sup>1</sup>|Yes|Hayır|Hayır|  
|Dal dağıtım noktası|Yes|Hayır|Hayır|  

 <sup>1</sup> Configuration Manager geçerli dal site sistemleri için sunucu paylaşımlarını desteklemez, ancak sunucu paylaşımındaki bir Configuration Manager 2007 dağıtım noktasının yükseltmesini destekler. Sunucu paylaşımındaki bir Configuration Manager 2007 dağıtım noktasını yükselttiğinizde, dağıtım noktası türü otomatik olarak sunucuya dönüştürülür ve tek örnekli içerik deposunu depolayacak dağıtım noktası bilgisayarındaki sürücüyü seçmeniz gerekir.  

> [!WARNING]  
>  Bir şube dağıtım noktasını yükseltmeden önce Configuration Manager 2007 istemci yazılımını kaldırın. Configuration Manager 2007 istemci yazılımının yüklü olduğu bir dal dağıtım noktasını yükselttiğinizde, bilgisayara önceden dağıtılmış olan içerik bilgisayardan kaldırılır ve dağıtım noktasının yükseltilmesi başarısız olur.  

**Kaynak hiyerarşisi** düğümündeki Configuration Manager konsolunda yükseltme için uygun olan dağıtım noktalarını tanımlamak için bir kaynak site seçin ve ardından **paylaşılan dağıtım noktaları** sekmesini seçin. uygun dağıtım noktaları **yükseltme için uygun** sütununda **Evet** olarak görüntülenir.  

Configuration Manager 2007 ikincil site sunucusunda yüklü bir dağıtım noktasını yükselttiğinizde, ikincil site kaynak hiyerarşisinden kaldırılır. Bu senaryo ikincil site yükseltme olarak adlandırılsa da, sadece dağıtım noktası site sistem rolü için geçerlidir. Sonuçta ikincil site yükseltilmez, bunun yerine kaldırılır. Bu, ikincil site sunucusu olan bilgisayardaki hedef hiyerarşisinden bir dağıtım noktası bırakır. Dağıtım noktasını ikincil bir sitede yükseltmeyi planlıyorsanız, bu konudaki [2007 ikincil siteleri Configuration Manager yükseltmeyi planlayın](#BKMK_UpgradeSS) bölümüne bakın.  

###  <a name="distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a> Dağıtım noktası yükseltme işlemi  
Hedef hiyerarşisiyle paylaştığınız Configuration Manager 2007 dağıtım noktasını yükseltmek için Configuration Manager konsolunu kullanabilirsiniz. Paylaşılan bir dağıtım noktasını yükselttiğinizde, dağıtım noktası Configuration Manager 2007 sitesinden kaldırılır. Daha sonra hedef hiyerarşisinde belirttiğiniz birincil veya ikincil bir siteye bağlı bir dağıtım noktası olarak yüklenir. Yükseltme işlemi, geçiş yapılan içeriğin dağıtım noktasında saklanan bir kopyasını oluşturur ve ardından bu kopyayı, tek örnek içerik deposuna dönüştürür. Configuration Manager bir paketi tek örnekli içerik deposuna dönüştürdüğünde, paketin **programı dağıtım noktasından Çalıştır**olarak ayarlanmış bir veya daha fazla reklamı olmadığı takdirde, bu paketi dağıtım noktası bilgisayarındaki SMSPKG paylaşımından siler.  

Dağıtım noktasını yükseltmek için Configuration Manager, kaynak sitenin SMS sağlayıcısından veri toplamak üzere ayarlanan **kaynak site erişim hesabını** kullanır. Bu hesap, kaynak siteden veri toplamak üzere site nesneleri için yalnızca **okuma** izni gerektirse de, yükseltme sırasında dağıtım noktasını Configuration Manager 2007 sitesinden başarıyla kaldırmak için **site** sınıfında **silme** ve **değiştirme** iznine de sahip olmalıdır.  

> [!NOTE]  
>  Configuration Manager, içeriği tek seferde yalnızca bir dağıtım noktasında tek örnek deposuna dönüştürebilir. Birden çok dağıtım noktası yükseltmesi ayarladığınızda, dağıtım noktaları yükseltme için sıraya alınır ve tek seferde işlenir.  

Paylaşılan bir dağıtım noktasını yükselttiğinizde, dağıtım noktasına dağıtılan tüm içeriğin geçirildiğinden emin olun. Dağıtım noktasını yükseltmeden önce geçişini yapmadığınız içerik, yükseltme sonrası hedef hiyerarşisinde kullanılamaz. Bir dağıtım noktasını yükselttiğinizde, geçiş yapılan paketlerin içeriği hedef hiyerarşisindeki tek örnek depoyla uyumlu bir biçime dönüştürülür.  

Configuration Manager konsolu içinden bir dağıtım noktasını yükseltmek için, Configuration Manager 2007 site sistem sunucusu aşağıdaki koşulları karşılamalıdır:  

-   Dağıtım noktası yapılandırması ve konumu yükseltme için uygun olmalıdır.  

-   Dağıtım noktası bilgisayarında Configuration Manager 2007 içerik depolama biçiminden tek örnek depo biçimine dönüştürülecek içerik için yeterli disk alanı olmalıdır. Bu dönüştürme dağıtım noktasında saklanan en büyük paketin boyutuna eşit kullanılabilir boş disk alanı gerektirir.  

-   Dağıtım noktası bilgisayarı, hedef hiyerarşisinde dağıtım noktası olarak desteklenen bir işletim sistemi sürümünde çalıştırılmalıdır.  

    > [!NOTE]  
    >  Configuration Manager, yükseltme için dağıtım noktasının uygunluğunu denetlediğinde, dağıtım noktası bilgisayarının işletim sistemi sürümünü doğrulamaz.  

Bir dağıtım noktasını yükseltmek için, **Yönetim** çalışma alanında, **geçiş**' i genişletin, **kaynak hiyerarşisi** düğümünü genişletin ve ardından yükseltmek istediğiniz dağıtım noktasını içeren siteyi seçin. Ardından ayrıntılar panelinden, **Paylaşılan Dağıtım Noktaları** sekmesinden yükseltmek istediğiniz dağıtım noktasını seçin.  

**Yeniden Atama için Uygun** sütununda durumu görüntüleyerek dağıtım noktasının yükseltme için hazır olduğunu doğrulayabilirsiniz.  Ardından, Configuration Manager konsolu şeridinde dağıtım **noktaları** sekmesinde, **dağıtım noktası** grubunda **yeniden ata**' yı seçin. Bu, dağıtım noktasının yükseltmesini bitirebilmeniz için kullandığınız bir Sihirbazı açar.  

Paylaşılan bir dağıtım noktasını yükseltirken, dağıtım noktasını hedef hiyerarşide tercih ettiğiniz birincil veya ikincil bir siteye atamanız gerekir. Dağıtım noktası yükseltildikten sonra, dağıtım noktasını diğer dağıtım noktaları gibi hedef hiyerarşideki bir dağıtım noktası olarak yönetin.  

**Yönetim** çalışma alanının **geçiş** düğümü altındaki **dağıtım noktası geçişi** düğümünü seçerek Configuration Manager konsolundaki dağıtım noktası yükseltmesinin ilerlemesini izleyebilirsiniz. Ayrıca, bilgileri hedef hiyerarşinin merkezi yönetim site sunucusunda **Migmctrl.log** içinde veya yükseltilmiş dağıtım noktasını yöneten hedef hiyerarşisindeki site sunucuda bulunan **distmgr.log** içinde görüntüleyebilirsiniz.  

> [!NOTE]  
>  Dağıtım noktasını hedef hiyerarşisine yükselttiğinizde, dağıtım noktası site sistemi rolü Configuration Manager 2007 kaynak sitesinden kaldırılır. Ancak, dağıtım noktasına gönderilen paketler Configuration Manager 2007 hiyerarşisinde güncellenmez. Configuration Manager 2007 konsolunda, dağıtım noktasına gönderilen paketler site sistem bilgisayarını **Bilinmeyen** **türde** bir dağıtım noktası olarak listemeye devam eder. Configuration Manager 2007 ' de paketin sonraki güncelleştirmeleri, site bilinmeyen site sisteminde paketi güncelleştirmeye çalıştığında, bu site için Distmgr. log dosyasında dağıtım Yöneticisi raporlama hatalarıyla sonuçlanır.  

Paylaşılan bir dağıtım noktasını yükseltmemeye karar verirseniz, önceki Configuration Manager 2007 dağıtım noktasındaki hedef hiyerarşisinden bir dağıtım noktası yüklemeye devam edebilirsiniz. Yeni dağıtım noktasını yüklemeden önce, dağıtım noktası bilgisayarından tüm Configuration Manager 2007 site sistem rollerini kaldırmanız gerekir. Bu, site sunucusu bilgisayar ise Configuration Manager 2007 sitesini içerir. Configuration Manager 2007 dağıtım noktasını kaldırdığınızda, dağıtım noktasına dağıtılan içerik bilgisayardan silinmez.  

###  <a name="plan-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a>Configuration Manager 2007 ikincil sitesini yükseltmeyi planlayın  
 Configuration Manager 2007 ikincil site sunucusunda barındırılan paylaşılan bir dağıtım noktasını yükseltmek için geçiş kullandığınızda, Configuration Manager dağıtım noktası site sistem rolünü hedef hiyerarşide bir dağıtım noktası olacak şekilde yükseltir. Ayrıca, ikincil siteyi kaynak hiyerarşisinden kaldırır. Sonuç, geçerli bir dal dağıtım noktası olan, ancak ikincil site olmayan Configuration Manager.  

 Site sunucusu bilgisayarındaki bir dağıtım noktasının yükseltmeye uygun olması için Configuration Manager, ikincil siteyi ve o bilgisayardaki site sistem rollerini kaldırabilmelidir. Genellikle Configuration Manager 2007 sunucu paylaşımındaki paylaşılan bir dağıtım noktası yükseltme için uygun değildir. Bununla birlikte, ikincil site sunucuda bir sunucu paylaşımı mevcut olduğunda, o bilgisayardaki ikincil site ve paylaşılan dağıtım noktaları yükseltme için uygun olmaz. Bunun nedeni, işlem ikincil siteyi kaldırmayı denediğinde sunucu paylaşımının ek site sistem nesnesi olarak kabul edilmesidir ve bu işlem bu nesneyi kaldıramaz. Bu senaryoda, ikincil site sunucuda standart dağıtım noktasını etkinleştirebilir ve ardından içeriği o standart dağıtım noktasına yeniden dağıtabilirsiniz. Bu işlem ağ bant genişliği kullanmaz ve işiniz bittiğinde, sunucu paylaşımındaki dağıtım noktasını kaldırabilir, sunucu paylaşımından kaldırabilirsiniz ve ardından dağıtım noktası ve ikincil siteyi yükseltebilirsiniz.  

 Paylaşılan bir dağıtım noktasını yükseltmeden önce, Configuration Manager 2007 ile kullanmak istediğiniz ikincil sitedeki bir dağıtım noktasını yükseltmeyi önlemek için Configuration Manager 2007 ' deki dağıtım noktası yapılandırmasını gözden geçirin. İkincil bir site sunucusunda bulunan paylaşılan bir dağıtım noktasını yükselttikten sonra, site sistem sunucusu Configuration Manager 2007 hiyerarşisinden kaldırılır ve artık bu hiyerarşi ile kullanılamaz. İkincil site kaldırıldığında, o ikincil sitede kalan tüm dağıtım noktaları yalnız bırakılır. Bu, Configuration Manager 2007 ' den yönetilmeyen hale geldikleri ve artık paylaşılmayan veya yükseltme için uygun olmadığı anlamına gelir.  

> [!WARNING]  
>  Configuration Manager konsolunda paylaşılan dağıtım noktalarını görüntülerken, paylaşılan dağıtım noktasının uzak bir site sistem sunucusunda veya ikincil site sunucusunda olduğu görünür bir gösterge yoktur.  

 Birincil bir ağ konumunda, bu uzak konuma içerik dağıtımını denetlemek için kullanılan bir ikincil siteniz varsa, paylaşılan dağıtım noktası olan ikincil siteleri yükseltmeyi göz önünde bulundurun. Configuration Manager geçerli bir dal dağıtım noktasına içerik dağıttığınızda bant genişliği denetimini ayarlayabilmeniz için, genellikle ikincil bir siteyi bir dağıtım noktasına yükseltebilir, bant genişliği denetimleri için dağıtım noktasını ayarlayabilir ve ikincil bir siteyi hedef hiyerarşisindeki o ağ konumuna yüklemekten kaçınabilirsiniz.  

 Paylaşılan bir dağıtım noktasının ikincil bir site sunucusuna yükseltilmesi işlemi, diğer tüm paylaşılan dağıtım noktası yükseltmesiyle aynıdır. İçerik kopyalanır ve hedef hiyerarşisi tarafından kullanılan tek örnek deposuna dönüştürülür. Ancak, ikincil bir site sunucusunda bulunan paylaşılan bir dağıtım noktasını yükselttiğinizde, yükseltme işlemi yönetim noktasını da kaldırır (varsa) ve ardından ikincil siteyi sunucudan kaldırır. Sonuç, İkincil sitenin Configuration Manager 2007 hiyerarşisinden kaldırılmasına neden olur. İkincil siteyi kaldırmak için Configuration Manager, kaynak siteden veri toplamak üzere ayarlanmış olan hesabı kullanır.  

 Yükseltme sırasında, Configuration Manager 2007 ikincil sitesinin kaldırılması ve hedef hiyerarşideki dağıtım noktasının yüklenmesi başladığında bir gecikme vardır. Veri toplama çevrimi, bu gecikmeyi dört saate kadar belirler. Gecikme, yeni dağıtım noktası yüklemesi başlamadan önce ikincil sitenin kaldırılması için zaman sağlamaya yöneliktir.  

 Paylaşılan bir dağıtım noktasını yükseltme hakkında daha fazla bilgi için bkz. [Configuration Manager 2007 paylaşılan dağıtım noktasını yükseltmeyi planlayın](#Planning_to_Upgrade_DPs).  

##  <a name="plan-to-reassign-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a>Configuration Manager dağıtım noktalarını yeniden atamayı planlayın  
 System Center 2012 Configuration Manager desteklenen bir sürümünden aynı sürümdeki bir hiyerarşiye geçiş yaptığınızda, paylaşılan bir dağıtım noktasını kaynak hiyerarşisinden hedef hiyerarşisindeki bir siteye yeniden atayabilirsiniz. Bu, Configuration Manager 2007 dağıtım noktasını hedef hiyerarşisinde bir dağıtım noktası olmak üzere yükseltme kavramı gibidir. Dağıtım noktalarını birincil sitelerden ve ikincil sitelerden yeniden atayabilirsiniz. Bir dağıtım noktasını yeniden atama eylemi, dağıtım noktasını kaynak hiyerarşiden kaldırır ve bilgisayarı ve dağıtım noktasını hedef hiyerarşisinde seçtiğiniz sitenin site sistem sunucusu olur.  

 Bir dağıtım noktasını yeniden atadığınızda, kaynak site dağıtım noktasında barındırılan geçişi yapılmış içeriği yeniden dağıtmanıza gerek yoktur. Ayrıca, bir Configuration Manager 2007 dağıtım noktasının yükseltilmesinden farklı olarak, dağıtım noktasının yeniden atanması dağıtım noktası bilgisayarında ek disk alanı gerektirmez. Bunun nedeni System Center 2012 Configuration Manager başlangıcından itibaren dağıtım noktalarının içerik için tek örnek depo biçimini kullanması. Dağıtım noktası hiyerarşiler arasında yeniden atandığında, dağıtım noktası bilgisayarındaki içeriğin dönüştürülmesine gerek yoktur.  

 Bir System Center 2012 Configuration Manager dağıtım noktasının yeniden atamaya uygun olması için, aşağıdaki ölçütleri karşılaması gerekir:  

-   Paylaşılan bir dağıtım noktası site sunucusundan farklı bir bilgisayara yüklenmiş olmalıdır.  

-   Paylaşılan dağıtım noktası, ek site sistem rolleriyle birlikte bulundurulamaz.  

**Kaynak hiyerarşisi** düğümünde Configuration Manager konsolunda yeniden atamaya uygun olan dağıtım noktalarını tanımlamak için bir kaynak site seçin ve ardından **paylaşılan dağıtım noktaları** sekmesini seçin. uygun dağıtım noktaları yeniden **atama için uygun** sütununda **Evet** olarak görüntülenir (Bu sütun System Center 2012 R2 Configuration Manager öncesinde **yükseltme için uygun** olarak adlandırılır).  

###  <a name="distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> Dağıtım noktası yeniden atama işlemi  
 Etkin bir kaynak hiyerarşisinden paylaştığınız dağıtım noktalarını yeniden atamak için Configuration Manager konsolunu kullanabilirsiniz. Paylaşılan bir dağıtım noktasını yeniden atadığınızda, dağıtım noktası kaynak sitesinden kaldırılır ve ardından hedef hiyerarşisinde belirttiğiniz birincil veya ikincil bir siteye bağlı bir dağıtım noktası olarak yüklenir.  

 Dağıtım noktasını yeniden atamak için, hedef hiyerarşisi kaynak sitenin SMS sağlayıcısından veri toplamak üzere ayarlanan kaynak site erişim hesabını kullanır. Gerekli izinler ve ek ön koşullar hakkında daha fazla bilgi için bkz. [geçiş önkoşulları](../../core/migration/prerequisites-for-migration.md).  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Birden çok paylaşılan dağıtım noktasını aynı anda geçirme
Sürüm 1610 ' den başlayarak, aynı anda en fazla 50 paylaşılan dağıtım noktasını paralel olarak Configuration Manager işlem yapmak için **dağıtım noktasını yeniden ata** ' yı kullanabilirsiniz. Bu, çalıştırılan desteklenen kaynak sitelerden paylaşılan dağıtım noktalarını içerir:  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- Configuration Manager (geçerli dal)

Dağıtım noktalarını yeniden atadığınızda, her bir dağıtım noktasının yükseltilmesi ya da yeniden atanması için uygun olması gerekir. Eylem ve işlem (yükseltme veya yeniden atama) dahil olmak üzere, kaynak sitenin hangi Configuration Manager sürümüne göre çalışır. Her iki eylemin de nihai sonuçları aynıdır: dağıtım noktası, içerik yerinde olan Güncel Dalı sitelerinizden birine atanır.

Sürüm 1610 ' den önce, Configuration Manager tek seferde yalnızca bir dağıtım noktasını işleyebilir. Artık aşağıdaki uyarılarla istediğiniz sayıda dağıtım noktası atayabilirsiniz:  
- Dağıtım noktalarını yeniden atamak için çoklu seçim yapamasanız da, birden fazla sıraya alınmışsa Configuration Manager, bir sonraki başlatmadan önce bir tane tamamlanmasını beklemek yerine, bu işlemleri paralel olarak işler.  
- Varsayılan olarak, en fazla 50 dağıtım noktası paralel olarak aynı anda işlenir. İlk dağıtım noktasının yeniden atanması bittikten sonra, Configuration Manager 5 1 ' i işlemeye başlar ve bu şekilde devam eder.  
- Configuration Manager SDK 'sını kullandığınızda **Shareddpımportthreadlimit** ' i değiştirerek Configuration Manager paralel olarak işleyebilmeleri için yeniden atanan dağıtım noktalarının sayısını ayarlayabilirsiniz.


##  <a name="assign-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a>İçerik geçişi sırasında içerik sahipliği atama  
 Dağıtım için içerik geçişi yaparken, içerik nesnesini hedef hiyerarşisindeki bir siteye atamanız gerekir. Böylece bu site hedef hiyerarşisinde o içeriğin sahibi olur. Hedef hiyerarşinizin en üst düzey sitesi, içerik için meta verileri geçirirken site olsa da, ağ genelindeki içerik için özgün kaynak dosyalarını kullanan atanan sitedir.  

 İçerik geçişi sırasında kullanılan ağ bant genişliğini minimuma indirmek için, içeriğin sahipliğini ağda kaynak hiyerarşisindeki içerik konumuna yakın bir hedef hiyerarşisi sitesine transfer etmeyi göz önünde bulundurun. Hedef hiyerarşisindeki içerik hakkındaki bilgiler global olarak paylaşıldığı için, tüm sitelerde kullanılabilir olacaktır.  

 İçerik hakkındaki bilgiler, veritabanı çoğaltma kullanılarak tüm sitelerle paylaşılsa da, birincil siteye atadığınız ve ardından diğer birincil sitelerdeki dağıtım noktalarına dağıttığınız tüm içerikler dosya tabanlı çoğaltmaya göre aktarım yapar. Bu aktarma, merkezi yönetim sitesi aracılığıyla ve ardından ek birincil siteye yönlendirilir. Bir siteyi içerik sahibi olarak atadığınızda, geçiş sırasında birden fazla birincil siteye dağıtmayı planladığınız paketleri merkezileştirerek, düşük bant genişlikli ağlarda veri aktarımını azaltabilirsiniz.
