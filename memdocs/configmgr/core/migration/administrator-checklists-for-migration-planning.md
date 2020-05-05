---
title: Geçiş denetim listeleri
titleSuffix: Configuration Manager
description: Geçerli dalı Configuration Manager için bir geçiş stratejisi planlamanız yardımcı olması için yönetici denetim listelerini kullanın.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e406a2b7674815bb3313200ba850baa249f17ebc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718948"
---
# <a name="administrator-checklists-for-migration-planning-in-configuration-manager"></a>Configuration Manager 'de geçiş planlaması için yönetici denetim listeleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Geçerli dalı Configuration Manager geçiş stratejinizi planlamada yardımcı olması için aşağıdaki yönetici denetim listelerini kullanın.

##  <a name="administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a>Geçiş planlaması için yönetici denetim listesi  
 Geçiş öncesi planlama adımları için aşağıdaki denetim listesini kullanın.  

-   **Geçerli ortamı değerlendirin:**  

     Kaynak hiyerarşisi tarafından karşılanan var olan iş gereksinimlerini belirleyin ve hedef hiyerarşisinde bu gereksinimleri karşılamaya devam etmek için planlar geliştirin.  

-   **Kullandığınız Configuration Manager sürümünde kullanılabilen işlevselliği ve değişiklikleri gözden geçirin ve hedef hiyerarşinizi tasarlamanıza yardımcı olması için bu bilgileri kullanın:**  

    Daha fazla bilgi için bkz. [Configuration Manager Temelleri](../../core/understand/fundamentals.md) ve [Yenilikler.](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)  


