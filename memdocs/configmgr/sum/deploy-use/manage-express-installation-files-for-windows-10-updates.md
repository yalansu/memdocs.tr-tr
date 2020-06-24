---
title: Windows 10 Express güncelleştirmelerini yönetme
titleSuffix: Configuration Manager
description: Configuration Manager, Windows 10 için hızlı indirme ve istemcilerde daha hızlı yükleme süreleri sağlayan hızlı yükleme dosyalarını destekler.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: ff018bc81ecdb3d11ebb71f1850804a5679c67f7
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746587"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Windows 10 güncelleştirmeleri için hızlı yükleme dosyalarını yönetme

Configuration Manager, Windows 10 güncelleştirmeleri için hızlı yükleme dosyalarını destekler. İstemciyi yalnızca geçerli ayın Windows 10 toplu kalite güncelleştirmesi ve önceki ayın güncelleştirmesi arasındaki değişiklikleri yükleyecek şekilde yapılandırın. Hızlı yükleme dosyaları olmadan Configuration Manager istemcileri, önceki aydan tüm güncelleştirmeler dahil olmak üzere her ay tam Windows 10 toplu güncelleştirmesini indirir. Hızlı yükleme dosyalarının kullanılması, istemcilerde daha küçük indirmeler ve daha hızlı yükleme süreleri sağlar.

Windows 10 ile güncel kalmak üzere güncelleştirme içeriğini yönetmek için Configuration Manager nasıl kullanacağınızı öğrenmek için bkz. [Windows 10 güncelleştirme teslimini iyileştirme](optimize-windows-10-update-delivery.md).  


> [!IMPORTANT]  
> İşletim sistemi istemci desteği, Windows Update aracısına yönelik bir güncelleştirme ile Windows 10, sürüm 1607 ' de kullanılabilir. Bu güncelleştirme, 11 Nisan 2017 ' de yayınlanan güncelleştirmelere dahildir. Bu güncelleştirmeler hakkında daha fazla bilgi için bkz. [Destek makalesi 4015217](https://support.microsoft.com/kb/4015217). Gelecekteki güncelleştirmeler, daha küçük indirmeler için Express 'ten faydalanır. Windows 10 ' un önceki sürümleri ve bu güncelleştirme olmadan Windows 10 sürüm 1607, hızlı yükleme dosyalarını desteklemez.  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Sitenin Windows 10 güncelleştirmeleri için hızlı yükleme dosyalarını indirmesini sağlar
Windows 10 Express yükleme dosyaları için meta verileri eşitlemeye başlamak için, yazılım güncelleştirme noktasının özelliklerinde etkinleştirin.  

1. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler** düğümünü seçin.  

2. Merkezi yönetim sitesini veya tek başına birincil siteyi seçin.  

3. Şeritte, **site bileşenlerini Yapılandır**' a tıklayın ve ardından **yazılım güncelleştirme noktası**' na tıklayın. **Güncelleştirme dosyaları** sekmesine geçin ve **Windows 10 için tüm onaylanan güncelleştirmeler ve hızlı yükleme dosyaları Için tam dosyaları indir**' i seçin.

> [!NOTE]    
> Yazılım güncelleştirme noktası bileşenini *yalnızca* hızlı güncelleştirmeleri yükleyecek şekilde yapılandıramazsınız.  Site, tam dosyalara ek olarak hızlı yükleme dosyalarını indirir. Bu, içerik kitaplığında depolanan içerik miktarını artırır ve dağıtım noktalarınıza dağıtılır ve bu noktalara depolanır.

> [!Tip]  
> Diskte kullanılmakta olan gerçek alanı öğrenmek için dosyanın **disk üzerindeki boyut** özelliğini denetleyin. Disk üzerindeki boyut, boyut değerinden önemli ölçüde daha küçük olmalıdır. Daha fazla bilgi için bkz. [Windows 10 güncelleştirme teslimini iyileştirmek Için SSS](optimize-windows-10-update-delivery.md#bkmk_faq).  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>İstemcilerin hızlı yükleme dosyalarını indirmesini ve yüklemesini sağlama
İstemcilerde hızlı yükleme dosyaları desteğini etkinleştirmek için, istemci ayarlarının **yazılım güncelleştirmeleri** grubunda hızlı yükleme dosyalarını etkinleştirin. Bu ayar, belirttiğiniz bağlantı noktasına hızlı yükleme dosyalarını indirme isteklerinin dinlediği yeni bir HTTP dinleyicisi oluşturur.

> [!NOTE]    
> Bu, istemcilerin dağıtım noktasından Express içeriğini indirmek üzere teslim Iyileştirme veya Arka Plan Akıllı Aktarım Hizmeti (BITS) isteklerini dinlemek için kullandığı bir yerel bağlantı noktasıdır. Tüm trafik yerel bilgisayarda olduğundan, bu bağlantı noktasını güvenlik duvarları üzerinde açmanız gerekmez.  

İstemcide bu işlevselliği etkinleştirmek üzere istemci ayarlarını dağıttıktan sonra, geçerli ayın Windows 10 toplu güncelleştirmesi ve önceki ayın güncelleştirmesi arasındaki Delta 'yı indirmeye çalışır. İstemcilerin Express yükleme dosyalarını destekleyen bir Windows 10 sürümü çalıştırması gerekir.  

1. Yazılım güncelleştirme noktası bileşeninin özelliklerindeki hızlı yükleme dosyaları desteğini etkinleştirin (önceki yordam).  

2. Configuration Manager konsolunda, **Yönetim** çalışma alanına gidin ve **istemci ayarları**' nı seçin.  

3. Uygun istemci ayarlarını seçin ve Şeritteki **Özellikler** ' e tıklayın.  

4. **Yazılım güncelleştirmeleri** grubunu seçin. **Istemcilerde hızlı güncelleştirme yüklemeyi etkinleştirme**ayarını **Evet** olarak yapılandırın. İstemci üzerindeki HTTP dinleyicisi tarafından kullanılan bağlantı noktasıyla **hızlı güncelleştirme için içerik indirmek için kullanılan bağlantı noktasını** yapılandırın.
    - Sürüm 1902 ' de, **Istemcilerde hızlı güncelleştirme yüklemesini etkinleştir** ayarı, **istemcilerin kullanılabilir olduğunda Delta Içerik yüklemelerine izin verecek**şekilde değiştirilmiştir.
    - Sürüm 1902 ' de, **Hızlı güncelleştirmeler için içerik indirmek için kullanılan bağlantı noktası** , **istemcilerin Delta içerik isteklerini almak Için kullandığı bağlantı noktası**olarak değiştirilmiştir.
    

## <a name="next-steps"></a>Sonraki adımlar

[Yazılım güncelleştirmelerini dağıtma](deploy-software-updates.md)
