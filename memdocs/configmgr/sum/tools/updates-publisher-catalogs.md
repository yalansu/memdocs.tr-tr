---
title: Güncelleştirme kataloglarını yönetme
titleSuffix: Configuration Manager
description: System Center Updates Publisher için yazılım güncelleştirme kataloglarını yönetme
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1314e2b4a6adc21b876e6bdbf8b25aa9e4fd3e9a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717772"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Güncelleştirmeler Yayımcısındaki yazılım güncelleştirme kataloglarını yönetme

*Uygulama hedefi: System Center Updates Publisher*

Yazılım güncelleştirme kataloglarını yönetmek için **kataloglar** **çalışma alanını** kullanın. Buna yeni kataloglar ekleme, var olan Katalog aboneliklerini yönetme ve bir katalogdan güncelleştirmelerle ilgili bilgileri güncelleştirme yayımcısı deposuna aktarma dahildir.

Yazılım güncelleştirme katalogları, Microsoft dışındaki kuruluşlar tarafından oluşturulan ilgili güncelleştirmeler hakkında bilgiler içerir. Diğer kuruluşlar, kataloglarını Microsoft 'a kaydettirdiğiniz kendi kuruluşunuzu ve üçüncü taraf yazılım satıcılarınızı içerir. Yazılım satıcılarından kayıtlı kataloglara *iş ortağı katalogları*denir. Oluşturduğunuz ve Microsoft 'a kayıtlı olmayan kataloglara *Kullanıcı* katalogları denir.

## <a name="add-software-update-catalogs"></a>Yazılım güncelleştirme katalogları ekleme
İçerdiği güncelleştirmeleri yönetebilmeniz için önce Updates Publisher 'a bir güncelleştirme kataloğu eklemeniz gerekir. Bir katalog eklediğinizde, güncelleştiren Publisher:
-   Bu kataloğa yönelik bir abonelik oluşturur, bu nedenle bu kataloğa yönelik güncelleştirmeleri denetleyebilir.
-   Kataloğu, **kataloglar çalışma alanının** **yazılım güncelleştirme katalogları** penceresinde bir listeye ekler.  

Abone olunan her katalogla ilgili bilgiler konsolunda bulunur. Bilgiler, indirme URL 'sini veya konumunu, kataloğu oluşturan şirket veya kuruluşun adını ve en son ne zaman içeri aktarılacağını veya değiştirildiğini içerir.

