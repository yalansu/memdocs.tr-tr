---
title: Özel raporlar oluşturma
titleSuffix: Configuration Manager
description: İş gereksinimlerinizi karşılayacak rapor modelleri tanımlayın ve ardından Configuration Manager için rapor modellerini dağıtın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: fe570eeedc2c050bdaf27903d30ddffff63109d9
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879157"
---
# <a name="creating-custom-report-models-for-configuration-manager-in-sql-server-reporting-services"></a>SQL Server Reporting Services Configuration Manager için özel rapor modelleri oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Örnek rapor modelleri Configuration Manager eklenmiştir, ancak kendi iş gereksinimlerinizi karşılayacak rapor modelleri tanımlayabilir ve ardından yeni model tabanlı raporlar oluştururken kullanılacak Configuration Manager Rapor modelini dağıtabilirsiniz. Aşağıda yer alan tablolar temel bir rapor modelini oluşturma ve dağıtmaya yönelik adımları sağlar.  

> [!NOTE]  
>  Daha gelişmiş bir rapor modeli oluşturmaya yönelik adımlar için bu konuda [Steps for Creating an Advanced Report Model in SQL Server Reporting Services](#AdvancedReportModel) bölümüne bakın.  

|Adım|Açıklama|Daha fazla bilgi|  
|----------|-----------------|----------------------|  
|SQL Server Business Intelligence Development Studio uygulamasının yüklü olduğunun doğrulanması|Rapor modelleri, SQL Server Business Intelligence Development Studio kullanılarak tasarlanır ve yapılır. SQL Server Business Intelligence Development Studio uygulamasının özel rapor modelini oluşturduğunuz bilgisayarda yüklü olduğunu doğrulayın.|SQL Server Business Intelligence Development Studio hakkında daha fazla bilgi için, SQL Server 2008 belgelerine bakın.|  
|Bir rapor modeli projesi oluşturma|Bir rapor modeli projesi veri kaynağı tanımını (bir .ds dosyası) bir veri kaynağı görünümü tanımını (bir .dsv dosyası) ve rapor modelini (bir .smdl dosyası) içerir.|Daha fazla bilgi için bu konunun [To create the report model project](#BKMK_CreateReportModelProject) bölümüne bakın.|  
|Bir rapor modeli için veri kaynağı tanımlama|Bir rapor modeli projesi oluşturduktan sonra, iş verilerini çıkaracağınız bir veri kaynağı tanımlamalısınız. Genellikle, bu Configuration Manager site veritabanıdır.|Daha fazla bilgi için bu konunun [To define the data source for the report model](#BKMK_DefineReportModelDataSource) bölümüne bakın.|  
|Bir rapor modeli için veri kaynağı görünümü tanımlama|Rapor modeli projenizde kullanacağınız veri kaynaklarını tanımladıktan sonraki adım, proje için bir veri kaynağı görünümü tanımlamaktır. Veri kaynağı görünümü, bir veya daha çok veri kaynağını temel alan bir mantık verisidir. Veri kaynağı görünümümleri, tablolar ve görünümler gibi altta yatan veri kaynaklarında bulunan fiziksel nesnelere erişimi kapsarlar. SQL Server Raporlama Hizmetleri veri kaynağı görünümünden rapor modeli oluşturur.<br /><br /> Veri kaynağı görünümleri, belirlediğiniz verilerin kullanışlı bir temsilini sağlayarak tasarım sürecini modellemenizi kolaylaştırırlar. Altta yatan veri kaynağını değiştirmeden tabloları ve alanları yeniden adlandırabilir ve alanları ve türetilen tabloları bir veri kaynağı görünümünde toplayabilirsiniz. Verimli bir model için yalnızca kullanmayı amaçladığınız tabloları veri kaynağı görünümüne ekleyin.|Daha fazla bilgi için bu konunun [To define the data source view for the report model](#BKMK_DefineReportModelDataSourceView) bölümüne bakın.|  
|Bir rapor modeli oluşturma|Bir rapor modeli, ticari kuruluşları, alanları ve rolleri tanımlayan bir veritabanını en üst katmanıdır. Yayımlandıklarında, Rapor Oluşturucu kullanıcıları bu modelleri kullanarak, veritabanı yapılarını bilmeleri veya anlamaları ve sorgular yazmaları gerekmeden raporları geliştirebilirler. Modeller, bu iş öğeleri arasında önceden tanımlı ilişkiler ve önceden tanımlı hesaplamalarla, kolay bir ad altında gruplanan ilgili rapor öğesi kümelerinden oluşurlar. Modeller, Semantik Model Tanım Dili (SMDL) adı verilen bir XML dili kullanılarak tanımlanırlar. Rapor modeli dosyalarının dosya uzantısı .smdl'dir.|Daha fazla bilgi için bu konunun [To create the report model](#BKMK_CreateReportModel) bölümüne bakın.|  
|Bir rapor modeli yayımlama|Henüz oluşturduğunuz modeli kullanarak bir rapor hazırlamak için, onu bir rapor sunucusuna yayımlamalısınız. Veri kaynağı ve veri kaynağı görünümü yayımlandığında modele dahil edilir.|Daha fazla bilgi için bu konunun [To publish the report model for use in SQL Server Reporting Services](#BKMK_PublishReportModel) bölümüne bakın.|  
|Configuration Manager için rapor modelini dağıtın|Model tabanlı bir rapor oluşturmak üzere **rapor oluşturma sihirbazında** özel bir rapor modeli kullanabilmeniz için, rapor modelini Configuration Manager dağıtmanız gerekir.|Daha fazla bilgi için bu konunun [To deploy the custom report model to Configuration Manager](#BKMK_DeployReportModel) bölümüne bakın.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>SQL Server Reporting Services’de temel rapor modeli oluşturma adımları  
 Sitenizdeki kullanıcıların, Configuration Manager veritabanının tek bir görünümündeki verileri temel alan belirli model tabanlı raporları oluşturmak için kullanabileceği temel bir rapor modeli oluşturmak için aşağıdaki yordamları kullanabilirsiniz. Sitenizde rapor yazarına istemci bilgisayarlar hakkındaki bilgileri sunan bir rapor modeli oluşturursunuz. Bu bilgiler, Configuration Manager veritabanındaki **v_R_System** görünümünden alınır.  

 Bu yordamları uyguladığınız bilgisayarda SQL Server Business Intelligence Development Studio uygulamasının yüklü olduğundan ve bilgisayarın raporlama hizmetleri nokta sunucusuna ağ bağlantısı bulunduğundan emin olun. SQL Server Business Intelligence Development Studio hakkında ayrıntılı bilgi için, SQL Server 2008 belgelerine bakın.  

###  <a name="to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a>Rapor modeli projesi oluşturmak için  

1.  Masaüstünde **Başlat**'a tıklayıp, **Microsoft SQL Server 2008**öğesine tıklayın ve ardından **SQL Server Business Intelligence Development Studio**öğesine tıklayın.  

2.  **SQL Server Business Intelligence Development Studio** Microsoft Visual Studio uygulamasında açıldıktan sonra **Dosya**, **Yeni**öğelerine tıklayıp, ardından **Proje**öğesine tıklayın.  

3.  **Yeni Proje** iletişim kutusunda **Şablonlar** listesinde **Rapor Modeli Projesi** öğesini seçin.  

4.  **Ad** kutusunda bu rapor modeli için bir ad belirleyin. Bu örnekte, **Simple_Model**yazın.  

5.  Rapor modeli projesi oluşturmak için **Tamam**'a tıklayın.  

6.  **Simple_Model** çözümü **Solution Explorer**bölmesinde görüntülenir.  

    > [!NOTE]  
    >  **Çözüm Gezgini** bölmesini göremiyorsanız, **Görünüm**'ü ve sonra **Çözüm Gezgini**'ne tıklayın.  

###  <a name="to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a>Rapor modeli için veri kaynağını tanımlamak için  

1.  **SQL Server Business Intelligence Development Studio** 'nun **Çözüm Gezgini**bölmesinde, **Veri Kaynakları** 'na sağ tıklayıp **Yeni Veri Kaynağı Ekle**'yi seçin.  

2.  **Veri Kaynağı Sihirbazına Hoş Geldiniz** sayfasında **İleri**'ye tıklayın.  

3.  **Bağlantının nasıl tanımlanacağını seçin** sayfasında, **Mevcut veya yeni bir bağlantıya dayalı bir veri kaynağı oluştur** 'un seçili olduğunu doğrulayın ve **Yeni**'ye tıklayın.  

4.  **Bağlantı Yöneticisi** iletişim kutusunda veri kaynağı için aşağıdaki bağlantı özelliklerini belirleyin:  

    -   **Sunucu adı**: Configuration Manager site veritabanı sunucunuzun adını yazın veya listeden seçin. Varsayılan örnek yerine adlandırılmış bir örnekle çalışıyorsanız, &lt;> *veritabanı sunucusu* > \\ &lt; *örnek adı* yazın.  

    -   **Windows Kimlik Doğrulaması Kullan**'ı seçin.  

    -   **Bir veritabanı adı seçin veya girin** listesinde, Configuration Manager site veritabanınızın adını seçin.  

5.  Veritabanı bağlantısını doğrulamak için **Bağlantıyı Test Et**öğesine tıklayın.  

6.  Bağlantı başarılı olursa, **Bağlantı Yöneticisi** iletişim kutusunu kapatmak için **Tamam** 'a tıklayın. Bağlantı başarılı olmazsa, girdiğiniz bilgilerin doğru olup olmadıklarını kontrol ettikten sonra **Bağlantıyı Test Et** öğesine yeniden tıklayın.  

7.  **Bağlantının nasıl tanımlanacağını seçin** sayfasında, **Mevcut veya yeni bir bağlantı ile veri kaynağı oluştur** seçeneğini seçili olduğundan emin olup, henüz belirlediğiniz veri kaynağının **Veri bağlantıları**listesinde seçili olduğunu doğrulayın ve ardından **İleri**'ye tıklayın.  

8.  **Veri kaynağı adı**' nda, veri kaynağı için bir ad belirtin ve ardından **son**' a tıklayın. Bu örnekte, **Simple_Model**yazın.  

9. **Simple_Model.ds** veri kaynağı artık **Veri Kaynakları** düğümünde **Solution Explorer** altında görüntülenir.  

    > [!NOTE]  
    >  Mevcut bir veri kaynağının özelliklerini düzenlemek için, **Çözüm Gezgini** bölmesinin **Veri Kaynakları** klasöründe veri kaynağına çift tıklayarak Veri Kaynağı Tasarımcısı'nda veri kaynağı özelliklerini görüntüleyin.  

###  <a name="to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a> To define the data source view for the report model  

1.  **Çözüm Gezgini**'nde, **Veri Kaynağı Görünümleri** 'ne sağ tıklayarak **Yeni Veri Kaynağı Görünümü Ekle**'yi seçin.  

2.  **Veri Kaynağı Görünümü Sihirbazına Hoş Geldiniz** sayfasında **İleri**'ye tıklayın. **Bir Veri Kaynağı Seç** sayfası görüntülenir.  

3.  **İlişkili veri kaynakları** penceresinde **Simple_Model** veri kaynağının seçili olduğunu doğrulayıp, ardından **İleri**'ye tıklayın.  

4.  **Tabloları ve Görünümleri Seç** sayfasında **Kullanılabilir nesneler** listesinde rapor modelinde kullanılacak şu görünümü seçin: **v_R_System (dbo)**.  

    > [!TIP]  
    >  **Kullanılabilir nesneler** listesinde görünümleri bulmayı kolaylaştırmak için, listenin başındaki **Ad** başlığına tıklayarak nesneleri alfabetik olarak sıralayın.  

5.  Görünümü seçtikten sonra, **>** nesneyi **dahil edilen nesneler** listesine aktarmak için öğesine tıklayın.  

6.  **Ad Eşleştirme** sayfası görüntülenirse, varsayılan seçimleri kabul edip, **İleri**'ye tıklayın.  

7.  Gerek duyduğunuz nesneleri seçtikten sonra, **İleri**'ye tıklayıp, ardından veri kaynağı görünümü için bir ad belirleyin. Bu örnekte, **Simple_Model**yazın.  

8.  **Son**'a tıklayın. **Simple_Model.dsv** veri kaynağı görünümü **Solution Explorer** bölmesinin **Veri Kaynağı Görünümleri**klasöründe görüntülenir.  

###  <a name="to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a>Rapor modeli oluşturmak için  

1.  **Çözüm Gezgini**'nde, **Rapor Modelleri** 'ne sağ tıklayıp **Yeni Rapor Modeli Ekle**'yi seçin.  

2.  **Rapor Modeli Sihirbazına Hoş Geldiniz** sayfasında **İleri**'ye tıklayın.  

3.  **Veri Kaynağı Görünümlerini Seç** sayfasında **Kullanılabilen veri kaynağı görünümleri** listesinde veri kaynağı görünümünü seçip, ardından **İleri**'ye tıklayın. Bu örnekte, **Simple_Model.dsv**'yi seçin.  

4.  **Rapor modeli oluşturma kurallarını seç** sayfasında varsayılan değerleri kabul edip, ardından **İleri**'ye tıklayın.  

5.  **Model İstatistiklerini Topla** sayfasında **Oluşturmadan önce model istatistiklerini güncelle** seçeneğinin seçili olduğundan emin olup, **İleri**'ye tıklayın.  

6.  **Sihirbazı Tamamlama** sayfasında rapor modeli için bir ad belirleyin. Bu örnek için **Simple_Model** öğesinin görüntülendiğinden emin olun.  

7.  Sihirbazı tamamlamak ve rapor modelini oluşturmak için **Çalıştır**öğesine tıklayın.  

8.  Sihirbazdan çıkmak için, **Bitir**'e tıklayın. Rapor modeli Tasarım penceresinde görüntülenir.  

###  <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> To publish the report model for use in SQL Server Reporting Services  

1.  **Solution Explorer**bölmesinde **Dağıt**öğesini seçmek için rapor modelini farenin sağ düğmesiyle tıklayın. Bu örnekte rapor modeli, **Simple_Model.smdl**adlı rapor modelidir.  

2.  **SQL Server Business Intelligence Development Studio** penceresinin sol alt köşesindeki dağıtım durumunu inceleyin. Dağıtım tamamlandığında, **Dağıtma İşlemi Başarılı** görüntülenir. Dağıtım başarısız olursa, başarısızlığın nedeni **Çıktı** penceresinde görüntülenir. Yeni rapor modeli şimdi SQL Server Raporlama Hizmetleri web sitenizde kullanılabilir.  

3.  **Dosya**, **Tümünü Kaydet**öğelerine tıklayın ve ardından **SQL Server Business Intelligence Development Studio**uygulamasını kapatın.  

###  <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a>Özel rapor modelini Configuration Manager dağıtmak için  

1. Rapor modeli projesini oluşturduğunuz klasörü bulun. Örneğin,%*USERPROFILE*% \ Studio 2008 \ Projects \\ * &lt; Proje adı \> .*  

2. Aşağıdaki dosyaları rapor modeli proje klasöründen bilgisayarınızda bir geçici klasöre kopyalayın.  

   -   * &lt; Model adı \> * **. dsv**  

   -   * &lt; Model adı \> * **. smdl**  

3. Not Defteri gibi bir metin düzenleyici kullanarak yukarıdaki dosyaları açın.  

4. Dosya _ &lt; modeli adı \> _**. dsv**'de, dosyanın ilk satırını bulun ve aşağıdaki gibi okur:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Bu satırı aşağıdaki gibi görünecek şekilde düzenleyin:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`  

5. Dosyanın tüm içeriğini Windows Panosuna kopyalayın.  

6. Dosya _ &lt; modeli adı \> _**. dsv**dosyasını kapatın.  

7. _ &lt; Ad \> _**. smdl**dosya modelinde, dosyanın aşağıdaki gibi görünen son üç satırını bulun:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Dosya _ &lt; modeli adı \> _**. dsv** içeriğini dosyanın son satırından (** &lt; SemanticModel \> **) doğrudan yapıştırın.  

9. Dosya _ &lt; modeli adı \> _**. smdl**dosyasını kaydedin ve kapatın.  

10. **. Smdl** dosya _ &lt; modeli \> adını_Configuration Manager site sunucusundaki *% ProgramFiles%* \Microsoft Configuration Manager \adminconsole\xmlstorage\other klasörüne kopyalayın.  

    > [!IMPORTANT]  
    >  Rapor modeli dosyasını Configuration Manager site sunucusuna kopyaladıktan sonra, rapor **oluşturma Sihirbazı**' nda rapor modelini kullanabilmeniz için Configuration Manager konsolundan çıkmanız ve yeniden başlatmanız gerekir.  

##  <a name="steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> Steps for Creating an Advanced Report Model in SQL Server Reporting Services  
 Sitenizdeki kullanıcıların, Configuration Manager veritabanının birden çok görünümündeki verileri temel alan belirli model tabanlı raporları oluşturmak için kullanabileceği gelişmiş bir rapor modeli oluşturmak için aşağıdaki yordamları kullanabilirsiniz. İstemci bilgisayarlar ve bu bilgisayarlarda yüklü işletim sistemi hakkında rapor yazarına bilgiler sunan bir rapor modeli oluşturursunuz. Bu bilgiler Configuration Manager veritabanında aşağıdaki görünümlerden alınmıştır:  

- **V_R_System**: bulunan bilgisayarlar ve Configuration Manager istemcisiyle ilgili bilgiler içerir.  

- **V_GS_OPERATING_SYSTEM**: İstemci bilgisayarda yüklü olan işletim sistemiyle ilgili bilgi içerir.  

  Önceki görünümlerde seçilen öğeler tek listede birleştirilir, bunlara kolay adlar verilir ve belirli raporlara eklenmek üzere Rapor Oluşturucu'da rapor yazana sunulur.  

  Bu yordamları uyguladığınız bilgisayarda SQL Server Business Intelligence Development Studio uygulamasının yüklü olduğundan ve bilgisayarın raporlama hizmetleri nokta sunucusuna ağ bağlantısı bulunduğundan emin olun. SQL Server Business Intelligence Development Studio hakkında ayrıntılı bilgi için, SQL Server belgelerine bakın.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  Masaüstünde **Başlat**'a tıklayıp, **Microsoft SQL Server 2008**öğesine tıklayın ve ardından **SQL Server Business Intelligence Development Studio**öğesine tıklayın.  

2.  **SQL Server Business Intelligence Development Studio** Microsoft Visual Studio uygulamasında açıldıktan sonra **Dosya**, **Yeni**öğelerine tıklayıp, ardından **Proje**öğesine tıklayın.  

3.  **Yeni Proje** iletişim kutusunda **Şablonlar** listesinde **Rapor Modeli Projesi** öğesini seçin.  

4.  **Ad** kutusunda bu rapor modeli için bir ad belirleyin. Bu örnekte, **Advanced_Model**yazın.  

5.  Rapor modeli projesi oluşturmak için **Tamam**'a tıklayın.  

6.  **Çözüm Gezgini** 'nde **Advanced_Model**çözümü görüntülenir.  

    > [!NOTE]  
    >  **Çözüm Gezgini** bölmesini göremiyorsanız, **Görünüm**'ü ve sonra **Çözüm Gezgini**'ne tıklayın.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>To define the data source for the report model  

1.  **SQL Server Business Intelligence Development Studio** 'nun **Çözüm Gezgini**bölmesinde, **Veri Kaynakları** 'na sağ tıklayıp **Yeni Veri Kaynağı Ekle**'yi seçin.  

2.  **Veri Kaynağı Sihirbazına Hoş Geldiniz** sayfasında **İleri**'ye tıklayın.  

3.  **Bağlantının nasıl tanımlanacağını seçin** sayfasında, **Mevcut veya yeni bir bağlantıya dayalı bir veri kaynağı oluştur** 'un seçili olduğunu doğrulayın ve **Yeni**'ye tıklayın.  

4.  **Bağlantı Yöneticisi** iletişim kutusunda veri kaynağı için aşağıdaki bağlantı özelliklerini belirleyin:  

    -   **Sunucu adı**: Configuration Manager site veritabanı sunucunuzun adını yazın veya listeden seçin. Varsayılan örnek yerine adlandırılmış bir örnekle çalışıyorsanız, &lt;> *veritabanı sunucusu* > \\ &lt; *örnek adı* yazın.  

    -   **Windows Kimlik Doğrulaması Kullan**'ı seçin.  

    -   **Bir veritabanı adı seçin veya girin** listesinde, Configuration Manager site veritabanınızın adını seçin.  

5.  Veritabanı bağlantısını doğrulamak için **Bağlantıyı Test Et**öğesine tıklayın.  

6.  Bağlantı başarılı olursa, **Bağlantı Yöneticisi** iletişim kutusunu kapatmak için **Tamam** 'a tıklayın. Bağlantı başarılı olmazsa, girdiğiniz bilgilerin doğru olup olmadıklarını kontrol ettikten sonra **Bağlantıyı Test Et** öğesine yeniden tıklayın.  

7.  **Bağlantının nasıl tanımlanacağını seçin** sayfasında, **Mevcut veya yeni bir bağlantıya dayalı bir veri kaynağı oluştur** 'un seçili olduğunu doğrulayın, yeni belirttiğiniz veri kaynağının **Veri bağlantıları** liste kutusunda seçili olduğunu doğrulayın ve **İleri**'ye tıklayın.  

8.  **Veri kaynağı adı**'nda, veri kaynağı için bir ad belirtin ve **Son**'a tıklayın. Bu örnekte, **Advanced_Model**yazın.  

9. **Advanced_Model.ds** veri kaynağı, **Veri Kaynakları** düğümü altında **Çözüm Gezgini** 'nde görüntülenir.  

    > [!NOTE]  
    >  Mevcut bir veri kaynağının özelliklerini düzenlemek için, **Çözüm Gezgini** bölmesinin **Veri Kaynakları** klasöründe veri kaynağına çift tıklayarak Veri Kaynağı Tasarımcısı'nda veri kaynağı özelliklerini görüntüleyin.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>To define the data source view for the report model  

1. **Çözüm Gezgini**'nde, **Veri Kaynağı Görünümleri** 'ne sağ tıklayarak **Yeni Veri Kaynağı Görünümü Ekle**'yi seçin.  

2. **Veri Kaynağı Görünümü Sihirbazına Hoş Geldiniz** sayfasında **İleri**'ye tıklayın. **Bir Veri Kaynağı Seç** sayfası görüntülenir.  

3. **İlişkisel veri kaynakları** penceresinde, **Advanced_Model** veri kaynağının seçili olduğunu doğrulayın ve **İleri**'ye tıklayın.  

4. **Tabloları ve Görünümleri Seç** sayfasında, rapor modelinde kullanılmak üzere **Kullanılabilir nesneler** listesinden aşağıdaki görünümleri seçin:  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     Her görünümü seçtikten sonra, **>** nesneyi **dahil edilen nesneler** listesine aktarmak için öğesine tıklayın.  

   > [!TIP]  
   >  **Kullanılabilir nesneler** listesinde görünümleri bulmayı kolaylaştırmak için, listenin başındaki **Ad** başlığına tıklayarak nesneleri alfabetik olarak sıralayın.  

5. **Ad Eşleştirme** iletişim kutusu görüntülenirse, varsayılan seçimleri kabul edip **İleri**'ye tıklayın.  

6. Gereken nesneleri seçtikten sonra, **İleri**'ye tıklayın ve veri kaynağı görünümü için bir ad belirtin. Bu örnekte, **Advanced_Model**yazın.  

7. **Son**'a tıklayın. **Advanced_Model.dsv** vergi kaynağı görünümü **Çözüm Gezgini** 'nin **Veri Kaynağı Görünümleri**klasöründe görüntülenir.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Veri kaynağı görünümünde ilişkileri tanımlamak için  

1.  **Çözüm Gezgini**'nde, **Advanced_Model.dsv** 'ye çift tıklayarak Tasarım penceresini açın.  

2.  **v_R_System** penceresinin başlık çubuğuna sağ tıklayıp **Tabloyu Değiştir**'i seçin ve sonra **Yeni Bir Adlandırılmış Sorguyla**'ya tıklayın.  

3.  **Adlandırılmış Sorgu Oluştur** iletişim kutusunda, **Tablo Ekle** simgesine tıklayın (genellikle şeritteki son simgedir).  

4.  **Tablo Ekle** iletişim kutusunda, **Görünümler** sekmesine tıklayın, listeden **V_GS_OPERATING_SYSTEM** 'i seçip **Ekle**'ye tıklayın.  

5.  **Kapat** 'a tıklayarak **Tablo Ekle** iletişim kutusunu kapatın.  

6.  **Adlandırılmış Sorgu Oluştur** iletişim kutusunda, aşağıdaki bilgileri belirtin:  

    -   **Ad:** Sorgunun adını belirtin. Bu örnekte, **Advanced_Model**yazın.  

    -   **Açıklama:** Sorgu için bir açıklama belirtin. Bu örnek için, **Örnek Raporlama Hizmetleri rapor modeli**yazın.  

7.  **v_R_System** penceresinde, nesneler listesinden rapor modelinde görüntülemek üzere aşağıdaki öğeleri seçin:  

    -   **RESOURCEID**  

    -   **Kaynak**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  **v_GS_OPERATING_SYSTEM** kutusunda, nesneler listesinden rapor modelinde görüntülemek üzere aşağıdaki öğeleri seçin:  

    -   **RESOURCEID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Bu görünümlerdeki nesneleri rapor yazarına tek liste halinde sunmak için, bir birleşim kullanarak iki tablo veya görünüm arasında bir ilişki belirtmeniz gerekir. Her iki görünümde de görünen **ResourceID**nesnesini kullanarak iki görünümü birleştirebilirsiniz.  

10. **v_R_System** penceresinde, **ResourceID** nesnesine tıklayıp tutun ve **v_GS_OPERATING_SYSTEM** penceresindeki **ResourceID** nesnesine sürükleyin.  

11. Tamam ' a tıklayın **.**  

12. **Advanced_Model** penceresi **v_R_System** penceresinin yerini alır ve **v_R_System** ve **v_GS_OPERATING_SYSTEM** görünümlerindeki rapor modeli için gereken tüm nesneleri içerir. Şimdi Veri Kaynağı Görünümü Tasarımcısı'ndan **v_GS_OPERATING_SYSTEM** penceresini silebilirsiniz . **v_GS_OPERATING_SYSTEM** penceresinin başlık çubuğuna sağ tıklayıp **Tabloyu DSV'den Sil**'i seçin. **Nesne Sil** iletişim kutusunda, silmeyi onaylamak için **Tamam** 'a tıklayın.  

13. **Dosya**'yı ve sonra **Tümünü Kaydet**'e tıklayın.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  **Çözüm Gezgini**'nde, **Rapor Modelleri** 'ne sağ tıklayıp **Yeni Rapor Modeli Ekle**'yi seçin.  

2.  **Rapor Modeli Sihirbazına Hoş Geldiniz** sayfasında **İleri**'ye tıklayın.  

3.  **Veri Kaynağı Görünümü Seç** sayfasında, **Kullanılabilir veri kaynağı görünümleri** listesinden veri kaynağı görünümünü seçin ve **İleri**'ye tıklayın. Bu örnekte, **Simple_Model.dsv**'yi seçin.  

4.  **Rapor modeli oluşturma kuralları seçin** sayfasında, varsayılan değerleri değiştirmeyin ve **İleri**'ye tıklayın.  

5.  **Model İstatistiklerini Topla** sayfasında **Oluşturmadan önce model istatistiklerini güncelle** seçeneğinin seçili olduğundan emin olup, **İleri**'ye tıklayın.  

6.  **Sihirbazı Tamamlama** sayfasında rapor modeli için bir ad belirleyin. Bu örnekte, **Advanced_Model** göründüğünü doğrulayın.  

7.  Sihirbazı tamamlamak ve rapor modelini oluşturmak için **Çalıştır**öğesine tıklayın.  

8.  Sihirbazdan çıkmak için, **Bitir**'e tıklayın.  

9. Rapor modeli Tasarım penceresinde görüntülenir.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Rapor modelindeki nesne adlarını değiştirmek için  

1.  **Çözüm Gezgini**'nde, bir rapor modeline sağ tıklayıp **Görünüm Tasarımcısı**'nı seçin. Bu örnekte, **Advanced_Model.smdl**'yi seçin.  

2.  Rapor modeli Tasarım görünümünde, herhangi bir nesne adına tıklayıp **Yeniden Adlandır**'ı seçin.  

3.  Seçili nesne için yeni bir ad yazıp Enter tuşuna basın. Örneğin, **CSD_Version_0** nesnesini **Windows Hizmet Paketi Sürümü**olarak yeniden adlandırabilirsiniz.  

4.  Nesneleri yeniden adlandırmanız bittiğinde **Dosya**'ya ve sonra **Tümünü Kaydet**'e tıklayın.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>To publish the report model for use in SQL Server Reporting Services  

1.  **Çözüm Gezgini**'nde, **Advanced_Model.smdl** 'ye sağ tıklayarak **Dağıt**'ı seçin.  

2.  **SQL Server Business Intelligence Development Studio** penceresinin sol alt köşesindeki dağıtım durumunu inceleyin. Dağıtım tamamlandığında, **Dağıtma İşlemi Başarılı** görüntülenir. Dağıtım başarısız olursa, başarısızlığın nedeni **Çıktı** penceresinde görüntülenir. Yeni rapor modeli şimdi SQL Server Raporlama Hizmetleri web sitenizde kullanılabilir.  

3.  **Dosya**, **Tümünü Kaydet**öğelerine tıklayın ve ardından **SQL Server Business Intelligence Development Studio**uygulamasını kapatın.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1. Rapor modeli projesini oluşturduğunuz klasörü bulun. Örneğin,%*USERPROFILE*% \ Studio 2008 \ Projects \\ * &lt; Proje adı \> .*  

2. Aşağıdaki dosyaları rapor modeli proje klasöründen bilgisayarınızda bir geçici klasöre kopyalayın.  

   -   * &lt; Model adı \> * **. dsv**  

   -   * &lt; Model adı \> * **. smdl**  

3. Not Defteri gibi bir metin düzenleyici kullanarak yukarıdaki dosyaları açın.  

4. Dosya _ &lt; modeli adı \> _**. dsv**'de, dosyanın ilk satırını bulun ve aşağıdaki gibi okur:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Bu satırı aşağıdaki gibi görünecek şekilde düzenleyin:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`

5. Dosyanın tüm içeriğini Windows Panosuna kopyalayın.  

6. Dosya _ &lt; modeli adı \> _**. dsv**dosyasını kapatın.  

7. _ &lt; Ad \> _**. smdl**dosya modelinde, dosyanın aşağıdaki gibi görünen son üç satırını bulun:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Dosya _ &lt; modeli adı \> _**. dsv** içeriğini dosyanın son satırından (** &lt; SemanticModel \> **) doğrudan yapıştırın.  

9. Dosya _ &lt; modeli adı \> _**. smdl**dosyasını kaydedin ve kapatın.  

10. _ &lt; Ad \> _**. smdl** dosya modelini Configuration Manager site sunucusundaki *% ProgramFiles%* \Microsoft Endpoint manager\adminconsole\xmlstorage\other klasörüne kopyalayın.  

    > [!IMPORTANT]  
    >  Rapor modeli dosyasını Configuration Manager site sunucusuna kopyaladıktan sonra, rapor **oluşturma Sihirbazı**' nda rapor modelini kullanabilmeniz için Configuration Manager konsolundan çıkmanız ve yeniden başlatmanız gerekir.  
