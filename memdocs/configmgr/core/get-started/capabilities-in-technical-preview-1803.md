---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Configuration Manager Technical Preview sürüm 1803 ' de bulunan yeni özellikler hakkında bilgi edinin.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719046"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Configuration Manager için Technical Preview 1803 ' deki yetenekler

*Uygulama hedefi: Configuration Manager (Technical Preview dalı)*

Bu makalede, sürüm 1803 Configuration Manager için Technical Preview 'da kullanılabilen özellikler tanıtılmaktadır. Bu sürümü, Technical Preview sitenize güncelleştirmek ve yeni özellikleri eklemek için yükleyebilirsiniz. 

Bu güncelleştirmeyi yüklemeden önce [Teknik Önizleme](technical-preview.md) makalesini gözden geçirin. Bu makalede, Technical Preview kullanımı, sürümler arasında nasıl güncelleştirme yapılacağı ve geri bildirimde bulunmak için genel gereksinimler ve sınırlamalar tamamladığınızda tercihinize.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Aşağıda, bu sürümle deneyebilmeniz için kullanabileceğiniz yeni özellikler verilmiştir.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Çekme dağıtım noktaları, bulut dağıtım noktalarını kaynak olarak destekler  
<!--1321554-->
Birçok müşteri, WAN genelindeki bir kaynak dağıtım noktasından içerik indirecek uzak veya şubelerde [çekme dağıtım noktalarını](../plan-design/hierarchy/use-a-pull-distribution-point.md) kullanır. Uzak ofislerinizin internete daha iyi bağlantısı varsa veya WAN bağlantılarınızda yükü azaltmak için artık kaynak olarak Microsoft Azure bir [bulut dağıtım noktası](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) kullanabilirsiniz. Dağıtım noktası özelliklerinin **çekme dağıtım noktası** sekmesine bir kaynak eklediğinizde, sitedeki herhangi bir bulut dağıtım noktası artık kullanılabilir bir dağıtım noktası olarak listelenir. Site sistem rollerinin her ikisi de aynı şekilde kalır. 

### <a name="prerequisites"></a>Önkoşullar
- Çekme dağıtım noktası, Microsoft Azure ile iletişim kurmak için internet erişimine ihtiyaç duyuyor.
- İçeriğin kaynak bulut dağıtım noktasına dağıtılması gerekir.

