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
ms.openlocfilehash: b4ed1c10e23b75dc4478a0409d197015c98aff8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710219"
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

## <a name="import"></a>İçeri Aktarma

> [!NOTE]
> Yalnızca UNC yollarındaki uygulamaları içeri aktarabilirsiniz, yerel diskinizden doğrudan içeri aktaramazsınız.

1. Configuration Manager konsolunda **uygulamalar** düğümünü seçin. Şeridin Oluştur grubunda, **uygulamayı Içeri aktar**' ı seçin.
1. İçe aktarmak istediğiniz ZIP dosyasını seçin ve **İleri ' yi**seçin.
1. Dosya Içeriği penceresi, uygulamayı içeri aktardığınızda ne olacağını gösterir. **İleri**’yi seçin.
1. Özet ekranını gözden geçirin ve **İleri ' yi**seçin.
1. Sihirbazı kapatın. Uygulama artık sitede kullanılabilir.

## <a name="see-also"></a>Ayrıca bkz.
 
PowerShell kullanarak uygulamaları içeri ve dışarı aktarmayı otomatikleştirin.

* [İçeri aktarma-Cmappte](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Dışarı aktarma-Cmappte](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
