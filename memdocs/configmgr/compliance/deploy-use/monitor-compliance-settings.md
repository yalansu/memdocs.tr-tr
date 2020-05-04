---
title: Uyumluluk ayarlarını izleme
titleSuffix: Configuration Manager
description: Yapılandırma temelinin uyumluluk durumunu göstermek için bu konudaki yordamlardan bir veya daha fazlasını kullanın.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 839c08c8782a815703a19999bf1315fd65980ed8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712298"
---
# <a name="monitor-compliance-settings-in-configuration-manager"></a>Configuration Manager uyumluluk ayarlarını izleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Hiyerarşinizdeki cihazlara Configuration Manager yapılandırma temelleri dağıttıktan sonra, yapılandırma temelinin uyumluluk durumunu göstermek için bu konudaki yordamlardan bir veya daha fazlasını kullanabilirsiniz:

> [!NOTE]  
>  Uyumluluk ayarları raporlarında doğrulama ölçütü alanları (istemci-tarafı rapordaki eşdeğeri **Kısıtlamalar**), temel alınan Hizmet Modelleme Dili’ni (SML) gösterir. Bu, Configuration Manager konsolundaki yapılandırma öğesini yazan yöneticilerin SML bilgisine sahip olmadıkları takdirde doğrulama ölçütlerinin ne olduğunu anlamasını zorlaştırır. Bu durumda, yapılandırma öğesinin özelliklerini ve doğrulama ölçütlerini görüntülemek için Configuration Manager konsolundaki **izleme** çalışma alanını kullanın.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Configuration Manager konsolundaki uyumluluk sonuçlarını görüntüleme  
 Configuration Manager konsolunda dağıtılan yapılandırma temellerinin uyumluluğuyla ilgili ayrıntıları görüntülemek için bu yordamı kullanın.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Configuration Manager konsolundaki uyumluluk sonuçlarını görüntüleme  

1.  Configuration Manager konsolunda, **izleme** > **dağıtımları**' nı tıklatın.  

3.  **Dağıtımlar** listesinden, uyumluluk bilgilerini incelemek istediğiniz yapılandırma temeli dağıtımını seçin.  

4.  Ana sayfada yapılandırma temeli dağıtımının uyumluluğuyla ilgili özet bilgileri gözden geçirebilirsiniz. Daha ayrıntılı bilgileri görüntülemek için, yapılandırma temeli dağıtımını seçin ve **Giriş** sekmesinde, **Dağıtım** grubunda, **Durumu Görüntüle** 'ye tıklayarak **Dağıtım Durumu** sayfasını açın.  

     **Dağıtım Durumu** sayfası aşağıdaki sekmeleri içerir:  

    -   **Uyumlu**: Etkilenen varlık sayısına göre yapılandırma temelinin uyumluluğunu görüntüler. Bir kurala tıklayarak, **Varlıklar ve Uyum** çalışma alanında bulunan **Kullanıcılar** veya **Cihazlar** düğümü altında, bu kuralla uyumlu tüm kullanıcı veya cihazları içeren geçici bir düğüm oluşturabilirsiniz. **Varlık Ayrıntıları** bölmesinde, yapılandırma temeliyle uyumlu olan kullanıcı veya cihazlar görüntülenir. Ek bilgi görüntülemek için listede bir kullanıcı veya cihaza çift tıklayın.  

        > [!IMPORTANT]  
        >  Bir yapılandırma öğesi kuralı, algılanmadığında veya bir istemci cihazda geçerli değilse değerlendirilmez; Bununla birlikte, kural uyumlu olarak döndürülür.  

    -   **Hata:** Etkilenen varlık sayısına göre, seçilen yapılandırma temeli dağıtımıyla ilgili tüm hataların listesini görüntüler. **Varlıklar ve Uyum** çalışma alanının **Kullanıcılar** veya **Cihazlar** düğümü altında bir kurala tıklayarak, bu kuralla hata oluşturan tüm kullanıcı veya cihazları içeren geçici bir düğüm oluşturabilirsiniz. Bir kullanıcı veya cihaz seçtiğinizde, **Varlık Ayrıntıları** bölmesi seçili sorundan etkilenen kullanıcı veya cihazları görüntüler. Sorunla ilgili ek bilgi görüntülemek için listeden bir kullanıcı veya cihaza çift tıklayın.  

    -   **Uyumsuz:** Etkilenen varlık sayısına göre, yapılandırma temeli içinde yer alan tüm uyumlu olmayan kuralların listesini görüntüler. Bir kurala tıklayarak, **Varlıklar ve Uyumluluk** çalışma alanının **Kullanıcılar** veya **Cihazlar** düğümü altında, bu kuralla uyumlu olmayan tüm kullanıcı veya cihazları içeren geçici bir düğüm oluşturabilirsiniz. Bir kullanıcı veya cihaz seçtiğinizde, **Varlık Ayrıntıları** bölmesi seçili sorundan etkilenen kullanıcı veya cihazları görüntüler. Sorun hakkında daha fazla bilgi görüntülemek için listeden bir kullanıcı veya cihaza çift tıklayın.  

    -   **Bilinmiyor**: Cihazların geçerli istemci durumunda seçili yapılandırma temeli dağıtımı için uyumluluk bildirmeyen tüm kullanıcı veya cihazların listesini görüntüler.  

