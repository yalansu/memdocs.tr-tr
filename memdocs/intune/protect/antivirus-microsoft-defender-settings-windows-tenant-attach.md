---
title: Kiracı ekli cihazlar için Microsoft Defender virüsten koruma ilke ayarları | Microsoft Docs
description: Configuration Manager tarafından yönetilen Windows 10 cihazları için Microsoft Defender virüsten koruma profilindeki ayarların listesini görüntüleyin. Bu ayarları, Configuration Manager için kiracı eklemeyi yapılandırdıktan sonra Microsoft Intune Endpoint Security virüsten koruma ilkesinin bir parçası olarak yapılandırabilirsiniz.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: 3bb1d4806271ab40c60f0ad419e4e708d36bbc97
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194132"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Microsoft Intune 'de kiracı ekli cihazlar için Microsoft Defender virüsten koruma ilkesi ayarları

Intune 'dan **Microsoft Defender virüsten koruma ilkesi (ConfigMgr)** profiliyle yönetebileceğiniz Microsoft Defender virüsten koruma ayarlarını görüntüleyin. Intune [Endpoint Security virüsten koruma ilkesini](../protect/endpoint-security-antivirus-policy.md)yapılandırırken profil kullanılabilir ve [kiracı iliştirme](../protect/tenant-attach-intune.md) senaryosunu yapılandırdığınızda Configuration Manager ile yönettiğiniz cihazlara dağıtılır.

## <a name="cloud-protection"></a>Bulut koruması

