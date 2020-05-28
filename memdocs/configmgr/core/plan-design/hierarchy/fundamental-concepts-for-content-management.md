---
title: İçerik yönetiminin temelleri
titleSuffix: Configuration Manager
description: Dağıttığınız içeriği yönetmek için Configuration Manager araç ve seçenekleri kullanın.
ms.date: 12/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cb91e62c4ffce37068b2de5e125865e28ff8c53b
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878948"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Configuration Manager 'de içerik yönetimi için temel kavramlar

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager, yazılım içeriğini yönetmek için güçlü bir araç ve seçenek sistemini destekler. Uygulamalar, paketler, yazılım güncelleştirmeleri ve işletim sistemi dağıtımları gibi yazılım dağıtımlarının hepsi içeriğe ihtiyacı vardır. Configuration Manager, içeriği hem site sunucularında hem de dağıtım noktalarında depolar. Bu içerik, konumlar arasında aktarıldığında büyük miktarda ağ bant genişliği gerektirir. İçerik yönetimi altyapısını etkin bir şekilde planlamak ve kullanmak için önce kullanılabilir seçenekleri ve konfigürasyonları anlayın. Daha sonra bunları ağ ortamınıza ve içerik dağıtımı ihtiyaçlarınıza en iyi şekilde uydurmak için nasıl kullanacağınızı göz önünde bulundurun.  

