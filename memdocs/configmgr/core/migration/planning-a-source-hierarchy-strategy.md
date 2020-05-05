---
title: Kaynak hiyerarşi stratejisi
titleSuffix: Configuration Manager
description: Bir Configuration Manager geçiş işini yapılandırmadan önce bir kaynak hiyerarşisini yapılandırın ve kaynak sitesinden veri toplayın.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28960753da06058ef181f94a5d11d9f2327ebf56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719683"
---
# <a name="plan-a-source-hierarchy-strategy-in-configuration-manager"></a>Configuration Manager bir kaynak hiyerarşisi stratejisi planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager ortamınızda bir geçiş işi ayarlamadan önce, bir kaynak hiyerarşi yapılandırmanız ve bu hiyerarşideki en az bir kaynak siteden veri toplamanız gerekir. Kaynak hiyerarşileri yapılandırmayı, kaynak siteleri yapılandırmayı ve Configuration Manager kaynak hiyerarşideki Kaynak sitelerden nasıl bilgi toplayacağını belirlemeyi planlamada yardımcı olması için aşağıdaki bölümleri kullanın. 

##  <a name="source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a>Kaynak hiyerarşileri  
Kaynak hiyerarşi, geçirmek istediğiniz verileri içeren Configuration Manager bir hiyerarşisidir. Geçiş ayarlama ve bir kaynak hiyerarşi belirttiğinizde, kaynak hiyerarşinin en üst düzey sitesini belirtirsiniz. Bu siteye kaynak site de denir. Kaynak hiyerarşideki verileri geçirebileceğiniz ek siteler de kaynak siteler olarak adlandırılır.  

-   Configuration Manager 2007 kaynak hiyerarşisinden veri geçirmek üzere bir geçiş işi ayarlarken, kaynak hiyerarşisindeki bir veya daha fazla belirli kaynak siteden veri geçirmek üzere yapılandırın.  

-   System Center 2012 Configuration Manager veya sonraki bir sürümünü çalıştıran bir kaynak hiyerarşisinden veri geçirmek üzere bir geçiş işi ayarladığınızda, yalnızca üst düzey siteyi belirtmeniz gerekir.  

Tek seferde yalnızca bir kaynak hiyerarşisi ayarlayabilirsiniz.  

-   Yeni bir kaynak hiyerarşisi ayarlarsanız, bu hiyerarşi otomatik olarak önceki kaynak hiyerarşisinin yerini alan geçerli kaynak hiyerarşisi olur.  

-   Bir kaynak hiyerarşisini ayarlarken, kaynak hiyerarşinin en üst düzey sitesini belirtmeniz ve bu kaynak sitenin SMS sağlayıcısı ve site veritabanına bağlanmak için kullanılacak Configuration Manager kimlik bilgilerini belirtmeniz gerekir.  

-   Configuration Manager, kaynak sitedeki nesneler ve dağıtım noktaları hakkında bilgi almak üzere veri toplamayı çalıştırmak için bu kimlik bilgilerini kullanır.  

-   Veri toplama işleminin parçası olarak, kaynak hiyerarşideki alt siteler tanımlanır.  

-   Kaynak hiyerarşisi bir Configuration Manager 2007 hiyerarşisidir bu ek siteleri, her kaynak sitesi için ayrı kimlik bilgileriyle kaynak siteler olarak ayarlayabilirsiniz.  

Art arda birden fazla kaynak hiyerarşisi ayarlayabilmenize karşın, geçiş bir seferde yalnızca bir kaynak hiyerarşisi için etkin olur.  

-   Geçerli kaynak hiyerarşisinden geçişi tamamlamadan önce ek bir kaynak hiyerarşisi ayarlarsanız, Configuration Manager tüm etkin geçiş işlerini iptal eder ve geçerli kaynak hiyerarşisi için zamanlanmış geçiş işlerini erteler.  

-   Yeni yapılandırılan kaynak hiyerarşisi bundan sonra geçerli kaynak hiyerarşisi olur ve özgün kaynak hiyerarşisi artık devre dışıdır.  

-   Daha sonra yeni kaynak hiyerarşisi için bağlantı kimlik bilgilerini, ek kaynak siteleri ve geçiş işlerini ayarlayabilirsiniz.  

Etkin olmayan bir kaynak hiyerarşisini geri yükler ve daha önce **Temizleme geçiş verilerini**kullanmadıysanız, bu kaynak hiyerarşi için daha önce yapılandırılan geçiş işlerini görüntüleyebilirsiniz. Bununla birlikte, bu hiyerarşiden geçişe devam edebilmeniz için önce kimlik bilgilerini hiyerarşideki ilgili kayna sitelere bağlanacak şekilde yeniden yapılandırmanız ve tamamlanmamış geçiş işleri varsa bunları da yeniden zamanlamanız gerekir.  

