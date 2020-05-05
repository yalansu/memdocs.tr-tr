---
title: Nesneleri geçirme
titleSuffix: Configuration Manager
description: Configuration Manager geçerli bir dal ortamındaki hiyerarşiler arasında nesnelerin geçirilmesini nasıl planlayacağınızı öğrenin.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9777fb12a2d63a990587386ac33cb2749bf19a4e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719655"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Configuration Manager nesnelerinin geçerli dala Configuration Manager geçişini planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli dalı Configuration Manager, bir kaynak sitede bulunan farklı özelliklerle ilişkilendirilmiş farklı nesnelerin çoğunu geçirebilirsiniz.

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a>Yazılım güncelleştirmelerini geçirmeyi planlayın  
 Yazılım güncelleştirme paketleri ve yazılım güncelleştirme dağıtımları gibi yazılım güncelleştirme nesnelerini geçirebilirsiniz.  

 Yazılım güncelleştirme nesnelerini başarılı bir şekilde geçirmek için önce hedef hiyerarşinizi kaynak hiyerarşi ortamınızla eşleşen yapılandırmalara ayarlamanız gerekir. Bunu yapmak şu işlemleri gerektirir:  

-   Hedef hiyerarşisinde etkin bir yazılım güncelleştirme noktası dağıtma  

-   Ürün ve dillerin kataloğunu, kaynak hiyerarşinizin yapılandırmasıyla eşleşecek şekilde ayarlayın  

-   Hedef hiyerarşideki yazılım güncelleştirme noktasını Windows Server Update Services (WSUS) ile eşitleme  

Yazılım güncelleştirmelerini geçirirken şunlara dikkat edin:  

-   Hedef hiyerarşinizdeki bilgileri kaynak hiyerarşinizin yapılandırmasıyla eşleşecek şekilde eşitlemediğiniz zaman, yazılım güncelleştirme nesnelerinin geçirilmesi başarısız olabilir.  

    > [!WARNING]  
    >  Configuration Manager, verileri kaynak ve hedef hiyerarşi arasında eşitlemek için WSUSutil aracının kullanımını desteklemez.  

-   System Center Updates Publisher kullanılarak yayımlanan özel güncelleştirmeleri geçiremezsiniz. Özel güncelleştirmeler bunun yerine hedef hiyerarşiye yeniden yayımlanmalıdır.  

Configuration Manager 2007 kaynak hiyerarşisinden geçiş yaptığınızda, geçiş işlemi bazı yazılım güncelleştirme nesnelerini hedef hiyerarşi tarafından kullanılan biçime değiştirir. Configuration Manager 2007 ' den yazılım güncelleştirme nesnelerinin geçişini planlamaya yardımcı olması için aşağıdaki tabloyu kullanın.  

|Configuration Manager 2007 nesnesi|Geçişten sonraki nesne adı|  
|-----------------------------------|---------------------------------|  
|Yazılım güncelleştirmesi listeleri|Yazılım güncelleştirme listeleri yazılım güncelleştirme gruplarına dönüştürülür.|  
|Yazılım güncelleştirme dağıtımları|Yazılım güncelleştirme dağıtımları, dağıtımlara ve güncelleştirme gruplarına dönüştürülür.<br /><br /> Configuration Manager 2007 ' dan bir yazılım güncelleştirme dağıtımını geçirdikten sonra, onu dağıtabilmeniz için önce hedef hiyerarşisinde etkinleştirmeniz gerekir.|  
|Yazılım güncelleştirme paketleri|Yazılım güncelleştirme paketleri yine yazılım güncelleştirme paketleri olarak kalır.|  
|Yazılım güncelleştirme şablonları|Yazılım güncelleştirme şablonları yine yazılım güncelleştirme şablonları olarak kalır.<br /><br /> Configuration Manager 2007 dağıtım şablonlarındaki **süre** değeri geçirilmez.|  

