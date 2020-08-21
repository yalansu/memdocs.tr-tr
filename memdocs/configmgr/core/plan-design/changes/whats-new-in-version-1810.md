---
title: Sürüm 1810’daki yenilikler
titleSuffix: Configuration Manager
description: Geçerli dalın Configuration Manager sürüm 1810 ' de tanıtılan değişiklikler ve yeni yetenekler hakkında ayrıntılı bilgi alın.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 04630815b3d10a232d7fc0eea50296062c823194
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699849"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Geçerli dalın Configuration Manager sürüm 1810 ' deki yenilikler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı için güncelleştirme 1810, konsol içi bir güncelleştirme olarak sunulmaktadır. 1710, 1802 veya 1806 sürümünü çalıştıran sitelerde bu güncelleştirmeyi uygulayın. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> Bu makalede Configuration Manager, sürüm 1810 ' deki değişiklikler ve yeni özellikler özetlenmektedir.  

Bu güncelleştirmeyi yüklemek için her zaman en son denetim listesini gözden geçirin. Daha fazla bilgi için bkz. [güncelleştirme 1810 yükleme denetim listesi](../../servers/manage/checklist-for-installing-update-1810.md). Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist)de gözden geçirin.

Yeni Configuration Manager özelliklerinden yararlanmak için önce istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> Bu sayfa güncelleştirildikten sonra bildirim almak için aşağıdaki URL 'YI kopyalayıp RSS Akış okuyucunuzun içine yapıştırın: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Kullanımdan kaldırılan özellikler ve işletim sistemleri

[Kaldırılan ve kullanımdan kaldırılan öğelerde](deprecated/removed-and-deprecated.md)uygulanmadan önce yapılan değişiklikler hakkında bilgi edinin.

