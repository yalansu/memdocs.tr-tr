---
title: Özel bir görev sırası oluşturma
titleSuffix: Configuration Manager
description: Görev dizisine adımlar eklemek için Configuration Manager bir özel görev dizisini düzenleyin.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9107e9787cf7f12cab624101c37344ea20684112
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720621"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Configuration Manager ile özel bir görev dizisi oluşturma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager içinde özel bir görev dizisi oluşturduğunuzda, görev dizisi adımları içermez. Görev dizisini oluşturduktan sonra düzenleyin ve gereken görev sırası adımlarını ekleyin.  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a>Özel görev dizisi oluşturma

Özel bir görev dizisi oluşturmak için aşağıdaki yordamı kullanın:

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve ardından **görev dizileri** düğümünü seçin.  

1. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **görev sırası oluştur**' u seçin. Bu eylem görev sırası oluşturma Sihirbazı 'Nı başlatır.  

1. **Yeni Görev Sırası Oluştur** sayfasında **Yeni bir özel görev sırası oluştur**öğesini seçin.  

1. **Görev sırası bilgileri** sayfasında, aşağıdakileri belirtin:

    - Görev sırası için bir ad
    - Görev dizisinin açıklaması
    - Kullanılacak görev sırası için isteğe bağlı bir önyükleme görüntüsü

Görev sırası oluşturma Sihirbazı 'Nı tamamladıktan sonra, Configuration Manager özel görev sırasını **görev sıraları** düğümüne ekler. Bundan böyle bu görev sırasını düzenleyerek görev sırası adımları ekleyebilirsiniz.  

## <a name="see-also"></a>Ayrıca bkz.

Kullanılabilir görev dizisi adımlarının bir listesi için bkz. [görev dizisi adımları](../understand/task-sequence-steps.md).  

Bir görev dizisinin nasıl düzenleneceği hakkında daha fazla bilgi için bkz. [görev dizisi düzenleyicisini kullanma](../understand/task-sequence-editor.md).  

Çoğu zaman, işletim sistemi dağıtımı görevlerini otomatikleştirmek için görev dizilerini kullanırsınız, ancak farklı türdeki görevleri otomatikleştirmek için özel bir görev dizisi oluşturabilirsiniz. Daha fazla bilgi için bkz. [işletim sistemi dışı dağıtımlar için görev dizisi oluşturma](create-a-task-sequence-for-non-operating-system-deployments.md).

Sürüm 2002 ' den başlayarak, uygulama modeli aracılığıyla görev dizilerini kullanarak karmaşık uygulamaları yüklemeyin. Uygulamayı yüklemek ya da kaldırmak için, bir görev dizisi olan bir uygulamaya dağıtım türü ekleyin. Daha fazla bilgi için bkz. [Windows uygulamaları oluşturma](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

## <a name="next-steps"></a>Sonraki adımlar

[Görev dizisini dağıtma](deploy-a-task-sequence.md)
