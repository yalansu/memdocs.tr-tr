---
title: Geçiş işlemleri
titleSuffix: Configuration Manager
description: Güncel dala Configuration Manager verileri ve istemcileri geçirmek için iş oluşturun ve çalıştırın.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a93269fc50c7bb39cd47f10e448d30742fc8ab22
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720922"
---
# <a name="operations-for-migrating-to-configuration-manager-current-branch"></a>Configuration Manager geçerli dala geçiş için işlemler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager geçiş için, desteklenen bir kaynak hiyerarşisindeki kaynak siteden verileri başarıyla topladıktan sonra verileri ve istemcileri geçirebilirsiniz. Veri ve istemcileri geçirmek üzere geçiş işleri oluşturmak ve çalıştırmak için aşağıdaki bölümlerdeki bilgileri kullanın ve ardından geçiş işlemini sona erdirin.  

-   [Geçiş işleri oluşturma ve düzenleme](#Create_Edit_migration_Jobs)  

-   [Geçiş işlerini çalıştırma](#Run_Migration_Jobs)  

-   [Paylaşılan bir dağıtım noktasını yükseltme veya yeniden atama](#BKMK_ProcUpgrdSS)  

-   [Geçiş çalışma alanında geçiş etkinliğini izleme](#Monitor_MIgration)  

-   [İstemcileri geçirme](#BKMK_MigrateClients)  

-   [Geçişi tamamlama](#Complete_Migration)  

##  <a name="create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Geçiş işleri oluşturma ve düzenleme  
 Veri geçiş işleri oluşturmak, koleksiyon tabanlı geçiş işleri için dışlama listesini düzenlemek, paylaşılan dağıtım noktalarını ayarlamak ve geçiş işi zamanlamalarını düzenlemek için aşağıdaki yordamları kullanın.  

> [!NOTE]  
>  Koleksiyonlara göre geçiş yapan bir geçiş işi oluşturmaya yönelik aşağıdaki yordam yalnızca Configuration Manager 2007 ' nin desteklenen bir sürümünü çalıştıran kaynak hiyerarşileri için geçerlidir. Koleksiyon tabanlı geçiş işi türü, bir System Center 2012 Configuration Manager veya geçerli dal kaynak hiyerarşisinden Configuration Manager geçiş yaparken kullanılamaz.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Koleksiyonlara göre geçirilecek geçiş işi oluşturma  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin ve **geçiş işleri**' ni seçin.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **geçiş işi oluştur**' u seçin.  

4.  Geçiş Işi oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdakileri ayarlayıp **Tamam**' ı seçin:  

    -   Geçiş işi için bir ad belirtin.  

    -   **İş türü** açılan listesinden, **Koleksiyon geçişi**'ni seçin.  

5.  **Koleksiyonları seçin** sayfasında, aşağıdakileri ayarlayın ve ardından **İleri**' yi seçin:  

    -   Geçirmek istediğiniz koleksiyonları seçin.  

    -   Yalnızca koleksiyonları geçirmek istiyorsanız, bu koleksiyonlarla ilişkilendirilmiş nesneleri değil, **belirtilen koleksiyonlarla ilişkilendirilmiş nesneleri geçir**seçeneğinin işaretini kaldırın. Bu seçeneğin işaretini kaldırırsanız, bu işte hiçbir ilişkili nesne geçirilmez ve 6. ve 7. adımları atlayabilirsiniz.  

6.  **Nesneleri seçin** sayfasında, geçiş yapmak istemediğiniz herhangi bir nesne türü veya belirli bir kullanılabilir nesne seçimini kaldırın. Varsayılan olarak, tüm ilişkilendirilmiş nesne türleri ve kullanılabilir nesneler seçilir. **İleri**’yi seçin.  

7.  **Içerik sahipliği** sayfasında, listelenen her bir kaynak sitenin içerik sahipliğini hedef hiyerarşideki bir siteye atayın ve ardından **İleri**' yi seçin.  

8.  **Güvenlik kapsamı** sayfasında, bu geçiş işinde geçirilecek nesnelere atamak için bir veya daha fazla rol tabanlı yönetim güvenlik kapsamı seçin ve ardından **İleri**' yi seçin.  

9. **Koleksiyon sınırlandırma** sayfasında, hedef hiyerarşiden bir koleksiyonu listelenen her koleksiyonun kapsamını sınırlayacak şekilde ayarlayın ve ardından **İleri**' yi seçin. Hiçbir koleksiyon listelenmiyorsa, **İleri**' yi seçin.  

10. **Site kodu değiştirme** sayfasında, listelenen her koleksiyon için Configuration Manager 2007 site kodunu değiştirmek üzere hedef hiyerarşiden bir site kodu atayın ve ardından **İleri**' yi seçin. Hiçbir koleksiyon listelenmiyorsa, **İleri**' yi seçin.  

11. Daha sonra görüntülenmek üzere görüntülenen bilgileri kaydetmek için **bilgileri gözden geçir** sayfasında **dosyaya kaydet** ' i seçin. Devam etmeye hazırsanız, **İleri**' yi seçin.  

12. **Ayarlar** sayfasında, geçiş işi ne zaman çalıştırılacağınızı ayarlayın, bu geçiş işi için gerekli olan diğer ayarları seçin ve ardından **İleri**' yi seçin.  

13. Ayarları onaylayın ve sihirbazı doğrulayın.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Nesnelere göre geçirilecek geçiş Işi oluşturma  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin ve **geçiş işleri**' ni seçin.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **geçiş işi oluştur**' u seçin.  

4.  Geçiş Işi oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdaki ayarı yapın ve ardından **İleri**' yi seçin:  

    -   Geçiş işi için bir ad belirtin.  

    -   **İş türü** açılan listesinden, **Nesne geçişi**'ni seçin.  

5.  **Nesneleri Seç** sayfasında, geçirmek istediğiniz nesne türlerini seçin. Varsayılan olarak, seçtiğiniz her nesne türü için kullanılabilir tüm nesneler seçilidir.  

6.  **Içerik sahipliği** sayfasında, listelenen her bir kaynak sitenin içerik sahipliğini hedef hiyerarşideki bir siteye atayın ve ardından **İleri**' yi seçin. Listelenen kaynak site yoksa **İleri**' yi seçin.  

7.  **Güvenlik kapsamı** sayfasında, bu geçiş işindeki nesnelere atamak için bir veya daha fazla rol tabanlı yönetim güvenlik kapsamı seçin ve ardından **İleri**' yi seçin.  

8.  Daha sonra görüntülenmek üzere görüntülenen bilgileri kaydetmek için **bilgileri gözden geçir** sayfasında **dosyaya kaydet** ' i seçin. Devam etmeye hazırsanız, **İleri**' yi seçin.  

9. **Ayarlar** sayfasında, geçiş işinin ne zaman çalışacağını ayarlayın ve bu geçiş işi için gereksinim duyduğunuz diğer ayarları seçin. Ardından **İleri**' yi seçin.  

10. Ayarları onaylayın ve sihirbazı doğrulayın.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Değiştirilen nesneleri geçirmek için bir geçiş işi oluşturma  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin ve **geçiş işleri**' ni seçin.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **geçiş işi oluştur**' u seçin.  

4.  Geçiş Işi oluşturma Sihirbazı ' nın **genel** sayfasında, aşağıdakileri ayarlayın ve ardından **İleri**' yi seçin:  

    -   Geçiş işi için bir ad belirtin.  

    -   **İş türü** aşağı açılan listesinde **geçişten sonra değiştirilen nesneler**' i seçin.  

5.  **Nesneleri Seç** sayfasında, geçirmek istediğiniz nesne türlerini seçin. Varsayılan olarak, seçtiğiniz her nesne türü için kullanılabilir tüm nesneler seçilidir.  

6.  **Içerik sahipliği** sayfasında, listelenen her bir kaynak sitenin içerik sahipliğini hedef hiyerarşideki bir siteye atayın ve ardından **İleri**' yi seçin. Listelenen kaynak site yoksa **İleri**' yi seçin.  

7.  **Güvenlik kapsamı** sayfasında, bu geçiş işindeki nesnelere atamak için bir veya daha fazla rol tabanlı yönetim güvenlik kapsamı seçin ve ardından **İleri**' yi seçin.  

8.  Daha sonra görüntülenmek üzere görüntülenen bilgileri kaydetmek için **bilgileri gözden geçir** sayfasında **dosyaya kaydet** ' i seçin. Devam etmeye hazırsanız, **İleri**' yi seçin.  

9. **Ayarlar** sayfasında, geçiş işinin ne zaman çalışacağını ayarlayın ve bu geçiş işi için gerekli olan diğer ayarları seçin. Diğer geçiş işi türlerinin aksine, bu geçiş işi Configuration Manager veritabanındaki daha önce geçirilmiş nesnelerin üzerine yazılmalıdır. **İleri**’yi seçin.  

10. Ayarları onaylayın ve Sihirbazı sona erdirin.  

###  <a name="modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a>Geçiş için dışlama listesini değiştirme  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, dışlama listesine erişim kazanmak için **geçiş** ' i seçin. Dışlama listesine **Kaynak Hiyerarşi** veya **Geçiş İşleri** düğümünden de erişebilirsiniz.  

3.  **Giriş** sekmesinde, **geçiş** grubunda, **dışlama listesini düzenle**' yi seçin.  

4.  **Dışlama listesini düzenle** iletişim kutusunda, dışlama listesinden kaldırmak istediğiniz dışlanan nesneyi seçin ve ardından **Kaldır**' ı seçin.  

5.  Değişiklikleri kaydetmek ve düzenlemeyi sona ermesini sağlamak için **Tamam** ' ı seçin. Geçerli değişiklikleri iptal etmek ve kaldırdığınız tüm nesneleri geri yüklemek için, **iptal**' i seçin ve ardından **Hayır**' ı seçin. Böylece nesnelerin kaldırılması iptal edilir ve **Çıkarma Listesini Düzenle** iletişim kutusu kapanır.  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Dağıtım noktalarını kaynak hiyerarşisinden paylaşma  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin, **kaynak hiyerarşisi**' ni seçin ve ardından ayarlamak istediğiniz kaynak siteyi seçin.  

3.  **Giriş** sekmesinde, **kaynak site** grubunda, **Yapılandır**' ı seçin.  

4.  **Kaynak site kimlik bilgileri** iletişim kutusunda, **kaynak site sunucusu için dağıtım noktası paylaşımını etkinleştir**' i seçin ve ardından **Tamam**' ı seçin.  

5.  Veri toplama bittiğinde **Kapat**' ı seçin.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Geçiş işinin zamanlamasını değiştirme  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin ve **geçiş işleri**' ni seçin.  

3.  Değiştirmek istediğiniz geçiş işini seçin. **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.  

4.  Geçiş işinin özelliklerinde, **Ayarlar** sekmesini seçin, geçiş işinin çalışma zamanını değiştirin ve ardından **Tamam**' ı seçin.  

##  <a name="run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Geçiş işlerini çalıştırma  
 Henüz başlamamış bir geçiş işini çalıştırmak için aşağıdaki yordamı kullanın.  


1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin ve **geçiş işleri**' ni seçin.  

3.  Çalıştırmak istediğiniz geçiş işini seçin. **Giriş** sekmesinde, **geçiş Işi** grubunda, **Başlat**' ı seçin.  

4.  Geçiş işini başlatmak için **Evet** ' i seçin.  

##  <a name="upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a>Paylaşılan bir dağıtım noktasını yükseltme veya yeniden atama  
 Configuration Manager 2007 kaynak sitesinden paylaşılan desteklenen bir dağıtım noktasını yükseltebilir (veya bir Configuration Manager kaynak sitesinden paylaşılan desteklenen bir dağıtım noktasını yeniden atayabilirsiniz), hedef hiyerarşideki bir dağıtım noktası olmasını sağlayabilirsiniz.  

> [!IMPORTANT]  
>  Configuration Manager 2007 dal dağıtım noktasını yükseltmeden önce, Configuration Manager 2007 istemci yazılımını şube dağıtım noktası bilgisayarından kaldırmanız gerekir. Dağıtım noktasını yükseltmeye çalıştığınızda Configuration Manager 2007 istemci yazılımı yüklenirse, yükseltme başarısız olur ve daha önce şube dağıtım noktasına dağıtılmış olan içerikler bilgisayardan kaldırılır.  

> [!CAUTION]  
>  Paylaşılan bir dağıtım noktasını yükselttiğinizde veya yeniden atadığınızda, dağıtım noktası site sistem rolü ve site sistem bilgisayarı kaynak siteden kaldırılır ve seçtiğiniz hedef hiyerarşideki siteye dağıtım noktası olarak eklenir.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Paylaşılan bir dağıtım noktasını yükseltme veya yeniden atama  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin ve **kaynak hiyerarşisi**' ni seçin.  

3.  Yükseltmek istediğiniz dağıtım noktasının sahibi olan siteyi seçin, **paylaşılan dağıtım noktaları** sekmesini seçin ve yükseltmek veya yeniden atamak istediğiniz uygun dağıtım noktasını seçin.  

4.  **Dağıtım noktası** sekmesindeki **dağıtım noktası** grubunda **yeniden ata**' yı seçin.  

5.  Paylaşılan dağıtım noktasını yeniden atama Sihirbazı 'ndaki ayarları, hedef hiyerarşi için yeni bir dağıtım noktası yüklediğiniz gibi, aşağıdaki ek bilgilerle belirtin:  

    -   **Içerik dönüştürme** sayfasında, var olan içeriğin dönüştürülmesi için gereken alanla ilgili kılavuzu gözden geçirin. Ardından, sihirbazın **sürücü ayarları** sayfasında, dağıtım noktası bilgisayarının seçilen sürücüsünde gereken miktarda boş disk alanı olduğundan emin olun.  

6.  Ayarları onaylayın ve Sihirbazı sona erdirin.  

##  <a name="monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Geçiş çalışma alanında geçiş etkinliğini izleme  
 Geçişi izlemek için Configuration Manager konsolunu kullanın.  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin ve **geçiş işleri**' ni seçin.  

3.  İzlemek istediğiniz geçiş işini seçin.  

4.  **Özet** ve **İşteki Nesneler**sekmelerinde seçili geçiş işinin ayrıntılarını ve durumunu görüntüleyin.  

##  <a name="migrate-clients"></a><a name="BKMK_MigrateClients"></a> İstemcileri geçirme  
 Hiyerarşi arasında istemciler için veri geçirdikten sonra, geçişi bitirmeden önce, istemcileri hedef hiyerarşiye geçirmeyi planlayın. Hiyerarşiler arasında istemcilerin geçişi, kaynak hiyerarşiye atanan bilgisayarlardan Configuration Manager istemci yazılımının kaldırılmasını ve ardından hedef hiyerarşisinden Configuration Manager istemci yazılımını yüklemeyi içerir. Hedef hiyerarşiden istemciyi yüklediğinizde, ayrıca istemciyi bu hiyerarşideki bir birincil siteye atarsınız. İstemcileri geçirme hakkında daha fazla bilgi için bkz. [istemci geçiş stratejisi planlama](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="finish-migration"></a><a name="Complete_Migration"></a>Geçişi tamamlama  
 Kaynak hiyerarşisinden geçiş işlemini yapmak için bu yordamı kullanın.  

1.  Configuration Manager konsolunda, **Yönetim**' i seçin.  

2.  **Yönetim** çalışma alanında, **geçiş**' i genişletin ve **kaynak hiyerarşisi**' ni seçin.  

3.  Configuration Manager 2007 kaynak hiyerarşisi için, kaynak hiyerarşinin en alt düzeyinde bulunan bir kaynak site seçin. Bir System Center 2012 Configuration Manager veya geçerli dal kaynağı hiyerarşisinde Configuration Manager, kullanılabilir kaynak siteyi seçin.  

4.  **Giriş** sekmesinde, **Temizleme** grubunda, **veri toplamayı durdur**' u seçin.  

5.  Eylemi doğrulamak için **Evet** 'i seçin.  

6.  Configuration Manager 2007 kaynak hiyerarşisi için, sonraki adıma geçmeden önce 3, 4 ve 5. adımları tekrarlayın. Hiyerarşinin en altından üst kısımdaki her bir sitede bulunan bu adımları izleyin. System Center 2012 Configuration Manager veya geçerli dal kaynak hiyerarşisi Configuration Manager bir sonraki adımla devam edin.  

7.  **Giriş** sekmesinde, **Temizleme** grubunda, **geçiş verilerini temizle**' yi seçin.  

8.  **Geçiş verilerini temizle** iletişim kutusunda, **kaynak hiyerarşi** açılan listesinden, kaynak hiyerarşinin en üst düzey sitesinin site kodunu ve site sunucusunu seçin ve ardından **Tamam**' ı seçin.  

9. Kaynak hiyerarşinin geçiş işlemini sona erdirmeyi sağlamak için **Evet** ' i seçin.  
