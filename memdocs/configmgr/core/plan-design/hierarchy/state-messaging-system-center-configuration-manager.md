---
title: Durum iletileri
titleSuffix: Configuration Manager
description: Desteklenen Configuration Manager sürümlerindeki durum iletilerinin açıklamaları.
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720936"
---
# <a name="state-messages-in-configuration-manager"></a>Configuration Manager durum iletileri 

*Uygulama hedefi: Configuration Manager (geçerli dal)*

Durum iletileri Configuration Manager istemcisindeki koşullar hakkında kısa bilgiler içerir. Durum mesajlaşma sistemi, yazılım güncelleştirmeleri ve yapılandırma ayarları gibi belirli Configuration Manager bileşenleri tarafından kullanılır.

Configuration Manager istemcileri, işlemlerin geçerli durumunu raporlamak için geri dönüş durum noktasına veya yönetim noktası site sistemlerine durum iletileri gönderir. Configuration Manager istemcileri tarafından gönderilen durum iletilerini görüntülemek için raporlar oluşturabilirsiniz.

Durum iletilerini kullanan her bir Configuration Manager özelliği, durum iletisinin konu türü tarafından tanımlanır. Bu makalede listelenen durum iletisi konu türleri, bir durum iletisinin ilişkili olduğu Configuration Manager özelliğini tanımlamak için kullanılabilir.

> [!NOTE]  
> Sıfır (0) durum iletisi KIMLIK değeri, genellikle konu türünün bilinmeyen bir durumda olduğunu gösterir.

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 0 | Uyumluluk durumu bilinmiyor|
| 1 | Uyumlu | 
| 2 | Uyumlu değil | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 0  | Zorlama durumu bilinmiyor |
| 1  | Güncelleştirme (ler) yükleniyor        | 
| 2  | Yeniden başlatma bekleniyor          | 
| 3  | Başka bir yüklemenin tamamlanması bekleniyor         | 
| 4  | Güncelleştirme (2) başarıyla yüklendi          | 
| 5  | Sistem yeniden başlatma bekleniyor         | 
| 6  | Güncelleştirme (ler) yüklenemedi         | 
| 7  | Güncelleştirmeler indiriliyor   | 
| 8  | Güncelleştirmeler indirildi    | 
| 9  | Güncelleştirme (ler) indirilemedi     | 
| 10 | Yüklemeden önce bakım penceresi bekleniyor         | 
| 11 | Düzenleme bekleniyor         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|      
| 0 | Değerlendirme durumu bilinmiyor|                 
| 1 |Değerlendirme etkinleştirildi      |
| 2 |Değerlendirme başarılı      |
| 3 |Değerlendirme başarısız oldu      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 0 | Algılama durumu bilinmiyor|
| 1 | Gerekli değil   |
| 2 | Algılanmadı    |
| 3 | Tespit edildi   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 0 | Uyumluluk durumu bilinmiyor|
| 1 |Uyumlu     |
| 2 |Uyumlu değil     |
| 3 |Çakışma algılandı    |
| 4 |Hata      |
| 5 |Bilinmiyor     |
| 6 |Kısmi uyumluluk   |
| 7 |Uyumluluk yapılandırılmadı    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 0  | Zorlama durumu bilinmiyor|
| 1  |Zorlama başlatıldı          |
| 2  |Zorlama içerik bekliyor         |
| 3  | Başka bir yüklemenin tamamlanması bekleniyor        |
| 4  |Yüklemeden önce bakım penceresi bekleniyor         |
| 5  |Yüklemeden önce yeniden başlatma gerekiyor         |
| 6  |Genel hata        |
| 7  |Yüklenmeyi bekliyor         |
| 8  |Güncelleştirme yükleniyor          |
| 9  |Sistem yeniden başlatma bekleniyor        |
| 10 |Güncelleştirme başarıyla yüklendi         |
| 11 |Güncelleştirme yüklenemedi        |
| 12 |Güncelleştirme indiriliyor        |
| 13 | Güncelleştirme indirildi        |
| 14 |Güncelleştirme indirilemedi        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
|0 |Algılama durumu bilinmiyor|
| 1 | Güncelleştirme gerekli değil  |
| 2 | Güncelleştirme gerekiyor   |
| 3 | Güncelleştirme yüklendi  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 0 |Tarama durumu bilinmiyor|
| 1 | Tarama, içerik bekliyor   |
| 2 | Tarama çalışıyor    |
| 3 | Tarama tamam    |
| 4 | Tarama yeniden deneme bekliyor   |
| 5 | Tarama başarısız oldu   |
| 6 | Tarama hatalarla tamamlandı |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

