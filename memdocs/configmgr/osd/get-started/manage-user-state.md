---
title: Kullanıcı durumunu yönetme
titleSuffix: Configuration Manager
description: Configuration Manager, işletim sistemi dağıtım senaryolarında Kullanıcı durumu verilerini yakalamak ve geri yüklemek için Kullanıcı Durumu Taşıma Aracı kullanır.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a720c68fc705187dedb6ff04fc3898a8b0b21c8
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124372"
---
# <a name="manage-user-state-in-configuration-manager"></a>Configuration Manager Kullanıcı durumunu yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli işletim sisteminin kullanıcı durumunu tutmak istediğiniz işletim sistemi dağıtım senaryolarında, Configuration Manager görev dizilerini kullanarak Kullanıcı durumu verilerini yakalayabilir ve geri yükleyebilirsiniz. Örnek:  

- Kullanıcı durumunu bir bilgisayardan yakalayıp diğer bilgisayara geri yüklemek istediğiniz dağıtımlar.  

- Kullanıcı durumunu yakalayıp aynı bilgisayara geri yüklemek istediğiniz güncelleştirme dağıtımları.  

Configuration Manager, işletim sistemi yüklemesi tamamlandıktan sonra bir kaynak bilgisayardan hedef bilgisayara Kullanıcı durumu verilerinin geçişini yönetmek için Kullanıcı Durumu Taşıma Aracı (USMT) 10,0 kullanır. USMT 10.0’a yönelik genel geçiş senaryoları hakkında daha fazla bilgi için bkz.  [Genel Geçiş Senaryoları](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios).

Kullanıcı verilerini yakalamanıza ve geri yüklemenize yardımcı olması için aşağıdaki bölümleri kullanın.

## <a name="store-user-state-data"></a><a name="BKMK_StoringUserData"></a>Kullanıcı durumu verilerini depolama

 Kullanıcı durumunu yakaladığınızda, kullanıcı durumu verilerini hedef bilgisayarda veya bir durum geçiş noktasında depolayabilirsiniz. Kullanıcı durumunu bir Kullanıcı durumu geçiş noktasında depolamak için durum geçiş noktası site sistemi rolünü barındıran bir Configuration Manager site sistem sunucusu kullanmanız gerekir. Kullanıcı durumunu hedef bilgisayarda depolamak için, görev dizinizi, bağlantıları kullanarak verileri yerel olarak depolayacak şekilde yapılandırmanız gerekir.

> [!NOTE]
> Kullanıcı durumunu yerel olarak depolamak için kullanılan bağlantılara sabit bağlantılar denir. Sabit bağlantılar, bilgisayarda kullanıcı dosyalarını ve ayarlarını tarayan ve ardından bu dosyalar için bir sabit bağlantılar dizini oluşturan bir USMT 10.0 özelliğidir. Bu sabit bağlantılar, yeni işletim sistemi dağıtıldıktan sonra kullanıcı verilerini geri yüklemek için kullanılır.

> [!IMPORTANT]
> Kullanıcı durumu verilerini depolamak için durum geçiş noktasını ve sabit bağlantıları aynı anda kullanamazsınız.

Kullanıcı durumu bilgisi yakalandığında, bilgiler aşağıdaki yöntemlerin biri kullanılarak depolanabilir:  

- Kullanıcı durumu verilerini, bir durum geçiş noktası yapılandırarak uzaktan depolayabilirsiniz. **Yakala** görev dizisi, verileri durum geçiş noktasına gönderir. Ardından, işletim sistemi dağıtıldıktan sonra **Geri yükle** görev dizisi verileri alır ve kullanıcı durumunu hedef bilgisayarda geri yükler.  

- Kullanıcı durumu verilerini, yerel olarak belirli bir konuma depolayabilirsiniz. Bu senaryoda **Yakala** görev dizisi, kullanıcı verilerini hedef bilgisayardaki belirli bir konuma kopyalar. Ardından, işletim sistemi dağıtıldıktan sonra **Geri yükle** görev dizisi kullanıcı verilerini o konumdan alır.  

- Kullanıcı verilerini orijinal konumuna geri yüklemek üzere kullanılabilecek sabit bağlantılar belirtebilirsiniz. Bu senaryoda, kullanıcı durumu verileri, eski işletim sistemi kaldırıldığında sürücüde kalır. Ardından, yeni işletim sistemi dağıtıldıktan sonra **Geri yükle** görev dizisi kullanıcı durumu verilerini orijinal konumuna geri yüklemek için sabit bağlantıları kullanır.  

