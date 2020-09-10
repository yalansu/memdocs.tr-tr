---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: c7fce3664d23d6402d28b053129fb2b15b540a87
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644127"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Bazı koleksiyonlar oluşturulamıyor veya düzenlenemiyor

<!--6197183-->
Technical Preview dalının bu sürümünde yeni bir koleksiyon oluşturamazsınız. Ayrıca var olan bir kullanıcı koleksiyonunun özelliklerini düzenleyemezsiniz.

Bu sorunu geçici olarak çözmek için Configuration Manager PowerShell cmdlet 'lerini kullanarak yeni Koleksiyonlar oluşturun ve mevcut kullanıcı koleksiyonlarını düzenleyin. Koleksiyonları yönetmek için kullanılabilir cmdlet 'lerden bazıları şunlardır:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)

- [-CMCollection 'ı al](/powershell/module/configurationmanager/get-cmcollection)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)