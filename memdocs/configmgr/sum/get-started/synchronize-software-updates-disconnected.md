---
title: 'Güncelleştirmeleri Internet bağlantısı olmadan eşitler '
titleSuffix: Configuration Manager
description: Internet bağlantısı kesilen en üst düzey yazılım güncelleştirme noktasında yazılım güncelleştirmeleri eşitlemesini çalıştırın.
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c2fd85ea9d72e0986f56e24c7ccb66826829079b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710380"
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Bağlantısı kesilmiş bir yazılım güncelleştirme noktasından yazılım güncelleştirmelerini eşitleme  

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Üst düzey sitedeki yazılım güncelleştirme noktasının internet bağlantısı kesildiğinde, yazılım güncelleştirmeleri meta verilerini eşitlemek için WSUSUtil aracının dışa ve içe aktar işlevlerini kullanmanız gerekir. Eşitleme kaynağı olarak Configuration Manager hiyerarşinizde bulunmayan mevcut bir WSUS sunucusunu seçebilirsiniz. Bu makalede, WSUSUtil aracının dışa ve içe aktarma işlevlerinin nasıl kullanılacağı hakkında bilgi sağlanır.  

 Yazılım güncelleştirme meta verilerini dışa ve içe aktarmak için, yazılım güncelleştirme meta verileri belirtilen dışa aktarma sunucusundaki WSUS veritabanından dışa aktarmanız, ardından yerel olarak saklanan lisans koşulları dosyalarını bağlı olmayan yazılım güncelleştirme noktasına kopyalamanız ve ardından yazılım güncelleştirme meta verilerini bağlı olmayan yazılım güncelleştirme noktasındaki WSUS veritabanına aktarmanız gerekir  

 Yazılım güncelleştirme meta verilerinin aktarılacağı dışa aktarma sunucusunu tanımlamak için aşağıdaki tabloyu kullanın.  

|Yazılım güncelleştirme noktası|Bağlı yazılım güncelleştirme noktaları için yukarı akış güncelleştirme kaynağı|Bağlı olmayan yazılım güncelleştirme noktası için dışa aktarma sunucusu|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Merkezi yönetim sitesi|Microsoft Update (İnternet)<br /><br /> Varolan WSUS sunucusu|Configuration Manager ortamınızda gereksinim duyduğunuz yazılım güncelleştirme sınıflandırmalarını, ürünlerini ve dillerini kullanarak Microsoft Update ile eşitlenen bir WSUS sunucusu seçin.|  
|Tekil birincil site|Microsoft Update (İnternet)<br /><br /> Varolan WSUS sunucusu|Configuration Manager ortamınızda gereksinim duyduğunuz yazılım güncelleştirme sınıflandırmalarını, ürünlerini ve dillerini kullanarak Microsoft Update ile eşitlenen bir WSUS sunucusu seçin.|  

 Dışa aktarma işlemine başlamadan önce, en son yazılım güncelleştirme meta verilerinin eşitlendiğinden emin olmak için seçilen dışa aktarma sunucusunda yazılım güncelleştirme eşitlemesinin tamamlandığını doğrulayın. Yazılım güncelleştirme eşitlemesinin başarıyla tamamlandığını doğrulamak için, aşağıdaki prosedürü kullanın.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Yazılım güncelleştirme eşitlemesinin dışa aktarma sunucusunda başarıyla tamamlandığını doğrulamak için  

1.  WSUS Yönetim konsolunu açın ve WSUS veritabanını dışa aktarma sunucusuna bağlayın.  

2.  WSUS Yönetim konsolunda, **Eşitlemeler**’e tıklayın. Yazılım güncelleştirmeleri eşitleme denemelerinin listesi sonuçlar panelinde görüntülenir.  

3.  Sonuçlar panelinde, son yazılım güncelleştirme eşitleme denemesini bulun ve başarıyla tamamlandığını doğrulayın.  

> [!IMPORTANT]  
> - WSUSUtil aracı yazılım güncelleştirme meta verilerini dışa aktarmak için, dışa aktarma sunucusunda yerel olarak çalıştırılmalıdır ve ayrıca yazılım güncelleştirmeleri meta verilerini içe aktarmak için bağlı olmayan yazılım güncelleştirme noktası sunucusunda da çalıştırılmalıdır. Buna ek olarak, WSUSUtil aracını çalıştıran kullanıcı, her sunucuda yerel Yöneticiler gurubunun üyesi olmalıdır.  
> - Windows Server 2012 kullanıyorsanız, [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) WSUS sunucularında yüklü olduğundan emin olun.

## <a name="export-process-for-software-updates"></a>Yazılım güncelleştirmeleri dışa aktarma işlemi  
 Yazılım güncelleştirmeleri için dışarı aktarma süreci iki temel adımdan oluşur: yerel olarak saklanan lisans koşulları dosyalarını bağlı olmayan yazılım güncelleştirme noktasına kopyalamak ve yazılım güncelleştirmeleri meta verilerini WSUS veritabanından dışa aktarma sunucusuna aktarmak.  

 Yerel lisans koşulları meta verilerini bağlı olmayan yazılım güncelleştirme noktasına kopyalamak için aşağıdaki prosedürü kullanın.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Yerel dosyaları dışa aktarma sunucusundan bağlı olmayan yazılım güncelleştirme noktası sunucusuna kopyalamak için  

