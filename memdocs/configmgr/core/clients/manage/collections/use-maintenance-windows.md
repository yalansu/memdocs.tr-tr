---
title: Bakım pencerelerini kullanma
titleSuffix: Configuration Manager
description: Configuration Manager ' deki istemcileri etkin bir şekilde yönetmek için Koleksiyonlar ve bakım pencerelerini kullanın.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b81599c6c5e4dda418b69c6e3c6d3b8cd144253
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428535"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Configuration Manager 'de bakım pencerelerini kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager cihazlarda etkileyen görevleri ne zaman çalıştırabileceği belirlemek için bakım pencerelerini kullanın. Bakım pencereleri yardımı istemci yapılandırma değişikliklerinin üretkenliği etkilemediği zamanlarda meydana geldiğinden emin olun. Yazılım Merkezi ile kullanıcılar, **yükleme durumu** sekmesinde cihazın sonraki bakım penceresini görebilirler. <!--1358131-->

Aşağıdaki görevler bakım pencerelerini destekler:

- Uygulama ve paket dağıtımları

- Yazılım güncelleştirme dağıtımları

- Uyumluluk ayarları dağıtımı ve değerlendirmesi

- İşletim sistemi ve özel görev sırası dağıtımları

Bakım pencerelerini etkin bir tarih, başlangıç ve bitiş saati ve yinelenme düzeniyle yapılandırın. Bir pencerenin en uzun süresi 24 saatten az olmalıdır. Konsol, 24 saatten uzun bir bakım penceresine izin vermez. Örneğin, tüm gün Cumartesi ve Pazar için bakım sağlamak istiyorsanız, her gün için 2 24 saatlik bakım pencereleri oluşturun.<!-- MEMDocs#310 -->

Varsayılan olarak, dağıtıma neden olan bilgisayar yeniden başlatmalarının bakım penceresi dışında yapılmasına izin verilmez, ancak varsayılanı geçersiz kılabilirsiniz. Bakım pencereleri yalnızca dağıtımın çalıştığı saati etkiler. Yerel olarak indirmek ve çalıştırmak için yapılandırdığınız dağıtımlar, içeriği pencerenin dışında indirebilir.

Bir istemci, bakım penceresi olan bir cihaz koleksiyonunun üyesiyse, dağıtım yalnızca izin verilen en fazla çalışma süresi pencerenin süresini aşmazsa çalışır. Dağıtım çalışamazsa, istemci bir uyarı oluşturur. Daha sonra, kullanılabilir zamana sahip bir sonraki zamanlanmış bakım penceresi sırasında dağıtımı yeniden çalıştırır.

## <a name="multiple-maintenance-windows"></a>Birden çok bakım penceresi

Bir istemci bilgisayar, bakım pencereleri olan birden çok cihaz koleksiyonunun üyesiyse, bu kurallar geçerlidir:  

- Bakım pencereleri çakışmazsa, istemci bunları iki bağımsız bakım penceresi olarak değerlendirir.

- Bakım pencereleri çakışırsa, istemci bunları her iki Windows için tek bir pencere olarak değerlendirir. Örneğin, bir koleksiyonda iki bakım penceresi oluşturursunuz. Birincisi 6:00 ' den 7:00 ' e kadar geçerlidir ve ikincisi de 6:30 ve 7:30 arasında geçerlidir. , 30 dakika içinde örtüştiğinden, Birleşik bakım penceresinin geçerlilik süresi 6:00 ile 7:30 90 dakikadır.

Bir kullanıcı yazılım merkezinden bir uygulama yüklediğinde, istemci bu uygulamayı hemen başlatır. Kullanıcının yöneticinin amacını önceliklendirir.

**Gerekli** amacına sahip bir uygulama dağıtımı, bir kullanıcının yazılım merkezi 'nde yapılandırdığı iş dışı saatlerde yükleme son tarihine ulaşırsa, istemci uygulamayı yüklüyor. Yöneticinin, kullanıcının kullanım amacını önceliklendirir.

