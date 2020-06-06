---
title: Önbellek içeriğini yapılandırma
titleSuffix: Configuration Manager
description: Bir kullanıcı görev sırasını yüklemeden önce istemcilerin işletim sistemi dağıtım içeriğini nasıl indirebileceğinizi öğrenin.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec465f3dee33ca311aec120e74a2994a81a90ec9
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455234"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Görev dizileri için ön önbellek içeriğini yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1021244-->
Kullanılabilir görev dizileri dağıtımları için ön önbellek özelliği, istemcilerin görev dizisini yüklemeden önce ilgili içeriği indirmelerini sağlar. İstemci, [bir işletim sistemini yükseltir](create-a-task-sequence-to-upgrade-an-operating-system.md) veya [bir işletim sistemi görüntüsü yükleyen](create-a-task-sequence-to-install-an-operating-system.md)görev dizileri için içeriği önceden önbelleğe alabilir.

> [!Note]  
> Sürüm 1910 ' de, Configuration Manager Bu özelliği varsayılan olarak sunar. Sürüm 1906 veya önceki sürümlerde, bu isteğe bağlı özelliği varsayılan olarak etkinleştirmez Configuration Manager. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Örneğin, yalnızca tüm kullanıcılar için tek bir yerinde yükseltme görev sırası istediğinizde ve birçok mimarinin ve dilin olması gerekir. Önceki sürümlerde, Kullanıcı yazılım merkezinden kullanılabilir bir görev sırası dağıtımını yüklediğinde içerik indirilmek üzere başlatılır. Bu gecikme, yükleme başlatılmaya hazırlanmadan önce ek süre ekler. Görev dizisinde başvurulan tüm içerikler indirilir. Bu içerik tüm diller ve mimarilere yönelik işletim sistemi yükseltme paketini içerir. Her yükseltme paketinin boyutu kabaca 3 GB ise, toplam içerik çok büyük olur.

Ön önbellek içeriği, istemcinin yalnızca ilgili içeriği ve tüm başvurulan içeriği dağıtımı alır almaz indirmesini sağlar. Kullanıcı yazılım merkezi 'nde **yükler** ' i tıkladığında içerik hazırlayın. İçerik yerel sabit sürücüde olduğundan yükleme işlemi hızlı bir şekilde başlatılır.

Configuration Manager sürüm 1902 ve önceki sürümlerde bu davranış yalnızca *Işletim sistemi yükseltme paketi*için geçerlidir. Bu paket, eşleşen mimari veya dili belirttiğiniz tek içeriktir. Örneğin, görev dizisi birden çok sürücü paketine başvuruyorsa, istemci onları indirir. Görev sırası altyapısı, görev dizisi çalıştırıldığında, adımlar üzerinde koşulları önceden değil, değerlendirir. İstemci, hangi içeriğin ön belleğe ekleneceğini öğrenmek için paket özelliklerindeki etiketleri kullanır.

Sürüm 1906 ' den başlayarak,<!--4224642--> Aşağıdaki içerik türlerinin bant genişliği tüketimini azaltmak için ön önbelleğe alma kullanabilirsiniz:

- İşletim sistemi yükseltme paketleri
- İşletim sistemi görüntüleri
- Sürücü paketleri
- Paketler

## <a name="configure-pre-caching"></a>Ön önbelleğe alma yapılandırma

Ön önbellek özelliğini yapılandırmak için üç adım vardır:

