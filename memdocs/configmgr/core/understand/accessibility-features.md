---
title: Erişilebilirlik
titleSuffix: Configuration Manager
description: Configuration Manager herkes için erişilebilir hale getirme özellikleri hakkında bilgi edinin.
ms.date: 05/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a6e406d55524caca71bf75b087c9fd78a470c939
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699390"
---
# <a name="accessibility-features-in-configuration-manager"></a>Configuration Manager erişilebilirlik özellikleri

*Uygulama hedefi: Configuration Manager (geçerli dal)*


Configuration Manager herkes için erişilebilir hale getirmenize yardımcı olacak özellikler içerir.

> [!Note]  
> Sürüm 1902 ' den başlayarak, Configuration Manager konsolunun erişilebilirlik özelliklerini geliştirmek için, konsolunu çalıştıran bilgisayarda .NET 'i 4,7 veya üzeri bir sürüme güncelleştirin. <!-- SCCMDocs-pr issue #3228 -->  
> 
> .NET 4.7.1 ve 4.7.2 ' de yapılan erişilebilirlik değişiklikleriyle ilgili daha fazla bilgi için, [.NET Framework erişilebilirlik](/dotnet/framework/whats-new/whats-new-in-accessibility)yenilikleri bölümüne bakın.  



## <a name="keyboard-shortcuts"></a>Klavye kısayolları

### <a name="console-workspaces"></a>Konsol çalışma alanları

Bir çalışma alanına erişmek için aşağıdaki klavye kısayollarını kullanın:  

|Klavye kısayolu| Çalışma alanı|
|--------|--------|  
|CTRL + 1| Varlıklar ve uyumluluk|
|CTRL + 2|  Yazılım Kitaplığı|
|CTRL + 3|  İzleme|
|Ctrl + 4|  Yönetim|


### <a name="other-console-shortcuts"></a>Diğer konsol kısayolları

|Klavye kısayolu|  Amaç|
|--------|--------|  
|CTRL + a|Ana (orta) bölmedeki odağı ayarlayın.|
|CTRL + T|Odağı gezinti bölmesindeki üst düğüme ayarlayın. Odak zaten bu bölmesdeyse, odak ziyaret ettiğiniz son düğüme ayarlanır.|
|Ctrl + I|Odağı, şeridin altında bulunan içerik haritası çubuğuna ayarlayın.|
|CTRL + L|Mevcut olduğunda odağı **arama** alanına ayarlayın.|
|CTRL + D|Varsa, odağı Ayrıntılar bölmesine ayarlayın.|
|Alt     |Şeridin içindeki ve çıkan odayı değiştirin.|

### <a name="cmpivot-shortcuts"></a><a name="bkmk_cmpshortcuts"></a> CMPivot kısayolları

Çoğu [Web tarayıcısı klavye kısayolu](https://support.microsoft.com/help/17456/windows-internet-explorer-ease-of-access-options) CMPivot içinde çalışacaktır.

|Klavye kısayolu|Amaç|
|--------|--------|  
|CTRL + 1|İlk sekmede odağı ayarlayın.|
|Alt + &lt;|Adrese geri dönmek için|


## <a name="other-accessibility-features"></a>Diğer erişilebilirlik özellikleri

- Gezinti bölmesinde gezinmek için bir düğüm adının harflerini yazın.

- Ana görünüm ve şerit ile klavye gezintisi dairesel.

- Ayrıntılar bölmesindeki klavye gezintisi dairesel. Önceki nesneye veya bölmeye dönmek için CTRL + D, ardından SHIFT + TAB tuşlarını kullanın.

- Çalışma alanı görünümünü yenilemeden sonra odak, bu çalışma alanının ana bölmesine ayarlanır.

- Çalışma alanı menüsüne erişmek için Genişlet/Daralt simgesi odaklanana kadar SEKME tuşunu seçin. Sonra, çalışma alanı menüsüne erişmek için aşağı ok tuşunu seçin.  

- Bir çalışma alanı menüsünde gezinmek için, ok tuşlarını kullanın.  

- Çalışma alanındaki farklı alanlara erişmek için Tab tuşunu ve SHIFT + TAB tuşlarını kullanın. Şerit gibi çalışma alanının bir alanı içinde gezinmek için ok tuşlarını kullanın.  

- Odaklanmanız ağaç düğümdeyse adres çubuğuna erişmek için, üç kez SHIFT + TAB kullanın.  

- Bir sihirbazda veya özellik sayfasında klavye kısayollarıyla kutular arasında geçiş yapabilirsiniz. Belirli bir kutuyu seçmek için alt tuşunu ve altı çizili karakteri (alt + _) seçin.     

- Bir çalışma alanının farklı düğümlerine gitmek için bir düğümün adının ilk harfini girin. Her tuş basma imleci bu harfle başlayan bir sonraki düğüme taşıtir. Ekran okuyucu kullanırken, okuyucu bu düğümün adını okur.



## <a name="see-also"></a>Ayrıca bkz.

Configuration Manager kullanıcı arabirimlerine gidilme temelleri hakkında daha fazla bilgi için aşağıdaki makalelere bakın:
- [Configuration Manager konsolunu kullanma](../servers/manage/admin-console.md)
- [Yazılım Merkezi kullanıcı kılavuzu](software-center.md)

> [!NOTE]  
> Bu makaledeki bilgiler yalnızca Birleşik Devletler Microsoft ürünlerini lisanslayan kullanıcılar için geçerlidir. Bu ürünü Birleşik Devletler dışında aldıysanız, yazılım paketinizle birlikte gelen yan kuruluş bilgi kartını kullanabilir veya Microsoft Destek Hizmetleri 'ne yönelik iletişim bilgileri için [Microsoft Erişilebilirlik Web sitesini](https://www.microsoft.com/accessibility/) ziyaret edebilirsiniz. Bu bölümde açıklanan ürün ve hizmet türlerinin bölgenizde kullanılabilir olup olmadığını öğrenmek için yan kuruluşuna başvurabilirsiniz. Erişilebilirlik hakkında bilgiler Japonca ve Fransızca'nın dahil olduğu farklı dillerde mevcuttur.