---
title: Windows 10 güncelleştirme teslimini en iyi duruma getirme
titleSuffix: Configuration Manager
description: Windows 10 ' da güncel kalmasını sağlamak üzere güncelleştirme içeriğini yönetmek için Configuration Manager nasıl kullanacağınızı öğrenin.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f16a5736d0bebbcb4f3b03989c6983cd55ac8f54
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696999"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Configuration Manager ile Windows 10 güncelleştirme teslimini iyileştirin

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Birçok müşteri için, Windows 10 aylık güncelleştirmelerini alma ve kullanmaya yönelik başarılı bir yol Configuration Manager kullanarak iyi bir içerik dağıtım stratejisiyle başlar. Aylık kalite güncelleştirmelerinin boyutu, büyük kuruluşlarda ilgili bir sorun olabilir. Güncelleştirme teslimini iyileştirmek için bant genişliği ve ağ yükünü azaltmaya yardımcı olmaya yönelik birkaç teknoloji mevcuttur. Bu makalede bu teknolojiler açıklanmakta, bunları karşılaştırılmaktadır ve hangisinin kullanılacağı konusunda kararlar almanıza yardımcı olacak öneriler sağlanır.  
 
Windows 10 çeşitli türlerde güncelleştirmeler sağlar. Daha fazla bilgi için bkz. [iş için Windows Update güncelleştirme türleri](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). Bu makale, Configuration Manager ile Windows 10 *kalite* güncelleştirmelerine odaklanır. 


## <a name="express-update-delivery"></a>Hızlı güncelleştirme teslimi

Windows 10 kaliteli güncelleştirme İndirmeleri büyük olabilir. Her paket, tutarlılık ve basitlik sağlamak için önceden yayımlanmış tüm düzeltmeleri içerir. Microsoft, her istemcinin Express adlı bir özellik ile indirdiği Windows 10 güncelleştirme içeriğinin boyutunu azaltabiliyor. Express bugün, güncelleştirmeleri doğrudan Windows Update hizmetinden çeken milyonlarca cihaz tarafından ve yükleme boyutunu önemli ölçüde azaltacak şekilde kullanılır. Bu avantaj, istemcileri Windows Update hizmetinden doğrudan indirmez olan müşteriler tarafından da kullanılabilir. 

Configuration Manager sürüm 1702 ' de Windows 10 kalite güncelleştirmelerinin [hızlı yükleme dosyaları](manage-express-installation-files-for-windows-10-updates.md) için destek eklendi. Bununla birlikte, en iyi deneyim için Configuration Manager sürüm 1802 veya sonraki bir sürümü kullanmanız önerilir. İndirme hızlarındaki en iyi performansı elde etmek için, Windows 10, sürüm 1703 veya sonraki bir sürümünü kullanmanız önerilir. 

> [!NOTE]  
> Express sürümü içeriği tam dosya sürümünden büyük ölçüde daha büyük. Bir hızlı yükleme dosyası, güncelleştirilmesi amaçlanan her bir dosyanın tüm olası çeşitlemelerini içerir. Sonuç olarak, Configuration Manager ' de hızlı desteği etkinleştirdiğinizde, güncelleştirme paketi kaynağındaki ve dağıtım noktalarındaki güncelleştirmeler için gereken disk alanı miktarı artar. Dağıtım noktalarındaki disk alanı gereksiniminin arttığı halde, istemcilerin bu dağıtım noktalarından indirdiği içerik boyutu azalır. İstemciler yalnızca ihtiyaç duydukları bitleri (deltas) indirir, ancak tüm güncelleştirmeyi kullanmaz.


## <a name="peer-to-peer-content-distribution"></a>Eşler arası içerik dağıtımı

İstemciler yalnızca ihtiyaç duydukları içeriğin parçalarını indirse de eşler arası içerik dağıtımını kullanarak ortamınızdaki Windows güncelleştirmelerini hızlandırın. Kalite güncelleştirmeleri için bir indirme kaynağı olarak eşler arasında yararlanmak, yerel dağıtım noktalarının Uzak ofislerde bulunmadığı ortamlar için yararlı olabilir. Bu davranış, tüm istemcilerin yavaş bir WAN bağlantısı üzerinden uzak bir dağıtım noktasından içerik indirmesi gereksinimini ortadan önler. İstemciler Windows Update hizmetine geri dönüşdiğinde eşleri kullanmak da yararlı olabilir. Diğer cihazların kullanabilmesi için buluttan güncelleştirme içeriğini indirmek için yalnızca bir eş gerekir.

