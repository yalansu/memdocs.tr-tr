---
title: Şirket içi siteyi genişletme ve Microsoft Azure için geçirme
titleSuffix: Configuration Manager
description: Configuration Manager için Azure sanal makinelerini programlı bir şekilde oluşturmak üzere geçiş aracının nasıl kullanılacağını öğrenin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 00f07e20c24ea9bb7d06b18f300e0206696c5e20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723456"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Şirket içi siteyi genişletme ve Microsoft Azure için geçirme

*Uygulama hedefi: Configuration Manager (Güncel Dalı)*


Sürüm 1910 ' de tanıtılan bu araç, Configuration Manager için programlı olarak Azure sanal makineleri (VM 'Ler) oluşturmanıza yardımcı olur. <!--3556022--> Bu, pasif site sunucusu, yönetim noktaları ve dağıtım noktaları gibi varsayılan ayarlar site rolleriyle yüklenebilir. Yeni rolleri doğruladıktan sonra, yüksek kullanılabilirlik için bunları ek site sistemleri olarak kullanın. Ayrıca şirket içi site sistem rolünü kaldırabilir ve yalnızca Azure VM rolünü tutabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- Bir Azure aboneliği

- ExpressRoute ağ geçidi ile Azure sanal ağı

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- Kullanıcı hesabınızın bir Configuration Manager **tam yönetici** olması ve birincil site sunucusunda yönetici haklarına sahip olması gerekir.

