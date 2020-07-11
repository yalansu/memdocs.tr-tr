---
title: "İstemci tarafından yönetilen Mac 'ler için yapılandırma öğeleri oluşturma "
titleSuffix: Configuration Manager
description: Mac OS X cihazların ayarlarını yönetmek için Configuration Manager Mac OS X yapılandırma öğesini kullanın.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 9323fc3c1203d20c77af1f2fd27cee0a377e8d68
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240091"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Mac OS X cihazları için yapılandırma öğeleri oluşturma
Configuration Manager istemcisi tarafından yönetilen Mac OS X cihazların ayarlarını yönetmek için Configuration Manager **Mac OS X (özel)** yapılandırma öğesini kullanın.  
  
Mac OS X işletim sistemi, uygulama ayarlarını depolamak için özellik listesi (. plist) dosyalarını kullanır. Bir özellik listesi dosyasındaki ayarları değerlendirmek ve düzeltmek için uyumluluk ayarlarını kullanın. Mac OS X ayarlarını, uyumluluk için değerlendirebileceğiniz ve düzeltebileceğiniz bir değer döndüren bir kabuk betiği yazarak da yönetebilirsiniz.  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>Özel bir Mac OS X yapılandırma öğesi oluşturma  
  
1. Configuration Manager konsolunda, **varlıklar ve uyumluluk**' i seçin.  
  
2. **Varlıklar ve uyum** çalışma alanında, **Uyumluluk ayarları**' nı genişletin ve **yapılandırma öğeleri**' ni seçin.  
  
3. **Giriş** sekmesinde, **Oluştur** grubunda, **yapılandırma öğesi oluştur**' u seçin.  
  
4. **Yapılandırma öğesi oluşturma** Sihirbazı ' nın **genel** sayfasında, yapılandırma öğesi için bir ad ve isteğe bağlı bir açıklama belirtin.  
  
5. **Oluşturmak istediğiniz yapılandırma öğesi türünü belirtin**’in altından **Mac OS X (özel)** seçeneğini belirleyin.  
  
6. Configuration Manager konsolundaki yapılandırma öğelerini aramanıza ve filtrelemenize yardımcı olacak kategoriler oluşturup atarsanız **Kategoriler**' i seçin.  
  
7. Sihirbazın **Desteklenen Platformlar** sayfasında, yapılandırma öğesini değerlendirecek belirli Mac OS X sürümlerini seçin.  
  
8. Sihirbazın **Ayarlar** sayfasında, Mac bilgisayarlarda uyumluluk için değerlendirilen yeni ayarlar ekleyin. **Ayar oluştur** iletişim kutusunu açmak için **Yeni** ' yi seçin.  
  
9. **Ayar Oluştur** iletişim kutusunda, ayar için benzersiz bir ad ve açıklama girin.  
  
