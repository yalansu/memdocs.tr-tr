---
title: Mac bilgisayar uygulamaları oluşturma
titleSuffix: Configuration Manager
description: Mac bilgisayarlara yönelik uygulamalar oluştururken ve dağıtırken dikkate almanız gereken önemli noktalar bölümüne bakın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3b734dc6149c1613d986205577b46160d363d31d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075797"
---
# <a name="create-mac-computer-applications-with-configuration-manager"></a>Configuration Manager ile Mac bilgisayar uygulamaları oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Mac bilgisayarlara yönelik uygulamalar oluştururken ve dağıtırken aşağıdaki noktaları göz önünde bulundurun.  

> [!IMPORTANT]  
>  Bu konudaki yordamlar, Configuration Manager istemcisini yüklediğiniz Mac bilgisayarlara uygulama dağıtma hakkındaki bilgileri kapsar. Microsoft Intune ile kaydettiğiniz Mac bilgisayarlar uygulama dağıtımını desteklemez.  

## <a name="general-considerations"></a>Dikkat edilmesi gereken temel noktalar  
 Configuration Manager, Configuration Manager Mac istemcisini çalıştıran Mac bilgisayarlara uygulama dağıtmak için kullanabilirsiniz. Mac bilgisayarlara yazılım dağıtma adımları, yazılımı Windows bilgisayarlarına dağıtmaya yönelik adımlara benzer. Ancak, Configuration Manager tarafından yönetilen Mac bilgisayarlara yönelik uygulamalar oluşturup dağıtmadan önce şunları göz önünde bulundurun:  

-   Mac uygulama paketlerini Mac bilgisayarlara dağıtabilmeniz için önce bir Mac bilgisayarında **CMAppUtil** aracını kullanarak bu uygulamaları Configuration Manager tarafından okunabilen bir biçime dönüştürmeniz gerekir.  

-   Configuration Manager, Mac uygulamalarının kullanıcılara dağıtımını desteklemez. Bunun yerine, bu dağıtımların bir cihaza yapılması gerekir. Benzer şekilde, Mac Uygulama dağıtımları için Configuration Manager, yazılım **Dağıtma Sihirbazı**'Nın **dağıtım ayarları** sayfasında **kullanıcının birincil cihazına yazılım ön dağıtımı** seçeneğini desteklemez.  

-   Mac uygulamaları sanal dağıtımları destekler.  

-   Mac bilgisayarlara amacı **Kullanılabilir**olan uygulamalar dağıtamazsınız.  

-   Yazılım dağıtırken uyandırma paketleri gönderme seçeneği Mac bilgisayarlarda desteklenmez.  

-   Mac bilgisayarlar, uygulama içeriğini indirmek için Arka Plan Akıllı Aktarım Hizmeti (BITS) desteklemez. Bir uygulamanın indirilmesi başarısız olursa, baştan başlatılır.  

-   Configuration Manager, Mac bilgisayarlar için dağıtım türleri oluştururken genel koşulları desteklemez.  

## <a name="steps-to-create-and-deploy-an-application"></a>Uygulama oluşturma ve dağıtma adımları  
 Aşağıdaki tabloda, Mac bilgisayarlara yönelik uygulamalar oluşturma ve dağıtma ile ilgili adımlar, Ayrıntılar ve bilgiler sağlanmaktadır.  


|                                         Adım                                          |                                                                                                             Ayrıntılar                                                                                                              |
|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            **1. adım**: Mac uygulamalarını Configuration Manager için hazırlama             | Mac yazılım paketlerinden Configuration Manager uygulamalar oluşturabilmeniz için önce bir Mac bilgisayarında **CMAppUtil** aracını kullanarak Mac yazılımını bir Configuration Manager<strong>. cmmac</strong> dosyasına dönüştürmeniz gerekir. |
| **2. adım**: Mac yazılımını içeren Configuration Manager bir uygulama oluşturma |                                                                       Mac yazılımına yönelik bir uygulama oluşturmak için **uygulama oluşturma Sihirbazı** 'nı kullanın.                                                                       |
|             **3. adım**: Mac uygulaması için dağıtım türü oluşturma              |                                                              Bu adım yalnızca bu bilgileri otomatik olarak uygulamadan içeri aktarmadıysanız gereklidir.                                                               |
|                        **4. adım**: Mac uygulamasını dağıtma                         |                                                                          Uygulamayı Mac bilgisayarlara dağıtmak için **Yazılım Dağıtma Sihirbazı** 'nı kullanın.                                                                          |
|               **5. adım**: Mac uygulamasının dağıtımını izleme               |                                                                                 Mac bilgisayarlara uygulama dağıtımlarının başarısını izleyin.                                                                                 |

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Mac bilgisayarlara yönelik uygulamalar oluşturmak ve dağıtmak için ek yordamlar  
 Configuration Manager tarafından yönetilen Mac bilgisayarlara yönelik uygulamalar oluşturmak ve dağıtmak için aşağıdaki yordamları kullanın.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Adım 1: Configuration Manager için Mac uygulamalarını hazırlama  
 Mac bilgisayarlara Configuration Manager uygulamaları oluşturma ve dağıtma işlemi, Windows bilgisayarları için dağıtım sürecine benzerdir. Ancak, Mac dağıtım türlerini içeren Configuration Manager uygulamalar oluşturmadan önce, **CMAppUtil** aracını kullanarak uygulamaları hazırlamanız gerekir. Bu araç Mac istemcisi yükleme dosyaları ile birlikte indirilir. **CMAppUtil** aracı uygulama hakkında, aşağıdaki Mac paketlerinden gelen verileri algılama dahil bilgiler toplayabilir:  

