---
title: Yazılım güncelleştirme yönetimine hazırlanma
titleSuffix: Configuration Manager
description: Güncelleştirmeleri yönetmeye hazırlanmak için, Configuration Manager konsolundaki uyumluluk değerlendirmesi verilerini göstermek üzere bu görevleri doldurun.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ab22fdcacf7574884f7cfd21859cb4b1aeb8e23f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717275"
---
# <a name="prepare-for-software-updates-management"></a>Yazılım güncelleştirme yönetimine hazırlanma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Yazılım güncelleştirmesinin uyumluluk değerlendirmesi verileri Configuration Manager konsolunda görüntülenmeden önce ve istemci bilgisayarlara yazılım güncelleştirmeleri dağıtmadan önce, aşağıdaki bölümlerdeki adımları tamamlamalısınız.

## <a name="step-1-install-a-software-update-point"></a>1. Adım: yazılım güncelleştirme noktası yüklemeyi  
Yazılım güncelleştirme noktası, merkezi yönetim sitesinde veya tek başına birincil sitede ve yazılım güncelleştirmeleri uyumluluk değerlendirmesini etkinleştirmek ve istemcilere yazılım güncelleştirmeleri dağıtmak için birincil sitelerde gereklidir. Yazılım güncelleştirme noktası ikincil sitelerde isteğe bağlıdır. Ayrıntılar için bkz. [yazılım güncelleştirme noktası yüklemesi](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Adım 2: Yazılım Güncelleştirmelerini Eşitleme
Yazılım güncelleştirmeleri eşitlemesi, yapılandırdığınız ölçütlere uyan yazılım güncelleştirmeleri meta verilerini alma işlemidir. Yazılım güncelleştirmeleri, yazılım güncelleştirmelerini eşitlene kadar Configuration Manager konsolunda görüntülenmez. Ayrıntılar için bkz. [yazılım güncelleştirmelerini Synchronize](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Adım 3: Sınıflandırmaları ve eşitlenecek ürünleri yapılandırma
Bu yapılandırmayı merkezi yönetim sitesinde veya tek başına birincil sitede uygulayın. Yazılım güncelleştirmelerini ilk kez eşitledikten sonra, Configuration Manager sınıflandırmaların ve ürünlerin güncelleştirilmiş bir listesini alır. Şimdi, yazılım güncelleştirme noktası bileşen özelliklerindeki yeni seçenekler arasından seçim yapabilirsiniz. Yeni sınıflandırmaların ve ürünlerin yapılandırıldıktan sonra, yazılım güncelleştirmeleri eşitlemesini başlatmak için adım 2 ' yi tekrarlayın ve yeni ölçütler için yazılım güncelleştirme meta verilerini alın. Ayrıntılar için bkz. [eşitlenmek için sınıflandırmaları ve ürünleri yapılandırma](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>4. Adım: yazılım güncelleştirmeleri için ayarları yönetme
Yazılım güncelleştirmelerini eşitledikten sonra, yazılım güncelleştirmelerini dağıtmadan önce istemci ayarlarını Configuration Manager, Grup ilkesi yapılandırmasını ve yazılım güncelleştirme ayarlarını doğrulayın. Ayrıntılar için bkz. [yazılım güncelleştirmeleri için ayarları yönetme](manage-settings-for-software-updates.md).
