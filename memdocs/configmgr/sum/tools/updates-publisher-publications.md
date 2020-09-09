---
title: Yayınları yönetme
titleSuffix: Configuration Manager
description: Yazılım güncelleştirme gruplarını System Center Updates Publisher yayın olarak yönetme
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e3dedef9ffe785ce7127fc371030cfd990d70e38
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608378"
---
# <a name="manage-publications-in-updates-publisher"></a>Updates Publisher 'da yayınları yönetme

*Uygulama hedefi: System Center Updates Publisher*

Güncelleştirme gruplarını ve paketleri tek bir nesne olarak yönetmek için yayınları kullanabilirsiniz. Bu, güncelleştirmelerin bir yönetim sunucusuna yayımlanmasını ve yayının başka bir Updates Publisher yüklemesi ile kullanılmak üzere bir grup olarak verilmesini içerir.

## <a name="create-publications"></a>Yayınlar oluşturun
Yayınlar iki şekilde oluşturulur:

-   Güncelleştirmeler **çalışma alanındaki**güncelleştirmeleri ve paketleri yönetirken, bunları o anda oluşturulan yeni bir yayına [atayabilirsiniz](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) .

-   **Yayınlar çalışma alanında,** şeridin **yayın** sekmesinde **Oluştur** düğmesini kullanabilirsiniz. Bu yöntem, ileride kullanılmak üzere bir yayın oluşturmanıza olanak sağlar. Daha sonra, güncelleştirmeleri atadığınızda bu yayını kullanabilirsiniz.

## <a name="rename-a-publication"></a>Yayını yeniden adlandırma
Bir yayını yeniden adlandırmak için **yayınlar çalışma alanının**içinden yayını seçin ve ardından şeridin **yayın** sekmesinde **Düzenle**' yi seçin.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Yayındaki güncelleştirmelerin yayın türünü değiştirme
Yayın **çalışma**alanından, bir yayına atanan güncelleştirme ve paket **yayın türünü** değiştirebilirsiniz.

1. Değiştirmek istediğiniz güncelleştirmeleri içeren yayını seçin ve ardından **tüm &lt; yayın adı> üye güncelleştirmeleri** listesinden bir veya daha fazla güncelleştirme ya da paket seçin.

2. Ardından, **giriş** sekmesinde, aşağıdaki seçeneklerden birini belirleyin. Kullanılabilir seçenekler, seçtiğiniz güncelleştirmelerin yayın türüne bağlıdır.

   -   **Automatic**
   -   **Tam Içerik**
   -   **Yalnızca meta veriler**

Değişiklik yaptıktan sonra, yeni değerleri görmek için yayın görünümünü yenilemeniz gerekebilir.