Varsayılan olarak, birden çok bakım penceresi ile istemci yalnızca **yazılım güncelleştirme** türü pencereleri sırasında yazılım güncelleştirmelerini yüklüyor. Tek tür olmadıkları takdirde **tüm dağıtımlar** bakım pencerelerini yoksayar. Bu davranışı **yazılım güncelleştirmeleri** grubundaki şu istemci ayarıyla yapılandırabilirsiniz: **"yazılım güncelleştirmesi" bakım penceresi kullanılabilir olduğunda "tüm dağıtımlar" bakım penceresinde yazılım güncelleştirmelerinin yüklenmesini etkinleştirin**. Daha fazla bilgi için bkz. [istemci ayarları hakkında](../../deploy/about-client-settings.md#bkmk_SUMMaint).<!-- SCCMDocs#1317 -->

> [!NOTE]
> Bu ayar ayrıca, **görev dizileri**için geçerli olacak şekilde yapılandırdığınız bakım pencereleri için de geçerlidir.<!-- SCCMDocs-pr #4596 -->
>
> İstemcide yalnızca bir **dağıtımlar** penceresi varsa, bu pencerede yazılım güncelleştirmelerini veya görev dizilerini yine de yüklenir.

## <a name="configure-maintenance-windows"></a>Bakım pencerelerini yapılandırma

1. Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin.

1. **Cihaz Koleksiyonları** düğümünü seçin ve ardından bir koleksiyon seçin.

    > [!NOTE]
    > **Tüm sistemler** koleksiyonu için bakım pencereleri oluşturamazsınız.

1. Şeridin **giriş** sekmesinde, **Özellikler** grubunda, **Özellikler**' i seçin.

1. **Bakım pencereleri** sekmesine geçin ve **Yeni** simgesini seçin.

    1. Koleksiyon için bu bakım penceresini benzersiz olarak tanımlayacak bir **ad** belirtin.

    1. **Saat** ayarlarını yapılandırın:

        - **Geçerlilik tarihi**: bakım pencerelerinin başladığı tarih. Varsayılan değer geçerli tarihtir.

        - **Başlangıç** ve **bitiş**: bakım penceresinin başlangıç ve bitiş zamanları. Pencerenin **süresini** hesaplar. En kısa süre beş dakikadır ve en yüksek değer 24 saattir. Varsayılan süre, 01:00 ile 04:00 arasında olmak üzere üç saattir.

        - **Eşgüdümlü Evrensel Saat (UTC)**: istemcinin UTC saat dilimindeki başlangıç ve bitiş zamanlarını yorumlaması için bu seçeneği etkinleştirin. Aynı koleksiyondaki bölgesel veya küresel olarak dağıtılmış cihazlarda, bu seçenek Bakım penceresini koleksiyondaki tüm cihazlarda aynı anda gerçekleşecek şekilde ayarlar. İstemcinin, cihazın yerel saat dilimini kullanması için bu seçeneği devre dışı bırakın. Bu seçenek varsayılan olarak devre dışıdır.

    1. Yinelenme modelini yapılandırın. Varsayılan değer haftanın geçerli gününde hafta başına bir kez olur.

    1. **Bu zamanlamayı öğesine Uygula**: varsayılan olarak, pencere **tüm dağıtımlar**için geçerlidir. Bu pencere sırasında hangi dağıtımların çalıştırılacağını daha fazla denetlemek için **yazılım güncelleştirmelerini** veya **görev dizilerini** seçebilirsiniz.

        > [!TIP]
        > Aynı koleksiyonda farklı türlerde birden çok bakım penceresi yapılandırırsanız, istemci davranışlarını anladığınızdan emin olun. Daha fazla bilgi için bkz. [birden çok bakım penceresi](#multiple-maintenance-windows).

1. Pencereyi kaydedip kapatmak için **Tamam ' ı** seçin.

Koleksiyon özelliklerinin **bakım pencereleri** sekmesi yapılandırılmış tüm pencereleri görüntüler.

## <a name="use-powershell"></a><a name="bkmk_powershell"></a>PowerShell 'i kullanma

PowerShell, bakım pencerelerini yapılandırmak için kullanılabilir. Daha fazla bilgi için aşağıdaki makaleleri inceleyin:

- [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow?view=sccm-ps)
- [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow?view=sccm-ps)
- [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow?view=sccm-ps)
- [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow?view=sccm-ps)
