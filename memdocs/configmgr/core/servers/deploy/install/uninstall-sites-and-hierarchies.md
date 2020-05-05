---
title: Siteleri kaldır
titleSuffix: Configuration Manager
description: Rolleri kaldırma ve siteleri ve hiyerarşileri kaldırma kılavuzu
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718052"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>Configuration Manager roller, siteler ve Hiyerarşiler kaldırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager site sistem rolünü, sitesini veya hiyerarşisini kaldırmak için bu makaleyi kılavuz olarak kullanın.

Sürüm 2002 ' den başlayarak, merkezi yönetim sitesini (CA 'LAR) bir hiyerarşiden de kaldırabilir, ancak birincil siteyi tutabilirsiniz.

## <a name="site-system-role"></a><a name="bkmk_role"></a>Site sistemi rolü

Aşağıdaki nedenlerden dolayı bir rolü site sistem sunucusundan kaldırmak isteyebilirsiniz:

- Ağ veya fiziksel konumlar gibi daha geniş altyapı değişikliği
- Temel alınan sunucunun yetkisini alma
- Maliyetleri ve karmaşıklığı azaltmak için rolleri birleştirin
- Site rollerini yeniden yapılandırma veya yeniden tasarlama
- Rolün desteklediği özelliğin kullanımını durdur

Bir rolü kaldırmanız gerektiğine karar verirken öncelikle aşağıdaki sorulara verdiğiniz yanıtları göz önünde bulundurun:

- Hala sitede rol mi gerekiyor? Varsa, başka bir site sistemi rolü zaten var mı?

- Bu role sahip diğer site sistemleri performans ve kullanılabilirlik için iş gereksinimlerinizi destekleyecek şekilde boyutlandırılabilir mi?

- Tüm istemciler başka bir rolü kullanmak üzere zaten yeniden yapılandırılmış mı? Geri dönebilmeniz veya başka bir sunucu bulmadan varsayılan istemci davranışlarına göre mi kullanacaksınız?

### <a name="procedure-to-remove-a-site-system-role"></a>Site sistemi rolünü kaldırma yordamı

Bir rolü kaldırmak için aşağıdaki yordamı kullanın:

1. **Configuration Manager** konsolunda **Yönetim** çalışma alanına gidin. **Site yapılandırması**' nı genişletin ve ardından **sunucular ve site sistemi rolleri** düğümünü seçin.

1. Kaldırılacak rolün bulunduğu site sistem sunucusunu seçin. **Site sistem rolleri** Ayrıntılar bölmesinde hedef rolü seçin.

1. Şeritte **site** rolü **sekmesindeki site rolü grubunda** **rolü kaldır**' ı seçin. Rolü kaldırmak istediğinizi onaylayın.

### <a name="additional-information-for-specific-roles"></a>Belirli roller için ek bilgiler

Bazı rollerin ek adımlara ve konuları olabilir.

#### <a name="software-update-point"></a>Yazılım güncelleştirme noktası

Yazılım güncelleştirme noktasını kaldırdıktan sonra, Configuration Manager yazılım güncelleştirme noktasını listeden kaldırmak için istemci ilkesini güncelleştirir. Sitedeki son yazılım güncelleştirme noktasını kaldırdığınızda, yazılım güncelleştirme noktası listesi hiçbir yazılım güncelleştirme noktası içermez. Hiçbir rol yoksa, yazılım güncelleştirme yönetimi temelde sitede devre dışı bırakılır.

Birincil sitede birden fazla yazılım güncelleştirme noktanız olduğunda ve eşitleme kaynağı olan yazılım güncelleştirme noktasını kaldırdığınızda, yeni eşitleme kaynağı olacak sitede başka bir yazılım güncelleştirme noktası seçin.

## <a name="secondary-site"></a><a name="bkmk_secondary"></a>İkincil site  