Durum kimliği yok.

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

Durum kimliği yok.

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
Durum kimliği yok.

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 100 |İstemci dağıtımı başlatıldı      |       
| 101 |İndirme bekleniyor       |       
| 102 |Dağıtım zamanlandı       |       
| 103 | Dağıtılmadan önce pencere bekleniyor |
| 104 |Dağıtım atlandı       |       
| 301 |Bilinmeyen istemci dağıtım hatası |       
| 302 |CCMSetup hizmeti oluşturulamadı  |       
| 303 |CCMSetup hizmeti silinemedi |       
| 304 |Sistem sürücüsünde etkinleştirilmiş dosya tabanlı yazma Filtresi (FBWF) ile birlikte katıştırılmış işletim sistemi yüklenemez |       
| 305 |Yerel güvenlik modu Windows 2000 ' de geçerli değildir  |       
| 306 |CCMSetup indirme işlemi başlatılamadı  |       
| 307 |Geçerli olmayan CCMSetup komut satırı |       
| 308 |Dosya, WINHTTP üzerinden şu adreste indirilemedi: |       
| 309 |Şu adresteki dosyalar BITS ile indirilemedi |       
| 310 |BITS sürümü yüklenemedi |       
| 311 |Önkoşul dosyasının MS imzalı olduğunu doğrulayamıyorum  |       
| 312 |Disk dolu olduğundan dosya kopyalanamadı |       
| 313 |Client. msi yüklemesi MSI hatasıyla başarısız oldu |       
| 314 |CCMSetup. xml bildirim dosyası yüklenemedi |       
| 315 |İstemci sertifikası alınamadı  |       
| 316 |Önkoşul dosyası MS imzalı değil |       
| 317 |Yüklemeye devam etmek için yeniden başlatma gerekiyor  |       
| 318 |MP ve istemci sürümleri eşleşmediğinden istemci MP 'ye yüklenemiyor |       
| 319 |İşletim sistemi veya hizmet paketi desteklenmiyor  |       
| 320 |Dağıtım desteklenmiyor       |       
| 321 |BITS eksik        |       
| 322 |Kaynak klasör kullanılamıyor       |       
| 323 |Appv desteklenmiyor              |       
| 324 |Yanlış site sürümü              |       
| 325 |Önkoşul karması uyuşmazlığı       |       
| 326 |MDM kaydı silme başarısız      |       
| 327 |MDM kaydı algılandı      |       
| 328 |Intune algılandı       |       
| 329 |Tarifeli ağa Izin verilmiyor      |       
| 400 |İstemci dağıtımı başarılı oldu |  
| 401 |Dağıtım başarılı yeniden başlatma gerekiyor     |       
| 402 |Dağıtım başarıyla yeniden başlatıldı     |
| 500 |İstemci ataması başlatıldı|
| 601 |Bilinmeyen istemci atama hatası|
| 602 |Aşağıdaki site kodu geçersiz|
| 603 |MP 'ye atanamadı|
| 604 |Varsayılan yönetim noktası bulunamadı|
| 605 |Site imzalama sertifikası indirilemedi|
| 606 |Site kodu otomatik olarak bulunamadı|
| 607 |Site ataması başarısız oldu; istemci sürümü, site sürümünden daha yüksek|
| 608 |Active Directory Domain Services ve SLP 'den site sürümü alınamadı|
| 609 |İstemci sürümü alınamadı|
| 700 |İstemci ataması başarılı oldu|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

Durum kimliği yok.

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 100 | Kayıt durumu   |
| 101 | Kayıt zamanlandı   |
| 102 | Kayıt iptal edildi   |
| 105 | Kayıt başlatıldı   |
| 106 | Kayıt başarılı ancak sağlanmadı
| 107 | Kayıt başarılı oldu ve sağlandı
| 108 | Kayıt etkin kullanıcı yok   |
| 110 | Kayıt başarısız oldu   |


## <a name="820--state_topictype_client_wufb"></a>820 STATE_TOPICTYPE_CLIENT_WUFB

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 | Iş Windows Update için istemci durumu| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 | Disk alanı   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