- Pasif bir sunucu eklemek için, birincil sitenin [site sunucusu yüksek kullanılabilirlik gereksinimlerini](../servers/deploy/configure/site-server-high-availability.md#prerequisites)karşılaması gerekir. Örneğin, [uzak bir içerik kitaplığı](../plan-design/hierarchy/the-content-library.md#bkmk_remote)gerektirir.

### <a name="required-azure-permissions"></a>Gerekli Azure izinleri

Aracı çalıştırdığınızda Azure 'da aşağıdaki izinlere sahip olmanız gerekir:
<!--5789222-->
Microsoft. resources/abonelikler/resourceGroups/Read <br>
Microsoft. resources/abonelikler/resourceGroups/Write <br>
Microsoft. resources/dağıtımlar/okuma <br>
Microsoft. resources/dağıtımlar/yazma <br>
Microsoft. resources/dağıtımlar/doğrulama/eylem <br>
Microsoft. COMPUTE/virtualMachines/Extensions/okuma <br>
Microsoft. COMPUTE/virtualMachines/uzantılar/Write <br>
Microsoft. COMPUTE/virtualMachines/okuma <br>
Microsoft. COMPUTE/virtualMachines/Write <br>
Microsoft. Network/virtualNetworks/Read <br>
Microsoft. Network/virtualNetworks/alt ağlar/okuma <br>
Microsoft. Network/virtualNetworks/alt ağlar/JOIN/Action <br>
Microsoft. Network/NetworkInterfaces/Read <br>
Microsoft. Network/NetworkInterfaces/Write <br>
Microsoft. Network/NetworkInterfaces/JOIN/Action <br>
Microsoft. Network/networkSecurityGroups/Write <br>
Microsoft. Network/networkSecurityGroups/Read <br>
Microsoft. Network/networkSecurityGroups/JOIN/Action <br>
Microsoft. Storage/storageAccounts/Write <br>
Microsoft. Storage/storageAccounts/Read <br>
Microsoft. Storage/storageAccounts/ListKeys/Action <br>
Microsoft. Storage/storageAccounts/listServiceSas/eylem <br>
Microsoft. Storage/storageAccounts/blobServices/kapsayıcılar/Write <br>
Microsoft. Storage/storageAccounts/blobServices/kapsayıcılar/okuma <br>
Microsoft. Keykasası/Vaults/dağıtım/eylem <br>
Microsoft. Keykasası/Kasaults/okuma <br>


İzinler ve rol atama hakkında daha fazla bilgi için bkz. [RBAC kullanarak Azure kaynaklarına erişimi yönetme](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

## <a name="run-the-tool"></a>Aracı çalıştırma

1. Birincil site sunucusunda oturum açın ve Configuration Manager yükleme dizininde aşağıdaki aracı çalıştırın:`Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. **Genel** sekmesindeki bilgileri gözden geçirin ve ardından **Azure Information** sekmesine geçin.

1. **Azure bilgileri** sekmesinde **Azure ortamınızı**seçin ve **oturum açın**.

    > [!TIP]
    > Doğru şekilde oturum açmak için `https://*.microsoft.com` güvenilir web siteleri listenize eklemeniz gerekebilir.

    [![Genişlet ve geçir aracında Azure bilgileri sekmesi](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. Oturum açtıktan sonra, **ABONELIK kimliğinizi** ve **Sanal ağınızı**seçin. Araç yalnızca bir ExpressRoute ağ geçidi olan ağları listeler.

## <a name="site-server-high-availability"></a>Site sunucusu yüksek kullanılabilirlik

1. **Site sunucusu yüksek kullanılabilirlik** sekmesinde, sitenizin hazır olduğunu değerlendirmek için **Denetle** ' yi seçin.

    Denetimlerden herhangi biri başarısız olursa, sorunu nasıl düzelteceğini belirlemek için **daha fazla ayrıntı** öğesini seçin. Bu Önkoşullar hakkında daha fazla bilgi için bkz. [site sunucusu yüksek kullanılabilirlik](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

2. Site sunucunuzu Azure 'a genişletmek veya geçirmek istiyorsanız, **Azure 'da site sunucusu oluştur**' u seçin. Ardından aşağıdaki alanları girin:

    |Adı|Açıklama|
    |---|---|
    |**Abonelik**|Salt okunurdur. Abonelik adı ve KIMLIĞINI gösterir.|
    |**Kaynak grubu**| Kullanılabilir kaynak gruplarını listeler. Yeni bir kaynak grubu oluşturmanız gerekiyorsa, [Azure Portal](https://portal.azure.com)kullanın ve ardından bu aracı yeniden çalıştırın.|
    |**Konum**| Salt okunurdur. Sanal ağınızın konumu tarafından belirlenir|
    |**VM boyutu**|İş yükünüze sığacak bir boyut seçin. Microsoft **Standard_DS3_v2**önerir.|
    |**İşletim sistemi**|Salt okunurdur. Araç Windows Server 2019 kullanır.|
    |**Disk türü**|Salt okunurdur. Araç en iyi performans için Premium SSD kullanır.|
    |**Sanal ağ**|Salt okunurdur.|
    |**Alt ağ**|Kullanılacak alt ağı seçin. Yeni bir alt ağ oluşturmanız gerekiyorsa [Azure Portal](https://portal.azure.com)kullanın.|
    |**Makine adı**|Azure 'da pasif site sunucusu VM 'sinin adını girin. [Azure Portal](https://portal.azure.com)gösterilenle aynı adı vardır.|
    |**Yerel Yönetici Kullanıcı adı**|Azure VM 'nin etki alanına katılmadan önce oluşturduğu yerel yönetici kullanıcının adını girin.|
    |**Yerel yönetici parolası**|Yerel yönetici kullanıcının parolası. Azure dağıtımı sırasında parolayı korumak için, parolayı [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview)bir gizli dizi olarak depolayın. Ardından, buradaki başvuruyu kullanın. Gerekirse, [Azure Portal](https://portal.azure.com)yeni bir tane oluşturun.|
    |**Etki alanı FQDN 'SI**|Active Directory etki alanının katılması için tam etki alanı adı. Varsayılan olarak, araç bu değeri geçerli makinenizden alır.|
    |**Etki alanı Kullanıcı adı**|Etki alanına katılmasına izin verilen etki alanı kullanıcısının adı. Araç varsayılan olarak, şu anda oturum açmış kullanıcının adını kullanır.|
    |**Etki alanı parolası**|Etki alanına katılacak etki alanı kullanıcısının parolası. Araç, **Başlat**' ı seçtikten sonra doğrular. Azure dağıtımı sırasında parolayı korumak için, parolayı [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview)bir gizli dizi olarak depolayın. Ardından, buradaki başvuruyu kullanın. Gerekirse, [Azure Portal](https://portal.azure.com)yeni bir tane oluşturun.|
    |**Etki alanı DNS IP 'si**|Etki alanına katılmak için kullanılır. Varsayılan olarak, araç geçerli makinenizden geçerli DNS 'i kullanır.|
    |**Tür**|Salt okunurdur. *Pasif site sunucusunu* tür olarak gösterir.|

    > [!IMPORTANT]
    > Varsayılan olarak, sanal makineler **mevcut Windows Server lisansını kullan**için **Hayır** olarak ayarlanır. Yazılım Güvencesi kapsamındaki şirket içi Windows Server lisanslarınızı kullanmak istiyorsanız, sanal makineler sağlandıktan sonra [Azure Portal](https://portal.azure.com) bu ayarı yapılandırın. Daha fazla bilgi için bkz. [Windows Server için Azure hibrit avantajı](https://docs.microsoft.com/windows-server/get-started/azure-hybrid-benefit).

1. Azure VM 'yi sağlamaya başlamak için **Başlat**' ı seçin. Dağıtım durumunu izlemek için, aracının **Azure 'Daki dağıtımlar** sekmesine geçin. En son durumu almak için **dağıtım durumunu yenile**' yi seçin.

    > [!TIP]
    > Ayrıca, durumu denetlemek, hataları bulmak ve olası düzeltmeleri öğrenmek için [Azure Portal](https://portal.azure.com) de kullanabilirsiniz.

1. Dağıtım tamamlandığında, SQL sunucularınıza gidin ve yeni Azure VM için izin verin. Daha fazla bilgi için bkz. [site sunucusu yüksek kullanılabilirlik-Önkoşullar](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

1. Azure VM 'yi pasif modda bir site sunucusu olarak eklemek için, **pasif modda site sunucusu Ekle**' yi seçin.

1. Site sunucusu site sunucusunu pasif modda eklediğinde, **site sunucusu yüksek kullanılabilirlik** sekmesinde durum görüntülenir.

   [![Site sunucusu yüksek kullanılabilirlik sekmesine eklenen pasif site sunucusu](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Ardından, dağıtımı tamamlaması için [Azure 'Daki dağıtımlar](#bkmk_deploy-azure) sekmesine gidin.

## <a name="site-database"></a>Site veritabanı

Araç, şu anda veritabanını Şirket içinden Azure 'a geçirmek için herhangi bir görev içermiyor. Veritabanını şirket içi SQL Server 'dan Azure SQL Server VM taşımayı seçebilirsiniz. Araç, yardım almak için **site veritabanı** sekmesinde aşağıdaki makaleleri listeler:

- [Veritabanını yedekleme ve geri yükleme](../servers/manage/backup-and-recovery.md)
- [SQL 'ı her zaman açık olarak yapılandırma ve verilerin çoğaltılmasına izin verme](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [Bir SQL veritabanını Azure SQL Server VM geçirme](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>Site sistemi rolleri

1. **Site sistemi rolleri** sekmesine geçin. Varsayılan ayarlarla yeni bir site sistem rolü sağlamak için **Yeni oluştur**' u seçin. Yönetim noktası, dağıtım noktası ve yazılım güncelleştirme noktası gibi roller sağlayabilirsiniz. Şu anda araçta tüm roller mevcut değil.

    [![Genişlet ve geçir aracında site sistem rolleri sekmesi](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. Sağlama penceresinde, Azure 'da site rolünün VM 'sini sağlamak için alanları girin. Bu ayrıntılar, site sunucusu için yukarıdaki listeye benzerdir.

1. Azure VM 'yi sağlamaya başlamak için **Başlat**' ı seçin. Dağıtım durumunu izlemek için, aracının **Azure 'Daki dağıtımlar** sekmesine geçin. En son durumu almak için **dağıtım durumunu yenile**' yi seçin.

    > [!TIP]
    > Ayrıca, durumu denetlemek, hataları bulmak ve olası düzeltmeleri öğrenmek için [Azure Portal](https://portal.azure.com) de kullanabilirsiniz.

1. Daha fazla site sistemi rolü eklemek için bu işlemi tekrarlayın.

1. Ardından, dağıtımı tamamlaması için [Azure 'Daki dağıtımlar](#bkmk_deploy-azure) sekmesine gidin.

1. Dağıtım tamamlandığında, site rolüne ek değişiklikler yapmak için Configuration Manager konsoluna gidin.

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a>Azure 'da dağıtımlar

1. Azure VM 'yi oluşturduktan sonra, araçtaki Azure sekmesinde **dağıtımlar** ' a geçiş yapın. Rolü varsayılan ayarlarla yapılandırmak için **Dağıt** ' ı seçin.

1. PowerShell betiğini başlatmak için **Çalıştır** ' ı seçin.

    [![Oluşturulan PowerShell betiğini çalıştırarak site rollerini dağıtma](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Daha fazla rol yapılandırmak için bu işlemi tekrarlayın.

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a>Mevcut bir sanal makine dağıtımına site rolleri ekleme
<!--5665775, 6307931-->
Configuration Manager sürüm 2002 ' den başlayarak, şirket içi siteyi genişletme ve geçirme Microsoft Azure Aracı, tek bir Azure sanal makinesinde birden çok site sistem rolü sağlamayı destekler. İlk Azure sanal makine dağıtımı tamamlandıktan sonra site sistemi rolleri ekleyebilirsiniz. Var olan bir sanal makineye yeni bir rol eklemek için aşağıdaki adımları uygulayın:
1. **Azure 'Daki dağıtımlar** sekmesinde, **tamamlandı** durumuna sahip bir sanal makine dağıtımına tıklayın.
1. Sanal makineye ek bir rol eklemek için **Yeni oluştur** düğmesine tıklayın.


## <a name="next-steps"></a>Sonraki adımlar

[Azure Portal](https://portal.azure.com) yaptığınız değişiklikleri gözden geçirin
