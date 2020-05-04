---
title: Güncelleştirme kayıt aracı
titleSuffix: Configuration Manager
description: Configuration Manager konsoluna el ile güncelleştirme aktarmak için güncelleştirme kayıt aracının ne zaman ve nasıl kullanılacağını öğrenin.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 420b13005e8f9ac3d79f7d94398e6aa0ddcc190c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711241"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-configuration-manager"></a>Düzeltmeleri Configuration Manager aktarmak için güncelleştirme kayıt aracını kullanın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager için bazı güncelleştirmeler, Microsoft bulut hizmetinde bulunmaz ve yalnızca bant dışından edinilir. Buna örnek olarak belirli bir soruna yönelik sınırlı bir düzeltme sürümü gösterilebilir.   
Bir bant dışı yayın yüklemesi yapmanız gerektiğinde ve güncelleştirme veya düzeltme dosya adı **Update. exe**uzantısıyla sona erdiğinde, güncelleştirmeyi Configuration Manager konsoluna el ile içeri aktarmak için **güncelleştirme kayıt aracını** kullanırsınız. Araç, güncelleştirme paketini ayıklayıp site sunucusuna aktarmanızı ve güncelleştirmeyi Configuration Manager konsoluna kaydetmenizi sağlar.  

 Düzeltme dosyası **. exe** dosya uzantısına sahipse ( **Update. exe**değil), bkz. [Configuration Manager güncelleştirmelerini yüklemek için düzeltme yükleyicisini kullanma](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Bu konu, Configuration Manager güncelleştiren düzeltmelerin nasıl yükleneceğine ilişkin genel yönergeler sağlar. Belirli bir düzeltme veya güncelleştirme hakkında ayrıntılar için Microsoft Desteği adresindeki ilgili Bilgi Bankası (KB) makalesine başvurun.  

 **Güncelleştirme kayıt aracını kullanmanın önkoşulları:**  

-   Bu araç kullanılarak yalnızca **. Update. exe** uzantısıyla biten bant dışı güncelleştirmeler yüklenebilir  

-   Araç, doğrudan Microsoft 'tan aldığınız ayrı güncelleştirmeler ile bağımsızdır.  

-   Aracın hizmet bağlantı noktasının moduna bir bağımlılığı yoktur.  

-   Araç hizmet bağlantı noktasını barındıran bilgisayarda çalıştırılmalıdır  

-   Aracın çalıştığı bilgisayarda (hizmet bağlantı noktası bilgisayarı) .NET Framework 4,52 yüklü olmalıdır  

-   Aracı çalıştırmak için kullandığınız hesabın, hizmet bağlantı noktasını barındıran (aracın çalıştığı) bilgisayarda **yerel yönetici** izinlerine sahip olması gerekir  

-   Aracı çalıştırmak için kullandığınız hesabın, hizmet bağlantı noktasını barındıran bilgisayardaki şu klasörde **yazma** izinlerine sahip olması gerekir: ** &lt;ConfigMgr yükleme dizini\>\easysetuppayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Güncelleştirme kayıt aracını kullanmak için  

1. Hizmet bağlantı noktasını barındıran bilgisayarda:  

   -   Yönetici ayrıcalıklarıyla bir komut istemi açın ve ardından dizinleri ** &lt;\>-&lt;ürün\>-&lt;ürün sürümü KB\>makalesi kimlik-ConfigMgr. Update. exe içeren konuma değiştirin**  

2. Güncelleştirme kayıt aracını başlatmak için aşağıdaki komutu çalıştırın:  

   -   **&lt;\>-Ürün&lt;\>ürün sürümü-KB makalesi kimliği\>-ConfigMgr. Update. exe&lt;**  

   Düzeltme kaydedildikten sonra, 24 saat içinde konsolda bir güncelleştirme olarak görünür.  İşlem hızlandıraseçebilirsiniz:

   - Configuration Manager konsolunu açın ve **Yönetim** > **güncelleştirmeleri ve bakım**' a gidin, sonra **Güncelleştirmeleri denetle**' ye tıklayın. (Sürüm 1702 ' den önce, güncelleştirmeler ve bakım, **Yönetim** > **Cloud Services**altındadır.) 

   Güncelleştirme kayıt aracı eylemlerini yerel bilgisayardaki bir .log dosyasına yazar. Günlük dosyası düzeltme. exe dosyası ile aynı ada sahiptir ve **% systemroot%/Temp** klasörüne yazılır.  

    Güncelleştirme kaydedildikten sonra güncelleştirme kayıt aracını kapatabilirsiniz.  

3. Configuration Manager konsolunu açın ve **Yönetim** > **güncelleştirmeleri ve bakım '** a gidin. İçeri aktarılan düzeltmeler artık yüklenmeye hazırdır. (Sürüm 1702 ' den önce, güncelleştirmeler ve bakım, **Yönetim** > **Cloud Services**altındadır.)

   Güncelleştirme yükleme hakkında bilgi için bkz. [Configuration Manager için konsol içi güncelleştirmeleri yükleme](../../../core/servers/manage/install-in-console-updates.md)  