Durum kimliği yok.

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

Durum kimliği yok.

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

Durum kimliği yok.

## <a name="1000--state_topictype_client_framework_comm"></a>1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 | İstemci, yönetim noktasıyla başarıyla iletişim kuruyor |
| 2 | İstemci, yönetim noktasıyla iletişim kuramadı |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |İstemci, sertifikayı yerel sertifika deposundan başarıyla aldı    |
| 2 |İstemci, sertifikayı yerel sertifika deposundan alamadı |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

Durum kimliği yok.

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

Durum kimliği yok.

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

Durum kimliği yok.

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

Durum kimliği yok.

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

Durum kimliği yok.

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

Durum kimliği yok.

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

Durum kimliği yok.

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

Durum kimliği yok.

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

Durum kimliği yok.

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

Durum kimliği yok.

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

Durum kimliği yok.

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

Durum kimliği yok.

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

Durum kimliği yok.

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

Durum kimliği yok.

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |İstemci yerel mod için hazırlanma  |
| 2 |İstemci yerel moda hazırlanıyor     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 | Başarılı|
| 2 | Başarılı değil |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

Durum kimliği yok.

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

Durum kimliği yok.

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

Durum kimliği yok.

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

Durum kimliği yok. 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Kullanıcı benzeşimi kümesi       |
| 2 |Kullanıcı benzeşimi kaldırıldı       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

Durum kimliği yok.

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

Durum kimliği yok.

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1000  |Yapılandırma öğesi başarılı oldu           |
| 1001 |Yapılandırma öğesi başarılı bir şekilde yüklendi         |
| 1002 |Yapılandırma öğesi başarılı ön kontrol          |
| 1003 |Yapılandırma öğesi hızlı durumu başarılı oldu          |
| 2000 |Yapılandırma öğesi devam ediyor           |
| 2001 |Yapılandırma öğesi devam ediyor, içerik bekleniyor         |
| 2002 |Yapılandırma öğesi yüklenirken devam ediyor          |
| 2003 |Yapılandırma öğesi devam eden yeniden başlatma bekliyor         |
| 2004 |Yapılandırma öğesi devam ediyor bakım penceresi bekleniyor        |
| 2005 |Yapılandırma öğesi devam ediyor, zamanlamayı bekliyor         |
| 2006 |Yapılandırma öğesi bağımlı içeriği indirmede devam ediyor     |
| 2007 |Yapılandırma öğesi bağımlılıkları yüklerken devam ediyor        |
| 2008 |Yapılandırma öğesi devam eden yeniden başlatma bekliyor         |
| 2009 |Yapılandırma öğesi, devam eden içerik indirildi         |
| 2010 |Yapılandırma öğesi devam ediyor, güncelleştirme bekliyor         |
| 2011 |Yapılandırma öğesi, kullanıcının yeniden bağlanmasını bekliyor        |
| 2012 |Yapılandırma öğesi Kullanıcı oturumunu beklerken devam ediyor         |
| 2013 |Yapılandırma öğesi Kullanıcı oturumunu beklerken devam ediyor         |
| 2014 |Yapılandırma öğesi devam ediyor, yüklemesi bekleniyor         |
| 2015 |Yapılandırma öğesi devam ediyor, yeniden deneme bekliyor         |
| 2016 |Yapılandırma öğesi devam ediyor, presmode bekleniyor         |
| 2017 |Yapılandırma öğesi, düzenleme için beklerken devam ediyor        |
| 2018 |Yapılandırma öğesi devam ediyor, ağ için bekleniyor         |
| 2019 |Yapılandırma öğesi devam ediyor VE güncelleştirme bekliyor         |
| 2020 |Yapılandırma öğesi VE güncelleştirme devam ediyor         |
| 3000 |Yapılandırma öğesi gereksinimleri karşılanmadı           |
| 3001 |Yapılandırma öğesi gereksinimleri karşılanmadı ana bilgisayar uygulanamaz        |
| 4000 |Yapılandırma öğesi bilinmiyor           |
| 5000 |Yapılandırma öğesi hatası            |
| 5001 |Yapılandırma öğesi hatası değerlendirilirken          |
| 5002 |Yapılandırma öğesi yüklenirken hata oluştu          |
| 5003 |Yapılandırma öğesi içerik alınırken hata oluştu         |
| 5004 |Bağımlılık yükleme yapılandırma öğesi hatası         |
| 5005 |Yapılandırma öğesi içerik bağımlılığı alınırken hata oluştu        |
| 5006 |Yapılandırma öğesi hata kuralları çakışması          |
| 5007 |Yapılandırma öğesi hatası yeniden denenme bekleniyor          |
| 5008 |Değiştirme kaldırma sırasında yapılandırma öğesi hatası        |
| 5009 |Yenisiyle değiştirilen yapılandırma öğesi hatası         |
| 5010 |Yapılandırma öğesi hata güncelleştirme VE          |
| 5011 |Yapılandırma öğesi lisans yüklenirken hata oluştu         |
| 5012 |Yapılandırma öğesi hatası alma tüm güvenilen uygulamalara izin ver       |
| 5013 |Yapılandırma öğesi hata No lisansı yok         |
| 5014 |Yapılandırma öğesi hata işletim sistemi desteklenmiyor          |
| 6000 |Yapılandırma öğesi başarıyla başlatılamadı            |
| 6010 |Yapılandırma öğesi başlatma hatası            |
| 6020 |Yapılandırma öğesi başlatma bilinmiyor|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

