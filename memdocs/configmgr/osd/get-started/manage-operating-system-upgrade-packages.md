---
title: İşletim sistemi yükseltme paketlerini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager işletim sistemi yükseltme paketlerini yönetme hakkında bilgi edinin.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a50592815ed4581c01489f90b6c3701e53bb4981
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124423"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Configuration Manager ile işletim sistemi yükseltme paketlerini yönetme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager bir IŞLETIM sistemi yükseltme paketi, bir bilgisayarda var olan bir işletim sistemini yükseltmek için Windows kurulumu kaynak dosyalarını içerir. Bu makalede bir işletim sistemi yükseltme paketinin nasıl ekleneceği, dağıtılacağı ve kullanılacağı açıklanmaktadır.

> [!NOTE]
> İşletim sistemi yükseltme paketleri, yeni Windows yüklemeleri için de kullanılabilir. Ancak, bu yöntemle uyumlu olan sürücülere bağımlıdır. Bir işletim sistemi yükseltme paketinden yeni Windows yüklemeleri gerçekleştirirken, Windows PE 'de hala Windows PE sırasında eklenen sürücüler yüklenir. Bazı sürücüler, Windows PE 'de çalışırken yüklenmekte olan ile uyumlu değildir. Sürücüler Windows PE 'de yükleme ile uyumlu değilse, bunun yerine **. wim**gibi bir [işletim sistemi görüntüsü](manage-operating-system-images.md)kullanın.

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a>Bir işletim sistemi yükseltme paketi Ekle  

Bir işletim sistemi yükseltme paketini kullanabilmeniz için önce Configuration Manager sitenize ekleyin.

1. Configuration Manager konsolunda, **yazılım kitaplığı** çalışma alanına gidin, **işletim sistemleri**' ni genişletin ve **işletim sistemi yükseltme paketleri** düğümünü seçin.  

2. Şeridin **giriş** sekmesinde, **Oluştur** grubunda, **işletim sistemi yükseltme paketi Ekle**' yi seçin. Bu eylem, Işletim sistemi yükseltme ekleme Sihirbazı 'Nı başlatır.  

3. **Veri kaynağı** sayfasında, aşağıdaki ayarları belirtin:

    - İşletim sistemi yükseltme paketinin yükleme kaynak dosyalarının ağ **yolu** . Örneğin, `\\server\share\path`.  

        > [!NOTE]  
        >  Yükleme kaynak dosyaları, işletim sistemini yüklemek için setup.exe ve diğer dosya ve klasörleri içerir.  

        > [!IMPORTANT]  
        >  İstenmeyen değişikliklere engel olmak için bu yükleme kaynak dosyalarına erişimi sınırlayın.  

    - **Seçili yükseltme paketinin Install. wim dosyasındaki belirli bir görüntü dizinini ayıklayın** ve ardından listeden bir görüntü dizini seçin.<!--4931110--> Sürüm 1910 ' den başlayarak, bu seçenek dosyadaki tüm görüntü dizinleri yerine otomatik olarak tek bir dizin aktarır. Bu seçeneğin kullanılması, daha küçük bir görüntü dosyası ve daha hızlı çevrimdışı bakım ile sonuçlanır. Ayrıca, yazılım güncelleştirmelerini uyguladıktan sonra küçük bir görüntü dosyası için [görüntü bakımını iyileştirme](#bkmk_resetbase)işlemini destekler.  

        > [!IMPORTANT]  
        > Configuration Manager, işletim sistemi yükseltme paketindeki var olan Install. wim dosyasını geçersiz kılar. Görüntü dizinini geçici bir konuma ayıklar ve sonra özgün kaynak dizinine taşıýr. Bir işletim sistemi yükseltme paketini içeri aktarmadan ve bu seçeneği etkinleştirmeden önce özgün kaynak dosyalarını yedeklediğinizden emin olun.

    - İçeriği bir istemcide önceden önbelleğe almak istiyorsanız görüntünün **mimarisini** ve **dilini** belirtin. Daha fazla bilgi için bkz. [ön önbellek Içeriğini yapılandırma](../deploy-use/configure-precache-content.md).  

4. **Genel** sayfasında, aşağıdaki bilgileri belirtin. Bu bilgiler, birden fazla işletim sistemi yükseltme paketiniz olduğunda tanımlama amaçları için yararlıdır.  

    - **Ad**: işletim sistemi yükseltme paketi için benzersiz bir ad.  

    - **Sürüm**: isteğe bağlı bir sürüm tanımlayıcısı. Bu özelliğin yükseltme paketinin işletim sistemi sürümü olması gerekmez. Bu, genellikle kuruluşunuzun paketinin sürümüdür.  

    - **Açıklama**: isteğe bağlı kısa bir açıklama.  

5. Sihirbazı tamamlayın.  

Sonra, işletim sistemi yükseltme paketini dağıtım noktalarına dağıtın.  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a>İçeriği bir dağıtım noktasına dağıtma  

İşletim sistemi yükseltme paketlerini, diğer içerikle aynı şekilde dağıtım noktalarına dağıtın. Görev sırasını dağıtmadan önce, işletim sistemi yükseltme paketini en az bir dağıtım noktasına dağıtın. Daha fazla bilgi için, bkz. [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>Sonraki adımlar

[İşletim sistemini yükseltmek için görev dizisi oluşturma](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
