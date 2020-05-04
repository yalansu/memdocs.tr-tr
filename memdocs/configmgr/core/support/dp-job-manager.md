---
title: DP İş Kuyruğu Yöneticisi
titleSuffix: Configuration Manager
description: Dağıtım noktalarını Configuration Manager için içerik dağıtım işlerini sorunlarını gidermek ve yönetmek için DP Iş kuyruğu yöneticisini kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713663"
---
# <a name="dp-job-queue-manager"></a>DP İş Kuyruğu Yöneticisi

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Dağıtım noktası (DP) Iş kuyruğu Yöneticisi [Configuration Manager araçlarından](tools.md)biridir. Dağıtım noktalarını Configuration Manager için devam eden içerik dağıtım işlerini sorunlarını gidermek ve yönetmek için kullanın. 

Araç, Paket Aktarma Yöneticisi bileşeninin kuyruğunda sahip olduğu işlerin listesini görüntüler. Ayrıca işlerin durumunu gösterir: yürütülene, çalıştırmaya veya yeniden denemeye hazırlanıyor. Kuyruktaki işleri değiştirmenize, listedeki işleri daha üst düzeye taşımanıza, bir işi iptal etmenize veya bir işi çalıştırmaya el ile başlayabilmenizi sağlar.

Ayrıca, dağıtım noktasının bir işi çalıştırdığı site sunucusundan bilgi alır. Araç sağlayıcı aracılığıyla site sunucusuna bağlanır. Bu bilgileri toplamak için her uzak dağıtım noktasına bağlanmaz. Eylemleri tetiklediği ve sağlayıcı aracılığıyla bilgi aldığından, uzak dağıtım noktalarından değişiklikleri yansıtmada bir gecikme vardır.



## <a name="usage"></a>Kullanım

**Dpjobmgr. exe dosyasını**çalıştırın. Aracının ana menüsü aşağıdaki sekmeleri içerir: 

