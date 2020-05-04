---
title: Paketleri analiz etme ve dönüştürme
titleSuffix: Configuration Manager
description: Configuration Manager 'de Paket Dönüştürme Yöneticisi ile paket çözümleme ve dönüştürme hakkında bilgi edinin.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f72e7330909bc5653e69790e38ae043e539cc239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709939"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Paket Dönüştürme Yöneticisi ile paketleri çözümleme ve dönüştürme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1357861-->

Bir paketi dönüştürebilmeniz için önce onu çözümleyin. Analiz sonuçlarına bağlı olarak, aşağıdaki görevlerden birini yapabilirsiniz:

- Paketi bir uygulamaya **dönüştürün** . Konsolundaki **paket** listesinde, hazırlık durumu **Otomatik**' i görüntüler.  

- Paketi **onarın ve dönüştürün** , Koleksiyonlar ekleyin ve genel koşullar oluşturun. Konsolundaki **paket** listesinde, hazırlık durumu **Otomatik**' i görüntüler.  

- Paketi **onarın ve dönüştürün** . Konsolundaki **paket** listesinde, hazırlık durumu **el ile**görüntülenir.  

- Paketi dönüştürülmemiş olarak bırakın. Konsolundaki **paket** listesinde, hazırlık durumu **geçerli değil**görüntülenir.  



## <a name="how-to-analyze-packages"></a><a name="bkmk_analyze"></a>Paketleri analiz etme

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Uygulama yönetimi**' ni genişletin ve **paketler** düğümünü seçin.  

2. Dönüştürülecek paketi seçin. Şeridin **giriş** sekmesinde, **paket dönüştürme** grubunda, **paketi çözümle**' yi seçin. Paket Dönüştürme Yöneticisi paketi analiz eder.  