[Bir hiyerarşiyi](#bkmk_hierarchy)kullanımdan kaldırırken, ikincil siteyi kaldırmanın ana nedeni ağ veya fiziksel konumlar gibi daha geniş bir altyapı değişikliğinden kaynaklanır. [İkincil site seçme](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary)nedenlerini de gözden geçirin.

İkincil bir siteyi kaldırmanız gerektiğine karar verirken öncelikle aşağıdaki sorulara verdiğiniz yanıtları göz önünde bulundurun:

- Site sunucusundan tüm site sistem rollerini kaldırdınız mı?

- İkincil siteyle ilişkili sınırlar veya sınır grupları mı var? Siteyi kaldırmadan önce sınırları yeniden yapılandırın.

- Tüm istemciler hala konumda mı?

- [Eş önbelleğe alma](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)gibi diğer içerik yönetimi seçeneklerini yapılandırdınız mı?

### <a name="options-to-delete-secondary-sites"></a>İkincil siteleri silme seçenekleri

İkincil bir siteyi başka bir birincil siteye taşıyamaz veya yeniden atayamazsınız. İkincil bir siteyi doğrudan üst sitesinden kaldırdığınızda, yüklemeyi kaldırmayı veya silmeyi seçin.

#### <a name="uninstall-the-secondary-site"></a>İkincil siteyi kaldır

Ağdan erişilebilen işlevsel bir ikincil siteyi kaldırmak için bu seçeneği kullanın. Bu seçenek, Configuration Manager ikincil site sunucusundan kaldırır. Daha sonra site ve kaynaklarıyla ilgili tüm bilgileri Configuration Manager sitesinden siler.

İkincil site için SQL Server Express Configuration Manager yüklüyse, Configuration Manager SQL Express 'i de kaldırır. İkincil siteyi yüklemeden önce SQL Server Express yüklediyseniz, Configuration Manager SQL Server Express kaldırmaz.

#### <a name="delete-the-secondary-site"></a>İkincil siteyi Sil

Aşağıdaki durumlarda bu seçeneği kullanın:

- Yüklenemedi

- Kaldırdıktan sonra, Configuration Manager konsolu ikincil siteyi hala gösteriyor

    Bu seçenek site ve kaynaklarıyla ilgili tüm bilgileri Configuration Manager hiyerarşisinden siler, ancak site sunucusunda herhangi bir değişiklik yapmaz.

    > [!TIP]
    >  İkincil bir siteyi silmek için Hiyerarşi Bakımı aracını **/DELSITE** seçeneğiyle de kullanabilirsiniz. Daha fazla bilgi için bkz. [hiyerarşi bakım aracı (Preinst. exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

### <a name="prerequisites-to-delete-a-secondary-site"></a>İkincil bir siteyi silme önkoşulları

Configuration Manager kurulumu 'nu çalıştıran yönetici kullanıcının aşağıdaki güvenlik haklarına ihtiyacı vardır:

- İkincil site sunucusunda yerel **yönetici** hakları

- Birincil site veritabanı sunucusu birincil site sunucusundan uzak ise, birincil site için uzak site veritabanı sunucusunda yerel **yönetici** hakları.

- Üst birincil sitede **Altyapı Yöneticisi** veya **tam yönetici** güvenlik rolü

- İkincil site veritabanında **sysadmin** hakları

### <a name="procedure-to-delete-a-secondary-site"></a>İkincil bir siteyi silme yordamı

İkincil bir siteyi kaldırmak veya silmek için aşağıdaki yordamı kullanın:

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.

1. Kaldırmak istediğiniz ikincil site sunucusunu seçin. Şeritte, **giriş** sekmesinde, **site** grubunda, **Sil**' i seçin.

1. **Genel** sayfasında, ikincil siteyi kaldırmayı veya silmeyi seçin.

1.  Sihirbazı tamamlayın.

## <a name="primary-site"></a><a name="bkmk_primary"></a>Birincil site  

Aşağıdaki nedenlerden dolayı hiyerarşinizden birincil bir siteyi kaldırmak isteyebilirsiniz:

- Maliyetleri ve karmaşıklığı azaltmak için siteleri birleştirin
- Hiyerarşinin sitelerini yeniden yapılandırın veya yeniden tasarlayabilirsiniz

CA 'lara yönelik çoğaltma bağlantısı için [Dağıtılmış görünümler](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) kullanan bir alt birincil siteyi kaldırmadan önce, hiyerarşinizdeki dağıtılmış görünümleri kapatın. Daha fazla bilgi edinmek için bkz. [Dağıtılmış görünümlerle yapılandırılan birincil siteyi kaldırma](#bkmk_distviews).

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a>Birincil siteyi kaldırmayı planlayın

Bir birincil siteyi kaldırmadan önce, aşağıdaki görevleri gözden geçirin:

- Sınırları, sınır gruplarını ve geri dönüş ilişkilerini gözden geçirin. İstemcileri yeni bir siteye atarsanız ancak sınırları değiştirmezseniz, bunlar dolaşım olarak düşünülebilir. Daha fazla bilgi için bkz. [site sınırlarını ve sınır gruplarını tanımlama](../configure/define-site-boundaries-and-boundary-groups.md).

- Tüm etkin istemcilerin hiyerarşideki başka bir birincil siteye yeniden atanmış olduğundan emin olun. Aksi takdirde, site kaldırıldıktan sonra istemciler yönetilmez. Daha fazla bilgi için bkz. [istemcileri bir siteye atama](../../../clients/deploy/assign-clients-to-a-site.md).

  - Yeni sitenin aynı hizmet düzeyini sağladığından emin olmak için site rollerinin listesini gözden geçirin.

  - Diğer site sistemlerini diğer sitede bu rolle doğru şekilde boyutlandırdığınızdan emin olun. Ek istemcilerle performans ve kullanılabilirlik için iş gereksinimlerinizi desteklemesi gerekecektir.

  - Bu sitede çok fazla istemci varsa, bunları aşamalar halinde yeniden atayın. İstemci tam envanteri ve diğer siteye özgü verileri yenilediği için veritabanı çoğaltmasını izleyin. Yazılım güncelleştirmelerini yönetiyorsanız, istemciler yeni bir yazılım güncelleştirme noktasına atanır. Bu davranış, güncelleştirme uyumluluğu için tam tarama oluşmasına neden olur.

  - İstemci yeniden atama, envanter verilerine ve durum tabanlı uyumluluğa dayanan raporları ve sorguları etkileyebilir. Geçiş sırasında istemci döngülerini geçici olarak ayarlamayı göz önünde bulundurun.

  - Hiçbirinin bu birincil siteye başvurmadığından emin olmak için tüm istemci atama yöntemlerini gözden geçirin.

- Hiyerarşide etkin olarak kullanılan herhangi bir nesnenin site koduna statik başvuruları olup olmadığını denetleyin. Örneğin, koleksiyon sorguları, görev dizileri veya yönetimsel betikler.

- Hiyerarşi otomatik site ataması için bir [geri dönüş sitesi](../configure/boundary-group-procedures.md#bkmk_site-fallback) kullanıyorsa, bu birincil siteye başvurbulunmadığından emin olun.

- Statik bir site koduna başvurmayan tüm [istemci yükleme yöntemlerini](../../../clients/deploy/plan/client-installation-methods.md) yeniden yapılandırın.

- Bu birincil sitede, siteye özgü, buluta bağlı herhangi bir hizmet varsa, bunları kaldırdığınızdan emin olun. Hala bulut kaynaklarına ihtiyacınız varsa, hiyerarşideki başka bir birincil siteye taşıyın. Kaldırmak istediğiniz birincil siteden kaldırın ve bunları başka bir birincil siteye ekleyin.

- Bu birincil sitede hiyerarşi için herhangi bir [bulma yöntemi](../configure/run-discovery.md) varsa, bunları başka bir siteye taşıyın.

- Site tabanlı [Işletim sistemi dağıtım medyasını](../../../../osd/deploy-use/create-task-sequence-media.md)devre dışı bırakın.

- Site ve site sunucusundan tüm site sistem rollerini kaldırın. Daha fazla bilgi için bkz. [site sistemi rollerini kaldırma](#bkmk_role). Bu hazırlık adımı gerekli olmasa da, site kaldırılmadan önce ek bağımlılıkların belirlenmesine yardımcı olur.

- Bu birincil sitenin altındaki tüm ikincil siteleri kaldırın. Daha fazla bilgi için [ikincil site](#bkmk_secondary) bölümüne bakın.

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a>Birincil siteyi kaldırma önkoşulları

Configuration Manager kurulumu 'nu çalıştıran yönetici kullanıcının aşağıdaki güvenlik haklarına ihtiyacı vardır:

- CAS sunucusunda yerel **yönetici** hakları

- CAS veritabanı sunucusu, site sunucusundan uzak ise, CA 'LAR için uzak site veritabanı sunucusunda yerel **yönetici** hakları.

- CAS site veritabanında **sysadmin** hakları

- Birincil site sunucusunda yerel **yönetici** hakları

- Birincil site veritabanı sunucusu birincil site sunucusundan uzak ise, birincil site için uzak site veritabanı sunucusunda yerel **yönetici** hakları.

- CAS üzerinde **Altyapı Yöneticisi** veya **tam yönetici** güvenlik rolü

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a>Birincil siteyi kaldırma yordamı

İlişkili ikincil sitesi olmayan birincil bir siteyi kaldırmak için Configuration Manager kurulumunu çalıştırırsınız. Birincil bir siteyi kaldırmak için aşağıdaki yordamı kullanın:

> [!TIP]
> Birincil site sunucusu artık kullanılamıyorsa, birincil siteyi site veritabanından silmek için CAS 'de Hiyerarşi Bakımı aracını kullanın. Daha fazla bilgi için bkz. [hiyerarşi bakım aracı (Preinst. exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

1. Aşağıdaki yöntemlerden birini kullanarak birincil site sunucusunda Configuration Manager kurulumunu başlatın:

    - **Başlat** menüsünde **Configuration Manager Kurulum**' u seçin.

    - Configuration Manager *yükleme medyası*dizininde öğesini açın `\SMSSETUP\BIN\X64\setup.exe`. Bu sürümün site sürümüyle aynı olduğundan emin olun.

    - Configuration Manager *yüklendiği*dizinde açın `\BIN\X64\setup.exe`.

1. **Başlamadan önce** sayfasındaki bilgileri gözden geçirin.

1. **Başlarken** sayfasında **Configuration Manager sitesini kaldır**' ı seçin.

    > [!IMPORTANT]  
    >  Birincil siteye bağlı ikincil bir site varsa, birincil siteyi kaldırabilmeniz için önce ikincil siteyi kaldırmanız gerekir.  

1. **Configuration Manager sitesini kaldırma** sayfasında, aşağıdaki seçeneklerden her ikisi de varsayılan olarak etkindir:

    - Site veritabanını birincil site sunucusundan kaldır
    - Configuration Manager konsolunu kaldırma

1. Configuration Manager birincil sitesini kaldırmayı onaylamak için **Evet** ' i seçin.

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a>Dağıtılmış görünümler kullanan bir birincil siteyi kaldırma

1. Bir alt birincil siteyi kaldırmadan önce, CA 'LAR ve birincil site arasındaki hiyerarşideki her bir bağlantıda dağıtılmış görünümleri kapatın.

1. Her bağlantıda dağıtılmış görünümleri kapattıktan sonra, birincil sitedeki verilerin CA 'larda yeniden başlatılmasına yönelik olduğunu onaylayın. Verilerin başlatılmasını izlemek için bkz. [çoğaltmayı izleme](../../manage/monitor-replication.md).

1. Veriler, CA 'LAR ile başarıyla yeniden başlatıldıktan sonra, [birincil siteyi kaldırabilirsiniz](#bkmk_pri-process).

1. Birincil site kaldırıldığında, CA 'lardan diğer birincil sitelere yapılan bağlantılardaki dağıtılmış görünümleri yeniden yapılandırabilirsiniz.

    > [!IMPORTANT]
    > Birincil siteyi her sitede dağıtılmış görünümleri kapatmadan önce kaldırırsanız veya birincil sitedeki veriler CA 'larda başarıyla yeniden başlatılmadan önce, veri çoğaltma başarısız olabilir.

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a>Hiyerarşinin yetkisini alma

Bazı kuruluşların birleşmeler, alımlar, test ortamları veya diğer iş gereksinimleri nedeniyle birden çok hiyerarşisi vardır. Yönetimi tek bir hiyerarşiye birleştirdiğinizde, bu eylem maliyetleri ve karmaşıklığı azaltmaya yardımcı olabilir. Hiyerarşinin yetkisini almaya yönelik başka bir nedenden dolayı, Microsoft Intune gibi yalnızca bulut yönetim hizmetine geçiş yapmanız ve şirket içi altyapınızı kaldırmaya hazırsınız.

Birden çok siteyle bir hiyerarşinin yetkisini almak için, kaldırma sırası önemlidir. Hiyerarşinin altındaki siteleri kaldırarak başlayın ve ardından yukarı doğru ilerleyin:

1. Birincil sitelere bağlı ikincil siteleri kaldırın.
2. Birincil siteleri kaldırın.
3. Tüm birincil siteleri kaldırdıktan sonra, CA 'ları kaldırabilirsiniz.

Daha fazla bilgi için aşağıdaki bölümlere bakın:

- [İkincil bir siteyi kaldırma](#bkmk_secondary)
- [Birincil siteyi kaldırma](#bkmk_primary)
- [CAS 'yi kaldırma](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a>CAS 'yi kaldırma

Hiyerarşinin yetkisini almak için son adım CA 'ları kaldırmadır. Alt birincil siteleri olmayan CA 'ları kaldırmak için Configuration Manager kurulumu 'nu çalıştırın.

#### <a name="prerequisites-to-uninstall-the-cas"></a>CA 'ları kaldırma önkoşulları

Configuration Manager kurulumu 'nu çalıştıran yönetici kullanıcının aşağıdaki güvenlik haklarına ihtiyacı vardır:

- CAS sunucusunda yerel **yönetici** hakları

- CAS veritabanı sunucusu, site sunucusundan uzak ise, CA 'LAR için uzak site veritabanı sunucusunda yerel **yönetici** hakları.

#### <a name="procedure-to-uninstall-the-cas"></a>CA 'ları kaldırma yordamı

1. Aşağıdaki yöntemlerden birini kullanarak CAS sunucusunda Configuration Manager kurulumunu başlatın:

    - **Başlat** menüsünde **Configuration Manager Kurulum**' u seçin.

    - Configuration Manager *yükleme medyası*dizininde öğesini açın `\SMSSETUP\BIN\X64\setup.exe`. Bu sürümün site sürümüyle aynı olduğundan emin olun.

    - Configuration Manager *yüklendiği*dizinde açın `\BIN\X64\setup.exe`.

1. **Başlamadan önce** sayfasındaki bilgileri gözden geçirin.

1. **Başlarken** sayfasında **Configuration Manager sitesini kaldır**' ı seçin.

    > [!IMPORTANT]  
    >  CAS 'yi kaldırabilmeniz için önce tüm alt birincil siteleri kaldırın.  

1. **Configuration Manager sitesini kaldırma** sayfasında, aşağıdaki seçeneklerden her ikisi de varsayılan olarak etkindir:

    - Site veritabanını CAS sunucusundan kaldır
    - Configuration Manager konsolunu kaldırma

1. Configuration Manager merkezi yönetim sitesini (CAS) kaldırmayı onaylamak için **Evet** ' i seçin.

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a>CAS 'yi kaldırma

<!-- 3607277 -->

Sürüm 2002 ' den başlayarak, hiyerarşi CAS ve tek bir alt birincil siteden oluşuyorsa, CA 'ları kaldırabilirsiniz. Bu eylem, Configuration Manager altyapınızı tek bir tek başına birincil siteye basitleştirir. Siteden siteye çoğaltmanın karmaşıklıklarını ortadan kaldırır ve yönetim görevlerinizi tek siteye odaklanır.

Daha fazla bilgi için bkz. [CA 'Ları kaldırma](remove-central-administration-site.md).
