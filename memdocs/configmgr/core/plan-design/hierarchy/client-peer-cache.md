---
title: İstemci eş önbelleği
titleSuffix: Configuration Manager
description: Configuration Manager ile içerik dağıtımında kaynak konumları için istemci eş önbelleğini kullanın.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c302e839c2a41ba27d160db24928f7e202de78dc
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110194"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Configuration Manager istemcileri için eş önbellek

*Uygulama hedefi: Configuration Manager (geçerli dal)*

<!--1101436-->
Uzak konumlardaki istemcilere içerik dağıtımını yönetmeye yardımcı olması için eş önbellek kullanın. Eş önbellek, istemcilerin diğer istemcilerle doğrudan yerel Önbelleklerinden içerik paylaşmasını sağlayan yerleşik bir Configuration Manager çözümüdür.   

> [!Note]  
> Sürüm 1906 ' de, Configuration Manager Bu özelliği varsayılan olarak sunar. Sürüm 1902 veya önceki sürümlerde, bu isteğe bağlı özelliği varsayılan olarak etkinleştirmez Configuration Manager. Bu özelliği kullanmadan önce etkinleştirmeniz gerekir. Daha fazla bilgi için, bkz. [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  



## <a name="overview"></a>Genel Bakış

Tanımlar  

- **Eş önbellek istemcisi**: bir eşten içerik indiren tüm Configuration Manager istemcileri  

- **Eş önbellek kaynağı**: eş önbellek için etkinleştirdiğiniz ve diğer istemcilerle paylaşılacak içeriğe sahip bir Configuration Manager istemcisi  

