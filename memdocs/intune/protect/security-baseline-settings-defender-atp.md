---
title: Microsoft Defender Gelişmiş tehdit koruması için Intune güvenlik temelleri ayarları
titleSuffix: Microsoft Intune
description: Microsoft Defender Gelişmiş tehdit koruması 'nı yönetmek için Intune tarafından desteklenen güvenlik taban çizgisi ayarları
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/22/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: a91a15bde690840f81a6895baf3724fcde173003
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91008371"
---
<!-- Pivots in use: 

September 2020 v5
::: zone pivot="atp-sept-2020"
::: zone-end

::: zone pivot="atp-april-2020,atp-sept-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"
::: zone-end

April 2020 v4
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end

March 2020 v3
::: zone pivot="atp-march-2020"
::: zone-end

-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Intune için Microsoft Defender Gelişmiş tehdit koruması temel ayarları

Microsoft Intune tarafından desteklenen Microsoft Defender Gelişmiş tehdit koruması taban çizgisi ayarlarını görüntüleyin. Gelişmiş tehdit koruması (ATP) taban çizgisi Varsayılanları, ATP için önerilen yapılandırmayı temsil eder ve diğer güvenlik temelleri için temel varsayılanlarla eşleşmeyebilir.

::: zone pivot="atp-sept-2020"

**Eylül 2020 için Microsoft Defender ATP temeli-sürüm 5**  
Güvenlik temelinin bu sürümü önceki sürümlerin yerini alır. Bu temel sürümün kullanılabilirliğine önce oluşturulan profiller:

- Artık salt okunurdur. Bu profilleri kullanmaya devam edebilirsiniz, ancak yapılandırmalarını değiştirecek şekilde düzenleyemezsiniz.
- En son sürüme güncelleştirilebilen olabilir. Geçerli temel sürümü güncelleştirdikten sonra ayarları değiştirmek için profili düzenleyebilirsiniz.

