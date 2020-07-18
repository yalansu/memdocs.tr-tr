---
title: Intune Endpoint Security saldırı yüzeyi azaltma ayarları | Microsoft Docs
description: Uç nokta güvenliği saldırı yüzeyi Azaltma ilkesi ayarları Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: 3ebca81f459f0e49345db08f992c288514a7331a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461615"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Intune 'da Endpoint Security için saldırı yüzeyi Azaltma ilkesi ayarları

[Endpoint Security ilkesinin](../protect/endpoint-security-policy.md)bir parçası olarak Intune 'un uç nokta güvenlik düğümündeki *saldırı yüzeyi azaltma* ilkesi için profillerde yapılandırabileceğiniz ayarları görüntüleyin.

Desteklenen platformlar ve profiller:

- **Windows 10 ve üzeri**:
  - Profil: **uygulama ve tarayıcı yalıtımı**
  - Profil: **Web koruması**
  - Profil: **uygulama denetimi**
  - Profil: **saldırı yüzeyi azaltma kuralları**
  - Profil: **cihaz denetimi**
  - Profil: **Exploit Protection**

## <a name="app-and-browser-isolation-profile"></a>Uygulama ve tarayıcı yalıtımı profili

### <a name="app-and-browser-isolation"></a>Uygulama ve tarayıcı yalıtımı

