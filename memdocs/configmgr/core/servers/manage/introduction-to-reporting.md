---
title: Raporlamaya giriş
titleSuffix: Configuration Manager
description: Configuration Manager raporlamayı yönetmek için kullanabileceğiniz araç ve kaynak kümesi hakkında bilgi edinin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bfed31b820ac1f09b240122207b5bf27e432b10a
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607529"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Configuration Manager 'de raporlamaya giriş

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager raporlama, SQL Server Reporting Services (SSRS) ve Power BI Rapor Sunucusu 'ın gelişmiş raporlama özelliklerini kullanmanıza yardımcı olan bir araç ve kaynak kümesi sağlar. Her iki raporlama platformu da özel raporlar için zengin yazma deneyimleri sağlar. Raporlama, kuruluşunuzda bulunan çok sayıda Configuration Manager verileri toplamanıza, düzenlemenize ve sunmanıza yardımcı olur. Configuration Manager, Raporlama Hizmetleri 'nde değişiklik yapmadan kullanabileceğiniz çok sayıda önceden tanımlı rapor sağlar. Gereksinimlerinizi karşılamak için varsayılan raporları çoğaltabilir ve değiştirebilir veya özel raporlar oluşturabilirsiniz.

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services, kuruluşunuz için raporlar oluşturmanıza, dağıtmanıza ve yönetmenize yardımcı olacak, kullanıma yönelik kullanıma yönelik bir araç ve hizmet yelpazesi sunar. Ayrıca, raporlama işlevini genişletmenizi ve özelleştirmenizi sağlayan programlama özellikleri de vardır. Raporlama Hizmetleri, farklı türlerde veri kaynakları için kapsamlı raporlama işlevi sağlayan, sunucu tabanlı bir raporlama platformudur.

Configuration Manager, SQL Server Reporting Services birincil raporlama çözümü olarak kullanır. Raporlama Hizmetleriyle entegrasyon, aşağıdaki avantajları sağlar:  

- Configuration Manager veritabanını sorgulamak için endüstri standardı bir raporlama sistemi kullanır.  

- Raporları Configuration Manager rapor görüntüleyicisini kullanarak veya rapor ile Web tabanlı bağlantı olan Rapor Yöneticisi kullanarak görüntüler.  

- Yüksek performans, kullanılabilirlik ve ölçeklenebilirlik sağlar.  

- Kullanıcıların abone olabileceği raporlara abonelik sağlar. Örneğin, bir yönetici, bir yazılım güncelleştirmesi dağıtımının durumunu ayrıntılarıyla belirten, her gün e-postayla gönderilen bir rapora abone olur.

- Raporları farklı türlerde popüler biçimlerde dışa aktarır.  

Daha fazla bilgi için bkz. [SQL Server Reporting Services (SSRS) nedir?](/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports)

## <a name="power-bi-report-server"></a>Power BI Rapor Sunucusu

<!-- 3721603 -->

Sürüm 2002 ' den başlayarak, Power BI Rapor Sunucusu Configuration Manager raporlama ile tümleştirin. Bu tümleştirme size modern görselleştirme ve daha iyi performans sağlar. Bu, SQL Server Reporting Services zaten mevcut olana benzer Power BI raporlar için konsol desteği ekler. Daha fazla bilgi için bkz. [Power BI rapor sunucusu tümleştirme](powerbi-report-server.md).

Power BI Rapor Sunucusu, raporları görüntüleyen ve yönettiğiniz bir Web portalına sahip şirket içi rapor sunucusudur. Power BI raporlar, sayfalandırılmış raporlar, mobil raporlar ve KPI 'ler oluşturmak için araçlar içerir. Daha fazla bilgi için bkz. [Power BI rapor sunucusu nedir?](/power-bi/report-server/get-started).

## <a name="reporting-services-point"></a>Raporlama hizmetleri noktası