Bir System Center 2012 Configuration Manager Configuration Manager veya geçerli dal kaynağı hiyerarşisinden nesne geçirdiğinizde, yazılım güncelleştirme nesneleri değiştirilmez.  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a>İçerik geçirmeyi planlayın  
 Desteklenen bir kaynak hiyerarşideki içeriği hedef hiyerarşinize geçirebilirsiniz. Configuration Manager 2007 kaynak hiyerarşisi için bu içerik, Microsoft Application Virtualization (App-V) gibi yazılım dağıtım paketleri ve programları ve sanal uygulamaları içerir. System Center 2012 Configuration Manager ve geçerli dal kaynak hiyerarşileri Configuration Manager, bu içerik uygulamalar ve App-V sanal uygulamalarını içerir. Hiyerarşileri arasında içerik geçirdiğinizde, sıkıştırılan kaynak dosyaları hedef hiyerarşiye geçirilir.  

### <a name="packages-and-programs"></a>Paketler ve programlar  
 Paket ve programları taşırken bunlar taşıma işlemi ile değiştirilmezler. Ancak, geçirmeden önce her bir paketi, kaynak dosya konumu için bir evrensel adlandırma kuralı (UNC) yolu kullanacak şekilde ayarlamanız gerekir. Paket ve programları geçirme yapılandırmasının parçası olarak, bu içeriği yönetmek için hedef hiyerarşide bir site atamanız gerekir. İçerik atanan siteden geçirilmez, ancak geçişten sonra atanan site, UNC eşlemesini kullanarak özgün kaynak dosyası konumuna erişir.  

 Bir paketi ve programı hedef hiyerarşiye geçirdikten sonra ve kaynak hiyerarşiden geçiş etkin olmaya devam ederken, paylaşılan bir dağıtım noktasını kullanarak içeriği o hiyerarşideki istemciler için kullanılabilir hale getirebilirsiniz. Paylaşılan dağıtım noktasını kullanabilmek için içeriğin kaynak sitedeki dağıtım noktasında erişilebilir kalması gerekir. Paylaşılan dağıtım noktaları hakkında daha fazla bilgi için bkz. [içerik dağıtımı geçiş stratejisi](../../core/migration/planning-a-content-deployment-migration-strategy.md)içindeki [kaynak ve hedef hiyerarşileri arasında dağıtım noktalarını paylaşma](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) .  

 Geçirilen içerikler, kaynak hiyerarşisinde veya hedef hiyerarşisinde içerik sürümü değişirse, istemciler artık hedef hiyerarşideki paylaşılan dağıtım noktasından içeriğe erişemez. Bu senaryoda, kaynak hiyerarşisi ve hedef hiyerarşisi arasında paketin tutarlı bir sürümünü geri yüklemek için içeriği yeniden geçirmeniz gerekir. Bu bilgiler veri toplama çevrimi sırasında eşitlenir.  

> [!TIP]  
>  Geçirdiğiniz her bir paket için, hedef hiyerarşisinde paketi güncelleştirin. Bu eylem, paketin hedef hiyerarşisindeki dağıtım noktalarına dağıtılmasıyla ilgili sorunları önleyebilir. Ancak, hedef hiyerarşisindeki dağıtım noktasındaki bir paketi güncelleştirdiğinizde, söz konusu hiyerarşideki istemciler artık o paketi paylaşılan bir dağıtım noktasından alamaz. Hedef hiyerarşisindeki bir paketi güncelleştirmek için, Configuration Manager konsolunda yazılım kitaplığı 'na gidin, pakete sağ tıklayın ve ardından **dağıtım noktalarını güncelleştir**' i seçin. Bu eylemi, geçiş yaptığınız her paket için yapın.  

> [!TIP]  
> Paketleri ve programları Configuration Manager uygulamalarına dönüştürmek için Paket Dönüştürme Yöneticisi 'ni kullanın. Daha fazla bilgi için bkz. [Paket Dönüştürme Yöneticisi](../../apps/pcm/package-conversion-manager.md).  

### <a name="virtual-applications"></a>Sanal uygulamalar  
Desteklenen bir Configuration Manager 2007 sitesinden App-V paketleri geçirdiğinizde, geçiş işlemi bunları hedef hiyerarşideki uygulamalara dönüştürür. Ayrıca, App-V paketine yönelik mevcut tanıtımlar temelinde, hedef hiyerarşisinde aşağıdaki dağıtım türleri oluşturulur:  

-   Bir tanıtım yoksa varsayılan dağıtım türü ayarlarını kullanan tek bir dağıtım türü oluşturulur.  

-   Bir reklam varsa, Configuration Manager 2007 tanıtımla aynı ayarları kullanan bir dağıtım türü oluşturulur.  

