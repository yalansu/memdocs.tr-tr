---
title: Uygulamaları içeri ve dışarı aktarma
titleSuffix: Configuration Manager
description: Ayrı hiyerarşiler arasında paylaşmak için Configuration Manager uygulamaları içeri ve dışarı aktarmayı öğrenin.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3db127deb353f30566a1f03cbc6ac0eef666cb37
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695265"
---
# <a name="import-and-export-applications"></a>Uygulamaları içeri ve dışarı aktarma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İki hiyerarşi arasında uygulamaları içeri ve dışarı aktarmak için Configuration Manager kullanın. Örneğin, bir uygulamayı bir test ortamından bir üretim ortamına kopyalayın.

## <a name="export"></a>Dışarı Aktarma

1. Configuration Manager konsolunda **uygulamalar** düğümünü seçin. Şeridin Oluştur grubunda, **uygulamayı dışarı aktar**' ı seçin.
1. **Genel** ekranında, içine aktarılacak yenı bir ZIP dosyasının yolunu girin. İsteğe bağlı olarak, *Seçili uygulamalar ve Bağımlılıklar için* *bağımlılıkların, yerine geçme ilişkilerinin, koşulların ve sanal ortamların*ve içeriğin dışa aktarılacağını belirtin.  İsterseniz Yönetici açıklamalarını girin ve **İleri**' yi seçin.
1. Uygulamanın ve tüm bağımlılıkların **Ilgili nesneler** sayfasında listelendiğini doğrulayın ve **İleri ' yi**seçin.
1. Özet sayfasında, **İleri**' yi seçin.
1. İşlem tamamlandıktan sonra ZIP dosyasını oluşturur ve Sihirbazı kapatabilirsiniz.

> [!IMPORTANT]
> Bu uygulamayı başka bir ortama kopyalayacaksanız, hem ZIP dosyasını hem de ona eşlik eden klasörü alın. ZIP dosyası oluşturulan klasörle aynı dizinde bulunmalıdır.

## <a name="import"></a>İçeri Aktar

> [!NOTE]
> Yalnızca UNC yollarındaki uygulamaları içeri aktarabilirsiniz, yerel diskinizden doğrudan içeri aktaramazsınız.

1. Configuration Manager konsolunda **uygulamalar** düğümünü seçin. Şeridin Oluştur grubunda, **uygulamayı Içeri aktar**' ı seçin.
1. İçe aktarmak istediğiniz ZIP dosyasını seçin ve **İleri ' yi**seçin.
1. Dosya Içeriği penceresi, uygulamayı içeri aktardığınızda ne olacağını gösterir. **İleri**’yi seçin.
1. Özet ekranını gözden geçirin ve **İleri ' yi**seçin.
1. Sihirbazı kapatın. Uygulama artık sitede kullanılabilir.

## <a name="see-also"></a>Ayrıca bkz.
 
PowerShell kullanarak uygulamaları içeri ve dışarı aktarmayı otomatikleştirin.

* [İçeri aktarma-Cmappte](/powershell/module/configurationmanager/import-cmapplication)
* [Dışarı aktarma-Cmappte](/powershell/module/configurationmanager/export-cmapplication)