Configuration Manager, aşağıdakiler dahil olmak üzere çok sayıda eşler arası teknolojiyi destekler:
- Windows teslim Iyileştirmesi
- Configuration Manager eş önbelleği
- Windows BranchCache  

Sonraki bölümlerde bu teknolojiler hakkında daha fazla bilgi sağlanmaktadır.

### <a name="windows-delivery-optimization"></a>Windows teslim Iyileştirmesi

[Teslim iyileştirme](/windows/deployment/update/waas-delivery-optimization) , Windows 10 ' da yerleşik olarak bulunan ana indirme teknolojisidir ve eşler arası dağıtım yöntemidir. Windows 10 istemcileri, yerel ağı üzerinde aynı güncelleştirmeleri yükleyen diğer cihazlardan içerik alabilir. [Teslim iyileştirme için kullanılabilen Windows seçeneklerini](/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options)kullanarak istemcileri gruplar halinde yapılandırabilirsiniz. Bu gruplandırma, kuruluşunuzun eşler arası istekleri karşılamak için büyük olasılıkla en iyi aday olan cihazları tanımlamasına olanak tanır. Teslim Iyileştirme, indirme süresini hızlandırırken cihazları güncel tutmak için kullanılan genel bant genişliğini önemli ölçüde azaltır.

> [!NOTE]  
> Teslim Iyileştirme, bulut tarafından yönetilen bir çözümdür. Teslim Iyileştirme bulut hizmetine Internet erişimi, eşler arası işlevselliğini kullanmak için bir gereksinimdir. Gerekli Internet uç noktaları hakkında daha fazla bilgi için bkz. [dağıtım iyileştirmesi hakkında sık sorulan sorular](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). 

