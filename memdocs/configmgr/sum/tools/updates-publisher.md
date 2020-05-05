---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Özel güncelleştirmeleri yönetmek için System Center Updates Publisher kullanma
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717702"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Uygulama hedefi: System Center Updates Publisher*

System Center Updates Publisher (yayımcı), bağımsız yazılım satıcılarının veya iş kolu uygulaması geliştiricilerinin özel güncelleştirmeleri yönetmesine olanak tanıyan bağımsız bir araçtır. Bu özel güncelleştirme yönetimi, sürücüler ve güncelleştirme paketleri gibi bağımlılıkları olan güncelleştirmeleri içerir.

Updates Publisher 'ı kullanarak şunları yapabilirsiniz:

-   Güncelleştirmeleri dış kataloglardan (Microsoft dışı güncelleştirme katalogları) içeri aktarın.
-   Uygulanabilirlik ve dağıtım meta verileri dahil olmak üzere Güncelleştirme tanımlarını değiştirin.
-   Güncelleştirmeleri dış kataloglara dışarı aktarın.
-   Güncelleştirme sunucusunda güncelleştirmeleri yayımlayın.

Güncelleştirme sunucusunda güncelleştirmeleri yayımladıktan sonra, bu güncelleştirmeleri yönetilen cihazlarınızda algılayıp dağıtmak için Configuration Manager kullanabilirsiniz.

## <a name="workspaces"></a>Çalışma Alanları
Updates Publisher 'ı açtığınızda, varsayılan olarak *güncelleştirmeler çalışma alanının* genel bakış düğümü olur.

![Updates Publisher konsolu](media/console1.png)


Updates Publisher 'ın düzenlenmesine yardımcı olmak için dört çalışma alanı vardır.


**Güncelleştirmeler çalışma alanı:** Yazılım güncelleştirmelerini [oluşturmak](create-updates-with-updates-publisher.md) ve [yönetmek](manage-updates-with-updates-publisher.md) ve paketleri güncelleştirmek için bu çalışma alanını kullanın. Bu çalışma alanı bir yayına güncelleştirme ve paket atamayı, yayımlamayı ve başka bir Updates yayımcı deposuna vermeyi içerir.

**Yayınlar çalışma alanı:** Bu çalışma alanı, [yayınları yönettiğiniz](updates-publisher-publications.md)yerdir. Bir yayın, güncelleştirmelerin dışa ve yayımlanmasını basitleştirmek için oluşturduğunuz güncelleştirmeler grubudur.

Yayınların yönetilmesi, istemcilerinizin bir sunucuya yayımlanmasını, diğer güncelleştirmeler yayımcı yüklemeleri tarafından kullanılmak üzere güncelleştirmeleri ve paketleri dışarı aktarmak ya da bir yayının içeriğini veya ayrıntılarını değiştirmek için bir sunucuya yayımlamayı içerir.

**Kurallar çalışma alanı:** Burada, kaydedilebilecek ve ardından dağıttığınız güncelleştirmelerle kullanılabilecek [uygulanabilirlik kurallarını yönetirsiniz](updates-publisher-applicability-rules.md) . İki tür kural vardır:

-   Yüklenebilir kurallar – bu kurallar, bir istemcinin bir güncelleştirmeyi yüklemesi gerekip gerekmediğini belirlemenize yardımcı olur.
-   Yüklü kurallar – bu kurallar bir güncelleştirmenin zaten yüklü olup olmadığını doğrular.

**Kataloglar çalışma alanı:** [Yazılım güncelleştirme katalogları](updates-publisher-catalogs.md)eklemek ve yönetmek için bu çalışma alanını kullanın. Bu çalışma alanı, bu kataloglardan yazılım güncelleştirmelerinin Updates yayımcı deposuna içe aktarımını içerir.

## <a name="whats-new-in-system-center-updates-publisher"></a>System Center Updates Publisher yenilikleri

>[!NOTE] 
> System Center Updates Publisher en son sürümü 6 Kasım 2019 ' de yayımlanmıştır. Daha fazla bilgi için [yayın geçmişi](#release-history) bölümüne bakın.

Güncelleştirmelerinizi yazmanıza yardımcı olacak yeni bir yazma modu System Center Updates Publisher. Yazma modunu etkinleştirdiğinizde Başlangıç ekranına bir **Kategoriler çalışma alanı** eklenir. Yazma modu etkinken **güncelleştirmeler çalışma alanına** yeni bir **detectoid** düğmesi de eklenir.

### <a name="to-enable-authoring-mode"></a>Yazma modunu etkinleştirmek için

1. Konsolun sol üst köşesinde, **Updates Publisher** **özellikleri** sekmesine tıklayın ve ardından **Seçenekler**' i seçin.
1. **Yazma** seçeneklerine gidin.
1. **Yazma modunu etkinleştir**kutusunu işaretleyin.

![Updates Publisher için yazma modunu etkinleştir](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Kategoriler çalışma alanı hakkında

Kategoriler çalışma alanı, güncelleştirme yazarlarının birlikte bulunan güncelleştirmeleri düzenlemesini sağlar. Örneğin, bir OEM 'sanız, güncelleştirmelerinizi modeller veya ürün hatları temelinde düzenlemek isteyebilirsiniz. İki düzeyden sınırlandırdığınız için, birden çok kategori ve alt kategori tanımlayabilirsiniz, ancak genel alt kategori kullanamazsınız.

![Kategoriler çalışma alanının ekran görüntüsü](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Bir kategoriye güncelleştirme atama

Güncelleştirmeyi yazdıktan **sonra, Güncelleştir** ' i seçerek kategoriyi bir kategoriye atayabilirsiniz. Ayrıca, güncelleştirmeye sağ tıklayıp, **kategorilere ayır**' ı seçebilirsiniz.

![Bir güncelleştirmeyi kategorilere ayırma ekran görüntüsü](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>Algılayıcısı hakkında

Yazma modu etkinleştirildikten sonra güncelleştirmeler için detectoıds oluşturabilirsiniz. Uygulanabilirlik belirlenmesi için aynı kuralı (veya bir kural kümesi) kullanan birden çok güncelleştirme olduğunda, algılayıcısı yararlı olur. Bu örneklerde, bir detectoıd oluşturup bir güncelleştirme için önkoşul olarak atamalısınız. Yazılan bir güncelleştirmeye birden çok algılayıcısı atayabilirsiniz.


### <a name="create-a-detectoid"></a>Bir detectoıd oluşturma

1. **Güncelleştirmeler çalışma alanını**açın.
1. Şeritte **Detectoıd** düğmesine tıklayın.
1. Detectoıd 'nizi oluşturmak için sihirbazdaki yönergeleri izleyin.



![Algılayıcısı kullanarak önkoşulları güncelleştirme](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>Yayın geçmişi

- [2019 RTW sürüm 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Yayınlanan Kasım, 6, 2019
- [KB4462765 'Den güncelleştirme paketi sürümü 6.0.283.0](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Yayın tarihi 7 Eylül 2018.
- [2017 RTW sürüm 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Yayın tarihi 26 Mart 2018.


## <a name="next-steps"></a>Sonraki adımlar
Başlamak için ilk olarak Updates Publisher seçeneklerini [yükleyip](install-updates-publisher.md) [yapılandırın](updates-publisher-options.md) .