### <a name="store-user-data-on-a-state-migration-point"></a><a name="BKMK_UserDataSMP"></a> Bir durum geçiş noktasına kullanıcı verilerini depolama

 Kullanıcı durumu verilerini bir durum geçiş noktasına depolamak için aşağıdakileri yapmanız gerekir:  

1. Kullanıcı durumu verilerini depolamak için[Configure a state migration point](#BKMK_StateMigrationPoint) .  

1. Kaynak bilgisayarla hedef bilgisayar arasındaki[Create a computer association](#BKMK_ComputerAssociation) . Bu ilişkiyi, kaynak bilgisayarda kullanıcı durumunu yakalamadan önce oluşturmanız gerekir.  

1. [Kullanıcı durumunu yakalamak ve geri yüklemek için bir görev dizisi oluşturun](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Özellikle, bir bilgisayardan Kullanıcı verilerini yakalamak, bir durum geçiş noktasında Kullanıcı tarihini depolamak ve Kullanıcı verilerini bir bilgisayara geri yüklemek için aşağıdaki görev dizisi adımlarını eklemeniz gerekir:  

    - Bir bilgisayardan durum yakalanırken veya bir bilgisayara durum geri yüklenirken durum geçiş noktası erişimi istemek için[Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore) .  

    - Kullanıcı durumu verilerini yakalamak ve durum geçiş noktasına depolamak için[Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) .  

    - Bir kullanıcı durumu geçiş noktasından verileri alarak kullanıcı durumunu hedef bilgisayara geri yüklemek için[Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) .  

    - Yakalama veya geri yükleme eyleminin tamamlanduğunu durum geçiş noktasına bildirmek için[Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) .  

### <a name="store-user-data-locally"></a><a name="BKMK_UserDataDestination"></a>Kullanıcı verilerini yerel olarak depolama

 Kullanıcı durumu verilerini yerel olarak depolamak için şunları yapmanız gerekir:  

- [Kullanıcı durumunu yakalamak ve geri yüklemek için bir görev dizisi oluşturun](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Özellikle, bir bilgisayardan Kullanıcı verilerini yakalamak ve sabit bağlantılar kullanarak Kullanıcı verilerini bir bilgisayara geri yüklemek için aşağıdaki görev dizisi adımlarını eklemeniz gerekir;

  - kullanıcı durumu verilerini yakalamak ve sabit bağlantılar kullanarak yerel klasöre depolamak için[Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) .  

  - Sabit bağlantıları ile verileri alarak kullanıcı durumunu hedef bilgisayara geri yüklemek için[Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) .  

    > [!NOTE]
    > Görev dizisi eski işletim sistemini kaldırdıktan sonra sabit bağlantıların başvurduğu kullanıcı durumu verileri bilgisayarda kalır. Bu veriler, yeni işletim sistemi dağıtıldığında kullanıcı durumunu geri yüklemek için kullanılan verilerdir.  

## <a name="configure-a-state-migration-point"></a><a name="BKMK_StateMigrationPoint"></a> Configure a state migration point

Durum yükseltme noktası, bir bilgisayarda yakalanan ve daha sonra diğer bir bilgisayara geri yüklenen kullanıcı durum verilerini depolar. Ancak, hedef bilgisayardaki işletim sistemini yenilerken gerçekleştirdiğiniz bir dağıtımda olduğu gibi aynı bilgisayar üzerinde işletim sistemi dağıtımı için kullanıcı ayarlarını yakaladığınızda, sabit bağlantılar kullanarak veriyi aynı bilgisayara veya bir durum geçişi noktasına depolayabilirsiniz. Bazı bilgisayar dağıtımları için, durum deposunu oluşturduğunuzda, Configuration Manager otomatik olarak durum deposu ve hedef bilgisayar arasında bir ilişki oluşturur. Durum geçiş noktasını kullanıcı durumu verilerini depolamak üzere yapılandırmak için aşağıdaki yöntemleri kullanabilirsiniz:  

- Durum geçiş noktası için yeni bir site sistemi sunucusu oluşturmak için **Site Sistemi Sunucusu Oluşturma Sihirbazı** 'nı kullanın.  

- Var olan bir sunucuya durum geçiş noktası eklemek için **Site Sistemi Rolleri Ekleme Sihirbazı** 'nı kullanın.  

  Bu sihirbazları kullandığınızda, durum geçiş noktası için aşağıdaki bilgileri sağlamanız istenir:  

- Kullanıcı durumu verilerinin depolanacağı klasörler.  

- Durum geçiş noktasında veri depolayabilen maksimum istemci sayısı.  

- Durum geçiş noktasının kullanıcı durumu verilerini depolaması için minimum boş alan.  

- Role ilişkin silme ilkesi. Kullanıcı durumu verilerinin bir bilgisayara geri yüklendikten hemen sonra silineceğini veya bilgisayara yüklenmesinin üzerinden belirli sayıda gün geçtikten sonra silineceğini belirtebilirsiniz.  

- Durum geçiş noktasının yalnızca kullanıcı durumu verilerini geri yükleme isteklerine yanıt verip vermeyeceği. Bu seçeneği etkinleştirdiğinizde, durum geçiş noktasını kullanıcı durumu verilerini depolamak için kullanamazsınız.  

  Durum geçiş noktası ve yapılandırma adımları hakkında daha fazla bilgi için bkz. [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="create-a-computer-association"></a><a name="BKMK_ComputerAssociation"></a> Create a computer association

Bir işletim sistemini yeni donanıma yüklediğinizde ve kullanıcı veri ayarlarını yakalayıp geri yüklemek istediğinizde kaynak bilgisayar ile hedef bilgisayar arasında ilişki tanımlamak üzere bir bilgisayar ilişkisi oluşturun. Kaynak bilgisayar, Configuration Manager yönettiği mevcut bir bilgisayardır. Yeni işletim sistemini hedef bilgisayara dağıttığınızda, kaynak bilgisayar, hedef bilgisayara geçirilen kullanıcı durumunu içerir.  

> [!NOTE]  
> Bir Configuration Manager üst sitesinde bulunan bilgisayarlar arasında bir alt sitede bulunan bilgisayarlar arasında bir bilgisayar ilişkilendirmesi oluşturmak desteklenmez. Bilgisayar Ilişkilendirmeleri siteye özgüdür ve çoğaltılmaz.  

### <a name="to-create-a-computer-association"></a>Bilgisayar ilişkisi oluşturmak için

1. Configuration Manager konsolunda, **Varlıklar ve Uyum**'u tıklatın.  

1. **Varlıklar ve Uyum** çalışma alanında, **Kullanıcı Durumu Geçişi**'ni tıklatın.  

1. **Giriş** sekmesinde, **Oluştur** grubunda, **Bilgisayar İlişkilendirmesi Oluştur**'u tıklatın.  

1. **Bilgisayar İlişkilendirme Özellikleri** iletişim kutusunun **Bilgisayar İlişkilendirmesi** sekmesinde, yakalanacak kullanıcı durumunun bulunduğu kaynak bilgisayarı ve kullanıcı durumu verilerinin geri yükleneceği hedef bilgisayarı belirtin.  

1. **Kullanıcı Hesapları** sekmesinde, hedef bilgisayara geçirilecek kullanıcı hesaplarını belirtin. Aşağıdaki ayarlardan birini belirtin:  

    - **Tüm kullanıcı hesaplarını yakala ve geri yükle**: Bu ayar, kullanıcı hesaplarının tümünü yakalar ve geri yükler. Aynı kaynak bilgisayara yönelik birden fazla ilişki oluşturmak için bu ayarı kullanın.  

    - **Tüm kullanıcı hesaplarını yakala ve belirtilen hesapları geri yükle**: Bu ayar, kaynak bilgisayardaki kullanıcı hesaplarının tümünü yakalar ve yalnızca hedef bilgisayarda belirttiğiniz hesapları geri yükler. Ayrıca, aynı kaynak bilgisayara yönelik birden fazla ilişki oluşturmak istediğinizde de bu ayarı kullanabilirsiniz.  

    - **Belirtilen kullanıcı hesaplarını yakala ve geri yükle**: Bu ayar, yalnızca belirttiğiniz hesapları yakalar ve geri yükler. Bu ayarı seçtiğinizde, aynı kaynak bilgisayara yönelik birden fazla ilişki oluşturamazsınız.  

## <a name="restore-user-state-data-when-an-operating-system-deployment-fails"></a><a name="BKMK_MigrationFails"></a> İşletim sistemi dağıtımı başarısız olduğunda kullanıcı durum verilerini geri yükleme

İşletim sistemi dağıtımı başarısız olursa, dağıtım işlemi sırasında yakalanan kullanıcı durumu verilerini almak için USMT 10.0 LoadState özelliğini kullanın. Bu, bir durum geçiş noktasında depolanan verileri veya hedef bilgisayarda yerel olarak kayıtlı verileri içerir. Bu USMT özelliği hakkında daha fazla bilgi için, bkz. [LoadState Sözdizimi](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).