3. Paketin hazırlık durumunu görmek için, **hazırlık** sütununu paketler listesine ekleyin. Paketin hazırlık durumu, sonraki eyleminizi belirler:  

    - **Otomatik**: [paketleri dönüştürme](#bkmk_convert)  

        Ayrıca, koleksiyonları eklemek ve **Otomatik** hazırlık durumuyla genel koşullar oluşturmak için bkz. [paketleri çözme ve dönüştürme](#bkmk_fix).  

    - **El ile**: [paketleri çözme ve dönüştürme](#bkmk_fix)

    - **Uygulanamaz**: Bu pakette gerekli içerik veya bir program eksik. Eksik içerik veya programları ekleyin ve çözümlemeyi yeniden deneyin. Ya da dönüştürülmemiş bir durumda bırakın ve paket olarak dağıtmaya devam edin.  

    - **Bilinmiyor**: önce **Çözümle** görevini çalıştırın veya zamanlanan bir sonraki analizler için bekleyin. Durum değişmezse, bkz. [Paket Dönüştürme Yöneticisi sorunlarını giderme](troubleshoot-pcm.md).<!-- SCCMDocs#2044 -->

## <a name="how-to-convert-packages"></a><a name="bkmk_convert"></a>Paketleri dönüştürme

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Uygulama yönetimi**' ni genişletin ve **paketler** düğümünü seçin.  

2. **Otomatik**hazırlık durumuyla dönüştürülecek paketi seçin. Şeridin **giriş** sekmesinde, **paket dönüştürme** grubunda, **paketi Dönüştür**' ü seçin. Paketi uygulamaya Dönüştürme Sihirbazı açılır.  

3. Paketi uygulamaya dönüştürme sihirbazında, seçili paketlerin listesini gözden geçirin. Dönüştürmek istemediğiniz paketleri kaldırın ve **Tamam**' ı seçin. Paket Dönüştürme Yöneticisi paketi dönüştürür. Dönüştürme Tamam penceresinde, yeni uygulamaların dönüştürme durumu listelenir.  

    > [!Note]  
    > Bir paketi dönüştürdüğünüzde, site dönüştürmenin tarih ve saatini UTC saati olarak kaydeder.  

4. Penceredeki yönergeleri izleyin. **Uygulamaları görüntüle** veya **Kapat**seçeneklerinden birini belirleyin.  



## <a name="how-to-fix-and-convert-packages"></a><a name="bkmk_fix"></a>Paketleri onarma ve dönüştürme

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin. **Uygulama yönetimi**' ni genişletin ve **paketler** düğümünü seçin.  

2. **El ile** veya **Otomatik**hazırlık durumuna sahip bir paket seçin. Şeridin **giriş** sekmesinde, **paket dönüştürme** grubunda, **düzeltir ve Dönüştür**' ü seçin.  

3. Paket Dönüştürme sihirbazında, **düzeltilmesi gereken öğeleri**gösteren **paket seçimi** sayfasındaki bilgileri gözden geçirin. Ardından **İleri**' yi seçin.  

4. **Bağımlılık incelemesi** sayfasında, paketin listelenen diğer paketlere bağımlı olup olmadığını gözden geçirin ve ardından **İleri**' yi seçin.  

    > [!Note]  
    > Listelenen bağımlı paketlerin hiçbirini dönüştürmediyse, önce bu paketleri dönüştürün. Ardından paket dönüştürme işlemini yeniden başlatın.  
    >  
    > Bağımlılık gerekmiyorsa, silin veya yoksayın ve dönüştürme işlemine devam edin.  

5. **Dağıtım türü** sayfasında, yeni uygulamanın dağıtım türlerini gözden geçirin. Önceliklerini değiştirin veya dağıtım türlerini silin.  

6. Yeni dağıtım türlerinden herhangi birinde ilişkili bir algılama yöntemi yoksa, **algılama yöntemi** sütununda bir uyarı simgesi görüntülenir. Aşağıdaki eylemleri doldurun:  

    1. **Düzenleme algılama yöntemini**seçin.  

    2. **Add (Ekle)** seçeneğini belirleyin.  

    3. Algılama kuralı iletişim kutusunda, bir **ayar türü**belirtin.  

    4. Belirtilen ayar türü için algılama kuralı için gereken ek bilgileri girin.  

    5. **Tamam**’ı seçin. Gerekirse, her dağıtım türüne birden çok algılama yöntemi eklemek için bu işlemi tekrarlayın.  

    6. **Tamam**’ı seçin. **Algılama yöntemi** sütununun, doğru belirtilen bir algılama yöntemini onaylamak için bir simge görüntülediğini doğrulayın.  

7. **İleri**’yi seçin.  

8. **Gereksinimler seçimi** sayfasında, yeni uygulamanın dağıtım türlerini gözden geçirin. Bir dağıtım türü seçin ve bu dağıtım türü için gereksinimleri gözden geçirin.  

    > [!Note]  
    > Sihirbaz yalnızca Paket Dönüştürme Yöneticisi 'nin dönüştürdüğü gereksinimleri görüntüler. Cihaz koleksiyonlarındaki tüm WQL sorgularını gereksinimlere dönüştürmez.  

9. Gerekirse, seçili bir dağıtım türü için gereksinimler ekleyin.  

10. **İleri**’yi seçin.  

11. Uygulamayı oluşturmak için Sihirbazı doldurun.  

    > [!Note]  
    > Bir paketi dönüştürdüğünüzde, site dönüştürmenin tarih ve saatini UTC saati olarak kaydeder.  



## <a name="monitor"></a><a name="bkmk_monitor"></a>İzleyicisi

Configuration Manager konsolunun **izleme** çalışma alanına gidin ve **paket dönüştürme durumu**' nu seçin. Bu panoda, sitedeki paketlerin genel analiz ve dönüştürme durumu gösterilmektedir. Yeni bir arka plan görevi, analiz verilerini otomatik olarak özetler.

> [!Tip]  
> Configuration Manager ile tümleştirilmiş Paket Dönüştürme Yöneticisi paketlerin analizini zamanlamanız gerektirmez. Bu eylem tümleşik özetleme görevi tarafından işlenir.

![Örnek paket dönüştürme durumu panosunun ekran görüntüsü](media/1357861-pcm-dashboard.png)