10. İstediğiniz **ayar türünü** seçin ve gerekli bilgileri sağlayın:  
  
    -   **Mac OS X Tercihleri**  
  
        -   **Uygulama kimliği**: bir anahtarı uyumluluk için değerlendirmek istediğiniz özellik listesi dosyasının uygulama kimliğini belirtin.  
  
             Örneğin Safari Web tarayıcısı ayarlarını değiştirmek isterseniz **com.apple.Safari.plist** kullanabilirsiniz.  
  
        -   **Anahtar**: Mac bilgisayarlarda uyumluluk için değerlendirmek istediğiniz anahtarın adını belirtin. Şu söz dizimini kullanın: */<sözlük\>/<anahtaradı\>*.  
  
            > [!IMPORTANT]  
            >  Anahtar adı büyük/küçük harfe duyarlıdır ve Mac bilgisayardaki anahtar adından farklıysa değerlendirilmeyecektir. Ayrıca, anahtarı belirledikten sonra anahtar adını düzenleyemezsiniz. Anahtar adını düzenlemeniz gerekirse ayarı silip yeniden oluşturun.  
  
    -   **Komut Dosyası**  
  
        -   **Bulma betiği**: **komut dosyası Ekle**' yi seçin ve Mac bilgisayardaki ayarları uyumluluk için değerlendirmek üzere bir kabuk betiği girin. Uyumluluk için Configuration Manager için değer döndürmek üzere kabuk betiğinde **echo** komutunu kullanın. Configuration Manager uyumluluğu değerlendirmek için **stdout** 'da döndürülen sonuçları kullanır.  
  
            > [!IMPORTANT]  
            >  Bulma betiğine **yeniden başlatma** komutunu eklemeyin. Bulma betiği istemci her yeniden başlatıldığında çalıştığından, Mac bilgisayarın sürekli olarak yeniden başlatılmasına neden olur.  
  
        -   **Düzeltme betiği (isteğe bağlı)**: isteğe bağlı olarak, **komut dosyası Ekle**' yi seçin ve ardından Mac istemci bilgisayarlarında bulunan tüm uyumsuz ayarları düzeltmek için kullanılan bir kabuk betiği girin.  
  
            > [!IMPORTANT]  
            >  Mac bilgisayarın yorumlayamayacağı biçimlendirme karakterlerini tanıttığınızdan emin olmak için kopyalama ve yapıştırmayı kullanmayın. Bunun yerine, komut dosyasını yazın.  
  
11. Ayarı değerlendirmek için kullanılmadan önce koşulun verileri döndürdüğü biçim olan **veri türünü**seçin.  
  
    > [!NOTE]  
    >  **Kayan nokta** veri türü, ondalık ayırıcıdan sonra yalnızca 3 basamağı destekler.  
    >   
    >  Configuration Manager, Mac yapılandırma öğesi betik ayarları için **Boolean** veri türü kullanımını desteklemez. Bunun yerine, veri türünü **tamsayı**olarak ayarlayın ve betiğin bir tamsayı değeri döndürdüğünden emin olun.  
  
12. Ayarı kaydetmek için **Tamam** ' ı seçin ve **ayar oluştur** iletişim kutusunu kapatın. Ardından, gerek duyduğunuz sayıda ayar eklemeye devam edin.  
  
13. Sihirbazın **Uyumluluk kuralları** sayfasında, bir yapılandırma öğesinin uyumluluğunu tanımlayan koşulları belirtin. Bu ayar, uyumluluk açısından değerlendirilmeden önce en az bir uyumluluk kuralına sahip olmalıdır. Yeni bir kural eklemek için **Yeni** ' yi seçin.  
  
