---
title: Destek Merkezi kullanıcı arabirimi başvurusu
titleSuffix: Configuration Manager
description: Destek Merkezi araçlarını kullanmayı öğrenin.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43bb35243b4f7e7b1e45b66319efd4ec21e92542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718619"
---
# <a name="support-center-user-interface-reference"></a>Destek Merkezi kullanıcı arabirimi başvurusu

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Bu makale, Destek Merkezi araçlarının kullanıcı arabirimlerini (UI) açıklayan bir başvurudur:
- Destek Merkezi
- Destek Merkezi günlük Görüntüleyici
- Destek Merkezi Görüntüleyicisi



## <a name="support-center-reference"></a>Destek Merkezi başvurusu

Bu bölümde, **Destek Merkezi** aracı için Kullanıcı arabirimi açıklanmaktadır. 
- [Pencere menüsü](#bkmk_support-window)  
- [Ana Sayfa sekmesi](#bkmk_support-home)  
- [İstemci sekmesi](#bkmk_support-client)  
- [İlke sekmesi](#bkmk_support-policy)  
- [İçerik sekmesi](#bkmk_support-content)  
- [Envanter sekmesi](#bkmk_support-inventory)  
- [Sorun giderme sekmesi](#bkmk_support-troubleshoot)  
- [Günlükler sekmesi](#bkmk_support-logs)  


### <a name="window-menu"></a><a name="bkmk_support-window"></a>Pencere menüsü

Destek Merkezi penceresinin sol üst köşesinde, mavi kutudaki oku seçerek bu menüyü açın.

#### <a name="local-machine-connection"></a>Yerel makine bağlantısı
Destek Merkezi günlük dosyalarını toplar ve Destek Merkezi 'ni çalıştıran istemcide sorun giderme gerçekleştirir.

#### <a name="remote-connection"></a>Uzak bağlantı
Başka bir Configuration Manager istemcisiyle uzak bağlantı kurun. Bağlandıktan sonra, Destek Merkezi günlük dosyalarını toplar ve bağlı olduğu istemcide sorun giderme gerçekleştirir.

#### <a name="about"></a>Hakkında
Destek Merkezi hakkında bilgi sağlar.

#### <a name="options"></a>Seçenekler
**Seçenekler** iletişim kutusunda şunları yapabilirsiniz:
- Animasyonlu Kullanıcı arabirimi öğelerinin hareketini azaltma  
- Veri paketi dosyaları için varsayılan kaydetme konumunu değiştirme  
- Geçici dosyaların konumunu değiştirme    
- Uyarıları sıfırlayın. Daha önce gizlenen tüm uyarı iletileri tetiklendiğinde yeniden görüntülenir.  
- Geçici dosya yolunu varsayılana sıfırlayın,`%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Çık
Destek merkezini kapatın.



### <a name="home-tab"></a><a name="bkmk_support-home"></a>Giriş sekmesi

#### <a name="collect-selected-data"></a>Seçili verileri topla
Destek Merkezi Configuration Manager istemcisinden bilgi toplar. Varsayılan olarak, aşağıdaki türleri toplar:
- Günlük dosyaları
- İstemci yapılandırma toplayıcısı
- İşletim sistemi

Diğer bilgi türlerini toplamak için, bu türün adının yanındaki onay kutusunu seçin.

Şeritteki **seçili verileri topla** düğmesinin altındaki açılan seçimi seçin ve **tüm verileri topla**' yı seçin. Bu eylem, tüm istemci durumu verileri kümesini toplar.

Destek Merkezi veri toplarken, durdurmak için **koleksiyonu Iptal et** ' i seçin.

#### <a name="data-types"></a>Veri türleri
Bir seçeneğe ait onay kutusunu seçtiğinizde, Destek Merkezi **seçili verileri**bir sonraki seçişinizde bu veri türünü toplar. Aşağıdaki türler kullanılabilir:  

- **Günlük dosyaları**: Kurulum günlükleri dahil istemci günlük dosyaları  

- **İlke**: istemci ilkesi koleksiyonu  

- **Sertifikalar**: istemci sertifikaları için ortak anahtar bilgileri. Destek Merkezi, sertifika özel anahtarlarını toplamaz.  

- **İstemci yapılandırma toplayıcısı**: istemci bilgilerini Configuration Manager. Bu veri türünü devre dışı bırakamıyorum.  

- **İstemci kayıt defteri**: kayıt defterinden istemci yapılandırma bilgilerini toplar. Destek Merkezi yalnızca Configuration Manager kayıt defteri bilgilerini toplar.  

- **ISTEMCI WMI**: WMI 'dan istemci yapılandırma bilgileri. Destek Merkezi istemci ilkesi toplanmaz.  

- **Sorun giderme**: Active Directory, yönetim noktaları, ağ, ilke atamaları ve kayıt ile yaygın istemci sorunlarını tanılamaya yardımcı olmak için gerçek zamanlı sorun giderme verileri.  

    > [!NOTE]  
    > Bu veri türü, başka bir istemciye uzak bağlantı yaptığınızda desteklenmez.  

- **Hata ayıklama dökümleri**: istemcinin ve ilgili işlemlerin hata ayıklama dökümünü yapın. Hata ayıklama dökümleri büyük olabilir. Bu seçeneği yalnızca istemci performansıyla ilgili sorunları giderirken etkinleştirin.  

    > [!WARNING]  
    > Hata ayıklama dökümlerinin toplanması veri paketlerinin çok büyük olmasına neden olur (bazı durumlarda, birkaç yüz MB).  
    >  
    > Hata ayıklama dökümlerinde parolalar, şifreleme gizli dizileri veya Kullanıcı verileri gibi hassas bilgiler bulunabilir. Hata ayıklama dökümlerinin yalnızca Microsoft Desteği personeli önerisine toplanması gerekir. Hata ayıklama dökümlerini içeren veri paketleri, yetkisiz erişimlerden korunmak için dikkatle işlenmelidir.  
    >  
    > Bu veri türü, başka bir istemciye uzak bağlantı yaptığınızda desteklenmez.  

- **İşletim sistemi**: yerel makineyle ilgili yapılandırma bilgilerini toplar. Bu veriler, Windows yüklemesi, ağ bağdaştırıcıları ve sistem hizmeti yapılandırması hakkında bilgiler içerir. Bu veri türünü devre dışı bırakamıyorum.  



### <a name="client-tab"></a><a name="bkmk_support-client"></a>İstemci sekmesi

#### <a name="load-or-refresh"></a>Yükleme veya yenileme
Destek Merkezi Configuration Manager istemcisinin ayrıntılarını yükler veya yeniler.

#### <a name="control-client-agent-service"></a>İstemci Aracısı hizmetini denetleme
Bağlı istemcideki Configuration Manager istemci Aracısı hizmeti (Ccmexec) üzerinde aşağıdaki eylemlerden birini gerçekleştirin:  

- **İstemciyi yeniden Başlat**  

    > [!IMPORTANT]  
    > İstemci Aracısı hizmeti başarıyla yeniden başlamazsa, hizmet başlatılana kadar istemci Configuration Manager tarafından yönetilemez.  

- **İstemciyi Başlat**  

- **İstemciyi durdur**  

    > [!IMPORTANT]  
    > İstemci, hizmet başlatılana kadar Configuration Manager tarafından yönetilemez.  

#### <a name="properties"></a>Özellikler
İstemci ayrıntılarını yüklediğinizde, Destek Merkezi aşağıdaki özellikleri gösterir:  

- **ISTEMCI kimliği**: Configuration Manager istemciyi tanımlamak için kullandığı benzersiz bir tanımlayıcı  

- **Donanım kimliği**: Configuration Manager istemci donanımını tanımlamak için kullanılan benzersiz bir tanımlayıcı  

- **Onaylandı**: istemcinin Configuration Manager karşı onaylanıp onaylanmadığını belirtir  

- **Kayıt durumu**: istemcinin Configuration Manager kayıtlı olup olmadığını belirtir  

- **İnternet 'e yönelik**: istemcinin Internet üzerinde olup olmadığını belirtir  

- **Sürüm**: yüklü Configuration Manager istemcisinin sürüm numarası  

- **Site kodu**: istemcinin atandığı birincil sitenin site kodu  

- **Atanan MP**: istemcinin şu anda atanmış olan yönetim noktasının tam etki alanı adı (FQDN)  

- **YERLEŞIK MP**: yerleşik yönetim noktasının FQDN 'si  

- **Proxy MP**: proxy yönetim noktasının ana bilgisayar adı veya FQDN 'si (varsa)  

- **Proxy site kodu**: ikincil site (varsa) için site kodu  

- **Proxy durumu**: Configuration Manager istemcisinin proxy yönetim noktasının durumu. Örneğin, **etkin** veya **Beklemede**.  



### <a name="policy-tab"></a><a name="bkmk_support-policy"></a>İlke sekmesi

Eski [policyspy](policy-spy.md) aracı yerine bu sekmedeki eylemleri kullanın.

#### <a name="load-policy"></a>Yükleme ilkesi
Bu seçenek görünüme bağlı olarak değişir:

- **Gerçek Ilkeyi yükle**: Görünüm grubunda **Gerçek** ' ı seçin ve ardından ilke grubunda bu seçeneği belirleyin. Destek Merkezi şu anda seçtiğiniz istemci ilkesini yükler.  

- **İstenen Ilkeyi yükle**: Görünüm grubunda **istendi** ' i seçin ve ardından ilke grubunda bu seçeneği belirleyin. Destek Merkezi, istemci tarafından istenen istemci ilkesini yükler.  

- **Varsayılan Ilkeyi yükle**: Görünüm grubunda **varsayılan** ' ı seçin ve ardından ilke grubunda bu seçeneği belirleyin. Destek Merkezi bu istemci için varsayılan ilkeyi yükler.  

Ek seçenekler için bu düğmenin altındaki açılan listeyi seçin:

- **Tümünü Yükle veya Yenile**: gerçek, istenen ve varsayılan ilkeyi aynı anda yükler veya yeniler.  

#### <a name="actual-view"></a>Gerçek görünüm
Gerçek ilke görünümünü açar

#### <a name="requested-view"></a>İstenen görünüm
İstenen ilke görünümünü açar

#### <a name="default-view"></a>Varsayılan görünüm
Varsayılan ilke görünümünü açar. (Bu ilke, Configuration Manager istemcisini yüklediğinizde cihazların aldığı şeydir.)

#### <a name="request-and-evaluate-policy"></a>İlke iste ve değerlendir
Destek Merkezi, istemci ilkesini yönetim noktasından ister ve ardından bu ilkeyi istemcide değerlendirir.

Ek seçenekler için bu düğmenin altındaki açılan listeyi seçin:  

- **İstek ilkesi**: Destek Merkezi istemci ilkesini yönetim noktasından ister.  

- **Ilkeyi değerlendir**: Destek Merkezi istemcide istemci ilkesini değerlendirir.  

- **Ilkeyi varsayılana sıfırlayın**: destek merkezi, Configuration Manager istemciye varsayılan ilkeyi yeniden uygulamayı söyler. İstemcideki tüm makine ve kullanıcı ilkelerini kaldırır.  

#### <a name="listen-for-policy-events"></a>İlke olaylarını dinleyin
Destek Merkezi, ilke olaylarını dinler. İlke olaylarını dinlemeyi devre dışı bırakmak için bu seçeneği tekrar seçin. **İlke olaylarını**görüntülemek için bu sekmenin altındaki oku seçin. 

#### <a name="clear-events"></a>Olayları Temizle
Destek Merkezi, tüm ilke olaylarını temizler.



### <a name="content-tab"></a><a name="bkmk_support-content"></a>İçerik sekmesi

Önbelleğe alınmış içerik dahil olmak üzere istemcideki içeriği görüntüleyin. Yazılım güncelleştirme ve uygulama dağıtımlarının ilerlemesini izleyin. 

#### <a name="load-or-refresh"></a>Yükleme veya yenileme
*Içerik ve önbellek görünümleri için geçerlidir*

Destek Merkezi, şu anda istemcideki içerik listesini yükler veya yeniler.

#### <a name="invoke-trigger"></a>Tetikleyiciyi çağır
Bu menüdeki şu öğeler içerikle ilgili bir istemci eylemi ister:  

- **Konum Hizmetleri**  

    - **İçerik konumlarını Yenile**: herhangi bir etkin içerik indirmeleri tarafından kullanılan dağıtım noktalarını yeniler.  

    - **Yönetim noktalarını Yenile**: istemci tarafından kullanılan yönetim noktalarının iç listesini güncelleştirir.  

    - **Zaman aşımı içerik istekleri**: herhangi bir içerik konumu isteği çok uzun süredir çalışıyorsa, bu eylem isteği sonlandırır.  

- **Uygulama dağıtımı değerlendirmesi**: dağıtılmış uygulamaları değerlendiren bir görev başlatır.  

- **Yazılım güncelleştirmeleri dağıtım değerlendirmesi**: dağıtılan yazılım güncelleştirmelerini değerlendiren bir görev başlatır.  

- **Yazılım güncelleştirmeleri kaynak taraması**: güncelleştirme kaynağı konumlarını tarayan bir görev başlatır.  

- **Windows Installer Kaynak Listesi güncelleştirmesi**: WINDOWS Installer (MSI) yüklemelerinin kaynak konumunu güncelleştiren bir görev başlatır.  

#### <a name="content-view"></a>İçerik görünümü
İstemciye yüklenen uygulamalar, paketler ve güncelleştirmeler bölümüne bakın. Bir uygulama, paket veya güncelleştirme seçtiğinizde, bu içerik hakkındaki ayrıntıları görüntüleyebilirsiniz. Bazı uygulamalar için aşağıdaki işlemleri de yapabilirsiniz:  

- **Yenile**: Ayrıntılar görünümünü yenile  

- **Doğrula veya indir**: bir uygulamanın indirme için kullanılabilir olduğunu doğrulama  

- **Install**: uygulamayı yükler  

- **Kaldır**: uygulamayı kaldır  

#### <a name="cache-view"></a>Önbellek görünümü
İstemci önbellek yapılandırmasını ve önbellek içeriğiyle ilgili ayrıntıları görüntüleyin. Destek merkezini yerel bir istemciye bağladığınızda, CA aşağıdaki işlemleri de yapmanız gerekir:  

- Önbellek konumunu değiştirmek için **önbellek konumu** alanının yanındaki **Değiştir** ' i seçin.  

- Önbelleğin boyutunu ayarlamak için **önbellek boyutu** alanının yanındaki **Değiştir** ' i seçin.  

- İstemci önbelleğini temizlemek için **kullanılan önbellek** alanının yanındaki **Temizle** ' yi seçin.  

Bu görünüm aşağıdaki özellikleri gösterir:  

- **Konum**: her önbellek klasörünün konumu. Windows Gezgini 'nde klasörü açmak için bağlantıyı seçin.   
- **İçerik KIMLIĞI**  
- **Önbellek KIMLIĞI**  
- **Boyut**  
- **Son başvuru**: Bu özellik, istemcinin önbellekteki bu öğeden en son ne zaman okunduğunu veya bu öğeden yazdığı tarihtir.  

#### <a name="monitoring-view"></a>İzleme görünümü
Yazılım güncelleştirmesi ve uygulama güncelleştirme dağıtımlarının etkin ilerlemesini görüntülemek için **izleyici** ' yi seçin. Bu görünüm, uygulama ve yazılım güncelleştirmeleri olay WMI iletilerinden kaynaklanan durum iletilerini gösterir.

Her olay için Görünüm aşağıdaki özellikleri gösterir:  

- **Zaman**: istemcinin olayı harekete aldığı zaman  
- **Konu türü**: durum iletisi türü  
- **Konu kimliği**: günlük dosyalarındaki olaylarla eşlemek için kullanılan durum iletisinin kimliği  
- **Konu kimliği türü**: durum iletisinin alt türü  
- **Durum kimliği**: izlemekte olduğunuz eylemin sonucu  
- **Ayrıntılar** ve **Olay verileri**: Bu görünümde gösterilen durum iletileri hakkında daha fazla bilgi. Durum ayrıntıları bazen boş olabilir.  



### <a name="inventory-tab"></a><a name="bkmk_support-inventory"></a>Envanter sekmesi

#### <a name="load-or-refresh"></a>Yükleme veya yenileme
Destek Merkezi şu anda seçili olan görünümün istemci envanter listesini yükler veya yeniler.

#### <a name="invoke-trigger"></a>Tetikleyiciyi çağır

> [!Note]  
> **Yazılım ölçer rapor döngüsünün**dışındaki görevler için:  
> - Başka bir envanter görevi zaten çalışırken görevi istemeniz durumunda, istemci, geçerli görevi ve diğer sıraya alınmış görevleri tamamladıktan sonra yeni görevi çalışacak şekilde sıraya alır.  
> - **InventoryAgent. log**dosyasında görevin ilerlemesini izleyin.  

Bu menüdeki şu öğeler, stokla ilgili istemci eylemini iste:  

- **Bulgu verileri toplama çevrimi (sinyal)**: cihaz bulma bilgilerini toplamak için kullanılan istemci görevini tetikler  

- **Dosya toplama çevrimi**: yerel dosyaları toplamak için kullanılan istemci görevini tetikler  

- **Donanım envanteri çevrimi**: donanım envanteri verilerini toplamak için kullanılan istemci görevini tetikler  

- **IDMIF toplama çevrimi**: IDMIF verilerini toplamak için kullanılan istemci görevini tetikler  

- **Yazılım envanteri çevrimi**: yazılım envanteri verilerini toplamak için kullanılan istemci görevini tetikler  

- **Yazılım ölçer rapor çevrimi**: bir yazılım kullanım ölçümü raporu oluşturmak ve yönetim noktasına göndermek için kullanılan istemci görevini tetikler. **SWMTRReportGen. log**dosyasında bu görevin ilerlemesini izleyin.

- **Kuyruktaki gönderilmemiş durum Iletilerini gönder**: durum iletilerinin sırasını temizlemek için istemci görevini tetikler.

- **Gelişmiş**  
    - **Donanım envanteri çevrimi (tam yeniden eşitleme)**  
    - **Yazılım envanteri çevrimi (tam yeniden eşitleme)**  


#### <a name="views"></a>Görünümler
Bir özellik etkin değilse, görünüm hiçbir veri görüntülemez. 

- **Durum**: istemcinin topladığı Envanter veri kümelerini göster  

- **DDR**: istemciden toplanan istemci keşif verileri hakkında bilgi  

- **Hinv**: istemciden toplanan donanım envanteri verileri hakkında bilgi  

- **Sinv**: istemciden toplanan yazılım envanteri verileri hakkında bilgi  

- **Dosya koleksiyonu**: istemciden toplanan dosyalarla ilgili bilgiler  

- **IDMIF**: istemciden toplanan IDMIF ve NOIDMIF verileri hakkında bilgi  

- **Ölçüm**: istemciden toplanan yazılım kullanım ölçümü verileri hakkında bilgi  



### <a name="troubleshooting-tab"></a><a name="bkmk_support-troubleshoot"></a>Sorun giderme sekmesi

Configuration Manager istemcileriyle ilgili en yaygın sorunlardan bazılarının sorunlarını giderin:  
- Active Directory sorunlar  
- Windows ağı  
- Configuration Manager   
    - Yönetim noktaları  
    - İlke ataması  
    - Kayıt  


> [!NOTE]  
> Bu sekme, uzak bir Configuration Manager istemcisine bağlandığınızda kullanılamaz.


#### <a name="start"></a>Başlat
İstemcinin sorunlarını gidermeye başlar

- **Active Directory**: yayımlanan Configuration Manager site bilgilerini almak için Active Directory sorgular  
- **Mpcertificate**: yönetim noktası sertifikalarını alır  
- **Mplist**: yönetim noktalarının bir listesini alır  
- **Mpkeyınformation**: yönetim noktası şifreleme anahtarı bilgilerini alır  
- **Ağ oluşturma**: ağlarla ilgili sorunları giderir  
- **Ilke atamaları**: ilke atamalarını alır  
- **Kayıt**: istemcinin siteye kayıtlı olduğunu doğrular  

#### <a name="view-selected-log"></a>Seçili günlüğü görüntüle
Sorun giderme sekmesinde bir satır seçtikten sonra, günlük dosyasını görüntülemek için bu eylemi seçin.

#### <a name="keep-previous-results"></a>Önceki sonuçları sakla
İstemcide sorun giderin ve sonra yeniden sorun gidermeyi denemek istiyorsanız, ilk girişiminizden elde edilecek sonuçları sürdürmek için bu seçeneği belirleyin. Aksi halde, Destek Merkezi önceki sorun giderme günlük dosyalarının üzerine yazar.



### <a name="logs-tab"></a><a name="bkmk_support-logs"></a>Günlükler sekmesi

Bu bölümde, Destek Merkezi aracının **Günlükler** sekmesindeki öğeler listelenir. 

Bu sekme, **günlük Görüntüleyici** aracı ile neredeyse aynıdır. **Günlük Görüntüleyici** Aracı, bu bölümde açıklanan **Istemci günlüğü** ve **günlük grupları** yapılandırma özelliklerini içermez. [Destek Merkezi günlük Görüntüleyici başvuru](#bkmk_log-viewer) bölümü, bu sekmede bulunan diğer seçeneklerin ayrıntılarını alır.

#### <a name="configure-client-logging"></a>İstemci günlüğünü yapılandırma

Aşağıdaki seçenekleri ayarlayın: 
- **İstemci günlük düzeyi**: günlük ayrıntı düzeyi ve dosya boyutu  
- **En fazla dosya sayısı**: belirli bir türde birden fazla günlük dosyasına izin ver  
- **En büyük dosya boyutu**: istemci yeni bir günlük oluşturmadan önce belirli bir günlük dosyasının bayt cinsinden boyutu  

> [!NOTE]  
> Bu değerleri çok düşük ayarlarsanız, istemci yararlı bilgileri günlüğe içermeyebilir. Bu değerleri çok yüksek olarak ayarlarsanız, istemci günlükleri büyük miktarlarda depolama alanı tüketebilir.  

#### <a name="log-groups"></a>Günlük grupları

Günlük dosyalarını **Açık Günlükler** düğmesini kullanarak el ile seçmek yerine, aşağıdaki Özellik alanlarıyla ilişkili tüm günlük dosyalarını açmak için bu açılan listeyi kullanın: 
- **İstenen yapılandırma yönetimi**
- **Envanter**
- **Yazılım dağıtımı**
- **Yazılım güncelleştirmeleri**
- **Uygulama yönetimi**
- **İlke**
- **İstemci kaydı**
- **İşletim Sistemi Dağıtımı**


## <a name="support-center-log-viewer-reference"></a><a name="bkmk_log-viewer"></a>Destek Merkezi günlük Görüntüleyici başvurusu

Bu bölümde, **Destek Merkezi günlük Görüntüleyici** aracı için Kullanıcı arabirimi açıklanmaktadır. 

- [Pencere menüsü](#bkmk_log-window)  
- [Ana Sayfa sekmesi](#bkmk_log-home)  

**Günlük Görüntüleyici** Aracı, **Destek Merkezi**'nin **Günlükler** sekmesiyle neredeyse aynıdır. **Günlük Görüntüleyici** Aracı, **Istemci günlüğü** ve **günlük gruplarını**yapılandırma seçeneklerini içermez.


### <a name="window-menu"></a><a name="bkmk_log-window"></a>Pencere menüsü

Destek Merkezi günlük Görüntüleyici penceresinin sol üst köşesinde, mavi kutudaki oku seçerek bu menüyü açın.

#### <a name="open-logs"></a>Günlükleri aç
Açılacak günlük dosyalarının konumuna gidin. 

#### <a name="options"></a>Seçenekler
**Seçenekler** iletişim kutusunda şunları yapabilirsiniz:
- Animasyonlu Kullanıcı arabirimi öğelerinin hareketini azaltma  
- Günlük görüntüleyicisini,. log ve. lo_ dosya uzantılarına sahip günlük dosyaları için varsayılan uygulama olarak kaydet  
- Uyarıları sıfırlayın. Daha önce gizlenen tüm uyarı iletileri tetiklendiğinde yeniden görüntülenir.  

#### <a name="about"></a>Hakkında
Destek Merkezi günlük Görüntüleyicisi hakkındaki bilgileri görüntüler

#### <a name="close"></a>Kapat
Destek Merkezi günlük görüntüleyicisini kapatır


### <a name="home-tab"></a><a name="bkmk_log-home"></a>Giriş sekmesi

#### <a name="open-logs"></a>Günlükleri aç 
Destek Merkezi, açılacak bir veya daha fazla günlük dosyası seçmenizi ister.

Şeritteki **Açık Günlükler** düğmesinin alt kısmındaki açılan seçimi seçin ve aşağıdaki ek seçeneklerden birini belirleyin: 
- **Günlükleri geçerli görünümde aç**: seçili günlük dosyalarını geçerli görünümde açar  
- **Günlükleri yeni pencerede aç**: seçili günlük dosyalarını yeni bir **günlük Görüntüleyici** penceresinde açar  

#### <a name="close-and-clear-logs"></a>Günlükleri kapatma ve Temizleme
Açık günlük dosyalarını kapatır. Ayrıca, penceredeki tüm günlük dosyası girişlerini de temizler. Destek Merkezi bu girdileri gelecekte görüntülemez.

Şeritteki **Kapat ve temizle** düğmesinin altındaki açılan seçimi seçin ve aşağıdaki ek seçeneklerden birini belirleyin: 
- **Tüm girişleri temizle**: penceredeki tüm günlük dosyası girişlerini temizler. Destek Merkezi bu girdileri gelecekte görüntülemez.  
- **Tüm günlükleri kapat**: açık günlük dosyalarını kapatır  

#### <a name="find"></a>Bul
**Bul** iletişim kutusunu açar. Aranacak dizeyi girin. Diğer dizelerde kısa dizelerdeki eşleşmelerin oluşmasını önlemek için, tüm sözcükleri eşleşmeyi seçebilirsiniz. Ayrıca, dize için büyük/küçük harfe duyarlı eşleştirme yapabilirsiniz.

#### <a name="find-next"></a>Sonrakini Bul
Aradığınız dize için bir eşleşme bulduktan sonra, bu seçenek sizi bir sonraki eşleştirmeye götürür.

#### <a name="find-previous"></a>Öncekini Bul
Aradığınız dize için iki veya daha fazla eşleşme bulduktan sonra, bu seçenek sizi önceki eşleştirmeye götürür.

#### <a name="options"></a>Seçenekler

- **Canlı güncelleştirme**: Şu anda açık olan bir günlük dosyasını değişiklikler için izleyin. Birden çok günlük dosyası açıkken bu özellik çalışmaz. Bu seçenek varsayılan olarak etkindir.  

- **Otomatik kaydırma**: Ayrıca **canlı güncelleştirme** seçeneğini belirlediyseniz, bu seçenek yeni eklenen girişleri göstermek için günlük görünümünü otomatik olarak kaydırır. Birden çok günlük dosyası açıkken bu özellik çalışmaz. Bu seçenek varsayılan olarak etkindir.  

- **Ayrıntıları göster**: bir günlük dosyası iletisi seçtiğinizde, **Günlükler** sekmesinin en altında günlük dosyası iletisinin ayrıntıları görüntülenir. Bu seçenek varsayılan olarak etkindir.  

- **Hızlı filtre**: belirli bir dizeyi bulmak için tüm açık günlük dosyalarındaki günlük dosyası iletilerini filtreleyin. Günlük metnine, bileşen adına ve iş parçacığı KIMLIĞINE göre filtreleyebilirsiniz. Benzer günlük iletilerini bulmak için, bir günlük iletisine sağ tıklayın ve günlük metninde **hızlı filtre** ' yi seçin.  

- **Günlük metnini sarın**: uzun ve çok satırlı iletileri tek bir sütuna sığacak şekilde sarın. Bu davranış, bu iletilerin okunmasını kolaylaştırır. Bu seçenek varsayılan olarak etkindir.  

- **Ham günlük girdisi görüntüleme**: işlenmemiş günlük satırlarını görüntüler.  

- **Gelişmiş filtreler**: **Gelişmiş filtreler** iletişim kutusunu açın. Daha fazla bilgi için bkz. [Gelişmiş günlük dosyası filtreleri](#bkmk_adv-filters).  

- **Hata kodu bağlantıları**: günlük metnindeki hata kodları vurgulanır ve tıklatılabilir. Bu seçenek varsayılan olarak etkindir.  

#### <a name="error-lookup"></a>Hata arama
Şu anda açık olan günlük dosyalarında bu hata kodunu aramak için bir hata kodu girin. Aşağıdaki hata kodu biçimlerini kullanın:
- **32-bit tamsayı (imzalanmış)**: Örneğin,`-2147024891`  
- **32-bit tamsayı (işaretsiz)**: Örneğin,`2147942405`  
- **32 bit onaltılı**: Örneğin,`0x80070005`  

#### <a name="decode-certificate"></a>Kod çözme sertifikası
**Kodu Çöz sertifikası** iletişim kutusunda, istemcideki herhangi bir sertifika için seri hale getirilmiş sertifika değerini yapıştırın. Bu değeri kayıt defterinde, günlük dosyalarında veya WMI 'da bulabilirsiniz. Sertifikayla ilgili genel bilgileri ve ayrıntıları görüntülemek için **işlem** ' i seçin. Bu bilgiler, sertifika yolunu içerir. Sertifikayı bir **. cer** dosyası olarak dışarı aktarmak Için **dışarı aktar** ' ı seçin.



## <a name="advanced-log-file-filters"></a><a name="bkmk_adv-filters"></a>Gelişmiş günlük dosyası filtreleri

Gelişmiş günlük dosyası filtreleri, belirli dizeleri dahil etme, hariç tutma veya vurgulamanıza olanak tanır. Günlük dosyası girişlerine baktığınızda, bu dizeler bir günlük dosyasında veya günlük dosyası grubunda gerçekleşebilir. Filtre oluştururken joker karakter aramalarını kullanın. Filtrelerin faydalı bir birleşimini kullandığınızda bunları bir *filtre kümesi*olarak kaydedin. 

Gelişmiş günlük dosyası filtreleri hızlı filtrelerin yerini alır. Her ikisini birlikte kullanın, ancak hızlı filtreler yalnızca, görüntülenecek günlük verileri için geçerlidir. Gelişmiş filtreler, herhangi bir hızlı filtre uygulamadan önce hangi verilerin başlangıçta görüntülendiğini tespit edilir.

Gelişmiş Filtreler iletişim kutusunda karmaşık filtre kümeleri oluşturabilirsiniz. Bu filtre kümeleri birçok günlük dosyası bileşeni arasında dize arar. Bu bileşenler ileti, iş parçacığı, günlük düzeyi ve bileşenleri içerir. Bir filtre kümesi, günlük dosyası iletilerini dahil etmek, dışlamak veya vurgulamak için kullandığınız birden çok filtre deyimi içerir. Filtre, bir işleç ve bir değer içinde aranacak günlük dosyası sütununu tanımlar. Değer, *Joker* karakter `*`gibi normal ifadeler içerebilir.


### <a name="add-a-filter"></a>Filtre ekleme

1. **Günlük Görüntüleyici** penceresinde veya Destek Merkezi **günlükleri** sekmesinde **Gelişmiş filtreler**' i seçin.  

2. Gelişmiş Filtreler iletişim kutusunda **Ekle**' yi seçin. Ardından, Filtrenizle eşleşen günlük girdilerine göre hareket etmek için aşağıdaki seçeneklerden birini belirleyin:  
    - **İçeriyor**  
    - **Exclude**  
    - **Vurgula**  

3. **Gelişmiş Filtre yapılandırması** iletişim kutusunda bir sütun ve işleç seçin:  

    - **Sütun**: Filtrenizle eşleşen dizelerin aranacağı yeri seçin:  

         - **Günlük metni**: günlük dosyası metni içinde arama  

         - **Günlük önem derecesi**: belirli bir önem düzeyine sahip günlükleri arayın. **Değer** alanında bu önem düzeylerini ayarlayın.  

         - **Bileşen**: belirli bir bileşeni ada göre ara  

         - **Iş parçacığı kimliği**: belirli bir Iş parçacığı kimliği olan günlük iletilerini arama  

         - **Kaynak dosya**: belirli bir günlük dosyasında gerçekleşen günlük iletilerini arama  

    - **İşleç**: filtreniz için bir operatör seçin  

4. **Değer** alanında filtrelemek için bir değer girin. Değer normal ifadeler içeriyorsa, **normal ifade eşleştirmeyi etkinleştir**' i seçin.  


### <a name="manage-filter-sets"></a>Filtre Kümelerini Yönet

- Bir filtreyi düzenlemek için filtreyi seçin ve ardından **Düzenle**' yi seçin.  

- Bir filtreyi silmek için filtreyi seçin ve **Sil**' i seçin.  

- Tüm filtreleri temizlemek için **Temizle**' yi seçin.  

- Geçerli filtre kümesini kaydetmek için **filtreleri kaydet**' i seçin. Sonra filtre kümesini **. Filterset** dosyası olarak kaydedin.  

- Kaydedilmiş bir filtre kümesini yüklemek için, **yükleme filtreleri**' ni seçin. Daha önce kaydedilmiş bir **. Filterset** dosyasına gözatın.  



## <a name="support-center-viewer-reference"></a><a name="bkmk_viewer"></a>Destek Merkezi Görüntüleyicisi başvurusu

Bu bölümde, Configuration Manager **Destek Merkezi Görüntüleyicisi** aracı için kullanıcı ARABIRIMI (UI) açıklanmaktadır. Kullanılabilir sekmeler, sorun giderme paketinin içeriğine göre farklılık gösterir. [Pencere menüsü](#bkmk_viewer-window) ve [Giriş sekmesi](#bkmk_viewer-home) varsayılan olarak gösterilir.
- [Pencere menüsü](#bkmk_viewer-window)
- [Ana Sayfa sekmesi](#bkmk_viewer-home)
- [Yapılandırma sekmesi](#bkmk_viewer-config)
- [Günlükler sekmesi](#bkmk_viewer-logs)
- [Hata ayıklama dökümleri sekmesi](#bkmk_viewer-debug)
- [WMI sekmesi](#bkmk_viewer-wmi)
- [Kayıt defteri sekmesi](#bkmk_viewer-registry)
- [İlke sekmesi](#bkmk_viewer-policy)
- [Sertifikalar sekmesi](#bkmk_viewer-certs)
- [Sorun giderme sekmesi](#bkmk_viewer-troubleshoot)


### <a name="window-menu"></a><a name="bkmk_viewer-window"></a>Pencere menüsü

Destek Merkezi Görüntüleyicisi penceresinin sol üst köşesinde, mavi kutudaki oku seçerek bu menüyü açın.

#### <a name="open-bundle"></a>Paketi aç
Destek Merkezi tarafından oluşturulan bir veri paketinin konumuna gidin.

#### <a name="about"></a>Hakkında
Destek Merkezi Görüntüleyicisi hakkındaki bilgileri görüntüler.

#### <a name="options"></a>Seçenekler
**Seçenekler** iletişim kutusunda şunları yapabilirsiniz:
- Animasyonlu Kullanıcı arabirimi öğelerinin hareketini azaltma  
- Geçici dosyaların konumunu değiştirme    
- Uyarıları sıfırlayın. Daha önce gizlenen tüm uyarı iletileri tetiklendiğinde yeniden görüntülenir.  
- Geçici dosya yolunu varsayılana sıfırlayın,`%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Çık
Destek Merkezi görüntüleyicisinden çıkar


### <a name="home-tab"></a><a name="bkmk_viewer-home"></a>Giriş sekmesi

#### <a name="open-bundle"></a>Paketi aç
Destek Merkezi tarafından oluşturulan bir veri paketinin konumuna gidin.

#### <a name="open-log-file"></a>Günlük dosyasını aç
Açmak için bir veya daha fazla günlük dosyası seçin.

#### <a name="decode-certificate"></a>Kod çözme sertifikası
**Kodu Çöz sertifikası** iletişim kutusunda, istemcideki herhangi bir sertifika için seri hale getirilmiş sertifika değerini yapıştırın. Bu değeri kayıt defterinde, günlük dosyalarında veya WMI 'da bulabilirsiniz. Sertifikayla ilgili genel bilgileri ve ayrıntıları görüntülemek için **işlem** ' i seçin. Bu bilgiler, sertifika yolunu içerir. Sertifikayı bir **. cer** dosyası olarak dışarı aktarmak Için **dışarı aktar** ' ı seçin.


### <a name="configuration-tab"></a><a name="bkmk_viewer-config"></a>Yapılandırma sekmesi

Destek Merkezi Görüntüleyicisi aracının **yapılandırma** SEKMESI, WMI sağlayıcılarından alınan verileri kullanarak aşağıdaki görünümleri sağlar:

#### <a name="client"></a>İstemci
Bu görünüm, Destek Merkezi 'nin **istemci** sekmesinde gösterilen bilgileri görüntüler.

#### <a name="operating-system"></a>İşletim sistemi
İstemcinin işletim sistemi için ayrıntılar. [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem) sınıfını kullanır.

#### <a name="computer"></a>Bilgisayar
İstemci bilgisayarın ayrıntıları. [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem) sınıfını kullanır.

#### <a name="services"></a>Hizmetler
İstemci bilgisayarda çalışan hizmetlerin ayrıntıları. [Win32_Service](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-service) sınıfını kullanır.

#### <a name="network-adapters"></a>Ağ bağdaştırıcıları
İstemci bilgisayarda yüklü olan ağ bağdaştırıcılarının ayrıntıları. [Win32_NetworkAdapterConfiguration](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration) sınıfını kullanır.


### <a name="logs-tab"></a><a name="bkmk_viewer-logs"></a>Günlükler sekmesi

**Günlükler** sekmesi, pakete dahil edilen günlük dosyalarının bir listesini gösterir. Bu sekmedeki her satır, günlük dosyasının yolunu, adını ve boyutunu sağlar. 

#### <a name="open"></a>Open
Günlük dosyasını seçtikten sonra, **günlük görüntüleyicisini**açmak için bu düğmeyi seçin. Destek Merkezi günlükleri sekmesinde görülen işlevselliğin bir alt kümesini sağlar.

#### <a name="decode-certificate"></a>Kod çözme sertifikası
**Kodu Çöz sertifikası** iletişim kutusunda, istemcideki herhangi bir sertifika için seri hale getirilmiş sertifika değerini yapıştırın. Bu değeri kayıt defterinde, günlük dosyalarında veya WMI 'da bulabilirsiniz. Sertifikayla ilgili genel bilgileri ve ayrıntıları görüntülemek için **işlem** ' i seçin. Bu bilgiler, sertifika yolunu içerir. Sertifikayı bir **. cer** dosyası olarak dışarı aktarmak Için **dışarı aktar** ' ı seçin.


### <a name="debug-dumps-tab"></a><a name="bkmk_viewer-debug"></a>Hata ayıklama dökümleri sekmesi

Bu sekmedeki her satır, dışarı aktarmak için kullanılabilen hata ayıklama döküm dosyaları hakkında ayrıntılar sağlar. Daha fazla analiz için hata ayıklama döküm dosyalarını (. dmp) dışarı aktarmak için bu sekmeyi kullanın. Bu analiz, WinDbg gibi bir hata ayıklama aracı kullanır. 

> [!WARNING]  
> Hata ayıklama dökümlerinde parolalar, şifreleme gizli dizileri veya Kullanıcı verileri gibi hassas bilgiler bulunabilir. Yalnızca Microsoft Desteği personeli için hata ayıklama dökümlerini toplayın. Hata ayıklama dökümlerini içeren veri paketleri, yetkisiz erişimlerden korunmak için dikkatle işlenmelidir.  

#### <a name="export"></a>Dışarı Aktarma
Seçili hata ayıklama döküm dosyasının bir kopyasını kaydedin.


### <a name="wmi-tab"></a><a name="bkmk_viewer-wmi"></a>WMI sekmesi

Bu sekme, veri paketinin içerdiği Configuration Manager istemcisinden WMI verisi kümesini gösterir. 

#### <a name="find"></a>Bul
Aşağıdaki özelliklere sahip olan bul iletişim kutusunu açar:  

- **Aranan: WMI**veri kümesinde aramak için bir dize girin. Joker karakterleri destekler.  

- **Bakış**: bir eşleşen **sınıf veya örnek adı**, **özellik**veya **değer**için WMI veri kümesi içinde arama yapmak isteyip istemediğinizi seçin.  

- **Yalnızca tüm dizeyi eşleştir**: varsayılan olarak, Bul iletişim kutusu, aradığınız dizeyi içeren dizeleri arar. Yalnızca belirttiğiniz dizeyle tam eşleşen dizeleri bulmak için bu onay kutusunu seçin.  

#### <a name="find-next"></a>Sonrakini Bul
Bu düğme, WMI veri kümesi içindeki bul iletişim kutusunda verdiğiniz dizenin bir sonraki örneğini açar.

#### <a name="decode-certificate"></a>Kod çözme sertifikası
**Kodu Çöz sertifikası** iletişim kutusunda, istemcideki herhangi bir sertifika için seri hale getirilmiş sertifika değerini yapıştırın. Bu değeri kayıt defterinde, günlük dosyalarında veya WMI 'da bulabilirsiniz. Sertifikayla ilgili genel bilgileri ve ayrıntıları görüntülemek için **işlem** ' i seçin. Bu bilgiler, sertifika yolunu içerir. Sertifikayı bir **. cer** dosyası olarak dışarı aktarmak Için **dışarı aktar** ' ı seçin.


### <a name="registry-tab"></a><a name="bkmk_viewer-registry"></a>Kayıt defteri sekmesi

Veri paketine dahil edilen kayıt defteri verilerini görüntülemek ve daha fazla analiz için bu verileri dışarı aktarmak için **kayıt defteri** sekmesini kullanın.

#### <a name="export"></a>Dışarı Aktarma
Kayıt defteri anahtarı ve seçtiğiniz alt anahtarların bir kopyasını kayıt defteri (. reg) dosyası olarak kaydedin.

#### <a name="find"></a>Bul
Aşağıdaki özelliklere sahip olan bul iletişim kutusunu açar:  

- **Aranan: WMI**veri kümesinde aramak için bir dize girin. Joker karakterleri destekler.  

- **Bakış**: bir eşleşen **sınıf veya örnek adı**, **özellik**veya **değer**için WMI veri kümesi içinde arama yapmak isteyip istemediğinizi seçin.  

- **Yalnızca tüm dizeyi eşleştir**: varsayılan olarak, Bul iletişim kutusu, aradığınız dizeyi içeren dizeleri arar. Yalnızca belirttiğiniz dizeyle tam eşleşen dizeleri bulmak için bu onay kutusunu seçin.  

#### <a name="find-next"></a>Sonrakini Bul
Bu düğme, WMI veri kümesi içindeki bul iletişim kutusunda verdiğiniz dizenin bir sonraki örneğini açar.

#### <a name="decode-certificate"></a>Kod çözme sertifikası
**Kodu Çöz sertifikası** iletişim kutusunda, istemcideki herhangi bir sertifika için seri hale getirilmiş sertifika değerini yapıştırın. Bu değeri kayıt defterinde, günlük dosyalarında veya WMI 'da bulabilirsiniz. Sertifikayla ilgili genel bilgileri ve ayrıntıları görüntülemek için **işlem** ' i seçin. Bu bilgiler, sertifika yolunu içerir. Sertifikayı bir **. cer** dosyası olarak dışarı aktarmak Için **dışarı aktar** ' ı seçin.


### <a name="policy-tab"></a><a name="bkmk_viewer-policy"></a>İlke sekmesi

**İlke** sekmesi, veri paketine dahil edilen ilke verilerini görüntülemek için kullanılır. 

#### <a name="find"></a>Bul
Aşağıdaki özelliklere sahip olan bul iletişim kutusunu açar:  

- **Aranan: WMI**veri kümesinde aramak için bir dize girin. Joker karakterleri destekler.  

- **Bakış**: bir eşleşen **sınıf veya örnek adı**, **özellik**veya **değer**için WMI veri kümesi içinde arama yapmak isteyip istemediğinizi seçin.  

- **Yalnızca tüm dizeyi eşleştir**: varsayılan olarak, Bul iletişim kutusu, aradığınız dizeyi içeren dizeleri arar. Yalnızca belirttiğiniz dizeyle tam eşleşen dizeleri bulmak için bu onay kutusunu seçin.  

#### <a name="find-next"></a>Sonrakini Bul
Bu düğme, WMI veri kümesi içindeki bul iletişim kutusunda verdiğiniz dizenin bir sonraki örneğini açar.

#### <a name="decode-certificate"></a>Kod çözme sertifikası
**Kodu Çöz sertifikası** iletişim kutusunda, istemcideki herhangi bir sertifika için seri hale getirilmiş sertifika değerini yapıştırın. Bu değeri kayıt defterinde, günlük dosyalarında veya WMI 'da bulabilirsiniz. Sertifikayla ilgili genel bilgileri ve ayrıntıları görüntülemek için **işlem** ' i seçin. Bu bilgiler, sertifika yolunu içerir. Sertifikayı bir **. cer** dosyası olarak dışarı aktarmak Için **dışarı aktar** ' ı seçin.


### <a name="certificates-tab"></a><a name="bkmk_viewer-certs"></a>Sertifikalar sekmesi

**Sertifikalar** sekmesi, veri paketine dahil edilen sertifikaları görüntülemek ve bunları dışarı aktarmak için kullanılır.

#### <a name="view-certificate"></a>Sertifikayı görüntüle
Seçilen sertifikayla ilgili bilgileri görüntüler.

#### <a name="export"></a>Dışarı Aktarma
Seçtiğiniz sertifikanın bir kopyasını kaydetmek için **farklı kaydet** iletişim kutusunu açar.


### <a name="troubleshooting-tab"></a><a name="bkmk_viewer-troubleshoot"></a>Sorun giderme sekmesi

Destek Merkezi sorun giderme sekmesi kullanılarak oluşturulan günlük dosyalarını görüntülemek için **sorun giderme** sekmesini kullanın.

#### <a name="view-log"></a>Günlüğü görüntüle
**Sorun giderme** sekmesinde bir satır seçtikten sonra, günlük Görüntüleyicisi ile günlük dosyasını görüntülemek için bu seçeneği belirleyin.
