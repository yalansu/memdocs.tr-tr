---
title: Yazılım güncelleştirmelerini planlama
titleSuffix: Configuration Manager
description: Yazılım güncelleştirme noktası altyapısı için bir plan, Configuration Manager üretim ortamında yazılım güncelleştirmelerini kullanmadan önce gereklidir.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: 991f367dbd842037aecf4f808f27c4fb2961cc38
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696727"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Configuration Manager yazılım güncelleştirmelerini planlayın

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager üretim ortamında yazılım güncelleştirmelerini kullanmadan önce, planlama sürecinde ileretmeniz önemlidir. Yazılım güncelleştirme noktası altyapısı için iyi bir plana sahip olmak, başarılı bir yazılım güncelleştirmeleri uygulamasının anahtarıdır. Yazılım güncelleştirmeleri için kapasite planlaması hakkında daha fazla bilgi için bkz. [boyut ve ölçek numaraları](../../core/plan-design/configs/size-and-scale-numbers.md#software-update-point).


##  <a name="determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a> Yazılım güncelleştirme noktası altyapısını belirleme  

Bu bölüm aşağıdaki alt konuları içerir:    
- [Yazılım güncelleştirme noktası listesi](#BKMK_SUPList)
- [Yazılım güncelleştirme noktası değiştirme](#BKMK_SUPSwitching)
- [İstemcileri el ile yeni bir yazılım güncelleştirme noktasına değiştirme](#BKMK_ManuallySwitchSUPs)
- [Güvenilmeyen bir ormandaki yazılım güncelleştirme noktaları](#BKMK_SUP_CrossForest)
- [Üst düzey sitede eşitleme kaynağı olarak var olan bir WSUS sunucusunu kullan](#BKMK_WSUSSyncSource)
- [İkincil sitedeki yazılım güncelleştirme noktası](#BKMK_SUPSecSite)  
- [Internet tabanlı istemciler için plan](#bkmk_internet-clients)  
- [Yazılım güncelleştirme içeriğini planlayın](#bkmk_content)  
- [Üçüncü taraf güncelleştirmeleri için plan yapın](#bkmk_thirdparty)  


Merkezi Yönetim sitesi ve tüm alt birincil siteler bir yazılım güncelleştirme noktasına sahip olmalıdır. Yazılım güncelleştirme noktası altyapısını planlarken, aşağıdaki bağımlılıkları saptayın:
- Site için yazılım güncelleştirme noktasının nereye yükleneceği  
- Internet tabanlı istemcilerden gelen iletişimi kabul eden bir yazılım güncelleştirme noktası gerektiren siteler
- İkincil sitelerde bir yazılım güncelleştirme noktasına ihtiyacınız olup olmadığı  

> [!IMPORTANT]  
>  Yazılım güncelleştirmeleri için gereken iç ve dış bağımlılıklar hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri Için Önkoşullar](prerequisites-for-software-updates.md).  

Hata toleransı sağlamak için Configuration Manager birincil sitesine birden çok yazılım güncelleştirme noktası ekleyin. Yazılım güncelleştirme noktasının yük devretme tasarımı, yönetim noktaları için tasarımda kullanılan saf rasgeleleştirme modelinden farklıdır. Yönetim noktalarının tasarımından farklı olarak, istemciler yeni bir yazılım güncelleştirme noktasına geçiş yaparken yazılım güncelleştirme noktası tasarımında istemci ve ağ performans maliyetleri vardır. İstemci yazılım güncelleştirmelerini taramak üzere yeni bir WSUS sunucusuna geçtiğinde, bu, katalog büyüklüğünde ve ilişkili istemci tarafı ve ağ performansı taleplerinde bir artışa yol açar. Bu nedenle, istemci, başarıyla tarandığı son yazılım güncelleştirme noktasıyla benzeşimli olarak korunur.  

Bir birincil siteye yüklediğiniz ilk yazılım güncelleştirme noktası, birincil siteye eklediğiniz tüm ek yazılım güncelleştirme noktaları için eşitleme kaynağıdır. Yazılım güncelleştirme noktalarını ekledikten ve eşitlemeyi başlattıktan sonra, yazılım güncelleştirme noktalarının durumunu ve **izleme** çalışma alanındaki **yazılım güncelleştirme noktası eşitleme durumu** düğümünden eşitleme kaynağını görüntüleyin.  

Site için eşitleme kaynağı olarak yapılandırılan yazılım güncelleştirme noktası hatası olduğunda, başarısız rolü el ile kaldırın. Ardından eşitleme kaynağı olarak kullanmak üzere yeni bir yazılım güncelleştirme noktası seçin. Daha fazla bilgi için bkz. [site sistemi rolünü kaldırma](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role).  


###  <a name="software-update-point-list"></a><a name="BKMK_SUPList"></a> Yazılım güncelleştirme noktası listesi  

Configuration Manager, aşağıdaki senaryolarda istemciye bir yazılım güncelleştirme noktası listesi sağlar:  

- Yeni bir istemci, yazılım güncelleştirmelerini etkinleştirme ilkesini alır  

- İstemci, atanmış yazılım güncelleştirme noktasıyla bağlantı kuramıyor ve başka bir anahtara geçiş yapması gerekiyor  

İstemci listeden rastgele bir yazılım güncelleştirme noktası seçer. Aynı ormandaki yazılım güncelleştirme noktalarını önceliklendirir. Configuration Manager, istemci türüne bağlı olarak, istemcilere farklı bir liste sağlar:  

-   **Intranet tabanlı istemciler**: yalnızca intranetten bağlantılara izin vermek üzere yapılandırabileceğiniz Yazılım güncelleştirme noktalarının listesini veya internet ve Intranet istemci bağlantılarına izin veren yazılım güncelleştirme noktalarının bir listesini alır.  

-   **Internet tabanlı istemciler**: yalnızca İnternet 'ten bağlantılara izin vermek üzere yapılandırdığınız yazılım güncelleştirme noktalarının listesini veya internet ve intranet istemci bağlantılarına izin veren yazılım güncelleştirme noktalarının bir listesini alır.  


###  <a name="software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a> Yazılım güncelleştirme noktası değiştirme  

> [!NOTE]  
> İstemciler yeni bir yazılım güncelleştirme noktası bulmak için sınır grupları kullanır. Geçerli yazılım güncelleştirme noktası artık erişilebilir değilse, yeni bir tane eklemek ve bulmak için sınır grupları da kullanır. Bir istemcinin bulabileceği sunucuları denetlemek için farklı sınır gruplarına bireysel yazılım güncelleştirme noktaları ekleyin. Daha fazla bilgi için bkz. [yazılım güncelleştirme noktaları](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

Bir sitede birden çok yazılım güncelleştirme noktanız varsa ve biri başarısız olursa ya da kullanılamaz hale gelirse, istemciler farklı bir yazılım güncelleştirme noktasına bağlanır. Bu yeni sunucu sayesinde istemciler en son yazılım güncelleştirmelerini taramaya devam eder. Bir istemci ilk olarak bir yazılım güncelleştirme noktasına atandığında, tarayamadıkça bu yazılım güncelleştirme noktasına atanmış kalır.  

Yazılım güncelleştirmeleri taraması, çeşitli farklı yeniden deneme veya yeniden deneme olmayan hata kodlarıyla başarısız olabilir. Tarama bir yeniden deneme hata koduyla başarısız olduğunda, istemci, yazılım güncelleştirme noktasında yazılım güncelleştirmelerini taramak için bir yeniden deneme işlemi başlatır. Bir yeniden deneme hata kodunda sonuçlanan yüksek düzey durumlar genelde, WSUS sunucusunun kullanılamaz olması veya geçici olarak aşırı yüklenmesi sebebiyledir. İstemci, yazılım güncelleştirmelerini tarayamadığında aşağıdaki süreci kullanır:  

1.  İstemci, yazılım güncelleştirmelerini tarar:  
    - Zamanlandığı zamanda
    - İstemci üzerindeki denetim masasından el ile çalıştırıldığında
    - İstemci bildirim eylemi aracılığıyla Configuration Manager konsolundan el ile çalıştırıldığında
    - Configuration Manager SDK yönteminden çalıştırıldığında  

2.  Tarama başarısız olursa, istemci 30 dakika bekleyerek taramayı yeniden dener. Aynı yazılım güncelleştirme noktasını kullanır.  

3.  İstemci 30 dakikada bir en az dört kez yeniden dener. Dördüncü hatadan sonra ve iki dakika daha bekledikten sonra, istemci, listesinde bir sonraki yazılım güncelleştirme noktasına gider.  

4.  İstemci bu işlemi yeni yazılım güncelleştirme noktasıyla tekrarlar. Başarılı bir taramadan sonra, istemci yeni yazılım güncelleştirme noktasına bağlanmaya devam eder.  

Aşağıdaki listede, yazılım güncelleştirme noktası yeniden deneme ve anahtarlama senaryolarına göz önünde bulundurmanız gereken ek bilgiler verilmiştir:  

-   Bir istemcinin intranet bağlantısı kesilirse ve yazılım güncelleştirmelerini tarayamazsa, başka bir yazılım güncelleştirme noktasına geçiş yapmaz. İstemci iç ağa veya intranetten bağlantılara izin veren bir yazılım güncelleştirme noktasına ulaşamadığı için bu hata beklenmektedir. Configuration Manager istemcisi, intranet yazılım güncelleştirme noktasının kullanılabilirliğini belirler.  

-   İnternet 'te istemcileri yönetiyorsanız ve Internet 'teki istemcilerden gelen iletişimi kabul etmek için birden çok yazılım güncelleştirme noktası yapılandırdıysanız, geçiş işlemi daha önce açıklanan standart yeniden deneme işlemini izler.  

-   Tarama işlemi başlarsa, ancak tarama tamamlanmadan önce istemci kapatılmışsa, tarama hatası olarak değerlendirilmez ve dört yeniden denemenin biri olarak sayılmaz.  

Configuration Manager aşağıdaki Windows Update Aracısı hata kodlarından herhangi birini aldığında, istemci bağlantıyı yeniden dener:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Bir hata kodunun anlamını aramak için, ondalık hata kodunu onaltılı olarak dönüştürün ve ardından bir sitede [Windows Update Agent-hata kodları wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx)gibi onaltılı değeri arayın. örneğin, 2149842970 ondalık hata kodu onaltılı bir 8024001A, bu da bir ilke değeri ayarlanmamış WU_E_POLICY_NOT_SET anlamına gelir.  


###  <a name="manually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a> İstemcileri el ile yeni bir yazılım güncelleştirme noktasına değiştirme

Etkin yazılım güncelleştirme noktasıyla ilgili sorunlar olduğunda Configuration Manager istemcileri yeni bir yazılım güncelleştirme noktasına geçirin. Bu değişiklik yalnızca bir istemci bir yönetim noktasından birden çok yazılım güncelleştirme noktası aldığında gerçekleşir.

> [!IMPORTANT]    
> Cihazları yeni bir sunucu kullanacak şekilde değiştirdiğinizde, cihazlar bu yeni sunucuyu bulmak için geri dönüş kullanır. İstemciler, bir sonraki yazılım güncelleştirmeleri tarama döngülerinde yeni yazılım güncelleştirme noktasına geçer.<!-- SCCMDocs#1537 -->
>
> Bu değişikliğe başlamadan önce, yazılım güncelleştirme noktalarınızın doğru sınır gruplarında olduğundan emin olmak için sınır grubu yapılandırmalarınızı gözden geçirin. Daha fazla bilgi için bkz. [yazılım güncelleştirme noktaları](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  
>
> Yeni bir yazılım güncelleştirme noktasına geçiş yapmak ek ağ trafiği oluşturur. Trafik miktarı, WSUS Yapılandırma ayarlarınıza bağlıdır, örneğin, eşitlenen sınıflandırmalar ve ürünler veya paylaşılan bir WSUS veritabanının kullanımı. Birden çok cihaza geçiş yapmayı planlıyorsanız, bakım pencereleri sırasında bunu yapmayı deneyin. Bu zamanlama, istemciler yeni yazılım güncelleştirme noktasını taradığı zaman ağınıza etkisini azaltır.  

#### <a name="process-to-switch-software-update-points"></a>Yazılım güncelleştirme noktalarını değiştirme işlemi  
Bu değişikliği bir cihaz koleksiyonunda başlatın. Tetiklendiğinde, istemciler bir sonraki taramada başka bir yazılım güncelleştirme noktası arar.  

1.  Configuration Manager konsolunda **varlıklar ve uyum** çalışma alanına gidin ve **Cihaz Koleksiyonları** düğümünü seçin.  

2.  Hedef koleksiyonu seçin. Şeridin **giriş** sekmesinde, **koleksiyon** grubunda, **İstemci bildirimi**' ne ve ardından **sonraki yazılım güncelleştirme noktasına geç ' e**tıklayın.  


###  <a name="software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> Güvenilmeyen bir ormandaki yazılım güncelleştirme noktaları  

Güvenilmeyen bir ormandaki istemcileri desteklemek için bir sitede bir veya daha fazla yazılım güncelleştirme noktası oluşturun. Başka bir ormana yazılım güncelleştirme noktası eklemek için, önce bu ormana bir WSUS sunucusu yükleyip yapılandırın. Ardından, yazılım güncelleştirme noktası site sistemi rolüne sahip bir Configuration Manager site sunucusu eklemek için Sihirbazı başlatın. Sihirbazda, güvenilmeyen ormandaki WSUS'ye başarılı şekilde bağlanmak üzere aşağıdaki ayarları yapılandırın:  

-   Güvenilmeyen ormandaki WSUS sunucusuna erişebilen bir **site sistemi yükleme hesabı** belirtin.  

-   WSUS sunucusuna bağlanmak için bir **WSUS sunucusu bağlantı hesabı** belirtin.  

Örneğin, iki yazılım güncelleştirme noktası (SUP01 ve SUP02) bulunan A ormanında bir birincil siteniz var. Aynı birincil site için, B ormanında iki yazılım güncelleştirme noktanız (SUP03 ve SUP04) de vardır. Bir sonraki yazılım güncelleştirme noktasına geçiş yaparken istemciler, sunucuları aynı ormandan önceliklendirmesine izin verir.  


###  <a name="use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a> Üst düzey sitede eşitleme kaynağı olarak var olan bir WSUS sunucusunu kullan  

Genellikle, hiyerarşinizdeki üst düzey site, yazılım güncelleştirmeleri meta verilerini Microsoft Update ile eşitlemek üzere yapılandırılmıştır. Kurumsal Güvenlik ilkeniz, üst düzey sitenin internet 'e erişmesine izin vermezse, en üst düzey site için eşitleme kaynağını mevcut bir WSUS sunucusunu kullanacak şekilde yapılandırın. Bu WSUS sunucusu Configuration Manager hiyerarşinizde değil. Örneğin, internet 'e bağlı bir ağda (DMZ) bir WSUS sunucusuna sahipsiniz, ancak üst düzey siteniz internet erişimi olmayan bir iç ağ içinde. DMZ 'deki WSUS sunucusunu, yazılım güncelleştirmeleri meta verileri için eşitleme kaynağınız olarak yapılandırın. Yazılım güncelleştirmelerini Configuration Manager için gereken ölçütlerle eşleştirmek için DMZ içindeki WSUS sunucusunu yapılandırın. Aksi takdirde, üst düzey site, beklediğiniz yazılım güncelleştirmelerini eşitlemeyebilir. Yazılım güncelleştirme noktasını yüklediğinizde bir WSUS sunucusu bağlantı hesabı yapılandırın. Bu hesabın DMZ 'deki WSUS sunucusuna erişmesi gerekir. Ayrıca, güvenlik duvarının ilgili bağlantı noktaları için trafiğe izin verdiğini onaylayın. Daha fazla bilgi için, [yazılım güncelleştirme noktası tarafından eşitleme kaynağı için kullanılan bağlantı noktaları](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS)bölümüne bakın.  


###  <a name="software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> İkincil sitedeki yazılım güncelleştirme noktası  

Yazılım güncelleştirme noktası ikincil bir sitede isteğe bağlıdır. İkincil bir siteye yalnızca bir yazılım güncelleştirme noktası yükler. İkincil sitede bir yazılım güncelleştirme noktası yüklü olmadığında, ikincil bir sitenin sınırları içindeki cihazlar atanmış birincil sitelerinde bir yazılım güncelleştirme noktası kullanır. İkincil sitedeki cihazlar ile üst birincil sitedeki yazılım güncelleştirme noktaları arasında sınırlı ağ bant genişliği olduğunda genellikle ikincil siteye bir yazılım güncelleştirme noktası yüklersiniz. Birincil sitedeki yazılım güncelleştirme noktası kapasite sınırına yaklaşırsa de bu yapılandırmayı kullanabilirsiniz. Bir yazılım güncelleştirme noktasını ikincil siteye başarıyla yükleyip yapılandırdıktan sonra, istemciler için site genelinde bir ilke güncelleştirilir ve yeni yazılım güncelleştirme noktasını kullanmaya başlar.  


### <a name="plan-for-internet-based-clients"></a><a name="bkmk_internet-clients"></a> Internet tabanlı istemciler için plan

Ağınızı Internet üzerinden dolaşan cihazları yönetmeniz gerektiğinde, bu cihazlarda yazılım güncelleştirmelerinin nasıl yönetileceğini gösteren bir plan geliştirin. Configuration Manager, bu senaryoya yönelik birkaç teknolojiyi destekler. Kuruluşunuzun gereksinimlerini karşılamak için gereken bir veya bir bileşim kullanın.

#### <a name="cloud-management-gateway"></a>Bulut yönetimi ağ geçidi
Microsoft Azure ' de bir bulut yönetimi ağ geçidi oluşturun ve internet tabanlı istemcilerden gelen trafiğe izin vermek için en az bir şirket içi yazılım güncelleştirme noktasını etkinleştirin. İstemciler İnternet üzerinde dolaşırken, yazılım güncelleştirme noktalarınıza karşı taramaya devam ederler. Tüm internet tabanlı istemciler her zaman Microsoft Update bulut hizmetinden içerik alır. 

Daha fazla bilgi için bkz. [bulut yönetimi ağ geçidini planlayın](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) ve [sınır gruplarını yapılandırın](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

#### <a name="internet-based-client-management"></a>Internet tabanlı istemci yönetimi
Bir yazılım güncelleştirme noktasını internet 'e yönelik bir ağa yerleştirin ve internet tabanlı istemcilerden gelen trafiğe izin vermek için etkinleştirin. İstemciler İnternet üzerinde dolaşırken, tarama için bu yazılım güncelleştirme noktasına geçer. Tüm internet tabanlı istemciler her zaman Microsoft Update bulut hizmetinden içerik alır.

Internet tabanlı istemci yönetiminin avantajları ve dezavantajları hakkında daha fazla bilgi için bkz. [İnternet 'te Istemcileri yönetme](../../core/clients/manage/manage-clients-internet.md).

#### <a name="windows-update-for-business"></a>İş İçin Windows Update
Iş Windows Update, en son kalite ve özellik güncelleştirmeleriyle Windows 10 cihazlarını her zaman güncel tutmanızı sağlar. Bu cihazlar, Windows Update bulut hizmetine doğrudan bağlanır. Configuration Manager, yazılım güncelleştirmelerini almak için WUfB ve WSUS kullanan Windows 10 bilgisayarları birbirinden ayırt edebilir.

Daha fazla bilgi için bkz. [iş için Windows Update tümleştirme](../deploy-use/integrate-windows-update-for-business-windows-10.md).


### <a name="plan-software-update-content"></a><a name="bkmk_content"></a> Yazılım güncelleştirme içeriğini planlayın

İstemciler, yüklemek için yazılım güncelleştirmeleri için içerik dosyalarını indirmeleri gerekir. Configuration Manager, bu içeriğin yönetimini ve teslimini desteklemek için çeşitli teknolojiler sağlar. Ya da istemcilerin doğrudan Microsoft Update bulut hizmetinden içerik almasını sağlamak veya istemek için yazılım güncelleştirme dağıtımlarını yapılandırın.

#### <a name="download-and-distribute-content"></a>İçerik indirme ve dağıtma 
Varsayılan olarak, Configuration Manager yazılım güncelleştirme yönetimi işlemi yerleşik içerik yönetimi özelliklerini kullanır. Bu özellikler Merkezi, tek örnekli depolama içerik kitaplığını ve dağıtım noktası site sistemi rolünün dağıtılmış tasarımını içerir. Yazılım güncelleştirme dağıtım paketlerini indirip dağıtırken bu özellikleri kullanırsınız. 

Daha fazla bilgi için bkz. [yazılım güncelleştirmelerini indirme](../deploy-use/download-software-updates.md).

#### <a name="manage-express-installation-files-for-windows-10"></a>Windows 10 için hızlı yükleme dosyalarını yönetme
Configuration Manager, Windows 10 güncelleştirmeleri için hızlı yükleme dosyalarının kullanılmasını destekler. Dağıtım Iyileştirmesi gibi hızlı güncelleştirme dosyaları ve destekleyici teknolojiler, büyük içerik dosyalarının istemcilere indirmesinin ağ etkisini azaltmaya yardımcı olabilir. 

Daha fazla bilgi için bkz. [Windows 10 güncelleştirme teslimini iyileştirme](../deploy-use/optimize-windows-10-update-delivery.md).

#### <a name="clients-download-content-from-the-internet"></a>İstemcileri internetten içerik indirir
Yazılım güncelleştirmelerini istemcilere dağıtırken, istemcileri Microsoft Update bulut hizmetinden içerik indirmek için dağıtımı yapılandırın. İstemciler başka bir içerik kaynağından içerik indirebilmemişse, yine de içeriği internet 'ten indirebilirler. 

Sürüm 1806 ' den başlayarak, yazılım güncelleştirmelerini dağıttığınızda bir dağıtım paketi oluşturmanız gerekmez. **Dağıtım paketi yok** seçeneğini belirlediğinizde istemciler, varsa yerel kaynaklardan içerik indirmeye devam edebilir, ancak genellikle Microsoft Update hizmetinden indirilir.<!--1357933-->

Internet tabanlı istemciler Microsoft Update bulut hizmetinden her zaman içerik indirir. Yazılım güncelleştirme dağıtım paketlerini bir bulut dağıtım noktasına dağıtmayın. Bulut dağıtım noktasıyla depolama alanı için ücretlendirilirsiniz, ancak istemciler bu paketleri indirmez. 


### <a name="plan-for-third-party-updates"></a><a name="bkmk_thirdparty"></a> Üçüncü taraf güncelleştirmeleri için plan yapın
Configuration Manager, Microsoft tarafından yayımlanan yazılım güncelleştirmelerini yerel olarak destekleyen WSUS ile tümleşir. Çoğu müşteri, aynı zamanda güncelleştirme gerektiren diğer üçüncü taraf uygulamaları kullanır. Üçüncü taraf uygulamalarının güncel tutulması için göz önünde bulundurmanız gereken birkaç seçenek vardır.

#### <a name="supersede-applications-to-update"></a>Güncelleştirilecek uygulamaları değiştirme
Mevcut uygulamaları yükseltmek veya değiştirmek için Configuration Manager 'de Uygulama Yönetimi özelliğiyle bir yerine geçme ilişkisi kullanın. Bir uygulamayı yenisiyle değiştirdiğinizde, yerine geçilen uygulamanın dağıtım türünü değiştirmek için yeni bir dağıtım türü belirtin. Ayrıca, yerine geçen uygulama yüklenmeden önce yerine geçilen uygulamayı yükseltmeye veya kaldırmaya karar verin.

Daha fazla bilgi için bkz. [uygulamaları gözden geçirme ve değiştirme](../../apps/deploy-use/revise-and-supersede-applications.md).

#### <a name="third-party-software-updates"></a>Üçüncü taraf yazılım güncelleştirmeleri
Sürüm 1806 ' den başlayarak, üçüncü taraf kataloglara abone olmak, güncelleştirmelerini yazılım güncelleştirme noktanya yayımlamak ve sonra istemcilere dağıtmak için Configuration Manager konsolundaki **üçüncü taraf yazılım güncelleştirme katalogları** düğümünü kullanın.<!--1352101-->

Daha fazla bilgi için bkz. [üçüncü taraf yazılım güncelleştirmeleri](../deploy-use/third-party-software-updates.md).

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
System Center Updates Publisher (SCUP), bağımsız yazılım satıcılarının veya iş kolu uygulaması geliştiricilerinin özel güncelleştirmeleri yönetmesine olanak tanıyan bağımsız bir araçtır. Bu güncelleştirmeler, sürücüler ve güncelleştirme paketleri gibi bağımlılıklara sahip olanları içerir.

Daha fazla bilgi için bkz. [System Center Updates Publisher](../tools/updates-publisher.md).



##  <a name="plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a> Yazılım güncelleştirme noktası yüklemesini planlayın  

Bu bölüm aşağıdaki alt konuları içerir:  
- [Yazılım güncelleştirme noktası gereksinimleri](#BKMK_SUPSystemRequirements)
- [WSUS yüklemesini planlayın](#BKMK_PlanningForWSUS)
- [Güvenlik duvarlarını yapılandırma](#BKMK_ConfigureFirewalls)  


Bu bölümde, yazılım güncelleştirme noktası yüklemesini başarıyla planlamak ve hazırlamak için uygulanması gereken adımlar hakkında bilgi verilmektedir. Configuration Manager yazılım güncelleştirme noktası için bir site sistemi rolü oluşturmadan önce göz önünde bulundurmanız gereken birkaç gereksinim vardır. Belirli gereksinimler Configuration Manager altyapısına bağlıdır. Yazılım güncelleştirme noktasını HTTPS kullanarak iletişim kuracak şekilde yapılandırdığınızda, bu bölümün incelenmesi özellikle önemlidir. HTTPS özellikli sunucular, düzgün çalışmak için ek adımlar gerektirir.  

###  <a name="requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> Yazılım güncelleştirme noktası gereksinimleri  

Yazılım güncelleştirme noktası rolünü, WSUS ve Configuration Manager site sistemleri için Desteklenen yapılandırmaların en düşük gereksinimlerini karşılayan bir site sistemine yükler.  

-   Windows Server 'da WSUS sunucu rolüne ilişkin en düşük gereksinimler hakkında daha fazla bilgi için bkz. [Gözden geçirme konuları ve sistem gereksinimleri](/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements).  

-   Configuration Manager site sistemleri için desteklenen konfigürasyonlar hakkında daha fazla bilgi için bkz. [site ve site sistemi önkoşulları](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


###  <a name="plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> WSUS yüklemesini planlama  

Yazılım güncelleştirme noktası rolü için yapılandırdığınız tüm site sistemi sunucularına WSUS 'nin desteklenen bir sürümünü yükleyebilirsiniz. Yazılım güncelleştirme noktasını site sunucusuna yüklememeniz durumunda, WSUS Yönetim Konsolu 'Nu site sunucusuna yükleyebilirsiniz. Bu bileşen, site sunucusunun yazılım güncelleştirme noktasında çalışan WSUS ile iletişim kurmasına olanak tanır.  

Windows Server 2012 veya sonraki sürümlerde WSUS kullandığınızda, Configuration Manager WSUS **Configuration Manager** bileşeninin WSUS 'a bağlanmasına izin vermek için ek izinler yapılandırın. Bu bileşen düzenli durum denetimleri gerçekleştirir. Gerekli izinleri yapılandırmak için aşağıdaki seçeneklerden birini belirleyin:  

-   **SYSTEM** hesabını **WSUS Administrators** grubuna ekle  

-   **NT AUTHORITY\SYSTEM** hesabını WSUS veritabanı (SUSDB) için bir kullanıcı olarak ekleyin. En düşük webService veritabanı rol üyeliğini yapılandırın.  
  
WSUS 'i Windows Server 'a yüklemek hakkında daha fazla bilgi için bkz. [WSUS sunucu rolünü yüklemek](/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Bir birincil siteye birden çok yazılım güncelleştirme noktası yüklediğinizde aynı Active Directory ormanındaki her yazılım güncelleştirme noktası için aynı WSUS veritabanını kullanın. Aynı veritabanının paylaşılması, istemciler yeni bir yazılım güncelleştirme noktasına geçiş yaparken performansı geliştirir. Daha fazla bilgi için bkz. [yazılım güncelleştirme noktaları için PAYLAŞıLAN WSUS veritabanı kullanma](software-updates-best-practices.md#bkmk_shared-susdb).  

#### <a name="configuring-the-wsus-content-directory-path"></a>WSUS içerik dizini yolunu yapılandırma

WSUS 'u yüklediğinizde bir içerik dizini yolu sağlamanız gerekir. WSUS içerik dizini öncelikle, tarama sırasında istemciler tarafından gereken Microsoft yazılım lisans koşulları dosyalarını depolamak için kullanılır. WSUS içerik dizininin Configuration Manager, Configuration Manager yazılım dağıtım paketleri için içerik kaynak dizininizle çakışmamalıdır. WSUS içerik dizininden ve Configuration Manager paket kaynağıyla örtüşerek, WSUS içerik dizininden yanlış dosyaların kaldırılmasına neden olur.

####  <a name="configure-wsus-to-use-a-custom-website"></a><a name="BKMK_CustomWebSite"></a> WSUS 'i özel bir Web sitesi kullanacak şekilde yapılandırma  
WSUS yüklerken mevcut IIS Varsayılan web sitesini kullanabilir veya özel bir WSUS web sitesi oluşturabilirsiniz. WSUS için özel bir Web sitesi oluşturun, böylece IIS, WSUS hizmetlerini ayrılmış bir sanal Web sitesinde barındırır. Aksi takdirde, diğer Configuration Manager site sistemleri veya uygulamaları tarafından kullanılan Web sitesini paylaşır. Bu yapılandırma özellikle yazılım güncelleştirme noktası rolünü site sunucusuna yüklediğinizde gereklidir. WSUS 'i Windows Server 2012 veya sonraki sürümlerde çalıştırdığınızda, WSUS varsayılan olarak HTTP için bağlantı noktası 8530 ve HTTPS için bağlantı noktası 8531 ' i kullanacak şekilde yapılandırılır. Bir sitede yazılım güncelleştirme noktası oluştururken bu bağlantı noktalarını belirtin.  


####  <a name="use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> Var olan bir WSUS altyapısını kullanma  
Configuration Manager yazılım güncelleştirme noktası olarak yüklemeden önce ortamınızda etkin olan bir WSUS sunucusu seçin. Yazılım güncelleştirme noktası yapılandırıldığında, eşitleme ayarlarını belirtin. Configuration Manager, yazılım güncelleştirme noktası sunucusunda çalışan WSUS sunucusuna bağlanır ve WSUS 'u aynı ayarlarla yapılandırır. 

Sunucuyu bir yazılım güncelleştirme noktası olarak yapılandırmadan önce, ürün ve sınıflandırmaların yapılandırmalarını Configuration Manager ayarlarınızla karşılaştırın. Mevcut WSUS sunucusunu bir yazılım güncelleştirme noktası olarak yapılandırmadan önce eşitledikten ve ürünlerin ve sınıflandırmaların listesi farklıysa, yapılandırılan ayarlardan bağımsız olarak tüm yazılım güncelleştirmeleri meta verilerini eşitler. Bu davranış, site veritabanında beklenmeyen yazılım güncelleştirmeleri meta verilerinin sonucu olarak sonuçlanır. 

Ürünleri veya sınıflandırmaları doğrudan WSUS yönetim konsoluna eklerken aynı davranışla karşılaşırsınız ve ardından bir eşitlemeyi hemen başlatabilirsiniz. Varsayılan olarak, her saat Configuration Manager WSUS 'a bağlanır ve Configuration Manager dışında değiştirilen tüm ayarları sıfırlar. Eşitleme ayarlarında belirttiğiniz ürün ve sınıflandırmaları karşılamayan yazılım güncelleştirmeleri, zaman aşımına uğradı olarak ayarlanır. Ardından, site veritabanından kaldırılır.  

Bir WSUS sunucusu bir yazılım güncelleştirme noktası olarak yapılandırıldığında, artık bunu bağımsız bir WSUS sunucusu olarak kullanamazsınız. Configuration Manager tarafından yönetilmeyen ayrı bir tek başına WSUS sunucusuna ihtiyacınız varsa, bunu farklı bir sunucuda yapılandırın.  

####  <a name="configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> WSUS'i çoğaltma sunucusu olarak yapılandırma  
Yazılım güncelleştirme noktası rolünü bir birincil site sunucusuna eklediğinizde, çoğaltma olarak yapılandırılmış bir WSUS sunucusu kullanamazsınız. WSUS sunucusu bir çoğaltma olarak yapılandırıldığında, Configuration Manager WSUS sunucusunu yapılandıramaz ve WSUS eşitlemesi başarısız olur. Bir birincil siteye yüklediğiniz birinci yazılım güncelleştirme noktası varsayılan yazılım güncelleştirme noktasıdır. Sitedeki diğer yazılım güncelleştirme noktaları varsayılan yazılım güncelleştirme noktasının yinelemeleri olarak yapılandırılır.  

####  <a name="decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> WSUS'i SSL kullanacak şekilde yapılandırmaya karar verme  
Yazılım güncelleştirme noktasının güvenliğini sağlamaya yardımcı olması için SSL protokolünü kullanın. WSUS istemci bilgisayarların ve akış aşağı WSUS sunucularının kimliğini WSUS sunucusunda doğrulamak için SSL kullanır. WSUS ayrıca yazılım güncelleştirme meta verilerini şifrelemek için SSL kullanır. WSUS güvenliğini SSL ile sağlamayı seçtiğinizde, yazılım güncelleştirme noktasını yüklemeden önce WSUS sunucusunu hazırlayın. Daha fazla bilgi için WSUS belgelerindeki [WSUS sunucusunda SSL 'Yi yapılandırma](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) makalesine bakın. 

Yazılım güncelleştirme noktasını yüklediğinizde ve yapılandırdığınızda, **WSUS sunucusu IÇIN SSL Iletişimini etkinleştirme**seçeneğini belirleyin. Aksi takdirde, Configuration Manager WSUS 'yi SSL kullanamayacak şekilde yapılandırır. Bir yazılım güncelleştirme noktasında SSL 'yi etkinleştirdiğinizde, alt sitelerdeki tüm yazılım güncelleştirme noktalarını da SSL kullanacak şekilde yapılandırın.  


###  <a name="configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a> Güvenlik duvarlarını yapılandırma  

Configuration Manager merkezi yönetim sitesindeki yazılım güncelleştirme noktası, yazılım güncelleştirme noktasındaki WSUS ile iletişim kurar. WSUS, yazılım güncelleştirmeleri meta verilerini eşitlemek için eşitleme kaynağıyla iletişim kurar. Bir alt sitedeki yazılım güncelleştirme noktaları, üst sitedeki yazılım güncelleştirme noktasıyla iletişim kurar. Birincil sitede birden fazla yazılım güncelleştirme noktası olduğunda, ek yazılım güncelleştirme noktaları varsayılan yazılım güncelleştirme noktasıyla iletişim kurar. Varsayılan rol, sitede yüklü olan ilk yazılım güncelleştirme noktasıdır.  

Aşağıdaki senaryolarda, WSUS tarafından kullanılan HTTP veya HTTPS trafiğine izin vermek için güvenlik duvarını yapılandırmanız gerekebilir: 
- Yazılım güncelleştirme noktası ve internet arasında
- Bir yazılım güncelleştirme noktası ve onun yukarı akış eşitleme kaynağı arasında
- Diğer yazılım güncelleştirme noktaları arasında  

Microsoft Update bağlantısı daima HTTP için bağlantı noktası 80 ve HTTPS için bağlantı noktası 443 kullanmak üzere yapılandırılır. Bir alt sitedeki yazılım güncelleştirme noktasındaki WSUS 'den, üst sitedeki yazılım güncelleştirme noktasında WSUS 'ye bağlantı için özel bir bağlantı noktası kullanın. Güvenlik ilkeniz bağlantıya izin vermezse, eşitleme ve içeri aktarma yöntemini kullanın. Daha fazla bilgi için bu makaledeki [eşitleme kaynağı](#BKMK_SyncSource) bölümüne bakın. WSUS tarafından kullanılan bağlantı noktaları hakkında daha fazla bilgi için bkz. [Configuration Manager 'DA WSUS tarafından kullanılan bağlantı noktası ayarlarını belirleme](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Belirli etki alanlarına erişimi kısıtlama  

Kuruluşunuz ağ iletişimini bir güvenlik duvarı veya ara cihaz kullanarak internet ile kısıtlarsa, etkin yazılım güncelleştirme noktasının İnternet uç noktalarına erişmesine izin vermeniz gerekir. Ardından WSUS ve otomatik güncelleştirmeler Microsoft Update bulut hizmetiyle iletişim kurabilir.

Daha fazla bilgi için bkz. [Internet erişimi gereksinimleri](../../core/plan-design/network/internet-endpoints.md#bkmk_sum).


##  <a name="plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Eşitleme ayarları planlaması  

Bu bölüm aşağıdaki alt konuları içerir:  
- [Eşitleme kaynağı](#BKMK_SyncSource)
- [Eşitleme zamanlaması](#BKMK_SyncSchedule)
- [Güncelleştirme sınıflandırmaları](#BKMK_UpdateClassifications)
- [Ürün](#BKMK_UpdateProducts)
- [Yerine geçme kuralları](#BKMK_SupersedenceRules)
- [Diller](#BKMK_UpdateLanguages)  
- [En fazla çalışma süresi](#bkmk_maxruntime)


Configuration Manager yazılım güncelleştirmeleri eşitlemesi, yapılandırdığınız ölçütlere göre yazılım güncelleştirmeleri meta verilerini indirir. Hiyerarşinizdeki üst düzey site, yazılım güncelleştirmelerini Microsoft Update eşitler. Üst düzey sitedeki yazılım güncelleştirme noktasını, Configuration Manager hiyerarşisinde değil, var olan bir WSUS sunucusuyla eşitlenmek üzere yapılandırma seçeneğiniz vardır. Alt birincil siteler, yazılım güncelleştirmeleri meta verilerini, merkezi yönetim sitesindeki yazılım güncelleştirme noktasından eşitler. Bir yazılım güncelleştirme noktası yüklemeden ve yapılandırmadan önce, eşitleme ayarlarını planlamak için bu bölümü kullanın.  


###  <a name="synchronization-source"></a><a name="BKMK_SyncSource"></a> Eşitleme kaynağı  

Yazılım güncelleştirme noktası için eşitleme kaynağı ayarları, yazılım güncelleştirme noktasının yazılım güncelleştirmeleri meta verilerini aldığı konumu belirtir. Eşitleme işleminin WSUS raporlama olayları oluşturup oluşturmadığını da belirtir.  

-   **Eşitleme kaynağı**: varsayılan olarak, üst düzey sitedeki yazılım güncelleştirme noktası Microsoft Update için eşitleme kaynağını yapılandırır. Üst düzey siteyi, var olan bir WSUS sunucusuyla eşitleme seçeneğiniz bulunmaktadır. Bir alt birincil sitedeki yazılım güncelleştirme noktası, eşitleme kaynağını merkezi yönetim sitesindeki yazılım güncelleştirme noktası olarak yapılandırır.  

    -  Bir birincil siteye yüklediğiniz varsayılan yazılım güncelleştirme noktası olan ilk yazılım güncelleştirme noktası, merkezi yönetim sitesiyle eşitlenir. Birincil sitedeki ek yazılım güncelleştirme noktaları, birincil sitedeki varsayılan yazılım güncelleştirme noktasıyla eşitlenir.  

    - Bir yazılım güncelleştirme noktasının Microsoft Update veya yukarı akış güncelleştirme sunucusu bağlantısı kesildiğinde, eşitleme kaynağını, yapılandırılmış bir eşitleme kaynağıyla eşitlenecek şekilde yapılandırın. Bunun yerine, yazılım güncelleştirmelerini eşitleyen **WSUSutil** aracının dışarı ve içeri aktarma işlevini kullanacak şekilde yapılandırın. Daha fazla bilgi için bkz. [Yazılım güncelleştirmelerini bağlantısı kesilen yazılım güncelleştirme noktasında eşitleme](../get-started/synchronize-software-updates-disconnected.md).  

-   **WSUS raporlama olayları:** İstemci bilgisayarlarındaki Windows Update Aracısı, WSUS raporlaması için olay iletileri oluşturabilir. Bu olaylar Configuration Manager tarafından kullanılmaz. Bu nedenle, **WSUS raporlama olayları oluşturma**seçeneği varsayılan olarak seçilidir. Bu olaylar oluşturulmadıysa, istemcinin WSUS sunucusuna bağlanması gereken tek zaman yazılım güncelleştirme değerlendirmesi ve uyumluluk taramaları sırasında olur. Bu olaylar Configuration Manager dışında raporlama için gerekiyorsa, bu ayarı, WSUS raporlama olayları oluşturmak üzere değiştirin.  


###  <a name="synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> Eşitleme zamanlaması  

Eşitleme zamanlamasını yalnızca Configuration Manager hiyerarşisindeki üst düzey sitede bulunan yazılım güncelleştirme noktasında yapılandırın. Eşitleme zamanlamasını yapılandırdığınızda, yazılım güncelleştirme noktası, belirttiğiniz tarih ve saatte eşitleme kaynağıyla eşitlenir. Özel zamanlama, ortamınız için optimize etmek üzere yazılım güncelleştirmelerini eşitlemenize olanak tanır. WSUS sunucusunun, site sunucusunun ve ağın performans taleplerini göz önünde bulundurun. Örneğin, haftada 2:00 ÖÖ. Alternatif olarak, Configuration Manager konsolundaki **tüm yazılım güncelleştirmeleri** veya **yazılım güncelleştirme grupları** düğümünden **eşitleme yazılım güncelleştirmeleri** eylemini kullanarak üst düzey sitede eşitlemeyi el ile başlatabilirsiniz.  

> [!TIP]  
>  Yazılım güncelleştirmeleri eşitlemesini ortamınıza uygun bir zaman kullanarak çalışacak şekilde zamanlayın. Tek bir yaygın senaryo, eşitleme zamanlamasının her ayın ikinci Salı günü Microsoft 'un normal yazılım güncelleştirme sürümünden kısa bir süre sonra çalışacak şekilde ayarlanmasıyla ilgili bir senaryodur. Bu güne genellikle *Salı düzeltme eki*olarak başvurulur. Endpoint Protection ve Windows Defender tanım ve altyapı güncelleştirmelerini sunmak için Configuration Manager kullanıyorsanız, eşitleme zamanlamasını günlük olarak çalışacak şekilde ayarlamayı göz önünde bulundurun.  

Yazılım güncelleştirme noktası başarıyla eşitlendiğinde, alt sitelere bir eşitleme isteği gönderir. Birincil sitede ek yazılım güncelleştirme noktalarınız varsa, her bir yazılım güncelleştirme noktasına bir eşitleme isteği gönderir. Bu işlem hiyerarşideki her sitede yinelenir.  


###  <a name="update-classifications"></a><a name="BKMK_UpdateClassifications"></a> Güncelleştirme sınıflandırmaları  

Her yazılım güncelleştirmesi, farklı güncelleştirme türlerinin düzenlenmesine yardımcı olan bir güncelleştirme sınıflandırmasıyla tanımlanır. Eşitleme işlemi sırasında, site belirtilen sınıflandırmalar için meta verileri eşitler. 

Configuration Manager, aşağıdaki güncelleştirme sınıflandırmalarının eşitlenmesini destekler:  

-   **Kritik güncelleştirmeler**: kritik, güvenlikle ilgili olmayan bir hatayı ele alan belirli bir sorun için yaygın olarak yayınlanan bir güncelleştirme.  

-   **Tanım güncelleştirmeleri**: virüs veya diğer tanım dosyalarına yönelik bir güncelleştirme.  

-   **Özellik paketleri**: bir ürün sürümünün dışında dağıtılan ve tipik olarak bir sonraki tam ürün sürümüne dahil edilen yeni ürün özellikleri.  

-   **Güvenlik güncelleştirmeleri**: ürüne özgü, güvenlikle ilgili bir sorun için yaygın olarak yayınlanan bir güncelleştirme.  

-   **Hizmet paketleri**: BIR işletim sistemine veya uygulamaya uygulanan toplu bir düzeltme kümesi. Bu düzeltmeler, güvenlik güncelleştirmeleri, kritik güncelleştirmeler ve yazılım güncelleştirmeleri içerir.  

-   **Araçlar**: bir veya daha fazla görevi tamamlamaya yardımcı olan bir yardımcı program veya özellik.  

-   **Güncelleştirme paketleri**: kolay dağıtım için bir arada paketlenmiş toplu bir düzeltme kümesidir. Bu düzeltmeler, güvenlik güncelleştirmeleri, kritik güncelleştirmeler ve yazılım güncelleştirmeleri içerir. Bir güncelleştirme paketi genellikle, güvenlik veya bir ürün bileşeni gibi belirli bir alana yöneliktir.  

-   **Güncelleştirmeler**: yüklü olan bir uygulama veya dosya için güncelleştirme.  

-   **Yükseltmeler**: Windows 10 ' un yeni sürümüne bir özellik güncelleştirmesi.  

Güncelleştirme sınıflandırması ayarlarını yalnızca üst düzey sitede yapılandırın. Güncelleştirme sınıflandırma ayarları, alt sitelerde yazılım güncelleştirme noktasında yapılandırılmaz, çünkü yazılım güncelleştirmeleri meta verileri en üst düzey siteden çoğaltılır. Güncelleştirme sınıflandırmalarını seçtiğinizde, ne kadar fazla sınıflandırma seçerseniz yazılım güncelleştirmeleri meta verilerinin eşitlenmesi daha uzun sürer.  

> [!WARNING]  
>  En iyi uygulama olarak, ilk kez eşitlemeden önce tüm sınıflandırmaları temizleyin. İlk eşitlemeden sonra, istenen sınıflandırmaları seçin ve ardından eşitlemeyi yeniden çalıştırın.  


###  <a name="products"></a><a name="BKMK_UpdateProducts"></a> Ürün  

Her yazılım güncelleştirmesinin meta verileri, güncelleştirmenin geçerli olduğu bir veya daha fazla ürünü tanımlar. Bir ürün, bir işletim sisteminin veya uygulamanın belirli bir sürümüdür. Bir ürün örneği Microsoft Windows 10 ' dur. Bir ürün ailesi, tek tek ürünlerin türetildiği temel işletim sistemi veya uygulamadır. Bir ürün ailesine örnek olarak, Windows 10 ve Windows Server 2016 ' in üye olduğu Microsoft Windows 'tur. Bir ürün ailesini veya bir ürün ailesi içinde bireysel ürünleri seçin.  

Yazılım güncelleştirmeleri birden fazla ürün için geçerli olduğunda ve ürünlerden en az biri eşitleme için seçildiyse, bazı ürünler seçilmese bile tüm ürünler Configuration Manager konsolunda görünür. Örneğin, yalnızca Windows Server 2012 ürününü seçersiniz. Bir yazılım güncelleştirmesi Windows Server 2012 ve Windows Server 2012 Datacenter Edition için geçerliyse, her iki ürün de site veritabanında bulunur.  

Ürün ayarlarını yalnızca üst düzey sitede yapılandırın. Ürün ayarları, alt siteler için yazılım güncelleştirme noktasında yapılandırılmaz, çünkü yazılım güncelleştirmeleri meta verileri en üst düzey siteden çoğaltılır. Ne kadar çok ürün seçerseniz, yazılım güncelleştirmeleri meta verilerinin eşitlenmesi de o kadar uzun sürer.  

> [!IMPORTANT]  
>  Configuration Manager, yazılım güncelleştirme noktasını ilk kez yüklerken seçtiğiniz ürünlerin ve ürün ailelerinin listesini depolar. Configuration Manager yayımlandıktan sonra yayınlanan ürünler ve ürün aileleri, eşitleme tamamlanana kadar seçme seçeneği sunulmayabilir. Eşitleme işlemi, aralarından seçim yapabileceğiniz kullanılabilir ürünlerin ve ürün ailelerinin listesini güncelleştirir. Yazılım güncelleştirmelerini ilk defa eşitlemeden önce tüm ürünleri temizleyin. İlk eşitlemeden sonra, istediğiniz ürünleri seçin ve ardından eşitlemeyi yeniden çalıştırın.  


###  <a name="supersedence-rules"></a><a name="BKMK_SupersedenceRules"></a> Yenisiyle değiştirme kuralları  

Genellikle, başka bir yazılım güncelleştirmesinin yerine geçen bir yazılım güncelleştirmesi aşağıdaki eylemlerin bir veya daha fazlasını yapar:  

-   Önceden sunulan bir veya daha fazla güncelleştirmenin sağladığı düzeltmeyi geliştirir, iyileştirir veya güncelleştirir.  

-   Güncelleştirme yüklenmek üzere onaylanırsa istemcilere yüklenen yenisiyle değiştirilen güncelleştirme dosya paketinin verimliliğini artırır. Örneğin, yenisiyle değiştirilen güncelleştirme, artık düzeltmeyle veya yeni güncelleştirme tarafından desteklenen işletim sistemleriyle ilgili olmayan dosyalar içerebilir. Bu dosyalar, güncelleştirmenin yerine geçen dosya paketine dahil değildir.  

-   Bir ürünün daha yeni sürümlerini güncelleştirir. Başka bir deyişle, bir ürünün daha eski sürümleri veya yapılandırmaları için artık uygun olmayan sürümleri güncelleştirir. Güncelleştirmeler ayrıca, dil desteğini genişletmek değişiklikler yapılmışsa başka güncelleştirmelerin de yerini alabilir. Örneğin, Microsoft 365 uygulamalar için bir ürün güncelleştirmesinin daha sonraki bir düzeltmesi, daha eski bir işletim sistemi için desteği kaldırabilir, ancak ilk güncelleştirme sürümünde yeni diller için ek destek ekleyebilir.  

Yazılım güncelleştirme noktasının özelliklerinde, yenisiyle değiştirilen yazılım güncelleştirmelerinin hemen dolduğunu belirtin. Bu ayar, yeni dağıtımlara eklenmesini engeller. Ayrıca, bir veya daha fazla zaman aşımına uğradı yazılım güncelleştirmeleri içerdiğini göstermek için mevcut dağıtımları işaretler. Veya yenisiyle değiştirilen yazılım güncelleştirmelerinin süresi dolmadan önce bir süre belirtin. Bu eylem, bunları dağıtmaya devam etmenize olanak tanır. 

Önceki bir yazılım güncelleştirmesini dağıtmanız gerekebilecek aşağıdaki senaryoları dikkate alın:  

-   Yerine geçen bir yazılım güncelleştirmesi bir işletim sisteminin yalnızca yeni sürümlerini destekler. İstemci bilgisayarlarınızın bazıları işletim sisteminin önceki sürümlerini çalıştırır.  

-   Yerine geçen bir yazılım güncelleştirmesinin, yerini aldığı yazılım güncelleştirmesinden daha fazla kısıtlı uygulanabilirliği vardır. Bu davranış, bazı istemciler için uygunsuz hale gelir.  

-   Yerine geçen bir yazılım güncelleştirmesi üretim ortamınızda dağıtım için onaylanmamışsa.  

    > [!NOTE]  
    > - Configuration Manager sürüm 1806 ' den önce, Configuration Manager yenisiyle değiştirilen bir yazılım güncelleştirmesini **zaman aşımına ermişse**, güncelleştirmeyi WSUS 'de **reddedildi** olarak ayarlamamıştır. İstemciler, güncelleştirme el ile veya özel bir komut dosyası aracılığıyla reddedilene kadar, süre dolma bir güncelleştirmeyi taramaya devam eder.  Configuration Manager sürüm 1806 ' den sonra, Configuration Manager WSUS 'teki yenisiyle değiştirilen güncelleştirmeleri de reddeder. WSUS temizleme görevi hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri Bakımı](../deploy-use/software-updates-maintenance.md).
    > - Configuration Manager sürüm 1810 ' den başlayarak, özellik **güncelleştirmeleri** için değiştirme kuralları davranışını **Özellik dışı güncelleştirmelerden**ayrı olarak belirtebilirsiniz.

###  <a name="languages"></a><a name="BKMK_UpdateLanguages"></a> Diller  

Yazılım güncelleştirme noktasının dil ayarları şunları yapılandırmanıza izin verir: 
- Özet ayrıntılarının (yazılım güncelleştirmeleri meta verileri) yazılım güncelleştirmeleri için eşitlendiği diller  
- Yazılım güncelleştirmeleri için indirilen yazılım güncelleştirme dosyası dilleri  

#### <a name="software-update-file"></a>Yazılım güncelleştirme dosyası  
Yazılım güncelleştirme noktasının özelliklerinde **yazılım güncelleştirme dosyası** ayarı için dilleri yapılandırın. Bu ayar, bir sitede yazılım güncelleştirmeleri indirdiğinizde kullanılabilecek varsayılan dilleri sağlar. Yazılım güncelleştirmelerinin indirildiği veya dağıtıldığı her seferinde varsayılan olarak seçilen dilleri değiştirin. İndirme işlemi sırasında, yapılandırılan dillere ait yazılım güncelleştirme dosyaları, seçili dilde yazılım güncelleştirme dosyaları varsa dağıtım paketi kaynak konumuna indirilir. Ardından, site sunucusundaki içerik kitaplığına kopyalanırlar. Ardından, paket için yapılandırılan dağıtım noktalarına dağıtılır.  

Yazılım güncelleştirme dosyası dil ayarlarını ortamınızda en sık kullanılan dillerle yapılandırın. Örneğin, sitenizdeki istemciler, Windows veya uygulamalar için çoğunlukla Ingilizce ve Japonca kullanır. Sitede kullanılan diğer birkaç dil vardır. Yazılım güncelleştirmesini indirdiğinizde veya dağıtırken **yazılım güncelleştirme dosyası** sütununda yalnızca Ingilizce ve Japonca ' yı seçin. Bu eylem, dağıtım ve indirme sihirbazlarının **Dil seçimi** sayfasında varsayılan ayarları kullanmanıza olanak sağlar. Bu eylem, gereksiz güncelleştirme dosyalarının indirilmesini de önler. Configuration Manager hiyerarşisindeki her bir yazılım güncelleştirme noktasında bu ayarı yapılandırın.  



#### <a name="summary-details"></a>Özet ayrıntılar  
Eşitleme işlemi sırasında, özet ayrıntı bilgileri (yazılım güncelleştirmeleri meta verileri) yalnızca belirttiğiniz dillerdeki yazılım güncelleştirmeleri için güncelleştirilir. Meta veriler yazılım güncelleştirmesiyle ilgili bilgiler sağlar, örneğin:
- Ad
- Açıklama
- Güncelleştirmenin desteklediği ürünler
- Güncelleştirme sınıflandırması
- Makale KIMLIĞI
- URL 'YI indir
- Uygulanabilirlik kuralları

Özet Ayrıntılar ayarlarını yalnızca üst düzey sitede yapılandırın. Yazılım güncelleştirmeleri meta verileri, dosya tabanlı çoğaltma kullanılarak merkezi yönetim sitesinden çoğaltıldığından, özet ayrıntıları alt sitelerdeki yazılım güncelleştirme noktasında yapılandırılmaz. Özet ayrıntıları dillerini seçerken, yalnızca ortamınızda gereksinim duyduğunuz dilleri seçin. Ne kadar çok dil seçerseniz, yazılım güncelleştirmeleri üst verilerini eşitlemeniz o kadar uzun sürer. Configuration Manager, yazılım güncelleştirmeleri meta verilerini, Configuration Manager konsolunun çalıştığı işletim sisteminin yerel ayarında görüntüler. Yazılım güncelleştirmelerinin yerelleştirilmiş özellikleri bu işletim sisteminin yerel ayarında yoksa, yazılım güncelleştirme bilgileri Ingilizce görüntülenir.  

> [!IMPORTANT]  
>  İhtiyaç duyduğunuz tüm Özet ayrıntı dillerini seçin. Üst düzey sitedeki yazılım güncelleştirme noktası eşitleme kaynağıyla eşitlendiğinde, seçili özet ayrıntıları dilleri aldığı yazılım güncelleştirmeleri meta verilerini belirlenir. Eşitleme en az bir kez çalıştıktan sonra Özet ayrıntıları dillerini değiştirirseniz, yalnızca yeni veya güncelleştirilmiş yazılım güncelleştirmeleri için değiştirilen Özet ayrıntı dillerinin yazılım güncelleştirme meta verilerini alır. Eşitleme kaynağındaki yazılım güncelleştirmesinde değişiklik olmadığı takdirde, zaten eşitlenmiş olan yazılım güncelleştirmeleri değiştirilen diller için yeni meta verilerle güncellenmez.


###  <a name="maximum-run-time"></a><a name="bkmk_maxruntime"></a> En fazla çalışma süresi
<!--3734426-->
*(Sürüm 1906 ' de tanıtılmıştır)*

Sürüm 1906 ' den başlayarak, bir yazılım güncelleştirmesi yüklemesinin tamamlaması için en uzun süreyi belirtebilirsiniz. Aşağıdakiler için en fazla çalışma süresini belirtebilirsiniz:

- **Windows özellik güncelleştirmeleri için maksimum çalışma süresi (dakika)**
  - **Özellik güncelleştirmeleri** -bu üç sınıflandırmadaki bir güncelleştirme:
    - Güncelleştirmelerini
    - Güncelleştirme paketleri
    - Hizmet paketleri

- **Windows için Office 365 güncelleştirmeleri ve Özellik dışı güncelleştirmeleri için maksimum çalışma süresi (dakika)**
  - **Özellik dışı güncelleştirmeler** -Özellik yükseltmesi olmayan ve ürünü aşağıdakilerden biri olarak listelenen bir güncelleştirmedir:
    - Windows 10 (tüm sürümler)
    - Windows Server 2012
    - Windows Server 2012 R2
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- Bu ayarlar yalnızca Microsoft Update eşitlenen yeni güncelleştirmeler için maksimum çalışma zamanını değiştirir. Mevcut özellik veya özellik dışı güncelleştirmelerde çalışma zamanını değiştirmez.
- Diğer tüm ürünler ve sınıflandırmalar bu ayarla yapılandırılamaz. Bu güncelleştirmelerden birinin en fazla çalışma süresini değiştirmeniz gerekiyorsa, [yazılım güncelleştirme ayarlarını yapılandırın](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings)

> [!NOTE]
> Sürüm 1906 ' de, en üst düzey yazılım güncelleştirme noktasını yüklediğinizde maksimum çalışma zamanı kullanılamaz. Yükleme sonrasında, en üst düzey yazılım güncelleştirme noktanağınızın çalışma süresini en fazla düzenleyin.

##  <a name="plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a> Yazılım güncelleştirmeleri bakım penceresi için plan  

Yazılım güncelleştirmeleri yüklemesi için ayrılmış bir bakım penceresi ekleyin. Bu eylem, bir genel bakım penceresi ve yazılım güncelleştirmeleri için farklı bir bakım penceresi yapılandırmanıza olanak tanır. Bir genel bakım penceresi ve yazılım güncelleştirmeleri bakım penceresi yapılandırdığınızda, istemciler yalnızca yazılım güncelleştirmeleri bakım penceresi sırasında yazılım güncelleştirmelerini yükler. 

Configuration Manager sürüm 1810 ' den başlayarak, bu davranışı değiştirebilir ve genel bakım penceresi sırasında yazılım güncelleştirmelerinin yüklenmesine izin verebilirsiniz. Bu istemci ayarı hakkında daha fazla bilgi için bkz. [yazılım güncelleştirmeleri istemci ayarları](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint).

Bakım pencereleri hakkında daha fazla bilgi için bkz. [bakım pencerelerini kullanma](../../core/clients/manage/collections/use-maintenance-windows.md).  


##  <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Windows 10 istemcileri için yazılım güncelleştirme yüklemesinden sonra yeniden başlatma seçenekleri

Yeniden başlatma gerektiren bir yazılım güncelleştirmesi dağıtıldığında ve Configuration Manager kullanılarak yüklendiğinde, istemci bekleyen bir yeniden başlatmayı zamanlar ve yeniden başlatma iletişim kutusu görüntüler.

Configuration Manager yazılım güncelleştirmesi için bekleyen bir yeniden başlatma işlemi olduğunda, **güncelleştirme ve yeniden başlatma** ve **güncelleştirme ve kapatma** seçeneği Windows 10 bilgisayarlarda Windows güç seçenekleri 'nde kullanılabilir. Bu seçeneklerden birini kullandıktan sonra, bilgisayar yeniden başlatıldıktan sonra yeniden başlatma iletişim kutusu görüntülenmez. Bazı durumlarda, işletim sistemi bekleyen yeniden başlatma seçeneklerini kaldırabilir. Windows 10 ' da hızlı başlangıç özelliği etkinse bu durum oluşabilir. Daha fazla bilgi için bkz. [güncelleştirmeler Windows 10 ' da hızlı başlangıç ile yüklenemeyebilir](https://support.microsoft.com/help/4011287/windows-updates-not-install-with-fast-startup).

## <a name="evaluate-software-updates-after-a-servicing-stack-update"></a><a name="bkmk_ssu"></a> Bakım yığını güncelleştirmesinden sonra yazılım güncelleştirmelerini değerlendir
<!--4639943-->
Sürüm 2002 ' den başlayarak Configuration Manager, bir hizmet yığını güncelleştirmesinin (SSU) birden çok güncelleştirme için bir yüklemenin parçası olup olmadığını algılar. Bir SSU algılandığında, önce yüklenir. SSU 'yı yükledikten sonra, kalan güncelleştirmeleri yüklemek için bir yazılım güncelleştirme değerlendirme çevrimi çalışır. Bu değişiklik, bakım yığını güncelleştirmesinden sonra bağımlı bir toplu güncelleştirmenin yüklenmesine izin verir. Cihazın yüklemeler arasında yeniden başlatılması gerekmez ve ek bir bakım penceresi oluşturmanız gerekmez. SSUs öncelikle yalnızca Kullanıcı tarafından başlatılan yüklemeler için yüklenir. Örneğin, bir kullanıcı yazılım merkezinden birden çok güncelleştirme için bir yükleme başlatırsa, önce SSU yüklenmemiş olabilir. Configuration Manager sürüm 2002 kullanılırken Windows Server işletim sistemleri için önce SSUs yüklemesi kullanılamaz. <!--7813007-->Bu işlevsellik, Windows Server işletim sistemleri için Configuration Manager sürüm 2006 ' ye eklenmiştir.



## <a name="next-steps"></a>Sonraki adımlar
Yazılım güncelleştirmelerini planlarken, bkz. [yazılım güncelleştirme yönetimi Için hazırlanma](../get-started/prepare-for-software-updates-management.md).  

Windows 'u hizmet olarak yönetme hakkında daha fazla bilgi için bkz. hizmet olarak [Configuration Manager Temelleri ve hizmet olarak Windows](../../core/understand/configuration-manager-and-windows-as-service.md).