---
title: Sınır gruplarını yapılandırma
titleSuffix: Configuration Manager
description: Sınırlar adlı ilgili ağ konumlarını mantıksal olarak düzenlemek için istemcilerin sınır gruplarını kullanarak site sistemlerini bulmasına yardımcı olma
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce77c43f49556b3a60e36f05127f82d4d135762a
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643256"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Configuration Manager için sınır grupları yapılandırma

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Altyapınızı yönetmeyi kolaylaştırmak için ilgili ağ konumlarını ([sınırlar](boundaries.md)) mantıksal olarak düzenlemek üzere Configuration Manager içindeki sınır gruplarını kullanın. Sınır grubunu kullanmadan önce sınır gruplarına sınırlar atayın.

Varsayılan olarak, Configuration Manager her sitede varsayılan bir site sınır grubu oluşturur.

Sınır gruplarını yapılandırmak için, sınırları (ağ konumları) ve dağıtım noktaları gibi site sistem rollerini sınır grubuna ilişkilendirin. Bu yapılandırma, istemcileri ağdaki istemcilerin yakınında bulunan dağıtım noktaları gibi site sistem sunucularıyla ilişkilendirmenize yardımcı olur.

Sunucuların kullanılabilirliğini daha geniş bir ağ konumu aralığına yükseltmek için aynı sınırı ve aynı sunucuyu birden fazla sınır grubuna atayın.

İstemciler için bir sınır grubu kullanır:  

