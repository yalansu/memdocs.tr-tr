---
title: Uygulamaları gözden geçirme ve değiştirme
titleSuffix: Configuration Manager
description: Configuration Manager uygulama sürümleriyle çalışmayı ve uygulamaları değiştirmeyi öğrenin.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6afed00b8207edb338b2a6dc62e083a5267fa47e
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343142"
---
# <a name="revise-and-supersede-applications-in-configuration-manager"></a>Configuration Manager uygulamaları gözden geçirme ve değiştirme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu konu başlığında Configuration Manager uygulama sürümleriyle çalışmayı ve uygulamaları yeni bir sürümle değiştirmeyi öğreneceksiniz.  

##  <a name="application-revisions"></a> Uygulama sürümleri  
 Bir uygulamada veya uygulamada yer alan bir dağıtım türünde düzeltmeler yaptığınızda, Configuration Manager uygulamanın yeni bir düzeltmesini oluşturur. Her uygulama düzeltmesinin geçmişini görüntüleyebilirsiniz. Ayrıca bir uygulamanın özelliklerini de görüntüleyebilir, önceki bir düzeltmesini geri yükleyebilir veya eski bir düzeltmesini silebilirsiniz.  

### <a name="to-display-an-application-revision-history"></a>Bir uygulama düzeltme geçmişini görüntülemek için  

1.  Configuration Manager konsolunda, **yazılım kitaplığı**  >  **uygulama yönetimi**  >  **uygulamaları**' nı seçin ve ardından istediğiniz uygulamayı seçin.  

3.  **Giriş** sekmesinde, **uygulama** grubunda, **değişiklik geçmişi** ' ni seçerek **uygulama düzeltme geçmişi** iletişim kutusunu açın.  

### <a name="to-view-an-application-revision"></a>Bir uygulama düzeltmesini görüntülemek için  

1.  **Uygulama düzeltme geçmişi** iletişim kutusunda, bir uygulama düzeltmesi seçip **görüntüle**' yi seçin.  

2.  **Özellikler** iletişim kutusunda, seçili uygulamanın özelliklerini inceleyin.  

    > [!NOTE]  
    >  Görüntülenen uygulama özellikleri salt okunurdur.  

3.  **Özellikler** iletişim kutusunu kapatın.  

### <a name="to-restore-an-application-revision"></a>Bir uygulama düzeltmesini geri yüklemek için  

1.  **Uygulama düzeltme geçmişi** iletişim kutusunda, bir uygulama düzeltmesi seçin ve ardından **geri yükle**' yi seçin.  

2.  **Düzeltme geri yüklemeyi Onayla** iletişim kutusunda, seçili uygulama düzeltmesini geri yüklemek için **Evet** ' i seçin.  

### <a name="to-delete-an-application-revision"></a>Bir uygulama düzeltmesini silmek için  

1.  **Uygulama düzeltme geçmişi** iletişim kutusunda, bir uygulama düzeltmesi seçip **Sil**' i seçin.  

2.  **Uygulama düzeltmesini Sil** Iletişim kutusunda **Evet**' i seçin.  

> [!IMPORTANT]  
>  Geçerli uygulama düzeltmesini yalnızca, uygulama kullanımdan kalkmışsa ve başvuru yoksa silebilirsiniz.  

##  <a name="application-supersedence"></a> Uygulamanın yerine geçme  
 Configuration Manager 'de uygulama yönetimi, bir yerine geçme ilişkisi kullanarak mevcut uygulamaları yükseltmenize veya değiştirmenize olanak sağlar. Bir uygulamayı yenisiyle değiştirdiğinizde, yerine geçilen uygulamanın dağıtım türünü değiştirmek üzere yeni bir dağıtım türü belirtebilir ve ayrıca yerine geçen uygulama yüklenmeden önce yerine geçilen uygulamayı yükseltip yükseltmemeye karar verebilirsiniz. Genel anlamda, yerine geçme zincirlerinin en fazla beş düzey derinlikte sınırlanmasını öneririz.
 
> [!IMPORTANT]  
>  Yerine geçilen dağıtım türünü kaldırma seçeneği belirlendiğinde, bir dağıtım türünün yerine, farklı bir koleksiyon türüne dağıtılan bir dağıtım türü geçirilemez.  Örneğin, yerine geçirilen dağıtım türünü kaldırma seçeneği belirlendiğinde, bir cihaz koleksiyonuna dağıtılan dağıtım türünün yerini, bir kullanıcı koleksiyonuna dağıtılan dağıtım türü alamaz.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Bir uygulamayı yükseltmeye veya değiştirmeye karar verme  
 Bir uygulamayı değiştirmeyi veya yükseltmeyi uygulama özellikleri iletişim kutusunun **Yerine Geçen İlişki Belirt** iletişim kutusunda belirtebilirsiniz. Yerine geçme türü, bu iletişim kutusunda **Kaldır** seçeneğini işaretleyip işaretlemediğinize bağlı olarak değişir:  