> [!Note]  
> Bu özellik, veri depolama ve ağ çıkışı için Azure aboneliğinize ücret vermez. Daha fazla bilgi için bkz. [bulut tabanlı dağıtım kullanma maliyeti](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>WAN kullanımını azaltmak için istemci eş önbelleğinde kısmi indirme desteği
<!--1357346-->
İstemci eş önbelleği kaynakları artık içeriği parçalara bölebilir. Bu parçalar, WAN kullanımını azaltmak için Ağ aktarımını en aza indirir. Yönetim noktası, içerik bölümlerinin daha ayrıntılı bir şekilde izlenmesini sağlar. Aynı içeriğin her sınır grubu için birden fazla indirilmesini ortadan kaldırmaya çalışır. 

### <a name="example-scenario"></a>Örnek senaryo
Contoso, iki sınır grubuna sahip tek bir birincil siteye sahiptir: Merkez (HQ) ve şube ofisi. Sınır grupları arasında 30 dakikalık bir geri dönüş ilişkisi vardır. Site için yönetim noktası ve dağıtım noktası yalnızca HQ sınırında bulunur. Şube ofis konumunun Yerel dağıtım noktası yok. Şube ofisindeki dört istemciden ikisi eş önbellek kaynakları olarak yapılandırılır. 

![Örnek senaryo için açıklandığı şekilde ağ yapılandırması diyagramı](media/1357346-peer-cache-source-parts.png)

1. Şube ofisindeki tüm dört istemci için içerik içeren bir dağıtımı hedefleyebilirsiniz. İçeriği yalnızca dağıtım noktasına dağıtım.
2. Client3 ve Client4 'in dağıtım için yerel bir kaynağı yoktur. Yönetim noktası, istemcileri uzak sınır grubuna geri dönmeden önce 30 dakika beklemesini söyler.
3. İSTEMCİ1 (PCS1), ilkeyi yönetim noktasıyla yenilemek için ilk eş önbellek kaynağıdır. Bu istemci bir eş önbellek kaynağı olarak etkinleştirildiğinden, yönetim noktası bunu dağıtım noktasından bir bölümünü hemen indirmeyi ister.  
4. Istemci2 (PCS2) yönetim noktasıyla iletişim kurduğunda, bir parçası zaten devam ediyor ancak henüz tamamlanmadığında, yönetim noktası bunu dağıtım noktasından B bölümünü hemen indirmeyi ister.
5. PCS1, A bölümünü indirmeyi tamamlar ve anında yönetim noktasına bildirir. B bölümü zaten devam ettiğinden ancak henüz tamamlanmadığında, yönetim noktası bunu dağıtım noktasından C bölümünü indirmeye başlamasını söyler.
6. PCS2 B bölümünü indirmeyi tamamlar ve yönetim noktasına anında bildirir. Yönetim noktası, bunu dağıtım noktasından D bölümünü indirmeye başlamasını söyler. 
7. PCS1, Bölüm C 'yi indirmeyi tamamlar ve anında yönetim noktasına bildirir. Yönetim noktası, uzak dağıtım noktasından daha fazla kullanılabilir bölüm olmadığını bildirir. Yönetim noktası, PCS2 'in yerel eşinden B bölümünü indirmesini söyler.
8. Bu işlem, her iki istemci eş önbelleği kaynağına ait tüm parçalar olana kadar devam eder. Yönetim noktası, eş önbellek kaynaklarını yerel eşlerden bölümleri indirmek üzere bir daha vermeden önce uzak dağıtım noktasından bölümleri önceliklendirir. 
9. Client3, 30 dakikalık geri dönüş döneminin süresi dolduktan sonra ilkeyi Yenileme ilkdir. Şimdi, yeni yerel kaynakları istemciye bildiren yönetim noktası ile geri kontrol eder. İçeriğin WAN genelindeki dağıtım noktasından tam olarak indirilmesi yerine, içeriği istemci eş önbelleği kaynaklarından birinden tam olarak indirir. İstemciler, yerel eş kaynakları önceliklendirdir. 

> [!Note]  
> İstemci eş önbelleği kaynaklarının sayısı, içerik bölümlerinin sayısından büyükse, yönetim noktası ek eş önbellek kaynaklarını normal bir istemci gibi geri dönüşü bekleyecek şekilde yönlendirir. 


### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

1. [Sınır gruplarını](../servers/deploy/configure/boundary-groups.md) ve [eş önbellek kaynaklarını](../plan-design/hierarchy/client-peer-cache.md) normal başına ayarlayın.
2. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler**' i seçin. Şeritte **Hiyerarşi ayarları** ' na tıklayın. 
3. **Genel** sekmesinde, **içeriği parçalara bölmek için istemci eş önbelleği kaynaklarını yapılandırma**seçeneğini etkinleştirin. 
4. İçerikle gerekli bir dağıtım oluşturun.  

   > [!Note]  
   > Bu işlev yalnızca istemci, gerekli bir dağıtım gibi arka planda içerik indirdiğinde geçerlidir. Kullanıcının yazılım merkezi 'nde kullanılabilir bir dağıtımı yüklemesi gibi isteğe bağlı indirmeler her zamanki gibi davranır.  

1. İçeriğin parçalar halinde indirilmesini işlemesini görmek için, istemci eş önbelleği kaynağında **ContentTransferManager. log** ' u ve yönetim noktasındaki **MP_Location. log** dosyasını inceleyin.  
 



## <a name="maintenance-windows-in-software-center"></a>Yazılım Merkezi 'nde bakım pencereleri
<!--1358131-->
Yazılım Merkezi artık bir sonraki zamanlanmış bakım penceresini görüntülüyor. Yükleme durumu sekmesinde, görünümü tümü ' nden yakında olacak şekilde değiştirin. Zamanlanan zaman aralığını ve dağıtım listesini görüntüler. Gelecekteki bakım pencereleri yoksa liste boştur. 

![Yükleme durumu sekmesindeki yaklaşan dağıtımlar listesini gösteren yazılım merkezi](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Yazılım Merkezi 'nde Web sayfası için özel sekme
<!--1358132-->
Artık yazılım merkezi 'nde bir Web sayfası açmak için özelleştirilmiş bir sekme oluşturabilirsiniz. Bu özellik, son kullanıcılarınıza yönelik içeriği tutarlı ve güvenilir bir şekilde gösterbırakmanıza olanak tanır. Aşağıdaki listede birkaç örnek verilmiştir:
- BT ile iletişim kurun: kuruluşunuzun BT departmanınızla iletişim kurma hakkında bilgi
- BT Destek Merkezi: Bilgi Bankası araması veya destek bileti açma gibi self servis eylemleri.
- Son Kullanıcı belgeleri: kuruluşunuzdaki kullanıcılar için uygulamalar kullanma veya Windows 10 ' a yükseltme gibi çeşitli BT konularına yönelik makaleler.


### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

1. Configuration Manager konsolu, **Yönetim** çalışma alanı, **Istemci ayarları** düğümünde **varsayılan istemci ayarları** ilkesini açın.
2. **Yazılım Merkezi** grubunu seçin.
3. **Yazılım Merkezi ayarları**için **Özelleştir**' e tıklayın.
4. **Sekmeler** sekmesine geçin.
5. **Yazılım Merkezi için özel bir sekme belirtme**seçeneğini etkinleştirin.
    1. **Sekme adı** metin alanına bir ad girin. Bu ad, yazılım merkezi 'nde kullanıcıya gösterilir.
    2. **İçerik URL 'si** metin alanına GEÇERLI bir URL girin. Bu URL, kullanıcılar bu sekmeye tıkladığınızda Software Center 'ın görüntülediği içeriktir.

> [!Tip]  
> Software Center, Web sayfasını işlemek için Internet Explorer bileşenlerini kullanır.

## <a name="enable-third-party-software-update-support-on-clients"></a>İstemcilerde üçüncü taraf yazılım güncelleştirme desteğini etkinleştir

Artık, üçüncü taraf yazılım güncelleştirmeleri için Configuration Manager istemcilerinin yapılandırılmasını etkinleştirebilirsiniz. SUP bileşen özellikleri için **üçüncü taraf yazılım güncelleştirmelerini etkinleştirdiğinizde** , SUP, WSUS tarafından üçüncü taraf güncelleştirmeleri için kullanılan imzalama sertifikasını indirir. <!--1357605-->

İstemci ayarlarında **üçüncü taraf yazılım güncelleştirmelerini etkinleştir** seçeneğinin belirlenmesi şunları yapar: 
- İstemcisinde, ' bir intranet Microsoft güncelleştirme hizmeti konumu için imzalı güncelleştirmelere Izin ver ' ilkesini ayarlar. 
- İmza sertifikasını istemcideki güvenilen yayımcı deposuna yükleme. 

### <a name="try-it-out"></a>Deneyin!
 Görevleri tamamlamayı deneyin. Sonra, nasıl çalıştığını öğrenmek için şeridin **giriş** sekmesinden **geri bildirim** gönderin.

1. Configuration Manager hiyerarşisindeki en üstteki sitede **Yönetim** düğümüne gidin, **Site yapılandırması**' nı ve ardından **siteler**' i genişletin.
2. En üst site sunucunuza sağ tıklayın ve **site bileşenlerini Yapılandır** ' ı ve ardından **yazılım güncelleştirme noktası**' nı seçin.
3. **Üçüncü taraf güncelleştirmeleri** sekmesine tıklayın ve **üçüncü taraf yazılım güncelleştirmelerini etkinleştir**' i işaretleyin.
4. **Istemci ayarları** ' nı açın ve **yazılım güncelleştirmeleri**ayarlarına gidin.
5. **Üçüncü taraf yazılım güncelleştirmelerinin etkinleştir** ' in **Evet**olarak ayarlandığından emin olun.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>İzleme görünümlerinden varlık ayrıntılarının kopyalanmasını/yapıştırmayı etkinleştir
[Kullanıcı sesli geri bildirimlerinizin](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det) bir sonucu olarak, dağıtım ve dağıtım durumu izleme görünümlerinde varlık ayrıntıları bölmesinde Kopyala/Yapıştır işlevini etkinleştirebilirsiniz.  <!--1357552-->

## <a name="scap-extensions"></a>SCAP Uzantıları
SCAP Extensions 'ın yayın öncesi sürümü, Smssetup\tools\configmgrscapextension\configmgrextensionsforscap.exe altında bulunan CD. Latest klasöründe bulunabilir. SCAP uzantılarının bu yayın öncesi sürümü şu anda desteklenen Configuration Manager geçerli dalının ve LTSB 1606 sürümlerine yüklenebilir.



## <a name="next-steps"></a>Sonraki adımlar
Technical Preview dalını yükleme veya güncelleştirme hakkında daha fazla bilgi için bkz. [Configuration Manager Için Teknik Önizleme](technical-preview.md).    
