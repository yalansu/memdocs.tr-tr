---
title: Koleksiyonları Yönet
titleSuffix: Configuration Manager
description: Configuration Manager içinde ortak koleksiyonlar yönetim görevleri yapın.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 063ce963e805651ffd795e830d2b21dfed6fc043
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693140"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Configuration Manager koleksiyonları yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager içindeki koleksiyonlara yönelik yönetim görevlerini gerçekleştirmenize yardımcı olması için bu makaledeki genel bakış bilgilerini kullanın.  

> [!NOTE]  
>  Configuration Manager koleksiyonlarının nasıl oluşturulacağı hakkında daha fazla bilgi için bkz. [koleksiyonları oluşturma](create-collections.md).



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a> Cihaz koleksiyonlarını yönetme  

**Varlıklar ve Uyumluluk** çalışma alanında **Cihaz Koleksiyonları**’nı, yönetilecek koleksiyonu seçin ve ardından bir yönetim görevini seçin.  


#### <a name="show-members"></a>Üyeleri Göster
**Cihazlar** düğümü altındaki geçici bir düğümde seçili koleksiyonun üyeleri olan tüm kaynakları gösterir.


#### <a name="add-selected-items"></a>Seçili Öğeleri Ekle
Aşağıdaki seçenekleri sağlar: 

- **Seçili öğeleri mevcut cihaz koleksiyonuna Ekle**: **Koleksiyon Seç** iletişim kutusunu açar. Seçili koleksiyonun üyelerini eklemek istediğiniz koleksiyonu seçin. Seçili koleksiyon bir **Koleksiyon Ekle** üyelik kuralı kullanılarak bu koleksiyona dahil edilir.  

- **Seçili öğeleri yeni cihaz koleksiyonuna Ekle**: yeni bir koleksiyon oluşturabileceğiniz **cihaz koleksiyonu oluşturma Sihirbazı** ' nı açar. Seçili koleksiyon bir **Koleksiyon Ekle** üyelik kuralı kullanılarak bu koleksiyona dahil edilir.  


Daha fazla bilgi için bkz. [koleksiyonlar oluşturma](create-collections.md).


#### <a name="install-client"></a>İstemci Yükle
**Istemci yüklemesi Sihirbazı**' nı açar. Bu sihirbaz, Seçili koleksiyondaki tüm bilgisayarlara bir Configuration Manager istemcisi yüklemek için client push yüklemesi kullanır. Daha fazla bilgi için bkz. [Client Push yüklemesi](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


#### <a name="run-script"></a>Betiği Çalıştır
Koleksiyondaki tüm istemcilerde bir PowerShell Betiği çalıştırmak için **Betiği Çalıştır** sihirbazını açar. Daha fazla bilgi için bkz. [PowerShell betikleri oluşturma ve çalıştırma](../../../../apps/deploy-use/create-deploy-scripts.md).


#### <a name="manage-affinity-requests"></a>Benzeşim İsteklerini Yönet
**Kullanıcı cihaz benzeşimi Isteklerini Yönet** iletişim kutusunu açar. Seçili koleksiyondaki cihazlar için Kullanıcı cihaz benzeşimleri oluşturmak üzere bekleyen istekleri onaylayın veya reddedin. Daha fazla bilgi için bkz. [Kullanıcı cihaz benzeşimi ile kullanıcıları ve cihazları bağlama](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)


#### <a name="clear-required-pxe-deployments"></a>Gerekli PXE Dağıtımlarını Temizle
Seçili koleksiyonun tüm üyelerinden gerekli PXE önyükleme dağıtımlarını siler. Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak IÇIN PXE kullanma](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).


#### <a name="update-membership"></a>Üyeliği Güncelleştir
Seçili koleksiyon için üyeliği değerlendirir. Çok sayıda üye içeren koleksiyonlar için bu güncelleştirmenin tamamlanması biraz zaman alabilir. Güncelleştirme tamamlandıktan sonra ekranı yeni koleksiyon üyeleriyle güncelleştirmek için **Yenile** eylemini kullanın.


#### <a name="add-resources"></a>Kaynak Ekle
**Koleksiyona Kaynak Ekle** iletişim kutusunu açar. Seçili koleksiyona eklemek üzere yeni kaynakları arayın. Güncelleştirme devam ederken seçili koleksiyonun simgesi kum saati sembolünü görüntüler.


#### <a name="client-notification"></a>İstemci Bildirimi
Daha fazla bilgi için bkz. [istemci bildirimleri](../client-notification.md).


