---
title: Uygulamaları konsoldan izleme
titleSuffix: Configuration Manager
description: Configuration Manager 'daki Izleme çalışma alanını kullanarak güncelleştirmeler, uyumluluk ayarları ve uygulamalar dahil olmak üzere yazılım dağıtımını izleyin.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 892a55ad4f3518794bef017f1d4e3a7a4de14e13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710058"
---
# <a name="monitor-applications-from-the-configuration-manager-console"></a>Configuration Manager konsolundan uygulamaları izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Configuration Manager, yazılım güncelleştirmeleri, uyumluluk ayarları, uygulamalar, görev dizileri, paketler ve programlar dahil olmak üzere tüm yazılımların dağıtımını izleyebilirsiniz. Configuration Manager konsolundaki **izleme** çalışma alanını veya raporları kullanarak dağıtımları izleyebilirsiniz.  

 Configuration Manager uygulamalar durum tabanlı izlemeyi destekler, bu da kullanıcılar ve cihazlar için son uygulama dağıtım durumunu izlemenize olanak sağlar. Bu durum iletileri, bireysel aygıtlar ile ilgili bilgileri görüntüler. Örneğin, bir uygulama bir kullanıcı koleksiyonuna dağıtılırsa, dağıtımın uyumluluk durumunu ve Configuration Manager konsolundaki dağıtım amacını görüntüleyebilirsiniz.  

## <a name="learn-about-compliance-states"></a>Uyumluluk durumları hakkında bilgi edinin
 Bir uygulama dağıtım durumunda aşağıdaki uyumluluk durumlarından biri görülür:  

-   **Başarılı** – Uygulama dağıtımı başarılı oldu veya daha önce yüklendiği bulundu.  

-   **Devam Ediyor** – Uygulama dağıtımı devam ediyor.  

-   **Bilinmiyor** – Uygulama dağıtımının durumu belirlenemedi. Bu durum **Kullanılabilir**amacına sahip dağıtımlar için geçerli değildir. Bu durum, genellikle istemciden gelen durum iletileri henüz alınmadığında görüntülenir.  

-   **Gereksinimler Karşılanmadı** – Uygulama, bir bağımlılık veya bir gereksinim kuralı ile uyumlu olmadığından veya dağıtıldığı işletim sistemi geçersiz olduğundan uygulama dağıtılmadı.  

-   **Hata** – Bir hata sebebiyle uygulamanın dağıtımı başarısız oldu.  

Uyumluluk durumu içindeki alt kategoriler ve bu kategorideki Kullanıcı ve cihaz sayısı dahil olmak üzere her uyumluluk durumu için ek bilgileri görüntüleyebilirsiniz. Örneğin, **Hata** uyumluluk durumu aşağıdaki alt kategorileri içerir:  

- Hata değerlendirme gereksinimleri  

- İçerikle ilgili hatalar  

- Yükleme hataları  

  Bir uygulamanın dağıtımı için birden çok uyumluluk durumunun geçerli olduğu durumlarda en düşük uyumluluğu temsil eden toplam durumu görebilirsiniz. Örneğin:  

  -   Bir Kullanıcı iki cihazda oturum açarsa ve uygulama bir cihaza başarıyla yüklenirse, ancak ikinci cihaza yüklenemediğinde, bu kullanıcı için uygulamanın toplam dağıtım durumu **hata**olarak görüntülenir.  

  -   Bir uygulama bir bilgisayarda oturum açtığında tüm kullanıcılara dağıtılırsa, o bilgisayar için birden çok dağıtım sonucu alırsınız. Dağıtımlardan biri başarısız olursa, o bilgisayardaki toplam dağıtım durumu **Hata**olarak görüntülenir.  

Paket ve program dağıtımları için dağıtım durumu toplanmaz.  

 Uygulama dağıtımı ile ilgili tüm önemli sorunlarınızı hızla saptamak için bu alt kategorileri kullanın. Ayrıca, uyumluluk durumunun belirli bir alt kategorisinde yer alan aygıtlar hakkında ek bilgileri de görüntüleyebilirsiniz.  

 Configuration Manager 'de uygulama yönetimi, uygulamalar ve dağıtımlar hakkındaki bilgileri izlemenizi sağlayan bir dizi yerleşik rapor içerir. Bu raporlar **Yazılım Dağıtma – Uygulama İzleme**'nin rapor kategorilerini içerir.  

 Configuration Manager raporlamayı yapılandırma hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Configuration Manager konsolundaki bir uygulamanın durumunu izleme  

1.  Configuration Manager konsolunda, **izleme**  >  **dağıtımları**' nı seçin.  

3.  Her uyumluluk durumu ve bu durumda bulunan cihazların dağıtım ayrıntılarını gözden geçirmek için bir dağıtım seçin, sonra **giriş** sekmesinde, **dağıtım** grubunda, **durumu görüntüle** ' yi seçerek **dağıtım durumu** bölmesini açın. Bu bölmede, her bir uyumluluk durumu ile varlıkları görüntüleyebilirsiniz. Söz konusu varlığa dağıtım durumu hakkında daha ayrıntılı bilgi görüntülemek için herhangi bir varlık seçin.  

    > [!NOTE]  
    >  **Dağıtım Durumu** bölmesinde görüntülenebilen öğelerin sayısı 20,000 ile sınırlıdır. Daha fazla öğe görmeniz gerekiyorsa, uygulama durumu verilerini görüntülemek için Configuration Manager raporlarını kullanın.  
    >   
    >  Dağıtım türlerinin durumu **Dağıtım Durumu** bölmesinde toplanır. Dağıtım türleri hakkında daha fazla bilgi görüntülemek için **Yazılım Dağıtma - Uygulama İzleme** rapor kategorisinde bulunan **Uygulama Altyapısı Hataları**raporunu kullanın.  

4.  Bir uygulama dağıtımı hakkında genel durum bilgilerini gözden geçirmek için bir dağıtım seçin ve ardından **Seçili dağıtım** penceresinde **Özet** sekmesini seçin.  

5.  Uygulamalar dağıtım türü hakkındaki bilgileri gözden geçirmek için bir dağıtım seçin ve ardından **Seçili dağıtım** penceresinde **dağıtım türleri** sekmesini seçin.  

**Durumu görüntüle** ' yi seçtikten sonra **dağıtım durumu** bölmesinde gösterilen bilgiler, Configuration Manager veritabanından canlı veriler olur. **Özet** sekmesinde ve **dağıtım türleri** sekmesinde gösterilen bilgiler, özetlenen veri.

**Özet** sekmesinde ve **dağıtım türleri** sekmesinde gösterilen veriler, **dağıtım durumu** bölmesinde gösterilen verilerle eşleşmiyorsa, bu sekmelerdeki verileri güncelleştirmek için **Özetlemeyi Çalıştır** ' ı seçin. Varsayılan uygulama dağıtımı özetleme aralığını şu şekilde yapılandırabilirsiniz:  

1. Configuration Manager konsolunda, **Yönetim**  >  **Site yapılandırması**  >  **siteler**' i seçin.

2. **Siteler** listesinden, özetleme aralığını yapılandırmak istediğiniz siteyi seçin ve **giriş** sekmesinde, **Ayarlar** grubunda, **durum hazırlayıcıları**' yi seçin.

3. **Durum hazırlayıcıları** Iletişim kutusunda **uygulama dağıtım Özetleyici**' nı seçin ve ardından **Düzenle**' yi seçin.  

4. **Uygulama dağıtımı Özetleyici özellikleri** iletişim kutusunda, gerekli özetleme aralıklarını yapılandırın ve ardından **Tamam**' ı seçin.  
