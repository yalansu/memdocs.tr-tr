---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712095"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a>Bazı koleksiyonlar oluşturulamıyor veya düzenlenemiyor

<!--6197183-->
Technical Preview dalının bu sürümünde yeni bir koleksiyon oluşturamazsınız. Ayrıca var olan bir kullanıcı koleksiyonunun özelliklerini düzenleyemezsiniz.

Bu sorunu geçici olarak çözmek için Configuration Manager PowerShell cmdlet 'lerini kullanarak yeni Koleksiyonlar oluşturun ve mevcut kullanıcı koleksiyonlarını düzenleyin. Koleksiyonları yönetmek için kullanılabilir cmdlet 'lerden bazıları şunlardır:

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [-CMCollection 'ı al](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
