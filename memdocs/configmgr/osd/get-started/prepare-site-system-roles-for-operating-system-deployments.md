---
title: Site sistemi rollerini OSD için hazırlama
titleSuffix: Configuration Manager
description: Configuration Manager ' de işletim sistemlerini dağıtmadan önce site sistem rollerini yapılandırın
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1beec2f5ef7b6da9f1f093300ec6c2b239e7396e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724058"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Configuration Manager ile IŞLETIM sistemi dağıtımları için site sistemi rolleri hazırlama

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Configuration Manager işletim sistemlerini dağıtmak için, önce belirli yapılandırmalara ve noktalara gerek gerektiren aşağıdaki site sistem rollerini hazırlayın.



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a> Dağıtım noktaları  

Dağıtım noktası site sistemi rolü, istemcilerin indirme kaynak dosyalarını barındırır. Bu içerik uygulamalar, yazılım güncelleştirmeleri, işletim sistemi görüntüleri, önyükleme görüntüleri ve sürücü paketleri içindir. Bant genişliği, azaltma ve zamanlama seçeneklerini kullanarak içerik dağıtımını denetleyin.  

İşletim sistemlerinin bilgisayarlara dağıtımını desteklemek için yeterli dağıtım noktanız olması önemlidir. Bu dağıtım noktalarının hiyerarşinize yerleştirmesini planlamanız de önemlidir. Daha fazla bilgi için bkz. [içeriği ve içerik altyapısını yönetme](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). Bu makale, işletim sistemi dağıtımına özel dağıtım noktaları için bazı ek planlama konuları içerir.  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a>Dağıtım noktaları için ek planlama konuları  

Aşağıdaki öğeler dağıtım noktaları için göz önünde bulundurmanız gereken ek planlardır:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>İstenmeyen işletim sistemi dağıtımlarını nasıl önleyebilirim?  
Configuration Manager, site sunucularını bir koleksiyondaki diğer hedef bilgisayarlardan ayırt etmez. Gerekli bir görev dizisini site sunucusu içeren bir koleksiyona dağıtırsanız, görev dizisini koleksiyondaki diğer bilgisayarla aynı şekilde çalıştırır. İşletim sistemi dağıtımınızın amaçlanan istemcileri içeren bir koleksiyon kullandığından emin olun.  

