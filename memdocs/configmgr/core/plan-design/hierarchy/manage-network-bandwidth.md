---
title: İçerik için ağ bant genişliğini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager için zamanlamayı, azaltmayı ve önceden hazırlanan içeriği yapılandırın.
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8ee7d00f3b5c98528d9999b83b07aa393b72e36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720593"
---
# <a name="manage-network-bandwidth-for-content"></a>İçerik için ağ bant genişliğini yönetme
Configuration Manager içerik yönetimi işlemi için kullanılan ağ bant genişliğini yönetmenize yardımcı olmak için, zamanlama ve azaltma için yerleşik denetimleri kullanabilirsiniz. Önceden hazırlanan içerik de kullanabilirsiniz. Aşağıdaki bölümlerde bu seçenekler daha ayrıntılı olarak açıklanır.

##  <a name="scheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Zamanlama ve daraltma  

 Bir paket oluşturduğunuzda, içerik için kaynak yolunu değiştirdiğinizde veya dağıtım noktasındaki içeriği güncelleştirdiğinizde, dosyalar kaynak yolundan site sunucusundaki içerik kitaplığına kopyalanır. Daha sonra içerik, site sunucusundaki içerik kitaplığından dağıtım noktalarındaki içerik kitaplığına kopyalanır. İçerik kaynak dosyaları güncelleştirilirken ve kaynak dosyalar zaten dağıtıldığında, Configuration Manager yalnızca yeni veya güncelleştirilmiş dosyaları alır ve bunları dağıtım noktasına gönderir.

 Siteden siteye iletişim için zamanlama ve azaltma denetimlerini, site sunucusu ile uzak dağıtım noktası arasındaki iletişimi de kullanabilirsiniz. Zamanlama ve daraltma denetimlerini ayarladıktan sonra bile ağ bant genişliği sınırlıysa, dağıtım noktasındaki içeriği önceden hazırlamayı düşünebilirsiniz.  

 Configuration Manager, bir zamanlama ayarlayabilir ve içerik dağıtımının ne zaman ve nasıl gerçekleştirileceğini belirleyen uzak dağıtım noktalarında daraltma ayarlarını belirtebilirsiniz. Her uzak dağıtım noktası, site sunucusundan uzak dağıtım noktasına ağ bant genişliği sınırlamalarını ele almak için farklı yapılandırmalara sahip olabilir. Uzak dağıtım noktasına zamanlama ve daraltma denetimleri, standart gönderici adresi ayarlarına benzerdir. Bu durumda, ayarlar Paket Aktarma Yöneticisi olarak adlandırılan yeni bir bileşen tarafından kullanılır.

 Paket Aktarma Yöneticisi, bir site sunucusundan, birincil site veya ikincil site olarak bir site sistemine yüklenen bir dağıtım noktasına içerik dağıtır. Daraltma ayarları **hız sınırları** sekmesinde belirtilir ve zamanlama ayarları, site sunucusunda olmayan bir dağıtım noktası için **zamanlama** sekmesinde belirtilir. Zaman ayarları dağıtım noktasından değil, gönderen sitenin saat dilimini temel alır.  

> [!IMPORTANT]  
>  **Oran limitleri** ve **zamanlama** sekmeleri yalnızca bir site sunucusunda yüklü olmayan dağıtım noktaları için özelliklerde görüntülenir.  

Daha fazla bilgi için bkz. [Configuration Manager dağıtım noktalarını yükleyip yapılandırma](../../servers/deploy/configure/install-and-configure-distribution-points.md).  

##  <a name="prestaged-content"></a><a name="BKMK_PrestagingContent"></a>Önceden hazırlanan içerik  
 İçeriği dağıtmadan önce içerik dosyalarını bir site sunucusundaki veya dağıtım noktasındaki içerik kitaplığına eklemek için içeriği önceden hazırlayabilirsiniz. İçerik dosyaları zaten içerik kitaplığında olduğundan, içeriği dağıttığınızda ağ üzerinden aktarılmaz. Uygulamalar ve paketler için içerik dosyalarını önceden hazırlayabilirsiniz.  

Configuration Manager konsolunda, önceden hazırlamak istediğiniz içeriği seçin ve ardından **önceden hazırlanan Içerik dosyası oluşturma Sihirbazı**' nı kullanın. Bu, içerik için dosyaları ve ilişkili meta verileri içeren sıkıştırılmış, önceden hazırlanmış bir içerik dosyası oluşturur. Daha sonra, bir site sunucusundaki veya dağıtım noktasındaki içeriği elle içeri aktarabilirsiniz. Aşağıdaki noktalara dikkat edin:  

-   Önceden hazırlanan içerik dosyasını bir site sunucusuna aktardığınızda, içerik dosyaları site sunucusundaki içerik kitaplığına eklenir ve ardından site sunucusu veritabanına kaydedilir.  

-   Önceden hazırlanan içerik dosyasını bir dağıtım noktasına aktardığınızda, içerik dosyaları dağıtım noktasındaki içerik kitaplığına eklenir. Site sunucusuna, içeriğin dağıtım noktasında kullanılabilir olduğunu bildiren bir durum iletisi gönderilir.  

