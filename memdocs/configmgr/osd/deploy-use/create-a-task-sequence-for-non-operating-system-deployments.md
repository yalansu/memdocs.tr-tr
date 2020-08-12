---
title: İşletim sistemi dışı dağıtımlar için görev dizisi oluşturma
titleSuffix: Configuration Manager
description: Yazılım dağıtma veya görevleri otomatikleştirme gibi bir işletim sistemini dağıtmak için olmayan görev dizileri oluşturun
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fcae4d520b1e81d0ef3470cd12ee68488b4f589
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125535"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>İşletim sistemi dışı dağıtımlar için görev dizisi oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager görev dizileri, ortamınızdaki farklı türdeki görevleri otomatikleştirmek için kullanılır. Bu görevler öncelikli olarak işletim sistemlerinin dağıtılması için tasarlanmış ve test edilmiştir. Configuration Manager, aşağıdaki senaryolar için kullandığınız birincil teknoloji olması gereken birçok farklı özelliğe sahiptir:

- [Uygulama yükleme](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > Sürüm 2002 ' den başlayarak, uygulama modeli aracılığıyla görev dizilerini kullanarak karmaşık uygulamaları yüklemeyin. Uygulamayı yüklemek ya da kaldırmak için, bir görev dizisi olan bir uygulamaya dağıtım türü ekleyin. Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [Yazılım güncelleştirmeleri yüklemesi](../../sum/understand/software-updates-introduction.md)

- [Ayar yapılandırması](../../compliance/understand/ensure-device-compliance.md)

Ayrıca, [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) ve [Service Management Automation](https://docs.microsoft.com/system-center/sma/)gibi diğer Microsoft System Center otomasyon teknolojilerini de göz önünde bulundurun.  

Görev sıralarının gücü esnekliğine ve bunları nasıl kullanmanıza göre yer alır. İstemci ayarlarını yapılandırabilir, yazılım dağıtabilir, sürücüleri güncelleştirebilir, Kullanıcı durumlarını düzenleyebilir ve işletim sistemi dağıtımından bağımsız diğer görevleri gerçekleştirebilir. İstediğiniz sayıda görev eklemek için özel bir görev dizisi oluşturabilirsiniz. İşletim sistemi dışındaki dağıtımlar için özel görev sıralarının kullanımı Configuration Manager desteklenir. Ancak, bir görev dizisi istenmeyen veya tutarsız sonuçlara neden olursa, işlemi basitleştirecek yöntemlere bakın:

- Daha basit adımları kullanın
- Eylemleri birden çok görev dizisi arasında bölme
- Görev dizisini oluşturma ve test etme için aşamalı bir yaklaşım alın

## <a name="supported-steps"></a>Desteklenen adımlar

Aşağıdaki adımlar, işletim sistemi olmayan dağıtım özel görev dizisinde kullanılmak üzere desteklenir:  

- [Hazır Olma Durumunu Kontrol Et](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Ağ Klasörüne Bağlan](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Paket İçeriğini İndirme](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Uygulamayı Yükle](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Paketi Yükle](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Yazılım Güncelleştirmelerini Yükle](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Bilgisayarı Yeniden Başlat](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Komut satırını Çalıştır](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [PowerShell Komut Dosyasını Çalıştır](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Görev sırasını Çalıştır](../understand/task-sequence-steps.md#child-task-sequence)  

- [Dinamik Değişkenleri Ayarla](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Görev Dizisi Değişkenini Ayarla](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Sonraki adımlar

[Özel bir görev sırası oluşturma](create-a-custom-task-sequence.md)