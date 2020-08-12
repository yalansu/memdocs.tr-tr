---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128350"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

Sürüm 1906 ' den başlayarak, tek başına bir uygulama olarak CMPivot kullanabilirsiniz. CMPivot tek başına yalnızca Ingilizce olarak kullanılabilir. Ortamınızdaki cihazların gerçek zamanlı durumunu görüntülemek için Configuration Manager konsolunun dışında CMPivot çalıştırın. Bu değişiklik, konsolu yüklemeden önce bir cihazda CMPivot kullanmanıza olanak sağlar.

> [!Tip]  
> Bu özellik ilk olarak sürüm 1906 ' de [yayın öncesi özelliği](../pre-release-features.md)olarak sunulmuştur. Sürüm 2002 ' den başlayarak, artık yayın öncesi bir özellik değildir.  

CMPivot 'in gücünden birini, yardım masası veya güvenlik yöneticileri gibi diğer kişilerle paylaşabilirsiniz. Bu kişiler, geleneksel olarak kullandıkları diğer araçlarla birlikte Configuration Manager sorgulamak için CMPivot kullanabilir. Bu zengin yönetim verilerini paylaşarak, roller arası iş sorunlarını önceden çözmek için birlikte çalışabilirsiniz.

#### <a name="install-cmpivot-standalone"></a>CMPivot tek başına yükleme

1. CMPivot çalıştırmak için gereken izinleri ayarlayın. Daha fazla bilgi için bkz. [Önkoşullar](../cmpivot.md#prerequisites). İzinler kullanıcıya uygunsa [Güvenlik Yöneticisi rolünü](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906) de kullanabilirsiniz.
2. Aşağıdaki yolda CMPivot uygulama yükleyicisini bulun: `<site install path>\tools\CMPivot\CMPivot.msi` . Bu yoldan çalıştırabilir veya başka bir konuma kopyalayabilirsiniz.
3. CMPivot tek başına uygulamasını çalıştırdığınızda bir siteye bağlanmanız istenir. Merkezi Yönetim veya birincil site sunucusunun tam etki alanı adını ya da bilgisayar adını belirtin.
   - Tek başına CMPivot her açışınızda bir site sunucusuna bağlanmanız istenir.
4. CMPivot çalıştırmak istediğiniz koleksiyona gidin ve sorgunuzu çalıştırın.

   ![Sorgunuzu çalıştırmak istediğiniz koleksiyona gidin](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - **Komut dosyalarını çalıştır**, **Kaynak Gezgini**ve Web araması gibi sağ tıklama eylemleri CMPivot tek başına kullanılamaz. CMPivot tek başına 'ın birincil kullanımı Configuration Manager altyapısından bağımsız olarak sorgulama yapılır. Güvenlik yöneticilerine yardım için, CMPivot tek başına, Microsoft Defender Güvenlik Merkezi 'ne bağlanma özelliğini içerir. <!--5605358-->
> - Sürüm 1910 ' den başlayarak, [CMPivot tek başına kullanarak yerel cihaz sorgu değerlendirmesi](../cmpivot-changes.md#bkmk_local-eval)yapabilirsiniz. <!--3197353--> 