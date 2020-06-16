---
title: Microsoft Intune - Azure ile cihaz ayrıntılarını görüntüleme | Microsoft Docs
description: İşletim sistemleri, depolama alanı, üretim ve modeli içeren cihaz ayrıntılarınızı görüntüleyin. Azure'da Microsoft Intune ile yüklü uygulamaların bir listesini alın, uyumluluk ilkelerini denetleyin ve TeamViewer'ı ayarlayın. Bu, yönettiğiniz cihazların envanterini görüntülemeye benzer.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 27d31e64e99e8dc796b0436052f7220260ab1029
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795678"
---
# <a name="see-device-details-in-intune"></a>Intune'da cihaz ayrıntılarına bakın

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**Cihazlar** özelliği, yönettiğiniz cihazlara donanım ve yüklü uygulamalar dahil ek ayrıntılar sağlar.

Bu makalede, tüm cihazlarınızı ve özelliklerini Azure portalında nasıl görüntüleyeceğiniz gösterilir.

## <a name="view-the-device-details"></a>Cihaz ayrıntılarını görüntüleme

1. [Microsoft Endpoint Manager Yönetim merkezinde](https://go.microsoft.com/fwlink/?linkid=2109431)oturum açın.
3. **Cihazlar**  >  **tüm cihazlar** ' ı seçin > listelenen cihazlarınızdan birini seçerek ayrıntılarını açın:

   - **Genel bakış** cihaz adını gösterir ve cihazın kişisel veya kurumsal bir cihaz, seri numarası, birincil kullanıcı ve daha fazlası gibi bazı temel özelliklerini listeler. Cihazda şunları yapabilirsiniz:
      - [Devre dışı bırak](devices-wipe.md#retire)
      - [Silme](devices-wipe.md#wipe)
      - [Sil](devices-wipe.md#delete-devices-from-the-intune-portal)
      - [Uzaktan kilitleme](device-remote-lock.md)
      - [Eşitle](device-sync.md)
      - [Geçiş kodunu sıfırla](device-passcode-reset.md)
      - [Yeniden başlatma](device-restart.md) (yalnızca Windows)
      - [Yeni başlangıç](device-fresh-start.md) (yalnızca Windows)
      - [Autopilot sıfırlaması](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (yalnızca Windows)
      - [Hızlı tarama](../configuration/device-restrictions-windows-10.md) (yalnızca Windows 10)
      - [Tam tarama](../configuration/device-restrictions-windows-10.md) (yalnızca Windows 10)
      - [Windows Defender güvenlik zekası 'nı güncelleştirme](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/manage-protection-updates-microsoft-defender-antivirus)
      - [BitLocker anahtar döndürme](https://docs.microsoft.com/mem/intune/protect/encrypt-devices#to-rotate-the-bitlocker-recovery-key)
      - [Cihazı yeniden adlandırma](device-rename.md)
      - [Yeni Uzaktan Yardım oturumu](https://docs.microsoft.com/mem/intune/remote-actions/teamviewer-support)
   - **Özellikler**’i kullanarak [oluşturduğunuz bir cihaz kategorisini](../enrollment/device-group-mapping.md) atayabilir ve cihazın sahipliğini kişisel veya şirket olarak değiştirebilirsiniz.
   - **Donanım** cihaz kimliği, işletim sistemi ve sürümü, depolama alanı ve daha fazla ayrıntı gibi cihazla ilgili birçok ayrıntıyı içerir.
   - **Bulunan uygulamalar**, Intune’un cihazda yüklü olduğunu bulduğu tüm uygulamaları ve uygulama sürümlerini listeler. Daha fazla bilgi için bkz. [Intune bulunan uygulamalar](../apps/app-discovered-apps.md).
   - **Cihaz uyumluluğu**, atanmış tüm uyumluluk ilkelerini ve cihazın uyumlu olup olmadığını listeler.
   - **Cihaz yapılandırması**, cihaza atanmış tüm yapılandırma ilkelerini ve ilkenin başarılı olup olmadığını gösterir.
   - **Uygulama yapılandırması** 
   - **Uç nokta güvenlik yapılandırması**
   - **Kurtarma anahtarları** , cihaz için bulunan kullanılabilir BitLocker anahtarlarını gösterir
   - **Yönetilen uygulamalar** , Intune 'un yapılandırdığı ve cihaza dağıttığındaki tüm yönetilen uygulamaları listeler. 

## <a name="hardware-device-details"></a>Donanım cihazı durumu
Cihazlar tarafından kullanılan taşıyıcıya bağlı olarak, tüm ayrıntılar toplanmayabilir

> [!Note]  
> Donanım ve yazılım envanteri, Intune hizmetinde her 7 günde bir yenilenir.

|Ayrıntı|Açıklama|Platform| 
|--------------|----------------------|----|  
|Name|Cihazın adı.|Windows, iOS|
|Yönetim adı|Yalnızca konsolda kullanılan cihaz adı. Bu adın değiştirilmesi, cihazdaki adı değiştirmez.|Windows, iOS|
|UDID|Cihazın Benzersiz Cihaz tanımlayıcısı.|Windows, iOS|
|Intune Cihaz Kimliği|Cihazı benzersiz şekilde tanımlayan GUID.|Windows, iOS|
|Seri numarası|Üreticisinden cihazın seri numarası.|Windows, iOS|
|Paylaşılan cihaz|**Evet** ise cihaz birden fazla kullanıcı tarafından paylaşılır.|Windows, iOS|
|Kullanıcı onaylı kayıt|Yanıt **Evet**ise, cihazın cihazdaki belirli güvenlik ayarlarını yönetmesine olanak tanıyan Kullanıcı onaylı kaydı vardır.|Windows, iOS|
|İşletim sistemi|Cihazda kullanılan işletim sistemi.|Windows, iOS|
|İşletim sistemi sürümü|Cihazdaki işletim sistemi sürümü.|Windows, iOS|
|İşletim sistemi dili|Cihazdaki işletim sisteminin dil kümesi.|Windows, iOS|
|Yapı numarası|İşletim sisteminin yapı numarası.|Android|
|Güvenlik Düzeltme eki düzeyi|Cihaz için güvenlik düzeltme eki düzeyi.|Android|
|Toplam depolama alanı|Cihazdaki toplam depolama alanı (gigabayt olarak).|Windows, iOS|
|Boş depolama alanı|Cihazdaki kullanılmayan depolama alanı (gigabayt olarak).|Windows, iOS|
|IMEI|Cihazın Uluslararası Mobil Ekipman Tanımlayıcısı.|Windows, iOS/ıpados, Android|
|MEID|Cihazın mobil ekipman tanımlayıcısı.|Windows, iOS/ıpados, Android|
|Üretici|Cihazın üreticisi.|Windows, iOS/ıpados, Android|
|Model|Cihazın modeli.|Windows, iOS/ıpados, Android|
|Telefon numarası|Cihaza atanan telefon numarası.|Windows, iOS/ıpados, Android *|
|Abone operatör|Cihazın kablosuz operatörü.|Windows, iOS/ıpados, Android|
|Hücresel teknoloji|Cihaz tarafından kullanılan radyo sistemi.|Windows, iOS/ıpados, Android|
|Wi-Fi MAC|Cihazın Ortam Erişim Denetimi adresi.|Windows, iOS/ıpados, Android|
|ICCID|Entegre Devre Kart Tanımlayıcısı, yani bir SIM kartın benzersiz kimlik numarası.|Windows, iOS/ıpados, Android|
|Kaydolma tarihi|Cihazın Intune’a kaydedildiği tarih ve saat.|Windows, iOS/ıpados, Android|
|Son iletişim|Cihazın Intune’a son bağlandığı tarih ve saat.|Windows, iOS/ıpados, Android|
|Etkinleştirme kilidi atlama kodu|Etkinleştirme kilidini devre dışı bırakmak için kullanılan kod.|iOS|
|Azure AD kayıtlı|**Evet** ise cihaz Azure Directory’ye kayıtlıdır.|Windows, iOS/ıpados, Android|
|Intune kayıtlı|Yanıt **Evet**ise, cihaz Intune 'a kaydedilir|Windows, iOS/ıpados, Android|
|Uyumluluk|Cihazın uyumluluk durumu.|Windows, iOS/ıpados, Android|
|EAS etkin|**Evet** ise cihaz Exchange posta kutusu ile eşitlenir.|Windows, iOS/ıpados, Android|
|EAS etkinleştirme kimliği|Cihazın Exchange ActiveSync tanımlayıcısı.|Windows, iOS/ıpados, Android|
|Denetimli|**Evet** ise yöneticiler cihaz üzerinde gelişmiş denetime sahiptir.|Windows, iOS/ıpados, Android|
|Şifreli|**Evet** ise cihazda depolanan veriler şifrelenir.|Windows, iOS/ıpados, Android|

> [!Note]  
> Telefon numarası, Android kurumsal adanmış veya tam olarak yönetilen cihazlarda envantere kaydedilmiş değildir.

## <a name="next-steps"></a>Sonraki adımlar
Intune ile [cihazlarınızı yönetmek](device-management.md) için başka neler yapabileceğinizi görün.