Yüksek riskli görev dizisi dağıtımları için davranışı yönetin. Yüksek riskli dağıtım, bir istemcide otomatik olarak yüklenir ve istenmeyen sonuçlara neden olabilir. Örneğin, bir işletim sistemini dağıtan, amacı gerekli olan bir görev dizisi. İstenmeyen yüksek riskli dağıtım riskini azaltmak için dağıtım doğrulama ayarlarını yapılandırın. Daha fazla bilgi için bkz. [yüksek riskli dağıtımları yönetme ayarları](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Tek bir dağıtım noktasından aynı anda kaç bilgisayar bir işletim sistemi görüntüsü alabilir?  
Kaç dağıtım noktasına ihtiyacınız olduğunu tahmin etmek için aşağıdaki değişkenleri göz önünde bulundurun:  
- Dağıtım noktasının işleme hızı
- Dağıtım noktasının disk hızı
- Ağ üzerindeki kullanılabilir bant genişliği
- Görüntü paketinin boyutu   
  
Örneğin, diğer sunucu kaynak faktörleri göz önünde bulundurmazsanız, 100 GB 'lık bir görüntü paketini 100 megabitlik/sn Ethernet ağında bir saat içinde işleyebileceğiniz en fazla bilgisayar sayısı 11 bilgisayarındadır.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Belirli bir zaman çerçevesinde belirli sayıda bilgisayara bir işletim sistemi dağıtmanız gerekiyorsa görüntüyü uygun sayıda dağıtım noktasına dağıtın.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Bir dağıtım noktasına işletim sistemi dağıtabilir miyim?  
Bir dağıtım noktasına işletim sistemi dağıtabilirsiniz, ancak işletim sistemi görüntüsünün farklı bir dağıtım noktasından alınması gerekir.  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a>PXE isteklerini kabul etmek için dağıtım noktalarını yapılandırma  

PXE önyükleme istekleri yapan istemcileri Configuration Manager işletim sistemlerini dağıtmak için, PXE isteklerini kabul etmek üzere bir veya daha fazla dağıtım noktası yapılandırın. Dağıtım noktasını yapılandırdıktan sonra, PXE önyükleme isteklerine yanıt verir ve yapılacak uygun dağıtım eylemini belirler. Daha fazla bilgi için, bkz. [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a>PXE 'yi destekleyen dağıtım noktalarında RamDisk TFTP bloğunu ve pencere boyutlarını özelleştirin  

PXE 'yi destekleyen dağıtım noktaları için RamDisk TFTP bloğunu ve pencere boyutlarını özelleştirebilirsiniz. Ağınızı özelleştirdiyseniz, büyük bir blok veya pencere boyutu, önyükleme görüntüsü indirmenin zaman aşımı hatası vererek başarısız olmasına neden olabilir. RamDisk TFTP blok ve pencere boyutu özelleştirmeleri, PXE kullanırken belirli ağ gereksinimlerinizi karşılayacak şekilde TFTP trafiğini iyileştirmenize olanak tanır. Yapılandırmanın en verimli olduğunu belirlemek için, özelleştirilmiş ayarları ortamınızda test edin.  

-   **TFTP blok boyutu**: blok boyutu, sunucunun dosyayı karşıdan yükleyen istemciye gönderdiği veri paketlerinin boyutudur. Daha büyük bir blok boyutu, sunucunun daha az paket göndermesine olanak tanıyarak sunucu ve istemci arasındaki gidiş dönüş gecikmelerini azaltır. Ancak, büyük bir blok boyutu, çoğu PXE istemci uygulaması tarafından desteklenmeyen parçalanmış paketlere yol açar.  

-   **TFTP pencere boyutu**: TFTP, gönderilen her veri bloğu için bir onay (ACK) paketi gerektirir. Sunucu, önceki blok için ACK paketini alıncaya kadar sırada sonraki bloğu göndermez. TFTP Pencereleme, bir pencereyi doldurması için kaç veri bloğu olduğunu tanımlamanızı sağlar. Sunucu, pencere doldurulana kadar veri bloklarını arka arkaya gönderir ve sonra istemci bir ACK paketi gönderir. Bu pencere boyutunu artırırsanız, istemci ve sunucu arasındaki gidiş dönüş gecikmelerinin sayısını azaltır ve bir önyükleme görüntüsünü indirmek için gereken toplam süreyi düşürür.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>RamDisk TFTP pencere boyutunu değiştirme  
RamDisk TFTP pencere boyutunu özelleştirmek için, PXE 'yi destekleyen dağıtım noktalarına aşağıdaki kayıt defteri anahtarını ekleyin:  

- **Konum**:`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Ad**: RamDiskTFTPWindowSize  
- **Tür**: REG_DWORD  
- **Değer**: (özelleştirilmiş pencere boyutu)  
    - Varsayılan değer **1** ' dir (bir veri bloğu pencereyi doldurur).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>RamDisk TFTP blok boyutunu değiştirme  
RamDisk TFTP pencere boyutunu özelleştirmek için, PXE 'yi destekleyen dağıtım noktalarına aşağıdaki kayıt defteri anahtarını ekleyin:  

- **Konum**:`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Ad**: RamDiskTFTPBlockSize  
- **Tür**: REG_DWORD  
- **Değer**: (özelleştirilmiş blok boyutu)  
    - Varsayılan değer **4096**' dir.  

> [!Note]  
> Hem Windows Dağıtım Hizmetleri hem de Configuration Manager PXE Yanıtlayıcı hizmeti bu TFTP yapılandırmasını destekler.  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a>Dağıtım noktalarını çok noktaya yayını destekleyecek şekilde yapılandırma  

Çok noktaya yayın, bir ağ iyileştirme yöntemidir. Birden çok istemci aynı anda aynı işletim sistemi görüntüsünü indirileceği zaman dağıtım noktalarında kullanın. Çok noktaya yayın kullandığınızda, birden çok bilgisayar, işletim sistemi görüntüsünü dağıtım noktası tarafından çok noktaya yayın olarak aynı anda indirebilir. Çok noktaya yayın olmadan dağıtım noktası, verilerin bir kopyasını ayrı bir bağlantı üzerinden her bir istemciye gönderir. Daha fazla bilgi için bkz. [Windows 'u ağ üzerinden dağıtmak için çok noktaya yayın kullanma](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

İşletim sistemini dağıtmadan önce, çok noktaya yayını destekleyecek şekilde bir dağıtım noktası yapılandırın. Daha fazla bilgi için bkz. [dağıtım noktalarını yükleyip yapılandırma](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> Durum geçiş noktası  

Durum geçiş noktası, USMT 'nin bir bilgisayar üzerinde yakaladığı Kullanıcı durumu verilerini depolar ve sonra başka bir bilgisayara geri yükler. Ancak, hedef bilgisayardaki Windows 'u yenilediğiniz bir dağıtım gibi aynı bilgisayarda bir işletim sistemi dağıtımı için Kullanıcı ayarlarını yakaladığınızda, sabit bağlantılar kullanarak verileri aynı bilgisayara depolamayı veya bir durum geçiş noktası kullanmayı seçebilirsiniz. Bazı bilgisayar dağıtımları için, durum deposunu oluşturduğunuzda, Configuration Manager otomatik olarak durum deposu ve hedef bilgisayar arasında bir ilişki oluşturur. Durum geçiş noktası için plan yaparken aşağıdaki faktörleri göz önünde bulundurun:    


### <a name="user-state-size"></a>Kullanıcı durumu boyutu  

Kullanıcı durumunun boyutu, durum yükseltme noktasındaki disk depolamasını ve yükseltme sırasındaki ağ performansını doğrudan etkiler. Kullanıcı durumunun boyutunu ve yükseltilecek bilgisayar sayısını göz önünde bulundurun. Ayrıca, bilgisayardan hangi ayarların geçirildiğini de göz önünde bulundurun. Örneğin **, Belgelerim klasörü zaten** bir sunucuya yedekleniyorsa, büyük olasılıkla bunu görüntü dağıtımının bir parçası olarak geçirmeniz gerekmez. Gereksiz geçişlere karşı, Kullanıcı durumunun genel boyutunu küçültün ve durum geçiş noktasındaki ağ performansı ve disk depolaması üzerinde sahip olacağı etkiyi azaltır.  


### <a name="user-state-migration-tool"></a>Kullanıcı Durumu Geçirme Aracı  

İşletim sistemlerinin dağıtımı sırasında Kullanıcı durumunu yakalamak ve geri yüklemek için, USMT kaynak dosyalarını işaret eden bir Kullanıcı Durumu Taşıma Aracı (USMT) paketini kullanın. Configuration Manager, bu paketi **yazılım kitaplığı** > **uygulama yönetimi** > **paketlerindeki**Configuration Manager konsolunda otomatik olarak oluşturur. Configuration Manager, Kullanıcı durumunu bir işletim sisteminden yakalamak ve sonra başka bir işletim sistemine geri yüklemek için USMT 10 ' u kullanır. Windows 10 için Windows değerlendirme ve Dağıtım Seti (Windows ADK), USMT 10 içerir.

USMT 10 için farklı geçiş senaryolarının açıklaması için, bkz. Windows belgelerindeki [genel geçiş senaryoları](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios) .  


### <a name="retention-policy"></a>Retention ilkesi  

Durum geçiş noktasını yapılandırırken, depoladığı Kullanıcı durumu verilerinin saklanacağı sürenin uzunluğunu belirtin. Verilerin durum yükseltme noktasında tutulma süresi iki duruma bağlıdır:  

-   Depolanan verilerin disk depolama üzerindeki etkisi.  

-   Verileri tekrar geçirmeniz gerektiğinde bu verileri bir süre bekletme gereksinimi.  
  
  
Durum geçişi iki aşamada gerçekleşir: verilerin yakalanması ve verilerin geri yüklenmesi. Verileri yakaladığınızda, kullanıcı durum verileri toplanır ve durum yükseltme noktasına kaydedilir. Verileri geri yüklediğinizde, kullanıcı durum verileri durum yükseltme noktasından alınıp hedef bilgisayara yazılır, sonra **Durum Depolama Alanını Serbest Bırak** görev dizisi adımı, depolanan verileri yayımlar. Veriler yayımlandığında bekletme süreölçeri başlatılır. Geçirilen verileri hemen silme seçeneğini belirlerseniz, Kullanıcı durumu verileri serbest bırakılır almaz silinir. Verileri belirli bir süre saklamak isterseniz veriler, yayımlanmalarının ardından belirttiğiniz süre geçtikten sonra silinir. Saklama süresini daha uzun süre ayarlamış olursunuz, muhtemelen daha fazla disk alanı gerekir.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Kullanıcı durumu geçiş verilerini depolamak için sürücüyü seçin  

Durum geçiş noktasını yapılandırdığınızda, Kullanıcı durumu taşıma verilerini depolamak için sunucuda sürücüyü belirtin. Sürücüler listesinden bir sürücü seçin. Ancak, bu sürücülerden bazıları CD sürücüsü veya ağ paylaşımsız sürücüler gibi yazılmayan sürücüleri temsil edebilir. Bazı sürücü harfleri bilgisayardaki herhangi bir sürücüyle eşlenmemiş olabilir. Durum geçiş noktasını yapılandırırken yazılabilir, paylaşılan bir sürücü belirtin.  


### <a name="configure-a-state-migration-point"></a>Bir durum geçiş noktası yapılandırın  

Bir durum geçiş noktasını Kullanıcı durumu verilerini depolamak üzere yapılandırmak için aşağıdaki yöntemleri kullanın:  

-   Durum geçiş noktası için yeni bir site sistemi sunucusu oluşturmak için **Site Sistemi Sunucusu Oluşturma Sihirbazı** 'nı kullanın.  

-   Var olan bir sunucuya durum geçiş noktası eklemek için **Site Sistemi Rolleri Ekleme Sihirbazı** 'nı kullanın.  

Bu sihirbazları kullandığınızda, durum geçiş noktası için aşağıdaki bilgileri sağlamanız istenir:  

-   Kullanıcı durumu verilerinin depolanacağı klasörler.  

-   Durum geçiş noktasında veri depolayabilen maksimum istemci sayısı.  

-   Durum geçiş noktasının kullanıcı durumu verilerini depolaması için minimum boş alan.  

-   Role ilişkin silme ilkesi. Kullanıcı durumu verilerinin bir bilgisayara geri yüklendikten hemen sonra silineceğini ya da bir bilgisayara Kullanıcı verileri geri yüklendikten sonra belirli bir gün sayısından sonra silineceğini belirtin.  

-   Durum geçiş noktasının yalnızca kullanıcı durumu verilerini geri yükleme isteklerine yanıt verip vermeyeceği. Bu seçeneği etkinleştirdiğinizde, durum geçiş noktasını Kullanıcı durumu verilerini depolamak için kullanamazsınız.  

Site sistemi rolü yüklemek için gereken adımlar için bkz. [site sistemi rolleri ekleme](../../core/servers/deploy/configure/add-site-system-roles.md).  