1. [Paketleri oluşturma ve yapılandırma](#bkmk_createpkg)
2. [Koşullu adımlarla bir görev dizisi oluşturma](#bkmk_createts)
3. [Görev sırasını dağıtın ve önceden önbelleğe almayı etkinleştirin](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a>1. paketleri oluşturma ve yapılandırma

İstemci, ön belleğe alma sırasında hangi içeriğin indirileceğini belirleyen paketlerin özniteliklerini değerlendirir.  

#### <a name="os-upgrade-package"></a>İşletim sistemi yükseltme paketi

Belirli mimariler ve diller için [Işletim sistemi yükseltme paketleri](../get-started/manage-operating-system-upgrade-packages.md) oluşturun. Özelliklerinin **veri kaynağı** sekmesinde **mimariyi** ve **dili** belirtin.

#### <a name="os-image"></a>İşletim sistemi görüntüsü

Belirli mimariler ve diller için [Işletim sistemi görüntüleri](../get-started/manage-operating-system-images.md) oluşturun. Özelliklerinin **veri kaynağı** sekmesinde **mimariyi** ve **dili** belirtin.

#### <a name="driver-package"></a>Sürücü paketi

Belirli donanım modelleri için [sürücü paketleri](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages) oluşturun. **Modeli** , özelliklerinin **genel** sekmesinde belirtin.

Ön belleğe alma sırasında indirilen sürücü paketini öğrenmek için, istemci modeli **Win32_ComputerSystemProduct** WMI sınıfının **Name** özelliğine göre değerlendirir.

> [!TIP]
> Asıl sorgu `LIKE` joker karakter içeren bir ifade kullanır: `select * from win32_computersystemproduct where name like "%yourstring%"` . Örneğin, `Surface` model olarak belirtirseniz, sorgu bu dizeyi içeren tüm modellerle eşleşir.<!-- 6315551 -->

#### <a name="package"></a>Paket

Belirli mimariler ve diller için [paketler](../../apps/deploy-use/packages-and-programs.md) oluşturun. Özelliklerinin **genel** sekmesinde **mimariyi** ve **dili** belirtin.


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a>2. bir görev dizisi oluşturun

Farklı diller ve mimarilere yönelik koşullu adımları veya sürücü paketleri için farklı donanım modellerini içeren bir görev dizisi oluşturun.

|İçerik|Adım|
|---------|---------|
|İşletim sistemi yükseltme paketi|[İşletim sistemini yükselt](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|İşletim sistemi görüntüsü|[İşletim sistemi görüntüsünü Uygula](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|Sürücü paketi|[Sürücü Paketini Uygula](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|Paket|[Paketi Yükle](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

Örneğin, aşağıdaki **yükseltme işletim sistemi** adımı İngilizce sürümünü kullanır:  

![TRK, DEU ve JPN için birden çok yükseltme işletim sistemi adımını gösteren görev dizisi Düzenleyicisi](../media/precacheproperties2.png)

![Yerel ayar ve OSArchitecture için WMI WQL sorgusunu görüntüleyen görev sırası Düzenleyicisi, Seçenekler sekmesi](../media/precacheoptions2.png)  

> [!Tip]
> Ingilizce (Birleşik Devletler) işletim sistemi ve 64-bit mimarisi için aşağıdaki WMI sorgusu önerilir:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> Önce **Işletim sistemi dil** koşulunu seçerek dili ekleyin. Ardından, mimari yan tümcesini içerecek şekilde WMI sorgusunu düzenleyin.

### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a>3. görev dizisini dağıtma

[Görev sırasını dağıtın](deploy-a-task-sequence.md). Ön önbellek özelliği için aşağıdaki ayarları yapılandırın:  

- **Genel** sekmesinde, **Bu görev dizisinin içeriğini önceden indir**' i seçin.  

- **Dağıtım ayarları** sekmesinde, görev dizisini **kullanılabilir**olarak yapılandırın.  

- **Zamanlama** sekmesinde, ayar için şu anda seçili zamanı seçin, **Bu dağıtımın ne zaman kullanılabilir olacağını zamanlayın**. İstemci, dağıtımın kullanılabilir saatinde önceden önbelleğe alma içeriği başlatır. Hedeflenen bir istemci bu ilkeyi aldığında, kullanılabilir saat geçmişte olur, bu nedenle ön önbellek indirme hemen başlatılır. İstemci bu ilkeyi alırsa, ancak kullanılabilir saat gelecekte ise, istemci, kullanılabilir saat gerçekleşene kadar ön belleğe alma işlemini başlatamaz.  

- **Dağıtım noktaları** sekmesinde, **dağıtım seçenekleri** ayarlarını yapılandırın. Bir Kullanıcı yüklemeyi başlamadan önce içerik önceden önbelleğe alınmamışsa, istemci bu ayarları kullanır.  

    > [!Important]  
    > İşletim sistemi görüntüsü yükleyen bir görev sırası için, **çalışan görev dizisi için gerektiğinde içeriği yerel olarak indirmek**için dağıtım seçeneğini kullanmayın. Görev dizisi, işletim sistemi görüntüsünü uygulamadan önce diski temizler, istemci önbelleğini kaldırır. İçerik kaybolduğundan, görev sırası başarısız olur.<!-- SCCMDocs-PR #1338 --> Bu dağıtım seçenekleri, dağıtım için belirlediğiniz diğer seçeneklere göre dinamiktir. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md#bkmk_deploy-options).<!-- MEMDocs#328, SCCMDocs#2114 -->

## <a name="user-experience"></a>Kullanıcı deneyimi

- İstemci dağıtım ilkesini aldığında, dağıtımın kullanılabilir zamanından sonra içeriği önceden önbelleğe alma başlar. Bu içerik, tüm başvurulan paketleri içerir, ancak yalnızca paketteki mimari ve dil öznitelikleriyle eşleşen işletim sistemi yükseltme paketidir.  

- İstemci, dağıtımı kullanıcılar için kullanılabilir hale geldiğinde, kullanıcıları yeni dağıtım hakkında bilgilendirmek için bir bildirim görüntülenir. Artık görev dizisi yazılım merkezi 'nde görünür. Kullanıcı yazılım merkezi 'ne gidebilir ve yüklemeyi başlatmak için **yükleme** ' ye tıklayabilir.  

- Kullanıcı görev sırasını yüklediğinde istemci içeriği tam olarak önceden önbelleğe mamışsa, istemci, dağıtımın **dağıtım seçeneği** sekmesinde belirttiğiniz ayarları kullanır.  

## <a name="see-also"></a>Ayrıca bkz.

- [İşletim sistemini yükseltmek için görev dizisi oluşturma](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Windows 'un en son sürümüne yükseltilme senaryosu](upgrade-windows-to-the-latest-version.md)
