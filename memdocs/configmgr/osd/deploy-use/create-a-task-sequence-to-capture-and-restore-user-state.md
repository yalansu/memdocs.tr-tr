---
title: Kullanıcı durumunu yakala ve geri yükle
titleSuffix: Configuration Manager
description: İşletim sistemi dağıtım senaryolarında Kullanıcı durumu verilerini yakalamak ve geri yüklemek için Configuration Manager görev dizilerini kullanın.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a1f11c46689b213b795c0d71221728f916a68bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125500"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Configuration Manager Kullanıcı durumunu yakalamak ve geri yüklemek için bir görev dizisi oluşturun

 *Uygulama hedefi: Configuration Manager (geçerli dal)*

 İşletim sistemi dağıtım senaryolarında Kullanıcı durumu verilerini yakalamak ve geri yüklemek için Configuration Manager görev dizilerini kullanın. Bu senaryolarda, geçerli işletim sisteminin kullanıcı durumunu bekletmek istiyorsunuz. Oluşturduğunuz görev dizisinin türüne bağlı olarak, yakalama ve geri yükleme adımları görev dizisine otomatik olarak eklenebilir. Diğer senaryolarda, yakalama ve geri yükleme adımlarını görev dizisine el ile yüklemeniz gerekebilir. Bu makalede, Kullanıcı durumu verilerini yakalamak ve geri yüklemek için var olan bir görev dizisine eklemeniz gereken adımlar sağlanmaktadır.  



## <a name="task-sequence-steps"></a>Görev dizisi adımları  

Kullanıcı durumunu yakalamak ve geri yüklemek için aşağıdaki adımları görev dizisine ekleyin:  

