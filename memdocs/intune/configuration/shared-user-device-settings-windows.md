---
title: Windows 10 paylaşılan cihaz ayarları-Microsoft Intune-Azure | Microsoft Docs
description: Paylaşılan veya Microsoft Intune birden çok kullanıcı tarafından kullanılan cihazları yapılandırmak için Windows 10 ' u ekleyin ve kullanın. Microsoft Surface dahil olmak üzere tüm ayarların ve cihazlarda ne yaptıkları hakkında bir liste görürsünüz. Konuk hesaplarını denetleme, hesapları yönetme ve etkin olmayan hesapları silme, yerel depolama alanına kaydetmeye izin verme veya bunu engelleme, güç ve uyku seçeneklerini ayarlama, güncelleştirmelerin ne zaman yükleneceğini seçme ve cihaz yapılandırma profilindeki eğitim ortamlarında cihazları kullanma.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f013074ac67b7622b509d8b9781de3ab5f4041e0
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429501"
---
# <a name="windows-10-and-later-settings-to-manage-shared-devices-using-intune"></a>Intune kullanarak paylaşılan cihazları yönetmek için Windows 10 ve üzeri ayarları

Microsoft yüzeyi gibi Windows 10 ve üzeri cihazlar birçok kullanıcı tarafından kullanılabilir. Birden çok kullanıcısı olan cihazlara paylaşılan cihaz denir ve mobil cihaz yönetimi (MDM) çözümlerinin bir parçasıdır.

Microsoft Intune kullanarak, son kullanıcılar bu paylaşılan cihazlarda Konuk hesabıyla oturum açabilir. Cihaz kullandıkları için, yalnızca izin verilen özelliklere erişim sağlar. Intune Yöneticisi olarak, erişimi yapılandırır, hesapların ne zaman silinmekte olduğunu, güç yönetimi ayarlarını kontrol edin ve paylaşılan Windows 10 cihazlarınız için daha fazlasını yapın.

Bu makalede, bir Windows 10 (ve üzeri) cihaz yapılandırma profilinde kullandığınız ayarlar listelenir ve açıklanmaktadır. Profil Intune 'da oluşturulduğunda, profilinizi kuruluşunuzdaki cihaz gruplarına dağıtır veya atarsınız. Ayrıca, bu profili karma cihaz türleri ve işletim sistemi sürümleri ile cihaz gruplarına da atayabilirsiniz.

Intune 'da bu özellik hakkında daha fazla bilgi için bkz. [PAYLAŞıLAN bilgisayar veya birden çok Kullanıcı cihazlarındaki erişimi, hesapları ve güç özelliklerini denetleme](shared-user-device-settings.md). Windows CSP hakkında daha fazla bilgi için bkz. [Sharedpc CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

## <a name="before-your-begin"></a>Başlamadan önce

[Profili oluşturun](shared-user-device-settings.md).

## <a name="shared-multi-user-device-settings"></a>Paylaşılan çok kullanıcılı cihaz ayarları

Bu ayarlar [Sharedpc CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp)kullanır.

- **PAYLAŞıLAN bilgisayar modu**: **Etkinleştir** ayarı, paylaşılan bilgisayar modunu etkinleştirir. Bu modda, tek seferde cihazda yalnızca bir Kullanıcı oturum açar. Birinci Kullanıcı oturumu kapatana kadar başka bir Kullanıcı oturum açamaz. **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.
- **Konuk hesabı**: oturum açma ekranında Konuk seçeneği oluşturmayı seçin. Konuk hesapları için Kullanıcı kimlik bilgileri veya kimlik doğrulaması gerekmez. Bu ayar her kullanıldığında yeni bir yerel hesap oluşturur. Seçenekleriniz şunlardır:
  - **Konuk**: cihazda yerel olarak bir Konuk hesabı oluşturur.
  - **Etki alanı**: Azure ACTIVE DIRECTORY (ad) içinde bir Konuk hesabı oluşturur.
  - **Konuk ve etki alanı**: cihazda yerel olarak bir Konuk hesabı oluşturur ve Azure ACTIVE DIRECTORY (ad).
