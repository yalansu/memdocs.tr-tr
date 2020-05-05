---
title: Uygulanabilirlik kuralları
titleSuffix: Configuration Manager
description: System Center Updates Publisher için uygulanabilirlik kurallarını yönet
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53a3aabfe65449723bdb6076486128b76a1a830c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078439"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Güncelleştirmeler Yayımcısındaki uygulanabilirlik kurallarını yönetme

*Uygulama hedefi: System Center Updates Publisher*

Updates Publisher ile uygulanabilirlik kuralları, cihazın bir güncelleştirmeyi yükleyebilmesi için karşılanması gereken gereksinimleri tanımlar. Kurallar, bilgisayarda yüklü bir güncelleştirme olup olmadığını belirlemede de kullanılır. Birden çok bölümden karmaşık olan uygulanabilirlik kuralı, kural kümesi olarak adlandırılır.

Güncelleştirme paketleri uygulanabilirlik kurallarını kullanmaz.

## <a name="overview-of-applicability-rules"></a>Uygulanabilirlik kurallarına genel bakış
Uygulanabilirlik kurallarını **kurallar çalışma**alanından yönetirsiniz. Bir kural oluşturduğunuzda bir veya daha fazla koşul belirtirsiniz. Birden çok koşul belirtildiğinde, aralarında sıralı olarak değerlendirilecek veya mantıksal **ve** **ya da deyimlerle** birleştirilecek şekilde koşullar arasındaki ilişkileri yapılandırabilirsiniz.

Örneğin, aşağıdaki üç kural içeren bir kural kümesidir. İlk kural, *Dosyam* dosyasının var olduğunu ve ikinci ve üçüncü kuralların, Windows işletim sistemi dilinin Ingilizce veya Japonca olduğunu doğrular.

``` Example
And  
  File '\[PROGRAM\_FILES\] \\Microsoft\\MyFile' exists  
  Or  
    Windows Language is English
    Windows Language is Japanese
```

Tüm güncelleştirmeler en az bir uygulanabilirlik kuralı gerektirir. İçeri aktardığınız güncelleştirmeler zaten uygulanabilirlik kuralları uygulanmış ve kendi güncelleştirmelerinizi oluşturduğunuzda, bunlara bir veya daha fazla kural eklemeniz gerekir. Updates Publisher 'daki herhangi bir güncelleştirmenin kurallarını değiştirebilir ve genişletebilirsiniz.

Oluşturduğunuz kuralları görüntülemek için, **kurallar çalışma alanında**, **kaydedilmiş kurallar** listesinden bir kural seçin. Bu kurala yönelik ayrı koşullar ve mantıksal işlemler, konsolunun **uygulanabilirlik kuralları** bölmesinde görüntülenir. İçeri aktardığınız güncelleştirmelerin kuralları yalnızca bu güncelleştirmeyi düzenlediğinizde görüntülenebilir ve değiştirilebilir.

Updates Publisher 'da iki konumda kurallar oluşturabilirsiniz:

-   **Kurallar çalışma alanında,** daha sonra kullanabileceğiniz kural kümelerini oluşturup **kaydedersiniz** . Bir güncelleştirme düzenlenirken veya oluştururken **kural türü**olarak **kaydedilmiş kural** ' ı seçebilir ve ardından önceden oluşturulmuş kural kümelerinizin listesinden seçim yapabilirsiniz.

-   Ayrıca, bir güncelleştirmeyi oluşturduğunuz veya düzenlediğiniz sırada yeni kurallar da oluşturabilirsiniz. Bu şekilde oluşturduğunuz kurallar ileride kullanılmak üzere kaydedilmez.