- [Durum depolama alanını iste](../understand/task-sequence-steps.md#BKMK_RequestStateStore): Kullanıcı durumunu durum geçiş noktasında depoluyiniz, bu adım gereklidir.  

- [Kullanıcı durumunu yakala](../understand/task-sequence-steps.md#BKMK_CaptureUserState): Bu adım, Kullanıcı durumu verilerini yakalar. Ardından, verileri durum geçiş noktasında veya hardlinks kullanarak yerel diskte depolar.  

- [Kullanıcı Durumunu Geri Yükle](../understand/task-sequence-steps.md#BKMK_RestoreUserState): Bu adım, kullanıcı durumu verilerini hedef bilgisayara geri yükler. Verileri bir durum geçiş noktasından alabilir veya yerel disk üzerinde bir bağlantı oluşturabilirsiniz.  

- [Yayın durumu deposu](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): Kullanıcı durumunu durum geçiş noktasında depolarsanız, bu adım gereklidir. Bu adım, verileri durum geçiş noktasından kaldırır.  


 Kullanıcı durumunu yakalamak ve geri yüklemek için gereken görev sırası adımlarını eklemek için aşağıdaki yordamları kullanın. Bir görev dizisi oluşturma hakkında daha fazla bilgi için bkz. [görevleri otomatikleştirmek için görev dizilerini yönetme](manage-task-sequences-to-automate-tasks.md).  



## <a name="capture-the-user-state"></a>Kullanıcı durumunu yakala  

 Kullanıcı durumunu yakalamak üzere görev sırası adımları eklemek için aşağıdaki adımları kullanın:

1.  **Görev Dizisi** listesinde, bir görev sırası seçin ve ardından **Düzenle**'yi tıklatın.  

2.  Kullanıcı durumunu depolamak için bir durum geçiş noktası kullanıyorsanız, görev dizisine **Istek durumu deposu** adımını ekleyin. **Görev sırası düzenleyicisinde** **Ekle**' ye tıklayın. **Kullanıcı durumu**' nun üzerine gelin ve ardından **durum deposu iste**' ye tıklayın. Bu adım için özellikleri ve seçenekleri yapılandırın ve ardından **Uygula**' ya tıklayın. Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Istek durumu deposu](../understand/task-sequence-steps.md#BKMK_RequestStateStore).  

3.  **Kullanıcı Durumunu Yakala** adımını görev dizisine ekleyin. **Görev sırası düzenleyicisinde** **Ekle**' ye tıklayın. **Kullanıcı durumu**' nun üzerine gelin ve ardından **Kullanıcı durumunu yakala**' yı tıklatın. Bu adım için özellikleri ve seçenekleri yapılandırın ve ardından **Uygula**' ya tıklayın. Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [yakalama Kullanıcı durumu](../understand/task-sequence-steps.md#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Bu adımı görev dizine eklediğinizde, Kullanıcı durumu verilerinin nerede depolanacağını belirtmek için **OSDStateStorePath** görev sırası değişkenini de ayarlayın. Kullanıcı durumunu yerel olarak depolumeniz durumunda, görev dizisinin başarısız olmasına neden olabilecek bir kök klasör belirtmeyin. Kullanıcı verilerini yerel olarak depolayacağınız zaman daima bir klasör veya alt klasör kullanın. Bu değişken hakkında daha fazla bilgi için bkz. [görev dizisi değişkenleri](../understand/task-sequence-variables.md#OSDStateStorePath).  

4.  Bir durum geçiş noktası kullanıyorsanız, görev dizisine **durum depolamayı serbest bırak** adımını ekleyin. **Görev sırası düzenleyicisinde** **Ekle**' ye tıklayın. **Kullanıcı durumu**' nun üzerine gelin ve ardından **durum deposunu serbest bırak**' a tıklayın. Bu adım için özellikleri ve seçenekleri yapılandırın ve ardından **Uygula**' ya tıklayın. Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  Durum depolama **alanını serbest bırakma** adımının başlamasından önce, **serbest bırakma** sonrasında çalışan görev sırası eyleminin başarılı olması gerekir.  


 Hedef bilgisayarda kullanıcı durumunu yakalamak için bu görev dizisini dağıtın. Görev dizilerini dağıtma hakkında bilgi için bkz. [Deploy a task sequence](deploy-a-task-sequence.md).  



## <a name="restore-the-user-state"></a>Kullanıcı durumunu geri yükleme  

 Kullanıcı durumunu geri yüklemek için görev sırası adımları eklemek için aşağıdaki adımları kullanın:

1. **Görev Dizisi** listesinde, bir görev sırası seçin ve ardından **Düzenle**'yi tıklatın.  

2. **Restore User State** adımını görev dizisine ekleyin. **Görev sırası düzenleyicisinde** **Ekle**' ye tıklayın. **Kullanıcı durumu**' nun üzerine gelin ve ardından **Kullanıcı durumunu geri yükle**' ye tıklayın. Bu adım, gerekirse durum geçiş noktası ile bağlantı kurar. Bu adım için özellikleri ve seçenekleri yapılandırın ve ardından **Uygula**' ya tıklayın. Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Kullanıcı durumunu geri yükleme](../understand/task-sequence-steps.md#BKMK_RestoreUserState).  

   > [!Important]  
   >  [Kullanıcı durumunu yakala](../understand/task-sequence-steps.md#BKMK_CaptureUserState) adımını **standart seçeneklerle tüm Kullanıcı profillerini yakalama**seçeneğiyle birlikte kullandığınızda, **Kullanıcı durumunu geri yükle** adımında **Yerel bilgisayar kullanıcı profillerini geri yükle** ayarını seçmeniz gerekir. Aksi takdirde görev dizisi başarısız olur.  

   > [!Note]  
   > Kullanıcı durumunu yerel hardlinks kullanarak depolu, geri yükleme başarılı olmazsa, verileri depolamak için oluşturulan hardlinks 'i el ile silebilirsiniz. Görev sırası, [komut satırı Çalıştır](../understand/task-sequence-steps.md#BKMK_RunCommandLine) adımı ile bu eylemi otomatikleştirmek Için USMTUtils aracını çalıştırabilir. Hardlink 'yi silmek için USMTUtils kullanırsanız, USMTUtils çalıştırdıktan sonra bir [restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) adımı ekleyin.  

3. Kullanıcı durumunu depolamak için bir durum geçiş noktası kullanıyorsanız, görev dizisine **durum depolamayı serbest bırak** adımını ekleyin. **Görev sırası düzenleyicisinde** **Ekle**' ye tıklayın. **Kullanıcı durumu**' nun üzerine gelin ve ardından **durum deposunu serbest bırak**' a tıklayın. Bu adım için özellikleri ve seçenekleri yapılandırın ve ardından **Uygula**' ya tıklayın. Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz. [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  Durum depolama **alanını serbest bırakma** adımının başlamasından önce, **serbest bırakma** sonrasında çalışan görev sırası eyleminin başarılı olması gerekir.  


 Kullanıcı durumunu bir hedef bilgisayara geri yüklemek için bu görev dizisini dağıtın. Görev dizilerini dağıtma hakkında bilgi için bkz. [Deploy a task sequence](deploy-a-task-sequence.md).  



## <a name="next-steps"></a>Sonraki adımlar

[Görev dizisi dağıtımını izleme](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