-   Apple Disk Görüntüsü (.dmg)  

-   Meta Paket Dosyası (.mpkg)  

-   Mac OS X Yükleyici Paketi (.pkg)  

-   Mac OS X Uygulaması (.app)  

Uygulama bilgilerini topladıktan sonra, **CMAppUtil** , uzantısı **.cmmac**olan bir dosya oluşturur. Bu dosya, Mac yazılımına ait yükleme dosyalarını ve uygulamanın zaten yüklü olup olmadığını değerlendirmek için kullanılan algılama yöntemleri ile ilgili bilgileri içerir. **CMAppUtil** , ayrıca, birden çok Mac uygulaması içeren **.dmg** dosyalarını işleyebilir ve her uygulama için farklı bir dağıtım türü oluşturabilir.  

1.  Mac yazılım uygulama paketini Mac bilgisayarında Microsoft İndirme Merkezi’nden indirdiğiniz **macclient.dmg** dosyasının içeriğini ayıkladığınız klasöre kopyalayın.  

2.  Aynı Mac bilgisayarında, bir terminal penceresi açın ve **macclient.dmg** dosyasının içeriğini ayıkladığınız klasöre gidin.  

3.  **Araçlar** klasörüne gidin ve aşağıdaki komut satırı komutunu yazın:  

     **./CMAppUtil** *<özellikler\>*  

     Örneğin, kullanıcının masaüstü klasöründe depolanan **MySoftware. dmg** adlı bir Apple disk görüntü dosyasının içeriğini aynı klasörde bir **cmmac** dosyasına dönüştürmek istediğinizi varsayalım. Ayrıca, disk görüntü dosyasında bulunan tüm uygulamalar için **cmmac** dosyaları oluşturmak istersiniz. Bunu yapmak için aşağıdaki komut satırını kullanın:  

     **./CMApputil –c /Users/** *<Kullanıcı Adı\>* **/Desktop/MySoftware.dmg -o /Users/** *<Kullanıcı Adı\>* **/Desktop -a**  

    > [!NOTE]  
    >  Uygulama adı 128 karakterden uzun olamaz.  

     **CMAppUtil**seçeneklerini yapılandırmak için, aşağıdaki tablonun komut satırı özelliklerini kullanın:  

    |Özellik|Daha fazla bilgi|  
    |--------------|----------------------|  
    |**-h**|Kullanılabilen komut satırı özelliklerini görüntüler.|  
    |**-r**|Verilen **.cmmac** dosyasının **detection.xml** dosyasını **stdout**’a çıkarır. Çıktı, algılama parametrelerini ve **.cmmac** dosyasını oluşturmak için kullanılan **CMAppUtil** sürümünü içerir.|  
    |**-c**|Dönüştürülecek kaynak dosyayı belirtir.|  
    |**-o**|– C özelliği ile birlikte çıkış yolunu belirtir.|  
    |**-a**|, Disk görüntü dosyasındaki tüm uygulamalar ve paketler için – c özelliği ile birlikte. cmmac dosyalarını otomatik olarak oluşturur.|  
    |**-s**|Hiçbir algılama parametresi bulunmazsa **detection.xml** dosyasını oluşturmayı atlar ve **.cmmac** dosyasını **detection.xml** dosyası olmadan oluşturulmaya zorlar.|  
    |**-v**|**CMAppUtil** aracından tanılama bilgileriyle birlikte daha ayrıntılı çıktı görüntüler.|  

4.  **.cmmac** dosyasının belirttiğiniz klasörde oluşturulduğundan emin olun.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Mac yazılımını içeren bir Configuration Manager uygulaması oluşturma  

Configuration Manager tarafından yönetilen Mac bilgisayarlara yönelik bir uygulama oluşturmanıza yardımcı olması için aşağıdaki yordamı kullanın.  

1.  Configuration Manager konsolunda, **yazılım kitaplığı** > **uygulama yönetimi** > **uygulamaları**' nı seçin.  

