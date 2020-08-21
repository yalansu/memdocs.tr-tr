---
title: '& Monitor aşamalı dağıtımlarını yönetme'
titleSuffix: Configuration Manager
description: Configuration Manager 'de yazılım için aşamalı dağıtımları yönetmeyi ve izlemeyi öğrenin.
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efc43258e65752e7371c9baadf61598aac820062
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698002"
---
# <a name="manage-and-monitor-phased-deployments"></a>Aşamalı dağıtım izleme ve yönetme

Bu makalede, aşamalı dağıtımları yönetme ve izleme işlemlerinin nasıl yapılacağı açıklanır. Yönetim görevleri bir sonraki aşamayı el ile başlatmak ve bir aşamayı askıya almak ya da sürdürmeyi içerir. 

İlk olarak, aşamalı bir dağıtım oluşturmanız gerekir: 
- [Uygulama](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  
- [Yazılım güncelleştirmesi](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Görev dizisi](create-phased-deployment-for-task-sequence.md)  



## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> Sonraki aşamaya geçin

Ayarı seçtiğinizde, **dağıtımın ikinci aşamasını el ile**başlatırsanız, site başarı ölçütlerine bağlı olarak bir sonraki aşamayı otomatik olarak başlamaz. Aşamalı dağıtımı sonraki aşamaya taşımanız gerekir.  

1. Bu eylemi başlatmak dağıtılan yazılımın türüne göre farklılık gösterir:  

    - **Uygulama** (yalnızca sürüm 1806 veya üzeri): **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar**' ı seçin.   

    - **Yazılım güncelleştirmesi** (yalnızca sürüm 1810 veya üzeri sürümlerde): **yazılım kitaplığı** çalışma alanına gidin ve aşağıdaki düğümlerden birini seçin:    
        - Yazılım Güncelleştirmeleri  
            - **Tüm yazılım güncelleştirmeleri**  
            - **Yazılım güncelleştirme grupları**   
        - Windows 10 bakımı, **tüm Windows 10 güncelleştirmeleri**  
        - Office 365 Istemci yönetimi, **office 365 güncelleştirmeleri**  

    - **Görev sırası**: **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin.   

2. Aşamalı dağıtıma sahip yazılımı seçin.  

3. Ayrıntılar bölmesinde, **aşamalı dağıtımlar** sekmesine geçin.  

4. Aşamalı dağıtımı seçin ve Şeritteki **sonraki aşamaya taşı** ' ya tıklayın.  

    ![Aşamalı dağıtımda eylemleri gösteren menü sağ tıklama](media/Suspend-phased-deployment.PNG)



## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Askıya alma ve özgeçmişler 

Aşamalı bir dağıtımı el ile askıya alabilir veya sürdürebilirsiniz. Örneğin, bir görev dizisi için aşamalı dağıtım oluşturursunuz. Pilot grubunuza yönelik aşamayı izlerken çok sayıda başarısızlık fark edersiniz. Başka cihazların görev dizisini çalıştırmasını durdurmak için aşamalı dağıtımı askıya alın. Sorunu çözdükten sonra, piyasaya çıkmaya devam etmek için aşamalı dağıtımı sürdürmeniz gerekir. 

1. Bu eylemi başlatmak dağıtılan yazılımın türüne göre farklılık gösterir:  

    - **Uygulama** (yalnızca sürüm 1806 veya üzeri): **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar**' ı seçin.   

    - **Yazılım güncelleştirmesi** (yalnızca sürüm 1810 veya üzeri sürümlerde): **yazılım kitaplığı** çalışma alanına gidin ve aşağıdaki düğümlerden birini seçin:    
        - Yazılım Güncelleştirmeleri  
            - **Tüm yazılım güncelleştirmeleri**  
            - **Yazılım güncelleştirme grupları**   
        - Windows 10 bakımı, **tüm Windows 10 güncelleştirmeleri**  
        - Office 365 Istemci yönetimi, **office 365 güncelleştirmeleri**  

    - **Görev sırası**: **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **görev dizileri**' ni seçin. Var olan bir görev dizisini seçin ve ardından şeritte **aşamalı dağıtım oluştur** ' a tıklayın.  

2. Aşamalı dağıtıma sahip yazılımı seçin.  

3. Ayrıntılar bölmesinde, **aşamalı dağıtımlar** sekmesine geçin.  

4. Aşamalı dağıtımı seçin ve şeritte **askıya al** veya geri **et** ' e tıklayın. 

> [!NOTE]
> 21 Nisan 2020 ' den itibaren Office 365 ProPlus, **Enterprise için Microsoft 365 uygulamalar**olarak yeniden adlandırıldı. Daha fazla bilgi için bkz. [Office 365 ProPlus Için ad değiştirme](/deployoffice/name-change). Konsol güncelleştirilirken Configuration Manager üründe ve belgelerde eski adı görmeye devam edebilirsiniz. 

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="monitor"></a><a name="bkmk_monitor"></a> İzleyicisi
<!--1358577-->
Sürüm 1902 ' den başlayarak, aşamalı dağıtımlar kendi adanmış izleme düğümüne sahiptir ve oluşturduğunuz aşamalı dağıtımları tanımlamanızı ve aşamalı dağıtım izleme görünümüne gitmelerini kolaylaştırır. **İzleme** çalışma alanından **aşamalı dağıtımlar**' ı seçin ve ardından durumu görmek için aşamalı dağıtımlardan birine çift tıklayın. <!--3555949-->

Configuration Manager 1806 ve 1810 ' de, aşamalı dağıtımlar için yerel izleme deneyimini görebilirsiniz. **İzleme** çalışma alanındaki **dağıtımlar** düğümünden aşamalı bir dağıtım seçin ve ardından şeritte **aşamalı dağıtım durumu** ' nu tıklatın.

![İki aşamaların durumunu gösteren aşamalı dağıtım durumu panosu](media/1358577-phased-deployment-status.png)

Bu Pano, dağıtımdaki her aşama için aşağıdaki bilgileri gösterir:  

- **Toplam cihaz** veya **Toplam kaynak**: Bu aşamada kaç cihaz hedeflenmiştir.  

- **Durum**: Bu aşamanın geçerli durumu. Her aşama aşağıdaki durumlardan birinde olabilir:  

    - **Dağıtım oluşturuldu**: aşamalı dağıtım, bu aşama için, yazılımın koleksiyona bir dağıtımını oluşturdu. İstemciler bu yazılımla etkin bir şekilde hedeflenmiştir.  

    - **Bekliyor**: önceki aşama, bu aşamaya devam etmek için dağıtımın başarı ölçütlerine henüz ulaşmadı.  

    - **Askıya alındı**: yönetici dağıtımı askıya aldı.  

- **İlerleme**: istemcilerden renk kodlu dağıtım durumları. Örneğin: başarılı, devam ediyor, hata, gereksinimler karşılanmadı ve bilinmiyor. 

#### <a name="success-criteria-tile"></a>Başarı ölçütleri kutucuğu

**Başarı ölçütleri** kutucuğunun görüntüsünü değiştirmek Için **Aşama Seç** açılan listesini kullanın. Bu kutucuk, **aşamanın hedefini** dağıtımın geçerli uyumluluğuyla karşılaştırır. Varsayılan ayarlarla, aşama hedefi %95 ' dir. Bu değer, dağıtımın bir sonraki aşamaya geçmek için %95 uyumluluğa sahip olması gerektiği anlamına gelir.

Örnekte, aşama hedefi %65 ve geçerli uyumluluk% 66,7 ' dir. Aşamalı dağıtım, ilk aşama başarı ölçütlerini karşıladığı için otomatik olarak ikinci aşamaya taşınır.  

   ![Hedefin %65 olduğu aşamalı dağıtım durumundan örnek başarı ölçütleri kutucuğu](media/pod-status-success-criteria-tile.png)

Aşama hedefi, *sonraki* aşama Için aşama ayarlarındaki **dağıtım başarı yüzdesi** ile aynıdır. Aşamalı dağıtımın sonraki aşamayı başlatması için, bu ikinci aşama ilk aşamanın başarısı için kriterleri tanımlar. Bu ayarı görüntülemek için: 

1. Yazılımdaki aşamalı dağıtım nesnesine gidin ve aşamalı dağıtım özelliklerini açın.  

2. **Aşamalar** sekmesine geçin. **aşama 2** ' yi seçin ve **görüntüle**' ye tıklayın.  

3. Aşama Özellikler penceresi, **aşama ayarları** sekmesine geçin.  

4. *Önceki aşama grubunun başarısı Için ölçütteki* **dağıtım başarısı yüzdesi** değerini görüntüleyin.  

Örneğin, aşağıdaki özellikler, yukarıdaki %65 ' de gösterilen başarı ölçütü kutucuğu ile aynı aşamada verilmiştir:  
![Aşama özelliklerindeki aşama ayarları sekmesi](media/phase-properties-phase-settings.png)