-   Aynı uygulamanın (aynı uygulama KIMLIĞI ile) daha yeni bir sürümüne güncelleştirmek istiyorsanız, **Kaldır** **seçeneğini işaretleyin** .  

-   Farklı bir uygulamaya (farklı uygulama kimliği ile) geçmek istiyorsanız **Kaldır**seçeneğini işaretleyin. Uygulamanın yenisiyle değiştirilen sürümünü kaldırmanız gerekir.  

### <a name="supersede-dependent-applications"></a>Bağımlı uygulamaların yerini değiştirme  
 Bu örnekte, **ana uygulama** , bağımlılıkları olan dağıtmakta olduğunuz uygulamayı ifade eder.  

 Bağımlı uygulamayı yeni bir sürüme güncelleştiren bir yerine geçme ilişkisi oluşturabilirsiniz.  

1. Yeni bağımlı uygulamanın ve özgün bağımlı uygulamanın ana uygulamada aynı bağımlılık grubunda olduğundan emin olun.  

2. Özgün bağımlı uygulamayı yeni bağımlı uygulamayla değiştiren bir yerine geçme ilişkisi oluşturun.  

   Ana uygulamanın yeni yüklemeleri sırasında yeni bağımlı uygulama yüklenir. Ana uygulamanın var olan yüklemeleri, yeni bağımlı uygulamayla güncelleştirilir.  

   Nihai sonuç, ana uygulamanın tüm dağıtımlarının yeni bağımlı uygulamayı kullanlarıdır.  

### <a name="further-considerations"></a>Dikkat edilecek diğer konular  

-   Bağımlı uygulamalar için birden çok yerine geçme ilişkisi belirtebilirsiniz. Yerine geçme zincirindeki en yüksek bağımlı uygulama yüklenir.  

-   Bağımlı uygulamalar, ana uygulamanın yüklü olduğu veya bağımlı uygulamanın yüklenemeyeceği cihaza dağıtılmalıdır.  

-   Ana uygulamanın yeni yüklemeleri için birden çok bağımlılığınız olduğunda, bağımlılık sırası bağımlı uygulamanın hangi sürümünün yükleneceğini belirler.  

### <a name="to-specify-a-supersedence-relationship"></a>Yerine geçme ilişkisi belirtmek için  

1.  Configuration Manager konsolunda, **yazılım kitaplığı**  >  **uygulama yönetimi**  >  **uygulamaları**' nı seçin ve ardından başka bir uygulamanın yerine geçen uygulamayı seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler** ' i seçerek uygulama adı **Özellikler** iletişim kutusunu açın.  

4.  *<uygulama adı \> * **Özellikler** iletişim kutusunun **yerine geçme** sekmesinde **Ekle**' yi seçin.  

5.  **Yerine Geçen İlişki Belirt** iletişim kutusunda, **Gözat**'a tıklayın.  

6.  **Uygulama Seç** iletişim kutusunda, yerine koymak istediğiniz uygulamayı seçin ve ardından **Tamam**' ı seçin.  

7.  Yerine geçen **Ilişki belirt** iletişim kutusunda, yerine geçilen uygulamanın dağıtım türünü değiştiren dağıtım türünü seçin.  

    > [!NOTE]  
    >  Varsayılan olarak, yeni dağıtım türü yerine geçilen uygulamanın dağıtım türünü kaldırmaz. Bu senaryo, varolan bir uygulamaya yükseltme dağıtmak istediğinizde sık kullanılır. Yeni dağıtım türü yüklenmeden önce varolan dağıtım türünü kaldırmak için **Kaldır** 'ı seçin. Bir uygulamayı yükseltmeye karar verirseniz, bunu önce laboratuar ortamında test etmeyi unutmayın.  

8.  **Yerine geçme Ilişkisini belirt** iletişim kutusunu kapatmak için **Tamam ' ı** seçin.  

9. *<uygulama adı \> * **Özellikler** iletişim kutusunu kapatmak için **Tamam ' ı** seçin.  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Geçerli uygulamanın yerine geçen uygulamaları görüntülemek için  

1.  Configuration Manager konsolunda **yazılım kitaplığı**' nı seçin.  

2.  **Yazılım kitaplığı** çalışma alanında **uygulama yönetimi**' ni genişletin, **uygulamalar**' ı seçin ve ardından istediğiniz uygulamayı seçin.  

3.  **Giriş** sekmesinde, **Özellikler** grubunda, **Özellikler** ' i seçerek *<uygulama adı \> * **Özellikler** iletişim kutusunu açın.  

4.  * \><uygulama adı* **Özellikler** iletişim kutusunun **Başvurular** sekmesinde, **Bu uygulamanın yerine geçen uygulamalar** **ilişki türü** açılan listesinden seçin.  

5.  Seçili uygulamanın yerini alan uygulamaların listesini gözden geçirin ve ardından **Tamam** ' ı seçerek *<uygulama adı \> * **Özellikler** iletişim kutusunu kapatın.  
