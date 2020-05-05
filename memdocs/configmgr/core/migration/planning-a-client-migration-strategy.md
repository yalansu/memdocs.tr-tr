---
title: İstemci geçişini planlayın
titleSuffix: Configuration Manager
description: İstemcileri bir kaynak hiyerarşisinden Configuration Manager geçerli dal hedefi hiyerarşisine geçiren görevler hakkında bilgi edinin.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720915"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>Configuration Manager bir istemci geçişi stratejisi planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İstemcileri kaynak hiyerarşisinden Configuration Manager geçerli dal hedef hiyerarşisine geçirmek için iki görev yapmanız gerekir. İstemciyle ilişkili nesneleri geçirmelisiniz, ardından kaynak hiyerarşisinden istemcileri yeniden yüklemeli veya hedef hiyerarşisine yeniden atamalısınız. İstemciler geçirildiğinde kullanılabilir durumda olmaları için nesneleri önce geçirirsiniz. İstemciyle ilişkili nesneler geçirme işleri kullanılarak geçirilir. İstemciyle ilişkili nesnelerin nasıl geçirileceği hakkında daha fazla bilgi için bkz. [geçiş işi stratejisi planlama](../../core/migration/planning-a-migration-job-strategy.md).  

 İstemcileri hedef hiyerarşisine geçirmeyi planlamanıza yardımcı olması için aşağıdaki bölümleri kullanın.  