-   **Rol tabanlı yönetim için kullanılacak yönetim güvenlik modelini belirleme:**  

    Daha fazla bilgi için bkz. [Configuration Manager için rol tabanlı yönetimin temelleri](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Ağınızı ve Active Directory topolojinizi değerlendirin:** Mevcut etki alanı yapınızı ve ağ topolojinizi gözden geçirin ve bunun hiyerarşi tasarımı ve geçiş görevlerinizi nasıl etkilediğini düşünün.  

-   **Hedef hiyerarşi tasarımınıza son şeklini verin:**  

    Bir merkezi yönetim sitesinin, birincil ve ikincil sitelerin ve içerik dağıtım seçeneklerinin yerleştirmesine karar verin.  

-   **Hiyerarşinizi, hedef hiyerarşideki siteler ve site sunucuları için kullanacağınız bilgisayarlara eşleyin:**  

    Sitelerin ve site sistem sunucularının hedef hiyerarşide kullanacağı bilgisayarları ve ardından var olan ve gelecekteki işletimsel gereksinimleri karşılamak için yeterli kapasiteye sahip olduklarından emin olun.  

-   **Nesne geçiş stratejinizi planlayın:**  

    Site sınırları, koleksiyonlar, tanıtımlar ve dağıtımlar dahil olmak üzere farklı nesneleri geçirmek için kullanılabilen geçiş işlerini kullanmayı planlayın. Daha fazla bilgi için, bkz. [geçiş Işi planlamadaki](../../core/migration/planning-a-migration-job-strategy.md) [geçiş işlerinin türleri](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration)  

    Configuration Manager yalnızca seçtiğiniz nesneleri geçirir. Geçirilmeyen ve hedef hiyerarşisinde gerekli olan tüm nesnelerin hedef hiyerarşisinde yeniden oluşturulması gerekir.  

    Geçirilebilen nesneler, geçiş işlerini yapılandırdığınızda görüntülenir.  

-   **İstemci geçiş stratejinizi planlayın:**  

    İstemcileri hedef hiyerarşisine geçirdiğinizde ağ bant genişliğini ve sunucu işleme gereksinimlerini sınırlandıran bir kontrollü yaklaşım kullanarak istemcileri geçirmeyi planlayın. İstemci geçiş stratejisi planlama hakkında daha fazla bilgi için bkz. [istemci geçiş stratejisi planlama](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Envanteri ve uyumluluk verilerini planlayın:**  

    Configuration Manager, yazılım güncelleştirmeleri veya istemcileri için donanım envanteri, yazılım envanteri veya istenen yapılandırma yönetimi uyumluluk verilerini geçirmeyi desteklemez.  

    Bunun yerine, hedef hiyerarşisindeki yeni sitesine geçirildikten ve bu yapılandırmalar için ilke aldıktan sonra istemci, bu bilgileri kendi atandığı siteye gönderir. Bu eylem, hedef site veritabanını mevcut envanter ve uyumluluk verileri ile doldurur.  

-   **Kaynak hiyerarşiden geçişin tamamlanmasını planlayın:**  

    Nesnelerin ve istemcilerin ne zaman geçirileceğine karar verin. Geçiş işlemi tamamlandığında kaynak hiyerarşisindeki site sunucularının yetkisini almayı planlayabilirsiniz.  

##  <a name="administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a>Hiyerarşi geçişi için yönetici denetim listesi  
Geçiş işlemine başlamadan önce bir hedef hiyerarşisi planlamanıza yardımcı olması için aşağıdaki denetim listesini kullanın.  

-   **Hedef hiyerarşide kullanılacak bilgisayarları belirleyin:**  

    Configuration Manager, Configuration Manager 2007 altyapısından yerinde yükseltmeyi desteklemez. Bunun yerine, Configuration Manager 2007 ' den geçerli dalı Configuration Manager verileri taşımak için geçiş kullanmanız gerekir. Bu, yan yana dağıtım kullanmanızı ve Configuration Manager yeni bilgisayarlara yüklemenizi gerektirir.  

    Benzer şekilde, başka bir Configuration Manager hiyerarşisinden geçiş yaptığınızda, kaynak hiyerarşinize bir yan yana dağıtım olan yeni bir hedef hiyerarşisi yüklemelisiniz.  

-   **Hedef hiyerarşinizi oluşturun:**  

    Geçişe hazırlanmak için, birincil site içeren bir Configuration Manager hedef hiyerarşisi yükleyip yapılandırın. Örneğin:  

    -   Bir merkezi yönetim sitesi yükleyip en az bir alt birincil site yükler.  

    -   Bir merkezi yönetim sitesi kullanmayı planlamıyorsanız, tek başına bir birincil yükler.  

-   **Yazılım güncelleştirmeleriyle ilgili bilgileri geçirmek istiyorsanız hedef hiyerarşide bir yazılım güncelleştirme noktası yapılandırın ve yazılım güncelleştirmelerini eşitleyin:**  

    Kaynak hiyerarşisindeki yazılım güncelleştirmelerini geçirmeden önce hedef hiyerarşisindeki yazılım güncelleştirmelerini yapılandırmanız ve eşitlemeniz gerekir.  


-   **Hedef hiyerarşiye ek sistem rolleri yükleyin ve bunları yapılandırın:**  

    İhtiyacınız olan ek site sistem rollerini ve site sistemlerini yapılandırın.  

-   **Hedef hiyerarşisindeki işletimsel işlevselliği denetleyin:**  

    Aşağıdakileri denetleyin:  

    -   Hedef hiyerarşisi birden fazla site içeriyorsa siteler arasında veritabanı çoğaltmanın çalıştığını doğrulayın. Veritabanı çoğaltma, tek başına birincil siteler için geçerli değildir.  

    -   Yüklü tüm site sistem rollerinin çalışır durumda olup olmadığını denetleyin.  

    -   Hedef hiyerarşiye yüklediğiniz Configuration Manager istemcilerinin atanan sitesiyle başarıyla iletişim kurabildiğini denetleyin.  


##  <a name="administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a>Geçiş için yönetici denetim listesi  
Verileri kaynak hiyerarşisinden hedef hiyerarşisine geçirmek için aşağıdaki denetim listesini kullanın.  

-   **Hedef hiyerarşide geçişi etkinleştirin:**  

    Kaynak hiyerarşinin en üst düzey sitesini belirterek bir kaynak hiyerarşisini yapılandırın. Kaynak siteyi belirtme hakkında daha fazla bilgi için bkz. [kaynak hiyerarşi stratejisi planlama](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Kaynak hiyerarşisi Configuration Manager 2007 SP2 çalıştırıyorsa, kaynak hiyerarşisinde ek siteler seçin ve yapılandırın:**  

    Verileri toplamak istediğiniz Configuration Manager 2007 SP2 kaynak hiyerarşisindeki her bir ek site için veri toplama için kimlik bilgilerini yapılandırmanız gerekir. Her bir kaynak siteyi yapılandırdığınızda, veri toplama işlemi hemen başlar ve o site için veri toplamayı durdurana kadar geçiş dönemi boyunca devam eder. Veri toplama, önceki bir veri toplama işleminden sonra güncellenen veya eklenen kaynak hiyerarşisinden nesneleri geçirebilmenizi sağlar.

    > [!NOTE]  
    >  Kaynak hiyerarşisi System Center 2012 Configuration Manager veya sonraki bir sürümünü çalıştırdığında ek kaynak siteleri yapılandırmanız gerekmez.  

-   **Dağıtım noktası paylaşımını yapılandırın:**  

    Hedef hiyerarşisindeki istemcilerde kullanılabilen geçirdiğiniz nesneler için içerik oluşturmak üzere iki hiyerarşi arasında dağıtım noktalarını paylaşabilirsiniz. Bu, aynı içeriğin her iki hiyerarşideki istemciler için kullanılabilir olmaya devam etmesini ve veri toplamayı durdurup geçişi bitirene kadar bu içeriği koruyabilmenizi sağlar.  

    Paylaşılan dağıtım noktaları hakkında bilgi için, bkz. [bir içerik dağıtımı geçiş stratejisi planlarken](../../core/migration/planning-a-content-deployment-migration-strategy.md) [kaynak ve hedef hiyerarşileri arasında dağıtım noktalarını paylaşma](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) .  

-   **Kaynak hiyerarşisindeki istemcilerle ilişkilendirilen nesneleri geçirmek için geçiş işlerini oluşturun ve çalıştırın:**  

    Hiyerarşiler arasında nesneleri geçirmek için geçiş işleri oluşturun. Her bir geçiş işi için gerekli olan yapılandırmalar, işin hangi veriyi geçirdiğine bağlı olarak değişebilir.  

    Örneğin, içeriği geçirdiğinizde bu içeriğin yönetimine sahip olmak için, kullandığınız geçiş işine bakmaksızın hedef hiyerarşisinde bir site atamanız gerekir. Atanan site, içerik için orijinal kaynak dosya konumuna erişir ve bu içeriği hedef hiyerarşisindeki dağıtım noktalarına dağıtmada sorumludur.  

    Daha fazla bilgi için bkz. [Configuration Manager için geçiş Işlerini oluşturma ve düzenleme](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) [işlemleri için Configuration Manager güncel dala geçme](../../core/migration/operations-for-migration.md).  

-   **İstemcileri hedef hiyerarşisine geçirin:**  

    İşlemcileri geçirme işlemi geçiş senaryonuza bağlıdır:  

    -   Hedef hiyerarşiyle aynı olmayan bir istemci sürümüne sahip istemcileri geçirdiğinizde, istemci yazılımını yükseltmeniz gerekir. Yükseltme, geçerli Configuration Manager istemcisinin kaldırılmasını ve ardından hedef siteyle eşleşen yeni istemci sürümünün yüklenmesini gerektirir.  

    -   Hedef hiyerarşisinin sürümüyle eşleşen bir istemci sürümü olan istemcileri geçirdiğinizde istemci yükseltilmez veya yeniden yüklenmez. Bunun yerine istemci, hedef hiyerarşisindeki bir birincil siteye tekrar atanır.  

    Bir istemciyi hedef hiyerarşisine geçirdiğinizde istemci, daha önce bu hedef hiyerarşisine geçirdiğiniz verileriyle ilişkilendirilir.  

    Daha fazla bilgi için bkz. [istemci geçiş stratejisi planlama](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Paylaşılan dağıtım noktalarını güncelleştirin veya yeniden atayın:**  

    Artık kaynak hiyerarşinizdeki istemcileri desteklemeniz gerekmiyorsa, paylaşılan dağıtım noktalarını bir Configuration Manager 2007 kaynak sitesinden yükseltebilir veya paylaşılan dağıtım noktalarını bir System Center 2012 Configuration Manager veya Configuration Manager güncel dal kaynak sitesinden yeniden atayabilirsiniz. Dağıtım noktasını yükselttiğinizde veya yeniden atadığınızda site sistem rolü hedef hiyerarşisindeki bir birincil siteye aktarılır ve dağıtım noktası kaynak hiyerarşisindeki kaynak siteden kaldırılır. Paylaşılan bir dağıtım noktasını yükselttiğinizde veya yeniden atadığınızda içerik, dağıtım noktası bilgisayarında kalır ve içeriği hedef hiyerarşisindeki yeni dağıtım noktalarına yeniden dağıtmanız gerekmez.  

    Ayrıca, bir Configuration Manager 2007 ikincil site sunucusunda birlikte bulunan bir dağıtım noktasını da yükseltebilirsiniz. Bu işlem ikincil siteyi kaldırır ve hedef hiyerarşisinde yalnızca bir dağıtım noktası bulunmasına neden olur.  

    Paylaşılan dağıtım noktaları hakkında bilgi için, bkz. [bir içerik dağıtımı geçiş stratejisi planlarken](../../core/migration/planning-a-content-deployment-migration-strategy.md) [kaynak ve hedef hiyerarşileri arasında dağıtım noktalarını paylaşma](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) .  

-   **Geçişi tamamlama:**  

    Kaynak hiyerarşisindeki tüm sitelerden verileri ve istemcileri geçirdikten ve geçerli dağıtım noktalarını yükseltmişseniz, geçiş işlemi gerçekleştirebilirsiniz. Geçişi tamamlaması için kaynak hiyerarşisindeki her kaynak site için veri toplamayı durdurabilirsiniz. Ardından ihtiyacınız olmayan geçiş bilgilerini kaldırabilir ve kaynak hiyerarşi altyapınızın yetkisini alabilirsiniz. Daha fazla bilgi için bkz. [taşımayı tamamlamayı planlama](../../core/migration/planning-to-complete-migration.md).  