Dağıtım noktasını, içerik dağıtımını yönetmeye yardımcı olmak için, isteğe bağlı olarak **önceden hazırlanmış** olarak yapılandırabilirsiniz. Ardından, içeriği dağıttığınızda şunları yapmak isteyip istemediğinizi seçebilirsiniz:  

-   Dağıtım noktasındaki içeriği her zaman önceden hazırlama.  

-   Paketin ilk içeriğini önceden hazırlama ve sonra içerikte güncelleştirmeler varken standart içerik dağıtım sürecini kullanın.  

-   Paketteki içerik için her zaman standart içerik dağıtım işlemini kullanın.  

###  <a name="determine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>İçeriğin önceden hazırlanıp hazırlanmayacağını belirleme  
 Aşağıdaki senaryolarda uygulamalar ve paketler için içeriği önceden hazırlamayı göz önünde bulundurun:  

-   **Site sunucusundan bir dağıtım noktasına sınırlı ağ bant genişliği sorununu gidermek için.** Zamanlama ve azaltma, bant genişliği hakkındaki kaygılarınızı karşılamak için yeterli değilse dağıtım noktasındaki içeriği önceden hazırlamayı göz önünde bulundurun. Her dağıtım noktası, dağıtım noktası özelliklerinde seçebileceğiniz **önceden hazırlanan içerik için bu dağıtım noktasını etkinleştir** ayarını içerir. Bu seçeneği etkinleştirdiğinizde, dağıtım noktası önceden hazırlanmış bir dağıtım noktası olarak tanımlanır ve içeriği paket başına temelinde nasıl yönetebileceğinizi seçebilirsiniz.  

    Aşağıdaki ayarlar bir uygulama, paket, sürücü paketi, önyükleme görüntüsü, işletim sistemi yükleyicisi ve görüntü için özelliklerde mevcuttur. Bu ayarlar, içerik dağıtımının önceden hazırlanan olarak tanımlanan uzak dağıtım noktalarında nasıl yönetileceğini seçmenizi sağlar:  

    -   **Paketler dağıtım noktalarına atandığında Içeriği otomatik olarak indir**: Bu seçeneği, daha küçük paketleriniz olduğunda kullanın ve zamanlama ve daraltma ayarları, içerik dağıtımı için yeterli denetim sağlar.  

    -   **Yalnızca dağıtım noktasındaki içerik değişikliklerini indir**: paketteki içerik için gelecekteki güncelleştirmelerin ilk paketten genellikle daha küçük olması için bu seçeneği kullanın. Örneğin, ilk paket boyutu 700 MB 'ın üzerinde olduğundan ve ağ üzerinden gönderilemeyecek kadar büyük olduğundan, Microsoft Office gibi bir uygulamayı önceden hazırlayabilirsiniz. Ancak, bu paketteki içerik güncelleştirmeleri 10 MB 'tan az olabilir ve ağ üzerinden dağıtmak için kabul edilebilir. Diğer bir örnek, ilk paket boyutunun büyük olduğu, ancak pakete artımlı sürücü eklemeleri küçük olabilecek sürücü paketleri olabilir.  

    -   **Bu paketteki içeriği dağıtım noktasına el ile Kopyala**: Bu seçeneği, işletim sistemi gibi içeriklere sahip olan büyük Paketleriniz varsa ve içeriği dağıtım noktasına dağıtmak için hiçbir zaman ağı kullanmak istemediğinizde kullanın. Bu seçeneği belirlediğinizde dağıtım noktasındaki içeriği önceden hazırlamanız gerekir.  

    > [!IMPORTANT]  
    >  Yukarıdaki seçenekler, paket başına temelinde geçerlidir ve yalnızca bir dağıtım noktası önceden hazırlanmış olarak tanımlandığında kullanılır. Önceden hazırlanmış olarak tanımlanmayan dağıtım noktaları bu ayarları yoksayar. Bu durumda, içerik her zaman site sunucusundan dağıtım noktalarına ağ üzerinden dağıtılır.  

-   **İçerik kitaplığını bir site sunucusuna geri yüklemek için.** Bir site sunucusu başarısız olduğunda, içerik kitaplığında bulunan paketler ve uygulamalar hakkında bilgiler geri yükleme işleminin bir parçası olarak site veritabanına geri yüklenir, ancak içerik kitaplığı dosyaları işlemin bir parçası olarak geri yüklenmez. İçerik kitaplığını geri yüklemek için bir dosya sistemi yedeğiniz yoksa, sahip olmanız gereken paketleri ve uygulamaları içeren başka bir siteden önceden hazırlanan bir içerik dosyası oluşturabilirsiniz. Daha sonra, kurtarılan site sunucusunda önceden hazırlanan içerik dosyasını ayıklayabilirsiniz. Site sunucusu yedekleme ve kurtarma hakkında daha fazla bilgi için bkz. [Configuration Manager Için Yedekleme ve kurtarma](../../servers/manage/backup-and-recovery.md).  