Durum kimliği yok.

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

Durum kimliği yok.

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

Durum kimliği yok.

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

Durum kimliği yok.

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

Durum kimliği yok.

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

Durum kimliği yok.

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

Durum kimliği yok.

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

Durum kimliği yok.

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Endpoint Protection yönetilmeyen   |
| 2 |Endpoint Protection yüklemesi bekleniyor  |
| 3 |Endpoint Protection yönetiliyor   |
| 4 |Endpoint Protection yüklenemedi  |
| 5 |Endpoint Protection yeniden başlatma bekleniyor  |
| 6 |Endpoint Protection desteklenmiyor   |
| 7 |Endpoint Protection birlikte yönetilen   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 0 |Endpoint Protection ilkesi uygulama durumu bilinmiyor    |
| 1 |Endpoint Protection ilkesi uygulaması başarılı oldu    |
| 2 |Endpoint Protection ilkesi uygulaması başarısız oldu    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 0 |  Bilinmiyor    |
| 1 |  Etkin    |
| 2 |  Etkin değil    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 | Uyandırma proxy 'Si yüklü değil    |
| 2 | Uyandırma proxy 'Si yüklemeyi bekliyor   |
| 3 | Uyandırma proxy 'Si yüklendi    |
| 4 | Uyandırma proxy 'Si yüklemesi başarısız oldu   |
| 5 | Uyandırma proxy 'Si yeniden başlatma bekliyor   |
| 6 | Uyandırma proxy 'Si bu işletim sisteminde desteklenmiyor  |
| 7 | Uyandırma proxy sunucusu geri çevirme   |
| 8 | Uyandırma proxy 'Si kaldırma başarısız   |
| 9 | Uyandırma proxy çalışma zamanı desteklenmiyor   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

Durum kimliği yok.

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

Durum kimliği yok.

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

Durum kimliği yok.

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
|0 | Windows anında Iletme bildirimi hizmeti Kanal kümesi|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

Durum kimliği yok.

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

Durum kimliği yok.

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

Durum kimliği yok.

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

Durum kimliği yok.

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

Durum kimliği yok.

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

Durum kimliği yok.

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

Durum kimliği yok.

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

Durum kimliği yok.

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

Durum kimliği yok.

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

Durum kimliği yok.

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

Durum kimliği yok.

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