- **Buluta teslim edilen korumayı aç**  
  CSP: [Allowcloudprotection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Varsayılan olarak, Windows 10 masaüstü cihazlarındaki Defender, bulduğu sorunlar hakkında Microsoft 'a bilgi gönderir. Microsoft, sizi ve diğer müşterileri etkileyen sorunlar hakkında daha fazla bilgi edinmek için bu bilgileri çözümleyerek geliştirilmiş çözümler sunar.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **İzin verilmiyor.** Microsoft Etkin Koruma Hizmeti kapatır.
  - **İzin verilen.**  Microsoft Etkin Koruma Hizmeti açar.

- **Buluta teslim edilen koruma düzeyi**  
  CSP: [Cloudblocklevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Agresif Defender virüsten koruma 'nın şüpheli dosyaları engelleme ve tarama hakkında daha fazla yapılandırma.
  - **Yapılandırılmadı** (*varsayılan*)-varsayılan Defender engelleme düzeyi.
  - İstemci performansını iyileştirirken, yanlış pozitif sonuçlar içeren daha büyük bir şanstan oluşan **yüksek** performanslı bir ungo blok.
  - **Yüksek artı-güvenip** , istemci performansını etkileyebilecek ek koruma önlemleri uygular.
  - **Sıfır toleransı** -tüm bilinmeyen yürütülebilir dosyaları engelle.

- **Defender bulut uzatılmış zaman aşımı (saniye)**  
  CSP: [Cloudextendedtimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender virüsten koruma, güvenli olduklarından emin olmak için kuşkulu dosyaları 10 saniye içinde otomatik olarak engeller. Bu ayarla, bu zaman aşımı için en fazla 50 ek saniye ekleyebilirsiniz.

## <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender virüsten koruma dışlamaları

Bu gruptaki her bir ayar için ayarı genişletebilir, **Ekle**' yi seçebilir ve sonra dışlama için bir değer belirtebilirsiniz.

- **Dışlanacak Defender işlemi**  
  CSP: [Excludedprocesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Bir tarama sırasında yoksayılacak işlem tarafından açılan dosyaların listesini belirtin. İşlemin kendisi taramadan çıkarılmaz.

- **Taramalardan ve gerçek zamanlı korumanın dışında tutulacak dosya uzantıları**  
  CSP: [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Tarama sırasında yoksayılacak dosya türü uzantılarının listesini belirtin.

- **Dışlanacak Defender dosyaları ve klasörleri**  
  CSP: [Excludedpaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Tarama sırasında yoksayılacak dosya ve Dizin yollarının listesini belirtin.

## <a name="real-time-protection"></a>Gerçek zamanlı koruma

- **Gerçek zamanlı korumayı aç**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Windows 10 Masaüstü cihazlarında Defender 'ın gerçek zamanlı Izleme işlevini kullanmasını gerektir.
  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir
  - **İzin verilmiyor.** Gerçek zamanlı izleme hizmetini kapatır.
  - **İzin verilen.** Gerçek zamanlı izleme hizmetini açar ve çalıştırır.

- **Erişim Koruması 'nı etkinleştir**  
  CSP: [Allowonaccessprotection](https://go.microsoft.com/fwlink/?linkid=2113935)

  İsteğe bağlı olarak, sürekli etkin olan virüs korumasını yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-Bu ilke, bir cihazdaki bu ayarın durumunu değiştirmez. Cihazdaki mevcut durum değişmeden kalır.
  - **İzin verilmiyor.** Gerçek zamanlı izleme hizmetini kapatır.
  - **İzin verilen.**

- **Gelen ve giden dosyalar için izleme**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Hangi NTFS dosyası ve program etkinliğinin izleneceğini öğrenmek için bu ayarı yapılandırın.
  - **Tüm dosyaları izle (çift yönlü).** (*varsayılan*)
  - **Gelen dosyaları izleyin.**
  - **Giden dosyaları izleyin.**

- **Davranış izlemeyi aç**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Varsayılan olarak, Windows 10 Masaüstü cihazlarda Defender davranış Izleme işlevini kullanır.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **İzin verilmiyor.** Davranış izlemeyi kapatır.
  - **İzin verilen.** Gerçek zamanlı davranış izlemeyi etkinleştirir.

- **Yetkisiz erişim önleme sistemine izin ver**  
  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **İzin verilmiyor.**
  - **İzin verilen.**

- **İndirilen tüm dosyaları ve ekleri Tara**  
  CSP: [Enablenetworkprotection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Tüm indirilen dosya ve ekleri taramak için Defender 'ı yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **İzin verilmiyor.**
  - **İzin verilen.**

- **Microsoft tarayıcılarında kullanılan betikleri tarayın**  
  CSP: [Allowscriptscanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Defender 'ı betikleri tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **İzin verilmiyor.**
  - **İzin verilen.**

- **Ağ dosyalarını Tara**  
  CSP: [Allowscanningnetworkfiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Defender 'ı ağ dosyalarını tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **İzin verilmiyor.** Ağ dosyalarının taranmasını devre dışı bırakır.
  - **İzin verilen.** Ağ dosyalarını tarar.

- **E-postaları Tara**  
  CSP: [Allowemailscanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Defender 'ı gelen e-postayı tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar sistem varsayılan ayarlarına geri yüklenir.
  - **İzin verilmiyor.** E-posta taramasını kapatır.
  - **İzin verilen.** E-posta taramasını etkinleştirir.

## <a name="remediation"></a>Düzeltme

- **Karantinaya alınan kötü amaçlı yazılımı tutmak için gün sayısı (0-90)**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Sistemin, karantinaya alınan öğeleri otomatik olarak kaldırılmadan önce depoladığından, 0 ile 90 arasında bir gün sayısı belirtin. Sıfır değeri, Karantinadaki öğeleri tutar ve onları otomatik olarak kaldırmaz.

- **Örnek onayı gönder**  

  - **Yapılandırılmadı** (*varsayılan*)
  - **Her zaman sor.**
  - **Güvenli örnekleri otomatik olarak gönderin.**
  - **Hiçbir şekilde gönderme.**
  - **Tüm örnekleri otomatik olarak gönder.**

- **İstenmeyebilecek uygulamalarda gerçekleştirilecek eylem**  
  CSP: [Puaprotection](https://go.microsoft.com/fwlink/?linkid=2114051)

  İstenmeyebilecek uygulamalar için algılama düzeyini belirtin (PUAs). Defender, istenmeyebilecek yazılımların indirileceği veya bir cihaza yüklenmeye çalıştığı durumlarda kullanıcıları uyarır.

  - **Yapılandırılmadı** (*varsayılan*)-ayar, Pua koruması kapalı olan sistem varsayılan ayarlarına geri yüklenir.
  - **PUA koruması kapalı.** Windows Defender, istenmeyebilecek uygulamalara karşı koruma sağlamaz.
  - **PUA koruma.** Algılanan öğeler engellendi. Bunlar, diğer tehditlerle birlikte geçmiş olarak gösterilir.
  - **Denetim modu.** Defender, istenmeyebilecek uygulamaları algılar, ancak hiçbir işlem gerçekleşmez. Olay Görüntüleyicisi Defender tarafından oluşturulan olayları arayarak, uygulama Defender ile ilgili bilgileri gözden geçirebilirsiniz.

- **Bilgisayarlar temizlenmeden önce bir sistem geri yükleme noktası oluştur**  
  - **Evet** (*varsayılan*)
  - **Hayır**
  - **Yapılandırılmadı**

- **Algılanan tehditler için Eylemler**  
  CSP: [Threatseveritydefaultaction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Kötü amaçlı yazılımın tehdit düzeyine bağlı olarak algılanan kötü amaçlı yazılım için Defender 'ın aldığı eylemi belirtin.
  
  Defender, algıladığı kötü amaçlı yazılımları aşağıdaki önem düzeylerinden biri olarak sınıflandırır:
  - **Düşük tehdit**
  - **Orta tehdit**
  - **Yüksek tehdit**
  - **Ciddi tehdit**

  Her düzey için gerçekleştirilecek eylemi belirtin. Her önem düzeyi için varsayılan değer *Yapılandırılmadı*.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Temizle** -hizmet, dosyaları kurtarmaya çalışır ve bulaşmaya çalışabilir.
  - **Karantina** -dosyaları karantinaya alma.
  - **Remove** -dosyaları cihazdan kaldırır.
  - **Allow** -dosyaya izin verir ve başka eylemler almaz.
  - **Kullanıcı tanımlı** -cihaz kullanıcısı hangi eylemin ele alınacağı kararını yapar.
  - **Blok** -dosya yürütmeyi engeller.

## <a name="scan"></a>Tarama

- **Arşiv dosyalarını tara**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Defender 'ı ZIP veya CAB dosyaları gibi arşiv dosyalarını tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar, arşivlenen dosyaları taramak için istemci varsayılan değerini döndürür, ancak Kullanıcı taramayı devre dışı bırakabilir.
Daha fazla bilgi edinin
  - **İzin verilmiyor** Arşivlenmiş dosyalardaki taramayı kapatır.
  - **İzin verilen.** Arşiv dosyalarını tarar.

- **Zamanlanan Taramalar için düşük CPU önceliğini etkinleştir**  
  CSP: [Enablelowcpupriınıd](https://go.microsoft.com/fwlink/?linkid=2113944)

  Zamanlanan Taramalar için CPU önceliğini yapılandırın.
  - **Yapılandırılmadı** (*varsayılan*)-ayar, CPU önceliğinde hiçbir değişiklik yapılmamakta sistem varsayılan değerini döndürür.
  - **Devre dışı**
  - **Etkin**

- **Yakalama tam taramasını devre dışı bırak**  
  CSP: [Disablecatch Upfullscan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Zamanlanan tam taramalar için yakalama taramaları yapılandırın. Bir yakalama taraması, düzenli olarak zamanlanmış bir tarama kaçırıldığı için başlayan bir taramadır. Bilgisayar zamanlanan saatte kapatılmış olduğundan, genellikle bu zamanlanmış taramalar kaçırıldı.

  - **Yapılandırılmadı** (*varsayılan*)-ayar, istemci Varsayılanı ' na döndürülür, bu, tam taramalar için yakala taramaların etkinleştirilmesi anlamına gelir, ancak kullanıcı bunları kapatabilir.
  - **Devre dışı**
  - **Etkin**

- **Yakalama hızlı taramayı devre dışı bırak**  
  CSP: [Disablecatchupquickscan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Zamanlanan hızlı taramalar için yakalama taramaları yapılandırın. Bir yakalama taraması, düzenli olarak zamanlanmış bir tarama kaçırıldığı için başlayan bir taramadır. Bilgisayar zamanlanan saatte kapatılmış olduğundan, genellikle bu zamanlanmış taramalar kaçırıldı.

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar, istemci Varsayılanı ' na döndürülür, bu da yakalama hızlı taramaların etkinleştirilmesi, ancak kullanıcı bunları kapatabilir.
  - **Devre dışı**
  - **Etkin**

- **Tarama başına CPU kullanım sınırı (yüzde 0-100)**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Defender taraması için Ortalama CPU yükleme faktörü olan 0 ile 100 arasında bir yüzde olarak belirtin.

- **Tam tarama sırasında eşlenmiş ağ sürücülerinin taranmasını etkinleştir**  
  CSP: [Allowfullscanonmappednetworkdrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Defender 'ı eşlenmiş ağ sürücülerine tarayacak şekilde yapılandırın.

  - **Yapılandırılmadı** (*varsayılan*)-ayar, eşlenen ağ sürücülerinde taramayı devre dışı bırakan sistem varsayılan ayarlarına geri yüklenir.
  - **İzin verilmiyor.** Eşlenen ağ sürücülerinde taramayı devre dışı bırakır.
  - **İzin verilen.** Eşlenen ağ sürücülerinizi tarar.

- **Günlük hızlı taramayı şurada Çalıştır:**  
  CSP: [Schedulequickscantime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Defender hızlı taramanın çalışacağı günün saatini seçin.
  Varsayılan olarak, bu seçenek **yapılandırılmaz**

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
  - **Devre dışı**
  - **Etkin**

- **Zamanlanmış taramayı ve güvenlik zekası güncelleştirme başlangıç zamanlarını rastgele yap**  
  -**Yapılandırılmadı** (*varsayılan*)-**Evet** 
  - **Hayır**

- **Tam tarama sırasında çıkarılabilir sürücüleri Tara**
  - **Yapılandırılmadı** (*varsayılan*)
  - **İzin verilmiyor.** Çıkarılabilir sürücülerde taramayı kapatır.
  - **İzin verilen.** Çıkarılabilir sürücüleri tarar.

## <a name="updates"></a>Güncelleştirmeler

- **Güvenlik Zekası güncelleştirmelerini denetleme sıklığını (0-24 saat) girin**  
  CSP: [Signatureupdateınterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  İmzaları denetlemek için kullanılan aralığı sıfır ile 24 arasında (saat cinsinden) belirtin. Sıfır değeri, yeni imzalar için denetim yok sonucunu vermez. 2 değeri her iki saatte bir denetlenir ve bu şekilde devam eder.

- **İmza güncelleştirme geri dönüş sırası (cihaz)**

- **İmza güncelleştirme dosya paylaşımları kaynakları (cihaz)**

- **Güvenlik Zekası konumu (cihaz)**  

## <a name="user-experience"></a>Kullanıcı deneyimi

- **Microsoft Defender uygulamasına Kullanıcı erişimini engelleyin**  
  - **Yapılandırılmadı** (*varsayılan*)
  - **İzin verilmiyor.** Kullanıcıların Kullanıcı arabirimine erişimini engeller.
  - **İzin verilen.** Kullanıcıların Kullanıcı arabirimine erişmesine izin verir.

- **Kullanıcının tam tarama çalıştırması, güvenlik zekasını güncelleştirmesi veya Windows Defender 'ı çevrimdışı çalıştırması gerektiğinde istemci bilgisayarda bildirim iletilerini göster**  
  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**
  - **Hayır**

- **İstemci kullanıcı arabirimini devre dışı bırak**  
  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**
  - **Hayır**

- **Kullanıcıların tüm geçmiş sonuçlarını görüntülemesine izin ver**
  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**
  - **Hayır**