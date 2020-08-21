---
title: Uygulamalar için yönetim görevleri
titleSuffix: Configuration Manager
description: Configuration Manager uygulamalarını ve dağıtım türlerini yönetin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 15c1be9ed388356e17f8591123114dccf7bcd612
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695214"
---
# <a name="management-tasks-for-configuration-manager-applications"></a>Configuration Manager uygulamalar için yönetim görevleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager uygulamalarını ve dağıtım türlerini yönetmenize yardımcı olması için bu makaledeki bilgileri kullanın.  

Uygulamalar ve dağıtım türleri oluşturma konusunda yardım için bkz. [uygulama oluşturma](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Uygulamanın veya dağıtım türünün türüne bağlı olarak bazı yönetim seçenekleri kullanılamayabilir.  

##  <a name="manage-applications"></a>Uygulamaları yönetme  
 **Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**  >  **uygulamaları**' nı genişletin, yönetilecek uygulamayı seçin ve ardından bir yönetim görevi seçin.  

|Görev|Ayrıntılar|  
|----------|-------------|  
|**Erişim Hesaplarını Yönet**|Seçilen uygulama ile ilişkilendirilen içerik için izin verilen erişim düzeyini belirleyebileceğiniz **Erişim Hesaplarını Yönet** iletişim kutusunu açar.|  
|**Önceden hazırlanan Içerik dosyası oluştur**|İçeriğin uzak dağıtım noktalarına dağıtımını yönetmenize yardımcı olan **Önceden Hazırlanan İçerik Dosyası Oluşturma Sihirbazı** 'nı açar. Zamanlama ve kısıtlama, uzak dağıtım noktası için geçerli bir çözüm sağlamadığında dağıtım noktasında içeriği önceden hazırlayabilirsiniz.<br /><br /> Bkz. [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Değişiklik Geçmişi**|Bu uygulamada yapılan düzeltmelerin özelliklerini görüntülemenize, eski uygulama düzeltmelerini silmenize ve bu uygulamanın eski sürümlerini geri yüklemenize olanak sağlayan **uygulama düzeltme geçmişi** iletişim kutusunu açar.<br /><br /> Bkz. [uygulamaları gözden geçirme ve değiştirme](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Dağıtım Türü Oluştur**|Seçili uygulamaya yeni bir dağıtım türü eklemenize olanak sağlayan **dağıtım türü oluşturma Sihirbazı** ' nı açar.<br /><br /> Bkz. [uygulama oluşturma](../../apps/deploy-use/create-applications.md).|  
|**Istatistikleri Güncelleştir**|**İzleme** çalışma alanının **Dağıtımlar** düğümünde görüntülenen bu uygulamanın dağıtımları hakkındaki bilgileri güncelleştirir.<br /><br /> Bkz. [Configuration Manager konsolundan uygulamaları izleme](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Yeniden uygulamaya koy**|**Devre dışı bırakma** yönetim görevi kullanılarak kullanımdan kaldırılan bir uygulamayı tekrar belirtir.|  
|**Devre dışı bırak**|Bir uygulamayı devre dışı bırakırsanız, artık dağıtım için kullanılamaz, ancak uygulamanın uygulaması ve dağıtımları silinmez. Bu uygulamanın istemci bilgisayarlarında yüklü olan mevcut kopyaları kaldırılmayacak. Uygulama için tüm düzeltmeler 60 gün sonra Configuration Manager'dan silinir. Ancak, uygulamanın yüklü kopyaları kaldırılmaz.<br /><br /> Bir uygulamayı silmek için, öncelikle uygulamayı devre dışı bırakmanız, tüm dağıtımları silmeniz, diğer dağıtımlar tarafından uygulamaya yapılan başvuruları kaldırmanız ve ardından uygulamanın tüm düzeltmelerini silmeniz gerekir.<br /><br /> Bkz. [uygulamaları gözden geçirme ve değiştirme](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Dışarı Aktarma**|Seçilen uygulamaları, daha sonra arşivleyebileceğiniz veya başka bir siteye yükleyebileceğiniz bir. zip dosyasına aktarmanızı sağlayan **Uygulama Verme Sihirbazı** ' nı açar. Uygulama içeriğini dışa aktarmayı seçerseniz, içeriğe sahip bir klasör oluşturulur.<br /><br /> Ayrıca uygulama bağımlılıklarını, yerine geçme ilişkilerini ve koşulları ve uygulama için içeriği ve bağımlılıklarını dışarı aktarabilirsiniz.<br /><br /> Windows PowerShell cmdlet 'i **dışarı aktarma-Cmappu**, aynı işlevi yapar. Daha fazla bilgi için bkz. [Export-Cmappte](/powershell/module/configurationmanager/export-cmapplication?view=sccm-ps).|  
|**Silme**|Şu anda seçili olan uygulamayı siler.<br /><br /> Diğer uygulamaların bağımlılığının bulunduğu, etkin bir dağıtımının olduğu veya bağımlı görev dizilerinin olduğu durumlarda bir uygulamayı silemezsiniz.|  
|**Dağıtımı Benzet**|Bir uygulamayı yüklemeden veya kaldırmadan uygulama dağıtımının sonuçlarını sınayabileceğiniz **Uygulama Dağıtımını Benzetme Sihirbazı** 'nı açar.<br /><br /> Bkz. [uygulama dağıtımlarının benzetimini](../../apps/deploy-use/simulate-application-deployments.md)yapma.|  
|**Dağıtma**|Seçilen uygulamayı hiyerarşinizdeki bilgisayar koleksiyonlarına dağıtabileceğiniz **Yazılım Dağıtma Sihirbazı** 'nı açar.<br /><br /> Bkz. [uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md).|  
|**İçeriği Dağıt**|Seçilen uygulamanın içeriğini hiyerarşinizdeki dağıtım noktalarına kopyalayabileceğiniz **İçerik Dağıtma Sihirbazı** 'nı açar.<br /><br /> Bkz. [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**İlişkileri Görüntüle**|Seçilen uygulamaların diğer uygulamalara ilişkilerinin grafik diyagramını gösterir. Aşağıdakilerden birini seçin:<br><br><ul><li>**Bağımlılık** – seçilen uygulamaya bağımlı uygulamaları ve Seçilen uygulamanın bağımlı olduğu uygulamaları gösterir.</li><li>**Yerine geçme** : Seçili uygulamanın yerine geçen uygulamaları ve Seçili uygulamanın yerine geçen uygulamaları gösterir.</li><li>**Genel koşullar** – bu uygulama tarafından başvurulan genel koşulları gösterir.</li></ol><br /> Bkz. [uygulamaları gözden geçirme ve değiştirme](../../apps/deploy-use/revise-and-supersede-applications.md) ve [genel koşullar oluşturma](../../apps/deploy-use/create-global-conditions.md).|  
|**Uygulamaları Kopyala**|Yeni bir tane oluşturmak için uygulamaları kopyalayın veya çoğaltın Configuration Manager. Bu eylem, bir şeyi test etmek veya benzer bir uygulama oluşturmanız gerektiğinde faydalıdır. Site, adlı yeni bir uygulama oluşturur ve bu ada **kopya** eklenir. Site meta verilerin çoğunu yeni uygulamaya kopyalarken, hiçbir dağıtımı kopyalamaz.|

##  <a name="manage-deployment-types"></a>Dağıtım türlerini Yönet  
 **Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin, **uygulamalar**' ı seçin ve ardından yönetmek istediğiniz dağıtım türünü içeren uygulamayı seçin. Ayrıntılar bölmesinde, **dağıtım türleri** sekmesini seçin, yönetmek istediğiniz dağıtım türünü seçin ve ardından bir yönetim görevi seçin.  

|Görev|Ayrıntılar|  
|----------|-------------|  
|**Önceliği Arttır**|Seçilen dağıtım türünün önceliğini arttırır. Dağıtım türleri sırayla değerlendirilir. Bir dağıtım türü belirtilen gereksinimleri karşıladığında, çalışır ve daha sonra öncelik listesinde başka hiçbir dağıtım türü değerlendirilir.|  
|**Önceliği Azalt**|Seçilen dağıtım türünün önceliğini azaltır.|  
|**Silme**|Seçilen dağıtım türünü siler.<br><br>Başka bir uygulamadaki bir dağıtım türü tarafından başvurulduğunda bir dağıtım türünü silemezsiniz.<br>Bir dağıtım türünü silmek için, diğer dağıtım türlerinde olan dağıtım türüne tüm bağımlılıkları kaldırmanız gerekir.<br>Ayrıca, silmek istediğiniz dağıtım türüne başvuran bir dağıtım türüne sahip tüm uygulamaların önceki düzeltmelerini de kaldırmanız gerekir.|  
|**İçeriği Güncelleştir**|Seçilen dağıtım türü için içeriği yeniler.<br /><br /> Sanal uygulamasına sahip bir dağıtım türü için bu sihirbazı başlattığınızda **Içerik Güncelleştirme Sihirbazı** başlatılır. Bu sihirbaz, seçili sanal uygulama için yayımlama seçeneklerini ve gereksinim kurallarını değiştirmenize olanak sağlar. Daha fazla bilgi için bkz. [uygulama oluşturma](../../apps/deploy-use/create-applications.md).<br /><br /> Dağıtım türünün içeriğini yenilediğinizde uygulamanın yeni bir düzeltmesi oluşturulur. Bu durum, istemci aygıtlarının yeni uygulama ile birlikte güncelleştirilmesine sebep olabilir.|