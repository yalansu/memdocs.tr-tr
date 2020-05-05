---
title: Güncelleştirmeleri yönetme
titleSuffix: Configuration Manager
description: Dağıttığınız ve System Center Updates Publisher ile oluşturduğunuz vapatları yönetme
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2cb1d1547c23357adbaa26e649e4e22a78e0f39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717814"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Güncelleştirmeler Yayımcısındaki yazılım güncelleştirmelerini yönetme

*Uygulama hedefi: System Center Updates Publisher*     

System Center Updates Publisher ' de, depoya aktardığınız yazılım güncelleştirmelerini ve paketleri yönetmek için **güncelleştirmeler çalışma alanını** kullanırsınız.  

Yönetim görevleri, güncelleştirmeleri ve paketleri çoğaltma, düzenlemenin ve süresi dolan veya yeniden etkinleştirme ve yayınlar için güncelleştirmeler ve paket atama içerir. Ayrıca, diğer Updates Publisher yüklemeleri ile kullanmak üzere özel katalogları dışarı aktarabilirsiniz.

Yönetebileceğiniz güncelleştirmeleri almak için:
-  Updates Publisher yüklemenize [bir güncelleştirme kataloğu ekleyin](updates-publisher-catalogs.md#add-software-update-catalogs)
-  Bu katalogdan güncelleştirmeleri deponuza [aktarın](updates-publisher-catalogs.md#import-updates) .

[Kendi güncelleştirmelerinizi de oluşturabilirsiniz](create-updates-with-updates-publisher.md).



## <a name="create-a-duplicate-of-an-update"></a>Güncelleştirme yinelemesi oluşturma
Deponuzdaki güncelleştirmelerin yinelemelerini veya kopyalarını oluşturabilirsiniz. Ardından, özgün güncelleştirmeyi değiştirmek yerine kopyayı değiştirebilirsiniz. Güncelleştirme paketlerinin kopyalarını oluşturamazsınız.

Bir kopya oluşturmak için **güncelleştirmeler çalışma alanında**bir güncelleştirme seçin ve ardından **Çoğalt**' ı seçin. Güncelleştirmenin kopyası, güncelleştirme çalışma alanındaki adına eklenen *kopyasıyla* aynı konumda görüntülenir.

Oluşturduğunuz yeni bir kopya, **süresi dolmamış**durumuna sahiptir, aksi takdirde orijinal ayarlarını korur.

## <a name="edit-updates-and-bundles"></a>Güncelleştirmeleri ve paketleri Düzenle
Bunları değiştirmek için deponuzda olan güncelleştirmeler ve paketleri seçebilirsiniz.

**Güncelleştirmeler çalışma alanında** bir güncelleştirme veya paket seçin ve ardından **giriş** sekmesinden **Düzenle** ' yi seçerek düzenleme sihirbazını açın. Güncelleştirmeler ve paketlerde her biri, [güncelleştirme oluşturma](create-updates-with-updates-publisher.md#use-the-create-update-wizard) veya [paket oluşturma](create-updates-with-updates-publisher.md#use-the-create-bundle-wizard) sihirbazları ile aynı seçenekleri sunan ayrı ancak yakından ilgili sihirbazlara sahiptir.

' İ düzenlediğinizde, güncelleştirme veya paket hakkındaki tüm kullanılabilir ayrıntıları ortamınızda kullanılabilmesi için değiştirebilirsiniz. Örneğin, uygulanabilirlik veya öncelik kurallarını düzenleyebilir veya dili değiştirebilirsiniz. Ayrıca, ürün ve satıcıyı değiştirerek, güncelleştirmeyi veya paketini kendi kullanım için güncelleştirmek üzere özel bir klasöre taşıyabilirsiniz.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Bir yayına güncelleştirmeler ve paketleri atama
Güncelleştirmeler **çalışma alanında** güncelleştirmeler ve paketseç ' i seçin ve ardından bir yayına eklemek Için şeridin **giriş** sekmesinden **ata** ' yı seçin. Bu, **yazılım güncelleştirmelerini atama** Sihirbazı 'nı başlatır.
-  Güncelleştirmeleri ve paketleri tek bir görev olarak seçme ve yayımlama hakkında bilgi için bkz. [güncelleştirmeleri ve paketleri yayımlama](#publish-updates-and-bundles-from-the-updates-workspace) .
-  Güncelleştirme gruplarını ve paketleri tek bir nesne olarak yönetme hakkında bilgi için bkz. [yayınları yönetme](updates-publisher-publications.md) . Bir yayına güncelleştirmeler atadıktan sonra, bu yayını yönetebilirsiniz ve bu da, atanan tüm güncelleştirmeleri içerir.

Bir yayına güncelleştirmeler atadığınızda:

-   Aynı yayında, zaman aşımına uğradı ve olmayan güncelleştirmeleri ve paketleri dahil edebilirsiniz.

-   Yayın türünü belirtin:

    -   **Tam içerik** – bu, güncelleştirmenin tam Içeriğini WSUS sunucunuza yayımlar. Bu meta verileri ve güncelleştirme ikili dosyalarını içerir.

    -   **Yalnızca meta veriler** – bu yalnızca meta verileri yayımlar; güncelleştirme ikilileri yayımlanmaz. Uyumluluk verilerini toplamak istediğinizde bu seçeneği belirleyebilirsiniz.

    -   **Otomatik** – Bu mod yalnızca güncelleştirmeler yayımcısını Configuration Manager 'e bağladığınızda kullanılabilir ( [ConfigMgr sunucu](updates-publisher-options.md#configmgr-server) seçeneğine bakın.)

    Bu tür ile güncelleştirmelerin veya paketgüncelleştirmelerinin tam içerik veya yalnızca meta veri ile yayımlanması gerekip gerekmediğini öğrenmek için yayımcı sorgularını güncelleştirir Configuration Manager. Güncelleştirme için tam içerik yalnızca bu güncelleştirme, Updates Publisher seçeneklerinin **ConfigMgr sunucu** sayfasında belirtilen **istenen istemci sayısı eşiğini** ve **paket kaynak boyutu eşiğini** karşılıyorsa yayımlanır.

-   Yayın seçin:

    -   Kullanmak istediğiniz bir yayını zaten oluşturduysanız **mevcut yayınlara yazılım güncelleştirmesi ata** ' yı kullanın. En az bir yayın mevcut olana kadar bu seçenek kullanılamaz.

    -   Uygun bir yayınınız yoksa, **yazılım güncelleştirmesini yeni bir yayına ata** ' yı kullanın. Bu, belirttiğiniz adla yeni bir yayın oluşturur.

Bir yayına güncelleştirmeler atadıktan sonra yayın **çalışma alanını** kullanarak yayını bir grup olarak [yayımlayabilir](updates-publisher-publications.md#publish-publications) veya [dışarı aktarabilirsiniz](updates-publisher-publications.md#export-a-publication) .

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Güncelleştirmeler çalışma alanından güncelleştirmeleri ve paketleri yayımlama
Güncelleştirmeleri ve paketleri yayımladığınızda, Updates Publisher bu güncelleştirmeler ve paketleri (meta veriler) ve muhtemelen güncelleştirmeler için ikili dosyalar (tam içerik) ile cihazlara dağıtım için bir güncelleştirme sunucusuna bilgi ekler.

Yayımlama seçeneğine sahip olmadan önce, Updates Publisher için [güncelleştirme sunucusu](updates-publisher-options.md#update-server) seçeneğini yapılandırmanız gerekir. Bu yapılandırma seçeneğini açmak için **güncelleştirmeler çalışma alanına** &gt; **Genel Bakış ' a** gidin ve **WSUS ve imzalama sertifikasını Yapılandır** ' ı seçin. Updates Publisher seçeneklerinde sunucu güncelleştirme sayfasına da gidebilirsiniz.

Güncelleştirmeleri ve paketleri yayımlamanın iki yolu vardır:
-   Doğrudan güncelleştirmeler çalışma alanından. ( *Güncelleştirmeleri ve paketleri yayımlamak için*aşağıdaki yordama bakın.)
-   Yayınlar çalışma alanından bir [yayın](updates-publisher-publications.md#publish-publications) olarak.  

> [!NOTE]   
> Updates Publisher, yalnızca 375 megabayt (MB) veya daha az boyut olan güncelleştirmeleri yayımlayabilir.

### <a name="to-publish-updates-and-bundles"></a>Güncelleştirmeleri ve paketleri yayımlamak için
1.  **Güncelleştirmeler çalışma alanı** ' na gidin ve yayımlamak istediğiniz bir veya daha fazla güncelleştirme ve paket seçin. Ardından şeridin **giriş** sekmesinde **Yayımla** ' yı seçin.

2.  **Yayımla** sihirbazının **Seç** sayfasında, güncelleştirmeleri nasıl yayımlamak istediğinizi seçin. Seçenekler, [güncelleştirme atama](#assign-updates-and-bundles-to-a-publication)ile aynıdır: **tam içerik**, **yalnızca meta veriler**veya **Otomatik**.

    Tüm güncelleştirmeleri yeni bir yayımlama sertifikasıyla imzalamayı da tercih edebilirsiniz.

3.  Sihirbazı tamamlayın.

Yayımlama başarısız olursa, daha fazla bilgi sağlayabilen UpdatesPublisher. log dosyasına bir bağlantı sunulur.

## <a name="export-updates"></a>Güncelleştirmeleri dışarı aktar
Özel bir güncelleştirme kataloğu oluşturmak için Updates Publisher deponuzdan güncelleştirmeleri ve paketleri dışarı aktarabilirsiniz. Daha sonra, bu kataloğu daha sonra bir Updates Publisher örneğine [ekleyip](updates-publisher-catalogs.md#add-software-update-catalogs) [içeri aktarabilirsiniz](updates-publisher-catalogs.md#import-updates) . ( [Güncelleştirmeleri bir yayın olarak da dışarı aktarabilirsiniz](updates-publisher-publications.md#export-a-publication).)

Doğrudan dışarı aktarmak için **güncelleştirmeler çalışma alanı** > **tüm yazılım güncelleştirmeleri** ' ne gidin ve bir veya daha fazla güncelleştirme ve paket seçin. Bir satıcıyı veya ürün klasörünü dışarı veremezsiniz, ancak bir klasörü seçip dışarı aktarma için bu klasördeki güncelleştirmeleri seçebilirsiniz.

Bir veya daha fazla güncelleştirme seçiliyken, şeridin **giriş** sekmesinden **dışarı aktar** ' ı seçin ve ardından Katalog dışa aktarma için bir yol ve dosya adı girin.

Bağımlı yazılım güncelleştirmelerini dışarı aktarma (dahil) seçeneğine sahip olursunuz.

## <a name="delete-updates-and-bundles"></a>Güncelleştirmeleri ve paketleri silme
Güncelleştirmeleri Updates Publisher deposundan kaldırmak için güncelleştirmeleri ve güncelleştirme paketlerini silebilirsiniz.

**Güncelleştirmeler çalışma alanı** > **tüm yazılım güncelleştirmeleri** ' ne gidin ve bir veya daha fazla tek güncelleştirme seçin. Ardından şeridin **giriş** sekmesinden **Sil** ' i seçin.

-   Seçiminiz yalnızca yayınlanmamış olan veya henüz bitmiş olan güncelleştirmeler veya paketleri içeriyorsa, silinmeden önce silme işlemini onaylamanız istenir.

-   Seçiminiz yayımlanmış olan ve henüz süresi dolmayan bir güncelleştirme veya paket içeriyorsa, size bir uyarı verilir. Bu güncelleştirmeleri [sona ermeli](updates-publisher-publications.md#expire-or-reactivate-updates-and-bundles) ve sonra depodan silmeden önce bu değişikliği yayımlamanız gerekir.  

Bir satıcıdan bir güncelleştirmeyi veya paketi siler ve ardından bu kataloğu yeniden içeri aktarırsanız, bu güncelleştirme deponuza geri yüklenir.

## <a name="manage-vendor-and-product-folders"></a>Satıcı ve ürün klasörlerini yönetme
Güncelleştirme içeri aktardığınız veya oluşturduğunuz her satıcı için satıcıların ve ürünlerin listesini görüntülemek için **güncelleştirmeler çalışma alanına** > **genel bakış** > **tüm yazılım güncelleştirmeleri**sayfasına gidin.

Yazılım güncelleştirmesi veya paketi içeri veya paket oluşturmak için sihirbaz kullandığınızda, satıcılar ve ürünler için klasörler güncelleştirmeler yayımcısı tarafından otomatik olarak oluşturulur. Ayrıca, bu klasörleri el ile de oluşturabilirsiniz.

-   Bir satıcı klasörü oluşturmak için, **güncelleştirmeler çalışma alanının**gezinti bölmesinde, **tüm yazılım güncelleştirmeleri**' ne sağ tıklayın ve ardından **satıcı oluştur**' u seçin.

-   Bir satıcı klasörü altında bir ürün klasörü oluşturmak için satıcı klasörüne sağ tıklayın ve **ürün oluştur**' u seçin.

Klasör oluşturmaya ek olarak, deponuzdaki herhangi bir satıcıyı veya ürün klasörünü yeniden adlandırabilir veya silebilirsiniz. Bunu yapmak için, klasöre sağ tıklayın ve istediğiniz seçeneği belirleyin, **yeniden adlandırın** veya **silin**. Bir klasörü silmek, bu klasörde ve ürün klasörlerindeki tüm güncelleştirmeleri ve paketleri Updates Publisher deposundan kaldırır.

Güncelleştirmeleri, oluşturduğunuz klasörlere dahil olmak üzere satıcı ve ürün klasörleri arasında taşıyabilirsiniz. Bir güncelleştirmeyi veya paketi yeni bir klasöre taşımak için, güncelleştirmeyi veya paketi seçmeniz ve sonra **düzenlemeniz** gerekir. Ardından, güncelleştirme düzenleme sihirbazının **bilgiler** sayfasında satıcıyı ve ürünü yeniden atayabilirsiniz. **Güncelleştirme düzenleme** Sihirbazı tamamlandığında, değişiklik uygulanır ve güncelleştirme yeni klasöre gider.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Bir güncelleştirmenin veya paketin XML 'sini görüntüleme
**Güncelleştirmeler çalışma alanında** tek bir güncelleştirme veya paket seçebilir ve sonra bu güncelleştirmenin XML yapısını görüntülemek için XML 'yi **görüntüle** ' yi seçebilirsiniz. XML yapısını doğrudan düzenleme seçeneği yoktur.
