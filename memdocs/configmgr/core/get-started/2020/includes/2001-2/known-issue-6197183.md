---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704245"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Bazı koleksiyonlar oluşturulamıyor veya düzenlenemiyor

<!--6197183-->
Technical Preview dalının bu sürümünde yeni bir koleksiyon oluşturamazsınız. Ayrıca var olan bir kullanıcı koleksiyonunun özelliklerini düzenleyemezsiniz.

Bu sorunu geçici olarak çözmek için Configuration Manager PowerShell cmdlet 'lerini kullanarak yeni Koleksiyonlar oluşturun ve mevcut kullanıcı koleksiyonlarını düzenleyin. Koleksiyonları yönetmek için kullanılabilir cmdlet 'lerden bazıları şunlardır:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [-CMCollection 'ı al](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)