-   [İstemcileri hedef hiyerarşiye geçirmeyi planlayın](#Planning_for_Client_Agent_Migration)  

-   [Geçiş sırasında istemcilerde korunan verilerin işlenmesini planlama](#Planning_for_Client_Data_Migration)  

-   [Geçiş sırasında envanter ve uyumluluk verilerini planlayın](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> İstemcileri hedef hiyerarşiye geçirmeyi planlama  
 İstemcileri bir kaynak hiyerarşisinden geçirdiğinizde, istemci bilgisayarındaki istemci yazılımı hedef hiyerarşisinin ürün sürümüyle eşleşecek şekilde yükseltir.  

-   **Configuration Manager 2007 kaynak hiyerarşisi:** Configuration Manager desteklenen bir sürümünü çalıştıran bir kaynak hiyerarşisinden istemcileri geçirdiğinizde, istemci yazılımı hedef hiyerarşinin istemci sürümüne yükseltir.  

-   **System Center 2012 Configuration Manager veya üzeri kaynak hiyerarşisi:** Aynı ürün sürümüne sahip hiyerarşiler arasında istemcileri geçirdiğinizde, istemci yazılımı değişmez veya yükseltme yapmaz. İstemci, bunun yerine, kaynak hiyerarşisinden hedef hiyerarşisindeki bir siteye yeniden atama yapar.  

    > [!NOTE]  
    >  Bir hiyerarşinin ürün sürümü hedef hiyerarşinize geçirmeyi desteklemediğinde, kaynak hiyerarşisindeki tüm siteleri ve istemcileri uyumlu ürün sürümüne yükseltin. Kaynak hiyerarşisi desteklenen bir ürün sürümüne yükseltme yaptıktan sonra, hiyerarşiler arasında geçirme yapabilirsiniz. Daha fazla bilgi için, [geçiş önkoşulları](../../core/migration/prerequisites-for-migration.md)içinde [geçiş Için Desteklenen Configuration Manager sürümleri](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) ' ne bakın.  

İstemci geçirmenizi planlamanıza yardımcı olması için aşağıdaki bilgileri kullanın:  

-   Bir kaynak siteden hedef siteye istemcileri yükseltmek veya yeniden atamak için, hedef hiyerarşisinde istemcileri dağıtmak için desteklenen istemci dağıtma yöntemlerinden herhangi birini kullanabilirsiniz. Tipik istemci dağıtma yöntemleri client push kurulumu, yazılım dağıtımı, Grup İlkesi ve yazılım güncelleme tabanlı istemci kurulumunu içerir. Daha fazla bilgi için bkz. [istemci yükleme yöntemleri](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Kaynak hiyerarşisinde istemci yazılımını çalıştıran cihazın en düşük donanım gereksinimlerini karşıladığından ve hedef hiyerarşisinde Configuration Manager sürümü tarafından desteklenen bir işletim sistemi çalıştırdığından emin olun.  

-   Bir istemciyi geçirmeden önce, istemcinin hedef hiyerarşisinde kullanacağı bilgileri geçirmek için bir geçiş işi çalıştırın.  

-   Yükseltme yapan istemciler dağıtımlar için çalıştırma geçmişini korur. Bu, dağıtımların hedef hiyerarşisinde gereksiz yere yeniden çalışmasını önler.  

    -   Configuration Manager 2007 istemcileri için reklam çalıştırma geçmişi korunur.  

    -   System Center 2012 Configuration Manager veya geçerli dalı Configuration Manager istemciler için dağıtım çalıştırma geçmişi korunur.  

-   Kaynak hiyerarşisi sitelerinden istemcileri seçtiğiniz herhangi bir sırada geçirebilirsiniz. Ancak, çok sayıda istemciyi tek seferde geçirmek yerine sınırlı sayıda istemciyi aşamalı olarak geçirmeyi düşünün. Aşamalı geçirme, yeni geliştirilen istemci ilk tam envanterini ve uygunluk verilerini atanan siteye gönderdiğinde, ağ bant genişliği gereksinimlerini ve sunucu işlemlerini azaltır.  

-   Configuration Manager 2007 istemcilerini geçirdiğinizde, mevcut istemci yazılımı istemci bilgisayarından kaldırılır ve yeni istemci yazılımı yüklenir.  

-   Configuration Manager App-v istemcisinin yüklü olduğu bir Configuration Manager 2007 istemcisini, App-V istemci sürümü 4,6 SP1 veya daha yeni bir sürüm olmadığı takdirde geçiremez.  

İstemci geçiş işlemini Configuration Manager konsolundaki **Yönetim** çalışma alanının **geçiş** düğümünde izleyebilirsiniz.  

İstemciyi hedef hiyerarşisine geçirdikten sonra, kaynak hiyerarşinizi kullanarak o aygıtı artık yönetemezsiniz ve istemciyi kaynak hiyerarşisinden kaldırmayı düşünmelisiniz. Hiyerarşileri geçirdiğinizde bunun bir gereksinim olmamasına karşın, bir kaynak hiyerarşisi raporunda geçirilen istemcinin belirlenmesini veya geçirme sırasında iki hiyerarşi arasındaki kaynak sayımının yanlış olmasını önlemeye yardımcı olur. Örneğin, bir geçirilen istemci kaynak site veritabanında kaldığında, artık hedef hiyerarşisi tarafından yönetildiği sırada o bilgisayarı yanlış şekilde yönetilmeyen olarak belirleyen bir yazılım güncellemeleri raporunu çalıştırabilirsiniz.  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a>Geçiş sırasında istemcilerde tutulan verilerin işlemesini planlayın  
Bir istemciyi kaynak hiyerarşisinden hedef hiyerarşisine geçirdiğinizde, bazı bilgiler aygıtta tutulurken, diğer bilgiler geçirme sonrası aygıta kullanılamaz.  

Aşağıdaki bilgiler istemci aygıtta tutulur:  

-   Bir istemciyi Configuration Manager veritabanındaki bilgileriyle ilişkilendiren benzersiz tanımlayıcı (GUID).  

-   İstemcilerin hedef hiyerarşisinde reklamları veya dağıtımları gereksiz yere yeniden çalıştırmasını önleyen reklam veya dağıtım geçmişi.  

Aşağıdaki bilgiler istemci aygıtta tutulmaz:  

-   İstemci önbelleğindeki dosyalar. Yazılımı yüklemek için istemci bu dosyalara gereksinim duyuyorsa, istemci bunları hedef hiyerarşisinden yeniden indirir.  

-   Henüz çalıştırılmamış tüm reklamlar veya dağıtımlar hakkında kaynak hiyerarşisinden bilgiler. İstemcinin geçirildikten sonra reklamları veya dağıtımları çalıştırmasını istiyorsanız, bunları hedef hiyerarşisinde istemciye yeniden dağıtmanız gerekir.  

-   Envanter hakkındaki bilgiler. İstemci geçirildikten ve yeni istemci verileri oluşturulduktan sonra istemci, bu bilgileri hedef hiyerarşisinde atanan siteye yeniden sonlandırır.  

-   Uygunluk verileri. İstemci geçirildikten ve yeni istemci verileri oluşturulduktan sonra istemci, bu bilgileri hedef hiyerarşisinde atanan siteye yeniden sonlandırır.  

İstemci geçirildiğinde, Configuration Manager istemci kayıt defteri ve dosya yolunda depolanan bilgiler korunmaz. Geçirme sonrasında bu ayarları yeniden uygulayın. Tipik ayarlar aşağıdakileri içerir:  

-   Güç düzenleri  

-   Oturum açma ayarları  

-   Yerel ilke ayarları  

Buna ek olarak, bazı uygulamaları yeniden yüklemeniz gerekebilir.  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Geçiş sırasında envanter ve uyumluluk verilerini planlama  
Bir istemciyi hedef hiyerarşisine geçirdiğinizde, istemci envanter ve uygunluk verileri kaydedilmez. Bu bilgiler bunun yerine, istemcinin atandığı siteye bilgilerini ilk gönderişinde hedef hiyerarşisinde yeniden oluşturulur. Sonuçta ortaya çıkan bant genişliği gereksinimlerini ve sunucu işlemlerini azaltmaya yardımcı olmak için, çok sayıda istemciyi tek seferde geçirmek yerine az sayıda istemciyi aşamalı olarak geçirmeyi düşünün.  

 Ayrıca, bir kaynak hiyerarşisinden donanım envanterine yönelik özelleştirmeleri geçiremezsiniz. Bunları hedef hiyerarşisinde geçirmeden bağımsız olarak girmeniz gerekir. Donanım envanterini genişletme hakkında daha fazla bilgi için bkz. [donanım envanterini yapılandırma](../../core/clients/manage/inventory/configure-hardware-inventory.md).  