Önceki sürümlerden taban çizgisinin bu sürümü ile nelerin değiştirildiğini anlamak için, bu taban çizgisi için *sürümler* bölmesi görüntülenirken kullanılabilen [temelleri Karşılaştır](../protect/security-baselines.md#compare-baseline-versions) eylemini kullanın. Görüntülemek istediğiniz taban çizgisinin sürümünü seçtiğinizden emin olun.

Bir güvenlik temeli profilini Bu taban çizgisinin en son sürümüne güncelleştirmek için, bkz. [bir profil için temel sürümü değiştirme](../protect/security-baselines.md#change-the-baseline-version-for-a-profile).


::: zone-end
::: zone pivot="atp-april-2020"

**Nisan 2020 için Microsoft Defender ATP temeli-sürüm 4**  
Güvenlik temelinin bu sürümü önceki sürümlerin yerini alır. Bu temel sürümün kullanılabilirliğine önce oluşturulan profiller:

- Artık salt okunurdur. Bu profilleri kullanmaya devam edebilirsiniz, ancak yapılandırmalarını değiştirecek şekilde düzenleyemezsiniz.
- En son sürüme güncelleştirilebilen olabilir. Geçerli temel sürümü güncelleştirdikten sonra ayarları değiştirmek için profili düzenleyebilirsiniz.

Önceki sürümlerden taban çizgisinin bu sürümü ile nelerin değiştirildiğini anlamak için, bu taban çizgisi için *sürümler* bölmesi görüntülenirken kullanılabilen [temelleri Karşılaştır](../protect/security-baselines.md#compare-baseline-versions) eylemini kullanın. Görüntülemek istediğiniz taban çizgisinin sürümünü seçtiğinizden emin olun.

Bir güvenlik temeli profilini Bu taban çizgisinin en son sürümüne güncelleştirmek için, bkz. [bir profil için temel sürümü değiştirme](../protect/security-baselines.md#change-the-baseline-version-for-a-profile).

::: zone-end
::: zone pivot="atp-march-2020"

**Mart 2020 için Microsoft Defender ATP temeli-sürüm 3**  
Güvenlik temelinin bu sürümü önceki sürümlerin yerini alır. Bu temel sürümün kullanılabilirliğine önce oluşturulan profiller:


- Artık salt okunurdur. Bu profilleri kullanmaya devam edebilirsiniz, ancak yapılandırmalarını değiştirecek şekilde düzenleyemezsiniz.
- En son sürüme güncelleştirilebilen olabilir. Geçerli temel sürümü güncelleştirdikten sonra ayarları değiştirmek için profili düzenleyebilirsiniz.

Önceki sürümlerden taban çizgisinin bu sürümü ile nelerin değiştirildiğini anlamak için, bu taban çizgisi için *sürümler* bölmesi görüntülenirken kullanılabilen [temelleri Karşılaştır](../protect/security-baselines.md#compare-baseline-versions) eylemini kullanın. Görüntülemek istediğiniz taban çizgisinin sürümünü seçtiğinizden emin olun.

Bir güvenlik temeli profilini Bu taban çizgisinin en son sürümüne güncelleştirmek için, bkz. [bir profil için temel sürümü değiştirme](../protect/security-baselines.md#change-the-baseline-version-for-a-profile).

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

Microsoft Defender Gelişmiş tehdit koruması temeli, ortamınız [Microsoft Defender Gelişmiş tehdit koruması](advanced-threat-protection.md#prerequisites)kullanımı için önkoşulları karşılıyorsa kullanılabilir.

Bu taban çizgisi fiziksel cihazlar için iyileştirilmiştir ve sanal makinelerde (VM) veya VDı uç noktalarında kullanılması önerilmez. Belirli taban çizgisi ayarları, sanallaştırılmış ortamlarda uzak etkileşimli oturumları etkileyebilir. Daha fazla bilgi için bkz. Windows belgelerindeki [Microsoft Defender ATP güvenlik temeliyle uyumluluğu artırma](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) .

::: zone-end
::: zone pivot="atp-sept-2020"

## <a name="attack-surface-reduction-rules"></a>Saldırı yüzeyi azaltma kuralları

- **Office iletişim uygulamalarının alt işlem oluşturmasını engelleyin**  
  ASR kuralı: [26190899-1602-49e8-8b27-eb1d0a1ce869](https://go.microsoft.com/fwlink/?linkid=874499)

  - **Etkinleştir** *(varsayılan)* -Office iletişim uygulamalarının alt işlem oluşturması engellenir.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Kullanıcı tanımlı**
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Adobe Reader 'ın alt işlem oluşturmasını engelleyin**  
  ASR kuralı: [7674ba52-37eb-4a4f-A9A1-f0f9a1619a2c](https://go.microsoft.com/fwlink/?linkid=853979)

  - **Etkinleştir** *(varsayılan)* -Adobe okuyucunun alt işlem oluşturması engellenir.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Kullanıcı tanımlı**
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Office uygulamalarının ekleme koddan diğer işlemlere engel**  
  ASR kuralı: [75668C1f-73b5-4CF0-bb93-3ecf5cb7cc84](https://go.microsoft.com/fwlink/?linkid=872974)

  - **Engelle** *(varsayılan)* -Office uygulamalarının ekleme kodu diğer işlemlere engellenir.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Office uygulamalarının yürütülebilir içerik oluşturmasını engelleyin**  
  ASR kuralı: [3B576869-A4EC-4529-8536-B80A7769E899](https://go.microsoft.com/fwlink/?linkid=872975)

  - **Engelle** *(varsayılan)* -Office uygulamalarının yürütülebilir içerik oluşturmasına izin verilmez.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **JavaScript veya VBScript 'in indirilen yürütülebilir içeriği başlatmasını engelle**  
  ASR kuralı: [D3E037E1-3EB8-44C8-A917-57927947596D](https://go.microsoft.com/fwlink/?linkid=872979)

  - **Engelle** *(varsayılan)*
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Ağ korumasını etkinleştir**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=3D872618)

  - **Etkinleştir** *(varsayılan)*
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Kullanıcı tanımlı**
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **USB 'den çalıştırılan güvenilmeyen ve imzasız işlemlerin engelle**  
  ASR kuralı: [b2b3f03d-6A65-4F7B-a9c7-1c7ef74a9ba4](https://go.microsoft.com/fwlink/?linkid=)

  - **Engelle** *(varsayılan)* -USB sürücüsünden yürütülen güvenilmeyen/imzasız süreçler engellenir.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Windows yerel güvenlik yetkilisi alt sisteminden kimlik bilgisi çalınmasını engelle (lsass.exe)**  
  ASR kuralı: [9e6c4e1f-7d60-472F-ba1a-a39ef669e4b2](https://go.microsoft.com/fwlink/?linkid=874499)

  - **Etkinleştir** *(varsayılan)* -lsass.exe aracılığıyla kimlik bilgilerini çalmaya çalışır.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Kullanıcı tanımlı**
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **E-posta ve Web postasından istemcilerinden yürütülebilir içerik indirmeyi engelle**  
  ASR kuralı: [BE9BA2D9-53EA-4CDC-84E5-9B1EEEE46550](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Engelle** *(varsayılan)* -e-posta ve web postası istemcilerinden indirilen yürütülebilir içerik engellenir. 
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Tüm Office uygulamalarının alt işlem oluşturmasını engelle**  
  ASR kuralı: [D4F940AB-401B-4EFC-AADC-AD5F3C50688A](https://go.microsoft.com/fwlink/?linkid=872976)

  - **Engelle** *(varsayılan)* -Office uygulamalarının alt işlem oluşturması engellenir. Engellenen uygulamalar Word, Excel, PowerPoint, OneNote ve Access ' i içerir.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Büyük olasılıkla karıştırılmış betiklerin yürütülmesini engelle (js/vbs/PS)**  
  ASR kuralı: [5Beb7efe-fd9a-4556-801d-275e5ffc04cc](https://go.microsoft.com/fwlink/?linkid=872978)

  - **Engelle** *(varsayılan)* -Defender, karıştırılmış betiklerin yürütülmesini engeller.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Office makrolarından Win32 API çağrıları engelle**  
  ASR kuralı: [92E97fa1-2EDF-4476-BDD6-9DD0B4DDDC7B](https://go.microsoft.com/fwlink/?linkid=872977)

  - **Engelle** *(varsayılan)* -Office makrosunda Win32 API çağrıları kullanılması engellenir.
  - **Yapılandırılmadı** -ayarı devre dışı olan Windows varsayılan öğesine döndürün.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

## <a name="application-guard"></a>Application Guard

Daha fazla bilgi için Windows belgelerindeki [Windowssavunma Derapplicationguard CSP](/windows/client-management/mdm/windowsdefenderapplicationguard-csp) bölümüne bakın.  

Microsoft Edge kullanırken, Microsoft Defender Application Guard, ortamınızı kuruluşunuz tarafından güvenilmeyen sitelerden korur. Kullanıcılar yalıtılmış ağ sınırlarında listelenmeyen siteleri ziyaret ettiğinde, siteler bir Hyper-V sanal gözatma oturumunda açılır. Güvenilen siteler bir ağ sınırı tarafından tanımlanır.  

- **Edge için Application Guard 'ı açma (Seçenekler)**  
  CSP: [Settings/Allowwindowssavunma Derapplicationguard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Edge Için etkinleştirildi** (*varsayılan*)-Application Guard, onaylanmamış siteleri bir Hyper-V sanallaştırılmış gözatma kapsayıcısında açar.
  - **Yapılandırılmadı** -bir sanallaştırılmış kapsayıcıda değil, cihazda herhangi bir site (güvenilen ve güvenilmeyen) açılır.  
  
  *Edge Için etkinleştir*olarak ayarlandığında, *dış içeriği blok olmayan bir şekilde onaylanan siteler* ve *Pano davranışından*yapılandırabilirsiniz.

  - **Kurumsal olmayan onaylanan sitelerden dış içeriği engelle**  
    CSP: [Ayarlar/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Evet** (*varsayılan*)-onaylanmayan Web sitelerindeki içeriğin yüklenmesini engelleyin.
    - **Yapılandırılmamış** -kurumsal olmayan siteler cihazda açılabilir

  - **Pano davranışı**  
    CSP: [Ayarlar/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Yerel BILGISAYAR ile Application Guard sanal tarayıcısı arasında kopyalama ve yapıştırma eylemlerine izin verileceğini seçin. Seçeneklere şunlar dahildir:
    - **Yapılandırılmadı**  
    - **Bilgisayar ile tarayıcı arasında kopyalama ve yapıştırmayı engelle** (*varsayılan*)-engelle. BILGISAYAR ve sanal tarayıcı arasında veri aktarılamaz.
    - **Tarayıcıdan yalnızca bilgisayara kopyalama ve yapıştırmaya Izin ver** -veriler bilgisayardan sanal tarayıcıya aktarılamaz.
    - **Bilgisayardan yalnızca tarayıcıya kopyalama ve yapıştırmaya Izin ver** -veriler sanal tarayıcıdan ana bilgisayar bilgisayarına aktarılamaz.
    - **Bilgisayar ve tarayıcı arasında kopyalama ve yapıştırmaya Izin ver** -içerik için hiçbir blok yok.

- **Windows ağ yalıtımı ilkesi**  
  CSP: [Ilke CSP-NetworkIsolation](/windows/client-management/mdm/policy-csp-networkisolation)

  Bulutta barındırılan ve Application Guard 'ın kuruluş siteleri olarak davrandığı kurumsal kaynaklar olan *ağ etki alanlarının*bir listesini belirtin
  - **Yapılandır** (*varsayılan*)
  - **Yapılandırılmadı**

  *Yapılandırma* olarak ayarlandığında, *ağ etki alanlarını*tanımlayabilirsiniz.

  - **Ağ etki alanları**  
    **Ekle** ' yi seçin ve etki ALANLARıNı, IP adresi aralıklarını ve ağ sınırlarını belirtin. Varsayılan olarak, *SecurityCenter.Windows.com* yapılandırılır.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

## <a name="bitlocker"></a>BitLocker

Daha fazla bilgi için, Windows belgelerindeki [BitLocker Grup İlkesi ayarları](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) .

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Depolama kartlarının şifrelenmesini gerektir (yalnızca mobil)**  
  CSP: [Requirestooygecardencryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Bu ayar yalnızca Windows Mobile ve mobil kurumsal SKU cihazları için geçerlidir.
  - **Evet** (*varsayılan*)-mobil cihazlar için depolama kartlarında şifreleme gereklidir.
  - **Yapılandırılmadı** -ayar, depolama kartı şifrelemesi gerektirmeyen işletim sistemi varsayılana döner.

  > [!NOTE]
  > [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) ve [Windows Phone 8,1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) desteği 2020 tarihinde sona erdi.

::: zone-end
::: zone pivot="atp-sept-2020"

- **Pille çalışırken bekleme durumları** CSP: [Power/Standbytimeoutonpili](https://go.microsoft.com/fwlink/?linkid=2067195)

  Bu ilke ayarı, Windows 'un bilgisayarı uyku durumuna geçirirken bekleme durumlarını kullanıp kullanamayacağını yönetir.
  - **Devre dışı** *(varsayılan)* -bekleme durumlarına (S1-S3) izin verilmez.
  - **Etkin** -Windows, bilgisayarı uyku durumuna geçirmek için bekleme durumlarını kullanır.
  - **Yapılandırılmadı** - *etkin*olarak aynı davranış.

- **Prize takılıyken uyurken bekleme durumları**  
  CSP: [Power/Standbytimeoutpluggedın](https://go.microsoft.com/fwlink/?linkid=2067196)

  Bu ilke ayarı, Windows 'un bilgisayarı uyku durumuna geçirirken bekleme durumlarını kullanıp kullanmeyeceğini yönetir.
  - **Devre dışı** *(varsayılan)* -bekleme durumlarına (S1-S3) izin verilmez.
  - **Etkin** -Windows, bilgisayarı uyku durumuna geçirmek için bekleme durumlarını kullanır.
  - **Yapılandırılmadı** - *etkin*olarak aynı davranış.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

- **İşletim sistemi ve sabit veri sürücüleri için tam disk şifrelemesini etkinleştir**  
  CSP: [Requiredeviceencryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Bu ilke uygulanmadan önce sürücü şifrelendiyse, ek bir eylem yapılmaz. Şifreleme yöntemi ve seçenekleri bu ilkeyle eşleşiyorsa, yapılandırma başarılı döndürmelidir. Yerinde bir BitLocker yapılandırma seçeneği bu ilkeyle eşleşmezse, yapılandırma muhtemelen bir hata döndürür.
  
  Bu ilkeyi zaten şifrelenmiş bir diske uygulamak için sürücünün şifresini çözün ve MDM ilkesini yeniden uygulayın. Windows varsayılan, BitLocker Sürücü Şifrelemesi gerektirmemelidir, ancak Azure AD 'ye katılmayı ve Microsoft hesabı (MSA) kayıt/oturum açma otomatik şifrelemesi, XTS-AES 128-bit şifreleme 'de BitLocker 'ı etkinleştirmeye olanak sağlayabilir.

  - **Evet** (*varsayılan*)-BitLocker kullanımını zorunlu tutun.
  - **Yapılandırılmadı** -BitLocker zorlaması gerçekleşmez.

- **BitLocker sistem sürücüsü ilkesi**  
  [BitLocker grup ilkesi ayarları](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Yapılandır** (*varsayılan*)
  - **Yapılandırılmadı**

  *Yapılandırma*olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:

::: zone-end
::: zone pivot="atp-sept-2020"

- **Başlangıç kimlik doğrulaması gerekiyor**  
  CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

  - **Evet** *(varsayılan)* -Güvenilir Platform Modülü (TPM) veya başlangıç PIN gereksinimlerinin kullanımı dahil olmak üzere sistem başlangıcında ek kimlik doğrulama gereksinimlerini yapılandırabilirsiniz:
  - **Yapılandırılmadı**

    - **Uyumlu TPM başlangıç PIN 'ı**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527) , bu ayar, *gerekli başlatma kimlik doğrulaması* *Evet*olarak ayarlandığında kullanılabilir.

      - **Engellendi** -PIN kullanımını engeller. 
      - **Gerekli** -BitLocker 'ın başarılı DÖNDÜRÜLMESI için PIN ve TPM 'nin mevcut olması gerekir. Sessiz etkinleştirme senaryolarında (Autopilot dahil), Kullanıcı etkileşimi gerekli olduğundan bu ayar başarılı olamaz. BitLocker 'ın sessiz etkinleştirilmesi gerektiği için PIN 'in devre dışı bırakılması önerilir.
      - **Izin verilen** *(varsayılan)* -varsa TPM 'yi kullanarak BitLocker 'ı etkinleştirin ve bir başlangıç PIN 'inin Kullanıcı tarafından yapılandırılmasına izin verin.
      - **Yapılandırılmadı**

    - **Uyumlu TPM başlangıç anahtarı**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527) , bu ayar, *gerekli başlatma kimlik doğrulaması* *Evet*olarak ayarlandığında kullanılabilir.

      - **Engellendi** -başlangıç anahtarlarının kullanımını engelleyin.
      - **Gerekli** *(varsayılan)* -BitLocker 'ı etkinleştirmek için BitLocker 'ın BIR başlangıç anahtarına ve TPM 'ye sahip olması gerekir. Sessiz etkinleştirme senaryolarında (Autopilot dahil), Kullanıcı etkileşimi gerekli olduğundan bu ayar başarılı olamaz. BitLocker 'ın sessiz etkinleştirilmesi gerektiğinde, başlangıç anahtarlarının devre dışı bırakılması önerilir.
      - **Izin verildi** -varsa TPM 'Yi kullanarak BitLocker 'ı etkinleştirin ve sürücülerin kilidini açmak için bir başlangıç anahtarı (USB sürücü gibi) var olmasına izin verin.
      - **Yapılandırılmadı** *(varsayılan)*

    - **TPM 'nin uyumsuz olduğu cihazlarda BitLocker 'ı devre dışı bırakma**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527) , bu ayar, *gerekli başlatma kimlik doğrulaması* *Evet*olarak ayarlandığında kullanılabilir.

      - **Evet** *(varsayılan)* -BITLOCKER 'ın uyumlu bir TPM yongası olmadan yapılandırılmasını devre dışı bırakın. Bu ayar test için yararlı olabilir, ancak TPM olmadan BitLocker 'ı etkinleştirmek önerilmez. TPM yoksa, BitLocker başlatma için bir parola veya USB sürücü gerektirir. Bu ayar yalnızca BitLocker etkinleştirilmesinde geçerlidir. Bu ayarı uygulamadan önce BitLocker zaten etkinse, hiçbir etkisi olmayacaktır.
      - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

  - **Işletim sistemi sürücüleri için şifreleme yöntemini yapılandırma**  
    CSP: [Encryptionmethodbydrivetype](https://go.microsoft.com/fwlink/?linkid=872526)  
    Bu ayar *BitLocker sistem sürücüsü Ilkesi* *Yapılandır*olarak ayarlandığında kullanılabilir.  

    Sistem sürücüleri için şifreleme yöntemini ve şifre gücünü yapılandırın.  *XTS-AES 128-bit* , Windows varsayılan şifreleme yöntemidir ve önerilen değerdir.

    - **Yapılandırılmadı** (*varsayılan*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

- **BitLocker sabit sürücü ilkesi**  
  [BitLocker grup ilkesi ayarları](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Yapılandır** (*varsayılan*)
  - **Yapılandırılmadı**

  *Yapılandırma*olarak ayarlandığında, *BitLocker tarafından korunmayan sabit veri sürücülerine blok yazma erişimini* yapılandırabilir ve *sabit veri sürücüleri için şifreleme yöntemini yapılandırabilirsiniz*.

  - **BitLocker tarafından korunmayan sabit veri sürücülerine yönelik yazma erişimini engelleyin**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Bu ayar *BitLocker sabit sürücü Ilkesi* *Yapılandır*olarak ayarlandığında kullanılabilir.

    - **Yapılandırılmamış** -veriler, şifrelenmemiş sabit sürücülere yazılabilir.
    - **Evet** (*varsayılan*)-Windows, BitLocker korumalı olmayan sabit sürücülere hiçbir verinin yazılmasına izin vermez. Sabit bir sürücü şifrelenmemişse, yazma erişimi verilmeden önce kullanıcının BitLocker kurulum Sihirbazı 'nı tamamlaması gerekir.

  - **Sabit veri sürücüleri için şifreleme yöntemini yapılandırma**  
    CSP: [Encryptionmethodbydrivetype](https://go.microsoft.com/fwlink/?linkid=872526)  
    Bu ayar *BitLocker sabit sürücü Ilkesi* *Yapılandır*olarak ayarlandığında kullanılabilir.

    Sabit veri sürücüleri diskleri için şifreleme yöntemini ve şifre gücünü yapılandırın. *XTS-AES 128-bit* , Windows varsayılan şifreleme yöntemidir ve önerilen değerdir.

    - **Yapılandırılmadı**
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS** (*varsayılan*)
    - **AES 256bit XTS**

- **BitLocker çıkarılabilir sürücü ilkesi**  
  [BitLocker grup ilkesi ayarları](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Yapılandır** (*varsayılan*)
  - **Yapılandırılmadı**

  *Yapılandırma*olarak ayarlandığında, *çıkarılabilir veri sürücüleri için şifreleme yöntemini* yapılandırın ve *BitLocker tarafından korunmayan çıkarılabilir veri sürücülerine yönelik yazma erişimini engelleyin*.

  - **Çıkarılabilir veri sürücüleri için şifreleme yöntemini yapılandırma**  
    CSP: [Encryptionmethodbydrivetype](https://go.microsoft.com/fwlink/?linkid=872526)  
    Bu ayar *BitLocker çıkarılabilir sürücü Ilkesi* *Yapılandır*olarak ayarlandığında kullanılabilir.

    Çıkarılabilir veri sürücüleri diskleri için şifreleme yöntemini ve şifre gücünü yapılandırın. *XTS-AES 128-bit* , Windows varsayılan şifreleme yöntemidir ve önerilen değerdir.

    - **Yapılandırılmadı**
    - **AES 128bit CBC** (*varsayılan*)
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **BitLocker tarafından korunmayan çıkarılabilir veri sürücülerine yönelik yazma erişimini engelleyin**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    Bu ayar *BitLocker çıkarılabilir sürücü Ilkesi* *Yapılandır*olarak ayarlandığında kullanılabilir.

    - **Yapılandırılmadı** (*varsayılan*)-veriler, şifrelenmemiş çıkarılabilir sürücülere yazılabilir.  
    - **Evet** -Windows, BitLocker korumalı olmayan çıkarılabilir sürücülere hiçbir verinin yazılmasına izin vermez. Çıkarılabilir bir sürücü şifrelenmemişse, yazma erişimi verilmeden önce kullanıcının BitLocker kurulum Sihirbazı 'nı tamamlaması gerekir.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

## <a name="browser"></a>Tarayıcı

- **Microsoft Edge için SmartScreen gerektir**  
  CSP: [tarayıcı/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Evet** (*varsayılan*)-kullanıcıları olası kimlik avı dolandırıcılarından ve kötü amaçlı yazılımlardan korumak için SmartScreen kullanın.
  - **Yapılandırılmadı**

- **Kötü amaçlı Site erişimini engelleyin**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Evet** (*varsayılan*)-kullanıcıların Microsoft Defender SmartScreen Filtresi uyarılarını yoksaymasını ve siteye gitmesini engelleyin.
  - **Yapılandırılmadı**

- **Doğrulanmamış dosya indirmeyi engelle**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Evet** (*varsayılan*)-kullanıcıların Microsoft Defender SmartScreen Filtresi uyarılarını yok saymasını engelleyin ve doğrulanmamış dosyaları indirmelerini engelleyin.
  - **Yapılandırılmadı**

## <a name="data-protection"></a>Veri Koruma

- **Doğrudan bellek erişimini engelle**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  Bu ilke ayarı yalnızca BitLocker veya cihaz şifrelemesi etkinleştirildiğinde zorlanır.

  - **Evet** (*varsayılan*)-Kullanıcı Windows 'a oturum açana kadar tüm etkin takılabilir PCI akış bağlantı noktaları için doğrudan bellek erişimini (DMA) engelleyin. Kullanıcı oturum açtıktan sonra, Windows, ana bilgisayar eklentisi PCI bağlantı noktalarına bağlı PCI cihazlarını numaralandırır. Kullanıcı makineyi her kilitlediğinde, Kullanıcı yeniden oturum açana kadar alt cihazları olmayan hot plug PCI bağlantı noktalarında DMA engellenir. Makine kilidi açıldığında zaten numaralandırılan cihazlar, söküle kadar çalışmaya devam eder.
  - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

## <a name="device-guard"></a>Device Guard  

- **Credential Guard 'ı aç**  
  CSP: [Deviceguard/Configuressystemutility Mguardlaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard, donanım gereksinimlerinin karşılanmasını gerektiren güvenli önyükleme ve DMA korumaları gerektiren korumalar sağlamak için Windows Hiper Yöneticisi 'ni kullanır.

  - **Yapılandırılmadı**
  - **UEFI kilidi Ile etkinleştir** (*varsayılan*)-Credential Guard 'ı etkinleştirin ve UEFI kalıcı yapılandırmanın el ile temizlenmesi gerektiği için uzaktan devre dışı bırakılamaz.
  - **UEFI kilidi olmadan etkinleştirin** -Credential Guard 'ı etkinleştirin ve makinenin makineye fiziksel erişimi olmadan kapatılmış olmasını sağlayın.
  - **Disable** -Windows varsayılan olan Credential Guard kullanımını devre dışı bırakın.

## <a name="device-installation"></a>Cihaz yüklemesi

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Cihaz tanımlayıcılarına göre donanım cihazı yüklemesi**  
  [Deviceınstallation/Preventınstalnmatchingdevicıdıd](https://go.microsoft.com/fwlink/?linkid=2066794)

  Bu ilke ayarı, Windows 'un yüklemesi engellenen cihazlar için Tak ve Kullan donanım kimliklerinin ve uyumlu kimliklerin bir listesini belirtmenizi sağlar. Bu ilke ayarı, Windows 'un bir cihaz yüklemesine izin veren diğer tüm ilke ayarlarından önceliklidir.  Uzak Masaüstü sunucusunda bu ilke ayarını etkinleştirirseniz, ilke ayarı, belirtilen cihazların uzak masaüstü istemcisinden uzak masaüstü sunucusuna yönlendirilmesini etkiler.

  - **Yapılandırılmadı**
  - **Donanım cihazı yüklemeye Izin ver** -cihazların izin verilen veya engellenen şekilde diğer ilke ayarları tarafından yüklenip güncelleştirilemeyebilir.
  - **Donanım cihazını yüklemeyi engelle** (*varsayılan*)-Windows 'un, sizin TANıMLADıĞıNıZ bir listede donanım kimliği veya uyumlu kimliği görünen bir cihaz yüklemesi engellenir.

  *Donanım cihazını yüklemeyi engelle* olarak ayarlandığında, *eşleşen donanım cihazlarını* ve *Engellenen donanım cihaz tanımlayıcılarını*Kaldır ' a göre yapılandırma yapabilirsiniz.

  - **Eşleşen donanım cihazlarını kaldırma**

    Bu ayar yalnızca *cihaz tanımlayıcılarına göre donanım cihaz yüklemesi* , *donanım cihazı yüklemeyi engelleyecek*şekilde ayarlandığında kullanılabilir.
    - **Evet** *(varsayılan)*
    - **Yapılandırılmadı**

  - **Engellenen donanım cihaz tanımlayıcıları**  

    Bu ayar yalnızca *cihaz tanımlayıcılarına göre donanım cihaz yüklemesi* , *donanım cihazı yüklemeyi engelleyecek*şekilde ayarlandığında kullanılabilir.

    **Ekle**' yi seçin ve ardından engellemek istediğiniz donanım cihaz tanımlayıcısını belirtin.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

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
    - **Yapılandırılmadı** *(varsayılan)*

  - **Engellenen donanım cihaz tanımlayıcıları**

    Bu ayar yalnızca *cihaz tanımlayıcılarına göre donanım cihaz yüklemesi* , *donanım cihazı yüklemeyi engelleyecek*şekilde ayarlandığında kullanılabilir.

    **Ekle**' yi seçin ve ardından engellemek istediğiniz donanım cihaz tanımlayıcısını belirtin.

## <a name="dma-guard"></a>DMA koruyucusu

- **Çekirdek DMA koruması ile uyumsuz dış cihazların numaralandırması**  
  CSP: [Dmaguard/DeviceEnumerationPolicy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Bu ilke, dış DMA özellikli cihazlara karşı ek güvenlik sağlayabilir. DMA yeniden eşleme/cihaz belleği yalıtımı ve korumalı alana alma ile uyumsuz olan dış DMA özellikli cihazların numaralandırılması üzerinde daha fazla denetim sağlar.

  Bu ilke, yalnızca çekirdek DMA koruması desteklenirken ve Sistem bellenimi tarafından etkinleştirildiğinde devreye girer. Çekirdek DMA koruması, üretim sırasında sistem tarafından desteklenmesi gereken bir platform özelliğidir. Sistemin çekirdek DMA korumasını destekleyip desteklemediğini denetlemek için MSINFO32.exe Özet sayfasındaki çekirdek DMA koruması alanını denetleyin.

::: zone-end
::: zone pivot="atp-sept-2020"

  - **Yapılandırılmadı**  
  - **Tümünü Engelle** *(erulat)*
  - **Tümüne izin ver**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Yapılandırılmadı** -(*varsayılan*)
  - **Tümünü engelle**
  - **Tümüne izin ver**

## <a name="endpoint-detection-and-response"></a>Uç nokta algılama ve yanıt

Aşağıdaki ayarlar hakkında daha fazla bilgi için Windows belgelerindeki [Windowsadvancedthreatprotection](/windows/client-management/mdm/windowsadvancedthreatprotection-csp) CSP bölümüne bakın.

- **Tüm dosyalar için örnek paylaşımı**  
  CSP: [yapılandırma/SampleSharing](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Microsoft Defender Gelişmiş tehdit koruması örnek paylaşımı yapılandırma parametresini döndürür veya ayarlar.
  
  - **Evet** (*varsayılan*)
  - **Yapılandırılmadı**

- **Telemetri raporlama sıklığını hızlandırın**  
  CSP: [yapılandırma/TelemetryReportingFrequency](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Microsoft Defender Gelişmiş tehdit koruması telemetri raporlama sıklığını hızlandırın.  

  - **Evet** (*varsayılan*)
  - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

## <a name="firewall"></a>Güvenlik Duvarı

Daha fazla bilgi için Windows belgelerindeki [güvenlik DUVARı CSP](/windows/client-management/mdm/firewall-csp) bölümüne bakın.

- **Durum bilgisi olan Dosya Aktarım Protokolü (FTP)**  
  CSP: [Mdmstore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Devre dışı** (*varsayılan*)-durum bilgisi olan FTP devre dışı bırakıldı.
  - **Izin ver** -güvenlik duvarı, ikincil bağlantılara izin vermek için durum bilgisi olan Dosya Aktarım Protokolü (FTP) filtrelemesi gerçekleştirir. Devre dışı
  - **Yapılandırılmadı**

- **Bir güvenlik ilişkisinin silinmeden önce boşta kalabileceği saniye sayısı**  
  CSP: [Mdmstore/Global/Saıdsaati](https://go.microsoft.com/fwlink/?linkid=872539)

  Ağ trafiği artık görülmedikçe güvenlik ilişkilerinin ne kadar süreyle tutulacağını belirtin. Yapılandırılmadığında, sistem, *300* saniye boyunca boşta kaldıktan sonra bir güvenlik ilişkilendirmesini siler (varsayılan).
  
  Sayı **300** ile **3600** saniye arasında olmalıdır.

- **Önceden paylaşılan anahtar kodlaması**  
  CSP: [Mdmstore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   UTF-8 gerekmiyorsa, önceden paylaşılmış anahtarlar UTF-8 kullanılarak kodlanacaktır. Bundan sonra cihaz kullanıcıları başka bir kodlama yöntemi seçebilirler.

  - **Yapılandırılmadı**
  - **Hiçbiri**
  - **UTF8** (*varsayılan*)

- **Sertifika iptal listesi (CRL) doğrulaması**  
  CSP: [Mdmstore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Sertifika iptal listesi (CRL) doğrulamanın nasıl uygulanacağını belirtin.  

  - **Yapılandırılmadı** (*varsayılan*)-CRL doğrulaması devre dışı bırakıldı.
  - **Hiçbiri**
  - **Girişimde**
  - **Gerektirme**

- **Paket Kuyruklama**  
  CSP: [Mdmstore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  IPSec tüneli ağ geçidi senaryosunda, şifreli alma ve şifresiz metin iletme için alma tarafında yazılım ölçeklendirmesinin nasıl etkinleştirildiğini belirtin. Bu ayar, paket sırasının korunmasını sağlar.

  - **Yapılandırılmadı** (*varsayılan*)-paket Kuyruklama, varsayılan olarak devre dışı olan istemci varsayılan değerini döndürür.
  - **Devre dışı**
  - **Gelen kuyruk**
  - **Giden kuyruk**
  - **Her Ikisini de kuyruğa al**

- **Güvenlik duvarı profili özel**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Yapılandır** (*varsayılan*)
  - **Yapılandırılmadı**

  *Yapılandırma*olarak ayarlandığında, aşağıdaki ek ayarları yapılandırabilirsiniz.

  - **Engellenen gelen bağlantılar**  
    CSP: [/Defaulınboundadction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Çok noktaya yayın yayınlarına tek noktaya yayın yanıtları gerekiyor**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Gerekli giden bağlantılar**  
    CSP: [/Defaultoutbounnection](https://aka.ms/intune-firewall-outboundaction)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Engellenen gelen bildirimler**  
    CSP: [/Disableınboundnotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Grup İlkesi ile birleştirilen genel bağlantı noktası kuralları**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Güvenlik Duvarı etkin**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Yapılandırılmadı**
    - **Engellendi**
    - **Izin verilen** (*varsayılan*)

  - **Grup ilkesinden yetkili uygulama kuralları birleştirilmedi**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Grup İlkesi 'nden bağlantı güvenlik kuralları birleştirilmedi**  
    CSP: [/Allowlocalıpsecpolicymerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Gelen trafik gerekli**  
    CSP: [/korumalı](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Grup ilkesinden ilke kuralları birleştirilmedi**  
    CSP: [/Allowlocalpolicymerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Gizli mod engellendi**  
    CSP: [/Disablestealthmode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

- **Güvenlik duvarı profili genel**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Yapılandır** (*varsayılan*)
  - **Yapılandırılmadı**

  *Yapılandırma*olarak ayarlandığında, aşağıdaki ek ayarları yapılandırabilirsiniz.

  - **Engellenen gelen bağlantılar**  
    CSP: [/Defaulınboundadction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Çok noktaya yayın yayınlarına tek noktaya yayın yanıtları gerekiyor**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Gerekli giden bağlantılar**  
    CSP: [/Defaultoutbounnection](https://aka.ms/intune-firewall-outboundaction)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Grup ilkesinden yetkili uygulama kuralları birleştirilmedi**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Engellenen gelen bildirimler**  
    CSP: [/Disableınboundnotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Grup İlkesi ile birleştirilen genel bağlantı noktası kuralları**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Güvenlik Duvarı etkin**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Yapılandırılmadı**
    - **Engellendi**
    - **Izin verilen** (*varsayılan*)

  - **Grup İlkesi 'nden bağlantı güvenlik kuralları birleştirilmedi**  
    CSP: [/Allowlocalıpsecpolicymerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Gelen trafik gerekli**  
    CSP: [/korumalı](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Grup ilkesinden ilke kuralları birleştirilmedi**  
    CSP: [/Allowlocalpolicymerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Gizli mod engellendi**  
    CSP: [/Disablestealthmode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

- **Güvenlik duvarı profili etki alanı**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Çok noktaya yayın yayınlarına tek noktaya yayın yanıtları gerekiyor**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Grup ilkesinden yetkili uygulama kuralları birleştirilmedi**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**  

  - **Engellenen gelen bildirimler**  
    CSP: [/Disableınboundnotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Grup İlkesi ile birleştirilen genel bağlantı noktası kuralları**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Güvenlik Duvarı etkin**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Yapılandırılmadı**
    - **Engellendi**
    - **Izin verilen** (*varsayılan*)

  - **Grup İlkesi 'nden bağlantı güvenlik kuralları birleştirilmedi**  
    CSP: [/Allowlocalıpsecpolicymerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

  - **Grup ilkesinden ilke kuralları birleştirilmedi**  
    CSP: [/Allowlocalpolicymerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Gizli mod engellendi**  
    CSP: [/Disablestealthmode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Evet** (*varsayılan*)
    - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

## <a name="microsoft-defender"></a>Microsoft Defender

::: zone-end
::: zone pivot="atp-sept-2020"

- **Gerçek zamanlı korumayı aç**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Evet** (*varsayılan*)-gerçek zamanlı izleme zorlanır ve Kullanıcı bunu devre dışı bırakamayabilir.
  - **Yapılandırılmadı** -ayar, üzerinde olan istemci varsayılanı olarak döndürülür, ancak kullanıcı bunu değiştirebilir. Gerçek zamanlı izlemeyi devre dışı bırakmak için özel bir URI kullanın.

- **Bulut koruması zaman aşımını uzatmak için ek süre (0-50 saniye)**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender virüsten koruma, güvenli olduklarından emin olmak için kuşkulu dosyaları 10 saniye içinde otomatik olarak engeller. Bu ayarla, bu zaman aşımı için en fazla 50 ek saniye ekleyebilirsiniz.  Varsayılan olarak, zaman aşımı sıfır (**0**) olarak ayarlanır.

- **İndirilen tüm dosyaları ve ekleri Tara**  
  CSP: [Defender/Allowwioavprotection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Evet** (*varsayılan*)-indirilen tüm dosyalar ve ekler taranır. Ayar, üzerinde olan istemci varsayılan öğesine döndürülür, ancak kullanıcı bunu değiştirebilir. Bu ayarı devre dışı bırakmak için özel bir URI kullanın.
  - **Yapılandırılmadı** -ayar, üzerinde olan istemci varsayılanı olarak döndürülür, ancak kullanıcı bunu değiştirebilir. Bu ayarı devre dışı bırakmak için özel bir URI kullanın.

- **Tarama türü**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Kullanıcı tanımlı**
  - **Devre dışı**
  - **Hızlı tarama** (*varsayılan*)
  - **Tam tarama**

- **Defender örnek gönderim onayı**  
  CSP: [Defender/Submitsamplesonayı](https://go.microsoft.com/fwlink/?linkid=2067131)

  Veri göndermek için Microsoft Defender 'daki Kullanıcı izin düzeyini denetler. Gerekli onay zaten verildiyse, Microsoft Defender bunları gönderir. Değilse (ve Kullanıcı hiçbir zaman sorma olarak belirtilmişse), veri göndermeden önce Kullanıcı izni ( *buluta teslim edilen koruma* *Evet*olarak ayarlandığında) ister.

  - **Güvenli örnekleri otomatik olarak gönder** (*varsayılan*)
  - **Her zaman sor**
  - **Hiçbir şekilde gönderme**
  - **Tüm örnekleri otomatik olarak gönder**

- **Buluta teslim edilen koruma düzeyi**  
  CSP: [Cloudblocklevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Agresif Defender virüsten koruma 'nın şüpheli dosyaları engelleme ve tarama hakkında daha fazla yapılandırma.
  - **Yapılandırılmadı** -varsayılan Defender engelleme düzeyi.
  - **Yüksek** *(varsayılan)* -istemci performansını iyileştirirken, yanlış pozitif sonuçlar içeren daha büyük bir şanstan daha fazla şans içeren bir performans vermez.
  - **Yüksek artı-güvenip** , istemci performansını etkileyebilecek ek koruma önlemleri uygular.
  - **Sıfır toleransı** -tüm bilinmeyen yürütülebilir dosyaları engelle.

- **Tam tarama sırasında çıkarılabilir sürücüleri Tara**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Evet** (*varsayılan*)-tam tarama sırasında, çıkarılabilir sürücüler (USB flash sürücüler gibi) taranır.
  - **Yapılandırılmadı** -Bu ayar, istemci Varsayılanı ' nı döndürür ve bu, kaldırılabilir sürücüleri tarar ancak kullanıcı bu taramayı devre dışı bırakabilir.

- **Defender istenmeyebilecek uygulama eylemi**  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  İstenmeyebilecek uygulamalar için algılama düzeyini belirtin (PUAs). Defender, istenmeyebilecek yazılımların indirileceği veya bir cihaza yüklenmeye çalıştığı durumlarda kullanıcıları uyarır.
  - **Cihaz varsayılanı**
  - **Engelle** (*varsayılan*)-algılanan öğeler engellenir ve diğer tehditlerle birlikte geçmiş olarak gösterilir.
  - **Denetim** -Defender, istenmeyebilecek uygulamaları algılar, ancak hiçbir işlem gerçekleşmez. Olay Görüntüleyicisi Defender tarafından oluşturulan olayları arayarak, uygulama Defender ile ilgili bilgileri gözden geçirebilirsiniz.

- **Buluta teslim edilen korumayı aç**  
  CSP: [Allowcloudprotection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Varsayılan olarak, Windows 10 masaüstü cihazlarındaki Defender, bulduğu sorunlar hakkında Microsoft 'a bilgi gönderir. Microsoft, sizi ve diğer müşterileri etkileyen sorunlar hakkında daha fazla bilgi edinmek için bu bilgileri çözümleyerek geliştirilmiş çözümler sunar.

  - **Evet** (*varsayılan*)-buluta teslim edilen koruma açıktır.  Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Yapılandırılmadı**  -ayar, sistem varsayılan ayarlarına geri yüklenir.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Günlük hızlı taramayı şurada Çalıştır:**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Günlük hızlı taramanın ne zaman çalışacağını yapılandırın. Varsayılan olarak, tarama çalıştırması **2**olarak ayarlanır.

- **Zamanlanmış tarama başlangıç zamanı**  
  
  Varsayılan olarak, başlangıç saati **2 ÖÖ**olarak ayarlanır.

- **Zamanlanan Taramalar için düşük CPU önceliğini yapılandırma**  
  CSP: [Defender/Enablelowcpupriınıd](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Evet** (*varsayılan*)
  - **Yapılandırılmadı**

- **Office iletişim uygulamalarının alt işlem oluşturmasını engelleyin**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874499)  

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Yapılandırılmadı** -Windows varsayılanı geri yüklenir, bu, alt işlemlerin oluşturulmasını engellemez.
  - **Kullanıcı tanımlı**
  - **Etkinleştir** (*varsayılan*)-Office iletişim uygulamalarının alt işlem oluşturması engellenir.
  - **Denetim modu** -Windows olayları, alt işlemlerin engellenmesi yerine oluşturulur.

- **Adobe Reader 'ın alt işlem oluşturmasını engelleyin**  
  [Saldırı yüzeyi azaltma kurallarıyla saldırı yüzeylerini azaltma](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **Yapılandırılmadı** -Windows varsayılanı geri yüklendi, alt işlemlerin oluşturulmasını engellemez.
  - **Kullanıcı tanımlı**
  - **Etkinleştir** (*varsayılan*)-Adobe okuyucunun alt işlem oluşturması engellenir.
  - **Denetim modu** -Windows olayları, alt işlemlerin engellenmesi yerine oluşturulur.

- **Gelen e-posta iletilerini Tara**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Evet** (*varsayılan*)-e-posta posta kutusu ve PST, dbx, mnx, MIME ve BINHEX gibi posta dosyaları taranır.
  - **Yapılandırılmadı** -ayar, taranmamış olan e-posta dosyalarının istemci varsayılan değerini döndürür.

- **Gerçek zamanlı korumayı aç**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Evet** (*varsayılan*)-gerçek zamanlı izleme zorlanır ve Kullanıcı bunu devre dışı bırakamayabilir.
  - **Yapılandırılmadı** -ayar, üzerinde olan istemci varsayılanı olarak döndürülür, ancak kullanıcı bunu değiştirebilir. Gerçek zamanlı izlemeyi devre dışı bırakmak için özel bir URI kullanın.

- **Karantinaya alınan kötü amaçlı yazılımı tutmak için gün sayısı (0-90)**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Silinmeden önce, maddelerin karantina klasöründe tutulması gereken gün sayısını yapılandırın. Varsayılan değer sıfırdır (**0**) ve bu, karantinaya alınan dosyaların neden kaldırılmayacağı anlamına gelir.

- **Defender sistem tarama zamanlaması**  
  CSP: [Defender/ScheduleScanDay](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Defender 'ın cihazları taradığı günü zamanlayın. Tarama, varsayılan olarak **Kullanıcı tanımlı** *, ancak*haftanın her gününde veya *Zamanlanmış tarama olmadan*ayarlanabilir.

- **Bulut koruması zaman aşımını uzatmak için ek süre (0-50 saniye)**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender virüsten koruma, güvenli olduklarından emin olmak için kuşkulu dosyaları 10 saniye içinde otomatik olarak engeller. Bu ayarla, bu zaman aşımı için en fazla 50 ek saniye ekleyebilirsiniz.  Varsayılan olarak, zaman aşımı sıfır (**0**) olarak ayarlanır.

- **Tam tarama sırasında eşlenmiş ağ sürücülerine tarama**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Evet** (*varsayılan*)-tam tarama sırasında, eşlenmiş ağ sürücüleri dahil edilir.
  - **Yapılandırılmadı** -istemci, eşlenmiş ağ sürücülerinde taramayı devre dışı bırakan varsayılan değerini döndürür.

- **Ağ korumasını aç**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Evet** (*varsayılan*)-ağ İnceleme sistemi (NIS) imzaları tarafından algılanan kötü amaçlı trafiği engelleyin.
  - **Yapılandırılmadı**

- **İndirilen tüm dosyaları ve ekleri Tara**  
  CSP: [Defender/Allowwioavprotection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Evet** (*varsayılan*)-indirilen tüm dosyalar ve ekler taranır. Ayar, üzerinde olan istemci varsayılan öğesine döndürülür, ancak kullanıcı bunu değiştirebilir. Bu ayarı devre dışı bırakmak için özel bir URI kullanın.
  - **Yapılandırılmadı** -ayar, üzerinde olan istemci varsayılanı olarak döndürülür, ancak kullanıcı bunu değiştirebilir. Bu ayarı devre dışı bırakmak için özel bir URI kullanın.

::: zone-end
::: zone pivot="atp-april-2020"

- **Erişim Koruması 'nda engelle**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Evet**
  - **Yapılandırılmadı** (*varsayılan*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Erişim Koruması 'nda engelle**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Evet** (*varsayılan*)
  - **Yapılandırılmadı**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Tarayıcı betiklerini Tara**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Evet** (*varsayılan*)-Microsoft Defender betik tarama işlevi zorlanır ve Kullanıcı bunları kapatamaz.
  - **Yapılandırılmadı** -Bu ayar, istemci varsayılanı olarak döndürülür, ancak betik taramasını etkinleştirir, ancak kullanıcı devre dışı bırakabilirsiniz.

- **Microsoft Defender uygulamasına Kullanıcı erişimini engelleyin**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **Evet** (*varsayılan*)-Microsoft Defender Kullanıcı arabirimine (UI) erişilemez ve bildirimler şaşırtır
  - **Yapılandırılmadı** Evet olarak ayarlandığında, Windows Defender Kullanıcı arabirimine (UI) erişilemez ve bildirimler şaşıracaktır. Yapılandırılmadı olarak ayarlandığında, ayar, Kullanıcı arabiriminin ve bildirimlerin izin verdiği istemci varsayılana döner

- **Tarama başına izin verilen en yüksek CPU kullanımı (yüzde 0-100)**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Bir tarama için kullanılacak en fazla CPU miktarı yüzdesi olarak belirtin. Varsayılan değer **50**' dir.

- **Tarama türü**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Kullanıcı tanımlı**
  - **Devre dışı**
  - **Hızlı tarama** (*varsayılan*)
  - **Tam tarama**

- **Güvenlik Zekası güncelleştirmelerini denetleme sıklığını (0-24 saat) girin**  
  CSP: [Defender/Signatureupdateınterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Güncelleştirilmiş imzaların ne sıklıkta kontrol etmek için saat cinsinden belirtin. Örneğin, 1 değeri her saat kontrol eder. 2 değeri her iki saatte bir denetlenir ve bu şekilde devam eder.

  Hiçbir değer tanımlanmamışsa, cihazlar varsayılan olarak **8** saat istemci kullanır.

- **Defender örnek gönderim onayı**  
  CSP: [Defender/Submitsamplesonayı](https://go.microsoft.com/fwlink/?linkid=2067131)

  Veri göndermek için Microsoft Defender 'daki Kullanıcı izin düzeyini denetler. Gerekli onay zaten verildiyse, Microsoft Defender bunları gönderir. Değilse (ve Kullanıcı hiçbir zaman sorma olarak belirtilmişse), veri göndermeden önce Kullanıcı izni ( *buluta teslim edilen koruma* *Evet*olarak ayarlandığında) ister.

  - **Güvenli örnekleri otomatik olarak gönder** (*varsayılan*)
  - **Her zaman sor**
  - **Hiçbir şekilde gönderme**
  - **Tüm örnekleri otomatik olarak gönder**

- **Buluta teslim edilen koruma düzeyi**  
  CSP: [Cloudblocklevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Agresif Defender virüsten koruma 'nın şüpheli dosyaları engelleme ve tarama hakkında daha fazla yapılandırma.
  - **Yapılandırılmadı** (*varsayılan*)-varsayılan Defender engelleme düzeyi.
  - İstemci performansını iyileştirirken, yanlış pozitif sonuçlar içeren daha büyük bir şanstan oluşan **yüksek** performanslı bir ungo blok.
  - **Yüksek artı-güvenip** , istemci performansını etkileyebilecek ek koruma önlemleri uygular.
  - **Sıfır toleransı** -tüm bilinmeyen yürütülebilir dosyaları engelle.

- **Arşiv dosyalarını tara**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Evet** (*varsayılan*)-ZIP veya CAB dosyaları gibi arşiv dosyalarının taranması zorlanır.
  - **Yapılandırılmadı** -Bu ayar, arşivlenen dosyaları taramak için varsayılan istemci varsayılana geri döndürülür, ancak Kullanıcı taramayı devre dışı bırakabilir.

- **Davranış izlemeyi aç**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Evet** (*varsayılan*)-davranış izleme zorlanır ve Kullanıcı bunu devre dışı bırakamayabilir.
  - **Yapılandırılmadı** -ayar, üzerinde olan istemci varsayılanı olarak döndürülür, ancak kullanıcı bunu değiştirebilir. Gerçek zamanlı izlemeyi devre dışı bırakmak için özel bir URI kullanın.
  
- **Tam tarama sırasında çıkarılabilir sürücüleri Tara**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Evet** (*varsayılan*)-tam tarama sırasında, çıkarılabilir sürücüler (USB flash sürücüler gibi) taranır.
  - **Yapılandırılmadı** -Bu ayar, istemci Varsayılanı ' nı döndürür ve bu, kaldırılabilir sürücüleri tarar ancak kullanıcı bu taramayı devre dışı bırakabilir.
  
- **Ağ dosyalarını Tara**  
  CSP: [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Evet** (*varsayılan*)-Microsoft Defender ağ dosyalarını tarar.
  - **Yapılandırılmadı** -istemci, ağ dosyalarının taranmasını devre dışı bırakan varsayılan değerini döndürür.

- **Defender istenmeyebilecek uygulama eylemi**  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  İstenmeyebilecek uygulamalar için algılama düzeyini belirtin (PUAs). Defender, istenmeyebilecek yazılımların indirileceği veya bir cihaza yüklenmeye çalıştığı durumlarda kullanıcıları uyarır.
  - **Cihaz varsayılanı**
  - **Engelle** (*varsayılan*)-algılanan öğeler engellenir ve diğer tehditlerle birlikte geçmiş olarak gösterilir.
  - **Denetim** -Defender, istenmeyebilecek uygulamaları algılar, ancak hiçbir işlem gerçekleşmez. Olay Görüntüleyicisi Defender tarafından oluşturulan olayları arayarak, uygulama Defender ile ilgili bilgileri gözden geçirebilirsiniz.

- **Buluta teslim edilen korumayı aç**  
  CSP: [Allowcloudprotection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Varsayılan olarak, Windows 10 masaüstü cihazlarındaki Defender, bulduğu sorunlar hakkında Microsoft 'a bilgi gönderir. Microsoft, sizi ve diğer müşterileri etkileyen sorunlar hakkında daha fazla bilgi edinmek için bu bilgileri çözümleyerek geliştirilmiş çözümler sunar.

  - **Evet** (*varsayılan*)-buluta teslim edilen koruma açıktır.  Cihaz kullanıcıları bu ayarı değiştiremezler.
  - **Yapılandırılmadı**  -ayar, sistem varsayılan ayarlarına geri yüklenir.

- **Office uygulamalarının ekleme koddan diğer işlemlere engel**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872974)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Engelle** (*varsayılan*)-Office uygulamalarının ekleme kodu diğer işlemlere engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Office uygulamalarının yürütülebilir içerik oluşturmasını engelleyin**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872975)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Engelle** (*varsayılan*)-Office uygulamalarının yürütülebilir içerik oluşturması engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.
  
- **JavaScript veya VBScript 'in indirilen yürütülebilir içeriği başlatmasını engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872979)

   Bu ASR kuralı şu GUID aracılığıyla denetlenir: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Engelle** (*varsayılan*)-Defender, Internet 'Ten indirilen JavaScript veya VBScript dosyalarını yürütülmeden engeller.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.
  
- **Ağ korumasını etkinleştir**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Yapılandırılmadı** -Bu ayar, devre dışı bırakılan Windows varsayılan öğesine geri döner.
  - **Kullanıcı tanımlı**
  - **Etkinleştir** -ağ koruması, sistemdeki tüm kullanıcılar için etkinleştirilmiştir.
  - **Denetim modu** (*varsayılan*)-kullanıcılar tehlikeli etki alanlarından engellenmez ve bunun yerine Windows olayları tetiklenir.

- **USB 'den çalıştırılan güvenilmeyen ve imzasız işlemlerin engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874502)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: b2b3f03d-6A65-4F7B-a9c7-1c7ef74a9ba4
  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Engelle** (*varsayılan*)-bir USB sürücüsünden çalıştırılan güvenilmeyen ve imzasız süreçler engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Windows yerel güvenlik yetkilisi alt sisteminden kimlik bilgisi çalınmasını engelle (lsass.exe)**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=874499)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 9e6c4e1f-7d60-472F-ba1a-a39ef669e4b2
  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Kullanıcı tanımlı**
  - **Etkinleştir** (*varsayılan*)-lsass.exe aracılığıyla kimlik bilgilerini çalmaya çalışır.
  - **Denetim modu** -kullanıcılar tehlikeli etki alanlarından engellenmez ve bunun yerine Windows olayları tetiklenir.

- **E-posta ve Web postasından istemcilerinden yürütülebilir içerik indirmeyi engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Engelle** (*varsayılan*)-e-posta ve web postası istemcilerinden indirilen yürütülebilir içerik engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Tüm Office uygulamalarının alt işlem oluşturmasını engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872976)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Engelle** (*varsayılan*)
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Büyük olasılıkla karıştırılmış betiklerin yürütülmesini engelle (js/vbs/PS)**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872978)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Engelle** (*varsayılan*)-Defender, karıştırılmış betiklerin yürütülmesini engeller.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

- **Office makrolarından Win32 API çağrıları engelle**  
  [Cihazları kötüye bilgisayarlardan koruyun](https://go.microsoft.com/fwlink/?linkid=872977)

  Bu ASR kuralı şu GUID aracılığıyla denetlenir: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Yapılandırılmadı** -Bu ayar, devre dışı olan Windows varsayılan öğesine döner.
  - **Engelle** (*varsayılan*)-Office makrosunda Win32 API çağrıları kullanılması engellenir.
  - **Denetim modu** -Windows olayları engelleme yerine oluşturulur.

## <a name="microsoft-defender-security-center"></a>Microsoft Defender Güvenlik Merkezi

- **Kullanıcıların Exploit Guard Koruma arabirimini düzenlemesini engelle**  
  CSP: [Windowssavunma Dersecuritycenter/Disallowpatıprotectionoverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Evet** (*varsayılan*)-kullanıcıların Microsoft Defender Güvenlik Merkezi 'ndeki yararlanma koruması ayarları alanında değişiklik yapmasını engelleyin.
  - **Yapılandırılmadı** -yerel kullanıcılar, açıktan yararlanma koruması ayarları alanında değişiklik yapabilirler.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

## <a name="smart-screen"></a>Akıllı ekran

::: zone-end
::: zone pivot="atp-sept-2020"

- **Kullanıcıların SmartScreen uyarılarını yoksaymalarını engelleyin**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Bu ayar ' Windows SmartScreen 'i aç ' ayarının Evet olarak ayarlanmasını gerektirir.
  - **Evet** (*varsayılan*)-SmartScreen etkin ve kullanıcılar dosyalar veya kötü amaçlı uygulamalar için uyarıları atlayamaz.
  - **Yapılandırılmadı** -kullanıcılar, dosyalar ve kötü amaçlı uygulamalar için SmartScreen uyarılarını yok sayabilir.

- **Windows SmartScreen 'i açma**  
  CSP: [SmartScreen/Enablesmartscreenınshell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Evet** (*varsayılan*)-tüm kullanıcılar için SmartScreen kullanımını zorunlu tutun.
  - **Yapılandırılmadı** -bu ayarı, SmartScreen 'i etkinleştirmek için Windows varsayılan ' e döndürün, ancak kullanıcılar bu ayarı değiştirebilir. SmartScreen 'i devre dışı bırakmak için özel bir URI kullanın.

- **Microsoft Edge için SmartScreen gerektir**  
  CSP: [tarayıcı/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Evet** (*varsayılan*)-site ve dosya Indirmelerine erişmek Için Microsoft Edge SmartScreen 'i etkinleştirin.
  - **Yapılandırılmadı**

- **Kötü amaçlı Site erişimini engelleyin**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Evet** (*varsayılan*)-kullanıcıların Microsoft Defender SmartScreen Filtresi uyarılarını yoksaymasını ve siteye gitmesini engelleyin.
  - **Yapılandırılmadı**

- **Doğrulanmamış dosya indirmeyi engelle**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Evet** (*varsayılan*)-kullanıcıların Microsoft Defender SmartScreen Filtresi uyarılarını yok saymasını engelleyin ve doğrulanmamış dosyaları indirmelerini engelleyin.
  - **Yapılandırılmadı**

- **Microsoft Defender SmartScreen 'i yapılandırma**  
  Bu ilke yalnızca Microsoft etkin bir etki alanına katılmış Windows örneklerinde kullanılabilir; ya da cihaz yönetimi için kaydedilen Windows 10 Pro veya Enterprise örneklerinde.

  Microsoft Defender SmartScreen, kullanıcılarınızın olası kimlik avı dolandırıcılarından ve kötü amaçlı yazılımlardan korunmasına yardımcı olmak için uyarı iletileri sağlar. Varsayılan olarak, Microsoft Defender SmartScreen açıktır.

  - **Etkin** *(varsayılan)* -Microsoft Defender SmartScreen açık ve kullanıcılar bu özelliği kapatamaz.
  - **Devre dışı** -Microsoft Defender SmartScreen kapalı ve kullanıcılar açamaz.
  - **Yapılandırılmadı** -kullanıcılar Microsoft Defender SmartScreen 'i kullanıp kullanmayacağınızı seçebilirler.

- **Siteler için Microsoft Defender SmartScreen istemlerinin atlanmasını engelle**  
  Bu ilke ayarı, kullanıcıların olası kötü amaçlı Web siteleri hakkında Microsoft Defender SmartScreen uyarılarını geçersiz kılıp kılamayacağını belirlemenize olanak sağlar.

  - **Etkin** *(varsayılan)* -bu ayarı etkinleştirirseniz, kullanıcılar Microsoft Defender SmartScreen uyarılarını yok sayamazlar ve siteye devam etmek engellenir.
  - **Devre dışı** -kullanıcılar Microsoft Defender SmartScreen uyarılarını yoksayabilir ve siteye devam edebilir.
  - **Yapılandırılmadı** - *devre dışı*olarak aynı davranış.

- **İndirmeler hakkında Microsoft Defender SmartScreen uyarılarını atlamayı engelle**  
  Bu ilke, kullanıcıların doğrulanmamış indirmeler hakkında Microsoft Defender SmartScreen uyarılarını geçersiz kılıp kılamayacağını belirlemenizi sağlar.

  - **Etkin** *(varsayılan)* -kuruluşunuzdaki kullanıcılar Microsoft Defender SmartScreen uyarılarını yok sayamazlar ve doğrulanmamış İndirmeleri tamamlamada engellenirler.
  - **Devre dışı** -kullanıcılar Microsoft Defender SmartScreen uyarılarını yoksayabilir ve doğrulanmamış İndirmeleri tamamlayabilir.
  - **Yapılandırılmadı** - *devre dışı*olarak aynı davranış.

- **Microsoft Defender SmartScreen 'i istenmeyebilecek uygulamaları engelleyecek şekilde yapılandırma**  
  Bu ilke yalnızca bir Microsoft Active Directory etki alanına katılmış Windows örneklerinde kullanılabilir; ya da cihaz yönetimi için kaydedilen Windows 10 Pro veya Enterprise örneklerinde.

  Bu ilke ayarı, Microsoft Defender SmartScreen 'te istenmeyebilecek uygulamalar için engellemeyi açıp kullanmayacağınızı yapılandırmanıza olanak tanır. Microsoft Defender SmartScreen 'te istenmeyebilecek uygulama engelleme, kullanıcıların reklam yazılımı, para Miners, Paketleyici, ve Web siteleri tarafından barındırılan diğer düşük ve olmayan uygulamalardan korunmasına yardımcı olmak için uyarı iletileri sağlar. Microsoft Defender SmartScreen 'te istenmeyebilecek uygulama engelleme özelliği varsayılan olarak kapalıdır.

  - **Etkin** *(varsayılan)* -Microsoft Defender SmartScreen 'te istenmeyebilecek uygulama engelleme açıktır.
  - **Devre dışı** -Microsoft Defender SmartScreen 'te istenmeyebilecek uygulama engelleme kapalı.
  - **Yapılandırılmadı** -bu ayarı yapılandırmazsanız, kullanıcılar Microsoft Defender SmartScreen 'te istenmeyebilecek uygulama engellemesinin kullanılıp kullanılmayacağını seçebilirler.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Kullanıcıların SmartScreen uyarılarını yoksaymalarını engelleyin**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Bu ayar ' Windows SmartScreen 'i aç ' ayarının Evet olarak ayarlanmasını gerektirir.
  - **Evet** (*varsayılan*)-SmartScreen etkin ve kullanıcılar dosyalar veya kötü amaçlı uygulamalar için uyarıları atlayamaz.
  - **Yapılandırılmadı** -kullanıcılar, dosyalar ve kötü amaçlı uygulamalar için SmartScreen uyarılarını yok sayabilir.

- **Yalnızca mağaza 'dan uygulama gerektir**  

  - **Evet** (*varsayılan*)
  - **Yapılandırılmadı**

- **Windows SmartScreen 'i açma**  
  CSP: [SmartScreen/Enablesmartscreenınshell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Evet** (*varsayılan*)-tüm kullanıcılar için SmartScreen kullanımını zorunlu tutun.
  - **Yapılandırılmadı** -bu ayarı, SmartScreen 'i etkinleştirmek için Windows varsayılan ' e döndürün, ancak kullanıcılar bu ayarı değiştirebilir. SmartScreen 'i devre dışı bırakmak için özel bir URI kullanın.

## <a name="windows-hello-for-business"></a>İş İçin Windows Hello

Daha fazla bilgi için Windows belgelerindeki [Passportforwork CSP](/windows/client-management/mdm/passportforwork-csp) bölümüne bakın.

- **Iş için Windows Hello 'Yu engelle**  

   Iş için Windows Hello, parolaları, akıllı kartları ve sanal akıllı kartları değiştirerek Windows 'da oturum açmak için alternatif bir yöntemdir.

  - **Yapılandırılmadı** -cihazlar cihaz, Windows için varsayılan olan Iş Için Windows Hello 'Yu temin etmez.
  - **Devre dışı** (*varsayılan*)-cihazlar Iş için Windows Hello 'yu temin edin.
  - **Etkin** -cihazlar herhangi bir kullanıcı için Iş Için Windows Hello 'yu sağlamalardır.

  *Devre dışı*olarak ayarlandığında, aşağıdaki ayarları yapılandırabilirsiniz:

  - **PIN kodunda küçük harfler**  
    - **İzin verilmiyor**
    - **Gerekli**
    - **Izin verilen** (*varsayılan*)

  - **PIN kodunda özel karakterler**
    - **İzin verilmiyor**
    - **Gerekli**
    - **Izin verilen** (*varsayılan*)

  - **PIN kodunda büyük harfler**
    - **İzin verilmiyor**
    - **Gerekli**
    - **Izin verilen** (*varsayılan*)

::: zone-end

## <a name="next-steps"></a>Sonraki adımlar

- [Güvenlik temelleri hakkında bilgi edinin](security-baselines.md)
- [Çakışmaları önleyin](security-baselines.md#avoid-conflicts)
- [Intune'da ilke ve profil sorunları giderme](../configuration/troubleshoot-policies-in-microsoft-intune.md)
