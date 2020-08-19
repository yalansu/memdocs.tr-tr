---
title: CAS 'yi kaldır
titleSuffix: Configuration Manager
description: Configuration Manager altyapınızı tek bir tek başına birincil siteye kolaylaştırmak için merkezi yönetim sitesini (CAS) kaldırın.
ms.date: 06/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b8b7ee17077c859a1f0a9eb41c5f9d0857db550
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591519"
---
# <a name="remove-the-central-administration-site"></a>Merkezi yönetim sitesini kaldırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!-- 3607277 -->

Sürüm 2002 ' den başlayarak, hiyerarşi merkezi yönetim sitesinden (CAS) ve tek bir alt birincil siteden oluşuyorsa, CA 'ları kaldırabilirsiniz. Bu eylem, Configuration Manager altyapınızı tek bir tek başına birincil siteye basitleştirir. Siteden siteye çoğaltmanın karmaşıklıklarını ortadan kaldırır ve yönetim görevlerinizi tek siteye odaklanır.

> [!IMPORTANT]
> Bu Configuration Manager sürümünde bu özellik ön sürümdür ve varsayılan olarak etkinleştirilmemiştir. Microsoft Premier müşterileri için şu anda kullanılabilir.
>
> Bu özelliği etkinleştirmek için yardım için teknik hesap yöneticinize başvurun:
>
> - TAM hesabınız, Microsoft Premier saatlerinizi kullanacak bir danışmanlık durumu açar.
> - Büyük/küçük harf önem derecesini değiştiremezsiniz.
> - Microsoft Desteği, bu danışmanlık çalışmalarına normal, hafta içi iş saatlerinde yardımcı olacaktır.

## <a name="plan"></a>Planlama