> [!CAUTION]  
>  Birden fazla kaynak hiyerarşiden veri geçirirseniz, ek kaynak hiyerarşilerin her birinin birtakım benzersiz site kodları içermesi gerekir.  
> Kaynak ve hedef hiyerarşileri farklı site kodları kümesi de gerektirir.

Kaynak hiyerarşisini yapılandırma hakkında daha fazla bilgi için bkz. [Configuration Manager geçerli dala geçiş için kaynak hiyerarşileri ve kaynak siteleri yapılandırma](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="source-sites"></a><a name="BKMK_Source_Sites"></a>Kaynak siteler  
 Kaynak siteler kaynak hiyerarşideki geçirmek istediğiniz verilerin bulunduğu sitelerdir. Kaynak hiyerarşinin üst düzey sitesi her zaman birinci kaynak sitedir. Geçiş yeni bir kaynak hiyerarşisinin ilk kaynak sitesinden veri topladığında, bu hiyerarşideki ek sitelerle ilgili bilgileri keşfeder.  

 İlk kaynak site için veri toplama tamamlandıktan sonra, gerçekleştireceğiniz site eylemleri kaynak hiyerarşinin ürün sürümüne göre değişir.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Configuration Manager 2007 SP2 çalıştıran kaynak siteleri  
 Configuration Manager 2007 SP2 hiyerarşisinin ilk kaynak sitesinden veriler toplandıktan sonra, geçiş işleri oluşturmadan önce ek kaynak siteler ayarlamanız gerekmez. Bununla birlikte, ek sitelerden veri geçirebilmeniz için önce, ek siteleri kaynak siteler olarak ayarlamanız ve Configuration Manager bu sitelerden verileri başarıyla toplaması gerekir.  

 Ek sitelerden veri toplamak için, her siteyi ayrı ayrı kaynak site olarak ayarlarsınız. Bu, her kaynak sitenin SMS sağlayıcısı ve site veritabanına bağlanmak için Configuration Manager kimlik bilgilerini belirtmenizi gerektirir. Bir kaynak site için kimlik bilgilerini ayarladıktan sonra, bu site için veri toplama işlemi başlar.  

 Configuration Manager 2007 SP2 kaynak hiyerarşisinde ek kaynak siteleri ayarlarken, en üst kısımdaki kaynak siteleri ayarlamanız gerekir, bu da en son alt katman sitelerini ayarlamanız anlamına gelir. Hiyerarşinin bir dalındaki kaynak siteleri istediğiniz zaman yapılandırabilirsiniz, ancak alt sitelerini kaynak siteler olarak ayarlamadan önce bir siteyi kaynak site olarak ayarlamanız gerekir.  

> [!NOTE]  
>  Geçiş için yalnızca Configuration Manager 2007 SP2 hiyerarşisindeki birincil siteler desteklenir.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>System Center 2012 Configuration Manager veya üstünü çalıştıran kaynak siteler  
 System Center 2012 Configuration Manager veya üzeri hiyerarşinin ilk kaynak sitesinden veriler toplandıktan sonra, bu kaynak hiyerarşisinde ek kaynak siteleri ayarlamanız gerekmez. Bunun nedeni, Configuration Manager 2007 ' den farklı olarak, Configuration Manager ' nin paylaşılan bir veritabanını kullanmasına ve paylaşılan veritabanının ilk kaynak sitedeki tüm kullanılabilir nesneleri tanımlayıp geçirebilmenizi sağlar.  

 Veri toplamak için erişim hesaplarını ayarlarken, kaynak hiyerarşideki birden fazla bilgisayara **kaynak SITE SMS sağlayıcı hesabı** erişimi vermeniz gerekebilir. Bu özellik, kaynak sitenin her bilgisayarda birden çok SMS Sağlayıcısı örneğini desteklediği durumlarda gerekli olabilir. Veri toplama başladığında, hedef hiyerarşinin üst düzey sitesi, kaynak hiyerarşideki üst düzey sitenin SMS Sağlayıcısının konumlarını belirlemek için bu siteyle bağlantı kurar. SMS sağlayıcının yalnızca ilk örneği tanımlanır. Veri toplama işlemi tanımladığı konumlarda SMS Sağlayıcıya erişemezse, işlem başarısız olur ve bu site için SMS Sağlayıcının bir örneğini çalıştıran ek bilgisayarlara bağlanmayı denemez.  

##  <a name="data-gathering"></a><a name="BKMK_Data_Gathering"></a>Veri toplama  
 Kaynak hiyerarşisini belirttikten, bir kaynak hiyerarşisindeki her bir ek kaynak sitesi için kimlik bilgilerini ayarladıktan veya bir kaynak sitenin dağıtım noktalarını paylaştıktan hemen sonra, Configuration Manager kaynak siteden veri toplamaya başlar.  

 Veri toplama işlemi daha sonra, kaynak sitedeki verilerde yapılan değişikliklerle eşitlemeyi devam ettirmek üzere basit bir takvim ile kendini tekrarlar. Varsayılan olarak, işlem dört saatte bir tekrarlanır. Bu döngüye yönelik zamanlamayı, kaynak sitenin **özelliklerini** düzenleyerek değiştirebilirsiniz. İlk veri toplama işlemi, Configuration Manager veritabanındaki tüm nesneleri gözden geçirmeli ve tamamlanması uzun zaman alabilir. Sonraki veri toplama işlemleri yalnızca verilerde yapılan değişiklikleri tanımlar ve tamamlanması daha kısa sürer.  

 Veri toplamak için, hedef hiyerarşideki üst düzey site SMS Sağlayıcıya ve kaynak sitenin veritabanına bağlanarak nesnelerin ve dağıtım noktaların listesini alır. Bu bağlantılar kaynak site erişim hesaplarını kullanır. Veri toplamaya yönelik gereken yapılandırma hakkında daha fazla bilgi için bkz. [geçiş önkoşulları](../../core/migration/prerequisites-for-migration.md).  

 **Şimdi veri topla** ve Configuration Manager konsolundaki **verileri toplamayı durdur** ' i kullanarak veri toplama işlemini başlatabilir ve durdurabilirsiniz.  

 Bir kaynak site için herhangi bir nedenle **veri toplamayı durdur** seçeneğini kullandıktan sonra, bu siteden veri toplayabilmeniz için önce sitenin kimlik bilgilerini yeniden yapılandırmanız gerekir. Kaynak siteyi yeniden yapılandırana kadar Configuration Manager, bu sitedeki yeni nesneleri veya daha önce geçirilmiş nesnelerdeki değişiklikleri tanımlayamaz.  

> [!NOTE]  
>  Tek başına birincil siteyi merkezi yönetim sitesi içeren bir hiyerarşiye genişlettikten önce tüm veri toplamayı durdurmanız gerekir. Site genişletmesi tamamlandıktan sonra veri toplamayı yeniden yapılandırabilirsiniz.  

### <a name="gather-data-now"></a>konsolundaki  
 Bir site için ilk veri toplama işlemi çalıştıktan sonra, bu işlem son veri toplama döngüsünden bu yana güncelleştirilen nesneleri tanımlamak için kendisini tekrarlar. İşlemi hemen başlatmak ve sonraki döngüsünün başlangıç saatini sıfırlamak için Configuration Manager konsolundaki **Şimdi verileri topla** eylemini de kullanabilirsiniz.  

 Bir kaynak site için veri toplama işlemi başarıyla tamamlandıktan sonra, kaynak siteden dağıtım noktalarını paylaşabilir ve siteden veri geçirmek üzere geçiş işleri yapılandırabilirsiniz. Veri toplama geçiş için tekrarlanan bir işlemdir ve kaynak hiyerarşisini değiştirene veya bu site için veri toplama işlemini sonlandırmak için **veri toplamayı durdur** ' u kullanmanıza kadar devam eder.  

### <a name="stop-gathering-data"></a>ve  
 Artık bu siteden yeni veya değiştirilmiş nesneleri tanımlamak Configuration Manager istemediğiniz zaman bir kaynak site için veri toplama işlemini sonlandırmak için veri **toplamayı durdur** ' i kullanabilirsiniz. Bu eylem Ayrıca Configuration Manager, hedef hiyerarşideki istemcileri, geçirdiğiniz içeriğin içerik konumları olarak kaynaktan paylaşılan dağıtım noktaları olarak sunmayı da engeller.  

 Her kaynak siteden veri toplamayı durdurmak için, en alt katman kaynak sitelerde **veri toplamayı durdur** ' u çalıştırmanız ve ardından her üst sitede işlemi tekrarlamanız gerekir. Kaynak hiyerarşisinin en üst düzeydeki sitesi, veri toplamayı durdurduğunuz son site olmalıdır. Bu eylemi bir üst sitede uygulamadan önce alt sitelerin her birinde veri toplamayı durdurmalısınız. Genellikle veri toplamayı yalnızca geçirme işlemini tamamlaya hazır olduğunuzda durdurursunuz.  

 Bir kaynak site için veri toplamayı durdurduktan sonra, bu sitedeki nesneler ve Koleksiyonlar hakkında daha önce toplanan bilgiler, yeni geçiş işleri ayarlarken kullanılabilir kalır. Bununla birlikte, yeni nesne veya koleksiyonlar görmezsiniz veya var olan nesnelerde yapılan değişiklikleri görmezsiniz. Kaynak siteyi yeniden yapılandırır ve veri toplamaya yeniden başlarsanız, daha önce geçirilen nesnelerle ilgili bilgileri ve durumu görürsünüz.  