Farklı yayın türleri hakkında daha fazla bilgi için bkz. [bir yayına güncelleştirme ve paket atama](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Bir paketin yayın türünü ayarladığınızda, bu paketteki tüm yazılım güncelleştirmeleri o paketin yayın türüyle yayımlanır.

## <a name="remove-updates-from-a-publication"></a>Güncelleştirmeleri yayından kaldırma
Bir yayından güncelleştirmeleri veya paketleri kaldırmak için **yayınlar çalışma alanında** , değiştirmek istediğiniz yayını seçin ve ardından kaldırmak istediğiniz güncelleştirmeleri ve paketleri seçin. Ardından, şeridin **giriş** sekmesinde **Kaldır**' ı seçin.

Güncelleştirmeler bir yayından kaldırıldıktan sonra güncelleştirmeler yayımcı deposunda kullanılabilir kalır.

## <a name="publish-publications"></a>Yayınları Yayımla
Güncelleştirmeleri ve paketleri yayımladığınızda, Updates Publisher bu güncelleştirmeler ve paketleri (meta veriler) ve muhtemelen güncelleştirmeler için ikili dosyalar (tam içerik) ile cihazlara dağıtım için bir güncelleştirme sunucusuna bilgi ekler.

Yayımlama seçeneğine sahip olmadan önce, Updates Publisher için [güncelleştirme sunucusu](updates-publisher-options.md#update-server) seçeneğini yapılandırmanız gerekir. Bu yapılandırma seçeneğini açmak için **güncelleştirmeler çalışma alanına** &gt; **Genel Bakış ' a** gidin ve **WSUS ve imzalama sertifikasını Yapılandır** ' ı seçin. Updates Publisher seçeneklerinde sunucu güncelleştirme sayfasına da gidebilirsiniz.

> [!NOTE]   
> Updates Publisher, yalnızca 375 megabayt (MB) veya daha az boyut olan güncelleştirmeleri yayımlayabilir.

### <a name="to-publish-a-publication"></a>Bir yayını yayımlamak için

1. **Yayınlar çalışma alanına**gidin ve ardından yayımlamak veya dışarı aktarmak istediğiniz güncelleştirme grubunu ve paketleri içeren bir yayını seçin. Ardından şeridin **giriş** sekmesinde **Yayımla** ' yı seçin.

2. **Yayımla** sihirbazının **Seç** sayfasında, tüm güncelleştirmeleri yeni bir yayımlama sertifikasıyla imzalamayı tercih edebilirsiniz, ancak yayın türünü değiştiremezsiniz.

3. Sihirbazı tamamlayın.

   Yayımlama başarısız olursa, daha fazla bilgi sağlayabilen UpdatesPublisher. log dosyasına bir bağlantı sunulur.

## <a name="export-a-publication"></a>Yayını dışarı aktarma
Updates Publisher deponuzdan bir yayını dışarı aktarabilirsiniz. Bunun yapılması, bu yayına atanan güncelleştirmeleri ve paketleri dışa aktarır ve bir güncelleştirme kataloğu oluşturur. Daha sonra bu kataloğu daha sonra bir Updates Publisher örneğine [ekleyip](updates-publisher-catalogs.md#add-software-update-catalogs) [içeri aktarabilirsiniz](updates-publisher-catalogs.md#import-updates) . Ayrıca, bir yayının parçası olmayan [güncelleştirmeleri dışarı aktarabilirsiniz](manage-updates-with-updates-publisher.md#export-updates) .

Bir yayını dışarı aktarmak için **yayınlar çalışma alanına** gidin ve dışarı aktarmak istediğiniz güncelleştirmeleri içeren yayını seçin. Tek seferde yalnızca bir yayın seçebilirsiniz.

Yayın seçili olduğunda, şeridin **giriş** sekmesinden **dışarı aktar** ' ı seçin ve ardından Katalog dışa aktarma için bir yol ve dosya adı belirtin.

Ayrıca, dışa aktarma kapsamında bağımlı yazılım güncelleştirmelerini dışarı aktarma (dahil etme) seçeneğiniz de vardır.

## <a name="delete-a-publication"></a>Yayını silme
Bir yayını silmek için **yayınlar çalışma alanını**Yayımla ' yı seçin ve ardından şeridin **yayın** sekmesinden **Sil** ' i seçin.

Yayın, güncelleştirmeler yayımcısından kaldırıldıktan sonra, yayındaki güncelleştirmeler Updates Publisher deposunda kullanılabilir kalır.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Güncelleştirmeleri ve paketleri sona erdirin veya yeniden etkinleştirin
Güncelleştirmeleri ve paketleri seçip yeniden etkinleştirmek için **güncelleştirmeler çalışma alanını** kullanabilirsiniz. Güncellemeleri ve paketleri seçtiğiniz kadar zaman sona erdirebilirsiniz ve yeniden etkinleştirebilirsiniz.

-   **Güncelleştirmeler veya paketlerindeki süre sonu için**, güncelleştirmeler çalışma alanında, kullanım süreleri dolan bir veya daha fazla güncelleştirme ya da paket seçin ve ardından **giriş** sekmesinden **süre sonu** ' nu seçin. Güncelleştirmeyi veya paketi Configuration Manager için zaman aşımına erene kadar yeniden etkinleştirebilirsiniz.

    Configuration Manager bir özel güncelleştirmeyi veya paketi kaldırabilmeniz için önce onu sona erdirmeli ve sonra bu süre dolan durumu Configuration Manager yayımlamanız gerekir. Configuration Manager güncelleştirmeler veya paketlerindeki süre dolduktan sonra, güncelleştirmeyi veya paketi artık dağıtamazsınız veya yeniden etkinleştiremezsiniz.

-   **Güncelleştirmeleri veya paketleri yeniden etkinleştirmek için**, güncelleştirmeler çalışma alanında, zaman aşımına uğradı bir veya daha fazla güncelleştirme seçin ve ardından şeridin **giriş** sekmesinden **yeniden etkinleştir** ' i seçin. Süre dolma tarihi daha önce Configuration Manager olarak yayınlandıysa, yeniden etkinleştiremezsiniz.