Durum kimliği yok.

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Sınama verildi         |
| 2 |Sınama sorunu başarısız oldu        |
| 3 |İstek oluşturma başarısız        |
| 4 |İstek gönderilemedi        |
| 5 |Sınama doğrulaması başarılı       |
| 6 |Sınama doğrulaması başarısız oldu       |
| 7 |Sorun başarısız oldu         |
| 8 |Sorun beklemede         |
| 9 |Verilmesi          |
| 10 |Yanıt işlenemedi       |
| 11 |Yanıt bekliyor         |
| 12 |Kayıt başarılı oldu         |
| 13 |Kayıt gerekli değil         |
| 14 |İptal Edildi          |
| 15 |Koleksiyondan kaldırıldı        |
| 16 |Yenileme doğrulandı         |
| 17 |Yüklenemedi        |
| 18 |Yüklendi         |
| 19 |Silme başarısız oldu         |
| 20 |Silme         |
| 21 |Yenileme istendi        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Sınama verildi         |
| 2 |Sınama sorunu başarısız oldu        |
| 3 |İstek oluşturma başarısız        |
| 4 |İstek gönderilemedi        |
| 5 |Sınama doğrulaması başarılı       |
| 6 |Sınama doğrulaması başarısız oldu       |
| 7 |Sorun başarısız oldu         |
| 8 |Sorun beklemede         |
| 9 |Verilmesi          |
| 10 |Yanıt işlenemedi       |
| 11 |Yanıt bekliyor         |
| 12 |Kayıt başarılı oldu         |
| 13 |Kayıt gerekli değil         |
| 14 |İptal Edildi          |
| 15 |Koleksiyondan kaldırıldı        |
| 16 |Yenileme doğrulandı         |
| 17 |Yüklenemedi        |
| 18 |Yüklendi         |
| 19 |Silme başarısız oldu         |
| 20 |Silme         |
| 21 |Yenileme istendi        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 | Durum sabitleme kurulumu başarılı oldu       |
| 2 | Durum sabitleme kurulumu başarısız oldu       |
| 3 | Durum PIN kurulumu desteklenmiyor      |
| 4 | Durum sabitleme kurulumu devam ediyor      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

Durum kimliği yok.

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

Durum kimliği yok.

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

Durum kimliği yok.

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

Durum kimliği yok.

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

Durum kimliği yok.

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

Durum kimliği yok.

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Sınama verildi    |
| 2 |Sınama sorunu başarısız oldu   |
| 3 |İstek oluşturma başarısız   |
| 4 |İstek gönderilemedi   |
| 5 |Sınama doğrulaması başarılı  |
| 6 |Sınama doğrulaması başarısız oldu  |
| 7 |Sorun başarısız oldu    |
| 8 |Sorun beklemede    |
| 9 |Verilmesi     |
| 10 |Yanıt işlenemedi  |
| 11 |Yanıt bekliyor    |
| 12 |Kayıt başarılı oldu    |
| 13 |Kayıt gerekli değil    |
| 14 |İptal Edildi     |
| 15 |Koleksiyondan kaldırıldı   |
| 16 |Yenileme doğrulandı    |
| 17 |Yüklenemedi   |
| 18 |Yüklendi    |
| 19 |Silme başarısız oldu    |
| 20 |Silme    |
| 21 |Yenileme istendi   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
|| 1 | Uyumluluk başarısı    |
| 2 | MP 'de uyumluluk başarısız oldu   |
| 3 | İstemcide uyumluluk başarısız oldu   |
| 4 | Intune 'da uyumluluk başarısız oldu   |
| 5 | AAD 'de uyumluluk başarısız oldu   |
| 6 | Uyumluluk comgmt Intune   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Eş önbellek kaynağı eklendi       |
| 2 |Eş önbellek kaynağı kaldırıldı      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Eş önbellek kaynağı devre dışı       |
| 2 |Eş önbellek kaynağı etkin       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Toplu verileri karşıya yüklemeyi indir       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Eş kaynak reddetme verileri karşıya yükleme     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

Durum kimliği yok.

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

Durum kimliği yok.

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

Durum kimliği yok.

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

Durum kimliği yok.

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     Durum Iletisi KIMLIĞI     |  Durum Iletisi açıklaması |
|:-------------|:------|
| 1 |Durum kanıtlama destekleniyor      |
| 2 |Sistem durumu kanıtlama desteklenmiyor      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

Durum kimliği yok.

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

Durum kimliği yok.

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

Durum kimliği yok.

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

Durum kimliği yok.

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

Durum kimliği yok.

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

Durum kimliği yok.

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

Durum kimliği yok.

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

Durum kimliği yok.

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

Durum kimliği yok.

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

Durum kimliği yok.

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

Durum kimliği yok.

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

Durum kimliği yok.

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

Durum kimliği yok.

## <a name="next-steps"></a>Sonraki adımlar

- [Configuration Manager durum mesajlaşma açıklaması](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Configuration Manager için yazılım güncelleştirme yönetimi teknik incelemesi](https://www.microsoft.com/download/details.aspx?id=44578)