- **Edge için Application Guard 'ı açma (Seçenekler)**  
  CSP: [Allowwindowssavunma Derapplicationguard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Yapılandırılmadı** (*varsayılan*)
  - **Edge Için etkinleştirilen** -Application Guard, onaylanmamış siteleri bir Hyper-V sanallaştırılmış gözatma kapsayıcısında açar.

  *Edge Için etkin*olarak ayarlandığında, aşağıdaki ayarlar kullanılabilir:
  
  - **Pano davranışı**  
    CSP: [Clipboardsettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Yerel bılgısayar ve Application Guard sanal tarayıcısından hangi kopyalama ve yapıştırma eylemlerine izin verileceğini seçin.
    - **Yapılandırılmadı** (*varsayılan*)
    - **BILGISAYAR ve tarayıcı arasında kopyalama ve yapıştırmayı engelle**
    - **Tarayıcıdan yalnızca BILGISAYARA kopyalama ve yapıştırmaya izin ver**
    - **BILGISAYARDAN yalnızca tarayıcıya kopyalama ve yapıştırmaya izin ver**
    - **BILGISAYAR ve tarayıcı arasında kopyalama ve yapıştırmaya izin ver**

  - **Kurumsal olmayan onaylanan sitelerden dış içeriği engelle**  
    CSP: [blok olmayan içerik](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -onaylanmamış Web sitelerinden içerik yüklemeyi engelleyin.

  - **Application Guard gözatma oturumunda oluşan olaylar için günlükleri toplayın**  
    CSP: [Auditapplicationguard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -bir Application Guard sanal gözatma oturumu içinde oluşan olaylar için günlükleri toplayın.

  - **Kullanıcı tarafından oluşturulan tarayıcı verilerinin kaydedilmesine izin ver**  
    CSP: [Allowkalıcılığı](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -bir Application Guard sanal gözatma oturumu sırasında oluşturulan kullanıcı verilerinin kaydedilmesine izin verin. Parola, Sık Kullanılanlar ve tanımlama bilgilerini içeren kullanıcı verilerine örnek olarak verilebilir.

  - **Donanım grafik hızlandırmasını etkinleştir**  
    CSP: [Allowvirtualgpu](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -Application Guard sanal gözatma oturumu içinde grafik yoğun Web sitelerini daha hızlı yüklemek için bir sanal grafik işleme birimi kullanın.

  - **Kullanıcıların Konak üzerine dosya indirmesine izin ver**  
    CSP: [Savefilestohost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -kullanıcıların sanallaştırılmış tarayıcıdan konak işletim sistemine dosya indirmesine izin verin.

- **Application Guard Yerel yazıcılara yazdırmaya izin ver**  

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -Yerel yazıcılara yazdırmaya izin ver.

- **Application Guard ağ yazıcılarına yazdırmaya izin ver**  

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -yazdırma yazdırma ağ yazıcılarına izin ver.

- **Application Guard PDF 'ye yazdırmaya izin ver**  

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**-PDF 'ye yazdırma yazdırmaya izin ver.

- **Application Guard XPS 'ye yazdırmaya izin ver**  

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** --yazdırma yazdırmaya izin ver.

- **Windows ağ yalıtımı ilkesi**  
  
  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -Windows ağ yalıtımı ilkesini yapılandırın.  
  
  *Evet*olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz.

  - **IP aralıkları**  
    Açılan listeyi genişletin, **Ekle**' yi seçin ve daha sonra bir *daha* daha daha sonra bir *üst*adres belirtin.

  - **Bulut kaynakları**  
    Açılan menüyü genişletin, **Ekle**' yi seçin ve bir *IP adresi veya FQDN* ve *proxy*belirtin.

  - **Ağ etki alanları**  
   Açılan listeyi genişletin, **Ekle**' yi seçin ve *ağ etki alanlarını*belirtin.

  - **Ara sunucular**  
    Açılan listeyi genişletin, **Ekle**' yi seçin ve *proxy sunucuları*' nı belirtin.

  - **İç proxy sunucular**  
    Açılan listeyi genişletin, **Ekle**' yi seçin ve ardından *iç proxy sunucuları*' nı belirtin.

  - **Nötr kaynaklar**  
    Açılan menüyü genişletin, **Ekle**' yi seçin ve ardından *nötr kaynaklar*' ı belirtin.

  - **Diğer kurumsal ara sunucu sunucularının otomatik algılanmasını devre dışı bırak**  
    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -diğer kurumsal ara sunucu sunucularının otomatik algılanmasını devre dışı bırakın.

  - **Diğer kurumsal IP aralıklarının otomatik algılanmasını devre dışı bırak**  
    - **Yapılandırılmadı** (*varsayılan*)
    - **Evet** -DIĞER kurumsal IP aralıklarının otomatik algılanmasını devre dışı bırakın.

## <a name="web-protection-profile"></a>Web koruması profili

### <a name="web-protection"></a>Web koruması

- **Ağ korumasını etkinleştir**  
  CSP: [Enablenetworkprotection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, devre dışı bırakılan Windows varsayılan öğesine geri döner.
  - **Kullanıcı tanımlı**
  - **Etkinleştir** -ağ koruması, sistemdeki tüm kullanıcılar için etkinleştirilmiştir.
  - **Denetim modu** -kullanıcılar tehlikeli etki alanlarından engellenmez ve bunun yerine Windows olayları tetiklenir.

- **Microsoft Edge için SmartScreen gerektir**  
  CSP: [tarayıcı/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Evet** -kullanıcıları olası kimlik avı dolandırıcılarından ve kötü amaçlı yazılımlardan korumak için SmartScreen kullanın.
  - **Yapılandırılmadı** (*varsayılan*)

- **Kötü amaçlı Site erişimini engelleyin**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Evet** -kullanıcıların Microsoft Defender SmartScreen Filtresi uyarılarını yoksaymasını ve siteye gitmesini engelleyin.
  - **Yapılandırılmadı** (*varsayılan*)

- **Doğrulanmamış dosya indirmeyi engelle**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Evet** -kullanıcıların Microsoft Defender SmartScreen Filtresi uyarılarını yok saymasını engelleyin ve doğrulanmamış dosyaları indirmelerini engelleyin.
  - **Yapılandırılmadı** (*varsayılan*)

## <a name="application-control-profile"></a>Uygulama denetim profili

### <a name="microsoft-defender-application-control"></a>Microsoft Defender uygulama denetimi

- **Uygulama dolabı uygulama denetimi**  
  - **Yapılandırılmadı** (*varsayılan*)
  - **Bileşenleri zorlama ve uygulamaları depolama**
  - **Bileşenleri denetleme ve uygulamaları depolama**
  - **Bileşenleri zorlama, Mağaza uygulamaları ve akıllı dolap**
  - **Denetim bileşenleri, Mağaza uygulamaları ve akıllı dolap**

- **Kullanıcıların SmartScreen uyarılarını yoksaymalarını engelleyin**  
  [PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Yapılandırılmadı** (*varsayılan*)-kullanıcılar, dosyalar ve kötü amaçlı uygulamalar için SmartScreen uyarılarını yok sayabilir.
  - **Evet** -SmartScreen etkin ve kullanıcılar dosyalar veya kötü amaçlı uygulamalar için uyarıları atlayamaz.

- **Windows SmartScreen 'i açma**  
  CSP: [SmartScreen/Enablesmartscreenınshell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Yapılandırılmadı** (*varsayılan*)-ayarı, SmartScreen 'i etkinleştirmek için Windows varsayılan olarak döndürür, ancak kullanıcılar bu ayarı değiştirebilir. SmartScreen 'i devre dışı bırakmak için özel bir URI kullanın.
  - **Evet** -tüm kullanıcılar için SmartScreen kullanımını zorunlu kıl.

## <a name="attack-surface-reduction-rules-profile"></a>Saldırı yüzeyi azaltma kuralları profili

### <a name="attack-surface-reduction-rules"></a>Saldırı yüzeyi azaltma kuralları

- **Windows yerel güvenlik yetkilisi alt sisteminden kimlik bilgisi çalınmasını engelle (lsass.exe)**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874499)

  Bu saldırı yüzeyi azaltma (ASR) kuralı şu GUID aracılığıyla denetlenir: 9e6c4e1f-7d60-472F-ba1a-a39ef669e4b2
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Kullanıcı tanımlı**
  - **Etkinleştir** -lsass.exe aracılığıyla kimlik bilgilerini çalmaya çalışır.
  - **Denetim modu** -kullanıcılar tehlikeli etki alanlarından engellenmez ve bunun yerine Windows olayları tetiklenir.

- **Adobe Reader 'ın alt işlem oluşturmasını engelleyin**  
  [Saldırı yüzeyi azaltma kurallarıyla saldırı yüzeylerini azaltma](https://go.microsoft.com/fwlink/?linkid=853979)
  
  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 7674ba52-37eb-4a4f-A9A1-f0f9a1619a2c
  - **Yapılandırılmadı** (*varsayılan*)-Windows varsayılanı geri yüklendi, alt işlemlerin oluşturulmasını engellemez.
  - **Kullanıcı tanımlı**
  - **Etkinleştir** -Adobe Reader 'ın alt işlem oluşturması engellenir.
  - **Denetim modu** -Windows olayları, alt işlemlerin engellenmesi yerine oluşturulur.

- **Office uygulamalarının ekleme koddan diğer işlemlere engel**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872974)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Block** -Office uygulamalarının diğer işlemlere ekleme kodu engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Office uygulamalarının yürütülebilir içerik oluşturmasını engelleyin**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872975)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Blok** -ofis uygulamalarının yürütülebilir içerik oluşturması engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Tüm Office uygulamalarının alt işlem oluşturmasını engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872976)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Blok** -Office uygulamalarının alt işlem oluşturması engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Office makrolarından Win32 API çağrıları engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872977)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Engelle** -Office makrosunda Win32 API çağrıları kullanılması engellenmiştir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Office iletişim uygulamalarının alt işlem oluşturmasını engelleyin**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874499)  

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Yapılandırılmadı** (*varsayılan*)-Windows varsayılanı geri yüklenir, bu, alt işlemlerin oluşturulmasını engellemez.
  - **Kullanıcı tanımlı**
  - **Etkinleştir** -Office iletişim uygulamalarının alt işlem oluşturması engellenir.
  - **Denetim modu** -Windows olayları, alt işlemlerin engellenmesi yerine oluşturulur.

- **Büyük olasılıkla karıştırılmış betiklerin yürütülmesini engelle (js/vbs/PS)**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872978)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Blok** -Defender, karıştırılmış betiklerin yürütülmesini engeller.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **JavaScript veya VBScript 'in indirilen yürütülebilir içeriği başlatmasını engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872979)

   Bu ASR kuralı şu GUID aracılığıyla denetlenir: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Engelleme** -Defender, Internet 'Ten indirilen JavaScript veya VBScript dosyalarını yürütülmesini engeller.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **PSExec ve WMI komutlarından kaynaklanan işlem oluşturma işlemlerini engelleyin**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874500)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: d1e49aac-8F56-4280-b9ba-993a6d77406c
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Block** -PSExec veya WMI komutları tarafından işlem oluşturma engellendi.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **USB 'den çalıştırılan güvenilmeyen ve imzasız işlemlerin engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874502)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: b2b3f03d-6A65-4F7B-a9c7-1c7ef74a9ba4
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Engelleme** -GÜVENILMEYEN ve USB sürücüsünden çalıştırılan imzasız süreçler engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Bir Preter, Age veya güvenilir liste ölçütlerine uymadıkları takdirde yürütülebilir dosyaların çalıştırılmasını engelleyin**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874503)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 01443614-CD74-433a-b99e-2ecdc07bfc25e
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Block**
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **E-posta ve Web postasından istemcilerinden yürütülebilir içerik indirmeyi engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Engelleme** -e-posta ve web postası istemcilerinden indirilen yürütülebilir içerik engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Fidye yazılımı ile gelişmiş koruma kullan**  
   [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874504)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Yapılandırılmadı** (*varsayılan*)-ayar, kapalı olan Windows varsayılan öğesine geri döner.
  - **Kullanıcı tanımlı**
  - **Etkinleştirme**
  - **Denetim modu** --Windows olayları engelleme yerine oluşturulur.

- **Klasör korumasını etkinleştir**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar, okuma veya yazma işlemleri engellenmeyen varsayılan değerini döndürür.
  - **Enable** -güvenilmeyen uygulamalar Için, Defender blokları korumalı klasörlerdeki dosyaları değiştirmeye veya silmeye veya disk sektörlerine yazmaya çalışır. Defender hangi uygulamalara güvenildiğini otomatik olarak belirler. Alternatif olarak, kendi güvenilir uygulamalar listenizi de tanımlayabilirsiniz.
  - **Denetim modu** -güvenilmeyen uygulamalar denetimli klasörlere erişirken, ancak hiçbir blok zorlanmadığında Windows olayları tetiklenir.
  - **Disk değişikliğini engelle** -yalnızca disk sektörlerine yazma denemeleri engellenir.
  - **Disk değişikliğini denetleme** -Windows olayları, disk sektörlerine yazma girişimlerini engelleme yerine getirilir.
  
- **Dosya ve yolları saldırı yüzeyi azaltma kurallarından çıkar**  
  CSP: [Ksurfacereductiononlydışlamalar](https://go.microsoft.com/fwlink/?linkid=872981)

  Açılır menüyü genişletin ve ardından **Ekle** ' yi seçerek saldırı yüzeyi azaltma kurallarından dışlanacak bir dosya veya klasörün **yolunu** tanımlayın.

## <a name="device-control-profile"></a>Cihaz denetimi profili

### <a name="device-control"></a>Cihaz denetimi

- **Cihaz tanımlayıcılarına göre donanım cihazı yüklemesi**  
  [Preventınstald Matchingdevicıdıd](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Bu ayar, Windows 'un yüklemesi engellenen cihazlara yönelik Tak ve Kullan donanım kimliklerinin ve uyumlu kimliklerin bir listesini belirtmenizi sağlar. Bu ilke ayarı, Windows 'un bir cihaz yüklemesine izin veren diğer tüm ilke ayarlarından önceliklidir.  Uzak Masaüstü sunucusunda bu ilke ayarını etkinleştirirseniz, ilke ayarı, belirtilen cihazların uzak masaüstü istemcisinden uzak masaüstü sunucusuna yönlendirilmesini etkiler.

  - **Yapılandırılmadı**
  - **Donanım cihazı yüklemeye Izin ver** -cihazların izin verilen veya engellenen şekilde diğer ilke ayarları tarafından yüklenip güncelleştirilemeyebilir.
  - **Donanım cihazını yüklemeyi engelle** (*varsayılan*)-Windows 'un, sizin TANıMLADıĞıNıZ bir listede donanım kimliği veya uyumlu kimliği görünen bir cihaz yüklemesi engellenir.

  *Donanım aygıtı yüklemesini engelle* olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:

  - **Eşleşen donanım cihazlarını kaldırma**

    Bu ayar yalnızca *cihaz tanımlayıcılarına göre donanım cihaz yüklemesi* , *donanım cihazı yüklemeyi engelleyecek*şekilde ayarlandığında kullanılabilir.
    - **Evet**
    - **Yapılandırılmadı**

  - **Engellenen donanım cihaz tanımlayıcıları**  

    Bu ayar yalnızca *cihaz tanımlayıcılarına göre donanım cihaz yüklemesi* , *donanım cihazı yüklemeyi engelleyecek*şekilde ayarlandığında kullanılabilir.

    **Ekle**' yi seçin ve ardından engellemek istediğiniz donanım cihaz tanımlayıcısını belirtin.

- **Kurulum sınıflarına göre donanım cihaz yüklemesi**  
  CSP: [Deviceınstallation/Allowwinstallationofmatchingdevicesetupclasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Bu ilke ayarı, Windows 'un yüklemesi engellenen cihaz sürücüleri için cihaz kurulum sınıfının genel benzersiz tanımlayıcıları (GUID 'Ler) listesini belirtmenizi sağlar. Bu ilke ayarı, Windows 'un bir cihaz yüklemesine izin veren diğer tüm ilke ayarlarından önceliklidir. Uzak Masaüstü sunucusunda bu ilke ayarını etkinleştirirseniz, ilke ayarı, belirtilen cihazların uzak masaüstü istemcisinden uzak masaüstü sunucusuna yönlendirilmesini etkiler.

  - **Yapılandırılmadı**
  - **Donanım cihazı yüklemeye Izin ver** -Windows, diğer ilke ayarları tarafından izin verilen veya engellenen cihazları yükleyebilir ve güncelleştirebilir.
  - **Donanım cihazını yüklemeyi engelle** (*varsayılan*)-Windows 'un, kurulum sınıfı GUID 'leri tanımladığınız bir listede göründüğü bir cihaz yüklemesi engellenir.

  *Donanım cihazını yüklemeyi engelle* olarak ayarlandığında, *eşleşen donanım cihazlarını* ve *Engellenen donanım cihaz tanımlayıcılarını*Kaldır ' a göre yapılandırma yapabilirsiniz.

  - **Eşleşen donanım cihazlarını kaldırma**

    Bu ayar yalnızca *cihaz tanımlayıcılarına göre donanım cihaz yüklemesi* , *donanım cihazı yüklemeyi engelleyecek*şekilde ayarlandığında kullanılabilir.
    - **Evet**
    - **Yapılandırılmadı**

  - **Engellenen donanım cihaz tanımlayıcıları**

    Bu ayar yalnızca *cihaz tanımlayıcılarına göre donanım cihaz yüklemesi* , *donanım cihazı yüklemeyi engelleyecek*şekilde ayarlandığında kullanılabilir.

    **Ekle**' yi seçin ve ardından engellemek istediğiniz donanım cihaz tanımlayıcısını belirtin.

- **Tam tarama sırasında çıkarılabilir sürücüleri Tara**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Yapılandırılmadı** (*varsayılan*)-Bu ayar, çıkarılabilir sürücüleri tarayan, ancak kullanıcı bu taramayı devre dışı bırakabilen istemci varsayılan değerini döndürür.
  - **Evet** -tam tarama sırasında, çıkarılabilir sürücüler (USB flash sürücüler gibi) taranır.

- **Doğrudan bellek erişimini engelle**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)

  Bu ilke ayarı yalnızca BitLocker veya cihaz şifrelemesi etkinleştirildiğinde zorlanır.

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -Kullanıcı Windows 'a oturum açana kadar, tüm ETKIN takılabilir PCI akış bağlantı noktaları için doğrudan bellek ERIŞIMINI (DMA) engelleyin. Kullanıcı oturum açtıktan sonra, Windows, ana bilgisayar eklentisi PCI bağlantı noktalarına bağlı PCI cihazlarını numaralandırır. Kullanıcı makineyi her kilitlediğinde, Kullanıcı yeniden oturum açana kadar alt cihazları olmayan hot plug PCI bağlantı noktalarında DMA engellenir. Makine kilidi açıldığında zaten numaralandırılan cihazlar, söküle kadar çalışmaya devam eder.

- **Çekirdek DMA koruması ile uyumsuz dış cihazların numaralandırması**  
  CSP: [Dmaguard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Bu ilke, dış DMA özellikli cihazlara karşı ek güvenlik sağlayabilir. DMA yeniden eşleme/cihaz belleği yalıtımı ve korumalı alana alma ile uyumsuz olan dış DMA özellikli cihazların numaralandırılması üzerinde daha fazla denetim sağlar.

  Bu ilke, yalnızca çekirdek DMA koruması desteklenirken ve Sistem bellenimi tarafından etkinleştirildiğinde devreye girer. Çekirdek DMA koruması, üretim sırasında sistem tarafından desteklenmesi gereken bir platform özelliğidir. Sistemin çekirdek DMA korumasını destekleyip desteklemediğini denetlemek için MSINFO32.exe Özet sayfasındaki çekirdek DMA koruması alanını denetleyin.

  - **Yapılandırılmadı** -(*varsayılan*)
  - **Tümünü engelle**
  - **Tümüne izin ver**

- **Bluetooth bağlantılarını engelle**  
  CSP: [Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -cihaza ve cihazdan Bluetooth bağlantılarını engelleyin.

- **Bluetooth bulunabilirliği engelle**  
  CSP: [Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -cihazın diğer Bluetooth özellikli cihazlar tarafından keşfedilmesini önler.

- **Bluetooth ön eşleştirmesini engelle**  
  CSP: [Bluetooth/Allowpreeşleştirmeyi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -belirli Bluetooth cihazlarının konak cihazla otomatik olarak eşleştirilmesini önler.

- **Bluetooth Advertising 'i engelle**  
  CSP: [Bluetooth/AllowAdvertising](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -cihazın Bluetooth tanıtımları göndermesini engeller.  

- **Bluetooth proxden bağlantıyı engelle**  
  CSP: [Bluetooth/AllowPromptedProximalConnections](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections) , kullanıcıların Swift çiftini ve diğer yakınlık tabanlı senaryoları kullanmasını engeller

  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet** -bir cihaz kullanıcısının Swift çiftini ve diğer yakınlık tabanlı senaryoları kullanmasını önler.  

  [Bluetooth/AllowPromptedProximalConnections CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Bluetooth izin verilen hizmetler**  
  CSP: [Bluetooth/ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist).  
  Hizmet listesi hakkında daha fazla bilgi için bkz. [Servicesallowedlist kullanım kılavuzu](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide)

  - **Ek** olarak Izin verilen Bluetooth hizmetleri ve profillerini, gibi onaltılı dizeler olarak belirtin `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}` .
  - **Içeri aktarma** -Bluetooth hizmetleri ve profillerinin bir listesini içeren bir. csv dosyasını, örneğin`{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`

## <a name="exploit-protection-profile"></a>Exploit Protection profili

### <a name="exploit-protection"></a>Exploit protection

- **XML 'yi karşıya yükle**  
  CSP: [Patıprotectionsettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  BT yöneticisinin, kuruluştaki tüm cihazlara istenen sistem ve uygulama azaltma seçeneklerini temsil eden bir yapılandırma gönderebilmesini sağlar. Yapılandırma bir XML dosyası tarafından temsil edilir. Yararlanma koruması, cihazları yaymak ve bulaşma için kötüye kullanılan kötü amaçlı yazılımlardan korumaya yardımcı olabilir. Windows güvenlik uygulamasını veya PowerShell 'i kullanarak bir azaltma kümesi (yapılandırma olarak bilinir) oluşturabilirsiniz. Daha sonra bu yapılandırmayı bir XML dosyası olarak dışarı aktarabilir ve ağınızdaki birden fazla makineyle paylaşarak, hepsi aynı azaltma ayarları kümesine sahip olurlar. Ayrıca, var olan bir EMET yapılandırma XML dosyasını bir Exploit Protection yapılandırması XML dosyasına dönüştürebilir ve içeri aktarabilirsiniz.

  **XML dosyası seç**' i SEÇIN, XML filet karşıya yüklemeyi belirtin ve ardından **Seç**' e tıklayın.
  - **Yapılandırılmadı** (*varsayılan*)
  - **Evet**

- **Kullanıcıların Exploit Guard Koruma arabirimini düzenlemesini engelle**  
  CSP: [Disallowpatıprotectionoverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Yapılandırılmadı** (*varsayılan*)-yerel kullanıcılar, açıktan yararlanma koruması ayarları alanında değişiklik yapabilirler.
  - **Evet** -kullanıcıların Microsoft Defender Güvenlik Merkezi 'ndeki yararlanma koruması ayarları alanında değişiklik yapmasını engelleyin.

## <a name="next-steps"></a>Sonraki adımlar

[ASR için uç nokta güvenlik ilkesi](../protect/endpoint-security-asr-policy.md)