#### <a name="endpoint-protection"></a>Uç Nokta Koruma
Daha fazla bilgi için bkz. [istemci bildirimleri](../client-notification.md).


#### <a name="export"></a>Dışarı Aktarma
Bu koleksiyonu bir Yönetilen Nesne Biçimi (MOF) dosyasına dışarı aktarmanıza yardımcı olan **koleksiyonu dışarı aktarma Sihirbazı** ' nı açar. Bu dosya daha sonra arşivlenebilir veya başka bir Configuration Manager sitesinde içeri aktarılabilir. Bir koleksiyonu dışarı aktardığınızda, başvurulan koleksiyonlar dışa aktarılmaz. Başvurulan bir koleksiyona, **ekleme** veya **dışlama** kuralı kullanılarak seçilen koleksiyon tarafından başvuruluyor.


#### <a name="copy"></a>Kopyala
Seçili koleksiyonun bir kopyasını oluşturur. Yeni koleksiyon, seçili koleksiyonu bir sınırlama koleksiyonu olarak kullanır.


#### <a name="refresh"></a>Yenile
Görünümü yenileyin.


#### <a name="delete"></a>Sil
Seçili koleksiyonu siler. Ayrıca, koleksiyondaki kaynakların tümünü site veritabanından silebilirsiniz. 