## <a name="create-applicability-rule"></a>Uygulanabilirlik kuralı oluştur
Aşağıdaki bilgiler, [güncelleştirme oluşturma Sihirbazı](create-updates-with-updates-publisher.md#use-the-create-update-wizard)içinden nasıl kural oluşturacağınız konusunda benzerdir. Ancak sihirbazın aksine, kural kümelerinizi daha sonra kullanmak üzere kaydetme seçeneğiniz vardır.

1. **Kural oluşturma** Sihirbazı 'nı açmak Için **kurallar çalışma alanında** **Oluştur** ' u seçin.

2. Kural için bir ad belirtin ve ardından yeni kural ![](media/newrule.png)' a tıklayın. Bu, kuralları yapılandırabileceğiniz **uygulanabilirlik kuralı** sayfasını açar.

3. **Kural türü** için aşağıdakilerden birini seçin. Yapılandırmanız gereken seçenekler her bir tür için farklılık gösterir:

   - **Dosya** – Bu güncelleştirme uygulanmadan önce, bir cihazın belirttiğiniz bir veya daha fazla ölçütü karşılayan bir dosyaya sahip bir dosyanın olmasını gerektirmek için bu kuralı kullanın.

   - **Kayıt defteri –** Bir cihaz bu güncelleştirmeyi yüklemeye uygun olmadan önce mevcut olması gereken kayıt defteri ayrıntılarını belirtmek için bu türü kullanın.

   - **Sistem –** Bu kural, uygulanabilirliği belirlemede sistem ayrıntılarını kullanır. Cihazların işletim sistemini tanımlamak için bir Windows sürümü, Windows dili, işlemci mimarisi tanımlamayı veya bir WMI sorgusu belirtmeyi seçebilirsiniz.

   - **Windows Installer –** Yüklü olan uygulanabilirliği öğrenmek için bu kural türünü kullanın. MSI veya Windows Installer Patch (. MSP). Ayrıca, gereksinimin bir parçası olarak belirli bileşenlerin veya özelliklerin yüklenip yüklenmediğini da belirleyebilirsiniz.

     > [!IMPORTANT]   
     > Yönetilen deıces Windows Update Aracısı, Kullanıcı başına yüklenen Windows yükleme paketlerini algılayamaz. Bu kural türünü kullandığınızda, Windows Installer paketinin Kullanıcı başına veya sistem başına olarak düzgün bir şekilde algılanabilmesi için dosya sürümleri veya kayıt defteri anahtarı değerleri gibi ek uygulanabilirlik kurallarını yapılandırın.

   - **Kaydedilen kural –** Bu seçenek, daha önce yapılandırdığınız ve kaydettiğiniz kuralları bulmanızı ve kullanmanızı sağlar.

4. İstediğiniz gibi ek kurallar eklemeye ve yapılandırmaya devam edin.

5. Daha karmaşık önkoşul denetimleri oluşturmak üzere farklı kuralları sıralamak ve gruplandırmak için mantıksal işlem düğmelerini kullanın.

6. Kural kümesi tamamlandığında, kaydetmek için **Tamam** ' ı tıklatın. Kural kümesi şimdi **kaydedilmiş kurallar** listesinde görünür.

## <a name="edit-applicability-rule-sets"></a>Uygulanabilirlik kuralı kümelerini Düzenle
Bir uygulanabilirlik kuralını düzenlemek için, **kurallar çalışma** alanında, **kaydedilmiş kurallar** listesinde kaydedilen herhangi bir kuralı seçin ve şeritten **Düzenle** ' yi seçin. Bu, **kural düzenleme** Sihirbazı ' nı açar.

**Kural düzenleme** Sihirbazı, kural kümesi için geçerli kuralları görüntüler. Kuralları, yeni kurallar oluşturmak için **kural oluşturma** Sihirbazı 'nı kullandığınız şekilde düzenleyebilirsiniz. Kural kümesini yeniden adlandırmak, kuralları silmek, kuralları ve ilişkileri yeniden sıralamak veya yeni kurallar eklemek için bu sihirbazı kullanabilirsiniz.

Değişiklik yaptıktan sonra, değişiklikleri kaydetmek ve Sihirbazı kapatmak için **Tamam** ' ı seçin.

Kural Sihirbazı 'nı kullanma hakkında daha fazla bilgi **için bkz.** [güncelleştirme oluşturma sihirbazının](create-updates-with-updates-publisher.md#use-the-create-update-wizard)uygulanabilirlik sayfası.

## <a name="delete-applicability-rules"></a>Uygulanabilirlik kurallarını Sil
Kaydedilmiş bir uygulanabilirlik kuralını silmek için, **kurallar çalışma alanında** , **kaydedilmiş kurallarım** listesinden kural veya kural kümesini seçin ve ardından şeritten **Sil** ' i seçin. Bu, kaydedilen kuralı veya kural kümesini güncelleştirmeler yayımcısından kaldırır.

Belirli bir güncelleştirmedeki bir kuralı silmek için, [güncelleştirmeyi düzenlemeniz](manage-updates-with-updates-publisher.md#edit-updates-and-bundles)gerekir.