-   Birden çok reklam varsa, bu tanıtıma yönelik ayarlar kullanılarak her Configuration Manager 2007 tanıtımı için bir dağıtım türü oluşturulur.  

> [!IMPORTANT]  
>  Daha önce geçirilmiş bir Configuration Manager 2007 App-V paketini geçirirseniz, sanal uygulama paketleri geçiş üzerine yazma davranışını desteklemediği için geçiş başarısız olur. Bu senaryoda, geçirilen sanal uygulama paketini hedef hiyerarşiden silmeniz ve sonra sanal uygulamayı geçirmek için yeni bir geçiş işi oluşturmanız gerekir.  

> [!NOTE]  
>  App-V paketini geçirdikten sonra, App-V dağıtım türlerinin kaynak yolunu değiştirmek için Içerik güncelleştirme sihirbazını kullanabilirsiniz. Bir dağıtım türü için içeriği güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager uygulamalar Için yönetim görevlerinde](../../apps/deploy-use/management-tasks-applications.md)dağıtım türlerini yönetme.  

System Center 2012 Configuration Manager Configuration Manager veya geçerli dal kaynak hiyerarşisinden geçiş yaparken App-v dağıtım türleri ve uygulamalarının yanı sıra App-V sanal ortamına yönelik nesneleri geçirebilirsiniz. App-V ortamları hakkında daha fazla bilgi için bkz. [App-v sanal uygulamalarını dağıtma](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Reklamlar  
Derleme temelli geçiş kullanarak, desteklenen bir Configuration Manager 2007 kaynak sitesinden tanıtımları hedef hiyerarşiye geçirebilirsiniz. İstemciyi yükseltiyorsanız, istemcinin geçirilmiş olan tanıtımları yeniden çalıştırmasına engel olmak için önceden çalıştırılmış tanıtımlar geçmişini koruyabilirsiniz.  

> [!NOTE]  
>  Sanal paketlere ait tanıtımları geçiremezsiniz. Tanıtımların geçirilmesi için bu bir özel durumdur.  

### <a name="applications"></a>Uygulamalar  
 Desteklenen bir System Center 2012 Configuration Manager veya geçerli dal kaynak hiyerarşisinden Configuration Manager bir hedef hiyerarşiye uygulama geçirebilirsiniz. Kaynak hiyerarşideki bir istemciyi hedef hiyerarşiye yeniden atadığınızda, o istemci geçirilmiş bir uygulamayı yeniden çalıştırmaya engel olmak için önceden yüklenmiş uygulamalar geçmişini korur.  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a>Koleksiyonları geçirmeyi planlayın  
 Koleksiyonlar için ölçütleri desteklenen bir System Center 2012 Configuration Manager veya geçerli dal kaynağı hiyerarşisinden Configuration Manager geçirebilirsiniz. Bunun için, nesne tabanlı bir geçiş işi kullanırsınız. Bir koleksiyonu geçirdiğinizde, koleksiyon üyeleriyle ilgili bilgileri veya koleksiyon üyeleriyle ilgili nesneler hakkındaki bilgileri değil o koleksiyonun kurallarını geçirirsiniz.  

 Configuration Manager 2007 kaynak hiyerarşisinden geçiş yaparken koleksiyon nesnesinin geçirilmesi desteklenmez.  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a>İşletim sistemi dağıtımlarını geçirmeyi planlayın  
Desteklenen bir kaynak hiyerarşisindeki aşağıdaki işletim sistemi dağıtım nesnelerini geçirebilirsiniz:  

-   İşletim sistemi görüntüleri ve paketleri. Önyükleme görüntülerinin kaynak yolu, hedef sitedeki Windows Yönetim yükleme seti (Windows AIK) için varsayılan görüntü konumuna güncelleştirilir. İşletim sistemi görüntülerini ve paketlerini geçirme koşulları ve sınırlamaları aşağıdaki gibidir:  

    -   Görüntü dosyalarını başarıyla geçirmek için, hedef hiyerarşinin üst düzey sitesi için SMS sağlayıcısı sunucusunun bilgisayar hesabı, kaynak sitenin Windows AIK konumunun görüntü kaynak dosyaları için **okuma** ve **yazma** iznine sahip olmalıdır.  

    -   Bir işletim sistemi yükleme paketini geçirdiğinizde, kaynak sitedeki paket yapılandırmasının WIM dosyasının kendisi için değil, WıM dosyasını içeren klasöre işaret ettiğini doğrulayın. Yükleme paketi WIM dosyasını gösteriyorsa yükleme paketinin geçirilmesi başarısız olur.  

    -   Bir önyükleme görüntüsü paketini Configuration Manager 2007 kaynak sitesinden geçirdiğinizde, paketin paket KIMLIĞI hedef sitede korunmaz. Bunun sonucu olarak hedef hiyerarşideki istemciler paylaşılan dağıtım noktalarında bulunan önyükleme görüntüsü paketlerini kullanamaz.  

-   Görev dizileri. İstemci yükleme paketine başvuru içeren bir görev dizisini geçirdiğinizde, bu başvuruya hedef hiyerarşinin istemci yükleme paketine yönelik bir başvuru konur.  

    > [!NOTE]  
    >  Bir görev dizisini geçirdiğinizde, Configuration Manager hedef hiyerarşide gerekli olmayan nesneleri geçirebilir. Bu nesneler önyükleme görüntülerini ve Configuration Manager 2007 istemci yükleme paketlerini içerir.  

-   Sürücüler ve sürücü paketleri. Sürücü paketlerini geçirdiğinizde, hedef hiyerarşideki SMS sağlayıcısının bilgisayar hesabı, paket kaynağında tam denetime sahip olmalıdır.

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a>İstenen yapılandırma yönetimini geçirmeyi planlayın  
Yapılandırma öğelerini ve yapılandırma temellerini geçirebilirsiniz.  

> [!NOTE]  
>  Configuration Manager 2007 kaynak hiyerarşilerinden yorumlanan yapılandırma öğeleri geçiş için desteklenmiyor. Bu yapılandırma öğelerini hedef hiyerarşiye geçiremez veya içeri aktaramazsınız. Yorumlanmamış yapılandırma öğeleri hakkında daha fazla bilgi için Configuration Manager 2007 belge kitaplığındaki [Istenen yapılandırma yönetimi konusundaki yapılandırma öğeleri hakkında](https://go.microsoft.com/fwlink/?LinkId=103846) bölümüne bakın.  

Configuration Manager 2007 yapılandırma paketini içeri aktarabilirsiniz. İçeri aktarma işlemi, yapılandırma paketlerini otomatik olarak Configuration Manager geçerli Dalla uyumlu olacak şekilde dönüştürür.  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a>Sınırları geçirmeyi planlayın  
 Hiyerarşiler arasında sınırları geçirebilirsiniz. Sınırları Configuration Manager 2007 ' dan geçirdiğinizde, kaynak sitedeki her bir sınır aynı anda geçirilir ve hedef hiyerarşisinde oluşturulan yeni bir sınır grubuna eklenir. Bir System Center 2012 Configuration Manager veya Configuration Manager geçerli dal hiyerarşisinden sınır geçirdiğinizde, seçtiğiniz her sınır hedef hiyerarşideki yeni bir sınır grubuna eklenir.  

 Otomatik olarak oluşturulan her bir sınır grubu içerik konumu için etkinleştirilir, ancak site ataması için etkinleştirilmez. Bu durum, kaynak ve hedef hiyerarşileri arasındaki site ataması için çakışan sınırları engeller. Configuration Manager 2007 kaynak sitesinden geçiş yaparken, bu, yüklenen yeni Configuration Manager 2007 istemcilerinin hedef hiyerarşiye yanlış atanmasını önlemeye yardımcı olur. Varsayılan olarak, Configuration Manager geçerli şube istemcileri Configuration Manager 2007 sitelerine otomatik olarak atanmaz.  

 Geçiş sırasında bir dağıtım noktasını hedef hiyerarşisiyle paylaşırsanız, bu dağıtımla ilişkilendirilen tüm sınırlar otomatik olarak hedef hiyerarşisine geçirilir. Hedef hiyerarşisinde geçiş, paylaşılan her dağıtım noktası için yeni bir salt okunurdur. Kaynak hiyerarşisindeki dağıtım noktası için sınırları değiştirirseniz hedef hiyerarşisindeki sınır grubu, sonraki veri toplama döngüsü sırasında bu değişikliklerle güncelleştirilir.  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a>Raporların geçişini planlayın  
Configuration Manager raporların geçişini desteklemez. Bunun yerine, raporları kaynak hiyerarşisinden dışa aktarmak ve daha sonra hedef hiyerarşisine içe aktarmak için SQL Server Raporlama Hizmetleri Rapor Oluşturucusu'nu kullanın.  

> [!NOTE]  
>  Configuration Manager 2007 ve geçerli dalı Configuration Manager arasındaki raporlara ait şema değişiklikleri olduğundan, Configuration Manager 2007 hiyerarşisinden içeri aktardığınız her raporu, beklendiği gibi çalıştığından emin olmak için test edin.  

Raporlama hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../servers/manage/introduction-to-reporting.md).  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a>Kuruluş ve arama klasörlerini geçirmeyi planlayın  
 Düzenlenmiş klasörleri ve arama klasörlerini desteklenen bir kaynak hiyerarşisinden hedef hiyerarşisine geçirebilirsiniz. Ayrıca, System Center 2012 Configuration Manager veya geçerli dal kaynağı hiyerarşisinden Configuration Manager, kayıtlı bir aramanın ölçütlerini hedef hiyerarşiye geçirebilirsiniz.  

 Varsayılan olarak geçiş işlemi, nesneleri ve koleksiyonları geçirdiğinizde bunlara ait arama klasörü ve yönetimsel klasör yapılarınızı tutar. Ancak, geçiş Işi oluşturma Sihirbazı 'nda, **Ayarlar** sayfasında, bu seçeneğe ait kutuyu işaretleyerek nesneler için kuruluş yapısını geçirmeyen bir geçiş işi ayarlayabilirsiniz. Koleksiyonların düzenlenmiş yapıları her zaman tutulur.  

 Bunun bir özel durumu ise sanal uygulamaları içeren bir arama klasörüdür. Bir App-V paketi geçirildiğinde, App-V paketi Configuration Manager içindeki bir uygulamaya dönüştürülür. Arama klasörünün geçişten sonra, yalnızca kalan paketler bulunur ve App-V paketi geçirildiğinde bu uygulamaya dönüştürme nedeniyle arama klasörü App-V paketini bulamaz.  

 Kayıtlı bir aramayı System Center 2012 Configuration Manager Configuration Manager veya geçerli dal kaynak hiyerarşisinden geçirdiğinizde, arama sonuçlarıyla ilgili bilgileri değil, arama ölçütlerini geçirolursunuz. Kayıtlı bir aramanın geçirilmesi Configuration Manager 2007 kaynak sitesinden geçerli değildir.  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a>Varlık Yönetim Bilgileri özelleştirmelerini geçirmeyi planlayın  
 Varlık Yönetim Bilgileri için özelleştirmeleri, desteklenen bir kaynak hiyerarşisinden hedef hiyerarşisine geçirebilirsiniz. Configuration Manager 2007 ve geçerli dalı Configuration Manager arasında Varlık Yönetim Bilgileri özelleştirmelerin yapısına önemli bir değişiklik yoktur.  

> [!NOTE]  
> Configuration Manager geçerli dal, Varlık Yönetim Bilgileri Service 2,0 (ASıS 2,0) kullanan bir Configuration Manager 2007 sitesinden Varlık Yönetim Bilgileri nesnelerinin geçirilmesini desteklemez.  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a>Yazılım kullanım ölçümü kuralları özelleştirmelerini geçirmeyi planlayın  
 Yazılım ölçümünün Configuration Manager 2007 ile geçerli dalı Configuration Manager arasında önemli bir değişiklik yoktur. Yazılım ölçme kurallarınızı, desteklenen bir kaynak hiyerarşisinden hedef hiyerarşisine geçirebilirsiniz.  

 Varsayılan olarak, bir hedef hiyerarşisine geçirdiğiniz yazılım kullanım ölçümü kuralları hedef hiyerarşisindeki belirli bir siteyle ilişkilendirilmez, bunun yerine hiyerarşideki tüm istemciler için geçerli olur. Bir yazılım kullanım ölçümü kuralını belirli bir sitedeki istemcilere uygulamak için geçirildikten sonra ölçme kuralını düzenlemeniz gerekir.  