En iyi sonuçlar için teslim Iyileştirme [indirme modunu](/windows/deployment/update/waas-delivery-optimization-reference#download-mode) **gruba (2)** ayarlamanız ve *grup kimliklerini*tanımlamanız gerekebilir. Grup modunda eşleme, uzak ofislerdeki cihazlar dahil olmak üzere aynı gruba ait olan cihazlar arasında iç alt ağları çapraz bir şekilde oluşturabilir. Etki alanlarından ve AD DS sitelerinden bağımsız olarak kendi özel grubunuzu oluşturmak için [Grup Kimliği seçeneğini](/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids) kullanın. Grup indirme modu, dağıtım Iyileştirmesi en iyi bant genişliği iyileştirmesine ulaşmak isteyen kuruluşların çoğu için önerilen seçenektir.

İstemcileri farklı ağlarda dolaşrsa, bu grup kimliklerinin el ile yapılandırılması zor olur. Configuration Manager sürüm 1802, [sınır gruplarını teslim iyileştirmesi ile tümleştirerek](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)bu işlemin yönetimini basitleştirmek için yeni bir özellik ekledi. İstemci uyandığında, ilkeleri almak için yönetim noktasıyla iletişim kurun ve ağ ve sınır grubu bilgilerini sağlar. Configuration Manager her sınır grubu için benzersiz bir KIMLIK oluşturur. Site, istemcinin teslim Iyileştirme grubu KIMLIĞINI Configuration Manager sınır KIMLIĞIYLE otomatik olarak yapılandırmak için istemcinin konum bilgilerini kullanır. İstemci başka bir sınır grubuna gezinse, yönetim noktasına yönlendirilir ve yeni bir sınır grubu KIMLIĞIYLE otomatik olarak yeniden yapılandırılır. Dağıtım Iyileştirmesi, bu tümleştirmeyle güncelleştirmelerin indirileceği bir eş bulmak için Configuration Manager sınır grubu bilgilerini kullanabilir.

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a> Sürüm 1910 ' den başlayarak teslim Iyileştirmesi
<!--4699118-->
Configuration Manager sürüm 1910 ' den başlayarak, yalnızca Express yükleme dosyalarını değil Windows 10 sürüm 1709 veya üstünü çalıştıran istemciler için tüm Windows Update içeriğinin dağıtımı için teslim Iyileştirmesi kullanabilirsiniz.

Tüm Windows Update yükleme dosyaları için teslim Iyileştirme 'yi kullanmak için aşağıdaki [yazılım güncelleştirmeleri istemci ayarlarını](../../core/clients/deploy/about-client-settings.md#software-updates)etkinleştirin:

- **Kullanılabilir olduğunda istemcilerin Delta içeriğini Indirmesine Izin ver** **.**
- **İstemcilerin Delta içerik için istekleri almak için kullandığı bağlantı noktası,** 8005 (varsayılan) veya özel bir bağlantı noktası numarası olarak ayarlanır.
 
> [!IMPORTANT]
> - Teslim Iyileştirme etkin olmalıdır (varsayılan) ve atlanmamalıdır. Daha fazla bilgi için bkz. [Windows teslim iyileştirme başvurusu](/windows/deployment/update/waas-delivery-optimization-reference).
> - Delta içeriği için [yazılım güncelleştirmeleri istemci ayarlarınızı](../../core/clients/deploy/about-client-settings.md#software-updates) değiştirirken [teslim iyileştirme istemci ayarlarınızı](../../core/clients/deploy/about-client-settings.md#delivery-optimization) doğrulayın.
> - Office COM etkinse, Microsoft 365 Apps istemci güncelleştirmeleri için teslim Iyileştirmesi kullanılamaz. Office COM, Configuration Manager tarafından Microsoft 365 Apps istemcilerine yönelik güncelleştirmeleri yönetmek için kullanılır. Microsoft 365 Apps güncelleştirmeleri için teslim Iyileştirmesi kullanılmasına izin vermek üzere Office COM kaydını silebilirsiniz. Office COM devre dışı bırakıldığında, Microsoft 365 uygulamalar için yazılım güncelleştirmeleri varsayılan Office otomatik güncelleştirmeler 2,0 zamanlanmış göreviyle yönetilir. Bu, Configuration Manager Microsoft 365 Apps güncelleştirmeleri için yükleme işlemini dikte etmiyor veya izmeyeceği anlamına gelir. Configuration Manager, konsolunda Office 365 Istemci yönetimi panosunu doldurmak üzere donanım envanterinden bilgi toplamaya devam edecektir. Office COM kaydını kaldırma hakkında bilgi için, bkz. [office 365 istemcilerinin Configuration Manager yerine OFFICE CDN 'den güncelleştirme almasını sağlama](/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).
> - İçerik depolaması için bir CMG kullanırken, kullanılabilir [istemci ayarı](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) etkinleştirildiğinde **Delta içeriğini indir** , üçüncü taraf güncelleştirmeler için içerik istemcilere indirmez. <!--6598587-->

#### <a name="configuration-recommendations-for-clients-downloading-delta-content"></a>Delta içeriğini indirirken istemciler için yapılandırma önerileri
<!--7913814-->
İstemciler yazılım güncelleştirme içeriği için kullanılabilir [istemci ayarı](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) etkinleştirildiğinde **Delta Içeriği Indirmelerine izin ver** , [dağıtım noktası geri dönüş](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_site-fallback) davranışında sınırlamalar vardır. Bu istemcilerin yazılım güncelleştirme içeriğini düzgün bir şekilde indirebilmeleri için aşağıdaki yapılandırmaların kullanılması önerilir:

- İstemcilerin bir sınır grubunda olduğundan ve bu sınır grubuyla ilişkili gereken içeriğe sahip güvenilir bir dağıtım noktası olduğundan emin olun.
- Doğrudan internet 'ten indirebilecek istemciler için Microsoft Update etkin olan yazılım güncelleştirmelerini dağıtın.
   - Bu geri dönüş davranışı için dağıtım ayarı, **yazılım güncelleştirmelerinin geçerli, komşu veya site sınır gruplarındaki dağıtım noktasında mevcut olmaması, Microsoft Updates 'ten içerik indirmesi** ve **indirme ayarları** sayfasında bulunur. Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini dağıtma](manually-deploy-software-updates.md#process-to-manually-deploy-the-software-updates-in-a-software-update-group).

Yukarıdaki seçeneklerden herhangi biri uygun değilse, istemcilerin, geri dönüşlerinin izin vermek için istemci ayarlarından devre dışı bırakılabilirler **Delta içeriğini Indirmesine Izin verin** . İstemci Delta kanalını kullanmayacaksa, bu durumda teslim Iyileştirme eşlemesi yararlanılabilir.

### <a name="configuration-manager-peer-cache"></a>Configuration Manager eş önbelleği

[Eş önbellek](../../core/plan-design/hierarchy/client-peer-cache.md) , istemcilerin doğrudan yerel Configuration Manager önbelleğinden diğer istemci içeriğiyle paylaşmasını sağlayan bir Configuration Manager özelliğidir. Eş önbellek, Windows BranchCache gibi diğer eş önbelleğe alma çözümlerinin kullanımını değiştirmez. Dağıtım noktaları gibi geleneksel içerik dağıtım çözümlerini genişletmek için daha fazla seçenek sağlamak üzere bunlarla birlikte çalışabilir. Eş önbellek BranchCache 'e bağlı değil. BranchCache 'i etkinleştirmezseniz veya kullanmıyorsanız, eş önbellek hala işe yarar.

> [!NOTE]  
> İstemciler yalnızca geçerli sınır grubundaki eş önbellek istemcilerinden içerik indirebilir.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](/windows-server/networking/branchcache/branchcache) , Windows 'da bir bant genişliği iyileştirme teknolojisidir. Her istemci bir önbelleğe sahiptir ve içerik için alternatif bir kaynak olarak davranır. Aynı ağdaki cihazlar bu içeriği talep edebilir. [Configuration Manager,](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) her biri ve bir dağıtım noktasıyla iletişim kurmak için birbirleriyle kaynak içeriğe yönelik eşler sağlamak üzere BranchCache kullanabilir. BranchCache kullanarak, dosyalar her bir istemcide önbelleğe alınır ve diğer istemciler bunları gerektiği gibi alabilir. Bu yaklaşım, tek bir alım noktası olması yerine önbelleği dağıtır. Bu davranış, istemcilerin istenen içeriği alma süresini azalttığından önemli miktarda bant genişliği kaydeder.



## <a name="selecting-the-right-peer-caching-technology"></a>Doğru eş önbelleğe alma teknolojisini seçme

Hızlı yükleme dosyaları için doğru eş önbelleğe alma teknolojisinin seçilmesi ortamınıza ve gereksinimlerinize bağlıdır. Configuration Manager, yukarıdaki eşler arası teknolojilerin tümünü desteklese de, ortamınız için en mantıklı olan bunları kullanmanız gerekir. Müşterilerin, teslim Iyileştirmesi için Internet gereksinimlerini karşılayabilecek olduğu varsayıldığında, teslim iyileştirmesine sahip Windows 10 yerleşik eş önbelleğe alma yeterli olmalıdır. İstemcileriniz bu internet gereksinimlerini karşılamazsa, Configuration Manager eş önbelleği özelliğini kullanmayı göz önünde bulundurun. Şu anda Configuration Manager ile BranchCache kullanıyorsanız ve tüm ihtiyaçlarınızı karşılıyorsa, BranchCache ile hızlı dosyalar sizin için doğru seçenek olabilir. 

### <a name="peer-cache-comparison-chart"></a>Eş önbellek karşılaştırma grafiği


| İşlev  | Teslim Iyileştirme  | Eş önbellek  | BranchCache  |
|---------|---------|---------|---------|
| Alt ağlar arasında destekleniyor | Evet | Evet | Hayır |
| Bant genişliği azaltma | Evet (yerel) | Evet (BITS aracılığıyla) | Evet (BITS aracılığıyla) |
| Kısmi içerik desteği | Evet, bu sütunda listelenen tüm desteklenen içerik türleri için bir sonraki satırda. | Yalnızca Microsoft 365 uygulamalar ve hızlı güncelleştirmeler için | Evet, bu sütunda listelenen tüm desteklenen içerik türleri için bir sonraki satırda. |
| Desteklenen içerik türleri | **ConfigMgr aracılığıyla:** </br> -Hızlı güncelleştirmeler </br> -Tüm Windows güncelleştirmeleri (sürüm 1910 ' den başlayarak). Bu, Microsoft 365 uygulama güncelleştirmeleri içermez.</br> </br> **Microsoft bulutu aracılığıyla:**</br> -Windows ve güvenlik güncelleştirmeleri</br> -Sürücüler</br> -Windows Mağazası uygulamaları</br> -Iş için Windows Mağazası uygulamaları | [WINDOWS PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) 'de indirilen görüntüler dahil tüm ConfigMgr içerik türleri | Tüm ConfigMgr içerik türleri, görüntüler hariç |
| Disk denetimindeki önbellek boyutu | Evet | Evet | Evet |
| Eş kaynağı bulma | Automatic | El ile (istemci Aracısı ayarı) | Automatic |
| Eş keşfi | Teslim Iyileştirme bulut hizmeti aracılığıyla (internet erişimi gerektirir) | Yönetim noktası aracılığıyla (istemci sınır gruplarına göre) | Noktalı |
| Raporlama | Evet (Masaüstü analizlerini kullanarak) | ConfigMgr istemci veri kaynakları panosu | ConfigMgr istemci veri kaynakları panosu |
| WAN kullanım denetimi | Evet (yerel, Grup İlkesi ayarları aracılığıyla denetlenebilirler) | Sınır grupları | Yalnızca alt ağ desteği |
| ConfigMgr aracılığıyla yönetim | Kısmi (istemci Aracısı ayarı) | Evet (istemci Aracısı ayarı) | Evet (istemci Aracısı ayarı) |



## <a name="conclusion"></a>Sonuç

Microsoft, gereken şekilde, hızlı yükleme dosyaları ve eş önbelleğe alma teknolojisiyle Configuration Manager kullanarak Windows 10 kaliteli güncelleştirme teslimini iyileştirmenizi önerir. Bu yaklaşım, kalite güncelleştirmelerini yüklemek için büyük içerikleri indirerek Windows 10 cihazlarıyla ilgili güçlükleri hafiflemelidir. Windows 10 cihazlarının kaliteli güncelleştirmeleri dağıtarak güncel tutulması de önerilir. Bu uygulama, her ay cihazlar için gereken kaliteli güncelleştirme içeriği değişimini azaltır. Bu içerik değişimini azaltmak, dağıtım noktalarından veya eş kaynaklardan daha küçük boyutlu indirmelere neden olur. 

Hızlı yükleme dosyalarının doğası nedeniyle, içerik boyutları geleneksel kendi içindeki dosyalardan oldukça büyük. Bu boyut, Windows Update hizmetinden Configuration Manager site sunucusuna güncelleştirme indirme sürelerinin uzamasına neden olur. Hem site sunucusu hem de dağıtım noktaları için gereken disk alanı miktarı da artar. Kalite güncelleştirmelerinin indirilmesi ve dağıtılması için gereken toplam süre daha uzun olabilir. Ancak, Windows 10 cihazlar tarafından kalite güncelleştirmelerinin indirilmesi ve yüklenmesi sırasında cihaz tarafı avantajları dikkat edilmelidir. Daha fazla bilgi için bkz. [hızlı yükleme dosyalarını kullanma](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)#using-express-installation-files).

Daha büyük boyutlu güncelleştirmelerin sunucu tarafı avantajları hızlı destek benimseme için engelleyiciler ise, ancak cihaz tarafı avantajları iş ve ortamınız açısından önemliyse, Microsoft, Configuration Manager [iş için Windows Update](integrate-windows-update-for-business-windows-10.md) kullanmanızı önerir. Iş için Windows Update, hızlı yükleme dosyalarını ortamınızda indirme, depolama ve dağıtmaya gerek kalmadan hızlı bir şekilde tüm avantajların avantajlarından yararlanmanızı sağlar. İstemciler içeriği doğrudan Windows Update hizmetinden indirir, bu nedenle teslim Iyileştirme kullanmaya devam edebilir.



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Sık sorulan sorular

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Windows Express nasıl yüklenir Configuration Manager?

Windows Update Aracısı (WUA) öncelikle içerik Express 'i ister. Hızlı güncelleştirme yüklenemediğinde, tam dosya güncelleştirmesine geri dönebilirler.  

1. Configuration Manager istemcisi WUA 'nin güncelleştirme içeriğini indirmesini söyler. WUA bir hızlı indirmeyi başlattığında, öncelikle Express paketinin bir parçası olan bir saplaması (örneğin, `Windows10.0-KB1234567-<platform>-express.cab` ) indirir.  

2. WUA bu saplamaya Windows Update yükleyicisi, bileşen tabanlı hizmet (CBS) geçirir. CBS, bir yerel sayım yapmak için saplama kullanır ve bu, cihazdaki dosyanın değişimleri öğesini, sunulan dosyanın en son sürümüne ulaşmak için gereken şekilde karşılaştırır.  

3. CBS daha sonra WUA 'dan gerekli aralıkları bir veya daha fazla Express. PSF dosyasından indirmesini ister.  

4. Teslim Iyileştirme etkinse ve eşler gerekli aralıklara sahip olacak şekilde bulunursa, istemci, eşler tarafından ConfigMgr istemcisinden bağımsız olarak indirilir. Teslim Iyileştirme devre dışıysa veya hiçbir eş gerekli aralıklara sahip değilse, ConfigMgr istemcisi bu aralıkları yerel bir dağıtım noktasından (veya bir eş veya Microsoft Update) indirir. Aralıklar, aralıkları uygulamak için CBS tarafından kullanılabilir hale getiren Windows Update aracısına geçirilir.


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Ccmcache klasöründe Configuration Manager eş kaynakları üzerinde depolandığında hızlı dosyalar (. PSF) neden çok büyük?

Hızlı dosyalar (. PSF) seyrek dosyalardır. Diskte kullanılmakta olan gerçek alanı öğrenmek için dosyanın **disk üzerindeki boyut** özelliğini denetleyin. Disk üzerindeki boyut, boyut değerinden önemli ölçüde daha küçük olmalıdır.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Configuration Manager Windows 10 özellik güncelleştirmeleriyle Express yükleme dosyalarını destekler mi?

Hayır, Configuration Manager şu anda yalnızca Windows 10 kalite güncelleştirmeleriyle Express yükleme dosyalarını desteklemektedir.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Site sunucusunda ve dağıtım noktalarında kalite güncelleştirmesi başına ne kadar disk alanı gerekir?

Duruma göre değişir. Her kalite güncelleştirmesi için, güncelleştirmenin tam dosya ve Express sürümü sunucularda depolanır. Windows 10 kalite güncelleştirmeleri birikimlidir, bu nedenle bu dosyaların boyutu her ay artar. Her dil için güncelleştirme başına en az 5 GB planlayın. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Configuration Manager istemciler Windows Update hizmetine geri döndüğünüzde hızlı yükleme dosyalarından hala faydalanır mi?

Evet. Aşağıdaki yazılım güncelleştirme dağıtım seçeneğini kullanırsanız, istemciler bulut hizmetine geri döntiklerinde yine de hızlı güncelleştirmeleri ve teslim Iyileştirmesini kullanır:  

**Güncel, komşu veya site gruplarındaki dağıtım noktasında yazılım güncelleştirmeleri yoksa, Microsoft Updates 'ten içerik indirin**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Hızlı dosya desteğini etkinleştirdikten sonra neden mevcut güncelleştirmeler için hızlı dosya içeriği indirilmiyor? 

Değişiklikler yalnızca, destek etkinleştirildikten sonra eşitlenmiş ve dağıtılan yeni güncelleştirmeler için geçerli olur.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Teslim Iyileştirme kullanarak eşlerden ne kadar içerik indirildiğini görmenin bir yolu var mı?
Windows 10, sürüm 1703 (ve üzeri), iki yeni PowerShell cmdlet 'i, **Get-teslimat Yoptimizationperfsnap** ve **Get-teslimat Yoptimizationstatus**içerir. Bu cmdlet 'ler teslim Iyileştirme ve önbellek kullanımıyla ilgili daha ayrıntılı bilgiler sağlar. Daha fazla bilgi için bkz. [Windows 10 güncelleştirmeleri Için teslim iyileştirmesi](/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>İstemciler ağ üzerinden teslim Iyileştirmesi ile nasıl iletişim kurar?
Ağ bağlantı noktaları, proxy gereksinimleri ve güvenlik duvarları için ana bilgisayar adları hakkında daha fazla bilgi için bkz. [dağıtım iyileştirmesi Için SSS](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

## <a name="log-files"></a>Günlük dosyaları

Delta İndirmeleri izlemek için aşağıdaki günlük dosyalarını kullanın:

- WUAHandler.log
- DeltaDownload. log

## <a name="next-steps"></a>Sonraki adımlar

- [Yazılım güncelleştirmelerini dağıtma](deploy-software-updates.md)
- [Yazılım güncelleştirmelerini otomatik dağıtma](automatically-deploy-software-updates.md)