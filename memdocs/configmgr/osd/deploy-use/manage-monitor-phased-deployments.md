---
title: '& Monitor aşamalı dağıtımlarını yönetme'
titleSuffix: Configuration Manager
description: Configuration Manager 'de yazılım için aşamalı dağıtımları yönetmeyi ve izlemeyi öğrenin.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7295e6f74764b378be8315599357424cbf6ead73
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820417"
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

    - **Uygulama**: **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar**' ı seçin.

    - **Yazılım güncelleştirmesi**: **yazılım kitaplığı** çalışma alanına gidin ve aşağıdaki düğümlerden birini seçin:
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

Sürüm 2002 ' den başlayarak, bu görev için aşağıdaki Windows PowerShell cmdlet 'ini kullanın: [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext?view=sccm-ps).

## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Askıya alma ve özgeçmişler

Aşamalı bir dağıtımı el ile askıya alabilir veya sürdürebilirsiniz. Örneğin, bir görev dizisi için aşamalı dağıtım oluşturursunuz. Pilot grubunuza yönelik aşamayı izlerken çok sayıda başarısızlık fark edersiniz. Başka cihazların görev dizisini çalıştırmasını durdurmak için aşamalı dağıtımı askıya alın. Sorunu çözdükten sonra, piyasaya çıkmaya devam etmek için aşamalı dağıtımı sürdürmeniz gerekir.

1. Bu eylemi başlatmak dağıtılan yazılımın türüne göre farklılık gösterir:  

    - **Uygulama**: **yazılım kitaplığı** çalışma alanına gidin, **uygulama yönetimi**' ni genişletin ve **uygulamalar**' ı seçin.

    - **Yazılım güncelleştirmesi**: **yazılım kitaplığı** çalışma alanına gidin ve aşağıdaki düğümlerden birini seçin:
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

Sürüm 2002 ' den başlayarak, bu görev için aşağıdaki Windows PowerShell cmdlet 'lerini kullanın:

- [Askıya al-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment?view=sccm-ps)
- [Özgeçmişi-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment?view=sccm-ps)

## <a name="monitor"></a><a name="bkmk_monitor"></a> İzleyicisi
<!--1358577-->

Aşamalı dağıtımlar kendi adanmış izleme düğümüne sahiptir ve oluşturduğunuz aşamalı dağıtımları belirlemeyi kolaylaştırır ve aşamalı dağıtım izleme görünümüne gidin. **İzleme** çalışma alanından **aşamalı dağıtımlar**' ı seçin ve ardından durumu görmek için aşamalı dağıtımlardan birine çift tıklayın. <!--3555949-->

![İki aşamaların durumunu gösteren aşamalı dağıtım durumu panosu](media/1358577-phased-deployment-status.png)

Bu Pano, dağıtımdaki her aşama için aşağıdaki bilgileri gösterir:  

- **Toplam cihaz** veya **Toplam kaynak**: Bu aşamada kaç cihaz hedeflenmiştir.  

- **Durum**: Bu aşamanın geçerli durumu. Her aşama aşağıdaki durumlardan birinde olabilir:  

  - **Dağıtım oluşturuldu**: aşamalı dağıtım, bu aşama için, yazılımın koleksiyona bir dağıtımını oluşturdu. İstemciler bu yazılımla etkin bir şekilde hedeflenmiştir.  

  - **Bekliyor**: önceki aşama, bu aşamaya devam etmek için dağıtımın başarı ölçütlerine henüz ulaşmadı.  

  - **Askıya alındı**: yönetici dağıtımı askıya aldı.  

- **İlerleme**: istemcilerden renk kodlu dağıtım durumları. Örneğin: başarılı, devam ediyor, hata, gereksinimler karşılanmadı ve bilinmiyor.

### <a name="success-criteria-tile"></a>Başarı ölçütleri kutucuğu

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

## <a name="powershell"></a>PowerShell

Aşamalı dağıtımları yönetmek için aşağıdaki Windows PowerShell cmdlet 'lerini kullanın:

### <a name="automatically-create-phased-deployments"></a>Aşamalı dağıtımları otomatik olarak oluştur

- [New-CMApplicationAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmapplicationautophaseddeployment?view=sccm-ps)
- [New-CMSoftwareUpdateAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdateautophaseddeployment?view=sccm-ps)
- [New-CMTaskSequenceAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequenceautophaseddeployment?view=sccm-ps)

### <a name="manually-create-phased-deployments"></a>Aşamalı dağıtımları el ile oluşturma

- [New-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/new-cmsoftwareupdatephase?view=sccm-ps)
- [New-CMSoftwareUpdateManualPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatemanualphaseddeployment?view=sccm-ps)
- [New-CMTaskSequencePhase](/powershell/module/configurationmanager/new-cmtasksequencephase?view=sccm-ps)
- [New-CMTaskSequenceManualPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequencemanualphaseddeployment?view=sccm-ps)

### <a name="get-existing-phased-deployment-objects"></a>Var olan aşamalı dağıtım nesnelerini al

- [Get-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/get-cmapplicationphaseddeployment?view=sccm-ps)
- [Get-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/get-cmsoftwareupdatephaseddeployment?view=sccm-ps)
- [Get-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/get-cmtasksequencephaseddeployment?view=sccm-ps)
- [Get-Cmphatıcı](/powershell/module/configurationmanager/get-cmphase?view=sccm-ps)

### <a name="monitor-phased-deployment-status"></a>Aşamalı dağıtım durumunu izleme

- [Get-CMPhasedDeploymentStatus](/powershell/module/configurationmanager/get-cmphaseddeploymentstatus?view=sccm-ps)

### <a name="manage-existing-phased-deployments"></a>Mevcut aşamalı dağıtımları yönetme

- [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext?view=sccm-ps)
- [Özgeçmişi-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment?view=sccm-ps)
- [Askıya al-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment?view=sccm-ps)

### <a name="modify-existing-phased-deployments"></a>Mevcut aşamalı dağıtımları Değiştir

- [Set-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/set-cmapplicationphaseddeployment?view=sccm-ps)
- [Set-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/set-cmsoftwareupdatephase?view=sccm-ps)
- [Set-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/set-cmsoftwareupdatephaseddeployment?view=sccm-ps)
- [Set-CMTaskSequencePhase](/powershell/module/configurationmanager/set-cmtasksequencephase?view=sccm-ps)
- [Set-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/set-cmtasksequencephaseddeployment?view=sccm-ps)
- [Remove-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/remove-cmapplicationphaseddeployment?view=sccm-ps)
- [Remove-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/remove-cmsoftwareupdatephaseddeployment?view=sccm-ps)
- [Remove-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/remove-cmtasksequencephaseddeployment?view=sccm-ps)