14 Ağustos 2018 ' den başlayarak, karma mobil cihaz yönetimi özelliği kullanım dışıdır. Daha fazla bilgi için bkz. [karma MDM 'ye ne oldu](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

Mac ve Linux için System Center Endpoint Protection (SCEP) desteği (tüm sürümler) 31 Aralık 2018 tarihinde sona erer. Mac için SCEP için yeni virüs tanımlarının kullanılabilirliği ve Linux için SCEP, destek sonuna kadar sonlandırılabilir. Daha fazla bilgi için bkz. [Destek Web günlüğü gönderisinin sonu](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).

Azure 'da klasik hizmet dağıtımları artık Configuration Manager kullanım dışıdır. Bulut yönetimi ağ geçidi ve bulut dağıtım noktası için Azure Resource Manager dağıtımlarını kullanmaya başlayın. Daha fazla bilgi için [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)konusuna bakın.



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site altyapısı

### <a name="support-for-windows-server-2019"></a>Windows Server 2019 için destek

<!--1359195-->
Configuration Manager artık Windows Server 2019 ve Windows Server, sürüm 1809 ' yi site sistemleri olarak desteklemektedir.

Daha fazla bilgi için bkz. [site sistemi sunucuları Için desteklenen işletim sistemleri](../configs/supported-operating-systems-for-site-system-servers.md).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Site sunucusu yüksek kullanılabilirlik için hiyerarşi desteği

<!--3607755, fka 1358224-->
Merkezi yönetim siteleri ve alt birincil siteler artık pasif modda ek bir site sunucusuna sahip olabilir.

Daha fazla bilgi için bkz. [site sunucusu yüksek kullanılabilirlik](../../servers/deploy/configure/site-server-high-availability.md).


### <a name="improvements-to-setup-prerequisites"></a>Kurulum önkoşulları geliştirmeleri

1810 sürümünü yüklediğinizde veya sürümüne güncelleştirdiğinizde, Configuration Manager Kurulum şimdi aşağıdaki önkoşul denetimlerini içerir veya geliştirir:

- **Sistemin yeniden başlatılması bekleniyor**: Bu önkoşul denetimi artık daha esnektir. Windows özellikleri için ek kayıt defteri anahtarlarını denetler. Daha fazla bilgi için bkz. [bekleyen sistem yeniden başlatması](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **SQL değişiklik izleme temizliği**: SITE veritabanının SQL değişiklik izleme verileri biriktirme listesine sahip olup olmadığı yeni bir denetim. Bu biriktirme listesini doğrulama ve temizleme yordamı dahil daha fazla bilgi için bkz. [SQL değişiklik izleme temizliği](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **SQL Native Client sürümü**: Bu önkoşul denetimi TLS 1,2 ' i destekleyen SQL Native Client sürümleri için güncelleştirilir. En düşük sürüm [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402)sürümüdür. Daha fazla bilgi için bkz. [SQL Native Client sürüm](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Windows küme düğümündeki site sistemi**: Configuration Manager Kurulum işlemi artık, yük devretme kümelemesi için Windows rolü olan bir bilgisayara site sunucusu rolünün yüklenmesini engeller. SQL Always on bu rolü gerektirir, bu nedenle daha önce site sunucusundaki site veritabanını birlikte bulunduramıyorsunuz. Bu değişiklik ile, SQL Always on ve site sunucusu ' nu pasif modda kullanarak daha az sunucu ile yüksek oranda kullanılabilir bir site oluşturabilirsiniz. Daha fazla bilgi için bkz. [Windows Yük devretme kümesi](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster). <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>İstemci bildirim eylemleri için yeni izin

<!--SCCMDocs-pr issue #2972-->
İstemci bildirim eylemleri artık SMS_Collection sınıfında **kaynağı bilgilendir** iznini gerektirir. Aşağıdaki yerleşik roller varsayılan olarak bu izne sahiptir:

- Tam Yönetici  
- Altyapı Yöneticisi  

Bu izni, istemci bildirimi eylemlerini kullanması gereken herhangi bir özel role ekleyin.

Daha fazla bilgi için bkz. [istemci bildirimleri](../../clients/manage/client-notification.md).



## <a name="content-management"></a><a name="bkmk_content"></a> İçerik yönetimi

### <a name="new-boundary-group-options"></a>Yeni sınır grubu seçenekleri

<!--1358749-->
Artık sınır grupları ortamınızda içerik dağıtımı üzerinde daha fazla denetim sağlamak için aşağıdaki ek ayarları içerir:

- **Aynı alt ağa sahip eş üzerinde dağıtım noktalarını tercih et**: varsayılan olarak, yönetim noktası, içerik konumları listesinin en üstündeki eş önbellek kaynaklarını önceliklendirir. Bu ayar eş önbellek kaynağıyla aynı alt ağda olan istemciler için bu önceliği tersine çevirir.  

- **Dağıtım noktaları üzerinden bulut dağıtım noktalarını tercih et**: daha hızlı bir internet bağlantısı olan bir şube ofisiniz varsa, artık bulut içeriğine öncelik verebilirsiniz.  

Daha fazla bilgi için bkz. [eş İndirmeleri Için sınır grubu seçenekleri](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Eş önbellek kaynak istemci sürümü için yönetim öngörüleri kuralı

<!-- 1358008 -->
**Yönetim öngörüleri** düğümü, bir eş önbellek kaynağı olarak hizmet veren ancak 1806 olmayan bir istemci sürümünden yükseltilmemiş istemcileri tanımlamak için yeni bir kural içerir. Yeni kural, **eş önbellek kaynaklarını Configuration Manager istemcisinin en son sürümüne yükseltir**ve yeni **proaktif bakım** kuralı grubunun bir parçasıdır. 1806 öncesi istemciler, sürüm 1806 veya üzerini çalıştıran istemciler için eş önbellek kaynağı olarak kullanılamaz. İstemci listesini görüntüleyen bir cihaz görünümü açmak için **Işlem yap** ' ı seçin.

Daha fazla bilgi için bkz. [Management Insights](../../servers/manage/management-insights.md).



## <a name="client-management"></a><a name="bkmk_client"></a> İstemci yönetimi

### <a name="new-client-notification-action-to-wake-up-device"></a>Cihazı Uyandırma için yeni istemci bildirim eylemi

<!--1317364-->
Artık istemci, site sunucusuyla aynı alt ağda olmasa bile Configuration Manager konsolundan istemcileri uyandırabilirsiniz. Bakım veya sorgu cihazları yapmanız gerekiyorsa, uykuda olan uzak istemcilerle sınırlı değilsiniz. Site sunucusu, aynı uzak alt ağda uyanık bir istemciyi tanımlamak için istemci bildirim kanalını kullanır. Uyuyan istemci daha sonra bir LAN 'da uyandırma isteği (Sihirli paket) gönderir.

Daha fazla bilgi için bkz. [LAN 'Da uyandırma 'Yı yapılandırma](../../clients/deploy/configure-wake-on-lan.md) ve [istemcileri uyandırma](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Cihazlar düğümünden istemci bildirimi gerçekleştirmeye yönelik yeni seçenek

<!--1317364-->
1810 tarihine kadar, **Istemci bildirim** seçeneği yalnızca cihaz koleksiyonu düğümünden veya bir cihaz koleksiyonunun üyeliğini görüntülerken kullanılabilir. Artık **cihazlar** düğümünden doğrudan bir **İstemci bildirimi** gerçekleştirmek mümkündür. Artık bir koleksiyon üyeliği görünümü içinde olması gerekmez.

Daha fazla bilgi için bkz. [istemci bildirimleri](../../clients/manage/client-notification.md).


### <a name="improvements-to-collection-evaluation"></a>Koleksiyon değerlendirmesine yönelik iyileştirmeler

<!--3607726, fka 1358981-->
Koleksiyon değerlendirme davranışında aşağıdaki değişiklikler site performansını iyileştirebilir:  

- Daha önce, sorgu tabanlı bir koleksiyonda bir zamanlama yapılandırdığınızda, **Bu koleksiyonda tam bir güncelleştirme zamanlamak**için koleksiyon ayarını etkinleştirmediyseniz, site sorguyu değerlendirmeye devam edebilir. Zamanlamayı tamamen devre dışı bırakmak için, zamanlamayı **none**olarak değiştirmeniz gerekiyordu. Artık bu ayarı devre dışı bıraktığınızda site zamanlamayı temizler. Koleksiyon değerlendirmesi için bir zamanlama belirtmek üzere **Bu koleksiyonda tam bir güncelleştirme zamanlama**seçeneğini etkinleştirin.  

- **Tüm sistemler**gibi yerleşik koleksiyonların değerlendirmesini devre dışı bırakamıyorum, ancak artık zamanlamayı yapılandırabilirsiniz. Bu davranış, bu eylemi iş gereksinimlerinizi karşılayan bir zamanda özelleştirmenize olanak sağlar.

Daha fazla bilgi için bkz. [koleksiyonlar oluşturma](../../clients/manage/collections/create-collections.md#bkmk_create).


### <a name="improvement-to-client-installation"></a>İstemci yüklemesine iyileştirme

<!--1358840-->
Configuration Manager istemcisi yüklenirken, CCMSetup işlemi, gerekli içeriğin yerini bulmak için yönetim noktasıyla iletişim kurar. Daha önce bu işlemde, yönetim noktası yalnızca istemcinin geçerli sınır grubundaki dağıtım noktalarını döndürür. Kullanılabilir içerik yoksa, kurulum işlemi yönetim noktasından içerik indirmeye geri döner. Gerekli içeriğe sahip olabilecek diğer sınır gruplarındaki dağıtım noktalarına geri döneme seçeneği yoktur. Artık yönetim noktası, sınır grubu yapılandırmasına bağlı olarak dağıtım noktaları döndürür.

Daha fazla bilgi için bkz. [sınır gruplarını yapılandırma](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup).



## <a name="co-management"></a><a name="bkmk_comgmt"></a> Ortak yönetim

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Ortak yönetilen cihazlar için gerekli uygulama uyumluluk ilkesi

<!--1358196-->
Gerekli uygulamalar için Configuration Manager uyumluluk ilkesi kurallarını tanımlayın. Bu uygulama değerlendirmesi, ortak yönetilen cihazlar için Microsoft Intune gönderilen genel uyumluluk durumunun bir parçasıdır.

Daha fazla bilgi için bkz. [ortak yönetim iş yükleri](../../../comanage/workloads.md).


### <a name="improvement-to-co-management-dashboard"></a>Ortak yönetim panosuna iyileştirme

<!--1358980-->
Ortak Yönetim Panosu, aşağıdaki daha ayrıntılı bilgilerle geliştirilmiştir:  

- **Ortak yönetim kayıt durumu** kutucuğu ek durumlar içerir

- Huni grafiği olan yeni bir **ortak yönetim durum** kutucuğu, kayıt işleminin durumlarını gösterir

- **Kayıt hatalarının** sayılarıyla yeni bir kutucuk

![En üstteki dört kutucuğu gösteren ortak yönetim panosu ekran görüntüsü](media/1358980-comgmt-dashboard.png)

Daha fazla bilgi için bkz. [Ortak Yönetim Panosu](../../../comanage/how-to-monitor.md#co-management-dashboard).


### <a name="improvements-to-internet-based-client-setup"></a>Internet tabanlı istemci kurulumu geliştirmeleri

<!--3607731, fka 1359181-->
Bu sürüm, internet üzerindeki istemciler için Configuration Manager istemci kurulum işlemini daha da basitleştirir. Site, bulut yönetimi ağ geçidine (CMG) ek Azure Active Directory (Azure AD) bilgileri yayımlar. Azure AD 'ye katılmış bir istemci, bu bilgileri Ccmsetup işlemi sırasında, katıldığı aynı kiracıyı kullanarak CMG 'den alır. Bu davranış, birden fazla Azure AD kiracısı olan bir ortamda cihazların ortak yönetime kaydedilmesini kolaylaştırır. Şimdi yalnızca iki zorunlu CCMSetup özelliği **CCMHOSTNAME** ve **smssitekodu**.

Daha fazla bilgi için bkz. [İnternet tabanlı cihazları ortak yönetim için hazırlama](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).



## <a name="application-management"></a><a name="bkmk_app"></a> Uygulama yönetimi

### <a name="convert-applications-to-msix"></a>Uygulamaları MALTıYA Dönüştür

<!--3607729, fka 1359029-->
Sürüm 1806 ' den başlayarak, Configuration Manager yeni Windows 10 uygulama paketi (. msix) biçiminin dağıtımını destekler. Artık mevcut Windows Installer (. msi) uygulamalarınızı MSIX biçimine dönüştürebilirsiniz.

Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).  


### <a name="repair-applications"></a>Uygulamaları onarma

<!--1357866-->
Windows Installer ve betik yükleyici dağıtım türleri için bir onarım komut satırı belirtin. Ardından, dağıtımda seçeneğini etkinleştirirseniz, yazılım merkezi 'nde uygulamayı **onarmak** için yeni bir düğme bulunur. Bir uygulamayı onarma programıyla yapılandırdığınızda, kullanıcılar komutu Software Center 'dan başlatabilir.

Daha fazla bilgi için bkz. [uygulama oluşturma](../../../apps/deploy-use/create-applications.md#bkmk_dt-content) ve [uygulama dağıtma](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Uygulama isteklerini e-postayla onaylama

<!--1321550-->
Uygulama onay istekleri için e-posta bildirimlerini yapılandırın. Bir Kullanıcı bir uygulama istediğinde, bir e-posta alırsınız. Configuration Manager konsolu gerekmeden isteği onaylamak veya reddetmek için e-postadaki bağlantılar ' a tıklayın.

Daha fazla bilgi için bkz. [uygulamaları onaylama](../../../apps/deploy-use/app-approval.md).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Algılama yöntemleri Windows PowerShell profillerini yüklemez

<!--3607762, fka 1359239-->
Yapılandırma öğelerindeki uygulamalar ve ayarlar üzerinde algılama yöntemleri için Windows PowerShell komut dosyalarını kullanabilirsiniz. Bu betikler istemcilerde çalıştığında, Configuration Manager istemcisi artık PowerShell 'i `-NoProfile` parametresiyle çağırır. Bu seçenek PowerShell 'i profil olmadan başlatır.

PowerShell profili, PowerShell başladığında çalışan bir betiktir. Ortamınızı özelleştirmek ve başlattığınız her PowerShell oturumuna oturuma özgü öğeler eklemek için bir PowerShell profili oluşturabilirsiniz.

> [!Note]  
> Bu davranış değişikliği [betikler](../../../apps/deploy-use/create-deploy-scripts.md) veya [CMPivot](../../servers/manage/cmpivot.md)için geçerlidir. Bu özelliklerin her ikisi de bu PowerShell parametresini zaten kullanıyor.  

Daha fazla bilgi için bkz. [uygulama oluşturma](../../../apps/deploy-use/create-applications.md) ve [özel yapılandırma öğeleri oluşturma](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).



## <a name="os-deployment"></a><a name="bkmk_osd"></a> İşletim sistemi dağıtımı

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Mevcut cihazlar için Windows Autopilot görev dizisi desteği

<!--3607717, fka 1358333-->
[Mevcut cihazlar Için Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) artık Windows 10, sürüm 1809 veya sonraki sürümlerde kullanılabilir. Bu yeni özellik, tek bir yerel Configuration Manager görev sırası kullanarak [Windows Autopilot Kullanıcı odaklı mod](/windows/deployment/windows-autopilot/user-driven) Için bir Windows 7 cihazını yeniden görüntülemenizi ve sağlamanızı sağlar.

Daha fazla bilgi için bkz. [Mevcut cihazlar için Windows Autopilot](../../../../autopilot/existing-devices.md).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Çevrimdışı işletim sistemi görüntüsü bakımı için sürücüyü belirtin

<!--1358924-->
Şimdi, işletim sistemi görüntülerine ve işletim sistemi yükseltme paketlerine yazılım güncelleştirmeleri eklerken Configuration Manager kullanacağı sürücüyü belirtin. Bu işlem geçici dosyalarla büyük miktarda disk alanı tüketebilir, bu nedenle kullanılacak sürücüyü seçme esnekliği sağlar.

Daha fazla bilgi için bkz. [OS görüntülerini yönetme](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive) veya [işletim sistemi yükseltme paketlerini yönetme](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Sınır grupları için görev dizisi desteği

<!--1359025-->
Bir cihaz bir görev dizisi çalıştırdığında ve içerik almaları gerektiğinde, artık Configuration Manager istemcisine benzer sınır grubu davranışları kullanır.

Daha fazla bilgi için bkz. [sınır grupları](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Sürücü Bakımı geliştirmeleri

<!--3607716, fka 1358270-->
Sürücü paketlerinin artık **üretici** ve **model**için ek meta veri alanları vardır. Bu alanları, genel muhasebe 'de yardım almak veya silebilecekleri eski ve yinelenen sürücüleri belirlemek için sürücü paketlerini etiketlemek üzere kullanın.

Daha fazla bilgi için bkz. [sürücüleri yönetme](../../../osd/get-started/manage-drivers.md).

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Windows 10 bakım planı filtrelerinde iyileştirmeler

<!--3098809, 3113836, 3204570 -->
Windows 10 bakım planlarına ek filtreler eklenmiştir. Artık **mimariye**, **ürün kategorisine**göre filtreleyerek ve yükseltmenin **yerini almıştır**.

Daha fazla bilgi için bkz. [Windows 10 bakım planı](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan).

### <a name="new-task-sequence-variable-for-last-action-name"></a>Son eylem adı için yeni görev sırası değişkeni

<!--SCCMDocs-pr issue #2964-->
Görev dizisi değişkeni ile birlikte _SMSTSLastActionRetCode, görev sırası da **_SMSTSLastActionName**yeni bir değişken ayarlar. Ayrıca, bu değeri Smsts. log dosyasına kaydeder. Bu yeni değişken, bir görev dizisinde sorun giderirken faydalıdır. Bir adım başarısız olduğunda, özel bir betik dönüş koduyla birlikte adım adını içerebilir.

Daha fazla bilgi için bkz. [görev dizisi değişkenleri](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName).



## <a name="software-updates"></a><a name="bkmk_sum"></a> Yazılım güncelleştirmeleri

### <a name="phased-deployment-of-software-updates"></a>Yazılım güncelleştirmelerinin aşamalı dağıtımı

<!--1358146-->
Yazılım güncelleştirmeleri için aşamalı dağıtımlar oluşturun. Aşamalı dağıtımlar, özelleştirilebilir ölçütlere ve gruplara göre düzenlenmiş, sıralı bir yazılım dağıtımını düzenlemenize olanak tanır.

Daha fazla bilgi için bkz. [aşamalı dağıtımlar oluşturma](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Yazılım güncelleştirmeleri için bakım pencerelerini geliştirme

<!--vso2839307-->
Aşağıdaki istemci ayarı, yazılım güncelleştirme grubu ' nda yazılım güncelleştirmeleri 'nin yükleme davranışını denetlemek için **yazılım güncelleştirmeleri** grubunda bulunur: **"yazılım güncelleştirmesi" bakım penceresi kullanılabilir olduğunda "tüm dağıtımlar" bakım penceresinde güncelleştirmelerin yüklenmesini etkinleştir**

Varsayılan olarak, bu seçenek mevcut davranışla tutarlı tutmak için **Hayır** ' dır. İstemcilerin yazılım güncelleştirmelerini yüklemek için diğer kullanılabilir bakım pencerelerini kullanmasına izin vermek için bunu **Evet** olarak değiştirin.

Daha fazla bilgi için bkz. [yazılım güncelleştirmeleri istemci ayarları](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint).


### <a name="improvement-to-software-updates-maintenance"></a>Yazılım güncelleştirme Bakımı geliştirmesi

<!--2839349-->
WSUS temizleme görevleri artık ikincil sitelerde çalışır. Süre dolma güncelleştirmeleri için WSUS temizliği çalışır ve yenisiyle değiştirilen güncelleştirmeler ikincil siteler için WSUS 'de reddedilir.

Daha fazla bilgi için bkz. [sürüm 1810 ' den başlayarak WSUS temizleme davranışı](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)

### <a name="improvement-to-software-update-supersedence-rules"></a>Yazılım güncelleştirme yerine geçme kurallarına iyileştirme

<!--3098809, 2977644-->
Artık özellik güncelleştirmeleri için yerine geçme kurallarını Özellik dışı güncelleştirmelerden ayrı olarak belirtebilirsiniz. Bu, Windows 10 istemcilerinize hizmet vermeyi tamamlanmadan önce Yükseltmelerinizin Configuration Manager kaldırılmayacağı anlamına gelir.

Daha fazla bilgi için, bkz. [Supersedence rules](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules).

## <a name="reporting"></a><a name="bkmk_report"></a> Rapor

### <a name="improvement-to-lifecycle-dashboard"></a>Yaşam döngüsü panosuna iyileştirme

<!--1358702-->
Ürün yaşam döngüsü panosu artık **System Center 2012 Configuration Manager ve üzeri**bilgilerini içerir.

Yeni bir rapor, **yaşam döngüsü 05A-ürün yaşam döngüsü panosu**da mevcuttur. Konsol içi pano olarak benzer bilgiler içerir.

Bu Pano hakkında daha fazla bilgi için bkz. [ürün yaşam döngüsü panosunu kullanma](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="improvement-to-data-warehouse"></a>Veri ambarına iyileştirme

<!--1358870-->
Artık site veritabanından veri ambarına daha fazla tablo aktarabilirsiniz. Bu değişiklik, iş gereksinimlerinize göre daha fazla rapor oluşturmanıza olanak sağlar.

Daha fazla bilgi için bkz. [veri ambarı](../../servers/manage/data-warehouse.md).



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager konsolu

### <a name="configuration-manager-administrator-authentication"></a>Configuration Manager yönetici kimlik doğrulaması

<!--1357013-->
Artık yöneticilerin Configuration Manager sitelere erişebileceği en düşük kimlik doğrulama düzeyini belirtebilirsiniz. Bu özellik, yöneticilerin Windows 'da gerekli düzeyiyle oturum açmasını zorlar. Bu ayarı yapılandırmak için, **Hiyerarşi ayarları**' nda **kimlik doğrulama** sekmesini bulun.

Daha fazla bilgi için bkz. [plan for SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth).


### <a name="support-center"></a>Destek Merkezi

<!--1357489-->
İstemci sorunlarını giderme, gerçek zamanlı günlük görüntüleme veya Configuration Manager istemci bilgisayarının durumunu daha sonra analiz edilmek üzere yakalama için destek merkezi 'ni kullanın. Destek Merkezi, birçok yönetici sorun giderme aracını birleştiren tek bir araçtır. Site sunucusunda, **CD. latest\SMSSETUP\Tools\SupportCenter** klasöründe bulunan destek merkezi yükleyicisini bulun.

Daha fazla bilgi için bkz. [Destek Merkezi](../../support/support-center.md).


### <a name="management-insights-dashboard"></a>Yönetim öngörüleri panosu

<!--1357979-->
**Yönetim öngörüleri** düğümü artık grafik panosu içerir. Bu Pano, kural durumlarına genel bir bakış gösterir, bu da ilerlemenizi göstermenizi kolaylaştırır. Pano aşağıdaki kutucukları içerir:

- **Management Insights dizini**: yönetim öngörüleri kurallarında genel ilerleme durumunu izler. Dizin ağırlıklı bir ortalamadır. Kritik kurallar en çok değer taşır. Bu dizin, isteğe bağlı kurallara en az ağırlığı verir.  

- **Yönetim öngörüleri grupları**: her bir gruptaki kuralların yüzdesini gösterir.  

- **Management Insights önceliği**: kuralların önceliğe göre yüzdesini gösterir.  

- **Tüm Öngörüler**: öncelik ve durum dahil olmak üzere Öngörüler tablosu.  

![Yönetim öngörüleri panosunun ekran görüntüsü](media/1357979-management-insights-dashboard.png)

Daha fazla bilgi için bkz. [Management Insights](../../servers/manage/management-insights.md).


### <a name="improvements-to-cmpivot"></a>CMPivot geliştirmeleri

<!--1359068-->
CMPivot aşağıdaki geliştirmeleri içerir:

- **Sık kullanılan** sorguları Kaydet  

- Sorgu Özeti sekmesinde, başarısız veya çevrimdışı cihazların sayısını seçin ve ardından **koleksiyon oluşturma**seçeneğini belirleyin.

CMPivot için ek performans ve sorun giderme geliştirmeleri hakkında daha fazla bilgi için bkz. [betiklerin geliştirmeleri](#bkmk_scripts).

CMPivot hakkında daha fazla bilgi için bkz. [CMPivot](../../servers/manage/cmpivot.md).


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a> Betiklerin geliştirmeleri

<!--1358239-->
Artık ham veya yapılandırılmış JSON biçiminde ayrıntılı betik çıktısını görüntüleyebilirsiniz. Bu biçimlendirme, çıktının okunmasını ve çözümlenmesini kolaylaştırır.

Aşağıdaki performans ve sorun giderme geliştirmeleri, hem CMPivot hem de betikler için geçerlidir:

- Güncelleştirilmiş istemciler, bir hızlı iletişim kanalı üzerinden siteye 80 KB 'tan daha az çıkış döndürüyor. Bu değişiklik, betik veya sorgu çıkışını görüntüleme performansını artırır.  

- Sorun giderme için ek Günlükler  

Daha fazla bilgi için aşağıdaki makaleleri inceleyin:  

- [Configuration Manager konsolundan PowerShell betikleri oluşturun ve çalıştırın](../../../apps/deploy-use/create-deploy-scripts.md)  

- [CMPivot sorunlarını giderme](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>SMS sağlayıcı API 'SI

<!--3607711, fka 1321523-->
SMS sağlayıcısı artık, **Yönetim hizmeti**olarak adlandırılan https üzerinden WMI 'ya salt okunurdur. Bu REST API, siteden bilgilere erişmek için özel bir Web hizmetinin yerine kullanılabilir.

**SMS sağlayıcısı** , bulut yönetimi ağ geçidi üzerinden iletişime izin veren bir seçeneğe sahip bir rol olarak görünür. Bu ayar için geçerli kullanım, uzak bir cihazdan e-posta aracılığıyla uygulama onaylarını etkinleştirmektir.

Daha fazla bilgi için bkz. [plan for SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Şirket içi MDM

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Yeni şirket içi MDM dağıtımları için bir Intune bağlantısı artık gerekli değildir

<!--1359124-->
Microsoft Intune aboneliğini yapılandırmak için şirket içi MDM önkoşulu artık Yeni dağıtımlar için gerekli değildir. Kuruluşunuz hala bu özelliği kullanmak için Intune lisansları istiyor. Şu anda mevcut şirket içi MDM dağıtımlarından Intune bağlantısını kaldıramazsınız. Daha fazla bilgi için bkz. [Intune destek blog gönderisi](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Diğer güncelleştirmeler

Bu sürüm, yeni özelliklerden başlayarak hata düzeltmeleri gibi ek değişiklikler de içerir. Daha fazla bilgi için bkz. [Configuration Manager geçerli daldaki değişikliklerin özeti, sürüm 1810](https://support.microsoft.com/help/4482169).

Configuration Manager için Windows PowerShell cmdlet 'lerinde yapılan değişiklikler hakkında daha fazla bilgi için bkz. [PowerShell sürüm 1810 sürüm notları](/powershell/sccm/1810-release-notes?view=sccm-ps).

Aşağıdaki güncelleştirme paketi (4488598) konsolunda 25 Mart 2019 tarihinden itibaren Mart 'ta kullanılabilir: [güncelleştirme paketi 2 Configuration Manager geçerli dalı, sürüm 1810](https://support.microsoft.com/help/4488598). Bu, önceki güncelleştirme paketinin yerini alır, KB 4486457.


### <a name="hotfixes"></a>Düzeltmeler

Aşağıdaki ek düzeltmeler belirli sorunları ele almak için kullanılabilir:

| ID | Başlık | Tarih | Konsol içi |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune bağlayıcı sertifikası Configuration Manager yenilemez | 18 Ocak 2019 | Evet |
| [4490434](https://support.microsoft.com/help/4490434) | Configuration Manager içinde yinelenen Kullanıcı keşfi sütunları oluşturuldu | 22 Şubat 2019 | Evet |
| [4490575](https://support.microsoft.com/help/4490575) | Güncelleştirme yüklemeleri yanıt vermeyi durdurur veya Configuration Manager, sürüm 1810 ' de hiçbir şekilde tamamlanmayı göstermez | 22 Şubat 2019 | Evet |


## <a name="next-steps"></a>Sonraki adımlar

Bu sürümü yüklemeye hazırsanız, [güncelleştirme 1810 ' i yüklemek için](../../servers/manage/checklist-for-installing-update-1810.md) [Configuration Manager güncelleştirmeleri](../../servers/manage/updates.md) ve denetim listesini yükleme bölümüne bakın.

> [!TIP]  
> Yeni bir site yüklemek için Configuration Manager temel bir sürümünü kullanın.  
>
> Aşağıdakiler hakkında daha fazla bilgi edinin:
>
> - [Yeni siteleri yükleme](../../servers/deploy/install/installing-sites.md)  
> - [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)  

Bilinen, önemli sorunlar için bkz. [sürüm notları](../../servers/deploy/install/release-notes.md).

Bir siteyi güncelleştirdikten sonra [güncelleştirme sonrası denetim listesini](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist)de gözden geçirin.