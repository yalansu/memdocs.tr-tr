---
title: Windows’u ağ üzerinden dağıtmak için Yazılım Merkezi’ni kullanma
titleSuffix: Configuration Manager
description: Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenilemek veya Windows 'un en son sürümüne yükseltmek için yazılım merkezi 'nden bir işletim sistemi dağıtın.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124610"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Configuration Manager ile Windows 'u ağ üzerinden dağıtmak için yazılım merkezi 'ni kullanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yazılım Merkezi 'nde kullanılabilir bir işletim sistemi yükleyen bir görev sırası yapabilirsiniz. Bir Kullanıcı aşağıdaki işletim sistemi dağıtım senaryoları için yazılım merkezi 'nden bir görev dizisi çalıştırabilir:

- [Mevcut bir bilgisayarı yeni bir Windows sürümü ile yenileme](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Windows’u en yeni sürüme yükseltme](upgrade-windows-to-the-latest-version.md)

- [İşletim sistemi dışı dağıtımlar için görev dizisi oluşturma](create-a-task-sequence-for-non-operating-system-deployments.md)

Bu işletim sistemi dağıtım senaryolarından birindeki adımları doldurun. Ardından, yazılım merkezi 'nde mevcut olan dağıtımlar için hazırlanmak üzere aşağıdaki bölümleri kullanın.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Görev dizisini dağıtma

Görev dizisini bir hedef koleksiyona dağıtın. Daha fazla bilgi için, bkz. [Deploy a task sequence](deploy-a-task-sequence.md).

Dağıtımın **dağıtım ayarları** sayfasında, **aşağıdaki için kullanılabilir yap** ayarı için aşağıdaki seçeneklerden birini belirleyin:

- Yalnızca Configuration Manager Istemcileri

- Configuration Manager istemcileri, medya ve PXE

Dağıtımın gerekli veya kullanılabilir olup olmadığını da yapılandırın:

- Gerekli dağıtım: gerekli dağıtımlar, görev dizisini yazılım merkezi 'nde kullanılabilir hale getirir. Yapılandırılan son tarihte otomatik olarak başlatılır.

- Kullanılabilir dağıtım: görev dizisi yazılım merkezi 'nde kullanılabilir ve Kullanıcı bunu isteğe bağlı olarak yükleyebilir.

Dağıtımı oluşturduktan sonra, hedef koleksiyondaki istemciler yazılım merkezi 'nde görev dizisini gösterir.

## <a name="next-steps"></a>Sonraki adımlar

[İşletim sistemi dağıtımı için kullanıcı deneyimleri](../understand/user-experience.md#software-center)