5.  **Dağıtım Durumu** sayfasında, dağıtılan yapılandırma temelinin uyumluluğuyla ilgili ayrıntılı bilgileri gözden geçirebilirsiniz. **Dağıtımlar** düğümünde, bu bilgileri tekrar hızla bulmanıza yardımcı olacak bir geçici düğüm oluşturulur.  

##  <a name="view-compliance-results-by-using-reports"></a>Raporları kullanarak uyumluluk sonuçlarını görüntüleme  
 Configuration Manager uyumluluk ayarları, yapılandırma öğeleri, yapılandırma temelleri ve dağıtımlar hakkındaki bilgileri izlemenize olanak sağlayan bir dizi yerleşik rapor içerir. Bu raporlar **Uyumluluk ve Ayarlar Yönetimi**rapor kategorisindedir.  

> [!IMPORTANT]  
>  Uyumluluk ayarları raporlarında **Cihaz filtresi** ve**%** Kullanıcı filtresi parametrelerini kullanırken joker karakteri () kullanmanız gerekir.  

 Configuration Manager raporlamayı yapılandırma hakkında daha fazla bilgi için bkz. [raporlamaya giriş](../../core/servers/manage/introduction-to-reporting.md).

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Configuration Manager Windows istemci bilgisayarında uyumluluk sonuçlarını görüntüleme

> [!NOTE]  
>  Bir etki alanı Konuk hesabı ile oturum açtıysanız Configuration Manager Windows istemcisinde bilgileri görüntüleyemezsiniz.    

1.  İstemci bilgisayarın Denetim Masası'ndaki **Configuration Manager** 'a gittikten sonra çift tıklayarak özelliklerini açın.  

2.  **Yapılandırmalar** sekmesine tıklayın ve dağıtılan yapılandırma temellerinin listesini görüntüleyin.  

3.  Her yapılandırma temeli için **Uyumluluk Durumu** ’nu görüntüleyin:  

    > [!IMPORTANT]  
    >  Değerlendirme sonuçları 15 dakika için istemcide önbelleğe alınır. 15 dakikalık süre içinde bir yeniden değerlendirme başlatırsanız, uyumluluk sonuçları yeni bir değerlendirme yerine bu önbellekten döndürülür. Bu nedenle, istemci üzerinde uyumluluk değerlendirme sonuçlarını etkileyebilecek bir değişiklik yaparsanız, yeniden değerlendirmeyi başlatmadan önce 15 dakika bekleyin.  

    -   **Uyumlu**: İstemci bilgisayar, değerlendirilen yapılandırma temeliyle uyumludur.  

    -   **Uyumlu Değil**: İstemci bilgisayar, değerlendirilen yapılandırma temeliyle uyumlu değildir.  

    -   **Bilinmiyor**: İstemci bilgisayar, yapılandırma temelini henüz değerlendirmemiştir. Değerlendirmeyi uyumluluk değerlendirme zamanlamasının dışında başlatmak istiyorsanız, değerlendirilecek yapılandırma temellerini seçin ve ardından **Değerlendir**’e tıklayın.  

        > [!NOTE]  
        >  İstemci bilgisayarda yerel yönetici kimlik bilgileriniz varsa, hangi yapılandırma öğesinin uyumsuz durum bildirdiğini belirlemek üzere, değerlendirilen her bir yapılandırma temelinin ayrıntılarını görüntüleyebilirsiniz. Bunu yapmak için yapılandırma temelini seçin ve ardından **Raporu Görüntüle**’ye tıklayın.  

4.  **Tamam**'a tıklayın.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Yapılandırma temeli uyumluluğuna göre koleksiyonlar oluşturma  
 Belirtilen uyumluluğa sahip cihazlara dayalı bir Configuration Manager koleksiyonu oluşturmak için aşağıdaki yordamı kullanın. Aşağıdaki uyumluluk durumlarına göre koleksiyonlar oluşturabilirsiniz:  

-   **Uyumlu**  

-   **Hata**  

-   **Uyumlu değil**  

-   **Bilinmiyor**  

1.  Configuration Manager konsolunda, **varlıklar ve uyumluluk** > **Uyumluluk ayarları** > **yapılandırma temelleri**' ne tıklayın.  

3.  **Yapılandırma Temelleri** listesinde, içinden bir koleksiyon oluşturmak istediğiniz yapılandırma temelini seçin.  

4.  **Dağıtım** sekmesindeki **Dağıtım Grubu**’nda **Yeni Koleksiyon Oluştur** ’a tıklayın ve ardından açılır listede koleksiyon oluşturmak istediğiniz uyumluluk düzeyini seçin.  

5.  Yapılandırma öğesinin kullanıcılara veya cihazlara dağıtıldığına bağlı olarak **Kullanıcı Koleksiyonu Oluşturma Sihirbazı** veya **Cihaz Koleksiyonu Oluşturma Sihirbazı** açılır. Sihirbaz, koleksiyonu oluşturmak için doğru değerlerle otomatik olarak doldurulur; ancak, bu değerleri düzenleyebilirsiniz.  

6.  Sihirbazı tamamladıktan sonra koleksiyon, **Varlıklar ve Uyumluluk** çalışma alanında **Kullanıcı Koleksiyonları** veya **Cihaz Koleksiyonları** düğümünü gösterir.  