3.  **Giriş** sekmesinde, **Oluştur** grubunda, **uygulama oluştur**' u seçin.  

4.  **Uygulama oluşturma Sihirbazı**' nın **genel** sayfasında **Bu uygulamayla ilgili bilgileri otomatik olarak yükleme dosyalarından algıla**' yı seçin.  

    > [!NOTE]  
    >  Uygulamayla ilgili bilgileri kendiniz belirtmek istiyorsanız **uygulama bilgilerini el ile belirt**' i seçin. Bilgileri el ile belirtme hakkında daha fazla bilgi için bkz. [Configuration Manager ile uygulama oluşturma](../../apps/deploy-use/create-applications.md).  

5.  **Tür** açılan listesinde, **Mac OS X**'i seçin.  

6.  **Konum** alanında, * \\ \\<Server\> \\<\> \\ \> * UNC yolunu, uygulama bilgilerini algılayacak Mac uygulama yükleme dosyasının (**. cmmac** dosyası)<dosya paylaşımından belirleyin. Alternatif olarak, yükleme dosyası konumuna gitmek ve seçmek için **Araştır** ' ı seçin.  

    > [!NOTE]  
    >  Uygulamayı içeren UNC yoluna erişiminizin olması gerekir.  

7.  **İleri**’yi seçin.  

8.  **Uygulama oluşturma Sihirbazı**'Nın **bilgileri içeri aktar** sayfasında, içeri aktarılan bilgileri gözden geçirin. Gerekirse, geri dönüp hataları düzeltmek için **önceki** seçeneğini belirleyebilirsiniz. Devam etmek için **İleri ' yi** seçin.  

9. **Uygulama oluşturma Sihirbazı**' nın **genel bilgiler** sayfasında uygulama adı, yorumlar, sürüm ve Configuration Manager konsolundaki uygulamaya başvuru yapmanıza yardımcı olacak isteğe bağlı bir başvuru gibi uygulama hakkında bilgi belirtin.  

    > [!NOTE]  
    >  Uygulama bilgileri, uygulama yükleme dosyalarından daha önce elde edilmişse bu sayfada zaten olabilir.  

10. **İleri**' yi seçin, **Özet** sayfasında uygulama bilgilerini gözden geçirin ve ardından **uygulama oluşturma Sihirbazı**' nı doldurun.  

11. Yeni uygulama Configuration Manager konsolunun **uygulamalar** düğümünde görüntülenir.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Adım 3: Mac uygulaması için dağıtım türü oluşturma  
 Configuration Manager tarafından yönetilen Mac bilgisayarlara yönelik dağıtım türü oluşturmanıza yardımcı olması için aşağıdaki yordamı kullanın.  

> [!NOTE]  
>  Uygulama **oluşturma sihirbazında**uygulamayla ilgili bilgileri otomatik olarak içeri aktardıysanız, uygulama için bir dağıtım türü zaten oluşturulmuş olabilir.  

1.  Configuration Manager konsolunda, **yazılım kitaplığı** > **uygulama yönetimi** > **uygulamaları**' nı seçin.  

3.  Bir uygulama seçin. Ardından, **giriş** sekmesinde, **uygulama** grubunda, bu uygulama için yeni bir dağıtım türü oluşturmak için **dağıtım türü oluştur** ' u seçin.  

    > [!NOTE]  
    >  **Dağıtım türü oluşturma Sihirbazı** 'nı **uygulama oluşturma Sihirbazı** 'ndan ve *<uygulama adı\> * **Özellikler** iletişim kutusunun **dağıtım türleri** sekmesinden de başlatabilirsiniz.  

4.  **Dağıtım türü Oluştur sihirbazının** **genel** sayfasında, **tür** açılan listesinde **Mac OS X**' yi seçin.  

5.  **Konum** \\ \\ alanında,<\> \\ Server<UNC yolunu, uygulama yükleme dosyasının (\> \\ **. cmmac** dosyası)\><dosya paylaşımından seçin. Alternatif olarak, yükleme dosyası konumuna gitmek ve seçmek için **Araştır** ' ı seçin.  

    > [!NOTE]  
    >  Uygulamayı içeren UNC yoluna erişiminizin olması gerekir.  

6.  **İleri**’yi seçin.  

7.  **Dağıtım Türü Oluşturma Sihirbazı** 'nın **İçeri Bilgi Aktar**sayfasında, içeri aktarılan bilgileri inceleyin. Gerekirse, geri dönüp hataları düzeltmek için **önceki** ' ni seçin. Devam etmek için **İleri**’yi seçin.  

8.  **Dağıtım Türü Oluşturma Sihirbazı** 'nın **Genel Bilgiler**sayfasında, uygulamayla ilgili uygulama adı, açıklamalar ve dağıtım türünün kullanılabildiği diller gibi bilgileri belirtin.  

    > [!NOTE]  
    >  Uygulama yükleme dosyalarından daha önce elde edilmişse, bazı dağıtım türü bilgileri bu sayfada zaten olabilir.  