Configuration Manager yerleşik olan koleksiyonları silemezsiniz. Yerleşik koleksiyonların bir listesi için bkz. [koleksiyonlara giriş](introduction-to-collections.md#built-in-collections).


#### <a name="simulate-deployment"></a>Dağıtımı Benzet
**Uygulama dağıtımı benzetimi Sihirbazı**' nı açar. Bu sihirbaz, uygulamayı yüklemeden veya kaldırmadan uygulama dağıtımının sonuçlarını test etmenizi sağlar. Daha fazla bilgi için bkz. [uygulama dağıtımlarının benzetimini yapma](../../../../apps/deploy-use/simulate-application-deployments.md).


#### <a name="deploy"></a>Dağıtma
Şu seçeneklerini gösterir:  

- **Uygulama**: **Yazılım Dağıtma Sihirbazı**' nı açar. Seçili koleksiyonda bir uygulama dağıtımını seçin ve yapılandırın. Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../../../apps/deploy-use/deploy-applications.md).  

- **Program**: **Yazılım Dağıtma Sihirbazı**' nı açar. Seçilen koleksiyonda bir paket ve program dağıtımı seçin ve yapılandırın. Daha fazla bilgi için bkz. [paketler ve programlar](../../../../apps/deploy-use/packages-and-programs.md).  

- **Yapılandırma temeli**: **yapılandırma temellerini dağıt** iletişim kutusunu açar. Seçili koleksiyona bir veya daha fazla yapılandırma temellerinin dağıtımını yapılandırın. Daha fazla bilgi için bkz. [yapılandırma temelleri nasıl dağıtılır](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  

- **Görev sırası**: **Yazılım Dağıtma Sihirbazı**' nı açar. Seçili koleksiyona bir görev dizisi dağıtımı seçin ve yapılandırın. Daha fazla bilgi için bkz. [görevleri otomatikleştirmek için görev dizilerini yönetme](../../../../osd/deploy-use/deploy-a-task-sequence.md).  

- **Yazılım güncelleştirmeleri**: **yazılım güncelleştirmelerini dağıtma Sihirbazı**' nı açar. Seçili koleksiyondaki kaynaklara yazılım güncelleştirmeleri dağıtımını yapılandırın. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini yönetme](../../../../sum/understand/software-updates-introduction.md).  


#### <a name="clear-server-group-deployment-locks"></a>Sunucu grubu dağıtım kilitlerini temizle
Koleksiyon için tüm sunucu grubu dağıtım kilitlerini el ile serbest bırakın. Daha fazla bilgi için bkz. [sunucu grubuna hizmet](../../../../sum/deploy-use/service-a-server-group.md).


#### <a name="move"></a>Taşı
Seçili koleksiyonu, **Cihaz Koleksiyonları** düğümündeki başka bir klasöre taşıyın. 


#### <a name="properties"></a>Özellikler
Daha fazla bilgi için bkz. [koleksiyon özellikleri](#BKMK_CollProp).  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a> Kullanıcı koleksiyonlarını yönetme  

**Varlıklar ve Uyumluluk** çalışma alanında **Kullanıcı Koleksiyonları**’nı, yönetilecek koleksiyonu ve ardından bir yönetim görevini seçin.  

> [!Note]  
> Aşağıdaki eylemler Kullanıcı koleksiyonlarında bulunur, ancak davranışları cihaz koleksiyonlarıyla aynı. Bunlar, Kullanıcı koleksiyonları ve içindeki kullanıcılar için geçerlidir. Daha fazla bilgi için bkz. [cihaz koleksiyonlarını yönetme](#bkmk_device)bölümünde ilgili eylem.  

- **Üyeleri Göster**  
- **Seçili Öğeleri Ekle**  
    - **Seçili öğeleri mevcut kullanıcı koleksiyonuna Ekle**  
    - **Seçili öğeleri yeni kullanıcı koleksiyonuna Ekle**  
- **Benzeşim İsteklerini Yönet**  
- **Üyeliği Güncelleştir**  
- **Kaynak Ekle**  
- **Dışarı Aktarma**  
- **Kopyala**  
- **Yenile**  
- **Silme**  
- **Dağıtımı Benzet**  
- **Dağıtma**  
    - **Uygulama**  
    - **Program**  
    - **Yapılandırma temeli**
- **Taşı**  
- **Özellikler**


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> Koleksiyon özellikleri  

Bir koleksiyonun **Özellikler** iletişim kutusunu açtığınızda, aşağıdaki seçenekleri görüntüleyin ve yapılandırın:  

#### <a name="general"></a>Genel
Koleksiyon adı ve sınırlayıcı koleksiyon dahil olmak üzere seçili koleksiyon hakkındaki genel bilgileri görüntüleyin ve yapılandırın.

#### <a name="membership-rules"></a>Üyelik Kuralları
Bu koleksiyonun üyeliğini tanımlayan üyelik kurallarını yapılandırın. Daha fazla bilgi için bkz. [koleksiyonlar oluşturma](create-collections.md).  

#### <a name="power-management"></a>Güç Yönetimi
Seçili koleksiyondaki bilgisayarlara atadığınız güç yönetimi planlarını yapılandırın. Daha fazla bilgi için bkz. [güç yönetimine giriş](../power/introduction-to-power-management.md).  

#### <a name="deployments"></a>Dağıtımlar
Seçilen koleksiyonun üyelerine dağıttığınız tüm yazılımları görüntüler.  

#### <a name="maintenance-windows"></a>Bakım Pencereleri
Seçili koleksiyonun üyelerine uygulanan bakım pencerelerini görüntüleyin ve yapılandırın. Daha fazla bilgi için bkz. [bakım pencerelerini kullanma](use-maintenance-windows.md).

#### <a name="collection-variables"></a>Koleksiyon Değişkenleri
Bu koleksiyona uygulanan ve görev dizileri tarafından kullanılabilen değişkenleri yapılandırın. Daha fazla bilgi için bkz. [görev dizisi değişkenlerini ayarlama](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set).  

#### <a name="distribution-point-groups"></a>Dağıtım Noktası Grupları
Bir veya daha fazla dağıtım noktası grubunu seçili koleksiyonun üyeleriyle ilişkilendirin. Daha fazla bilgi için bkz. [içeriği ve içerik altyapısını yönetme](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md).

#### <a name="aad-group-sync"></a>AAD grubu eşitleme
Koleksiyon üyeliği sonuçlarını Azure Active Directory gruplarıyla eşitler. Bu eşitleme sürüm 1906 ' den başlayarak [yayın öncesi bir özelliktir](../../../servers/manage/pre-release-features.md) . Daha fazla bilgi için bkz. [koleksiyon oluşturma](create-collections.md#bkmk_aadcollsync).

#### <a name="security"></a>Güvenlik
İlişkili roller ve güvenlik kapsamlarından seçili koleksiyon için izinlere sahip yönetici kullanıcıları görüntüler. Daha fazla bilgi için bkz. [rol tabanlı yönetimin temelleri](../../../understand/fundamentals-of-role-based-administration.md).  

#### <a name="alerts"></a>Uyarılar 
İstemci durumu ve Endpoint Protection için uyarıların ne zaman oluşturulduğunu yapılandırın. Daha fazla bilgi için bkz. [istemci durumunu yapılandırma](../../deploy/configure-client-status.md) ve [Endpoint Protection izleme](../../../../protect/deploy-use/monitor-endpoint-protection.md).  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> PowerShell 'i kullanma

PowerShell, koleksiyonları yönetmek için kullanılabilir.  Daha fazla bilgi için bkz.

* [-CMCollection 'ı al](/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)
* [-CMCollection 'ı Kopyala](/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](/powershell/module/configurationmanager/import-cmcollection)
* [Dışarı aktarma-CMCollection](/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-Cmcollectiontoyönetitiveuser](/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)