- **Hesap yönetimi**: hesapların otomatik olarak silinip silinmediğini seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Etkin**: konuklar tarafından oluşturulan hesaplar ve ad ve Azure AD 'de hesaplar otomatik olarak silinir. Kullanıcı cihazda oturumu kapattığında veya sistem bakımı çalıştırıldığında, bu hesaplar silinir.

    Şunları da girin:

    - **Hesap silme**: hesapların ne zaman silineceğini seçin:
      - **Depolama alanı eşiğine göre**
      - **Depolama alanı eşiği ve etkin olmayan eşik**
      - **Oturum kapatıldıktan hemen sonra**

    Şunları da girin:

    - **Delete eşiğini Başlat (%)**: disk alanı yüzdesi (0-100) girin. Toplam disk/depolama alanı girdiğiniz değerin altına düştüğünde, önbelleğe alınmış hesaplar silinir. Disk alanı kazanmak için hesapları sürekli olarak siler. En uzun devre dışı olan hesaplar önce silinir.
    - **Silme eşiğini Durdur (%)**: disk alanı yüzdesi (0-100) girin. Toplam disk/depolama alanı girdiğiniz değeri karşılıyorsa, silme işlemini sonlandırır.
    - **Etkin olmayan hesap eşiği**: 0-60 günden itibaren, oturum açmamış hesabı silmeden önce ardışık gün sayısını girin.

  - **Devre dışı**: konuklar tarafından oluşturulan yerel, ad ve Azure AD hesapları cihazda kalır ve silinmez.

- **Yerel depolama**: yerel depolama ile, kullanıcılar cihazın sabit sürücüsündeki dosyaları kaydedebilir ve görüntüleyebilir. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Etkin**: kullanıcıların cihazın sabit sürücüsündeki dosyaları kaydetmesini ve görüntülemesini engeller.
  - **Devre dışı**: kullanıcıların dosya Gezgini 'ni kullanarak yerel olarak dosya görüp kaydetmesine izin verir.

- **Güç ilkeleri**: kullanıcıların güç ayarlarını değiştirmesini sağlar veya engelleyin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Etkin**: kullanıcılar hazırda beklemeyi kapatamaz, tüm uyku işlemlerini geçersiz kılamazsınız (kapağı kapatma gibi) ve güç ayarlarını değiştiremezler.
  - **Devre dışı**: kullanıcılar cihazı hazırda beklemeye alabilir, cihazı uyku moduna almak için kapağı kapatabilir ve güç ayarlarını değiştirebilir.

- **Uyku zaman aşımı (saniye cinsinden)**: Cihaz uyku moduna geçmeden önce etkin olmayan saniyeler (0-18000) sayısını girin. `0`, cihazın hiçbir şekilde uyku moduna geçme anlamına gelir. Bir zaman ayarlamazsanız, cihaz 3600 saniye (60 dakika) sonra uyku moduna geçer.

- **Bilgisayar uyandığında oturum açma**: Cihaz uyku modundan çıktıktan sonra kullanıcıların oturum açması gerekiyorsa seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Etkin**: Cihaz uyku modundan geldiği zaman kullanıcıların bir parolayla oturum açmasını gerektirir.
  - **Devre dışı**: kullanıcıların kullanıcı adını ve parolasını girmesi gerekmez.

- **Bakım başlangıç zamanı (gece yarısından itibaren dakika)**: Windows Update, gibi otomatik bakım görevleri çalıştırıldığında, dakika cinsinden süreyi (0-1440) girin. Varsayılan başlangıç saati gece yarısı veya sıfır ( `0` ) dakikadır. Başlangıç saatini, gece yarısından dakikalar içinde bir başlangıç saati girerek değiştirin. Örneğin, bakımın 2 ' de başlamasını istiyorsanız, girin `120` . Bakımın 8 PM 'de başlamasını istiyorsanız girin `1200` .

  **Yapılandırılmadı** (varsayılan) olarak ayarlandığında, Intune bu ayarı değiştirmez veya güncelleştirmez.

- **Eğitim ilkeleri**: eğitim ortamı ilkelerinin etkinleştirilip etkinleştirilmeyeceğini seçin. Seçenekleriniz şunlardır:
  - **Yapılandırılmadı** (varsayılan): Intune bu ayarı değiştirmez veya güncelleştirmez.
  - **Etkin**: okulda kullanılan ve daha kısıtlayıcı olan cihazlar için önerilen ayarları kullanır.
  - **Devre dışı**: varsayılan ve önerilen eğitim ilkeleri kullanılmaz.

  Eğitim ilkelerinin ne yaptığı hakkında daha fazla bilgi için bkz. [Eğitim müşterileri Için Windows 10 yapılandırma önerileri](https://docs.microsoft.com/education/windows/configure-windows-for-education).

> [!TIP]
> [Paylaşılan veya Konuk BIR bilgisayar ayarlama](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (başka bir Belgeler Web sitesini açar), paylaşılan modda ayarlanulabilecek kavramlar ve grup ilkeleri de dahil olmak üzere bu Windows 10 özelliğindeki harika bir kaynaktır.

## <a name="next-steps"></a>Sonraki adımlar

- [Profili atama](device-profile-assign.md) ve [durumunu izleme](device-profile-monitor.md).
- Bkz. [Windows holographic for Business](shared-user-device-settings-windows-holographic.md)için ayarlar.
