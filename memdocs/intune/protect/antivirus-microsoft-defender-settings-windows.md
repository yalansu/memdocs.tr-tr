---
title: Intune için Microsoft Defender virüsten koruma için Windows 10 Antivirus ilke ayarları | Microsoft Docs
description: Windows 10 için Microsoft Defender virüsten koruma profilindeki ayarların listesini görüntüleyin. Bu ayarları, Microsoft Intune Endpoint Security virüsten koruma ilkesinin bir parçası olarak yapılandırabilirsiniz.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/05/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 7d8ea221b6c1768055e3ca1839c20ed64e2e3838
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802030"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Microsoft Intune 'de Windows 10 Microsoft Defender virüsten koruma ilkesi ayarları

Microsoft Intune 'de Windows 10 için Microsoft Defender virüsten koruma profili için yapılandırabileceğiniz virüsten koruma ilkesi ayarlarını görüntüleyin.

## <a name="cloud-protection"></a>Bulut koruması

- **Buluta teslim edilen korumayı aç**  
  CSP: [Allowcloudprotection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Varsayılan olarak, Windows 10 masaüstü cihazlarındaki Defender, bulduğu sorunlar hakkında Microsoft 'a bilgi gönderir. Microsoft, sizi ve diğer müşterileri etkileyen sorunlar hakkında daha fazla bilgi edinmek için bu bilgileri çözümleyerek geliştirilmiş çözümler sunar.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -buluta teslim edilen koruma açıktır.  Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Buluta teslim edilen koruma düzeyi**  
  CSP: [Cloudblocklevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Agresif Defender virüsten koruma 'nın şüpheli dosyaları engelleme ve tarama hakkında daha fazla yapılandırma.
  - **Yapılandırılmadı** (*varsayılan*)-varsayılan Defender engelleme düzeyi.
  - İstemci performansını iyileştirirken, yanlış pozitif sonuçlar içeren daha büyük bir şanstan oluşan **yüksek** performanslı bir ungo blok.
  - **Yüksek artı-güvenip** , istemci performansını etkileyebilecek ek koruma önlemleri uygular.
  - **Sıfır toleransı** -tüm bilinmeyen yürütülebilir dosyaları engelle.

- **Defender bulut uzatılmış zaman aşımı (saniye)**  
  CSP: [Cloudextendedtimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender virüsten koruma, güvenli olduklarından emin olmak için kuşkulu dosyaları 10 saniye içinde otomatik olarak engeller. Bu ayarla, bu zaman aşımı için en fazla 50 ek saniye ekleyebilirsiniz.

## <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender virüsten koruma dışlamaları

Bu gruptaki her bir ayar için ayarı genişletebilir, **Ekle**' yi seçebilir ve sonra dışlama için bir değer belirtebilirsiniz.

- **Dışlanacak Defender işlemi**  
  CSP: [Excludedprocesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Bir tarama sırasında yoksayılacak işlem tarafından açılan dosyaların listesini belirtin. İşlemin kendisi taramadan çıkarılmaz.

- **Taramalardan ve gerçek zamanlı korumanın dışında tutulacak dosya uzantıları**  
  CSP: [ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Tarama sırasında yoksayılacak dosya türü uzantılarının listesini belirtin.

- **Dışlanacak Defender dosyaları ve klasörleri**  
  CSP: [Excludedpaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Tarama sırasında yoksayılacak dosya ve Dizin yollarının listesini belirtin.

## <a name="real-time-protection"></a>Gerçek zamanlı koruma

- **Gerçek zamanlı korumayı aç**  
  CSP: [AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Windows 10 Masaüstü cihazlarında Defender 'ın gerçek zamanlı Izleme işlevini kullanmasını gerektir.
  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -gerçek zamanlı izlemenin kullanımını zorla. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Erişim Koruması 'nı etkinleştir**  
  CSP: [Allowonaccessprotection](https://go.microsoft.com/fwlink/?linkid=2113935)

  İsteğe bağlı olarak, sürekli etkin olan virüs korumasını yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-Bu ilke, bir cihazdaki bu ayarın durumunu değiştirmez. Cihazdaki mevcut durum değişmeden kalır.
  - Cihazlarda erişim koruması için **hiçbir blok yok** . Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -açık erişim koruması cihazlarda etkin.

- **Gelen ve giden dosyalar için izleme**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Hangi NTFS dosyası ve program etkinliğinin izleneceğini öğrenmek için bu ayarı yapılandırın.
  - **Tüm dosyaları izle** (*varsayılan*)
  - **Yalnızca gelen dosyaları izle**
  - **Yalnızca giden dosyaları izle**

- **Davranış izlemeyi aç**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Varsayılan olarak, Windows 10 Masaüstü cihazlarda Defender davranış Izleme işlevini kullanır.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -gerçek zamanlı davranış izlemenin kullanımını zorunlu tutun. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Ağ korumasını aç**  
  CSP: [Enablenetworkprotection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Herhangi bir uygulamanın kimlik avı dolandırıcılığı, yararlanma siteleri ve Internet 'teki kötü amaçlı içeriklere erişmesini kullanarak cihaz kullanıcılarını koruyun. Koruma, üçüncü taraf tarayıcıların tehlikeli sitelere bağlanmasını engellemeyi de kapsar.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -ağ koruması açıktır. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **İndirilen tüm dosyaları ve ekleri Tara**  
  CSP: [Enablenetworkprotection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Tüm indirilen dosya ve ekleri taramak için Defender 'ı yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -Defender indirilen tüm dosya ve ekleri tarar. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Microsoft tarayıcılarında kullanılan betikleri tarayın**  
  CSP: [Allowscriptscanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Defender 'ı betikleri tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -Defender betikleri tarar. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Ağ dosyalarını Tara**  
  CSP: [Allowscanningnetworkfiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Defender 'ı ağ dosyalarını tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -ağ dosyalarının taranmasını aç. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **E-postaları Tara**  
  CSP: [Allowemailscanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Defender 'ı gelen e-postayı tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -e-posta taramasını açın. Cihaz kullanıcıları bu ayarı değiştiremezler.

## <a name="remediation"></a>Düzeltme

- **Karantinaya alınan kötü amaçlı yazılımı tutmak için gün sayısı (0-90)**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Sistemin, karantinaya alınan öğeleri otomatik olarak kaldırılmadan önce depoladığından, 0 ile 90 arasında bir gün sayısı belirtin. Sıfır değeri, Karantinadaki öğeleri tutar ve onları otomatik olarak kaldırmaz.

- **Örnek onayı gönder**  

  - **Yapılandırılmadı** (*varsayılan*)
  - **Güvenli örnekleri otomatik olarak gönder**
  - **Her zaman sor**
  - **Hiçbir şekilde gönderme**
  - **Tüm örnekleri otomatik olarak gönder**

- **İstenmeyebilecek uygulamalarda gerçekleştirilecek eylem**  
  CSP: [Puaprotection](https://go.microsoft.com/fwlink/?linkid=2114051)

  İstenmeyebilecek uygulamalar için algılama düzeyini belirtin (PUAs). Defender, istenmeyebilecek yazılımların indirileceği veya bir cihaza yüklenmeye çalıştığı durumlarda kullanıcıları uyarır.

  - **Yapılandırılmadı** (*varsayılan*)-ayar, Pua koruması kapalı olan sistem varsayılan ayarlarına geri yüklenir.
  - **Devre Dışı Bırak**
  - **Enable** -algılanan öğeler engellenir ve diğer tehditlerle birlikte geçmiş olarak gösterilir.
  - **Denetim modu** -Defender istenmeyebilecek uygulamaları algılar, ancak hiçbir işlem gerçekleşmez. Olay Görüntüleyicisi Defender tarafından oluşturulan olayları arayarak, uygulama Defender ile ilgili bilgileri gözden geçirebilirsiniz.

- **Algılanan tehditler için Eylemler**  
  CSP: [Threatseveritydefaultaction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Kötü amaçlı yazılımın tehdit düzeyine bağlı olarak algılanan kötü amaçlı yazılım için Defender 'ın aldığı eylemi belirtin.
  
  Defender, algıladığı kötü amaçlı yazılımları aşağıdaki önem düzeylerinden biri olarak sınıflandırır:
  - **Düşük önem derecesi**
  - **Orta önem derecesi**
  - **Yüksek önem derecesi**
  - **Ciddi önem derecesi**

  Her düzey için gerçekleştirilecek eylemi belirtin. Her önem düzeyi için varsayılan değer *Yapılandırılmadı*.

  - **Yapılandırılmadı**
  - **Temizle** -hizmet, dosyaları kurtarmaya çalışır ve bulaşmaya çalışabilir.
  - **Karantina** -dosyaları karantinaya alma.
  - **Remove** -dosyaları cihazdan kaldırır.
  - **Allow** -dosyaya izin verir ve başka eylemler almaz.
  - **Kullanıcı tanımlı** -cihaz kullanıcısı hangi eylemin ele alınacağı kararını yapar.
  - **Blok** -dosya yürütmeyi engeller.

## <a name="scan"></a>Tara

- **Arşiv dosyalarını tara**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Defender 'ı ZIP veya CAB dosyaları gibi arşiv dosyalarını tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar, arşivlenen dosyaları taramak için istemci varsayılan değerini döndürür, ancak kullanıcı bunu devre dışı bırakabilir.
Daha fazla bilgi edinin
  - Dosya Arşivi **taranmaz.** Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -arşiv dosyalarının taranmasını etkinleştirin. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Zamanlanan Taramalar için düşük CPU önceliği kullan**  
  CSP: [Enablelowcpupriınıd](https://go.microsoft.com/fwlink/?linkid=2113944)

  Zamanlanan Taramalar için CPU önceliğini yapılandırın.
  - **Yapılandırılmadı** (*varsayılan*)-ayar, CPU önceliğinde hiçbir değişiklik yapılmamakta sistem varsayılan değerini döndürür.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -düşük CPU önceliği, zamanlanmış taramalar sırasında kullanılacaktır. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Yakalama tam taramasını devre dışı bırak**  
  CSP: [Disablecatch Upfullscan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Zamanlanan tam taramalar için yakalama taramaları yapılandırın. Bir yakalama taraması, düzenli olarak zamanlanmış bir tarama kaçırıldığı için başlatılan bir taramadır. Bilgisayar zamanlanan saatte kapatılmış olduğundan, genellikle bu zamanlanmış taramalar kaçırıldı.

  - **Yapılandırılmadı** (*varsayılan*)-ayar, istemci Varsayılanı ' na döndürülür, bu, tam taramalar için yakala taramaların etkinleştirilmesi anlamına gelir, ancak kullanıcı bunları kapatabilir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -zamanlanmış tam taramalar için yakalama taramaları zorlanır ve Kullanıcı bunları devre dışı bırakamaz. Arka arkaya iki zamanlanmış tarama için bir bilgisayar çevrimdışıysa, bir Kullanıcı bilgisayarda ilk kez oturum açtığında bir yakalama taraması başlatılır. Yapılandırılmış zamanlanmış tarama yoksa, hiçbir yakalama tarama çalıştırması olmaz. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Yakalama hızlı taramayı devre dışı bırak**  
  CSP: [Disablecatchupquickscan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Zamanlanan hızlı taramalar için yakalama taramaları yapılandırın. Bir yakalama taraması, düzenli olarak zamanlanmış bir tarama kaçırıldığı için başlatılan bir taramadır. Bilgisayar zamanlanan saatte kapatılmış olduğundan, genellikle bu zamanlanmış taramalar kaçırıldı.

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar, istemci Varsayılanı ' na döndürülür, bu da yakalama hızlı taramaların etkinleştirilmesi, ancak kullanıcı bunları kapatabilir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -zamanlanmış hızlı taramalar için yakalama taramaları zorlanır ve Kullanıcı bunları devre dışı bırakamaz. Arka arkaya iki zamanlanmış tarama için bir bilgisayar çevrimdışıysa, bir Kullanıcı bilgisayarda ilk kez oturum açtığında bir yakalama taraması başlatılır. Yapılandırılmış zamanlanmış tarama yoksa, hiçbir yakalama tarama çalıştırması olmaz. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Tarama başına CPU kullanım sınırı**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Defender taraması için Ortalama CPU yükleme faktörü olan 0 ile 100 arasında bir yüzde olarak belirtin.

- **Tam tarama sırasında eşlenmiş ağ sürücülerine Tara**  
  CSP: [Allowfullscanonmappednetworkdrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Defender 'ı eşlenmiş ağ sürücülerine tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar, eşlenen ağ sürücülerinde taramayı devre dışı bırakan sistem varsayılan ayarlarına geri yüklenir.
  - **Hayır** -ayar devre dışı bırakıldı. Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Evet** -eşlenen ağ sürücülerinin taranmasını etkinleştirin. Cihaz kullanıcıları bu ayarı değiştiremezler.

- **Günlük hızlı taramayı şurada Çalıştır:**  
  CSP: [Schedulequickscantime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Defender hızlı taramanın çalışacağı günün saatini seçin.
  Varsayılan olarak, bu **yapılandırılmaz**

- **Tarama türü**  
  CSP: [Scanparameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Defender 'ın çalıştığı taramanın türünü seçin.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Hızlı tarama**
  - **Tam tarama**

- **Zamanlanmış tarama çalıştırmak için haftanın günü**  
  - **Yapılandırılmadı** (*varsayılan*)

- **Zamanlanan taramayı çalıştırmak için günün saati**  
  - **Yapılandırılmadı** (*varsayılan*)

- **Taramayı çalıştırmadan önce imza güncelleştirmelerini denetle**  
  - **Yapılandırılmadı** (*varsayılan*)
  - **Hayır**
  - **Evet**

## <a name="updates"></a>Güncelleştirmeler

- **Güvenlik Zekası güncelleştirmelerini denetleme sıklığını (0-24 saat) girin**  
  CSP: [Signatureupdateınterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  İmzaları denetlemek için kullanılan aralığı sıfır ile 24 arasında (saat cinsinden) belirtin. Sıfır değeri, yeni imzalar için denetim yok sonucunu vermez. 2 değeri her iki saatte bir denetlenir ve bu şekilde devam eder.

## <a name="user-experience"></a>Kullanıcı deneyimleri

- **Microsoft Defender uygulamasına kullanıcı erişimine izin ver**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **Yapılandırılmadı** (*varsayılan*)-ayar, Kullanıcı arabirimi ve bildirimlerine izin verilen istemci varsayılan değerini döndürür.
  - **Hayır** -Defender Kullanıcı ARABIRIMINE (UI) erişilemiyor ve bildirimler Ware gizlendi.
  - **Evet**

