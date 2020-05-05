---
title: Sürüm 2012 ' den değişiklikler
titleSuffix: Configuration Manager
description: Configuration Manager 'da Configuration Manager ve yeni özellikleri, System Center 2012 göre belirler.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720831"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>System Center 2012 ' den nelerin değiştirilmesi Configuration Manager

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçerli dalı, System Center 2012 Configuration Manager önemli değişiklikleri sunmaktadır. Bu makalede, geçerli dalın Configuration Manager özgün temel 1511 sürümünde bulunan önemli değişiklikler ve yeni yetenekler tanımlanmaktadır. Configuration Manager yönelik son güncelleştirmelerde tanıtılan değişiklikler hakkında bilgi edinmek için, bkz. [Configuration Manager artımlı sürümlerindeki](whats-new-incremental-versions.md)yenilikler.

> [!NOTE]
> Sürüm 1910 ' den başlayarak Configuration Manager artık Microsoft Endpoint Manager 'ın bir parçasıdır. Daha fazla bilgi için bkz. [Microsoft uç noktası Configuration Manager](whats-new-in-version-1910.md#bkmk_mem).

Configuration Manager Aralık 2015 sürümü (sürüm 1511), Microsoft 'un geçerli Configuration Manager ürününün ilk sürümüdür. Genellikle Configuration Manager geçerli dal olarak adlandırılır. *Geçerli dal* , bu sürümün ürüne yönelik Artımlı güncelleştirmeleri desteklediğini gösterir. Ayrıca, bu sürüm ve önceki Configuration Manager sürümlerini ayırt etmenin bir yolunu sunar.  

Geçerli dalı Configuration Manager:  

- Ürün adında yıl veya ürün tanımlayıcısı kullanmaz. Configuration Manager 2007 veya System Center 2012 Configuration Manager gibi geçmiş sürümlerden farklı olarak.  

- Güncelleştirme sürümleri olarak da adlandırılan, artımlı ve ürün içi güncelleştirmeleri destekler. İlk sürüm 1511 sürümüdür. Sonraki sürümler, sürüm 1910 gibi konsol içi güncelleştirmeler olarak bir yılda birkaç kez yayımlanır.  

- , Temel bir sürüm kullanılarak yüklenir. 1511 özgün temel sürüm olduğundan, yeni temel sürümler aynı zamanda, 2002 gibi bir zamana göre de serbest bırakılır. Temel sürümler yeni bir Configuration Manager sitesi ve hiyerarşisi yüklemek ya da System Center 2012 Configuration Manager desteklenen bir sürümünden yükseltmek için kullanılabilir.  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a>Konsol içi güncelleştirmeler

Configuration Manager **, güncelleştirmeler ve bakım** adlı, önerilen güncelleştirmelerin yerini bulmayı ve yüklemeyi kolaylaştıran konsol içi bir hizmet yöntemi kullanır.  

Bazı sürümler yalnızca Configuration Manager konsolu içinden mevcut siteler için güncelleştirmeler olarak kullanılabilir. Bu güncelleştirmeleri yeni bir Configuration Manager sitesini yüklemek için kullanamazsınız. Örneğin, 1910 güncelleştirmesi yalnızca Configuration Manager konsolundan kullanılabilir. Zaten desteklenen bir Configuration Manager sürümünü çalıştıran bir siteyi güncelleştirmek için kullanılır.

Düzenli aralıklarla, bir güncelleştirme sürümü de yeni bir *temel* sürüm olarak yayımlanır. Örneğin, güncelleştirme sürümü 2002 de bir temeldir. Yeni bir site veya hiyerarşi yüklemek için temel sürümü kullanın. 1802 gibi eski bir temel sürüm ile başlamamayın ve en güncel sürüme yükseltin. Her zaman en son taban çizgisini kullanın.

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Configuration Manager güncelleştirmeleri](../../servers/manage/updates.md)
- [Temel ve güncelleştirme sürümleri](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a>Hizmet bağlantı noktası  

Geçerli dalı Configuration Manager, **hizmet bağlantı noktası**olan yeni bir site sistemi rolü içerir:  

- Bulut özellikli birçok özellik için bir iletişim noktası

- Siteniz için güncelleştirmeleri indirir

- Siteniz hakkında tanılama ve kullanım verilerini Microsoft bulutuna yükler

Bu site sistemi rolü hem çevrimiçi hem de çevrimdışı işlem modlarını destekler. Daha fazla bilgi için bkz. [hizmet bağlantı noktası hakkında](../../servers/deploy/configure/about-the-service-connection-point.md).  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a>Tanılama ve kullanım verileri

Configuration Manager siteleriniz ve altyapınız hakkında tanılama ve kullanım verileri toplar. Bu bilgiler, hizmet bağlantı noktası tarafından derlenip Microsoft bulut hizmetine gönderilir. Configuration Manager, bu verilerin ortamınız için geçerli olan güncelleştirmeleri indirmesini gerektirir. Hizmet bağlantı noktasını ayarlarken, hem topladığı veri düzeyini hem de otomatik olarak (çevrimiçi) veya el ile (çevrimdışı) verileri göndermeyeceğinizi belirtebilirsiniz.

Daha fazla bilgi için bkz. [Tanılama ve kullanım verileri](../diagnostics/diagnostics-and-usage-data.md).  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a> Kullanım dışı işlev  

[Intel Active Management Technology (AMT)](#bkmk_AMT) tabanlı bilgisayarlar Için yerel destek gibi bazı özellikler Configuration Manager konsolundan kaldırılır. Ağ erişim koruması gibi diğer özellikler tamamen kaldırılır. Ayrıca, Windows Vista, Windows Server 2008 ve SQL Server 2008 gibi bazı eski Microsoft ürünleri artık desteklenmemektedir.  

Kullanım dışı bırakılan özelliklerin bir listesi için bkz. [kaldırılan ve kullanım dışı öğeler](deprecated/removed-and-deprecated.md).  

Desteklenen Ürünler, işletim sistemleri ve yapılandırmalara ilişkin ayrıntılar için bkz. [desteklenen konfigürasyonlar](../configs/supported-configurations.md).  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Intel Aktif Yönetim Teknolojisi (AMT) desteği  

Geçerli dalı Configuration Manager, AMT tabanlı bilgisayarların yerel desteğini Configuration Manager konsolundan kaldırır. [Microsoft Configuration Manager Için ıNTEL SCS eklentisi '](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)nı kullandığınızda AMT tabanlı bilgisayarlar tam olarak yönetilmeye devam eder. Eklenti, AMT 'yi yönetmek için en son yeteneklere erişmenizi sağlar. bu değişiklikler, Configuration Manager bu değişiklikleri birleştirebilene kadar sunulan sınırlamaları ortadan kaldırır.  

Configuration Manager için tümleşik AMT 'nin kaldırılması bant dışı yönetimi içerir. Bant dışı yönetim noktası site sistemi rolü artık kullanılamıyor.  

> [!Note]
> Bu değişiklik, System Center 2012 Configuration Manager bant dışı yönetimini etkilemez.

## <a name="changes-in-functionality"></a>İşlevselliğindeki değişiklikler

Aşağıdaki bölümlerde, System Center 2012 R2 Configuration Manager arasındaki özellik alanlarındaki önemli değişikliklerden bazıları ve geçerli dalın Configuration Manager sürüm 1511 sürümü özetlenmektedir. İşlevlerde yapılan son değişiklikler hakkında daha fazla bilgi için bkz. [artımlı sürümlerdeki yenilikler](whats-new-incremental-versions.md).

### <a name="client-deployment"></a>İstemci dağıtımı  

Configuration Manager, sitenin geri kalanını yeni yazılımlarla yükseltmeden önce Configuration Manager istemcisinin yeni sürümlerini test etmeye yönelik yeni bir özellik sunar. Yeni bir istemciyi pilot yapmak için bir ön üretim koleksiyonu ayarlayabilirsiniz. Ön üretim aşamasındaki yeni istemci yazılımını memnun olduktan sonra, istemciyi sitenin geri kalanını yeni sürüme otomatik olarak yükseltecek şekilde yükseltebilirsiniz.  

İstemcileri test etme hakkında daha fazla bilgi için bkz. [bir ön üretim koleksiyonundaki istemci yükseltmelerini test etme](../../clients/manage/upgrade/test-client-upgrades.md).  

### <a name="os-deployment"></a>İşletim sistemi dağıtımı  

İşletim sistemi dağıtımı için aşağıdaki değişiklikleri unutmayın:

- Görev sırası oluşturma sihirbazında yeni bir görev dizisi türü mevcuttur: **bir işletim sistemini yükseltme paketinden yükseltme**. Windows 7 veya Windows 8.1 bilgisayarları Windows 10 ' a yükseltmek için gereken adımları oluşturur. Daha fazla bilgi için bkz. [Windows 'u en son sürüme yükseltme](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Windows PE Eş Önbelleği artık işletim sistemlerini dağıttığınızda kullanılabilir. İşletim sistemini dağıtmak için bir görev dizisi çalıştıran bilgisayarlar, bir dağıtım noktasından içerik indirmek yerine bir eş önbellek kaynağından içerik almak üzere Windows PE Eş Önbelleği kullanabilir. Bu davranış, yerel dağıtım noktası olmayan şube senaryolarında WAN trafiğini en aza indirmeye yardımcı olur. Daha fazla bilgi için bkz. [WAN trafiğini azaltmak Için WINDOWS PE eş önbelleğini hazırlama](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

- Artık ortamınızdaki hizmet olarak Windows 'un durumunu görüntüleyebilirsiniz. Ayrıca, dağıtım halkalarını biçimlendirmek üzere bakım planları oluşturabilir ve yeni derlemeler yayınlandığında Windows 10 ' un geçerli dal bilgisayarlarının güncel tutulduğundan emin olabilirsiniz. Ayrıca, Windows 10 istemcileri kendi derlemesi için destek sonuna yaklaştıklarında uyarıları görüntüleyebilirsiniz. Daha fazla bilgi için bkz. [Windows 'u hizmet olarak yönetme](../../../osd/deploy-use/manage-windows-as-a-service.md).  

### <a name="application-management"></a>Uygulama yönetimi  

Uygulama yönetimi için aşağıdaki değişiklikleri unutmayın:

- Configuration Manager, Windows 10 ve üzeri çalıştıran cihazlar için Evrensel Windows Platformu (UWP) uygulamaları dağıtmanıza olanak tanır. Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../../../apps/get-started/creating-windows-applications.md).  

- Yazılım Merkezi 'Nde yeni ve modern bir görünüm bulunur. Daha önce yalnızca uygulama kataloğunda görüntülenen kullanıcı tarafından kullanılabilir uygulamalar artık uygulamalar sekmesi altındaki yazılım merkezi 'nde görünür. Bu davranış, bu dağıtımların daha keşfedilebilir olmasını sağlar ve kullanıcıların ayrı uygulama kataloğuna başvurmasını gereksiz hale getirir. Ayrıca, Silverlight özellikli bir tarayıcı artık gerekli değildir. Daha fazla bilgi için bkz. [uygulama yönetimini planlayın ve yapılandırın](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

- MDM uygulamasındaki yeni Windows Installer, Windows Installer tabanlı uygulamalar oluşturmanıza ve bunları Windows 10 çalıştıran kayıtlı cihazlara dağıtmanıza imkan sağlar. Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../../../apps/get-started/creating-windows-applications.md).  

- Configuration Manager 2012 ' de, Windows Mağazası 'ndaki bir uygulamanın bağlantısını belirtmek için bağlantıyı doğrudan belirtebilir veya uygulamanın yüklü olduğu uzak bir bilgisayara gidebilirsiniz. Geçerli dalı Configuration Manager, doğrudan bağlantıyı girmeye devam edebilirsiniz, ancak artık başvuru bilgisayarına göz atmak yerine, uygulama için mağazaya doğrudan Configuration Manager konsolundan göz atabilirsiniz.  

### <a name="software-updates"></a>Yazılım güncelleştirmeleri  

Yazılım güncelleştirmelerine yönelik aşağıdaki değişikliklerden haberdar olun:

- Configuration Manager, artık bilgisayarlar için yazılım güncelleştirme yönetimi yöntemleri arasındaki farkı algılayabilir. Özellikle, Windows Update for Business 'a (WUfB) bağlanan bir Windows 10 bilgisayarı ve WSUS 'a bağlı bir bilgisayar arasında ayrım yapabilir. **UseWUServer** özniteliği yenidir ve bilgisayarın WUfB ile yönetilip yönetilmediğini belirtir. Bu ayarı, bu bilgisayarları yazılım güncelleştirme yönetiminden kaldırmak için bir koleksiyonda kullanabilirsiniz. Daha fazla bilgi için bkz. [Windows 10’da Windows Update for Business ile Tümleştirme](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

- Şimdi de Configuration Manager konsolundan WSUS temizleme görevini zamanlayabilir ve çalıştırabilirsiniz. **Yazılım güncelleştirme noktası bileşen** özellikleri ' nde, WSUS temizleme görevini çalıştırmayı seçtiğinizde, bir sonraki yazılım güncelleştirmeleri eşitlemede çalışır. Tarihi geçen yazılım güncelleştirmeleri, WSUS sunucusunda reddedildi durumuna ayarlanır ve bilgisayarlardaki Windows Update Aracısı bu yazılım güncelleştirmelerini artık taramamıştır. Daha fazla bilgi için bkz. [WSUS temizleme görevini zamanlama ve çalıştırma](../../../sum/deploy-use/software-updates-maintenance.md).  

### <a name="compliance-settings"></a>Uyumluluk ayarları  

Uyumluluk ayarlarına aşağıdaki değişiklikleri unutmayın:

- Configuration Manager, yapılandırma öğeleri oluşturmak için iş akışını geliştirir. Bundan böyle bir yapılandırma öğesi oluşturduğunuzda ve desteklenen platformları seçtiğinizde yalnızca bu platformla ilgili ayarlar kullanılabilir. Bkz. [Uyumluluk ayarlarına başlama](../../../compliance/get-started/get-started-with-compliance-settings.md).  

- **Yapılandırma öğesi oluşturma** Sihirbazı artık oluşturmak istediğiniz yapılandırma öğesi türünü seçmenizi kolaylaştırır. Ayrıca, yeni ve güncelleştirilmiş yapılandırma öğeleri aşağıdakiler için kullanılabilir:  

    - Configuration Manager istemcisiyle yönetilen Windows 10 cihazları  

    - Configuration Manager istemcisiyle yönetilen cihazlar Mac OS X  

    - Configuration Manager istemcisiyle yönetilen Windows Masaüstü ve sunucu bilgisayarları  

    - Configuration Manager istemcisi olmadan yönetilen Windows 8.1 ve Windows 10 cihazları  

    Daha fazla bilgi için bkz. [yapılandırma öğeleri oluşturma](../../../compliance/deploy-use/create-configuration-items.md).  

- Configuration Manager istemcisi olmadan yönetilen Mac OS X bilgisayarlardaki ayarları yönetme desteği.

### <a name="on-premises-mobile-device-management"></a>Şirket içi mobil cihaz yönetimi  

Artık, şirket içi Configuration Manager altyapısını kullanarak mobil cihazları yönetebilirsiniz. Tüm cihaz ve yönetim verileri şirket içinde işlenir ve Microsoft Intune veya diğer bulut hizmetlerinin bir parçası değildir. Bu cihaz yönetimi türü istemci yazılımı gerektirmez. Configuration Manager cihaz işletim sisteminde yerleşik işlevlere sahip cihazları yönetir.  

Daha fazla bilgi için bkz. [Şirket içi altyapıyla mobil cihazları yönetme](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

## <a name="next-steps"></a>Sonraki adımlar

[Artımlı sürümlerdeki yenilikler](whats-new-incremental-versions.md)