Raporlama Hizmetleri noktası, Microsoft SQL Server Reporting Services çalıştıran bir sunucuya eklediğiniz bir site sistem rolüdür. Raporlama Hizmetleri noktası aşağıdaki işlevleri yapar:

- Configuration Manager rapor tanımlarını Raporlama Hizmetleri 'ne kopyalar
- Rapor kategorilerine göre rapor klasörleri oluşturur
- Rapor klasörlerinde ve raporlarında güvenlik ilkesini ayarlar. Bu ilkeler, yönetici kullanıcılar Configuration Manager için rol tabanlı izinleri temel alır. 10 dakikalık bir aralıkta, Raporlama Hizmetleri noktası, değişiklik yaptıysanız güvenlik ilkesini yeniden uygulamak için Raporlama Hizmetleri 'ne bağlanır.

Bir Raporlama Hizmetleri noktasının nasıl planlanacağı ve yükleneceği hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Raporlama planı](planning-for-reporting.md)

- [Raporlamayı yapılandırma](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Configuration Manager raporları

Configuration Manager, 50 ' den fazla rapor klasöründeki 400 üzerinde rapor tanımları sağlar. Raporlama Hizmetleri noktası yükleme işlemi sırasında, onları SQL Server Reporting Services kök rapor klasörüne kopyalar. Configuration Manager konsolu raporları gösterir ve bunları rapor kategorisine göre alt klasörlerde düzenler.

Raporlar Configuration Manager hiyerarşisini yukarı veya aşağı yaymayın. Bunlar yalnızca sizin oluşturduğunuz sitenin veritabanına karşı çalışır. Configuration Manager genel verileri hiyerarşinin tamamında çoğalttığından, raporlardaki hiyerarşi genelinde bilgilere erişebilirsiniz. Bir rapor, bir site veritabanından veri aldığında, geçerli site ve alt siteler için site verilerine, hiyerarşideki her site için global verilere erişimi vardır.

Diğer Configuration Manager nesneleri gibi, bir yönetici kullanıcının raporları çalıştırmak veya değiştirmek için uygun izinlere sahip olması gerekir. Bir raporu çalıştırmak için bir yönetici kullanıcının nesne için **Raporu Çalıştır** iznine sahip olması gerekir. Bir raporu oluşturmak veya değiştirmek için bir yönetici kullanıcının nesne için **Raporu Değiştir** iznine sahip olması gerekir.

### <a name="create-and-modify-reports"></a>Raporları oluşturma ve değiştirme

Raporlama Hizmetleri tabanlı raporlar için Configuration Manager, model tabanlı ve SQL tabanlı raporlar için özel yazma ve düzen aracı olarak Microsoft SQL Server Rapor Oluşturucusu kullanır. Configuration Manager konsolunda bir rapor oluşturduğunuzda veya düzenlediğinizde Rapor Oluşturucusu açılır. Daha fazla bilgi için bkz. [Raporlama Için işlemler ve bakım](operations-and-maintenance-for-reporting.md).

Sürüm 2002 ' den başlayarak Power BI raporları oluşturmak veya düzenlemek için, konsolu Power BI Desktop tümleştirilir. Daha fazla bilgi için bkz. [Power BI raporları oluşturma](powerbi-report-server.md#create-power-bi-reports).

### <a name="run-reports"></a>Raporları çalıştırma

Configuration Manager konsolunda Raporlama Hizmetleri tabanlı bir rapor çalıştırdığınızda, rapor Görüntüleyici açılır ve Raporlama Hizmetleri 'ne bağlanır. Gerekli herhangi bir rapor parametresini belirttikten sonra, Raporlama hizmetleri verileri alır ve sonuçları görüntüleyicide görüntüler. Ayrıca SQL Services Raporlama Hizmetleri'ne bağlanabilir, site için veri kaynağına bağlanabilir ve raporları çalıştırabilirsiniz.

Sürüm 2002 ' den başlayarak, Power BI tabanlı bir rapor çalıştırdığınızda Web tarayıcısında açılır.

### <a name="report-prompts"></a>Rapor istemleri

Bir rapor oluşturduğunuzda veya değiştirdiğinizde bir rapor istemi veya parametresi yapılandırabilirsiniz. Bir raporun aldığı verileri sınırlamak veya hedeflemek için Rapor istemleri oluşturun. Bir rapor, birden fazla istem içerebilir. İstem adlarının benzersiz olduğundan ve tanımlayıcılara yönelik SQL Server kurallara uyan alfasayısal karakterler içerdiğinden emin olun.

Bir raporu çalıştırdığınızda, istem gerekli bir parametre için bir değer ister. Parametre değerine bağlı olarak, rapor verilerini alır. Örneğin, **belirli bir bilgisayar Için bilgisayar bilgileri** rapor bir bilgisayar adı ister. Raporlama Hizmetleri, belirtilen değeri raporun SQL ifadesinde tanımlı bir değişkene geçirir.

### <a name="report-links"></a>Rapor bağlantıları

Configuration Manager rapor bağlantıları, ek verilere kolay erişim sağlamak için bir kaynak raporda kullanılır. Örneğin, kaynak rapordaki her bir öğe hakkında daha ayrıntılı bilgilere bağlantı verebilir. Hedef rapor, bir veya daha fazla istemin çalıştırılmasını gerektiriyorsa, kaynak raporun her bir istem için uygun değerler bulunan bir sütun içermesi gerekir.

Bağlantının, istem değeri ile sütun numarasını belirtmesi gerekir. Örneğin:

- Sitenin yakın zamanda bulduğu bilgisayarları listeleyen bir rapor vardır.
- Belirli bir bilgisayar için sitenin aldığı son iletileri listeleyen başka bir rapora bağlarsınız.
- Bağlantıyı oluşturun ve `2` kaynak raporundaki bu sütunun bilgisayar adını içerdiğini belirtin. Bu değer, hedef rapor için gerekli bir istem.
- Kaynak raporu çalıştırırsanız, her veri satırının solunda bir bağlantı simgesi görüntülenir.
- Bir satırda simgeyi seçersiniz ve rapor Görüntüleyicisi bu satır için belirtilen sütundaki değeri hedef raporun istem değeri olarak geçirir.

Bir rapor için yalnızca bir bağlantı yapılandırabilirsiniz ve bu bağlantı yalnızca tek bir hedef rapora bağlanabilir.

> [!WARNING]  
> Bir hedef raporu farklı bir rapor klasörüne taşırsanız, hedef raporun konumu değişir. Configuration Manager, kaynak rapordaki rapor bağlantısını yeni konum ile otomatik olarak güncelleştirmez ve bağlantı kaynak raporda çalışmaz.

## <a name="report-folders"></a>Rapor klasörleri

Rapor klasörleri, Raporlama hizmetlerinde Configuration Manager depolayan raporları sıralamak ve filtrelemek için bir yöntem sağlar. Yönetim için çok sayıda raporunuz olduğunda rapor klasörleri faydalıdır. Bir raporlama hizmetleri noktası yüklediğinizde, raporlar Raporlama Hizmetleri 'ne kopyalanır ve bunları 50 ' den fazla rapor klasörü olarak düzenler. Rapor klasörleri salt okunurdur. Bunları Configuration Manager konsolunda değiştiremezsiniz.

## <a name="report-subscriptions"></a>Rapor abonelikleri

Raporlama hizmetlerindeki rapor aboneliği, bir raporu belirli bir zamanda veya bir olaya yanıt olarak teslim etmek için yinelenen bir istedir. Abonelik bir uygulama dosyası biçiminde belirtirsiniz. Abonelikler, bir raporu talep üzerine çalıştırmaya bir alternatif sunar. Talep üzerine raporlama, raporu her görüntülemek istediğinizde onu aktif şekilde seçmenizi gerektirir. Zıt şekilde, abonelikler, bir raporun gönderimini planlamak ve ardından otomatik hale getirmek üzere kullanılabilir.

Configuration Manager konsolunda rapor aboneliklerini yönetebilirsiniz. Rapor sunucusu abonelikleri işler. Sunucuya dağıtılan teslim uzantılarını kullanarak bunları dağıtır. Varsayılan olarak, bir paylaşımlı klasöre veya bir e-posta adresine raporlar gönderen abonelikler oluşturabilirsiniz.

Daha fazla bilgi için bkz. [rapor aboneliklerini yönetme](operations-and-maintenance-for-reporting.md#bkmk_subscription).

## <a name="report-builder"></a>Rapor Oluşturucusu

Raporlama Hizmetleri tabanlı raporlar için Configuration Manager, model tabanlı ve SQL tabanlı raporlar için özel yazma ve düzenleyici aracı olarak Microsoft SQL Server Rapor Oluşturucusu kullanır. Configuration Manager konsolunda bir rapor oluşturur veya düzenlerseniz Rapor Oluşturucusu açılır. Bir raporu ilk kez oluşturduğunuzda veya değiştirirken, Rapor Oluşturucusu otomatik olarak yüklenir. Raporları çalıştırdığınızda veya düzenlediğinizde, SQL Server yüklü sürümüyle ilişkili Rapor Oluşturucu sürümü açılır.  

 Rapor Oluşturucu yüklemesi, 20'den fazla dil için destek getirir. Rapor Oluşturucusu çalıştırdığınızda, verileri yerel bilgisayarın işletim sisteminin dilinde görüntüler. Rapor Oluşturucusu dili desteklemiyorsa, verileri Ingilizce olarak görüntüler. Rapor Oluşturucusu, aşağıdaki özellikleri içeren SQL Server Reporting Services tam yeteneklerini destekler:

- Microsoft 365 uygulamalarına benzer bir görünümle, sezgisel bir rapor yazma ortamı sunar.  

- SQL Server rapor tanım dili 'nin (RDL) esnek rapor yerleşimini sunar.  

- Tablolar ve göstergeleri içeren çeşitli veri görselleştirme biçimleri sağlar.  

- Zengin biçimli metin kutuları sağlar  

- Microsoft Word biçiminde dışa aktarır.  

Ayrıca, doğrudan SQL Server Reporting Services Rapor Oluşturucusu de açabilirsiniz.

## <a name="report-models-in-sql-server-reporting-services"></a>SQL Server Raporlama Hizmetleri'nde rapor modelleri

SQL Raporlama Hizmetleri, model tabanlı raporlara dahil etmek üzere Configuration Manager veritabanından öğe seçmenize yardımcı olmak için rapor modelleri kullanır. Rapor oluşturduğunuzda, rapor modelleri yalnızca belirtilen görünümleri ve aralarından seçim yapılacak öğeleri sunar. Model tabanlı raporlar oluşturmak için, en az bir rapor modelinin kullanılabilir olması gerekir.

Rapor modellerinin aşağıdaki özellikleri vardır:

- Veritabanı alanları ve görünümlerine mantıksal iş adları verin. Rapor oluşturmak için Configuration Manager veritabanı yapısı hakkında bilgi sahibi olmanız gerekmez.

- Öğeleri mantıksal olarak gruplandırın.  

- Öğeler arasındaki ilişkileri tanımlayın.  

- Yönetici kullanıcıların yalnızca görme iznine sahip oldukları verileri görebilmesi için güvenli model öğeleri.

Configuration Manager, örnek rapor modelleri sunmakla birlikte, kendi iş gereksinimlerinizi karşılayacak rapor modelleri de tanımlayabilirsiniz. Rapor modelleri oluşturma hakkında daha fazla bilgi için bkz. [özel rapor modelleri oluşturma](creating-custom-report-models-in-sql-server-reporting-services.md).

## <a name="next-steps"></a>Sonraki adımlar

[Raporlama planı](planning-for-reporting.md)