İstemcilerin eş önbellek kaynakları olmasını sağlamak için istemci ayarlarını kullanın. Eş önbellek istemcilerini etkinleştirmeniz gerekmez. İstemcilerin eş önbellek kaynakları olmasını etkinleştirdiğinizde, yönetim noktası bunları içerik konumu kaynakları listesine ekler.<!--510397--> Bu işlem hakkında daha fazla bilgi için bkz. [işlemler](#operations).  

Eş önbellek kaynağı, eş önbellek istemcisinin geçerli sınır grubunun bir üyesi olmalıdır. Yönetim noktası, istemci sağlayan içerik kaynakları listesindeki bir komşu sınır grubundan eş önbellek kaynakları içermez. Yalnızca bir komşu sınır grubundan dağıtım noktaları içerir. Geçerli ve komşu sınır grupları hakkında daha fazla bilgi için bkz. [sınır grupları](../../servers/deploy/configure/boundary-groups.md).<!--SCCMDocs issue 685-->  

Configuration Manager istemcisi, önbellekteki her içerik türüne diğer istemcilere hizmet vermek için eş önbelleği kullanır. Bu içerik, kurumsal dosyalar ve hızlı yükleme dosyaları için Microsoft 365 uygulamalar içerir.<!--SMS.500850-->  

Eş önbellek, Windows BranchCache veya teslim Iyileştirme gibi diğer çözümlerin kullanımını değiştirmez. Eş önbellek diğer çözümlerle birlikte çalışmaktadır. Bu teknolojiler, dağıtım noktaları gibi geleneksel içerik dağıtım çözümlerini genişletmek için size daha fazla seçenek sunar. Eş önbellek, BranchCache üzerinde hiçbir rahatlık olmadan özel bir çözümdür. BranchCache 'i etkinleştirmezseniz veya kullanmıyorsanız, eş önbellek hala işe yarar.  

> [!Note]  
> Sürüm 1802 ' den başlayarak, dağıtımlar üzerinde Windows BranchCache her zaman etkindir. **İstemcilerin aynı alt ağdaki diğer istemcilerle içerik paylaşmasına Izin verme** ayarı kaldırılır.<!--SCCMDocs issue 539--> Dağıtım noktası destekliyorsa ve istemci ayarlarında etkinleştirildiyse, istemciler BranchCache kullanır. Daha fazla bilgi için bkz. [BranchCache yapılandırma](../../clients/deploy/about-client-settings.md#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>İşlemler

Eş önbelleği etkinleştirmek için, [istemci ayarlarını](#bkmk_settings) bir koleksiyona dağıtın. Ardından, bu koleksiyonun üyeleri aynı sınır grubundaki diğer istemciler için eş önbellek kaynağı görevi görür.  

- Eş içerik kaynağı olarak çalışan bir istemci, kullanılabilir önbelleğe alınmış içeriğin listesini durum iletilerini kullanarak yönetim noktasına gönderir.

   > [!NOTE]
   > 7200, 7201, 7202 ve 7203 durum iletisi kimliklerine sahip olan ilgili eşdüzey içerik kaynağı durum iletilerinin listesi için [Configuration Manager durum iletilerine](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map) bakın.

- Aynı sınır grubundaki başka bir istemci, yönetim noktasına bir içerik konumu isteği yapar. Sunucu olası içerik kaynakları listesini döndürür. Bu liste, içeriğe sahip ve çevrimiçi olan her eş önbellek kaynağını içerir. Ayrıca, bu sınır grubundaki dağıtım noktalarını ve diğer içerik kaynak konumlarını da içerir. Daha fazla bilgi için bkz. [içerik kaynağı önceliği](fundamental-concepts-for-content-management.md#content-source-priority).  

- Her zamanki gibi, içeriği arayan istemci, belirtilen listeden bir kaynak seçer. İstemci daha sonra içeriği almaya çalışır.  

Sürüm 1806 ' den başlayarak, sınır grupları ortamınızda içerik dağıtımı üzerinde daha fazla denetim sağlamak için ek ayarlar içerir. Daha fazla bilgi için bkz. [eş İndirmeleri Için sınır grubu seçenekleri](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> İstemci içerik için bir komşu sınır grubuna geri düşerse, yönetim noktası eş önbellek kaynaklarını komşu sınır grubundan olası içerik kaynağı konumları listesine eklemez.  

Yalnızca eş önbellek kaynakları olarak en uygun istemcileri seçin. Kasa türü, disk alanı ve ağ bağlantısı gibi özniteliklere göre istemci uygunluğunu değerlendirin. Eş önbellek için kullanılacak en iyi istemcileri seçmenize yardımcı olabilecek daha fazla bilgi için, [Microsoft danışman tarafından bu bloga](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801)bakın.


### <a name="limited-access-to-a-peer-cache-source"></a>Eş önbellek kaynağına sınırlı erişim  

Eş önbellek kaynağı, bir eşin içerik istemesi durumunda aşağıdaki koşullardan herhangi birini karşıladığında içerik isteklerini reddeder:  

- Düşük pil modu  

- İşlemci yükü %80 ' ü aşıyor  

- Disk g/ç, 10 ' u aşan bir *Avgdiskqueuelength* öğesine sahiptir  

- Bilgisayar için kullanılabilir başka bağlantı yok  

> [!Tip]  
> Bu ayarları, Configuration Manager SDK 'sindeki eş kaynak özelliği (*SMS_WinPEPeerCacheConfig*) için istemci yapılandırma sunucusu WMI sınıfını kullanarak yapılandırın.  

Eş önbellek kaynağı içerik için bir isteği reddettiğinde, eş önbellek istemcisi içerik kaynak konumları listesinden içerik aramaya devam eder.   



## <a name="requirements"></a>Gereksinimler

- Eş önbellek [, istemciler ve cihazlar Için desteklenen işletim sistemlerinde](../configs/supported-operating-systems-for-clients-and-devices.md)desteklenmiş gibi listelenen tüm Windows sürümlerini destekler. Windows dışı işletim sistemleri, eş önbellek kaynakları veya eş önbellek istemcileri olarak desteklenmez.  

- Eş önbellek kaynağı, etki alanına katılmış bir Configuration Manager istemcisi olmalıdır. Ancak, etki alanına katılmış olmayan bir istemci, etki alanına katılmış bir eş önbellek kaynağından içerik alabilir.  

- İstemciler, yalnızca geçerli sınır grubundaki eş önbellek kaynaklarından içerik indirebilir.  

- Şu özel durumla bir [ağ erişim hesabı](accounts.md#network-access-account) gerekli değildir:  

  - Eş önbellek özellikli bir istemci yazılım merkezinden bir görev sırası çalıştırdığında sitede bir ağ erişim hesabı yapılandırın ve bir önyükleme görüntüsüne yeniden başlatılır. Cihaz Windows PE 'de olduğunda, eş önbellek kaynağından içerik almak için ağ erişim hesabını kullanır.  

  - Gerektiğinde, eş önbellek kaynağı, eşlerden gelen indirme isteklerinin kimliğini doğrulamak için ağ erişim hesabını kullanır. Bu hesap, bu amaçla yalnızca etki alanı kullanıcı izinleri gerektirir.  

- Sürüm 1802 ve öncesinde, istemcinin en son sinyal bulma gönderimi, eş önbellek kaynağının geçerli sınırını belirler. Farklı bir sınır grubuna dolaşmakta olan bir istemci, eş önbellek amaçları için eski sınır grubunun bir üyesi olmaya devam edebilir. Bu davranış, bir istemcinin kendi ağ konumunda olmayan bir eş önbellek kaynağı olarak sunulmasına neden olur. Gezici istemcileri eş önbellek kaynağı olarak etkinleştirmeyin.<!--SCCMDocs issue 641-->  

  > [!Important]  
  > Sürüm 1806 ' den başlayarak, eş önbellek kaynağının başka bir konuma dolaşıma alındığını belirlemek için Configuration Manager daha etkilidir. Bu davranış, yönetim noktasının, eski konumda değil, yeni konumdaki istemcilere içerik kaynağı olarak sunabilmesini sağlar. Eş önbellek özelliğini gezici eş önbellek kaynaklarıyla kullanıyorsanız, siteyi sürüm 1806 ' e güncelleştirdikten sonra tüm eş önbellek kaynaklarını en son istemci sürümüne de güncelleştirin. Yönetim noktası, en az sürüm 1806 ' e güncelleştirilene kadar bu eş önbellek kaynaklarını içerik konumları listesinde içermez.<!--SCCMDocs issue 850-->  

- İçeriği indirmeyi denemeden önce, yönetim noktası ilk olarak eş önbellek kaynağının çevrimiçi olduğunu doğrular.<!--sms.498675--> Bu doğrulama, TCP bağlantı noktası 10123 kullanan istemci bildirimi için "hızlı kanal" aracılığıyla yapılır.<!--511673-->  

> [!Note]  
> Yeni Configuration Manager özelliklerinden yararlanmak için önce istemcileri en son sürüme güncelleştirin. Site ve konsolu güncelleştirdiğinizde Configuration Manager konsolunda yeni işlevsellik göründüğünde, istemci sürümü de en son olana kadar, tüm senaryo işlevsel değildir.  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a>Eş önbellek istemci ayarları

Eş önbellek istemci ayarları hakkında daha fazla bilgi için bkz. [istemci önbellek ayarları](../../clients/deploy/about-client-settings.md#client-cache-settings). 

Bu ayarları yapılandırma hakkında daha fazla bilgi için bkz. [istemci ayarlarını yapılandırma](../../clients/deploy/configure-client-settings.md).

Windows Güvenlik Duvarı 'nı kullanan eş önbellek özellikli istemcilerde, Configuration Manager istemci ayarlarında belirttiğiniz güvenlik duvarı bağlantı noktalarını yapılandırır.



## <a name="partial-download-support"></a><a name="bkmk_parts"></a>Kısmi indirme desteği
<!--1357346-->
Sürüm 1806 ' den başlayarak, istemci eş önbelleği kaynakları artık içeriği parçalara ayırabiliyor. Bu parçalar, WAN kullanımını azaltmak için Ağ aktarımını en aza indirir. Yönetim noktası, içerik bölümlerinin daha ayrıntılı bir şekilde izlenmesini sağlar. Aynı içeriğin her sınır grubu için birden fazla indirilmesini ortadan kaldırmaya çalışır. 


### <a name="example-scenario"></a>Örnek senaryo

Contoso, iki sınır grubuna sahip tek bir birincil siteye sahiptir: Merkez (HQ) ve şube ofisi. Sınır grupları arasında 30 dakikalık bir geri dönüş ilişkisi vardır. Site için yönetim noktası ve dağıtım noktası yalnızca HQ sınırında bulunur. Şube ofis konumunun Yerel dağıtım noktası yok. Şube ofisindeki dört istemciden ikisi eş önbellek kaynakları olarak yapılandırılır. 

![Örnek senaryo için açıklandığı şekilde ağ yapılandırması diyagramı](media/1357346-peer-cache-source-parts.png)

1. Şube ofisindeki tüm dört istemci için içerik içeren bir dağıtımı hedefleyebilirsiniz. İçeriği yalnızca dağıtım noktasına dağıtım.  

2. Client3 ve Client4 dağıtım için yerel bir kaynak içermez. Yönetim noktası, istemcileri uzak sınır grubuna geri dönmeden önce 30 dakika beklemesini söyler.  

3. İSTEMCİ1 (PCS1), ilkeyi yönetim noktasıyla yenilemek için ilk eş önbellek kaynağıdır. Bu istemci bir eş önbellek kaynağı olarak etkinleştirildiğinden, yönetim noktası bunu dağıtım noktasından bir bölümünü hemen indirmeyi ister.  

4. Istemci2 (PCS2) yönetim noktasıyla iletişim kurduğunda, bir parçası zaten devam ediyor ancak henüz tamamlanmadığında, yönetim noktası bunu dağıtım noktasından B bölümünü hemen indirmeyi ister.  

5. PCS1, A bölümünü indirmeyi tamamlar ve anında yönetim noktasına bildirir. B bölümü zaten devam ettiğinden ancak henüz tamamlanmadığında, yönetim noktası bunu dağıtım noktasından C bölümünü indirmeye başlamasını söyler.  

6. PCS2 B bölümünü indirmeyi tamamlar ve yönetim noktasına anında bildirir. Yönetim noktası, bunu dağıtım noktasından D bölümünü indirmeye başlamasını söyler.  

7. PCS1, Bölüm C 'yi indirmeyi tamamlar ve anında yönetim noktasına bildirir. Yönetim noktası, uzak dağıtım noktasından daha fazla kullanılabilir bölüm olmadığını bildirir. Yönetim noktası, PCS2 'in yerel eşinden B bölümünü indirmesini söyler.  

8. Bu işlem, her iki istemci eş önbelleği kaynağına ait tüm parçalar olana kadar devam eder. Yönetim noktası, eş önbellek kaynaklarını yerel eşlerden bölümleri indirmek üzere bir daha vermeden önce uzak dağıtım noktasından bölümleri önceliklendirir.  

9. Client3, 30 dakikalık geri dönüş döneminin süresi dolduktan sonra ilkeyi Yenileme ilkdir. Şimdi, yeni yerel kaynakları istemciye bildiren yönetim noktası ile geri kontrol eder. İçeriğin WAN genelindeki dağıtım noktasından tam olarak indirilmesi yerine, içeriği istemci eş önbelleği kaynaklarından birinden tam olarak indirir. İstemciler, yerel eş kaynakları önceliklendirdir. 

> [!Note]  
> İstemci eş önbelleği kaynaklarının sayısı, içerik bölümlerinin sayısından büyükse, yönetim noktası ek eş önbellek kaynaklarını normal bir istemci gibi geri dönüşü bekleyecek şekilde yönlendirir. 


### <a name="configure-partial-download"></a>Kısmi indirmeyi Yapılandır

1. [Sınır gruplarını](../../servers/deploy/configure/boundary-groups.md) ve eş önbellek kaynaklarını normal başına ayarlayın.  

2. Configuration Manager konsolunda **Yönetim** çalışma alanına gidin, **Site yapılandırması**' nı genişletin ve **siteler**' i seçin. Şeritte **Hiyerarşi ayarları** ' na tıklayın.  

3. **Genel** sekmesinde, **içeriği parçalara bölmek için istemci eş önbelleği kaynaklarını yapılandırma**seçeneğini etkinleştirin.  

4. İçerikle gerekli bir dağıtım oluşturun.  

   > [!Note]  
   > Bu işlev yalnızca istemci, gerekli bir dağıtım gibi arka planda içerik indirdiğinde geçerlidir. Kullanıcının yazılım merkezi 'nde kullanılabilir bir dağıtımı yüklemesi gibi isteğe bağlı indirmeler her zamanki gibi davranır.  

İçeriğin parçalar halinde indirilmesini işlemesini görmek için, istemci eş önbelleği kaynağında **ContentTransferManager. log** ' u ve yönetim noktasındaki **MP_Location. log** dosyasını inceleyin.  



## <a name="guidance-for-cache-management"></a>Önbellek Yönetimi Kılavuzu
<!--510645-->
Eş önbellek, içerik paylaşmak için Configuration Manager istemci önbelleğine bağımlıdır. Ortamınızdaki istemci önbelleğini yönetmek için aşağıdaki noktaları göz önünde bulundurun:  

- Configuration Manager istemci önbelleği, bir dağıtım noktasındaki içerik kitaplığı gibi değildir. Bir dağıtım noktasına dağıttığınız içeriği yönetirken, Configuration Manager istemcisi içeriği önbelleğinde otomatik olarak yönetir. Eş önbellek kaynağı önbelleğindeki içeriğin ne olduğunu denetlemeye yardımcı olacak ayarlar ve yöntemler vardır. Daha fazla bilgi için bkz. [Configuration Manager istemcileri için istemci önbelleğini yapılandırma](../../clients/manage/manage-clients.md#BKMK_ClientCache).  

- Normal önbellek boyutu ve bakım, eş önbellek kaynakları için geçerlidir. Daha fazla bilgi için bkz. [istemci önbellek boyutunu yapılandırma](../../clients/deploy/about-client-settings.md#configure-client-cache-size). İşletim sistemi yükseltme paketleri veya Windows 10 Express güncelleştirme dosyaları gibi daha büyük içeriklerin boyutunu göz önünde bulundurun. Bu içeriğe yönelik gereksiniminizi eş önbellek kaynaklarındaki kullanılabilir disk alanına göre karşılaştırın.  

- Eş önbellek kaynak istemcisi, bir eş tarafından indirildiğinde önbellekteki içeriğin son başvurulan zamanını güncelleştirir. İstemci, önbelleğini otomatik olarak koruduğu zaman damgasını kullanır, önce eski içerikleri kaldırır. Bu nedenle, eş önbellek istemcilerinin tümünde daha sık indirileceği içeriği kaldırmayı beklemesi gerekir.  

- Gerekirse, bir işletim sistemi dağıtımı görev sırası sırasında, içeriği istemci önbelleğinde tutmak için **SMSTSPreserveContent** değişkenini kullanın. Daha fazla bilgi için bkz. [görev dizisi değişkenleri](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent).  

- Gerekirse, aşağıdaki yazılımı oluştururken **içeriği istemci önbelleğinde kalıcı hale**getirmek için seçeneğini kullanın:  
  - Uygulamalar
  - Paketler
  - İşletim sistemi görüntüleri
  - İşletim sistemi yükseltme paketleri
  - Önyükleme görüntüleri



## <a name="monitoring"></a>İzleme   

Eş önbelleğinin kullanımını anlamanıza yardımcı olması için **Istemci veri kaynakları** panosunu görüntüleyin. Daha fazla bilgi için bkz. [istemci veri kaynakları panosu](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

Ayrıca, eş önbellek kullanımını görüntülemek için raporları kullanın. Konsolunda **izleme** çalışma alanına gidin, **Raporlama**' yı genişletin ve **raporlar** düğümünü seçin. Aşağıdaki raporların hepsi bir tür **yazılım dağıtım içeriğine**sahiptir:  

1.  **Eş önbellek kaynağı içerik reddi**: sınır grubundaki eş önbellek kaynaklarının bir içerik isteğini reddetme sıklığı.  

    > [!Note]  
    > **Bilinen sorun**<!--486652-->: *MaxCPULoad* veya *Maxdiskio*gibi sonuçlarda detaya gidilirken, raporu veya ayrıntıları öneren bir hata alabilirsiniz. Bu sorunu geçici olarak çözmek için, sonuçları doğrudan gösteren diğer iki raporu kullanın.  

2. **Koşula göre eş önbellek kaynağı içeriğini reddetme**: belirtilen sınır grubu veya reddetme türü için reddetme ayrıntılarını gösterir. 

    > [!Note]  
    > **Bilinen sorun**<!--486652-->: Kullanılabilir parametrelerden seçim yapamazsınız, bunun yerine bunları el ile girmeniz gerekir. *Sınır grubu adı* ve *reddetme türü* değerlerini **eş önbellek kaynağı içerik reddetme** raporunda göründüğü şekilde girin. Örneğin, *ret türü* için *MaxCPULoad* veya *maxdiskio*girebilirsiniz.  

3. **Eş önbellek kaynağı içerik reddetme ayrıntıları**: istemcinin reddedildiğinde istediği içeriği gösterir.  

    > [!Note]  
    > **Bilinen sorun**<!--486652-->: Kullanılabilir parametrelerden seçim yapamazsınız, bunun yerine bunları el ile girmeniz gerekir. **Eş önbellek kaynağı içerik reddetme** raporunda gösterildiği gibi *reddetme türü* için değeri girin. Daha sonra hakkında daha fazla bilgi edinmek istediğiniz içerik kaynağı için *kaynak kimliğini* girin. 
    > 
    > İçerik kaynağının kaynak KIMLIĞINI bulmak için:  
    > 
    > 1. **Koşula göre eş önbellek kaynağı içeriğini reddetme** raporu sonuçlarında *eş önbellek kaynağı* olarak görüntülenen bilgisayar adını bulun.  
    > 
    > 2. **Varlıklar ve uyum** çalışma alanına gidin, **cihazlar** düğümünü seçin ve bu bilgisayarın adını arayın. Kaynak KIMLIĞI sütunundaki değeri kullanın.  