9. **İleri**’yi seçin.  

10. **Dağıtım türü oluşturma Sihirbazı**' nın **gereksinimler** sayfasında, dağıtım türünün Mac bilgisayarlara yüklenebilmesi için karşılanması gereken koşulları belirtebilirsiniz.  

11. **Gereksinim Oluştur** iletişim kutusunu açmak için **Ekle** ' yi seçin ve yeni bir gereksinim ekleyin.  

    > [!NOTE]  
    >  Yeni gereksinimleri *<dağıtım türü adı\>* **Özellikler** iletişim kutusunun **Gereksinimler** sekmesinde de ekleyebilirsiniz.  

12. **Kategori** açılan listesinden, bu gereksinimin bir cihaz için olduğunu seçin.  

13. **Koşul** açılan listesinden, Mac bilgisayarın yükleme gereksinimlerini karşılayıp karşılamadığını değerlendirmek için kullanmak istediğiniz koşulu seçin. Bu listenin içeriği, seçtiğiniz kategoriye göre değişir.  

14. **İşleç** açılan listesinden, kullanıcının veya cihazın yükleme gereksinimlerini karşılayıp karşılamadığını değerlendirmek için seçilen koşulu belirtilen değerle karşılaştırmak üzere kullanılacak işleci seçin. Kullanılabilir operatörler, seçilen koşula bağlı olarak farklılık gösterir.  

15. **Değer** alanında, kullanıcının veya cihazın yükleme gereksiniminde karşılayıp karşılamadığını değerlendirmek için seçilen koşul ve işleçle birlikte kullanılacak değerleri belirtin. Kullanılabilir değerler, seçtiğiniz koşula ve işlece bağlı olarak değişir.

16. Gereksinim kuralını kaydetmek ve **Gereksinim Oluştur** iletişim kutusundan çıkmak için **Tamam** ' ı seçin.  

17. **Dağıtım türü oluşturma Sihirbazı**' nın **gereksinimler** sayfasında, **İleri**' yi seçin.  

18. **Dağıtım Türü Oluşturma Sihirbazı** 'nın **Özet**sayfasında, sihirbazın yapacağı işlemleri inceleyin.  Gerekirse, geri dönüp dağıtım türü ayarlarını değiştirmek için **önceki** ' ni seçin. Dağıtım türünü oluşturmak için **İleri ' yi** seçin.  

19. **İlerleme** sayfası tamamlandıktan sonra, yapılan işlemleri gözden geçirin ve ardından **Kapat** ' ı seçerek **dağıtım türü oluşturma Sihirbazı**' nı doldurun.  

20. Bu Sihirbazı **uygulama oluşturma Sihirbazı**' ndan başlattıysanız, **dağıtım türleri** sayfasına dönersiniz.  

###  <a name="deploy-the-mac-application"></a>Mac uygulamasını dağıtma  
 Mac bilgisayarlara uygulama dağıtma adımları, aşağıdaki farklar dışında bir uygulamayı Windows bilgisayarlarına dağıtmaya yönelik adımlarla aynıdır:  

-   Uygulamaların kullanıcılara dağıtılması desteklenmez.  

-   Amacı **Kullanılabilir** olan dağıtımlar desteklenmez.  

-   Yazılım **Dağıtma Sihirbazının** **dağıtım ayarları** sayfasında **kullanıcının birincil cihazına yazılımın ön dağıtımını** yapın seçeneği desteklenmez.  

-   Mac bilgisayarlar Yazılım Merkezi 'ni desteklemediği için **Yazılım Dağıtma Sihirbazının** **Kullanıcı deneyimi** sayfasındaki **Kullanıcı bildirimleri** ayarı yok sayılır.  

-   Yazılım dağıtırken uyandırma paketleri gönderme seçeneği Mac bilgisayarlarda desteklenmez.  

> [!NOTE]  
>  Yalnızca Mac bilgisayarları içeren bir koleksiyon oluşturabilirsiniz. Bunu yapmak için sorgu kuralı kullanan bir koleksiyon oluşturun ve sorgu [oluşturma](../../core/servers/manage/create-queries.md) konusunun örnek wql sorgusunu kullanın.  

 Daha fazla bilgi için bkz. [uygulamaları dağıtma](../../apps/deploy-use/deploy-applications.md).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>5. Adım: Mac uygulamasının dağıtımını Izleme  
 Windows bilgisayarlarına uygulama dağıtımlarını izlemek üzere, Mac bilgisayarlara uygulama dağıtımlarını izlemek için aynı işlemi kullanabilirsiniz.  

 Daha fazla bilgi için bkz. [uygulamaları izleme](../deploy-use/monitor-applications-from-the-console.md).  