1. Dışa aktarma sunucusunda, yazılım güncelleştirmelerinin ve yazılım güncelleştirmeleri için lisans koşullarının saklandığı klasöre gidin. Varsayılan olarak, WSUS sunucusu dosyaları <*WSUSInstallationDrive*>\WSUS\WSUSContent\\ adresinde saklar, burada, *WSUSYüklemeSürücüsü* WSUS’un yüklü olduğu sürücüdür.  

2. Bu konumdaki tüm dosyaları ve klasörleri, bağlı olmayan yazılım güncelleştirme noktası sunucusundaki WSUSContent klasörüne kopyalayın.  

   Yazılım güncelleştirme meta verilerini WSUS veritabanından dışa aktarma sunucusuna aktarmak için aşağıdaki prosedürü kullanın.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Yazılım güncelleştirme meta verilerini WSUS veritabanından dışa aktarma sunucusuna aktarmak için  

1.  Dışarı aktarma sunucusunda komut isteminde, WSUSutil.exe dosyasını içeren klasöre gidin. Varsayılan olarak, bu araç %*ProgramFiles*%\Update Services\Tools konumunda bulunur. Örneğin, araç varsayılan konumda bulunuyorsa **cd %ProgramFiles%\Update Services\Tools**yazın.  

2.  Yazılım güncelleştirme meta verilerini bir paket dosyasına aktarmak için aşağıdakileri yazın:  

     **wsusutil.exe export**  *packagename*  *logfile*  
 
     Örneğin:  

     **WSUSutil. exe Export Export. xml. gz Export. log**  

     Biçim şu şekilde özetlenebilir: WSUSutil. exe ' nin ardından dışa aktarma seçeneği, dışa aktarma işlemi sırasında oluşturulan Export. xml. gz dosyasının adı ve günlük dosyasının adı. WSUSutil.exe dışa aktarma sunucusundan meta verileri dışa aktarır ve işlemin günlük dosyasını oluşturur.  

    > [!NOTE]  
    >  Paket (. xml. gz dosyası) ve günlük dosyası adı geçerli klasörde benzersiz olmalıdır.  

3.  Dışa aktarma paketini, içe aktarma WSUS sunucusundaki WSUSutil.exe'yi içeren klasöre taşıyın.  

    > [!NOTE]  
    >  Paketi bu klasöre taşırsanız, içe aktarma deneyimi daha kolay olabilir. Paketi içe aktarma sunucusuna erişebilen herhangi bir konuma taşıyabilir ve ardından WSUSutil.exe'yi çalıştırdığınızda konumu belirtebilirsiniz.  

## <a name="import-software-updates-metadata"></a>Yazılım güncelleştirmeleri meta verilerini içe aktarma  
 Yazılım güncelleştirme meta verilerini dışa aktarma sunucusundan bağlı olmayan yazılım güncelleştirme noktasına aktarmak için aşağıdaki prosedürü kullanın.  

> [!IMPORTANT]  
>  Güvenmediğiniz bir kaynaktan aktarılmış bilgileri kesinlikle içe aktarmayın. Güvenmediğiniz bir kaynaktan içerik aktarırsanız, WSUS sunucunuzun güvenliği riskli olabilir.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Meta verilerin içe aktarma sunucularının veritabanına aktarılması  

1.  İçeri aktarma WSUS sunucusunda komut isteminde, WSUSutil.exe dosyasını içeren klasöre gidin. Varsayılan olarak, bu araç %*ProgramFiles*%\Update Services\Tools konumunda bulunur.  

2.  Aşağıdakileri yazın:  

     **wsusutil.exe import**  *packagename*  *logfile*  

     Örneğin:  

     **WSUSutil. exe Import Export. xml. gz Import. log**  

     Biçim şu şekilde özetlenebilir: WSUSutil. exe ' nin ardından içeri aktarma komutu, dışa aktarma işlemi sırasında oluşturulan paket dosyasının adı (. xml. gz), farklı bir klasörsde ise paket dosyasının yolu ve günlük dosyasının adı gelir. WSUSutil.exe dışa aktarma sunucusundan meta verileri içe aktarır ve işlemin günlük dosyasını oluşturur.  

## <a name="next-steps"></a>Sonraki adımlar
Yazılım güncelleştirmelerini ilk kez eşitledikten sonra veya yeni sınıflandırmalar veya ürünler varsa, yeni [sınıflandırmaları ve ürünleri](configure-classifications-and-products.md) yeni ölçütlerle, yazılım güncelleştirmelerini eşitleyecek şekilde yapılandırmanız gerekir.

Yazılım güncelleştirmelerini ihtiyacınız olan ölçütlerle eşitledikten sonra, [yazılım güncelleştirmeleri için ayarları yönetin](manage-settings-for-software-updates.md).   