- [Bağlan](#bkmk_connect): birincil site sunucusuna ilk bağlantıyı oluşturma  

- [Genel bakış](#bkmk_overview): tüm dağıtım noktalarında çalışan tüm işleri tek bir görünümde özetler  

- [Dağıtım noktası bilgisi](#bkmk_dp-info): bunları izlemek için çoklu seçim dağıtım noktaları ve tek bir ilgilendiğiniz işi yönetin  

- [Işleri yönetme](#bkmk_manage-jobs): tek bir düz görünümde tüm işlerin ve bunların durumlarının bir listesini gösterir. İşleri işleme, onları taşıma, iptal etme veya el ile başlatma.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Bağlan sekmesi

Birincil site sunucusuna ilk bağlantıyı kurmak için bu sekmeyi kullanın. Şu anda oturum açmış olan kullanıcının kimlik bilgilerini kullanır. Merkezi yönetim sitesine veya ikincil sitelere bağlanamazsınız. Bağlantı, **tam yönetici** güvenlik rolünü gerektirir.

Araç başarılı bir şekilde bağlantı kurduktan sonra, aracın alt kısmındaki bir bildirim site sunucusuna bağlı olduğunu onaylar. 


### <a name="overview-tab"></a><a name="bkmk_overview"></a>Genel Bakış sekmesi

Tüm dağıtım noktalarında tüm işlerin özetini gösterir. Aşağıdaki sütunlara bakın:  

- **Dağıtım noktası**: dağıtım noktalarının adlarını listeler  

- **Çalışan işler**: belirli bir dağıtım noktasında çalışan eşzamanlı işlerin sayısını gösterir.  

    > [!Tip]  
    > Eşzamanlı yazılım dağıtımları sayısı bir site ayarıdır. Bu ayar, yazılım dağıtım bileşeni özelliklerinde değiştirildi.  

- **Toplam iş**: belirli bir dağıtım noktasına hedeflenen tüm işlerin sayısını gösterir. Bu sayı, çalıştıran, yeniden denenen veya yürütülmesi bekleyen işleri içerir.  

- **Toplam yeniden deneme**sayısı: belirli bir dağıtım noktasındaki işlerin kaç kez yeniden denenme sayısını gösterir. Daha yüksek bir sayı söz konusu dağıtım noktasındaki genel bir sorunu temsil edebilir.  


> [!Tip]  
> - Bu sekmedeki her bir sütunu sıralamak için sütun adına tıklayın  
> 
> - **Yenile** ' ye tıklayarak bu sekmedeki bilgileri el ile yenileyin  
> 
> - Otomatik **yenilemeyi Başlat** ' a tıklayıp otomatik yenileme aralığını ayarlayarak bu sekmedeki bilgileri otomatik olarak yenileyin. Varsayılan yenileme aralığı iki dakikadır.  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a>Dağıtım noktası bilgisi sekmesi

Bağlı site altındaki tüm dağıtım noktalarının listesini gösterir. Sol taraftaki bölmede tüm dağıtım noktaları listelenir. **Tümünü Seç** veya gerekli **Tüm Seçimleri Kaldır** ' a tıklayın veya bu listede belirli dağıtım noktalarını çoklu seçin. Sağ taraftaki bölmede, seçili dağıtım noktaları için işler gösterilir.

Sekiz sütun vardır:  

- **Durum simgesi**: üç olası durum simgesi vardır:  

    - **Ready**: belirli bir işin tüm doğrulama adımlarını tamamladığını gösterir. Çalışan eşzamanlı işlere eklenmeye hazırlanıyor. Bu durumdaki işler genellikle bekleme aşamasıdır. Bunlar için, geçerli çalışan işlemlerin bitmesini bekler ve bu işlem için bir alan açın.  

    - **Çalışıyor**: belirli bir işin bir dağıtım noktasında çalışmakta olduğunu gösterir. Uzun süre çalışan işler (büyük paketler) için genellikle ilerlemeyi alma zamanı (%) tamamlama doğru. Bu, bu görünümün **ilerleme** sütununda bu yüzdeyi gösterir. Küçük paketler için, **ilerleme** sütunu boş kalabilir. İş, uzak dağıtım noktasından durumu aldığı zaman tarafından zaten tamamlanmış olabilir.  

    - **Yeniden deneme**: belirli bir işin başarısız olduğunu ve şimdi yeniden deneme durumunda olduğunu gösterir. Bu iş, yeniden deneme aralığından sonra yeniden denenir. Bu Aralık yapılandırılabilir ve varsayılan olarak 30 dakikaya ayarlanır.  

- **Yazılım**: belirli bir dağıtım noktasını hedefleyen paketin adı  

- **Paket kimliği**: belirli bir dağıtım noktasına hedeflenen PAKETIN paket kimliği  

- **Boyut**: KB cinsinden paket boyutu  

- **İlerleme**: iş tamamlanma yüzdesi. Daha fazla bilgi için bkz. **çalışma** durumu simgesi açıklaması.  

- **Başlangıç/yeniden başlatma zamanı**: çalışan bir iş için, bu değer başlangıç saati (yeşil). Bir yeniden deneme işi için, bu değer işi yeniden deneeceği süredir.  

- **Yeniden denemeler**: Bu paketi yeniden deneme sayısı.  

- **Dağıtım noktası adı**: dağıtım noktasının tam etki alanı adı (FQDN)  

> [!Tip]  
> - Bu sekmedeki her bir sütunu sıralamak için sütun adına tıklayın  
> 
> - **Yenile** ' ye tıklayarak bu sekmedeki bilgileri el ile yenileyin  
> 
> - Otomatik **yenilemeyi Başlat** ' a tıklayıp otomatik yenileme aralığını ayarlayarak bu sekmedeki bilgileri otomatik olarak yenileyin. Varsayılan yenileme aralığı iki dakikadır.  
> 
> - Belirli bir işi değiştirmeniz gerekiyorsa, bu görünümdeki işe sağ tıklayın ve **Işi Yönet**' i seçin. Bu eylem [Işleri Yönet sekmesini](#bkmk_manage-jobs)açar.  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a>Işleri yönetme sekmesi

Tek bir düz görünümde tüm işlerin ve bunların durumlarının bir listesini gösterir. [Dağıtım noktası bilgileri sekmesiyle](#bkmk_dp-info)aynı sekiz sütunu içerir. Bu görünümde, aşağıdaki eylemler için işlere sağ tıklayın:  

- **Çalıştır**: çalıştırılenden farklı bir durumda olan bir işi başlatır  

- **En üste taşı**: bir veya daha fazla işi sıranın en üstüne taşır. Bu eylem, işlerin hemen çalıştırılmasına neden olabilir. Bu eylem nedeniyle daha düşük bir öncelik işi duraklatılamayabilir.  

- **Yukarı taşı**: belirli bir işi yukarıdaki bir satır taşır. Bu eylem nedeniyle daha düşük bir öncelik işi çalışmayı duraklatabilir.  

- **Aşağı taşı**: belirli bir işi aşağıda bir satır taşır.  

- **En alta taşı**: bir veya daha fazla işi sıranın en altına taşır.  

    > [!Tip]  
    > Taşımak için listedeki işleri sürükleyip bırakın.  

- **İptal**: bir veya daha fazla işi iptal etmeyi dener.  

    > [!Note]  
    > Son tamamlanma zamanına yakın işleri iptal edemezsiniz. Site sunucusu aynı zamanda bir dağıtım noktası ise, site sunucusundaki işleri iptal edemezsiniz.  



## <a name="see-also"></a>Ayrıca bkz.

- [İçerik yönetimi için temel kavramlar](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Paket Aktarma Yöneticisi](../plan-design/hierarchy/package-transfer-manager.md)
