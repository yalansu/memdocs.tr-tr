---
title: Yazılım güncelleştirmeleri eşitlemesini yönetme
titleSuffix: Configuration Manager
description: Yazılım güncelleştirmeleri eşitlemesini zamanlamak, yazılım güncelleştirmeleri eşitlemesini el ile başlatmak ve yazılım güncelleştirmeleri eşitlemesini izlemek için bu adımları kullanın.
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1b47965fa5cc36b0c0eb6d47c2214d1dceb8ee8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712683"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a>Yazılım güncelleştirmelerini eşitler

*Uygulama hedefi: Configuration Manager (geçerli dal)*

 Configuration Manager yazılım güncelleştirme eşitlemesi, yapılandırdığınız ölçütlere uyan yazılım güncelleştirme meta verilerini alma işlemidir. Bu belirli ürünleri, sınıflandırmaları ve dilleri içerir. Genellikle, merkezi yönetim sitesindeki yazılım güncelleştirme noktası veya bağımsız bir birincil sitede meta verileri Microsoft Update alır. Daha sonra, üst düzey site diğer sitelere bir eşitleme isteği gönderir. Bir site üst siteden eşitleme isteği aldığında, site için yazılım güncelleştirme noktası yukarı akış [eşitleme kaynağından](../plan-design/plan-for-software-updates.md#BKMK_SyncSource)yazılım güncelleştirmeleri meta verilerini alır. Yazılım güncelleştirme eşitleme işlemi hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri eşitlemesi](../understand/software-updates-introduction.md#BKMK_Synchronization).

Yazılım güncelleştirme eşitlemesini, en üst düzey sitedeki yazılım güncelleştirme noktasının özelliklerinde bir zamanlamaya göre çalışacak şekilde yapılandırırsınız. Eşitleme zamanlamasını yapılandırdıktan sonra, genellikle zamanlamayı normal işlemlerin parçası olarak değiştirirsiniz. Ancak, gerekli olduğunda yazılım güncelleştirme eşitlemesini el ile de başlatabilirsiniz.

  > [!NOTE]  
  >  Yazılım güncelleştirmelerini eşitlemek için yazılım güncelleştirme noktalarının yukarı akış eşitleme kaynaklarına bağlanması gerekir. Bir yazılım güncelleştirme noktasının, yukarı akış eşitleme kaynağıyla bağlantısı kesildiğinde, yazılım güncelleştirmelerini eşitlemek için dışarı ve içeri aktarma yöntemini kullanabilirsiniz. Daha fazla bilgi için bkz. [Yazılım güncelleştirmelerini bağlantısı kesilen yazılım güncelleştirme noktasında eşitleme](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Yazılım güncelleştirmeleri eşitlemesini zamanla
Yazılım güncelleştirmeleri eşitlemesi için bir zamanlama yapılandırdığınızda, en üst düzey yazılım güncelleştirme noktası zamanlanan tarih ve saatte Microsoft Update eşitlemeyi başlatır. Özel zamanlama, Windows Server Update Services (WSUS) sunucusu, site sunucusu ve ağ taleplerinin düşük olduğu bir tarih ve saatte yazılım güncelleştirmelerini eşitlemenizi sağlar. Örneğin, zamanlamayı, yazılım güncelleştirmelerinin 2:00:00 ' da her hafta eşitlenecek şekilde ayarlayabilirsiniz. Zamanlanan eşitleme sırasında, zamanlanan son eşitlemeden bu yana yazılım güncelleştirmeleri meta verilerinde yapılan tüm değişiklikler site veritabanına girilir. Bu, yeni yazılım güncelleştirme meta verilerini veya değiştirilen, kaldırılan veya artık süresi dolan meta verileri içerir.

Yazılım güncelleştirmeleri eşitlemesini zamanlamak için üst düzey sitede aşağıdaki yordamları kullanın.  

#### <a name="to-schedule-software-updates-synchronization"></a>Yazılım güncelleştirmeleri eşitlemesini zamanlamak için  

  1.  Configuration Manager konsolunda, **Yönetim**’e tıklayın.  

  2.  Yönetim çalışma alanında, **Site Yapılandırması**'nı genişletin ve **Siteler**'e tıklayın.  

  3.  Sonuçlar bölmesinde yönetim merkezi sitesini veya tek başına birincil siteyi tıklatın.  

  4.  **Giriş** sekmesindeki **Ayarlar** grubunda **Site Bileşenlerini Yapılandır**’a, ardından da **Yazılım Güncelleştirme Noktası**’na tıklayın.  

  5.  Yazılım Güncelleştirme Noktası Bileşen Özellikleri iletişim kutusunda **Eşitlemeyi zamanında etkinleştir**’i seçin ve ardından eşitleme zamanlamasını belirtin.  

## <a name="manually-start-software-updates-synchronization"></a>Yazılım güncelleştirmeleri eşitlemesini el ile Başlat
Yazılım **kitaplığı** çalışma alanındaki **tüm yazılım güncelleştirmeleri** düğümünden Configuration Manager konsolundaki en üst düzey sitede yazılım güncelleştirmeleri eşitlemesini el ile başlatabilirsiniz.  

Yazılım güncelleştirmeleri eşitlemesini el ile başlatmak için üst düzey sitede aşağıdaki yordamları kullanın.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Yazılım güncelleştirmeleri eşitlemesini el ile başlatmak için  

1. Merkezi yönetim sitesine veya tek başına birincil siteye bağlı Configuration Manager konsolunda, **yazılım kitaplığı**' na tıklayın.  

2. Yazılım Kitaplığı çalışma alanında **Yazılım Güncelleştirmeleri** ’ni genişletin ve **Tüm Yazılım Güncelleştirmeleri** veya **Yazılım Güncelleştirme Grupları**’na tıklayın.  

3. **Giriş** sekmesinde, **Oluştur** grubunda, **Yazılım Güncelleştirmeleri Eşitle**’ye tıklayın. İletişim kutusunda **Evet** ’e tıklayarak eşitleme işlemini başlatmak istediğinizi onaylayın.  

   Yazılım güncelleştirme noktasında eşitleme işlemini başlattıktan sonra, hiyerarşinizdeki tüm yazılım güncelleştirme noktaları için Configuration Manager konsolundan eşitleme işlemini izleyebilirsiniz. Yazılım güncelleştirmeleri eşitlemesini izlemek için aşağıdaki prosedürü kullanın.  


## <a name="monitor-software-updates-synchronization"></a>Yazılım güncelleştirmeleri eşitlemesini izleme
Eşitleme işlemini başlattıktan sonra, hiyerarşinizdeki tüm yazılım güncelleştirme noktaları için işlemi izlemek üzere Configuration Manager konsolunu kullanabilirsiniz. Yazılım güncelleştirme eşitlemesini izlemek için aşağıdaki prosedürü kullanın. Eşitleme işlemi de dahil olmak üzere yazılım güncelleştirmelerini izleme hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmelerini izleme](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Yazılım güncelleştirmeleri eşitleme işlemini izlemek için  

1. Configuration Manager konsolunda, **izleme**' yi tıklatın.  

2. **İzleme** çalışma alanında **Yazılım Güncelleştirme Noktası Eşitleme Durumu**’na tıklayın.  

   Configuration Manager hiyerarşinizdeki yazılım güncelleştirme noktaları sonuçlar bölmesinde görüntülenir. Bu görünümden, tüm yazılım güncelleştirme noktalarının eşitleme durumunu izleyebilirsiniz. Eşitleme işlemine ilişkin daha ayrıntılı bilgi isterseniz, her site sunucuda <*ConfigMgrInstallationPath*>\Logs adresinde bulunan wsyncmgr.log dosyasını gözden geçirebilirsiniz.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Microsoft Update kataloğundan güncelleştirmeleri içeri aktarma

En üst düzey yazılım güncelleştirme noktası, Microsoft 'tan Configuration Manager 'ye yazılım güncelleştirmeleri hakkında bilgi almak için WSUS kullanır. Bazen, seçili ürünleriniz ve sınıflandırmalarınız için WSUS ile otomatik olarak eşitlenmeyen ancak [Microsoft Update kataloğunda](https://catalog.update.microsoft.com)kullanılabilen bir güncelleştirmeye ihtiyacınız vardır. WSUS ile otomatik olarak eşitlemez güncelleştirmeler genellikle yüksek oranda özel sorunları çözmektir. Genellikle katalogda bir güncelleştirme varsa, bunu WSUS 'e aktarabilirsiniz. Daha sonra Configuration Manager ile eşitleyebilir ve diğer tüm güncelleştirmeler gibi dağıtabilirsiniz.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Microsoft Update kataloğundan bir güncelleştirmeyi içeri aktarmak için

1. WSUS Yönetim konsolunu açın ve hiyerarşinizdeki en üst düzey WSUS sunucusuna bağlayın.
   - Internet Explorer bilgisayarın varsayılan Web tarayıcısı değilse, geçici olarak varsayılan olarak ayarlayın.
2. **Güncelleştirmeler** ' e tıklayın veya WSUS sunucunuzun adına tıklayın. 
3. **Eylemler** bölmesinde, [Microsoft Update kataloğuna](https://catalog.update.microsoft.com)bir tarayıcı penceresi açacak **güncelleştirmeleri içeri aktar...** öğesini seçin.
   ![WSUS konsolunda güncelleştirmeleri içeri aktar ' ı seçin](media/wsus-console-import-updates.png)
4. İstenirse, Microsoft Update Catalog ActiveX denetimini yüklemelisiniz. Güncelleştirmelerin WSUS 'e aktarılması için denetimin yüklü olması gerekir. 
5. Tarayıcı penceresinde, istediğiniz güncelleştirmeyi arayın. Sepete eklemek için **Ekle*** düğmesine tıklayın.
6. **Sepeti görüntüle**' ye tıklayın. **Windows Server Update Services 'a doğrudan Içeri aktarma** seçeneğinin seçili olduğundan emin olun. Ardından **Içeri aktar**' a tıklayın.
    ![Güncelleştirme kataloğundan WSUS 'e aktarma](./media/import-catalog-update-into-wsus.png)
7. İçeri aktarma işlemi tamamlandıktan sonra tarayıcı penceresinde **Kapat** ' a tıklayın.
     - Gerekirse varsayılan tarayıcınızı sıfırlayın.
8. Configuration Manager yazılım güncelleştirme noktanızı eşitler.


## <a name="next-steps"></a>Sonraki adımlar
Yazılım güncelleştirmelerini ilk kez eşitledikten sonra veya yeni sınıflandırmalar veya ürünler varsa, yeni [sınıflandırmaları ve ürünleri](configure-classifications-and-products.md) yeni ölçütlerle, yazılım güncelleştirmelerini eşitleyecek şekilde yapılandırmanız gerekir.

Yazılım güncelleştirmelerini ihtiyacınız olan ölçütlerle eşitledikten sonra, [yazılım güncelleştirmeleri için ayarları yönetin](manage-settings-for-software-updates.md).  