14. **Kural Oluştur** iletişim kutusunda, aşağıdaki bilgileri sağlayın:  
  
    -   **Ad**: uyumluluk kuralı için bir ad girin.  
  
    -   **Açıklama**: uyumluluk kuralı için bir açıklama girin.  
  
    -   **Seçili ayar**: **Ayar seç** Iletişim kutusunu açmak için **Gözden** geçirme ' yi seçin. Kural tanımlamak istediğiniz ayarı seçin veya **yeni ayar**' ı seçin. İşiniz bittiğinde **Seç**' i seçin.  
  
        > [!TIP]  
        >  Ayrıca, şu anda seçili olan ayar hakkındaki bilgileri görüntülemek için **Özellikler** ' i de seçebilirsiniz.  
  
    -   **Kural türü**: kullanmak istediğiniz uyumluluk kuralının türünü seçin:  
  
        -   **Değer**: yapılandırma öğesi tarafından döndürülen değeri belirttiğiniz değerle karşılaştıran bir kural oluşturun.  
  
        -   **Varlıksal**: bir cihazda var olup olmadığına bağlı olarak ayarı değerlendiren bir kural oluşturun.  
  
    -   **Değer** kural türü için aşağıdaki bilgileri belirtin:  
  
        -   **Ayar, şu kurala uygun olmalıdır**: seçili ayarla uyumluluk açısından değerlendirilen bir işleç ve değer seçin. Aşağıdaki işleçleri kullanabilirsiniz:  
  
            -   **Eşittir**  
  
            -   **Eşit değildir**  
  
            -   **Büyüktür**  
  
            -   **Küçüktür**  
  
            -   **Aralarında**  
  
            -   **Büyük veya eşittir**  
  
            -   **Küçüktür veya eşittir**  
  
            -   **Bunlardan biri**: metin kutusunda, her satırda bir giriş belirtin.  
  
            -   **Hiçbiri**: metin kutusunda, her satırda bir giriş belirtin.  
  
        -   **Desteklendiğinde uyumsuz kuralları düzelt**: uyumsuz kuralları otomatik olarak düzeltmek Configuration Manager istiyorsanız bu seçeneği belirleyin.  
  
            > [!IMPORTANT]  
            >  Uyumsuz kuralları, yalnızca kural işleci **Eşittir** olarak ayarlandığında düzeltebilirsiniz.  
  
        -   **Bu ayar örneği bulunmazsa uyumsuzluğu bildir**: Bu ayar Mac bilgisayarda bulunamazsa yapılandırma öğesi uyumsuzluğu raporlar.  
  
        -   **Raporlar Için uyumsuzluk önem derecesi**: Bu uyumluluk kuralının başarısız olması durumunda bildirilen önem derecesini belirtin. Kullanılabilen önem dereceleri aşağıdaki gibidir:  
  
            -   **Hiçbiri**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için bir hata önem derecesi raporlamaz.  
  
            -   **Bilgi**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **bilgi** hata önem derecesi raporlar.  
  
            -   **Uyarı**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **Uyarı** hata önem derecesi raporlar.  
  
            -   **Kritik**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **kritik** hata önem derecesini raporlar.  
  
            -   **Kritik ve olayla**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **kritik** hata önem derecesini raporlar. Mac istemci bilgisayarı da bu önem derecesini günlüğe kaydeder.  
  
    -   **Varlıksal** kural türü için aşağıdaki bilgileri belirtin:  
  
        -   Aşağıdakilerden birini seçin:  
  
            -   **Ayar istemci cihazlarda mevcut olmalıdır**  
  
            -   **Ayar istemci cihazlarda mevcut olmamalıdır**  
  
        -   **Raporlar Için uyumsuzluk önem derecesi**: Bu uyumluluk kuralının başarısız olması durumunda bildirilen önem derecesini belirtin. Kullanılabilen önem dereceleri aşağıdaki gibidir:  
  
            -   **Hiçbiri**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için bir hata önem derecesi raporlamaz.  
  
            -   **Bilgi**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **bilgi** hata önem derecesi raporlar.  
  
            -   **Uyarı**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **Uyarı** hata önem derecesi raporlar.  
  
            -   **Kritik**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **kritik** hata önem derecesini raporlar.  
  
            -   **Kritik ve olayla**: Bu uyumluluk kuralında başarısız olan bilgisayarlar Configuration Manager raporları için **kritik** hata önem derecesini raporlar. Mac istemci bilgisayarı da bu önem derecesini günlüğe kaydeder.  
  
        > [!NOTE]  
        >  Gösterilen seçenekler, için bir kural yapılandırmakta olduğunuz ayar türüne bağlı olarak değişiklik gösterebilir.  
  
15. **Kural oluştur** iletişim kutusunu kapatmak için **Tamam ' ı** seçin.  
  
16. **Özet** sayfasında, yeni yapılandırma öğesi için ayarları onaylayın. Ardından, Sihirbazı doldurun.  
  
**Varlıklar ve uyum** çalışma alanının **yapılandırma öğeleri** düğümündeki yeni yapılandırma öğesine bakın.  
  
Artık bu yapılandırma öğesini bir yapılandırma temeline eklemek istiyorsanız, bkz. [yapılandırma temelleri oluşturma](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="next-steps"></a>Sonraki adımlar

 [Configuration Manager istemcisiyle yönetilen cihazlar için yapılandırma öğeleri](../../compliance/deploy-use/create-configuration-items.md)