- Otomatik site ataması  
- Hizmet sağlayabilecek bir site sistemi sunucusunu bulmak için şunlar da dahildir:

  - İçerik konumu için dağıtım noktaları  
  - Yazılım güncelleştirme noktaları  
  - Durum geçiş noktaları  

    > [!NOTE]
    > Durum geçiş noktası, geri dönüş ilişkilerini kullanmaz. Daha fazla bilgi için bkz. [geri dönüş](#fallback).

  - Tercih edilen yönetim noktaları  

    > [!NOTE]  
    > Tercih edilen yönetim noktalarını kullanırsanız, hiyerarşi için bu seçeneği, sınır grubu yapılandırmasının içinden değil, etkinleştirin. Daha fazla bilgi için bkz. [tercih edilen yönetim noktalarının kullanımını etkinleştirme](boundary-group-procedures.md#bkmk_proc-prefer).  

  - Bulut yönetimi ağ geçidi (sürüm 1902 ' den başlayarak)

## <a name="boundary-groups-and-relationships"></a>Sınır grupları ve ilişkiler

Hiyerarşinizdeki her sınır grubu için şunları atayabilirsiniz:

- Bir veya daha fazla sınır. Bir istemcinin **geçerli** sınır grubu, belirli bir sınır grubuna atanmış sınır olarak tanımlanan bir ağ konumudur. Bir istemci birden fazla geçerli sınır grubuna sahip olabilir.  

- Bir veya daha fazla site sistemi rolü. İstemciler, her zaman geçerli sınır grubuyla ilişkili rolleri kullanabilir. Ek yapılandırmalara bağlı olarak, ek sınır gruplarında rolleri kullanabilirler.  

Oluşturduğunuz her sınır grubu için, başka bir sınır grubuna tek yönlü bir bağlantı yapılandırabilirsiniz. Bağlantıya bir **ilişki**denir. Bağlantı oluşturduğunuz sınır gruplarına **komşu** sınır grupları denir. Sınır grubu, her biri belirli bir komşu sınır grubuyla birden fazla ilişkiye sahip olabilir.

Bir istemci, geçerli sınır grubunda kullanılabilir bir site sistemi bulamazsa, her ilişkinin yapılandırması, bir komşu sınır grubu aramaya ne zaman başlayacağını belirler. Ek grupların bu aramasına **geri dönüş**adı verilir.

Daha fazla bilgi için, aşağıdaki yordamlara bakın:  

- [Sınır grubu oluşturma](boundary-group-procedures.md#bkmk_create)  
- [Sınır grubu yapılandırma](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a>Cihazların sınır gruplarını gösterme

<!--6521835-->

Sürüm 2002 ' den başlayarak, sınır gruplarıyla cihaz davranışlarını daha iyi tanımanıza ve sorunlarını gidermenize yardımcı olması için, belirli cihazların sınır gruplarını görüntüleyebilirsiniz. **Cihazlar** düğümünde veya bir **cihaz koleksiyonunun**üyelerini gösterdiğinizde, yeni **sınır grupları** sütununu liste görünümüne ekleyin.

- Bir cihaz birden fazla sınır grubunda yer alıyorsa, değer sınır grubu adlarının virgülle ayrılmış listesidir.

- İstemci, siteye veya en fazla 24 saatte bir konum isteği yaptığında verileri güncelleştirir.

- Bir istemci dolaşımda ve bir sınır grubunun üyesi değilse, değer boştur.

> [!NOTE]
> Bu bilgiler site verileri ve yalnızca birincil sitelerde kullanılabilir. Configuration Manager bir merkezi yönetim sitesine bağladığınızda bu sütun için bir değer görmezsiniz.

## <a name="fallback"></a>Geri dönüş

İstemcileri geçerli sınır gruplarında kullanılabilir bir site sistemi bulamadığında sorunları engellemek için, geri dönüş davranışı için sınır grupları arasındaki ilişkiyi tanımlayın. Geri dönüş, bir istemcinin kullanılabilir bir site sistemini bulmak için aramasını ek sınır gruplarına genişletmesine olanak sağlar.

İlişkiler bir sınır grubu özellikleri **ilişkiler** sekmesinde yapılandırılır. Bir ilişki yapılandırdığınızda, bir komşu sınır grubuna bir bağlantı tanımlarsınız. Desteklenen her site sistemi rolü türü için, komşu sınır grubuna geri dönüş için bağımsız ayarları yapılandırın. Daha fazla bilgi için bkz. [geri dönüş davranışını yapılandırma](boundary-group-procedures.md#bkmk_bg-fallback).

Örneğin, belirli bir sınır grubuyla bir ilişki yapılandırdığınızda, dağıtım noktalarının geri dönüşünü 20 dakika sonra gerçekleşecek şekilde ayarlayın. Daha kapsamlı bir örnek Için varsayılan değer 120 dakikadır, bkz. [sınır gruplarını kullanma örneği](#example-of-using-boundary-groups).

İstemci geçerli sınır grubunda kullanılabilir bir site sistemi rolü bulamazsa, istemci geri dönüş süresini dakika cinsinden kullanır. Bu geri dönüş süresi, istemcinin komşu sınır grubuyla ilişkili kullanılabilir bir site sistemini aramaya ne zaman başlayacağını belirler.  

İstemci kullanılabilir bir site sistemi bulamadığında, komşu sınır gruplarından konumları aramaya başlar. Bu davranış, kullanılabilir site sistemleri havuzunu arttırır. Sınır gruplarının ve ilişkilerinin yapılandırması, istemcinin bu kullanılabilir site sistemleri havuzunun kullanımını tanımlar.

- Sınır grubu birden fazla ilişkiye sahip olabilir. Bu yapılandırmayla, her site sistemi türü için geri dönüşü farklı bir süre sonra gerçekleşecek farklı komşulara yapılandırabilirsiniz.  

- İstemciler yalnızca geçerli sınır grubunun doğrudan komşusu olan bir sınır grubuna geri döner.  

- Bir istemci birden fazla sınır grubunun üyesi olduğunda, geçerli sınır grubunu tüm sınır gruplarının birleşimi olarak tanımlar. İstemci, bu orijinal sınır gruplarının herhangi birinin komşuları 'na geri döner.  

> [!NOTE]
> Durum geçiş noktası rolü geri dönüş ilişkileri kullanmaz. Hem durum geçiş noktası hem de dağıtım noktası rollerini aynı site sistemi sunucusuna eklerseniz, onun sınır grubuna geri dönüşü yapılandırmayın. Dağıtım noktası için sınır grubu geri dönüşü kullanmanız gerekiyorsa, farklı bir site sistemi sunucusuna durum geçiş noktası rolünü ekleyin.<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>Varsayılan site sınır grubu

Kendi sınır gruplarınızı oluşturabilirsiniz ve her sitenin Configuration Manager oluşturduğu varsayılan bir site sınır grubu vardır. Bu grup **varsayılan-site-sınır-grup&lt;sitekodu>** olarak adlandırılmıştır. Örneğin, ABC sitesi grubu **varsayılan-site-sınır-&lt;grubu ABC>** olarak adlandırılır.

Oluşturduğunuz her sınır grubu için, Configuration Manager hiyerarşideki her bir varsayılan site sınırı grubuna otomatik olarak örtülü bir bağlantı oluşturur.  

- Kapsanan bağlantı, geçerli bir sınır grubundan sitenin varsayılan sınır grubuna varsayılan bir geri dönüş seçeneğidir. Varsayılan geri dönüş süresi 120 dakikadır.  

- Herhangi bir sınır grubuyla ilişkili bir sınır olmayan istemciler için: geçerli site sistem rollerini belirlemek için, varsayılan site sınır grubunu atanan sitesinden kullanın.  

Varsayılan site sınır grubuna geri dönüşü yönetmek için:  

- Site varsayılan sınır grubunun özelliklerini açın ve **varsayılan davranış** sekmesindeki değerleri değiştirin. burada yaptığınız değişiklikler, bu sınır grubuna yönelik *Tüm* kapsanan bağlantılar için geçerlidir. Bu varsayılan site sınır grubuna başka bir sınır grubundan açık bir bağlantı yapılandırdığınızda, bu varsayılan ayarları geçersiz kılarsınız.  

- Özel bir sınır grubunun özelliklerini açın. Açık bağlantının değerlerini varsayılan bir site sınır grubuyla değiştirin. Geri dönüş veya blok geri dönüşü için dakikalar içinde yeni bir süre ayarladığınızda, bu değişiklik yalnızca yapılandırdığınız bağlantıyı etkiler. Açık bağlantının yapılandırması, varsayılan bir site sınır grubunun **varsayılan davranış** sekmesindeki ayarları geçersiz kılar.  

## <a name="site-assignment"></a>Site ataması  

Her sınır grubunu istemciler için atanan bir site ile yapılandırabilirsiniz.  

- Otomatik site ataması kullanan yeni yüklenmiş bir istemci, istemcinin geçerli ağ konumunu içeren bir sınır grubunun atanan sitesine katılır.  

- Bir siteye atandıktan sonra istemci, ağ konumunu değiştirdiğinde site atamasını değiştirmez. Örneğin, bir istemci yeni bir ağ konumuna gezini. Bu konum, farklı bir site atamasına sahip bir sınır grubundaki bir sınırdır. İstemcinin atanan sitesi değişmez.  

- Active Directory sistem bulma yeni bir kaynağı tespit ettiğinizde, site, kaynak için ağ bilgilerini sınır gruplarındaki sınırlara göre değerlendirir. Bu işlem yeni kaynağı, client push yükleme yöntemi tarafından kullanılmak üzere atanmış bir siteyle ilişkilendirir.  

- Sınır, farklı atanmış sitelere sahip birden fazla sınır grubunun üyesi olduğunda, istemciler sitelerden birini rastgele seçer.  

- Sınır gruplarına atanan bir sitede yapılan değişiklikler yalnızca yeni site atama eylemlerine uygulanır. Daha önce bir siteye atanan istemciler, bir sınır grubunun yapılandırmasındaki değişikliklere (veya kendi ağ konumlarına) göre site atamasını yeniden değerlendirmemelidir.  

İstemci site ataması hakkında daha fazla bilgi için bkz. [bilgisayarlar için otomatik site atamasını kullanma](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment).  

Site atamasını yapılandırma hakkında daha fazla bilgi için, aşağıdaki yordamlara bakın:

- [Site atamasını yapılandırma ve site sistemi sunucularını seçme](boundary-group-procedures.md#bkmk_references)
- [Otomatik site ataması için bir geri dönüş sitesi yapılandırma](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>Dağıtım noktaları

Bir istemci bir dağıtım noktasının konumunu istediğinde, Configuration Manager istemciye site sistemlerinin bir listesini gönderir. Bu site sistemleri, istemcinin geçerli ağ konumunu içeren her bir sınır grubuyla ilişkili uygun türdür:

- **Yazılım dağıtımı sırasında**istemciler, geçerli bir içerik kaynağındaki dağıtım içeriği için bir konum ister. Bu konum bir dağıtım noktası veya eş önbellek kaynağı olabilir.  

- **İşletim sistemi dağıtımı sırasında**istemciler, durum geçiş bilgilerini göndermek veya almak için bir konum ister.  

  - İstemciler sınır grubu davranışlarına göre içerik alır. Daha fazla bilgi için bkz. [sınır grupları Için görev sırası desteği](#bkmk_bgr-osd).  

İçerik dağıtımı sırasında, bir istemci, geçerli sınır grubundaki bir kaynaktan kullanılamayan içerikleri isterse, istemci bu içeriği talep etmeye devam eder. İstemci, bir komşu veya varsayılan site sınır grubu için geri dönüş süresine ulaşana kadar, geçerli sınır grubunda farklı içerik kaynakları dener. İstemci hala içerik bulmamışsa, komşu sınır gruplarını eklemek için içerik kaynakları aramasını genişletir.

İçeriği talep üzerine dağıtılacak şekilde yapılandırırsanız ve bir istemci istediğinde bir dağıtım noktasında kullanılabilir değilse, site içeriği bu dağıtım noktasına aktarmaya başlar. İstemci, bir komşu sınır grubu kullanmaya geri dönmeden önce bu sunucuyu içerik kaynağı olarak buluyor olabilir.

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a>İstemci yüklemesi

<!--1358840-->
Configuration Manager istemcisi yüklenirken, CCMSetup işlemi, gerekli içeriğin yerini bulmak için yönetim noktasıyla iletişim kurar. Yönetim noktası, sınır grubu yapılandırmasına bağlı olarak dağıtım noktaları döndürür. Sınır grubunda ilişkiler tanımlarsanız, yönetim noktası dağıtım noktalarını aşağıdaki sırada döndürür:

1. Geçerli sınır grubu  
2. Komşu sınır grupları  
3. Site varsayılan sınır grubu  

> [!Note]  
> İstemci kurulum işlemi geri dönüş süresini kullanmaz. İçeriği mümkün olduğunca hızlı bir şekilde bulmak için hemen sonraki sınır grubuna geri döner.
>
> Önceki Configuration Manager sürümlerinde, bu işlem sırasında yönetim noktası yalnızca istemcinin geçerli sınır grubundaki dağıtım noktalarını döndürür. Kullanılabilir içerik yoksa, kurulum işlemi içeriği yönetim noktasından indirmeye geri döndü. Gerekli içeriğe sahip olabilecek diğer sınır gruplarındaki dağıtım noktalarına geri dönüş seçeneği yoktu.

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a>Sınır grupları için görev dizisi desteği

<!--1359025-->
Bir cihaz bir görev dizisi çalıştırdığında ve içerik almaları gerektiğinde, Configuration Manager istemcisine benzer sınır grubu davranışları kullanır.

Görev sırası dağıtımının **dağıtım noktaları** sayfasında aşağıdaki ayarları kullanarak bu davranışı yapılandırın:

- **Kullanılabilir yerel dağıtım noktası olmadığında, uzak bir dağıtım noktası kullan**: Bu dağıtım için, görev dizisi bir komşu sınır grubundaki dağıtım noktalarına geri dönebilir.  

- **İstemcilerin varsayılan site sınırı grubundan dağıtım noktaları kullanmasına Izin ver**: Bu dağıtım için, görev sırası varsayılan site sınır grubundaki dağıtım noktalarına geri dönebilir.  

Bu yeni davranışı kullanmak için, istemcileri en son sürüme güncelleştirdiğinizden emin olun.

#### <a name="location-priority"></a>Konum önceliği  

Görev dizisi, aşağıdaki sırayla içerik almaya çalışır:  

1. Eş önbellek kaynakları  

2. *Geçerli* sınır grubundaki dağıtım noktaları  

3. Bir *komşu* sınır grubundaki dağıtım noktaları  

    > [!Important]  
    > Görev dizisi işlemenin gerçek zamanlı doğası nedeniyle, bir komşu sınır grubundaki yük devretme süresini beklemez. Komşu sınır gruplarını önceliklendirme için yük devretme sürelerini kullanır. Örneğin, görev dizisi, geçerli sınır grubundaki bir dağıtım noktasından içerik elde kuramazsa, en kısa yük devretme zamanına sahip bir komşu sınır grubundaki bir dağıtım noktasını hemen dener. Bu işlem başarısız olursa, yük devretme süresi daha fazla olan bir komşu sınır grubundaki dağıtım noktasına yük devreder.  

4. *Site varsayılan* sınır grubundaki dağıtım noktaları  

Görev dizisi günlük dosyası **Smsts. log** , dağıtım özelliklerine göre kullandığı konum kaynaklarının önceliğini gösterir.

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Eş indirmeleri için sınır grubu seçenekleri

<!--1356193, 1358749-->
Sınır grupları, ortamınızda içerik dağıtımı üzerinde daha fazla denetim sağlamak için aşağıdaki ek ayarları içerir:  

- [Bu sınır grubunda eş indirmelere izin ver](#bkmk_bgoptions1)  

- [Eş İndirmeleri sırasında yalnızca aynı alt ağda bulunan eşleri kullanın](#bkmk_bgoptions2)  

- [Aynı alt ağa sahip eş üzerinde dağıtım noktalarını tercih et](#bkmk_bgoptions3)  

- [Dağıtım noktaları üzerinden bulut dağıtım noktalarını tercih et](#bkmk_bgoptions4)  

Bu ayarları yapılandırma hakkında daha fazla bilgi için bkz. [sınır grubunu yapılandırma](boundary-group-procedures.md#bkmk_config).

Bir cihaz birden fazla sınır grubındayken, bu ayarlar için aşağıdaki davranışlar geçerlidir:

- **Bu sınır grubunda eş Indirmeye Izin ver**: herhangi bir sınır grubunda devre dışıysa, istemci teslim iyileştirmesini kullanmaz.
- **Eş Indirmeleri sırasında yalnızca aynı alt ağa sahip olan eşleri kullanın**: herhangi bir sınır grubunda etkinleştirilirse, bu ayar geçerli olur.
- **Aynı alt ağ içindeki eşler üzerinde dağıtım noktalarını tercih et**: herhangi bir sınır grubunda etkinse, bu ayar geçerli olur.
- Şirket **içi kaynaklar üzerinde bulut tabanlı kaynakları tercih etme**: herhangi bir sınır grubunda etkinse, bu ayar geçerli olur.

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a>Bu sınır grubunda eş indirmelere izin ver

Bu ayar, varsayılan olarak etkinleştirilmiştir. Yönetim noktası, istemcilere eş kaynakları içeren içerik konumlarının bir listesini sağlar. Bu ayar, [teslim iyileştirmesi](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)Için Grup kimliklerinin uygulanmasını da etkiler.  

Bu seçeneği devre dışı bırakmayı göz önünde bulundurmanız gereken iki yaygın senaryo vardır:  

- VPN gibi coğrafi olarak dağınık konumlardan sınır içeren bir sınır grubunuz varsa. VPN üzerinden bağlı olduklarından iki istemci aynı sınır grubunda olabilir, ancak içeriğin eş paylaşımı için uygun olmayan büyük ölçüde farklı konumlarda olabilir.  

- Site ataması için herhangi bir dağıtım noktasına başvurmayan tek bir büyük sınır grubu kullanıyorsanız.  

> [!IMPORTANT]
> Bir cihaz birden fazla sınır grubındayken, bu ayarı cihaz için tüm sınır gruplarında etkinleştirdiğinizden emin olun. Aksi takdirde istemci teslim iyileştirmesi kullanmaz. Örneğin, Dogroupıd kayıt defteri anahtarını yapmaz.

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a>Eş İndirmeleri sırasında yalnızca aynı alt ağda bulunan eşleri kullanın

Bu ayar, önceki seçeneğe bağımlıdır. Bu seçeneği etkinleştirirseniz, yönetim noktası yalnızca istemciyle aynı alt ağda bulunan içerik konumu listesi eş kaynaklarını içerir.

Bu seçeneği etkinleştirmeye yönelik yaygın senaryolar:

- İçerik dağıtımı için sınır grubu tasarımınız, diğer küçük sınır gruplarıyla örtüşen bir büyük sınır grubu içerir. Bu yeni ayar ile, yönetim noktasının istemcilerine sağladığı içerik kaynakları listesi yalnızca aynı alt ağdaki eş kaynakları içerir.

- Tüm uzak Office konumları için tek bir büyük sınır grubunuz vardır. Bu seçeneği etkinleştirin ve istemciler, konumlar arasında içerik paylaşımı yapmak yerine yalnızca uzak ofis konumundaki alt ağ içindeki içeriği paylaşır.

Sürüm 2002 ' den başlayarak ağınızın yapılandırmasına bağlı olarak, belirli alt ağları eşleştirme için dışlayabilirsiniz. Örneğin, bir sınır eklemek, ancak belirli bir VPN alt ağını dışlamak istiyorsunuz. Varsayılan olarak, Configuration Manager varsayılan Teredo alt ağını (`2001:0000:%`) dışlar.<!--3555777-->

> [!NOTE]
> Sürüm 2002 ' de, [tek başına bir birincil siteyi](../install/prerequisites-for-installing-sites.md#bkmk_expand) bir merkezi yönetim SITESI (CAS) eklemek üzere genişlettiğinizde, alt ağ dışlama listesi varsayılana geri döner. Bu sorunu geçici olarak çözmek için, site genişletmesinden sonra CA 'daki alt ağ dışlama listesini özelleştirmek üzere PowerShell betiğini çalıştırın.<!-- 6309068 -->

Alt ağ dışlama listenizi, virgülle ayrılmış bir alt ağ dizesi olarak içeri aktarın. Yüzde işaretini (`%`) joker karakter olarak kullanın. Üst düzey site sunucusunda, **SMS_SCI_Component** sınıfındaki **SMS_HIERARCHY_MANAGER** bileşeni Için **Subnetexclusıonlist** Embedded özelliğini ayarlayın veya okuyun. Daha fazla bilgi için bkz. [SMS_SCI_Component sunucusu WMI sınıfı](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md).

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>Alt ağ dışlama listesini güncelleştirmek için örnek PowerShell betiği

Aşağıdaki betik, bu değeri değiştirmenin örnek bir yoludur. Sonrasında `2001:0000:%,172.16.16.0`alt ağlarınızı **PropertyValue** değişkenine ekleyin. Bu, virgülle ayrılmış bir dizedir. Bu betiği hiyerarşinizdeki üst düzey site sunucusunda çalıştırın.

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> Varsayılan olarak, Configuration Manager Bu listedeki Teredo alt ağını içerir. Listeyi değiştirdiğinizde, her zaman ilk olarak mevcut değeri okuyun. Listeye ek alt ağlar ekleyin ve ardından yeni değeri ayarlayın.

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a>Aynı alt ağa sahip eş üzerinde dağıtım noktalarını tercih et

Varsayılan olarak, yönetim noktası, içerik konumları listesinin en üstünde eş önbellek kaynaklarını önceliklendirir. Bu ayar eş önbellek kaynağıyla aynı alt ağda olan istemciler için bu önceliği tersine çevirir.

> [!TIP]
> Bu davranış Configuration Manager istemcisi için geçerlidir. Görev sırası içeriği indirdiğinde uygulanmaz. Görev sırası çalıştırıldığında, dağıtım noktaları üzerinden eş önbellek kaynaklarını tercih eder.<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a>Dağıtım noktaları üzerinden bulut dağıtım noktalarını tercih et

Daha hızlı bir internet bağlantısı olan bir şube ofisiniz varsa, artık bulut içeriğinin önceliklerini belirleyebilirsiniz.  

Sürüm 1902 ' de, bu ayar artık şirket **içi kaynaklar üzerinde bulut tabanlı kaynakları tercih**ediyor. Bulut tabanlı kaynaklar şunları içerir:<!-- SCCMDocs#1529 -->

- Bulut dağıtım noktaları
- Microsoft Update (sürüm 1902 ' de eklendi)

## <a name="software-update-points"></a>Yazılım güncelleştirme noktaları

İstemciler yeni bir yazılım güncelleştirme noktası bulmak için sınır grupları kullanır. Bir istemcinin bulabileceği sunucuları denetlemek için, farklı sınır gruplarına bireysel yazılım güncelleştirme noktaları ekleyin.

Var olan tüm yazılım güncelleştirme noktalarını varsayılan site sınır grubuna eklerseniz, istemci kullanılabilir sunucular havuzundan bir yazılım güncelleştirme noktası seçer. Bu davranış, Configuration Manager geçerli dalın önceki sürümlerine benzerdir. Denetimli seçim ve geri dönüş davranışı için, farklı sınır gruplarına ayrı yazılım güncelleştirme noktaları ekleyin.

Yeni bir site yüklerseniz, yazılım güncelleştirme noktaları varsayılan site sınır grubuna eklenmez. İstemcilerin bunları bulabilmesi ve kullanabilmesi için, bir sınır grubuna yazılım güncelleştirme noktaları atayın.

### <a name="fallback-for-software-update-points"></a>Yazılım güncelleştirme noktaları için geri dönüş

Yazılım güncelleştirme noktaları için geri dönüş, diğer site sistem rolleri gibi yapılandırılır, ancak aşağıdaki uyarılar vardır:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Yeni istemciler, yazılım güncelleştirme noktalarını seçmek için sınır grupları kullanır

Yeni istemcileri yüklediğinizde, yapılandırdığınız sınır gruplarıyla ilişkili sunuculardan bir yazılım güncelleştirme noktası seçer. Bu davranış, istemcilerin bir yazılım güncelleştirme noktasını istemcinin ormanını paylaşan sunucular listesinden rastgele olarak seçleyeceği önceki davranışın yerini alır.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>İstemciler yeni bir yazılım güncelleştirme noktası bulmaya devam edene kadar yeni bir en iyi

Zaten bir yazılım güncelleştirme noktası olan istemciler, ulaşılana kadar bu uygulamayı kullanmaya devam eder. Bu davranış, istemcinin geçerli sınır grubuyla ilişkili olmayan bir yazılım güncelleştirme noktasının devam eden kullanımını içerir.

Bu davranış bilerek yapılır. İstemci, istemcinin geçerli sınır grubunda olmasa bile mevcut bir yazılım güncelleştirme noktasını kullanmaya devam eder. Yazılım güncelleştirme noktası değiştiğinde, istemci verileri yeni sunucu ile eşitler ve bu da önemli ölçüde ağ kullanımına neden olur. Tüm istemciler aynı anda yeni bir sunucuya geçiş yapışında, geçişte gecikme, ağınızı doygunluğu önlemeye yardımcı olur.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>İstemci her zaman, geri dönüşü başlatmadan önce 120 dakika boyunca bilinen son iyi yazılım güncelleştirme noktasına ulaşmaya çalışır

120 dakika sonra istemci iletişim kurmadıysa, geri dönüş başlar. Geri dönüş başladığında istemci, geçerli sınır grubundaki tüm yazılım güncelleştirme noktalarının listesini alır. Komşu ve site varsayılan sınır gruplarındaki ek yazılım güncelleştirme noktaları, geri dönüş yapılandırmalarına bağlı olarak kullanılabilir.

### <a name="fallback-configurations-for-software-update-points"></a>Yazılım güncelleştirme noktaları için geri dönüş yapılandırması

Yazılım güncelleştirme noktalarının 120 dakikadan kısa olması için **geri dönüş sürelerini (dakika cinsinden)** yapılandırabilirsiniz. Ancak, istemci hala 120 dakika boyunca özgün yazılım güncelleştirme noktasına ulaşmaya çalışır. Daha sonra aramasını ek sunuculara genişletir. Sınır grubu geri dönüş süreleri, istemci ilk olarak orijinal sunucusuna ulaşamazsa başlar. İstemci aramasını genişlediğinde, site 120 dakikadan kısa bir süre için yapılandırılmış herhangi bir sınır grubu sağlar.

Bir yazılım güncelleştirme noktasının bir komşu sınır grubuna geri dönüşü engellemek için, ayarı **hiçbir şekilde geri dönüş**olarak yapılandırın.

İkinci saat boyunca özgün sunucusuna ulaşamadıktan sonra istemci, yeni bir yazılım güncelleştirme noktasıyla bağlantı kurmak için daha kısa bir döngüye kullanır. Bu davranış, istemcinin olası yazılım güncelleştirme noktalarının genişleyen listesini hızla aramasını sağlar.

#### <a name="example"></a>Örnek

Sınır grubu *A* 'daki yazılım güncelleştirme noktalarını **10** dakika sonra geri dönüş için yapılandırırsınız. *B* sınır grubu için aynı ayarı **130** dakika olarak yapılandırırsınız. *Z* sınır grubundaki bir istemci, bilinen son iyi yazılım güncelleştirme noktasına ulaşamazsa.

- Sonraki 120 dakika boyunca istemci, Z sınır grubundaki yalnızca özgün sunucusuna ulaşmaya çalışır. 10 dakika sonra Configuration Manager, A sınır grubundan yazılım güncelleştirme noktalarını kullanılabilir sunucular havuzuna ekler. Ancak, ilk 120 dakikalık süre sona erdiğinde, istemci bunlarla veya diğer bir sunucuyla iletişim kurmaya çalışır.  

- 120 dakika boyunca özgün yazılım güncelleştirme noktası ile iletişim kurmaya çalıştıktan sonra istemci, aramasını genişletir. Sunucuları, mevcut olan yazılım güncelleştirme noktalarının mevcut havuzuna ve 120 dakika veya daha kısa bir süre için yapılandırılmış komşu sınır gruplarına ekler. Bu havuz, daha önce kullanılabilir sunucular havuzuna eklenmiş olan A sınır grubu sunucularını içerir.  

- 10 dakika sonra istemci, arama 'yı B sınır grubundan yazılım güncelleştirme noktaları içerecek şekilde genişletir. Bu süre, istemci ilk bilinen son iyi yazılım güncelleştirme noktasına ulaşamadıktan sonra geçen toplam süre olan 130 dakikadır.  

### <a name="manually-switch-to-a-new-software-update-point"></a>El ile yeni bir yazılım güncelleştirme noktasına geçme

Geri dönüş ile birlikte, bir cihazı yeni bir yazılım güncelleştirme noktasına geçiş için el ile zorlamak üzere istemci bildirimini kullanın.

Yeni bir sunucuya geçtiğinizde, cihazlar bu yeni sunucuyu bulmak için geri dönüş kullanır. İstemciler, bir sonraki yazılım güncelleştirmeleri tarama döngülerinde yeni yazılım güncelleştirme noktasına geçer.<!-- SCCMDocs#1537 -->

Sınır grubu yapılandırmalarınızı gözden geçirin. Bu değişikliği başlatmaya başlamadan önce, yazılım güncelleştirme noktalarınızın doğru sınır gruplarında olduğundan emin olun.

Daha fazla bilgi için bkz. [Istemcileri el ile yeni bir yazılım güncelleştirme noktasına değiştirme](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

## <a name="management-points"></a>Yönetim noktaları

<!-- 1324594 -->
Sınır grupları arasındaki yönetim noktaları için geri dönüş ilişkilerini yapılandırın. Bu davranış, istemcilerin kullandığı yönetim noktaları için daha fazla denetim sağlar. Sınır grubu özelliklerinin **ilişkiler** sekmesinde, yönetim noktası için bir sütun vardır. Yeni bir geri dönüş sınır grubu eklediğinizde, yönetim noktası için geri dönüş süresi şu anda her zaman sıfırdır (0). Bu davranış, sitenin varsayılan sınır grubundaki **varsayılan davranış** için aynıdır.

Daha önce, güvenli bir ağda korumalı bir yönetim noktanız olduğunda yaygın bir sorun oluştu. Ana ağdaki istemciler, bir güvenlik duvarı genelinde iletişim kuramasa bile, bu korumalı yönetim noktasını içeren ilke aldı. Bu sorunu şimdi ele almak için, istemcilerin iletişim kurabileceği yönetim noktalarına geri dönebilmeleri için **hiçbir durumda geri dönüş** seçeneğini kullanın.

> [!Note]  
> Site varsayılan sınır grubundaki dağıtım noktalarını geri dönüş için etkinleştirirseniz ve bir yönetim noktası bir dağıtım noktasında birlikte bulunuyorsa, site aynı zamanda o yönetim noktasını site varsayılan sınır grubuna ekler.<!--VSO 2841292-->  

Bir istemci, atanmış yönetim noktası olmayan bir sınır grubuysa, site istemciye tüm yönetim noktaları listesini verir. Bu davranış, bir istemcinin her zaman bir yönetim noktaları listesi aldığından emin olur.

Yönetim noktası sınır grubu geri dönüş, istemci yüklemesi sırasında davranışı değiştirmez (CCMSetup. exe). Komut satırı/MP parametresini kullanarak ilk yönetim noktasını belirtmezse, yeni istemci kullanılabilir yönetim noktalarının tam listesini alır. İlk önyükleme işlemi için istemci, erişebileceği ilk yönetim noktasını kullanır. İstemci sitesiyle kaydolduğunda, bu yeni davranışla birlikte yönetim noktası listesini doğru şekilde sıralanmış olarak alır.

Yükleme sırasında istemci içeriği alma davranışı hakkında daha fazla bilgi için bkz. [istemci yüklemesi](#bkmk_ccmsetup).

İstemci yükseltmesi sırasında,/MP komut satırı parametresini belirtmezseniz, istemci, kullanılabilir herhangi bir yönetim noktası için Active Directory ve WMI gibi kaynakları sorgular. İstemci yükseltmesi sınır grubu yapılandırmasını dikkate almaz. <!--VSO 2841292-->  

İstemcilerin bu özelliği kullanabilmesi için aşağıdaki ayarı etkinleştirin: Istemciler, **hiyerarşi ayarlarında** **sınır gruplarında belirtilen yönetim noktalarını kullanmayı tercih eder** .

> [!Note]  
> İşletim sistemi dağıtım işlemlerinde yönetim noktaları için sınır grupları farkında değildir.  

### <a name="troubleshooting"></a>Sorun giderme

Yeni girişler **LocationServices. log**dosyasında görünür. **Yerleşim** özniteliği aşağıdaki durumlardan birini tanımlar:

- **0**: bilinmiyor  

- **1**: belirtilen yönetim noktası, geri dönüş için yalnızca site varsayılan sınır grubunda bulunur  

- **2**: belirtilen yönetim noktası uzak veya komşu sınır grubunda. Yönetim noktası hem komşu hem de site varsayılan sınır gruplarında olduğunda, konum 2 ' dir.  

- **3**: belirtilen yönetim noktası yerel veya geçerli sınır grubunda. Yönetim noktası geçerli sınır grubunda ve bir komşu ya da site varsayılan sınır grubındayken, konum 3 ' dir. Hiyerarşi Ayarları ' nda tercih edilen yönetim noktaları ayarını etkinleştirmezseniz, yönetim noktasının hangi sınır grubuna bakılmaksızın konum her zaman 3 olur.  

İstemciler önce yerel yönetim noktalarını (konum 3), uzak ikinci (konum 2), ardından geri dönüş (konum 1) kullanır.

İstemci 10 dakika içinde beş hata aldığında ve geçerli sınır grubundaki bir yönetim noktasıyla iletişim kuramazsa, bir komşu veya site varsayılan sınır grubundaki bir yönetim noktasıyla iletişim kurmayı dener. Geçerli sınır grubundaki yönetim noktası daha sonra yeniden çevrimiçi duruma gelirse, istemci sonraki yenileme döngüsündeki yerel yönetim noktasına geri döner. Yenileme çevrimi 24 saattir veya Configuration Manager Aracı hizmeti yeniden başlatılır.

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a>Tercih edilen yönetim noktaları

> [!Note]
> Bu hiyerarşi ayarının davranışı, **istemciler sınır gruplarında belirtilen yönetim noktalarını kullanmayı tercih eder**, sürüm 1802 ' de değişmiştir. Bu ayarı etkinleştirdiğinizde, Configuration Manager atanan yönetim noktası için sınır grubu işlevini kullanır. Daha fazla bilgi için bkz. [Yönetim noktaları](#management-points).

Tercih edilen yönetim noktaları, bir istemcinin geçerli ağ konumuyla (sınır) ilişkili bir yönetim noktasını belirlemesini sağlar.  

- İstemci, atanan sitesinden tercih edilen olarak yapılandırılmamış bir yapılandırma kullanmadan önce, atanmış sitesinden tercih edilen bir yönetim noktası kullanmayı dener.  

- Bu seçeneği kullanmak için, Istemcileri **hiyerarşi ayarlarındaki** **sınır gruplarında belirtilen yönetim noktalarını kullanmayı tercih eder** . Ardından, tek tek birincil sitelerde sınır grupları yapılandırın. Bu sınır grubunun ilişkili sınırlarıyla ilişkilendirilmesi gereken yönetim noktalarını ekleyin. Daha fazla bilgi için bkz. [tercih edilen yönetim noktalarının kullanımını etkinleştirme](boundary-group-procedures.md#bkmk_proc-prefer).  

- Tercih edilen yönetim noktalarını yapılandırdığınızda ve bir istemci, yönetim noktaları listesini düzenlediğinde istemci, tercih edilen yönetim noktalarını listenin en üstüne koyar. Bu liste, istemcinin atanmış sitesinin tüm yönetim noktalarını içerir.  

> [!NOTE]  
> İstemci dolaşımı, ağ konumlarını değiştirdiği anlamına gelir. Örneğin, bir dizüstü bilgisayar uzak bir ofis konumuna seyahat edildiğinde. Bir istemci dolaşımda, atanan sitesinden bir sunucuyu kullanmayı denemeden önce yerel siteden bir yönetim noktası kullanabilir. Atanmış sitesinin bu sunucu listesi, tercih edilen yönetim noktalarını içerir. Daha fazla bilgi için bkz. [İstemcilerin site kaynaklarını ve hizmetleri nasıl bulduklarını anlama](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Çakışan sınırlar  

Configuration Manager, içerik konumu için çakışan sınır yapılandırmalarının kullanılmasını destekler. İstemcinin ağ konumu birden fazla sınır grubuna ait olduğunda:

- İstemci içerik istediğinde, Configuration Manager istemciye, içeriğe sahip olan tüm dağıtım noktalarının bir listesini gönderir.  

- İstemci, durum geçiş bilgilerini göndermek veya almak için bir sunucu istediğinde, Configuration Manager istemciye, istemcinin geçerli ağ konumunu içeren bir sınır grubuyla ilişkilendirilmiş tüm durum geçiş noktalarının listesini gönderir.  

Bu davranış istemcinin içeriği veya durum geçiş bilgilerini aktarmada kullanılacak en yakın sunucuyu seçmesine olanak sağlar.  

## <a name="example-of-using-boundary-groups"></a>Sınır gruplarını kullanma örneği

Aşağıdaki örnek, bir dağıtım noktasından içerik arayan bir istemci kullanır. Bu örnek, sınır grupları kullanan diğer site sistem rollerine uygulanabilir.

Sınırları veya site sistemi sunucularını paylaşmaz üç sınır grubu oluşturun:  

- Dağıtım noktaları DP_A1 ve DP_A2 BG_A gruplandırın  

- Dağıtım noktaları DP_B1 ve DP_B2 BG_B gruplandırın  

- Dağıtım noktaları DP_C1 ve DP_C2 BG_C gruplandırın  

İstemcilerinizin ağ konumlarını sınır olarak yalnızca BG_A sınır grubuna ekleyin. Ardından, bu sınır grubundan diğer iki sınır grubuyla ilişkileri yapılandırın:  

- 10 dakika sonra kullanılacak ilk *komşu* grubu (BG_B) için dağıtım noktalarını yapılandırın. Bu grup DP_B1 ve DP_B2 dağıtım noktalarını içerir. Her ikisi de ilk grubun sınır konumlarına bağlıdır.  

- 20 dakika sonra kullanılacak ikinci *komşu* grubunu (BG_C) yapılandırın. Bu grup DP_C1 ve DP_C2 dağıtım noktalarını içerir. Her ikisi de diğer iki sınır grubundan bir WAN üzerinden yapılır.  

- Ayrıca, site sunucusundaki diğer bir dağıtım noktasını varsayılan site sınır grubuna ekleyin. Bu sunucu, tercih ettiğiniz en az içerik kaynağı konumudur, ancak tüm sınır gruplarınız üzerinde merkezi olarak bulunur.

    Sınır grupları ve geri dönüş süreleri örneği:

    ![Sınır grupları ve geri dönüş süreleri örneği](media/BG_Fallback.png)  

Bu yapılandırmayla:  

- İstemci, *geçerli* sınır grubundaki (BG_A) dağıtım noktalarından içerik aramaya başlar. Her dağıtım noktasını iki dakika boyunca arar ve sonra sınır grubundaki bir sonraki dağıtım noktasına geçer. İstemcinin geçerli içerik kaynak konumları havuzu DP_A1 ve DP_A2 içerir.  

- İstemci, 10 dakika aramadan sonra *geçerli* sınır grubundan içerik bulamazsa, dağıtım noktalarını BG_B sınır grubundan aramaya ekler. Daha sonra Birleşik Sunucu havuzundaki bir dağıtım noktasından içerik aramaya devam eder. Bu havuz artık hem BG_A hem de BG_B sınır gruplarının sunucularını içerir. İstemci her bir dağıtım noktasıyla iki dakika boyunca iletişim kurmaya devam eder ve ardından havuzundaki sonraki sunucuya geçiş yapar. İstemcinin geçerli içerik kaynak konumları havuzu DP_A1, DP_A2, DP_B1 ve DP_B2 içerir.  

- 10 dakikadan (Toplam 20 dakika) sonra, istemci hala içeriğe sahip bir dağıtım noktası bulmamışsa, havuzunu ikinci *komşu* grubundan, sınır grubu BG_C bulunan sunucuları içerecek şekilde genişletir. İstemci artık arama yapmak için altı dağıtım noktasına sahiptir: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 ve DP_C2. İçerik bulana kadar her iki dakikada bir yeni bir dağıtım noktasına değiştirmeye devam eder.  

- İstemci toplam 120 dakikadan sonra içerik bulmamışsa, devam eden aramasının bir parçası olarak *varsayılan site sınır grubunu* dahil etmek için geri döner. Artık havuz, üç yapılandırılmış sınır grubundan tüm dağıtım noktalarını ve site sunucusunda bulunan son dağıtım noktasını içerir. İstemci daha sonra içerik aramaya devam eder ve içerik bulunana kadar her iki dakikada bir dağıtım noktasını değiştirir.  

Farklı komşu grupları farklı zamanlarda kullanılabilir olacak şekilde yapılandırarak, belirli dağıtım noktalarının içerik kaynağı konumu olarak ne zaman ekleneceğini kontrol edersiniz. İstemci, diğer herhangi bir konumdan kullanılamayan içerik için bir güvenlik ağı olarak varsayılan site sınır grubuna geri dönüş kullanır.

## <a name="changes-from-prior-versions"></a>Önceki sürümlerden yapılan değişiklikler

Sınır gruplarında önemli değişiklikler ve istemcilerin Configuration Manager geçerli dalda içerik bulma yöntemleri aşağıda verilmiştir. Bu değişikliklerin ve kavramların birçoğu birlikte çalışır.

### <a name="configurations-for-fast-or-slow-are-removed"></a>Hızlı veya yavaş yapılandırma kaldırılır

Artık tek tek dağıtım noktalarını hızlı veya yavaş olacak şekilde yapılandıramazsınız. Bunun yerine, bir sınır grubuyla ilişkilendirilmiş her site sistemi aynı şekilde değerlendirilir. Bu değişiklik nedeniyle, sınır grubu özelliklerinin **Başvurular** sekmesi artık hızlı veya yavaş yapılandırmayı desteklememektedir.  

### <a name="new-default-boundary-group-at-each-site"></a>Her sitede yeni varsayılan sınır grubu

Her birincil sitenin **Default-site-sınır-Group&lt;sitekodu>** adlı yeni bir varsayılan sınır grubu vardır. Bir istemci, bir sınır grubuna atanan bir ağ konumunda olmadığında, atanmış sitesinden varsayılan grupla ilişkili site sistemlerini kullanır. Bu sınır grubunu, geri dönüş içerik konumu kavramının yerini alarak kullanmayı planlayın.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>**İçerik için geri dönüş kaynak konumlarına Izin ver** kaldırıldı

Artık geri dönüş için kullanılacak bir dağıtım noktasını açıkça yapılandıramazsınız. Bu ayarı yapılandırma seçenekleri konsolundan kaldırılır.

Ayrıca, istemcilerin uygulama için dağıtım türündeki **içerik için bir geri dönüş kaynak konumu kullanmasına Izin ver** ayarının sonucu değişmiştir. Dağıtım türündeki bu ayar artık istemcinin varsayılan site sınır grubunu içerik kaynağı konumu olarak kullanmasına olanak sağlar.

#### <a name="boundary-groups-relationships"></a>Sınır grupları ilişkileri

Her sınır grubunu bir veya daha fazla ek sınır grubuna bağlayabilirsiniz. Bu bağlantılar, yeni sınır grubu özellikleri sekmesinde yapılandırdığınız **ilişkiler adlı ilişkileri**oluşturur:  

- Bir istemcinin doğrudan ilişkilendirildiği her sınır grubuna **geçerli** bir sınır grubu denir.  

- İstemcinin *geçerli* sınır grubu ile başka bir gruba bir **komşu** sınır grubu olarak adlandırılan bir ilişki nedeniyle istemci tarafından kullanılabilecek tüm sınır grupları.  

- **İlişkiler** sekmesinde, *komşu* sınır grubu olarak kullanılacak sınır gruplarını ekleyin. Ayrıca, geri dönüş için dakika cinsinden bir süre yapılandırın. Bir istemci, *geçerli* gruptaki bir dağıtım noktasından içerik bulamazsa, bu kez istemci, *komşu* sınır gruplarından içerik konumlarını aramaya başladığında olur.  

    Bir sınır grubu yapılandırması eklediğinizde veya değiştirirken, bu belirli sınır grubuna, yapılandırmakta olduğunuz geçerli gruptan geri dönüşü engelleyebilirsiniz.  

Yeni yapılandırmayı kullanmak için, bir sınır grubundan diğerine açık ilişkiler (bağlantılar) tanımlayın. Bu ilişkili gruptaki tüm dağıtım noktalarını dakikalar içinde aynı sürede yapılandırın. Bir istemci, *geçerli* sınır grubundan bir içerik kaynağı bulamazsa, yapılandırdığınız zaman, komşu sınır grubundan içerik kaynaklarını aramaya ne zaman başlayacağını belirler.

Açıkça yapılandırdığınız sınır gruplarının yanı sıra, her sınır grubu, varsayılan site sınır grubuna yönelik örtülü bir bağlantıya sahiptir. Bu bağlantı 120 dakika sonra etkin hale gelir. Ardından, varsayılan site sınır grubu bir komşu sınır grubu olur. Bu davranış, istemcilerin, bu sınır grubuyla ilişkili dağıtım noktalarını içerik kaynak konumları olarak kullanmasına izin verir.

Bu davranış, daha önce içeriğe geri dönüş olarak adlandırılan nelerin yerini alır. Varsayılan site sınır grubunu *geçerli* bir grupla doğrudan ilişkilendirerek, 120 dakikalık varsayılan davranışını geçersiz kılın. Belirli bir zamanı dakikalar içinde ayarlayın veya kullanımını engellemek için tamamen geri dönüşü engelleyin.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>İstemciler her dağıtım noktasından en fazla iki dakika boyunca içerik almaya çalışır

İstemci bir içerik kaynak konumunu aradığında, daha sonra başka bir dağıtım noktası denemeden önce her bir dağıtım noktasına iki dakika boyunca erişmeyi dener. Bu davranış, istemcilerin bir dağıtım noktasına en fazla iki saate bağlanmayı denediği önceki sürümlerden yapılan bir değişikdir.

- İstemciler, istemcinin *geçerli* sınır grubundaki (veya gruplarındaki) kullanılabilir sunucular havuzundan ilk dağıtım noktasını rastgele seçer.  

- İki dakika sonra istemci içerik bulmadıysa, yeni bir dağıtım noktasına geçer ve bu sunucudan içerik almaya çalışır. Bu işlem, istemci içeriği bulana veya havuzundaki son sunucuya ulaşana kadar her iki dakikada bir yinelenir.  

- Bir *istemci, bir* *komşu* sınır grubuna geri dönüş için döneme ulaşmadan önce geçerli havuzundan geçerli bir içerik kaynağı konumu bulamazsa, istemci o *komşu* grubundan dağıtım noktalarını geçerli listesinin sonuna ekler. Daha sonra, her iki sınır grubundan dağıtım noktalarını içeren genişletilmiş kaynak konumları grubunu arar.  

    > [!TIP]  
    > Geçerli sınır grubundan varsayılan site sınır grubuna açık bir bağlantı oluşturduğunuzda ve bir komşu sınır grubuna bağlantının geri dönüş zamanından daha az bir geri dönüş süresi tanımladığınızda, istemciler, komşu grubunu eklemeden önce varsayılan site sınırı grubundan kaynak konumları aramaya başlar.  

- İstemci, havuzdaki son sunucudan içerik alabilmek için işlemi yeniden başlatır.  

## <a name="see-also"></a>Ayrıca bkz.

- [Sınır gruplarına yönelik yordamlar](boundary-group-procedures.md)  

- [Sınırlar hakkında](boundaries.md)  

- [İçerik yönetimi için temel kavramlar](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  