- Hiyerarşinin CAS ve tek bir alt birincil siteden oluşması gerekir. Birincil site ikincil sitelere sahip olabilir. Diğer alt birincil siteleri hiyerarşiden kaldırmak için, [bir birincil siteyi kaldırmak](uninstall-sites-and-hierarchies.md#bkmk_primary)üzere planlama adımlarını ve önkoşulları gözden geçirin.

- Alt birincil sitenizin [tek başına birincil site](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri)için boyut ve ölçek gereksinimlerini karşıladığından emin olun.

- Hizmet bağlantı noktası ve yazılım güncelleştirme noktası dışında, CA 'larda Site rollerini taşıyın veya devre dışı bırakın. Configuration Manager Kurulum, CA 'ları kaldırdığınızda bu iki rolü işler.

  Aşağıdaki roller, CA 'larda en yaygın olarak birincil siteye devre dışı bırakmanız veya taşımanız gerekir:

  - Varlık Yönetim Bilgileri eşitleme noktası
  - Uç Nokta Koruma noktası
  - Raporlama hizmetleri noktası
  - Veri ambarı hizmet noktası
  - Bulut yönetimi ağ geçidi (CMG)

    > [!NOTE]
    > İçerik için CMG 'yi etkinleştirdiyseniz, birincil sitede CMG 'yi yeniden oluşturduktan sonra içeriği yeniden dağıtmanız Planlanın.<!-- 6608659 -->

- Dağıtılmış görünümleri kapatma

- Configuration Manager, Configuration Manager istemcisi gibi yerleşik paketlerin paket kaynak konumlarını otomatik olarak işler. CAS üzerinde bir paylaşma kullanmadığından emin olmak için diğer tüm içerik kaynak konumlarını gözden geçirin.

- Tüm etkin geçiş işlerini durdurun ve geçiş için tüm konfigürasyonları kaldırın. Daha fazla bilgi için bkz. [başka bir hiyerarşiden etkin geçişi durdurma](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy).

- Yazılım güncelleştirmeleri için otomatik dağıtım kuralları kullanıyorsanız, bunları alt birincil sitede yeniden oluşturun.

- [Üçüncü taraf yazılım güncelleştirmelerini](../../../../sum/deploy-use/third-party-software-updates.md)yönetmek için Configuration Manager veya System Center Updates Publisher KULLANıRSANıZ, WSUS IMZALAMA sertifikasını CAS üzerindeki yazılım güncelleştirme noktasından dışarı aktarın.

  - CAS 'yi kaldırmadan önce, üçüncü taraf yazılım güncelleştirmelerinin gerekli dağıtımlarının son tarihleri için bekleyin. İstemciler gerekli dağıtımlar için içeriği önceden indirir ve yazılım güncelleştirme noktasını değiştirdiğinizde, içerik karması, yazılım güncelleştirmelerinin *Yerel yayımlaması* ile değiştirilir. (Bu davranış diğer içerik türlerini etkilemez, yalnızca üçüncü taraf yazılım güncelleştirmelerinin yerel yayımlaması olur.) CAS 'yi bu gerekli dağıtımlara devam eden devam eden bir şekilde kaldırırsanız, karma uyumsuzluğu hatası olan istemcilerde başarısız olur.

- CA 'lara bağımlılığı olabilecek tüm üçüncü taraf yazılımları gözden geçirin.

## <a name="prerequisites"></a>Ön koşullar

- Configuration Manager kurulumu 'nu çalıştıran yönetici kullanıcının aşağıdaki güvenlik haklarına ihtiyacı vardır:

  - CAS sunucusunda yerel **yönetici** hakları

  - CAS veritabanı sunucusu, site sunucusundan uzak ise, CA 'LAR için uzak site veritabanı sunucusunda yerel **yönetici** hakları.

  - CAS site veritabanında **sysadmin** hakları

  - Birincil site sunucusunda yerel **yönetici** hakları

  - Birincil site veritabanı sunucusu birincil site sunucusundan uzak ise, birincil site için uzak site veritabanı sunucusunda yerel **yönetici** hakları.

  - Birincil site veritabanında **sysadmin** hakları

  - CAS ve birincil sitede **Altyapı Yöneticisi** veya **tam yönetici** güvenlik rolü

- Hiyerarşide yalnızca bir alt birincil site. Daha fazla bilgi için bkz. [birincil siteyi kaldırma](uninstall-sites-and-hierarchies.md#bkmk_primary).

## <a name="process"></a>İşlem

1. Aşağıdaki yöntemlerden birini kullanarak CAS sunucusunda Configuration Manager kurulumunu başlatın:

    - **Başlat** menüsünde **Configuration Manager Kurulum**' u seçin.

    - Configuration Manager *yükleme medyası*dizininde öğesini açın `\SMSSETUP\BIN\X64\setup.exe` . Bu sürümün site sürümüyle aynı olduğundan emin olun.

    - Configuration Manager *yüklendiği*dizinde açın `\BIN\X64\setup.exe` .

1. **Başlamadan önce** sayfasındaki bilgileri gözden geçirin.

1. **Başlarken** sayfasında, **Site bakımı yap veya bu siteyi sıfırla**' yı seçin.

1. **Site Bakımı** sayfasında **Merkezi yönetim sitesini kaldır**' ı seçin. <!-- or is it still "delete"? -->

1. **Var olan site sistemi rollerini yeniden yapılandırma** sayfasında:

    - **Hizmet bağlantı noktası**: Bu gerekli rolü barındırmak için birincil sitedeki site sisteminin tam etki alanı adını girin. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../configure/about-the-service-connection-point.md).

    - **Yazılım güncelleştirme noktası**: birincil sitede mevcut bir yazılım güncelleştirme noktası seçin. Kurulum, bu yazılım güncelleştirme noktasını CAS yapılandırmasıyla aynı şekilde eşitleyecek şekilde yapılandırır.

    Kurulum, belirtilen sunucuların önkoşulları karşıladığını denetler. Devam etmeye hazırsanız **Yüklemeyi Başlat** ' ı seçin.

Kurulum bir sorun genelinde geliyorsa, işlemi yeniden denemek için Sihirbazı kullanın.

Kurulum tamamlandığında, birincil siteyi sıfırlar. Daha fazla bilgi için bkz. [site sıfırlaması çalıştırma](../../manage/modify-your-infrastructure.md#bkmk_reset).

## <a name="monitor-and-verify"></a>İzleme ve doğrulama

Kurulum işlemi sırasında aşağıdaki günlükleri gözden geçirin:

- `C:\ConfigMgrSetup.log` CAS sunucusunda

- birincil site sunucusundaki Configuration Manager logs dizininde **HMAN. log**

Hiyerarşideki değişiklikleri görselleştirmek için **izleme** çalışma alanındaki **site hiyerarşisi** düğümünü kullanın. Örneğin, aşağıdaki grafik, **Shy** CAS, **Haw** birincil sitesi ve **VWT** ikincil sitesinin önceki ve sonraki karşılaştırılmasını göstermektedir:

| Önce  | Sonra   |
|---------|---------|
|![CAS, birincil sitenin ve ikincil sitenin örnek site hiyerarşisi görünümü](media/3607277-cas-primary-secondary.png)|![Birincil sitenin ve ikincil sitenin örnek site hiyerarşisi görünümü](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Kurulum sonrası görevler

CAS 'yi kaldırdıktan sonra, ortamınız için uygulanan aşağıdaki adımları gözden geçirin.

- CAS sunucusu bilgisayar hesabını birincil site yerel gruplarından el ile kaldırın.

- Ek eylemler gerektirebilecek, güvenilen kök anahtarı değişti:

  - İşletim sistemi dağıtımı önyükleme görüntülerini en son Configuration Manager ikili dosyaları içerecek şekilde güncelleştirin.

  - [Işletim sistemi dağıtım medyasını](../../../../osd/deploy-use/create-task-sequence-media.md)yeniden oluşturun.

- Configuration Manager [Azure izleyici](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=/mem/configmgr/core/context/core-context)ile bağlanıyorsanız, bağlantıyı sıfırlamanız gerekir. Sorunları çözecek ilk adım [gizli anahtarı yenilemeyecektir](../configure/azure-services-wizard.md#bkmk_renew). Bu sorunu çözmezse, bağlantıyı yeniden oluşturun.<!-- 5584635 -->

- Sürüm 2002 ' de yüzey sürücülerinin eşitlenmesini etkinleştirirseniz, CA 'ları kaldırdıktan sonra bu özelliği yeniden yapılandırın. Daha fazla bilgi için bkz. [Microsoft Surface Drivers ve bellenim Updates](../../../../sum/deploy-use/surface-drivers.md).<!-- 5728727 -->

- Üçüncü taraf yazılım güncelleştirmelerini yönetiyorsanız:

  1. Henüz yapmadıysanız, CA 'larda yazılım güncelleştirme noktasından WSUS imzalama sertifikasını dışarı aktarın.

  1. Yeni dağıtımlar oluşturmadan önce, mevcut dağıtımlardan ve yazılım güncelleştirme paketlerinden güncelleştirmeyi kaldırın.

  1. Yazılım güncelleştirme meta verilerini kullanılabilir bir duruma kurtarmak için, abone olunan katalogları yeniden eşitleyin. Ayrıca, Configuration Manager otomatik olarak yeniden eşitleme için de bekleyebilirsiniz.

  1. Configuration Manager, WSUS 'tan geçerli durumuyla güncelleştirmek için normal bir yazılım güncelleştirme eşitleme işlemini başlatın veya bekleyin. İsteğe bağlı olarak, güncelleştirmeleri silmek ve yeniden eklemek için SCUP veya WSUS PowerShell cmdlet 'lerini kullanın.

  1. Dağıtmanız gereken güncelleştirmelerin içeriğini yeniden yayımlayın.