> [!TIP]  
> İçerik dağıtım işlemi hakkında daha fazla bilgi edinmek ve genel içerik dağıtım sorunlarını tanılamada ve çözmede yardım bulmak için bkz. [Microsoft Configuration Manager 'de Içerik dağıtımını anlama ve sorun giderme](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Aşağıdaki bölümler, içerik yönetimi için temel kavramlardır. Bir kavram, ek veya karmaşık bilgiler gerektirdiğinde bu ayrıntılar için size bağlantılar sağlanmaktadır.


## <a name="accounts-used-for-content-management"></a>İçerik yönetimi için kullanılan hesaplar

İçerik yönetimi ile aşağıdaki hesaplar kullanılabilir:  

### <a name="network-access-account"></a>Ağ erişim hesabı

İstemciler tarafından bir dağıtım noktasına bağlanmak ve içeriğe erişmek için kullanılır. Varsayılan olarak, önce bilgisayar hesabı denenir.  

Bu hesap, uzak bir ormandaki kaynak dağıtım noktasından içerik indirmek için çekme dağıtım noktaları tarafından da kullanılır.  

Sürüm 1806 ' den başlayarak, bazı senaryolar artık bir ağ erişim hesabı gerektirmez. Sitenin Azure Active Directory kimlik doğrulamasıyla gelişmiş HTTP kullanmasını sağlayabilirsiniz.<!--1358228-->

Daha fazla bilgi için bkz. [ağ erişim hesabı](accounts.md#network-access-account).

### <a name="package-access-account"></a>Paket erişim hesabı

Varsayılan olarak, Configuration Manager bir dağıtım noktasındaki içeriğe, kullanıcılara ve yöneticilere genel erişim hesapları için erişim verir. Ancak, erişimi kısıtlamak için ek izinler yapılandırabilirsiniz.

Daha fazla bilgi için bkz. [paket erişim hesabı](accounts.md#package-access-account).


## <a name="bandwidth-throttling-and-scheduling"></a>Bant genişliği daraltma ve zamanlama

Hem daraltma hem de zamanlama, içeriğin ne zaman bir site sunucusundan dağıtım noktalarına dağıtılacağını denetlemenize yardımcı olan seçeneklerdir. Bu yetenekler, siteden siteye dosya tabanlı çoğaltma için bant genişliği denetimleriyle doğrudan ilgili değildir ancak ile benzerdir.  

Daha fazla bilgi için bkz. [ağ bant genişliğini yönetme](manage-network-bandwidth.md).


## <a name="binary-differential-replication"></a>İkili farklar çoğaltması

Configuration Manager, daha önce diğer sitelere veya uzak dağıtım noktalarına dağıttığınız içeriği güncelleştirmek için ikili farklar çoğaltmasını (BDR) kullanır. BDR 'nin bant genişliği kullanımını azaltmasını desteklemek için, dağıtım noktalarına **uzaktan değişiklikleri sıkıştırma** özelliğini yükler. Daha fazla bilgi için bkz. [dağıtım noktası önkoşulları](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq).

BDR, dağıtılmış içeriğe ilişkin güncelleştirmeleri göndermek için kullanılan ağ bant genişliğini en aza indirir. Bu dosyaları her değiştirdiğiniz her içerik kaynak dosyası kümesinin tamamını göndermek yerine yalnızca yeni veya değişen içeriği yeniden sonlandırır.  

BDR kullanıldığında Configuration Manager, daha önce dağıttığınız her içerik kümesi için kaynak dosyalarda meydana gelen değişiklikleri tanımlar.  

- Kaynak içerikteki dosyalar değiştiğinde, site içeriğin yeni bir artımlı sürümünü oluşturur. Daha sonra yalnızca değiştirilen dosyaları hedef sitelere ve dağıtım noktalarına çoğaltır. Yeniden adlandırdıysanız veya taşıdıysanız ya da dosyanın içeriğini değiştirdiyseniz bir dosya değiştirilmiş olarak kabul edilir. Örneğin, daha önce birkaç siteye dağıttığınız bir sürücü paketi için tek bir sürücü dosyasını değiştirirseniz, yalnızca değiştirilen sürücü dosyası çoğaltılır.  

- Configuration Manager, içerik kümesinin tamamını yeniden yazmadan önce bir içerik kümesinin beş adede kadar artımlı sürümünü destekler. Beşinci güncelleştirmeden sonra, içerik kümesinde yapılan bir sonraki değişiklik, sitenin içerik kümesinin yeni bir sürümünü oluşturmasına neden olur. Configuration Manager daha sonra, önceki kümeyi ve onun artımlı sürümlerini değiştirmek için içerik kümesinin yeni sürümünü dağıtır. Yeni içerik kümesi dağıtıldıktan sonra, kaynak dosyalarda daha sonra artımlı değişiklikler BDR tarafından yeniden çoğaltılır.  

BDR, hiyerarşideki her üst ve alt site arasında desteklenir. BDR, site sunucusu ile normal dağıtım noktaları arasındaki bir site içinde desteklenir. Bununla birlikte, çekme dağıtım noktaları ve bulut dağıtım noktaları, içerik aktarmak için BDR 'yi desteklemez. Çekme dağıtım noktaları dosya düzeyi deltas destekler, yeni dosyaları aktarma, ancak bir dosya içinde blokları desteklemez.

Uygulamalar her zaman ikili farklar çoğaltmasını kullanır. BDR, paketler için isteğe bağlıdır ve varsayılan olarak etkin değildir. Paketler için BDR 'yi kullanmak için, her paket için bu işlevi etkinleştirin. Bir paket oluştururken veya düzenlerken **ikili değişiklik çoğaltmasını etkinleştir** seçeneğini belirleyin.


### <a name="bdr-or-delta-replication"></a>BDR veya Delta çoğaltma

<!-- SCCMDocs#1209 -->
Aşağıdaki listeler, *ikili farklar çoğaltması* (BDR) ve *Delta çoğaltma*arasındaki farklılıkları özetler.

#### <a name="summary-of-binary-differential-replication"></a>İkili değişiklik çoğaltmasının Özeti

- Windows **uzaktan değişiklikleri sıkıştırma** için Configuration Manager terimi
- *Blok*düzeyinde farklılıklar
- Uygulamalar için her zaman etkin
- Eski paketlerde isteğe bağlı
- Dağıtım noktasında zaten bir dosya varsa ve bir değişiklik varsa, site tüm dosya yerine blok düzeyinde değişikliği çoğaltmak için BDR 'yi kullanır.

#### <a name="summary-of-delta-replication"></a>Delta çoğaltma Özeti

- *Dosya*düzeyi farklılıkları
- Varsayılan olarak açık, yapılandırılamaz
- Bir paket değiştiğinde, site tüm paket yerine ayrı dosyalarda değişiklik olup olmadığını denetler.
    - Bir dosya değişirse, işi yapmak için BDR kullanın
    - Yeni bir dosya varsa, yeni dosyayı kopyalayın


## <a name="peer-caching-technologies"></a>Eş önbelleğe alma teknolojileri

<!-- SCCMDocs#1044 -->

Configuration Manager, aynı ağdaki eş cihazlar arasında içerik yönetmeye yönelik çeşitli seçenekleri destekler:

- [BranchCache](#branchcache)
- [Teslim Iyileştirme](#delivery-optimization)
- [Configuration Manager eş önbelleği](#peer-cache)

Aşağıdaki tabloyu kullanarak bu teknolojilerin önemli özelliklerini karşılaştırın:

| Özellik  | Eş &nbsp; önbellek  | Teslim &nbsp; iyileştirme  | BranchCache  |
|---------|---------|---------|---------|
| Alt ağlar arasında | Yes | Yes | Hayır |
| Bant genişliğini kısıtlama | Evet (BITS) | Evet (yerel) | Evet (BITS) |
| Kısmi içerik | Yes | Yes | Yes |
| Diskte denetim önbelleği boyutu | Yes | Yes | Yes |
| Eş kaynak keşfi | El ile (istemci ayarı) | Automatic | Automatic |
| Eş keşfi | Sınır grupları kullanarak yönetim noktası aracılığıyla | Bulut hizmeti yap | Yayınla |
| Raporlama | İstemci veri kaynakları panosu | İstemci veri kaynakları panosu | İstemci veri kaynakları panosu |
| WAN kullanım denetimi | Sınır grupları | GroupID yap | Yalnızca alt ağ |
| Desteklenen içerik | Tüm ConfigMgr içeriği | Windows güncelleştirmeleri, sürücüler, Mağaza uygulamaları | Tüm ConfigMgr içeriği |
| İlke denetimi | İstemci Aracısı ayarları | İstemci Aracısı ayarları (kısmi) | İstemci Aracısı ayarları |

### <a name="recommendations"></a>Öneriler

- Modern yönetim: Intune gibi modern araçları zaten kullanıyorsanız, teslim Iyileştirme uygulayın

- Configuration Manager ve ortak yönetim: eş önbellek ve teslim Iyileştirmesinin birleşimini kullanın. Eş önbellek 'yi şirket içi dağıtım noktalarıyla kullanın ve bulut senaryoları için teslim Iyileştirmesi kullanın.

- Mevcut BranchCache uygulandı: üç teknolojiyi de paralel olarak kullanın. BranchCache tarafından desteklenmeyen senaryolar için eş önbellek ve teslim Iyileştirmesi kullanın.


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) bir Windows teknolojisidir. BranchCache 'i destekleyen ve BranchCache için yapılandırdığınız bir dağıtımı indirmiş olan istemciler, daha sonra BranchCache özellikli diğer istemcilere bir içerik kaynağı olarak görev yapar.  

Örneğin, Windows Server 2012 veya üstünü çalıştıran ve BranchCache sunucusu olarak yapılandırılmış bir dağıtım noktanız vardır. BranchCache özellikli ilk istemci bu sunucudan içerik istediğinde, istemci bu içeriği indirir ve önbelleğe alır.  

- Bu istemci daha sonra içeriği aynı alt ağda bulunan BranchCache özellikli ek istemciler için de içeriği önbelleğe alarak kullanılabilir hale getirir.  
- Aynı alt ağdaki diğer istemciler, dağıtım noktasından içerik indirmek zorunda kalmaz.  
- İçerik, gelecekteki aktarımlar için birden fazla istemciye dağıtılır.  

Daha fazla bilgi için bkz. [Windows BranchCache Için destek](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache).

## <a name="delivery-optimization"></a>Teslim Iyileştirme

<!-- 1324696 -->
Şirket ağınızda ve Uzak ofislerde içerik dağıtımını tanımlamak ve düzenlemek için Configuration Manager sınır gruplarını kullanırsınız. [Windows teslim iyileştirme](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) , Windows 10 cihazları arasında içerik paylaşmak için bulut tabanlı ve eşler arası bir teknolojidir. Dağıtım Iyileştirmesini, içerik eşleri arasında paylaşırken sınır gruplarınızı kullanacak şekilde yapılandırın. İstemci ayarları, sınır grubu tanımlayıcısını istemcide teslim Iyileştirme grubu tanımlayıcısı olarak uygular. İstemci, teslim Iyileştirme bulut hizmeti ile iletişim kurduğunda, içerik ile eşleri bulmak için bu tanımlayıcıyı kullanır. Daha fazla bilgi için bkz. [teslim iyileştirme](../../clients/deploy/about-client-settings.md#delivery-optimization) istemci ayarları.

Teslim Iyileştirme, Windows 10 kalite güncelleştirmeleri için hızlı yükleme dosyalarının Windows 10 güncelleştirme teslimini iyileştirmek için önerilen teknolojiden oluşur. Configuration Manager sürüm 1910 ' den başlayarak, dağıtım Iyileştirmesi bulut hizmetine yönelik Deliveryınternet erişimi, eşler arası işlevselliğini kullanmak için bir gereksinimdir. Gerekli Internet uç noktaları hakkında daha fazla bilgi için bkz. [dağıtım iyileştirmesi hakkında sık sorulan sorular](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). En iyi duruma getirme, tüm Windows güncelleştirmeleri için kullanılabilir. Daha fazla bilgi için bkz. [Windows 10 güncelleştirme teslimini iyileştirme](../../../sum/deploy-use/optimize-windows-10-update-delivery.md).


## <a name="microsoft-connected-cache"></a>Microsoft Bağlı Önbellek

<!--3555764-->
Sürüm 1906 ' den başlayarak dağıtım noktalarınıza Microsoft bağlı önbellek sunucusu yükleyebilirsiniz. Bu içeriği şirket içinde önbelleğe alarak istemcileriniz teslim Iyileştirme özelliğinden yararlanabilir, ancak WAN bağlantılarını korumaya yardımcı olabilirsiniz.

> [!NOTE]
> Sürüm 1910 ' den başlayarak, bu özellik artık **Microsoft bağlı önbelleği**olarak adlandırılmaktadır. Daha önce teslim Iyileştirmesi-ağ önbelleği olarak bilinirdi.

Bu önbellek sunucusu teslim Iyileştirmesi tarafından indirilen içerik için isteğe bağlı bir saydam önbellek işlevi görür. Bu sunucunun yalnızca yerel Configuration Manager sınır grubunun üyelerine sunulmakta olduğundan emin olmak için istemci ayarlarını kullanın.

Bu önbellek Configuration Manager dağıtım noktası içeriğinden ayrıdır. Dağıtım noktası rolüyle aynı sürücüyü seçerseniz, içeriği ayrı olarak depolar.

Daha fazla bilgi için bkz. [Microsoft bağlı önbelleği Configuration Manager](microsoft-connected-cache.md).


## <a name="peer-cache"></a>Eş önbellek

İstemci eş önbelleği, uzak konumlardaki istemcilerin içerik dağıtımını yönetmenize yardımcı olur. Eş önbellek, istemcilerin diğer istemcilerle doğrudan yerel Önbelleklerinden içerik paylaşmasını sağlayan yerleşik bir Configuration Manager çözümüdür.

Önce, bir koleksiyona eş önbelleği etkinleştiren istemci ayarlarını dağıtın. Daha sonra, bu koleksiyonun üyeleri aynı sınır grubundaki diğer istemciler için bir eş içerik kaynağı olarak hareket edebilir.

Sürüm 1806 ' den başlayarak, istemci eş önbelleği kaynakları içeriği parçalara ayırabilir. Bu parçalar, WAN kullanımını azaltmak için Ağ aktarımını en aza indirir. Yönetim noktası, içerik bölümlerinin daha ayrıntılı bir şekilde izlenmesini sağlar. Aynı içeriğin her sınır grubu için birden fazla indirilmesini ortadan kaldırmaya çalışır.<!--1357346-->

Daha fazla bilgi için bkz. [Configuration Manager istemcileri Için eş önbellek](client-peer-cache.md).


## <a name="windows-pe-peer-cache"></a>Windows PE eş önbelleği

Configuration Manager ile yeni bir işletim sistemi dağıtırken, görev dizisini çalıştıran bilgisayarlar Windows PE Eş Önbelleği kullanabilir. Bir dağıtım noktası yerine bir eş önbellek kaynağından içerik indirir. Bu davranış, yerel dağıtım noktası olmayan şube senaryolarında WAN trafiğini en aza indirmeye yardımcı olur.

Daha fazla bilgi için bkz. [WINDOWS PE Eş Önbelleği](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="windows-ledbat"></a>Windows LEDBAT

<!--1358112-->
Windows düşük ekstra gecikmeli arka plan taşıması (LEDBAT), arka plan ağ aktarımlarının yönetilmesine yardımcı olmak için Windows Server 'ın bir ağ tıkanıklığı denetim özelliğidir. Desteklenen Windows Server sürümlerinde çalışan dağıtım noktaları için, ağ trafiğini ayarlamanıza yardımcı olacak bir seçenek etkinleştirin. İstemciler yalnızca kullanılabilir olduğunda ağ bant genişliğini kullanır.

Genel olarak Windows LEDBAT hakkında daha fazla bilgi için [yeni aktarım](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726) geliştirmeleri Web günlüğü gönderisine bakın.

Windows LEDBAT 'i Configuration Manager dağıtım noktalarıyla kullanma hakkında daha fazla bilgi için, [bir dağıtım noktasının genel ayarlarını yapılandırırken](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general) **kullanılmayan ağ bant GENIŞLIĞINI (Windows ledbat) kullanmak üzere indirme hızını ayarlama** ayarına bakın.


## <a name="client-locations"></a>İstemci konumları

Aşağıdakiler istemcilerin içeriğe erişebileceği konumlardır:  

- **İntranet** (şirket içi):  

    - Dağıtım noktaları HTTP veya HTTPs kullanabilir.  

    - Yalnızca şirket içi dağıtım noktaları kullanılabilir olmadığında geri dönüş için bir bulut dağıtım noktası kullanın.  

- **Internet**:  

    - HTTPS 'yi kabul etmek için internet 'e yönelik dağıtım noktaları gerektirir.  

    - , Bir bulut dağıtım noktası veya bulut yönetimi ağ geçidi (CMG) kullanabilir.  

        Sürüm 1806 ' den başlayarak bir CMG, istemcilere içerik de sunabilir. Bu işlevsellik, Azure VM 'lerinin gerekli sertifikalarını ve maliyetini azaltır. Daha fazla bilgi için bkz. [CMG 'Yi değiştirme](../../clients/manage/cmg/setup-cloud-management-gateway.md).

- **Çalışma grubu**:  

    - Dağıtım noktalarının HTTPS kabul etmesini gerektirir.  

    - , Bir bulut dağıtım noktası veya CMG kullanabilir.  


## <a name="content-source-priority"></a>İçerik kaynağı önceliği

Bir istemci içeriğe ihtiyaç duyduğunda, yönetim noktasına bir içerik konumu isteği yapar. Yönetim noktası, istenen içerik için geçerli olan kaynak konumların bir listesini döndürür. Bu liste, belirli senaryoya, kullanımdaki teknolojilere, site tasarımına, sınır gruplarına ve dağıtım ayarlarına bağlı olarak değişir. Aşağıdaki listede, bir istemcinin kullanabileceği tüm olası içerik kaynak konumları, bunların öncelik sırasına göre verilmiştir:  

1. İstemciyle aynı bilgisayardaki dağıtım noktası
2. Aynı ağ alt ağındaki eş kaynak
3. Aynı ağ alt ağındaki bir dağıtım noktası
4. Aynı sınır grubundaki bir eş kaynağı
5. Geçerli sınır grubundaki bir dağıtım noktası
6. Bir komşu sınır grubundaki geri dönüş için yapılandırılmış bir dağıtım noktası
7. Varsayılan site sınır grubundaki bir dağıtım noktası
8. Windows Update bulut hizmeti
9. İnternet 'e yönelik bir dağıtım noktası
10. Azure 'da bir bulut dağıtım noktası

> [!Note]  
> <!-- SCCMDocs#1607 -->Teslim Iyileştirme bu kaynak önceliği için geçerli değildir. Bu liste, Configuration Manager istemcisinin içeriği nasıl bulduğunu belirler. Windows Update Aracısı teslim Iyileştirme için içerik indirir. Windows Update Aracısı içeriği bulamazsa, Configuration Manager istemcisi bu listeyi aramak için kullanır.

## <a name="content-library"></a>İçerik Kitaplığı

İçerik kitaplığı, Configuration Manager içeriğin tek örnekli deposudur. Bu kitaplık, dağıttığınız içeriğin genel boyutunu azaltır.  

- [İçerik kitaplığı](the-content-library.md)hakkında daha fazla bilgi edinin.
- Artık bir uygulamayla ilişkili olmayan içeriği kaldırmak için [içerik kitaplığı Temizleme aracını](content-library-cleanup-tool.md) kullanın.  


## <a name="distribution-points"></a>Dağıtım noktaları

Configuration Manager, yazılımın istemci bilgisayarlarında çalışması için gerekli dosyaları depolamak için dağıtım noktalarını kullanır. İstemcilerin, dağıttığınız içerik için dosyaları indirebilecekleri en az bir dağıtım noktasına erişimi olmalıdır.  

Temel (özel olmayan) dağıtım noktası genellikle standart dağıtım noktası olarak adlandırılır. Standart dağıtım noktasında özel olarak dikkat edilen iki çeşitleme vardır:  

- **Çekme dağıtım noktası**: dağıtım noktasının başka bir dağıtım noktasından (bir kaynak dağıtım noktası) içerik aldığı bir dağıtım noktasının çeşitlemesi. Bu işlem, istemcilerin dağıtım noktalarından içerik indirmelerine benzer. Çekme dağıtım noktaları, site sunucusunun içeriği her dağıtım noktasına doğrudan dağıtması gerektiğinde oluşan ağ bant genişliği performans sorunlarını önlemenize yardımcı olabilir. [Bir çekme dağıtım noktası kullanın](use-a-pull-distribution-point.md).

- **Bulut dağıtım noktası**: Microsoft Azure yüklenen bir dağıtım noktası çeşitlemesi. [Bulut dağıtım noktası kullanmayı öğrenin](use-a-cloud-based-distribution-point.md).  

Standart dağıtım noktaları, bir dizi yapılandırma ve özelliği destekler:  

- Bu aktarımı denetlemeye yardımcı olması için **zamanlamalar** veya **bant genişliği azaltma** gibi denetimleri kullanın.  

- **Önceden hazırlanan içerik**ve ağ tüketimini en aza indirmek ve denetlemek için **çekme dağıtım noktaları** dahil diğer seçenekleri kullanın.  

- **BranchCache**, **eş önbellek**ve **teslim iyileştirme** , içerik dağıtırken kullanılan ağ bant genişliğini azaltmak için eşler arası teknolojilerdir.  

- İşletim sistemi dağıtımları için **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** ve **[çok noktaya yayın](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** gibi farklı yapılandırma vardır  

- **Mobil cihaz** seçenekleri  
  
Bulut ve çekme dağıtım noktaları aynı yapılandırmaların çoğunu destekler, ancak her bir dağıtım noktası varyasyonuna özgü sınırlamalar vardır.  


## <a name="distribution-point-groups"></a>Dağıtım noktası grupları

Dağıtım noktası grupları, içerik dağıtımını basitleştirebilecek dağıtım noktalarının mantıksal gruplandırmalarıdır.  

Daha fazla bilgi için bkz. [dağıtım noktası gruplarını yönetme](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).


## <a name="distribution-point-priority"></a>Dağıtım noktası önceliği

Dağıtım noktası öncelik değeri önceki dağıtımların o dağıtım noktasına aktarımının ne kadar sürdüğünü temel alır.  

- Bu değer kendi kendini ayarlamadır. Her dağıtım noktasında, daha fazla dağıtım noktasına içerik daha hızlı bir şekilde aktarmaya Configuration Manager yardımcı olacak şekilde ayarlanır.  

- İçeriği aynı anda birden çok dağıtım noktasına veya bir dağıtım noktası grubuna dağıttığınızda, site ilk olarak içeriği en yüksek önceliğe sahip sunucuya gönderir. Daha sonra, aynı içeriği daha düşük önceliğe sahip bir dağıtım noktasına gönderir.  

- Dağıtım noktası önceliği, paketler için dağıtım önceliğinin yerini almaz. Paket önceliği, sitenin farklı içerik gönderdiği karar derecesi olarak kalır.  

Örneğin, yüksek paket önceliğine sahip bir paketiniz vardır. Bunu, düşük bir dağıtım noktası önceliğine sahip bir sunucuya dağıtırsınız. Bu yüksek öncelikli paket, en düşük önceliğe sahip bir paketten önce her zaman aktarır. Site daha düşük öncelikli paketleri daha yüksek dağıtım noktası öncelikleri olan sunuculara dağıtsa bile paket önceliği geçerlidir.

Paketin yüksek önceliği, Configuration Manager daha düşük önceliğe sahip herhangi bir paket göndermeden önce bu içeriği dağıtım noktalarına dağıtmasını sağlar.  

> [!NOTE]  
> Çekme dağıtım noktaları, kaynak dağıtım noktalarının sırasını belirlemek için bir öncelik kavramı da kullanır.  
>
> - Sunucuya içerik aktarımları için dağıtım noktası önceliği, çekme dağıtım noktalarının kullandığı öncelikten farklıdır. Çekme dağıtım noktaları, kaynak dağıtım noktasından içerik ararken bunların önceliklerini kullanır.  
> - Daha fazla bilgi için bkz. [çekme dağıtım noktası kullanma](use-a-pull-distribution-point.md).  


## <a name="fallback"></a>Geri dönüş

İstemciler, geri dönüş dahil olmak üzere içeriği olan bir dağıtım noktasını bulmadığının Configuration Manager geçerli dalı ile değiştirilmiştir.

Geçerli sınır grubuyla ilişkili bir dağıtım noktasından içerik bulamamaları gereken istemciler, komşu sınır gruplarıyla ilişkili içerik kaynak konumlarını kullanmaya geri döner. Geri dönüş için kullanılmak üzere, bir komşu sınır grubunun istemcinin geçerli sınır grubuyla tanımlı bir ilişkisi olmalıdır. Bu ilişki, içeriği yerel olarak bulamamayan bir istemci, aramasının bir parçası olarak komşu sınır grubundan içerik kaynakları dahil etmeden önce geçmesi gereken yapılandırılmış bir süreyi içerir.

Tercih edilen dağıtım noktalarının kavramları artık kullanılmamaktadır ve **içerik için geri dönüş kaynak konumlarına Izin ver** ayarları artık kullanılamaz veya zorlanmaz.

Daha fazla bilgi için bkz. [sınır grupları](../../servers/deploy/configure/boundary-groups.md).


## <a name="network-bandwidth"></a>Ağ bant genişliği

İçerik dağıtırken kullanılan ağ bant genişliği miktarını yönetmenize yardımcı olmak için aşağıdaki seçenekleri kullanabilirsiniz:  

- **Önceden hazırlanan içerik**: içeriği ağ üzerinden dağıtmadan bir dağıtım noktasına içerik aktarma.  

- **Zamanlama ve daraltma**: İçeriğin dağıtım noktalarına ne zaman ve nasıl dağıtılacağını denetlemenize yardımcı olan yapılandırma.  

Daha fazla bilgi için bkz. [ağ bant genişliğini yönetme](manage-network-bandwidth.md).


## <a name="network-connection-speed-to-content-source"></a>İçerik kaynağına yönelik ağ bağlantısı hızı

İstemcilerin içeriği olan bir dağıtım noktası bulması için Configuration Manager geçerli Dalla birlikte çeşitli şeyler değişmiştir. Bu değişiklikler, bir içerik kaynağına yönelik ağ hızını içerir.

**Hızlı** veya **yavaş** olarak bir dağıtım noktası tanımlayan ağ bağlantı hızları artık kullanılmamaktadır. Bunun yerine, bir sınır grubuyla ilişkilendirilmiş her site sistemi aynı şekilde değerlendirilir.

Daha fazla bilgi için bkz. [sınır grupları](../../servers/deploy/configure/boundary-groups.md).


## <a name="on-demand-content-distribution"></a>İsteğe bağlı içerik dağıtımı

İsteğe bağlı içerik dağıtımı, bireysel uygulama ve paket dağıtımları için bir seçenektir. Bu seçenek, tercih edilen sunuculara yönelik isteğe bağlı içerik dağıtımını sağlar.  

- Bu ayarı bir dağıtım için etkinleştirmek üzere etkinleştirin: **Bu paketin içeriğini tercih edilen dağıtım noktalarına dağıtın**.  

- Bu seçeneği bir dağıtım için etkinleştirdiğinizde ve bir istemci, istemcinin tercih ettiği dağıtım noktalarında bu içeriği ancak içeriği istediğinde, Configuration Manager otomatik olarak istemcinin tercih edilen dağıtım noktalarına dağıtır.  

- Bu, içeriği otomatik olarak bu istemcinin tercih edilen dağıtım noktalarına dağıtmak üzere Configuration Manager tetiklerse, istemci için tercih edilen dağıtım noktaları dağıtımı almadan önce istemci o içeriği diğer dağıtım noktalarından elde edebilir. Bu davranış oluştuğunda, içerik o dağıtımı arayan bir sonraki istemci tarafından kullanılmak üzere bu dağıtım noktasında mevcut olacaktır.  

Daha fazla bilgi için bkz. [sınır grupları](../../servers/deploy/configure/boundary-groups.md).


## <a name="package-transfer-manager"></a>Paket Aktarma Yöneticisi

Paket Aktarma Yöneticisi, diğer bilgisayarlardaki dağıtım noktalarına içerik aktaran site sunucusu bileşenidir.  

Daha fazla bilgi için bkz. [Paket Aktarma Yöneticisi](package-transfer-manager.md).  


## <a name="prestage-content"></a>İçeriği önceden hazırlama

İçeriği önceden hazırlama, içeriği ağ üzerinden dağıtmadan bir dağıtım noktasına aktarmaya yönelik bir işlemdir.  

Daha fazla bilgi için bkz. [ağ bant genişliğini yönetme](manage-network-bandwidth.md).