Updates Publisher, her başlatıldığında aboneliklerinizi otomatik olarak denetleyebilir. Bu, [Gelişmiş bir seçenek](updates-publisher-options.md#advanced)olarak yapılandırılır. Güncelleştirme yayımcısı yapılandırıldığında, aboneliğin indirme URL 'SI veya konum bilgilerine başvurur ve katalogda en son içeri aktarışınızda bu yana yapılan değişiklikler olduğunda sizi uyarır.

Katalog güncelleştirmesini el ile denetlemek için, **yazılım güncelleştirme katalogları** listesinden kataloğu seçin ve ardından şeritten **Yenile** ' yi seçin.

Katalog eklemeye ve abone olunan kataloglarla ilgili bilgileri görüntülemeye ek olarak şunları yapabilirsiniz:
-  *Kullanıcı* kataloglarının bilgilerini **düzenleyin** .
-  Updates Publisher 'dan bir kataloğu **silin** (kaldırın).
-  Güncelleştirmeleri bir katalogdan Updates Publisher deposuna **aktarın** . Güncelleştirmeleri içeri aktardığınızda, bu katalogda bulunan tüm güncelleştirmeleri içeri aktarırsınız. Ardından güncelleştirme sunucunuzda güncelleştirmeleri seçip yayımlayabileceğiniz güncelleştirmeler çalışma alanında güncelleştirmeleri görüntüleyebilirsiniz.

> [!NOTE]   
> Bir kataloğun Updates yayımcısından silinmesi, söz konusu katalogdaki bu katalogdaki güncelleştirmelerin deponuzdan kaldırılmasına neden olur. Bu, güncelleştirme sunucunuzda yayımladığınız güncelleştirmeleri etkilemez. Güncelleştirme sunucunuzda, deponuzda olmayan güncelleştirmeleri kaldırmak için bkz. [başvurulmayan yazılım güncelleştirmelerinin süre sonu](updates-publisher-options.md#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Güncelleştirme kataloglarını yönetme
İçeri aktardığınız liste kataloglarını, **kataloglar çalışma alanının** **yazılım güncelleştirme kataloglarımı** penceresinde görebilirsiniz. Bu çalışma alanından şunları yapabilirsiniz:

-   **İş ortağı kataloğu ekle:** Yeni iş ortağı kataloglarını bulmak için aşağıdakilerden birini kullanın:

    -   Konsolunda, **güncelleştirmeler çalışma alanına** > **Genel Bakış ' a**gidin. **Başlarken** penceresinde **ortak yazılım güncelleştirme katalogları Ekle**' yi seçin.

    -   Konsolunda, **kataloglar çalışma alanı** > **kataloglarım**' a gidin. Ardından, şeritte **Katalog Ekle**' yi seçin.

-   **Kullanıcı kataloğu ekle:** Konsolunda, **kataloglar çalışma alanı** > **kataloglarım**' a gidin. Ardından, şeritte **Katalog Ekle**' yi seçin. . Cab dosyasının konumuna ek olarak, kataloğu tanımlamak için bir yayımcı, ad ve açıklama belirtmeniz gerekir.


-   **Kataloglarda güncelleştirmeleri denetle:** Bir veya daha fazla katalog seçin ve ardından şeritten **Yenile** ' yi seçin.

-   **Kullanıcı kataloğunu düzenleyin:** Bir *Kullanıcı* kataloğu seçin ve şeritten **Düzenle** ' yi seçin. Daha sonra Kullanıcı tanımlı Özellikler ' i değiştirebilirsiniz.

-   **Katalogları Sil:** Bir veya daha fazla katalog seçin ve şeritten **Kaldır** ' ı seçin. Bu, katalog, aboneliğiniz ve bu kataloglardan gelen güncelleştirmeleri Updates Publisher deponuzdan kaldırır.

-   **Katalogdan bir katalogdan güncelleştirme ekleme**: **Katalog içeri aktarma** Sihirbazı 'nı başlatmak Için şeritten **içeri aktar** ' ı seçin. Daha fazla bilgi için bkz. [güncelleştirmeleri Içeri aktarma](#import-updates)

## <a name="import-updates"></a>Güncelleştirmeleri içeri aktar
Bir kataloğu içeri aktardığınızda, Updates Manager güncelleştirmeleri bu katalogdan Updates Publisher deposuna ekler. Güncelleştirmeler alındıktan sonra, bunları yönetilen cihazlar için kullanılabilir hale getirmek üzere güncelleştirme sunucunuzda yayımlayabilirsiniz.

### <a name="to-import-updates"></a>Güncelleştirmeleri içeri aktarmak için
1. **Katalog Içeri aktarma** Sihirbazı 'nı başlatmak için aşağıdaki çalışma alanlarından birindeki şeritten **içeri aktar** ' ı seçin:

   -   Kataloglar çalışma alanı

   -   Güncelleştirmeler çalışma alanı

2. **Içeri aktarma türü** sayfasında, Updates Publisher 'a eklediğiniz bir veya daha fazla katalog seçin veya henüz abonelik olarak eklemediğiniz bir kataloğun yolunu belirtin. Özet ekranını görüntülemek için **İleri** ' yi seçin ve hazırlık sırasında, **İleri** ' yi seçerek içeri aktarmayı başlatın.

3. **Güvenlik uyarısı – Katalog doğrulama** penceresinde, Katalog sertifikasını gözden geçirin ve hazırlık sırasında, güncelleştirmeleri içeri aktarmak Için **kabul et** ' i seçin.

   > [!CAUTION]
   > Yalnızca güvendiğiniz yayımcıların güncelleştirmelerini kabul edin. Güvenilir olmayan yayımcıların yazılım güncelleştirmeleri, güncelleştirmeleri tararken istemci bilgisayarlara zarar verebilir.
   > 
   >  Artık bir yayımcıya güvenmiyorsanız, bu yayımcıyı Güvenilen Yayımcılar listesinden kaldırın. Katalogları kabul etme hakkında daha fazla bilgi edinmek için **güvenlik uyarısı – Katalog doğrulaması** Iletişim kutusunda **daha fazla bilgi ver** ' e tıklayın.

   Bir yayımcının kataloğunu her zaman kabul et ' i seçerseniz, bu yayımcı [Güvenilen yayımcılar listesine](updates-publisher-options.md#trusted-publishers)eklenir. Bu listeyi bir Updates Publisher seçeneği olarak gözden geçirebilir ve düzenleyebilirsiniz.

4. Güncelleştirme zaten depoda olduğunda ve aşağıdakilerden biri doğru olduğunda içeri aktarma bir güncelleştirmeyi içeri aktarmayı atlar:

   -   Güncelleştirme, son içeri aktarılırken değiştirilmez.

   -   Güncelleştirme düzenlendi ve yeni bir dijital karması vardır. Bir güncelleştirmenin düzenlenmesinin yapılması, yeni bir güncelleştirmenin yaptığınız gibi özgün dosyanın üzerine yazılmasını engeller. böylece, dağıttığınız değişikliklerin üzerine yazılır.

5. **Onay** sayfasında içeri aktarma sonuçları gözden geçirin.

6. Sihirbazı tamamladıktan sonra **Kapat** ' a tıklayın. Artık güncelleştirmeler çalışma alanında bu kataloğa yönelik güncelleştirmeleri görüntüleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Güncelleştirmeleri içeri aktardıktan sonra, genel eylemler şunları içerir:
-   Güncelleştirme sunucunuza paket eklemek, atamak ve dağıtmak için [güncelleştirmeleri yönetin](manage-updates-with-updates-publisher.md) .
-   Güncelleştirmelerin güncelleştirme sunucunuza ne zaman dağıtılacağını belirlemesine yardımcı olmak için [uygulanabilirlik kuralları oluşturun](updates-publisher-applicability-rules.md) .
