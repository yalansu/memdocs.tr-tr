---
title: İstemci Gözetleme
titleSuffix: Configuration Manager
description: Configuration Manager istemcilerinde yazılım dağıtımı, envanteri ve yazılım kullanım ölçümü sorunlarını gidermek için Istemci Spy kullanın.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723435"
---
# <a name="client-spy"></a>İstemci Gözetleme

*Uygulama hedefi: Configuration Manager (geçerli dal)*

İstemci Spy [Configuration Manager araçlarından](tools.md)biridir. Configuration Manager istemcilerinde yazılım dağıtımı, envanteri ve yazılım kullanım ölçümü sorunlarını gidermeye yönelik bir araçtır. 

Araç tarafından alınan bilgilerin çoğu yazılım dağıtımlarıyla ilgilidir:
- Tüm geçerli yazılım dağıtımları 
- Yazılım dağıtım geçmişi
- İstemci önbelleği yapılandırması
- Önbelleğe alınmış öğeler
- Bekleyen gerekli dağıtımlar
- Kullanılabilir dağıtımlar  

Ayrıca, aşağıdaki envanter bilgilerini görüntüler
- En son envanter çevrimi tarihi
- Son rapor tarihi
- Yazılım envanteri birincil ve ikincil sürümleri
- Dosya koleksiyonu
- Donanım envanteri
- IDMıF koleksiyonu
- Bulgu verileri kayıtları (DDR 'ler) 

Yazılım kullanım ölçümü kuralları da görüntülenir. 

> [!Note]   
> Bu araç, performansı artırmak için, her bir sekmeye ilişkin bilgileri yalnızca siz seçtiğinizde toplar. Benzer şekilde, **Yenile**' ye tıkladığınızda yalnızca görüntülenmekte olan sekmeye ait bilgiler yenilenir.



## <a name="usage"></a>Kullanım


### <a name="tools-menu"></a>Araçlar menüsü

**Araçlar** menüsünde aşağıdaki eylemler mevcuttur:  

#### <a name="connect"></a>Bağlan
Farklı bir bilgisayardan bilgi alın.  

- Varsayılan olarak, araç geçerli bilgisayardan bilgileri görüntüler. 

- Hesap için uzak bilgisayar adını, Kullanıcı adını ve parolayı kullanarak bağlanın. Araç, uzak bilgisayardaki IPC $ paylaşımıyla bir bağlantı oluşturur. Araç çıktığında ya da başka bir bilgisayara bağlandığınızda bağlantıyı siler.  

- Bilgileri almak için yeterli kimlik bilgilerine sahip bir hesap gerektirir.  

- Bir Kullanıcı adı ve parola belirtmezseniz, Istemci Spy bağlantıyı yapmayı denemek için şu anda oturum açmış olan kullanıcının güvenlik bağlamını kullanır.  

- Uzak bir bilgisayara bağlandığınızda, görüntülenen tüm sekmeler uzak bilgisayardan bilgileri gösterir.

#### <a name="software-distribution"></a>Yazılım Dağıtımı
[Yazılım dağıtımı](#software-distribution) sekmelerini görüntüler ve diğer sekmeleri gizler. Varsayılan olarak, Istemci Spy yazılım dağıtım sekmelerini görüntüler.

#### <a name="inventory"></a>Envanter
Stok sekmesini görüntüler ve diğer sekmeleri gizler.

#### <a name="software-metering"></a>Yazılım Kullanım Ölçümü
Yazılım kullanım ölçümü sekmesini görüntüler ve diğer sekmeleri gizler.

#### <a name="save-current-tab-to-file"></a>Geçerli sekmeyi dosyaya kaydet
Bilgileri görüntülenmekte olan sekmeye belirttiğiniz bir metin dosyasına kaydeder. 

#### <a name="save-all-tabs-to-file"></a>Tüm sekmeleri dosyaya kaydet
Tüm sekmelerdeki bilgileri belirttiğiniz bir metin dosyasına kaydeder. Yalnızca hesabınızın görebileceği bilgileri kaydeder.



## <a name="software-distribution-tab"></a>Yazılım dağıtımı sekmesi

Aşağıdaki dört sekmede ayarları yapılandırın:
- [Yazılım dağıtımı yürütme Istekleri](#bkmk_exec-requests)
- [Yazılım dağıtım geçmişi](#bkmk_history)
- [Yazılım dağıtımı önbellek bilgileri](#bkmk_cache-info)
- [Yazılım dağıtımı bekleyen yürütmeler](#bkmk_pending-exec)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a>Yazılım dağıtımı yürütme Istekleri

Bu sekme, hem cihaz hem de kullanıcı hedefli dağıtımlar dahil olmak üzere tüm mevcut dağıtımları görüntüler.

Yazılım dağıtımı yürütme Istekleri sekmesindeki her ağaç öğesi aşağıdaki dört özniteliği içerir:
- Tanıtım KIMLIĞI. Bu değer, kullanılabilir bir dağıtım ise boş olabilir. 
- Paket Kimliği 
- Program Adı 
- Kullanıcısını. Bu, hedeflenen kullanıcı SID 'SI veya isteği başlatan kullanıcının SID 'SI olabilir. Her ikisi de sistem isteklerinden, görüntülenen kullanıcı sistemidir. 

Her çalıştırma isteği için, bir alt ağaç yapısında aşağıdaki bilgiler de görüntülenir:
- Program Adı 
- Paket Kimliği 
- Paket Adı 
- İstek oluşturma zamanı 
- Durum 
- Durum çalışıyorsa çalışma durumu 
- Yürütme bağlamı (Kullanıcı veya yönetici) 
- Geçmiş durumu (başarı, hata veya NotRun) 
- LastRunTime (program daha önce çalıştırılmadıysa, hiçbir koşulda) 
- RetryCount, durum WaitingRetry ise 
- ContentAccess (yeniden deneme sayısı, durum WaitingRetry ise) 
- FailureCode, durum WaitingRetry ise 
- FailureReason, durum WaitingRetry ise 

İstek içerik gerektiriyorsa, durum WaitingContent olur. Yazılım dağıtım önbelleği bilgileri sekmesinde, bu indirme isteğinin ayrıntıları gösterilir.

Çalıştırma isteği bir indirme isteği ise, indirilen bayt sayısını da görüntüler.

> [!Note]   
> Bir çalıştırma isteğinin değişen durumları için farklı simgeler kullanır.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a>Yazılım dağıtım geçmişi

Bu sekme, daha önce çalıştırılan tüm programlarla ilgili bilgiler içerir. Bu bilgiler kayıt defterinde saklanır.

Bu ağacın ana dalları, sistem dahil farklı Kullanıcı geçmişlerdir. Her Kullanıcı için programların çalıştırıldığı paketlerin listesini içeren bir alt ağacı görüntüler. 

Her paket alt ağacı için paket KIMLIĞI ve paket adı, çalışan programların bir listesini görüntüler. Her biri için aşağıdaki öznitelikleri görüntüler: 
- Program adı
- Çalışma durumu
- Son çalışma zamanı
- Hata kodu
- Hata nedeni  

Bir program başarıyla çalıştırıldığında hata kodu ve hata nedeni boştur.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a>Yazılım dağıtımı önbellek bilgileri

#### <a name="cache-config"></a>Önbellek yapılandırması
Configuration Manager Istemci önbelleğiyle ilgili bilgileri içerir. Bu bilgiler önbellek konumunu, önbellek boyutunu ve şu anda kullanımda olup olmadığını içerir. 

#### <a name="cached-items"></a>Önbelleğe alınmış öğeler
Şu anda önbellekte bulunan tüm öğelerin bir alt ağacını içerir. Her ağaç öğesi, her öğe hakkında aşağıdaki bilgileri içerir: 
- Önbellekte öğenin konumu (klasörü)
- Geçerli durum
- Paket Kimliği
- Paket adı
- Paket sürümü
- Paket boyutu
- Geçerli başvuru sayısı
- Son başvurulan saat (UTC)  

#### <a name="downloading-items"></a>Öğeler indiriliyor
İstemci şu anda indirmekte olan öğelerdir. Her biri, önbelleğe alınmış öğeler tarafından gösterilen bilgilerin yanı sıra indirilen kilobayt sayısını gösterir. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a>Yazılım dağıtımı bekleyen yürütmeler

Bu sekme, geçmiş ve gelecekteki gerekli dağıtımların ve kullanılabilir dağıtımların bir listesinin ayrıntılarını içeren bilgileri içerir.

Her ağaç dalı, sistem dahil olmak üzere kullanılabilir dağıtımları olan her kullanıcı hesabı içindir.

Her Kullanıcı için, bir alt ağaç aşağıdaki üç öğeyi içerir:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Gelecekteki yürütmeler Ile zorunlu tanıtımlar
Bunlar, hala çalışmaya kalan programları olan zorunlu tanıtımlar. Bunlar yinelenen, tek seferlik veya birden çok zamanlama tanıtımları olabilir. Her biri reklam KIMLIĞINI, sonraki çalışma zamanını ve reklamın çalıştığı zamanlamayı görüntüler. 

#### <a name="optional-advertisements"></a>İsteğe bağlı tanıtımlar
Yayımlanan tüm tanıtımlar listesini görüntüler. Ayrıca, her biri için tanıtım KIMLIĞI, program adı ve paket adı gibi ayrıntıları da görüntüler. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Gelecekteki zamanlanmış yürütmeler olmadan geçmiş zorunlu tanıtımlar
Bu, istemcide çalışan ve gelecekte zamanlanmış programları olmayan reklamları içeren bir listesidir. Tanıtım KIMLIĞI, paket adı ve program adı görüntülenir. İsteğe bağlı olan tüm tanıtımlar için bir alt ağaç öğesi görüntülenir.

> [!Note]  
> Paket adı bilgileri yalnızca, görüntülenen bilgisayarda bunlarla ilişkili tanıtılan ilkeleri olan paketler için kullanılabilir. Artık bunlarla ilişkili kullanılabilir ilkeleri olmayan paketler, "paket adı artık kullanılamıyor" iletisini görüntüler.  



## <a name="inventory-tab"></a>Envanter sekmesi

Envanter bilgilerini içeren tek bir sekme vardır. Ana ağaç aşağıdaki beş öğeyi içerir:  

- **Yazılım envanteri**: son döngüsünün başladığı tarihi, son raporun tarihini ve son raporun ikincil ve ana sürümlerini içerir.  

- **Dosya koleksiyonu**: son döngüsünün başladığı tarihi, son raporun tarihini ve son raporun ikincil ve ana sürümlerini içerir.  

- **Donanım envanteri**: son döngüsünün başladığı tarihi, son raporun tarihini ve son raporun ikincil ve ana sürümlerini içerir.  

- **IDMIF Collection**: son döngüsünün başladığı tarihi, son raporun tarihini ve son raporun ikincil ve ana sürümlerini içerir.  

- **DDR**: son döngüsünün başladığı tarihi, son raporun tarihini ve son raporun ikincil ve ana sürümlerini içerir. DDR bilgileri de bir alt ağaçta görüntülenir.



## <a name="software-metering-tab"></a>Yazılım ölçer sekmesi

Bu sekme, bilgileri bir alt ağaç olarak görüntüler ve tüm yazılım kullanım ölçümü kurallarını içerir. Her kuralı, dosya adı ve kural KIMLIĞI tarafından tanımlanan bir düğüm olarak görüntüler. Ağaçtaki her düğümü genişletin ve aşağıdaki bilgileri görüntüleyin:
- Gezgin dosyası adı 
- Özgün dosya adı
- Kural Kimliği
- Dosya sürümü
- Dil


